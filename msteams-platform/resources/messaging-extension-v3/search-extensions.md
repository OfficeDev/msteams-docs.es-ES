---
title: Buscar con extensiones de mensajería
description: Describe cómo desarrollar extensiones de mensajería basadas en búsquedas
keywords: búsqueda de extensiones de mensajería de Team Extensions
ms.date: 07/20/2019
ms.openlocfilehash: f46548d2e7e03ecebd8bc0fb6685aeb82b8eec6e
ms.sourcegitcommit: 0aeb60027f423d8ceff3b377db8c3efbb6da4d17
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/11/2020
ms.locfileid: "48998003"
---
# <a name="search-with-messaging-extensions"></a>Buscar con extensiones de mensajería

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Las extensiones de mensajería basadas en búsquedas le permiten consultar su servicio y enviar la información en forma de una tarjeta, directamente en su mensaje.

![Ejemplo de tarjeta de extensión de mensajería](~/assets/images/compose-extensions/ceexample.png)

En las secciones siguientes se describe cómo hacerlo.

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="search-type-message-extensions"></a>Extensiones de mensajes de tipo de búsqueda

Para la extensión de mensajería basada en búsquedas establezca el `type` parámetro en `query` . A continuación se muestra un ejemplo de un manifiesto con un único comando de búsqueda. Una sola extensión de mensajería puede tener hasta 10 comandos diferentes asociados a ella. Esto puede incluir varios comandos de búsqueda y varios basados en acciones.

#### <a name="complete-app-manifest-example"></a>Ejemplo de manifiesto de aplicación completo

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.bing",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://bingbotservice.azurewebsites.net/",
    "privacyUrl": "http://bingbotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://bingbotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "Bing",
    "full": "Bing"
  },
  "description": {
    "short": "Find Bing search results",
    "full": "Find Bing search results and share them with your team members."
  },
  "icons": {
    "outline": "bing-outline.jpg",
    "color": "bing-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [{
          "id": "searchCmd",
          "description": "Search Bing for information on the web",
          "title": "Search",
          "initialRun": true,
          "parameters": [{
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "bingbotservice.azurewebsites.net",
    "*.bingbotservice.azurewebsites.net"
  ]
}
```

### <a name="test-via-uploading"></a>Prueba mediante carga

Puede probar la extensión de mensajería cargando la aplicación.

Para abrir la extensión de mensajería, navegue a cualquiera de sus chats o canales. Elija el botón **más opciones** ( **&#8943;** ) en el cuadro de redacción y elija su extensión de mensajería.

## <a name="add-event-handlers"></a>Agregar controladores de eventos

La mayor parte de su trabajo implica el `onQuery` evento, que controla todas las interacciones en la ventana de la extensión de mensajería.

Si establece en `canUpdateConfiguration` `true` en el manifiesto, habilita el elemento de menú **configuración** para la extensión de mensajería y también debe controlar `onQuerySettingsUrl` y `onSettingsUpdate` .

### <a name="handle-onquery-events"></a>Controlar eventos de consulta

Una extensión de mensajería recibe un `onQuery` evento cuando ocurre algo en la ventana de la extensión de mensajería o se envía a la ventana.

Si su extensión de mensajería usa una página de configuración, el controlador para `onQuery` debe comprobar primero si hay información de configuración almacenada; si la extensión de mensajería no está configurada, devuelva una `config` respuesta con un vínculo a la página de configuración. Tenga en cuenta que la respuesta de la página de configuración también se controla mediante `onQuery` . (La única excepción es cuando el controlador llama a la página de configuración de `onQuerySettingsUrl` ; Consulte la sección siguiente).

Si su extensión de mensajería requiere autenticación, Compruebe la información de estado del usuario; Si el usuario no ha iniciado sesión, siga las instrucciones de la sección [autenticación](#authentication) más adelante en este tema.

A continuación, compruebe si `initialRun` está establecido; si es así, realice las acciones adecuadas, como proporciona instrucciones o una lista de respuestas.

El resto del controlador para `onQuery` solicita información al usuario, muestra una lista de tarjetas de vista previa y devuelve la tarjeta seleccionada por el usuario.

### <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a>Controlar eventos onQuerySettingsUrl y onSettingsUpdate

Los `onQuerySettingsUrl` `onSettingsUpdate` eventos y funcionan de forma conjunta para habilitar el elemento de menú **configuración** .

![Capturas de pantallas de ubicaciones del elemento de menú configuración](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

El controlador para `onQuerySettingsUrl` devuelve la dirección URL de la página de configuración; una vez que se cierra la página de configuración, el controlador para `onSettingsUpdate` acepta y guarda el estado devuelto. (Este es el caso en el que `onQuery` *no* recibe la respuesta de la página de configuración.)

## <a name="receive-and-respond-to-queries"></a>Recibir y responder a consultas

Cada solicitud a su extensión de mensajería se realiza a través de un `Activity` objeto que se publica en la dirección URL de devolución de llamada. La solicitud contiene información sobre el comando de usuario, como los valores ID y Parameter. La solicitud también proporciona metadatos sobre el contexto en el que se ha invocado la extensión, incluidos el identificador de usuario y de inquilino, junto con el identificador de chat o los identificadores de canal y de equipo.

### <a name="receive-user-requests"></a>Recibir solicitudes de usuario

Cuando un usuario realiza una consulta, Microsoft Teams envía al servicio un objeto de .NET Framework estándar `Activity` . El servicio debe realizar su lógica para un `Activity` que tenga `type` establecido en `invoke` y `name` establecido en un tipo admitido `composeExtension` , como se muestra en la siguiente tabla.

Además de las propiedades de actividad de bot estándar, la carga contiene los siguientes metadatos de solicitud:

|Nombre de propiedad|Finalidad|
|---|---|
|`type`| Tipo de solicitud; debe ser `invoke` . |
|`name`| Tipo de comando que se emite para el servicio. Actualmente se admiten los siguientes tipos: <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| IDENTIFICADOR del usuario que envió la solicitud. |
|`from.name`| Nombre del usuario que envió la solicitud. |
|`from.aadObjectId`| Identificador de objeto de Azure Active Directory del usuario que envió la solicitud. |
|`channelData.tenant.id`| Identificador del inquilino de Azure Active Directory |
|`channelData.channel.id`| IDENTIFICADOR de canal (si la solicitud se realizó en un canal). |
|`channelData.team.id`| IDENTIFICADOR del equipo (si la solicitud se realizó en un canal). |
|`clientInfo`|Metadatos opcionales sobre el software de cliente que se usa para enviar un mensaje de un usuario. La entidad puede contener dos propiedades:<br>El `country` campo contiene la ubicación detectada del usuario.<br>El `platform` campo describe la plataforma de cliente de mensajería. <br>Para obtener más información, *vea* [tipos de entidades que no son IRI — clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).|

Los propios parámetros de la solicitud se encuentran en el objeto de valor, que incluye las siguientes propiedades:

| Nombre de propiedad | Finalidad |
|---|---|
| `commandId` | Nombre del comando invocado por el usuario, que coincide con uno de los comandos declarados en el manifiesto de la aplicación. |
| `parameters` | Matriz de parámetros. Cada objeto Parameter contiene el nombre del parámetro, junto con el valor del parámetro proporcionado por el usuario. |
| `queryOptions` | Parámetros de paginación: <br>`skip`: recuento de omitidos para esta consulta <br>`count`: número de elementos que se devolverá |

#### <a name="request-example"></a>Ejemplo de solicitud

```json
{
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "searchKeywords",
        "value": "Toronto"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  "type": "invoke",
  "timestamp": "2017-05-01T15:45:51.876Z",
  "localTimestamp": "2017-05-01T08:45:51.876-07:00",
  "id": "f:622749630322482883",
  "channelId": "msteams",
  "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
  "from": {
    "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
    "name": "Larry Jin",
    "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
  },
  "conversation": {
    "id": "19:skypespaces_8198cfe0dd2647ae91930f0974768a40@thread.skype"
  },
  "recipient": {
    "id": "28:b4922ea1-5315-4fd0-9b21-d941ab06e39f",
    "name": "TheComposeExtensionDev"
  },
  "entities": [
    {
    "type": "clientInfo",
      "country": "US",
      "platform": "Windows"
    }
  ]
}
```

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a>Recibir solicitudes de vínculos insertados en el cuadro de mensaje de redacción

Como alternativa (o adicional), a la búsqueda en el servicio externo, puede usar una dirección URL insertada en el cuadro de mensaje de redacción para consultar su servicio y devolver una tarjeta. En la captura de pantalla siguiente, un usuario ha pegado en una dirección URL de un elemento de trabajo en Azure DevOps que la extensión de mensajería se ha resuelto en una tarjeta.

![Ejemplo de vínculo unfurling](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

Para habilitar la extensión de mensajería para que interactúe con los vínculos de esta forma, primero tendrá que agregar la `messageHandlers` matriz al manifiesto de la aplicación, como en el ejemplo siguiente:

```json
"composeExtensions": [
  {
    "botId": "abc123456-ab12-ab12-ab12-abcdef123456",
    "messageHandlers": [
      {
        "type": "link",
        "value": {
          "domains": [
            "*.trackeddomain.com"
          ]
        }
      }
    ]
  }
]
```

Una vez que haya agregado el dominio para escuchar en el manifiesto de la aplicación, deberá cambiar el código de bot para [responder](#respond-to-user-requests) a la siguiente solicitud de invocación.

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

Si la aplicación devuelve varios elementos solo se usará el primero.

### <a name="respond-to-user-requests"></a>Responder a solicitudes de usuario

Cuando el usuario realiza una consulta, Microsoft Teams emite una solicitud HTTP sincrónica a su servicio. En ese momento, el código tiene 5 segundos para proporcionar una respuesta HTTP a la solicitud. Durante este tiempo, el servicio puede realizar búsquedas adicionales o cualquier otra lógica empresarial necesaria para atender la solicitud.

El servicio debe responder con los resultados que coincidan con la consulta de usuario. La respuesta debe indicar un código de Estado HTTP de `200 OK` y un objeto Application/JSON válido con el siguiente cuerpo:

|Nombre de propiedad|Finalidad|
|---|---|
|`composeExtension`|Sobre de respuesta de nivel superior.|
|`composeExtension.type`|Tipo de respuesta. Se admiten los siguientes tipos: <br>`result`: muestra una lista de los resultados de la búsqueda <br>`auth`: pide al usuario que se autentique <br>`config`: pide al usuario que configure la extensión de mensajería. <br>`message`: muestra un mensaje de texto sin formato |
|`composeExtension.attachmentLayout`|Especifica el diseño de los datos adjuntos. Se usa para las respuestas de tipo `result` . <br>Actualmente se admiten los siguientes tipos: <br>`list`: una lista de objetos Card que contiene miniaturas, títulos y campos de texto <br>`grid`: una cuadrícula de imágenes en miniatura |
|`composeExtension.attachments`|Matriz de objetos Attachment válidos. Se usa para las respuestas de tipo `result` . <br>Actualmente se admiten los siguientes tipos: <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|Acciones sugeridas. Se usa para las respuestas de tipo `auth` o `config` . |
|`composeExtension.text`|Mensaje que se va a mostrar. Se usa para las respuestas de tipo `message` . |

#### <a name="response-card-types-and-previews"></a>Tipos y vistas previas de las tarjetas de respuesta

Se admiten los siguientes tipos de datos adjuntos:

* [Tarjeta en miniatura](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Tarjeta Hero](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Tarjeta de conector de Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Tarjeta adaptable](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Consulte las [tarjetas](~/task-modules-and-cards/what-are-cards.md) para obtener información general.

Para obtener información sobre cómo usar los tipos de tarjetas en miniatura y Heroes, consulte [Add Cards and Card Actions](~/task-modules-and-cards/cards/cards-actions.md).

Para obtener documentación adicional sobre la tarjeta de conector de Office 365, consulte [using office 365 Connector Cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).

La lista de resultados se muestra en la interfaz de usuario de Microsoft Teams con una vista previa de cada elemento. La vista previa se genera de una de estas dos maneras:

* Uso de la `preview` propiedad en el `attachment` objeto. El `preview` archivo adjunto solo puede ser un héroe o una tarjeta de miniaturas.
* Se extraen de `title` las `text` propiedades Basic, y `image` de los datos adjuntos. Solo se usan si la `preview` propiedad no está establecida y estas propiedades están disponibles.

Puede mostrar una vista previa de una tarjeta de conector de Office 365 adaptable en la lista de resultados simplemente estableciendo su propiedad Preview; Esto no es necesario si los resultados ya son un héroe o tarjetas en miniatura. Si usa la vista previa de datos adjuntos, debe ser un héroe o una tarjeta en miniatura. Si no se especifica ninguna propiedad de vista previa, se producirá un error en la vista previa de la tarjeta y no se mostrará nada.

#### <a name="response-example"></a>Ejemplo de respuesta

En este ejemplo se muestra una respuesta con dos resultados, mezclando distintos formatos de tarjeta: conector de Office 365 y adaptable. Aunque es probable que desee ceñirse a un formato de tarjeta en la respuesta, muestra cómo la `preview` propiedad de cada elemento de la `attachments` colección debe definir explícitamente una vista previa en el formato de héroe o miniatura, como se ha descrito anteriormente.

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "attachments": [
      {
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage": "https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value": "[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        }
      },
      {
        "contentType": "application/vnd.microsoft.card.adaptive",
        "content": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Container",
              "items": [
                {
                  "type": "TextBlock",
                  "text": "Microsoft Corp (NASDAQ: MSFT)",
                  "size": "medium",
                  "isSubtle": true
                },
                {
                  "type": "TextBlock",
                  "text": "September 19, 4:00 PM EST",
                  "isSubtle": true
                }
              ]
            },
            {
              "type": "Container",
              "spacing": "none",
              "items": [
                {
                  "type": "ColumnSet",
                  "columns": [
                    {
                      "type": "Column",
                      "width": "stretch",
                      "items": [
                        {
                          "type": "TextBlock",
                          "text": "75.30",
                          "size": "extraLarge"
                        },
                        {
                          "type": "TextBlock",
                          "text": "▼ 0.20 (0.32%)",
                          "size": "small",
                          "color": "attention",
                          "spacing": "none"
                        }
                      ]
                    },
                    {
                      "type": "Column",
                      "width": "auto",
                      "items": [
                        {
                          "type": "FactSet",
                          "facts": [
                            {
                              "title": "Open",
                              "value": "62.24"
                            },
                            {
                              "title": "High",
                              "value": "62.98"
                            },
                            {
                              "title": "Low",
                              "value": "62.20"
                            }
                          ]
                        }
                      ]
                    }
                  ]
                }
              ]
            }
          ],
          "version": "1.0"
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "Microsoft Corp (NASDAQ: MSFT)",
            "text": "75.30 ▼ 0.20 (0.32%)"
          }
        }
      }
    ]
  }
}
```

### <a name="default-query"></a>Consulta predeterminada

Si establece en `initialRun` `true` en el manifiesto, Microsoft Teams emite una consulta "predeterminada" cuando el usuario abre por primera vez la extensión de mensajería. El servicio puede responder a esta consulta con un conjunto de resultados rellenados previamente. Esto puede ser útil para mostrar, por ejemplo, elementos vistos recientemente, favoritos o cualquier otra información que no dependa de los datos proporcionados por el usuario.

La consulta predeterminada tiene la misma estructura que cualquier consulta de usuario normal, excepto con un parámetro `initialRun` cuyo valor de cadena es `true` .

#### <a name="request-example-for-a-default-query"></a>Ejemplo de solicitud de una consulta predeterminada

```json
{
  "type": "invoke",
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "initialRun",
        "value": "true"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  ⋮
}
```

## <a name="identify-the-user"></a>Identificar al usuario

Todas las solicitudes a los servicios incluyen el identificador ofuscado del usuario que realizó la solicitud, así como el nombre para mostrar del usuario y el identificador de objeto de Azure Active Directory.

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

`id` `aadObjectId` Se garantiza que los valores y son los del usuario de Teams autenticado. Se pueden usar como claves para buscar credenciales o cualquier estado almacenado en la memoria caché del servicio. Además, cada solicitud contiene el identificador de inquilino de Azure Active Directory del usuario, que se puede usar para identificar la organización del usuario. Si procede, la solicitud también contiene los identificadores de equipo y de canal desde los que se originó la solicitud.

## <a name="authentication"></a>Autenticación

Si su servicio requiere la autenticación del usuario, debe iniciar sesión en el usuario antes de que pueda usar la extensión de mensajería. Si ha escrito un bot o una pestaña que inicia sesión en el usuario, esta sección debería resultarle familiar.

La secuencia es la siguiente:

1. El usuario emite una consulta o se envía automáticamente la consulta predeterminada a su servicio.
2. El servicio comprueba si el usuario se ha autenticado primero mediante la inspección del identificador de usuario de Teams.
3. Si el usuario no se ha autenticado, vuelva a enviar una `auth` respuesta con una `openUrl` acción sugerida que incluya la dirección URL de autenticación.
4. El cliente de Microsoft Teams inicia una ventana emergente que hospeda la página web con la dirección URL de autenticación especificada.
5. Después de que el usuario inicie sesión, debe cerrar la ventana y enviar un "código de autenticación" al cliente de Teams.
6. A continuación, el cliente de Microsoft Teams envía la consulta a su servicio, que incluye el código de autenticación pasado en el paso 5.

El servicio debe comprobar que el código de autenticación recibido en el paso 6 coincida con el del paso 5. Esto garantiza que un usuario malintencionado no intente imitar ni poner en peligro el flujo de inicio de sesión. De hecho, "cierra el bucle" para finalizar la secuencia de autenticación segura.

### <a name="respond-with-a-sign-in-action"></a>Responder con una acción de inicio de sesión

Para solicitar a un usuario no autenticado que inicie sesión, responda con una acción sugerida de tipo `openUrl` que incluya la dirección URL de autenticación.

#### <a name="response-example-for-a-sign-in-action"></a>Ejemplo de respuesta de una acción de inicio de sesión

```json
{
  "composeExtension":{
    "type":"auth",
    "suggestedActions":{
      "actions":[
        {
          "type": "openUrl",
          "value": "https://example.com/auth",
          "title": "Sign in to this app"
        }
      ]
    }
  }
}
```

> [!NOTE]
> Para que la experiencia de inicio de sesión se hospede en una ventana emergente de Teams, la parte de dominio de la dirección URL debe estar en la lista de dominios válidos de la aplicación. (Vea [validDomains](~/resources/schema/manifest-schema.md#validdomains) en el esquema del manifiesto).

### <a name="start-the-sign-in-flow"></a>Iniciar el flujo de inicio de sesión

La experiencia de inicio de sesión debe ser eficaz y ajustarse en una ventana emergente. Debe integrarse con el [SDK cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client), que usa el paso de mensajes.

Al igual que con otras experiencias incrustadas que se ejecutan dentro de Microsoft Teams, el código dentro de la ventana debe llamar primero `microsoftTeams.initialize()` . Si el código realiza un flujo de OAuth, puede pasar el identificador de usuario de Teams a la ventana, que puede pasarla a la dirección URL de inicio de sesión de OAuth.

### <a name="complete-the-sign-in-flow"></a>Completar el flujo de inicio de sesión

Cuando la solicitud de inicio de sesión se completa y redirige de nuevo a la página, debe realizar los siguientes pasos:

1. Generar un código de seguridad. (Puede ser un número aleatorio). Debe almacenar en caché este código en el servicio, junto con las credenciales obtenidas a través del flujo de inicio de sesión (por ejemplo, los tokens 2,0 de OAuth).
2. Llamar `microsoftTeams.authentication.notifySuccess` y pasar el código de seguridad.

En este momento, la ventana se cierra y el control se pasa al cliente de Teams. El cliente ahora puede volver a emitir la consulta de usuario original, junto con el código de seguridad de la `state` propiedad. El código puede usar el código de seguridad para buscar las credenciales almacenadas anteriormente para completar la secuencia de autenticación y, a continuación, completar la solicitud del usuario.

#### <a name="reissued-request-example"></a>Ejemplo de solicitud reemitiendo

```json
{
    "name": "composeExtension/query",
    "value": {
        "commandId": "insertWiki",
        "parameters": [{
            "name": "searchKeyword",
            "value": "lakers"
        }],
        "state": "12345",
        "queryOptions": {
            "skip": 0,
            "count": 25
        }
    },
    "type": "invoke",
    "timestamp": "2017-04-26T05:18:25.629Z",
    "localTimestamp": "2017-04-25T22:18:25.629-07:00",
    "entities": [{
        "type": "clientInfo",
        "country": "US",
        "platform": "Web",
        
    }],
    "text": "",
    "attachments": [],
    "address": {
        "id": "f:7638210432489287768",
        "channelId": "msteams",
        "user": {
            "id": "29:1A5TJWHkbOwSyu_L9Ktk9QFI1d_kBOEPeNEeO1INscpKHzHTvWfiau5AX_6y3SuiOby-r73dzHJ17HipUWqGPgw",
            "aadObjectId": "fc8ca1c0-d043-4af6-b09f-141536207403"
        },
        "conversation": {
            "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
        },
        "bot": {
            "id": "28:c073afa8-7e77-4f92-b3e7-aa589e952a3e",
            "name": "maotestbot2"
        },
        "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
        "useAuth": true
    },
    "source": "msteams"
}
```

## <a name="sdk-support"></a>Compatibilidad con SDK

### <a name="net"></a>.NET

Para recibir y controlar consultas con el SDK de bot Builder para .NET, puede comprobar el `invoke` tipo de acción en la actividad entrante y, a continuación, usar el método auxiliar en el paquete NuGet [Microsoft. bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) para determinar si se trata de una actividad de extensión de mensajería.

#### <a name="example-code-in-net"></a>Código de ejemplo en .NET

```csharp
public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
{
    if (activity.Type == ActivityTypes.Invoke) // Received an invoke
    {
        if (activity.IsComposeExtensionQuery())
        {
            // This is the response object that will get sent back to the messaging extension request.
            ComposeExtensionResponse invokeResponse = null;

            // This helper method gets the query as an object.
            var query = activity.GetComposeExtensionQueryData();

            if (query.CommandId != null && query.Parameters != null && query.Parameters.Count > 0)
            {
                // query.Parameters has the parameters sent by client
                var results = new ComposeExtensionResult()
                {
                    AttachmentLayout = "list",
                    Type = "result",
                    Attachments = new List<ComposeExtensionAttachment>(),
                };
                invokeResponse.ComposeExtension = results;
            }

            // Return the response
            return Request.CreateResponse<ComposeExtensionResponse>(HttpStatusCode.OK, invokeResponse);
        } else
        {
            // Handle other types of Invoke activities here.
        }
    } else {
      // Failure case catch-all.
      var response = Request.CreateResponse(HttpStatusCode.BadRequest);
      response.Content = new StringContent("Invalid request! This API supports only messaging extension requests. Check your query and try again");
      return response;
    }
}
```

### <a name="nodejs"></a>Node.js

#### <a name="example-code-in-nodejs"></a>Código de ejemplo en Node.js

```javascript
require('dotenv').config();

import * as restify from 'restify';
import * as builder from 'botbuilder';
import * as teamBuilder from 'botbuilder-teams';

class App {
    run() {
        const server = restify.createServer();
        let teamChatConnector = new teamBuilder.TeamsChatConnector({
            appId: process.env.MICROSOFT_APP_ID,
            appPassword: process.env.MICROSOFT_APP_PASSWORD
        });

        // Command ID must match what's defined in manifest
        teamChatConnector.onQuery('<%= commandId %>',
            (event: builder.IEvent,
            query: teamBuilder.ComposeExtensionQuery,
            callback: (err: Error, result: teamBuilder.IComposeExtensionResponse, statusCode: number) => void) => {
                // Check for initialRun; i.e., when you should return default results
                // if (query.parameters[0].name === 'initialRun') {}

                // Check query.queryOptions.count and query.queryOptions.skip for paging

                // Return auth response
                // let response = teamBuilder.ComposeExtensionResponse.auth().actions([
                //     builder.CardAction.openUrl(null, 'https://authUrl', 'Please sign in')
                // ]).toResponse();

                // Return config response
                // let response = teamBuilder.ComposeExtensionResponse.config().actions([
                //     builder.CardAction.openUrl(null, 'https://configUrl', 'Please sign in')
                // ]).toResponse();

                // Return result response
                let response = teamBuilder.ComposeExtensionResponse.result('list').attachments([
                    new builder.ThumbnailCard()
                        .title('Test thumbnail card')
                        .text('This is a test thumbnail card')
                        .images([new builder.CardImage().url('https://bot-framework.azureedge.net/bot-icons-v1/bot-framework-default-9.png')])
                        .toAttachment()
                ]).toResponse();
                callback(null, response, 200);
            });
        server.post('/api/composeExtension', teamChatConnector.listen());
        server.listen(process.env.PORT, () => console.log(`listening to port:` + process.env.PORT));
    }
}

const app = new App();
app.run();
```
*Vea también* [ejemplos del marco de bot](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).

---
title: Búsqueda con extensiones de mensajería
description: Describe cómo desarrollar extensiones de mensajería basadas en búsquedas
keywords: Búsqueda de extensiones de mensajería de extensiones de mensajería de teams
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 07/20/2019
ms.openlocfilehash: dca01a22d4479d1f7c59689c5321483371c4aff2
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453715"
---
# <a name="search-with-messaging-extensions"></a>Búsqueda con extensiones de mensajería

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Las extensiones de mensajería basadas en búsquedas permiten consultar el servicio y publicar esa información en forma de tarjeta, directamente en el mensaje.

![Ejemplo de tarjeta de extensión de mensajería](~/assets/images/compose-extensions/ceexample.png)

En las secciones siguientes se describe cómo hacerlo:

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

## <a name="search-type-message-extensions"></a>Extensiones de mensaje de tipo de búsqueda

Para la extensión de mensajería basada en búsqueda, establezca el `type` parámetro en `query`. A continuación se muestra un ejemplo de un manifiesto con un único comando de búsqueda. Una sola extensión de mensajería puede tener hasta 10 comandos diferentes asociados. Esto puede incluir varias búsquedas y varios comandos basados en acción.

### <a name="complete-app-manifest-example"></a>Ejemplo de manifiesto de aplicación completa

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

## <a name="test-via-uploading"></a>Probar mediante carga

Puedes probar la extensión de mensajería cargando la aplicación.

Para abrir la extensión de mensajería, vaya a cualquiera de los chats o canales. Elija el **botón Más opciones** (**&#8943;**) en el cuadro de redacción y elija la extensión de mensajería.

## <a name="add-event-handlers"></a>Agregar controladores de eventos

La mayoría del trabajo implica el evento `onQuery` , que controla todas las interacciones en la ventana de extensión de mensajería.

Si se establece `canUpdateConfiguration` en en `true` el manifiesto, se habilita el elemento de menú **Configuración** para la extensión de mensajería y también debe controlar `onQuerySettingsUrl` y `onSettingsUpdate`.

## <a name="handle-onquery-events"></a>Controlar eventos onQuery

Una extensión de mensajería recibe un `onQuery` evento cuando ocurre algo en la ventana de extensión de mensajería o se envía a la ventana.

Si la extensión de mensajería usa una página de configuración, `onQuery` el controlador debe comprobar primero si hay información de configuración almacenada; si la extensión de mensajería no está configurada, `config` devuelva una respuesta con un vínculo a la página de configuración. Tenga en cuenta que la respuesta de la página de configuración también se controla mediante `onQuery`. La única excepción es cuando el controlador llama a la página de configuración; `onQuerySettingsUrl`vea la sección siguiente:

Si la extensión de mensajería requiere autenticación, compruebe la información de estado del usuario; si el usuario no ha iniciado sesión, siga las instrucciones de la sección [Autenticación](#authentication) más adelante en este tema.

A continuación, compruebe si `initialRun` está establecido; si es así, tome las medidas adecuadas, como proporcionar instrucciones o una lista de respuestas.

El resto del controlador solicita `onQuery` información al usuario, muestra una lista de tarjetas de vista previa y devuelve la tarjeta seleccionada por el usuario.

## <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a>Controlar eventos onQuerySettingsUrl y onSettingsUpdate

Los `onQuerySettingsUrl` eventos y `onSettingsUpdate` funcionan juntos para habilitar el **Configuración** de menú.

![Capturas de pantalla de ubicaciones de Configuración elemento de menú](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

El controlador para `onQuerySettingsUrl` devuelve la dirección URL de la página de configuración; una vez que se cierra la página de configuración, `onSettingsUpdate` el controlador acepta y guarda el estado devuelto. Este es el único caso en el que `onQuery` *no recibe* la respuesta de la página de configuración.

## <a name="receive-and-respond-to-queries"></a>Recibir y responder a consultas

Cada solicitud a la extensión de mensajería se realiza a través de un `Activity` objeto que se publica en la dirección URL de devolución de llamada. La solicitud contiene información sobre el comando de usuario, como id. y valores de parámetro. La solicitud también proporciona metadatos sobre el contexto en el que se invocó la extensión, incluidos los identificadores de usuario y inquilino, junto con identificadores de chat o de canal y de equipo.

### <a name="receive-user-requests"></a>Recibir solicitudes de usuario

Cuando un usuario realiza una consulta, Microsoft Teams envía al servicio un objeto Bot Framework `Activity` estándar. El servicio debe realizar su lógica para un `Activity` que `name` `type` `invoke` se ha establecido en y establecido en un tipo `composeExtension` compatible, como se muestra en la tabla siguiente.

Además de las propiedades de actividad del bot estándar, la carga contiene los siguientes metadatos de solicitud:

|Nombre de propiedad|Objetivo|
|---|---|
|`type`| Tipo de solicitud; debe ser `invoke`. |
|`name`| Tipo de comando que se emite al servicio. Actualmente se admiten los siguientes tipos: <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| Id. del usuario que envió la solicitud. |
|`from.name`| Nombre del usuario que envió la solicitud. |
|`from.aadObjectId`| Microsoft Azure Active Directory (Azure AD) de objeto del usuario que envió la solicitud. |
|`channelData.tenant.id`| Microsoft Azure Active Directory (Azure AD) de inquilino. |
|`channelData.channel.id`| Identificador de canal (si la solicitud se realizó en un canal). |
|`channelData.team.id`| Id. de equipo (si la solicitud se realizó en un canal). |
|`clientInfo`|Metadatos opcionales sobre el software cliente usado para enviar el mensaje de un usuario. La entidad puede contener dos propiedades:<br>El `country` campo contiene la ubicación detectada por el usuario.<br>El `platform` campo describe la plataforma de cliente de mensajería. <br>Para obtener información adicional *, consulte* [Tipos de entidad que no son IRI: clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).|

Los parámetros de solicitud en sí se encuentran en el objeto value, que incluye las siguientes propiedades:

| Nombre de propiedad | Objetivo |
|---|---|
| `commandId` | Nombre del comando invocado por el usuario, que coincide con uno de los comandos declarados en el manifiesto de la aplicación. |
| `parameters` | Matriz de parámetros: cada objeto de parámetro contiene el nombre del parámetro, junto con el valor del parámetro proporcionado por el usuario. |
| `queryOptions` | Parámetros de paginación: <br>`skip`: recuento de omitir para esta consulta <br>`count`: número de elementos que se devolverán |

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

Como alternativa (o además) a la búsqueda en el servicio externo, puede usar una dirección URL insertada en el cuadro de mensaje de redacción para consultar el servicio y devolver una tarjeta. En la captura de pantalla siguiente, un usuario ha pegado en una dirección URL un elemento de trabajo en Azure DevOps que la extensión de mensajería ha resuelto en una tarjeta.

![Ejemplo de desafusado de vínculos](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

Para habilitar la extensión de mensajería para que interactúe `messageHandlers` con vínculos de esta manera, primero tendrás que agregar la matriz al manifiesto de la aplicación como en el ejemplo siguiente:

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

Una vez que hayas agregado el dominio para escuchar el manifiesto de la aplicación, tendrás que cambiar el código del bot para responder a la [](#respond-to-user-requests) siguiente solicitud de invocación.

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

Si la aplicación devuelve varios elementos, solo se usará el primero.

### <a name="respond-to-user-requests"></a>Responder a solicitudes de usuario

Cuando el usuario realiza una consulta, Microsoft Teams emite una solicitud HTTP sincrónica al servicio. En ese momento, el código tiene 5 segundos para proporcionar una respuesta HTTP a la solicitud. Durante este tiempo, el servicio puede realizar búsquedas adicionales o cualquier otra lógica empresarial necesaria para atender la solicitud.

El servicio debe responder con los resultados que coincidan con la consulta de usuario. La respuesta debe indicar un código de estado HTTP y `200 OK` un objeto application/json válido con el siguiente cuerpo:

|Nombre de propiedad|Objetivo|
|---|---|
|`composeExtension`|Sobre de respuesta de nivel superior.|
|`composeExtension.type`|Tipo de respuesta. Se admiten los siguientes tipos: <br>`result`: muestra una lista de resultados de búsqueda <br>`auth`: pide al usuario que se autentique <br>`config`: pide al usuario que configure la extensión de mensajería <br>`message`: muestra un mensaje de texto sin formato |
|`composeExtension.attachmentLayout`|Especifica el diseño de los datos adjuntos. Se usa para respuestas de tipo `result`. <br>Actualmente se admiten los siguientes tipos: <br>`list`: una lista de objetos de tarjeta que contienen miniaturas, título y campos de texto <br>`grid`: una cuadrícula de imágenes en miniatura |
|`composeExtension.attachments`|Matriz de objetos de datos adjuntos válidos. Se usa para respuestas de tipo `result`. <br>Actualmente se admiten los siguientes tipos: <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|Acciones sugeridas. Se usa para respuestas de tipo `auth` o `config`. |
|`composeExtension.text`|Mensaje que se mostrará. Se usa para respuestas de tipo `message`. |

#### <a name="response-card-types-and-previews"></a>Tipos y vistas previas de tarjetas de respuesta

Se admiten los siguientes tipos de datos adjuntos:

* [Tarjeta miniatura](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Tarjeta de héroe](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Tarjeta conector de Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Tarjeta adaptable](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Para obtener más información, vea [Tarjetas](~/task-modules-and-cards/what-are-cards.md) para obtener información general.

Para obtener información sobre cómo usar los tipos de miniaturas y tarjetas de héroe, consulta [Agregar tarjetas y acciones de tarjeta](~/task-modules-and-cards/cards/cards-actions.md).

Para obtener documentación adicional acerca de la Office 365 Connector, consulte [Using Office 365 Connector cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).

La lista de resultados se muestra en la interfaz Microsoft Teams con una vista previa de cada elemento. La vista previa se genera de dos maneras:

* Uso de la `preview` propiedad dentro del `attachment` objeto. Los `preview` datos adjuntos solo pueden ser una tarjeta Hero o Thumbnail.
* Extraído de las propiedades `title`básicas , `text`y `image` de los datos adjuntos. Solo se usan si la `preview` propiedad no está establecida y estas propiedades están disponibles.

Puede mostrar una vista previa de una tarjeta Adaptive o Office 365 Connector en la lista de resultados simplemente estableciendo su propiedad de vista previa; esto no es necesario si los resultados ya son tarjetas de miniatura o de héroe. Si usas los datos adjuntos de vista previa, debe ser una tarjeta hero o thumbnail. Si no se especifica ninguna propiedad de vista previa, se producirá un error en la vista previa de la tarjeta y no se mostrará nada.

#### <a name="response-example"></a>Ejemplo de respuesta

En este ejemplo se muestra una respuesta con dos resultados, que mezclan diferentes formatos de tarjeta: Office 365 Connector y Adaptive. Aunque probablemente quieras seguir con un formato de tarjeta en la respuesta, `preview` `attachments` muestra cómo la propiedad de cada elemento de la colección debe definir explícitamente una vista previa en formato de miniatura o de héroe como se describió anteriormente.

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
              "activityImage&quot;: &quot;https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value&quot;: &quot;[Larry Brown](mailto:larryb@example.com)"
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

Si se establece `initialRun` en en `true` el manifiesto, Microsoft Teams una consulta "predeterminada" cuando el usuario abre por primera vez la extensión de mensajería. El servicio puede responder a esta consulta con un conjunto de resultados prepopulados. Esto puede ser útil para mostrar, por ejemplo, elementos vistos recientemente, favoritos o cualquier otra información que no dependa de la entrada del usuario.

La consulta predeterminada tiene la misma estructura que cualquier consulta de usuario normal, excepto con un parámetro `initialRun` cuyo valor de cadena es `true`.

#### <a name="request-example-for-a-default-query"></a>Ejemplo de solicitud para una consulta predeterminada

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

Cada solicitud a los servicios incluye el identificador ofuscado del usuario que realizó la solicitud, así como el nombre para mostrar del usuario y el identificador de objeto Microsoft Azure Active Directory (Azure AD).

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

Se `id` garantiza `aadObjectId` que los valores y son los del usuario Teams autenticado. Se pueden usar como claves para buscar credenciales o cualquier estado almacenado en caché en el servicio. Además, cada solicitud contiene el identificador de inquilino Microsoft Azure Active Directory (Azure AD) del usuario, que se puede usar para identificar la organización del usuario. Si procede, la solicitud también contiene los IDs de equipo y canal desde los que se originó la solicitud.

## <a name="authentication"></a>Autenticación

Si el servicio requiere autenticación de usuario, debe iniciar sesión en el usuario antes de poder usar la extensión de mensajería. Si ha escrito un bot o una pestaña que inicia sesión en el usuario, esta sección debe ser familiar.

La secuencia es la siguiente:

1. El usuario emite una consulta o la consulta predeterminada se envía automáticamente al servicio.
2. El servicio comprueba si el usuario se ha autenticado primero inspeccionando el Teams de usuario.
3. Si el usuario no se ha autenticado, envíe una `auth` respuesta con una `openUrl` acción sugerida, incluida la dirección URL de autenticación.
4. El Microsoft Teams inicia una ventana emergente que hospeda la página web mediante la dirección URL de autenticación determinada.
5. Después de que el usuario inicia sesión, debe cerrar la ventana y enviar un "código de autenticación" al Teams cliente.
6. A continuación, Teams cliente reedición de la consulta al servicio, que incluye el código de autenticación pasado en el paso 5.

El servicio debe comprobar que el código de autenticación recibido en el paso 6 coincide con el del paso 5. Esto garantiza que un usuario malintencionado no intente suplantar o poner en peligro el flujo de inicio de sesión. Esto "cierra el bucle" para finalizar la secuencia de autenticación segura.

### <a name="respond-with-a-sign-in-action"></a>Responder con una acción de inicio de sesión

Para solicitar a un usuario no autenticado que inicie sesión, responda con una acción sugerida de tipo `openUrl` que incluya la dirección URL de autenticación.

#### <a name="response-example-for-a-sign-in-action"></a>Ejemplo de respuesta para una acción de inicio de sesión

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
> Para que la experiencia de inicio de sesión se hospeda en una ventana emergente de Teams, la parte de dominio de la dirección URL debe estar en la lista de dominios válidos de la aplicación. Para obtener más información, [vea validDomains](~/resources/schema/manifest-schema.md#validdomains) en el esquema de manifiesto.

### <a name="start-the-sign-in-flow"></a>Iniciar el flujo de inicio de sesión

La experiencia de inicio de sesión debe responder y caber dentro de una ventana emergente. Debe integrarse con el SDK [Microsoft Teams cliente de JavaScript](/javascript/api/overview/msteams-client), que usa el paso de mensajes.

Al igual que con otras experiencias incrustadas que se ejecutan Microsoft Teams, el código dentro de la ventana debe llamar primero`microsoftTeams.initialize()`. Si el código realiza un flujo de OAuth, puedes pasar el identificador de usuario de Teams a la ventana, que luego puede pasarlo a la dirección URL de inicio de sesión de OAuth.

### <a name="complete-the-sign-in-flow"></a>Completar el flujo de inicio de sesión

Cuando la solicitud de inicio de sesión se completa y vuelve a redirigir a la página, debe realizar los siguientes pasos:

1. Generar un código de seguridad. (Puede ser un número aleatorio). Debe almacenar en caché este código en el servicio, junto con las credenciales obtenidas a través del flujo de inicio de sesión, como tokens de OAuth 2.0.
2. Llama `microsoftTeams.authentication.notifySuccess` y pasa el código de seguridad.

En este momento, la ventana se cierra y el control se pasa al Teams cliente. El cliente ahora puede volver a emitir la consulta de usuario original, junto con el código de seguridad de la `state` propiedad. El código puede usar el código de seguridad para buscar las credenciales almacenadas anteriormente para completar la secuencia de autenticación y, a continuación, completar la solicitud de usuario.

#### <a name="reissued-request-example"></a>Ejemplo de solicitud ree emitida

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

Para recibir y controlar consultas con el SDK de Bot Builder para .NET, `invoke` puede comprobar el tipo de acción en la actividad entrante y, a continuación, usar el método auxiliar en el paquete de NuGet [Microsoft.Bot.Connector.Teams para](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) determinar si se trata de una actividad de extensión de mensajería.

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

## <a name="see-also"></a>Vea también

[Ejemplos de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).

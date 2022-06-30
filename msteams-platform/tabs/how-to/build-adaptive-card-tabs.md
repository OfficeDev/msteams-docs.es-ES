---
title: Crear pestañas de tarjeta adaptable
author: KirtiPereira
description: En este módulo, obtendrá información sobre cómo crear pestañas mediante Tarjetas adaptables con ejemplos de código, como la invocación de actividades, la comprensión del flujo de trabajo del módulo de tareas y la autenticación.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: 48415f4cba1a748dafd9d21e8429a59414769b98
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558180"
---
# <a name="build-tabs-with-adaptive-cards"></a>Compilar pestañas con tarjetas adaptables

> [!IMPORTANT]
>
> * Actualmente, las pestañas con Tarjetas adaptables solo se admiten como aplicaciones personales.

Al desarrollar una pestaña con el método tradicional, podría encontrarse con estas incidencias:

* Consideraciones sobre HTML y CSS
* Tiempos de carga lentos
* Restricciones de iFrame
* Mantenimiento y costes del servidor

Las pestañas de tarjeta adaptable son una nueva forma de crear pestañas en Teams. En lugar de incrustar contenido web en un IFrame, puede representar Tarjetas adaptables en una pestaña. Aunque el front-end se representa con Tarjetas adaptables, el back-end se basa en un bot. El bot es responsable de aceptar las solicitudes y responder adecuadamente con la tarjeta adaptable que se representa.

Puede crear sus pestañas con bloques de creación de interfaz de usuario (UI) listos para usar nativos en equipos de escritorio, web y móviles. Este artículo le ayuda a comprender los cambios necesarios para realizar en el manifiesto de la aplicación. El artículo también identifica cómo la actividad de invocación solicita y envía información en la pestaña con Tarjetas adaptables y su efecto en el flujo de trabajo del módulo de tareas.

En la imagen siguiente se muestran las pestañas de compilación con Tarjetas adaptables en equipos de escritorio y móviles:

:::image type="content" source="../../assets/images/adaptive-cards-rendered-in-tabs.png" alt-text="Ejemplo de tarjeta adaptable representada en pestañas.":::

## <a name="prerequisites"></a>Requisitos previos

Antes de empezar a usar Tarjetas adaptables para crear pestañas, debe:

* Familiarizarse con el [desarrollo de bots](../../bots/what-are-bots.md), [Tarjetas adaptables](https://adaptivecards.io/) y [Módulos de tareas](../../task-modules-and-cards/task-modules/task-modules-bots.md) en Teams.
* Haga que un bot se ejecute en Teams para su desarrollo.

## <a name="changes-to-app-manifest"></a>Cambios en el manifiesto de la aplicación

Las aplicaciones personales que representan pestañas deben incluir una matriz de `staticTabs` en su manifiesto de aplicación. Las pestañas de tarjeta adaptable se representan cuando se proporciona la propiedad `contentBotId` en la definición de `staticTab`. Las definiciones de pestañas estáticas deben contener un `contentBotId`especificando una pestaña tarjeta adaptable o un `contentUrl`especificando una experiencia típica de pestaña de contenido web hospedada.

> [!NOTE]
> La propiedad `contentBotId` está disponible actualmente en la versión 1.9 ó posterior del manifiesto.

Proporcione la propiedad `contentBotId` con el `botId` con el que debe comunicarse la pestaña Tarjeta adaptable. El `entityId` configurado para la pestaña Tarjeta adaptable se envía en el parámetro `tabContext` de cada solicitud de invocación y se puede usar para diferenciar las pestañas de tarjeta adaptables con tecnología del mismo bot. Para obtener más información sobre otros campos de definición de pestañas estáticas, vea [esquema de manifiesto](../../resources/schema/manifest-schema.md#statictabs).

A continuación se muestra un manifiesto de pestaña de tarjeta adaptable de ejemplo:

```json
{
  "$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
  "manifestVersion": "1.9",
  "id": "00000000-0000-0000-0000-000000000000",
  "version": "0.0.1",
  "packageName": "acprototype",
  "developer": {
    "name": "Contoso",
    "websiteUrl": "https://contoso.yourwebsite.com",
    "privacyUrl": "https://contoso.yourwebsite.com/privacy.html",
    "termsOfUseUrl": "https://contoso.yourwebsite.com/terms.html"
  },
  "name": {
    "short": "Contoso",
    "full": "Contoso Home"
  },
  "description": {
    "short": "Add short description here",
    "full": "Add full description here"
  },
  "icons": {
    "outline": "icon-outline.png",
    "color": "icon-color.png"
  },
  "accentColor": "#D85028",
  "configurableTabs": [],
  "staticTabs": [
    {
      "entityId": "homeTab",
      "name": "Home",
      "contentBotId": "00000000-0000-0000-0000-000000000000",
      "scopes": ["personal"]
    },
    {
      "entityId": "moreTab",
      "name": "More",
      "contentBotId": "00000000-0000-0000-0000-000000000000",
      "scopes": ["personal"]
    }
  ],
  "connectors": [],
  "composeExtensions": [],
  "permissions": ["identity", "messageTeamMembers"],
  "validDomains": [
    "contoso.yourwebsite.com",
    "token.botframework.com"
  ]
}
```

## <a name="invoke-activities"></a>Invocar actividades

La comunicación entre la pestaña tarjeta adaptable y el bot se realiza a través de `invoke` actividades. Cada actividad de `invoke` tiene un nombre de **correspondiente**. Use el nombre de cada actividad para diferenciar cada solicitud. `tab/fetch` y `tab/submit` son las actividades que se tratan en esta sección.

> [!NOTE]
>
> * Los bots deben enviar todas las respuestas a [dirección URL del servicio](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#base-uri&preserve-view=true). La dirección URL del servicio se recibe como parte de la carga de `activity` entrante.
> * El tamaño de la carga de invocación ha aumentado a 80 KB.

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a>Capturar tarjeta adaptable para representar en una pestaña

`tab/fetch` es la primera solicitud de invocación que recibe el bot cuando un usuario abre una pestaña de tarjeta adaptable. Cuando el bot recibe la solicitud, envía una pestaña **continuar** de respuesta o una pestaña **autenticación** de respuesta.
El **continuar** de respuesta incluye una matriz para **tarjetas**, que se representa verticalmente en la pestaña en el orden de la matriz.

> [!NOTE]
> Para obtener más información sobre **respuesta de autenticación**, consulte [autenticación](#authentication).

En el código siguiente se proporcionan ejemplos de `tab/fetch` solicitud y respuesta:

**`tab/fetch` solicitud**

```json
// tab/fetch POST request: agents/{botId}/invoke
{
    "name": "tab/fetch",
    "value: {
        "tabContext": {
            "tabEntityId": "{tab_entity_id}"
        },
        "context": {
            "theme": "default"
            }
    },
    "conversation": {
        "id": "{generated_conversation_id}"
    },
    "imdisplayname": "{user_display_name}"
}
```

**`tab/fetch` respuesta**

```json
// tab/fetch **continue** POST response:
{
    "tab": {
        "type": "continue",
        "value": {
            "cards": [
                {
                    "card": adaptiveCard1,
                },
                {
                    "card": adaptiveCard2,
                },
                {
                    "card": adaptiveCard3
                }  
            ]
        },
    },
    "responseType": "tab"
}
```

### <a name="handle-submits-from-adaptive-card"></a>Control de envíos desde la tarjeta adaptable

Después de representar una tarjeta adaptable en la pestaña, puede responder a las interacciones del usuario. La solicitud de invocación de `tab/submit` controla esta respuesta.

Cuando un usuario selecciona un botón en la pestaña Tarjeta adaptable, la solicitud de `tab/submit` se desencadena en el bot con los datos correspondientes a través de la función `Action.Submit` de tarjeta adaptable. Los datos de la tarjeta adaptable están disponibles a través de la propiedad de datos de la solicitud de `tab/submit`. Recibirá cualquiera de las siguientes respuestas a su solicitud:

* Un código de estado HTTP `200` respuesta sin cuerpo. Una respuesta 200 vacía no da como resultado ninguna acción realizada por el cliente.
* La respuesta de **continuar** de la pestaña estándar`200`, como se explica en [Captura de tarjeta adaptable](#fetch-adaptive-card-to-render-to-a-tab). Una pestaña **continuar** de respuesta desencadena que el cliente actualice la pestaña tarjeta adaptable representada con las Tarjetas adaptables proporcionado en la matriz de tarjetas del **continuar** de respuesta.

En el código siguiente se proporcionan ejemplos de `tab/submit` solicitud y respuesta:

**`tab/submit` solicitud**

```json
// tab/submit POST request: agents/{botId}/invoke:
{
    "name": "tab/submit",
    "value": {
        "data": {
            "type": "tab/submit",
            //...<data properties>
            },
        "context": {
            "theme": "default"
            },
        "tabContext": {
            "tabEntityId": "{tab_entity_id}"
            },
        },
    "conversation": {
           "id": "{generated_conversation_id}" 
        },
    "imdisplayname": "{user_display_name}"
}
```

**`tab/submit` respuesta**

```json
//tab/fetch **continue** POST response:
{
    "tab": {
        "type": "continue",
        "value": {
            "cards": [
              {
                "card": adaptiveCard1,
                },
              {
                "card": adaptiveCard2,
                } 
            ]
        },
    },
    "responseType": "tab"
}
```

## <a name="understand-task-module-workflow"></a>Descripción del flujo de trabajo del módulo de tareas

El módulo de tareas también usa la tarjeta adaptable para invocar solicitudes y respuestas `task/fetch` y `task/submit`. Para obtener más información, vea [usar módulos de tareas en bots de Microsoft Teams](../../task-modules-and-cards/task-modules/task-modules-bots.md).

Con la introducción de la pestaña Tarjeta adaptable, hay un cambio en la forma en que el bot responde a una solicitud de `task/submit`. Si usa una pestaña tarjeta adaptable, el bot responde a la solicitud de invocación `task/submit` con la pestaña estándar **continuar** de respuesta y cierra el módulo de tareas. La pestaña Tarjeta adaptable se actualiza mediante la representación de la nueva lista de tarjetas proporcionada en la pestaña **continuar** como cuerpo de respuesta.

### <a name="invoke-taskfetch"></a>Invocar `task/fetch`

En el código siguiente se proporcionan ejemplos de `task/fetch` solicitud y respuesta:

**`task/fetch` solicitud**

```json
// task/fetch POST request: agents/{botId}/invoke
{
    "name": "task/fetch",
    "value": {
        "data": {
            "type": "task/fetch"
        },
        "context": {
            "theme": "default",
        },
        "tabContext": {
            "tabEntityId": "{tab_entity_id}"
        }
    },
    "imdisplayname": "{user_display_name}",
    "conversation": {
        "id": "{generated_conversation_id}"
    } 
}
```

**`task/fetch` respuesta**

```json
// task/fetch POST response: agents/{botId}/invoke
{
    "task": {
        "value": {
            "title": "Ninja Cat",
            "height": "small",
            "width": "small",
            "card": {
                "contentType": "application/vnd.microsoft.card.adaptive",
                "content": adaptiveCard,
            }
        },
    "type": "continue"
    },
    "responseType": "task"
}
```

### <a name="invoke-tasksubmit"></a>Invocar `task/submit`

En el código siguiente se proporcionan ejemplos de `task/submit` solicitud y respuesta:

**`task/submit` solicitud**

```json
// task/submit POST request: agent/{botId}/invoke:
{
    "name": "task/submit",
    "value": {
        "data": {serialized_data_object},
        "context": {
            "theme": "default"
        },
    "tabContext": {
        "tabEntityId": "{tab_entity_id}"
        },
    },
    "conversation": {
        "id": "{generated_conversation_id}"
    },
    "imdisplayname": "{user_display_name}",
}
```

**`task/submit` tipo de respuesta de pestaña**

```json
// tab/fetch **continue** POST response: 
{
    "task":{
        "value": {
            "tab": {
                "type": "continue",
                "value": {
                    "cards": [
                        {
                            "card": adaptiveCard1
                        },
                        {
                            "card": adaptiveCard2
                        }
                    ]
                }
            }
        },
        "type": "continue"
    },
    "responseType": "task"
}
```

## <a name="authentication"></a>Autenticación

En las secciones anteriores, ha visto que la mayor parte de los paradigmas de desarrollo se pueden extender desde las solicitudes y respuestas del módulo de tareas a las solicitudes de tabulación y las respuestas. Cuando se trata de controlar la autenticación, el flujo de trabajo de la pestaña Tarjeta adaptable sigue el patrón de autenticación para las extensiones de mensaje. Para obtener más información, vea [agregar autenticación](../../messaging-extensions/how-to/add-authentication.md).

`tab/fetch` solicitudes pueden tener una respuesta **continuar** o una respuesta **autenticación**. Cuando se desencadena una solicitud de `tab/fetch` y recibe una pestaña **autenticación** de respuesta, la página de inicio de sesión se muestra al usuario.

**Para obtener un código de autenticación a través de `tab/fetch` invocar**

1. Abra la aplicación. Aparece la página de inicio de sesión.

    > [!NOTE]
    > El logotipo de la aplicación se proporciona a través de la propiedad `icon` definida en el manifiesto de la aplicación. Título que aparece después de definir el logotipo en la propiedad `title` devuelta en la pestaña **autenticación** de cuerpo de respuesta.

1. Seleccione **Iniciar sesión**. Se le redirigirá a la dirección URL de autenticación proporcionada en la propiedad `value` del cuerpo de respuesta **autenticación**.
1. Aparecerá una ventana emergente. Esta ventana emergente hospeda la página web mediante la dirección URL de autenticación.
1. Después de iniciar sesión, cierre la ventana. Se envía un **código de autenticación** al cliente de Teams.
1. A continuación, el cliente de Teams vuelve a emitir la solicitud de `tab/fetch` al servicio, que incluye el código de autenticación proporcionado por la página web hospedada.

### <a name="tabfetch-authentication-data-flow"></a>flujo de datos de autenticación `tab/fetch`

En la imagen siguiente se proporciona información general sobre cómo funciona el flujo de datos de autenticación para una invocación de `tab/fetch`.

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="Ejemplo de flujo de autenticación de pestaña de tarjeta adaptable.":::

**`tab/fetch` respuesta de autenticación**

El código siguiente proporciona un ejemplo de `tab/fetch` como respuesta de autenticación:

```json
// tab/auth POST response (openURL)
{
    "tab": {
        "type": "auth",
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

### <a name="example"></a>Ejemplo

En el código siguiente se muestra un ejemplo de solicitud reemitido:

```json
{
    "name": "tab/fetch",
    "type": "invoke",
    "timestamp": "2021-01-15T00:10:12.253Z",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "from": {
        "id": "{id}",
        "name": "John Smith",
        "aadObjectId": "00000000-0000-0000-0000-000000000000"
    },
    "conversation": {
        "tenantId": "{tenantId}",
        "id": "tab:{guid}"
    },
    "recipients": {
        "id": "28:00000000-0000-0000-0000-000000000000",
        "name": "ContosoApp"
    },
    "entities": [
        {
            "locale": "en-us",
            "country": "US",
            "platform": "Windows",
            "timezone": "America/Los_Angeles",
            "type": "clientInfo"
        }
    ],
    "channelData": {
        "tenant": { "id": "00000000-0000-0000-0000-000000000000" },
        "source": { "name": "message" }
    },
    "value": {
        "tabContext": { "tabEntityId": "homeTab" },
        "state": "0.43195668034524815"
    },
    "locale": "en-US",
    "localTimeZone": "America/Los_Angeles"
}
```

## <a name="code-sample"></a>Ejemplo de código

|**Ejemplo de nombre** | **Descripción** |**.NET** | **Node.js** |
|----------------|-----------------|--------------|--------------|
| Mostrar Tarjetas adaptables en la pestaña Teams | Código de ejemplo de pestaña de Microsoft Teams, que muestra cómo mostrar Tarjetas adaptables en Teams. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/csharp)| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/nodejs) |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Expansión del vínculo de pestañas y la Vista de fases](~/tabs/tabs-link-unfurling.md)

## <a name="see-also"></a>Consulte también

* [Tarjeta adaptable](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [Pestañas de Teams](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de grupo o de canal](~/tabs/how-to/create-channel-group-tab.md)
* [Pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md)
* [Comentarios de finalización de formularios](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)

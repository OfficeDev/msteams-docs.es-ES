---
title: Crear pestañas de tarjeta adaptables
author: KirtiPereira
description: Obtenga información sobre la creación de pestañas mediante tarjetas adaptables con ejemplos de código, como la invocación de actividades, la comprensión del flujo de trabajo del módulo de tareas y la autenticación.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
keywords: flujo de datos de autenticación de aplicaciones personales de tarjeta adaptable
ms.openlocfilehash: 95507373671f9044bec788e981f66931b4588705
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104528"
---
# <a name="build-tabs-with-adaptive-cards"></a>Compilar pestañas con tarjetas adaptables

> [!IMPORTANT]
>
> * Actualmente, las pestañas con tarjetas adaptables solo se admiten como aplicaciones personales.

Al desarrollar una pestaña con el método tradicional, puede encontrarse con estos problemas:

* Consideraciones sobre HTML y CSS
* Tiempos de carga lentos
* Restricciones de iFrame
* Mantenimiento y costos del servidor

Las pestañas de tarjeta adaptable son una nueva forma de crear pestañas en Teams. En lugar de insertar contenido web en un IFrame, puede representar tarjetas adaptables en una pestaña. Mientras el front-end se representa con tarjetas adaptables, el back-end funciona con un bot. El bot es responsable de aceptar solicitudes y responder correctamente con la tarjeta adaptable que se representa.

Puede crear las pestañas con bloques de creación de interfaz de usuario (UI) listos para crear bloques nativos en escritorio, web y dispositivos móviles. Este artículo le ayuda a comprender los cambios necesarios para realizar en el manifiesto de la aplicación. En el artículo también se identifica cómo la actividad de invocación solicita y envía información en la pestaña con tarjetas adaptables y su efecto en el flujo de trabajo del módulo de tareas.

En la imagen siguiente se muestran pestañas de compilación con tarjetas adaptables en dispositivos móviles y de escritorio:

:::image type="content" source="../../assets/images/adaptive-cards-rendered-in-tabs.png" alt-text="Ejemplo de tarjeta adaptable representada en pestañas." border="false":::

## <a name="prerequisites"></a>Requisitos previos

Antes de empezar a usar tarjetas adaptables para crear pestañas, debe:

* Familiarícese con el [desarrollo de bots](../../bots/what-are-bots.md), [tarjetas adaptables](https://adaptivecards.io/) y [módulos de tareas](../../task-modules-and-cards/task-modules/task-modules-bots.md) en Teams.
* Tener un bot en ejecución en Teams para el desarrollo.

## <a name="changes-to-app-manifest"></a>Cambios en el manifiesto de la aplicación

Las aplicaciones personales que representan pestañas deben incluir una `staticTabs` matriz en el manifiesto de la aplicación. Las pestañas de tarjeta adaptable se representan cuando se proporciona la `contentBotId` propiedad en la `staticTab` definición. Las definiciones de pestañas estáticas deben contener , `contentBotId`especificando una pestaña tarjeta adaptable o , `contentUrl`especificando una experiencia típica de pestaña de contenido web hospedada.

> [!NOTE]
> La `contentBotId` propiedad está disponible actualmente en la versión de manifiesto 1.9 o posterior.

Proporcione la `contentBotId` propiedad con la `botId` que la pestaña Tarjeta adaptable debe comunicarse. La `entityId` pestaña configurada para la tarjeta adaptable se envía en el `tabContext` parámetro de cada solicitud de invocación y se puede usar para diferenciar las pestañas de tarjeta adaptable que funcionan con el mismo bot. Para obtener más información sobre otros campos de definición de tabulación estática, vea [esquema de manifiesto](../../resources/schema/manifest-schema.md#statictabs).

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

## <a name="invoke-activities"></a>Invocación de actividades

La comunicación entre la pestaña Tarjeta adaptable y el bot se realiza a través de `invoke` actividades. Cada `invoke` actividad tiene un **nombre** correspondiente. Use el nombre de cada actividad para diferenciar cada solicitud. `tab/fetch` y `tab/submit` son las actividades que se tratan en esta sección.

> [!NOTE]
>
> * Los bots deben enviar todas las respuestas a la [dirección URL del servicio](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#base-uri&preserve-view=true). La dirección URL del servicio se recibe como parte de la carga entrante `activity` .
> * El tamaño de carga de invocación ha aumentado a 80 kb.

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a>Capturar tarjeta adaptable para representarla en una pestaña

`tab/fetch` es la primera solicitud de invocación que recibe el bot cuando un usuario abre una pestaña tarjeta adaptable. Cuando el bot recibe la solicitud, envía una respuesta de **continuación** de pestaña o una respuesta de **autenticación** de pestaña.
La respuesta **continue** incluye una matriz para **las tarjetas**, que se representa verticalmente en la pestaña en el orden de la matriz.

> [!NOTE]
> Para obtener más información sobre la respuesta **de autenticación** , consulte [autenticación](#authentication).

El código siguiente proporciona ejemplos de `tab/fetch` solicitud y respuesta:

**`tab/fetch` Petición**

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

**`tab/fetch` Respuesta**

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

Después de representar una tarjeta adaptable en la pestaña, puede responder a las interacciones del usuario. Esta respuesta se controla mediante la solicitud de `tab/submit` invocación.

Cuando un usuario selecciona un botón en la pestaña Tarjeta adaptable, la solicitud se desencadena en el `tab/submit` bot con los datos correspondientes a través de la `Action.Submit` función de tarjeta adaptable. Los datos de la tarjeta adaptable están disponibles a través de la propiedad data de la `tab/submit` solicitud. Recibe cualquiera de las siguientes respuestas a la solicitud:

* Respuesta de código `200` de estado HTTP sin cuerpo. Una respuesta vacía de 200 da como resultado que el cliente no realice ninguna acción.
* La respuesta de **continuación** de la pestaña estándar`200`, como se explica en [Captura de tarjeta adaptable](#fetch-adaptive-card-to-render-to-a-tab). Una respuesta **de continuar** de pestaña desencadena que el cliente actualice la pestaña tarjeta adaptable representada con las tarjetas adaptables proporcionadas en la matriz de tarjetas de la respuesta **de continuar** .

El código siguiente proporciona ejemplos de `tab/submit` solicitud y respuesta:

**`tab/submit` Petición**

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

**`tab/submit` Respuesta**

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

El módulo de tareas también usa la tarjeta adaptable para invocar `task/fetch` y `task/submit` solicitudes y respuestas. Para obtener más información, consulte [Uso de módulos de tareas en bots de Microsoft Teams](../../task-modules-and-cards/task-modules/task-modules-bots.md).

Con la introducción de la pestaña Tarjeta adaptable, hay un cambio en la forma en que el bot responde a una `task/submit` solicitud. Si usa una pestaña Tarjeta adaptable, el bot responde a la solicitud de `task/submit` invocación con la respuesta **de continuación** de la pestaña estándar y cierra el módulo de tareas. La pestaña Tarjeta adaptable se actualiza representando la nueva lista de tarjetas proporcionada en el cuerpo de la respuesta **de continuación** de la pestaña.

### <a name="invoke-taskfetch"></a>Invocar `task/fetch`

El código siguiente proporciona ejemplos de `task/fetch` solicitud y respuesta:

**`task/fetch` Petición**

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

**`task/fetch` Respuesta**

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

El código siguiente proporciona ejemplos de `task/submit` solicitud y respuesta:

**`task/submit` Petición**

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

**`task/submit` tipo de respuesta tab**

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

En las secciones anteriores, ha visto que la mayoría de los paradigmas de desarrollo se pueden ampliar desde las solicitudes y respuestas del módulo de tareas hasta las solicitudes y respuestas de tabulación. A la hora de controlar la autenticación, el flujo de trabajo de la pestaña Tarjeta adaptable sigue el patrón de autenticación de las extensiones de mensaje. Para obtener más información, vea [Agregar autenticación](../../messaging-extensions/how-to/add-authentication.md).

`tab/fetch` las solicitudes pueden tener una respuesta **continue** o **auth** . Cuando se desencadena una `tab/fetch` solicitud y recibe una respuesta de **autenticación** de pestaña, la página de inicio de sesión se muestra al usuario.

**Para obtener un código de autenticación a través de `tab/fetch` la invocación**

1. Abra la aplicación. Aparece la página de inicio de sesión.

    > [!NOTE]
    > El logotipo de la aplicación se proporciona a través de la `icon` propiedad definida en el manifiesto de la aplicación. El título que aparece después de definir el logotipo en la `title` propiedad devuelta en el cuerpo de la respuesta **de autenticación** de tabulación.

1. Seleccione **Iniciar sesión**. Se le redirigirá a la dirección URL de autenticación proporcionada en la `value` propiedad del cuerpo de la respuesta de **autenticación** .
1. Aparecerá una ventana emergente. Esta ventana emergente hospeda la página web mediante la dirección URL de autenticación.
1. Después de iniciar sesión, cierre la ventana. Se envía **un código de autenticación** al cliente de Teams.
1. A continuación, el cliente Teams vuelve a emitir la `tab/fetch` solicitud al servicio, que incluye el código de autenticación proporcionado por la página web hospedada.

### <a name="tabfetch-authentication-data-flow"></a>`tab/fetch` flujo de datos de autenticación

En la imagen siguiente se proporciona información general sobre cómo funciona el flujo de datos de autenticación para una `tab/fetch` invocación.

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="Ejemplo de flujo de autenticación de la pestaña de tarjeta adaptable." border="false":::

**`tab/fetch` respuesta de autenticación**

El código siguiente proporciona un ejemplo de respuesta de `tab/fetch` autenticación:

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

En el código siguiente se muestra un ejemplo de solicitud reemitida:

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
| Mostrar tarjetas adaptables en Teams pestaña | Microsoft Teams código de ejemplo de pestaña, que muestra cómo mostrar tarjetas adaptables en Teams. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/csharp)| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/nodejs) |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Expansión del vínculo de la pestaña y vista de fases](~/tabs/tabs-link-unfurling.md)

## <a name="see-also"></a>Vea también

* [Tarjeta adaptable](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [pestañas de Teams](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de canal o grupo](~/tabs/how-to/create-channel-group-tab.md)
* [Pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md)
* [Comentarios de finalización de formularios](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)

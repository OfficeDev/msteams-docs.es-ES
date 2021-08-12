---
title: Crear pestañas de tarjeta adaptable
author: KirtiPereira
description: Crear pestañas con tarjetas adaptables
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 6b969461669f9edb7d7f3e216b3b91dd700881b34de17389f8a43348b09830f8
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2021
ms.locfileid: "57705088"
---
# <a name="build-tabs-with-adaptive-cards"></a>Compilar pestañas con tarjetas adaptables

> [!IMPORTANT]
> * Esta característica se encuentra en [Public Developer Preview y](~/resources/dev-preview/developer-preview-intro.md) se admite en dispositivos de escritorio y móviles. La compatibilidad con el explorador web está disponible próximamente.
> * Las pestañas con tarjetas adaptables actualmente solo se admiten como aplicaciones personales.

Al desarrollar una pestaña con el método tradicional, puede encontrarse con estos problemas:

* Consideraciones de HTML y CSS
* Tiempos de carga lentos
* Restricciones de iFrame
* Mantenimiento y costos del servidor

Las pestañas de tarjeta adaptable son una nueva forma de crear pestañas en Teams. En lugar de insertar contenido web en un IFrame, puedes representar tarjetas adaptables en una pestaña. Mientras que el front-end se representa con tarjetas adaptables, el back-end está alimentado por un bot. El bot es responsable de aceptar solicitudes y responder correctamente con la tarjeta adaptable que se representa.

Puedes crear las pestañas con bloques de creación de interfaz de usuario (UI) listos para usar nativos en escritorio, web y móvil. Este artículo te ayuda a comprender los cambios necesarios para realizar el manifiesto de la aplicación. El artículo también identifica cómo la actividad de invocación solicita y envía información en pestaña con tarjetas adaptables y su efecto en el flujo de trabajo del módulo de tareas.

En la siguiente imagen se muestran las pestañas de compilación con tarjetas adaptables en escritorio y móvil:

:::image type="content" source="../../assets/images/tabs/adaptive-cards-rendered-in-tabs.jpg" alt-text="Ejemplo de tarjeta adaptable que se representa en pestañas." border="false":::

## <a name="prerequisites"></a>Requisitos previos

Antes de empezar a usar tarjetas adaptables para crear pestañas, debe:

* Familiarícese con el [desarrollo de bots,](../../bots/what-are-bots.md) [las tarjetas adaptables](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)y los módulos [de](../../task-modules-and-cards/task-modules/task-modules-bots.md) tareas en Teams.
* Hacer que un bot se ejecute Teams para su desarrollo.
* Estar en [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).

## <a name="changes-to-app-manifest"></a>Cambios en el manifiesto de la aplicación

Las aplicaciones personales que representan pestañas deben incluir `staticTabs` una matriz en el manifiesto de la aplicación. Las pestañas de tarjeta adaptable se representan cuando se `contentBotId` proporciona la propiedad en la `staticTab` definición. Las definiciones de tabulación estáticas deben contener una pestaña , que especifique una pestaña Tarjeta adaptable o una , que especifique una experiencia típica de pestaña de contenido `contentBotId` `contentUrl` web hospedado.

> [!NOTE]
> La `contentBotId` propiedad está disponible actualmente en la versión 1.9 del manifiesto o posterior.

Proporcione a la propiedad la ficha Tarjeta adaptable con la que `contentBotId` `botId` debe comunicarse. La ficha Tarjeta adaptable se envía en el parámetro de cada solicitud de invocación y se puede usar para diferenciar las pestañas de tarjeta adaptable que funcionan con `entityId` `tabContext` el mismo bot. Para obtener más información acerca de otros campos de definición de tabulación estática, vea [esquema de manifiesto](../../resources/schema/manifest-schema.md#statictabs).

A continuación se muestra un manifiesto de ficha Tarjeta adaptable de ejemplo:

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

La comunicación entre la pestaña Tarjeta adaptable y el bot se realiza a través de `invoke` actividades. Cada `invoke` actividad tiene un nombre **correspondiente**. Use el nombre de cada actividad para diferenciar cada solicitud. `tab/fetch` y `tab/submit` son las actividades que se tratan en esta sección.

> [!NOTE]
> Los bots deben enviar todas las respuestas a [la dirección URL del servicio](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#base-uri&preserve-view=true). La dirección URL del servicio se recibe como parte de la carga `activity` entrante.

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a>Capturar tarjeta adaptable para representar en una pestaña

`tab/fetch` es la primera solicitud de invocación que recibe el bot cuando un usuario abre una pestaña Tarjeta adaptable. Cuando el bot recibe la solicitud, envía una respuesta **de** tabulación o una respuesta **de autenticación de** tabulación.
La **respuesta** continue incluye una matriz para **tarjetas**, que se representa verticalmente en la pestaña en el orden de la matriz.

> [!NOTE]
> Para obtener más información sobre **la respuesta de** autenticación, vea [authentication](#authentication).

El código siguiente proporciona ejemplos de `tab/fetch` solicitud y respuesta:

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
                }
                {
                    "card": adaptiveCard3
                }  
            ]
        },
    },
    "responseType": "tab"
}
```

### <a name="handle-submits-from-adaptive-card"></a>Controlar envíos desde tarjeta adaptable

Después de representar una tarjeta adaptable en la pestaña, puede responder a las interacciones del usuario. Esta respuesta se controla mediante la `tab/submit` solicitud de invocación.

Cuando un usuario selecciona un botón en la pestaña Tarjeta adaptable, la solicitud se desencadena en el bot con los datos correspondientes a través de la función `tab/submit` `Action.Submit` de tarjeta adaptable. Los datos de la tarjeta adaptable están disponibles a través de la propiedad data de la `tab/submit` solicitud. Recibirá una de las siguientes respuestas a su solicitud:

* Respuesta de código de `200` estado HTTP sin cuerpo. Una respuesta vacía de 200 da como resultado que el cliente no haya realizado ninguna acción.
* La respuesta `200` de la pestaña estándar **continúa,** como se explica [en fetch Adaptive Card](#fetch-adaptive-card-to-render-to-a-tab). Una respuesta **de tabulación** continúa desencadena que el cliente actualice la pestaña Tarjeta adaptable con las tarjetas adaptables proporcionadas en la matriz de tarjetas de **la respuesta** continua.

El código siguiente proporciona ejemplos de `tab/submit` solicitud y respuesta:

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

## <a name="understand-task-module-workflow"></a>Comprender el flujo de trabajo del módulo de tareas

El módulo de tareas también usa la tarjeta adaptable para invocar `task/fetch` y las solicitudes y `task/submit` respuestas. Para obtener más información, [vea using Task Modules in Microsoft Teams bots](../../task-modules-and-cards/task-modules/task-modules-bots.md).

Con la introducción de la pestaña Tarjeta adaptable, hay un cambio en la forma en que el bot responde a una `task/submit` solicitud. Si usa una pestaña Tarjeta adaptable, el bot responde a la solicitud de invocación con la respuesta de la pestaña estándar y `task/submit` cierra el módulo de tareas.  La pestaña Tarjeta adaptable se actualiza representando la nueva lista de tarjetas proporcionadas en el cuerpo de la respuesta de la pestaña **continuar.**

### <a name="invoke-taskfetch"></a>Invocar `task/fetch`

El código siguiente proporciona ejemplos de `task/fetch` solicitud y respuesta:

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

El código siguiente proporciona ejemplos de `task/submit` solicitud y respuesta:

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

En las secciones anteriores, ha visto que la mayoría de los paradigmas de desarrollo se pueden extender desde las solicitudes y respuestas del módulo de tareas a las solicitudes y respuestas de tabulación. Cuando se trata de controlar la autenticación, el flujo de trabajo de la pestaña Tarjeta adaptable sigue el patrón de autenticación para las extensiones de mensajería. Para obtener más información, vea [Agregar autenticación](../../messaging-extensions/how-to/add-authentication.md).

`tab/fetch`las solicitudes pueden tener una **respuesta continue** o **auth.** Cuando se desencadena una solicitud y recibe una respuesta de `tab/fetch` **autenticación de** pestaña, la página de inicio de sesión se muestra al usuario.

**Para obtener un código de autenticación mediante la `tab/fetch` invocación**

1. Abre la aplicación. Aparece la página de inicio de sesión.

    > [!NOTE]
    > El logotipo de la aplicación se proporciona a través de la `icon` propiedad definida en el manifiesto de la aplicación. El título que aparece después de definir el logotipo en la propiedad devuelta en el cuerpo de la `title` **respuesta de autenticación** de tabulación.

1. Seleccione **Iniciar sesión**. Se le redirige a la dirección URL de autenticación proporcionada en la `value` propiedad del cuerpo **de** la respuesta de autenticación.
1. Aparecerá una ventana emergente. Esta ventana emergente hospeda la página web mediante la dirección URL de autenticación.
1. Después de iniciar sesión, cierre la ventana. Se **envía un código** de autenticación al Teams cliente.
1. A continuación, Teams cliente reedición de la solicitud al servicio, que incluye el código de autenticación proporcionado por la `tab/fetch` página web hospedada.

### <a name="tabfetch-authentication-data-flow"></a>`tab/fetch` flujo de datos de autenticación

En la siguiente imagen se proporciona información general sobre cómo funciona el flujo de datos de autenticación para una `tab/fetch` invocación.

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="Ejemplo de flujo de autenticación de ficha de tarjeta adaptable." border="false":::

**`tab/fetch` respuesta de autenticación**

El código siguiente proporciona un ejemplo de `tab/fetch` respuesta de autenticación:

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

El código siguiente muestra un ejemplo de solicitud ree emitida:

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
| Mostrar tarjetas adaptables en Teams pestaña | Microsoft Teams ejemplo de pestaña, que muestra cómo mostrar tarjetas adaptables en Teams. |[Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/csharp)| [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/nodejs) |

## <a name="see-also"></a>Consulte también

* [Tarjeta adaptable](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [Teams pestañas](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de canal o grupo](~/tabs/how-to/create-channel-group-tab.md)
* [Pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Expansión del vínculo de la pestaña y vista de fases](~/tabs/tabs-link-unfurling.md)

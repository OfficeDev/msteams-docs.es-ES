---
title: Crear pestañas de tarjeta adaptable
author: KirtiPereira
description: Crear pestañas con tarjetas adaptables
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: d65fc537b5282c050d891a6a73ff114c630e2c1c
ms.sourcegitcommit: c59d90ae03eae32996db49f162855965b55c52fe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/26/2021
ms.locfileid: "52668851"
---
# <a name="build-tabs-with-adaptive-cards"></a>Compilar pestañas con tarjetas adaptables

> [!IMPORTANT]
> * Esta característica se encuentra en [Public Developer Preview y](~/resources/dev-preview/developer-preview-intro.md) se admite en dispositivos de escritorio y móviles. La compatibilidad con el explorador web está disponible próximamente.
> * Las pestañas con tarjetas adaptables actualmente solo se admiten como aplicaciones personales.

Usa tarjetas adaptables para crear pestañas con facilidad. Puedes crear tus pestañas con bloques de Lego de interfaz de usuario listos para usar que se ven y se sienten nativos en escritorio, web y móvil. Crear pestañas con tarjetas adaptables centraliza todas las funcionalidades de la aplicación Teams en torno a un back-end de bot y un front-end de tarjeta adaptable, lo que elimina la necesidad de un back-end diferente para el bot y las pestañas. Esto reduce en gran medida los costos de servidor y mantenimiento de la Teams aplicación. Este artículo te ayuda a comprender los cambios necesarios para realizar el manifiesto de la aplicación, cómo la actividad de invocación solicita y envía información en pestaña con tarjetas adaptables y el impacto en el flujo de trabajo del módulo de tareas. 

En la siguiente imagen se muestran las pestañas de compilación con tarjetas adaptables en escritorio y móvil: ejemplo de tarjeta :::image type="content" source="../../assets/images/tabs/adaptive-cards-rendered-in-tabs.jpg" alt-text="adaptable representada en pestañas." border="false":::

## <a name="prerequisites"></a>Requisitos previos

Antes de empezar a usar tarjetas adaptables para crear pestañas, debe:

* Familiarícese con el [desarrollo de bots,](../../bots/what-are-bots.md) [las tarjetas adaptables](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)y los módulos [de](../../task-modules-and-cards/task-modules/task-modules-bots.md) tareas en Teams.
* Hacer que un bot se ejecute Teams para su desarrollo.
* Estar en [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).

## <a name="changes-to-app-manifest"></a>Cambios en el manifiesto de la aplicación

Las aplicaciones personales que representan pestañas deben incluir `staticTabs` una matriz en el manifiesto de la aplicación. La pestaña Tarjeta adaptable se representa cuando se `contentBotId` proporciona la propiedad en la `staticTab` definición. Las definiciones de pestaña estáticas deben contener una , que especifique una pestaña de tarjeta adaptable o una , que especifique una experiencia típica de pestaña de contenido `contentBotId` `contentUrl` web hospedado.

> [!NOTE]
> La `contentBotId` propiedad está disponible actualmente en la versión 1.9 del manifiesto o posterior. 

Proporcione a `contentBotId` la propiedad la pestaña de tarjeta adaptable con la que debe `botId` comunicarse. La configuración de la pestaña Tarjeta adaptable se envía en el parámetro de cada solicitud de invocación y se puede usar para diferenciar diferentes pestañas de tarjeta adaptable que funcionan con `entityId` `tabContext` el mismo bot. Para obtener más información acerca de otros campos de definición de tabulación estática, vea [esquema de manifiesto](../../resources/schema/manifest-schema.md#statictabs).

A continuación se muestra un manifiesto de ficha de tarjeta adaptable de ejemplo:

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

La comunicación entre la pestaña tarjeta adaptable y el bot se realiza a través de `invoke` actividades. Cada `invoke` actividad tiene un nombre *correspondiente*. Use el nombre de cada actividad para diferenciar cada solicitud. `tab/fetch` y `tab/submit` son las actividades que se tratan en esta sección.

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a>Capturar tarjeta adaptable para representar en una pestaña

`tab/fetch` es la primera solicitud de invocación que recibe el bot cuando un usuario abre una pestaña de tarjeta adaptable. Cuando el bot recibe la solicitud,  enviará una respuesta de tabulación o una respuesta **de autenticación de** tabulación.
La **respuesta** continue incluye una matriz para **tarjetas**, que se representa verticalmente en la pestaña en el orden de la matriz.

> [!NOTE]
> La **respuesta de** autenticación se explica detalladamente en la sección de [autenticación.](#authentication)

Los siguientes fragmentos de código son ejemplos de `tab/fetch` solicitud y respuesta:

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

Después de representar una tarjeta adaptable en la pestaña, debe poder responder a las interacciones del usuario. Esta respuesta se controla mediante la `tab/submit` solicitud de invocación.

Cuando un usuario selecciona un botón en la pestaña Tarjeta adaptable, la solicitud se desencadena en el bot con los datos correspondientes a través de la función `tab/submit` *Action.Submit* de la tarjeta adaptable. Los datos de la tarjeta adaptable están disponibles a través de la propiedad data de la `tab/submit` solicitud. Recibirá cualquiera de las siguientes respuestas a su solicitud:

* Respuesta de código de `200` estado http sin cuerpo. Una respuesta vacía de 200 dará como resultado que el cliente no haya realizado ninguna acción.
* La pestaña `200` estándar **continúa la** respuesta, como se explica en la sección Capturar [tarjeta adaptable.](#fetch-adaptive-card-to-render-to-a-tab) Una respuesta **de tabulación** continúa desencadena que el cliente actualice la pestaña tarjeta adaptable con las tarjetas adaptables proporcionadas en la matriz de tarjetas de **la respuesta** continua.

Los siguientes fragmentos de código son ejemplos de `tab/submit` solicitud y respuesta:

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

El módulo de tareas también usa la tarjeta adaptable para invocar `task/fetch` y las solicitudes y `task/submit` respuestas. Para obtener más información, vea [Using Task Modules in Microsoft Teams bots](../../task-modules-and-cards/task-modules/task-modules-bots.md).

Sin embargo, con la introducción de la pestaña Tarjeta adaptable, hay un cambio en la forma en que el bot responde a una `task/submit` solicitud. Si usa una pestaña de tarjeta adaptable, el bot responde a la solicitud de invocación con la respuesta de continuación de pestaña estándar y `task/submit` cierra el módulo de tareas.  La pestaña Tarjeta adaptable se actualiza representando la nueva lista de tarjetas proporcionadas en el cuerpo de la respuesta **de** la pestaña Continuar.

### <a name="invoke-taskfetch"></a>Invocar `task/fetch`

Los siguientes fragmentos de código son ejemplos de `task/fetch` solicitud y respuesta:

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

Los siguientes fragmentos de código son ejemplos de `task/submit` solicitud y respuesta:

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

En las secciones anteriores de este artículo, ha visto que la mayoría de los paradigmas de desarrollo podrían extrapolarse de las solicitudes y respuestas del módulo de tareas a las solicitudes y respuestas de tabulación. Sin embargo, cuando se trata de controlar la autenticación, el flujo de trabajo de la pestaña Tarjeta adaptable sigue el patrón de autenticación para las extensiones de mensajería. Para obtener más información, vea [Agregar autenticación](../../messaging-extensions/how-to/add-authentication.md). 

En la [sección actividades de](#invoke-activities) invocación, se le informó de que las solicitudes pueden tener una respuesta de continuar o `tab/fetch`  **de** autenticación. Cuando se desencadena una solicitud y recibe una respuesta de `tab/fetch` **autenticación de** pestaña, la página de inicio de sesión se muestra al usuario. 

**Para obtener un código de autenticación mediante la `tab/fetch` invocación**

1. Abre la aplicación. Aparece la página de inicio de sesión.

    > [!NOTE]
    > El logotipo de la aplicación se proporciona a través de la propiedad definida en el manifiesto de la aplicación y el título que aparece después de definir el logotipo en la propiedad devuelta en el cuerpo de la respuesta de autenticación `icon` `title` de tabulación. 

1. Seleccione **Iniciar sesión**. Se le redirige a la dirección URL de autenticación proporcionada en la `value` propiedad del cuerpo **de** la respuesta de autenticación. 
1. Aparecerá una ventana emergente. Esta ventana emergente hospeda la página web mediante la dirección URL de autenticación.
1. Después de iniciar sesión, cierre la ventana. Se *envía un código* de autenticación al Teams cliente.
1. A continuación, Teams cliente reedición de la solicitud al servicio, que incluye el código de autenticación proporcionado por la `tab/fetch` página web hospedada. 

### <a name="tabfetch-authentication-data-flow"></a>`tab/fetch` flujo de datos de autenticación

En la siguiente imagen se proporciona información general sobre cómo funciona el flujo de datos de autenticación para una `tab/fetch` invocación.

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="Ejemplo de flujo de autenticación de ficha de tarjeta adaptable." border="false":::

**`tab/fetch` respuesta de autenticación**

El siguiente fragmento de código es un ejemplo de `tab/fetch` respuesta de autenticación:

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

A continuación se muestra un ejemplo de solicitud ree emitida:

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

## <a name="see-also"></a>Vea también

> [!div class="nextstepaction"]
> [Tarjeta adaptable](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)


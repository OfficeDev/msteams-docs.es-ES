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
# <a name="build-tabs-with-adaptive-cards"></a><span data-ttu-id="cc707-103">Compilar pestañas con tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="cc707-103">Build tabs with Adaptive Cards</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="cc707-104">Esta característica se encuentra en [Public Developer Preview y](~/resources/dev-preview/developer-preview-intro.md) se admite en dispositivos de escritorio y móviles.</span><span class="sxs-lookup"><span data-stu-id="cc707-104">This feature is in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) and is supported in desktop and mobile.</span></span> <span data-ttu-id="cc707-105">La compatibilidad con el explorador web está disponible próximamente.</span><span class="sxs-lookup"><span data-stu-id="cc707-105">Support in the web browser is coming soon.</span></span>
> * <span data-ttu-id="cc707-106">Las pestañas con tarjetas adaptables actualmente solo se admiten como aplicaciones personales.</span><span class="sxs-lookup"><span data-stu-id="cc707-106">Tabs with Adaptive Cards are currently only supported as personal apps.</span></span>

<span data-ttu-id="cc707-107">Usa tarjetas adaptables para crear pestañas con facilidad.</span><span class="sxs-lookup"><span data-stu-id="cc707-107">Use Adaptive Cards to build tabs with ease.</span></span> <span data-ttu-id="cc707-108">Puedes crear tus pestañas con bloques de Lego de interfaz de usuario listos para usar que se ven y se sienten nativos en escritorio, web y móvil.</span><span class="sxs-lookup"><span data-stu-id="cc707-108">You can build your tabs with ready-made UI Lego-blocks that look and feel native on desktop, web, and mobile.</span></span> <span data-ttu-id="cc707-109">Crear pestañas con tarjetas adaptables centraliza todas las funcionalidades de la aplicación Teams en torno a un back-end de bot y un front-end de tarjeta adaptable, lo que elimina la necesidad de un back-end diferente para el bot y las pestañas.</span><span class="sxs-lookup"><span data-stu-id="cc707-109">Building tabs with Adaptive Cards centralizes all Teams app capabilities around a bot backend and Adaptive Card frontend, thus, eliminating the need for a different backend for your bot and tabs.</span></span> <span data-ttu-id="cc707-110">Esto reduce en gran medida los costos de servidor y mantenimiento de la Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="cc707-110">This greatly reduces server and maintenance costs of your Teams app.</span></span> <span data-ttu-id="cc707-111">Este artículo te ayuda a comprender los cambios necesarios para realizar el manifiesto de la aplicación, cómo la actividad de invocación solicita y envía información en pestaña con tarjetas adaptables y el impacto en el flujo de trabajo del módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="cc707-111">This article helps you understand the changes required to be made to the app manifest, how the invoke activity requests and sends information in tab with Adaptive Cards, and the impact on the task module workflow.</span></span> 

En la siguiente imagen se muestran las pestañas de compilación con tarjetas adaptables en escritorio y móvil: ejemplo de tarjeta :::image type="content" source="../../assets/images/tabs/adaptive-cards-rendered-in-tabs.jpg" alt-text="adaptable representada en pestañas." border="false":::

## <a name="prerequisites"></a><span data-ttu-id="cc707-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cc707-113">Prerequisites</span></span>

<span data-ttu-id="cc707-114">Antes de empezar a usar tarjetas adaptables para crear pestañas, debe:</span><span class="sxs-lookup"><span data-stu-id="cc707-114">Before you start using Adaptive Cards to build tabs, you must:</span></span>

* <span data-ttu-id="cc707-115">Familiarícese con el [desarrollo de bots,](../../bots/what-are-bots.md) [las tarjetas adaptables](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)y los módulos [de](../../task-modules-and-cards/task-modules/task-modules-bots.md) tareas en Teams.</span><span class="sxs-lookup"><span data-stu-id="cc707-115">Be familiar with, [bot development](../../bots/what-are-bots.md), [Adaptive Cards](../../task-modules-and-cards/what-are-cards.md#adaptive-cards), and [Task Modules](../../task-modules-and-cards/task-modules/task-modules-bots.md) in Teams.</span></span>
* <span data-ttu-id="cc707-116">Hacer que un bot se ejecute Teams para su desarrollo.</span><span class="sxs-lookup"><span data-stu-id="cc707-116">Have a bot running in Teams for your development.</span></span>
* <span data-ttu-id="cc707-117">Estar en [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="cc707-117">Be in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

## <a name="changes-to-app-manifest"></a><span data-ttu-id="cc707-118">Cambios en el manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="cc707-118">Changes to app manifest</span></span>

<span data-ttu-id="cc707-119">Las aplicaciones personales que representan pestañas deben incluir `staticTabs` una matriz en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cc707-119">Personal apps that render tabs must include a `staticTabs` array in their app manifest.</span></span> <span data-ttu-id="cc707-120">La pestaña Tarjeta adaptable se representa cuando se `contentBotId` proporciona la propiedad en la `staticTab` definición.</span><span class="sxs-lookup"><span data-stu-id="cc707-120">Adaptive Card Tab are rendered when the `contentBotId` property is provided in the `staticTab` definition.</span></span> <span data-ttu-id="cc707-121">Las definiciones de pestaña estáticas deben contener una , que especifique una pestaña de tarjeta adaptable o una , que especifique una experiencia típica de pestaña de contenido `contentBotId` `contentUrl` web hospedado.</span><span class="sxs-lookup"><span data-stu-id="cc707-121">Static tab definitions must contain either a `contentBotId`, specifying an Adaptive Card Tab or a `contentUrl`, specifying a typical hosted web content tab experience.</span></span>

> [!NOTE]
> <span data-ttu-id="cc707-122">La `contentBotId` propiedad está disponible actualmente en la versión 1.9 del manifiesto o posterior.</span><span class="sxs-lookup"><span data-stu-id="cc707-122">The `contentBotId` property is currently available manifest version 1.9 or later.</span></span> 

<span data-ttu-id="cc707-123">Proporcione a `contentBotId` la propiedad la pestaña de tarjeta adaptable con la que debe `botId` comunicarse.</span><span class="sxs-lookup"><span data-stu-id="cc707-123">Provide the `contentBotId` property with the `botId` that the Adaptive Card Tab must communicate with.</span></span> <span data-ttu-id="cc707-124">La configuración de la pestaña Tarjeta adaptable se envía en el parámetro de cada solicitud de invocación y se puede usar para diferenciar diferentes pestañas de tarjeta adaptable que funcionan con `entityId` `tabContext` el mismo bot.</span><span class="sxs-lookup"><span data-stu-id="cc707-124">The `entityId` configured for the Adaptive Card Tab is sent in the `tabContext` parameter of each invoke request, and can be used to differentiate different Adaptive Card Tabs that are powered by the same bot.</span></span> <span data-ttu-id="cc707-125">Para obtener más información acerca de otros campos de definición de tabulación estática, vea [esquema de manifiesto](../../resources/schema/manifest-schema.md#statictabs).</span><span class="sxs-lookup"><span data-stu-id="cc707-125">For more information about other static tab definition fields, see [manifest schema](../../resources/schema/manifest-schema.md#statictabs).</span></span>

<span data-ttu-id="cc707-126">A continuación se muestra un manifiesto de ficha de tarjeta adaptable de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cc707-126">Following is a sample Adaptive Card Tab manifest:</span></span>

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

## <a name="invoke-activities"></a><span data-ttu-id="cc707-127">Invocar actividades</span><span class="sxs-lookup"><span data-stu-id="cc707-127">Invoke activities</span></span>

<span data-ttu-id="cc707-128">La comunicación entre la pestaña tarjeta adaptable y el bot se realiza a través de `invoke` actividades.</span><span class="sxs-lookup"><span data-stu-id="cc707-128">Communication between your Adaptive Card Tab and your bot is done through `invoke` activities.</span></span> <span data-ttu-id="cc707-129">Cada `invoke` actividad tiene un nombre *correspondiente*.</span><span class="sxs-lookup"><span data-stu-id="cc707-129">Each `invoke` activity has a corresponding *name*.</span></span> <span data-ttu-id="cc707-130">Use el nombre de cada actividad para diferenciar cada solicitud.</span><span class="sxs-lookup"><span data-stu-id="cc707-130">Use the name of each activity to differentiate each request.</span></span> <span data-ttu-id="cc707-131">`tab/fetch` y `tab/submit` son las actividades que se tratan en esta sección.</span><span class="sxs-lookup"><span data-stu-id="cc707-131">`tab/fetch` and `tab/submit` are the activities covered in this section.</span></span>

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a><span data-ttu-id="cc707-132">Capturar tarjeta adaptable para representar en una pestaña</span><span class="sxs-lookup"><span data-stu-id="cc707-132">Fetch Adaptive Card to render to a tab</span></span>

<span data-ttu-id="cc707-133">`tab/fetch` es la primera solicitud de invocación que recibe el bot cuando un usuario abre una pestaña de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="cc707-133">`tab/fetch` is the first invoke request that your bot receives when a user opens an Adaptive Card Tabs.</span></span> <span data-ttu-id="cc707-134">Cuando el bot recibe la solicitud,  enviará una respuesta de tabulación o una respuesta **de autenticación de** tabulación.</span><span class="sxs-lookup"><span data-stu-id="cc707-134">When your bot receives the request, it will either send a tab **continue** response or a tab **auth** response.</span></span>
<span data-ttu-id="cc707-135">La **respuesta** continue incluye una matriz para **tarjetas**, que se representa verticalmente en la pestaña en el orden de la matriz.</span><span class="sxs-lookup"><span data-stu-id="cc707-135">The **continue** response includes an array for **cards**, which is rendered vertically to the tab in the order of the array.</span></span>

> [!NOTE]
> <span data-ttu-id="cc707-136">La **respuesta de** autenticación se explica detalladamente en la sección de [autenticación.](#authentication)</span><span class="sxs-lookup"><span data-stu-id="cc707-136">The **auth** response is explained in detail in the [authentication](#authentication) section.</span></span>

<span data-ttu-id="cc707-137">Los siguientes fragmentos de código son ejemplos de `tab/fetch` solicitud y respuesta:</span><span class="sxs-lookup"><span data-stu-id="cc707-137">The following code snippets are examples of `tab/fetch` request and response:</span></span>

<span data-ttu-id="cc707-138">**`tab/fetch` solicitud**</span><span class="sxs-lookup"><span data-stu-id="cc707-138">**`tab/fetch` request**</span></span>

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

<span data-ttu-id="cc707-139">**`tab/fetch` respuesta**</span><span class="sxs-lookup"><span data-stu-id="cc707-139">**`tab/fetch` response**</span></span>

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

### <a name="handle-submits-from-adaptive-card"></a><span data-ttu-id="cc707-140">Controlar envíos desde tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="cc707-140">Handle submits from Adaptive Card</span></span>

<span data-ttu-id="cc707-141">Después de representar una tarjeta adaptable en la pestaña, debe poder responder a las interacciones del usuario.</span><span class="sxs-lookup"><span data-stu-id="cc707-141">After an Adaptive Card is rendered in the tab, it must be able to respond to user interactions.</span></span> <span data-ttu-id="cc707-142">Esta respuesta se controla mediante la `tab/submit` solicitud de invocación.</span><span class="sxs-lookup"><span data-stu-id="cc707-142">This response is handled by the `tab/submit` invoke request.</span></span>

<span data-ttu-id="cc707-143">Cuando un usuario selecciona un botón en la pestaña Tarjeta adaptable, la solicitud se desencadena en el bot con los datos correspondientes a través de la función `tab/submit` *Action.Submit* de la tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="cc707-143">When a user selects a button on the Adaptive Card Tab, the `tab/submit` request is triggered to your bot with the corresponding data through the *Action.Submit* function of Adaptive Card.</span></span> <span data-ttu-id="cc707-144">Los datos de la tarjeta adaptable están disponibles a través de la propiedad data de la `tab/submit` solicitud.</span><span class="sxs-lookup"><span data-stu-id="cc707-144">The Adaptive Card data is available through the data property of the `tab/submit` request.</span></span> <span data-ttu-id="cc707-145">Recibirá cualquiera de las siguientes respuestas a su solicitud:</span><span class="sxs-lookup"><span data-stu-id="cc707-145">You will receive either of the following responses to your request:</span></span>

* <span data-ttu-id="cc707-146">Respuesta de código de `200` estado http sin cuerpo.</span><span class="sxs-lookup"><span data-stu-id="cc707-146">A http status code `200` response with no body.</span></span> <span data-ttu-id="cc707-147">Una respuesta vacía de 200 dará como resultado que el cliente no haya realizado ninguna acción.</span><span class="sxs-lookup"><span data-stu-id="cc707-147">An empty 200 response will result in no action taken by the client.</span></span>
* <span data-ttu-id="cc707-148">La pestaña `200` estándar **continúa la** respuesta, como se explica en la sección Capturar [tarjeta adaptable.](#fetch-adaptive-card-to-render-to-a-tab)</span><span class="sxs-lookup"><span data-stu-id="cc707-148">The standard `200` tab **continue** response, as explained in [Fetch Adaptive Card](#fetch-adaptive-card-to-render-to-a-tab) section.</span></span> <span data-ttu-id="cc707-149">Una respuesta **de tabulación** continúa desencadena que el cliente actualice la pestaña tarjeta adaptable con las tarjetas adaptables proporcionadas en la matriz de tarjetas de **la respuesta** continua.</span><span class="sxs-lookup"><span data-stu-id="cc707-149">A tab **continue** response triggers the client to update the rendered Adaptive Card Tab with the Adaptive Cards provided in the cards array of the **continue** response.</span></span>

<span data-ttu-id="cc707-150">Los siguientes fragmentos de código son ejemplos de `tab/submit` solicitud y respuesta:</span><span class="sxs-lookup"><span data-stu-id="cc707-150">The following code snippets are examples of `tab/submit` request and response:</span></span>

<span data-ttu-id="cc707-151">**`tab/submit` solicitud**</span><span class="sxs-lookup"><span data-stu-id="cc707-151">**`tab/submit` request**</span></span>

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

<span data-ttu-id="cc707-152">**`tab/submit` respuesta**</span><span class="sxs-lookup"><span data-stu-id="cc707-152">**`tab/submit` response**</span></span>

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

## <a name="understand-task-module-workflow"></a><span data-ttu-id="cc707-153">Comprender el flujo de trabajo del módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="cc707-153">Understand task module workflow</span></span>

<span data-ttu-id="cc707-154">El módulo de tareas también usa la tarjeta adaptable para invocar `task/fetch` y las solicitudes y `task/submit` respuestas.</span><span class="sxs-lookup"><span data-stu-id="cc707-154">The task module also uses Adaptive Card to invoke `task/fetch` and `task/submit` requests and responses.</span></span> <span data-ttu-id="cc707-155">Para obtener más información, vea [Using Task Modules in Microsoft Teams bots](../../task-modules-and-cards/task-modules/task-modules-bots.md).</span><span class="sxs-lookup"><span data-stu-id="cc707-155">For more information, see [Using Task Modules in Microsoft Teams bots](../../task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="cc707-156">Sin embargo, con la introducción de la pestaña Tarjeta adaptable, hay un cambio en la forma en que el bot responde a una `task/submit` solicitud.</span><span class="sxs-lookup"><span data-stu-id="cc707-156">However, with the introduction of Adaptive Card Tab there is a change in how the bot responds to a `task/submit` request.</span></span> <span data-ttu-id="cc707-157">Si usa una pestaña de tarjeta adaptable, el bot responde a la solicitud de invocación con la respuesta de continuación de pestaña estándar y `task/submit` cierra el módulo de tareas. </span><span class="sxs-lookup"><span data-stu-id="cc707-157">If you are using an Adaptive Card Tab, the bot responds to the `task/submit` invoke request with the standard tab **continue** response, and closes the task module.</span></span> <span data-ttu-id="cc707-158">La pestaña Tarjeta adaptable se actualiza representando la nueva lista de tarjetas proporcionadas en el cuerpo de la respuesta **de** la pestaña Continuar.</span><span class="sxs-lookup"><span data-stu-id="cc707-158">The Adaptive Card Tab is updated by rendering the new list of cards provided in the tab **continue** response body.</span></span>

### <a name="invoke-taskfetch"></a><span data-ttu-id="cc707-159">Invocar `task/fetch`</span><span class="sxs-lookup"><span data-stu-id="cc707-159">Invoke `task/fetch`</span></span>

<span data-ttu-id="cc707-160">Los siguientes fragmentos de código son ejemplos de `task/fetch` solicitud y respuesta:</span><span class="sxs-lookup"><span data-stu-id="cc707-160">The following code snippets are examples of `task/fetch` request and response:</span></span>

<span data-ttu-id="cc707-161">**`task/fetch` solicitud**</span><span class="sxs-lookup"><span data-stu-id="cc707-161">**`task/fetch` request**</span></span>
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

<span data-ttu-id="cc707-162">**`task/fetch` respuesta**</span><span class="sxs-lookup"><span data-stu-id="cc707-162">**`task/fetch` response**</span></span>

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

### <a name="invoke-tasksubmit"></a><span data-ttu-id="cc707-163">Invocar `task/submit`</span><span class="sxs-lookup"><span data-stu-id="cc707-163">Invoke `task/submit`</span></span>

<span data-ttu-id="cc707-164">Los siguientes fragmentos de código son ejemplos de `task/submit` solicitud y respuesta:</span><span class="sxs-lookup"><span data-stu-id="cc707-164">The following code snippets are examples of `task/submit` request and response:</span></span>

<span data-ttu-id="cc707-165">**`task/submit` solicitud**</span><span class="sxs-lookup"><span data-stu-id="cc707-165">**`task/submit` request**</span></span>

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

<span data-ttu-id="cc707-166">**`task/submit` tipo de respuesta tab**</span><span class="sxs-lookup"><span data-stu-id="cc707-166">**`task/submit` tab response type**</span></span>

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

## <a name="authentication"></a><span data-ttu-id="cc707-167">Autenticación</span><span class="sxs-lookup"><span data-stu-id="cc707-167">Authentication</span></span>

<span data-ttu-id="cc707-168">En las secciones anteriores de este artículo, ha visto que la mayoría de los paradigmas de desarrollo podrían extrapolarse de las solicitudes y respuestas del módulo de tareas a las solicitudes y respuestas de tabulación.</span><span class="sxs-lookup"><span data-stu-id="cc707-168">In the previous sections of this article, you have seen that most of the development paradigms could be extrapolated from the task module requests and responses into tab requests and responses.</span></span> <span data-ttu-id="cc707-169">Sin embargo, cuando se trata de controlar la autenticación, el flujo de trabajo de la pestaña Tarjeta adaptable sigue el patrón de autenticación para las extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="cc707-169">However, when it comes to handling authentication, the workflow for Adaptive Card Tab follows the authentication pattern for messaging extensions.</span></span> <span data-ttu-id="cc707-170">Para obtener más información, vea [Agregar autenticación](../../messaging-extensions/how-to/add-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="cc707-170">For more information, see [add authentication](../../messaging-extensions/how-to/add-authentication.md).</span></span> 

<span data-ttu-id="cc707-171">En la [sección actividades de](#invoke-activities) invocación, se le informó de que las solicitudes pueden tener una respuesta de continuar o `tab/fetch`  **de** autenticación.</span><span class="sxs-lookup"><span data-stu-id="cc707-171">In the [invoke activities](#invoke-activities) section, you were informed that `tab/fetch` requests can have either a **continue** or an **auth** response.</span></span> <span data-ttu-id="cc707-172">Cuando se desencadena una solicitud y recibe una respuesta de `tab/fetch` **autenticación de** pestaña, la página de inicio de sesión se muestra al usuario.</span><span class="sxs-lookup"><span data-stu-id="cc707-172">When a `tab/fetch` request is triggered and receives a tab **auth** response, the sign-in page is shown to the user.</span></span> 

<span data-ttu-id="cc707-173">**Para obtener un código de autenticación mediante la `tab/fetch` invocación**</span><span class="sxs-lookup"><span data-stu-id="cc707-173">**To get an authentication code through `tab/fetch` invoke**</span></span>

1. <span data-ttu-id="cc707-174">Abre la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cc707-174">Open your app.</span></span> <span data-ttu-id="cc707-175">Aparece la página de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="cc707-175">The sign in page appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cc707-176">El logotipo de la aplicación se proporciona a través de la propiedad definida en el manifiesto de la aplicación y el título que aparece después de definir el logotipo en la propiedad devuelta en el cuerpo de la respuesta de autenticación `icon` `title` de tabulación. </span><span class="sxs-lookup"><span data-stu-id="cc707-176">The app logo is provided through the `icon` property defined in the app manifest, and the title appearing after the logo is defined in the `title` property returned in the tab **auth** response body.</span></span>

1. <span data-ttu-id="cc707-177">Seleccione **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="cc707-177">Select **Sign in**.</span></span> <span data-ttu-id="cc707-178">Se le redirige a la dirección URL de autenticación proporcionada en la `value` propiedad del cuerpo **de** la respuesta de autenticación.</span><span class="sxs-lookup"><span data-stu-id="cc707-178">You are redirected to the authentication URL provided in the `value` property of the **auth** response body.</span></span> 
1. <span data-ttu-id="cc707-179">Aparecerá una ventana emergente.</span><span class="sxs-lookup"><span data-stu-id="cc707-179">A pop-up window appears.</span></span> <span data-ttu-id="cc707-180">Esta ventana emergente hospeda la página web mediante la dirección URL de autenticación.</span><span class="sxs-lookup"><span data-stu-id="cc707-180">This pop-up window hosts your web page using the authentication URL.</span></span>
1. <span data-ttu-id="cc707-181">Después de iniciar sesión, cierre la ventana.</span><span class="sxs-lookup"><span data-stu-id="cc707-181">After you sign in, close the window.</span></span> <span data-ttu-id="cc707-182">Se *envía un código* de autenticación al Teams cliente.</span><span class="sxs-lookup"><span data-stu-id="cc707-182">An *authentication code* is sent to the Teams client.</span></span>
1. <span data-ttu-id="cc707-183">A continuación, Teams cliente reedición de la solicitud al servicio, que incluye el código de autenticación proporcionado por la `tab/fetch` página web hospedada.</span><span class="sxs-lookup"><span data-stu-id="cc707-183">The Teams client then reissues the `tab/fetch` request to your service, which includes the authentication code provided by your hosted web page.</span></span> 

### <a name="tabfetch-authentication-data-flow"></a><span data-ttu-id="cc707-184">`tab/fetch` flujo de datos de autenticación</span><span class="sxs-lookup"><span data-stu-id="cc707-184">`tab/fetch` authentication data flow</span></span>

<span data-ttu-id="cc707-185">En la siguiente imagen se proporciona información general sobre cómo funciona el flujo de datos de autenticación para una `tab/fetch` invocación.</span><span class="sxs-lookup"><span data-stu-id="cc707-185">The following image provides an overview of how the authentication data flow works for a `tab/fetch` invoke.</span></span>

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="Ejemplo de flujo de autenticación de ficha de tarjeta adaptable." border="false":::

<span data-ttu-id="cc707-187">**`tab/fetch` respuesta de autenticación**</span><span class="sxs-lookup"><span data-stu-id="cc707-187">**`tab/fetch` auth response**</span></span>

<span data-ttu-id="cc707-188">El siguiente fragmento de código es un ejemplo de `tab/fetch` respuesta de autenticación:</span><span class="sxs-lookup"><span data-stu-id="cc707-188">The following code snippet is an example of `tab/fetch` auth response:</span></span>

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

### <a name="example"></a><span data-ttu-id="cc707-189">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="cc707-189">Example</span></span>

<span data-ttu-id="cc707-190">A continuación se muestra un ejemplo de solicitud ree emitida:</span><span class="sxs-lookup"><span data-stu-id="cc707-190">The following shows a reissued request example:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="cc707-191">Consulte también</span><span class="sxs-lookup"><span data-stu-id="cc707-191">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cc707-192">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="cc707-192">Adaptive Card</span></span>](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)


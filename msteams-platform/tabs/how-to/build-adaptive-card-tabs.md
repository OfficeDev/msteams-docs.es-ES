---
title: Crear pestañas de tarjeta adaptable
author: KirtiPereira
description: Crear pestañas con tarjetas adaptables
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 4359b20d5839b86955082b7a5da8db262e13600c
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179905"
---
# <a name="build-tabs-with-adaptive-cards"></a><span data-ttu-id="85cd8-103">Compilar pestañas con tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="85cd8-103">Build tabs with Adaptive Cards</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="85cd8-104">Esta característica se encuentra en [Public Developer Preview y](~/resources/dev-preview/developer-preview-intro.md) se admite en dispositivos de escritorio y móviles.</span><span class="sxs-lookup"><span data-stu-id="85cd8-104">This feature is in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) and is supported in desktop and mobile.</span></span> <span data-ttu-id="85cd8-105">La compatibilidad con el explorador web está disponible próximamente.</span><span class="sxs-lookup"><span data-stu-id="85cd8-105">Support in the web browser is coming soon.</span></span>
> * <span data-ttu-id="85cd8-106">Las pestañas con tarjetas adaptables actualmente solo se admiten como aplicaciones personales.</span><span class="sxs-lookup"><span data-stu-id="85cd8-106">Tabs with Adaptive Cards are currently only supported as personal apps.</span></span>

<span data-ttu-id="85cd8-107">Al desarrollar una pestaña con el método tradicional, es posible que se deba a estos problemas, como consideraciones de HTML y CSS, tiempos de carga lentos, restricciones de iFrame y costos y mantenimiento del servidor.</span><span class="sxs-lookup"><span data-stu-id="85cd8-107">When developing a tab using the traditional method, you might run into these issues, such as HTML and CSS considerations, slow load times, iFrame constraints, and server maintenance and costs.</span></span> <span data-ttu-id="85cd8-108">Las pestañas de tarjeta adaptable son una nueva forma de crear pestañas en Teams.</span><span class="sxs-lookup"><span data-stu-id="85cd8-108">Adaptive Card tabs is a new way to build tabs in Teams.</span></span> <span data-ttu-id="85cd8-109">En lugar de insertar contenido web en un IFrame, puedes representar tarjetas adaptables en una pestaña. Mientras que el front-end se representa con tarjetas adaptables, el back-end está alimentado por un bot.</span><span class="sxs-lookup"><span data-stu-id="85cd8-109">Instead of embedding web content in an IFrame, you can render Adaptive Cards to a tab. While the front-end is rendered with Adaptive Cards, the backend is powered by a bot.</span></span> <span data-ttu-id="85cd8-110">El bot es responsable de aceptar solicitudes y responder correctamente con la tarjeta adaptable que se representa.</span><span class="sxs-lookup"><span data-stu-id="85cd8-110">The bot is responsible for accepting requests and responding appropriately with the Adaptive Card that is rendered.</span></span>

<span data-ttu-id="85cd8-111">Puedes crear tus pestañas con bloques de Lego de interfaz de usuario (UI) listos para usar que se ven y se sienten nativos en escritorio, web y móvil.</span><span class="sxs-lookup"><span data-stu-id="85cd8-111">You can build your tabs with ready-made user interface (UI) Lego-blocks that look and feel native on desktop, web, and mobile.</span></span> <span data-ttu-id="85cd8-112">Este artículo te ayuda a comprender los cambios necesarios para realizar el manifiesto de la aplicación, cómo la actividad de invocación solicita y envía información en pestaña con tarjetas adaptables y el impacto en el flujo de trabajo del módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="85cd8-112">This article helps you understand the changes required to be made to the app manifest, how the invoke activity requests and sends information in tab with Adaptive Cards, and the impact on the task module workflow.</span></span>

<span data-ttu-id="85cd8-113">En la siguiente imagen se muestran las pestañas de compilación con tarjetas adaptables en escritorio y móvil:</span><span class="sxs-lookup"><span data-stu-id="85cd8-113">The following image depicts build tabs with Adaptive Cards in desktop and mobile:</span></span>

:::image type="content" source="../../assets/images/tabs/adaptive-cards-rendered-in-tabs.jpg" alt-text="Ejemplo de tarjeta adaptable que se representa en pestañas." border="false":::

## <a name="prerequisites"></a><span data-ttu-id="85cd8-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="85cd8-115">Prerequisites</span></span>

<span data-ttu-id="85cd8-116">Antes de empezar a usar tarjetas adaptables para crear pestañas, debe:</span><span class="sxs-lookup"><span data-stu-id="85cd8-116">Before you start using Adaptive Cards to build tabs, you must:</span></span>

* <span data-ttu-id="85cd8-117">Familiarícese con el [desarrollo de bots,](../../bots/what-are-bots.md) [las tarjetas adaptables](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)y los módulos [de](../../task-modules-and-cards/task-modules/task-modules-bots.md) tareas en Teams.</span><span class="sxs-lookup"><span data-stu-id="85cd8-117">Be familiar with, [bot development](../../bots/what-are-bots.md), [Adaptive Cards](../../task-modules-and-cards/what-are-cards.md#adaptive-cards), and [task modules](../../task-modules-and-cards/task-modules/task-modules-bots.md) in Teams.</span></span>
* <span data-ttu-id="85cd8-118">Hacer que un bot se ejecute Teams para su desarrollo.</span><span class="sxs-lookup"><span data-stu-id="85cd8-118">Have a bot running in Teams for your development.</span></span>
* <span data-ttu-id="85cd8-119">Estar en [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="85cd8-119">Be in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

## <a name="changes-to-app-manifest"></a><span data-ttu-id="85cd8-120">Cambios en el manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="85cd8-120">Changes to app manifest</span></span>

<span data-ttu-id="85cd8-121">Las aplicaciones personales que representan pestañas deben incluir `staticTabs` una matriz en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="85cd8-121">Personal apps that render tabs must include a `staticTabs` array in their app manifest.</span></span> <span data-ttu-id="85cd8-122">Las pestañas de tarjeta adaptable se representan cuando se `contentBotId` proporciona la propiedad en la `staticTab` definición.</span><span class="sxs-lookup"><span data-stu-id="85cd8-122">Adaptive Card tabs are rendered when the `contentBotId` property is provided in the `staticTab` definition.</span></span> <span data-ttu-id="85cd8-123">Las definiciones de tabulación estáticas deben contener una pestaña , que especifique una pestaña Tarjeta adaptable o una , que especifique una experiencia típica de pestaña de contenido `contentBotId` `contentUrl` web hospedado.</span><span class="sxs-lookup"><span data-stu-id="85cd8-123">Static tab definitions must contain either a `contentBotId`, specifying an Adaptive Card tab or a `contentUrl`, specifying a typical hosted web content tab experience.</span></span>

> [!NOTE]
> <span data-ttu-id="85cd8-124">La `contentBotId` propiedad está disponible actualmente en la versión 1.9 del manifiesto o posterior.</span><span class="sxs-lookup"><span data-stu-id="85cd8-124">The `contentBotId` property is currently available in manifest version 1.9 or later.</span></span>

<span data-ttu-id="85cd8-125">Proporcione a la propiedad la ficha Tarjeta adaptable con la que `contentBotId` `botId` debe comunicarse.</span><span class="sxs-lookup"><span data-stu-id="85cd8-125">Provide the `contentBotId` property with the `botId` that the Adaptive Card tab must communicate with.</span></span> <span data-ttu-id="85cd8-126">La ficha Tarjeta adaptable se envía en el parámetro de cada solicitud de invocación y se puede usar para diferenciar las pestañas de tarjeta adaptable que funcionan con `entityId` `tabContext` el mismo bot.</span><span class="sxs-lookup"><span data-stu-id="85cd8-126">The `entityId` configured for the Adaptive Card tab is sent in the `tabContext` parameter of each invoke request, and can be used to differentiate Adaptive Card Tabs that are powered by the same bot.</span></span> <span data-ttu-id="85cd8-127">Para obtener más información acerca de otros campos de definición de tabulación estática, vea [esquema de manifiesto](../../resources/schema/manifest-schema.md#statictabs).</span><span class="sxs-lookup"><span data-stu-id="85cd8-127">For more information about other static tab definition fields, see [manifest schema](../../resources/schema/manifest-schema.md#statictabs).</span></span>

<span data-ttu-id="85cd8-128">A continuación se muestra un manifiesto de ficha Tarjeta adaptable de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="85cd8-128">Following is a sample Adaptive Card tab manifest:</span></span>

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

## <a name="invoke-activities"></a><span data-ttu-id="85cd8-129">Invocar actividades</span><span class="sxs-lookup"><span data-stu-id="85cd8-129">Invoke activities</span></span>

<span data-ttu-id="85cd8-130">La comunicación entre la pestaña Tarjeta adaptable y el bot se realiza a través de `invoke` actividades.</span><span class="sxs-lookup"><span data-stu-id="85cd8-130">Communication between your Adaptive Card tab and your bot is done through `invoke` activities.</span></span> <span data-ttu-id="85cd8-131">Cada `invoke` actividad tiene un nombre **correspondiente**.</span><span class="sxs-lookup"><span data-stu-id="85cd8-131">Each `invoke` activity has a corresponding **name**.</span></span> <span data-ttu-id="85cd8-132">Use el nombre de cada actividad para diferenciar cada solicitud.</span><span class="sxs-lookup"><span data-stu-id="85cd8-132">Use the name of each activity to differentiate each request.</span></span> <span data-ttu-id="85cd8-133">`tab/fetch` y `tab/submit` son las actividades que se tratan en esta sección.</span><span class="sxs-lookup"><span data-stu-id="85cd8-133">`tab/fetch` and `tab/submit` are the activities covered in this section.</span></span>

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a><span data-ttu-id="85cd8-134">Capturar tarjeta adaptable para representar en una pestaña</span><span class="sxs-lookup"><span data-stu-id="85cd8-134">Fetch Adaptive Card to render to a tab</span></span>

<span data-ttu-id="85cd8-135">`tab/fetch` es la primera solicitud de invocación que recibe el bot cuando un usuario abre una pestaña Tarjeta adaptable. Cuando el bot recibe la solicitud, envía una respuesta **de** tabulación o una respuesta **de autenticación de** tabulación.</span><span class="sxs-lookup"><span data-stu-id="85cd8-135">`tab/fetch` is the first invoke request that your bot receives when a user opens an Adaptive Card tab. When your bot receives the request, it either sends a tab **continue** response or a tab **auth** response.</span></span>
<span data-ttu-id="85cd8-136">La **respuesta** continue incluye una matriz para **tarjetas**, que se representa verticalmente en la pestaña en el orden de la matriz.</span><span class="sxs-lookup"><span data-stu-id="85cd8-136">The **continue** response includes an array for **cards**, which is rendered vertically to the tab in the order of the array.</span></span>

> [!NOTE]
> <span data-ttu-id="85cd8-137">Para obtener más información sobre **la respuesta de** autenticación, vea [authentication](#authentication).</span><span class="sxs-lookup"><span data-stu-id="85cd8-137">For more information on **auth** response, see [authentication](#authentication).</span></span>

<span data-ttu-id="85cd8-138">El código siguiente proporciona ejemplos de `tab/fetch` solicitud y respuesta:</span><span class="sxs-lookup"><span data-stu-id="85cd8-138">The following code provides examples of `tab/fetch` request and response:</span></span>

<span data-ttu-id="85cd8-139">**`tab/fetch` solicitud**</span><span class="sxs-lookup"><span data-stu-id="85cd8-139">**`tab/fetch` request**</span></span>

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

<span data-ttu-id="85cd8-140">**`tab/fetch` respuesta**</span><span class="sxs-lookup"><span data-stu-id="85cd8-140">**`tab/fetch` response**</span></span>

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

### <a name="handle-submits-from-adaptive-card"></a><span data-ttu-id="85cd8-141">Controlar envíos desde tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="85cd8-141">Handle submits from Adaptive Card</span></span>

<span data-ttu-id="85cd8-142">Después de representar una tarjeta adaptable en la pestaña, debe poder responder a las interacciones del usuario.</span><span class="sxs-lookup"><span data-stu-id="85cd8-142">After an Adaptive Card is rendered in the tab, it must be able to respond to user interactions.</span></span> <span data-ttu-id="85cd8-143">Esta respuesta se controla mediante la `tab/submit` solicitud de invocación.</span><span class="sxs-lookup"><span data-stu-id="85cd8-143">This response is handled by the `tab/submit` invoke request.</span></span>

<span data-ttu-id="85cd8-144">Cuando un usuario selecciona un botón en la pestaña Tarjeta adaptable, la solicitud se desencadena en el bot con los datos correspondientes a través de la función `tab/submit` `Action.Submit` de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="85cd8-144">When a user selects a button on the Adaptive Card tab, the `tab/submit` request is triggered to your bot with the corresponding data through the `Action.Submit` function of Adaptive Card.</span></span> <span data-ttu-id="85cd8-145">Los datos de la tarjeta adaptable están disponibles a través de la propiedad data de la `tab/submit` solicitud.</span><span class="sxs-lookup"><span data-stu-id="85cd8-145">The Adaptive Card data is available through the data property of the `tab/submit` request.</span></span> <span data-ttu-id="85cd8-146">Recibirá una de las siguientes respuestas a su solicitud:</span><span class="sxs-lookup"><span data-stu-id="85cd8-146">You receive either of the following responses to your request:</span></span>

* <span data-ttu-id="85cd8-147">Respuesta de código de `200` estado HTTP sin cuerpo.</span><span class="sxs-lookup"><span data-stu-id="85cd8-147">An HTTP status code `200` response with no body.</span></span> <span data-ttu-id="85cd8-148">Una respuesta vacía de 200 da como resultado que el cliente no haya realizado ninguna acción.</span><span class="sxs-lookup"><span data-stu-id="85cd8-148">An empty 200 response results in no action taken by the client.</span></span>
* <span data-ttu-id="85cd8-149">La respuesta `200` de la pestaña estándar **continúa,** como se explica [en fetch Adaptive Card](#fetch-adaptive-card-to-render-to-a-tab).</span><span class="sxs-lookup"><span data-stu-id="85cd8-149">The standard `200` tab **continue** response, as explained in [fetch Adaptive Card](#fetch-adaptive-card-to-render-to-a-tab).</span></span> <span data-ttu-id="85cd8-150">Una respuesta **de tabulación** continúa desencadena que el cliente actualice la pestaña Tarjeta adaptable con las tarjetas adaptables proporcionadas en la matriz de tarjetas de **la respuesta** continua.</span><span class="sxs-lookup"><span data-stu-id="85cd8-150">A tab **continue** response triggers the client to update the rendered Adaptive Card tab with the Adaptive Cards provided in the cards array of the **continue** response.</span></span>

<span data-ttu-id="85cd8-151">El código siguiente proporciona ejemplos de `tab/submit` solicitud y respuesta:</span><span class="sxs-lookup"><span data-stu-id="85cd8-151">The following code provides examples of `tab/submit` request and response:</span></span>

<span data-ttu-id="85cd8-152">**`tab/submit` solicitud**</span><span class="sxs-lookup"><span data-stu-id="85cd8-152">**`tab/submit` request**</span></span>

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

<span data-ttu-id="85cd8-153">**`tab/submit` respuesta**</span><span class="sxs-lookup"><span data-stu-id="85cd8-153">**`tab/submit` response**</span></span>

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

## <a name="understand-task-module-workflow"></a><span data-ttu-id="85cd8-154">Comprender el flujo de trabajo del módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="85cd8-154">Understand task module workflow</span></span>

<span data-ttu-id="85cd8-155">El módulo de tareas también usa la tarjeta adaptable para invocar `task/fetch` y las solicitudes y `task/submit` respuestas.</span><span class="sxs-lookup"><span data-stu-id="85cd8-155">The task module also uses Adaptive Card to invoke `task/fetch` and `task/submit` requests and responses.</span></span> <span data-ttu-id="85cd8-156">Para obtener más información, [vea using Task Modules in Microsoft Teams bots](../../task-modules-and-cards/task-modules/task-modules-bots.md).</span><span class="sxs-lookup"><span data-stu-id="85cd8-156">For more information, see [using Task Modules in Microsoft Teams bots](../../task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="85cd8-157">Con la introducción de la pestaña Tarjeta adaptable, hay un cambio en la forma en que el bot responde a una `task/submit` solicitud.</span><span class="sxs-lookup"><span data-stu-id="85cd8-157">With the introduction of Adaptive Card tab, there is a change in how the bot responds to a `task/submit` request.</span></span> <span data-ttu-id="85cd8-158">Si usa una pestaña Tarjeta adaptable, el bot responde a la solicitud de invocación con la respuesta de la pestaña estándar y `task/submit` cierra el módulo de tareas. </span><span class="sxs-lookup"><span data-stu-id="85cd8-158">If you are using an Adaptive Card tab, the bot responds to the `task/submit` invoke request with the standard tab **continue** response, and closes the task module.</span></span> <span data-ttu-id="85cd8-159">La pestaña Tarjeta adaptable se actualiza representando la nueva lista de tarjetas proporcionadas en el cuerpo de la respuesta de la pestaña **continuar.**</span><span class="sxs-lookup"><span data-stu-id="85cd8-159">The Adaptive Card tab is updated by rendering the new list of cards provided in the tab **continue** response body.</span></span>

### <a name="invoke-taskfetch"></a><span data-ttu-id="85cd8-160">Invocar `task/fetch`</span><span class="sxs-lookup"><span data-stu-id="85cd8-160">Invoke `task/fetch`</span></span>

<span data-ttu-id="85cd8-161">El código siguiente proporciona ejemplos de `task/fetch` solicitud y respuesta:</span><span class="sxs-lookup"><span data-stu-id="85cd8-161">The following code provides examples of `task/fetch` request and response:</span></span>

<span data-ttu-id="85cd8-162">**`task/fetch` solicitud**</span><span class="sxs-lookup"><span data-stu-id="85cd8-162">**`task/fetch` request**</span></span>
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

<span data-ttu-id="85cd8-163">**`task/fetch` respuesta**</span><span class="sxs-lookup"><span data-stu-id="85cd8-163">**`task/fetch` response**</span></span>

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

### <a name="invoke-tasksubmit"></a><span data-ttu-id="85cd8-164">Invocar `task/submit`</span><span class="sxs-lookup"><span data-stu-id="85cd8-164">Invoke `task/submit`</span></span>

<span data-ttu-id="85cd8-165">El código siguiente proporciona ejemplos de `task/submit` solicitud y respuesta:</span><span class="sxs-lookup"><span data-stu-id="85cd8-165">The following code provides examples of `task/submit` request and response:</span></span>

<span data-ttu-id="85cd8-166">**`task/submit` solicitud**</span><span class="sxs-lookup"><span data-stu-id="85cd8-166">**`task/submit` request**</span></span>

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

<span data-ttu-id="85cd8-167">**`task/submit` tipo de respuesta tab**</span><span class="sxs-lookup"><span data-stu-id="85cd8-167">**`task/submit` tab response type**</span></span>

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

## <a name="authentication"></a><span data-ttu-id="85cd8-168">Autenticación</span><span class="sxs-lookup"><span data-stu-id="85cd8-168">Authentication</span></span>

<span data-ttu-id="85cd8-169">En las secciones anteriores de este artículo, ha visto que la mayoría de los paradigmas de desarrollo se pueden extender desde las solicitudes y respuestas del módulo de tareas a las solicitudes y respuestas de tabulación.</span><span class="sxs-lookup"><span data-stu-id="85cd8-169">In the previous sections of this article, you have seen that most of the development paradigms can be extended from the task module requests and responses into tab requests and responses.</span></span> <span data-ttu-id="85cd8-170">Cuando se trata de controlar la autenticación, el flujo de trabajo de la pestaña Tarjeta adaptable sigue el patrón de autenticación para las extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="85cd8-170">When it comes to handling authentication, the workflow for Adaptive Card tab follows the authentication pattern for messaging extensions.</span></span> <span data-ttu-id="85cd8-171">Para obtener más información, vea [Agregar autenticación](../../messaging-extensions/how-to/add-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="85cd8-171">For more information, see [add authentication](../../messaging-extensions/how-to/add-authentication.md).</span></span>

<span data-ttu-id="85cd8-172">`tab/fetch`las solicitudes pueden tener una **respuesta continue** o **auth.**</span><span class="sxs-lookup"><span data-stu-id="85cd8-172">`tab/fetch` requests can have either a **continue** or an **auth** response.</span></span> <span data-ttu-id="85cd8-173">Cuando se desencadena una solicitud y recibe una respuesta de `tab/fetch` **autenticación de** pestaña, la página de inicio de sesión se muestra al usuario.</span><span class="sxs-lookup"><span data-stu-id="85cd8-173">When a `tab/fetch` request is triggered and receives a tab **auth** response, the sign-in page is shown to the user.</span></span>

<span data-ttu-id="85cd8-174">**Para obtener un código de autenticación mediante la `tab/fetch` invocación**</span><span class="sxs-lookup"><span data-stu-id="85cd8-174">**To get an authentication code through `tab/fetch` invoke**</span></span>

1. <span data-ttu-id="85cd8-175">Abre la aplicación.</span><span class="sxs-lookup"><span data-stu-id="85cd8-175">Open your app.</span></span> <span data-ttu-id="85cd8-176">Aparece la página de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="85cd8-176">The sign in page appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="85cd8-177">El logotipo de la aplicación se proporciona a través de la `icon` propiedad definida en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="85cd8-177">The app logo is provided through the `icon` property defined in the app manifest.</span></span> <span data-ttu-id="85cd8-178">El título que aparece después de definir el logotipo en la propiedad devuelta en el cuerpo de la `title` **respuesta de autenticación** de tabulación.</span><span class="sxs-lookup"><span data-stu-id="85cd8-178">The title appearing after the logo is defined in the `title` property returned in the tab **auth** response body.</span></span>

1. <span data-ttu-id="85cd8-179">Seleccione **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="85cd8-179">Select **Sign in**.</span></span> <span data-ttu-id="85cd8-180">Se le redirige a la dirección URL de autenticación proporcionada en la `value` propiedad del cuerpo **de** la respuesta de autenticación.</span><span class="sxs-lookup"><span data-stu-id="85cd8-180">You are redirected to the authentication URL provided in the `value` property of the **auth** response body.</span></span>
1. <span data-ttu-id="85cd8-181">Aparecerá una ventana emergente.</span><span class="sxs-lookup"><span data-stu-id="85cd8-181">A pop-up window appears.</span></span> <span data-ttu-id="85cd8-182">Esta ventana emergente hospeda la página web mediante la dirección URL de autenticación.</span><span class="sxs-lookup"><span data-stu-id="85cd8-182">This pop-up window hosts your web page using the authentication URL.</span></span>
1. <span data-ttu-id="85cd8-183">Después de iniciar sesión, cierre la ventana.</span><span class="sxs-lookup"><span data-stu-id="85cd8-183">After you sign in, close the window.</span></span> <span data-ttu-id="85cd8-184">Se **envía un código** de autenticación al Teams cliente.</span><span class="sxs-lookup"><span data-stu-id="85cd8-184">An **authentication code** is sent to the Teams client.</span></span>
1. <span data-ttu-id="85cd8-185">A continuación, Teams cliente reedición de la solicitud al servicio, que incluye el código de autenticación proporcionado por la `tab/fetch` página web hospedada.</span><span class="sxs-lookup"><span data-stu-id="85cd8-185">The Teams client then reissues the `tab/fetch` request to your service, which includes the authentication code provided by your hosted web page.</span></span>

### <a name="tabfetch-authentication-data-flow"></a><span data-ttu-id="85cd8-186">`tab/fetch` flujo de datos de autenticación</span><span class="sxs-lookup"><span data-stu-id="85cd8-186">`tab/fetch` authentication data flow</span></span>

<span data-ttu-id="85cd8-187">En la siguiente imagen se proporciona información general sobre cómo funciona el flujo de datos de autenticación para una `tab/fetch` invocación.</span><span class="sxs-lookup"><span data-stu-id="85cd8-187">The following image provides an overview of how the authentication data flow works for a `tab/fetch` invoke.</span></span>

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="Ejemplo de flujo de autenticación de ficha de tarjeta adaptable." border="false":::

<span data-ttu-id="85cd8-189">**`tab/fetch` respuesta de autenticación**</span><span class="sxs-lookup"><span data-stu-id="85cd8-189">**`tab/fetch` auth response**</span></span>

<span data-ttu-id="85cd8-190">El código siguiente proporciona un ejemplo de `tab/fetch` respuesta de autenticación:</span><span class="sxs-lookup"><span data-stu-id="85cd8-190">The following code provides an example of `tab/fetch` auth response:</span></span>

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

### <a name="example"></a><span data-ttu-id="85cd8-191">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="85cd8-191">Example</span></span>

<span data-ttu-id="85cd8-192">El código siguiente muestra un ejemplo de solicitud ree emitida:</span><span class="sxs-lookup"><span data-stu-id="85cd8-192">The following code shows a reissued request example:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="85cd8-193">Vea también</span><span class="sxs-lookup"><span data-stu-id="85cd8-193">See also</span></span>

* [<span data-ttu-id="85cd8-194">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="85cd8-194">Adaptive Card</span></span>](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [<span data-ttu-id="85cd8-195">Teams pestañas</span><span class="sxs-lookup"><span data-stu-id="85cd8-195">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="85cd8-196">Crear una pestaña personal</span><span class="sxs-lookup"><span data-stu-id="85cd8-196">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="85cd8-197">Crear una pestaña de canal o grupo</span><span class="sxs-lookup"><span data-stu-id="85cd8-197">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="85cd8-198">Pestañas en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="85cd8-198">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)

## <a name="next-step"></a><span data-ttu-id="85cd8-199">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="85cd8-199">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="85cd8-200">Expansión del vínculo de la pestaña y vista de fases</span><span class="sxs-lookup"><span data-stu-id="85cd8-200">Tabs link unfurling and Stage View</span></span>](~/tabs/tabs-link-unfurling.md)
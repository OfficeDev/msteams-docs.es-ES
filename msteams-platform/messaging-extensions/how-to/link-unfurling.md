---
title: Apertura de vínculos
author: clearab
description: Cómo realizar la implementación de vínculos con la extensión de mensajería en una aplicación de Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 628c5e760a4bc038443a20714e6960f1ffe8a2ad
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696236"
---
# <a name="link-unfurling"></a><span data-ttu-id="e1600-103">Apertura de vínculos</span><span class="sxs-lookup"><span data-stu-id="e1600-103">Link unfurling</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="e1600-104">Este documento te guía sobre cómo agregar la actualización de vínculos al manifiesto de la aplicación con App studio y manualmente.</span><span class="sxs-lookup"><span data-stu-id="e1600-104">This document guides you on how to add link unfurling to your app manifest using App studio and manually.</span></span> <span data-ttu-id="e1600-105">Con la apertura de vínculos su aplicación puede registrarse para recibir una actividad `invoke` cuando se pegan las direcciones URL con un dominio en particular en el área de redacción de mensajes.</span><span class="sxs-lookup"><span data-stu-id="e1600-105">With link unfurling your app can register to receive an `invoke` activity when URLs with a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="e1600-106">Contiene la dirección URL completa pegada en el área del mensaje de redacción y puede responder con una tarjeta que el usuario pueda deshacer, proporcionando información o `invoke` acciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="e1600-106">The `invoke` contains the full URL that was pasted into the compose message area, and you can respond with a card that the user can unfurl, providing additional information or actions.</span></span> <span data-ttu-id="e1600-107">Esto funciona de forma similar a un comando de búsqueda con la dirección URL que actúa como término de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="e1600-107">This works similar to a search command with the URL serving as the search term.</span></span>

> [!NOTE]
> <span data-ttu-id="e1600-108">Actualmente, la desafución de vínculos no se admite en clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="e1600-108">Currently, link unfurling is not supported on Mobile clients.</span></span>

<span data-ttu-id="e1600-109">La extensión de mensajería de Azure DevOps usa la implementación de vínculos para buscar direcciones URL pegadas en el área de mensajes de redacción que apunten a un elemento de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e1600-109">The Azure DevOps messaging extension uses link unfurling to look for URLs pasted into the compose message area pointing to a work item.</span></span> <span data-ttu-id="e1600-110">En la imagen siguiente, un usuario ha pegado una dirección URL de un elemento de trabajo en Azure DevOps, que la extensión de mensajería ha resuelto en una tarjeta:</span><span class="sxs-lookup"><span data-stu-id="e1600-110">In the following image, a user has pasted a URL for a work item in Azure DevOps, which the messaging extension has resolved into a card:</span></span>

![Ejemplo de desafusado de vínculos](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a><span data-ttu-id="e1600-112">Agregar la implementación de vínculos al manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="e1600-112">Add link unfurling to your app manifest</span></span>

<span data-ttu-id="e1600-113">Para agregar la implementación de vínculos al manifiesto de la aplicación, agrega una nueva matriz a la sección json del manifiesto `messageHandlers` `composeExtensions` de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e1600-113">To add link unfurling to your app manifest, add a new `messageHandlers` array to the `composeExtensions` section of your app manifest JSON.</span></span> <span data-ttu-id="e1600-114">Puedes agregar la matriz con la ayuda de App Studio o manualmente.</span><span class="sxs-lookup"><span data-stu-id="e1600-114">You can add the array either with the help of App Studio or manually.</span></span> <span data-ttu-id="e1600-115">Las listas de dominios pueden incluir caracteres comodín, por ejemplo `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="e1600-115">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="e1600-116">Esto coincide exactamente con un segmento del dominio; si necesita hacer `a.b.example.com` coincidir, use `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="e1600-116">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span>

> [!NOTE]
> <span data-ttu-id="e1600-117">No agregue dominios que no estén en su control, ya sea directamente o a través de caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="e1600-117">Donot add domains that are not in your control, either directly or through wildcards.</span></span> <span data-ttu-id="e1600-118">Por ejemplo, `yourapp.onmicrosoft.com` es válido, pero `*.onmicrosoft.com` no es válido.</span><span class="sxs-lookup"><span data-stu-id="e1600-118">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span> <span data-ttu-id="e1600-119">Además, los dominios de nivel superior están prohibidos.</span><span class="sxs-lookup"><span data-stu-id="e1600-119">Also, the top-level domains are prohibited.</span></span> <span data-ttu-id="e1600-120">Por ejemplo, `*.com` , `*.org` .</span><span class="sxs-lookup"><span data-stu-id="e1600-120">For example, `*.com`, `*.org`.</span></span>

### <a name="add-link-unfurling-using-app-studio"></a><span data-ttu-id="e1600-121">Agregar un despliegue de vínculos con App Studio</span><span class="sxs-lookup"><span data-stu-id="e1600-121">Add link unfurling using App Studio</span></span>

1. <span data-ttu-id="e1600-122">Abre **App Studio** desde el cliente de Microsoft Teams y selecciona la pestaña Editor **de** manifiestos.</span><span class="sxs-lookup"><span data-stu-id="e1600-122">Open **App Studio** from the Microsoft Teams client, and select the **Manifest Editor** tab.</span></span>
1. <span data-ttu-id="e1600-123">Cargue el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e1600-123">Load your app manifest.</span></span>
1. <span data-ttu-id="e1600-124">En la **página Extensión de** mensajería, agregue el dominio que desea buscar en la sección Controladores **de** mensajes.</span><span class="sxs-lookup"><span data-stu-id="e1600-124">On the **Messaging Extension** page, add the domain that you want to look for in the **Message handlers** section.</span></span> <span data-ttu-id="e1600-125">En la siguiente imagen se explica el proceso:</span><span class="sxs-lookup"><span data-stu-id="e1600-125">The following image explains the process:</span></span>

    ![sección controladores de mensajes en App Studio](~/assets/images/link-unfurling.png)
    
### <a name="add-link-unfurling-manually"></a><span data-ttu-id="e1600-127">Agregar la actualización manual de vínculos</span><span class="sxs-lookup"><span data-stu-id="e1600-127">Add link unfurling manually</span></span>

<span data-ttu-id="e1600-128">Para habilitar la extensión de mensajería para que interactúe con vínculos, primero debes agregar la `messageHandlers` matriz al manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e1600-128">To enable your messaging extension to interact with links, first you must add the `messageHandlers` array to your app manifest.</span></span> <span data-ttu-id="e1600-129">En el siguiente ejemplo se explica cómo agregar manualmente la actualización de vínculos:</span><span class="sxs-lookup"><span data-stu-id="e1600-129">The following example explains how to add link unfurling manually:</span></span> 


```json
...
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
],
...
```

<span data-ttu-id="e1600-130">Para obtener un ejemplo de manifiesto completo, vea [referencia de manifiesto](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="e1600-130">For a complete manifest example, see [manifest reference](~/resources/schema/manifest-schema.md).</span></span>

## <a name="handle-the-composeextensionquerylink-invoke"></a><span data-ttu-id="e1600-131">Controlar la `composeExtension/queryLink` invocación</span><span class="sxs-lookup"><span data-stu-id="e1600-131">Handle the `composeExtension/queryLink` invoke</span></span>

<span data-ttu-id="e1600-132">Después de agregar el dominio al manifiesto de la aplicación, debes actualizar el código del servicio web para controlar la solicitud de invocación.</span><span class="sxs-lookup"><span data-stu-id="e1600-132">After adding the domain to the app manifest, you must update your web service code to handle the invoke request.</span></span> <span data-ttu-id="e1600-133">Use la dirección URL recibida para buscar en el servicio y crear una respuesta de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e1600-133">Use the received URL to search your service and create a card response.</span></span> <span data-ttu-id="e1600-134">Si responde con más de una tarjeta, solo se usará la primera respuesta de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e1600-134">If you respond with more than one card, only the first card response is used.</span></span>

<span data-ttu-id="e1600-135">Se admiten los siguientes tipos de tarjeta:</span><span class="sxs-lookup"><span data-stu-id="e1600-135">The following card types are supported:</span></span>

* [<span data-ttu-id="e1600-136">Tarjeta miniatura</span><span class="sxs-lookup"><span data-stu-id="e1600-136">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="e1600-137">Tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="e1600-137">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="e1600-138">Tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="e1600-138">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="e1600-139">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="e1600-139">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

### <a name="example"></a><span data-ttu-id="e1600-140">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="e1600-140">Example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="e1600-141">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e1600-141">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsAppBasedLinkQueryAsync(ITurnContext<IInvokeActivity> turnContext, AppBasedLinkQuery query, CancellationToken cancellationToken)
{
    //You'll use the query.link value to search your service and create a card response
    var card = new HeroCard
    {
        Title = "Hero Card",
        Text = query.Url,
        Images = new List<CardImage> { new CardImage("https://raw.githubusercontent.com/microsoft/botframework-sdk/master/icon.png") },
    };

    var attachments = new MessagingExtensionAttachment(HeroCard.ContentType, null, card);
    var result = new MessagingExtensionResult(AttachmentLayoutTypes.List, "result", new[] { attachments }, null, "test unfurl");

    return new MessagingExtensionResponse(result);
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="e1600-142">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="e1600-142">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsLinkUnfurlingBot extends TeamsActivityHandler {
  handleTeamsAppBasedLinkQuery(context, query) {
    const attachment = CardFactory.thumbnailCard('Thumbnail Card',
      query.url,
      ['https://raw.githubusercontent.com/microsoft/botframework-sdk/master/icon.png']);

    const result = {
      attachmentLayout: 'list',
      type: 'result',
      attachments: [attachment]
    };

    const response = {
      composeExtension: result
    };
    return response;
  }
}
```

# <a name="json"></a>[<span data-ttu-id="e1600-143">JSON</span><span class="sxs-lookup"><span data-stu-id="e1600-143">JSON</span></span>](#tab/json)

<span data-ttu-id="e1600-144">A continuación se muestra un ejemplo `invoke` del bot enviado:</span><span class="sxs-lookup"><span data-stu-id="e1600-144">Following is an example of the `invoke` sent to your bot:</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="e1600-145">A continuación se muestra un ejemplo de la respuesta:</span><span class="sxs-lookup"><span data-stu-id="e1600-145">Following is an example of the response:</span></span>

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
        }
      }
    ]
  }
}
```

* * *

## <a name="see-also"></a><span data-ttu-id="e1600-146">Consulte también</span><span class="sxs-lookup"><span data-stu-id="e1600-146">See also</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="e1600-147">Qué son las tarjetas</span><span class="sxs-lookup"><span data-stu-id="e1600-147">What are cards</span></span>](~/task-modules-and-cards/what-are-cards.md)

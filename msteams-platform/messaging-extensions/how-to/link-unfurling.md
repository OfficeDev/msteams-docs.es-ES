---
title: Apertura de vínculos
author: surbhigupta
description: Cómo realizar el despliegue de vínculos con la extensión de mensajería en una Microsoft Teams aplicación.
localization_priority: Normal
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 7713fe794c9d15453438cfe3e1bde0238bde9d8c
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068951"
---
# <a name="link-unfurling"></a><span data-ttu-id="94581-103">Apertura de vínculos</span><span class="sxs-lookup"><span data-stu-id="94581-103">Link unfurling</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="94581-104">Este documento te guía sobre cómo agregar la actualización de vínculos al manifiesto de la aplicación con App studio y manualmente.</span><span class="sxs-lookup"><span data-stu-id="94581-104">This document guides you on how to add link unfurling to your app manifest using App studio and manually.</span></span> <span data-ttu-id="94581-105">Con la apertura de vínculos su aplicación puede registrarse para recibir una actividad `invoke` cuando se pegan las direcciones URL con un dominio en particular en el área de redacción de mensajes.</span><span class="sxs-lookup"><span data-stu-id="94581-105">With link unfurling your app can register to receive an `invoke` activity when URLs with a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="94581-106">Contiene la dirección URL completa pegada en el área del mensaje de redacción y puede responder con una tarjeta que el usuario pueda deshacer, proporcionando información o `invoke` acciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="94581-106">The `invoke` contains the full URL that was pasted into the compose message area, and you can respond with a card that the user can unfurl, providing additional information or actions.</span></span> <span data-ttu-id="94581-107">Esto funciona de forma similar a un comando de búsqueda con la dirección URL que actúa como término de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="94581-107">This works similar to a search command with the URL serving as the search term.</span></span>

> [!NOTE]
> * <span data-ttu-id="94581-108">Actualmente, la desafución de vínculos no se admite en clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="94581-108">Currently, link unfurling is not supported on Mobile clients.</span></span>
> * <span data-ttu-id="94581-109">El resultado de la descarga de vínculos se almacena en caché durante 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="94581-109">The link unfurling result is cached for 30 minutes.</span></span>

<span data-ttu-id="94581-110">La Azure DevOps de mensajería usa la desamuestra de vínculos para buscar direcciones URL pegadas en el área de mensaje de redacción que apunten a un elemento de trabajo.</span><span class="sxs-lookup"><span data-stu-id="94581-110">The Azure DevOps messaging extension uses link unfurling to look for URLs pasted into the compose message area pointing to a work item.</span></span> <span data-ttu-id="94581-111">En la siguiente imagen, un usuario ha pegado una dirección URL de un elemento de trabajo en Azure DevOps, que la extensión de mensajería ha resuelto en una tarjeta:</span><span class="sxs-lookup"><span data-stu-id="94581-111">In the following image, a user has pasted a URL for a work item in Azure DevOps, which the messaging extension has resolved into a card:</span></span>

![Ejemplo de desafusado de vínculos](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a><span data-ttu-id="94581-113">Agregar la implementación de vínculos al manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="94581-113">Add link unfurling to your app manifest</span></span>

<span data-ttu-id="94581-114">Para agregar la implementación de vínculos al manifiesto de la aplicación, agrega una nueva matriz a la sección json del manifiesto `messageHandlers` `composeExtensions` de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="94581-114">To add link unfurling to your app manifest, add a new `messageHandlers` array to the `composeExtensions` section of your app manifest JSON.</span></span> <span data-ttu-id="94581-115">Puedes agregar la matriz con la ayuda de App Studio o manualmente.</span><span class="sxs-lookup"><span data-stu-id="94581-115">You can add the array either with the help of App Studio or manually.</span></span> <span data-ttu-id="94581-116">Las listas de dominios pueden incluir caracteres comodín, por ejemplo `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="94581-116">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="94581-117">Esto coincide exactamente con un segmento del dominio; si necesita hacer `a.b.example.com` coincidir, use `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="94581-117">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span>

> [!NOTE]
> <span data-ttu-id="94581-118">No agregue dominios que no estén en su control, ya sea directamente o a través de caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="94581-118">Donot add domains that are not in your control, either directly or through wildcards.</span></span> <span data-ttu-id="94581-119">Por ejemplo, `yourapp.onmicrosoft.com` es válido, pero `*.onmicrosoft.com` no es válido.</span><span class="sxs-lookup"><span data-stu-id="94581-119">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span> <span data-ttu-id="94581-120">Además, los dominios de nivel superior están prohibidos.</span><span class="sxs-lookup"><span data-stu-id="94581-120">Also, the top-level domains are prohibited.</span></span> <span data-ttu-id="94581-121">Por ejemplo, `*.com` , `*.org` .</span><span class="sxs-lookup"><span data-stu-id="94581-121">For example, `*.com`, `*.org`.</span></span>

### <a name="add-link-unfurling-using-app-studio"></a><span data-ttu-id="94581-122">Agregar un despliegue de vínculos con App Studio</span><span class="sxs-lookup"><span data-stu-id="94581-122">Add link unfurling using App Studio</span></span>

1. <span data-ttu-id="94581-123">Abre **App Studio** desde el Microsoft Teams y selecciona la pestaña Editor **de** manifiestos.</span><span class="sxs-lookup"><span data-stu-id="94581-123">Open **App Studio** from the Microsoft Teams client, and select the **Manifest Editor** tab.</span></span>
1. <span data-ttu-id="94581-124">Cargue el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="94581-124">Load your app manifest.</span></span>
1. <span data-ttu-id="94581-125">En la **página Extensión de** mensajería, agregue el dominio que desea buscar en la sección Controladores **de** mensajes.</span><span class="sxs-lookup"><span data-stu-id="94581-125">On the **Messaging Extension** page, add the domain that you want to look for in the **Message handlers** section.</span></span> <span data-ttu-id="94581-126">En la siguiente imagen se explica el proceso:</span><span class="sxs-lookup"><span data-stu-id="94581-126">The following image explains the process:</span></span>

    ![sección controladores de mensajes en App Studio](~/assets/images/link-unfurling.png)
    
### <a name="add-link-unfurling-manually"></a><span data-ttu-id="94581-128">Agregar la actualización manual de vínculos</span><span class="sxs-lookup"><span data-stu-id="94581-128">Add link unfurling manually</span></span>

<span data-ttu-id="94581-129">Para habilitar la extensión de mensajería para que interactúe con vínculos, primero debes agregar la `messageHandlers` matriz al manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="94581-129">To enable your messaging extension to interact with links, first you must add the `messageHandlers` array to your app manifest.</span></span> <span data-ttu-id="94581-130">En el siguiente ejemplo se explica cómo agregar manualmente la actualización de vínculos:</span><span class="sxs-lookup"><span data-stu-id="94581-130">The following example explains how to add link unfurling manually:</span></span> 


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

<span data-ttu-id="94581-131">Para obtener un ejemplo de manifiesto completo, vea [referencia de manifiesto](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="94581-131">For a complete manifest example, see [manifest reference](~/resources/schema/manifest-schema.md).</span></span>

## <a name="handle-the-composeextensionquerylink-invoke"></a><span data-ttu-id="94581-132">Controlar la `composeExtension/queryLink` invocación</span><span class="sxs-lookup"><span data-stu-id="94581-132">Handle the `composeExtension/queryLink` invoke</span></span>

<span data-ttu-id="94581-133">Después de agregar el dominio al manifiesto de la aplicación, debes actualizar el código del servicio web para controlar la solicitud de invocación.</span><span class="sxs-lookup"><span data-stu-id="94581-133">After adding the domain to the app manifest, you must update your web service code to handle the invoke request.</span></span> <span data-ttu-id="94581-134">Use la dirección URL recibida para buscar en el servicio y crear una respuesta de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="94581-134">Use the received URL to search your service and create a card response.</span></span> <span data-ttu-id="94581-135">Si responde con más de una tarjeta, solo se usará la primera respuesta de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="94581-135">If you respond with more than one card, only the first card response is used.</span></span>

<span data-ttu-id="94581-136">Se admiten los siguientes tipos de tarjeta:</span><span class="sxs-lookup"><span data-stu-id="94581-136">The following card types are supported:</span></span>

* [<span data-ttu-id="94581-137">Tarjeta miniatura</span><span class="sxs-lookup"><span data-stu-id="94581-137">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="94581-138">Tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="94581-138">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="94581-139">Office 365 Tarjeta de conector</span><span class="sxs-lookup"><span data-stu-id="94581-139">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="94581-140">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="94581-140">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

### <a name="example"></a><span data-ttu-id="94581-141">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="94581-141">Example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="94581-142">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="94581-142">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="94581-143">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="94581-143">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="94581-144">JSON</span><span class="sxs-lookup"><span data-stu-id="94581-144">JSON</span></span>](#tab/json)

<span data-ttu-id="94581-145">A continuación se muestra un ejemplo `invoke` del bot enviado:</span><span class="sxs-lookup"><span data-stu-id="94581-145">Following is an example of the `invoke` sent to your bot:</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="94581-146">A continuación se muestra un ejemplo de la respuesta:</span><span class="sxs-lookup"><span data-stu-id="94581-146">Following is an example of the response:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="94581-147">Consulte también</span><span class="sxs-lookup"><span data-stu-id="94581-147">See also</span></span> 

* [<span data-ttu-id="94581-148">Tarjetas</span><span class="sxs-lookup"><span data-stu-id="94581-148">Cards</span></span>](~/task-modules-and-cards/what-are-cards.md)
* [<span data-ttu-id="94581-149">Expansión del vínculo de la pestaña y vista de fases</span><span class="sxs-lookup"><span data-stu-id="94581-149">Tabs link unfurling and Stage View</span></span>](~/tabs/tabs-link-unfurling.md)

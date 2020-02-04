---
title: Vincular unfurling
author: clearab
description: Cómo realizar unfurling de vínculos con la extensión de mensajería en una aplicación de Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 5b20ea303a2c3d085651a53b01af4bb449d386de
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676210"
---
# <a name="link-unfurling"></a><span data-ttu-id="6a779-103">Vincular unfurling</span><span class="sxs-lookup"><span data-stu-id="6a779-103">Link unfurling</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="6a779-104">Con unfurling de vínculos se puede registrar la aplicación para `invoke` recibir una actividad cuando se pegan direcciones URL con un dominio en particular en el área de mensaje de redacción.</span><span class="sxs-lookup"><span data-stu-id="6a779-104">With link unfurling your app can register to receive an `invoke` activity when URLs with a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="6a779-105">El `invoke` contendrá la dirección URL completa que se pegó en el área de mensaje de redacción y puede responder con una tarjeta que el usuario puede *unfurl*, lo que proporciona información o acciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="6a779-105">The `invoke` will contain the full URL that was pasted into the compose message area, and you can respond with a card the user can *unfurl*, providing additional information or actions.</span></span> <span data-ttu-id="6a779-106">Esto funciona de manera muy similar a un [comando de búsqueda](~/messaging-extensions/how-to/search-commands/define-search-command.md), con la dirección URL que actúa como el término de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="6a779-106">This works very similarly to a [search command](~/messaging-extensions/how-to/search-commands/define-search-command.md), with the URL serving as the search term.</span></span>

<span data-ttu-id="6a779-107">La extensión de mensajería de Azure DevOps usa el vínculo unfurling para buscar direcciones URL pegadas en el área de mensaje de redacción que apunta a un elemento de trabajo.</span><span class="sxs-lookup"><span data-stu-id="6a779-107">The Azure DevOps messaging extension uses link unfurling to look for URLs pasted into the compose message area pointing to a work item.</span></span> <span data-ttu-id="6a779-108">En la siguiente captura de pantalla, un usuario ha pegado en una dirección URL de un elemento de trabajo en Azure DevOps que la extensión de mensajería se ha resuelto en una tarjeta.</span><span class="sxs-lookup"><span data-stu-id="6a779-108">In the screenshot below, a user has pasted in a URL for a work item in Azure DevOps which the messaging extension has resolved into a card.</span></span>

![Ejemplo de vínculo unfurling](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a><span data-ttu-id="6a779-110">Agregar vínculo unfurling al manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="6a779-110">Add link unfurling to your app manifest</span></span>

<span data-ttu-id="6a779-111">Para ello, agregará una nueva `messageHandlers` matriz a la `composeExtensions` sección del JSON del manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6a779-111">To do this you'll add a new `messageHandlers` array to the `composeExtensions` section of your app manifest JSON.</span></span> <span data-ttu-id="6a779-112">Puede hacerlo con la ayuda de App Studio, o bien manualmente.</span><span class="sxs-lookup"><span data-stu-id="6a779-112">You can either do so with the help of App Studio, or manually.</span></span> <span data-ttu-id="6a779-113">Las listas de dominios pueden incluir caracteres comodín, por `*.example.com`ejemplo.</span><span class="sxs-lookup"><span data-stu-id="6a779-113">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="6a779-114">Esto coincide exactamente con un segmento del dominio; Si tiene que hacer coincidir `a.b.example.com` , `*.*.example.com`use.</span><span class="sxs-lookup"><span data-stu-id="6a779-114">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span>

### <a name="using-app-studio"></a><span data-ttu-id="6a779-115">Uso de App Studio</span><span class="sxs-lookup"><span data-stu-id="6a779-115">Using App Studio</span></span>

1. <span data-ttu-id="6a779-116">En App Studio, en la pestaña Editor de manifiestos, cargue el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6a779-116">In App Studio, on the Manifest editor tab, load your app manifest.</span></span>
1. <span data-ttu-id="6a779-117">En la página **extensión de mensajería** , agregue el dominio que quiera buscar en la sección **controladores de mensajes** , como se muestra en la captura de pantalla siguiente.</span><span class="sxs-lookup"><span data-stu-id="6a779-117">On the **Messaging Extension** page, add the domain you want to look for in the **Message handlers** section as in the screenshot below.</span></span>

![sección Controladores de mensajes en App Studio](~/assets/images/link-unfurling.png)

### <a name="manually"></a><span data-ttu-id="6a779-119">Manualmente</span><span class="sxs-lookup"><span data-stu-id="6a779-119">Manually</span></span>

<span data-ttu-id="6a779-120">Para habilitar la extensión de mensajería para que interactúe con los vínculos de esta forma, primero tendrá `messageHandlers` que agregar la matriz al manifiesto de la aplicación, como en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="6a779-120">To enable your messaging extension to interact with links this way you'll first need to add the `messageHandlers` array to your app manifest as in the example below.</span></span> <span data-ttu-id="6a779-121">Este ejemplo no es el manifiesto completo, vea el manifiesto [referencia](~/resources/schema/manifest-schema.md) para obtener un ejemplo completo de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="6a779-121">This example is not the complete manifest, see [manifest reference](~/resources/schema/manifest-schema.md) for a complete manifest example.</span></span>

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

## <a name="handle-the-composeextensionquerylink-invoke"></a><span data-ttu-id="6a779-122">Controlar la `composeExtension/queryLink` invocación</span><span class="sxs-lookup"><span data-stu-id="6a779-122">Handle the `composeExtension/queryLink` invoke</span></span>

<span data-ttu-id="6a779-123">Una vez que haya agregado el dominio para escuchar en el manifiesto de la aplicación, deberá actualizar el código del servicio web para administrar la solicitud de invocación.</span><span class="sxs-lookup"><span data-stu-id="6a779-123">Once you've added the domain to listen on to the app manifest, you'll need to update your web service code to handle the invoke request.</span></span> <span data-ttu-id="6a779-124">Use la dirección URL que reciba para buscar en el servicio y crear una respuesta de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="6a779-124">Use the URL you receive to search your service and create a card response.</span></span> <span data-ttu-id="6a779-125">Si responde con más de una tarjeta, solo se usará la primera.</span><span class="sxs-lookup"><span data-stu-id="6a779-125">If you respond with more than one card, only the first will be used.</span></span>

<span data-ttu-id="6a779-126">Se admiten los siguientes tipos de tarjeta:</span><span class="sxs-lookup"><span data-stu-id="6a779-126">We support the following card types:</span></span>

* [<span data-ttu-id="6a779-127">Tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="6a779-127">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="6a779-128">Tarjeta Hero</span><span class="sxs-lookup"><span data-stu-id="6a779-128">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="6a779-129">Tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="6a779-129">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="6a779-130">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="6a779-130">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="6a779-131">Consulte [¿Qué son las tarjetas](~/task-modules-and-cards/what-are-cards.md) para obtener información general).</span><span class="sxs-lookup"><span data-stu-id="6a779-131">See [What are cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="6a779-132">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6a779-132">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsAppBasedLinkQueryAsync(ITurnContext<IInvokeActivity> turnContext, AppBasedLinkQuery query, CancellationToken cancellationToken)
{
    //You'll use the query.link value to search your service and create a card response
    var heroCard = new ThumbnailCard
    {
        Title = "Thumbnail Card",
        Text = query.Url,
        Images = new List<CardImage> { new CardImage("https://raw.githubusercontent.com/microsoft/botframework-sdk/master/icon.png") },
    };

    var attachments = new MessagingExtensionAttachment(HeroCard.ContentType, null, heroCard);
    var result = new MessagingExtensionResult(AttachmentLayoutTypes.List, "result", new[] { attachments }, null, "test unfurl");

    return new MessagingExtensionResponse(result);
}
```

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="6a779-133">JavaScript/node. js</span><span class="sxs-lookup"><span data-stu-id="6a779-133">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="6a779-134">JSON</span><span class="sxs-lookup"><span data-stu-id="6a779-134">JSON</span></span>](#tab/json)

<span data-ttu-id="6a779-135">Este es un ejemplo del que `invoke` se ha enviado a su bot.</span><span class="sxs-lookup"><span data-stu-id="6a779-135">This is an example of the `invoke` sent to your bot.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="6a779-136">A continuación se muestra un ejemplo de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="6a779-136">An example of the response is shown below.</span></span>

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
        }
      }
    ]
  }
}
```

* * *

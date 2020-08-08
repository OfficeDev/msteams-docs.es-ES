---
title: Apertura de vínculos
author: clearab
description: Cómo realizar unfurling de vínculos con la extensión de mensajería en una aplicación de Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 32d19fcd44f2475047539350706d2745aeec3691
ms.sourcegitcommit: 7a2da3b65246a125d441a971e7e6a6418355adbe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2020
ms.locfileid: "46587807"
---
# <a name="link-unfurling"></a><span data-ttu-id="9d8b4-103">Apertura de vínculos</span><span class="sxs-lookup"><span data-stu-id="9d8b4-103">Link unfurling</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

> [!NOTE]
> <span data-ttu-id="9d8b4-104">Actualmente, Link unfurling no se admite en clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="9d8b4-104">Currently, Link unfurling is not supported on Mobile clients.</span></span>

<span data-ttu-id="9d8b4-105">Con unfurling de vínculos se puede registrar la aplicación para recibir una `invoke` actividad cuando se pegan direcciones URL con un dominio en particular en el área de mensaje de redacción.</span><span class="sxs-lookup"><span data-stu-id="9d8b4-105">With link unfurling your app can register to receive an `invoke` activity when URLs with a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="9d8b4-106">El `invoke` contendrá la dirección URL completa que se pegó en el área de mensaje de redacción y puede responder con una tarjeta que el usuario puede *unfurl*, lo que proporciona información o acciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="9d8b4-106">The `invoke` will contain the full URL that was pasted into the compose message area, and you can respond with a card the user can *unfurl*, providing additional information or actions.</span></span> <span data-ttu-id="9d8b4-107">Esto funciona de manera muy similar a un [comando de búsqueda](~/messaging-extensions/how-to/search-commands/define-search-command.md), con la dirección URL que actúa como el término de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9d8b4-107">This works very similarly to a [search command](~/messaging-extensions/how-to/search-commands/define-search-command.md), with the URL serving as the search term.</span></span>

<span data-ttu-id="9d8b4-108">La extensión de mensajería de Azure DevOps usa el vínculo unfurling para buscar direcciones URL pegadas en el área de mensaje de redacción que apunta a un elemento de trabajo.</span><span class="sxs-lookup"><span data-stu-id="9d8b4-108">The Azure DevOps messaging extension uses link unfurling to look for URLs pasted into the compose message area pointing to a work item.</span></span> <span data-ttu-id="9d8b4-109">En la siguiente captura de pantalla, un usuario ha pegado en una dirección URL de un elemento de trabajo en Azure DevOps que la extensión de mensajería se ha resuelto en una tarjeta.</span><span class="sxs-lookup"><span data-stu-id="9d8b4-109">In the screenshot below, a user has pasted in a URL for a work item in Azure DevOps which the messaging extension has resolved into a card.</span></span>

![Ejemplo de vínculo unfurling](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a><span data-ttu-id="9d8b4-111">Agregar vínculo unfurling al manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="9d8b4-111">Add link unfurling to your app manifest</span></span>

<span data-ttu-id="9d8b4-112">Para ello, agregará una nueva `messageHandlers` matriz a la `composeExtensions` sección del JSON del manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9d8b4-112">To do this you'll add a new `messageHandlers` array to the `composeExtensions` section of your app manifest JSON.</span></span> <span data-ttu-id="9d8b4-113">Puede hacerlo con la ayuda de App Studio, o bien manualmente.</span><span class="sxs-lookup"><span data-stu-id="9d8b4-113">You can either do so with the help of App Studio, or manually.</span></span> <span data-ttu-id="9d8b4-114">Las listas de dominios pueden incluir caracteres comodín, por ejemplo `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="9d8b4-114">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="9d8b4-115">Esto coincide exactamente con un segmento del dominio; Si tiene que hacer coincidir `a.b.example.com` , use `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="9d8b4-115">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span>

### <a name="using-app-studio"></a><span data-ttu-id="9d8b4-116">Usar App Studio</span><span class="sxs-lookup"><span data-stu-id="9d8b4-116">Using App Studio</span></span>

1. <span data-ttu-id="9d8b4-117">En App Studio, en la pestaña Editor de manifiestos, cargue el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9d8b4-117">In App Studio, on the Manifest editor tab, load your app manifest.</span></span>
1. <span data-ttu-id="9d8b4-118">En la página **extensión de mensajería** , agregue el dominio que quiera buscar en la sección **controladores de mensajes** , como se muestra en la captura de pantalla siguiente.</span><span class="sxs-lookup"><span data-stu-id="9d8b4-118">On the **Messaging Extension** page, add the domain you want to look for in the **Message handlers** section as in the screenshot below.</span></span>

![sección Controladores de mensajes en App Studio](~/assets/images/link-unfurling.png)

### <a name="manually"></a><span data-ttu-id="9d8b4-120">Manualmente</span><span class="sxs-lookup"><span data-stu-id="9d8b4-120">Manually</span></span>

<span data-ttu-id="9d8b4-121">Para habilitar la extensión de mensajería para que interactúe con los vínculos de esta forma, primero tendrá que agregar la `messageHandlers` matriz al manifiesto de la aplicación, como en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="9d8b4-121">To enable your messaging extension to interact with links this way you'll first need to add the `messageHandlers` array to your app manifest as in the example below.</span></span> <span data-ttu-id="9d8b4-122">Este ejemplo no es el manifiesto completo, vea el manifiesto [referencia](~/resources/schema/manifest-schema.md) para obtener un ejemplo completo de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="9d8b4-122">This example is not the complete manifest, see [manifest reference](~/resources/schema/manifest-schema.md) for a complete manifest example.</span></span>

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

## <a name="handle-the-composeextensionquerylink-invoke"></a><span data-ttu-id="9d8b4-123">Controlar la `composeExtension/queryLink` invocación</span><span class="sxs-lookup"><span data-stu-id="9d8b4-123">Handle the `composeExtension/queryLink` invoke</span></span>

<span data-ttu-id="9d8b4-124">Una vez que haya agregado el dominio para escuchar en el manifiesto de la aplicación, deberá actualizar el código del servicio web para administrar la solicitud de invocación.</span><span class="sxs-lookup"><span data-stu-id="9d8b4-124">Once you've added the domain to listen on to the app manifest, you'll need to update your web service code to handle the invoke request.</span></span> <span data-ttu-id="9d8b4-125">Use la dirección URL que reciba para buscar en el servicio y crear una respuesta de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="9d8b4-125">Use the URL you receive to search your service and create a card response.</span></span> <span data-ttu-id="9d8b4-126">Si responde con más de una tarjeta, solo se usará la primera.</span><span class="sxs-lookup"><span data-stu-id="9d8b4-126">If you respond with more than one card, only the first will be used.</span></span>

<span data-ttu-id="9d8b4-127">Se admiten los siguientes tipos de tarjeta:</span><span class="sxs-lookup"><span data-stu-id="9d8b4-127">We support the following card types:</span></span>

* [<span data-ttu-id="9d8b4-128">Tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="9d8b4-128">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="9d8b4-129">Tarjeta Hero</span><span class="sxs-lookup"><span data-stu-id="9d8b4-129">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="9d8b4-130">Tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="9d8b4-130">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="9d8b4-131">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="9d8b4-131">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="9d8b4-132">Consulte [¿Qué son las tarjetas](~/task-modules-and-cards/what-are-cards.md) para obtener información general).</span><span class="sxs-lookup"><span data-stu-id="9d8b4-132">See [What are cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="9d8b4-133">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9d8b4-133">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="9d8b4-134">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="9d8b4-134">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="9d8b4-135">JSON</span><span class="sxs-lookup"><span data-stu-id="9d8b4-135">JSON</span></span>](#tab/json)

<span data-ttu-id="9d8b4-136">Este es un ejemplo del que se ha `invoke` enviado a su bot.</span><span class="sxs-lookup"><span data-stu-id="9d8b4-136">This is an example of the `invoke` sent to your bot.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="9d8b4-137">A continuación se muestra un ejemplo de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="9d8b4-137">An example of the response is shown below.</span></span>

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

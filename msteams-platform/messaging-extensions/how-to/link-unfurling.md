---
title: Apertura de vínculos
author: clearab
description: Cómo realizar el desenlazaje de vínculos con la extensión de mensajería en una aplicación de Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 0d488638e63b8ec78bfa5bed8cf6f4f037883fb1
ms.sourcegitcommit: bf61ae5ad2afa4efdb0311158184d0cbb9c40174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/13/2021
ms.locfileid: "49845640"
---
# <a name="link-unfurling"></a><span data-ttu-id="55d41-103">Apertura de vínculos</span><span class="sxs-lookup"><span data-stu-id="55d41-103">Link unfurling</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

> [!NOTE]
> <span data-ttu-id="55d41-104">Actualmente, la desafución de vínculos no se admite en los clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="55d41-104">Currently, Link unfurling is not supported on Mobile clients.</span></span>

<span data-ttu-id="55d41-105">Con el desenlazaje de vínculos, la aplicación puede registrarse para recibir una actividad cuando las direcciones URL con un dominio determinado se pegan en el `invoke` área de redacción de mensajes.</span><span class="sxs-lookup"><span data-stu-id="55d41-105">With link unfurling your app can register to receive an `invoke` activity when URLs with a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="55d41-106">Contendrá la dirección URL completa pegada en el área de redacción de mensajes, y puede responder con una tarjeta que el usuario puede deshacer, proporcionando información o acciones `invoke` adicionales. </span><span class="sxs-lookup"><span data-stu-id="55d41-106">The `invoke` will contain the full URL that was pasted into the compose message area, and you can respond with a card the user can *unfurl*, providing additional information or actions.</span></span> <span data-ttu-id="55d41-107">Esto funciona de forma muy similar a un comando [de búsqueda,](~/messaging-extensions/how-to/search-commands/define-search-command.md)con la dirección URL que actúa como término de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="55d41-107">This works very similarly to a [search command](~/messaging-extensions/how-to/search-commands/define-search-command.md), with the URL serving as the search term.</span></span>

<span data-ttu-id="55d41-108">La extensión de mensajería de Azure DevOps usa el desenlace de vínculos para buscar direcciones URL pegadas en el área de redacción de mensajes que apunten a un elemento de trabajo.</span><span class="sxs-lookup"><span data-stu-id="55d41-108">The Azure DevOps messaging extension uses link unfurling to look for URLs pasted into the compose message area pointing to a work item.</span></span> <span data-ttu-id="55d41-109">En la siguiente captura de pantalla, un usuario ha pegado una dirección URL de un elemento de trabajo en Azure DevOps que la extensión de mensajería ha resuelto en una tarjeta.</span><span class="sxs-lookup"><span data-stu-id="55d41-109">In the screenshot below, a user has pasted in a URL for a work item in Azure DevOps which the messaging extension has resolved into a card.</span></span>

![Ejemplo de desenlazaje de vínculos](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a><span data-ttu-id="55d41-111">Agregar un vínculo que se desenlameje al manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="55d41-111">Add link unfurling to your app manifest</span></span>

 <span data-ttu-id="55d41-112">Para agregar el desenlazaje de vínculos al manifiesto de la aplicación, agregue una nueva matriz a la sección del JSON del `messageHandlers` `composeExtensions` manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="55d41-112">To add link unfurling to your app manifest add a new `messageHandlers` array to the `composeExtensions` section of your app manifest JSON.</span></span> <span data-ttu-id="55d41-113">Puede agregar la matriz con la ayuda de App Studio o manualmente.</span><span class="sxs-lookup"><span data-stu-id="55d41-113">You can add the array either with the help of App Studio or manually.</span></span> <span data-ttu-id="55d41-114">Las listas de dominios pueden incluir caracteres comodín, por `*.example.com` ejemplo.</span><span class="sxs-lookup"><span data-stu-id="55d41-114">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="55d41-115">Esto coincide exactamente con un segmento del dominio; si necesita hacer `a.b.example.com` coincidir, use `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="55d41-115">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span>

> [!NOTE]
> <span data-ttu-id="55d41-116">No agregue dominios que estén fuera de su control, ya sea directamente o a través de caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="55d41-116">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="55d41-117">Por ejemplo, yourapp.onmicrosoft.com es válido, pero \*.onmicrosoft.com no es válido.</span><span class="sxs-lookup"><span data-stu-id="55d41-117">For example, yourapp.onmicrosoft.com is valid, but \*.onmicrosoft.com is not valid.</span></span> <span data-ttu-id="55d41-118">Además, los dominios de nivel superior están prohibidos.</span><span class="sxs-lookup"><span data-stu-id="55d41-118">Also, the top-level domains are prohibited.</span></span> <span data-ttu-id="55d41-119">Por ejemplo, \*.com, \*.org.</span><span class="sxs-lookup"><span data-stu-id="55d41-119">For example, \*.com, \*.org.</span></span>

### <a name="using-app-studio"></a><span data-ttu-id="55d41-120">Usar App Studio</span><span class="sxs-lookup"><span data-stu-id="55d41-120">Using App Studio</span></span>

1. <span data-ttu-id="55d41-121">En App Studio, en la pestaña Editor de manifiestos, carga el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="55d41-121">In App Studio, on the Manifest editor tab, load your app manifest.</span></span>
1. <span data-ttu-id="55d41-122">En la **página Extensión de** mensajería, agregue el  dominio que desea buscar en la sección Controladores de mensajes, como en la captura de pantalla siguiente.</span><span class="sxs-lookup"><span data-stu-id="55d41-122">On the **Messaging Extension** page, add the domain you want to look for in the **Message handlers** section as in the screenshot below.</span></span>

![sección controladores de mensajes en App Studio](~/assets/images/link-unfurling.png)

### <a name="manually"></a><span data-ttu-id="55d41-124">Manualmente</span><span class="sxs-lookup"><span data-stu-id="55d41-124">Manually</span></span>

<span data-ttu-id="55d41-125">Para permitir que la extensión de mensajería interactúe con vínculos de esta forma, primero tendrá que agregar la matriz al manifiesto de la aplicación, como en `messageHandlers` el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="55d41-125">To enable your messaging extension to interact with links this way you'll first need to add the `messageHandlers` array to your app manifest as in the example below.</span></span> <span data-ttu-id="55d41-126">Este ejemplo no es el manifiesto completo, vea [la referencia del manifiesto](~/resources/schema/manifest-schema.md) para obtener un ejemplo de manifiesto completo.</span><span class="sxs-lookup"><span data-stu-id="55d41-126">This example is not the complete manifest, see [manifest reference](~/resources/schema/manifest-schema.md) for a complete manifest example.</span></span>

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

## <a name="handle-the-composeextensionquerylink-invoke"></a><span data-ttu-id="55d41-127">Controlar la `composeExtension/queryLink` invocación</span><span class="sxs-lookup"><span data-stu-id="55d41-127">Handle the `composeExtension/queryLink` invoke</span></span>

<span data-ttu-id="55d41-128">Una vez que haya agregado el dominio para escuchar el manifiesto de la aplicación, tendrá que actualizar el código del servicio web para controlar la solicitud de invocación.</span><span class="sxs-lookup"><span data-stu-id="55d41-128">Once you've added the domain to listen on to the app manifest, you'll need to update your web service code to handle the invoke request.</span></span> <span data-ttu-id="55d41-129">Use la dirección URL que recibe para buscar en el servicio y crear una respuesta de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="55d41-129">Use the URL you receive to search your service and create a card response.</span></span> <span data-ttu-id="55d41-130">Si responde con más de una tarjeta, solo se usará la primera.</span><span class="sxs-lookup"><span data-stu-id="55d41-130">If you respond with more than one card, only the first will be used.</span></span>

<span data-ttu-id="55d41-131">Se admiten los siguientes tipos de tarjetas:</span><span class="sxs-lookup"><span data-stu-id="55d41-131">We support the following card types:</span></span>

* [<span data-ttu-id="55d41-132">Tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="55d41-132">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="55d41-133">Tarjeta principal</span><span class="sxs-lookup"><span data-stu-id="55d41-133">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="55d41-134">Tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="55d41-134">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="55d41-135">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="55d41-135">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="55d41-136">Consulta [Qué son las tarjetas](~/task-modules-and-cards/what-are-cards.md) para obtener información general.</span><span class="sxs-lookup"><span data-stu-id="55d41-136">See [What are cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="55d41-137">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="55d41-137">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="55d41-138">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="55d41-138">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="55d41-139">JSON</span><span class="sxs-lookup"><span data-stu-id="55d41-139">JSON</span></span>](#tab/json)

<span data-ttu-id="55d41-140">Este es un ejemplo del `invoke` bot enviado.</span><span class="sxs-lookup"><span data-stu-id="55d41-140">This is an example of the `invoke` sent to your bot.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="55d41-141">A continuación se muestra un ejemplo de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="55d41-141">An example of the response is shown below.</span></span>

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

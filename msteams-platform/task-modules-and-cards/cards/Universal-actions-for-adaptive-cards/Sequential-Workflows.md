---
title: Flujos de trabajo secuenciales
description: Ejemplo de flujos de trabajo secuenciales mediante acciones universales
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: f36e65133572569cd01de1053044336c810656f3
ms.sourcegitcommit: 999f5c607671e088ea8a461fa7dbb63f8d61c39b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2021
ms.locfileid: "52649652"
---
# <a name="sequential-workflows"></a><span data-ttu-id="7b2da-103">Flujos de trabajo secuenciales</span><span class="sxs-lookup"><span data-stu-id="7b2da-103">Sequential Workflows</span></span>

<span data-ttu-id="7b2da-104">Las tarjetas adaptables ahora admiten flujos de trabajo secuenciales que es cuando las tarjetas adaptables se actualizan en la acción del usuario y el usuario puede avanzar a través de una serie de tarjetas que requieren la entrada del usuario.</span><span class="sxs-lookup"><span data-stu-id="7b2da-104">Adaptive Cards now support Sequential Workflows that is when Adaptive Cards are updated on user action and user can progress through a series of cards that require user input.</span></span> <span data-ttu-id="7b2da-105">Esto se admite a través de , lo que permite a los `Action.Execute` desarrolladores de bots devolver tarjetas adaptables en respuesta a una acción del usuario.</span><span class="sxs-lookup"><span data-stu-id="7b2da-105">This is supported through `Action.Execute`, which allows bot developers to return Adaptive Cards in response to a user action.</span></span>

<span data-ttu-id="7b2da-106">Por ejemplo, tome un escenario en el que la cafetería quiera realizar un pedido para un equipo o canal.</span><span class="sxs-lookup"><span data-stu-id="7b2da-106">For example, take a scenario where the cafeteria wants to take an order for a team or channel.</span></span> <span data-ttu-id="7b2da-107">Con la elección del usuario para varios elementos, como `Action.Execute` comida, bebidas, y así sucesivamente, se puede registrar secuencialmente.</span><span class="sxs-lookup"><span data-stu-id="7b2da-107">With `Action.Execute` the user's choice for various items, such as food, drinks, and so on can be recorded sequentially.</span></span> <span data-ttu-id="7b2da-108">El usuario también puede ir y venir a través de las tarjetas según la lógica definida por el desarrollador del bot.</span><span class="sxs-lookup"><span data-stu-id="7b2da-108">User can also go back and forth through the cards as per the logic defined by the bot developer.</span></span> <br/>

<span data-ttu-id="7b2da-109">La siguiente imagen muestra el flujo de trabajo secuencial:</span><span class="sxs-lookup"><span data-stu-id="7b2da-109">The following image shows the Sequential Workflow:</span></span>

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

<span data-ttu-id="7b2da-110">Un usuario puede avanzar a través de su flujo de trabajo sin modificar la tarjeta para otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="7b2da-110">A user can progress through their workflow without modifying the card for other users.</span></span> <span data-ttu-id="7b2da-111">Esto también es útil para realizar cuestionarios con tarjetas adaptables secuenciales.</span><span class="sxs-lookup"><span data-stu-id="7b2da-111">This is also useful for conducting quizzes using sequential Adaptive Cards.</span></span> <span data-ttu-id="7b2da-112">Como se muestra en la siguiente imagen, los diferentes usuarios pueden estar en distintas fases del flujo de trabajo y ver diferentes estados de la tarjeta:</span><span class="sxs-lookup"><span data-stu-id="7b2da-112">As shown in the following image, different users can be at different stages of the workflow and they see different states of the card:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="Estados del bot de restauración":::

> [!NOTE]
> <span data-ttu-id="7b2da-114">Para sincronizar el progreso del usuario entre dispositivos, use la `refresh` propiedad en ADAPTIVE Card JSON.</span><span class="sxs-lookup"><span data-stu-id="7b2da-114">In order to sync the user's progress across devices, use the `refresh` property in Adaptive Card JSON.</span></span>

## <a name="sequential-workflow-for-adaptive-cards"></a><span data-ttu-id="7b2da-115">Flujo de trabajo secuencial para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="7b2da-115">Sequential Workflow for Adaptive Cards</span></span>

<span data-ttu-id="7b2da-116">El siguiente código proporciona un ejemplo de tarjetas adaptables:</span><span class="sxs-lookup"><span data-stu-id="7b2da-116">The following code provides an example of Adaptive Cards:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "body": [
    {
      "type": "TextBlock",
      "text": "Select from food options"
    },
    { 
      "type": "ActionSet",
      "actions": [
        {
          "type": "Action.Execute",
          "title": "Chicken",
          "verb": "food",
          "data": {
              "item": "chicken"
          }
        },
        {
          "type": "Action.Execute",
          "title": "Beef",
          "verb": "food",
          "data": {
              "item": "beef"
          }
        },
        {
          "type": "Action.Execute",
          "title": "Vegan",
          "verb": "food",
          "data": {
              "item": "vegan"
          }
        }
      ]
    }
  ]
}
```

<span data-ttu-id="7b2da-117">`Action.Execute`invocar el bot puede devolver tarjetas adaptables como respuesta, lo que reemplaza a la tarjeta existente en Teams.</span><span class="sxs-lookup"><span data-stu-id="7b2da-117">`Action.Execute` invoking the bot can return Adaptive Cards as a response, which replaces the existing card in Teams.</span></span>
<span data-ttu-id="7b2da-118">En el siguiente ejemplo se proporciona lo que devuelve el bot en la selección de comida o bebida o en la confirmación del pedido:</span><span class="sxs-lookup"><span data-stu-id="7b2da-118">The following example provides what the bot returns on food or drink selection or order confirmation:</span></span>

* <span data-ttu-id="7b2da-119">En la selección de alimentos de la tarjeta 1, el bot puede devolver una tarjeta para la selección de las bebidas que es Tarjeta 2.</span><span class="sxs-lookup"><span data-stu-id="7b2da-119">On food selection from Card 1, bot can return a card for selection of drinks that is Card 2.</span></span>
* <span data-ttu-id="7b2da-120">En la selección de la bebida de la tarjeta 2, el bot puede devolver una tarjeta de confirmación de pedido que sea Tarjeta 3.</span><span class="sxs-lookup"><span data-stu-id="7b2da-120">On drink selection from Card 2, bot can return an order confirmation card that is Card 3.</span></span>
* <span data-ttu-id="7b2da-121">Al confirmar el pedido desde la tarjeta 3, el bot puede devolver una tarjeta confirmada de pedido que es La tarjeta 4.</span><span class="sxs-lookup"><span data-stu-id="7b2da-121">On order confirmation from Card 3, bot can return an order confirmed card that is Card 4.</span></span>

## <a name="invoke-request-received-on-bot-side"></a><span data-ttu-id="7b2da-122">Invocar solicitud recibida en el lado del bot</span><span class="sxs-lookup"><span data-stu-id="7b2da-122">Invoke request received on bot side</span></span>

<span data-ttu-id="7b2da-123">El siguiente código proporciona un ejemplo de una solicitud de invocación recibida en el lado del bot:</span><span class="sxs-lookup"><span data-stu-id="7b2da-123">The following code provides an example of an invoke request received on bot side:</span></span>

```JSON
{ 
  "type": "invoke",
  "name": "adaptiveCard/action",

  // ... other properties omitted for brevity

  "value": { 
    "action": { 
      "type": "Action.Execute", 
      "id": "", 
      "verb": "food",
      "data": { 
            "item": "vegan"
      } 
    },
    "trigger": "manual" 
  }
}
```

## <a name="invoke-response-to-return-adaptive-cards"></a><span data-ttu-id="7b2da-124">Invocar respuesta para devolver tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="7b2da-124">Invoke response to return Adaptive Cards</span></span>

<span data-ttu-id="7b2da-125">El código siguiente proporciona un ejemplo de una respuesta de invocación para devolver tarjetas adaptables:</span><span class="sxs-lookup"><span data-stu-id="7b2da-125">The following code provides an example of an invoke response to return Adaptive Cards:</span></span>

```C#
string cardJson = "<adaptive card json>";
var card = JsonConvert.DeserializeObject(cardJson);

var adaptiveCardResponse = JObject.FromObject(new
 {
    statusCode = 200,
    type = "application/vnd.microsoft.adaptive.card",
    value = card
 });
```

## <a name="code-sample"></a><span data-ttu-id="7b2da-126">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="7b2da-126">Code sample</span></span>

|<span data-ttu-id="7b2da-127">Nombre de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7b2da-127">Sample name</span></span> | <span data-ttu-id="7b2da-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="7b2da-128">Description</span></span> | <span data-ttu-id="7b2da-129">. NETCore</span><span class="sxs-lookup"><span data-stu-id="7b2da-129">.NETCore</span></span> |
|----------------|-----------------|--------------|
| <span data-ttu-id="7b2da-130">Teams bot de restauración</span><span class="sxs-lookup"><span data-stu-id="7b2da-130">Teams catering bot</span></span> | <span data-ttu-id="7b2da-131">Crea un bot simple que acepte el pedido de alimentos con tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="7b2da-131">Create a simple bot that accepts food order using Adaptive Cards.</span></span> |[<span data-ttu-id="7b2da-132">View</span><span class="sxs-lookup"><span data-stu-id="7b2da-132">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)|

## <a name="see-also"></a><span data-ttu-id="7b2da-133">Consulte también</span><span class="sxs-lookup"><span data-stu-id="7b2da-133">See also</span></span>

* [<span data-ttu-id="7b2da-134">Acciones de tarjeta adaptable en Teams</span><span class="sxs-lookup"><span data-stu-id="7b2da-134">Adaptive Card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [<span data-ttu-id="7b2da-135">Cómo funcionan los bots</span><span class="sxs-lookup"><span data-stu-id="7b2da-135">How bots work</span></span>](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [<span data-ttu-id="7b2da-136">Trabajar con Acciones universales para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="7b2da-136">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)

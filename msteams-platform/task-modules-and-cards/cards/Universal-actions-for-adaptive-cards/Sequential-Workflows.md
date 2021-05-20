---
title: Flujos de trabajo secuenciales
description: Ejemplo de flujos de trabajo secuenciales mediante acciones universales
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 7f285bf76aac4f0ca276321aee2ce4b4e5c3e7e4
ms.sourcegitcommit: 9ef3b415cbba484c2201abe9c6927e08d974388e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52555405"
---
# <a name="sequential-workflows"></a><span data-ttu-id="7608e-103">Flujos de trabajo secuenciales</span><span class="sxs-lookup"><span data-stu-id="7608e-103">Sequential Workflows</span></span>

<span data-ttu-id="7608e-104">Las tarjetas adaptables ahora admiten flujos de trabajo secuenciales que es cuando las tarjetas adaptables se actualizan en la acción del usuario y el usuario puede progresar a través de una serie de tarjetas que requieren la entrada del usuario.</span><span class="sxs-lookup"><span data-stu-id="7608e-104">Adaptive Cards now support Sequential Workflows that is when Adaptive Cards are updated on user action and user can progress through a series of cards that require user input.</span></span> <span data-ttu-id="7608e-105">Esto es compatible con `Action.Execute` , lo que permite a los desarrolladores de bots devolver tarjetas adaptables en respuesta a una acción del usuario.</span><span class="sxs-lookup"><span data-stu-id="7608e-105">This is supported through `Action.Execute`, which allows bot developers to return Adaptive Cards in response to a user action.</span></span>

<span data-ttu-id="7608e-106">Por ejemplo, tome un escenario en el que la cafetería desee realizar un pedido para un equipo o canal.</span><span class="sxs-lookup"><span data-stu-id="7608e-106">For example, take a scenario where the cafeteria wants to take an order for a team or channel.</span></span> <span data-ttu-id="7608e-107">Con `Action.Execute` la elección del usuario para varios artículos, tales como alimentos, bebidas, etc. se puede registrar secuencialmente.</span><span class="sxs-lookup"><span data-stu-id="7608e-107">With `Action.Execute` the user's choice for various items, such as food, drinks, and so on can be recorded sequentially.</span></span> <span data-ttu-id="7608e-108">El usuario también puede ir y venir a través de las tarjetas según la lógica definida por el desarrollador del bot.</span><span class="sxs-lookup"><span data-stu-id="7608e-108">User can also go back and forth through the cards as per the logic defined by the bot developer.</span></span> <br/>

<span data-ttu-id="7608e-109">La siguiente imagen muestra el flujo de trabajo secuencial:</span><span class="sxs-lookup"><span data-stu-id="7608e-109">The following image shows the Sequential Workflow:</span></span>

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

<span data-ttu-id="7608e-110">Un usuario puede progresar a través de su flujo de trabajo sin modificar la tarjeta para otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="7608e-110">A user can progress through their workflow without modifying the card for other users.</span></span> <span data-ttu-id="7608e-111">Esto también es útil para realizar cuestionarios utilizando tarjetas adaptables secuenciales.</span><span class="sxs-lookup"><span data-stu-id="7608e-111">This is also useful for conducting quizzes using sequential Adaptive Cards.</span></span> <span data-ttu-id="7608e-112">Como se muestra en la siguiente imagen, diferentes usuarios pueden estar en diferentes etapas del flujo de trabajo y ven diferentes estados de la tarjeta:</span><span class="sxs-lookup"><span data-stu-id="7608e-112">As shown in the following image, different users can be at different stages of the workflow and they see different states of the card:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="Estados del bot de catering":::

> [!NOTE]
> <span data-ttu-id="7608e-114">Para sincronizar el progreso del usuario entre dispositivos, utilice la `refresh` propiedad en JSON de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="7608e-114">In order to sync the user's progress across devices, use the `refresh` property in Adaptive Card JSON.</span></span>

## <a name="sequential-workflow-for-adaptive-cards"></a><span data-ttu-id="7608e-115">Flujo de trabajo secuencial para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="7608e-115">Sequential Workflow for Adaptive Cards</span></span>

<span data-ttu-id="7608e-116">El código siguiente proporciona un ejemplo de tarjetas adaptables:</span><span class="sxs-lookup"><span data-stu-id="7608e-116">The following code provides an example of Adaptive Cards:</span></span>

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

<span data-ttu-id="7608e-117">`Action.Execute`invocar el bot puede devolver tarjetas adaptables como respuesta, lo que reemplaza la tarjeta existente en Teams.</span><span class="sxs-lookup"><span data-stu-id="7608e-117">`Action.Execute` invoking the bot can return Adaptive Cards as a response, which replaces the existing card in Teams.</span></span>
<span data-ttu-id="7608e-118">En el ejemplo siguiente se proporciona lo que el bot devuelve en la selección de alimentos o bebidas o la confirmación del pedido:</span><span class="sxs-lookup"><span data-stu-id="7608e-118">The following example provides what the bot returns on food or drink selection or order confirmation:</span></span>

* <span data-ttu-id="7608e-119">En la selección de alimentos de la tarjeta 1, bot puede devolver una tarjeta para la selección de bebidas que es la tarjeta 2.</span><span class="sxs-lookup"><span data-stu-id="7608e-119">On food selection from Card 1, bot can return a card for selection of drinks that is Card 2.</span></span>
* <span data-ttu-id="7608e-120">En la selección de bebidas de la tarjeta 2, bot puede devolver una tarjeta de confirmación del pedido que es la tarjeta 3.</span><span class="sxs-lookup"><span data-stu-id="7608e-120">On drink selection from Card 2, bot can return an order confirmation card that is Card 3.</span></span>
* <span data-ttu-id="7608e-121">Al confirmar el pedido desde la tarjeta 3, bot puede devolver una tarjeta confirmada del pedido que es la tarjeta 4.</span><span class="sxs-lookup"><span data-stu-id="7608e-121">On order confirmation from Card 3, bot can return an order confirmed card that is Card 4.</span></span>

## <a name="invoke-request-received-on-bot-side"></a><span data-ttu-id="7608e-122">Invocar solicitud recibida en el lado del bot</span><span class="sxs-lookup"><span data-stu-id="7608e-122">Invoke request received on bot side</span></span>

<span data-ttu-id="7608e-123">El código siguiente proporciona un ejemplo de una solicitud de invocación recibida en el lado del bot:</span><span class="sxs-lookup"><span data-stu-id="7608e-123">The following code provides an example of an invoke request received on bot side:</span></span>

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

## <a name="invoke-response-to-return-adaptive-cards"></a><span data-ttu-id="7608e-124">Invocar respuesta para devolver tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="7608e-124">Invoke response to return Adaptive Cards</span></span>

<span data-ttu-id="7608e-125">El código siguiente proporciona un ejemplo de una respuesta de invocación para devolver tarjetas adaptables:</span><span class="sxs-lookup"><span data-stu-id="7608e-125">The following code provides an example of an invoke response to return Adaptive Cards:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="7608e-126">Vea también</span><span class="sxs-lookup"><span data-stu-id="7608e-126">See also</span></span>

* [<span data-ttu-id="7608e-127">Acciones de la tarjeta adaptable en Teams</span><span class="sxs-lookup"><span data-stu-id="7608e-127">Adaptive Card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [<span data-ttu-id="7608e-128">Cómo funcionan los bots</span><span class="sxs-lookup"><span data-stu-id="7608e-128">How bots work</span></span>](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [<span data-ttu-id="7608e-129">Trabajar con Acciones universales para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="7608e-129">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)

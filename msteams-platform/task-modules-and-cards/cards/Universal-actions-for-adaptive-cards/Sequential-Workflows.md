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
# <a name="sequential-workflows"></a>Flujos de trabajo secuenciales

Las tarjetas adaptables ahora admiten flujos de trabajo secuenciales que es cuando las tarjetas adaptables se actualizan en la acción del usuario y el usuario puede avanzar a través de una serie de tarjetas que requieren la entrada del usuario. Esto se admite a través de , lo que permite a los `Action.Execute` desarrolladores de bots devolver tarjetas adaptables en respuesta a una acción del usuario.

Por ejemplo, tome un escenario en el que la cafetería quiera realizar un pedido para un equipo o canal. Con la elección del usuario para varios elementos, como `Action.Execute` comida, bebidas, y así sucesivamente, se puede registrar secuencialmente. El usuario también puede ir y venir a través de las tarjetas según la lógica definida por el desarrollador del bot. <br/>

La siguiente imagen muestra el flujo de trabajo secuencial:

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

Un usuario puede avanzar a través de su flujo de trabajo sin modificar la tarjeta para otros usuarios. Esto también es útil para realizar cuestionarios con tarjetas adaptables secuenciales. Como se muestra en la siguiente imagen, los diferentes usuarios pueden estar en distintas fases del flujo de trabajo y ver diferentes estados de la tarjeta:

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="Estados del bot de restauración":::

> [!NOTE]
> Para sincronizar el progreso del usuario entre dispositivos, use la `refresh` propiedad en ADAPTIVE Card JSON.

## <a name="sequential-workflow-for-adaptive-cards"></a>Flujo de trabajo secuencial para tarjetas adaptables

El siguiente código proporciona un ejemplo de tarjetas adaptables:

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

`Action.Execute`invocar el bot puede devolver tarjetas adaptables como respuesta, lo que reemplaza a la tarjeta existente en Teams.
En el siguiente ejemplo se proporciona lo que devuelve el bot en la selección de comida o bebida o en la confirmación del pedido:

* En la selección de alimentos de la tarjeta 1, el bot puede devolver una tarjeta para la selección de las bebidas que es Tarjeta 2.
* En la selección de la bebida de la tarjeta 2, el bot puede devolver una tarjeta de confirmación de pedido que sea Tarjeta 3.
* Al confirmar el pedido desde la tarjeta 3, el bot puede devolver una tarjeta confirmada de pedido que es La tarjeta 4.

## <a name="invoke-request-received-on-bot-side"></a>Invocar solicitud recibida en el lado del bot

El siguiente código proporciona un ejemplo de una solicitud de invocación recibida en el lado del bot:

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

## <a name="invoke-response-to-return-adaptive-cards"></a>Invocar respuesta para devolver tarjetas adaptables

El código siguiente proporciona un ejemplo de una respuesta de invocación para devolver tarjetas adaptables:

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

## <a name="see-also"></a>Consulte también

* [Acciones de tarjeta adaptable en Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [Cómo funcionan los bots](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [Trabajar con Acciones universales para tarjetas adaptables](Work-with-universal-actions-for-adaptive-cards.md)

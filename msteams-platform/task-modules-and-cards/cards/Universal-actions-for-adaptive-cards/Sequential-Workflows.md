---
title: Flujos de trabajo secuenciales
description: Más información sobre los flujos de trabajo secuenciales para tarjetas adaptables mediante acciones universales con ejemplos de código
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 32200fc7a4df12567ba4000aad34e5a229dbc466
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073784"
---
# <a name="sequential-workflows"></a>Flujos de trabajo secuenciales

Las tarjetas adaptables ahora admiten flujos de trabajo secuenciales que se actualizan en la acción del usuario. Con flujos de trabajo secuenciales, las tarjetas adaptables se actualizan en la acción del usuario y el usuario puede avanzar a través de una serie de tarjetas que requieren la entrada del usuario. `Action.Execute` admite flujos de trabajo secuenciales, lo que permite a los desarrolladores de bots devolver tarjetas adaptables en respuesta a una acción del usuario.

Por ejemplo, tome un escenario en el que la cafetería quiera realizar un pedido para un equipo o canal. Con `Action.Execute` la elección del usuario para diversos artículos, como alimentos y bebidas, se puede registrar secuencialmente. El usuario también puede ir y venir a través de las tarjetas según la lógica definida por el desarrollador del bot. <br/>

En la imagen siguiente se muestra el flujo de trabajo secuencial:

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

Un usuario puede avanzar a través de su flujo de trabajo sin modificar la tarjeta para otros usuarios. El flujo de trabajo también es útil para realizar cuestionarios mediante tarjetas adaptables secuenciales. En la imagen siguiente se muestran diferentes usuarios que pueden estar en diferentes fases del flujo de trabajo y los estados de la tarjeta:

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="Estados del bot de catering" lightbox="../../../assets/images/adaptive-cards/universal-bots-catering-bot.png":::

> [!NOTE]
> Para sincronizar el progreso del usuario entre dispositivos, use la `refresh` propiedad en JSON de tarjeta adaptable.

## <a name="sequential-workflow-for-adaptive-cards"></a>Flujo de trabajo secuencial para tarjetas adaptables

El código siguiente proporciona un ejemplo de tarjetas adaptables:

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

`Action.Execute`La invocación del bot puede devolver tarjetas adaptables como respuesta, lo que reemplaza a la tarjeta existente en Teams.
En el ejemplo siguiente se proporciona lo que devuelve el bot en la selección de alimentos o bebidas o la confirmación del pedido:

* En la selección de alimentos de la Tarjeta 1, el bot puede devolver una tarjeta para la selección de bebidas que es la Tarjeta 2.
* En la selección de bebidas de la Tarjeta 2, el bot puede devolver una tarjeta de confirmación de pedido que sea la Tarjeta 3.
* En la confirmación del pedido de la Tarjeta 3, el bot puede devolver una tarjeta confirmada por pedido que sea la Tarjeta 4.

## <a name="invoke-request-received-on-bot-side"></a>Invocación de la solicitud recibida en el lado del bot

El código siguiente proporciona un ejemplo de una solicitud de invocación recibida en el bot:

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

## <a name="invoke-response-to-return-adaptive-cards"></a>Invocación de la respuesta para devolver tarjetas adaptables

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

## <a name="code-samples"></a>Ejemplos de código

|Ejemplo de nombre | Descripción | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Bot de servicio de alimentos de Teams | Cree un bot que acepte el pedido de alimentos mediante tarjetas adaptables. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)| Aún no disponible |
| Tarjetas adaptables de flujos de trabajo secuenciales | Muestra cómo implementar flujos de trabajo secuenciales, vistas específicas del usuario y tarjetas adaptables actualizadas en bots. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>Consulte también

* [Acciones de tarjeta adaptable en Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [Cómo funcionan los bots](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [Trabajar con Acciones universales para tarjetas adaptables](Work-with-universal-actions-for-adaptive-cards.md)
* [Comentarios de finalización de formularios](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)

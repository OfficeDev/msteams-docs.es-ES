---
title: Actualizar y eliminar mensajes enviados desde el bot
author: WashingtonKayaker
description: Cómo actualizar y eliminar mensajes enviados desde el bot de Microsoft Teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 04a17914efd40173d761537773613b93563999aa
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596206"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a>Actualizar y eliminar mensajes enviados desde el bot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="update-messages"></a>Actualizar mensajes

El bot puede actualizar dinámicamente los mensajes después de enviarlos. Puede usar actualizaciones dinámicas de mensajes para escenarios como las actualizaciones de sondeo, la modificación de acciones disponibles después de presionar un botón o cualquier otro cambio de estado asincrónico.

El nuevo mensaje no necesita coincidir con el tipo original. Por ejemplo, si el mensaje original contenía datos adjuntos, el nuevo mensaje puede ser un mensaje de texto simple.

# <a name="c"></a>[C#](#tab/dotnet)

Para actualizar un mensaje existente, pase un nuevo objeto con el identificador de actividad `Activity` existente al método de la `UpdateActivityAsync` `TurnContext` clase. Vea [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Para actualizar un mensaje existente, pase un nuevo objeto con el identificador de actividad `Activity` existente al método del `updateActivity` `TurnContext` objeto. Vea [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[Python](#tab/python)

Para actualizar un mensaje existente, pase un nuevo objeto con el identificador de actividad `Activity` existente al método de la `update_activity` `TurnContext` clase. Vea [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

# <a name="rest-api"></a>[API de REST](#tab/rest)

>[!NOTE]
>Puede desarrollar aplicaciones de Teams en cualquier tecnología de programación web y llamar directamente a las API rest del servicio [Bot Connector.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true) Para ello, debe implementar procedimientos de seguridad [de](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) autenticación con las solicitudes de API.

Para actualizar una actividad existente dentro de una conversación, incluya y `conversationId` en el extremo de `activityId` solicitud. Para completar este escenario, debe almacenar en caché el identificador de actividad devuelto por la llamada POST original.

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|Solicitud |Respuesta |
|----|----|
|Un [objeto Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) |Un [objeto ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true)  |

---

## <a name="update-cards"></a>Actualizar tarjetas

Para actualizar la tarjeta existente en la selección de botón, puede usar `ReplyToId` la actividad entrante.

# <a name="c"></a>[C#](#tab/dotnet)

Para actualizar la tarjeta existente en un clic de botón, pase un nuevo objeto con la tarjeta actualizada y como identificador de actividad `Activity` al método de la `ReplyToId` `UpdateActivityAsync` `TurnContext` clase. Vea [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).
```csharp
var activity = MessageFactory.Attachment(card.ToAttachment());
activity.Id = turnContext.Activity.ReplyToId;
await turnContext.UpdateActivityAsync(activity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)


Para actualizar la tarjeta existente en un clic de botón, pase un nuevo objeto con la tarjeta actualizada y como identificador de actividad al `Activity` `replyToId` método del `updateActivity` `TurnContext` objeto. Vea [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).
```typescript
const message = MessageFactory.attachment(card);
message.id = context.activity.replyToId;
await context.updateActivity(message);
```

# <a name="python"></a>[Python](#tab/python)

Para actualizar la tarjeta existente en un clic de botón, pase un nuevo objeto con la tarjeta actualizada y como identificador de actividad `Activity` al método de la `reply_to_id` `update_activity` `TurnContext` clase. Vea [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).

```python
updated_activity = MessageFactory.attachment(CardFactory.hero_card(card))
updated_activity.id = turn_context.activity.reply_to_id
await turn_context.update_activity(updated_activity)

```

# <a name="rest-api"></a>[API de REST](#tab/rest)

Para actualizar una actividad existente dentro de una conversación, incluya y `conversationId` en el extremo de `activityId` solicitud. Para completar este escenario, debe almacenar en caché el identificador de actividad devuelto por la llamada posterior original.

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|Solicitud |Respuesta |
|----|----|
| Un [objeto Activity.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) | Un [objeto ResourceResponse.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) |

---

## <a name="delete-messages"></a>Eliminar mensajes

En Bot Framework, cada mensaje tiene su propio identificador de actividad único.
Los mensajes se pueden eliminar con el método de Bot `DeleteActivity` Framework, como se muestra aquí.

# <a name="c"></a>[C#](#tab/dotnet)

Para eliminar ese mensaje, pase el identificador de esa actividad al `DeleteActivityAsync` método de la `TurnContext` clase. Consulta [TurnContext.DeleteActivityAsync (método).](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true)

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Para eliminar ese mensaje, pase el identificador de esa actividad al `deleteActivity` método del `TurnContext` objeto. Vea [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true).

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[Python](#tab/python)

Para eliminar ese mensaje, pase el identificador de esa actividad al `delete_activity` método del `TurnContext` objeto. Vea [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[API de REST](#tab/rest)

Para eliminar una actividad existente dentro de una conversación, incluya y `conversationId` en el extremo de `activityId` solicitud.

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

|Solicitud |Respuesta |
|----|----|
| N/D | Código de estado HTTP que indica el resultado de la operación. No se especifica nada en el cuerpo de la respuesta. |

---

## <a name="code-samples"></a>Muestras de código

Los conceptos básicos de la conversación oficial son los siguientes:

| Nombre de ejemplo           | Descripción                                                                      | .NET    | Node.js   | Python  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|Conceptos básicos de la conversación de Teams  | Muestra los conceptos básicos de las conversaciones en Teams, incluida la actualización y eliminación de mensajes.|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot)|

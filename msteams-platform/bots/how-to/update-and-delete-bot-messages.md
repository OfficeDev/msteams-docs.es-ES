---
title: Actualizar y eliminar mensajes enviados desde el bot
author: WashingtonKayaker
description: Obtenga información sobre cómo actualizar y eliminar los mensajes enviados desde el bot Microsoft Teams en diferentes entornos y con api de REST con ejemplos de código.
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: b92eb5c566df1d23b0228a218afa546160a3bb91
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889345"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a>Actualizar y eliminar mensajes enviados desde el bot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

El bot puede actualizar dinámicamente los mensajes después de enviarlos en lugar de tenerlos como instantáneas estáticas de datos. Los mensajes también se pueden eliminar mediante el método de Bot `DeleteActivity` Framework.

## <a name="update-messages"></a>Actualizar mensajes

Puede usar actualizaciones dinámicas de mensajes para escenarios, como las actualizaciones de sondeo, la modificación de las acciones disponibles después de presionar un botón o cualquier otro cambio de estado asincrónico.

No es necesario que el nuevo mensaje coincida con el tipo original. Por ejemplo, si el mensaje original contiene datos adjuntos, el nuevo mensaje puede ser un mensaje de texto simple.

# <a name="c"></a>[C#](#tab/dotnet)

Para actualizar un mensaje existente, pase un nuevo objeto con el identificador de actividad `Activity` existente al método de la `UpdateActivityAsync` `TurnContext` clase. Para obtener más información, [vea TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Para actualizar un mensaje existente, pase un nuevo objeto con el identificador de actividad `Activity` existente al método del `updateActivity` `TurnContext` objeto. Para obtener más información, [vea updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).

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

> [!NOTE]

> Puede desarrollar aplicaciones Teams en cualquier tecnología de programación web y llamar directamente a las API rest del servicio [Bot Connector.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true) Para ello, debe implementar procedimientos de seguridad [de](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) autenticación con las solicitudes de API.

Para actualizar una actividad existente dentro de una conversación, incluya y `conversationId` en el extremo de `activityId` solicitud. Para completar este escenario, debe almacenar en caché el identificador de actividad devuelto por la llamada posterior original.

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|Solicitud |Respuesta |
|----|----|
| Un [objeto Activity.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) | Un [objeto ResourceResponse.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) |

---
* * *

Ahora que ha actualizado los mensajes, actualice la tarjeta existente en la selección de botón para las actividades entrantes.

## <a name="update-cards"></a>Actualizar tarjetas

Para actualizar la tarjeta existente en la selección de botón, puede usar `ReplyToId` la actividad entrante.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

Para actualizar la tarjeta existente en una selección de botón, pase un nuevo objeto con la tarjeta actualizada y como identificador de actividad `Activity` al método de la `ReplyToId` `UpdateActivityAsync` `TurnContext` clase. Vea [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).

```csharp
var activity = MessageFactory.Attachment(card.ToAttachment());
activity.Id = turnContext.Activity.ReplyToId;
await turnContext.UpdateActivityAsync(activity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Para actualizar la tarjeta existente en una selección de botón, pase un nuevo objeto con la tarjeta actualizada y como identificador de actividad `Activity` `replyToId` al método del `updateActivity` `TurnContext` objeto. Vea [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).

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

> [!NOTE]
> Puede desarrollar aplicaciones Teams en cualquier tecnología de programación web y llamar directamente a las API rest del servicio [de conector de bot.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true) Para ello, debe implementar procedimientos de seguridad [de](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) autenticación con las solicitudes DE API.

Para actualizar una actividad existente dentro de una conversación, incluya y `conversationId` en el extremo de `activityId` solicitud. Para completar este escenario, debe almacenar en caché el identificador de actividad devuelto por la llamada posterior original.

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|Solicitud |Respuesta |
|----|----|
| Un [objeto activity.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) | Un [objeto ResourceResponse.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) |

* * *

Ahora que ha actualizado las tarjetas, puede eliminar mensajes con Bot Framework.

## <a name="delete-messages"></a>Eliminar mensajes

En Bot Framework, cada mensaje tiene su identificador de actividad único. Los mensajes se pueden eliminar mediante el método de Bot `DeleteActivity` Framework.

# <a name="c"></a>[C#](#tab/dotnet)

Para eliminar un mensaje, pase el identificador de esa actividad al `DeleteActivityAsync` método de la `TurnContext` clase. Para obtener más información, [consulta TurnContext.DeleteActivityAsync (método).](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true)

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Para eliminar un mensaje, pase el identificador de esa actividad al `deleteActivity` método del `TurnContext` objeto. Para obtener más información, [vea deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true).

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[Python](#tab/python)

Para eliminar ese mensaje, pase el identificador de esa actividad al `delete_activity` método del `TurnContext` objeto. Para obtener más información, [vea activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[API de REST](#tab/rest)

Para eliminar una actividad existente dentro de una conversación, incluya y `conversationId` en el extremo de `activityId` solicitud.

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| **Solicitud y respuesta** | **Descripción** |
|----|----|
| N/D | Un código de estado HTTP que indica el resultado de la operación. No se especifica nada en el cuerpo de la respuesta. |

---

## <a name="code-sample"></a>Ejemplo de código

En el ejemplo de código siguiente se muestran los conceptos básicos de las conversaciones:

| **Ejemplo de nombre** | **Descripción** | **.NET** | **Node.js** | **Python** |
|----------------------|-----------------|--------|-------------|--------|
| Teams Conceptos básicos de conversación  | Muestra los conceptos básicos de las conversaciones en Teams actualización y eliminación de mensajes. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Obtener Teams contexto](~/bots/how-to/get-teams-context.md)

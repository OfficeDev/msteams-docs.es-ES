---
title: Actualización y eliminación de mensajes enviados desde su bot
author: WashingtonKayaker
description: Obtenga información sobre cómo actualizar y eliminar los mensajes enviados desde el bot de Microsoft Teams en diferentes entornos y con las API rest mediante ejemplos (.NET, Node.js, Python).
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: d85bb7086661eba58c6cf852cab599970fdc9c80
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100822"
---
# <a name="update-and-delete-messages-sent-from-bot"></a>Actualización y eliminación de mensajes enviados desde el bot 

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Su bot puede actualizar dinámicamente los mensajes después de enviarlos en lugar de tenerlos como instantáneas estáticas de datos. Los mensajes también se pueden eliminar mediante el método `DeleteActivity` de Bot Framework.

## <a name="update-messages"></a>Actualizar mensajes

Puede usar actualizaciones de mensajes dinámicos para escenarios como las actualizaciones de sondeo, la modificación de las acciones disponibles después de presionar un botón o cualquier otro cambio de estado asincrónico.

No es necesario que el nuevo mensaje coincida con el tipo original. Por ejemplo, si el mensaje original contenía datos adjuntos, el nuevo mensaje puede ser un mensaje de texto simple.

# <a name="c"></a>[C#](#tab/dotnet)

Para actualizar un mensaje existente, pase un nuevo objeto `Activity` con el identificador de actividad existente al método `UpdateActivityAsync` de la clase `TurnContext`. Para obtener más información, consulte [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Para actualizar un mensaje existente, pase un nuevo objeto `Activity` con el identificador de actividad existente al método `updateActivity` del objeto `TurnContext`. Para obtener más información, consulte [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[Python](#tab/python)

Para actualizar un mensaje existente, pase un nuevo objeto `Activity` con el identificador de actividad existente al método `update_activity` de la clase `TurnContext`. Consulte [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).

```python
new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)
```

# <a name="rest-api"></a>[API de REST](#tab/rest)

> [!NOTE]
> Puede desarrollar aplicaciones de Teams en cualquier tecnología de programación web y llamar directamente a las [API de REST del servicio Bot Connector](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true). Para ello, debe implementar la [Autenticación](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) de procedimientos seguridad con sus solicitudes de API.

Para actualizar una actividad existente en una conversación, incluya el `conversationId` y `activityId` en el punto de conexión de solicitud. Para completar este escenario, debe almacenar en caché el identificador de actividad devuelto por la llamada post original.

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|Solicitud |Respuesta |
|----|----|
| Un objeto de [Actividad](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true). | Un objeto [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true). |

---
---

Ahora que ha actualizado los mensajes, actualice la tarjeta existente en la selección de botón para las actividades entrantes.

## <a name="update-cards"></a>Actualizar tarjetas

Para actualizar la tarjeta existente en la selección de botón, puede usar `ReplyToId` de actividad entrante.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

Para actualizar la tarjeta existente en una selección de botón, pase un nuevo objeto `Activity` con tarjeta actualizada y `ReplyToId` como identificador de actividad al método `UpdateActivityAsync` de la clase `TurnContext`. Consulte [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).

```csharp
var activity = MessageFactory.Attachment(card.ToAttachment());
activity.Id = turnContext.Activity.ReplyToId;
await turnContext.UpdateActivityAsync(activity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Para actualizar la tarjeta existente en una selección de botón, pase un nuevo objeto `Activity` con tarjeta actualizada y `replyToId` como identificador de actividad al método `updateActivity` del objeto `TurnContext`. Consulte [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).

```typescript
const message = MessageFactory.attachment(card);
message.id = context.activity.replyToId;
await context.updateActivity(message);
```

# <a name="python"></a>[Python](#tab/python)

Para actualizar la tarjeta existente al hacer clic en un botón, pase un nuevo objeto `Activity` con tarjeta actualizada y `reply_to_id` como identificador de actividad al método `update_activity` de la clase `TurnContext`. Consulte [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).

```python
updated_activity = MessageFactory.attachment(CardFactory.hero_card(card))
updated_activity.id = turn_context.activity.reply_to_id
await turn_context.update_activity(updated_activity)
```

# <a name="rest-api"></a>[API de REST](#tab/rest)

> [!NOTE]
> Puede desarrollar aplicaciones de Teams en cualquier tecnología de programación web y llamar directamente a las [API de REST del servicio Bot Connector](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true). Para ello, debe implementar la [autenticación](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) de procedimientos de seguridad con las solicitudes de API.

Para actualizar una actividad existente en una conversación, incluya el `conversationId` y `activityId` en el punto de conexión de solicitud. Para completar este escenario, debe almacenar en caché el identificador de actividad devuelto por la llamada post original.

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|Solicitud |Respuesta |
|----|----|
| Un objeto de [actividad](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true). | Un objeto [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true). |

---

Ahora que ha actualizado las tarjetas, puede eliminar mensajes mediante Bot Framework.

## <a name="delete-messages"></a>Eliminar mensajes

En Bot Framework, cada mensaje tiene su identificador de actividad único. Los mensajes se pueden eliminar mediante el método `DeleteActivity` de Bot Framework.

# <a name="c"></a>[C#](#tab/dotnet)

Para eliminar un mensaje, pase el identificador de esa actividad al método `DeleteActivityAsync` de la clase `TurnContext`. Para obtener más información, consulte [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true).

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Para eliminar un mensaje, pase el identificador de esa actividad al método `deleteActivity` del objeto `TurnContext`. Para obtener más información, consulte [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true).

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[Python](#tab/python)

Para eliminar ese mensaje, pase el identificador de esa actividad al método `delete_activity` del objeto `TurnContext`. Para obtener más información, consulte [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[API de REST](#tab/rest)

Para eliminar una actividad existente en una conversación, incluya el `conversationId` y `activityId` en el punto de conexión de la solicitud.

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| **Solicitud y respuesta** | **Descripción** |
|----|----|
| N/D | Código de estado HTTP que indica el resultado de la operación. No se especifica nada en el cuerpo de la respuesta. |

---

## <a name="code-sample"></a>Ejemplo de código

En el ejemplo de código siguiente se muestran los datos básicos de las conversaciones:

| **Ejemplo de nombre** | **Descripción** | **.NET** | **Node.js** | **Python** |
|----------------------|-----------------|--------|-------------|--------|
| Conceptos básicos de conversación de Teams  | Muestra los datos básicos de las conversaciones en Teams, incluida la actualización y eliminación de mensajes. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> Consulte [Obtener contexto de Teams](~/bots/how-to/get-teams-context.md).

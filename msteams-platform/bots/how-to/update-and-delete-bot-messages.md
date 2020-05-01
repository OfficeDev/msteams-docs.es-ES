---
title: Actualizar y eliminar los mensajes enviados desde el bot
author: WashingtonKayaker
description: Cómo actualizar y eliminar los mensajes enviados desde su bot de Microsoft Teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 46994c6810197002ef1c108af4f725426395b37f
ms.sourcegitcommit: 2b1fd50466d807869fd173371ba7dfd82a0064ac
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2020
ms.locfileid: "43957190"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a>Actualizar y eliminar los mensajes enviados desde el bot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="updating-messages"></a>Actualizar mensajes

En lugar de que los mensajes sean instantáneas estáticas de los datos, el bot puede actualizar de forma dinámica los mensajes después de enviarlos. Puede usar actualizaciones de mensajes dinámicas para escenarios como sondeos de actualizaciones, modificación de acciones disponibles después de presionar un botón o cualquier otro cambio de estado asincrónico.

El nuevo mensaje no tiene que coincidir con el original en el tipo. Por ejemplo, si el mensaje original contenía datos adjuntos, el nuevo mensaje puede ser un mensaje de texto simple.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

Para actualizar un mensaje existente, pase un nuevo `Activity` objeto con el identificador de actividad existente al `UpdateActivityAsync` método de la `TurnContext` clase. *Consulte* [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

Para actualizar un mensaje existente, pase un nuevo `Activity` objeto con el identificador de actividad existente al `updateActivity` método del `TurnContext` objeto. *Consulte* [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[Python](#tab/python)

Para actualizar un mensaje existente, pase un nuevo `Activity` objeto con el identificador de actividad existente al `update_activity` método de la `TurnContext` clase. Consulte [TurnContextClass](link to Python API ref docs).

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

# <a name="rest-api"></a>[API de REST](#tab/rest)

>[!NOTE]
>Puede desarrollar las aplicaciones de Microsoft Teams en cualquier tecnología de programación web y llamar directamente a las [API de REST del servicio de conector de bot](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0). Para ello, deberá implementar los procedimientos de seguridad de [autenticación](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0) con sus solicitudes de API.

Para actualizar una actividad existente dentro de una conversación, incluya `conversationId` el `activityId` y en el punto de conexión de la solicitud. Para completar este escenario, debe almacenar en caché el identificador de actividad devuelto por la llamada de publicación original.

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| **Cuerpo de la solicitud** | Un objeto [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object) |
| **Devuelve** | Un objeto [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object) |

---

## <a name="deleting-messages"></a>Eliminación de mensajes

En el marco de bot, todos los mensajes tienen su propio identificador de actividad único.
Los mensajes se pueden eliminar mediante el método del `DeleteActivity` marco de trabajo de bot, como se muestra aquí.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

Para eliminar ese mensaje, pase el `DeleteActivityAsync` identificador de la actividad al método de la `TurnContext` clase. *Consulte* [método TurnContext. DeleteActivityAsync](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

Para eliminar ese mensaje, pase el `deleteActivity` identificador de la actividad al método del `TurnContext` objeto. *Consulte* [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[Python](#tab/python)

Para eliminar ese mensaje, pase el `delete_activity` identificador de la actividad al método del `TurnContext` objeto. Consulte [Activity-Update-and-Delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[API de REST](#tab/rest)

 Para eliminar una actividad existente dentro de una conversación, incluya `conversationId` el `activityId` y en el extremo de la solicitud.

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| **Cuerpo de la solicitud** | N/D |
| **Devuelve** | Código de Estado HTTP que indica el resultado de la operación. No se especifica nada en el cuerpo de la respuesta. |

---

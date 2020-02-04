---
title: Actualizar y eliminar los mensajes enviados desde el bot
author: WashingtonKayaker
description: Cómo actualizar y eliminar los mensajes enviados desde su bot de Microsoft Teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 012a6edb77f75c43cff01c58fb94e03fd4f61a85
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676095"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a>Actualizar y eliminar los mensajes enviados desde el bot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="updating-messages"></a>Actualizar mensajes

En lugar de que los mensajes sean instantáneas estáticas de los datos, el bot puede actualizar de forma dinámica los mensajes después de enviarlos. Puede usar actualizaciones de mensajes dinámicas para escenarios como sondeos de actualizaciones, modificación de acciones disponibles después de presionar un botón o cualquier otro cambio de estado asincrónico.

El nuevo mensaje no tiene que coincidir con el original en el tipo. Por ejemplo, si el mensaje original contenía datos adjuntos, el nuevo mensaje puede ser un mensaje de texto simple.

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

Para actualizar un mensaje existente, pase un nuevo `Activity` objeto con el identificador de actividad existente al `UpdateActivityAsync` método de la `TurnContext` clase. *Consulte* [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node. js](#tab/typescript)

Para actualizar un mensaje existente, pase un nuevo `Activity` objeto con el identificador de actividad existente al `updateActivity` método del `TurnContext` objeto. *Consulte* [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="pythontabpython"></a>[Python](#tab/python)

Para actualizar un mensaje existente, pase un nuevo `Activity` objeto con el identificador de actividad existente al `update_activity` método de la `TurnContext` clase. Consulte [TurnContextClass](link to Python API ref docs).

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

---

## <a name="deleting-messages"></a>Eliminación de mensajes

En el marco de bot, todos los mensajes tienen su propio identificador de actividad único.
Los mensajes se pueden eliminar mediante el método del `DeleteActivity` marco de trabajo de bot, como se muestra aquí.

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

Para eliminar ese mensaje, pase el `DeleteActivityAsync` identificador de la actividad al método de la `TurnContext` clase. *Consulte* [método TurnContext. DeleteActivityAsync](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node. js](#tab/typescript)

Para eliminar ese mensaje, pase el `deleteActivity` identificador de la actividad al método del `TurnContext` objeto. *Consulte* [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="pythontabpython"></a>[Python](#tab/python)

Para eliminar ese mensaje, pase el `delete_activity` identificador de la actividad al método del `TurnContext` objeto. Consulte [delete_activity](link to Python API ref docs).

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

---


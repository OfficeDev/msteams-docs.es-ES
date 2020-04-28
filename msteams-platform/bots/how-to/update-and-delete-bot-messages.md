---
title: Actualizar y eliminar los mensajes enviados desde el bot
author: WashingtonKayaker
description: Cómo actualizar y eliminar los mensajes enviados desde su bot de Microsoft Teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 222409fa0d02a571b7295dedb0c60b1ca3f90cca
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2020
ms.locfileid: "43914612"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a><span data-ttu-id="c071c-103">Actualizar y eliminar los mensajes enviados desde el bot</span><span class="sxs-lookup"><span data-stu-id="c071c-103">Update and delete messages sent from your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="updating-messages"></a><span data-ttu-id="c071c-104">Actualizar mensajes</span><span class="sxs-lookup"><span data-stu-id="c071c-104">Updating messages</span></span>

<span data-ttu-id="c071c-105">En lugar de que los mensajes sean instantáneas estáticas de los datos, el bot puede actualizar de forma dinámica los mensajes después de enviarlos.</span><span class="sxs-lookup"><span data-stu-id="c071c-105">Rather than have your messages be static snapshots of data, your bot can dynamically update messages after sending them.</span></span> <span data-ttu-id="c071c-106">Puede usar actualizaciones de mensajes dinámicas para escenarios como sondeos de actualizaciones, modificación de acciones disponibles después de presionar un botón o cualquier otro cambio de estado asincrónico.</span><span class="sxs-lookup"><span data-stu-id="c071c-106">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="c071c-107">El nuevo mensaje no tiene que coincidir con el original en el tipo.</span><span class="sxs-lookup"><span data-stu-id="c071c-107">The new message need not match the original in type.</span></span> <span data-ttu-id="c071c-108">Por ejemplo, si el mensaje original contenía datos adjuntos, el nuevo mensaje puede ser un mensaje de texto simple.</span><span class="sxs-lookup"><span data-stu-id="c071c-108">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="c071c-109">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="c071c-109">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="c071c-110">Para actualizar un mensaje existente, pase un nuevo `Activity` objeto con el identificador de actividad existente al `UpdateActivityAsync` método de la `TurnContext` clase.</span><span class="sxs-lookup"><span data-stu-id="c071c-110">To update an existing message, pass a new `Activity` object with the existing activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="c071c-111">*Consulte* [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)</span><span class="sxs-lookup"><span data-stu-id="c071c-111">*See* [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)</span></span>

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="c071c-112">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="c071c-112">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="c071c-113">Para actualizar un mensaje existente, pase un nuevo `Activity` objeto con el identificador de actividad existente al `updateActivity` método del `TurnContext` objeto.</span><span class="sxs-lookup"><span data-stu-id="c071c-113">To update an existing message, pass a new `Activity` object with the existing activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="c071c-114">*Consulte* [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)</span><span class="sxs-lookup"><span data-stu-id="c071c-114">*See* [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)</span></span>

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[<span data-ttu-id="c071c-115">Python</span><span class="sxs-lookup"><span data-stu-id="c071c-115">Python</span></span>](#tab/python)

<span data-ttu-id="c071c-116">Para actualizar un mensaje existente, pase un nuevo `Activity` objeto con el identificador de actividad existente al `update_activity` método de la `TurnContext` clase.</span><span class="sxs-lookup"><span data-stu-id="c071c-116">To update an existing message, pass a new `Activity` object with the existing activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="c071c-117">Consulte [TurnContextClass](link to Python API ref docs).</span><span class="sxs-lookup"><span data-stu-id="c071c-117">See [TurnContextClass](link to Python API ref docs).</span></span>

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

---

## <a name="deleting-messages"></a><span data-ttu-id="c071c-118">Eliminación de mensajes</span><span class="sxs-lookup"><span data-stu-id="c071c-118">Deleting messages</span></span>

<span data-ttu-id="c071c-119">En el marco de bot, todos los mensajes tienen su propio identificador de actividad único.</span><span class="sxs-lookup"><span data-stu-id="c071c-119">In the Bot Framework, every message has its own unique activity identifier.</span></span>
<span data-ttu-id="c071c-120">Los mensajes se pueden eliminar mediante el método del `DeleteActivity` marco de trabajo de bot, como se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="c071c-120">Messages can be deleted using the Bot Framework's `DeleteActivity` method as shown here.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="c071c-121">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="c071c-121">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="c071c-122">Para eliminar ese mensaje, pase el `DeleteActivityAsync` identificador de la actividad al método de la `TurnContext` clase.</span><span class="sxs-lookup"><span data-stu-id="c071c-122">To delete that message, pass that activity's ID to the `DeleteActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="c071c-123">*Consulte* [método TurnContext. DeleteActivityAsync](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)</span><span class="sxs-lookup"><span data-stu-id="c071c-123">*See* [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)</span></span>

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="c071c-124">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="c071c-124">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="c071c-125">Para eliminar ese mensaje, pase el `deleteActivity` identificador de la actividad al método del `TurnContext` objeto.</span><span class="sxs-lookup"><span data-stu-id="c071c-125">To delete that message, pass that activity's ID to the `deleteActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="c071c-126">*Consulte* [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)</span><span class="sxs-lookup"><span data-stu-id="c071c-126">*See* [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)</span></span>

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[<span data-ttu-id="c071c-127">Python</span><span class="sxs-lookup"><span data-stu-id="c071c-127">Python</span></span>](#tab/python)

<span data-ttu-id="c071c-128">Para eliminar ese mensaje, pase el `delete_activity` identificador de la actividad al método del `TurnContext` objeto.</span><span class="sxs-lookup"><span data-stu-id="c071c-128">To delete that message, pass that activity's ID to the `delete_activity` method of the `TurnContext` object.</span></span> <span data-ttu-id="c071c-129">Consulte [Activity-Update-and-Delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span><span class="sxs-lookup"><span data-stu-id="c071c-129">See [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span></span>

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

---


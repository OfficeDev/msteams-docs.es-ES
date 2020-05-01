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
# <a name="update-and-delete-messages-sent-from-your-bot"></a><span data-ttu-id="b6829-103">Actualizar y eliminar los mensajes enviados desde el bot</span><span class="sxs-lookup"><span data-stu-id="b6829-103">Update and delete messages sent from your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="updating-messages"></a><span data-ttu-id="b6829-104">Actualizar mensajes</span><span class="sxs-lookup"><span data-stu-id="b6829-104">Updating messages</span></span>

<span data-ttu-id="b6829-105">En lugar de que los mensajes sean instantáneas estáticas de los datos, el bot puede actualizar de forma dinámica los mensajes después de enviarlos.</span><span class="sxs-lookup"><span data-stu-id="b6829-105">Rather than have your messages be static snapshots of data, your bot can dynamically update messages after sending them.</span></span> <span data-ttu-id="b6829-106">Puede usar actualizaciones de mensajes dinámicas para escenarios como sondeos de actualizaciones, modificación de acciones disponibles después de presionar un botón o cualquier otro cambio de estado asincrónico.</span><span class="sxs-lookup"><span data-stu-id="b6829-106">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="b6829-107">El nuevo mensaje no tiene que coincidir con el original en el tipo.</span><span class="sxs-lookup"><span data-stu-id="b6829-107">The new message need not match the original in type.</span></span> <span data-ttu-id="b6829-108">Por ejemplo, si el mensaje original contenía datos adjuntos, el nuevo mensaje puede ser un mensaje de texto simple.</span><span class="sxs-lookup"><span data-stu-id="b6829-108">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="b6829-109">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="b6829-109">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="b6829-110">Para actualizar un mensaje existente, pase un nuevo `Activity` objeto con el identificador de actividad existente al `UpdateActivityAsync` método de la `TurnContext` clase.</span><span class="sxs-lookup"><span data-stu-id="b6829-110">To update an existing message, pass a new `Activity` object with the existing activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="b6829-111">*Consulte* [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)</span><span class="sxs-lookup"><span data-stu-id="b6829-111">*See* [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)</span></span>

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="b6829-112">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="b6829-112">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="b6829-113">Para actualizar un mensaje existente, pase un nuevo `Activity` objeto con el identificador de actividad existente al `updateActivity` método del `TurnContext` objeto.</span><span class="sxs-lookup"><span data-stu-id="b6829-113">To update an existing message, pass a new `Activity` object with the existing activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="b6829-114">*Consulte* [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)</span><span class="sxs-lookup"><span data-stu-id="b6829-114">*See* [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)</span></span>

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[<span data-ttu-id="b6829-115">Python</span><span class="sxs-lookup"><span data-stu-id="b6829-115">Python</span></span>](#tab/python)

<span data-ttu-id="b6829-116">Para actualizar un mensaje existente, pase un nuevo `Activity` objeto con el identificador de actividad existente al `update_activity` método de la `TurnContext` clase.</span><span class="sxs-lookup"><span data-stu-id="b6829-116">To update an existing message, pass a new `Activity` object with the existing activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="b6829-117">Consulte [TurnContextClass](link to Python API ref docs).</span><span class="sxs-lookup"><span data-stu-id="b6829-117">See [TurnContextClass](link to Python API ref docs).</span></span>

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

# <a name="rest-api"></a>[<span data-ttu-id="b6829-118">API de REST</span><span class="sxs-lookup"><span data-stu-id="b6829-118">REST API</span></span>](#tab/rest)

>[!NOTE]
><span data-ttu-id="b6829-119">Puede desarrollar las aplicaciones de Microsoft Teams en cualquier tecnología de programación web y llamar directamente a las [API de REST del servicio de conector de bot](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0).</span><span class="sxs-lookup"><span data-stu-id="b6829-119">You can develop Teams apps in any web-programming technology and directly call the [Bot Connector service REST APIs](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0).</span></span> <span data-ttu-id="b6829-120">Para ello, deberá implementar los procedimientos de seguridad de [autenticación](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0) con sus solicitudes de API.</span><span class="sxs-lookup"><span data-stu-id="b6829-120">To do so, you'll need to implement [Authentication](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0) security procedures with your API requests.</span></span>

<span data-ttu-id="b6829-121">Para actualizar una actividad existente dentro de una conversación, incluya `conversationId` el `activityId` y en el punto de conexión de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="b6829-121">To update an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span> <span data-ttu-id="b6829-122">Para completar este escenario, debe almacenar en caché el identificador de actividad devuelto por la llamada de publicación original.</span><span class="sxs-lookup"><span data-stu-id="b6829-122">To complete this scenario, you should cache the activity ID returned by the original POST call.</span></span>

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| <span data-ttu-id="b6829-123">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="b6829-123">**Request body**</span></span> | <span data-ttu-id="b6829-124">Un objeto [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object)</span><span class="sxs-lookup"><span data-stu-id="b6829-124">An [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object) object</span></span> |
| <span data-ttu-id="b6829-125">**Devuelve**</span><span class="sxs-lookup"><span data-stu-id="b6829-125">**Returns**</span></span> | <span data-ttu-id="b6829-126">Un objeto [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object)</span><span class="sxs-lookup"><span data-stu-id="b6829-126">A [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object) object</span></span> |

---

## <a name="deleting-messages"></a><span data-ttu-id="b6829-127">Eliminación de mensajes</span><span class="sxs-lookup"><span data-stu-id="b6829-127">Deleting messages</span></span>

<span data-ttu-id="b6829-128">En el marco de bot, todos los mensajes tienen su propio identificador de actividad único.</span><span class="sxs-lookup"><span data-stu-id="b6829-128">In the Bot Framework, every message has its own unique activity identifier.</span></span>
<span data-ttu-id="b6829-129">Los mensajes se pueden eliminar mediante el método del `DeleteActivity` marco de trabajo de bot, como se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="b6829-129">Messages can be deleted using the Bot Framework's `DeleteActivity` method as shown here.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="b6829-130">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="b6829-130">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="b6829-131">Para eliminar ese mensaje, pase el `DeleteActivityAsync` identificador de la actividad al método de la `TurnContext` clase.</span><span class="sxs-lookup"><span data-stu-id="b6829-131">To delete that message, pass that activity's ID to the `DeleteActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="b6829-132">*Consulte* [método TurnContext. DeleteActivityAsync](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)</span><span class="sxs-lookup"><span data-stu-id="b6829-132">*See* [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)</span></span>

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="b6829-133">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="b6829-133">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="b6829-134">Para eliminar ese mensaje, pase el `deleteActivity` identificador de la actividad al método del `TurnContext` objeto.</span><span class="sxs-lookup"><span data-stu-id="b6829-134">To delete that message, pass that activity's ID to the `deleteActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="b6829-135">*Consulte* [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)</span><span class="sxs-lookup"><span data-stu-id="b6829-135">*See* [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)</span></span>

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[<span data-ttu-id="b6829-136">Python</span><span class="sxs-lookup"><span data-stu-id="b6829-136">Python</span></span>](#tab/python)

<span data-ttu-id="b6829-137">Para eliminar ese mensaje, pase el `delete_activity` identificador de la actividad al método del `TurnContext` objeto.</span><span class="sxs-lookup"><span data-stu-id="b6829-137">To delete that message, pass that activity's ID to the `delete_activity` method of the `TurnContext` object.</span></span> <span data-ttu-id="b6829-138">Consulte [Activity-Update-and-Delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span><span class="sxs-lookup"><span data-stu-id="b6829-138">See [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span></span>

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[<span data-ttu-id="b6829-139">API de REST</span><span class="sxs-lookup"><span data-stu-id="b6829-139">REST API</span></span>](#tab/rest)

 <span data-ttu-id="b6829-140">Para eliminar una actividad existente dentro de una conversación, incluya `conversationId` el `activityId` y en el extremo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="b6829-140">To delete an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span>

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| <span data-ttu-id="b6829-141">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="b6829-141">**Request body**</span></span> | <span data-ttu-id="b6829-142">N/D</span><span class="sxs-lookup"><span data-stu-id="b6829-142">n/a</span></span> |
| <span data-ttu-id="b6829-143">**Devuelve**</span><span class="sxs-lookup"><span data-stu-id="b6829-143">**Returns**</span></span> | <span data-ttu-id="b6829-144">Código de Estado HTTP que indica el resultado de la operación.</span><span class="sxs-lookup"><span data-stu-id="b6829-144">An HTTP Status code that indicates the outcome of the operation.</span></span> <span data-ttu-id="b6829-145">No se especifica nada en el cuerpo de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="b6829-145">Nothing is specified in the body of the response.</span></span> |

---

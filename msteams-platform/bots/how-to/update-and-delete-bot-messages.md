---
title: Actualizar y eliminar mensajes enviados desde el bot
author: WashingtonKayaker
description: Cómo actualizar y eliminar mensajes enviados desde el bot de Microsoft Teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 664bd531bdee0093c6766bc23e35d2bf10307eb4
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449503"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a><span data-ttu-id="54af5-103">Actualizar y eliminar mensajes enviados desde el bot</span><span class="sxs-lookup"><span data-stu-id="54af5-103">Update and delete messages sent from your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="update-messages"></a><span data-ttu-id="54af5-104">Actualizar mensajes</span><span class="sxs-lookup"><span data-stu-id="54af5-104">Update messages</span></span>

<span data-ttu-id="54af5-105">El bot puede actualizar dinámicamente los mensajes después de enviarlos.</span><span class="sxs-lookup"><span data-stu-id="54af5-105">Your bot can dynamically update messages after sending them.</span></span> <span data-ttu-id="54af5-106">Puede usar actualizaciones dinámicas de mensajes para escenarios como las actualizaciones de sondeo, la modificación de acciones disponibles después de presionar un botón o cualquier otro cambio de estado asincrónico.</span><span class="sxs-lookup"><span data-stu-id="54af5-106">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="54af5-107">El nuevo mensaje no necesita coincidir con el tipo original.</span><span class="sxs-lookup"><span data-stu-id="54af5-107">The new message need not match the original in type.</span></span> <span data-ttu-id="54af5-108">Por ejemplo, si el mensaje original contenía datos adjuntos, el nuevo mensaje puede ser un mensaje de texto simple.</span><span class="sxs-lookup"><span data-stu-id="54af5-108">For example, if the original message contained an attachment, the new message can be a simple text message.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="54af5-109">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="54af5-109">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="54af5-110">Para actualizar un mensaje existente, pase un nuevo objeto con el identificador de actividad `Activity` existente al método de la `UpdateActivityAsync` `TurnContext` clase.</span><span class="sxs-lookup"><span data-stu-id="54af5-110">To update an existing message, pass a new `Activity` object with the existing activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="54af5-111">Vea [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="54af5-111">See [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="54af5-112">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="54af5-112">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="54af5-113">Para actualizar un mensaje existente, pase un nuevo objeto con el identificador de actividad `Activity` existente al método del `updateActivity` `TurnContext` objeto.</span><span class="sxs-lookup"><span data-stu-id="54af5-113">To update an existing message, pass a new `Activity` object with the existing activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="54af5-114">Vea [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="54af5-114">See [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span></span>

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[<span data-ttu-id="54af5-115">Python</span><span class="sxs-lookup"><span data-stu-id="54af5-115">Python</span></span>](#tab/python)

<span data-ttu-id="54af5-116">Para actualizar un mensaje existente, pase un nuevo objeto con el identificador de actividad `Activity` existente al método de la `update_activity` `TurnContext` clase.</span><span class="sxs-lookup"><span data-stu-id="54af5-116">To update an existing message, pass a new `Activity` object with the existing activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="54af5-117">Vea [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest).</span><span class="sxs-lookup"><span data-stu-id="54af5-117">See [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest).</span></span>

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

# <a name="rest-api"></a>[<span data-ttu-id="54af5-118">API de REST</span><span class="sxs-lookup"><span data-stu-id="54af5-118">REST API</span></span>](#tab/rest)

>[!NOTE]
><span data-ttu-id="54af5-119">Puede desarrollar aplicaciones de Teams en cualquier tecnología de programación web y llamar directamente a las API rest del servicio [Bot Connector.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="54af5-119">You can develop Teams apps in any web-programming technology and directly call the [Bot Connector service REST APIs](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span> <span data-ttu-id="54af5-120">Para ello, debe implementar procedimientos de seguridad [de](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) autenticación con las solicitudes de API.</span><span class="sxs-lookup"><span data-stu-id="54af5-120">To do so, you need to implement [Authentication](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) security procedures with your API requests.</span></span>

<span data-ttu-id="54af5-121">Para actualizar una actividad existente dentro de una conversación, incluya y `conversationId` en el extremo de `activityId` solicitud.</span><span class="sxs-lookup"><span data-stu-id="54af5-121">To update an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span> <span data-ttu-id="54af5-122">Para completar este escenario, debe almacenar en caché el identificador de actividad devuelto por la llamada POST original.</span><span class="sxs-lookup"><span data-stu-id="54af5-122">To complete this scenario, you must cache the activity ID returned by the original POST call.</span></span>

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| <span data-ttu-id="54af5-123">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="54af5-123">**Request body**</span></span> | <span data-ttu-id="54af5-124">Un [objeto Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="54af5-124">An [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) object</span></span> |
| <span data-ttu-id="54af5-125">**Devuelve**</span><span class="sxs-lookup"><span data-stu-id="54af5-125">**Returns**</span></span> | <span data-ttu-id="54af5-126">Un [objeto ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="54af5-126">A [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) object</span></span> |

---

## <a name="update-cards"></a><span data-ttu-id="54af5-127">Actualizar tarjetas</span><span class="sxs-lookup"><span data-stu-id="54af5-127">Update cards</span></span>

<span data-ttu-id="54af5-128">Para actualizar la tarjeta existente en la selección de botón, puede usar `ReplyToId` la actividad entrante.</span><span class="sxs-lookup"><span data-stu-id="54af5-128">To update the existing card on button selection, you can use `ReplyToId` of incoming activity.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="54af5-129">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="54af5-129">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="54af5-130">Para actualizar la tarjeta existente en un clic de botón, pase un nuevo objeto con la tarjeta actualizada y como identificador de actividad `Activity` al método de la `ReplyToId` `UpdateActivityAsync` `TurnContext` clase.</span><span class="sxs-lookup"><span data-stu-id="54af5-130">To update existing card on a button click, pass a new `Activity` object with updated card and `ReplyToId` as activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="54af5-131">Vea [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="54af5-131">See [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>
```csharp
var activity = MessageFactory.Attachment(card.ToAttachment());
activity.Id = turnContext.Activity.ReplyToId;
await turnContext.UpdateActivityAsync(activity, cancellationToken);
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="54af5-132">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="54af5-132">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="54af5-133">Para actualizar la tarjeta existente en un clic de botón, pase un nuevo objeto con la tarjeta actualizada y como identificador de actividad al `Activity` `replyToId` método del `updateActivity` `TurnContext` objeto.</span><span class="sxs-lookup"><span data-stu-id="54af5-133">To update existing card on a button click, pass a new `Activity` object with updated card and `replyToId` as activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="54af5-134">Vea [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="54af5-134">See [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span></span>
```typescript
const message = MessageFactory.attachment(card);
message.id = context.activity.replyToId;
await context.updateActivity(message);
```

# <a name="python"></a>[<span data-ttu-id="54af5-135">Python</span><span class="sxs-lookup"><span data-stu-id="54af5-135">Python</span></span>](#tab/python)

<span data-ttu-id="54af5-136">Para actualizar la tarjeta existente en un clic de botón, pase un nuevo objeto con la tarjeta actualizada y como identificador de actividad `Activity` al método de la `reply_to_id` `update_activity` `TurnContext` clase.</span><span class="sxs-lookup"><span data-stu-id="54af5-136">To update existing card on a button click, pass a new `Activity` object with updated card and `reply_to_id` as activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="54af5-137">Vea [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest).</span><span class="sxs-lookup"><span data-stu-id="54af5-137">See [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest).</span></span>

```python
updated_activity = MessageFactory.attachment(CardFactory.hero_card(card))
updated_activity.id = turn_context.activity.reply_to_id
await turn_context.update_activity(updated_activity)

```

## <a name="delete-messages"></a><span data-ttu-id="54af5-138">Eliminar mensajes</span><span class="sxs-lookup"><span data-stu-id="54af5-138">Delete messages</span></span>

<span data-ttu-id="54af5-139">En Bot Framework, cada mensaje tiene su propio identificador de actividad único.</span><span class="sxs-lookup"><span data-stu-id="54af5-139">In the Bot Framework, every message has its own unique activity identifier.</span></span>
<span data-ttu-id="54af5-140">Los mensajes se pueden eliminar con el método de Bot `DeleteActivity` Framework, como se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="54af5-140">Messages can be deleted using the Bot Framework's `DeleteActivity` method as shown here.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="54af5-141">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="54af5-141">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="54af5-142">Para eliminar ese mensaje, pase el identificador de esa actividad al `DeleteActivityAsync` método de la `TurnContext` clase.</span><span class="sxs-lookup"><span data-stu-id="54af5-142">To delete that message, pass that activity's ID to the `DeleteActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="54af5-143">Consulta [TurnContext.DeleteActivityAsync (método).](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="54af5-143">See [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="54af5-144">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="54af5-144">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="54af5-145">Para eliminar ese mensaje, pase el identificador de esa actividad al `deleteActivity` método del `TurnContext` objeto.</span><span class="sxs-lookup"><span data-stu-id="54af5-145">To delete that message, pass that activity's ID to the `deleteActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="54af5-146">Vea [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="54af5-146">See [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true).</span></span>

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[<span data-ttu-id="54af5-147">Python</span><span class="sxs-lookup"><span data-stu-id="54af5-147">Python</span></span>](#tab/python)

<span data-ttu-id="54af5-148">Para eliminar ese mensaje, pase el identificador de esa actividad al `delete_activity` método del `TurnContext` objeto.</span><span class="sxs-lookup"><span data-stu-id="54af5-148">To delete that message, pass that activity's ID to the `delete_activity` method of the `TurnContext` object.</span></span> <span data-ttu-id="54af5-149">Vea [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span><span class="sxs-lookup"><span data-stu-id="54af5-149">See [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span></span>

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[<span data-ttu-id="54af5-150">API de REST</span><span class="sxs-lookup"><span data-stu-id="54af5-150">REST API</span></span>](#tab/rest)

 <span data-ttu-id="54af5-151">Para eliminar una actividad existente dentro de una conversación, incluya y `conversationId` en el extremo de `activityId` solicitud.</span><span class="sxs-lookup"><span data-stu-id="54af5-151">To delete an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span>

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| <span data-ttu-id="54af5-152">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="54af5-152">**Request body**</span></span> | <span data-ttu-id="54af5-153">n/a</span><span class="sxs-lookup"><span data-stu-id="54af5-153">n/a</span></span> |
| <span data-ttu-id="54af5-154">**Devuelve**</span><span class="sxs-lookup"><span data-stu-id="54af5-154">**Returns**</span></span> | <span data-ttu-id="54af5-155">Código de estado HTTP que indica el resultado de la operación.</span><span class="sxs-lookup"><span data-stu-id="54af5-155">An HTTP Status code that indicates the outcome of the operation.</span></span> <span data-ttu-id="54af5-156">No se especifica nada en el cuerpo de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="54af5-156">Nothing is specified in the body of the response.</span></span> |

---

## <a name="code-samples"></a><span data-ttu-id="54af5-157">Ejemplos de código</span><span class="sxs-lookup"><span data-stu-id="54af5-157">Code samples</span></span>

<span data-ttu-id="54af5-158">Los conceptos básicos de la conversación oficial son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="54af5-158">The official conversation basics are as follows:</span></span>

| <span data-ttu-id="54af5-159">Nombre de ejemplo</span><span class="sxs-lookup"><span data-stu-id="54af5-159">Sample Name</span></span>           | <span data-ttu-id="54af5-160">Descripción</span><span class="sxs-lookup"><span data-stu-id="54af5-160">Description</span></span>                                                                      | <span data-ttu-id="54af5-161">.NET</span><span class="sxs-lookup"><span data-stu-id="54af5-161">.NET</span></span>    | <span data-ttu-id="54af5-162">JavaScript</span><span class="sxs-lookup"><span data-stu-id="54af5-162">JavaScript</span></span>   | <span data-ttu-id="54af5-163">Python</span><span class="sxs-lookup"><span data-stu-id="54af5-163">Python</span></span>  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|<span data-ttu-id="54af5-164">Conceptos básicos de la conversación de Teams</span><span class="sxs-lookup"><span data-stu-id="54af5-164">Teams Conversation Basics</span></span>  | <span data-ttu-id="54af5-165">Muestra los conceptos básicos de las conversaciones en Teams, incluida la actualización y eliminación de mensajes.</span><span class="sxs-lookup"><span data-stu-id="54af5-165">Demonstrates basics of conversations in Teams, including message update and delete.</span></span>|[<span data-ttu-id="54af5-166">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="54af5-166">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="54af5-167">JavaScript</span><span class="sxs-lookup"><span data-stu-id="54af5-167">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="54af5-168">Python</span><span class="sxs-lookup"><span data-stu-id="54af5-168">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot)|

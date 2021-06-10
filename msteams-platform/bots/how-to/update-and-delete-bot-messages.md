---
title: Actualizar y eliminar mensajes enviados desde el bot
author: WashingtonKayaker
description: Cómo actualizar y eliminar mensajes enviados desde el Microsoft Teams bot
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 90dc50fd2ec153813457f199ac029e17a0157502
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101537"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a><span data-ttu-id="c6394-103">Actualizar y eliminar mensajes enviados desde el bot</span><span class="sxs-lookup"><span data-stu-id="c6394-103">Update and delete messages sent from your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="c6394-104">El bot puede actualizar dinámicamente los mensajes después de enviarlos en lugar de tenerlos como instantáneas estáticas de datos.</span><span class="sxs-lookup"><span data-stu-id="c6394-104">Your bot can dynamically update messages after sending them instead of having them as static snapshots of data.</span></span> <span data-ttu-id="c6394-105">Los mensajes también se pueden eliminar mediante el método de Bot `DeleteActivity` Framework.</span><span class="sxs-lookup"><span data-stu-id="c6394-105">Messages can also be deleted using the Bot Framework's `DeleteActivity` method.</span></span>

## <a name="update-messages"></a><span data-ttu-id="c6394-106">Actualizar mensajes</span><span class="sxs-lookup"><span data-stu-id="c6394-106">Update messages</span></span>

<span data-ttu-id="c6394-107">Puede usar actualizaciones dinámicas de mensajes para escenarios, como las actualizaciones de sondeo, la modificación de las acciones disponibles después de presionar un botón o cualquier otro cambio de estado asincrónico.</span><span class="sxs-lookup"><span data-stu-id="c6394-107">You can use dynamic message updates for scenarios, such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="c6394-108">No es necesario que el nuevo mensaje coincida con el tipo original.</span><span class="sxs-lookup"><span data-stu-id="c6394-108">It is not necessary for the new message to match the original in type.</span></span> <span data-ttu-id="c6394-109">Por ejemplo, si el mensaje original contiene datos adjuntos, el nuevo mensaje puede ser un mensaje de texto simple.</span><span class="sxs-lookup"><span data-stu-id="c6394-109">For example, if the original message contains an attachment, the new message can be a simple text message.</span></span>

# <a name="c"></a>[<span data-ttu-id="c6394-110">C#</span><span class="sxs-lookup"><span data-stu-id="c6394-110">C#</span></span>](#tab/dotnet)

<span data-ttu-id="c6394-111">Para actualizar un mensaje existente, pase un nuevo objeto con el identificador de actividad `Activity` existente al método de la `UpdateActivityAsync` `TurnContext` clase.</span><span class="sxs-lookup"><span data-stu-id="c6394-111">To update an existing message, pass a new `Activity` object with the existing activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="c6394-112">Para obtener más información, [vea TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="c6394-112">For more information, see [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescript"></a>[<span data-ttu-id="c6394-113">TypeScript</span><span class="sxs-lookup"><span data-stu-id="c6394-113">TypeScript</span></span>](#tab/typescript)

<span data-ttu-id="c6394-114">Para actualizar un mensaje existente, pase un nuevo objeto con el identificador de actividad `Activity` existente al método del `updateActivity` `TurnContext` objeto.</span><span class="sxs-lookup"><span data-stu-id="c6394-114">To update an existing message, pass a new `Activity` object with the existing activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="c6394-115">Para obtener más información, [vea updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="c6394-115">For more information, see [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span></span>

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[<span data-ttu-id="c6394-116">Python</span><span class="sxs-lookup"><span data-stu-id="c6394-116">Python</span></span>](#tab/python)

<span data-ttu-id="c6394-117">Para actualizar un mensaje existente, pase un nuevo objeto con el identificador de actividad `Activity` existente al método de la `update_activity` `TurnContext` clase.</span><span class="sxs-lookup"><span data-stu-id="c6394-117">To update an existing message, pass a new `Activity` object with the existing activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="c6394-118">Vea [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="c6394-118">See [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).</span></span>

```python
new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)
```

# <a name="rest-api"></a>[<span data-ttu-id="c6394-119">API de REST</span><span class="sxs-lookup"><span data-stu-id="c6394-119">REST API</span></span>](#tab/rest)

> [!NOTE]

> <span data-ttu-id="c6394-120">Puede desarrollar aplicaciones Teams en cualquier tecnología de programación web y llamar directamente a las API rest del servicio [Bot Connector.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c6394-120">You can develop Teams apps in any web-programming technology and directly call the [Bot Connector service REST APIs](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span> <span data-ttu-id="c6394-121">Para ello, debe implementar procedimientos de seguridad [de](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) autenticación con las solicitudes de API.</span><span class="sxs-lookup"><span data-stu-id="c6394-121">To do so, you need to implement [Authentication](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) security procedures with your API requests.</span></span>

<span data-ttu-id="c6394-122">Para actualizar una actividad existente dentro de una conversación, incluya y `conversationId` en el extremo de `activityId` solicitud.</span><span class="sxs-lookup"><span data-stu-id="c6394-122">To update an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span> <span data-ttu-id="c6394-123">Para completar este escenario, debe almacenar en caché el identificador de actividad devuelto por la llamada posterior original.</span><span class="sxs-lookup"><span data-stu-id="c6394-123">To complete this scenario, you must cache the activity ID returned by the original post call.</span></span>

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|<span data-ttu-id="c6394-124">Solicitud</span><span class="sxs-lookup"><span data-stu-id="c6394-124">Request</span></span> |<span data-ttu-id="c6394-125">Respuesta</span><span class="sxs-lookup"><span data-stu-id="c6394-125">Response</span></span> |
|----|----|
| <span data-ttu-id="c6394-126">Un [objeto Activity.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c6394-126">An [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) object.</span></span> | <span data-ttu-id="c6394-127">Un [objeto ResourceResponse.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c6394-127">A [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) object.</span></span> |

---
* * *

<span data-ttu-id="c6394-128">Ahora que ha actualizado los mensajes, actualice la tarjeta existente en la selección de botón para las actividades entrantes.</span><span class="sxs-lookup"><span data-stu-id="c6394-128">Now that you have updated messages, update the existing card on button selection for incoming activities.</span></span>

## <a name="update-cards"></a><span data-ttu-id="c6394-129">Actualizar tarjetas</span><span class="sxs-lookup"><span data-stu-id="c6394-129">Update cards</span></span>

<span data-ttu-id="c6394-130">Para actualizar la tarjeta existente en la selección de botón, puede usar `ReplyToId` la actividad entrante.</span><span class="sxs-lookup"><span data-stu-id="c6394-130">To update the existing card on button selection, you can use `ReplyToId` of incoming activity.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="c6394-131">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="c6394-131">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="c6394-132">Para actualizar la tarjeta existente en una selección de botón, pase un nuevo objeto con la tarjeta actualizada y como identificador de actividad `Activity` al método de la `ReplyToId` `UpdateActivityAsync` `TurnContext` clase.</span><span class="sxs-lookup"><span data-stu-id="c6394-132">To update existing card on a button selection, pass a new `Activity` object with updated card and `ReplyToId` as activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="c6394-133">Vea [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="c6394-133">See [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
var activity = MessageFactory.Attachment(card.ToAttachment());
activity.Id = turnContext.Activity.ReplyToId;
await turnContext.UpdateActivityAsync(activity, cancellationToken);
```

# <a name="typescript"></a>[<span data-ttu-id="c6394-134">TypeScript</span><span class="sxs-lookup"><span data-stu-id="c6394-134">TypeScript</span></span>](#tab/typescript)

<span data-ttu-id="c6394-135">Para actualizar la tarjeta existente en una selección de botón, pase un nuevo objeto con la tarjeta actualizada y como identificador de actividad `Activity` `replyToId` al método del `updateActivity` `TurnContext` objeto.</span><span class="sxs-lookup"><span data-stu-id="c6394-135">To update existing card on a button selection, pass a new `Activity` object with updated card and `replyToId` as activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="c6394-136">Vea [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="c6394-136">See [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span></span>

```typescript
const message = MessageFactory.attachment(card);
message.id = context.activity.replyToId;
await context.updateActivity(message);
```

# <a name="python"></a>[<span data-ttu-id="c6394-137">Python</span><span class="sxs-lookup"><span data-stu-id="c6394-137">Python</span></span>](#tab/python)

<span data-ttu-id="c6394-138">Para actualizar la tarjeta existente en un clic de botón, pase un nuevo objeto con la tarjeta actualizada y como identificador de actividad `Activity` al método de la `reply_to_id` `update_activity` `TurnContext` clase.</span><span class="sxs-lookup"><span data-stu-id="c6394-138">To update existing card on a button click, pass a new `Activity` object with updated card and `reply_to_id` as activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="c6394-139">Vea [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="c6394-139">See [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).</span></span>

```python
updated_activity = MessageFactory.attachment(CardFactory.hero_card(card))
updated_activity.id = turn_context.activity.reply_to_id
await turn_context.update_activity(updated_activity)
```

# <a name="rest-api"></a>[<span data-ttu-id="c6394-140">API de REST</span><span class="sxs-lookup"><span data-stu-id="c6394-140">REST API</span></span>](#tab/rest)

> [!NOTE]
> <span data-ttu-id="c6394-141">Puede desarrollar aplicaciones Teams en cualquier tecnología de programación web y llamar directamente a las API rest del servicio [de conector de bot.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c6394-141">You can develop Teams apps in any web programming technology and directly call the [bot connector service REST APIs](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span> <span data-ttu-id="c6394-142">Para ello, debe implementar procedimientos de seguridad [de](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) autenticación con las solicitudes DE API.</span><span class="sxs-lookup"><span data-stu-id="c6394-142">To do this, you must implement [authentication](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) security procedures with your API requests.</span></span>

<span data-ttu-id="c6394-143">Para actualizar una actividad existente dentro de una conversación, incluya y `conversationId` en el extremo de `activityId` solicitud.</span><span class="sxs-lookup"><span data-stu-id="c6394-143">To update an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span> <span data-ttu-id="c6394-144">Para completar este escenario, debe almacenar en caché el identificador de actividad devuelto por la llamada posterior original.</span><span class="sxs-lookup"><span data-stu-id="c6394-144">To complete this scenario, you must cache the activity ID returned by the original post call.</span></span>

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|<span data-ttu-id="c6394-145">Solicitud</span><span class="sxs-lookup"><span data-stu-id="c6394-145">Request</span></span> |<span data-ttu-id="c6394-146">Respuesta</span><span class="sxs-lookup"><span data-stu-id="c6394-146">Response</span></span> |
|----|----|
| <span data-ttu-id="c6394-147">Un [objeto activity.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c6394-147">An [activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) object.</span></span> | <span data-ttu-id="c6394-148">Un [objeto ResourceResponse.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c6394-148">A [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) object.</span></span> |

* * *

<span data-ttu-id="c6394-149">Ahora que ha actualizado las tarjetas, puede eliminar mensajes con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="c6394-149">Now that you have updated cards, you can delete messages using the Bot Framework.</span></span>

## <a name="delete-messages"></a><span data-ttu-id="c6394-150">Eliminar mensajes</span><span class="sxs-lookup"><span data-stu-id="c6394-150">Delete messages</span></span>

<span data-ttu-id="c6394-151">En Bot Framework, cada mensaje tiene su identificador de actividad único.</span><span class="sxs-lookup"><span data-stu-id="c6394-151">In the Bot Framework, every message has its unique activity identifier.</span></span> <span data-ttu-id="c6394-152">Los mensajes se pueden eliminar mediante el método de Bot `DeleteActivity` Framework.</span><span class="sxs-lookup"><span data-stu-id="c6394-152">Messages can be deleted using the Bot Framework's `DeleteActivity` method.</span></span>

# <a name="c"></a>[<span data-ttu-id="c6394-153">C#</span><span class="sxs-lookup"><span data-stu-id="c6394-153">C#</span></span>](#tab/dotnet)

<span data-ttu-id="c6394-154">Para eliminar un mensaje, pase el identificador de esa actividad al `DeleteActivityAsync` método de la `TurnContext` clase.</span><span class="sxs-lookup"><span data-stu-id="c6394-154">To delete a message, pass that activity's ID to the `DeleteActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="c6394-155">Para obtener más información, [consulta TurnContext.DeleteActivityAsync (método).](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c6394-155">For more information, see [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="c6394-156">TypeScript</span><span class="sxs-lookup"><span data-stu-id="c6394-156">TypeScript</span></span>](#tab/typescript)

<span data-ttu-id="c6394-157">Para eliminar un mensaje, pase el identificador de esa actividad al `deleteActivity` método del `TurnContext` objeto.</span><span class="sxs-lookup"><span data-stu-id="c6394-157">To delete a message, pass that activity's ID to the `deleteActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="c6394-158">Para obtener más información, [vea deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="c6394-158">For more information, see [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true).</span></span>

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[<span data-ttu-id="c6394-159">Python</span><span class="sxs-lookup"><span data-stu-id="c6394-159">Python</span></span>](#tab/python)

<span data-ttu-id="c6394-160">Para eliminar ese mensaje, pase el identificador de esa actividad al `delete_activity` método del `TurnContext` objeto.</span><span class="sxs-lookup"><span data-stu-id="c6394-160">To delete that message, pass that activity's ID to the `delete_activity` method of the `TurnContext` object.</span></span> <span data-ttu-id="c6394-161">Para obtener más información, [vea activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span><span class="sxs-lookup"><span data-stu-id="c6394-161">For more information, see [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span></span>

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[<span data-ttu-id="c6394-162">API de REST</span><span class="sxs-lookup"><span data-stu-id="c6394-162">REST API</span></span>](#tab/rest)

<span data-ttu-id="c6394-163">Para eliminar una actividad existente dentro de una conversación, incluya y `conversationId` en el extremo de `activityId` solicitud.</span><span class="sxs-lookup"><span data-stu-id="c6394-163">To delete an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span>

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| <span data-ttu-id="c6394-164">**Solicitud y respuesta**</span><span class="sxs-lookup"><span data-stu-id="c6394-164">**Request and response**</span></span> | <span data-ttu-id="c6394-165">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="c6394-165">**Description**</span></span> |
|----|----|
| <span data-ttu-id="c6394-166">N/D</span><span class="sxs-lookup"><span data-stu-id="c6394-166">N/A</span></span> | <span data-ttu-id="c6394-167">Un código de estado HTTP que indica el resultado de la operación.</span><span class="sxs-lookup"><span data-stu-id="c6394-167">An HTTP status code indicating the outcome of the operation.</span></span> <span data-ttu-id="c6394-168">No se especifica nada en el cuerpo de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="c6394-168">Nothing is specified in the body of the response.</span></span> |

---

## <a name="code-sample"></a><span data-ttu-id="c6394-169">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="c6394-169">Code sample</span></span>

<span data-ttu-id="c6394-170">En el ejemplo de código siguiente se muestran los conceptos básicos de las conversaciones:</span><span class="sxs-lookup"><span data-stu-id="c6394-170">The following code sample demonstrates basics of conversations:</span></span>

| <span data-ttu-id="c6394-171">**Nombre de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="c6394-171">**Sample name**</span></span> | <span data-ttu-id="c6394-172">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="c6394-172">**Description**</span></span> | <span data-ttu-id="c6394-173">**.NET**</span><span class="sxs-lookup"><span data-stu-id="c6394-173">**.NET**</span></span> | <span data-ttu-id="c6394-174">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="c6394-174">**Node.js**</span></span> | <span data-ttu-id="c6394-175">**Python**</span><span class="sxs-lookup"><span data-stu-id="c6394-175">**Python**</span></span> |
|----------------------|-----------------|--------|-------------|--------|
| <span data-ttu-id="c6394-176">Teams Conceptos básicos de conversación</span><span class="sxs-lookup"><span data-stu-id="c6394-176">Teams Conversation Basics</span></span>  | <span data-ttu-id="c6394-177">Muestra los conceptos básicos de las conversaciones en Teams actualización y eliminación de mensajes.</span><span class="sxs-lookup"><span data-stu-id="c6394-177">Demonstrates basics of conversations in Teams including message update and delete.</span></span> | [<span data-ttu-id="c6394-178">View</span><span class="sxs-lookup"><span data-stu-id="c6394-178">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [<span data-ttu-id="c6394-179">View</span><span class="sxs-lookup"><span data-stu-id="c6394-179">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="c6394-180">View</span><span class="sxs-lookup"><span data-stu-id="c6394-180">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a><span data-ttu-id="c6394-181">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="c6394-181">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c6394-182">Obtener Teams contexto</span><span class="sxs-lookup"><span data-stu-id="c6394-182">Get Teams context</span></span>](~/bots/how-to/get-teams-context.md)

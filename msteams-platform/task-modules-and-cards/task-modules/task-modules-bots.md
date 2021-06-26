---
title: Usar módulos de tareas en Microsoft Teams bots
description: Cómo usar módulos de tareas con Microsoft Teams bots, incluidas las tarjetas de Bot Framework, las tarjetas adaptables y los vínculos profundos.
localization_priority: Normal
ms.topic: how-to
keywords: bots de equipos de módulos de tareas
ms.openlocfilehash: 5d9aa2b651a4c99cee75aada62a4d1176a589d79
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140313"
---
# <a name="use-task-modules-from-bots"></a><span data-ttu-id="a82a9-104">Usar módulos de tareas desde bots</span><span class="sxs-lookup"><span data-stu-id="a82a9-104">Use task modules from bots</span></span>

<span data-ttu-id="a82a9-105">Los módulos de tareas se pueden invocar desde bots Microsoft Teams mediante botones en tarjetas adaptables y tarjetas de Marco de bots que son hero, thumbnail y Office 365 Connector.</span><span class="sxs-lookup"><span data-stu-id="a82a9-105">Task modules can be invoked from Microsoft Teams bots using buttons on Adaptive Cards and Bot Framework cards that is hero, thumbnail, and Office 365 Connector.</span></span> <span data-ttu-id="a82a9-106">Los módulos de tareas suelen ser una mejor experiencia de usuario que varios pasos de conversación.</span><span class="sxs-lookup"><span data-stu-id="a82a9-106">Task modules are often a better user experience than multiple conversation steps.</span></span> <span data-ttu-id="a82a9-107">Realice un seguimiento del estado del bot y permita al usuario interrumpir o cancelar la secuencia.</span><span class="sxs-lookup"><span data-stu-id="a82a9-107">Keep track of bot state and allow the user to interrupt or cancel the sequence.</span></span>

<span data-ttu-id="a82a9-108">Hay dos formas de invocar módulos de tareas:</span><span class="sxs-lookup"><span data-stu-id="a82a9-108">There are two ways of invoking task modules:</span></span>

* <span data-ttu-id="a82a9-109">Un nuevo tipo de mensaje de invocación: el uso de la acción de tarjeta para las tarjetas de Bot Framework o la acción de tarjeta para tarjetas adaptables, con , módulo de tarea, ya sea una dirección URL o una tarjeta adaptable, se captura dinámicamente desde `task/fetch` `invoke` [](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) `Action.Submit` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) `task/fetch` el bot.</span><span class="sxs-lookup"><span data-stu-id="a82a9-109">A new kind of invoke message `task/fetch`: Using the `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) for Bot Framework cards, or the `Action.Submit` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, with `task/fetch`, task module either a URL or an Adaptive Card, is fetched dynamically from your bot.</span></span>
* <span data-ttu-id="a82a9-110">Direcciones URL de vínculo profundo: mediante la sintaxis de vínculo profundo para módulos de [tareas,](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)puede usar la acción de tarjeta para tarjetas bot Framework o la acción de tarjeta para tarjetas `openUrl` [](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl) `Action.OpenUrl` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) adaptables, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="a82a9-110">Deep link URLs: Using the [deep link syntax for task modules](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax), you can use the `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl) for Bot Framework cards or the `Action.OpenUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive Cards, respectively.</span></span> <span data-ttu-id="a82a9-111">Con las direcciones URL de vínculo profundo, ya se sabe que la dirección URL del módulo de tareas o el cuerpo de la tarjeta adaptable evitan un recorrido de ida y vuelta del servidor con relación a `task/fetch` .</span><span class="sxs-lookup"><span data-stu-id="a82a9-111">With deep link URLs, the task module URL or Adaptive Card body is already known to avoid a server round-trip relative to `task/fetch`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a82a9-112">Cada `url` uno y debe implementar el protocolo de cifrado `fallbackUrl` HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a82a9-112">Each `url` and `fallbackUrl` must implement the HTTPS encryption protocol.</span></span>

<span data-ttu-id="a82a9-113">En la siguiente sección se proporcionan detalles sobre cómo invocar un módulo de tareas mediante `task/fetch` .</span><span class="sxs-lookup"><span data-stu-id="a82a9-113">The next section provides details on invoking a task module using `task/fetch`.</span></span>

## <a name="invoke-a-task-module-using-taskfetch"></a><span data-ttu-id="a82a9-114">Invocar un módulo de tareas mediante task/fetch</span><span class="sxs-lookup"><span data-stu-id="a82a9-114">Invoke a task module using task/fetch</span></span>

<span data-ttu-id="a82a9-115">Cuando el objeto de la acción de tarjeta o se inicializa y cuando un usuario selecciona el botón, se envía un mensaje `value` `invoke` al `Action.Submit` `invoke` bot.</span><span class="sxs-lookup"><span data-stu-id="a82a9-115">When the `value` object of the `invoke` card action or `Action.Submit` is initialized and when a user selects the button, an `invoke` message is sent to the bot.</span></span> <span data-ttu-id="a82a9-116">En la respuesta HTTP al mensaje, hay un objeto TaskInfo incrustado en un objeto contenedor, que Teams `invoke` usa para mostrar el módulo de tareas. [](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)</span><span class="sxs-lookup"><span data-stu-id="a82a9-116">In the HTTP response to the `invoke` message, there is a [TaskInfo object](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) embedded in a wrapper object, which Teams uses to display the task module.</span></span>

![solicitud o respuesta task/fetch](~/assets/images/task-module/task-module-invoke-request-response.png)

<span data-ttu-id="a82a9-118">Los pasos siguientes proporcionan el módulo de tareas de invocación mediante task/fetch:</span><span class="sxs-lookup"><span data-stu-id="a82a9-118">The following steps provides the invoke task module using task/fetch:</span></span>

1. <span data-ttu-id="a82a9-119">Esta imagen muestra una tarjeta principal de Bot Framework con una **acción Comprar** `invoke` [tarjeta](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke).</span><span class="sxs-lookup"><span data-stu-id="a82a9-119">This image shows a Bot Framework hero card with a **Buy** `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke).</span></span> <span data-ttu-id="a82a9-120">El valor de la `type` propiedad es y el resto del objeto puede ser de su `task/fetch` `value` elección.</span><span class="sxs-lookup"><span data-stu-id="a82a9-120">The value of the `type` property is `task/fetch` and the rest of the `value` object can be of your choice.</span></span>
1. <span data-ttu-id="a82a9-121">El bot recibe el `invoke` mensaje HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="a82a9-121">The bot receives the `invoke` HTTP POST message.</span></span>
1. <span data-ttu-id="a82a9-122">El bot crea un objeto de respuesta y lo devuelve en el cuerpo de la respuesta POST con un código de respuesta HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="a82a9-122">The bot creates a response object and returns it in the body of the POST response with an HTTP 200 response code.</span></span> <span data-ttu-id="a82a9-123">Para obtener más información sobre el esquema de respuestas, vea [la discusión sobre la tarea/enviar](#the-flexibility-of-tasksubmit).</span><span class="sxs-lookup"><span data-stu-id="a82a9-123">For more information on schema for responses, see [the discussion on task/submit](#the-flexibility-of-tasksubmit).</span></span> <span data-ttu-id="a82a9-124">El siguiente código proporciona un ejemplo de cuerpo de la respuesta HTTP que contiene un [objeto TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) incrustado en un objeto contenedor:</span><span class="sxs-lookup"><span data-stu-id="a82a9-124">The following code provides an example of body of the HTTP response that contains a [TaskInfo object](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) embedded in a wrapper object:</span></span>

    ```json
    {
      "task": {
        "type": "continue",
        "value": {
          "title": "Task module title",
          "height": 500,
          "width": "medium",
          "url": "https://contoso.com/msteams/taskmodules/newcustomer",
          "fallbackUrl": "https://contoso.com/msteams/taskmodules/newcustomer"
        }
      }
    }
    ```

    <span data-ttu-id="a82a9-125">El `task/fetch` evento y su respuesta para bots es similar a la función del SDK de `microsoftTeams.tasks.startTask()` cliente.</span><span class="sxs-lookup"><span data-stu-id="a82a9-125">The `task/fetch` event and its response for bots is similar to the `microsoftTeams.tasks.startTask()` function in the client SDK.</span></span>

1. <span data-ttu-id="a82a9-126">Microsoft Teams muestra el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="a82a9-126">Microsoft Teams displays the task module.</span></span>

<span data-ttu-id="a82a9-127">En la siguiente sección se proporcionan detalles sobre cómo enviar el resultado de un módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="a82a9-127">The next section provides details on submitting the result of a task module.</span></span>

## <a name="submit-the-result-of-a-task-module"></a><span data-ttu-id="a82a9-128">Enviar el resultado de un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="a82a9-128">Submit the result of a task module</span></span>

<span data-ttu-id="a82a9-129">Cuando el usuario ha terminado con el módulo de tareas, enviar el resultado de vuelta al bot es similar a la forma en que funciona con las pestañas.</span><span class="sxs-lookup"><span data-stu-id="a82a9-129">When the user is finished with the task module, submitting the result back to the bot is similar to the way it works with tabs.</span></span> <span data-ttu-id="a82a9-130">Para obtener más información, [vea el ejemplo de envío del resultado de un módulo de tareas](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module).</span><span class="sxs-lookup"><span data-stu-id="a82a9-130">For more information, see [example of submitting the result of a task module](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module).</span></span> <span data-ttu-id="a82a9-131">Hay algunas diferencias como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="a82a9-131">There are a few differences as follows:</span></span>

* <span data-ttu-id="a82a9-132">HTML o JavaScript es decir: una vez validado lo que el usuario ha escrito, se llama a la función SDK a la que se hace referencia a continuación con fines `TaskInfo.url` `microsoftTeams.tasks.submitTask()` de `submitTask()` legibilidad.</span><span class="sxs-lookup"><span data-stu-id="a82a9-132">HTML or JavaScript that is `TaskInfo.url`: Once you have validated what the user has entered, you call the `microsoftTeams.tasks.submitTask()` SDK function referred to hereafter as `submitTask()` for readability purposes.</span></span> <span data-ttu-id="a82a9-133">Puede llamar sin ningún parámetro si desea Teams cerrar el módulo de tareas, pero debe pasar un objeto o una cadena `submitTask()` a su `submitHandler` .</span><span class="sxs-lookup"><span data-stu-id="a82a9-133">You can call `submitTask()` without any parameters if you want Teams to close the task module, but you must pass an object or a string to your `submitHandler`.</span></span> <span data-ttu-id="a82a9-134">Pásalo como primer parámetro, `result` .</span><span class="sxs-lookup"><span data-stu-id="a82a9-134">Pass it as the first parameter, `result`.</span></span> <span data-ttu-id="a82a9-135">Teams invoca , `submitHandler` `err` es `null` y `result` es el objeto o cadena que se pasó a `submitTask()` .</span><span class="sxs-lookup"><span data-stu-id="a82a9-135">Teams invokes `submitHandler`, `err` is `null`, and `result` is the object or string you passed to `submitTask()`.</span></span> <span data-ttu-id="a82a9-136">Si llama `submitTask()` con un `result` parámetro, debe pasar una o una `appId` matriz de `appId` cadenas.</span><span class="sxs-lookup"><span data-stu-id="a82a9-136">If you call `submitTask()` with a `result` parameter, you must pass an `appId` or an array of `appId` strings.</span></span> <span data-ttu-id="a82a9-137">Esto permite Teams validar que la aplicación que envía el resultado es la misma que invocó el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="a82a9-137">This allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span> <span data-ttu-id="a82a9-138">El bot recibe un `task/submit` mensaje que incluye `result` .</span><span class="sxs-lookup"><span data-stu-id="a82a9-138">Your bot receives a `task/submit` message including `result`.</span></span> <span data-ttu-id="a82a9-139">Para obtener más información, vea [payload of `task/fetch` y `task/submit` messages](#payload-of-taskfetch-and-tasksubmit-messages).</span><span class="sxs-lookup"><span data-stu-id="a82a9-139">For more information, see [payload of `task/fetch` and `task/submit` messages](#payload-of-taskfetch-and-tasksubmit-messages).</span></span>
* <span data-ttu-id="a82a9-140">Tarjeta adaptable que es: el cuerpo de la tarjeta adaptable tal como lo rellena el usuario se envía al bot a través de un mensaje cuando el usuario `TaskInfo.card` `task/submit` selecciona cualquier `Action.Submit` botón.</span><span class="sxs-lookup"><span data-stu-id="a82a9-140">Adaptive Card that is `TaskInfo.card`: The Adaptive Card body as filled in by the user is sent to the bot through a `task/submit` message when the user selects any `Action.Submit` button.</span></span>

<span data-ttu-id="a82a9-141">En la siguiente sección se proporcionan detalles sobre la flexibilidad de `task/submit` .</span><span class="sxs-lookup"><span data-stu-id="a82a9-141">The next section provides details on the flexibility of `task/submit`.</span></span>

## <a name="the-flexibility-of-tasksubmit"></a><span data-ttu-id="a82a9-142">Flexibilidad de tarea/envío</span><span class="sxs-lookup"><span data-stu-id="a82a9-142">The flexibility of task/submit</span></span>

<span data-ttu-id="a82a9-143">Cuando el usuario termina con un módulo de tareas invocado desde un bot, el bot siempre recibe un `task/submit invoke` mensaje.</span><span class="sxs-lookup"><span data-stu-id="a82a9-143">When the user finishes with a task module invoked from a bot, the bot always receives a `task/submit invoke` message.</span></span> <span data-ttu-id="a82a9-144">Tiene varias opciones al responder al `task/submit` mensaje de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="a82a9-144">You have several options when responding to the `task/submit` message as follows:</span></span>

| <span data-ttu-id="a82a9-145">Respuesta del cuerpo HTTP</span><span class="sxs-lookup"><span data-stu-id="a82a9-145">HTTP body response</span></span>                      | <span data-ttu-id="a82a9-146">Escenario</span><span class="sxs-lookup"><span data-stu-id="a82a9-146">Scenario</span></span>                                |
| --------------------------------------- | --------------------------------------- |
| <span data-ttu-id="a82a9-147">Ninguno omite el `task/submit` mensaje</span><span class="sxs-lookup"><span data-stu-id="a82a9-147">None ignore the `task/submit` message</span></span> | <span data-ttu-id="a82a9-148">La respuesta más sencilla no es ninguna respuesta.</span><span class="sxs-lookup"><span data-stu-id="a82a9-148">The simplest response is no response at all.</span></span> <span data-ttu-id="a82a9-149">No es necesario que el bot responda cuando el usuario haya terminado con el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="a82a9-149">Your bot is not required to respond when the user is finished with the task module.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | <span data-ttu-id="a82a9-150">Teams muestra el valor de `value` en un cuadro de mensaje emergente.</span><span class="sxs-lookup"><span data-stu-id="a82a9-150">Teams displays the value of `value` in a pop-up message box.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | <span data-ttu-id="a82a9-151">Permite encadenar secuencias de tarjetas adaptables juntas en una experiencia de asistente o de varios pasos.</span><span class="sxs-lookup"><span data-stu-id="a82a9-151">Allows you to chain sequences of Adaptive Cards together in a wizard or multi-step experience.</span></span> |

> [!NOTE]
> <span data-ttu-id="a82a9-152">Encadenar tarjetas adaptables en una secuencia es un escenario avanzado.</span><span class="sxs-lookup"><span data-stu-id="a82a9-152">Chaining Adaptive Cards into a sequence is an advanced scenario.</span></span> <span data-ttu-id="a82a9-153">La Node.js de ejemplo lo admite.</span><span class="sxs-lookup"><span data-stu-id="a82a9-153">The Node.js sample app supports it.</span></span> <span data-ttu-id="a82a9-154">Para obtener más información, [vea Microsoft Teams módulo de tareas Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes).</span><span class="sxs-lookup"><span data-stu-id="a82a9-154">For more information, see [Microsoft Teams task module Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes).</span></span>

<span data-ttu-id="a82a9-155">En la siguiente sección se proporcionan detalles sobre la carga de `task/fetch` y `task/submit` los mensajes.</span><span class="sxs-lookup"><span data-stu-id="a82a9-155">The next section provides details on payload of `task/fetch` and `task/submit` messages.</span></span>

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a><span data-ttu-id="a82a9-156">Carga de los mensajes task/fetch y task/submit</span><span class="sxs-lookup"><span data-stu-id="a82a9-156">Payload of task/fetch and task/submit messages</span></span>

<span data-ttu-id="a82a9-157">En esta sección se define el esquema de lo que el bot recibe cuando recibe un `task/fetch` objeto `task/submit` o Bot `Activity` Framework.</span><span class="sxs-lookup"><span data-stu-id="a82a9-157">This section defines the schema of what your bot receives when it receives a `task/fetch` or `task/submit` Bot Framework `Activity` object.</span></span> <span data-ttu-id="a82a9-158">En la tabla siguiente se proporcionan las propiedades de carga de `task/fetch` y `task/submit` mensajes:</span><span class="sxs-lookup"><span data-stu-id="a82a9-158">The following table provides the properties of payload of `task/fetch` and `task/submit` messages:</span></span>

| <span data-ttu-id="a82a9-159">Propiedad</span><span class="sxs-lookup"><span data-stu-id="a82a9-159">Property</span></span> | <span data-ttu-id="a82a9-160">Descripción</span><span class="sxs-lookup"><span data-stu-id="a82a9-160">Description</span></span>                          |
| -------- | ------------------------------------ |
| `type`   | <span data-ttu-id="a82a9-161">Siempre es `invoke` .</span><span class="sxs-lookup"><span data-stu-id="a82a9-161">Is always `invoke`.</span></span>           |
| `name`   | <span data-ttu-id="a82a9-162">Es o `task/fetch` `task/submit` .</span><span class="sxs-lookup"><span data-stu-id="a82a9-162">Is either `task/fetch` or `task/submit`.</span></span> |
| `value`  | <span data-ttu-id="a82a9-163">Es la carga definida por el desarrollador.</span><span class="sxs-lookup"><span data-stu-id="a82a9-163">Is the developer-defined payload.</span></span> <span data-ttu-id="a82a9-164">La estructura del `value` objeto es la misma que la que se envía desde Teams.</span><span class="sxs-lookup"><span data-stu-id="a82a9-164">The structure of the `value` object is the same as what is sent from Teams.</span></span> <span data-ttu-id="a82a9-165">En este caso, sin embargo, es diferente.</span><span class="sxs-lookup"><span data-stu-id="a82a9-165">In this case, however, it is different.</span></span> <span data-ttu-id="a82a9-166">Requiere compatibilidad con la captura dinámica que es de Bot Framework, que `task/fetch` es y acciones de tarjeta `value` `Action.Submit` adaptable, que es `data` .</span><span class="sxs-lookup"><span data-stu-id="a82a9-166">It requires support for dynamic fetch that is `task/fetch` from both Bot Framework, which is `value` and Adaptive Card `Action.Submit` actions, which is `data`.</span></span> <span data-ttu-id="a82a9-167">Se requiere una forma de Teams al bot además de lo `context` que se incluye en o `value` `data` .</span><span class="sxs-lookup"><span data-stu-id="a82a9-167">A way to communicate Teams `context` to the bot is required in addition to what is included in `value` or `data`.</span></span><br/><br/><span data-ttu-id="a82a9-168">Combine "valor" y "datos" en un objeto primario:</span><span class="sxs-lookup"><span data-stu-id="a82a9-168">Combine 'value' and 'data' into a parent object:</span></span><br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

<span data-ttu-id="a82a9-169">La siguiente sección proporciona un ejemplo de recepción y respuesta a e `task/fetch` `task/submit` invocar mensajes en Node.js.</span><span class="sxs-lookup"><span data-stu-id="a82a9-169">The next section provides an example of receiving and responding to `task/fetch` and `task/submit` invoke messages in Node.js.</span></span>

## <a name="example-of-taskfetch-and-tasksubmit-invoke-messages-in-nodejs-and-c"></a><span data-ttu-id="a82a9-170">Ejemplo de task/fetch y task/submit invoke messages en Node.js y C #</span><span class="sxs-lookup"><span data-stu-id="a82a9-170">Example of task/fetch and task/submit invoke messages in Node.js and C#</span></span>

# <a name="nodejs"></a>[<span data-ttu-id="a82a9-171">Node.js</span><span class="sxs-lookup"><span data-stu-id="a82a9-171">Node.js</span></span>](#tab/nodejs)

```typescript
handleTeamsTaskModuleFetch(context, taskModuleRequest) {
    // Called when the user selects an options from the displayed HeroCard or
    // AdaptiveCard.  The result is the action to perform.

    const cardTaskFetchValue = taskModuleRequest.data.data;
    var taskInfo = {}; // TaskModuleTaskInfo

    if (cardTaskFetchValue === TaskModuleIds.YouTube) {
        // Display the YouTube.html page
        taskInfo.url = taskInfo.fallbackUrl = this.baseUrl + '/' + TaskModuleIds.YouTube + '.html';
        this.setTaskInfo(taskInfo, TaskModuleUIConstants.YouTube);
    } else if (cardTaskFetchValue === TaskModuleIds.CustomForm) {
        // Display the CustomForm.html page, and post the form data back via
        // handleTeamsTaskModuleSubmit.
        taskInfo.url = taskInfo.fallbackUrl = this.baseUrl + '/' + TaskModuleIds.CustomForm + '.html';
        this.setTaskInfo(taskInfo, TaskModuleUIConstants.CustomForm);
    } else if (cardTaskFetchValue === TaskModuleIds.AdaptiveCard) {
        // Display an AdaptiveCard to prompt user for text, and post it back via
        // handleTeamsTaskModuleSubmit.
        taskInfo.card = this.createAdaptiveCardAttachment();
        this.setTaskInfo(taskInfo, TaskModuleUIConstants.AdaptiveCard);
    }

    return TaskModuleResponseFactory.toTaskModuleResponse(taskInfo);
}

async handleTeamsTaskModuleSubmit(context, taskModuleRequest) {
    // Called when data is being returned from the selected option (see `handleTeamsTaskModuleFetch').

    // Echo the users input back.  In a production bot, this is where you'd add behavior in
    // response to the input.
    await context.sendActivity(MessageFactory.text('handleTeamsTaskModuleSubmit: ' + JSON.stringify(taskModuleRequest.data)));

    // Return TaskModuleResponse
    return {
        // TaskModuleMessageResponse
        task: {
            type: 'message',
            value: 'Thanks!'
        }
    };
}

setTaskInfo(taskInfo, uiSettings) {
    taskInfo.height = uiSettings.height;
    taskInfo.width = uiSettings.width;
    taskInfo.title = uiSettings.title;
}
```

# <a name="c"></a>[<span data-ttu-id="a82a9-172">C#</span><span class="sxs-lookup"><span data-stu-id="a82a9-172">C#</span></span>](#tab/csharp)

```csharp
protected override Task<TaskModuleResponse> OnTeamsTaskModuleFetchAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
{
    var asJobject = JObject.FromObject(taskModuleRequest.Data);
    var value = asJobject.ToObject<CardTaskFetchValue<string>>()?.Data;

    var taskInfo = new TaskModuleTaskInfo();
    switch (value)
    {
        case TaskModuleIds.YouTube:
            taskInfo.Url = taskInfo.FallbackUrl = _baseUrl + "/" + TaskModuleIds.YouTube;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.YouTube);
            break;
        case TaskModuleIds.CustomForm:
            taskInfo.Url = taskInfo.FallbackUrl = _baseUrl + "/" + TaskModuleIds.CustomForm;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.CustomForm);
            break;
        case TaskModuleIds.AdaptiveCard:
            taskInfo.Card = CreateAdaptiveCardAttachment();
            SetTaskInfo(taskInfo, TaskModuleUIConstants.AdaptiveCard);
            break;
        default:
            break;
    }

    return Task.FromResult(taskInfo.ToTaskModuleResponse());
}

protected override async Task<TaskModuleResponse> OnTeamsTaskModuleSubmitAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
{
    var reply = MessageFactory.Text("OnTeamsTaskModuleSubmitAsync Value: " + JsonConvert.SerializeObject(taskModuleRequest));
    await turnContext.SendActivityAsync(reply, cancellationToken);

    return TaskModuleResponseFactory.CreateResponse("Thanks!");
}

private static void SetTaskInfo(TaskModuleTaskInfo taskInfo, UISettings uIConstants)
{
    taskInfo.Height = uIConstants.Height;
    taskInfo.Width = uIConstants.Width;
    taskInfo.Title = uIConstants.Title.ToString();
}
```

---

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a><span data-ttu-id="a82a9-173">Acciones de tarjeta de Bot Framework frente a acciones Adaptive Card Action.Submit</span><span class="sxs-lookup"><span data-stu-id="a82a9-173">Bot Framework card actions vs. Adaptive Card Action.Submit actions</span></span>

<span data-ttu-id="a82a9-174">El esquema de las acciones de tarjeta de Bot Framework es diferente de las acciones de tarjeta adaptable y la forma de invocar `Action.Submit` módulos de tareas también es diferente.</span><span class="sxs-lookup"><span data-stu-id="a82a9-174">The schema for Bot Framework card actions is different from Adaptive Card `Action.Submit` actions and the way to invoke task modules is also different.</span></span> <span data-ttu-id="a82a9-175">El `data` objeto de contiene un objeto para que no `Action.Submit` `msteams` interfiera con otras propiedades de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="a82a9-175">The `data` object in `Action.Submit` contains an `msteams` object so it does not interfere with other properties in the card.</span></span> <span data-ttu-id="a82a9-176">En la tabla siguiente se muestra un ejemplo de cada acción de tarjeta:</span><span class="sxs-lookup"><span data-stu-id="a82a9-176">The following table shows an example of each card action:</span></span>

| <span data-ttu-id="a82a9-177">Acción de tarjeta de Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a82a9-177">Bot Framework card action</span></span>                              | <span data-ttu-id="a82a9-178">Acción Adaptive Card Action.Submit</span><span class="sxs-lookup"><span data-stu-id="a82a9-178">Adaptive Card Action.Submit action</span></span>                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="code-sample"></a><span data-ttu-id="a82a9-179">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="a82a9-179">Code sample</span></span>

|<span data-ttu-id="a82a9-180">Nombre de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a82a9-180">Sample name</span></span> | <span data-ttu-id="a82a9-181">Descripción</span><span class="sxs-lookup"><span data-stu-id="a82a9-181">Description</span></span> | <span data-ttu-id="a82a9-182">.NET</span><span class="sxs-lookup"><span data-stu-id="a82a9-182">.NET</span></span> | <span data-ttu-id="a82a9-183">Node.js</span><span class="sxs-lookup"><span data-stu-id="a82a9-183">Node.js</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="a82a9-184">Bots de ejemplo de módulo de tareas-V4</span><span class="sxs-lookup"><span data-stu-id="a82a9-184">Task module sample bots-V4</span></span> | <span data-ttu-id="a82a9-185">Ejemplos para crear módulos de tareas.</span><span class="sxs-lookup"><span data-stu-id="a82a9-185">Samples for creating task modules.</span></span> |[<span data-ttu-id="a82a9-186">View</span><span class="sxs-lookup"><span data-stu-id="a82a9-186">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[<span data-ttu-id="a82a9-187">View</span><span class="sxs-lookup"><span data-stu-id="a82a9-187">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="see-also"></a><span data-ttu-id="a82a9-188">Vea también</span><span class="sxs-lookup"><span data-stu-id="a82a9-188">See also</span></span>

* [<span data-ttu-id="a82a9-189">Microsoft Teams ejemplo de módulo de tareas en Node.js</span><span class="sxs-lookup"><span data-stu-id="a82a9-189">Microsoft Teams task module sample code in Node.js</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [<span data-ttu-id="a82a9-190">Ejemplos de Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a82a9-190">Bot Framework samples</span></span>](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)

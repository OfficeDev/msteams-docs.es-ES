---
title: Uso de módulos de tareas en bots de Microsoft Teams
description: Cómo usar los módulos de tareas con los bots de Microsoft Teams, incluidas las tarjetas de Framework de bot, las tarjetas adaptables y los vínculos profundos.
keywords: módulos de tareas bots de Teams
ms.openlocfilehash: 09b0ede85c613d5724c6ecddbccd2a59c43cad74
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228097"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a><span data-ttu-id="fecc7-104">Uso de módulos de tareas de bots de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="fecc7-104">Using task modules from Microsoft Teams bots</span></span>

<span data-ttu-id="fecc7-105">Los módulos de tareas se pueden invocar desde bots de Microsoft Teams con botones en tarjetas adaptables y tarjetas de entorno de Bot? (Hero, thumbnail y Office 365 Connector).</span><span class="sxs-lookup"><span data-stu-id="fecc7-105">Task modules can be invoked from Microsoft Teams bots using buttons on Adaptive cards and Bot Framework cards (Hero, Thumbnail, and Office 365 Connector).</span></span> <span data-ttu-id="fecc7-106">Los módulos de tareas suelen ser una mejor experiencia de usuario que varios pasos de conversación en los que, como desarrollador, tiene que realizar un seguimiento del estado de los robots y permitir al usuario interrumpir/cancelar la secuencia.</span><span class="sxs-lookup"><span data-stu-id="fecc7-106">Task modules are often a better user experience than multiple conversation steps where you as a developer have to keep track of bot state and allow the user to interrupt/cancel the sequence.</span></span>

<span data-ttu-id="fecc7-107">Hay dos formas de invocar módulos de tareas:</span><span class="sxs-lookup"><span data-stu-id="fecc7-107">There are two ways of invoking task modules:</span></span>

* <span data-ttu-id="fecc7-108">**Un nuevo tipo de mensaje `task/fetch`de invocación.**</span><span class="sxs-lookup"><span data-stu-id="fecc7-108">**A new kind of invoke message `task/fetch`.**</span></span> <span data-ttu-id="fecc7-109">Mediante la `invoke` [acción de tarjeta](~/task-modules-and-cards/cards/cards-actions.md#invoke) de las tarjetas de .NET Framework `Action.Submit` o la [acción de tarjeta](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) para tarjetas `task/fetch`adaptables, con, el módulo de tareas (ya sea una dirección URL o una tarjeta adaptable) se obtiene dinámicamente desde el bot.</span><span class="sxs-lookup"><span data-stu-id="fecc7-109">Using the `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke) for Bot Framework cards, or the `Action.Submit` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, with `task/fetch`, the task module (either a URL or an Adaptive card) is fetched dynamically from your bot.</span></span>
* <span data-ttu-id="fecc7-110">**Direcciones URL de vínculo en profundidad.**</span><span class="sxs-lookup"><span data-stu-id="fecc7-110">**Deep link URLs.**</span></span> <span data-ttu-id="fecc7-111">Mediante la [Sintaxis de vínculo profundo para módulos de tareas](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax), puede usar `openUrl` la [acción de tarjeta](~/task-modules-and-cards/cards/cards-actions.md#openurl) para las tarjetas de `Action.OpenUrl` bot Framework o la acción de la [tarjeta](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) para tarjetas adaptables, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="fecc7-111">Using the [deep link syntax for task modules](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax), you can use the `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#openurl) for Bot Framework cards or the `Action.OpenUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, respectively.</span></span> <span data-ttu-id="fecc7-112">Con las direcciones URL de vínculo en profundidad, la dirección URL del módulo de tareas o el cuerpo de la tarjeta adaptable se conoce obviamente `task/fetch`de antemano, evitando un viaje de ida y vuelta en el servidor con respecto a.</span><span class="sxs-lookup"><span data-stu-id="fecc7-112">With deep link URLs, the task module URL or Adaptive card body is obviously known in advance, avoiding a server round-trip relative to `task/fetch`.</span></span>

## <a name="invoking-a-task-module-via-taskfetch"></a><span data-ttu-id="fecc7-113">Invocación de un módulo de tareas a través de la tarea/obtención</span><span class="sxs-lookup"><span data-stu-id="fecc7-113">Invoking a task module via task/fetch</span></span>

<span data-ttu-id="fecc7-114">Cuando el `value` objeto de la `invoke` acción de la `Action.Submit` tarjeta o se inicializa de la manera adecuada (explicado con más detalle a continuación), cuando un usuario presiona `invoke` el botón, se envía un mensaje al bot.</span><span class="sxs-lookup"><span data-stu-id="fecc7-114">When the `value` object of the `invoke` card action or `Action.Submit` is initialized in the proper way (explained in more detail below), when a user presses the button an `invoke` message is sent to the bot.</span></span> <span data-ttu-id="fecc7-115">En la respuesta HTTP al `invoke` mensaje, hay un [objeto TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) incrustado en un objeto contenedor, que Microsoft Teams usa para mostrar el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="fecc7-115">In the HTTP response to the `invoke` message, there's a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, which Teams uses to display the task module.</span></span>

![solicitud y respuesta de la tarea/obtención](~/assets/images/task-module/task-module-invoke-request-response.png)

<span data-ttu-id="fecc7-117">Echemos un vistazo a cada paso con un poco más de detalle:</span><span class="sxs-lookup"><span data-stu-id="fecc7-117">Let's look at each step in a bit more detail:</span></span>

1. <span data-ttu-id="fecc7-118">En este ejemplo se muestra una tarjeta Hero Framework Hero con una `invoke` [acción de tarjeta](~/task-modules-and-cards/cards/cards-actions.md#invoke)"Buy".</span><span class="sxs-lookup"><span data-stu-id="fecc7-118">This example shows a Bot Framework Hero card with a "Buy" `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke).</span></span> <span data-ttu-id="fecc7-119">El valor de la `type` propiedad es `task/fetch` : el resto del `value` objeto puede ser cualquier cosa que desee.</span><span class="sxs-lookup"><span data-stu-id="fecc7-119">The value of the `type` property is `task/fetch` - the rest of the `value` object can be whatever you like.</span></span>
2. <span data-ttu-id="fecc7-120">El bot recibe el `invoke` mensaje http post.</span><span class="sxs-lookup"><span data-stu-id="fecc7-120">The bot receives the `invoke` HTTP POST message.</span></span>
3. <span data-ttu-id="fecc7-121">El bot crea un objeto de respuesta y lo devuelve en el cuerpo de la respuesta POST con un código de respuesta HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="fecc7-121">The bot creates a response object and returns it in the body of the POST response with an HTTP 200 response code.</span></span> <span data-ttu-id="fecc7-122">El esquema de respuestas se describe [a continuación en la discusión sobre la tarea o el envío](#the-flexibility-of-tasksubmit), pero lo importante que debe recordar ahora es que el cuerpo de la respuesta http contiene un [objeto TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) incrustado en un objeto contenedor, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fecc7-122">The schema for responses is described [below in the discussion on task/submit](#the-flexibility-of-tasksubmit), but the important thing to remember now is that the body of the HTTP response contains a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, e.g.:</span></span>

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
    
    <span data-ttu-id="fecc7-123">El `task/fetch` evento y su respuesta para bots son similares, conceptualmente, a la `microsoftTeams.tasks.startTask()` función en el SDK del cliente.</span><span class="sxs-lookup"><span data-stu-id="fecc7-123">The `task/fetch` event and its response for bots is similar, conceptually, to the `microsoftTeams.tasks.startTask()` function in the client SDK.</span></span>
4. <span data-ttu-id="fecc7-124">Microsoft Teams muestra el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="fecc7-124">Microsoft Teams displays the task module.</span></span>

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="fecc7-125">Enviar el resultado de un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="fecc7-125">Submitting the result of a task module</span></span>

<span data-ttu-id="fecc7-126">Cuando el usuario termina con el módulo de tareas, el envío del resultado al bot es similar [a como funciona con las pestañas](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), pero hay algunas diferencias, por lo que también se describe aquí.</span><span class="sxs-lookup"><span data-stu-id="fecc7-126">When the user is finished with the task module, submitting the result back to the bot is similar [to the way it works with tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), but there are a few differences, so it's described here too.</span></span>

* <span data-ttu-id="fecc7-127">**HTML/JavaScript (`TaskInfo.url`)**.</span><span class="sxs-lookup"><span data-stu-id="fecc7-127">**HTML/JavaScript (`TaskInfo.url`)**.</span></span> <span data-ttu-id="fecc7-128">Una vez que haya validado lo que ha escrito el usuario, llame `microsoftTeams.tasks.submitTask()` a la función SDK (denominada a `submitTask()` partir de ahora con fines de legibilidad).</span><span class="sxs-lookup"><span data-stu-id="fecc7-128">Once you've validated what the user has entered, you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="fecc7-129">Si solo desea `submitTask()` que Microsoft Teams cierre el módulo de tareas, puede llamar a sin ningún parámetro, pero la mayoría de las veces querrá pasar un objeto o una cadena a `submitHandler`su.</span><span class="sxs-lookup"><span data-stu-id="fecc7-129">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span> <span data-ttu-id="fecc7-130">Simplemente páselo como el primer parámetro, `result`.</span><span class="sxs-lookup"><span data-stu-id="fecc7-130">Simply pass it as the first parameter, `result`.</span></span> <span data-ttu-id="fecc7-131">Microsoft Teams `submitHandler`invocará `err` : `null` será `result` y será el objeto o la cadena que ha `submitTask()`pasado a.</span><span class="sxs-lookup"><span data-stu-id="fecc7-131">Teams will invoke `submitHandler`: `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="fecc7-132">Si `submitTask()` llama a con `result` un parámetro, **debe** pasar una `appId` o una matriz de `appId` cadenas: Esto permite a Microsoft Teams validar que la aplicación que envía el resultado es la misma que ha invocado el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="fecc7-132">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span> <span data-ttu-id="fecc7-133">El bot recibirá un `task/submit` mensaje que `result` incluye lo que se describe [a continuación](#payload-of-taskfetch-and-tasksubmit-messages).</span><span class="sxs-lookup"><span data-stu-id="fecc7-133">Your bot will receive a `task/submit` message including `result` as described [below](#payload-of-taskfetch-and-tasksubmit-messages).</span></span>
* <span data-ttu-id="fecc7-134">**Tarjeta adaptable`TaskInfo.card`()**.</span><span class="sxs-lookup"><span data-stu-id="fecc7-134">**Adaptive card (`TaskInfo.card`)**.</span></span> <span data-ttu-id="fecc7-135">El cuerpo de la tarjeta adaptable (como rellenado por el usuario) se enviará al `task/submit` bot a través de un mensaje `Action.Submit` cuando el usuario presione cualquier botón.</span><span class="sxs-lookup"><span data-stu-id="fecc7-135">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit` message when the user presses any `Action.Submit` button.</span></span>

## <a name="the-flexibility-of-tasksubmit"></a><span data-ttu-id="fecc7-136">La flexibilidad de la tarea o el envío</span><span class="sxs-lookup"><span data-stu-id="fecc7-136">The flexibility of task/submit</span></span>

<span data-ttu-id="fecc7-137">En la sección anterior, aprendió que cuando el usuario termina con un módulo de tareas invocado desde un bot, el bot siempre recibe un `task/submit invoke` mensaje.</span><span class="sxs-lookup"><span data-stu-id="fecc7-137">In the previous section, you learned that when the user finishes with a task module invoked from a bot, the bot always receives a `task/submit invoke` message.</span></span> <span data-ttu-id="fecc7-138">Como desarrollador, tiene varias opciones para *responder* al `task/submit` mensaje:</span><span class="sxs-lookup"><span data-stu-id="fecc7-138">As a developer, you have several options when *responding* to the `task/submit` message:</span></span>

| <span data-ttu-id="fecc7-139">Respuesta del cuerpo HTTP</span><span class="sxs-lookup"><span data-stu-id="fecc7-139">HTTP Body Response</span></span>                      | <span data-ttu-id="fecc7-140">Escenario</span><span class="sxs-lookup"><span data-stu-id="fecc7-140">Scenario</span></span>                                |
| --------------------------------------- | --------------------------------------- |
| <span data-ttu-id="fecc7-141">Ninguno (omitir `task/submit` el mensaje)</span><span class="sxs-lookup"><span data-stu-id="fecc7-141">None (ignore the `task/submit` message)</span></span> | <span data-ttu-id="fecc7-142">La respuesta más sencilla no es ninguna respuesta.</span><span class="sxs-lookup"><span data-stu-id="fecc7-142">The simplest response is no response at all.</span></span> <span data-ttu-id="fecc7-143">No es necesario que el bot responda cuando el usuario haya terminado con el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="fecc7-143">Your bot is not required to respond when the user is finished with the task module.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | <span data-ttu-id="fecc7-144">Microsoft Teams mostrará el valor `value` de en un cuadro de mensaje emergente.</span><span class="sxs-lookup"><span data-stu-id="fecc7-144">Teams will display the value of `value` in a popup message box.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | <span data-ttu-id="fecc7-145">Permite "encadenar" secuencias de tarjetas adaptables juntas en un asistente/experiencia de varios pasos.</span><span class="sxs-lookup"><span data-stu-id="fecc7-145">Allows you to "chain" sequences of Adaptive cards together in a wizard/multi-step experience.</span></span> <span data-ttu-id="fecc7-146">_Tenga en cuenta que encadenar tarjetas adaptables en una secuencia es un escenario avanzado y no se documenta aquí. Sin embargo, la aplicación de ejemplo de node. js lo admite y el modo en que funciona se documenta en [su archivo README.MD](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._</span><span class="sxs-lookup"><span data-stu-id="fecc7-146">_Note that chaining Adaptive cards into a sequence is an advanced scenario and not documented here. The Node.js sample app supports it, however, and how it works is documented in [its README.md file](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._</span></span> |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a><span data-ttu-id="fecc7-147">Carga de tarea/búsqueda y mensajes de tarea o envío</span><span class="sxs-lookup"><span data-stu-id="fecc7-147">Payload of task/fetch and task/submit messages</span></span>

<span data-ttu-id="fecc7-148">En esta sección se define el esquema de lo que el bot recibe cuando `task/fetch` recibe `task/submit` un objeto `Activity` de marco de bot? o.</span><span class="sxs-lookup"><span data-stu-id="fecc7-148">This section defines the schema of what your bot receives when it receives a `task/fetch` or `task/submit` Bot Framework `Activity` object.</span></span> <span data-ttu-id="fecc7-149">El nivel superior importante aparece a continuación:</span><span class="sxs-lookup"><span data-stu-id="fecc7-149">The important top-level appear below:</span></span>

| <span data-ttu-id="fecc7-150">Propiedad</span><span class="sxs-lookup"><span data-stu-id="fecc7-150">Property</span></span> | <span data-ttu-id="fecc7-151">Descripción</span><span class="sxs-lookup"><span data-stu-id="fecc7-151">Description</span></span>                          |
| -------- | ------------------------------------ |
| `type`   | <span data-ttu-id="fecc7-152">Siempre será`invoke`</span><span class="sxs-lookup"><span data-stu-id="fecc7-152">Will always be `invoke`</span></span>              |
| `name`   | <span data-ttu-id="fecc7-153">Ya `task/fetch` sea o`task/submit`</span><span class="sxs-lookup"><span data-stu-id="fecc7-153">Either `task/fetch` or `task/submit`</span></span> |
| `value`  | <span data-ttu-id="fecc7-154">La carga definida por el desarrollador.</span><span class="sxs-lookup"><span data-stu-id="fecc7-154">The developer-defined payload.</span></span> <span data-ttu-id="fecc7-155">Normalmente, la estructura del `value` objeto refleja lo que se envió desde Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="fecc7-155">Normally the structure of the `value` object mirrors what was sent from Teams.</span></span> <span data-ttu-id="fecc7-156">En este caso, sin embargo, es diferente porque queremos admitir la recuperación dinámica (`task/fetch`) de bot Framework (`value`) y de las acciones de `Action.Submit` tarjeta adaptable (`data`), y necesitamos una forma de comunicar `context` Teams al bot además de lo que se incluyó `value` / `data`en.</span><span class="sxs-lookup"><span data-stu-id="fecc7-156">In this case, however, it's different because we want to support dynamic fetch (`task/fetch`) from both Bot Framework (`value`) and Adaptive card `Action.Submit` actions (`data`), and we need a way to communicate Teams `context` to the bot in addition to what was included in `value`/`data`.</span></span><br/><br/><span data-ttu-id="fecc7-157">Para ello, se combinan los dos en un objeto primario:</span><span class="sxs-lookup"><span data-stu-id="fecc7-157">We do this by combining the two into a parent object:</span></span><br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a><span data-ttu-id="fecc7-158">Ejemplo: recibir y responder a la tarea/búsqueda y a la tarea o enviar mensajes de invocación-node. js</span><span class="sxs-lookup"><span data-stu-id="fecc7-158">Example: Receiving and responding to task/fetch and task/submit invoke messages - Node.js</span></span>

> [!NOTE]
> <span data-ttu-id="fecc7-159">El siguiente código de ejemplo se modificó entre Technical Preview y la versión final de esta característica: `task/fetch` el esquema de la solicitud cambió para seguir el que se [documentó en la sección anterior](#payload-of-taskfetch-and-tasksubmit-messages).</span><span class="sxs-lookup"><span data-stu-id="fecc7-159">The sample code below was modified between Technical Preview and final release of this feature: the schema of the `task/fetch` request changed to follow what was [documented in the previous section](#payload-of-taskfetch-and-tasksubmit-messages).</span></span> <span data-ttu-id="fecc7-160">Es decir, la documentación era correcta, pero la implementación no.</span><span class="sxs-lookup"><span data-stu-id="fecc7-160">That is, the documentation was correct but the implementation was not.</span></span> <span data-ttu-id="fecc7-161">Vea los `// for Technical Preview [...]` comentarios a continuación para saber qué ha cambiado.</span><span class="sxs-lookup"><span data-stu-id="fecc7-161">See the `// for Technical Preview [...]` comments below for what changed.</span></span>

```typescript
// Handle requests and responses for a "Custom Form" and an "Adaptive card" task module.
// Assumes request is coming from an Adaptive card Action.Submit button that has a "taskModule" property indicating what to invoke
private async onInvoke(event: builder.IEvent, cb: (err: Error, body: any, status?: number) => void): Promise<void> {
    let invokeType = (event as any).name;
    let invokeValue = (event as any).value;
    if (invokeType === undefined) {
        invokeType = null;
    }
    switch (invokeType) {
        case "task/fetch": {
            if (invokeValue !== undefined && invokeValue.data.taskModule === "customform") { // for Technical Preview, was invokeValue.taskModule
                // Return the specified task module response to the bot
                let fetchTemplate: any = {
                    "task": {
                        "type": "continue",
                        "value": {
                            "title": "Custom Form",
                            "height": 510,
                            "width": 430,
                            "fallbackUrl": "https://contoso.com/teamsapp/customform",
                            "url": "https://contoso.com/teamsapp/customform",
                        }
                    }
                };
                cb(null, fetchTemplate, 200);
            };
            if (invokeValue !== undefined && invokeValue.data.taskModule === "adaptivecard") { // for Technical Preview, was invokeValue.taskModule
                let adaptiveCard = {
                    "type": "AdaptiveCard",
                    "body": [
                        {
                            "type": "TextBlock",
                            "text": "Here is a ninja cat:"
                        },
                        {
                            "type": "Image",
                            "url": "http://adaptivecards.io/content/cats/1.png",
                            "size": "Medium"
                        }
                    ],
                    "version": "1.0"
                };
                // Return the specified task module response to the bot
                let fetchTemplate: any = {
                    "task": {
                        "type": "continue",
                        "value": {
                            "title": "Ninja Cat",
                            "height": "small",
                            "width": "small",
                            "card": {
                                contentType: "application/vnd.microsoft.card.adaptive",
                                content: adaptiveCard,
                            }
                        }
                    }
                };
                cb(null, fetchTemplate, 200);
            };
            break;
        }
        case "task/submit": {
            if (invokeValue.data !== undefined) {
                // It's a valid task module response
                let submitResponse: any = {
                    "task": {
                        "type": "message",
                        "value": "Task complete!",
                    }
                };
                cb(null, fetchTemplates.submitMessageResponse, 200)
            }
        }
    }
}
```

<span data-ttu-id="fecc7-162">*Consulte también*el [código de ejemplo del módulo de tareas de Microsoft Teams: NodeJS](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts) y [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="fecc7-162">*See also*, [Microsoft Teams task module sample code — nodejs](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts) and  [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a><span data-ttu-id="fecc7-163">Ejemplo: recibir y responder a la tarea/búsqueda y a la tarea o enviar mensajes de invocación-C #</span><span class="sxs-lookup"><span data-stu-id="fecc7-163">Example: Receiving and responding to task/fetch and task/submit invoke messages - C#</span></span>

<span data-ttu-id="fecc7-164">En los bots de `invoke` C#, un `HttpResponseMessage()` controlador que procesa un `Activity` mensaje procesa los mensajes.</span><span class="sxs-lookup"><span data-stu-id="fecc7-164">In C# bots, `invoke` messages are processed by an `HttpResponseMessage()` controller processing an `Activity` message.</span></span> <span data-ttu-id="fecc7-165">Las `task/fetch` solicitudes `task/submit` y respuestas de y son JSON.</span><span class="sxs-lookup"><span data-stu-id="fecc7-165">The `task/fetch` and `task/submit` requests and responses are JSON.</span></span> <span data-ttu-id="fecc7-166">En C#, no es tan cómodo tratar con JSON sin procesar como en node. js, por lo que necesita que las clases de contenedor controlen la serialización a y desde JSON.</span><span class="sxs-lookup"><span data-stu-id="fecc7-166">In C#, it's not as convenient to deal with raw JSON as it is in Node.js, so you need wrapper classes to handle the serialization to and from JSON.</span></span> <span data-ttu-id="fecc7-167">Aún no hay compatibilidad directa con esto en el SDK de Microsoft Teams [C#](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) , pero puede ver un ejemplo del aspecto que tendrían estas clases de contenedor sencillas en la [aplicación de ejemplo de c#](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).</span><span class="sxs-lookup"><span data-stu-id="fecc7-167">There's no direct support for this in the Microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) yet, but you can see an example of what these simple wrapper classes would look like in the [C# sample app](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).</span></span>

<span data-ttu-id="fecc7-168">A continuación se muestra código de ejemplo en `task/fetch` C# `task/submit` para controlar y mensajes mediante estas`TaskInfo`clases `TaskEnvelope`contenedoras (,), extraídos del [ejemplo](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):</span><span class="sxs-lookup"><span data-stu-id="fecc7-168">Below is example code in C# for handling `task/fetch` and `task/submit` messages using these wrapper classes (`TaskInfo`, `TaskEnvelope`), excerpted from the [sample](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):</span></span>

```csharp
private HttpResponseMessage HandleInvokeMessages(Activity activity)
{
    var activityValue = activity.Value.ToString();
    if (activity.Name == "task/fetch")
    {
        var action = Newtonsoft.Json.JsonConvert.DeserializeObject<Models.BotFrameworkCardValue<string>>(activityValue);

        Models.TaskInfo taskInfo = GetTaskInfo(action.Data);
        Models.TaskEnvelope taskEnvelope = new Models.TaskEnvelope
        {
            Task = new Models.Task()
            {
                Type = Models.TaskType.Continue,
                TaskInfo = taskInfo
            }
        };
        return Request.CreateResponse(HttpStatusCode.OK, taskEnvelope);
    }
    else if (activity.Name == "task/submit")
    {
        ConnectorClient connector = new ConnectorClient(new Uri(activity.ServiceUrl));
        Activity reply = activity.CreateReply("Received = " + activity.Value.ToString());
        connector.Conversations.ReplyToActivity(reply);
    }
    return new HttpResponseMessage(HttpStatusCode.Accepted);
}

// Helper function for building the TaskInfo object based on the incoming request
private static Models.TaskInfo GetTaskInfo(string actionInfo)
{
    Models.TaskInfo taskInfo = new Models.TaskInfo();
    switch (actionInfo)
    {
        case TaskModuleIds.YouTube:
            taskInfo.Url = taskInfo.FallbackUrl = ApplicationSettings.BaseUrl + "/" + TaskModuleIds.YouTube;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.YouTube);
            break;
        case TaskModuleIds.PowerApp:
            taskInfo.Url = taskInfo.FallbackUrl = ApplicationSettings.BaseUrl + "/" + TaskModuleIds.PowerApp;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.PowerApp);
            break;
        case TaskModuleIds.CustomForm:
            taskInfo.Url = taskInfo.FallbackUrl = ApplicationSettings.BaseUrl + "/" + TaskModuleIds.CustomForm;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.CustomForm);
            break;
        case TaskModuleIds.AdaptiveCard:
            taskInfo.Card = AdaptiveCardHelper.GetAdaptiveCard();
            SetTaskInfo(taskInfo, TaskModuleUIConstants.AdaptiveCard);
            break;
        default:
            break;
    }
    return taskInfo;
}
```

<span data-ttu-id="fecc7-169">No se muestra en el ejemplo anterior es `SetTaskInfo()` la función, que establece `height`las `width`propiedades, `title` y del `TaskInfo` objeto para cada caso.</span><span class="sxs-lookup"><span data-stu-id="fecc7-169">Not shown in the above example is the `SetTaskInfo()` function, which sets the `height`, `width`, and `title` properties of the `TaskInfo` object for each case.</span></span> <span data-ttu-id="fecc7-170">Este es el [código fuente para SetTaskInfo ()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).</span><span class="sxs-lookup"><span data-stu-id="fecc7-170">Here's the [source code for SetTaskInfo()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).</span></span>

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a><span data-ttu-id="fecc7-171">Las acciones de la tarjeta de bot Framework y la acción de tarjeta adaptable. acciones de envío</span><span class="sxs-lookup"><span data-stu-id="fecc7-171">Bot Framework card actions vs. Adaptive card Action.Submit actions</span></span>

<span data-ttu-id="fecc7-172">El esquema de las acciones de la tarjeta de entorno de bot es `Action.Submit` ligeramente diferente de las acciones de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="fecc7-172">The schema for Bot Framework card actions is slightly different from Adaptive card `Action.Submit` actions.</span></span> <span data-ttu-id="fecc7-173">Como resultado, la manera de invocar módulos de tareas también es ligeramente distinta: `data` el objeto `Action.Submit` de contiene `msteams` un objeto para que no interfiera con otras propiedades de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="fecc7-173">As a result, the way to invoke task modules is slightly different too: the `data` object in `Action.Submit` contains an `msteams` object so it won't interfere with other properties in the card.</span></span> <span data-ttu-id="fecc7-174">En la siguiente tabla se muestra un ejemplo de cada uno:</span><span class="sxs-lookup"><span data-stu-id="fecc7-174">The following table shows an example of each:</span></span>

| <span data-ttu-id="fecc7-175">Acción de la tarjeta de bot Framework</span><span class="sxs-lookup"><span data-stu-id="fecc7-175">Bot Framework card action</span></span>                              | <span data-ttu-id="fecc7-176">Acción de tarjeta adaptable. acción enviar</span><span class="sxs-lookup"><span data-stu-id="fecc7-176">Adaptive card Action.Submit action</span></span>                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

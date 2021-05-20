---
title: Uso de módulos de tareas en bots Microsoft Teams
description: Cómo usar módulos de tareas con bots Microsoft Teams, incluidas tarjetas Bot Framework, tarjetas adaptables y vínculos profundos
localization_priority: Normal
ms.topic: how-to
keywords: módulos de tareas equipos bots
ms.openlocfilehash: bfaf3dfe791c1736aeb418e2689e513908f04534
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566574"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a><span data-ttu-id="ee545-104">Uso de módulos de tareas de bots Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ee545-104">Using task modules from Microsoft Teams bots</span></span>

<span data-ttu-id="ee545-105">Los módulos de tareas se pueden invocar desde Microsoft Teams bots mediante botones en tarjetas adaptables y tarjetas Bot Framework (Conector de héroe, miniatura y Office 365).</span><span class="sxs-lookup"><span data-stu-id="ee545-105">Task modules can be invoked from Microsoft Teams bots using buttons on Adaptive cards and Bot Framework cards (Hero, Thumbnail, and Office 365 Connector).</span></span> <span data-ttu-id="ee545-106">Los módulos de tareas suelen ser una mejor experiencia de usuario que varios pasos de conversación en los que usted como desarrollador tiene que realizar un seguimiento del estado del bot y permitir al usuario interrumpir o cancelar la secuencia.</span><span class="sxs-lookup"><span data-stu-id="ee545-106">Task modules are often a better user experience than multiple conversation steps where you as a developer have to keep track of bot state and allow the user to interrupt/cancel the sequence.</span></span>

<span data-ttu-id="ee545-107">Hay dos formas de invocar módulos de tareas:</span><span class="sxs-lookup"><span data-stu-id="ee545-107">There are two ways of invoking task modules:</span></span>

* <span data-ttu-id="ee545-108">**Un nuevo tipo de mensaje de invocación `task/fetch` .**</span><span class="sxs-lookup"><span data-stu-id="ee545-108">**A new kind of invoke message `task/fetch`.**</span></span> <span data-ttu-id="ee545-109">Mediante la `invoke` [acción de tarjeta](~/task-modules-and-cards/cards/cards-actions.md#invoke) para las tarjetas de Bot Framework, o la acción de la `Action.Submit` [tarjeta](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) para tarjetas adaptables, con `task/fetch` , el módulo de tareas (ya sea una DIRECCIÓN URL o una tarjeta adaptable) se obtiene dinámicamente desde el bot.</span><span class="sxs-lookup"><span data-stu-id="ee545-109">Using the `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke) for Bot Framework cards, or the `Action.Submit` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, with `task/fetch`, the task module (either a URL or an Adaptive card) is fetched dynamically from your bot.</span></span>
* <span data-ttu-id="ee545-110">**URL de vínculo profundo.**</span><span class="sxs-lookup"><span data-stu-id="ee545-110">**Deep link URLs.**</span></span> <span data-ttu-id="ee545-111">Con la [sintaxis de vínculo profundo para módulos de tareas,](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)puede usar la acción de `openUrl` [tarjeta](~/task-modules-and-cards/cards/cards-actions.md#openurl) para las tarjetas de Bot Framework o la `Action.OpenUrl` [acción de la tarjeta](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) para las tarjetas adaptables, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="ee545-111">Using the [deep link syntax for task modules](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax), you can use the `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#openurl) for Bot Framework cards or the `Action.OpenUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, respectively.</span></span> <span data-ttu-id="ee545-112">Con las URL de vínculo profundo, la DIRECCIÓN URL del módulo de tareas o el cuerpo de la tarjeta adaptable se conocen obviamente de antemano, evitando un viaje de ida y vuelta del servidor en relación con `task/fetch` .</span><span class="sxs-lookup"><span data-stu-id="ee545-112">With deep link URLs, the task module URL or Adaptive card body is obviously known in advance, avoiding a server round-trip relative to `task/fetch`.</span></span>

>[!IMPORTANT]
><span data-ttu-id="ee545-113">Para garantizar comunicaciones seguras, cada `url` uno y debe implementar el protocolo de cifrado `fallbackUrl` HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ee545-113">To ensure secure communications, each `url` and `fallbackUrl` must implement the HTTPS encryption protocol.</span></span>

## <a name="invoking-a-task-module-through-taskfetch"></a><span data-ttu-id="ee545-114">Invocar un módulo de tareas a través de tareas/captura</span><span class="sxs-lookup"><span data-stu-id="ee545-114">Invoking a task module through task/fetch</span></span>

<span data-ttu-id="ee545-115">Cuando el `value` objeto de la acción de la tarjeta o se inicializa de `invoke` la manera adecuada `Action.Submit` (explicado con más detalle a continuación), cuando un usuario presiona el botón se envía un `invoke` mensaje al bot.</span><span class="sxs-lookup"><span data-stu-id="ee545-115">When the `value` object of the `invoke` card action or `Action.Submit` is initialized in the proper way (explained in more detail below), when a user presses the button an `invoke` message is sent to the bot.</span></span> <span data-ttu-id="ee545-116">En la respuesta HTTP al `invoke` mensaje, hay un [objeto TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) incrustado en un objeto contenedor, que Teams utiliza para mostrar el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="ee545-116">In the HTTP response to the `invoke` message, there's a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, which Teams uses to display the task module.</span></span>

![tarea/solicitud de obtención/respuesta](~/assets/images/task-module/task-module-invoke-request-response.png)

<span data-ttu-id="ee545-118">Echemos un vistazo a cada paso con un poco más de detalle:</span><span class="sxs-lookup"><span data-stu-id="ee545-118">Let's look at each step in a bit more detail:</span></span>

1. <span data-ttu-id="ee545-119">En este ejemplo se muestra una tarjeta Bot Framework Hero con una `invoke` [acción de tarjeta](~/task-modules-and-cards/cards/cards-actions.md#invoke)"Comprar".</span><span class="sxs-lookup"><span data-stu-id="ee545-119">This example shows a Bot Framework Hero card with a "Buy" `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke).</span></span> <span data-ttu-id="ee545-120">El valor de la `type` propiedad es - el resto del objeto puede ser lo que `task/fetch` `value` quieras.</span><span class="sxs-lookup"><span data-stu-id="ee545-120">The value of the `type` property is `task/fetch` - the rest of the `value` object can be whatever you like.</span></span>
1. <span data-ttu-id="ee545-121">El bot recibe el `invoke` mensaje HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="ee545-121">The bot receives the `invoke` HTTP POST message.</span></span>
1. <span data-ttu-id="ee545-122">El bot crea un objeto de respuesta y lo devuelve en el cuerpo de la respuesta POST con un código de respuesta HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="ee545-122">The bot creates a response object and returns it in the body of the POST response with an HTTP 200 response code.</span></span> <span data-ttu-id="ee545-123">El esquema para las respuestas se describe [a continuación en la discusión sobre la tarea/envío](#the-flexibility-of-tasksubmit), pero lo importante que debe recordar ahora es que el cuerpo de la respuesta HTTP contiene un objeto [TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) incrustado en un objeto contenedor.</span><span class="sxs-lookup"><span data-stu-id="ee545-123">The schema for responses is described [below in the discussion on task/submit](#the-flexibility-of-tasksubmit), but the important thing to remember now is that the body of the HTTP response contains a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object.</span></span> <span data-ttu-id="ee545-124">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ee545-124">For example:</span></span>

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

    <span data-ttu-id="ee545-125">El `task/fetch` evento y su respuesta para bots es similar, conceptualmente, a la función en el SDK de `microsoftTeams.tasks.startTask()` cliente.</span><span class="sxs-lookup"><span data-stu-id="ee545-125">The `task/fetch` event and its response for bots is similar, conceptually, to the `microsoftTeams.tasks.startTask()` function in the client SDK.</span></span>
1. <span data-ttu-id="ee545-126">Microsoft Teams muestra el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="ee545-126">Microsoft Teams displays the task module.</span></span>

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="ee545-127">Envío del resultado de un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="ee545-127">Submitting the result of a task module</span></span>

<span data-ttu-id="ee545-128">Cuando el usuario ha terminado con el módulo de tareas, enviar el resultado de nuevo al bot es similar [a la forma en que funciona con las pestañas,](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)pero hay algunas diferencias, por lo que se describe aquí también.</span><span class="sxs-lookup"><span data-stu-id="ee545-128">When the user is finished with the task module, submitting the result back to the bot is similar [to the way it works with tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), but there are a few differences, so it's described here too.</span></span>

* <span data-ttu-id="ee545-129">**HTML/JavaScript ( `TaskInfo.url` )**.</span><span class="sxs-lookup"><span data-stu-id="ee545-129">**HTML/JavaScript (`TaskInfo.url`)**.</span></span> <span data-ttu-id="ee545-130">Una vez que haya validado lo que ha especificado el usuario, llame a la `microsoftTeams.tasks.submitTask()` función SDK (denominada en adelante `submitTask()` para fines de legibilidad).</span><span class="sxs-lookup"><span data-stu-id="ee545-130">Once you've validated what the user has entered, you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="ee545-131">Puede llamar `submitTask()` sin ningún parámetro si solo desea que Teams cierre el módulo de tareas, pero la mayoría de las veces querrá pasar un objeto o una cadena a su `submitHandler` archivo .</span><span class="sxs-lookup"><span data-stu-id="ee545-131">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span> <span data-ttu-id="ee545-132">Simplemente páselo como el primer parámetro, `result` .</span><span class="sxs-lookup"><span data-stu-id="ee545-132">Simply pass it as the first parameter, `result`.</span></span> <span data-ttu-id="ee545-133">Teams `submitHandler` invocará: `err` será `null` y será `result` el objeto/cadena al que `submitTask()` pasó.</span><span class="sxs-lookup"><span data-stu-id="ee545-133">Teams will invoke `submitHandler`: `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="ee545-134">Si llama `submitTask()` con un `result` parámetro, **debe** pasar una `appId` o una matriz de `appId` cadenas: esto permite a Teams validar que la aplicación que envía el resultado es la misma que invocó el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="ee545-134">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span> <span data-ttu-id="ee545-135">El bot recibirá un `task/submit` mensaje, incluso `result` como se describe [a continuación.](#payload-of-taskfetch-and-tasksubmit-messages)</span><span class="sxs-lookup"><span data-stu-id="ee545-135">Your bot will receive a `task/submit` message including `result` as described [below](#payload-of-taskfetch-and-tasksubmit-messages).</span></span>
* <span data-ttu-id="ee545-136">**Tarjeta adaptativa ( `TaskInfo.card` ).**</span><span class="sxs-lookup"><span data-stu-id="ee545-136">**Adaptive card (`TaskInfo.card`)**.</span></span> <span data-ttu-id="ee545-137">El cuerpo de la tarjeta adaptable (rellenado por el usuario) se enviará al bot a través de un `task/submit` mensaje cuando el usuario presione cualquier `Action.Submit` botón.</span><span class="sxs-lookup"><span data-stu-id="ee545-137">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit` message when the user presses any `Action.Submit` button.</span></span>

## <a name="the-flexibility-of-tasksubmit"></a><span data-ttu-id="ee545-138">La flexibilidad de la tarea/enviar</span><span class="sxs-lookup"><span data-stu-id="ee545-138">The flexibility of task/submit</span></span>

<span data-ttu-id="ee545-139">En la sección anterior, aprendió que cuando el usuario termina con un módulo de tareas invocado desde un bot, el bot siempre recibe un `task/submit invoke` mensaje.</span><span class="sxs-lookup"><span data-stu-id="ee545-139">In the previous section, you learned that when the user finishes with a task module invoked from a bot, the bot always receives a `task/submit invoke` message.</span></span> <span data-ttu-id="ee545-140">Como desarrollador, tiene varias opciones al *responder* al `task/submit` mensaje:</span><span class="sxs-lookup"><span data-stu-id="ee545-140">As a developer, you have several options when *responding* to the `task/submit` message:</span></span>

| <span data-ttu-id="ee545-141">Respuesta del cuerpo HTTP</span><span class="sxs-lookup"><span data-stu-id="ee545-141">HTTP Body Response</span></span>                      | <span data-ttu-id="ee545-142">Escenario</span><span class="sxs-lookup"><span data-stu-id="ee545-142">Scenario</span></span>                                |
| --------------------------------------- | --------------------------------------- |
| <span data-ttu-id="ee545-143">Ninguno (ignore el `task/submit` mensaje)</span><span class="sxs-lookup"><span data-stu-id="ee545-143">None (ignore the `task/submit` message)</span></span> | <span data-ttu-id="ee545-144">La respuesta más simple no es ninguna respuesta en absoluto.</span><span class="sxs-lookup"><span data-stu-id="ee545-144">The simplest response is no response at all.</span></span> <span data-ttu-id="ee545-145">El bot no es necesario para responder cuando el usuario haya terminado con el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="ee545-145">Your bot is not required to respond when the user is finished with the task module.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | <span data-ttu-id="ee545-146">Teams mostrará el valor de un cuadro de `value` mensaje emergente.</span><span class="sxs-lookup"><span data-stu-id="ee545-146">Teams will display the value of `value` in a popup message box.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | <span data-ttu-id="ee545-147">Le permite "encadenar" secuencias de tarjetas adaptables juntas en una experiencia wizard/multi-step.</span><span class="sxs-lookup"><span data-stu-id="ee545-147">Allows you to "chain" sequences of Adaptive cards together in a wizard/multi-step experience.</span></span> <span data-ttu-id="ee545-148">_Tenga en cuenta que encadenar tarjetas adaptables en una secuencia es un escenario avanzado y no se documenta aquí. Sin embargo, la aplicación de ejemplo Node.js la admite y cómo funciona se documenta en [su archivo README.md.](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)_</span><span class="sxs-lookup"><span data-stu-id="ee545-148">_Note that chaining Adaptive cards into a sequence is an advanced scenario and not documented here. The Node.js sample app supports it, however, and how it works is documented in [its README.md file](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._</span></span> |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a><span data-ttu-id="ee545-149">Carga útil de mensajes task/fetch y task/submit</span><span class="sxs-lookup"><span data-stu-id="ee545-149">Payload of task/fetch and task/submit messages</span></span>

<span data-ttu-id="ee545-150">En esta sección se define el esquema de lo que recibe el bot cuando recibe un `task/fetch` objeto o `task/submit` Bot `Activity` Framework.</span><span class="sxs-lookup"><span data-stu-id="ee545-150">This section defines the schema of what your bot receives when it receives a `task/fetch` or `task/submit` Bot Framework `Activity` object.</span></span> <span data-ttu-id="ee545-151">El nivel superior importante aparece a continuación:</span><span class="sxs-lookup"><span data-stu-id="ee545-151">The important top-level appear below:</span></span>

| <span data-ttu-id="ee545-152">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ee545-152">Property</span></span> | <span data-ttu-id="ee545-153">Descripción</span><span class="sxs-lookup"><span data-stu-id="ee545-153">Description</span></span>                          |
| -------- | ------------------------------------ |
| `type`   | <span data-ttu-id="ee545-154">Siempre será `invoke`</span><span class="sxs-lookup"><span data-stu-id="ee545-154">Will always be `invoke`</span></span>              |
| `name`   | <span data-ttu-id="ee545-155">O bien `task/fetch` o `task/submit`</span><span class="sxs-lookup"><span data-stu-id="ee545-155">Either `task/fetch` or `task/submit`</span></span> |
| `value`  | <span data-ttu-id="ee545-156">La carga definida por el desarrollador.</span><span class="sxs-lookup"><span data-stu-id="ee545-156">The developer-defined payload.</span></span> <span data-ttu-id="ee545-157">Normalmente, la estructura del `value` objeto refleja lo que se envió desde Teams.</span><span class="sxs-lookup"><span data-stu-id="ee545-157">Normally the structure of the `value` object mirrors what was sent from Teams.</span></span> <span data-ttu-id="ee545-158">En este caso, sin embargo, es diferente porque queremos admitir la captura dinámica ( `task/fetch` ) tanto desde Bot Framework ( ) como desde acciones de tarjeta adaptable `value` `Action.Submit` `data` (), y necesitamos una forma de comunicar Teams al bot `context` además `value` / `data` de lo que se incluyó en .</span><span class="sxs-lookup"><span data-stu-id="ee545-158">In this case, however, it's different because we want to support dynamic fetch (`task/fetch`) from both Bot Framework (`value`) and Adaptive card `Action.Submit` actions (`data`), and we need a way to communicate Teams `context` to the bot in addition to what was included in `value`/`data`.</span></span><br/><br/><span data-ttu-id="ee545-159">Hacemos esto combinando los dos en un objeto primario:</span><span class="sxs-lookup"><span data-stu-id="ee545-159">We do this by combining the two into a parent object:</span></span><br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a><span data-ttu-id="ee545-160">Ejemplo: Recepción y respuesta a mensajes de invocación de tareas/captura y tareas/envíos- Node.js</span><span class="sxs-lookup"><span data-stu-id="ee545-160">Example: Receiving and responding to task/fetch and task/submit invoke messages - Node.js</span></span>

> [!NOTE]
> <span data-ttu-id="ee545-161">El código de ejemplo siguiente se modificó entre Technical Preview y la versión final de esta característica: el esquema de la `task/fetch` solicitud cambió para seguir lo que se [documentó en la sección anterior.](#payload-of-taskfetch-and-tasksubmit-messages)</span><span class="sxs-lookup"><span data-stu-id="ee545-161">The sample code below was modified between Technical Preview and final release of this feature: the schema of the `task/fetch` request changed to follow what was [documented in the previous section](#payload-of-taskfetch-and-tasksubmit-messages).</span></span> <span data-ttu-id="ee545-162">Es decir, la documentación era correcta, pero la implementación no lo era.</span><span class="sxs-lookup"><span data-stu-id="ee545-162">That is, the documentation was correct but the implementation was not.</span></span> <span data-ttu-id="ee545-163">Consulte los `// for Technical Preview [...]` comentarios a continuación para ver qué cambió.</span><span class="sxs-lookup"><span data-stu-id="ee545-163">See the `// for Technical Preview [...]` comments below for what changed.</span></span>

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

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a><span data-ttu-id="ee545-164">Ejemplo: Recepción y respuesta a mensajes de invocación task/fetch y task/submit - C #</span><span class="sxs-lookup"><span data-stu-id="ee545-164">Example: Receiving and responding to task/fetch and task/submit invoke messages - C#</span></span>

<span data-ttu-id="ee545-165">En los bots de C#, `invoke` los mensajes son procesados por un controlador `HttpResponseMessage()` que procesa un `Activity` mensaje.</span><span class="sxs-lookup"><span data-stu-id="ee545-165">In C# bots, `invoke` messages are processed by an `HttpResponseMessage()` controller processing an `Activity` message.</span></span> <span data-ttu-id="ee545-166">Las `task/fetch` `task/submit` solicitudes y respuestas son JSON.</span><span class="sxs-lookup"><span data-stu-id="ee545-166">The `task/fetch` and `task/submit` requests and responses are JSON.</span></span> <span data-ttu-id="ee545-167">En C#, no es tan conveniente tratar con JSON sin procesar como en Node.js, por lo que necesita clases contenedoras para controlar la serialización hacia y desde JSON.</span><span class="sxs-lookup"><span data-stu-id="ee545-167">In C#, it's not as convenient to deal with raw JSON as it is in Node.js, so you need wrapper classes to handle the serialization to and from JSON.</span></span> <span data-ttu-id="ee545-168">Todavía no hay compatibilidad directa con esto en el SDK de [Microsoft Teams C#,](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) pero puede ver un ejemplo de cómo serían estas clases contenedoras simples en la [aplicación de ejemplo de C#.](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs)</span><span class="sxs-lookup"><span data-stu-id="ee545-168">There's no direct support for this in the Microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) yet, but you can see an example of what these simple wrapper classes would look like in the [C# sample app](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).</span></span>

<span data-ttu-id="ee545-169">A continuación se muestra el código de ejemplo en C# para el control `task/fetch` y los mensajes que utilizan estas clases `task/submit` contenedoras ( , ), extraído `TaskInfo` del `TaskEnvelope` [ejemplo:](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)</span><span class="sxs-lookup"><span data-stu-id="ee545-169">Below is example code in C# for handling `task/fetch` and `task/submit` messages using these wrapper classes (`TaskInfo`, `TaskEnvelope`), excerpted from the [sample](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):</span></span>

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

<span data-ttu-id="ee545-170">En el ejemplo anterior no se muestra la `SetTaskInfo()` función, que establece el `height` objeto y las propiedades del objeto para cada `width` `title` `TaskInfo` caso.</span><span class="sxs-lookup"><span data-stu-id="ee545-170">Not shown in the above example is the `SetTaskInfo()` function, which sets the `height`, `width`, and `title` properties of the `TaskInfo` object for each case.</span></span> <span data-ttu-id="ee545-171">Aquí está el [código fuente de SetTaskInfo()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).</span><span class="sxs-lookup"><span data-stu-id="ee545-171">Here's the [source code for SetTaskInfo()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).</span></span>

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a><span data-ttu-id="ee545-172">Acciones de la tarjeta Bot Framework frente a acciones de action.submit de tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="ee545-172">Bot Framework card actions vs. Adaptive card Action.Submit actions</span></span>

<span data-ttu-id="ee545-173">El esquema de las acciones de la tarjeta bot framework es ligeramente diferente de las acciones de la tarjeta `Action.Submit` adaptable.</span><span class="sxs-lookup"><span data-stu-id="ee545-173">The schema for Bot Framework card actions is slightly different from Adaptive card `Action.Submit` actions.</span></span> <span data-ttu-id="ee545-174">Como resultado, la forma de invocar módulos de tareas también es ligeramente diferente: el `data` objeto contiene un objeto para que no `Action.Submit` `msteams` interfiera con otras propiedades de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="ee545-174">As a result, the way to invoke task modules is slightly different too: the `data` object in `Action.Submit` contains an `msteams` object so it won't interfere with other properties in the card.</span></span> <span data-ttu-id="ee545-175">En la tabla siguiente se muestra un ejemplo de cada uno:</span><span class="sxs-lookup"><span data-stu-id="ee545-175">The following table shows an example of each:</span></span>

| <span data-ttu-id="ee545-176">Acción de la tarjeta Bot Framework</span><span class="sxs-lookup"><span data-stu-id="ee545-176">Bot Framework card action</span></span>                              | <span data-ttu-id="ee545-177">Acción de tarjeta adaptable.Enviar acción</span><span class="sxs-lookup"><span data-stu-id="ee545-177">Adaptive card Action.Submit action</span></span>                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="see-also"></a><span data-ttu-id="ee545-178">Vea también</span><span class="sxs-lookup"><span data-stu-id="ee545-178">See also</span></span>

* [<span data-ttu-id="ee545-179">Microsoft Teams código de ejemplo del módulo de tareas — nodejs</span><span class="sxs-lookup"><span data-stu-id="ee545-179">Microsoft Teams task module sample code — nodejs</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* <span data-ttu-id="ee545-180">[Muestras de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="ee545-180">[Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>
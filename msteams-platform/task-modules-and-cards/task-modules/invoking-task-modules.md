---
title: Invocar y descartar módulos de tareas
description: Invocar y descartar módulos de tareas.
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: a23d5cee3f13967772a4b58ed973bf08906e36a6
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140781"
---
# <a name="invoke-and-dismiss-task-modules"></a><span data-ttu-id="7df38-103">Invocar y descartar módulos de tareas</span><span class="sxs-lookup"><span data-stu-id="7df38-103">Invoke and dismiss task modules</span></span>

<span data-ttu-id="7df38-104">Los módulos de tareas se pueden invocar desde pestañas, bots o vínculos profundos.</span><span class="sxs-lookup"><span data-stu-id="7df38-104">Task modules can be invoked from tabs, bots, or deep links.</span></span> <span data-ttu-id="7df38-105">La respuesta puede estar en HTML, JavaScript o como una tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="7df38-105">The response can be either in HTML, JavaScript, or as an Adaptive Card.</span></span> <span data-ttu-id="7df38-106">Hay mucha flexibilidad en términos de cómo se invocan los módulos de tareas y cómo tratar la respuesta de la interacción del usuario.</span><span class="sxs-lookup"><span data-stu-id="7df38-106">There is a lot of flexibility in terms of how task modules are invoked and how to deal with the response of the user's interaction.</span></span> <span data-ttu-id="7df38-107">En la tabla siguiente se resume cómo funciona esto:</span><span class="sxs-lookup"><span data-stu-id="7df38-107">The following table summarizes how this works:</span></span>

| <span data-ttu-id="7df38-108">Invocado mediante</span><span class="sxs-lookup"><span data-stu-id="7df38-108">Invoked using</span></span> | <span data-ttu-id="7df38-109">Módulo de tareas con HTML o JavaScript</span><span class="sxs-lookup"><span data-stu-id="7df38-109">Task module with HTML or JavaScript</span></span> | <span data-ttu-id="7df38-110">Módulo de tareas con tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="7df38-110">Task module with Adaptive Card</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7df38-111">JavaScript en una pestaña</span><span class="sxs-lookup"><span data-stu-id="7df38-111">JavaScript in a tab</span></span> | <span data-ttu-id="7df38-112">1. Use la función Teams SDK de cliente `tasks.startTask()` con una función de devolución de llamada `submitHandler(err, result)` opcional.</span><span class="sxs-lookup"><span data-stu-id="7df38-112">1. Use the Teams client SDK function `tasks.startTask()` with an optional `submitHandler(err, result)` callback function.</span></span> <br/><br/> <span data-ttu-id="7df38-113">2. En el código del módulo de tareas, cuando el usuario haya realizado las acciones, llame a la función sdk de Teams con un objeto `tasks.submitTask()` `result` como parámetro.</span><span class="sxs-lookup"><span data-stu-id="7df38-113">2. In the task module code, when the user has performed the actions, call the Teams SDK function `tasks.submitTask()` with a `result` object as a parameter.</span></span> <span data-ttu-id="7df38-114">Si se especificó una devolución de llamada `submitHandler` en , Teams la llama con como `tasks.startTask()` `result` parámetro.</span><span class="sxs-lookup"><span data-stu-id="7df38-114">If a `submitHandler` callback was specified in `tasks.startTask()`, Teams calls it with `result` as a parameter.</span></span> <span data-ttu-id="7df38-115">Si se produjo un error al invocar , se llama a la `tasks.startTask()` función con una cadena en su `submitHandler` `err` lugar.</span><span class="sxs-lookup"><span data-stu-id="7df38-115">If there was an error when invoking `tasks.startTask()`, the `submitHandler` function is called with an `err` string instead.</span></span> <br/><br/> <span data-ttu-id="7df38-116">3. También puede especificar un al `completionBotId` llamar `teams.startTask()` a .</span><span class="sxs-lookup"><span data-stu-id="7df38-116">3. You can also specify a `completionBotId` when calling `teams.startTask()`.</span></span> <span data-ttu-id="7df38-117">A `result` continuación, se envía al bot en su lugar.</span><span class="sxs-lookup"><span data-stu-id="7df38-117">Then the `result` is sent to the bot instead.</span></span> | <span data-ttu-id="7df38-118">1. Llame a la función Teams SDK de cliente con un objeto TaskInfo y que contenga el JSON para que la tarjeta adaptable se muestre en la ventana emergente del módulo `tasks.startTask()` de [](#the-taskinfo-object) `TaskInfo.card` tareas.</span><span class="sxs-lookup"><span data-stu-id="7df38-118">1. Call the Teams client SDK function `tasks.startTask()` with a [TaskInfo object](#the-taskinfo-object) and `TaskInfo.card` containing the JSON for the Adaptive Card to show in the task module pop-up.</span></span> <br/><br/> <span data-ttu-id="7df38-119">2. Si se especificó una devolución de llamada en , Teams la llama con una cadena, si se produjo un error al invocar o si el usuario cierra el elemento emergente del módulo de tareas con la X en la parte `submitHandler` `tasks.startTask()` superior `err` `tasks.startTask()` derecha.</span><span class="sxs-lookup"><span data-stu-id="7df38-119">2. If a `submitHandler` callback was specified in `tasks.startTask()`, Teams calls it with an `err` string, if there was an error when invoking `tasks.startTask()` or if the user closes the task module pop-up using the X at the upper right.</span></span> <br/><br/> <span data-ttu-id="7df38-120">3. Si el usuario presiona un `Action.Submit` botón, su `data` objeto se devuelve como el valor de `result` .</span><span class="sxs-lookup"><span data-stu-id="7df38-120">3. If the user presses an `Action.Submit` button then its `data` object is returned as the value of `result`.</span></span> |
| <span data-ttu-id="7df38-121">Botón de tarjeta bot</span><span class="sxs-lookup"><span data-stu-id="7df38-121">Bot card button</span></span> | <span data-ttu-id="7df38-122">1. Los botones de tarjeta bot, según el tipo de botón, pueden invocar módulos de tareas de dos maneras, una dirección URL de vínculo profundo o enviando un `task/fetch` mensaje.</span><span class="sxs-lookup"><span data-stu-id="7df38-122">1. Bot card buttons, depending on the type of button, can invoke task modules in two ways, a deep link URL or by sending a `task/fetch` message.</span></span> <br/><br/> <span data-ttu-id="7df38-123">2. Si la acción del botón es el tipo de botón para tarjetas adaptables, se envía un evento que es `type` un POST HTTP al `task/fetch` `Action.Submit` `task/fetch invoke` bot.</span><span class="sxs-lookup"><span data-stu-id="7df38-123">2. If the button's action `type` is `task/fetch` that is `Action.Submit` button type for Adaptive Cards, a `task/fetch invoke` event that is an HTTP POST is sent to the bot.</span></span> <span data-ttu-id="7df38-124">El bot responde al POST con HTTP 200 y al cuerpo de la respuesta que contiene un contenedor alrededor del [objeto TaskInfo](#the-taskinfo-object).</span><span class="sxs-lookup"><span data-stu-id="7df38-124">The bot responds to the POST with HTTP 200 and the response body containing a wrapper around the [TaskInfo object](#the-taskinfo-object).</span></span> <span data-ttu-id="7df38-125">Para obtener más información, [vea invocar `task/fetch` un módulo de tareas mediante ](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch).</span><span class="sxs-lookup"><span data-stu-id="7df38-125">For more information, see [invoking a task module using `task/fetch`](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch).</span></span> <span data-ttu-id="7df38-126">Teams muestra el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="7df38-126">Teams displays the task module.</span></span> <br/><br/> <span data-ttu-id="7df38-127">3. Después de que el usuario haya realizado las acciones, llame a la función Teams SDK `tasks.submitTask()` con un objeto como `result` parámetro.</span><span class="sxs-lookup"><span data-stu-id="7df38-127">3. After the user has performed the actions, call the Teams SDK function `tasks.submitTask()` with a `result` object as a parameter.</span></span> <span data-ttu-id="7df38-128">El bot recibe un `task/submit invoke` mensaje que contiene el `result` objeto.</span><span class="sxs-lookup"><span data-stu-id="7df38-128">The bot receives a `task/submit invoke` message that contains the `result` object.</span></span> <br/><br/> <span data-ttu-id="7df38-129">4. Tiene tres formas diferentes de responder al mensaje, sin hacer nada que sea la tarea completada correctamente, mostrando un mensaje al usuario en una ventana emergente o invocando otra ventana del módulo de `task/submit` tareas.</span><span class="sxs-lookup"><span data-stu-id="7df38-129">4. You have three different ways to respond to the `task/submit` message, by doing nothing that is the task completed successfully, by displaying a message to the user in a pop-up window, or by invoking another task module window.</span></span> <span data-ttu-id="7df38-130">Para obtener más información, vea [discusión detallada sobre `task/submit` ](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span><span class="sxs-lookup"><span data-stu-id="7df38-130">For more information, see [detailed discussion on `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span></span> | <ul><li> <span data-ttu-id="7df38-131">Al igual que los botones de las tarjetas de Bot Framework, los botones de las tarjetas adaptables admiten dos formas de invocar módulos de tareas, las direcciones URL de vínculo profundo con botones y `Action.openUrl` `task/fetch` el uso de `Action.Submit` botones.</span><span class="sxs-lookup"><span data-stu-id="7df38-131">Like buttons on Bot Framework cards, buttons on Adaptive Cards support two ways of invoking task modules, deep link URLs with `Action.openUrl` buttons, and `task/fetch` using `Action.Submit` buttons.</span></span> </li></ul> <br/><br/> <ul><li> <span data-ttu-id="7df38-132">Los módulos de tareas con tarjetas adaptables funcionan de forma muy similar al caso html o JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7df38-132">Task modules with Adaptive Cards work very similarly to the HTML or JavaScript case.</span></span> <span data-ttu-id="7df38-133">La principal diferencia es que, dado que no hay JavaScript cuando se usan tarjetas adaptables, no hay forma de llamar a `tasks.submitTask()` .</span><span class="sxs-lookup"><span data-stu-id="7df38-133">The major difference is that since there is no JavaScript when you are using Adaptive Cards, there is no way to call `tasks.submitTask()`.</span></span> <span data-ttu-id="7df38-134">En su lugar, Teams toma el objeto y `data` lo devuelve como la carga del `Action.Submit` `task/submit` evento.</span><span class="sxs-lookup"><span data-stu-id="7df38-134">Instead, Teams takes the `data` object from `Action.Submit` and returns it as the payload of the `task/submit` event.</span></span> <span data-ttu-id="7df38-135">Para obtener más información, [vea flexibilidad de `task/submit` ](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span><span class="sxs-lookup"><span data-stu-id="7df38-135">For more information, see [flexibility of `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span></span> </li></ul> |
| <span data-ttu-id="7df38-136">URL de vínculo profundo</span><span class="sxs-lookup"><span data-stu-id="7df38-136">Deep link URL</span></span> <br/>[<span data-ttu-id="7df38-137">sintaxis URL</span><span class="sxs-lookup"><span data-stu-id="7df38-137">URL syntax</span></span>](#task-module-deep-link-syntax) | <span data-ttu-id="7df38-138">1. Teams invoca el módulo de tareas que es la dirección URL que aparece dentro del especificado en el `<iframe>` `url` parámetro del vínculo profundo.</span><span class="sxs-lookup"><span data-stu-id="7df38-138">1. Teams invokes the task module that is the URL that appears inside the `<iframe>` specified in the `url` parameter of the deep link.</span></span> <span data-ttu-id="7df38-139">No hay `submitHandler` devolución de llamada.</span><span class="sxs-lookup"><span data-stu-id="7df38-139">There is no `submitHandler` callback.</span></span> <br/><br/> <span data-ttu-id="7df38-140">2. Dentro del JavaScript de la página del módulo de tareas, llame para cerrarlo con un objeto como parámetro, lo mismo que al invocarlo desde una pestaña o un botón de tarjeta `tasks.submitTask()` `result` de bot.</span><span class="sxs-lookup"><span data-stu-id="7df38-140">2. Within the JavaScript of the page in the task module, call `tasks.submitTask()` to close it with a `result` object as a parameter, the same as when invoking it from a tab or a bot card button.</span></span> <span data-ttu-id="7df38-141">Sin embargo, la lógica de finalización es ligeramente diferente.</span><span class="sxs-lookup"><span data-stu-id="7df38-141">However, completion logic is slightly different.</span></span> <span data-ttu-id="7df38-142">Si la lógica de finalización reside en el cliente que es si no hay bot, no hay devolución de llamada, por lo que cualquier lógica de finalización debe estar en el código anterior a la `submitHandler` llamada a `tasks.submitTask()` .</span><span class="sxs-lookup"><span data-stu-id="7df38-142">If your completion logic resides on the client that is if there is no bot, there is no `submitHandler` callback, so any completion logic must be in the code preceding the call to `tasks.submitTask()`.</span></span> <span data-ttu-id="7df38-143">Los errores de invocación solo se notifican a través de la consola.</span><span class="sxs-lookup"><span data-stu-id="7df38-143">Invocation errors are only reported through the console.</span></span> <span data-ttu-id="7df38-144">Si tiene un bot, puede especificar un parámetro en el vínculo profundo para `completionBotId` enviar el objeto a través de un `result` `task/submit` evento.</span><span class="sxs-lookup"><span data-stu-id="7df38-144">If you have a bot, then you can specify a `completionBotId` parameter in the deep link to send the `result` object through a `task/submit` event.</span></span> | <span data-ttu-id="7df38-145">1. Teams invoca el módulo de tareas que es el cuerpo de la tarjeta JSON de la tarjeta adaptable que se especifica como un valor codificado en URL del parámetro del `card` vínculo profundo.</span><span class="sxs-lookup"><span data-stu-id="7df38-145">1. Teams invokes the task module that is the JSON card body of the Adaptive Card that is specified as a URL-encoded value of the `card` parameter of the deep link.</span></span> <br/><br/> <span data-ttu-id="7df38-146">2. El usuario cierra el módulo de tareas seleccionando la X en la parte superior derecha del módulo de tareas o presionando un `Action.Submit` botón en la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="7df38-146">2. The user closes the task module by selecting the X at the upper right of the task module or by pressing an `Action.Submit` button on the card.</span></span> <span data-ttu-id="7df38-147">Dado que no hay `submitHandler` que llamar, el usuario debe tener un bot para enviar el valor de los campos de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="7df38-147">Since there is no `submitHandler` to call, the user must have a bot to send the value of the Adaptive Card fields.</span></span> <span data-ttu-id="7df38-148">El usuario debe usar el parámetro en el vínculo profundo para especificar el bot al que se enviarán `completionBotId` los datos mediante un `task/submit invoke` evento.</span><span class="sxs-lookup"><span data-stu-id="7df38-148">The user must use the `completionBotId` parameter in the deep link to specify the bot to send the data to using a `task/submit invoke` event.</span></span> |

> [!NOTE]
> <span data-ttu-id="7df38-149">La invocación de un módulo de tareas desde JavaScript no se admite en dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="7df38-149">Invoking a task module from JavaScript is not supported on mobile.</span></span>

<span data-ttu-id="7df38-150">La siguiente sección especifica el `TaskInfo` objeto que define determinados atributos para un módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="7df38-150">The next section specifies the `TaskInfo` object that defines certain attributes for a task module.</span></span>

## <a name="the-taskinfo-object"></a><span data-ttu-id="7df38-151">El objeto TaskInfo</span><span class="sxs-lookup"><span data-stu-id="7df38-151">The TaskInfo object</span></span>

<span data-ttu-id="7df38-152">El `TaskInfo` objeto contiene los metadatos de un módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="7df38-152">The `TaskInfo` object contains the metadata for a task module.</span></span> <span data-ttu-id="7df38-153">Defina el `url` para un iFrame incrustado o `card` para una tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="7df38-153">Define the `url` for an embedded iFrame or `card` for an Adaptive Card.</span></span> <span data-ttu-id="7df38-154">En la tabla siguiente se proporciona la definición de objeto:</span><span class="sxs-lookup"><span data-stu-id="7df38-154">The following table provides the object definition:</span></span>

| <span data-ttu-id="7df38-155">Atributo</span><span class="sxs-lookup"><span data-stu-id="7df38-155">Attribute</span></span> | <span data-ttu-id="7df38-156">Tipo</span><span class="sxs-lookup"><span data-stu-id="7df38-156">Type</span></span> | <span data-ttu-id="7df38-157">Descripción</span><span class="sxs-lookup"><span data-stu-id="7df38-157">Description</span></span> |
| --- | --- | --- |
| `title` | <span data-ttu-id="7df38-158">string</span><span class="sxs-lookup"><span data-stu-id="7df38-158">string</span></span> | <span data-ttu-id="7df38-159">Este atributo aparece debajo del nombre de la aplicación y a la derecha del icono de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7df38-159">This attribute appears below the app name and to the right of the app icon.</span></span> |
| `height` | <span data-ttu-id="7df38-160">número o cadena</span><span class="sxs-lookup"><span data-stu-id="7df38-160">number or string</span></span> | <span data-ttu-id="7df38-161">Este atributo puede ser un número que representa el alto del módulo de tareas en píxeles, `small` o , `medium` o `large` .</span><span class="sxs-lookup"><span data-stu-id="7df38-161">This attribute can be a number representing the task module's height in pixels, or `small`, `medium`, or `large`.</span></span> <span data-ttu-id="7df38-162">Para obtener más información, vea [task module sizing](#task-module-sizing).</span><span class="sxs-lookup"><span data-stu-id="7df38-162">For more information, see [task module sizing](#task-module-sizing).</span></span> |
| `width` | <span data-ttu-id="7df38-163">número o cadena</span><span class="sxs-lookup"><span data-stu-id="7df38-163">number or string</span></span> | <span data-ttu-id="7df38-164">Este atributo puede ser un número que representa el ancho del módulo de tareas en píxeles, `small` o , `medium` o `large` .</span><span class="sxs-lookup"><span data-stu-id="7df38-164">This attribute can be a number representing the task module's width in pixels, or `small`, `medium`, or `large`.</span></span> <span data-ttu-id="7df38-165">Para obtener más información, vea [task module sizing](#task-module-sizing).</span><span class="sxs-lookup"><span data-stu-id="7df38-165">For more information, see [task module sizing](#task-module-sizing).</span></span> |
| `url` | <span data-ttu-id="7df38-166">string</span><span class="sxs-lookup"><span data-stu-id="7df38-166">string</span></span> | <span data-ttu-id="7df38-167">Este atributo es la dirección URL de la página cargada como `<iframe>` dentro del módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="7df38-167">This attribute is the URL of the page loaded as an `<iframe>` inside the task module.</span></span> <span data-ttu-id="7df38-168">El dominio de la dirección URL debe estar en la matriz [validDomains](~/resources/schema/manifest-schema.md#validdomains) de la aplicación en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7df38-168">The URL's domain must be in the app's [validDomains array](~/resources/schema/manifest-schema.md#validdomains) in your app's manifest.</span></span> |
| `card` | <span data-ttu-id="7df38-169">Datos adjuntos de tarjeta adaptable o de bot de tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="7df38-169">Adaptive Card or Adaptive Card bot card attachment</span></span> | <span data-ttu-id="7df38-170">Este atributo es el JSON para que la tarjeta adaptable aparezca en el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="7df38-170">This attribute is the JSON for the Adaptive Card to appear in the task module.</span></span> <span data-ttu-id="7df38-171">Si el usuario invoca desde un bot, use el JSON de tarjeta adaptable en un objeto Bot `attachment` Framework.</span><span class="sxs-lookup"><span data-stu-id="7df38-171">If the user is invoking from a bot, use the Adaptive Card JSON in a Bot Framework `attachment` object.</span></span> <span data-ttu-id="7df38-172">Desde una pestaña, el usuario debe usar una tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="7df38-172">From a tab, the user must use an Adaptive Card.</span></span> <span data-ttu-id="7df38-173">Para obtener más información, consulte [Adaptive Card or Adaptive Card bot card attachment](#adaptive-card-or-adaptive-card-bot-card-attachment)</span><span class="sxs-lookup"><span data-stu-id="7df38-173">For more information, see [Adaptive Card or Adaptive Card bot card attachment](#adaptive-card-or-adaptive-card-bot-card-attachment)</span></span> |
| `fallbackUrl` | <span data-ttu-id="7df38-174">string</span><span class="sxs-lookup"><span data-stu-id="7df38-174">string</span></span> | <span data-ttu-id="7df38-175">Este atributo abre la dirección URL en una pestaña del explorador, si un cliente no admite la característica del módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="7df38-175">This attribute opens the URL in a browser tab, if a client does not support the task module feature.</span></span> |
| `completionBotId` | <span data-ttu-id="7df38-176">string</span><span class="sxs-lookup"><span data-stu-id="7df38-176">string</span></span> | <span data-ttu-id="7df38-177">Este atributo especifica un identificador de aplicación bot para enviar el resultado de la interacción del usuario con el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="7df38-177">This attribute specifies a bot App ID to send the result of the user's interaction with the task module.</span></span> <span data-ttu-id="7df38-178">Si se especifica, el bot recibe un `task/submit invoke` evento con un objeto JSON en la carga del evento.</span><span class="sxs-lookup"><span data-stu-id="7df38-178">If specified, the bot receives a `task/submit invoke` event with a JSON object in the event payload.</span></span> |

> [!NOTE]
> <span data-ttu-id="7df38-179">La característica del módulo de tareas requiere que los dominios de las direcciones URL que quiera cargar se incluyan en la matriz en el `validDomains` manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7df38-179">The task module feature requires that the domains of any URLs you want to load are included in the `validDomains` array in your app's manifest.</span></span>

<span data-ttu-id="7df38-180">En la siguiente sección se especifica el tamaño del módulo de tareas que permite al usuario establecer el alto y el ancho del módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="7df38-180">The next section specifies task module sizing that enables the user to set the height and width of the task module.</span></span>

## <a name="task-module-sizing"></a><span data-ttu-id="7df38-181">Tamaño del módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="7df38-181">Task module sizing</span></span>

<span data-ttu-id="7df38-182">El uso de enteros `TaskInfo.width` para y , establece el alto y el ancho del módulo de tareas en `TaskInfo.height` píxeles.</span><span class="sxs-lookup"><span data-stu-id="7df38-182">Using integers for `TaskInfo.width` and `TaskInfo.height`, sets the height and width of the task module in pixels.</span></span> <span data-ttu-id="7df38-183">Sin embargo, según el tamaño de la ventana y la resolución de pantalla del equipo, se reducen proporcionalmente mientras se mantiene la relación de aspecto que es de ancho o alto.</span><span class="sxs-lookup"><span data-stu-id="7df38-183">However, depending on the size of the Team's window and screen resolution they are reduced proportionally while maintaining the aspect ratio that is width or height.</span></span>

<span data-ttu-id="7df38-184">Si y son , o , el tamaño del rectángulo rojo de la siguiente imagen es una proporción del espacio `TaskInfo.width` `TaskInfo.height` `"small"` `"medium"` `"large"` disponible, 20%, 50% y 60% para y `width` 20%, 50% y 66% para `height` :</span><span class="sxs-lookup"><span data-stu-id="7df38-184">If `TaskInfo.width` and `TaskInfo.height` are `"small"`, `"medium"`, or `"large"`, the size of the red rectangle in the following image is a proportion of the available space, 20%, 50%, and 60% for `width` and 20%, 50%, and 66% for `height`:</span></span>

![Ejemplo del módulo de tareas](~/assets/images/task-module/task-module-example.png)

<span data-ttu-id="7df38-186">Los módulos de tareas invocados desde una pestaña se pueden cambiar dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="7df38-186">Task modules invoked from a tab can be dynamically resized.</span></span> <span data-ttu-id="7df38-187">Después de llamar, puede llamar a donde las propiedades height y width del objeto newSize se ajustan a la especificación `tasks.startTask()` `tasks.updateTask(newSize)` TaskInfo, por ejemplo `{ height: 'medium', width: 'medium' }` .</span><span class="sxs-lookup"><span data-stu-id="7df38-187">After calling `tasks.startTask()` you can call `tasks.updateTask(newSize)` where height and width properties on the newSize object conform to the TaskInfo specification, for example `{ height: 'medium', width: 'medium' }`.</span></span>

<span data-ttu-id="7df38-188">En la siguiente sección se proporcionan ejemplos de la inserción de módulos de tareas en un vídeo de YouTube y una PowerApp.</span><span class="sxs-lookup"><span data-stu-id="7df38-188">The next section provides examples of embedding task modules in a YouTube video and a PowerApp.</span></span>

## <a name="task-module-css-for-html-or-javascript-task-modules"></a><span data-ttu-id="7df38-189">CSS del módulo de tareas para módulos de tareas HTML o JavaScript</span><span class="sxs-lookup"><span data-stu-id="7df38-189">Task module CSS for HTML or JavaScript task modules</span></span>

<span data-ttu-id="7df38-190">Los módulos de tareas basados en HTML o JavaScript tienen acceso a todo el área del módulo de tareas debajo del encabezado.</span><span class="sxs-lookup"><span data-stu-id="7df38-190">HTML or JavaScript-based task modules have access to the entire area of the task module below the header.</span></span> <span data-ttu-id="7df38-191">Aunque eso ofrece una gran flexibilidad, si desea que el relleno alrededor de los bordes se alinee con los elementos de encabezado y evite barras de desplazamiento innecesarias, el usuario debe proporcionar el CSS correcto.</span><span class="sxs-lookup"><span data-stu-id="7df38-191">While that offers a great deal of flexibility, if you want padding around the edges to align with the header elements and avoid unnecessary scroll bars, the user must provide the right CSS.</span></span> <span data-ttu-id="7df38-192">Las secciones siguientes proporcionan algunos ejemplos para algunos casos de uso.</span><span class="sxs-lookup"><span data-stu-id="7df38-192">The next sections provide some examples for a few use cases.</span></span>

<span data-ttu-id="7df38-193">**Ejemplo 1: Vídeo de YouTube**</span><span class="sxs-lookup"><span data-stu-id="7df38-193">**Example 1: YouTube video**</span></span>

<span data-ttu-id="7df38-194">YouTube ofrece la posibilidad de insertar vídeos en páginas web.</span><span class="sxs-lookup"><span data-stu-id="7df38-194">YouTube offers the ability to embed videos on web pages.</span></span> <span data-ttu-id="7df38-195">Es fácil insertar vídeos en páginas web en un módulo de tareas mediante una página web de código auxiliar simple.</span><span class="sxs-lookup"><span data-stu-id="7df38-195">It is easy to embed videos on web pages in a task module using a simple stub web page.</span></span>

![Vídeo de YouTube](~/assets/images/task-module/youtube-example.png)

<span data-ttu-id="7df38-197">El código siguiente proporciona un ejemplo de HTML para la página web sin css:</span><span class="sxs-lookup"><span data-stu-id="7df38-197">The following code provides an example of the HTML for the web page without the CSS:</span></span>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  ⋮
</head>
<body>
  <div id="embed-container">
    <iframe width="1000" height="700" src="https://www.youtube.com/embed/rd0Rd8w3FZ0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen=""></iframe>
  </div>
</body>
</html>
```

<span data-ttu-id="7df38-198">El código siguiente proporciona un ejemplo de CSS:</span><span class="sxs-lookup"><span data-stu-id="7df38-198">The following code provides an example of the CSS:</span></span>

```css
#embed-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 95%;
    height: 95%;
    padding-left: 20px;
    padding-right: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    border-style: none;
}
```

<span data-ttu-id="7df38-199">**Ejemplo 2: PowerApp**</span><span class="sxs-lookup"><span data-stu-id="7df38-199">**Example 2: PowerApp**</span></span>

<span data-ttu-id="7df38-200">El usuario también puede usar el mismo enfoque para insertar una PowerApp.</span><span class="sxs-lookup"><span data-stu-id="7df38-200">The user can use the same approach to embed a PowerApp as well.</span></span> <span data-ttu-id="7df38-201">Como el alto o el ancho de cualquier PowerApp individual es personalizable, el usuario puede ajustar el alto y el ancho para lograr la presentación deseada.</span><span class="sxs-lookup"><span data-stu-id="7df38-201">As the height or width of any individual PowerApp is customizable, the user can adjust the height and width to achieve the desired presentation.</span></span>

![PowerApp de administración de activos](~/assets/images/task-module/powerapp-example.png)

<span data-ttu-id="7df38-203">El código siguiente proporciona un ejemplo de HTML para PowerApp:</span><span class="sxs-lookup"><span data-stu-id="7df38-203">The following code provides an example of the HTML for PowerApp:</span></span>

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

<span data-ttu-id="7df38-204">El código siguiente proporciona un ejemplo de CSS:</span><span class="sxs-lookup"><span data-stu-id="7df38-204">The following code provides an example of the CSS:</span></span>

```css
#embed-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 94%;
    height: 95%;
    padding-left: 20px;
    padding-right: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    border-style: none;
}
```

<span data-ttu-id="7df38-205">En la siguiente sección se proporcionan detalles sobre cómo invocar la tarjeta mediante datos adjuntos de tarjeta adaptable o de bot de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="7df38-205">The next section provides details on invoking your card using Adaptive Card or Adaptive Card bot card attachment.</span></span>

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a><span data-ttu-id="7df38-206">Datos adjuntos de tarjeta adaptable o de bot de tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="7df38-206">Adaptive Card or Adaptive Card bot card attachment</span></span>

<span data-ttu-id="7df38-207">Dependiendo de cómo invoje su , debe usar una tarjeta adaptable o un archivo adjunto de tarjeta bot de tarjeta adaptable, que es una tarjeta adaptable envuelta `card` en un objeto de datos adjuntos.</span><span class="sxs-lookup"><span data-stu-id="7df38-207">Depending on how you are invoking your `card`, you must use either an Adaptive Card or an Adaptive Card bot card attachment, which is an Adaptive Card wrapped in an attachment object.</span></span>

<span data-ttu-id="7df38-208">Cuando se invoca desde una pestaña, el usuario debe usar una tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="7df38-208">When you are invoking from a tab, the user must use an Adaptive Card.</span></span>

<span data-ttu-id="7df38-209">El código siguiente proporciona un ejemplo de una tarjeta adaptable:</span><span class="sxs-lookup"><span data-stu-id="7df38-209">The following code provides an example of an Adaptive Card:</span></span>

```json
{
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
}
```

<span data-ttu-id="7df38-210">El código siguiente proporciona un ejemplo de datos adjuntos de una tarjeta bot de tarjeta adaptable cuando se invoca desde un bot:</span><span class="sxs-lookup"><span data-stu-id="7df38-210">The following code provides an example of an Adaptive Card bot card attachment when you are invoking from a bot:</span></span>

```json
{
    "contentType": "application/vnd.microsoft.card.adaptive",
    "content": {
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
    }
}
```

<span data-ttu-id="7df38-211">En la siguiente sección se proporcionan detalles sobre la sintaxis de vínculo profundo del módulo de tareas, `TaskInfo` incluidos el objeto `APP_ID` y `BOT_APP_ID` .</span><span class="sxs-lookup"><span data-stu-id="7df38-211">The next section provides details on task module deep link syntax including the `TaskInfo` object and `APP_ID` and `BOT_APP_ID`.</span></span>

## <a name="task-module-deep-link-syntax"></a><span data-ttu-id="7df38-212">Sintaxis de vínculo profundo del módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="7df38-212">Task module deep link syntax</span></span>

<span data-ttu-id="7df38-213">Un vínculo profundo del módulo de tareas es una serialización del objeto TaskInfo con los otros dos detalles siguientes, y `APP_ID` opcionalmente: `BOT_APP_ID`</span><span class="sxs-lookup"><span data-stu-id="7df38-213">A task module deep link is a serialization of the TaskInfo object with the following two other details, `APP_ID` and optionally the `BOT_APP_ID`:</span></span>

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

<span data-ttu-id="7df38-214">Para los tipos de datos y los valores permitidos para `<TaskInfo.url>` , , , y , vea `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` `<TaskInfo.title>` [TaskInfo (objeto).](#the-taskinfo-object)</span><span class="sxs-lookup"><span data-stu-id="7df38-214">For the data types and allowable values for `<TaskInfo.url>`, `<TaskInfo.card>`, `<TaskInfo.height>`, `<TaskInfo.width>`, and `<TaskInfo.title>`, see [TaskInfo object](#the-taskinfo-object).</span></span>

> [!TIP]
> <span data-ttu-id="7df38-215">La dirección URL codifica el vínculo profundo al usar el `card` parámetro, por ejemplo, la función de [ `encodeURI()` JavaScript](https://www.w3schools.com/jsref/jsref_encodeURI.asp).</span><span class="sxs-lookup"><span data-stu-id="7df38-215">URL encode the deep link when using the `card` parameter, for example, JavaScript's [`encodeURI()` function](https://www.w3schools.com/jsref/jsref_encodeURI.asp).</span></span>

<span data-ttu-id="7df38-216">En la tabla siguiente se proporciona información `APP_ID` sobre `BOT_APP_ID` y :</span><span class="sxs-lookup"><span data-stu-id="7df38-216">The following table provides information on `APP_ID` and `BOT_APP_ID`:</span></span>

| <span data-ttu-id="7df38-217">Valor</span><span class="sxs-lookup"><span data-stu-id="7df38-217">Value</span></span> | <span data-ttu-id="7df38-218">Tipo</span><span class="sxs-lookup"><span data-stu-id="7df38-218">Type</span></span> | <span data-ttu-id="7df38-219">Necesario</span><span class="sxs-lookup"><span data-stu-id="7df38-219">Required</span></span> | <span data-ttu-id="7df38-220">Descripción</span><span class="sxs-lookup"><span data-stu-id="7df38-220">Description</span></span> |
| --- | --- | --- | --- |
| `APP_ID` | <span data-ttu-id="7df38-221">string</span><span class="sxs-lookup"><span data-stu-id="7df38-221">string</span></span> | <span data-ttu-id="7df38-222">Sí</span><span class="sxs-lookup"><span data-stu-id="7df38-222">Yes</span></span> | <span data-ttu-id="7df38-223">El [identificador](~/resources/schema/manifest-schema.md#id) de la aplicación que invoca el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="7df38-223">The [ID](~/resources/schema/manifest-schema.md#id) of the app invoking the task module.</span></span> <span data-ttu-id="7df38-224">La [matriz validDomains](~/resources/schema/manifest-schema.md#validdomains) del manifiesto `APP_ID` para debe contener el dominio para if está en la dirección `url` `url` URL.</span><span class="sxs-lookup"><span data-stu-id="7df38-224">The [validDomains array](~/resources/schema/manifest-schema.md#validdomains) in the manifest for `APP_ID` must contain the domain for `url` if `url` is in the URL.</span></span> <span data-ttu-id="7df38-225">El identificador de la aplicación ya se conoce cuando se invoca un módulo de tareas desde una pestaña o un bot, por lo que no se incluye en `TaskInfo` .</span><span class="sxs-lookup"><span data-stu-id="7df38-225">The app ID is already known when a task module is invoked from a tab or a bot, which is why it is not included in `TaskInfo`.</span></span> |
| `BOT_APP_ID` | <span data-ttu-id="7df38-226">string</span><span class="sxs-lookup"><span data-stu-id="7df38-226">string</span></span> | <span data-ttu-id="7df38-227">No</span><span class="sxs-lookup"><span data-stu-id="7df38-227">No</span></span> | <span data-ttu-id="7df38-228">Si se especifica `completionBotId` un valor para, el `result` objeto se envía mediante un mensaje al bot `task/submit invoke` especificado.</span><span class="sxs-lookup"><span data-stu-id="7df38-228">If a value for `completionBotId` is specified, the `result` object is sent using a `task/submit invoke` message to the specified bot.</span></span> <span data-ttu-id="7df38-229">`BOT_APP_ID` debe especificarse como bot en el manifiesto de la aplicación, es decir, no se puede enviar a ningún bot.</span><span class="sxs-lookup"><span data-stu-id="7df38-229">`BOT_APP_ID` must be specified as a bot in the app's manifest, that is you cannot send it to any bot.</span></span> |

> [!NOTE]
> <span data-ttu-id="7df38-230">`APP_ID` y puede ser lo mismo en muchos casos, si una aplicación tiene un bot recomendado para usarlo como id. de una `BOT_APP_ID` aplicación si la hay.</span><span class="sxs-lookup"><span data-stu-id="7df38-230">`APP_ID` and `BOT_APP_ID` can be the same in many cases, if an app has a recommended bot to use as an app's ID if there is one.</span></span>

<span data-ttu-id="7df38-231">En la siguiente sección se proporcionan detalles sobre cómo usar un teclado con el módulo de tareas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7df38-231">The next section provides details on using a keyboard with your app's task module.</span></span>

## <a name="keyboard-and-accessibility-guidelines"></a><span data-ttu-id="7df38-232">Directrices de teclado y accesibilidad</span><span class="sxs-lookup"><span data-stu-id="7df38-232">Keyboard and accessibility guidelines</span></span>

<span data-ttu-id="7df38-233">Con módulos de tareas basados en HTML o JavaScript, debes asegurarte de que el módulo de tareas de la aplicación se pueda usar con un teclado.</span><span class="sxs-lookup"><span data-stu-id="7df38-233">With HTML or JavaScript-based task modules, you must ensure your app's task module can be used with a keyboard.</span></span> <span data-ttu-id="7df38-234">Los programas de lector de pantalla también dependen de la capacidad de navegar con el teclado.</span><span class="sxs-lookup"><span data-stu-id="7df38-234">Screen reader programs also depend on the ability to navigate using the keyboard.</span></span> <span data-ttu-id="7df38-235">Esto incluye las dos cosas siguientes:</span><span class="sxs-lookup"><span data-stu-id="7df38-235">This includes the following two things:</span></span>

* <span data-ttu-id="7df38-236">Usar el [atributo tabindex en](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) las etiquetas HTML para controlar qué elementos se pueden centrar.</span><span class="sxs-lookup"><span data-stu-id="7df38-236">Using the [tabindex attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) in your HTML tags to control which elements can be focused.</span></span> <span data-ttu-id="7df38-237">Además, usa el atributo tabindex para identificar dónde participa en la navegación secuencial del teclado normalmente con las teclas <kbd>Tab</kbd> y <kbd>Mayús-Tab.</kbd></span><span class="sxs-lookup"><span data-stu-id="7df38-237">Also, use tabindex attribute to identify where it participates in sequential keyboard navigation usually with the <kbd>Tab</kbd> and <kbd>Shift-Tab</kbd> keys.</span></span>
* <span data-ttu-id="7df38-238">Control de <kbd>la clave Esc</kbd> en JavaScript para el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="7df38-238">Handling the <kbd>Esc</kbd> key in the JavaScript for your task module.</span></span> <span data-ttu-id="7df38-239">El código siguiente proporciona un ejemplo de cómo controlar la <kbd>clave Esc:</kbd></span><span class="sxs-lookup"><span data-stu-id="7df38-239">The following code provides an example of how to handle the <kbd>Esc</kbd> key:</span></span>

    ```javascript
    // Handle the Esc key
    document.onkeyup = function(event) {
    if ((event.key === 27) || (event.key === "Escape")) {
      microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
      }
    }
    ```

<span data-ttu-id="7df38-240">Microsoft Teams garantiza que la navegación por teclado funciona correctamente desde el encabezado del módulo de tareas al HTML y viceversa.</span><span class="sxs-lookup"><span data-stu-id="7df38-240">Microsoft Teams ensures that keyboard navigation works properly from the task module header into your HTML and vice-versa.</span></span>

## <a name="code-sample"></a><span data-ttu-id="7df38-241">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="7df38-241">Code sample</span></span>

|<span data-ttu-id="7df38-242">Nombre de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7df38-242">Sample name</span></span> | <span data-ttu-id="7df38-243">Descripción</span><span class="sxs-lookup"><span data-stu-id="7df38-243">Description</span></span> | <span data-ttu-id="7df38-244">.NET</span><span class="sxs-lookup"><span data-stu-id="7df38-244">.NET</span></span> | <span data-ttu-id="7df38-245">Node.js</span><span class="sxs-lookup"><span data-stu-id="7df38-245">Node.js</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="7df38-246">Bots de ejemplo de módulo de tareas-V4</span><span class="sxs-lookup"><span data-stu-id="7df38-246">Task module sample bots-V4</span></span> | <span data-ttu-id="7df38-247">Ejemplos para crear módulos de tareas.</span><span class="sxs-lookup"><span data-stu-id="7df38-247">Samples for creating task modules.</span></span> |[<span data-ttu-id="7df38-248">View</span><span class="sxs-lookup"><span data-stu-id="7df38-248">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[<span data-ttu-id="7df38-249">View</span><span class="sxs-lookup"><span data-stu-id="7df38-249">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|
|<span data-ttu-id="7df38-250">Fichas de ejemplo del módulo de tareas y bots-V3</span><span class="sxs-lookup"><span data-stu-id="7df38-250">Task module sample tabs and bots-V3</span></span> | <span data-ttu-id="7df38-251">Ejemplos para crear módulos de tareas.</span><span class="sxs-lookup"><span data-stu-id="7df38-251">Samples for creating task modules.</span></span> |[<span data-ttu-id="7df38-252">View</span><span class="sxs-lookup"><span data-stu-id="7df38-252">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[<span data-ttu-id="7df38-253">View</span><span class="sxs-lookup"><span data-stu-id="7df38-253">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 

## <a name="see-also"></a><span data-ttu-id="7df38-254">Vea también</span><span class="sxs-lookup"><span data-stu-id="7df38-254">See also</span></span>

* [<span data-ttu-id="7df38-255">Solicitar permisos de dispositivo</span><span class="sxs-lookup"><span data-stu-id="7df38-255">Request device permissions</span></span>](~/concepts/device-capabilities/native-device-permissions.md)
* [<span data-ttu-id="7df38-256">Integrar capacidades multimedia</span><span class="sxs-lookup"><span data-stu-id="7df38-256">Integrate media capabilities</span></span>](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [<span data-ttu-id="7df38-257">Integrar la funcionalidad de escáner de códigos QR o códigos de barras en Teams</span><span class="sxs-lookup"><span data-stu-id="7df38-257">Integrate QR or barcode scanner capability in Teams</span></span>](~/concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [<span data-ttu-id="7df38-258">Integrar las capacidades de ubicación en Teams</span><span class="sxs-lookup"><span data-stu-id="7df38-258">Integrate location capabilities in Teams</span></span>](~/concepts/device-capabilities/location-capability.md)

## <a name="next-step"></a><span data-ttu-id="7df38-259">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="7df38-259">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7df38-260">Usar módulos de tareas en pestañas</span><span class="sxs-lookup"><span data-stu-id="7df38-260">Use task modules in tabs</span></span>](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
---
title: Usar módulos de tareas en Microsoft Teams pestañas
description: Explica cómo invocar módulos de tareas desde Teams pestañas mediante el SDK Microsoft Teams cliente.
localization_priority: Normal
ms.topic: how-to
keywords: sdk de cliente de pestañas de teams de módulos de tareas
ms.openlocfilehash: 8afd2c93261f28aa7ced4c98d29be27dca35f8b1
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140558"
---
# <a name="use-task-modules-in-tabs"></a><span data-ttu-id="4e06b-104">Usar módulos de tareas en pestañas</span><span class="sxs-lookup"><span data-stu-id="4e06b-104">Use task modules in tabs</span></span>

<span data-ttu-id="4e06b-105">Agregue un módulo de tareas a la pestaña para simplificar la experiencia del usuario para los flujos de trabajo que requieran entrada de datos.</span><span class="sxs-lookup"><span data-stu-id="4e06b-105">Add a task module to your tab to simplify your user's experience for any workflows that require data input.</span></span> <span data-ttu-id="4e06b-106">Los módulos de tareas permiten recopilar sus entradas en una ventana emergente Teams-Aware Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4e06b-106">Task modules allow you to gather their input in a Microsoft Teams-Aware pop-up.</span></span> <span data-ttu-id="4e06b-107">Un buen ejemplo de esto es la edición de tarjetas planner.</span><span class="sxs-lookup"><span data-stu-id="4e06b-107">A good example of this is editing Planner cards.</span></span> <span data-ttu-id="4e06b-108">Puede usar módulos de tareas para crear una experiencia similar.</span><span class="sxs-lookup"><span data-stu-id="4e06b-108">You can use task modules to create a similar experience.</span></span>

<span data-ttu-id="4e06b-109">Para admitir la característica de módulo de tareas, se agregan dos nuevas funciones al SDK Teams [cliente](/javascript/api/overview/msteams-client).</span><span class="sxs-lookup"><span data-stu-id="4e06b-109">To support the task module feature, two new functions are added to the [Teams client SDK](/javascript/api/overview/msteams-client).</span></span> <span data-ttu-id="4e06b-110">El código siguiente muestra un ejemplo de estas dos funciones:</span><span class="sxs-lookup"><span data-stu-id="4e06b-110">The following code shows an example of these two functions:</span></span>

```typescript
microsoftTeams.tasks.startTask(
    taskInfo: TaskInfo,
    submitHandler?: (err: string, result: string | any) => void
): void;

microsoftTeams.tasks.submitTask(
    result?: string | any,
    appIds?: string | string[]
): void;
```

<span data-ttu-id="4e06b-111">Puede ver cómo funciona invocar un módulo de tareas desde una pestaña y enviar el resultado de un módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="4e06b-111">You can see how invoking a task module from a tab and submitting the result of a task module works.</span></span>

## <a name="invoke-a-task-module-from-a-tab"></a><span data-ttu-id="4e06b-112">Invocar un módulo de tareas desde una pestaña</span><span class="sxs-lookup"><span data-stu-id="4e06b-112">Invoke a task module from a tab</span></span>

<span data-ttu-id="4e06b-113">Para invocar un módulo de tarea desde una pestaña, use `microsoftTeams.tasks.startTask()` pasar un [objeto TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) y una función `submitHandler` de devolución de llamada opcional.</span><span class="sxs-lookup"><span data-stu-id="4e06b-113">To invoke a task module from a tab use `microsoftTeams.tasks.startTask()` passing a [TaskInfo object](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) and an optional `submitHandler` callback function.</span></span> <span data-ttu-id="4e06b-114">Hay dos casos a tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="4e06b-114">There are two cases to consider:</span></span>

* <span data-ttu-id="4e06b-115">El valor de `TaskInfo.url` se establece en una dirección URL.</span><span class="sxs-lookup"><span data-stu-id="4e06b-115">The value of `TaskInfo.url` is set to a URL.</span></span> <span data-ttu-id="4e06b-116">La ventana del módulo de tareas aparece `TaskModule.url` y se carga como dentro de `<iframe>` ella.</span><span class="sxs-lookup"><span data-stu-id="4e06b-116">The task module window appears and `TaskModule.url` is loaded as an `<iframe>` inside it.</span></span> <span data-ttu-id="4e06b-117">JavaScript en esa página llama `microsoftTeams.initialize()` a .</span><span class="sxs-lookup"><span data-stu-id="4e06b-117">JavaScript on that page calls `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="4e06b-118">Si hay una función en la página y hay un error al invocar , se invoca con set en la cadena `submitHandler` de error que indica lo `microsoftTeams.tasks.startTask()` `submitHandler` `err` mismo.</span><span class="sxs-lookup"><span data-stu-id="4e06b-118">If there is a `submitHandler` function on the page and there is an error when invoking `microsoftTeams.tasks.startTask()`, then `submitHandler` is invoked with `err` set to the error string indicating the same.</span></span> <span data-ttu-id="4e06b-119">Para obtener más información, vea [errores de invocación del módulo de tareas](#task-module-invocation-errors).</span><span class="sxs-lookup"><span data-stu-id="4e06b-119">For more information, see [task module invocation errors](#task-module-invocation-errors).</span></span>
* <span data-ttu-id="4e06b-120">El valor de `taskInfo.card` es el JSON de una tarjeta [adaptable](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span><span class="sxs-lookup"><span data-stu-id="4e06b-120">The value of `taskInfo.card` is the [JSON for an Adaptive Card](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span></span> <span data-ttu-id="4e06b-121">No hay ninguna función de JavaScript a la que llamar cuando el usuario cierra o `submitHandler` presiona un botón en la tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="4e06b-121">There is no JavaScript `submitHandler` function to call when the user closes or presses a button on the Adaptive Card.</span></span> <span data-ttu-id="4e06b-122">La única forma de recibir lo que el usuario ha escrito es pasando el resultado a un bot.</span><span class="sxs-lookup"><span data-stu-id="4e06b-122">The only way to receive what the user entered is by passing the result to a bot.</span></span> <span data-ttu-id="4e06b-123">Para usar un módulo de tareas de tarjeta adaptable desde una pestaña, la aplicación debe incluir un bot para obtener cualquier respuesta del usuario.</span><span class="sxs-lookup"><span data-stu-id="4e06b-123">To use an Adaptive Card task module from a tab, your app must include a bot to get any response from the user.</span></span>

<span data-ttu-id="4e06b-124">En la siguiente sección se muestra un ejemplo de invocar un módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="4e06b-124">The next section gives an example of invoking a task module.</span></span>

## <a name="example-of-invoking-a-task-module"></a><span data-ttu-id="4e06b-125">Ejemplo de invocar un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="4e06b-125">Example of invoking a task module</span></span>

<span data-ttu-id="4e06b-126">En la siguiente imagen se muestra el módulo de tareas:</span><span class="sxs-lookup"><span data-stu-id="4e06b-126">The following image displays the task module:</span></span>

![Módulo de tareas: formulario personalizado](~/assets/images/task-module/task-module-custom-form.png)

<span data-ttu-id="4e06b-128">El siguiente código se adapta del [ejemplo del módulo de tareas:](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample)</span><span class="sxs-lookup"><span data-stu-id="4e06b-128">The following code is adapted from [the task module sample](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample):</span></span>

```javascript
let taskInfo = {
    title: null,
    height: null,
    width: null,
    url: null,
    card: null,
    fallbackUrl: null,
    completionBotId: null,
};

taskInfo.url = "https://contoso.com/teamsapp/customform";
taskInfo.title = "Custom Form";
taskInfo.height = 510;
taskInfo.width = 430;
submitHandler = (err, result) => {
    console.log(`Submit handler - err: ${err}`);
    console.log(`Submit handler - result\rName: ${result.name}\rEmail: ${result.email}\rFavorite book: ${result.favoriteBook}`);
};
microsoftTeams.tasks.startTask(taskInfo, submitHandler);
```

<span data-ttu-id="4e06b-129">El `submitHandler` es muy simple y hace eco del valor de o de la `err` `result` consola.</span><span class="sxs-lookup"><span data-stu-id="4e06b-129">The `submitHandler` is very simple and it echoes the value of `err` or `result` to the console.</span></span>

## <a name="submit-the-result-of-a-task-module"></a><span data-ttu-id="4e06b-130">Enviar el resultado de un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="4e06b-130">Submit the result of a task module</span></span>

<span data-ttu-id="4e06b-131">La `submitHandler` función reside en la página web y se usa con `TaskInfo.url` `TaskInfo.url` .</span><span class="sxs-lookup"><span data-stu-id="4e06b-131">The `submitHandler` function resides in the `TaskInfo.url` web page and is used with `TaskInfo.url`.</span></span> <span data-ttu-id="4e06b-132">Si hay un error al invocar el módulo de tareas, la función se invoca inmediatamente con una `submitHandler` cadena que indica qué error se `err` [produjo](#task-module-invocation-errors).</span><span class="sxs-lookup"><span data-stu-id="4e06b-132">If there is an error when invoking the task module, your `submitHandler` function is immediately invoked with an `err` string indicating what [error occurred](#task-module-invocation-errors).</span></span> <span data-ttu-id="4e06b-133">También se llama a la función con una cadena cuando el usuario selecciona X en la esquina superior derecha del módulo de tareas `submitHandler` `err` para cerrarla.</span><span class="sxs-lookup"><span data-stu-id="4e06b-133">The `submitHandler` function is also called with an `err` string when the user selects X at the upper right of the task module to close it.</span></span>

<span data-ttu-id="4e06b-134">Si no hay ningún error de invocación y el usuario no selecciona X para descartarlo, el usuario elige un botón cuando finaliza.</span><span class="sxs-lookup"><span data-stu-id="4e06b-134">If there is no invocation error and the user does not select X to dismiss it, the user chooses a button when finished.</span></span> <span data-ttu-id="4e06b-135">Según si se trata de una dirección URL o una tarjeta adaptable en el módulo de tareas, las siguientes secciones proporcionan detalles sobre lo que ocurre.</span><span class="sxs-lookup"><span data-stu-id="4e06b-135">Depending on whether it is a URL or an Adaptive Card in the task module, the next sections provide details on what occurs.</span></span>

### <a name="html-or-javascript-taskinfourl"></a><span data-ttu-id="4e06b-136">HTML o JavaScript `TaskInfo.url`</span><span class="sxs-lookup"><span data-stu-id="4e06b-136">HTML or JavaScript `TaskInfo.url`</span></span>

<span data-ttu-id="4e06b-137">Después de validar las entradas del usuario, llame a la `microsoftTeams.tasks.submitTask()` función SDK denominada `submitTask()` .</span><span class="sxs-lookup"><span data-stu-id="4e06b-137">After validating the user's inputs, call the `microsoftTeams.tasks.submitTask()` SDK function referred to as `submitTask()`.</span></span> <span data-ttu-id="4e06b-138">Llame `submitTask()` sin ningún parámetro si solo desea Teams cerrar el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="4e06b-138">Call `submitTask()` without any parameters if you just want Teams to close the task module.</span></span> <span data-ttu-id="4e06b-139">Puede pasar un objeto o una cadena a `submitHandler` su .</span><span class="sxs-lookup"><span data-stu-id="4e06b-139">You can pass an object or a string to your `submitHandler`.</span></span>

<span data-ttu-id="4e06b-140">Pase el resultado como primer parámetro.</span><span class="sxs-lookup"><span data-stu-id="4e06b-140">Pass your result as the first parameter.</span></span> <span data-ttu-id="4e06b-141">Teams invoca dónde `submitHandler` `err` es y es el objeto o cadena que pasó a `null` `result` `submitTask()` .</span><span class="sxs-lookup"><span data-stu-id="4e06b-141">Teams invokes `submitHandler` where `err` is `null` and `result` is the object or string you passed to `submitTask()`.</span></span> <span data-ttu-id="4e06b-142">Si llama `submitTask()` con un `result` parámetro, debe pasar una o una `appId` matriz de `appId` cadenas.</span><span class="sxs-lookup"><span data-stu-id="4e06b-142">If you call `submitTask()` with a `result` parameter, you must pass an `appId` or an array of `appId` strings.</span></span> <span data-ttu-id="4e06b-143">Esto permite Teams validar que la aplicación que envía el resultado es la misma que el módulo de tareas invocado.</span><span class="sxs-lookup"><span data-stu-id="4e06b-143">This permits Teams to validate that the app sending the result is same as the invoked task module.</span></span>

### <a name="adaptive-card-taskinfocard"></a><span data-ttu-id="4e06b-144">Tarjeta adaptable `TaskInfo.card`</span><span class="sxs-lookup"><span data-stu-id="4e06b-144">Adaptive Card `TaskInfo.card`</span></span>

<span data-ttu-id="4e06b-145">Al invocar el módulo de tareas con a y el usuario selecciona un botón, los valores de la tarjeta se devuelven `submitHandler` como el valor de `Action.Submit` `result` .</span><span class="sxs-lookup"><span data-stu-id="4e06b-145">When you invoke the task module with a `submitHandler` and the user selects an `Action.Submit` button, the values in the card are returned as the value of `result`.</span></span> <span data-ttu-id="4e06b-146">Si el usuario selecciona la tecla Esc o X en la parte superior derecha, `err` se devuelve en su lugar.</span><span class="sxs-lookup"><span data-stu-id="4e06b-146">If the user selects the Esc key or X at the top right, `err` is returned instead.</span></span> <span data-ttu-id="4e06b-147">Si la aplicación contiene un bot además de una pestaña, simplemente puedes incluir el bot como el `appId` valor `completionBotId` del `TaskInfo` objeto.</span><span class="sxs-lookup"><span data-stu-id="4e06b-147">If your app contains a bot in addition to a tab, you can simply include the `appId` of the bot as the value of `completionBotId` in the `TaskInfo` object.</span></span> <span data-ttu-id="4e06b-148">El cuerpo de la tarjeta adaptable tal como lo rellena el usuario se envía al bot mediante un mensaje cuando el usuario `task/submit invoke` selecciona un `Action.Submit` botón.</span><span class="sxs-lookup"><span data-stu-id="4e06b-148">The Adaptive Card body as filled in by the user is sent to the bot using a `task/submit invoke` message when the user selects an `Action.Submit` button.</span></span> <span data-ttu-id="4e06b-149">El esquema del objeto que recibe es muy similar al esquema que recibe para los mensajes [task/fetch y task/submit](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span><span class="sxs-lookup"><span data-stu-id="4e06b-149">The schema for the object you receive is very similar to [the schema you receive for task/fetch and task/submit messages](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span></span> <span data-ttu-id="4e06b-150">La única diferencia es que el esquema del objeto JSON es un objeto Adaptive Card en lugar de un objeto que contiene un objeto Adaptive Card como cuando se usan [tarjetas adaptables](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)con bots .</span><span class="sxs-lookup"><span data-stu-id="4e06b-150">The only difference is that the schema of the JSON object is an Adaptive Card object as opposed to an object containing an Adaptive Card object as [when Adaptive cards are used with bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span></span>

<span data-ttu-id="4e06b-151">En la siguiente sección se muestra un ejemplo de envío del resultado de un módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="4e06b-151">The next section gives an example of submitting the result of a task module.</span></span>

## <a name="example-of-submitting-the-result-of-a-task-module"></a><span data-ttu-id="4e06b-152">Ejemplo de envío del resultado de un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="4e06b-152">Example of submitting the result of a task module</span></span>

<span data-ttu-id="4e06b-153">Para obtener más información, vea el [formulario HTML en el módulo de tareas](#example-of-invoking-a-task-module).</span><span class="sxs-lookup"><span data-stu-id="4e06b-153">For more information, see the [HTML form in the task module](#example-of-invoking-a-task-module).</span></span> <span data-ttu-id="4e06b-154">En el siguiente código se muestra un ejemplo de dónde se define el formulario:</span><span class="sxs-lookup"><span data-stu-id="4e06b-154">The following code gives an example of where the form is defined:</span></span>

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

<span data-ttu-id="4e06b-155">Hay cinco campos en este formulario, pero para este ejemplo solo se requieren tres valores, `name` , `email` y `favoriteBook` .</span><span class="sxs-lookup"><span data-stu-id="4e06b-155">There are five fields on this form but for this example only three values are required, `name`, `email`, and `favoriteBook`.</span></span>

<span data-ttu-id="4e06b-156">El siguiente código proporciona un ejemplo de la `validateForm()` función que llama a `submitTask()` :</span><span class="sxs-lookup"><span data-stu-id="4e06b-156">The following code gives an example of the `validateForm()` function that calls `submitTask()`:</span></span>

```javascript
function validateForm() {
    var customerInfo = {
        name: document.forms["customerForm"]["name"].value,
        email: document.forms["customerForm"]["email"].value,
        favoriteBook: document.forms["customerForm"]["favoriteBook"].value
    }
    microsoftTeams.tasks.submitTask(customerInfo, "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx");
    return true;
}
```

<span data-ttu-id="4e06b-157">La siguiente sección proporciona problemas de invocación de módulo de tareas y sus mensajes de error.</span><span class="sxs-lookup"><span data-stu-id="4e06b-157">The next section provides task module invocation problems and their error messages.</span></span>

## <a name="task-module-invocation-errors"></a><span data-ttu-id="4e06b-158">Errores de invocación de módulos de tareas</span><span class="sxs-lookup"><span data-stu-id="4e06b-158">Task module invocation errors</span></span>

<span data-ttu-id="4e06b-159">En la tabla siguiente se proporcionan los valores posibles `err` que puede recibir su `submitHandler` :</span><span class="sxs-lookup"><span data-stu-id="4e06b-159">The following table provides the possible values of `err` that can be received by your `submitHandler`:</span></span>

| <span data-ttu-id="4e06b-160">Problema</span><span class="sxs-lookup"><span data-stu-id="4e06b-160">Problem</span></span> | <span data-ttu-id="4e06b-161">Mensaje de error que es el valor de `err`</span><span class="sxs-lookup"><span data-stu-id="4e06b-161">Error message that is value of `err`</span></span> |
| ------- | ------------------------------ |
| <span data-ttu-id="4e06b-162">Valores para ambos `TaskInfo.url` y `TaskInfo.card` se especificaron.</span><span class="sxs-lookup"><span data-stu-id="4e06b-162">Values for both `TaskInfo.url` and `TaskInfo.card` were specified.</span></span> | <span data-ttu-id="4e06b-163">Se especificaron valores para la tarjeta y la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="4e06b-163">Values for both card and URL were specified.</span></span> <span data-ttu-id="4e06b-164">Uno u otro, pero no ambos, están permitidos.</span><span class="sxs-lookup"><span data-stu-id="4e06b-164">One or the other, but not both, are allowed.</span></span> |
| <span data-ttu-id="4e06b-165">No `TaskInfo.url` se especifica ni se `TaskInfo.card` especifica.</span><span class="sxs-lookup"><span data-stu-id="4e06b-165">Neither `TaskInfo.url` nor `TaskInfo.card` specified.</span></span> | <span data-ttu-id="4e06b-166">Debe especificar un valor para la tarjeta o la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="4e06b-166">You must specify a value for either card or URL.</span></span> |
| <span data-ttu-id="4e06b-167">No es `appId` válido .</span><span class="sxs-lookup"><span data-stu-id="4e06b-167">Invalid `appId`.</span></span> | <span data-ttu-id="4e06b-168">Id. de aplicación no válido.</span><span class="sxs-lookup"><span data-stu-id="4e06b-168">Invalid app ID.</span></span> |
| <span data-ttu-id="4e06b-169">El usuario seleccionó el botón X y lo cerró.</span><span class="sxs-lookup"><span data-stu-id="4e06b-169">User selected X button, closing it.</span></span> | <span data-ttu-id="4e06b-170">El usuario canceló o cerró el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="4e06b-170">User cancelled or closed the task module.</span></span> |

## <a name="code-sample"></a><span data-ttu-id="4e06b-171">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="4e06b-171">Code sample</span></span>

|<span data-ttu-id="4e06b-172">Nombre de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4e06b-172">Sample name</span></span> | <span data-ttu-id="4e06b-173">Descripción</span><span class="sxs-lookup"><span data-stu-id="4e06b-173">Description</span></span> | <span data-ttu-id="4e06b-174">.NET</span><span class="sxs-lookup"><span data-stu-id="4e06b-174">.NET</span></span> | <span data-ttu-id="4e06b-175">Node.js</span><span class="sxs-lookup"><span data-stu-id="4e06b-175">Node.js</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="4e06b-176">Fichas de ejemplo del módulo de tareas y bots-V3</span><span class="sxs-lookup"><span data-stu-id="4e06b-176">Task module sample tabs and bots-V3</span></span> | <span data-ttu-id="4e06b-177">Ejemplos para crear módulos de tareas.</span><span class="sxs-lookup"><span data-stu-id="4e06b-177">Samples for creating task modules.</span></span> |[<span data-ttu-id="4e06b-178">View</span><span class="sxs-lookup"><span data-stu-id="4e06b-178">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[<span data-ttu-id="4e06b-179">View</span><span class="sxs-lookup"><span data-stu-id="4e06b-179">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 

## <a name="see-also"></a><span data-ttu-id="4e06b-180">Vea también</span><span class="sxs-lookup"><span data-stu-id="4e06b-180">See also</span></span>

[<span data-ttu-id="4e06b-181">Invocar y descartar módulos de tareas</span><span class="sxs-lookup"><span data-stu-id="4e06b-181">Invoke and dismiss task modules</span></span>](~/task-modules-and-cards/task-modules/invoking-task-modules.md)

## <a name="next-step"></a><span data-ttu-id="4e06b-182">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="4e06b-182">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4e06b-183">Uso de módulos de tareas desde bots</span><span class="sxs-lookup"><span data-stu-id="4e06b-183">Using task modules from bots</span></span>](~/task-modules-and-cards/task-modules/task-modules-bots.md)

---
title: Uso de módulos de tareas Microsoft Teams pestañas
description: Explica cómo invocar módulos de tareas desde Teams pestañas mediante el SDK Microsoft Teams cliente
localization_priority: Normal
ms.topic: how-to
keywords: sdk de cliente de pestañas de teams de módulos de tareas
ms.openlocfilehash: 5e85fd0662b8a15d6b98d9c2d2dfa5137b05fa39
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019527"
---
# <a name="using-task-modules-in-tabs"></a><span data-ttu-id="7fe6d-104">Uso de módulos de tareas en pestañas</span><span class="sxs-lookup"><span data-stu-id="7fe6d-104">Using task modules in tabs</span></span>

<span data-ttu-id="7fe6d-105">Agregar un módulo de tareas a la pestaña puede simplificar enormemente la experiencia del usuario para cualquier flujo de trabajo que requiera entrada de datos.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-105">Adding a task module to your tab can greatly simplify your user's experience for any workflows that require data input.</span></span> <span data-ttu-id="7fe6d-106">Los módulos de tareas permiten recopilar sus entradas en un Teams emergente que tenga en cuenta las tareas.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-106">Task modules allow you to gather their input in a Teams-aware popup.</span></span> <span data-ttu-id="7fe6d-107">Un buen ejemplo de esto es la edición de tarjetas planner; puede usar módulos de tareas para crear una experiencia similar.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-107">A good example of this is editing Planner cards; you can use task modules to create a similar experience.</span></span>

<span data-ttu-id="7fe6d-108">Para admitir la característica del módulo de tareas, se agregaron dos nuevas funciones al SDK Microsoft Teams [cliente:](/javascript/api/overview/msteams-client)</span><span class="sxs-lookup"><span data-stu-id="7fe6d-108">To support the task module feature, two new functions were added to the [Microsoft Teams client SDK](/javascript/api/overview/msteams-client):</span></span>

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

<span data-ttu-id="7fe6d-109">Veamos cómo funcionan cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-109">Let's see how each of them work.</span></span>

## <a name="invoking-a-task-module-from-a-tab"></a><span data-ttu-id="7fe6d-110">Invocar un módulo de tareas desde una pestaña</span><span class="sxs-lookup"><span data-stu-id="7fe6d-110">Invoking a task module from a tab</span></span>

<span data-ttu-id="7fe6d-111">Para invocar un módulo de tarea desde una pestaña, use `microsoftTeams.tasks.startTask()` pasar un [objeto TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) y una función `submitHandler` de devolución de llamada opcional.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-111">To invoke a task module from a tab use `microsoftTeams.tasks.startTask()` passing a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) and an optional `submitHandler` callback function.</span></span> <span data-ttu-id="7fe6d-112">Como se describió anteriormente, hay dos casos a tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="7fe6d-112">As described earlier, there are two cases to consider:</span></span>

1. <span data-ttu-id="7fe6d-113">El valor de `TaskInfo.url` se establece en una dirección URL.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-113">The value of `TaskInfo.url` is set to a URL.</span></span> <span data-ttu-id="7fe6d-114">La ventana del módulo de tareas aparece `TaskModule.url` y se carga como dentro de `<iframe>` ella.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-114">The task module window appears and `TaskModule.url` is loaded as an `<iframe>` inside it.</span></span> <span data-ttu-id="7fe6d-115">JavaScript en esa página debe llamar `microsoftTeams.initialize()` a .</span><span class="sxs-lookup"><span data-stu-id="7fe6d-115">JavaScript on that page should call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="7fe6d-116">Si hay una función en la página y hay un error al invocar , se invoca con set en la cadena de error que indica el error como se describe a `submitHandler` `microsoftTeams.tasks.startTask()` `submitHandler` `err` [continuación](#task-module-invocation-errors).</span><span class="sxs-lookup"><span data-stu-id="7fe6d-116">If there is a `submitHandler` function on the page and there is an error when invoking `microsoftTeams.tasks.startTask()`, then `submitHandler` is invoked with `err` set to the error string indicating the error as described [below](#task-module-invocation-errors).</span></span>
1. <span data-ttu-id="7fe6d-117">El valor de `taskInfo.card` es el JSON de una tarjeta [adaptable](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span><span class="sxs-lookup"><span data-stu-id="7fe6d-117">The value of `taskInfo.card` is the [JSON for an Adaptive card](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span></span> <span data-ttu-id="7fe6d-118">En este caso, obviamente, no hay ninguna función de JavaScript a la que llamar cuando el usuario cierra o presiona un botón en la tarjeta adaptable; la única forma de recibir lo que el usuario ha escrito es pasando el resultado a un `submitHandler` bot.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-118">In this case there's obviously not any JavaScript `submitHandler` function to call when the user closes or presses a button on the Adaptive card; the only way to receive what the user entered is by passing the result to a bot.</span></span> <span data-ttu-id="7fe6d-119">Para usar un módulo de tareas de tarjeta adaptable desde una pestaña, la aplicación debe incluir un bot para obtener información del usuario.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-119">To use an Adaptive card task module from a tab your app must include a bot to get any information back from the user.</span></span> <span data-ttu-id="7fe6d-120">Esto se explica a continuación.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-120">This is explained below.</span></span>

## <a name="example-invoking-a-task-module"></a><span data-ttu-id="7fe6d-121">Ejemplo: Invocar un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="7fe6d-121">Example: Invoking a task module</span></span>

<span data-ttu-id="7fe6d-122">El código siguiente se adapta del [ejemplo de módulo de tareas](~/task-modules-and-cards/what-are-task-modules.md#code-sample).</span><span class="sxs-lookup"><span data-stu-id="7fe6d-122">The code below is adapted from [the task module sample](~/task-modules-and-cards/what-are-task-modules.md#code-sample).</span></span> <span data-ttu-id="7fe6d-123">Este es el aspecto del módulo de tareas:</span><span class="sxs-lookup"><span data-stu-id="7fe6d-123">Here's what the task module looks like:</span></span>

![Módulo de tareas: formulario personalizado](~/assets/images/task-module/task-module-custom-form.png)

<span data-ttu-id="7fe6d-125">El `submitHandler` es muy simple; solo hace eco del valor de `err` o de la `result` consola:</span><span class="sxs-lookup"><span data-stu-id="7fe6d-125">The `submitHandler` is very simple; it just echoes the value of `err` or `result` to the console:</span></span>

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

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="7fe6d-126">Enviar el resultado de un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="7fe6d-126">Submitting the result of a task module</span></span>

<span data-ttu-id="7fe6d-127">La `submitHandler` función se usa con `TaskInfo.url` .</span><span class="sxs-lookup"><span data-stu-id="7fe6d-127">The `submitHandler` function is used with `TaskInfo.url`.</span></span> <span data-ttu-id="7fe6d-128">La `submitHandler` función reside en la página `TaskInfo.url` web.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-128">The `submitHandler` function resides in the `TaskInfo.url` web page.</span></span> <span data-ttu-id="7fe6d-129">Si hay un error al invocar el módulo de tareas, la función se invocará inmediatamente con una cadena `submitHandler` que indique qué error se `err` [produjo](#task-module-invocation-errors).</span><span class="sxs-lookup"><span data-stu-id="7fe6d-129">If there's an error when invoking the task module your `submitHandler` function will be immediately invoked with an `err` string indicating which [error occurred](#task-module-invocation-errors).</span></span> <span data-ttu-id="7fe6d-130">También se llama a la función con una cadena cuando el usuario presiona la X en `submitHandler` la parte superior derecha del módulo de `err` tareas.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-130">The `submitHandler` function is also called with an `err` string when the user presses the X at the upper right of task module.</span></span>

<span data-ttu-id="7fe6d-131">Si no hay ningún error de invocación y el usuario no presiona X para descartarlo, el usuario presiona un botón cuando finaliza.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-131">If there's no invocation error and the user doesn't press X to dismiss it, the user presses a button when finished.</span></span> <span data-ttu-id="7fe6d-132">Según si se trata de una dirección URL o una tarjeta adaptable en el módulo de tareas, esto es lo que sucede:</span><span class="sxs-lookup"><span data-stu-id="7fe6d-132">Depending on whether it's a URL or an Adaptive card in the task module, here's what happens:</span></span>

### <a name="htmljavascript-taskinfourl"></a><span data-ttu-id="7fe6d-133">HTML/JavaScript ( `TaskInfo.url` )</span><span class="sxs-lookup"><span data-stu-id="7fe6d-133">HTML/JavaScript (`TaskInfo.url`)</span></span>

<span data-ttu-id="7fe6d-134">Una vez validado lo que el usuario ha escrito, se llama a la función SDK (a la que se hace referencia a continuación con fines `microsoftTeams.tasks.submitTask()` `submitTask()` de legibilidad).</span><span class="sxs-lookup"><span data-stu-id="7fe6d-134">Once you've validated what the user has entered you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="7fe6d-135">Puede llamar sin ningún parámetro si solo desea que Teams cierre el módulo de tareas, pero la mayoría de las veces querrá pasar un objeto o una cadena `submitTask()` a `submitHandler` su .</span><span class="sxs-lookup"><span data-stu-id="7fe6d-135">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span>

<span data-ttu-id="7fe6d-136">Pase el resultado como primer parámetro.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-136">Pass your result as the first parameter.</span></span> <span data-ttu-id="7fe6d-137">Teams `submitHandler` invocará dónde `err` estará y será el objeto o cadena que pasó a `null` `result` `submitTask()` .</span><span class="sxs-lookup"><span data-stu-id="7fe6d-137">Teams will invoke `submitHandler` where `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="7fe6d-138">Si llamas con un parámetro, debes pasar una o una matriz de `submitTask()` `result` cadenas:  esto permite a Teams validar que la aplicación que envía el resultado es la misma que invocó el módulo de `appId` `appId` tareas.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-138">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span>

### <a name="adaptive-card-taskinfocard"></a><span data-ttu-id="7fe6d-139">Tarjeta adaptable ( `TaskInfo.card` )</span><span class="sxs-lookup"><span data-stu-id="7fe6d-139">Adaptive card (`TaskInfo.card`)</span></span>

<span data-ttu-id="7fe6d-140">Si invocó el módulo de tareas con un , cuando el usuario presiona un botón, los valores de la tarjeta se devolverán `submitHandler` como el valor de `Action.Submit` `result` .</span><span class="sxs-lookup"><span data-stu-id="7fe6d-140">If you invoked the task module with a `submitHandler`, when the user presses an `Action.Submit` button the values in the card will be returned as the value of `result`.</span></span> <span data-ttu-id="7fe6d-141">Si el usuario presiona el botón Esc o presiona la X, `err` se devolverá en su lugar.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-141">If the user presses the Esc button or presses the X, `err` will be returned instead.</span></span> <span data-ttu-id="7fe6d-142">Como alternativa, si la aplicación contiene un bot además de una pestaña, simplemente puedes incluir el bot como el valor `appId` `completionBotId` del `TaskInfo` objeto.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-142">Alternatively, if your app contains a bot in addition to a tab you can simply include the `appId` of the bot as the value of `completionBotId` in the `TaskInfo` object.</span></span> <span data-ttu-id="7fe6d-143">El cuerpo de la tarjeta adaptable (como lo rellena el usuario) se enviará al bot a través de un mensaje cuando el usuario `task/submit invoke` presione un `Action.Submit` botón.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-143">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit invoke` message when the user presses an `Action.Submit` button.</span></span> <span data-ttu-id="7fe6d-144">El esquema del objeto que recibe es muy similar al esquema que recibe para los mensajes [task/fetch y task/submit](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages); la única diferencia es que el esquema del objeto JSON es  un objeto de tarjeta adaptable en lugar de un objeto que contiene un objeto de tarjeta adaptable como cuando se usan [tarjetas adaptables](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)con bots .</span><span class="sxs-lookup"><span data-stu-id="7fe6d-144">The schema for the object you receive is very similar to [the schema you receive for task/fetch and task/submit messages](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages); the only difference is that the schema of the JSON object is an Adaptive card object as opposed to an object *containing* an Adaptive card object as [when Adaptive cards are used with bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span></span>

## <a name="example-submitting-the-result-of-a-task-module"></a><span data-ttu-id="7fe6d-145">Ejemplo: enviar el resultado de un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="7fe6d-145">Example: submitting the result of a task module</span></span>

<span data-ttu-id="7fe6d-146">Recuerde el [formulario del módulo de tareas anterior](#example-invoking-a-task-module) con un formulario HTML.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-146">Recall the [form in the task module above](#example-invoking-a-task-module) with an HTML form.</span></span> <span data-ttu-id="7fe6d-147">Aquí es donde se define el formulario:</span><span class="sxs-lookup"><span data-stu-id="7fe6d-147">Here's where the form is defined:</span></span>

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

<span data-ttu-id="7fe6d-148">Hay cinco campos en este formulario, pero solo nos interesan los valores de tres de ellos para este ejemplo: `name` , `email` y `favoriteBook` .</span><span class="sxs-lookup"><span data-stu-id="7fe6d-148">There are five fields on this form but we're only interested in the values of three of them for this example: `name`, `email`, and `favoriteBook`.</span></span>

<span data-ttu-id="7fe6d-149">Esta es la `validateForm()` función que llama a `submitTask()` :</span><span class="sxs-lookup"><span data-stu-id="7fe6d-149">Here's the `validateForm()` function that calls `submitTask()`:</span></span>

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

## <a name="task-module-invocation-errors"></a><span data-ttu-id="7fe6d-150">Errores de invocación de módulos de tareas</span><span class="sxs-lookup"><span data-stu-id="7fe6d-150">Task module invocation errors</span></span>

<span data-ttu-id="7fe6d-151">Estos son los posibles valores `err` que puede recibir su `submitHandler` :</span><span class="sxs-lookup"><span data-stu-id="7fe6d-151">Here are the possible values of `err` that can be received by your `submitHandler`:</span></span>

| <span data-ttu-id="7fe6d-152">Problema</span><span class="sxs-lookup"><span data-stu-id="7fe6d-152">Problem</span></span> | <span data-ttu-id="7fe6d-153">Mensaje de error (valor de `err` )</span><span class="sxs-lookup"><span data-stu-id="7fe6d-153">Error message (value of `err`)</span></span> |
| ------- | ------------------------------ |
| <span data-ttu-id="7fe6d-154">Valores para ambos `TaskInfo.url` y `TaskInfo.card` se especificaron.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-154">Values for both `TaskInfo.url` and `TaskInfo.card` were specified.</span></span> | <span data-ttu-id="7fe6d-155">"Se especificaron valores para la tarjeta y la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-155">"Values for both card and url were specified.</span></span> <span data-ttu-id="7fe6d-156">Uno u otro, pero no ambos, están permitidos".</span><span class="sxs-lookup"><span data-stu-id="7fe6d-156">One or the other, but not both, are allowed."</span></span> |
| <span data-ttu-id="7fe6d-157">No `TaskInfo.url` se especifica ni se `TaskInfo.card` especifica.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-157">Neither `TaskInfo.url` nor `TaskInfo.card` specified.</span></span> | <span data-ttu-id="7fe6d-158">"Debe especificar un valor para la tarjeta o la dirección URL".</span><span class="sxs-lookup"><span data-stu-id="7fe6d-158">"You must specify a value for either card or url."</span></span> |
| <span data-ttu-id="7fe6d-159">No es `appId` válido .</span><span class="sxs-lookup"><span data-stu-id="7fe6d-159">Invalid `appId`.</span></span> | <span data-ttu-id="7fe6d-160">"AppId no válido".</span><span class="sxs-lookup"><span data-stu-id="7fe6d-160">"Invalid appId."</span></span> |
| <span data-ttu-id="7fe6d-161">El usuario ha presionado el botón X y lo cierra.</span><span class="sxs-lookup"><span data-stu-id="7fe6d-161">User pressed X button, closing it.</span></span> | <span data-ttu-id="7fe6d-162">"El usuario canceló o cerró el módulo de tareas".</span><span class="sxs-lookup"><span data-stu-id="7fe6d-162">"User cancelled/closed the task module."</span></span> |

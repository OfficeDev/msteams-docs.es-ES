---
title: Uso de módulos de tareas en las pestañas de Microsoft Teams
description: Explica cómo invocar módulos de tareas desde las pestañas de Teams mediante el SDK del cliente de Microsoft Teams.
keywords: módulos de tareas el SDK del cliente de pestañas de Teams
ms.openlocfilehash: e10958195713f338a9b5e0a0672d8b6a29da9264
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676145"
---
# <a name="using-task-modules-in-tabs"></a><span data-ttu-id="702c1-104">Uso de módulos de tareas en pestañas</span><span class="sxs-lookup"><span data-stu-id="702c1-104">Using task modules in tabs</span></span>

<span data-ttu-id="702c1-105">Agregar un módulo de tareas a la pestaña puede simplificar enormemente la experiencia del usuario para los flujos de trabajo que requieran la entrada de datos.</span><span class="sxs-lookup"><span data-stu-id="702c1-105">Adding a task module to your tab can greatly simplify your user's experience for any workflows that require data input.</span></span> <span data-ttu-id="702c1-106">Los módulos de tareas le permiten recopilar su entrada en un elemento emergente que reconozca los equipos.</span><span class="sxs-lookup"><span data-stu-id="702c1-106">Task modules allow you to gather their input in a Teams-aware popup.</span></span> <span data-ttu-id="702c1-107">Un buen ejemplo de esto es editar las tarjetas de Planner; puede usar los módulos de tareas para crear una experiencia similar.</span><span class="sxs-lookup"><span data-stu-id="702c1-107">A good example of this is editing Planner cards; you can use task modules to create a similar experience.</span></span>

<span data-ttu-id="702c1-108">Para admitir la característica de módulo de tareas, se agregaron dos nuevas funciones al [SDK del cliente de Microsoft Teams](/javascript/api/overview/msteams-client):</span><span class="sxs-lookup"><span data-stu-id="702c1-108">To support the task module feature, two new functions were added to the [Microsoft Teams client SDK](/javascript/api/overview/msteams-client):</span></span>

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

<span data-ttu-id="702c1-109">Vamos a ver cómo funciona cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="702c1-109">Let's see how each of them work.</span></span>

## <a name="invoking-a-task-module-from-a-tab"></a><span data-ttu-id="702c1-110">Invocar un módulo de tareas desde una pestaña</span><span class="sxs-lookup"><span data-stu-id="702c1-110">Invoking a task module from a tab</span></span>

<span data-ttu-id="702c1-111">Para invocar un módulo de tareas desde una `microsoftTeams.tasks.startTask()` pestaña, use el paso de un `submitHandler` [objeto TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) y una función de devolución de llamada opcional.</span><span class="sxs-lookup"><span data-stu-id="702c1-111">To invoke a task module from a tab use `microsoftTeams.tasks.startTask()` passing a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) and an optional `submitHandler` callback function.</span></span> <span data-ttu-id="702c1-112">Como se describió anteriormente, hay dos casos que hay que tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="702c1-112">As described earlier, there are two cases to consider:</span></span>

1. <span data-ttu-id="702c1-113">El valor de `TaskInfo.url` se establece en una dirección URL.</span><span class="sxs-lookup"><span data-stu-id="702c1-113">The value of `TaskInfo.url` is set to a URL.</span></span> <span data-ttu-id="702c1-114">Aparece la ventana módulo de tarea `TaskModule.url` y se carga como `<iframe>` en su interior.</span><span class="sxs-lookup"><span data-stu-id="702c1-114">The task module window appears and `TaskModule.url` is loaded as an `<iframe>` inside it.</span></span> <span data-ttu-id="702c1-115">JavaScript en esa página debe llamar `microsoftTeams.initialize()`a.</span><span class="sxs-lookup"><span data-stu-id="702c1-115">JavaScript on that page should call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="702c1-116">`submitHandler` Si hay una función en la página y se produce un error al invocar `microsoftTeams.tasks.startTask()`, entonces `submitHandler` se invoca con `err` set en la cadena de error que indica el error, como se describe [a continuación](#task-module-invocation-errors).</span><span class="sxs-lookup"><span data-stu-id="702c1-116">If there is a `submitHandler` function on the page and there is an error when invoking `microsoftTeams.tasks.startTask()`, then `submitHandler` is invoked with `err` set to the error string indicating the error as described [below](#task-module-invocation-errors).</span></span>
1. <span data-ttu-id="702c1-117">El valor de `taskInfo.card` es el [JSON de una tarjeta adaptable](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span><span class="sxs-lookup"><span data-stu-id="702c1-117">The value of `taskInfo.card` is the [JSON for an Adaptive card](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span></span> <span data-ttu-id="702c1-118">En este caso, obviamente no hay ninguna función `submitHandler` JavaScript para llamar cuando el usuario cierra o presiona un botón en la tarjeta adaptable; la única forma de recibir lo que el usuario ha escrito es pasar el resultado a un bot.</span><span class="sxs-lookup"><span data-stu-id="702c1-118">In this case there's obviously not any JavaScript `submitHandler` function to call when the user closes or presses a button on the Adaptive card; the only way to receive what the user entered is by passing the result to a bot.</span></span> <span data-ttu-id="702c1-119">Para usar un módulo de tareas de tarjeta adaptable desde una pestaña, la aplicación debe incluir un bot para obtener la información del usuario.</span><span class="sxs-lookup"><span data-stu-id="702c1-119">To use an Adaptive card task module from a tab your app must include a bot to get any information back from the user.</span></span> <span data-ttu-id="702c1-120">Esto se explica a continuación.</span><span class="sxs-lookup"><span data-stu-id="702c1-120">This is explained below.</span></span>

## <a name="example-invoking-a-task-module"></a><span data-ttu-id="702c1-121">Ejemplo: invocación de un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="702c1-121">Example: Invoking a task module</span></span>

<span data-ttu-id="702c1-122">El siguiente código se adapta desde [el ejemplo de módulo de tarea](~/task-modules-and-cards/what-are-task-modules.md#task-module-samples).</span><span class="sxs-lookup"><span data-stu-id="702c1-122">The code below is adapted from [the task module sample](~/task-modules-and-cards/what-are-task-modules.md#task-module-samples).</span></span> <span data-ttu-id="702c1-123">Así es como se ve el módulo de tareas:</span><span class="sxs-lookup"><span data-stu-id="702c1-123">Here's what the task module looks like:</span></span>

![Módulo de tareas-formulario personalizado](~/assets/images/task-module/task-module-custom-form.png)

<span data-ttu-id="702c1-125">El `submitHandler` es muy sencillo; simplemente, se repite el `err` valor `result` de o a la consola:</span><span class="sxs-lookup"><span data-stu-id="702c1-125">The `submitHandler` is very simple; it just echoes the value of `err` or `result` to the console:</span></span>

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

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="702c1-126">Enviar el resultado de un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="702c1-126">Submitting the result of a task module</span></span>

<span data-ttu-id="702c1-127">La `submitHandler` función se usa con `TaskInfo.url`.</span><span class="sxs-lookup"><span data-stu-id="702c1-127">The `submitHandler` function is used with `TaskInfo.url`.</span></span> <span data-ttu-id="702c1-128">La `submitHandler` función reside en la `TaskInfo.url` Página Web.</span><span class="sxs-lookup"><span data-stu-id="702c1-128">The `submitHandler` function resides in the `TaskInfo.url` web page.</span></span> <span data-ttu-id="702c1-129">Si hay un error al invocar el módulo de tareas, `submitHandler` la función se invocará inmediatamente con una `err` cadena que indica el [error que se ha producido](#task-module-invocation-errors).</span><span class="sxs-lookup"><span data-stu-id="702c1-129">If there's an error when invoking the task module your `submitHandler` function will be immediately invoked with an `err` string indicating which [error occurred](#task-module-invocation-errors).</span></span> <span data-ttu-id="702c1-130">También `submitHandler` se llama a la función con `err` una cadena cuando el usuario presiona la X en la parte superior derecha del módulo de tarea.</span><span class="sxs-lookup"><span data-stu-id="702c1-130">The `submitHandler` function is also called with an `err` string when the user presses the X at the upper right of task module.</span></span>

<span data-ttu-id="702c1-131">Si no hay ningún error de invocación y el usuario no presiona X para descartarlo, el usuario presiona un botón cuando termina.</span><span class="sxs-lookup"><span data-stu-id="702c1-131">If there's no invocation error and the user doesn't press X to dismiss it, the user presses a button when finished.</span></span> <span data-ttu-id="702c1-132">En función de si es una dirección URL o una tarjeta adaptable en el módulo de tareas, esto es lo que sucede:</span><span class="sxs-lookup"><span data-stu-id="702c1-132">Depending on whether it's a URL or an Adaptive card in the task module, here's what happens:</span></span>

### <a name="htmljavascript-taskinfourl"></a><span data-ttu-id="702c1-133">HTML/JavaScript (`TaskInfo.url`)</span><span class="sxs-lookup"><span data-stu-id="702c1-133">HTML/JavaScript (`TaskInfo.url`)</span></span>

<span data-ttu-id="702c1-134">Una vez que haya validado lo que ha escrito el usuario, `microsoftTeams.tasks.submitTask()` llame a la función SDK (denominada `submitTask()` de ahora en adelante con fines de legibilidad).</span><span class="sxs-lookup"><span data-stu-id="702c1-134">Once you've validated what the user has entered you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="702c1-135">Si solo desea `submitTask()` que Microsoft Teams cierre el módulo de tareas, puede llamar a sin ningún parámetro, pero la mayoría de las veces querrá pasar un objeto o una cadena a `submitHandler`su.</span><span class="sxs-lookup"><span data-stu-id="702c1-135">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span>

<span data-ttu-id="702c1-136">Pase el resultado como primer parámetro.</span><span class="sxs-lookup"><span data-stu-id="702c1-136">Pass your result as the first parameter.</span></span> <span data-ttu-id="702c1-137">Microsoft Teams `submitHandler` invocará `err` dónde `null` será `result` y será el objeto o la cadena que haya `submitTask()`pasado.</span><span class="sxs-lookup"><span data-stu-id="702c1-137">Teams will invoke `submitHandler` where `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="702c1-138">Si `submitTask()` llama a con `result` un parámetro, **debe** pasar una `appId` o una matriz de `appId` cadenas: Esto permite a Microsoft Teams validar que la aplicación que envía el resultado es la misma que ha invocado el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="702c1-138">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span>

### <a name="adaptive-card-taskinfocard"></a><span data-ttu-id="702c1-139">Tarjeta adaptable`TaskInfo.card`()</span><span class="sxs-lookup"><span data-stu-id="702c1-139">Adaptive card (`TaskInfo.card`)</span></span>

<span data-ttu-id="702c1-140">Si ha invocado el módulo de tareas con `submitHandler`una, cuando el usuario presiona `Action.Submit` un botón, los valores de la tarjeta se devolverán como `result`el valor de.</span><span class="sxs-lookup"><span data-stu-id="702c1-140">If you invoked the task module with a `submitHandler`, when the user presses an `Action.Submit` button the values in the card will be returned as the value of `result`.</span></span> <span data-ttu-id="702c1-141">Si el usuario presiona el botón ESC o presiona la X, `err` se devolverá en su lugar.</span><span class="sxs-lookup"><span data-stu-id="702c1-141">If the user presses the Esc button or presses the X, `err` will be returned instead.</span></span> <span data-ttu-id="702c1-142">Como alternativa, si la aplicación contiene un bot, además de una pestaña, puede incluir simplemente el `appId` bot? n como el valor de `completionBotId` en el `TaskInfo` objeto.</span><span class="sxs-lookup"><span data-stu-id="702c1-142">Alternatively, if your app contains a bot in addition to a tab you can simply include the `appId` of the bot as the value of `completionBotId` in the `TaskInfo` object.</span></span> <span data-ttu-id="702c1-143">El cuerpo de la tarjeta adaptable (como rellenado por el usuario) se enviará al `task/submit invoke` bot a través de un mensaje `Action.Submit` cuando el usuario presione un botón.</span><span class="sxs-lookup"><span data-stu-id="702c1-143">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit invoke` message when the user presses an `Action.Submit` button.</span></span> <span data-ttu-id="702c1-144">El esquema del objeto que recibe es muy similar al [esquema que recibe para los mensajes de tarea/búsqueda y de tarea o envío](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages); la única diferencia es que el esquema del objeto JSON es un objeto de tarjeta adaptable en lugar de un objeto *que contiene* un objeto de tarjeta adaptable, como [cuando se usan tarjetas adaptables con bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span><span class="sxs-lookup"><span data-stu-id="702c1-144">The schema for the object you receive is very similar to [the schema you receive for task/fetch and task/submit messages](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages); the only difference is that the schema of the JSON object is an Adaptive card object as opposed to an object *containing* an Adaptive card object as [when Adaptive cards are used with bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span></span>

## <a name="example-submitting-the-result-of-a-task-module"></a><span data-ttu-id="702c1-145">Ejemplo: enviar el resultado de un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="702c1-145">Example: submitting the result of a task module</span></span>

<span data-ttu-id="702c1-146">Recupere el [formulario en el módulo de tareas anterior](#example-invoking-a-task-module) con un formulario HTML.</span><span class="sxs-lookup"><span data-stu-id="702c1-146">Recall the [form in the task module above](#example-invoking-a-task-module) with an HTML form.</span></span> <span data-ttu-id="702c1-147">Aquí es donde se define el formulario:</span><span class="sxs-lookup"><span data-stu-id="702c1-147">Here's where the form is defined:</span></span>

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

<span data-ttu-id="702c1-148">Hay cinco campos en este formulario, pero solo estamos interesados en los valores de tres de ellos para este ejemplo: `name`, `email`y. `favoriteBook`</span><span class="sxs-lookup"><span data-stu-id="702c1-148">There are five fields on this form but we're only interested in the values of three of them for this example: `name`, `email`, and `favoriteBook`.</span></span>

<span data-ttu-id="702c1-149">Esta es la `validateForm()` función que llama `submitTask()`:</span><span class="sxs-lookup"><span data-stu-id="702c1-149">Here's the `validateForm()` function that calls `submitTask()`:</span></span>

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

## <a name="task-module-invocation-errors"></a><span data-ttu-id="702c1-150">Errores de invocación de módulo de tarea</span><span class="sxs-lookup"><span data-stu-id="702c1-150">Task module invocation errors</span></span>

<span data-ttu-id="702c1-151">Estos son los valores posibles `err` que puede recibir: `submitHandler`</span><span class="sxs-lookup"><span data-stu-id="702c1-151">Here are the possible values of `err` that can be received by your `submitHandler`:</span></span>

| <span data-ttu-id="702c1-152">Problema</span><span class="sxs-lookup"><span data-stu-id="702c1-152">Problem</span></span> | <span data-ttu-id="702c1-153">Mensaje de error (valor `err`de)</span><span class="sxs-lookup"><span data-stu-id="702c1-153">Error message (value of `err`)</span></span> |
| ------- | ------------------------------ |
| <span data-ttu-id="702c1-154">Los valores para `TaskInfo.url` ambos `TaskInfo.card` y se especificaron.</span><span class="sxs-lookup"><span data-stu-id="702c1-154">Values for both `TaskInfo.url` and `TaskInfo.card` were specified.</span></span> | <span data-ttu-id="702c1-155">"Se especificaron los valores de la tarjeta y la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="702c1-155">"Values for both card and url were specified.</span></span> <span data-ttu-id="702c1-156">Se permite una o la otra, pero no ambas.</span><span class="sxs-lookup"><span data-stu-id="702c1-156">One or the other, but not both, are allowed."</span></span> |
| <span data-ttu-id="702c1-157">Ni `TaskInfo.url` tampoco `TaskInfo.card` se especifican.</span><span class="sxs-lookup"><span data-stu-id="702c1-157">Neither `TaskInfo.url` nor `TaskInfo.card` specified.</span></span> | <span data-ttu-id="702c1-158">"Debe especificar un valor para cualquier tarjeta o dirección URL."</span><span class="sxs-lookup"><span data-stu-id="702c1-158">"You must specify a value for either card or url."</span></span> |
| <span data-ttu-id="702c1-159">No `appId`válido.</span><span class="sxs-lookup"><span data-stu-id="702c1-159">Invalid `appId`.</span></span> | <span data-ttu-id="702c1-160">"AppId no válido".</span><span class="sxs-lookup"><span data-stu-id="702c1-160">"Invalid appId."</span></span> |
| <span data-ttu-id="702c1-161">El usuario presionó el botón X y lo cerraba.</span><span class="sxs-lookup"><span data-stu-id="702c1-161">User pressed X button, closing it.</span></span> | <span data-ttu-id="702c1-162">"El usuario canceló o cerró el módulo de tarea".</span><span class="sxs-lookup"><span data-stu-id="702c1-162">"User cancelled/closed the task module."</span></span> |

---
title: Uso de módulos de tareas en las pestañas de Microsoft Teams
description: Explica cómo invocar módulos de tareas desde las pestañas de Teams mediante el SDK del cliente de Microsoft Teams.
keywords: módulos de tareas el SDK del cliente de pestañas de Teams
ms.openlocfilehash: e10958195713f338a9b5e0a0672d8b6a29da9264
ms.sourcegitcommit: 2a84a3c8b10771e37ce51bf603a967633947a3e4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/10/2020
ms.locfileid: "44801447"
---
# <a name="using-task-modules-in-tabs"></a>Uso de módulos de tareas en pestañas

Agregar un módulo de tareas a la pestaña puede simplificar enormemente la experiencia del usuario para los flujos de trabajo que requieran la entrada de datos. Los módulos de tareas le permiten recopilar su entrada en un elemento emergente que reconozca los equipos. Un buen ejemplo de esto es editar las tarjetas de Planner; puede usar los módulos de tareas para crear una experiencia similar.

Para admitir la característica de módulo de tareas, se agregaron dos nuevas funciones al [SDK del cliente de Microsoft Teams](/javascript/api/overview/msteams-client):

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

Vamos a ver cómo funciona cada uno de ellos.

## <a name="invoking-a-task-module-from-a-tab"></a>Invocar un módulo de tareas desde una pestaña

Para invocar un módulo de tareas desde una pestaña, use el `microsoftTeams.tasks.startTask()` paso de un [objeto TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) y una `submitHandler` función de devolución de llamada opcional. Como se describió anteriormente, hay dos casos que hay que tener en cuenta:

1. El valor de `TaskInfo.url` se establece en una dirección URL. Aparece la ventana módulo de tarea y `TaskModule.url` se carga como `<iframe>` en su interior. JavaScript en esa página debe llamar a `microsoftTeams.initialize()` . Si hay una `submitHandler` función en la página y se produce un error al invocar `microsoftTeams.tasks.startTask()` , entonces `submitHandler` se invoca con `err` set en la cadena de error que indica el error, como se describe [a continuación](#task-module-invocation-errors).
1. El valor de `taskInfo.card` es el [JSON de una tarjeta adaptable](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment). En este caso, obviamente no hay ninguna `submitHandler` función JavaScript para llamar cuando el usuario cierra o presiona un botón en la tarjeta adaptable; la única forma de recibir lo que el usuario ha escrito es pasar el resultado a un bot. Para usar un módulo de tareas de tarjeta adaptable desde una pestaña, la aplicación debe incluir un bot para obtener la información del usuario. Esto se explica a continuación.

## <a name="example-invoking-a-task-module"></a>Ejemplo: invocación de un módulo de tareas

El siguiente código se adapta desde [el ejemplo de módulo de tarea](~/task-modules-and-cards/what-are-task-modules.md#task-module-samples). Así es como se ve el módulo de tareas:

![Módulo de tareas-formulario personalizado](~/assets/images/task-module/task-module-custom-form.png)

El `submitHandler` es muy sencillo; solo repite el valor de `err` o `result` a la consola:

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

## <a name="submitting-the-result-of-a-task-module"></a>Enviar el resultado de un módulo de tareas

La `submitHandler` función se usa con `TaskInfo.url` . La `submitHandler` función reside en la `TaskInfo.url` Página Web. Si hay un error al invocar el módulo de tareas `submitHandler` , la función se invocará inmediatamente con una `err` cadena que indica el [error que se ha producido](#task-module-invocation-errors). `submitHandler`También se llama a la función con una `err` cadena cuando el usuario presiona la X en la parte superior derecha del módulo de tarea.

Si no hay ningún error de invocación y el usuario no presiona X para descartarlo, el usuario presiona un botón cuando termina. En función de si es una dirección URL o una tarjeta adaptable en el módulo de tareas, esto es lo que sucede:

### <a name="htmljavascript-taskinfourl"></a>HTML/JavaScript ( `TaskInfo.url` )

Una vez que haya validado lo que ha escrito el usuario, llame a la `microsoftTeams.tasks.submitTask()` función SDK (denominada de ahora en adelante con `submitTask()` fines de legibilidad). `submitTask()`Si solo desea que Microsoft Teams cierre el módulo de tareas, puede llamar a sin ningún parámetro, pero la mayoría de las veces querrá pasar un objeto o una cadena a su `submitHandler` .

Pase el resultado como primer parámetro. Microsoft Teams invocará `submitHandler` dónde será `err` `null` y `result` será el objeto o la cadena que haya pasado `submitTask()` . Si llama a `submitTask()` con un `result` parámetro, **debe** pasar una `appId` o una matriz de `appId` cadenas: Esto permite a Microsoft Teams validar que la aplicación que envía el resultado es la misma que ha invocado el módulo de tareas.

### <a name="adaptive-card-taskinfocard"></a>Tarjeta adaptable ( `TaskInfo.card` )

Si ha invocado el módulo de tareas con una `submitHandler` , cuando el usuario presiona un `Action.Submit` botón, los valores de la tarjeta se devolverán como el valor de `result` . Si el usuario presiona el botón ESC o presiona la X, se `err` devolverá en su lugar. Como alternativa, si la aplicación contiene un bot, además de una pestaña, puede incluir simplemente el `appId` Bot? n como el valor de `completionBotId` en el `TaskInfo` objeto. El cuerpo de la tarjeta adaptable (como rellenado por el usuario) se enviará al bot a través de un `task/submit invoke` mensaje cuando el usuario presione un `Action.Submit` botón. El esquema del objeto que recibe es muy similar al [esquema que recibe para los mensajes de tarea/búsqueda y de tarea o envío](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages); la única diferencia es que el esquema del objeto JSON es un objeto de tarjeta adaptable en lugar de un objeto *que contiene* un objeto de tarjeta adaptable, como [cuando se usan tarjetas adaptables con bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).

## <a name="example-submitting-the-result-of-a-task-module"></a>Ejemplo: enviar el resultado de un módulo de tareas

Recupere el [formulario en el módulo de tareas anterior](#example-invoking-a-task-module) con un formulario HTML. Aquí es donde se define el formulario:

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

Hay cinco campos en este formulario, pero solo estamos interesados en los valores de tres de ellos para este ejemplo: `name` , `email` y `favoriteBook` .

Esta es la `validateForm()` función que llama `submitTask()` :

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

## <a name="task-module-invocation-errors"></a>Errores de invocación de módulo de tarea

Estos son los valores posibles `err` que puede recibir `submitHandler` :

| Problema | Mensaje de error (valor de `err` ) |
| ------- | ------------------------------ |
| Los valores para ambos `TaskInfo.url` y `TaskInfo.card` se especificaron. | "Se especificaron los valores de la tarjeta y la dirección URL. Se permite una o la otra, pero no ambas. |
| Ni `TaskInfo.url` tampoco se `TaskInfo.card` especifican. | "Debe especificar un valor para cualquier tarjeta o dirección URL." |
| No válido `appId` . | "AppId no válido". |
| El usuario presionó el botón X y lo cerraba. | "El usuario canceló o cerró el módulo de tarea". |

---
title: Uso de módulos de tareas en pestañas de Microsoft Teams
description: Explica cómo invocar módulos de tareas desde pestañas de Teams mediante el SDK de cliente de Microsoft Teams.
keywords: sdk de cliente de pestañas de teams de módulos de tareas
ms.openlocfilehash: 3f1da4d5eec31638d69adc01a45831534d015f41
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449559"
---
# <a name="using-task-modules-in-tabs"></a>Uso de módulos de tareas en pestañas

Agregar un módulo de tareas a la pestaña puede simplificar enormemente la experiencia del usuario para cualquier flujo de trabajo que requiera entrada de datos. Los módulos de tareas le permiten recopilar sus entradas en un elemento emergente de Teams. Un buen ejemplo de esto es la edición de tarjetas planner; puede usar módulos de tareas para crear una experiencia similar.

Para admitir la característica del módulo de tareas, se agregaron dos nuevas funciones al [SDK de cliente de Microsoft Teams:](/javascript/api/overview/msteams-client)

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

Veamos cómo funcionan cada uno de ellos.

## <a name="invoking-a-task-module-from-a-tab"></a>Invocar un módulo de tareas desde una pestaña

Para invocar un módulo de tarea desde una pestaña, use `microsoftTeams.tasks.startTask()` pasar un [objeto TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) y una función `submitHandler` de devolución de llamada opcional. Como se describió anteriormente, hay dos casos a tener en cuenta:

1. El valor de `TaskInfo.url` se establece en una dirección URL. La ventana del módulo de tareas aparece `TaskModule.url` y se carga como dentro de `<iframe>` ella. JavaScript en esa página debe llamar `microsoftTeams.initialize()` a . Si hay una función en la página y hay un error al invocar , se invoca con set en la cadena de error que indica el error como se describe a `submitHandler` `microsoftTeams.tasks.startTask()` `submitHandler` `err` [continuación](#task-module-invocation-errors).
1. El valor de `taskInfo.card` es el JSON de una tarjeta [adaptable](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment). En este caso, obviamente, no hay ninguna función de JavaScript a la que llamar cuando el usuario cierra o presiona un botón en la tarjeta adaptable; la única forma de recibir lo que el usuario ha escrito es pasando el resultado a un `submitHandler` bot. Para usar un módulo de tareas de tarjeta adaptable desde una pestaña, la aplicación debe incluir un bot para obtener información del usuario. Esto se explica a continuación.

## <a name="example-invoking-a-task-module"></a>Ejemplo: Invocar un módulo de tareas

El código siguiente se adapta del [ejemplo de módulo de tareas](~/task-modules-and-cards/what-are-task-modules.md#code-sample). Este es el aspecto del módulo de tareas:

![Módulo de tareas: formulario personalizado](~/assets/images/task-module/task-module-custom-form.png)

El `submitHandler` es muy simple; solo hace eco del valor de `err` o de la `result` consola:

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

La `submitHandler` función se usa con `TaskInfo.url` . La `submitHandler` función reside en la página `TaskInfo.url` web. Si hay un error al invocar el módulo de tareas, la función se invocará inmediatamente con una cadena `submitHandler` que indique qué error se `err` [produjo](#task-module-invocation-errors). También se llama a la función con una cadena cuando el usuario presiona la X en `submitHandler` la parte superior derecha del módulo de `err` tareas.

Si no hay ningún error de invocación y el usuario no presiona X para descartarlo, el usuario presiona un botón cuando finaliza. Según si se trata de una dirección URL o una tarjeta adaptable en el módulo de tareas, esto es lo que sucede:

### <a name="htmljavascript-taskinfourl"></a>HTML/JavaScript ( `TaskInfo.url` )

Una vez validado lo que el usuario ha escrito, se llama a la función SDK (a la que se hace referencia a continuación con fines `microsoftTeams.tasks.submitTask()` `submitTask()` de legibilidad). Puedes llamar sin ningún parámetro si solo quieres que Teams cierre el módulo de tareas, pero la mayoría de las veces querrás pasar un objeto o una cadena `submitTask()` a tu `submitHandler` .

Pase el resultado como primer parámetro. Teams invocará `submitHandler` dónde estará y será el objeto o cadena que pasó a `err` `null` `result` `submitTask()` . Si llama con un parámetro, debe pasar una o una matriz de cadenas: esto permite a Teams validar que la aplicación que envía el resultado es la misma que invocó el módulo `submitTask()` `result` de  `appId` `appId` tareas.

### <a name="adaptive-card-taskinfocard"></a>Tarjeta adaptable ( `TaskInfo.card` )

Si invocó el módulo de tareas con un , cuando el usuario presiona un botón, los valores de la tarjeta se devolverán `submitHandler` como el valor de `Action.Submit` `result` . Si el usuario presiona el botón Esc o presiona la X, `err` se devolverá en su lugar. Como alternativa, si la aplicación contiene un bot además de una pestaña, simplemente puedes incluir el bot como el valor `appId` `completionBotId` del `TaskInfo` objeto. El cuerpo de la tarjeta adaptable (como lo rellena el usuario) se enviará al bot a través de un mensaje cuando el usuario `task/submit invoke` presione un `Action.Submit` botón. El esquema del objeto que recibe es muy similar al esquema que recibe para los mensajes [task/fetch y task/submit](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages); la única diferencia es que el esquema del objeto JSON es  un objeto de tarjeta adaptable en lugar de un objeto que contiene un objeto de tarjeta adaptable como cuando se usan [tarjetas adaptables](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)con bots .

## <a name="example-submitting-the-result-of-a-task-module"></a>Ejemplo: enviar el resultado de un módulo de tareas

Recuerde el [formulario del módulo de tareas anterior](#example-invoking-a-task-module) con un formulario HTML. Aquí es donde se define el formulario:

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

Hay cinco campos en este formulario, pero solo nos interesan los valores de tres de ellos para este ejemplo: `name` , `email` y `favoriteBook` .

Esta es la `validateForm()` función que llama a `submitTask()` :

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

## <a name="task-module-invocation-errors"></a>Errores de invocación del módulo de tareas

Estos son los posibles valores `err` que puede recibir su `submitHandler` :

| Problema | Mensaje de error (valor de `err` ) |
| ------- | ------------------------------ |
| Valores para ambos `TaskInfo.url` y `TaskInfo.card` se especificaron. | "Se especificaron valores para la tarjeta y la dirección URL. Uno u otro, pero no ambos, están permitidos". |
| No `TaskInfo.url` se especifica ni se `TaskInfo.card` especifica. | "Debe especificar un valor para la tarjeta o la dirección URL". |
| No es `appId` válido . | "AppId no válido". |
| El usuario ha presionado el botón X y lo cierra. | "El usuario canceló o cerró el módulo de tareas". |

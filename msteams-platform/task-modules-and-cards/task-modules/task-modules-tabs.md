---
title: Usar módulos de tareas en Microsoft Teams pestañas
description: Explica cómo invocar módulos de tareas desde Teams pestañas mediante el SDK Microsoft Teams cliente.
ms.localizationpriority: medium
ms.topic: how-to
keywords: sdk de cliente de pestañas de teams de módulos de tareas
ms.openlocfilehash: 0f6c1569a1aa18921df4635bdbaab505526c1e2e
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157450"
---
# <a name="use-task-modules-in-tabs"></a>Uso de módulos de tareas en pestañas

Agregue un módulo de tareas a la pestaña para simplificar la experiencia del usuario para los flujos de trabajo que requieran entrada de datos. Los módulos de tareas permiten recopilar sus entradas en una ventana emergente Teams-Aware Microsoft. Un buen ejemplo de esto es la edición de tarjetas planner. Puede usar módulos de tareas para crear una experiencia similar.

Para admitir la característica de módulo de tareas, se agregan dos nuevas funciones al SDK Teams [cliente](/javascript/api/overview/msteams-client). El código siguiente muestra un ejemplo de estas dos funciones:

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

Puede ver cómo funciona invocar un módulo de tareas desde una pestaña y enviar el resultado de un módulo de tareas.

## <a name="invoke-a-task-module-from-a-tab"></a>Invocar un módulo de tareas desde una pestaña

Para invocar un módulo de tarea desde una pestaña, use `microsoftTeams.tasks.startTask()` pasar un [objeto TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) y una función `submitHandler` de devolución de llamada opcional. Hay dos casos a tener en cuenta:

* El valor de `TaskInfo.url` se establece en una dirección URL. La ventana del módulo de tareas aparece `TaskModule.url` y se carga como dentro de `<iframe>` ella. JavaScript en esa página llama `microsoftTeams.initialize()` a . Si hay una función en la página y hay un error al invocar , se invoca con set en la cadena `submitHandler` de error que indica lo `microsoftTeams.tasks.startTask()` `submitHandler` `err` mismo. Para obtener más información, vea [errores de invocación del módulo de tareas](#task-module-invocation-errors).
* El valor de `taskInfo.card` es el JSON de una tarjeta [adaptable](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment). No hay ninguna función de JavaScript a la que llamar cuando el usuario cierra o `submitHandler` presiona un botón en la tarjeta adaptable. La única forma de recibir lo que el usuario ha escrito es pasando el resultado a un bot. Para usar un módulo de tareas de tarjeta adaptable desde una pestaña, la aplicación debe incluir un bot para obtener cualquier respuesta del usuario.

En la siguiente sección se muestra un ejemplo de invocar un módulo de tareas.

## <a name="example-of-invoking-a-task-module"></a>Ejemplo de invocar un módulo de tareas

En la siguiente imagen se muestra el módulo de tareas:

![Módulo de tareas: formulario personalizado](~/assets/images/task-module/task-module-custom-form.png)

El siguiente código se adapta del [ejemplo del módulo de tareas:](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample)

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

El `submitHandler` es muy simple y hace eco del valor de o de la `err` `result` consola.

## <a name="submit-the-result-of-a-task-module"></a>Enviar el resultado de un módulo de tareas

La `submitHandler` función reside en la página web y se usa con `TaskInfo.url` `TaskInfo.url` . Si hay un error al invocar el módulo de tareas, la función se invoca inmediatamente con una `submitHandler` cadena que indica qué error se `err` [produjo](#task-module-invocation-errors). También se llama a la función con una cadena cuando el usuario selecciona X en la esquina superior derecha del módulo de tareas `submitHandler` `err` para cerrarla.

Si no hay ningún error de invocación y el usuario no selecciona X para descartarlo, el usuario elige un botón cuando finaliza. Según si se trata de una dirección URL o una tarjeta adaptable en el módulo de tareas, las siguientes secciones proporcionan detalles sobre lo que ocurre.

### <a name="html-or-javascript-taskinfourl"></a>HTML o JavaScript `TaskInfo.url`

Después de validar las entradas del usuario, llame a la `microsoftTeams.tasks.submitTask()` función SDK denominada `submitTask()` . Llame `submitTask()` sin ningún parámetro si solo desea Teams cerrar el módulo de tareas. Puede pasar un objeto o una cadena a `submitHandler` su .

Pase el resultado como primer parámetro. Teams invoca dónde `submitHandler` `err` es y es el objeto o cadena que pasó a `null` `result` `submitTask()` . Si llama `submitTask()` con un `result` parámetro, debe pasar una o una `appId` matriz de `appId` cadenas. Esto permite Teams validar que la aplicación que envía el resultado es la misma que el módulo de tareas invocado.

### <a name="adaptive-card-taskinfocard"></a>Tarjeta adaptable `TaskInfo.card`

Al invocar el módulo de tareas con a y el usuario selecciona un botón, los valores de la tarjeta se devuelven `submitHandler` como el valor de `Action.Submit` `result` . Si el usuario selecciona la tecla Esc o X en la parte superior derecha, `err` se devuelve en su lugar. Si la aplicación contiene un bot además de una pestaña, simplemente puedes incluir el bot como el `appId` valor `completionBotId` del `TaskInfo` objeto. El cuerpo de la tarjeta adaptable tal como lo rellena el usuario se envía al bot mediante un mensaje cuando el usuario `task/submit invoke` selecciona un `Action.Submit` botón. El esquema del objeto que recibe es muy similar al esquema que recibe para los mensajes [task/fetch y task/submit](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages). La única diferencia es que el esquema del objeto JSON es un objeto Adaptive Card en lugar de un objeto que contiene un objeto Adaptive Card como cuando se usan [tarjetas adaptables](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)con bots .

En la siguiente sección se muestra un ejemplo de envío del resultado de un módulo de tareas.

## <a name="example-of-submitting-the-result-of-a-task-module"></a>Ejemplo de envío del resultado de un módulo de tareas

Para obtener más información, vea el [formulario HTML en el módulo de tareas](#example-of-invoking-a-task-module). En el siguiente código se muestra un ejemplo de dónde se define el formulario:

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

Hay cinco campos en este formulario, pero para este ejemplo solo se requieren tres valores, `name` , `email` y `favoriteBook` .

El siguiente código proporciona un ejemplo de la `validateForm()` función que llama a `submitTask()` :

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

La siguiente sección proporciona problemas de invocación de módulo de tareas y sus mensajes de error.

## <a name="task-module-invocation-errors"></a>Errores de invocación de módulos de tareas

En la tabla siguiente se proporcionan los valores posibles `err` que puede recibir su `submitHandler` :

| Problema | Mensaje de error que es el valor de `err` |
| ------- | ------------------------------ |
| Valores para ambos `TaskInfo.url` y `TaskInfo.card` se especificaron. | Se especificaron valores para la tarjeta y la dirección URL. Uno u otro, pero no ambos, están permitidos. |
| No `TaskInfo.url` se especifica ni se `TaskInfo.card` especifica. | Debe especificar un valor para la tarjeta o la dirección URL. |
| No es `appId` válido . | Id. de aplicación no válido. |
| El usuario seleccionó el botón X y lo cerró. | El usuario canceló o cerró el módulo de tareas. |

## <a name="code-sample"></a>Ejemplo de código

|Ejemplo de nombre | Descripción | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Fichas de ejemplo del módulo de tareas y bots-V3 | Ejemplos para crear módulos de tareas. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 

## <a name="see-also"></a>Consulte también

[Invocar y descartar módulos de tareas](~/task-modules-and-cards/task-modules/invoking-task-modules.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Uso de módulos de tareas desde bots](~/task-modules-and-cards/task-modules/task-modules-bots.md)

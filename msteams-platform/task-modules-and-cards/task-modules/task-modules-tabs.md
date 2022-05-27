---
title: Usar módulos de tareas en pestañas de Microsoft Teams
description: Explica cómo invocar módulos de tareas desde pestañas de Teams y enviar su resultado mediante el SDK de cliente de Microsoft Teams. Incluye ejemplos de código.
ms.localizationpriority: medium
ms.topic: how-to
keywords: SDK de cliente de pestañas de teams de módulos de tareas
ms.openlocfilehash: 61955a9afd070a17b17210239054819f02d3b484
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2022
ms.locfileid: "65756699"
---
# <a name="use-task-modules-in-tabs"></a>Uso de módulos de tareas en pestañas

Agregue un módulo de tareas a la pestaña para simplificar la experiencia del usuario para cualquier flujo de trabajo que requiera entrada de datos. Los módulos de tareas le permiten recopilar sus entradas en un elemento emergente compatible con Microsoft Teams. Un buen ejemplo de ello es la edición de tarjetas de Planner. Puede usar módulos de tareas para crear una experiencia similar.

Para admitir la funcionalidad de módulo de tareas, se agregan dos funciones nuevas al SDK de cliente de [Teams](/javascript/api/overview/msteams-client). En el código siguiente se muestra un ejemplo de esas dos funciones:

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

Puede ver cómo funciona la invocación de un módulo de tareas desde una pestaña y el envío del resultado de un módulo de tareas.

## <a name="invoke-a-task-module-from-a-tab"></a>Invocación de un módulo de tareas desde una pestaña

Para invocar un módulo de tareas desde una pestaña, use `microsoftTeams.tasks.startTask()` pasar un[ objeto TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) y una función de devolución de llamada `submitHandler` opcional. Hay dos casos que se deben tener en consideración:

* El valor de `TaskInfo.url` se establece en una dirección URL. Aparece la ventana del módulo de tareas y `TaskModule.url` se carga como un `<iframe>` dentro de ella. JavaScript en esa página llama a `microsoftTeams.initialize()`. Si hay una `submitHandler` función en la página y hay un error al invocar `microsoftTeams.tasks.startTask()`, `submitHandler` se invoca con `err` establecido en la cadena de error que indica lo mismo. Para obtener más información, vea [errores de invocación del módulo de tareas](#task-module-invocation-errors).
* El valor de `taskInfo.card` es el [JSON de una tarjeta adaptable](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment). No hay ninguna función de JavaScript `submitHandler` a la que llamar cuando el usuario cierre o presione un botón en la tarjeta adaptable. La única manera de recibir lo que el usuario especificó es pasando el resultado a un bot. Para usar un módulo de tareas de tarjeta adaptable desde una pestaña, la aplicación debe incluir un bot para obtener cualquier respuesta del usuario.

En la sección siguiente se proporciona un ejemplo de invocación de un módulo de tareas.

## <a name="example-of-invoking-a-task-module"></a>Ejemplo de invocación de un módulo de tareas

En la imagen siguiente se muestra el módulo de tareas:

:::image type="content" source="../../assets/images/task-module/task-module-custom-form.png" alt-text="Formulario personalizado del módulo de tareas":::

El código siguiente se adapta de [el ejemplo de módulo de tareas](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample):

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

`submitHandler` Es simple y se hace eco del valor de `err` o `result` de la consola.

## <a name="submit-the-result-of-a-task-module"></a>Enviar el resultado de un módulo de tareas

La función `submitHandler` reside en la página web de `TaskInfo.url` y se usa con `TaskInfo.url`. Si se produce un error al invocar el módulo de tareas, `submitHandler` la función se invoca inmediatamente con una `err` cadena que indica qué [error se produjo](#task-module-invocation-errors). También se llama a la función `submitHandler` con una cadena `err` cuando el usuario selecciona X en la esquina superior derecha del módulo de tareas para cerrarla.

Si no hay ningún error de invocación y el usuario no selecciona X para descartarlo, el usuario elige un botón cuando termine. En función de si se trata de una dirección URL o una tarjeta adaptable en el módulo de tareas, las secciones siguientes proporcionan detalles sobre lo que ocurre.

### <a name="html-or-javascript-taskinfourl"></a>`TaskInfo.url` HTML o JavaScript

Después de validar las entradas del usuario, llame a la función del SDK de `microsoftTeams.tasks.submitTask()` denominada `submitTask()`. Llame a `submitTask()` sin parámetros si solo desea que Teams cierre el módulo de tareas. Puede pasar un objeto o una cadena al `submitHandler`.

Pase el resultado como primer parámetro. Teams invoca `submitHandler` donde `err` es `null` y `result` es el objeto o la cadena que usted ha pasado a `submitTask()`. Si llama`submitTask()` con un `result` parámetro, debe pasar una `appId` o una matriz de `appId` cadenas. Esto permite a Teams validar que la aplicación que envía el resultado es la misma que el módulo de tareas invocado.

### <a name="adaptive-card-taskinfocard"></a>`TaskInfo.card` Tarjeta adaptable

Cuando se invoca el módulo de tareas con un `submitHandler` y el usuario selecciona un botón `Action.Submit`, los valores de la tarjeta se devuelven como el valor de `result`. Si el usuario selecciona la tecla Esc o X en la parte superior derecha, se devuelve `err` en su lugar. Si la aplicación contiene un bot además de una pestaña, puede incluir el `appId` del bot como el valor de `completionBotId` en el `TaskInfo` objeto . El cuerpo de la tarjeta adaptable rellenado por el usuario se envía al bot mediante un mensaje de `task/submit invoke` cuando el usuario selecciona un botón de `Action.Submit`. El esquema del objeto que recibe es similar al [esquema que recibe para los mensajes task/fetch y task/submit](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages). La única diferencia es que el esquema del objeto JSON es un objeto de tarjeta adaptable en lugar de un objeto que contiene un objeto de tarjeta adaptable como [cuando se usan tarjetas adaptables con bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).

En la sección siguiente se proporciona un ejemplo de envío del resultado de un módulo de tareas.

## <a name="example-of-submitting-the-result-of-a-task-module"></a>Ejemplo de envío del resultado de un módulo de tareas

Para obtener más información, vea el formulario HTML de [en el módulo de tareas](#example-of-invoking-a-task-module). El código siguiente proporciona un ejemplo de dónde se define el formulario:

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

Hay cinco campos en este formulario, pero para este ejemplo solo se requieren tres valores, `name`, `email`y `favoriteBook`.

El código siguiente proporciona un ejemplo de la función `validateForm()` que llama a `submitTask()`:

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

En la sección siguiente se proporcionan problemas de invocación del módulo de tareas y sus mensajes de error.

## <a name="task-module-invocation-errors"></a>Errores de invocación de módulos de tareas

En la tabla siguiente se proporcionan los valores posibles de `err` que puede recibir su `submitHandler`:

| Problema | Mensaje de error que es el valor de `err` |
| ------- | ------------------------------ |
| Se especificaron valores para `TaskInfo.url` y `TaskInfo.card`. | Se especificaron valores para la tarjeta y la dirección URL. Se permiten una u otra, pero no ambos elementos. |
| No se especificó `TaskInfo.url` ni `TaskInfo.card`. | Debe especificar un valor para la tarjeta o la dirección URL. |
| `appId`No válido. | Id. de aplicación no válido. |
| El usuario seleccionó el botón X y lo cerró. | El usuario canceló o cerró el módulo de tareas. |

## <a name="code-sample"></a>Ejemplo de código

|Ejemplo de nombre | Descripción | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Pestañas y bots de ejemplo del módulo de tareas-V3 | Ejemplos para crear módulos de tareas. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Uso de módulos de tareas de bots](~/task-modules-and-cards/task-modules/task-modules-bots.md)

## <a name="see-also"></a>Consulte también

[Invocar y descartar módulos de tareas](~/task-modules-and-cards/task-modules/invoking-task-modules.md)

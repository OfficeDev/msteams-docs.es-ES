---
title: Uso de módulos de tareas en pestañas de Microsoft Teams
description: Explica cómo invocar módulos de tareas desde Teams pestañas y enviar su resultado mediante el SDK de cliente de Microsoft Teams. Incluye ejemplos de código.
ms.localizationpriority: medium
ms.topic: how-to
keywords: módulos de tarea teams tabs client sdk
ms.openlocfilehash: 63ac1df5b9cdbbba46ba204103a9a5c989b3a323
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073763"
---
# <a name="use-task-modules-in-tabs"></a>Uso de módulos de tareas en pestañas

Agregue un módulo de tareas a la pestaña para simplificar la experiencia del usuario para cualquier flujo de trabajo que requiera entrada de datos. Los módulos de tareas le permiten recopilar su entrada en un elemento emergente de Microsoft Teams-Aware. Un buen ejemplo de esto es la edición de tarjetas de Planner. Puede usar módulos de tareas para crear una experiencia similar.

Para admitir la característica de módulo de tareas, se agregan dos nuevas funciones al [SDK de cliente Teams](/javascript/api/overview/msteams-client). En el código siguiente se muestra un ejemplo de estas dos funciones:

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

Para invocar un módulo de tareas desde una pestaña, use `microsoftTeams.tasks.startTask()` pasar un [objeto TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) y una función de devolución de llamada opcional `submitHandler` . Hay dos casos a tener en cuenta:

* El valor de `TaskInfo.url` se establece en una dirección URL. Aparece la ventana del módulo de tareas y `TaskModule.url` se carga como una `<iframe>` dentro de ella. JavaScript en esa página llama a `microsoftTeams.initialize()`. Si hay una `submitHandler` función en la página y hay un error al invocar `microsoftTeams.tasks.startTask()`, `submitHandler` se invoca con `err` establecido en la cadena de error que indica lo mismo. Para obtener más información, vea [Errores de invocación del módulo de tareas](#task-module-invocation-errors).
* El valor de `taskInfo.card` es el [JSON de una tarjeta adaptable](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment). No hay ninguna función de JavaScript `submitHandler` a la que llamar cuando el usuario cierra o presiona un botón en la tarjeta adaptable. La única manera de recibir lo que el usuario especificó es pasando el resultado a un bot. Para usar un módulo de tareas tarjeta adaptable desde una pestaña, la aplicación debe incluir un bot para obtener cualquier respuesta del usuario.

En la sección siguiente se proporciona un ejemplo de invocación de un módulo de tareas.

## <a name="example-of-invoking-a-task-module"></a>Ejemplo de invocación de un módulo de tareas

En la imagen siguiente se muestra el módulo de tareas:

:::image type="content" source="../../assets/images/task-module/task-module-custom-form.png" alt-text="Formulario personalizado del módulo de tareas":::

El código siguiente se adapta a partir [del ejemplo del módulo de tareas](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample):

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

es `submitHandler` muy simple y se hace eco del valor de `err` o `result` de la consola.

## <a name="submit-the-result-of-a-task-module"></a>Envío del resultado de un módulo de tareas

La `submitHandler` función reside en la `TaskInfo.url` página web y se usa con `TaskInfo.url`. Si se produce un error al invocar el módulo de tareas, `submitHandler` la función se invoca inmediatamente con una `err` cadena que indica qué [error se produjo](#task-module-invocation-errors). También `submitHandler` se llama a la función con una `err` cadena cuando el usuario selecciona X en la esquina superior derecha del módulo de tareas para cerrarla.

Si no hay ningún error de invocación y el usuario no selecciona X para descartarlo, el usuario elige un botón cuando termine. En función de si se trata de una dirección URL o una tarjeta adaptable en el módulo de tareas, en las secciones siguientes se proporcionan detalles sobre lo que ocurre.

### <a name="html-or-javascript-taskinfourl"></a>HTML o JavaScript `TaskInfo.url`

Después de validar las entradas del usuario, llame a la función del `microsoftTeams.tasks.submitTask()` SDK denominada `submitTask()`. Llame a `submitTask()` sin parámetros si solo desea Teams cerrar el módulo de tareas. Puede pasar un objeto o una cadena a `submitHandler`.

Pase el resultado como primer parámetro. Teams invoca `submitHandler` dónde `err` está `null` y `result` es el objeto o cadena que se ha pasado a `submitTask()`. Si llama a `submitTask()` con un `result` parámetro, debe pasar una `appId` matriz de `appId` cadenas o . Esto permite Teams validar que la aplicación que envía el resultado es igual que el módulo de tareas invocado.

### <a name="adaptive-card-taskinfocard"></a>Tarjeta adaptable `TaskInfo.card`

Al invocar el módulo de tareas con y `submitHandler` el usuario selecciona un `Action.Submit` botón, los valores de la tarjeta se devuelven como el valor de `result`. Si el usuario selecciona la tecla Esc o X en la parte superior derecha, `err` se devuelve en su lugar. Si la aplicación contiene un bot además de una pestaña, puede incluir simplemente el `appId` del bot como el valor de `completionBotId` en el `TaskInfo` objeto . El cuerpo de la tarjeta adaptable rellenada por el usuario se envía al bot mediante un `task/submit invoke` mensaje cuando el usuario selecciona un `Action.Submit` botón. El esquema del objeto que recibe es muy similar al [esquema que recibe para los mensajes task/fetch y task/submit](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages). La única diferencia es que el esquema del objeto JSON es un objeto de tarjeta adaptable en lugar de un objeto que contiene un objeto de tarjeta adaptable como [cuando se usan tarjetas adaptables con bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).

En la sección siguiente se proporciona un ejemplo de envío del resultado de un módulo de tareas.

## <a name="example-of-submitting-the-result-of-a-task-module"></a>Ejemplo de envío del resultado de un módulo de tareas

Para obtener más información, vea el [formulario HTML en el módulo de tareas](#example-of-invoking-a-task-module). El código siguiente proporciona un ejemplo de dónde se define el formulario:

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

Hay cinco campos en este formulario, pero en este ejemplo solo se requieren tres valores, `name`, `email`y `favoriteBook`.

El código siguiente proporciona un ejemplo de la `validateForm()` función que llama a `submitTask()`:

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

En la tabla siguiente se proporcionan los valores posibles de `err` que puede recibir `submitHandler`:

| Problema | Mensaje de error que es el valor de `err` |
| ------- | ------------------------------ |
| Se especificaron valores para `TaskInfo.url` y `TaskInfo.card` . | Se especificaron valores para la tarjeta y la dirección URL. Se permiten una u otra, pero no ambas. |
| Ni se `TaskInfo.url` `TaskInfo.card` especifica. | Debe especificar un valor para la tarjeta o la dirección URL. |
| No es válido `appId`. | Identificador de aplicación no válido. |
| Botón X seleccionado por el usuario, cerrando. | El usuario canceló o cerró el módulo de tareas. |

## <a name="code-sample"></a>Ejemplo de código

|Ejemplo de nombre | Descripción | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Pestañas y bots de ejemplo del módulo de tareas-V3 | Ejemplos para crear módulos de tareas. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Uso de módulos de tareas de bots](~/task-modules-and-cards/task-modules/task-modules-bots.md)

## <a name="see-also"></a>Ver también

[Invocar y descartar módulos de tareas](~/task-modules-and-cards/task-modules/invoking-task-modules.md)

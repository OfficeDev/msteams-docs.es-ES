---
title: Utilizar módulos de tareas en los bots de Microsoft Teams
description: Aprenda a usar módulos de tareas con bots de Microsoft Teams, incluidas tarjetas de Bot Framework, tarjetas adaptables y vínculos profundos.
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: e7bed83d9f13913b9a72997ac3679f844db3034a
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142986"
---
# <a name="use-task-modules-from-bots"></a>Uso de módulos de tareas desde los bots

Los módulos de tareas se pueden invocar desde Microsoft Teams bots mediante botones en tarjetas adaptables y tarjetas de Bot Framework que son hero, thumbnail y Office 365 Connector. Los módulos de tareas suelen ser una mejor experiencia para el usuario que los múltiples pasos de conversación. Realizar un seguimiento del estado del bot y permitir al usuario interrumpir o cancelar la secuencia.

Hay dos formas de invocar los módulos de tareas:

* Un nuevo mensaje `task/fetch`de invocación: el uso de la `invoke` [acción de tarjeta](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) para las tarjetas de Bot Framework o la `Action.Submit` [acción de tarjeta](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) para tarjetas adaptables, con `task/fetch`, el módulo de tareas una dirección URL o una tarjeta adaptable se captura dinámicamente desde el bot.
* URL de vínculo profundo: utilizando la [sintaxis de vínculo profundo para los módulos de tareas](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax), puede utilizar la `openUrl` [acción de tarjeta](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl) para las tarjetas de Bot Framework o la`Action.OpenUrl` [acción de tarjeta](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) para las tarjetas adaptables, respectivamente. Con las URL de vínculos profundos, la URL del módulo de tareas o el cuerpo de la tarjeta adaptable ya se conocen para evitar un viaje de ida y vuelta del servidor en relación con `task/fetch`.

> [!IMPORTANT]
> Cada `url` y `fallbackUrl` debe implementar el protocolo de encriptación HTTPS.

La siguiente sección proporciona detalles sobre la invocación de un módulo de tareas utilizando `task/fetch`.

## <a name="invoke-a-task-module-using-taskfetch"></a>Invocar un módulo de tareas mediante tarea/recuperar

Cuando el `value` objeto de la `invoke` acción de la tarjeta o `Action.Submit` se inicializa y cuando un usuario selecciona el botón, se envía un `invoke` mensaje al bot. En la respuesta HTTP al `invoke` mensaje, hay un [objeto TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) incrustado en un objeto contenedor, que Teams usa para mostrar el módulo de tareas.

:::image type="content" source="../../assets/images/task-module/task-module-invoke-request-response.png" alt-text="solicitud o respuesta a tarea/recuperar opción recuperar tarea":::

En los pasos siguientes se proporciona el módulo de tareas invoke mediante task/fetch:

1. Esta imagen muestra una carta de elemento principal del Bot Framework con una **acción de cartas de** `invoke`[Compras](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke). El valor de la `type` propiedad es `task/fetch` y el resto del `value` objeto puede ser de su elección.
1. El bot recibe el mensaje `invoke` HTTP POST.
1. El bot crea un objeto de respuesta y lo devuelve en el cuerpo de la respuesta POST con un código de respuesta HTTP 200. Para obtener más información sobre el esquema de las respuestas, consulte [la discusión sobre la opción tarea/enviar](#the-flexibility-of-tasksubmit). El siguiente código proporciona un ejemplo de cuerpo de la respuesta HTTP que contiene un [objeto TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) incrustado en un objeto contenedor:

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

    El `task/fetch` evento y su respuesta para los bots es similar a la `microsoftTeams.tasks.startTask()` función en el SDK del cliente.

1. Microsoft Teams muestra el módulo de tareas.

La siguiente sección proporciona detalles sobre la presentación del resultado de un módulo de tareas.

## <a name="submit-the-result-of-a-task-module"></a>Enviar el resultado de un módulo de tareas

Cuando el usuario termina con el módulo de tareas, el envío del resultado al bot es similar a la forma en que funciona con las pestañas.. Para obtener más información, consulte [ejemplo de envío del resultado de un módulo de tareas](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module). Hay algunas diferencias como las siguientes:

* HTML o JavaScript que es `TaskInfo.url`: una vez que haya validado lo que el usuario ha especificado, llame a la función del SDK a la `microsoftTeams.tasks.submitTask()` que se hace referencia en lo sucesivo con `submitTask()` fines de legibilidad. Puede llamar `submitTask()` sin ningún parámetro si quiere que Teams cierre el módulo de tareas, pero debe pasar un objeto o una cadena a su `submitHandler`.  Páselo como primer parámetro, `result`. Teams invoca `submitHandler`, `err`es `null`, y `result` es el objeto o la cadena que se ha pasado a `submitTask()`. Si llama`submitTask()` con un `result` parámetro, debe pasar una `appId` o una matriz de `appId` cadenas. Esto permite Teams validar que la aplicación que envía el resultado es la misma, que invocó el módulo de tareas. Tu bot recibe un `task/submit`mensaje que incluye `result`. Para obtener más información, consulte [carga de `task/fetch` y `task/submit` los mensajes](#payload-of-taskfetch-and-tasksubmit-messages).
* Tarjeta adaptable que es `TaskInfo.card`: el cuerpo de la tarjeta adaptable rellenado por el usuario se envía al bot a través de un `task/submit` mensaje cuando el usuario selecciona cualquier `Action.Submit` botón.

La siguiente sección ofrece detalles sobre la flexibilidad de `task/submit`.

## <a name="the-flexibility-of-tasksubmit"></a>La flexibilidad de tarea/enviar

Cuando el usuario termina con un módulo de tarea invocado desde un bot, éste siempre recibe un `task/submit invoke` mensaje. A la hora de responder al `task/submit` mensaje, tiene varias opciones, como se indica a continuación:

| Respuesta del cuerpo HTTP                      | Escenario                                |
| --------------------------------------- | --------------------------------------- |
| Ninguno omite el `task/submit` mensaje | La respuesta más sencilla es no responder. No es necesario que el bot responda cuando el usuario haya terminado con el módulo de tareas. |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teams muestra el valor de `value` en un cuadro de mensaje emergente. |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | Permite encadenar secuencias de tarjetas adaptables en una experiencia de asistente o de varios pasos. |

> [!NOTE]
> Encadenamiento de tarjetas adaptables en una secuencia es un escenario avanzado. La aplicación de ejemplo Node.js lo admite. Para obtener más información, consulte [Módulo de tareas de Microsoft Teams Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes).

La siguiente sección proporciona detalles sobre la carga de `task/fetch` y `task/submit` los mensajes.

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>Carga útil de mensajes de tarea/recuperar y tarea/enviar

Esta sección define el esquema de lo que recibe su bot cuando recibe un `task/fetch` o `task/submit` objeto de Bot Framework`Activity`. La siguiente tabla proporciona las propiedades de la carga de `task/fetch` y `task/submit` los mensajes:

| Propiedad | Descripción                          |
| -------- | ------------------------------------ |
| `type`   | Siempre es `invoke`.           |
| `name`   | Es `task/fetch` o `task/submit`. |
| `value`  | Es la carga definida por el desarrollador. La estructura del `value` objeto es la misma que se envía desde Teams. En este caso, sin embargo, es diferente. Requiere compatibilidad con la recuperación dinámica que procede `task/fetch` de Bot Framework, que es `value` y acciones de tarjeta `Action.Submit` adaptable, que es `data`. Es necesario una forma de comunicar de Teams `context` al bot además de lo que se incluye en`value` o `data`.<br/><br/>Combina "valor" y "datos" en un objeto primario:<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

La siguiente sección proporciona un ejemplo de recepción y respuesta a `task/fetch` y `task/submit` de mensajes de invocación en Node.js.

## <a name="example-of-taskfetch-and-tasksubmit-invoke-messages-in-nodejs-and-c"></a>Ejemplo de mensajes de invocación tarea/recuperar y tarea/enviar en Node.js y C#

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```typescript
handleTeamsTaskModuleFetch(context, taskModuleRequest) {
    // Called when the user selects an options from the displayed HeroCard or
    // AdaptiveCard.  The result is the action to perform.

    const cardTaskFetchValue = taskModuleRequest.data.data;
    var taskInfo = {}; // TaskModuleTaskInfo

    if (cardTaskFetchValue === TaskModuleIds.YouTube) {
        // Display the YouTube.html page
        taskInfo.url = taskInfo.fallbackUrl = this.baseUrl + '/' + TaskModuleIds.YouTube + '.html';
        this.setTaskInfo(taskInfo, TaskModuleUIConstants.YouTube);
    } else if (cardTaskFetchValue === TaskModuleIds.CustomForm) {
        // Display the CustomForm.html page, and post the form data back via
        // handleTeamsTaskModuleSubmit.
        taskInfo.url = taskInfo.fallbackUrl = this.baseUrl + '/' + TaskModuleIds.CustomForm + '.html';
        this.setTaskInfo(taskInfo, TaskModuleUIConstants.CustomForm);
    } else if (cardTaskFetchValue === TaskModuleIds.AdaptiveCard) {
        // Display an AdaptiveCard to prompt user for text, and post it back via
        // handleTeamsTaskModuleSubmit.
        taskInfo.card = this.createAdaptiveCardAttachment();
        this.setTaskInfo(taskInfo, TaskModuleUIConstants.AdaptiveCard);
    }

    return TaskModuleResponseFactory.toTaskModuleResponse(taskInfo);
}

async handleTeamsTaskModuleSubmit(context, taskModuleRequest) {
    // Called when data is being returned from the selected option (see `handleTeamsTaskModuleFetch').

    // Echo the users input back.  In a production bot, this is where you'd add behavior in
    // response to the input.
    await context.sendActivity(MessageFactory.text('handleTeamsTaskModuleSubmit: ' + JSON.stringify(taskModuleRequest.data)));

    // Return TaskModuleResponse
    return {
        // TaskModuleMessageResponse
        task: {
            type: 'message',
            value: 'Thanks!'
        }
    };
}

setTaskInfo(taskInfo, uiSettings) {
    taskInfo.height = uiSettings.height;
    taskInfo.width = uiSettings.width;
    taskInfo.title = uiSettings.title;
}
```

# <a name="c"></a>[C#](#tab/csharp)

```csharp
protected override Task<TaskModuleResponse> OnTeamsTaskModuleFetchAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
{
    var asJobject = JObject.FromObject(taskModuleRequest.Data);
    var value = asJobject.ToObject<CardTaskFetchValue<string>>()?.Data;

    var taskInfo = new TaskModuleTaskInfo();
    switch (value)
    {
        case TaskModuleIds.YouTube:
            taskInfo.Url = taskInfo.FallbackUrl = _baseUrl + "/" + TaskModuleIds.YouTube;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.YouTube);
            break;
        case TaskModuleIds.CustomForm:
            taskInfo.Url = taskInfo.FallbackUrl = _baseUrl + "/" + TaskModuleIds.CustomForm;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.CustomForm);
            break;
        case TaskModuleIds.AdaptiveCard:
            taskInfo.Card = CreateAdaptiveCardAttachment();
            SetTaskInfo(taskInfo, TaskModuleUIConstants.AdaptiveCard);
            break;
        default:
            break;
    }

    return Task.FromResult(taskInfo.ToTaskModuleResponse());
}

protected override async Task<TaskModuleResponse> OnTeamsTaskModuleSubmitAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
{
    var reply = MessageFactory.Text("OnTeamsTaskModuleSubmitAsync Value: " + JsonConvert.SerializeObject(taskModuleRequest));
    await turnContext.SendActivityAsync(reply, cancellationToken);

    return TaskModuleResponseFactory.CreateResponse("Thanks!");
}

private static void SetTaskInfo(TaskModuleTaskInfo taskInfo, UISettings uIConstants)
{
    taskInfo.Height = uIConstants.Height;
    taskInfo.Width = uIConstants.Width;
    taskInfo.Title = uIConstants.Title.ToString();
}
```

---

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Acciones de tarjeta de Bot Framework vs. Acciones de tarjeta adaptable. Enviar acciones

El esquema de las acciones de la tarjeta del Bot Framework es diferente al de las acciones de la tarjeta adaptable `Action.Submit` y la forma de invocar los módulos de tareas también es diferente. El `data` objeto de `Action.Submit` contiene un `msteams` objeto para que no interfiera con otras propiedades de la tarjeta. La siguiente tabla muestra un ejemplo de cada acción de la tarjeta:

| Acción de la tarjeta de Bot Framework                              | Acción de tarjeta adaptable. Enviar acción                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="code-sample"></a>Ejemplo de código

|Ejemplo de nombre | Descripción | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Módulo de tareas de muestra bots-V4 | Ejemplos para crear módulos de tareas. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="step-by-step-guide"></a>Guía paso a paso

Siga la [guía paso a paso](../../sbs-botbuilder-taskmodule.yml) para crear y obtener el bot del módulo de tareas en Teams.

## <a name="see-also"></a>Consulte también

* [Código de ejemplo del módulo de tareas de Microsoft Teams en Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [Ejemplos de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)

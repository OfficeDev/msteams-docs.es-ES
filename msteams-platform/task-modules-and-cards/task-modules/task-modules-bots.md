---
title: Usar módulos de tareas en Microsoft Teams bots
description: Cómo usar módulos de tareas con Microsoft Teams bots, incluidas las tarjetas bot Framework, las tarjetas adaptables y los vínculos profundos.
ms.localizationpriority: medium
ms.topic: how-to
keywords: módulos de tareas teams bots deep links adaptive card
ms.openlocfilehash: 39df7f3845cc11e6e15da03c72b0c792a795af35
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2022
ms.locfileid: "63355723"
---
# <a name="use-task-modules-from-bots"></a>Uso de módulos de tareas desde los bots
 
Los módulos de tareas se pueden invocar desde Microsoft Teams bots usando botones en tarjetas adaptables y tarjetas de Bot Framework que son principales, miniaturas y Office 365 Connector. Los módulos de tareas suelen ser una mejor experiencia de usuario que varios pasos de conversación. Realice un seguimiento del estado del bot y permita al usuario interrumpir o cancelar la secuencia.

Hay dos formas de invocar módulos de tareas:

* Un nuevo tipo de mensaje de invocación: `invoke` el uso de la acción de tarjeta para las tarjetas [](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) de Bot Framework o `Action.Submit` la acción de tarjeta para tarjetas adaptables, [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) `task/fetch`con , módulo de tarea, ya sea una dirección URL o una tarjeta adaptable, se captura dinámicamente desde el bot.`task/fetch`
* Direcciones URL de vínculo profundo: mediante la sintaxis de vínculo profundo para módulos [](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl) de [tareas,](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)`openUrl` puede usar la acción de tarjeta para tarjetas de Bot Framework [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) `Action.OpenUrl` o la acción de tarjeta para tarjetas adaptables, respectivamente. Con las direcciones URL de vínculo profundo, ya se sabe que la dirección URL del módulo de tareas o el cuerpo de la tarjeta adaptable evitan un recorrido de ida y vuelta del servidor con relación a `task/fetch`.

> [!IMPORTANT]
> Cada uno `url` y `fallbackUrl` debe implementar el protocolo de cifrado HTTPS.

En la siguiente sección se proporcionan detalles sobre cómo invocar un módulo de tareas mediante `task/fetch`.

## <a name="invoke-a-task-module-using-taskfetch"></a>Invocar un módulo de tareas mediante task/fetch

Cuando el `value` objeto de la acción `invoke` de tarjeta `Action.Submit` o se inicializa y cuando un usuario selecciona el botón, `invoke` se envía un mensaje al bot. En la respuesta HTTP `invoke` al mensaje, hay un objeto [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) incrustado en un objeto contenedor, que Teams usa para mostrar el módulo de tareas.

![solicitud o respuesta task/fetch](~/assets/images/task-module/task-module-invoke-request-response.png)

Los pasos siguientes proporcionan el módulo de tareas de invocación mediante task/fetch:

1. Esta imagen muestra una tarjeta principal de Bot Framework con una **acción Comprar** `invoke` [tarjeta](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke). El valor de la propiedad `type` es `task/fetch` y el resto del `value` objeto puede ser de su elección.
1. El bot recibe el mensaje `invoke` HTTP POST.
1. El bot crea un objeto de respuesta y lo devuelve en el cuerpo de la respuesta POST con un código de respuesta HTTP 200. Para obtener más información sobre el esquema de respuestas, vea [la discusión sobre la tarea o el envío](#the-flexibility-of-tasksubmit). El siguiente código proporciona un ejemplo de cuerpo de la respuesta HTTP que contiene un [objeto TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) incrustado en un objeto contenedor:

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

    El `task/fetch` evento y su respuesta para bots es similar a la `microsoftTeams.tasks.startTask()` función del SDK de cliente.

1. Microsoft Teams muestra el módulo de tareas.

En la siguiente sección se proporcionan detalles sobre cómo enviar el resultado de un módulo de tareas.

## <a name="submit-the-result-of-a-task-module"></a>Enviar el resultado de un módulo de tareas

Cuando el usuario ha terminado con el módulo de tareas, enviar el resultado de vuelta al bot es similar a la forma en que funciona con las pestañas. Para obtener más información, vea [el ejemplo de envío del resultado de un módulo de tareas](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module). Hay algunas diferencias como se muestra a continuación:

* HTML o JavaScript `TaskInfo.url`es decir: una vez validado lo que el usuario ha escrito, `microsoftTeams.tasks.submitTask()` se llama a la función SDK `submitTask()` a la que se hace referencia a continuación con fines de legibilidad. Puede llamar sin `submitTask()` ningún parámetro si desea Teams cerrar el módulo de tareas, pero debe pasar un objeto o una cadena a su `submitHandler`. Pásalo como primer parámetro, `result`. Teams invoca `submitHandler`, `err` es `null`y `result` es el objeto o cadena que se pasó a `submitTask()`. Si llama con `submitTask()` un parámetro `result` , debe pasar una `appId` o una matriz de `appId` cadenas. Esto permite Teams validar que la aplicación que envía el resultado es la misma que invocó el módulo de tareas. El bot recibe un mensaje `task/submit` que incluye `result`. Para obtener más información, vea [payload of `task/fetch` and `task/submit` messages](#payload-of-taskfetch-and-tasksubmit-messages).
* Tarjeta adaptable que es `TaskInfo.card`: el cuerpo de la tarjeta adaptable tal como lo rellena el usuario se envía al bot a `task/submit` través de un mensaje cuando el usuario selecciona cualquier `Action.Submit` botón.

En la siguiente sección se proporcionan detalles sobre la flexibilidad de `task/submit`.

## <a name="the-flexibility-of-tasksubmit"></a>Flexibilidad de tarea/envío

Cuando el usuario termina con un módulo de tareas invocado desde un bot, el bot siempre recibe un `task/submit invoke` mensaje. Tiene varias opciones al responder al `task/submit` mensaje de la siguiente manera:

| Respuesta del cuerpo HTTP                      | Escenario                                |
| --------------------------------------- | --------------------------------------- |
| Ninguno omite el `task/submit` mensaje | La respuesta más sencilla no es ninguna respuesta. No es necesario que el bot responda cuando el usuario haya terminado con el módulo de tareas. |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teams muestra el valor de en `value` un cuadro de mensaje emergente. |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | Permite encadenar secuencias de tarjetas adaptables juntas en una experiencia de asistente o de varios pasos. |

> [!NOTE]
> Encadenar tarjetas adaptables en una secuencia es un escenario avanzado. La Node.js de ejemplo lo admite. Para obtener más información, [vea Microsoft Teams módulo de tareas Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes).

En la siguiente sección se proporcionan detalles sobre la carga de `task/fetch` y los `task/submit` mensajes.

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>Carga de los mensajes task/fetch y task/submit

En esta sección se define el esquema de lo que el bot recibe cuando recibe un objeto `task/fetch` o `task/submit` Bot Framework `Activity` . En la tabla siguiente se proporcionan las propiedades de carga de `task/fetch` y `task/submit` mensajes:

| Propiedad | Descripción                          |
| -------- | ------------------------------------ |
| `type`   | Siempre es `invoke`.           |
| `name`   | Es o `task/fetch` `task/submit`. |
| `value`  | Es la carga definida por el desarrollador. La estructura del objeto `value` es la misma que la que se envía desde Teams. En este caso, sin embargo, es diferente. Requiere compatibilidad con la captura dinámica que es `task/fetch` de Bot Framework, que es `value` y acciones de tarjeta `Action.Submit` adaptable, que es `data`. Se requiere una forma de Teams `context` al bot además de lo que se incluye en `value` o `data`.<br/><br/>Combine "valor" y "datos" en un objeto primario:<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

La siguiente sección proporciona un ejemplo de recepción y respuesta a `task/fetch` `task/submit` e invocar mensajes en Node.js.

## <a name="example-of-taskfetch-and-tasksubmit-invoke-messages-in-nodejs-and-c"></a>Ejemplo de task/fetch y task/submit invoke messages en Node.js y C #

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

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Acciones de tarjeta de Bot Framework frente a acciones Adaptive Card Action.Submit

El esquema de las acciones de tarjeta de Bot Framework es diferente de las acciones de `Action.Submit` tarjeta adaptable y la forma de invocar módulos de tareas también es diferente. El `data` objeto de `Action.Submit` contiene un `msteams` objeto para que no interfiera con otras propiedades de la tarjeta. En la tabla siguiente se muestra un ejemplo de cada acción de tarjeta:

| Acción de tarjeta de Bot Framework                              | Acción Adaptive Card Action.Submit                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="code-sample"></a>Ejemplo de código

|Ejemplo de nombre | Descripción | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Bots de ejemplo de módulo de tareas-V4 | Ejemplos para crear módulos de tareas. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="step-by-step-guide"></a>Guía paso a paso

Siga la [guía paso a paso para](../../sbs-botbuilder-taskmodule.yml) crear y capturar bot de módulo de tareas en Teams.

## <a name="see-also"></a>Vea también

* [Microsoft Teams ejemplo de módulo de tareas en Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [Ejemplos de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)

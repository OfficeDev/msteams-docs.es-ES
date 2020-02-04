---
title: Uso de módulos de tareas en bots de Microsoft Teams
description: Cómo usar los módulos de tareas con los bots de Microsoft Teams, incluidas las tarjetas de Framework de bot, las tarjetas adaptables y los vínculos profundos.
keywords: módulos de tareas bots de Teams
ms.openlocfilehash: 3a0e4591dbb26ff4afa8cc06edc0a03365da0eca
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675911"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a>Uso de módulos de tareas de bots de Microsoft Teams

Los módulos de tareas se pueden invocar desde bots de Microsoft Teams con botones en tarjetas adaptables y tarjetas de entorno de Bot? (Hero, thumbnail y Office 365 Connector). Los módulos de tareas suelen ser una mejor experiencia de usuario que varios pasos de conversación en los que, como desarrollador, tiene que realizar un seguimiento del estado de los robots y permitir al usuario interrumpir/cancelar la secuencia.

Hay dos formas de invocar módulos de tareas:

* **Un nuevo tipo de mensaje `task/fetch`de invocación.** Mediante la `invoke` [acción de tarjeta](~/task-modules-and-cards/cards/cards-actions.md#invoke) de las tarjetas de .NET Framework `Action.Submit` o la [acción de tarjeta](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) para tarjetas `task/fetch`adaptables, con, el módulo de tareas (ya sea una dirección URL o una tarjeta adaptable) se obtiene dinámicamente desde el bot.
* **Direcciones URL de vínculo en profundidad.** Mediante la [Sintaxis de vínculo profundo para módulos de tareas](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax), puede usar `openUrl` la [acción de tarjeta](~/task-modules-and-cards/cards/cards-actions.md#openurl) para las tarjetas de `Action.OpenUrl` bot Framework o la acción de la [tarjeta](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) para tarjetas adaptables, respectivamente. Con las direcciones URL de vínculo en profundidad, la dirección URL del módulo de tareas o el cuerpo de la tarjeta adaptable se conoce obviamente `task/fetch`de antemano, evitando un viaje de ida y vuelta en el servidor con respecto a.

## <a name="invoking-a-task-module-via-taskfetch"></a>Invocación de un módulo de tareas a través de la tarea/obtención

Cuando el `value` objeto de la `invoke` acción de la `Action.Submit` tarjeta o se inicializa de la manera adecuada (explicado con más detalle a continuación), cuando un usuario presiona `invoke` el botón, se envía un mensaje al bot. En la respuesta HTTP al `invoke` mensaje, hay un [objeto TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) incrustado en un objeto contenedor, que Microsoft Teams usa para mostrar el módulo de tareas.

![solicitud y respuesta de la tarea/obtención](~/assets/images/task-module/task-module-invoke-request-response.png)

Echemos un vistazo a cada paso con un poco más de detalle:

1. En este ejemplo se muestra una tarjeta Hero Framework Hero con una `invoke` [acción de tarjeta](~/task-modules-and-cards/cards/cards-actions.md#invoke)"Buy". El valor de la `type` propiedad es `task/fetch` : el resto del `value` objeto puede ser cualquier cosa que desee.
2. El bot recibe el `invoke` mensaje http post.
3. El bot crea un objeto de respuesta y lo devuelve en el cuerpo de la respuesta POST con un código de respuesta HTTP 200. El esquema de respuestas se describe [a continuación en la discusión sobre la tarea o el envío](#the-flexibility-of-tasksubmit), pero lo importante que debe recordar ahora es que el cuerpo de la respuesta http contiene un [objeto TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) incrustado en un objeto contenedor, por ejemplo:

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
    
    El `task/fetch` evento y su respuesta para bots son similares, conceptualmente, a la `microsoftTeams.tasks.startTask()` función en el SDK del cliente.
4. Microsoft Teams muestra el módulo de tareas.

## <a name="submitting-the-result-of-a-task-module"></a>Enviar el resultado de un módulo de tareas

Cuando el usuario termina con el módulo de tareas, el envío del resultado al bot es similar [a como funciona con las pestañas](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), pero hay algunas diferencias, por lo que también se describe aquí.

* **HTML/JavaScript (`TaskInfo.url`)**. Una vez que haya validado lo que ha escrito el usuario, llame `microsoftTeams.tasks.submitTask()` a la función SDK (denominada a `submitTask()` partir de ahora con fines de legibilidad). Si solo desea `submitTask()` que Microsoft Teams cierre el módulo de tareas, puede llamar a sin ningún parámetro, pero la mayoría de las veces querrá pasar un objeto o una cadena a `submitHandler`su. Simplemente páselo como el primer parámetro, `result`. Microsoft Teams `submitHandler`invocará `err` : `null` será `result` y será el objeto o la cadena que ha `submitTask()`pasado a. Si `submitTask()` llama a con `result` un parámetro, **debe** pasar una `appId` o una matriz de `appId` cadenas: Esto permite a Microsoft Teams validar que la aplicación que envía el resultado es la misma que ha invocado el módulo de tareas. El bot recibirá un `task/submit` mensaje que `result` incluye lo que se describe [a continuación](#payload-of-taskfetch-and-tasksubmit-messages).
* **Tarjeta adaptable`TaskInfo.card`()**. El cuerpo de la tarjeta adaptable (como rellenado por el usuario) se enviará al `task/submit` bot a través de un mensaje `Action.Submit` cuando el usuario presione cualquier botón.

## <a name="the-flexibility-of-tasksubmit"></a>La flexibilidad de la tarea o el envío

En la sección anterior, aprendió que cuando el usuario termina con un módulo de tareas invocado desde un bot, el bot siempre recibe un `task/submit invoke` mensaje. Como desarrollador, tiene varias opciones para *responder* al `task/submit` mensaje:

| Respuesta del cuerpo HTTP                      | Escenario                                |
| --------------------------------------- | --------------------------------------- |
| Ninguno (omitir `task/submit` el mensaje) | La respuesta más sencilla no es ninguna respuesta. No es necesario que el bot responda cuando el usuario haya terminado con el módulo de tareas. |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Microsoft Teams mostrará el valor `value` de en un cuadro de mensaje emergente. |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | Permite "encadenar" secuencias de tarjetas adaptables juntas en un asistente/experiencia de varios pasos. _Tenga en cuenta que encadenar tarjetas adaptables en una secuencia es un escenario avanzado y no se documenta aquí. Sin embargo, la aplicación de ejemplo de node. js lo admite y el modo en que funciona se documenta en [su archivo README.MD](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._ |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>Carga de tarea/búsqueda y mensajes de tarea o envío

En esta sección se define el esquema de lo que el bot recibe cuando `task/fetch` recibe `task/submit` un objeto `Activity` de marco de bot? o. El nivel superior importante aparece a continuación:

| Propiedad | Descripción                          |
| -------- | ------------------------------------ |
| `type`   | Siempre será`invoke`              |
| `name`   | Ya `task/fetch` sea o`task/submit` |
| `value`  | La carga definida por el desarrollador. Normalmente, la estructura del `value` objeto refleja lo que se envió desde Microsoft Teams. En este caso, sin embargo, es diferente porque queremos admitir la recuperación dinámica (`task/fetch`) de bot Framework (`value`) y de las acciones de `Action.Submit` tarjeta adaptable (`data`), y necesitamos una forma de comunicar `context` Teams al bot además de lo que se incluyó `value` / `data`en.<br/><br/>Para ello, se combinan los dos en un objeto primario:<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a>Ejemplo: recibir y responder a la tarea/búsqueda y a la tarea o enviar mensajes de invocación-node. js

La gestión `invoke` de los mensajes en el marco de trabajo de bot puede ser un poco complicada porque no hay soporte formal para ellos en el SDK de bot Framework. Para que sea más fácil, Microsoft Teams ha creado `onInvoke()` funciones auxiliares en el [paquete NPM de botbuilder-Teams (para node. js)](https://www.npmjs.com/package/botbuilder-teams). En este ejemplo se muestra cómo hacerlo:

> [!NOTE]
> El siguiente código de ejemplo se modificó entre Technical Preview y la versión final de esta característica: `task/fetch` el esquema de la solicitud cambió para seguir el que se [documentó en la sección anterior](#payload-of-taskfetch-and-tasksubmit-messages). Es decir, la documentación era correcta, pero la implementación no. Vea los `// for Technical Preview [...]` comentarios a continuación para saber qué ha cambiado.

```typescript
// Handle requests and responses for a "Custom Form" and an "Adaptive card" task module.
// Assumes request is coming from an Adaptive card Action.Submit button that has a "taskModule" property indicating what to invoke
private async onInvoke(event: builder.IEvent, cb: (err: Error, body: any, status?: number) => void): Promise<void> {
    let invokeType = (event as any).name;
    let invokeValue = (event as any).value;
    if (invokeType === undefined) {
        invokeType = null;
    }
    switch (invokeType) {
        case "task/fetch": {
            if (invokeValue !== undefined && invokeValue.data.taskModule === "customform") { // for Technical Preview, was invokeValue.taskModule
                // Return the specified task module response to the bot
                let fetchTemplate: any = {
                    "task": {
                        "type": "continue",
                        "value": {
                            "title": "Custom Form",
                            "height": 510,
                            "width": 430,
                            "fallbackUrl": "https://contoso.com/teamsapp/customform",
                            "url": "https://contoso.com/teamsapp/customform",
                        }
                    }
                };
                cb(null, fetchTemplate, 200);
            };
            if (invokeValue !== undefined && invokeValue.data.taskModule === "adaptivecard") { // for Technical Preview, was invokeValue.taskModule
                let adaptiveCard = {
                    "type": "AdaptiveCard",
                    "body": [
                        {
                            "type": "TextBlock",
                            "text": "Here is a ninja cat:"
                        },
                        {
                            "type": "Image",
                            "url": "http://adaptivecards.io/content/cats/1.png",
                            "size": "Medium"
                        }
                    ],
                    "version": "1.0"
                };
                // Return the specified task module response to the bot
                let fetchTemplate: any = {
                    "task": {
                        "type": "continue",
                        "value": {
                            "title": "Ninja Cat",
                            "height": "small",
                            "width": "small",
                            "card": {
                                contentType: "application/vnd.microsoft.card.adaptive",
                                content: adaptiveCard,
                            }
                        }
                    }
                };
                cb(null, fetchTemplate, 200);
            };
            break;
        }
        case "task/submit": {
            if (invokeValue.data !== undefined) {
                // It's a valid task module response
                let submitResponse: any = {
                    "task": {
                        "type": "message",
                        "value": "Task complete!",
                    }
                };
                cb(null, fetchTemplates.submitMessageResponse, 200)
            }
        }
    }
}
```

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a>Ejemplo: recibir y responder a la tarea/búsqueda y a la tarea o enviar mensajes de invocación-C #

En los bots de `invoke` C#, un `HttpResponseMessage()` controlador que procesa un `Activity` mensaje procesa los mensajes. Las `task/fetch` solicitudes `task/submit` y respuestas de y son JSON. En C#, no es tan cómodo tratar con JSON sin procesar como en node. js, por lo que necesita que las clases de contenedor controlen la serialización a y desde JSON. Aún no hay compatibilidad directa con esto en el SDK de Microsoft Teams [C#](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) , pero puede ver un ejemplo del aspecto que tendrían estas clases de contenedor sencillas en la [aplicación de ejemplo de c#](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).

A continuación se muestra código de ejemplo en `task/fetch` C# `task/submit` para controlar y mensajes mediante estas`TaskInfo`clases `TaskEnvelope`contenedoras (,), extraídos del [ejemplo](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):

```csharp
private HttpResponseMessage HandleInvokeMessages(Activity activity)
{
    var activityValue = activity.Value.ToString();
    if (activity.Name == "task/fetch")
    {
        var action = Newtonsoft.Json.JsonConvert.DeserializeObject<Models.BotFrameworkCardValue<string>>(activityValue);

        Models.TaskInfo taskInfo = GetTaskInfo(action.Data);
        Models.TaskEnvelope taskEnvelope = new Models.TaskEnvelope
        {
            Task = new Models.Task()
            {
                Type = Models.TaskType.Continue,
                TaskInfo = taskInfo
            }
        };
        return Request.CreateResponse(HttpStatusCode.OK, taskEnvelope);
    }
    else if (activity.Name == "task/submit")
    {
        ConnectorClient connector = new ConnectorClient(new Uri(activity.ServiceUrl));
        Activity reply = activity.CreateReply("Received = " + activity.Value.ToString());
        connector.Conversations.ReplyToActivity(reply);
    }
    return new HttpResponseMessage(HttpStatusCode.Accepted);
}

// Helper function for building the TaskInfo object based on the incoming request
private static Models.TaskInfo GetTaskInfo(string actionInfo)
{
    Models.TaskInfo taskInfo = new Models.TaskInfo();
    switch (actionInfo)
    {
        case TaskModuleIds.YouTube:
            taskInfo.Url = taskInfo.FallbackUrl = ApplicationSettings.BaseUrl + "/" + TaskModuleIds.YouTube;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.YouTube);
            break;
        case TaskModuleIds.PowerApp:
            taskInfo.Url = taskInfo.FallbackUrl = ApplicationSettings.BaseUrl + "/" + TaskModuleIds.PowerApp;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.PowerApp);
            break;
        case TaskModuleIds.CustomForm:
            taskInfo.Url = taskInfo.FallbackUrl = ApplicationSettings.BaseUrl + "/" + TaskModuleIds.CustomForm;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.CustomForm);
            break;
        case TaskModuleIds.AdaptiveCard:
            taskInfo.Card = AdaptiveCardHelper.GetAdaptiveCard();
            SetTaskInfo(taskInfo, TaskModuleUIConstants.AdaptiveCard);
            break;
        default:
            break;
    }
    return taskInfo;
}
```

No se muestra en el ejemplo anterior es `SetTaskInfo()` la función, que establece `height`las `width`propiedades, `title` y del `TaskInfo` objeto para cada caso. Este es el [código fuente para SetTaskInfo ()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Las acciones de la tarjeta de bot Framework y la acción de tarjeta adaptable. acciones de envío

El esquema de las acciones de la tarjeta de entorno de bot es `Action.Submit` ligeramente diferente de las acciones de tarjeta adaptable. Como resultado, la manera de invocar módulos de tareas también es ligeramente distinta: `data` el objeto `Action.Submit` de contiene `msteams` un objeto para que no interfiera con otras propiedades de la tarjeta. En la siguiente tabla se muestra un ejemplo de cada uno:

| Acción de la tarjeta de bot Framework                              | Acción de tarjeta adaptable. acción enviar                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

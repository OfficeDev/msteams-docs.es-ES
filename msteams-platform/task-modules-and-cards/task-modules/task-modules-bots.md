---
title: Uso de módulos de tareas en bots Microsoft Teams
description: Cómo usar módulos de tareas con bots Microsoft Teams, incluidas tarjetas Bot Framework, tarjetas adaptables y vínculos profundos
localization_priority: Normal
ms.topic: how-to
keywords: módulos de tareas equipos bots
ms.openlocfilehash: bfaf3dfe791c1736aeb418e2689e513908f04534
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566574"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a>Uso de módulos de tareas de bots Microsoft Teams

Los módulos de tareas se pueden invocar desde Microsoft Teams bots mediante botones en tarjetas adaptables y tarjetas Bot Framework (Conector de héroe, miniatura y Office 365). Los módulos de tareas suelen ser una mejor experiencia de usuario que varios pasos de conversación en los que usted como desarrollador tiene que realizar un seguimiento del estado del bot y permitir al usuario interrumpir o cancelar la secuencia.

Hay dos formas de invocar módulos de tareas:

* **Un nuevo tipo de mensaje de invocación `task/fetch` .** Mediante la `invoke` [acción de tarjeta](~/task-modules-and-cards/cards/cards-actions.md#invoke) para las tarjetas de Bot Framework, o la acción de la `Action.Submit` [tarjeta](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) para tarjetas adaptables, con `task/fetch` , el módulo de tareas (ya sea una DIRECCIÓN URL o una tarjeta adaptable) se obtiene dinámicamente desde el bot.
* **URL de vínculo profundo.** Con la [sintaxis de vínculo profundo para módulos de tareas,](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)puede usar la acción de `openUrl` [tarjeta](~/task-modules-and-cards/cards/cards-actions.md#openurl) para las tarjetas de Bot Framework o la `Action.OpenUrl` [acción de la tarjeta](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) para las tarjetas adaptables, respectivamente. Con las URL de vínculo profundo, la DIRECCIÓN URL del módulo de tareas o el cuerpo de la tarjeta adaptable se conocen obviamente de antemano, evitando un viaje de ida y vuelta del servidor en relación con `task/fetch` .

>[!IMPORTANT]
>Para garantizar comunicaciones seguras, cada `url` uno y debe implementar el protocolo de cifrado `fallbackUrl` HTTPS.

## <a name="invoking-a-task-module-through-taskfetch"></a>Invocar un módulo de tareas a través de tareas/captura

Cuando el `value` objeto de la acción de la tarjeta o se inicializa de `invoke` la manera adecuada `Action.Submit` (explicado con más detalle a continuación), cuando un usuario presiona el botón se envía un `invoke` mensaje al bot. En la respuesta HTTP al `invoke` mensaje, hay un [objeto TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) incrustado en un objeto contenedor, que Teams utiliza para mostrar el módulo de tareas.

![tarea/solicitud de obtención/respuesta](~/assets/images/task-module/task-module-invoke-request-response.png)

Echemos un vistazo a cada paso con un poco más de detalle:

1. En este ejemplo se muestra una tarjeta Bot Framework Hero con una `invoke` [acción de tarjeta](~/task-modules-and-cards/cards/cards-actions.md#invoke)"Comprar". El valor de la `type` propiedad es - el resto del objeto puede ser lo que `task/fetch` `value` quieras.
1. El bot recibe el `invoke` mensaje HTTP POST.
1. El bot crea un objeto de respuesta y lo devuelve en el cuerpo de la respuesta POST con un código de respuesta HTTP 200. El esquema para las respuestas se describe [a continuación en la discusión sobre la tarea/envío](#the-flexibility-of-tasksubmit), pero lo importante que debe recordar ahora es que el cuerpo de la respuesta HTTP contiene un objeto [TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) incrustado en un objeto contenedor. Por ejemplo:

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

    El `task/fetch` evento y su respuesta para bots es similar, conceptualmente, a la función en el SDK de `microsoftTeams.tasks.startTask()` cliente.
1. Microsoft Teams muestra el módulo de tareas.

## <a name="submitting-the-result-of-a-task-module"></a>Envío del resultado de un módulo de tareas

Cuando el usuario ha terminado con el módulo de tareas, enviar el resultado de nuevo al bot es similar [a la forma en que funciona con las pestañas,](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)pero hay algunas diferencias, por lo que se describe aquí también.

* **HTML/JavaScript ( `TaskInfo.url` )**. Una vez que haya validado lo que ha especificado el usuario, llame a la `microsoftTeams.tasks.submitTask()` función SDK (denominada en adelante `submitTask()` para fines de legibilidad). Puede llamar `submitTask()` sin ningún parámetro si solo desea que Teams cierre el módulo de tareas, pero la mayoría de las veces querrá pasar un objeto o una cadena a su `submitHandler` archivo . Simplemente páselo como el primer parámetro, `result` . Teams `submitHandler` invocará: `err` será `null` y será `result` el objeto/cadena al que `submitTask()` pasó. Si llama `submitTask()` con un `result` parámetro, **debe** pasar una `appId` o una matriz de `appId` cadenas: esto permite a Teams validar que la aplicación que envía el resultado es la misma que invocó el módulo de tareas. El bot recibirá un `task/submit` mensaje, incluso `result` como se describe [a continuación.](#payload-of-taskfetch-and-tasksubmit-messages)
* **Tarjeta adaptativa ( `TaskInfo.card` ).** El cuerpo de la tarjeta adaptable (rellenado por el usuario) se enviará al bot a través de un `task/submit` mensaje cuando el usuario presione cualquier `Action.Submit` botón.

## <a name="the-flexibility-of-tasksubmit"></a>La flexibilidad de la tarea/enviar

En la sección anterior, aprendió que cuando el usuario termina con un módulo de tareas invocado desde un bot, el bot siempre recibe un `task/submit invoke` mensaje. Como desarrollador, tiene varias opciones al *responder* al `task/submit` mensaje:

| Respuesta del cuerpo HTTP                      | Escenario                                |
| --------------------------------------- | --------------------------------------- |
| Ninguno (ignore el `task/submit` mensaje) | La respuesta más simple no es ninguna respuesta en absoluto. El bot no es necesario para responder cuando el usuario haya terminado con el módulo de tareas. |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teams mostrará el valor de un cuadro de `value` mensaje emergente. |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | Le permite "encadenar" secuencias de tarjetas adaptables juntas en una experiencia wizard/multi-step. _Tenga en cuenta que encadenar tarjetas adaptables en una secuencia es un escenario avanzado y no se documenta aquí. Sin embargo, la aplicación de ejemplo Node.js la admite y cómo funciona se documenta en [su archivo README.md.](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)_ |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>Carga útil de mensajes task/fetch y task/submit

En esta sección se define el esquema de lo que recibe el bot cuando recibe un `task/fetch` objeto o `task/submit` Bot `Activity` Framework. El nivel superior importante aparece a continuación:

| Propiedad | Descripción                          |
| -------- | ------------------------------------ |
| `type`   | Siempre será `invoke`              |
| `name`   | O bien `task/fetch` o `task/submit` |
| `value`  | La carga definida por el desarrollador. Normalmente, la estructura del `value` objeto refleja lo que se envió desde Teams. En este caso, sin embargo, es diferente porque queremos admitir la captura dinámica ( `task/fetch` ) tanto desde Bot Framework ( ) como desde acciones de tarjeta adaptable `value` `Action.Submit` `data` (), y necesitamos una forma de comunicar Teams al bot `context` además `value` / `data` de lo que se incluyó en .<br/><br/>Hacemos esto combinando los dos en un objeto primario:<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a>Ejemplo: Recepción y respuesta a mensajes de invocación de tareas/captura y tareas/envíos- Node.js

> [!NOTE]
> El código de ejemplo siguiente se modificó entre Technical Preview y la versión final de esta característica: el esquema de la `task/fetch` solicitud cambió para seguir lo que se [documentó en la sección anterior.](#payload-of-taskfetch-and-tasksubmit-messages) Es decir, la documentación era correcta, pero la implementación no lo era. Consulte los `// for Technical Preview [...]` comentarios a continuación para ver qué cambió.

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

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a>Ejemplo: Recepción y respuesta a mensajes de invocación task/fetch y task/submit - C #

En los bots de C#, `invoke` los mensajes son procesados por un controlador `HttpResponseMessage()` que procesa un `Activity` mensaje. Las `task/fetch` `task/submit` solicitudes y respuestas son JSON. En C#, no es tan conveniente tratar con JSON sin procesar como en Node.js, por lo que necesita clases contenedoras para controlar la serialización hacia y desde JSON. Todavía no hay compatibilidad directa con esto en el SDK de [Microsoft Teams C#,](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) pero puede ver un ejemplo de cómo serían estas clases contenedoras simples en la [aplicación de ejemplo de C#.](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs)

A continuación se muestra el código de ejemplo en C# para el control `task/fetch` y los mensajes que utilizan estas clases `task/submit` contenedoras ( , ), extraído `TaskInfo` del `TaskEnvelope` [ejemplo:](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)

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

En el ejemplo anterior no se muestra la `SetTaskInfo()` función, que establece el `height` objeto y las propiedades del objeto para cada `width` `title` `TaskInfo` caso. Aquí está el [código fuente de SetTaskInfo()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Acciones de la tarjeta Bot Framework frente a acciones de action.submit de tarjeta adaptable

El esquema de las acciones de la tarjeta bot framework es ligeramente diferente de las acciones de la tarjeta `Action.Submit` adaptable. Como resultado, la forma de invocar módulos de tareas también es ligeramente diferente: el `data` objeto contiene un objeto para que no `Action.Submit` `msteams` interfiera con otras propiedades de la tarjeta. En la tabla siguiente se muestra un ejemplo de cada uno:

| Acción de la tarjeta Bot Framework                              | Acción de tarjeta adaptable.Enviar acción                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="see-also"></a>Vea también

* [Microsoft Teams código de ejemplo del módulo de tareas — nodejs](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [Muestras de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).
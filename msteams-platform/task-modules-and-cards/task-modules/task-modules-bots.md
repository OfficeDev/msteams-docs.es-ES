---
title: Uso de módulos de tareas en bots de Microsoft Teams
description: Cómo usar módulos de tareas con bots de Microsoft Teams, incluidas tarjetas bot Framework, tarjetas adaptables y vínculos profundos
localization_priority: Normal
ms.topic: how-to
keywords: bots de equipos de módulos de tareas
ms.openlocfilehash: 948af0c71acb20f4d84fa25ba79618045dad9da7
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020278"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a>Uso de módulos de tareas de bots de Microsoft Teams

Los módulos de tareas se pueden invocar desde bots de Microsoft Teams con botones en tarjetas adaptables y tarjetas de Bot Framework (Hero, Thumbnail y Office 365 Connector). Los módulos de tareas suelen ser una mejor experiencia de usuario que varios pasos de conversación en los que, como desarrollador, debe realizar un seguimiento del estado del bot y permitir que el usuario interrumpa o cancele la secuencia.

Hay dos formas de invocar módulos de tareas:

* **Un nuevo tipo de mensaje de invocación `task/fetch` .** El uso de la acción de tarjeta para las tarjetas de Bot Framework o la acción de tarjeta para tarjetas adaptables, con , el módulo de tareas (ya sea una dirección URL o una tarjeta adaptable) se captura dinámicamente `invoke` [](~/task-modules-and-cards/cards/cards-actions.md#invoke) desde `Action.Submit` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) `task/fetch` el bot.
* **Direcciones URL de vínculos profundos.** Con la [sintaxis de vínculo profundo](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)para módulos de tareas, puede usar la acción de tarjeta para tarjetas bot Framework o la acción de tarjeta para `openUrl` [](~/task-modules-and-cards/cards/cards-actions.md#openurl) `Action.OpenUrl` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) tarjetas adaptables, respectivamente. Con las direcciones URL de vínculo profundo, la dirección URL del módulo de tareas o el cuerpo de la tarjeta adaptable se conocen de antemano, lo que evita un recorrido de ida y vuelta del servidor con relación a `task/fetch` .

>[!IMPORTANT]
>Para garantizar comunicaciones seguras, cada uno `url` y debe implementar el protocolo de cifrado `fallbackUrl` HTTPS.

## <a name="invoking-a-task-module-via-taskfetch"></a>Invocar un módulo de tareas mediante task/fetch

Cuando el objeto de la acción de tarjeta o se inicializa de la forma correcta (se explica con más detalle a continuación), cuando un usuario presiona el botón se envía un mensaje `value` `invoke` al `Action.Submit` `invoke` bot. En la respuesta HTTP al mensaje, hay un objeto TaskInfo incrustado en un objeto contenedor, que Teams usa `invoke` para mostrar el módulo de tareas. [](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)

![solicitud/respuesta task/fetch](~/assets/images/task-module/task-module-invoke-request-response.png)

Veamos cada paso con un poco más de detalle:

1. En este ejemplo se muestra una tarjeta de Bot Framework Hero con una acción de tarjeta `invoke` ["Comprar".](~/task-modules-and-cards/cards/cards-actions.md#invoke) El valor de la `type` propiedad `task/fetch` es: el resto del `value` objeto puede ser lo que quieras.
2. El bot recibe el `invoke` mensaje HTTP POST.
3. El bot crea un objeto de respuesta y lo devuelve en el cuerpo de la respuesta POST con un código de respuesta HTTP 200. El esquema de respuestas se describe a continuación en la discusión sobre [tarea/envío,](#the-flexibility-of-tasksubmit)pero lo importante que debe recordarse ahora es que el cuerpo de la respuesta HTTP contiene un objeto [TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) incrustado en un objeto contenedor, por ejemplo:

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

    El `task/fetch` evento y su respuesta para bots es similar, conceptualmente, a la función del SDK de `microsoftTeams.tasks.startTask()` cliente.
4. Microsoft Teams muestra el módulo de tareas.

## <a name="submitting-the-result-of-a-task-module"></a>Enviar el resultado de un módulo de tareas

Cuando el usuario ha terminado con el módulo de tareas, enviar el resultado al bot es similar a la forma en que funciona con las pestañas, pero hay algunas [diferencias,](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)por lo que también se describe aquí.

* **HTML/JavaScript ( `TaskInfo.url` )**. Una vez validado lo que el usuario ha escrito, se llama a la función SDK (a la que se hace referencia a continuación con fines `microsoftTeams.tasks.submitTask()` `submitTask()` de legibilidad). Puedes llamar sin ningún parámetro si solo quieres que Teams cierre el módulo de tareas, pero la mayoría de las veces querrás pasar un objeto o una cadena `submitTask()` a tu `submitHandler` . Simplemente pásalo como primer parámetro, `result` . Teams invocará `submitHandler` : será y será el objeto o cadena que pasó a `err` `null` `result` `submitTask()` . Si llama con un parámetro, debe pasar una o una matriz de cadenas: esto permite a Teams validar que la aplicación que envía el resultado es la misma que invocó el módulo `submitTask()` `result` de  `appId` `appId` tareas. El bot recibirá un mensaje `task/submit` incluido como se describe a `result` [continuación](#payload-of-taskfetch-and-tasksubmit-messages).
* **Tarjeta adaptable ( `TaskInfo.card` )**. El cuerpo de la tarjeta adaptable (como lo ha rellenado el usuario) se enviará al bot a través de un mensaje cuando el usuario `task/submit` presione cualquier `Action.Submit` botón.

## <a name="the-flexibility-of-tasksubmit"></a>Flexibilidad de tarea/envío

En la sección anterior, aprendió que cuando el usuario termina con un módulo de tareas invocado desde un bot, el bot siempre recibe un `task/submit invoke` mensaje. Como desarrollador, tiene varias opciones al *responder* al `task/submit` mensaje:

| Respuesta del cuerpo HTTP                      | Escenario                                |
| --------------------------------------- | --------------------------------------- |
| Ninguno (omitir el `task/submit` mensaje) | La respuesta más sencilla no es ninguna respuesta. No es necesario que el bot responda cuando el usuario haya terminado con el módulo de tareas. |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teams mostrará el valor de `value` en un cuadro de mensaje emergente. |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | Permite "encadenar" secuencias de tarjetas adaptables juntas en una experiencia de asistente y varios pasos. _Tenga en cuenta que encadenar tarjetas adaptables en una secuencia es un escenario avanzado y no se documenta aquí. La Node.js de ejemplo es compatible con ella, sin embargo, y su funcionamiento se documenta en [su README.md archivo](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._ |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>Carga de los mensajes task/fetch y task/submit

En esta sección se define el esquema de lo que el bot recibe cuando recibe un `task/fetch` objeto `task/submit` o Bot `Activity` Framework. A continuación se muestra el nivel superior importante:

| Propiedad | Descripción                          |
| -------- | ------------------------------------ |
| `type`   | Siempre será `invoke`              |
| `name`   | Cualquiera `task/fetch` o `task/submit` |
| `value`  | La carga definida por el desarrollador. Normalmente, la estructura del `value` objeto refleja lo que se envió desde Teams. En este caso, sin embargo, es diferente porque queremos admitir la captura dinámica ( ) de bot Framework ( ) y las acciones de tarjeta adaptable ( ), y necesitamos una forma de comunicar Teams al bot además de lo que se incluyó `task/fetch` `value` en `Action.Submit` `data` `context` `value` / `data` .<br/><br/>Para ello, combinamos los dos en un objeto primario:<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a>Ejemplo: recibir y responder a los mensajes de invocación task/fetch y task/submit : Node.js

> [!NOTE]
> El código de ejemplo siguiente se modificó entre technical preview y la versión final de esta característica: el esquema de la solicitud cambió para seguir lo que se `task/fetch` [documentó en la sección anterior](#payload-of-taskfetch-and-tasksubmit-messages). Es decir, la documentación era correcta, pero la implementación no era correcta. Vea los `// for Technical Preview [...]` comentarios siguientes para ver lo que ha cambiado.

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

*Vea también ,* Código de ejemplo del módulo de tareas [de Microsoft Teams: nodejs](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts) y  [ejemplos de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a>Ejemplo: recibir y responder a los mensajes de invocación task/fetch y task/submit - C #

En C# bots, los mensajes los procesa un `invoke` controlador que procesa un `HttpResponseMessage()` `Activity` mensaje. Las `task/fetch` solicitudes y las `task/submit` respuestas son JSON. En C#, no es tan conveniente tratar con JSON sin formato como en Node.js, por lo que necesitas clases contenedoras para controlar la serialización desde y hacia JSON. Todavía no hay compatibilidad directa con esto en el SDK de Microsoft Teams [C#,](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) pero puedes ver un ejemplo de cómo serían estas clases contenedoras sencillas en la aplicación de ejemplo [C#.](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs)

A continuación se muestra un código de C# para controlar y los mensajes que usan estas clases contenedoras ( , ), que se `task/fetch` `task/submit` `TaskInfo` `TaskEnvelope` excerdió del [ejemplo](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):

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

No se muestra en el ejemplo anterior la función, que `SetTaskInfo()` establece las propiedades , y del objeto para cada `height` `width` `title` `TaskInfo` caso. Este es el código [fuente de SetTaskInfo().](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Acciones de tarjeta de Bot Framework frente a acciones Action.Submit de tarjeta adaptable

El esquema de las acciones de tarjeta de Bot Framework es ligeramente diferente de las acciones de tarjeta `Action.Submit` adaptable. Como resultado, la forma de invocar módulos de tareas también es ligeramente diferente: el objeto en contiene un objeto para que no interfiera con otras propiedades `data` `Action.Submit` de la `msteams` tarjeta. En la tabla siguiente se muestra un ejemplo de cada una:

| Acción de tarjeta de Bot Framework                              | Acción Action.Submit de tarjeta adaptable                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

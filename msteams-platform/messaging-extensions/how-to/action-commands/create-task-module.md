---
title: Crear y enviar el módulo de tareas
author: clearab
description: Cómo controlar la acción de invocación inicial y responder con un módulo de tarea desde un comando de extensión de mensajería de acciones
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 58fb7e1ff5690b33c2e23f68529f05869afa9016
ms.sourcegitcommit: ce74f821660b1258c72b3c3f71c1cf177e7e92ef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2021
ms.locfileid: "50072878"
---
# <a name="create-and-send-the-task-module"></a>Crear y enviar el módulo de tareas

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Si no va a rellenar el módulo de tareas con parámetros definidos en el manifiesto de la aplicación, debe crear el módulo de tareas para los usuarios. Usa una tarjeta adaptable o una vista web incrustada.

## <a name="the-initial-invoke-request"></a>La solicitud de invocación inicial

Con este método, el servicio recibirá un objeto de tipo y debe responder con un objeto que contenga la tarjeta adaptable o una dirección URL a la `Activity` `composeExtension/fetchTask` vista web `task` incrustada. Junto con las propiedades de actividad de bot estándar, la carga inicial de invocación contiene los siguientes metadatos de solicitud:

|Nombre de propiedad|Finalidad|
|---|---|
|`type`| Tipo de solicitud. Debe ser `invoke` . |
|`name`| Tipo de comando que se emite al servicio. Debe ser `composeExtension/fetchTask` . |
|`from.id`| Identificador del usuario que envió la solicitud. |
|`from.name`| Nombre del usuario que envió la solicitud. |
|`from.aadObjectId`| Identificador de objeto de Azure Active Directory del usuario que envió la solicitud. |
|`channelData.tenant.id`| Identificador del inquilino de Azure Active Directory |
|`channelData.channel.id`| Id. de canal (si la solicitud se realizó en un canal). |
|`channelData.team.id`| Identificador de equipo (si la solicitud se realizó en un canal). |
|`value.commandId` | Contiene el identificador del comando que se invocó. |
|`value.commandContext` | Contexto que desencadenó el evento. Debe ser `compose` . |
|`value.context.theme` | El tema de cliente del usuario, útil para el formato de vista web incrustada. Debe ser `default` o `contrast` `dark` . |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-11-chat-are-listed-in-the-following-section"></a>Las propiedades de actividad de carga cuando se invoca un módulo de tarea desde el chat 1:1 se enumeran en la siguiente sección:

|Nombre de propiedad|Finalidad|
|---|---|
|`type`| Tipo de solicitud. Debe ser `invoke` . |
|`name`| Tipo de comando que se emite al servicio. Debe ser `composeExtension/fetchTask` . |
|`from.id`| Identificador del usuario que envió la solicitud. |
|`from.name`| Nombre del usuario que envió la solicitud. |
|`from.aadObjectId`| Identificador de objeto de Azure Active Directory del usuario que envió la solicitud. |
|`channelData.tenant.id`| Identificador del inquilino de Azure Active Directory |
|`channelData.source.name`| Nombre de origen desde el que se invoca el módulo de tareas. |
|`ChannelData.legacy. replyToId`| Obtiene o establece el identificador del mensaje al que este mensaje es una respuesta. |
|`value.commandId` | Contiene el identificador del comando que se invocó. |
|`value.commandContext` | Contexto que desencadenó el evento. Debe ser `compose` . |
|`value.context.theme` | El tema de cliente del usuario, útil para el formato de vista web incrustada. Debe ser `default` o `contrast` `dark` . |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-group-chat-are-listed-in-the-following-section"></a>Las propiedades de actividad de carga cuando se invoca un módulo de tarea desde un chat de grupo se enumeran en la siguiente sección:

|Nombre de propiedad|Finalidad|
|---|---|
|`type`| Tipo de solicitud. Debe ser `invoke` . |
|`name`| Tipo de comando que se emite al servicio. Debe ser `composeExtension/fetchTask` . |
|`from.id`| Identificador del usuario que envió la solicitud. |
|`from.name`| Nombre del usuario que envió la solicitud. |
|`from.aadObjectId`| Identificador de objeto de Azure Active Directory del usuario que envió la solicitud. |
|`channelData.tenant.id`| Identificador del inquilino de Azure Active Directory |
|`channelData.source.name`| Nombre de origen desde el que se invoca el módulo de tareas. |
|`ChannelData.legacy. replyToId`| Obtiene o establece el identificador del mensaje al que este mensaje es una respuesta. |
|`value.commandId` | Contiene el identificador del comando que se invocó. |
|`value.commandContext` | Contexto que desencadenó el evento. Debe ser `compose` . |
|`value.context.theme` | El tema de cliente del usuario, útil para el formato de vista web incrustada. Debe ser `default` o `contrast` `dark` . |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-channel-new-post-are-listed-in-the-following-section"></a>Las propiedades de actividad de carga cuando se invoca un módulo de tarea desde un canal (nueva publicación) se enumeran en la siguiente sección:

|Nombre de propiedad|Finalidad|
|---|---|
|`type`| Tipo de solicitud. Debe ser `invoke` . |
|`name`| Tipo de comando que se emite al servicio. Debe ser `composeExtension/fetchTask` . |
|`from.id`| Identificador del usuario que envió la solicitud. |
|`from.name`| Nombre del usuario que envió la solicitud. |
|`from.aadObjectId`| Identificador de objeto de Azure Active Directory del usuario que envió la solicitud. |
|`channelData.tenant.id`| Identificador del inquilino de Azure Active Directory |
|`channelData.channel.id`| Id. de canal (si la solicitud se realizó en un canal). |
|`channelData.team.id`| Identificador de equipo (si la solicitud se realizó en un canal). |
|`channelData.source.name`| Nombre de origen desde el que se invoca el módulo de tareas. |
|`ChannelData.legacy. replyToId`| Obtiene o establece el identificador del mensaje al que este mensaje es una respuesta. |
|`value.commandId` | Contiene el identificador del comando que se invocó. |
|`value.commandContext` | Contexto que desencadenó el evento. Debe ser `compose` . |
|`value.context.theme` | El tema de cliente del usuario, útil para el formato de vista web incrustada. Debe ser `default` o `contrast` `dark` . |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-channel-reply-to-thread-are-listed-in-the-following-section"></a>Las propiedades de actividad de carga cuando se invoca un módulo de tarea desde un canal (responder a subproceso) se enumeran en la siguiente sección:

|Nombre de propiedad|Finalidad|
|---|---|
|`type`| Tipo de solicitud. Debe ser `invoke` . |
|`name`| Tipo de comando que se emite al servicio. Debe ser `composeExtension/fetchTask` . |
|`from.id`| Identificador del usuario que envió la solicitud. |
|`from.name`| Nombre del usuario que envió la solicitud. |
|`from.aadObjectId`| Identificador de objeto de Azure Active Directory del usuario que envió la solicitud. |
|`channelData.tenant.id`| Identificador del inquilino de Azure Active Directory |
|`channelData.channel.id`| Id. de canal (si la solicitud se realizó en un canal). |
|`channelData.team.id`| Identificador de equipo (si la solicitud se realizó en un canal). |
|`channelData.source.name`| Nombre de origen desde el que se invoca el módulo de tareas. |
|`ChannelData.legacy. replyToId`| Obtiene o establece el identificador del mensaje al que este mensaje es una respuesta. |
|`value.commandId` | Contiene el identificador del comando que se invocó. |
|`value.commandContext` | Contexto que desencadenó el evento. Debe ser `compose` . |
|`value.context.theme` | El tema de cliente del usuario, útil para el formato de vista web incrustada. Debe ser `default` o `contrast` `dark` . |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-command-box-are-listed-in-the-following-section"></a>Las propiedades de actividad de carga cuando se invoca un módulo de tarea desde un cuadro de comando se enumeran en la siguiente sección:

|Nombre de propiedad|Finalidad|
|---|---|
|`type`| Tipo de solicitud. Debe ser `invoke` . |
|`name`| Tipo de comando que se emite al servicio. Debe ser `composeExtension/fetchTask` . |
|`from.id`| Identificador del usuario que envió la solicitud. |
|`from.name`| Nombre del usuario que envió la solicitud. |
|`from.aadObjectId`| Identificador de objeto de Azure Active Directory del usuario que envió la solicitud. |
|`channelData.tenant.id`| Identificador del inquilino de Azure Active Directory |
|`channelData.source.name`| Nombre de origen desde el que se invoca el módulo de tareas. |
|`value.commandId` | Contiene el identificador del comando que se invocó. |
|`value.commandContext` | Contexto que desencadenó el evento. Debe ser `compose` . |
|`value.context.theme` | El tema de cliente del usuario, útil para el formato de vista web incrustada. Debe ser `default` o `contrast` `dark` . |

### <a name="example-fetchtask-request"></a>Ejemplo de solicitud fetchTask

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "name": "composeExtension/fetchTask",
  "type": "invoke",
  "timestamp": "2019-07-01T22:57:22.175Z",
  "localTimestamp": "2019-07-01T15:57:22.175-07:00",
  "id": "f:0123456878990178955",
  "channelId": "msteams",
  "serviceURL": "https://smba.trafficmanager.net/amer/",
  "from": {
    "id": "29:1test2GgHIa0DXzDT_OGwL5vSMZdAxDlGR7hYxZ6_JBVqHz2Zq9Nm44FUNWqHCdGBwHg8WrlFRsYrd0cCAS7dig",
    "name": "John Smith",
    "aadObjectId": "1234567d-1234-462a-8952-35b75f16f1e1"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "tenantId": "1234abcd-1234-12ab-12ab-35b75f16f1e1",
    "id": "19:83ed1d507cb5427c93495cf914326310@thread.skype"
  },
  "recipient": {
    "id": "28:049566e0-4401-4bcf-86a1-ce22082ce03a",
    "name": "mess"
  },
  "entities": [
    {
      "locale": "en-US",
      "country": "US",
      "platform": "Windows",
      "type": "clientInfo"
    }
  ],
  "channelData": {
    "channel": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "team": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "tenant": {
      "id": "1234abcd-1234-12ab-12ab-35b75f16f1e1"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "hello",
    "commandContext": "compose",
    "context": {
      "theme": "dark"
    }
  },
  "locale": "en-US"
}
```

* * *

## <a name="initial-invoke-request-from-a-message"></a>Solicitud de invocación inicial de un mensaje

Cuando se invoca el bot desde un mensaje en lugar del área de redacción o la barra de comandos, el objeto de la solicitud inicial debe contener los detalles del mensaje desde el que se invoca la extensión `value` de mensajería. Vea la sección siguiente para ver el ejemplo de este objeto. Las matrices y son opcionales y no están presentes si no hay ninguna reacción o `reactions` `mentions` mención en el mensaje original.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
...
  "value": {
    "commandId": "setReminder",
    "commandContext": "message",
    "messagePayload": {
      "id": "1111111111",
      "replyToId": null,
      "createdDateTime": "2019-02-25T21:29:36.065Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "subject": "Message subject",
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "This is the message the messaging extension was invoked from."
    },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "wxyz12ab8-ab12-cd34-ef56-098abc123876",
          "displayName": "Jamie Smythe"
        },
        "application": null
      },
      "reactions": [
        {
          "reactionType": "like",
          "createdDateTime": "2019-02-25T22:40:40.806Z",
          "user": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "qrst12346-ab12-cd34-ef56-098abc123876",
              "displayName": "Jim Brown"
            },
            "application": null
          }
        }
      ],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Sarah",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "ab12345678-ab12-cd34-ef56-098abc123876",
              "displayName": "Sarah"
            },
            "application": null
          }
        }
      ]
    }
  ...
```

* * *

## <a name="respond-to-the-fetchtask"></a>Responder a fetchTask

Responda a la solicitud de invocación con un objeto que contenga un objeto con la tarjeta adaptable o la dirección URL web, o `task` un mensaje de cadena `taskInfo` simple.

|Nombre de propiedad|Finalidad|
|---|---|
|`type`| Puede ser `continue` para presentar un formulario o para un elemento emergente `message` simple. |
|`value`| Un objeto `taskInfo` de un formulario o un `string` mensaje. |

El esquema del objeto taskInfo es:

|Nombre de propiedad|Finalidad|
|---|---|
|`title`| Título del módulo de tareas.|
|`height`| Debe ser un entero (en píxeles) o `small` `medium` , `large` .|
|`width`| Debe ser un entero (en píxeles) o `small` `medium` , `large` .|
|`card`| La tarjeta adaptable que define el formulario (si se usa uno).
|`url`| Dirección URL que se abrirá dentro del módulo de tareas como una vista web incrustada.|
|`fallbackUrl`| Si un cliente no admite la característica del módulo de tareas, esta dirección URL se abre en una pestaña del explorador. |

### <a name="with-an-adaptive-card"></a>Con una tarjeta adaptable

Al usar una tarjeta adaptable, debes responder con un `task` objeto con el objeto que contiene una tarjeta `value` adaptable.

#### <a name="example-fetchtask-response-with-an-adaptive-card"></a>Ejemplo de respuesta fetchTask con una tarjeta adaptable

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

En este ejemplo se usa [el paquete NuGet AdaptiveCards](https://www.nuget.org/packages/AdaptiveCards) además del SDK de Bot Framework.

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Card = new Attachment()
        {
          ContentType = AdaptiveCard.ContentType,
          Content = new AdaptiveCard("1.0")
          {
            Body = new List<AdaptiveElement>()
            {
              new AdaptiveTextInput() { Id = "FormField1", Placeholder = placeholder},
              new AdaptiveTextInput() { Id = "FormField2", Placeholder = "FormField2"},
              new AdaptiveTextInput() { Id = "FormField3", Placeholder = "FormField3"},
            },
            Actions = new List<AdaptiveAction>()
            {
              new AdaptiveSubmitAction()
              {
                Type = AdaptiveSubmitAction.TypeName,
                Title = "Submit",
              },
            },
          },
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    handleTeamsMessagingExtensionFetchTask(context, action) {
      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [{
          data: { submitLocation: 'messagingExtensionFetchTask'},
          title: 'Submit',
          type: 'Action.Submit'
        }],
        body: [
          { text: 'Task Module', type: 'TextBlock', weight: 'bolder'},
          { type: 'TextBlock', text: 'Enter text for Question:' },
          { id: 'Question', placeholder: 'Question text here', type: 'Input.Text', value: userText },
          { type: 'TextBlock', text: 'Options for Question:' },
          { type: 'TextBlock', text: 'Is Multi-Select:' },
          {
            choices: [{ title: 'True', value: 'true' }, { title: 'False', value: 'false' }],
            id: 'MultiSelect',
            isMultiSelect: false,
            style: 'expanded',
            type: 'Input.ChoiceSet',
            value: isMultiSelect ? 'true' : 'false'
          },
          { id: 'Option1', placeholder: 'Option 1 here', type: 'Input.Text', value: option1 },
          { id: 'Option2', placeholder: 'Option 2 here', type: 'Input.Text', value: option2 }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });

      return {
        task: {
          type: 'continue',
          value: {
            card: adaptiveCard,
            height: 450,
            title: 'Task Module Fetch Example',
            url: null,
            width: 500
          }
        }
      };
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
 {
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "card": {
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Input.Text",
            "placeholder": "FormField1",
            "id": "FormField1"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField2",
            "id": "FormField2"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField3",
            "id": "FormField3"
          },
          {
            "type": "ActionSet",
            "actions": [
              {
                "type": "Action.Submit",
                "title": "Action.Submit",
                "id": "submitAction"
              }
            ]
          }
        ]
      }
    }
  }
}
```

* * *

### <a name="with-an-embedded-web-view"></a>Con una vista web incrustada

Al usar una vista web incrustada, debe responder con un objeto con el objeto que contiene la dirección URL del formulario web que `task` `value` desea cargar. Los dominios de cualquier dirección URL que quiera cargar deben incluirse en la `validDomains` matriz en el manifiesto de la aplicación. Consulte la documentación [del módulo de tareas](~/task-modules-and-cards/what-are-task-modules.md) para obtener información completa sobre cómo crear la vista web incrustada.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Url = "https://contoso.com/msteams/taskmodules/newcustomer",
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    return {
      task: {
        type: 'continue',
        value: {
          width: 500,
          height: 450,
          title: 'Task Module Fetch Example',
          url: 'https://contoso.com/msteams/taskmodules/newcustomer',
          fallbackUrl: 'https://contoso.com/msteams/taskmodules/newcustomer'
        }
      }
    };
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

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

* * *

### <a name="request-to-install-your-conversational-bot"></a>Solicitud para instalar el bot de conversación

Si la aplicación contiene un bot de conversación, instale el bot en la conversación antes de cargar el módulo de tareas. Es útil obtener contexto adicional para el módulo de tareas. Un ejemplo típico de este escenario es capturar la lista para rellenar un control de selector de personas o la lista de canales de un equipo.

Cuando la extensión de mensajería reciba la invocación, compruebe si el bot está instalado `composeExtension/fetchTask` en el contexto actual para facilitar el flujo. Por ejemplo, compruebe el flujo con una llamada de lista de obtener. Si el bot no está instalado, devuelve una tarjeta adaptable con una acción que solicita al usuario que instale el bot. Vea la acción en el ejemplo siguiente. El usuario debe tener permiso para instalar las aplicaciones en esa ubicación para su comprobación. Si la instalación de la aplicación no se realiza correctamente, el usuario recibe un mensaje para ponerse en contacto con el administrador.

#### <a name="example-of-the-response"></a>Ejemplo de la respuesta:

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Looks like you haven't used Disco in this team/chat"
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Continue",
      "data": {
        "msteams": {
          "justInTimeInstall": true
        }
      }
    }
  ],
  "version": "1.0"
}
```

Después de la instalación, el bot recibe otro mensaje de invocación con `name = composeExtension/submitAction` y `value.data.msteams.justInTimeInstall = true` .

#### <a name="example-of-the-invoke"></a>Ejemplo de la invocación:

```json
{
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "msteams": {
        "justInTimeInstall": true
      }
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  },
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith"
}
```

La respuesta de tarea a la invocación debe ser similar a la del bot instalado.

#### <a name="example-of-just-in-time-installation-of-app-with-adaptive-card"></a>Ejemplo de instalación just-in-time de la aplicación con tarjeta adaptable: 

```csharp
private static Attachment GetAdaptiveCardAttachmentFromFile(string fileName)
  {
      //Read the card json and create attachment.
         string[] paths = { ".", "Resources", fileName };
         var adaptiveCardJson = File.ReadAllText(Path.Combine(paths));
         var adaptiveCardAttachment = new Attachment()
            {
                ContentType = "application/vnd.microsoft.card.adaptive",
                Content = JsonConvert.DeserializeObject(adaptiveCardJson),
            };
            return adaptiveCardAttachment;
        }
```

* * *

## <a name="next-steps"></a>Pasos siguientes

Si permite que los usuarios envíen una respuesta desde el módulo de tareas, debe controlar la acción de envío.

* [Crear y responder con un módulo de tareas](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]

---
title: Iniciar acciones con extensiones de mensajería
description: Crear extensiones de mensajería basadas en acciones para permitir que los usuarios desencadenen servicios externos
keywords: búsqueda de extensiones de mensajería de Team Extensions
ms.openlocfilehash: 9b7d3bd53ba45d55e80f858a3c89be265c13482b
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676000"
---
# <a name="initiate-actions-with-messaging-extensions"></a>Iniciar acciones con extensiones de mensajería

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Las extensiones de mensajería basadas en acciones permiten a los usuarios desencadenar acciones en servicios externos mientras se encuentran dentro de Microsoft Teams.

![Ejemplo de tarjeta de extensión de mensajería](~/assets/images/compose-extensions/ceexample.png)

En las secciones siguientes se describe cómo hacerlo.

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a>Tipo de acción extensiones de mensajes

Para iniciar acciones desde una extensión de mensajería, `type` establezca el `action`parámetro en. A continuación se muestra un ejemplo de un manifiesto con una búsqueda y un comando crear. Una sola extensión de mensajería puede tener hasta 10 comandos diferentes. Esto puede incluir varios comandos de búsqueda y varios basados en acciones.

#### <a name="complete-app-manifest-example"></a>Ejemplo de manifiesto de aplicación completo

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.Todo",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://todobotservice.azurewebsites.net/",
    "privacyUrl": "http://todobotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://todobotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "To Do",
    "full": "To Do"
  },
  "description": {
    "short": "Find or create a new task in To Do",
    "full": "Find or create a new task in To Do"
  },
  "icons": {
    "outline": "todo-outline.jpg",
    "color": "todo-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "searchCmd",
          "description": "Search you Todo's",
          "title": "Search",
          "initialRun": true,
          "context": ["commandBox", "compose"],
          "parameters": [
            {
              "name": "searchKeyword",
              "description": "Enter your search keywords",
              "title": "Keywords"
            }
          ]
        },
        {
          "id": "addTodo",
          "description": "Create a To Do item",
          "title": "Create To Do",
          "type": "action",
          "context": ["commandBox", "message", "compose"],
          "parameters": [
            {
              "name": "Name",
              "description": "To Do Title",
              "title": "Title",
              "inputType": "text"
            },
            {
              "name": "Description",
              "description": "Description of the task",
              "title": "Description",
              "inputType": "textarea"
            },
            {
              "name": "Date",
              "description": "Due date for the task",
              "title": "Date",
              "inputType": "date"
            }
          ]
        },
        {
          "id": "reassignTodo",
          "description": "Reassign a todo item",
          "title": "Reassign a todo item",
          "type": "action",
          "fetchTask": true,
          "parameters": [
            {
              "name": "Name",
              "title": "Title"
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "todobotservice.azurewebsites.net",
    "*.todobotservice.azurewebsites.net"
  ]
}
```

### <a name="initiate-actions-from-messages"></a>Iniciar acciones desde mensajes

Además de iniciar acciones desde el área de mensaje de redacción, también puede usar la extensión de mensajería para iniciar una acción desde un mensaje. Esto le permitirá enviar el contenido del mensaje a su bot para su procesamiento y, opcionalmente, responder a ese mensaje con una respuesta mediante el método que se describe en [responder a envío](#responding-to-submit). La respuesta se insertará como respuesta al mensaje que los usuarios pueden editar antes de enviarlo. Los usuarios pueden acceder a la extensión de mensajería desde `...` el menú de desbordamiento `Take action` y, a continuación, seleccionar como en la imagen siguiente.

![Ejemplo de inicio de una acción desde un mensaje](~/assets/images/compose-extensions/messageextensions_messageaction.png)

Para habilitar la extensión de mensajería para que funcione desde un mensaje, deberá agregar el `context` parámetro al `commands` objeto de la extensión de mensajería en el manifiesto de la aplicación, como se muestra en el ejemplo siguiente. Las cadenas válidas `context` para la `"message"`matriz `"commandBox"`son, `"compose"`y. El valor predeterminado es `["compose", "commandBox"]`. Consulte la sección [definir comandos](#define-commands) para obtener detalles completos del `context` parámetro.

```json
"composeExtensions": [
  {
    "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "reassignTodo",
        "description": "Reassign a todo item",
        "title": "Create To Do",
        "type": "Action",
        "context": ["message"],
        "fetchTask": true
    }]
    ...

```

A continuación se muestra un ejemplo `value` del objeto que contiene los detalles del mensaje que se enviará como `composeExtension` parte de la solicitud que se enviará a su bot.

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
        "content": "this is the message"
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

### <a name="test-via-uploading"></a>Prueba mediante carga

Puede probar la extensión de mensajería cargando la aplicación. Consulte [cargar la aplicación en un equipo](~/concepts/deploy-and-publish/apps-upload.md) para obtener más información.

Para abrir la extensión de mensajería, navegue a cualquiera de sus chats o canales. Elija el botón **más opciones** (**&#8943;**) en el cuadro de redacción y elija su extensión de mensajería.

## <a name="collecting-input-from-users"></a>Recopilar la entrada de los usuarios

Hay tres formas de recopilar información de un usuario final en Microsoft Teams.

### <a name="static-parameter-list"></a>Lista de parámetros estáticos

En este método, todo lo que debe hacer es definir una lista estática de parámetros en el manifiesto, tal como se muestra más arriba en el comando "crear tarea". Para usar este método, `fetchTask` Asegúrese de que `false` se establece en y de que define los parámetros en el manifiesto.

Cuando un usuario elige un comando con parámetros estáticos, Microsoft Teams generará un formulario en un módulo de tareas con los parámetros definidos en el manifiesto. Al presionar enviar, `composeExtension/submitAction` se envía al bot. Consulte el tema [respuesta a envío](#responding-to-submit) para obtener más información sobre el conjunto de respuestas esperado.

### <a name="dynamic-input-using-an-adaptive-card"></a>Entrada dinámica con una tarjeta adaptable

En este método, el servicio puede definir una tarjeta adaptable personalizada para recopilar la entrada del usuario final. Para este enfoque, establezca el `fetchTask` parámetro `true` en en el manifiesto. Tenga en cuenta que si `fetchTask` establece `true` en cualquier parámetro estático definido para el comando, se omitirá.

En este método, el servicio recibirá `composeExtension/fetchTask` un evento y debe responder con una [respuesta del módulo de tareas](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)de tarjeta adaptable. A continuación se muestra una respuesta de ejemplo con una tarjeta adaptable:

```json
{
    "task": {
        "type": "continue",
        "value": {
            "card": {
                "contentType": "application/vnd.microsoft.card.adaptive",
                "content": {
                    "body": [
                        {
                            "type": "TextBlock",
                            "text": "Please enter the following information:"
                        },
                        {
                            "type": "TextBlock",
                            "text": "Name"
                        },
                        {
                            "type": "Input.Text",
                            "spacing": "None",
                            "title": "New Input.Toggle",
                            "placeholder": "Placeholder text"
                        },
                        {
                            "type": "TextBlock",
                            "text": "Date of birth"
                        },
                        {
                            "type": "Input.Date",
                            "spacing": "None",
                            "title": "New Input.Toggle"
                        }
                    ],
                    "type": "AdaptiveCard",
                    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
                    "version": "1.0"
                }
            }
        }
    }
}
```

El bot también puede responder con una respuesta de auth/config si el usuario necesita autenticar o configurar la extensión antes de obtener la entrada del usuario.

### <a name="dynamic-input-using-a-web-view"></a>Entrada dinámica con una vista Web

En este método, el servicio puede mostrar `<iframe>` un widget basado en para mostrar una interfaz de usuario personalizada y recopilar entradas de usuario. Para este enfoque, establezca el `fetchTask` parámetro `true` en en el manifiesto.

Al igual que en el flujo de tarjeta adaptable, el servicio `fetchTask` enviará un evento y debe responder con una [respuesta del módulo de tarea](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)basada en URL. A continuación se muestra una respuesta de ejemplo con una tarjeta adaptable:

```json
{
    "task": {
        "value": {
            "url": "http://mywebapp.com/input"
        },
        "type": "continue"
    }
}
```

### <a name="request-to-install-your-conversational-bot"></a>Solicitud para instalar el bot Conversation

Si la aplicación también contiene un bot Conversation, puede que sea necesario asegurarse de que el bot está instalado en la conversación antes de cargar el módulo de tareas. Esto puede ser útil en situaciones en las que necesita obtener contexto adicional para el módulo de tareas. Por ejemplo, puede que necesite recuperar la lista para rellenar un control de selector de personas o la lista de canales en un equipo.

Para facilitar este flujo, cuando la extensión de mensajería recibe primero `composeExtension/fetchTask` la comprobación de la invocación para ver si el bot está instalado en el contexto actual (para ello, puede intentar la llamada obtener lista, por ejemplo). Si el bot no está instalado, se devuelve una tarjeta adaptable con una acción que solicita al usuario que instale el bot. Consulte el ejemplo siguiente. Tenga en cuenta que esto requiere que el usuario tenga permiso para instalar aplicaciones en esa ubicación; Si no se pueden presentar con un mensaje que les pide que se ponga en contacto con el administrador.

Este es un ejemplo de la respuesta:

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

Una vez que el usuario completa la instalación, el bot recibirá otro mensaje de `name = composeExtension/submitAction`llamada con `value.data.msteams.justInTimeInstall = true`y.

A continuación, se muestra un ejemplo de Invoke:

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

Debe responder a esta Invocación con la misma respuesta de tarea que habría respondido si el bot ya está instalado.

## <a name="responding-to-submit"></a>Responder al envío

Una vez que un usuario termina de escribir su entrada, el bot `composeExtension/submitAction` recibirá un evento con el identificador de comando y los valores de parámetro establecidos.

Estas son las diferentes respuestas esperadas a `submitAction`un.

### <a name="task-module-response"></a>Respuesta del módulo de tareas

Se usa cuando la extensión tiene que encadenar cuadros de diálogo juntos para obtener más información. La respuesta es exactamente la misma que `fetchTask` se mencionó anteriormente.

### <a name="compose-extension-authconfig-response"></a>Escribir respuesta de autenticación/configuración de extensión

Se usa cuando la extensión debe ser autenticada o configurada para continuar. Consulte la [sección autenticación](~/resources/messaging-extension-v3/search-extensions.md#authentication) en la sección Buscar para obtener más información.

### <a name="compose-extension-result-response"></a>Respuesta de resultado de la extensión de redacción

Esto se usa para insertar una tarjeta en el cuadro de redacción como resultado de un comando. Se trata de la misma respuesta que se usa en el comando de búsqueda, pero está limitada a una tarjeta o a un resultado de la matriz.

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        },
    "attachments": [
      {  
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage": "https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value": "[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        }
      }
    ]
  }
}
```

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a>Responder con un mensaje de tarjeta adaptable enviado desde un bot

También puede responder a la acción de envío Insertando un mensaje con una tarjeta adaptable en el canal con un bot. El usuario podrá obtener una vista previa del mensaje antes de enviarlo y, potencialmente, editarlo o interactuar con él. Esto puede ser muy útil en escenarios en los que es necesario recopilar información de los usuarios antes de crear una respuesta de tarjeta adaptable. El siguiente escenario muestra cómo se puede usar este flujo para configurar un sondeo sin incluir los pasos de configuración en el mensaje de canal.

1. El usuario hace clic en la extensión de mensajería para desencadenar el módulo de tareas.
1. El usuario usa el módulo de tareas para configurar el sondeo.
1. Después de enviar el módulo de tareas de configuración, la aplicación usa la información proporcionada en el módulo de tareas para diseñar una tarjeta adaptable `botMessagePreview` y enviarla como respuesta al cliente.
1. A continuación, el usuario puede obtener una vista previa del mensaje de tarjeta adaptable antes de que el bot lo inserte en el canal. Si el bot todavía no es miembro del canal, al hacer clic `Send` se agregará el bot.
1. La interacción con la tarjeta adaptable modificará el mensaje antes de enviarlo.
1. Una vez que el usuario `Send` hace clic en el bot, el mensaje se enviará al canal.

Para habilitar este flujo, el módulo de tareas debe responder como se muestra en el ejemplo siguiente, que presentará el mensaje de vista previa al usuario.

>[!Note]
>El `activityPreview` debe contener una `message` actividad con exactamente 1 archivo adjunto de tarjeta adaptable.

```json
{
  "composeExtension": {
    "type": "botMessagePreview",
    "activityPreview": {
      "type": "message",
      "attachments":  [
        {
          "contentType": "application/vnd.microsoft.card.adaptive",
          "content": << Card Payload >>
        }
      ]
    }
  }
}
```

La extensión de mensajes ahora tendrá que responder a dos nuevos tipos de interacciones `value.botMessagePreviewAction = "send"` y `value.botMessagePreviewAction = "edit"`. A continuación se muestra un ejemplo `value` del objeto que tendrá que procesar:

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "send" | "edit",
    "botActivityPreview": [
      {
        "type": "message/card",
        "attachments": [
          {
            "content":
              {
                "type": "AdaptiveCard",
                "body": [{<<card payload>>}]
              },
            "contentType" : "application/vnd.microsoft.card.adaptive"
          }
        ],
        "context": { "theme": "default" }
      }
    ],
  }
}
```

Al responder a la `edit` solicitud, debe responder con una `task` respuesta con los valores que se han rellenado con la información que el usuario ya ha enviado. Al responder a la `send` solicitud, debe enviar un mensaje al canal que contiene la tarjeta adaptable que ha finalizado.

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node. js](#tab/typescript)

En el ejemplo siguiente, se muestra cómo hacerlo con el [SDK de Team. js para Teams Builder](https://www.npmjs.com/package/botbuilder-teams).

```typescript
teamChatConnector.onComposeExtensionSubmitAction((
    event: builder.IEvent,
    request: teamBuilder.IComposeExtensionActionCommandRequest,
    callback: (err: Error, result: any, statusCode: number) => void) => {
        let invokeValue = (<any> event).value;

        if (invokeValue.botMessagePreviewAction ) {
            let attachment = invokeValue.botActivityPreview[0].attachments[0];

            if (invokeValue.botMessagePreviewAction === 'send') {
                let msg = new builder.Message()
                    .address(event.address)
                    .addAttachment(attachment);
                teamChatConnector.send([msg.toMessage()],
                    (error) => {
                        if(error){
                            //TODO: Handle error and callback
                        }
                        else {
                            callback(null, null, 200);
                        }
                    }
                );
            }

            else if (invokeValue.botMessagePreviewAction === 'edit') {
              // Create the card and populate with user-inputted information
              let card = { ... }

              let taskResponse = {
                task: {
                  type: "continue",
                  value: {
                    title: "Card Preview",
                    card: {
                      contentType: 'application/vnd.microsoft.card.adaptive',
                      content: card
                    }
                  }
                }
              }
              callback(null, taskResponse, 200);
            }

        else {
            let attachment = {
                  //create adaptive card
                };
            let activity = new builder.Message().addAttachment(attachment).toMessage();
            let response = teamBuilder.ComposeExtensionResponse.messagePreview()
                .preview(activity)
                .toResponse();
            callback(null, response, 200);
        }
    });
```

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

En este ejemplo se muestra este flujo mediante el [SDK de Microsoft. bot. Connector. Teams (V3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).

```csharp
public class MessagesController : ApiController
{

    [BotAuthentication]
    public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
    {
        MicrosoftAppCredentials.TrustServiceUrl(activity.ServiceUrl, DateTime.MaxValue);
        ConnectorClient connectorClient = new ConnectorClient(
            new Uri(activity.ServiceUrl),
            ConfigurationManager.AppSettings[MicrosoftAppCredentials.MicrosoftAppIdKey],
            ConfigurationManager.AppSettings[MicrosoftAppCredentials.MicrosoftAppPasswordKey]);

        if (activity.Type == ActivityTypes.Invoke)
        {
            // Initial task module presented to the user
            if (activity.Name == "composeExtension/fetchTask")
            {
                string task = GetTaskModule();

                return Request.CreateResponse(HttpStatusCode.OK, JObject.Parse(task));
            }
            else if (activity.Name == "composeExtension/submitAction")
            {
                dynamic activityValue = JObject.FromObject(activity.Value);
                string botMessagePreviewAction = activityValue["botMessagePreviewAction"];

                //This is the initial card response sent after the task module is submitted
                if (botMessagePreviewAction is null)
                {
                    string text = activityValue.data.cardMessage;

                    AdaptiveCard card = new AdaptiveCard(new AdaptiveSchemaVersion("1.0"));
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = "This card will be inserted into the conversation by the bot.",
                        Size = AdaptiveTextSize.Large,
                        Wrap = true
                    });
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = "The text below is what you provided."
                    });
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = text,
                    });

                    string cardJson = card.ToJson();

                    string cardMessage = $@"{{
                        'composeExtension': {{
                        'type': 'botMessagePreview',
                        'activityPreview': {{
                            'type': 'message',
                            'attachments': [{{
                                'contentType': 'application/vnd.microsoft.card.adaptive',
                                'content': {cardJson}
                            }}]
                        }}
                        }}
                    }}";

                    JObject res = JObject.Parse(cardMessage);
                    return Request.CreateResponse(HttpStatusCode.OK, res);

                }
                else
                {
                    //This is the "send the card to the channel" event
                    if (botMessagePreviewAction.Equals("send"))
                    {
                        string cardJson = JsonConvert.SerializeObject(activityValue.botActivityPreview[0].attachments[0].content);

                        AdaptiveCardParseResult cardResult = AdaptiveCard.FromJson(cardJson);
                        AdaptiveCard card = cardResult.Card;
                        Attachment cardAttachment = new Attachment
                        {
                            ContentType = AdaptiveCard.ContentType,
                            Content = card
                        };


                        Activity response = activity.CreateReply();
                        response.Attachments.Add(cardAttachment);

                        var result = await connectorClient.Conversations.SendToConversationAsync(response);
                    }
                    //This is fired if the user edits the card before sending it
                    else if (botMessagePreviewAction.Equals("edit"))
                    {
                        string task = GetTaskModule();

                        return Request.CreateResponse(HttpStatusCode.OK, JObject.Parse(task));
                    }
                    else
                    {
                        return Request.CreateResponse(HttpStatusCode.NotImplemented);
                    }
                }
            }
        }

        return Request.CreateResponse(HttpStatusCode.NotImplemented);

    }

    private static string GetTaskModule()
    {
        AdaptiveCard card = new AdaptiveCard(new AdaptiveSchemaVersion("1.0"));
        card.Body.Add(new AdaptiveTextBlock()
        {
            Text = "Please enter the following information:",
            Size = AdaptiveTextSize.Large
        });
        card.Body.Add(new AdaptiveTextBlock()
        {
            Text = "Card Message:"
        });
        card.Body.Add(new AdaptiveTextInput()
        {
            Id = "cardMessage",
            Spacing = AdaptiveSpacing.None,
            Placeholder = "Card message goes here."
        });
        card.Actions.Add(new AdaptiveSubmitAction()
        {
            Title = "Submit"
        });

        string cardJson = card.ToJson();

        //Create the task module response
        string task = $@"{{
                            'task': {{
                                'type': 'continue',
                                'value': {{
                                    'card': {{
                                        'contentType': 'application/vnd.microsoft.card.adaptive',
                                        'content': {cardJson}
                                        }}
                                    }}
                                }}
                            }}";
        return task;
    }

}
```

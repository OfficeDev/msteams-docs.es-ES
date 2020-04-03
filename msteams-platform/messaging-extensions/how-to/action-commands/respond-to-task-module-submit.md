---
title: Responder a la acción de envío del módulo de tareas
author: clearab
description: Describe cómo responder a la acción de envío del módulo de tareas desde un comando de acción de la extensión de mensajería.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 6372a683a7c9f08551a9c0d126a0db2ab9212e66
ms.sourcegitcommit: 058b7bbd817af5f513e0e018f2ef562dc3086a84
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2020
ms.locfileid: "43120265"
---
# <a name="respond-to-the-task-module-submit-action"></a>Responder a la acción de envío del módulo de tareas

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Una vez que un usuario envía el módulo de tareas, el servicio web recibirá un `composeExtension/submitAction` mensaje de invocación con los valores del identificador de comando y el parámetro establecidos. La aplicación tendrá cinco segundos para responder a la invocación, de lo contrario el usuario recibirá el mensaje de error "no se puede comunicar la aplicación" y cualquier respuesta a la invocación será ignorada por el cliente de Teams.

Tiene las siguientes opciones para responder.

* Sin respuesta: puede elegir usar la acción enviar para desencadenar un proceso en un sistema externo y no enviar comentarios al usuario. Esto puede ser útil para los procesos de ejecución prolongada y puede elegir proporcionar comentarios de otra forma (por ejemplo, con un [mensaje proactivo](~/bots/how-to/conversations/send-proactive-messages.md)).
* [Otro módulo de tareas](#respond-with-another-task-module) : puede responder con un módulo de tareas adicional como parte de una interacción de varios pasos.
* [Respuesta de tarjeta](#respond-with-a-card-inserted-into-the-compose-message-area) : puede responder con una tarjeta a la que el usuario puede interactuar o insertarla en un mensaje.
* [Tarjeta adaptable desde bot](#bot-response-with-adaptive-card) : Inserte una tarjeta adaptable directamente en la conversación.
* [Solicitar al usuario que se autentique](~/messaging-extensions/how-to/add-authentication.md)
* [Solicitar al usuario que proporcione una configuración adicional](~/messaging-extensions/how-to/add-configuration-page.md)

En la tabla siguiente se muestran los tipos de respuestas disponibles en función de la ubicación`commandContext`de invocación () de la extensión de mensajería. Para la autenticación o la configuración, una vez que el usuario completa el flujo, la invocación original se volverá a enviar a su servicio Web.

|Tipo de respuesta | elaborar | barra de comandos | mensaje |
|--------------|:-------------:|:-------------:|:---------:|
|Respuesta de tarjeta | x | x | x |
|Otro módulo de tareas | x | x | x |
|Bot con tarjeta adaptable | x |  | x |
| Sin respuesta | x | x | x |

## <a name="the-submitaction-invoke-event"></a>Evento Invoke de submitAction

A continuación se muestran ejemplos de cómo recibir el mensaje de invocación.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejs"></a>[JavaScript/node. js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  constructor() {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
  
  //code to handle the submit action
    }
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

Este es un ejemplo del objeto JSON que recibirá. El `commandContext` parámetro indica desde dónde se desencadenó la extensión de mensajería. El `data` objeto contiene los campos en el formulario como parámetros y los valores enviados por el usuario. El objeto JSON se acorta para resaltar los campos más relevantes.

```json
{
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith",
  "serviceUrl": "https://smba.trafficmanager.net/amer/",
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "id": "submitButton",
      "formField1": "formField1_value",
      "formField2": "formField2_value",
      "formField3": "formField3_value"
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  }
}
```

* * *

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a>Responder con una tarjeta insertada en el área de redacción del mensaje

La forma más común de responder a la `composeExtension/submitAction` solicitud es con una tarjeta insertada en el área de redacción del mensaje. A continuación, el usuario puede elegir enviar la tarjeta a la conversación. Para obtener más información sobre el uso de tarjetas [, consulte acciones de tarjetas y tarjetas](~/task-modules-and-cards/cards/cards-actions.md).

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
    dynamic Data = JObject.Parse(action.Data.ToString());
    var response = new MessagingExtensionActionResponse
    {
        ComposeExtension = new MessagingExtensionResult
        {
            AttachmentLayout = "list",
            Type = "result",
        },
    };
    var card = new HeroCard
    {
        Title = Data["formField1"] as string,
        Subtitle = Data["formField2"]  as string,
        Text = Data["formField3"]  as string,
    };

    var attachments = new List<MessagingExtensionAttachment>();
    attachments.Add(new MessagingExtensionAttachment
    {
        Content = card,
        ContentType = HeroCard.ContentType,
        Preview = card.ToAttachment(),
    });

    response.ComposeExtension.Attachments = attachments;

    return response;

}
```

# <a name="javascriptnodejs"></a>[JavaScript/node. js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
    const data = action.data;
    const heroCard = CardFactory.heroCard(data.title, data.text);
    heroCard.content.subtitle = data.subTitle;
    const attachment = { contentType: heroCard.contentType, content: heroCard.content, preview: heroCard };

    return {
      composeExtension: {
        type: 'result',
        attachmentLayout: 'list',
        attachments: [
          attachment
        ]
      }
    }
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "composeExtension": {
    "attachmentLayout": "list",
    "type": "result",
    "attachments": [
      {
        "preview": {
          "contentType": "application/vnd.microsoft.card.hero",
          "content": {
            "title": "formField1_value",
            "subtitle": "formField2_value",
            "text": "formField3_value"
          }
        },
        "contentType": "application/vnd.microsoft.card.hero",
        "content": {
          "title": "formField1_value",
          "subtitle": "formField2_value",
          "text": "formField3_value"
        }
      }
    ]
  }
}
```

* * *

## <a name="respond-with-another-task-module"></a>Responder con otro módulo de tareas

Puede elegir responder al `submitAction` evento con un módulo de tareas adicional. Esto puede ser útil cuando:

* Tiene que recopilar grandes cantidades de información.
* Si necesita cambiar dinámicamente la información que va a recopilar en función de los datos proporcionados por el usuario
* Si necesita validar la información enviada por el usuario y, potencialmente, volver a enviar el formulario con un mensaje de error si algo es incorrecto. 

El método para Response es el mismo que [responder al evento `fetchTask` inicial](~/messaging-extensions/how-to/action-commands/create-task-module.md). Si está usando el SDK de bot Framework, el mismo evento se activará para las acciones de envío. Esto significa que debe asegurarse de agregar una lógica que determine la respuesta correcta.

## <a name="bot-response-with-adaptive-card"></a>Respuesta de bot con tarjeta adaptable

>[!Note]
>Este flujo requiere que agregue el `bot` objeto al manifiesto de la aplicación y que haya definido el ámbito necesario para el bot. Use el mismo identificador que su extensión de mensajería para el bot.

También puede responder a la acción de envío Insertando un mensaje con una tarjeta adaptable en el canal con un bot. El usuario podrá obtener una vista previa del mensaje antes de enviarlo y, potencialmente, editarlo o interactuar con él. Esto puede ser muy útil en escenarios en los que necesite recopilar información de los usuarios antes de crear una respuesta de tarjeta adaptable, o cuando vaya a necesitar actualizar la tarjeta después de que alguien interactúe con ella. El siguiente escenario muestra cómo la aplicación Polly usa este flujo para configurar un sondeo sin incluir los pasos de configuración en la conversación de canal.

1. El usuario hace clic en la extensión de mensajería para desencadenar el módulo de tareas.
2. El usuario configura el sondeo con el módulo de tareas.
3. Después de enviar el módulo de tareas, la aplicación usa la información proporcionada para compilar el sondeo como una tarjeta adaptable y enviarla como `botMessagePreview` respuesta al cliente.
4. A continuación, el usuario puede obtener una vista previa del mensaje de tarjeta adaptable antes de que el bot lo inserte en el canal. Si la aplicación aún no es miembro del canal, al hacer clic `Send` se agregará.
   1. El usuario también puede elegir `Edit` el mensaje, que lo devuelve al módulo de tareas original.
5. Interactuar con la tarjeta adaptable cambia el mensaje antes de enviarlo.
6. Una vez que el usuario `Send` hace clic en el bot, el mensaje se envía al canal.

### <a name="respond-to-initial-submit-action"></a>Responder a la acción de envío inicial

Para habilitar este flujo, el módulo de tareas debe responder al `composeExtension/submitAction` mensaje inicial con una vista previa de la tarjeta que el bot enviará al canal. De esta forma, el usuario tendrá la oportunidad de comprobar la tarjeta antes de enviarla y también intentará instalar el bot en la conversación, si no está ya instalado.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  dynamic Data = JObject.Parse(action.Data.ToString());
  var response = new MessagingExtensionActionResponse
  {
    ComposeExtension = new MessagingExtensionResult
    {
      Type = "botMessagePreview",
      ActivityPreview = MessageFactory.Attachment(new Attachment
      {
        Content = new AdaptiveCard("1.0")
        {
          Body = new List<AdaptiveElement>()
          {
            new AdaptiveTextBlock() { Text = "FormField1 value was:", Size = AdaptiveTextSize.Large },
            new AdaptiveTextBlock() { Text = Data["FormField1"] as string }
          },
          Height = AdaptiveHeight.Auto,
          Actions = new List<AdaptiveAction>()
          {
            new AdaptiveSubmitAction
            {
              Type = AdaptiveSubmitAction.TypeName,
              Title = "Submit",
              Data = new JObject { { "submitLocation", "messagingExtensionFetchTask" } },
            },
          }
        },
        ContentType = AdaptiveCard.ContentType
      }) as Activity
    }
  };

  return response;
}
```

# <a name="javascriptnodejs"></a>[JavaScript/node. js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
    const submittedData = action.data;
    const adaptiveCard = CardFactory.adaptiveCard({
      actions: [
        { type: 'Action.Submit', title: 'Submit', data: { submitLocation: 'messagingExtensionSubmit' } }
      ],
      body: [
          { text: 'Adaptive Card from Task Module', type: 'TextBlock', weight: 'bolder' },
          { text: `${ submittedData.Question }`, type: 'TextBlock', id: 'Question' },
          { id: 'Answer', placeholder: 'Answer here...', type: 'Input.Text' },
        {
          choices: [
            { title: submittedData.Option1, value: submittedData.Option1 },
            { title: submittedData.Option2, value: submittedData.Option2 },
            { title: submittedData.Option3, value: submittedData.Option3 }
          ],
          id: 'Choices',
          isMultiSelect: submittedData.MultiSelect,
          style: 'expanded',
          type: 'Input.ChoiceSet'
        }
      ],
      type: 'AdaptiveCard',
      version: '1.0'
    });
    return {
      composeExtension: {
        activityPreview: MessageFactory.attachment(adaptiveCard, null, null, InputHints.ExpectingInput),
        type: 'botMessagePreview'
      }
    };
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

>[!Note]
>El `activityPreview` debe contener una `message` actividad con exactamente 1 archivo adjunto de tarjeta adaptable. El `<< Card Payload >>` valor es un marcador de posición para la tarjeta que desea enviar.

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

* * *

### <a name="the-botmessagepreview-send-and-edit-events"></a>Los eventos de envío y edición de botMessagePreview

La extensión de mensajes ahora tendrá que responder a dos nuevas variedades de la `composeExtension/submitAction` llamada, donde `value.botMessagePreviewAction = "send"`y `value.botMessagePreviewAction = "edit"`.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionBotMessagePreviewEditAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle the event
}

protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionBotMessagePreviewSendAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle the event
}

```

# <a name="javascriptnodejs"></a>[JavaScript/node. js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionBotMessagePreviewEdit(context, action) {

    //handle the event
  }
  
  handleTeamsMessagingExtensionBotMessagePreviewSend(context, action) {

    //handle the event
  }
}

```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "edit | send",
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

* * *

### <a name="respond-to-botmessagepreview-edit"></a>Responder a la edición de botMessagePreview

Si el usuario decide editar la tarjeta antes de enviarla haciendo clic en el botón **Editar** , recibirá `composeExtension/submitAction` una llamada `value.botMessagePreviewAction = edit`con el. Por lo general, debe responder devolviendo el módulo de tarea que envió como respuesta `composeExtension/fetchTask` a la invocación inicial que inició la interacción. Esto permite al usuario iniciar el proceso volviendo a introducir la información original. También debe considerar la posibilidad de usar la información que ya tiene disponible para rellenar previamente el módulo de tareas, de modo que el usuario no haya rellenado toda la información desde cero.

Consulte [responder al evento inicial `fetchTask` ](~/messaging-extensions/how-to/action-commands/create-task-module.md).

### <a name="respond-to-botmessagepreview-send"></a>Responder a botMessagePreview envío

Una vez que el usuario hace clic en el botón **Enviar** , recibirá `composeExtension/submitAction` una `value.botMessagePreviewAction = send`llamada con. El servicio Web tendrá que crear y enviar un mensaje proactivo con la tarjeta adaptable a la conversación y también responder a la invocación.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionBotMessagePreviewSendAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var activityPreview = action.BotActivityPreview[0];
  var attachmentContent = activityPreview.Attachments[0].Content;
  var previewedCard = JsonConvert.DeserializeObject<AdaptiveCard>(attachmentContent.ToString(),
          new JsonSerializerSettings { NullValueHandling = NullValueHandling.Ignore });
  
  previewedCard.Version = "1.0";

  var responseActivity = Activity.CreateMessageActivity();
  Attachment attachment = new Attachment()
  {
    ContentType = AdaptiveCard.ContentType,
    Content = previewedCard
  };
  responseActivity.Attachments.Add(attachment);
  
  await turnContext.SendActivityAsync(responseActivity);

  return new MessagingExtensionActionResponse();
}
```

# <a name="javascriptnodejs"></a>[JavaScript/node. js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionBotMessagePreviewSend(context, action) {
      // The data has been returned to the bot in the action structure.
      const activityPreview = action.botActivityPreview[0];
      const attachmentContent = activityPreview.attachments[0].content;
      const userText = attachmentContent.body[1].text;
      const choiceSet = attachmentContent.body[3];
      
      const submitData = {
        MultiSelect: choiceSet.isMultiSelect ? 'true' : 'false',
        Option1: choiceSet.choices[0].title,
        Option2: choiceSet.choices[1].title,
        Option3: choiceSet.choices[2].title,
        Question: userText
      };
    
      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [
          { type: 'Action.Submit', title: 'Submit', data: { submitLocation: 'messagingExtensionSubmit' } }
        ],
        body: [
          { text: 'Adaptive Card from Task Module', type: 'TextBlock', weight: 'bolder' },
          { text: `${ submitData.Question }`, type: 'TextBlock', id: 'Question' },
          { id: 'Answer', placeholder: 'Answer here...', type: 'Input.Text' },
          {
            choices: [
                { title: submitData.Option1, value: submitData.Option1 },
                { title: submitData.Option2, value: submitData.Option2 },
                { title: submitData.Option3, value: submitData.Option3 }
            ],
            id: 'Choices',
            isMultiSelect: submitData.MultiSelect,
            style: 'expanded',
            type: 'Input.ChoiceSet'
          }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });
      const responseActivity = { type: 'message', attachments: [adaptiveCard] };
    
      await context.sendActivity(responseActivity);
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

Recibirá un mensaje nuevo `composeExtension/submitAction` similar al que se muestra a continuación.

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "send",
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

* * *

## <a name="next-steps"></a>Siguientes pasos

Agregar un comando de búsqueda

* [Definir comandos de búsqueda](~/messaging-extensions/how-to/search-commands/define-search-command.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]

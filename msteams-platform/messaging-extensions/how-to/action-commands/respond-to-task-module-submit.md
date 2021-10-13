---
title: Responder a la acción de envío del módulo de tareas
author: surbhigupta
description: Describe cómo responder a la acción de envío del módulo de tareas desde un comando de acción de extensión de mensajería
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: cab33a36862ed027f9c110eccaac43d4e4aff20e
ms.sourcegitcommit: 37b1724bb0d2f1b087c356e0fd0ff80145671e22
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2021
ms.locfileid: "60291642"
---
# <a name="respond-to-the-task-module-submit-action"></a>Responder a la acción de envío del módulo de tareas

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Este documento te guía sobre cómo la aplicación responde a los comandos de acción, como la acción de envío del módulo de tareas del usuario.
Después de que un usuario envíe el módulo de tareas, el servicio web recibe un mensaje de invocación `composeExtension/submitAction` con el identificador de comando y los valores de parámetro. La aplicación tiene cinco segundos para responder a la invocación, de lo contrario, el usuario recibe un mensaje de error No se puede llegar a la aplicación **y** el cliente de Teams omite cualquier respuesta a la invocación.

Tiene las siguientes opciones para responder:

* Sin respuesta: use la acción enviar para desencadenar un proceso en un sistema externo y no proporcionar comentarios al usuario. Esto es útil para procesos de larga ejecución y puede seleccionar proporcionar comentarios alternativamente. Por ejemplo, puede enviar comentarios con un [mensaje proactivo](~/bots/how-to/conversations/send-proactive-messages.md).
* [Otro módulo de](#respond-with-another-task-module)tareas: puede responder con un módulo de tareas adicional como parte de una interacción de varios pasos.
* [Respuesta de](#respond-with-a-card-inserted-into-the-compose-message-area)tarjeta: puede responder con una tarjeta con la que el usuario puede interactuar o insertar en un mensaje.
* [Tarjeta adaptable desde el bot:](#bot-response-with-adaptive-card)inserte una tarjeta adaptable directamente en la conversación.
* [Solicitar al usuario que autentique](~/messaging-extensions/how-to/add-authentication.md).
* [Solicitar al usuario que proporcione una configuración adicional]~/get-started/first-message-extension.md).

Para la autenticación o configuración, después de que el usuario complete el proceso, la invocación original se resiente al servicio web. En la tabla siguiente se muestran los tipos de respuestas disponibles en función de la ubicación de invocación `commandContext` de la extensión de mensajería: 

|Tipo de respuesta | Redacción | Barra de comandos | Message |
|--------------|:-------------:|:-------------:|:---------:|
|Respuesta de tarjeta | ✔ | ✔ | ✔ |
|Otro módulo de tareas | ✔ | ✔ | ✔ |
|Bot con tarjeta adaptable | ✔ | x | ✔ |
| Sin respuesta | ✔ | ✔ | ✔ |

> [!NOTE]
> * Cuando selecciona **Action.Submit** a través de tarjetas ME, envía actividad invoke con el nombre **composeExtension**, donde el valor es igual a la carga habitual.
> * Cuando selecciona **Action.Submit** a través de la conversación, recibe actividad de mensaje con el nombre **onCardButtonClicked**, donde el valor es igual a la carga habitual.

## <a name="the-submitaction-invoke-event"></a>El evento de invocación submitAction

Los ejemplos de recibir el mensaje de invocación son los siguientes:

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

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

Este es un ejemplo del objeto JSON que recibe. El `commandContext` parámetro indica de dónde se desencadenó la extensión de mensajería. El `data` objeto contiene los campos del formulario como parámetros y los valores enviados por el usuario. El objeto JSON aquí se abrevia para resaltar los campos más relevantes.

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

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a>Responder con una tarjeta insertada en el área del mensaje de redacción

La forma más común de responder a la `composeExtension/submitAction` solicitud es con una tarjeta insertada en el área del mensaje de redacción. El usuario envía la tarjeta a la conversación. Para obtener más información sobre el uso de tarjetas, vea [tarjetas y acciones de tarjeta.](~/task-modules-and-cards/cards/cards-actions.md)

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
    var response = new MessagingExtensionActionResponse
    {
        ComposeExtension = new MessagingExtensionResult
        {
            AttachmentLayout = "list",
            Type = "result",
        },
    };
    var createCardData = ((JObject)action.Data).ToObject<CreateCardData>();
var card = new HeroCard
{
     Title = createCardData.Title,
     Subtitle = createCardData.Subtitle,
     Text = createCardData.Text,
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

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

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

Puede seleccionar para responder al evento `submitAction` con un módulo de tareas adicional. Esto resulta útil cuando:

* Debe recopilar grandes cantidades de información.
* Debe cambiar dinámicamente la información que está recopilando en función de la entrada del usuario.
* Debe validar la información enviada por el usuario y volver a enviar el formulario con un mensaje de error si hay algún error. 

El método de respuesta es el mismo que [responder al evento `fetchTask` inicial](~/messaging-extensions/how-to/action-commands/create-task-module.md). Si usa el SDK de Bot Framework, los mismos desencadenadores de eventos para ambas acciones de envío. Para que esto funcione, debe agregar lógica que determine la respuesta correcta.

## <a name="bot-response-with-adaptive-card"></a>Respuesta del bot con tarjeta adaptable

> [!NOTE]
> El requisito previo para obtener la respuesta del bot con una tarjeta adaptable es que debes agregar el objeto al manifiesto de la aplicación y definir el ámbito `bot` necesario para el bot. Usa el mismo identificador que la extensión de mensajería para el bot.
 
También puede responder al insertar un mensaje con una tarjeta adaptable `submitAction` en el canal con un bot. El usuario puede obtener una vista previa del mensaje antes de enviarlo. Esto es muy útil en escenarios en los que se recopila información de los usuarios antes de crear una respuesta de tarjeta adaptable o cuando se actualiza la tarjeta después de que alguien interactúa con ella. 

El siguiente escenario muestra cómo la aplicación Polly configura un sondeo sin incluir los pasos de configuración en la conversación del canal:

**Para configurar el sondeo**

1. El usuario selecciona la extensión de mensajería para invocar el módulo de tareas.
1. El usuario configura el sondeo con el módulo de tareas.
1. Después de enviar el módulo de tareas, la aplicación usa la información proporcionada para crear el sondeo como una tarjeta adaptable y la envía como respuesta `botMessagePreview` al cliente.
1. A continuación, el usuario puede obtener una vista previa del mensaje de tarjeta adaptable antes de que el bot lo inserte en el canal. Si la aplicación aún no es miembro del canal, selecciona `Send` para agregarla.

    > [!NOTE] 
    > * Los usuarios también pueden seleccionar `Edit` el mensaje, que los devuelve al módulo de tareas original. 
    > * La interacción con la tarjeta adaptable cambia el mensaje antes de enviarlo.
1. Después de que el usuario seleccione `Send` el bot, publica el mensaje en el canal.

## <a name="respond-to-initial-submit-action"></a>Responder a la acción de envío inicial

El módulo de tareas debe responder al mensaje inicial con una vista previa de la tarjeta que el `composeExtension/submitAction` bot envía al canal. El usuario puede comprobar la tarjeta antes de enviar e intentar instalar el bot en la conversación si el bot aún no está instalado.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  dynamic createCardData = ((JObject) action.Data).ToObject(typeof(JObject));
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

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

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

> [!NOTE]
> * Debe `activityPreview` contener una actividad con exactamente un dato adjunto de tarjeta `message` adaptable. El `<< Card Payload >>` valor es un marcador de posición para la tarjeta que desea enviar.

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

### <a name="the-botmessagepreview-send-and-edit-events"></a>Eventos de envío y edición botMessagePreview

La extensión de mensajería debe responder a dos nuevos tipos de `composeExtension/submitAction` invocación, where `value.botMessagePreviewAction = "send"` y `value.botMessagePreviewAction = "edit"` .

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

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

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

### <a name="respond-to-botmessagepreview-edit"></a>Responder a la edición botMessagePreview

Si el usuario edita la tarjeta antes de enviarla, **seleccionando Editar**, recibirá una `composeExtension/submitAction` invocación con `value.botMessagePreviewAction = edit` . Debe responder devolviendo el módulo de tareas que envió, en respuesta a la invocación inicial `composeExtension/fetchTask` que inició la interacción. Esto permite al usuario iniciar el proceso entrando de nuevo en la información original. Use la información disponible para actualizar el módulo de tareas de modo que el usuario no necesite rellenar toda la información desde cero.
Para obtener más información sobre cómo responder al evento inicial, vea `fetchTask` responding to the initial [ `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).

### <a name="respond-to-botmessagepreview-send"></a>Responder al envío botMessagePreview

Después de que el usuario seleccione **El envío**, recibirá una `composeExtension/submitAction` invocación con `value.botMessagePreviewAction = send` . El servicio web debe crear y enviar un mensaje proactivo con la tarjeta adaptable a la conversación y responder también a la invocación.

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
  
  // Attribute the message to the user on whose behalf the bot is posting
  responseActivity.ChannelData = new {
    OnBehalfOf = new []
    {
      new
      {
        ItemId = 0,
        MentionType = "person",
        Mri = turnContext.Activity.From.Id,
        DisplayName = turnContext.Activity.From.Name
      }  
    }
  };
  
  await turnContext.SendActivityAsync(responseActivity);

  return new MessagingExtensionActionResponse();
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

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
      const responseActivity = { type: 'message', attachments: [adaptiveCard], channelData: {
          onBehalfOf: [
              { itemId: 0, mentionType: 'person', mri: context.activity.from.id, displayname: context.activity.from.name }
          ]
      }};

      await context.sendActivity(responseActivity);
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

Recibirá un nuevo `composeExtension/submitAction` mensaje similar al siguiente:

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

### <a name="user-attribution-for-bots-messages"></a>Atribución de usuarios para mensajes de bots 

En escenarios en los que un bot envía mensajes en nombre de un usuario, la atribución del mensaje a ese usuario ayuda a la interacción y muestra un flujo de interacción más natural. Esta característica le permite atribuir un mensaje del bot a un usuario en cuyo nombre se envió.

En la imagen siguiente, a la izquierda hay un mensaje de tarjeta enviado por un bot sin atribución del usuario y a la derecha es una tarjeta enviada por un bot con atribución de usuario.

![bots de atribución de usuarios](../../../assets/images/messaging-extension/user-attribution-bots.png)

Para usar la atribución de usuario en teams, debe agregar la entidad de mención en la carga que `OnBehalfOf` `ChannelData` se envía a `Activity` Teams.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet-1)

```csharp
    OnBehalfOf = new []
    {
      new
      {
        ItemId = 0,
        MentionType = "person",
        Mri = turnContext.Activity.From.Id,
        DisplayName = turnContext.Activity.From.Name
      }  
    }

```

# <a name="json"></a>[JSON](#tab/json-1)

```json
{
    "text": "Hello World!",
    "ChannelData": {
        "OnBehalfOf": [{
            "itemid": 0,
            "mentionType": "person",
            "mri": "29:orgid:89e6508d-6c0f-4ffe-9f6a-b58416d965ae",
            "displayName": "Sowrabh N R S"
        }]
    }
}
```

* * *

#### <a name="details-of--onbehalfof-entity-schema"></a>Detalles del  `OnBehalfOf` esquema de entidad

La siguiente sección es una descripción de las entidades de la `OnBehalfOf` matriz:

|Campo|Tipo|Descripción|
|:---|:---|:---|
|`itemId`|Entero|Describe la identificación del elemento. Su valor debe ser `0` .|
|`mentionType`|String|Describe la mención de una "persona".|
|`mri`|String|Identificador de recurso de mensaje (MRI) de la persona en cuyo nombre se envía el mensaje. El nombre del remitente del mensaje aparecería como " \<user\> a \<bot name\> través de ".|
|`displayName`|Cadena|Nombre de la persona. Se usa como reserva en caso de que la resolución de nombres no esté disponible.|
  
## <a name="code-sample"></a>Ejemplo de código

| Nombre de ejemplo           | Descripción | .NET    | Node.js   |   
|:---------------------|:--------------|:---------|:--------|
|Teams extensión de mensajería| Describe cómo definir comandos de acción, crear módulo de tareas y responder a la acción de envío del módulo de tareas. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|Teams de extensión de mensajería   |  Describe cómo definir comandos de búsqueda y responder a las búsquedas.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Definición de comandos de búsqueda](~/messaging-extensions/how-to/search-commands/define-search-command.md)


---
title: Responder a la acción de envío del módulo de tareas
author: clearab
description: Describe cómo responder a la acción de envío del módulo de tarea desde un comando de acción de extensión de mensajería
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 1fb2f2dc51d7de1208a5a913abf2d38cb80c401a
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231648"
---
# <a name="respond-to-the-task-module-submit-action"></a>Responder a la acción de envío del módulo de tareas

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Una vez que un usuario envía el módulo de tarea, el servicio web recibe un mensaje de invocación con los valores de identificador de comando `composeExtension/submitAction` y parámetros. La aplicación tiene cinco segundos para responder a la invocación; de lo contrario, el usuario recibe un mensaje de error No se puede contactar con la aplicación y el cliente de Teams omite cualquier respuesta a la invocación.

Tiene las siguientes opciones para responder:

* Sin respuesta: puedes elegir usar la acción de envío para desencadenar un proceso en un sistema externo y no proporcionar comentarios al usuario. Esto puede ser útil para procesos de larga duración y puede optar por proporcionar comentarios de otra manera (por ejemplo, con un [mensaje proactivo).](~/bots/how-to/conversations/send-proactive-messages.md)
* [Otro módulo de](#respond-with-another-task-module) tareas: puede responder con un módulo de tarea adicional como parte de una interacción de varios pasos.
* [Respuesta de](#respond-with-a-card-inserted-into-the-compose-message-area) tarjeta: puede responder con una tarjeta con la que el usuario pueda interactuar o insertar en un mensaje.
* [Tarjeta adaptable desde el bot:](#bot-response-with-adaptive-card) inserta una tarjeta adaptable directamente en la conversación.
* [Solicitar la autenticación del usuario](~/messaging-extensions/how-to/add-authentication.md)
* [Solicitar al usuario que proporcione una configuración adicional](~/messaging-extensions/how-to/add-configuration-page.md)

Para la autenticación o configuración, una vez que el usuario completa el flujo, la invocación original se vuelve a enviar al servicio web. En la tabla siguiente se muestran los tipos de respuestas disponibles en función de la ubicación de invocación `commandContext` de la extensión de mensajería: 

|Tipo de respuesta | redacción | barra de comandos | mensaje |
|--------------|:-------------:|:-------------:|:---------:|
|Respuesta de tarjeta | x | x | x |
|Otro módulo de tareas | x | x | x |
|Bot con tarjeta adaptable | x |  | x |
| Sin respuesta | x | x | x |

## <a name="the-submitaction-invoke-event"></a>El evento de invocación submitAction

A continuación se muestran ejemplos de recepción del mensaje de invocación:

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

Este es un ejemplo del objeto JSON que recibe. El `commandContext` parámetro indica desde dónde se desencadenó la extensión de mensajería. El objeto contiene los campos del formulario como parámetros y los `data` valores que envió el usuario. El objeto JSON aquí se abrevia para resaltar los campos más relevantes.

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

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a>Responder con una tarjeta insertada en el área de redacción de mensajes

La forma más común de responder a la solicitud es con una `composeExtension/submitAction` tarjeta insertada en el área de redacción de mensajes. A continuación, el usuario puede elegir enviar la tarjeta a la conversación. Para obtener más información sobre el uso de [tarjetas,](~/task-modules-and-cards/cards/cards-actions.md)vea tarjetas y acciones de tarjetas.

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

Puede elegir responder al evento `submitAction` con un módulo de tarea adicional. Esto puede ser útil cuando:

* Debe recopilar grandes cantidades de información.
* Si necesita cambiar dinámicamente la información que recopila en función de la entrada del usuario
* Si necesita validar la información enviada por el usuario y enviar el formulario potencialmente con un mensaje de error si hay algún error. 

El método de respuesta es el mismo que [responder al evento `fetchTask` inicial.](~/messaging-extensions/how-to/action-commands/create-task-module.md) Si usa el SDK de Bot Framework, los mismos desencadenadores de eventos para ambas acciones de envío. Esto significa que debe agregar lógica que determine la respuesta correcta.

## <a name="bot-response-with-adaptive-card"></a>Respuesta de bot con tarjeta adaptable

>[!Note]
>Este flujo requiere que agregue el objeto al manifiesto de la aplicación y que tenga definido el ámbito necesario `bot` para el bot. Use el mismo identificador que la extensión de mensajería para el bot.

También puedes responder a la acción de envío insertando un mensaje con una tarjeta adaptable en el canal con un bot. El usuario puede obtener una vista previa del mensaje antes de enviarlo y, potencialmente, editarlo o interactuar con él también. Esto puede ser muy útil en escenarios en los que recopilas información de los usuarios antes de crear una respuesta de tarjeta adaptable o cuando actualizas la tarjeta después de que alguien interactúe con ella. El siguiente escenario muestra cómo la aplicación Polly usa este flujo para configurar un sondeo sin incluir los pasos de configuración en la conversación de canal:

1. El usuario selecciona la extensión de mensajería para desencadenar el módulo de tareas.
2. El usuario configura el sondeo con el módulo de tareas.
3. Después de enviar el módulo de tareas, la aplicación usa la información proporcionada para crear el sondeo como una tarjeta adaptable y lo envía como respuesta `botMessagePreview` al cliente.
4. A continuación, el usuario puede obtener una vista previa del mensaje de tarjeta adaptable antes de que el bot lo inserte en el canal. Si la aplicación aún no es miembro del canal, al seleccionarla `Send` se agrega.
   1. El usuario también puede elegir el `Edit` mensaje, que los devuelve al módulo de tareas original.
5. Interactuar con la tarjeta adaptable cambia el mensaje antes de enviarlo.
6. Una vez que el usuario selecciona `Send` el bot, publica el mensaje en el canal.

### <a name="respond-to-initial-submit-action"></a>Responder a la acción de envío inicial

Para habilitar este flujo, el módulo de tareas debe responder al mensaje inicial con una vista previa de la tarjeta que el `composeExtension/submitAction` bot envía al canal. Esto ofrece al usuario la oportunidad de comprobar la tarjeta antes de enviarla e intentar instalar el bot en la conversación si aún no está instalado.

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

>[!Note]
>Debe contener una actividad con exactamente 1 archivo `activityPreview` adjunto de tarjeta `message` adaptable. El `<< Card Payload >>` valor es un marcador de posición para la tarjeta que desea enviar.

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

### <a name="the-botmessagepreview-send-and-edit-events"></a>El botMessagePreview envía y edita eventos

La extensión del mensaje debe responder ahora a dos nuevas variedades de la `composeExtension/submitAction` invocación, donde `value.botMessagePreviewAction = "send"` y `value.botMessagePreviewAction = "edit"` .

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

Si el usuario edita la tarjeta antes de enviarla seleccionando el botón **Editar,** recibirá una `composeExtension/submitAction` invocación con `value.botMessagePreviewAction = edit` . Normalmente debe responder devolviendo el módulo de tareas que envió en respuesta a la invocación inicial `composeExtension/fetchTask` que inició la interacción. Esto permite al usuario iniciar el proceso de nuevo al volver a escribir la información original. Use la información disponible para rellenar previamente el módulo de tareas para que el usuario no tenga que rellenar toda la información desde cero.

Vea [responder al evento `fetchTask` inicial.](~/messaging-extensions/how-to/action-commands/create-task-module.md)

### <a name="respond-to-botmessagepreview-send"></a>Responder al envío botMessagePreview

Después de que el usuario seleccione el **botón Enviar,** recibirá una `composeExtension/submitAction` invocación con `value.botMessagePreviewAction = send` . El servicio web tiene que crear y enviar un mensaje proactivo con la tarjeta adaptable a la conversación y responder también a la invocación.

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

En escenarios en los que un bot envía mensajes en nombre de un usuario, la atribución del mensaje a ese usuario puede ayudar con la interacción y presentar un flujo de interacción más natural. Esta característica le permite atribuir un mensaje del bot a un usuario en cuyo nombre se envió.

En la siguiente imagen, a la izquierda hay un mensaje de tarjeta enviado por un *bot* sin atribución del usuario y, a la derecha, hay una tarjeta enviada por un *bot* con atribución de usuario.

![Captura de pantalla](../../../assets/images/messaging-extension/user-attribution-bots.png)

Para usar la atribución de usuarios en teams, debe agregar la entidad de mención a la carga que `OnBehalfOf` `ChannelData` se envía a `Activity` Teams.

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

La siguiente sección es una descripción de las entidades de la `OnBehalfOf` matriz:

#### <a name="details-of--onbehalfof-entity-schema"></a>Detalles del esquema  `OnBehalfOf` de entidad

|Field|Tipo|Descripción|
|:---|:---|:---|
|`itemId`|Entero|Debe ser 0|
|`mentionType`|Cadena|Debe ser "persona"|
|`mri`|Cadena|Identificador de recursos de mensaje (MRI) de la persona en cuyo nombre se envía el mensaje. El nombre del remitente del mensaje aparecería como " \<user\> a través \<bot name\> de ".|
|`displayName`|Cadena|Nombre de la persona. Se usa como reserva en caso de que la resolución de nombres no esté disponible.|
  
## <a name="next-steps"></a>Siguientes pasos

Agregar un comando de búsqueda

* [Definición de comandos de búsqueda](~/messaging-extensions/how-to/search-commands/define-search-command.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]

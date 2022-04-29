---
title: Responder a la acción de envío del módulo de tareas
author: surbhigupta
description: Describe cómo responder a la acción de envío del módulo de tareas desde un comando de acción de extensión de mensajería con mensaje proactivo, otro módulo de tareas, bot de tarjeta adaptable y mucho más mediante ejemplos de código.
ms.localizationpriority: high
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: dfd8b04c07c60231ed5dfdae4cc5acac2346fe2c
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111496"
---
# <a name="respond-to-the-task-module-submit-action"></a>Responder a la acción de envío del módulo de tareas

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Este documento le guía sobre cómo responde la aplicación a los comandos de acción, como la acción de envío del módulo de tareas del usuario.
Una vez que un usuario envía el módulo de tareas, el servicio web recibe un mensaje de invocación `composeExtension/submitAction` con el identificador de comando y los valores de parámetro. La aplicación tiene cinco segundos para responder a la invocación; de lo contrario, el usuario recibe un mensaje de error **No se puede acceder a la aplicación** y el cliente Teams omite cualquier respuesta que se va a invocar.

Tiene las siguientes opciones:

* Sin respuesta: use la acción enviar para desencadenar un proceso en un sistema externo y no proporcionar comentarios al usuario. Resulta útil para los procesos de larga duración y para proporcionar comentarios de forma alternativa. Por ejemplo, puede enviar comentarios con un [mensaje proactivo](~/bots/how-to/conversations/send-proactive-messages.md).
* [Otro módulo de tarea](#respond-with-another-task-module): puede responder con otro módulo de tarea como parte de una interacción de varios pasos.
* [Responder con tarjetas](#respond-with-a-card-inserted-into-the-compose-message-area): responder con una tarjeta con la que el usuario pueda interactuar o que el usuario pueda insertar en un mensaje.
* [Tarjeta adaptable del bot](#bot-response-with-adaptive-card): inserte una tarjeta adaptable directamente en la conversación.
* [Solicite al usuario que se autentique](~/messaging-extensions/how-to/add-authentication.md).
* [Solicite al usuario que proporcione una configuración adicional](~/get-started/first-message-extension.md).

Para la autenticación o configuración, una vez que el usuario completa el proceso, la invocación original se resiente para el servicio web. En la tabla siguiente se muestra qué tipos de respuestas están disponibles en función de la ubicación `commandContext` de invocación de la extensión de mensaje:

|Tipo de respuesta | Redacción | Barra de comandos | Message |
|--------------|:-------------:|:-------------:|:---------:|
|Respuesta de tarjeta | ✔ | ✔ | ✔ |
|Otro módulo de tareas | ✔ | ✔ | ✔ |
|Bot con tarjeta adaptable | ✔ | x | ✔ |
| Sin respuesta | ✔ | ✔ | ✔ |

> [!NOTE]
>
> * Al seleccionar **Action.Submit** a través de tarjetas ME, envía la actividad de invocación con el nombre **composeExtension**, donde el valor es igual a la carga habitual.
> * Al seleccionar **Action.Submit** a través de la conversación, recibirá la actividad del mensaje con el nombre **onCardButtonClicked**, donde el valor es igual a la carga habitual.

Si la aplicación contiene un bot conversacional, instale el bot en la conversación y, a continuación, cargue el módulo de tareas. El bot es útil para obtener contexto adicional para el módulo de tareas. Para instalar el bot conversacional, consulte [Solicitud para instalar el bot conversacional](create-task-module.md#request-to-install-your-conversational-bot).

## <a name="the-submitaction-invoke-event"></a>Evento de invocación submitAction

Los ejemplos de recepción del mensaje de invocación son los siguientes:

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

Este es un ejemplo del objeto JSON que recibe. El parámetro `commandContext` indica desde dónde se desencadenó la extensión de mensaje. El objeto `data` contiene los campos del formulario como parámetros y los valores que envió el usuario. El objeto JSON resalta los campos más relevantes.

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

La manera más común de responder a la solicitud `composeExtension/submitAction` es con una tarjeta insertada en el área del mensaje de redacción. El usuario envía la tarjeta a la conversación. Para obtener más información sobre el uso de tarjetas, consulte [tarjetas y acciones de tarjetas](~/task-modules-and-cards/cards/cards-actions.md).

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

Puede seleccionar responder al evento `submitAction` con un módulo de tareas adicional. Esto resulta útil cuando necesita:

* Recopilar grandes cantidades de información.
* Cambiar dinámicamente la recopilación de información en función de la entrada del usuario.
* Validar la información enviada por el usuario y volver a enviar el formulario con un mensaje de error si hay algún error.

El método de respuesta es el mismo que [responder al evento inicial`fetchTask`](~/messaging-extensions/how-to/action-commands/create-task-module.md). Si usa el SDK de Bot Framework, los mismos desencadenadores de eventos para ambas acciones de envío. Para que esto funcione, debe agregar la lógica que determine la respuesta correcta.

## <a name="bot-response-with-adaptive-card"></a>Respuesta del bot con tarjeta adaptable

> [!NOTE]
> El requisito previo para obtener la respuesta del bot con una tarjeta adaptable es que debe agregar el objeto `bot` al manifiesto de la aplicación y definir el ámbito necesario para el bot. Use el mismo identificador que la extensión de mensaje para el bot.

También puede responder a `submitAction` mediante la inserción de un mensaje con una tarjeta adaptable en el canal con un bot. El usuario puede obtener una vista previa del mensaje antes de enviarlo. Esto resulta útil en escenarios en los que se recopila información de los usuarios antes de crear una respuesta de tarjeta adaptable o cuando se actualiza la tarjeta después de que alguien interactúe con ella.

En el siguiente escenario se muestra cómo la aplicación Polly configura un sondeo sin incluir los pasos de configuración en la conversación del canal:

Para configurar el sondeo:

1. El usuario selecciona la extensión de mensaje para invocar el módulo de tareas.
1. El usuario configura el sondeo con el módulo de tareas.
1. Después de enviar el módulo de tareas, la aplicación usa la información proporcionada para compilar el sondeo como una tarjeta adaptable y la envía como respuesta `botMessagePreview` al cliente.
1. A continuación, el usuario puede obtener una vista previa del mensaje de tarjeta adaptable antes de que el bot lo inserte en el canal. Si la aplicación no es miembro del canal, seleccione `Send` para agregarla.

    > [!NOTE]
    >
    > * Los usuarios también pueden seleccionar `Edit` en el mensaje, que los devuelve al módulo de tareas original.
    > * La interacción con la tarjeta adaptable cambia el mensaje antes de enviarlo.
    >
1. Una vez que el usuario selecciona `Send`, el bot publica el mensaje en el canal.

## <a name="respond-to-initial-submit-action"></a>Respuesta a la acción de envío inicial

El módulo de tareas debe responder al mensaje inicial `composeExtension/submitAction` con una vista previa de la tarjeta que el bot envía al canal. El usuario puede comprobar la tarjeta antes del envío e intentar instalar el bot en la conversación si el bot aún no está instalado.

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
>
> * `activityPreview` debe contener una actividad `message` con exactamente un archivo adjunto de tarjeta adaptable. El valor `<< Card Payload >>` es un marcador de posición para la tarjeta que desea enviar.

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

### <a name="the-botmessagepreview-send-and-edit-events"></a>BotMessagePreview envía y edita eventos

La extensión de mensaje debe responder a dos tipos nuevos de la invocación `composeExtension/submitAction`, donde `value.botMessagePreviewAction = "send"` y `value.botMessagePreviewAction = "edit"`.

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

Si el usuario edita la tarjeta antes de enviarla, al seleccionar **Editar**, recibirá una `composeExtension/submitAction` invocación con `value.botMessagePreviewAction = edit`. Responda devolviendo el módulo de tareas que envió, en respuesta a la invocación inicial `composeExtension/fetchTask` que inició la interacción. Esto permite al usuario iniciar el proceso volviendo a escribir la información original. Use la información disponible para actualizar el módulo de tareas de modo que el usuario no necesite rellenar toda la información desde cero.
Para obtener más información sobre cómo responder al evento inicial `fetchTask`, consulte [Responder al evento inicial`fetchTask`](~/messaging-extensions/how-to/action-commands/create-task-module.md).

### <a name="respond-to-botmessagepreview-send"></a>Respuesta al envío de botMessagePreview

Después de que el usuario seleccione **Enviar**, recibirá una `composeExtension/submitAction` invocación con `value.botMessagePreviewAction = send`. El servicio web debe crear y enviar un mensaje proactivo con la tarjeta adaptable a la conversación y también responder a la invocación.

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

En escenarios en los que un bot envía mensajes en nombre de un usuario, atribuir el mensaje a ese usuario ayuda con la interacción y muestra un flujo de interacción más natural. Esta característica le permite atribuir un mensaje del bot a un usuario en cuyo nombre se envió.

En la imagen siguiente, a la izquierda hay un mensaje de tarjeta enviado por un bot sin atribución de usuario y a la derecha una tarjeta enviada por un bot con atribución de usuario.

![bots de atribución de usuarios](../../../assets/images/messaging-extension/user-attribution-bots.png)

Para usar la atribución de usuario en Teams, debe agregar la `OnBehalfOf` entidad de mención a `ChannelData` en `Activity` la carga que se envía a Teams.

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

#### <a name="details-of--onbehalfof-entity-schema"></a>Detalles del esquema de  `OnBehalfOf` entidad

La sección siguiente es una descripción de las entidades de la matriz `OnBehalfOf`:

|Field|Tipo|Descripción|
|:---|:---|:---|
|`itemId`|Entero|Describe la identificación del elemento. Su valor debe ser `0`.|
|`mentionType`|Cadena|Describe la mención de una “persona”.|
|`mri`|Cadena|Identificador de recurso de mensaje (MRI) de la persona en cuyo nombre se envía el mensaje. El nombre del remitente del mensaje aparecería como”"\<user\> a \<bot name\>“.|
|`displayName`|Cadena|Nombre de la persona que publicó el flujo de trabajo. Se usa como reserva en la resolución de nombres de caso no está disponible.|
  
## <a name="code-sample"></a>Ejemplo de código

| Ejemplo de nombre           | Descripción | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Acción de extensión de mensaje de Teams| Describe cómo definir comandos de acción, crear un módulo de tareas y responder a la acción de envío del módulo de tareas. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) |
|Búsqueda de extensión de mensaje de Teams   |  Describe cómo definir comandos de búsqueda y responder a búsquedas.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Definición de comandos de búsqueda](~/messaging-extensions/how-to/search-commands/define-search-command.md)

## <a name="see-also"></a>Consulte también

[Responder a consultas de comandos de búsqueda](~/messaging-extensions/how-to/search-commands/respond-to-search.md)

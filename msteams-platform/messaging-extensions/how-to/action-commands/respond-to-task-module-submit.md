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
# <a name="respond-to-the-task-module-submit-action"></a><span data-ttu-id="ca17d-103">Responder a la acción de envío del módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="ca17d-103">Respond to the task module submit action</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="ca17d-104">Una vez que un usuario envía el módulo de tarea, el servicio web recibe un mensaje de invocación con los valores de identificador de comando `composeExtension/submitAction` y parámetros.</span><span class="sxs-lookup"><span data-stu-id="ca17d-104">After a user submits the task module, your web service receives a `composeExtension/submitAction` invoke message with the command ID and parameter values.</span></span> <span data-ttu-id="ca17d-105">La aplicación tiene cinco segundos para responder a la invocación; de lo contrario, el usuario recibe un mensaje de error No se puede contactar con la aplicación y el cliente de Teams omite cualquier respuesta a la invocación.</span><span class="sxs-lookup"><span data-stu-id="ca17d-105">Your app has five seconds to respond to the invoke, otherwise the user receives an error message *Unable to reach the app*, and any reply to the invoke is ignored by the Teams client.</span></span>

<span data-ttu-id="ca17d-106">Tiene las siguientes opciones para responder:</span><span class="sxs-lookup"><span data-stu-id="ca17d-106">You have the following options for responding:</span></span>

* <span data-ttu-id="ca17d-107">Sin respuesta: puedes elegir usar la acción de envío para desencadenar un proceso en un sistema externo y no proporcionar comentarios al usuario.</span><span class="sxs-lookup"><span data-stu-id="ca17d-107">No response - You can choose to use the submit action to trigger a process in an external system, and not provide any feedback to the user.</span></span> <span data-ttu-id="ca17d-108">Esto puede ser útil para procesos de larga duración y puede optar por proporcionar comentarios de otra manera (por ejemplo, con un [mensaje proactivo).](~/bots/how-to/conversations/send-proactive-messages.md)</span><span class="sxs-lookup"><span data-stu-id="ca17d-108">This can be useful for long-running processes, and you may choose to provide feedback in another manner (for example, with a [proactive message](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>
* <span data-ttu-id="ca17d-109">[Otro módulo de](#respond-with-another-task-module) tareas: puede responder con un módulo de tarea adicional como parte de una interacción de varios pasos.</span><span class="sxs-lookup"><span data-stu-id="ca17d-109">[Another task module](#respond-with-another-task-module) - You can respond with an additional task module as part of a multi-step interaction.</span></span>
* <span data-ttu-id="ca17d-110">[Respuesta de](#respond-with-a-card-inserted-into-the-compose-message-area) tarjeta: puede responder con una tarjeta con la que el usuario pueda interactuar o insertar en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="ca17d-110">[Card response](#respond-with-a-card-inserted-into-the-compose-message-area) - You can respond with a card that the user can then interact with and/or insert into a message.</span></span>
* <span data-ttu-id="ca17d-111">[Tarjeta adaptable desde el bot:](#bot-response-with-adaptive-card) inserta una tarjeta adaptable directamente en la conversación.</span><span class="sxs-lookup"><span data-stu-id="ca17d-111">[Adaptive Card from bot](#bot-response-with-adaptive-card) - Insert an Adaptive Card directly into the conversation.</span></span>
* [<span data-ttu-id="ca17d-112">Solicitar la autenticación del usuario</span><span class="sxs-lookup"><span data-stu-id="ca17d-112">Request the user authenticate</span></span>](~/messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="ca17d-113">Solicitar al usuario que proporcione una configuración adicional</span><span class="sxs-lookup"><span data-stu-id="ca17d-113">Request the user provide additional configuration</span></span>](~/messaging-extensions/how-to/add-configuration-page.md)

<span data-ttu-id="ca17d-114">Para la autenticación o configuración, una vez que el usuario completa el flujo, la invocación original se vuelve a enviar al servicio web.</span><span class="sxs-lookup"><span data-stu-id="ca17d-114">For authentication or configuration, after the user completes the flow the original invoke is re-sent to your web service.</span></span> <span data-ttu-id="ca17d-115">En la tabla siguiente se muestran los tipos de respuestas disponibles en función de la ubicación de invocación `commandContext` de la extensión de mensajería:</span><span class="sxs-lookup"><span data-stu-id="ca17d-115">The following table shows which types of responses are available based on the invoke location `commandContext` of the messaging extension:</span></span> 

|<span data-ttu-id="ca17d-116">Tipo de respuesta</span><span class="sxs-lookup"><span data-stu-id="ca17d-116">Response Type</span></span> | <span data-ttu-id="ca17d-117">redacción</span><span class="sxs-lookup"><span data-stu-id="ca17d-117">compose</span></span> | <span data-ttu-id="ca17d-118">barra de comandos</span><span class="sxs-lookup"><span data-stu-id="ca17d-118">command bar</span></span> | <span data-ttu-id="ca17d-119">mensaje</span><span class="sxs-lookup"><span data-stu-id="ca17d-119">message</span></span> |
|--------------|:-------------:|:-------------:|:---------:|
|<span data-ttu-id="ca17d-120">Respuesta de tarjeta</span><span class="sxs-lookup"><span data-stu-id="ca17d-120">Card response</span></span> | <span data-ttu-id="ca17d-121">x</span><span class="sxs-lookup"><span data-stu-id="ca17d-121">x</span></span> | <span data-ttu-id="ca17d-122">x</span><span class="sxs-lookup"><span data-stu-id="ca17d-122">x</span></span> | <span data-ttu-id="ca17d-123">x</span><span class="sxs-lookup"><span data-stu-id="ca17d-123">x</span></span> |
|<span data-ttu-id="ca17d-124">Otro módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="ca17d-124">Another task module</span></span> | <span data-ttu-id="ca17d-125">x</span><span class="sxs-lookup"><span data-stu-id="ca17d-125">x</span></span> | <span data-ttu-id="ca17d-126">x</span><span class="sxs-lookup"><span data-stu-id="ca17d-126">x</span></span> | <span data-ttu-id="ca17d-127">x</span><span class="sxs-lookup"><span data-stu-id="ca17d-127">x</span></span> |
|<span data-ttu-id="ca17d-128">Bot con tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="ca17d-128">Bot with Adaptive Card</span></span> | <span data-ttu-id="ca17d-129">x</span><span class="sxs-lookup"><span data-stu-id="ca17d-129">x</span></span> |  | <span data-ttu-id="ca17d-130">x</span><span class="sxs-lookup"><span data-stu-id="ca17d-130">x</span></span> |
| <span data-ttu-id="ca17d-131">Sin respuesta</span><span class="sxs-lookup"><span data-stu-id="ca17d-131">No response</span></span> | <span data-ttu-id="ca17d-132">x</span><span class="sxs-lookup"><span data-stu-id="ca17d-132">x</span></span> | <span data-ttu-id="ca17d-133">x</span><span class="sxs-lookup"><span data-stu-id="ca17d-133">x</span></span> | <span data-ttu-id="ca17d-134">x</span><span class="sxs-lookup"><span data-stu-id="ca17d-134">x</span></span> |

## <a name="the-submitaction-invoke-event"></a><span data-ttu-id="ca17d-135">El evento de invocación submitAction</span><span class="sxs-lookup"><span data-stu-id="ca17d-135">The submitAction invoke event</span></span>

<span data-ttu-id="ca17d-136">A continuación se muestran ejemplos de recepción del mensaje de invocación:</span><span class="sxs-lookup"><span data-stu-id="ca17d-136">Examples of receiving the invoke message are as follows:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="ca17d-137">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="ca17d-137">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="ca17d-138">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="ca17d-138">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  constructor() {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
  
  //code to handle the submit action
    }
  }
}
```

# <a name="json"></a>[<span data-ttu-id="ca17d-139">JSON</span><span class="sxs-lookup"><span data-stu-id="ca17d-139">JSON</span></span>](#tab/json)

<span data-ttu-id="ca17d-140">Este es un ejemplo del objeto JSON que recibe.</span><span class="sxs-lookup"><span data-stu-id="ca17d-140">This is an example of the JSON object you receive.</span></span> <span data-ttu-id="ca17d-141">El `commandContext` parámetro indica desde dónde se desencadenó la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="ca17d-141">The `commandContext` parameter indicates where your messaging extension was triggered from.</span></span> <span data-ttu-id="ca17d-142">El objeto contiene los campos del formulario como parámetros y los `data` valores que envió el usuario.</span><span class="sxs-lookup"><span data-stu-id="ca17d-142">The `data` object contains the fields on the form as parameters, and the values the user submitted.</span></span> <span data-ttu-id="ca17d-143">El objeto JSON aquí se abrevia para resaltar los campos más relevantes.</span><span class="sxs-lookup"><span data-stu-id="ca17d-143">The JSON object here is shortened to highlight the most relevant fields.</span></span>

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

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a><span data-ttu-id="ca17d-144">Responder con una tarjeta insertada en el área de redacción de mensajes</span><span class="sxs-lookup"><span data-stu-id="ca17d-144">Respond with a card inserted into the compose message area</span></span>

<span data-ttu-id="ca17d-145">La forma más común de responder a la solicitud es con una `composeExtension/submitAction` tarjeta insertada en el área de redacción de mensajes.</span><span class="sxs-lookup"><span data-stu-id="ca17d-145">The most common way to respond to the `composeExtension/submitAction` request is with a card inserted into the compose message area.</span></span> <span data-ttu-id="ca17d-146">A continuación, el usuario puede elegir enviar la tarjeta a la conversación.</span><span class="sxs-lookup"><span data-stu-id="ca17d-146">The user can then choose to submit the card to the conversation.</span></span> <span data-ttu-id="ca17d-147">Para obtener más información sobre el uso de [tarjetas,](~/task-modules-and-cards/cards/cards-actions.md)vea tarjetas y acciones de tarjetas.</span><span class="sxs-lookup"><span data-stu-id="ca17d-147">For more information on using cards see [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="ca17d-148">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="ca17d-148">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="ca17d-149">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="ca17d-149">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="ca17d-150">JSON</span><span class="sxs-lookup"><span data-stu-id="ca17d-150">JSON</span></span>](#tab/json)

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

## <a name="respond-with-another-task-module"></a><span data-ttu-id="ca17d-151">Responder con otro módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="ca17d-151">Respond with another task module</span></span>

<span data-ttu-id="ca17d-152">Puede elegir responder al evento `submitAction` con un módulo de tarea adicional.</span><span class="sxs-lookup"><span data-stu-id="ca17d-152">You can choose to respond to the `submitAction` event with an additional task module.</span></span> <span data-ttu-id="ca17d-153">Esto puede ser útil cuando:</span><span class="sxs-lookup"><span data-stu-id="ca17d-153">This can be useful when:</span></span>

* <span data-ttu-id="ca17d-154">Debe recopilar grandes cantidades de información.</span><span class="sxs-lookup"><span data-stu-id="ca17d-154">You need to collect large amounts of information.</span></span>
* <span data-ttu-id="ca17d-155">Si necesita cambiar dinámicamente la información que recopila en función de la entrada del usuario</span><span class="sxs-lookup"><span data-stu-id="ca17d-155">If you need to dynamically change what information you are collecting based on user input</span></span>
* <span data-ttu-id="ca17d-156">Si necesita validar la información enviada por el usuario y enviar el formulario potencialmente con un mensaje de error si hay algún error.</span><span class="sxs-lookup"><span data-stu-id="ca17d-156">If you need to validate the information submitted by the user and potentially resend the form with an error message if something is wrong.</span></span> 

<span data-ttu-id="ca17d-157">El método de respuesta es el mismo que [responder al evento `fetchTask` inicial.](~/messaging-extensions/how-to/action-commands/create-task-module.md)</span><span class="sxs-lookup"><span data-stu-id="ca17d-157">The method for response is the same as [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span> <span data-ttu-id="ca17d-158">Si usa el SDK de Bot Framework, los mismos desencadenadores de eventos para ambas acciones de envío.</span><span class="sxs-lookup"><span data-stu-id="ca17d-158">If you are using the Bot Framework SDK the same event triggers for both submit actions.</span></span> <span data-ttu-id="ca17d-159">Esto significa que debe agregar lógica que determine la respuesta correcta.</span><span class="sxs-lookup"><span data-stu-id="ca17d-159">This means you must add logic which determines the correct response.</span></span>

## <a name="bot-response-with-adaptive-card"></a><span data-ttu-id="ca17d-160">Respuesta de bot con tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="ca17d-160">Bot response with Adaptive Card</span></span>

>[!Note]
><span data-ttu-id="ca17d-161">Este flujo requiere que agregue el objeto al manifiesto de la aplicación y que tenga definido el ámbito necesario `bot` para el bot.</span><span class="sxs-lookup"><span data-stu-id="ca17d-161">This flow requires that you add the `bot` object to your app manifest, and that you have the necessary scope defined for the bot.</span></span> <span data-ttu-id="ca17d-162">Use el mismo identificador que la extensión de mensajería para el bot.</span><span class="sxs-lookup"><span data-stu-id="ca17d-162">Use the same ID as your messaging extension for your bot.</span></span>

<span data-ttu-id="ca17d-163">También puedes responder a la acción de envío insertando un mensaje con una tarjeta adaptable en el canal con un bot.</span><span class="sxs-lookup"><span data-stu-id="ca17d-163">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="ca17d-164">El usuario puede obtener una vista previa del mensaje antes de enviarlo y, potencialmente, editarlo o interactuar con él también.</span><span class="sxs-lookup"><span data-stu-id="ca17d-164">Your user can preview the message before submitting it, and potentially edit or interact with it as well.</span></span> <span data-ttu-id="ca17d-165">Esto puede ser muy útil en escenarios en los que recopilas información de los usuarios antes de crear una respuesta de tarjeta adaptable o cuando actualizas la tarjeta después de que alguien interactúe con ella.</span><span class="sxs-lookup"><span data-stu-id="ca17d-165">This can be very useful in scenarios where you gather information from your users before creating an adaptive card response, or when you update the card after someone interacts with it.</span></span> <span data-ttu-id="ca17d-166">El siguiente escenario muestra cómo la aplicación Polly usa este flujo para configurar un sondeo sin incluir los pasos de configuración en la conversación de canal:</span><span class="sxs-lookup"><span data-stu-id="ca17d-166">The following scenario shows how the app Polly uses this flow to configure a poll without including the configuration steps in the channel conversation:</span></span>

1. <span data-ttu-id="ca17d-167">El usuario selecciona la extensión de mensajería para desencadenar el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="ca17d-167">The user selects the messaging extension to trigger the task module.</span></span>
2. <span data-ttu-id="ca17d-168">El usuario configura el sondeo con el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="ca17d-168">The user configures the poll with the task module.</span></span>
3. <span data-ttu-id="ca17d-169">Después de enviar el módulo de tareas, la aplicación usa la información proporcionada para crear el sondeo como una tarjeta adaptable y lo envía como respuesta `botMessagePreview` al cliente.</span><span class="sxs-lookup"><span data-stu-id="ca17d-169">After submitting the task module the app uses the information provided to build the poll as an Adaptive Card and sends it as a `botMessagePreview` response to the client.</span></span>
4. <span data-ttu-id="ca17d-170">A continuación, el usuario puede obtener una vista previa del mensaje de tarjeta adaptable antes de que el bot lo inserte en el canal.</span><span class="sxs-lookup"><span data-stu-id="ca17d-170">The user can then preview the adaptive card message before the bot inserts it into the channel.</span></span> <span data-ttu-id="ca17d-171">Si la aplicación aún no es miembro del canal, al seleccionarla `Send` se agrega.</span><span class="sxs-lookup"><span data-stu-id="ca17d-171">If the app is not already a member of the channel, selecting `Send` adds it.</span></span>
   1. <span data-ttu-id="ca17d-172">El usuario también puede elegir el `Edit` mensaje, que los devuelve al módulo de tareas original.</span><span class="sxs-lookup"><span data-stu-id="ca17d-172">The user can also choose to `Edit` the message, which returns them to the original task module.</span></span>
5. <span data-ttu-id="ca17d-173">Interactuar con la tarjeta adaptable cambia el mensaje antes de enviarlo.</span><span class="sxs-lookup"><span data-stu-id="ca17d-173">Interacting with the adaptive card changes the message before sending it.</span></span>
6. <span data-ttu-id="ca17d-174">Una vez que el usuario selecciona `Send` el bot, publica el mensaje en el canal.</span><span class="sxs-lookup"><span data-stu-id="ca17d-174">After the user selects `Send` the bot posts the message to the channel.</span></span>

### <a name="respond-to-initial-submit-action"></a><span data-ttu-id="ca17d-175">Responder a la acción de envío inicial</span><span class="sxs-lookup"><span data-stu-id="ca17d-175">Respond to initial submit action</span></span>

<span data-ttu-id="ca17d-176">Para habilitar este flujo, el módulo de tareas debe responder al mensaje inicial con una vista previa de la tarjeta que el `composeExtension/submitAction` bot envía al canal.</span><span class="sxs-lookup"><span data-stu-id="ca17d-176">To enable this flow your task module should respond to the initial `composeExtension/submitAction` message with a preview of the card that the bot send to the channel.</span></span> <span data-ttu-id="ca17d-177">Esto ofrece al usuario la oportunidad de comprobar la tarjeta antes de enviarla e intentar instalar el bot en la conversación si aún no está instalado.</span><span class="sxs-lookup"><span data-stu-id="ca17d-177">This gives the user the opportunity to verify the card before sending, and also attempt to install your bot in the conversation if it is not already installed.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="ca17d-178">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="ca17d-178">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="ca17d-179">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="ca17d-179">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="ca17d-180">JSON</span><span class="sxs-lookup"><span data-stu-id="ca17d-180">JSON</span></span>](#tab/json)

>[!Note]
><span data-ttu-id="ca17d-181">Debe contener una actividad con exactamente 1 archivo `activityPreview` adjunto de tarjeta `message` adaptable.</span><span class="sxs-lookup"><span data-stu-id="ca17d-181">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span> <span data-ttu-id="ca17d-182">El `<< Card Payload >>` valor es un marcador de posición para la tarjeta que desea enviar.</span><span class="sxs-lookup"><span data-stu-id="ca17d-182">The `<< Card Payload >>` value is a placeholder for the card you wish to send.</span></span>

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

### <a name="the-botmessagepreview-send-and-edit-events"></a><span data-ttu-id="ca17d-183">El botMessagePreview envía y edita eventos</span><span class="sxs-lookup"><span data-stu-id="ca17d-183">The botMessagePreview send and edit events</span></span>

<span data-ttu-id="ca17d-184">La extensión del mensaje debe responder ahora a dos nuevas variedades de la `composeExtension/submitAction` invocación, donde `value.botMessagePreviewAction = "send"` y `value.botMessagePreviewAction = "edit"` .</span><span class="sxs-lookup"><span data-stu-id="ca17d-184">Your message extension must respond now to two new varieties of the `composeExtension/submitAction` invoke, where `value.botMessagePreviewAction = "send"`and `value.botMessagePreviewAction = "edit"`.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="ca17d-185">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="ca17d-185">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="ca17d-186">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="ca17d-186">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="ca17d-187">JSON</span><span class="sxs-lookup"><span data-stu-id="ca17d-187">JSON</span></span>](#tab/json)

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

### <a name="respond-to-botmessagepreview-edit"></a><span data-ttu-id="ca17d-188">Responder a la edición botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="ca17d-188">Respond to botMessagePreview edit</span></span>

<span data-ttu-id="ca17d-189">Si el usuario edita la tarjeta antes de enviarla seleccionando el botón **Editar,** recibirá una `composeExtension/submitAction` invocación con `value.botMessagePreviewAction = edit` .</span><span class="sxs-lookup"><span data-stu-id="ca17d-189">If the user edits the card before sending by selecting the **Edit** button, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = edit`.</span></span> <span data-ttu-id="ca17d-190">Normalmente debe responder devolviendo el módulo de tareas que envió en respuesta a la invocación inicial `composeExtension/fetchTask` que inició la interacción.</span><span class="sxs-lookup"><span data-stu-id="ca17d-190">You should typically respond by returning the task module you sent in response to the initial `composeExtension/fetchTask` invoke that began the interaction.</span></span> <span data-ttu-id="ca17d-191">Esto permite al usuario iniciar el proceso de nuevo al volver a escribir la información original.</span><span class="sxs-lookup"><span data-stu-id="ca17d-191">This allows the user to start the process over by re-entering the original information.</span></span> <span data-ttu-id="ca17d-192">Use la información disponible para rellenar previamente el módulo de tareas para que el usuario no tenga que rellenar toda la información desde cero.</span><span class="sxs-lookup"><span data-stu-id="ca17d-192">Use the available information to pre-populate the task module so the user does not have to fill out all of the information from scratch.</span></span>

<span data-ttu-id="ca17d-193">Vea [responder al evento `fetchTask` inicial.](~/messaging-extensions/how-to/action-commands/create-task-module.md)</span><span class="sxs-lookup"><span data-stu-id="ca17d-193">See [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span>

### <a name="respond-to-botmessagepreview-send"></a><span data-ttu-id="ca17d-194">Responder al envío botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="ca17d-194">Respond to botMessagePreview send</span></span>

<span data-ttu-id="ca17d-195">Después de que el usuario seleccione el **botón Enviar,** recibirá una `composeExtension/submitAction` invocación con `value.botMessagePreviewAction = send` .</span><span class="sxs-lookup"><span data-stu-id="ca17d-195">After the user selects the **Send** button, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = send`.</span></span> <span data-ttu-id="ca17d-196">El servicio web tiene que crear y enviar un mensaje proactivo con la tarjeta adaptable a la conversación y responder también a la invocación.</span><span class="sxs-lookup"><span data-stu-id="ca17d-196">Your web service has to create and send a proactive message with the Adaptive Card to the conversation, and also reply to the invoke.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="ca17d-197">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="ca17d-197">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="ca17d-198">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="ca17d-198">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="ca17d-199">JSON</span><span class="sxs-lookup"><span data-stu-id="ca17d-199">JSON</span></span>](#tab/json)

<span data-ttu-id="ca17d-200">Recibirá un nuevo `composeExtension/submitAction` mensaje similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="ca17d-200">You receive a new `composeExtension/submitAction` message similar to the following:</span></span>

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

### <a name="user-attribution-for-bots-messages"></a><span data-ttu-id="ca17d-201">Atribución de usuarios para mensajes de bots</span><span class="sxs-lookup"><span data-stu-id="ca17d-201">User attribution for bots messages</span></span> 

<span data-ttu-id="ca17d-202">En escenarios en los que un bot envía mensajes en nombre de un usuario, la atribución del mensaje a ese usuario puede ayudar con la interacción y presentar un flujo de interacción más natural.</span><span class="sxs-lookup"><span data-stu-id="ca17d-202">In scenarios where a bot sends messages on behalf of a user, attributing the message to that user can help with engagement and showcase a more natural interaction flow.</span></span> <span data-ttu-id="ca17d-203">Esta característica le permite atribuir un mensaje del bot a un usuario en cuyo nombre se envió.</span><span class="sxs-lookup"><span data-stu-id="ca17d-203">This feature allows you to attribute a message from your bot to a user on whose behalf it was sent.</span></span>

<span data-ttu-id="ca17d-204">En la siguiente imagen, a la izquierda hay un mensaje de tarjeta enviado por un *bot* sin atribución del usuario y, a la derecha, hay una tarjeta enviada por un *bot* con atribución de usuario.</span><span class="sxs-lookup"><span data-stu-id="ca17d-204">In the following image, on the left is a card message sent by a bot *without* user attribution and on the right is a card sent by a bot *with* user attribution.</span></span>

![Captura de pantalla](../../../assets/images/messaging-extension/user-attribution-bots.png)

<span data-ttu-id="ca17d-206">Para usar la atribución de usuarios en teams, debe agregar la entidad de mención a la carga que `OnBehalfOf` `ChannelData` se envía a `Activity` Teams.</span><span class="sxs-lookup"><span data-stu-id="ca17d-206">To use the user attribution in teams, you must  add the `OnBehalfOf` mention entity to `ChannelData` in your `Activity` payload that is sent to Teams.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="ca17d-207">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="ca17d-207">C#/.NET</span></span>](#tab/dotnet-1)

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

# <a name="json"></a>[<span data-ttu-id="ca17d-208">JSON</span><span class="sxs-lookup"><span data-stu-id="ca17d-208">JSON</span></span>](#tab/json-1)

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

<span data-ttu-id="ca17d-209">La siguiente sección es una descripción de las entidades de la `OnBehalfOf` matriz:</span><span class="sxs-lookup"><span data-stu-id="ca17d-209">The following section is a description of the entities in the `OnBehalfOf` of Array:</span></span>

#### <a name="details-of--onbehalfof-entity-schema"></a><span data-ttu-id="ca17d-210">Detalles del esquema  `OnBehalfOf` de entidad</span><span class="sxs-lookup"><span data-stu-id="ca17d-210">Details of  `OnBehalfOf` entity schema</span></span>

|<span data-ttu-id="ca17d-211">Field</span><span class="sxs-lookup"><span data-stu-id="ca17d-211">Field</span></span>|<span data-ttu-id="ca17d-212">Tipo</span><span class="sxs-lookup"><span data-stu-id="ca17d-212">Type</span></span>|<span data-ttu-id="ca17d-213">Descripción</span><span class="sxs-lookup"><span data-stu-id="ca17d-213">Description</span></span>|
|:---|:---|:---|
|`itemId`|<span data-ttu-id="ca17d-214">Entero</span><span class="sxs-lookup"><span data-stu-id="ca17d-214">Integer</span></span>|<span data-ttu-id="ca17d-215">Debe ser 0</span><span class="sxs-lookup"><span data-stu-id="ca17d-215">Should be 0</span></span>|
|`mentionType`|<span data-ttu-id="ca17d-216">Cadena</span><span class="sxs-lookup"><span data-stu-id="ca17d-216">String</span></span>|<span data-ttu-id="ca17d-217">Debe ser "persona"</span><span class="sxs-lookup"><span data-stu-id="ca17d-217">Should be "person"</span></span>|
|`mri`|<span data-ttu-id="ca17d-218">Cadena</span><span class="sxs-lookup"><span data-stu-id="ca17d-218">String</span></span>|<span data-ttu-id="ca17d-219">Identificador de recursos de mensaje (MRI) de la persona en cuyo nombre se envía el mensaje.</span><span class="sxs-lookup"><span data-stu-id="ca17d-219">Message resource identifier (MRI) of the person on whose behalf the message is sent.</span></span> <span data-ttu-id="ca17d-220">El nombre del remitente del mensaje aparecería como " \<user\> a través \<bot name\> de ".</span><span class="sxs-lookup"><span data-stu-id="ca17d-220">Message sender name would appear as "\<user\> via \<bot name\>".</span></span>|
|`displayName`|<span data-ttu-id="ca17d-221">Cadena</span><span class="sxs-lookup"><span data-stu-id="ca17d-221">String</span></span>|<span data-ttu-id="ca17d-222">Nombre de la persona.</span><span class="sxs-lookup"><span data-stu-id="ca17d-222">Name of the person.</span></span> <span data-ttu-id="ca17d-223">Se usa como reserva en caso de que la resolución de nombres no esté disponible.</span><span class="sxs-lookup"><span data-stu-id="ca17d-223">Used as fallback in case name resolution is unavailable.</span></span>|
  
## <a name="next-steps"></a><span data-ttu-id="ca17d-224">Siguientes pasos</span><span class="sxs-lookup"><span data-stu-id="ca17d-224">Next Steps</span></span>

<span data-ttu-id="ca17d-225">Agregar un comando de búsqueda</span><span class="sxs-lookup"><span data-stu-id="ca17d-225">Add a search command</span></span>

* [<span data-ttu-id="ca17d-226">Definición de comandos de búsqueda</span><span class="sxs-lookup"><span data-stu-id="ca17d-226">Define search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]

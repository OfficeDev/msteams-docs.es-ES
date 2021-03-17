---
title: Responder a la acción de envío del módulo de tareas
author: clearab
description: Describe cómo responder a la acción de envío del módulo de tareas desde un comando de acción de extensión de mensajería
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: fecc0ace5f767da3764529a9e8a590b37e547bb0
ms.sourcegitcommit: 1ce74ed167bb81bf09f7f6f8d518093efafb549e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/16/2021
ms.locfileid: "50827945"
---
# <a name="respond-to-the-task-module-submit-action"></a><span data-ttu-id="eb15f-103">Responder a la acción de envío del módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="eb15f-103">Respond to the task module submit action</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="eb15f-104">Después de que un usuario envíe el módulo de tareas, el servicio web recibe un mensaje de invocación `composeExtension/submitAction` con el identificador de comando y los valores de parámetro.</span><span class="sxs-lookup"><span data-stu-id="eb15f-104">After a user submits the task module, your web service receives a `composeExtension/submitAction` invoke message with the command ID and parameter values.</span></span> <span data-ttu-id="eb15f-105">La aplicación tiene cinco segundos para responder a la  invocación, de lo contrario, el usuario recibe un mensaje de error No se puede llegar a la aplicación y el cliente de Teams omite cualquier respuesta a la invocación.</span><span class="sxs-lookup"><span data-stu-id="eb15f-105">Your app has five seconds to respond to the invoke, otherwise the user receives an error message **Unable to reach the app** and any reply to the invoke is ignored by the Teams client.</span></span>

<span data-ttu-id="eb15f-106">Tiene las siguientes opciones para responder:</span><span class="sxs-lookup"><span data-stu-id="eb15f-106">You have the following options for responding:</span></span>

* <span data-ttu-id="eb15f-107">Sin respuesta: puede elegir usar la acción enviar para desencadenar un proceso en un sistema externo y no proporcionar comentarios al usuario.</span><span class="sxs-lookup"><span data-stu-id="eb15f-107">No response - You can choose to use the submit action to trigger a process in an external system, and not provide any feedback to the user.</span></span> <span data-ttu-id="eb15f-108">Esto puede ser útil para procesos de larga ejecución y puede elegir proporcionar comentarios de otra manera (por ejemplo, con un [mensaje proactivo](~/bots/how-to/conversations/send-proactive-messages.md).</span><span class="sxs-lookup"><span data-stu-id="eb15f-108">This can be useful for long-running processes, and you may choose to provide feedback in another manner (for example, with a [proactive message](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>
* <span data-ttu-id="eb15f-109">[Otro módulo de](#respond-with-another-task-module) tareas: puede responder con un módulo de tareas adicional como parte de una interacción de varios pasos.</span><span class="sxs-lookup"><span data-stu-id="eb15f-109">[Another task module](#respond-with-another-task-module) - You can respond with an additional task module as part of a multi-step interaction.</span></span>
* <span data-ttu-id="eb15f-110">[Respuesta de](#respond-with-a-card-inserted-into-the-compose-message-area) tarjeta: puede responder con una tarjeta con la que el usuario pueda interactuar y/o insertar en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="eb15f-110">[Card response](#respond-with-a-card-inserted-into-the-compose-message-area) - You can respond with a card that the user can then interact with and/or insert into a message.</span></span>
* <span data-ttu-id="eb15f-111">[Tarjeta adaptable del bot:](#bot-response-with-adaptive-card) inserte una tarjeta adaptable directamente en la conversación.</span><span class="sxs-lookup"><span data-stu-id="eb15f-111">[Adaptive Card from bot](#bot-response-with-adaptive-card) - Insert an Adaptive Card directly into the conversation.</span></span>
* [<span data-ttu-id="eb15f-112">Solicitar la autenticación del usuario</span><span class="sxs-lookup"><span data-stu-id="eb15f-112">Request the user authenticate</span></span>](~/messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="eb15f-113">Solicitar al usuario que proporcione una configuración adicional</span><span class="sxs-lookup"><span data-stu-id="eb15f-113">Request the user provide additional configuration</span></span>](~/messaging-extensions/how-to/add-configuration-page.md)

<span data-ttu-id="eb15f-114">Para la autenticación o la configuración, después de que el usuario complete el flujo, la invocación original se vuelve a enviar al servicio web.</span><span class="sxs-lookup"><span data-stu-id="eb15f-114">For authentication or configuration, after the user completes the flow the original invoke is re-sent to your web service.</span></span> <span data-ttu-id="eb15f-115">En la tabla siguiente se muestran los tipos de respuestas disponibles en función de la ubicación de invocación `commandContext` de la extensión de mensajería:</span><span class="sxs-lookup"><span data-stu-id="eb15f-115">The following table shows which types of responses are available based on the invoke location `commandContext` of the messaging extension:</span></span> 

|<span data-ttu-id="eb15f-116">Tipo de respuesta</span><span class="sxs-lookup"><span data-stu-id="eb15f-116">Response Type</span></span> | <span data-ttu-id="eb15f-117">redacción</span><span class="sxs-lookup"><span data-stu-id="eb15f-117">compose</span></span> | <span data-ttu-id="eb15f-118">barra de comandos</span><span class="sxs-lookup"><span data-stu-id="eb15f-118">command bar</span></span> | <span data-ttu-id="eb15f-119">mensaje</span><span class="sxs-lookup"><span data-stu-id="eb15f-119">message</span></span> |
|--------------|:-------------:|:-------------:|:---------:|
|<span data-ttu-id="eb15f-120">Respuesta de tarjeta</span><span class="sxs-lookup"><span data-stu-id="eb15f-120">Card response</span></span> | <span data-ttu-id="eb15f-121">x</span><span class="sxs-lookup"><span data-stu-id="eb15f-121">x</span></span> | <span data-ttu-id="eb15f-122">x</span><span class="sxs-lookup"><span data-stu-id="eb15f-122">x</span></span> | <span data-ttu-id="eb15f-123">x</span><span class="sxs-lookup"><span data-stu-id="eb15f-123">x</span></span> |
|<span data-ttu-id="eb15f-124">Otro módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="eb15f-124">Another task module</span></span> | <span data-ttu-id="eb15f-125">x</span><span class="sxs-lookup"><span data-stu-id="eb15f-125">x</span></span> | <span data-ttu-id="eb15f-126">x</span><span class="sxs-lookup"><span data-stu-id="eb15f-126">x</span></span> | <span data-ttu-id="eb15f-127">x</span><span class="sxs-lookup"><span data-stu-id="eb15f-127">x</span></span> |
|<span data-ttu-id="eb15f-128">Bot con tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="eb15f-128">Bot with Adaptive Card</span></span> | <span data-ttu-id="eb15f-129">x</span><span class="sxs-lookup"><span data-stu-id="eb15f-129">x</span></span> |  | <span data-ttu-id="eb15f-130">x</span><span class="sxs-lookup"><span data-stu-id="eb15f-130">x</span></span> |
| <span data-ttu-id="eb15f-131">Sin respuesta</span><span class="sxs-lookup"><span data-stu-id="eb15f-131">No response</span></span> | <span data-ttu-id="eb15f-132">x</span><span class="sxs-lookup"><span data-stu-id="eb15f-132">x</span></span> | <span data-ttu-id="eb15f-133">x</span><span class="sxs-lookup"><span data-stu-id="eb15f-133">x</span></span> | <span data-ttu-id="eb15f-134">x</span><span class="sxs-lookup"><span data-stu-id="eb15f-134">x</span></span> |

> [!NOTE]
> * <span data-ttu-id="eb15f-135">Cuando selecciona **Action.Submit** a través de tarjetas ME, envía actividad invoke con el nombre **composeExtension**, donde el valor es igual a la carga habitual.</span><span class="sxs-lookup"><span data-stu-id="eb15f-135">When you select **Action.Submit** through ME cards, it sends invoke activity with the name **composeExtension**, where the value is equal to the usual payload.</span></span>
> * <span data-ttu-id="eb15f-136">Cuando selecciona **Action.Submit** a través de la conversación, recibe actividad de mensaje con el nombre **onCardButtonClicked**, donde el valor es igual a la carga habitual.</span><span class="sxs-lookup"><span data-stu-id="eb15f-136">When you select **Action.Submit** through conversation, you receive message activity with the name **onCardButtonClicked**, where the value is equal to the usual payload.</span></span>

## <a name="the-submitaction-invoke-event"></a><span data-ttu-id="eb15f-137">El evento de invocación submitAction</span><span class="sxs-lookup"><span data-stu-id="eb15f-137">The submitAction invoke event</span></span>

<span data-ttu-id="eb15f-138">Los ejemplos de recibir el mensaje de invocación son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="eb15f-138">Examples of receiving the invoke message are as follows:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="eb15f-139">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="eb15f-139">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="eb15f-140">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="eb15f-140">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  constructor() {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
  
  //code to handle the submit action
    }
  }
}
```

# <a name="json"></a>[<span data-ttu-id="eb15f-141">JSON</span><span class="sxs-lookup"><span data-stu-id="eb15f-141">JSON</span></span>](#tab/json)

<span data-ttu-id="eb15f-142">Este es un ejemplo del objeto JSON que recibe.</span><span class="sxs-lookup"><span data-stu-id="eb15f-142">This is an example of the JSON object you receive.</span></span> <span data-ttu-id="eb15f-143">El `commandContext` parámetro indica de dónde se desencadenó la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="eb15f-143">The `commandContext` parameter indicates where your messaging extension was triggered from.</span></span> <span data-ttu-id="eb15f-144">El `data` objeto contiene los campos del formulario como parámetros y los valores enviados por el usuario.</span><span class="sxs-lookup"><span data-stu-id="eb15f-144">The `data` object contains the fields on the form as parameters, and the values the user submitted.</span></span> <span data-ttu-id="eb15f-145">El objeto JSON aquí se abrevia para resaltar los campos más relevantes.</span><span class="sxs-lookup"><span data-stu-id="eb15f-145">The JSON object here is shortened to highlight the most relevant fields.</span></span>

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

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a><span data-ttu-id="eb15f-146">Responder con una tarjeta insertada en el área del mensaje de redacción</span><span class="sxs-lookup"><span data-stu-id="eb15f-146">Respond with a card inserted into the compose message area</span></span>

<span data-ttu-id="eb15f-147">La forma más común de responder a la `composeExtension/submitAction` solicitud es con una tarjeta insertada en el área del mensaje de redacción.</span><span class="sxs-lookup"><span data-stu-id="eb15f-147">The most common way to respond to the `composeExtension/submitAction` request is with a card inserted into the compose message area.</span></span> <span data-ttu-id="eb15f-148">A continuación, el usuario puede elegir enviar la tarjeta a la conversación.</span><span class="sxs-lookup"><span data-stu-id="eb15f-148">The user can then choose to submit the card to the conversation.</span></span> <span data-ttu-id="eb15f-149">Para obtener más información sobre el uso de tarjetas, [vea tarjetas y acciones de tarjeta](~/task-modules-and-cards/cards/cards-actions.md).</span><span class="sxs-lookup"><span data-stu-id="eb15f-149">For more information on using cards see [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="eb15f-150">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="eb15f-150">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="eb15f-151">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="eb15f-151">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="eb15f-152">JSON</span><span class="sxs-lookup"><span data-stu-id="eb15f-152">JSON</span></span>](#tab/json)

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

## <a name="respond-with-another-task-module"></a><span data-ttu-id="eb15f-153">Responder con otro módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="eb15f-153">Respond with another task module</span></span>

<span data-ttu-id="eb15f-154">Puede elegir responder al evento con `submitAction` un módulo de tareas adicional.</span><span class="sxs-lookup"><span data-stu-id="eb15f-154">You can choose to respond to the `submitAction` event with an additional task module.</span></span> <span data-ttu-id="eb15f-155">Esto puede ser útil cuando:</span><span class="sxs-lookup"><span data-stu-id="eb15f-155">This can be useful when:</span></span>

* <span data-ttu-id="eb15f-156">Debe recopilar grandes cantidades de información.</span><span class="sxs-lookup"><span data-stu-id="eb15f-156">You need to collect large amounts of information.</span></span>
* <span data-ttu-id="eb15f-157">Si necesita cambiar dinámicamente la información que está recopilando en función de la entrada del usuario</span><span class="sxs-lookup"><span data-stu-id="eb15f-157">If you need to dynamically change what information you are collecting based on user input</span></span>
* <span data-ttu-id="eb15f-158">Si necesita validar la información enviada por el usuario y potencialmente reenviar el formulario con un mensaje de error si hay algún error.</span><span class="sxs-lookup"><span data-stu-id="eb15f-158">If you need to validate the information submitted by the user and potentially resend the form with an error message if something is wrong.</span></span> 

<span data-ttu-id="eb15f-159">El método de respuesta es el mismo que [responder al evento `fetchTask` inicial](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span><span class="sxs-lookup"><span data-stu-id="eb15f-159">The method for response is the same as [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span> <span data-ttu-id="eb15f-160">Si usa el SDK de Bot Framework, los mismos desencadenadores de eventos para ambas acciones de envío.</span><span class="sxs-lookup"><span data-stu-id="eb15f-160">If you are using the Bot Framework SDK the same event triggers for both submit actions.</span></span> <span data-ttu-id="eb15f-161">Esto significa que debe agregar lógica que determine la respuesta correcta.</span><span class="sxs-lookup"><span data-stu-id="eb15f-161">This means you must add logic which determines the correct response.</span></span>

## <a name="bot-response-with-adaptive-card"></a><span data-ttu-id="eb15f-162">Respuesta del bot con tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="eb15f-162">Bot response with Adaptive Card</span></span>

>[!Note]
><span data-ttu-id="eb15f-163">Este flujo requiere que agregue el objeto al manifiesto de la aplicación y que tenga definido el `bot` ámbito necesario para el bot.</span><span class="sxs-lookup"><span data-stu-id="eb15f-163">This flow requires that you add the `bot` object to your app manifest, and that you have the necessary scope defined for the bot.</span></span> <span data-ttu-id="eb15f-164">Usa el mismo identificador que la extensión de mensajería para el bot.</span><span class="sxs-lookup"><span data-stu-id="eb15f-164">Use the same ID as your messaging extension for your bot.</span></span>

<span data-ttu-id="eb15f-165">También puedes responder a la acción de envío insertando un mensaje con una tarjeta adaptable en el canal con un bot.</span><span class="sxs-lookup"><span data-stu-id="eb15f-165">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="eb15f-166">El usuario puede obtener una vista previa del mensaje antes de enviarlo y, potencialmente, editarlo o interactuar con él también.</span><span class="sxs-lookup"><span data-stu-id="eb15f-166">Your user can preview the message before submitting it, and potentially edit or interact with it as well.</span></span> <span data-ttu-id="eb15f-167">Esto puede ser muy útil en escenarios en los que se recopila información de los usuarios antes de crear una respuesta de tarjeta adaptable o cuando se actualiza la tarjeta después de que alguien interactúe con ella.</span><span class="sxs-lookup"><span data-stu-id="eb15f-167">This can be very useful in scenarios where you gather information from your users before creating an adaptive card response, or when you update the card after someone interacts with it.</span></span> <span data-ttu-id="eb15f-168">En el siguiente escenario se muestra cómo la aplicación Polly usa este flujo para configurar un sondeo sin incluir los pasos de configuración en la conversación del canal:</span><span class="sxs-lookup"><span data-stu-id="eb15f-168">The following scenario shows how the app Polly uses this flow to configure a poll without including the configuration steps in the channel conversation:</span></span>

1. <span data-ttu-id="eb15f-169">El usuario selecciona la extensión de mensajería para desencadenar el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="eb15f-169">The user selects the messaging extension to trigger the task module.</span></span>
2. <span data-ttu-id="eb15f-170">El usuario configura el sondeo con el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="eb15f-170">The user configures the poll with the task module.</span></span>
3. <span data-ttu-id="eb15f-171">Después de enviar el módulo de tareas, la aplicación usa la información proporcionada para crear el sondeo como una tarjeta adaptable y la envía como respuesta `botMessagePreview` al cliente.</span><span class="sxs-lookup"><span data-stu-id="eb15f-171">After submitting the task module the app uses the information provided to build the poll as an Adaptive Card and sends it as a `botMessagePreview` response to the client.</span></span>
4. <span data-ttu-id="eb15f-172">A continuación, el usuario puede obtener una vista previa del mensaje de tarjeta adaptable antes de que el bot lo inserte en el canal.</span><span class="sxs-lookup"><span data-stu-id="eb15f-172">The user can then preview the adaptive card message before the bot inserts it into the channel.</span></span> <span data-ttu-id="eb15f-173">Si la aplicación aún no es miembro del canal, al seleccionarla `Send` se agrega.</span><span class="sxs-lookup"><span data-stu-id="eb15f-173">If the app is not already a member of the channel, selecting `Send` adds it.</span></span>
   1. <span data-ttu-id="eb15f-174">El usuario también puede elegir el `Edit` mensaje, que los devuelve al módulo de tareas original.</span><span class="sxs-lookup"><span data-stu-id="eb15f-174">The user can also choose to `Edit` the message, which returns them to the original task module.</span></span>
5. <span data-ttu-id="eb15f-175">La interacción con la tarjeta adaptable cambia el mensaje antes de enviarlo.</span><span class="sxs-lookup"><span data-stu-id="eb15f-175">Interacting with the adaptive card changes the message before sending it.</span></span>
6. <span data-ttu-id="eb15f-176">Después de que el usuario seleccione `Send` el bot, publica el mensaje en el canal.</span><span class="sxs-lookup"><span data-stu-id="eb15f-176">After the user selects `Send` the bot posts the message to the channel.</span></span>

### <a name="respond-to-initial-submit-action"></a><span data-ttu-id="eb15f-177">Responder a la acción de envío inicial</span><span class="sxs-lookup"><span data-stu-id="eb15f-177">Respond to initial submit action</span></span>

<span data-ttu-id="eb15f-178">Para habilitar este flujo, el módulo de tareas debe responder al mensaje inicial con una vista previa de la tarjeta que el `composeExtension/submitAction` bot envía al canal.</span><span class="sxs-lookup"><span data-stu-id="eb15f-178">To enable this flow your task module should respond to the initial `composeExtension/submitAction` message with a preview of the card that the bot send to the channel.</span></span> <span data-ttu-id="eb15f-179">Esto ofrece al usuario la oportunidad de comprobar la tarjeta antes de enviarla e intentar instalar el bot en la conversación si aún no está instalado.</span><span class="sxs-lookup"><span data-stu-id="eb15f-179">This gives the user the opportunity to verify the card before sending, and also attempt to install your bot in the conversation if it is not already installed.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="eb15f-180">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="eb15f-180">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="eb15f-181">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="eb15f-181">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="eb15f-182">JSON</span><span class="sxs-lookup"><span data-stu-id="eb15f-182">JSON</span></span>](#tab/json)

>[!Note]
><span data-ttu-id="eb15f-183">Debe contener una actividad con exactamente 1 archivo `activityPreview` adjunto de tarjeta `message` adaptable.</span><span class="sxs-lookup"><span data-stu-id="eb15f-183">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span> <span data-ttu-id="eb15f-184">El `<< Card Payload >>` valor es un marcador de posición para la tarjeta que desea enviar.</span><span class="sxs-lookup"><span data-stu-id="eb15f-184">The `<< Card Payload >>` value is a placeholder for the card you wish to send.</span></span>

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

### <a name="the-botmessagepreview-send-and-edit-events"></a><span data-ttu-id="eb15f-185">Eventos de envío y edición botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="eb15f-185">The botMessagePreview send and edit events</span></span>

<span data-ttu-id="eb15f-186">La extensión de mensaje debe responder ahora a dos nuevas variedades de `composeExtension/submitAction` la invocación, donde `value.botMessagePreviewAction = "send"` y `value.botMessagePreviewAction = "edit"` .</span><span class="sxs-lookup"><span data-stu-id="eb15f-186">Your message extension must respond now to two new varieties of the `composeExtension/submitAction` invoke, where `value.botMessagePreviewAction = "send"`and `value.botMessagePreviewAction = "edit"`.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="eb15f-187">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="eb15f-187">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="eb15f-188">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="eb15f-188">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="eb15f-189">JSON</span><span class="sxs-lookup"><span data-stu-id="eb15f-189">JSON</span></span>](#tab/json)

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

### <a name="respond-to-botmessagepreview-edit"></a><span data-ttu-id="eb15f-190">Responder a la edición botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="eb15f-190">Respond to botMessagePreview edit</span></span>

<span data-ttu-id="eb15f-191">Si el usuario edita la tarjeta antes de enviarla seleccionando el botón **Editar,** recibirá una `composeExtension/submitAction` invocación con `value.botMessagePreviewAction = edit` .</span><span class="sxs-lookup"><span data-stu-id="eb15f-191">If the user edits the card before sending by selecting the **Edit** button, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = edit`.</span></span> <span data-ttu-id="eb15f-192">Normalmente, debe responder devolviendo el módulo de tareas que envió en respuesta a la invocación inicial `composeExtension/fetchTask` que inició la interacción.</span><span class="sxs-lookup"><span data-stu-id="eb15f-192">You should typically respond by returning the task module you sent in response to the initial `composeExtension/fetchTask` invoke that began the interaction.</span></span> <span data-ttu-id="eb15f-193">Esto permite al usuario iniciar el proceso de nuevo entrando de nuevo en la información original.</span><span class="sxs-lookup"><span data-stu-id="eb15f-193">This allows the user to start the process over by re-entering the original information.</span></span> <span data-ttu-id="eb15f-194">Use la información disponible para rellenar previamente el módulo de tareas para que el usuario no tenga que rellenar toda la información desde cero.</span><span class="sxs-lookup"><span data-stu-id="eb15f-194">Use the available information to pre-populate the task module so the user does not have to fill out all of the information from scratch.</span></span>

<span data-ttu-id="eb15f-195">Vea [responder al evento `fetchTask` inicial](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span><span class="sxs-lookup"><span data-stu-id="eb15f-195">See [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span>

### <a name="respond-to-botmessagepreview-send"></a><span data-ttu-id="eb15f-196">Responder al envío botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="eb15f-196">Respond to botMessagePreview send</span></span>

<span data-ttu-id="eb15f-197">Después de que el usuario seleccione el **botón Enviar,** recibirá una `composeExtension/submitAction` invocación con `value.botMessagePreviewAction = send` .</span><span class="sxs-lookup"><span data-stu-id="eb15f-197">After the user selects the **Send** button, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = send`.</span></span> <span data-ttu-id="eb15f-198">El servicio web debe crear y enviar un mensaje proactivo con la tarjeta adaptable a la conversación y responder también a la invocación.</span><span class="sxs-lookup"><span data-stu-id="eb15f-198">Your web service has to create and send a proactive message with the Adaptive Card to the conversation, and also reply to the invoke.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="eb15f-199">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="eb15f-199">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="eb15f-200">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="eb15f-200">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="eb15f-201">JSON</span><span class="sxs-lookup"><span data-stu-id="eb15f-201">JSON</span></span>](#tab/json)

<span data-ttu-id="eb15f-202">Recibirá un nuevo `composeExtension/submitAction` mensaje similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="eb15f-202">You receive a new `composeExtension/submitAction` message similar to the following:</span></span>

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

### <a name="user-attribution-for-bots-messages"></a><span data-ttu-id="eb15f-203">Atribución de usuarios para mensajes de bots</span><span class="sxs-lookup"><span data-stu-id="eb15f-203">User attribution for bots messages</span></span> 

<span data-ttu-id="eb15f-204">En escenarios en los que un bot envía mensajes en nombre de un usuario, atribuir el mensaje a ese usuario puede ayudar con la interacción y mostrar un flujo de interacción más natural.</span><span class="sxs-lookup"><span data-stu-id="eb15f-204">In scenarios where a bot sends messages on behalf of a user, attributing the message to that user can help with engagement and showcase a more natural interaction flow.</span></span> <span data-ttu-id="eb15f-205">Esta característica le permite atribuir un mensaje del bot a un usuario en cuyo nombre se envió.</span><span class="sxs-lookup"><span data-stu-id="eb15f-205">This feature allows you to attribute a message from your bot to a user on whose behalf it was sent.</span></span>

<span data-ttu-id="eb15f-206">En la imagen siguiente, a la izquierda hay un mensaje de tarjeta enviado por un *bot* sin atribución del usuario y a la derecha es una tarjeta enviada por un *bot* con atribución de usuario.</span><span class="sxs-lookup"><span data-stu-id="eb15f-206">In the following image, on the left is a card message sent by a bot *without* user attribution and on the right is a card sent by a bot *with* user attribution.</span></span>

![Captura de pantalla](../../../assets/images/messaging-extension/user-attribution-bots.png)

<span data-ttu-id="eb15f-208">Para usar la atribución de usuario en teams, debe agregar la entidad de mención en la carga que `OnBehalfOf` `ChannelData` se envía a `Activity` Teams.</span><span class="sxs-lookup"><span data-stu-id="eb15f-208">To use the user attribution in teams, you must  add the `OnBehalfOf` mention entity to `ChannelData` in your `Activity` payload that is sent to Teams.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="eb15f-209">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="eb15f-209">C#/.NET</span></span>](#tab/dotnet-1)

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

# <a name="json"></a>[<span data-ttu-id="eb15f-210">JSON</span><span class="sxs-lookup"><span data-stu-id="eb15f-210">JSON</span></span>](#tab/json-1)

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

<span data-ttu-id="eb15f-211">La siguiente sección es una descripción de las entidades de la `OnBehalfOf` matriz:</span><span class="sxs-lookup"><span data-stu-id="eb15f-211">The following section is a description of the entities in the `OnBehalfOf` of Array:</span></span>

#### <a name="details-of--onbehalfof-entity-schema"></a><span data-ttu-id="eb15f-212">Detalles del  `OnBehalfOf` esquema de entidad</span><span class="sxs-lookup"><span data-stu-id="eb15f-212">Details of  `OnBehalfOf` entity schema</span></span>

|<span data-ttu-id="eb15f-213">Field</span><span class="sxs-lookup"><span data-stu-id="eb15f-213">Field</span></span>|<span data-ttu-id="eb15f-214">Tipo</span><span class="sxs-lookup"><span data-stu-id="eb15f-214">Type</span></span>|<span data-ttu-id="eb15f-215">Description</span><span class="sxs-lookup"><span data-stu-id="eb15f-215">Description</span></span>|
|:---|:---|:---|
|`itemId`|<span data-ttu-id="eb15f-216">Entero</span><span class="sxs-lookup"><span data-stu-id="eb15f-216">Integer</span></span>|<span data-ttu-id="eb15f-217">Debe ser 0</span><span class="sxs-lookup"><span data-stu-id="eb15f-217">Should be 0</span></span>|
|`mentionType`|<span data-ttu-id="eb15f-218">Cadena</span><span class="sxs-lookup"><span data-stu-id="eb15f-218">String</span></span>|<span data-ttu-id="eb15f-219">Debe ser "persona"</span><span class="sxs-lookup"><span data-stu-id="eb15f-219">Should be "person"</span></span>|
|`mri`|<span data-ttu-id="eb15f-220">Cadena</span><span class="sxs-lookup"><span data-stu-id="eb15f-220">String</span></span>|<span data-ttu-id="eb15f-221">Identificador de recurso de mensaje (MRI) de la persona en cuyo nombre se envía el mensaje.</span><span class="sxs-lookup"><span data-stu-id="eb15f-221">Message resource identifier (MRI) of the person on whose behalf the message is sent.</span></span> <span data-ttu-id="eb15f-222">El nombre del remitente del mensaje aparecería como " \<user\> via \<bot name\> ".</span><span class="sxs-lookup"><span data-stu-id="eb15f-222">Message sender name would appear as "\<user\> via \<bot name\>".</span></span>|
|`displayName`|<span data-ttu-id="eb15f-223">Cadena</span><span class="sxs-lookup"><span data-stu-id="eb15f-223">String</span></span>|<span data-ttu-id="eb15f-224">Nombre de la persona.</span><span class="sxs-lookup"><span data-stu-id="eb15f-224">Name of the person.</span></span> <span data-ttu-id="eb15f-225">Se usa como reserva en caso de que la resolución de nombres no esté disponible.</span><span class="sxs-lookup"><span data-stu-id="eb15f-225">Used as fallback in case name resolution is unavailable.</span></span>|
  
## <a name="next-steps"></a><span data-ttu-id="eb15f-226">Siguientes pasos</span><span class="sxs-lookup"><span data-stu-id="eb15f-226">Next Steps</span></span>

<span data-ttu-id="eb15f-227">Agregar un comando de búsqueda</span><span class="sxs-lookup"><span data-stu-id="eb15f-227">Add a search command</span></span>

* [<span data-ttu-id="eb15f-228">Definición de comandos de búsqueda</span><span class="sxs-lookup"><span data-stu-id="eb15f-228">Define search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]

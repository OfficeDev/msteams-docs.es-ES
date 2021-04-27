---
title: Responder a la acción de envío del módulo de tareas
author: clearab
description: Describe cómo responder a la acción de envío del módulo de tareas desde un comando de acción de extensión de mensajería
localization_priority: Normal
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 3ed682eadde410a545f73768943a51ef95123e49
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019835"
---
# <a name="respond-to-the-task-module-submit-action"></a><span data-ttu-id="f9c94-103">Responder a la acción de envío del módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="f9c94-103">Respond to the task module submit action</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="f9c94-104">Este documento te guía sobre cómo la aplicación responde a los comandos de acción, como la acción de envío del módulo de tareas del usuario.</span><span class="sxs-lookup"><span data-stu-id="f9c94-104">This document guides you on how your app responds to the action commands, such as user's task module submit action.</span></span>
<span data-ttu-id="f9c94-105">Después de que un usuario envíe el módulo de tareas, el servicio web recibe un mensaje de invocación `composeExtension/submitAction` con el identificador de comando y los valores de parámetro.</span><span class="sxs-lookup"><span data-stu-id="f9c94-105">After a user submits the task module, your web service receives a `composeExtension/submitAction` invoke message with the command ID and parameter values.</span></span> <span data-ttu-id="f9c94-106">La aplicación tiene cinco segundos para responder a la invocación, de lo contrario, el usuario recibe un mensaje de error No se puede llegar a la aplicación y el cliente de Teams omite cualquier respuesta a la invocación.</span><span class="sxs-lookup"><span data-stu-id="f9c94-106">Your app has five seconds to respond to the invoke, otherwise the user receives an error message **Unable to reach the app**, and any reply to the invoke is ignored by the Teams client.</span></span>

<span data-ttu-id="f9c94-107">Tiene las siguientes opciones para responder:</span><span class="sxs-lookup"><span data-stu-id="f9c94-107">You have the following options to respond:</span></span>

* <span data-ttu-id="f9c94-108">Sin respuesta: use la acción enviar para desencadenar un proceso en un sistema externo y no proporcionar comentarios al usuario.</span><span class="sxs-lookup"><span data-stu-id="f9c94-108">No response: Use the submit action to trigger a process in an external system, and not provide any feedback to the user.</span></span> <span data-ttu-id="f9c94-109">Esto es útil para procesos de larga ejecución y puede seleccionar proporcionar comentarios alternativamente.</span><span class="sxs-lookup"><span data-stu-id="f9c94-109">This is useful for long-running processes, and you can select to provide feedback alternately.</span></span> <span data-ttu-id="f9c94-110">Por ejemplo, puede enviar comentarios con un [mensaje proactivo](~/bots/how-to/conversations/send-proactive-messages.md).</span><span class="sxs-lookup"><span data-stu-id="f9c94-110">For example, you can give feedback with a [proactive message](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>
* <span data-ttu-id="f9c94-111">[Otro módulo de](#respond-with-another-task-module)tareas: puede responder con un módulo de tareas adicional como parte de una interacción de varios pasos.</span><span class="sxs-lookup"><span data-stu-id="f9c94-111">[Another task module](#respond-with-another-task-module): You can respond with an additional task module as part of a multi-step interaction.</span></span>
* <span data-ttu-id="f9c94-112">[Respuesta de](#respond-with-a-card-inserted-into-the-compose-message-area)tarjeta: puede responder con una tarjeta con la que el usuario puede interactuar o insertar en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="f9c94-112">[Card response](#respond-with-a-card-inserted-into-the-compose-message-area): You can respond with a card that the user can interact with or insert into a message.</span></span>
* <span data-ttu-id="f9c94-113">[Tarjeta adaptable desde el bot:](#bot-response-with-adaptive-card)inserte una tarjeta adaptable directamente en la conversación.</span><span class="sxs-lookup"><span data-stu-id="f9c94-113">[Adaptive Card from bot](#bot-response-with-adaptive-card): Insert an Adaptive Card directly into the conversation.</span></span>
* <span data-ttu-id="f9c94-114">[Solicitar al usuario que autentique](~/messaging-extensions/how-to/add-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f9c94-114">[Request the user to authenticate](~/messaging-extensions/how-to/add-authentication.md).</span></span>
* <span data-ttu-id="f9c94-115">[Solicite al usuario que proporcione una configuración adicional](~/messaging-extensions/how-to/add-configuration-page.md).</span><span class="sxs-lookup"><span data-stu-id="f9c94-115">[Request the user to provide additional configuration](~/messaging-extensions/how-to/add-configuration-page.md).</span></span>

<span data-ttu-id="f9c94-116">Para la autenticación o configuración, después de que el usuario complete el proceso, la invocación original se resiente al servicio web.</span><span class="sxs-lookup"><span data-stu-id="f9c94-116">For authentication or configuration, after the user completes the process, the original invoke is resent to your web service.</span></span> <span data-ttu-id="f9c94-117">En la tabla siguiente se muestran los tipos de respuestas disponibles en función de la ubicación de invocación `commandContext` de la extensión de mensajería:</span><span class="sxs-lookup"><span data-stu-id="f9c94-117">The following table shows which types of responses are available based on the invoke location `commandContext` of the messaging extension:</span></span> 

|<span data-ttu-id="f9c94-118">Tipo de respuesta</span><span class="sxs-lookup"><span data-stu-id="f9c94-118">Response Type</span></span> | <span data-ttu-id="f9c94-119">Redacción</span><span class="sxs-lookup"><span data-stu-id="f9c94-119">Compose</span></span> | <span data-ttu-id="f9c94-120">Barra de comandos</span><span class="sxs-lookup"><span data-stu-id="f9c94-120">Command bar</span></span> | <span data-ttu-id="f9c94-121">Message</span><span class="sxs-lookup"><span data-stu-id="f9c94-121">Message</span></span> |
|--------------|:-------------:|:-------------:|:---------:|
|<span data-ttu-id="f9c94-122">Respuesta de tarjeta</span><span class="sxs-lookup"><span data-stu-id="f9c94-122">Card response</span></span> | <span data-ttu-id="f9c94-123">✔</span><span class="sxs-lookup"><span data-stu-id="f9c94-123">✔</span></span> | <span data-ttu-id="f9c94-124">✔</span><span class="sxs-lookup"><span data-stu-id="f9c94-124">✔</span></span> | <span data-ttu-id="f9c94-125">✔</span><span class="sxs-lookup"><span data-stu-id="f9c94-125">✔</span></span> |
|<span data-ttu-id="f9c94-126">Otro módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="f9c94-126">Another task module</span></span> | <span data-ttu-id="f9c94-127">✔</span><span class="sxs-lookup"><span data-stu-id="f9c94-127">✔</span></span> | <span data-ttu-id="f9c94-128">✔</span><span class="sxs-lookup"><span data-stu-id="f9c94-128">✔</span></span> | <span data-ttu-id="f9c94-129">✔</span><span class="sxs-lookup"><span data-stu-id="f9c94-129">✔</span></span> |
|<span data-ttu-id="f9c94-130">Bot con tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="f9c94-130">Bot with Adaptive Card</span></span> | <span data-ttu-id="f9c94-131">✔</span><span class="sxs-lookup"><span data-stu-id="f9c94-131">✔</span></span> | <span data-ttu-id="f9c94-132">x</span><span class="sxs-lookup"><span data-stu-id="f9c94-132">x</span></span> | <span data-ttu-id="f9c94-133">✔</span><span class="sxs-lookup"><span data-stu-id="f9c94-133">✔</span></span> |
| <span data-ttu-id="f9c94-134">Sin respuesta</span><span class="sxs-lookup"><span data-stu-id="f9c94-134">No response</span></span> | <span data-ttu-id="f9c94-135">✔</span><span class="sxs-lookup"><span data-stu-id="f9c94-135">✔</span></span> | <span data-ttu-id="f9c94-136">✔</span><span class="sxs-lookup"><span data-stu-id="f9c94-136">✔</span></span> | <span data-ttu-id="f9c94-137">✔</span><span class="sxs-lookup"><span data-stu-id="f9c94-137">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="f9c94-138">Cuando selecciona **Action.Submit** a través de tarjetas ME, envía actividad invoke con el nombre **composeExtension**, donde el valor es igual a la carga habitual.</span><span class="sxs-lookup"><span data-stu-id="f9c94-138">When you select **Action.Submit** through ME cards, it sends invoke activity with the name **composeExtension**, where the value is equal to the usual payload.</span></span>
> * <span data-ttu-id="f9c94-139">Cuando selecciona **Action.Submit** a través de la conversación, recibe actividad de mensaje con el nombre **onCardButtonClicked**, donde el valor es igual a la carga habitual.</span><span class="sxs-lookup"><span data-stu-id="f9c94-139">When you select **Action.Submit** through conversation, you receive message activity with the name **onCardButtonClicked**, where the value is equal to the usual payload.</span></span>

## <a name="the-submitaction-invoke-event"></a><span data-ttu-id="f9c94-140">El evento de invocación submitAction</span><span class="sxs-lookup"><span data-stu-id="f9c94-140">The submitAction invoke event</span></span>

<span data-ttu-id="f9c94-141">Los ejemplos de recibir el mensaje de invocación son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="f9c94-141">Examples of receiving the invoke message are as follows:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f9c94-142">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f9c94-142">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="f9c94-143">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f9c94-143">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  constructor() {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
  
  //code to handle the submit action
    }
  }
}
```

# <a name="json"></a>[<span data-ttu-id="f9c94-144">JSON</span><span class="sxs-lookup"><span data-stu-id="f9c94-144">JSON</span></span>](#tab/json)

<span data-ttu-id="f9c94-145">Este es un ejemplo del objeto JSON que recibe.</span><span class="sxs-lookup"><span data-stu-id="f9c94-145">This is an example of the JSON object that you receive.</span></span> <span data-ttu-id="f9c94-146">El `commandContext` parámetro indica de dónde se desencadenó la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="f9c94-146">The `commandContext` parameter indicates where your messaging extension was triggered from.</span></span> <span data-ttu-id="f9c94-147">El `data` objeto contiene los campos del formulario como parámetros y los valores enviados por el usuario.</span><span class="sxs-lookup"><span data-stu-id="f9c94-147">The `data` object contains the fields on the form as parameters, and the values the user submitted.</span></span> <span data-ttu-id="f9c94-148">El objeto JSON aquí se abrevia para resaltar los campos más relevantes.</span><span class="sxs-lookup"><span data-stu-id="f9c94-148">The JSON object here is shortened to highlight the most relevant fields.</span></span>

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

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a><span data-ttu-id="f9c94-149">Responder con una tarjeta insertada en el área del mensaje de redacción</span><span class="sxs-lookup"><span data-stu-id="f9c94-149">Respond with a card inserted into the compose message area</span></span>

<span data-ttu-id="f9c94-150">La forma más común de responder a la `composeExtension/submitAction` solicitud es con una tarjeta insertada en el área del mensaje de redacción.</span><span class="sxs-lookup"><span data-stu-id="f9c94-150">The most common way to respond to the `composeExtension/submitAction` request is with a card inserted into the compose message area.</span></span> <span data-ttu-id="f9c94-151">El usuario envía la tarjeta a la conversación.</span><span class="sxs-lookup"><span data-stu-id="f9c94-151">The user submits the card to the conversation.</span></span> <span data-ttu-id="f9c94-152">Para obtener más información sobre el uso de tarjetas, vea [tarjetas y acciones de tarjeta.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="f9c94-152">For more information on using cards, see [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f9c94-153">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f9c94-153">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="f9c94-154">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f9c94-154">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="f9c94-155">JSON</span><span class="sxs-lookup"><span data-stu-id="f9c94-155">JSON</span></span>](#tab/json)

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

## <a name="respond-with-another-task-module"></a><span data-ttu-id="f9c94-156">Responder con otro módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="f9c94-156">Respond with another task module</span></span>

<span data-ttu-id="f9c94-157">Puede seleccionar para responder al evento `submitAction` con un módulo de tareas adicional.</span><span class="sxs-lookup"><span data-stu-id="f9c94-157">You can select to respond to the `submitAction` event with an additional task module.</span></span> <span data-ttu-id="f9c94-158">Esto resulta útil cuando:</span><span class="sxs-lookup"><span data-stu-id="f9c94-158">This is useful when:</span></span>

* <span data-ttu-id="f9c94-159">Debe recopilar grandes cantidades de información.</span><span class="sxs-lookup"><span data-stu-id="f9c94-159">You need to collect large amounts of information.</span></span>
* <span data-ttu-id="f9c94-160">Debe cambiar dinámicamente la información que está recopilando en función de la entrada del usuario.</span><span class="sxs-lookup"><span data-stu-id="f9c94-160">You need to dynamically change the information you are collecting based on user input.</span></span>
* <span data-ttu-id="f9c94-161">Debe validar la información enviada por el usuario y volver a enviar el formulario con un mensaje de error si hay algún error.</span><span class="sxs-lookup"><span data-stu-id="f9c94-161">You need to validate the information submitted by the user and resend the form with an error message if something is wrong.</span></span> 

<span data-ttu-id="f9c94-162">El método de respuesta es el mismo que [responder al evento `fetchTask` inicial](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span><span class="sxs-lookup"><span data-stu-id="f9c94-162">The method for response is the same as [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span> <span data-ttu-id="f9c94-163">Si usa el SDK de Bot Framework, los mismos desencadenadores de eventos para ambas acciones de envío.</span><span class="sxs-lookup"><span data-stu-id="f9c94-163">If you are using the Bot Framework SDK the same event triggers for both submit actions.</span></span> <span data-ttu-id="f9c94-164">Para que esto funcione, debe agregar lógica que determine la respuesta correcta.</span><span class="sxs-lookup"><span data-stu-id="f9c94-164">To make this work, you must add logic that determines the correct response.</span></span>

## <a name="bot-response-with-adaptive-card"></a><span data-ttu-id="f9c94-165">Respuesta del bot con tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="f9c94-165">Bot response with Adaptive Card</span></span>

> [!NOTE]
> <span data-ttu-id="f9c94-166">El requisito previo para obtener la respuesta del bot con una tarjeta adaptable es que debes agregar el objeto al manifiesto de la aplicación y definir el ámbito `bot` necesario para el bot.</span><span class="sxs-lookup"><span data-stu-id="f9c94-166">The prerequisite to get the bot response with an Adaptive card is that you must add the `bot` object to your app manifest, and define the required scope for the bot.</span></span> <span data-ttu-id="f9c94-167">Usa el mismo identificador que la extensión de mensajería para el bot.</span><span class="sxs-lookup"><span data-stu-id="f9c94-167">Use the same ID as your messaging extension for your bot.</span></span>
 
<span data-ttu-id="f9c94-168">También puede responder al insertar un mensaje con una tarjeta adaptable `submitAction` en el canal con un bot.</span><span class="sxs-lookup"><span data-stu-id="f9c94-168">You can also respond to the `submitAction` by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="f9c94-169">El usuario puede obtener una vista previa del mensaje antes de enviarlo.</span><span class="sxs-lookup"><span data-stu-id="f9c94-169">The user can preview the message before submitting it.</span></span> <span data-ttu-id="f9c94-170">Esto es muy útil en escenarios en los que se recopila información de los usuarios antes de crear una respuesta de tarjeta adaptable o cuando se actualiza la tarjeta después de que alguien interactúa con ella.</span><span class="sxs-lookup"><span data-stu-id="f9c94-170">This is very useful in scenarios where you gather information from the users before creating an Adaptive Card response, or when you update the card after someone interacts with it.</span></span> 

<span data-ttu-id="f9c94-171">El siguiente escenario muestra cómo la aplicación Polly configura un sondeo sin incluir los pasos de configuración en la conversación del canal:</span><span class="sxs-lookup"><span data-stu-id="f9c94-171">The following scenario shows how the app Polly configures a poll without including the configuration steps in the channel conversation:</span></span>

<span data-ttu-id="f9c94-172">**Para configurar el sondeo**</span><span class="sxs-lookup"><span data-stu-id="f9c94-172">**To configure the poll**</span></span>

1. <span data-ttu-id="f9c94-173">El usuario selecciona la extensión de mensajería para invocar el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="f9c94-173">The user selects the messaging extension to invoke the task module.</span></span>
1. <span data-ttu-id="f9c94-174">El usuario configura el sondeo con el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="f9c94-174">The user configures the poll with the task module.</span></span>
1. <span data-ttu-id="f9c94-175">Después de enviar el módulo de tareas, la aplicación usa la información proporcionada para crear el sondeo como una tarjeta adaptable y la envía como respuesta `botMessagePreview` al cliente.</span><span class="sxs-lookup"><span data-stu-id="f9c94-175">After submitting the task module, the app uses the information provided to build the poll as an Adaptive Card and sends it as a `botMessagePreview` response to the client.</span></span>
1. <span data-ttu-id="f9c94-176">A continuación, el usuario puede obtener una vista previa del mensaje de tarjeta adaptable antes de que el bot lo inserte en el canal.</span><span class="sxs-lookup"><span data-stu-id="f9c94-176">The user can then preview the Adaptive Card message before the bot inserts it into the channel.</span></span> <span data-ttu-id="f9c94-177">Si la aplicación aún no es miembro del canal, selecciona `Send` para agregarla.</span><span class="sxs-lookup"><span data-stu-id="f9c94-177">If the app is not already a member of the channel, select `Send` to add it.</span></span>

    > [!NOTE] 
    > * <span data-ttu-id="f9c94-178">Los usuarios también pueden seleccionar `Edit` el mensaje, que los devuelve al módulo de tareas original.</span><span class="sxs-lookup"><span data-stu-id="f9c94-178">The users can also select to `Edit` the message, which returns them to the original task module.</span></span> 
    > * <span data-ttu-id="f9c94-179">La interacción con la tarjeta adaptable cambia el mensaje antes de enviarlo.</span><span class="sxs-lookup"><span data-stu-id="f9c94-179">Interaction with the Adaptive Card changes the message before sending it.</span></span>
1. <span data-ttu-id="f9c94-180">Después de que el usuario seleccione `Send` el bot, publica el mensaje en el canal.</span><span class="sxs-lookup"><span data-stu-id="f9c94-180">After the user selects `Send` the bot posts the message to the channel.</span></span>

## <a name="respond-to-initial-submit-action"></a><span data-ttu-id="f9c94-181">Responder a la acción de envío inicial</span><span class="sxs-lookup"><span data-stu-id="f9c94-181">Respond to initial submit action</span></span>

<span data-ttu-id="f9c94-182">El módulo de tareas debe responder al mensaje inicial con una vista previa de la tarjeta que el `composeExtension/submitAction` bot envía al canal.</span><span class="sxs-lookup"><span data-stu-id="f9c94-182">Your task module must respond to the initial `composeExtension/submitAction` message with a preview of the card that the bot sends to the channel.</span></span> <span data-ttu-id="f9c94-183">El usuario puede comprobar la tarjeta antes de enviar e intentar instalar el bot en la conversación si el bot aún no está instalado.</span><span class="sxs-lookup"><span data-stu-id="f9c94-183">The user can verify the card before sending, and also try to install your bot in the conversation if the bot is not already installed.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f9c94-184">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f9c94-184">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="f9c94-185">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f9c94-185">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="f9c94-186">JSON</span><span class="sxs-lookup"><span data-stu-id="f9c94-186">JSON</span></span>](#tab/json)

> [!NOTE]
> * <span data-ttu-id="f9c94-187">Debe `activityPreview` contener una actividad con exactamente un dato adjunto de tarjeta `message` adaptable.</span><span class="sxs-lookup"><span data-stu-id="f9c94-187">The `activityPreview` must contain a `message` activity with exactly one Adaptive Card attachment.</span></span> <span data-ttu-id="f9c94-188">El `<< Card Payload >>` valor es un marcador de posición para la tarjeta que desea enviar.</span><span class="sxs-lookup"><span data-stu-id="f9c94-188">The `<< Card Payload >>` value is a placeholder for the card you want to send.</span></span>

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

### <a name="the-botmessagepreview-send-and-edit-events"></a><span data-ttu-id="f9c94-189">Eventos de envío y edición botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="f9c94-189">The botMessagePreview send and edit events</span></span>

<span data-ttu-id="f9c94-190">La extensión de mensajería debe responder a dos nuevos tipos de `composeExtension/submitAction` invocación, where `value.botMessagePreviewAction = "send"` y `value.botMessagePreviewAction = "edit"` .</span><span class="sxs-lookup"><span data-stu-id="f9c94-190">Your messaging extension must respond to two new types of the `composeExtension/submitAction` invoke, where `value.botMessagePreviewAction = "send"`and `value.botMessagePreviewAction = "edit"`.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f9c94-191">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f9c94-191">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="f9c94-192">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f9c94-192">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="f9c94-193">JSON</span><span class="sxs-lookup"><span data-stu-id="f9c94-193">JSON</span></span>](#tab/json)

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

### <a name="respond-to-botmessagepreview-edit"></a><span data-ttu-id="f9c94-194">Responder a la edición botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="f9c94-194">Respond to botMessagePreview edit</span></span>

<span data-ttu-id="f9c94-195">Si el usuario edita la tarjeta antes de enviarla, **seleccionando Editar**, recibirá una `composeExtension/submitAction` invocación con `value.botMessagePreviewAction = edit` .</span><span class="sxs-lookup"><span data-stu-id="f9c94-195">If the user edits the card before sending, by selecting **Edit**, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = edit`.</span></span> <span data-ttu-id="f9c94-196">Debe responder devolviendo el módulo de tareas que envió, en respuesta a la invocación inicial `composeExtension/fetchTask` que inició la interacción.</span><span class="sxs-lookup"><span data-stu-id="f9c94-196">You must respond by returning the task module you sent, in response to the initial `composeExtension/fetchTask` invoke that began the interaction.</span></span> <span data-ttu-id="f9c94-197">Esto permite al usuario iniciar el proceso entrando de nuevo en la información original.</span><span class="sxs-lookup"><span data-stu-id="f9c94-197">This allows the user to start the process by re-entering the original information.</span></span> <span data-ttu-id="f9c94-198">Use la información disponible para actualizar el módulo de tareas de modo que el usuario no necesite rellenar toda la información desde cero.</span><span class="sxs-lookup"><span data-stu-id="f9c94-198">Use the available information to update the task module so that the user need not fill out all information from scratch.</span></span>
<span data-ttu-id="f9c94-199">Para obtener más información sobre cómo responder al evento inicial, vea `fetchTask` responding to the initial [ `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span><span class="sxs-lookup"><span data-stu-id="f9c94-199">For more information on responding to the initial `fetchTask` event, see [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span>

### <a name="respond-to-botmessagepreview-send"></a><span data-ttu-id="f9c94-200">Responder al envío botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="f9c94-200">Respond to botMessagePreview send</span></span>

<span data-ttu-id="f9c94-201">Después de que el usuario seleccione **El envío**, recibirá una `composeExtension/submitAction` invocación con `value.botMessagePreviewAction = send` .</span><span class="sxs-lookup"><span data-stu-id="f9c94-201">After the user selects the **Send**, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = send`.</span></span> <span data-ttu-id="f9c94-202">El servicio web debe crear y enviar un mensaje proactivo con la tarjeta adaptable a la conversación y responder también a la invocación.</span><span class="sxs-lookup"><span data-stu-id="f9c94-202">Your web service has to create and send a proactive message with the Adaptive Card to the conversation, and also reply to the invoke.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f9c94-203">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f9c94-203">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="f9c94-204">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f9c94-204">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="f9c94-205">JSON</span><span class="sxs-lookup"><span data-stu-id="f9c94-205">JSON</span></span>](#tab/json)

<span data-ttu-id="f9c94-206">Recibirá un nuevo `composeExtension/submitAction` mensaje similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="f9c94-206">You receive a new `composeExtension/submitAction` message similar to the following:</span></span>

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

### <a name="user-attribution-for-bots-messages"></a><span data-ttu-id="f9c94-207">Atribución de usuarios para mensajes de bots</span><span class="sxs-lookup"><span data-stu-id="f9c94-207">User attribution for bots messages</span></span> 

<span data-ttu-id="f9c94-208">En escenarios en los que un bot envía mensajes en nombre de un usuario, la atribución del mensaje a ese usuario ayuda a la interacción y muestra un flujo de interacción más natural.</span><span class="sxs-lookup"><span data-stu-id="f9c94-208">In scenarios where a bot sends messages on behalf of a user, attributing the message to that user helps with engagement and showcase a more natural interaction flow.</span></span> <span data-ttu-id="f9c94-209">Esta característica le permite atribuir un mensaje del bot a un usuario en cuyo nombre se envió.</span><span class="sxs-lookup"><span data-stu-id="f9c94-209">This feature allows you to attribute a message from your bot to a user on whose behalf it was sent.</span></span>

<span data-ttu-id="f9c94-210">En la imagen siguiente, a la izquierda hay un mensaje de tarjeta enviado por un bot sin atribución del usuario y a la derecha es una tarjeta enviada por un bot con atribución de usuario.</span><span class="sxs-lookup"><span data-stu-id="f9c94-210">In the following image, on the left is a card message sent by a bot without user attribution and on the right is a card sent by a bot with user attribution.</span></span>

![bots de atribución de usuarios](../../../assets/images/messaging-extension/user-attribution-bots.png)

<span data-ttu-id="f9c94-212">Para usar la atribución de usuario en teams, debe agregar la entidad de mención en la carga que `OnBehalfOf` `ChannelData` se envía a `Activity` Teams.</span><span class="sxs-lookup"><span data-stu-id="f9c94-212">To use the user attribution in teams, you must add the `OnBehalfOf` mention entity to `ChannelData` in your `Activity` payload that is sent to Teams.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f9c94-213">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f9c94-213">C#/.NET</span></span>](#tab/dotnet-1)

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

# <a name="json"></a>[<span data-ttu-id="f9c94-214">JSON</span><span class="sxs-lookup"><span data-stu-id="f9c94-214">JSON</span></span>](#tab/json-1)

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

#### <a name="details-of--onbehalfof-entity-schema"></a><span data-ttu-id="f9c94-215">Detalles del  `OnBehalfOf` esquema de entidad</span><span class="sxs-lookup"><span data-stu-id="f9c94-215">Details of  `OnBehalfOf` entity schema</span></span>

<span data-ttu-id="f9c94-216">La siguiente sección es una descripción de las entidades de la `OnBehalfOf` matriz:</span><span class="sxs-lookup"><span data-stu-id="f9c94-216">The following section is a description of the entities in the `OnBehalfOf` Array:</span></span>

|<span data-ttu-id="f9c94-217">Field</span><span class="sxs-lookup"><span data-stu-id="f9c94-217">Field</span></span>|<span data-ttu-id="f9c94-218">Tipo</span><span class="sxs-lookup"><span data-stu-id="f9c94-218">Type</span></span>|<span data-ttu-id="f9c94-219">Descripción</span><span class="sxs-lookup"><span data-stu-id="f9c94-219">Description</span></span>|
|:---|:---|:---|
|`itemId`|<span data-ttu-id="f9c94-220">Entero</span><span class="sxs-lookup"><span data-stu-id="f9c94-220">Integer</span></span>|<span data-ttu-id="f9c94-221">Describe la identificación del elemento.</span><span class="sxs-lookup"><span data-stu-id="f9c94-221">Describes identification of the item.</span></span> <span data-ttu-id="f9c94-222">Su valor debe ser `0` .</span><span class="sxs-lookup"><span data-stu-id="f9c94-222">Its value must be `0`.</span></span>|
|`mentionType`|<span data-ttu-id="f9c94-223">Cadena</span><span class="sxs-lookup"><span data-stu-id="f9c94-223">String</span></span>|<span data-ttu-id="f9c94-224">Describe la mención de una "persona".</span><span class="sxs-lookup"><span data-stu-id="f9c94-224">Describes the mention of a "person".</span></span>|
|`mri`|<span data-ttu-id="f9c94-225">Cadena</span><span class="sxs-lookup"><span data-stu-id="f9c94-225">String</span></span>|<span data-ttu-id="f9c94-226">Identificador de recurso de mensaje (MRI) de la persona en cuyo nombre se envía el mensaje.</span><span class="sxs-lookup"><span data-stu-id="f9c94-226">Message resource identifier (MRI) of the person on whose behalf the message is sent.</span></span> <span data-ttu-id="f9c94-227">El nombre del remitente del mensaje aparecería como " \<user\> a \<bot name\> través de ".</span><span class="sxs-lookup"><span data-stu-id="f9c94-227">Message sender name would appear as "\<user\> through \<bot name\>".</span></span>|
|`displayName`|<span data-ttu-id="f9c94-228">Cadena</span><span class="sxs-lookup"><span data-stu-id="f9c94-228">String</span></span>|<span data-ttu-id="f9c94-229">Nombre de la persona.</span><span class="sxs-lookup"><span data-stu-id="f9c94-229">Name of the person.</span></span> <span data-ttu-id="f9c94-230">Se usa como reserva en caso de que la resolución de nombres no esté disponible.</span><span class="sxs-lookup"><span data-stu-id="f9c94-230">Used as fallback in case name resolution is unavailable.</span></span>|
  
## <a name="code-sample"></a><span data-ttu-id="f9c94-231">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="f9c94-231">Code sample</span></span>

| <span data-ttu-id="f9c94-232">Nombre de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f9c94-232">Sample Name</span></span>           | <span data-ttu-id="f9c94-233">Descripción</span><span class="sxs-lookup"><span data-stu-id="f9c94-233">Description</span></span> | <span data-ttu-id="f9c94-234">.NET</span><span class="sxs-lookup"><span data-stu-id="f9c94-234">.NET</span></span>    | <span data-ttu-id="f9c94-235">Node.js</span><span class="sxs-lookup"><span data-stu-id="f9c94-235">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="f9c94-236">Acción de extensión de mensajería de Teams</span><span class="sxs-lookup"><span data-stu-id="f9c94-236">Teams messaging extension action</span></span>| <span data-ttu-id="f9c94-237">Describe cómo definir comandos de acción, crear módulo de tareas y responder a la acción de envío del módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="f9c94-237">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="f9c94-238">View</span><span class="sxs-lookup"><span data-stu-id="f9c94-238">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="f9c94-239">View</span><span class="sxs-lookup"><span data-stu-id="f9c94-239">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="f9c94-240">Búsqueda de extensión de mensajería de Teams</span><span class="sxs-lookup"><span data-stu-id="f9c94-240">Teams messaging extension search</span></span>   |  <span data-ttu-id="f9c94-241">Describe cómo definir comandos de búsqueda y responder a las búsquedas.</span><span class="sxs-lookup"><span data-stu-id="f9c94-241">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="f9c94-242">View</span><span class="sxs-lookup"><span data-stu-id="f9c94-242">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="f9c94-243">View</span><span class="sxs-lookup"><span data-stu-id="f9c94-243">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a><span data-ttu-id="f9c94-244">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="f9c94-244">Next Step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f9c94-245">Definición de comandos de búsqueda</span><span class="sxs-lookup"><span data-stu-id="f9c94-245">Define search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)


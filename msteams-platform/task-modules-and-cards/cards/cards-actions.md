---
title: Agregar acciones de tarjeta en un bot
description: Describe las acciones de tarjeta en Microsoft Teams y cómo usarlas en sus bots.
localization_priority: Normal
ms.topic: conceptual
keywords: acciones de tarjetas de bots de equipos
ms.openlocfilehash: 4af152f6179785687d4fd7371d202c56e1aee170
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254205"
---
# <a name="card-actions"></a><span data-ttu-id="17e7b-104">Acciones de tarjeta</span><span class="sxs-lookup"><span data-stu-id="17e7b-104">Card actions</span></span>

<span data-ttu-id="17e7b-105">Las tarjetas que usan los bots y las extensiones de mensajería en Teams admiten los siguientes tipos[`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) de actividad:</span><span class="sxs-lookup"><span data-stu-id="17e7b-105">Cards used by bots and messaging extensions in Teams support the following activity [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) types:</span></span>

> [!NOTE]
> <span data-ttu-id="17e7b-106">Las acciones de `CardAction` difieren de `potentialActions` para las tarjetas del conector de Office 365 cuando se usan desde conectores.</span><span class="sxs-lookup"><span data-stu-id="17e7b-106">The `CardAction` actions differ from `potentialActions` for Office 365 Connector cards when used from connectors.</span></span>

| <span data-ttu-id="17e7b-107">Tipo</span><span class="sxs-lookup"><span data-stu-id="17e7b-107">Type</span></span> | <span data-ttu-id="17e7b-108">Acción</span><span class="sxs-lookup"><span data-stu-id="17e7b-108">Action</span></span> |
| --- | --- |
| `openUrl` | <span data-ttu-id="17e7b-109">Abre una dirección URL en el explorador predeterminado.</span><span class="sxs-lookup"><span data-stu-id="17e7b-109">Opens a URL in the default browser.</span></span> |
| `messageBack` | <span data-ttu-id="17e7b-110">Envía un mensaje y una carga al bot desde el usuario que seleccionó el botón o tocó la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="17e7b-110">Sends a message and payload to the bot from the user who selected the button or tapped the card.</span></span> <span data-ttu-id="17e7b-111">Envía un mensaje independiente a la secuencia de chat.</span><span class="sxs-lookup"><span data-stu-id="17e7b-111">Sends a separate message to the chat stream.</span></span> |
| `imBack`| <span data-ttu-id="17e7b-112">Envía un mensaje al bot desde el usuario que seleccionó el botón o tocó la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="17e7b-112">Sends a message to the bot from the user who selected the button or tapped the card.</span></span> <span data-ttu-id="17e7b-113">Este mensaje del usuario al bot es visible para todos los participantes de la conversación.</span><span class="sxs-lookup"><span data-stu-id="17e7b-113">This message from user to bot is visible to all conversation participants.</span></span> |
| `invoke` | <span data-ttu-id="17e7b-114">Envía un mensaje y una carga al bot desde el usuario que seleccionó el botón o tocó la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="17e7b-114">Sends a message and payload to the bot from the user who selected the button or tapped the card.</span></span> <span data-ttu-id="17e7b-115">Este mensaje no está visible.</span><span class="sxs-lookup"><span data-stu-id="17e7b-115">This message is not visible.</span></span> |
| `signin` | <span data-ttu-id="17e7b-116">Inicia el flujo de OAuth, lo que permite a los bots conectarse con servicios seguros.</span><span class="sxs-lookup"><span data-stu-id="17e7b-116">Initiates OAuth flow, allowing bots to connect with secure services.</span></span> |

> [!NOTE]
>* <span data-ttu-id="17e7b-117">Teams no admite `CardAction` tipos no enumerados en la tabla anterior.</span><span class="sxs-lookup"><span data-stu-id="17e7b-117">Teams does not support `CardAction` types not listed in the previous table.</span></span>
>* <span data-ttu-id="17e7b-118">Teams no admite la `potentialActions` propiedad.</span><span class="sxs-lookup"><span data-stu-id="17e7b-118">Teams does not support the `potentialActions` property.</span></span>
>* <span data-ttu-id="17e7b-119">Las acciones de tarjeta son diferentes a [las acciones sugeridas](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) en Bot Framework o Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="17e7b-119">Card actions are different than [suggested actions](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) in Bot Framework or Azure Bot Service.</span></span> <span data-ttu-id="17e7b-120">Las acciones sugeridas no se admiten en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="17e7b-120">Suggested actions are not supported in Microsoft Teams.</span></span> <span data-ttu-id="17e7b-121">Si desea que los botones aparezcan en un mensaje de bot de Teams, use una tarjeta.</span><span class="sxs-lookup"><span data-stu-id="17e7b-121">If you want buttons to appear on a Teams bot message, use a card.</span></span>
>* <span data-ttu-id="17e7b-122">Si usa una acción de tarjeta como parte de una extensión de mensajería, las acciones no funcionarán hasta que la tarjeta se envíe al canal.</span><span class="sxs-lookup"><span data-stu-id="17e7b-122">If you are using a card action as part of a messaging extension, the actions do not work until the card is submitted to the channel.</span></span> <span data-ttu-id="17e7b-123">Las acciones no funcionan mientras la tarjeta está en el cuadro de redacción del mensaje.</span><span class="sxs-lookup"><span data-stu-id="17e7b-123">The actions do not work while the card is in the compose message box.</span></span>

## <a name="action-type-openurl"></a><span data-ttu-id="17e7b-124">Tipo de acción, openURL</span><span class="sxs-lookup"><span data-stu-id="17e7b-124">Action type openUrl</span></span>

<span data-ttu-id="17e7b-125">`openUrl` El tipo de acción especifica una dirección URL para iniciar en el explorador predeterminado.</span><span class="sxs-lookup"><span data-stu-id="17e7b-125">`openUrl` action type specifies a URL to launch in the default browser.</span></span>

> [!NOTE]
> <span data-ttu-id="17e7b-126">El bot no recibe ningún aviso sobre qué botón fue seleccionado.</span><span class="sxs-lookup"><span data-stu-id="17e7b-126">Your bot does not receive any notice on which button was selected.</span></span>

<span data-ttu-id="17e7b-127">Con `openUrl`, puede crear una acción con las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="17e7b-127">With `openUrl`, you can create an action with the following properties:</span></span>

| <span data-ttu-id="17e7b-128">Propiedad</span><span class="sxs-lookup"><span data-stu-id="17e7b-128">Property</span></span> | <span data-ttu-id="17e7b-129">Descripción</span><span class="sxs-lookup"><span data-stu-id="17e7b-129">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="17e7b-130">Aparece como la etiqueta del botón.</span><span class="sxs-lookup"><span data-stu-id="17e7b-130">Appears as the button label.</span></span> |
| `value` | <span data-ttu-id="17e7b-131">Este campo debe contener una dirección URL completa y con el formato correcto.</span><span class="sxs-lookup"><span data-stu-id="17e7b-131">This field must contain a full and properly formed URL.</span></span> |

# <a name="json"></a>[<span data-ttu-id="17e7b-132">JSON</span><span class="sxs-lookup"><span data-stu-id="17e7b-132">JSON</span></span>](#tab/json)

<span data-ttu-id="17e7b-133">El siguiente código muestra un ejemplo de `openUrl`un tipo de acción en JSON:</span><span class="sxs-lookup"><span data-stu-id="17e7b-133">The following code shows an example of `openUrl` action type in JSON:</span></span>

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

# <a name="c"></a>[<span data-ttu-id="17e7b-134">C#</span><span class="sxs-lookup"><span data-stu-id="17e7b-134">C#</span></span>](#tab/csharp)

<span data-ttu-id="17e7b-135">El siguiente código muestra un ejemplo de `openUrl`un tipo de acción en C#:</span><span class="sxs-lookup"><span data-stu-id="17e7b-135">The following code shows an example of `openUrl` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.OpenUrl,
    Title = "Tabs in Teams",
    Value = "https://docs.microsoft.com/en-us/microsoftteams/platform/"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="17e7b-136">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="17e7b-136">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="17e7b-137">El siguiente código muestra un ejemplo de `openUrl`un tipo de acción en JavaScript:</span><span class="sxs-lookup"><span data-stu-id="17e7b-137">The following code shows an example of `openUrl` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: 'openUrl',
    title: 'Tabs in Teams',
    value: 'https://docs.microsoft.com/en-us/microsoftteams/platform/'
}])
```

---

## <a name="action-type-messageback"></a><span data-ttu-id="17e7b-138">Tipo de acción messageBack</span><span class="sxs-lookup"><span data-stu-id="17e7b-138">Action type messageBack</span></span>

<span data-ttu-id="17e7b-139">Con `messageBack`, puede crear una acción totalmente personalizada con las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="17e7b-139">With `messageBack`, you can create a fully customized action with the following properties:</span></span>

| <span data-ttu-id="17e7b-140">Propiedad</span><span class="sxs-lookup"><span data-stu-id="17e7b-140">Property</span></span> | <span data-ttu-id="17e7b-141">Descripción</span><span class="sxs-lookup"><span data-stu-id="17e7b-141">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="17e7b-142">Aparece como la etiqueta del botón.</span><span class="sxs-lookup"><span data-stu-id="17e7b-142">Appears as the button label.</span></span> |
| `displayText` | <span data-ttu-id="17e7b-143">Opcional.</span><span class="sxs-lookup"><span data-stu-id="17e7b-143">Optional.</span></span> <span data-ttu-id="17e7b-144">Lo usa el usuario en la secuencia de chat cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="17e7b-144">Used by the user in the chat stream when the action is performed.</span></span> <span data-ttu-id="17e7b-145">Este texto no se envía al bot.</span><span class="sxs-lookup"><span data-stu-id="17e7b-145">This text is not sent to your bot.</span></span> |
| `value` | <span data-ttu-id="17e7b-146">Se envía al bot cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="17e7b-146">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="17e7b-147">Puede codificar el contexto para la acción, tales como identificadores únicos o un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="17e7b-147">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="17e7b-148">Se envía al bot cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="17e7b-148">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="17e7b-149">Use esta propiedad para simplificar el desarrollo de los bots.</span><span class="sxs-lookup"><span data-stu-id="17e7b-149">Use this property to simplify bot development.</span></span> <span data-ttu-id="17e7b-150">Su código puede comprobar una sola propiedad de nivel superior para distribuir la lógica del bot.</span><span class="sxs-lookup"><span data-stu-id="17e7b-150">Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="17e7b-151">La flexibilidad de `messageBack` significa que su código no puede dejar un mensaje de usuario visible en el historial simplemente sin usar `displayText`.</span><span class="sxs-lookup"><span data-stu-id="17e7b-151">The flexibility of `messageBack` means that your code cannot leave a visible user message in the history simply by not using `displayText`.</span></span>

# <a name="json"></a>[<span data-ttu-id="17e7b-152">JSON</span><span class="sxs-lookup"><span data-stu-id="17e7b-152">JSON</span></span>](#tab/json)

<span data-ttu-id="17e7b-153">El siguiente código muestra un ejemplo de `messageBack`un tipo de acción en JSON:</span><span class="sxs-lookup"><span data-stu-id="17e7b-153">The following code shows an example of `messageBack` action type in JSON:</span></span>

```json
{
  "buttons": [
    {
    "type": "messageBack",
    "title": "My MessageBack button",
    "displayText": "I clicked this button",
    "text": "User just clicked the MessageBack button",
    "value": "{\"property\": \"propertyValue\" }"
    }
  ]
}
```

<span data-ttu-id="17e7b-154">La propiedad `value` puede ser una cadena JSON serializada o un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="17e7b-154">The `value` property can be either a serialized JSON string or a JSON object.</span></span>

# <a name="c"></a>[<span data-ttu-id="17e7b-155">C#</span><span class="sxs-lookup"><span data-stu-id="17e7b-155">C#</span></span>](#tab/csharp)

<span data-ttu-id="17e7b-156">El siguiente código muestra un ejemplo de `messageBack`un tipo de acción en C#:</span><span class="sxs-lookup"><span data-stu-id="17e7b-156">The following code shows an example of `messageBack` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.MessageBack,
    Title = "My MessageBack button",
    DisplayText = "I clicked this button",
    Text = "User just clicked the MessageBack button",
    Value = "{\"property\": \"propertyValue\" }"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="17e7b-157">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="17e7b-157">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="17e7b-158">El siguiente código muestra un ejemplo de `messageBack`un tipo de acción en JavaScript:</span><span class="sxs-lookup"><span data-stu-id="17e7b-158">The following code shows an example of `messageBack` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: 'messageBack',
    title: "My MessageBack button",
    displayText: "I clicked this button",
    text: "User just clicked the MessageBack button",
    value: {property: "propertyValue" }
}])
```

---

### <a name="inbound-message-example"></a><span data-ttu-id="17e7b-159">Ejemplo de un mensaje entrante</span><span class="sxs-lookup"><span data-stu-id="17e7b-159">Inbound message example</span></span>

<span data-ttu-id="17e7b-160">`replyToId` contiene el id. del mensaje del que proviene la acción de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="17e7b-160">`replyToId` contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="17e7b-161">Úselo si desea actualizar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="17e7b-161">Use it if you want to update the message.</span></span>

<span data-ttu-id="17e7b-162">El siguiente código muestra un ejemplo de un mensaje entrante:</span><span class="sxs-lookup"><span data-stu-id="17e7b-162">The following code shows an example of inbound message:</span></span>

```json
{
   "text":"User just clicked the MessageBack button",
   "value":{
      "property":"propertyValue"
   },
   "type":"message",
   "timestamp":"2017-06-22T22:38:47.407Z",
   "id":"f:5261769396935243054",
   "channelId":"msteams",
   "serviceUrl":"https://smba.trafficmanager.net/amer-client-ss.msg/",
   "from":{
      "id":"29:102jd210jd010icsoaeclaejcoa9ue09u",
      "name":"John Smith"
   },
   "conversation":{
      "id":"19:malejcou081i20ojmlcau0@thread.skype;messageid=1498171086622"
   },
   "recipient":{
      "id":"28:76096e45-119f-4736-859c-6dfff54395f7",
      "name":"MyBot"
   },
   "entities":[
      {
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo" 
      }
   ],
   "channelData":{
      "channel":{
         "id":"19:malejcou081i20ojmlcau0@thread.skype"
      },
      "team":{
         "id":"19:12d021jdoijsaeoaue0u@thread.skype"
      },
      "tenant":{
         "id":"bec8e231-67ad-484e-87f4-3e5438390a77"
      }
   },
        "replyToId": "1575667808184",
}
```

## <a name="action-type-imback"></a><span data-ttu-id="17e7b-163">Tipo de acción imBack</span><span class="sxs-lookup"><span data-stu-id="17e7b-163">Action type imBack</span></span>

<span data-ttu-id="17e7b-164">La acción `imBack` desencadena un mensaje de devolución su bot, como si el usuario lo hubiera escrito en un mensaje de chat normal.</span><span class="sxs-lookup"><span data-stu-id="17e7b-164">The `imBack` action triggers a return message to your bot, as if the user typed it in a normal chat message.</span></span> <span data-ttu-id="17e7b-165">Sul usuario y todos los demás usuarios de un canal pueden ver el botón de respuesta.</span><span class="sxs-lookup"><span data-stu-id="17e7b-165">Your user and all other users in a channel can see the button response.</span></span>

<span data-ttu-id="17e7b-166">Con `imBack`, puede crear una acción con las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="17e7b-166">With `imBack`, you can create an action with the following properties:</span></span>

| <span data-ttu-id="17e7b-167">Propiedad</span><span class="sxs-lookup"><span data-stu-id="17e7b-167">Property</span></span> | <span data-ttu-id="17e7b-168">Descripción</span><span class="sxs-lookup"><span data-stu-id="17e7b-168">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="17e7b-169">Aparece como la etiqueta del botón.</span><span class="sxs-lookup"><span data-stu-id="17e7b-169">Appears as the button label.</span></span> |
| `value` | <span data-ttu-id="17e7b-170">Este campo debe contener la cadena de texto que se usa en el chat y, por tanto, se envía al bot.</span><span class="sxs-lookup"><span data-stu-id="17e7b-170">This field must contain the text string used in the chat and therefore sent back to the bot.</span></span> <span data-ttu-id="17e7b-171">Este es el texto del mensaje que se procesa en su bot para realizar la lógica deseada.</span><span class="sxs-lookup"><span data-stu-id="17e7b-171">This is the message text you process in your bot to perform the desired logic.</span></span> |

> [!NOTE]
> <span data-ttu-id="17e7b-172">El campo `value` es una cadena simple.</span><span class="sxs-lookup"><span data-stu-id="17e7b-172">The `value` field is a simple string.</span></span> <span data-ttu-id="17e7b-173">No se admite el formato ni los caracteres ocultos.</span><span class="sxs-lookup"><span data-stu-id="17e7b-173">There is no support for formatting or hidden characters.</span></span>

# <a name="json"></a>[<span data-ttu-id="17e7b-174">JSON</span><span class="sxs-lookup"><span data-stu-id="17e7b-174">JSON</span></span>](#tab/json)

<span data-ttu-id="17e7b-175">El siguiente código muestra un ejemplo de `imBack`un tipo de acción en JSON:</span><span class="sxs-lookup"><span data-stu-id="17e7b-175">The following code shows an example of `imBack` action type in JSON:</span></span>

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

# <a name="c"></a>[<span data-ttu-id="17e7b-176">C#</span><span class="sxs-lookup"><span data-stu-id="17e7b-176">C#</span></span>](#tab/csharp)

<span data-ttu-id="17e7b-177">El siguiente código muestra un ejemplo de `imBack`un tipo de acción en C#:</span><span class="sxs-lookup"><span data-stu-id="17e7b-177">The following code shows an example of `imBack` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.ImBack,
    Title = "More",
    Value = "Show me more"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="17e7b-178">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="17e7b-178">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="17e7b-179">El siguiente código muestra un ejemplo de `imBack`un tipo de acción en JavaScript:</span><span class="sxs-lookup"><span data-stu-id="17e7b-179">The following code shows an example of `imBack` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: "imBack",
    title: "More",
    value: "Show me more"
}])
```

---

## <a name="action-type-invoke"></a><span data-ttu-id="17e7b-180">Tipo de acción invoke</span><span class="sxs-lookup"><span data-stu-id="17e7b-180">Action type invoke</span></span>

<span data-ttu-id="17e7b-181">La acción `invoke` se usa para invocar [módulos de tareas](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span><span class="sxs-lookup"><span data-stu-id="17e7b-181">The `invoke` action is used for invoking [task modules](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="17e7b-182">La acción `invoke` contiene tres propiedades, `type`, `title`y `value`.</span><span class="sxs-lookup"><span data-stu-id="17e7b-182">The `invoke` action contains three properties, `type`, `title`, and `value`.</span></span>

<span data-ttu-id="17e7b-183">Con `invoke`, puede crear una acción con las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="17e7b-183">With `invoke`, you can create an action with the following properties:</span></span>

| <span data-ttu-id="17e7b-184">Propiedad</span><span class="sxs-lookup"><span data-stu-id="17e7b-184">Property</span></span> | <span data-ttu-id="17e7b-185">Descripción</span><span class="sxs-lookup"><span data-stu-id="17e7b-185">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="17e7b-186">Aparece como la etiqueta del botón.</span><span class="sxs-lookup"><span data-stu-id="17e7b-186">Appears as the button label.</span></span> |
| `value` | <span data-ttu-id="17e7b-187">Esta propiedad puede contener una cadena, un objeto JSON con cadenas o un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="17e7b-187">This property can contain a string, a stringified JSON object, or a JSON object.</span></span> |

# <a name="json"></a>[<span data-ttu-id="17e7b-188">JSON</span><span class="sxs-lookup"><span data-stu-id="17e7b-188">JSON</span></span>](#tab/json)

<span data-ttu-id="17e7b-189">El siguiente código muestra un ejemplo de `invoke`un tipo de acción en JSON:</span><span class="sxs-lookup"><span data-stu-id="17e7b-189">The following code shows an example of `invoke` action type in JSON:</span></span>

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

<span data-ttu-id="17e7b-190">Cuando un usuario selecciona el botón, su bot recibe el objeto `value` con información adicional.</span><span class="sxs-lookup"><span data-stu-id="17e7b-190">When a user selects the button, your bot receives the `value` object with some additional information.</span></span>

> [!NOTE]
> <span data-ttu-id="17e7b-191">El tipo de actividad es `invoke` en lugar de `message` que es `activity.Type == "invoke"`.</span><span class="sxs-lookup"><span data-stu-id="17e7b-191">The activity type is `invoke` instead of `message` that is `activity.Type == "invoke"`.</span></span>

# <a name="c"></a>[<span data-ttu-id="17e7b-192">C#</span><span class="sxs-lookup"><span data-stu-id="17e7b-192">C#</span></span>](#tab/csharp)

<span data-ttu-id="17e7b-193">El siguiente código muestra un ejemplo de `invoke`un tipo de acción en C#:</span><span class="sxs-lookup"><span data-stu-id="17e7b-193">The following code shows an example of `invoke` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="17e7b-194">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="17e7b-194">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="17e7b-195">El siguiente código muestra un ejemplo de `invoke`un tipo de acción Node.js:</span><span class="sxs-lookup"><span data-stu-id="17e7b-195">The following code shows an example of `invoke` action type in Node.js:</span></span>

```javascript
CardFactory.actions([
{
    type: "invoke",
    title: "Option 1",
    value: {
        option: "opt1"
    }
}])
```

---

### <a name="example-of-incoming-invoke-message"></a><span data-ttu-id="17e7b-196">Ejemplo de mensaje de invocación entrante</span><span class="sxs-lookup"><span data-stu-id="17e7b-196">Example of incoming invoke message</span></span>

<span data-ttu-id="17e7b-197">La propiedad del nível superiror`replyToId` contiene el id. del mensaje del cual proviene la acción de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="17e7b-197">The top-level `replyToId` property contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="17e7b-198">Úselo si desea actualizar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="17e7b-198">Use it if you want to update the message.</span></span>

<span data-ttu-id="17e7b-199">El siguiente código muestra un ejemplo de un mensaje de invocación entrante:</span><span class="sxs-lookup"><span data-stu-id="17e7b-199">The following code shows an example of incoming invoke message:</span></span>

```json
{
    "type": "invoke",
    "value": {
        "option": "opt1"
    },
    "timestamp": "2017-02-10T04:11:19.614Z",
    "localTimestamp": "2017-02-09T21:11:19.614-07:00",
    "id": "f:6894910862892785420",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1Eniglq0-uVL83xNB9GU6w_G5a4SZF0gcJLprZzhtEbel21G_5h-
    NgoprRw45mP0AXUIZVeqrsIHSYV4ntgfVJQ",
        "name": "John Doe"
    },
    "conversation": {
        "id": "19:97b1ec61-45bf-453c-9059-6e8984e0cef4_8d88f59b-ae61-4300-bec0-caace7d28446@unq.gbl.spaces"
    },
    "recipient": {
        "id": "28:8d88f59b-ae61-4300-bec0-caace7d28446",
        "name": "MyBot"
    },
    "entities": [
        {
            "locale": "en-US",
            "country": "US",
            "platform": "Web",
            "type": "clientInfo"
        }
    ],
    "channelData": {
        "channel": {
            "id": "19:dc5ba12695be4eb7bf457cad6b4709eb@thread.skype"
        },
        "team": {
            "id": "19:712c61d0ef384e5fa681ba90ca943398@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184"
}
```

## <a name="action-type-signin"></a><span data-ttu-id="17e7b-200">Tipo de acción signin</span><span class="sxs-lookup"><span data-stu-id="17e7b-200">Action type signin</span></span>

<span data-ttu-id="17e7b-201">`signin` El tipo de acción inicia un flujo de OAuth que permite a los bots conectarse con servicios seguros.</span><span class="sxs-lookup"><span data-stu-id="17e7b-201">`signin` action type initiates an OAuth flow that permits bots to connect with secure services.</span></span> <span data-ttu-id="17e7b-202">Para más información, consulte [flujos de autenticación en bots](~/bots/how-to/authentication/auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="17e7b-202">For more information, see [authentication flow in bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

<span data-ttu-id="17e7b-203">Teams también admite[acciones de tarjetas adaptables](#adaptive-cards-actions) que solo usan las tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="17e7b-203">Teams also supports [Adaptive Cards actions](#adaptive-cards-actions) that are only used by Adaptive Cards.</span></span>

# <a name="json"></a>[<span data-ttu-id="17e7b-204">JSON</span><span class="sxs-lookup"><span data-stu-id="17e7b-204">JSON</span></span>](#tab/json)

<span data-ttu-id="17e7b-205">El siguiente código muestra un ejemplo de `signin`un tipo de acción en JSON:</span><span class="sxs-lookup"><span data-stu-id="17e7b-205">The following code shows an example of `signin` action type in JSON:</span></span>

```json
{
"type": "signin",
"title": "Click me for signin",
"value": "https://signin.com"
}
```

# <a name="c"></a>[<span data-ttu-id="17e7b-206">C#</span><span class="sxs-lookup"><span data-stu-id="17e7b-206">C#</span></span>](#tab/csharp)

<span data-ttu-id="17e7b-207">El siguiente código muestra un ejemplo de `signin`un tipo de acción en C#:</span><span class="sxs-lookup"><span data-stu-id="17e7b-207">The following code shows an example of `signin` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.Signin,
    Title = "Click me for signin",
    Value = "https://signin.com"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="17e7b-208">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="17e7b-208">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="17e7b-209">El siguiente código muestra un ejemplo de `signin`un tipo de acción en JavaScript:</span><span class="sxs-lookup"><span data-stu-id="17e7b-209">The following code shows an example of `signin` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: "signin",
    title: "Click me for signin",
    value: "https://signin.com"
}])
```

---

## <a name="adaptive-cards-actions"></a><span data-ttu-id="17e7b-210">Acciones de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="17e7b-210">Adaptive Cards actions</span></span>

<span data-ttu-id="17e7b-211">Las arjetas adaptables admiten cuatro tipos de acción:</span><span class="sxs-lookup"><span data-stu-id="17e7b-211">Adaptive Cards support four action types:</span></span>

* [<span data-ttu-id="17e7b-212">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="17e7b-212">Action.OpenUrl</span></span>](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [<span data-ttu-id="17e7b-213">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="17e7b-213">Action.Submit</span></span>](http://adaptivecards.io/explorer/Action.Submit.html)
* [<span data-ttu-id="17e7b-214">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="17e7b-214">Action.ShowCard</span></span>](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [<span data-ttu-id="17e7b-215">Action.Execute</span><span class="sxs-lookup"><span data-stu-id="17e7b-215">Action.Execute</span></span>](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

<span data-ttu-id="17e7b-216">También puede modificar la carga `Action.Submit` de la tarjeta adaptable para admitir acciones de Bot Framework existentes mediante una`msteams`propiedad en el`data` objeto de `Action.Submit`.</span><span class="sxs-lookup"><span data-stu-id="17e7b-216">You can also modify the Adaptive Card `Action.Submit` payload to support existing Bot Framework actions using an `msteams` property in the `data` object of `Action.Submit`.</span></span> <span data-ttu-id="17e7b-217">En la siguiente sección se proporcionan detalles sobre cómo usar las acciones de Bot Framework existentes con tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="17e7b-217">The next section provide details on how to use existing Bot Framework actions with Adaptive Cards.</span></span>

> [!NOTE]
> <span data-ttu-id="17e7b-218">Agregar `msteams` a los datos con una acción Bot Framework no funciona con un módulo de tareas de una tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="17e7b-218">Adding `msteams` to data with a Bot Framework action does not work with an Adaptive Card task module.</span></span>

### <a name="adaptive-cards-with-messageback-action"></a><span data-ttu-id="17e7b-219">Tarjetas adaptables con la acción messageBack</span><span class="sxs-lookup"><span data-stu-id="17e7b-219">Adaptive Cards with messageBack action</span></span>

<span data-ttu-id="17e7b-220">Para incluir una acción `messageBack` con una tarjeta adaptable, incluya los detalles siguientes en el`msteams`objeto :</span><span class="sxs-lookup"><span data-stu-id="17e7b-220">To include a `messageBack` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="17e7b-221">Puede incluir propiedades ocultas adicionales en el objeto `data`, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="17e7b-221">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="17e7b-222">Propiedad</span><span class="sxs-lookup"><span data-stu-id="17e7b-222">Property</span></span> | <span data-ttu-id="17e7b-223">Descripción</span><span class="sxs-lookup"><span data-stu-id="17e7b-223">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="17e7b-224">Establecer a`messageBack`.</span><span class="sxs-lookup"><span data-stu-id="17e7b-224">Set to `messageBack`.</span></span> |
| `displayText` | <span data-ttu-id="17e7b-225">Opcional.</span><span class="sxs-lookup"><span data-stu-id="17e7b-225">Optional.</span></span> <span data-ttu-id="17e7b-226">Lo usa el usuario en la secuencia de chat cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="17e7b-226">Used by the user in the chat stream when the action is performed.</span></span> <span data-ttu-id="17e7b-227">Este texto no se envía al bot.</span><span class="sxs-lookup"><span data-stu-id="17e7b-227">This text is not sent to your bot.</span></span> |
| `value` | <span data-ttu-id="17e7b-228">Se envía al bot cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="17e7b-228">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="17e7b-229">Puede codificar el contexto para la acción, tales como identificadores únicos o un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="17e7b-229">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="17e7b-230">Se envía al bot cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="17e7b-230">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="17e7b-231">Use esta propiedad para simplificar el desarrollo de los bots.</span><span class="sxs-lookup"><span data-stu-id="17e7b-231">Use this property to simplify bot development.</span></span> <span data-ttu-id="17e7b-232">Su código puede comprobar una sola propiedad de nivel superior para distribuir la lógica del bot.</span><span class="sxs-lookup"><span data-stu-id="17e7b-232">Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="17e7b-233">El siguiente código muestra un ejemplo de tarjetas adaptables `messageBack`con la acción:</span><span class="sxs-lookup"><span data-stu-id="17e7b-233">The following code shows an example of Adaptive Cards with `messageBack` action:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "Click me for messageBack",
  "data": {
    "msteams": {
        "type": "messageBack",
        "displayText": "I clicked this button",
        "text": "text to bots",
        "value": "{\"bfKey\": \"bfVal\", \"conflictKey\": \"from value\"}"
    }
  }
}
```

### <a name="adaptive-cards-with-imback-action"></a><span data-ttu-id="17e7b-234">Tarjetas adaptables con la acción imBack</span><span class="sxs-lookup"><span data-stu-id="17e7b-234">Adaptive Cards with imBack action</span></span>

<span data-ttu-id="17e7b-235">Para incluir una acción `imBack` con una tarjeta adaptable, incluya los detalles siguientes en el`msteams`objeto :</span><span class="sxs-lookup"><span data-stu-id="17e7b-235">To include an `imBack` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="17e7b-236">Puede incluir propiedades ocultas adicionales en el objeto `data`, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="17e7b-236">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="17e7b-237">Propiedad</span><span class="sxs-lookup"><span data-stu-id="17e7b-237">Property</span></span> | <span data-ttu-id="17e7b-238">Descripción</span><span class="sxs-lookup"><span data-stu-id="17e7b-238">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="17e7b-239">Establecer a`imBack`.</span><span class="sxs-lookup"><span data-stu-id="17e7b-239">Set to `imBack`.</span></span> |
| `value` | <span data-ttu-id="17e7b-240">Cadena que debe repetirse en el chat.</span><span class="sxs-lookup"><span data-stu-id="17e7b-240">String that needs to be echoed back in the chat.</span></span> |

<span data-ttu-id="17e7b-241">El siguiente código muestra un ejemplo de tarjetas adaptables `imBack`con la acción:</span><span class="sxs-lookup"><span data-stu-id="17e7b-241">The following code shows an example of Adaptive Cards with `imBack` action:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "Click me for imBack",
  "data": {
    "msteams": {
        "type": "imBack",
        "value": "Text to reply in chat"
    }
  }
}
```

### <a name="adaptive-cards-with-signin-action"></a><span data-ttu-id="17e7b-242">Tarjetas adaptables con la acción signin</span><span class="sxs-lookup"><span data-stu-id="17e7b-242">Adaptive Cards with signin action</span></span>

<span data-ttu-id="17e7b-243">Para incluir una acción `signin` con una tarjeta adaptable, incluya los detalles siguientes en el`msteams`objeto :</span><span class="sxs-lookup"><span data-stu-id="17e7b-243">To include a `signin` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="17e7b-244">Puede incluir propiedades ocultas adicionales en el objeto `data`, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="17e7b-244">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="17e7b-245">Propiedad</span><span class="sxs-lookup"><span data-stu-id="17e7b-245">Property</span></span> | <span data-ttu-id="17e7b-246">Descripción</span><span class="sxs-lookup"><span data-stu-id="17e7b-246">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="17e7b-247">Establecer a`signin`.</span><span class="sxs-lookup"><span data-stu-id="17e7b-247">Set to `signin`.</span></span> |
| `value` | <span data-ttu-id="17e7b-248">Establézcala en la dirección URL a la que desea redirigir.</span><span class="sxs-lookup"><span data-stu-id="17e7b-248">Set to the URL where you want to redirect.</span></span>  |

<span data-ttu-id="17e7b-249">El siguiente código muestra un ejemplo de tarjetas adaptables `signin`con la acción:</span><span class="sxs-lookup"><span data-stu-id="17e7b-249">The following code shows an example of Adaptive Cards with `signin` action:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "Click me for signin",
  "data": {
    "msteams": {
        "type": "signin",
        "value": "https://signin.com"
    }
  }
}
```

### <a name="adaptive-cards-with-invoke-action"></a><span data-ttu-id="17e7b-250">Tarjetas adaptables con la acción invoke</span><span class="sxs-lookup"><span data-stu-id="17e7b-250">Adaptive Cards with invoke action</span></span>

<span data-ttu-id="17e7b-251">Para incluir una acción `invoke` con una tarjeta adaptable, incluya los detalles siguientes en el`msteams`objeto :</span><span class="sxs-lookup"><span data-stu-id="17e7b-251">To include an `invoke` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="17e7b-252">Puede incluir propiedades ocultas adicionales en el objeto `data`, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="17e7b-252">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="17e7b-253">Propiedad</span><span class="sxs-lookup"><span data-stu-id="17e7b-253">Property</span></span> | <span data-ttu-id="17e7b-254">Descripción</span><span class="sxs-lookup"><span data-stu-id="17e7b-254">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="17e7b-255">Establecer a`task/fetch`.</span><span class="sxs-lookup"><span data-stu-id="17e7b-255">Set to `task/fetch`.</span></span> |
| `data` | <span data-ttu-id="17e7b-256">Establezca el valor.</span><span class="sxs-lookup"><span data-stu-id="17e7b-256">Set the value.</span></span>  |

<span data-ttu-id="17e7b-257">El siguiente código muestra un ejemplo de tarjetas adaptables `invoke`con la acción:</span><span class="sxs-lookup"><span data-stu-id="17e7b-257">The following code shows an example of Adaptive Cards with `invoke` action:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "submit",
  "data": {
    "msteams": {
        "type": "task/fetch"
    }
  }
}
```

<span data-ttu-id="17e7b-258">El siguiente código muestra un ejemplo de tarjetas adaptables `invoke`con la acción con datos de carga adicionales:</span><span class="sxs-lookup"><span data-stu-id="17e7b-258">The following code shows an example of Adaptive Cards with `invoke` action with additional payload data:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "submit"
  "data": {
    "msteams": {
        "type": "task/fetch"
    },
    "Value1": "some value"
  }
}
```

## <a name="see-also"></a><span data-ttu-id="17e7b-259">Consulte también</span><span class="sxs-lookup"><span data-stu-id="17e7b-259">See also</span></span>

[<span data-ttu-id="17e7b-260">Referencia de tarjetas</span><span class="sxs-lookup"><span data-stu-id="17e7b-260">Cards reference</span></span>](./cards-reference.md)

## <a name="next-step"></a><span data-ttu-id="17e7b-261">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="17e7b-261">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="17e7b-262">Acciones universales para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="17e7b-262">Universal Actions for Adaptive Cards</span></span>](../cards/Universal-actions-for-adaptive-cards/Overview.md)

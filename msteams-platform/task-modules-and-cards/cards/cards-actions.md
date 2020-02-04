---
title: Agregar acciones de tarjeta en un bot
description: Describe las acciones de tarjeta en Microsoft Teams y cómo usarlas en los bots.
keywords: acciones de las tarjetas de los equipos bots
ms.openlocfilehash: e0b050cde9adf5bd811d5d95ce1c6f1bf60546a1
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675916"
---
# <a name="card-actions"></a><span data-ttu-id="28925-104">Acciones de tarjeta</span><span class="sxs-lookup"><span data-stu-id="28925-104">Card actions</span></span>

<span data-ttu-id="28925-105">Las tarjetas que usan los bots y las extensiones de mensajería de Microsoft Teams son compatibles con los siguientes tipos de actividad ([`CardAction`](https://docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards)).</span><span class="sxs-lookup"><span data-stu-id="28925-105">Cards used by bots and messaging extensions in Teams support the following activity ([`CardAction`](https://docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards)) types.</span></span> <span data-ttu-id="28925-106">Tenga en cuenta que estas acciones `potentialActions` difieren de las tarjetas conector de Office 365 cuando se usan desde conectores.</span><span class="sxs-lookup"><span data-stu-id="28925-106">Note that these actions differ from `potentialActions` for Office 365 Connector cards when used from Connectors.</span></span>

| <span data-ttu-id="28925-107">Tipo</span><span class="sxs-lookup"><span data-stu-id="28925-107">Type</span></span> | <span data-ttu-id="28925-108">Action</span><span class="sxs-lookup"><span data-stu-id="28925-108">Action</span></span> |
| --- | --- |
| `openUrl` | <span data-ttu-id="28925-109">Abre una dirección URL en el explorador predeterminado.</span><span class="sxs-lookup"><span data-stu-id="28925-109">Opens a URL in the default browser.</span></span> |
| `messageBack` | <span data-ttu-id="28925-110">Envía un mensaje y una carga al bot (del usuario que hizo clic en el botón o ahusado la tarjeta) y envía un mensaje independiente al flujo de chat.</span><span class="sxs-lookup"><span data-stu-id="28925-110">Sends a message and payload to the bot (from the user who clicked the button or tapped the card) and sends a separate message to the chat stream.</span></span> |
| `imBack`| <span data-ttu-id="28925-111">Envía un mensaje al bot (del usuario que hizo clic en el botón o ahusado la tarjeta).</span><span class="sxs-lookup"><span data-stu-id="28925-111">Sends a message to the bot (from the user who clicked the button or tapped the card).</span></span> <span data-ttu-id="28925-112">Este mensaje (de usuario a bot) es visible para todos los participantes de la conversación.</span><span class="sxs-lookup"><span data-stu-id="28925-112">This message (from user to bot) is visible to all conversation participants.</span></span> |
| `invoke` | <span data-ttu-id="28925-113">Envía un mensaje y una carga al bot (del usuario que hizo clic en el botón o ahusado la tarjeta).</span><span class="sxs-lookup"><span data-stu-id="28925-113">Sends a message and payload to the bot (from the user who clicked the button or tapped the card).</span></span> <span data-ttu-id="28925-114">Este mensaje no es visible.</span><span class="sxs-lookup"><span data-stu-id="28925-114">This message is not visible.</span></span> |
| `signin` | <span data-ttu-id="28925-115">Inicia el flujo de OAuth y permite que los bots se conecten con los servicios seguros.</span><span class="sxs-lookup"><span data-stu-id="28925-115">Initiates OAuth flow, allowing bots to connect with secure services.</span></span> |

> [!NOTE]
>* <span data-ttu-id="28925-116">Teams no admite `CardAction` tipos que no aparecen en la tabla anterior.</span><span class="sxs-lookup"><span data-stu-id="28925-116">Teams does not support `CardAction` types not listed in the preceding table.</span></span>
>* <span data-ttu-id="28925-117">Teams no admite la `potentialActions` propiedad.</span><span class="sxs-lookup"><span data-stu-id="28925-117">Teams does not support the `potentialActions` property.</span></span>
>* <span data-ttu-id="28925-118">Las acciones de tarjeta son diferentes de [las acciones sugeridas](https://docs.microsoft.com/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button) en el servicio de bot Framework/Azure bot.</span><span class="sxs-lookup"><span data-stu-id="28925-118">Card actions are different than [suggested actions](https://docs.microsoft.com/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button) in Bot Framework/Azure Bot Service.</span></span> <span data-ttu-id="28925-119">Las acciones sugeridas no son compatibles con Microsoft Teams: Si desea que aparezcan botones en un mensaje de bot de Teams, use una tarjeta.</span><span class="sxs-lookup"><span data-stu-id="28925-119">Suggested actions are not supported in Microsoft Teams: if you want buttons to appear on a Teams bot message, use a card.</span></span>
>* <span data-ttu-id="28925-120">Si está usando una acción de tarjeta como parte de una extensión de mensajería, las acciones no funcionarán hasta que la tarjeta se envíe al canal (no funcionarán mientras la tarjeta se encuentra en el cuadro de mensaje de redacción).</span><span class="sxs-lookup"><span data-stu-id="28925-120">If you're using a card action as part of a messaging extension, the actions will be not work until the card is submitted to the channel (they will not work while the card is in the compose message box).</span></span>

<span data-ttu-id="28925-121">Teams también admite [acciones de tarjetas adaptables](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions), que solo se usan en tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="28925-121">Teams also supports [Adaptive Cards actions](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions), which are only used by Adaptive Cards.</span></span> <span data-ttu-id="28925-122">Estas acciones se enumeran en su propia sección al final de esta referencia.</span><span class="sxs-lookup"><span data-stu-id="28925-122">These actions are listed in their own section at the end of this reference.</span></span>

## <a name="openurl"></a><span data-ttu-id="28925-123">openUrl</span><span class="sxs-lookup"><span data-stu-id="28925-123">openUrl</span></span>

<span data-ttu-id="28925-124">Este tipo de acción especifica una dirección URL que se iniciará en el explorador predeterminado.</span><span class="sxs-lookup"><span data-stu-id="28925-124">This action type specifies a URL to launch in the default browser.</span></span> <span data-ttu-id="28925-125">Tenga en cuenta que el bot no recibe ningún aviso en el botón en el que se hizo clic.</span><span class="sxs-lookup"><span data-stu-id="28925-125">Note that your bot does not receive any notice on which button was clicked.</span></span>

<span data-ttu-id="28925-126">El `value` campo debe contener una dirección URL completa y con formato correcto.</span><span class="sxs-lookup"><span data-stu-id="28925-126">The `value` field must contain a full and properly formed URL.</span></span>

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a><span data-ttu-id="28925-127">messageBack</span><span class="sxs-lookup"><span data-stu-id="28925-127">messageBack</span></span>

<span data-ttu-id="28925-128">Con `messageBack`, puede crear una acción completamente personalizada con las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="28925-128">With `messageBack`, you can create a fully customized action with the following properties:</span></span>

| <span data-ttu-id="28925-129">Propiedad</span><span class="sxs-lookup"><span data-stu-id="28925-129">Property</span></span> | <span data-ttu-id="28925-130">Descripción</span><span class="sxs-lookup"><span data-stu-id="28925-130">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="28925-131">Aparece como etiqueta del botón.</span><span class="sxs-lookup"><span data-stu-id="28925-131">Appears as the button label.</span></span> |
| `displayText` | <span data-ttu-id="28925-132">Opcional.</span><span class="sxs-lookup"><span data-stu-id="28925-132">Optional.</span></span> <span data-ttu-id="28925-133">El usuario los repite en la secuencia de chat cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="28925-133">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="28925-134">Este texto *no* se envía a su bot.</span><span class="sxs-lookup"><span data-stu-id="28925-134">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="28925-135">Se envía a su bot cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="28925-135">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="28925-136">Puede codificar el contexto de la acción, como identificadores únicos o un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="28925-136">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="28925-137">Se envía a su bot cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="28925-137">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="28925-138">Use esta propiedad para simplificar el desarrollo de los robots: el código puede comprobar una única propiedad de nivel superior para enviar la lógica del bot.</span><span class="sxs-lookup"><span data-stu-id="28925-138">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="28925-139">La flexibilidad de `messageBack` significa que el código puede elegir no dejar un mensaje de usuario visible en el historial simplemente por no usar `displayText`.</span><span class="sxs-lookup"><span data-stu-id="28925-139">The flexibility of `messageBack` means that your code can choose not to leave a visible user message in the history simply by not using `displayText`.</span></span>

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

<span data-ttu-id="28925-140">La `value` propiedad puede ser una cadena JSON serializada o un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="28925-140">The `value` property can be either a serialized JSON string or a JSON object.</span></span>

### <a name="inbound-message-example"></a><span data-ttu-id="28925-141">Ejemplo de mensaje entrante</span><span class="sxs-lookup"><span data-stu-id="28925-141">Inbound message example</span></span>

<span data-ttu-id="28925-142">`replyToId`contiene el identificador del mensaje del que procedía la acción de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="28925-142">`replyToId` contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="28925-143">Úselo si desea actualizar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="28925-143">Use it if you want to update the message.</span></span>

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

## <a name="imback"></a><span data-ttu-id="28925-144">retroceder</span><span class="sxs-lookup"><span data-stu-id="28925-144">imBack</span></span>

<span data-ttu-id="28925-145">Esta acción desencadena un mensaje de vuelta al bot, como si el usuario lo hubiera escrito en un mensaje de chat normal.</span><span class="sxs-lookup"><span data-stu-id="28925-145">This action triggers a return message to your bot, as if the user typed it in a normal chat message.</span></span> <span data-ttu-id="28925-146">El usuario, y todos los demás usuarios en un canal, verán la respuesta del botón.</span><span class="sxs-lookup"><span data-stu-id="28925-146">Your user, and all other users if in a channel, will see that button response.</span></span>

<span data-ttu-id="28925-147">El `value` campo debe contener la cadena de texto que se mostrará en el chat y, por lo tanto, volver a enviarla al bot.</span><span class="sxs-lookup"><span data-stu-id="28925-147">The `value` field should contain the text string echoed in the chat and therefore sent back to the bot.</span></span> <span data-ttu-id="28925-148">Este es el texto del mensaje que se procesará en el bot para realizar la lógica deseada.</span><span class="sxs-lookup"><span data-stu-id="28925-148">This is the message text you will process in your bot to perform the desired logic.</span></span> <span data-ttu-id="28925-149">Nota: este campo es una cadena sencilla: no se admite el formato ni los caracteres ocultos.</span><span class="sxs-lookup"><span data-stu-id="28925-149">Note: this field is a simple string - there is no support for formatting or hidden characters.</span></span>

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a><span data-ttu-id="28925-150">ejecuta</span><span class="sxs-lookup"><span data-stu-id="28925-150">invoke</span></span>

<span data-ttu-id="28925-151">La `invoke` acción se usa para invocar [módulos de tareas](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span><span class="sxs-lookup"><span data-stu-id="28925-151">The `invoke` action is used for invoking [task modules](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="28925-152">La `invoke` acción contiene tres propiedades: `type`, `title`y `value`.</span><span class="sxs-lookup"><span data-stu-id="28925-152">The `invoke` action contains three properties: `type`, `title`, and `value`.</span></span> <span data-ttu-id="28925-153">La `value` propiedad puede contener una cadena, un objeto JSON stringified o un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="28925-153">The `value` property can contain a string, a stringified JSON object, or a JSON object.</span></span>

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

<span data-ttu-id="28925-154">Cuando un usuario hace clic en el botón, el bot recibirá `value` el objeto con alguna información adicional.</span><span class="sxs-lookup"><span data-stu-id="28925-154">When a user clicks the button, your bot will receive the `value` object with some additional info.</span></span> <span data-ttu-id="28925-155">Tenga en cuenta que el tipo `invoke` de actividad será en lugar `message` de`activity.Type == "invoke"`().</span><span class="sxs-lookup"><span data-stu-id="28925-155">Please note that the activity type will be `invoke` instead of `message` (`activity.Type == "invoke"`).</span></span>

### <a name="example-invoke-button-definition-net"></a><span data-ttu-id="28925-156">Ejemplo: Invoke Button Definition (.NET)</span><span class="sxs-lookup"><span data-stu-id="28925-156">Example: Invoke button definition (.NET)</span></span>

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a><span data-ttu-id="28925-157">Ejemplo: mensaje de invocación entrante</span><span class="sxs-lookup"><span data-stu-id="28925-157">Example: Incoming invoke message</span></span>

<span data-ttu-id="28925-158">La propiedad de nivel `replyToId` superior contiene el identificador del mensaje de la que proviene la acción de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="28925-158">The top-level `replyToId` property contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="28925-159">Úselo si desea actualizar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="28925-159">Use it if you want to update the message.</span></span>

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

## <a name="signin"></a><span data-ttu-id="28925-160">signin</span><span class="sxs-lookup"><span data-stu-id="28925-160">signin</span></span>

<span data-ttu-id="28925-161">Inicia un flujo de OAuth, lo que permite que los bots se conecten a servicios seguros, tal como se describe aquí más detalladamente: [flujo de autenticación en bots](~/bots/how-to/authentication/auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="28925-161">Initiates an OAuth flow, allowing bots to connect with secure services, as described in more detail here: [Authentication flow in bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

## <a name="adaptive-cards-actions"></a><span data-ttu-id="28925-162">Acciones de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="28925-162">Adaptive Cards actions</span></span>

<span data-ttu-id="28925-163">Las tarjetas adaptables admiten tres tipos de acciones:</span><span class="sxs-lookup"><span data-stu-id="28925-163">Adaptive Cards support three action types:</span></span>

* [<span data-ttu-id="28925-164">Action. OpenUrl</span><span class="sxs-lookup"><span data-stu-id="28925-164">Action.OpenUrl</span></span>](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [<span data-ttu-id="28925-165">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="28925-165">Action.Submit</span></span>](http://adaptivecards.io/explorer/Action.Submit.html)
* [<span data-ttu-id="28925-166">Action. ShowCard</span><span class="sxs-lookup"><span data-stu-id="28925-166">Action.ShowCard</span></span>](http://adaptivecards.io/explorer/Action.ShowCard.html)

<span data-ttu-id="28925-167">Además de las acciones mencionadas anteriormente, puede modificar la carga de la `Action.Submit` tarjeta adaptable para admitir acciones de bot Framework `msteams` existentes con una `data` propiedad en `Action.Submit`el objeto de.</span><span class="sxs-lookup"><span data-stu-id="28925-167">In addition to the actions mentioned above, you can modify the Adaptive Card `Action.Submit` payload to support existing Bot Framework actions using a `msteams` property in the `data` object of `Action.Submit`.</span></span> <span data-ttu-id="28925-168">Las secciones siguientes explican cómo usar las acciones de bot Framework existentes con tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="28925-168">The below sections detail how to use existing Bot Framework actions with Adaptive Cards.</span></span>

### <a name="adaptive-cards-with-messageback-action"></a><span data-ttu-id="28925-169">Tarjetas adaptables con acción messageBack</span><span class="sxs-lookup"><span data-stu-id="28925-169">Adaptive Cards with messageBack action</span></span>

<span data-ttu-id="28925-170">Para incluir una `messageBack` acción con una tarjeta adaptable, incluya los siguientes detalles `msteams` en el objeto.</span><span class="sxs-lookup"><span data-stu-id="28925-170">To include a `messageBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="28925-171">Tenga en cuenta que puede incluir propiedades ocultas adicionales `data` en el objeto, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="28925-171">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="28925-172">Propiedad</span><span class="sxs-lookup"><span data-stu-id="28925-172">Property</span></span> | <span data-ttu-id="28925-173">Descripción</span><span class="sxs-lookup"><span data-stu-id="28925-173">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="28925-174">Establece en`messageBack`</span><span class="sxs-lookup"><span data-stu-id="28925-174">Set to `messageBack`</span></span> |
| `displayText` | <span data-ttu-id="28925-175">Opcional.</span><span class="sxs-lookup"><span data-stu-id="28925-175">Optional.</span></span> <span data-ttu-id="28925-176">El usuario los repite en la secuencia de chat cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="28925-176">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="28925-177">Este texto *no* se envía a su bot.</span><span class="sxs-lookup"><span data-stu-id="28925-177">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="28925-178">Se envía a su bot cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="28925-178">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="28925-179">Puede codificar el contexto de la acción, como identificadores únicos o un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="28925-179">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="28925-180">Se envía a su bot cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="28925-180">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="28925-181">Use esta propiedad para simplificar el desarrollo de los robots: el código puede comprobar una única propiedad de nivel superior para enviar la lógica del bot.</span><span class="sxs-lookup"><span data-stu-id="28925-181">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

#### <a name="example"></a><span data-ttu-id="28925-182">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="28925-182">Example</span></span>

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

### <a name="adaptive-cards-with-imback-action"></a><span data-ttu-id="28925-183">Tarjetas adaptables con acción de deshacer</span><span class="sxs-lookup"><span data-stu-id="28925-183">Adaptive Cards with imBack action</span></span>

<span data-ttu-id="28925-184">Para incluir una `imBack` acción con una tarjeta adaptable, incluya los siguientes detalles `msteams` en el objeto.</span><span class="sxs-lookup"><span data-stu-id="28925-184">To include a `imBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="28925-185">Tenga en cuenta que puede incluir propiedades ocultas adicionales `data` en el objeto, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="28925-185">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="28925-186">Propiedad</span><span class="sxs-lookup"><span data-stu-id="28925-186">Property</span></span> | <span data-ttu-id="28925-187">Descripción</span><span class="sxs-lookup"><span data-stu-id="28925-187">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="28925-188">Establece en`imBack`</span><span class="sxs-lookup"><span data-stu-id="28925-188">Set to `imBack`</span></span> |
| `value` | <span data-ttu-id="28925-189">Cadena que debe volver a mostrarse en el chat</span><span class="sxs-lookup"><span data-stu-id="28925-189">String that needs to be echoed back in the chat</span></span> |

#### <a name="example"></a><span data-ttu-id="28925-190">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="28925-190">Example</span></span>

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

### <a name="adaptive-cards-with-signin-action"></a><span data-ttu-id="28925-191">Tarjetas adaptables con acción de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="28925-191">Adaptive Cards with signin action</span></span>

<span data-ttu-id="28925-192">Para incluir una `signin` acción con una tarjeta adaptable, incluya los siguientes detalles `msteams` en el objeto.</span><span class="sxs-lookup"><span data-stu-id="28925-192">To include a `signin` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="28925-193">Tenga en cuenta que puede incluir propiedades ocultas adicionales `data` en el objeto, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="28925-193">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="28925-194">Propiedad</span><span class="sxs-lookup"><span data-stu-id="28925-194">Property</span></span> | <span data-ttu-id="28925-195">Descripción</span><span class="sxs-lookup"><span data-stu-id="28925-195">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="28925-196">Establece en`signin`</span><span class="sxs-lookup"><span data-stu-id="28925-196">Set to `signin`</span></span> |
| `value` | <span data-ttu-id="28925-197">Establezca en la dirección URL a la que desea redirigir</span><span class="sxs-lookup"><span data-stu-id="28925-197">Set to the URL that you want to redirect to</span></span>  |

#### <a name="example"></a><span data-ttu-id="28925-198">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="28925-198">Example</span></span>

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

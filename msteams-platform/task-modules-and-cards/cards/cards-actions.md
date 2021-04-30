---
title: Agregar acciones de tarjeta en un bot
description: Describe acciones de tarjeta en Microsoft Teams y cómo usarlas en los bots
localization_priority: Normal
ms.topic: conceptual
keywords: acciones de tarjetas de bots de teams
ms.openlocfilehash: 75dcd6e1de1968f021a1ebe66c6770c4f641c94d
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088797"
---
# <a name="card-actions"></a><span data-ttu-id="e1c1c-104">Acciones de tarjeta</span><span class="sxs-lookup"><span data-stu-id="e1c1c-104">Card actions</span></span>

<span data-ttu-id="e1c1c-105">Las tarjetas usadas por bots y extensiones de mensajería en Teams admiten los siguientes tipos de actividad ( [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) ) .</span><span class="sxs-lookup"><span data-stu-id="e1c1c-105">Cards used by bots and messaging extensions in Teams support the following activity ([`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards)) types.</span></span> <span data-ttu-id="e1c1c-106">Tenga en cuenta que estas acciones difieren de `potentialActions` Office 365 tarjetas connector cuando se usan de Connectors.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-106">Note that these actions differ from `potentialActions` for Office 365 Connector cards when used from Connectors.</span></span>

| <span data-ttu-id="e1c1c-107">Tipo</span><span class="sxs-lookup"><span data-stu-id="e1c1c-107">Type</span></span> | <span data-ttu-id="e1c1c-108">Acción</span><span class="sxs-lookup"><span data-stu-id="e1c1c-108">Action</span></span> |
| --- | --- |
| `openUrl` | <span data-ttu-id="e1c1c-109">Abre una dirección URL en el explorador predeterminado.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-109">Opens a URL in the default browser.</span></span> |
| `messageBack` | <span data-ttu-id="e1c1c-110">Envía un mensaje y una carga al bot (del usuario que ha hecho clic en el botón o ha pulsado la tarjeta) y envía un mensaje independiente a la secuencia de chat.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-110">Sends a message and payload to the bot (from the user who clicked the button or tapped the card) and sends a separate message to the chat stream.</span></span> |
| `imBack`| <span data-ttu-id="e1c1c-111">Envía un mensaje al bot (del usuario que ha hecho clic en el botón o ha pulsado la tarjeta).</span><span class="sxs-lookup"><span data-stu-id="e1c1c-111">Sends a message to the bot (from the user who clicked the button or tapped the card).</span></span> <span data-ttu-id="e1c1c-112">Este mensaje (de usuario a bot) es visible para todos los participantes de la conversación.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-112">This message (from user to bot) is visible to all conversation participants.</span></span> |
| `invoke` | <span data-ttu-id="e1c1c-113">Envía un mensaje y una carga al bot (del usuario que ha hecho clic en el botón o ha pulsado la tarjeta).</span><span class="sxs-lookup"><span data-stu-id="e1c1c-113">Sends a message and payload to the bot (from the user who clicked the button or tapped the card).</span></span> <span data-ttu-id="e1c1c-114">Este mensaje no está visible.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-114">This message is not visible.</span></span> |
| `signin` | <span data-ttu-id="e1c1c-115">Inicia el flujo de OAuth, lo que permite a los bots conectarse con servicios seguros.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-115">Initiates OAuth flow, allowing bots to connect with secure services.</span></span> |

> [!NOTE]
>* <span data-ttu-id="e1c1c-116">Teams no admite tipos `CardAction` no enumerados en la tabla anterior.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-116">Teams does not support `CardAction` types not listed in the preceding table.</span></span>
>* <span data-ttu-id="e1c1c-117">Teams no admite la `potentialActions` propiedad.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-117">Teams does not support the `potentialActions` property.</span></span>
>* <span data-ttu-id="e1c1c-118">Las acciones de tarjeta son diferentes de [las acciones sugeridas](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) en Bot Framework/Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-118">Card actions are different than [suggested actions](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) in Bot Framework/Azure Bot Service.</span></span> <span data-ttu-id="e1c1c-119">Las acciones sugeridas no se admiten en Microsoft Teams: si desea que los botones aparezcan en un mensaje Teams bot, use una tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-119">Suggested actions are not supported in Microsoft Teams: if you want buttons to appear on a Teams bot message, use a card.</span></span>
>* <span data-ttu-id="e1c1c-120">Si usa una acción de tarjeta como parte de una extensión de mensajería, las acciones no funcionarán hasta que la tarjeta se envía al canal (no funcionarán mientras la tarjeta esté en el cuadro de mensaje de redacción).</span><span class="sxs-lookup"><span data-stu-id="e1c1c-120">If you're using a card action as part of a messaging extension, the actions will be not work until the card is submitted to the channel (they will not work while the card is in the compose message box).</span></span>

<span data-ttu-id="e1c1c-121">Teams también admite acciones [de tarjetas adaptables,](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)que solo las usan las tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-121">Teams also supports [Adaptive Cards actions](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions), which are only used by Adaptive Cards.</span></span> <span data-ttu-id="e1c1c-122">Estas acciones se enumeran en su propia sección al final de esta referencia.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-122">These actions are listed in their own section at the end of this reference.</span></span>

## <a name="openurl"></a><span data-ttu-id="e1c1c-123">openUrl</span><span class="sxs-lookup"><span data-stu-id="e1c1c-123">openUrl</span></span>

<span data-ttu-id="e1c1c-124">Este tipo de acción especifica una dirección URL que se iniciará en el explorador predeterminado.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-124">This action type specifies a URL to launch in the default browser.</span></span> <span data-ttu-id="e1c1c-125">Tenga en cuenta que el bot no recibe ningún aviso en el que se hizo clic en el botón.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-125">Note that your bot does not receive any notice on which button was clicked.</span></span>

<span data-ttu-id="e1c1c-126">El `value` campo debe contener una dirección URL completa y correctamente formada.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-126">The `value` field must contain a full and properly formed URL.</span></span>

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a><span data-ttu-id="e1c1c-127">messageBack</span><span class="sxs-lookup"><span data-stu-id="e1c1c-127">messageBack</span></span>

<span data-ttu-id="e1c1c-128">Con `messageBack` , puede crear una acción totalmente personalizada con las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="e1c1c-128">With `messageBack`, you can create a fully customized action with the following properties:</span></span>

| <span data-ttu-id="e1c1c-129">Propiedad</span><span class="sxs-lookup"><span data-stu-id="e1c1c-129">Property</span></span> | <span data-ttu-id="e1c1c-130">Descripción</span><span class="sxs-lookup"><span data-stu-id="e1c1c-130">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="e1c1c-131">Aparece como la etiqueta del botón.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-131">Appears as the button label.</span></span> |
| `displayText` | <span data-ttu-id="e1c1c-132">Opcional.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-132">Optional.</span></span> <span data-ttu-id="e1c1c-133">El usuario hizo eco en la secuencia de chat cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-133">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="e1c1c-134">Este texto no *se* envía al bot.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-134">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="e1c1c-135">Se envía al bot cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-135">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="e1c1c-136">Puede codificar el contexto de la acción, como identificadores únicos o un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-136">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="e1c1c-137">Se envía al bot cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-137">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="e1c1c-138">Use esta propiedad para simplificar el desarrollo de bots: el código puede comprobar una sola propiedad de nivel superior para distribuir la lógica del bot.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-138">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="e1c1c-139">La flexibilidad de significa que el código puede elegir no dejar un mensaje de usuario visible en el historial simplemente sin `messageBack` usar `displayText` .</span><span class="sxs-lookup"><span data-stu-id="e1c1c-139">The flexibility of `messageBack` means that your code can choose not to leave a visible user message in the history simply by not using `displayText`.</span></span>

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

<span data-ttu-id="e1c1c-140">La `value` propiedad puede ser una cadena JSON serializada o un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-140">The `value` property can be either a serialized JSON string or a JSON object.</span></span>

### <a name="inbound-message-example"></a><span data-ttu-id="e1c1c-141">Ejemplo de mensaje entrante</span><span class="sxs-lookup"><span data-stu-id="e1c1c-141">Inbound message example</span></span>

<span data-ttu-id="e1c1c-142">`replyToId` contiene el identificador del mensaje del que provenía la acción de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-142">`replyToId` contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="e1c1c-143">Úselo si desea actualizar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-143">Use it if you want to update the message.</span></span>

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

## <a name="imback"></a><span data-ttu-id="e1c1c-144">imBack</span><span class="sxs-lookup"><span data-stu-id="e1c1c-144">imBack</span></span>

<span data-ttu-id="e1c1c-145">Esta acción desencadena un mensaje devuelto al bot, como si el usuario lo hubiera especificado en un mensaje de chat normal.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-145">This action triggers a return message to your bot, as if the user typed it in a normal chat message.</span></span> <span data-ttu-id="e1c1c-146">El usuario, y todos los demás usuarios si están en un canal, verán la respuesta del botón.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-146">Your user, and all other users if in a channel, will see that button response.</span></span>

<span data-ttu-id="e1c1c-147">El campo debe contener la cadena de texto que se hace eco en el chat y, por lo `value` tanto, se envía de nuevo al bot.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-147">The `value` field should contain the text string echoed in the chat and therefore sent back to the bot.</span></span> <span data-ttu-id="e1c1c-148">Este es el texto del mensaje que procesará en el bot para realizar la lógica deseada.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-148">This is the message text you will process in your bot to perform the desired logic.</span></span> <span data-ttu-id="e1c1c-149">Nota: este campo es una cadena sencilla: no hay compatibilidad con el formato ni los caracteres ocultos.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-149">Note: this field is a simple string - there is no support for formatting or hidden characters.</span></span>

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a><span data-ttu-id="e1c1c-150">invoke</span><span class="sxs-lookup"><span data-stu-id="e1c1c-150">invoke</span></span>

<span data-ttu-id="e1c1c-151">La `invoke` acción se usa para invocar módulos de [tareas](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span><span class="sxs-lookup"><span data-stu-id="e1c1c-151">The `invoke` action is used for invoking [task modules](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="e1c1c-152">La `invoke` acción contiene tres propiedades: , y `type` `title` `value` .</span><span class="sxs-lookup"><span data-stu-id="e1c1c-152">The `invoke` action contains three properties: `type`, `title`, and `value`.</span></span> <span data-ttu-id="e1c1c-153">La `value` propiedad puede contener una cadena, un objeto JSON con cadena o un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-153">The `value` property can contain a string, a stringified JSON object, or a JSON object.</span></span>

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

<span data-ttu-id="e1c1c-154">Cuando un usuario hace clic en el botón, el bot recibirá el `value` objeto con información adicional.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-154">When a user clicks the button, your bot will receive the `value` object with some additional info.</span></span> <span data-ttu-id="e1c1c-155">Tenga en cuenta que el tipo de actividad será `invoke` en lugar de ( `message` `activity.Type == "invoke"` ).</span><span class="sxs-lookup"><span data-stu-id="e1c1c-155">Please note that the activity type will be `invoke` instead of `message` (`activity.Type == "invoke"`).</span></span>

### <a name="example-invoke-button-definition-net"></a><span data-ttu-id="e1c1c-156">Ejemplo: Invocar definición de botón (.NET)</span><span class="sxs-lookup"><span data-stu-id="e1c1c-156">Example: Invoke button definition (.NET)</span></span>

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a><span data-ttu-id="e1c1c-157">Ejemplo: Mensaje de invocación entrante</span><span class="sxs-lookup"><span data-stu-id="e1c1c-157">Example: Incoming invoke message</span></span>

<span data-ttu-id="e1c1c-158">La propiedad de nivel superior contiene el identificador del mensaje del que provenía la `replyToId` acción de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-158">The top-level `replyToId` property contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="e1c1c-159">Úselo si desea actualizar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-159">Use it if you want to update the message.</span></span>

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

## <a name="signin"></a><span data-ttu-id="e1c1c-160">signin</span><span class="sxs-lookup"><span data-stu-id="e1c1c-160">signin</span></span>

<span data-ttu-id="e1c1c-161">Inicia un flujo de OAuth, lo que permite a los bots conectarse con servicios seguros, como se describe con más detalle aquí: Flujo de [autenticación en bots](~/bots/how-to/authentication/auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="e1c1c-161">Initiates an OAuth flow, allowing bots to connect with secure services, as described in more detail here: [Authentication flow in bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

## <a name="adaptive-cards-actions"></a><span data-ttu-id="e1c1c-162">Acciones de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="e1c1c-162">Adaptive Cards actions</span></span>

<span data-ttu-id="e1c1c-163">Las tarjetas adaptables admiten cuatro tipos de acción:</span><span class="sxs-lookup"><span data-stu-id="e1c1c-163">Adaptive Cards support four action types:</span></span>

* [<span data-ttu-id="e1c1c-164">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="e1c1c-164">Action.OpenUrl</span></span>](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [<span data-ttu-id="e1c1c-165">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="e1c1c-165">Action.Submit</span></span>](http://adaptivecards.io/explorer/Action.Submit.html)
* [<span data-ttu-id="e1c1c-166">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="e1c1c-166">Action.ShowCard</span></span>](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [<span data-ttu-id="e1c1c-167">Action.Exebonito</span><span class="sxs-lookup"><span data-stu-id="e1c1c-167">Action.Execute</span></span>](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

<span data-ttu-id="e1c1c-168">Además de las acciones mencionadas anteriormente, puede modificar la carga de la tarjeta adaptable para admitir acciones existentes de Bot Framework mediante una propiedad `Action.Submit` en el objeto de `msteams` `data` `Action.Submit` .</span><span class="sxs-lookup"><span data-stu-id="e1c1c-168">In addition to the actions mentioned above, you can modify the Adaptive Card `Action.Submit` payload to support existing Bot Framework actions using a `msteams` property in the `data` object of `Action.Submit`.</span></span> <span data-ttu-id="e1c1c-169">En las secciones siguientes se detalla cómo usar acciones existentes de Bot Framework con tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-169">The below sections detail how to use existing Bot Framework actions with Adaptive Cards.</span></span>

> [!NOTE]
> <span data-ttu-id="e1c1c-170">Agregar `msteams` a datos, con una acción de Bot Framework, no funciona con un módulo de tareas de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-170">Adding `msteams` to data, with a Bot Framework action, does not work with an Adaptive Card task module.</span></span>

### <a name="adaptive-cards-with-messageback-action"></a><span data-ttu-id="e1c1c-171">Tarjetas adaptables con acción messageBack</span><span class="sxs-lookup"><span data-stu-id="e1c1c-171">Adaptive Cards with messageBack action</span></span>

<span data-ttu-id="e1c1c-172">Para incluir una `messageBack` acción con una tarjeta adaptable, incluya los siguientes detalles en el `msteams` objeto.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-172">To include a `messageBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="e1c1c-173">Tenga en cuenta que puede incluir propiedades ocultas adicionales en el `data` objeto si es necesario.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-173">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="e1c1c-174">Propiedad</span><span class="sxs-lookup"><span data-stu-id="e1c1c-174">Property</span></span> | <span data-ttu-id="e1c1c-175">Descripción</span><span class="sxs-lookup"><span data-stu-id="e1c1c-175">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="e1c1c-176">Establecer en `messageBack`</span><span class="sxs-lookup"><span data-stu-id="e1c1c-176">Set to `messageBack`</span></span> |
| `displayText` | <span data-ttu-id="e1c1c-177">Opcional.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-177">Optional.</span></span> <span data-ttu-id="e1c1c-178">El usuario hizo eco en la secuencia de chat cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-178">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="e1c1c-179">Este texto no *se* envía al bot.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-179">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="e1c1c-180">Se envía al bot cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-180">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="e1c1c-181">Puede codificar el contexto de la acción, como identificadores únicos o un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-181">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="e1c1c-182">Se envía al bot cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-182">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="e1c1c-183">Use esta propiedad para simplificar el desarrollo de bots: el código puede comprobar una sola propiedad de nivel superior para distribuir la lógica del bot.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-183">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

#### <a name="example"></a><span data-ttu-id="e1c1c-184">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="e1c1c-184">Example</span></span>

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

### <a name="adaptive-cards-with-imback-action"></a><span data-ttu-id="e1c1c-185">Tarjetas adaptables con acción de imBack</span><span class="sxs-lookup"><span data-stu-id="e1c1c-185">Adaptive Cards with imBack action</span></span>

<span data-ttu-id="e1c1c-186">Para incluir una `imBack` acción con una tarjeta adaptable, incluya los siguientes detalles en el `msteams` objeto.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-186">To include a `imBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="e1c1c-187">Tenga en cuenta que puede incluir propiedades ocultas adicionales en el `data` objeto si es necesario.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-187">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="e1c1c-188">Propiedad</span><span class="sxs-lookup"><span data-stu-id="e1c1c-188">Property</span></span> | <span data-ttu-id="e1c1c-189">Descripción</span><span class="sxs-lookup"><span data-stu-id="e1c1c-189">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="e1c1c-190">Establecer en `imBack`</span><span class="sxs-lookup"><span data-stu-id="e1c1c-190">Set to `imBack`</span></span> |
| `value` | <span data-ttu-id="e1c1c-191">Cadena que debe tener eco en el chat</span><span class="sxs-lookup"><span data-stu-id="e1c1c-191">String that needs to be echoed back in the chat</span></span> |

#### <a name="example"></a><span data-ttu-id="e1c1c-192">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="e1c1c-192">Example</span></span>

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

### <a name="adaptive-cards-with-signin-action"></a><span data-ttu-id="e1c1c-193">Tarjetas adaptables con acción de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="e1c1c-193">Adaptive Cards with signin action</span></span>

<span data-ttu-id="e1c1c-194">Para incluir una `signin` acción con una tarjeta adaptable, incluya los siguientes detalles en el `msteams` objeto.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-194">To include a `signin` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="e1c1c-195">Tenga en cuenta que puede incluir propiedades ocultas adicionales en el `data` objeto si es necesario.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-195">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="e1c1c-196">Propiedad</span><span class="sxs-lookup"><span data-stu-id="e1c1c-196">Property</span></span> | <span data-ttu-id="e1c1c-197">Descripción</span><span class="sxs-lookup"><span data-stu-id="e1c1c-197">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="e1c1c-198">Establecer en `signin`</span><span class="sxs-lookup"><span data-stu-id="e1c1c-198">Set to `signin`</span></span> |
| `value` | <span data-ttu-id="e1c1c-199">Establecer en la dirección URL a la que desea redirigir</span><span class="sxs-lookup"><span data-stu-id="e1c1c-199">Set to the URL that you want to redirect to</span></span>  |

#### <a name="example"></a><span data-ttu-id="e1c1c-200">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="e1c1c-200">Example</span></span>

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

### <a name="adaptive-cards-with-invoke-action"></a><span data-ttu-id="e1c1c-201">Tarjetas adaptables con acción invocar</span><span class="sxs-lookup"><span data-stu-id="e1c1c-201">Adaptive Cards with invoke action</span></span>
 
<span data-ttu-id="e1c1c-202">Para incluir una `invoke` acción con una tarjeta adaptable, incluya los siguientes detalles en el `msteams` objeto.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-202">To include a `invoke` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="e1c1c-203">Tenga en cuenta que puede incluir propiedades ocultas adicionales en el `data` objeto si es necesario.</span><span class="sxs-lookup"><span data-stu-id="e1c1c-203">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="e1c1c-204">Propiedad</span><span class="sxs-lookup"><span data-stu-id="e1c1c-204">Property</span></span> | <span data-ttu-id="e1c1c-205">Descripción</span><span class="sxs-lookup"><span data-stu-id="e1c1c-205">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="e1c1c-206">Establecer en `task/fetch`</span><span class="sxs-lookup"><span data-stu-id="e1c1c-206">Set to `task/fetch`</span></span> |
| `data` | <span data-ttu-id="e1c1c-207">Establecer el valor</span><span class="sxs-lookup"><span data-stu-id="e1c1c-207">Set the value</span></span>  |

#### <a name="example"></a><span data-ttu-id="e1c1c-208">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="e1c1c-208">Example</span></span>

```json
{
  "type": "Action.Submit",
  "title": "submit"
  "data": {
    "msteams": {
        "type": "task/fetch"
    }
  }
}
```

#### <a name="example-2-with-additional-payload-data"></a><span data-ttu-id="e1c1c-209">Ejemplo 2 (con datos de carga adicionales)</span><span class="sxs-lookup"><span data-stu-id="e1c1c-209">Example 2 (with additional payload data)</span></span>

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

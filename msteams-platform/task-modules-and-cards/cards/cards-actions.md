---
title: Agregar acciones de tarjeta en un bot
description: Describe acciones de tarjeta en Microsoft Teams y cómo usarlas en los bots
localization_priority: Normal
ms.topic: conceptual
keywords: acciones de tarjetas de bots de teams
ms.openlocfilehash: b9276c7197070df43ba447707e6fa4d3d4098591
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566855"
---
# <a name="card-actions"></a><span data-ttu-id="5478e-104">Acciones de tarjeta</span><span class="sxs-lookup"><span data-stu-id="5478e-104">Card actions</span></span>

<span data-ttu-id="5478e-105">Las tarjetas usadas por bots y extensiones de mensajería en Teams admiten los siguientes tipos de actividad ( [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) ) .</span><span class="sxs-lookup"><span data-stu-id="5478e-105">Cards used by bots and messaging extensions in Teams support the following activity ([`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards)) types.</span></span> <span data-ttu-id="5478e-106">Tenga en cuenta que estas acciones difieren de `potentialActions` Office 365 tarjetas connector cuando se usan de Connectors.</span><span class="sxs-lookup"><span data-stu-id="5478e-106">Note that these actions differ from `potentialActions` for Office 365 Connector cards when used from Connectors.</span></span>

| <span data-ttu-id="5478e-107">Tipo</span><span class="sxs-lookup"><span data-stu-id="5478e-107">Type</span></span> | <span data-ttu-id="5478e-108">Acción</span><span class="sxs-lookup"><span data-stu-id="5478e-108">Action</span></span> |
| --- | --- |
| `openUrl` | <span data-ttu-id="5478e-109">Abre una dirección URL en el explorador predeterminado.</span><span class="sxs-lookup"><span data-stu-id="5478e-109">Opens a URL in the default browser.</span></span> |
| `messageBack` | <span data-ttu-id="5478e-110">Envía un mensaje y una carga al bot del usuario que ha hecho clic en el botón o ha pulsado la tarjeta y envía un mensaje independiente a la secuencia de chat.</span><span class="sxs-lookup"><span data-stu-id="5478e-110">Sends a message and payload to the bot from the user who clicked the button or tapped the card and sends a separate message to the chat stream.</span></span> |
| `imBack`| <span data-ttu-id="5478e-111">Envía un mensaje al bot del usuario que ha hecho clic en el botón o ha pulsado la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="5478e-111">Sends a message to the bot from the user who clicked the button or tapped the card.</span></span> <span data-ttu-id="5478e-112">Este mensaje (de usuario a bot) es visible para todos los participantes de la conversación.</span><span class="sxs-lookup"><span data-stu-id="5478e-112">This message (from user to bot) is visible to all conversation participants.</span></span> |
| `invoke` | <span data-ttu-id="5478e-113">Envía un mensaje y una carga al bot del usuario que ha hecho clic en el botón o ha pulsado la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="5478e-113">Sends a message and payload to the bot from the user who clicked the button or tapped the card.</span></span> <span data-ttu-id="5478e-114">Este mensaje no está visible.</span><span class="sxs-lookup"><span data-stu-id="5478e-114">This message is not visible.</span></span> |
| `signin` | <span data-ttu-id="5478e-115">Inicia el flujo de OAuth, lo que permite a los bots conectarse con servicios seguros.</span><span class="sxs-lookup"><span data-stu-id="5478e-115">Initiates OAuth flow, allowing bots to connect with secure services.</span></span> |

> [!NOTE]
>* <span data-ttu-id="5478e-116">Teams no admite tipos `CardAction` no enumerados en la tabla anterior.</span><span class="sxs-lookup"><span data-stu-id="5478e-116">Teams does not support `CardAction` types not listed in the preceding table.</span></span>
>* <span data-ttu-id="5478e-117">Teams no admite la `potentialActions` propiedad.</span><span class="sxs-lookup"><span data-stu-id="5478e-117">Teams does not support the `potentialActions` property.</span></span>
>* <span data-ttu-id="5478e-118">Las acciones de tarjeta son diferentes de [las acciones sugeridas](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) en Bot Framework/Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="5478e-118">Card actions are different than [suggested actions](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) in Bot Framework/Azure Bot Service.</span></span> <span data-ttu-id="5478e-119">Las acciones sugeridas no se admiten en Microsoft Teams: si desea que los botones aparezcan en un mensaje Teams bot, use una tarjeta.</span><span class="sxs-lookup"><span data-stu-id="5478e-119">Suggested actions are not supported in Microsoft Teams: if you want buttons to appear on a Teams bot message, use a card.</span></span>
>* <span data-ttu-id="5478e-120">Si usa una acción de tarjeta como parte de una extensión de mensajería, las acciones no funcionarán hasta que la tarjeta se envía al canal.</span><span class="sxs-lookup"><span data-stu-id="5478e-120">If you are using a card action as part of a messaging extension, the actions do not work until the card is submitted to the channel.</span></span> <span data-ttu-id="5478e-121">No funcionan mientras la tarjeta está en el cuadro de mensaje de redacción.</span><span class="sxs-lookup"><span data-stu-id="5478e-121">They do not work while the card is in the compose message box.</span></span>

<span data-ttu-id="5478e-122">Teams también admite acciones [de tarjetas adaptables,](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)que solo las usan las tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="5478e-122">Teams also supports [Adaptive Cards actions](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions), which are only used by Adaptive Cards.</span></span> <span data-ttu-id="5478e-123">Estas acciones se enumeran en su propia sección al final de esta referencia.</span><span class="sxs-lookup"><span data-stu-id="5478e-123">These actions are listed in their own section at the end of this reference.</span></span>

## <a name="openurl"></a><span data-ttu-id="5478e-124">openUrl</span><span class="sxs-lookup"><span data-stu-id="5478e-124">openUrl</span></span>

<span data-ttu-id="5478e-125">Este tipo de acción especifica una dirección URL que se iniciará en el explorador predeterminado.</span><span class="sxs-lookup"><span data-stu-id="5478e-125">This action type specifies a URL to launch in the default browser.</span></span> <span data-ttu-id="5478e-126">Tenga en cuenta que el bot no recibe ningún aviso en el que se hizo clic en el botón.</span><span class="sxs-lookup"><span data-stu-id="5478e-126">Note that your bot does not receive any notice on which button was clicked.</span></span>

<span data-ttu-id="5478e-127">El `value` campo debe contener una dirección URL completa y correctamente formada.</span><span class="sxs-lookup"><span data-stu-id="5478e-127">The `value` field must contain a full and properly formed URL.</span></span>

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a><span data-ttu-id="5478e-128">messageBack</span><span class="sxs-lookup"><span data-stu-id="5478e-128">messageBack</span></span>

<span data-ttu-id="5478e-129">Con `messageBack` , puede crear una acción totalmente personalizada con las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="5478e-129">With `messageBack`, you can create a fully customized action with the following properties:</span></span>

| <span data-ttu-id="5478e-130">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5478e-130">Property</span></span> | <span data-ttu-id="5478e-131">Descripción</span><span class="sxs-lookup"><span data-stu-id="5478e-131">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="5478e-132">Aparece como la etiqueta del botón.</span><span class="sxs-lookup"><span data-stu-id="5478e-132">Appears as the button label.</span></span> |
| `displayText` | <span data-ttu-id="5478e-133">Opcional.</span><span class="sxs-lookup"><span data-stu-id="5478e-133">Optional.</span></span> <span data-ttu-id="5478e-134">El usuario hizo eco en la secuencia de chat cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="5478e-134">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="5478e-135">Este texto no *se* envía al bot.</span><span class="sxs-lookup"><span data-stu-id="5478e-135">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="5478e-136">Se envía al bot cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="5478e-136">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="5478e-137">Puede codificar el contexto de la acción, como identificadores únicos o un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="5478e-137">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="5478e-138">Se envía al bot cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="5478e-138">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="5478e-139">Use esta propiedad para simplificar el desarrollo de bots: el código puede comprobar una sola propiedad de nivel superior para distribuir la lógica del bot.</span><span class="sxs-lookup"><span data-stu-id="5478e-139">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="5478e-140">La flexibilidad de significa que el código puede elegir no dejar un mensaje de usuario visible en el historial simplemente sin `messageBack` usar `displayText` .</span><span class="sxs-lookup"><span data-stu-id="5478e-140">The flexibility of `messageBack` means that your code can choose not to leave a visible user message in the history simply by not using `displayText`.</span></span>

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

<span data-ttu-id="5478e-141">La `value` propiedad puede ser una cadena JSON serializada o un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="5478e-141">The `value` property can be either a serialized JSON string or a JSON object.</span></span>

### <a name="inbound-message-example"></a><span data-ttu-id="5478e-142">Ejemplo de mensaje entrante</span><span class="sxs-lookup"><span data-stu-id="5478e-142">Inbound message example</span></span>

<span data-ttu-id="5478e-143">`replyToId` contiene el identificador del mensaje del que provenía la acción de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="5478e-143">`replyToId` contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="5478e-144">Úselo si desea actualizar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="5478e-144">Use it if you want to update the message.</span></span>

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

## <a name="imback"></a><span data-ttu-id="5478e-145">imBack</span><span class="sxs-lookup"><span data-stu-id="5478e-145">imBack</span></span>

<span data-ttu-id="5478e-146">Esta acción desencadena un mensaje devuelto al bot, como si el usuario lo hubiera especificado en un mensaje de chat normal.</span><span class="sxs-lookup"><span data-stu-id="5478e-146">This action triggers a return message to your bot, as if the user typed it in a normal chat message.</span></span> <span data-ttu-id="5478e-147">El usuario, y todos los demás usuarios si están en un canal, verán la respuesta del botón.</span><span class="sxs-lookup"><span data-stu-id="5478e-147">Your user, and all other users if in a channel, will see that button response.</span></span>

<span data-ttu-id="5478e-148">El campo debe contener la cadena de texto que se hace eco en el chat y, por lo `value` tanto, se envía de nuevo al bot.</span><span class="sxs-lookup"><span data-stu-id="5478e-148">The `value` field should contain the text string echoed in the chat and therefore sent back to the bot.</span></span> <span data-ttu-id="5478e-149">Este es el texto del mensaje que procesará en el bot para realizar la lógica deseada.</span><span class="sxs-lookup"><span data-stu-id="5478e-149">This is the message text you will process in your bot to perform the desired logic.</span></span> <span data-ttu-id="5478e-150">Nota: este campo es una cadena sencilla: no hay compatibilidad con el formato ni los caracteres ocultos.</span><span class="sxs-lookup"><span data-stu-id="5478e-150">Note: this field is a simple string - there is no support for formatting or hidden characters.</span></span>

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a><span data-ttu-id="5478e-151">invoke</span><span class="sxs-lookup"><span data-stu-id="5478e-151">invoke</span></span>

<span data-ttu-id="5478e-152">La `invoke` acción se usa para invocar módulos de [tareas](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span><span class="sxs-lookup"><span data-stu-id="5478e-152">The `invoke` action is used for invoking [task modules](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="5478e-153">La `invoke` acción contiene tres propiedades: , y `type` `title` `value` .</span><span class="sxs-lookup"><span data-stu-id="5478e-153">The `invoke` action contains three properties: `type`, `title`, and `value`.</span></span> <span data-ttu-id="5478e-154">La `value` propiedad puede contener una cadena, un objeto JSON con cadena o un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="5478e-154">The `value` property can contain a string, a stringified JSON object, or a JSON object.</span></span>

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

<span data-ttu-id="5478e-155">Cuando un usuario hace clic en el botón, el bot recibirá el `value` objeto con información adicional.</span><span class="sxs-lookup"><span data-stu-id="5478e-155">When a user clicks the button, your bot will receive the `value` object with some additional info.</span></span> <span data-ttu-id="5478e-156">Tenga en cuenta que el tipo de actividad será `invoke` en lugar de ( `message` `activity.Type == "invoke"` ).</span><span class="sxs-lookup"><span data-stu-id="5478e-156">Please note that the activity type will be `invoke` instead of `message` (`activity.Type == "invoke"`).</span></span>

### <a name="example-invoke-button-definition-net"></a><span data-ttu-id="5478e-157">Ejemplo: Invocar definición de botón (.NET)</span><span class="sxs-lookup"><span data-stu-id="5478e-157">Example: Invoke button definition (.NET)</span></span>

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a><span data-ttu-id="5478e-158">Ejemplo: Mensaje de invocación entrante</span><span class="sxs-lookup"><span data-stu-id="5478e-158">Example: Incoming invoke message</span></span>

<span data-ttu-id="5478e-159">La propiedad de nivel superior contiene el identificador del mensaje del que provenía la `replyToId` acción de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="5478e-159">The top-level `replyToId` property contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="5478e-160">Úselo si desea actualizar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="5478e-160">Use it if you want to update the message.</span></span>

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

## <a name="signin"></a><span data-ttu-id="5478e-161">signin</span><span class="sxs-lookup"><span data-stu-id="5478e-161">signin</span></span>

<span data-ttu-id="5478e-162">Inicia un flujo de OAuth, lo que permite a los bots conectarse con servicios seguros, como se describe con más detalle aquí: Flujo de [autenticación en bots](~/bots/how-to/authentication/auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="5478e-162">Initiates an OAuth flow, allowing bots to connect with secure services, as described in more detail here: [Authentication flow in bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

## <a name="adaptive-cards-actions"></a><span data-ttu-id="5478e-163">Acciones de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="5478e-163">Adaptive Cards actions</span></span>

<span data-ttu-id="5478e-164">Las tarjetas adaptables admiten cuatro tipos de acción:</span><span class="sxs-lookup"><span data-stu-id="5478e-164">Adaptive Cards support four action types:</span></span>

* [<span data-ttu-id="5478e-165">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="5478e-165">Action.OpenUrl</span></span>](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [<span data-ttu-id="5478e-166">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="5478e-166">Action.Submit</span></span>](http://adaptivecards.io/explorer/Action.Submit.html)
* [<span data-ttu-id="5478e-167">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="5478e-167">Action.ShowCard</span></span>](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [<span data-ttu-id="5478e-168">Action.Exebonito</span><span class="sxs-lookup"><span data-stu-id="5478e-168">Action.Execute</span></span>](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

<span data-ttu-id="5478e-169">Además de las acciones mencionadas anteriormente, puede modificar la carga de la tarjeta adaptable para admitir acciones existentes de Bot Framework mediante una propiedad `Action.Submit` en el objeto de `msteams` `data` `Action.Submit` .</span><span class="sxs-lookup"><span data-stu-id="5478e-169">In addition to the actions mentioned above, you can modify the Adaptive Card `Action.Submit` payload to support existing Bot Framework actions using a `msteams` property in the `data` object of `Action.Submit`.</span></span> <span data-ttu-id="5478e-170">En las secciones siguientes se detalla cómo usar acciones existentes de Bot Framework con tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="5478e-170">The below sections detail how to use existing Bot Framework actions with Adaptive Cards.</span></span>

> [!NOTE]
> <span data-ttu-id="5478e-171">Agregar `msteams` a datos, con una acción de Bot Framework, no funciona con un módulo de tareas de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="5478e-171">Adding `msteams` to data, with a Bot Framework action, does not work with an Adaptive Card task module.</span></span>

### <a name="adaptive-cards-with-messageback-action"></a><span data-ttu-id="5478e-172">Tarjetas adaptables con acción messageBack</span><span class="sxs-lookup"><span data-stu-id="5478e-172">Adaptive Cards with messageBack action</span></span>

<span data-ttu-id="5478e-173">Para incluir una `messageBack` acción con una tarjeta adaptable, incluya los siguientes detalles en el `msteams` objeto.</span><span class="sxs-lookup"><span data-stu-id="5478e-173">To include a `messageBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="5478e-174">Tenga en cuenta que puede incluir propiedades ocultas adicionales en el `data` objeto si es necesario.</span><span class="sxs-lookup"><span data-stu-id="5478e-174">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="5478e-175">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5478e-175">Property</span></span> | <span data-ttu-id="5478e-176">Descripción</span><span class="sxs-lookup"><span data-stu-id="5478e-176">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="5478e-177">Establecer en `messageBack`</span><span class="sxs-lookup"><span data-stu-id="5478e-177">Set to `messageBack`</span></span> |
| `displayText` | <span data-ttu-id="5478e-178">Opcional.</span><span class="sxs-lookup"><span data-stu-id="5478e-178">Optional.</span></span> <span data-ttu-id="5478e-179">El usuario hizo eco en la secuencia de chat cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="5478e-179">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="5478e-180">Este texto no *se* envía al bot.</span><span class="sxs-lookup"><span data-stu-id="5478e-180">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="5478e-181">Se envía al bot cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="5478e-181">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="5478e-182">Puede codificar el contexto de la acción, como identificadores únicos o un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="5478e-182">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="5478e-183">Se envía al bot cuando se realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="5478e-183">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="5478e-184">Use esta propiedad para simplificar el desarrollo de bots: el código puede comprobar una sola propiedad de nivel superior para distribuir la lógica del bot.</span><span class="sxs-lookup"><span data-stu-id="5478e-184">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

#### <a name="example"></a><span data-ttu-id="5478e-185">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="5478e-185">Example</span></span>

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

### <a name="adaptive-cards-with-imback-action"></a><span data-ttu-id="5478e-186">Tarjetas adaptables con acción de imBack</span><span class="sxs-lookup"><span data-stu-id="5478e-186">Adaptive Cards with imBack action</span></span>

<span data-ttu-id="5478e-187">Para incluir una `imBack` acción con una tarjeta adaptable, incluya los siguientes detalles en el `msteams` objeto.</span><span class="sxs-lookup"><span data-stu-id="5478e-187">To include a `imBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="5478e-188">Tenga en cuenta que puede incluir propiedades ocultas adicionales en el `data` objeto si es necesario.</span><span class="sxs-lookup"><span data-stu-id="5478e-188">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="5478e-189">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5478e-189">Property</span></span> | <span data-ttu-id="5478e-190">Descripción</span><span class="sxs-lookup"><span data-stu-id="5478e-190">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="5478e-191">Establecer en `imBack`</span><span class="sxs-lookup"><span data-stu-id="5478e-191">Set to `imBack`</span></span> |
| `value` | <span data-ttu-id="5478e-192">Cadena que debe tener eco en el chat</span><span class="sxs-lookup"><span data-stu-id="5478e-192">String that needs to be echoed back in the chat</span></span> |

#### <a name="example"></a><span data-ttu-id="5478e-193">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="5478e-193">Example</span></span>

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

### <a name="adaptive-cards-with-signin-action"></a><span data-ttu-id="5478e-194">Tarjetas adaptables con acción de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="5478e-194">Adaptive Cards with signin action</span></span>

<span data-ttu-id="5478e-195">Para incluir una `signin` acción con una tarjeta adaptable, incluya los siguientes detalles en el `msteams` objeto.</span><span class="sxs-lookup"><span data-stu-id="5478e-195">To include a `signin` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="5478e-196">Tenga en cuenta que puede incluir propiedades ocultas adicionales en el `data` objeto si es necesario.</span><span class="sxs-lookup"><span data-stu-id="5478e-196">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="5478e-197">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5478e-197">Property</span></span> | <span data-ttu-id="5478e-198">Descripción</span><span class="sxs-lookup"><span data-stu-id="5478e-198">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="5478e-199">Se establece en `signin` .</span><span class="sxs-lookup"><span data-stu-id="5478e-199">Set to `signin`.</span></span> |
| `value` | <span data-ttu-id="5478e-200">Establezca la dirección URL a la que desea redirigir.</span><span class="sxs-lookup"><span data-stu-id="5478e-200">Set to the URL that you want to redirect to.</span></span>  |

#### <a name="example"></a><span data-ttu-id="5478e-201">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="5478e-201">Example</span></span>

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

### <a name="adaptive-cards-with-invoke-action"></a><span data-ttu-id="5478e-202">Tarjetas adaptables con acción invocar</span><span class="sxs-lookup"><span data-stu-id="5478e-202">Adaptive Cards with invoke action</span></span>
 
<span data-ttu-id="5478e-203">Para incluir una `invoke` acción con una tarjeta adaptable, incluya los siguientes detalles en el `msteams` objeto.</span><span class="sxs-lookup"><span data-stu-id="5478e-203">To include a `invoke` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="5478e-204">Tenga en cuenta que puede incluir propiedades ocultas adicionales en el `data` objeto si es necesario.</span><span class="sxs-lookup"><span data-stu-id="5478e-204">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="5478e-205">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5478e-205">Property</span></span> | <span data-ttu-id="5478e-206">Descripción</span><span class="sxs-lookup"><span data-stu-id="5478e-206">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="5478e-207">Establecer en `task/fetch`</span><span class="sxs-lookup"><span data-stu-id="5478e-207">Set to `task/fetch`</span></span> |
| `data` | <span data-ttu-id="5478e-208">Establecer el valor</span><span class="sxs-lookup"><span data-stu-id="5478e-208">Set the value</span></span>  |

#### <a name="example"></a><span data-ttu-id="5478e-209">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="5478e-209">Example</span></span>

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

#### <a name="example-2-with-additional-payload-data"></a><span data-ttu-id="5478e-210">Ejemplo 2 (con datos de carga adicionales)</span><span class="sxs-lookup"><span data-stu-id="5478e-210">Example 2 (with additional payload data)</span></span>

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

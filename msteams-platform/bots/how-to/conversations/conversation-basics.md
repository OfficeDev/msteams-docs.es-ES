---
title: Conceptos básicos de la conversación
author: clearab
description: Cómo tener una conversación con un bot de Microsoft Teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: bc016a8f0dcce474f80898dc93e309692ba20471
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/15/2020
ms.locfileid: "47819056"
---
# <a name="conversation-basics"></a><span data-ttu-id="275ef-103">Conceptos básicos de la conversación</span><span class="sxs-lookup"><span data-stu-id="275ef-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="275ef-104">Una conversación es una serie de mensajes enviados entre el bot y uno o más usuarios.</span><span class="sxs-lookup"><span data-stu-id="275ef-104">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="275ef-105">Hay tres tipos de conversaciones (también denominadas ámbitos) en Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="275ef-105">There are three kinds of conversations (also called scopes) in Teams:</span></span>

* <span data-ttu-id="275ef-106">`teams` También se denominan conversaciones de canal, visibles para todos los miembros del canal.</span><span class="sxs-lookup"><span data-stu-id="275ef-106">`teams` Also called channel conversations, visible to all members of the channel.</span></span>
* <span data-ttu-id="275ef-107">`personal` Conversaciones entre bots y un único usuario.</span><span class="sxs-lookup"><span data-stu-id="275ef-107">`personal` Conversations between bots and a single user.</span></span>
* <span data-ttu-id="275ef-108">`groupChat` Chatear entre un bot y dos o más usuarios.</span><span class="sxs-lookup"><span data-stu-id="275ef-108">`groupChat` Chat between a bot and two or more users.</span></span> <span data-ttu-id="275ef-109">También habilita el bot en los chats de reuniones.</span><span class="sxs-lookup"><span data-stu-id="275ef-109">Also enables your bot in meeting chats.</span></span>

<span data-ttu-id="275ef-110">Un bot tiene un comportamiento ligeramente diferente en función del tipo de conversación en el que esté involucrado:</span><span class="sxs-lookup"><span data-stu-id="275ef-110">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="275ef-111">Los bots en conversaciones de chat en el grupo y en el canal requieren al usuario que mencione el bot para invocarlo en un canal.</span><span class="sxs-lookup"><span data-stu-id="275ef-111">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="275ef-112">Los bots de una conversación uno a uno no requieren @ mención.</span><span class="sxs-lookup"><span data-stu-id="275ef-112">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="275ef-113">Todos los mensajes enviados por el usuario se enrutarán a su bot.</span><span class="sxs-lookup"><span data-stu-id="275ef-113">All messages sent by the user will be routed to your bot.</span></span>

<span data-ttu-id="275ef-114">Para habilitar el bot en un ámbito determinado, agregue ese ámbito al manifiesto de la [aplicación](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="275ef-114">To enable your bot in a particular scope, add that scope to your [app manifest](~/resources/schema/manifest-schema.md).</span></span>

## <a name="activities"></a><span data-ttu-id="275ef-115">Actividades</span><span class="sxs-lookup"><span data-stu-id="275ef-115">Activities</span></span>

<span data-ttu-id="275ef-116">Cada mensaje es un `Activity` objeto de tipo `messageType: message` .</span><span class="sxs-lookup"><span data-stu-id="275ef-116">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="275ef-117">Cuando un usuario envía un mensaje, Microsoft Teams expone el mensaje a su bot; en concreto, envía un objeto JSON al extremo de mensajería de bot.</span><span class="sxs-lookup"><span data-stu-id="275ef-117">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="275ef-118">El bot examina el mensaje para determinar su tipo y responde en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="275ef-118">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="275ef-119">La conversación básica se controla a través del conector de bot Framework, una única API de REST para permitir que su bot se comunique con Microsoft Teams y otros canales.</span><span class="sxs-lookup"><span data-stu-id="275ef-119">Basic conversation is handled through the Bot Framework Connector, a single REST API to enable your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="275ef-120">El SDK de bot Builder proporciona acceso sencillo a esta API, funcionalidad adicional para administrar el flujo de conversaciones y el estado, y formas sencillas de incorporar servicios cognitivos como el procesamiento de lenguaje natural (NLP).</span><span class="sxs-lookup"><span data-stu-id="275ef-120">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as natural language processing (NLP).</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="275ef-121">Recibir un mensaje</span><span class="sxs-lookup"><span data-stu-id="275ef-121">Receive a message</span></span>

<span data-ttu-id="275ef-122">Para recibir un mensaje de texto, use la `Text` propiedad del `Activity` objeto.</span><span class="sxs-lookup"><span data-stu-id="275ef-122">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="275ef-123">En el controlador de actividad del bot, use el objeto convertir contexto `Activity` para leer una única solicitud de mensaje.</span><span class="sxs-lookup"><span data-stu-id="275ef-123">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="275ef-124">El código siguiente muestra un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="275ef-124">The code below shows an example.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="275ef-125">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="275ef-125">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="275ef-126">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="275ef-126">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            await context.sendActivity(`Echo: '${context.activity.text}'`);
            await next();
        });
    }
}

```

# <a name="python"></a>[<span data-ttu-id="275ef-127">Python</span><span class="sxs-lookup"><span data-stu-id="275ef-127">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="275ef-128">JSON</span><span class="sxs-lookup"><span data-stu-id="275ef-128">JSON</span></span>](#tab/json)

```json
{
    "type": "message",
    "id": "1485983408511",
    "timestamp": "2017-02-01T21:10:07.437Z",
    "localTimestamp": "2017-02-01T14:10:07.437-07:00",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "channelId": "msteams",
    "from": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB39ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen",
        "aadObjectId": "7faf8ab2-3d56-4244-b585-20c8a42ed2b8"
    },
    "conversation": {
        "conversationType": "personal",
        "id": "a:17I0kl9EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-"
    },
    "recipient": {
        "id": "28:c9e8c047-2a74-40a2-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "textFormat": "plain",
    "text": "Hello Teams TestBot",
    "entities": [
      { 
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo"
      }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

---

## <a name="send-a-message"></a><span data-ttu-id="275ef-129">Enviar un mensaje</span><span class="sxs-lookup"><span data-stu-id="275ef-129">Send a message</span></span>

<span data-ttu-id="275ef-130">Para enviar un mensaje de texto, especifique la cadena que desea enviar como la actividad.</span><span class="sxs-lookup"><span data-stu-id="275ef-130">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="275ef-131">En los controladores de actividad del bot, use el método Turn context del objeto `SendActivityAsync` para enviar una respuesta de mensaje único.</span><span class="sxs-lookup"><span data-stu-id="275ef-131">In the bot's activity handlers, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="275ef-132">También puede usar el método del objeto `SendActivitiesAsync` para enviar varias respuestas a la vez.</span><span class="sxs-lookup"><span data-stu-id="275ef-132">You can also use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span> <span data-ttu-id="275ef-133">El siguiente código muestra un ejemplo de cómo enviar un mensaje cuando alguien se agrega a una conversación</span><span class="sxs-lookup"><span data-stu-id="275ef-133">The code below shows an example of sending a message when someone is added to a conversation</span></span>  

# <a name="cnet"></a>[<span data-ttu-id="275ef-134">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="275ef-134">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="275ef-135">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="275ef-135">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            await context.sendActivity('Hello and welcome!');
            await next();
        });
    }
}
```

# <a name="python"></a>[<span data-ttu-id="275ef-136">Python</span><span class="sxs-lookup"><span data-stu-id="275ef-136">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="275ef-137">JSON</span><span class="sxs-lookup"><span data-stu-id="275ef-137">JSON</span></span>](#tab/json)

```json
{
    "text": "hi",
    "textFormat": "plain",
    "type": "message",
    "timestamp": "2019-10-31T20:57:27.2347285Z",
    "localTimestamp": "2019-10-31T13:57:27.2347285-07:00",
    "id": "1572555447214",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "from": {
        "id": "29:1Xv-kvy4dKirR0rZfSF_kAVUzotoT1SXuEzkC9XGkuZng8YBw8qyu5uh4128fQRjlGgvEiRLx-0XP4KYMwcgdZw",
        "name": "Jane Doe",
        "aadObjectId": "df486eae-88fd-42a5-b45e-c581588186db"
    },
    "conversation": {
        "conversationType": "personal",
        "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
        "id": "a:1oAmWTVBBe9E0JrpGxauqNyx4CCE_iQf2ZuWon9D42722Fon3wYIpbhgbRChE3wgVS1Gwl9zS1pZy4FSu6-x1vGEq5KBQK-EbBgyPyeP_C-lbLBY3vxnGk9m9D_282jbg"
    },
    "recipient": {
        "id": "28:5baea8d1-d4ea-43a1-b101-882f4c8d9cb4",
        "name": "Imported Bot"
    },
    "entities": [
        {
            "locale": "en-US",
            "country": "US",
            "platform": "Windows",
            "type": "clientInfo"
        }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

---

## <a name="teams-channel-data"></a><span data-ttu-id="275ef-138">Datos del canal de Teams</span><span class="sxs-lookup"><span data-stu-id="275ef-138">Teams channel data</span></span>

<span data-ttu-id="275ef-139">El `channelData` objeto contiene información específica de Microsoft Teams y es la fuente definitiva de los identificadores de equipo y de canal.</span><span class="sxs-lookup"><span data-stu-id="275ef-139">The `channelData` object contains Teams-specific information and is the definitive source for team and channel IDs.</span></span> <span data-ttu-id="275ef-140">Es posible que necesite almacenar en caché y usar estos identificadores como claves para el almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="275ef-140">You may need to cache and use these ids as keys for local storage.</span></span> <span data-ttu-id="275ef-141">La `TeamsActivityHandler` en el SDK suele extraer información importante del `channelData` objeto para que sea más fácil de acceder, pero siempre puede tener acceso a la información original del `turnContext` objeto.</span><span class="sxs-lookup"><span data-stu-id="275ef-141">The `TeamsActivityHandler` in the SDK will typically pull out important information from the `channelData` object to make it more easily accessible, however you can always access the original information from the `turnContext` object.</span></span>

<span data-ttu-id="275ef-142">El `channelData` objeto no está incluido en los mensajes de las conversaciones personales, ya que éstos tienen lugar fuera de cualquier canal.</span><span class="sxs-lookup"><span data-stu-id="275ef-142">The `channelData` object is not included in messages in personal conversations since these take place outside of any channel.</span></span>

<span data-ttu-id="275ef-143">Un objeto channelData típico de una actividad enviada a su bot contiene la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="275ef-143">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="275ef-144">`eventType` Tipo de evento de Teams; solo se pasa en casos de [eventos de modificación de canal](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="275ef-144">`eventType` Teams event type; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span></span>
* <span data-ttu-id="275ef-145">`tenant.id` IDENTIFICADOR de inquilino de Azure Active Directory; se pasan en todos los contextos</span><span class="sxs-lookup"><span data-stu-id="275ef-145">`tenant.id` Azure Active Directory tenant ID; passed in all contexts</span></span>
* <span data-ttu-id="275ef-146">`team` Solo se pasa en contextos de canal, no en chat personal.</span><span class="sxs-lookup"><span data-stu-id="275ef-146">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="275ef-147">`id` GUID para el canal</span><span class="sxs-lookup"><span data-stu-id="275ef-147">`id` GUID for the channel</span></span>
  * <span data-ttu-id="275ef-148">`name` Nombre del equipo; solo se pasa en casos de [eventos de cambio de nombre de equipo](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="275ef-148">`name` Name of the team; passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span></span>
* <span data-ttu-id="275ef-149">`channel` Solo se pasa en contextos de canal cuando se menciona el bot o para eventos en los canales en equipos en los que se ha agregado el bot</span><span class="sxs-lookup"><span data-stu-id="275ef-149">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added</span></span>
  * <span data-ttu-id="275ef-150">`id` GUID para el canal</span><span class="sxs-lookup"><span data-stu-id="275ef-150">`id` GUID for the channel</span></span>
  * <span data-ttu-id="275ef-151">`name` Nombre del canal; se pasa solo en casos de [eventos de modificación de canal](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="275ef-151">`name` Channel name; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="275ef-152">`channelData.teamsTeamId` En desuso.</span><span class="sxs-lookup"><span data-stu-id="275ef-152">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="275ef-153">Esta propiedad se incluye únicamente para la compatibilidad con versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="275ef-153">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="275ef-154">`channelData.teamsChannelId` En desuso.</span><span class="sxs-lookup"><span data-stu-id="275ef-154">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="275ef-155">Esta propiedad se incluye únicamente para la compatibilidad con versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="275ef-155">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="275ef-156">Ejemplo de objeto channelData (evento channelCreated)</span><span class="sxs-lookup"><span data-stu-id="275ef-156">Example channelData object (channelCreated event)</span></span>

```json
"channelData": {
    "eventType": "channelCreated",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    },
    "channel": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype",
        "name": "My New Channel"
    },
    "team": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype"
    }
}
```

## <a name="message-content"></a><span data-ttu-id="275ef-157">Contenido del mensaje</span><span class="sxs-lookup"><span data-stu-id="275ef-157">Message content</span></span>

<span data-ttu-id="275ef-158">El bot puede enviar texto enriquecido, imágenes y tarjetas.</span><span class="sxs-lookup"><span data-stu-id="275ef-158">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="275ef-159">Los usuarios pueden enviar texto enriquecido e imágenes a su bot.</span><span class="sxs-lookup"><span data-stu-id="275ef-159">Users can send rich text and pictures to your bot.</span></span>

| <span data-ttu-id="275ef-160">Formato</span><span class="sxs-lookup"><span data-stu-id="275ef-160">Format</span></span>    | <span data-ttu-id="275ef-161">De un usuario a un bot</span><span class="sxs-lookup"><span data-stu-id="275ef-161">From user to bot</span></span> | <span data-ttu-id="275ef-162">De bot a User</span><span class="sxs-lookup"><span data-stu-id="275ef-162">From bot to user</span></span> | <span data-ttu-id="275ef-163">Notas</span><span class="sxs-lookup"><span data-stu-id="275ef-163">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="275ef-164">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="275ef-164">Rich text</span></span> | <span data-ttu-id="275ef-165">✔</span><span class="sxs-lookup"><span data-stu-id="275ef-165">✔</span></span>                | <span data-ttu-id="275ef-166">✔</span><span class="sxs-lookup"><span data-stu-id="275ef-166">✔</span></span>                |                                                                                         |
| <span data-ttu-id="275ef-167">Imágenes</span><span class="sxs-lookup"><span data-stu-id="275ef-167">Pictures</span></span>  | <span data-ttu-id="275ef-168">✔</span><span class="sxs-lookup"><span data-stu-id="275ef-168">✔</span></span>                | <span data-ttu-id="275ef-169">✔</span><span class="sxs-lookup"><span data-stu-id="275ef-169">✔</span></span>                | <span data-ttu-id="275ef-170">Máximo de 1024 × 1024 y 1 MB en formato PNG, JPEG o GIF; no se admiten GIF animados</span><span class="sxs-lookup"><span data-stu-id="275ef-170">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported</span></span>  |
| <span data-ttu-id="275ef-171">Tarjetas</span><span class="sxs-lookup"><span data-stu-id="275ef-171">Cards</span></span>     | <span data-ttu-id="275ef-172">✖</span><span class="sxs-lookup"><span data-stu-id="275ef-172">✖</span></span>                | <span data-ttu-id="275ef-173">✔</span><span class="sxs-lookup"><span data-stu-id="275ef-173">✔</span></span>                | <span data-ttu-id="275ef-174">Ver la [referencia de la tarjeta Teams](~/task-modules-and-cards/cards/cards-reference.md) para tarjetas compatibles</span><span class="sxs-lookup"><span data-stu-id="275ef-174">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards</span></span> |
| <span data-ttu-id="275ef-175">Emojis</span><span class="sxs-lookup"><span data-stu-id="275ef-175">Emojis</span></span>    | <span data-ttu-id="275ef-176">✖</span><span class="sxs-lookup"><span data-stu-id="275ef-176">✖</span></span>                | <span data-ttu-id="275ef-177">✔</span><span class="sxs-lookup"><span data-stu-id="275ef-177">✔</span></span>                | <span data-ttu-id="275ef-178">Actualmente, los equipos son compatibles con emojis mediante UTF-16 (como U + 1F600 para la cara Grinning).</span><span class="sxs-lookup"><span data-stu-id="275ef-178">Teams currently supports emojis via UTF-16 (such as U+1F600 for grinning face)</span></span>          |

## <a name="adding-notifications-to-your-message"></a><span data-ttu-id="275ef-179">Adición de notificaciones al mensaje</span><span class="sxs-lookup"><span data-stu-id="275ef-179">Adding notifications to your message</span></span>

<span data-ttu-id="275ef-180">Las notificaciones alertan a los usuarios sobre nuevas tareas, menciones y comentarios relacionados con el trabajo en el que están trabajando, o bien deben consultarse mediante la inserción de un aviso en su fuente de actividades.</span><span class="sxs-lookup"><span data-stu-id="275ef-180">Notifications alert users about new tasks, mentions and comments related to what they are working on, or need to look at by inserting a notice into their Activity Feed.</span></span> <span data-ttu-id="275ef-181">Puede establecer notificaciones para que desencadenen desde el mensaje de bot estableciendo la `TeamsChannelData` propiedad Objects `Notification.Alert` en true.</span><span class="sxs-lookup"><span data-stu-id="275ef-181">You can set notifications to trigger from your bot message by setting the `TeamsChannelData` objects `Notification.Alert` property to true.</span></span> <span data-ttu-id="275ef-182">El hecho de que se genere una notificación dependerá en última instancia de la configuración de Teams del usuario individual y no podrá reemplazar esta configuración mediante programación.</span><span class="sxs-lookup"><span data-stu-id="275ef-182">Whether or not a notification is raised will ultimately depend on the individual user's Teams settings and you cannot programmatically override these settings.</span></span> <span data-ttu-id="275ef-183">El tipo de notificación será un banner, un banner o un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="275ef-183">The type of notification will be either a banner or both a banner and an email.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="275ef-184">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="275ef-184">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="275ef-185">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="275ef-185">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="275ef-186">Python</span><span class="sxs-lookup"><span data-stu-id="275ef-186">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="275ef-187">JSON</span><span class="sxs-lookup"><span data-stu-id="275ef-187">JSON</span></span>](#tab/json)

```json
{
  "type": "message",
  "timestamp": "2017-04-24T21:46:00.9663655Z",
  "localTimestamp": "2017-04-24T14:46:00.9663655-07:00",
  "serviceUrl": "https://callback.com",
  "channelId": "msteams",
  "from": {
    "id": "28:e4fda94a-4b80-40eb-9bf0-6314491bc793",
    "name": "The bot"
  },
  "conversation": {
    "id": "a:1pL6i0oY3C0K8oAj8"
  },
  "recipient": {
    "id": "29:1rsVJmSSFMScF0YFyCXpvNWlo",
    "name": "User"
  },
  "text": "John Phillips assigned you a weekly todo",
  "summary": "Don't forget to meet with Marketing next week",
  "channelData": {
    "notification": {
      "alert": true
    }
  },
  "replyToId": "1493070356924"
}
```

---

## <a name="picture-messages"></a><span data-ttu-id="275ef-188">Mensajes de imagen</span><span class="sxs-lookup"><span data-stu-id="275ef-188">Picture messages</span></span>

<span data-ttu-id="275ef-189">Las imágenes se envían agregando datos adjuntos a un mensaje.</span><span class="sxs-lookup"><span data-stu-id="275ef-189">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="275ef-190">Puede encontrar más información sobre los datos adjuntos en la [documentación de bot Framework](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0).</span><span class="sxs-lookup"><span data-stu-id="275ef-190">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0).</span></span>

<span data-ttu-id="275ef-191">Las imágenes pueden tener como máximo 1024 x 1024 y 1 MB en formato PNG, JPEG o GIF; GIF animado no es compatible.</span><span class="sxs-lookup"><span data-stu-id="275ef-191">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not supported.</span></span>

<span data-ttu-id="275ef-192">Le recomendamos que especifique el alto y el ancho de cada imagen utilizando XML.</span><span class="sxs-lookup"><span data-stu-id="275ef-192">We recommend that you specify the height and width of each image by using XML.</span></span> <span data-ttu-id="275ef-193">Si usa Markdown, el tamaño de imagen predeterminado es de 256 × 256.</span><span class="sxs-lookup"><span data-stu-id="275ef-193">If you use Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="275ef-194">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="275ef-194">For example:</span></span>

* <span data-ttu-id="275ef-195">Utilizados `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="275ef-195">Use - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="275ef-196">No use- `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="275ef-196">Don't use - `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="next-steps"></a><span data-ttu-id="275ef-197">Siguientes pasos</span><span class="sxs-lookup"><span data-stu-id="275ef-197">Next steps</span></span>

* [<span data-ttu-id="275ef-198">Envío de mensajes proactivos</span><span class="sxs-lookup"><span data-stu-id="275ef-198">Sending proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
* [<span data-ttu-id="275ef-199">Suscribirse a eventos de conversación</span><span class="sxs-lookup"><span data-stu-id="275ef-199">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

---
title: Conceptos básicos de la conversación
description: describe formas de tener una conversación con un bot de Microsoft Teams
ms.topic: overview
ms.author: anclear
keyword: conversations basics receive message send message picture message channel data adaptive cards
ms.openlocfilehash: a045f02a146782ebdbbbb14fe5f4187cb517a109
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093960"
---
# <a name="conversation-basics"></a><span data-ttu-id="caf41-103">Conceptos básicos de la conversación</span><span class="sxs-lookup"><span data-stu-id="caf41-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="caf41-104">Una conversación es una serie de mensajes enviados entre el bot y uno o más usuarios.</span><span class="sxs-lookup"><span data-stu-id="caf41-104">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="caf41-105">Hay tres tipos de conversaciones, también denominadas ámbitos en Teams:</span><span class="sxs-lookup"><span data-stu-id="caf41-105">There are three types of conversations, also called scopes in Teams:</span></span>

| <span data-ttu-id="caf41-106">Tipo de conversación</span><span class="sxs-lookup"><span data-stu-id="caf41-106">Conversation type</span></span> | <span data-ttu-id="caf41-107">Descripción</span><span class="sxs-lookup"><span data-stu-id="caf41-107">Description</span></span> |
| ------- | ----------- |
|  `teams` | <span data-ttu-id="caf41-108">También se denominan conversaciones de canal, visibles para todos los miembros del canal.</span><span class="sxs-lookup"><span data-stu-id="caf41-108">Also called channel conversations, visible to all members of the channel.</span></span> |
| `personal` | <span data-ttu-id="caf41-109">Conversaciones entre bots y un solo usuario.</span><span class="sxs-lookup"><span data-stu-id="caf41-109">Conversations between bots and a single user.</span></span> |
| `groupChat` | <span data-ttu-id="caf41-110">Chatear entre un bot y dos o más usuarios.</span><span class="sxs-lookup"><span data-stu-id="caf41-110">Chat between a bot and two or more users.</span></span> <span data-ttu-id="caf41-111">También habilita el bot en los chats de reuniones.</span><span class="sxs-lookup"><span data-stu-id="caf41-111">Also enables your bot in meeting chats.</span></span> |

<span data-ttu-id="caf41-112">Un bot se comporta de forma ligeramente diferente en función del tipo de conversación en la que esté implicado:</span><span class="sxs-lookup"><span data-stu-id="caf41-112">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="caf41-113">Los bots en conversaciones de chat de canal y grupo requieren que el usuario @ mencione el bot para invocarlo en un canal.</span><span class="sxs-lookup"><span data-stu-id="caf41-113">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="caf41-114">Los bots de una conversación uno a uno no requieren una mención @.</span><span class="sxs-lookup"><span data-stu-id="caf41-114">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="caf41-115">Todos los mensajes enviados por el usuario se enruta al bot.</span><span class="sxs-lookup"><span data-stu-id="caf41-115">All messages sent by the user routes to your bot.</span></span>

<span data-ttu-id="caf41-116">Para habilitar el bot en un ámbito determinado, agregue ese ámbito al manifiesto [de la aplicación.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="caf41-116">To enable your bot in a particular scope, add that scope to your [app manifest](~/resources/schema/manifest-schema.md).</span></span>

## <a name="activities"></a><span data-ttu-id="caf41-117">Actividades</span><span class="sxs-lookup"><span data-stu-id="caf41-117">Activities</span></span>

<span data-ttu-id="caf41-118">Cada mensaje es un `Activity` objeto de tipo `messageType: message` .</span><span class="sxs-lookup"><span data-stu-id="caf41-118">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="caf41-119">Cuando un usuario envía un mensaje, Teams publica el mensaje en el bot; específicamente, envía un objeto JSON al extremo de mensajería del bot.</span><span class="sxs-lookup"><span data-stu-id="caf41-119">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="caf41-120">El bot examina el mensaje para determinar su tipo y responde en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="caf41-120">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="caf41-121">Las conversaciones básicas se controlan a través de Bot Framework Connector, una única API de REST.</span><span class="sxs-lookup"><span data-stu-id="caf41-121">Basic conversations are handled through the Bot Framework Connector, a single REST API.</span></span> <span data-ttu-id="caf41-122">Esta API permite que el bot se comunique con Teams y otros canales.</span><span class="sxs-lookup"><span data-stu-id="caf41-122">This API enables your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="caf41-123">El SDK de Bot Builder proporciona un fácil acceso a esta API, funciones adicionales para administrar el estado y el flujo de conversación, y formas sencillas de incorporar servicios cognitivas, como el procesamiento de lenguaje natural (NLP).</span><span class="sxs-lookup"><span data-stu-id="caf41-123">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as Natural Language Processing (NLP).</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="caf41-124">Recibir un mensaje</span><span class="sxs-lookup"><span data-stu-id="caf41-124">Receive a message</span></span>

<span data-ttu-id="caf41-125">Para recibir un mensaje de texto, utilice la `Text` propiedad del `Activity` objeto.</span><span class="sxs-lookup"><span data-stu-id="caf41-125">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="caf41-126">En el controlador de actividad del bot, use el objeto turn context `Activity` para leer una sola solicitud de mensaje.</span><span class="sxs-lookup"><span data-stu-id="caf41-126">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="caf41-127">El código siguiente muestra un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="caf41-127">The following code shows an example.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="caf41-128">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="caf41-128">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="caf41-129">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="caf41-129">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="caf41-130">Python</span><span class="sxs-lookup"><span data-stu-id="caf41-130">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="caf41-131">JSON</span><span class="sxs-lookup"><span data-stu-id="caf41-131">JSON</span></span>](#tab/json)

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

## <a name="send-a-message"></a><span data-ttu-id="caf41-132">Enviar un mensaje</span><span class="sxs-lookup"><span data-stu-id="caf41-132">Send a message</span></span>

<span data-ttu-id="caf41-133">Para enviar un mensaje de texto, especifique la cadena que desea enviar como actividad.</span><span class="sxs-lookup"><span data-stu-id="caf41-133">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="caf41-134">En el controlador de actividad del bot, use el método del objeto turn context `SendActivityAsync` para enviar una única respuesta de mensaje.</span><span class="sxs-lookup"><span data-stu-id="caf41-134">In the bot's activity handler, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="caf41-135">Utilice el método del objeto `SendActivitiesAsync` para enviar varias respuestas a la vez.</span><span class="sxs-lookup"><span data-stu-id="caf41-135">Use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span> <span data-ttu-id="caf41-136">El siguiente código muestra un ejemplo de envío de un mensaje cuando alguien se agrega a una conversación.</span><span class="sxs-lookup"><span data-stu-id="caf41-136">The following code shows an example of sending a message when someone is added to a conversation.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="caf41-137">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="caf41-137">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="caf41-138">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="caf41-138">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="caf41-139">Python</span><span class="sxs-lookup"><span data-stu-id="caf41-139">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="caf41-140">JSON</span><span class="sxs-lookup"><span data-stu-id="caf41-140">JSON</span></span>](#tab/json)

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

## <a name="teams-channel-data"></a><span data-ttu-id="caf41-141">Datos del canal de Teams</span><span class="sxs-lookup"><span data-stu-id="caf41-141">Teams channel data</span></span>

<span data-ttu-id="caf41-142">El `channelData` objeto contiene información específica de Teams y es una fuente definitiva de los IDs de equipo y canal.</span><span class="sxs-lookup"><span data-stu-id="caf41-142">The `channelData` object contains Teams-specific information and is a definitive source for team and channel IDs.</span></span> <span data-ttu-id="caf41-143">Es posible que tenga que almacenar en caché y usar estos IDs como claves para el almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="caf41-143">You may need to cache and use these IDs as keys for local storage.</span></span> <span data-ttu-id="caf41-144">En `TeamsActivityHandler` el SDK, normalmente se extrae información importante del `channelData` objeto para que sea fácilmente accesible.</span><span class="sxs-lookup"><span data-stu-id="caf41-144">The `TeamsActivityHandler` in the SDK, typically pulls out important information from the `channelData` object to make it easily accessible.</span></span> <span data-ttu-id="caf41-145">Sin embargo, siempre puede tener acceso a los datos originales desde el `turnContext` objeto.</span><span class="sxs-lookup"><span data-stu-id="caf41-145">However, you can always access the original data from the `turnContext` object.</span></span>

<span data-ttu-id="caf41-146">El `channelData` objeto no se incluye en los mensajes de las conversaciones personales, ya que tienen lugar fuera de cualquier canal.</span><span class="sxs-lookup"><span data-stu-id="caf41-146">The `channelData` object is not included in messages in personal conversations, as these take place outside of any channel.</span></span>

<span data-ttu-id="caf41-147">Un objeto channelData típico de una actividad enviada al bot contiene la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="caf41-147">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="caf41-148">`eventType`Tipo de evento de Teams; se pasa solo en casos de [eventos de modificación de canal.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="caf41-148">`eventType` Teams event type; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="caf41-149">`tenant.id` Identificador de inquilino de Azure Active Directory, pasado en todos los contextos.</span><span class="sxs-lookup"><span data-stu-id="caf41-149">`tenant.id` Azure Active Directory tenant ID, passed in all contexts.</span></span>
* <span data-ttu-id="caf41-150">`team` Se pasa solo en contextos de canal, no en chat personal.</span><span class="sxs-lookup"><span data-stu-id="caf41-150">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="caf41-151">`id` GUID del canal.</span><span class="sxs-lookup"><span data-stu-id="caf41-151">`id` GUID for the channel.</span></span>
  * <span data-ttu-id="caf41-152">`name`Nombre del equipo; se pasa solo en los casos de [eventos de cambio de nombre de equipo.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="caf41-152">`name` Name of the team; passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="caf41-153">`channel` Se pasa solo en contextos de canal cuando se menciona el bot o para eventos en canales de equipos donde se ha agregado el bot.</span><span class="sxs-lookup"><span data-stu-id="caf41-153">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added.</span></span>
  * <span data-ttu-id="caf41-154">`id` GUID del canal.</span><span class="sxs-lookup"><span data-stu-id="caf41-154">`id` GUID for the channel.</span></span>
  * <span data-ttu-id="caf41-155">`name`Nombre del canal; se pasa solo en casos de [eventos de modificación de canal.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="caf41-155">`name` Channel name; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="caf41-156">`channelData.teamsTeamId` En desuso.</span><span class="sxs-lookup"><span data-stu-id="caf41-156">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="caf41-157">Esta propiedad se incluye solo por compatibilidad con versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="caf41-157">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="caf41-158">`channelData.teamsChannelId` En desuso.</span><span class="sxs-lookup"><span data-stu-id="caf41-158">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="caf41-159">Esta propiedad se incluye solo por compatibilidad con versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="caf41-159">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="caf41-160">Ejemplo de objeto channelData (evento channelCreated)</span><span class="sxs-lookup"><span data-stu-id="caf41-160">Example channelData object (channelCreated event)</span></span>

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

## <a name="message-content"></a><span data-ttu-id="caf41-161">Contenido del mensaje</span><span class="sxs-lookup"><span data-stu-id="caf41-161">Message content</span></span>

<span data-ttu-id="caf41-162">El bot puede enviar texto enriquecido, imágenes y tarjetas.</span><span class="sxs-lookup"><span data-stu-id="caf41-162">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="caf41-163">Los usuarios pueden enviar texto enriquecido e imágenes al bot.</span><span class="sxs-lookup"><span data-stu-id="caf41-163">Users can send rich text and pictures to your bot.</span></span>

| <span data-ttu-id="caf41-164">Formato</span><span class="sxs-lookup"><span data-stu-id="caf41-164">Format</span></span>    | <span data-ttu-id="caf41-165">De usuario a bot</span><span class="sxs-lookup"><span data-stu-id="caf41-165">From user to bot</span></span> | <span data-ttu-id="caf41-166">De bot a usuario</span><span class="sxs-lookup"><span data-stu-id="caf41-166">From bot to user</span></span> | <span data-ttu-id="caf41-167">Notas</span><span class="sxs-lookup"><span data-stu-id="caf41-167">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="caf41-168">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="caf41-168">Rich text</span></span> | <span data-ttu-id="caf41-169">✔</span><span class="sxs-lookup"><span data-stu-id="caf41-169">✔</span></span>                | <span data-ttu-id="caf41-170">✔</span><span class="sxs-lookup"><span data-stu-id="caf41-170">✔</span></span>                |                                                                                         |
| <span data-ttu-id="caf41-171">Imágenes</span><span class="sxs-lookup"><span data-stu-id="caf41-171">Pictures</span></span>  | <span data-ttu-id="caf41-172">✔</span><span class="sxs-lookup"><span data-stu-id="caf41-172">✔</span></span>                | <span data-ttu-id="caf41-173">✔</span><span class="sxs-lookup"><span data-stu-id="caf41-173">✔</span></span>                | <span data-ttu-id="caf41-174">Máximo de 1024×1024 y 1 MB en formato PNG, JPEG o GIF; GIF animado no se admite</span><span class="sxs-lookup"><span data-stu-id="caf41-174">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported</span></span>  |
| <span data-ttu-id="caf41-175">Tarjetas</span><span class="sxs-lookup"><span data-stu-id="caf41-175">Cards</span></span>     | <span data-ttu-id="caf41-176">✖</span><span class="sxs-lookup"><span data-stu-id="caf41-176">✖</span></span>                | <span data-ttu-id="caf41-177">✔</span><span class="sxs-lookup"><span data-stu-id="caf41-177">✔</span></span>                | <span data-ttu-id="caf41-178">Ver la referencia [de tarjetas de Teams](~/task-modules-and-cards/cards/cards-reference.md) para las tarjetas compatibles</span><span class="sxs-lookup"><span data-stu-id="caf41-178">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards</span></span> |
| <span data-ttu-id="caf41-179">Emojis</span><span class="sxs-lookup"><span data-stu-id="caf41-179">Emojis</span></span>    | <span data-ttu-id="caf41-180">✖</span><span class="sxs-lookup"><span data-stu-id="caf41-180">✖</span></span>                | <span data-ttu-id="caf41-181">✔</span><span class="sxs-lookup"><span data-stu-id="caf41-181">✔</span></span>                | <span data-ttu-id="caf41-182">Actualmente, Teams admite emojis a través de UTF-16 (como U+1F600 para el movimiento facial)</span><span class="sxs-lookup"><span data-stu-id="caf41-182">Teams currently supports emojis via UTF-16 (such as U+1F600 for grinning face)</span></span>          |

## <a name="adding-notifications-to-your-message"></a><span data-ttu-id="caf41-183">Agregar notificaciones al mensaje</span><span class="sxs-lookup"><span data-stu-id="caf41-183">Adding notifications to your message</span></span>

<span data-ttu-id="caf41-184">Las notificaciones alertan a los usuarios sobre nuevas tareas, menciones y comentarios relacionados con lo que están trabajando o necesitan ver insertando un aviso en su fuente de actividades.</span><span class="sxs-lookup"><span data-stu-id="caf41-184">Notifications alert users about new tasks, mentions, and comments related to what they are working on or need to look at by inserting a notice into their activity feed.</span></span> <span data-ttu-id="caf41-185">Puede establecer las notificaciones para que se desencadene desde el mensaje de bot estableciendo la `TeamsChannelData` propiedad `Notification.Alert` objects en true.</span><span class="sxs-lookup"><span data-stu-id="caf41-185">You can set notifications to trigger from your bot-message by setting the `TeamsChannelData` objects `Notification.Alert` property to true.</span></span> <span data-ttu-id="caf41-186">La generación o no de una notificación depende en última instancia de la configuración de Teams del usuario individual y no se puede invalidar mediante programación.</span><span class="sxs-lookup"><span data-stu-id="caf41-186">Whether or not a notification is raised ultimately depends on the individual user's Teams settings and you cannot programmatically override these settings.</span></span> <span data-ttu-id="caf41-187">El tipo de notificación es un banner o un banner y un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="caf41-187">The type of notification is either a banner or both a banner and an email.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="caf41-188">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="caf41-188">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="caf41-189">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="caf41-189">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="caf41-190">Python</span><span class="sxs-lookup"><span data-stu-id="caf41-190">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="caf41-191">JSON</span><span class="sxs-lookup"><span data-stu-id="caf41-191">JSON</span></span>](#tab/json)

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

## <a name="picture-messages"></a><span data-ttu-id="caf41-192">Mensajes de imagen</span><span class="sxs-lookup"><span data-stu-id="caf41-192">Picture messages</span></span>

<span data-ttu-id="caf41-193">Las imágenes se envían agregando datos adjuntos a un mensaje.</span><span class="sxs-lookup"><span data-stu-id="caf41-193">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="caf41-194">Puede encontrar más información sobre los datos adjuntos en la [documentación de Bot Framework.](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)</span><span class="sxs-lookup"><span data-stu-id="caf41-194">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments).</span></span>

<span data-ttu-id="caf41-195">Las imágenes pueden tener como máximo 1024×1024 y 1 MB en formato PNG, JPEG o GIF.</span><span class="sxs-lookup"><span data-stu-id="caf41-195">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="caf41-196">Gif animado no es compatible.</span><span class="sxs-lookup"><span data-stu-id="caf41-196">Animated GIF is not supported.</span></span>

<span data-ttu-id="caf41-197">Especifique siempre el alto y el ancho de cada imagen mediante XML.</span><span class="sxs-lookup"><span data-stu-id="caf41-197">Always specify the height and width of each image by using XML.</span></span> <span data-ttu-id="caf41-198">En Markdown, el tamaño de imagen predeterminado es 256×256.</span><span class="sxs-lookup"><span data-stu-id="caf41-198">In Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="caf41-199">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="caf41-199">For example:</span></span>

* <span data-ttu-id="caf41-200">Use - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="caf41-200">Use - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="caf41-201">No usar: `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="caf41-201">Don't use - `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="caf41-202">Tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="caf41-202">Adaptive cards</span></span>

<span data-ttu-id="caf41-203">Usa el siguiente código para enviar una tarjeta adaptable simple:</span><span class="sxs-lookup"><span data-stu-id="caf41-203">Use the following code to send a simple adaptive card:</span></span>

```json
{
    "type": "AdaptiveCard",
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.5",
    "body": [
    {
        "items": [
        {
            "size": "large",
            "text": " Simple Adaptivecard Example with a Textbox",
            "type": "TextBlock",
            "weight": "bolder",
            "wrap": true
        },
        ],
        "spacing": "extraLarge",
        "type": "Container",
        "verticalContentAlignment": "center"
    }
    ]
}
```

<span data-ttu-id="caf41-204">Para obtener más información acerca de las tarjetas y las tarjetas de los bots, consulte [la documentación sobre tarjetas.](~/task-modules-and-cards/what-are-cards.md)</span><span class="sxs-lookup"><span data-stu-id="caf41-204">To know more about cards and cards in bots, see [cards documentation](~/task-modules-and-cards/what-are-cards.md).</span></span>
<span data-ttu-id="caf41-205">Cuando una respuesta contiene mensajes de texto y datos adjuntos, ambas respuestas se envían por separado.</span><span class="sxs-lookup"><span data-stu-id="caf41-205">When a response contains text messages and attachments, both responses are sent separately.</span></span> <span data-ttu-id="caf41-206">Los datos adjuntos se envían después del mensaje de texto.</span><span class="sxs-lookup"><span data-stu-id="caf41-206">The attachment is sent after the text message.</span></span>

## <a name="code-sample"></a><span data-ttu-id="caf41-207">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="caf41-207">Code sample</span></span>
|<span data-ttu-id="caf41-208">**Nombre de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="caf41-208">**Sample name**</span></span> | <span data-ttu-id="caf41-209">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="caf41-209">**Description**</span></span> | <span data-ttu-id="caf41-210">**. NETCore**</span><span class="sxs-lookup"><span data-stu-id="caf41-210">**.NETCore**</span></span> | <span data-ttu-id="caf41-211">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="caf41-211">**JavaScript**</span></span> | <span data-ttu-id="caf41-212">**Python**</span><span class="sxs-lookup"><span data-stu-id="caf41-212">**Python**</span></span>|
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="caf41-213">Bot de conversación de Teams</span><span class="sxs-lookup"><span data-stu-id="caf41-213">Teams Conversation Bot</span></span> | <span data-ttu-id="caf41-214">Control de eventos de mensajería y conversación.</span><span class="sxs-lookup"><span data-stu-id="caf41-214">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="caf41-215">View</span><span class="sxs-lookup"><span data-stu-id="caf41-215">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="caf41-216">View</span><span class="sxs-lookup"><span data-stu-id="caf41-216">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [<span data-ttu-id="caf41-217">View</span><span class="sxs-lookup"><span data-stu-id="caf41-217">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-steps"></a><span data-ttu-id="caf41-218">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="caf41-218">Next steps</span></span>

* [<span data-ttu-id="caf41-219">Envío de mensajes proactivos</span><span class="sxs-lookup"><span data-stu-id="caf41-219">Sending proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
* [<span data-ttu-id="caf41-220">Suscribirse a eventos de conversación</span><span class="sxs-lookup"><span data-stu-id="caf41-220">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

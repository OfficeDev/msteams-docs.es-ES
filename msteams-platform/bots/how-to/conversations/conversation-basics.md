---
title: Conceptos básicos de la conversación
author: clearab
description: Cómo tener una conversación con un bot de Microsoft Teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 6f7e7a4d1be08126c96dff07ddbc3e1156700a90
ms.sourcegitcommit: 94ad961ecd002805b4e0424601d1c0ec191ff376
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2021
ms.locfileid: "50075696"
---
# <a name="conversation-basics"></a><span data-ttu-id="e36dd-103">Conceptos básicos de la conversación</span><span class="sxs-lookup"><span data-stu-id="e36dd-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="e36dd-104">Una conversación es una serie de mensajes enviados entre el bot y uno o más usuarios.</span><span class="sxs-lookup"><span data-stu-id="e36dd-104">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="e36dd-105">Hay tres tipos de conversaciones (también denominadas ámbitos) en Teams:</span><span class="sxs-lookup"><span data-stu-id="e36dd-105">There are three kinds of conversations (also called scopes) in Teams:</span></span>

* <span data-ttu-id="e36dd-106">`teams` También se denominan conversaciones de canal, visibles para todos los miembros del canal.</span><span class="sxs-lookup"><span data-stu-id="e36dd-106">`teams` Also called channel conversations, visible to all members of the channel.</span></span>
* <span data-ttu-id="e36dd-107">`personal` Conversaciones entre bots y un solo usuario.</span><span class="sxs-lookup"><span data-stu-id="e36dd-107">`personal` Conversations between bots and a single user.</span></span>
* <span data-ttu-id="e36dd-108">`groupChat` Chatear entre un bot y dos o más usuarios.</span><span class="sxs-lookup"><span data-stu-id="e36dd-108">`groupChat` Chat between a bot and two or more users.</span></span> <span data-ttu-id="e36dd-109">También habilita el bot en los chats de reuniones.</span><span class="sxs-lookup"><span data-stu-id="e36dd-109">Also enables your bot in meeting chats.</span></span>

<span data-ttu-id="e36dd-110">Un bot se comporta de forma ligeramente diferente en función del tipo de conversación en la que esté implicado:</span><span class="sxs-lookup"><span data-stu-id="e36dd-110">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="e36dd-111">Los bots en conversaciones de chat de canal y grupo requieren que el usuario @ mencione el bot para invocarlo en un canal.</span><span class="sxs-lookup"><span data-stu-id="e36dd-111">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="e36dd-112">Los bots de una conversación uno a uno no requieren una mención @.</span><span class="sxs-lookup"><span data-stu-id="e36dd-112">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="e36dd-113">Todos los mensajes enviados por el usuario se enrutarán al bot.</span><span class="sxs-lookup"><span data-stu-id="e36dd-113">All messages sent by the user will be routed to your bot.</span></span>

<span data-ttu-id="e36dd-114">Para habilitar el bot en un ámbito determinado, agregue ese ámbito al manifiesto [de la aplicación.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="e36dd-114">To enable your bot in a particular scope, add that scope to your [app manifest](~/resources/schema/manifest-schema.md).</span></span>

## <a name="activities"></a><span data-ttu-id="e36dd-115">Actividades</span><span class="sxs-lookup"><span data-stu-id="e36dd-115">Activities</span></span>

<span data-ttu-id="e36dd-116">Cada mensaje es un `Activity` objeto de tipo `messageType: message` .</span><span class="sxs-lookup"><span data-stu-id="e36dd-116">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="e36dd-117">Cuando un usuario envía un mensaje, Teams publica el mensaje en el bot; específicamente, envía un objeto JSON al extremo de mensajería del bot.</span><span class="sxs-lookup"><span data-stu-id="e36dd-117">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="e36dd-118">El bot examina el mensaje para determinar su tipo y responde en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="e36dd-118">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="e36dd-119">La conversación básica se controla a través de Bot Framework Connector, una única API de REST para permitir que el bot se comunique con Teams y otros canales.</span><span class="sxs-lookup"><span data-stu-id="e36dd-119">Basic conversation is handled through the Bot Framework Connector, a single REST API to enable your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="e36dd-120">El SDK de Bot Builder proporciona fácil acceso a esta API, funcionalidad adicional para administrar el estado y el flujo de conversación, y formas sencillas de incorporar servicios cognitivas, como el procesamiento de lenguaje natural (NLP).</span><span class="sxs-lookup"><span data-stu-id="e36dd-120">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as natural language processing (NLP).</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="e36dd-121">Recibir un mensaje</span><span class="sxs-lookup"><span data-stu-id="e36dd-121">Receive a message</span></span>

<span data-ttu-id="e36dd-122">Para recibir un mensaje de texto, utilice la `Text` propiedad del `Activity` objeto.</span><span class="sxs-lookup"><span data-stu-id="e36dd-122">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="e36dd-123">En el controlador de actividad del bot, use el objeto turn context `Activity` para leer una sola solicitud de mensaje.</span><span class="sxs-lookup"><span data-stu-id="e36dd-123">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="e36dd-124">El código siguiente muestra un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e36dd-124">The code below shows an example.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="e36dd-125">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e36dd-125">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="e36dd-126">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="e36dd-126">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="e36dd-127">Python</span><span class="sxs-lookup"><span data-stu-id="e36dd-127">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="e36dd-128">JSON</span><span class="sxs-lookup"><span data-stu-id="e36dd-128">JSON</span></span>](#tab/json)

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

## <a name="send-a-message"></a><span data-ttu-id="e36dd-129">Enviar un mensaje</span><span class="sxs-lookup"><span data-stu-id="e36dd-129">Send a message</span></span>

<span data-ttu-id="e36dd-130">Para enviar un mensaje de texto, especifique la cadena que desea enviar como actividad.</span><span class="sxs-lookup"><span data-stu-id="e36dd-130">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="e36dd-131">En los controladores de actividad del bot, use el método del objeto turn context para `SendActivityAsync` enviar una única respuesta de mensaje.</span><span class="sxs-lookup"><span data-stu-id="e36dd-131">In the bot's activity handlers, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="e36dd-132">También puede usar el método del objeto `SendActivitiesAsync` para enviar varias respuestas a la vez.</span><span class="sxs-lookup"><span data-stu-id="e36dd-132">You can also use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span> <span data-ttu-id="e36dd-133">El siguiente código muestra un ejemplo de envío de un mensaje cuando alguien se agrega a una conversación</span><span class="sxs-lookup"><span data-stu-id="e36dd-133">The code below shows an example of sending a message when someone is added to a conversation</span></span>  

# <a name="cnet"></a>[<span data-ttu-id="e36dd-134">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e36dd-134">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="e36dd-135">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="e36dd-135">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="e36dd-136">Python</span><span class="sxs-lookup"><span data-stu-id="e36dd-136">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="e36dd-137">JSON</span><span class="sxs-lookup"><span data-stu-id="e36dd-137">JSON</span></span>](#tab/json)

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

## <a name="teams-channel-data"></a><span data-ttu-id="e36dd-138">Datos del canal de Teams</span><span class="sxs-lookup"><span data-stu-id="e36dd-138">Teams channel data</span></span>

<span data-ttu-id="e36dd-139">El objeto contiene información específica de Teams y es el origen definitivo de `channelData` los IDs de equipo y canal.</span><span class="sxs-lookup"><span data-stu-id="e36dd-139">The `channelData` object contains Teams-specific information and is the definitive source for team and channel IDs.</span></span> <span data-ttu-id="e36dd-140">Es posible que tenga que almacenar en caché y usar estos identificadores como claves para el almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="e36dd-140">You may need to cache and use these ids as keys for local storage.</span></span> <span data-ttu-id="e36dd-141">El SDK normalmente extraerá información importante del objeto para que sea más fácil acceder a ella, pero siempre se puede tener acceso a la información `TeamsActivityHandler` `channelData` original desde el `turnContext` objeto.</span><span class="sxs-lookup"><span data-stu-id="e36dd-141">The `TeamsActivityHandler` in the SDK will typically pull out important information from the `channelData` object to make it more easily accessible, however you can always access the original information from the `turnContext` object.</span></span>

<span data-ttu-id="e36dd-142">El `channelData` objeto no se incluye en los mensajes de las conversaciones personales, ya que tienen lugar fuera de cualquier canal.</span><span class="sxs-lookup"><span data-stu-id="e36dd-142">The `channelData` object is not included in messages in personal conversations since these take place outside of any channel.</span></span>

<span data-ttu-id="e36dd-143">Un objeto channelData típico de una actividad enviada al bot contiene la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="e36dd-143">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="e36dd-144">`eventType` Tipo de evento de Teams; se pasa solo en casos de [eventos de modificación de canal](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="e36dd-144">`eventType` Teams event type; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span></span>
* <span data-ttu-id="e36dd-145">`tenant.id` Id. de inquilino de Azure Active Directory; pasado en todos los contextos</span><span class="sxs-lookup"><span data-stu-id="e36dd-145">`tenant.id` Azure Active Directory tenant ID; passed in all contexts</span></span>
* <span data-ttu-id="e36dd-146">`team` Se pasa solo en contextos de canal, no en chat personal.</span><span class="sxs-lookup"><span data-stu-id="e36dd-146">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="e36dd-147">`id` GUID del canal</span><span class="sxs-lookup"><span data-stu-id="e36dd-147">`id` GUID for the channel</span></span>
  * <span data-ttu-id="e36dd-148">`name` Nombre del equipo; se pasa solo en casos de eventos [de cambio de nombre de equipo](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="e36dd-148">`name` Name of the team; passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span></span>
* <span data-ttu-id="e36dd-149">`channel` Se pasa solo en contextos de canal cuando se menciona el bot o para eventos en canales de equipos donde se ha agregado el bot</span><span class="sxs-lookup"><span data-stu-id="e36dd-149">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added</span></span>
  * <span data-ttu-id="e36dd-150">`id` GUID del canal</span><span class="sxs-lookup"><span data-stu-id="e36dd-150">`id` GUID for the channel</span></span>
  * <span data-ttu-id="e36dd-151">`name`Nombre del canal; se pasa solo en casos de [eventos de modificación de canal.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="e36dd-151">`name` Channel name; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="e36dd-152">`channelData.teamsTeamId` En desuso.</span><span class="sxs-lookup"><span data-stu-id="e36dd-152">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="e36dd-153">Esta propiedad se incluye solo por compatibilidad con versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="e36dd-153">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="e36dd-154">`channelData.teamsChannelId` En desuso.</span><span class="sxs-lookup"><span data-stu-id="e36dd-154">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="e36dd-155">Esta propiedad se incluye solo por compatibilidad con versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="e36dd-155">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="e36dd-156">Ejemplo de objeto channelData (evento channelCreated)</span><span class="sxs-lookup"><span data-stu-id="e36dd-156">Example channelData object (channelCreated event)</span></span>

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

## <a name="message-content"></a><span data-ttu-id="e36dd-157">Contenido del mensaje</span><span class="sxs-lookup"><span data-stu-id="e36dd-157">Message content</span></span>

<span data-ttu-id="e36dd-158">El bot puede enviar texto enriquecido, imágenes y tarjetas.</span><span class="sxs-lookup"><span data-stu-id="e36dd-158">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="e36dd-159">Los usuarios pueden enviar texto enriquecido e imágenes al bot.</span><span class="sxs-lookup"><span data-stu-id="e36dd-159">Users can send rich text and pictures to your bot.</span></span>

| <span data-ttu-id="e36dd-160">Formato</span><span class="sxs-lookup"><span data-stu-id="e36dd-160">Format</span></span>    | <span data-ttu-id="e36dd-161">De usuario a bot</span><span class="sxs-lookup"><span data-stu-id="e36dd-161">From user to bot</span></span> | <span data-ttu-id="e36dd-162">De bot a usuario</span><span class="sxs-lookup"><span data-stu-id="e36dd-162">From bot to user</span></span> | <span data-ttu-id="e36dd-163">Notas</span><span class="sxs-lookup"><span data-stu-id="e36dd-163">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="e36dd-164">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="e36dd-164">Rich text</span></span> | <span data-ttu-id="e36dd-165">✔</span><span class="sxs-lookup"><span data-stu-id="e36dd-165">✔</span></span>                | <span data-ttu-id="e36dd-166">✔</span><span class="sxs-lookup"><span data-stu-id="e36dd-166">✔</span></span>                |                                                                                         |
| <span data-ttu-id="e36dd-167">Imágenes</span><span class="sxs-lookup"><span data-stu-id="e36dd-167">Pictures</span></span>  | <span data-ttu-id="e36dd-168">✔</span><span class="sxs-lookup"><span data-stu-id="e36dd-168">✔</span></span>                | <span data-ttu-id="e36dd-169">✔</span><span class="sxs-lookup"><span data-stu-id="e36dd-169">✔</span></span>                | <span data-ttu-id="e36dd-170">Máximo de 1024×1024 y 1 MB en formato PNG, JPEG o GIF; GIF animado no se admite</span><span class="sxs-lookup"><span data-stu-id="e36dd-170">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported</span></span>  |
| <span data-ttu-id="e36dd-171">Tarjetas</span><span class="sxs-lookup"><span data-stu-id="e36dd-171">Cards</span></span>     | <span data-ttu-id="e36dd-172">✖</span><span class="sxs-lookup"><span data-stu-id="e36dd-172">✖</span></span>                | <span data-ttu-id="e36dd-173">✔</span><span class="sxs-lookup"><span data-stu-id="e36dd-173">✔</span></span>                | <span data-ttu-id="e36dd-174">Ver la referencia [de tarjetas de Teams](~/task-modules-and-cards/cards/cards-reference.md) para las tarjetas compatibles</span><span class="sxs-lookup"><span data-stu-id="e36dd-174">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards</span></span> |
| <span data-ttu-id="e36dd-175">Emojis</span><span class="sxs-lookup"><span data-stu-id="e36dd-175">Emojis</span></span>    | <span data-ttu-id="e36dd-176">✖</span><span class="sxs-lookup"><span data-stu-id="e36dd-176">✖</span></span>                | <span data-ttu-id="e36dd-177">✔</span><span class="sxs-lookup"><span data-stu-id="e36dd-177">✔</span></span>                | <span data-ttu-id="e36dd-178">Actualmente, Teams admite emojis a través de UTF-16 (como U+1F600 para el movimiento facial)</span><span class="sxs-lookup"><span data-stu-id="e36dd-178">Teams currently supports emojis via UTF-16 (such as U+1F600 for grinning face)</span></span>          |

## <a name="adding-notifications-to-your-message"></a><span data-ttu-id="e36dd-179">Agregar notificaciones al mensaje</span><span class="sxs-lookup"><span data-stu-id="e36dd-179">Adding notifications to your message</span></span>

<span data-ttu-id="e36dd-180">Las notificaciones alertan a los usuarios sobre nuevas tareas, menciones y comentarios relacionados con lo que están trabajando o necesitan mirar insertando un aviso en su Fuente de actividades.</span><span class="sxs-lookup"><span data-stu-id="e36dd-180">Notifications alert users about new tasks, mentions and comments related to what they are working on, or need to look at by inserting a notice into their Activity Feed.</span></span> <span data-ttu-id="e36dd-181">Puedes establecer las notificaciones para que se desencadene desde el mensaje de bot estableciendo la `TeamsChannelData` propiedad `Notification.Alert` objects en true.</span><span class="sxs-lookup"><span data-stu-id="e36dd-181">You can set notifications to trigger from your bot message by setting the `TeamsChannelData` objects `Notification.Alert` property to true.</span></span> <span data-ttu-id="e36dd-182">La generación o no de una notificación dependerá en última instancia de la configuración de Teams del usuario individual y no se puede invalidar mediante programación.</span><span class="sxs-lookup"><span data-stu-id="e36dd-182">Whether or not a notification is raised will ultimately depend on the individual user's Teams settings and you cannot programmatically override these settings.</span></span> <span data-ttu-id="e36dd-183">El tipo de notificación será un banner o un banner y un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="e36dd-183">The type of notification will be either a banner or both a banner and an email.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="e36dd-184">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e36dd-184">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="e36dd-185">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="e36dd-185">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="e36dd-186">Python</span><span class="sxs-lookup"><span data-stu-id="e36dd-186">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="e36dd-187">JSON</span><span class="sxs-lookup"><span data-stu-id="e36dd-187">JSON</span></span>](#tab/json)

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

## <a name="picture-messages"></a><span data-ttu-id="e36dd-188">Mensajes de imagen</span><span class="sxs-lookup"><span data-stu-id="e36dd-188">Picture messages</span></span>

<span data-ttu-id="e36dd-189">Las imágenes se envían agregando datos adjuntos a un mensaje.</span><span class="sxs-lookup"><span data-stu-id="e36dd-189">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="e36dd-190">Puede encontrar más información sobre los datos adjuntos en la [documentación de Bot Framework.](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="e36dd-190">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true).</span></span>

<span data-ttu-id="e36dd-191">Las imágenes pueden tener como máximo 1024×1024 y 1 MB en formato PNG, JPEG o GIF; GIF animado no es compatible.</span><span class="sxs-lookup"><span data-stu-id="e36dd-191">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not supported.</span></span>

<span data-ttu-id="e36dd-192">Se recomienda especificar el alto y el ancho de cada imagen mediante XML.</span><span class="sxs-lookup"><span data-stu-id="e36dd-192">We recommend that you specify the height and width of each image by using XML.</span></span> <span data-ttu-id="e36dd-193">Si usas Markdown, el tamaño de imagen predeterminado es 256×256.</span><span class="sxs-lookup"><span data-stu-id="e36dd-193">If you use Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="e36dd-194">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e36dd-194">For example:</span></span>

* <span data-ttu-id="e36dd-195">Use - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="e36dd-195">Use - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="e36dd-196">No usar: `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="e36dd-196">Don't use - `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="code-sample"></a><span data-ttu-id="e36dd-197">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="e36dd-197">Code sample</span></span>
|<span data-ttu-id="e36dd-198">**Nombre de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="e36dd-198">**Sample name**</span></span> | <span data-ttu-id="e36dd-199">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="e36dd-199">**Description**</span></span> | <span data-ttu-id="e36dd-200">**. NETCore**</span><span class="sxs-lookup"><span data-stu-id="e36dd-200">**.NETCore**</span></span> | <span data-ttu-id="e36dd-201">**Javascript**</span><span class="sxs-lookup"><span data-stu-id="e36dd-201">**Javascript**</span></span> | <span data-ttu-id="e36dd-202">**Python**</span><span class="sxs-lookup"><span data-stu-id="e36dd-202">**Python**</span></span>|
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="e36dd-203">Bot de conversación de Teams</span><span class="sxs-lookup"><span data-stu-id="e36dd-203">Teams Conversation Bot</span></span> | <span data-ttu-id="e36dd-204">Control de eventos de mensajería y conversación.</span><span class="sxs-lookup"><span data-stu-id="e36dd-204">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="e36dd-205">View</span><span class="sxs-lookup"><span data-stu-id="e36dd-205">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="e36dd-206">View</span><span class="sxs-lookup"><span data-stu-id="e36dd-206">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [<span data-ttu-id="e36dd-207">View</span><span class="sxs-lookup"><span data-stu-id="e36dd-207">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-steps"></a><span data-ttu-id="e36dd-208">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e36dd-208">Next steps</span></span>

* [<span data-ttu-id="e36dd-209">Envío de mensajes proactivos</span><span class="sxs-lookup"><span data-stu-id="e36dd-209">Sending proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
* [<span data-ttu-id="e36dd-210">Suscribirse a eventos de conversación</span><span class="sxs-lookup"><span data-stu-id="e36dd-210">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

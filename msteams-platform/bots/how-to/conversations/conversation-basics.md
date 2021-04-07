---
title: Conceptos básicos de la conversación
description: describe formas de tener una conversación con un bot de Microsoft Teams
ms.topic: overview
ms.author: anclear
keyword: conversations basics receive message send message picture message channel data adaptive cards
ms.openlocfilehash: 193a93dbf775389383e0385207fa4112440bffe5
ms.sourcegitcommit: 82bda0599ba2676ab9348c2f4284f73c7dad0838
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596677"
---
# <a name="conversation-basics"></a><span data-ttu-id="60e30-103">Conceptos básicos de la conversación</span><span class="sxs-lookup"><span data-stu-id="60e30-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="60e30-104">Una conversación es una serie de mensajes enviados entre el bot de Microsoft Teams y uno o varios usuarios.</span><span class="sxs-lookup"><span data-stu-id="60e30-104">A conversation is a series of messages sent between your Microsoft Teams bot and one or more users.</span></span> <span data-ttu-id="60e30-105">Hay tres tipos de conversaciones, también denominadas ámbitos en Teams:</span><span class="sxs-lookup"><span data-stu-id="60e30-105">There are three types of conversations, also called scopes in Teams:</span></span>

| <span data-ttu-id="60e30-106">Tipo de conversación</span><span class="sxs-lookup"><span data-stu-id="60e30-106">Conversation type</span></span> | <span data-ttu-id="60e30-107">Descripción</span><span class="sxs-lookup"><span data-stu-id="60e30-107">Description</span></span> |
| ------- | ----------- |
| `channel` | <span data-ttu-id="60e30-108">Este tipo de conversación es visible para todos los miembros del canal.</span><span class="sxs-lookup"><span data-stu-id="60e30-108">This conversation type is visible to all members of the channel.</span></span> |
| `personal` | <span data-ttu-id="60e30-109">Este tipo de conversación incluye conversaciones entre bots y un solo usuario.</span><span class="sxs-lookup"><span data-stu-id="60e30-109">This conversation type includes conversations between bots and a single user.</span></span> |
| `groupChat` | <span data-ttu-id="60e30-110">Este tipo de conversación incluye chat entre un bot y dos o más usuarios.</span><span class="sxs-lookup"><span data-stu-id="60e30-110">This conversation type includes chat between a bot and two or more users.</span></span> <span data-ttu-id="60e30-111">También habilita el bot en chats de reunión.</span><span class="sxs-lookup"><span data-stu-id="60e30-111">It also enables your bot in meeting chats.</span></span> |

<span data-ttu-id="60e30-112">Un bot se comporta de forma diferente en función de la conversación en la que esté implicado:</span><span class="sxs-lookup"><span data-stu-id="60e30-112">A bot behaves differently depending on the conversation it is involved in:</span></span>

* <span data-ttu-id="60e30-113">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span><span class="sxs-lookup"><span data-stu-id="60e30-113">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="60e30-114">Los bots de una conversación uno a uno no requieren una mención @.</span><span class="sxs-lookup"><span data-stu-id="60e30-114">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="60e30-115">Todos los mensajes enviados por el usuario se enrutan al bot.</span><span class="sxs-lookup"><span data-stu-id="60e30-115">All messages sent by the user routes to your bot.</span></span>

<span data-ttu-id="60e30-116">Para que el bot funcione en una conversación o ámbito en particular, agregue compatibilidad a ese ámbito en el manifiesto [de la aplicación](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="60e30-116">For the bot to work in a particular conversation or scope, add support to that scope in the [app manifest](~/resources/schema/manifest-schema.md).</span></span>

## <a name="messages-in-bot-conversations"></a><span data-ttu-id="60e30-117">Mensajes en conversaciones de bot</span><span class="sxs-lookup"><span data-stu-id="60e30-117">Messages in bot conversations</span></span>

<span data-ttu-id="60e30-118">Cada mensaje de una conversación es un `Activity` objeto de tipo `messageType: message` .</span><span class="sxs-lookup"><span data-stu-id="60e30-118">Each message in a conversation is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="60e30-119">Cuando un usuario envía un mensaje, Teams publica el mensaje en el bot.</span><span class="sxs-lookup"><span data-stu-id="60e30-119">When a user sends a message, Teams posts the message to your bot.</span></span> <span data-ttu-id="60e30-120">Teams envía un objeto JSON al extremo de mensajería del bot.</span><span class="sxs-lookup"><span data-stu-id="60e30-120">Teams sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="60e30-121">El bot examina el mensaje para determinar su tipo y responde en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="60e30-121">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="60e30-122">Las conversaciones básicas se controlan a través del conector de Bot Framework, una única API de REST.</span><span class="sxs-lookup"><span data-stu-id="60e30-122">Basic conversations are handled through the Bot Framework connector, a single REST API.</span></span> <span data-ttu-id="60e30-123">Esta API permite que el bot se comunique con Teams y otros canales.</span><span class="sxs-lookup"><span data-stu-id="60e30-123">This API enables your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="60e30-124">El SDK de Bot Builder proporciona lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="60e30-124">The Bot Builder SDK provides the following:</span></span>

* <span data-ttu-id="60e30-125">Fácil acceso al conector de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="60e30-125">Easy access to the Bot Framework connector.</span></span>
* <span data-ttu-id="60e30-126">Funcionalidad adicional para administrar el estado y el flujo de conversación.</span><span class="sxs-lookup"><span data-stu-id="60e30-126">Additional functionality to manage conversation flow and state.</span></span>
* <span data-ttu-id="60e30-127">Formas sencillas de incorporar servicios cognitivos como el procesamiento de lenguaje natural (NLP).</span><span class="sxs-lookup"><span data-stu-id="60e30-127">Simple ways to incorporate cognitive services such as Natural Language Processing (NLP).</span></span>

<span data-ttu-id="60e30-128">El bot recibe mensajes de Teams mediante la propiedad y envía una `Text` o varias respuestas de mensaje a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="60e30-128">Your bot receives messages from Teams using the `Text` property and it sends single or multiple message responses to the users.</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="60e30-129">Recibir un mensaje</span><span class="sxs-lookup"><span data-stu-id="60e30-129">Receive a message</span></span>

<span data-ttu-id="60e30-130">Para recibir un mensaje de texto, use la propiedad `Text` del objeto `Activity`.</span><span class="sxs-lookup"><span data-stu-id="60e30-130">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="60e30-131">En el controlador de actividades del bot, use convertir `Activity` del objeto de contexto para leer una solicitud de mensaje única.</span><span class="sxs-lookup"><span data-stu-id="60e30-131">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="60e30-132">El siguiente código muestra un ejemplo de recepción de un mensaje:</span><span class="sxs-lookup"><span data-stu-id="60e30-132">The following code shows an example of receiving a message:</span></span>

# <a name="c"></a>[<span data-ttu-id="60e30-133">C#</span><span class="sxs-lookup"><span data-stu-id="60e30-133">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescript"></a>[<span data-ttu-id="60e30-134">TypeScript</span><span class="sxs-lookup"><span data-stu-id="60e30-134">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="60e30-135">Python</span><span class="sxs-lookup"><span data-stu-id="60e30-135">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="60e30-136">JSON</span><span class="sxs-lookup"><span data-stu-id="60e30-136">JSON</span></span>](#tab/json)

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

## <a name="send-a-message"></a><span data-ttu-id="60e30-137">Enviar un mensaje</span><span class="sxs-lookup"><span data-stu-id="60e30-137">Send a message</span></span>

<span data-ttu-id="60e30-138">Para enviar un mensaje de texto, especifique la string que desee enviar como actividad.</span><span class="sxs-lookup"><span data-stu-id="60e30-138">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="60e30-139">En el controlador de actividad del bot, use el método del objeto turn context `SendActivityAsync` para enviar una única respuesta de mensaje.</span><span class="sxs-lookup"><span data-stu-id="60e30-139">In the bot's activity handler, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="60e30-140">Use el método del `SendActivitiesAsync` objeto para enviar varias respuestas a la vez.</span><span class="sxs-lookup"><span data-stu-id="60e30-140">Use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span> <span data-ttu-id="60e30-141">El siguiente código muestra un ejemplo de envío de un mensaje cuando se agrega un usuario a una conversación:</span><span class="sxs-lookup"><span data-stu-id="60e30-141">The following code shows an example of sending a message when a user is added to a conversation:</span></span>

<span data-ttu-id="60e30-142">El código siguiente muestra un ejemplo de envío de un mensaje:</span><span class="sxs-lookup"><span data-stu-id="60e30-142">The following code shows an example of sending a message:</span></span>

# <a name="c"></a>[<span data-ttu-id="60e30-143">C#</span><span class="sxs-lookup"><span data-stu-id="60e30-143">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescript"></a>[<span data-ttu-id="60e30-144">TypeScript</span><span class="sxs-lookup"><span data-stu-id="60e30-144">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="60e30-145">Python</span><span class="sxs-lookup"><span data-stu-id="60e30-145">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="60e30-146">JSON</span><span class="sxs-lookup"><span data-stu-id="60e30-146">JSON</span></span>](#tab/json)

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

> [!NOTE]
> <span data-ttu-id="60e30-147">La división de mensajes se produce cuando se envían un mensaje de texto y datos adjuntos en la misma carga de actividad.</span><span class="sxs-lookup"><span data-stu-id="60e30-147">Message splitting occurs when a text message and an attachment are sent in the same activity payload.</span></span> <span data-ttu-id="60e30-148">Microsoft Teams divide esta actividad en actividades independientes, una con solo un mensaje de texto y otra con datos adjuntos.</span><span class="sxs-lookup"><span data-stu-id="60e30-148">This activity is split into separate activities by Microsoft Teams, one with just a text message and the other with an attachment.</span></span> <span data-ttu-id="60e30-149">Como la actividad está dividida, no recibe el identificador de mensaje en respuesta, que se usa para actualizar o [eliminar](~/bots/how-to/update-and-delete-bot-messages.md) el mensaje de forma proactiva.</span><span class="sxs-lookup"><span data-stu-id="60e30-149">As the activity is split, you do not receive the message ID in response, which is used to [update or delete](~/bots/how-to/update-and-delete-bot-messages.md) the message proactively.</span></span> <span data-ttu-id="60e30-150">Se recomienda enviar actividades independientes en lugar de depender de la división de mensajes.</span><span class="sxs-lookup"><span data-stu-id="60e30-150">It is recommended to send separate activities instead of depending on message splitting.</span></span>

<span data-ttu-id="60e30-151">Los mensajes enviados entre usuarios y bots incluyen datos de canal internos dentro del mensaje.</span><span class="sxs-lookup"><span data-stu-id="60e30-151">Messages sent between users and bots include internal channel data within the message.</span></span> <span data-ttu-id="60e30-152">Estos datos permiten al bot comunicarse correctamente en ese canal.</span><span class="sxs-lookup"><span data-stu-id="60e30-152">This data allows the bot to communicate properly on that channel.</span></span> <span data-ttu-id="60e30-153">El SDK del generador de bots permite modificar la estructura del mensaje.</span><span class="sxs-lookup"><span data-stu-id="60e30-153">The Bot Builder SDK allows you to modify the message structure.</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="60e30-154">Datos del canal de Teams</span><span class="sxs-lookup"><span data-stu-id="60e30-154">Teams channel data</span></span>

<span data-ttu-id="60e30-155">El `channelData` objeto contiene información específica de Teams y es un origen definitivo para los IDs de equipo y canal.</span><span class="sxs-lookup"><span data-stu-id="60e30-155">The `channelData` object contains Teams-specific information and is a definitive source for team and channel IDs.</span></span> <span data-ttu-id="60e30-156">Opcionalmente, puede almacenar en caché y usar estos IDs como claves para el almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="60e30-156">Optionally, you can cache and use these IDs as keys for local storage.</span></span> <span data-ttu-id="60e30-157">El SDK normalmente extrae información importante del `TeamsActivityHandler` objeto para que sea fácilmente `channelData` accesible.</span><span class="sxs-lookup"><span data-stu-id="60e30-157">The `TeamsActivityHandler` in the SDK typically pulls out important information from the `channelData` object to make it easily accessible.</span></span> <span data-ttu-id="60e30-158">Sin embargo, siempre puede tener acceso a los datos originales desde el `turnContext` objeto.</span><span class="sxs-lookup"><span data-stu-id="60e30-158">However, you can always access the original data from the `turnContext` object.</span></span>

<span data-ttu-id="60e30-159">El objeto no se incluye en los mensajes de conversaciones personales, ya que tienen lugar `channelData` fuera de un canal.</span><span class="sxs-lookup"><span data-stu-id="60e30-159">The `channelData` object is not included in messages in personal conversations, as these take place outside of a channel.</span></span>

<span data-ttu-id="60e30-160">Un objeto `channelData` típico de una actividad enviada al bot contiene la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="60e30-160">A typical `channelData` object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="60e30-161">`eventType`: Tipo de evento de Teams pasado solo en casos de [eventos de modificación de canal](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="60e30-161">`eventType`: Teams event type passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="60e30-162">`tenant.id`: Identificador de inquilino de Azure Active Directory pasado en todos los contextos.</span><span class="sxs-lookup"><span data-stu-id="60e30-162">`tenant.id`: Azure Active Directory tenant ID passed in all contexts.</span></span>
* <span data-ttu-id="60e30-163">`team`: Se pasa solo en contextos de canal, no en chat personal.</span><span class="sxs-lookup"><span data-stu-id="60e30-163">`team`: Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="60e30-164">`id`: GUID para el canal.</span><span class="sxs-lookup"><span data-stu-id="60e30-164">`id`: GUID for the channel.</span></span>
  * <span data-ttu-id="60e30-165">`name`: Nombre del equipo pasado solo en casos de [eventos de cambio de nombre de equipo](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="60e30-165">`name`: Name of the team passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="60e30-166">`channel`: Se pasa solo en contextos de canal cuando se menciona el bot o para eventos en canales de equipos donde se ha agregado el bot.</span><span class="sxs-lookup"><span data-stu-id="60e30-166">`channel`: Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added.</span></span>
  * <span data-ttu-id="60e30-167">`id`: GUID para el canal.</span><span class="sxs-lookup"><span data-stu-id="60e30-167">`id`: GUID for the channel.</span></span>
  * <span data-ttu-id="60e30-168">`name`: Nombre del canal pasado solo en casos de [eventos de modificación de canal](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="60e30-168">`name`: Channel name passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="60e30-169">`channelData.teamsTeamId`: En desuso.</span><span class="sxs-lookup"><span data-stu-id="60e30-169">`channelData.teamsTeamId`: Deprecated.</span></span> <span data-ttu-id="60e30-170">Esta propiedad solo se incluye por compatibilidad con versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="60e30-170">This property is only included for backward compatibility.</span></span>
* <span data-ttu-id="60e30-171">`channelData.teamsChannelId`: En desuso.</span><span class="sxs-lookup"><span data-stu-id="60e30-171">`channelData.teamsChannelId`: Deprecated.</span></span> <span data-ttu-id="60e30-172">Esta propiedad solo se incluye por compatibilidad con versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="60e30-172">This property is only included for backward compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="60e30-173">Objeto channelData de ejemplo (evento channelCreated)</span><span class="sxs-lookup"><span data-stu-id="60e30-173">Example channelData object (channelCreated event)</span></span>

<span data-ttu-id="60e30-174">El siguiente código muestra un ejemplo del objeto channelData:</span><span class="sxs-lookup"><span data-stu-id="60e30-174">The following code shows an example of channelData object:</span></span>

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

<span data-ttu-id="60e30-175">Los mensajes recibidos o enviados al bot pueden incluir diferentes tipos de contenido de mensaje.</span><span class="sxs-lookup"><span data-stu-id="60e30-175">Messages received from or sent to your bot can include different types of message content.</span></span>

## <a name="message-content"></a><span data-ttu-id="60e30-176">Contenido del mensaje</span><span class="sxs-lookup"><span data-stu-id="60e30-176">Message content</span></span>

<span data-ttu-id="60e30-177">El bot puede enviar texto enriquecido, imágenes y tarjetas.</span><span class="sxs-lookup"><span data-stu-id="60e30-177">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="60e30-178">Los usuarios pueden enviar texto enriquecido e imágenes al bot.</span><span class="sxs-lookup"><span data-stu-id="60e30-178">Users can send rich text and pictures to your bot.</span></span>

| <span data-ttu-id="60e30-179">Formato</span><span class="sxs-lookup"><span data-stu-id="60e30-179">Format</span></span>    | <span data-ttu-id="60e30-180">De usuario a bot</span><span class="sxs-lookup"><span data-stu-id="60e30-180">From user to bot</span></span> | <span data-ttu-id="60e30-181">De bot a usuario</span><span class="sxs-lookup"><span data-stu-id="60e30-181">From bot to user</span></span> | <span data-ttu-id="60e30-182">Notas</span><span class="sxs-lookup"><span data-stu-id="60e30-182">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="60e30-183">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="60e30-183">Rich text</span></span> | <span data-ttu-id="60e30-184">✔</span><span class="sxs-lookup"><span data-stu-id="60e30-184">✔</span></span>                | <span data-ttu-id="60e30-185">✔</span><span class="sxs-lookup"><span data-stu-id="60e30-185">✔</span></span>                |                                                                                         |
| <span data-ttu-id="60e30-186">Imágenes</span><span class="sxs-lookup"><span data-stu-id="60e30-186">Pictures</span></span>  | <span data-ttu-id="60e30-187">✔</span><span class="sxs-lookup"><span data-stu-id="60e30-187">✔</span></span>                | <span data-ttu-id="60e30-188">✔</span><span class="sxs-lookup"><span data-stu-id="60e30-188">✔</span></span>                | <span data-ttu-id="60e30-189">Máximo 1024×1024 y 1 MB en formato PNG, JPEG o GIF.</span><span class="sxs-lookup"><span data-stu-id="60e30-189">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="60e30-190">Gif animado no es compatible.</span><span class="sxs-lookup"><span data-stu-id="60e30-190">Animated GIF is not supported.</span></span>  |
| <span data-ttu-id="60e30-191">Tarjetas</span><span class="sxs-lookup"><span data-stu-id="60e30-191">Cards</span></span>     | <span data-ttu-id="60e30-192">✖</span><span class="sxs-lookup"><span data-stu-id="60e30-192">✖</span></span>                | <span data-ttu-id="60e30-193">✔</span><span class="sxs-lookup"><span data-stu-id="60e30-193">✔</span></span>                | <span data-ttu-id="60e30-194">Consulta la referencia [de la tarjeta de Teams](~/task-modules-and-cards/cards/cards-reference.md) para obtener las tarjetas compatibles.</span><span class="sxs-lookup"><span data-stu-id="60e30-194">See the [Teams card reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards.</span></span> |
| <span data-ttu-id="60e30-195">Emojis</span><span class="sxs-lookup"><span data-stu-id="60e30-195">Emojis</span></span>    | <span data-ttu-id="60e30-196">✖</span><span class="sxs-lookup"><span data-stu-id="60e30-196">✖</span></span>                | <span data-ttu-id="60e30-197">✔</span><span class="sxs-lookup"><span data-stu-id="60e30-197">✔</span></span>                | <span data-ttu-id="60e30-198">Actualmente, Teams admite emojis a través de UTF-16, como U+1F600 para el rostro sonriente.</span><span class="sxs-lookup"><span data-stu-id="60e30-198">Teams currently supports emojis through UTF-16, such as U+1F600 for grinning face.</span></span> |

<span data-ttu-id="60e30-199">También puede agregar notificaciones al mensaje mediante la `Notification.Alert` propiedad.</span><span class="sxs-lookup"><span data-stu-id="60e30-199">You can also add notifications to your message using the `Notification.Alert` property.</span></span>

## <a name="notifications-to-your-message"></a><span data-ttu-id="60e30-200">Notificaciones al mensaje</span><span class="sxs-lookup"><span data-stu-id="60e30-200">Notifications to your message</span></span>

<span data-ttu-id="60e30-201">Las notificaciones alertan a los usuarios sobre nuevas tareas, menciones y comentarios.</span><span class="sxs-lookup"><span data-stu-id="60e30-201">Notifications alert users about new tasks, mentions, and comments.</span></span> <span data-ttu-id="60e30-202">Estas alertas están relacionadas con lo que los usuarios están trabajando o lo que deben ver insertando un aviso en su fuente de actividad.</span><span class="sxs-lookup"><span data-stu-id="60e30-202">These alerts are related to what users are working on or what they must look at by inserting a notice into their activity feed.</span></span> <span data-ttu-id="60e30-203">Para que las notificaciones se desencadene desde el mensaje del bot, establezca la `TeamsChannelData` propiedad `Notification.Alert` objects en true.</span><span class="sxs-lookup"><span data-stu-id="60e30-203">For notifications to trigger from your bot message, set the `TeamsChannelData` objects `Notification.Alert` property to true.</span></span> <span data-ttu-id="60e30-204">Si se genera o no una notificación depende de la configuración de Teams del usuario individual y no se puede invalidar esta configuración.</span><span class="sxs-lookup"><span data-stu-id="60e30-204">Whether or not a notification is raised depends on the individual user's Teams settings and you cannot override these settings.</span></span> <span data-ttu-id="60e30-205">El tipo de notificación es un banner o un banner y un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="60e30-205">The notification type is either a banner or both a banner and an email.</span></span>

> [!NOTE]
> <span data-ttu-id="60e30-206">El **campo Resumen** muestra cualquier texto del usuario como un mensaje de notificación en la fuente.</span><span class="sxs-lookup"><span data-stu-id="60e30-206">The **Summary** field displays any text from the user as a notification message in the feed.</span></span>

<span data-ttu-id="60e30-207">El siguiente código muestra un ejemplo de cómo agregar notificaciones al mensaje:</span><span class="sxs-lookup"><span data-stu-id="60e30-207">The following code shows an example of adding notifications to your message:</span></span>

# <a name="c"></a>[<span data-ttu-id="60e30-208">C#</span><span class="sxs-lookup"><span data-stu-id="60e30-208">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescript"></a>[<span data-ttu-id="60e30-209">TypeScript</span><span class="sxs-lookup"><span data-stu-id="60e30-209">TypeScript</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="60e30-210">Python</span><span class="sxs-lookup"><span data-stu-id="60e30-210">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="60e30-211">JSON</span><span class="sxs-lookup"><span data-stu-id="60e30-211">JSON</span></span>](#tab/json)

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

<span data-ttu-id="60e30-212">Para mejorar el mensaje, puede incluir imágenes como datos adjuntos a ese mensaje.</span><span class="sxs-lookup"><span data-stu-id="60e30-212">To enhance your message, you can include pictures as attachments to that message.</span></span>

## <a name="picture-messages"></a><span data-ttu-id="60e30-213">Mensajes de imagen</span><span class="sxs-lookup"><span data-stu-id="60e30-213">Picture messages</span></span>

<span data-ttu-id="60e30-214">Las imágenes se envían agregando datos adjuntos a un mensaje.</span><span class="sxs-lookup"><span data-stu-id="60e30-214">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="60e30-215">Para obtener más información sobre los datos [adjuntos,](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)consulte Bot Framework documentation .</span><span class="sxs-lookup"><span data-stu-id="60e30-215">For more information on attachments, see [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments).</span></span>

<span data-ttu-id="60e30-216">Las imágenes pueden tener como máximo 1024×1024 y 1 MB en formato PNG, JPEG o GIF.</span><span class="sxs-lookup"><span data-stu-id="60e30-216">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="60e30-217">Gif animado no es compatible.</span><span class="sxs-lookup"><span data-stu-id="60e30-217">Animated GIF is not supported.</span></span>

<span data-ttu-id="60e30-218">Especifique el alto y el ancho de cada imagen mediante XML.</span><span class="sxs-lookup"><span data-stu-id="60e30-218">Specify the height and width of each image by using XML.</span></span> <span data-ttu-id="60e30-219">En markdown, el tamaño de imagen es predeterminado 256×256.</span><span class="sxs-lookup"><span data-stu-id="60e30-219">In markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="60e30-220">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="60e30-220">For example:</span></span>

* <span data-ttu-id="60e30-221">Use: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>` .</span><span class="sxs-lookup"><span data-stu-id="60e30-221">Use: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`.</span></span>
* <span data-ttu-id="60e30-222">No usar: `![Duck on a rock](http://aka.ms/Fo983c)` .</span><span class="sxs-lookup"><span data-stu-id="60e30-222">Do not use: `![Duck on a rock](http://aka.ms/Fo983c)`.</span></span>

<span data-ttu-id="60e30-223">Un bot conversacional puede incluir tarjetas adaptables que simplifican los flujos de trabajo empresariales.</span><span class="sxs-lookup"><span data-stu-id="60e30-223">A conversational bot can include adaptive cards that simplify business workflows.</span></span> <span data-ttu-id="60e30-224">Las tarjetas adaptables ofrecen texto personalizable enriquecido, voz, imágenes, botones y campos de entrada.</span><span class="sxs-lookup"><span data-stu-id="60e30-224">Adaptive cards offer rich customizable text, speech, images, buttons, and input fields.</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="60e30-225">Tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="60e30-225">Adaptive cards</span></span>

<span data-ttu-id="60e30-226">Las tarjetas adaptables se pueden crear en un bot y mostrarse en varias aplicaciones, como Teams, tu sitio web, entre otras.</span><span class="sxs-lookup"><span data-stu-id="60e30-226">Adaptive cards can be authored in a bot and shown in multiple apps such as Teams, your website, and so on.</span></span> <span data-ttu-id="60e30-227">Para obtener más información, vea [adaptive cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span><span class="sxs-lookup"><span data-stu-id="60e30-227">For more information, see [adaptive cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>

<span data-ttu-id="60e30-228">El siguiente código muestra un ejemplo de envío de una tarjeta adaptable sencilla:</span><span class="sxs-lookup"><span data-stu-id="60e30-228">The following code shows an example of sending a simple adaptive card:</span></span>

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

<span data-ttu-id="60e30-229">Para obtener más información acerca de las tarjetas y las tarjetas de los bots, consulte [la documentación sobre tarjetas](~/task-modules-and-cards/what-are-cards.md).</span><span class="sxs-lookup"><span data-stu-id="60e30-229">To know more about cards and cards in bots, see [cards documentation](~/task-modules-and-cards/what-are-cards.md).</span></span>

<span data-ttu-id="60e30-230">En la siguiente sección se proporcionan respuestas de código de estado para los errores generados desde las API de bot.</span><span class="sxs-lookup"><span data-stu-id="60e30-230">The next section provides status code responses for errors generated from Bot APIs.</span></span>

## <a name="status-code-responses"></a><span data-ttu-id="60e30-231">Respuestas de código de estado</span><span class="sxs-lookup"><span data-stu-id="60e30-231">Status code responses</span></span>

<span data-ttu-id="60e30-232">A continuación se desenván los códigos de estado y sus valores de mensaje y código de error:</span><span class="sxs-lookup"><span data-stu-id="60e30-232">Following are the status codes and their error code and message values:</span></span>

| <span data-ttu-id="60e30-233">Código de estado</span><span class="sxs-lookup"><span data-stu-id="60e30-233">Status code</span></span> | <span data-ttu-id="60e30-234">Código de error y valores de mensaje</span><span class="sxs-lookup"><span data-stu-id="60e30-234">Error code and message values</span></span> | <span data-ttu-id="60e30-235">Descripción</span><span class="sxs-lookup"><span data-stu-id="60e30-235">Description</span></span> |
|----------------|-----------------|-----------------|
| <span data-ttu-id="60e30-236">403</span><span class="sxs-lookup"><span data-stu-id="60e30-236">403</span></span> | <span data-ttu-id="60e30-237">**Código**: `ConversationBlockedByUser`</span><span class="sxs-lookup"><span data-stu-id="60e30-237">**Code**: `ConversationBlockedByUser`</span></span> <br/> <span data-ttu-id="60e30-238">**Mensaje:**"El usuario bloqueó la conversación con el bot".</span><span class="sxs-lookup"><span data-stu-id="60e30-238">**Message**: "User blocked the conversation with the bot."</span></span> | <span data-ttu-id="60e30-239">El usuario bloqueó el bot en un chat 1:1 o un canal mediante la configuración de moderación.</span><span class="sxs-lookup"><span data-stu-id="60e30-239">User blocked the bot in 1:1 chat or a channel through moderation settings.</span></span> |
| <span data-ttu-id="60e30-240">403</span><span class="sxs-lookup"><span data-stu-id="60e30-240">403</span></span> | <span data-ttu-id="60e30-241">**Código**: `BotNotInConversationRoster`</span><span class="sxs-lookup"><span data-stu-id="60e30-241">**Code**: `BotNotInConversationRoster`</span></span> <br/> <span data-ttu-id="60e30-242">**Mensaje:**"El bot no forma parte de la lista de conversaciones".</span><span class="sxs-lookup"><span data-stu-id="60e30-242">**Message**: "The bot is not part of the conversation roster."</span></span> | <span data-ttu-id="60e30-243">El bot no forma parte de la conversación.</span><span class="sxs-lookup"><span data-stu-id="60e30-243">The bot is not part of the conversation.</span></span> |
| <span data-ttu-id="60e30-244">403</span><span class="sxs-lookup"><span data-stu-id="60e30-244">403</span></span> | <span data-ttu-id="60e30-245">**Código**: `BotDisabledByAdmin`</span><span class="sxs-lookup"><span data-stu-id="60e30-245">**Code**: `BotDisabledByAdmin`</span></span> <br/> <span data-ttu-id="60e30-246">**Mensaje:**"El administrador de inquilinos deshabilitó este bot".</span><span class="sxs-lookup"><span data-stu-id="60e30-246">**Message**: "The tenant admin disabled this bot."</span></span> | <span data-ttu-id="60e30-247">El inquilino bloqueó el bot.</span><span class="sxs-lookup"><span data-stu-id="60e30-247">Tenant blocked the bot.</span></span> |
| <span data-ttu-id="60e30-248">401</span><span class="sxs-lookup"><span data-stu-id="60e30-248">401</span></span> | <span data-ttu-id="60e30-249">**Código**: `BotNotRegistered`</span><span class="sxs-lookup"><span data-stu-id="60e30-249">**Code**: `BotNotRegistered`</span></span> <br/> <span data-ttu-id="60e30-250">**Mensaje:**"No se encontró ningún registro para este bot".</span><span class="sxs-lookup"><span data-stu-id="60e30-250">**Message**: “No registration found for this bot.”</span></span> | <span data-ttu-id="60e30-251">No se encontró el registro de este bot.</span><span class="sxs-lookup"><span data-stu-id="60e30-251">The registration for this bot was not found.</span></span> |
| <span data-ttu-id="60e30-252">412</span><span class="sxs-lookup"><span data-stu-id="60e30-252">412</span></span> | <span data-ttu-id="60e30-253">**Código**: `PreconditionFailed`</span><span class="sxs-lookup"><span data-stu-id="60e30-253">**Code**: `PreconditionFailed`</span></span> <br/> <span data-ttu-id="60e30-254">**Mensaje:**"Error en la condición previa, inténtelo de nuevo".</span><span class="sxs-lookup"><span data-stu-id="60e30-254">**Message**: “Precondition failed, please try again.”</span></span> | <span data-ttu-id="60e30-255">Error en una de nuestras dependencias debido a varias operaciones simultáneas en la misma conversación.</span><span class="sxs-lookup"><span data-stu-id="60e30-255">A precondition failed on one of our dependencies due to multiple concurrent operations on the same conversation.</span></span> |
| <span data-ttu-id="60e30-256">404</span><span class="sxs-lookup"><span data-stu-id="60e30-256">404</span></span> | <span data-ttu-id="60e30-257">**Código**: `ConversationNotFound`</span><span class="sxs-lookup"><span data-stu-id="60e30-257">**Code**: `ConversationNotFound`</span></span> <br/> <span data-ttu-id="60e30-258">**Mensaje:**"No se encontró la conversación".</span><span class="sxs-lookup"><span data-stu-id="60e30-258">**Message**: “Conversation not found.”</span></span> | <span data-ttu-id="60e30-259">No se encontró la conversación.</span><span class="sxs-lookup"><span data-stu-id="60e30-259">The conversation was not found.</span></span> |
| <span data-ttu-id="60e30-260">413</span><span class="sxs-lookup"><span data-stu-id="60e30-260">413</span></span> | <span data-ttu-id="60e30-261">**Código**: `MessageSizeTooBig`</span><span class="sxs-lookup"><span data-stu-id="60e30-261">**Code**: `MessageSizeTooBig`</span></span> <br/> <span data-ttu-id="60e30-262">**Mensaje:**"Tamaño del mensaje demasiado grande".</span><span class="sxs-lookup"><span data-stu-id="60e30-262">**Message**: “Message size too large.”</span></span> | <span data-ttu-id="60e30-263">El tamaño de la solicitud entrante era demasiado grande.</span><span class="sxs-lookup"><span data-stu-id="60e30-263">The size on the incoming request was too large.</span></span> |
| <span data-ttu-id="60e30-264">429</span><span class="sxs-lookup"><span data-stu-id="60e30-264">429</span></span> | <span data-ttu-id="60e30-265">**Código**: `Throttled`</span><span class="sxs-lookup"><span data-stu-id="60e30-265">**Code**: `Throttled`</span></span> <br/> <span data-ttu-id="60e30-266">**Mensaje:**"Demasiadas solicitudes".</span><span class="sxs-lookup"><span data-stu-id="60e30-266">**Message**: “Too many requests.”</span></span> <span data-ttu-id="60e30-267">También devuelve cuándo reintentar después.</span><span class="sxs-lookup"><span data-stu-id="60e30-267">Also returns when to retry after.</span></span> | <span data-ttu-id="60e30-268">El bot envió demasiadas solicitudes.</span><span class="sxs-lookup"><span data-stu-id="60e30-268">Too many requests were sent by the bot.</span></span> <span data-ttu-id="60e30-269">Para obtener más información, vea [rate limit](~/bots/how-to/rate-limit.md).</span><span class="sxs-lookup"><span data-stu-id="60e30-269">For more information, see [rate limit](~/bots/how-to/rate-limit.md).</span></span> |

<span data-ttu-id="60e30-270">En la siguiente sección se muestra un ejemplo de código simple que incorpora un flujo de conversación básico en una aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="60e30-270">The next section illustrates a simple code sample that incorporates basic conversational flow into a Teams application.</span></span>

## <a name="code-sample"></a><span data-ttu-id="60e30-271">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="60e30-271">Code sample</span></span>

<span data-ttu-id="60e30-272">A continuación se muestran los ejemplos de código para el bot de conversación de Teams:</span><span class="sxs-lookup"><span data-stu-id="60e30-272">Following are the code samples for Teams conversation bot:</span></span>

|<span data-ttu-id="60e30-273">Nombre de ejemplo</span><span class="sxs-lookup"><span data-stu-id="60e30-273">Sample name</span></span> | <span data-ttu-id="60e30-274">Descripción</span><span class="sxs-lookup"><span data-stu-id="60e30-274">Description</span></span> | <span data-ttu-id="60e30-275">. NETCore</span><span class="sxs-lookup"><span data-stu-id="60e30-275">.NETCore</span></span> | <span data-ttu-id="60e30-276">Node.js</span><span class="sxs-lookup"><span data-stu-id="60e30-276">Node.js</span></span> | <span data-ttu-id="60e30-277">Python</span><span class="sxs-lookup"><span data-stu-id="60e30-277">Python</span></span> |
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="60e30-278">Bot de conversación de Teams</span><span class="sxs-lookup"><span data-stu-id="60e30-278">Teams conversation bot</span></span> | <span data-ttu-id="60e30-279">Control de eventos de mensajería y conversación.</span><span class="sxs-lookup"><span data-stu-id="60e30-279">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="60e30-280">View</span><span class="sxs-lookup"><span data-stu-id="60e30-280">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="60e30-281">View</span><span class="sxs-lookup"><span data-stu-id="60e30-281">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [<span data-ttu-id="60e30-282">View</span><span class="sxs-lookup"><span data-stu-id="60e30-282">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="see-also"></a><span data-ttu-id="60e30-283">Ver también</span><span class="sxs-lookup"><span data-stu-id="60e30-283">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="60e30-284">Enviar mensajes proactivos</span><span class="sxs-lookup"><span data-stu-id="60e30-284">Send proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="60e30-285">Suscribirse a eventos de conversación</span><span class="sxs-lookup"><span data-stu-id="60e30-285">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

## <a name="next-step"></a><span data-ttu-id="60e30-286">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="60e30-286">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="60e30-287">Menús de comandos bot</span><span class="sxs-lookup"><span data-stu-id="60e30-287">Bot command menus</span></span>](~/bots/how-to/create-a-bot-commands-menu.md)

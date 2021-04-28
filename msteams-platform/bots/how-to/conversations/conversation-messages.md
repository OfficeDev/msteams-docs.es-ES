---
title: Mensajes en conversaciones de bot
description: Describe formas de tener una conversación con un bot de Microsoft Teams
ms.topic: overview
ms.author: anclear
localization_priority: Normal
keyword: receive message send message picture message channel data adaptive cards
ms.openlocfilehash: 5b23e3b2548e3d0eab98fae73d37316063fe60c1
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058603"
---
# <a name="messages-in-bot-conversations"></a><span data-ttu-id="acb9c-103">Mensajes en conversaciones de bot</span><span class="sxs-lookup"><span data-stu-id="acb9c-103">Messages in bot conversations</span></span>

<span data-ttu-id="acb9c-104">Cada mensaje de una conversación es un `Activity` objeto de tipo `messageType: message` .</span><span class="sxs-lookup"><span data-stu-id="acb9c-104">Each message in a conversation is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="acb9c-105">Cuando un usuario envía un mensaje, Teams publica el mensaje en el bot.</span><span class="sxs-lookup"><span data-stu-id="acb9c-105">When a user sends a message, Teams posts the message to your bot.</span></span> <span data-ttu-id="acb9c-106">Teams envía un objeto JSON al extremo de mensajería del bot.</span><span class="sxs-lookup"><span data-stu-id="acb9c-106">Teams sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="acb9c-107">El bot examina el mensaje para determinar su tipo y responde en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="acb9c-107">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="acb9c-108">Las conversaciones básicas se controlan a través del conector de Bot Framework, una única API de REST.</span><span class="sxs-lookup"><span data-stu-id="acb9c-108">Basic conversations are handled through the Bot Framework connector, a single REST API.</span></span> <span data-ttu-id="acb9c-109">Esta API permite que el bot se comunique con Teams y otros canales.</span><span class="sxs-lookup"><span data-stu-id="acb9c-109">This API enables your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="acb9c-110">El SDK de Bot Builder proporciona las siguientes características:</span><span class="sxs-lookup"><span data-stu-id="acb9c-110">The Bot Builder SDK provides the following features:</span></span>

* <span data-ttu-id="acb9c-111">Fácil acceso al conector de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="acb9c-111">Easy access to the Bot Framework connector.</span></span>
* <span data-ttu-id="acb9c-112">Funcionalidad adicional para administrar el estado y el flujo de conversación.</span><span class="sxs-lookup"><span data-stu-id="acb9c-112">Additional functionality to manage conversation flow and state.</span></span>
* <span data-ttu-id="acb9c-113">Formas sencillas de incorporar servicios cognitivos, como el procesamiento de lenguaje natural (NLP).</span><span class="sxs-lookup"><span data-stu-id="acb9c-113">Simple ways to incorporate cognitive services, such as natural language processing (NLP).</span></span>

<span data-ttu-id="acb9c-114">El bot recibe mensajes de Teams mediante la propiedad y envía una `Text` o varias respuestas de mensaje a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="acb9c-114">Your bot receives messages from Teams using the `Text` property and it sends single or multiple message responses to the users.</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="acb9c-115">Recibir un mensaje</span><span class="sxs-lookup"><span data-stu-id="acb9c-115">Receive a message</span></span>

<span data-ttu-id="acb9c-116">Para recibir un mensaje de texto, use la propiedad `Text` del objeto `Activity`.</span><span class="sxs-lookup"><span data-stu-id="acb9c-116">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="acb9c-117">En el controlador de actividades del bot, use convertir `Activity` del objeto de contexto para leer una solicitud de mensaje única.</span><span class="sxs-lookup"><span data-stu-id="acb9c-117">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="acb9c-118">El siguiente código muestra un ejemplo de recepción de un mensaje:</span><span class="sxs-lookup"><span data-stu-id="acb9c-118">The following code shows an example of receiving a message:</span></span>

# <a name="c"></a>[<span data-ttu-id="acb9c-119">C#</span><span class="sxs-lookup"><span data-stu-id="acb9c-119">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescript"></a>[<span data-ttu-id="acb9c-120">TypeScript</span><span class="sxs-lookup"><span data-stu-id="acb9c-120">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="acb9c-121">Python</span><span class="sxs-lookup"><span data-stu-id="acb9c-121">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="acb9c-122">JSON</span><span class="sxs-lookup"><span data-stu-id="acb9c-122">JSON</span></span>](#tab/json)

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

## <a name="send-a-message"></a><span data-ttu-id="acb9c-123">Enviar un mensaje</span><span class="sxs-lookup"><span data-stu-id="acb9c-123">Send a message</span></span>

<span data-ttu-id="acb9c-124">Para enviar un mensaje de texto, especifique la string que desee enviar como actividad.</span><span class="sxs-lookup"><span data-stu-id="acb9c-124">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="acb9c-125">En el controlador de actividad del bot, use el método del objeto turn context `SendActivityAsync` para enviar una única respuesta de mensaje.</span><span class="sxs-lookup"><span data-stu-id="acb9c-125">In the bot's activity handler, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="acb9c-126">Use el método del `SendActivitiesAsync` objeto para enviar varias respuestas a la vez.</span><span class="sxs-lookup"><span data-stu-id="acb9c-126">Use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span>

<span data-ttu-id="acb9c-127">El siguiente código muestra un ejemplo de envío de un mensaje cuando se agrega un usuario a una conversación:</span><span class="sxs-lookup"><span data-stu-id="acb9c-127">The following code shows an example of sending a message when a user is added to a conversation:</span></span>

# <a name="c"></a>[<span data-ttu-id="acb9c-128">C#</span><span class="sxs-lookup"><span data-stu-id="acb9c-128">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescript"></a>[<span data-ttu-id="acb9c-129">TypeScript</span><span class="sxs-lookup"><span data-stu-id="acb9c-129">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="acb9c-130">Python</span><span class="sxs-lookup"><span data-stu-id="acb9c-130">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="acb9c-131">JSON</span><span class="sxs-lookup"><span data-stu-id="acb9c-131">JSON</span></span>](#tab/json)

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
> <span data-ttu-id="acb9c-132">La división de mensajes se produce cuando se envían un mensaje de texto y datos adjuntos en la misma carga de actividad.</span><span class="sxs-lookup"><span data-stu-id="acb9c-132">Message splitting occurs when a text message and an attachment are sent in the same activity payload.</span></span> <span data-ttu-id="acb9c-133">Microsoft Teams divide esta actividad en actividades independientes, una con solo un mensaje de texto y otra con datos adjuntos.</span><span class="sxs-lookup"><span data-stu-id="acb9c-133">This activity is split into separate activities by Microsoft Teams, one with just a text message and the other with an attachment.</span></span> <span data-ttu-id="acb9c-134">Como la actividad está dividida, no recibe el identificador de mensaje en respuesta, que se usa para actualizar o [eliminar](~/bots/how-to/update-and-delete-bot-messages.md) el mensaje de forma proactiva.</span><span class="sxs-lookup"><span data-stu-id="acb9c-134">As the activity is split, you do not receive the message ID in response, which is used to [update or delete](~/bots/how-to/update-and-delete-bot-messages.md) the message proactively.</span></span> <span data-ttu-id="acb9c-135">Se recomienda enviar actividades independientes en lugar de depender de la división de mensajes.</span><span class="sxs-lookup"><span data-stu-id="acb9c-135">It is recommended to send separate activities instead of depending on message splitting.</span></span>

<span data-ttu-id="acb9c-136">Los mensajes enviados entre usuarios y bots incluyen datos de canal internos dentro del mensaje.</span><span class="sxs-lookup"><span data-stu-id="acb9c-136">Messages sent between users and bots include internal channel data within the message.</span></span> <span data-ttu-id="acb9c-137">Estos datos permiten al bot comunicarse correctamente en ese canal.</span><span class="sxs-lookup"><span data-stu-id="acb9c-137">This data allows the bot to communicate properly on that channel.</span></span> <span data-ttu-id="acb9c-138">El SDK del generador de bots permite modificar la estructura del mensaje.</span><span class="sxs-lookup"><span data-stu-id="acb9c-138">The Bot Builder SDK allows you to modify the message structure.</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="acb9c-139">Datos del canal de Teams</span><span class="sxs-lookup"><span data-stu-id="acb9c-139">Teams channel data</span></span>

<span data-ttu-id="acb9c-140">El `channelData` objeto contiene información específica de Teams y es un origen definitivo para los IDs de equipo y canal.</span><span class="sxs-lookup"><span data-stu-id="acb9c-140">The `channelData` object contains Teams-specific information and is a definitive source for team and channel IDs.</span></span> <span data-ttu-id="acb9c-141">Opcionalmente, puede almacenar en caché y usar estos IDs como claves para el almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="acb9c-141">Optionally, you can cache and use these IDs as keys for local storage.</span></span> <span data-ttu-id="acb9c-142">El SDK extrae información importante del objeto para que `TeamsActivityHandler` `channelData` sea fácilmente accesible.</span><span class="sxs-lookup"><span data-stu-id="acb9c-142">The `TeamsActivityHandler` in the SDK pulls out important information from the `channelData` object to make it easily accessible.</span></span> <span data-ttu-id="acb9c-143">Sin embargo, siempre puede tener acceso a los datos originales desde el `turnContext` objeto.</span><span class="sxs-lookup"><span data-stu-id="acb9c-143">However, you can always access the original data from the `turnContext` object.</span></span>

<span data-ttu-id="acb9c-144">El objeto no se incluye en los mensajes de conversaciones personales, ya que tienen lugar `channelData` fuera de un canal.</span><span class="sxs-lookup"><span data-stu-id="acb9c-144">The `channelData` object is not included in messages in personal conversations, as these take place outside of a channel.</span></span>

<span data-ttu-id="acb9c-145">Un objeto `channelData` típico de una actividad enviada al bot contiene la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="acb9c-145">A typical `channelData` object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="acb9c-146">`eventType`: Tipo de evento de Teams pasado solo en casos de [eventos de modificación de canal](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="acb9c-146">`eventType`: Teams event type passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="acb9c-147">`tenant.id`: Identificador de inquilino de Azure Active Directory pasado en todos los contextos.</span><span class="sxs-lookup"><span data-stu-id="acb9c-147">`tenant.id`: Azure Active Directory tenant ID passed in all contexts.</span></span>
* <span data-ttu-id="acb9c-148">`team`: Se pasa solo en contextos de canal, no en chat personal.</span><span class="sxs-lookup"><span data-stu-id="acb9c-148">`team`: Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="acb9c-149">`id`: GUID para el canal.</span><span class="sxs-lookup"><span data-stu-id="acb9c-149">`id`: GUID for the channel.</span></span>
  * <span data-ttu-id="acb9c-150">`name`: Nombre del equipo pasado solo en casos de [eventos de cambio de nombre de equipo](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="acb9c-150">`name`: Name of the team passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="acb9c-151">`channel`: Se pasa solo en contextos de canal cuando se menciona el bot o para eventos en canales de equipos donde se ha agregado el bot.</span><span class="sxs-lookup"><span data-stu-id="acb9c-151">`channel`: Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added.</span></span>
  * <span data-ttu-id="acb9c-152">`id`: GUID para el canal.</span><span class="sxs-lookup"><span data-stu-id="acb9c-152">`id`: GUID for the channel.</span></span>
  * <span data-ttu-id="acb9c-153">`name`: Nombre del canal pasado solo en casos de [eventos de modificación de canal](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="acb9c-153">`name`: Channel name passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="acb9c-154">`channelData.teamsTeamId`: En desuso.</span><span class="sxs-lookup"><span data-stu-id="acb9c-154">`channelData.teamsTeamId`: Deprecated.</span></span> <span data-ttu-id="acb9c-155">Esta propiedad solo se incluye por compatibilidad con versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="acb9c-155">This property is only included for backward compatibility.</span></span>
* <span data-ttu-id="acb9c-156">`channelData.teamsChannelId`: En desuso.</span><span class="sxs-lookup"><span data-stu-id="acb9c-156">`channelData.teamsChannelId`: Deprecated.</span></span> <span data-ttu-id="acb9c-157">Esta propiedad solo se incluye por compatibilidad con versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="acb9c-157">This property is only included for backward compatibility.</span></span>

### <a name="example-channeldata-object-or-channelcreated-event"></a><span data-ttu-id="acb9c-158">Evento channelData de ejemplo o channelCreated</span><span class="sxs-lookup"><span data-stu-id="acb9c-158">Example channelData object or channelCreated event</span></span>

<span data-ttu-id="acb9c-159">El siguiente código muestra un ejemplo del objeto channelData:</span><span class="sxs-lookup"><span data-stu-id="acb9c-159">The following code shows an example of channelData object:</span></span>

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

<span data-ttu-id="acb9c-160">Los mensajes recibidos o enviados al bot pueden incluir diferentes tipos de contenido de mensaje.</span><span class="sxs-lookup"><span data-stu-id="acb9c-160">Messages received from or sent to your bot can include different types of message content.</span></span>

## <a name="message-content"></a><span data-ttu-id="acb9c-161">Contenido del mensaje</span><span class="sxs-lookup"><span data-stu-id="acb9c-161">Message content</span></span>

| <span data-ttu-id="acb9c-162">Formato</span><span class="sxs-lookup"><span data-stu-id="acb9c-162">Format</span></span>    | <span data-ttu-id="acb9c-163">De usuario a bot</span><span class="sxs-lookup"><span data-stu-id="acb9c-163">From user to bot</span></span> | <span data-ttu-id="acb9c-164">De bot a usuario</span><span class="sxs-lookup"><span data-stu-id="acb9c-164">From bot to user</span></span> | <span data-ttu-id="acb9c-165">Notas</span><span class="sxs-lookup"><span data-stu-id="acb9c-165">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="acb9c-166">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="acb9c-166">Rich text</span></span> | <span data-ttu-id="acb9c-167">✔</span><span class="sxs-lookup"><span data-stu-id="acb9c-167">✔</span></span>                | <span data-ttu-id="acb9c-168">✔</span><span class="sxs-lookup"><span data-stu-id="acb9c-168">✔</span></span>                | <span data-ttu-id="acb9c-169">El bot puede enviar texto enriquecido, imágenes y tarjetas.</span><span class="sxs-lookup"><span data-stu-id="acb9c-169">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="acb9c-170">Los usuarios pueden enviar texto enriquecido e imágenes al bot.</span><span class="sxs-lookup"><span data-stu-id="acb9c-170">Users can send rich text and pictures to your bot.</span></span>                                                                                        |
| <span data-ttu-id="acb9c-171">Imágenes</span><span class="sxs-lookup"><span data-stu-id="acb9c-171">Pictures</span></span>  | <span data-ttu-id="acb9c-172">✔</span><span class="sxs-lookup"><span data-stu-id="acb9c-172">✔</span></span>                | <span data-ttu-id="acb9c-173">✔</span><span class="sxs-lookup"><span data-stu-id="acb9c-173">✔</span></span>                | <span data-ttu-id="acb9c-174">Máximo 1024×1024 y 1 MB en formato PNG, JPEG o GIF.</span><span class="sxs-lookup"><span data-stu-id="acb9c-174">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="acb9c-175">Gif animado no es compatible.</span><span class="sxs-lookup"><span data-stu-id="acb9c-175">Animated GIF is not supported.</span></span>  |
| <span data-ttu-id="acb9c-176">Tarjetas</span><span class="sxs-lookup"><span data-stu-id="acb9c-176">Cards</span></span>     | <span data-ttu-id="acb9c-177">✖</span><span class="sxs-lookup"><span data-stu-id="acb9c-177">✖</span></span>                | <span data-ttu-id="acb9c-178">✔</span><span class="sxs-lookup"><span data-stu-id="acb9c-178">✔</span></span>                | <span data-ttu-id="acb9c-179">Consulta la referencia [de la tarjeta de Teams](~/task-modules-and-cards/cards/cards-reference.md) para obtener las tarjetas compatibles.</span><span class="sxs-lookup"><span data-stu-id="acb9c-179">See the [Teams card reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards.</span></span> |
| <span data-ttu-id="acb9c-180">Emojis</span><span class="sxs-lookup"><span data-stu-id="acb9c-180">Emojis</span></span>    | <span data-ttu-id="acb9c-181">✖</span><span class="sxs-lookup"><span data-stu-id="acb9c-181">✖</span></span>                | <span data-ttu-id="acb9c-182">✔</span><span class="sxs-lookup"><span data-stu-id="acb9c-182">✔</span></span>                | <span data-ttu-id="acb9c-183">Actualmente, Teams admite emojis a través de UTF-16, como U+1F600 para el rostro sonriente.</span><span class="sxs-lookup"><span data-stu-id="acb9c-183">Teams currently supports emojis through UTF-16, such as U+1F600 for grinning face.</span></span> |

<span data-ttu-id="acb9c-184">También puede agregar notificaciones al mensaje mediante la `Notification.Alert` propiedad.</span><span class="sxs-lookup"><span data-stu-id="acb9c-184">You can also add notifications to your message using the `Notification.Alert` property.</span></span>

## <a name="notifications-to-your-message"></a><span data-ttu-id="acb9c-185">Notificaciones al mensaje</span><span class="sxs-lookup"><span data-stu-id="acb9c-185">Notifications to your message</span></span>

<span data-ttu-id="acb9c-186">Las notificaciones alertan a los usuarios sobre nuevas tareas, menciones y comentarios.</span><span class="sxs-lookup"><span data-stu-id="acb9c-186">Notifications alert users about new tasks, mentions, and comments.</span></span> <span data-ttu-id="acb9c-187">Estas alertas están relacionadas con lo que los usuarios están trabajando o lo que deben ver insertando un aviso en su fuente de actividad.</span><span class="sxs-lookup"><span data-stu-id="acb9c-187">These alerts are related to what users are working on or what they must look at by inserting a notice into their activity feed.</span></span> <span data-ttu-id="acb9c-188">Para que las notificaciones se desencadene desde el mensaje del bot, establezca la `TeamsChannelData` propiedad objects en `Notification.Alert` *true*.</span><span class="sxs-lookup"><span data-stu-id="acb9c-188">For notifications to trigger from your bot message, set the `TeamsChannelData` objects `Notification.Alert` property to *true*.</span></span> <span data-ttu-id="acb9c-189">Si se genera o no una notificación depende de la configuración de Teams del usuario individual y no se puede invalidar esta configuración.</span><span class="sxs-lookup"><span data-stu-id="acb9c-189">Whether or not a notification is raised depends on the individual user's Teams settings and you cannot override these settings.</span></span> <span data-ttu-id="acb9c-190">El tipo de notificación es un banner o un banner y un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="acb9c-190">The notification type is either a banner, or both a banner and an email.</span></span>

> [!NOTE]
> <span data-ttu-id="acb9c-191">El **campo Resumen** muestra cualquier texto del usuario como un mensaje de notificación en la fuente.</span><span class="sxs-lookup"><span data-stu-id="acb9c-191">The **Summary** field displays any text from the user as a notification message in the feed.</span></span>

<span data-ttu-id="acb9c-192">El siguiente código muestra un ejemplo de cómo agregar notificaciones al mensaje:</span><span class="sxs-lookup"><span data-stu-id="acb9c-192">The following code shows an example of adding notifications to your message:</span></span>

# <a name="c"></a>[<span data-ttu-id="acb9c-193">C#</span><span class="sxs-lookup"><span data-stu-id="acb9c-193">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescript"></a>[<span data-ttu-id="acb9c-194">TypeScript</span><span class="sxs-lookup"><span data-stu-id="acb9c-194">TypeScript</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="acb9c-195">Python</span><span class="sxs-lookup"><span data-stu-id="acb9c-195">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="acb9c-196">JSON</span><span class="sxs-lookup"><span data-stu-id="acb9c-196">JSON</span></span>](#tab/json)

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

<span data-ttu-id="acb9c-197">Para mejorar el mensaje, puede incluir imágenes como datos adjuntos a ese mensaje.</span><span class="sxs-lookup"><span data-stu-id="acb9c-197">To enhance your message, you can include pictures as attachments to that message.</span></span>

## <a name="picture-messages"></a><span data-ttu-id="acb9c-198">Mensajes de imagen</span><span class="sxs-lookup"><span data-stu-id="acb9c-198">Picture messages</span></span>

<span data-ttu-id="acb9c-199">Las imágenes se envían agregando datos adjuntos a un mensaje.</span><span class="sxs-lookup"><span data-stu-id="acb9c-199">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="acb9c-200">Para obtener más información sobre los datos [adjuntos,](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)consulte Bot Framework documentation .</span><span class="sxs-lookup"><span data-stu-id="acb9c-200">For more information on attachments, see [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments).</span></span>

<span data-ttu-id="acb9c-201">Las imágenes pueden tener como máximo 1024×1024 y 1 MB en formato PNG, JPEG o GIF.</span><span class="sxs-lookup"><span data-stu-id="acb9c-201">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="acb9c-202">Gif animado no es compatible.</span><span class="sxs-lookup"><span data-stu-id="acb9c-202">Animated GIF is not supported.</span></span>

<span data-ttu-id="acb9c-203">Especifique el alto y el ancho de cada imagen mediante XML.</span><span class="sxs-lookup"><span data-stu-id="acb9c-203">Specify the height and width of each image by using XML.</span></span> <span data-ttu-id="acb9c-204">En markdown, el tamaño de imagen es predeterminado 256×256.</span><span class="sxs-lookup"><span data-stu-id="acb9c-204">In markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="acb9c-205">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="acb9c-205">For example:</span></span>

* <span data-ttu-id="acb9c-206">Use: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>` .</span><span class="sxs-lookup"><span data-stu-id="acb9c-206">Use: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`.</span></span>
* <span data-ttu-id="acb9c-207">No usar: `![Duck on a rock](http://aka.ms/Fo983c)` .</span><span class="sxs-lookup"><span data-stu-id="acb9c-207">Do not use: `![Duck on a rock](http://aka.ms/Fo983c)`.</span></span>

<span data-ttu-id="acb9c-208">Un bot conversacional puede incluir tarjetas adaptables que simplifican los flujos de trabajo empresariales.</span><span class="sxs-lookup"><span data-stu-id="acb9c-208">A conversational bot can include Adaptive Cards that simplify business workflows.</span></span> <span data-ttu-id="acb9c-209">Las tarjetas adaptables ofrecen texto personalizable enriquecido, voz, imágenes, botones y campos de entrada.</span><span class="sxs-lookup"><span data-stu-id="acb9c-209">Adaptive Cards offer rich customizable text, speech, images, buttons, and input fields.</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="acb9c-210">Tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="acb9c-210">Adaptive Cards</span></span>

<span data-ttu-id="acb9c-211">Las tarjetas adaptables se pueden crear en un bot y mostrarse en varias aplicaciones, como Teams, tu sitio web, entre otras.</span><span class="sxs-lookup"><span data-stu-id="acb9c-211">Adaptive Cards can be authored in a bot and shown in multiple apps such as Teams, your website, and so on.</span></span> <span data-ttu-id="acb9c-212">Para obtener más información, vea [Adaptive Cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span><span class="sxs-lookup"><span data-stu-id="acb9c-212">For more information, see [Adaptive Cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>

<span data-ttu-id="acb9c-213">El siguiente código muestra un ejemplo de envío de una tarjeta adaptable sencilla:</span><span class="sxs-lookup"><span data-stu-id="acb9c-213">The following code shows an example of sending a simple Adaptive Card:</span></span>

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

<span data-ttu-id="acb9c-214">Para obtener más información acerca de las tarjetas y las tarjetas de los bots, consulte [la documentación sobre tarjetas](~/task-modules-and-cards/what-are-cards.md).</span><span class="sxs-lookup"><span data-stu-id="acb9c-214">To know more about cards and cards in bots, see [cards documentation](~/task-modules-and-cards/what-are-cards.md).</span></span>

## <a name="status-code-responses"></a><span data-ttu-id="acb9c-215">Respuestas de código de estado</span><span class="sxs-lookup"><span data-stu-id="acb9c-215">Status code responses</span></span>

<span data-ttu-id="acb9c-216">A continuación se desenván los códigos de estado y sus valores de mensaje y código de error:</span><span class="sxs-lookup"><span data-stu-id="acb9c-216">Following are the status codes and their error code and message values:</span></span>

| <span data-ttu-id="acb9c-217">Código de estado</span><span class="sxs-lookup"><span data-stu-id="acb9c-217">Status code</span></span> | <span data-ttu-id="acb9c-218">Código de error y valores de mensaje</span><span class="sxs-lookup"><span data-stu-id="acb9c-218">Error code and message values</span></span> | <span data-ttu-id="acb9c-219">Description</span><span class="sxs-lookup"><span data-stu-id="acb9c-219">Description</span></span> |
|----------------|-----------------|-----------------|
| <span data-ttu-id="acb9c-220">403</span><span class="sxs-lookup"><span data-stu-id="acb9c-220">403</span></span> | <span data-ttu-id="acb9c-221">**Código**: `ConversationBlockedByUser`</span><span class="sxs-lookup"><span data-stu-id="acb9c-221">**Code**: `ConversationBlockedByUser`</span></span> <br/> <span data-ttu-id="acb9c-222">**Mensaje:** El usuario bloqueó la conversación con el bot.</span><span class="sxs-lookup"><span data-stu-id="acb9c-222">**Message**: User blocked the conversation with the bot.</span></span> | <span data-ttu-id="acb9c-223">El usuario bloqueó el bot en un chat 1:1 o un canal mediante la configuración de moderación.</span><span class="sxs-lookup"><span data-stu-id="acb9c-223">User blocked the bot in 1:1 chat or a channel through moderation settings.</span></span> |
| <span data-ttu-id="acb9c-224">403</span><span class="sxs-lookup"><span data-stu-id="acb9c-224">403</span></span> | <span data-ttu-id="acb9c-225">**Código**: `BotNotInConversationRoster`</span><span class="sxs-lookup"><span data-stu-id="acb9c-225">**Code**: `BotNotInConversationRoster`</span></span> <br/> <span data-ttu-id="acb9c-226">**Mensaje:** el bot no forma parte de la lista de conversaciones.</span><span class="sxs-lookup"><span data-stu-id="acb9c-226">**Message**: The bot is not part of the conversation roster.</span></span> | <span data-ttu-id="acb9c-227">El bot no forma parte de la conversación.</span><span class="sxs-lookup"><span data-stu-id="acb9c-227">The bot is not part of the conversation.</span></span> |
| <span data-ttu-id="acb9c-228">403</span><span class="sxs-lookup"><span data-stu-id="acb9c-228">403</span></span> | <span data-ttu-id="acb9c-229">**Código**: `BotDisabledByAdmin`</span><span class="sxs-lookup"><span data-stu-id="acb9c-229">**Code**: `BotDisabledByAdmin`</span></span> <br/> <span data-ttu-id="acb9c-230">**Mensaje:** el administrador de inquilinos deshabilitó este bot.</span><span class="sxs-lookup"><span data-stu-id="acb9c-230">**Message**: The tenant admin disabled this bot.</span></span> | <span data-ttu-id="acb9c-231">El inquilino bloqueó el bot.</span><span class="sxs-lookup"><span data-stu-id="acb9c-231">Tenant blocked the bot.</span></span> |
| <span data-ttu-id="acb9c-232">401</span><span class="sxs-lookup"><span data-stu-id="acb9c-232">401</span></span> | <span data-ttu-id="acb9c-233">**Código**: `BotNotRegistered`</span><span class="sxs-lookup"><span data-stu-id="acb9c-233">**Code**: `BotNotRegistered`</span></span> <br/> <span data-ttu-id="acb9c-234">**Mensaje:** no se encontró ningún registro para este bot.</span><span class="sxs-lookup"><span data-stu-id="acb9c-234">**Message**: No registration found for this bot.</span></span> | <span data-ttu-id="acb9c-235">No se encontró el registro de este bot.</span><span class="sxs-lookup"><span data-stu-id="acb9c-235">The registration for this bot was not found.</span></span> |
| <span data-ttu-id="acb9c-236">412</span><span class="sxs-lookup"><span data-stu-id="acb9c-236">412</span></span> | <span data-ttu-id="acb9c-237">**Código**: `PreconditionFailed`</span><span class="sxs-lookup"><span data-stu-id="acb9c-237">**Code**: `PreconditionFailed`</span></span> <br/> <span data-ttu-id="acb9c-238">**Mensaje**: Error en la condición previa, inténtelo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="acb9c-238">**Message**: Precondition failed, please try again.</span></span> | <span data-ttu-id="acb9c-239">Error en una de nuestras dependencias debido a varias operaciones simultáneas en la misma conversación.</span><span class="sxs-lookup"><span data-stu-id="acb9c-239">A precondition failed on one of our dependencies due to multiple concurrent operations on the same conversation.</span></span> |
| <span data-ttu-id="acb9c-240">404</span><span class="sxs-lookup"><span data-stu-id="acb9c-240">404</span></span> | <span data-ttu-id="acb9c-241">**Código**: `ConversationNotFound`</span><span class="sxs-lookup"><span data-stu-id="acb9c-241">**Code**: `ConversationNotFound`</span></span> <br/> <span data-ttu-id="acb9c-242">**Mensaje:** No se encontró la conversación.</span><span class="sxs-lookup"><span data-stu-id="acb9c-242">**Message**: Conversation not found.</span></span> | <span data-ttu-id="acb9c-243">No se encontró la conversación.</span><span class="sxs-lookup"><span data-stu-id="acb9c-243">The conversation was not found.</span></span> |
| <span data-ttu-id="acb9c-244">413</span><span class="sxs-lookup"><span data-stu-id="acb9c-244">413</span></span> | <span data-ttu-id="acb9c-245">**Código**: `MessageSizeTooBig`</span><span class="sxs-lookup"><span data-stu-id="acb9c-245">**Code**: `MessageSizeTooBig`</span></span> <br/> <span data-ttu-id="acb9c-246">**Mensaje:** Tamaño del mensaje demasiado grande.</span><span class="sxs-lookup"><span data-stu-id="acb9c-246">**Message**: Message size too large.</span></span> | <span data-ttu-id="acb9c-247">El tamaño de la solicitud entrante era demasiado grande.</span><span class="sxs-lookup"><span data-stu-id="acb9c-247">The size on the incoming request was too large.</span></span> |
| <span data-ttu-id="acb9c-248">429</span><span class="sxs-lookup"><span data-stu-id="acb9c-248">429</span></span> | <span data-ttu-id="acb9c-249">**Código**: `Throttled`</span><span class="sxs-lookup"><span data-stu-id="acb9c-249">**Code**: `Throttled`</span></span> <br/> <span data-ttu-id="acb9c-250">**Mensaje:** Demasiadas solicitudes.</span><span class="sxs-lookup"><span data-stu-id="acb9c-250">**Message**: Too many requests.</span></span> <span data-ttu-id="acb9c-251">También devuelve cuándo reintentar después.</span><span class="sxs-lookup"><span data-stu-id="acb9c-251">Also returns when to retry after.</span></span> | <span data-ttu-id="acb9c-252">El bot envió demasiadas solicitudes.</span><span class="sxs-lookup"><span data-stu-id="acb9c-252">Too many requests were sent by the bot.</span></span> <span data-ttu-id="acb9c-253">Para obtener más información, vea [rate limit](~/bots/how-to/rate-limit.md).</span><span class="sxs-lookup"><span data-stu-id="acb9c-253">For more information, see [rate limit](~/bots/how-to/rate-limit.md).</span></span> |

## <a name="code-sample"></a><span data-ttu-id="acb9c-254">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="acb9c-254">Code sample</span></span>

|<span data-ttu-id="acb9c-255">Nombre de ejemplo</span><span class="sxs-lookup"><span data-stu-id="acb9c-255">Sample name</span></span> | <span data-ttu-id="acb9c-256">Description</span><span class="sxs-lookup"><span data-stu-id="acb9c-256">Description</span></span> | <span data-ttu-id="acb9c-257">. NETCore</span><span class="sxs-lookup"><span data-stu-id="acb9c-257">.NETCore</span></span> | <span data-ttu-id="acb9c-258">Node.js</span><span class="sxs-lookup"><span data-stu-id="acb9c-258">Node.js</span></span> | <span data-ttu-id="acb9c-259">Python</span><span class="sxs-lookup"><span data-stu-id="acb9c-259">Python</span></span> |
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="acb9c-260">Bot de conversación de Teams</span><span class="sxs-lookup"><span data-stu-id="acb9c-260">Teams conversation bot</span></span> | <span data-ttu-id="acb9c-261">Control de eventos de mensajería y conversación.</span><span class="sxs-lookup"><span data-stu-id="acb9c-261">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="acb9c-262">View</span><span class="sxs-lookup"><span data-stu-id="acb9c-262">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="acb9c-263">View</span><span class="sxs-lookup"><span data-stu-id="acb9c-263">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [<span data-ttu-id="acb9c-264">View</span><span class="sxs-lookup"><span data-stu-id="acb9c-264">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="see-also"></a><span data-ttu-id="acb9c-265">Vea también</span><span class="sxs-lookup"><span data-stu-id="acb9c-265">See also</span></span>

- [<span data-ttu-id="acb9c-266">Enviar mensajes proactivos</span><span class="sxs-lookup"><span data-stu-id="acb9c-266">Send proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)

- [<span data-ttu-id="acb9c-267">Suscribirse a eventos de conversación</span><span class="sxs-lookup"><span data-stu-id="acb9c-267">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

## <a name="next-step"></a><span data-ttu-id="acb9c-268">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="acb9c-268">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="acb9c-269">Menús de comandos bot</span><span class="sxs-lookup"><span data-stu-id="acb9c-269">Bot command menus</span></span>](~/bots/how-to/create-a-bot-commands-menu.md)

---
title: Conversaciones de canal y grupo con un bot
author: clearab
description: Cómo enviar, recibir y controlar mensajes de un bot en un chat de canal o grupo.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 8a9a58208fff5cc2fe376fcb9932bad6ac2bf36f
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797844"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="d4c67-103">Conversaciones de chat de canal y grupo con un bot de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d4c67-103">Channel and group chat conversations with a Microsoft Teams bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="d4c67-104">Al agregar el ámbito o al bot, puede estar disponible para instalarse en un chat de `teams` `groupchat` grupo o equipo.</span><span class="sxs-lookup"><span data-stu-id="d4c67-104">By adding the `teams` or `groupchat` scope to your bot, it can be available to be installed in a team or group chat.</span></span> <span data-ttu-id="d4c67-105">Esto permite que todos los miembros de la conversación interactúen con el bot.</span><span class="sxs-lookup"><span data-stu-id="d4c67-105">This allows all members of the conversation to interact with your bot.</span></span> <span data-ttu-id="d4c67-106">Una vez instalado, también tendrá acceso a metadatos sobre la conversación, como la lista de miembros de la conversación, y cuando se instala en los detalles de un equipo sobre ese equipo y la lista completa de canales.</span><span class="sxs-lookup"><span data-stu-id="d4c67-106">Once installed, it will also have access to metadata about the conversation like the list of conversation members, and when installed in a team details about that team and the full list of channels.</span></span>

<span data-ttu-id="d4c67-107">Los bots de un grupo o canal solo reciben mensajes cuando se mencionan (@botname), no reciben ningún otro mensaje enviado a la conversación.</span><span class="sxs-lookup"><span data-stu-id="d4c67-107">Bots in a group or channel only receive messages when they are mentioned (@botname), they do not receive any other messages sent to the conversation.</span></span>

> [!NOTE]
> <span data-ttu-id="d4c67-108">El bot debe ser @mentioned directamente.</span><span class="sxs-lookup"><span data-stu-id="d4c67-108">The bot must be @mentioned directly.</span></span> <span data-ttu-id="d4c67-109">El bot no recibirá un mensaje cuando se menciona al equipo o al canal, o cuando alguien responda a un mensaje de su bot sin @mentioning lo haga.</span><span class="sxs-lookup"><span data-stu-id="d4c67-109">Your bot will not receive a message when the team or channel is mentioned, or when someone replies to a message from your bot without @mentioning it.</span></span>

## <a name="design-guidelines"></a><span data-ttu-id="d4c67-110">Directrices de diseño</span><span class="sxs-lookup"><span data-stu-id="d4c67-110">Design guidelines</span></span>

<span data-ttu-id="d4c67-111">Vea cómo diseñar [conversaciones de bot en canales y chats.](~/bots/design/bots.md)</span><span class="sxs-lookup"><span data-stu-id="d4c67-111">See how to [design bot conversations in channels and chats](~/bots/design/bots.md).</span></span>

## <a name="creating-new-conversation-threads"></a><span data-ttu-id="d4c67-112">Creación de nuevos subprocesos de conversación</span><span class="sxs-lookup"><span data-stu-id="d4c67-112">Creating new conversation threads</span></span>

<span data-ttu-id="d4c67-113">Cuando el bot está instalado en un equipo, a veces puede ser necesario crear un nuevo hilo de conversación en lugar de responder a uno existente.</span><span class="sxs-lookup"><span data-stu-id="d4c67-113">When your bot is installed in a team, it can sometimes be necessary to create a new conversation thread rather than replying to an existing one.</span></span> <span data-ttu-id="d4c67-114">Se trata de una forma de [mensajería proactiva.](~/bots/how-to/conversations/send-proactive-messages.md)</span><span class="sxs-lookup"><span data-stu-id="d4c67-114">This is a form of [proactive messaging](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>

## <a name="working-with-mentions"></a><span data-ttu-id="d4c67-115">Trabajar con menciones</span><span class="sxs-lookup"><span data-stu-id="d4c67-115">Working with mentions</span></span>

<span data-ttu-id="d4c67-116">Cada mensaje a su bot desde un grupo o canal contendrá un @mention con su propio nombre en el texto del mensaje, por lo que tendrá que asegurarse de que el análisis de mensajes lo controla.</span><span class="sxs-lookup"><span data-stu-id="d4c67-116">Every message to your bot from a group or channel will contain an @mention with its own name in the message text, so you'll need to ensure your message parsing handles that.</span></span> <span data-ttu-id="d4c67-117">El bot también puede recuperar otros usuarios mencionados en un mensaje y agregar menciones a los mensajes que envíe.</span><span class="sxs-lookup"><span data-stu-id="d4c67-117">Your bot can also retrieve other users mentioned in a message, and add mentions to any messages it sends.</span></span>

### <a name="stripping-mentions-from-message-text"></a><span data-ttu-id="d4c67-118">Quitar menciones del texto del mensaje</span><span class="sxs-lookup"><span data-stu-id="d4c67-118">Stripping mentions from message text</span></span>

<span data-ttu-id="d4c67-119">Es posible que sea necesario quitar el @mentions del texto del mensaje que recibe el bot.</span><span class="sxs-lookup"><span data-stu-id="d4c67-119">You may find it necessary to strip out the @mentions from the text of the message your bot receives.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="d4c67-120">Recuperar menciones</span><span class="sxs-lookup"><span data-stu-id="d4c67-120">Retrieving mentions</span></span>

<span data-ttu-id="d4c67-121">Las menciones se devuelven en el objeto en carga y contienen el identificador único del usuario y, en la mayoría de los casos, el nombre `entities` del usuario mencionado.</span><span class="sxs-lookup"><span data-stu-id="d4c67-121">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="d4c67-122">El texto del mensaje también incluirá la mención como `<at>@John Smith<at>` .</span><span class="sxs-lookup"><span data-stu-id="d4c67-122">The text of the message will also include the mention like `<at>@John Smith<at>`.</span></span> <span data-ttu-id="d4c67-123">Sin embargo, no debe confiar en el texto del mensaje para recuperar información sobre el usuario; es posible que la persona que envía el mensaje lo modifique.</span><span class="sxs-lookup"><span data-stu-id="d4c67-123">However, you should not rely on the text in the message to retrieve any information about the user; it is possible for the person sending the message to alter it.</span></span> <span data-ttu-id="d4c67-124">En su lugar, use el `entities` objeto.</span><span class="sxs-lookup"><span data-stu-id="d4c67-124">Instead, use the `entities` object.</span></span>

<span data-ttu-id="d4c67-125">Puede recuperar todas las menciones del mensaje llamando a la función en el SDK de `GetMentions` Bot Builder que devuelve una matriz de `Mention` objetos.</span><span class="sxs-lookup"><span data-stu-id="d4c67-125">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK which returns an array of `Mention` objects.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="d4c67-126">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="d4c67-126">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    Mention[] mentions = turnContext.Activity.GetMentions();
    if(mentions != null)
    {
        ChannelAccount firstMention = mentions[0].Mentioned;
        await turnContext.SendActivityAsync($"Hello {firstMention.Name}");
    }
    else
    {
        await turnContext.SendActivityAsync("Aw, no one was mentioned.");
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="d4c67-127">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="d4c67-127">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    const mentions = TurnContext.getMentions(turnContext.activity);
    if (mentions){
        const firstMention = mentions[0].mentioned;
        await turnContext.sendActivity(`Hello ${firstMention.name}.`);
    } else {
        await turnContext.sendActivity(`Aw, no one was mentioned.`);
    }

    await next();
});
```

# <a name="json"></a>[<span data-ttu-id="d4c67-128">JSON</span><span class="sxs-lookup"><span data-stu-id="d4c67-128">JSON</span></span>](#tab/json)

```json
{
    "type": "message",
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "29:9e52142b-5e5e-4d7b-bb3e-e82dcf620000",
        "name": "Jane Smith"
    },
    "conversation": {
        "id": "19:aebd0ad4d6ab42c8b9ed19c251c2fc37@thread.skype;messageid=1481567603816"
    },
    "recipient": {
        "id": "8:orgid:6aebbad0-e5a5-424a-834a-20fb051f3c1a",
        "name": "stlrgload100"
    },
    "attachments": [
        {
            "contentType": "image/png",
            "contentUrl": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
            "name": "Bender_Rodriguez.png"
        }
    ],
    "entities": [
        {
            "type":"mention",
            "mentioned":{
                "id":"29:08q2j2o3jc09au90eucae",
                "name":"Pranav Smith"
            },
            "text": "<at>@Pranav Smith</at>"
        }
    ],
    "replyToId": "3UP4UTkzUk1zzeyW"
}
```

# <a name="python"></a>[<span data-ttu-id="d4c67-129">Python</span><span class="sxs-lookup"><span data-stu-id="d4c67-129">Python</span></span>](#tab/python)

```python
@staticmethod
def get_mentions(activity: Activity) -> List[Mention]:
    result: List[Mention] = []
    if activity.entities is not None:
        for entity in activity.entities:
            if entity.type.lower() == "mention":
                    result.append(entity)
     return result
```

* * *

### <a name="adding-mentions-to-your-messages"></a><span data-ttu-id="d4c67-130">Agregar menciones a los mensajes</span><span class="sxs-lookup"><span data-stu-id="d4c67-130">Adding mentions to your messages</span></span>

<span data-ttu-id="d4c67-131">El bot puede mencionar a otros usuarios en mensajes publicados en canales.</span><span class="sxs-lookup"><span data-stu-id="d4c67-131">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="d4c67-132">Para ello, el mensaje debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d4c67-132">To do this, your message must do the following:</span></span>

<span data-ttu-id="d4c67-133">El `Mention` objeto tiene dos propiedades que deberá establecer:</span><span class="sxs-lookup"><span data-stu-id="d4c67-133">The `Mention` object has two properties that you will need to set:</span></span>

* <span data-ttu-id="d4c67-134">Incluir <at>@username</at> en el texto del mensaje</span><span class="sxs-lookup"><span data-stu-id="d4c67-134">Include <at>@username</at> in the message text</span></span>
* <span data-ttu-id="d4c67-135">Incluir el objeto de mención dentro de la colección de entidades</span><span class="sxs-lookup"><span data-stu-id="d4c67-135">Include the mention object inside the entities collection</span></span>

<span data-ttu-id="d4c67-136">El SDK de Bot Framework proporciona objetos y métodos auxiliares para facilitar la construcción de la mención.</span><span class="sxs-lookup"><span data-stu-id="d4c67-136">The Bot Framework SDK provides helper methods and objects to make constructing the mention easier.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="d4c67-137">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="d4c67-137">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var mention = new Mention
    {
        Mentioned = turnContext.Activity.From,
        Text = $"<at>{XmlConvert.EncodeName(turnContext.Activity.From.Name)}</at>",
    };

    var replyActivity = MessageFactory.Text($"Hello {mention.Text}.");
    replyActivity.Entities = new List<Entity> { mention };

    await turnContext.SendActivityAsync(replyActivity, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="d4c67-138">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="d4c67-138">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    const mention = {
        mentioned: turnContext.activity.from,
        text: `<at>${ new TextEncoder().encode(turnContext.activity.from.name) }</at>`,
    } as Mention;

    const replyActivity = MessageFactory.text(`Hello ${mention.text}`);
    replyActivity.entities = [mention];

    await turnContext.sendActivity(replyActivity);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="json"></a>[<span data-ttu-id="d4c67-139">JSON</span><span class="sxs-lookup"><span data-stu-id="d4c67-139">JSON</span></span>](#tab/json)

<span data-ttu-id="d4c67-140">El `text` campo del objeto de la `entities` matriz debe coincidir *exactamente* con una parte del campo de `text` mensaje.</span><span class="sxs-lookup"><span data-stu-id="d4c67-140">The `text` field in the object in the `entities` array must *exactly* match a portion of the message `text` field.</span></span> <span data-ttu-id="d4c67-141">Si no es así, se omitirá la mención.</span><span class="sxs-lookup"><span data-stu-id="d4c67-141">If it does not, the mention will be ignored.</span></span>

```json
{
    "type": "message",
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "29:9e52142b-5e5e-4d7b-bb3e-e82dcf620000",
        "name": "Jane Smith"
    },
    "conversation": {
        "id": "19:aebd0ad4d6ab42c8b9ed19c251c2fc37@thread.skype;messageid=1481567603816"
    },
    "recipient": {
        "id": "8:orgid:6aebbad0-e5a5-424a-834a-20fb051f3c1a",
        "name": "stlrgload100"
    },
    "attachments": [
        {
            "contentType": "image/png",
            "contentUrl": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
            "name": "Bender_Rodriguez.png"
        }
    ],
    "entities": [
        {
            "type":"mention",
            "mentioned":{
                "id":"29:08q2j2o3jc09au90eucae",
                "name":"Pranav Smith"
            },
            "text": "<at>@Pranav Smith</at>"
        }
    ],
    "replyToId": "3UP4UTkzUk1zzeyW"
}
```

# <a name="python"></a>[<span data-ttu-id="d4c67-142">Python</span><span class="sxs-lookup"><span data-stu-id="d4c67-142">Python</span></span>](#tab/python)

```python
async def _mention_activity(self, turn_context: TurnContext):
        mention = Mention(
            mentioned=turn_context.activity.from_property,
            text=f"<at>{turn_context.activity.from_property.name}</at>",
            type="mention"
        )

        reply_activity = MessageFactory.text(f"Hello {mention.text}")
        reply_activity.entities = [Mention().deserialize(mention.serialize())]
        await turn_context.send_activity(reply_activity)
```

* * *

## <a name="sending-a-message-on-installation"></a><span data-ttu-id="d4c67-143">Enviar un mensaje durante la instalación</span><span class="sxs-lookup"><span data-stu-id="d4c67-143">Sending a message on installation</span></span>

<span data-ttu-id="d4c67-144">Cuando el bot se agrega por primera vez al grupo o equipo, puede resultar útil enviar un mensaje que lo presenta.</span><span class="sxs-lookup"><span data-stu-id="d4c67-144">When your bot is first added to the group or team, it may be useful to send a message introducing it.</span></span> <span data-ttu-id="d4c67-145">El mensaje debe proporcionar una breve descripción de las características del bot y cómo usarlas.</span><span class="sxs-lookup"><span data-stu-id="d4c67-145">The message should provide a brief description of the bot's features, and how to use them.</span></span> <span data-ttu-id="d4c67-146">You'll want to subscribe to the `conversationUpdate` event, with the `teamMemberAdded` eventType.</span><span class="sxs-lookup"><span data-stu-id="d4c67-146">You'll want to subscribe to the `conversationUpdate` event, with the `teamMemberAdded` eventType.</span></span>  <span data-ttu-id="d4c67-147">Dado que el evento se envía cuando se agrega un nuevo miembro del equipo, debe comprobar si el nuevo miembro agregado es el bot.</span><span class="sxs-lookup"><span data-stu-id="d4c67-147">Since the event is sent when any new team member is added, you need to check to determine if the new member added is the bot.</span></span> <span data-ttu-id="d4c67-148">Consulte [Enviar un mensaje de bienvenida a un nuevo miembro del equipo](~/bots/how-to/conversations/send-proactive-messages.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="d4c67-148">See [Sending a welcome message to a new team member](~/bots/how-to/conversations/send-proactive-messages.md) for more details.</span></span>

<span data-ttu-id="d4c67-149">Es posible que también desee enviar un mensaje personal a cada miembro del equipo cuando se agrega el bot.</span><span class="sxs-lookup"><span data-stu-id="d4c67-149">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="d4c67-150">Para ello, puede obtener la lista del equipo y enviar un mensaje directo a cada usuario.</span><span class="sxs-lookup"><span data-stu-id="d4c67-150">To do this, you could get the team roster and send each user a direct message.</span></span>

<span data-ttu-id="d4c67-151">No se recomienda enviar un mensaje en las siguientes situaciones:</span><span class="sxs-lookup"><span data-stu-id="d4c67-151">It is not recommended to send a message in the following situations:</span></span>

* <span data-ttu-id="d4c67-152">El equipo es grande (obviamente subjetivo, pero por ejemplo más de 100 miembros).</span><span class="sxs-lookup"><span data-stu-id="d4c67-152">The team is large (obviously subjective, but for example larger than 100 members).</span></span> <span data-ttu-id="d4c67-153">Es posible que el bot se vea como "spammy" y la persona que lo agregó puede recibir quejas a menos que comunique claramente la propuesta de valor del bot a todos los usuarios que vean el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="d4c67-153">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="d4c67-154">El bot se menciona por primera vez en un grupo o canal (frente a que se agrega por primera vez a un equipo)</span><span class="sxs-lookup"><span data-stu-id="d4c67-154">Your bot is first mentioned in a group or channel (versus being first added to a team)</span></span>
* <span data-ttu-id="d4c67-155">Se cambia el nombre de un grupo o canal</span><span class="sxs-lookup"><span data-stu-id="d4c67-155">A group or channel is renamed</span></span>
* <span data-ttu-id="d4c67-156">Se agrega un miembro del equipo a un grupo o canal</span><span class="sxs-lookup"><span data-stu-id="d4c67-156">A team member is added to a group or channel</span></span>

## <a name="learn-more"></a><span data-ttu-id="d4c67-157">Más información</span><span class="sxs-lookup"><span data-stu-id="d4c67-157">Learn more</span></span>

<span data-ttu-id="d4c67-158">El bot tiene acceso a información adicional sobre el chat en grupo o el equipo en el que está instalado.</span><span class="sxs-lookup"><span data-stu-id="d4c67-158">Your bot has access to additional information about the group chat or team it is installed in.</span></span> <span data-ttu-id="d4c67-159">Vea [obtener el contexto de teams](~/bots/how-to/get-teams-context.md) para obtener api adicionales disponibles para su bot.</span><span class="sxs-lookup"><span data-stu-id="d4c67-159">See [get teams context](~/bots/how-to/get-teams-context.md) for additional APIs available for your bot.</span></span>

<span data-ttu-id="d4c67-160">También hay eventos adicionales a los que el bot puede suscribirse y responder.</span><span class="sxs-lookup"><span data-stu-id="d4c67-160">There are also additional events that your bot can subscribe and respond to.</span></span> <span data-ttu-id="d4c67-161">Vea [suscribirse a eventos de conversación](~/bots/how-to/conversations/subscribe-to-conversation-events.md) para obtener información sobre cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="d4c67-161">See [subscribe to conversation events](~/bots/how-to/conversations/subscribe-to-conversation-events.md) to learn how.</span></span>

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

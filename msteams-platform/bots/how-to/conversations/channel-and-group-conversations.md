---
title: Conversaciones en canales y grupos
author: clearab
description: Cómo enviar, recibir y administrar mensajes para un bot en un canal o un chat en grupo.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: ccc27d7638820cfa3c2b7cfe12b91b3a3a9fef1d
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/31/2020
ms.locfileid: "44801526"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="351d3-103">Conversaciones de chat en grupo y en el canal con un bot de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="351d3-103">Channel and Group chat conversations with a Microsoft Teams bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="351d3-104">Al agregar el `teams` `groupchat` ámbito o al bot, puede estar disponible para instalarse en un chat de grupo o de equipo.</span><span class="sxs-lookup"><span data-stu-id="351d3-104">By adding the `teams` or `groupchat` scope to your bot, it can be available to be installed in a team or group chat.</span></span> <span data-ttu-id="351d3-105">Esto permite a todos los miembros de la conversación interactuar con el bot.</span><span class="sxs-lookup"><span data-stu-id="351d3-105">This allows all members of the conversation to interact with your bot.</span></span> <span data-ttu-id="351d3-106">Una vez instalado, también tendrá acceso a los metadatos sobre la conversación, como la lista de miembros de la conversación, y cuando se instale en un equipo detalles sobre ese equipo y la lista completa de canales.</span><span class="sxs-lookup"><span data-stu-id="351d3-106">Once installed, it will also have access to metadata about the conversation like the list of conversation members, and when installed in a team details about that team and the full list of channels.</span></span>

<span data-ttu-id="351d3-107">Los bots de un grupo o canal solo reciben mensajes cuando se mencionan ("@botname"), no reciben ningún otro mensaje que se envíe a la conversación.</span><span class="sxs-lookup"><span data-stu-id="351d3-107">Bots in a group or channel only receive messages when they are mentioned ("@botname"), they do not receive any other messages sent to the conversation.</span></span>

> [!NOTE]
> <span data-ttu-id="351d3-108">El bot debe estar @mentioned directamente.</span><span class="sxs-lookup"><span data-stu-id="351d3-108">The bot must be @mentioned directly.</span></span> <span data-ttu-id="351d3-109">El bot no recibirá un mensaje cuando se menciona el equipo o el canal, o cuando alguien responde a un mensaje desde el bot sin @mentioning.</span><span class="sxs-lookup"><span data-stu-id="351d3-109">Your bot will not receive a message when the team or channel is mentioned, or when someone replies to a message from your bot without @mentioning it.</span></span>

## <a name="design-considerations"></a><span data-ttu-id="351d3-110">Consideraciones sobre diseño</span><span class="sxs-lookup"><span data-stu-id="351d3-110">Design considerations</span></span>

<span data-ttu-id="351d3-111">Un bot debe proporcionar información que sea adecuada y relevante para todos los miembros de un grupo o canal.</span><span class="sxs-lookup"><span data-stu-id="351d3-111">A bot should provide information that is both appropriate and relevant to all members in a group or channel.</span></span> <span data-ttu-id="351d3-112">Las conversaciones con él son visibles para todos los usuarios que forman parte del grupo o del canal.</span><span class="sxs-lookup"><span data-stu-id="351d3-112">Conversations with it are visible to everyone that is a part of the group or channel.</span></span> <span data-ttu-id="351d3-113">Un robot bien diseñado puede agregar valor a todos los usuarios y no compartir involuntariamente información que sea más adecuada en una conversación de uno a uno.</span><span class="sxs-lookup"><span data-stu-id="351d3-113">A well designed bot can add value to all users while not inadvertently sharing information that is more appropriate in a one-to-one conversation.</span></span> <span data-ttu-id="351d3-114">En su lugar, las conversaciones de varios turnos, como los cuadros de diálogo, deben evitarse y usar tarjetas o módulos de tareas para recopilar información.</span><span class="sxs-lookup"><span data-stu-id="351d3-114">Multi-turn conversations like dialogs should be avoided - use cards and/or task modules to collect information instead.</span></span>

## <a name="creating-new-conversation-threads"></a><span data-ttu-id="351d3-115">Crear nuevos hilos de conversación</span><span class="sxs-lookup"><span data-stu-id="351d3-115">Creating new conversation threads</span></span>

<span data-ttu-id="351d3-116">Cuando se instala el bot en un equipo, a veces puede ser necesario crear una nueva secuencia de conversación en lugar de responder a una existente.</span><span class="sxs-lookup"><span data-stu-id="351d3-116">When your bot is installed in a team, it can sometimes be necessary to create a new conversation thread rather than replying to an existing one.</span></span> <span data-ttu-id="351d3-117">Esta es una forma de [Mensajería proactiva](~/bots/how-to/conversations/send-proactive-messages.md).</span><span class="sxs-lookup"><span data-stu-id="351d3-117">This is a form of [proactive messaging](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>

## <a name="working-with-mentions"></a><span data-ttu-id="351d3-118">Trabajar con menciones</span><span class="sxs-lookup"><span data-stu-id="351d3-118">Working with mentions</span></span>

<span data-ttu-id="351d3-119">Cada mensaje en el bot desde un grupo o canal contendrá un @mention con su propio nombre en el texto del mensaje, por lo que deberá asegurarse de que los controladores de análisis de mensajes lo hagan.</span><span class="sxs-lookup"><span data-stu-id="351d3-119">Every message to your bot from a group or channel will contain an @mention with its own name in the message text, so you'll need to ensure your message parsing handles that.</span></span> <span data-ttu-id="351d3-120">El bot también puede recuperar a otros usuarios mencionados en un mensaje y agregar menciones a los mensajes que envía.</span><span class="sxs-lookup"><span data-stu-id="351d3-120">Your bot can also retrieve other users mentioned in a message, and add mentions to any messages it sends.</span></span>

### <a name="stripping-mentions-from-message-text"></a><span data-ttu-id="351d3-121">Eliminación de menciones del texto del mensaje</span><span class="sxs-lookup"><span data-stu-id="351d3-121">Stripping mentions from message text</span></span>

<span data-ttu-id="351d3-122">Es posible que necesite quitar el @mentions del texto del mensaje que el bot recibe.</span><span class="sxs-lookup"><span data-stu-id="351d3-122">You may find it necessary to strip out the @mentions from the text of the message your bot receives.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="351d3-123">Recuperación de menciones</span><span class="sxs-lookup"><span data-stu-id="351d3-123">Retrieving mentions</span></span>

<span data-ttu-id="351d3-124">Las menciones se devuelven en el `entities` objeto en la carga y contienen el identificador único del usuario y, en la mayoría de los casos, el nombre del usuario mencionado.</span><span class="sxs-lookup"><span data-stu-id="351d3-124">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="351d3-125">El texto del mensaje también incluirá la mención like `<at>@John Smith<at>` .</span><span class="sxs-lookup"><span data-stu-id="351d3-125">The text of the message will also include the mention like `<at>@John Smith<at>`.</span></span> <span data-ttu-id="351d3-126">Sin embargo, no debe confiar en el texto del mensaje para recuperar la información sobre el usuario; es posible que la persona que envía el mensaje la altere.</span><span class="sxs-lookup"><span data-stu-id="351d3-126">However, you should not rely on the text in the message to retrieve any information about the user; it is possible for the person sending the message to alter it.</span></span> <span data-ttu-id="351d3-127">En su lugar, use el `entities` objeto.</span><span class="sxs-lookup"><span data-stu-id="351d3-127">Instead, use the `entities` object.</span></span>

<span data-ttu-id="351d3-128">Puede recuperar todas las menciones del mensaje llamando a la `GetMentions` función en el SDK del generador de robots que devuelve una matriz de `Mention` objetos.</span><span class="sxs-lookup"><span data-stu-id="351d3-128">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK which returns an array of `Mention` objects.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="351d3-129">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="351d3-129">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="351d3-130">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="351d3-130">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="351d3-131">JSON</span><span class="sxs-lookup"><span data-stu-id="351d3-131">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="351d3-132">Python</span><span class="sxs-lookup"><span data-stu-id="351d3-132">Python</span></span>](#tab/python)

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

### <a name="adding-mentions-to-your-messages"></a><span data-ttu-id="351d3-133">Adición de menciones a los mensajes</span><span class="sxs-lookup"><span data-stu-id="351d3-133">Adding mentions to your messages</span></span>

<span data-ttu-id="351d3-134">El bot puede mencionar a otros usuarios en los mensajes enviados a los canales.</span><span class="sxs-lookup"><span data-stu-id="351d3-134">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="351d3-135">Para ello, el mensaje debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="351d3-135">To do this, your message must do the following:</span></span>

<span data-ttu-id="351d3-136">El `Mention` objeto tiene dos propiedades que tendrá que establecer:</span><span class="sxs-lookup"><span data-stu-id="351d3-136">The `Mention` object has two properties that you will need to set:</span></span>

* <span data-ttu-id="351d3-137">Incluir <at>@username</at> en el texto del mensaje</span><span class="sxs-lookup"><span data-stu-id="351d3-137">Include <at>@username</at> in the message text</span></span>
* <span data-ttu-id="351d3-138">Incluir el objeto de menciones dentro de la colección Entities</span><span class="sxs-lookup"><span data-stu-id="351d3-138">Include the mention object inside the entities collection</span></span>

<span data-ttu-id="351d3-139">El SDK de bot proporciona objetos y métodos auxiliares para facilitar la creación de la mención.</span><span class="sxs-lookup"><span data-stu-id="351d3-139">The Bot Framework SDK provides helper methods and objects to make constructing the mention easier.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="351d3-140">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="351d3-140">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="351d3-141">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="351d3-141">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="351d3-142">JSON</span><span class="sxs-lookup"><span data-stu-id="351d3-142">JSON</span></span>](#tab/json)

<span data-ttu-id="351d3-143">El `text` campo del objeto de la `entities` matriz debe coincidir *exactamente* con una parte del `text` campo mensaje.</span><span class="sxs-lookup"><span data-stu-id="351d3-143">The `text` field in the object in the `entities` array must *exactly* match a portion of the message `text` field.</span></span> <span data-ttu-id="351d3-144">Si no es así, se omitirá la mención.</span><span class="sxs-lookup"><span data-stu-id="351d3-144">If it does not, the mention will be ignored.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="351d3-145">Python</span><span class="sxs-lookup"><span data-stu-id="351d3-145">Python</span></span>](#tab/python)

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

## <a name="sending-a-message-on-installation"></a><span data-ttu-id="351d3-146">Enviar un mensaje durante la instalación</span><span class="sxs-lookup"><span data-stu-id="351d3-146">Sending a message on installation</span></span>

<span data-ttu-id="351d3-147">Cuando el bot se agrega por primera vez al grupo o equipo, puede resultar útil enviar un mensaje que lo presenta.</span><span class="sxs-lookup"><span data-stu-id="351d3-147">When your bot is first added to the group or team, it may be useful to send a message introducing it.</span></span> <span data-ttu-id="351d3-148">El mensaje debe proporcionar una breve descripción de las características del bot y cómo usarlas.</span><span class="sxs-lookup"><span data-stu-id="351d3-148">The message should provide a brief description of the bot's features, and how to use them.</span></span> <span data-ttu-id="351d3-149">Querrá suscribirse al `conversationUpdate` evento con `teamMemberAdded` EventType.</span><span class="sxs-lookup"><span data-stu-id="351d3-149">You'll want to subscribe to the `conversationUpdate` event, with the `teamMemberAdded` eventType.</span></span>  <span data-ttu-id="351d3-150">Dado que el evento se envía cuando se agrega un nuevo miembro del equipo, debe comprobarlo para determinar si el nuevo miembro agregado es el bot.</span><span class="sxs-lookup"><span data-stu-id="351d3-150">Since the event is sent when any new team member is added, you need to check to determine if the new member added is the bot.</span></span> <span data-ttu-id="351d3-151">Consulte [Enviar un mensaje de bienvenida a un nuevo integrante del equipo](~/bots/how-to/conversations/send-proactive-messages.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="351d3-151">See [Sending a welcome message to a new team member](~/bots/how-to/conversations/send-proactive-messages.md) for more details.</span></span>

<span data-ttu-id="351d3-152">Es posible que también desee enviar un mensaje personal a cada miembro del equipo cuando se agregue el bot.</span><span class="sxs-lookup"><span data-stu-id="351d3-152">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="351d3-153">Para ello, puede obtener la lista del equipo y enviar a cada usuario un mensaje directo.</span><span class="sxs-lookup"><span data-stu-id="351d3-153">To do this, you could get the team roster and send each user a direct message.</span></span>

<span data-ttu-id="351d3-154">No se recomienda enviar un mensaje en las siguientes situaciones:</span><span class="sxs-lookup"><span data-stu-id="351d3-154">It is not recommended to send a message in the following situations:</span></span>

* <span data-ttu-id="351d3-155">El equipo es grande (obviamente subjetivo, pero por ejemplo, más de 100 miembros).</span><span class="sxs-lookup"><span data-stu-id="351d3-155">The team is large (obviously subjective, but for example larger than 100 members).</span></span> <span data-ttu-id="351d3-156">El bot puede aparecer como "correo no deseado" y la persona que lo agregó puede recibir quejas a menos que comunique claramente la propuesta de valor de su bot a todos los usuarios que ven el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="351d3-156">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="351d3-157">El bot se menciona primero en un grupo o canal (en lugar de agregarse primero a un equipo)</span><span class="sxs-lookup"><span data-stu-id="351d3-157">Your bot is first mentioned in a group or channel (versus being first added to a team)</span></span>
* <span data-ttu-id="351d3-158">Se cambia el nombre de un grupo o canal</span><span class="sxs-lookup"><span data-stu-id="351d3-158">A group or channel is renamed</span></span>
* <span data-ttu-id="351d3-159">Un miembro del equipo se agrega a un grupo o un canal</span><span class="sxs-lookup"><span data-stu-id="351d3-159">A team member is added to a group or channel</span></span>

## <a name="learn-more"></a><span data-ttu-id="351d3-160">Más información</span><span class="sxs-lookup"><span data-stu-id="351d3-160">Learn more</span></span>

<span data-ttu-id="351d3-161">El bot tiene acceso a información adicional sobre el equipo o el chat de grupo en el que está instalado.</span><span class="sxs-lookup"><span data-stu-id="351d3-161">Your bot has access to additional information about the group chat or team it is installed in.</span></span> <span data-ttu-id="351d3-162">Consulte [obtener contexto de Microsoft Teams](~/bots/how-to/get-teams-context.md) para API adicionales disponibles para el bot.</span><span class="sxs-lookup"><span data-stu-id="351d3-162">See [get teams context](~/bots/how-to/get-teams-context.md) for additional APIs available for your bot.</span></span>

<span data-ttu-id="351d3-163">También hay eventos adicionales a los que puede suscribirse y responder su bot.</span><span class="sxs-lookup"><span data-stu-id="351d3-163">There are also additional events that your bot can subscribe and respond to.</span></span> <span data-ttu-id="351d3-164">Consulte [Subscribe to conversate Events](~/bots/how-to/conversations/subscribe-to-conversation-events.md) para obtener información sobre cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="351d3-164">See [subscribe to conversation events](~/bots/how-to/conversations/subscribe-to-conversation-events.md) to learn how.</span></span>

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

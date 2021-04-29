---
title: Conversaciones de canal y grupo con un bot
author: clearab
description: Cómo enviar, recibir y controlar mensajes de un bot en un chat de canal o grupo.
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 2d7eece1fc74781456024f6dcb9414fefbadb8f4
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075755"
---
# <a name="channel-and-group-chat-conversations-with-a-bot"></a><span data-ttu-id="d8764-103">Conversaciones de chat de canal y grupo con un bot</span><span class="sxs-lookup"><span data-stu-id="d8764-103">Channel and group chat conversations with a bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="d8764-104">Para instalar el bot de Microsoft Teams en un chat de grupo o equipo, agregue el `teams` ámbito o `groupchat` al bot.</span><span class="sxs-lookup"><span data-stu-id="d8764-104">To install the Microsoft Teams bot in a team or group chat, add the `teams` or `groupchat` scope to your bot.</span></span> <span data-ttu-id="d8764-105">Esto permite que todos los miembros de la conversación interactúen con el bot.</span><span class="sxs-lookup"><span data-stu-id="d8764-105">This allows all members of the conversation to interact with your bot.</span></span> <span data-ttu-id="d8764-106">Una vez instalado el bot, tiene acceso a metadatos sobre la conversación, como la lista de miembros de la conversación.</span><span class="sxs-lookup"><span data-stu-id="d8764-106">After the bot is installed, it has access to metadata about the conversation, such as the list of conversation members.</span></span> <span data-ttu-id="d8764-107">Además, cuando se instala en un equipo, el bot tiene acceso a detalles sobre ese equipo y a la lista completa de canales.</span><span class="sxs-lookup"><span data-stu-id="d8764-107">Also, when it is installed in a team, the bot has access to details about that team and the full list of channels.</span></span>

<span data-ttu-id="d8764-108">Los bots de un grupo o canal solo reciben mensajes cuando se mencionan `@botname` .</span><span class="sxs-lookup"><span data-stu-id="d8764-108">Bots in a group or channel only receive messages when they are mentioned `@botname`.</span></span> <span data-ttu-id="d8764-109">No reciben ningún otro mensaje enviado a la conversación.</span><span class="sxs-lookup"><span data-stu-id="d8764-109">They do not receive any other messages sent to the conversation.</span></span>

> [!NOTE]
> <span data-ttu-id="d8764-110">El bot debe ser `@mentioned` directamente.</span><span class="sxs-lookup"><span data-stu-id="d8764-110">The bot must be `@mentioned` directly.</span></span> <span data-ttu-id="d8764-111">El bot no recibe un mensaje cuando se menciona el equipo o el canal, o cuando alguien responde a un mensaje del bot sin @mentioning.</span><span class="sxs-lookup"><span data-stu-id="d8764-111">Your bot does not receive a message when the team or channel is mentioned, or when someone replies to a message from your bot without @mentioning it.</span></span>

## <a name="design-guidelines"></a><span data-ttu-id="d8764-112">Directrices de diseño</span><span class="sxs-lookup"><span data-stu-id="d8764-112">Design guidelines</span></span>

<span data-ttu-id="d8764-113">A diferencia de los chats personales, en los chats de grupo y canales, el bot debe proporcionar una introducción rápida.</span><span class="sxs-lookup"><span data-stu-id="d8764-113">Unlike personal chats, in group chats and channels, your bot must provide a quick introduction.</span></span> <span data-ttu-id="d8764-114">Debe seguir estas y más directrices de diseño de bots.</span><span class="sxs-lookup"><span data-stu-id="d8764-114">You must follow these and more bot design guidelines.</span></span> <span data-ttu-id="d8764-115">Para obtener más información sobre cómo diseñar bots en Teams, vea cómo diseñar conversaciones de [bots en canales y chats.](~/bots/design/bots.md)</span><span class="sxs-lookup"><span data-stu-id="d8764-115">For more information on how to design bots in Teams, see [how to design bot conversations in channels and chats](~/bots/design/bots.md).</span></span>

<span data-ttu-id="d8764-116">Ahora, puedes crear nuevos subprocesos de conversación y administrar fácilmente diferentes conversaciones en canales.</span><span class="sxs-lookup"><span data-stu-id="d8764-116">Now, you can create new conversation threads and easily manage different conversations in channels.</span></span>

## <a name="create-new-conversation-threads"></a><span data-ttu-id="d8764-117">Crear nuevos subprocesos de conversación</span><span class="sxs-lookup"><span data-stu-id="d8764-117">Create new conversation threads</span></span>

<span data-ttu-id="d8764-118">Cuando el bot está instalado en un equipo, debe crear un nuevo subproceso de conversación en lugar de responder a uno existente.</span><span class="sxs-lookup"><span data-stu-id="d8764-118">When your bot is installed in a team, you must create a new conversation thread rather than reply to an existing one.</span></span> <span data-ttu-id="d8764-119">A veces es difícil diferenciar entre dos conversaciones.</span><span class="sxs-lookup"><span data-stu-id="d8764-119">At times it is difficult to differentiate between two conversations.</span></span> <span data-ttu-id="d8764-120">Si la conversación se enhebra, es más fácil organizar y administrar diferentes conversaciones en canales.</span><span class="sxs-lookup"><span data-stu-id="d8764-120">If the conversation is threaded, it is easier to organize and manage different conversations in channels.</span></span> <span data-ttu-id="d8764-121">Se trata de una forma de [mensajería proactiva](~/bots/how-to/conversations/send-proactive-messages.md).</span><span class="sxs-lookup"><span data-stu-id="d8764-121">This is a form of [proactive messaging](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>

<span data-ttu-id="d8764-122">A continuación, puede recuperar menciones con el `entities` objeto y agregar menciones a los mensajes mediante el `Mention` objeto.</span><span class="sxs-lookup"><span data-stu-id="d8764-122">Next, you can retrieve mentions using the `entities` object and add mentions to your messages using the `Mention` object.</span></span>

## <a name="work-with-mentions"></a><span data-ttu-id="d8764-123">Trabajar con menciones</span><span class="sxs-lookup"><span data-stu-id="d8764-123">Work with mentions</span></span>

<span data-ttu-id="d8764-124">Cada mensaje al bot de un grupo o canal contiene @mention con su nombre en el texto del mensaje.</span><span class="sxs-lookup"><span data-stu-id="d8764-124">Every message to your bot from a group or channel contains an @mention with its name in the message text.</span></span> <span data-ttu-id="d8764-125">Asegúrese de que el análisis de mensajes controla @mention.</span><span class="sxs-lookup"><span data-stu-id="d8764-125">Ensure that your message parsing handles @mention.</span></span> <span data-ttu-id="d8764-126">El bot también puede recuperar otros usuarios mencionados en un mensaje y agregar menciones a los mensajes que envía.</span><span class="sxs-lookup"><span data-stu-id="d8764-126">Your bot can also retrieve other users mentioned in a message and add mentions to any messages it sends.</span></span>

<span data-ttu-id="d8764-127">También debe quitar el @mentions del contenido del mensaje que recibe el bot.</span><span class="sxs-lookup"><span data-stu-id="d8764-127">You must also strip out the @mentions from the content of the message your bot receives.</span></span>

### <a name="retrieve-mentions"></a><span data-ttu-id="d8764-128">Recuperar menciones</span><span class="sxs-lookup"><span data-stu-id="d8764-128">Retrieve mentions</span></span>

<span data-ttu-id="d8764-129">Las menciones se devuelven en el objeto en payload y contienen el identificador único del usuario y el nombre `entities` del usuario mencionado.</span><span class="sxs-lookup"><span data-stu-id="d8764-129">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and the name of the user mentioned.</span></span> <span data-ttu-id="d8764-130">El texto del mensaje también incluye la mención, como `<at>@John Smith<at>` .</span><span class="sxs-lookup"><span data-stu-id="d8764-130">The text of the message also includes the mention, such as `<at>@John Smith<at>`.</span></span> <span data-ttu-id="d8764-131">Sin embargo, no confíe en el texto del mensaje para recuperar información sobre el usuario.</span><span class="sxs-lookup"><span data-stu-id="d8764-131">However, do not rely on the text in the message to retrieve any information about the user.</span></span> <span data-ttu-id="d8764-132">Es posible que la persona que envía el mensaje lo modifique.</span><span class="sxs-lookup"><span data-stu-id="d8764-132">It is possible for the person sending the message to alter it.</span></span> <span data-ttu-id="d8764-133">Por lo tanto, use el `entities` objeto.</span><span class="sxs-lookup"><span data-stu-id="d8764-133">Therefore, use the `entities` object.</span></span>

<span data-ttu-id="d8764-134">Puede recuperar todas las menciones del mensaje llamando a la función en bot `GetMentions` Builder SDK, que devuelve una matriz de `Mention` objetos.</span><span class="sxs-lookup"><span data-stu-id="d8764-134">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK, which returns an array of `Mention` objects.</span></span>

<span data-ttu-id="d8764-135">El siguiente código muestra un ejemplo de recuperación de menciones:</span><span class="sxs-lookup"><span data-stu-id="d8764-135">The following code shows an example of retrieving mentions:</span></span>

# <a name="c"></a>[<span data-ttu-id="d8764-136">C#</span><span class="sxs-lookup"><span data-stu-id="d8764-136">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="d8764-137">TypeScript</span><span class="sxs-lookup"><span data-stu-id="d8764-137">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="d8764-138">JSON</span><span class="sxs-lookup"><span data-stu-id="d8764-138">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="d8764-139">Python</span><span class="sxs-lookup"><span data-stu-id="d8764-139">Python</span></span>](#tab/python)

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

### <a name="add-mentions-to-your-messages"></a><span data-ttu-id="d8764-140">Agregar menciones a los mensajes</span><span class="sxs-lookup"><span data-stu-id="d8764-140">Add mentions to your messages</span></span>

<span data-ttu-id="d8764-141">El bot puede mencionar a otros usuarios en mensajes publicados en canales.</span><span class="sxs-lookup"><span data-stu-id="d8764-141">Your bot can mention other users in messages posted into channels.</span></span>

<span data-ttu-id="d8764-142">El `Mention` objeto tiene dos propiedades que debe establecer con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d8764-142">The `Mention` object has two properties that you must set using the following:</span></span>

* <span data-ttu-id="d8764-143">Incluya <at>@username</at> en el texto del mensaje.</span><span class="sxs-lookup"><span data-stu-id="d8764-143">Include <at>@username</at> in the message text.</span></span>
* <span data-ttu-id="d8764-144">Incluya el objeto de mención dentro de la colección de entidades.</span><span class="sxs-lookup"><span data-stu-id="d8764-144">Include the mention object inside the entities collection.</span></span>

<span data-ttu-id="d8764-145">El SDK de Bot Framework proporciona métodos auxiliares y objetos para crear menciones.</span><span class="sxs-lookup"><span data-stu-id="d8764-145">The Bot Framework SDK provides helper methods and objects to create mentions.</span></span>

<span data-ttu-id="d8764-146">En el siguiente código se muestra un ejemplo de cómo agregar menciones a los mensajes:</span><span class="sxs-lookup"><span data-stu-id="d8764-146">The following code shows an example of adding mentions to your messages:</span></span>

# <a name="c"></a>[<span data-ttu-id="d8764-147">C#</span><span class="sxs-lookup"><span data-stu-id="d8764-147">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="d8764-148">TypeScript</span><span class="sxs-lookup"><span data-stu-id="d8764-148">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="d8764-149">JSON</span><span class="sxs-lookup"><span data-stu-id="d8764-149">JSON</span></span>](#tab/json)

<span data-ttu-id="d8764-150">El `text` campo del objeto de la `entities` matriz debe coincidir con una parte del campo de `text` mensaje.</span><span class="sxs-lookup"><span data-stu-id="d8764-150">The `text` field in the object in the `entities` array must match a portion of the message `text` field.</span></span> <span data-ttu-id="d8764-151">Si no lo hace, se omite la mención.</span><span class="sxs-lookup"><span data-stu-id="d8764-151">If it does not, the mention is ignored.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="d8764-152">Python</span><span class="sxs-lookup"><span data-stu-id="d8764-152">Python</span></span>](#tab/python)

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

<span data-ttu-id="d8764-153">Ahora puedes enviar un mensaje de introducción cuando el bot se instala por primera vez o se agrega a un grupo o equipo.</span><span class="sxs-lookup"><span data-stu-id="d8764-153">Now you can send an introduction message when your bot is first installed or added to a group or team.</span></span>

## <a name="send-a-message-on-installation"></a><span data-ttu-id="d8764-154">Enviar un mensaje durante la instalación</span><span class="sxs-lookup"><span data-stu-id="d8764-154">Send a message on installation</span></span>

<span data-ttu-id="d8764-155">Cuando el bot se agrega por primera vez al grupo o equipo, se debe enviar un mensaje de introducción.</span><span class="sxs-lookup"><span data-stu-id="d8764-155">When your bot is first added to the group or team, an introduction message must be sent.</span></span> <span data-ttu-id="d8764-156">El mensaje debe proporcionar una breve descripción de las características del bot y cómo usarlas.</span><span class="sxs-lookup"><span data-stu-id="d8764-156">The message must provide a brief description of the bot's features and how to use them.</span></span> <span data-ttu-id="d8764-157">Debe suscribirse al `conversationUpdate` evento con `teamMemberAdded` eventType.</span><span class="sxs-lookup"><span data-stu-id="d8764-157">You must subscribe to the `conversationUpdate` event with the `teamMemberAdded` eventType.</span></span>  <span data-ttu-id="d8764-158">El evento se envía cuando se agrega un nuevo miembro del equipo.</span><span class="sxs-lookup"><span data-stu-id="d8764-158">The event is sent when any new team member is added.</span></span> <span data-ttu-id="d8764-159">Compruebe si el nuevo miembro agregado es el bot.</span><span class="sxs-lookup"><span data-stu-id="d8764-159">Check if the new member added is the bot.</span></span> <span data-ttu-id="d8764-160">Para obtener más información, vea [sending a welcome message to a new team member](~/bots/how-to/conversations/send-proactive-messages.md).</span><span class="sxs-lookup"><span data-stu-id="d8764-160">For more information, see [sending a welcome message to a new team member](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>

<span data-ttu-id="d8764-161">Envíe un mensaje personal a cada miembro del equipo cuando se agrega el bot.</span><span class="sxs-lookup"><span data-stu-id="d8764-161">Send a personal message to each team member when the bot is added.</span></span> <span data-ttu-id="d8764-162">Para ello, obtenga la lista de equipos y envíe un mensaje directo a cada usuario.</span><span class="sxs-lookup"><span data-stu-id="d8764-162">To do this, get the team roster and send each user a direct message.</span></span>

<span data-ttu-id="d8764-163">No envíe un mensaje en los siguientes casos:</span><span class="sxs-lookup"><span data-stu-id="d8764-163">Do not send a message in the following cases:</span></span>

* <span data-ttu-id="d8764-164">El equipo es grande, por ejemplo, más de 100 miembros.</span><span class="sxs-lookup"><span data-stu-id="d8764-164">The team is large, for example, larger than 100 members.</span></span> <span data-ttu-id="d8764-165">El bot se puede ver como correo no deseado y la persona que lo agregó puede recibir quejas.</span><span class="sxs-lookup"><span data-stu-id="d8764-165">Your bot can be seen as spam and the person who added it can get complaints.</span></span> <span data-ttu-id="d8764-166">Debe comunicar claramente la propuesta de valor del bot a todos los usuarios que ve el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="d8764-166">You must clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="d8764-167">El bot se menciona por primera vez en un grupo o canal en lugar de agregarse primero a un equipo.</span><span class="sxs-lookup"><span data-stu-id="d8764-167">Your bot is first mentioned in a group or channel instead of being first added to a team.</span></span>
* <span data-ttu-id="d8764-168">Se cambia el nombre de un grupo o canal.</span><span class="sxs-lookup"><span data-stu-id="d8764-168">A group or channel is renamed.</span></span>
* <span data-ttu-id="d8764-169">Un miembro del equipo se agrega a un grupo o canal.</span><span class="sxs-lookup"><span data-stu-id="d8764-169">A team member is added to a group or channel.</span></span>

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## <a name="see-also"></a><span data-ttu-id="d8764-170">Consulte también</span><span class="sxs-lookup"><span data-stu-id="d8764-170">See also</span></span>

[<span data-ttu-id="d8764-171">Obtener contexto de Teams</span><span class="sxs-lookup"><span data-stu-id="d8764-171">Get Teams context</span></span>](~/bots/how-to/get-teams-context.md)

## <a name="next-step"></a><span data-ttu-id="d8764-172">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="d8764-172">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d8764-173">Suscribirse a eventos de conversación</span><span class="sxs-lookup"><span data-stu-id="d8764-173">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

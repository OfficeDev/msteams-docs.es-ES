---
title: Conversaciones de canal y grupo con un bot
author: clearab
description: Cómo enviar, recibir y controlar mensajes de un bot en un chat de canal o grupo.
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: ef5cf8464fa0e93d5ea3840003a2b0c04a4a5ef5
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631002"
---
# <a name="channel-and-group-chat-conversations-with-a-bot"></a><span data-ttu-id="b6949-103">Conversaciones de chat de canal y grupo con un bot</span><span class="sxs-lookup"><span data-stu-id="b6949-103">Channel and group chat conversations with a bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="b6949-104">Para instalar el Microsoft Teams bot en un chat de grupo o equipo, agregue el `teams` ámbito o `groupchat` al bot.</span><span class="sxs-lookup"><span data-stu-id="b6949-104">To install the Microsoft Teams bot in a team or group chat, add the `teams` or `groupchat` scope to your bot.</span></span> <span data-ttu-id="b6949-105">Esto permite que todos los miembros de la conversación interactúen con el bot.</span><span class="sxs-lookup"><span data-stu-id="b6949-105">This allows all members of the conversation to interact with your bot.</span></span> <span data-ttu-id="b6949-106">Una vez instalado el bot, tiene acceso a metadatos sobre la conversación, como la lista de miembros de la conversación.</span><span class="sxs-lookup"><span data-stu-id="b6949-106">After the bot is installed, it has access to metadata about the conversation, such as the list of conversation members.</span></span> <span data-ttu-id="b6949-107">Además, cuando se instala en un equipo, el bot tiene acceso a detalles sobre ese equipo y a la lista completa de canales.</span><span class="sxs-lookup"><span data-stu-id="b6949-107">Also, when it is installed in a team, the bot has access to details about that team and the full list of channels.</span></span>

<span data-ttu-id="b6949-108">Los bots de un grupo o canal solo reciben mensajes cuando se mencionan @botname.</span><span class="sxs-lookup"><span data-stu-id="b6949-108">Bots in a group or channel only receive messages when they are mentioned @botname.</span></span> <span data-ttu-id="b6949-109">No reciben ningún otro mensaje enviado a la conversación.</span><span class="sxs-lookup"><span data-stu-id="b6949-109">They do not receive any other messages sent to the conversation.</span></span> <span data-ttu-id="b6949-110">El bot debe ser @mencionado directamente.</span><span class="sxs-lookup"><span data-stu-id="b6949-110">The bot must be @mentioned directly.</span></span> <span data-ttu-id="b6949-111">El bot no recibe un mensaje cuando se menciona el equipo o el canal, o cuando alguien responde a un mensaje del bot sin @mentioning.</span><span class="sxs-lookup"><span data-stu-id="b6949-111">Your bot does not receive a message when the team or channel is mentioned, or when someone replies to a message from your bot without @mentioning it.</span></span>

> [!NOTE]
> <span data-ttu-id="b6949-112">Esta característica está disponible actualmente solo en [la versión preliminar del desarrollador](../../../resources/dev-preview/developer-preview-intro.md) público.</span><span class="sxs-lookup"><span data-stu-id="b6949-112">This feature is currently available in [public developer preview](../../../resources/dev-preview/developer-preview-intro.md) only.</span></span>
>
> <span data-ttu-id="b6949-113">Con el consentimiento específico de recursos (RSC), los bots pueden recibir todos los mensajes de canal en los equipos en los que está instalado sin que se @mentioned.</span><span class="sxs-lookup"><span data-stu-id="b6949-113">Using resource-specific consent (RSC), bots can receive all channel messages in teams that it is installed in without being @mentioned.</span></span> <span data-ttu-id="b6949-114">Para obtener más información, vea [recibir todos los mensajes de canal con RSC](channel-messages-with-rsc.md).</span><span class="sxs-lookup"><span data-stu-id="b6949-114">For more information, see [receive all channel messages with RSC](channel-messages-with-rsc.md).</span></span>

## <a name="design-guidelines"></a><span data-ttu-id="b6949-115">Directrices de diseño</span><span class="sxs-lookup"><span data-stu-id="b6949-115">Design guidelines</span></span>

<span data-ttu-id="b6949-116">A diferencia de los chats personales, en los chats de grupo y canales, el bot debe proporcionar una introducción rápida.</span><span class="sxs-lookup"><span data-stu-id="b6949-116">Unlike personal chats, in group chats and channels, your bot must provide a quick introduction.</span></span> <span data-ttu-id="b6949-117">Debe seguir estas y más directrices de diseño de bots.</span><span class="sxs-lookup"><span data-stu-id="b6949-117">You must follow these and more bot design guidelines.</span></span> <span data-ttu-id="b6949-118">Para obtener más información sobre cómo diseñar bots en Teams, vea cómo diseñar conversaciones de [bot en canales y chats.](~/bots/design/bots.md)</span><span class="sxs-lookup"><span data-stu-id="b6949-118">For more information on how to design bots in Teams, see [how to design bot conversations in channels and chats](~/bots/design/bots.md).</span></span>

<span data-ttu-id="b6949-119">Ahora, puedes crear nuevos subprocesos de conversación y administrar fácilmente diferentes conversaciones en canales.</span><span class="sxs-lookup"><span data-stu-id="b6949-119">Now, you can create new conversation threads and easily manage different conversations in channels.</span></span>

## <a name="create-new-conversation-threads"></a><span data-ttu-id="b6949-120">Crear nuevos subprocesos de conversación</span><span class="sxs-lookup"><span data-stu-id="b6949-120">Create new conversation threads</span></span>

<span data-ttu-id="b6949-121">Cuando el bot está instalado en un equipo, debe crear un nuevo subproceso de conversación en lugar de responder a uno existente.</span><span class="sxs-lookup"><span data-stu-id="b6949-121">When your bot is installed in a team, you must create a new conversation thread rather than reply to an existing one.</span></span> <span data-ttu-id="b6949-122">A veces es difícil diferenciar entre dos conversaciones.</span><span class="sxs-lookup"><span data-stu-id="b6949-122">At times it is difficult to differentiate between two conversations.</span></span> <span data-ttu-id="b6949-123">Si la conversación se enhebra, es más fácil organizar y administrar diferentes conversaciones en canales.</span><span class="sxs-lookup"><span data-stu-id="b6949-123">If the conversation is threaded, it is easier to organize and manage different conversations in channels.</span></span> <span data-ttu-id="b6949-124">Se trata de una forma de [mensajería proactiva](~/bots/how-to/conversations/send-proactive-messages.md).</span><span class="sxs-lookup"><span data-stu-id="b6949-124">This is a form of [proactive messaging](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>

<span data-ttu-id="b6949-125">A continuación, puede recuperar menciones con el `entities` objeto y agregar menciones a los mensajes mediante el `Mention` objeto.</span><span class="sxs-lookup"><span data-stu-id="b6949-125">Next, you can retrieve mentions using the `entities` object and add mentions to your messages using the `Mention` object.</span></span>

## <a name="work-with-mentions"></a><span data-ttu-id="b6949-126">Trabajar con menciones</span><span class="sxs-lookup"><span data-stu-id="b6949-126">Work with mentions</span></span>

<span data-ttu-id="b6949-127">Cada mensaje al bot de un grupo o canal contiene @mention con su nombre en el texto del mensaje.</span><span class="sxs-lookup"><span data-stu-id="b6949-127">Every message to your bot from a group or channel contains an @mention with its name in the message text.</span></span> <span data-ttu-id="b6949-128">El bot también puede recuperar otros usuarios mencionados en un mensaje y agregar menciones a los mensajes que envía.</span><span class="sxs-lookup"><span data-stu-id="b6949-128">Your bot can also retrieve other users mentioned in a message and add mentions to any messages it sends.</span></span>

<span data-ttu-id="b6949-129">También debe quitar el @mentions del contenido del mensaje que recibe el bot.</span><span class="sxs-lookup"><span data-stu-id="b6949-129">You must also strip out the @mentions from the content of the message your bot receives.</span></span>

### <a name="retrieve-mentions"></a><span data-ttu-id="b6949-130">Recuperar menciones</span><span class="sxs-lookup"><span data-stu-id="b6949-130">Retrieve mentions</span></span>

<span data-ttu-id="b6949-131">Las menciones se devuelven en el objeto en payload y contienen el identificador único del usuario y el nombre `entities` del usuario mencionado.</span><span class="sxs-lookup"><span data-stu-id="b6949-131">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and the name of the user mentioned.</span></span> <span data-ttu-id="b6949-132">El texto del mensaje también incluye la mención, como `<at>@John Smith<at>` .</span><span class="sxs-lookup"><span data-stu-id="b6949-132">The text of the message also includes the mention, such as `<at>@John Smith<at>`.</span></span> <span data-ttu-id="b6949-133">Sin embargo, no confíe en el texto del mensaje para recuperar información sobre el usuario.</span><span class="sxs-lookup"><span data-stu-id="b6949-133">However, do not rely on the text in the message to retrieve any information about the user.</span></span> <span data-ttu-id="b6949-134">Es posible que la persona que envía el mensaje lo modifique.</span><span class="sxs-lookup"><span data-stu-id="b6949-134">It is possible for the person sending the message to alter it.</span></span> <span data-ttu-id="b6949-135">Por lo tanto, use el `entities` objeto.</span><span class="sxs-lookup"><span data-stu-id="b6949-135">Therefore, use the `entities` object.</span></span>

<span data-ttu-id="b6949-136">Puede recuperar todas las menciones del mensaje llamando a la función en bot `GetMentions` Builder SDK, que devuelve una matriz de `Mention` objetos.</span><span class="sxs-lookup"><span data-stu-id="b6949-136">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK, which returns an array of `Mention` objects.</span></span>

<span data-ttu-id="b6949-137">El siguiente código muestra un ejemplo de recuperación de menciones:</span><span class="sxs-lookup"><span data-stu-id="b6949-137">The following code shows an example of retrieving mentions:</span></span>

# <a name="c"></a>[<span data-ttu-id="b6949-138">C#</span><span class="sxs-lookup"><span data-stu-id="b6949-138">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="b6949-139">TypeScript</span><span class="sxs-lookup"><span data-stu-id="b6949-139">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="b6949-140">JSON</span><span class="sxs-lookup"><span data-stu-id="b6949-140">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="b6949-141">Python</span><span class="sxs-lookup"><span data-stu-id="b6949-141">Python</span></span>](#tab/python)

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

### <a name="add-mentions-to-your-messages"></a><span data-ttu-id="b6949-142">Agregar menciones a los mensajes</span><span class="sxs-lookup"><span data-stu-id="b6949-142">Add mentions to your messages</span></span>

<span data-ttu-id="b6949-143">El bot puede mencionar a otros usuarios en mensajes publicados en canales.</span><span class="sxs-lookup"><span data-stu-id="b6949-143">Your bot can mention other users in messages posted into channels.</span></span>

<span data-ttu-id="b6949-144">El `Mention` objeto tiene dos propiedades que debe establecer con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b6949-144">The `Mention` object has two properties that you must set using the following:</span></span>

* <span data-ttu-id="b6949-145">Incluya <at>@username</at> en el texto del mensaje.</span><span class="sxs-lookup"><span data-stu-id="b6949-145">Include <at>@username</at> in the message text.</span></span>
* <span data-ttu-id="b6949-146">Incluya el objeto de mención dentro de la colección de entidades.</span><span class="sxs-lookup"><span data-stu-id="b6949-146">Include the mention object inside the entities collection.</span></span>

<span data-ttu-id="b6949-147">El SDK de Bot Framework proporciona métodos auxiliares y objetos para crear menciones.</span><span class="sxs-lookup"><span data-stu-id="b6949-147">The Bot Framework SDK provides helper methods and objects to create mentions.</span></span>

<span data-ttu-id="b6949-148">En el siguiente código se muestra un ejemplo de cómo agregar menciones a los mensajes:</span><span class="sxs-lookup"><span data-stu-id="b6949-148">The following code shows an example of adding mentions to your messages:</span></span>

# <a name="c"></a>[<span data-ttu-id="b6949-149">C#</span><span class="sxs-lookup"><span data-stu-id="b6949-149">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="b6949-150">TypeScript</span><span class="sxs-lookup"><span data-stu-id="b6949-150">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="b6949-151">JSON</span><span class="sxs-lookup"><span data-stu-id="b6949-151">JSON</span></span>](#tab/json)

<span data-ttu-id="b6949-152">El `text` campo del objeto de la `entities` matriz debe coincidir con una parte del campo de `text` mensaje.</span><span class="sxs-lookup"><span data-stu-id="b6949-152">The `text` field in the object in the `entities` array must match a portion of the message `text` field.</span></span> <span data-ttu-id="b6949-153">Si no lo hace, se omite la mención.</span><span class="sxs-lookup"><span data-stu-id="b6949-153">If it does not, the mention is ignored.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="b6949-154">Python</span><span class="sxs-lookup"><span data-stu-id="b6949-154">Python</span></span>](#tab/python)

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

<span data-ttu-id="b6949-155">Ahora puedes enviar un mensaje de introducción cuando el bot se instala por primera vez o se agrega a un grupo o equipo.</span><span class="sxs-lookup"><span data-stu-id="b6949-155">Now you can send an introduction message when your bot is first installed or added to a group or team.</span></span>

## <a name="send-a-message-on-installation"></a><span data-ttu-id="b6949-156">Enviar un mensaje durante la instalación</span><span class="sxs-lookup"><span data-stu-id="b6949-156">Send a message on installation</span></span>

<span data-ttu-id="b6949-157">Cuando el bot se agrega por primera vez al grupo o equipo, se debe enviar un mensaje de introducción.</span><span class="sxs-lookup"><span data-stu-id="b6949-157">When your bot is first added to the group or team, an introduction message must be sent.</span></span> <span data-ttu-id="b6949-158">El mensaje debe proporcionar una breve descripción de las características del bot y cómo usarlas.</span><span class="sxs-lookup"><span data-stu-id="b6949-158">The message must provide a brief description of the bot's features and how to use them.</span></span> <span data-ttu-id="b6949-159">Debe suscribirse al `conversationUpdate` evento con `teamMemberAdded` eventType.</span><span class="sxs-lookup"><span data-stu-id="b6949-159">You must subscribe to the `conversationUpdate` event with the `teamMemberAdded` eventType.</span></span>  <span data-ttu-id="b6949-160">El evento se envía cuando se agrega un nuevo miembro del equipo.</span><span class="sxs-lookup"><span data-stu-id="b6949-160">The event is sent when any new team member is added.</span></span> <span data-ttu-id="b6949-161">Compruebe si el nuevo miembro agregado es el bot.</span><span class="sxs-lookup"><span data-stu-id="b6949-161">Check if the new member added is the bot.</span></span> <span data-ttu-id="b6949-162">Para obtener más información, vea [sending a welcome message to a new team member](~/bots/how-to/conversations/send-proactive-messages.md).</span><span class="sxs-lookup"><span data-stu-id="b6949-162">For more information, see [sending a welcome message to a new team member](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>

<span data-ttu-id="b6949-163">Envíe un mensaje personal a cada miembro del equipo cuando se agrega el bot.</span><span class="sxs-lookup"><span data-stu-id="b6949-163">Send a personal message to each team member when the bot is added.</span></span> <span data-ttu-id="b6949-164">Para ello, obtenga la lista de equipos y envíe un mensaje directo a cada usuario.</span><span class="sxs-lookup"><span data-stu-id="b6949-164">To do this, get the team roster and send each user a direct message.</span></span>

<span data-ttu-id="b6949-165">No envíe un mensaje en los siguientes casos:</span><span class="sxs-lookup"><span data-stu-id="b6949-165">Do not send a message in the following cases:</span></span>

* <span data-ttu-id="b6949-166">El equipo es grande, por ejemplo, más de 100 miembros.</span><span class="sxs-lookup"><span data-stu-id="b6949-166">The team is large, for example, larger than 100 members.</span></span> <span data-ttu-id="b6949-167">El bot se puede ver como correo no deseado y la persona que lo agregó puede recibir quejas.</span><span class="sxs-lookup"><span data-stu-id="b6949-167">Your bot can be seen as spam and the person who added it can get complaints.</span></span> <span data-ttu-id="b6949-168">Debe comunicar claramente la propuesta de valor del bot a todos los usuarios que ve el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="b6949-168">You must clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="b6949-169">El bot se menciona por primera vez en un grupo o canal en lugar de agregarse primero a un equipo.</span><span class="sxs-lookup"><span data-stu-id="b6949-169">Your bot is first mentioned in a group or channel instead of being first added to a team.</span></span>
* <span data-ttu-id="b6949-170">Se cambia el nombre de un grupo o canal.</span><span class="sxs-lookup"><span data-stu-id="b6949-170">A group or channel is renamed.</span></span>
* <span data-ttu-id="b6949-171">Un miembro del equipo se agrega a un grupo o canal.</span><span class="sxs-lookup"><span data-stu-id="b6949-171">A team member is added to a group or channel.</span></span>

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## <a name="see-also"></a><span data-ttu-id="b6949-172">Consulte también</span><span class="sxs-lookup"><span data-stu-id="b6949-172">See also</span></span>

[<span data-ttu-id="b6949-173">Obtener Teams contexto</span><span class="sxs-lookup"><span data-stu-id="b6949-173">Get Teams context</span></span>](~/bots/how-to/get-teams-context.md)

## <a name="next-step"></a><span data-ttu-id="b6949-174">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="b6949-174">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b6949-175">Suscribirse a eventos de conversación</span><span class="sxs-lookup"><span data-stu-id="b6949-175">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

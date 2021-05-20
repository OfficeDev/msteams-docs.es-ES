---
title: Conversaciones de chat de canal y grupo con bots
description: Describe el escenario de extremo a extremo de tener una conversación con un bot en un canal en Microsoft Teams
keywords: escenarios de equipos canaliza bot de conversación
localization_priority: Normal
ms.topic: conceptual
ms.date: 06/25/2019
ms.openlocfilehash: e254302271cf101638c897e1a1952d302705d6a4
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566799"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="21153-104">Conversaciones de chat de canal y grupo con un bot de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="21153-104">Channel and Group chat conversations with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="21153-105">Microsoft Teams permite a los usuarios llevar bots a sus conversaciones de chat de canal o grupo.</span><span class="sxs-lookup"><span data-stu-id="21153-105">Microsoft Teams allows users to bring bots into their channel or group chat conversations.</span></span> <span data-ttu-id="21153-106">Al agregar un bot a un equipo o chatear, todos los usuarios de la conversación pueden aprovechar la funcionalidad del bot directamente en la conversación.</span><span class="sxs-lookup"><span data-stu-id="21153-106">By adding a bot to a team or chat, all users of the conversation can take advantage of the bot functionality right in the conversation.</span></span> <span data-ttu-id="21153-107">También puede acceder a Teams funcionalidad específica del bot, como consultar información del equipo y @mentioning usuarios.</span><span class="sxs-lookup"><span data-stu-id="21153-107">You can also access Teams-specific functionality within your bot like querying team information and @mentioning users.</span></span>

<span data-ttu-id="21153-108">Chatear en canales y chats de grupo difieren del chat personal en el que el usuario necesita @mention el bot.</span><span class="sxs-lookup"><span data-stu-id="21153-108">Chat in channels and group chats differ from personal chat in that the user needs to @mention the bot.</span></span> <span data-ttu-id="21153-109">Si un bot se usa en varios ámbitos como personal, groupchat o canal, debe detectar de qué ámbito proceden los mensajes de bot y procesarlos en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="21153-109">If a bot is used in multiple scopes such as personal, groupchat, or channel, you need to detect what scope the bot messages came from, and process them accordingly.</span></span>

## <a name="designing-a-great-bot-for-channels-or-groups"></a><span data-ttu-id="21153-110">Diseñar un gran bot para canales o grupos</span><span class="sxs-lookup"><span data-stu-id="21153-110">Designing a great bot for channels or groups</span></span>

<span data-ttu-id="21153-111">Bots añadido a un equipo se convierten en otro miembro del equipo y se pueden @mentioned como parte de la conversación.</span><span class="sxs-lookup"><span data-stu-id="21153-111">Bots added to a team become another team member and can be @mentioned as part of the conversation.</span></span> <span data-ttu-id="21153-112">De hecho, los bots solo reciben mensajes cuando se @mentioned, por lo que otras conversaciones en el canal no se envían al bot.</span><span class="sxs-lookup"><span data-stu-id="21153-112">In fact, bots only receive messages when they are @mentioned, so other conversations on the channel are not sent to the bot.</span></span>

<span data-ttu-id="21153-113">Un bot de un grupo o canal debe proporcionar información relevante y adecuada para todos los miembros.</span><span class="sxs-lookup"><span data-stu-id="21153-113">A bot in a group or channel should provide information relevant and appropriate for all members.</span></span> <span data-ttu-id="21153-114">Si bien su bot ciertamente puede proporcionar cualquier información relevante para la experiencia, tenga en cuenta que las conversaciones con él son visibles para todos.</span><span class="sxs-lookup"><span data-stu-id="21153-114">While your bot can certainly provide any information relevant to the experience, keep in mind conversations with it are visible to everyone.</span></span> <span data-ttu-id="21153-115">Por lo tanto, un gran bot en un grupo o canal debe agregar valor a todos los usuarios, y ciertamente no compartir información inadvertidamente más adecuada a una conversación uno a uno.</span><span class="sxs-lookup"><span data-stu-id="21153-115">Therefore, a great bot in a group or channel should add value to all users, and certainly not inadvertently share information more appropriate to a one-to-one conversation.</span></span>

<span data-ttu-id="21153-116">Su bot, tal como es, puede ser completamente relevante en todos los ámbitos sin requerir trabajo adicional.</span><span class="sxs-lookup"><span data-stu-id="21153-116">Your bot, just as it is, may be entirely relevant in all scopes without requiring additional work.</span></span> <span data-ttu-id="21153-117">En Microsoft Teams no hay ninguna expectativa de que el bot funcione en todos los ámbitos, pero debe asegurarse de que el bot proporciona valor de usuario en los ámbitos que elija admitir.</span><span class="sxs-lookup"><span data-stu-id="21153-117">In Microsoft Teams there is no expectation that your bot function in all scopes, but you should ensure that your bot provides user value in whichever scope(s) you choose to support.</span></span> <span data-ttu-id="21153-118">Para obtener más información sobre los ámbitos, consulte [Aplicaciones en Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).</span><span class="sxs-lookup"><span data-stu-id="21153-118">For more information on scopes, see [Apps in Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="21153-119">El desarrollo de un bot que funciona en grupos o canales utiliza gran parte de la misma funcionalidad que las conversaciones personales.</span><span class="sxs-lookup"><span data-stu-id="21153-119">Developing a bot that works in groups or channels uses much of the same functionality as personal conversations.</span></span> <span data-ttu-id="21153-120">Los eventos y datos adicionales de la carga proporcionan información de grupo y canal Teams.</span><span class="sxs-lookup"><span data-stu-id="21153-120">Additional events and data in the payload provide Teams group and channel information.</span></span> <span data-ttu-id="21153-121">Estas diferencias, así como las diferencias clave en la funcionalidad común se describen en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="21153-121">Those differences, as well as key differences in common functionality are described in the following sections.</span></span>

### <a name="creating-messages"></a><span data-ttu-id="21153-122">Creación de mensajes</span><span class="sxs-lookup"><span data-stu-id="21153-122">Creating messages</span></span>

<span data-ttu-id="21153-123">Para obtener más información sobre los bots que crean mensajes en canales, consulte [Mensajería proactiva para bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)y, específicamente, [Creación de una conversación de canal.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)</span><span class="sxs-lookup"><span data-stu-id="21153-123">For more information on bots creating messages in channels see [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md), and specifically [Creating a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).</span></span>

### <a name="receiving-messages"></a><span data-ttu-id="21153-124">Recepción de mensajes</span><span class="sxs-lookup"><span data-stu-id="21153-124">Receiving messages</span></span>

<span data-ttu-id="21153-125">Para un bot en un grupo o canal, además del [esquema de mensaje normal,](https://docs.botframework.com/core-concepts/reference/#activity)el bot también recibe las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="21153-125">For a bot in a group or channel, in addition to the [regular message schema](https://docs.botframework.com/core-concepts/reference/#activity), your bot also receives the following properties:</span></span>

* <span data-ttu-id="21153-126">`channelData`Consulte [Teams datos del canal](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data).</span><span class="sxs-lookup"><span data-stu-id="21153-126">`channelData` See [Teams channel data](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data).</span></span> <span data-ttu-id="21153-127">En un chat de grupo, contiene información específica de ese chat.</span><span class="sxs-lookup"><span data-stu-id="21153-127">In a group chat, contains information specific to that chat.</span></span>
* <span data-ttu-id="21153-128">`conversation.id` El ID de cadena de respuesta, que consta de ID de canal más el ID del primer mensaje de la cadena de respuesta.</span><span class="sxs-lookup"><span data-stu-id="21153-128">`conversation.id` The reply chain ID, consisting of channel ID plus the ID of the first message in the reply chain.</span></span>
* <span data-ttu-id="21153-129">`conversation.isGroup` Es `true` para mensajes de bot en canales o chats de grupo.</span><span class="sxs-lookup"><span data-stu-id="21153-129">`conversation.isGroup` Is `true` for bot messages in channels or group chats.</span></span>
* <span data-ttu-id="21153-130">`conversation.conversationType` O `groupChat` `channel` bien .</span><span class="sxs-lookup"><span data-stu-id="21153-130">`conversation.conversationType` Either `groupChat` or `channel`.</span></span>
* <span data-ttu-id="21153-131">`entities` Puede contener una o más menciones.</span><span class="sxs-lookup"><span data-stu-id="21153-131">`entities` Can contain one or more mentions.</span></span> <span data-ttu-id="21153-132">Para obtener más información, consulte [Menciones](#-mentions).</span><span class="sxs-lookup"><span data-stu-id="21153-132">For more information, see [Mentions](#-mentions).</span></span>

### <a name="replying-to-messages"></a><span data-ttu-id="21153-133">Responder a los mensajes</span><span class="sxs-lookup"><span data-stu-id="21153-133">Replying to messages</span></span>

<span data-ttu-id="21153-134">Para responder a un mensaje existente, llame a [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) .NET o [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) en Node.js.</span><span class="sxs-lookup"><span data-stu-id="21153-134">To reply to an existing message, call [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) in .NET or [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) in Node.js.</span></span> <span data-ttu-id="21153-135">El SDK de Bot Builder controla todos los detalles.</span><span class="sxs-lookup"><span data-stu-id="21153-135">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="21153-136">Si decide usar la API de REST, también puede llamar al [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="21153-136">If you choose to use the REST API, you can also call the [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) endpoint.</span></span>

<span data-ttu-id="21153-137">En un canal, responder a un mensaje se muestra como respuesta a la cadena de respuesta de inicio.</span><span class="sxs-lookup"><span data-stu-id="21153-137">In a channel, replying to a message shows as a reply to the initiating reply chain.</span></span> <span data-ttu-id="21153-138">Contiene `conversation.id` el canal y el identificador de mensaje de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="21153-138">The `conversation.id` contains the channel and the top level message ID.</span></span> <span data-ttu-id="21153-139">Aunque Bot Framework se encarga de los detalles, puede almacenar en caché eso `conversation.id` para futuras respuestas a ese subproceso de conversación según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="21153-139">Although the Bot Framework takes care of the details, you can cache that `conversation.id` for future replies to that conversation thread as needed.</span></span>

### <a name="best-practice-welcome-messages-in-teams"></a><span data-ttu-id="21153-140">Mejores prácticas: Mensajes de bienvenida en Teams</span><span class="sxs-lookup"><span data-stu-id="21153-140">Best practice: Welcome messages in Teams</span></span>

<span data-ttu-id="21153-141">Cuando el bot se agrega por primera vez al grupo o equipo, generalmente es útil enviar un mensaje de bienvenida introduciendo el bot a todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="21153-141">When your bot is first added to the group or team, it is generally useful to send a welcome message introducing the bot to all users.</span></span> <span data-ttu-id="21153-142">El mensaje de bienvenida debe proporcionar una descripción de la funcionalidad del bot y las ventajas del usuario.</span><span class="sxs-lookup"><span data-stu-id="21153-142">The welcome message should provide a description of the bot’s functionality and user benefits.</span></span> <span data-ttu-id="21153-143">Idealmente, el mensaje también debe incluir comandos para que el usuario interactúe con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="21153-143">Ideally the message should also include commands for the user to interact with the app.</span></span> <span data-ttu-id="21153-144">Para ello, asegúrese de que el bot responde al `conversationUpdate` mensaje, con el `teamsAddMembers` eventType en el `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="21153-144">To do this, ensure that your bot responds to the `conversationUpdate` message, with the `teamsAddMembers` eventType in the `channelData` object.</span></span> <span data-ttu-id="21153-145">Asegúrese de que el `memberAdded` identificador es el propio ID de aplicación del bot, porque el mismo evento se envía cuando se agrega un usuario a un equipo.</span><span class="sxs-lookup"><span data-stu-id="21153-145">Be sure that the `memberAdded` ID is the bot's App ID itself, because the same event is sent when a user is added to a team.</span></span> <span data-ttu-id="21153-146">Consulte [Miembro del equipo o adición de bots](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="21153-146">See [Team member or bot addition](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) for more details.</span></span>

<span data-ttu-id="21153-147">También es posible que desee enviar un mensaje personal a cada miembro del equipo cuando se agrega el bot.</span><span class="sxs-lookup"><span data-stu-id="21153-147">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="21153-148">Para ello, puede [obtener la lista de equipos](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) y enviar a cada usuario un mensaje [directo.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)</span><span class="sxs-lookup"><span data-stu-id="21153-148">To do this, you could [fetch the team roster](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) and send each user a [direct message](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span></span>

<span data-ttu-id="21153-149">Le recomendamos que el bot *no* envíe un mensaje de bienvenida en las siguientes situaciones:</span><span class="sxs-lookup"><span data-stu-id="21153-149">We recommend that your bot *not* send a welcome message in the following situations:</span></span>

* <span data-ttu-id="21153-150">El equipo es grande (obviamente subjetivo, por ejemplo, más de 100 miembros).</span><span class="sxs-lookup"><span data-stu-id="21153-150">The team is big (obviously subjective, for example, more than 100 members).</span></span> <span data-ttu-id="21153-151">Su bot puede ser visto como 'spam' y la persona que lo agregó puede recibir quejas a menos que comunique claramente la propuesta de valor de su bot a todos los que ven el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="21153-151">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="21153-152">El bot se menciona primero en un grupo o canal, en lugar de agregarse primero a un equipo.</span><span class="sxs-lookup"><span data-stu-id="21153-152">Your bot is first mentioned in a group or channel, versus being first added to a team.</span></span>
* <span data-ttu-id="21153-153">Se cambia el nombre de un grupo o canal.</span><span class="sxs-lookup"><span data-stu-id="21153-153">A group or channel is renamed.</span></span>
* <span data-ttu-id="21153-154">Un miembro del equipo se agrega a un grupo o canal.</span><span class="sxs-lookup"><span data-stu-id="21153-154">A team member is added to a group or channel.</span></span>

## <a name="-mentions"></a><span data-ttu-id="21153-155">@ Menciones</span><span class="sxs-lookup"><span data-stu-id="21153-155">@ Mentions</span></span>

<span data-ttu-id="21153-156">Dado que los bots de un grupo o canal responden solo cuando se mencionan ("@_botname")_ en un mensaje, cada mensaje recibido por un bot en un canal de grupo contiene su propio nombre y debe asegurarse de que el análisis de mensajes controla eso.</span><span class="sxs-lookup"><span data-stu-id="21153-156">Because bots in a group or channel respond only when they are mentioned ("@_botname_") in a message, every message received by a bot in a group channel contains its own name, and you must ensure your message parsing handles that.</span></span> <span data-ttu-id="21153-157">Además, los bots pueden analizar a otros usuarios mencionados y mencionar a los usuarios como parte de sus mensajes.</span><span class="sxs-lookup"><span data-stu-id="21153-157">In addition, bots can parse out other users mentioned and mention users as part of their messages.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="21153-158">Recuperación de menciones</span><span class="sxs-lookup"><span data-stu-id="21153-158">Retrieving mentions</span></span>

<span data-ttu-id="21153-159">Las menciones se devuelven en el `entities` objeto en la carga útil y contienen tanto el identificador único del usuario como, en la mayoría de los casos, el nombre del usuario mencionado.</span><span class="sxs-lookup"><span data-stu-id="21153-159">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="21153-160">Puede recuperar todas las menciones del mensaje llamando a la `GetMentions` función en el SDK de Bot Builder para .NET, que devuelve una matriz de `Mentioned` objetos.</span><span class="sxs-lookup"><span data-stu-id="21153-160">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK for .NET, which returns an array of `Mentioned` objects.</span></span>

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="21153-161">Código de ejemplo de .NET: compruebe y elimine @bot mención</span><span class="sxs-lookup"><span data-stu-id="21153-161">.NET example code: Check for and strip @bot mention</span></span>

```csharp
Mention[] m = sourceMessage.GetMentions();
var messageText = sourceMessage.Text;

for (int i = 0;i < m.Length;i++)
{
    if (m[i].Mentioned.Id == sourceMessage.Recipient.Id)
    {
        //Bot is in the @mention list.
        //The below example will strip the bot name out of the message, so you can parse it as if it wasn't included. Note that the Text object will contain the full bot name, if applicable.
        if (m[i].Text != null)
            messageText = messageText.Replace(m[i].Text, "");
    }
}
```

> [!NOTE]
> <span data-ttu-id="21153-162">También puede utilizar la función de extensión Teams `GetTextWithoutMentions` , que elimina todas las menciones, incluido el bot.</span><span class="sxs-lookup"><span data-stu-id="21153-162">You can also use the Teams extension function `GetTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="21153-163">Node.js código de ejemplo: Compruebe si hay una mención @bot</span><span class="sxs-lookup"><span data-stu-id="21153-163">Node.js example code: Check for and strip @bot mention</span></span>

```javascript
var text = message.text;
if (message.entities) {
    message.entities
        .filter(entity => ((entity.type === "mention") && (entity.mentioned.id.toLowerCase() === botId)))
        .forEach(entity => {
            text = text.replace(entity.text, "");
        });
    text = text.trim();
}
```

<span data-ttu-id="21153-164">También puede utilizar la función de extensión Teams `getTextWithoutMentions` , que elimina todas las menciones, incluido el bot.</span><span class="sxs-lookup"><span data-stu-id="21153-164">You can also use the Teams extension function `getTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="21153-165">Construcción de menciones</span><span class="sxs-lookup"><span data-stu-id="21153-165">Constructing mentions</span></span>

<span data-ttu-id="21153-166">El bot puede mencionar a otros usuarios en los mensajes publicados en canales.</span><span class="sxs-lookup"><span data-stu-id="21153-166">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="21153-167">Para ello, el mensaje debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="21153-167">To do this, your message must do the following:</span></span>

* <span data-ttu-id="21153-168">Incluir `<at>@username</at>` en el texto del mensaje.</span><span class="sxs-lookup"><span data-stu-id="21153-168">Include `<at>@username</at>` in the message text.</span></span>
* <span data-ttu-id="21153-169">Incluya el `mention` objeto dentro de la colección entities.</span><span class="sxs-lookup"><span data-stu-id="21153-169">Include the `mention` object inside the entities collection.</span></span>

#### <a name="net-example"></a><span data-ttu-id="21153-170">Ejemplo de .NET</span><span class="sxs-lookup"><span data-stu-id="21153-170">.NET example</span></span>

<span data-ttu-id="21153-171">En este ejemplo se usa el paquete [NuGet Microsoft.Bot.Connector.Teams.](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)</span><span class="sxs-lookup"><span data-stu-id="21153-171">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a><span data-ttu-id="21153-172">Node.js ejemplo</span><span class="sxs-lookup"><span data-stu-id="21153-172">Node.js example</span></span>

```javascript
// User to mention
var toMention: builder.IIdentity = {
    name: 'John Doe',
    id: userId
};

// Create a message and add mention to it
var msg = new teams.TeamsMessage(session).text(teams.TeamsMessage.getTenantId(session.message));
var mentionedMsg = msg.addMentionToText(toMention);

// Post the message
var generalMessage = mentionedMsg.routeReplyToGeneralChannel();
session.send(generalMessage);
```

#### <a name="example-outgoing-message-with-user-mentioned"></a><span data-ttu-id="21153-173">Ejemplo: Mensaje saliente con el usuario mencionado</span><span class="sxs-lookup"><span data-stu-id="21153-173">Example: Outgoing message with user mentioned</span></span>

```json
{
    "type": "message", 
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "28:9e52142b-5e5e-4d7b-bb3e- e82dcf620000",
        "name": "SchemaTestBot"
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

## <a name="accessing-groupchat-or-channel-scope"></a><span data-ttu-id="21153-174">Acceso a groupChat o alcance de canal</span><span class="sxs-lookup"><span data-stu-id="21153-174">Accessing groupChat or channel scope</span></span>

<span data-ttu-id="21153-175">El bot puede hacer algo más que enviar y recibir mensajes en grupos y equipos.</span><span class="sxs-lookup"><span data-stu-id="21153-175">Your bot can do more than send and receive messages in groups and teams.</span></span> <span data-ttu-id="21153-176">Por ejemplo, también puede obtener la lista de miembros, incluida la información de su perfil, así como la lista de canales.</span><span class="sxs-lookup"><span data-stu-id="21153-176">For instance, it can also fetch the list of members, including their profile information, as well as the list of channels.</span></span> <span data-ttu-id="21153-177">Para obtener más información, consulte [Obtener contexto para el bot de Microsoft Teams](~/resources/bot-v3/bots-context.md).</span><span class="sxs-lookup"><span data-stu-id="21153-177">For more information, see [Get context for your Microsoft Teams bot](~/resources/bot-v3/bots-context.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="21153-178">Vea también</span><span class="sxs-lookup"><span data-stu-id="21153-178">See also</span></span>

[<span data-ttu-id="21153-179">Muestras de Bot Framework</span><span class="sxs-lookup"><span data-stu-id="21153-179">Bot Framework samples</span></span>](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)

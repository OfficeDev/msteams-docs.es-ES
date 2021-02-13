---
title: Conversaciones de chat de canal y grupo con bots
description: Describe el escenario completo de tener una conversación con un bot en un canal de Microsoft Teams
keywords: bot de conversación de canales de escenarios de teams
ms.date: 06/25/2019
ms.openlocfilehash: e556eb006257a83ddf93adb62f79857201d6a9ad
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231634"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="bcc35-104">Conversaciones de chat de canal y grupo con un bot de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="bcc35-104">Channel and Group chat conversations with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="bcc35-105">Microsoft Teams permite a los usuarios traer bots a sus conversaciones de chat en grupo o canal.</span><span class="sxs-lookup"><span data-stu-id="bcc35-105">Microsoft Teams allows users to bring bots into their channel or group chat conversations.</span></span> <span data-ttu-id="bcc35-106">Al agregar un bot a un equipo o chat, todos los usuarios de la conversación pueden aprovechar la funcionalidad del bot directamente en la conversación.</span><span class="sxs-lookup"><span data-stu-id="bcc35-106">By adding a bot to a team or chat, all users of the conversation can take advantage of the bot functionality right in the conversation.</span></span> <span data-ttu-id="bcc35-107">También puede acceder a la funcionalidad específica de Teams dentro de su bot, como consultar la información del equipo y @mentioning usuarios.</span><span class="sxs-lookup"><span data-stu-id="bcc35-107">You can also access Teams-specific functionality within your bot like querying team information and @mentioning users.</span></span>

<span data-ttu-id="bcc35-108">El chat en canales y chats de grupo difiere del chat personal en que el usuario necesita @mention el bot.</span><span class="sxs-lookup"><span data-stu-id="bcc35-108">Chat in channels and group chats differ from personal chat in that the user needs to @mention the bot.</span></span> <span data-ttu-id="bcc35-109">Si un bot se usa en varios ámbitos (personal, groupchat o channel), deberá detectar de qué ámbito procesó los mensajes del bot y procesarlos en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="bcc35-109">If a bot is used in multiple scopes (personal, groupchat or channel) you will need to detect what scope the bot messages came from, and process them accordingly.</span></span>

## <a name="designing-a-great-bot-for-channels-or-groups"></a><span data-ttu-id="bcc35-110">Diseño de un bot excelente para canales o grupos</span><span class="sxs-lookup"><span data-stu-id="bcc35-110">Designing a great bot for channels or groups</span></span>

<span data-ttu-id="bcc35-111">Los bots agregados a un equipo se convierten en otro miembro del equipo y @mentioned como parte de la conversación.</span><span class="sxs-lookup"><span data-stu-id="bcc35-111">Bots added to a team become another team member and can be @mentioned as part of the conversation.</span></span> <span data-ttu-id="bcc35-112">De hecho, los bots solo reciben mensajes cuando @mentioned, por lo que otras conversaciones en el canal no se envían al bot.</span><span class="sxs-lookup"><span data-stu-id="bcc35-112">In fact, bots only receive messages when they are @mentioned, so other conversations on the channel are not sent to the bot.</span></span>

<span data-ttu-id="bcc35-113">Un bot de un grupo o canal debe proporcionar información relevante y adecuada para todos los miembros.</span><span class="sxs-lookup"><span data-stu-id="bcc35-113">A bot in a group or channel should provide information relevant and appropriate for all members.</span></span> <span data-ttu-id="bcc35-114">Aunque el bot puede proporcionar ciertamente cualquier información relevante para la experiencia, tenga en cuenta que las conversaciones con él son visibles para todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="bcc35-114">While your bot can certainly provide any information relevant to the experience, keep in mind conversations with it are visible to everyone.</span></span> <span data-ttu-id="bcc35-115">Por lo tanto, un excelente bot en un grupo o canal debe agregar valor a todos los usuarios y, desde luego, no compartir accidentalmente información más adecuada para una conversación uno a uno.</span><span class="sxs-lookup"><span data-stu-id="bcc35-115">Therefore, a great bot in a group or channel should add value to all users, and certainly not inadvertently share information more appropriate to a one-to-one conversation.</span></span>

<span data-ttu-id="bcc35-116">El bot, tal como es, puede ser totalmente relevante en todos los ámbitos sin necesidad de trabajo adicional.</span><span class="sxs-lookup"><span data-stu-id="bcc35-116">Your bot, just as it is, may be entirely relevant in all scopes without requiring additional work.</span></span> <span data-ttu-id="bcc35-117">En Microsoft Teams no hay ninguna expectativa de que el bot funcione en todos los ámbitos, pero debe asegurarse de que el bot proporciona valor de usuario en los ámbitos que elija admitir.</span><span class="sxs-lookup"><span data-stu-id="bcc35-117">In Microsoft Teams there is no expectation that your bot function in all scopes, but you should ensure that your bot provides user value in whichever scope(s) you choose to support.</span></span> <span data-ttu-id="bcc35-118">Para obtener más información sobre los ámbitos, vea [Aplicaciones en Microsoft Teams.](~/concepts/build-and-test/app-studio-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bcc35-118">For more information on scopes, see [Apps in Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="bcc35-119">El desarrollo de un bot que funciona en grupos o canales usa gran parte de la misma funcionalidad que las conversaciones personales.</span><span class="sxs-lookup"><span data-stu-id="bcc35-119">Developing a bot that works in groups or channels uses much of the same functionality as personal conversations.</span></span> <span data-ttu-id="bcc35-120">Los eventos y datos adicionales de la carga proporcionan información de grupo y canal de Teams.</span><span class="sxs-lookup"><span data-stu-id="bcc35-120">Additional events and data in the payload provide Teams group and channel information.</span></span> <span data-ttu-id="bcc35-121">Estas diferencias, así como las diferencias clave en la funcionalidad común se describen en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="bcc35-121">Those differences, as well as key differences in common functionality are described in the following sections.</span></span>

### <a name="creating-messages"></a><span data-ttu-id="bcc35-122">Creación de mensajes</span><span class="sxs-lookup"><span data-stu-id="bcc35-122">Creating messages</span></span>

<span data-ttu-id="bcc35-123">Para obtener más información sobre los bots que crean mensajes en [canales,](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)vea Mensajería proactiva para bots y, específicamente, [crear una conversación de canal.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)</span><span class="sxs-lookup"><span data-stu-id="bcc35-123">For more information on bots creating messages in channels see [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md), and specifically [Creating a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).</span></span>

### <a name="receiving-messages"></a><span data-ttu-id="bcc35-124">Recibir mensajes</span><span class="sxs-lookup"><span data-stu-id="bcc35-124">Receiving messages</span></span>

<span data-ttu-id="bcc35-125">Para un bot en un grupo o canal, además del esquema de mensajes [normal,](https://docs.botframework.com/core-concepts/reference/#activity)el bot también recibe las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="bcc35-125">For a bot in a group or channel, in addition to the [regular message schema](https://docs.botframework.com/core-concepts/reference/#activity), your bot also receives the following properties:</span></span>

* <span data-ttu-id="bcc35-126">`channelData`Vea los [datos del canal de Teams.](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data)</span><span class="sxs-lookup"><span data-stu-id="bcc35-126">`channelData` See [Teams channel data](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data).</span></span> <span data-ttu-id="bcc35-127">En un chat de grupo, contiene información específica de ese chat.</span><span class="sxs-lookup"><span data-stu-id="bcc35-127">In a group chat, contains information specific to that chat.</span></span>
* <span data-ttu-id="bcc35-128">`conversation.id` El identificador de cadena de respuesta, que consta del identificador de canal más el identificador del primer mensaje de la cadena de respuesta</span><span class="sxs-lookup"><span data-stu-id="bcc35-128">`conversation.id` The reply chain ID, consisting of channel ID plus the ID of the first message in the reply chain</span></span>
* <span data-ttu-id="bcc35-129">`conversation.isGroup` Es `true` para mensajes de bot en canales o chats de grupo</span><span class="sxs-lookup"><span data-stu-id="bcc35-129">`conversation.isGroup` Is `true` for bot messages in channels or group chats</span></span>
* <span data-ttu-id="bcc35-130">`conversation.conversationType` Cualquiera `groupChat` de las dos `channel`</span><span class="sxs-lookup"><span data-stu-id="bcc35-130">`conversation.conversationType` Either `groupChat` or `channel`</span></span>
* <span data-ttu-id="bcc35-131">`entities`Puede contener una o más menciones (vea [Menciones)](#-mentions)</span><span class="sxs-lookup"><span data-stu-id="bcc35-131">`entities` Can contain one or more mentions (see [Mentions](#-mentions))</span></span>

### <a name="replying-to-messages"></a><span data-ttu-id="bcc35-132">Responder a mensajes</span><span class="sxs-lookup"><span data-stu-id="bcc35-132">Replying to messages</span></span>

<span data-ttu-id="bcc35-133">Para responder a un mensaje existente, llame [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) en .NET o [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) en Node.js.</span><span class="sxs-lookup"><span data-stu-id="bcc35-133">To reply to an existing message, call [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) in .NET or [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) in Node.js.</span></span> <span data-ttu-id="bcc35-134">El SDK de Bot Builder controla todos los detalles.</span><span class="sxs-lookup"><span data-stu-id="bcc35-134">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="bcc35-135">Si decide usar la API de REST, también puede llamar al punto de [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) conexión.</span><span class="sxs-lookup"><span data-stu-id="bcc35-135">If you choose to use the REST API, you can also call the [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) endpoint.</span></span>

<span data-ttu-id="bcc35-136">En un canal, la respuesta a un mensaje se muestra como una respuesta a la cadena de respuesta de inicio.</span><span class="sxs-lookup"><span data-stu-id="bcc35-136">In a channel, replying to a message shows as a reply to the initiating reply chain.</span></span> <span data-ttu-id="bcc35-137">Contiene `conversation.id` el canal y el identificador de mensaje de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="bcc35-137">The `conversation.id` contains the channel and the top level message ID.</span></span> <span data-ttu-id="bcc35-138">Aunque Bot Framework se encarga de los detalles, puede almacenarlo en caché para futuras respuestas a ese hilo `conversation.id` de conversación según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="bcc35-138">Although the Bot Framework takes care of the details, you can cache that `conversation.id` for future replies to that conversation thread as needed.</span></span>

### <a name="best-practice-welcome-messages-in-teams"></a><span data-ttu-id="bcc35-139">Procedimiento recomendado: Mensajes de bienvenida en Teams</span><span class="sxs-lookup"><span data-stu-id="bcc35-139">Best practice: Welcome messages in Teams</span></span>

<span data-ttu-id="bcc35-140">Cuando el bot se agrega por primera vez al grupo o equipo, generalmente resulta útil enviar un mensaje de bienvenida que presenta el bot a todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="bcc35-140">When your bot is first added to the group or team, it is generally useful to send a welcome message introducing the bot to all users.</span></span> <span data-ttu-id="bcc35-141">El mensaje de bienvenida debe proporcionar una descripción de la funcionalidad del bot y las ventajas del usuario.</span><span class="sxs-lookup"><span data-stu-id="bcc35-141">The welcome message should provide a description of the bot’s functionality and user benefits.</span></span> <span data-ttu-id="bcc35-142">Lo ideal es que el mensaje también incluya comandos para que el usuario interactúe con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bcc35-142">Ideally the message should also include commands for the user to interact with the app.</span></span> <span data-ttu-id="bcc35-143">Para ello, asegúrese de que el bot responde al `conversationUpdate` mensaje, con `teamsAddMembers` el eventType en el `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="bcc35-143">To do this, ensure that your bot responds to the `conversationUpdate` message, with the `teamsAddMembers` eventType in the `channelData` object.</span></span> <span data-ttu-id="bcc35-144">Asegúrese de que el identificador es el id. de aplicación del bot, ya que se envía el mismo evento cuando se agrega un usuario `memberAdded` a un equipo.</span><span class="sxs-lookup"><span data-stu-id="bcc35-144">Be sure that the `memberAdded` ID is the bot's App ID itself, because the same event is sent when a user is added to a team.</span></span> <span data-ttu-id="bcc35-145">Vea [la adición de bots o miembros](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) del equipo para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="bcc35-145">See [Team member or bot addition](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) for more details.</span></span>

<span data-ttu-id="bcc35-146">Es posible que también desee enviar un mensaje personal a cada miembro del equipo cuando se agrega el bot.</span><span class="sxs-lookup"><span data-stu-id="bcc35-146">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="bcc35-147">Para ello, puede capturar [la lista](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) del equipo y enviar un mensaje directo a [cada usuario.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)</span><span class="sxs-lookup"><span data-stu-id="bcc35-147">To do this, you could [fetch the team roster](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) and send each user a [direct message](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span></span>

<span data-ttu-id="bcc35-148">Se recomienda que el bot *no envíe* un mensaje de bienvenida en las siguientes situaciones:</span><span class="sxs-lookup"><span data-stu-id="bcc35-148">We recommend that your bot *not* send a welcome message in the following situations:</span></span>

* <span data-ttu-id="bcc35-149">El equipo es grande (obviamente subjetivo, pero, por ejemplo, más de 100 miembros).</span><span class="sxs-lookup"><span data-stu-id="bcc35-149">The team is large (obviously subjective, but for example larger than 100 members).</span></span> <span data-ttu-id="bcc35-150">Es posible que el bot se vea como "spammy" y la persona que lo agregó puede recibir quejas a menos que comunique claramente la propuesta de valor del bot a todos los usuarios que vean el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="bcc35-150">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="bcc35-151">El bot se menciona por primera vez en un grupo o canal (frente a que se agrega por primera vez a un equipo)</span><span class="sxs-lookup"><span data-stu-id="bcc35-151">Your bot is first mentioned in a group or channel (versus being first added to a team)</span></span>
* <span data-ttu-id="bcc35-152">Se cambia el nombre de un grupo o canal</span><span class="sxs-lookup"><span data-stu-id="bcc35-152">A group or channel is renamed</span></span>
* <span data-ttu-id="bcc35-153">Se agrega un miembro del equipo a un grupo o canal</span><span class="sxs-lookup"><span data-stu-id="bcc35-153">A team member is added to a group or channel</span></span>

## <a name="-mentions"></a><span data-ttu-id="bcc35-154">@ Menciones</span><span class="sxs-lookup"><span data-stu-id="bcc35-154">@ Mentions</span></span>

<span data-ttu-id="bcc35-155">Dado que los bots de un grupo o canal responden solo cuando se mencionan ("@_botname_") en un mensaje, cada mensaje recibido por un bot en un canal de grupo contiene su propio nombre y debe asegurarse de que el análisis de mensajes lo controla.</span><span class="sxs-lookup"><span data-stu-id="bcc35-155">Because bots in a group or channel respond only when they are mentioned ("@_botname_") in a message, every message received by a bot in a group channel contains its own name, and you must ensure your message parsing handles that.</span></span> <span data-ttu-id="bcc35-156">Además, los bots pueden analizar otros usuarios mencionados y mencionar a los usuarios como parte de sus mensajes.</span><span class="sxs-lookup"><span data-stu-id="bcc35-156">In addition, bots can parse out other users mentioned and mention users as part of their messages.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="bcc35-157">Recuperar menciones</span><span class="sxs-lookup"><span data-stu-id="bcc35-157">Retrieving mentions</span></span>

<span data-ttu-id="bcc35-158">Las menciones se devuelven en el objeto en carga y contienen el identificador único del usuario y, en la mayoría de los casos, el nombre `entities` del usuario mencionado.</span><span class="sxs-lookup"><span data-stu-id="bcc35-158">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="bcc35-159">Puede recuperar todas las menciones del mensaje llamando a la función en bot Builder SDK para .NET, que devuelve una `GetMentions` matriz de `Mentioned` objetos.</span><span class="sxs-lookup"><span data-stu-id="bcc35-159">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK for .NET, which returns an array of `Mentioned` objects.</span></span>

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="bcc35-160">Código de ejemplo de .NET: comprobar y quitar @bot mención</span><span class="sxs-lookup"><span data-stu-id="bcc35-160">.NET example code: Check for and strip @bot mention</span></span>

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
> <span data-ttu-id="bcc35-161">También puede usar la función de extensión de Teams, que elimina todas `GetTextWithoutMentions` las menciones, incluido el bot.</span><span class="sxs-lookup"><span data-stu-id="bcc35-161">You can also use the Teams extension function `GetTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="bcc35-162">Node.js código de ejemplo: Comprobar y quitar @bot mención</span><span class="sxs-lookup"><span data-stu-id="bcc35-162">Node.js example code: Check for and strip @bot mention</span></span>

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

<span data-ttu-id="bcc35-163">También puede usar la función de extensión de Teams, que elimina todas `getTextWithoutMentions` las menciones, incluido el bot.</span><span class="sxs-lookup"><span data-stu-id="bcc35-163">You can also use the Teams extension function `getTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="bcc35-164">Construcción de menciones</span><span class="sxs-lookup"><span data-stu-id="bcc35-164">Constructing mentions</span></span>

<span data-ttu-id="bcc35-165">El bot puede mencionar a otros usuarios en mensajes publicados en canales.</span><span class="sxs-lookup"><span data-stu-id="bcc35-165">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="bcc35-166">Para ello, el mensaje debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="bcc35-166">To do this, your message must do the following:</span></span>

* <span data-ttu-id="bcc35-167">Incluir `<at>@username</at>` en el texto del mensaje</span><span class="sxs-lookup"><span data-stu-id="bcc35-167">Include `<at>@username</at>` in the message text</span></span>
* <span data-ttu-id="bcc35-168">Incluir el `mention` objeto dentro de la colección de entidades</span><span class="sxs-lookup"><span data-stu-id="bcc35-168">Include the `mention` object inside the entities collection</span></span>

#### <a name="net-example"></a><span data-ttu-id="bcc35-169">Ejemplo de .NET</span><span class="sxs-lookup"><span data-stu-id="bcc35-169">.NET example</span></span>

<span data-ttu-id="bcc35-170">En este ejemplo se usa [el paquete NuGet Microsoft.Bot.Connector.Teams.](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)</span><span class="sxs-lookup"><span data-stu-id="bcc35-170">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a><span data-ttu-id="bcc35-171">Node.js ejemplo</span><span class="sxs-lookup"><span data-stu-id="bcc35-171">Node.js example</span></span>

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

#### <a name="example-outgoing-message-with-user-mentioned"></a><span data-ttu-id="bcc35-172">Ejemplo: mensaje saliente con el usuario mencionado</span><span class="sxs-lookup"><span data-stu-id="bcc35-172">Example: Outgoing message with user mentioned</span></span>

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

## <a name="accessing-groupchat-or-channel-scope"></a><span data-ttu-id="bcc35-173">Acceso a groupChat o ámbito de canal</span><span class="sxs-lookup"><span data-stu-id="bcc35-173">Accessing groupChat or channel scope</span></span>

<span data-ttu-id="bcc35-174">El bot puede hacer más que enviar y recibir mensajes en grupos y equipos.</span><span class="sxs-lookup"><span data-stu-id="bcc35-174">Your bot can do more than send and receive messages in groups and teams.</span></span> <span data-ttu-id="bcc35-175">Por ejemplo, también puede capturar la lista de miembros, incluida su información de perfil, así como la lista de canales.</span><span class="sxs-lookup"><span data-stu-id="bcc35-175">For instance, it can also fetch the list of members, including their profile information, as well as the list of channels.</span></span> <span data-ttu-id="bcc35-176">Consulte [Obtener contexto para el bot de Microsoft Teams](~/resources/bot-v3/bots-context.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="bcc35-176">See [Get context for your Microsoft Teams bot](~/resources/bot-v3/bots-context.md) to learn more.</span></span>

<span data-ttu-id="bcc35-177">*Vea también ejemplos* [de Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)</span><span class="sxs-lookup"><span data-stu-id="bcc35-177">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

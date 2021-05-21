---
title: Conversaciones de chat de canal y grupo con bots
description: Describe el escenario completo de tener una conversación con un bot en un canal de Microsoft Teams
keywords: escenarios de teams canaliza bot de conversación
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
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="b7842-104">Conversaciones de chat de canal y grupo con un bot de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b7842-104">Channel and Group chat conversations with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="b7842-105">Microsoft Teams permite a los usuarios llevar bots a sus conversaciones de chat de grupo o canal.</span><span class="sxs-lookup"><span data-stu-id="b7842-105">Microsoft Teams allows users to bring bots into their channel or group chat conversations.</span></span> <span data-ttu-id="b7842-106">Al agregar un bot a un equipo o chat, todos los usuarios de la conversación pueden aprovechar la funcionalidad del bot directamente en la conversación.</span><span class="sxs-lookup"><span data-stu-id="b7842-106">By adding a bot to a team or chat, all users of the conversation can take advantage of the bot functionality right in the conversation.</span></span> <span data-ttu-id="b7842-107">También puede obtener acceso a Teams funcionalidad específica del bot, como consultar la información del equipo y @mentioning usuarios.</span><span class="sxs-lookup"><span data-stu-id="b7842-107">You can also access Teams-specific functionality within your bot like querying team information and @mentioning users.</span></span>

<span data-ttu-id="b7842-108">El chat en canales y chats de grupo difiere del chat personal en que el usuario necesita @mention el bot.</span><span class="sxs-lookup"><span data-stu-id="b7842-108">Chat in channels and group chats differ from personal chat in that the user needs to @mention the bot.</span></span> <span data-ttu-id="b7842-109">Si un bot se usa en varios ámbitos, como personal, groupchat o channel, debe detectar el ámbito del que provenían los mensajes del bot y procesarlos en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="b7842-109">If a bot is used in multiple scopes such as personal, groupchat, or channel, you need to detect what scope the bot messages came from, and process them accordingly.</span></span>

## <a name="designing-a-great-bot-for-channels-or-groups"></a><span data-ttu-id="b7842-110">Diseño de un excelente bot para canales o grupos</span><span class="sxs-lookup"><span data-stu-id="b7842-110">Designing a great bot for channels or groups</span></span>

<span data-ttu-id="b7842-111">Los bots agregados a un equipo se convierten en otro miembro del equipo y @mentioned como parte de la conversación.</span><span class="sxs-lookup"><span data-stu-id="b7842-111">Bots added to a team become another team member and can be @mentioned as part of the conversation.</span></span> <span data-ttu-id="b7842-112">De hecho, los bots solo reciben mensajes cuando @mentioned, por lo que otras conversaciones en el canal no se envían al bot.</span><span class="sxs-lookup"><span data-stu-id="b7842-112">In fact, bots only receive messages when they are @mentioned, so other conversations on the channel are not sent to the bot.</span></span>

<span data-ttu-id="b7842-113">Un bot de un grupo o canal debe proporcionar información relevante y apropiada para todos los miembros.</span><span class="sxs-lookup"><span data-stu-id="b7842-113">A bot in a group or channel should provide information relevant and appropriate for all members.</span></span> <span data-ttu-id="b7842-114">Aunque el bot ciertamente puede proporcionar cualquier información relevante para la experiencia, tenga en cuenta que las conversaciones con él son visibles para todos.</span><span class="sxs-lookup"><span data-stu-id="b7842-114">While your bot can certainly provide any information relevant to the experience, keep in mind conversations with it are visible to everyone.</span></span> <span data-ttu-id="b7842-115">Por lo tanto, un gran bot en un grupo o canal debe agregar valor a todos los usuarios y, desde luego, no compartir accidentalmente información más adecuada para una conversación uno a uno.</span><span class="sxs-lookup"><span data-stu-id="b7842-115">Therefore, a great bot in a group or channel should add value to all users, and certainly not inadvertently share information more appropriate to a one-to-one conversation.</span></span>

<span data-ttu-id="b7842-116">El bot, tal como está, puede ser totalmente relevante en todos los ámbitos sin necesidad de trabajo adicional.</span><span class="sxs-lookup"><span data-stu-id="b7842-116">Your bot, just as it is, may be entirely relevant in all scopes without requiring additional work.</span></span> <span data-ttu-id="b7842-117">En Microsoft Teams no hay ninguna expectativa de que el bot funcione en todos los ámbitos, pero debes asegurarte de que el bot proporciona valor de usuario en cualquiera de los ámbitos que elijas admitir.</span><span class="sxs-lookup"><span data-stu-id="b7842-117">In Microsoft Teams there is no expectation that your bot function in all scopes, but you should ensure that your bot provides user value in whichever scope(s) you choose to support.</span></span> <span data-ttu-id="b7842-118">Para obtener más información sobre los ámbitos, vea [Aplicaciones en Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b7842-118">For more information on scopes, see [Apps in Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="b7842-119">El desarrollo de un bot que funciona en grupos o canales usa gran parte de la misma funcionalidad que las conversaciones personales.</span><span class="sxs-lookup"><span data-stu-id="b7842-119">Developing a bot that works in groups or channels uses much of the same functionality as personal conversations.</span></span> <span data-ttu-id="b7842-120">Los eventos y datos adicionales de la carga proporcionan Teams de grupo y canal.</span><span class="sxs-lookup"><span data-stu-id="b7842-120">Additional events and data in the payload provide Teams group and channel information.</span></span> <span data-ttu-id="b7842-121">Estas diferencias, así como las diferencias clave en la funcionalidad común se describen en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="b7842-121">Those differences, as well as key differences in common functionality are described in the following sections.</span></span>

### <a name="creating-messages"></a><span data-ttu-id="b7842-122">Creación de mensajes</span><span class="sxs-lookup"><span data-stu-id="b7842-122">Creating messages</span></span>

<span data-ttu-id="b7842-123">Para obtener más información sobre los bots que crean mensajes en [canales,](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)vea Proactive messaging for bots y specifically [Creating a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).</span><span class="sxs-lookup"><span data-stu-id="b7842-123">For more information on bots creating messages in channels see [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md), and specifically [Creating a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).</span></span>

### <a name="receiving-messages"></a><span data-ttu-id="b7842-124">Recepción de mensajes</span><span class="sxs-lookup"><span data-stu-id="b7842-124">Receiving messages</span></span>

<span data-ttu-id="b7842-125">Para un bot de un grupo o canal, además del esquema de mensaje [normal,](https://docs.botframework.com/core-concepts/reference/#activity)el bot también recibe las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="b7842-125">For a bot in a group or channel, in addition to the [regular message schema](https://docs.botframework.com/core-concepts/reference/#activity), your bot also receives the following properties:</span></span>

* <span data-ttu-id="b7842-126">`channelData`Vea [Teams datos del canal](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data).</span><span class="sxs-lookup"><span data-stu-id="b7842-126">`channelData` See [Teams channel data](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data).</span></span> <span data-ttu-id="b7842-127">En un chat de grupo, contiene información específica de ese chat.</span><span class="sxs-lookup"><span data-stu-id="b7842-127">In a group chat, contains information specific to that chat.</span></span>
* <span data-ttu-id="b7842-128">`conversation.id` El identificador de cadena de respuesta, que consta de identificador de canal más el identificador del primer mensaje de la cadena de respuesta.</span><span class="sxs-lookup"><span data-stu-id="b7842-128">`conversation.id` The reply chain ID, consisting of channel ID plus the ID of the first message in the reply chain.</span></span>
* <span data-ttu-id="b7842-129">`conversation.isGroup` Es `true` para mensajes de bot en canales o chats de grupo.</span><span class="sxs-lookup"><span data-stu-id="b7842-129">`conversation.isGroup` Is `true` for bot messages in channels or group chats.</span></span>
* <span data-ttu-id="b7842-130">`conversation.conversationType` O `groupChat` `channel` .</span><span class="sxs-lookup"><span data-stu-id="b7842-130">`conversation.conversationType` Either `groupChat` or `channel`.</span></span>
* <span data-ttu-id="b7842-131">`entities` Puede contener una o más menciones.</span><span class="sxs-lookup"><span data-stu-id="b7842-131">`entities` Can contain one or more mentions.</span></span> <span data-ttu-id="b7842-132">Para obtener más información, vea [Menciones](#-mentions).</span><span class="sxs-lookup"><span data-stu-id="b7842-132">For more information, see [Mentions](#-mentions).</span></span>

### <a name="replying-to-messages"></a><span data-ttu-id="b7842-133">Responder a mensajes</span><span class="sxs-lookup"><span data-stu-id="b7842-133">Replying to messages</span></span>

<span data-ttu-id="b7842-134">Para responder a un mensaje existente, llame [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) en .NET o [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) en Node.js.</span><span class="sxs-lookup"><span data-stu-id="b7842-134">To reply to an existing message, call [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) in .NET or [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) in Node.js.</span></span> <span data-ttu-id="b7842-135">El SDK de Bot Builder controla todos los detalles.</span><span class="sxs-lookup"><span data-stu-id="b7842-135">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="b7842-136">Si elige usar la API de REST, también puede llamar al punto de [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) conexión.</span><span class="sxs-lookup"><span data-stu-id="b7842-136">If you choose to use the REST API, you can also call the [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) endpoint.</span></span>

<span data-ttu-id="b7842-137">En un canal, la respuesta a un mensaje se muestra como una respuesta a la cadena de respuesta que inicia.</span><span class="sxs-lookup"><span data-stu-id="b7842-137">In a channel, replying to a message shows as a reply to the initiating reply chain.</span></span> <span data-ttu-id="b7842-138">Contiene `conversation.id` el canal y el identificador de mensaje de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="b7842-138">The `conversation.id` contains the channel and the top level message ID.</span></span> <span data-ttu-id="b7842-139">Aunque Bot Framework se encarga de los detalles, puede almacenar en caché para futuras respuestas a ese hilo `conversation.id` de conversación según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b7842-139">Although the Bot Framework takes care of the details, you can cache that `conversation.id` for future replies to that conversation thread as needed.</span></span>

### <a name="best-practice-welcome-messages-in-teams"></a><span data-ttu-id="b7842-140">Procedimiento recomendado: Recibir mensajes en Teams</span><span class="sxs-lookup"><span data-stu-id="b7842-140">Best practice: Welcome messages in Teams</span></span>

<span data-ttu-id="b7842-141">Cuando el bot se agrega por primera vez al grupo o equipo, por lo general resulta útil enviar un mensaje de bienvenida que presenta el bot a todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="b7842-141">When your bot is first added to the group or team, it is generally useful to send a welcome message introducing the bot to all users.</span></span> <span data-ttu-id="b7842-142">El mensaje de bienvenida debe proporcionar una descripción de la funcionalidad y las ventajas del usuario del bot.</span><span class="sxs-lookup"><span data-stu-id="b7842-142">The welcome message should provide a description of the bot’s functionality and user benefits.</span></span> <span data-ttu-id="b7842-143">Lo ideal es que el mensaje también incluya comandos para que el usuario interactúe con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b7842-143">Ideally the message should also include commands for the user to interact with the app.</span></span> <span data-ttu-id="b7842-144">Para ello, asegúrese de que el bot responde al mensaje, con `conversationUpdate` `teamsAddMembers` eventType en el `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="b7842-144">To do this, ensure that your bot responds to the `conversationUpdate` message, with the `teamsAddMembers` eventType in the `channelData` object.</span></span> <span data-ttu-id="b7842-145">Asegúrese de que el identificador es el id. de aplicación del bot, ya que el mismo evento se envía cuando se agrega un usuario `memberAdded` a un equipo.</span><span class="sxs-lookup"><span data-stu-id="b7842-145">Be sure that the `memberAdded` ID is the bot's App ID itself, because the same event is sent when a user is added to a team.</span></span> <span data-ttu-id="b7842-146">Consulta [Adición de bots o](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) miembros del equipo para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="b7842-146">See [Team member or bot addition](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) for more details.</span></span>

<span data-ttu-id="b7842-147">Es posible que también quieras enviar un mensaje personal a cada miembro del equipo cuando se agrega el bot.</span><span class="sxs-lookup"><span data-stu-id="b7842-147">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="b7842-148">Para ello, puede capturar [la lista de equipos](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) y enviar a cada usuario un mensaje [directo](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span><span class="sxs-lookup"><span data-stu-id="b7842-148">To do this, you could [fetch the team roster](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) and send each user a [direct message](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span></span>

<span data-ttu-id="b7842-149">Se recomienda que el bot *no envíe* un mensaje de bienvenida en las siguientes situaciones:</span><span class="sxs-lookup"><span data-stu-id="b7842-149">We recommend that your bot *not* send a welcome message in the following situations:</span></span>

* <span data-ttu-id="b7842-150">El equipo es grande (obviamente subjetivo, por ejemplo, más de 100 miembros).</span><span class="sxs-lookup"><span data-stu-id="b7842-150">The team is big (obviously subjective, for example, more than 100 members).</span></span> <span data-ttu-id="b7842-151">El bot puede verse como "spammy" y la persona que lo agregó puede recibir quejas a menos que comuniques claramente la propuesta de valor del bot a todos los usuarios que vean el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="b7842-151">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="b7842-152">El bot se menciona por primera vez en un grupo o canal, en lugar de agregarse primero a un equipo.</span><span class="sxs-lookup"><span data-stu-id="b7842-152">Your bot is first mentioned in a group or channel, versus being first added to a team.</span></span>
* <span data-ttu-id="b7842-153">Se cambia el nombre de un grupo o canal.</span><span class="sxs-lookup"><span data-stu-id="b7842-153">A group or channel is renamed.</span></span>
* <span data-ttu-id="b7842-154">Un miembro del equipo se agrega a un grupo o canal.</span><span class="sxs-lookup"><span data-stu-id="b7842-154">A team member is added to a group or channel.</span></span>

## <a name="-mentions"></a><span data-ttu-id="b7842-155">@ Menciones</span><span class="sxs-lookup"><span data-stu-id="b7842-155">@ Mentions</span></span>

<span data-ttu-id="b7842-156">Dado que los bots de un grupo o canal responden solo cuando se mencionan ("@_botname_") en un mensaje, cada mensaje recibido por un bot en un canal de grupo contiene su propio nombre y debe asegurarse de que el análisis de mensajes lo controla.</span><span class="sxs-lookup"><span data-stu-id="b7842-156">Because bots in a group or channel respond only when they are mentioned ("@_botname_") in a message, every message received by a bot in a group channel contains its own name, and you must ensure your message parsing handles that.</span></span> <span data-ttu-id="b7842-157">Además, los bots pueden analizar otros usuarios mencionados y mencionar a los usuarios como parte de sus mensajes.</span><span class="sxs-lookup"><span data-stu-id="b7842-157">In addition, bots can parse out other users mentioned and mention users as part of their messages.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="b7842-158">Recuperación de menciones</span><span class="sxs-lookup"><span data-stu-id="b7842-158">Retrieving mentions</span></span>

<span data-ttu-id="b7842-159">Las menciones se devuelven en el objeto en carga y contienen el identificador único del usuario y, en la mayoría de los casos, el nombre `entities` del usuario mencionado.</span><span class="sxs-lookup"><span data-stu-id="b7842-159">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="b7842-160">Puede recuperar todas las menciones del mensaje llamando a la función en bot `GetMentions` Builder SDK para .NET, que devuelve una matriz de `Mentioned` objetos.</span><span class="sxs-lookup"><span data-stu-id="b7842-160">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK for .NET, which returns an array of `Mentioned` objects.</span></span>

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="b7842-161">Código de ejemplo de .NET: comprobar y quitar @bot mención</span><span class="sxs-lookup"><span data-stu-id="b7842-161">.NET example code: Check for and strip @bot mention</span></span>

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
> <span data-ttu-id="b7842-162">También puede usar la función Teams extensión , que elimina todas las `GetTextWithoutMentions` menciones, incluido el bot.</span><span class="sxs-lookup"><span data-stu-id="b7842-162">You can also use the Teams extension function `GetTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="b7842-163">Node.js ejemplo: comprobar y quitar @bot menciones</span><span class="sxs-lookup"><span data-stu-id="b7842-163">Node.js example code: Check for and strip @bot mention</span></span>

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

<span data-ttu-id="b7842-164">También puede usar la función Teams extensión , que elimina todas las `getTextWithoutMentions` menciones, incluido el bot.</span><span class="sxs-lookup"><span data-stu-id="b7842-164">You can also use the Teams extension function `getTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="b7842-165">Menciones de construcción</span><span class="sxs-lookup"><span data-stu-id="b7842-165">Constructing mentions</span></span>

<span data-ttu-id="b7842-166">El bot puede mencionar a otros usuarios en mensajes publicados en canales.</span><span class="sxs-lookup"><span data-stu-id="b7842-166">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="b7842-167">Para ello, el mensaje debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b7842-167">To do this, your message must do the following:</span></span>

* <span data-ttu-id="b7842-168">Incluir `<at>@username</at>` en el texto del mensaje.</span><span class="sxs-lookup"><span data-stu-id="b7842-168">Include `<at>@username</at>` in the message text.</span></span>
* <span data-ttu-id="b7842-169">Incluya el `mention` objeto dentro de la colección de entidades.</span><span class="sxs-lookup"><span data-stu-id="b7842-169">Include the `mention` object inside the entities collection.</span></span>

#### <a name="net-example"></a><span data-ttu-id="b7842-170">Ejemplo de .NET</span><span class="sxs-lookup"><span data-stu-id="b7842-170">.NET example</span></span>

<span data-ttu-id="b7842-171">En este ejemplo se [usa microsoft.bot.connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet paquete.</span><span class="sxs-lookup"><span data-stu-id="b7842-171">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a><span data-ttu-id="b7842-172">Node.js ejemplo</span><span class="sxs-lookup"><span data-stu-id="b7842-172">Node.js example</span></span>

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

#### <a name="example-outgoing-message-with-user-mentioned"></a><span data-ttu-id="b7842-173">Ejemplo: mensaje saliente con el usuario mencionado</span><span class="sxs-lookup"><span data-stu-id="b7842-173">Example: Outgoing message with user mentioned</span></span>

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

## <a name="accessing-groupchat-or-channel-scope"></a><span data-ttu-id="b7842-174">Acceso a groupChat o ámbito de canal</span><span class="sxs-lookup"><span data-stu-id="b7842-174">Accessing groupChat or channel scope</span></span>

<span data-ttu-id="b7842-175">El bot puede hacer más que enviar y recibir mensajes en grupos y equipos.</span><span class="sxs-lookup"><span data-stu-id="b7842-175">Your bot can do more than send and receive messages in groups and teams.</span></span> <span data-ttu-id="b7842-176">Por ejemplo, también puede capturar la lista de miembros, incluida su información de perfil, así como la lista de canales.</span><span class="sxs-lookup"><span data-stu-id="b7842-176">For instance, it can also fetch the list of members, including their profile information, as well as the list of channels.</span></span> <span data-ttu-id="b7842-177">Para obtener más información, vea [Get context for your Microsoft Teams bot](~/resources/bot-v3/bots-context.md).</span><span class="sxs-lookup"><span data-stu-id="b7842-177">For more information, see [Get context for your Microsoft Teams bot](~/resources/bot-v3/bots-context.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="b7842-178">Consulte también</span><span class="sxs-lookup"><span data-stu-id="b7842-178">See also</span></span>

[<span data-ttu-id="b7842-179">Ejemplos de Bot Framework</span><span class="sxs-lookup"><span data-stu-id="b7842-179">Bot Framework samples</span></span>](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)

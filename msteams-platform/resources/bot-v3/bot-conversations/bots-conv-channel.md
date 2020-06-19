---
title: Conversaciones de chat en grupo y de canal con bots
description: Describe el escenario de un extremo a otro de tener una conversación con un bot en un canal en Microsoft Teams.
keywords: escenarios de conferencia de canales de Teams
ms.date: 06/25/2019
ms.openlocfilehash: d2d72bdba43de6ebb10c7504dd309459cb09d56c
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801474"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="04239-104">Conversaciones de chat en grupo y en el canal con un bot de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="04239-104">Channel and Group chat conversations with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="04239-105">Microsoft Teams permite a los usuarios traer bots a sus conversaciones de chat en el canal o en el grupo.</span><span class="sxs-lookup"><span data-stu-id="04239-105">Microsoft Teams allows users to bring bots into their channel or group chat conversations.</span></span> <span data-ttu-id="04239-106">Al agregar un bot a un equipo o un chat, todos los usuarios de la conversación pueden aprovechar la funcionalidad de bot en la conversación.</span><span class="sxs-lookup"><span data-stu-id="04239-106">By adding a bot to a team or chat, all users of the conversation can take advantage of the bot functionality right in the conversation.</span></span> <span data-ttu-id="04239-107">También puede tener acceso a la funcionalidad específica de Teams dentro de su bot, como consultar la información del equipo y los usuarios de @mentioning.</span><span class="sxs-lookup"><span data-stu-id="04239-107">You can also access Teams-specific functionality within your bot like querying team information and @mentioning users.</span></span>

<span data-ttu-id="04239-108">Los chats de canales y chats de grupo se diferencian de los chats personales en que el usuario debe @mention el bot.</span><span class="sxs-lookup"><span data-stu-id="04239-108">Chat in channels and group chats differ from personal chat in that the user needs to @mention the bot.</span></span> <span data-ttu-id="04239-109">Si se usa un bot en varios ámbitos (personal, Groupchat o Channel), tendrá que detectar el ámbito desde el que proceden los mensajes de Bot y procesarlos en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="04239-109">If a bot is used in multiple scopes (personal, groupchat or channel) you will need to detect what scope the bot messages came from, and process them accordingly.</span></span>

## <a name="designing-a-great-bot-for-channels-or-groups"></a><span data-ttu-id="04239-110">Diseño de un gran robot para canales o grupos</span><span class="sxs-lookup"><span data-stu-id="04239-110">Designing a great bot for channels or groups</span></span>

<span data-ttu-id="04239-111">Los bots agregados a un equipo se convierten en otro miembro del equipo, que puede ser @mentioned como parte de la conversación.</span><span class="sxs-lookup"><span data-stu-id="04239-111">Bots added to a team become another team member, who can be @mentioned as part of the conversation.</span></span> <span data-ttu-id="04239-112">De hecho, los bots sólo reciben mensajes cuando se @mentioned, por lo que no se envían otras conversaciones en el canal al bot.</span><span class="sxs-lookup"><span data-stu-id="04239-112">In fact, bots only receive messages when they are @mentioned, so other conversations on the channel are not sent to the bot.</span></span>

> [!NOTE]
> <span data-ttu-id="04239-113">Por comodidad al responder a los mensajes de bot en un canal, el nombre del bot se antepone en el cuadro de mensaje de redacción de forma automática.</span><span class="sxs-lookup"><span data-stu-id="04239-113">For convenience when replying to bot messages in a channel, the bot name is prepended in the compose message box automatically.</span></span>

<span data-ttu-id="04239-114">Un bot en un grupo o un canal debe proporcionar información relevante y adecuada para todos los miembros.</span><span class="sxs-lookup"><span data-stu-id="04239-114">A bot in a group or channel should provide information relevant and appropriate for all members.</span></span> <span data-ttu-id="04239-115">Aunque el bot puede proporcionar toda la información relevante para la experiencia, tenga en cuenta que todos los usuarios pueden ver las conversaciones.</span><span class="sxs-lookup"><span data-stu-id="04239-115">While your bot can certainly provide any information relevant to the experience, keep in mind conversations with it are visible to everyone.</span></span> <span data-ttu-id="04239-116">Por lo tanto, un gran bot en un grupo o un canal debe agregar valor a todos los usuarios y, ciertamente, no compartir información de forma más adecuada en una conversación de uno a uno.</span><span class="sxs-lookup"><span data-stu-id="04239-116">Therefore, a great bot in a group or channel should add value to all users, and certainly not inadvertently share information more appropriate in a one-to-one conversation.</span></span>

<span data-ttu-id="04239-117">El bot puede ser totalmente relevante en todos los ámbitos tal y como es, y no se requiere un trabajo adicional importante para permitir que el bot funcione a través de ellos.</span><span class="sxs-lookup"><span data-stu-id="04239-117">Your bot might be entirely relevant in all scopes as is, and no significant extra work is required to allow your bot to work across them.</span></span> <span data-ttu-id="04239-118">En Microsoft Teams no hay expectativa de que la función bot funcione en todos los ámbitos, pero debe asegurarse de que su bot proporciona valor de usuario en el ámbito o ámbitos que desee admitir.</span><span class="sxs-lookup"><span data-stu-id="04239-118">In Microsoft Teams there is no expectation that your bot function in all scopes, but you should ensure your bot provides user value in whichever scope(s) you choose to support.</span></span> <span data-ttu-id="04239-119">Para obtener más información sobre los ámbitos, consulte [aplicaciones en Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04239-119">For more information on scopes, see [Apps in Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="04239-120">El desarrollo de un bot que funciona en grupos o canales usa la mayor parte de la funcionalidad de las conversaciones personales.</span><span class="sxs-lookup"><span data-stu-id="04239-120">Developing a bot that works in groups or channels uses much of the same functionality from personal conversations.</span></span> <span data-ttu-id="04239-121">Los datos y los eventos adicionales de la carga proporcionan información sobre el grupo y el canal de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="04239-121">Additional events and data in the payload provide Teams group and channel information.</span></span> <span data-ttu-id="04239-122">Estas diferencias, así como las diferencias clave en la funcionalidad común, se describen en las siguientes secciones.</span><span class="sxs-lookup"><span data-stu-id="04239-122">Those differences, as well as key differences in common functionality are described in the following sections.</span></span>

### <a name="creating-messages"></a><span data-ttu-id="04239-123">Crear mensajes</span><span class="sxs-lookup"><span data-stu-id="04239-123">Creating messages</span></span>

<span data-ttu-id="04239-124">Para obtener más información acerca de los bots que crean mensajes en canales, consulte [Mensajería proactiva para bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)y [crear específicamente una conversación de canal](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).</span><span class="sxs-lookup"><span data-stu-id="04239-124">For more information on bots creating messages in channels see [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md), and specifically [Creating a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).</span></span>

### <a name="receiving-messages"></a><span data-ttu-id="04239-125">Recibir mensajes</span><span class="sxs-lookup"><span data-stu-id="04239-125">Receiving messages</span></span>

<span data-ttu-id="04239-126">Para un bot en un grupo o canal, además del [esquema normal del mensaje](https://docs.botframework.com/core-concepts/reference/#activity), el bot también recibe las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="04239-126">For a bot in a group or channel, in addition to the [regular message schema](https://docs.botframework.com/core-concepts/reference/#activity), your bot also receives the following properties:</span></span>

* <span data-ttu-id="04239-127">`channelData`Consulte [Teams Data Channels](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data).</span><span class="sxs-lookup"><span data-stu-id="04239-127">`channelData` See [Teams channel data](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data).</span></span> <span data-ttu-id="04239-128">En un chat en grupo, contiene información específica de ese chat.</span><span class="sxs-lookup"><span data-stu-id="04239-128">In a group chat, contains information specific to that chat.</span></span>
* <span data-ttu-id="04239-129">`conversation.id`IDENTIFICADOR de la cadena de respuesta que consta del identificador de canal más el identificador del primer mensaje en la cadena de respuesta.</span><span class="sxs-lookup"><span data-stu-id="04239-129">`conversation.id` The reply chain ID, consisting of channel ID plus the ID of the first message in the reply chain</span></span>
* <span data-ttu-id="04239-130">`conversation.isGroup`Está `true` destinado a los mensajes de bot en canales o chats de grupo</span><span class="sxs-lookup"><span data-stu-id="04239-130">`conversation.isGroup` Is `true` for bot messages in channels or group chats</span></span>
* <span data-ttu-id="04239-131">`conversation.conversationType`Ya sea `groupChat` o`channel`</span><span class="sxs-lookup"><span data-stu-id="04239-131">`conversation.conversationType` Either `groupChat` or `channel`</span></span>
* <span data-ttu-id="04239-132">`entities`Puede contener una o más menciones (vea las [menciones](#-mentions))</span><span class="sxs-lookup"><span data-stu-id="04239-132">`entities` Can contain one or more mentions (see [Mentions](#-mentions))</span></span>

### <a name="replying-to-messages"></a><span data-ttu-id="04239-133">Responder a mensajes</span><span class="sxs-lookup"><span data-stu-id="04239-133">Replying to messages</span></span>

<span data-ttu-id="04239-134">Para responder a un mensaje existente, llame a [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) .net o a [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) Node.js.</span><span class="sxs-lookup"><span data-stu-id="04239-134">To reply to an existing message, call [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) in .NET or [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) in Node.js.</span></span> <span data-ttu-id="04239-135">El SDK de bot Builder controla todos los detalles.</span><span class="sxs-lookup"><span data-stu-id="04239-135">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="04239-136">Si decide usar la API de REST, también puede llamar al punto de [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) conexión.</span><span class="sxs-lookup"><span data-stu-id="04239-136">If you choose to use the REST API, you can also call the [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) endpoint.</span></span>

<span data-ttu-id="04239-137">En un canal, la respuesta a un mensaje se muestra como una respuesta a la cadena de respuesta de iniciación.</span><span class="sxs-lookup"><span data-stu-id="04239-137">In a channel, replying to a message shows as a reply to the initiating reply chain.</span></span> <span data-ttu-id="04239-138">El `conversation.id` contiene el canal y el identificador de mensaje de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="04239-138">The `conversation.id` contains the channel and the top level message ID.</span></span> <span data-ttu-id="04239-139">Aunque el marco de bot se encarga de los detalles, puede almacenar en la memoria caché el que, en el `conversation.id` caso de respuestas futuras, a ese hilo de conversación según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="04239-139">Although the Bot Framework takes care of the details, you can cache that `conversation.id` for future replies to that conversation thread as needed.</span></span>

### <a name="best-practice-welcome-messages-in-teams"></a><span data-ttu-id="04239-140">Procedimiento recomendado: mensajes de bienvenida en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="04239-140">Best practice: Welcome messages in Teams</span></span>

<span data-ttu-id="04239-141">Cuando el bot se agrega por primera vez al grupo o equipo, suele ser útil enviar un mensaje de bienvenida que presenta el bot a todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="04239-141">When your bot is first added to the group or team, it is generally useful to send a welcome message introducing the bot to all users.</span></span> <span data-ttu-id="04239-142">El mensaje de bienvenida debe proporcionar una descripción de las ventajas del usuario y la funcionalidad del bot.</span><span class="sxs-lookup"><span data-stu-id="04239-142">The welcome message should provide a description of the bot’s functionality and user benefits.</span></span> <span data-ttu-id="04239-143">Lo ideal es que el mensaje también incluya comandos para que el usuario interactúe con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="04239-143">Ideally the message should also include commands for the user to interact with the app.</span></span> <span data-ttu-id="04239-144">Para ello, asegúrese de que el bot responde al `conversationUpdate` mensaje, con el `teamsAddMembers` EventType en el `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="04239-144">To do this, ensure that your bot responds to the `conversationUpdate` message, with the `teamsAddMembers` eventType in the `channelData` object.</span></span> <span data-ttu-id="04239-145">Asegúrese de que el `memberAdded` identificador es el propio identificador de aplicación del bot, ya que se envía el mismo evento cuando se agrega un usuario a un equipo.</span><span class="sxs-lookup"><span data-stu-id="04239-145">Be sure that the `memberAdded` ID is the bot's App ID itself, because the same event is sent when a user is added to a team.</span></span> <span data-ttu-id="04239-146">Consulte el [miembro del equipo o la adición de bot](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="04239-146">See [Team member or bot addition](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) for more details.</span></span>

<span data-ttu-id="04239-147">Es posible que también desee enviar un mensaje personal a cada miembro del equipo cuando se agregue el bot.</span><span class="sxs-lookup"><span data-stu-id="04239-147">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="04239-148">Para ello, puede [recuperar la lista de equipos](~/resources/bot-v3/bots-context.md#fetching-the-team-roster) y enviar a cada usuario un [mensaje directo](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span><span class="sxs-lookup"><span data-stu-id="04239-148">To do this, you could [fetch the team roster](~/resources/bot-v3/bots-context.md#fetching-the-team-roster) and send each user a [direct message](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span></span>

<span data-ttu-id="04239-149">Se recomienda que el bot *no* envíe un mensaje de bienvenida en las siguientes situaciones:</span><span class="sxs-lookup"><span data-stu-id="04239-149">We recommend that your bot *not* send a welcome message in the following situations:</span></span>

* <span data-ttu-id="04239-150">El equipo es grande (obviamente subjetivo, pero por ejemplo, más de 100 miembros).</span><span class="sxs-lookup"><span data-stu-id="04239-150">The team is large (obviously subjective, but for example larger than 100 members).</span></span> <span data-ttu-id="04239-151">El bot puede aparecer como "correo no deseado" y la persona que lo agregó puede recibir quejas a menos que comunique claramente la propuesta de valor de su bot a todos los usuarios que ven el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="04239-151">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="04239-152">El bot se menciona primero en un grupo o canal (en lugar de agregarse primero a un equipo)</span><span class="sxs-lookup"><span data-stu-id="04239-152">Your bot is first mentioned in a group or channel (versus being first added to a team)</span></span>
* <span data-ttu-id="04239-153">Se cambia el nombre de un grupo o canal</span><span class="sxs-lookup"><span data-stu-id="04239-153">A group or channel is renamed</span></span>
* <span data-ttu-id="04239-154">Un miembro del equipo se agrega a un grupo o un canal</span><span class="sxs-lookup"><span data-stu-id="04239-154">A team member is added to a group or channel</span></span>

## <a name="-mentions"></a><span data-ttu-id="04239-155">@ Menciones</span><span class="sxs-lookup"><span data-stu-id="04239-155">@ Mentions</span></span>

<span data-ttu-id="04239-156">Debido a que los bots de un grupo o canal solo responden cuando se mencionan ("@_botname_") en un mensaje, cada mensaje recibido por un bot en un canal de grupo contiene su propio nombre y debe asegurarse de que los controladores de análisis de mensajes.</span><span class="sxs-lookup"><span data-stu-id="04239-156">Because bots in a group or channel respond only when they are mentioned ("@_botname_") in a message, every message received by a bot in a group channel contains its own name, and you must ensure your message parsing handles that.</span></span> <span data-ttu-id="04239-157">Además, los bots pueden analizar a otros usuarios mencionados y mencionar a los usuarios como parte de sus mensajes.</span><span class="sxs-lookup"><span data-stu-id="04239-157">In addition, bots can parse out other users mentioned and mention users as part of their messages.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="04239-158">Recuperación de menciones</span><span class="sxs-lookup"><span data-stu-id="04239-158">Retrieving mentions</span></span>

<span data-ttu-id="04239-159">Las menciones se devuelven en el `entities` objeto en la carga y contienen el identificador único del usuario y, en la mayoría de los casos, el nombre del usuario mencionado.</span><span class="sxs-lookup"><span data-stu-id="04239-159">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="04239-160">Puede recuperar todas las menciones del mensaje llamando a la `GetMentions` función en el SDK de bot Builder para .net, que devuelve una matriz `Mentioned` de objetos.</span><span class="sxs-lookup"><span data-stu-id="04239-160">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK for .NET, which returns an array of `Mentioned` objects.</span></span>

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="04239-161">Código de ejemplo de .NET: comprobar y quitar @bot mención</span><span class="sxs-lookup"><span data-stu-id="04239-161">.NET example code: Check for and strip @bot mention</span></span>

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
> <span data-ttu-id="04239-162">También puede usar la función de extensión de Teams `GetTextWithoutMentions` , que elimina todas las menciones, incluido el bot.</span><span class="sxs-lookup"><span data-stu-id="04239-162">You can also use the Teams extension function `GetTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="04239-163">Código de ejemplo Node.js: buscar y quitar @bot mención</span><span class="sxs-lookup"><span data-stu-id="04239-163">Node.js example code: Check for and strip @bot mention</span></span>

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

<span data-ttu-id="04239-164">También puede usar la función de extensión de Teams `getTextWithoutMentions` , que elimina todas las menciones, incluido el bot.</span><span class="sxs-lookup"><span data-stu-id="04239-164">You can also use the Teams extension function `getTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="04239-165">Creación de menciones</span><span class="sxs-lookup"><span data-stu-id="04239-165">Constructing mentions</span></span>

<span data-ttu-id="04239-166">El bot puede mencionar a otros usuarios en los mensajes enviados a los canales.</span><span class="sxs-lookup"><span data-stu-id="04239-166">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="04239-167">Para ello, el mensaje debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="04239-167">To do this, your message must do the following:</span></span>

* <span data-ttu-id="04239-168">Incluir `<at>@username</at>` en el texto del mensaje</span><span class="sxs-lookup"><span data-stu-id="04239-168">Include `<at>@username</at>` in the message text</span></span>
* <span data-ttu-id="04239-169">Incluir el `mention` objeto dentro de la colección Entities</span><span class="sxs-lookup"><span data-stu-id="04239-169">Include the `mention` object inside the entities collection</span></span>

#### <a name="net-example"></a><span data-ttu-id="04239-170">Ejemplo de .NET</span><span class="sxs-lookup"><span data-stu-id="04239-170">.NET example</span></span>

<span data-ttu-id="04239-171">En este ejemplo se usa el paquete NuGet [Microsoft. bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) .</span><span class="sxs-lookup"><span data-stu-id="04239-171">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a><span data-ttu-id="04239-172">Ejemplo de Node.js</span><span class="sxs-lookup"><span data-stu-id="04239-172">Node.js example</span></span>

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

#### <a name="example-outgoing-message-with-user-mentioned"></a><span data-ttu-id="04239-173">Ejemplo: mensaje saliente con el usuario mencionado</span><span class="sxs-lookup"><span data-stu-id="04239-173">Example: Outgoing message with user mentioned</span></span>

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

## <a name="accessing-groupchat-or-channel-scope"></a><span data-ttu-id="04239-174">Acceso a groupChat o al ámbito del canal</span><span class="sxs-lookup"><span data-stu-id="04239-174">Accessing groupChat or channel scope</span></span>

<span data-ttu-id="04239-175">El bot puede hacer más cosas que enviar y recibir mensajes en grupos y equipos.</span><span class="sxs-lookup"><span data-stu-id="04239-175">Your bot can do more than send and receive messages in groups and teams.</span></span> <span data-ttu-id="04239-176">Por ejemplo, también puede recuperar la lista de miembros, incluida la información de su perfil, así como la lista de canales.</span><span class="sxs-lookup"><span data-stu-id="04239-176">For instance, it can also fetch the list of members, including their profile information, as well as the list of channels.</span></span> <span data-ttu-id="04239-177">Consulte [obtener contexto de su bot de Microsoft Teams](~/resources/bot-v3/bots-context.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="04239-177">See [Get context for your Microsoft Teams bot](~/resources/bot-v3/bots-context.md) to learn more.</span></span>

<span data-ttu-id="04239-178">*Vea también* [ejemplos del marco de bot](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="04239-178">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

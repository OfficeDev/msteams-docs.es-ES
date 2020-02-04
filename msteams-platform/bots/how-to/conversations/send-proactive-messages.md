---
title: Enviar mensajes proactivos
author: clearab
description: Cómo enviar mensajes proactivos con su bot de Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: e60fdbfb909abec2c6d64ed0d32fa1a4c4b463a6
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675853"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="9888d-103">Enviar mensajes proactivos</span><span class="sxs-lookup"><span data-stu-id="9888d-103">Send proactive messages</span></span>

> [!Note]
> <span data-ttu-id="9888d-104">En los ejemplos de código de este artículo se usa el SDK de V3 Framework SDK y las extensiones de SDK de Teams bot Builder de V3.</span><span class="sxs-lookup"><span data-stu-id="9888d-104">The code samples in this article make use of the v3 Bot Framework SDK, and v3 Teams Bot Builder SDK extensions.</span></span> <span data-ttu-id="9888d-105">Conceptualmente, la información se aplica cuando se usan las versiones V4 del SDK, pero el código es ligeramente diferente.</span><span class="sxs-lookup"><span data-stu-id="9888d-105">Conceptually, the information applies when using the v4 versions of the SDK, but the code is slightly different.</span></span>

<span data-ttu-id="9888d-106">Un mensaje proactivo es un mensaje enviado por un bot para iniciar una conversación.</span><span class="sxs-lookup"><span data-stu-id="9888d-106">A proactive message is a message that is sent by a bot to start a conversation.</span></span> <span data-ttu-id="9888d-107">Es posible que desee que el bot inicie una conversación por varios motivos, entre los que se incluyen:</span><span class="sxs-lookup"><span data-stu-id="9888d-107">You may want your bot to start a conversation for a number of reasons, including:</span></span>

* <span data-ttu-id="9888d-108">Mensajes de bienvenida para conversaciones de bot personal</span><span class="sxs-lookup"><span data-stu-id="9888d-108">Welcome messages for personal bot conversations</span></span>
* <span data-ttu-id="9888d-109">Respuestas de sondeo</span><span class="sxs-lookup"><span data-stu-id="9888d-109">Poll responses</span></span>
* <span data-ttu-id="9888d-110">Notificaciones de eventos externos</span><span class="sxs-lookup"><span data-stu-id="9888d-110">External event notifications</span></span>

<span data-ttu-id="9888d-111">El envío de un mensaje para iniciar una nueva conversación es diferente al de enviar un mensaje en respuesta a una conversación existente: cuando el bot inicia una nueva conversación, no hay ninguna conversación preexistente para publicar el mensaje en.</span><span class="sxs-lookup"><span data-stu-id="9888d-111">Sending a message to start a new conversation thread is different than sending a message in response to an existing conversation: when your bot starts a new a conversation, there is no pre-existing conversation to post the message to.</span></span> <span data-ttu-id="9888d-112">Para poder enviar un mensaje proactivo debe:</span><span class="sxs-lookup"><span data-stu-id="9888d-112">In order to send a proactive message you need to:</span></span>

1. [<span data-ttu-id="9888d-113">Decide qué vas a decir</span><span class="sxs-lookup"><span data-stu-id="9888d-113">Decide what you're going to say</span></span>](#best-practices-for-proactive-messaging)
1. [<span data-ttu-id="9888d-114">Obtener el identificador único del usuario y el identificador de inquilino</span><span class="sxs-lookup"><span data-stu-id="9888d-114">Obtain the user's unique Id and tenant Id</span></span>](#obtain-necessary-user-information)
1. [<span data-ttu-id="9888d-115">Enviar el mensaje</span><span class="sxs-lookup"><span data-stu-id="9888d-115">Send the message</span></span>](#examples)

<span data-ttu-id="9888d-116">Al crear mensajes proactivos \*\*\*\* a los `MicrosoftAppCredentials.TrustServiceUrl`que se debe llamar y pasar la dirección URL del `ConnectorClient` servicio antes de crear el, se usará para enviar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="9888d-116">When creating proactive messages you **must** call `MicrosoftAppCredentials.TrustServiceUrl`, and pass in the service URL before creating the `ConnectorClient` you will use to send the message.</span></span> <span data-ttu-id="9888d-117">Si no lo hace, la aplicación recibirá una `401: Unauthorized` respuesta.</span><span class="sxs-lookup"><span data-stu-id="9888d-117">If you do not, your app will receive a `401: Unauthorized` response.</span></span> 

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="9888d-118">Procedimientos recomendados para la mensajería proactiva</span><span class="sxs-lookup"><span data-stu-id="9888d-118">Best practices for proactive messaging</span></span>

<span data-ttu-id="9888d-119">El envío de mensajes proactivos a los usuarios puede ser una forma muy eficaz de comunicarse con los usuarios.</span><span class="sxs-lookup"><span data-stu-id="9888d-119">Sending proactive messages to users can be a very effective way to communicate with your users.</span></span> <span data-ttu-id="9888d-120">Sin embargo, desde su perspectiva puede parecer que este mensaje no se solicita completamente y, en el caso de los mensajes de bienvenida, será la primera vez que interactuen con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9888d-120">However, from their perspective this message can appear to come to them completely unprompted, and in the case of welcome messages will be the first time they've interacted with your app.</span></span> <span data-ttu-id="9888d-121">Por lo tanto, es muy importante usar esta funcionalidad con moderación (no enviar correo no deseado a los usuarios) y proporcionarle la información suficiente para que puedan comprender por qué se les está enviando un mensaje.</span><span class="sxs-lookup"><span data-stu-id="9888d-121">As such, it is very important to use this functionality sparingly (don't spam your users), and to provide them with enough information to let them understand why they are being messaged.</span></span>

<span data-ttu-id="9888d-122">Generalmente, los mensajes proactivos se dividen en dos categorías, mensajes de bienvenida o notificaciones.</span><span class="sxs-lookup"><span data-stu-id="9888d-122">Proactive messages generally fall into one of two categories, welcome messages or notifications.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="9888d-123">Mensajes de bienvenida</span><span class="sxs-lookup"><span data-stu-id="9888d-123">Welcome messages</span></span>

<span data-ttu-id="9888d-124">Al usar la mensajería proactiva para enviar un mensaje de bienvenida a un usuario, debe tener en cuenta que para la mayoría de las personas que reciben el mensaje no tendrán contexto por el motivo por el que lo reciben.</span><span class="sxs-lookup"><span data-stu-id="9888d-124">When using proactive messaging to send a welcome message to a user you must keep in mind that for most people receiving the message they will have no context for why they are receiving it.</span></span> <span data-ttu-id="9888d-125">También es la primera vez que interactuarán con la aplicación; es su oportunidad para crear una buena primera impresión.</span><span class="sxs-lookup"><span data-stu-id="9888d-125">This is also the first time they will have interacted with your app; it is your opportunity to create a good first impression.</span></span> <span data-ttu-id="9888d-126">Los mejores mensajes de bienvenida incluirán:</span><span class="sxs-lookup"><span data-stu-id="9888d-126">The best welcome messages will include:</span></span>

* <span data-ttu-id="9888d-127">**¿Por qué reciben este mensaje?**</span><span class="sxs-lookup"><span data-stu-id="9888d-127">**Why are they receiving this message.**</span></span> <span data-ttu-id="9888d-128">El usuario debe ser muy claro por qué reciben el mensaje.</span><span class="sxs-lookup"><span data-stu-id="9888d-128">It should be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="9888d-129">Si el bot se ha instalado en un canal y se ha enviado un mensaje de bienvenida a todos los usuarios, hágales saber en qué canal se ha instalado y que podrían instalarlo.</span><span class="sxs-lookup"><span data-stu-id="9888d-129">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="9888d-130">**Qué ofrece.**</span><span class="sxs-lookup"><span data-stu-id="9888d-130">**What do you offer.**</span></span> <span data-ttu-id="9888d-131">¿Qué puede hacer con la aplicación?</span><span class="sxs-lookup"><span data-stu-id="9888d-131">What can they do with your app?</span></span> <span data-ttu-id="9888d-132">¿Qué valor puede aportar a ellos?</span><span class="sxs-lookup"><span data-stu-id="9888d-132">What value can you bring to them?</span></span>
* <span data-ttu-id="9888d-133">**Qué debería hacer a continuación.**</span><span class="sxs-lookup"><span data-stu-id="9888d-133">**What should they do next.**</span></span> <span data-ttu-id="9888d-134">Invitar a probar un comando o interactuar con la aplicación de alguna manera.</span><span class="sxs-lookup"><span data-stu-id="9888d-134">Invite them to try out a command, or interact with your app in some way.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="9888d-135">Mensajes de notificación</span><span class="sxs-lookup"><span data-stu-id="9888d-135">Notification messages</span></span>

<span data-ttu-id="9888d-136">Al usar la mensajería proactiva para enviar notificaciones, debe asegurarse de que los usuarios tienen una ruta de acceso clara para emprender acciones comunes en función de la notificación y un conocimiento claro de la razón por la que se produjo la notificación.</span><span class="sxs-lookup"><span data-stu-id="9888d-136">When using proactive messaging to send notifications you need to make sure your users have a clear path to take common actions based on your notification, and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="9888d-137">Por lo general, los mensajes de notificación son correctos:</span><span class="sxs-lookup"><span data-stu-id="9888d-137">Good notification messages will generally include:</span></span>

* <span data-ttu-id="9888d-138">**Qué ha pasado.**</span><span class="sxs-lookup"><span data-stu-id="9888d-138">**What happened.**</span></span> <span data-ttu-id="9888d-139">Una indicación clara de lo que ha sucedido para provocar la notificación.</span><span class="sxs-lookup"><span data-stu-id="9888d-139">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="9888d-140">**Qué ocurrió.**</span><span class="sxs-lookup"><span data-stu-id="9888d-140">**What it happened to.**</span></span> <span data-ttu-id="9888d-141">Debe estar claro qué elemento/Thing se actualizó para provocar la notificación.</span><span class="sxs-lookup"><span data-stu-id="9888d-141">It should be clear what item/thing was updated to cause the notification.</span></span>
* <span data-ttu-id="9888d-142">**Quién lo llevó a cabo.**</span><span class="sxs-lookup"><span data-stu-id="9888d-142">**Who did it.**</span></span> <span data-ttu-id="9888d-143">Quién llevó a cabo la acción que hizo que se enviara la notificación.</span><span class="sxs-lookup"><span data-stu-id="9888d-143">Who took the action that caused the notification to be sent.</span></span>
* <span data-ttu-id="9888d-144">**Qué pueden hacer al respecto.**</span><span class="sxs-lookup"><span data-stu-id="9888d-144">**What they can do about it.**</span></span> <span data-ttu-id="9888d-145">Facilite a los usuarios que realicen acciones basadas en las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="9888d-145">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="9888d-146">**Cómo se pueden dejar de participar.** Debe proporcionar una ruta de acceso para que los usuarios puedan optar por las notificaciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="9888d-146">**How they can opt out.** You need to provide a path for users to opt out of additional notifications.</span></span>

## <a name="obtain-necessary-user-information"></a><span data-ttu-id="9888d-147">Obtener información de usuario necesaria</span><span class="sxs-lookup"><span data-stu-id="9888d-147">Obtain necessary user information</span></span>

<span data-ttu-id="9888d-148">Los bots pueden crear nuevas conversaciones con un usuario individual de Microsoft Teams obteniendo el *identificador único* del usuario y el *identificador de inquilino.*</span><span class="sxs-lookup"><span data-stu-id="9888d-148">Bots can create new conversations with an individual Microsoft Teams user by obtaining the user’s *unique ID* and *tenant ID.*</span></span> <span data-ttu-id="9888d-149">Puede obtener estos valores mediante uno de los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9888d-149">You can obtain these values using one of the following methods:</span></span>

* <span data-ttu-id="9888d-150">Mediante [la recopilación de la lista de equipos](../get-teams-context.md#fetching-the-roster-or-user-profile) desde un canal en el que está instalada la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9888d-150">By [fetching the team roster](../get-teams-context.md#fetching-the-roster-or-user-profile) from a channel your app is installed in.</span></span>
* <span data-ttu-id="9888d-151">Mediante el almacenamiento en la memoria caché cuando un usuario [interactúa con el bot en un canal](./channel-and-group-conversations.md).</span><span class="sxs-lookup"><span data-stu-id="9888d-151">By caching them when a user [interacts with your bot in a channel](./channel-and-group-conversations.md).</span></span>
* <span data-ttu-id="9888d-152">Cuando se @mentioned a un usuario [en una conversación de canal](./channel-and-group-conversations.md#retrieving-mentions) a la que pertenece el bot.</span><span class="sxs-lookup"><span data-stu-id="9888d-152">When a users is [@mentioned in a channel conversation](./channel-and-group-conversations.md#retrieving-mentions) the bot is a part of.</span></span>
* <span data-ttu-id="9888d-153">Al almacenarlos en la memoria caché cuando [recibe el `conversationUpdate` ](./subscribe-to-conversation-events.md#team-members-added) evento cuando la aplicación está instalada en un ámbito personal o se agregan nuevos miembros a un canal o chat de grupo que</span><span class="sxs-lookup"><span data-stu-id="9888d-153">By caching them when you [receive the `conversationUpdate`](./subscribe-to-conversation-events.md#team-members-added) event when your app is installed in a personal scope, or new members are added to a channel or group chat that</span></span>

### <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="9888d-154">Instalar de forma proactiva la aplicación con Graph</span><span class="sxs-lookup"><span data-stu-id="9888d-154">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="9888d-155">La instalación de aplicaciones de forma proactiva con Graph se encuentra actualmente en versión beta.</span><span class="sxs-lookup"><span data-stu-id="9888d-155">Proactively installing apps using graph is currently in beta.</span></span>

<span data-ttu-id="9888d-156">En ocasiones, es posible que sea necesario enviar un mensaje de forma proactiva a los usuarios que no hayan instalado ni interactúen con la aplicación anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9888d-156">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="9888d-157">Por ejemplo, desea usar el Communicator de la [compañía](~/samples/app-templates.md#company-communicator) para enviar mensajes a toda la organización.</span><span class="sxs-lookup"><span data-stu-id="9888d-157">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="9888d-158">Para este escenario, puede usar la API de Graph para instalar proactivamente la aplicación para sus usuarios y, a continuación, almacenar en `conversationUpdate` caché los valores necesarios del evento que la aplicación recibirá en el momento de la instalación.</span><span class="sxs-lookup"><span data-stu-id="9888d-158">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app will receive upon install.</span></span>

<span data-ttu-id="9888d-159">Solo puede instalar aplicaciones que estén en el catálogo de aplicaciones de la organización o en la tienda de aplicaciones de Teams.</span><span class="sxs-lookup"><span data-stu-id="9888d-159">You can only install apps that are in your organizational app catalogue, or the Teams app store.</span></span>

<span data-ttu-id="9888d-160">Consulte [install apps for users](/graph/teams-proactive-messaging) en la documentación de Graph para obtener detalles completos.</span><span class="sxs-lookup"><span data-stu-id="9888d-160">See [Install apps for users](/graph/teams-proactive-messaging) in the Graph documentation for complete details.</span></span> <span data-ttu-id="9888d-161">También hay un [ejemplo en .net](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span><span class="sxs-lookup"><span data-stu-id="9888d-161">There is also a [sample in .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span></span>

## <a name="examples"></a><span data-ttu-id="9888d-162">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="9888d-162">Examples</span></span>

<span data-ttu-id="9888d-163">Asegúrese de autenticar y de tener un token de portador antes de crear una nueva conversación mediante la API de REST.</span><span class="sxs-lookup"><span data-stu-id="9888d-163">Be sure that you authenticate and have a bearer token before creating a new conversation using the REST API.</span></span> <span data-ttu-id="9888d-164">El `members.id` campo del siguiente objeto es único para la combinación de Bot y un usuario.</span><span class="sxs-lookup"><span data-stu-id="9888d-164">The `members.id` field in the object below is unique to the combination of your bot and a user.</span></span> <span data-ttu-id="9888d-165">No puede obtenerla a través de cualquier otro método que no se haya descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9888d-165">You cannot obtain it via any other method than those outlined above.</span></span>

```json
POST /v3/conversations
{
  "bot": {
    "id": "28:10j12ou0d812-2o1098-c1mjojzldxcj-1098028n ",
    "name": "The Bot"
  },
  "members": [
    {
      "id": "29:012d20j1cjo20211"
    }
  ],
  "channelData": {
    "tenant": {
      "id": "197231joe-1209j01821-012kdjoj"
    }
  }
}
```

<span data-ttu-id="9888d-166">Debe proporcionar el identificador de usuario y el identificador de inquilino.</span><span class="sxs-lookup"><span data-stu-id="9888d-166">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="9888d-167">Si la llamada se realiza correctamente, la API devuelve el siguiente objeto de respuesta.</span><span class="sxs-lookup"><span data-stu-id="9888d-167">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

<span data-ttu-id="9888d-168">Este identificador es el identificador de conversación único de chat personal.</span><span class="sxs-lookup"><span data-stu-id="9888d-168">This ID is the personal chat's unique conversation ID.</span></span> <span data-ttu-id="9888d-169">Almacene este valor y vuelva a usarlo para interacciones futuras con el usuario.</span><span class="sxs-lookup"><span data-stu-id="9888d-169">Please store this value and reuse it for future interactions with the user.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="9888d-170">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9888d-170">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="9888d-171">En este ejemplo se usa el paquete NuGet [Microsoft. bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) .</span><span class="sxs-lookup"><span data-stu-id="9888d-171">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

```csharp
// Create or get existing chat conversation with user
var response = client.Conversations.CreateOrGetDirectConversation(activity.Recipient, activity.From, activity.GetTenantId());

// Construct the message to post to conversation
Activity newActivity = new Activity()
{
    Text = "Hello",
    Type = ActivityTypes.Message,
    Conversation = new ConversationAccount
    {
        Id = response.Id
    },
};

// Post the message to chat conversation with user
await client.Conversations.SendToConversationAsync(newActivity, response.Id);
```

# <a name="javascripttabjavascript"></a>[<span data-ttu-id="9888d-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="9888d-172">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="9888d-173">En este ejemplo se usa el paquete NPM [de botbuilder-Teams](https://www.npmjs.com/package/botbuilder-teams) .</span><span class="sxs-lookup"><span data-stu-id="9888d-173">This example uses the [botbuilder-teams](https://www.npmjs.com/package/botbuilder-teams) npm package.</span></span>

```javascript
var address =
{
    channelId: 'msteams',
    user: { id: userId },
    channelData: {
        tenant: {
            id: tenantId
        }
    },
    bot:
    {
        id: appId,
        name: appName
    },
    serviceUrl: session.message.address.serviceUrl,
    useAuth: true
}

var msg = new builder.Message().address(address);
msg.text('Hello, this is a notification');
bot.send(msg);
```

# <a name="pythontabpython"></a>[<span data-ttu-id="9888d-174">Python</span><span class="sxs-lookup"><span data-stu-id="9888d-174">Python</span></span>](#tab/python)

```python
async def _send_proactive_message():
  for conversation_reference in CONVERSATION_REFERENCES.values():
    return await ADAPTER.continue_conversation(APP_ID, conversation_reference,
      lambda turn_context: turn_context.send_activity("proactive hello")
    )

```

---

## <a name="creating-a-channel-conversation"></a><span data-ttu-id="9888d-175">Crear una conversación de canal</span><span class="sxs-lookup"><span data-stu-id="9888d-175">Creating a channel conversation</span></span>

<span data-ttu-id="9888d-176">El bot agregado por el equipo puede exponer en un canal para crear una nueva cadena de respuesta.</span><span class="sxs-lookup"><span data-stu-id="9888d-176">Your team-added bot can post into a channel to create a new reply chain.</span></span> <span data-ttu-id="9888d-177">Si usa el SDK de Team. js Teams, use `startReplyChain()` que le proporcione una dirección completa con el identificador de actividad y el identificador de conversación correctos. Si usa C#, vea el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="9888d-177">If you're using the Node.js Teams SDK, use `startReplyChain()` which gives you a fully-populated address with the correct activity id and conversation id. If you are using C#, see the example below.</span></span>

<span data-ttu-id="9888d-178">Como alternativa, puede usar la API de REST y enviar una solicitud POST al [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) recurso.</span><span class="sxs-lookup"><span data-stu-id="9888d-178">Alternatively, you can use the REST API and issue a POST request to [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) resource.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="9888d-179">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9888d-179">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="9888d-180">El siguiente fragmento de código es de [este ejemplo](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs).</span><span class="sxs-lookup"><span data-stu-id="9888d-180">The following code snippet is from [this sample](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs).</span></span>


```csharp
using Microsoft.Bot.Builder.Dialogs;
using Microsoft.Bot.Connector;
using Microsoft.Bot.Connector.Teams.Models;
using Microsoft.Teams.TemplateBotCSharp.Properties;
using System;
using System.Threading.Tasks;

namespace Microsoft.Teams.TemplateBotCSharp.Dialogs
{
    [Serializable]
    public class ProactiveMsgTo1to1Dialog : IDialog<object>
    {
        public async Task StartAsync(IDialogContext context)
        {
            if (context == null)
            {
                throw new ArgumentNullException(nameof(context));
            }

            var channelData = context.Activity.GetChannelData<TeamsChannelData>();
            var message = Activity.CreateMessageActivity();
            message.Text = "Hello World";

            var conversationParameters = new ConversationParameters
            {
                  IsGroup = true,
                  ChannelData = new TeamsChannelData
                  {
                      Channel = new ChannelInfo(channelData.Channel.Id),
                  },
                  Activity = (Activity) message
            };

            MicrosoftAppCredentials.TrustServiceUrl(serviceUrl, DateTime.MaxValue);
            var connectorClient = new ConnectorClient(new Uri(activity.ServiceUrl));
            var response = await connectorClient.Conversations.CreateConversationAsync(conversationParameters);

            context.Done<object>(null);
        }
    }
}
```

# <a name="javascripttabjavascript"></a>[<span data-ttu-id="9888d-181">JavaScript</span><span class="sxs-lookup"><span data-stu-id="9888d-181">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="9888d-182">En este ejemplo se usa el paquete NPM [de botbuilder-Teams](https://www.npmjs.com/package/botbuilder-teams) .</span><span class="sxs-lookup"><span data-stu-id="9888d-182">This example uses the [botbuilder-teams](https://www.npmjs.com/package/botbuilder-teams) npm package.</span></span> <span data-ttu-id="9888d-183">El siguiente fragmento de código es de [teamsConversationBot. js](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/57.teams-conversation-bot/bots/teamsConversationBot.js).</span><span class="sxs-lookup"><span data-stu-id="9888d-183">The following code snippet is from [teamsConversationBot.js](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/57.teams-conversation-bot/bots/teamsConversationBot.js).</span></span>

[!code-javascript[messageAllMembersAsync](~/../botbuilder-samples/samples/javascript_nodejs/57.teams-conversation-bot/bots/teamsConversationBot.js?range=115-134&highlight=13-15)]

# <a name="pythontabpython"></a>[<span data-ttu-id="9888d-184">Python</span><span class="sxs-lookup"><span data-stu-id="9888d-184">Python</span></span>](#tab/python)

[!code-python[message-all-members](~/../botbuilder-samples/samples/python/57.teams-conversation-bot/bots/teams_conversation_bot.py?range=101-135)]

---

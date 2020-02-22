---
title: Mensajes proactivos
description: Describe los bots puede iniciar una conversación en Microsoft Teams.
keywords: escenarios de la conversación de mensajería proactiva de Teams
ms.openlocfilehash: 2f644820da33acc885a7972b13a1f61c167d6d8f
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228069"
---
# <a name="proactive-messaging-for-bots"></a><span data-ttu-id="e3964-104">Mensajería proactiva para bots</span><span class="sxs-lookup"><span data-stu-id="e3964-104">Proactive messaging for bots</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="e3964-105">Un mensaje proactivo es un mensaje enviado por un bot para iniciar una conversación.</span><span class="sxs-lookup"><span data-stu-id="e3964-105">A proactive message is a message that is sent by a bot to start a conversation.</span></span> <span data-ttu-id="e3964-106">Es posible que desee que el bot inicie una conversación por varios motivos, entre los que se incluyen:</span><span class="sxs-lookup"><span data-stu-id="e3964-106">You may want your bot to start a conversation for a number of reasons, including:</span></span>

* <span data-ttu-id="e3964-107">Mensajes de bienvenida para conversaciones de bot personal</span><span class="sxs-lookup"><span data-stu-id="e3964-107">Welcome messages for personal bot conversations</span></span>
* <span data-ttu-id="e3964-108">Respuestas de sondeo</span><span class="sxs-lookup"><span data-stu-id="e3964-108">Poll responses</span></span>
* <span data-ttu-id="e3964-109">Notificaciones de eventos externos</span><span class="sxs-lookup"><span data-stu-id="e3964-109">External event notifications</span></span>

<span data-ttu-id="e3964-110">El envío de un mensaje para iniciar una nueva conversación es diferente al de enviar un mensaje en respuesta a una conversación existente: cuando el bot inicia una nueva conversación, no hay ninguna conversación preexistente para publicar el mensaje en.</span><span class="sxs-lookup"><span data-stu-id="e3964-110">Sending a message to start a new conversation thread is different than sending a message in response to an existing conversation: when your bot starts a new a conversation, there is no pre-existing conversation to post the message to.</span></span> <span data-ttu-id="e3964-111">Para poder enviar un mensaje proactivo debe:</span><span class="sxs-lookup"><span data-stu-id="e3964-111">In order to send a proactive message you need to:</span></span>

1. [<span data-ttu-id="e3964-112">Decide qué vas a decir</span><span class="sxs-lookup"><span data-stu-id="e3964-112">Decide what you're going to say</span></span>](#best-practices-for-proactive-messaging)
1. [<span data-ttu-id="e3964-113">Obtener el identificador único del usuario y el identificador de inquilino</span><span class="sxs-lookup"><span data-stu-id="e3964-113">Obtain the user's unique Id and tenant Id</span></span>](#obtain-necessary-user-information)
1. [<span data-ttu-id="e3964-114">Enviar el mensaje</span><span class="sxs-lookup"><span data-stu-id="e3964-114">Send the message</span></span>](#examples)

<span data-ttu-id="e3964-115">Al crear mensajes proactivos \*\*\*\* a los `MicrosoftAppCredentials.TrustServiceUrl`que se debe llamar y pasar la dirección URL del `ConnectorClient` servicio antes de crear el, se usará para enviar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="e3964-115">When creating proactive messages you **must** call `MicrosoftAppCredentials.TrustServiceUrl`, and pass in the service URL before creating the `ConnectorClient` you will use to send the message.</span></span> <span data-ttu-id="e3964-116">Si no lo hace, la aplicación recibirá una `401: Unauthorized` respuesta.</span><span class="sxs-lookup"><span data-stu-id="e3964-116">If you do not, your app will receive a `401: Unauthorized` response.</span></span> <span data-ttu-id="e3964-117">Vea [los ejemplos siguientes](#net-example-from-this-sample).</span><span class="sxs-lookup"><span data-stu-id="e3964-117">See [the samples below](#net-example-from-this-sample).</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="e3964-118">Procedimientos recomendados para la mensajería proactiva</span><span class="sxs-lookup"><span data-stu-id="e3964-118">Best practices for proactive messaging</span></span>

<span data-ttu-id="e3964-119">El envío de mensajes proactivos a los usuarios puede ser una forma muy eficaz de comunicarse con los usuarios.</span><span class="sxs-lookup"><span data-stu-id="e3964-119">Sending proactive messages to users can be a very effective way to communicate with your users.</span></span> <span data-ttu-id="e3964-120">Sin embargo, desde su perspectiva puede parecer que este mensaje no se solicita completamente y, en el caso de los mensajes de bienvenida, será la primera vez que interactuen con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e3964-120">However, from their perspective this message can appear to come to them completely unprompted, and in the case of welcome messages will be the first time they've interacted with your app.</span></span> <span data-ttu-id="e3964-121">Por lo tanto, es muy importante usar esta funcionalidad con moderación (no enviar correo no deseado a los usuarios) y proporcionarle la información suficiente para que puedan comprender por qué se les está enviando un mensaje.</span><span class="sxs-lookup"><span data-stu-id="e3964-121">As such, it is very important to use this functionality sparingly (don't spam your users), and to provide them with enough information to let them understand why they are being messaged.</span></span>

<span data-ttu-id="e3964-122">Generalmente, los mensajes proactivos se dividen en dos categorías, mensajes de bienvenida o notificaciones.</span><span class="sxs-lookup"><span data-stu-id="e3964-122">Proactive messages generally fall into one of two categories, welcome messages or notifications.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="e3964-123">Mensajes de bienvenida</span><span class="sxs-lookup"><span data-stu-id="e3964-123">Welcome messages</span></span>

<span data-ttu-id="e3964-124">Al usar la mensajería proactiva para enviar un mensaje de bienvenida a un usuario, debe tener en cuenta que para la mayoría de las personas que reciben el mensaje no tendrán contexto por el motivo por el que lo reciben.</span><span class="sxs-lookup"><span data-stu-id="e3964-124">When using proactive messaging to send a welcome message to a user you must keep in mind that for most people receiving the message they will have no context for why they are receiving it.</span></span> <span data-ttu-id="e3964-125">También es la primera vez que interactuarán con la aplicación; es su oportunidad para crear una buena primera impresión.</span><span class="sxs-lookup"><span data-stu-id="e3964-125">This is also the first time they will have interacted with your app; it is your opportunity to create a good first impression.</span></span> <span data-ttu-id="e3964-126">Los mejores mensajes de bienvenida incluirán:</span><span class="sxs-lookup"><span data-stu-id="e3964-126">The best welcome messages will include:</span></span>

* <span data-ttu-id="e3964-127">**¿Por qué reciben este mensaje?**</span><span class="sxs-lookup"><span data-stu-id="e3964-127">**Why are they receiving this message.**</span></span> <span data-ttu-id="e3964-128">El usuario debe ser muy claro por qué reciben el mensaje.</span><span class="sxs-lookup"><span data-stu-id="e3964-128">It should be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="e3964-129">Si el bot se ha instalado en un canal y se ha enviado un mensaje de bienvenida a todos los usuarios, hágales saber en qué canal se ha instalado y que podrían instalarlo.</span><span class="sxs-lookup"><span data-stu-id="e3964-129">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="e3964-130">**Qué ofrece.**</span><span class="sxs-lookup"><span data-stu-id="e3964-130">**What do you offer.**</span></span> <span data-ttu-id="e3964-131">¿Qué puede hacer con la aplicación?</span><span class="sxs-lookup"><span data-stu-id="e3964-131">What can they do with your app?</span></span> <span data-ttu-id="e3964-132">¿Qué valor puede aportar a ellos?</span><span class="sxs-lookup"><span data-stu-id="e3964-132">What value can you bring to them?</span></span>
* <span data-ttu-id="e3964-133">**Qué debería hacer a continuación.**</span><span class="sxs-lookup"><span data-stu-id="e3964-133">**What should they do next.**</span></span> <span data-ttu-id="e3964-134">Invitar a probar un comando o interactuar con la aplicación de alguna manera.</span><span class="sxs-lookup"><span data-stu-id="e3964-134">Invite them to try out a command, or interact with your app in some way.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="e3964-135">Mensajes de notificación</span><span class="sxs-lookup"><span data-stu-id="e3964-135">Notification messages</span></span>

<span data-ttu-id="e3964-136">Al usar la mensajería proactiva para enviar notificaciones, debe asegurarse de que los usuarios tienen una ruta de acceso clara para emprender acciones comunes en función de la notificación y un conocimiento claro de la razón por la que se produjo la notificación.</span><span class="sxs-lookup"><span data-stu-id="e3964-136">When using proactive messaging to send notifications you need to make sure your users have a clear path to take common actions based on your notification, and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="e3964-137">Por lo general, los mensajes de notificación son correctos:</span><span class="sxs-lookup"><span data-stu-id="e3964-137">Good notification messages will generally include:</span></span>

* <span data-ttu-id="e3964-138">**Qué ha pasado.**</span><span class="sxs-lookup"><span data-stu-id="e3964-138">**What happened.**</span></span> <span data-ttu-id="e3964-139">Una indicación clara de lo que ha sucedido para provocar la notificación.</span><span class="sxs-lookup"><span data-stu-id="e3964-139">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="e3964-140">**Qué ocurrió.**</span><span class="sxs-lookup"><span data-stu-id="e3964-140">**What it happened to.**</span></span> <span data-ttu-id="e3964-141">Debe estar claro qué elemento/Thing se actualizó para provocar la notificación.</span><span class="sxs-lookup"><span data-stu-id="e3964-141">It should be clear what item/thing was updated to cause the notification.</span></span>
* <span data-ttu-id="e3964-142">**Quién lo llevó a cabo.**</span><span class="sxs-lookup"><span data-stu-id="e3964-142">**Who did it.**</span></span> <span data-ttu-id="e3964-143">Quién llevó a cabo la acción que hizo que se enviara la notificación.</span><span class="sxs-lookup"><span data-stu-id="e3964-143">Who took the action that caused the notification to be sent.</span></span>
* <span data-ttu-id="e3964-144">**Qué pueden hacer al respecto.**</span><span class="sxs-lookup"><span data-stu-id="e3964-144">**What they can do about it.**</span></span> <span data-ttu-id="e3964-145">Facilite a los usuarios que realicen acciones basadas en las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="e3964-145">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="e3964-146">**Cómo se pueden dejar de participar.** Debe proporcionar una ruta de acceso para que los usuarios puedan optar por las notificaciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="e3964-146">**How they can opt out.** You need to provide a path for users to opt out of additional notifications.</span></span>

## <a name="obtain-necessary-user-information"></a><span data-ttu-id="e3964-147">Obtener información de usuario necesaria</span><span class="sxs-lookup"><span data-stu-id="e3964-147">Obtain necessary user information</span></span>

<span data-ttu-id="e3964-148">Los bots pueden crear nuevas conversaciones con un usuario individual de Microsoft Teams obteniendo el *identificador único* del usuario y el *identificador de inquilino.*</span><span class="sxs-lookup"><span data-stu-id="e3964-148">Bots can create new conversations with an individual Microsoft Teams user by obtaining the user’s *unique ID* and *tenant ID.*</span></span> <span data-ttu-id="e3964-149">Puede obtener estos valores mediante uno de los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e3964-149">You can obtain these values using one of the following methods:</span></span>

* <span data-ttu-id="e3964-150">Mediante [la recopilación de la lista de equipos](~/resources/bot-v3/bots-context.md#fetching-the-team-roster) desde un canal en el que está instalada la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e3964-150">By [fetching the team roster](~/resources/bot-v3/bots-context.md#fetching-the-team-roster) from a channel your app is installed in.</span></span>
* <span data-ttu-id="e3964-151">Mediante el almacenamiento en la memoria caché cuando un usuario [interactúa con el bot en un canal](~/resources/bot-v3/bot-conversations/bots-conv-channel.md).</span><span class="sxs-lookup"><span data-stu-id="e3964-151">By caching them when a user [interacts with your bot in a channel](~/resources/bot-v3/bot-conversations/bots-conv-channel.md).</span></span>
* <span data-ttu-id="e3964-152">Cuando se @mentioned a un usuario [en una conversación de canal](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) a la que pertenece el bot.</span><span class="sxs-lookup"><span data-stu-id="e3964-152">When a users is [@mentioned in a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) the bot is a part of.</span></span>
* <span data-ttu-id="e3964-153">Al almacenarlos en la memoria caché cuando [recibe el `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) evento cuando la aplicación está instalada en un ámbito personal o se agregan nuevos miembros a un canal o chat de grupo que</span><span class="sxs-lookup"><span data-stu-id="e3964-153">By caching them when you [receive the `conversationUpdate`](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) event when your app is installed in a personal scope, or new members are added to a channel or group chat that</span></span>

### <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="e3964-154">Instalar de forma proactiva la aplicación con Graph</span><span class="sxs-lookup"><span data-stu-id="e3964-154">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="e3964-155">La instalación de aplicaciones de forma proactiva con Graph se encuentra actualmente en versión beta.</span><span class="sxs-lookup"><span data-stu-id="e3964-155">Proactively installing apps using graph is currently in beta.</span></span>

<span data-ttu-id="e3964-156">En ocasiones, es posible que sea necesario enviar un mensaje de forma proactiva a los usuarios que no hayan instalado ni interactúen con la aplicación anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e3964-156">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="e3964-157">Por ejemplo, desea usar el Communicator de la [compañía](~/samples/app-templates.md#company-communicator) para enviar mensajes a toda la organización.</span><span class="sxs-lookup"><span data-stu-id="e3964-157">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="e3964-158">Para este escenario, puede usar la API de Graph para instalar proactivamente la aplicación para sus usuarios y, a continuación, almacenar en `conversationUpdate` caché los valores necesarios del evento que la aplicación recibirá en el momento de la instalación.</span><span class="sxs-lookup"><span data-stu-id="e3964-158">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app will receive upon install.</span></span>

<span data-ttu-id="e3964-159">Solo puede instalar aplicaciones que estén en el catálogo de aplicaciones de la organización o en la tienda de aplicaciones de Teams.</span><span class="sxs-lookup"><span data-stu-id="e3964-159">You can only install apps that are in your organizational app catalogue, or the Teams app store.</span></span>

<span data-ttu-id="e3964-160">Consulte [install apps for users](/graph/teams-proactive-messaging) en la documentación de Graph para obtener detalles completos.</span><span class="sxs-lookup"><span data-stu-id="e3964-160">See [Install apps for users](/graph/teams-proactive-messaging) in the Graph documentation for complete details.</span></span> <span data-ttu-id="e3964-161">También hay un [ejemplo en .net](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span><span class="sxs-lookup"><span data-stu-id="e3964-161">There is also a [sample in .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span></span>

## <a name="examples"></a><span data-ttu-id="e3964-162">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="e3964-162">Examples</span></span>

<span data-ttu-id="e3964-163">Asegúrese de autenticar y de tener un token de portador antes de crear una nueva conversación mediante la API de REST.</span><span class="sxs-lookup"><span data-stu-id="e3964-163">Be sure that you authenticate and have a bearer token before creating a new conversation using the REST API.</span></span>

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

<span data-ttu-id="e3964-164">Debe proporcionar el identificador de usuario y el identificador de inquilino.</span><span class="sxs-lookup"><span data-stu-id="e3964-164">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="e3964-165">Si la llamada se realiza correctamente, la API devuelve el siguiente objeto de respuesta.</span><span class="sxs-lookup"><span data-stu-id="e3964-165">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

<span data-ttu-id="e3964-166">Este identificador es el identificador de conversación único de chat personal.</span><span class="sxs-lookup"><span data-stu-id="e3964-166">This ID is the personal chat's unique conversation ID.</span></span> <span data-ttu-id="e3964-167">Almacene este valor y vuelva a usarlo para interacciones futuras con el usuario.</span><span class="sxs-lookup"><span data-stu-id="e3964-167">Please store this value and reuse it for future interactions with the user.</span></span>

### <a name="using-net"></a><span data-ttu-id="e3964-168">Uso de .NET</span><span class="sxs-lookup"><span data-stu-id="e3964-168">Using .NET</span></span>

<span data-ttu-id="e3964-169">En este ejemplo se usa el paquete NuGet [Microsoft. bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) .</span><span class="sxs-lookup"><span data-stu-id="e3964-169">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

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

### <a name="using-nodejs"></a><span data-ttu-id="e3964-170">Uso de node. js</span><span class="sxs-lookup"><span data-stu-id="e3964-170">Using Node.js</span></span>

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

<span data-ttu-id="e3964-171">*Vea también* [ejemplos del marco de bot](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="e3964-171">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="creating-a-channel-conversation"></a><span data-ttu-id="e3964-172">Crear una conversación de canal</span><span class="sxs-lookup"><span data-stu-id="e3964-172">Creating a channel conversation</span></span>

<span data-ttu-id="e3964-173">El bot agregado por el equipo puede exponer en un canal para crear una nueva cadena de respuesta.</span><span class="sxs-lookup"><span data-stu-id="e3964-173">Your team-added bot can post into a channel to create a new reply chain.</span></span> <span data-ttu-id="e3964-174">Si usa el SDK de Team. js Teams, use `startReplyChain()` que le proporcione una dirección completa con el identificador de actividad y el identificador de conversación correctos. Si usa C#, vea el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="e3964-174">If you're using the Node.js Teams SDK, use `startReplyChain()` which gives you a fully-populated address with the correct activity id and conversation id. If you are using C#, see the example below.</span></span>

<span data-ttu-id="e3964-175">Como alternativa, puede usar la API de REST y enviar una solicitud POST al [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) recurso.</span><span class="sxs-lookup"><span data-stu-id="e3964-175">Alternatively, you can use the REST API and issue a POST request to [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) resource.</span></span>

### <a name="net-example-from-this-sample"></a><span data-ttu-id="e3964-176">Ejemplo de .NET (de [este ejemplo](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs))</span><span class="sxs-lookup"><span data-stu-id="e3964-176">.NET example (from [this sample](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs))</span></span>

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

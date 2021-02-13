---
title: Mensajes proactivos
description: Describe los bots que pueden iniciar una conversación en Microsoft Teams
keywords: 'Escenarios de teams: bot de conversación de mensajería proactiva'
ms.openlocfilehash: 8c93696f79b5d99c32162a7374c7d9adccacb984
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231627"
---
# <a name="proactive-messaging-for-bots"></a><span data-ttu-id="3e154-104">Mensajería proactiva para bots</span><span class="sxs-lookup"><span data-stu-id="3e154-104">Proactive messaging for bots</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="3e154-105">Un mensaje proactivo es un mensaje enviado por un bot para iniciar una conversación.</span><span class="sxs-lookup"><span data-stu-id="3e154-105">A proactive message is a message that is sent by a bot to start a conversation.</span></span> <span data-ttu-id="3e154-106">Es posible que desee que el bot inicie una conversación por varios motivos, entre los que se incluyen:</span><span class="sxs-lookup"><span data-stu-id="3e154-106">You may want your bot to start a conversation for a number of reasons, including:</span></span>

* <span data-ttu-id="3e154-107">Mensajes de bienvenida para conversaciones de bots personales</span><span class="sxs-lookup"><span data-stu-id="3e154-107">Welcome messages for personal bot conversations</span></span>
* <span data-ttu-id="3e154-108">Respuestas de sondeo</span><span class="sxs-lookup"><span data-stu-id="3e154-108">Poll responses</span></span>
* <span data-ttu-id="3e154-109">Notificaciones de eventos externos</span><span class="sxs-lookup"><span data-stu-id="3e154-109">External event notifications</span></span>

<span data-ttu-id="3e154-110">El envío de un mensaje para iniciar un nuevo hilo de conversación es diferente al envío de un mensaje en respuesta a una conversación existente: cuando el bot inicia una nueva conversación, no hay ninguna conversación preexistida en la que publicar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="3e154-110">Sending a message to start a new conversation thread is different than sending a message in response to an existing conversation: when your bot starts a new a conversation, there is no pre-existing conversation to post the message to.</span></span> <span data-ttu-id="3e154-111">Para enviar un mensaje proactivo, necesita:</span><span class="sxs-lookup"><span data-stu-id="3e154-111">In order to send a proactive message you need to:</span></span>

1. [<span data-ttu-id="3e154-112">Decide lo que vas a decir</span><span class="sxs-lookup"><span data-stu-id="3e154-112">Decide what you're going to say</span></span>](#best-practices-for-proactive-messaging)
1. [<span data-ttu-id="3e154-113">Obtener el identificador único del usuario y el id. de espacio empresarial</span><span class="sxs-lookup"><span data-stu-id="3e154-113">Obtain the user's unique Id and tenant Id</span></span>](#obtain-necessary-user-information)
1. [<span data-ttu-id="3e154-114">Enviar el mensaje</span><span class="sxs-lookup"><span data-stu-id="3e154-114">Send the message</span></span>](#examples)

<span data-ttu-id="3e154-115">Al crear mensajes proactivos, **debe** llamar y pasar la dirección URL del servicio antes de crear la que `MicrosoftAppCredentials.TrustServiceUrl` usará para enviar el `ConnectorClient` mensaje.</span><span class="sxs-lookup"><span data-stu-id="3e154-115">When creating proactive messages you **must** call `MicrosoftAppCredentials.TrustServiceUrl`, and pass in the service URL before creating the `ConnectorClient` you will use to send the message.</span></span> <span data-ttu-id="3e154-116">Si no lo haces, la aplicación recibirá una `401: Unauthorized` respuesta.</span><span class="sxs-lookup"><span data-stu-id="3e154-116">If you do not, your app will receive a `401: Unauthorized` response.</span></span> <span data-ttu-id="3e154-117">Vea [los ejemplos siguientes.](#net-example-from-this-sample)</span><span class="sxs-lookup"><span data-stu-id="3e154-117">See [the samples below](#net-example-from-this-sample).</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="3e154-118">Procedimientos recomendados para mensajería proactiva</span><span class="sxs-lookup"><span data-stu-id="3e154-118">Best practices for proactive messaging</span></span>

<span data-ttu-id="3e154-119">Enviar mensajes proactivos a los usuarios puede ser una forma muy eficaz de comunicarse con los usuarios.</span><span class="sxs-lookup"><span data-stu-id="3e154-119">Sending proactive messages to users can be a very effective way to communicate with your users.</span></span> <span data-ttu-id="3e154-120">Sin embargo, desde su perspectiva, puede parecer que este mensaje no se muestra correctamente y, en el caso de los mensajes de bienvenida, será la primera vez que interactúen con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e154-120">However, from their perspective this message can appear to come to them completely unprompted, and in the case of welcome messages will be the first time they've interacted with your app.</span></span> <span data-ttu-id="3e154-121">Por lo tanto, es muy importante usar esta funcionalidad con moderación (no enviar correo no deseado a los usuarios) y proporcionarles información suficiente para que comprendan por qué se les envía un mensaje.</span><span class="sxs-lookup"><span data-stu-id="3e154-121">As such, it is very important to use this functionality sparingly (don't spam your users), and to provide them with enough information to let them understand why they are being messaged.</span></span>

<span data-ttu-id="3e154-122">Los mensajes proactivos suelen estar en una de dos categorías: mensajes de bienvenida o notificaciones.</span><span class="sxs-lookup"><span data-stu-id="3e154-122">Proactive messages generally fall into one of two categories, welcome messages or notifications.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="3e154-123">Mensajes de bienvenida</span><span class="sxs-lookup"><span data-stu-id="3e154-123">Welcome messages</span></span>

<span data-ttu-id="3e154-124">Al usar la mensajería proactiva para enviar un mensaje de bienvenida a un usuario, debe tener en cuenta que para la mayoría de las personas que reciben el mensaje no tendrán contexto de por qué lo reciben.</span><span class="sxs-lookup"><span data-stu-id="3e154-124">When using proactive messaging to send a welcome message to a user you must keep in mind that for most people receiving the message they will have no context for why they are receiving it.</span></span> <span data-ttu-id="3e154-125">Esta también es la primera vez que interactuarán con la aplicación; es su oportunidad de crear una buena primera impresión.</span><span class="sxs-lookup"><span data-stu-id="3e154-125">This is also the first time they will have interacted with your app; it is your opportunity to create a good first impression.</span></span> <span data-ttu-id="3e154-126">Entre los mensajes de bienvenida más importantes se incluyen:</span><span class="sxs-lookup"><span data-stu-id="3e154-126">The best welcome messages will include:</span></span>

* <span data-ttu-id="3e154-127">**¿Por qué reciben este mensaje?**</span><span class="sxs-lookup"><span data-stu-id="3e154-127">**Why are they receiving this message.**</span></span> <span data-ttu-id="3e154-128">Debe ser muy claro para el usuario por qué está recibiendo el mensaje.</span><span class="sxs-lookup"><span data-stu-id="3e154-128">It should be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="3e154-129">Si el bot se instaló en un canal y envió un mensaje de bienvenida a todos los usuarios, indálles en qué canal se instaló y quién lo instaló.</span><span class="sxs-lookup"><span data-stu-id="3e154-129">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="3e154-130">**¿Qué ofrece?**</span><span class="sxs-lookup"><span data-stu-id="3e154-130">**What do you offer.**</span></span> <span data-ttu-id="3e154-131">¿Qué pueden hacer con la aplicación?</span><span class="sxs-lookup"><span data-stu-id="3e154-131">What can they do with your app?</span></span> <span data-ttu-id="3e154-132">¿Qué valor puede aportarles?</span><span class="sxs-lookup"><span data-stu-id="3e154-132">What value can you bring to them?</span></span>
* <span data-ttu-id="3e154-133">**Qué deben hacer a continuación.**</span><span class="sxs-lookup"><span data-stu-id="3e154-133">**What should they do next.**</span></span> <span data-ttu-id="3e154-134">Invítelos a probar un comando o interactuar con la aplicación de alguna manera.</span><span class="sxs-lookup"><span data-stu-id="3e154-134">Invite them to try out a command, or interact with your app in some way.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="3e154-135">Mensajes de notificación</span><span class="sxs-lookup"><span data-stu-id="3e154-135">Notification messages</span></span>

<span data-ttu-id="3e154-136">Al usar la mensajería proactiva para enviar notificaciones, debe asegurarse de que los usuarios tienen una ruta clara para realizar acciones comunes basadas en la notificación y una comprensión clara de por qué se produjo la notificación.</span><span class="sxs-lookup"><span data-stu-id="3e154-136">When using proactive messaging to send notifications you need to make sure your users have a clear path to take common actions based on your notification, and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="3e154-137">Por lo general, los mensajes de notificación de buena calidad incluyen:</span><span class="sxs-lookup"><span data-stu-id="3e154-137">Good notification messages will generally include:</span></span>

* <span data-ttu-id="3e154-138">**Qué ha pasado.**</span><span class="sxs-lookup"><span data-stu-id="3e154-138">**What happened.**</span></span> <span data-ttu-id="3e154-139">Una indicación clara de lo que ocurrió para provocar la notificación.</span><span class="sxs-lookup"><span data-stu-id="3e154-139">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="3e154-140">**Qué ha ocurrido.**</span><span class="sxs-lookup"><span data-stu-id="3e154-140">**What it happened to.**</span></span> <span data-ttu-id="3e154-141">Debe estar claro qué elemento o elemento se actualizó para provocar la notificación.</span><span class="sxs-lookup"><span data-stu-id="3e154-141">It should be clear what item/thing was updated to cause the notification.</span></span>
* <span data-ttu-id="3e154-142">**Quién lo hizo.**</span><span class="sxs-lookup"><span data-stu-id="3e154-142">**Who did it.**</span></span> <span data-ttu-id="3e154-143">Quién realizó la acción que provocó el envío de la notificación.</span><span class="sxs-lookup"><span data-stu-id="3e154-143">Who took the action that caused the notification to be sent.</span></span>
* <span data-ttu-id="3e154-144">**Lo que pueden hacer al respecto.**</span><span class="sxs-lookup"><span data-stu-id="3e154-144">**What they can do about it.**</span></span> <span data-ttu-id="3e154-145">Facilita a los usuarios la realización de acciones en función de las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="3e154-145">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="3e154-146">**Cómo pueden optar por no participar.** Debes proporcionar una ruta de acceso para que los usuarios puedan optar por no recibir notificaciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="3e154-146">**How they can opt out.** You need to provide a path for users to opt out of additional notifications.</span></span>

## <a name="obtain-necessary-user-information"></a><span data-ttu-id="3e154-147">Obtener la información de usuario necesaria</span><span class="sxs-lookup"><span data-stu-id="3e154-147">Obtain necessary user information</span></span>

<span data-ttu-id="3e154-148">Los bots pueden crear nuevas conversaciones con un usuario individual de Microsoft Teams mediante la obtención del identificador único del usuario y *del* *inquilino.*</span><span class="sxs-lookup"><span data-stu-id="3e154-148">Bots can create new conversations with an individual Microsoft Teams user by obtaining the user's *unique ID* and *tenant ID.*</span></span> <span data-ttu-id="3e154-149">Puede obtener estos valores mediante uno de los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3e154-149">You can obtain these values using one of the following methods:</span></span>

* <span data-ttu-id="3e154-150">Mediante [la obtención de la lista de equipo](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) desde un canal en el que está instalada la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e154-150">By [fetching the team roster](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) from a channel your app is installed in.</span></span>
* <span data-ttu-id="3e154-151">Al almacenarlos en caché cuando un usuario [interactúa con el bot en un canal.](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)</span><span class="sxs-lookup"><span data-stu-id="3e154-151">By caching them when a user [interacts with your bot in a channel](~/resources/bot-v3/bot-conversations/bots-conv-channel.md).</span></span>
* <span data-ttu-id="3e154-152">Cuando un usuario está [@mentioned en una conversación de canal](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) de la que forma parte el bot.</span><span class="sxs-lookup"><span data-stu-id="3e154-152">When a users is [@mentioned in a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) the bot is a part of.</span></span>
* <span data-ttu-id="3e154-153">Al almacenarlos en [ `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) caché cuando recibe el evento cuando la aplicación está instalada en un ámbito personal, o cuando se agregan nuevos miembros a un canal o chat de grupo que</span><span class="sxs-lookup"><span data-stu-id="3e154-153">By caching them when you [receive the `conversationUpdate`](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) event when your app is installed in a personal scope, or new members are added to a channel or group chat that</span></span>

### <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="3e154-154">Instalar de forma proactiva la aplicación con Graph</span><span class="sxs-lookup"><span data-stu-id="3e154-154">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="3e154-155">La instalación proactiva de aplicaciones con graph se encuentra actualmente en la versión beta.</span><span class="sxs-lookup"><span data-stu-id="3e154-155">Proactively installing apps using graph is currently in beta.</span></span>

<span data-ttu-id="3e154-156">En ocasiones, puede que sea necesario enviar mensajes de forma proactiva a los usuarios que no han instalado o interactuado con la aplicación anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3e154-156">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="3e154-157">Por ejemplo, desea usar el comunicador de la empresa [para](~/samples/app-templates.md#company-communicator) enviar mensajes a toda la organización.</span><span class="sxs-lookup"><span data-stu-id="3e154-157">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="3e154-158">Para este escenario, puede usar la API de Graph para instalar de forma proactiva la aplicación para los usuarios y, a continuación, almacenar en caché los valores necesarios del evento que la aplicación recibirá al `conversationUpdate` instalarse.</span><span class="sxs-lookup"><span data-stu-id="3e154-158">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app will receive upon install.</span></span>

<span data-ttu-id="3e154-159">Solo puede instalar aplicaciones que se encuentran en el catálogo de aplicaciones de su organización o en la tienda de aplicaciones de Teams.</span><span class="sxs-lookup"><span data-stu-id="3e154-159">You can only install apps that are in your organizational app catalogue, or the Teams app store.</span></span>

<span data-ttu-id="3e154-160">Consulte [Instalar aplicaciones para usuarios en](/graph/teams-proactive-messaging) la documentación de Graph para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="3e154-160">See [Install apps for users](/graph/teams-proactive-messaging) in the Graph documentation for complete details.</span></span> <span data-ttu-id="3e154-161">También hay un [ejemplo en .NET.](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)</span><span class="sxs-lookup"><span data-stu-id="3e154-161">There is also a [sample in .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span></span>

## <a name="examples"></a><span data-ttu-id="3e154-162">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="3e154-162">Examples</span></span>

<span data-ttu-id="3e154-163">Asegúrese de autenticarse y tener un token de portador antes de crear una nueva conversación con la API de REST.</span><span class="sxs-lookup"><span data-stu-id="3e154-163">Be sure that you authenticate and have a bearer token before creating a new conversation using the REST API.</span></span>

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

<span data-ttu-id="3e154-164">Debe proporcionar el id. de usuario y el id. de inquilino.</span><span class="sxs-lookup"><span data-stu-id="3e154-164">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="3e154-165">Si la llamada se realiza correctamente, la API devuelve el siguiente objeto de respuesta.</span><span class="sxs-lookup"><span data-stu-id="3e154-165">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

<span data-ttu-id="3e154-166">Este identificador es el identificador de conversación único del chat personal.</span><span class="sxs-lookup"><span data-stu-id="3e154-166">This ID is the personal chat's unique conversation ID.</span></span> <span data-ttu-id="3e154-167">Almacene este valor y reutilice para futuras interacciones con el usuario.</span><span class="sxs-lookup"><span data-stu-id="3e154-167">Please store this value and reuse it for future interactions with the user.</span></span>

### <a name="using-net"></a><span data-ttu-id="3e154-168">Uso de .NET</span><span class="sxs-lookup"><span data-stu-id="3e154-168">Using .NET</span></span>

<span data-ttu-id="3e154-169">En este ejemplo se usa [el paquete NuGet Microsoft.Bot.Connector.Teams.](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)</span><span class="sxs-lookup"><span data-stu-id="3e154-169">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

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

### <a name="using-nodejs"></a><span data-ttu-id="3e154-170">Uso de Node.js</span><span class="sxs-lookup"><span data-stu-id="3e154-170">Using Node.js</span></span>

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

<span data-ttu-id="3e154-171">*Vea también ejemplos* [de Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)</span><span class="sxs-lookup"><span data-stu-id="3e154-171">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="creating-a-channel-conversation"></a><span data-ttu-id="3e154-172">Creación de una conversación de canal</span><span class="sxs-lookup"><span data-stu-id="3e154-172">Creating a channel conversation</span></span>

<span data-ttu-id="3e154-173">El bot agregado por el equipo puede publicar en un canal para crear una nueva cadena de respuesta.</span><span class="sxs-lookup"><span data-stu-id="3e154-173">Your team-added bot can post into a channel to create a new reply chain.</span></span> <span data-ttu-id="3e154-174">Si usa el SDK de Node.js Teams, use el que le proporciona una dirección completa con el identificador de actividad y el identificador de `startReplyChain()` conversación correctos. Si usa C#, vea el siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3e154-174">If you're using the Node.js Teams SDK, use `startReplyChain()` which gives you a fully-populated address with the correct activity id and conversation id. If you are using C#, see the example below.</span></span>

<span data-ttu-id="3e154-175">Como alternativa, puede usar la API de REST y emitir una solicitud POST al [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) recurso.</span><span class="sxs-lookup"><span data-stu-id="3e154-175">Alternatively, you can use the REST API and issue a POST request to [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) resource.</span></span>

### <a name="net-example-from-this-sample"></a><span data-ttu-id="3e154-176">Ejemplo de .NET (de [este ejemplo)](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)</span><span class="sxs-lookup"><span data-stu-id="3e154-176">.NET example (from [this sample](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs))</span></span>

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

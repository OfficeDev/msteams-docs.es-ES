---
title: Controlar eventos de bots
description: Describe cómo controlar eventos en bots para Microsoft Teams
keywords: equipos bots eventos
ms.date: 05/20/2019
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: da624ea0e92e193f4ad7f334d958349d542dd6e0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566470"
---
# <a name="handle-bot-events-in-microsoft-teams"></a><span data-ttu-id="e78b8-104">Controlar eventos de bots en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e78b8-104">Handle bot events in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="e78b8-105">Microsoft Teams envía notificaciones al bot para los cambios o eventos que se producen en ámbitos donde el bot está activo.</span><span class="sxs-lookup"><span data-stu-id="e78b8-105">Microsoft Teams sends notifications to your bot for changes or events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="e78b8-106">Puede usar estos eventos para desencadenar la lógica de servicio, como los siguientes:</span><span class="sxs-lookup"><span data-stu-id="e78b8-106">You can use these events to trigger service logic, such as the following:</span></span>

* <span data-ttu-id="e78b8-107">Active un mensaje de bienvenida cuando se agregue el bot a un equipo.</span><span class="sxs-lookup"><span data-stu-id="e78b8-107">Trigger a welcome message when your bot is added to a team.</span></span>
* <span data-ttu-id="e78b8-108">Consulta y almacena en caché la información del grupo cuando el bot se agrega a un chat de grupo.</span><span class="sxs-lookup"><span data-stu-id="e78b8-108">Query and cache group information when the bot is added to a group chat.</span></span>
* <span data-ttu-id="e78b8-109">Actualice la información almacenada en caché sobre la pertenencia al equipo o la información del canal.</span><span class="sxs-lookup"><span data-stu-id="e78b8-109">Update cached information on team membership or channel information.</span></span>
* <span data-ttu-id="e78b8-110">Quite la información almacenada en caché para un equipo si se quita el bot.</span><span class="sxs-lookup"><span data-stu-id="e78b8-110">Remove cached information for a team if the bot is removed.</span></span>
* <span data-ttu-id="e78b8-111">Cuando un usuario gusta un mensaje de bot.</span><span class="sxs-lookup"><span data-stu-id="e78b8-111">When a bot message is liked by a user.</span></span>

<span data-ttu-id="e78b8-112">Cada evento bot se envía como un `Activity` objeto en el que se define qué información hay en el `messageType` objeto.</span><span class="sxs-lookup"><span data-stu-id="e78b8-112">Each bot event is sent as an `Activity` object in which `messageType` defines what information is in the object.</span></span> <span data-ttu-id="e78b8-113">Para ver los mensajes de tipo `message` , consulte Envío y recepción de [mensajes](~/resources/bot-v3/bot-conversations/bots-conversations.md).</span><span class="sxs-lookup"><span data-stu-id="e78b8-113">For messages of type `message`, see [Sending and receiving messages](~/resources/bot-v3/bot-conversations/bots-conversations.md).</span></span>

<span data-ttu-id="e78b8-114">Teams y eventos de grupo, normalmente desencadenados del `conversationUpdate` tipo, tienen información adicional Teams eventos pasadas como parte del objeto y, por lo tanto, el controlador de `channelData` eventos debe consultar la carga para los metadatos Teams y específicos de eventos `channelData` `eventType` adicionales.</span><span class="sxs-lookup"><span data-stu-id="e78b8-114">Teams and group events, usually triggered off the `conversationUpdate` type, have additional Teams event information passed as part of the `channelData` object, and therefore your event handler must query the `channelData` payload for the Teams `eventType` and additional event-specific metadata.</span></span>

<span data-ttu-id="e78b8-115">En la tabla siguiente se enumeran los eventos que el bot puede recibir y realizar.</span><span class="sxs-lookup"><span data-stu-id="e78b8-115">The following table lists the events that your bot can receive and take action on.</span></span>

|<span data-ttu-id="e78b8-116">Tipo</span><span class="sxs-lookup"><span data-stu-id="e78b8-116">Type</span></span>|<span data-ttu-id="e78b8-117">Objeto de carga útil</span><span class="sxs-lookup"><span data-stu-id="e78b8-117">Payload object</span></span>|<span data-ttu-id="e78b8-118">Teams eventoType</span><span class="sxs-lookup"><span data-stu-id="e78b8-118">Teams eventType</span></span> |<span data-ttu-id="e78b8-119">Descripción</span><span class="sxs-lookup"><span data-stu-id="e78b8-119">Description</span></span>|<span data-ttu-id="e78b8-120">Ámbito</span><span class="sxs-lookup"><span data-stu-id="e78b8-120">Scope</span></span>|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[<span data-ttu-id="e78b8-121">Miembro añadido al equipo</span><span class="sxs-lookup"><span data-stu-id="e78b8-121">Member added to team</span></span>](#team-member-or-bot-addition)| <span data-ttu-id="e78b8-122">todo</span><span class="sxs-lookup"><span data-stu-id="e78b8-122">all</span></span> |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[<span data-ttu-id="e78b8-123">Miembro fue retirado del equipo</span><span class="sxs-lookup"><span data-stu-id="e78b8-123">Member was removed from team</span></span>](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [<span data-ttu-id="e78b8-124">Equipo fue renombrado</span><span class="sxs-lookup"><span data-stu-id="e78b8-124">Team was renamed</span></span>](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [<span data-ttu-id="e78b8-125">Se creó un canal</span><span class="sxs-lookup"><span data-stu-id="e78b8-125">A channel was created</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [<span data-ttu-id="e78b8-126">Un canal fue renombrado</span><span class="sxs-lookup"><span data-stu-id="e78b8-126">A channel was renamed</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [<span data-ttu-id="e78b8-127">Se eliminó un canal</span><span class="sxs-lookup"><span data-stu-id="e78b8-127">A channel was deleted</span></span>](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [<span data-ttu-id="e78b8-128">Reacción al mensaje del bot</span><span class="sxs-lookup"><span data-stu-id="e78b8-128">Reaction to bot message</span></span>](#reactions)| <span data-ttu-id="e78b8-129">todo</span><span class="sxs-lookup"><span data-stu-id="e78b8-129">all</span></span> |
| `messageReaction` |`reactionsRemoved`|| [<span data-ttu-id="e78b8-130">Reacción eliminada del mensaje del bot</span><span class="sxs-lookup"><span data-stu-id="e78b8-130">Reaction removed from bot message</span></span>](#reactions)| <span data-ttu-id="e78b8-131">todo</span><span class="sxs-lookup"><span data-stu-id="e78b8-131">all</span></span> |

## <a name="team-member-or-bot-addition"></a><span data-ttu-id="e78b8-132">Miembro del equipo o adición de bots</span><span class="sxs-lookup"><span data-stu-id="e78b8-132">Team member or bot addition</span></span>

<span data-ttu-id="e78b8-133">El [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true) evento se envía al bot cuando recibe información sobre las actualizaciones de pertenencia para los equipos donde se ha agregado.</span><span class="sxs-lookup"><span data-stu-id="e78b8-133">The [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true) event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="e78b8-134">También recibe una actualización cuando se ha agregado por primera vez, específicamente para conversaciones personales.</span><span class="sxs-lookup"><span data-stu-id="e78b8-134">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span> <span data-ttu-id="e78b8-135">Tenga en cuenta que la información de usuario ( `Id` ) es única para el bot y puede ser almacenada en caché para su uso futuro por el servicio, por ejemplo, el envío de un mensaje a un usuario específico.</span><span class="sxs-lookup"><span data-stu-id="e78b8-135">Note that the user information (`Id`) is unique for your bot and can be cached for future use by your service, such as, sending a message to a specific user.</span></span>

### <a name="bot-or-user-added-to-a-team"></a><span data-ttu-id="e78b8-136">Bot o usuario añadido a un equipo</span><span class="sxs-lookup"><span data-stu-id="e78b8-136">Bot or user added to a team</span></span>

<span data-ttu-id="e78b8-137">El `conversationUpdate` evento con el objeto de la carga se envía cuando se agrega un bot a un equipo o `membersAdded` se agrega un nuevo usuario a un equipo donde se ha agregado un bot.</span><span class="sxs-lookup"><span data-stu-id="e78b8-137">The `conversationUpdate` event with the `membersAdded` object in the payload is sent when either a bot is added to a team or a new user is added to a team where a bot has been added.</span></span> <span data-ttu-id="e78b8-138">Microsoft Teams también agrega `eventType.teamMemberAdded` en el `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="e78b8-138">Microsoft Teams also adds `eventType.teamMemberAdded` in the `channelData` object.</span></span>

<span data-ttu-id="e78b8-139">Dado que este evento se envía en ambos casos, debe analizar el `membersAdded` objeto para determinar si la adición era un usuario o el propio bot.</span><span class="sxs-lookup"><span data-stu-id="e78b8-139">Because this event is sent in both cases, you should parse the `membersAdded` object to determine whether the addition was a user or the bot itself.</span></span> <span data-ttu-id="e78b8-140">Para este último, una práctica recomendada es enviar un [mensaje de bienvenida](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) al canal para que los usuarios puedan comprender las características que proporciona el bot.</span><span class="sxs-lookup"><span data-stu-id="e78b8-140">For the latter, a best practice is to send a [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) to the channel so users can understand the features your bot provides.</span></span>

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a><span data-ttu-id="e78b8-141">Código de ejemplo: Comprobación de si bot era el miembro agregado</span><span class="sxs-lookup"><span data-stu-id="e78b8-141">Example code: Checking whether bot was the added member</span></span>

##### <a name="net"></a><span data-ttu-id="e78b8-142">.NET</span><span class="sxs-lookup"><span data-stu-id="e78b8-142">.NET</span></span>

```csharp
    for (int i = 0; i < sourceMessage.MembersAdded.Count; i++)
    {
        if (sourceMessage.MembersAdded[i].Id == sourceMessage.Recipient.Id)
        {
            addedBot = true;
            break;
        }
    }
```

##### <a name="nodejs"></a><span data-ttu-id="e78b8-143">Node.js</span><span class="sxs-lookup"><span data-stu-id="e78b8-143">Node.js</span></span>

```javascript
const builder = require('botbuilder');

var c = new builder.ChatConnector({appId: BOT_APP_ID, appPassword: .BOT_SECRET});
var bot = new builder.UniversalBot(c);

bot.on('conversationUpdate', (msg) => {
    var members = msg.membersAdded;
    // Loop through all members that were just added to the team
    for (var i = 0; i < members.length; i++) {

        // See if the member added was our bot
        if (members[i].id.includes(BOT_APP_ID)) {
            var botmessage = new builder.Message()
                .address(msg.address)
                .text('Hello World!');

            bot.send(botmessage, function(err) {});
        }
    }
});
```

#### <a name="schema-example-bot-added-to-team"></a><span data-ttu-id="e78b8-144">Ejemplo de esquema: Bot agregado al equipo</span><span class="sxs-lookup"><span data-stu-id="e78b8-144">Schema example: Bot added to team</span></span>

```json
{
   "membersAdded":[
      {
         "id":"28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
      }
   ],
   "type":"conversationUpdate",
   "timestamp":"2017-02-23T19:38:35.312Z",
   "localTimestamp":"2017-02-23T12:38:35.312-07:00",
   "id":"f:5f85c2ad",
   "channelId":"msteams",
   "serviceUrl":"https://smba.trafficmanager.net/amer-client-ss.msg/",
   "from":{
      "id":"29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
   },
   "conversation":{
      "isGroup":true,
      "conversationType":"channel",
      "id":"19:efa9296d959346209fea44151c742e73@thread.skype"
   },
   "recipient":{
      "id":"28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
      "name":"SongsuggesterBot"
   },
   "channelData":{
      "team":{
         "id":"19:efa9296d959346209fea44151c742e73@thread.skype"
      },
      "eventType":"teamMemberAdded",
      "tenant":{
         "id":"72f988bf-86f1-41af-91ab-2d7cd011db47"
      }
   }
}
```

### <a name="user-added-to-a-meeting"></a><span data-ttu-id="e78b8-145">Usuario añadido a una reunión</span><span class="sxs-lookup"><span data-stu-id="e78b8-145">User Added to a meeting</span></span>

<span data-ttu-id="e78b8-146">El `conversationUpdate` evento con el objeto de la carga se envía cuando se agrega un usuario a una reunión privada `membersAdded` programada.</span><span class="sxs-lookup"><span data-stu-id="e78b8-146">The `conversationUpdate` event with the `membersAdded` object in the payload is sent when a user is added to a private scheduled meeting.</span></span> <span data-ttu-id="e78b8-147">Los detalles del evento se enviarán incluso cuando los usuarios anónimos se unan a la reunión.</span><span class="sxs-lookup"><span data-stu-id="e78b8-147">The event details will be sent even when anonymous users join the meeting.</span></span> 

> [!NOTE]
>
>* <span data-ttu-id="e78b8-148">Cuando se agrega un usuario anónimo a una reunión, el objeto de carga útil membersAdded no tiene `aadObjectId` campo.</span><span class="sxs-lookup"><span data-stu-id="e78b8-148">When an anonymous user is added to a meeting, membersAdded payload object does not have `aadObjectId` field.</span></span>
>* <span data-ttu-id="e78b8-149">Cuando se agrega un usuario anónimo a una reunión, `from` el objeto de la carga siempre tiene el identificador del organizador de la reunión, incluso si otro presentador agregó al usuario anónimo.</span><span class="sxs-lookup"><span data-stu-id="e78b8-149">When an anonymous user is added to a meeting, `from` object in the payload always have the id of the meeting organizer, even if the anonymous user was added by another presenter.</span></span>

#### <a name="schema-example-user-added-to-meeting"></a><span data-ttu-id="e78b8-150">Ejemplo de esquema: Usuario agregado a la reunión</span><span class="sxs-lookup"><span data-stu-id="e78b8-150">Schema example: User added to meeting</span></span>

```json
{
   "membersAdded":[
      {
         "id":"229:1Z_XHWBMhDuehhDBYoPQD6Y1DSFsTtqOZx-SA5Jh9Y4zHKm4VbFGRn7-rK7SWiW1JECwxkMdrWpHoBut2sSyQPA"
      }
   ],
   "type":"conversationUpdate",
   "timestamp":"2017-02-23T19:38:35.312Z",
   "localTimestamp":"2020-09-29T21:11:38.6542339Z",
   "id":"f:a8cd1b51-9ddb-bd35-624b-7f7474165df8",
   "channelId":"msteams",
   "serviceUrl":"https://canary.botapi.skype.com/amer/",
   "from":{
      "id":"29:1siKxZhSoTapsXvI0gyf7Gywm_HM-4kEQW4BJnWuFYVIVu87xCNP99nidgQRCcwD3L3p_schiMShzx8IDRzf8mw",
      "aadObjectId":"f30ba569-abef-4e97-8762-35f85cbae706"
   },
   "conversation":{
      "isGroup":true,
      "tenantId":"e15762ef-a8d8-416b-871c-25516354f1fe",
      "id":"19:meeting_MWJlNGViOTgtMGExYi00NDA3LWExODgtOTZhMWNlYjM4ZTRj@thread.v2"
   },
   "recipient":{
      "id":"28:3af3604a-d4fc-486b-911e-86fab41aa91c",
      "name":"EchoBot1_Rename"
   },
   "channelData":{
      "tenant":{
         "id":"e15762ef-a8d8-416b-871c-25516354f1fe"
      },
      "source":null,
      "meeting":{
         "id":"MCMxOTptZWV0aW5nX01XSmxOR1ZpT1RndE1HRXhZaTAwTkRBM0xXRXhPRGd0T1RaaE1XTmxZak00WlRSakB0aHJlYWQudjIjMA=="
      }
   }
}

```

### <a name="bot-added-for-personal-context-only"></a><span data-ttu-id="e78b8-151">Bot añadido solo para contexto personal</span><span class="sxs-lookup"><span data-stu-id="e78b8-151">Bot added for personal context only</span></span>

<span data-ttu-id="e78b8-152">El bot recibe un `conversationUpdate` con cuando un usuario lo agrega directamente para el chat `membersAdded` personal.</span><span class="sxs-lookup"><span data-stu-id="e78b8-152">Your bot receives a `conversationUpdate` with `membersAdded` when a user adds it directly for personal chat.</span></span> <span data-ttu-id="e78b8-153">En este caso, la carga útil que recibe el bot no contiene el `channelData.team` objeto.</span><span class="sxs-lookup"><span data-stu-id="e78b8-153">In this case, the payload that your bot receives doesn't contain the `channelData.team` object.</span></span> <span data-ttu-id="e78b8-154">Debe usar esto como filtro en caso de que desee que el bot ofrezca un [mensaje de bienvenida](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) diferente en función del ámbito.</span><span class="sxs-lookup"><span data-stu-id="e78b8-154">You should use this as a filter in case you want your bot to offer a different [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) depending on scope.</span></span>

> [!NOTE]
> <span data-ttu-id="e78b8-155">Para bots de ámbito personal, el bot recibirá el `conversationUpdate` evento varias veces, incluso si el bot se quita y se vuelve a agregar.</span><span class="sxs-lookup"><span data-stu-id="e78b8-155">For personal scoped bots, your bot will  receive the `conversationUpdate` event multiple times, even if the bot is removed and re-added.</span></span> <span data-ttu-id="e78b8-156">Para el desarrollo y las pruebas, es posible que le resulte útil agregar una función auxiliar que le permita restablecer el bot por completo.</span><span class="sxs-lookup"><span data-stu-id="e78b8-156">For development and testing you may find it useful to add a helper function that will allow you to reset your bot completely.</span></span> <span data-ttu-id="e78b8-157">Vea un [ ejemplo deNode.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) o un ejemplo de [C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) para obtener más detalles sobre cómo implementar esto.</span><span class="sxs-lookup"><span data-stu-id="e78b8-157">See a [Node.js example](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) or [C# example](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) for more details on implementing this.</span></span>

#### <a name="schema-example-bot-added-to-personal-context"></a><span data-ttu-id="e78b8-158">Ejemplo de esquema: bot agregado al contexto personal</span><span class="sxs-lookup"><span data-stu-id="e78b8-158">Schema example: bot added to personal context</span></span>

```json
{
  "membersAdded": [{
      "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
    },
    {
      "id": "29:<userID>",
      "aadObjectId": "***"
    }
  ],
  "type": "conversationUpdate",
  "timestamp": "2019-04-23T10:17:44.349Z",
  "id": "f:5f85c2ad",
  "channelId": "msteams",
  "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
  "from": {
    "id": "29:<USERID>",
    "aadObjectId": "***"
  },
  "conversation": {
    "conversationType": "personal",
    "id": "***"
  },
  "recipient": {
    "id": "28:<BOT ID>",
    "name": "<BOT NAME>"
  },
  "channelData": {
    "tenant": {
      "id": "<TENANT ID>"
    }
  }
}
```

## <a name="team-member-or-bot-removed"></a><span data-ttu-id="e78b8-159">Miembro del equipo o bot eliminado</span><span class="sxs-lookup"><span data-stu-id="e78b8-159">Team member or bot removed</span></span>

<span data-ttu-id="e78b8-160">El `conversationUpdate` evento con el objeto de la carga se envía cuando el bot se quita de un equipo o `membersRemoved` se quita un usuario de un equipo donde se ha agregado un bot.</span><span class="sxs-lookup"><span data-stu-id="e78b8-160">The `conversationUpdate` event with the `membersRemoved` object in the payload is sent when either your bot is removed from a team, or a user is removed from a team where a bot has been added.</span></span> <span data-ttu-id="e78b8-161">Microsoft Teams también agrega `eventType.teamMemberRemoved` en el `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="e78b8-161">Microsoft Teams also adds `eventType.teamMemberRemoved` in the `channelData` object.</span></span> <span data-ttu-id="e78b8-162">Al igual que con el `membersAdded` objeto, debe analizar el objeto para el `membersRemoved` identificador de aplicación del bot para determinar quién se eliminó.</span><span class="sxs-lookup"><span data-stu-id="e78b8-162">As with the `membersAdded` object, you should parse the `membersRemoved` object for your bot's App ID to determine who was removed.</span></span>

### <a name="schema-example-team-member-removed"></a><span data-ttu-id="e78b8-163">Ejemplo de esquema: miembro del equipo eliminado</span><span class="sxs-lookup"><span data-stu-id="e78b8-163">Schema example: Team member removed</span></span>

```json
{
    "membersRemoved": [
        {
            "id": "29:1_LCi5Up14pAy65yZuaJzG1uIT7ujYhjjSTsUNqjORsZHjLHKiQIBJa4cX2XsAsRoaY7va2w6ZymA9-1VtSY_g"
        }
    ],
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:37:06.96Z",
    "localTimestamp": "2017-02-23T12:37:06.96-07:00",
    "id": "f:d8a6a4aa",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient":
    {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "teamMemberRemoved",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

### <a name="user-removed-from-a-meeting"></a><span data-ttu-id="e78b8-164">Usuario eliminado de una reunión</span><span class="sxs-lookup"><span data-stu-id="e78b8-164">User removed from a meeting</span></span>

<span data-ttu-id="e78b8-165">El `conversationUpdate` evento con el objeto de la carga se envía cuando se quita un usuario de una reunión programada `membersRemoved` privada.</span><span class="sxs-lookup"><span data-stu-id="e78b8-165">The `conversationUpdate` event with the `membersRemoved` object in the payload is sent when a user is removed from a private scheduled meeting.</span></span> <span data-ttu-id="e78b8-166">Los detalles del evento se enviarán incluso cuando los usuarios anónimos se unan a la reunión.</span><span class="sxs-lookup"><span data-stu-id="e78b8-166">The event details will be sent even when anonymous users join the meeting.</span></span> 

> [!NOTE]
>
>* <span data-ttu-id="e78b8-167">Cuando un usuario anónimo se quita de una reunión, membersRemoved objeto de carga útil no tiene `aadObjectId` campo.</span><span class="sxs-lookup"><span data-stu-id="e78b8-167">When an anonymous user is removed from a meeting, membersRemoved payload object does not have `aadObjectId` field.</span></span>
>* <span data-ttu-id="e78b8-168">Cuando un usuario anónimo se quita de una reunión, `from` el objeto de la carga siempre tiene el identificador del organizador de la reunión, incluso si otro presentador eliminó al usuario anónimo.</span><span class="sxs-lookup"><span data-stu-id="e78b8-168">When an anonymous user is removed from a meeting, `from` object in the payload always have the id of the meeting organizer, even if the anonymous user was removed by another presenter.</span></span>

#### <a name="schema-example-user-removed-from-meeting"></a><span data-ttu-id="e78b8-169">Ejemplo de esquema: Usuario eliminado de la reunión</span><span class="sxs-lookup"><span data-stu-id="e78b8-169">Schema example: User removed from meeting</span></span>

```
{   
      "membersRemoved": 
        {  
          "id": "29:1Z_XHWBMhDuehhDBYoPQD6Y1DSFsTtqOZx-SA5Jh9Y4zHKm4VbFGRn7-rK7SWiW1JECwxkMdrWpHoBut2sSyQPA"   
        }   
      ],   
      "type": "conversationUpdate",   
      "timestamp": "2020-09-29T21:15:08.6391139Z",   
      "id": "f:ee8dfdf3-54ac-51de-05da-9d49514974bb",   
      "channelId": "msteams",   
      "serviceUrl": "https://canary.botapi.skype.com/amer/",   
      "from": {   
        "id": "29:1siKxZhSoTapsXvI0gyf7Gywm_HM-4kEQW4BJnWuFYVIVu87xCNP99nidgQRCcwD3L3p_schiMShzx8IDRzf8mw",   
        "aadObjectId": "f30ba569-abef-4e97-8762-35f85cbae706"   
      },   
      "conversation": {    
        "isGroup": true,   
        "tenantId": "e15762ef-a8d8-416b-871c-25516354f1fe",   
        "id": "19:meeting_MWJlNGViOTgtMGExYi00NDA3LWExODgtOTZhMWNlYjM4ZTRj@thread.v2"   
      },   
      "recipient": {   
        "id": "28:3af3604a-d4fc-486b-911e-86fab41aa91c",   
        "name": "EchoBot1_Rename"   
      },   
      "channelData": {   
        "tenant": {   
          "id": "e15762ef-a8d8-416b-871c-25516354f1fe"   
        },   
        "source": null,   
        "meeting": {   
          "id": "MCMxOTptZWV0aW5nX01XSmxOR1ZpT1RndE1HRXhZaTAwTkRBM0xXRXhPRGd0T1RaaE1XTmxZak00WlRSakB0aHJlYWQudjIjMA=="   
        }   
      }   
}
```

## <a name="team-name-updates"></a><span data-ttu-id="e78b8-170">Actualizaciones del nombre del equipo</span><span class="sxs-lookup"><span data-stu-id="e78b8-170">Team name updates</span></span>

> [!NOTE]
> <span data-ttu-id="e78b8-171">No hay ninguna funcionalidad para consultar todos los nombres de equipo y el nombre del equipo no se devuelve en cargas útiles de otros eventos.</span><span class="sxs-lookup"><span data-stu-id="e78b8-171">There is no functionality to query all team names, and team name is not returned in payloads from other events.</span></span>

<span data-ttu-id="e78b8-172">Se notifica al bot cuando se ha cambiado el nombre del equipo en el que se encuentra.</span><span class="sxs-lookup"><span data-stu-id="e78b8-172">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="e78b8-173">Recibe un `conversationUpdate` evento con en el `eventType.teamRenamed` `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="e78b8-173">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span> <span data-ttu-id="e78b8-174">Tenga en cuenta que no hay notificaciones para la creación o eliminación del equipo, porque los bots existen solo como parte de los equipos y no tienen visibilidad fuera del ámbito en el que se han agregado.</span><span class="sxs-lookup"><span data-stu-id="e78b8-174">Please note that there are no notifications for team creation or deletion, because bots exist only as part of teams and have no visibility outside the scope in which they have been added.</span></span>

### <a name="schema-example-team-renamed"></a><span data-ttu-id="e78b8-175">Ejemplo de esquema: Cambio de nombre del equipo</span><span class="sxs-lookup"><span data-stu-id="e78b8-175">Schema example: Team renamed</span></span>

```json
{ 
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:35:56.825Z",
    "localTimestamp": "2017-02-23T12:35:56.825-07:00",
    "id": "f:1406033e",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/", 
    "from": { 
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    }, 
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": { 
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype",
            "name": "New Team Name"
        },
        "eventType": "teamRenamed",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

## <a name="channel-updates"></a><span data-ttu-id="e78b8-176">Actualizaciones de canales</span><span class="sxs-lookup"><span data-stu-id="e78b8-176">Channel updates</span></span>

<span data-ttu-id="e78b8-177">El bot se notifica cuando se crea, cambia el nombre o elimina un canal en un equipo donde se ha agregado.</span><span class="sxs-lookup"><span data-stu-id="e78b8-177">Your bot is notified when a channel is created, renamed, or deleted in a team where it has been added.</span></span> <span data-ttu-id="e78b8-178">Una vez más, se recibe el `conversationUpdate` evento y se envía un identificador de evento específico de Teams como parte del `channelData.eventType` objeto, donde los datos de canal son `channel.id` el GUID del canal y contiene `channel.name` el propio nombre del canal.</span><span class="sxs-lookup"><span data-stu-id="e78b8-178">Again, the `conversationUpdate` event is received, and a Teams-specific event identifier is sent as part of the `channelData.eventType` object, where the channel data's  `channel.id` is the GUID for the channel, and `channel.name` contains the channel name itself.</span></span>

<span data-ttu-id="e78b8-179">Los eventos de canal son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="e78b8-179">The channel events are as follows:</span></span>

* <span data-ttu-id="e78b8-180">**canalCreado** &emsp; Un usuario agrega un nuevo canal al equipo.</span><span class="sxs-lookup"><span data-stu-id="e78b8-180">**channelCreated**&emsp;A user adds a new channel to the team.</span></span>
* <span data-ttu-id="e78b8-181">**canalRenamed** &emsp; Un usuario cambia el nombre de un canal existente.</span><span class="sxs-lookup"><span data-stu-id="e78b8-181">**channelRenamed**&emsp;A user renames an existing channel.</span></span>
* <span data-ttu-id="e78b8-182">**canalDeleted** &emsp; Un usuario quita un canal.</span><span class="sxs-lookup"><span data-stu-id="e78b8-182">**channelDeleted**&emsp;A user removes a channel.</span></span>

### <a name="full-schema-example-channelcreated"></a><span data-ttu-id="e78b8-183">Ejemplo de esquema completo: channelCreated</span><span class="sxs-lookup"><span data-stu-id="e78b8-183">Full schema example: channelCreated</span></span>

```json
{
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:34:07.478Z",
    "localTimestamp": "2017-02-23T12:34:07.478-07:00",
    "id": "f:dd6ec311",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1wR7IdIRIoerMIWbewMi75JA3scaMuxvFon9eRQW2Nix5loMDo0362st2IaRVRirPZBv1WdXT8TIFWWmlQCizZQ"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "channel": {
            "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
            "name": "FunDiscussions"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "channelCreated",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a><span data-ttu-id="e78b8-184">Extracto de esquema: channelData para channelRenamed</span><span class="sxs-lookup"><span data-stu-id="e78b8-184">Schema excerpt: channelData for channelRenamed</span></span>

```json
⋮
"channelData": {
    "channel": {
        "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
        "name": "PhotographyUpdates"
    },
    "team": {
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "eventType": "channelRenamed",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    }
}
⋮
```

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a><span data-ttu-id="e78b8-185">Extracto de esquema: channelData para channelDeleted</span><span class="sxs-lookup"><span data-stu-id="e78b8-185">Schema excerpt: channelData for channelDeleted</span></span>

```json
⋮
"channelData": {
    "channel": {
        "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
        "name": "PhotographyUpdates"
    },
    "team": {
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "eventType": "channelDeleted",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    }
}
⋮
```

## <a name="reactions"></a><span data-ttu-id="e78b8-186">Reacciones</span><span class="sxs-lookup"><span data-stu-id="e78b8-186">Reactions</span></span>

<span data-ttu-id="e78b8-187">El `messageReaction` evento se envía cuando un usuario agrega o elimina su reacción a un mensaje que fue enviado originalmente por el bot.</span><span class="sxs-lookup"><span data-stu-id="e78b8-187">The `messageReaction` event is sent when a user adds or removes his or her reaction to a message which was originally sent by your bot.</span></span> <span data-ttu-id="e78b8-188">`replyToId` contiene el identificador del mensaje específico.</span><span class="sxs-lookup"><span data-stu-id="e78b8-188">`replyToId` contains the ID of the specific message.</span></span>

### <a name="schema-example-a-user-likes-a-message"></a><span data-ttu-id="e78b8-189">Ejemplo de esquema: a un usuario le gusta un mensaje</span><span class="sxs-lookup"><span data-stu-id="e78b8-189">Schema example: A user likes a message</span></span>

```json
{
    "reactionsAdded": [
        {
            "type": "like"
        }
    ],
    "type": "messageReaction",
    "timestamp": "2017-10-16T18:45:41.943Z",
    "id": "f:9f78d1f3",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA",
        "aadObjectId": "c33aafc4-646d-4543-9d4c-abd28e4d2110"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "channel": {
            "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184"
}
```

### <a name="schema-example-a-user-un-likes-a-message"></a><span data-ttu-id="e78b8-190">Ejemplo de esquema: a un usuario no le gusta un mensaje</span><span class="sxs-lookup"><span data-stu-id="e78b8-190">Schema example: A user un-likes a message</span></span>

```json
{
    "reactionsRemoved": [
        {
            "type": "like"
        }
    ],
    "type": "messageReaction",
    "timestamp": "2017-10-16T18:45:41.943Z",
    "id": "f:9f78d1f3",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA",
        "aadObjectId": "c33aafc4-646d-4543-9d4c-abd28e4d2110"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "channel": {
            "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184"
}
```

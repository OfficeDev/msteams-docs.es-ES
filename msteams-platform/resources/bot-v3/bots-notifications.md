---
title: Controlar eventos de bot
description: Describe cómo controlar eventos en bots para Microsoft Teams.
keywords: eventos de bots de Teams
ms.date: 05/20/2019
author: laujan
ms.openlocfilehash: 5ef37a931d421f245cca4fbb984b69217f779785
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796179"
---
# <a name="handle-bot-events-in-microsoft-teams"></a><span data-ttu-id="ea421-104">Controlar eventos de bot en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ea421-104">Handle bot events in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="ea421-105">Microsoft Teams envía notificaciones a su bot para cambios o eventos que ocurren en ámbitos donde el bot está activo.</span><span class="sxs-lookup"><span data-stu-id="ea421-105">Microsoft Teams sends notifications to your bot for changes or events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="ea421-106">Puede usar estos eventos para desencadenar la lógica del servicio, como los siguientes:</span><span class="sxs-lookup"><span data-stu-id="ea421-106">You can use these events to trigger service logic, such as the following:</span></span>

* <span data-ttu-id="ea421-107">Desencadenar un mensaje de bienvenida cuando se agrega un bot a un equipo</span><span class="sxs-lookup"><span data-stu-id="ea421-107">Trigger a welcome message when your bot is added to a team</span></span>
* <span data-ttu-id="ea421-108">Información del grupo de consultas y caché cuando se agrega el bot a un chat en grupo</span><span class="sxs-lookup"><span data-stu-id="ea421-108">Query and cache group information when the bot is added to a group chat</span></span>
* <span data-ttu-id="ea421-109">Actualizar la información almacenada en caché de la información del canal o la pertenencia del equipo</span><span class="sxs-lookup"><span data-stu-id="ea421-109">Update cached information on team membership or channel information</span></span>
* <span data-ttu-id="ea421-110">Quitar la información almacenada en caché de un equipo si se quita el bot</span><span class="sxs-lookup"><span data-stu-id="ea421-110">Remove cached information for a team if the bot is removed</span></span>
* <span data-ttu-id="ea421-111">Cuando un usuario le gusta un mensaje de bot?</span><span class="sxs-lookup"><span data-stu-id="ea421-111">When a bot message is liked by a user</span></span>

<span data-ttu-id="ea421-112">Cada evento de bot se envía como un `Activity` objeto en el que `messageType` define qué información se encuentra en el objeto.</span><span class="sxs-lookup"><span data-stu-id="ea421-112">Each bot event is sent as an `Activity` object in which `messageType` defines what information is in the object.</span></span> <span data-ttu-id="ea421-113">Para los mensajes de tipo `message` , vea [enviar y recibir mensajes](~/resources/bot-v3/bot-conversations/bots-conversations.md).</span><span class="sxs-lookup"><span data-stu-id="ea421-113">For messages of type `message`, see [Sending and receiving messages](~/resources/bot-v3/bot-conversations/bots-conversations.md).</span></span>

<span data-ttu-id="ea421-114">Los eventos de grupo y de equipo, que normalmente se desactivan `conversationUpdate` en el tipo, tienen información de eventos de Microsoft teams que se pasan como parte del `channelData` objeto y, por lo tanto, el controlador de eventos debe consultar la `channelData` carga de los equipos `eventType` y metadatos específicos del evento adicionales.</span><span class="sxs-lookup"><span data-stu-id="ea421-114">Teams and group events, usually triggered off the `conversationUpdate` type, have additional Teams event information passed as part of the `channelData` object, and therefore your event handler must query the `channelData` payload for the Teams `eventType` and additional event-specific metadata.</span></span>

<span data-ttu-id="ea421-115">En la siguiente tabla se enumeran los eventos que el bot puede recibir y en los que se puede realizar una acción.</span><span class="sxs-lookup"><span data-stu-id="ea421-115">The following table lists the events that your bot can receive and take action on.</span></span>

|<span data-ttu-id="ea421-116">Tipo</span><span class="sxs-lookup"><span data-stu-id="ea421-116">Type</span></span>|<span data-ttu-id="ea421-117">Objeto payload</span><span class="sxs-lookup"><span data-stu-id="ea421-117">Payload object</span></span>|<span data-ttu-id="ea421-118">EventType de Teams</span><span class="sxs-lookup"><span data-stu-id="ea421-118">Teams eventType</span></span> |<span data-ttu-id="ea421-119">Descripción</span><span class="sxs-lookup"><span data-stu-id="ea421-119">Description</span></span>|<span data-ttu-id="ea421-120">Ámbito</span><span class="sxs-lookup"><span data-stu-id="ea421-120">Scope</span></span>|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[<span data-ttu-id="ea421-121">Miembro agregado al equipo</span><span class="sxs-lookup"><span data-stu-id="ea421-121">Member added to team</span></span>](#team-member-or-bot-addition)| <span data-ttu-id="ea421-122">todos</span><span class="sxs-lookup"><span data-stu-id="ea421-122">all</span></span> |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[<span data-ttu-id="ea421-123">El miembro se quitó del equipo</span><span class="sxs-lookup"><span data-stu-id="ea421-123">Member was removed from team</span></span>](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [<span data-ttu-id="ea421-124">Se cambió el nombre del equipo</span><span class="sxs-lookup"><span data-stu-id="ea421-124">Team was renamed</span></span>](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [<span data-ttu-id="ea421-125">Se ha creado un canal</span><span class="sxs-lookup"><span data-stu-id="ea421-125">A channel was created</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [<span data-ttu-id="ea421-126">Se cambió el nombre de un canal</span><span class="sxs-lookup"><span data-stu-id="ea421-126">A channel was renamed</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [<span data-ttu-id="ea421-127">Se ha eliminado un canal</span><span class="sxs-lookup"><span data-stu-id="ea421-127">A channel was deleted</span></span>](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [<span data-ttu-id="ea421-128">Mensaje de reacción a bot</span><span class="sxs-lookup"><span data-stu-id="ea421-128">Reaction to bot message</span></span>](#reactions)| <span data-ttu-id="ea421-129">todos</span><span class="sxs-lookup"><span data-stu-id="ea421-129">all</span></span> |
| `messageReaction` |`reactionsRemoved`|| [<span data-ttu-id="ea421-130">Se ha eliminado la reacción del mensaje de bot</span><span class="sxs-lookup"><span data-stu-id="ea421-130">Reaction removed from bot message</span></span>](#reactions)| <span data-ttu-id="ea421-131">todos</span><span class="sxs-lookup"><span data-stu-id="ea421-131">all</span></span> |

## <a name="team-member-or-bot-addition"></a><span data-ttu-id="ea421-132">Adición de un miembro del equipo o bot</span><span class="sxs-lookup"><span data-stu-id="ea421-132">Team member or bot addition</span></span>

<span data-ttu-id="ea421-133">El [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate) evento se envía a su bot cuando recibe información sobre las actualizaciones de pertenencia para equipos en los que se ha agregado.</span><span class="sxs-lookup"><span data-stu-id="ea421-133">The [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate) event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="ea421-134">También recibe una actualización cuando se ha agregado por primera vez específicamente para conversaciones personales.</span><span class="sxs-lookup"><span data-stu-id="ea421-134">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span> <span data-ttu-id="ea421-135">Tenga en cuenta que la información del usuario ( `Id` ) es única para su bot y puede almacenarse en caché para su uso en el futuro por parte del servicio (por ejemplo, enviar un mensaje a un usuario específico).</span><span class="sxs-lookup"><span data-stu-id="ea421-135">Note that the user information (`Id`) is unique for your bot and can be cached for future use by your service (such as sending a message to a specific user).</span></span>

### <a name="bot-or-user-added-to-a-team"></a><span data-ttu-id="ea421-136">Bot o usuario agregado a un equipo</span><span class="sxs-lookup"><span data-stu-id="ea421-136">Bot or user added to a team</span></span>

<span data-ttu-id="ea421-137">El `conversationUpdate` evento con el `membersAdded` objeto en la carga se envía cuando se agrega un bot a un equipo o se agrega un nuevo usuario a un equipo en el que se ha agregado un bot.</span><span class="sxs-lookup"><span data-stu-id="ea421-137">The `conversationUpdate` event with the `membersAdded` object in the payload is sent when either a bot is added to a team or a new user is added to a team where a bot has been added.</span></span> <span data-ttu-id="ea421-138">Microsoft Teams también agrega `eventType.teamMemberAdded` en el `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="ea421-138">Microsoft Teams also adds `eventType.teamMemberAdded` in the `channelData` object.</span></span>

<span data-ttu-id="ea421-139">Como este evento se envía en ambos casos, debe analizar el `membersAdded` objeto para determinar si la adición fue un usuario o el bot en sí.</span><span class="sxs-lookup"><span data-stu-id="ea421-139">Because this event is sent in both cases, you should parse the `membersAdded` object to determine whether the addition was a user or the bot itself.</span></span> <span data-ttu-id="ea421-140">Para la segunda, un procedimiento recomendado es enviar un [mensaje de bienvenida](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) al canal para que los usuarios puedan comprender las características que proporciona el bot.</span><span class="sxs-lookup"><span data-stu-id="ea421-140">For the latter, a best practice is to send a [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) to the channel so users can understand the features your bot provides.</span></span>

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a><span data-ttu-id="ea421-141">Código de ejemplo: comprobar si Bot fue el miembro agregado</span><span class="sxs-lookup"><span data-stu-id="ea421-141">Example code: Checking whether bot was the added member</span></span>

##### <a name="net"></a><span data-ttu-id="ea421-142">.NET</span><span class="sxs-lookup"><span data-stu-id="ea421-142">.NET</span></span>

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

##### <a name="nodejs"></a><span data-ttu-id="ea421-143">Node.js</span><span class="sxs-lookup"><span data-stu-id="ea421-143">Node.js</span></span>

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

#### <a name="schema-example-bot-added-to-team"></a><span data-ttu-id="ea421-144">Ejemplo de esquema: bot agregado al equipo</span><span class="sxs-lookup"><span data-stu-id="ea421-144">Schema example: Bot added to team</span></span>

```json
{
    "membersAdded": [
        {
            "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
        }
    ],
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:38:35.312Z",
    "localTimestamp": "2017-02-23T12:38:35.312-07:00",
    "id": "f:5f85c2ad",
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
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "teamMemberAdded",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

### <a name="bot-added-for-personal-context-only"></a><span data-ttu-id="ea421-145">Bot agregado solo para contexto personal</span><span class="sxs-lookup"><span data-stu-id="ea421-145">Bot added for personal context only</span></span>

<span data-ttu-id="ea421-146">El bot recibe un `conversationUpdate` con `membersAdded` cuando un usuario lo agrega directamente al chat personal.</span><span class="sxs-lookup"><span data-stu-id="ea421-146">Your bot receives a `conversationUpdate` with `membersAdded` when a user adds it directly for personal chat.</span></span> <span data-ttu-id="ea421-147">En este caso, la carga que el bot recibe no contiene el `channelData.team` objeto.</span><span class="sxs-lookup"><span data-stu-id="ea421-147">In this case, the payload that your bot receives doesn't contain the `channelData.team` object.</span></span> <span data-ttu-id="ea421-148">Debe usarlo como filtro en caso de que desee que el bot ofrezca un [mensaje de bienvenida](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) diferente según el ámbito.</span><span class="sxs-lookup"><span data-stu-id="ea421-148">You should use this as a filter in case you want your bot to offer a different [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) depending on scope.</span></span>

> [!NOTE]
> <span data-ttu-id="ea421-149">En el caso de los bots de ámbito personal, el bot solo recibirá el `conversationUpdate` evento una sola vez, incluso si el bot se quita y se vuelve a agregar.</span><span class="sxs-lookup"><span data-stu-id="ea421-149">For personal scoped bots, your bot will only ever receive the `conversationUpdate` event a single time, even if the bot is removed and re-added.</span></span> <span data-ttu-id="ea421-150">Para el desarrollo y las pruebas, puede que le resulte útil agregar una función auxiliar que le permita restablecer su bot por completo.</span><span class="sxs-lookup"><span data-stu-id="ea421-150">For development and testing you may find it useful to add a helper function that will allow you to reset your bot completely.</span></span> <span data-ttu-id="ea421-151">Vea un [ ejemplo deNode.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) o un [ejemplo de C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) para obtener más información sobre la implementación de esto.</span><span class="sxs-lookup"><span data-stu-id="ea421-151">See a [Node.js example](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) or [C# example](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) for more details on implementing this.</span></span>

#### <a name="schema-example-bot-added-to-personal-context"></a><span data-ttu-id="ea421-152">Ejemplo de esquema: bot agregado a contexto personal</span><span class="sxs-lookup"><span data-stu-id="ea421-152">Schema example: bot added to personal context</span></span>

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
    "aadObjectId": "**_"
  },
  "conversation": {
    "conversationType": "personal",
    "id": "_*_"
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

## <a name="team-member-or-bot-removed"></a><span data-ttu-id="ea421-153">Miembro o bot quitado del equipo</span><span class="sxs-lookup"><span data-stu-id="ea421-153">Team member or bot removed</span></span>

<span data-ttu-id="ea421-154">El `conversationUpdate` evento con el `membersRemoved` objeto en la carga se envía cuando el bot se quita de un equipo, o bien cuando se quita un usuario de un equipo en el que se ha agregado un bot.</span><span class="sxs-lookup"><span data-stu-id="ea421-154">The `conversationUpdate` event with the `membersRemoved` object in the payload is sent when either your bot is removed from a team, or a user is removed from a team where a bot has been added.</span></span> <span data-ttu-id="ea421-155">Microsoft Teams también agrega `eventType.teamMemberRemoved` en el `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="ea421-155">Microsoft Teams also adds `eventType.teamMemberRemoved` in the `channelData` object.</span></span> <span data-ttu-id="ea421-156">Al igual que con el `membersAdded` objeto, debe analizar el objeto del identificador de la `membersRemoved` aplicación de bot para determinar quién se ha quitado.</span><span class="sxs-lookup"><span data-stu-id="ea421-156">As with the `membersAdded` object, you should parse the `membersRemoved` object for your bot's App ID to determine who was removed.</span></span>

### <a name="schema-example-team-member-removed"></a><span data-ttu-id="ea421-157">Ejemplo de esquema: miembro del equipo quitado</span><span class="sxs-lookup"><span data-stu-id="ea421-157">Schema example: Team member removed</span></span>

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

## <a name="team-name-updates"></a><span data-ttu-id="ea421-158">Actualizaciones de nombres de equipo</span><span class="sxs-lookup"><span data-stu-id="ea421-158">Team name updates</span></span>

> [!NOTE]
> <span data-ttu-id="ea421-159">No hay ninguna funcionalidad para consultar todos los nombres de los equipos, y el nombre del equipo no se devuelve en cargas de otros eventos.</span><span class="sxs-lookup"><span data-stu-id="ea421-159">There is no functionality to query all team names, and team name is not returned in payloads from other events.</span></span>

<span data-ttu-id="ea421-160">El bot recibirá una notificación cuando se haya cambiado el nombre al equipo en el que se encuentra.</span><span class="sxs-lookup"><span data-stu-id="ea421-160">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="ea421-161">Recibe un `conversationUpdate` evento con `eventType.teamRenamed` en el `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="ea421-161">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span> <span data-ttu-id="ea421-162">Tenga en cuenta que no hay notificaciones para la creación o eliminación del equipo porque los bots solo existen como parte de los equipos y no tienen visibilidad fuera del ámbito en el que se han agregado.</span><span class="sxs-lookup"><span data-stu-id="ea421-162">Please note that there are no notifications for team creation or deletion, because bots exist only as part of teams and have no visibility outside the scope in which they have been added.</span></span>

### <a name="schema-example-team-renamed"></a><span data-ttu-id="ea421-163">Ejemplo de esquema: nombre del equipo</span><span class="sxs-lookup"><span data-stu-id="ea421-163">Schema example: Team renamed</span></span>

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

## <a name="channel-updates"></a><span data-ttu-id="ea421-164">Actualizaciones de canal</span><span class="sxs-lookup"><span data-stu-id="ea421-164">Channel updates</span></span>

<span data-ttu-id="ea421-165">El bot recibe una notificación cuando se crea, se cambia el nombre o se elimina un canal en un equipo en el que se ha agregado.</span><span class="sxs-lookup"><span data-stu-id="ea421-165">Your bot is notified when a channel is created, renamed, or deleted in a team where it has been added.</span></span> <span data-ttu-id="ea421-166">`conversationUpdate`Una vez más, se recibe el evento y se envía un identificador de evento específico de equipo como parte del `channelData.eventType` objeto, donde los datos del canal `channel.id` son el GUID para el canal y `channel.name` contiene el propio nombre del canal.</span><span class="sxs-lookup"><span data-stu-id="ea421-166">Again, the `conversationUpdate` event is received, and a Teams-specific event identifier is sent as part of the `channelData.eventType` object, where the channel data's  `channel.id` is the GUID for the channel, and `channel.name` contains the channel name itself.</span></span>

<span data-ttu-id="ea421-167">Los eventos de canal son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="ea421-167">The channel events are as follows:</span></span>

<span data-ttu-id="ea421-168">_ **channelCreated** &emsp; un usuario agrega un canal nuevo al equipo</span><span class="sxs-lookup"><span data-stu-id="ea421-168">_ **channelCreated**&emsp;A user adds a new channel to the team</span></span>
* <span data-ttu-id="ea421-169">**channelRenamed** &emsp; Un usuario cambia el nombre de un canal existente</span><span class="sxs-lookup"><span data-stu-id="ea421-169">**channelRenamed**&emsp;A user renames an existing channel</span></span>
* <span data-ttu-id="ea421-170">**channelDeleted** &emsp; Un usuario quita un canal</span><span class="sxs-lookup"><span data-stu-id="ea421-170">**channelDeleted**&emsp;A user removes a channel</span></span>

### <a name="full-schema-example-channelcreated"></a><span data-ttu-id="ea421-171">Ejemplo de esquema completo: channelCreated</span><span class="sxs-lookup"><span data-stu-id="ea421-171">Full schema example: channelCreated</span></span>

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

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a><span data-ttu-id="ea421-172">Extracto de esquema: channelData para channelRenamed</span><span class="sxs-lookup"><span data-stu-id="ea421-172">Schema excerpt: channelData for channelRenamed</span></span>

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

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a><span data-ttu-id="ea421-173">Extracto de esquema: channelData para channelDeleted</span><span class="sxs-lookup"><span data-stu-id="ea421-173">Schema excerpt: channelData for channelDeleted</span></span>

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

## <a name="reactions"></a><span data-ttu-id="ea421-174">Comunicar</span><span class="sxs-lookup"><span data-stu-id="ea421-174">Reactions</span></span>

<span data-ttu-id="ea421-175">El `messageReaction` evento se envía cuando un usuario agrega o quita su reacción a un mensaje enviado originalmente por el bot.</span><span class="sxs-lookup"><span data-stu-id="ea421-175">The `messageReaction` event is sent when a user adds or removes his or her reaction to a message which was originally sent by your bot.</span></span> <span data-ttu-id="ea421-176">`replyToId` contiene el identificador del mensaje específico.</span><span class="sxs-lookup"><span data-stu-id="ea421-176">`replyToId` contains the ID of the specific message.</span></span>

### <a name="schema-example-a-user-likes-a-message"></a><span data-ttu-id="ea421-177">Ejemplo de esquema: un usuario le gusta un mensaje</span><span class="sxs-lookup"><span data-stu-id="ea421-177">Schema example: A user likes a message</span></span>

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

### <a name="schema-example-a-user-un-likes-a-message"></a><span data-ttu-id="ea421-178">Ejemplo de esquema: un usuario no le gusta un mensaje</span><span class="sxs-lookup"><span data-stu-id="ea421-178">Schema example: A user un-likes a message</span></span>

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

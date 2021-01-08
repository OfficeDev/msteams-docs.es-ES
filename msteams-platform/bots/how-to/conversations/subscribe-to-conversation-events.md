---
title: Suscribirse a eventos de conversación
author: WashingtonKayaker
description: Cómo suscribirse a eventos de conversación desde su bot de Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: f0da861834bbf221fe715d35c0beea6c3bd08f26
ms.sourcegitcommit: 5f1d6c12d80d48f403b73586f68bacf15785c855
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/30/2020
ms.locfileid: "49739038"
---
# <a name="subscribe-to-conversation-events"></a><span data-ttu-id="57164-103">Suscribirse a eventos de conversación</span><span class="sxs-lookup"><span data-stu-id="57164-103">Subscribe to conversation events</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="57164-104">Microsoft Teams envía notificaciones a su bot para eventos que ocurren en ámbitos donde el bot está activo.</span><span class="sxs-lookup"><span data-stu-id="57164-104">Microsoft Teams sends notifications to your bot for events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="57164-105">Puede capturar estos eventos en el código y realizar acciones en ellos, como los siguientes:</span><span class="sxs-lookup"><span data-stu-id="57164-105">You can capture these events in your code and take action on them, such as the following:</span></span>

* <span data-ttu-id="57164-106">Desencadenar un mensaje de bienvenida cuando se agrega un bot a un equipo</span><span class="sxs-lookup"><span data-stu-id="57164-106">Trigger a welcome message when your bot is added to a team</span></span>
* <span data-ttu-id="57164-107">Desencadenar un mensaje de bienvenida cuando se agrega o se quita un nuevo integrante del grupo</span><span class="sxs-lookup"><span data-stu-id="57164-107">Trigger a welcome message when a new team member is added or removed</span></span>
* <span data-ttu-id="57164-108">Desencadenar una notificación cuando se crea un canal, se le cambia el nombre o se elimina</span><span class="sxs-lookup"><span data-stu-id="57164-108">Trigger a notification when a channel is created, renamed or deleted</span></span>
* <span data-ttu-id="57164-109">Cuando un usuario le gusta un mensaje de bot?</span><span class="sxs-lookup"><span data-stu-id="57164-109">When a bot message is liked by a user</span></span>

## <a name="conversation-update-events"></a><span data-ttu-id="57164-110">Eventos de actualización de conversación</span><span class="sxs-lookup"><span data-stu-id="57164-110">Conversation update events</span></span>

> [!Important]
> <span data-ttu-id="57164-111">Los nuevos eventos se pueden agregar en cualquier momento y el bot empezará a recibirlos.</span><span class="sxs-lookup"><span data-stu-id="57164-111">New events can be added at any time, and your bot will begin to receive them.</span></span>
> <span data-ttu-id="57164-112">Debe diseñar la posibilidad de recibir eventos inesperados.</span><span class="sxs-lookup"><span data-stu-id="57164-112">You must design for the possibility of receiving unexpected events.</span></span>
> <span data-ttu-id="57164-113">Si usa el SDK de bot Framework, el bot responderá automáticamente con un `200 - OK` a todos los eventos que no decida controlar.</span><span class="sxs-lookup"><span data-stu-id="57164-113">If you are using the Bot Framework SDK, your bot will automatically respond with a `200 - OK` to any events you do not choose to handle.</span></span>

<span data-ttu-id="57164-114">Un bot recibe un `conversationUpdate` evento cuando se ha agregado a una conversación, se han agregado o quitado otros miembros de una conversación, o bien se han cambiado los metadatos de la conversación.</span><span class="sxs-lookup"><span data-stu-id="57164-114">A bot receives a `conversationUpdate` event when it has been added to a conversation, other members have been added to or removed from a conversation, or conversation metadata has changed.</span></span>

<span data-ttu-id="57164-115">El `conversationUpdate` evento se envía a su bot cuando recibe información sobre las actualizaciones de pertenencia para equipos en los que se ha agregado.</span><span class="sxs-lookup"><span data-stu-id="57164-115">The `conversationUpdate` event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="57164-116">También recibe una actualización cuando se ha agregado por primera vez específicamente para conversaciones personales.</span><span class="sxs-lookup"><span data-stu-id="57164-116">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span>

<span data-ttu-id="57164-117">En la siguiente tabla se muestra una lista de los eventos de actualización de conversación de Microsoft Teams, con vínculos a más detalles.</span><span class="sxs-lookup"><span data-stu-id="57164-117">The following table shows a list of Teams conversation update events, with links to more details.</span></span>

| <span data-ttu-id="57164-118">Acción emprendida</span><span class="sxs-lookup"><span data-stu-id="57164-118">Action Taken</span></span>        | <span data-ttu-id="57164-119">EventType</span><span class="sxs-lookup"><span data-stu-id="57164-119">EventType</span></span>         | <span data-ttu-id="57164-120">Método denominado</span><span class="sxs-lookup"><span data-stu-id="57164-120">Method Called</span></span>              | <span data-ttu-id="57164-121">Descripción</span><span class="sxs-lookup"><span data-stu-id="57164-121">Description</span></span>                | <span data-ttu-id="57164-122">Ámbito</span><span class="sxs-lookup"><span data-stu-id="57164-122">Scope</span></span> |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| <span data-ttu-id="57164-123">canal creado</span><span class="sxs-lookup"><span data-stu-id="57164-123">channel created</span></span>     | <span data-ttu-id="57164-124">channelCreated</span><span class="sxs-lookup"><span data-stu-id="57164-124">channelCreated</span></span>    | <span data-ttu-id="57164-125">OnTeamsChannelCreatedAsync</span><span class="sxs-lookup"><span data-stu-id="57164-125">OnTeamsChannelCreatedAsync</span></span> | [<span data-ttu-id="57164-126">Se ha creado un canal</span><span class="sxs-lookup"><span data-stu-id="57164-126">A channel was created</span></span>](#channel-created) | <span data-ttu-id="57164-127">Equipo</span><span class="sxs-lookup"><span data-stu-id="57164-127">Team</span></span> |
| <span data-ttu-id="57164-128">canal con nombre cambiado</span><span class="sxs-lookup"><span data-stu-id="57164-128">channel renamed</span></span>     | <span data-ttu-id="57164-129">channelRenamed</span><span class="sxs-lookup"><span data-stu-id="57164-129">channelRenamed</span></span>    | <span data-ttu-id="57164-130">OnTeamsChannelRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="57164-130">OnTeamsChannelRenamedAsync</span></span> | [<span data-ttu-id="57164-131">Se cambió el nombre de un canal</span><span class="sxs-lookup"><span data-stu-id="57164-131">A channel was renamed</span></span>](#channel-renamed) | <span data-ttu-id="57164-132">Equipo</span><span class="sxs-lookup"><span data-stu-id="57164-132">Team</span></span> |
| <span data-ttu-id="57164-133">canal eliminado</span><span class="sxs-lookup"><span data-stu-id="57164-133">channel deleted</span></span>     | <span data-ttu-id="57164-134">channelDeleted</span><span class="sxs-lookup"><span data-stu-id="57164-134">channelDeleted</span></span>    | <span data-ttu-id="57164-135">OnTeamsChannelDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="57164-135">OnTeamsChannelDeletedAsync</span></span> | [<span data-ttu-id="57164-136">Se ha eliminado un canal</span><span class="sxs-lookup"><span data-stu-id="57164-136">A channel was deleted</span></span>](#channel-deleted) | <span data-ttu-id="57164-137">Equipo</span><span class="sxs-lookup"><span data-stu-id="57164-137">Team</span></span> |
| <span data-ttu-id="57164-138">canal restaurado</span><span class="sxs-lookup"><span data-stu-id="57164-138">channel restored</span></span>    | <span data-ttu-id="57164-139">channelRestored</span><span class="sxs-lookup"><span data-stu-id="57164-139">channelRestored</span></span>    | <span data-ttu-id="57164-140">OnTeamsChannelRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="57164-140">OnTeamsChannelRestoredAsync</span></span> | [<span data-ttu-id="57164-141">Se restauró un canal</span><span class="sxs-lookup"><span data-stu-id="57164-141">A channel was restored</span></span>](#channel-deleted) | <span data-ttu-id="57164-142">Equipo</span><span class="sxs-lookup"><span data-stu-id="57164-142">Team</span></span> |
| <span data-ttu-id="57164-143">miembros agregados</span><span class="sxs-lookup"><span data-stu-id="57164-143">members added</span></span>   | <span data-ttu-id="57164-144">membersAdded</span><span class="sxs-lookup"><span data-stu-id="57164-144">membersAdded</span></span>   | <span data-ttu-id="57164-145">OnTeamsMembersAddedAsync</span><span class="sxs-lookup"><span data-stu-id="57164-145">OnTeamsMembersAddedAsync</span></span>   | [<span data-ttu-id="57164-146">Un miembro agregado</span><span class="sxs-lookup"><span data-stu-id="57164-146">A member added</span></span>](#team-members-added)   | <span data-ttu-id="57164-147">Todo</span><span class="sxs-lookup"><span data-stu-id="57164-147">All</span></span> |
| <span data-ttu-id="57164-148">miembros quitados</span><span class="sxs-lookup"><span data-stu-id="57164-148">members removed</span></span> | <span data-ttu-id="57164-149">membersRemoved</span><span class="sxs-lookup"><span data-stu-id="57164-149">membersRemoved</span></span> | <span data-ttu-id="57164-150">OnTeamsMembersRemovedAsync</span><span class="sxs-lookup"><span data-stu-id="57164-150">OnTeamsMembersRemovedAsync</span></span> | [<span data-ttu-id="57164-151">Se ha quitado un miembro</span><span class="sxs-lookup"><span data-stu-id="57164-151">A member was removed</span></span>](#team-members-removed) | <span data-ttu-id="57164-152">& equipo de groupChat</span><span class="sxs-lookup"><span data-stu-id="57164-152">groupChat & team</span></span> |
| <span data-ttu-id="57164-153">nombre del equipo</span><span class="sxs-lookup"><span data-stu-id="57164-153">team renamed</span></span>        | <span data-ttu-id="57164-154">teamRenamed</span><span class="sxs-lookup"><span data-stu-id="57164-154">teamRenamed</span></span>       | <span data-ttu-id="57164-155">OnTeamsTeamRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="57164-155">OnTeamsTeamRenamedAsync</span></span>    | [<span data-ttu-id="57164-156">Se cambió el nombre de un equipo</span><span class="sxs-lookup"><span data-stu-id="57164-156">A Team was renamed</span></span>](#team-renamed)       | <span data-ttu-id="57164-157">Equipo</span><span class="sxs-lookup"><span data-stu-id="57164-157">Team</span></span> |
| <span data-ttu-id="57164-158">Archivado en equipo</span><span class="sxs-lookup"><span data-stu-id="57164-158">team archived</span></span>        | <span data-ttu-id="57164-159">teamArchived</span><span class="sxs-lookup"><span data-stu-id="57164-159">teamArchived</span></span>       | <span data-ttu-id="57164-160">OnTeamsTeamArchivedAsync</span><span class="sxs-lookup"><span data-stu-id="57164-160">OnTeamsTeamArchivedAsync</span></span>    | [<span data-ttu-id="57164-161">Se archivó un equipo</span><span class="sxs-lookup"><span data-stu-id="57164-161">A Team was archived</span></span>](#team-archived)       | <span data-ttu-id="57164-162">Equipo</span><span class="sxs-lookup"><span data-stu-id="57164-162">Team</span></span> |
| <span data-ttu-id="57164-163">equipo restaurado</span><span class="sxs-lookup"><span data-stu-id="57164-163">team restored</span></span>        | <span data-ttu-id="57164-164">teamRestored</span><span class="sxs-lookup"><span data-stu-id="57164-164">teamRestored</span></span>      | <span data-ttu-id="57164-165">OnTeamsTeamRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="57164-165">OnTeamsTeamRestoredAsync</span></span>    | [<span data-ttu-id="57164-166">Se cambió el nombre de un equipo</span><span class="sxs-lookup"><span data-stu-id="57164-166">A Team was renamed</span></span>](#team-renamed)       | <span data-ttu-id="57164-167">Equipo</span><span class="sxs-lookup"><span data-stu-id="57164-167">Team</span></span> |

### <a name="channel-created"></a><span data-ttu-id="57164-168">Canal creado</span><span class="sxs-lookup"><span data-stu-id="57164-168">Channel created</span></span>

<span data-ttu-id="57164-169">El evento creado por el canal se envía a su bot cuando se crea un nuevo canal en un equipo en el que está instalado el bot.</span><span class="sxs-lookup"><span data-stu-id="57164-169">The channel created event is sent to your bot whenever a new channel is created in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="57164-170">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="57164-170">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="57164-171">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="57164-171">TypeScript/Node.js</span></span>](#tab/typescript)

<!-- From sample: botbuilder-js\libraries\botbuilder\tests\teams\conversationUpdate\src\conversationUpdateBot.ts -->

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelCreatedEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Created', `${channelInfo.name} is the Channel created`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="57164-172">JSON</span><span class="sxs-lookup"><span data-stu-id="57164-172">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="57164-173">Python</span><span class="sxs-lookup"><span data-stu-id="57164-173">Python</span></span>](#tab/python)

```python
async def on_teams_channel_created(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(
            f"The new channel is {channel_info.name}. The channel id is {channel_info.id}"
        )
    )
```

* * *

### <a name="channel-renamed"></a><span data-ttu-id="57164-174">Canal con nombre cambiado</span><span class="sxs-lookup"><span data-stu-id="57164-174">Channel renamed</span></span>

<span data-ttu-id="57164-175">El evento de canal cambiado de nombre se envía a su bot cuando se cambia el nombre de un canal en un equipo en el que está instalado el bot.</span><span class="sxs-lookup"><span data-stu-id="57164-175">The channel renamed event is sent to your bot whenever a channel is renamed in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="57164-176">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="57164-176">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="57164-177">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="57164-177">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelRenamedEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Renamed', `${channelInfo.name} is the new Channel name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
```

# <a name="json"></a>[<span data-ttu-id="57164-178">JSON</span><span class="sxs-lookup"><span data-stu-id="57164-178">JSON</span></span>](#tab/json)

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
}
```

# <a name="python"></a>[<span data-ttu-id="57164-179">Python</span><span class="sxs-lookup"><span data-stu-id="57164-179">Python</span></span>](#tab/python)

```python
async def on_teams_channel_renamed(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new channel name is {channel_info.name}")
    )
```

* * *

### <a name="channel-deleted"></a><span data-ttu-id="57164-180">Canal eliminado</span><span class="sxs-lookup"><span data-stu-id="57164-180">Channel Deleted</span></span>

<span data-ttu-id="57164-181">El evento de canal eliminado se envía a su bot cuando se elimina un canal en un equipo en el que está instalado el bot.</span><span class="sxs-lookup"><span data-stu-id="57164-181">The channel deleted event is sent to your bot whenever a channel is deleted in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="57164-182">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="57164-182">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="57164-183">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="57164-183">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelDeletedEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Deleted', `${channelInfo.name} is the Channel deleted`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="57164-184">JSON</span><span class="sxs-lookup"><span data-stu-id="57164-184">JSON</span></span>](#tab/json)

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
}
```

# <a name="python"></a>[<span data-ttu-id="57164-185">Python</span><span class="sxs-lookup"><span data-stu-id="57164-185">Python</span></span>](#tab/python)

```python
async def on_teams_channel_deleted(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The deleted channel is {channel_info.name}")
    )
```

* * *

### <a name="channel-restored"></a><span data-ttu-id="57164-186">Canal restaurado</span><span class="sxs-lookup"><span data-stu-id="57164-186">Channel restored</span></span>

<span data-ttu-id="57164-187">El evento de canal restaurado se envía a su bot cuando un canal que se eliminó anteriormente se restaura en un equipo en el que el bot ya está instalado.</span><span class="sxs-lookup"><span data-stu-id="57164-187">The channel restored event is sent to your bot whenever a channel that was previously deleted is restored in a team that your bot is already installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="57164-188">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="57164-188">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRestoredAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel restored.");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="57164-189">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="57164-189">TypeScript/Node.js</span></span>](#tab/typescript)

<!-- From sample: botbuilder-js\libraries\botbuilder\tests\teams\conversationUpdate\src\conversationUpdateBot.ts -->

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelRestoredEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Restored', `${channelInfo.name} is the Channel restored`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="57164-190">JSON</span><span class="sxs-lookup"><span data-stu-id="57164-190">JSON</span></span>](#tab/json)

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
        "eventType": "channelRestored",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="57164-191">Python</span><span class="sxs-lookup"><span data-stu-id="57164-191">Python</span></span>](#tab/python)

```python
async def on_teams_channel_restored(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(
            f"The restored channel is {channel_info.name}. The channel id is {channel_info.id}"
        )
    )
```

* * *

### <a name="team-members-added"></a><span data-ttu-id="57164-192">Miembros del equipo agregados</span><span class="sxs-lookup"><span data-stu-id="57164-192">Team members added</span></span>

<span data-ttu-id="57164-193">El `teamMemberAdded` evento se envía a su bot la primera vez que se agrega a una conversación y cada vez que se agrega un nuevo usuario a un equipo o chat de grupo en el que se instala el bot.</span><span class="sxs-lookup"><span data-stu-id="57164-193">The `teamMemberAdded` event is sent to your bot the first time it is added to a conversation and every time a new user is added to a team or group chat that your bot is installed in.</span></span> <span data-ttu-id="57164-194">La información del usuario (ID) es única para el bot y puede almacenarse en caché para su uso en el servicio (por ejemplo, enviar un mensaje a un usuario específico).</span><span class="sxs-lookup"><span data-stu-id="57164-194">The user information (ID) is unique for your bot and can be cached for future use by your service (such as sending a message to a specific user).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="57164-195">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="57164-195">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsMembersAddedAsync(IList<TeamsChannelAccount> teamsMembersAdded , TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (TeamsChannelAccount member in teamsMembersAdded)
    {
        if (member.Id == turnContext.Activity.Recipient.Id)
        {
            // Send a message to introduce the bot to the team
            var heroCard = new HeroCard(text: $"The {member.Name} bot has joined {teamInfo.Name}");
            await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
        }
        else
        {
            var heroCard = new HeroCard(text: $"{member.Name} joined {teamInfo.Name}");
            await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
        }
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="57164-196">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="57164-196">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsMembersAddedEvent(async (membersAdded: ChannelAccount[], teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
                let newMembers: string = '';
                console.log(JSON.stringify(membersAdded));
                membersAdded.forEach((account) => {
                    newMembers += account.id + ' ';
                });
                const name = !teamInfo ? 'not in team' : teamInfo.name;
                const card = CardFactory.heroCard('Account Added', `${newMembers} joined ${name}.`);
                const message = MessageFactory.attachment(card);
                await turnContext.sendActivity(message);
                await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="57164-197">JSON</span><span class="sxs-lookup"><span data-stu-id="57164-197">JSON</span></span>](#tab/json)

<span data-ttu-id="57164-198">Este es el mensaje que recibirá el bot cuando se agregue el bot **a un equipo**.</span><span class="sxs-lookup"><span data-stu-id="57164-198">This is the message your bot will receive when the bot is added **to a team**.</span></span>

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

<span data-ttu-id="57164-199">Este es el mensaje que recibirá el bot cuando se agregue el bot \**a un chat de uno a uno*.</span><span class="sxs-lookup"><span data-stu-id="57164-199">This is the message your bot will receive when the bot is added \**to a one-to-one chat*.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="57164-200">Python</span><span class="sxs-lookup"><span data-stu-id="57164-200">Python</span></span>](#tab/python)

```python
async def on_teams_members_added(
    self, teams_members_added: [TeamsChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(
            MessageFactory.text(f"Welcome your new team member {member.id}")
        )
    return
```

<span data-ttu-id="57164-201">_ \* \*</span><span class="sxs-lookup"><span data-stu-id="57164-201">_ \* \*</span></span>

### <a name="team-members-removed"></a><span data-ttu-id="57164-202">Miembros del equipo quitados</span><span class="sxs-lookup"><span data-stu-id="57164-202">Team members removed</span></span>

<span data-ttu-id="57164-203">El `teamMemberRemoved` evento se envía a su bot si se quita de un equipo y cada vez que se quita un usuario de un equipo del que es miembro el bot.</span><span class="sxs-lookup"><span data-stu-id="57164-203">The `teamMemberRemoved` event is sent to your bot if it is removed from a team and every time any user is removed from a team that your bot is a member of.</span></span> <span data-ttu-id="57164-204">Puede determinar si el nuevo miembro quitado era el propio bot o un usuario mirando en el `Activity` objeto del `turnContext` .</span><span class="sxs-lookup"><span data-stu-id="57164-204">You can determine if the new member removed was the bot itself or a user by looking at the `Activity` object of the `turnContext`.</span></span>  <span data-ttu-id="57164-205">Si el `Id` campo del `MembersRemoved` objeto es el mismo que el `Id` campo del `Recipient` objeto, el miembro quitado es el bot; de lo contrario, es un usuario.</span><span class="sxs-lookup"><span data-stu-id="57164-205">If the `Id` field of the `MembersRemoved` object is the same as the `Id` field of the `Recipient` object, then the member removed is the bot, otherwise, it is a user.</span></span>  <span data-ttu-id="57164-206">Normalmente, el bot será `Id` : `28:<MicrosoftAppId>`</span><span class="sxs-lookup"><span data-stu-id="57164-206">The bot's `Id` will generally be: `28:<MicrosoftAppId>`</span></span>

[!Note] <span data-ttu-id="57164-207">Cuando un usuario se elimina permanentemente de un espacio empresarial, `membersRemoved conversationUpdate` se desencadena un evento.</span><span class="sxs-lookup"><span data-stu-id="57164-207">When a user is permanently deleted from a tenant, `membersRemoved conversationUpdate` event is triggered.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="57164-208">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="57164-208">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsMembersRemovedAsync(IList<ChannelAccount> membersRemoved, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (TeamsChannelAccount member in membersRemoved)
    {
        if (member.Id == turnContext.Activity.Recipient.Id)
        {
            // The bot was removed
            // You should clear any cached data you have for this team
        }
        else
        {
            var heroCard = new HeroCard(text: $"{member.Name} was removed from {teamInfo.Name}");
            await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
        }
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="57164-209">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="57164-209">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsMembersRemovedEvent(async (membersRemoved: ChannelAccount[], teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            let removedMembers: string = '';
            console.log(JSON.stringify(membersRemoved));
            membersRemoved.forEach((account) => {
                removedMembers += account.id + ' ';
            });
            const name = !teamInfo ? 'not in team' : teamInfo.name;
            const card = CardFactory.heroCard('Account Removed', `${removedMembers} removed from ${teamInfo.name}.`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="57164-210">JSON</span><span class="sxs-lookup"><span data-stu-id="57164-210">JSON</span></span>](#tab/json)

<span data-ttu-id="57164-211">El `channelData` objeto del siguiente ejemplo de carga se basa en la adición de un miembro a un equipo en lugar de a un chat de grupo, o el inicio de una nueva conversación uno a uno:</span><span class="sxs-lookup"><span data-stu-id="57164-211">The `channelData` object in the following payload example is based on adding a member to a team rather than a group chat, or initiating a new one-to-one conversation:</span></span>

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


# <a name="python"></a>[<span data-ttu-id="57164-212">Python</span><span class="sxs-lookup"><span data-stu-id="57164-212">Python</span></span>](#tab/python)

```python
async def on_teams_members_removed(
    self, teams_members_removed: [TeamsChannelAccount], turn_context: TurnContext
):
    for member in teams_members_removed:
        await turn_context.send_activity(
            MessageFactory.text(f"Say goodbye to {member.id}")
        )
    return
```

* * *

### <a name="team-renamed"></a><span data-ttu-id="57164-213">Nombre del equipo</span><span class="sxs-lookup"><span data-stu-id="57164-213">Team renamed</span></span>

<span data-ttu-id="57164-214">El bot recibirá una notificación cuando se haya cambiado el nombre al equipo en el que se encuentra.</span><span class="sxs-lookup"><span data-stu-id="57164-214">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="57164-215">Recibe un `conversationUpdate` evento con `eventType.teamRenamed` en el `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="57164-215">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="57164-216">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="57164-216">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="57164-217">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="57164-217">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamRenamedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team Renamed', `${teamInfo.name} is the new Team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="57164-218">JSON</span><span class="sxs-lookup"><span data-stu-id="57164-218">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="57164-219">Python</span><span class="sxs-lookup"><span data-stu-id="57164-219">Python</span></span>](#tab/python)

```python
async def on_teams_team_renamed(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new team name is {team_info.name}")
    )
```

* * *

### <a name="team-archived"></a><span data-ttu-id="57164-220">Archivado en equipo</span><span class="sxs-lookup"><span data-stu-id="57164-220">Team archived</span></span>

<span data-ttu-id="57164-221">El bot recibe una notificación cuando se archiva el equipo en el que está instalado.</span><span class="sxs-lookup"><span data-stu-id="57164-221">The bot receives a notification when the team it is installed in is archived.</span></span> <span data-ttu-id="57164-222">Recibe un `conversationUpdate` evento con `eventType.teamarchived` en el `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="57164-222">It receives a `conversationUpdate` event with `eventType.teamarchived` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="57164-223">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="57164-223">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamArchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="57164-224">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="57164-224">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamArchivedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team archived', `${teamInfo.name} is the team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="57164-225">JSON</span><span class="sxs-lookup"><span data-stu-id="57164-225">JSON</span></span>](#tab/json)

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
            "name": "Team Name"
        },
        "eventType": "teamArchived",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="57164-226">Python</span><span class="sxs-lookup"><span data-stu-id="57164-226">Python</span></span>](#tab/python)

```python
async def on_teams_team_archived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

### <a name="team-restored"></a><span data-ttu-id="57164-227">Equipo restaurado</span><span class="sxs-lookup"><span data-stu-id="57164-227">Team restored</span></span>

<span data-ttu-id="57164-228">El bot recibe una notificación cuando se restaura el equipo en el que está instalado.</span><span class="sxs-lookup"><span data-stu-id="57164-228">The bot receives a notification when the team it is installed in is restored.</span></span> <span data-ttu-id="57164-229">Recibe un `conversationUpdate` evento con `eventType.teamrestored` en el `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="57164-229">It receives a `conversationUpdate` event with `eventType.teamrestored` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="57164-230">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="57164-230">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamrestoredAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="57164-231">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="57164-231">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamrestoredEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team restored', `${teamInfo.name} is the team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="57164-232">JSON</span><span class="sxs-lookup"><span data-stu-id="57164-232">JSON</span></span>](#tab/json)

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
            "name": "Team Name"
        },
        "eventType": "teamrestored",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="57164-233">Python</span><span class="sxs-lookup"><span data-stu-id="57164-233">Python</span></span>](#tab/python)

```python
async def on_teams_team_restored(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

## <a name="message-reaction-events"></a><span data-ttu-id="57164-234">Eventos de reacción del mensaje</span><span class="sxs-lookup"><span data-stu-id="57164-234">Message reaction events</span></span>

<span data-ttu-id="57164-235">El `messageReaction` evento se envía cuando un usuario agrega o quita reacciones de un mensaje enviado por el bot.</span><span class="sxs-lookup"><span data-stu-id="57164-235">The `messageReaction` event is sent when a user adds or removes reactions to a message which was sent by your bot.</span></span> <span data-ttu-id="57164-236">El `replyToId` contiene el identificador del mensaje específico y el `Type` es el tipo de reacción en formato de texto.</span><span class="sxs-lookup"><span data-stu-id="57164-236">The `replyToId` contains the ID of the specific message, and the `Type` is the type of reaction in text format.</span></span>  <span data-ttu-id="57164-237">Entre los tipos de reacciones se incluyen: "enfadado", "corazón", "Laugh", "like", "triste", "sorprenda".</span><span class="sxs-lookup"><span data-stu-id="57164-237">The types of reactions include: "angry", "heart", "laugh", "like", "Sad", "surprised".</span></span> <span data-ttu-id="57164-238">Este evento no contiene el contenido del mensaje original, por lo que, si es importante procesar las reacciones a los mensajes para el bot, deberá almacenarlos cuando los envíe.</span><span class="sxs-lookup"><span data-stu-id="57164-238">This event does not contain the contents of the original message, so if processing reactions to your messages is important for your bot you'll need to store the messages when you send them.</span></span>

| <span data-ttu-id="57164-239">EventType</span><span class="sxs-lookup"><span data-stu-id="57164-239">EventType</span></span>       | <span data-ttu-id="57164-240">Objeto payload</span><span class="sxs-lookup"><span data-stu-id="57164-240">Payload object</span></span>   | <span data-ttu-id="57164-241">Descripción</span><span class="sxs-lookup"><span data-stu-id="57164-241">Description</span></span>                                                             | <span data-ttu-id="57164-242">Ámbito</span><span class="sxs-lookup"><span data-stu-id="57164-242">Scope</span></span> |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| <span data-ttu-id="57164-243">messageReaction</span><span class="sxs-lookup"><span data-stu-id="57164-243">messageReaction</span></span> | <span data-ttu-id="57164-244">reactionsAdded</span><span class="sxs-lookup"><span data-stu-id="57164-244">reactionsAdded</span></span>   | [<span data-ttu-id="57164-245">Mensaje de reacción a bot</span><span class="sxs-lookup"><span data-stu-id="57164-245">Reaction to bot message</span></span>](#reactions-to-a-bot-message)                   | <span data-ttu-id="57164-246">Todo</span><span class="sxs-lookup"><span data-stu-id="57164-246">All</span></span>   |
| <span data-ttu-id="57164-247">messageReaction</span><span class="sxs-lookup"><span data-stu-id="57164-247">messageReaction</span></span> | <span data-ttu-id="57164-248">reactionsRemoved</span><span class="sxs-lookup"><span data-stu-id="57164-248">reactionsRemoved</span></span> | [<span data-ttu-id="57164-249">Se ha eliminado la reacción del mensaje de bot</span><span class="sxs-lookup"><span data-stu-id="57164-249">Reaction removed from bot message</span></span>](#reactions-removed-from-bot-message) | <span data-ttu-id="57164-250">Todo</span><span class="sxs-lookup"><span data-stu-id="57164-250">All</span></span>   |

### <a name="reactions-to-a-bot-message"></a><span data-ttu-id="57164-251">Reacciones a un mensaje de bot</span><span class="sxs-lookup"><span data-stu-id="57164-251">Reactions to a bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="57164-252">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="57164-252">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnReactionsAddedAsync(IList<MessageReaction> messageReactions, ITurnContext<IMessageReactionActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (var reaction in messageReactions)
    {
      var newReaction = $"You reacted with '{reaction.Type}' to the following message: '{turnContext.Activity.ReplyToId}'";
      var replyActivity = MessageFactory.Text(newReaction);
      var resourceResponse = await turnContext.SendActivityAsync(replyActivity, cancellationToken);
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="57164-253">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="57164-253">TypeScript/Node.js</span></span>](#tab/typescript)

<!-- Verify -->

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onReactionsAdded(async (context, next) => {
           const reactionsAdded = context.activity.reactionsAdded;
            if (reactionsAdded && reactionsAdded.length > 0) {
                for (let i = 0; i < reactionsAdded.length; i++) {
                    const reaction = reactionsAdded[i];
                    const newReaction = `You reacted with '${reaction.type}' to the following message: '${context.activity.replyToId}'`;
                    const resourceResponse = context.sendActivity(newReaction);
                    // Save information about the sent message and its ID (resourceResponse.id).
                }
            }
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="57164-254">JSON</span><span class="sxs-lookup"><span data-stu-id="57164-254">JSON</span></span>](#tab/json)

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
    "replyToId": "1575667808184",
    "legacy": {
      "replyToId": "1:19uJ8TZA1cZcms7-2HLOW3pWRF4nSWEoVnRqc0DPa_kY"
    }
}
```

# <a name="python"></a>[<span data-ttu-id="57164-255">Python</span><span class="sxs-lookup"><span data-stu-id="57164-255">Python</span></span>](#tab/python)

```python
async def on_reactions_added(
    self, message_reactions: List[MessageReaction], turn_context: TurnContext
):
    for reaction in message_reactions:
        activity = await self._log.find(turn_context.activity.reply_to_id)
        if not activity:
            await self._send_message_and_log_activity_id(
                turn_context,
                f"Activity {turn_context.activity.reply_to_id} not found in log",
            )
        else:
            await self._send_message_and_log_activity_id(
                turn_context,
                f"You added '{reaction.type}' regarding '{activity.text}'",
            )
    return
```

* * *

### <a name="reactions-removed-from-bot-message"></a><span data-ttu-id="57164-256">Reacciones eliminadas del mensaje de bot</span><span class="sxs-lookup"><span data-stu-id="57164-256">Reactions removed from bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="57164-257">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="57164-257">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnReactionsRemovedAsync(IList<MessageReaction> messageReactions, ITurnContext<IMessageReactionActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (var reaction in messageReactions)
    {
      var newReaction = $"You removed the reaction '{reaction.Type}' from the following message: '{turnContext.Activity.ReplyToId}'";
      var replyActivity = MessageFactory.Text(newReaction);
      var resourceResponse = await turnContext.SendActivityAsync(replyActivity, cancellationToken);
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="57164-258">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="57164-258">TypeScript/Node.js</span></span>](#tab/typescript)

<!-- Verify -->

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onReactionsRemoved(async(context,next)=>{
            const reactionsRemoved = context.activity.reactionsRemoved;
            if (reactionsRemoved && reactionsRemoved.length > 0) {
                for (let i = 0; i < reactionsRemoved.length; i++) {
                    const reaction = reactionsRemoved[i];
                    const newReaction = `You removed the reaction '${reaction.type}' from the message: '${context.activity.replyToId}'`;
                    const resourceResponse = context.sendActivity(newReaction);
                    // Save information about the sent message and its ID (resourceResponse.id).
                }
            }
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="57164-259">JSON</span><span class="sxs-lookup"><span data-stu-id="57164-259">JSON</span></span>](#tab/json)

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
    "replyToId": "1575667808184",
    "legacy": {
      "replyToId": "1:19uJ8TZA1cZcms7-2HLOW3pWRF4nSWEoVnRqc0DPa_kY"
    }
}
```

# <a name="python"></a>[<span data-ttu-id="57164-260">Python</span><span class="sxs-lookup"><span data-stu-id="57164-260">Python</span></span>](#tab/python)

```python
async def on_reactions_removed(
    self, message_reactions: List[MessageReaction], turn_context: TurnContext
):
    for reaction in message_reactions:
        activity = await self._log.find(turn_context.activity.reply_to_id)
        if not activity:
            await self._send_message_and_log_activity_id(
                turn_context,
                f"Activity {turn_context.activity.reply_to_id} not found in log",
            )
        else:
            await self._send_message_and_log_activity_id(
                turn_context,
                f"You removed '{reaction.type}' regarding '{activity.text}'",
            )
    return
```

* * *

---
title: Suscribirse a eventos de conversación
author: WashingtonKayaker
description: Cómo suscribirse a eventos de conversación desde su bot de Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: c678690b1dc2c948cceacdf42c95f169fff753bb
ms.sourcegitcommit: 560bf433129c16888135879e2703dbdeb38ec99f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2020
ms.locfileid: "48397683"
---
# <a name="subscribe-to-conversation-events"></a><span data-ttu-id="609fd-103">Suscribirse a eventos de conversación</span><span class="sxs-lookup"><span data-stu-id="609fd-103">Subscribe to conversation events</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="609fd-104">Microsoft Teams envía notificaciones a su bot para eventos que ocurren en ámbitos donde el bot está activo.</span><span class="sxs-lookup"><span data-stu-id="609fd-104">Microsoft Teams sends notifications to your bot for events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="609fd-105">Puede capturar estos eventos en el código y realizar acciones en ellos, como los siguientes:</span><span class="sxs-lookup"><span data-stu-id="609fd-105">You can capture these events in your code and take action on them, such as the following:</span></span>

* <span data-ttu-id="609fd-106">Desencadenar un mensaje de bienvenida cuando se agrega un bot a un equipo</span><span class="sxs-lookup"><span data-stu-id="609fd-106">Trigger a welcome message when your bot is added to a team</span></span>
* <span data-ttu-id="609fd-107">Desencadenar un mensaje de bienvenida cuando se agrega o se quita un nuevo integrante del grupo</span><span class="sxs-lookup"><span data-stu-id="609fd-107">Trigger a welcome message when a new team member is added or removed</span></span>
* <span data-ttu-id="609fd-108">Desencadenar una notificación cuando se crea un canal, se le cambia el nombre o se elimina</span><span class="sxs-lookup"><span data-stu-id="609fd-108">Trigger a notification when a channel is created, renamed or deleted</span></span>
* <span data-ttu-id="609fd-109">Cuando un usuario le gusta un mensaje de bot?</span><span class="sxs-lookup"><span data-stu-id="609fd-109">When a bot message is liked by a user</span></span>

## <a name="conversation-update-events"></a><span data-ttu-id="609fd-110">Eventos de actualización de conversación</span><span class="sxs-lookup"><span data-stu-id="609fd-110">Conversation update events</span></span>

<span data-ttu-id="609fd-111">Un bot recibe un `conversationUpdate` evento cuando se ha agregado a una conversación, se han agregado o quitado otros miembros de una conversación, o bien se han cambiado los metadatos de la conversación.</span><span class="sxs-lookup"><span data-stu-id="609fd-111">A bot receives a `conversationUpdate` event when it has been added to a conversation, other members have been added to or removed from a conversation, or conversation metadata has changed.</span></span>

<span data-ttu-id="609fd-112">El `conversationUpdate` evento se envía a su bot cuando recibe información sobre las actualizaciones de pertenencia para equipos en los que se ha agregado.</span><span class="sxs-lookup"><span data-stu-id="609fd-112">The `conversationUpdate` event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="609fd-113">También recibe una actualización cuando se ha agregado por primera vez específicamente para conversaciones personales.</span><span class="sxs-lookup"><span data-stu-id="609fd-113">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span>

<span data-ttu-id="609fd-114">En la siguiente tabla se muestra una lista de los eventos de actualización de conversación de Microsoft Teams, con vínculos a más detalles.</span><span class="sxs-lookup"><span data-stu-id="609fd-114">The following table shows a list of Teams conversation update events, with links to more details.</span></span>

| <span data-ttu-id="609fd-115">Acción emprendida</span><span class="sxs-lookup"><span data-stu-id="609fd-115">Action Taken</span></span>        | <span data-ttu-id="609fd-116">EventType</span><span class="sxs-lookup"><span data-stu-id="609fd-116">EventType</span></span>         | <span data-ttu-id="609fd-117">Método denominado</span><span class="sxs-lookup"><span data-stu-id="609fd-117">Method Called</span></span>              | <span data-ttu-id="609fd-118">Descripción</span><span class="sxs-lookup"><span data-stu-id="609fd-118">Description</span></span>                | <span data-ttu-id="609fd-119">Ámbito</span><span class="sxs-lookup"><span data-stu-id="609fd-119">Scope</span></span> |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| <span data-ttu-id="609fd-120">canal creado</span><span class="sxs-lookup"><span data-stu-id="609fd-120">channel created</span></span>     | <span data-ttu-id="609fd-121">channelCreated</span><span class="sxs-lookup"><span data-stu-id="609fd-121">channelCreated</span></span>    | <span data-ttu-id="609fd-122">OnTeamsChannelCreatedAsync</span><span class="sxs-lookup"><span data-stu-id="609fd-122">OnTeamsChannelCreatedAsync</span></span> | [<span data-ttu-id="609fd-123">Se ha creado un canal</span><span class="sxs-lookup"><span data-stu-id="609fd-123">A channel was created</span></span>](#channel-created) | <span data-ttu-id="609fd-124">Equipo</span><span class="sxs-lookup"><span data-stu-id="609fd-124">Team</span></span> |
| <span data-ttu-id="609fd-125">canal con nombre cambiado</span><span class="sxs-lookup"><span data-stu-id="609fd-125">channel renamed</span></span>     | <span data-ttu-id="609fd-126">channelRenamed</span><span class="sxs-lookup"><span data-stu-id="609fd-126">channelRenamed</span></span>    | <span data-ttu-id="609fd-127">OnTeamsChannelRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="609fd-127">OnTeamsChannelRenamedAsync</span></span> | [<span data-ttu-id="609fd-128">Se cambió el nombre de un canal</span><span class="sxs-lookup"><span data-stu-id="609fd-128">A channel was renamed</span></span>](#channel-renamed) | <span data-ttu-id="609fd-129">Equipo</span><span class="sxs-lookup"><span data-stu-id="609fd-129">Team</span></span> |
| <span data-ttu-id="609fd-130">canal eliminado</span><span class="sxs-lookup"><span data-stu-id="609fd-130">channel deleted</span></span>     | <span data-ttu-id="609fd-131">channelDeleted</span><span class="sxs-lookup"><span data-stu-id="609fd-131">channelDeleted</span></span>    | <span data-ttu-id="609fd-132">OnTeamsChannelDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="609fd-132">OnTeamsChannelDeletedAsync</span></span> | [<span data-ttu-id="609fd-133">Se ha eliminado un canal</span><span class="sxs-lookup"><span data-stu-id="609fd-133">A channel was deleted</span></span>](#channel-deleted) | <span data-ttu-id="609fd-134">Equipo</span><span class="sxs-lookup"><span data-stu-id="609fd-134">Team</span></span> |
| <span data-ttu-id="609fd-135">miembros del equipo agregados</span><span class="sxs-lookup"><span data-stu-id="609fd-135">team members added</span></span>   | <span data-ttu-id="609fd-136">teamMemberAdded</span><span class="sxs-lookup"><span data-stu-id="609fd-136">teamMemberAdded</span></span>   | <span data-ttu-id="609fd-137">OnTeamsMembersAddedAsync</span><span class="sxs-lookup"><span data-stu-id="609fd-137">OnTeamsMembersAddedAsync</span></span>   | [<span data-ttu-id="609fd-138">Un miembro agregado al equipo</span><span class="sxs-lookup"><span data-stu-id="609fd-138">A Member added to team</span></span>](#team-members-added)   | <span data-ttu-id="609fd-139">Todo</span><span class="sxs-lookup"><span data-stu-id="609fd-139">All</span></span> |
| <span data-ttu-id="609fd-140">miembros del equipo quitados</span><span class="sxs-lookup"><span data-stu-id="609fd-140">team members removed</span></span> | <span data-ttu-id="609fd-141">teamMemberRemoved</span><span class="sxs-lookup"><span data-stu-id="609fd-141">teamMemberRemoved</span></span> | <span data-ttu-id="609fd-142">OnTeamsMembersRemovedAsync</span><span class="sxs-lookup"><span data-stu-id="609fd-142">OnTeamsMembersRemovedAsync</span></span> | [<span data-ttu-id="609fd-143">Se ha quitado un miembro del equipo</span><span class="sxs-lookup"><span data-stu-id="609fd-143">A Member was removed from team</span></span>](#team-members-removed) | <span data-ttu-id="609fd-144">& equipo de groupChat</span><span class="sxs-lookup"><span data-stu-id="609fd-144">groupChat & team</span></span> |
| <span data-ttu-id="609fd-145">nombre del equipo</span><span class="sxs-lookup"><span data-stu-id="609fd-145">team renamed</span></span>        | <span data-ttu-id="609fd-146">teamRenamed</span><span class="sxs-lookup"><span data-stu-id="609fd-146">teamRenamed</span></span>       | <span data-ttu-id="609fd-147">OnTeamsTeamRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="609fd-147">OnTeamsTeamRenamedAsync</span></span>    | [<span data-ttu-id="609fd-148">Se cambió el nombre de un equipo</span><span class="sxs-lookup"><span data-stu-id="609fd-148">A Team was renamed</span></span>](#team-renamed)       | <span data-ttu-id="609fd-149">Equipo</span><span class="sxs-lookup"><span data-stu-id="609fd-149">Team</span></span> |

### <a name="channel-created"></a><span data-ttu-id="609fd-150">Canal creado</span><span class="sxs-lookup"><span data-stu-id="609fd-150">Channel created</span></span>

<span data-ttu-id="609fd-151">El evento creado por el canal se envía a su bot cuando se crea un nuevo canal en un equipo en el que está instalado el bot.</span><span class="sxs-lookup"><span data-stu-id="609fd-151">The channel created event is sent to your bot whenever a new channel is created in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="609fd-152">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="609fd-152">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="609fd-153">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="609fd-153">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="609fd-154">JSON</span><span class="sxs-lookup"><span data-stu-id="609fd-154">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="609fd-155">Python</span><span class="sxs-lookup"><span data-stu-id="609fd-155">Python</span></span>](#tab/python)

```python
async def on_teams_channel_created_activity(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(
            f"The new channel is {channel_info.name}. The channel id is {channel_info.id}"
        )
    )
```

* * *

### <a name="channel-renamed"></a><span data-ttu-id="609fd-156">Canal con nombre cambiado</span><span class="sxs-lookup"><span data-stu-id="609fd-156">Channel renamed</span></span>

<span data-ttu-id="609fd-157">El evento de canal cambiado de nombre se envía a su bot cuando se cambia el nombre de un canal en un equipo en el que está instalado el bot.</span><span class="sxs-lookup"><span data-stu-id="609fd-157">The channel renamed event is sent to your bot whenever a channel is renamed in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="609fd-158">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="609fd-158">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="609fd-159">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="609fd-159">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="609fd-160">JSON</span><span class="sxs-lookup"><span data-stu-id="609fd-160">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="609fd-161">Python</span><span class="sxs-lookup"><span data-stu-id="609fd-161">Python</span></span>](#tab/python)

```python
async def on_teams_channel_renamed_activity(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new channel name is {channel_info.name}")
    )
```

* * *

### <a name="channel-deleted"></a><span data-ttu-id="609fd-162">Canal eliminado</span><span class="sxs-lookup"><span data-stu-id="609fd-162">Channel Deleted</span></span>

<span data-ttu-id="609fd-163">El evento de canal eliminado se envía a su bot cuando se elimina un canal en un equipo en el que está instalado el bot.</span><span class="sxs-lookup"><span data-stu-id="609fd-163">The channel deleted event is sent to your bot whenever a channel is deleted in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="609fd-164">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="609fd-164">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="609fd-165">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="609fd-165">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="609fd-166">JSON</span><span class="sxs-lookup"><span data-stu-id="609fd-166">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="609fd-167">Python</span><span class="sxs-lookup"><span data-stu-id="609fd-167">Python</span></span>](#tab/python)

```python
async def on_teams_channel_deleted_activity(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The deleted channel is {channel_info.name}")
    )
```

* * *

### <a name="team-members-added"></a><span data-ttu-id="609fd-168">Miembros del equipo agregados</span><span class="sxs-lookup"><span data-stu-id="609fd-168">Team members added</span></span>

<span data-ttu-id="609fd-169">El `teamMemberAdded` evento se envía a su bot la primera vez que se agrega a una conversación y cada vez que se agrega un nuevo usuario a un equipo o chat de grupo en el que se instala el bot.</span><span class="sxs-lookup"><span data-stu-id="609fd-169">The `teamMemberAdded` event is sent to your bot the first time it is added to a conversation and every time a new user is added to a team or group chat that your bot is installed in.</span></span> <span data-ttu-id="609fd-170">La información del usuario (ID) es única para el bot y puede almacenarse en caché para su uso en el servicio (por ejemplo, enviar un mensaje a un usuario específico).</span><span class="sxs-lookup"><span data-stu-id="609fd-170">The user information (ID) is unique for your bot and can be cached for future use by your service (such as sending a message to a specific user).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="609fd-171">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="609fd-171">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsMembersAddedAsync(IList<ChannelAccount> membersAdded, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (TeamsChannelAccount member in membersAdded)
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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="609fd-172">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="609fd-172">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="609fd-173">JSON</span><span class="sxs-lookup"><span data-stu-id="609fd-173">JSON</span></span>](#tab/json)

<span data-ttu-id="609fd-174">Este es el mensaje que recibirá el bot cuando se agregue el bot **a un equipo**.</span><span class="sxs-lookup"><span data-stu-id="609fd-174">This is the message your bot will receive when the bot is added **to a team**.</span></span>

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

<span data-ttu-id="609fd-175">Este es el mensaje que recibirá el bot cuando se agregue el bot \**a un chat de uno a uno*.</span><span class="sxs-lookup"><span data-stu-id="609fd-175">This is the message your bot will receive when the bot is added \**to a one-to-one chat*.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="609fd-176">Python</span><span class="sxs-lookup"><span data-stu-id="609fd-176">Python</span></span>](#tab/python)

```python
async def on_teams_members_added_activity(
    self, teams_members_added: [TeamsChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(
            MessageFactory.text(f"Welcome your new team member {member.id}")
        )
    return
```

* * *

### <a name="team-members-removed"></a><span data-ttu-id="609fd-177">Miembros del equipo quitados</span><span class="sxs-lookup"><span data-stu-id="609fd-177">Team members removed</span></span>

<span data-ttu-id="609fd-178">El `teamMemberRemoved` evento se envía a su bot si se quita de un equipo y cada vez que se quita un usuario de un equipo del que es miembro el bot.</span><span class="sxs-lookup"><span data-stu-id="609fd-178">The `teamMemberRemoved` event is sent to your bot if it is removed from a team and every time any user is removed from a team that your bot is a member of.</span></span> <span data-ttu-id="609fd-179">Puede determinar si el nuevo miembro quitado era el propio bot o un usuario mirando en el `Activity` objeto del `turnContext` .</span><span class="sxs-lookup"><span data-stu-id="609fd-179">You can determine if the new member removed was the bot itself or a user by looking at the `Activity` object of the `turnContext`.</span></span>  <span data-ttu-id="609fd-180">Si el `Id` campo del `MembersRemoved` objeto es el mismo que el `Id` campo del `Recipient` objeto, el miembro quitado es el bot; de lo contrario, es un usuario.</span><span class="sxs-lookup"><span data-stu-id="609fd-180">If the `Id` field of the `MembersRemoved` object is the same as the `Id` field of the `Recipient` object, then the member removed is the bot, otherwise it is a user.</span></span>  <span data-ttu-id="609fd-181">Normalmente, el bot será `Id` : `28:<MicrosoftAppId>`</span><span class="sxs-lookup"><span data-stu-id="609fd-181">The bot's `Id` will generally be: `28:<MicrosoftAppId>`</span></span>

[!Note] <span data-ttu-id="609fd-182">Cuando un usuario se elimina permanentemente de un espacio empresarial, `membersRemoved conversationUpdate` se desencadena un evento.</span><span class="sxs-lookup"><span data-stu-id="609fd-182">When a user is permanently deleted from a tenant, `membersRemoved conversationUpdate` event is triggered.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="609fd-183">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="609fd-183">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="609fd-184">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="609fd-184">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="609fd-185">JSON</span><span class="sxs-lookup"><span data-stu-id="609fd-185">JSON</span></span>](#tab/json)

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


# <a name="python"></a>[<span data-ttu-id="609fd-186">Python</span><span class="sxs-lookup"><span data-stu-id="609fd-186">Python</span></span>](#tab/python)

```python
async def on_teams_members_removed_activity(
    self, teams_members_removed: [TeamsChannelAccount], turn_context: TurnContext
):
    for member in teams_members_removed:
        await turn_context.send_activity(
            MessageFactory.text(f"Say goodbye to your team member {member.id}")
        )
    return
```

* * *

### <a name="team-renamed"></a><span data-ttu-id="609fd-187">Nombre del equipo</span><span class="sxs-lookup"><span data-stu-id="609fd-187">Team renamed</span></span>

<span data-ttu-id="609fd-188">El bot recibirá una notificación cuando se haya cambiado el nombre al equipo en el que se encuentra.</span><span class="sxs-lookup"><span data-stu-id="609fd-188">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="609fd-189">Recibe un `conversationUpdate` evento con `eventType.teamRenamed` en el `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="609fd-189">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="609fd-190">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="609fd-190">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="609fd-191">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="609fd-191">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="609fd-192">JSON</span><span class="sxs-lookup"><span data-stu-id="609fd-192">JSON</span></span>](#tab/json)

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


# <a name="python"></a>[<span data-ttu-id="609fd-193">Python</span><span class="sxs-lookup"><span data-stu-id="609fd-193">Python</span></span>](#tab/python)

```python
async def on_teams_team_renamed_activity(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new team name is {team_info.name}")
    )
```

* * *

## <a name="message-reaction-events"></a><span data-ttu-id="609fd-194">Eventos de reacción del mensaje</span><span class="sxs-lookup"><span data-stu-id="609fd-194">Message reaction events</span></span>

<span data-ttu-id="609fd-195">El `messageReaction` evento se envía cuando un usuario agrega o quita reacciones de un mensaje enviado por el bot.</span><span class="sxs-lookup"><span data-stu-id="609fd-195">The `messageReaction` event is sent when a user adds or removes reactions to a message which was sent by your bot.</span></span> <span data-ttu-id="609fd-196">El `replyToId` contiene el identificador del mensaje específico y el `Type` es el tipo de reacción en formato de texto.</span><span class="sxs-lookup"><span data-stu-id="609fd-196">The `replyToId` contains the ID of the specific message, and the `Type` is the type of reaction in text format.</span></span>  <span data-ttu-id="609fd-197">Entre los tipos de reacciones se incluyen: "enfadado", "corazón", "Laugh", "like", "triste", "sorprenda".</span><span class="sxs-lookup"><span data-stu-id="609fd-197">The types of reactions include: "angry", "heart", "laugh", "like", "Sad", "surprised".</span></span> <span data-ttu-id="609fd-198">Este evento no contiene el contenido del mensaje original, por lo que, si es importante procesar las reacciones a los mensajes para el bot, deberá almacenarlos cuando los envíe.</span><span class="sxs-lookup"><span data-stu-id="609fd-198">This event does not contain the contents of the original message, so if processing reactions to your messages is important for your bot you'll need to store the messages when you send them.</span></span>

| <span data-ttu-id="609fd-199">EventType</span><span class="sxs-lookup"><span data-stu-id="609fd-199">EventType</span></span>       | <span data-ttu-id="609fd-200">Objeto payload</span><span class="sxs-lookup"><span data-stu-id="609fd-200">Payload object</span></span>   | <span data-ttu-id="609fd-201">Descripción</span><span class="sxs-lookup"><span data-stu-id="609fd-201">Description</span></span>                                                             | <span data-ttu-id="609fd-202">Ámbito</span><span class="sxs-lookup"><span data-stu-id="609fd-202">Scope</span></span> |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| <span data-ttu-id="609fd-203">messageReaction</span><span class="sxs-lookup"><span data-stu-id="609fd-203">messageReaction</span></span> | <span data-ttu-id="609fd-204">reactionsAdded</span><span class="sxs-lookup"><span data-stu-id="609fd-204">reactionsAdded</span></span>   | [<span data-ttu-id="609fd-205">Mensaje de reacción a bot</span><span class="sxs-lookup"><span data-stu-id="609fd-205">Reaction to bot message</span></span>](#reactions-to-a-bot-message)                   | <span data-ttu-id="609fd-206">Todo</span><span class="sxs-lookup"><span data-stu-id="609fd-206">All</span></span>   |
| <span data-ttu-id="609fd-207">messageReaction</span><span class="sxs-lookup"><span data-stu-id="609fd-207">messageReaction</span></span> | <span data-ttu-id="609fd-208">reactionsRemoved</span><span class="sxs-lookup"><span data-stu-id="609fd-208">reactionsRemoved</span></span> | [<span data-ttu-id="609fd-209">Se ha eliminado la reacción del mensaje de bot</span><span class="sxs-lookup"><span data-stu-id="609fd-209">Reaction removed from bot message</span></span>](#reactions-removed-from-bot-message) | <span data-ttu-id="609fd-210">Todo</span><span class="sxs-lookup"><span data-stu-id="609fd-210">All</span></span>   |

### <a name="reactions-to-a-bot-message"></a><span data-ttu-id="609fd-211">Reacciones a un mensaje de bot</span><span class="sxs-lookup"><span data-stu-id="609fd-211">Reactions to a bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="609fd-212">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="609fd-212">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="609fd-213">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="609fd-213">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="609fd-214">JSON</span><span class="sxs-lookup"><span data-stu-id="609fd-214">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="609fd-215">Python</span><span class="sxs-lookup"><span data-stu-id="609fd-215">Python</span></span>](#tab/python)

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

### <a name="reactions-removed-from-bot-message"></a><span data-ttu-id="609fd-216">Reacciones eliminadas del mensaje de bot</span><span class="sxs-lookup"><span data-stu-id="609fd-216">Reactions removed from bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="609fd-217">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="609fd-217">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="609fd-218">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="609fd-218">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="609fd-219">JSON</span><span class="sxs-lookup"><span data-stu-id="609fd-219">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="609fd-220">Python</span><span class="sxs-lookup"><span data-stu-id="609fd-220">Python</span></span>](#tab/python)

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

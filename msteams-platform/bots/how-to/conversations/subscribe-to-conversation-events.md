---
title: Suscribirse a eventos de conversación
author: WashingtonKayaker
description: Cómo suscribirse a eventos de conversación desde el bot de Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: b4dc70e4619043bd0b675206770093b086fc5ec6
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014323"
---
# <a name="subscribe-to-conversation-events"></a><span data-ttu-id="f1147-103">Suscribirse a eventos de conversación</span><span class="sxs-lookup"><span data-stu-id="f1147-103">Subscribe to conversation events</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="f1147-104">Microsoft Teams envía notificaciones al bot para eventos que se suceden en ámbitos donde el bot está activo.</span><span class="sxs-lookup"><span data-stu-id="f1147-104">Microsoft Teams sends notifications to your bot for events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="f1147-105">Puedes capturar estos eventos en el código y tomar medidas en ellos, como los siguientes:</span><span class="sxs-lookup"><span data-stu-id="f1147-105">You can capture these events in your code and take action on them, such as the following:</span></span>

* <span data-ttu-id="f1147-106">Desencadenar un mensaje de bienvenida cuando el bot se agrega a un equipo</span><span class="sxs-lookup"><span data-stu-id="f1147-106">Trigger a welcome message when your bot is added to a team</span></span>
* <span data-ttu-id="f1147-107">Desencadenar un mensaje de bienvenida cuando se agrega o quita un nuevo miembro del equipo</span><span class="sxs-lookup"><span data-stu-id="f1147-107">Trigger a welcome message when a new team member is added or removed</span></span>
* <span data-ttu-id="f1147-108">Desencadenar una notificación cuando se crea, se cambia el nombre o se elimina un canal</span><span class="sxs-lookup"><span data-stu-id="f1147-108">Trigger a notification when a channel is created, renamed or deleted</span></span>
* <span data-ttu-id="f1147-109">Cuando un usuario le gusta un mensaje de bot</span><span class="sxs-lookup"><span data-stu-id="f1147-109">When a bot message is liked by a user</span></span>

## <a name="conversation-update-events"></a><span data-ttu-id="f1147-110">Eventos de actualización de conversación</span><span class="sxs-lookup"><span data-stu-id="f1147-110">Conversation update events</span></span>

> [!Important]
> <span data-ttu-id="f1147-111">Se pueden agregar eventos nuevos en cualquier momento y el bot empezará a recibirlos.</span><span class="sxs-lookup"><span data-stu-id="f1147-111">New events can be added at any time, and your bot will begin to receive them.</span></span>
> <span data-ttu-id="f1147-112">Debe diseñar la posibilidad de recibir eventos inesperados.</span><span class="sxs-lookup"><span data-stu-id="f1147-112">You must design for the possibility of receiving unexpected events.</span></span>
> <span data-ttu-id="f1147-113">Si usa el SDK de Bot Framework, el bot responderá automáticamente con un a a cualquier evento `200 - OK` que no elija controlar.</span><span class="sxs-lookup"><span data-stu-id="f1147-113">If you are using the Bot Framework SDK, your bot will automatically respond with a `200 - OK` to any events you do not choose to handle.</span></span>

<span data-ttu-id="f1147-114">Un bot recibe un evento cuando se ha agregado a una conversación, se han agregado o quitado otros miembros de una conversación, o los metadatos de `conversationUpdate` la conversación han cambiado.</span><span class="sxs-lookup"><span data-stu-id="f1147-114">A bot receives a `conversationUpdate` event when it has been added to a conversation, other members have been added to or removed from a conversation, or conversation metadata has changed.</span></span>

<span data-ttu-id="f1147-115">El evento se envía al bot cuando recibe información sobre las actualizaciones de pertenencia de los equipos a los que `conversationUpdate` se ha agregado.</span><span class="sxs-lookup"><span data-stu-id="f1147-115">The `conversationUpdate` event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="f1147-116">También recibe una actualización cuando se ha agregado por primera vez específicamente para conversaciones personales.</span><span class="sxs-lookup"><span data-stu-id="f1147-116">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span>

<span data-ttu-id="f1147-117">En la tabla siguiente se muestra una lista de eventos de actualización de conversaciones de Teams, con vínculos para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="f1147-117">The following table shows a list of Teams conversation update events, with links to more details.</span></span>

| <span data-ttu-id="f1147-118">Acción realizada</span><span class="sxs-lookup"><span data-stu-id="f1147-118">Action Taken</span></span>        | <span data-ttu-id="f1147-119">EventType</span><span class="sxs-lookup"><span data-stu-id="f1147-119">EventType</span></span>         | <span data-ttu-id="f1147-120">Método llamado</span><span class="sxs-lookup"><span data-stu-id="f1147-120">Method Called</span></span>              | <span data-ttu-id="f1147-121">Descripción</span><span class="sxs-lookup"><span data-stu-id="f1147-121">Description</span></span>                | <span data-ttu-id="f1147-122">Ámbito</span><span class="sxs-lookup"><span data-stu-id="f1147-122">Scope</span></span> |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| <span data-ttu-id="f1147-123">canal creado</span><span class="sxs-lookup"><span data-stu-id="f1147-123">channel created</span></span>     | <span data-ttu-id="f1147-124">channelCreated</span><span class="sxs-lookup"><span data-stu-id="f1147-124">channelCreated</span></span>    | <span data-ttu-id="f1147-125">OnTeamsChannelCreatedAsync</span><span class="sxs-lookup"><span data-stu-id="f1147-125">OnTeamsChannelCreatedAsync</span></span> | [<span data-ttu-id="f1147-126">Se creó un canal</span><span class="sxs-lookup"><span data-stu-id="f1147-126">A channel was created</span></span>](#channel-created) | <span data-ttu-id="f1147-127">Equipo</span><span class="sxs-lookup"><span data-stu-id="f1147-127">Team</span></span> |
| <span data-ttu-id="f1147-128">se cambió el nombre del canal</span><span class="sxs-lookup"><span data-stu-id="f1147-128">channel renamed</span></span>     | <span data-ttu-id="f1147-129">channelRenamed</span><span class="sxs-lookup"><span data-stu-id="f1147-129">channelRenamed</span></span>    | <span data-ttu-id="f1147-130">OnTeamsChannelRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="f1147-130">OnTeamsChannelRenamedAsync</span></span> | [<span data-ttu-id="f1147-131">Se cambió el nombre de un canal</span><span class="sxs-lookup"><span data-stu-id="f1147-131">A channel was renamed</span></span>](#channel-renamed) | <span data-ttu-id="f1147-132">Equipo</span><span class="sxs-lookup"><span data-stu-id="f1147-132">Team</span></span> |
| <span data-ttu-id="f1147-133">canal eliminado</span><span class="sxs-lookup"><span data-stu-id="f1147-133">channel deleted</span></span>     | <span data-ttu-id="f1147-134">channelDeleted</span><span class="sxs-lookup"><span data-stu-id="f1147-134">channelDeleted</span></span>    | <span data-ttu-id="f1147-135">OnTeamsChannelDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="f1147-135">OnTeamsChannelDeletedAsync</span></span> | [<span data-ttu-id="f1147-136">Se eliminó un canal</span><span class="sxs-lookup"><span data-stu-id="f1147-136">A channel was deleted</span></span>](#channel-deleted) | <span data-ttu-id="f1147-137">Equipo</span><span class="sxs-lookup"><span data-stu-id="f1147-137">Team</span></span> |
| <span data-ttu-id="f1147-138">canal restaurado</span><span class="sxs-lookup"><span data-stu-id="f1147-138">channel restored</span></span>    | <span data-ttu-id="f1147-139">channelRestored</span><span class="sxs-lookup"><span data-stu-id="f1147-139">channelRestored</span></span>    | <span data-ttu-id="f1147-140">OnTeamsChannelRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="f1147-140">OnTeamsChannelRestoredAsync</span></span> | [<span data-ttu-id="f1147-141">Se restauró un canal</span><span class="sxs-lookup"><span data-stu-id="f1147-141">A channel was restored</span></span>](#channel-deleted) | <span data-ttu-id="f1147-142">Equipo</span><span class="sxs-lookup"><span data-stu-id="f1147-142">Team</span></span> |
| <span data-ttu-id="f1147-143">miembros agregados</span><span class="sxs-lookup"><span data-stu-id="f1147-143">members added</span></span>   | <span data-ttu-id="f1147-144">membersAdded</span><span class="sxs-lookup"><span data-stu-id="f1147-144">membersAdded</span></span>   | <span data-ttu-id="f1147-145">OnTeamsMembersAddedAsync</span><span class="sxs-lookup"><span data-stu-id="f1147-145">OnTeamsMembersAddedAsync</span></span>   | [<span data-ttu-id="f1147-146">Un miembro agregado</span><span class="sxs-lookup"><span data-stu-id="f1147-146">A member added</span></span>](#team-members-added)   | <span data-ttu-id="f1147-147">Todo</span><span class="sxs-lookup"><span data-stu-id="f1147-147">All</span></span> |
| <span data-ttu-id="f1147-148">miembros quitados</span><span class="sxs-lookup"><span data-stu-id="f1147-148">members removed</span></span> | <span data-ttu-id="f1147-149">membersRemoved</span><span class="sxs-lookup"><span data-stu-id="f1147-149">membersRemoved</span></span> | <span data-ttu-id="f1147-150">OnTeamsMembersRemovedAsync</span><span class="sxs-lookup"><span data-stu-id="f1147-150">OnTeamsMembersRemovedAsync</span></span> | [<span data-ttu-id="f1147-151">Se quitó un miembro</span><span class="sxs-lookup"><span data-stu-id="f1147-151">A member was removed</span></span>](#team-members-removed) | <span data-ttu-id="f1147-152">groupChat & team</span><span class="sxs-lookup"><span data-stu-id="f1147-152">groupChat & team</span></span> |
| <span data-ttu-id="f1147-153">se cambió el nombre del equipo</span><span class="sxs-lookup"><span data-stu-id="f1147-153">team renamed</span></span>        | <span data-ttu-id="f1147-154">teamRenamed</span><span class="sxs-lookup"><span data-stu-id="f1147-154">teamRenamed</span></span>       | <span data-ttu-id="f1147-155">OnTeamsTeamRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="f1147-155">OnTeamsTeamRenamedAsync</span></span>    | [<span data-ttu-id="f1147-156">Se cambió el nombre de un equipo</span><span class="sxs-lookup"><span data-stu-id="f1147-156">A Team was renamed</span></span>](#team-renamed)       | <span data-ttu-id="f1147-157">Equipo</span><span class="sxs-lookup"><span data-stu-id="f1147-157">Team</span></span> |
| <span data-ttu-id="f1147-158">equipo eliminado</span><span class="sxs-lookup"><span data-stu-id="f1147-158">team deleted</span></span>        | <span data-ttu-id="f1147-159">teamDeleted</span><span class="sxs-lookup"><span data-stu-id="f1147-159">teamDeleted</span></span>       | <span data-ttu-id="f1147-160">OnTeamsTeamDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="f1147-160">OnTeamsTeamDeletedAsync</span></span>    | [<span data-ttu-id="f1147-161">Se eliminó un equipo</span><span class="sxs-lookup"><span data-stu-id="f1147-161">A Team was deleted</span></span>](#team-deleted)       | <span data-ttu-id="f1147-162">Equipo</span><span class="sxs-lookup"><span data-stu-id="f1147-162">Team</span></span> |
| <span data-ttu-id="f1147-163">equipo archivado</span><span class="sxs-lookup"><span data-stu-id="f1147-163">team archived</span></span>        | <span data-ttu-id="f1147-164">teamArchived</span><span class="sxs-lookup"><span data-stu-id="f1147-164">teamArchived</span></span>       | <span data-ttu-id="f1147-165">OnTeamsTeamArchivedAsync</span><span class="sxs-lookup"><span data-stu-id="f1147-165">OnTeamsTeamArchivedAsync</span></span>    | [<span data-ttu-id="f1147-166">Se archivó un equipo</span><span class="sxs-lookup"><span data-stu-id="f1147-166">A Team was archived</span></span>](#team-archived)       | <span data-ttu-id="f1147-167">Equipo</span><span class="sxs-lookup"><span data-stu-id="f1147-167">Team</span></span> |
| <span data-ttu-id="f1147-168">equipo sin jerarquía</span><span class="sxs-lookup"><span data-stu-id="f1147-168">team unarchived</span></span>        | <span data-ttu-id="f1147-169">teamUnarchived</span><span class="sxs-lookup"><span data-stu-id="f1147-169">teamUnarchived</span></span>       | <span data-ttu-id="f1147-170">OnTeamsTeamUnarchivedAsync</span><span class="sxs-lookup"><span data-stu-id="f1147-170">OnTeamsTeamUnarchivedAsync</span></span>    | [<span data-ttu-id="f1147-171">Un equipo no se harchivo</span><span class="sxs-lookup"><span data-stu-id="f1147-171">A Team was unarchived</span></span>](#team-unarchived)       | <span data-ttu-id="f1147-172">Equipo</span><span class="sxs-lookup"><span data-stu-id="f1147-172">Team</span></span> |
| <span data-ttu-id="f1147-173">equipo restaurado</span><span class="sxs-lookup"><span data-stu-id="f1147-173">team restored</span></span>        | <span data-ttu-id="f1147-174">teamRestored</span><span class="sxs-lookup"><span data-stu-id="f1147-174">teamRestored</span></span>      | <span data-ttu-id="f1147-175">OnTeamsTeamRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="f1147-175">OnTeamsTeamRestoredAsync</span></span>    | [<span data-ttu-id="f1147-176">Se restauró un equipo</span><span class="sxs-lookup"><span data-stu-id="f1147-176">A Team was restored</span></span>](#team-restored)       | <span data-ttu-id="f1147-177">Equipo</span><span class="sxs-lookup"><span data-stu-id="f1147-177">Team</span></span> |

### <a name="channel-created"></a><span data-ttu-id="f1147-178">Canal creado</span><span class="sxs-lookup"><span data-stu-id="f1147-178">Channel created</span></span>

<span data-ttu-id="f1147-179">El evento de canal creado se envía al bot cada vez que se crea un nuevo canal en un equipo en el que está instalado el bot.</span><span class="sxs-lookup"><span data-stu-id="f1147-179">The channel created event is sent to your bot whenever a new channel is created in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f1147-180">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f1147-180">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f1147-181">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f1147-181">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f1147-182">JSON</span><span class="sxs-lookup"><span data-stu-id="f1147-182">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="f1147-183">Python</span><span class="sxs-lookup"><span data-stu-id="f1147-183">Python</span></span>](#tab/python)

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

### <a name="channel-renamed"></a><span data-ttu-id="f1147-184">Se cambió el nombre del canal</span><span class="sxs-lookup"><span data-stu-id="f1147-184">Channel renamed</span></span>

<span data-ttu-id="f1147-185">El evento de cambio de nombre de canal se envía al bot siempre que se cambie el nombre de un canal en un equipo en el que esté instalado el bot.</span><span class="sxs-lookup"><span data-stu-id="f1147-185">The channel renamed event is sent to your bot whenever a channel is renamed in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f1147-186">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f1147-186">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f1147-187">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f1147-187">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f1147-188">JSON</span><span class="sxs-lookup"><span data-stu-id="f1147-188">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="f1147-189">Python</span><span class="sxs-lookup"><span data-stu-id="f1147-189">Python</span></span>](#tab/python)

```python
async def on_teams_channel_renamed(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new channel name is {channel_info.name}")
    )
```

* * *

### <a name="channel-deleted"></a><span data-ttu-id="f1147-190">Canal eliminado</span><span class="sxs-lookup"><span data-stu-id="f1147-190">Channel Deleted</span></span>

<span data-ttu-id="f1147-191">El evento de eliminación de canal se envía al bot cada vez que se elimina un canal en un equipo en el que está instalado el bot.</span><span class="sxs-lookup"><span data-stu-id="f1147-191">The channel deleted event is sent to your bot whenever a channel is deleted in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f1147-192">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f1147-192">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f1147-193">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f1147-193">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f1147-194">JSON</span><span class="sxs-lookup"><span data-stu-id="f1147-194">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="f1147-195">Python</span><span class="sxs-lookup"><span data-stu-id="f1147-195">Python</span></span>](#tab/python)

```python
async def on_teams_channel_deleted(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The deleted channel is {channel_info.name}")
    )
```

* * *

### <a name="channel-restored"></a><span data-ttu-id="f1147-196">Canal restaurado</span><span class="sxs-lookup"><span data-stu-id="f1147-196">Channel restored</span></span>

<span data-ttu-id="f1147-197">El evento restaurado del canal se envía al bot cada vez que se restaura un canal que se eliminó anteriormente en un equipo en el que el bot ya está instalado.</span><span class="sxs-lookup"><span data-stu-id="f1147-197">The channel restored event is sent to your bot whenever a channel that was previously deleted is restored in a team that your bot is already installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f1147-198">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f1147-198">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRestoredAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel restored.");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f1147-199">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f1147-199">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f1147-200">JSON</span><span class="sxs-lookup"><span data-stu-id="f1147-200">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="f1147-201">Python</span><span class="sxs-lookup"><span data-stu-id="f1147-201">Python</span></span>](#tab/python)

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

### <a name="team-members-added"></a><span data-ttu-id="f1147-202">Se agregaron miembros del equipo</span><span class="sxs-lookup"><span data-stu-id="f1147-202">Team members added</span></span>

<span data-ttu-id="f1147-203">El evento se envía al bot la primera vez que se agrega a una conversación y cada vez que se agrega un nuevo usuario a un chat de grupo o equipo en el que está instalado el `teamMemberAdded` bot.</span><span class="sxs-lookup"><span data-stu-id="f1147-203">The `teamMemberAdded` event is sent to your bot the first time it is added to a conversation and every time a new user is added to a team or group chat that your bot is installed in.</span></span> <span data-ttu-id="f1147-204">La información de usuario (ID) es única para el bot y puede almacenarse en caché para que el servicio la use en el futuro (por ejemplo, enviar un mensaje a un usuario específico).</span><span class="sxs-lookup"><span data-stu-id="f1147-204">The user information (ID) is unique for your bot and can be cached for future use by your service (such as sending a message to a specific user).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f1147-205">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f1147-205">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f1147-206">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f1147-206">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f1147-207">JSON</span><span class="sxs-lookup"><span data-stu-id="f1147-207">JSON</span></span>](#tab/json)

<span data-ttu-id="f1147-208">Este es el mensaje que el bot recibirá cuando el bot se agrega **a un equipo.**</span><span class="sxs-lookup"><span data-stu-id="f1147-208">This is the message your bot will receive when the bot is added **to a team**.</span></span>

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

<span data-ttu-id="f1147-209">Este es el mensaje que el bot recibirá cuando el bot se agrega \* a un *chat uno a uno.*</span><span class="sxs-lookup"><span data-stu-id="f1147-209">This is the message your bot will receive when the bot is added \**to a one-to-one chat*.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="f1147-210">Python</span><span class="sxs-lookup"><span data-stu-id="f1147-210">Python</span></span>](#tab/python)

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

<span data-ttu-id="f1147-211">_ \* \*</span><span class="sxs-lookup"><span data-stu-id="f1147-211">_ \* \*</span></span>

### <a name="team-members-removed"></a><span data-ttu-id="f1147-212">Miembros del equipo eliminados</span><span class="sxs-lookup"><span data-stu-id="f1147-212">Team members removed</span></span>

<span data-ttu-id="f1147-213">El evento se envía al bot si se quita de un equipo y cada vez que se quita un usuario de un equipo del que el `teamMemberRemoved` bot es miembro.</span><span class="sxs-lookup"><span data-stu-id="f1147-213">The `teamMemberRemoved` event is sent to your bot if it is removed from a team and every time any user is removed from a team that your bot is a member of.</span></span> <span data-ttu-id="f1147-214">Puede determinar si el nuevo miembro quitado era el propio bot o un usuario mirando el `Activity` objeto del `turnContext` archivo .</span><span class="sxs-lookup"><span data-stu-id="f1147-214">You can determine if the new member removed was the bot itself or a user by looking at the `Activity` object of the `turnContext`.</span></span>  <span data-ttu-id="f1147-215">Si el campo del objeto es el mismo que el campo del objeto, el miembro quitado es el bot; de lo `Id` `MembersRemoved` `Id` `Recipient` contrario, es un usuario.</span><span class="sxs-lookup"><span data-stu-id="f1147-215">If the `Id` field of the `MembersRemoved` object is the same as the `Id` field of the `Recipient` object, then the member removed is the bot, otherwise, it is a user.</span></span>  <span data-ttu-id="f1147-216">Por lo `Id` general, los bots serán: `28:<MicrosoftAppId>`</span><span class="sxs-lookup"><span data-stu-id="f1147-216">The bot's `Id` will generally be: `28:<MicrosoftAppId>`</span></span>

[!Note] <span data-ttu-id="f1147-217">Cuando un usuario se elimina permanentemente de un inquilino, `membersRemoved conversationUpdate` se desencadena el evento.</span><span class="sxs-lookup"><span data-stu-id="f1147-217">When a user is permanently deleted from a tenant, `membersRemoved conversationUpdate` event is triggered.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f1147-218">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f1147-218">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f1147-219">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f1147-219">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f1147-220">JSON</span><span class="sxs-lookup"><span data-stu-id="f1147-220">JSON</span></span>](#tab/json)

<span data-ttu-id="f1147-221">El objeto del siguiente ejemplo de carga se basa en agregar un miembro a un equipo en lugar de un chat grupal o iniciar una nueva conversación uno `channelData` a uno:</span><span class="sxs-lookup"><span data-stu-id="f1147-221">The `channelData` object in the following payload example is based on adding a member to a team rather than a group chat, or initiating a new one-to-one conversation:</span></span>

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


# <a name="python"></a>[<span data-ttu-id="f1147-222">Python</span><span class="sxs-lookup"><span data-stu-id="f1147-222">Python</span></span>](#tab/python)

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

### <a name="team-renamed"></a><span data-ttu-id="f1147-223">Se cambió el nombre del equipo</span><span class="sxs-lookup"><span data-stu-id="f1147-223">Team renamed</span></span>

<span data-ttu-id="f1147-224">El bot recibe una notificación cuando se ha cambiado el nombre del equipo en el que se encuentra.</span><span class="sxs-lookup"><span data-stu-id="f1147-224">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="f1147-225">Recibe un `conversationUpdate` evento con en el `eventType.teamRenamed` `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="f1147-225">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f1147-226">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f1147-226">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f1147-227">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f1147-227">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f1147-228">JSON</span><span class="sxs-lookup"><span data-stu-id="f1147-228">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="f1147-229">Python</span><span class="sxs-lookup"><span data-stu-id="f1147-229">Python</span></span>](#tab/python)

```python
async def on_teams_team_renamed(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new team name is {team_info.name}")
    )
```

* * *

### <a name="team-deleted"></a><span data-ttu-id="f1147-230">Equipo eliminado</span><span class="sxs-lookup"><span data-stu-id="f1147-230">Team deleted</span></span>

<span data-ttu-id="f1147-231">El bot recibe una notificación cuando se ha eliminado el equipo en el que se encuentra.</span><span class="sxs-lookup"><span data-stu-id="f1147-231">Your bot is notified when the team it is in has been deleted.</span></span> <span data-ttu-id="f1147-232">Recibe un `conversationUpdate` evento con en el `eventType.teamDeleted` `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="f1147-232">It receives a `conversationUpdate` event with `eventType.teamDeleted` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f1147-233">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f1147-233">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamDeletedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    //handle delete event
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f1147-234">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f1147-234">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamDeletedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            //handle delete event
            await next();
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="f1147-235">JSON</span><span class="sxs-lookup"><span data-stu-id="f1147-235">JSON</span></span>](#tab/json)

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
        "eventType": "teamDeleted",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="f1147-236">Python</span><span class="sxs-lookup"><span data-stu-id="f1147-236">Python</span></span>](#tab/python)

```python
async def on_teams_team_deleted(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    //handle delete event
    )
```

* * *

### <a name="team-restored"></a><span data-ttu-id="f1147-237">Equipo restaurado</span><span class="sxs-lookup"><span data-stu-id="f1147-237">Team restored</span></span>

<span data-ttu-id="f1147-238">El bot recibe una notificación cuando se restaura desde la eliminación.</span><span class="sxs-lookup"><span data-stu-id="f1147-238">The bot receives a notification when it is restored from deletion.</span></span> <span data-ttu-id="f1147-239">Recibe un `conversationUpdate` evento con en el `eventType.teamrestored` `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="f1147-239">It receives a `conversationUpdate` event with `eventType.teamrestored` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f1147-240">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f1147-240">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamrestoredAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f1147-241">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f1147-241">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f1147-242">JSON</span><span class="sxs-lookup"><span data-stu-id="f1147-242">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="f1147-243">Python</span><span class="sxs-lookup"><span data-stu-id="f1147-243">Python</span></span>](#tab/python)

```python
async def on_teams_team_restored(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

### <a name="team-archived"></a><span data-ttu-id="f1147-244">Equipo archivado</span><span class="sxs-lookup"><span data-stu-id="f1147-244">Team archived</span></span>

<span data-ttu-id="f1147-245">El bot recibe una notificación cuando se archiva el equipo en el que está instalado.</span><span class="sxs-lookup"><span data-stu-id="f1147-245">The bot receives a notification when the team it is installed in is archived.</span></span> <span data-ttu-id="f1147-246">Recibe un `conversationUpdate` evento con en el `eventType.teamarchived` `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="f1147-246">It receives a `conversationUpdate` event with `eventType.teamarchived` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f1147-247">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f1147-247">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamArchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f1147-248">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f1147-248">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f1147-249">JSON</span><span class="sxs-lookup"><span data-stu-id="f1147-249">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="f1147-250">Python</span><span class="sxs-lookup"><span data-stu-id="f1147-250">Python</span></span>](#tab/python)

```python
async def on_teams_team_archived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *


### <a name="team-unarchived"></a><span data-ttu-id="f1147-251">Equipo sin jerarquía</span><span class="sxs-lookup"><span data-stu-id="f1147-251">Team unarchived</span></span>

<span data-ttu-id="f1147-252">El bot recibe una notificación cuando el equipo en el que está instalado no se harchivo.</span><span class="sxs-lookup"><span data-stu-id="f1147-252">The bot receives a notification when the team it is installed in is unarchived.</span></span> <span data-ttu-id="f1147-253">Recibe un `conversationUpdate` evento con en el `eventType.teamUnarchived` `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="f1147-253">It receives a `conversationUpdate` event with `eventType.teamUnarchived` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f1147-254">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f1147-254">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamUnarchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f1147-255">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f1147-255">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamUnarchivedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team archived', `${teamInfo.name} is the team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="f1147-256">JSON</span><span class="sxs-lookup"><span data-stu-id="f1147-256">JSON</span></span>](#tab/json)

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
        "eventType": "teamUnarchived",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="f1147-257">Python</span><span class="sxs-lookup"><span data-stu-id="f1147-257">Python</span></span>](#tab/python)

```python
async def on_teams_team_unarchived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

## <a name="message-reaction-events"></a><span data-ttu-id="f1147-258">Eventos de reacción de mensajes</span><span class="sxs-lookup"><span data-stu-id="f1147-258">Message reaction events</span></span>

<span data-ttu-id="f1147-259">El evento se envía cuando un usuario agrega o quita las reacción `messageReaction` a un mensaje enviado por el bot.</span><span class="sxs-lookup"><span data-stu-id="f1147-259">The `messageReaction` event is sent when a user adds or removes reactions to a message which was sent by your bot.</span></span> <span data-ttu-id="f1147-260">Contiene el identificador del mensaje específico y el tipo de reacción `replyToId` `Type` en formato de texto.</span><span class="sxs-lookup"><span data-stu-id="f1147-260">The `replyToId` contains the ID of the specific message, and the `Type` is the type of reaction in text format.</span></span>  <span data-ttu-id="f1147-261">Entre los tipos de reacción se incluyen: "resalte", "corazón", "desanualizado", "me gusta", "Lamentablemente", "sorpresa".</span><span class="sxs-lookup"><span data-stu-id="f1147-261">The types of reactions include: "angry", "heart", "laugh", "like", "Sad", "surprised".</span></span> <span data-ttu-id="f1147-262">Este evento no contiene el contenido del mensaje original, por lo que si el procesamiento de las reacción a los mensajes es importante para el bot, tendrá que almacenar los mensajes cuando los envíe.</span><span class="sxs-lookup"><span data-stu-id="f1147-262">This event does not contain the contents of the original message, so if processing reactions to your messages is important for your bot you'll need to store the messages when you send them.</span></span>

| <span data-ttu-id="f1147-263">EventType</span><span class="sxs-lookup"><span data-stu-id="f1147-263">EventType</span></span>       | <span data-ttu-id="f1147-264">Payload (objeto)</span><span class="sxs-lookup"><span data-stu-id="f1147-264">Payload object</span></span>   | <span data-ttu-id="f1147-265">Descripción</span><span class="sxs-lookup"><span data-stu-id="f1147-265">Description</span></span>                                                             | <span data-ttu-id="f1147-266">Ámbito</span><span class="sxs-lookup"><span data-stu-id="f1147-266">Scope</span></span> |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| <span data-ttu-id="f1147-267">messageReaction</span><span class="sxs-lookup"><span data-stu-id="f1147-267">messageReaction</span></span> | <span data-ttu-id="f1147-268">reactionsAdded</span><span class="sxs-lookup"><span data-stu-id="f1147-268">reactionsAdded</span></span>   | [<span data-ttu-id="f1147-269">Reacción al mensaje de bot</span><span class="sxs-lookup"><span data-stu-id="f1147-269">Reaction to bot message</span></span>](#reactions-to-a-bot-message)                   | <span data-ttu-id="f1147-270">Todo</span><span class="sxs-lookup"><span data-stu-id="f1147-270">All</span></span>   |
| <span data-ttu-id="f1147-271">messageReaction</span><span class="sxs-lookup"><span data-stu-id="f1147-271">messageReaction</span></span> | <span data-ttu-id="f1147-272">reactionsRemoved</span><span class="sxs-lookup"><span data-stu-id="f1147-272">reactionsRemoved</span></span> | [<span data-ttu-id="f1147-273">Reacción eliminada del mensaje de bot</span><span class="sxs-lookup"><span data-stu-id="f1147-273">Reaction removed from bot message</span></span>](#reactions-removed-from-bot-message) | <span data-ttu-id="f1147-274">Todo</span><span class="sxs-lookup"><span data-stu-id="f1147-274">All</span></span>   |

### <a name="reactions-to-a-bot-message"></a><span data-ttu-id="f1147-275">Reacción a un mensaje de bot</span><span class="sxs-lookup"><span data-stu-id="f1147-275">Reactions to a bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f1147-276">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f1147-276">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f1147-277">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f1147-277">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f1147-278">JSON</span><span class="sxs-lookup"><span data-stu-id="f1147-278">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="f1147-279">Python</span><span class="sxs-lookup"><span data-stu-id="f1147-279">Python</span></span>](#tab/python)

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

### <a name="reactions-removed-from-bot-message"></a><span data-ttu-id="f1147-280">Respuestas eliminadas del mensaje de bot</span><span class="sxs-lookup"><span data-stu-id="f1147-280">Reactions removed from bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f1147-281">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f1147-281">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f1147-282">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f1147-282">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f1147-283">JSON</span><span class="sxs-lookup"><span data-stu-id="f1147-283">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="f1147-284">Python</span><span class="sxs-lookup"><span data-stu-id="f1147-284">Python</span></span>](#tab/python)

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

## <a name="samples"></a><span data-ttu-id="f1147-285">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="f1147-285">Samples</span></span>
<span data-ttu-id="f1147-286">Para obtener código de ejemplo que muestre los eventos de conversación de bots, vea:</span><span class="sxs-lookup"><span data-stu-id="f1147-286">For sample code showing the bots conversation events, see:</span></span>

[<span data-ttu-id="f1147-287">Ejemplo de eventos de conversación de bots de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f1147-287">Microsoft Teams bots conversation events sample</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)




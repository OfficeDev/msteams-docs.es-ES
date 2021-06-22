---
title: Eventos de conversación
author: WashingtonKayaker
description: Cómo trabajar con eventos de conversación desde el Microsoft Teams bot.
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 39d3a6d54b275fd6b9f28eb38b124435e9ba8bfd
ms.sourcegitcommit: 3d02dfc13331b28cffba42b39560cfeb1503abe2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/22/2021
ms.locfileid: "53049052"
---
# <a name="conversation-events-in-your-teams-bot"></a><span data-ttu-id="4c714-103">Eventos de conversación en el bot de Teams</span><span class="sxs-lookup"><span data-stu-id="4c714-103">Conversation events in your Teams bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="4c714-104">Al crear los bots de conversación para Microsoft Teams, puede trabajar con eventos de conversación.</span><span class="sxs-lookup"><span data-stu-id="4c714-104">When building your conversational bots for Microsoft Teams, you can work with conversation events.</span></span> <span data-ttu-id="4c714-105">Teams envía notificaciones al bot para eventos de conversación que se suceden en ámbitos donde el bot está activo.</span><span class="sxs-lookup"><span data-stu-id="4c714-105">Teams sends notifications to your bot for conversation events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="4c714-106">Puede capturar estos eventos en el código y realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="4c714-106">You can capture these events in your code and take the following actions:</span></span>

* <span data-ttu-id="4c714-107">Desencadena un mensaje de bienvenida cuando el bot se agrega a un equipo.</span><span class="sxs-lookup"><span data-stu-id="4c714-107">Trigger a welcome message when your bot is added to a team.</span></span>
* <span data-ttu-id="4c714-108">Desencadena un mensaje de bienvenida cuando se agrega o quita un nuevo miembro del equipo.</span><span class="sxs-lookup"><span data-stu-id="4c714-108">Trigger a welcome message when a new team member is added or removed.</span></span>
* <span data-ttu-id="4c714-109">Desencadena una notificación cuando se crea, cambia el nombre o elimina un canal.</span><span class="sxs-lookup"><span data-stu-id="4c714-109">Trigger a notification when a channel is created, renamed, or deleted.</span></span>
* <span data-ttu-id="4c714-110">Cuando un usuario le gusta un mensaje de bot.</span><span class="sxs-lookup"><span data-stu-id="4c714-110">When a bot message is liked by a user.</span></span>

## <a name="conversation-update-events"></a><span data-ttu-id="4c714-111">Eventos de actualización de conversación</span><span class="sxs-lookup"><span data-stu-id="4c714-111">Conversation update events</span></span>

<span data-ttu-id="4c714-112">Puedes usar eventos de actualización de conversación para proporcionar mejores notificaciones y acciones de bot más eficaces.</span><span class="sxs-lookup"><span data-stu-id="4c714-112">You can use conversation update events to provide better notifications and more effective bot actions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="4c714-113">Puedes agregar eventos nuevos en cualquier momento y el bot comienza a recibirlos.</span><span class="sxs-lookup"><span data-stu-id="4c714-113">You can add new events any time and your bot begins to receive them.</span></span>
> * <span data-ttu-id="4c714-114">Debe diseñar el bot para recibir eventos inesperados.</span><span class="sxs-lookup"><span data-stu-id="4c714-114">You must design your bot to receive unexpected events.</span></span>
> * <span data-ttu-id="4c714-115">Si usa el SDK de Bot Framework, el bot responde automáticamente con un a a los eventos `200 - OK` que decida no controlar.</span><span class="sxs-lookup"><span data-stu-id="4c714-115">If you are using the Bot Framework SDK, your bot automatically responds with a `200 - OK` to any events you choose not to handle.</span></span>

<span data-ttu-id="4c714-116">Un bot recibe un `conversationUpdate` evento en cualquiera de los siguientes casos:</span><span class="sxs-lookup"><span data-stu-id="4c714-116">A bot receives a `conversationUpdate` event in either of the following cases:</span></span>

* <span data-ttu-id="4c714-117">Cuando el bot se ha agregado a una conversación.</span><span class="sxs-lookup"><span data-stu-id="4c714-117">When bot has been added to a conversation.</span></span>
* <span data-ttu-id="4c714-118">Otros miembros se agregan o quitan de una conversación.</span><span class="sxs-lookup"><span data-stu-id="4c714-118">Other members are added to or removed from a conversation.</span></span>
* <span data-ttu-id="4c714-119">Los metadatos de conversación han cambiado.</span><span class="sxs-lookup"><span data-stu-id="4c714-119">Conversation metadata has changed.</span></span>

<span data-ttu-id="4c714-120">El evento `conversationUpdate` se envía al bot cuando recibe información sobre las actualizaciones de suscripción de los equipos donde se ha agregado.</span><span class="sxs-lookup"><span data-stu-id="4c714-120">The `conversationUpdate` event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="4c714-121">También recibe una actualización cuando se ha agregado por primera vez para conversaciones personales.</span><span class="sxs-lookup"><span data-stu-id="4c714-121">It also receives an update when it has been added for the first time for personal conversations.</span></span>

<span data-ttu-id="4c714-122">En la tabla siguiente se muestra una lista de Teams eventos de actualización de conversación con más detalles:</span><span class="sxs-lookup"><span data-stu-id="4c714-122">The following table shows a list of Teams conversation update events with more details:</span></span>

| <span data-ttu-id="4c714-123">Acción realizada</span><span class="sxs-lookup"><span data-stu-id="4c714-123">Action taken</span></span>        | <span data-ttu-id="4c714-124">EventType</span><span class="sxs-lookup"><span data-stu-id="4c714-124">EventType</span></span>         | <span data-ttu-id="4c714-125">Método llamado</span><span class="sxs-lookup"><span data-stu-id="4c714-125">Method called</span></span>              | <span data-ttu-id="4c714-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="4c714-126">Description</span></span>                | <span data-ttu-id="4c714-127">Ámbito</span><span class="sxs-lookup"><span data-stu-id="4c714-127">Scope</span></span> |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| <span data-ttu-id="4c714-128">Canal creado</span><span class="sxs-lookup"><span data-stu-id="4c714-128">Channel created</span></span>     | <span data-ttu-id="4c714-129">channelCreated</span><span class="sxs-lookup"><span data-stu-id="4c714-129">channelCreated</span></span>    | <span data-ttu-id="4c714-130">OnTeamsChannelCreatedAsync</span><span class="sxs-lookup"><span data-stu-id="4c714-130">OnTeamsChannelCreatedAsync</span></span> | <span data-ttu-id="4c714-131">[Se crea un canal](#channel-created).</span><span class="sxs-lookup"><span data-stu-id="4c714-131">[A channel is created](#channel-created).</span></span> | <span data-ttu-id="4c714-132">Equipo</span><span class="sxs-lookup"><span data-stu-id="4c714-132">Team</span></span> |
| <span data-ttu-id="4c714-133">Cambio de nombre del canal</span><span class="sxs-lookup"><span data-stu-id="4c714-133">Channel renamed</span></span>     | <span data-ttu-id="4c714-134">channelRenamed</span><span class="sxs-lookup"><span data-stu-id="4c714-134">channelRenamed</span></span>    | <span data-ttu-id="4c714-135">OnTeamsChannelRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="4c714-135">OnTeamsChannelRenamedAsync</span></span> | <span data-ttu-id="4c714-136">[Se cambia el nombre de un canal](#channel-renamed).</span><span class="sxs-lookup"><span data-stu-id="4c714-136">[A channel is renamed](#channel-renamed).</span></span> | <span data-ttu-id="4c714-137">Equipo</span><span class="sxs-lookup"><span data-stu-id="4c714-137">Team</span></span> |
| <span data-ttu-id="4c714-138">Canal eliminado</span><span class="sxs-lookup"><span data-stu-id="4c714-138">Channel deleted</span></span>     | <span data-ttu-id="4c714-139">channelDeleted</span><span class="sxs-lookup"><span data-stu-id="4c714-139">channelDeleted</span></span>    | <span data-ttu-id="4c714-140">OnTeamsChannelDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="4c714-140">OnTeamsChannelDeletedAsync</span></span> | <span data-ttu-id="4c714-141">[Se elimina un canal](#channel-deleted).</span><span class="sxs-lookup"><span data-stu-id="4c714-141">[A channel is deleted](#channel-deleted).</span></span> | <span data-ttu-id="4c714-142">Equipo</span><span class="sxs-lookup"><span data-stu-id="4c714-142">Team</span></span> |
| <span data-ttu-id="4c714-143">Canal restaurado</span><span class="sxs-lookup"><span data-stu-id="4c714-143">Channel restored</span></span>    | <span data-ttu-id="4c714-144">channelRestored</span><span class="sxs-lookup"><span data-stu-id="4c714-144">channelRestored</span></span>    | <span data-ttu-id="4c714-145">OnTeamsChannelRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="4c714-145">OnTeamsChannelRestoredAsync</span></span> | <span data-ttu-id="4c714-146">[Se restaura un canal](#channel-deleted).</span><span class="sxs-lookup"><span data-stu-id="4c714-146">[A channel is restored](#channel-deleted).</span></span> | <span data-ttu-id="4c714-147">Equipo</span><span class="sxs-lookup"><span data-stu-id="4c714-147">Team</span></span> |
| <span data-ttu-id="4c714-148">Miembros agregados</span><span class="sxs-lookup"><span data-stu-id="4c714-148">Members added</span></span>   | <span data-ttu-id="4c714-149">membersAdded</span><span class="sxs-lookup"><span data-stu-id="4c714-149">membersAdded</span></span>   | <span data-ttu-id="4c714-150">OnTeamsMembersAddedAsync</span><span class="sxs-lookup"><span data-stu-id="4c714-150">OnTeamsMembersAddedAsync</span></span>   | <span data-ttu-id="4c714-151">[Se agrega un miembro](#team-members-added).</span><span class="sxs-lookup"><span data-stu-id="4c714-151">[A member is added](#team-members-added).</span></span> | <span data-ttu-id="4c714-152">Todo</span><span class="sxs-lookup"><span data-stu-id="4c714-152">All</span></span> |
| <span data-ttu-id="4c714-153">Miembros eliminados</span><span class="sxs-lookup"><span data-stu-id="4c714-153">Members removed</span></span> | <span data-ttu-id="4c714-154">membersRemoved</span><span class="sxs-lookup"><span data-stu-id="4c714-154">membersRemoved</span></span> | <span data-ttu-id="4c714-155">OnTeamsMembersRemovedAsync</span><span class="sxs-lookup"><span data-stu-id="4c714-155">OnTeamsMembersRemovedAsync</span></span> | <span data-ttu-id="4c714-156">[Se quita un miembro](#team-members-removed).</span><span class="sxs-lookup"><span data-stu-id="4c714-156">[A member is removed](#team-members-removed).</span></span> | <span data-ttu-id="4c714-157">groupChat y equipo</span><span class="sxs-lookup"><span data-stu-id="4c714-157">groupChat and team</span></span> |
| <span data-ttu-id="4c714-158">Cambio de nombre de equipo</span><span class="sxs-lookup"><span data-stu-id="4c714-158">Team renamed</span></span>        | <span data-ttu-id="4c714-159">teamRenamed</span><span class="sxs-lookup"><span data-stu-id="4c714-159">teamRenamed</span></span>       | <span data-ttu-id="4c714-160">OnTeamsTeamRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="4c714-160">OnTeamsTeamRenamedAsync</span></span>    | <span data-ttu-id="4c714-161">[Se cambia el nombre de un equipo](#team-renamed).</span><span class="sxs-lookup"><span data-stu-id="4c714-161">[A team is renamed](#team-renamed).</span></span>       | <span data-ttu-id="4c714-162">Equipo</span><span class="sxs-lookup"><span data-stu-id="4c714-162">Team</span></span> |
| <span data-ttu-id="4c714-163">Equipo eliminado</span><span class="sxs-lookup"><span data-stu-id="4c714-163">Team deleted</span></span>        | <span data-ttu-id="4c714-164">teamDeleted</span><span class="sxs-lookup"><span data-stu-id="4c714-164">teamDeleted</span></span>       | <span data-ttu-id="4c714-165">OnTeamsTeamDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="4c714-165">OnTeamsTeamDeletedAsync</span></span>    | <span data-ttu-id="4c714-166">[Se elimina un equipo](#team-deleted).</span><span class="sxs-lookup"><span data-stu-id="4c714-166">[A team is deleted](#team-deleted).</span></span>       | <span data-ttu-id="4c714-167">Equipo</span><span class="sxs-lookup"><span data-stu-id="4c714-167">Team</span></span> |
| <span data-ttu-id="4c714-168">Equipo archivado</span><span class="sxs-lookup"><span data-stu-id="4c714-168">Team archived</span></span>        | <span data-ttu-id="4c714-169">teamArchived</span><span class="sxs-lookup"><span data-stu-id="4c714-169">teamArchived</span></span>       | <span data-ttu-id="4c714-170">OnTeamsTeamArchivedAsync</span><span class="sxs-lookup"><span data-stu-id="4c714-170">OnTeamsTeamArchivedAsync</span></span>    | <span data-ttu-id="4c714-171">[Se archiva un equipo](#team-archived).</span><span class="sxs-lookup"><span data-stu-id="4c714-171">[A team is archived](#team-archived).</span></span>       | <span data-ttu-id="4c714-172">Equipo</span><span class="sxs-lookup"><span data-stu-id="4c714-172">Team</span></span> |
| <span data-ttu-id="4c714-173">Equipo sin jerarquía</span><span class="sxs-lookup"><span data-stu-id="4c714-173">Team unarchived</span></span>        | <span data-ttu-id="4c714-174">teamUnarchived</span><span class="sxs-lookup"><span data-stu-id="4c714-174">teamUnarchived</span></span>       | <span data-ttu-id="4c714-175">OnTeamsTeamUnarchivedAsync</span><span class="sxs-lookup"><span data-stu-id="4c714-175">OnTeamsTeamUnarchivedAsync</span></span>    | <span data-ttu-id="4c714-176">[Un equipo no está anárquico.](#team-unarchived)</span><span class="sxs-lookup"><span data-stu-id="4c714-176">[A team is unarchived](#team-unarchived).</span></span>       | <span data-ttu-id="4c714-177">Equipo</span><span class="sxs-lookup"><span data-stu-id="4c714-177">Team</span></span> |
| <span data-ttu-id="4c714-178">Equipo restaurado</span><span class="sxs-lookup"><span data-stu-id="4c714-178">Team restored</span></span>        | <span data-ttu-id="4c714-179">teamRestored</span><span class="sxs-lookup"><span data-stu-id="4c714-179">teamRestored</span></span>      | <span data-ttu-id="4c714-180">OnTeamsTeamRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="4c714-180">OnTeamsTeamRestoredAsync</span></span>    | [<span data-ttu-id="4c714-181">Se restaura un equipo</span><span class="sxs-lookup"><span data-stu-id="4c714-181">A team is restored</span></span>](#team-restored)       | <span data-ttu-id="4c714-182">Equipo</span><span class="sxs-lookup"><span data-stu-id="4c714-182">Team</span></span> |

### <a name="channel-created"></a><span data-ttu-id="4c714-183">Canal creado</span><span class="sxs-lookup"><span data-stu-id="4c714-183">Channel created</span></span>

<span data-ttu-id="4c714-184">El evento de canal creado se envía al bot cada vez que se crea un nuevo canal en un equipo donde está instalado el bot.</span><span class="sxs-lookup"><span data-stu-id="4c714-184">The channel created event is sent to your bot whenever a new channel is created in a team where your bot is installed.</span></span>

<span data-ttu-id="4c714-185">El siguiente código muestra un ejemplo de evento creado por el canal:</span><span class="sxs-lookup"><span data-stu-id="4c714-185">The following code shows an example of channel created event:</span></span>

# <a name="c"></a>[<span data-ttu-id="4c714-186">C#</span><span class="sxs-lookup"><span data-stu-id="4c714-186">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="4c714-187">TypeScript</span><span class="sxs-lookup"><span data-stu-id="4c714-187">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="4c714-188">JSON</span><span class="sxs-lookup"><span data-stu-id="4c714-188">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="4c714-189">Python</span><span class="sxs-lookup"><span data-stu-id="4c714-189">Python</span></span>](#tab/python)

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

---

### <a name="channel-renamed"></a><span data-ttu-id="4c714-190">Cambio de nombre del canal</span><span class="sxs-lookup"><span data-stu-id="4c714-190">Channel renamed</span></span>

<span data-ttu-id="4c714-191">El evento de cambio de nombre de canal se envía al bot siempre que se cambie el nombre de un canal en un equipo donde esté instalado el bot.</span><span class="sxs-lookup"><span data-stu-id="4c714-191">The channel renamed event is sent to your bot whenever a channel is renamed in a team where your bot is installed.</span></span>

<span data-ttu-id="4c714-192">El siguiente código muestra un ejemplo de evento con el nombre de canal:</span><span class="sxs-lookup"><span data-stu-id="4c714-192">The following code shows an example of channel renamed event:</span></span>

# <a name="c"></a>[<span data-ttu-id="4c714-193">C#</span><span class="sxs-lookup"><span data-stu-id="4c714-193">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="4c714-194">TypeScript</span><span class="sxs-lookup"><span data-stu-id="4c714-194">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="4c714-195">JSON</span><span class="sxs-lookup"><span data-stu-id="4c714-195">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="4c714-196">Python</span><span class="sxs-lookup"><span data-stu-id="4c714-196">Python</span></span>](#tab/python)

```python
async def on_teams_channel_renamed(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new channel name is {channel_info.name}")
    )
```

---

### <a name="channel-deleted"></a><span data-ttu-id="4c714-197">Canal eliminado</span><span class="sxs-lookup"><span data-stu-id="4c714-197">Channel deleted</span></span>

<span data-ttu-id="4c714-198">El evento de eliminación de canal se envía al bot cada vez que se elimina un canal en un equipo donde está instalado el bot.</span><span class="sxs-lookup"><span data-stu-id="4c714-198">The channel deleted event is sent to your bot whenever a channel is deleted in a team where your bot is installed.</span></span>

<span data-ttu-id="4c714-199">El siguiente código muestra un ejemplo de evento eliminado del canal:</span><span class="sxs-lookup"><span data-stu-id="4c714-199">The following code shows an example of channel deleted event:</span></span>

# <a name="c"></a>[<span data-ttu-id="4c714-200">C#</span><span class="sxs-lookup"><span data-stu-id="4c714-200">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="4c714-201">TypeScript</span><span class="sxs-lookup"><span data-stu-id="4c714-201">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="4c714-202">JSON</span><span class="sxs-lookup"><span data-stu-id="4c714-202">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="4c714-203">Python</span><span class="sxs-lookup"><span data-stu-id="4c714-203">Python</span></span>](#tab/python)

```python
async def on_teams_channel_deleted(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The deleted channel is {channel_info.name}")
    )
```

---

### <a name="channel-restored"></a><span data-ttu-id="4c714-204">Canal restaurado</span><span class="sxs-lookup"><span data-stu-id="4c714-204">Channel restored</span></span>

<span data-ttu-id="4c714-205">El evento restaurado del canal se envía al bot cada vez que se restaura un canal que se eliminó anteriormente en un equipo en el que el bot ya está instalado.</span><span class="sxs-lookup"><span data-stu-id="4c714-205">The channel restored event is sent to your bot whenever a channel that was previously deleted is restored in a team where your bot is already installed.</span></span>

<span data-ttu-id="4c714-206">El código siguiente muestra un ejemplo de evento restaurado del canal:</span><span class="sxs-lookup"><span data-stu-id="4c714-206">The following code shows an example of channel restored event:</span></span>

# <a name="c"></a>[<span data-ttu-id="4c714-207">C#</span><span class="sxs-lookup"><span data-stu-id="4c714-207">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRestoredAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel restored.");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="4c714-208">TypeScript</span><span class="sxs-lookup"><span data-stu-id="4c714-208">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="4c714-209">JSON</span><span class="sxs-lookup"><span data-stu-id="4c714-209">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="4c714-210">Python</span><span class="sxs-lookup"><span data-stu-id="4c714-210">Python</span></span>](#tab/python)

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

---

### <a name="team-members-added"></a><span data-ttu-id="4c714-211">Miembros del equipo agregados</span><span class="sxs-lookup"><span data-stu-id="4c714-211">Team members added</span></span>

<span data-ttu-id="4c714-212">El evento se envía al bot la primera vez que se `teamMemberAdded` agrega a una conversación.</span><span class="sxs-lookup"><span data-stu-id="4c714-212">The `teamMemberAdded` event is sent to your bot the first time it is added to a conversation.</span></span> <span data-ttu-id="4c714-213">El evento se envía al bot cada vez que se agrega un nuevo usuario a un chat de grupo o equipo donde está instalado el bot.</span><span class="sxs-lookup"><span data-stu-id="4c714-213">The event is sent to your bot every time a new user is added to a team or group chat where your bot is installed.</span></span> <span data-ttu-id="4c714-214">La información del usuario que es id. es única para el bot y puede almacenarse en caché para su uso futuro por el servicio, como enviar un mensaje a un usuario específico.</span><span class="sxs-lookup"><span data-stu-id="4c714-214">The user information that is ID is unique for your bot and can be cached for future use by your service, such as sending a message to a specific user.</span></span>

<span data-ttu-id="4c714-215">El código siguiente muestra un ejemplo de evento agregado por los miembros del equipo:</span><span class="sxs-lookup"><span data-stu-id="4c714-215">The following code shows an example of team members added event:</span></span>

# <a name="c"></a>[<span data-ttu-id="4c714-216">C#</span><span class="sxs-lookup"><span data-stu-id="4c714-216">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="4c714-217">TypeScript</span><span class="sxs-lookup"><span data-stu-id="4c714-217">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="4c714-218">JSON</span><span class="sxs-lookup"><span data-stu-id="4c714-218">JSON</span></span>](#tab/json)

<span data-ttu-id="4c714-219">Este es el mensaje que el bot recibe cuando se agrega el bot a un equipo.</span><span class="sxs-lookup"><span data-stu-id="4c714-219">This is the message your bot receives when the bot is added to a team.</span></span>

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

<span data-ttu-id="4c714-220">Este es el mensaje que el bot recibe cuando se agrega el bot a un chat uno a uno.</span><span class="sxs-lookup"><span data-stu-id="4c714-220">This is the message your bot receives when the bot is added to a one-to-one chat.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="4c714-221">Python</span><span class="sxs-lookup"><span data-stu-id="4c714-221">Python</span></span>](#tab/python)

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

---

### <a name="team-members-removed"></a><span data-ttu-id="4c714-222">Miembros del equipo eliminados</span><span class="sxs-lookup"><span data-stu-id="4c714-222">Team members removed</span></span>

<span data-ttu-id="4c714-223">El `teamMemberRemoved` evento se envía al bot si se quita de un equipo.</span><span class="sxs-lookup"><span data-stu-id="4c714-223">The `teamMemberRemoved` event is sent to your bot if it is removed from a team.</span></span> <span data-ttu-id="4c714-224">El evento se envía al bot cada vez que se quita cualquier usuario de un equipo en el que el bot es miembro.</span><span class="sxs-lookup"><span data-stu-id="4c714-224">The event is sent to your bot every time any user is removed from a team where your bot is a member.</span></span> <span data-ttu-id="4c714-225">Para determinar si el nuevo miembro quitado era el propio bot o un usuario, compruebe el `Activity` objeto de `turnContext` .</span><span class="sxs-lookup"><span data-stu-id="4c714-225">To determine if the new member removed was the bot itself or a user, check the `Activity` object of the `turnContext`.</span></span>  <span data-ttu-id="4c714-226">Si el campo del objeto es el mismo que el campo del objeto, el miembro quitado es el bot, de lo contrario `Id` `MembersRemoved` es un `Id` `Recipient` usuario.</span><span class="sxs-lookup"><span data-stu-id="4c714-226">If the `Id` field of the `MembersRemoved` object is the same as the `Id` field of the `Recipient` object, then the member removed is the bot, else it is a user.</span></span> <span data-ttu-id="4c714-227">Por lo general, el bot `Id` es `28:<MicrosoftAppId>` .</span><span class="sxs-lookup"><span data-stu-id="4c714-227">The bot's `Id` generally is `28:<MicrosoftAppId>`.</span></span>

> [!NOTE]
> <span data-ttu-id="4c714-228">Cuando un usuario se elimina permanentemente de un inquilino, `membersRemoved conversationUpdate` se desencadena el evento.</span><span class="sxs-lookup"><span data-stu-id="4c714-228">When a user is permanently deleted from a tenant, `membersRemoved conversationUpdate` event is triggered.</span></span>

<span data-ttu-id="4c714-229">El código siguiente muestra un ejemplo de evento de miembros del equipo eliminados:</span><span class="sxs-lookup"><span data-stu-id="4c714-229">The following code shows an example of team members removed event:</span></span>

# <a name="c"></a>[<span data-ttu-id="4c714-230">C#</span><span class="sxs-lookup"><span data-stu-id="4c714-230">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="4c714-231">TypeScript</span><span class="sxs-lookup"><span data-stu-id="4c714-231">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="4c714-232">JSON</span><span class="sxs-lookup"><span data-stu-id="4c714-232">JSON</span></span>](#tab/json)

<span data-ttu-id="4c714-233">El objeto del siguiente ejemplo de carga se basa en agregar un miembro a un equipo en lugar de un chat de grupo o iniciar una nueva conversación uno `channelData` a uno:</span><span class="sxs-lookup"><span data-stu-id="4c714-233">The `channelData` object in the following payload example is based on adding a member to a team rather than a group chat, or initiating a new one-to-one conversation:</span></span>

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


# <a name="python"></a>[<span data-ttu-id="4c714-234">Python</span><span class="sxs-lookup"><span data-stu-id="4c714-234">Python</span></span>](#tab/python)

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

---

### <a name="team-renamed"></a><span data-ttu-id="4c714-235">Cambio de nombre de equipo</span><span class="sxs-lookup"><span data-stu-id="4c714-235">Team renamed</span></span>

<span data-ttu-id="4c714-236">El bot recibe una notificación cuando se ha cambiado el nombre del equipo en el que está.</span><span class="sxs-lookup"><span data-stu-id="4c714-236">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="4c714-237">Recibe un `conversationUpdate` evento con en el `eventType.teamRenamed` `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="4c714-237">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span>

<span data-ttu-id="4c714-238">El siguiente código muestra un ejemplo de evento con el nombre de equipo:</span><span class="sxs-lookup"><span data-stu-id="4c714-238">The following code shows an example of team renamed event:</span></span>

# <a name="c"></a>[<span data-ttu-id="4c714-239">C#</span><span class="sxs-lookup"><span data-stu-id="4c714-239">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="4c714-240">TypeScript</span><span class="sxs-lookup"><span data-stu-id="4c714-240">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="4c714-241">JSON</span><span class="sxs-lookup"><span data-stu-id="4c714-241">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="4c714-242">Python</span><span class="sxs-lookup"><span data-stu-id="4c714-242">Python</span></span>](#tab/python)

```python
async def on_teams_team_renamed(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new team name is {team_info.name}")
    )
```

---

### <a name="team-deleted"></a><span data-ttu-id="4c714-243">Equipo eliminado</span><span class="sxs-lookup"><span data-stu-id="4c714-243">Team deleted</span></span>

<span data-ttu-id="4c714-244">El bot recibe una notificación cuando se ha eliminado el equipo en el que se encuentra.</span><span class="sxs-lookup"><span data-stu-id="4c714-244">Your bot is notified when the team it is in has been deleted.</span></span> <span data-ttu-id="4c714-245">Recibe un `conversationUpdate` evento con en el `eventType.teamDeleted` `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="4c714-245">It receives a `conversationUpdate` event with `eventType.teamDeleted` in the `channelData` object.</span></span>

<span data-ttu-id="4c714-246">El código siguiente muestra un ejemplo de evento eliminado por el equipo:</span><span class="sxs-lookup"><span data-stu-id="4c714-246">The following code shows an example of team deleted event:</span></span>

# <a name="c"></a>[<span data-ttu-id="4c714-247">C#</span><span class="sxs-lookup"><span data-stu-id="4c714-247">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamDeletedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    //handle delete event
}
```

# <a name="typescript"></a>[<span data-ttu-id="4c714-248">TypeScript</span><span class="sxs-lookup"><span data-stu-id="4c714-248">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="4c714-249">JSON</span><span class="sxs-lookup"><span data-stu-id="4c714-249">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="4c714-250">Python</span><span class="sxs-lookup"><span data-stu-id="4c714-250">Python</span></span>](#tab/python)

```python
async def on_teams_team_deleted(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    //handle delete event
    )
```

---

### <a name="team-restored"></a><span data-ttu-id="4c714-251">Equipo restaurado</span><span class="sxs-lookup"><span data-stu-id="4c714-251">Team restored</span></span>

<span data-ttu-id="4c714-252">El bot recibe una notificación cuando se restaura un equipo después de eliminarse.</span><span class="sxs-lookup"><span data-stu-id="4c714-252">The bot receives a notification when a team is restored after being deleted.</span></span> <span data-ttu-id="4c714-253">Recibe un `conversationUpdate` evento con en el `eventType.teamrestored` `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="4c714-253">It receives a `conversationUpdate` event with `eventType.teamrestored` in the `channelData` object.</span></span>

<span data-ttu-id="4c714-254">El código siguiente muestra un ejemplo de evento restaurado por el equipo:</span><span class="sxs-lookup"><span data-stu-id="4c714-254">The following code shows an example of team restored event:</span></span>

# <a name="c"></a>[<span data-ttu-id="4c714-255">C#</span><span class="sxs-lookup"><span data-stu-id="4c714-255">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamrestoredAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="4c714-256">TypeScript</span><span class="sxs-lookup"><span data-stu-id="4c714-256">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="4c714-257">JSON</span><span class="sxs-lookup"><span data-stu-id="4c714-257">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="4c714-258">Python</span><span class="sxs-lookup"><span data-stu-id="4c714-258">Python</span></span>](#tab/python)

```python
async def on_teams_team_restored(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

---

### <a name="team-archived"></a><span data-ttu-id="4c714-259">Equipo archivado</span><span class="sxs-lookup"><span data-stu-id="4c714-259">Team archived</span></span>

<span data-ttu-id="4c714-260">El bot recibe una notificación cuando se archiva el equipo en el que está instalado.</span><span class="sxs-lookup"><span data-stu-id="4c714-260">The bot receives a notification when the team it is installed in is archived.</span></span> <span data-ttu-id="4c714-261">Recibe un `conversationUpdate` evento con en el `eventType.teamarchived` `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="4c714-261">It receives a `conversationUpdate` event with `eventType.teamarchived` in the `channelData` object.</span></span>

<span data-ttu-id="4c714-262">El siguiente código muestra un ejemplo de evento archivado por el equipo:</span><span class="sxs-lookup"><span data-stu-id="4c714-262">The following code shows an example of team archived event:</span></span>

# <a name="c"></a>[<span data-ttu-id="4c714-263">C#</span><span class="sxs-lookup"><span data-stu-id="4c714-263">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamArchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="4c714-264">TypeScript</span><span class="sxs-lookup"><span data-stu-id="4c714-264">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="4c714-265">JSON</span><span class="sxs-lookup"><span data-stu-id="4c714-265">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="4c714-266">Python</span><span class="sxs-lookup"><span data-stu-id="4c714-266">Python</span></span>](#tab/python)

```python
async def on_teams_team_archived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

---


### <a name="team-unarchived"></a><span data-ttu-id="4c714-267">Equipo sin jerarquía</span><span class="sxs-lookup"><span data-stu-id="4c714-267">Team unarchived</span></span>

<span data-ttu-id="4c714-268">El bot recibe una notificación cuando el equipo en el que está instalado no estárchivo.</span><span class="sxs-lookup"><span data-stu-id="4c714-268">The bot receives a notification when the team it is installed in is unarchived.</span></span> <span data-ttu-id="4c714-269">Recibe un `conversationUpdate` evento con en el `eventType.teamUnarchived` `channelData` objeto.</span><span class="sxs-lookup"><span data-stu-id="4c714-269">It receives a `conversationUpdate` event with `eventType.teamUnarchived` in the `channelData` object.</span></span>

<span data-ttu-id="4c714-270">En el código siguiente se muestra un ejemplo de evento de equipo no anárquico:</span><span class="sxs-lookup"><span data-stu-id="4c714-270">The following code shows an example of team unarchived event:</span></span>

# <a name="c"></a>[<span data-ttu-id="4c714-271">C#</span><span class="sxs-lookup"><span data-stu-id="4c714-271">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamUnarchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="4c714-272">TypeScript</span><span class="sxs-lookup"><span data-stu-id="4c714-272">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="4c714-273">JSON</span><span class="sxs-lookup"><span data-stu-id="4c714-273">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="4c714-274">Python</span><span class="sxs-lookup"><span data-stu-id="4c714-274">Python</span></span>](#tab/python)

```python
async def on_teams_team_unarchived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

---

<span data-ttu-id="4c714-275">Ahora que ha trabajado con los eventos de actualización de conversación, puede comprender los eventos de reacción de mensajes que se producen para diferentes reacciones a un mensaje.</span><span class="sxs-lookup"><span data-stu-id="4c714-275">Now that you have worked with the conversation update events, you can understand the message reaction events that occur for different reactions to a message.</span></span>

## <a name="message-reaction-events"></a><span data-ttu-id="4c714-276">Eventos de reacción de mensajes</span><span class="sxs-lookup"><span data-stu-id="4c714-276">Message reaction events</span></span>

<span data-ttu-id="4c714-277">El evento se envía cuando un usuario agrega o quita las reacciones a un mensaje enviado `messageReaction` por el bot.</span><span class="sxs-lookup"><span data-stu-id="4c714-277">The `messageReaction` event is sent when a user adds or removes reactions to a message which was sent by your bot.</span></span> <span data-ttu-id="4c714-278">Contiene el identificador del mensaje y es el tipo `replyToId` de reacción en formato de `Type` texto.</span><span class="sxs-lookup"><span data-stu-id="4c714-278">The `replyToId` contains the ID of the message, and the `Type` is the type of reaction in text format.</span></span> <span data-ttu-id="4c714-279">Los tipos de reacciones incluyen el enojo, el corazón, la carcajada, como, la tristeza y la sorpresa.</span><span class="sxs-lookup"><span data-stu-id="4c714-279">The types of reactions include angry, heart, laugh, like, sad, and surprised.</span></span> <span data-ttu-id="4c714-280">Este evento no contiene el contenido del mensaje original.</span><span class="sxs-lookup"><span data-stu-id="4c714-280">This event does not contain the contents of the original message.</span></span> <span data-ttu-id="4c714-281">Si el procesamiento de las reacciones a los mensajes es importante para el bot, debe almacenar los mensajes al enviarlos.</span><span class="sxs-lookup"><span data-stu-id="4c714-281">If processing reactions to your messages is important for your bot, you must store the messages when you send them.</span></span> <span data-ttu-id="4c714-282">En la tabla siguiente se proporciona más información sobre el tipo de evento y los objetos de carga:</span><span class="sxs-lookup"><span data-stu-id="4c714-282">The following table provides more information about the event type and payload objects:</span></span>

| <span data-ttu-id="4c714-283">EventType</span><span class="sxs-lookup"><span data-stu-id="4c714-283">EventType</span></span>       | <span data-ttu-id="4c714-284">Payload (objeto)</span><span class="sxs-lookup"><span data-stu-id="4c714-284">Payload object</span></span>   | <span data-ttu-id="4c714-285">Descripción</span><span class="sxs-lookup"><span data-stu-id="4c714-285">Description</span></span>                                                             | <span data-ttu-id="4c714-286">Ámbito</span><span class="sxs-lookup"><span data-stu-id="4c714-286">Scope</span></span> |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| <span data-ttu-id="4c714-287">messageReaction</span><span class="sxs-lookup"><span data-stu-id="4c714-287">messageReaction</span></span> | <span data-ttu-id="4c714-288">reactionsAdded</span><span class="sxs-lookup"><span data-stu-id="4c714-288">reactionsAdded</span></span>   | <span data-ttu-id="4c714-289">[Reacciones agregadas al mensaje de bot](#reactions-added-to-bot-message).</span><span class="sxs-lookup"><span data-stu-id="4c714-289">[Reactions added to bot message](#reactions-added-to-bot-message).</span></span>           | <span data-ttu-id="4c714-290">Todo</span><span class="sxs-lookup"><span data-stu-id="4c714-290">All</span></span>   |
| <span data-ttu-id="4c714-291">messageReaction</span><span class="sxs-lookup"><span data-stu-id="4c714-291">messageReaction</span></span> | <span data-ttu-id="4c714-292">reactionsRemoved</span><span class="sxs-lookup"><span data-stu-id="4c714-292">reactionsRemoved</span></span> | <span data-ttu-id="4c714-293">[Reacciones eliminadas del mensaje de bot](#reactions-removed-from-bot-message).</span><span class="sxs-lookup"><span data-stu-id="4c714-293">[Reactions removed from bot message](#reactions-removed-from-bot-message).</span></span> | <span data-ttu-id="4c714-294">Todo</span><span class="sxs-lookup"><span data-stu-id="4c714-294">All</span></span> |

### <a name="reactions-added-to-bot-message"></a><span data-ttu-id="4c714-295">Reacciones agregadas al mensaje de bot</span><span class="sxs-lookup"><span data-stu-id="4c714-295">Reactions added to bot message</span></span>

<span data-ttu-id="4c714-296">El código siguiente muestra un ejemplo de las reacciones a un mensaje de bot:</span><span class="sxs-lookup"><span data-stu-id="4c714-296">The following code shows an example of reactions to a bot message:</span></span>

# <a name="c"></a>[<span data-ttu-id="4c714-297">C#</span><span class="sxs-lookup"><span data-stu-id="4c714-297">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="4c714-298">TypeScript</span><span class="sxs-lookup"><span data-stu-id="4c714-298">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="4c714-299">JSON</span><span class="sxs-lookup"><span data-stu-id="4c714-299">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="4c714-300">Python</span><span class="sxs-lookup"><span data-stu-id="4c714-300">Python</span></span>](#tab/python)

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

---

### <a name="reactions-removed-from-bot-message"></a><span data-ttu-id="4c714-301">Reacciones eliminadas del mensaje de bot</span><span class="sxs-lookup"><span data-stu-id="4c714-301">Reactions removed from bot message</span></span>

<span data-ttu-id="4c714-302">El siguiente código muestra un ejemplo de las reacciones eliminadas del mensaje del bot:</span><span class="sxs-lookup"><span data-stu-id="4c714-302">The following code shows an example of reactions removed from bot message:</span></span>

# <a name="c"></a>[<span data-ttu-id="4c714-303">C#</span><span class="sxs-lookup"><span data-stu-id="4c714-303">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="4c714-304">TypeScript</span><span class="sxs-lookup"><span data-stu-id="4c714-304">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="4c714-305">JSON</span><span class="sxs-lookup"><span data-stu-id="4c714-305">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="4c714-306">Python</span><span class="sxs-lookup"><span data-stu-id="4c714-306">Python</span></span>](#tab/python)

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

---

## <a name="installation-update-event"></a><span data-ttu-id="4c714-307">Evento de actualización de instalación</span><span class="sxs-lookup"><span data-stu-id="4c714-307">Installation update event</span></span>

<span data-ttu-id="4c714-308">El bot recibe un `installationUpdate` evento al instalar un bot en un subproceso de conversación.</span><span class="sxs-lookup"><span data-stu-id="4c714-308">The bot receives an `installationUpdate` event when you install a bot to a conversation thread.</span></span> <span data-ttu-id="4c714-309">La desinstalación del bot del subproceso también desencadena el evento.</span><span class="sxs-lookup"><span data-stu-id="4c714-309">Uninstallation of the bot from the thread also triggers the event.</span></span> <span data-ttu-id="4c714-310">Al instalar un bot, el campo **de** acción del evento se establece  en *agregar* y, cuando se desinstala el bot, el campo de acción se establece en *quitar*.</span><span class="sxs-lookup"><span data-stu-id="4c714-310">On installing a bot, the **action** field in the event is set to *add*, and when the bot is uninstalled the **action** field is set to *remove*.</span></span>
 
> [!NOTE]
> <span data-ttu-id="4c714-311">Al actualizar una aplicación y, a continuación, agregar o quitar un bot, la acción también desencadena el `installationUpdate` evento.</span><span class="sxs-lookup"><span data-stu-id="4c714-311">When you upgrade an application, and then add or remove a bot, the action also triggers the `installationUpdate` event.</span></span> <span data-ttu-id="4c714-312">El **campo** de acción se establece en *add-upgrade* si agrega un bot o *remove-upgrade* si quita un bot.</span><span class="sxs-lookup"><span data-stu-id="4c714-312">The **action** field is set to *add-upgrade* if you add a bot or *remove-upgrade* if you remove a bot.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="4c714-313">Los eventos de actualización de instalación están en versión preliminar del desarrollador hoy y estarán disponibles generalmente (GA) en marzo de 2021.</span><span class="sxs-lookup"><span data-stu-id="4c714-313">Installation update events are in developer preview today and will be Generally Available (GA) in March 2021.</span></span> <span data-ttu-id="4c714-314">Para ver los eventos de actualización de instalación, puedes mover el cliente de Teams a la vista previa del desarrollador público y agregar la aplicación personalmente o a un equipo o un chat.</span><span class="sxs-lookup"><span data-stu-id="4c714-314">To see the installation update events, you can move your Teams client to public developer preview, and add your app personally or to a team or a chat.</span></span>

### <a name="install-update-event"></a><span data-ttu-id="4c714-315">Evento Install update</span><span class="sxs-lookup"><span data-stu-id="4c714-315">Install update event</span></span>
<span data-ttu-id="4c714-316">Use el `installationUpdate` evento para enviar un mensaje introductorio desde el bot durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="4c714-316">Use the `installationUpdate` event to send an introductory message from your bot on installation.</span></span> <span data-ttu-id="4c714-317">Este evento le ayuda a cumplir los requisitos de privacidad y retención de datos.</span><span class="sxs-lookup"><span data-stu-id="4c714-317">This event helps you to meet your privacy and data retention requirements.</span></span> <span data-ttu-id="4c714-318">También puede limpiar y eliminar datos de usuario o subproceso cuando se desinstala el bot.</span><span class="sxs-lookup"><span data-stu-id="4c714-318">You can also clean up and delete user or thread data when the bot is uninstalled.</span></span>

# <a name="c"></a>[<span data-ttu-id="4c714-319">C#</span><span class="sxs-lookup"><span data-stu-id="4c714-319">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task
OnInstallationUpdateActivityAsync(ITurnContext<IInstallationUpdateActivity> turnContext, CancellationToken cancellationToken) {
var activity = turnContext.Activity; if
(string.Equals(activity.Action, "Add",
StringComparison.InvariantCultureIgnoreCase)) {
// TO:DO Installation workflow }
else
{ // TO:DO Uninstallation workflow
} return; }
```

<span data-ttu-id="4c714-320">También puede usar un controlador dedicado para *agregar* *o* quitar escenarios como método alternativo para capturar un evento.</span><span class="sxs-lookup"><span data-stu-id="4c714-320">You can also use a dedicated handler for *add* or *remove* scenarios as an alternative method to capture an event.</span></span>

```csharp
protected override async Task
OnInstallationUpdateAddAsync(ITurnContext<IInstallationUpdateActivity>
turnContext, CancellationToken cancellationToken) {
// TO:DO Installation workflow return;
}
```

# <a name="typescript"></a>[<span data-ttu-id="4c714-321">TypeScript</span><span class="sxs-lookup"><span data-stu-id="4c714-321">TypeScript</span></span>](#tab/typescript)

<span data-ttu-id="4c714-322">No disponible</span><span class="sxs-lookup"><span data-stu-id="4c714-322">Not available</span></span>

# <a name="json"></a>[<span data-ttu-id="4c714-323">JSON</span><span class="sxs-lookup"><span data-stu-id="4c714-323">JSON</span></span>](#tab/json)

```json
{ 
  "action": "add", 
  "type": "installationUpdate", 
  "timestamp": "2020-10-20T22:08:07.869Z", 
  "id": "f:3033745319439849398", 
  "channelId": "msteams", 
  "serviceUrl": "https://smba.trafficmanager.net/amer/", 
  "from": { 
    "id": "sample id", 
    "aadObjectId": "sample AAD Object ID" 
  },
  "conversation": { 
    "isGroup": true, 
    "conversationType": "channel", 
    "tenantId": "sample tenant ID", 
    "id": "sample conversation Id@thread.skype" 
  }, 

  "recipient": { 
    "id": "sample reciepent bot ID", 
    "name": "bot name" 
  }, 
  "entities": [ 
    { 
      "locale": "en", 
      "platform": "Windows", 
      "type": "clientInfo" 
    } 
  ], 
  "channelData": { 
    "settings": { 
      "selectedChannel": { 
        "id": "sample channel ID@thread.skype" 
      } 
    }, 
    "channel": { 
      "id": "sample channel ID" 
    }, 
    "team": { 
      "id": "sample team ID" 
    }, 
    "tenant": { 
      "id": "sample tenant ID" 
    }, 
    "source": { 
      "name": "message" 
    } 
  }, 
  "locale": "en" 
}
```

# <a name="python"></a>[<span data-ttu-id="4c714-324">Python</span><span class="sxs-lookup"><span data-stu-id="4c714-324">Python</span></span>](#tab/python)

<span data-ttu-id="4c714-325">No disponible</span><span class="sxs-lookup"><span data-stu-id="4c714-325">Not available</span></span>

---

## <a name="uninstall-behavior-for-personal-app-with-bot"></a><span data-ttu-id="4c714-326">Comportamiento de desinstalación de la aplicación personal con bot</span><span class="sxs-lookup"><span data-stu-id="4c714-326">Uninstall behavior for personal app with bot</span></span>

> [!NOTE]
> <span data-ttu-id="4c714-327">El comportamiento de desinstalación de la aplicación personal con bot solo está disponible actualmente en [la versión preliminar del desarrollador público.](../../../resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="4c714-327">Uninstall behavior for personal app with bot is currently available only in [public developer preview](../../../resources/dev-preview/developer-preview-intro.md).</span></span>

<span data-ttu-id="4c714-328">Al desinstalar una aplicación, el bot también se desinstala.</span><span class="sxs-lookup"><span data-stu-id="4c714-328">When you uninstall an app, the bot is also uninstalled.</span></span> <span data-ttu-id="4c714-329">Cuando un usuario envía un mensaje a la aplicación, recibe un código de respuesta 403.</span><span class="sxs-lookup"><span data-stu-id="4c714-329">When a user sends a message to your app, they receive a 403 response code.</span></span> <span data-ttu-id="4c714-330">El bot recibe un código de respuesta 403 para los nuevos mensajes publicados por el bot.</span><span class="sxs-lookup"><span data-stu-id="4c714-330">Your bot receives a 403 response code for new messages posted by your bot.</span></span> <span data-ttu-id="4c714-331">El comportamiento posterior a la desinstalación de bots en el ámbito personal con los ámbitos Teams y groupChat ahora están alineados.</span><span class="sxs-lookup"><span data-stu-id="4c714-331">The post uninstall behavior for bots in the personal scope with the Teams and groupChat scopes are now aligned.</span></span> <span data-ttu-id="4c714-332">No puedes enviar ni recibir mensajes después de desinstalar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="4c714-332">You cannot send or receive messages after an app has been uninstalled.</span></span>

<img src="~/assets/images/bots/uninstallbot.png" alt="Uninstall event" width="900" height="900"/>

## <a name="event-handling-for-install-and-uninstall-events"></a><span data-ttu-id="4c714-333">Control de eventos para eventos de instalación y desinstalación</span><span class="sxs-lookup"><span data-stu-id="4c714-333">Event handling for install and uninstall events</span></span>

<span data-ttu-id="4c714-334">Al usar estos eventos de instalación y desinstalación, hay algunas instancias en las que los bots dan excepciones al recibir eventos inesperados de Teams.</span><span class="sxs-lookup"><span data-stu-id="4c714-334">When you use these install and uninstall events, there are some instances where bots give exceptions on receiving unexpected events from Teams.</span></span> <span data-ttu-id="4c714-335">Esto ocurre en los siguientes casos:</span><span class="sxs-lookup"><span data-stu-id="4c714-335">This occurs in the following cases:</span></span>

* <span data-ttu-id="4c714-336">Creas el bot sin el SDK Microsoft Bot Framework y, como resultado, el bot da una excepción al recibir un evento inesperado.</span><span class="sxs-lookup"><span data-stu-id="4c714-336">You build your bot without the Microsoft Bot Framework SDK, and as a result the bot gives an exception on receiving an unexpected event.</span></span>
* <span data-ttu-id="4c714-337">Creas el bot con el SDK de Microsoft Bot Framework y seleccionas modificar el comportamiento de evento predeterminado invalidando el identificador de evento base.</span><span class="sxs-lookup"><span data-stu-id="4c714-337">You build your bot with the Microsoft Bot Framework SDK, and you select to alter the default event behavior by overriding the base event handle.</span></span>

<span data-ttu-id="4c714-338">Es importante saber que los nuevos eventos se pueden agregar en cualquier momento en el futuro y el bot comienza a recibirlos.</span><span class="sxs-lookup"><span data-stu-id="4c714-338">It is important to know that new events can be added anytime in the future and your bot begins to receive them.</span></span> <span data-ttu-id="4c714-339">Por lo tanto, debe diseñar la posibilidad de recibir eventos inesperados.</span><span class="sxs-lookup"><span data-stu-id="4c714-339">So you must design for the possibility of receiving unexpected events.</span></span> <span data-ttu-id="4c714-340">Si usa el SDK de Bot Framework, el bot responde automáticamente con un 200: aceptar cualquier evento que no elija controlar.</span><span class="sxs-lookup"><span data-stu-id="4c714-340">If you are using the Bot Framework SDK, your bot automatically responds with a 200 – OK to any events you do not choose to handle.</span></span>

## <a name="code-sample"></a><span data-ttu-id="4c714-341">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="4c714-341">Code sample</span></span>

| <span data-ttu-id="4c714-342">**Nombre de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4c714-342">**Sample name**</span></span> | <span data-ttu-id="4c714-343">**Description**</span><span class="sxs-lookup"><span data-stu-id="4c714-343">**Description**</span></span> | <span data-ttu-id="4c714-344">**.NET**</span><span class="sxs-lookup"><span data-stu-id="4c714-344">**.NET**</span></span> | <span data-ttu-id="4c714-345">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="4c714-345">**Node.js**</span></span> | <span data-ttu-id="4c714-346">**Python**</span><span class="sxs-lookup"><span data-stu-id="4c714-346">**Python**</span></span> |
|----------|-----------------|----------|
| <span data-ttu-id="4c714-347">Bot de conversación</span><span class="sxs-lookup"><span data-stu-id="4c714-347">Conversation bot</span></span> | <span data-ttu-id="4c714-348">Código de ejemplo para eventos de conversación de bots.</span><span class="sxs-lookup"><span data-stu-id="4c714-348">Sample code for bots conversation events.</span></span> | [<span data-ttu-id="4c714-349">View</span><span class="sxs-lookup"><span data-stu-id="4c714-349">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)  | [<span data-ttu-id="4c714-350">View</span><span class="sxs-lookup"><span data-stu-id="4c714-350">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="4c714-351">View</span><span class="sxs-lookup"><span data-stu-id="4c714-351">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a><span data-ttu-id="4c714-352">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="4c714-352">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4c714-353">Enviar mensajes proactivos</span><span class="sxs-lookup"><span data-stu-id="4c714-353">Send proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)

---
title: Obtener el contexto específico del equipo para el bot
author: clearab
description: Cómo obtener el contexto específico del equipo de Microsoft para su bot, incluidos la lista de conversaciones, los detalles y la lista de canales.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 9f70e3e052903365f03c541db83f196f33fc2322
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676097"
---
# <a name="get-teams-specific-context-for-your-bot"></a><span data-ttu-id="731a1-103">Obtener el contexto específico del equipo para el bot</span><span class="sxs-lookup"><span data-stu-id="731a1-103">Get Team's specific context for your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="731a1-104">Un bot puede tener acceso a datos de contexto adicionales sobre un equipo o un chat en los que está instalado.</span><span class="sxs-lookup"><span data-stu-id="731a1-104">A bot can access additional context data about a team or chat it is installed in.</span></span> <span data-ttu-id="731a1-105">Esta información puede usarse para enriquecer la funcionalidad del bot y proporcionar una experiencia más personalizada.</span><span class="sxs-lookup"><span data-stu-id="731a1-105">This information can be used to enrich the bot's functionality and provide a more personalized experience.</span></span>

## <a name="fetching-the-roster-or-user-profile"></a><span data-ttu-id="731a1-106">Obtención de la lista o el perfil de usuario</span><span class="sxs-lookup"><span data-stu-id="731a1-106">Fetching the roster or user profile</span></span>

<span data-ttu-id="731a1-107">El bot puede consultar la lista de miembros y sus perfiles básicos, incluidos los identificadores de usuario de Microsoft Teams y la información de Azure Active Directory (Azure AD), como Name y objectId.</span><span class="sxs-lookup"><span data-stu-id="731a1-107">Your bot can query for the list of members and their basic profiles, including Teams user IDs and Azure Active Directory (Azure AD) information such as name and objectId.</span></span> <span data-ttu-id="731a1-108">Puede usar esta información para correlacionar identidades de usuario, por ejemplo, para comprobar si un usuario, conectado a una pestaña a través de las credenciales de Azure AD, es miembro del equipo.</span><span class="sxs-lookup"><span data-stu-id="731a1-108">You can use this information to correlate user identities, e.g., to check whether a user, logged into a tab through Azure AD credentials, is a member of the team.</span></span> <span data-ttu-id="731a1-109">También puede usar esta llamada en un chat de uno a uno para obtener información adicional sobre el usuario.</span><span class="sxs-lookup"><span data-stu-id="731a1-109">You can also use this call in a one-to-one chat to gain additional information about your user.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="731a1-110">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="731a1-110">C#/.NET</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        IEnumerable<TeamsChannelAccount> members = await TeamsInfo.GetMembersAsync(turnContext, cancellationToken);
    }
}
```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="731a1-111">TypeScript/node. js</span><span class="sxs-lookup"><span data-stu-id="731a1-111">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            const members = await TeamsInfo.getMembers(turnContext);

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });
    }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="731a1-112">JSON</span><span class="sxs-lookup"><span data-stu-id="731a1-112">JSON</span></span>](#tab/json)
<span data-ttu-id="731a1-113">Puede emitir directamente una solicitud `/v3/conversations/{teamId}/members/`Get usando el valor de como punto de `serviceUrl` conexión.</span><span class="sxs-lookup"><span data-stu-id="731a1-113">You can directly issue a GET request on `/v3/conversations/{teamId}/members/`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="731a1-114">El valor de `serviceUrl` tiende a ser estable, pero puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="731a1-114">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="731a1-115">Cuando llega un nuevo mensaje, el bot debe comprobar su valor almacenado para `serviceUrl`.</span><span class="sxs-lookup"><span data-stu-id="731a1-115">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span>

```http
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/members

Response body
[{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "objectId": "9d3e08f9-a7ae-43aa-a4d3-de3f319a8a9c",
    "givenName": "Larry",
    "surname": "Brown",
    "email": "Larry.Brown@fabrikam.com",
    "userPrincipalName": "labrown@fabrikam.com"
}, {
    "id": "29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk",
    "objectId": "76b0b09f-d410-48fd-993e-84da521a597b",
    "givenName": "John",
    "surname": "Patterson",
    "email": "johnp@fabrikam.com",
    "userPrincipalName": "johnp@fabrikam.com"
}, {
    "id": "29:1URzNQM1x1PNMr1D7L5_lFe6qF6gEfAbkdG8_BUxOW2mTKryQqEZtBTqDt10-MghkzjYDuUj4KG6nvg5lFAyjOLiGJ4jzhb99WrnI7XKriCs",
    "objectId": "6b7b3b2a-2c4b-4175-8582-41c9e685c1b5",
    "givenName": "Rick",
    "surname": "Stevens",
    "email": "Rick.Stevens@fabrikam.com",
    "userPrincipalName": "rstevens@fabrikam.com"
}]
```

# <a name="pythontabpython"></a>[<span data-ttu-id="731a1-116">Python</span><span class="sxs-lookup"><span data-stu-id="731a1-116">Python</span></span>](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    members = await TeamsInfo.get_team_members(turn_context)
```

* * *

## <a name="get-teams-details"></a><span data-ttu-id="731a1-117">Obtener detalles del equipo</span><span class="sxs-lookup"><span data-stu-id="731a1-117">Get team's details</span></span>

<span data-ttu-id="731a1-118">Cuando se instala en un equipo, el bot puede consultar los metadatos de ese equipo, incluido el groupId de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="731a1-118">When installed in a team, your bot can query for metadata about that team including the Azure AD groupId.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="731a1-119">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="731a1-119">C#/.NET</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        TeamDetails teamDetails = await TeamsInfo.GetTeamDetailsAsync(turnContext, turnContext.Activity.TeamsGetTeamInfo().Id, cancellationToken);
        if (teamDetails != null) {
            await turnContext.SendActivityAsync($"The groupId is: {teamDetails.AadGroupId}");
        }
        else {
            await turnContext.SendActivityAsync($"Message did not come from a channel in a team.");
        }
    }
}
```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="731a1-120">TypeScript/node. js</span><span class="sxs-lookup"><span data-stu-id="731a1-120">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            const teamDetails = await TeamsInfo.getTeamDetails(turnContext);
            if (teamDetails) {
                await turnContext.sendActivity(`The group ID is: ${teamDetails.aadGroupId}`);
            } else {
                await turnContext.sendActivity('This message did not come from a channel in a team.');
            }

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });
    }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="731a1-121">JSON</span><span class="sxs-lookup"><span data-stu-id="731a1-121">JSON</span></span>](#tab/json)

<span data-ttu-id="731a1-122">Puede emitir directamente una solicitud `/v3/teams/{teamId}`Get usando el valor de como punto de `serviceUrl` conexión.</span><span class="sxs-lookup"><span data-stu-id="731a1-122">You can directly issue a GET request on `/v3/teams/{teamId}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="731a1-123">El valor de `serviceUrl` tiende a ser estable, pero puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="731a1-123">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="731a1-124">Cuando llega un nuevo mensaje, el bot debe comprobar su valor almacenado para `serviceUrl`.</span><span class="sxs-lookup"><span data-stu-id="731a1-124">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span>

```http
GET /v3/teams/19:ja0cu120i1jod12j@skype.net

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "name": "The Team Name",
    "aadGroupId": "02ce3874-dd86-41ba-bddc-013f34019978"
}
```

# <a name="pythontabpython"></a>[<span data-ttu-id="731a1-125">Python</span><span class="sxs-lookup"><span data-stu-id="731a1-125">Python</span></span>](#tab/python)

```python
async def _show_details(self, turn_context: TurnContext):
    team_details = await TeamsInfo.get_team_details(turn_context)
    reply = MessageFactory.text(f"The team name is {team_details.name}. The team ID is {team_details.id}. The AADGroupID is {team_details.aad_group_id}.")
    await turn_context.send_activity(reply)
```

* * *

## <a name="get-the-list-of-channels-in-a-team"></a><span data-ttu-id="731a1-126">Obtener la lista de canales en un equipo</span><span class="sxs-lookup"><span data-stu-id="731a1-126">Get the list of channels in a team</span></span>

<span data-ttu-id="731a1-127">El bot puede consultar la lista de canales de un equipo.</span><span class="sxs-lookup"><span data-stu-id="731a1-127">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="731a1-128">El nombre del canal general predeterminado se devuelve como `null` permitir para la localización.</span><span class="sxs-lookup"><span data-stu-id="731a1-128">The name of the default General channel is returned as `null` to allow for localization.</span></span>
>* <span data-ttu-id="731a1-129">El identificador de canal para el canal general coincide siempre con el identificador del equipo.</span><span class="sxs-lookup"><span data-stu-id="731a1-129">The channel ID for the General channel always matches the team ID.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="731a1-130">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="731a1-130">C#/.NET</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        IEnumerable<ChannelInfo> channels = await TeamsInfo.GetTeamChannelsAsync(turnContext, turnContext.Activity.TeamsGetTeamInfo().Id, cancellationToken);

        await turnContext.SendActivityAsync($"The channel count is: {channels.Count()}");
    }
}
```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="731a1-131">TypeScript/node. js</span><span class="sxs-lookup"><span data-stu-id="731a1-131">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            const channels = await TeamsInfo.getTeamChannels(turnContext);

            await turnContext.sendActivity(`The channel count is: ${channels.length}`);

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });
    }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="731a1-132">JSON</span><span class="sxs-lookup"><span data-stu-id="731a1-132">JSON</span></span>](#tab/json)

<span data-ttu-id="731a1-133">Puede emitir directamente una solicitud `/v3/teams/{teamId}/conversations`Get usando el valor de como punto de `serviceUrl` conexión.</span><span class="sxs-lookup"><span data-stu-id="731a1-133">You can directly issue a GET request on `/v3/teams/{teamId}/conversations`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="731a1-134">El valor de `serviceUrl` tiende a ser estable, pero puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="731a1-134">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="731a1-135">Cuando llega un nuevo mensaje, el bot debe comprobar su valor almacenado para `serviceUrl`.</span><span class="sxs-lookup"><span data-stu-id="731a1-135">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span>

```http
GET /v3/teams/19%3A033451497ea84fcc83d17ed7fb08a1b6%40thread.skype/conversations

Response body
{
    "conversations": [{
        "id": "19:033451497ea84fcc83d17ed7fb08a1b6@thread.skype",
        "name": null
    }, {
        "id": "19:cc25e4aae50746ecbb11473bba24c70a@thread.skype",
        "name": "Materials"
    }, {
        "id": "19:b7b84cba410c406ba671dbbf5e0a3519@thread.skype",
        "name": "Design"
    }, {
        "id": "19:fc5db2aed489454e8f8c06829ed6c986@thread.skype",
        "name": "Marketing"
    }]
}
```


# <a name="pythontabpython"></a>[<span data-ttu-id="731a1-136">Python</span><span class="sxs-lookup"><span data-stu-id="731a1-136">Python</span></span>](#tab/python)

```python
async def _show_channels(
    self, turn_context: TurnContext
):
    channels = await TeamsInfo.get_team_channels(turn_context)
    reply = MessageFactory.text(f"Total of {len(channels)} channels are currently in team")
    await turn_context.send_activity(reply)
```

* * *

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

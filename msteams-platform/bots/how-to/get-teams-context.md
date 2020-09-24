---
title: Obtener el contexto específico del equipo para el bot
author: clearab
description: Cómo obtener el contexto específico del equipo de Microsoft para su bot, incluidos la lista de conversaciones, los detalles y la lista de canales.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 55f93a914cdb0f92885ff535424cd823072184aa
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237797"
---
# <a name="get-teams-specific-context-for-your-bot"></a>Obtener el contexto específico del equipo para el bot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Un bot puede tener acceso a datos de contexto adicionales sobre un equipo o un chat en los que está instalado. Esta información puede usarse para enriquecer la funcionalidad del bot y proporcionar una experiencia más personalizada.

## <a name="fetching-the-roster-or-user-profile"></a>Obtención de la lista o el perfil de usuario

El bot puede consultar la lista de miembros y sus perfiles básicos, incluidos los identificadores de usuario de Microsoft Teams y la información de Azure Active Directory (Azure AD), como Name y objectId. Puede usar esta información para correlacionar identidades de usuario, por ejemplo, para comprobar si un usuario, conectado a una pestaña a través de las credenciales de Azure AD, es miembro del equipo. En el código de ejemplo siguiente se usa el punto de conexión paginado para recuperar la lista. Aunque puede seguir usando la versión no paginada, no será confiable en equipos grandes y no debe usarse. Consulte [este artículo](~/resources/team-chat-member-api-changes.md) para obtener más información.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        var members = new List<TeamsChannelAccount>();
        string continuationToken = null;

        do
        {
            var currentPage = await TeamsInfo.GetPagedMembersAsync(turnContext, 100, continuationToken, cancellationToken);
            continuationToken = currentPage.ContinuationToken;
            members.AddRange(currentPage.Members);
         }
         while (continuationToken != null);
     }
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            var continuationToken;
            var members = [];

            do {
                var pagedMembers = await TeamsInfo.getPagedMembers(context, 100, continuationToken);
                continuationToken = pagedMembers.continuationToken;
                members.push(...pagedMembers.members);
            }
            while(continuationToken !== undefined)

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    members = await TeamsInfo.get_team_members(turn_context)
```

# <a name="json"></a>[JSON](#tab/json)

Puede emitir directamente una solicitud GET `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}` usando el valor de `serviceUrl` como punto de conexión. El valor de `serviceUrl` tiende a ser estable, pero puede cambiar. Cuando llega un nuevo mensaje, el bot debe comprobar su valor almacenado para `serviceUrl` .

```http
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/pagedmembers?pageSize=100&continuationToken=asdfasdfalkdsjfalksjdf

Response body
{
    "continuationToken": "asdfqwerueiqpiewr",
    "members":
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
}
```

* * *

## <a name="get-single-member-details"></a>Obtener detalles de un solo miembro

También puede recuperar los detalles de un usuario concreto mediante su identificador de usuario de equipo, UPN o identificador de objeto de AAD.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);
    }
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        const member = await TeamsInfo.getMember(context, encodeURI('someone@somecompany.com'));

        // By calling next() you ensure that the next BotHandler is run.
        await next();
        });
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    member = TeamsInfo.get_member(turn_context, turn_context.activity.from_property.id)
```

# <a name="json"></a>[JSON](#tab/json)

Puede emitir directamente una solicitud GET `/v3/conversations/{conversationId}/members/{userId}` usando el valor de `serviceUrl` como punto de conexión. El valor de `serviceUrl` tiende a ser estable, pero puede cambiar. Cuando llega un nuevo mensaje, el bot debe comprobar su valor almacenado para `serviceUrl` .

```http
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/members/labrown@fabrikam.com"

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "objectId": "9d3e08f9-a7ae-43aa-a4d3-de3f319a8a9c",
    "givenName": "Larry",
    "surname": "Brown",
    "email": "Larry.Brown@fabrikam.com",
    "userPrincipalName": "labrown@fabrikam.com"
}
```

* * *

## <a name="get-teams-details"></a>Obtener detalles del equipo

Cuando se instala en un equipo, el bot puede consultar los metadatos de ese equipo, incluido el groupId de Azure AD.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

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

# <a name="python"></a>[Python](#tab/python)

```python
async def _show_details(self, turn_context: TurnContext):
    team_details = await TeamsInfo.get_team_details(turn_context)
    reply = MessageFactory.text(f"The team name is {team_details.name}. The team ID is {team_details.id}. The AADGroupID is {team_details.aad_group_id}.")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[JSON](#tab/json)

Puede emitir directamente una solicitud GET `/v3/teams/{teamId}` usando el valor de `serviceUrl` como punto de conexión. El valor de `serviceUrl` tiende a ser estable, pero puede cambiar. Cuando llega un nuevo mensaje, el bot debe comprobar su valor almacenado para `serviceUrl` .

```http
GET /v3/teams/19:ja0cu120i1jod12j@skype.net

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "name": "The Team Name",
    "aadGroupId": "02ce3874-dd86-41ba-bddc-013f34019978"
}
```

* * *

## <a name="get-the-list-of-channels-in-a-team"></a>Obtener la lista de canales en un equipo

El bot puede consultar la lista de canales de un equipo.

> [!NOTE]
>
>* El nombre del canal general predeterminado se devuelve como `null` permitir para la localización.
>* El identificador de canal para el canal general coincide siempre con el identificador del equipo.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

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

# <a name="python"></a>[Python](#tab/python)

```python
async def _show_channels(
    self, turn_context: TurnContext
):
    channels = await TeamsInfo.get_team_channels(turn_context)
    reply = MessageFactory.text(f"Total of {len(channels)} channels are currently in team")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[JSON](#tab/json)

Puede emitir directamente una solicitud GET `/v3/teams/{teamId}/conversations` usando el valor de `serviceUrl` como punto de conexión. El valor de `serviceUrl` tiende a ser estable, pero puede cambiar. Cuando llega un nuevo mensaje, el bot debe comprobar su valor almacenado para `serviceUrl` .

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

* * *

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

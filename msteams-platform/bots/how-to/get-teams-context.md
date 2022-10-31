---
title: Obtención del contexto específico de Teams para un bot
author: surbhigupta
description: Obtenga el contexto específico de Teams para el bot, capture el perfil de usuario, obtenga un solo miembro, el equipo y la lista de canales en los detalles de un equipo. Ejemplo al crear un subproceso de canal.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: lajanuar
ms.openlocfilehash: 1958d45bf4fac927c32b628ea8aebc4c1c03ad46
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789992"
---
# <a name="get-teams-specific-context-for-your-bot"></a>Obtención del contexto específico de Teams para un bot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Un bot puede acceder a datos de contexto adicionales sobre un equipo o el chat donde está instalado. Esta información se puede usar para enriquecer la funcionalidad del bot y proporcionar una experiencia más personalizada.

## <a name="fetch-the-roster-or-user-profile"></a>Captura de la lista o el perfil del usuario

El bot puede consultar la lista de miembros y sus perfiles de usuario básicos, incluidos los identificadores de usuario de Teams e información de Microsoft Azure Active Directory (Azure AD), como name y objectId. Puede usar esta información para correlacionar las identidades de usuario. Por ejemplo, para comprobar si un usuario ha iniciado sesión en una pestaña a través de las credenciales de Azure AD, es miembro del equipo. Para obtener miembros de la conversación, el tamaño mínimo o máximo de la página depende de la implementación. El tamaño de página menor que 50, se trata como 50 y mayor que 500, se limita a 500. Incluso si usa la versión no paginada, no es confiable en equipos grandes y no se debe usar. Para obtener más información, consulte [cambios en las API del bot de Teams para capturar miembros del equipo o del chat](~/resources/team-chat-member-api-changes.md).

El código de ejemplo siguiente usa el punto de conexión paginado para capturar la lista:

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            var continuationToken;
            var members = [];

            do {
                var pagedMembers = await TeamsInfo.getPagedMembers(turnContext, 100, continuationToken);
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

Puede emitir directamente una solicitud GET en `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}`, utilizando el valor de `serviceUrl` como punto de conexión. El valor de `serviceUrl` es estable, pero puede cambiar. Cuando llega un nuevo mensaje, el bot debe comprobar su valor almacenado para `serviceUrl`. La carga de respuesta también indica si el usuario es un usuario normal o anónimo.

```http
GET /v3/conversations/19:meeting_N2QzYTA3YmItYmMwOC00OTJmLThkYzMtZWMzZGU0NGIyZGI0@thread.v2/pagedmembers?pageSize=100&continuationToken=asdfasdfalkdsjfalksjdf

Response body
{
   "continuationToken":"asdfqwerueiqpiewr",
   "members":[
      {
         "id":"29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
         "name":"Anon1 (Guest)",
         "tenantId":"29:1UX7p8Fkx7p93MZlBFS71swTB9juQOCfnXf2L3wxOUITCcIGpFcRX-JiFjLDVZhxGpEfzSTGNsZeEyTKr1iu3Vw",
         "userRole":"anonymous"
      },
      {
         "id":"29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk",
         "objectId":"76b0b09f-d410-48fd-993e-84da521a597b",
         "givenName":"John",
         "surname":"Patterson",
         "email":"johnp@fabrikam.com",
         "userPrincipalName":"johnp@fabrikam.com",
         "tenantId":"29:1UX7p8Fkx7p93MZlBFS71swTB9juQOCfnXf2L3wxOUITCcIGpFcRX-JiFjLDVZhxGpEfzSTGNsZeEyTKr1iu3Vw",
         "userRole":"user"
      },
      {
         "id":"29:1URzNQM1x1PNMr1D7L5_lFe6qF6gEfAbkdG8_BUxOW2mTKryQqEZtBTqDt10-MghkzjYDuUj4KG6nvg5lFAyjOLiGJ4jzhb99WrnI7XKriCs",
         "objectId":"6b7b3b2a-2c4b-4175-8582-41c9e685c1b5",
         "givenName":"Rick",
         "surname":"Stevens",
         "email":"Rick.Stevens@fabrikam.com",
         "userPrincipalName":"rstevens@fabrikam.com",
         "tenantId":"29:1UX7p8Fkx7p93MZlBFS71swTB9juQOCfnXf2L3wxOUITCcIGpFcRX-JiFjLDVZhxGpEfzSTGNsZeEyTKr1iu3Vw",
         "userRole":"user"
      }
   ]
}
```

* * *

Después de capturar la lista o el perfil de usuario, puede obtener detalles de un único miembro. Actualmente, para recuperar información de uno o varios miembros de un chat o equipo, use las API `TeamsInfo.GetMembersAsync` del bot de Microsoft Teams para C# o `TeamsInfo.getMembers` para las API de TypeScript.

## <a name="get-single-member-details"></a>Obtener detalles de un miembro

También puede recuperar los detalles de un usuario determinado mediante su id. de usuario de Teams, UPN o el id. de objeto de Azure AD.

El siguiente código de ejemplo se usa para obtener detalles de un solo miembro:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            const member = await TeamsInfo.getMember(turnContext, encodeURI('someone@somecompany.com'));

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
    member = await TeamsInfo.get_member(turn_context, turn_context.activity.from_property.id)
```

# <a name="json"></a>[JSON](#tab/json)

Puede emitir directamente una solicitud GET en `/v3/conversations/{conversationId}/members/{userId}`, utilizando el valor de `serviceUrl` como punto de conexión. El valor de `serviceUrl` es estable, pero puede cambiar. Cuando llega un nuevo mensaje, el bot debe comprobar su valor almacenado para `serviceUrl`. Esto se puede usar para usuarios normales y usuarios anónimos.

A continuación se muestra el ejemplo de respuesta para el usuario normal:

```http
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/members/29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "objectId": "9d3e08f9-a7ae-43aa-a4d3-de3f319a8a9c",
    "givenName": "Larry",
    "surname": "Brown",
    "email": "Larry.Brown@fabrikam.com",
    "userPrincipalName": "labrown@fabrikam.com",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47", 
    "userRole":"user"
}
```

A continuación se muestra el ejemplo de respuesta para el usuario anónimo:

```http
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/members/<anonymous user id>"

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "name": "Anon1 (Guest)",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47", 
    "userRole":"anonymous"
}
```

* * *

Después de obtener los detalles de un solo miembro, puede obtener los detalles del equipo. Actualmente, para recuperar información de un equipo, use las API de bot de Teams `TeamsInfo.GetMemberDetailsAsync` para C# o `TeamsInfo.getTeamDetails` para TypeScript.

## <a name="get-teams-details"></a>Obtener los detalles del equipo

Cuando se instala en un equipo, el bot puede consultar metadatos sobre ese equipo, incluido el identificador de grupo de Azure AD.

El siguiente código de ejemplo se usa para obtener los detalles del equipo:

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

Puede emitir directamente una solicitud GET en `/v3/teams/{teamId}`, utilizando el valor de `serviceUrl` como punto de conexión. El valor de `serviceUrl` es estable, pero puede cambiar. Cuando llega un nuevo mensaje, el bot debe comprobar su valor almacenado para `serviceUrl`.

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

Después de obtener los detalles del equipo, puede obtener la lista de canales de un equipo. Actualmente, para recuperar información de una lista de canales de un equipo, use las API de bot de Teams `TeamsInfo.GetTeamChannelsAsync` para C# o `TeamsInfo.getTeamChannels` para las API de TypeScript.

## <a name="get-the-list-of-channels-in-a-team"></a>Obtiene la lista de canales en un equipo

El bot puede consultar la lista de canales de un equipo.

> [!NOTE]
>
> * El nombre del canal predeterminado General se devuelve como `null` para permitir la localización.
> * El identificador de canal General siempre coincide con el identificador de equipo.

El siguiente código de ejemplo se usa para obtener la lista de canales de un equipo:

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

Puede emitir directamente una solicitud GET en `/v3/teams/{teamId}/conversations`, utilizando el valor de `serviceUrl` como punto de conexión. El valor de `serviceUrl` es estable, pero puede cambiar. Cuando llega un nuevo mensaje, el bot debe comprobar su valor almacenado para `serviceUrl`.

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

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Enviar y recibir archivos a través del bot](~/bots/how-to/bots-filesv4.md)

## <a name="see-also"></a>Consulte también

* [Localizar la aplicación](../../concepts/build-and-test/apps-localization.md)
* [Obtener la foto de perfil de un usuario, un grupo, un equipo o un contacto de Outlook](/graph/api/profilephoto-get)

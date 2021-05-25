---
title: Obtener Teams contexto específico para el bot
author: laujan
description: Cómo obtener el contexto específico de Microsoft Team para el bot, incluida la lista de conversaciones, los detalles y la lista de canales.
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 6a8f903fb2f3ed8120e31b7536b65f22fdf6d620
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630169"
---
# <a name="get-teams-specific-context-for-your-bot"></a><span data-ttu-id="abce8-103">Obtener Teams contexto específico para el bot</span><span class="sxs-lookup"><span data-stu-id="abce8-103">Get Teams specific context for your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="abce8-104">Un bot puede tener acceso a datos de contexto adicionales sobre un equipo o chat donde está instalado.</span><span class="sxs-lookup"><span data-stu-id="abce8-104">A bot can access additional context data about a team or chat where it is installed.</span></span> <span data-ttu-id="abce8-105">Esta información se puede usar para enriquecer la funcionalidad del bot y proporcionar una experiencia más personalizada.</span><span class="sxs-lookup"><span data-stu-id="abce8-105">This information can be used to enrich the bot's functionality and provide a more personalized experience.</span></span>

## <a name="fetch-the-roster-or-user-profile"></a><span data-ttu-id="abce8-106">Capturar la lista o el perfil de usuario</span><span class="sxs-lookup"><span data-stu-id="abce8-106">Fetch the roster or user profile</span></span>

<span data-ttu-id="abce8-107">El bot puede consultar la lista de miembros y sus perfiles de usuario básicos, incluidos Teams id. de usuario e información de Azure Active Directory (AAD), como name y objectId.</span><span class="sxs-lookup"><span data-stu-id="abce8-107">Your bot can query for the list of members and their basic user profiles, including Teams user IDs and Azure Active Directory (AAD) information, such as name and objectId.</span></span> <span data-ttu-id="abce8-108">Puede usar esta información para correlacionar identidades de usuario.</span><span class="sxs-lookup"><span data-stu-id="abce8-108">You can use this information to correlate user identities.</span></span> <span data-ttu-id="abce8-109">Por ejemplo, para comprobar si un usuario ha iniciado sesión en una pestaña a través de credenciales de AAD, es miembro del equipo.</span><span class="sxs-lookup"><span data-stu-id="abce8-109">For example, to check whether a user logged into a tab through AAD credentials, is a member of the team.</span></span> <span data-ttu-id="abce8-110">Para obtener miembros de conversación, el tamaño mínimo o máximo de la página depende de la implementación.</span><span class="sxs-lookup"><span data-stu-id="abce8-110">For get conversation members, minimum or maximum page size depends on the implementation.</span></span> <span data-ttu-id="abce8-111">El tamaño de página inferior a 50, se trata como 50 y mayor que 500, se recorta en 500.</span><span class="sxs-lookup"><span data-stu-id="abce8-111">Page size less than 50, are treated as 50, and greater than 500, are capped at 500.</span></span> <span data-ttu-id="abce8-112">Incluso si usa la versión no paginada, no es confiable en equipos grandes y no debe usarse.</span><span class="sxs-lookup"><span data-stu-id="abce8-112">Even if you use the non-paged version, it is unreliable in large teams and must not be used.</span></span> <span data-ttu-id="abce8-113">Para obtener más información, vea cambios en las API Teams [Bot para capturar miembros de equipo o chat.](~/resources/team-chat-member-api-changes.md)</span><span class="sxs-lookup"><span data-stu-id="abce8-113">For more information, see [changes to Teams Bot APIs for fetching team or chat members](~/resources/team-chat-member-api-changes.md).</span></span>

<span data-ttu-id="abce8-114">El siguiente código de ejemplo usa el extremo paginado para capturar la lista:</span><span class="sxs-lookup"><span data-stu-id="abce8-114">The following sample code uses the paged endpoint for fetching the roster:</span></span>

# <a name="c"></a>[<span data-ttu-id="abce8-115">C#</span><span class="sxs-lookup"><span data-stu-id="abce8-115">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="abce8-116">TypeScript</span><span class="sxs-lookup"><span data-stu-id="abce8-116">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="abce8-117">Python</span><span class="sxs-lookup"><span data-stu-id="abce8-117">Python</span></span>](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    members = await TeamsInfo.get_team_members(turn_context)
```

# <a name="json"></a>[<span data-ttu-id="abce8-118">JSON</span><span class="sxs-lookup"><span data-stu-id="abce8-118">JSON</span></span>](#tab/json)

<span data-ttu-id="abce8-119">Puede emitir directamente una solicitud GET en `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}` , usando el valor de como punto de `serviceUrl` conexión.</span><span class="sxs-lookup"><span data-stu-id="abce8-119">You can directly issue a GET request on `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="abce8-120">El valor de `serviceUrl` es estable, pero puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="abce8-120">The value of `serviceUrl` is stable but can change.</span></span> <span data-ttu-id="abce8-121">Cuando llega un mensaje nuevo, el bot debe comprobar su valor almacenado para `serviceUrl` .</span><span class="sxs-lookup"><span data-stu-id="abce8-121">When a new message arrives, your bot must verify its stored value for `serviceUrl`.</span></span> <span data-ttu-id="abce8-122">La carga de respuesta también indica si el usuario es un usuario normal o anónimo.</span><span class="sxs-lookup"><span data-stu-id="abce8-122">The response payload also indicates if the user is a regular or anonymous user.</span></span>

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

<span data-ttu-id="abce8-123">Después de capturar la lista o el perfil de usuario, puede obtener los detalles de un solo miembro.</span><span class="sxs-lookup"><span data-stu-id="abce8-123">After you fetch the roster or user profile, you can get details of a single member.</span></span> <span data-ttu-id="abce8-124">Actualmente, para recuperar información para uno o varios miembros de un chat o equipo, use las API de bots de Microsoft Teams para C# o para las `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` API de TypeScript.</span><span class="sxs-lookup"><span data-stu-id="abce8-124">Currently, to retrieve information for one or more members of a chat or team, use the Microsoft Teams bot APIs `TeamsInfo.GetMembersAsync` for C# or `TeamsInfo.getMembers` for TypeScript APIs.</span></span>

## <a name="get-single-member-details"></a><span data-ttu-id="abce8-125">Obtener detalles de un solo miembro</span><span class="sxs-lookup"><span data-stu-id="abce8-125">Get single member details</span></span>

<span data-ttu-id="abce8-126">También puede recuperar los detalles de un usuario determinado mediante su Teams de usuario, UPN o id. de objeto de AAD.</span><span class="sxs-lookup"><span data-stu-id="abce8-126">You can also retrieve the details of a particular user using their Teams user ID, UPN, or AAD Object ID.</span></span>

<span data-ttu-id="abce8-127">El siguiente código de ejemplo se usa para obtener detalles de un solo miembro:</span><span class="sxs-lookup"><span data-stu-id="abce8-127">The following sample code is used to get single member details:</span></span>

# <a name="c"></a>[<span data-ttu-id="abce8-128">C#</span><span class="sxs-lookup"><span data-stu-id="abce8-128">C#</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);
    }
}
```

# <a name="typescript"></a>[<span data-ttu-id="abce8-129">TypeScript</span><span class="sxs-lookup"><span data-stu-id="abce8-129">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="abce8-130">Python</span><span class="sxs-lookup"><span data-stu-id="abce8-130">Python</span></span>](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    member = await TeamsInfo.get_member(turn_context, turn_context.activity.from_property.id)
```

# <a name="json"></a>[<span data-ttu-id="abce8-131">JSON</span><span class="sxs-lookup"><span data-stu-id="abce8-131">JSON</span></span>](#tab/json)

<span data-ttu-id="abce8-132">Puede emitir directamente una solicitud GET en `/v3/conversations/{conversationId}/members/{userId}` , usando el valor de como punto de `serviceUrl` conexión.</span><span class="sxs-lookup"><span data-stu-id="abce8-132">You can directly issue a GET request on `/v3/conversations/{conversationId}/members/{userId}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="abce8-133">El valor de `serviceUrl` es estable, pero puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="abce8-133">The value of `serviceUrl` is stable but can change.</span></span> <span data-ttu-id="abce8-134">Cuando llega un mensaje nuevo, el bot debe comprobar su valor almacenado para `serviceUrl` .</span><span class="sxs-lookup"><span data-stu-id="abce8-134">When a new message arrives, your bot must verify its stored value for `serviceUrl`.</span></span> <span data-ttu-id="abce8-135">Esto se puede usar para usuarios normales y usuarios anónimos.</span><span class="sxs-lookup"><span data-stu-id="abce8-135">This can be used for regular users and anonymous users.</span></span>

<span data-ttu-id="abce8-136">A continuación se muestra el ejemplo de respuesta para el usuario normal:</span><span class="sxs-lookup"><span data-stu-id="abce8-136">The following is the response sample for regular user:</span></span>

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

<span data-ttu-id="abce8-137">A continuación se muestra el ejemplo de respuesta para el usuario anónimo:</span><span class="sxs-lookup"><span data-stu-id="abce8-137">The following is the response sample for anonymous user:</span></span>

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

<span data-ttu-id="abce8-138">Después de obtener los detalles de un solo miembro, puede obtener detalles del equipo.</span><span class="sxs-lookup"><span data-stu-id="abce8-138">After you get details of a single member, you can get details of the team.</span></span> <span data-ttu-id="abce8-139">Actualmente, para recuperar información para un equipo, use las API de bots Microsoft Teams para `TeamsInfo.GetMemberDetailsAsync` C# o `TeamsInfo.getTeamDetails` para TypeScript.</span><span class="sxs-lookup"><span data-stu-id="abce8-139">Currently, to retrieve information for a team, use the Microsoft Teams bot APIs `TeamsInfo.GetMemberDetailsAsync` for C# or `TeamsInfo.getTeamDetails` for TypeScript.</span></span>

## <a name="get-teams-details"></a><span data-ttu-id="abce8-140">Obtener los detalles del equipo</span><span class="sxs-lookup"><span data-stu-id="abce8-140">Get team's details</span></span>

<span data-ttu-id="abce8-141">Cuando se instala en un equipo, el bot puede consultar metadatos sobre ese equipo, incluido el identificador de grupo de AAD.</span><span class="sxs-lookup"><span data-stu-id="abce8-141">When installed in a team, your bot can query for metadata about that team including the AAD group ID.</span></span>

<span data-ttu-id="abce8-142">El siguiente código de ejemplo se usa para obtener los detalles del equipo:</span><span class="sxs-lookup"><span data-stu-id="abce8-142">The following sample code is used to get team's details:</span></span>

# <a name="c"></a>[<span data-ttu-id="abce8-143">C#</span><span class="sxs-lookup"><span data-stu-id="abce8-143">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="abce8-144">TypeScript</span><span class="sxs-lookup"><span data-stu-id="abce8-144">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="abce8-145">Python</span><span class="sxs-lookup"><span data-stu-id="abce8-145">Python</span></span>](#tab/python)

```python
async def _show_details(self, turn_context: TurnContext):
    team_details = await TeamsInfo.get_team_details(turn_context)
    reply = MessageFactory.text(f"The team name is {team_details.name}. The team ID is {team_details.id}. The AADGroupID is {team_details.aad_group_id}.")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[<span data-ttu-id="abce8-146">JSON</span><span class="sxs-lookup"><span data-stu-id="abce8-146">JSON</span></span>](#tab/json)

<span data-ttu-id="abce8-147">Puede emitir directamente una solicitud GET en `/v3/teams/{teamId}` , usando el valor de como punto de `serviceUrl` conexión.</span><span class="sxs-lookup"><span data-stu-id="abce8-147">You can directly issue a GET request on `/v3/teams/{teamId}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="abce8-148">El valor de `serviceUrl` es estable, pero puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="abce8-148">The value of `serviceUrl` is stable but can change.</span></span> <span data-ttu-id="abce8-149">Cuando llega un mensaje nuevo, el bot debe comprobar su valor almacenado para `serviceUrl` .</span><span class="sxs-lookup"><span data-stu-id="abce8-149">When a new message arrives, your bot must verify its stored value for `serviceUrl`.</span></span>

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

<span data-ttu-id="abce8-150">Después de obtener los detalles del equipo, puede obtener la lista de canales de un equipo.</span><span class="sxs-lookup"><span data-stu-id="abce8-150">After you get details of the team, you can get the list of channels in a team.</span></span> <span data-ttu-id="abce8-151">Actualmente, para recuperar información de una lista de canales de un equipo, use las API de bots de Microsoft Teams para C# o para las `TeamsInfo.GetTeamChannelsAsync` `TeamsInfo.getTeamChannels` API de TypeScript.</span><span class="sxs-lookup"><span data-stu-id="abce8-151">Currently, to retrieve information for a list of channels in a team, use the Microsoft Teams bot APIs `TeamsInfo.GetTeamChannelsAsync` for C# or `TeamsInfo.getTeamChannels` for TypeScript APIs.</span></span>

## <a name="get-the-list-of-channels-in-a-team"></a><span data-ttu-id="abce8-152">Obtener la lista de canales de un equipo</span><span class="sxs-lookup"><span data-stu-id="abce8-152">Get the list of channels in a team</span></span>

<span data-ttu-id="abce8-153">El bot puede consultar la lista de canales de un equipo.</span><span class="sxs-lookup"><span data-stu-id="abce8-153">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
> * <span data-ttu-id="abce8-154">El nombre del canal general predeterminado se devuelve como `null` para permitir la localización.</span><span class="sxs-lookup"><span data-stu-id="abce8-154">The name of the default General channel is returned as `null` to allow for localization.</span></span>
> * <span data-ttu-id="abce8-155">El identificador de canal del canal general siempre coincide con el id. de equipo.</span><span class="sxs-lookup"><span data-stu-id="abce8-155">The channel ID for the General channel always matches the team ID.</span></span>

<span data-ttu-id="abce8-156">El siguiente código de ejemplo se usa para obtener la lista de canales de un equipo:</span><span class="sxs-lookup"><span data-stu-id="abce8-156">The following sample code is used to get the list of channels in a team:</span></span>

# <a name="c"></a>[<span data-ttu-id="abce8-157">C#</span><span class="sxs-lookup"><span data-stu-id="abce8-157">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="abce8-158">TypeScript</span><span class="sxs-lookup"><span data-stu-id="abce8-158">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="abce8-159">Python</span><span class="sxs-lookup"><span data-stu-id="abce8-159">Python</span></span>](#tab/python)

```python
async def _show_channels(
    self, turn_context: TurnContext
):
    channels = await TeamsInfo.get_team_channels(turn_context)
    reply = MessageFactory.text(f"Total of {len(channels)} channels are currently in team")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[<span data-ttu-id="abce8-160">JSON</span><span class="sxs-lookup"><span data-stu-id="abce8-160">JSON</span></span>](#tab/json)

<span data-ttu-id="abce8-161">Puede emitir directamente una solicitud GET en `/v3/teams/{teamId}/conversations` , usando el valor de como punto de `serviceUrl` conexión.</span><span class="sxs-lookup"><span data-stu-id="abce8-161">You can directly issue a GET request on `/v3/teams/{teamId}/conversations`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="abce8-162">El valor de `serviceUrl` es estable, pero puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="abce8-162">The value of `serviceUrl` is stable but can change.</span></span> <span data-ttu-id="abce8-163">Cuando llega un mensaje nuevo, el bot debe comprobar su valor almacenado para `serviceUrl` .</span><span class="sxs-lookup"><span data-stu-id="abce8-163">When a new message arrives, your bot must verify its stored value for `serviceUrl`.</span></span>

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

## <a name="next-step"></a><span data-ttu-id="abce8-164">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="abce8-164">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="abce8-165">Enviar y recibir archivos a través del bot</span><span class="sxs-lookup"><span data-stu-id="abce8-165">Send and receive files through the bot</span></span>](~/bots/how-to/bots-filesv4.md)

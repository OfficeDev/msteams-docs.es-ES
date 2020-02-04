---
title: Obtener contexto para el bot
description: Describe cómo obtener el contexto de bots en Microsoft Teams.
keywords: contexto de los bots de Microsoft Teams
ms.date: 05/20/2019
ms.openlocfilehash: 2dea6fd51e7274fa899d9ae882441a21618d7e09
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676196"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a><span data-ttu-id="0b6ff-104">Obtener contexto para su bot de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0b6ff-104">Get context for your Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="0b6ff-105">El bot puede tener acceso al contexto adicional del equipo o del chat, como un perfil de usuario.</span><span class="sxs-lookup"><span data-stu-id="0b6ff-105">Your bot can access additional context about the team or chat, such as user profile.</span></span> <span data-ttu-id="0b6ff-106">Esta información puede usarse para enriquecer la funcionalidad del bot y proporcionar una experiencia más personalizada.</span><span class="sxs-lookup"><span data-stu-id="0b6ff-106">This information can be used to enrich your bot's functionality and provide a more personalized experience.</span></span>

> [!NOTE]
> <span data-ttu-id="0b6ff-107">Se puede obtener&ndash;acceso mejor a estas API de bot específicas de Microsoft Teams mediante nuestras extensiones para el SDK de bot Builder.</span><span class="sxs-lookup"><span data-stu-id="0b6ff-107">These Microsoft Teams&ndash;specific bot APIs are best accessed through our extensions for the Bot Builder SDK.</span></span> <span data-ttu-id="0b6ff-108">Para C#/.NET, descargue nuestro paquete NuGet [Microsoft. bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) .</span><span class="sxs-lookup"><span data-stu-id="0b6ff-108">For C#/.NET, download our [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span> <span data-ttu-id="0b6ff-109">Para el desarrollo de node. js, puede instalar el paquete NPM [de botbuilder-Teams](https://www.npmjs.com/package/botbuilder-teams) .</span><span class="sxs-lookup"><span data-stu-id="0b6ff-109">For Node.js development, you can install the [botbuilder-teams](https://www.npmjs.com/package/botbuilder-teams) npm package.</span></span> <span data-ttu-id="0b6ff-110">El creador de bot de destino V3 de ambos SDK.</span><span class="sxs-lookup"><span data-stu-id="0b6ff-110">Both SDKs target Bot Builder v3.</span></span>

## <a name="fetching-the-team-roster"></a><span data-ttu-id="0b6ff-111">Obtención de la lista del equipo</span><span class="sxs-lookup"><span data-stu-id="0b6ff-111">Fetching the team roster</span></span>

<span data-ttu-id="0b6ff-112">El bot puede consultar la lista de miembros del equipo y sus perfiles básicos, que incluye los identificadores de usuario de Microsoft Teams y Azure Active Directory (Azure AD) información como Name y objectId.</span><span class="sxs-lookup"><span data-stu-id="0b6ff-112">Your bot can query for the list of team members and their basic profiles, which includes Teams user IDs and Azure Active Directory (Azure AD) information such as name and objectId.</span></span> <span data-ttu-id="0b6ff-113">Puede usar esta información para correlacionar las identidades de usuario; por ejemplo, para comprobar si un usuario que inició sesión en una pestaña a través de las credenciales de Azure AD es miembro del equipo.</span><span class="sxs-lookup"><span data-stu-id="0b6ff-113">You can use this information to correlate user identities; for example, to check whether a user logged into a tab through Azure AD credentials is a member of the team.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="0b6ff-114">Ejemplo de API de REST</span><span class="sxs-lookup"><span data-stu-id="0b6ff-114">REST API example</span></span>

<span data-ttu-id="0b6ff-115">Puede emitir directamente una solicitud [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members)Get usando el valor de como punto de `serviceUrl` conexión.</span><span class="sxs-lookup"><span data-stu-id="0b6ff-115">You can directly issue a GET request on [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members), using the value of `serviceUrl` as the endpoint.</span></span>

<span data-ttu-id="0b6ff-116">El `teamId` puede encontrarse en `channeldata` el objeto de la carga de actividad que el bot recibe en los siguientes escenarios:</span><span class="sxs-lookup"><span data-stu-id="0b6ff-116">The `teamId` can be found in the `channeldata` object of the activity payload that your bot receives in the following scenarios:</span></span>
* <span data-ttu-id="0b6ff-117">Cuando un usuario recibe un mensaje o interactúa con el bot en un contexto de equipo (consulte [recibir mensajes](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages))</span><span class="sxs-lookup"><span data-stu-id="0b6ff-117">When a user messages or interacts with your bot in a team context (see [Receiving Messages](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages))</span></span>
* <span data-ttu-id="0b6ff-118">Cuando se agrega un nuevo usuario o un bot a un equipo (vea el [Bot o el usuario agregado a un equipo](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team))</span><span class="sxs-lookup"><span data-stu-id="0b6ff-118">When a new user or bot is added to a team (see [Bot or user added to a team](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team))</span></span>

> [!NOTE]
>* <span data-ttu-id="0b6ff-119">Asegúrese de usar el identificador de equipo al llamar a la API</span><span class="sxs-lookup"><span data-stu-id="0b6ff-119">Make sure to use the team id when calling the api</span></span>
>* <span data-ttu-id="0b6ff-120">El valor de `serviceUrl` tiende a ser estable, pero puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="0b6ff-120">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="0b6ff-121">Cuando llega un nuevo mensaje, el bot debe comprobar su valor almacenado de `serviceUrl`.</span><span class="sxs-lookup"><span data-stu-id="0b6ff-121">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

```json
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

### <a name="net-example"></a><span data-ttu-id="0b6ff-122">Ejemplo de .NET</span><span class="sxs-lookup"><span data-stu-id="0b6ff-122">.NET example</span></span>

<span data-ttu-id="0b6ff-123">Llamar `GetConversationMembersAsync` a `Team.Id` usando para devolver una lista de identificadores de usuario.</span><span class="sxs-lookup"><span data-stu-id="0b6ff-123">Call `GetConversationMembersAsync` using `Team.Id` to return a list of user IDs.</span></span>

```csharp
// Fetch the members in the current conversation
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));
var teamId = context.Activity.GetChannelData<TeamsChannelData>().Team.Id;
var members = await connector.Conversations.GetConversationMembersAsync(teamId);

// Concatenate information about all members into a string
var sb = new StringBuilder();
foreach (var member in members.AsTeamsChannelAccounts())
{
    sb.AppendFormat(
        "GivenName = {0}, TeamsMemberId = {1}",
        member.Name, member.Id);

    sb.AppendLine();
}

// Post the member info back into the conversation
await context.PostAsync($"People in this conversation: {sb.ToString()}");
```

### <a name="nodejstypescript-example"></a><span data-ttu-id="0b6ff-124">Ejemplo de node. js/TypeScript</span><span class="sxs-lookup"><span data-stu-id="0b6ff-124">Node.js/TypeScript example</span></span>

<span data-ttu-id="0b6ff-125">En el siguiente ejemplo, se usan las [extensiones de Microsoft Teams para el SDK de bot Builder para node. js](https://www.npmjs.com/package/botbuilder-teams).</span><span class="sxs-lookup"><span data-stu-id="0b6ff-125">The following example uses the [Microsoft Teams extensions for the Bot Builder SDK for Node.js](https://www.npmjs.com/package/botbuilder-teams).</span></span>

```typescript

[...]
import * as builder from "botbuilder";
[...]

var teamId = session.message.sourceEvent.team.id;
connector.fetchMembers(
  (<builder.IChatConnectorAddress>session.message.address).serviceUrl,
  teamId,
  (err, result) => {
    if (err) {
      session.endDialog('There is some error');
    }
    else {
      session.endDialog('%s', JSON.stringify(result));
    }
  }
);
```

## <a name="fetching-user-profile-or-roster-in-personal-or-group-chat"></a><span data-ttu-id="0b6ff-126">Obtención de un perfil de usuario o una lista en un chat de grupo o personal</span><span class="sxs-lookup"><span data-stu-id="0b6ff-126">Fetching user profile or roster in personal or group chat</span></span>

<span data-ttu-id="0b6ff-127">También puede realizar la misma llamada de API para cualquier chat personal para obtener la información de perfil del usuario que Chatea con su bot.</span><span class="sxs-lookup"><span data-stu-id="0b6ff-127">You can also make the same API call for any personal chat to obtain the profile information of the user chatting with your bot.</span></span>

<span data-ttu-id="0b6ff-128">Los métodos Call y SDK de la API son idénticos a la recopilación de la lista de equipos, al igual que el objeto de respuesta.</span><span class="sxs-lookup"><span data-stu-id="0b6ff-128">The API call and SDK methods are identical to fetching the team roster, as is the response object.</span></span> <span data-ttu-id="0b6ff-129">La única diferencia es que se pasa `conversationId` el en lugar del `teamId`.</span><span class="sxs-lookup"><span data-stu-id="0b6ff-129">The only difference is you pass the `conversationId` instead of the `teamId`.</span></span>

## <a name="fetching-the-list-of-channels-in-a-team"></a><span data-ttu-id="0b6ff-130">Obtención de la lista de canales en un equipo</span><span class="sxs-lookup"><span data-stu-id="0b6ff-130">Fetching the list of channels in a team</span></span>

<span data-ttu-id="0b6ff-131">El bot puede consultar la lista de canales de un equipo.</span><span class="sxs-lookup"><span data-stu-id="0b6ff-131">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="0b6ff-132">El nombre del canal general predeterminado se devuelve como `null` permitir para la localización.</span><span class="sxs-lookup"><span data-stu-id="0b6ff-132">The name of the default General channel is returned as `null` to allow for localization.</span></span>
>* <span data-ttu-id="0b6ff-133">El identificador de canal para el canal general coincide siempre con el identificador del equipo.</span><span class="sxs-lookup"><span data-stu-id="0b6ff-133">The channel ID for the General channel always matches the team ID.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="0b6ff-134">Ejemplo de API de REST</span><span class="sxs-lookup"><span data-stu-id="0b6ff-134">REST API example</span></span>

<span data-ttu-id="0b6ff-135">Puede emitir directamente una solicitud `/teams/{teamId}/conversations/`Get usando el valor de como punto de `serviceUrl` conexión.</span><span class="sxs-lookup"><span data-stu-id="0b6ff-135">You can directly issue a GET request on `/teams/{teamId}/conversations/`, using the value of `serviceUrl` as the endpoint.</span></span>

<span data-ttu-id="0b6ff-136">El único origen de `teamId` es un mensaje del contexto de equipo, ya sea un mensaje de un usuario o el mensaje que el bot recibe cuando se agrega a un equipo (vea el [Bot o el usuario agregado a un equipo](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)).</span><span class="sxs-lookup"><span data-stu-id="0b6ff-136">The only source for `teamId` is a message from the team context - either a message from a user or the message that your bot receives when it is added to a team (see [Bot or user added to a team](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)).</span></span>

> [!NOTE]
> <span data-ttu-id="0b6ff-137">El valor de `serviceUrl` tiende a ser estable, pero puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="0b6ff-137">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="0b6ff-138">Cuando llega un nuevo mensaje, el bot debe comprobar su valor almacenado de `serviceUrl`.</span><span class="sxs-lookup"><span data-stu-id="0b6ff-138">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

```json
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

#### <a name="net-example"></a><span data-ttu-id="0b6ff-139">Ejemplo de .NET</span><span class="sxs-lookup"><span data-stu-id="0b6ff-139">.NET example</span></span>

<span data-ttu-id="0b6ff-140">En el siguiente ejemplo, `FetchChannelList` se usa la llamada de las [extensiones de Microsoft Teams para el SDK de bot Builder para .net](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):</span><span class="sxs-lookup"><span data-stu-id="0b6ff-140">The following example uses the `FetchChannelList` call from the [Microsoft Teams extensions for the Bot Builder SDK for .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):</span></span>

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a><span data-ttu-id="0b6ff-141">Ejemplo de node. js</span><span class="sxs-lookup"><span data-stu-id="0b6ff-141">Node.js example</span></span>

<span data-ttu-id="0b6ff-142">En el siguiente ejemplo `fetchChannelList` , se usa la llamada de las [extensiones de Microsoft Teams para el SDK de bot Builder para node. js](https://www.npmjs.com/package/botbuilder-teams).</span><span class="sxs-lookup"><span data-stu-id="0b6ff-142">The following example uses `fetchChannelList` call from the [Microsoft Teams extensions for the Bot Builder SDK for Node.js](https://www.npmjs.com/package/botbuilder-teams).</span></span>

```javascript
var teamId = session.message.sourceEvent.team.id;
connector.fetchChannelList(
  (session.message.address).serviceUrl,
  teamId,
  (err, result) => {
    if (err) {
      session.endDialog('There is an error');
    }
    else {
      session.endDialog('%s', JSON.stringify(result));
    }
  }
);
```

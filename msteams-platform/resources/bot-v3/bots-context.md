---
title: Obtener contexto para el bot de Microsoft Teams
description: Describe cómo obtener contexto para bots en Microsoft Teams
keywords: contexto de bots de teams
ms.topic: conceptual
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: 154a276c65987955cfe20e5b7ce4ed2e8973cbfd
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020663"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a><span data-ttu-id="2ce8e-104">Obtener contexto para el bot de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="2ce8e-104">Get context for your Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="2ce8e-105">El bot puede tener acceso a contexto adicional sobre el equipo o el chat, como el perfil de usuario.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-105">Your bot can access additional context about the team or chat, such as user profile.</span></span> <span data-ttu-id="2ce8e-106">Esta información se puede usar para enriquecer la funcionalidad del bot y proporcionar una experiencia más personalizada.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-106">This information can be used to enrich your bot's functionality and provide a more personalized experience.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="2ce8e-107">Las API de bot específicas de Microsoft Teams tienen mejor acceso a través de nuestras extensiones para el SDK de Bot Builder.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-107">Microsoft Teams-specific bot APIs are best accessed through our extensions for the Bot Builder SDK.</span></span>
> * <span data-ttu-id="2ce8e-108">Para C# o .NET, descargue nuestro [paquete NuGet de Microsoft.Bot.Connector.Teams.](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)</span><span class="sxs-lookup"><span data-stu-id="2ce8e-108">For C# or .NET, download our [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>
> * <span data-ttu-id="2ce8e-109">Para Node.js desarrollo, la funcionalidad del Generador de bots para Teams se incorpora al [SDK de Bot Framework](https://github.com/microsoft/botframework-sdk) v4.6.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-109">For Node.js development, the Bot Builder for Teams functionality is incorporated into the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) v4.6.</span></span>

## <a name="fetch-the-team-roster"></a><span data-ttu-id="2ce8e-110">Capturar la lista de equipos</span><span class="sxs-lookup"><span data-stu-id="2ce8e-110">Fetch the team roster</span></span>

<span data-ttu-id="2ce8e-111">El bot puede consultar la lista de miembros del equipo y sus perfiles básicos.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-111">Your bot can query for the list of team members and their basic profiles.</span></span> <span data-ttu-id="2ce8e-112">Los perfiles básicos incluyen identificadores de usuario de Teams e información de Azure Active Directory (AAD), como el nombre y el identificador de objeto.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-112">The basic profiles include Teams user IDs and Azure Active Directory (AAD) information such as name and object ID.</span></span> <span data-ttu-id="2ce8e-113">Puede usar esta información para correlacionar identidades de usuario.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-113">You can use this information to correlate user identities.</span></span> <span data-ttu-id="2ce8e-114">Por ejemplo, compruebe si un usuario que ha iniciado sesión en una pestaña a través de las credenciales de AAD es un miembro del equipo.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-114">For example, check if a user logged into a tab through AAD credentials is a team member.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="2ce8e-115">Ejemplo de API de REST</span><span class="sxs-lookup"><span data-stu-id="2ce8e-115">REST API example</span></span>

<span data-ttu-id="2ce8e-116">Emita directamente una solicitud GET en [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members) , usando el valor como punto de `serviceUrl` conexión.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-116">Directly issue a GET request on [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members), using the `serviceUrl` value as the endpoint.</span></span>

<span data-ttu-id="2ce8e-117">Se `teamId` puede encontrar en el objeto de la carga de actividad que el bot recibe en los siguientes `channeldata` escenarios:</span><span class="sxs-lookup"><span data-stu-id="2ce8e-117">The `teamId` can be found in the `channeldata` object of the activity payload that your bot receives in the following scenarios:</span></span>

* <span data-ttu-id="2ce8e-118">Cuando un usuario mensajes o interactúa con el bot en un contexto de equipo.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-118">When a user messages or interacts with your bot in a team context.</span></span> <span data-ttu-id="2ce8e-119">Para obtener más información, vea [recibir mensajes](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages).</span><span class="sxs-lookup"><span data-stu-id="2ce8e-119">For more information, see [receiving messages](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages).</span></span>
* <span data-ttu-id="2ce8e-120">Cuando se agrega un nuevo usuario o bot a un equipo.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-120">When a new user or bot is added to a team.</span></span> <span data-ttu-id="2ce8e-121">Para obtener más información, vea [bot or user added to a team](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team).</span><span class="sxs-lookup"><span data-stu-id="2ce8e-121">For more information, see [bot or user added to a team](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team).</span></span>

> [!NOTE]
>
>* <span data-ttu-id="2ce8e-122">Use siempre el identificador de equipo al llamar a la API.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-122">Always use the team ID when calling the API.</span></span>
>* <span data-ttu-id="2ce8e-123">El `serviceUrl` valor tiende a ser estable, pero puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-123">The `serviceUrl` value tends to be stable but can change.</span></span> <span data-ttu-id="2ce8e-124">Cuando llega un mensaje nuevo, el bot debe comprobar su valor `serviceUrl` almacenado.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-124">When a new message arrives, your bot must verify its stored `serviceUrl` value.</span></span>

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

### <a name="net-example"></a><span data-ttu-id="2ce8e-125">Ejemplo de .NET</span><span class="sxs-lookup"><span data-stu-id="2ce8e-125">.NET example</span></span>

<span data-ttu-id="2ce8e-126">Llamar `GetConversationMembersAsync` a using para devolver una lista de `Team.Id` id. de usuario.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-126">Call `GetConversationMembersAsync` using `Team.Id` to return a list of user IDs.</span></span>

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

### <a name="nodejs-or-typescript-example"></a><span data-ttu-id="2ce8e-127">Node.js o TypeScript</span><span class="sxs-lookup"><span data-stu-id="2ce8e-127">Node.js or TypeScript example</span></span>

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

<span data-ttu-id="2ce8e-128">Además, vea [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="2ce8e-128">Also, see [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a><span data-ttu-id="2ce8e-129">Capturar perfil de usuario o lista en chat personal o de grupo</span><span class="sxs-lookup"><span data-stu-id="2ce8e-129">Fetch user profile or roster in personal or group chat</span></span>

<span data-ttu-id="2ce8e-130">Puedes realizar la llamada api para cualquier chat personal para obtener la información de perfil del usuario que chatea con el bot.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-130">You can make the API call for any personal chat to obtain the profile information of the user chatting with your bot.</span></span>

<span data-ttu-id="2ce8e-131">La llamada a la API, los métodos sdk y el objeto de respuesta son idénticos a la captura de la lista de equipos.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-131">The API call, SDK methods, and the response object are identical to fetching the team roster.</span></span> <span data-ttu-id="2ce8e-132">La única diferencia es que se pasa el `conversationId` en lugar de `teamId` .</span><span class="sxs-lookup"><span data-stu-id="2ce8e-132">The only difference is you pass the `conversationId` instead of the `teamId`.</span></span>

## <a name="fetch-the-list-of-channels-in-a-team"></a><span data-ttu-id="2ce8e-133">Capturar la lista de canales de un equipo</span><span class="sxs-lookup"><span data-stu-id="2ce8e-133">Fetch the list of channels in a team</span></span>

<span data-ttu-id="2ce8e-134">El bot puede consultar la lista de canales de un equipo.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-134">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="2ce8e-135">El nombre del canal general predeterminado se devuelve como `null` para permitir la localización.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-135">The name of the default General channel is returned as `null` to allow for localization.</span></span>
>* <span data-ttu-id="2ce8e-136">El identificador de canal del canal general siempre coincide con el id. de equipo.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-136">The channel ID for the General channel always matches the team ID.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="2ce8e-137">Ejemplo de API de REST</span><span class="sxs-lookup"><span data-stu-id="2ce8e-137">REST API example</span></span>

<span data-ttu-id="2ce8e-138">Emita directamente una solicitud GET en `/teams/{teamId}/conversations/` , usando el valor como punto de `serviceUrl` conexión.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-138">Directly issue a GET request on `/teams/{teamId}/conversations/`, using the `serviceUrl` value as the endpoint.</span></span>

<span data-ttu-id="2ce8e-139">El único origen es `teamId` un mensaje del contexto del equipo.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-139">The only source for `teamId` is a message from the team context.</span></span> <span data-ttu-id="2ce8e-140">El mensaje es un mensaje de un usuario o el mensaje que el bot recibe cuando se agrega a un equipo.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-140">The message is either a message from a user or the message that your bot receives when it is added to a team.</span></span> <span data-ttu-id="2ce8e-141">Para obtener más información, vea [bot or user added to a team](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition).</span><span class="sxs-lookup"><span data-stu-id="2ce8e-141">For more information, see [bot or user added to a team](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition).</span></span>

> [!NOTE]
> <span data-ttu-id="2ce8e-142">El `serviceUrl` valor tiende a ser estable, pero puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-142">The `serviceUrl` value tends to be stable but can change.</span></span> <span data-ttu-id="2ce8e-143">Cuando llega un mensaje nuevo, el bot debe comprobar su valor `serviceUrl` almacenado.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-143">When a new message arrives, your bot must verify its stored `serviceUrl` value.</span></span>

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

#### <a name="net-example"></a><span data-ttu-id="2ce8e-144">Ejemplo de .NET</span><span class="sxs-lookup"><span data-stu-id="2ce8e-144">.NET example</span></span>

<span data-ttu-id="2ce8e-145">En el ejemplo siguiente se usa la llamada desde las extensiones de Teams para `FetchChannelList` el SDK de Bot Builder para [.NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):</span><span class="sxs-lookup"><span data-stu-id="2ce8e-145">The following example uses the `FetchChannelList` call from the [Teams extensions for the Bot Builder SDK for .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):</span></span>

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a><span data-ttu-id="2ce8e-146">Node.js ejemplo</span><span class="sxs-lookup"><span data-stu-id="2ce8e-146">Node.js example</span></span>

<span data-ttu-id="2ce8e-147">En el ejemplo siguiente se usa una llamada desde las extensiones de Teams para el `fetchChannelList` SDK de Bot Builder para [Node.js](https://www.npmjs.com/package/botbuilder-teams):</span><span class="sxs-lookup"><span data-stu-id="2ce8e-147">The following example uses `fetchChannelList` call from the [Teams extensions for the Bot Builder SDK for Node.js](https://www.npmjs.com/package/botbuilder-teams):</span></span>

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

## <a name="get-clientinfo-in-your-bot-context"></a><span data-ttu-id="2ce8e-148">Obtener clientInfo en el contexto del bot</span><span class="sxs-lookup"><span data-stu-id="2ce8e-148">Get clientInfo in your bot context</span></span>

<span data-ttu-id="2ce8e-149">Puede capturar el clientInfo dentro de la actividad del bot.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-149">You can fetch the clientInfo within your bot's activity.</span></span> <span data-ttu-id="2ce8e-150">El clientInfo contiene las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="2ce8e-150">The clientInfo contains the following properties:</span></span>

* <span data-ttu-id="2ce8e-151">Locale</span><span class="sxs-lookup"><span data-stu-id="2ce8e-151">Locale</span></span>
* <span data-ttu-id="2ce8e-152">País</span><span class="sxs-lookup"><span data-stu-id="2ce8e-152">Country</span></span>
* <span data-ttu-id="2ce8e-153">Plataforma</span><span class="sxs-lookup"><span data-stu-id="2ce8e-153">Platform</span></span>
* <span data-ttu-id="2ce8e-154">Zona horaria</span><span class="sxs-lookup"><span data-stu-id="2ce8e-154">Timezone</span></span>

### <a name="json-example"></a><span data-ttu-id="2ce8e-155">Ejemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="2ce8e-155">JSON example</span></span>

```json
[
    {
        "type": "clientInfo",
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "Asia/Calcutta"
    }
]
```

### <a name="c-example"></a><span data-ttu-id="2ce8e-156">C# ejemplo</span><span class="sxs-lookup"><span data-stu-id="2ce8e-156">C# example</span></span>

```csharp
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));

{
    var clientinfo = context.Activity.Entities[0];
    await context.PostAsync($"ClientInfo: clientinfo ");
}
```

---
title: Obtener contexto para el bot de Microsoft Teams
description: Describe cómo obtener contexto para bots en Microsoft Teams
keywords: Contexto de bots de teams
ms.date: 05/20/2019
ms.openlocfilehash: 1465e6624b4eaadd73e2d4d9cf87fccedc002e52
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231557"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a>Obtener contexto para el bot de Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

El bot puede acceder a contexto adicional sobre el equipo o chat, como el perfil de usuario. Esta información se puede usar para enriquecer la funcionalidad del bot y proporcionar una experiencia más personalizada.

> [!NOTE]
>
> * Se puede acceder mejor a las API de bot específicas de Microsoft Teams a través de nuestras extensiones para el SDK de Bot Builder.
> * Para C# o .NET, descargue nuestro [paquete NuGet Microsoft.Bot.Connector.Teams.](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)
> * Para Node.js desarrollo, la funcionalidad del Generador de bots para Teams se incorpora al SDK de [Bot Framework](https://github.com/microsoft/botframework-sdk) v4.6.

## <a name="fetch-the-team-roster"></a>Obtener la lista del equipo

El bot puede consultar la lista de miembros del equipo y sus perfiles básicos. Los perfiles básicos incluyen identificadores de usuario de Teams e información de Azure Active Directory (AAD), como el nombre y el id. de objeto. Puede usar esta información para correlacionar las identidades de usuario. Por ejemplo, compruebe si un usuario que ha iniciado sesión en una pestaña a través de las credenciales de AAD es un miembro del equipo.

### <a name="rest-api-example"></a>Ejemplo de API de REST

Emitir directamente una solicitud GET [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members) en , usando el valor como el punto de `serviceUrl` conexión.

Puede `teamId` encontrarse en el objeto de la carga de actividad que el bot recibe en los siguientes `channeldata` escenarios:

* Cuando un usuario mensajes o interactúa con el bot en un contexto de equipo. Para obtener más información, vea [la recepción de mensajes.](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages)
* Cuando se agrega un nuevo usuario o bot a un equipo. Para obtener más información, vea [bot o usuario agregado a un equipo.](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team)

> [!NOTE]
>
>* Use siempre el identificador de equipo al llamar a la API.
>* El `serviceUrl` valor tiende a ser estable, pero puede cambiar. Cuando llega un nuevo mensaje, el bot debe comprobar su valor `serviceUrl` almacenado.

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

### <a name="net-example"></a>Ejemplo de .NET

Llamada `GetConversationMembersAsync` que se usa para devolver una lista de `Team.Id` id. de usuario.

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

### <a name="nodejs-or-typescript-example"></a>Node.js o TypeScript

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

Vea también ejemplos [de Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a>Obtener perfil de usuario o lista en chat personal o de grupo

Puede realizar la llamada API de cualquier chat personal para obtener la información de perfil del usuario que chatea con su bot.

La llamada API, los métodos sdk y el objeto de respuesta son idénticos a recuperar la lista de equipo. La única diferencia es que se pasa el `conversationId` archivo en lugar del archivo `teamId` .

## <a name="fetch-the-list-of-channels-in-a-team"></a>Obtener la lista de canales de un equipo

El bot puede consultar la lista de canales de un equipo.

> [!NOTE]
>
>* Se devuelve el nombre del canal general predeterminado para `null` permitir la localización.
>* El identificador de canal para el canal General siempre coincide con el identificador de equipo.

### <a name="rest-api-example"></a>Ejemplo de API de REST

Emitir directamente una solicitud GET `/teams/{teamId}/conversations/` en , usando el valor como el punto de `serviceUrl` conexión.

El único origen es `teamId` un mensaje del contexto del equipo. El mensaje es un mensaje de un usuario o el mensaje que el bot recibe cuando se agrega a un equipo. Para obtener más información, vea [bot o usuario agregado a un equipo.](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)

> [!NOTE]
> El `serviceUrl` valor tiende a ser estable, pero puede cambiar. Cuando llega un nuevo mensaje, el bot debe comprobar su valor `serviceUrl` almacenado.

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

#### <a name="net-example"></a>Ejemplo de .NET

En el siguiente ejemplo se `FetchChannelList` usa la llamada de las extensiones de Teams para el SDK de Bot Builder para [.NET:](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a>Node.js ejemplo

En el ejemplo siguiente se `fetchChannelList` usa la llamada de las extensiones de Teams para el SDK de Bot Builder [Node.js: ](https://www.npmjs.com/package/botbuilder-teams)

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

## <a name="get-clientinfo-in-your-bot-context"></a>Obtener clientInfo en el contexto del bot

Puede capturar clientInfo dentro de la actividad del bot. ClientInfo contiene las siguientes propiedades:

* Locale
* País
* Plataforma
* Zona horaria

### <a name="json-example"></a>Ejemplo de JSON

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

### <a name="c-example"></a>Ejemplo de C#

```csharp
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));

{
    var clientinfo = context.Activity.Entities[0];
    await context.PostAsync($"ClientInfo: clientinfo ");
}
```
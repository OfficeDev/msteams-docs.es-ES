---
title: Obtener contexto para el bot
description: Describe cómo obtener el contexto de bots en Microsoft Teams.
keywords: contexto de los bots de Microsoft Teams
ms.date: 05/20/2019
ms.openlocfilehash: 8f054661664850ffb843714230e209c8e4737f0a
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228009"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a>Obtener contexto para su bot de Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

El bot puede tener acceso al contexto adicional del equipo o del chat, como un perfil de usuario. Esta información puede usarse para enriquecer la funcionalidad del bot y proporcionar una experiencia más personalizada.

> [!NOTE]
> Se puede obtener&ndash;acceso mejor a estas API de bot específicas de Microsoft Teams mediante nuestras extensiones para el SDK de bot Builder. Para C#/.NET, descargue nuestro paquete NuGet [Microsoft. bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) . Para el desarrollo de node. js, la funcionalidad de BotBuilder para Microsoft Teams se ha incorporado al [SDK de bot Framework](https://github.com/microsoft/botframework-sdk) a partir de la versión de v 4.6.

## <a name="fetching-the-team-roster"></a>Obtención de la lista del equipo

El bot puede consultar la lista de miembros del equipo y sus perfiles básicos, que incluye los identificadores de usuario de Microsoft Teams y Azure Active Directory (Azure AD) información como Name y objectId. Puede usar esta información para correlacionar las identidades de usuario; por ejemplo, para comprobar si un usuario que inició sesión en una pestaña a través de las credenciales de Azure AD es miembro del equipo.

### <a name="rest-api-example"></a>Ejemplo de API de REST

Puede emitir directamente una solicitud [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members)Get usando el valor de como punto de `serviceUrl` conexión.

El `teamId` puede encontrarse en `channeldata` el objeto de la carga de actividad que el bot recibe en los siguientes escenarios:
* Cuando un usuario recibe un mensaje o interactúa con el bot en un contexto de equipo (consulte [recibir mensajes](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages))
* Cuando se agrega un nuevo usuario o un bot a un equipo (vea el [Bot o el usuario agregado a un equipo](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team))

> [!NOTE]
>* Asegúrese de usar el identificador de equipo al llamar a la API
>* El valor de `serviceUrl` tiende a ser estable, pero puede cambiar. Cuando llega un nuevo mensaje, el bot debe comprobar su valor almacenado de `serviceUrl`.

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

Llamar `GetConversationMembersAsync` a `Team.Id` usando para devolver una lista de identificadores de usuario.

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

### <a name="nodejstypescript-example"></a>Ejemplo de node. js/TypeScript

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

*Vea también* [ejemplos del marco de bot](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).

## <a name="fetching-user-profile-or-roster-in-personal-or-group-chat"></a>Obtención de un perfil de usuario o una lista en un chat de grupo o personal

También puede realizar la misma llamada de API para cualquier chat personal para obtener la información de perfil del usuario que Chatea con su bot.

Los métodos Call y SDK de la API son idénticos a la recopilación de la lista de equipos, al igual que el objeto de respuesta. La única diferencia es que se pasa `conversationId` el en lugar del `teamId`.

## <a name="fetching-the-list-of-channels-in-a-team"></a>Obtención de la lista de canales en un equipo

El bot puede consultar la lista de canales de un equipo.

> [!NOTE]
>
>* El nombre del canal general predeterminado se devuelve como `null` permitir para la localización.
>* El identificador de canal para el canal general coincide siempre con el identificador del equipo.

### <a name="rest-api-example"></a>Ejemplo de API de REST

Puede emitir directamente una solicitud `/teams/{teamId}/conversations/`Get usando el valor de como punto de `serviceUrl` conexión.

El único origen de `teamId` es un mensaje del contexto de equipo, ya sea un mensaje de un usuario o el mensaje que el bot recibe cuando se agrega a un equipo (vea el [Bot o el usuario agregado a un equipo](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)).

> [!NOTE]
> El valor de `serviceUrl` tiende a ser estable, pero puede cambiar. Cuando llega un nuevo mensaje, el bot debe comprobar su valor almacenado de `serviceUrl`.

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

En el siguiente ejemplo, `FetchChannelList` se usa la llamada de las [extensiones de Microsoft Teams para el SDK de bot Builder para .net](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a>Ejemplo de node. js

En el siguiente ejemplo `fetchChannelList` , se usa la llamada de las [extensiones de Microsoft Teams para el SDK de bot Builder para node. js](https://www.npmjs.com/package/botbuilder-teams).

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

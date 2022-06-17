---
title: Obtener contexto para el bot de Microsoft Teams
description: En este módulo, obtenga información sobre cómo obtener contexto para bots en Microsoft Teams, capturar la lista de equipos y el perfil de usuario o la lista en chat personal o grupal.
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: 3fd75e063f9b12c09bc4dded167bd8cdaead6b7a
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143119"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a>Obtener contexto para el bot de Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

El bot puede acceder a contextos adicionales sobre el equipo o el chat, como el perfil de usuario. Esta información se puede usar para enriquecer la funcionalidad del bot y proporcionar una experiencia más personalizada.

> [!NOTE]
>
> * Microsoft Teams API de bot específicas se accede mejor a través de nuestras extensiones del SDK de Bot Builder.
> * Para C# o .NET, descargue nuestro paquete [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet.
> * Para Node.js desarrollo, bot Builder para Teams funcionalidad se incorpora al [SDK de Bot Framework](https://github.com/microsoft/botframework-sdk) v4.6.

## <a name="fetch-the-team-roster"></a>Captura de la lista de equipos

El bot puede consultar la lista de miembros del equipo y sus perfiles básicos. Los perfiles básicos incluyen Teams identificadores de usuario e información de Microsoft Azure Active Directory (Azure AD), como el nombre y el identificador de objeto. Puede usar esta información para correlacionar las identidades de usuario. Por ejemplo, compruebe si un usuario que ha iniciado sesión en una pestaña a través de las credenciales de Microsoft Azure Active Directory (Azure AD) es miembro del equipo.

### <a name="rest-api-example"></a>Ejemplo de API REST

Emita directamente una solicitud GET en [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members), utilizando el `serviceUrl` valor como punto de conexión.

`teamId` Se puede encontrar en el `channeldata` objeto de la carga de actividad que recibe el bot en los siguientes escenarios:

* Cuando un usuario mensajes o interactúa con el bot en un contexto de equipo. Para obtener más información, consulte [Recepción de mensajes](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages).
* Cuando se agrega un nuevo usuario o bot a un equipo. Para obtener más información, consulte [bot o usuario agregado a un equipo](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team).

> [!NOTE]
>
>* Use siempre el identificador de equipo al llamar a la API.
>* El `serviceUrl` valor tiende a ser estable, pero puede cambiar. Cuando llega un nuevo mensaje, el bot debe comprobar su valor almacenado `serviceUrl` .

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

Llame a `GetConversationMembersAsync` using `Team.Id` para devolver una lista de identificadores de usuario.

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

### <a name="nodejs-or-typescript-example"></a>ejemplo de Node.js o TypeScript

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

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a>Capturar perfil de usuario o lista en chat personal o grupal

Puede realizar la llamada a la API para cualquier chat personal para obtener la información de perfil del usuario que chatea con el bot.

La llamada API, los métodos del SDK y el objeto de respuesta son idénticos a la captura de la lista de equipos. La única diferencia es que pasa en `conversationId` lugar de .`teamId`

## <a name="fetch-the-list-of-channels-in-a-team"></a>Captura de la lista de canales de un equipo

El bot puede consultar la lista de canales de un equipo.

> [!NOTE]
>
>* El nombre del canal predeterminado General se devuelve como `null` para permitir la localización.
>* El identificador de canal General siempre coincide con el identificador de equipo.

### <a name="rest-api-example"></a>Ejemplo de API REST

Emita directamente una solicitud GET en `/teams/{teamId}/conversations/`, utilizando el `serviceUrl` valor como punto de conexión.

El único origen de `teamId` es un mensaje del contexto del equipo. El mensaje es un mensaje de un usuario o el mensaje que recibe el bot cuando se agrega a un equipo. Para obtener más información, consulte [bot o usuario agregado a un equipo](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition).

> [!NOTE]
> El `serviceUrl` valor tiende a ser estable, pero puede cambiar. Cuando llega un nuevo mensaje, el bot debe comprobar su valor almacenado `serviceUrl` .

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

En el ejemplo siguiente se usa la `FetchChannelList` llamada desde las [extensiones de Teams del SDK de Bot Builder para .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a>Ejemplo de Node.js

En el ejemplo siguiente se usa `fetchChannelList` la llamada desde las [extensiones de Teams del SDK de Bot Builder para Node.js](https://www.npmjs.com/package/botbuilder-teams):

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
* Timezone

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

## <a name="see-also"></a>Consulte también

[Ejemplos de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).

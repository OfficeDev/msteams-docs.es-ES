---
title: Obtenga contexto para su bot de Microsoft Teams
description: Describe cómo obtener contexto para bots en Microsoft Teams
keywords: contexto de bots de equipos
ms.topic: conceptual
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: cda2e24816330964342b097f52bb955c8846c54a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566491"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a>Obtenga contexto para su bot de Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

El bot puede acceder a contexto adicional sobre el equipo o el chat, como el perfil de usuario. Esta información se puede utilizar para enriquecer la funcionalidad de su bot y proporcionar una experiencia más personalizada.

> [!NOTE]
>
> * Se puede acceder mejor a las API de bots específicas de Microsoft Teams a través de nuestras extensiones para el SDK de Bot Builder.
> * Para C# o .NET, descargue nuestro paquete de NuGet [Microsoft.Bot.Connector.Teams.](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)
> * Para Node.js desarrollo, el Generador de bots para Teams funcionalidad se incorpora al SDK de [Bot Framework](https://github.com/microsoft/botframework-sdk) v4.6.

## <a name="fetch-the-team-roster"></a>Buscar la lista del equipo

El bot puede consultar la lista de miembros del equipo y sus perfiles básicos. Los perfiles básicos incluyen Teams Azure Active Directory id. Puede utilizar esta información para correlacionar las identidades de usuario. Por ejemplo, compruebe si un usuario que ha iniciado sesión en una pestaña a través de credenciales de AAD es miembro del equipo.

### <a name="rest-api-example"></a>Ejemplo de API de REST

Emita directamente una solicitud GET en [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members) , utilizando el valor como punto de `serviceUrl` conexión.

Se `teamId` puede encontrar en el objeto de la carga de actividad que recibe el bot en los siguientes `channeldata` escenarios:

* Cuando un usuario envía mensajes o interactúa con el bot en un contexto de equipo. Para obtener más información, consulte [recepción de mensajes](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages).
* Cuando se agrega un nuevo usuario o bot a un equipo. Para obtener más información, consulte [bot o usuario agregado a un equipo.](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team)

> [!NOTE]
>
>* Utilice siempre el identificador de equipo al llamar a la API.
>* El `serviceUrl` valor tiende a ser estable, pero puede cambiar. Cuando llega un nuevo mensaje, el bot debe comprobar su `serviceUrl` valor almacenado.

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

Llamada `GetConversationMembersAsync` mediante el uso para devolver una lista de ID de `Team.Id` usuario.

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

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a>Obtenga el perfil de usuario o la lista en el chat personal o grupal

Puede realizar la llamada a la API para cualquier chat personal para obtener la información de perfil del usuario que chatea con su bot.

La llamada a la API, los métodos del SDK y el objeto de respuesta son idénticos a la obtención de la lista de equipos. La única diferencia es que pasas el `conversationId` en lugar del `teamId` .

## <a name="fetch-the-list-of-channels-in-a-team"></a>Obtener la lista de canales en un equipo

El bot puede consultar la lista de canales de un equipo.

> [!NOTE]
>
>* Se devuelve el nombre del canal General predeterminado `null` para permitir la localización.
>* El ID de canal del canal General siempre coincide con el ID de equipo.

### <a name="rest-api-example"></a>Ejemplo de API de REST

Emita directamente una solicitud GET en `/teams/{teamId}/conversations/` , utilizando el valor como punto de `serviceUrl` conexión.

El único origen para `teamId` es un mensaje del contexto del equipo. El mensaje es un mensaje de un usuario o el mensaje que recibe el bot cuando se agrega a un equipo. Para obtener más información, consulte [bot o usuario agregado a un equipo.](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)

> [!NOTE]
> El `serviceUrl` valor tiende a ser estable, pero puede cambiar. Cuando llega un nuevo mensaje, el bot debe comprobar su `serviceUrl` valor almacenado.

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

En el ejemplo siguiente se usa la `FetchChannelList` llamada desde las extensiones de Teams para el SDK de Bot Builder para [.NET:](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a>Node.js ejemplo

En el ejemplo siguiente se utiliza `fetchChannelList` la llamada desde las extensiones de Teams para el SDK de Bot Builder para [Node.js: ](https://www.npmjs.com/package/botbuilder-teams)

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

## <a name="get-clientinfo-in-your-bot-context"></a>Obtenga clientInfo en el contexto del bot

Puede capturar clientInfo dentro de la actividad del bot. ClientInfo contiene las siguientes propiedades:

* Locale
* País
* Plataforma
* Zona horaria

### <a name="json-example"></a>Ejemplo JSON

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

## <a name="see-also"></a>Vea también

[Muestras de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).
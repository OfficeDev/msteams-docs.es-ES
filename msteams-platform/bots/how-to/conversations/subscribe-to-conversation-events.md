---
title: Eventos de conversación
author: WashingtonKayaker
description: Cómo trabajar con eventos de conversación desde el bot de Microsoft Teams, actualizaciones de eventos de canal, eventos de miembros del equipo y eventos de reacción de mensajes con ejemplos de código.
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
keywords: conversación de reacción de mensaje de canal de bot de eventos
ms.openlocfilehash: 8052ec921a0e0e72ea6b64323ec713b84d18d18d
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453449"
---
# <a name="conversation-events-in-your-teams-bot"></a>Eventos de conversación en el bot de Teams

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Al crear los bots de conversación para Microsoft Teams, puede trabajar con eventos de conversación. Teams envía notificaciones al bot para eventos de conversación que se suceden en ámbitos donde el bot está activo. Puede capturar estos eventos en el código y realizar las siguientes acciones:

* Desencadena un mensaje de bienvenida cuando el bot se agrega a un equipo.
* Desencadena un mensaje de bienvenida cuando se agrega o quita un nuevo miembro del equipo.
* Desencadena una notificación cuando se crea, cambia el nombre o elimina un canal.
* Cuando un usuario le gusta un mensaje de bot.

## <a name="conversation-update-events"></a>Eventos de actualización de conversación

Puedes usar eventos de actualización de conversación para proporcionar mejores notificaciones y acciones de bot más eficaces.

> [!IMPORTANT]
>
> * Puedes agregar eventos nuevos en cualquier momento y el bot comienza a recibirlos.
> * Debe diseñar el bot para recibir eventos inesperados.
> * Si usa el SDK de Bot Framework, el bot responde automáticamente con un a a los `200 - OK` eventos que decida no controlar.

Un bot recibe un `conversationUpdate` evento en cualquiera de los siguientes casos:

* Cuando el bot se ha agregado a una conversación.
* Otros miembros se agregan o quitan de una conversación.
* Los metadatos de conversación han cambiado.

El evento `conversationUpdate` se envía al bot cuando recibe información sobre las actualizaciones de suscripción de los equipos donde se ha agregado. También recibe una actualización cuando se ha agregado por primera vez para conversaciones personales.

En la tabla siguiente se muestra una lista de Teams eventos de actualización de conversación con más detalles:

| Acción realizada        | EventType         | Método llamado              | Descripción                | Ámbito |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| Canal creado     | channelCreated    | OnTeamsChannelCreatedAsync | [Se crea un canal](#channel-created). | Equipo |
| Se cambió el nombre del canal     | channelRenamed    | OnTeamsChannelRenamedAsync | [Se cambia el nombre de un canal](#channel-renamed). | Equipo |
| Canal eliminado     | channelDeleted    | OnTeamsChannelDeletedAsync | [Se elimina un canal](#channel-deleted). | Equipo |
| Canal restaurado    | channelRestored    | OnTeamsChannelRestoredAsync | [Se restaura un canal](#channel-deleted). | Equipo |
| Miembros agregados   | membersAdded   | OnTeamsMembersAddedAsync   | [Se agrega un miembro](#team-members-added). | Todo |
| Miembros eliminados | membersRemoved | OnTeamsMembersRemovedAsync | [Se quita un miembro](#team-members-removed). | groupChat y equipo |
| Se cambió el nombre del equipo        | teamRenamed       | OnTeamsTeamRenamedAsync    | [Se cambia el nombre de un equipo](#team-renamed).       | Equipo |
| Equipo eliminado        | teamDeleted       | OnTeamsTeamDeletedAsync    | [Se elimina un equipo](#team-deleted).       | Equipo |
| Equipo archivado        | teamArchived       | OnTeamsTeamArchivedAsync    | [Se archiva un equipo](#team-archived).       | Equipo |
| Equipo desarchivado        | teamUnarchived       | OnTeamsTeamUnarchivedAsync    | [Un equipo no está anárquico](#team-unarchived).       | Equipo |
| Equipo restaurado        | teamRestored      | OnTeamsTeamRestoredAsync    | [Se restaura un equipo](#team-restored)       | Equipo |

### <a name="channel-created"></a>Canal creado

El evento de canal creado se envía al bot cada vez que se crea un nuevo canal en un equipo donde está instalado el bot.

El siguiente código muestra un ejemplo de evento creado por el canal:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

<!-- From sample: botbuilder-js\libraries\botbuilder\tests\teams\conversationUpdate\src\conversationUpdateBot.ts -->

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelCreatedEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Created', `${channelInfo.name} is the Channel created`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:34:07.478Z",
    "localTimestamp": "2017-02-23T12:34:07.478-07:00",
    "id": "f:dd6ec311",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1wR7IdIRIoerMIWbewMi75JA3scaMuxvFon9eRQW2Nix5loMDo0362st2IaRVRirPZBv1WdXT8TIFWWmlQCizZQ"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "channel": {
            "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
            "name": "FunDiscussions"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "channelCreated",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_channel_created(
 self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(
   f"The new channel is {channel_info.name}. The channel id is {channel_info.id}"
  )
 )
```

---

### <a name="channel-renamed"></a>Se cambió el nombre del canal

El evento de cambio de nombre de canal se envía al bot siempre que se cambie el nombre de un canal en un equipo donde esté instalado el bot.

El siguiente código muestra un ejemplo de evento con el nombre de canal:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelRenamedEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Renamed', `${channelInfo.name} is the new Channel name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:34:07.478Z",
    "localTimestamp": "2017-02-23T12:34:07.478-07:00",
    "id": "f:dd6ec311",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1wR7IdIRIoerMIWbewMi75JA3scaMuxvFon9eRQW2Nix5loMDo0362st2IaRVRirPZBv1WdXT8TIFWWmlQCizZQ"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "channel": {
            "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
            "name": "PhotographyUpdates"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "channelRenamed",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_channel_renamed(
 self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(f"The new channel name is {channel_info.name}")
 )
```

---

### <a name="channel-deleted"></a>Canal eliminado

El evento de eliminación de canal se envía al bot, siempre que se elimine un canal en un equipo donde esté instalado el bot.

El siguiente código muestra un ejemplo de evento eliminado del canal:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelDeletedEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Deleted', `${channelInfo.name} is the Channel deleted`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:34:07.478Z",
    "localTimestamp": "2017-02-23T12:34:07.478-07:00",
    "id": "f:dd6ec311",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1wR7IdIRIoerMIWbewMi75JA3scaMuxvFon9eRQW2Nix5loMDo0362st2IaRVRirPZBv1WdXT8TIFWWmlQCizZQ"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "channel": {
            "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
            "name": "PhotographyUpdates"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "channelDeleted",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_channel_deleted(
 self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(f"The deleted channel is {channel_info.name}")
 )
```

---

### <a name="channel-restored"></a>Canal restaurado

El evento restaurado del canal se envía al bot, siempre que se restaure un canal que se eliminó anteriormente en un equipo en el que el bot ya está instalado.

El código siguiente muestra un ejemplo de evento restaurado del canal:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRestoredAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel restored.");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

<!-- From sample: botbuilder-js\libraries\botbuilder\tests\teams\conversationUpdate\src\conversationUpdateBot.ts -->

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelRestoredEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Restored', `${channelInfo.name} is the Channel restored`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:34:07.478Z",
    "localTimestamp": "2017-02-23T12:34:07.478-07:00",
    "id": "f:dd6ec311",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1wR7IdIRIoerMIWbewMi75JA3scaMuxvFon9eRQW2Nix5loMDo0362st2IaRVRirPZBv1WdXT8TIFWWmlQCizZQ"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "channel": {
            "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
            "name": "FunDiscussions"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "channelRestored",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_channel_restored(
 self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(
   f"The restored channel is {channel_info.name}. The channel id is {channel_info.id}"
  )
 )
```

---

### <a name="team-members-added"></a>Miembros del equipo agregados

El `teamMemberAdded` evento se envía al bot la primera vez que se agrega a una conversación. El evento se envía al bot cada vez que se agrega un nuevo usuario a un chat de grupo o equipo donde está instalado el bot. La información del usuario que es id., es única para el bot y puede almacenarse en caché para su uso futuro por el servicio, como enviar un mensaje a un usuario específico.

El código siguiente muestra un ejemplo de evento agregado por los miembros del equipo:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsMembersAddedAsync(IList<TeamsChannelAccount> teamsMembersAdded , TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (TeamsChannelAccount member in teamsMembersAdded)
    {
        if (member.Id == turnContext.Activity.Recipient.Id)
        {
            // Send a message to introduce the bot to the team
            var heroCard = new HeroCard(text: $"The {member.Name} bot has joined {teamInfo.Name}");
            await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
        }
        else
        {
            var heroCard = new HeroCard(text: $"{member.Name} joined {teamInfo.Name}");
            await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
        }
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsMembersAddedEvent(async (membersAdded: ChannelAccount[], teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
                let newMembers: string = '';
                console.log(JSON.stringify(membersAdded));
                membersAdded.forEach((account) => {
                    newMembers += account.id + ' ';
                });
                const name = !teamInfo ? 'not in team' : teamInfo.name;
                const card = CardFactory.heroCard('Account Added', `${newMembers} joined ${name}.`);
                const message = MessageFactory.attachment(card);
                await turnContext.sendActivity(message);
                await next();
        });
    }
}

```

# <a name="json"></a>[JSON](#tab/json)

Este es el mensaje que el bot recibe cuando se agrega el bot a un equipo.

```json
{
    "membersAdded": [
        {
            "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
        }
    ],
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:38:35.312Z",
    "localTimestamp": "2017-02-23T12:38:35.312-07:00",
    "id": "f:5f85c2ad",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "teamMemberAdded",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

Este es el mensaje que el bot recibe cuando se agrega el bot a un chat uno a uno.

```json
{
  "membersAdded": [{
      "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
    },
    {
      "id": "29:<userID>",
      "aadObjectId": "***"
    }
  ],
  "type": "conversationUpdate",
  "timestamp": "2019-04-23T10:17:44.349Z",
  "id": "f:5f85c2ad",
  "channelId": "msteams",
  "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
  "from": {
    "id": "29:<USERID>",
    "aadObjectId": "***"
  },
  "conversation": {
    "conversationType": "personal",
    "id": "***"
  },
  "recipient": {
    "id": "28:<BOT ID>",
    "name": "<BOT NAME>"
  },
  "channelData": {
    "tenant": {
      "id": "<TENANT ID>"
    }
  }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_members_added(
 self, teams_members_added: [TeamsChannelAccount], turn_context: TurnContext
):
 for member in teams_members_added:
  await turn_context.send_activity(
   MessageFactory.text(f"Welcome your new team member {member.id}")
  )
 return
```

---

### <a name="team-members-removed"></a>Miembros del equipo eliminados

El `teamMemberRemoved` evento se envía al bot si se quita de un equipo. El evento se envía al bot cada vez que se quita cualquier usuario de un equipo en el que el bot es miembro. Para determinar si el nuevo miembro quitado era el propio bot o un usuario, compruebe el `Activity` objeto de `turnContext`.  Si el `Id` campo del `MembersRemoved` objeto es el `Id` `Recipient` mismo que el campo del objeto, el miembro quitado es el bot, de lo contrario es un usuario. Por lo general, el bot `Id` es `28:<MicrosoftAppId>`.

> [!NOTE]
> Cuando un usuario se elimina permanentemente de un inquilino, se `membersRemoved conversationUpdate` desencadena el evento.

El código siguiente muestra un ejemplo de evento de miembros del equipo eliminados:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsMembersRemovedAsync(IList<ChannelAccount> membersRemoved, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (TeamsChannelAccount member in membersRemoved)
    {
        if (member.Id == turnContext.Activity.Recipient.Id)
        {
            // The bot was removed
            // You should clear any cached data you have for this team
        }
        else
        {
            var heroCard = new HeroCard(text: $"{member.Name} was removed from {teamInfo.Name}");
            await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
        }
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsMembersRemovedEvent(async (membersRemoved: ChannelAccount[], teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            let removedMembers: string = '';
            console.log(JSON.stringify(membersRemoved));
            membersRemoved.forEach((account) => {
                removedMembers += account.id + ' ';
            });
            const name = !teamInfo ? 'not in team' : teamInfo.name;
            const card = CardFactory.heroCard('Account Removed', `${removedMembers} removed from ${teamInfo.name}.`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[JSON](#tab/json)

El `channelData` objeto del siguiente ejemplo de carga se basa en agregar un miembro a un equipo en lugar de un chat de grupo o iniciar una nueva conversación uno a uno:

```json
{
    "membersRemoved": [
        {
            "id": "29:1_LCi5Up14pAy65yZuaJzG1uIT7ujYhjjSTsUNqjORsZHjLHKiQIBJa4cX2XsAsRoaY7va2w6ZymA9-1VtSY_g"
        }
    ],
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:37:06.96Z",
    "localTimestamp": "2017-02-23T12:37:06.96-07:00",
    "id": "f:d8a6a4aa",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient":
    {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "teamMemberRemoved",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```


# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_members_removed(
 self, teams_members_removed: [TeamsChannelAccount], turn_context: TurnContext
):
 for member in teams_members_removed:
  await turn_context.send_activity(
   MessageFactory.text(f"Say goodbye to {member.id}")
  )
 return
```

---

### <a name="team-renamed"></a>Se cambió el nombre del equipo

El bot se notifica cuando se cambia el nombre del equipo. Recibe un evento `conversationUpdate` con `eventType.teamRenamed` en el `channelData` objeto.

El siguiente código muestra un ejemplo de evento con el nombre de equipo:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamRenamedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team Renamed', `${teamInfo.name} is the new Team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{ 
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:35:56.825Z",
    "localTimestamp": "2017-02-23T12:35:56.825-07:00",
    "id": "f:1406033e",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/", 
    "from": { 
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    }, 
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": { 
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype",
            "name": "New Team Name"
        },
        "eventType": "teamRenamed",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_team_renamed(
 self, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(f"The new team name is {team_info.name}")
 )
```

---

### <a name="team-deleted"></a>Equipo eliminado

El bot se notifica cuando se elimina el equipo. Recibe un evento `conversationUpdate` con `eventType.teamDeleted` en el `channelData` objeto.

El código siguiente muestra un ejemplo de evento eliminado por el equipo:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamDeletedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    //handle delete event
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamDeletedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            //handle delete event
            await next();
        });
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{ 
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:35:56.825Z",
    "localTimestamp": "2017-02-23T12:35:56.825-07:00",
    "id": "f:1406033e",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/", 
    "from": { 
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    }, 
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": { 
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype",
            "name": "Team Name"
        },
        "eventType": "teamDeleted",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_team_deleted(
 self, team_info: TeamInfo, turn_context: TurnContext
):
 //handle delete event
 )
```

---

### <a name="team-restored"></a>Equipo restaurado

El bot recibe una notificación cuando se restaura un equipo después de eliminarse. Recibe un evento `conversationUpdate` con `eventType.teamrestored` en el `channelData` objeto.

El código siguiente muestra un ejemplo de evento restaurado por el equipo:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamrestoredAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamrestoredEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team restored', `${teamInfo.name} is the team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{ 
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:35:56.825Z",
    "localTimestamp": "2017-02-23T12:35:56.825-07:00",
    "id": "f:1406033e",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/", 
    "from": { 
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    }, 
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": { 
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype",
            "name": "Team Name"
        },
        "eventType": "teamrestored",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_team_restored(
 self, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(f"The team name is {team_info.name}")
 )
```

---

### <a name="team-archived"></a>Equipo archivado

El bot recibe una notificación cuando el equipo está instalado y archivado. Recibe un evento `conversationUpdate` con `eventType.teamarchived` en el `channelData` objeto.

El siguiente código muestra un ejemplo de evento archivado por el equipo:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamArchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamArchivedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team archived', `${teamInfo.name} is the team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{ 
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:35:56.825Z",
    "localTimestamp": "2017-02-23T12:35:56.825-07:00",
    "id": "f:1406033e",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/", 
    "from": { 
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    }, 
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": { 
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype",
            "name": "Team Name"
        },
        "eventType": "teamArchived",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_team_archived(
 self, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(f"The team name is {team_info.name}")
 )
```

---

### <a name="team-unarchived"></a>Equipo desarchivado

El bot recibe una notificación cuando el equipo está instalado y sin jerarquía. Recibe un evento `conversationUpdate` con `eventType.teamUnarchived` en el `channelData` objeto.

En el código siguiente se muestra un ejemplo de evento de equipo no anárquico:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamUnarchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamUnarchivedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team archived', `${teamInfo.name} is the team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{ 
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:35:56.825Z",
    "localTimestamp": "2017-02-23T12:35:56.825-07:00",
    "id": "f:1406033e",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/", 
    "from": { 
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    }, 
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": { 
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype",
            "name": "Team Name"
        },
        "eventType": "teamUnarchived",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_team_unarchived(
 self, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(f"The team name is {team_info.name}")
 )
```

---

Ahora que ha trabajado con los eventos de actualización de conversación, puede comprender los eventos de reacción de mensajes que se producen para diferentes reacciones a un mensaje.

## <a name="message-reaction-events"></a>Eventos de reacción de mensajes

El `messageReaction` evento se envía cuando un usuario agrega o quita las reacciones a un mensaje enviado por el bot. Contiene `replyToId` el identificador del mensaje y es `Type` el tipo de reacción en formato de texto. Los tipos de reacciones incluyen el enojo, el corazón, la carcajada, como, la tristeza y la sorpresa. Este evento no contiene el contenido del mensaje original. Si el procesamiento de las reacciones a los mensajes es importante para el bot, debe almacenar los mensajes al enviarlos. En la tabla siguiente se proporciona más información sobre el tipo de evento y los objetos de carga:

| EventType       | Payload (objeto)   | Descripción                                                             | Ámbito |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| messageReaction | reactionsAdded   | [Reacciones agregadas al mensaje del bot](#reactions-added-to-bot-message).           | Todo   |
| messageReaction | reactionsRemoved | [Reacciones eliminadas del mensaje de bot](#reactions-removed-from-bot-message). | Todo |

### <a name="reactions-added-to-bot-message"></a>Reacciones agregadas al mensaje de bot

El código siguiente muestra un ejemplo de las reacciones a un mensaje de bot:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnReactionsAddedAsync(IList<MessageReaction> messageReactions, ITurnContext<IMessageReactionActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (var reaction in messageReactions)
    {
      var newReaction = $"You reacted with '{reaction.Type}' to the following message: '{turnContext.Activity.ReplyToId}'";
      var replyActivity = MessageFactory.Text(newReaction);
      var resourceResponse = await turnContext.SendActivityAsync(replyActivity, cancellationToken);
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

<!-- Verify -->

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onReactionsAdded(async (context, next) => {
           const reactionsAdded = context.activity.reactionsAdded;
            if (reactionsAdded && reactionsAdded.length > 0) {
                for (let i = 0; i < reactionsAdded.length; i++) {
                    const reaction = reactionsAdded[i];
                    const newReaction = `You reacted with '${reaction.type}' to the following message: '${context.activity.replyToId}'`;
                    const resourceResponse = context.sendActivity(newReaction);
                    // Save information about the sent message and its ID (resourceResponse.id).
                }
            }
        });
    }
}

```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "reactionsAdded": [
        {
            "type": "like"
        }
    ],
    "type": "messageReaction",
    "timestamp": "2017-10-16T18:45:41.943Z",
    "id": "f:9f78d1f3",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA",
        "aadObjectId": "c33aafc4-646d-4543-9d4c-abd28e4d2110"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "channel": {
            "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184",
    "legacy": {
      "replyToId": "1:19uJ8TZA1cZcms7-2HLOW3pWRF4nSWEoVnRqc0DPa_kY"
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_reactions_added(
 self, message_reactions: List[MessageReaction], turn_context: TurnContext
):
 for reaction in message_reactions:
  activity = await self._log.find(turn_context.activity.reply_to_id)
  if not activity:
   await self._send_message_and_log_activity_id(
    turn_context,
    f"Activity {turn_context.activity.reply_to_id} not found in log",
   )
  else:
   await self._send_message_and_log_activity_id(
    turn_context,
    f"You added '{reaction.type}' regarding '{activity.text}'",
   )
 return
```

---

### <a name="reactions-removed-from-bot-message"></a>Reacciones eliminadas del mensaje de bot

El siguiente código muestra un ejemplo de las reacciones eliminadas del mensaje del bot:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnReactionsRemovedAsync(IList<MessageReaction> messageReactions, ITurnContext<IMessageReactionActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (var reaction in messageReactions)
    {
      var newReaction = $"You removed the reaction '{reaction.Type}' from the following message: '{turnContext.Activity.ReplyToId}'";
      var replyActivity = MessageFactory.Text(newReaction);
      var resourceResponse = await turnContext.SendActivityAsync(replyActivity, cancellationToken);
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

<!-- Verify -->

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onReactionsRemoved(async(context,next)=>{
            const reactionsRemoved = context.activity.reactionsRemoved;
            if (reactionsRemoved && reactionsRemoved.length > 0) {
                for (let i = 0; i < reactionsRemoved.length; i++) {
                    const reaction = reactionsRemoved[i];
                    const newReaction = `You removed the reaction '${reaction.type}' from the message: '${context.activity.replyToId}'`;
                    const resourceResponse = context.sendActivity(newReaction);
                    // Save information about the sent message and its ID (resourceResponse.id).
                }
            }
        });
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "reactionsRemoved": [
        {
            "type": "like"
        }
    ],
    "type": "messageReaction",
    "timestamp": "2017-10-16T18:45:41.943Z",
    "id": "f:9f78d1f3",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA",
        "aadObjectId": "c33aafc4-646d-4543-9d4c-abd28e4d2110"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "channel": {
            "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184",
    "legacy": {
      "replyToId": "1:19uJ8TZA1cZcms7-2HLOW3pWRF4nSWEoVnRqc0DPa_kY"
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_reactions_removed(
 self, message_reactions: List[MessageReaction], turn_context: TurnContext
):
 for reaction in message_reactions:
  activity = await self._log.find(turn_context.activity.reply_to_id)
  if not activity:
   await self._send_message_and_log_activity_id(
    turn_context,
    f"Activity {turn_context.activity.reply_to_id} not found in log",
   )
  else:
   await self._send_message_and_log_activity_id(
    turn_context,
    f"You removed '{reaction.type}' regarding '{activity.text}'",
   )
 return
```

---

## <a name="installation-update-event"></a>Evento de actualización de instalación

El bot recibe un evento `installationUpdate` al instalar un bot en un subproceso de conversación. La desinstalación del bot del subproceso también desencadena el evento. Al instalar un bot, el **campo de** acción del evento se establece en *agregar* y, cuando se desinstala el bot, el campo **de** acción se establece para *quitar*.

> [!NOTE]
> Al actualizar una aplicación y, a continuación, agregar o quitar un bot, la acción también desencadena el `installationUpdate` evento. El **campo** de acción se establece en *add-upgrade* si agrega un bot o *remove-upgrade* si quita un bot.

### <a name="install-update-event"></a>Evento Install update

Use el `installationUpdate` evento para enviar un mensaje introductorio desde el bot durante la instalación. Este evento le ayuda a cumplir los requisitos de privacidad y retención de datos. También puede limpiar y eliminar datos de usuario o subproceso cuando se desinstala el bot.

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task
OnInstallationUpdateActivityAsync(ITurnContext<IInstallationUpdateActivity> turnContext, CancellationToken cancellationToken) {
var activity = turnContext.Activity; if
(string.Equals(activity.Action, "Add",
StringComparison.InvariantCultureIgnoreCase)) {
// TO:DO Installation workflow }
else
{ // TO:DO Uninstallation workflow
} return; }
```

También puede usar un controlador dedicado para *agregar* *o quitar* escenarios como método alternativo para capturar un evento.

```csharp
protected override async Task
OnInstallationUpdateAddAsync(ITurnContext<IInstallationUpdateActivity>
turnContext, CancellationToken cancellationToken) {
// TO:DO Installation workflow return;
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
async onInstallationUpdateActivity(context: TurnContext) {
        var activity = context.activity.action;
        if(activity == "Add") {
            await context.sendActivity(MessageFactory.text("Added"));
        }
        else {
            await context.sendActivity(MessageFactory.text("Uninstalled"));
        }
    }
```

# <a name="json"></a>[JSON](#tab/json)

```json
{ 
  "action": "add", 
  "type": "installationUpdate", 
  "timestamp": "2020-10-20T22:08:07.869Z", 
  "id": "f:3033745319439849398", 
  "channelId": "msteams", 
  "serviceUrl": "https://smba.trafficmanager.net/amer/", 
  "from": { 
    "id": "sample id", 
    "aadObjectId": "sample Azure AD Object ID" 
  },
  "conversation": { 
    "isGroup": true, 
    "conversationType": "channel", 
    "tenantId": "sample tenant ID", 
    "id": "sample conversation Id@thread.skype" 
  }, 

  "recipient": { 
    "id": "sample reciepent bot ID", 
    "name": "bot name" 
  }, 
  "entities": [ 
    { 
      "locale": "en", 
      "platform": "Windows", 
      "type": "clientInfo" 
    } 
  ], 
  "channelData": { 
    "settings": { 
      "selectedChannel": { 
        "id": "sample channel ID@thread.skype" 
      } 
    }, 
    "channel": { 
      "id": "sample channel ID" 
    }, 
    "team": { 
      "id": "sample team ID" 
    }, 
    "tenant": { 
      "id": "sample tenant ID" 
    }, 
    "source": { 
      "name": "message" 
    } 
  }, 
  "locale": "en" 
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_installation_update(self, turn_context: TurnContext):
   if turn_context.activity.action == "add":   
       await turn_context.send_activity(MessageFactory.text("Added"))
   else:
       await turn_context.send_activity(MessageFactory.text("Uninstalled"))
```

---

## <a name="uninstall-behavior-for-personal-app-with-bot"></a>Comportamiento de desinstalación de la aplicación personal con bot

> [!NOTE]
> El comportamiento de desinstalación de la aplicación personal con bot está disponible actualmente solo en [la versión preliminar del desarrollador público](../../../resources/dev-preview/developer-preview-intro.md).

Al desinstalar una aplicación, el bot también se desinstala. Cuando un usuario envía un mensaje a la aplicación, recibe un código de respuesta 403. El bot recibe un código de respuesta 403 para los nuevos mensajes publicados por el bot. El comportamiento posterior a la desinstalación de bots en el ámbito personal con los ámbitos Teams y groupChat ahora están alineados. No puedes enviar ni recibir mensajes después de desinstalar una aplicación.

<img src="~/assets/images/bots/uninstallbot.png" alt="Uninstall event" width="900" height="900"/>

## <a name="event-handling-for-install-and-uninstall-events"></a>Control de eventos para eventos de instalación y desinstalación

Al usar estos eventos de instalación y desinstalación, hay algunas instancias en las que los bots dan excepciones al recibir eventos inesperados de Teams. Esto ocurre en los siguientes casos:

* Creas el bot sin el SDK Microsoft Bot Framework y, como resultado, el bot proporciona una excepción al recibir un evento inesperado.
* Creas el bot con el SDK de Microsoft Bot Framework y seleccionas modificar el comportamiento de evento predeterminado invalidando el identificador de evento base.

Es importante saber que los nuevos eventos se pueden agregar en cualquier momento en el futuro y el bot comienza a recibirlos. Por lo tanto, debe diseñar la posibilidad de recibir eventos inesperados. Si usa el SDK de Bot Framework, el bot responde automáticamente con un 200: aceptar cualquier evento que no elija controlar.

## <a name="code-sample"></a>Ejemplo de código

| **Ejemplo de nombre** | **Descripción** | **.NET** | **Node.js** | **Python** |
|----------|-----------------|----------|
| Bot de conversación | Código de ejemplo para eventos de conversación de bots. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)  | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [Ver](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Enviar mensajes proactivos](~/bots/how-to/conversations/send-proactive-messages.md)

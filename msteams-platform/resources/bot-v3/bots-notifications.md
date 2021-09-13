---
title: Controlar eventos de bot
description: Describe cómo controlar eventos en bots para Microsoft Teams
keywords: eventos de bots de teams
ms.date: 05/20/2019
ms.topic: how-to
ms.localizationpriority: medium
ms.author: lajanuar
author: surbhigupta
ms.openlocfilehash: 6189460e16459e737656f68945f1b0a2a3549834
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157501"
---
# <a name="handle-bot-events-in-microsoft-teams"></a>Controlar eventos de bot en Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams envía notificaciones al bot para los cambios o eventos que ocurren en ámbitos donde el bot está activo. Puede usar estos eventos para desencadenar la lógica de servicio, como la siguiente:

* Desencadena un mensaje de bienvenida cuando el bot se agrega a un equipo.
* Consultar y almacenar en caché la información de grupo cuando el bot se agrega a un chat de grupo.
* Actualice la información almacenada en caché sobre la pertenencia al equipo o la información del canal.
* Quite la información almacenada en caché de un equipo si se quita el bot.
* Cuando un usuario le gusta un mensaje de bot.

Cada evento bot se envía como `Activity` un objeto en el que se define qué información hay en el `messageType` objeto. Para obtener mensajes de `message` tipo , vea Sending and receiving [messages](~/resources/bot-v3/bot-conversations/bots-conversations.md).

Teams eventos de grupo, normalmente desencadenados fuera del tipo, tienen información de evento Teams adicional pasada como parte del objeto y, por lo tanto, el controlador de eventos debe consultar la carga de los metadatos Teams y específicos de eventos `conversationUpdate` `channelData` `channelData` `eventType` adicionales.

En la tabla siguiente se enumeran los eventos en los que el bot puede recibir y realizar acciones.

|Tipo|Payload (objeto)|Teams eventType |Descripción|Ámbito|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[Miembro agregado al equipo](#team-member-or-bot-addition)| all |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[Miembro se quitó del equipo](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [Se cambió el nombre del equipo](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [Se creó un canal](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [Se cambió el nombre de un canal](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [Se eliminó un canal](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [Reacción al mensaje del bot](#reactions)| all |
| `messageReaction` |`reactionsRemoved`|| [Reacción eliminada del mensaje del bot](#reactions)| all |

## <a name="team-member-or-bot-addition"></a>Adición de un miembro del equipo o bot

El evento se envía al bot cuando recibe información sobre las actualizaciones de pertenencia de los equipos en los que [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true) se ha agregado. También recibe una actualización cuando se ha agregado por primera vez, específicamente para conversaciones personales. Tenga en cuenta que la información del usuario ( ) es única para el bot y puede almacenarse en caché para su uso futuro por parte del servicio, como enviar un mensaje `Id` a un usuario específico.

### <a name="bot-or-user-added-to-a-team"></a>Bot o usuario agregado a un equipo

El evento con el objeto en la carga se envía cuando se agrega un bot a un equipo o se agrega un nuevo usuario a un equipo en el que se ha `conversationUpdate` `membersAdded` agregado un bot. Microsoft Teams agrega también `eventType.teamMemberAdded` en el `channelData` objeto.

Dado que este evento se envía en ambos casos, debe analizar el objeto para determinar si la adición era `membersAdded` un usuario o el propio bot. Para este último, un procedimiento recomendado es enviar [un](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) mensaje de bienvenida al canal para que los usuarios puedan comprender las características que proporciona el bot.

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a>Código de ejemplo: comprobar si el bot era el miembro agregado

##### <a name="net"></a>.NET

```csharp
    for (int i = 0; i < sourceMessage.MembersAdded.Count; i++)
    {
        if (sourceMessage.MembersAdded[i].Id == sourceMessage.Recipient.Id)
        {
            addedBot = true;
            break;
        }
    }
```

##### <a name="nodejs"></a>Node.js

```javascript
const builder = require('botbuilder');

var c = new builder.ChatConnector({appId: BOT_APP_ID, appPassword: .BOT_SECRET});
var bot = new builder.UniversalBot(c);

bot.on('conversationUpdate', (msg) => {
    var members = msg.membersAdded;
    // Loop through all members that were just added to the team
    for (var i = 0; i < members.length; i++) {

        // See if the member added was our bot
        if (members[i].id.includes(BOT_APP_ID)) {
            var botmessage = new builder.Message()
                .address(msg.address)
                .text('Hello World!');

            bot.send(botmessage, function(err) {});
        }
    }
});
```

#### <a name="schema-example-bot-added-to-team"></a>Ejemplo de esquema: Bot agregado al equipo

```json
{
   "membersAdded":[
      {
         "id":"28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
      }
   ],
   "type":"conversationUpdate",
   "timestamp":"2017-02-23T19:38:35.312Z",
   "localTimestamp":"2017-02-23T12:38:35.312-07:00",
   "id":"f:5f85c2ad",
   "channelId":"msteams",
   "serviceUrl":"https://smba.trafficmanager.net/amer-client-ss.msg/",
   "from":{
      "id":"29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
   },
   "conversation":{
      "isGroup":true,
      "conversationType":"channel",
      "id":"19:efa9296d959346209fea44151c742e73@thread.skype"
   },
   "recipient":{
      "id":"28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
      "name":"SongsuggesterBot"
   },
   "channelData":{
      "team":{
         "id":"19:efa9296d959346209fea44151c742e73@thread.skype"
      },
      "eventType":"teamMemberAdded",
      "tenant":{
         "id":"72f988bf-86f1-41af-91ab-2d7cd011db47"
      }
   }
}
```

### <a name="user-added-to-a-meeting"></a>Usuario agregado a una reunión

El evento con el objeto en la carga se envía cuando se agrega un usuario `conversationUpdate` a una reunión programada `membersAdded` privada. Los detalles del evento se enviarán incluso cuando los usuarios anónimos se unan a la reunión. 

> [!NOTE]
>
>* Cuando se agrega un usuario anónimo a una reunión, membersAdded payload object no tiene `aadObjectId` campo.
>* Cuando se agrega un usuario anónimo a una reunión, el objeto de la carga siempre tiene el identificador del organizador de la reunión, incluso si otro moderador agregó `from` el usuario anónimo.

#### <a name="schema-example-user-added-to-meeting"></a>Ejemplo de esquema: Usuario agregado a reunión

```json
{
   "membersAdded":[
      {
         "id":"229:1Z_XHWBMhDuehhDBYoPQD6Y1DSFsTtqOZx-SA5Jh9Y4zHKm4VbFGRn7-rK7SWiW1JECwxkMdrWpHoBut2sSyQPA"
      }
   ],
   "type":"conversationUpdate",
   "timestamp":"2017-02-23T19:38:35.312Z",
   "localTimestamp":"2020-09-29T21:11:38.6542339Z",
   "id":"f:a8cd1b51-9ddb-bd35-624b-7f7474165df8",
   "channelId":"msteams",
   "serviceUrl":"https://canary.botapi.skype.com/amer/",
   "from":{
      "id":"29:1siKxZhSoTapsXvI0gyf7Gywm_HM-4kEQW4BJnWuFYVIVu87xCNP99nidgQRCcwD3L3p_schiMShzx8IDRzf8mw",
      "aadObjectId":"f30ba569-abef-4e97-8762-35f85cbae706"
   },
   "conversation":{
      "isGroup":true,
      "tenantId":"e15762ef-a8d8-416b-871c-25516354f1fe",
      "id":"19:meeting_MWJlNGViOTgtMGExYi00NDA3LWExODgtOTZhMWNlYjM4ZTRj@thread.v2"
   },
   "recipient":{
      "id":"28:3af3604a-d4fc-486b-911e-86fab41aa91c",
      "name":"EchoBot1_Rename"
   },
   "channelData":{
      "tenant":{
         "id":"e15762ef-a8d8-416b-871c-25516354f1fe"
      },
      "source":null,
      "meeting":{
         "id":"MCMxOTptZWV0aW5nX01XSmxOR1ZpT1RndE1HRXhZaTAwTkRBM0xXRXhPRGd0T1RaaE1XTmxZak00WlRSakB0aHJlYWQudjIjMA=="
      }
   }
}

```

### <a name="bot-added-for-personal-context-only"></a>Bot agregado solo para contexto personal

El bot recibe un `conversationUpdate` con cuando un usuario lo agrega directamente para chat `membersAdded` personal. En este caso, la carga que recibe el bot no contiene el `channelData.team` objeto. Debes usarlo como filtro en caso de que quieras que el bot ofrezca un mensaje de [bienvenida diferente](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) en función del ámbito.

> [!NOTE]
> Para los bots con ámbito personal, el bot recibirá el evento varias veces, incluso si el `conversationUpdate` bot se quita y se vuelve a agregar. Para el desarrollo y las pruebas puede resultar útil agregar una función auxiliar que te permita restablecer el bot completamente. Vea un [Node.js ejemplo o](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) C# ejemplo [para](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) obtener más información sobre cómo implementar esto.

#### <a name="schema-example-bot-added-to-personal-context"></a>Ejemplo de esquema: bot agregado al contexto personal

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

## <a name="team-member-or-bot-removed"></a>Miembro del equipo o bot quitado

El evento con el objeto en la carga se envía cuando se quita el bot de un equipo o se quita un usuario de un equipo en el que `conversationUpdate` se ha agregado un `membersRemoved` bot. Microsoft Teams agrega también `eventType.teamMemberRemoved` en el `channelData` objeto. Al igual que con el objeto, debe analizar el objeto del identificador de aplicación del `membersAdded` bot para determinar quién se `membersRemoved` quitó.

### <a name="schema-example-team-member-removed"></a>Ejemplo de esquema: Miembro del equipo quitado

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

### <a name="user-removed-from-a-meeting"></a>Usuario quitado de una reunión

El evento con el objeto en la carga se envía cuando se quita `conversationUpdate` un usuario de una reunión programada `membersRemoved` privada. Los detalles del evento se enviarán incluso cuando los usuarios anónimos se unan a la reunión. 

> [!NOTE]
>
>* Cuando se quita un usuario anónimo de una reunión, el objeto de carga membersRemoved no tiene `aadObjectId` campo.
>* Cuando se quita un usuario anónimo de una reunión, el objeto de la carga siempre tiene el identificador del organizador de la reunión, incluso si otro moderador quitó `from` el usuario anónimo.

#### <a name="schema-example-user-removed-from-meeting"></a>Ejemplo de esquema: Usuario quitado de reunión

```
{   
      "membersRemoved": 
        {  
          "id": "29:1Z_XHWBMhDuehhDBYoPQD6Y1DSFsTtqOZx-SA5Jh9Y4zHKm4VbFGRn7-rK7SWiW1JECwxkMdrWpHoBut2sSyQPA"   
        }   
      ],   
      "type": "conversationUpdate",   
      "timestamp": "2020-09-29T21:15:08.6391139Z",   
      "id": "f:ee8dfdf3-54ac-51de-05da-9d49514974bb",   
      "channelId": "msteams",   
      "serviceUrl": "https://canary.botapi.skype.com/amer/",   
      "from": {   
        "id": "29:1siKxZhSoTapsXvI0gyf7Gywm_HM-4kEQW4BJnWuFYVIVu87xCNP99nidgQRCcwD3L3p_schiMShzx8IDRzf8mw",   
        "aadObjectId": "f30ba569-abef-4e97-8762-35f85cbae706"   
      },   
      "conversation": {    
        "isGroup": true,   
        "tenantId": "e15762ef-a8d8-416b-871c-25516354f1fe",   
        "id": "19:meeting_MWJlNGViOTgtMGExYi00NDA3LWExODgtOTZhMWNlYjM4ZTRj@thread.v2"   
      },   
      "recipient": {   
        "id": "28:3af3604a-d4fc-486b-911e-86fab41aa91c",   
        "name": "EchoBot1_Rename"   
      },   
      "channelData": {   
        "tenant": {   
          "id": "e15762ef-a8d8-416b-871c-25516354f1fe"   
        },   
        "source": null,   
        "meeting": {   
          "id": "MCMxOTptZWV0aW5nX01XSmxOR1ZpT1RndE1HRXhZaTAwTkRBM0xXRXhPRGd0T1RaaE1XTmxZak00WlRSakB0aHJlYWQudjIjMA=="   
        }   
      }   
}
```

## <a name="team-name-updates"></a>Actualizaciones de nombres de equipo

> [!NOTE]
> No hay ninguna funcionalidad para consultar todos los nombres de equipo y el nombre del equipo no se devuelve en cargas de otros eventos.

El bot recibe una notificación cuando se ha cambiado el nombre del equipo en el que está. Recibe un `conversationUpdate` evento con en el `eventType.teamRenamed` `channelData` objeto. Tenga en cuenta que no hay notificaciones para la creación o eliminación de equipos, ya que los bots solo existen como parte de los equipos y no tienen visibilidad fuera del ámbito en el que se han agregado.

### <a name="schema-example-team-renamed"></a>Ejemplo de esquema: Cambio de nombre del equipo

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

## <a name="channel-updates"></a>Actualizaciones de canales

El bot recibe una notificación cuando se crea, cambia el nombre o elimina un canal en un equipo en el que se ha agregado. De nuevo, se recibe el evento y se envía un identificador de evento específico de Teams como parte del objeto, donde los datos del canal son el GUID del canal y contiene el propio nombre del `conversationUpdate` `channelData.eventType` `channel.id` `channel.name` canal.

Los eventos de canal son los siguientes:

* **channelCreated** &emsp; Un usuario agrega un nuevo canal al equipo.
* **channelRenamed** &emsp; Un usuario cambia el nombre de un canal existente.
* **channelDeleted** &emsp; Un usuario quita un canal.

### <a name="full-schema-example-channelcreated"></a>Ejemplo de esquema completo: channelCreated

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

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a>Extracto de esquema: channelData para channelRenamed

```json
⋮
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
⋮
```

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a>Extracto de esquema: channelData para channelDeleted

```json
⋮
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
⋮
```

## <a name="reactions"></a>Reacciones

El evento se envía cuando un usuario agrega o quita su reacción a un mensaje enviado `messageReaction` originalmente por el bot. `replyToId` contiene el identificador del mensaje específico.

### <a name="schema-example-a-user-likes-a-message"></a>Ejemplo de esquema: a un usuario le gusta un mensaje

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
    "replyToId": "1575667808184"
}
```

### <a name="schema-example-a-user-un-likes-a-message"></a>Ejemplo de esquema: un usuario no le gusta un mensaje

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
    "replyToId": "1575667808184"
}
```

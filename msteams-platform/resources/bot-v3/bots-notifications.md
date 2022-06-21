---
title: Control de eventos de bot
description: En este módulo, aprenderá a controlar eventos en bots para Microsoft Teams, Teams miembro o adición del bot, miembro del equipo o bot eliminado, etc.
ms.date: 05/20/2019
ms.topic: how-to
ms.localizationpriority: medium
ms.author: lajanuar
author: surbhigupta
ms.openlocfilehash: 95d6439d396a61471c0e7dbe5942d4b88cc00a87
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189316"
---
# <a name="handle-bot-events-in-microsoft-teams"></a>Control de eventos de bot en Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams envía notificaciones al bot para los cambos o eventos que se suceden en ámbitos donde el bot está activo. Puede usar estos eventos para desencadenar la lógica de servicio, como la siguiente:

* Desencadenar un mensaje de bienvenida cuando se añade el bot a un equipo;
* Consultar y almacenar en caché la información del grupo cuando se agrega el bot a un chat grupal.
* Actualizar la información almacenada en caché sobre la pertenencia al equipo o la información del canal.
* Quitar la información almacenada en caché de un equipo si se quita el bot.
* Cuando a un usuario le gusta un mensaje de bot.

Cada evento de bot se envía como un objeto `Activity` en el que `messageType` define qué información hay en el objeto. Para los mensajes de tipo `message`, vea [Enviar y recibir mensajes](~/resources/bot-v3/bot-conversations/bots-conversations.md).

Teams y los eventos de grupo, desencadenados fuera del `conversationUpdate` tipo, tienen más Teams información de eventos pasada como parte del objeto y, por lo tanto, el `channelData` controlador de eventos debe consultar la `channelData` carga de la Teams `eventType` y metadatos más específicos del evento.

En la tabla siguiente se enumeran los eventos en los que el bot puede recibir y ejecutar acciones.

|Tipo|Objeto de carga|Teams eventType |Descripción|Ámbito|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[Miembro agregado al equipo](#team-member-or-bot-addition)| todo |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[Miembro quitado del equipo](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [Se cambió el nombre del equipo](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [Se creó un canal](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [Se cambió el nombre de un canal](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [Se eliminó un canal](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [Reacción al mensaje del bot](#reactions)| todo |
| `messageReaction` |`reactionsRemoved`|| [Reacción eliminada del mensaje del bot](#reactions)| todo |

## <a name="team-member-or-bot-addition"></a>Adición de miembro del equipo o bot

El evento [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true) se envía al bot cuando recibe información sobre las actualizaciones de suscripción de los equipos donde se ha agregado. También recibe una actualización cuando se ha agregado por primera vez, específicamente para conversaciones personales. La información de usuario (`Id`) es única para el bot y puede almacenarse en caché para su uso futuro por el servicio, como, por ejemplo, enviar un mensaje a un usuario específico.

### <a name="bot-or-user-added-to-a-team"></a>Bot o usuario agregado a un equipo

El evento `conversationUpdate` con el objeto `membersAdded` en la carga se envía cuando se agrega un bot a un equipo o se agrega un nuevo usuario a un equipo donde se ha agregado un bot. Teams también agrega `eventType.teamMemberAdded` en el `channelData` objeto .

Dado que este evento se envía en ambos casos, debe analizar el objeto `membersAdded` para determinar si la adición fue un usuario o el propio bot. Para lo último, un procedimiento recomendado es enviar un [mensaje de bienvenida](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) al canal para que los usuarios puedan comprender las características que proporciona el bot.

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a>Código de ejemplo: comprobando si el bot era el miembro agregado

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

#### <a name="schema-example-bot-added-to-team"></a>Ejemplo de esquema: bot agregado al equipo

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

El evento `conversationUpdate` con el objeto `membersAdded` de la carga se envía cuando se agrega un usuario a una reunión programada privada. Los detalles del evento se enviarán incluso cuando los usuarios anónimos se unan a la reunión.

> [!NOTE]
>
>* Cuando se agrega un usuario anónimo a una reunión, el objeto de carga membersAdded no tiene el campo `aadObjectId`.
>* Cuando se agrega un usuario anónimo a una reunión, el objeto `from` de la carga siempre tiene el identificador del organizador de la reunión, incluso si otro moderador agregó el usuario anónimo.

#### <a name="schema-example-user-added-to-meeting"></a>Ejemplo de esquema: usuario agregado a la reunión

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

El bot recibe un `conversationUpdate` con `membersAdded` cuando un usuario lo agrega directamente para el chat personal. En este caso, la carga que recibe el bot no contiene el objeto `channelData.team`. Debe usarlo como filtro en caso de que quiera que el bot ofrezca un [mensaje de bienvenida](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) diferente en función del ámbito.

> [!NOTE]
> En el caso de los bots con ámbito personal, el bot recibirá el evento de `conversationUpdate` varias veces, incluso si el bot se quita y se vuelve a agregar. Para el desarrollo y las pruebas, es posible que le resulte útil agregar una función auxiliar que le permita restablecer el bot por completo. Vea un [ejemplo de Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) o [ejemplo de C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) para obtener más detalles sobre cómo implementarlo.

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

El evento `conversationUpdate` con el objeto `membersRemoved` en la carga se envía cuando se quita el bot de un equipo o se quita un usuario de un equipo donde se ha agregado un bot. Teams también agrega `eventType.teamMemberRemoved` en el `channelData` objeto . Al igual que con el objeto `membersAdded`, debe analizar el objeto `membersRemoved` para el identificador de aplicación del bot para determinar quién se quitó.

### <a name="schema-example-team-member-removed"></a>Ejemplo de esquema: miembro del equipo quitado

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

El evento `conversationUpdate` con el objeto `membersRemoved` de la carga se envía cuando se quita un usuario de una reunión programada privada. Los detalles del evento se enviarán incluso cuando los usuarios anónimos se unan a la reunión.

> [!NOTE]
>
>* Cuando se quita un usuario anónimo de una reunión, el objeto de carga membersRemoved no tiene el campo `aadObjectId`.
>* Cuando se quita un usuario anónimo de una reunión, el objeto `from` de la carga siempre tiene el identificador del organizador de la reunión, incluso si otro moderador quitó el usuario anónimo.

#### <a name="schema-example-user-removed-from-meeting"></a>Ejemplo de esquema: usuario quitado de la reunión

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
> No hay ninguna funcionalidad para consultar todos los nombres del equipo y no se devuelve el nombre de equipo en las cargas de otros eventos.

El bot recibe una notificación cuando se cambia el nombre del equipo en el que se encuentra. Recibe un evento `conversationUpdate` con `eventType.teamRenamed` en el objeto `channelData`. Tenga en cuenta que no hay ninguna notificación para la creación o eliminación de equipos, ya que los bots solo existen como parte de los equipos y no tienen visibilidad fuera del ámbito en el que se han agregado.

### <a name="schema-example-team-renamed"></a>Ejemplo de esquema: se ha cambiado el nombre del equipo

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

## <a name="channel-updates"></a>Actualizaciones de canal

El bot recibe una notificación cuando se crea, se cambia el nombre o se elimina un canal en un equipo en el que se ha agregado. De nuevo, se recibe el evento `conversationUpdate` y se envía un identificador de evento específico de Teams como parte del objeto `channelData.eventType`, donde el `channel.id` de los datos del canal es el GUID del canal y `channel.name` contiene el propio nombre del canal.

Los eventos de canal son los siguientes:

* **channelCreated**&emsp;Un usuario agrega un nuevo canal al equipo.
* **channelRenamed**&emsp;Un usuario cambia el nombre de un canal existente.
* **channelDeleted**&emsp;Un usuario quita un canal.

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

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a>Extracto de esquema: channelData para channelProgramed

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

El `messageReaction` evento se envía cuando un usuario agrega o quita su reacción a un mensaje, que fue enviado originalmente por el bot. `replyToId` contiene el identificador del mensaje específico.

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

### <a name="schema-example-a-user-un-likes-a-message"></a>Ejemplo de esquema: un usuario quita el me gusta de un mensaje

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

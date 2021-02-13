---
title: Conversaciones de chat de canal y grupo con bots
description: Describe el escenario completo de tener una conversación con un bot en un canal de Microsoft Teams
keywords: bot de conversación de canales de escenarios de teams
ms.date: 06/25/2019
ms.openlocfilehash: e556eb006257a83ddf93adb62f79857201d6a9ad
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231634"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Conversaciones de chat de canal y grupo con un bot de Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams permite a los usuarios traer bots a sus conversaciones de chat en grupo o canal. Al agregar un bot a un equipo o chat, todos los usuarios de la conversación pueden aprovechar la funcionalidad del bot directamente en la conversación. También puede acceder a la funcionalidad específica de Teams dentro de su bot, como consultar la información del equipo y @mentioning usuarios.

El chat en canales y chats de grupo difiere del chat personal en que el usuario necesita @mention el bot. Si un bot se usa en varios ámbitos (personal, groupchat o channel), deberá detectar de qué ámbito procesó los mensajes del bot y procesarlos en consecuencia.

## <a name="designing-a-great-bot-for-channels-or-groups"></a>Diseño de un bot excelente para canales o grupos

Los bots agregados a un equipo se convierten en otro miembro del equipo y @mentioned como parte de la conversación. De hecho, los bots solo reciben mensajes cuando @mentioned, por lo que otras conversaciones en el canal no se envían al bot.

Un bot de un grupo o canal debe proporcionar información relevante y adecuada para todos los miembros. Aunque el bot puede proporcionar ciertamente cualquier información relevante para la experiencia, tenga en cuenta que las conversaciones con él son visibles para todos los usuarios. Por lo tanto, un excelente bot en un grupo o canal debe agregar valor a todos los usuarios y, desde luego, no compartir accidentalmente información más adecuada para una conversación uno a uno.

El bot, tal como es, puede ser totalmente relevante en todos los ámbitos sin necesidad de trabajo adicional. En Microsoft Teams no hay ninguna expectativa de que el bot funcione en todos los ámbitos, pero debe asegurarse de que el bot proporciona valor de usuario en los ámbitos que elija admitir. Para obtener más información sobre los ámbitos, vea [Aplicaciones en Microsoft Teams.](~/concepts/build-and-test/app-studio-overview.md)

El desarrollo de un bot que funciona en grupos o canales usa gran parte de la misma funcionalidad que las conversaciones personales. Los eventos y datos adicionales de la carga proporcionan información de grupo y canal de Teams. Estas diferencias, así como las diferencias clave en la funcionalidad común se describen en las secciones siguientes.

### <a name="creating-messages"></a>Creación de mensajes

Para obtener más información sobre los bots que crean mensajes en [canales,](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)vea Mensajería proactiva para bots y, específicamente, [crear una conversación de canal.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)

### <a name="receiving-messages"></a>Recibir mensajes

Para un bot en un grupo o canal, además del esquema de mensajes [normal,](https://docs.botframework.com/core-concepts/reference/#activity)el bot también recibe las siguientes propiedades:

* `channelData`Vea los [datos del canal de Teams.](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data) En un chat de grupo, contiene información específica de ese chat.
* `conversation.id` El identificador de cadena de respuesta, que consta del identificador de canal más el identificador del primer mensaje de la cadena de respuesta
* `conversation.isGroup` Es `true` para mensajes de bot en canales o chats de grupo
* `conversation.conversationType` Cualquiera `groupChat` de las dos `channel`
* `entities`Puede contener una o más menciones (vea [Menciones)](#-mentions)

### <a name="replying-to-messages"></a>Responder a mensajes

Para responder a un mensaje existente, llame [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) en .NET o [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) en Node.js. El SDK de Bot Builder controla todos los detalles.

Si decide usar la API de REST, también puede llamar al punto de [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) conexión.

En un canal, la respuesta a un mensaje se muestra como una respuesta a la cadena de respuesta de inicio. Contiene `conversation.id` el canal y el identificador de mensaje de nivel superior. Aunque Bot Framework se encarga de los detalles, puede almacenarlo en caché para futuras respuestas a ese hilo `conversation.id` de conversación según sea necesario.

### <a name="best-practice-welcome-messages-in-teams"></a>Procedimiento recomendado: Mensajes de bienvenida en Teams

Cuando el bot se agrega por primera vez al grupo o equipo, generalmente resulta útil enviar un mensaje de bienvenida que presenta el bot a todos los usuarios. El mensaje de bienvenida debe proporcionar una descripción de la funcionalidad del bot y las ventajas del usuario. Lo ideal es que el mensaje también incluya comandos para que el usuario interactúe con la aplicación. Para ello, asegúrese de que el bot responde al `conversationUpdate` mensaje, con `teamsAddMembers` el eventType en el `channelData` objeto. Asegúrese de que el identificador es el id. de aplicación del bot, ya que se envía el mismo evento cuando se agrega un usuario `memberAdded` a un equipo. Vea [la adición de bots o miembros](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) del equipo para obtener más información.

Es posible que también desee enviar un mensaje personal a cada miembro del equipo cuando se agrega el bot. Para ello, puede capturar [la lista](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) del equipo y enviar un mensaje directo a [cada usuario.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)

Se recomienda que el bot *no envíe* un mensaje de bienvenida en las siguientes situaciones:

* El equipo es grande (obviamente subjetivo, pero, por ejemplo, más de 100 miembros). Es posible que el bot se vea como "spammy" y la persona que lo agregó puede recibir quejas a menos que comunique claramente la propuesta de valor del bot a todos los usuarios que vean el mensaje de bienvenida.
* El bot se menciona por primera vez en un grupo o canal (frente a que se agrega por primera vez a un equipo)
* Se cambia el nombre de un grupo o canal
* Se agrega un miembro del equipo a un grupo o canal

## <a name="-mentions"></a>@ Menciones

Dado que los bots de un grupo o canal responden solo cuando se mencionan ("@_botname_") en un mensaje, cada mensaje recibido por un bot en un canal de grupo contiene su propio nombre y debe asegurarse de que el análisis de mensajes lo controla. Además, los bots pueden analizar otros usuarios mencionados y mencionar a los usuarios como parte de sus mensajes.

### <a name="retrieving-mentions"></a>Recuperar menciones

Las menciones se devuelven en el objeto en carga y contienen el identificador único del usuario y, en la mayoría de los casos, el nombre `entities` del usuario mencionado. Puede recuperar todas las menciones del mensaje llamando a la función en bot Builder SDK para .NET, que devuelve una `GetMentions` matriz de `Mentioned` objetos.

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a>Código de ejemplo de .NET: comprobar y quitar @bot mención

```csharp
Mention[] m = sourceMessage.GetMentions();
var messageText = sourceMessage.Text;

for (int i = 0;i < m.Length;i++)
{
    if (m[i].Mentioned.Id == sourceMessage.Recipient.Id)
    {
        //Bot is in the @mention list.
        //The below example will strip the bot name out of the message, so you can parse it as if it wasn't included. Note that the Text object will contain the full bot name, if applicable.
        if (m[i].Text != null)
            messageText = messageText.Replace(m[i].Text, "");
    }
}
```

> [!NOTE]
> También puede usar la función de extensión de Teams, que elimina todas `GetTextWithoutMentions` las menciones, incluido el bot.

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a>Node.js código de ejemplo: Comprobar y quitar @bot mención

```javascript
var text = message.text;
if (message.entities) {
    message.entities
        .filter(entity => ((entity.type === "mention") && (entity.mentioned.id.toLowerCase() === botId)))
        .forEach(entity => {
            text = text.replace(entity.text, "");
        });
    text = text.trim();
}
```

También puede usar la función de extensión de Teams, que elimina todas `getTextWithoutMentions` las menciones, incluido el bot.

### <a name="constructing-mentions"></a>Construcción de menciones

El bot puede mencionar a otros usuarios en mensajes publicados en canales. Para ello, el mensaje debe hacer lo siguiente:

* Incluir `<at>@username</at>` en el texto del mensaje
* Incluir el `mention` objeto dentro de la colección de entidades

#### <a name="net-example"></a>Ejemplo de .NET

En este ejemplo se usa [el paquete NuGet Microsoft.Bot.Connector.Teams.](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a>Node.js ejemplo

```javascript
// User to mention
var toMention: builder.IIdentity = {
    name: 'John Doe',
    id: userId
};

// Create a message and add mention to it
var msg = new teams.TeamsMessage(session).text(teams.TeamsMessage.getTenantId(session.message));
var mentionedMsg = msg.addMentionToText(toMention);

// Post the message
var generalMessage = mentionedMsg.routeReplyToGeneralChannel();
session.send(generalMessage);
```

#### <a name="example-outgoing-message-with-user-mentioned"></a>Ejemplo: mensaje saliente con el usuario mencionado

```json
{
    "type": "message", 
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "28:9e52142b-5e5e-4d7b-bb3e- e82dcf620000",
        "name": "SchemaTestBot"
    },
    "conversation": {
        "id": "19:aebd0ad4d6ab42c8b9ed19c251c2fc37@thread.skype;messageid=1481567603816"
    },
    "recipient": {
        "id": "8:orgid:6aebbad0-e5a5-424a-834a-20fb051f3c1a",
        "name": "stlrgload100"
    },
    "attachments": [
        {
            "contentType": "image/png",
            "contentUrl": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
            "name": "Bender_Rodriguez.png"
        }
    ],
    "entities": [
        {
            "type":"mention",
            "mentioned":{
                "id":"29:08q2j2o3jc09au90eucae",
                "name":"Pranav Smith"
            },
            "text": "<at>@Pranav Smith</at>"
        }
    ],
    "replyToId": "3UP4UTkzUk1zzeyW"
}
```

## <a name="accessing-groupchat-or-channel-scope"></a>Acceso a groupChat o ámbito de canal

El bot puede hacer más que enviar y recibir mensajes en grupos y equipos. Por ejemplo, también puede capturar la lista de miembros, incluida su información de perfil, así como la lista de canales. Consulte [Obtener contexto para el bot de Microsoft Teams](~/resources/bot-v3/bots-context.md) para obtener más información.

*Vea también ejemplos* [de Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)

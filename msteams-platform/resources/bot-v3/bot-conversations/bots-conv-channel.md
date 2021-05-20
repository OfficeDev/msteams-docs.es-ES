---
title: Conversaciones de chat de canal y grupo con bots
description: Describe el escenario de extremo a extremo de tener una conversación con un bot en un canal en Microsoft Teams
keywords: escenarios de equipos canaliza bot de conversación
localization_priority: Normal
ms.topic: conceptual
ms.date: 06/25/2019
ms.openlocfilehash: e254302271cf101638c897e1a1952d302705d6a4
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566799"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Conversaciones de chat de canal y grupo con un bot de Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams permite a los usuarios llevar bots a sus conversaciones de chat de canal o grupo. Al agregar un bot a un equipo o chatear, todos los usuarios de la conversación pueden aprovechar la funcionalidad del bot directamente en la conversación. También puede acceder a Teams funcionalidad específica del bot, como consultar información del equipo y @mentioning usuarios.

Chatear en canales y chats de grupo difieren del chat personal en el que el usuario necesita @mention el bot. Si un bot se usa en varios ámbitos como personal, groupchat o canal, debe detectar de qué ámbito proceden los mensajes de bot y procesarlos en consecuencia.

## <a name="designing-a-great-bot-for-channels-or-groups"></a>Diseñar un gran bot para canales o grupos

Bots añadido a un equipo se convierten en otro miembro del equipo y se pueden @mentioned como parte de la conversación. De hecho, los bots solo reciben mensajes cuando se @mentioned, por lo que otras conversaciones en el canal no se envían al bot.

Un bot de un grupo o canal debe proporcionar información relevante y adecuada para todos los miembros. Si bien su bot ciertamente puede proporcionar cualquier información relevante para la experiencia, tenga en cuenta que las conversaciones con él son visibles para todos. Por lo tanto, un gran bot en un grupo o canal debe agregar valor a todos los usuarios, y ciertamente no compartir información inadvertidamente más adecuada a una conversación uno a uno.

Su bot, tal como es, puede ser completamente relevante en todos los ámbitos sin requerir trabajo adicional. En Microsoft Teams no hay ninguna expectativa de que el bot funcione en todos los ámbitos, pero debe asegurarse de que el bot proporciona valor de usuario en los ámbitos que elija admitir. Para obtener más información sobre los ámbitos, consulte [Aplicaciones en Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).

El desarrollo de un bot que funciona en grupos o canales utiliza gran parte de la misma funcionalidad que las conversaciones personales. Los eventos y datos adicionales de la carga proporcionan información de grupo y canal Teams. Estas diferencias, así como las diferencias clave en la funcionalidad común se describen en las secciones siguientes.

### <a name="creating-messages"></a>Creación de mensajes

Para obtener más información sobre los bots que crean mensajes en canales, consulte [Mensajería proactiva para bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)y, específicamente, [Creación de una conversación de canal.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)

### <a name="receiving-messages"></a>Recepción de mensajes

Para un bot en un grupo o canal, además del [esquema de mensaje normal,](https://docs.botframework.com/core-concepts/reference/#activity)el bot también recibe las siguientes propiedades:

* `channelData`Consulte [Teams datos del canal](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data). En un chat de grupo, contiene información específica de ese chat.
* `conversation.id` El ID de cadena de respuesta, que consta de ID de canal más el ID del primer mensaje de la cadena de respuesta.
* `conversation.isGroup` Es `true` para mensajes de bot en canales o chats de grupo.
* `conversation.conversationType` O `groupChat` `channel` bien .
* `entities` Puede contener una o más menciones. Para obtener más información, consulte [Menciones](#-mentions).

### <a name="replying-to-messages"></a>Responder a los mensajes

Para responder a un mensaje existente, llame a [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) .NET o [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) en Node.js. El SDK de Bot Builder controla todos los detalles.

Si decide usar la API de REST, también puede llamar al [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) punto de conexión.

En un canal, responder a un mensaje se muestra como respuesta a la cadena de respuesta de inicio. Contiene `conversation.id` el canal y el identificador de mensaje de nivel superior. Aunque Bot Framework se encarga de los detalles, puede almacenar en caché eso `conversation.id` para futuras respuestas a ese subproceso de conversación según sea necesario.

### <a name="best-practice-welcome-messages-in-teams"></a>Mejores prácticas: Mensajes de bienvenida en Teams

Cuando el bot se agrega por primera vez al grupo o equipo, generalmente es útil enviar un mensaje de bienvenida introduciendo el bot a todos los usuarios. El mensaje de bienvenida debe proporcionar una descripción de la funcionalidad del bot y las ventajas del usuario. Idealmente, el mensaje también debe incluir comandos para que el usuario interactúe con la aplicación. Para ello, asegúrese de que el bot responde al `conversationUpdate` mensaje, con el `teamsAddMembers` eventType en el `channelData` objeto. Asegúrese de que el `memberAdded` identificador es el propio ID de aplicación del bot, porque el mismo evento se envía cuando se agrega un usuario a un equipo. Consulte [Miembro del equipo o adición de bots](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) para obtener más detalles.

También es posible que desee enviar un mensaje personal a cada miembro del equipo cuando se agrega el bot. Para ello, puede [obtener la lista de equipos](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) y enviar a cada usuario un mensaje [directo.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)

Le recomendamos que el bot *no* envíe un mensaje de bienvenida en las siguientes situaciones:

* El equipo es grande (obviamente subjetivo, por ejemplo, más de 100 miembros). Su bot puede ser visto como 'spam' y la persona que lo agregó puede recibir quejas a menos que comunique claramente la propuesta de valor de su bot a todos los que ven el mensaje de bienvenida.
* El bot se menciona primero en un grupo o canal, en lugar de agregarse primero a un equipo.
* Se cambia el nombre de un grupo o canal.
* Un miembro del equipo se agrega a un grupo o canal.

## <a name="-mentions"></a>@ Menciones

Dado que los bots de un grupo o canal responden solo cuando se mencionan ("@_botname")_ en un mensaje, cada mensaje recibido por un bot en un canal de grupo contiene su propio nombre y debe asegurarse de que el análisis de mensajes controla eso. Además, los bots pueden analizar a otros usuarios mencionados y mencionar a los usuarios como parte de sus mensajes.

### <a name="retrieving-mentions"></a>Recuperación de menciones

Las menciones se devuelven en el `entities` objeto en la carga útil y contienen tanto el identificador único del usuario como, en la mayoría de los casos, el nombre del usuario mencionado. Puede recuperar todas las menciones del mensaje llamando a la `GetMentions` función en el SDK de Bot Builder para .NET, que devuelve una matriz de `Mentioned` objetos.

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a>Código de ejemplo de .NET: compruebe y elimine @bot mención

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
> También puede utilizar la función de extensión Teams `GetTextWithoutMentions` , que elimina todas las menciones, incluido el bot.

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a>Node.js código de ejemplo: Compruebe si hay una mención @bot

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

También puede utilizar la función de extensión Teams `getTextWithoutMentions` , que elimina todas las menciones, incluido el bot.

### <a name="constructing-mentions"></a>Construcción de menciones

El bot puede mencionar a otros usuarios en los mensajes publicados en canales. Para ello, el mensaje debe hacer lo siguiente:

* Incluir `<at>@username</at>` en el texto del mensaje.
* Incluya el `mention` objeto dentro de la colección entities.

#### <a name="net-example"></a>Ejemplo de .NET

En este ejemplo se usa el paquete [NuGet Microsoft.Bot.Connector.Teams.](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)

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

#### <a name="example-outgoing-message-with-user-mentioned"></a>Ejemplo: Mensaje saliente con el usuario mencionado

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

## <a name="accessing-groupchat-or-channel-scope"></a>Acceso a groupChat o alcance de canal

El bot puede hacer algo más que enviar y recibir mensajes en grupos y equipos. Por ejemplo, también puede obtener la lista de miembros, incluida la información de su perfil, así como la lista de canales. Para obtener más información, consulte [Obtener contexto para el bot de Microsoft Teams](~/resources/bot-v3/bots-context.md).

## <a name="see-also"></a>Vea también

[Muestras de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)

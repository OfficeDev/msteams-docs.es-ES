---
title: Conversaciones de chat en grupo y de canal con bots
description: Describe el escenario de un extremo a otro de tener una conversación con un bot en un canal en Microsoft Teams.
keywords: escenarios de conferencia de canales de Teams
ms.date: 06/25/2019
ms.openlocfilehash: d2d72bdba43de6ebb10c7504dd309459cb09d56c
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801474"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Conversaciones de chat en grupo y en el canal con un bot de Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams permite a los usuarios traer bots a sus conversaciones de chat en el canal o en el grupo. Al agregar un bot a un equipo o un chat, todos los usuarios de la conversación pueden aprovechar la funcionalidad de bot en la conversación. También puede tener acceso a la funcionalidad específica de Teams dentro de su bot, como consultar la información del equipo y los usuarios de @mentioning.

Los chats de canales y chats de grupo se diferencian de los chats personales en que el usuario debe @mention el bot. Si se usa un bot en varios ámbitos (personal, Groupchat o Channel), tendrá que detectar el ámbito desde el que proceden los mensajes de Bot y procesarlos en consecuencia.

## <a name="designing-a-great-bot-for-channels-or-groups"></a>Diseño de un gran robot para canales o grupos

Los bots agregados a un equipo se convierten en otro miembro del equipo, que puede ser @mentioned como parte de la conversación. De hecho, los bots sólo reciben mensajes cuando se @mentioned, por lo que no se envían otras conversaciones en el canal al bot.

> [!NOTE]
> Por comodidad al responder a los mensajes de bot en un canal, el nombre del bot se antepone en el cuadro de mensaje de redacción de forma automática.

Un bot en un grupo o un canal debe proporcionar información relevante y adecuada para todos los miembros. Aunque el bot puede proporcionar toda la información relevante para la experiencia, tenga en cuenta que todos los usuarios pueden ver las conversaciones. Por lo tanto, un gran bot en un grupo o un canal debe agregar valor a todos los usuarios y, ciertamente, no compartir información de forma más adecuada en una conversación de uno a uno.

El bot puede ser totalmente relevante en todos los ámbitos tal y como es, y no se requiere un trabajo adicional importante para permitir que el bot funcione a través de ellos. En Microsoft Teams no hay expectativa de que la función bot funcione en todos los ámbitos, pero debe asegurarse de que su bot proporciona valor de usuario en el ámbito o ámbitos que desee admitir. Para obtener más información sobre los ámbitos, consulte [aplicaciones en Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).

El desarrollo de un bot que funciona en grupos o canales usa la mayor parte de la funcionalidad de las conversaciones personales. Los datos y los eventos adicionales de la carga proporcionan información sobre el grupo y el canal de Microsoft Teams. Estas diferencias, así como las diferencias clave en la funcionalidad común, se describen en las siguientes secciones.

### <a name="creating-messages"></a>Crear mensajes

Para obtener más información acerca de los bots que crean mensajes en canales, consulte [Mensajería proactiva para bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)y [crear específicamente una conversación de canal](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).

### <a name="receiving-messages"></a>Recibir mensajes

Para un bot en un grupo o canal, además del [esquema normal del mensaje](https://docs.botframework.com/core-concepts/reference/#activity), el bot también recibe las siguientes propiedades:

* `channelData`Consulte [Teams Data Channels](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data). En un chat en grupo, contiene información específica de ese chat.
* `conversation.id`IDENTIFICADOR de la cadena de respuesta que consta del identificador de canal más el identificador del primer mensaje en la cadena de respuesta.
* `conversation.isGroup`Está `true` destinado a los mensajes de bot en canales o chats de grupo
* `conversation.conversationType`Ya sea `groupChat` o`channel`
* `entities`Puede contener una o más menciones (vea las [menciones](#-mentions))

### <a name="replying-to-messages"></a>Responder a mensajes

Para responder a un mensaje existente, llame a [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) .net o a [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) Node.js. El SDK de bot Builder controla todos los detalles.

Si decide usar la API de REST, también puede llamar al punto de [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) conexión.

En un canal, la respuesta a un mensaje se muestra como una respuesta a la cadena de respuesta de iniciación. El `conversation.id` contiene el canal y el identificador de mensaje de nivel superior. Aunque el marco de bot se encarga de los detalles, puede almacenar en la memoria caché el que, en el `conversation.id` caso de respuestas futuras, a ese hilo de conversación según sea necesario.

### <a name="best-practice-welcome-messages-in-teams"></a>Procedimiento recomendado: mensajes de bienvenida en Microsoft Teams

Cuando el bot se agrega por primera vez al grupo o equipo, suele ser útil enviar un mensaje de bienvenida que presenta el bot a todos los usuarios. El mensaje de bienvenida debe proporcionar una descripción de las ventajas del usuario y la funcionalidad del bot. Lo ideal es que el mensaje también incluya comandos para que el usuario interactúe con la aplicación. Para ello, asegúrese de que el bot responde al `conversationUpdate` mensaje, con el `teamsAddMembers` EventType en el `channelData` objeto. Asegúrese de que el `memberAdded` identificador es el propio identificador de aplicación del bot, ya que se envía el mismo evento cuando se agrega un usuario a un equipo. Consulte el [miembro del equipo o la adición de bot](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) para obtener más información.

Es posible que también desee enviar un mensaje personal a cada miembro del equipo cuando se agregue el bot. Para ello, puede [recuperar la lista de equipos](~/resources/bot-v3/bots-context.md#fetching-the-team-roster) y enviar a cada usuario un [mensaje directo](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).

Se recomienda que el bot *no* envíe un mensaje de bienvenida en las siguientes situaciones:

* El equipo es grande (obviamente subjetivo, pero por ejemplo, más de 100 miembros). El bot puede aparecer como "correo no deseado" y la persona que lo agregó puede recibir quejas a menos que comunique claramente la propuesta de valor de su bot a todos los usuarios que ven el mensaje de bienvenida.
* El bot se menciona primero en un grupo o canal (en lugar de agregarse primero a un equipo)
* Se cambia el nombre de un grupo o canal
* Un miembro del equipo se agrega a un grupo o un canal

## <a name="-mentions"></a>@ Menciones

Debido a que los bots de un grupo o canal solo responden cuando se mencionan ("@_botname_") en un mensaje, cada mensaje recibido por un bot en un canal de grupo contiene su propio nombre y debe asegurarse de que los controladores de análisis de mensajes. Además, los bots pueden analizar a otros usuarios mencionados y mencionar a los usuarios como parte de sus mensajes.

### <a name="retrieving-mentions"></a>Recuperación de menciones

Las menciones se devuelven en el `entities` objeto en la carga y contienen el identificador único del usuario y, en la mayoría de los casos, el nombre del usuario mencionado. Puede recuperar todas las menciones del mensaje llamando a la `GetMentions` función en el SDK de bot Builder para .net, que devuelve una matriz `Mentioned` de objetos.

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
> También puede usar la función de extensión de Teams `GetTextWithoutMentions` , que elimina todas las menciones, incluido el bot.

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a>Código de ejemplo Node.js: buscar y quitar @bot mención

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

También puede usar la función de extensión de Teams `getTextWithoutMentions` , que elimina todas las menciones, incluido el bot.

### <a name="constructing-mentions"></a>Creación de menciones

El bot puede mencionar a otros usuarios en los mensajes enviados a los canales. Para ello, el mensaje debe hacer lo siguiente:

* Incluir `<at>@username</at>` en el texto del mensaje
* Incluir el `mention` objeto dentro de la colección Entities

#### <a name="net-example"></a>Ejemplo de .NET

En este ejemplo se usa el paquete NuGet [Microsoft. bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) .

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a>Ejemplo de Node.js

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

## <a name="accessing-groupchat-or-channel-scope"></a>Acceso a groupChat o al ámbito del canal

El bot puede hacer más cosas que enviar y recibir mensajes en grupos y equipos. Por ejemplo, también puede recuperar la lista de miembros, incluida la información de su perfil, así como la lista de canales. Consulte [obtener contexto de su bot de Microsoft Teams](~/resources/bot-v3/bots-context.md) para obtener más información.

*Vea también* [ejemplos del marco de bot](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).

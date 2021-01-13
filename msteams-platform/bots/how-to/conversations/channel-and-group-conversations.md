---
title: Conversaciones de canal y grupo con un bot
author: clearab
description: Cómo enviar, recibir y controlar mensajes de un bot en un chat de canal o grupo.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 8a9a58208fff5cc2fe376fcb9932bad6ac2bf36f
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797844"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Conversaciones de chat de canal y grupo con un bot de Microsoft Teams

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Al agregar el ámbito o al bot, puede estar disponible para instalarse en un chat de `teams` `groupchat` grupo o equipo. Esto permite que todos los miembros de la conversación interactúen con el bot. Una vez instalado, también tendrá acceso a metadatos sobre la conversación, como la lista de miembros de la conversación, y cuando se instala en los detalles de un equipo sobre ese equipo y la lista completa de canales.

Los bots de un grupo o canal solo reciben mensajes cuando se mencionan (@botname), no reciben ningún otro mensaje enviado a la conversación.

> [!NOTE]
> El bot debe ser @mentioned directamente. El bot no recibirá un mensaje cuando se menciona al equipo o al canal, o cuando alguien responda a un mensaje de su bot sin @mentioning lo haga.

## <a name="design-guidelines"></a>Directrices de diseño

Vea cómo diseñar [conversaciones de bot en canales y chats.](~/bots/design/bots.md)

## <a name="creating-new-conversation-threads"></a>Creación de nuevos subprocesos de conversación

Cuando el bot está instalado en un equipo, a veces puede ser necesario crear un nuevo hilo de conversación en lugar de responder a uno existente. Se trata de una forma de [mensajería proactiva.](~/bots/how-to/conversations/send-proactive-messages.md)

## <a name="working-with-mentions"></a>Trabajar con menciones

Cada mensaje a su bot desde un grupo o canal contendrá un @mention con su propio nombre en el texto del mensaje, por lo que tendrá que asegurarse de que el análisis de mensajes lo controla. El bot también puede recuperar otros usuarios mencionados en un mensaje y agregar menciones a los mensajes que envíe.

### <a name="stripping-mentions-from-message-text"></a>Quitar menciones del texto del mensaje

Es posible que sea necesario quitar el @mentions del texto del mensaje que recibe el bot.

### <a name="retrieving-mentions"></a>Recuperar menciones

Las menciones se devuelven en el objeto en carga y contienen el identificador único del usuario y, en la mayoría de los casos, el nombre `entities` del usuario mencionado. El texto del mensaje también incluirá la mención como `<at>@John Smith<at>` . Sin embargo, no debe confiar en el texto del mensaje para recuperar información sobre el usuario; es posible que la persona que envía el mensaje lo modifique. En su lugar, use el `entities` objeto.

Puede recuperar todas las menciones del mensaje llamando a la función en el SDK de `GetMentions` Bot Builder que devuelve una matriz de `Mention` objetos.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    Mention[] mentions = turnContext.Activity.GetMentions();
    if(mentions != null)
    {
        ChannelAccount firstMention = mentions[0].Mentioned;
        await turnContext.SendActivityAsync($"Hello {firstMention.Name}");
    }
    else
    {
        await turnContext.SendActivityAsync("Aw, no one was mentioned.");
    }
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    const mentions = TurnContext.getMentions(turnContext.activity);
    if (mentions){
        const firstMention = mentions[0].mentioned;
        await turnContext.sendActivity(`Hello ${firstMention.name}.`);
    } else {
        await turnContext.sendActivity(`Aw, no one was mentioned.`);
    }

    await next();
});
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "type": "message",
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "29:9e52142b-5e5e-4d7b-bb3e-e82dcf620000",
        "name": "Jane Smith"
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

# <a name="python"></a>[Python](#tab/python)

```python
@staticmethod
def get_mentions(activity: Activity) -> List[Mention]:
    result: List[Mention] = []
    if activity.entities is not None:
        for entity in activity.entities:
            if entity.type.lower() == "mention":
                    result.append(entity)
     return result
```

* * *

### <a name="adding-mentions-to-your-messages"></a>Agregar menciones a los mensajes

El bot puede mencionar a otros usuarios en mensajes publicados en canales. Para ello, el mensaje debe hacer lo siguiente:

El `Mention` objeto tiene dos propiedades que deberá establecer:

* Incluir <at>@username</at> en el texto del mensaje
* Incluir el objeto de mención dentro de la colección de entidades

El SDK de Bot Framework proporciona objetos y métodos auxiliares para facilitar la construcción de la mención.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var mention = new Mention
    {
        Mentioned = turnContext.Activity.From,
        Text = $"<at>{XmlConvert.EncodeName(turnContext.Activity.From.Name)}</at>",
    };

    var replyActivity = MessageFactory.Text($"Hello {mention.Text}.");
    replyActivity.Entities = new List<Entity> { mention };

    await turnContext.SendActivityAsync(replyActivity, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    const mention = {
        mentioned: turnContext.activity.from,
        text: `<at>${ new TextEncoder().encode(turnContext.activity.from.name) }</at>`,
    } as Mention;

    const replyActivity = MessageFactory.text(`Hello ${mention.text}`);
    replyActivity.entities = [mention];

    await turnContext.sendActivity(replyActivity);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="json"></a>[JSON](#tab/json)

El `text` campo del objeto de la `entities` matriz debe coincidir *exactamente* con una parte del campo de `text` mensaje. Si no es así, se omitirá la mención.

```json
{
    "type": "message",
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "29:9e52142b-5e5e-4d7b-bb3e-e82dcf620000",
        "name": "Jane Smith"
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

# <a name="python"></a>[Python](#tab/python)

```python
async def _mention_activity(self, turn_context: TurnContext):
        mention = Mention(
            mentioned=turn_context.activity.from_property,
            text=f"<at>{turn_context.activity.from_property.name}</at>",
            type="mention"
        )

        reply_activity = MessageFactory.text(f"Hello {mention.text}")
        reply_activity.entities = [Mention().deserialize(mention.serialize())]
        await turn_context.send_activity(reply_activity)
```

* * *

## <a name="sending-a-message-on-installation"></a>Enviar un mensaje durante la instalación

Cuando el bot se agrega por primera vez al grupo o equipo, puede resultar útil enviar un mensaje que lo presenta. El mensaje debe proporcionar una breve descripción de las características del bot y cómo usarlas. You'll want to subscribe to the `conversationUpdate` event, with the `teamMemberAdded` eventType.  Dado que el evento se envía cuando se agrega un nuevo miembro del equipo, debe comprobar si el nuevo miembro agregado es el bot. Consulte [Enviar un mensaje de bienvenida a un nuevo miembro del equipo](~/bots/how-to/conversations/send-proactive-messages.md) para obtener más información.

Es posible que también desee enviar un mensaje personal a cada miembro del equipo cuando se agrega el bot. Para ello, puede obtener la lista del equipo y enviar un mensaje directo a cada usuario.

No se recomienda enviar un mensaje en las siguientes situaciones:

* El equipo es grande (obviamente subjetivo, pero por ejemplo más de 100 miembros). Es posible que el bot se vea como "spammy" y la persona que lo agregó puede recibir quejas a menos que comunique claramente la propuesta de valor del bot a todos los usuarios que vean el mensaje de bienvenida.
* El bot se menciona por primera vez en un grupo o canal (frente a que se agrega por primera vez a un equipo)
* Se cambia el nombre de un grupo o canal
* Se agrega un miembro del equipo a un grupo o canal

## <a name="learn-more"></a>Más información

El bot tiene acceso a información adicional sobre el chat en grupo o el equipo en el que está instalado. Vea [obtener el contexto de teams](~/bots/how-to/get-teams-context.md) para obtener api adicionales disponibles para su bot.

También hay eventos adicionales a los que el bot puede suscribirse y responder. Vea [suscribirse a eventos de conversación](~/bots/how-to/conversations/subscribe-to-conversation-events.md) para obtener información sobre cómo hacerlo.

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

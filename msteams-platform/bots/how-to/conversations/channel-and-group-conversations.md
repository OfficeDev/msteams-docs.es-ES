---
title: Conversaciones de canales y grupos
author: clearab
description: Cómo enviar, recibir y administrar mensajes para un bot en un canal o un chat en grupo.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: ada2839ba41e4004b5f48449f4e057830dd841b9
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676111"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Conversaciones de chat en grupo y en el canal con un bot de Microsoft Teams

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Al agregar el `teams` ámbito `groupchat` o al bot, puede estar disponible para instalarse en un chat de grupo o de equipo. Esto permite a todos los miembros de la conversación interactuar con el bot. Una vez instalado, también tendrá acceso a los metadatos sobre la conversación, como la lista de miembros de la conversación, y cuando se instale en un equipo detalles sobre ese equipo y la lista completa de canales.

Los bots de un grupo o canal solo reciben mensajes cuando se mencionan ("@botname"), no reciben ningún otro mensaje que se envíe a la conversación.

> [!NOTE]
> El bot debe estar @mentioned directamente. El bot no recibirá un mensaje cuando se menciona el equipo o el canal, o cuando alguien responde a un mensaje desde el bot sin @mentioning.

## <a name="design-considerations"></a>Consideraciones sobre diseño

Un bot debe proporcionar información que sea adecuada y relevante para todos los miembros de un grupo o canal. Las conversaciones con él son visibles para todos los usuarios que forman parte del grupo o del canal. Un robot bien diseñado puede agregar valor a todos los usuarios y no compartir involuntariamente información que sea más adecuada en una conversación de uno a uno. En su lugar, las conversaciones de varios turnos, como los cuadros de diálogo, deben evitarse y usar tarjetas o módulos de tareas para recopilar información.

## <a name="creating-new-conversation-threads"></a>Crear nuevos hilos de conversación

Cuando se instala el bot en un equipo, a veces puede ser necesario crear una nueva secuencia de conversación en lugar de responder a una existente. Esta es una forma de [Mensajería proactiva](~/bots/how-to/conversations/send-proactive-messages.md).

## <a name="working-with--mentions"></a>Trabajar con las @ menciones

Cada mensaje en el bot desde un grupo o canal contendrá un @mention con su propio nombre en el texto del mensaje, por lo que deberá asegurarse de que los controladores de análisis de mensajes lo hagan. El bot también puede recuperar a otros usuarios mencionados en un mensaje y agregar menciones a los mensajes que envía.

### <a name="stripping-mentions-from-message-text"></a>Eliminación de menciones del texto del mensaje

Es posible que necesite quitar el @mentions del texto del mensaje que el bot recibe.

### <a name="retrieving-mentions"></a>Recuperación de menciones

Las menciones se devuelven en el objeto en la `entities` carga y contienen el identificador único del usuario y, en la mayoría de los casos, el nombre del usuario mencionado. El texto del mensaje también incluirá la mención like `<at>@John Smith<at>`. Sin embargo, no debe confiar en el texto del mensaje para recuperar la información sobre el usuario; es posible que la persona que envía el mensaje la altere. En su lugar, use `entities` el objeto.

Puede recuperar todas las menciones del mensaje llamando a la `GetMentions` función en el SDK del generador de robots que devuelve una `Mention` matriz de objetos.

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node. js](#tab/typescript)

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

# <a name="jsontabjson"></a>[JSON](#tab/json)

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

# <a name="pythontabpython"></a>[Python](#tab/python)

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

### <a name="adding-mentions-to-your-messages"></a>Adición de menciones a los mensajes

El bot puede mencionar a otros usuarios en los mensajes enviados a los canales. Para ello, el mensaje debe hacer lo siguiente:

El `Mention` objeto tiene dos propiedades que tendrá que establecer:

* Incluir <at>@username</at> en el texto del mensaje
* Incluir el objeto de menciones dentro de la colección Entities

El SDK de bot proporciona objetos y métodos auxiliares para facilitar la creación de la mención.

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node. js](#tab/typescript)

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

# <a name="jsontabjson"></a>[JSON](#tab/json)

El `text` campo del objeto de la `entities` matriz debe coincidir *exactamente* con una parte del campo `text` mensaje. Si no es así, se omitirá la mención.

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

# <a name="pythontabpython"></a>[Python](#tab/python)

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

Cuando el bot se agrega por primera vez al grupo o equipo, puede resultar útil enviar un mensaje que lo presenta. El mensaje debe proporcionar una breve descripción de las características del bot y cómo usarlas. Querrá suscribirse al `conversationUpdate` evento con `teamMemberAdded` EventType.  Dado que el evento se envía cuando se agrega un nuevo miembro del equipo, debe comprobarlo para determinar si el nuevo miembro agregado es el bot. Consulte [Enviar un mensaje de bienvenida a un nuevo integrante del equipo](~/bots/how-to/conversations/send-proactive-messages.md) para obtener más información.

Es posible que también desee enviar un mensaje personal a cada miembro del equipo cuando se agregue el bot. Para ello, puede obtener la lista del equipo y enviar a cada usuario un mensaje directo.

No se recomienda enviar un mensaje en las siguientes situaciones:

* El equipo es grande (obviamente subjetivo, pero por ejemplo, más de 100 miembros). El bot puede aparecer como "correo no deseado" y la persona que lo agregó puede recibir quejas a menos que comunique claramente la propuesta de valor de su bot a todos los usuarios que ven el mensaje de bienvenida.
* El bot se menciona primero en un grupo o canal (en lugar de agregarse primero a un equipo)
* Se cambia el nombre de un grupo o canal
* Un miembro del equipo se agrega a un grupo o un canal

## <a name="learn-more"></a>Más información

El bot tiene acceso a información adicional sobre el equipo o el chat de grupo en el que está instalado. Consulte [obtener contexto de Microsoft Teams](~/bots/how-to/get-teams-context.md) para API adicionales disponibles para el bot.

También hay eventos adicionales a los que puede suscribirse y responder su bot. Consulte [Subscribe to conversate Events](~/bots/how-to/conversations/subscribe-to-conversation-events.md) para obtener información sobre cómo hacerlo.

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

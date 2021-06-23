---
title: Conversaciones de canal y grupo con un bot
author: surbhigupta
description: Cómo enviar, recibir y controlar mensajes de un bot en un chat de canal o grupo.
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 399f7d7487b4992e70d4ee515b26101e2b253a62
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069006"
---
# <a name="channel-and-group-chat-conversations-with-a-bot"></a>Conversaciones de chat de canal y grupo con un bot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Para instalar el Microsoft Teams bot en un chat de grupo o equipo, agregue el `teams` ámbito o `groupchat` al bot. Esto permite que todos los miembros de la conversación interactúen con el bot. Una vez instalado el bot, tiene acceso a metadatos sobre la conversación, como la lista de miembros de la conversación. Además, cuando se instala en un equipo, el bot tiene acceso a detalles sobre ese equipo y a la lista completa de canales.

Los bots de un grupo o canal solo reciben mensajes cuando se mencionan @botname. No reciben ningún otro mensaje enviado a la conversación. El bot debe ser @mencionado directamente. El bot no recibe un mensaje cuando se menciona el equipo o el canal, o cuando alguien responde a un mensaje del bot sin @mentioning.

> [!NOTE]
> Esta característica está disponible actualmente solo en [la versión preliminar del desarrollador](../../../resources/dev-preview/developer-preview-intro.md) público.
>
> Con el consentimiento específico de recursos (RSC), los bots pueden recibir todos los mensajes de canal en los equipos en los que está instalado sin que se @mentioned. Para obtener más información, vea [recibir todos los mensajes de canal con RSC](channel-messages-with-rsc.md).

## <a name="design-guidelines"></a>Directrices de diseño

A diferencia de los chats personales, en los chats de grupo y canales, el bot debe proporcionar una introducción rápida. Debe seguir estas y más directrices de diseño de bots. Para obtener más información sobre cómo diseñar bots en Teams, vea cómo diseñar conversaciones de [bot en canales y chats.](~/bots/design/bots.md)

Ahora, puedes crear nuevos subprocesos de conversación y administrar fácilmente diferentes conversaciones en canales.

## <a name="create-new-conversation-threads"></a>Crear nuevos subprocesos de conversación

Cuando el bot está instalado en un equipo, debe crear un nuevo subproceso de conversación en lugar de responder a uno existente. A veces es difícil diferenciar entre dos conversaciones. Si la conversación se enhebra, es más fácil organizar y administrar diferentes conversaciones en canales. Se trata de una forma de [mensajería proactiva](~/bots/how-to/conversations/send-proactive-messages.md).

A continuación, puede recuperar menciones con el `entities` objeto y agregar menciones a los mensajes mediante el `Mention` objeto.

## <a name="work-with-mentions"></a>Trabajar con menciones

Cada mensaje al bot de un grupo o canal contiene @mention con su nombre en el texto del mensaje. El bot también puede recuperar otros usuarios mencionados en un mensaje y agregar menciones a los mensajes que envía.

También debe quitar el @mentions del contenido del mensaje que recibe el bot.

### <a name="retrieve-mentions"></a>Recuperar menciones

Las menciones se devuelven en el objeto en payload y contienen el identificador único del usuario y el nombre `entities` del usuario mencionado. El texto del mensaje también incluye la mención, como `<at>@John Smith<at>` . Sin embargo, no confíe en el texto del mensaje para recuperar información sobre el usuario. Es posible que la persona que envía el mensaje lo modifique. Por lo tanto, use el `entities` objeto.

Puede recuperar todas las menciones del mensaje llamando a la función en bot `GetMentions` Builder SDK, que devuelve una matriz de `Mention` objetos.

El siguiente código muestra un ejemplo de recuperación de menciones:

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

### <a name="add-mentions-to-your-messages"></a>Agregar menciones a los mensajes

El bot puede mencionar a otros usuarios en mensajes publicados en canales.

El `Mention` objeto tiene dos propiedades que debe establecer con lo siguiente:

* Incluya <at>@username</at> en el texto del mensaje.
* Incluya el objeto de mención dentro de la colección de entidades.

El SDK de Bot Framework proporciona métodos auxiliares y objetos para crear menciones.

En el siguiente código se muestra un ejemplo de cómo agregar menciones a los mensajes:

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

El `text` campo del objeto de la `entities` matriz debe coincidir con una parte del campo de `text` mensaje. Si no lo hace, se omite la mención.

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

Ahora puedes enviar un mensaje de introducción cuando el bot se instala por primera vez o se agrega a un grupo o equipo.

## <a name="send-a-message-on-installation"></a>Enviar un mensaje durante la instalación

Cuando el bot se agrega por primera vez al grupo o equipo, se debe enviar un mensaje de introducción. El mensaje debe proporcionar una breve descripción de las características del bot y cómo usarlas. Debe suscribirse al `conversationUpdate` evento con `teamMemberAdded` eventType.  El evento se envía cuando se agrega un nuevo miembro del equipo. Compruebe si el nuevo miembro agregado es el bot. Para obtener más información, vea [sending a welcome message to a new team member](~/bots/how-to/conversations/send-proactive-messages.md).

Envíe un mensaje personal a cada miembro del equipo cuando se agrega el bot. Para ello, obtenga la lista de equipos y envíe un mensaje directo a cada usuario.

No envíe un mensaje en los siguientes casos:

* El equipo es grande, por ejemplo, más de 100 miembros. El bot se puede ver como correo no deseado y la persona que lo agregó puede recibir quejas. Debe comunicar claramente la propuesta de valor del bot a todos los usuarios que ve el mensaje de bienvenida.
* El bot se menciona por primera vez en un grupo o canal en lugar de agregarse primero a un equipo.
* Se cambia el nombre de un grupo o canal.
* Un miembro del equipo se agrega a un grupo o canal.

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## <a name="see-also"></a>Consulte también

[Obtener Teams contexto](~/bots/how-to/get-teams-context.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Suscribirse a eventos de conversación](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

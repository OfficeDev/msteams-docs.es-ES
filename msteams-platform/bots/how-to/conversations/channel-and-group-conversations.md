---
title: Canal y conversaciones de chat de grupo con un bot
author: surbhigupta
description: Cómo enviar, recibir y controlar mensajes de un bot en un chat de canal o de grupo. Obtenga información sobre las directrices de diseño, la creación de subprocesos de conversación, el uso de @mentions mediante ejemplos de código
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 6b3adf491ccfed2401308f0b6d283047f24f91e2
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757181"
---
# <a name="channel-and-group-chat-conversations-with-a-bot"></a>Canal y conversaciones de chat de grupo con un bot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Para instalar el bot de Microsoft Teams en un chat de grupo o equipo, agregue el ámbito `teams` o `groupchat` al bot. Esto permite que todos los miembros de la conversación interactúen con el bot. Una vez instalado el bot, tiene acceso a metadatos sobre la conversación, como la lista de miembros de la conversación. Además, cuando se instala en un equipo, el bot tiene acceso a los detalles sobre ese equipo y a la lista completa de canales.

Los bots de un grupo o canal solo reciben mensajes cuando se mencionan @botname. No reciben ningún otro mensaje enviado a la conversación. El bot debe ser @mencionado directamente. El bot no recibe un mensaje cuando se menciona el equipo o el canal, o cuando alguien responde a un mensaje del bot sin @mentioning.

> [!NOTE]
> Esta característica solo está disponible actualmente en la [versión preliminar para desarrolladores públicos](../../../resources/dev-preview/developer-preview-intro.md).
>
> Mediante el consentimiento específico de recursos (RSC), los bots pueden recibir todos los mensajes de canal en los equipos en los que está instalado sin @mentioned. Para obtener más información, consulte [Recepción de todos los mensajes del canal con RSC](channel-messages-with-rsc.md).
>
> Actualmente no se admite la publicación de un mensaje o una tarjeta adaptable en un canal privado.

## <a name="design-guidelines"></a>Directrices de diseño

A diferencia de los chats personales, en los chats y canales de grupo, el bot debe proporcionar una introducción rápida. Debe seguir estas y más instrucciones de diseño de bots. Para obtener más información sobre cómo diseñar bots en Teams, consulte [cómo diseñar conversaciones de bots en canales y chats](~/bots/design/bots.md).

Ahora, puede crear nuevos subprocesos de conversación y administrar fácilmente diferentes conversaciones en canales.

## <a name="create-new-conversation-threads"></a>Creación de nuevos subprocesos de conversación

Cuando el bot está instalado en un equipo, debe crear un nuevo subproceso de conversación en lugar de responder a uno existente. A veces es difícil diferenciar entre dos conversaciones. Si la conversación está encadenada, es más fácil organizar y administrar diferentes conversaciones en canales. Se trata de una forma de [mensajería proactiva](~/bots/how-to/conversations/send-proactive-messages.md).

A continuación, puede recuperar las menciones mediante el objeto `entities` y agregar menciones a los mensajes mediante el objeto `Mention`.

## <a name="work-with-mentions"></a>Trabajar con menciones

Cada mensaje al bot de un grupo o canal contendrá una @mention con su propio nombre en el texto del mensaje. El bot también puede recuperar otros usuarios mencionados en un mensaje y agregar menciones a cualquier mensaje que envíe.

Puede que encuentre necesario quitar las @menciones del texto del mensaje que recibe el bot.

### <a name="retrieve-mentions"></a>Recuperar menciones

Las menciones se devuelven en el objeto `entities` de entidades en carga y contienen tanto el id. único del usuario como, en la mayoría de los casos, el nombre del usuario mencionado. El texto del mensaje también incluye la mención, como `<at>@John Smith<at>`. Sin embargo, no confíe en el texto del mensaje para recuperar información sobre el usuario. Es posible que la persona que envía el mensaje lo altere. Por lo tanto, use el objeto `entities`.

Puede recuperar todas las menciones del mensaje llamando a la función `GetMentions` en el SDK de Bot Builder, que devuelve una matriz de objetos `Mention`.

En el siguiente código se muestra un ejemplo de recuperación de menciones:

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

El bot puede mencionar a otros usuarios en loa mensajes publicados en canales.

El objeto `Mention` tiene dos propiedades que debe establecer mediante lo siguiente:

* Incluya *@username* en el texto del mensaje.
* Incluya el objeto mention dentro de la colección entities.

El SDK de Bot Framework proporciona métodos auxiliares y objetos para crear menciones.

En el siguiente código se muestra un ejemplo de adición de menciones en los mensajes:

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

El campo `text` del objeto de la matriz `entities` debe coincidir con una parte del campo `text` del mensaje. Si no es así, se omite la mención.

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

Ahora puede enviar un mensaje de introducción cuando el bot se instala por primera vez o se agrega a un grupo o equipo.

## <a name="send-a-message-on-installation"></a>Enviar un mensaje durante la instalación

Cuando el bot se agrega por primera vez al grupo o equipo, se debe enviar un mensaje de introducción. El mensaje debe proporcionar una breve descripción de las características del bot y cómo usarlas. Debe suscribirse al evento `conversationUpdate` con el eventType `teamMemberAdded`.  El evento se envía cuando se agrega un nuevo miembro del equipo. Compruebe si el nuevo miembro agregado es el bot. Para obtener más información, consulte [Envío de un mensaje de bienvenida a un nuevo miembro del equipo](~/bots/how-to/conversations/send-proactive-messages.md).

Envíe un mensaje personal a cada miembro del equipo cuando se agregue el bot. Para ello, obtenga la lista de equipos y envíe un mensaje directo a cada usuario.

No envíe un mensaje en los siguientes casos:

* El equipo es grande, por ejemplo, tiene más de 100 miembros. El bot se puede ver como correo no deseado y la persona que lo agregó puede recibir quejas. Debe comunicar claramente la propuesta de valor del bot a todos los usuarios que ven el mensaje de bienvenida.
* El bot se menciona por primera vez en un grupo o canal en lugar de agregarse primero a un equipo.
* Se cambia el nombre del grupo o canal.
* Un miembro del equipo se agrega a un grupo o canal.

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## <a name="step-by-step-guide"></a>Guía paso a paso

Siga la [guía paso a paso](../../../sbs-teams-conversation-bot.yml) para crear un bot conversacional Teams.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Suscribirse a eventos de conversación](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

## <a name="see-also"></a>Consulte también

[Obtención del contexto de Teams para un bot](~/bots/how-to/get-teams-context.md)

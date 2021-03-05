---
title: Conceptos básicos de la conversación
description: describe formas de tener una conversación con un bot de Microsoft Teams
ms.topic: overview
ms.author: anclear
keyword: conversations basics receive message send message picture message channel data adaptive cards
ms.openlocfilehash: 4eba22e9b29f5378dc03480ba5f6ba421f816eb3
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449510"
---
# <a name="conversation-basics"></a>Conceptos básicos de la conversación

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Una conversación es una serie de mensajes enviados entre el bot y uno o más usuarios. Hay tres tipos de conversaciones, también denominadas ámbitos en Teams:

| Tipo de conversación | Descripción |
| ------- | ----------- |
|  `teams` | También se denomina conversaciones de canal, visibles para todos los miembros del canal. |
| `personal` | Conversaciones entre bots y un solo usuario. |
| `groupChat` | Chatear entre un bot y dos o más usuarios. También habilita el bot en chats de reunión. |

Un bot se comporta de forma ligeramente diferente en función del tipo de conversación en la que esté implicado:

* Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.
* Los bots de una conversación uno a uno no requieren una mención @. Todos los mensajes enviados por el usuario se enrutan al bot.

Para habilitar el bot en un ámbito determinado, agrega ese ámbito al manifiesto [de la aplicación.](~/resources/schema/manifest-schema.md)

## <a name="activities"></a>Actividades

Cada mensaje es un `Activity` objeto de tipo `messageType: message` . Cuando un usuario envía un mensaje, Teams publica el mensaje en el bot; específicamente, envía un objeto JSON al punto de conexión de mensajería del bot. El bot examina el mensaje para determinar su tipo y responde en consecuencia.

Las conversaciones básicas se controlan a través de Bot Framework Connector, una única API de REST. Esta API permite que el bot se comunique con Teams y otros canales. El SDK de Bot Builder proporciona acceso fácil a esta API, funcionalidad adicional para administrar el estado y el flujo de conversación, y formas sencillas de incorporar servicios cognitivos como el procesamiento de lenguaje natural (NLP).

## <a name="receive-a-message"></a>Recibir un mensaje

Para recibir un mensaje de texto, use la `Text` propiedad del `Activity` objeto. En el controlador de actividad del bot, use el objeto turn context para `Activity` leer una única solicitud de mensaje.

El código siguiente muestra un ejemplo.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            await context.sendActivity(`Echo: '${context.activity.text}'`);
            await next();
        });
    }
}

```

# <a name="python"></a>[Python](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "type": "message",
    "id": "1485983408511",
    "timestamp": "2017-02-01T21:10:07.437Z",
    "localTimestamp": "2017-02-01T14:10:07.437-07:00",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "channelId": "msteams",
    "from": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB39ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen",
        "aadObjectId": "7faf8ab2-3d56-4244-b585-20c8a42ed2b8"
    },
    "conversation": {
        "conversationType": "personal",
        "id": "a:17I0kl9EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-"
    },
    "recipient": {
        "id": "28:c9e8c047-2a74-40a2-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "textFormat": "plain",
    "text": "Hello Teams TestBot",
    "entities": [
      { 
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo"
      }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

---

## <a name="send-a-message"></a>Enviar un mensaje

Para enviar un mensaje de texto, especifique la cadena que desea enviar como actividad. En el controlador de actividad del bot, use el método del objeto turn context `SendActivityAsync` para enviar una única respuesta de mensaje. Use el método del `SendActivitiesAsync` objeto para enviar varias respuestas a la vez. El código siguiente muestra un ejemplo de envío de un mensaje cuando se agrega alguien a una conversación.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            await context.sendActivity('Hello and welcome!');
            await next();
        });
    }
}
```

# <a name="python"></a>[Python](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "text": "hi",
    "textFormat": "plain",
    "type": "message",
    "timestamp": "2019-10-31T20:57:27.2347285Z",
    "localTimestamp": "2019-10-31T13:57:27.2347285-07:00",
    "id": "1572555447214",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "from": {
        "id": "29:1Xv-kvy4dKirR0rZfSF_kAVUzotoT1SXuEzkC9XGkuZng8YBw8qyu5uh4128fQRjlGgvEiRLx-0XP4KYMwcgdZw",
        "name": "Jane Doe",
        "aadObjectId": "df486eae-88fd-42a5-b45e-c581588186db"
    },
    "conversation": {
        "conversationType": "personal",
        "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
        "id": "a:1oAmWTVBBe9E0JrpGxauqNyx4CCE_iQf2ZuWon9D42722Fon3wYIpbhgbRChE3wgVS1Gwl9zS1pZy4FSu6-x1vGEq5KBQK-EbBgyPyeP_C-lbLBY3vxnGk9m9D_282jbg"
    },
    "recipient": {
        "id": "28:5baea8d1-d4ea-43a1-b101-882f4c8d9cb4",
        "name": "Imported Bot"
    },
    "entities": [
        {
            "locale": "en-US",
            "country": "US",
            "platform": "Windows",
            "type": "clientInfo"
        }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

---

> [!NOTE]
> La división de mensajes se produce cuando se envían un mensaje de texto y datos adjuntos en la misma carga de actividad. Microsoft Teams divide esta actividad en actividades independientes, una actividad con solo un mensaje de texto y otra con datos adjuntos. Como la actividad está dividida, no recibe el identificador de mensaje en respuesta, que se usa para actualizar o [eliminar](~/bots/how-to/update-and-delete-bot-messages.md) el mensaje de forma proactiva. Se recomienda enviar actividades independientes en lugar de depender de la división de mensajes.

## <a name="teams-channel-data"></a>Datos del canal de Teams

El `channelData` objeto contiene información específica de Teams y es un origen definitivo para los IDs de equipo y canal. Es posible que necesite almacenar en caché y usar estos IDs como claves para el almacenamiento local. En `TeamsActivityHandler` el SDK, normalmente se extrae información importante del `channelData` objeto para que sea fácilmente accesible. Sin embargo, siempre puede tener acceso a los datos originales desde el `turnContext` objeto.

El objeto no se incluye en los mensajes de conversaciones personales, ya que se llevan a `channelData` cabo fuera de cualquier canal.

Un objeto channelData típico de una actividad enviada al bot contiene la siguiente información:

* `eventType` Tipo de evento teams; se pasa solo en casos de [eventos de modificación de canal](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* `tenant.id` Identificador de inquilino de Azure Active Directory, pasado en todos los contextos.
* `team` Se pasa solo en contextos de canal, no en chat personal.
  * `id` GUID del canal.
  * `name`Nombre del equipo; se pasa solo en casos de [eventos de cambio de nombre de equipo.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* `channel` Se pasa solo en contextos de canal cuando se menciona el bot o para eventos en canales de equipos donde se ha agregado el bot.
  * `id` GUID del canal.
  * `name` Nombre del canal; se pasa solo en casos de [eventos de modificación de canal](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* `channelData.teamsTeamId` En desuso. Esta propiedad se incluye solo por compatibilidad con versiones anteriores.
* `channelData.teamsChannelId` En desuso. Esta propiedad se incluye solo por compatibilidad con versiones anteriores.

### <a name="example-channeldata-object-channelcreated-event"></a>Objeto channelData de ejemplo (evento channelCreated)

```json
"channelData": {
    "eventType": "channelCreated",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    },
    "channel": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype",
        "name": "My New Channel"
    },
    "team": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype"
    }
}
```

## <a name="message-content"></a>Contenido del mensaje

El bot puede enviar texto enriquecido, imágenes y tarjetas. Los usuarios pueden enviar texto enriquecido e imágenes al bot.

| Formato    | De usuario a bot | De bot a usuario | Notas                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| Texto enriquecido  | ✔                | ✔                |                                                                                         |
| Imágenes  | ✔                | ✔                | Máximo 1024×1024 y 1 MB en formato PNG, JPEG o GIF; GIF animado no se admite  |
| Tarjetas     | ✖                | ✔                | Consulta referencia [de tarjetas de Teams](~/task-modules-and-cards/cards/cards-reference.md) para obtener tarjetas compatibles |
| Emojis    | ✖                | ✔                | Teams actualmente admite emojis a través de UTF-16 (como U+1F600 para la cara sonriente)          |

## <a name="adding-notifications-to-your-message"></a>Agregar notificaciones al mensaje

Las notificaciones alertan a los usuarios sobre nuevas tareas, menciones y comentarios relacionados con lo que están trabajando o necesitan ver insertando un aviso en su fuente de actividad. Puede establecer las notificaciones para que se desencadene desde el bot-message estableciendo la `TeamsChannelData` propiedad `Notification.Alert` objects en true. La generación o no de una notificación depende en última instancia de la configuración de Teams del usuario individual y no se puede invalidar mediante programación esta configuración. El tipo de notificación es un banner o un banner y un correo electrónico.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[Python](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "type": "message",
  "timestamp": "2017-04-24T21:46:00.9663655Z",
  "localTimestamp": "2017-04-24T14:46:00.9663655-07:00",
  "serviceUrl": "https://callback.com",
  "channelId": "msteams",
  "from": {
    "id": "28:e4fda94a-4b80-40eb-9bf0-6314491bc793",
    "name": "The bot"
  },
  "conversation": {
    "id": "a:1pL6i0oY3C0K8oAj8"
  },
  "recipient": {
    "id": "29:1rsVJmSSFMScF0YFyCXpvNWlo",
    "name": "User"
  },
  "text": "John Phillips assigned you a weekly todo",
  "summary": "Don't forget to meet with Marketing next week",
  "channelData": {
    "notification": {
      "alert": true
    }
  },
  "replyToId": "1493070356924"
}
```

---

## <a name="picture-messages"></a>Mensajes de imagen

Las imágenes se envían agregando datos adjuntos a un mensaje. Encontrará más información sobre los datos adjuntos en la [documentación de Bot Framework](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments).

Las imágenes pueden tener como máximo 1024×1024 y 1 MB en formato PNG, JPEG o GIF. Gif animado no es compatible.

Especifique siempre el alto y el ancho de cada imagen mediante XML. En Markdown, el tamaño de imagen es 256×256. Por ejemplo:

* Usar - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* No usar - `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="adaptive-cards"></a>Tarjetas adaptables

Use el siguiente código para enviar una tarjeta adaptable sencilla:

```json
{
    "type": "AdaptiveCard",
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.5",
    "body": [
    {
        "items": [
        {
            "size": "large",
            "text": " Simple Adaptivecard Example with a Textbox",
            "type": "TextBlock",
            "weight": "bolder",
            "wrap": true
        },
        ],
        "spacing": "extraLarge",
        "type": "Container",
        "verticalContentAlignment": "center"
    }
    ]
}
```

Para obtener más información acerca de las tarjetas y las tarjetas de los bots, consulte [la documentación sobre tarjetas](~/task-modules-and-cards/what-are-cards.md).

## <a name="code-sample"></a>Ejemplo de código

|**Nombre de ejemplo** | **Descripción** | **. NETCore** | **JavaScript** | **Python**|
|----------------|-----------------|--------------|----------------|-----------|
| Bot de conversación de Teams | Control de eventos de mensajería y conversación. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-steps"></a>Siguientes pasos

* [Envío de mensajes proactivos](~/bots/how-to/conversations/send-proactive-messages.md)
* [Suscribirse a eventos de conversación](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

---
title: Mensajes en conversaciones de bot
description: Describe formas de tener una conversación con un Microsoft Teams bot
ms.topic: overview
ms.author: anclear
localization_priority: Normal
keyword: receive message send message picture message channel data adaptive cards
ms.openlocfilehash: 5b23e3b2548e3d0eab98fae73d37316063fe60c1
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058603"
---
# <a name="messages-in-bot-conversations"></a>Mensajes en conversaciones de bot

Cada mensaje de una conversación es un `Activity` objeto de tipo `messageType: message` . Cuando un usuario envía un mensaje, Teams el mensaje al bot. Teams envía un objeto JSON al extremo de mensajería del bot. El bot examina el mensaje para determinar su tipo y responde en consecuencia.

Las conversaciones básicas se controlan a través del conector de Bot Framework, una única API de REST. Esta API permite que el bot se comunique con Teams y otros canales. El SDK de Bot Builder proporciona las siguientes características:

* Fácil acceso al conector de Bot Framework.
* Funcionalidad adicional para administrar el estado y el flujo de conversación.
* Formas sencillas de incorporar servicios cognitivos, como el procesamiento de lenguaje natural (NLP).

El bot recibe mensajes de Teams mediante la propiedad y envía una o varias respuestas de `Text` mensaje a los usuarios.

## <a name="receive-a-message"></a>Recibir un mensaje

Para recibir un mensaje de texto, use la propiedad `Text` del objeto `Activity`. En el controlador de actividades del bot, use convertir `Activity` del objeto de contexto para leer una solicitud de mensaje única.

El siguiente código muestra un ejemplo de recepción de un mensaje:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

Para enviar un mensaje de texto, especifique la string que desee enviar como actividad. En el controlador de actividad del bot, use el método del objeto turn context `SendActivityAsync` para enviar una única respuesta de mensaje. Use el método del `SendActivitiesAsync` objeto para enviar varias respuestas a la vez.

El siguiente código muestra un ejemplo de envío de un mensaje cuando se agrega un usuario a una conversación:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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
> La división de mensajes se produce cuando se envían un mensaje de texto y datos adjuntos en la misma carga de actividad. Esta actividad se divide en actividades independientes por Microsoft Teams, una con solo un mensaje de texto y otra con datos adjuntos. Como la actividad está dividida, no recibe el identificador de mensaje en respuesta, que se usa para actualizar o [eliminar](~/bots/how-to/update-and-delete-bot-messages.md) el mensaje de forma proactiva. Se recomienda enviar actividades independientes en lugar de depender de la división de mensajes.

Los mensajes enviados entre usuarios y bots incluyen datos de canal internos dentro del mensaje. Estos datos permiten al bot comunicarse correctamente en ese canal. El SDK del generador de bots permite modificar la estructura del mensaje.

## <a name="teams-channel-data"></a>Teams de canal

El objeto contiene Teams información específica y es un origen definitivo para `channelData` los IDs de equipo y canal. Opcionalmente, puede almacenar en caché y usar estos IDs como claves para el almacenamiento local. El SDK extrae información importante del objeto para que `TeamsActivityHandler` `channelData` sea fácilmente accesible. Sin embargo, siempre puede tener acceso a los datos originales desde el `turnContext` objeto.

El objeto no se incluye en los mensajes de conversaciones personales, ya que tienen lugar `channelData` fuera de un canal.

Un objeto `channelData` típico de una actividad enviada al bot contiene la siguiente información:

* `eventType`: Teams tipo de evento pasado solo en casos de [eventos de modificación de canal](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* `tenant.id`: Azure Active Directory de inquilino pasado en todos los contextos.
* `team`: Se pasa solo en contextos de canal, no en chat personal.
  * `id`: GUID para el canal.
  * `name`: Nombre del equipo pasado solo en casos de [eventos de cambio de nombre de equipo](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* `channel`: Se pasa solo en contextos de canal cuando se menciona el bot o para eventos en canales de equipos donde se ha agregado el bot.
  * `id`: GUID para el canal.
  * `name`: Nombre del canal pasado solo en casos de [eventos de modificación de canal](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* `channelData.teamsTeamId`: En desuso. Esta propiedad solo se incluye por compatibilidad con versiones anteriores.
* `channelData.teamsChannelId`: En desuso. Esta propiedad solo se incluye por compatibilidad con versiones anteriores.

### <a name="example-channeldata-object-or-channelcreated-event"></a>Evento channelData de ejemplo o channelCreated

El siguiente código muestra un ejemplo del objeto channelData:

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

Los mensajes recibidos o enviados al bot pueden incluir diferentes tipos de contenido de mensaje.

## <a name="message-content"></a>Contenido del mensaje

| Formato    | De usuario a bot | De bot a usuario | Notas                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| Texto enriquecido  | ✔                | ✔                | El bot puede enviar texto enriquecido, imágenes y tarjetas. Los usuarios pueden enviar texto enriquecido e imágenes al bot.                                                                                        |
| Imágenes  | ✔                | ✔                | Máximo 1024×1024 y 1 MB en formato PNG, JPEG o GIF. Gif animado no es compatible.  |
| Tarjetas     | ✖                | ✔                | Consulta la [referencia Teams tarjeta para](~/task-modules-and-cards/cards/cards-reference.md) las tarjetas admitidas. |
| Emojis    | ✖                | ✔                | Teams admite emojis a través de UTF-16, como U+1F600 para la cara sonriente. |

También puede agregar notificaciones al mensaje mediante la `Notification.Alert` propiedad.

## <a name="notifications-to-your-message"></a>Notificaciones al mensaje

Las notificaciones alertan a los usuarios sobre nuevas tareas, menciones y comentarios. Estas alertas están relacionadas con lo que los usuarios están trabajando o lo que deben ver insertando un aviso en su fuente de actividad. Para que las notificaciones se desencadene desde el mensaje del bot, establezca la `TeamsChannelData` propiedad objects en `Notification.Alert` *true*. Si se genera o no una notificación depende de la configuración de Teams usuario individual y no se puede invalidar esta configuración. El tipo de notificación es un banner o un banner y un correo electrónico.

> [!NOTE]
> El **campo Resumen** muestra cualquier texto del usuario como un mensaje de notificación en la fuente.

El siguiente código muestra un ejemplo de cómo agregar notificaciones al mensaje:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

Para mejorar el mensaje, puede incluir imágenes como datos adjuntos a ese mensaje.

## <a name="picture-messages"></a>Mensajes de imagen

Las imágenes se envían agregando datos adjuntos a un mensaje. Para obtener más información sobre los datos [adjuntos,](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)consulte Bot Framework documentation .

Las imágenes pueden tener como máximo 1024×1024 y 1 MB en formato PNG, JPEG o GIF. Gif animado no es compatible.

Especifique el alto y el ancho de cada imagen mediante XML. En markdown, el tamaño de imagen es predeterminado 256×256. Por ejemplo:

* Use: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>` .
* No usar: `![Duck on a rock](http://aka.ms/Fo983c)` .

Un bot conversacional puede incluir tarjetas adaptables que simplifican los flujos de trabajo empresariales. Las tarjetas adaptables ofrecen texto personalizable enriquecido, voz, imágenes, botones y campos de entrada.

## <a name="adaptive-cards"></a>Tarjetas adaptables

Las tarjetas adaptables se pueden crear en un bot y mostrarse en varias aplicaciones, como Teams, el sitio web, y así sucesivamente. Para obtener más información, vea [Adaptive Cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card).

El siguiente código muestra un ejemplo de envío de una tarjeta adaptable sencilla:

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

## <a name="status-code-responses"></a>Respuestas de código de estado

A continuación se desenván los códigos de estado y sus valores de mensaje y código de error:

| Código de estado | Código de error y valores de mensaje | Descripción |
|----------------|-----------------|-----------------|
| 403 | **Código**: `ConversationBlockedByUser` <br/> **Mensaje:** El usuario bloqueó la conversación con el bot. | El usuario bloqueó el bot en un chat 1:1 o un canal mediante la configuración de moderación. |
| 403 | **Código**: `BotNotInConversationRoster` <br/> **Mensaje:** el bot no forma parte de la lista de conversaciones. | El bot no forma parte de la conversación. |
| 403 | **Código**: `BotDisabledByAdmin` <br/> **Mensaje:** el administrador de inquilinos deshabilitó este bot. | El inquilino bloqueó el bot. |
| 401 | **Código**: `BotNotRegistered` <br/> **Mensaje:** no se encontró ningún registro para este bot. | No se encontró el registro de este bot. |
| 412 | **Código**: `PreconditionFailed` <br/> **Mensaje**: Error en la condición previa, inténtelo de nuevo. | Error en una de nuestras dependencias debido a varias operaciones simultáneas en la misma conversación. |
| 404 | **Código**: `ConversationNotFound` <br/> **Mensaje:** No se encontró la conversación. | No se encontró la conversación. |
| 413 | **Código**: `MessageSizeTooBig` <br/> **Mensaje:** Tamaño del mensaje demasiado grande. | El tamaño de la solicitud entrante era demasiado grande. |
| 429 | **Código**: `Throttled` <br/> **Mensaje:** Demasiadas solicitudes. También devuelve cuándo reintentar después. | El bot envió demasiadas solicitudes. Para obtener más información, vea [rate limit](~/bots/how-to/rate-limit.md). |

## <a name="code-sample"></a>Ejemplo de código

|Nombre de ejemplo | Descripción | . NETCore | Node.js | Python |
|----------------|-----------------|--------------|----------------|-----------|
| Bot de conversación de Teams | Control de eventos de mensajería y conversación. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="see-also"></a>Consulte también

- [Enviar mensajes proactivos](~/bots/how-to/conversations/send-proactive-messages.md)

- [Suscribirse a eventos de conversación](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Menús de comandos bot](~/bots/how-to/create-a-bot-commands-menu.md)

---
title: Conceptos básicos de la conversación
author: clearab
description: Cómo tener una conversación con un bot de Microsoft Teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2d241ad04509c596e97647138bab2a749fa0f74c
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675854"
---
# <a name="conversation-basics"></a>Conceptos básicos de la conversación

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Una conversación es una serie de mensajes enviados entre el bot y uno o más usuarios. Hay tres tipos de conversaciones (también denominadas ámbitos) en Microsoft Teams:

* `teams`También se denominan conversaciones de canal, visibles para todos los miembros del canal.
* `personal`Conversaciones entre bots y un único usuario.
* `groupChat`Chatear entre un bot y dos o más usuarios. También habilita el bot en los chats de reuniones.

Un bot tiene un comportamiento ligeramente diferente en función del tipo de conversación en el que esté involucrado:

* Los bots en conversaciones de chat en el grupo y en el canal requieren al usuario que mencione el bot para invocarlo en un canal.
* Los bots de una conversación uno a uno no requieren @ mención. Todos los mensajes enviados por el usuario se enrutarán a su bot.

Para habilitar el bot en un ámbito determinado, agregue ese ámbito al manifiesto de la [aplicación](~/resources/schema/manifest-schema.md).

## <a name="activities"></a>Actividades

Cada mensaje es un `Activity` objeto de tipo `messageType: message`. Cuando un usuario envía un mensaje, Microsoft Teams expone el mensaje a su bot; en concreto, envía un objeto JSON al extremo de mensajería de bot. El bot examina el mensaje para determinar su tipo y responde en consecuencia.

La conversación básica se controla a través del conector de bot Framework, una única API de REST para permitir que su bot se comunique con Microsoft Teams y otros canales. El SDK de bot Builder proporciona acceso sencillo a esta API, funcionalidad adicional para administrar el flujo de conversaciones y el estado, y formas sencillas de incorporar servicios cognitivos como el procesamiento de lenguaje natural (NLP).

## <a name="receive-a-message"></a>Recibir un mensaje

Para recibir un mensaje de texto, use `Text` la propiedad del `Activity` objeto. En el controlador de actividad del bot, use el objeto convertir contexto `Activity` para leer una única solicitud de mensaje.

El código siguiente muestra un ejemplo.

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node. js](#tab/typescript)

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

# <a name="pythontabpython"></a>[Python](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="jsontabjson"></a>[JSON](#tab/json)

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

Para enviar un mensaje de texto, especifique la cadena que desea enviar como la actividad. En los controladores de actividad del bot, use el método Turn context `SendActivityAsync` del objeto para enviar una respuesta de mensaje único. También puede usar el método del `SendActivitiesAsync` objeto para enviar varias respuestas a la vez. El siguiente código muestra un ejemplo de cómo enviar un mensaje cuando alguien se agrega a una conversación  

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node. js](#tab/typescript)

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

# <a name="pythontabpython"></a>[Python](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="jsontabjson"></a>[JSON](#tab/json)

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

## <a name="teams-channel-data"></a>Datos del canal de Teams

El `channelData` objeto contiene información específica de Microsoft Teams y es la fuente definitiva de los identificadores de equipo y de canal. Es posible que necesite almacenar en caché y usar estos identificadores como claves para el almacenamiento local. La `TeamsActivityHandler` en el SDK suele extraer información importante del `channelData` objeto para que sea más fácil de acceder, pero siempre puede tener acceso a la información original del `turnContext` objeto.

El `channelData` objeto no está incluido en los mensajes de las conversaciones personales, ya que éstos tienen lugar fuera de cualquier canal.

Un objeto channelData típico de una actividad enviada a su bot contiene la siguiente información:

* `eventType`Tipo de evento de Teams; solo se pasa en casos de [eventos de modificación de canal](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* `tenant.id`IDENTIFICADOR de inquilino de Azure Active Directory; se pasan en todos los contextos
* `team`Solo se pasa en contextos de canal, no en chat personal.
  * `id`GUID para el canal
  * `name`Nombre del equipo; solo se pasa en casos de [eventos de cambio de nombre de equipo](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* `channel`Solo se pasa en contextos de canal cuando se menciona el bot o para eventos en los canales en equipos en los que se ha agregado el bot
  * `id`GUID para el canal
  * `name`Nombre del canal; se pasa solo en casos de [eventos de modificación de canal](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* `channelData.teamsTeamId`En desuso. Esta propiedad se incluye únicamente para la compatibilidad con versiones anteriores.
* `channelData.teamsChannelId`En desuso. Esta propiedad se incluye únicamente para la compatibilidad con versiones anteriores.

### <a name="example-channeldata-object-channelcreated-event"></a>Ejemplo de objeto channelData (evento channelCreated)

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

El bot puede enviar texto enriquecido, imágenes y tarjetas. Los usuarios pueden enviar texto enriquecido e imágenes a su bot.

| Formato    | De un usuario a un bot | De bot a User | Notas                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| Texto enriquecido  | ✔                | ✔                |                                                                                         |
| Imágenes  | ✔                | ✔                | Máximo de 1024 × 1024 y 1 MB en formato PNG, JPEG o GIF; no se admiten GIF animados  |
| Tarjetas     | ✖                | ✔                | Ver la [referencia de la tarjeta Teams](~/task-modules-and-cards/cards/cards-reference.md) para tarjetas compatibles |
| Emojis    | ✖                | ✔                | Actualmente, los equipos son compatibles con emojis mediante UTF-16 (como U + 1F600 para la cara Grinning).          |

## <a name="adding-notifications-to-your-message"></a>Adición de notificaciones al mensaje

Las notificaciones alertan a los usuarios sobre nuevas tareas, menciones y comentarios relacionados con el trabajo en el que están trabajando, o bien deben consultarse mediante la inserción de un aviso en su fuente de actividades. Puede establecer notificaciones para que desencadenen desde el mensaje de bot estableciendo la `TeamsChannelData` propiedad `Notification.Alert` Objects en true. El hecho de que se genere una notificación dependerá en última instancia de la configuración de Teams del usuario individual y no podrá reemplazar esta configuración mediante programación. El tipo de notificación será un banner, un banner o un correo electrónico.

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node. js](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="pythontabpython"></a>[Python](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="jsontabjson"></a>[JSON](#tab/json)

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

Las imágenes se envían agregando datos adjuntos a un mensaje. Puede encontrar más información sobre los datos adjuntos en la [documentación de bot Framework](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0).

Las imágenes pueden tener como máximo 1024 x 1024 y 1 MB en formato PNG, JPEG o GIF; GIF animado no es compatible.

Le recomendamos que especifique el alto y el ancho de cada imagen utilizando XML. Si usa Markdown, el tamaño de imagen predeterminado es de 256 × 256. Por ejemplo:

* Utilizados`<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* No use-`![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="next-steps"></a>Siguientes pasos

* [Envío de mensajes proactivos](~/bots/how-to/conversations/send-proactive-messages.md)
* [Suscribirse a eventos de conversación](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

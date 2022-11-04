---
title: Mensajes en conversaciones de bot
description: Obtenga información sobre cómo enviar un mensaje, acciones sugeridas, notificación, datos adjuntos, imágenes, tarjeta adaptable y respuestas de código de error de estado.
ms.topic: overview
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: 16849a9e8ed97854e91934aef9de463eb355fec5
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833208"
---
# <a name="messages-in-bot-conversations"></a>Mensajes en conversaciones de bot

Cada mensaje de una conversación es un `Activity` objeto de tipo `messageType: message`. Cuando un usuario envía un mensaje, Microsoft Teams publica el mensaje en el bot. Teams envía un objeto JSON al punto de conexión de mensajería del bot y Teams solo permite un punto de conexión para la mensajería. El bot examina el mensaje para determinar su tipo y responder correctamente.

Las conversaciones básicas se controlan a través del conector de Bot Framework, una única API REST. Esta API permite que el bot se comunique con Teams y otros canales. El SDK de Bot Builder proporciona las siguientes características:

* Fácil acceso al conector de Bot Framework.
* Funcionalidad para administrar el flujo y el estado de la conversación.
* Formas sencillas de incorporar servicios cognitivos, como el procesamiento de lenguaje natural (NLP).

El bot recibe mensajes de Teams mediante la `Text` propiedad y envía una o varias respuestas de mensaje a los usuarios.

Para obtener más información, consulte [atribución de usuarios para mensajes de bot](/microsoftteams/platform/messaging-extensions/how-to/action-commands/respond-to-task-module-submit?tabs=dotnet%2Cdotnet-1&branch=pr-en-us-5926#user-attribution-for-bots-messages).

## <a name="receive-a-message"></a>Recibir un mensaje

Para recibir un mensaje de texto, use la `Text` propiedad de un `Activity` objeto . En el controlador de actividades del bot, use convertir `Activity` del objeto de contexto para leer una solicitud de mensaje única.

En el código siguiente se muestra un ejemplo de recepción de un mensaje:

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
    "text": "Hello Teams TestBot.Sending bold-italic rich text",
    "attachments": [
      {
            "contentType": "text/html",
            "content": "<div><div>Hello Teams TestBot. Sending <strong>bold</strong>-<em>italic</em> rich text.</div>\n</div>"
      } 
    ],
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

Para enviar un mensaje de texto, especifique la cadena que desea enviar como actividad. En el controlador de actividad del bot, use el método del objeto de contexto turn `SendActivityAsync` para enviar una única respuesta de mensaje. Use el método del `SendActivitiesAsync` objeto para enviar varias respuestas.

En el código siguiente se muestra un ejemplo de envío de un mensaje cuando se agrega un usuario a una conversación:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript

    this.onMembersAddedActivity(async (context, next) => {
        await Promise.all((context.activity.membersAdded || []).map(async (member) => {
            if (member.id !== context.activity.recipient.id) {
                await context.sendActivity(
                    `Welcome to the team ${member.givenName} ${member.surname}`
                );
            }
        }));

        await next();
    });
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
    "type": "message",
    "from": {
        "id": "28:c9e8c047-2a34-40a1-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "conversation": {
        "id": "a:17I0kl8EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-",
        "name": "Convo1"
   },
   "recipient": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB25ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen"
    },
    "text": "My bot's reply",
    "replyToId": "1632474074231"
}

```

---

> [!NOTE]
>
>* La división de mensajes se produce cuando se envían un mensaje de texto y datos adjuntos en la misma carga de actividad. Teams divide esta actividad en dos actividades independientes, una con un mensaje de texto y la otra con datos adjuntos. A medida que se divide la actividad, no recibe el identificador de mensaje en respuesta, que se usa para [actualizar o eliminar](~/bots/how-to/update-and-delete-bot-messages.md) el mensaje de forma proactiva. Se recomienda enviar actividades independientes en lugar de depender de la división de mensajes.
>* Los mensajes enviados se pueden localizar para proporcionar personalización. Para obtener más información, consulte [Localización de la aplicación](../../../concepts/build-and-test/apps-localization.md).

Los mensajes enviados entre usuarios y bots incluyen datos de canal internos dentro del mensaje. Estos datos permiten que el bot se comunique correctamente en ese canal. El SDK de Bot Builder permite modificar la estructura del mensaje.

## <a name="send-suggested-actions"></a>Envío de acciones sugeridas

Las acciones sugeridas permiten al bot presentar botones que el usuario puede seleccionar para proporcionar entrada. Las acciones sugeridas mejoran la experiencia del usuario al permitir que el usuario responda a una pregunta o haga una elección con la selección de un botón, en lugar de escribir una respuesta con un teclado.
Cuando el usuario selecciona un botón, permanece visible y accesible en las tarjetas enriquecidas, pero no para las acciones sugeridas. Esto impide que el usuario seleccione botones obsoletos dentro de una conversación.

Para agregar acciones sugeridas a un mensaje, establezca la `suggestedActions` propiedad de un objeto de [actividad](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference) para especificar la lista de objetos de [acción de tarjeta](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference) que representan los botones que se van a presentar al usuario. Para obtener más información, consulte [`sugestedActions`](/dotnet/api/microsoft.bot.builder.messagefactory.suggestedactions).

A continuación se muestra un ejemplo de implementación y experiencia de acciones sugeridas:

``` json
"suggestedActions": {
    "actions": [
      {
        "type": "imBack",
        "title": "Action 1",
        "value": "Action 1"
      },
      {
        "type": "imBack",
        "title": "Action 2",
        "value": "Action 2"
      }
    ],
    "to": [<list of recepientIds>]
  }
```

A continuación se muestra un ejemplo de acciones sugeridas:

:::image type="content" source="~/assets/images/Cards/suggested-actions.png" alt-text="Acciones sugeridas por bot" border="true":::

> [!NOTE]
>
> * `SuggestedActions` solo se admiten para bots de chat uno a uno y mensajes basados en texto y no para tarjetas adaptables o datos adjuntos.
> * `imBack` es el único tipo de acción admitido y Teams muestra hasta tres acciones sugeridas.

## <a name="teams-channel-data"></a>Datos del canal de Teams

El `channelData` objeto contiene información específica de Teams y es un origen definitivo para los identificadores de equipo y canal. Opcionalmente, puede almacenar en caché y usar estos identificadores como claves para el almacenamiento local. en `TeamsActivityHandler` el SDK extrae información importante del `channelData` objeto para que sea accesible. Sin embargo, siempre puede acceder a los datos originales desde el `turnContext` objeto .

El `channelData` objeto no se incluye en los mensajes de las conversaciones personales, ya que tienen lugar fuera de un canal.

Un objeto típico `channelData` de una actividad enviada al bot contiene la siguiente información:

* `eventType`: el tipo de evento de Teams solo se pasa en los casos de [eventos de modificación del canal](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* `tenant.id`: Microsoft Azure Active Directory identificador de inquilino (Azure AD) pasado en todos los contextos.
* `team`: solo se pasa en contextos de canal, no en chat personal.
  * `id`: GUID para el canal.
  * `name`: nombre del equipo pasado solo en los casos de [eventos de cambio de nombre del equipo](subscribe-to-conversation-events.md#team-renamed).
* `channel`: solo se pasa en contextos de canal, cuando se menciona el bot o para eventos en canales de teams, donde se ha agregado el bot.
  * `id`: GUID para el canal.
  * `name`: el nombre del canal solo se pasa en los casos de [eventos de modificación del canal](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* `channelData.teamsTeamId`:Obsoleto. Esta propiedad solo se incluye por compatibilidad con versiones anteriores.
* `channelData.teamsChannelId`:Obsoleto. Esta propiedad solo se incluye por compatibilidad con versiones anteriores.

### <a name="example-channeldata-object-channelcreated-event"></a>Ejemplo de objeto channelData (evento channelCreated)

En el código siguiente se muestra un ejemplo del objeto channelData:

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

Los mensajes recibidos o enviados al bot pueden incluir diferentes tipos de contenido de mensaje.

| Formato    | De usuario a bot | De bot a usuario | Notas                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| Texto enriquecido  | ✔️                | ✔️                | El bot puede enviar texto enriquecido, imágenes y tarjetas. Los usuarios pueden enviar texto enriquecido e imágenes al bot.                                                                                        |
| Imágenes  | ✔️                | ✔️                | Máximo 1024 × 1024 píxeles y 1 MB en formato PNG, JPEG o GIF. No admite el GIF animado. |
| Tarjetas     | ❌                | ✔️                | Consulte [Referencia de tarjetas de Teams](~/task-modules-and-cards/cards/cards-reference.md) para obtener las tarjetas admitidas. |
| Emojis    | ✔️                | ✔️                | Teams admite actualmente emojis a través de UTF-16, como U+1F600 para la cara sonriente. |

### <a name="picture-messages"></a>Mensajes de imagen

Para mejorar el mensaje, puede incluir imágenes como datos adjuntos a ese mensaje. Para obtener más información sobre los datos adjuntos, vea [Agregar datos adjuntos multimedia a los mensajes](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments).

Las imágenes pueden tener como máximo 1024 × 1024 píxeles y 1 MB en formato PNG, JPEG o GIF. No se admite el uso de un GIF animado.

Especifique el alto y el ancho de cada imagen mediante XML. En Markdown, el tamaño predeterminado de la imagen es 256×256. Por ejemplo:

* Use: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`.
* No use: `![Duck on a rock](http://aka.ms/Fo983c)`.

Un bot conversacional puede incluir tarjetas adaptables que simplifican los flujos de trabajo empresariales. Las tarjetas adaptables ofrecen texto personalizable enriquecido, voz, imágenes, botones y campos de entrada.

### <a name="adaptive-cards"></a>Tarjetas adaptables

Las tarjetas adaptables se pueden crear en un bot y mostrarse en varias aplicaciones, como Teams, su sitio web, etc. Para obtener más información, vea [Tarjetas adaptables](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card).

En el código siguiente se muestra un ejemplo de envío de una tarjeta adaptable simple:

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

#### <a name="form-completion-feedback"></a>Comentarios de finalización de formularios

Puede generar comentarios de finalización de formularios mediante una tarjeta adaptable. El mensaje de finalización del formulario aparece en Tarjetas adaptables al enviar una respuesta al bot. El mensaje puede ser de dos tipos, error o éxito:

* **Error**: Cuando se produce un error en una respuesta enviada al bot, **se produce un error, aparece el mensaje Volver a intentarlo** .

     :::image type="content" source="../../../assets/images/Cards/error-message.png" alt-text="Mensaje de error"border="true":::

* **Correcto**: cuando una respuesta enviada al bot se realiza correctamente, aparece **la respuesta que se envió al mensaje de la aplicación** .

     :::image type="content" source="../../../assets/images/Cards/success.PNG" alt-text="Mensaje de correcto"border="true":::

     Puede seleccionar **Cerrar** o cambiar el chat para descartar el mensaje.

     Si no desea mostrar el mensaje correcto, establezca el atributo `hide` `true` en en la `msTeams` `feedback` propiedad . A continuación se muestra un ejemplo:

     ```json
        "content": {
            "type": "AdaptiveCard",
            "title": "Card with hidden footer messages",
            "version": "1.0",
            "actions": [
            {
                "type": "Action.Submit",
                "title": "Submit",
                "msTeams": {
                    "feedback": {
                    "hide": true
                    }
                }
            }
            ]
        } 
     ```

Para obtener más información sobre tarjetas y tarjetas en bots, consulte [la documentación de las tarjetas](~/task-modules-and-cards/what-are-cards.md).

## <a name="add-notifications-to-your-message"></a>Adición de notificaciones al mensaje

Hay dos maneras de enviar una notificación desde la aplicación:

* Al establecer la propiedad en el `Notification.Alert` mensaje del bot.
* Mediante el envío de una notificación de fuente de actividad mediante el Graph API.

Puede agregar notificaciones al mensaje mediante la `Notification.Alert` propiedad . Las notificaciones alertan a los usuarios de un evento en la aplicación, como nuevas tareas, menciones o comentarios. Estas alertas están relacionadas con lo que los usuarios están trabajando o con lo que deben examinar insertando un aviso en su fuente de actividad. Para que las notificaciones se desencadenen desde el mensaje del bot, establezca la `TeamsChannelData` propiedad objects `Notification.Alert` en *true*. Si se genera una notificación depende de la configuración de Teams del usuario individual y no puede invalidar esta configuración.

Si desea generar una notificación arbitraria sin enviar un mensaje al usuario, puede usar el Graph API. Para obtener más información, consulte [cómo enviar notificaciones de fuente de actividad mediante Graph API](/graph/teams-send-activityfeednotifications) junto con los [procedimientos recomendados](/graph/teams-activity-feed-notifications-best-practices).

> [!NOTE]
> El campo **Resumen** muestra cualquier texto del usuario como mensaje de notificación en la fuente.

En el código siguiente se muestra un ejemplo de cómo agregar notificaciones al mensaje:

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

## <a name="status-codes-from-bot-conversational-apis"></a>Códigos de estado de las API conversacionales del bot

Asegúrese de controlar estos errores correctamente en la aplicación de Teams. En la tabla siguiente se enumeran los códigos de error y las descripciones con las que se generan los errores:

| Código de estado | Código de error y valores de mensaje | Descripción | Solicitud de reintento | Acción del desarrollador |
|----------------|-----------------|-----------------|----------------|----------------|
| 400 | **Código**: `Bad Argument` <br/> **Mensaje**: *específico del escenario | Carga de solicitud no válida proporcionada por el bot. Consulte el mensaje de error para obtener detalles específicos. | No | Vuelva a evaluar la carga de la solicitud para ver si hay errores. Compruebe el mensaje de error devuelto para obtener más información. |
| 401 | **Código**: `BotNotRegistered` <br/> **Mensaje**: No se encontró ningún registro para este bot. | No se encontró el registro de este bot. | No | Compruebe el identificador y la contraseña del bot. Asegúrese de que el identificador del bot (id. de AAD) está registrado en el Portal para desarrolladores de Teams o mediante el registro del canal de bot de Azure en Azure con el canal "Teams" habilitado.|
| 403 | **Código**: `BotDisabledByAdmin` <br/> **Mensaje**: El administrador de inquilinos deshabilitó este bot | El administrador de inquilinos ha bloqueado las interacciones entre el usuario y la aplicación del bot. El administrador de inquilinos debe permitir la aplicación para el usuario dentro de las directivas de la aplicación. Para obtener más información, consulte [Directivas de aplicación](/microsoftteams/app-policies). | No | Deje de publicar en la conversación hasta que un usuario inicie explícitamente la interacción con el bot en la conversación, lo que indica que el bot ya no está bloqueado. |
| 403 | **Código**: `BotNotInConversationRoster` <br/> **Mensaje**: El bot no forma parte de la lista de conversaciones. | El bot no forma parte de la conversación. La aplicación debe volver a instalarse en la conversación. | No | Antes de intentar enviar otra solicitud de conversación, espere un [`installationUpdate`](~/bots/how-to/conversations/subscribe-to-conversation-events.md#install-update-event) evento, lo que indica que el bot se ha vuelto a agregar.|
| 403 | **Código**: `ConversationBlockedByUser` <br/> **Mensaje**: El usuario bloqueó la conversación con el bot. | El usuario ha bloqueado el bot en un chat personal o un canal a través de la configuración de moderación. | No | Elimine la conversación de la memoria caché. Deje de intentar publicar en las conversaciones hasta que un usuario inicie explícitamente la interacción con el bot en la conversación, lo que indica que el bot ya no está bloqueado. |
| 403 |**Código**: `InvalidBotApiHost` <br/> **Mensaje**: Host de api de bot no válido. Para los inquilinos de GCC, llame a `https://smba.infra.gcc.teams.microsoft.com`.|El bot llamó al punto de conexión de API público para una conversación que pertenece a un inquilino de GCC.| No | Actualice la dirección URL del servicio de la conversación a y vuelva a `https://smba.infra.gcc.teams.microsoft.com` intentar la solicitud.|
| 403 | **Código**: `NotEnoughPermissions` <br/> **Mensaje**: *específico del escenario | El bot no tiene los permisos necesarios para realizar la acción solicitada. | No | Determine la acción necesaria del mensaje de error. |
| 404 | **Código**: `ActivityNotFoundInConversation` <br/> **Mensaje**: No se encontró la conversación. | No se encontró el identificador de mensaje proporcionado en la conversación. El mensaje no existe o se ha eliminado. | No | Compruebe si el identificador de mensaje enviado es un valor esperado. Quite el identificador si se ha almacenado en caché. |
| 404 | **Código**: `ConversationNotFound` <br/> **Mensaje**: No se encontró la conversación. | No se encontró la conversación, ya que no existe o se ha eliminado. | No | Compruebe si el identificador de conversación enviado es un valor esperado. Quite el identificador si se ha almacenado en caché. |
| 412 | **Código**: `PreconditionFailed` <br/> **Mensaje**: Error de condición previa, inténtelo de nuevo. | Error de condición previa en una de nuestras dependencias debido a varias operaciones simultáneas en la misma conversación. | Sí | Vuelva a intentarlo con retroceso exponencial. |
| 413 | **Código**: `MessageSizeTooBig` <br/> **Mensaje**: tamaño del mensaje demasiado grande. | El tamaño de la solicitud entrante era demasiado grande. Para obtener más información, consulte [Dar formato a los mensajes del bot](/microsoftteams/platform/bots/how-to/format-your-bot-messages). | No | Reduzca el tamaño de la carga. |
| 429 | **Código**: `Throttled` <br/> **Mensaje**: Demasiadas solicitudes. También devuelve cuándo volver a intentarlo después. | El bot envió demasiadas solicitudes. Para obtener más información, consulte [límite de velocidad](/microsoftteams/platform/bots/how-to/rate-limit). | Sí | Vuelva a intentar usar el `Retry-After` encabezado para determinar el tiempo de retroceso. |
| 500 | **Código**: `ServiceError` <br/> **Mensaje**: *varios | Error interno del servidor. | No | Informe del problema en la [comunidad de desarrolladores](~/feedback.md#developer-community-help). |
| 502 | **Código**: `ServiceError` <br/> **Mensaje**: *varios | Problema de dependencia de servicio. | Sí | Vuelva a intentarlo con retroceso exponencial. Si el problema persiste, informe del problema en la [comunidad de desarrolladores](~/feedback.md#developer-community-help). |
| 503 | | El servicio no está disponible. | Sí | Vuelva a intentarlo con retroceso exponencial. Si el problema persiste, informe del problema en la [comunidad de desarrolladores](~/feedback.md#developer-community-help). |
| 504 | | Tiempo de espera de la puerta de enlace. | Sí | Vuelva a intentarlo con retroceso exponencial. Si el problema persiste, informe del problema en la [comunidad de desarrolladores](~/feedback.md#developer-community-help). |

### <a name="status-codes-retry-guidance"></a>Guía de reintento de códigos de estado

La guía general de reintentos para cada código de estado se muestra en la tabla siguiente; el bot debe evitar reintentar los códigos de estado que no se especifican:

|Código de estado | Estrategia de reintento |
|----------------|-----------------|
| 403 | Vuelva a intentarlo llamando a la API `https://smba.infra.gcc.teams.microsoft.com` de GCC para `InvalidBotApiHost`.|
| 412 | Vuelva a intentarlo con el retroceso exponencial. |
| 429 | Vuelva a intentar usar el `Retry-After` encabezado para determinar el tiempo de espera en segundos y entre solicitudes, si está disponible. De lo contrario, vuelva a intentar usar el retroceso exponencial con el identificador de subproceso, si es posible. |
| 502 | Vuelva a intentarlo con el retroceso exponencial. |
| 503 | Vuelva a intentarlo con el retroceso exponencial. |
| 504 | Vuelva a intentarlo con el retroceso exponencial. |

## <a name="code-sample"></a>Ejemplo de código

| Ejemplo de nombre | Descripción | Node.js | .NETCore | Python | .NET |
|----------------|-----------------|--------------|----------------|-----------|-----|
| Bot de conversación de Teams | Control de eventos de mensajería y conversación. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [Ver](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) | ND |
| Localización de aplicaciones de Teams | Localización de aplicaciones de Teams mediante bot y pestaña. | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) | ND | ND | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Menús de comandos del bot](~/bots/how-to/create-a-bot-commands-menu.md)

## <a name="see-also"></a>Vea también

* [Enviar mensajes proactivos](~/bots/how-to/conversations/send-proactive-messages.md)
* [Suscribirse a eventos de conversación](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* [Enviar y recibir archivos a través del bot](~/bots/how-to/bots-filesv4.md)
* [Envío del identificador de inquilino y el identificador de conversación a los encabezados de solicitud del bot](~/bots/how-to/conversations/request-headers-of-the-bot.md)
* [Localizar la aplicación](../../../concepts/build-and-test/apps-localization.md)

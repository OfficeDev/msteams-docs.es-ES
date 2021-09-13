---
title: Enviar y recibir mensajes con un bot
description: Describe cómo enviar y recibir mensajes con bots en Microsoft Teams
ms.topic: overview
ms.localizationpriority: medium
keywords: mensajes de bots de teams
ms.date: 05/20/2019
ms.openlocfilehash: c82f96c42992f49f61d19c2bf5c6a19283e8ee95
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157413"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a>Tener una conversación con un Microsoft Teams bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Una conversación es una serie de mensajes enviados entre el bot y uno o más usuarios. Hay tres tipos de conversaciones (también denominadas ámbitos) en Teams:

* `teams` También se denomina conversaciones de canal, visibles para todos los miembros del canal.
* `personal` Conversaciones entre bots y un solo usuario.
* `groupChat` Chatear entre un bot y dos o más usuarios.

Un bot se comporta de forma ligeramente diferente en función del tipo de conversación en la que esté implicado:

* [Bots in channel and group chat conversations](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) require the user to @mention the bot to invoke it in a channel.
* [Bots in single user conversations](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) do not require an @mention - the user can just type.

Para que el bot funcione en un ámbito determinado, debe aparecer como compatible con ese ámbito en el manifiesto. Los ámbitos se definen y se analizan más adelante en la [referencia de manifiesto](~/resources/schema/manifest-schema.md).

## <a name="proactive-messages"></a>Mensajes proactivos

Los bots pueden participar en una conversación o iniciar una. La mayoría de la comunicación es en respuesta a otro mensaje. Si un bot inicia una conversación, se denomina mensaje *proactivo*. Algunos ejemplos son:

* Mensajes de bienvenida
* Notificaciones de eventos
* Mensajes de sondeo

## <a name="conversation-basics"></a>Conceptos básicos de la conversación

Cada mensaje es un objeto `Activity` de tipo `messageType: message`. Cuando un usuario envía un mensaje, Teams publica el mensaje en el bot; en concreto, envía un objeto JSON al punto de conexión de mensajería del bot. El bot examina el mensaje para determinar su tipo y responde en consecuencia.

Los bots también admiten mensajes de estilo de evento. Para obtener más información, vea [Handle bot events in Microsoft Teams](~/resources/bot-v3/bots-notifications.md). Actualmente, no se admite voz.

En la mayoría de los casos, los mensajes son iguales en todos los ámbitos, pero hay diferencias en la forma en que se accede al bot en la interfaz de usuario y diferencias entre bastidores que necesitarás conocer.

La conversación básica se controla a través de Bot Framework Connector, una única API de REST para permitir que el bot se comunique con Teams y otros canales. El SDK de Bot Builder proporciona acceso fácil a esta API, funcionalidad adicional para administrar el estado y el flujo de conversación, y formas sencillas de incorporar servicios cognitivos como el procesamiento de lenguaje natural (NLP).

## <a name="message-content"></a>Contenido del mensaje

El bot puede enviar texto enriquecido, imágenes y tarjetas. Los usuarios pueden enviar texto enriquecido e imágenes al bot. Puede especificar el tipo de contenido que el bot puede controlar en la página Microsoft Teams configuración del bot.

| Formato | De usuario a bot  | De bot a usuario |  Notas |
| --- | :---: | :---: | --- |
| Texto enriquecido  | ✔ | ✔ |  |
| Imágenes | ✔ | ✔ | Máximo 1024×1024 y 1 MB en formato PNG, JPEG o GIF; GIF animado no se admite. |
| Tarjetas | ✖ | ✔ | Consulta la [referencia Teams tarjeta para](~/task-modules-and-cards/cards/cards-reference.md) ver las tarjetas admitidas. |
| Emojis | ✖ | ✔ | Teams admite emojis a través de UTF-16, como U+1F600 para la cara sonriente. |
|

Para obtener más información sobre los tipos de interacción de bot compatibles con Bot Framework, [](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true) en los que se basan los bots de teams, consulte la documentación de Bot Framework sobre el flujo de conversación y los conceptos relacionados en la documentación para bot [Builder SDK for .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true) y bot Builder SDK [for Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true).

## <a name="message-formatting"></a>Formato de mensajes

Puede establecer la propiedad opcional de a para controlar cómo se representa el contenido de texto [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) `message` del mensaje. Consulte [Formato de mensaje para](~/resources/bot-v3/bots-message-format.md) obtener una descripción detallada del formato admitido en los mensajes de bot.
Puede establecer la propiedad opcional para controlar cómo se representa el contenido de texto [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) del mensaje.

Para obtener información detallada sobre cómo Teams formato de texto en equipos, vea [Formato de texto en mensajes de bot](~/resources/bot-v3/bots-text-formats.md).

Para obtener más información sobre el formato de tarjetas en los mensajes, vea [Formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).

## <a name="picture-messages"></a>Mensajes de imagen

Las imágenes se envían agregando datos adjuntos a un mensaje. Encontrará más información sobre los datos adjuntos en la [documentación de Bot Framework](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true).

Las imágenes pueden tener como máximo 1024×1024 y 1 MB en formato PNG, JPEG o GIF; GIF animado no es compatible.

Se recomienda especificar el alto y el ancho de cada imagen mediante XML. Si usa Markdown, el tamaño de la imagen tiene el valor predeterminado 256×256. Por ejemplo:

* Use `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* No usar `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="receiving-messages&quot;></a>Recepción de mensajes

Según los ámbitos declarados, el bot puede recibir mensajes en los siguientes contextos:

* **chat personal** Los usuarios pueden interactuar en una conversación privada con un bot simplemente seleccionando el bot agregado en el historial de chat o escribiendo su nombre o identificador de aplicación en el cuadro Para: en un nuevo chat.
* **Canales** Se puede mencionar un bot (&quot;@_botname")_ en un canal si se ha agregado al equipo. Tenga en cuenta que las respuestas adicionales a un bot en un canal requieren mencionar el bot. No responderá a las respuestas en las que no se menciona.

Para los mensajes entrantes, el bot recibe un [objeto Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) de tipo `messageType: message` . Aunque el objeto puede contener otros tipos de información, como las actualizaciones de canal enviadas al bot, el tipo representa la comunicación `Activity` entre bot y [](~/resources/bot-v3/bots-notifications.md#channel-updates) `message` usuario.

El bot recibe una carga que contiene el mensaje de usuario, así como otra información sobre el usuario, el origen del mensaje y `Text` Teams información. Nota:

* `timestamp` La fecha y hora del mensaje en hora universal coordinada (UTC).
* `localTimestamp` La fecha y hora del mensaje en la zona horaria del remitente.
* `channelId` Siempre "msteams". Esto hace referencia a un canal de marco de bot, no a un canal de teams.
* `from.id` Un identificador único y cifrado para ese usuario para el bot; adecuado como clave si la aplicación necesita almacenar datos de usuario. Es único para el bot y no se puede usar directamente fuera de la instancia del bot de ninguna manera significativa para identificar a ese usuario.
* `channelData.tenant.id` El identificador de inquilino del usuario.

> [!NOTE]
> `from.id` es único para el bot y no se puede usar directamente fuera de la instancia del bot de ninguna manera significativa para identificar a ese usuario.

## <a name="combining-channel-and-private-interactions-with-your-bot"></a>Combinar interacciones privadas y de canal con el bot

Al interactuar en un canal, el bot debe ser inteligente para desconectar determinadas conversaciones con un usuario. Por ejemplo, supongamos que un usuario está intentando coordinar una tarea compleja, como la programación con un conjunto de miembros del equipo. En lugar de tener toda la secuencia de interacciones visible para el canal, considere la posibilidad de enviar un mensaje de chat personal al usuario. El bot debe poder realizar una transición fácil al usuario entre conversaciones personales y de canal sin perder el estado.

> [!NOTE]
>No olvide actualizar el canal cuando se complete la interacción para notificar a los demás miembros del equipo.

## <a name="full-inbound-schema-example"></a>Ejemplo de esquema entrante completo

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

> [!NOTE]
> El campo de texto de los mensajes entrantes a veces contiene menciones. Asegúrese de comprobar y quitar los archivos correctamente. Para obtener más información, vea [Menciones](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).

## <a name="teams-channel-data"></a>Teams de canal

El objeto contiene Teams información específica y es el origen definitivo de `channelData` los IDs de equipo y canal. Debe almacenar en caché y usar estos identificadores como claves para el almacenamiento local.

El objeto no se incluye en los mensajes de las conversaciones personales, ya que se llevan a `channelData` cabo fuera de cualquier canal.

Un objeto channelData típico de una actividad enviada al bot contiene la siguiente información:

* `eventType`Teams tipo de evento; se pasa solo en casos de [eventos de modificación de canal](~/resources/bot-v3/bots-notifications.md#channel-updates).
* `tenant.id`Azure Active Directory de inquilino; pasado en todos los contextos.
* `team` Se pasa solo en contextos de canal, no en chat personal.
  * `id` GUID del canal.
  * `name`Nombre del equipo; se pasa solo en casos de [eventos de cambio de nombre de equipo.](~/resources/bot-v3/bots-notifications.md#team-name-updates)
* `channel` Se pasa solo en contextos de canal cuando se menciona el bot o para eventos en canales de equipos donde se ha agregado el bot.
  * `id` GUID del canal.
  * `name` Nombre del canal; se pasa solo en casos de [eventos de modificación de canal](~/resources/bot-v3/bots-notifications.md#channel-updates).
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

### <a name="net-example"></a>Ejemplo de .NET

El [paquete Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet proporciona un objeto especializado, que expone propiedades para obtener acceso a `TeamsChannelData` Teams información específica.

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a>Enviar respuestas a mensajes

Para responder a un mensaje existente, llame [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) en .NET o [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) en Node.js. El SDK de Bot Builder controla todos los detalles.

Si elige usar la API de REST, también puede llamar al punto de [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) conexión.

El contenido del mensaje en sí puede contener texto simple o algunas de las tarjetas y acciones de [tarjeta proporcionadas](~/task-modules-and-cards/cards/cards-actions.md)por Bot Framework.

Tenga en cuenta que en el esquema saliente siempre debe usar lo mismo `serviceUrl` que el que recibió. Tenga en cuenta que el valor `serviceUrl` de tiende a ser estable pero puede cambiar. Cuando llega un mensaje nuevo, el bot debe comprobar su valor almacenado de `serviceUrl` .

## <a name="updating-messages"></a>Actualizar mensajes

En lugar de hacer que los mensajes sean instantáneas estáticas de datos, el bot puede actualizar dinámicamente los mensajes en línea después de enviarlos. Puede usar actualizaciones dinámicas de mensajes para escenarios como las actualizaciones de sondeo, la modificación de acciones disponibles después de presionar un botón o cualquier otro cambio de estado asincrónico.

El nuevo mensaje no necesita coincidir con el tipo original. Por ejemplo, si el mensaje original contenía datos adjuntos, el nuevo mensaje puede ser un mensaje de texto simple.

> [!NOTE]
> Solo puede actualizar el contenido enviado en mensajes de datos adjuntos únicos y diseños de carrusel. No se admite la publicación de actualizaciones en mensajes con varios datos adjuntos en el diseño de lista.

### <a name="rest-api"></a>API REST

Para emitir una actualización de mensaje, solo tiene que realizar una solicitud PUT en el `/v3/conversations/<conversationId>/activities/<activityId>/` extremo mediante un identificador de actividad determinado. Para completar este escenario, debe almacenar en caché el identificador de actividad devuelto por la llamada POST original.

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a>Ejemplo de .NET

Puede usar el método `UpdateActivityAsync` en el SDK de Bot Builder para actualizar un mensaje existente.

```csharp
public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
{
  if (activity.Type == ActivityTypes.Message)
  {
    ConnectorClient connector = new ConnectorClient(new Uri(activity.ServiceUrl));
    Activity reply = activity.CreateReply($"You sent {activity.Text} which was {activity.Text.Length} characters");
    var msgToUpdate = await connector.Conversations.ReplyToActivityAsync(reply);
    Activity updatedReply = activity.CreateReply($"This is an updated message");
    await connector.Conversations.UpdateActivityAsync(reply.Conversation.Id, msgToUpdate.Id, updatedReply);
  }
}
```

### <a name="nodejs-example"></a>Node.js ejemplo

Puede usar el método `session.connector.update` en el SDK de Bot Builder para actualizar un mensaje existente.

```javascript
function sendCardUpdate(bot, session, originalMessage, address) {

  var origAttachment = originalMessage.data.attachments[0];
  origAttachment.content.subtitle = 'Assigned to Larry Jin';

  var updatedMsg = new builder.Message()
    .address(address)
    .textFormat(builder.TextFormat.markdown)
    .addAttachment(origAttachment)
    .toMessage();

  session.connector.update(updatedMsg, function(err, addresses) {
    if (err) {
      console.log(`Could not update the message`);
    }
  });
}
```

## <a name="starting-a-conversation-proactive-messaging"></a>Iniciar una conversación (mensajería proactiva)

Puedes crear una conversación personal con un usuario o iniciar una nueva cadena de respuesta en un canal para el bot de equipo. Esto le permite enviar un mensaje a su usuario o usuarios sin que inicien el primer contacto con el bot. Para obtener más información, consulte los siguientes temas:

Consulta [Mensajería proactiva para bots para](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) obtener más información general sobre las conversaciones iniciadas por bots.

## <a name="deleting-messages"></a>Eliminación de mensajes

Los mensajes se pueden eliminar mediante el método connectors [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) en el SDK de [BotBuilder](/bot-framework/bot-builder-overview-getstarted).

```typescript
bot.dialog('BotDeleteMessage', function (session: builder.Session) {
  var msg = new teams.TeamsMessage(session).text("Bot will delete this message in 5 sec.")
  bot.send(msg, function (err, response) {
    if (err) {
      console.log(err);
      session.endDialog();
    }

    console.log('Proactive message response:');
    console.log(response);
    console.log('---------------------------------------------------')
    setTimeout(function () {
      var activityId: string = null;
      var messageAddress: builder.IChatConnectorAddress = null;
      if (response[0]){
        messageAddress = response[0];
        activityId = messageAddress.id;
      }

      if (activityId == null)
      {
        console.log('Message failed to send.');
        session.endDialog();
        return;
      }

      // Bot delete message
      let address: builder.IChatConnectorAddress  = {
        channelId: 'msteams',
        user: messageAddress.user,
        bot: messageAddress.bot,
        id : activityId,
        serviceUrl : (<builder.IChatConnectorAddress>session.message.address).serviceUrl,
        conversation: {
          id: session.message.address.conversation.id
        }
      };

      connector.delete(address, function (err) {
        if (err)
        {
          console.log(err);
        }
        else
        {
          console.log("Message: " + activityId + " deleted successfully.");
        }

        // Try editing deleted message would fail
        var newMsg = new builder.Message().address(address).text("To edit message.");
        connector.update(newMsg.toMessage(), function (err, address) {
          if (err)
          {
            console.log(err);
            console.log('Deleted message can not be edited.');
          }
          else
          {
            console.log("There is something wrong. Message: " + activityId + " edited successfully.");
            console.log(address);
          }

          session.endDialog();
        });
      });
    }, 5000);
  });
})
```

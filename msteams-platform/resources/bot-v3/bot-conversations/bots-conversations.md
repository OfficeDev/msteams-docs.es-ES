---
title: Enviar y recibir mensajes con un bot
description: Describe cómo enviar y recibir mensajes con bots en Microsoft Teams
ms.topic: overview
localization_priority: Normal
keywords: equipos bots mensajes
ms.date: 05/20/2019
ms.openlocfilehash: e1926afe42bca45eda5f39be1be8342452b3aa24
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566498"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a>Tener una conversación con un bot Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Una conversación es una serie de mensajes enviados entre el bot y uno o más usuarios. Hay tres tipos de conversaciones (también denominadas ámbitos) en Teams:

* `teams` También se denominan conversaciones de canal, visibles para todos los miembros del canal.
* `personal` Conversaciones entre bots y un solo usuario.
* `groupChat` Chatea entre un bot y dos o más usuarios.

Un bot se comporta ligeramente diferente dependiendo del tipo de conversación en la que esté involucrado:

* [Los bots en conversaciones](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) de chat de canal y grupo requieren que el usuario @mention que el bot lo invoque en un canal.
* [Los bots en conversaciones de un solo usuario](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) no requieren una @mention- el usuario solo puede escribir.

Para que el bot funcione en un ámbito determinado, debe aparecer como compatible con ese ámbito en el manifiesto. Los ámbitos se definen y se describen más a fondo en la [referencia de manifiesto.](~/resources/schema/manifest-schema.md)

## <a name="proactive-messages"></a>Mensajes proactivos

Los bots pueden participar en una conversación o iniciar una. La mayoría de la comunicación es en respuesta a otro mensaje. Si un bot inicia una conversación se denomina *mensaje proactivo.* Algunos ejemplos son:

* Mensajes de bienvenida
* Notificaciones de eventos
* Mensajes de votación

## <a name="conversation-basics"></a>Conceptos básicos de la conversación

Cada mensaje es un objeto `Activity` de tipo `messageType: message`. Cuando un usuario envía un mensaje, Teams publica el mensaje en el bot; en concreto, envía un objeto JSON al punto de conexión de mensajería del bot. El bot examina el mensaje para determinar su tipo y responde en consecuencia.

Los bots también admiten mensajes de estilo de evento. Para obtener más información, consulte [Controlar eventos de bot en Microsoft Teams](~/resources/bot-v3/bots-notifications.md). Actualmente no se admite el discurso.

Los mensajes son en su mayor parte los mismos en todos los ámbitos, pero hay diferencias en cómo se accede al bot en la interfaz de usuario y las diferencias entre bastidores que necesitará saber.

La conversación básica se controla a través de Bot Framework Connector, una única API de REST para permitir que el bot se comunique con Teams y otros canales. El SDK de Bot Builder proporciona un fácil acceso a esta API, funcionalidad adicional para administrar el flujo y el estado de la conversación y formas sencillas de incorporar servicios cognitivos como el procesamiento de lenguaje natural (PNL).

## <a name="message-content"></a>Contenido del mensaje

El bot puede enviar texto enriquecido, imágenes y tarjetas. Los usuarios pueden enviar texto enriquecido e imágenes al bot. Puede especificar el tipo de contenido que el bot puede controlar en la página de configuración de Microsoft Teams del bot.

| Formato | De usuario a bot  | Del bot al usuario |  Notas |
| --- | :---: | :---: | --- |
| Texto enriquecido  | ✔ | ✔ |  |
| Imágenes | ✔ | ✔ | Máximo 1024×1024 y 1 MB en formato PNG, JPEG o GIF; GIF animados no son compatibles. |
| Tarjetas | ✖ | ✔ | Consulte la [referencia de la tarjeta Teams](~/task-modules-and-cards/cards/cards-reference.md) para las tarjetas compatibles. |
| Emojis | ✖ | ✔ | Teams actualmente es compatible con emojis a través de UTF-16 como, U+1F600 para la cara sonriente. |
|

Para obtener más información sobre los tipos de interacción con bots admitidos por Bot Framework, en qué bots de equipos se basan, consulte la documentación de Bot Framework sobre el [flujo de conversaciones](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true) y los conceptos relacionados en la documentación del SDK de Bot Builder para [.NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true) y [el SDK de Bot Builder para Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true).

## <a name="message-formatting"></a>Formato de mensajes

Puede establecer la propiedad opcional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) de a para controlar cómo se representa el contenido de texto del `message` mensaje. Consulte [Formato de mensaje](~/resources/bot-v3/bots-message-format.md) para obtener una descripción detallada del formato admitido en los mensajes de bot.
Puede establecer la propiedad opcional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) para controlar cómo se representa el contenido de texto del mensaje.

Para obtener información detallada sobre cómo Teams admite el formato de texto en los equipos, vea [Formato de texto en mensajes de bot.](~/resources/bot-v3/bots-text-formats.md)

Para obtener más información sobre el formato de tarjetas en mensajes, consulte [Formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).

## <a name="picture-messages"></a>Mensajes de imagen

Las imágenes se envían añadiendo archivos adjuntos a un mensaje. Puede encontrar más información sobre los datos adjuntos en la [documentación de Bot Framework](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true).

Las imágenes pueden ser como máximo 1024×1024 y 1 MB en formato PNG, JPEG o GIF; GIF animado no es compatible.

Se recomienda especificar la altura y el ancho de cada imagen mediante XML. Si utiliza Markdown, el tamaño de imagen predeterminado es 256×256. Por ejemplo:

* Use `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* No uses `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="receiving-messages&quot;></a>Recepción de mensajes

En función de los ámbitos declarados, el bot puede recibir mensajes en los contextos siguientes:

* **chat personal** Los usuarios pueden interactuar en una conversación privada con un bot simplemente seleccionando el bot agregado en el historial de chat, o escribiendo su nombre o ID de aplicación en el cuadro Para: en un nuevo chat.
* **Canales** Se puede mencionar un bot (&quot;@_botname_") en un canal si se ha agregado al equipo. Tenga en cuenta que las respuestas adicionales a un bot en un canal requieren mencionar el bot. No responderá a las respuestas cuando no se mencione.

Para los mensajes entrantes, el bot recibe un [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0&preserve-view=true) objeto de tipo `messageType: message` . Aunque el `Activity` objeto puede contener otros tipos de información, como las actualizaciones de canal [enviadas](~/resources/bot-v3/bots-notifications.md#channel-updates) al bot, el tipo representa la `message` comunicación entre bot y usuario.

El bot recibe una carga que contiene el mensaje de `Text` usuario, así como otra información sobre el usuario, el origen del mensaje y Teams información. Cabe destacar:

* `timestamp` La fecha y hora del mensaje en hora universal coordinada (UTC).
* `localTimestamp` La fecha y hora del mensaje en la zona horaria del remitente.
* `channelId` Siempre "msteams". Esto hace referencia a un canal de marco de trabajo de bots, no a un canal de equipos.
* `from.id` Un identificador único y cifrado para ese usuario para el bot; adecuado como clave si la aplicación necesita almacenar datos de usuario. Es único para el bot y no se puede utilizar directamente fuera de la instancia de bot de ninguna manera significativa para identificar a ese usuario.
* `channelData.tenant.id` El identificador de inquilino del usuario.

> [!NOTE]
> `from.id` es único para el bot y no se puede utilizar directamente fuera de la instancia de bot de ninguna manera significativa para identificar a ese usuario.

## <a name="combining-channel-and-private-interactions-with-your-bot"></a>Combinación de canal e interacciones privadas con su bot

Al interactuar en un canal, el bot debe ser inteligente para desconectar ciertas conversaciones con un usuario. Por ejemplo, supongamos que un usuario está intentando coordinar una tarea compleja, como la programación con un conjunto de miembros del equipo. En lugar de tener toda la secuencia de interacciones visibles para el canal, considere la posibilidad de enviar un mensaje de chat personal al usuario. El bot debe ser capaz de realizar una transición fácil del usuario entre conversaciones personales y de canal sin perder el estado.

> [!NOTE]
>No olvide actualizar el canal cuando se complete la interacción para notificar a los demás miembros del equipo.

## <a name="full-inbound-schema-example"></a>Ejemplo completo de esquema entrante

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
> El campo de texto para los mensajes entrantes a veces contiene menciones. Asegúrese de comprobarlos correctamente y quitarlos. Para obtener más información, consulte [Menciones](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).

## <a name="teams-channel-data"></a>datos de canal Teams

El `channelData` objeto contiene información específica de Teams y es el origen definitivo para los ID de equipo y canal. Debe almacenar en caché y usar estos identificadores como claves para el almacenamiento local.

El `channelData` objeto no se incluye en los mensajes en conversaciones personales, ya que tienen lugar fuera de cualquier canal.

Un objeto channelData típico de una actividad enviada al bot contiene la siguiente información:

* `eventType`Teams tipo de evento; pasado sólo en casos de eventos de modificación de [canal.](~/resources/bot-v3/bots-notifications.md#channel-updates)
* `tenant.id`Azure Active Directory id. de inquilino; pasado en todos los contextos.
* `team` Pasado sólo en contextos de canal, no en chat personal.
  * `id` GUID para el canal.
  * `name`Nombre del equipo; pasado sólo en los casos de eventos de cambio de nombre del [equipo.](~/resources/bot-v3/bots-notifications.md#team-name-updates)
* `channel` Solo se pasa en contextos de canal cuando se menciona el bot o para eventos en canales de equipos donde se ha agregado el bot.
  * `id` GUID para el canal.
  * `name`Nombre del canal; pasado sólo en casos de eventos de modificación de [canal.](~/resources/bot-v3/bots-notifications.md#channel-updates)
* `channelData.teamsTeamId` obsolescente. Esta propiedad solo se incluye para compatibilidad con versiones anteriores.
* `channelData.teamsChannelId` obsolescente. Esta propiedad solo se incluye para compatibilidad con versiones anteriores.

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

El paquete [NuGet Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) proporciona un `TeamsChannelData` objeto especializado, que expone propiedades para tener acceso a información específica de Teams.

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a>Envío de respuestas a mensajes

Para responder a un mensaje existente, llame a [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) .NET o [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) en Node.js. El SDK de Bot Builder controla todos los detalles.

Si decide usar la API de REST, también puede llamar al [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) punto de conexión.

El contenido del mensaje en sí puede contener texto simple o algunas de las tarjetas y acciones de [tarjeta proporcionadas](~/task-modules-and-cards/cards/cards-actions.md)por Bot Framework.

Tenga en cuenta que en el esquema de salida siempre debe usar lo mismo `serviceUrl` que el que recibió. Tenga en cuenta que el valor de `serviceUrl` tiende a ser estable, pero puede cambiar. Cuando llega un nuevo mensaje, el bot debe comprobar su valor almacenado de `serviceUrl` .

## <a name="updating-messages"></a>Actualización de mensajes

En lugar de que los mensajes sean instantáneas estáticas de datos, el bot puede actualizar dinámicamente los mensajes en línea después de enviarlos. Puede usar actualizaciones de mensajes dinámicos para escenarios como actualizaciones de sondeo, modificación de acciones disponibles después de pulsar un botón o cualquier otro cambio de estado asincrónico.

El nuevo mensaje no tiene por qué coincidir con el original en tipo. Por ejemplo, si el mensaje original contenía un archivo adjunto, el nuevo mensaje puede ser un mensaje de texto simple.

> [!NOTE]
> Solo puede actualizar el contenido enviado en mensajes de datos adjuntos únicos y diseños de carrusel. No se admite la publicación de actualizaciones en mensajes con varios datos adjuntos en el diseño de lista.

### <a name="rest-api"></a>API REST

Para emitir una actualización de mensaje, simplemente realice una solicitud PUT en el `/v3/conversations/<conversationId>/activities/<activityId>/` punto de conexión mediante un identificador de actividad determinado. Para completar este escenario, debe almacenar en caché el identificador de actividad devuelto por la llamada POST original.

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a>Ejemplo de .NET

Puede usar el `UpdateActivityAsync` método en el SDK de Bot Builder para actualizar un mensaje existente.

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

Puede usar el `session.connector.update` método en el SDK de Bot Builder para actualizar un mensaje existente.

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

## <a name="starting-a-conversation-proactive-messaging"></a>Inicio de una conversación (mensajería proactiva)

Puede crear una conversación personal con un usuario o iniciar una nueva cadena de respuesta en un canal para el bot de su equipo. Esto le permite enviar un mensaje a su usuario o usuarios sin que primero inicien contacto con el bot. Para obtener más información, consulte los siguientes temas:

Consulte [Mensajería proactiva para bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) para obtener información más general sobre las conversaciones iniciadas por bots.

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

---
title: Enviar y recibir mensajes con un bot
description: Describe cómo enviar y recibir mensajes con bots en Microsoft Teams.
keywords: mensajes de los bots de Microsoft Teams
ms.date: 05/20/2019
ms.openlocfilehash: 4a15bb9b4ae8c0ede3214d3a534649e2769baf6e
ms.sourcegitcommit: 2b1fd50466d807869fd173371ba7dfd82a0064ac
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2020
ms.locfileid: "44801510"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a>Tener una conversación con un bot de Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Una conversación es una serie de mensajes enviados entre el bot y uno o más usuarios. Hay tres tipos de conversaciones (también denominadas ámbitos) en Microsoft Teams:

* `teams`También se denominan conversaciones de canal, visibles para todos los miembros del canal.
* `personal`Conversaciones entre bots y un único usuario.
* `groupChat`Chatear entre un bot y dos o más usuarios.

Un bot tiene un comportamiento ligeramente diferente en función del tipo de conversación en el que esté involucrado:

* Los [bots en conversaciones de chat en el grupo y en el canal](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) requieren al usuario que mencione el bot para invocarlo en un canal.
* Los [bots en conversaciones de usuario único](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) no necesitan @ mencionar: el usuario simplemente puede escribir.

Para que el bot funcione en un ámbito determinado, debe aparecer como compatible con ese ámbito en el manifiesto. Los ámbitos se definen y explican con más detalle en la [Referencia del manifiesto](~/resources/schema/manifest-schema.md).

## <a name="proactive-messages"></a>Mensajes proactivos

Los bots pueden participar en una conversación o iniciar una. La mayor parte de la comunicación está en respuesta a otro mensaje. Si un bot inicia una conversación, se denomina *mensaje proactivo*. Algunos ejemplos son:

* Mensajes de bienvenida
* Notificaciones de eventos
* Mensajes de sondeo

## <a name="conversation-basics"></a>Conceptos básicos de la conversación

Cada mensaje es un `Activity` objeto de tipo `messageType: message` . Cuando un usuario envía un mensaje, Microsoft Teams expone el mensaje a su bot; en concreto, envía un objeto JSON al extremo de mensajería de bot. El bot examina el mensaje para determinar su tipo y responde en consecuencia.

Los bots también admiten mensajes de estilo de evento. Consulte [administrar eventos de bot en Microsoft Teams](~/resources/bot-v3/bots-notifications.md) para obtener más información. Actualmente no se admite la voz.

Los mensajes son, en su mayoría, iguales en todos los ámbitos, pero hay diferencias en el modo en que se tiene acceso a bot en la interfaz de usuario y las diferencias entre bastidores que necesitará conocer.

La conversación básica se controla a través del conector de bot Framework, una única API de REST para permitir que su bot se comunique con Microsoft Teams y otros canales. El SDK de bot Builder proporciona acceso sencillo a esta API, funcionalidad adicional para administrar el flujo de conversaciones y el estado, y formas sencillas de incorporar servicios cognitivos como el procesamiento de lenguaje natural (NLP).

## <a name="message-content"></a>Contenido del mensaje

El bot puede enviar texto enriquecido, imágenes y tarjetas. Los usuarios pueden enviar texto enriquecido e imágenes a su bot. Puede especificar el tipo de contenido que puede controlar el bot en la página de configuración de Microsoft Teams de su bot.

| Formato | De un usuario a un bot  | De bot a User |  Notas |
| --- | :---: | :---: | --- |
| Texto enriquecido  | ✔ | ✔ |  |
| Imágenes | ✔ | ✔ | Máximo de 1024 × 1024 y 1 MB en formato PNG, JPEG o GIF; no se admiten GIF animados |
| Tarjetas | ✖ | ✔ | Ver la [referencia de la tarjeta Teams](~/task-modules-and-cards/cards/cards-reference.md) para tarjetas compatibles |
| Emojis | ✖ | ✔ | Actualmente, los equipos son compatibles con emojis mediante UTF-16 (como U + 1F600 para la cara Grinning). |
|

Para obtener más información acerca de los tipos de interacción de bot admitidos por el marco de robots (en el que se basan los bots en Teams), vea la documentación sobre el [flujo](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0) de las conversaciones y los conceptos relacionados en la documentación del [SDK de bot Builder para .net](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0) y [el SDK del generador de robots para obtener Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0).

## <a name="message-formatting"></a>Formato de mensajes

Puede establecer la propiedad Optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) de `message` a para controlar cómo se representa el contenido de texto del mensaje. Vea [Message Formatting](~/resources/bot-v3/bots-message-format.md) para obtener una descripción detallada del formato admitido en los mensajes de bot.
Puede establecer la propiedad opcional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) para controlar cómo se representa el contenido de texto del mensaje.

Para obtener información detallada sobre cómo Teams admite el formato de texto en Teams, vea [Text Formatting Text messages in Bot messages](~/resources/bot-v3/bots-text-formats.md).

Para obtener información sobre cómo dar formato a las tarjetas de los mensajes, vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).

## <a name="picture-messages"></a>Mensajes de imagen

Las imágenes se envían agregando datos adjuntos a un mensaje. Puede encontrar más información sobre los datos adjuntos en la [documentación de bot Framework](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0).

Las imágenes pueden tener como máximo 1024 x 1024 y 1 MB en formato PNG, JPEG o GIF; GIF animado no es compatible.

Le recomendamos que especifique el alto y el ancho de cada imagen utilizando XML. Si usa Markdown, el tamaño de imagen predeterminado es de 256 × 256. Por ejemplo:

* Utilizados`<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* No use`![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="receiving-messages"></a>Recibir mensajes

Dependiendo de los ámbitos que se declaren, el bot puede recibir mensajes en los siguientes contextos:

* **chat personal** Los usuarios pueden interactuar en una conversación privada con un bot seleccionando el bot agregado en el historial de chats o escribiendo su nombre o identificador de aplicación en el cuadro para: de un nuevo chat.
* **Canales** Un bot puede mencionarse ("@_botname_") en un canal si se ha agregado al equipo. Tenga en cuenta que las respuestas adicionales a un bot en un canal requieren la mención del bot. No responderá a las respuestas en las que no se haya mencionado.

Para los mensajes entrantes, el bot recibe un [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0) objeto de tipo `messageType: message` . Aunque el `Activity` objeto puede contener otros tipos de información, como [las actualizaciones de canal](~/resources/bot-v3/bots-notifications.md#channel-updates) enviadas a su bot, el `message` tipo representa la comunicación entre el bot y el usuario.

El bot recibe una carga que contiene el mensaje de usuario, así `Text` como otra información sobre el usuario, el origen del mensaje y la información de los equipos. De Nota:

* `timestamp`La fecha y la hora del mensaje en la hora universal coordinada (UTC)
* `localTimestamp`La fecha y la hora del mensaje en la zona horaria del remitente
* `channelId`Siempre es "msteams". Se refiere a un canal del marco de bot, no a un canal de Teams.
* `from.id`Un identificador único y cifrado para el usuario de su bot; adecuado como clave si la aplicación necesita almacenar datos de usuario. Es único para el bot y no se puede usar directamente fuera de la instancia de bot de ninguna forma significativa para identificar al usuario
* `channelData.tenant.id`El identificador de inquilino del usuario.

> [!NOTE]
> `from.id`es único para el bot y no se puede usar directamente fuera de la instancia de bot de ninguna forma significativa para identificar a ese usuario.

## <a name="combining-channel-and-private-interactions-with-your-bot"></a>Combinación de interacciones de canal y privado con el bot

Al interactuar en un canal, el bot debe ser inteligente al poner en línea ciertas conversaciones con un usuario. Por ejemplo, supongamos que un usuario intenta coordinar una tarea compleja, como la programación con un conjunto de miembros del equipo. En lugar de tener la secuencia completa de interacciones visibles para el canal, considere la posibilidad de enviar un mensaje de chat personal al usuario. El bot debe poder realizar una transición sencilla al usuario entre conversaciones personales y de canal sin perder el estado.

> [!NOTE]
>No olvide actualizar el canal cuando la interacción se haya completado para notificar a los demás miembros del equipo.

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
> El campo de texto de los mensajes entrantes a veces contiene menciones. Asegúrese de comprobarlos y eliminarlos correctamente. Para obtener más información, vea [menciones](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).

## <a name="teams-channel-data"></a>Datos del canal de Teams

El `channelData` objeto contiene información específica de Microsoft Teams y es la fuente definitiva de los identificadores de equipo y de canal. Debe almacenar en caché y usar estos identificadores como claves para el almacenamiento local.

El `channelData` objeto no está incluido en los mensajes de las conversaciones personales, ya que éstos tienen lugar fuera de cualquier canal.

Un objeto channelData típico de una actividad enviada a su bot contiene la siguiente información:

* `eventType`Tipo de evento de Teams; solo se pasa en casos de [eventos de modificación de canal](~/resources/bot-v3/bots-notifications.md#channel-updates)
* `tenant.id`IDENTIFICADOR de inquilino de Azure Active Directory; se pasan en todos los contextos
* `team`Solo se pasa en contextos de canal, no en chat personal.
  * `id`GUID para el canal
  * `name`Nombre del equipo; solo se pasa en casos de [eventos de cambio de nombre de equipo](~/resources/bot-v3/bots-notifications.md#team-name-updates)
* `channel`Solo se pasa en contextos de canal cuando se menciona el bot o para eventos en los canales en equipos en los que se ha agregado el bot
  * `id`GUID para el canal
  * `name`Nombre del canal; se pasa solo en casos de [eventos de modificación de canal](~/resources/bot-v3/bots-notifications.md#channel-updates).
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

### <a name="net-example"></a>Ejemplo de .NET

El paquete NuGet [Microsoft. bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) proporciona un `TeamsChannelData` objeto especializado, que expone propiedades para obtener acceso a información específica de Teams.

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a>Enviar respuestas a mensajes

Para responder a un mensaje existente, llame a [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_) .net o a [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities) Node.js. El SDK de bot Builder controla todos los detalles.

Si decide usar la API de REST, también puede llamar al punto de [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0) conexión.

El contenido del mensaje puede contener texto simple o algunas de las [tarjetas y las acciones](~/task-modules-and-cards/cards/cards-actions.md)de la tarjeta suministradas con bot Framework.

Tenga en cuenta que en el esquema saliente siempre debe usar el mismo que `serviceUrl` el que recibió. Tenga en cuenta que el valor de `serviceUrl` tiende a ser estable, pero puede cambiar. Cuando llega un nuevo mensaje, el bot debe comprobar su valor almacenado de `serviceUrl` .

## <a name="updating-messages"></a>Actualizar mensajes

En lugar de que los mensajes sean instantáneas estáticas de los datos, el bot puede actualizar de forma dinámica los mensajes en línea después de enviarlos. Puede usar actualizaciones de mensajes dinámicas para escenarios como sondeos de actualizaciones, modificación de acciones disponibles después de presionar un botón o cualquier otro cambio de estado asincrónico.

El nuevo mensaje no tiene que coincidir con el original en el tipo. Por ejemplo, si el mensaje original contenía datos adjuntos, el nuevo mensaje puede ser un mensaje de texto simple.

> [!NOTE]
> Solo puede actualizar contenido enviado en diseños de carrusel y mensajes de datos adjuntos únicos. No se admite el envío de actualizaciones a mensajes con varios datos adjuntos en el diseño de lista.

### <a name="rest-api"></a>API REST

Para emitir una actualización de mensaje, simplemente realice una solicitud PUT contra el `/v3/conversations/<conversationId>/activities/<activityId>/` extremo con un identificador de actividad determinado. Para completar este escenario, debe almacenar en caché el identificador de actividad devuelto por la llamada de publicación original.

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a>Ejemplo de .NET

Puede usar el `UpdateActivityAsync` método en el SDK del generador de robots para actualizar un mensaje existente.

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

### <a name="nodejs-example"></a>Ejemplo de Node.js

Puede usar el `session.connector.update` método en el SDK del generador de robots para actualizar un mensaje existente.

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

Puede crear una conversación personal con un usuario o iniciar una nueva cadena de respuesta en un canal para su bot de equipo. Esto le permite enviar un mensaje a su usuario o usuarios sin que ellos inicien primero contacto con su bot. Para obtener más información, vea los siguientes temas:

Consulte [Mensajería proactiva de bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) para obtener más información general sobre las conversaciones iniciadas por bots.

## <a name="deleting-messages"></a>Eliminación de mensajes

Los mensajes se pueden eliminar con el [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) método Connectors en el [SDK de BotBuilder](/bot-framework/bot-builder-overview-getstarted).

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

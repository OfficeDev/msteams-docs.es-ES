---
title: Envío y recepción de mensajes con un bot
description: Describe cómo enviar y recibir mensajes con bots en Microsoft Teams
ms.topic: overview
ms.localizationpriority: high
keywords: mensajes de bots de teams
ms.date: 05/20/2019
ms.openlocfilehash: dd43c31147c43c06b4f96c709fb0e5af5cd6bb41
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111601"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a>Tener una conversación con un bot de Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Una conversación es una serie de mensajes enviados entre el bot y uno o más usuarios. Hay tres tipos de conversaciones (también denominadas ámbitos) en Teams:

* `teams`: también denominadas conversaciones de canal, visibles para todos los miembros del canal
* `personal`: conversaciones entre bots y un único usuario
* `groupChat` Chat entre un bot y dos o más usuarios.

Un bot se comporta de modo ligeramente diferente según el tipo de conversación en la que participe:

* [Los bots en conversaciones de chat de canal y grupo](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) requieren que el usuario lo @mencione para se lo invoque en un canal.
* [Bots en conversaciones de usuario único](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) no requieren una @mención: el usuario puede simplemente escribir.

Para que el bot funcione en un ámbito determinado, debe aparecer como compatible con ese ámbito en el manifiesto. Los ámbitos se definen y se describen más detalladamente en la [Referencia del Manifiesto](~/resources/schema/manifest-schema.md).

## <a name="proactive-messages"></a>Mensajes proactivos

Los bots pueden participar en una conversación o iniciar una. La mayor parte de la comunicación es en respuesta a otro mensaje. Si un bot inicia una conversación, se denomina *mensaje reactivo*. Algunos ejemplos son:

* Mensajes de bienvenida
* Notificaciones de eventos
* Sondeo de mensajes

## <a name="conversation-basics"></a>Conceptos básicos de la conversación

Cada mensaje es un objeto `Activity` de tipo `messageType: message`. Cuando un usuario envía un mensaje, Teams publica el mensaje en el bot; en concreto, envía un objeto JSON al punto de conexión de mensajería del bot. El bot examina el mensaje para determinar su tipo y responder correctamente.

Los bots también admiten mensajes de estilo de evento. Para obtener más información, vea [Manejo de eventos de bot en Microsoft Teams](~/resources/bot-v3/bots-notifications.md). Actualmente no se admite la voz.

Los mensajes son, en su mayor parte, los mismos en todos los ámbitos, pero hay diferencias en el modo en que se accede al bot en la interfaz de usuario y en las diferencias en segundo plano que deberá conocer.

La conversación básica se controla a través de Bot Framework Connector, una única API REST para permitir que el bot se comunique con Teams y otros canales. El SDK de Bot Builder proporciona acceso sencillo a esta API, funcionalidad adicional para administrar el flujo y el estado de la conversación y formas sencillas de incorporar servicios cognitivos, como el procesamiento de lenguaje natural (NLP).

## <a name="message-content"></a>Contenido del mensaje

El bot puede enviar texto enriquecido, imágenes y tarjetas. Los usuarios pueden enviar texto enriquecido e imágenes al bot. Puede especificar el tipo de contenido que el bot puede controlar en la página de configuración de Microsoft Teams del bot.

| Formato | De usuario a bot  | De bot a usuario |  Notas |
| --- | :---: | :---: | --- |
| Texto enriquecido  | ✔ | ✔ |  |
| Imágenes | ✔ | ✔ | Máximo 1024>1024 y 1 MB en formato PNG, JPEG o GIF; No se admiten GIF animados. |
| Tarjetas | ✖ | ✔ | Consulte la [Referencia de Tarjetas de Teams](~/task-modules-and-cards/cards/cards-reference.md) para ver las tarjetas admitidas. |
| Emojis | ✖ | ✔ | Teams admite actualmente emojis a través de UTF-16, como U+1F600 para la cara sonriente. |
|

Para obtener más información sobre los tipos de interacción de bots admitidos por el Bot Framework, en los que se basan los bots de los equipos, consulte la documentación Bot Framework sobre [flujo de la conversación](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true) y los conceptos relacionados en la documentación de [el Bo Builder de SDK para .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true) y el [Bot Builder de SDK para Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true).

## <a name="message-formatting"></a>Formato de mensajes

Puede establecer la propiedad opcional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) de un `message` para controlar cómo se representa el contenido de texto del mensaje. Consulte [Formato de mensajes](~/resources/bot-v3/bots-message-format.md) para obtener una descripción detallada del formato admitido en los mensajes del bot.
Puede establecer la propiedad opcional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) para controlar cómo se representa el contenido de texto del mensaje.

Para obtener información detallada sobre cómo Teams admite el formato de texto en teams, vea [Formateo de texto en mensajes de bot](~/resources/bot-v3/bots-text-formats.md).

Para obtener más información sobre cómo dar formato a tarjetas en mensajes, vea [Formato de tarjetas](~/task-modules-and-cards/cards/cards-format.md).

## <a name="picture-messages"></a>Mensajes de imagen

Las imágenes se envían agregando datos adjuntos a un mensaje. Puede encontrar más información sobre los datos adjuntos en la [Bot Framework documentación](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true).

Las imágenes deben tener como máximo 1024×1024 y 1MB en formato PNG, JPEG o GIF. No se admiten los GIF animados.

Se recomienda especificar el alto y el ancho de cada imagen mediante XML. Si usa Markdown, el tamaño predeterminado de la imagen es 256>256. Por ejemplo:

* Use `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* No usar `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="receiving-messages"></a>Recepción de mensajes

En función de los ámbitos que se declaren, el bot puede recibir mensajes en los contextos siguientes:

* **chat personal** Los usuarios pueden interactuar en una conversación privada con un bot simplemente seleccionando el bot agregado en el historial de chats o escribiendo su nombre o identificador de aplicación en el cuadro Para: en un nuevo chat.
* **Channels** Se puede mencionar un bot ("@*nombredelbo* t") en un canal si se ha agregado al equipo. Tenga en cuenta que las respuestas adicionales a un bot en un canal requieren mencionar el bot. No responderá a las respuestas en las que no se menciona.

Para los mensajes entrantes, el bot recibe un objeto [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) de tipo `messageType: message`. Aunque el objeto `Activity` puede contener otros tipos de información, al igual que [actualizaciones de canal](~/resources/bot-v3/bots-notifications.md#channel-updates) enviadas al bot, el tipo `message` representa la comunicación entre el bot y el usuario.

El bot recibe una carga que contiene el mensaje de usuario `Text` así como otra información sobre el usuario, el origen del mensaje y la información de Teams. Nota:

* `timestamp` La fecha y hora del mensaje en hora universal coordinada (UTC).
* `localTimestamp` La fecha y hora del mensaje en la zona horaria del remitente.
* `channelId` Siempre "msteams". Esto hace referencia a un canal de Bot Framework, no a un canal de teams.
* `from.id` un identificador único y cifrado para ese usuario para el bot; adecuado como clave si la aplicación necesita almacenar datos de usuario. Es único para el bot y no se puede usar directamente fuera de la instancia del bot de ninguna manera significativa para identificar a ese usuario.
* `channelData.tenant.id` El identificador de espacio empresarial del usuario.

> [!NOTE]
> `from.id` es único para el bot y no se puede usar directamente fuera de la instancia del bot de ninguna manera significativa para identificar a ese usuario.

## <a name="combining-channel-and-private-interactions-with-your-bot"></a>Combinación de interacciones de canal y privadas con el bot

Al interactuar en un canal, el bot debe ser inteligente para desconectar determinadas conversaciones con un usuario. Por ejemplo, supongamos que un usuario está intentando coordinar una tarea compleja, como la programación con un conjunto de miembros del equipo. En lugar de hacer que toda la secuencia de interacciones sea visible para el canal, considere la posibilidad de enviar un mensaje de chat personal al usuario. El bot debería poder realizar fácilmente la transición del usuario entre conversaciones personales y de canal sin perder el estado.

> [!NOTE]
>No olvide actualizar el canal cuando se complete la interacción para notificar a los demás miembros del equipo.

## <a name="full-inbound-schema-example"></a>Ejemplo de esquema de entrada completa

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
> El campo de texto para los mensajes entrantes a veces contiene menciones. Asegúrese de comprobarlos y quitarlos correctamente. Para obtener más información, consulte [Menciones](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).

## <a name="teams-channel-data"></a>Datos del canal de Teams

El objeto `channelData` contiene información específica de Teams y es el origen definitivo de los identificadores de equipo y canal. Debe almacenar en caché y usar estos identificadores como claves para el almacenamiento local.

Un objeto channelData típico de una actividad enviada al bot contiene la siguiente información:

* `eventType` Tipo de evento de Teams; se pasa solo en los casos de [eventos de modificación de canal](~/resources/bot-v3/bots-notifications.md#channel-updates).
* `tenant.id` Microsoft Azure Active Directory (Azure AD) id. de inquilino; se pasa en todos los contextos.
* `team` Solo se pasa en contextos de canal, no en chat personal.
  * `id` GUID para el canal.
  * `name` Nombre del equipo; solo se pasa en los casos de [Eventos de renombramiento de equipos](~/resources/bot-v3/bots-notifications.md#team-name-updates).
* `channel` Solo se pasa en contextos de canal cuando se menciona el bot o para eventos en canales de equipos en los que se ha agregado el bot.
  * `id` GUID para el canal.
  * `name` Nombre de canal; se pasa solo en los casos de [eventos de canal de modificación](~/resources/bot-v3/bots-notifications.md#channel-updates).
* `channelData.teamsTeamId` En desuso Esta propiedad solo se incluye por compatibilidad con versiones anteriores.
* `channelData.teamsChannelId` En desuso Esta propiedad solo se incluye por compatibilidad con versiones anteriores.

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

El paquete NuGet [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) proporciona un objeto `TeamsChannelData` especializado, que expone propiedades para acceder a información específica de Teams.

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a>Envío de respuestas a mensajes

Para responder a un mensaje existente, llame a [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) en .NET o [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true)en Node.js. El Bot Builder de SDK controla todos los detalles.

Si decide usar la API rest, también puede llamar al punto de conexión [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true).

El propio contenido del mensaje puede contener texto simple o algunos de los Bot Framework proporcionados [tarjetas y acciones de tarjeta](~/task-modules-and-cards/cards/cards-actions.md).

Tenga en cuenta que en el esquema de salida siempre debe usar el mismo `serviceUrl` que el que recibió. Tenga en cuenta que el valor de `serviceUrl` tiende a ser estable, pero puede cambiar. Cuando llega un mensaje nuevo, el bot debe comprobar su valor almacenado de `serviceUrl`.

## <a name="updating-messages"></a>Actualizando mensaje...

En lugar de que los mensajes sean instantáneas estáticas de datos, el bot puede actualizar dinámicamente los mensajes insertados después de enviarlos. Puede usar actualizaciones de mensajes dinámicos para escenarios como las actualizaciones de sondeo, la modificación de las acciones disponibles después de presionar un botón o cualquier otro cambio de estado asincrónico.

El nuevo mensaje no tiene que coincidir con el original en el tipo. Por ejemplo, si el mensaje original contenía datos adjuntos, el nuevo mensaje puede ser un mensaje de texto simple.

> [!NOTE]
> Solo puede actualizar el contenido enviado en mensajes de datos adjuntos únicos y diseños de carrusel. No se admite la publicación de actualizaciones en mensajes con varios datos adjuntos en el diseño de lista.

### <a name="rest-api"></a>API de REST

Para emitir una actualización de mensaje, simplemente realice una solicitud PUT en el punto de conexión `/v3/conversations/<conversationId>/activities/<activityId>/` con un identificador de actividad determinado. Para completar este escenario, debe almacenar en caché el identificador de actividad devuelto por la llamada POST original.

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

### <a name="nodejs-example"></a>Ejemplo de Node.js

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

Puede crear una conversación personal con un usuario o iniciar una nueva cadena de respuestas en un canal para el bot de equipo. Esto le permite enviar un mensaje al usuario o a los usuarios sin que primero inicien contacto con el bot. Para obtener más información, consulte los siguientes temas:

Consulte [Mensajería activa para bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) para obtener información más general sobre las conversaciones iniciadas por los bots.

## <a name="deleting-messages"></a>Eliminar mensajes

Los mensajes se pueden eliminar mediante los conectores [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) en el [BotBuilder SDK](/bot-framework/bot-builder-overview-getstarted).

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

---
title: Mensajes proactivos
description: Describe que los bots pueden iniciar una conversación en Microsoft Teams
ms.topic: conceptual
ms.localizationpriority: medium
keywords: escenarios de teams bot de conversación de mensajería proactiva
ms.openlocfilehash: efa77e0202c55973d6ede2454cab4c0ce738a44d
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157213"
---
# <a name="proactive-messaging-for-bots"></a>Mensajería proactiva para bots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Un mensaje proactivo es un mensaje que envía un bot para iniciar una conversación. Puede que quiera que el bot inicie una conversación por varios motivos, entre los que se incluyen:

* Mensajes de bienvenida para conversaciones de bots personales.
* Respuestas de sondeo.
* Notificaciones de eventos externos.

Enviar un mensaje para iniciar un nuevo hilo de conversación es diferente al envío de un mensaje en respuesta a una conversación existente: cuando el bot inicia una nueva conversación, no hay ninguna conversación preexistida en la que publicar el mensaje. Para enviar un mensaje proactivo, debe:

1. [Decidir lo que vas a decir](#best-practices-for-proactive-messaging)
1. [Obtener el identificador único del usuario y el identificador de inquilino](#obtain-necessary-user-information)
1. [Enviar el mensaje](#examples)

Al crear mensajes proactivos, **debe** llamar y pasar la dirección URL del servicio antes de crear la `MicrosoftAppCredentials.TrustServiceUrl` que usará para enviar el `ConnectorClient` mensaje. Si no lo haces, la aplicación recibirá una `401: Unauthorized` respuesta. Para obtener más información, vea [los ejemplos siguientes](#net-example-from-this-sample).

## <a name="best-practices-for-proactive-messaging"></a>Procedimientos recomendados para mensajería proactiva

Enviar mensajes proactivos a los usuarios puede ser una forma muy eficaz de comunicarse con los usuarios. Sin embargo, desde su perspectiva, este mensaje puede parecer que no se les ha enviado y, en el caso de los mensajes de bienvenida, será la primera vez que interactúen con la aplicación. Por lo tanto, es muy importante usar esta funcionalidad con moderación (no enviar correo no deseado a los usuarios) y proporcionarles suficiente información para que comprendan por qué se envían mensajes.

Generalmente, los mensajes proactivos se divide en dos categorías: mensajes de bienvenida o notificaciones.

### <a name="welcome-messages"></a>Mensajes de bienvenida

Al usar la mensajería proactiva para enviar un mensaje de bienvenida a un usuario, debe tener en cuenta que para la mayoría de las personas que reciben el mensaje no tendrán contexto para saber por qué lo están recibiendo. También es la primera vez que interactúan con la aplicación; es la oportunidad de crear una buena primera impresión. Los mejores mensajes de bienvenida incluirán:

* **Por qué reciben este mensaje.** Debe ser muy claro para el usuario por qué están recibiendo el mensaje. Si el bot se instaló en un canal y envió un mensaje de bienvenida a todos los usuarios, hágles saber en qué canal se instaló y quién lo instaló.
* **¿Qué ofrece?** ¿Qué pueden hacer con la aplicación? ¿Qué valor puede aportarles?
* **Qué deben hacer a continuación.** Invítelos a probar un comando o interactuar con la aplicación de alguna manera.

### <a name="notification-messages"></a>Mensajes de notificación

Al usar la mensajería proactiva para enviar notificaciones, debe asegurarse de que los usuarios tienen una ruta de acceso clara para realizar acciones comunes en función de la notificación y una comprensión clara de por qué se produjo la notificación. Por lo general, los mensajes de notificación de buena calidad incluirán:

* **Qué ha pasado.** Una indicación clara de lo que ocurrió para causar la notificación.
* **Lo que ocurrió.** Debe estar claro qué elemento/cosa se actualizó para provocar la notificación.
* **Quién lo hizo.** Quién la acción que hizo que se enviara la notificación.
* **Lo que pueden hacer al respecto.** Facilita a los usuarios realizar acciones en función de las notificaciones.
* **Cómo pueden optar por no participar.** Debe proporcionar una ruta de acceso para que los usuarios no puedan participar en notificaciones adicionales.

## <a name="obtain-necessary-user-information"></a>Obtener información de usuario necesaria

Los bots pueden crear nuevas conversaciones con un usuario Microsoft Teams individual obteniendo el identificador único del usuario y el *identificador* *de inquilino.* Puede obtener estos valores mediante uno de los siguientes métodos:

* Al [capturar la lista de equipos](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) desde un canal en el que se instala la aplicación.
* Al almacenarlos en caché cuando un usuario [interactúa con el bot en un canal](~/resources/bot-v3/bot-conversations/bots-conv-channel.md).
* Cuando un usuario se [@mentioned en una conversación de canal,](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) el bot forma parte.
* Al almacenarlos en caché cuando [recibes `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) el evento cuando la aplicación está instalada en un ámbito personal, o se agregan nuevos miembros a un chat de canal o grupo que.

### <a name="proactively-install-your-app-using-graph"></a>Instale proactivamente la aplicación con Graph

> [!Note]
> La instalación proactiva de aplicaciones con graph se encuentra actualmente en fase beta.

En ocasiones, es posible que sea necesario enviar mensajes de forma proactiva a los usuarios que no han instalado o interactuado con la aplicación anteriormente. Por ejemplo, desea usar el comunicador de la compañía [para](~/samples/app-templates.md#company-communicator) enviar mensajes a toda la organización. Para este escenario, puedes usar la API de Graph para instalar proactivamente la aplicación para los usuarios y, a continuación, almacenar en caché los valores necesarios del evento que la aplicación recibirá al `conversationUpdate` instalarla.

Solo puedes instalar aplicaciones que estén en el catálogo de aplicaciones de la organización o en la Teams de aplicaciones.

Consulta [Instalar aplicaciones para usuarios en](/graph/api/userteamwork-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true) la Graph documentación para obtener información completa. También hay un [ejemplo en .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).

## <a name="examples"></a>Ejemplos

Asegúrese de autenticarse y tener un token de portador antes de crear una nueva conversación con la API de REST.

```json
POST /v3/conversations
{
  "bot": {
    "id": "28:10j12ou0d812-2o1098-c1mjojzldxcj-1098028n ",
    "name": "The Bot"
  },
  "members": [
    {
      "id": "29:012d20j1cjo20211"
    }
  ],
  "channelData": {
    "tenant": {
      "id": "197231joe-1209j01821-012kdjoj"
    }
  }
}
```

Debe proporcionar el identificador de usuario y el identificador de inquilino. Si la llamada se realiza correctamente, la API devuelve el siguiente objeto de respuesta.

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

Este identificador es el identificador de conversación único del chat personal. Almacene este valor y reutilice para futuras interacciones con el usuario.

### <a name="using-net"></a>Uso de .NET

En este ejemplo se [usa microsoft.bot.connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet paquete.

```csharp
// Create or get existing chat conversation with user
var response = client.Conversations.CreateOrGetDirectConversation(activity.Recipient, activity.From, activity.GetTenantId());

// Construct the message to post to conversation
Activity newActivity = new Activity()
{
    Text = "Hello",
    Type = ActivityTypes.Message,
    Conversation = new ConversationAccount
    {
        Id = response.Id
    },
};

// Post the message to chat conversation with user
await client.Conversations.SendToConversationAsync(newActivity, response.Id);
```

### <a name="using-nodejs"></a>Uso de Node.js

```javascript
var address =
{
    channelId: 'msteams',
    user: { id: userId },
    channelData: {
        tenant: {
            id: tenantId
        }
    },
    bot:
    {
        id: appId,
        name: appName
    },
    serviceUrl: session.message.address.serviceUrl,
    useAuth: true
}

var msg = new builder.Message().address(address);
msg.text('Hello, this is a notification');
bot.send(msg);
```

## <a name="creating-a-channel-conversation"></a>Crear una conversación de canal

El bot agregado por el equipo puede publicar en un canal para crear una nueva cadena de respuesta. Si usa el SDK de Node.js Teams, use lo que le proporciona una dirección completa con el identificador de actividad y el identificador de `startReplyChain()` conversación correctos. Si está usando C#, vea el ejemplo siguiente.

Como alternativa, puede usar la API de REST y emitir una solicitud POST al [`/conversations`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) recurso.

### <a name="net-example-from-this-sample"></a>Ejemplo de .NET (de [este ejemplo)](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)

```csharp
using Microsoft.Bot.Builder.Dialogs;
using Microsoft.Bot.Connector;
using Microsoft.Bot.Connector.Teams.Models;
using Microsoft.Teams.TemplateBotCSharp.Properties;
using System;
using System.Threading.Tasks;

namespace Microsoft.Teams.TemplateBotCSharp.Dialogs
{
    [Serializable]
    public class ProactiveMsgTo1to1Dialog : IDialog<object>
    {
        public async Task StartAsync(IDialogContext context)
        {
            if (context == null)
            {
                throw new ArgumentNullException(nameof(context));
            }

            var channelData = context.Activity.GetChannelData<TeamsChannelData>();
            var message = Activity.CreateMessageActivity();
            message.Text = "Hello World";

            var conversationParameters = new ConversationParameters
            {
                  IsGroup = true,
                  ChannelData = new TeamsChannelData
                  {
                      Channel = new ChannelInfo(channelData.Channel.Id),
                  },
                  Activity = (Activity) message
            };

            MicrosoftAppCredentials.TrustServiceUrl(serviceUrl, DateTime.MaxValue);
            var connectorClient = new ConnectorClient(new Uri(activity.ServiceUrl));
            var response = await connectorClient.Conversations.CreateConversationAsync(conversationParameters);

            context.Done<object>(null);
        }
    }
}
```

## <a name="see-also"></a>Consulte también

[Ejemplos de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)

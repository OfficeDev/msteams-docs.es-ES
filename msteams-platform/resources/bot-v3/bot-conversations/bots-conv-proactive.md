---
title: Mensajería proactiva para bots
description: Aprenda a usar la mensajería proactiva para bots en Microsoft Teams
ms.topic: conceptual
ms.localizationpriority: high
keywords: bot de conversación de mensajería proactiva de escenarios de teams
ms.openlocfilehash: 12c6f9ad79d7e28f31e3985930557339e75ccbbf
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111489"
---
# <a name="proactive-messaging-for-bots"></a>Mensajería proactiva para bots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Un mensaje proactivo es un mensaje que envía un bot para iniciar una conversación. Puede que quiera que el bot inicie una conversación por varios motivos, entre los que se incluyen:

* Mensajes de bienvenida para conversaciones de bot personales
* Respuestas de sondeo
* Notificaciones de eventos externos

Enviar un mensaje para iniciar un nuevo subproceso de conversación es diferente a enviar un mensaje en respuesta a una conversación existente: cuando el bot inicia una nueva conversación, no hay ninguna conversación preexistente en la que publicar el mensaje. Para enviar un mensaje proactivo, debe:

1. [Decidir qué va a decir](#best-practices-for-proactive-messaging)
1. [Obtener el identificador único del usuario y el identificador de inquilino](#obtain-necessary-user-information)
1. [Enviar el mensaje](#examples)

Al crear mensajes proactivos **, debe** llamar a `MicrosoftAppCredentials.TrustServiceUrl` y enviar la dirección URL del servicio antes de crear la `ConnectorClient` usada para enviar el mensaje. Si no lo hace, la aplicación recibe una respuesta `401: Unauthorized`. Para obtener más información, consulte [los ejemplos a continuación](#net-example-from-this-sample).

## <a name="best-practices-for-proactive-messaging"></a>Procedimientos recomendados para la mensajería proactiva

El envío de mensajes proactivos a los usuarios es una manera eficaz de comunicarse con los usuarios. Sin embargo, desde la perspectiva del usuario, el mensaje aparece sin aprobaciones. Si hay un mensaje de bienvenida, será la primera vez que interactúen con la aplicación. Es importante usar esta funcionalidad y proporcionar la información completa al usuario para comprender el propósito de este mensaje.

Generalmente, los mensajes proactivos se divide en dos categorías: mensajes de bienvenida o notificaciones.

### <a name="welcome-messages"></a>Mensajes de bienvenida

Al usar la mensajería proactiva para enviar un mensaje de bienvenida a un usuario, asegúrese de que, desde la perspectiva del usuario, el mensaje aparece sin ser solicitado. Si hay un mensaje de bienvenida, será la primera vez que interactúen con la aplicación. Los mejores mensajes de bienvenida incluyen:

* **Por qué reciben este mensaje**: debería estar claro para el usuario por qué recibe este mensaje. Si el bot se instaló en un canal y envió un mensaje de bienvenida a todos los usuarios, hágales saber en qué canal se instaló y quién lo instaló.
* **Qué ofrece**: qué pueden hacer con la aplicación. ¿Qué valor puede aportarles?
* **Qué deben hacer a continuación**: invitar a los usuarios a probar un comando o interactuar con la aplicación.

### <a name="notification-messages"></a>Mensajes de notificación

Al usar mensajes proactivos para enviar notificaciones, necesita asegurarse de que los usuarios tengan una ruta clara para tomar acciones comunes basadas en la notificación y una clara comprensión del motivo de la notificación. Los buenos mensajes de notificación suelen incluir:

* **Qué ha ocurrido**: una indicación clara de lo que ha ocurrido para recibir la notificación.
* **Qué pasó con**: debe estar claro qué elemento u objeto se actualizó para provocar la notificación.
* **Quién o qué la activó**: quién o qué realizó la acción que provocó el envío de la notificación.
* **Qué pueden hacer los usuarios en respuesta**: facilite a los usuarios la realización de acciones basadas en sus notificaciones.
* **Cómo pueden optar por no participar**: proporcione una ruta de acceso para que los usuarios no puedan participar en notificaciones adicionales.

## <a name="obtain-necessary-user-information"></a>Obtención de la información de usuario necesaria

Los bots pueden crear nuevas conversaciones con un usuario individual de Microsoft Teams obteniendo el *identificador único* y el *identificador de inquilino* del usuario. Puede obtener estos valores mediante uno de los métodos siguientes:

* Al [capturar la lista de equipos](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) de un canal que está instalada la aplicación.
* Al almacenarlos en caché cuando un usuario [interactúa con el bot en un canal](~/resources/bot-v3/bot-conversations/bots-conv-channel.md).
* Cuando un usuario se [@mentioned en una conversación de canal](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) del que el bot forma parte.
* Al almacenarlos en caché al [recibir el evento `conversationUpdate`](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) cuando la aplicación está instalada en un ámbito personal, o se agregan nuevos miembros a un canal o chat de grupo.

### <a name="proactively-install-your-app-using-graph"></a>Instale proactivamente su aplicación con Graph

> [!Note]
> La instalación proactiva de aplicaciones con Graph está actualmente en versión beta.

En ocasiones, es posible que sea necesario enviar mensajes de forma proactiva a los usuarios que no hayan instalado o interactuado con la aplicación anteriormente. Por ejemplo, desea usar el [comunicador de la empresa](~/samples/app-templates.md#company-communicator) para enviar mensajes a toda la organización. En este escenario, puede usar la API de Graph para instalar proactivamente la aplicación para los usuarios y, a continuación, almacenar en caché los valores necesarios del evento `conversationUpdate` que recibirá la aplicación tras la instalación.

Solo puede instalar aplicaciones que se encuentran en el catálogo de aplicaciones de la organización o en la App Store de Teams.

Consulte [Instalación de aplicaciones para usuarios](/graph/api/userteamwork-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true) en la documentación de Graph para obtener detalles completos. También hay un [ejemplo en .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).

## <a name="examples"></a>Ejemplos

Asegúrese de autenticarse y tener un token de portador antes de crear una nueva conversación mediante la API de REST.

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

Debe proporcionar el identificador de usuario y el identificador de inquilino. Si la llamada se realiza correctamente, la API devuelve el siguiente objeto de respuesta:

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

Este identificador es el identificador de conversación único del chat personal. Almacenar este valor y reutilizarlo para futuras interacciones con el usuario.

### <a name="using-net"></a>Uso de .NET

En este ejemplo se usa el paquete [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) de NuGet.

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

El bot agregado por el equipo puede publicar en un canal para crear una nueva cadena de respuesta. Si usa el SDK de Node.js de Teams, use `startReplyChain()`, que proporciona una dirección completamente rellenada con el identificador de actividad y el identificador de conversación correctos. Si usa C#, consulte el ejemplo siguiente.

Como alternativa, puede usar la API de REST y emitir una solicitud POST al recurso [`/conversations`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation).

### <a name="net-example-from-this-sample"></a>Ejemplo de .NET (de [esta muestra](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs))

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

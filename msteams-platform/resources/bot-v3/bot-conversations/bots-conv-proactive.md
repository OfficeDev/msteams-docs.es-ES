---
title: Mensajes proactivos
description: Describe los bots que pueden iniciar una conversación en Microsoft Teams
keywords: 'Escenarios de teams: bot de conversación de mensajería proactiva'
ms.openlocfilehash: 8c93696f79b5d99c32162a7374c7d9adccacb984
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231627"
---
# <a name="proactive-messaging-for-bots"></a>Mensajería proactiva para bots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Un mensaje proactivo es un mensaje enviado por un bot para iniciar una conversación. Es posible que desee que el bot inicie una conversación por varios motivos, entre los que se incluyen:

* Mensajes de bienvenida para conversaciones de bots personales
* Respuestas de sondeo
* Notificaciones de eventos externos

El envío de un mensaje para iniciar un nuevo hilo de conversación es diferente al envío de un mensaje en respuesta a una conversación existente: cuando el bot inicia una nueva conversación, no hay ninguna conversación preexistida en la que publicar el mensaje. Para enviar un mensaje proactivo, necesita:

1. [Decide lo que vas a decir](#best-practices-for-proactive-messaging)
1. [Obtener el identificador único del usuario y el id. de espacio empresarial](#obtain-necessary-user-information)
1. [Enviar el mensaje](#examples)

Al crear mensajes proactivos, **debe** llamar y pasar la dirección URL del servicio antes de crear la que `MicrosoftAppCredentials.TrustServiceUrl` usará para enviar el `ConnectorClient` mensaje. Si no lo haces, la aplicación recibirá una `401: Unauthorized` respuesta. Vea [los ejemplos siguientes.](#net-example-from-this-sample)

## <a name="best-practices-for-proactive-messaging"></a>Procedimientos recomendados para mensajería proactiva

Enviar mensajes proactivos a los usuarios puede ser una forma muy eficaz de comunicarse con los usuarios. Sin embargo, desde su perspectiva, puede parecer que este mensaje no se muestra correctamente y, en el caso de los mensajes de bienvenida, será la primera vez que interactúen con la aplicación. Por lo tanto, es muy importante usar esta funcionalidad con moderación (no enviar correo no deseado a los usuarios) y proporcionarles información suficiente para que comprendan por qué se les envía un mensaje.

Los mensajes proactivos suelen estar en una de dos categorías: mensajes de bienvenida o notificaciones.

### <a name="welcome-messages"></a>Mensajes de bienvenida

Al usar la mensajería proactiva para enviar un mensaje de bienvenida a un usuario, debe tener en cuenta que para la mayoría de las personas que reciben el mensaje no tendrán contexto de por qué lo reciben. Esta también es la primera vez que interactuarán con la aplicación; es su oportunidad de crear una buena primera impresión. Entre los mensajes de bienvenida más importantes se incluyen:

* **¿Por qué reciben este mensaje?** Debe ser muy claro para el usuario por qué está recibiendo el mensaje. Si el bot se instaló en un canal y envió un mensaje de bienvenida a todos los usuarios, indálles en qué canal se instaló y quién lo instaló.
* **¿Qué ofrece?** ¿Qué pueden hacer con la aplicación? ¿Qué valor puede aportarles?
* **Qué deben hacer a continuación.** Invítelos a probar un comando o interactuar con la aplicación de alguna manera.

### <a name="notification-messages"></a>Mensajes de notificación

Al usar la mensajería proactiva para enviar notificaciones, debe asegurarse de que los usuarios tienen una ruta clara para realizar acciones comunes basadas en la notificación y una comprensión clara de por qué se produjo la notificación. Por lo general, los mensajes de notificación de buena calidad incluyen:

* **Qué ha pasado.** Una indicación clara de lo que ocurrió para provocar la notificación.
* **Qué ha ocurrido.** Debe estar claro qué elemento o elemento se actualizó para provocar la notificación.
* **Quién lo hizo.** Quién realizó la acción que provocó el envío de la notificación.
* **Lo que pueden hacer al respecto.** Facilita a los usuarios la realización de acciones en función de las notificaciones.
* **Cómo pueden optar por no participar.** Debes proporcionar una ruta de acceso para que los usuarios puedan optar por no recibir notificaciones adicionales.

## <a name="obtain-necessary-user-information"></a>Obtener la información de usuario necesaria

Los bots pueden crear nuevas conversaciones con un usuario individual de Microsoft Teams mediante la obtención del identificador único del usuario y *del* *inquilino.* Puede obtener estos valores mediante uno de los métodos siguientes:

* Mediante [la obtención de la lista de equipo](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) desde un canal en el que está instalada la aplicación.
* Al almacenarlos en caché cuando un usuario [interactúa con el bot en un canal.](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)
* Cuando un usuario está [@mentioned en una conversación de canal](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) de la que forma parte el bot.
* Al almacenarlos en [ `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) caché cuando recibe el evento cuando la aplicación está instalada en un ámbito personal, o cuando se agregan nuevos miembros a un canal o chat de grupo que

### <a name="proactively-install-your-app-using-graph"></a>Instalar de forma proactiva la aplicación con Graph

> [!Note]
> La instalación proactiva de aplicaciones con graph se encuentra actualmente en la versión beta.

En ocasiones, puede que sea necesario enviar mensajes de forma proactiva a los usuarios que no han instalado o interactuado con la aplicación anteriormente. Por ejemplo, desea usar el comunicador de la empresa [para](~/samples/app-templates.md#company-communicator) enviar mensajes a toda la organización. Para este escenario, puede usar la API de Graph para instalar de forma proactiva la aplicación para los usuarios y, a continuación, almacenar en caché los valores necesarios del evento que la aplicación recibirá al `conversationUpdate` instalarse.

Solo puede instalar aplicaciones que se encuentran en el catálogo de aplicaciones de su organización o en la tienda de aplicaciones de Teams.

Consulte [Instalar aplicaciones para usuarios en](/graph/teams-proactive-messaging) la documentación de Graph para obtener más información. También hay un [ejemplo en .NET.](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)

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

Debe proporcionar el id. de usuario y el id. de inquilino. Si la llamada se realiza correctamente, la API devuelve el siguiente objeto de respuesta.

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

Este identificador es el identificador de conversación único del chat personal. Almacene este valor y reutilice para futuras interacciones con el usuario.

### <a name="using-net"></a>Uso de .NET

En este ejemplo se usa [el paquete NuGet Microsoft.Bot.Connector.Teams.](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)

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

*Vea también ejemplos* [de Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)

## <a name="creating-a-channel-conversation"></a>Creación de una conversación de canal

El bot agregado por el equipo puede publicar en un canal para crear una nueva cadena de respuesta. Si usa el SDK de Node.js Teams, use el que le proporciona una dirección completa con el identificador de actividad y el identificador de `startReplyChain()` conversación correctos. Si usa C#, vea el siguiente ejemplo.

Como alternativa, puede usar la API de REST y emitir una solicitud POST al [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) recurso.

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

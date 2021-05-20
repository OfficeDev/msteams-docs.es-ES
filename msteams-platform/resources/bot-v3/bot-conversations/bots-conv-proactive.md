---
title: Mensajes proactivos
description: Describe que los bots pueden iniciar una conversación en Microsoft Teams
ms.topic: conceptual
localization_priority: Normal
keywords: equipos escenarios de mensajería proactiva conversación bot
ms.openlocfilehash: baf148d0f4d0a669de582dfca70ed5d5bed0274c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566792"
---
# <a name="proactive-messaging-for-bots"></a>Mensajería proactiva para bots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Un mensaje proactivo es un mensaje enviado por un bot para iniciar una conversación. Puede que quiera que el bot inicie una conversación por varios motivos, entre los que se incluyen:

* Mensajes de bienvenida para conversaciones personales con bots.
* Respuestas de las encuestas.
* Notificaciones de eventos externos.

Enviar un mensaje para iniciar un nuevo subproceso de conversación es diferente de enviar un mensaje en respuesta a una conversación existente: cuando el bot inicia una nueva conversación, no hay ninguna conversación preexistente a la que publicar el mensaje. Para enviar un mensaje proactivo usted necesita:

1. [Decide lo que vas a decir](#best-practices-for-proactive-messaging)
1. [Obtenga el identificador único del usuario y el identificador de inquilino](#obtain-necessary-user-information)
1. [Enviar el mensaje](#examples)

Al crear mensajes **proactivos, debe** llamar y pasar la dirección URL del servicio antes de crear el `MicrosoftAppCredentials.TrustServiceUrl` que `ConnectorClient` usará para enviar el mensaje. Si no lo hace, la aplicación recibirá una `401: Unauthorized` respuesta. Para obtener más información, consulte [los ejemplos siguientes](#net-example-from-this-sample).

## <a name="best-practices-for-proactive-messaging"></a>Mejores prácticas para la mensajería proactiva

Enviar mensajes proactivos a los usuarios puede ser una forma muy eficaz de comunicarse con sus usuarios. Sin embargo, desde su perspectiva este mensaje puede parecer que viene a ellos completamente sin probar, y en el caso de los mensajes de bienvenida será la primera vez que hayan interactuado con la aplicación. Como tal, es muy importante utilizar esta funcionalidad con moderación (no enviar spam a los usuarios), y proporcionarles suficiente información para permitirles entender por qué se les está enviando mensajes.

Generalmente, los mensajes proactivos se divide en dos categorías: mensajes de bienvenida o notificaciones.

### <a name="welcome-messages"></a>Mensajes de bienvenida

Al usar mensajes proactivos para enviar un mensaje de bienvenida a un usuario, debe tener en cuenta que para la mayoría de las personas que reciben el mensaje no tendrán contexto por qué lo reciben. Esta es también la primera vez que habrán interactuado con la aplicación; es su oportunidad de crear una buena primera impresión. Los mejores mensajes de bienvenida incluirán:

* **¿Por qué están recibiendo este mensaje?** Debe ser muy claro para el usuario por qué está recibiendo el mensaje. Si el bot se instaló en un canal y envió un mensaje de bienvenida a todos los usuarios, hágales saber en qué canal se instaló y potencialmente quién lo instaló.
* **¿Qué ofreces?** ¿Qué pueden hacer con tu aplicación? ¿Qué valor puedes aportarles?
* **¿Qué deberían hacer a continuación?** Invítelos a probar un comando o interactuar con la aplicación de alguna manera.

### <a name="notification-messages"></a>Mensajes de notificación

Al usar mensajes proactivos para enviar notificaciones, debe asegurarse de que los usuarios tienen una ruta clara para realizar acciones comunes basadas en la notificación y una comprensión clara de por qué se produjo la notificación. Los buenos mensajes de notificación generalmente incluirán:

* **Qué ha pasado.** Una clara indicación de lo que sucedió para causar la notificación.
* **A qué le pasó.** Debe estar claro qué elemento/cosa se actualizó para causar la notificación.
* **Quién lo hizo.** Quién tomó la medida que provocó el envío de la notificación.
* **Lo que pueden hacer al respecto.** Facilite a los usuarios la real realo de acciones basadas en sus notificaciones.
* **Cómo pueden optar por no participar.** Debe proporcionar una ruta para que los usuarios opten por no recibir notificaciones adicionales.

## <a name="obtain-necessary-user-information"></a>Obtener la información necesaria del usuario

Los bots pueden crear nuevas conversaciones con un usuario Microsoft Teams individual obteniendo el *identificador único* del usuario y el identificador de *inquilino.* Puede obtener estos valores utilizando uno de los métodos siguientes:

* Al [obtener la lista](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) de equipos de un canal en el que está instalada la aplicación.
* Al almacenarlos en caché cuando un usuario [interactúa con el bot en un canal.](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)
* Cuando un usuario está [@mentioned en una conversación de canal](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) del que forma parte el bot.
* Al almacenarlos en caché cuando [recibes el `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) evento cuando la aplicación está instalada en un ámbito personal, o se agregan nuevos miembros a un canal o chat de grupo que.

### <a name="proactively-install-your-app-using-graph"></a>Instale de forma proactiva la aplicación con Graph

> [!Note]
> La instalación proactiva de aplicaciones mediante el gráfico está actualmente en fase beta.

En ocasiones, puede ser necesario enviar mensajes de forma proactiva a los usuarios que no han instalado o interactuado con la aplicación anteriormente. Por ejemplo, desea usar el [comunicador de empresa](~/samples/app-templates.md#company-communicator) para enviar mensajes a toda la organización. Para este escenario, puede usar la API de Graph para instalar de forma proactiva la aplicación para los usuarios y, a continuación, almacenar en caché los valores necesarios del evento que recibirá la `conversationUpdate` aplicación al instalarse.

Solo puedes instalar aplicaciones que estén en tu catálogo de aplicaciones organizativas o en la tienda de aplicaciones Teams.

Consulte [Instalar aplicaciones para usuarios](/graph/teams-proactive-messaging) en la documentación de Graph para obtener detalles completos. También hay un [ejemplo en .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).

## <a name="examples"></a>Ejemplos

Asegúrese de autenticar y tener un token de portador antes de crear una nueva conversación mediante la API de REST.

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

Debe proporcionar el IDENTIFICADOR de usuario y el identificador de inquilino. Si la llamada se realiza correctamente, la API devuelve con el siguiente objeto de respuesta.

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

Este ID es el ID de conversación único del chat personal. Por favor, almacene este valor y reutilízcalo para futuras interacciones con el usuario.

### <a name="using-net"></a>Uso de .NET

En este ejemplo se usa el paquete [NuGet Microsoft.Bot.Connector.Teams.](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)

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

El bot agregado por el equipo puede publicar en un canal para crear una nueva cadena de respuesta. Si usa el SDK de Node.js Teams, use `startReplyChain()` el que le proporciona una dirección completamente rellenada con el identificador de actividad y el identificador de conversación correctos. Si está utilizando C#, consulte el ejemplo siguiente.

Como alternativa, puede usar la API de REST y emitir una solicitud POST para [`/conversations`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) obtener recursos.

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

## <a name="see-also"></a>Vea también

[Muestras de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
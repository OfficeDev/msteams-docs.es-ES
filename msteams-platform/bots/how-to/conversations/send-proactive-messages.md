---
title: Envío de mensajes proactivos
author: clearab
description: Cómo enviar mensajes proactivos con su bot de Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2dfb8e18243079ca38d505f4b80deb7abf2de32f
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874852"
---
# <a name="send-proactive-messages"></a>Envío de mensajes proactivos

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

Un mensaje proactivo es cualquier mensaje enviado por un bot que no responde directamente a una solicitud de un usuario. Esto puede incluir mensajes como:

* Mensajes de bienvenida
* Notificaciones
* Mensajes programados

Para que el bot envíe un mensaje proactivo, debe tener acceso al usuario, al chat de grupo o al equipo al que desea enviar el mensaje. Para un equipo o chat de grupo, esto significa que la aplicación que contiene el bot debe instalarse primero en esa ubicación. Puede [instalar de forma proactiva su aplicación con Graph](#proactively-install-your-app-using-graph) en un equipo si es necesario o usar una [Directiva de aplicación](/microsoftteams/teams-custom-app-policies-and-settings) para insertar aplicaciones en Microsoft Teams y los usuarios de su inquilino. Para los usuarios, su aplicación debe estar instalada para ese usuario o bien el usuario debe formar parte de un equipo en el que se instale la aplicación.

El envío de un mensaje proactivo es diferente al envío de un mensaje normal, ya que no tendrá un activo `turnContext` que usar para responder. Es posible que también necesite crear la conversación (por ejemplo, un nuevo chat uno a uno o un nuevo hilo de conversación en un canal) antes de enviar el mensaje. No puede crear un nuevo chat de grupo o un nuevo canal en un equipo con mensajería proactiva.

En un nivel alto, los pasos que tendrá que completar para enviar un mensaje proactivo son los siguientes:

1. [Obtenga el identificador de usuario o de equipo o de canal](#get-the-user-id-or-teamchannel-id) (si es necesario).
1. [Cree la conversación o hilo de conversación](#create-the-conversation) (si es necesario).
1. [Obtener el identificador de la conversación](#get-the-conversation-id).
1. [Enviar el mensaje](#send-the-message).

Los fragmentos de código de la sección de [ejemplos](#examples) que se muestran a continuación son para crear una conversación de uno a uno, consulte la sección [referencias](#references) para obtener vínculos para completar ejemplos de trabajo para conversaciones de uno a una y grupo/canales.

## <a name="get-the-user-id-or-teamchannel-id"></a>Obtener el identificador de usuario o de equipo o de canal

Si necesita crear una conversación o un hilo de conversación nuevos en un canal, primero necesitará el identificador correcto para crear la conversación. Puede recibir o recuperar este identificador de varias formas:

1. Cuando la aplicación está instalada en un contexto determinado, recibirá una [ `onMembersAdded` actividad](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
1. Cuando se agrega un nuevo usuario a un contexto donde la aplicación está instalada, recibirá una [ `onMembersAdded` actividad](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
1. Puede recuperar la [lista de canales](~/bots/how-to/get-teams-context.md) en un equipo en el que está instalada la aplicación.
1. Puede recuperar la [lista de miembros](~/bots/how-to/get-teams-context.md) de un equipo en el que está instalada la aplicación.
1. Cada actividad que recibe el bot contendrá la información necesaria.

Independientemente de cómo obtenga la información, tendrá que almacenar el `tenantId` y el `userId` o `channelId` para crear una nueva conversación. También puede usar el `teamId` para crear una nueva secuencia de conversación en el canal general/predeterminado de un equipo.

El `userId` es único para el identificador de Bot y un usuario en particular, no puede volver a usarlos entre bots. El `channelId` es global, sin embargo, el bot _debe_ estar instalado en el equipo para poder enviar un mensaje proactivo a un canal.

## <a name="create-the-conversation"></a>Crear la conversación

Una vez que tenga la información de usuario/canal, tendrá que crear la conversación si todavía no existe (o no sabe la `conversationId` ). Solo debe crear la conversación una vez; Asegúrese de almacenar el `conversationId` valor o el `conversationReference` objeto que se va a usar en el futuro.

## <a name="get-the-conversation-id"></a>Obtener el identificador de conversación

Una vez que se haya creado la conversación, deberá usar el `conversationReference` objeto o el `conversationId` y el `tenantId` para enviar el mensaje. Puede obtener este identificador si crea la conversación o la almacena desde cualquier actividad que se le envíe desde ese contexto. Asegúrese de almacenar este identificador.

## <a name="send-the-message"></a>Enviar el mensaje

Ahora que tiene la información de dirección correcta, puede enviar el mensaje. Si estás usando el SDK, tendrás que hacerlo usando el `continueConversation` método y el `conversationId` y `tenantId` para realizar una llamada directa a la API.  Necesitará configurar `conversationParameters` correctamente para que el mensaje se envíe correctamente; vea los [ejemplos](#examples) siguientes o use uno de los ejemplos que se enumeran en la sección [referencias](#references) .

## <a name="best-practices-for-proactive-messaging"></a>Procedimientos recomendados para la mensajería proactiva

El envío de mensajes proactivos a los usuarios puede ser una forma muy eficaz de comunicarse con los usuarios. Sin embargo, desde su perspectiva, este mensaje puede aparecer completamente sin intervención del usuario y, en el caso de los mensajes de bienvenida, será la primera vez que interactuen con la aplicación. Por lo tanto, es muy importante usar esta funcionalidad con moderación (no enviar correo no deseado a los usuarios) y proporcionar suficiente información para que los usuarios sepan por qué se les está enviando un mensaje.

### <a name="welcome-messages"></a>Mensajes de bienvenida

Al usar la mensajería proactiva para enviar un mensaje de bienvenida a un usuario, debe tener en cuenta que, en la mayoría de las personas que reciben el mensaje, no habrá ningún contexto para la razón por la cual lo reciben. También es la primera vez que interactuarán con la aplicación; es su oportunidad para crear una buena primera impresión. Los mejores mensajes de bienvenida incluirán:

* **Por qué un usuario recibe el mensaje.** El usuario debe ser muy claro por qué reciben el mensaje. Si el bot se ha instalado en un canal y se ha enviado un mensaje de bienvenida a todos los usuarios, hágales saber en qué canal se ha instalado y que podrían instalarlo.
* **Qué ofrece.** ¿Qué puede hacer con la aplicación? ¿Qué valor puede aportar a ellos?
* **Qué debería hacer a continuación.** Invitar a probar un comando o interactuar con la aplicación de alguna manera.

Recuerde que los mensajes de bienvenida deficientes pueden dar lugar a que los usuarios bloqueen su bot. Debe dedicar mucho tiempo a elaborar los mensajes de bienvenida y realizar iteraciones en ellos si no tienen el efecto deseado.

### <a name="notification-messages"></a>Mensajes de notificación

Al usar la mensajería proactiva para enviar notificaciones, debe asegurarse de que los usuarios tienen una ruta de acceso clara para emprender acciones comunes en función de la notificación y un conocimiento claro de la razón por la que se produjo la notificación. Por lo general, los mensajes de notificación son correctos:

* **Qué ha pasado.** Una indicación clara de lo que ha sucedido para provocar la notificación.
* **Cuál era el resultado.** Debe estar claro qué elemento/Thing se actualizó para provocar la notificación.
* **Quién/lo ha desencadenado.** Quién o qué emprendió acciones que hacían que se enviara la notificación.
* **Qué pueden hacer los usuarios en respuesta.** Facilite a los usuarios que realicen acciones basadas en las notificaciones.
* **Cómo pueden deselegir los usuarios.** Debe proporcionar una ruta de acceso para que los usuarios puedan optar por las notificaciones adicionales.

## <a name="proactively-install-your-app-using-graph"></a>Instalar de forma proactiva la aplicación con Graph

> [!Note]
> La instalación de aplicaciones con Microsoft Graph de forma proactiva se encuentra actualmente en versión beta.

En ocasiones, es posible que sea necesario enviar un mensaje de forma proactiva a los usuarios que no hayan instalado ni interactúen con la aplicación anteriormente. Por ejemplo, desea usar el Communicator de la [compañía](~/samples/app-templates.md#company-communicator) para enviar mensajes a toda la organización. Para este escenario, puede usar la API de Graph para instalar proactivamente la aplicación para sus usuarios y, a continuación, almacenar en caché los valores necesarios del `conversationUpdate` evento que la aplicación recibirá en el momento de la instalación.

Solo puede instalar aplicaciones que estén en el catálogo de aplicaciones de la organización o en la tienda de aplicaciones de Teams.

Consulte [instalar aplicaciones para usuarios](/graph/teams-proactive-messaging) en la documentación de Graph y la [instalación y mensajería de robots proactivas en Teams con Microsoft Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md). También hay un [ejemplo de Microsoft .NET Framework](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)  en la plataforma de github.

## <a name="examples"></a>Ejemplos

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
private async Task MessageAllMembersAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var teamsChannelId = turnContext.Activity.TeamsGetChannelId();
    var serviceUrl = turnContext.Activity.ServiceUrl;
    var credentials = new MicrosoftAppCredentials(_appId, _appPassword);
    ConversationReference conversationReference = null;

    //Get the set of member IDs to send the message to
    var members = await GetPagedMembers(turnContext, cancellationToken);

    foreach (var teamMember in members)
    {
        var proactiveMessage = MessageFactory.Text($"Hello {teamMember.GivenName} {teamMember.Surname}. I'm a Teams conversation bot.");

        var conversationParameters = new ConversationParameters
        {
            IsGroup = false,
            Bot = turnContext.Activity.Recipient,
            Members = new ChannelAccount[] { teamMember },
            TenantId = turnContext.Activity.Conversation.TenantId,
        };
        //create the new one-to-one conversations
        await ((BotFrameworkAdapter)turnContext.Adapter).CreateConversationAsync(
            teamsChannelId,
            serviceUrl,
            credentials,
            conversationParameters,
            async (t1, c1) =>
            {
                //Get the conversationReference
                conversationReference = t1.Activity.GetConversationReference();
                //Send the proactive message
                await ((BotFrameworkAdapter)turnContext.Adapter).ContinueConversationAsync(
                    _appId,
                    conversationReference,
                    async (t2, c2) =>
                    {
                        await t2.SendActivityAsync(proactiveMessage, c2);
                    },
                    cancellationToken);
            },
            cancellationToken);
    }

    await turnContext.SendActivityAsync(MessageFactory.Text("All messages have been sent."), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```javascript

async messageAllMembersAsync(context) {
    const members = await this.getPagedMembers(context);

    members.forEach(async (teamMember) => {
        const message = MessageFactory.text('Hello ${ teamMember.givenName } ${ teamMember.surname }. I\'m a Teams conversation bot.');

        var ref = TurnContext.getConversationReference(context.activity);
        ref.user = teamMember;

        await context.adapter.createConversation(ref,
            async (t1) => {
                const ref2 = TurnContext.getConversationReference(t1.activity);
                await t1.adapter.continueConversation(ref2, async (t2) => {
                    await t2.sendActivity(message);
                });
            });
    });

    await context.sendActivity(MessageFactory.text('All messages have been sent.'));
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def _message_all_members(self, turn_context: TurnContext):
    team_members = await self._get_paged_members(turn_context)

    for member in team_members:
        conversation_reference = TurnContext.get_conversation_reference(
            turn_context.activity
        )

        conversation_parameters = ConversationParameters(
            is_group=False,
            bot=turn_context.activity.recipient,
            members=[member],
            tenant_id=turn_context.activity.conversation.tenant_id,
        )

        async def get_ref(tc1):
            conversation_reference_inner = TurnContext.get_conversation_reference(
                tc1.activity
            )
            return await tc1.adapter.continue_conversation(
                conversation_reference_inner, send_message, self._app_id
            )

        async def send_message(tc2: TurnContext):
            return await tc2.send_activity(
                f"Hello {member.name}. I'm a Teams conversation bot."
            )

        await turn_context.adapter.create_conversation(
            conversation_reference, get_ref, conversation_parameters
        )

    await turn_context.send_activity(
        MessageFactory.text("All messages have been sent")
    )

```

# <a name="json"></a>[JSON](#tab/json)

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

---

## <a name="references"></a>Referencias

A continuación se enumeran los ejemplos de mensajería proactiva oficial.

|  No.  | Nombre de ejemplo           | Description                                                                      | .NET    | JavaScript   | Python  |
|:--:|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|57|Conceptos básicos de la conversación de Microsoft Teams  | Muestra los conceptos básicos de las conversaciones en Microsoft Teams, incluido el envío de mensajes proactivos de uno a uno.|[.NET &nbsp; Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|58|Iniciar un nuevo hilo en un canal     | Muestra cómo crear un nuevo hilo en un canal. |[.NET &nbsp; Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

En el siguiente ejemplo se muestra la cantidad mínima de información necesaria para enviar un mensaje proactivo (sin usar un `conversationReference` objeto). Este ejemplo puede resultar útil si está usando llamadas API de REST directamente o si no ha almacenado `conversationReference` objetos completos.

* [Mensajería proactiva de Microsoft Teams](https://github.com/clearab/teamsProactiveMessaging)

## <a name="view-additional-code"></a>Ver código adicional
>
> [!div class="nextstepaction"]
> [**Ejemplos de código de mensajería proactiva de Microsoft Teams**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
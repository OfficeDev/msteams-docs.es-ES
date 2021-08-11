---
title: Enviar mensajes proactivos
description: Describe cómo enviar mensajes proactivos con el Microsoft Teams bot.
ms.topic: conceptual
ms.author: anclear
localization_priority: Normal
Keywords: enviar un mensaje obtener id. de usuario Id. id. de conversación de conversación
ms.openlocfilehash: 5a999769879c8661d16b79f885b463166be557903a6448c709eb06ed16e49345
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2021
ms.locfileid: "57705703"
---
# <a name="proactive-messages"></a>Mensajes proactivos

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

Un mensaje proactivo es cualquier mensaje enviado por un bot que no responde a una solicitud de un usuario. Esto puede incluir mensajes, como:

* Mensajes de bienvenida
* Notificaciones
* Mensajes programados

Para que el bot envíe un mensaje proactivo a un usuario, chat de grupo o equipo, debe tener acceso para enviar el mensaje. Para un chat de grupo o un equipo, la aplicación que contiene el bot debe instalarse primero en esa ubicación. Puedes instalar [proactivamente](#proactively-install-your-app-using-graph) la aplicación con Microsoft Graph en un equipo, [](/microsoftteams/teams-custom-app-policies-and-settings) si es necesario, o usar una directiva de aplicación para enviar aplicaciones a equipos y usuarios de tu inquilino. Para los usuarios, la aplicación debe estar instalada para el usuario o el usuario debe formar parte de un equipo donde esté instalada la aplicación.

Enviar un mensaje proactivo es diferente del envío de un mensaje normal. No hay ningún activo `turnContext` que usar para una respuesta. Debe crear la conversación antes de enviar el mensaje. Por ejemplo, un nuevo chat uno a uno o un nuevo hilo de conversación en un canal. No puede crear un nuevo chat de grupo o un nuevo canal en un equipo con mensajería proactiva.

**Para enviar un mensaje proactivo**

1. [Obtiene el id. de usuario, id. de equipo o id. de canal,](#get-the-user-id-team-id-or-channel-id)si es necesario.
1. [Cree la conversación](#create-the-conversation), si es necesario.
1. [Obtener el identificador de conversación](#get-the-conversation-id).
1. [Enviar el mensaje](#send-the-message).

Los fragmentos de código de la [sección samples](#samples) son para crear una conversación uno a uno. Para ver los vínculos a ejemplos de trabajo completos para conversaciones uno a uno y grupos o canales, vea [el ejemplo de código](#code-sample).

Para usar mensajes proactivos de forma eficaz, vea [procedimientos recomendados para la mensajería proactiva.](#best-practices-for-proactive-messaging) Para determinados escenarios, debes [instalar proactivamente la aplicación con Graph](#proactively-install-your-app-using-graph). Los fragmentos de código de la [sección samples](#samples) son para crear una conversación uno a uno. Para obtener ejemplos de trabajo completos para conversaciones uno a uno y grupos o canales, vea [el ejemplo de código](#code-sample).

## <a name="get-the-user-id-team-id-or-channel-id"></a>Obtener el id. de usuario, id. de equipo o id. de canal

Para crear un nuevo hilo de conversación o conversación en un canal, debe tener el identificador correcto. Puede recibir o recuperar este identificador con cualquiera de las siguientes opciones:

* Cuando la aplicación está instalada en un contexto determinado, recibes una [ `onMembersAdded` actividad](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* Cuando se agrega un nuevo usuario a un contexto donde está instalada la aplicación, recibes una [ `onMembersAdded` actividad](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* Puedes recuperar la [lista de canales](~/bots/how-to/get-teams-context.md) de un equipo donde está instalada la aplicación.
* Puedes recuperar la [lista de miembros](~/bots/how-to/get-teams-context.md) de un equipo donde está instalada la aplicación.
* Cada actividad que recibe el bot debe contener la información necesaria.

Independientemente de cómo obtenga la información, debe almacenar el o para `tenantId` `userId` crear una nueva `channelId` conversación. También puede usar el para crear un nuevo subproceso de conversación en el canal `teamId` general o predeterminado de un equipo.

El `userId` es único para el identificador del bot y un usuario en particular. No puede volver a usar `userId` los bots entre. El `channelId` es global. Sin embargo, el bot debe instalarse en el equipo para poder enviar un mensaje proactivo a un canal.

Después de tener la información del usuario o del canal, debe crear la conversación.

## <a name="create-the-conversation"></a>Crear la conversación

Debe crear la conversación si no existe o si no conoce el `conversationId` archivo . Solo debe crear la conversación una vez y almacenar el `conversationId` valor u `conversationReference` objeto.

Después de crear la conversación, debe obtener el identificador de conversación.

## <a name="get-the-conversation-id"></a>Obtener el identificador de conversación

Use el `conversationReference` objeto o y envíe el `conversationId` `tenantId` mensaje. Para obtener este identificador, puede crear la conversación o almacenarla desde cualquier actividad que se le envíe desde ese contexto. Almacene este identificador como referencia.

Después de obtener la información de dirección adecuada, puede enviar el mensaje.

## <a name="send-the-message"></a>Enviar el mensaje

Ahora que tiene la información de dirección correcta, puede enviar el mensaje. Si usa el SDK, debe usar el método `continueConversation` y y realizar una llamada directa a la `conversationId` `tenantId` API. Debe establecer `conversationParameters` correctamente para enviar correctamente el mensaje. Vea la [sección de](#samples) ejemplos o use uno de los ejemplos enumerados en la sección de [ejemplo de](#code-sample) código.

Ahora que ha enviado el mensaje proactivo, debe seguir estos procedimientos recomendados mientras envía mensajes proactivos para un mejor intercambio de información entre los usuarios y el bot.

## <a name="best-practices-for-proactive-messaging"></a>Procedimientos recomendados para mensajería proactiva

Enviar mensajes proactivos a los usuarios es una forma muy eficaz de comunicarse con los usuarios. Sin embargo, desde su punto de vista, este mensaje puede aparecer completamente sin respuesta y, en el caso de los mensajes de bienvenida, es la primera vez que interactúan con la aplicación. Por lo tanto, es muy importante usar la mensajería proactiva con moderación, no enviar correo no deseado a los usuarios y proporcionar suficiente información para que los usuarios comprendan por qué están recibiendo los mensajes.

### <a name="welcome-messages"></a>Mensajes de bienvenida

Cuando se usa la mensajería proactiva para enviar un mensaje de bienvenida a un usuario, no hay contexto para la razón por la que los usuarios reciben el mensaje. También es la primera vez que los usuarios interactúan con la aplicación. Es una oportunidad para crear una buena primera impresión. Los mejores mensajes de bienvenida deben incluir:

* Por qué un usuario recibe el mensaje: debe ser muy claro para el usuario por qué está recibiendo el mensaje. Si el bot se instaló en un canal y envió un mensaje de bienvenida a todos los usuarios, háles saber en qué canal se instaló y quién lo instaló.
* Qué ofrece: los usuarios deben ser capaces de identificar lo que pueden hacer con la aplicación y qué valor puede aportarles.
* Qué deben hacer a continuación: Invitar a los usuarios a probar un comando o interactuar con la aplicación.

Los mensajes de bienvenida deficientes pueden provocar que los usuarios bloqueen el bot. Escribe en el punto y borra los mensajes de bienvenida. Itera en los mensajes de bienvenida si no tienen el efecto deseado.

### <a name="notification-messages"></a>Mensajes de notificación

Para enviar notificaciones mediante mensajería proactiva, asegúrese de que los usuarios tienen una ruta de acceso clara para realizar acciones comunes en función de la notificación. Asegúrese de que los usuarios comprendan claramente por qué han recibido una notificación. Por lo general, los mensajes de notificación de buena calidad incluyen lo siguiente:

* Qué ocurrió: una indicación clara de lo que ocurrió para provocar la notificación.
* Cuál fue el resultado: debe estar claro qué elemento se actualizó para provocar la notificación.
* Quién o lo que lo desencadenó: Quién o qué acción llevó a que se enviara la notificación.
* Qué pueden hacer los usuarios en respuesta: facilita que los usuarios realicen acciones en función de las notificaciones.
* Cómo pueden optar por no participar los usuarios: debe proporcionar una ruta de acceso para que los usuarios no puedan participar en notificaciones adicionales.

Para enviar mensajes a un gran grupo de usuarios, por ejemplo, a su organización, instale proactivamente la aplicación mediante Graph.

### <a name="scheduled-messages"></a>Mensajes programados

Al usar la mensajería proactiva para enviar mensajes programados a los usuarios, compruebe que la zona horaria se actualiza a su zona horaria. Esto garantiza que los mensajes se entreguen a los usuarios en el momento correspondiente. Por lo general, los mensajes de programación incluyen:

* ¿Por qué recibe el usuario el mensaje?: Haga que sea fácil para los usuarios comprender el motivo por el que están recibiendo el mensaje.
* Qué puede hacer el usuario a continuación: los usuarios pueden realizar la acción necesaria en función del contenido del mensaje.

## <a name="proactively-install-your-app-using-graph"></a>Instale proactivamente la aplicación con Graph

> [!Note]
> La instalación proactiva de aplicaciones Graph está actualmente en versión beta.

Envía un mensaje de forma proactiva a los usuarios que no han instalado o interactuado anteriormente con la aplicación. Por ejemplo, desea usar el comunicador de la compañía [para](~/samples/app-templates.md#company-communicator) enviar mensajes a toda la organización. En este caso, puedes usar la API Graph para instalar proactivamente la aplicación para los usuarios. Almacena en caché los valores necesarios del `conversationUpdate` evento que la aplicación recibe al instalarlo.

Solo puedes instalar aplicaciones que estén en el catálogo de aplicaciones de la organización o en Teams App Store.

Consulta [instalar aplicaciones para usuarios en](/graph/api/userteamwork-post-installedapps) la documentación Graph y la instalación proactiva de [bots](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)y la mensajería en Teams con Graph . También hay un ejemplo [de Microsoft .NET Framework](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) en la plataforma GitHub.

## <a name="samples"></a>Ejemplos

El siguiente código muestra cómo enviar mensajes proactivos:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
[Route("api/notify")]
[ApiController]
public class NotifyController : ControllerBase
{
    private readonly IBotFrameworkHttpAdapter _adapter;
    private readonly string _appId;
    private readonly ConcurrentDictionary<string, ConversationReference> _conversationReferences;

    public NotifyController(IBotFrameworkHttpAdapter adapter, IConfiguration configuration, ConcurrentDictionary<string, ConversationReference> conversationReferences)
    {
        _adapter = adapter;
        _conversationReferences = conversationReferences;
        _appId = configuration["MicrosoftAppId"] ?? string.Empty;
    }

    public async Task<IActionResult> Get()
    {
        foreach (var conversationReference in _conversationReferences.Values)
        {
            await ((BotAdapter)_adapter).ContinueConversationAsync(_appId, conversationReference, BotCallback, default(CancellationToken));
        }
        
        // Let the caller know proactive messages have been sent
        return new ContentResult()
        {
            Content = "<html><body><h1>Proactive messages have been sent.</h1></body></html>",
            ContentType = "text/html",
            StatusCode = (int)HttpStatusCode.OK,
        };
    }

    private async Task BotCallback(ITurnContext turnContext, CancellationToken cancellationToken)
    {
        // If you encounter permission-related errors when sending this message, see
        // https://aka.ms/BotTrustServiceUrl
        await turnContext.SendActivityAsync("proactive hello");
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

Debe proporcionar el identificador de usuario y el identificador de inquilino. Si la llamada se realiza correctamente, la API devuelve el siguiente objeto de respuesta:

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

> [!NOTE]
> Actualmente, los bots no pueden crear un chat de grupo a través de API de bots o Graph. `createConversation` solo está disponible para chats 1:1.

## <a name="code-sample"></a>Ejemplo de código

En la tabla siguiente se proporciona un ejemplo de código simple que incorpora el flujo de conversación básico en una aplicación de Teams y cómo crear un nuevo subproceso de conversación en un canal en Teams:

| **Nombre de ejemplo** | **Descripción** | **.NET** | **Node.js** | **Python** |
|---------------|--------------|--------|-------------|--------|
| Teams Conceptos básicos de conversación  | Muestra los conceptos básicos de las conversaciones Teams, incluido el envío de mensajes proactivos de uno a uno.| [Ver](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot) | [Ver](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [Ver](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot) |
| Iniciar nuevo subproceso en un canal | Muestra la creación de un nuevo subproceso en un canal. | [Ver](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel) | [Ver](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel) | [Ver](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |
| Instalación proactiva de la aplicación y envío de notificaciones proactivas | En este ejemplo se muestra cómo usar la instalación proactiva de la aplicación para los usuarios y enviar notificaciones proactivas llamando a las API Graph Microsoft. | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/csharp) | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/nodejs) | |

### <a name="additional-code-sample"></a>Ejemplo de código adicional

> [!div class="nextstepaction"]
> [Teams de código de mensajería proactiva](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)

## <a name="see-also"></a>Vea también

[**Teams de código de mensajería proactiva**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Formatear los mensajes del bot](~/bots/how-to/format-your-bot-messages.md)

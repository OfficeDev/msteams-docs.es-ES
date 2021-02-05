---
title: enviar mensajes proactivos
description: describe cómo enviar mensajes proactivos con el bot de Microsoft Teams.
ms.topic: overview
ms.author: anclear
Keywords: enviar un mensaje para obtener el id. de usuario id. de la conversación de conversación de id. de canal
ms.openlocfilehash: 2d7ff10469a181bb06fda5029c8f6b2725b0402d
ms.sourcegitcommit: 7db6eabe3ef128ac7f14b32d07e9e86c995d187f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/04/2021
ms.locfileid: "50103608"
---
# <a name="send-proactive-messages"></a>Enviar mensajes proactivos

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

Un mensaje proactivo es cualquier mensaje enviado por un bot que no está en respuesta directa a una solicitud de un usuario. Esto puede incluir mensajes como:

* Mensajes de bienvenida
* Notificaciones
* Mensajes programados

Para que el bot envíe un mensaje proactivo, debe tener acceso al usuario, al chat en grupo o al equipo al que desea enviar el mensaje. Para un chat de grupo o equipo, esto significa que la aplicación que contiene el bot debe instalarse primero en esa ubicación. Puede instalar [la aplicación de](#proactively-install-your-app-using-graph) forma proactiva con Graph [](/microsoftteams/teams-custom-app-policies-and-settings) en un equipo, si es necesario o usar una directiva de aplicación para enviar aplicaciones a equipos y usuarios de su espacio empresarial. Para los usuarios, la aplicación debe estar instalada para el usuario o el usuario debe formar parte de un equipo donde esté instalada la aplicación.

El envío de un mensaje proactivo es diferente al envío de un mensaje normal. En ese caso, no hay ningún activo `turnContext` para usar para una respuesta. Es posible que también necesite crear la conversación antes de enviar el mensaje. Por ejemplo, un nuevo chat uno a uno o un nuevo hilo de conversación en un canal. No puede crear un nuevo chat de grupo o un nuevo canal en un equipo con mensajería proactiva.

En un nivel alto, los pasos que deberá completar para enviar un mensaje proactivo son:

1. [Obtenga el identificador de usuario o el identificador de equipo o canal](#get-the-user-id-or-teamchannel-id) (si es necesario).
1. [Cree el hilo de conversación o conversación](#create-the-conversation) (si es necesario).
1. [Obtener el id. de conversación.](#get-the-conversation-id)
1. [Envíe el mensaje.](#send-the-message)

Los fragmentos de código de la [sección de](#examples) ejemplos son para crear una conversación uno a uno. Para obtener vínculos a ejemplos de trabajo completos para conversaciones de uno a uno y grupos o canales, vea [ejemplos de código.](#code-samples)

## <a name="get-the-user-id-or-teamchannel-id"></a>Obtener el identificador de usuario o el identificador de equipo o canal

Para crear una conversación o conversación nueva en un canal, necesita el identificador correcto. Puede recibir o recuperar este identificador de varias maneras:

1. Cuando la aplicación esté instalada en cualquier contexto en particular, recibirás una [ `onMembersAdded` actividad.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
1. Cuando se agrega un nuevo usuario a un contexto donde está instalada la aplicación, recibirás una [ `onMembersAdded` actividad.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
1. Puedes recuperar la [lista de canales](~/bots/how-to/get-teams-context.md) de un equipo en el que está instalada la aplicación.
1. Puedes recuperar la [lista de miembros](~/bots/how-to/get-teams-context.md) de un equipo que tiene instalada la aplicación.
1. Cada actividad que reciba el bot debe contener la información necesaria.

Independientemente de cómo obtenga la información, tendrá que almacenar la conversación o `tenantId` `userId` `channelId` crearla. También puede usar la opción para crear un nuevo hilo de conversación en el canal general o `teamId` predeterminado de un equipo.

El identificador de bot y un usuario determinado son únicos, no se `userId` pueden volver a usar entre bots. Sin embargo, el bot es global y debe instalarse en el equipo para poder enviar un mensaje `channelId` proactivo a un canal.

## <a name="create-the-conversation"></a>Crear la conversación

Una vez que tenga la información del usuario o del canal, debe crear la conversación si aún no existe o si no conoce el `conversationId` archivo . Solo debe crear la conversación una vez y asegurarse de almacenar el `conversationId` valor u objeto que se va a usar en el `conversationReference` futuro.

## <a name="get-the-conversation-id"></a>Obtener el identificador de conversación

Después de crear la conversación, use el `conversationReference` objeto o envíe el `conversationId` `tenantId` mensaje. Para obtener este identificador, puede crear la conversación o almacenarla desde cualquier actividad que se le envíe desde ese contexto. Asegúrese de almacenar este identificador.

## <a name="send-the-message"></a>Enviar el mensaje

Ahora que tiene la información de dirección correcta, puede enviar el mensaje. Si usa el SDK, lo hará con el método y con `continueConversation` la llamada a la API `conversationId` `tenantId` directa. Debe establecer la configuración `conversationParameters` correcta para enviar correctamente el mensaje. Vea la [sección de](#examples) ejemplos o use uno de los ejemplos enumerados en la sección de [ejemplos de](#code-samples) código.

## <a name="best-practices-for-proactive-messaging"></a>Procedimientos recomendados para mensajería proactiva

Enviar mensajes proactivos a los usuarios es una forma muy eficaz de comunicarse con los usuarios. Sin embargo, desde su punto de vista, este mensaje puede aparecer completamente desprotegido y, en el caso de los mensajes de bienvenida, es la primera vez que interactúan con la aplicación. Por lo tanto, es muy importante usar esta funcionalidad con moderación, no enviar correo no deseado a los usuarios y proporcionar información suficiente para que los usuarios comprendan por qué se les envía un mensaje.

### <a name="welcome-messages"></a>Mensajes de bienvenida

Al usar la mensajería proactiva para enviar un mensaje de bienvenida a un usuario, debe tener en cuenta que, para la mayoría de las personas que reciben el mensaje, no hay contexto para por qué lo está recibiendo. También es la primera vez que interactúan con la aplicación. Es su oportunidad de crear una buena primera impresión. Los mensajes de bienvenida más importantes deben incluir:

* **Por qué un usuario recibe el mensaje.** Debe ser muy claro para el usuario por qué está recibiendo el mensaje. Si el bot se instaló en un canal y envió un mensaje de bienvenida a todos los usuarios, indálles en qué canal se instaló y quién lo instaló.
* **¿Qué ofrece?** ¿Qué pueden hacer con la aplicación? ¿Qué valor puede aportarles?
* **Qué deben hacer a continuación.** Invítelos a probar un comando o interactuar con la aplicación de alguna manera.

Recuerde que los mensajes de bienvenida deficientes pueden provocar que los usuarios bloqueen el bot. Dedica mucho tiempo a elaborar los mensajes de bienvenida y repite en ellos si no tienen el efecto deseado.

### <a name="notification-messages"></a>Mensajes de notificación

Al usar la mensajería proactiva para enviar notificaciones, debe asegurarse de que los usuarios tienen una ruta clara para realizar acciones comunes basadas en la notificación y una comprensión clara de por qué se produjo la notificación. Por lo general, los mensajes de notificación de buena calidad incluyen:

* **Qué ha pasado.** Una indicación clara de lo que ocurrió para provocar la notificación.
* **Cuál fue el resultado.** Debe estar claro qué elemento o cosa se actualizó para provocar la notificación.
* **Quién/qué lo desencadenó.** Quién o qué acción realizó que se enviara la notificación.
* **Qué pueden hacer los usuarios en respuesta.** Facilita a los usuarios la realización de acciones en función de las notificaciones.
* **Cómo pueden optar por no participar los usuarios.** Debes proporcionar una ruta de acceso para que los usuarios puedan optar por no recibir notificaciones adicionales.

## <a name="proactively-install-your-app-using-graph"></a>Instalar de forma proactiva la aplicación con Graph

> [!Note]
> La instalación proactiva de aplicaciones con Microsoft Graph se encuentra actualmente en versión beta.

En ocasiones, puede que sea necesario enviar mensajes de forma proactiva a los usuarios que no han instalado o interactuado con la aplicación anteriormente. Por ejemplo, desea usar el comunicador de la empresa [para](~/samples/app-templates.md#company-communicator) enviar mensajes a toda la organización. Para este escenario, puede usar la API de Graph para instalar de forma proactiva la aplicación para los usuarios y, a continuación, almacenar en caché los valores necesarios del evento que la aplicación recibe `conversationUpdate` tras la instalación.

Solo puede instalar aplicaciones que se encuentran en el catálogo de aplicaciones de su organización o en la tienda de aplicaciones de Teams.

Consulte [Instalar aplicaciones para usuarios en la](/graph/api/userteamwork-post-installedapps) documentación de Graph e instalación proactiva de bots y mensajes en Teams con Microsoft [Graph.](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md) También hay un ejemplo [de Microsoft .NET Framework](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) en la plataforma GitHub.

## <a name="examples"></a>Ejemplos

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

Debe proporcionar el identificador de usuario y el id. de inquilino. Si la llamada se realiza correctamente, la API devuelve el siguiente objeto de respuesta.

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-samples"></a>Ejemplos de código

Los ejemplos oficiales de mensajería proactiva son los siguientes:

| Nombre de ejemplo           | Descripción                                                                      | .NET    | JavaScript   | Python  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|Conceptos básicos de la conversación de Teams  | Muestra los conceptos básicos de las conversaciones en Teams, incluido el envío de mensajes proactivos de uno a uno.|[.NET &nbsp; Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|Iniciar nuevo subproceso en un canal     | Muestra cómo crear un nuevo subproceso en un canal. |[.NET &nbsp; Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

## <a name="view-additional-code-samples"></a>Ver ejemplos de código adicionales
>
> [!div class="nextstepaction"]
> [**Ejemplos de código de mensajería proactiva de Teams**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>

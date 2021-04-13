---
title: enviar mensajes proactivos
description: describe cómo enviar mensajes proactivos con el bot de Microsoft Teams.
ms.topic: overview
ms.author: anclear
Keywords: enviar un mensaje obtener id. de usuario Id. id. de conversación de conversación
ms.openlocfilehash: 7da470eaba6ae9ecb82c9a7ba04d69b2f196a9d7
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654296"
---
# <a name="send-proactive-messages"></a>Enviar mensajes proactivos

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

Un mensaje proactivo es cualquier mensaje enviado por un bot que no está en respuesta directa a una solicitud de un usuario. Esto puede incluir mensajes como:

* Mensajes de bienvenida
* Notificaciones
* Mensajes programados

Para que el bot envíe un mensaje proactivo, debe tener acceso al usuario, al chat de grupo o al equipo al que desea enviar el mensaje. Para un chat de grupo o un equipo, esto significa que la aplicación que contiene el bot debe instalarse en esa ubicación primero. Puedes instalar [la aplicación de](#proactively-install-your-app-using-graph) forma proactiva con Graph [](/microsoftteams/teams-custom-app-policies-and-settings) en un equipo, si es necesario o usar una directiva de aplicación para enviar aplicaciones a equipos y usuarios de tu inquilino. Para los usuarios, la aplicación debe estar instalada para el usuario o el usuario debe formar parte de un equipo donde esté instalada la aplicación.

Enviar un mensaje proactivo es diferente al envío de un mensaje normal. En ese caso, no hay ningún activo `turnContext` que usar para una respuesta. Es posible que también necesite crear la conversación antes de enviar el mensaje. Por ejemplo, un nuevo chat uno a uno o un nuevo hilo de conversación en un canal. No puede crear un nuevo chat de grupo o un nuevo canal en un equipo con mensajería proactiva.

En un nivel alto, los pasos que deberá completar para enviar un mensaje proactivo son:

1. [Obtener el id. de usuario o el id. de equipo/canal](#get-the-user-id-or-teamchannel-id) (si es necesario).
1. [Cree el hilo de conversación o conversación](#create-the-conversation) (si es necesario).
1. [Obtener el identificador de conversación](#get-the-conversation-id).
1. [Enviar el mensaje](#send-the-message).

Los fragmentos de código de la [sección ejemplos](#examples) son para crear una conversación uno a uno. Para obtener vínculos a ejemplos de trabajo completos para conversaciones de uno a uno y grupos o canales, vea [ejemplos de código](#code-samples).

## <a name="get-the-user-id-or-teamchannel-id"></a>Obtener el id. de usuario o el id. de equipo o canal

Para crear un nuevo hilo de conversación o conversación en un canal, necesita el identificador correcto. Puede recibir o recuperar este identificador de varias maneras:

1. Cuando la aplicación esté instalada en un contexto determinado, recibirás un [ `onMembersAdded` objeto Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
1. Cuando se agrega un nuevo usuario a un contexto donde está instalada la aplicación, recibirás un [ `onMembersAdded` objeto Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
1. Puedes recuperar la lista [de canales](~/bots/how-to/get-teams-context.md) de un equipo en el que está instalada la aplicación.
1. Puedes recuperar la [lista de miembros](~/bots/how-to/get-teams-context.md) de un equipo que tiene instalada la aplicación.
1. Cada actividad que reciba el bot debe contener la información necesaria.

Independientemente de cómo obtenga la información, tendrá que almacenar la conversación o `tenantId` `userId` `channelId` crearla. También puede usar el para crear un nuevo subproceso de conversación en el canal `teamId` general o predeterminado de un equipo.

El `userId` es único para el identificador de bot y un usuario determinado, no puede volver a usarlos entre bots. Sin embargo, el bot es global y debe instalarse en el equipo para poder enviar un mensaje `channelId` proactivo a un canal.

## <a name="create-the-conversation"></a>Crear la conversación

Después de tener la información del usuario o del canal, debe crear la conversación si aún no existe o si no conoce el `conversationId` archivo . Solo debe crear la conversación una vez y asegurarse de almacenar el valor u objeto que se va a `conversationId` `conversationReference` usar en el futuro.

## <a name="get-the-conversation-id"></a>Obtener el identificador de conversación

Después de crear la conversación, use el `conversationReference` objeto o y envíe el `conversationId` `tenantId` mensaje. Puede obtener este identificador creando la conversación o almacenéndola desde cualquier actividad que se le envíe desde ese contexto. Asegúrese de almacenar este identificador.

## <a name="send-the-message"></a>Enviar el mensaje

Ahora que tiene la información de dirección correcta, puede enviar el mensaje. Si usas el SDK, lo harás con el método y con y para realizar `continueConversation` una llamada directa a la `conversationId` `tenantId` API. Debe establecer `conversationParameters` correctamente para enviar correctamente el mensaje. Vea la [sección de](#examples) ejemplos o use uno de los ejemplos enumerados en la sección de [ejemplos de](#code-samples) código.

## <a name="best-practices-for-proactive-messaging"></a>Procedimientos recomendados para mensajería proactiva

Enviar mensajes proactivos a los usuarios es una forma muy eficaz de comunicarse con los usuarios. Sin embargo, desde su punto de vista, este mensaje puede aparecer completamente sin respuesta y, en el caso de los mensajes de bienvenida, es la primera vez que interactúan con la aplicación. Por lo tanto, es muy importante usar esta funcionalidad con moderación, no enviar correo no deseado a los usuarios y proporcionar suficiente información para que los usuarios comprendan por qué se envían mensajes.

### <a name="welcome-messages"></a>Mensajes de bienvenida

Al usar mensajes proactivos para enviar un mensaje de bienvenida a un usuario, debe tener en cuenta que, para la mayoría de las personas que reciben el mensaje, no hay contexto para el motivo de su recepción. También es la primera vez que interactúan con la aplicación. Es su oportunidad de crear una buena primera impresión. Los mejores mensajes de bienvenida deben incluir:

* **Por qué un usuario recibe el mensaje.** Debe ser muy claro para el usuario por qué está recibiendo el mensaje. Si el bot se instaló en un canal y envió un mensaje de bienvenida a todos los usuarios, hágles saber en qué canal se instaló y quién lo instaló.
* **¿Qué ofrece?** ¿Qué pueden hacer con la aplicación? ¿Qué valor puede aportarles?
* **Qué deben hacer a continuación.** Invítelos a probar un comando o interactuar con la aplicación de alguna manera.

Recuerde que los mensajes de bienvenida deficientes pueden provocar que los usuarios bloqueen el bot. Dedica mucho tiempo a crear tus mensajes de bienvenida y recorre en iteración si no tienen el efecto deseado.

### <a name="notification-messages"></a>Mensajes de notificación

Al usar la mensajería proactiva para enviar notificaciones, debe asegurarse de que los usuarios tienen una ruta de acceso clara para realizar acciones comunes en función de la notificación y una comprensión clara de por qué se produjo la notificación. Por lo general, los mensajes de notificación de buena calidad incluyen:

* **Qué ha pasado.** Una indicación clara de lo que ocurrió para causar la notificación.
* **Cuál fue el resultado.** Debe estar claro qué elemento o cosa se actualizó para provocar la notificación.
* **Quién o qué lo desencadenó.** Quién o qué acción hizo que se enviara la notificación.
* **Qué pueden hacer los usuarios en respuesta.** Facilita a los usuarios realizar acciones en función de las notificaciones.
* **Cómo pueden los usuarios optar por no participar.** Debe proporcionar una ruta de acceso para que los usuarios no puedan participar en notificaciones adicionales.

### <a name="scheduled-messages"></a>Mensajes programados

Al usar la mensajería proactiva para enviar mensajes programados a los usuarios, compruebe que la zona horaria se actualiza a su zona horaria. Esto garantiza que los mensajes se entreguen a los usuarios en el momento correspondiente. Por lo general, los mensajes de programación incluyen:

* **Por qué el usuario recibe el mensaje:** Facilita que los usuarios comprendan el motivo por el que están recibiendo el mensaje.
* **Qué puede hacer el usuario a continuación:** los usuarios pueden realizar la acción necesaria en función del contenido del mensaje.

## <a name="proactively-install-your-app-using-graph"></a>Instalar proactivamente la aplicación con Graph

> [!Note]
> Actualmente, la instalación proactiva de aplicaciones con Microsoft Graph está en versión beta.

En ocasiones, es posible que sea necesario enviar mensajes de forma proactiva a los usuarios que no han instalado o interactuado con la aplicación anteriormente. Por ejemplo, desea usar el comunicador de la compañía [para](~/samples/app-templates.md#company-communicator) enviar mensajes a toda la organización. Para este escenario, puedes usar la API de Graph para instalar proactivamente la aplicación para los usuarios y, a continuación, almacenar en caché los valores necesarios del evento que la `conversationUpdate` aplicación recibe al instalarla.

Solo puedes instalar aplicaciones que estén en el catálogo de aplicaciones de la organización o en la tienda de aplicaciones de Teams.

Consulta [Instalar aplicaciones para usuarios en](/graph/api/userteamwork-post-installedapps) la documentación de Graph y La instalación y mensajería proactiva de [bots en Teams con Microsoft Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md). También hay un ejemplo [de Microsoft .NET framework](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) en la plataforma GitHub.

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

Debe proporcionar el identificador de usuario y el identificador de inquilino. Si la llamada se realiza correctamente, la API devuelve el siguiente objeto de respuesta.

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-samples"></a>Ejemplos de código

Los ejemplos de mensajería proactiva oficiales son los siguientes:

| Nombre de ejemplo           | Descripción                                                                      | .NET    | JavaScript   | Python  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|Conceptos básicos de la conversación de Teams  | Muestra los conceptos básicos de las conversaciones en Teams, incluido el envío de mensajes proactivos de uno a uno.|[.NET &nbsp; Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|Iniciar nuevo subproceso en un canal     | Muestra la creación de un nuevo subproceso en un canal. |[.NET &nbsp; Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

## <a name="view-additional-code-samples"></a>Ver ejemplos de código adicionales
>
> [!div class="nextstepaction"]
> [**Ejemplos de código de mensajería proactiva de Teams**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>

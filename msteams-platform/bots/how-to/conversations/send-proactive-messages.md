---
title: Enviar mensajes proactivos
description: Obtenga información sobre cómo enviar mensajes proactivos con el bot de Microsoft Teams, instalar de forma proactiva la aplicación mediante Microsoft Graph y comprobar los ejemplos de código basados en el bot Framework SDK v4.
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: high
Keywords: enviar un mensaje obtener el id. de usuario id. de canal id. de conversación
ms.openlocfilehash: fd3ed48022239aaa84e00c8b3b59701970d9a0af
ms.sourcegitcommit: aa95313cdab4fbf0a9f62a047ebbe6a5f1fbbf5d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2022
ms.locfileid: "65602274"
---
# <a name="proactive-messages"></a>Mensajes proactivos

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

Un mensaje proactivo es cualquier mensaje enviado por un bot que no responde a una solicitud de un usuario. Esto puede incluir mensajes, como:

* Mensajes de bienvenida
* Notificaciones
* Mensajes programados

> [!IMPORTANT]
> Actualmente, los bots están disponibles en Government Community Cloud (GCC) y GCC-High, pero no en el Departamento de defensa (DOD).
>
> Para los mensajes proactivos, los bots deben utilizar los siguientes puntos de conexión para los entornos de la nube de administración pública:
>    * GCC: `https://smba.infra.gcc.teams.microsoft.com/gcc`.
>    * GCCH: `https://smba.infra.gov.teams.microsoft.us/gcch`.

Para que el bot envíe un mensaje proactivo a un usuario, chat grupal o equipo, debe tener acceso para enviar el mensaje. La aplicación que contiene el bot debe instalarse en primer lugar en un chat de grupo o de equipo.
Puede instalar [proactivamente la aplicación con Microsoft Graph](#proactively-install-your-app-using-graph) en un equipo, si es necesario, o usar una [directiva de aplicación](/microsoftteams/teams-custom-app-policies-and-settings) para enviar aplicaciones a equipos y usuarios en su inquilino. Si es usuario, debe tener la aplicación instalada o ser miembro del equipo en el que está instalada la aplicación.

Enviar un mensaje proactivo es diferente a enviar un mensaje normal. No hay ningún activo `turnContext` que usar como respuesta. Debe crear la conversación antes de enviar el mensaje. Por ejemplo, un nuevo chat individual o un nuevo hilo de conversación en un canal. No puede crear un nuevo chat grupal ni un canal nuevo en un equipo con mensajería proactiva.

Para enviar un mensaje proactivo, siga estos pasos:

1. [Obtenga el id. de usuario, id. de equipo o id. de canal,](#get-the-user-id-team-id-or-channel-id)si es necesario.
1. [Cree la conversación](#create-the-conversation), si es necesario.
1. [Obtenga el identificador de conversación](#get-the-conversation-id).
1. [Envíe el mensaje](#send-the-message).

Los fragmentos de código de la sección [ejemplos](#samples) son para crear una conversación individual. Para obtener vínculos a ejemplos completos de trabajo tanto para conversaciones individuales como para grupos o canales, consulte el [ejemplo de código](#code-sample).

Para usar mensajes proactivos de forma eficaz, consulte [procedimientos recomendados para la mensajería proactiva](#best-practices-for-proactive-messaging). Para determinados escenarios, debe [instalar de forma proactiva la aplicación mediante Graph](#proactively-install-your-app-using-graph). Los fragmentos de código de la sección [ejemplos](#samples) son para crear una conversación individual. Para obtener ejemplos de trabajo completos para conversaciones individuales y grupos o canales, consulte [ejemplo de código](#code-sample).

## <a name="get-the-user-id-team-id-or-channel-id"></a>Obtener el id. de usuario, id. de equipo o id. de canal

Para crear una nueva conversación o hilo de conversación en un canal, debe tener el id. correcto. Puede recibir o recuperar este identificador mediante cualquiera de las siguientes opciones:

* Cuando la aplicación está instalada en un contexto determinado, recibe una [`onMembersAdded` actividad](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* Cuando se agrega un nuevo usuario a un contexto donde está instalada la aplicación, recibe una [`onMembersAdded` actividad](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* Puede recuperar la [lista de canales](~/bots/how-to/get-teams-context.md) en un equipo donde está instalada la aplicación.
* Puede recuperar la [lista de miembros](~/bots/how-to/get-teams-context.md) de un equipo donde está instalada la aplicación.
* Cada actividad que recibe el bot debe contener la información necesaria.

Independientemente de cómo obtenga la información, debe almacenar el `tenantId` y el `userId` o `channelId` para crear una nueva conversación. También puede usar el `teamId` para crear un nuevo hilo de conversación en el canal general o predeterminado de un equipo.

El `userId` es único para el identificador del bot y un usuario en particular. No se puede volver a usar el `userId` entre bots. El `channelId` es global. Sin embargo, el bot debe instalarse en el equipo para poder enviar un mensaje proactivo a un canal.

Una vez que tenga la información de usuario o canal, debe crear la conversación.

## <a name="create-the-conversation"></a>Crear la conversación

Debe crear la conversación si no existe o si no conoce el `conversationId`. Solo debe crear la conversación una vez y almacenar el `conversationId` valor u `conversationReference` objeto.

Una vez creada la conversación, debe obtener el identificador de conversación.

## <a name="get-the-conversation-id"></a>Obtener el identificador de conversación

Use el `conversationReference` objeto o `conversationId` y `tenantId` para enviar el mensaje. Puede obtener este identificador creando la conversación o almacenándola desde cualquier actividad que se le envíe desde ese contexto. Almacene este identificador como referencia.

Después de obtener la información de dirección adecuada, puede enviar el mensaje.

## <a name="send-the-message"></a>Enviar el mensaje

Ahora que tiene la información de dirección correcta, puede enviar el mensaje. Si usa el SDK, debe usar el método `continueConversation` y el `conversationId` y `tenantId` para realizar una llamada API directa. Debe establecer el `conversationParameters` correctamente para enviar con éxito el mensaje. Vea la sección de [ejemplos](#samples) o use uno de los ejemplos mostrados en la sección de [ejemplo de código](#code-sample).

Ahora que ha enviado el mensaje proactivo, debe seguir estos procedimientos recomendados al enviar mensajes proactivos para un mejor intercambio de información entre los usuarios y el bot.

## <a name="best-practices-for-proactive-messaging"></a>Procedimientos recomendados para la mensajería proactiva

El envío de mensajes proactivos a los usuarios es una manera eficaz de comunicarse con los usuarios. Sin embargo, desde la perspectiva del usuario, el mensaje aparece sin aprobaciones. Si hay un mensaje de bienvenida, será la primera vez que interactúen con la aplicación. Es importante usar esta funcionalidad y proporcionar la información completa al usuario para comprender el propósito de este mensaje.

### <a name="welcome-messages"></a>Mensajes de bienvenida

Cuando se utiliza la mensajería proactiva para enviar un mensaje de bienvenida a un usuario, no hay contexto para que los usuarios reciban el mensaje. Es también la primera vez que los usuarios interactúan con la aplicación. Es una oportunidad para crear una buena primera impresión. Los mejores mensajes de bienvenida deben incluir:

* Por qué un usuario está recibiendo el mensaje: debe quedar muy claro para el usuario por qué está recibiendo el mensaje. Si su bot se instaló en un canal y envió un mensaje de bienvenida a todos los usuarios, hágales saber en qué canal se instaló y quién lo instaló.
* Qué ofrece: los usuarios deben ser capaces de identificar qué pueden hacer con la aplicación y qué valor puede aportarles.
* Qué deben hacer a continuación: Invitar a los usuarios a probar un comando o interactuar con la aplicación.
Los mensajes de bienvenida deficientes pueden llevar a los usuarios a bloquear el bot. Escriba mensajes de bienvenida claros y concisos. Itere los mensajes de bienvenida si no tienen el efecto deseado.

### <a name="notification-messages"></a>Mensajes de notificación

Para enviar notificaciones mediante mensajería proactiva, asegúrese de que los usuarios tienen una ruta clara para realizar acciones comunes basadas en la notificación. Asegúrese de que los usuarios comprendan claramente por qué han recibido una notificación. Los buenos mensajes de notificación suelen incluir lo siguiente:

* Qué ha ocurrido: una indicación clara de lo que ha ocurrido para recibir la notificación.
* Cuál fue el resultado: debe quedar claro, qué elemento se actualiza para obtener la notificación.
* Quién o qué la activó: quién o qué realizó la acción que provocó el envío de la notificación.
* Qué pueden hacer los usuarios en respuesta: facilite a los usuarios la realización de acciones basadas en sus notificaciones.
* Cómo pueden los usuarios no participar: debe proporcionar una vía para que los usuarios se excluyan de las notificaciones adicionales.

Para enviar mensajes a un gran grupo de usuarios, por ejemplo a su organización, instale proactivamente su aplicación utilizando Graph.

### <a name="scheduled-messages"></a>Mensajes programados

Cuando utilice la mensajería proactiva para enviar mensajes programados a los usuarios, verifique que su zona horaria esté actualizada a su zona horaria. Esto garantiza que los mensajes se entreguen a los usuarios en el momento pertinente. Por lo general, los mensajes de programación incluyen:

* Por qué el usuario recibe el mensaje: facilite a sus usuarios la comprensión de la razón por la que están recibiendo el mensaje.
* Qué puede hacer el usuario a continuación: los usuarios pueden realizar la acción requerida en base al contenido del mensaje.

## <a name="proactively-install-your-app-using-graph"></a>Instale proactivamente su aplicación con Graph

Envíe mensajes proactivos a los usuarios que no hayan instalado o interactuado con su aplicación. Por ejemplo, desea usar el [comunicador de la empresa](~/samples/app-templates.md#company-communicator) para enviar mensajes a toda la organización. En este caso, puede usar la API de Graph para instalar de forma proactiva la aplicación para los usuarios. Almacene en caché los valores necesarios del `conversationUpdate` evento que recibe su aplicación tras la instalación.

Solo puede instalar aplicaciones que se encuentran en el catálogo de aplicaciones de la organización o en la App Store de Teams.

Consulte [instalar aplicaciones para usuarios](/graph/api/userteamwork-post-installedapps) en la documentación de Graph e [instalación proactiva de bots y mensajería en Teams con Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md). También hay un [ejemplo de Microsoft .NET Framework](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) en la plataforma GitHub.

## <a name="samples"></a>Muestras

El código siguiente muestra cómo enviar mensajes proactivos:

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

## <a name="code-sample"></a>Ejemplo de código

En la tabla siguiente se proporciona un ejemplo de código sencillo que incorpora un flujo de conversación básico en una aplicación de Teams y cómo crear un nuevo hilo de conversación en un canal en Teams:

| **Nombre de ejemplo** | **Descripción** | **.NET** | **Node.js** | **Python** |
|---------------|--------------|--------|-------------|--------|
| Conceptos básicos de conversación de Teams  | Muestra los conceptos básicos de las conversaciones de Teams, incluido el envío de mensajes proactivos individuales.| [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot) |
| Iniciar nuevo hilo en un canal | Muestra cómo crear un nuevo hilo en un canal. | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |
| Instalación proactiva de la aplicación y envío de notificaciones proactivas | En este ejemplo se muestra cómo puede usar la instalación proactiva de la aplicación para usuarios y enviar notificaciones proactivas mediante una llamada a las API de Microsoft Graph. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/nodejs) | |

### <a name="additional-code-sample"></a>Ejemplo de código adicional

> [!div class="nextstepaction"]
> [Ejemplos de código de mensajería proactiva de Teams](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)

## <a name="step-by-step-guide"></a>Guía paso a paso

Siga la [guía paso a paso](../../../sbs-send-proactive.yml), que le ayudará a enviar un mensaje proactivo desde un bot.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Formatear los mensajes del bot](~/bots/how-to/format-your-bot-messages.md)

## <a name="see-also"></a>Vea también

* [**Ejemplos de código de mensajería proactiva de Teams**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)
* [Canal y conversaciones de chat de grupo con un bot](~/bots/how-to/conversations/channel-and-group-conversations.md)
* [Responder a la acción de envío del módulo de tareas](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)
* [Enviar notificaciones proactivas a los usuarios](/azure/bot-service/bot-builder-howto-proactive-message)

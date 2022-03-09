---
title: Bots y SDK
author: surbhigupta
description: Información general sobre las herramientas y SDK para crear Microsoft Teams bots.
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 9aef0786d643c80879700ed6c2d4b05ce7c2e09a
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2022
ms.locfileid: "63398662"
---
# <a name="bots-and-sdks"></a>Bots y SDK

Puede crear un bot que funcione en Microsoft Teams con una de las siguientes herramientas o funcionalidades:

* [Microsoft Bot Framework SDK](#bots-with-the-microsoft-bot-framework)
* [Power Virtual Agents](#bots-with-power-virtual-agents)
* [Virtual Assistant](~/samples/virtual-assistant.md)
* [Webhooks y conectores](#bots-with-webhooks-and-connectors)

## <a name="bots-with-the-microsoft-bot-framework"></a>Bots con el Microsoft Bot Framework

El Teams bot consta de lo siguiente:

* Un servicio web accesible públicamente hospedado por usted.
* Registro de Bot Framework para el servicio web.
* El Teams de la aplicación, que conecta el Teams cliente al servicio web.

> [!TIP]
> Use el Portal de desarrolladores para registrar el servicio web con Bot Framework y especificar las configuraciones de la aplicación. Para obtener más información, consulta [Administrar tus aplicaciones con el Portal de desarrolladores para Teams](~/concepts/build-and-test/teams-developer-portal.md).

[Bot Framework es](https://dev.botframework.com/) un SDK enriquecido que se usa para crear bots con C#, Java, Python y JavaScript. Si ya tienes un bot basado en Bot Framework, puedes modificarlo fácilmente para que funcione en Teams. Use C# o Node.js para aprovechar nuestros [SDK](/microsoftteams/platform/#pivot=sdk-tools). Estos paquetes amplían las clases y métodos básicos del SDK de Bot Builder de la siguiente manera:

* Use tipos de tarjeta especializados como la Office 365 de conector.
* Establezca Teams de canal específicos de las actividades.
* Procesar solicitudes de extensión de mensajería.

> [!IMPORTANT]
> Puede desarrollar aplicaciones Teams en cualquier tecnología de programación web y llamar directamente a las [API de REST de Bot Framework](/bot-framework/rest-api/bot-framework-rest-overview). Pero debe realizar el control de tokens en todos los casos.

## <a name="bots-with-power-virtual-agents"></a>Bots con Power Virtual Agents

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) es un servicio de chatbot basado en la plataforma Microsoft Power y Bot Framework. El proceso de desarrollo de Power Virtual Agent usa un enfoque de interfaz gráfica y sin código guiado que permite a los miembros del equipo crear y mantener fácilmente un agente virtual inteligente. Después de crear el chatbot en [el portal de Power Virtual Agents](https://powervirtualagents.microsoft.com), puede [integrarlo fácilmente con Teams](how-to/add-power-virtual-agents-bot-to-teams.md). Para obtener más información sobre cómo empezar, [consulte Power Virtual Agents documentación](/power-virtual-agents).

## <a name="bots-with-webhooks-and-connectors"></a>Bots con webhooks y conectores

Los webhooks y conectores conectan el bot a los servicios web. Con webhooks y conectores, puede crear un bot simple para la interacción básica, como crear un flujo de trabajo u otros comandos simples. Solo están disponibles en el equipo donde los cree y están diseñados para procesos sencillos específicos del flujo de trabajo de su empresa. Para obtener más información, [vea what are webhooks and connectors](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).

## <a name="advantages-of-bots"></a>Ventajas de los bots

Los bots en Microsoft Teams pueden formar parte de una conversación uno a uno, de un chat de grupo o de un canal de un equipo. Cada ámbito proporciona oportunidades y desafíos únicos para el bot de conversación.

| En un canal | En un chat de grupo | En un chat uno a uno |
| :-- | :-- | :-- |
| Alcance masivo | Menos miembros | Forma tradicional |
| Interacciones individuales concisos | @mention bot  | P&bots A |
| @mention bot | Similar al canal | Bots que cuentan chistes y toman notas |

### <a name="in-a-channel"></a>En un canal

Los canales contienen conversaciones en subprocesos entre varias personas incluso hasta dos mil. Esto potencialmente le da al bot un alcance masivo, pero las interacciones individuales deben ser concisos. Las interacciones tradicionales de varios turnos no funcionan. En su lugar, debe buscar usar tarjetas interactivas o módulos de tareas, o mover la conversación a una conversación uno a uno para recopilar mucha información. El bot solo tiene acceso a los mensajes donde está `@mentioned`. Puede recuperar mensajes adicionales de la conversación con permisos de microsoft Graph y de nivel de organización.

Los bots funcionan mejor en un canal en los siguientes casos:

* Notificaciones, donde se proporciona una tarjeta interactiva para que los usuarios puedan tomar información adicional.
* Escenarios de comentarios, como sondeos y encuestas.
* Un solo ciclo de solicitud o respuesta resuelve interacciones y los resultados son útiles para varios miembros de la conversación.
* Bots sociales o divertidos, donde obtienes una imagen de gato increíble, eliges aleatoriamente un ganador, y así sucesivamente.

### <a name="in-a-group-chat"></a>En un chat de grupo

Los chats de grupo son conversaciones entre tres o más personas que no se desarrollan en hilos. Tienden a tener menos miembros que un canal y son más transitorios. De forma similar a un canal, el bot solo tiene acceso a los mensajes donde está `@mentioned` directamente.

En los casos en los que los bots funcionan mejor en un canal también funcionan mejor en un chat en grupo.

### <a name="in-a-one-to-one-chat"></a>En un chat uno a uno

El chat uno a uno es una forma tradicional de que un bot conversacional interactúe con un usuario. Algunos ejemplos de bots de conversación uno a uno son:

* P&bots A
* bots que inician flujos de trabajo en otros sistemas
* bots que cuentan chistes
* bots that take notes Before creating one-to-one chatbots, consider whether a conversation-based interface is the best way to present your functionality.

## <a name="disadvantages-of-bots"></a>Desventajas de los bots

Un amplio diálogo entre el bot y el usuario es una forma lenta y compleja de completar una tarea. Un bot que admite comandos excesivos, especialmente una amplia gama de comandos, no se ve correctamente o los usuarios no ven positivamente.

### <a name="have-multi-turn-experiences-in-chat"></a>Tener experiencias de varios turnos en el chat

Un cuadro de diálogo amplio requiere que el desarrollador mantenga el estado. Para salir de este estado, un usuario debe tener tiempo de espera o seleccionar **Cancelar**. Además, el proceso es tedioso. Por ejemplo, vea el siguiente escenario de conversación:

USUARIO: Programar una reunión con Megan.

BOT: he encontrado 200 resultados, incluya un nombre y apellidos.

USUARIO: Programar una reunión con Megan Bowen.

BOT: ¿A qué hora te gustaría reunirte con Megan Bowen?

USUARIO: 1:00 p.m.

BOT: ¿En qué día?

### <a name="support-too-many-commands"></a>Admitir demasiados comandos

Como solo hay seis comandos visibles en el menú del bot actual, es poco probable que se utilice algo más con cualquier frecuencia. Bots that go deep into a specific area rather than trying to be a broad assistant work and fare better.

### <a name="maintain-a-large-knowledge-base"></a>Mantener una gran base de conocimientos

Una de las desventajas de los bots es que es difícil mantener una gran base de conocimientos de recuperación con respuestas sin crear. Los bots son los más adecuados para interacciones breves y rápidas, y no para el control de listas largas en busca de una respuesta.

## <a name="code-snippets"></a>Fragmentos de código

El código siguiente proporciona un ejemplo de actividad de bot para un ámbito de equipo de canal:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var mention = new Mention
    {
        Mentioned = turnContext.Activity.From,
        Text = $"<at>{XmlConvert.EncodeName(turnContext.Activity.From.Name)}</at>",
    };

    var replyActivity = MessageFactory.Text($"Hello {mention.Text}.");
    replyActivity.Entities = new List<Entity> { mention };

    await turnContext.SendActivityAsync(replyActivity, cancellationToken);
}

```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

this.onMessage(async (turnContext, next) => {
    const mention = {
        mentioned: turnContext.activity.from,
        text: `<at>${ new TextEncoder().encode(turnContext.activity.from.name) }</at>`,
    } as Mention;

    const replyActivity = MessageFactory.text(`Hello ${mention.text}`);
    replyActivity.entities = [mention];

    await turnContext.sendActivity(replyActivity);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});

```

---

El código siguiente proporciona un ejemplo de actividad de bot para un chat uno a uno:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

// Handle message activity
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    turnContext.Activity.RemoveRecipientMention();
    var text = turnContext.Activity.Text.Trim().ToLower();
  await turnContext.SendActivityAsync(MessageFactory.Text($"Your message is {text}."), cancellationToken);
}
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript
this.onMessage(async (context, next) => {
    await context.sendActivity(MessageFactory.text("Your message is:" + context.activity.text));
    await next();
});
```

---

## <a name="code-sample"></a>Ejemplo de código

|Ejemplo de nombre | Descripción | .NETCore | Node.js |
|----------------|-----------------|--------------|----------------|
| Bot de conversación de Teams | Control de eventos de mensajería y conversación. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)|

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Controladores de actividad de bots](~/bots/bot-basics.md)

## <a name="see-also"></a>Vea también

* [Llamadas y reuniones en el bot](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)
* [Conversaciones de bot](~/bots/how-to/conversations/conversation-basics.md)
* [Menús de comandos bot](~/bots/how-to/create-a-bot-commands-menu.md)
* [Flujo de autenticación para bots en Microsoft Teams](~/bots/how-to/authentication/auth-flow-bot.md)
* [Uso de módulos de tareas desde los bots](~/task-modules-and-cards/task-modules/task-modules-bots.md)

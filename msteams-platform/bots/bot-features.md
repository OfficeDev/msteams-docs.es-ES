---
title: Bots y SDK
author: surbhigupta
description: Información general sobre las herramientas y los SDK para crear bots en Microsoft Teams.
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 6e4384bc4594dd3751afca781bd2121ad8aeb210
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2022
ms.locfileid: "65756866"
---
# <a name="bots-and-sdks"></a>Bots y SDK

Puede crear un bot que funcione en Microsoft Teams con una de las siguientes herramientas o funcionalidades:

* [SDK de Microsoft Bot Framework](#bots-with-the-microsoft-bot-framework)
* [Power Virtual Agents](#bots-with-power-virtual-agents)
* [Virtual Assistant](~/samples/virtual-assistant.md)
* [Webhooks y conectores](#bots-with-webhooks-and-connectors)
* [Servicio de bot de Azure](#azure-bot-service)

## <a name="bots-with-the-microsoft-bot-framework"></a>Bots con el Microsoft Bot Framework

El bot de Teams consta de lo siguiente:

* Un servicio web accesible públicamente que la organización hospeda.
* Un registro de Bot Framework para el servicio web.
* El paquete de la aplicación Teams, que conecta el cliente de Teams al servicio web.

> [!TIP]
> Use el Portal para desarrolladores para registrar el servicio web con Bot Framework y especificar las configuraciones de la aplicación. Para obtener más información, consulte [Administración de aplicaciones con el Portal para desarrolladores para Teams](~/concepts/build-and-test/teams-developer-portal.md).

El [Bot Framework](https://dev.botframework.com/) es un SDK enriquecido que se usa para crear bots mediante C#, Java, Python y JavaScript. Si tiene un bot basado en el Bot Framework, puede modificarlo para que funcione en Teams. Microsoft le recomienda usar C# o Node.js para aprovechar nuestros [SDK](/microsoftteams/platform/#pivot=sdk-tools). En estos paquetes, se amplían las clases y métodos básicos del SDK de Bot Builder:

* Use tipos de tarjeta especializados, como la tarjeta del conector Office 365.
* Establezca datos de canal específicos de Teams en las actividades.
* Procesar solicitudes de extensión de mensaje.

> [!IMPORTANT]
> Puede desarrollar aplicaciones Teams en cualquier tecnología de programación web y llamar directamente a las [API REST de Bot Framework](/bot-framework/rest-api/bot-framework-rest-overview). Pero debe realizar el control de tokens en todos los casos.

## <a name="bots-with-power-virtual-agents"></a>Bots con Power Virtual Agents

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) es un servicio de bot de chat basado en la plataforma Microsoft Power y Bot Framework. El proceso de desarrollo de Power Virtual Agent usa un enfoque guiado, sin código e interfaz gráfica que permite a los miembros del equipo crear y mantener fácilmente un agente virtual inteligente. Después de crear el bot de chat en el [portal de Power Virtual Agents](https://powervirtualagents.microsoft.com), puede [integrarlo fácilmente con Teams](how-to/add-power-virtual-agents-bot-to-teams.md). Para obtener más información sobre cómo empezar, consulte [Documentación de Power Virtual Agents](/power-virtual-agents).

>[!NOTE]
>No debe usar Microsoft Power Platform para crear aplicaciones que se van a publicar en la tienda de aplicaciones de Teams. Las aplicaciones de Microsoft Power Platform solo se pueden publicar en la tienda de aplicaciones de una organización.

## <a name="bots-with-webhooks-and-connectors"></a>Bots con webhooks y conectores

Los webhooks y los conectores conectan el bot a los servicios web. Con webhooks y conectores, puede crear un bot para la interacción básica, como la creación de un flujo de trabajo u otros comandos simples. Solo están disponibles en el equipo donde los crea y están diseñados para procesos sencillos específicos del flujo de trabajo de su empresa. Para obtener más información, consulte [qué son los webhooks y los conectores](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).

## <a name="azure-bot-service"></a>Servicio de bot de Azure

El servicio bot de Azure, junto con Bot Framework, proporciona herramientas para compilar, probar, implementar y administrar bots inteligentes, todo en un solo lugar. También puede crear el bot en Azure Bot Service.

> [!IMPORTANT]
> Las aplicaciones de bots en Microsoft Teams están disponibles en GCC-High a través de [Azure Bot Service](/azure/bot-service/channel-connect-teams).

> [!NOTE]
> * Los bots de GCCH solo admiten hasta la versión de manifiesto v1.10.
> * Las direcciones URL de imagen de las tarjetas adaptables no se admiten en el entorno de GCCH. Puede reemplazar una dirección URL de imagen con DataUri codificado en Base64.
> * El registro de canales de bot en Azure Government aprovisionará bot de aplicación web, app service (plan de App Service) y Application Insights también, pero no admite el aprovisionamiento del servicio bot de Azure solo (sin app service).
>   <details>
>   <summary><b>Si solo desea realizar el registro de bots</b></summary>
>
>   * Vaya al grupo de recursos y elimine manualmente los recursos sin usar. Como app service, el plan de App Service (si creó durante el registro del bot) y application Insights (si decide habilitarlo durante el registro del bot).
>   * También puede usar az-cli para realizar el registro de bots:
>
>     1. Inicie sesión en Azure y establezca la suscripción. <br> 
>           &nbsp; az cloud set –name "AzureUSGovernment" <br> 
>           &nbsp; az account set –name "`subscriptionname/id`".<br>
>     1. Creación del registro de aplicaciones  
>           &nbsp; az ad app create --display-name "`name`" <br> 
>           &nbsp; --password "`password`" --available-to-other-tenants.<br> 
>           El identificador de la aplicación se crearía aquí.<br>
>     1. Creación de un recurso de bot <br>
>           &nbsp; az bot create –resource-group "`resource-group`"<br>
>           &nbsp; --appid "`appid`"<br>
>           &nbsp; --name "`botid`"<br>
>           &nbsp; --kind "registration".<br>
>
> </details>

Para el entorno GCCH, debe registrar un bot mediante [Azure Government portal](https://portal.azure.us).

:::image type="content" source="../assets/videos/abs-bot.gif" alt-text="portal de Azure Government":::
<br>
<br>
Los siguientes cambios son necesarios en el bot para GCC-High entorno:
<br>
<br>
<details>
<summary><b>Cambios de configuración</b></summary>

A medida que el registro del bot se produce en Azure Government portal, asegúrese de actualizar las configuraciones del bot para conectarse a instancias de Azure govermnet. A continuación se muestran los detalles de configuración:

| Nombre de configuración | Valor |
|----|----|
| ChannelService | `https://botframework.azure.us` |
| OAuthUrl | `https://tokengcch.botframework.azure.us` |
| ToChannelFromBotLoginUrl | `https://login.microsoftonline.us/MicrosoftServices.onmicrosoft.us` |
| ToChannelFromBotOAuthScope | `https://api.botframework.us` |
| ToBotFromChannelTokenIssuer | `https://api.botframework.us`  |
| BotOpenIdMetadata | `https://login.botframework.azure.us/v1/.well-known/openidconfiguration` |

</details>
<br>
<details>
<summary><b>Actualización a appsettings.json & startup.cs</b></summary>

1. **Actualice appsettings.json:**

    * Establezca `ConnectionName` en el nombre de la configuración de conexión de OAuth que agregó al bot.

    * Establezca `MicrosoftAppId` y `MicrosoftAppPassword` en el identificador de aplicación y el secreto de aplicación del bot.
    
    En función de los caracteres del secreto del bot, es posible que deba aplicar un escape XML a la contraseña. Por ejemplo, las y comercial (&) deben codificarse como `&amp;`.

    ```json
    {
      "MicrosoftAppType": "",
      "MicrosoftAppId": "",
      "MicrosoftAppPassword": "",
      "MicrosoftAppTenantId": "",
      "ConnectionName": ""
    }
    ```
2. **Actualizar Startup.cs:**

    Para usar OAuth en *nubes de Azure no públicas*, como la nube gubernamental o en bots con residencia de datos, debe agregar el código siguiente en el archivo **Startup.cs** .
    
    ```csharp
    string uri = "<uri-to-use>";
    MicrosoftAppCredentials.TrustServiceUrl(uri);
    OAuthClientConfig.OAuthEndpoint = uri;
    ```
    
    Donde \<uri-to-use\> es uno de los siguientes URI:

    |**URI**|**Descripción**|
    |---|---|
    |`https://europe.api.botframework.com`|Para bots de nube pública con residencia de datos en Europa.|
    |`https://unitedstates.api.botframework.com`|Para bots en la nube pública con residencia de datos en el Estados Unidos.|
    |`https://apiGCCH.botframework.azure.us`|Para Estados Unidos bots en la nube gubernamental sin residencia de datos.|
    |`https://api.botframework.com`|Para bots de nube pública sin residencia de datos. Este es el URI predeterminado y no requiere un cambio en **Startup.cs**.|

3. La dirección URL de redireccionamiento para el registro de aplicaciones de Azure debe actualizarse a `https://tokengcch.botframework.azure.us/.auth/web/redirect`.

</details>

## <a name="advantages-of-bots"></a>Ventajas de los bots

Los bots en Microsoft Teams pueden formar parte de una conversación uno a uno, de un chat de grupo o de un canal de un equipo. Cada ámbito proporciona oportunidades y dificultades únicas para su bot de conversación.

| En un canal | En un chat de grupo | En un chat individual |
| :-- | :-- | :-- |
| Alcance masivo | Menos miembros | Manera tradicional |
| Interacciones individuales concisas | @mention al bot  | Bots de Q&A |
| @mention al bot | Similar al canal | Bots que cuentan chistes y toman notas |

### <a name="in-a-channel"></a>En un canal

Los canales contienen conversaciones encadenadas entre varias personas, incluso hasta dos mil. Esto proporciona un alcance potencialmente masivo al bot, pero las interacciones individuales deben ser concretas. Las interacciones tradicionales de varios turnos no funcionan. En su lugar, intente usar tarjetas interactivas o módulos de tareas, o mover la conversación a una conversación individual si necesita recopilar una gran cantidad de información. El bot solo tiene acceso a los mensajes en los que es `@mentioned`. Puede recuperar mensajes adicionales de la conversación con Microsoft Graph y los permisos a nivel de organización.

Los bots funcionan mejor en un canal en los siguientes casos:

* Notificaciones, especialmente si se proporciona una tarjeta interactiva para que los usuarios puedan obtener información adicional.
* Escenarios de comentarios, como sondeos y encuestas.
* El ciclo de solicitud o respuesta única resuelve las interacciones y los resultados son útiles para varios miembros de la conversación.
* Bots sociales o divertidos, donde hay imágenes de gatos geniales, se elige aleatoriamente un ganador, etc.

### <a name="in-a-group-chat"></a>En un chat de grupo

Los chats de grupo son conversaciones entre tres o más personas que no se desarrollan en hilos. Tienden a tener menos miembros que un canal y son más transitorios. De forma similar a un canal, el bot solo tiene acceso a los mensajes donde está `@mentioned` directamente.

En los casos en los que los bots funcionan mejor en un canal también funcionan mejor en un chat de grupo.

### <a name="in-a-one-to-one-chat"></a>En un chat individual

Esta es la manera tradicional en la que un bot de conversación interactúa con un usuario. Algunos ejemplos de bots conversacionales individuales son:

* Bots de Q&A
* Bots que inician flujos de trabajo en otros sistemas
* Bots que cuentan chistes
* Bots que toman notas. Antes de crear bots de chat individuales, piense si una interfaz basada en conversaciones es la mejor manera de presentar la funcionalidad.

## <a name="disadvantages-of-bots"></a>Desventajas de los bots

Un amplio diálogo entre el bot y el usuario es una manera lenta y compleja de completar una tarea. Un bot que admite comandos excesivos, especialmente una amplia gama de comandos, no es correcto o los usuarios no los ven de forma positiva.

### <a name="have-multi-turn-experiences-in-chat"></a>Tener experiencias de varios turnos en el chat

Un cuadro de diálogo extenso requiere que el desarrollador mantenga el estado. Para salir de este estado, un usuario debe agotar el tiempo de espera o seleccionar **Cancelar**. Además, el proceso es tedioso. Por ejemplo, consulte el siguiente escenario de conversación:

USUARIO: Programe una reunión con Megan.

BOT: He encontrado 200 resultados, incluya el nombre y el apellido.

USUARIO: Programe una reunión con Megan Bowen.

BOT: Ok, ¿a qué hora le gustaría reunirse con Megan Bowen?

USUARIO: 1:00 p.m.

BOT: ¿En qué día?

### <a name="support-too-many-commands"></a>Compatibilidad con demasiados comandos

Dado que solo hay seis comandos visibles en el menú del bot actual, es poco probable que se use ningún otro con frecuencia. Bots que profundizan en un área específica en lugar de tratar de ser un asistente de trabajo amplio y funcionan mejor.

### <a name="maintain-a-large-knowledge-base"></a>Mantener una amplia knowledge base

Una de las desventajas de los bots es que es difícil mantener una gran knowledge base de recuperación con respuestas no clasificadas. Los bots son más adecuados para interacciones breves y rápidas y no para examinar listas largas en busca de una respuesta.

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

El código siguiente proporciona un ejemplo de actividad de bot para un chat individual:

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

|Ejemplo de nombre | Descripción | .NETCore | Node.js | Python|
|----------------|-----------------|--------------|----------------|-------|
| Bot de conversación de Teams | Control de eventos de mensajería y conversación. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot)|
| Ejemplos de bot | Conjunto de ejemplos de bots | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore) |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python)|

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Controladores de actividad de bots](~/bots/bot-basics.md)

## <a name="see-also"></a>Consulte también

* [Bots de llamadas y reuniones](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)
* [Conversaciones de bot](~/bots/how-to/conversations/conversation-basics.md)
* [Menús de comandos del bot](~/bots/how-to/create-a-bot-commands-menu.md)
* [Flujo de autenticación para bots en Microsoft Teams](~/bots/how-to/authentication/auth-flow-bot.md)
* [Uso de módulos de tareas desde los bots](~/task-modules-and-cards/task-modules/task-modules-bots.md)

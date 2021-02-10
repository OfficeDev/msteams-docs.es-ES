---
title: Usar Microsoft Graph para habilitar la instalación proactiva de bots y la mensajería en Teams
description: Describe la mensajería proactiva en Teams y cómo implementarla.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams proactive messaging chat installation Graph
ms.openlocfilehash: 4f26b4d2f4e82fcf50b7a35c46bcd07e5afecf19
ms.sourcegitcommit: b99ed616db734371e4af4594b7e895c5b05737c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2021
ms.locfileid: "50162897"
---
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a>Habilitar la instalación proactiva de bots y la mensajería proactiva en Teams con Microsoft Graph (versión preliminar pública)

>[!IMPORTANT]
> Las vistas previas públicas de Microsoft Graph y Microsoft Teams están disponibles para el acceso anticipado y los comentarios. Aunque esta versión se ha sometido a pruebas exhaustivas, no está pensada para su uso en producción.

## <a name="proactive-messaging-in-teams"></a>Mensajería proactiva en Teams

Los bots inician mensajes proactivos para iniciar conversaciones con un usuario. Sirven para muchos propósitos, como enviar mensajes de bienvenida, realizar encuestas o sondeos y difundir notificaciones en toda la organización.  Los mensajes proactivos en Teams se pueden entregar como **conversaciones ad hoc** o **basadas en cuadros de** diálogo:

|Tipo de mensaje | Descripción |
|----------------|-------------- |
|Mensaje proactivo ad hoc| El bot intercala un mensaje sin interrumpir el flujo de conversación.|
|Mensaje proactivo basado en cuadros de diálogo | El bot crea un nuevo subproceso de diálogo, toma el control de una conversación, entrega el mensaje proactivo, se cierra y devuelve el control al cuadro de diálogo anterior.|

*Vea*, [Enviar notificaciones proactivas a los usuarios SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

## <a name="proactive-app-installation-in-teams"></a>Instalación proactiva de aplicaciones en Teams

Para que el bot pueda enviar mensajes de forma proactiva a un usuario, debe instalarse como una aplicación personal o en un equipo en el que el usuario sea miembro. En ocasiones, es posible que deba enviar mensajes de forma proactiva a los usuarios que no han instalado o interactuado previamente con la aplicación.  Por ejemplo, la necesidad de enviar información vital a todos los usuarios de la organización. Para estos escenarios, puede usar la API de Microsoft Graph para instalar de forma proactiva el bot para los usuarios.

## <a name="permissions"></a>Permisos

Los permisos de tipo de recurso [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) de Microsoft Graph le permiten administrar el ciclo de vida de instalación de la aplicación para todos los ámbitos de usuario (personal) o equipo (canal) dentro de la plataforma de Microsoft Teams:

|Permisos de aplicación | Descripción|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Permite que una aplicación de Teams se lea, instale, actualice y desinstale para cualquier **usuario,** sin necesidad de iniciar sesión o usarse previamente.|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Permite que una aplicación de Teams se lea, instale, actualice y desinstale en cualquier **equipo,** sin necesidad de iniciar sesión o usarse previamente.|

Para usar estos permisos, debe agregar una clave [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) al manifiesto de la aplicación con los siguientes valores:
> [!div class="checklist"]
> [!div class="checklist"]
>
> * **id.:**  id. de aplicación de Azure AD.
> * **recurso:** la dirección URL del recurso para la aplicación.
>

>[!NOTE]
>
> * El bot requiere _permisos de_ aplicación _no delegados_ por el usuario porque la instalación no es para usted, sino para otros usuarios.
>
> * Un administrador de inquilinos de Azure AD debe [conceder permisos explícitamente a una aplicación.](/graph/security-authorization#grant-permissions-to-an-application) Después de conceder permisos a una aplicación, _todos los_ miembros del inquilino de Azure AD obtendrán los permisos concedidos.

## <a name="enable-proactive-app-installation-and-messaging"></a>Habilitar la mensajería y la instalación de aplicaciones proactivas

 > [!IMPORTANT]
>Microsoft Graph solo instalará las aplicaciones publicadas en el catálogo de aplicaciones de su organización [o](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) [en AppSource.](https://appsource.microsoft.com/)

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a>✔ crear y publicar el bot de mensajería proactiva para Teams

To get started, you will need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with proactive [messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities and  [published](../../concepts/deploy-and-publish/overview.md) in your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).

>[!TIP]
> La plantilla de aplicación de empresa [**Communicator**](../..//samples/app-templates.md#company-communicator) lista para producción habilita la mensajería de difusión y es una buena base para crear la aplicación bot proactiva.

### <a name="-get-the-teamsappid-for-your-app"></a>✔ obtener la `teamsAppId` aplicación

**1.** Necesitará los pasos `teamsAppId`  siguientes.

Se puede recuperar del catálogo de aplicaciones `teamsAppId` de su organización:

**Referencia de página de Microsoft Graph: tipo** [de recurso teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

**Solicitud HTTP GET:**

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

La solicitud devolverá un `teamsApp`  objeto. El objeto devuelto es el identificador de aplicación generado por el catálogo de la aplicación y es diferente del "id:" que proporcionó en el manifiesto de `id`  la aplicación de Teams:

```json
{
  "value": [
    {
      "id": "b1c5353a-7aca-41b3-830f-27d5218fe0e5",
      "externalId": "f31b1263-ba99-435a-a679-911d24850d7c",
      "name": "Test App",
      "version": "1.0.1",
      "distributionMethod": "Organization"
    }
  ]
}
```

**2.**  Si la aplicación ya se ha cargado o cargado localmente para un usuario en el ámbito personal, puede recuperar lo `teamsAppId` siguiente:

**Referencia de página de Microsoft Graph: Enumerar** [las aplicaciones instaladas para el usuario](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Solicitud HTTP GET:**

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

**3.** Si la aplicación ya se ha cargado o cargado localmente para un canal en el ámbito de equipo, puede recuperar lo `teamsAppId` siguiente:

**Referencia de página de Microsoft Graph: Enumerar** [aplicaciones en equipo](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Solicitud HTTP GET:**

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> Puede filtrar por cualquiera de los campos del objeto [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) para restringir la lista de resultados.

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>✔ determinar si el bot está instalado actualmente para un destinatario de mensaje

**Referencia de página de Microsoft Graph: Enumerar** [las aplicaciones instaladas para el usuario](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Solicitud HTTP GET:**

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

Esta solicitud devolverá una matriz vacía si la aplicación no está instalada o una matriz con un único objeto [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) si se ha instalado.

### <a name="-install-your-app"></a>✔ instalar la aplicación

**Referencia de página de Microsoft Graph:** [Instalar la aplicación para el usuario](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Solicitud HTTP POST:**

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

Si el usuario tiene Microsoft Teams en ejecución, es posible que vea que la aplicación se instala inmediatamente. Como alternativa, puede que sea necesario reiniciar para ver la aplicación instalada.

### <a name="-retrieve-the-conversation-chatid"></a>✔ recuperar el **chatId de conversación**

Cuando la aplicación esté instalada para el usuario, el bot recibirá una notificación de evento que contendrá la información necesaria para `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) enviar el mensaje proactivo.

También `chatId` se puede recuperar de la siguiente manera:

**Referencia de página de Microsoft Graph:** [Obtener chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)

**1.** Necesitará el archivo `{teamsAppInstallationId}` . Si no lo tiene, use lo siguiente:

**Solicitud HTTP GET:**

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

La **propiedad id** de la respuesta es `teamsAppInstallationId` .

**2.** Realice la siguiente solicitud para `chatId` capturar:

**Solicitud HTTP GET** `TeamsAppInstallation.ReadWriteSelfForUser.All` (permiso):  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

La **propiedad id** de la respuesta es `chatId` .

Como alternativa, puede recuperar la solicitud siguiente, pero `chatId`  requerirá el permiso más `Chat.Read.All` amplio:

**Solicitud HTTP GET** `Chat.Read.All` (permiso):

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a>✔ enviar mensajes proactivos

Una vez que el bot se ha agregado para un usuario o equipo y ha adquirido la información de usuario necesaria, puede empezar a [enviar mensajes proactivos.](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

# <a name="c--net"></a>[C# / .NET](#tab/csharp)

El siguiente fragmento de código es de los ejemplos [de Microsoft Bot Framework para C#.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)

```csharp
using System.Collections.Concurrent;
using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Bot.Builder;
using Microsoft.Bot.Schema;

namespace Microsoft.BotBuilderSamples
{
    public class ProactiveBot : ActivityHandler
    {
        // Message to send to users when the bot receives a Conversation Update event
        private const string WelcomeMessage = "Welcome to the Proactive Bot sample.  Navigate to http://localhost:3978/api/notify to proactively message everyone who has previously messaged this bot.";

        // Dependency injected dictionary for storing ConversationReference objects used in NotifyController to proactively message users
        private readonly ConcurrentDictionary<string, ConversationReference> _conversationReferences;

        public ProactiveBot(ConcurrentDictionary<string, ConversationReference> conversationReferences)
        {
            _conversationReferences = conversationReferences;
        }

        private void AddConversationReference(Activity activity)
        {
            var conversationReference = activity.GetConversationReference();
            _conversationReferences.AddOrUpdate(conversationReference.User.Id, conversationReference, (key, newValue) => conversationReference);
        }

        protected override Task OnConversationUpdateActivityAsync(ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            AddConversationReference(turnContext.Activity as Activity);

            return base.OnConversationUpdateActivityAsync(turnContext, cancellationToken);
        }

        protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            foreach (var member in membersAdded)
            {
                // Greet anyone that was not the target (recipient) of this message.
                if (member.Id != turnContext.Activity.Recipient.Id)
                {
                    await turnContext.SendActivityAsync(MessageFactory.Text(WelcomeMessage), cancellationToken);
                }
            }
        }

        protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
        {
            AddConversationReference(turnContext.Activity as Activity);

            // Echo back what the user said
            await turnContext.SendActivityAsync(MessageFactory.Text($"You sent '{turnContext.Activity.Text}'"), cancellationToken);
        }
    }
}
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

El siguiente fragmento de código es de los ejemplos [de Microsoft Bot Framework para JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages).

```javascript
const { ActivityHandler, TurnContext } = require('botbuilder');

class ProactiveBot extends ActivityHandler {
    constructor(conversationReferences) {
        super();

        // Dependency injected dictionary for storing ConversationReference objects used in NotifyController to proactively message users
        this.conversationReferences = conversationReferences;

        this.onConversationUpdate(async (context, next) => {
            this.addConversationReference(context.activity);

            await next();
        });

        this.onMembersAdded(async (context, next) => {
            const membersAdded = context.activity.membersAdded;
            for (let cnt = 0; cnt < membersAdded.length; cnt++) {
                if (membersAdded[cnt].id !== context.activity.recipient.id) {
                    const welcomeMessage = 'Welcome to the Proactive Bot sample.  Navigate to http://localhost:3978/api/notify to proactively message everyone who has previously messaged this bot.';
                    await context.sendActivity(welcomeMessage);
                }
            }

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });

        this.onMessage(async (context, next) => {
            this.addConversationReference(context.activity);

            // Echo back what the user said
            await context.sendActivity(`You sent '${ context.activity.text }'`);
            await next();
        });
    }

    addConversationReference(activity) {
        const conversationReference = TurnContext.getConversationReference(activity);
        this.conversationReferences[conversationReference.conversation.id] = conversationReference;
    }
}

module.exports.ProactiveBot = ProactiveBot;

```
---

## <a name="related-topic-for-teams-administrators"></a>Tema relacionado para los administradores de Teams
>
> [!div class="nextstepaction"]
> [**Administrar directivas de configuración de aplicación en Microsoft Teams**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a>Ver ejemplos de código adicionales
>
> [!div class="nextstepaction"]
> [**Ejemplos de código de mensajería proactiva de Teams**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>

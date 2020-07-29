---
title: Usar Microsoft Graph para habilitar la instalación y mensajería proactiva de robots en Microsoft Teams
description: Describe la mensajería proactiva en Microsoft Teams y cómo implementarla.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Gráfico de instalación de chat de mensajería proactiva de Teams
ms.openlocfilehash: 735dbfa39222f312b4f3714b5c009dfd1bf28b05
ms.sourcegitcommit: 1b909fb9ccf6cdd84ed0d8f9ea0463243a802a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "45434499"
---
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a>Habilitar la instalación proactiva de Bot y la mensajería proactiva en Teams con Microsoft Graph (vista previa pública)

>[!IMPORTANT]
> Hay disponibles vistas previas públicas de Microsoft Graph para los comentarios y el acceso anticipado. Aunque esta versión se ha sometido a pruebas exhaustivas, no está pensada para su uso en producción.

## <a name="proactive-messaging-in-teams"></a>Mensajería proactiva en Microsoft Teams

Los bots inician los mensajes proactivos para iniciar conversaciones con los usuarios. Tienen varios fines, entre los que se incluyen el envío de mensajes de bienvenida, la realización de encuestas o sondeos, y la difusión de notificaciones de toda la organización.  Los mensajes proactivos en Microsoft Teams se pueden entregar como conversaciones **ad-hoc** o **basadas en cuadros de diálogo** :

|Tipo de mensaje | Descripción |
|----------------|-------------- |
|Mensaje proactivo ad-hoc| El bot interjects un mensaje sin interrumpir el flujo de conversación.|
|Mensaje proactivo basado en cuadros de diálogo | El bot crea un nuevo subproceso de diálogo, toma el control de una conversación, entrega el mensaje proactivo, se cierra y devuelve el control al cuadro de diálogo anterior.|

*Ver*, [enviar notificaciones proactivas a los usuarios SDK V4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)

## <a name="proactive-app-installation-in-teams"></a>Instalación proactiva de aplicaciones en Microsoft Teams

Antes de que el Bot pueda enviar mensajes a un usuario de forma proactiva, debe instalarse como una aplicación personal o en un equipo en el que el usuario sea miembro. En ocasiones, es posible que deba realizar mensajes de forma proactiva para los usuarios que _no_ hayan instalado o que se hayan interactuado anteriormente con la aplicación. Por ejemplo, la necesidad de mensajes vitales para todos los usuarios de la organización. Para estos escenarios, puede usar la API de Microsoft Graph para instalar de forma proactiva su bot para los usuarios.

## <a name="permissions"></a>Permisos

Los permisos de [tipo de recurso teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0) de Microsoft Graph permiten administrar el ciclo de vida de la instalación de la aplicación para todos los ámbitos de usuario (personal) o de equipo (canal) dentro de la plataforma de Microsoft Teams:

|Permisos de aplicación | Descripción|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Permite a una aplicación de Teams leer, instalar, actualizar y desinstalar para cualquier **usuario**, sin necesidad de iniciar sesión ni usar previamente.|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Permite a una aplicación de Teams leer, instalar, actualizar y desinstalar en cualquier **equipo**, sin necesidad de iniciar sesión ni usar previamente.|

Para usar estos permisos, debe agregar una clave [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) al manifiesto de la aplicación con los siguientes valores:
> [!div class="checklist"]
> [!div class="checklist"]
>
> * **ID** : el identificador de la aplicación de Azure ad.
> * **recurso** : la dirección URL del recurso de la aplicación.
>

>[!NOTE]
>
> * El bot requiere que la _aplicación_ no tenga permisos _delegados_ porque la instalación no es para sí mismo sino para otros.
>
> * Un administrador de inquilinos de Azure AD debe [conceder explícitamente permisos a una aplicación](/graph/security-authorization#grant-permissions-to-an-application). Después de que se concedan permisos a una aplicación, _todos_ los miembros del inquilino de Azure ad obtendrán los permisos concedidos.

## <a name="enable-proactive-app-installation-and-messaging"></a>Habilitar la instalación y mensajería proactivas de aplicaciones

 > [!IMPORTANT]
>Microsoft Graph solo instalará aplicaciones publicadas en el [Catálogo de aplicaciones](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) de la organización o en [AppSource](https://appsource.microsoft.com/).

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a>✔ Crear y publicar su bot de mensajería proactiva para Microsoft Teams

Para empezar, necesitará un [bot para Teams](../../bots/how-to/create-a-bot-for-teams.md) con capacidades de [Mensajería proactiva](../../concepts/bots/bot-conversations/bots-conv-proactive.md) y [publicada](../../concepts/deploy-and-publish/overview.md) en el catálogo de [aplicaciones](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) de su organización o en [AppSource](https://appsource.microsoft.com/).

>[!TIP]
> La plantilla de aplicación de [**Communicator**](../..//samples/app-templates.md#company-communicator) de producción preparada permite la mensajería de difusión y es una buena base para crear una aplicación de bot proactiva.

### <a name="-get-the-teamsappid-for-your-app"></a>✔ Obtener el `teamsAppId` para la aplicación

**1.** necesitará el `teamsAppId` para los pasos siguientes.

El `teamsAppId` puede recuperarse del catálogo de aplicaciones de su organización:

**Referencia de página de Microsoft Graph:** [tipo de recurso teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0)

Solicitud **http Get** :

```http
GET https://graph.microsoft.com/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

La solicitud devolverá un `teamsApp` objeto. El objeto devuelto `id` es el identificador de aplicación generado por el catálogo de la aplicación y es diferente del "ID:" que ha proporcionado en el manifiesto de la aplicación Teams:

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

**2.** si la aplicación ya se ha cargado o realizado localmente para un usuario en el ámbito personal, puede recuperar el como se `teamsAppId` indica a continuación:

**Referencia de página de Microsoft Graph:** [lista de aplicaciones instaladas para el usuario](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)

Solicitud **http Get** :

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

**3.** si la aplicación ya se ha cargado o transferido localmente para un canal en el ámbito de equipo, puede recuperar el `teamsAppId` como se indica a continuación:

**Referencia de página de Microsoft Graph:** [enumerar aplicaciones en el equipo](/graph/api/teamsappinstallation-list?view=graph-rest-beta&tabs=http)

Solicitud **http Get** :

```http
GET https://graph.microsoft.com/beta/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{manifestId}'
```

>[!TIP]
> Puede filtrar por cualquiera de los campos del objeto [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0) para restringir la lista de resultados.

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>✔ Determinar si su bot está instalado actualmente para un destinatario de mensaje

**Referencia de página de Microsoft Graph:** [lista de aplicaciones instaladas para el usuario](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)

Solicitud **http Get** :

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

Esta solicitud devolverá una matriz vacía si la aplicación no está instalada, o una matriz con un solo objeto [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-beta) si se ha instalado.

### <a name="-install-your-app"></a>✔ Instalar la aplicación

**Referencia de Microsoft Graph:** [instalar la aplicación para el usuario](/graph/api/user-add-teamsappinstallation?view=graph-rest-beta&tabs=http)

Solicitud **http post** :

```http
POST https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/beta/appCatalogs/teamsApps/{teamsAppId}"
}
```

Si el usuario tiene Microsoft Teams ejecutándose, puede que vea la aplicación inmediatamente. Como alternativa, puede que sea necesario reiniciar para ver la aplicación instalada.

### <a name="-retrieve-the-conversation-chatid"></a>✔ Recuperar el **chatId** de conversación

Cuando la aplicación está instalada para el usuario, el bot recibirá una `conversationUpdate` [notificación de evento](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) que contendrá la información necesaria para enviar el mensaje proactivo.

El `chatId` también se puede recuperar de la siguiente manera:

**Referencia de Microsoft Graph:** [obtener chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http)

**1.** necesitará la aplicación `{teamsAppInstallationId}` si no la tiene, use lo siguiente:

Solicitud **http Get** :

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

La propiedad **ID** de la respuesta es `teamsAppInstallationId` .

**2.** realice la siguiente solicitud para obtener `chatId` :

Solicitud **get de http** (permiso `TeamsAppInstallation.ReadWriteSelfForUser.All` ):  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

La propiedad **ID** de la respuesta es `chatId` .

Como alternativa, puede recuperar el `chatId` con la solicitud a continuación, pero necesitará el permiso más amplio `Chat.Read.All` :

Solicitud **get de http** (permiso `Chat.Read.All` ):

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a>✔ Enviar mensajes proactivos

Una vez que se ha agregado el bot a un usuario o equipo y se ha adquirido la información de usuario necesaria, puede empezar a [enviar mensajes proactivos](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp).

# <a name="c--net"></a>[C#/.NET](#tab/csharp)

El siguiente fragmento de código es de los [ejemplos de Microsoft bot Framework para C#.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)

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

El siguiente fragmento de código es de los [ejemplos de Microsoft bot Framework para JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages).

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

## <a name="related-topic-for-teams-administrators"></a>Tema relacionado para administradores de Microsoft Teams
>
> [!div class="nextstepaction"]
> [**Administrar directivas de configuración de aplicaciones en Microsoft Teams**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a>Ver ejemplos de código adicionales
>
> [!div class="nextstepaction"]
> [**Ejemplos de código de mensajería proactiva de Microsoft Teams**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
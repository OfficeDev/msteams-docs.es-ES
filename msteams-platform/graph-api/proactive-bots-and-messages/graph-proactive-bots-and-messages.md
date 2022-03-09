---
title: Use Microsoft Graph para autorizar la instalación proactiva de bots y la mensajería en Teams
description: Describe la mensajería proactiva en Teams y cómo implementarla. Obtenga información sobre cómo habilitar la instalación proactiva de aplicaciones y la mensajería mediante el ejemplo de código.
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: instalación proactiva de chat de mensajería de teams Graph
ms.openlocfilehash: 11fb1188cc88c983b1ee958b1df264346af22693
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2022
ms.locfileid: "63398711"
---
# <a name="proactive-installation-of-apps-using-graph-api-to-send-messages"></a>Instalación proactiva de aplicaciones con Graph API para enviar mensajes

## <a name="proactive-messaging-in-teams"></a>Mensajería proactiva en Teams

Los bots inician mensajes proactivos para iniciar conversaciones con un usuario. Sirven para muchos propósitos, como enviar mensajes de bienvenida, realizar encuestas o sondeos y difundir notificaciones en toda la organización. Los mensajes proactivos Teams pueden entregarse como conversaciones **ad-hoc** o **basadas en cuadros de** diálogo:

|Tipo de mensaje | Descripción |
|----------------|-------------- |
|Mensaje proactivo ad hoc| El bot interje un mensaje sin interrumpir el flujo de conversación.|
|Mensaje proactivo basado en cuadros de diálogo | El bot crea un nuevo subproceso de diálogo, toma el control de una conversación, entrega el mensaje proactivo, se cierra y devuelve el control al cuadro de diálogo anterior.|

## <a name="proactive-app-installation-in-teams"></a>Instalación proactiva de aplicaciones en Teams

Para que el bot pueda enviar un mensaje de forma proactiva a un usuario, debe instalarse como una aplicación personal o en un equipo en el que el usuario sea miembro. En ocasiones, debes enviar mensajes de forma proactiva a los usuarios que no han instalado ni interactuado previamente con la aplicación. Por ejemplo, la necesidad de enviar información importante a todos los usuarios de la organización. Para estos escenarios, puede usar la API de Microsoft Graph para instalar proactivamente el bot para los usuarios.

## <a name="permissions"></a>Permisos

Los permisos de tipo de recurso [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) de Microsoft Graph le ayudan a administrar el ciclo de vida de instalación de la aplicación para todos los ámbitos de usuario (personal) o de equipo (canal) dentro de la plataforma Microsoft Teams web:

|Permiso de aplicación | Descripción|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Permite que Teams aplicación se lea, instale, actualice y se desinstale para cualquier *usuario, sin* necesidad de iniciar sesión o usar previamente.|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Permite que Teams aplicación se lea, instale, actualice y se desinstale en cualquier *equipo, sin* necesidad de iniciar sesión o usar previamente.|

Para usar estos permisos, debe agregar una clave [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) al manifiesto de la aplicación con los siguientes valores:

* **id**: El Azure Active Directory de la aplicación.
* **recurso**: la dirección URL del recurso para la aplicación.

> [!NOTE]
>
> * El bot requiere permisos delegados de aplicación y no de usuario porque la instalación es para otros usuarios.
>
> * Un Azure AD de inquilinos debe [conceder explícitamente permisos a una aplicación](/graph/security-authorization#grant-permissions-to-an-application). Después de conceder permisos a la aplicación, todos los miembros del Azure AD obtienen los permisos concedidos.

## <a name="enable-proactive-app-installation-and-messaging"></a>Habilitar la instalación proactiva de aplicaciones y la mensajería

> [!IMPORTANT]
> Microsoft Graph solo puede instalar aplicaciones publicadas en la tienda de aplicaciones de su organización o en la Teams de aplicaciones.

### <a name="create-and-publish-your-proactive-messaging-bot-for-teams"></a>Crear y publicar el bot de mensajería proactiva para Teams

Para empezar, necesita un [bot](../../bots/how-to/create-a-bot-for-teams.md) para Teams con capacidades de mensajería proactiva [](../../concepts/bots/bot-conversations/bots-conv-proactive.md) que se encuentra en la tienda de [](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) aplicaciones de la organización o en la [Teams de almacenamiento](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).

> [!TIP]
> La plantilla de aplicación [*de Communicator*](../..//samples/app-templates.md#company-communicator) lista para producción permite la mensajería de difusión y es un buen comienzo para crear la aplicación de bot proactiva.

### <a name="get-the-teamsappid-for-your-app"></a>Obtener la `teamsAppId` aplicación para

Puede recuperar las siguientes `teamsAppId` formas:

* Desde el catálogo de aplicaciones de la organización:

    **Referencia Graph página de Microsoft:** [tipo de recurso teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

    **Solicitud HTTP GET** :

    ```http
    GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
    ```

    La solicitud debe devolver un `teamsApp` objeto `id`, que es el identificador de aplicación generado por el catálogo de la aplicación. Esto es diferente del identificador que proporcionaste en el manifiesto Teams aplicación:

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

* Si la aplicación ya se ha cargado o se ha cargado localmente para un usuario en el ámbito personal:

    **Referencia Graph página de Microsoft: Enumerar** [las aplicaciones instaladas para el usuario](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

    **Solicitud HTTP GET** :

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

* Si la aplicación ya se ha cargado o se ha cargado localmente para un canal en el ámbito de grupo:

    **Referencia Graph página de Microsoft: Enumerar** [aplicaciones en equipo](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

    **Solicitud HTTP GET** :

    ```http
    GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

    > [!TIP]
    > Para restringir la lista de resultados, puede filtrar cualquiera de los campos del [**objeto teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) .

### <a name="determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>Determinar si el bot está instalado actualmente para un destinatario de mensaje

Puede determinar si el bot está instalado actualmente para un destinatario de mensaje de la siguiente manera:

**Referencia Graph página de Microsoft: Enumerar** [las aplicaciones instaladas para el usuario](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Solicitud HTTP GET** :

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

La solicitud devuelve:

* Una matriz vacía si la aplicación no está instalada.
* Una matriz con un único [objeto teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) si la aplicación está instalada.

### <a name="install-your-app"></a>Instalar la aplicación

Puedes instalar la aplicación de la siguiente manera:

**Referencia Graph página de Microsoft:** [Instalar aplicación para el usuario](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Solicitud HTTP POST** :

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

Si el usuario tiene Microsoft Teams, la instalación de la aplicación se produce inmediatamente. Es posible que sea necesario reiniciar para ver la aplicación instalada.

### <a name="retrieve-the-conversation-chatid"></a>Recuperar la conversación `chatId`

Cuando la aplicación está instalada para el usuario, el bot `conversationUpdate` recibe una notificación de evento que contiene la información necesaria para enviar el mensaje proactivo.[](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)

**Referencia Graph página de Microsoft:** [Obtener chat](/graph/api/chat-get?view=graph-rest-v1.0&tabs=http&preserve-view=true)

1. Debes tener el archivo `{teamsAppInstallationId}`. Si no lo tiene, use lo siguiente:

    **Solicitud HTTP GET** :

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
    ```

    La **propiedad id** de la respuesta es .`teamsAppInstallationId`

1. Realice la siguiente solicitud para capturar :`chatId`

    **Solicitud HTTP GET** (permiso — `TeamsAppInstallation.ReadWriteSelfForUser.All`):  

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
    ```

    La **propiedad id** de la respuesta es .`chatId`

    También puede recuperar la solicitud `chatId` con la siguiente solicitud, pero requiere el permiso más `Chat.Read.All` amplio:

    **Solicitud HTTP GET** (permiso — `Chat.Read.All`):

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
    ```

### <a name="send-proactive-messages"></a>Enviar mensajes proactivos

El bot puede [enviar mensajes proactivos](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) después de que el bot se haya agregado para un usuario o un equipo y haya recibido toda la información del usuario.

## <a name="code-snippets"></a>Fragmentos de código

El siguiente código proporciona un ejemplo de envío de mensajes proactivos:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
public async Task<int> SendNotificationToAllUsersAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
   int msgSentCount = 0;

   // Send notification to all the members
   foreach (var conversationReference in _conversationReferences.Values)
   {
       await turnContext.Adapter.ContinueConversationAsync(_configuration["MicrosoftAppId"], conversationReference, BotCallback, cancellationToken);
       msgSentCount++;
   }

   return msgSentCount;
}

private async Task BotCallback(ITurnContext turnContext, CancellationToken cancellationToken)
{
   await turnContext.SendActivityAsync("Proactive hello.");
}
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript
server.get('/api/notify', async (req, res) => {
    for (const conversationReference of Object.values(conversationReferences)) {
        await adapter.continueConversationAsync(process.env.MicrosoftAppId, conversationReference, async context => {
            await context.sendActivity('proactive hello');
        });
    }

    res.setHeader('Content-Type', 'text/html');
    res.writeHead(200);
    res.write('<html><body><h1>Proactive messages have been sent.</h1></body></html>');
    res.end();
});
```

---

## <a name="code-sample"></a>Ejemplo de código

| **Nombre de ejemplo** | **Descripción** | **.NET** | **Node.js** |
|---------------|--------------|--------|-------------|
| Instalación proactiva de la aplicación y envío de notificaciones proactivas | En este ejemplo se muestra cómo puede usar la instalación proactiva de la aplicación para usuarios y enviar notificaciones proactivas mediante una llamada a las API de Microsoft Graph. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/nodejs) |

## <a name="additional-code-samples"></a>Ejemplos de código adicionales
>
> [!div class="nextstepaction"]
> [**Ejemplos de código de mensajería proactiva de Teams**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)

## <a name="see-also"></a>Vea también

* [Administrar directivas de configuración de aplicación en Microsoft Teams](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [Enviar notificaciones proactivas a usuarios SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

---
title: Usar Microsoft Graph para autorizar la instalación y mensajería proactiva de bots en Teams
description: Describe la mensajería proactiva en Teams y cómo implementarla. Obtenga información sobre cómo habilitar la instalación proactiva de aplicaciones y la mensajería mediante un código de ejemplo.
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: Graph de instalación del chat de mensajería proactiva de Teams
ms.openlocfilehash: 7a133b91aabe920b109b644331bc6526cd950858
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757706"
---
# <a name="proactive-installation-of-apps-using-graph-api-to-send-messages"></a>Instalación proactiva de aplicaciones con Graph API para enviar mensajes

## <a name="proactive-messaging-in-teams"></a>Mensajería proactiva en Teams

Los bots inician mensajes proactivos para iniciar conversaciones con un usuario. Sirven para muchos propósitos, como el envío de mensajes de bienvenida, la realización de encuestas o sondeos y la difusión de notificaciones de toda la organización. Los mensajes proactivos en Teams se pueden entregar como **ad-hoc** o conversaciones **basadas en diálogos**:

|Tipo de mensaje | Descripción |
|----------------|-------------- |
|Mensaje proactivo ad hoc| El bot intercepta un mensaje sin interrumpir el flujo de conversación.|
|Mensaje proactivo basado en diálogos | El bot crea un nuevo subproceso de diálogo, asume el control de una conversación, entrega el mensaje proactivo, lo cierra y devuelve el control al diálogo anterior.|

## <a name="proactive-app-installation-in-teams"></a>Instalación proactiva de aplicaciones en Teams

Antes de que el bot pueda enviar mensajes de forma proactiva a un usuario, debe estar instalado como una aplicación personal o en un equipo del que el usuario sea miembro. En ocasiones, debe enviar mensajes de forma proactiva a los usuarios que no han instalado o han interactuado previamente con la aplicación. Por ejemplo, si necesita enviar información importante a todos los usuarios de su organización, puede usar microsoft Graph API para instalar el bot de forma proactiva para los usuarios.

## <a name="permissions"></a>Permisos

Los permisos del [tipo de recurso teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) de Microsoft Graph le ayudan a administrar el ciclo de vida de instalación de la aplicación para todos los ámbitos de usuario (personal) o de equipo (canal) dentro de la plataforma de Microsoft Teams:

|Permiso de la aplicación | Descripción|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Permite que una aplicación de Teams se lea, instale, actualice y desinstale por sí misma para cualquier *usuario*, sin que se haya usado o iniciado sesión en ella previamente.|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Permite que una aplicación de Teams se lea, instale, actualice y desinstale a sí misma en cualquier *equipo* sin que se haya usado o iniciado sesión en ella previamente.|

Para usar estos permisos, debe agregar una clave [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) al manifiesto de la aplicación con los siguientes valores:

* **id**: El id. de la aplicación de Azure Active Directory.
* **resource**: La dirección URL del recurso de la aplicación.

> [!NOTE]
>
> * El bot requiere permisos delegados de aplicación y no de usuario porque la instalación es para otros usuarios.
>
> * El administrador de inquilinos de Azure AD debe [conceder los permisos de forma explícita a la aplicación](/graph/security-authorization#grant-permissions-to-an-application). Una vez que se conceden permisos a la aplicación, todos los miembros del espacio empresarial de Azure AD obtienen los permisos concedidos.

## <a name="enable-proactive-app-installation-and-messaging"></a>Habilitar la instalación y mensajería proactivas de la aplicación

> [!IMPORTANT]
> Microsoft Graph solo puede instalar aplicaciones publicadas en la tienda de aplicaciones de su organización o en la tienda de Teams.

### <a name="create-and-publish-your-proactive-messaging-bot-for-teams"></a>Crear y publicar el bot de mensajería proactiva para Teams

Para empezar, necesita un [bot para Teams](../../bots/how-to/create-a-bot-for-teams.md) con la funcionalidad de [mensajería proactiva](../../concepts/bots/bot-conversations/bots-conv-proactive.md) que se encuentra en la [tienda de aplicaciones de la organización](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) o en la [tienda de Teams](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).

> [!TIP]
> La plantilla de la aplicación lista para producción [*Company Communicator*](../..//samples/app-templates.md#company-communicator) permite la difusión de mensajes y es un buen punto de partida para crear la aplicación de bot proactiva.

### <a name="get-the-teamsappid-for-your-app"></a>Obtener el `teamsAppId` para la aplicación

Puede recuperar el `teamsAppId` de las siguientes maneras:

* Desde al catálogo de aplicaciones de su organización:

    **Referencia de la página de Microsoft Graph:** [tipo de recurso teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

    Solicitud **HTTP GET**:

    ```http
    GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
    ```

    La solicitud debe devolver un objeto de `teamsApp` `id`, que es el id. de aplicación generado por el catálogo de la aplicación. Esto es diferente del id. que proporcionó en el manifiesto de la aplicación de Teams:

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

* Si la aplicación ya fue cargada o transferida localmente para un usuario en el ámbito personal:

    **Referencia de la página de Microsoft Graph:** [Enumerar las aplicaciones instaladas para el usuario](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

    Solicitud **HTTP GET**:

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

* Si la aplicación ya fue cargada o transferida localmente para un canal en el ámbito del equipo:

    **Referencia de la página de Microsoft Graph:** [Enumerar las aplicaciones en el equipo](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

    Solicitud **HTTP GET**:

    ```http
    GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

    > [!TIP]
    > Para restringir la lista de resultados, puede filtrar cualquiera de los campos del objeto [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true).

### <a name="determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>Determinar si el bot está instalado actualmente para algún destinatario del mensaje

Puede determinar si el bot está instalado actualmente para un destinatario del mensaje de la siguiente manera:

**Referencia de la página de Microsoft Graph:** [Enumerar las aplicaciones instaladas para el usuario](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

Solicitud **HTTP GET**:

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

La solicitud devuelve:

* Matriz vacía si la aplicación no está instalada.
* Una matriz con un objeto [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) único si la aplicación está instalada.

### <a name="install-your-app"></a>Instalar la aplicación

Puede instalar la aplicación de la siguiente manera:

**Referencia de página de Microsoft Graph:** [Instalación de la aplicación para el usuario](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

Solicitud **HTTP POST**:

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

Si el usuario está ejecutando Microsoft Teams, la instalación de la aplicación se produce inmediatamente. Podría ser necesario reiniciar para ver la aplicación instalada.

### <a name="retrieve-the-conversation-chatid"></a>Recuperar la conversación `chatId`

Cuando se instala la aplicación para el usuario, el bot recibe una [notificación de evento](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) `conversationUpdate` que contiene la información necesaria para enviar el mensaje proactivo.

**Referencia de página de Microsoft Graph:** [Obtener chat](/graph/api/chat-get?view=graph-rest-v1.0&tabs=http&preserve-view=true)

1. Debe tener el `{teamsAppInstallationId}` de la aplicación. Si no lo tiene, use lo siguiente:

    Solicitud **HTTP GET**:

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
    ```

    La propiedad del **id** de la respuesta es el `teamsAppInstallationId`.

1. Realice la siguiente solicitud para capturar el `chatId`:

    Solicitud **HTTP GET** (permiso):`TeamsAppInstallation.ReadWriteSelfForUser.All`  

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
    ```

    La propiedad del **id** de la respuesta es el `chatId`.

    También puede recuperar el `chatId` con la siguiente solicitud, aunque requiere un permiso `Chat.Read.All` más amplio:

    Solicitud **HTTP GET** (permiso):`Chat.Read.All`

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
    ```

### <a name="send-proactive-messages"></a>Enviar mensajes proactivos

El bot puede [enviar mensajes proactivos](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) para un usuario o equipo después de agregado y después de que haya recibido toda la información del usuario.

## <a name="code-snippets"></a>Fragmentos de código

El código siguiente proporciona un ejemplo de envío de mensajes proactivos:

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

## <a name="additional-code-samples"></a>Ejemplo de código adicional
>
> [!div class="nextstepaction"]
> [**Ejemplos de código de mensajería proactiva de Teams**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)

## <a name="see-also"></a>Vea también

* [Administrar directivas de configuración de aplicación en Microsoft Teams](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [Enviar notificaciones proactivas a los usuarios SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

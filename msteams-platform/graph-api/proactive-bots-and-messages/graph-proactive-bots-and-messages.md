---
title: Use Microsoft Graph para autorizar la instalación proactiva de bots y la mensajería en Teams
description: Describe la mensajería proactiva en Teams y cómo implementarla. Obtenga información sobre cómo habilitar la instalación proactiva de aplicaciones y la mensajería mediante el ejemplo de código.
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: instalación proactiva de chat de mensajería de teams Graph
ms.openlocfilehash: a3b7ffd24f7601c8247f1f11c6fe1a562d9cd847
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/10/2021
ms.locfileid: "60888009"
---
# <a name="proactive-installation-of-apps-using-graph-api-to-send-messages"></a>Instalación proactiva de aplicaciones con Graph API para enviar mensajes

>[!IMPORTANT]
> Microsoft Graph y Microsoft Teams vistas previas públicas están disponibles para obtener acceso anticipado y comentarios. Aunque esta versión se ha sometido a pruebas exhaustivas, no está diseñada para su uso en producción.

## <a name="proactive-messaging-in-teams"></a>Mensajería proactiva en Teams

Los bots inician mensajes proactivos para iniciar conversaciones con un usuario. Sirven para muchos propósitos, como enviar mensajes de bienvenida, realizar encuestas o sondeos y difundir notificaciones en toda la organización. Los mensajes proactivos Teams pueden entregarse como conversaciones **ad-hoc** o **basadas en cuadros de** diálogo:

|Tipo de mensaje | Descripción |
|----------------|-------------- |
|Mensaje proactivo ad hoc| El bot interje un mensaje sin interrumpir el flujo de conversación.|
|Mensaje proactivo basado en cuadros de diálogo | El bot crea un nuevo subproceso de diálogo, toma el control de una conversación, entrega el mensaje proactivo, se cierra y devuelve el control al cuadro de diálogo anterior.|

## <a name="proactive-app-installation-in-teams"></a>Instalación proactiva de aplicaciones en Teams

Para que el bot pueda enviar un mensaje de forma proactiva a un usuario, debe instalarse como una aplicación personal o en un equipo en el que el usuario sea miembro. En ocasiones, debes enviar mensajes de forma proactiva a los usuarios que no han instalado ni interactuado previamente con la aplicación. Por ejemplo, la necesidad de enviar información importante a todos los usuarios de la organización. Para estos escenarios, puede usar la API de Microsoft Graph para instalar proactivamente el bot para los usuarios.

## <a name="permissions"></a>Permisos

Los permisos de tipo de recurso [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) de Microsoft Graph le ayudan a administrar el ciclo de vida de instalación de la aplicación para todos los ámbitos de usuario (personal) o de equipo (canal) de la plataforma Microsoft Teams usuario:

|Permiso de aplicación | Descripción|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Permite que Teams aplicación lea, instale, actualice y desinstale a sí misma para cualquier *usuario,* sin iniciar sesión o usar previamente.|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Permite que Teams aplicación se lea, instale, actualice y se desinstale en cualquier *equipo,* sin necesidad de iniciar sesión o usar previamente.|

Para usar estos permisos, debe agregar una clave [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) al manifiesto de la aplicación con los siguientes valores:

* **id:** El identificador Azure Active Directory aplicación (AAD).
* **recurso:** la dirección URL del recurso para la aplicación.

> [!NOTE]
>
> * El bot requiere permisos delegados de aplicación y no de usuario porque la instalación es para otros usuarios.
>
> * Un AAD de inquilinos debe [conceder explícitamente permisos a una aplicación](/graph/security-authorization#grant-permissions-to-an-application). Después de conceder permisos a la aplicación, todos los miembros del AAD obtienen los permisos concedidos.

## <a name="enable-proactive-app-installation-and-messaging"></a>Habilitar la instalación proactiva de aplicaciones y la mensajería

> [!IMPORTANT]
> Microsoft Graph solo puede instalar aplicaciones publicadas en la tienda de aplicaciones de su organización o en la Teams de aplicaciones.

### <a name="create-and-publish-your-proactive-messaging-bot-for-teams"></a>Crear y publicar el bot de mensajería proactiva para Teams

Para empezar, necesita un [bot](../../bots/how-to/create-a-bot-for-teams.md) para Teams [](../../concepts/bots/bot-conversations/bots-conv-proactive.md) con capacidades de [](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) mensajería proactiva que se encuentra en la tienda de aplicaciones de su organización o en la [Teams de almacenamiento](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).

> [!TIP]
> La plantilla de aplicación [*de*](../..//samples/app-templates.md#company-communicator) Communicator lista para producción permite la mensajería de difusión y es un buen comienzo para crear la aplicación de bot proactiva.

### <a name="get-the-teamsappid-for-your-app"></a>Obtener la `teamsAppId` aplicación para

Puede recuperar las `teamsAppId` siguientes formas:

* Desde el catálogo de aplicaciones de la organización:

    **Referencia Graph página de Microsoft:** [tipo de recurso teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

    **Solicitud HTTP GET:**

    ```http
    GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
    ```

    La solicitud debe devolver un objeto , que es el identificador de aplicación generado por `teamsApp` el catálogo de la `id` aplicación. Esto es diferente del identificador que proporcionaste en el manifiesto Teams aplicación:

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

    **Solicitud HTTP GET:**

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

* Si la aplicación ya se ha cargado o se ha cargado localmente para un canal en el ámbito de grupo:

    **Referencia Graph página de Microsoft: Enumerar** [aplicaciones en equipo](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

    **Solicitud HTTP GET:**

    ```http
    GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

    > [!TIP]
    > Para restringir la lista de resultados, puede filtrar cualquiera de los campos del [**objeto teamsApp.**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

### <a name="determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>Determinar si el bot está instalado actualmente para un destinatario de mensaje

Puede determinar si el bot está instalado actualmente para un destinatario de mensaje de la siguiente manera:

**Referencia Graph página de Microsoft: Enumerar** [las aplicaciones instaladas para el usuario](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Solicitud HTTP GET:**

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

La solicitud devuelve:

* Una matriz vacía si la aplicación no está instalada.
* Una matriz con un único [objeto teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) si la aplicación está instalada.

### <a name="install-your-app"></a>Instalar la aplicación

Puedes instalar la aplicación de la siguiente manera:

**Referencia Graph página de Microsoft:** [Instalar aplicación para el usuario](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Solicitud HTTP POST:**

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

Si el usuario tiene Microsoft Teams, la instalación de la aplicación se produce inmediatamente. Es posible que sea necesario reiniciar para ver la aplicación instalada.

### <a name="retrieve-the-conversation-chatid"></a>Recuperar la conversación `chatId`

Cuando la aplicación está instalada para el usuario, el bot recibe una notificación de evento que contiene la `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) información necesaria para enviar el mensaje proactivo.

**Referencia Graph página de Microsoft:** [Obtener chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)

1. Debes tener el `{teamsAppInstallationId}` archivo . Si no lo tiene, use lo siguiente:

    **Solicitud HTTP GET:**

    ```http
    GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
    ```

    La **propiedad id** de la respuesta es `teamsAppInstallationId` .

1. Realice la siguiente solicitud para capturar `chatId` :

    **Solicitud HTTP GET** (permiso `TeamsAppInstallation.ReadWriteSelfForUser.All` — ):  

    ```http
    GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
    ```

    La **propiedad id** de la respuesta es `chatId` .

    También puede recuperar la `chatId` solicitud con la siguiente solicitud, pero requiere el permiso más `Chat.Read.All` amplio:

    **Solicitud HTTP GET** (permiso `Chat.Read.All` — ):

    ```http
    GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
    ```

### <a name="send-proactive-messages"></a>Enviar mensajes proactivos

El bot puede [enviar mensajes proactivos](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) después de que el bot se haya agregado para un usuario o un equipo y haya recibido toda la información del usuario.

## <a name="code-sample"></a>Ejemplo de código

| **Nombre de ejemplo** | **Descripción** | **.NET** | **Node.js** |
|---------------|--------------|--------|-------------|
| Instalación proactiva de la aplicación y envío de notificaciones proactivas | En este ejemplo se muestra cómo usar la instalación proactiva de la aplicación para los usuarios y enviar notificaciones proactivas llamando a las API Graph Microsoft. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/nodejs) |

## <a name="additional-code-samples"></a>Ejemplos de código adicionales
>
> [!div class="nextstepaction"]
> [**Teams de código de mensajería proactiva**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)

## <a name="see-also"></a>Consulte también

* [**Administrar directivas de configuración de aplicaciones en Microsoft Teams**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [Enviar notificaciones proactivas a usuarios SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

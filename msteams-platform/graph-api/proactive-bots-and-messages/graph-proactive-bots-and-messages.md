---
title: Use Microsoft Graph para autorizar la instalación proactiva de bots y la mensajería en Teams
description: Describe la mensajería proactiva en Teams y cómo implementar.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: instalación proactiva de chat de mensajería de teams Graph
ms.openlocfilehash: 62974f6f3b26e53558658f0b6cfda815dee1de8a
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101803"
---
# <a name="proactive-installation-of-apps-using-graph-api-and-send-messages"></a>Instalación proactiva de aplicaciones usando la API de Graph y el envío de mensajes

>[!IMPORTANT]
> Microsoft Graph y Microsoft Teams vistas previas públicas están disponibles para obtener acceso anticipado y comentarios. Aunque esta versión se ha sometido a pruebas exhaustivas, no está diseñada para su uso en producción.

## <a name="proactive-messaging-in-teams"></a>Mensajería proactiva en Teams

Los bots inician mensajes proactivos para iniciar conversaciones con un usuario. Sirven para muchos propósitos, como enviar mensajes de bienvenida, realizar encuestas o sondeos y difundir notificaciones en toda la organización. Los mensajes proactivos Teams pueden entregarse como conversaciones **ad-hoc** o **basadas en cuadros de** diálogo:

|Tipo de mensaje | Descripción |
|----------------|-------------- |
|Mensaje proactivo ad hoc| El bot interje un mensaje sin interrumpir el flujo de conversación.|
|Mensaje proactivo basado en cuadros de diálogo | El bot crea un nuevo subproceso de diálogo, toma el control de una conversación, entrega el mensaje proactivo, se cierra y devuelve el control al cuadro de diálogo anterior.|

Vea Enviar [notificaciones proactivas a los usuarios SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true).

## <a name="proactive-app-installation-in-teams"></a>Instalación proactiva de aplicaciones en Teams

Para que el bot pueda enviar un mensaje de forma proactiva a un usuario, debe instalarse como una aplicación personal o en un equipo en el que el usuario sea miembro. En ocasiones, debes enviar mensajes de forma proactiva a los usuarios que no han instalado ni interactuado previamente con la aplicación. Por ejemplo, la necesidad de enviar información vital a todos los usuarios de la organización. Para estos escenarios, puede usar la API de Microsoft Graph para instalar proactivamente el bot para los usuarios.

## <a name="permissions"></a>Permisos

Los permisos de tipo de recurso [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) de Microsoft Graph le ayudan a administrar el ciclo de vida de instalación de la aplicación para todos los ámbitos de usuario (personal) o de equipo (canal) de la plataforma Microsoft Teams usuario:

|Permisos de aplicación | Descripción|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Permite que Teams aplicación lea, instale, actualice y desinstale a sí misma para cualquier **usuario,** sin iniciar sesión o usar previamente.|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Permite que Teams aplicación se lea, instale, actualice y se desinstale en cualquier **equipo,** sin necesidad de iniciar sesión o usar previamente.|

Para usar estos permisos, debe agregar una clave [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) al manifiesto de la aplicación con los siguientes valores:
> [!div class="checklist"]
> [!div class="checklist"]
>
> * **id:** el identificador de la aplicación de Azure AD.
> * **recurso:** la dirección URL del recurso para la aplicación.
>
>[!NOTE]
>
> * El bot requiere permisos delegados de aplicación y no de usuario porque la instalación es para otros usuarios.
>
> * Un administrador de inquilinos de Azure AD debe [conceder explícitamente permisos a una aplicación](/graph/security-authorization#grant-permissions-to-an-application). Después de conceder permisos a una aplicación, todos los miembros del inquilino de Azure AD obtienen los permisos concedidos.

## <a name="enable-proactive-app-installation-and-messaging"></a>Habilitar la instalación proactiva de aplicaciones y la mensajería

> [!IMPORTANT]
>Microsoft Graph solo puede instalar aplicaciones publicadas en la tienda de aplicaciones de su organización o en la Teams de aplicaciones.

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a>✔ Crear y publicar el bot de mensajería proactiva para Teams

Para empezar, necesita un [bot](../../bots/how-to/create-a-bot-for-teams.md) para Teams [](../../concepts/bots/bot-conversations/bots-conv-proactive.md) con capacidades de [](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) mensajería proactiva que se encuentra en la tienda de aplicaciones de su organización o en la [Teams de almacenamiento](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).

>[!TIP]
> La plantilla de aplicación [**de Communicator**](../..//samples/app-templates.md#company-communicator) lista para producción permite la mensajería de difusión y es una buena base para crear la aplicación de bot proactiva.

### <a name="-get-the-teamsappid-for-your-app"></a>✔ Obtener la `teamsAppId` para la aplicación

**1.** Necesita los `teamsAppId` pasos siguientes.

Se puede recuperar desde el catálogo de aplicaciones de `teamsAppId` la organización:

**Referencia Graph página de Microsoft:** [tipo de recurso teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

**Solicitud HTTP GET:**

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

La solicitud debe devolver un `teamsApp` objeto. El objeto devuelto es el identificador de aplicación generado por el catálogo de la aplicación y es diferente del identificador que proporcionaste en el manifiesto Teams `id` aplicación:

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

**2.**  Si la aplicación ya se ha cargado o se ha cargado localmente para un usuario en el ámbito personal, puede recuperar lo `teamsAppId` siguiente:

**Referencia Graph página de Microsoft: Enumerar** [las aplicaciones instaladas para el usuario](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Solicitud HTTP GET:**

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

**3.** Si la aplicación se ha cargado o se ha cargado localmente para un canal en el ámbito de grupo, puede recuperar lo `teamsAppId` siguiente:

**Referencia Graph página de Microsoft: Enumerar** [aplicaciones en equipo](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Solicitud HTTP GET:**

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> Para restringir la lista de resultados, puede filtrar en cualquiera de los campos del [**objeto teamsApp.**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>✔ Determine si el bot está instalado actualmente para un destinatario de mensaje

**Referencia Graph página de Microsoft: Enumerar** [las aplicaciones instaladas para el usuario](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Solicitud HTTP GET:**

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

Esta solicitud devuelve una matriz vacía si la aplicación no está instalada y una matriz con un único [objeto teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) si la aplicación está instalada.

### <a name="-install-your-app"></a>✔ instalar la aplicación

**Referencia Graph página de Microsoft:** [Instalar aplicación para el usuario](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Solicitud HTTP POST:**

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

Si el usuario tiene Microsoft Teams, la instalación de la aplicación se ve inmediatamente. Es posible que sea necesario reiniciar para ver la aplicación instalada.

### <a name="-retrieve-the-conversation-chatid"></a>✔ recuperar el **chatId de conversación**

Cuando la aplicación está instalada para el usuario, el bot recibe una notificación de evento que contiene la `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) información necesaria para enviar el mensaje proactivo.

También `chatId` se puede recuperar de la siguiente manera:

**Referencia Graph página de Microsoft:** [Obtener chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)

**1.** Debe necesitar el `{teamsAppInstallationId}` archivo . Si no lo tiene, use lo siguiente:

**Solicitud HTTP GET:**

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

La **propiedad id** de la respuesta es `teamsAppInstallationId` .

**2.** Realice la siguiente solicitud para capturar `chatId` :

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

### <a name="-send-proactive-messages"></a>✔ enviar mensajes proactivos

El bot puede [enviar mensajes proactivos](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) después de que el bot se haya agregado para un usuario o un equipo y haya recibido toda la información del usuario.

## <a name="related-topic-for-teams-administrators"></a>Tema relacionado para Teams administradores
>
> [!div class="nextstepaction"]
> [**Administrar directivas de configuración de aplicación en Microsoft Teams**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a>Ver ejemplos de código adicionales
>
> [!div class="nextstepaction"]
> [**Teams de código de mensajería proactiva**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>

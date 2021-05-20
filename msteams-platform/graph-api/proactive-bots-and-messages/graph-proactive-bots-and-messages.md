---
title: Use Microsoft Graph para autorizar la instalación y mensajería proactiva de bots en Teams
description: Describe la mensajería proactiva en Teams y cómo implementar.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: equipos de instalación proactiva de chat de mensajería Graph
ms.openlocfilehash: 06b50e5ab8594c257959430383bab5e355af4e06
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566155"
---
# <a name="proactive-installation-of-apps-using-graph-api-and-send-messages"></a>Instalación proactiva de aplicaciones usando la API de Graph y el envío de mensajes

>[!IMPORTANT]
> Las vistas previas públicas de Microsoft Graph y Microsoft Teams están disponibles para el acceso anticipado y los comentarios. Aunque esta versión ha sido sometida a extensas pruebas, no está destinada a su uso en producción.

## <a name="proactive-messaging-in-teams"></a>Mensajería proactiva en Teams

Los bots inician mensajes proactivos para iniciar conversaciones con un usuario. Sirven para muchos propósitos, incluyendo el envío de mensajes de bienvenida, la realización de encuestas o encuestas, y la difusión de notificaciones en toda la organización. Los mensajes proactivos en Teams se pueden entregar como conversaciones **ad hoc** o basadas **en cuadros de diálogo:**

|Tipo de mensaje | Descripción |
|----------------|-------------- |
|Mensaje proactivo ad hoc| El bot interpone un mensaje sin interrumpir el flujo de conversación.|
|Mensaje proactivo basado en diálogos | El bot crea un nuevo subproceso de cuadro de diálogo, toma el control de una conversación, entrega el mensaje proactivo, cierra y devuelve el control al cuadro de diálogo anterior.|

## <a name="proactive-app-installation-in-teams"></a>Instalación proactiva de aplicaciones en Teams

Antes de que el bot pueda enviar mensajes de forma proactiva a un usuario, debe instalarse como una aplicación personal o en un equipo donde el usuario sea miembro. A veces, debe enviar mensajes de forma proactiva a los usuarios que no hayan instalado o interactuado previamente con la aplicación. Por ejemplo, la necesidad de enviar información vital a todos los miembros de su organización. Para estos escenarios, puede usar la API de Microsoft Graph para instalar de forma proactiva el bot para los usuarios.

## <a name="permissions"></a>Permisos

Permisos de tipo de recurso de Microsoft Graph [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) le ayudan a administrar el ciclo de vida de instalación de la aplicación para todos los ámbitos de usuario (personal) o de equipo (canal) dentro de la plataforma Microsoft Teams:

|Permisos de aplicación | Descripción|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Permite que una aplicación Teams lea, instale, actualice y desinstale para cualquier **usuario,** sin inicio de sesión o uso previo.|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Permite que una aplicación Teams lea, instale, actualice y desinstale en cualquier **equipo,** sin inicio de sesión o uso previo.|

Para usar estos permisos, debe agregar una clave [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) al manifiesto de la aplicación con los siguientes valores:
> [!div class="checklist"]
> [!div class="checklist"]
>
> * **id:** el identificador de la aplicación de Azure AD.
> * **recurso** : la dirección URL del recurso de la aplicación.
>
>[!NOTE]
>
> * El bot requiere permisos delegados por aplicación y no por el usuario porque la instalación es para otros.
>
> * Un administrador de inquilinos de Azure AD debe [conceder explícitamente permisos a una aplicación.](/graph/security-authorization#grant-permissions-to-an-application) Después de conceder permisos a una aplicación, todos los miembros del inquilino de Azure AD obtienen los permisos concedidos.

## <a name="enable-proactive-app-installation-and-messaging"></a>Habilitar la instalación proactiva de aplicaciones y mensajería

> [!IMPORTANT]
>Microsoft Graph solo puede instalar aplicaciones publicadas en la tienda de aplicaciones de su organización o en la tienda de Teams.

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a>✔ Crear y publicar el bot de mensajería proactiva para Teams

Para empezar, necesita un [bot para Teams](../../bots/how-to/create-a-bot-for-teams.md) con capacidades de mensajería [proactivas](../../concepts/bots/bot-conversations/bots-conv-proactive.md) que se en la [tienda de aplicaciones de](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) su organización o en la tienda [de Teams.](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store)

>[!TIP]
> La plantilla [**de aplicación Communicator empresa**](../..//samples/app-templates.md#company-communicator) lista para la producción permite la difusión de mensajes y es una buena base para crear su aplicación de bot proactiva.

### <a name="-get-the-teamsappid-for-your-app"></a>✔ Obtener la `teamsAppId` para la aplicación

**1.** Necesita los `teamsAppId` siguientes pasos.

Se `teamsAppId` puede recuperar del catálogo de aplicaciones de su organización:

**Referencia de página de Microsoft Graph:** [tipo de recurso teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

**Solicitud HTTP GET:**

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

La solicitud debe devolver un `teamsApp` objeto. El objeto devuelto `id` es el identificador de aplicación generado por catálogo de la aplicación y es diferente del identificador que proporcionó en el manifiesto de la aplicación Teams:

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

**2.**  Si la aplicación ya se ha cargado o cargado lateralmente para un usuario en el ámbito personal, puede recuperar lo `teamsAppId` siguiente:

**Referencia de página de Microsoft Graph:** [lista de aplicaciones instaladas para el usuario](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Solicitud HTTP GET:**

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

**3.** Si la aplicación se ha cargado o descargado lateralmente para un canal en el ámbito del equipo, puede recuperar lo `teamsAppId` siguiente:

**Referencia de página de Microsoft Graph:** [lista de aplicaciones en equipo](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Solicitud HTTP GET:**

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> Para restringir la lista de resultados, puede filtrar en cualquiera de los campos de [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) objeto.

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>✔ Determinar si el bot está instalado actualmente para un destinatario de mensaje

**Referencia de página de Microsoft Graph:** [lista de aplicaciones instaladas para el usuario](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Solicitud HTTP GET:**

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

Esta solicitud devuelve una matriz vacía si la aplicación no está instalada y una matriz con un único [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) objeto si la aplicación está instalada.

### <a name="-install-your-app"></a>✔ Instalar la aplicación

**Referencia de página de Microsoft Graph:** [instalar la aplicación para el usuario](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Solicitud HTTP POST:**

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

Si el usuario tiene Microsoft Teams en ejecución, la instalación de la aplicación se ve inmediatamente. Es posible que sea necesario reiniciar para ver la aplicación instalada.

### <a name="-retrieve-the-conversation-chatid"></a>✔ Recuperar el **chat de conversaciónId**

Cuando la aplicación está instalada para el usuario, el bot recibe una `conversationUpdate` [notificación de evento](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) que contiene la información necesaria para enviar el mensaje proactivo.

También `chatId` se puede recuperar de la siguiente manera:

**Referencia de página de Microsoft Graph:** [obtener chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)

**1.** Debes necesitar la `{teamsAppInstallationId}` aplicación. Si no lo tiene, utilice lo siguiente:

**Solicitud HTTP GET:**

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

La propiedad **id** de la respuesta es el `teamsAppInstallationId` archivo .

**2.** Haga la siguiente solicitud para `chatId` obtener:

**Solicitud HTTP GET** (permiso — `TeamsAppInstallation.ReadWriteSelfForUser.All` ):  

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

La propiedad **id** de la respuesta es el `chatId` archivo .

También puede recuperar la `chatId` siguiente solicitud, pero requiere el permiso más `Chat.Read.All` amplio:

**Solicitud HTTP GET** (permiso — `Chat.Read.All` ):

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a>✔ Enviar mensajes proactivos

El bot puede [enviar mensajes proactivos](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) después de que se haya agregado el bot para un usuario o un equipo y haya recibido toda la información del usuario.

## <a name="see-also"></a>Vea también

* [**Administrar directivas de configuración de aplicaciones en Microsoft Teams**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [Enviar notificaciones proactivas a los usuarios SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

## <a name="view-additional-code-samples"></a>Ver ejemplos de código adicionales
>
> [!div class="nextstepaction"]
> [**Teams ejemplos proactivos de código de mensajería**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
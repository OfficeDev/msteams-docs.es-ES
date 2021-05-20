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
# <a name="proactive-installation-of-apps-using-graph-api-and-send-messages"></a><span data-ttu-id="f5348-104">Instalación proactiva de aplicaciones usando la API de Graph y el envío de mensajes</span><span class="sxs-lookup"><span data-stu-id="f5348-104">Proactive installation of apps using Graph API and send messages</span></span>

>[!IMPORTANT]
> <span data-ttu-id="f5348-105">Las vistas previas públicas de Microsoft Graph y Microsoft Teams están disponibles para el acceso anticipado y los comentarios.</span><span class="sxs-lookup"><span data-stu-id="f5348-105">Microsoft Graph and Microsoft Teams public previews are available for early access and feedback.</span></span> <span data-ttu-id="f5348-106">Aunque esta versión ha sido sometida a extensas pruebas, no está destinada a su uso en producción.</span><span class="sxs-lookup"><span data-stu-id="f5348-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="f5348-107">Mensajería proactiva en Teams</span><span class="sxs-lookup"><span data-stu-id="f5348-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="f5348-108">Los bots inician mensajes proactivos para iniciar conversaciones con un usuario.</span><span class="sxs-lookup"><span data-stu-id="f5348-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="f5348-109">Sirven para muchos propósitos, incluyendo el envío de mensajes de bienvenida, la realización de encuestas o encuestas, y la difusión de notificaciones en toda la organización.</span><span class="sxs-lookup"><span data-stu-id="f5348-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span> <span data-ttu-id="f5348-110">Los mensajes proactivos en Teams se pueden entregar como conversaciones **ad hoc** o basadas **en cuadros de diálogo:**</span><span class="sxs-lookup"><span data-stu-id="f5348-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="f5348-111">Tipo de mensaje</span><span class="sxs-lookup"><span data-stu-id="f5348-111">Message Type</span></span> | <span data-ttu-id="f5348-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="f5348-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="f5348-113">Mensaje proactivo ad hoc</span><span class="sxs-lookup"><span data-stu-id="f5348-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="f5348-114">El bot interpone un mensaje sin interrumpir el flujo de conversación.</span><span class="sxs-lookup"><span data-stu-id="f5348-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="f5348-115">Mensaje proactivo basado en diálogos</span><span class="sxs-lookup"><span data-stu-id="f5348-115">Dialog-based proactive message</span></span> | <span data-ttu-id="f5348-116">El bot crea un nuevo subproceso de cuadro de diálogo, toma el control de una conversación, entrega el mensaje proactivo, cierra y devuelve el control al cuadro de diálogo anterior.</span><span class="sxs-lookup"><span data-stu-id="f5348-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="f5348-117">Instalación proactiva de aplicaciones en Teams</span><span class="sxs-lookup"><span data-stu-id="f5348-117">Proactive app installation in Teams</span></span>

<span data-ttu-id="f5348-118">Antes de que el bot pueda enviar mensajes de forma proactiva a un usuario, debe instalarse como una aplicación personal o en un equipo donde el usuario sea miembro.</span><span class="sxs-lookup"><span data-stu-id="f5348-118">Before your bot can proactively message a user, it must be installed either as a personal app or in a team where the user is a member.</span></span> <span data-ttu-id="f5348-119">A veces, debe enviar mensajes de forma proactiva a los usuarios que no hayan instalado o interactuado previamente con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f5348-119">At times, you need to proactively message users that have not installed or previously interacted with your app.</span></span> <span data-ttu-id="f5348-120">Por ejemplo, la necesidad de enviar información vital a todos los miembros de su organización.</span><span class="sxs-lookup"><span data-stu-id="f5348-120">For example, the need to message vital information to everyone in your organization.</span></span> <span data-ttu-id="f5348-121">Para estos escenarios, puede usar la API de Microsoft Graph para instalar de forma proactiva el bot para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="f5348-121">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="f5348-122">Permisos</span><span class="sxs-lookup"><span data-stu-id="f5348-122">Permissions</span></span>

<span data-ttu-id="f5348-123">Permisos de tipo de recurso de Microsoft Graph [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) le ayudan a administrar el ciclo de vida de instalación de la aplicación para todos los ámbitos de usuario (personal) o de equipo (canal) dentro de la plataforma Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="f5348-123">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) permissions helps you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="f5348-124">Permisos de aplicación</span><span class="sxs-lookup"><span data-stu-id="f5348-124">Application permission</span></span> | <span data-ttu-id="f5348-125">Descripción</span><span class="sxs-lookup"><span data-stu-id="f5348-125">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="f5348-126">Permite que una aplicación Teams lea, instale, actualice y desinstale para cualquier **usuario,** sin inicio de sesión o uso previo.</span><span class="sxs-lookup"><span data-stu-id="f5348-126">Allows a Teams app to read, install, upgrade, and uninstall itself for any **user**, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="f5348-127">Permite que una aplicación Teams lea, instale, actualice y desinstale en cualquier **equipo,** sin inicio de sesión o uso previo.</span><span class="sxs-lookup"><span data-stu-id="f5348-127">Allows a Teams app to read, install, upgrade, and uninstall itself in any **team**, without prior sign in or use.</span></span>|

<span data-ttu-id="f5348-128">Para usar estos permisos, debe agregar una clave [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) al manifiesto de la aplicación con los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="f5348-128">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>
> [!div class="checklist"]
> [!div class="checklist"]
>
> * <span data-ttu-id="f5348-129">**id:** el identificador de la aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5348-129">**id** — your Azure AD app ID.</span></span>
> * <span data-ttu-id="f5348-130">**recurso** : la dirección URL del recurso de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f5348-130">**resource** — the resource URL for the app.</span></span>
>
>[!NOTE]
>
> * <span data-ttu-id="f5348-131">El bot requiere permisos delegados por aplicación y no por el usuario porque la instalación es para otros.</span><span class="sxs-lookup"><span data-stu-id="f5348-131">Your bot requires application and not user delegated permissions because the installation is for others.</span></span>
>
> * <span data-ttu-id="f5348-132">Un administrador de inquilinos de Azure AD debe [conceder explícitamente permisos a una aplicación.](/graph/security-authorization#grant-permissions-to-an-application)</span><span class="sxs-lookup"><span data-stu-id="f5348-132">An Azure AD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="f5348-133">Después de conceder permisos a una aplicación, todos los miembros del inquilino de Azure AD obtienen los permisos concedidos.</span><span class="sxs-lookup"><span data-stu-id="f5348-133">After an application is granted permissions, all members of the Azure AD tenant gain the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="f5348-134">Habilitar la instalación proactiva de aplicaciones y mensajería</span><span class="sxs-lookup"><span data-stu-id="f5348-134">Enable proactive app installation and messaging</span></span>

> [!IMPORTANT]
><span data-ttu-id="f5348-135">Microsoft Graph solo puede instalar aplicaciones publicadas en la tienda de aplicaciones de su organización o en la tienda de Teams.</span><span class="sxs-lookup"><span data-stu-id="f5348-135">Microsoft Graph can only install apps published to your organization's app store or the Teams store.</span></span>

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="f5348-136">✔ Crear y publicar el bot de mensajería proactiva para Teams</span><span class="sxs-lookup"><span data-stu-id="f5348-136">✔ Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="f5348-137">Para empezar, necesita un [bot para Teams](../../bots/how-to/create-a-bot-for-teams.md) con capacidades de mensajería [proactivas](../../concepts/bots/bot-conversations/bots-conv-proactive.md) que se en la [tienda de aplicaciones de](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) su organización o en la tienda [de Teams.](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store)</span><span class="sxs-lookup"><span data-stu-id="f5348-137">To get started, you need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities that's in your [organization's app store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) or the [Teams store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).</span></span>

>[!TIP]
> <span data-ttu-id="f5348-138">La plantilla [**de aplicación Communicator empresa**](../..//samples/app-templates.md#company-communicator) lista para la producción permite la difusión de mensajes y es una buena base para crear su aplicación de bot proactiva.</span><span class="sxs-lookup"><span data-stu-id="f5348-138">The production-ready [**Company Communicator**](../..//samples/app-templates.md#company-communicator) app template permits broadcast messaging and is a good foundation for building your proactive bot application.</span></span>

### <a name="-get-the-teamsappid-for-your-app"></a><span data-ttu-id="f5348-139">✔ Obtener la `teamsAppId` para la aplicación</span><span class="sxs-lookup"><span data-stu-id="f5348-139">✔ Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="f5348-140">**1.** Necesita los `teamsAppId` siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="f5348-140">**1.** You need the `teamsAppId` for the next steps.</span></span>

<span data-ttu-id="f5348-141">Se `teamsAppId` puede recuperar del catálogo de aplicaciones de su organización:</span><span class="sxs-lookup"><span data-stu-id="f5348-141">The `teamsAppId` can be retrieved from your organization's app catalog:</span></span>

<span data-ttu-id="f5348-142">**Referencia de página de Microsoft Graph:** [tipo de recurso teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="f5348-142">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span></span>

<span data-ttu-id="f5348-143">**Solicitud HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="f5348-143">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

<span data-ttu-id="f5348-144">La solicitud debe devolver un `teamsApp` objeto.</span><span class="sxs-lookup"><span data-stu-id="f5348-144">The request must return a `teamsApp` object.</span></span> <span data-ttu-id="f5348-145">El objeto devuelto `id` es el identificador de aplicación generado por catálogo de la aplicación y es diferente del identificador que proporcionó en el manifiesto de la aplicación Teams:</span><span class="sxs-lookup"><span data-stu-id="f5348-145">The returned object `id` is the app's catalog generated app ID and is different from the ID that you provided in your Teams app manifest:</span></span>

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

<span data-ttu-id="f5348-146">**2.**  Si la aplicación ya se ha cargado o cargado lateralmente para un usuario en el ámbito personal, puede recuperar lo `teamsAppId` siguiente:</span><span class="sxs-lookup"><span data-stu-id="f5348-146">**2.**  If your app has already been uploaded or sideloaded for a user in the personal scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="f5348-147">**Referencia de página de Microsoft Graph:** [lista de aplicaciones instaladas para el usuario](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="f5348-147">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="f5348-148">**Solicitud HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="f5348-148">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

<span data-ttu-id="f5348-149">**3.** Si la aplicación se ha cargado o descargado lateralmente para un canal en el ámbito del equipo, puede recuperar lo `teamsAppId` siguiente:</span><span class="sxs-lookup"><span data-stu-id="f5348-149">**3.** If your app has been uploaded or sideloaded for a channel in the team scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="f5348-150">**Referencia de página de Microsoft Graph:** [lista de aplicaciones en equipo](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="f5348-150">**Microsoft Graph page reference:** [List apps in team](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="f5348-151">**Solicitud HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="f5348-151">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> <span data-ttu-id="f5348-152">Para restringir la lista de resultados, puede filtrar en cualquiera de los campos de [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) objeto.</span><span class="sxs-lookup"><span data-stu-id="f5348-152">To narrow the list of results, you can filter on any of the fields of [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) object.</span></span>

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="f5348-153">✔ Determinar si el bot está instalado actualmente para un destinatario de mensaje</span><span class="sxs-lookup"><span data-stu-id="f5348-153">✔ Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="f5348-154">**Referencia de página de Microsoft Graph:** [lista de aplicaciones instaladas para el usuario](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="f5348-154">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="f5348-155">**Solicitud HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="f5348-155">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="f5348-156">Esta solicitud devuelve una matriz vacía si la aplicación no está instalada y una matriz con un único [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) objeto si la aplicación está instalada.</span><span class="sxs-lookup"><span data-stu-id="f5348-156">This request returns an empty array if the app is not installed and an array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) object if the app is installed.</span></span>

### <a name="-install-your-app"></a><span data-ttu-id="f5348-157">✔ Instalar la aplicación</span><span class="sxs-lookup"><span data-stu-id="f5348-157">✔ Install your app</span></span>

<span data-ttu-id="f5348-158">**Referencia de página de Microsoft Graph:** [instalar la aplicación para el usuario](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="f5348-158">**Microsoft Graph page reference:** [Install app for user](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="f5348-159">**Solicitud HTTP POST:**</span><span class="sxs-lookup"><span data-stu-id="f5348-159">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="f5348-160">Si el usuario tiene Microsoft Teams en ejecución, la instalación de la aplicación se ve inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="f5348-160">If the user has Microsoft Teams running, app installation is seen immediately.</span></span> <span data-ttu-id="f5348-161">Es posible que sea necesario reiniciar para ver la aplicación instalada.</span><span class="sxs-lookup"><span data-stu-id="f5348-161">A restart may be required to view the installed app.</span></span>

### <a name="-retrieve-the-conversation-chatid"></a><span data-ttu-id="f5348-162">✔ Recuperar el **chat de conversaciónId**</span><span class="sxs-lookup"><span data-stu-id="f5348-162">✔ Retrieve the conversation **chatId**</span></span>

<span data-ttu-id="f5348-163">Cuando la aplicación está instalada para el usuario, el bot recibe una `conversationUpdate` [notificación de evento](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) que contiene la información necesaria para enviar el mensaje proactivo.</span><span class="sxs-lookup"><span data-stu-id="f5348-163">When your app is installed for the user, the bot receives a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that contains the necessary information to send the proactive message.</span></span>

<span data-ttu-id="f5348-164">También `chatId` se puede recuperar de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="f5348-164">The `chatId` can also be retrieved as follows:</span></span>

<span data-ttu-id="f5348-165">**Referencia de página de Microsoft Graph:** [obtener chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="f5348-165">**Microsoft Graph page reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="f5348-166">**1.** Debes necesitar la `{teamsAppInstallationId}` aplicación.</span><span class="sxs-lookup"><span data-stu-id="f5348-166">**1.** You must need your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="f5348-167">Si no lo tiene, utilice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f5348-167">If you don't have it, use the following:</span></span>

<span data-ttu-id="f5348-168">**Solicitud HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="f5348-168">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="f5348-169">La propiedad **id** de la respuesta es el `teamsAppInstallationId` archivo .</span><span class="sxs-lookup"><span data-stu-id="f5348-169">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

<span data-ttu-id="f5348-170">**2.** Haga la siguiente solicitud para `chatId` obtener:</span><span class="sxs-lookup"><span data-stu-id="f5348-170">**2.** Make the following request to fetch the `chatId`:</span></span>

<span data-ttu-id="f5348-171">**Solicitud HTTP GET** (permiso — `TeamsAppInstallation.ReadWriteSelfForUser.All` ):</span><span class="sxs-lookup"><span data-stu-id="f5348-171">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

<span data-ttu-id="f5348-172">La propiedad **id** de la respuesta es el `chatId` archivo .</span><span class="sxs-lookup"><span data-stu-id="f5348-172">The **id** property of the response is the `chatId`.</span></span>

<span data-ttu-id="f5348-173">También puede recuperar la `chatId` siguiente solicitud, pero requiere el permiso más `Chat.Read.All` amplio:</span><span class="sxs-lookup"><span data-stu-id="f5348-173">You can also retrieve the `chatId` with the following request but it requires the broader `Chat.Read.All` permission:</span></span>

<span data-ttu-id="f5348-174">**Solicitud HTTP GET** (permiso — `Chat.Read.All` ):</span><span class="sxs-lookup"><span data-stu-id="f5348-174">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a><span data-ttu-id="f5348-175">✔ Enviar mensajes proactivos</span><span class="sxs-lookup"><span data-stu-id="f5348-175">✔ Send proactive messages</span></span>

<span data-ttu-id="f5348-176">El bot puede [enviar mensajes proactivos](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) después de que se haya agregado el bot para un usuario o un equipo y haya recibido toda la información del usuario.</span><span class="sxs-lookup"><span data-stu-id="f5348-176">Your bot can [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) after the bot has been added for a user or a team and has received all the user information.</span></span>

## <a name="see-also"></a><span data-ttu-id="f5348-177">Vea también</span><span class="sxs-lookup"><span data-stu-id="f5348-177">See also</span></span>

* [<span data-ttu-id="f5348-178">**Administrar directivas de configuración de aplicaciones en Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="f5348-178">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [<span data-ttu-id="f5348-179">Enviar notificaciones proactivas a los usuarios SDK v4</span><span class="sxs-lookup"><span data-stu-id="f5348-179">Send proactive notifications to users SDK v4</span></span>](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

## <a name="view-additional-code-samples"></a><span data-ttu-id="f5348-180">Ver ejemplos de código adicionales</span><span class="sxs-lookup"><span data-stu-id="f5348-180">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="f5348-181">**Teams ejemplos proactivos de código de mensajería**</span><span class="sxs-lookup"><span data-stu-id="f5348-181">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
---
title: Use Microsoft Graph para autorizar la instalación proactiva de bots y la mensajería en Teams
description: Describe la mensajería proactiva en Teams y cómo implementar.
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: instalación proactiva de chat de mensajería de teams Graph
ms.openlocfilehash: 0ece7d3ec3a9e00774ff2f529f7c38bc1932469d
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069092"
---
# <a name="proactive-installation-of-apps-using-graph-api-to-send-messages"></a><span data-ttu-id="e7cee-104">Instalación proactiva de aplicaciones que usan Graph API para enviar mensajes</span><span class="sxs-lookup"><span data-stu-id="e7cee-104">Proactive installation of apps using Graph API to send messages</span></span>

>[!IMPORTANT]
> <span data-ttu-id="e7cee-105">Microsoft Graph y Microsoft Teams vistas previas públicas están disponibles para obtener acceso anticipado y comentarios.</span><span class="sxs-lookup"><span data-stu-id="e7cee-105">Microsoft Graph and Microsoft Teams public previews are available for early access and feedback.</span></span> <span data-ttu-id="e7cee-106">Aunque esta versión se ha sometido a pruebas exhaustivas, no está diseñada para su uso en producción.</span><span class="sxs-lookup"><span data-stu-id="e7cee-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="e7cee-107">Mensajería proactiva en Teams</span><span class="sxs-lookup"><span data-stu-id="e7cee-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="e7cee-108">Los bots inician mensajes proactivos para iniciar conversaciones con un usuario.</span><span class="sxs-lookup"><span data-stu-id="e7cee-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="e7cee-109">Sirven para muchos propósitos, como enviar mensajes de bienvenida, realizar encuestas o sondeos y difundir notificaciones en toda la organización.</span><span class="sxs-lookup"><span data-stu-id="e7cee-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span> <span data-ttu-id="e7cee-110">Los mensajes proactivos Teams pueden entregarse como conversaciones **ad-hoc** o **basadas en cuadros de** diálogo:</span><span class="sxs-lookup"><span data-stu-id="e7cee-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="e7cee-111">Tipo de mensaje</span><span class="sxs-lookup"><span data-stu-id="e7cee-111">Message Type</span></span> | <span data-ttu-id="e7cee-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="e7cee-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="e7cee-113">Mensaje proactivo ad hoc</span><span class="sxs-lookup"><span data-stu-id="e7cee-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="e7cee-114">El bot interje un mensaje sin interrumpir el flujo de conversación.</span><span class="sxs-lookup"><span data-stu-id="e7cee-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="e7cee-115">Mensaje proactivo basado en cuadros de diálogo</span><span class="sxs-lookup"><span data-stu-id="e7cee-115">Dialog-based proactive message</span></span> | <span data-ttu-id="e7cee-116">El bot crea un nuevo subproceso de diálogo, toma el control de una conversación, entrega el mensaje proactivo, se cierra y devuelve el control al cuadro de diálogo anterior.</span><span class="sxs-lookup"><span data-stu-id="e7cee-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="e7cee-117">Instalación proactiva de aplicaciones en Teams</span><span class="sxs-lookup"><span data-stu-id="e7cee-117">Proactive app installation in Teams</span></span>

<span data-ttu-id="e7cee-118">Para que el bot pueda enviar un mensaje de forma proactiva a un usuario, debe instalarse como una aplicación personal o en un equipo en el que el usuario sea miembro.</span><span class="sxs-lookup"><span data-stu-id="e7cee-118">Before your bot can proactively message a user, it must be installed either as a personal app or in a team where the user is a member.</span></span> <span data-ttu-id="e7cee-119">En ocasiones, debes enviar mensajes de forma proactiva a los usuarios que no han instalado ni interactuado previamente con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e7cee-119">At times, you need to proactively message users that have not installed or previously interacted with your app.</span></span> <span data-ttu-id="e7cee-120">Por ejemplo, la necesidad de enviar información vital a todos los usuarios de la organización.</span><span class="sxs-lookup"><span data-stu-id="e7cee-120">For example, the need to message vital information to everyone in your organization.</span></span> <span data-ttu-id="e7cee-121">Para estos escenarios, puede usar la API de Microsoft Graph para instalar proactivamente el bot para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="e7cee-121">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="e7cee-122">Permisos</span><span class="sxs-lookup"><span data-stu-id="e7cee-122">Permissions</span></span>

<span data-ttu-id="e7cee-123">Los permisos de tipo de recurso [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) de Microsoft Graph le ayudan a administrar el ciclo de vida de instalación de la aplicación para todos los ámbitos de usuario (personal) o de equipo (canal) de la plataforma Microsoft Teams usuario:</span><span class="sxs-lookup"><span data-stu-id="e7cee-123">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) permissions helps you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="e7cee-124">Permisos de aplicación</span><span class="sxs-lookup"><span data-stu-id="e7cee-124">Application permission</span></span> | <span data-ttu-id="e7cee-125">Descripción</span><span class="sxs-lookup"><span data-stu-id="e7cee-125">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="e7cee-126">Permite que Teams aplicación lea, instale, actualice y desinstale a sí misma para cualquier **usuario,** sin iniciar sesión o usar previamente.</span><span class="sxs-lookup"><span data-stu-id="e7cee-126">Allows a Teams app to read, install, upgrade, and uninstall itself for any **user**, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="e7cee-127">Permite que Teams aplicación se lea, instale, actualice y se desinstale en cualquier **equipo,** sin necesidad de iniciar sesión o usar previamente.</span><span class="sxs-lookup"><span data-stu-id="e7cee-127">Allows a Teams app to read, install, upgrade, and uninstall itself in any **team**, without prior sign in or use.</span></span>|

<span data-ttu-id="e7cee-128">Para usar estos permisos, debe agregar una clave [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) al manifiesto de la aplicación con los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="e7cee-128">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>
> [!div class="checklist"]
> [!div class="checklist"]
>
> * <span data-ttu-id="e7cee-129">**id:** el identificador de la aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7cee-129">**id** — your Azure AD app ID.</span></span>
> * <span data-ttu-id="e7cee-130">**recurso:** la dirección URL del recurso para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e7cee-130">**resource** — the resource URL for the app.</span></span>
>
>[!NOTE]
>
> * <span data-ttu-id="e7cee-131">El bot requiere permisos delegados de aplicación y no de usuario porque la instalación es para otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="e7cee-131">Your bot requires application and not user delegated permissions because the installation is for others.</span></span>
>
> * <span data-ttu-id="e7cee-132">Un administrador de inquilinos de Azure AD debe [conceder explícitamente permisos a una aplicación](/graph/security-authorization#grant-permissions-to-an-application).</span><span class="sxs-lookup"><span data-stu-id="e7cee-132">An Azure AD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="e7cee-133">Después de conceder permisos a una aplicación, todos los miembros del inquilino de Azure AD obtienen los permisos concedidos.</span><span class="sxs-lookup"><span data-stu-id="e7cee-133">After an application is granted permissions, all members of the Azure AD tenant gain the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="e7cee-134">Habilitar la instalación proactiva de aplicaciones y la mensajería</span><span class="sxs-lookup"><span data-stu-id="e7cee-134">Enable proactive app installation and messaging</span></span>

> [!IMPORTANT]
><span data-ttu-id="e7cee-135">Microsoft Graph solo puede instalar aplicaciones publicadas en la tienda de aplicaciones de su organización o en la Teams de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e7cee-135">Microsoft Graph can only install apps published to your organization's app store or the Teams store.</span></span>

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="e7cee-136">✔ Crear y publicar el bot de mensajería proactiva para Teams</span><span class="sxs-lookup"><span data-stu-id="e7cee-136">✔ Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="e7cee-137">Para empezar, necesita un [bot](../../bots/how-to/create-a-bot-for-teams.md) para Teams [](../../concepts/bots/bot-conversations/bots-conv-proactive.md) con capacidades de [](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) mensajería proactiva que se encuentra en la tienda de aplicaciones de su organización o en la [Teams de almacenamiento](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).</span><span class="sxs-lookup"><span data-stu-id="e7cee-137">To get started, you need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities that's in your [organization's app store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) or the [Teams store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).</span></span>

>[!TIP]
> <span data-ttu-id="e7cee-138">La plantilla de aplicación [**de Communicator**](../..//samples/app-templates.md#company-communicator) lista para producción permite la mensajería de difusión y es una buena base para crear la aplicación de bot proactiva.</span><span class="sxs-lookup"><span data-stu-id="e7cee-138">The production-ready [**Company Communicator**](../..//samples/app-templates.md#company-communicator) app template permits broadcast messaging and is a good foundation for building your proactive bot application.</span></span>

### <a name="-get-the-teamsappid-for-your-app"></a><span data-ttu-id="e7cee-139">✔ Obtener la `teamsAppId` para la aplicación</span><span class="sxs-lookup"><span data-stu-id="e7cee-139">✔ Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="e7cee-140">**1.** Necesita los `teamsAppId` pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="e7cee-140">**1.** You need the `teamsAppId` for the next steps.</span></span>

<span data-ttu-id="e7cee-141">Se puede recuperar desde el catálogo de aplicaciones de `teamsAppId` la organización:</span><span class="sxs-lookup"><span data-stu-id="e7cee-141">The `teamsAppId` can be retrieved from your organization's app catalog:</span></span>

<span data-ttu-id="e7cee-142">**Referencia Graph página de Microsoft:** [tipo de recurso teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="e7cee-142">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span></span>

<span data-ttu-id="e7cee-143">**Solicitud HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="e7cee-143">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

<span data-ttu-id="e7cee-144">La solicitud debe devolver un `teamsApp` objeto.</span><span class="sxs-lookup"><span data-stu-id="e7cee-144">The request must return a `teamsApp` object.</span></span> <span data-ttu-id="e7cee-145">El objeto devuelto es el identificador de aplicación generado por el catálogo de la aplicación y es diferente del identificador que proporcionaste en el manifiesto Teams `id` aplicación:</span><span class="sxs-lookup"><span data-stu-id="e7cee-145">The returned object `id` is the app's catalog generated app ID and is different from the ID that you provided in your Teams app manifest:</span></span>

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

<span data-ttu-id="e7cee-146">**2.**  Si la aplicación ya se ha cargado o se ha cargado localmente para un usuario en el ámbito personal, puede recuperar lo `teamsAppId` siguiente:</span><span class="sxs-lookup"><span data-stu-id="e7cee-146">**2.**  If your app has already been uploaded or sideloaded for a user in the personal scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="e7cee-147">**Referencia Graph página de Microsoft: Enumerar** [las aplicaciones instaladas para el usuario](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="e7cee-147">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="e7cee-148">**Solicitud HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="e7cee-148">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

<span data-ttu-id="e7cee-149">**3.** Si la aplicación se ha cargado o se ha cargado localmente para un canal en el ámbito de grupo, puede recuperar lo `teamsAppId` siguiente:</span><span class="sxs-lookup"><span data-stu-id="e7cee-149">**3.** If your app has been uploaded or sideloaded for a channel in the team scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="e7cee-150">**Referencia Graph página de Microsoft: Enumerar** [aplicaciones en equipo](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="e7cee-150">**Microsoft Graph page reference:** [List apps in team](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="e7cee-151">**Solicitud HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="e7cee-151">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> <span data-ttu-id="e7cee-152">Para restringir la lista de resultados, puede filtrar en cualquiera de los campos del [**objeto teamsApp.**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="e7cee-152">To narrow the list of results, you can filter on any of the fields of [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) object.</span></span>

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="e7cee-153">✔ Determine si el bot está instalado actualmente para un destinatario de mensaje</span><span class="sxs-lookup"><span data-stu-id="e7cee-153">✔ Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="e7cee-154">**Referencia Graph página de Microsoft: Enumerar** [las aplicaciones instaladas para el usuario](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="e7cee-154">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="e7cee-155">**Solicitud HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="e7cee-155">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="e7cee-156">Esta solicitud devuelve una matriz vacía si la aplicación no está instalada y una matriz con un único [objeto teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) si la aplicación está instalada.</span><span class="sxs-lookup"><span data-stu-id="e7cee-156">This request returns an empty array if the app is not installed and an array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) object if the app is installed.</span></span>

### <a name="-install-your-app"></a><span data-ttu-id="e7cee-157">✔ instalar la aplicación</span><span class="sxs-lookup"><span data-stu-id="e7cee-157">✔ Install your app</span></span>

<span data-ttu-id="e7cee-158">**Referencia Graph página de Microsoft:** [Instalar aplicación para el usuario](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="e7cee-158">**Microsoft Graph page reference:** [Install app for user](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="e7cee-159">**Solicitud HTTP POST:**</span><span class="sxs-lookup"><span data-stu-id="e7cee-159">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="e7cee-160">Si el usuario tiene Microsoft Teams, la instalación de la aplicación se ve inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="e7cee-160">If the user has Microsoft Teams running, app installation is seen immediately.</span></span> <span data-ttu-id="e7cee-161">Es posible que sea necesario reiniciar para ver la aplicación instalada.</span><span class="sxs-lookup"><span data-stu-id="e7cee-161">A restart may be required to view the installed app.</span></span>

### <a name="-retrieve-the-conversation-chatid"></a><span data-ttu-id="e7cee-162">✔ recuperar el **chatId de conversación**</span><span class="sxs-lookup"><span data-stu-id="e7cee-162">✔ Retrieve the conversation **chatId**</span></span>

<span data-ttu-id="e7cee-163">Cuando la aplicación está instalada para el usuario, el bot recibe una notificación de evento que contiene la `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) información necesaria para enviar el mensaje proactivo.</span><span class="sxs-lookup"><span data-stu-id="e7cee-163">When your app is installed for the user, the bot receives a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that contains the necessary information to send the proactive message.</span></span>

<span data-ttu-id="e7cee-164">También `chatId` se puede recuperar de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="e7cee-164">The `chatId` can also be retrieved as follows:</span></span>

<span data-ttu-id="e7cee-165">**Referencia Graph página de Microsoft:** [Obtener chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="e7cee-165">**Microsoft Graph page reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="e7cee-166">**1.** Debe necesitar el `{teamsAppInstallationId}` archivo .</span><span class="sxs-lookup"><span data-stu-id="e7cee-166">**1.** You must need your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="e7cee-167">Si no lo tiene, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e7cee-167">If you don't have it, use the following:</span></span>

<span data-ttu-id="e7cee-168">**Solicitud HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="e7cee-168">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="e7cee-169">La **propiedad id** de la respuesta es `teamsAppInstallationId` .</span><span class="sxs-lookup"><span data-stu-id="e7cee-169">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

<span data-ttu-id="e7cee-170">**2.** Realice la siguiente solicitud para capturar `chatId` :</span><span class="sxs-lookup"><span data-stu-id="e7cee-170">**2.** Make the following request to fetch the `chatId`:</span></span>

<span data-ttu-id="e7cee-171">**Solicitud HTTP GET** (permiso `TeamsAppInstallation.ReadWriteSelfForUser.All` — ):</span><span class="sxs-lookup"><span data-stu-id="e7cee-171">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

<span data-ttu-id="e7cee-172">La **propiedad id** de la respuesta es `chatId` .</span><span class="sxs-lookup"><span data-stu-id="e7cee-172">The **id** property of the response is the `chatId`.</span></span>

<span data-ttu-id="e7cee-173">También puede recuperar la `chatId` solicitud con la siguiente solicitud, pero requiere el permiso más `Chat.Read.All` amplio:</span><span class="sxs-lookup"><span data-stu-id="e7cee-173">You can also retrieve the `chatId` with the following request but it requires the broader `Chat.Read.All` permission:</span></span>

<span data-ttu-id="e7cee-174">**Solicitud HTTP GET** (permiso `Chat.Read.All` — ):</span><span class="sxs-lookup"><span data-stu-id="e7cee-174">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a><span data-ttu-id="e7cee-175">✔ enviar mensajes proactivos</span><span class="sxs-lookup"><span data-stu-id="e7cee-175">✔ Send proactive messages</span></span>

<span data-ttu-id="e7cee-176">El bot puede [enviar mensajes proactivos](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) después de que el bot se haya agregado para un usuario o un equipo y haya recibido toda la información del usuario.</span><span class="sxs-lookup"><span data-stu-id="e7cee-176">Your bot can [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) after the bot has been added for a user or a team and has received all the user information.</span></span>

## <a name="see-also"></a><span data-ttu-id="e7cee-177">Consulte también</span><span class="sxs-lookup"><span data-stu-id="e7cee-177">See also</span></span>

* [<span data-ttu-id="e7cee-178">**Administrar directivas de configuración de aplicaciones en Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="e7cee-178">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [<span data-ttu-id="e7cee-179">Enviar notificaciones proactivas a usuarios SDK v4</span><span class="sxs-lookup"><span data-stu-id="e7cee-179">Send proactive notifications to users SDK v4</span></span>](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

## <a name="view-additional-code-samples"></a><span data-ttu-id="e7cee-180">Ver ejemplos de código adicionales</span><span class="sxs-lookup"><span data-stu-id="e7cee-180">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e7cee-181">**Teams de código de mensajería proactiva**</span><span class="sxs-lookup"><span data-stu-id="e7cee-181">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)

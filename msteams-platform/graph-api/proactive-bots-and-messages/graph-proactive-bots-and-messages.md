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
# <a name="proactive-installation-of-apps-using-graph-api-and-send-messages"></a><span data-ttu-id="ef83a-104">Instalación proactiva de aplicaciones usando la API de Graph y el envío de mensajes</span><span class="sxs-lookup"><span data-stu-id="ef83a-104">Proactive installation of apps using Graph API and send messages</span></span>

>[!IMPORTANT]
> <span data-ttu-id="ef83a-105">Microsoft Graph y Microsoft Teams vistas previas públicas están disponibles para obtener acceso anticipado y comentarios.</span><span class="sxs-lookup"><span data-stu-id="ef83a-105">Microsoft Graph and Microsoft Teams public previews are available for early access and feedback.</span></span> <span data-ttu-id="ef83a-106">Aunque esta versión se ha sometido a pruebas exhaustivas, no está diseñada para su uso en producción.</span><span class="sxs-lookup"><span data-stu-id="ef83a-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="ef83a-107">Mensajería proactiva en Teams</span><span class="sxs-lookup"><span data-stu-id="ef83a-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="ef83a-108">Los bots inician mensajes proactivos para iniciar conversaciones con un usuario.</span><span class="sxs-lookup"><span data-stu-id="ef83a-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="ef83a-109">Sirven para muchos propósitos, como enviar mensajes de bienvenida, realizar encuestas o sondeos y difundir notificaciones en toda la organización.</span><span class="sxs-lookup"><span data-stu-id="ef83a-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span> <span data-ttu-id="ef83a-110">Los mensajes proactivos Teams pueden entregarse como conversaciones **ad-hoc** o **basadas en cuadros de** diálogo:</span><span class="sxs-lookup"><span data-stu-id="ef83a-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="ef83a-111">Tipo de mensaje</span><span class="sxs-lookup"><span data-stu-id="ef83a-111">Message Type</span></span> | <span data-ttu-id="ef83a-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="ef83a-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="ef83a-113">Mensaje proactivo ad hoc</span><span class="sxs-lookup"><span data-stu-id="ef83a-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="ef83a-114">El bot interje un mensaje sin interrumpir el flujo de conversación.</span><span class="sxs-lookup"><span data-stu-id="ef83a-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="ef83a-115">Mensaje proactivo basado en cuadros de diálogo</span><span class="sxs-lookup"><span data-stu-id="ef83a-115">Dialog-based proactive message</span></span> | <span data-ttu-id="ef83a-116">El bot crea un nuevo subproceso de diálogo, toma el control de una conversación, entrega el mensaje proactivo, se cierra y devuelve el control al cuadro de diálogo anterior.</span><span class="sxs-lookup"><span data-stu-id="ef83a-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

<span data-ttu-id="ef83a-117">Vea Enviar [notificaciones proactivas a los usuarios SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="ef83a-117">See, [Send proactive notifications to users SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true).</span></span>

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="ef83a-118">Instalación proactiva de aplicaciones en Teams</span><span class="sxs-lookup"><span data-stu-id="ef83a-118">Proactive app installation in Teams</span></span>

<span data-ttu-id="ef83a-119">Para que el bot pueda enviar un mensaje de forma proactiva a un usuario, debe instalarse como una aplicación personal o en un equipo en el que el usuario sea miembro.</span><span class="sxs-lookup"><span data-stu-id="ef83a-119">Before your bot can proactively message a user, it must be installed either as a personal app or in a team where the user is a member.</span></span> <span data-ttu-id="ef83a-120">En ocasiones, debes enviar mensajes de forma proactiva a los usuarios que no han instalado ni interactuado previamente con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ef83a-120">At times, you need to proactively message users that have not installed or previously interacted with your app.</span></span> <span data-ttu-id="ef83a-121">Por ejemplo, la necesidad de enviar información vital a todos los usuarios de la organización.</span><span class="sxs-lookup"><span data-stu-id="ef83a-121">For example, the need to message vital information to everyone in your organization.</span></span> <span data-ttu-id="ef83a-122">Para estos escenarios, puede usar la API de Microsoft Graph para instalar proactivamente el bot para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="ef83a-122">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="ef83a-123">Permisos</span><span class="sxs-lookup"><span data-stu-id="ef83a-123">Permissions</span></span>

<span data-ttu-id="ef83a-124">Los permisos de tipo de recurso [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) de Microsoft Graph le ayudan a administrar el ciclo de vida de instalación de la aplicación para todos los ámbitos de usuario (personal) o de equipo (canal) de la plataforma Microsoft Teams usuario:</span><span class="sxs-lookup"><span data-stu-id="ef83a-124">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) permissions helps you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="ef83a-125">Permisos de aplicación</span><span class="sxs-lookup"><span data-stu-id="ef83a-125">Application permission</span></span> | <span data-ttu-id="ef83a-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="ef83a-126">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="ef83a-127">Permite que Teams aplicación lea, instale, actualice y desinstale a sí misma para cualquier **usuario,** sin iniciar sesión o usar previamente.</span><span class="sxs-lookup"><span data-stu-id="ef83a-127">Allows a Teams app to read, install, upgrade, and uninstall itself for any **user**, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="ef83a-128">Permite que Teams aplicación se lea, instale, actualice y se desinstale en cualquier **equipo,** sin necesidad de iniciar sesión o usar previamente.</span><span class="sxs-lookup"><span data-stu-id="ef83a-128">Allows a Teams app to read, install, upgrade, and uninstall itself in any **team**, without prior sign in or use.</span></span>|

<span data-ttu-id="ef83a-129">Para usar estos permisos, debe agregar una clave [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) al manifiesto de la aplicación con los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="ef83a-129">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>
> [!div class="checklist"]
> [!div class="checklist"]
>
> * <span data-ttu-id="ef83a-130">**id:** el identificador de la aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef83a-130">**id** — your Azure AD app ID.</span></span>
> * <span data-ttu-id="ef83a-131">**recurso:** la dirección URL del recurso para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ef83a-131">**resource** — the resource URL for the app.</span></span>
>
>[!NOTE]
>
> * <span data-ttu-id="ef83a-132">El bot requiere permisos delegados de aplicación y no de usuario porque la instalación es para otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="ef83a-132">Your bot requires application and not user delegated permissions because the installation is for others.</span></span>
>
> * <span data-ttu-id="ef83a-133">Un administrador de inquilinos de Azure AD debe [conceder explícitamente permisos a una aplicación](/graph/security-authorization#grant-permissions-to-an-application).</span><span class="sxs-lookup"><span data-stu-id="ef83a-133">An Azure AD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="ef83a-134">Después de conceder permisos a una aplicación, todos los miembros del inquilino de Azure AD obtienen los permisos concedidos.</span><span class="sxs-lookup"><span data-stu-id="ef83a-134">After an application is granted permissions, all members of the Azure AD tenant gain the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="ef83a-135">Habilitar la instalación proactiva de aplicaciones y la mensajería</span><span class="sxs-lookup"><span data-stu-id="ef83a-135">Enable proactive app installation and messaging</span></span>

> [!IMPORTANT]
><span data-ttu-id="ef83a-136">Microsoft Graph solo puede instalar aplicaciones publicadas en la tienda de aplicaciones de su organización o en la Teams de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ef83a-136">Microsoft Graph can only install apps published to your organization's app store or the Teams store.</span></span>

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="ef83a-137">✔ Crear y publicar el bot de mensajería proactiva para Teams</span><span class="sxs-lookup"><span data-stu-id="ef83a-137">✔ Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="ef83a-138">Para empezar, necesita un [bot](../../bots/how-to/create-a-bot-for-teams.md) para Teams [](../../concepts/bots/bot-conversations/bots-conv-proactive.md) con capacidades de [](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) mensajería proactiva que se encuentra en la tienda de aplicaciones de su organización o en la [Teams de almacenamiento](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).</span><span class="sxs-lookup"><span data-stu-id="ef83a-138">To get started, you need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities that's in your [organization's app store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) or the [Teams store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).</span></span>

>[!TIP]
> <span data-ttu-id="ef83a-139">La plantilla de aplicación [**de Communicator**](../..//samples/app-templates.md#company-communicator) lista para producción permite la mensajería de difusión y es una buena base para crear la aplicación de bot proactiva.</span><span class="sxs-lookup"><span data-stu-id="ef83a-139">The production-ready [**Company Communicator**](../..//samples/app-templates.md#company-communicator) app template permits broadcast messaging and is a good foundation for building your proactive bot application.</span></span>

### <a name="-get-the-teamsappid-for-your-app"></a><span data-ttu-id="ef83a-140">✔ Obtener la `teamsAppId` para la aplicación</span><span class="sxs-lookup"><span data-stu-id="ef83a-140">✔ Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="ef83a-141">**1.** Necesita los `teamsAppId` pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="ef83a-141">**1.** You need the `teamsAppId` for the next steps.</span></span>

<span data-ttu-id="ef83a-142">Se puede recuperar desde el catálogo de aplicaciones de `teamsAppId` la organización:</span><span class="sxs-lookup"><span data-stu-id="ef83a-142">The `teamsAppId` can be retrieved from your organization's app catalog:</span></span>

<span data-ttu-id="ef83a-143">**Referencia Graph página de Microsoft:** [tipo de recurso teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="ef83a-143">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span></span>

<span data-ttu-id="ef83a-144">**Solicitud HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="ef83a-144">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

<span data-ttu-id="ef83a-145">La solicitud debe devolver un `teamsApp` objeto.</span><span class="sxs-lookup"><span data-stu-id="ef83a-145">The request must return a `teamsApp` object.</span></span> <span data-ttu-id="ef83a-146">El objeto devuelto es el identificador de aplicación generado por el catálogo de la aplicación y es diferente del identificador que proporcionaste en el manifiesto Teams `id` aplicación:</span><span class="sxs-lookup"><span data-stu-id="ef83a-146">The returned object `id` is the app's catalog generated app ID and is different from the ID that you provided in your Teams app manifest:</span></span>

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

<span data-ttu-id="ef83a-147">**2.**  Si la aplicación ya se ha cargado o se ha cargado localmente para un usuario en el ámbito personal, puede recuperar lo `teamsAppId` siguiente:</span><span class="sxs-lookup"><span data-stu-id="ef83a-147">**2.**  If your app has already been uploaded or sideloaded for a user in the personal scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="ef83a-148">**Referencia Graph página de Microsoft: Enumerar** [las aplicaciones instaladas para el usuario](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="ef83a-148">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="ef83a-149">**Solicitud HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="ef83a-149">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

<span data-ttu-id="ef83a-150">**3.** Si la aplicación se ha cargado o se ha cargado localmente para un canal en el ámbito de grupo, puede recuperar lo `teamsAppId` siguiente:</span><span class="sxs-lookup"><span data-stu-id="ef83a-150">**3.** If your app has been uploaded or sideloaded for a channel in the team scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="ef83a-151">**Referencia Graph página de Microsoft: Enumerar** [aplicaciones en equipo](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="ef83a-151">**Microsoft Graph page reference:** [List apps in team](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="ef83a-152">**Solicitud HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="ef83a-152">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> <span data-ttu-id="ef83a-153">Para restringir la lista de resultados, puede filtrar en cualquiera de los campos del [**objeto teamsApp.**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="ef83a-153">To narrow the list of results, you can filter on any of the fields of [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) object.</span></span>

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="ef83a-154">✔ Determine si el bot está instalado actualmente para un destinatario de mensaje</span><span class="sxs-lookup"><span data-stu-id="ef83a-154">✔ Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="ef83a-155">**Referencia Graph página de Microsoft: Enumerar** [las aplicaciones instaladas para el usuario](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="ef83a-155">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="ef83a-156">**Solicitud HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="ef83a-156">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="ef83a-157">Esta solicitud devuelve una matriz vacía si la aplicación no está instalada y una matriz con un único [objeto teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) si la aplicación está instalada.</span><span class="sxs-lookup"><span data-stu-id="ef83a-157">This request returns an empty array if the app is not installed and an array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) object if the app is installed.</span></span>

### <a name="-install-your-app"></a><span data-ttu-id="ef83a-158">✔ instalar la aplicación</span><span class="sxs-lookup"><span data-stu-id="ef83a-158">✔ Install your app</span></span>

<span data-ttu-id="ef83a-159">**Referencia Graph página de Microsoft:** [Instalar aplicación para el usuario](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="ef83a-159">**Microsoft Graph page reference:** [Install app for user](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="ef83a-160">**Solicitud HTTP POST:**</span><span class="sxs-lookup"><span data-stu-id="ef83a-160">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="ef83a-161">Si el usuario tiene Microsoft Teams, la instalación de la aplicación se ve inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="ef83a-161">If the user has Microsoft Teams running, app installation is seen immediately.</span></span> <span data-ttu-id="ef83a-162">Es posible que sea necesario reiniciar para ver la aplicación instalada.</span><span class="sxs-lookup"><span data-stu-id="ef83a-162">A restart may be required to view the installed app.</span></span>

### <a name="-retrieve-the-conversation-chatid"></a><span data-ttu-id="ef83a-163">✔ recuperar el **chatId de conversación**</span><span class="sxs-lookup"><span data-stu-id="ef83a-163">✔ Retrieve the conversation **chatId**</span></span>

<span data-ttu-id="ef83a-164">Cuando la aplicación está instalada para el usuario, el bot recibe una notificación de evento que contiene la `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) información necesaria para enviar el mensaje proactivo.</span><span class="sxs-lookup"><span data-stu-id="ef83a-164">When your app is installed for the user, the bot receives a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that contains the necessary information to send the proactive message.</span></span>

<span data-ttu-id="ef83a-165">También `chatId` se puede recuperar de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="ef83a-165">The `chatId` can also be retrieved as follows:</span></span>

<span data-ttu-id="ef83a-166">**Referencia Graph página de Microsoft:** [Obtener chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="ef83a-166">**Microsoft Graph page reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="ef83a-167">**1.** Debe necesitar el `{teamsAppInstallationId}` archivo .</span><span class="sxs-lookup"><span data-stu-id="ef83a-167">**1.** You must need your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="ef83a-168">Si no lo tiene, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ef83a-168">If you don't have it, use the following:</span></span>

<span data-ttu-id="ef83a-169">**Solicitud HTTP GET:**</span><span class="sxs-lookup"><span data-stu-id="ef83a-169">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="ef83a-170">La **propiedad id** de la respuesta es `teamsAppInstallationId` .</span><span class="sxs-lookup"><span data-stu-id="ef83a-170">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

<span data-ttu-id="ef83a-171">**2.** Realice la siguiente solicitud para capturar `chatId` :</span><span class="sxs-lookup"><span data-stu-id="ef83a-171">**2.** Make the following request to fetch the `chatId`:</span></span>

<span data-ttu-id="ef83a-172">**Solicitud HTTP GET** (permiso `TeamsAppInstallation.ReadWriteSelfForUser.All` — ):</span><span class="sxs-lookup"><span data-stu-id="ef83a-172">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

<span data-ttu-id="ef83a-173">La **propiedad id** de la respuesta es `chatId` .</span><span class="sxs-lookup"><span data-stu-id="ef83a-173">The **id** property of the response is the `chatId`.</span></span>

<span data-ttu-id="ef83a-174">También puede recuperar la `chatId` solicitud con la siguiente solicitud, pero requiere el permiso más `Chat.Read.All` amplio:</span><span class="sxs-lookup"><span data-stu-id="ef83a-174">You can also retrieve the `chatId` with the following request but it requires the broader `Chat.Read.All` permission:</span></span>

<span data-ttu-id="ef83a-175">**Solicitud HTTP GET** (permiso `Chat.Read.All` — ):</span><span class="sxs-lookup"><span data-stu-id="ef83a-175">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a><span data-ttu-id="ef83a-176">✔ enviar mensajes proactivos</span><span class="sxs-lookup"><span data-stu-id="ef83a-176">✔ Send proactive messages</span></span>

<span data-ttu-id="ef83a-177">El bot puede [enviar mensajes proactivos](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) después de que el bot se haya agregado para un usuario o un equipo y haya recibido toda la información del usuario.</span><span class="sxs-lookup"><span data-stu-id="ef83a-177">Your bot can [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) after the bot has been added for a user or a team and has received all the user information.</span></span>

## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="ef83a-178">Tema relacionado para Teams administradores</span><span class="sxs-lookup"><span data-stu-id="ef83a-178">Related topic for Teams administrators</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ef83a-179">**Administrar directivas de configuración de aplicación en Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="ef83a-179">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a><span data-ttu-id="ef83a-180">Ver ejemplos de código adicionales</span><span class="sxs-lookup"><span data-stu-id="ef83a-180">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ef83a-181">**Teams de código de mensajería proactiva**</span><span class="sxs-lookup"><span data-stu-id="ef83a-181">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>

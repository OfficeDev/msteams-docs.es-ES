---
title: Usar Microsoft Graph para habilitar la instalación y mensajería proactiva de robots en Microsoft Teams
description: Describe la mensajería proactiva en Microsoft Teams y cómo implementarla.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Gráfico de instalación de chat de mensajería proactiva de Teams
ms.openlocfilehash: ee1620c8fdcaeeecf0e8b0992017bf6f2fbacbf9
ms.sourcegitcommit: d0e71ea63af2f67eba75ba283ec46cc7cdf87d75
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/24/2020
ms.locfileid: "49731975"
---
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a><span data-ttu-id="2cbe9-104">Habilitar la instalación proactiva de Bot y la mensajería proactiva en Teams con Microsoft Graph (vista previa pública)</span><span class="sxs-lookup"><span data-stu-id="2cbe9-104">Enable proactive bot installation and proactive messaging in Teams with Microsoft Graph (Public Preview)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="2cbe9-105">Las vistas previas públicas de Microsoft Graph y Microsoft Teams están disponibles para el acceso anticipado y los comentarios.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="2cbe9-106">Aunque esta versión se ha sometido a pruebas exhaustivas, no está pensada para su uso en producción.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="2cbe9-107">Mensajería proactiva en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="2cbe9-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="2cbe9-108">Los bots inician los mensajes proactivos para iniciar conversaciones con un usuario.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="2cbe9-109">Tienen varios fines, entre los que se incluyen el envío de mensajes de bienvenida, la realización de encuestas o sondeos, y la difusión de notificaciones de toda la organización.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span>  <span data-ttu-id="2cbe9-110">Los mensajes proactivos en Microsoft Teams se pueden entregar como conversaciones **ad-hoc** o **basadas en cuadros de diálogo** :</span><span class="sxs-lookup"><span data-stu-id="2cbe9-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="2cbe9-111">Tipo de mensaje</span><span class="sxs-lookup"><span data-stu-id="2cbe9-111">Message Type</span></span> | <span data-ttu-id="2cbe9-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="2cbe9-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="2cbe9-113">Mensaje proactivo ad-hoc</span><span class="sxs-lookup"><span data-stu-id="2cbe9-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="2cbe9-114">El bot interjects un mensaje sin interrumpir el flujo de conversación.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="2cbe9-115">Mensaje proactivo basado en cuadros de diálogo</span><span class="sxs-lookup"><span data-stu-id="2cbe9-115">Dialog-based proactive message</span></span> | <span data-ttu-id="2cbe9-116">El bot crea un nuevo subproceso de diálogo, toma el control de una conversación, entrega el mensaje proactivo, se cierra y devuelve el control al cuadro de diálogo anterior.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

<span data-ttu-id="2cbe9-117">*Ver*, [enviar notificaciones proactivas a los usuarios SDK V4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2cbe9-117">*See*, [Send proactive notifications to users SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)</span></span>

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="2cbe9-118">Instalación proactiva de aplicaciones en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="2cbe9-118">Proactive app installation in Teams</span></span>

<span data-ttu-id="2cbe9-119">Antes de que el Bot pueda enviar mensajes a un usuario de forma proactiva, debe instalarse como una aplicación personal o en un equipo en el que el usuario sea miembro.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-119">Before your bot can proactively message a user, it needs to be installed either as a personal app, or in a team where the user is a member.</span></span> <span data-ttu-id="2cbe9-120">En ocasiones, es posible que deba realizar mensajes de forma proactiva para los usuarios que _no_ hayan instalado o que se hayan interactuado anteriormente con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-120">At times,  you may need to proactively message users that have _not_ installed or previously interacted with your app.</span></span> <span data-ttu-id="2cbe9-121">Por ejemplo, la necesidad de mensajes vitales para todos los usuarios de la organización.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-121">For instance, the need to message vital information to everyone in your organization.</span></span> <span data-ttu-id="2cbe9-122">Para estos escenarios, puede usar la API de Microsoft Graph para instalar de forma proactiva su bot para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-122">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="2cbe9-123">Permisos</span><span class="sxs-lookup"><span data-stu-id="2cbe9-123">Permissions</span></span>

<span data-ttu-id="2cbe9-124">Los permisos de [tipo de recurso teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) de Microsoft Graph permiten administrar el ciclo de vida de la instalación de la aplicación para todos los ámbitos de usuario (personal) o de equipo (canal) dentro de la plataforma de Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="2cbe9-124">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) permissions allow you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="2cbe9-125">Permisos de aplicación</span><span class="sxs-lookup"><span data-stu-id="2cbe9-125">Application permission</span></span> | <span data-ttu-id="2cbe9-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="2cbe9-126">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="2cbe9-127">Permite a una aplicación de Teams leer, instalar, actualizar y desinstalar para cualquier **usuario**, sin necesidad de iniciar sesión ni usar previamente.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-127">Allows a Teams app to read, install, upgrade, and uninstall itself for any **user**, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="2cbe9-128">Permite a una aplicación de Teams leer, instalar, actualizar y desinstalar en cualquier **equipo**, sin necesidad de iniciar sesión ni usar previamente.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-128">Allows a Teams app to read, install, upgrade, and uninstall itself in any **team**, without prior sign in or use.</span></span>|

<span data-ttu-id="2cbe9-129">Para usar estos permisos, debe agregar una clave [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) al manifiesto de la aplicación con los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="2cbe9-129">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>
> [!div class="checklist"]
> [!div class="checklist"]
>
> * <span data-ttu-id="2cbe9-130">**ID**  : el identificador de la aplicación de Azure ad.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-130">**id**  — your Azure AD app id.</span></span>
> * <span data-ttu-id="2cbe9-131">**recurso** : la dirección URL del recurso de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-131">**resource** — the resource URL for the app.</span></span>
>

>[!NOTE]
>
> * <span data-ttu-id="2cbe9-132">El bot requiere que la _aplicación_ no tenga permisos _delegados_ porque la instalación no es para sí mismo sino para otros.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-132">Your bot requires _application_ not _user delegated_ permissions because the installation is not for yourself but for others.</span></span>
>
> * <span data-ttu-id="2cbe9-133">Un administrador de inquilinos de Azure AD debe [conceder explícitamente permisos a una aplicación](/graph/security-authorization#grant-permissions-to-an-application).</span><span class="sxs-lookup"><span data-stu-id="2cbe9-133">An Azure AD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="2cbe9-134">Después de que se concedan permisos a una aplicación, _todos_ los miembros del inquilino de Azure ad obtendrán los permisos concedidos.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-134">After an application is granted permissions, _all_ members of the Azure AD tenant will gain the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="2cbe9-135">Habilitar la instalación y mensajería proactivas de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="2cbe9-135">Enable proactive app installation and messaging</span></span>

 > [!IMPORTANT]
><span data-ttu-id="2cbe9-136">Microsoft Graph solo instalará aplicaciones publicadas en el [Catálogo de aplicaciones](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) de la organización o en [AppSource](https://appsource.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="2cbe9-136">Microsoft Graph will only install apps published within your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="2cbe9-137">✔ Crear y publicar su bot de mensajería proactiva para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="2cbe9-137">✔ Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="2cbe9-138">Para empezar, necesitará un [bot para Teams](../../bots/how-to/create-a-bot-for-teams.md) con capacidades de [Mensajería proactiva](../../concepts/bots/bot-conversations/bots-conv-proactive.md) y  [publicada](../../concepts/deploy-and-publish/overview.md) en el catálogo de [aplicaciones](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) de su organización o en [AppSource](https://appsource.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="2cbe9-138">To get started, you will need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities and  [published](../../concepts/deploy-and-publish/overview.md) in your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

>[!TIP]
> <span data-ttu-id="2cbe9-139">La plantilla de aplicación de [**Communicator**](../..//samples/app-templates.md#company-communicator) de producción preparada permite la mensajería de difusión y es una buena base para crear una aplicación de bot proactiva.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-139">The production-ready [**Company Communicator**](../..//samples/app-templates.md#company-communicator) app template enables broadcast messaging and is a good foundation for building your proactive bot application.</span></span>

### <a name="-get-the-teamsappid-for-your-app"></a><span data-ttu-id="2cbe9-140">✔ Obtener el `teamsAppId` para la aplicación</span><span class="sxs-lookup"><span data-stu-id="2cbe9-140">✔ Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="2cbe9-141">**1.** necesitará el `teamsAppId`  para los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-141">**1.** You will need the `teamsAppId`  for the next steps.</span></span>

<span data-ttu-id="2cbe9-142">El `teamsAppId` puede recuperarse del catálogo de aplicaciones de su organización:</span><span class="sxs-lookup"><span data-stu-id="2cbe9-142">The `teamsAppId` can be retrieved from your organization's app catalog:</span></span>

<span data-ttu-id="2cbe9-143">**Referencia de página de Microsoft Graph:** [tipo de recurso teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2cbe9-143">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span></span>

<span data-ttu-id="2cbe9-144">Solicitud **http Get** :</span><span class="sxs-lookup"><span data-stu-id="2cbe9-144">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

<span data-ttu-id="2cbe9-145">La solicitud devolverá un `teamsApp`  objeto.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-145">The request will return a `teamsApp`  object.</span></span> <span data-ttu-id="2cbe9-146">El objeto devuelto `id`  es el identificador de aplicación generado por el catálogo de la aplicación y es diferente del "ID:" que ha proporcionado en el manifiesto de la aplicación Teams:</span><span class="sxs-lookup"><span data-stu-id="2cbe9-146">The returned object's `id`  is the app's catalog generated app id and is different from the "id:" that you provided in your Teams app manifest:</span></span>

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

<span data-ttu-id="2cbe9-147">**2.**  si la aplicación ya se ha cargado o realizado localmente para un usuario en el ámbito personal, puede recuperar el como se `teamsAppId` indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="2cbe9-147">**2.**  If your app has already been uploaded/sideloaded for a user in the personal scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="2cbe9-148">**Referencia de página de Microsoft Graph:** [lista de aplicaciones instaladas para el usuario](/graph/api/userteamwork-list-installedapps?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2cbe9-148">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="2cbe9-149">Solicitud **http Get** :</span><span class="sxs-lookup"><span data-stu-id="2cbe9-149">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

<span data-ttu-id="2cbe9-150">**3.** si la aplicación ya se ha cargado o transferido localmente para un canal en el ámbito de equipo, puede recuperar el `teamsAppId` como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="2cbe9-150">**3.** If your app has already been uploaded/sideloaded for a channel in the team scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="2cbe9-151">**Referencia de página de Microsoft Graph:** [enumerar aplicaciones en el equipo](/graph/api/team-list-installedapps?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2cbe9-151">**Microsoft Graph page reference:** [List apps in team](/graph/api/team-list-installedapps?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="2cbe9-152">Solicitud **http Get** :</span><span class="sxs-lookup"><span data-stu-id="2cbe9-152">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> <span data-ttu-id="2cbe9-153">Puede filtrar por cualquiera de los campos del objeto [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) para restringir la lista de resultados.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-153">You can filter on any of the fields of the [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) object to narrow the list of results.</span></span>

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="2cbe9-154">✔ Determinar si su bot está instalado actualmente para un destinatario de mensaje</span><span class="sxs-lookup"><span data-stu-id="2cbe9-154">✔ Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="2cbe9-155">**Referencia de página de Microsoft Graph:** [lista de aplicaciones instaladas para el usuario](/graph/api/userteamwork-list-installedapps?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2cbe9-155">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="2cbe9-156">Solicitud **http Get** :</span><span class="sxs-lookup"><span data-stu-id="2cbe9-156">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="2cbe9-157">Esta solicitud devolverá una matriz vacía si la aplicación no está instalada, o una matriz con un solo objeto [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-beta&preserve-view=true) si se ha instalado.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-157">This request will return an empty array if the app is not installed, or an array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-beta&preserve-view=true) object if it has been installed.</span></span>

### <a name="-install-your-app"></a><span data-ttu-id="2cbe9-158">✔ Instalar la aplicación</span><span class="sxs-lookup"><span data-stu-id="2cbe9-158">✔ Install your app</span></span>

<span data-ttu-id="2cbe9-159">**Referencia de página de Microsoft Graph:** [instalar la aplicación para el usuario](/graph/api/userteamwork-post-installedapps?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2cbe9-159">**Microsoft Graph page reference:** [Install app for user](/graph/api/userteamwork-post-installedapps?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="2cbe9-160">Solicitud **http post** :</span><span class="sxs-lookup"><span data-stu-id="2cbe9-160">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/beta/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="2cbe9-161">Si el usuario tiene Microsoft Teams ejecutándose, puede que vea la aplicación inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-161">If the user has Microsoft Teams running, they may see the app install immediately.</span></span> <span data-ttu-id="2cbe9-162">Como alternativa, puede que sea necesario reiniciar para ver la aplicación instalada.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-162">Alternatively,  a  restart may be necessary to see the installed app.</span></span>

### <a name="-retrieve-the-conversation-chatid"></a><span data-ttu-id="2cbe9-163">✔ Recuperar el **chatId** de conversación</span><span class="sxs-lookup"><span data-stu-id="2cbe9-163">✔ Retrieve the conversation **chatId**</span></span>

<span data-ttu-id="2cbe9-164">Cuando la aplicación está instalada para el usuario, el bot recibirá una `conversationUpdate` [notificación de evento](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) que contendrá la información necesaria para enviar el mensaje proactivo.</span><span class="sxs-lookup"><span data-stu-id="2cbe9-164">When your app is installed for the user, the bot will receive a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that will contain the necessary information to send the proactive message.</span></span>

<span data-ttu-id="2cbe9-165">El `chatId` también se puede recuperar de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="2cbe9-165">The `chatId` can also be retrieved as follows:</span></span>

<span data-ttu-id="2cbe9-166">**Referencia de página de Microsoft Graph:** [obtener chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2cbe9-166">**Microsoft Graph page reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="2cbe9-167">**1.** necesitará la aplicación `{teamsAppInstallationId}` .</span><span class="sxs-lookup"><span data-stu-id="2cbe9-167">**1.** You will need your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="2cbe9-168">Si no la tiene, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2cbe9-168">If you don't have it, use the following:</span></span>

<span data-ttu-id="2cbe9-169">Solicitud **http Get** :</span><span class="sxs-lookup"><span data-stu-id="2cbe9-169">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="2cbe9-170">La propiedad **ID** de la respuesta es `teamsAppInstallationId` .</span><span class="sxs-lookup"><span data-stu-id="2cbe9-170">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

<span data-ttu-id="2cbe9-171">**2.** realice la siguiente solicitud para obtener `chatId` :</span><span class="sxs-lookup"><span data-stu-id="2cbe9-171">**2.** Make the following request to fetch the `chatId`:</span></span>

<span data-ttu-id="2cbe9-172">Solicitud **get de http** (permiso `TeamsAppInstallation.ReadWriteSelfForUser.All` ):</span><span class="sxs-lookup"><span data-stu-id="2cbe9-172">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

<span data-ttu-id="2cbe9-173">La propiedad **ID** de la respuesta es `chatId` .</span><span class="sxs-lookup"><span data-stu-id="2cbe9-173">The **id** property of the response is the `chatId`.</span></span>

<span data-ttu-id="2cbe9-174">Como alternativa, puede recuperar el `chatId`  con la solicitud a continuación, pero necesitará el permiso más amplio `Chat.Read.All` :</span><span class="sxs-lookup"><span data-stu-id="2cbe9-174">Alternately, you can retrieve the `chatId`  with the request below, but it will require the broader `Chat.Read.All` permission:</span></span>

<span data-ttu-id="2cbe9-175">Solicitud **get de http** (permiso `Chat.Read.All` ):</span><span class="sxs-lookup"><span data-stu-id="2cbe9-175">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a><span data-ttu-id="2cbe9-176">✔ Enviar mensajes proactivos</span><span class="sxs-lookup"><span data-stu-id="2cbe9-176">✔ Send proactive messages</span></span>

<span data-ttu-id="2cbe9-177">Una vez que se ha agregado el bot a un usuario o equipo y se ha adquirido la información de usuario necesaria, puede empezar a [enviar mensajes proactivos](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="2cbe9-177">Once your bot has been added for a user or team and has acquired the necessary user  information, it can begin to [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true).</span></span>

# <a name="c--net"></a>[<span data-ttu-id="2cbe9-178">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="2cbe9-178">C# / .NET</span></span>](#tab/csharp)

<span data-ttu-id="2cbe9-179">El siguiente fragmento de código es de los [ejemplos de Microsoft bot Framework para C#.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)</span><span class="sxs-lookup"><span data-stu-id="2cbe9-179">The following code snippet is from the [Microsoft Bot Framework Samples for C#.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="2cbe9-180">JavaScript</span><span class="sxs-lookup"><span data-stu-id="2cbe9-180">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="2cbe9-181">El siguiente fragmento de código es de los [ejemplos de Microsoft bot Framework para JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages).</span><span class="sxs-lookup"><span data-stu-id="2cbe9-181">The following code snippet is from the [Microsoft Bot Framework Samples for JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages).</span></span>

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

## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="2cbe9-182">Tema relacionado para administradores de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="2cbe9-182">Related topic for Teams administrators</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="2cbe9-183">**Administrar directivas de configuración de aplicación en Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="2cbe9-183">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a><span data-ttu-id="2cbe9-184">Ver ejemplos de código adicionales</span><span class="sxs-lookup"><span data-stu-id="2cbe9-184">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="2cbe9-185">**Ejemplos de código de mensajería proactiva de Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="2cbe9-185">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>

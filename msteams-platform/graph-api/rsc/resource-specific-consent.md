---
title: Consentimiento específico de recursos en Microsoft Teams
description: Describe el consentimiento específico del recurso en Microsoft Teams y cómo aprovecharlo.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Gráfico RSC de OAuth SSO de OAuth para Microsoft Teams
ms.openlocfilehash: bf449b338e8c0f42dfef776e533fb6b5ff591529
ms.sourcegitcommit: 1b909fb9ccf6cdd84ed0d8f9ea0463243a802a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "45434506"
---
# <a name="resource-specific-consent-rsc--developer-preview"></a><span data-ttu-id="5e2c1-104">Autorización específica de recursos (RSC): vista previa para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="5e2c1-104">Resource-specific consent (RSC) — Developer Preview</span></span>

>[!NOTE]

><span data-ttu-id="5e2c1-105">Los permisos de consentimiento específicos de recursos están disponibles en los clientes Web y de escritorio una vez habilitada la vista previa para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-105">The resource-specific consent permissions are available in desktop and web clients after Developer Preview has been enabled.</span></span> <span data-ttu-id="5e2c1-106">Vea [Cómo habilito la vista previa para desarrolladores](../../resources/dev-preview/developer-preview-intro.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-106">See [How do I enable Developer Preview](../../resources/dev-preview/developer-preview-intro.md) for more information.</span></span>

<span data-ttu-id="5e2c1-107">El consentimiento específico de recursos (RSC) es una integración de Microsoft Teams y Graph API que permite a su aplicación usar puntos de conexión de API para administrar equipos específicos dentro de una organización.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-107">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="5e2c1-108">El modelo de permisos de autorización específica de recursos (RSC) permite a los *propietarios del equipo* conceder el consentimiento para que una aplicación acceda a los datos de un equipo o los modifique.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-108">The resource-specific consent (RSC) permissions model enables *team owners* to grant consent for an application to access and/or modify a team's data.</span></span> <span data-ttu-id="5e2c1-109">Los permisos de RSC específicos, específicos de Teams, definen lo que una aplicación puede hacer dentro de un equipo específico:</span><span class="sxs-lookup"><span data-stu-id="5e2c1-109">The granular, Teams-specific, RSC permissions define what an application can do within a specific team:</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="5e2c1-110">Permisos específicos de recursos</span><span class="sxs-lookup"><span data-stu-id="5e2c1-110">Resource-specific permissions</span></span>

|<span data-ttu-id="5e2c1-111">Permisos de aplicación</span><span class="sxs-lookup"><span data-stu-id="5e2c1-111">Application permission</span></span>| <span data-ttu-id="5e2c1-112">Acción</span><span class="sxs-lookup"><span data-stu-id="5e2c1-112">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="5e2c1-113">TeamSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="5e2c1-113">TeamSettings.Read.Group</span></span> | <span data-ttu-id="5e2c1-114">Obtener la configuración de este equipo.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-114">Get the settings for this team.</span></span>|
|<span data-ttu-id="5e2c1-115">TeamSettings. Edit. Group</span><span class="sxs-lookup"><span data-stu-id="5e2c1-115">TeamSettings.Edit.Group</span></span>|<span data-ttu-id="5e2c1-116">Actualice la configuración de este equipo.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-116">Update the settings for this team.</span></span>|
|<span data-ttu-id="5e2c1-117">ChannelSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="5e2c1-117">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="5e2c1-118">Obtenga los nombres de canal, las descripciones de canales y la configuración de canal para este equipo.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-118">Get the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="5e2c1-119">ChannelSettings.Edit.Group</span><span class="sxs-lookup"><span data-stu-id="5e2c1-119">ChannelSettings.Edit.Group</span></span>|<span data-ttu-id="5e2c1-120">Actualice los nombres de canal, las descripciones de canal y la configuración de canal para este equipo.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-120">Update the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="5e2c1-121">Channel.Create.Group</span><span class="sxs-lookup"><span data-stu-id="5e2c1-121">Channel.Create.Group</span></span>|<span data-ttu-id="5e2c1-122">Crear canales en este equipo.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-122">Create channels in this team.</span></span>|
|<span data-ttu-id="5e2c1-123">Channel.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="5e2c1-123">Channel.Delete.Group</span></span>|<span data-ttu-id="5e2c1-124">Eliminar los canales de este equipo.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-124">Delete channels in this team.</span></span>|
|<span data-ttu-id="5e2c1-125">ChannelMessage.Read.Group</span><span class="sxs-lookup"><span data-stu-id="5e2c1-125">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="5e2c1-126">Obtiene los mensajes del canal de este equipo.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-126">Get this team's channel messages.</span></span>|
|<span data-ttu-id="5e2c1-127">TeamsApp.Read.Group</span><span class="sxs-lookup"><span data-stu-id="5e2c1-127">TeamsApp.Read.Group</span></span>|<span data-ttu-id="5e2c1-128">Obtenga una lista de las aplicaciones instaladas de este equipo.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-128">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="5e2c1-129">TeamsTab.Read.Group</span><span class="sxs-lookup"><span data-stu-id="5e2c1-129">TeamsTab.Read.Group</span></span>|<span data-ttu-id="5e2c1-130">Obtener una lista de las pestañas de este equipo.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-130">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="5e2c1-131">TeamsTab.Create.Group</span><span class="sxs-lookup"><span data-stu-id="5e2c1-131">TeamsTab.Create.Group</span></span>|<span data-ttu-id="5e2c1-132">Crear pestañas en este equipo.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-132">Create tabs in this team.</span></span>|
|<span data-ttu-id="5e2c1-133">TeamsTab.Edit.Group</span><span class="sxs-lookup"><span data-stu-id="5e2c1-133">TeamsTab.Edit.Group</span></span>|<span data-ttu-id="5e2c1-134">Actualice las pestañas de este equipo.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-134">Update this team's tabs.</span></span>|
|<span data-ttu-id="5e2c1-135">TeamsTab.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="5e2c1-135">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="5e2c1-136">Eliminar las pestañas de este equipo.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-136">Delete this team's tabs.</span></span>|
|<span data-ttu-id="5e2c1-137">Member.Read.Group</span><span class="sxs-lookup"><span data-stu-id="5e2c1-137">Member.Read.Group</span></span>|<span data-ttu-id="5e2c1-138">Obtener los miembros de este equipo.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-138">Get this team's members.</span></span>|
|<span data-ttu-id="5e2c1-139">Owner.Read.Group</span><span class="sxs-lookup"><span data-stu-id="5e2c1-139">Owner.Read.Group</span></span>|<span data-ttu-id="5e2c1-140">Obtener los propietarios de este equipo.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-140">Get this team's owners.</span></span>|

>[!NOTE]
><span data-ttu-id="5e2c1-141">Los permisos específicos de recursos solo están disponibles para las aplicaciones de Teams instaladas en el cliente de Teams y actualmente no forman parte del portal de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-141">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory portal.</span></span>

## <a name="enable-resource-specific-consent-in-your-application"></a><span data-ttu-id="5e2c1-142">Habilitar el consentimiento específico de recursos en la aplicación</span><span class="sxs-lookup"><span data-stu-id="5e2c1-142">Enable resource-specific consent in your application</span></span>

<span data-ttu-id="5e2c1-143">Los pasos para habilitar RSC en la aplicación son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="5e2c1-143">The steps for enabling RSC in your application are as follows:</span></span>

1. <span data-ttu-id="5e2c1-144">[Configure las opciones de consentimiento del propietario del grupo en el portal de Azure Active Directory](#configure-group-owner-consent-settings-in-the-azure-ad-portal).</span><span class="sxs-lookup"><span data-stu-id="5e2c1-144">[Configure group owner consent settings in the Azure Active Directory portal](#configure-group-owner-consent-settings-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="5e2c1-145">[Registre su aplicación con la plataforma de identidad de Microsoft a través del portal de Azure ad](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span><span class="sxs-lookup"><span data-stu-id="5e2c1-145">[Register your app with Microsoft identity platform via the Azure AD portal](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
1. [<span data-ttu-id="5e2c1-146">Revisar los permisos de la aplicación en el portal de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e2c1-146">Review your application permissions in the Azure AD portal</span></span>](#review-your-application-permissions-in-the-azure-ad-portal)
1. <span data-ttu-id="5e2c1-147">[Obtener un token de acceso desde la plataforma de identidad de Microsoft](#obtain-an-access-token-from-the-microsoft-identity-platform).</span><span class="sxs-lookup"><span data-stu-id="5e2c1-147">[Obtain an access token from the Microsoft Identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="5e2c1-148">[Actualizar el manifiesto de la aplicación de Teams](#update-your-teams-app-manifest).</span><span class="sxs-lookup"><span data-stu-id="5e2c1-148">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="5e2c1-149">[Instale la aplicación directamente en Teams](#install-your-app-directly-in-teams).</span><span class="sxs-lookup"><span data-stu-id="5e2c1-149">[Install your app directly in Teams](#install-your-app-directly-in-teams).</span></span>
1. <span data-ttu-id="5e2c1-150">[Compruebe si la aplicación tiene permisos RSC agregados](#check-your-app-for-added-rsc-permissions).</span><span class="sxs-lookup"><span data-stu-id="5e2c1-150">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a><span data-ttu-id="5e2c1-151">Configurar las opciones de consentimiento del propietario del grupo en el portal de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e2c1-151">Configure group owner consent settings in the Azure AD portal</span></span>

<span data-ttu-id="5e2c1-152">Puede habilitar o deshabilitar el [consentimiento del propietario del grupo](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data) directamente en Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="5e2c1-152">You can enable or disable  [group owner consent](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="5e2c1-153">Inicie sesión en [Azure portal](https://portal.azure.com) como administrador [global o administrador](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)de la compañía.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-153">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).</span></span>  
 > - <span data-ttu-id="5e2c1-154">Seleccione configuración de usuario de aplicaciones empresariales de **Azure Active Directory**  => **Enterprise applications**  => **User settings**.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-154">Select **Azure Active Directory** =>**Enterprise applications** =>**User settings**.</span></span>
> - <span data-ttu-id="5e2c1-155">Habilitar, deshabilitar o limitar el consentimiento del usuario con el control etiquetado **los usuarios pueden dar su consentimiento a las aplicaciones que tienen acceso a los datos de la compañía para los grupos a los que** pertenecen (esta funcionalidad está habilitada de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="5e2c1-155">Enable, disable, or limit user consent with the control labeled **Users can consent to apps accessing company data for the groups they own** (This capability is enabled by default).</span></span>

![configuración de RSC de Azure](../../assets/images/azure-rsc-configuration.svg)

| <span data-ttu-id="5e2c1-157">Valor</span><span class="sxs-lookup"><span data-stu-id="5e2c1-157">Value</span></span> | <span data-ttu-id="5e2c1-158">Descripción</span><span class="sxs-lookup"><span data-stu-id="5e2c1-158">Description</span></span>|
|--- | --- |
|<span data-ttu-id="5e2c1-159">Sí</span><span class="sxs-lookup"><span data-stu-id="5e2c1-159">Yes</span></span> | <span data-ttu-id="5e2c1-160">Habilitar el consentimiento específico del grupo para todos los propietarios del grupo.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-160">Enable group-specific consent for all group owners.</span></span>|
|<span data-ttu-id="5e2c1-161">No</span><span class="sxs-lookup"><span data-stu-id="5e2c1-161">No</span></span> |<span data-ttu-id="5e2c1-162">Deshabilitar el consentimiento específico de grupo para todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-162">Disable group-specific consent for all users.</span></span>| 
|<span data-ttu-id="5e2c1-163">Limitada</span><span class="sxs-lookup"><span data-stu-id="5e2c1-163">Limited</span></span> | <span data-ttu-id="5e2c1-164">Habilitar el consentimiento específico de grupo para los miembros de un grupo seleccionado.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-164">Enable group-specific consent for members of a selected group.</span></span>|

<span data-ttu-id="5e2c1-165">Para habilitar o deshabilitar el consentimiento del propietario del grupo dentro de Azure portal con PowerShell, siga los pasos descritos en [configurar el consentimiento del propietario del grupo con PowerShell](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell).</span><span class="sxs-lookup"><span data-stu-id="5e2c1-165">To enable or disable group owner consent within the Azure portal using PowerShell, follow the steps outlined in [Configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell).</span></span>

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a><span data-ttu-id="5e2c1-166">Registrar la aplicación con la plataforma de identidad de Microsoft mediante el portal de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e2c1-166">Register your app with Microsoft identity platform via the Azure AD portal</span></span>

<span data-ttu-id="5e2c1-167">El portal de Azure Active Directory proporciona una plataforma central para registrar y configurar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-167">The Azure Active Directory portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="5e2c1-168">La aplicación debe estar registrada en el portal de Azure AD para integrarse con la plataforma de identidad de Microsoft y las API de gráficos de llamadas.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-168">Your app must be registered in the Azure AD portal to integrate with the Microsoft identity platform and call Graph APIs.</span></span> <span data-ttu-id="5e2c1-169">*Consulte* [registrar una aplicación con la plataforma de identidad de Microsoft](/graph/auth-register-app-v2).</span><span class="sxs-lookup"><span data-stu-id="5e2c1-169">*See* [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).</span></span>

>[!WARNING]
><span data-ttu-id="5e2c1-170">No registre varias aplicaciones de Microsoft Teams en el mismo identificador de aplicación de Azure AD. El identificador de la aplicación debe ser único para cada aplicación.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-170">Do not register multiple Teams apps to the same Azure AD app id. The app id must be unique for each app.</span></span> <span data-ttu-id="5e2c1-171">Se producirá un error si intenta instalar varias aplicaciones en el mismo identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-171">Attempts to install multiple apps to the same app id will fail.</span></span>

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a><span data-ttu-id="5e2c1-172">Revisar los permisos de la aplicación en el portal de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e2c1-172">Review your application permissions in the Azure AD portal</span></span>

<span data-ttu-id="5e2c1-173">Vaya a la página registros de aplicaciones **domésticas**  =>  **App registrations** y seleccione su aplicación RSC.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-173">Navigate to the **Home** => **App registrations** page and select your RSC app.</span></span> <span data-ttu-id="5e2c1-174">Elija **permisos de API** en la barra de navegación izquierda y examine la lista de permisos configurados para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-174">Choose **API permissions** from the left nav bar and examine the list of configured permissions for your app.</span></span> <span data-ttu-id="5e2c1-175">Si la aplicación solo realiza llamadas de gráfico RSC, elimine todos los permisos de esa página.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-175">If your app will only make RSC Graph calls, delete all the permission on that page.</span></span> <span data-ttu-id="5e2c1-176">Si la aplicación también va a realizar llamadas que no son RSC, conserve dichos permisos según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-176">If your app will also make non-RSC calls, keep those permissions as needed.</span></span>

>[!IMPORTANT]
><span data-ttu-id="5e2c1-177">El portal de Azure AD no se puede usar para solicitar permisos RSC.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-177">The Azure AD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="5e2c1-178">Los permisos RSC actualmente son exclusivos de las aplicaciones de Teams instaladas en el cliente de Microsoft Teams y se declaran en el archivo de manifiesto de la aplicación (JSON).</span><span class="sxs-lookup"><span data-stu-id="5e2c1-178">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="5e2c1-179">Obtener un token de acceso desde la plataforma de identidad de Microsoft</span><span class="sxs-lookup"><span data-stu-id="5e2c1-179">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="5e2c1-180">Para realizar llamadas a la API de Graph, debe obtener un token de acceso para la aplicación desde la plataforma de identidad.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-180">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="5e2c1-181">Para que la aplicación pueda obtener un token de la plataforma de identidad de Microsoft, debe estar registrado en el portal de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-181">Before your app can get a token from the Microsoft identity platform, it must be registered in the Azure AD portal.</span></span> <span data-ttu-id="5e2c1-182">El token de acceso contiene información sobre la aplicación y los permisos que tiene para los recursos y las API disponibles a través de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-182">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="5e2c1-183">Necesitará tener los siguientes valores del proceso de registro de Azure AD para recuperar un token de acceso de la plataforma de identidad:</span><span class="sxs-lookup"><span data-stu-id="5e2c1-183">You'll need to have the following values from the Azure AD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="5e2c1-184">IDENTIFICADOR de la **aplicación** asignado por el portal de registro de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-184">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="5e2c1-185">Si la aplicación admite el inicio de sesión único (SSO), debe usar el mismo identificador de aplicación para la aplicación y el SSO.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-185">If your app supports single sign-on (SSO) you should use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="5e2c1-186">El **secreto de cliente/contraseña** o un par de claves pública y privada (**certificado**).</span><span class="sxs-lookup"><span data-stu-id="5e2c1-186">The  **Client secret/password** or a public/private key pair (**Certificate**).</span></span> <span data-ttu-id="5e2c1-187">Esto no es necesario para las aplicaciones nativas.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-187">This is not required for native apps.</span></span>
- <span data-ttu-id="5e2c1-188">Un **URI de redireccionamiento** (o dirección URL de respuesta) de la aplicación para recibir respuestas de Azure ad.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-188">A **Redirect URI** (or reply URL) for your app to receive responses from Azure AD.</span></span>

 <span data-ttu-id="5e2c1-189">*Vea* [obtener acceso en nombre de un usuario](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token) y [obtener acceso sin un usuario](/graph/auth-v2-service)</span><span class="sxs-lookup"><span data-stu-id="5e2c1-189">*See* [Get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token) and [Get access without a user](/graph/auth-v2-service)</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="5e2c1-190">Actualizar el manifiesto de la aplicación de Teams</span><span class="sxs-lookup"><span data-stu-id="5e2c1-190">Update your Teams app manifest</span></span>

<span data-ttu-id="5e2c1-191">Los permisos RSC se declaran en el archivo de manifiesto de la aplicación (JSON).</span><span class="sxs-lookup"><span data-stu-id="5e2c1-191">The RSC permissions are declared in you app manifest (JSON) file.</span></span>  <span data-ttu-id="5e2c1-192">Agregue una clave [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) al manifiesto de la aplicación con los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="5e2c1-192">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="5e2c1-193">**ID** : el identificador de la aplicación de Azure ad. *Consulte* [registrar la aplicación en el portal de Azure ad](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span><span class="sxs-lookup"><span data-stu-id="5e2c1-193">**id**  — your Azure AD app id. *See* [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="5e2c1-194">**recurso** : cualquier cadena.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-194">**resource**  — any string.</span></span> <span data-ttu-id="5e2c1-195">Este campo no tiene ninguna operación en RSC, pero debe agregarse y tener un valor para evitar una respuesta de error; se realizará cualquier cadena.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-195">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>
> - <span data-ttu-id="5e2c1-196">**permisos de aplicación** : permisos RSC para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-196">**application permissions** — RSC permissions for  your app.</span></span> <span data-ttu-id="5e2c1-197">*Consulte* [permisos específicos de recursos](resource-specific-consent.md#resource-specific-permissions).</span><span class="sxs-lookup"><span data-stu-id="5e2c1-197">*See* [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

>
>[!IMPORTANT]
> <span data-ttu-id="5e2c1-198">Los permisos no RSC se almacenan en Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-198">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="5e2c1-199">No los agregue al manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-199">Do not add them to the app manifest.</span></span>
>

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelMessage.Read.Group",
      "TeamSettings.Edit.Group",
      "ChannelSettings.Edit.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.Edit.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group"
    ]
  }
```

## <a name="install-your-app-directly-in-teams"></a><span data-ttu-id="5e2c1-200">Instalar la aplicación directamente en Teams</span><span class="sxs-lookup"><span data-stu-id="5e2c1-200">Install your app directly in Teams</span></span>

<span data-ttu-id="5e2c1-201">Una vez que haya creado la aplicación, puede [cargar el paquete de la aplicación](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) directamente a un equipo específico.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-201">Once you've created your app you can [upload your app package](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) directly to a specific team.</span></span>  <span data-ttu-id="5e2c1-202">Para ello, la configuración de directiva **cargar aplicaciones personalizadas** debe estar habilitada como parte de las directivas de configuración de aplicaciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-202">To do so, the **Upload custom apps** policy setting must be enabled as part of the custom app setup policies.</span></span> <span data-ttu-id="5e2c1-203">*Consulte* [Custom App Policy Settings](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings).</span><span class="sxs-lookup"><span data-stu-id="5e2c1-203">*See* [Custom app policy settings](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings).</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="5e2c1-204">Comprobar si la aplicación tiene permisos RSC agregados</span><span class="sxs-lookup"><span data-stu-id="5e2c1-204">Check your app for added RSC permissions</span></span>

>[!IMPORTANT]
><span data-ttu-id="5e2c1-205">Los permisos RSC no se atribuyen a un usuario.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-205">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="5e2c1-206">Las llamadas se realizan con los permisos de aplicaciones, no con los permisos delegados de usuario.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-206">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="5e2c1-207">Por lo tanto, es posible que se permita a la aplicación realizar acciones que el usuario no puede, como crear un canal o eliminar una pestaña. Debe revisar la intención del propietario del equipo de su caso de uso antes de hacer llamadas a la API RSC.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-207">Thus, the app may be allowed to perform actions that the user cannot, such as creating a channel or deleting a tab. You should review the team owner's intent for your use case prior to making RSC API calls.</span></span> <span data-ttu-id="5e2c1-208">*Vea* [información general de la API de Microsoft Teams](/graph/teams-concept-overview).</span><span class="sxs-lookup"><span data-stu-id="5e2c1-208">*See* [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="5e2c1-209">Una vez instalada la aplicación en un equipo, puede usar el [probador de Graph](https://developer.microsoft.com/graph/graph-explorer) para ver los permisos que se han concedido a la aplicación en un equipo:</span><span class="sxs-lookup"><span data-stu-id="5e2c1-209">Once the app has been installed to a team, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)  to view the permissions that have been granted to the app in a team:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="5e2c1-210">Obtenga el **GROUPID** del equipo del cliente de Teams.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-210">Get the team's **groupId** from the Teams client.</span></span>
> - <span data-ttu-id="5e2c1-211">En el cliente de Microsoft Teams, seleccione **Teams** en la barra de navegación de la parte izquierda.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-211">In the Teams client, select **Teams** from the far left nav bar.</span></span>
> - <span data-ttu-id="5e2c1-212">Seleccione el equipo en el que se instalará la aplicación desde el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-212">Select the team where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="5e2c1-213">Seleccione el icono **más opciones** (&#8943;).</span><span class="sxs-lookup"><span data-stu-id="5e2c1-213">Select the **More options** icon (&#8943;).</span></span>
> - <span data-ttu-id="5e2c1-214">Seleccione **obtener vínculo a equipo**.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-214">Select **Get link to team**.</span></span>
> - <span data-ttu-id="5e2c1-215">Copie y guarde el valor **GROUPID** de la cadena.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-215">Copy and save the **groupId** value from the string.</span></span>
> - <span data-ttu-id="5e2c1-216">Inicie sesión en el **probador de Graph**.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-216">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="5e2c1-217">Realice una llamada **Get** al siguiente punto de conexión: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` .</span><span class="sxs-lookup"><span data-stu-id="5e2c1-217">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="5e2c1-218">El campo clientAppId de la respuesta se asignará al appId especificado en el manifiesto de la aplicación Teams.</span><span class="sxs-lookup"><span data-stu-id="5e2c1-218">The clientAppId field in the response will map to the appId specified in the Teams app manifest.</span></span>

 ![Respuesta del explorador de Graph para obtener la llamada.](../../assets/images/graph-permissions.png)
 
## <a name="test-resource-specific-consent"></a><span data-ttu-id="5e2c1-220">Probar el consentimiento específico del recurso</span><span class="sxs-lookup"><span data-stu-id="5e2c1-220">Test resource-specific consent</span></span>
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="5e2c1-221">**Probar permisos de consentimiento específicos de recursos en Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="5e2c1-221">**Test resource-specific consent permissions in Teams**</span></span>](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="5e2c1-222">Tema relacionado para administradores de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="5e2c1-222">Related topic for Teams administrators</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5e2c1-223">**Consentimiento específico de recursos en Microsoft Teams para administradores**</span><span class="sxs-lookup"><span data-stu-id="5e2c1-223">**Resource-specific consent in Microsoft Teams for admins**</span></span>](/MicrosoftTeams/resource-specific-consent)
> 

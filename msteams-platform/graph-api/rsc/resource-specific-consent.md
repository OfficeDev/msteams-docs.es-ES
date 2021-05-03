---
title: Consentimiento específico de recursos en Teams
description: Describe el consentimiento específico de los recursos en Teams y cómo aprovecharlo.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: autorización de teams OAuth SSO AAD rsc Graph
ms.openlocfilehash: 39e5c1bb8375fb5b5a3bd3900cb6ad870a3ff677
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101796"
---
# <a name="resource-specific-consent-rsc"></a><span data-ttu-id="0a18e-104">Consentimiento específico de recursos (RSC)</span><span class="sxs-lookup"><span data-stu-id="0a18e-104">Resource-specific consent (RSC)</span></span>

<span data-ttu-id="0a18e-105">El consentimiento específico de recursos (RSC) es una integración de api de Microsoft Teams y Microsoft Graph que permite a la aplicación usar puntos de conexión de API para administrar equipos específicos dentro de una organización.</span><span class="sxs-lookup"><span data-stu-id="0a18e-105">Resource-specific consent (RSC) is a Microsoft Teams and Microsoft Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="0a18e-106">El modelo de permisos de consentimiento específico  de recursos (RSC) permite a los propietarios del equipo conceder el consentimiento para que una aplicación acceda o modifique los datos de un equipo.</span><span class="sxs-lookup"><span data-stu-id="0a18e-106">The resource-specific consent (RSC) permissions model enables *team owners* to grant consent for an application to access and/or modify a team's data.</span></span> <span data-ttu-id="0a18e-107">Los permisos de RSC pormenorizados, Teams específicos de la aplicación definen lo que una aplicación puede hacer dentro de un equipo específico:</span><span class="sxs-lookup"><span data-stu-id="0a18e-107">The granular, Teams-specific, RSC permissions define what an application can do within a specific team:</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="0a18e-108">Permisos específicos de recursos</span><span class="sxs-lookup"><span data-stu-id="0a18e-108">Resource-specific permissions</span></span>

|<span data-ttu-id="0a18e-109">Permisos de aplicación</span><span class="sxs-lookup"><span data-stu-id="0a18e-109">Application permission</span></span>| <span data-ttu-id="0a18e-110">Acción</span><span class="sxs-lookup"><span data-stu-id="0a18e-110">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="0a18e-111">TeamSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="0a18e-111">TeamSettings.Read.Group</span></span> | <span data-ttu-id="0a18e-112">Obtén la configuración de este equipo.</span><span class="sxs-lookup"><span data-stu-id="0a18e-112">Get the settings for this team.</span></span>|
|<span data-ttu-id="0a18e-113">TeamSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="0a18e-113">TeamSettings.ReadWrite.Group</span></span>|<span data-ttu-id="0a18e-114">Actualizar la configuración de este equipo.</span><span class="sxs-lookup"><span data-stu-id="0a18e-114">Update the settings for this team.</span></span>|
|<span data-ttu-id="0a18e-115">ChannelSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="0a18e-115">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="0a18e-116">Obtenga los nombres de canal, las descripciones de canales y la configuración del canal para este equipo.</span><span class="sxs-lookup"><span data-stu-id="0a18e-116">Get the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="0a18e-117">ChannelSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="0a18e-117">ChannelSettings.ReadWrite.Group</span></span>|<span data-ttu-id="0a18e-118">Actualice los nombres de canal, las descripciones de canales y la configuración del canal para este equipo.</span><span class="sxs-lookup"><span data-stu-id="0a18e-118">Update the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="0a18e-119">Channel.Create.Group</span><span class="sxs-lookup"><span data-stu-id="0a18e-119">Channel.Create.Group</span></span>|<span data-ttu-id="0a18e-120">Crear canales en este equipo.</span><span class="sxs-lookup"><span data-stu-id="0a18e-120">Create channels in this team.</span></span>|
|<span data-ttu-id="0a18e-121">Channel.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="0a18e-121">Channel.Delete.Group</span></span>|<span data-ttu-id="0a18e-122">Eliminar canales en este equipo.</span><span class="sxs-lookup"><span data-stu-id="0a18e-122">Delete channels in this team.</span></span>|
|<span data-ttu-id="0a18e-123">ChannelMessage.Read.Group</span><span class="sxs-lookup"><span data-stu-id="0a18e-123">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="0a18e-124">Obtener los mensajes de canal de este equipo.</span><span class="sxs-lookup"><span data-stu-id="0a18e-124">Get this team's channel messages.</span></span>|
|<span data-ttu-id="0a18e-125">TeamsAppInstallation.Read.Group</span><span class="sxs-lookup"><span data-stu-id="0a18e-125">TeamsAppInstallation.Read.Group</span></span>|<span data-ttu-id="0a18e-126">Obtén una lista de las aplicaciones instaladas de este equipo.</span><span class="sxs-lookup"><span data-stu-id="0a18e-126">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="0a18e-127">TeamsTab.Read.Group</span><span class="sxs-lookup"><span data-stu-id="0a18e-127">TeamsTab.Read.Group</span></span>|<span data-ttu-id="0a18e-128">Obtener una lista de las pestañas de este equipo.</span><span class="sxs-lookup"><span data-stu-id="0a18e-128">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="0a18e-129">TeamsTab.Create.Group</span><span class="sxs-lookup"><span data-stu-id="0a18e-129">TeamsTab.Create.Group</span></span>|<span data-ttu-id="0a18e-130">Crear pestañas en este equipo.</span><span class="sxs-lookup"><span data-stu-id="0a18e-130">Create tabs in this team.</span></span>|
|<span data-ttu-id="0a18e-131">TeamsTab.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="0a18e-131">TeamsTab.ReadWrite.Group</span></span>|<span data-ttu-id="0a18e-132">Actualizar las pestañas de este equipo.</span><span class="sxs-lookup"><span data-stu-id="0a18e-132">Update this team's tabs.</span></span>|
|<span data-ttu-id="0a18e-133">TeamsTab.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="0a18e-133">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="0a18e-134">Eliminar las pestañas de este equipo.</span><span class="sxs-lookup"><span data-stu-id="0a18e-134">Delete this team's tabs.</span></span>|
|<span data-ttu-id="0a18e-135">TeamMember.Read.Group</span><span class="sxs-lookup"><span data-stu-id="0a18e-135">TeamMember.Read.Group</span></span>|<span data-ttu-id="0a18e-136">Obtener los miembros de este equipo.</span><span class="sxs-lookup"><span data-stu-id="0a18e-136">Get this team's members.</span></span>|

>[!NOTE]
><span data-ttu-id="0a18e-137">Los permisos específicos de recursos solo están disponibles para Teams aplicaciones instaladas en el cliente Teams y actualmente no forman parte del portal Azure Active Directory web.</span><span class="sxs-lookup"><span data-stu-id="0a18e-137">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory portal.</span></span>

## <a name="enable-resource-specific-consent-in-your-application"></a><span data-ttu-id="0a18e-138">Habilitar el consentimiento específico de recursos en la aplicación</span><span class="sxs-lookup"><span data-stu-id="0a18e-138">Enable resource-specific consent in your application</span></span>

<span data-ttu-id="0a18e-139">Los pasos para habilitar RSC en la aplicación son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="0a18e-139">The steps for enabling RSC in your application are as follows:</span></span>

1. <span data-ttu-id="0a18e-140">[Configure las opciones de consentimiento del](#configure-group-owner-consent-settings-in-the-azure-ad-portal)propietario del grupo en Azure Active Directory portal .</span><span class="sxs-lookup"><span data-stu-id="0a18e-140">[Configure group owner consent settings in the Azure Active Directory portal](#configure-group-owner-consent-settings-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="0a18e-141">[Registre la aplicación con Plataforma de identidad de Microsoft a través del portal de Azure AD](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span><span class="sxs-lookup"><span data-stu-id="0a18e-141">[Register your app with Microsoft identity platform via the Azure AD portal](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="0a18e-142">[Revise los permisos de la aplicación en el Portal de Azure AD](#review-your-application-permissions-in-the-azure-ad-portal).</span><span class="sxs-lookup"><span data-stu-id="0a18e-142">[Review your application permissions in the Azure AD portal](#review-your-application-permissions-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="0a18e-143">[Obtener un token de acceso de la plataforma Microsoft Identity](#obtain-an-access-token-from-the-microsoft-identity-platform).</span><span class="sxs-lookup"><span data-stu-id="0a18e-143">[Obtain an access token from the Microsoft Identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="0a18e-144">[Actualizar el manifiesto Teams aplicación](#update-your-teams-app-manifest).</span><span class="sxs-lookup"><span data-stu-id="0a18e-144">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="0a18e-145">[Instala la aplicación directamente en Teams](#sideload-your-app-in-teams).</span><span class="sxs-lookup"><span data-stu-id="0a18e-145">[Install your app directly in Teams](#sideload-your-app-in-teams).</span></span>
1. <span data-ttu-id="0a18e-146">[Comprueba si la aplicación tiene permisos RSC agregados.](#check-your-app-for-added-rsc-permissions)</span><span class="sxs-lookup"><span data-stu-id="0a18e-146">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a><span data-ttu-id="0a18e-147">Configurar la configuración del consentimiento del propietario del grupo en el Portal de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a18e-147">Configure group owner consent settings in the Azure AD portal</span></span>

<span data-ttu-id="0a18e-148">Puede habilitar o deshabilitar el consentimiento del [propietario del grupo](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directamente en Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="0a18e-148">You can enable or disable [group owner consent](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="0a18e-149">Inicie sesión en [Azure Portal](https://portal.azure.com) como administrador [global/administrador de la compañía](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).</span><span class="sxs-lookup"><span data-stu-id="0a18e-149">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).</span></span>  
 > - <span data-ttu-id="0a18e-150">[Seleccione](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** Enterprise  =>  **aplicaciones Consent** y  =>  **permisos** Configuración de  =>  **consentimiento de usuario**.</span><span class="sxs-lookup"><span data-stu-id="0a18e-150">[Select](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** => **Enterprise applications** => **Consent and permissions** => **User consent settings**.</span></span>
> - <span data-ttu-id="0a18e-151">Habilitar, deshabilitar o limitar el consentimiento del usuario con el control etiquetado Consentimiento del propietario del grupo para las aplicaciones que tienen acceso a datos **(El** valor predeterminado es Permitir el consentimiento del propietario del grupo para todos **los propietarios del grupo).**</span><span class="sxs-lookup"><span data-stu-id="0a18e-151">Enable, disable, or limit user consent with the control labeled **Group owner consent for apps accessing data** (The default is **Allow group owner consent for all group owners**).</span></span> <span data-ttu-id="0a18e-152">Para que el propietario de un equipo instale una aplicación con RSC, el consentimiento del propietario del grupo debe estar habilitado para ese usuario.</span><span class="sxs-lookup"><span data-stu-id="0a18e-152">For a team owner to install an app using RSC, group owner consent must be enabled for that user.</span></span>

![configuración de azure rsc](../../assets/images/azure-rsc-configuration.png)

<span data-ttu-id="0a18e-154">Para habilitar o deshabilitar el consentimiento del propietario del grupo con PowerShell, siga los pasos descritos en [Configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="0a18e-154">To enable or disable group owner consent using PowerShell, follow the steps outlined in [Configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).</span></span>

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a><span data-ttu-id="0a18e-155">Registrar la aplicación con Plataforma de identidad de Microsoft a través del portal de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a18e-155">Register your app with Microsoft identity platform via the Azure AD portal</span></span>

<span data-ttu-id="0a18e-156">El Azure Active Directory web proporciona una plataforma central para que se registren y configuren las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0a18e-156">The Azure Active Directory portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="0a18e-157">La aplicación debe estar registrada en Azure AD Portal para integrarse con el Plataforma de identidad de Microsoft y llamar a las API Graph Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0a18e-157">Your app must be registered in the Azure AD portal to integrate with the Microsoft identity platform and call Microsoft Graph APIs.</span></span> <span data-ttu-id="0a18e-158">*Vea* [Registrar una aplicación con el Plataforma de identidad de Microsoft](/graph/auth-register-app-v2).</span><span class="sxs-lookup"><span data-stu-id="0a18e-158">*See* [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).</span></span>

>[!WARNING]
><span data-ttu-id="0a18e-159">No registre varias aplicaciones Teams en el mismo identificador de aplicación de Azure AD. El identificador de la aplicación debe ser único para cada aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a18e-159">Do not register multiple Teams apps to the same Azure AD app id. The app id must be unique for each app.</span></span> <span data-ttu-id="0a18e-160">Se producirá un error al intentar instalar varias aplicaciones en el mismo identificador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a18e-160">Attempts to install multiple apps to the same app id will fail.</span></span>

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a><span data-ttu-id="0a18e-161">Revisar los permisos de la aplicación en el Portal de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a18e-161">Review your application permissions in the Azure AD portal</span></span>

<span data-ttu-id="0a18e-162">Vaya a la **página Registros** de la aplicación principal y seleccione la aplicación  =>   RSC.</span><span class="sxs-lookup"><span data-stu-id="0a18e-162">Navigate to the **Home** => **App registrations** page and select your RSC app.</span></span> <span data-ttu-id="0a18e-163">Elija **permisos de API en** la barra de navegación izquierda y examine la lista de permisos configurados para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a18e-163">Choose **API permissions** from the left nav bar and examine the list of configured permissions for your app.</span></span> <span data-ttu-id="0a18e-164">Si la aplicación solo realizará llamadas Graph API de RSC, elimina todos los permisos de esa página.</span><span class="sxs-lookup"><span data-stu-id="0a18e-164">If your app will only make RSC Graph API calls, delete all the permission on that page.</span></span> <span data-ttu-id="0a18e-165">Si la aplicación también realizará llamadas que no son de RSC, mantén esos permisos según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0a18e-165">If your app will also make non-RSC calls, keep those permissions as needed.</span></span>

>[!IMPORTANT]
><span data-ttu-id="0a18e-166">El portal de Azure AD no se puede usar para solicitar permisos de RSC.</span><span class="sxs-lookup"><span data-stu-id="0a18e-166">The Azure AD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="0a18e-167">Actualmente, los permisos RSC son exclusivos Teams aplicaciones instaladas en el cliente de Teams y se declaran en el archivo de manifiesto de aplicación (JSON).</span><span class="sxs-lookup"><span data-stu-id="0a18e-167">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="0a18e-168">Obtener un token de acceso de la Plataforma de identidad de Microsoft</span><span class="sxs-lookup"><span data-stu-id="0a18e-168">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="0a18e-169">Para realizar Graph API, debes obtener un token de acceso para la aplicación desde la plataforma de identidad.</span><span class="sxs-lookup"><span data-stu-id="0a18e-169">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="0a18e-170">Para que la aplicación pueda obtener un token del Plataforma de identidad de Microsoft, debe registrarse en el Portal de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a18e-170">Before your app can get a token from the Microsoft identity platform, it must be registered in the Azure AD portal.</span></span> <span data-ttu-id="0a18e-171">El token de acceso contiene información sobre la aplicación y los permisos que tiene para los recursos y las API disponibles a través de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="0a18e-171">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="0a18e-172">Deberá tener los siguientes valores del proceso de registro de Azure AD para recuperar un token de acceso de la plataforma de identidad:</span><span class="sxs-lookup"><span data-stu-id="0a18e-172">You'll need to have the following values from the Azure AD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="0a18e-173">Id. **de aplicación** asignado por el portal de registro de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0a18e-173">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="0a18e-174">Si la aplicación admite el inicio de sesión único (SSO), debes usar el mismo identificador de aplicación para tu aplicación y SSO.</span><span class="sxs-lookup"><span data-stu-id="0a18e-174">If your app supports single sign-on (SSO) you should use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="0a18e-175">El  **secreto de cliente/contraseña** o un par de claves público/privado (**Certificado**).</span><span class="sxs-lookup"><span data-stu-id="0a18e-175">The  **Client secret/password** or a public/private key pair (**Certificate**).</span></span> <span data-ttu-id="0a18e-176">Esto no es necesario para las aplicaciones nativas.</span><span class="sxs-lookup"><span data-stu-id="0a18e-176">This is not required for native apps.</span></span>
- <span data-ttu-id="0a18e-177">Uri **de redireccionamiento** (o dirección URL de respuesta) para que la aplicación reciba respuestas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a18e-177">A **Redirect URI** (or reply URL) for your app to receive responses from Azure AD.</span></span>

 <span data-ttu-id="0a18e-178">*Consulta* [Obtener acceso en nombre de un usuario y](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) Obtener acceso sin un [usuario](/graph/auth-v2-service)</span><span class="sxs-lookup"><span data-stu-id="0a18e-178">*See* [Get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) and [Get access without a user](/graph/auth-v2-service)</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="0a18e-179">Actualizar el manifiesto Teams aplicación</span><span class="sxs-lookup"><span data-stu-id="0a18e-179">Update your Teams app manifest</span></span>

<span data-ttu-id="0a18e-180">Los permisos RSC se declaran en el archivo de manifiesto de aplicación (JSON).</span><span class="sxs-lookup"><span data-stu-id="0a18e-180">The RSC permissions are declared in your app manifest (JSON) file.</span></span>  <span data-ttu-id="0a18e-181">Agregue una [clave webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) al manifiesto de la aplicación con los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="0a18e-181">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="0a18e-182">**id:**  el identificador de la aplicación de Azure AD. *Vea* [Registrar la aplicación en el Portal de Azure AD](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span><span class="sxs-lookup"><span data-stu-id="0a18e-182">**id**  — your Azure AD app id. *See* [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="0a18e-183">**resource:**  cualquier cadena.</span><span class="sxs-lookup"><span data-stu-id="0a18e-183">**resource**  — any string.</span></span> <span data-ttu-id="0a18e-184">Este campo no tiene ninguna operación en RSC, pero debe agregarse y tener un valor para evitar una respuesta de error; cualquier cadena lo hará.</span><span class="sxs-lookup"><span data-stu-id="0a18e-184">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>
> - <span data-ttu-id="0a18e-185">**permisos de aplicación:** permisos RSC para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a18e-185">**application permissions** — RSC permissions for  your app.</span></span> <span data-ttu-id="0a18e-186">*Consulte* [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span><span class="sxs-lookup"><span data-stu-id="0a18e-186">*See* [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

>
>[!IMPORTANT]
> <span data-ttu-id="0a18e-187">Los permisos que no son RSC se almacenan en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0a18e-187">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="0a18e-188">No los agregues al manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a18e-188">Do not add them to the app manifest.</span></span>
>

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelMessage.Read.Group",
      "TeamSettings.Edit.Group",
      "ChannelSettings.ReadWrite.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.ReadWrite.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group"
    ]
  }
```

## <a name="sideload-your-app-in-teams"></a><span data-ttu-id="0a18e-189">Descarga local de la aplicación en Teams</span><span class="sxs-lookup"><span data-stu-id="0a18e-189">Sideload your app in Teams</span></span>

<span data-ttu-id="0a18e-190">Si el Teams permite cargas de aplicaciones personalizadas, [puedes](~/concepts/deploy-and-publish/apps-upload.md) realizar la instalación local de la aplicación directamente en un equipo específico.</span><span class="sxs-lookup"><span data-stu-id="0a18e-190">If your Teams admin allows custom app uploads, you can [sideload your app](~/concepts/deploy-and-publish/apps-upload.md) directly to a specific team.</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="0a18e-191">Comprueba la aplicación para obtener permisos RSC agregados</span><span class="sxs-lookup"><span data-stu-id="0a18e-191">Check your app for added RSC permissions</span></span>

>[!IMPORTANT]
><span data-ttu-id="0a18e-192">Los permisos RSC no se atribuyó a un usuario.</span><span class="sxs-lookup"><span data-stu-id="0a18e-192">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="0a18e-193">Las llamadas se realizan con permisos de aplicación, no con permisos delegados por el usuario.</span><span class="sxs-lookup"><span data-stu-id="0a18e-193">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="0a18e-194">Por lo tanto, es posible que la aplicación pueda realizar acciones que el usuario no pueda, como crear un canal o eliminar una pestaña. Debe revisar la intención del propietario del equipo para su caso de uso antes de realizar llamadas a la API de RSC.</span><span class="sxs-lookup"><span data-stu-id="0a18e-194">Thus, the app may be allowed to perform actions that the user cannot, such as creating a channel or deleting a tab. You should review the team owner's intent for your use case prior to making RSC API calls.</span></span> <span data-ttu-id="0a18e-195">*Vea* [Microsoft Teams introducción a la API .](/graph/teams-concept-overview)</span><span class="sxs-lookup"><span data-stu-id="0a18e-195">*See* [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="0a18e-196">Una vez instalada la aplicación en un equipo, puedes usar [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) para ver los permisos que se han concedido a la aplicación en un equipo:</span><span class="sxs-lookup"><span data-stu-id="0a18e-196">Once the app has been installed to a team, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)  to view the permissions that have been granted to the app in a team:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="0a18e-197">Obtenga el **groupId** del equipo desde el Teams cliente.</span><span class="sxs-lookup"><span data-stu-id="0a18e-197">Get the team's **groupId** from the Teams client.</span></span>
> - <span data-ttu-id="0a18e-198">En el Teams, seleccione **Teams** de la barra de navegación de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="0a18e-198">In the Teams client, select **Teams** from the far left nav bar.</span></span>
> - <span data-ttu-id="0a18e-199">Selecciona el equipo donde está instalada la aplicación en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="0a18e-199">Select the team where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="0a18e-200">Seleccione el **icono Más opciones** (&#8943;).</span><span class="sxs-lookup"><span data-stu-id="0a18e-200">Select the **More options** icon (&#8943;).</span></span>
> - <span data-ttu-id="0a18e-201">Seleccione **Obtener vínculo al equipo**.</span><span class="sxs-lookup"><span data-stu-id="0a18e-201">Select **Get link to team**.</span></span>
> - <span data-ttu-id="0a18e-202">Copie y guarde el **valor groupId** de la cadena.</span><span class="sxs-lookup"><span data-stu-id="0a18e-202">Copy and save the **groupId** value from the string.</span></span>
> - <span data-ttu-id="0a18e-203">Inicie sesión **en Graph Explorer**.</span><span class="sxs-lookup"><span data-stu-id="0a18e-203">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="0a18e-204">Realice una **llamada GET** al siguiente extremo: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` .</span><span class="sxs-lookup"><span data-stu-id="0a18e-204">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="0a18e-205">El campo clientAppId de la respuesta se asignará al appId especificado en el manifiesto Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a18e-205">The clientAppId field in the response will map to the appId specified in the Teams app manifest.</span></span>
  <span data-ttu-id="0a18e-206">![Graph respuesta del explorador a la llamada GET.](../../assets/images/graph-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="0a18e-206">![Graph explorer response to GET call.](../../assets/images/graph-permissions.png)</span></span>

## <a name="code-sample"></a><span data-ttu-id="0a18e-207">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="0a18e-207">Code sample</span></span>
| <span data-ttu-id="0a18e-208">**Nombre de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="0a18e-208">**Sample name**</span></span> | <span data-ttu-id="0a18e-209">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="0a18e-209">**Description**</span></span> | <span data-ttu-id="0a18e-210">**.NET**</span><span class="sxs-lookup"><span data-stu-id="0a18e-210">**.NET**</span></span> |<span data-ttu-id="0a18e-211">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="0a18e-211">**Node.js**</span></span> |
|-----------------|-----------------|----------------|----------------|
| <span data-ttu-id="0a18e-212">Consentimiento específico de recursos (RSC)</span><span class="sxs-lookup"><span data-stu-id="0a18e-212">Resource Specific Consent (RSC)</span></span> | <span data-ttu-id="0a18e-213">Use RSC para llamar a Graph API.</span><span class="sxs-lookup"><span data-stu-id="0a18e-213">Use RSC to call Graph APIs.</span></span> | [<span data-ttu-id="0a18e-214">View</span><span class="sxs-lookup"><span data-stu-id="0a18e-214">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[<span data-ttu-id="0a18e-215">View</span><span class="sxs-lookup"><span data-stu-id="0a18e-215">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|



## <a name="test-resource-specific-consent"></a><span data-ttu-id="0a18e-216">Probar el consentimiento específico de los recursos</span><span class="sxs-lookup"><span data-stu-id="0a18e-216">Test resource-specific consent</span></span>
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="0a18e-217">**Probar permisos de consentimiento específicos de recursos en Teams**</span><span class="sxs-lookup"><span data-stu-id="0a18e-217">**Test resource-specific consent permissions in Teams**</span></span>](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="0a18e-218">Tema relacionado para Teams administradores</span><span class="sxs-lookup"><span data-stu-id="0a18e-218">Related topic for Teams administrators</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0a18e-219">**Consentimiento específico de recursos en Microsoft Teams para administradores**</span><span class="sxs-lookup"><span data-stu-id="0a18e-219">**Resource-specific consent in Microsoft Teams for admins**</span></span>](/MicrosoftTeams/resource-specific-consent)
> 


---
title: Probar permisos de consentimiento específicos de recursos en Teams
description: Detalles que prueban el consentimiento específico de recursos Teams con Postman
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: tutorial
keywords: autorización de teams OAuth SSO AAD rsc Postman Graph
ms.openlocfilehash: 29dc0241bfd5b42cb1853de3e89e43344c223c24
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994276"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a><span data-ttu-id="88c13-104">Probar permisos de consentimiento específicos de recursos en Teams</span><span class="sxs-lookup"><span data-stu-id="88c13-104">Test resource-specific consent permissions in Teams</span></span>

> [!NOTE]
> <span data-ttu-id="88c13-105">El consentimiento específico de los recursos para el ámbito de chat solo está disponible en [la versión preliminar del desarrollador](../../resources/dev-preview/developer-preview-intro.md) público.</span><span class="sxs-lookup"><span data-stu-id="88c13-105">Resource-specific consent for chat scope is available in [public developer preview](../../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="88c13-106">El consentimiento específico de recursos (RSC) es una integración de api de Microsoft Teams y Graph que permite a la aplicación usar puntos de conexión de API para administrar recursos específicos (ya sea equipos o chats) dentro de una organización.</span><span class="sxs-lookup"><span data-stu-id="88c13-106">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific resources—either teams or chats—within an organization.</span></span> <span data-ttu-id="88c13-107">Para obtener más información, vea [Resource-specific consent (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).</span><span class="sxs-lookup"><span data-stu-id="88c13-107">For more information, see [Resource-specific consent (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).</span></span>

> [!NOTE]
> <span data-ttu-id="88c13-108">Para probar los permisos de RSC, el archivo de manifiesto Teams aplicación debe incluir una clave **webApplicationInfo** rellenada con los campos siguientes:</span><span class="sxs-lookup"><span data-stu-id="88c13-108">To test the RSC permissions, your Teams app manifest file must include a **webApplicationInfo** key populated with the following fields:</span></span>
>
> - <span data-ttu-id="88c13-109">**id:** El identificador de la aplicación de Azure AD, consulte [Registrar la aplicación en el Portal de Azure AD](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span><span class="sxs-lookup"><span data-stu-id="88c13-109">**id**: Your Azure AD app ID, see [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="88c13-110">**resource**: Any string, see the note in [Update your Teams app manifest](resource-specific-consent.md#update-your-teams-app-manifest).</span><span class="sxs-lookup"><span data-stu-id="88c13-110">**resource**: Any string, see the note in  [Update your Teams app manifest](resource-specific-consent.md#update-your-teams-app-manifest).</span></span>
> - <span data-ttu-id="88c13-111">**permisos de aplicación:** permisos RSC para la aplicación, consulta [Permisos específicos de recursos](resource-specific-consent.md#resource-specific-permissions).</span><span class="sxs-lookup"><span data-stu-id="88c13-111">**application permissions**: RSC permissions for  your app, see [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

## <a name="example-for-a-team"></a><span data-ttu-id="88c13-112">Ejemplo para un equipo</span><span class="sxs-lookup"><span data-stu-id="88c13-112">Example for a team</span></span>
```json
"webApplicationInfo":{
      "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
      "resource":"https://AnyString",
      "applicationPermissions":[
         "Channel.Create.Group",
         "Channel.Delete.Group",
         "ChannelMessage.Read.Group",
         "ChannelSettings.Read.Group",
         "ChannelSettings.Edit.Group",
         "Member.Read.Group",
         "Owner.Read.Group",
         "TeamsApp.Read.Group",
         "TeamsTab.Read.Group",
         "TeamsTab.Create.Group",
         "TeamsTab.Edit.Group",
         "TeamsTab.Delete.Group",
         "TeamSettings.Read.Group",
         "TeamSettings.Edit.Group"
      ]
   }
```

## <a name="example-for-a-chat"></a><span data-ttu-id="88c13-113">Ejemplo para un chat</span><span class="sxs-lookup"><span data-stu-id="88c13-113">Example for a chat</span></span>
```json
"webApplicationInfo":{
      "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
      "resource":"https://AnyString",
      "applicationPermissions":[
          "ChatSettings.Read.Chat",
          "ChatSettings.ReadWrite.Chat",
          "ChatMessage.Read.Chat",
          "ChatMember.Read.Chat",
          "Chat.Manage.Chat",
          "TeamsTab.Read.Chat",
          "TeamsTab.Create.Chat",
          "TeamsTab.Delete.Chat",
          "TeamsTab.ReadWrite.Chat",
          "TeamsAppInstallation.Read.Chat",
          "OnlineMeeting.ReadBasic.Chat"
      ]
   }
```

> [!IMPORTANT]
> <span data-ttu-id="88c13-114">En el manifiesto de la aplicación, solo incluye los permisos de RSC que quieras que tenga la aplicación.</span><span class="sxs-lookup"><span data-stu-id="88c13-114">In your app manifest, only include the RSC permissions that you want your app to have.</span></span>

>[!NOTE]
><span data-ttu-id="88c13-115">Si la aplicación está pensada para admitir la instalación en ámbitos de equipo y chat, los permisos de equipo y chat se pueden especificar en el mismo manifiesto en `applicationPermissions` .</span><span class="sxs-lookup"><span data-stu-id="88c13-115">If the app is meant to support installation in both team and chat scopes, then both team and chat permissions can be specified in the same manifest under `applicationPermissions`.</span></span>

## <a name="test-added-rsc-permissions-to-a-team-using-the-postman-app"></a><span data-ttu-id="88c13-116">Probar los permisos RSC agregados a un equipo mediante la aplicación Postman</span><span class="sxs-lookup"><span data-stu-id="88c13-116">Test added RSC permissions to a team using the Postman app</span></span>

<span data-ttu-id="88c13-117">Para comprobar si la carga de solicitud de API está respetando los permisos RSC, debe copiar el código de prueba JSON de [RSC](test-team-rsc-json-file.md) para el equipo en el entorno local y actualizar los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="88c13-117">To check whether the RSC permissions are being honored by the API request payload, you need to copy the [RSC JSON test code for team](test-team-rsc-json-file.md) into your local environment and update the following values:</span></span>

* <span data-ttu-id="88c13-118">`azureADAppId`: Id. de aplicación de Azure AD de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="88c13-118">`azureADAppId`: Your app's Azure AD app ID.</span></span>
* <span data-ttu-id="88c13-119">`azureADAppSecret`: la contraseña de la aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88c13-119">`azureADAppSecret`: Your Azure AD app password.</span></span>
* <span data-ttu-id="88c13-120">`token_scope`: el ámbito es necesario para obtener un token.</span><span class="sxs-lookup"><span data-stu-id="88c13-120">`token_scope`: The scope is required to get a token.</span></span> <span data-ttu-id="88c13-121">establezca el valor en https://graph.microsoft.com/.default .</span><span class="sxs-lookup"><span data-stu-id="88c13-121">set the value to https://graph.microsoft.com/.default.</span></span>
* <span data-ttu-id="88c13-122">`teamGroupId`: Puede obtener el identificador de grupo de grupo del Teams de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="88c13-122">`teamGroupId`: You can get the team group id from the Teams client as follows:</span></span>

    1. <span data-ttu-id="88c13-123">En el Teams, seleccione **Teams** en la barra de navegación de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="88c13-123">In the Teams client, select **Teams** from the far left navigation bar.</span></span>
    2. <span data-ttu-id="88c13-124">Selecciona el equipo donde está instalada la aplicación en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="88c13-124">Select the team where the app is installed from the dropdown menu.</span></span>
    3. <span data-ttu-id="88c13-125">Seleccione el **icono Más opciones** (&#8943;).</span><span class="sxs-lookup"><span data-stu-id="88c13-125">Select the **More options** icon (&#8943;).</span></span>
    4. <span data-ttu-id="88c13-126">Seleccione **Obtener vínculo al equipo**.</span><span class="sxs-lookup"><span data-stu-id="88c13-126">Select **Get link to team**.</span></span> 
    5. <span data-ttu-id="88c13-127">Copie y guarde el **valor groupId** de la cadena.</span><span class="sxs-lookup"><span data-stu-id="88c13-127">Copy and save the **groupId** value from the string.</span></span>

## <a name="test-added-rsc-permissions-to-a-chat-using-the-postman-app"></a><span data-ttu-id="88c13-128">Probar los permisos RSC agregados a un chat con la aplicación Postman</span><span class="sxs-lookup"><span data-stu-id="88c13-128">Test added RSC permissions to a chat using the Postman app</span></span>

<span data-ttu-id="88c13-129">Para comprobar si la carga de solicitud de API está respetando los permisos RSC, debe copiar el código de prueba JSON de [RSC](test-chat-rsc-json-file.md) para chats en el entorno local y actualizar los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="88c13-129">To check whether the RSC permissions are being honored by the API request payload, you need to copy the [RSC JSON test code for chats](test-chat-rsc-json-file.md) into your local environment and update the following values:</span></span>

* <span data-ttu-id="88c13-130">`azureADAppId`: Id. de aplicación de Azure AD de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="88c13-130">`azureADAppId`: Your app's Azure AD app ID.</span></span>
* <span data-ttu-id="88c13-131">`azureADAppSecret`: la contraseña de la aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88c13-131">`azureADAppSecret`: Your Azure AD app password.</span></span>
* <span data-ttu-id="88c13-132">`token_scope`: el ámbito es necesario para obtener un token.</span><span class="sxs-lookup"><span data-stu-id="88c13-132">`token_scope`: The scope is required to get a token.</span></span> <span data-ttu-id="88c13-133">establezca el valor en https://graph.microsoft.com/.default .</span><span class="sxs-lookup"><span data-stu-id="88c13-133">set the value to https://graph.microsoft.com/.default.</span></span>
* <span data-ttu-id="88c13-134">`tenantId`: el nombre o el identificador de objeto de AAD del inquilino.</span><span class="sxs-lookup"><span data-stu-id="88c13-134">`tenantId`: The name or the AAD Object ID of your tenant.</span></span>
* <span data-ttu-id="88c13-135">`chatId`: Puede obtener el identificador de subproceso de chat del Teams *web* de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="88c13-135">`chatId`: You can get the chat thread id from the Teams *web* client as follows:</span></span>

    1. <span data-ttu-id="88c13-136">En el Teams web, seleccione **Chat** en la barra de navegación de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="88c13-136">In the Teams web client, select **Chat** from the far left navigation bar.</span></span>
    2. <span data-ttu-id="88c13-137">Selecciona el chat donde está instalada la aplicación en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="88c13-137">Select the chat where the app is installed from the dropdown menu.</span></span>
    3. <span data-ttu-id="88c13-138">Copie la dirección URL web y guarde el identificador del subproceso de chat de la cadena.</span><span class="sxs-lookup"><span data-stu-id="88c13-138">Copy the web URL and save the chat thread id from the string.</span></span>
<span data-ttu-id="88c13-139">![Identificador de subproceso de chat desde la dirección URL web.](../../assets/images/chat-thread-id.png)</span><span class="sxs-lookup"><span data-stu-id="88c13-139">![Chat thread id from web URL.](../../assets/images/chat-thread-id.png)</span></span>

### <a name="use-postman"></a><span data-ttu-id="88c13-140">Usar Postman</span><span class="sxs-lookup"><span data-stu-id="88c13-140">Use Postman</span></span>

1. <span data-ttu-id="88c13-141">Abre la [aplicación Postman.](https://www.postman.com)</span><span class="sxs-lookup"><span data-stu-id="88c13-141">Open the [Postman](https://www.postman.com) app.</span></span>
2. <span data-ttu-id="88c13-142">Seleccione **Importar**  >    >  **archivo Importar archivo para** cargar el archivo JSON actualizado desde el entorno.</span><span class="sxs-lookup"><span data-stu-id="88c13-142">Select **File** > **Import** > **Import file** to upload the updated JSON file from your environment.</span></span>  
3. <span data-ttu-id="88c13-143">Seleccione la **pestaña Colecciones.**</span><span class="sxs-lookup"><span data-stu-id="88c13-143">Select the **Collections** tab.</span></span> 
4. <span data-ttu-id="88c13-144">Seleccione el chevron **>** junto al **RSC** de prueba para expandir la vista de detalles y ver las solicitudes de API.</span><span class="sxs-lookup"><span data-stu-id="88c13-144">Select the chevron **>** next to the **Test RSC** to expand the details view and see the API requests.</span></span>

<span data-ttu-id="88c13-145">Ejecute toda la colección de permisos para cada llamada a la API.</span><span class="sxs-lookup"><span data-stu-id="88c13-145">Execute the entire permissions collection for each API call.</span></span> <span data-ttu-id="88c13-146">Los permisos especificados en el manifiesto de la aplicación deben ser correctos, mientras que los no especificados deben producir un error con un código de estado HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="88c13-146">The permissions that you specified in your app manifest must succeed, while those not specified must fail with an HTTP 403 status code.</span></span> <span data-ttu-id="88c13-147">Comprueba todos los códigos de estado de respuesta para confirmar que el comportamiento de los permisos de RSC en la aplicación cumple las expectativas.</span><span class="sxs-lookup"><span data-stu-id="88c13-147">Check all of the response status codes to confirm that the behavior of the RSC permissions in your app meet expectations.</span></span>

> [!NOTE]
> <span data-ttu-id="88c13-148">Para probar llamadas API DELETE y READ específicas, agregue esos escenarios de instancia al archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="88c13-148">To test specific DELETE and READ API calls, add those instance scenarios to the JSON file.</span></span>

## <a name="test-revoked-rsc-permissions-using-postman"></a><span data-ttu-id="88c13-149">Probar permisos RSC revocados con [Postman](https://www.postman.com/)</span><span class="sxs-lookup"><span data-stu-id="88c13-149">Test revoked RSC permissions using [Postman](https://www.postman.com/)</span></span>

1. <span data-ttu-id="88c13-150">Desinstale la aplicación del recurso específico.</span><span class="sxs-lookup"><span data-stu-id="88c13-150">Uninstall the app from the specific resource.</span></span>
2. <span data-ttu-id="88c13-151">Siga los pasos para chat o equipo:</span><span class="sxs-lookup"><span data-stu-id="88c13-151">Follow the steps for either chat or team:</span></span> 
    1. <span data-ttu-id="88c13-152">[Probar los permisos RSC agregados a un equipo mediante Postman](#test-added-rsc-permissions-to-a-team-using-the-postman-app).</span><span class="sxs-lookup"><span data-stu-id="88c13-152">[Test added RSC permissions to a team using Postman](#test-added-rsc-permissions-to-a-team-using-the-postman-app).</span></span>
    2. <span data-ttu-id="88c13-153">[Probar los permisos RSC agregados a un chat con Postman](#test-added-rsc-permissions-to-a-chat-using-the-postman-app).</span><span class="sxs-lookup"><span data-stu-id="88c13-153">[Test added RSC permissions to a chat using Postman](#test-added-rsc-permissions-to-a-chat-using-the-postman-app).</span></span>
3. <span data-ttu-id="88c13-154">Compruebe todos los códigos de estado de respuesta para confirmar que las llamadas API específicas han fallado con un código de estado **HTTP 403**.</span><span class="sxs-lookup"><span data-stu-id="88c13-154">Check all the response status codes to confirm that the specific API calls **have failed with an HTTP 403 status code**.</span></span>

## <a name="see-also"></a><span data-ttu-id="88c13-155">Ver también</span><span class="sxs-lookup"><span data-stu-id="88c13-155">See also</span></span>

[<span data-ttu-id="88c13-156">API Graph Microsoft y Teams</span><span class="sxs-lookup"><span data-stu-id="88c13-156">Microsoft Graph API and Teams</span></span>](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)


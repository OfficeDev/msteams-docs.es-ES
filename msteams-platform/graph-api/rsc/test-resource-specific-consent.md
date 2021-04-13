---
title: Probar permisos de consentimiento específicos de recursos en Teams
description: Detalles que prueban el consentimiento específico de recursos en Teams con Postman
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: tutorial
keywords: Autorización de teams OAuth SSO AAD rsc Postman Graph
ms.openlocfilehash: ea764ec2cbca653221d7194d0759ac39f93ec802
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654429"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a><span data-ttu-id="16f1f-104">Probar permisos de consentimiento específicos de recursos en Teams</span><span class="sxs-lookup"><span data-stu-id="16f1f-104">Test resource-specific consent permissions in Teams</span></span>

<span data-ttu-id="16f1f-105">El consentimiento específico de los recursos (RSC) es una integración de Microsoft Teams y la API de Graph que permite a la aplicación usar puntos de conexión de API para administrar equipos específicos dentro de una organización.</span><span class="sxs-lookup"><span data-stu-id="16f1f-105">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="16f1f-106">Para obtener más información, vea [Resource-specific consent (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).</span><span class="sxs-lookup"><span data-stu-id="16f1f-106">For more information, see [Resource-specific consent (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).</span></span>

> [!NOTE]
> <span data-ttu-id="16f1f-107">Para probar los permisos de RSC, el archivo de manifiesto de la aplicación teams debe incluir una clave **webApplicationInfo** rellenada con los campos siguientes:</span><span class="sxs-lookup"><span data-stu-id="16f1f-107">To test the RSC permissions, your Teams app manifest file must include a **webApplicationInfo** key populated with the following fields:</span></span>
>
> - <span data-ttu-id="16f1f-108">**id:** El identificador de la aplicación de Azure AD, consulte [Registrar la aplicación en el Portal de Azure AD](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span><span class="sxs-lookup"><span data-stu-id="16f1f-108">**id**: Your Azure AD app ID, see [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="16f1f-109">**resource**: Any string, see the note in  [Update your Teams app manifest](resource-specific-consent.md#update-your-teams-app-manifest).</span><span class="sxs-lookup"><span data-stu-id="16f1f-109">**resource**: Any string, see the note in  [Update your Teams app manifest](resource-specific-consent.md#update-your-teams-app-manifest).</span></span>
> - <span data-ttu-id="16f1f-110">**permisos de aplicación:** permisos RSC para la aplicación, consulta [Permisos específicos de recursos](resource-specific-consent.md#resource-specific-permissions).</span><span class="sxs-lookup"><span data-stu-id="16f1f-110">**application permissions**: RSC permissions for  your app, see [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

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

> [!IMPORTANT]
> <span data-ttu-id="16f1f-111">En el manifiesto de la aplicación, solo incluye los permisos de RSC que quieras que tenga la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16f1f-111">In your app manifest, only include the RSC permissions that you want your app to have.</span></span>

## <a name="test-added-rsc-permissions-using-the-postman-app"></a><span data-ttu-id="16f1f-112">Probar permisos RSC agregados mediante la aplicación Postman</span><span class="sxs-lookup"><span data-stu-id="16f1f-112">Test added RSC permissions using the Postman app</span></span>

<span data-ttu-id="16f1f-113">Para comprobar si la carga de solicitud de API está respetando los permisos RSC, debe copiar el código de prueba JSON de [RSC](test-rsc-json-file.md) en el entorno local y actualizar los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="16f1f-113">To check whether the RSC permissions are being honored by the API request payload, you need to copy the [RSC JSON test code](test-rsc-json-file.md) into your local environment and update the following values:</span></span>

* <span data-ttu-id="16f1f-114">`azureADAppId`: Id. de aplicación de Azure AD de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16f1f-114">`azureADAppId`: Your app's Azure AD app ID.</span></span>
* <span data-ttu-id="16f1f-115">`azureADAppSecret`: la contraseña de la aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16f1f-115">`azureADAppSecret`: Your Azure AD app password.</span></span>
* <span data-ttu-id="16f1f-116">`token_scope`: el ámbito es necesario para obtener un token.</span><span class="sxs-lookup"><span data-stu-id="16f1f-116">`token_scope`: The scope is required to get a token.</span></span> <span data-ttu-id="16f1f-117">establezca el valor en https://graph.microsoft.com/.default .</span><span class="sxs-lookup"><span data-stu-id="16f1f-117">set the value to https://graph.microsoft.com/.default.</span></span>
* <span data-ttu-id="16f1f-118">`teamGroupId`: Puede obtener el identificador de grupo de grupo del cliente de Teams de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="16f1f-118">`teamGroupId`: You can get the team group id from the Teams client as follows:</span></span>

    1. <span data-ttu-id="16f1f-119">En el cliente de Teams, seleccione **Teams en** la barra de navegación de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="16f1f-119">In the Teams client, select **Teams** from the far left navigation bar.</span></span>
    2. <span data-ttu-id="16f1f-120">Selecciona el equipo donde está instalada la aplicación en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="16f1f-120">Select the team where the app is installed from the dropdown menu.</span></span>
    3. <span data-ttu-id="16f1f-121">Seleccione el **icono Más opciones** (&#8943;).</span><span class="sxs-lookup"><span data-stu-id="16f1f-121">Select the **More options** icon (&#8943;).</span></span>
    4. <span data-ttu-id="16f1f-122">Seleccione **Obtener vínculo al equipo**.</span><span class="sxs-lookup"><span data-stu-id="16f1f-122">Select **Get link to team**.</span></span> 
    5. <span data-ttu-id="16f1f-123">Copie y guarde el **valor groupId** de la cadena.</span><span class="sxs-lookup"><span data-stu-id="16f1f-123">Copy and save the **groupId** value from the string.</span></span>

### <a name="use-postman"></a><span data-ttu-id="16f1f-124">Usar Postman</span><span class="sxs-lookup"><span data-stu-id="16f1f-124">Use Postman</span></span>

1. <span data-ttu-id="16f1f-125">Abre la [aplicación Postman.](https://www.postman.com)</span><span class="sxs-lookup"><span data-stu-id="16f1f-125">Open the [Postman](https://www.postman.com) app.</span></span>
2. <span data-ttu-id="16f1f-126">Seleccione **Importar**  >    >  **archivo Importar archivo para** cargar el archivo JSON actualizado desde el entorno.</span><span class="sxs-lookup"><span data-stu-id="16f1f-126">Select **File** > **Import** > **Import file** to upload the updated JSON file from your environment.</span></span>  
3. <span data-ttu-id="16f1f-127">Seleccione la **pestaña Colecciones.**</span><span class="sxs-lookup"><span data-stu-id="16f1f-127">Select the **Collections** tab.</span></span> 
4. <span data-ttu-id="16f1f-128">Seleccione el chevron **>** junto al **RSC** de prueba para expandir la vista de detalles y ver las solicitudes de API.</span><span class="sxs-lookup"><span data-stu-id="16f1f-128">Select the chevron **>** next to the **Test RSC** to expand the details view and see the API requests.</span></span>

<span data-ttu-id="16f1f-129">Ejecute toda la colección de permisos para cada llamada a la API.</span><span class="sxs-lookup"><span data-stu-id="16f1f-129">Execute the entire permissions collection for each API call.</span></span> <span data-ttu-id="16f1f-130">Los permisos especificados en el manifiesto de la aplicación deben ser correctos, mientras que los no especificados deben producir un error con un código de estado HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="16f1f-130">The permissions that you specified in your app manifest must succeed, while those not specified must fail with an HTTP 403 status code.</span></span> <span data-ttu-id="16f1f-131">Comprueba todos los códigos de estado de respuesta para confirmar que el comportamiento de los permisos de RSC en la aplicación cumple las expectativas.</span><span class="sxs-lookup"><span data-stu-id="16f1f-131">Check all of the response status codes to confirm that the behavior of the RSC permissions in your app meet expectations.</span></span>

> [!NOTE]
> <span data-ttu-id="16f1f-132">Para probar llamadas API DELETE y READ específicas, agregue esos escenarios de instancia al archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="16f1f-132">To test specific DELETE and READ API calls, add those instance scenarios to the JSON file.</span></span>

## <a name="test-revoked-rsc-permissions-using-postman"></a><span data-ttu-id="16f1f-133">Probar permisos RSC revocados con [Postman](https://www.postman.com/)</span><span class="sxs-lookup"><span data-stu-id="16f1f-133">Test revoked RSC permissions using [Postman](https://www.postman.com/)</span></span>

1. <span data-ttu-id="16f1f-134">Desinstale la aplicación del equipo específico.</span><span class="sxs-lookup"><span data-stu-id="16f1f-134">Uninstall the app from the specific team.</span></span>
2. <span data-ttu-id="16f1f-135">Siga los pasos para probar los permisos [RSC agregados mediante Postman](#test-added-rsc-permissions-using-the-postman-app).</span><span class="sxs-lookup"><span data-stu-id="16f1f-135">Follow the steps for [Test added RSC permissions using Postman](#test-added-rsc-permissions-using-the-postman-app).</span></span>
3. <span data-ttu-id="16f1f-136">Compruebe todos los códigos de estado de respuesta para confirmar que las llamadas API específicas, correctamente, han fallado con un código de estado **HTTP 403**.</span><span class="sxs-lookup"><span data-stu-id="16f1f-136">Check all the response status codes to confirm that the specific API calls, **succeeded, have failed with an HTTP 403 status code**.</span></span>

## <a name="see-also"></a><span data-ttu-id="16f1f-137">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="16f1f-137">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="16f1f-138">API de Microsoft Graph y Teams</span><span class="sxs-lookup"><span data-stu-id="16f1f-138">Microsoft Graph API and Teams</span></span>](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)


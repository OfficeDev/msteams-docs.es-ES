---
title: Probar el consentimiento específico de los recursos en Microsoft Teams
description: Detalles de prueba del consentimiento específico del recurso en Microsoft Teams con Postman
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: tutorial
keywords: Gráfico de autorización de equipo de OAuth de OAuth SSO de AAD de Microsoft Teams
ms.openlocfilehash: f50f61e7eb62e3bcc6af2dafc1c7c781ff2145de
ms.sourcegitcommit: 43e1be9d9e3651ce73a8d2139e44d75550a0ca60
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2020
ms.locfileid: "49366857"
---
# <a name="test-resource-specific-consent-permissions--in-teams"></a><span data-ttu-id="28fc7-104">Probar permisos de consentimiento específicos de recursos en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="28fc7-104">Test resource-specific consent permissions  in Teams</span></span>

<span data-ttu-id="28fc7-105">El consentimiento específico de recursos (RSC) es una integración de Microsoft Teams y Graph API que permite a su aplicación usar puntos de conexión de API para administrar equipos específicos dentro de una organización.</span><span class="sxs-lookup"><span data-stu-id="28fc7-105">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="28fc7-106">*Consulte*[autorización específica de recursos (RSC): API de Microsoft Teams Graph](resource-specific-consent.md).  </span><span class="sxs-lookup"><span data-stu-id="28fc7-106">Please *see*  [Resource-specific consent (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).</span></span>

> [!NOTE]
><span data-ttu-id="28fc7-107">Para probar los permisos RSC, el archivo de manifiesto de la aplicación de Microsoft Teams debe incluir una clave **webApplicationInfo** rellenada con los siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="28fc7-107">To test the RSC permissions, your Teams app manifest file must include a **webApplicationInfo** key populated with the following fields:</span></span>
>
> - <span data-ttu-id="28fc7-108">**ID**  : el identificador de la aplicación de Azure ad, *vea* [registrar la aplicación en el portal de Azure ad](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span><span class="sxs-lookup"><span data-stu-id="28fc7-108">**id**  — your Azure AD app id, *see* [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="28fc7-109">**recurso**  : cualquier cadena, *vea* la nota en  [actualizar el manifiesto de la aplicación Teams](resource-specific-consent.md#update-your-teams-app-manifest)</span><span class="sxs-lookup"><span data-stu-id="28fc7-109">**resource**  — any string, *see* the note in  [Update your Teams app manifest](resource-specific-consent.md#update-your-teams-app-manifest)</span></span>
> - <span data-ttu-id="28fc7-110">**permisos de aplicación** : permisos RSC para la aplicación, *vea* [permisos específicos de recursos](resource-specific-consent.md#resource-specific-permissions).</span><span class="sxs-lookup"><span data-stu-id="28fc7-110">**application permissions** — RSC permissions for  your app, *see* [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

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

>[!IMPORTANT]
><span data-ttu-id="28fc7-111">En el manifiesto de la aplicación, incluya solo los permisos RSC que desea que tenga la aplicación.</span><span class="sxs-lookup"><span data-stu-id="28fc7-111">In your app manifest, only include the RSC permissions that you want your app to have.</span></span>

## <a name="test-added-rsc-permissions-using-the-postman-app"></a><span data-ttu-id="28fc7-112">Probar los permisos RSC agregados mediante la aplicación Postman</span><span class="sxs-lookup"><span data-stu-id="28fc7-112">Test added RSC permissions using the Postman app</span></span>

<span data-ttu-id="28fc7-113">Para comprobar si la carga de solicitud de API respeta los permisos RSC, deberá copiar el [código de prueba JSON de RSC](test-rsc-json-file.md) en su entorno local y actualizar los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="28fc7-113">To check whether the RSC permissions are being honored by the API request payload, you'll need to copy the [RSC JSON test code](test-rsc-json-file.md) into your local environment and update the following values:</span></span>

1. <span data-ttu-id="28fc7-114">`azureADAppId`  -identificador de la aplicación de Azure AD de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="28fc7-114">`azureADAppId`  — your app's Azure AD app id.</span></span>
1. <span data-ttu-id="28fc7-115">`azureADAppSecret`  : su secreto de la aplicación de Azure AD (contraseña)</span><span class="sxs-lookup"><span data-stu-id="28fc7-115">`azureADAppSecret`  — your Azure AD app secret (password)</span></span>
1. <span data-ttu-id="28fc7-116">`token_scope`  — el ámbito es obligatorio para obtener un token: establezca el valor en https://graph.microsoft.com/.default</span><span class="sxs-lookup"><span data-stu-id="28fc7-116">`token_scope`  — the scope is required to get a token - set the value to https://graph.microsoft.com/.default</span></span>
1. <span data-ttu-id="28fc7-117">`teamGroupId` puede obtener el identificador del grupo de equipos desde el cliente de Microsoft Teams de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="28fc7-117">`teamGroupId` — you can get the team group id from the Teams client as follows:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="28fc7-118">En el cliente de Microsoft Teams, seleccione **Teams** en la barra de navegación de la parte izquierda.</span><span class="sxs-lookup"><span data-stu-id="28fc7-118">In the Teams client, select **Teams** from the far left nav bar .</span></span>
> * <span data-ttu-id="28fc7-119">Seleccione el equipo en el que se instalará la aplicación desde el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="28fc7-119">Select the team where the app is installed from the dropdown menu.</span></span>
> * <span data-ttu-id="28fc7-120">Seleccione el icono **más opciones** (&#8943;)</span><span class="sxs-lookup"><span data-stu-id="28fc7-120">Select the **More options** icon (&#8943;)</span></span>
> * <span data-ttu-id="28fc7-121">Seleccione **obtener vínculo a equipo**</span><span class="sxs-lookup"><span data-stu-id="28fc7-121">Select **Get link to team**</span></span> 
> * <span data-ttu-id="28fc7-122">Copie y guarde el valor **GROUPID** de la cadena.</span><span class="sxs-lookup"><span data-stu-id="28fc7-122">Copy and save the **groupId** value from the string.</span></span>

### <a name="using-postman"></a><span data-ttu-id="28fc7-123">Uso de Postman</span><span class="sxs-lookup"><span data-stu-id="28fc7-123">Using Postman</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="28fc7-124">Abra la aplicación [Postman](https://www.postman.com) .</span><span class="sxs-lookup"><span data-stu-id="28fc7-124">Open the [Postman](https://www.postman.com) app.</span></span>
> * <span data-ttu-id="28fc7-125">Seleccione **archivo**  =>  **importar**  =>  **Importar archivo** para cargar el archivo JSON actualizado desde su entorno.</span><span class="sxs-lookup"><span data-stu-id="28fc7-125">Select **File** => **Import** => **Import file** to upload the updated JSON file from your environment.</span></span>  
> * <span data-ttu-id="28fc7-126">Seleccione la pestaña **colecciones** .</span><span class="sxs-lookup"><span data-stu-id="28fc7-126">Select the **Collections** tab.</span></span> 
> * <span data-ttu-id="28fc7-127">Seleccione la comilla angular (>) junto a la **prueba RSC** para expandir la vista de detalles y ver las solicitudes de la API.</span><span class="sxs-lookup"><span data-stu-id="28fc7-127">Select the chevron (>) next to the **Test RSC** to expand the details view and see the API requests.</span></span>

<span data-ttu-id="28fc7-128">Ejecutar toda la colección de permisos para cada llamada a la API.</span><span class="sxs-lookup"><span data-stu-id="28fc7-128">Execute the entire permissions collection for each API call.</span></span> <span data-ttu-id="28fc7-129">Los permisos especificados en el manifiesto de la aplicación deben realizarse correctamente, mientras que los que no se hayan especificado deben generar un error con un código de Estado HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="28fc7-129">The permissions that you specified in your app manifest should succeed, while those not specified should fail with an HTTP 403 status code.</span></span> <span data-ttu-id="28fc7-130">Compruebe todos los códigos de estado de respuesta para confirmar que el comportamiento de los permisos RSC en la aplicación cumple las expectativas.</span><span class="sxs-lookup"><span data-stu-id="28fc7-130">Check all of the response status codes to confirm that the behavior of the RSC permissions in your app meet expectations.</span></span>

>[!NOTE]
><span data-ttu-id="28fc7-131">Para probar las llamadas específicas de eliminación y lectura de la API, agregue los escenarios de instancia al archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="28fc7-131">To test specific DELETE and READ API calls, please add those instance scenarios to the JSON file.</span></span>

## <a name="test--revoked-rsc-permissions-using-postman"></a><span data-ttu-id="28fc7-132">Probar los permisos RSC revocados mediante [Postman](https://www.postman.com/)</span><span class="sxs-lookup"><span data-stu-id="28fc7-132">Test  revoked RSC permissions using [Postman](https://www.postman.com/)</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="28fc7-133">Desinstalar la aplicación del equipo específico.</span><span class="sxs-lookup"><span data-stu-id="28fc7-133">Uninstall the app from the specific team.</span></span>
> * <span data-ttu-id="28fc7-134">Siga los pasos anteriores para [probar los permisos RSC agregados mediante Postman](#test-added-rsc-permissions-using-the-postman-app).</span><span class="sxs-lookup"><span data-stu-id="28fc7-134">Follow the steps above for [Test added RSC permissions using Postman](#test-added-rsc-permissions-using-the-postman-app).</span></span>
> * <span data-ttu-id="28fc7-135">Compruebe todos los códigos de estado de respuesta para confirmar que se han producido errores en las llamadas API específicas que han tenido éxito con un código de Estado HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="28fc7-135">Check all of the response status codes to confirm that the specific API calls that succeeded have failed with an HTTP 403 status code.</span></span>

> [!div class="nextstepaction"]
>
> [<span data-ttu-id="28fc7-136">Más información: Microsoft Graph API y Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="28fc7-136">Learn more: Microsoft Graph API and Teams</span></span>](/graph/api/resources/teams-api-overview?view=graph-rest-1.0)


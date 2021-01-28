---
title: Preparar el espacio empresarial de Microsoft 365
description: Cómo empezar a trabajar con Teams en Microsoft 365
ms.topic: how-to
keywords: Configurar la carga de Microsoft 365 Tenant Teams
ms.openlocfilehash: bfeb1a5d39b8a6ad8d1dd4d631f984ecec4e26f1
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014456"
---
# <a name="prepare-your-microsoft-365-tenant"></a><span data-ttu-id="6a9ef-104">Preparar el espacio empresarial de Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="6a9ef-104">Prepare your Microsoft 365 tenant</span></span>

<span data-ttu-id="6a9ef-105">Si está suscrito a Microsoft 365, puede desarrollar aplicaciones para Microsoft Teams con uno de los siguientes [planes:](https://products.office.com/business/compare-more-office-365-for-business-plans)</span><span class="sxs-lookup"><span data-stu-id="6a9ef-105">If you are a Microsoft 365 subscriber, you can develop apps for Microsoft Teams with one of the following [plans](https://products.office.com/business/compare-more-office-365-for-business-plans):</span></span>

* <span data-ttu-id="6a9ef-106">Basic</span><span class="sxs-lookup"><span data-stu-id="6a9ef-106">Basic</span></span>
* <span data-ttu-id="6a9ef-107">Estándar</span><span class="sxs-lookup"><span data-stu-id="6a9ef-107">Standard</span></span>
* <span data-ttu-id="6a9ef-108">Enterprise E1, E3 y E5</span><span class="sxs-lookup"><span data-stu-id="6a9ef-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="6a9ef-109">Developer</span><span class="sxs-lookup"><span data-stu-id="6a9ef-109">Developer</span></span>
* <span data-ttu-id="6a9ef-110">Education, Education Plus y Education E5</span><span class="sxs-lookup"><span data-stu-id="6a9ef-110">Education, Education Plus, and Education E5</span></span>

<span data-ttu-id="6a9ef-111">Microsoft Teams también estará disponible para los clientes que se suscriban a E4 antes de su [retirada.](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)</span><span class="sxs-lookup"><span data-stu-id="6a9ef-111">Microsoft Teams will also be available to customers who subscribed to E4 prior to its [retirement](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span></span>

## <a name="just-need-a-development-environment"></a><span data-ttu-id="6a9ef-112">¿Solo necesita un entorno de desarrollo?</span><span class="sxs-lookup"><span data-stu-id="6a9ef-112">Just need a development environment?</span></span>

<span data-ttu-id="6a9ef-113">Si actualmente no tiene una cuenta de Microsoft 365, puede registrarse para obtener una suscripción al Programa de desarrolladores de [Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="6a9ef-113">If you don't currently have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="6a9ef-114">Es gratuito *durante* 90 días y se renovará continuamente siempre que lo use para la actividad de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-114">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="6a9ef-115">Si tiene una suscripción a Visual Studio *Enterprise* o *Professional,* ambos programas incluyen una suscripción gratuita de desarrollador de Microsoft 365, activa durante el período de vida de su Visual Studio suscripción. [](https://aka.ms/MyVisualStudioBenefits)</span><span class="sxs-lookup"><span data-stu-id="6a9ef-115">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="6a9ef-116">*Consulte* [Configurar una suscripción de desarrollador de Microsoft 365.](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)</span><span class="sxs-lookup"><span data-stu-id="6a9ef-116">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>

## <a name="enable-microsoft-teams-for-your-organization"></a><span data-ttu-id="6a9ef-117">Habilitar Microsoft Teams para su organización</span><span class="sxs-lookup"><span data-stu-id="6a9ef-117">Enable Microsoft Teams for your organization</span></span> 

<span data-ttu-id="6a9ef-118">Si Microsoft Teams no se ha habilitado para su organización, primero tendrá que hacerlo.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-118">If Microsoft Teams has not been enabled for your organization, you'll need to do that first.</span></span> <span data-ttu-id="6a9ef-119">Echa un vistazo a nuestras instrucciones detalladas para [habilitar Teams para tu organización.](/microsoftteams/enable-features-office-365)</span><span class="sxs-lookup"><span data-stu-id="6a9ef-119">Take a look at our detailed guidance for [enabling Teams for your organization](/microsoftteams/enable-features-office-365).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="6a9ef-120">Habilitar aplicaciones personalizadas de Teams y activar la carga de aplicaciones personalizadas</span><span class="sxs-lookup"><span data-stu-id="6a9ef-120">Enable custom Teams apps and turn on custom app uploading</span></span>

<span data-ttu-id="6a9ef-121">Active la instalación de instalación local de aplicaciones personalizadas para su inquilino de desarrollador de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="6a9ef-121">Turn on custom app sideloading for your developer tenant as follows:</span></span>

1. <span data-ttu-id="6a9ef-122">Inicie sesión en el Centro de administración de [Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) con su credencial de administrador.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-122">Login to [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credential.</span></span> 

2. <span data-ttu-id="6a9ef-123">Seleccione **Mostrar todos los**  -->  **equipos.**</span><span class="sxs-lookup"><span data-stu-id="6a9ef-123">Select **Show All** --> **Teams**.</span></span> 

![imagen del menú del centro de administración](~/assets/images/prepare-test-tenant/admin-center.png)

> [!Note] 
> <span data-ttu-id="6a9ef-125">La opción "Teams" puede tardar hasta 24 horas en aparecer.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-125">It can take up to 24 hours for the "Teams" option to appear.</span></span> <span data-ttu-id="6a9ef-126">Durante la fase provisional, puede [cargar la aplicación personalizada en un entorno de Teams](/microsoftteams/upload-custom-apps#validate) para pruebas y validación.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-126">During interim, you can [Upload your custom app to a Teams environment](/microsoftteams/upload-custom-apps#validate) for testing and validation.</span></span>

3. <span data-ttu-id="6a9ef-127">Navegar a las **directivas de configuración** de aplicaciones de Teams global  -->    -->  **(configuración predeterminada para toda la organización)**</span><span class="sxs-lookup"><span data-stu-id="6a9ef-127">Navigate to **Teams apps** --> **Setup Policies** --> **Global(Org-wide default)**</span></span>  

![activar la vista de instalación de instalación de instalación de local](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. <span data-ttu-id="6a9ef-129">Alterna **la carga de aplicaciones personalizadas** en la **posición** de posición.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-129">Toggle **upload custom apps** to the **on** position.</span></span>

<span data-ttu-id="6a9ef-130">Y eso es todo.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-130">That's it!</span></span> <span data-ttu-id="6a9ef-131">El inquilino de prueba ahora permitirá la instalación de prueba de aplicaciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-131">Your test tenant will now allow custom app sideloading.</span></span>

> [!Note] 
> <span data-ttu-id="6a9ef-132">La instalación de instalación local puede tardar hasta 24 horas en habilitarse.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-132">It can take up to 24 hours before sideloading is enabled.</span></span> <span data-ttu-id="6a9ef-133">Durante el período provisional, puedes usar **la carga para probar \<your tenant>** la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-133">During interim, you can use **upload for \<your tenant>** to test your app.</span></span>

![vista de aplicación updload](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

<span data-ttu-id="6a9ef-135">Para obtener información completa sobre cómo interactúan estas opciones *de* configuración, vea , Administrar directivas y configuraciones de aplicaciones personalizadas en [Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) y Administrar directivas de configuración de aplicaciones en [Microsoft Teams.](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)</span><span class="sxs-lookup"><span data-stu-id="6a9ef-135">For complete information on how these settings interact, *See*, [Manage custom app policies and settings in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) and [Manage app setup policies in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span></span>

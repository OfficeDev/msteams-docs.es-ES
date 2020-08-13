---
title: Preparar el entorno de desarrollo de Microsoft Teams
description: Cómo configurar el entorno para desarrollar aplicaciones de Teams
keywords: Configurar los equipos del inquilino de Office 365 para cargar el desarrollo del entorno
ms.openlocfilehash: 701c6c110026007cf1670e783348bbdbe1aff498
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652201"
---
# <a name="prepare-your-development-environment"></a><span data-ttu-id="cfd58-104">Preparar el entorno de desarrollo</span><span class="sxs-lookup"><span data-stu-id="cfd58-104">Prepare your development environment</span></span>

<span data-ttu-id="cfd58-105">Si es suscriptor de Office 365, puede desarrollar aplicaciones para Microsoft Teams con uno de los siguientes [planes](https://products.office.com/business/compare-more-office-365-for-business-plans):</span><span class="sxs-lookup"><span data-stu-id="cfd58-105">If you are an Office 365 subscriber, you can develop apps for Microsoft Teams with one of the following [plans](https://products.office.com/business/compare-more-office-365-for-business-plans):</span></span>

* <span data-ttu-id="cfd58-106">Empresa Essentials</span><span class="sxs-lookup"><span data-stu-id="cfd58-106">Business Essentials</span></span>
* <span data-ttu-id="cfd58-107">Empresa Premium</span><span class="sxs-lookup"><span data-stu-id="cfd58-107">Business Premium</span></span>
* <span data-ttu-id="cfd58-108">Enterprise E1, E3 y E5</span><span class="sxs-lookup"><span data-stu-id="cfd58-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="cfd58-109">Developer</span><span class="sxs-lookup"><span data-stu-id="cfd58-109">Developer</span></span>
* <span data-ttu-id="cfd58-110">Educación, educación Plus y educación E5</span><span class="sxs-lookup"><span data-stu-id="cfd58-110">Education, Education Plus, and Education E5</span></span>

<span data-ttu-id="cfd58-111">Microsoft Teams también estará disponible para los clientes que se suscribieron a E4 antes de su [jubilación](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span><span class="sxs-lookup"><span data-stu-id="cfd58-111">Microsoft Teams will also be available to customers who subscribed to E4 prior to its [retirement](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span></span>

## <a name="just-need-a-development-environment"></a><span data-ttu-id="cfd58-112">¿Solo necesita un entorno de desarrollo?</span><span class="sxs-lookup"><span data-stu-id="cfd58-112">Just need a development environment?</span></span>

<span data-ttu-id="cfd58-113">Si actualmente no tiene una cuenta de Office 365, puede registrarse para obtener una suscripción al [programa de desarrolladores de Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program) .</span><span class="sxs-lookup"><span data-stu-id="cfd58-113">If you don't currently have an Office 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="cfd58-114">Es *gratuita* durante 90 días y se renovará continuamente siempre que la use para la actividad de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="cfd58-114">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="cfd58-115">Si tiene una suscripción de Visual Studio *Enterprise* o *Professional* , ambos programas incluyen una suscripción gratuita al [desarrollador](https://aka.ms/MyVisualStudioBenefits)de Microsoft 365, activa durante la vida de su suscripción a Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cfd58-115">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="cfd58-116">*Consulte* [configurar una suscripción de desarrollador de Microsoft 365](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span><span class="sxs-lookup"><span data-stu-id="cfd58-116">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>

## <a name="enable-microsoft-teams-for-your-organization"></a><span data-ttu-id="cfd58-117">Habilitación de Microsoft Teams para la organización</span><span class="sxs-lookup"><span data-stu-id="cfd58-117">Enable Microsoft Teams for your organization</span></span>

<span data-ttu-id="cfd58-118">Si Microsoft Teams no se ha habilitado para su organización, deberá hacerlo primero.</span><span class="sxs-lookup"><span data-stu-id="cfd58-118">If Microsoft Teams has not been enabled for your organization, you'll need to do that first.</span></span> <span data-ttu-id="cfd58-119">Eche un vistazo a nuestras instrucciones detalladas para [Habilitar Microsoft Teams en su organización](https://docs.microsoft.com/microsoftteams/enable-features-office-365).</span><span class="sxs-lookup"><span data-stu-id="cfd58-119">Take a look at our detailed guidance for [enabling Teams for your organization](https://docs.microsoft.com/microsoftteams/enable-features-office-365).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="cfd58-120">Habilitar las aplicaciones personalizadas de Teams y activar la carga de aplicaciones personalizadas</span><span class="sxs-lookup"><span data-stu-id="cfd58-120">Enable custom Teams apps and turn on custom app uploading</span></span>

<span data-ttu-id="cfd58-121">Active la transferencia local de aplicaciones personalizada para su inquilino de desarrollador de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="cfd58-121">Turn on custom app sideloading for your developer tenant as follows:</span></span>

1. <span data-ttu-id="cfd58-122">Inicie sesión en el [centro de administración de Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) con sus credenciales de administrador.</span><span class="sxs-lookup"><span data-stu-id="cfd58-122">Login to [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credential.</span></span> 

2. <span data-ttu-id="cfd58-123">Seleccione **Mostrar todos los**  -->  **equipos**.</span><span class="sxs-lookup"><span data-stu-id="cfd58-123">Select **Show All** --> **Teams**.</span></span> 

![imagen del menú de desbordamiento de la aplicación](~/assets/images/prepare-test-tenant/admin-center.png)

3. <span data-ttu-id="cfd58-125">Vaya a directivas de configuración global de aplicaciones de Microsoft **Teams**  -->  **Setup Policies**  -->  **(valor predeterminado para toda la organización)**</span><span class="sxs-lookup"><span data-stu-id="cfd58-125">Navigate to **Teams apps** --> **Setup Policies** --> **Global(Org-wide default)**</span></span>  

![imagen del menú de desbordamiento de la aplicación](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. <span data-ttu-id="cfd58-127">Alternar **cargar aplicaciones personalizadas** en la posición **activado** .</span><span class="sxs-lookup"><span data-stu-id="cfd58-127">Toggle **upload custom apps** to the **on** position.</span></span>

<span data-ttu-id="cfd58-128">Y eso es todo.</span><span class="sxs-lookup"><span data-stu-id="cfd58-128">That's it!</span></span> <span data-ttu-id="cfd58-129">El inquilino de prueba permitirá ahora la versión de prueba de aplicaciones personalizada.</span><span class="sxs-lookup"><span data-stu-id="cfd58-129">Your test tenant will now allow custom app sideloading.</span></span>

> [!Note] 
> <span data-ttu-id="cfd58-130">Puede tardar hasta 24 horas antes de que se habilite la transferencia local.</span><span class="sxs-lookup"><span data-stu-id="cfd58-130">It can take up to 24 hours before sideloading is enabled.</span></span> <span data-ttu-id="cfd58-131">Durante la versión provisional, puede usar **cargar \<your tenant> para** para probar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cfd58-131">During interim, you can use **upload for \<your tenant>** to test your app.</span></span>

![imagen del menú de desbordamiento de la aplicación](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

<span data-ttu-id="cfd58-133">Para obtener información completa sobre cómo interactúa esta configuración *See*, vea [Administrar directivas y configuraciones de aplicaciones personalizadas en Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) y [Administrar directivas de configuración de aplicaciones en Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span><span class="sxs-lookup"><span data-stu-id="cfd58-133">For complete information on how these settings interact, *See*, [Manage custom app policies and settings in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) and [Manage app setup policies in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span></span>
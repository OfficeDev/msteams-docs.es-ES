---
title: Preparar el inquilino de Office 365
description: Introducción a teams en Office 365
keywords: Configurar la carga de equipos del inquilino de Office 365
ms.openlocfilehash: 447968c9b56010e515fc1d1346eac4d8485c7f80
ms.sourcegitcommit: 7a2da3b65246a125d441a971e7e6a6418355adbe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2020
ms.locfileid: "46587782"
---
# <a name="prepare-your-office-365-tenant"></a><span data-ttu-id="606be-104">Preparar el inquilino de Office 365</span><span class="sxs-lookup"><span data-stu-id="606be-104">Prepare your Office 365 tenant</span></span>

<span data-ttu-id="606be-105">Si es suscriptor de Office 365, puede desarrollar aplicaciones para Microsoft Teams con uno de los siguientes [planes](https://products.office.com/business/compare-more-office-365-for-business-plans):</span><span class="sxs-lookup"><span data-stu-id="606be-105">If you are an Office 365 subscriber, you can develop apps for Microsoft Teams with one of the following [plans](https://products.office.com/business/compare-more-office-365-for-business-plans):</span></span>

* <span data-ttu-id="606be-106">Empresa Essentials</span><span class="sxs-lookup"><span data-stu-id="606be-106">Business Essentials</span></span>
* <span data-ttu-id="606be-107">Empresa Premium</span><span class="sxs-lookup"><span data-stu-id="606be-107">Business Premium</span></span>
* <span data-ttu-id="606be-108">Enterprise E1, E3 y E5</span><span class="sxs-lookup"><span data-stu-id="606be-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="606be-109">Developer</span><span class="sxs-lookup"><span data-stu-id="606be-109">Developer</span></span>
* <span data-ttu-id="606be-110">Educación, educación Plus y educación E5</span><span class="sxs-lookup"><span data-stu-id="606be-110">Education, Education Plus, and Education E5</span></span>

<span data-ttu-id="606be-111">Microsoft Teams también estará disponible para los clientes que se suscribieron a E4 antes de su [jubilación](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span><span class="sxs-lookup"><span data-stu-id="606be-111">Microsoft Teams will also be available to customers who subscribed to E4 prior to its [retirement](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span></span>

## <a name="just-need-a-development-environment"></a><span data-ttu-id="606be-112">¿Solo necesita un entorno de desarrollo?</span><span class="sxs-lookup"><span data-stu-id="606be-112">Just need a development environment?</span></span>

<span data-ttu-id="606be-113">Si actualmente no tiene una cuenta de Office 365, puede registrarse para obtener una suscripción al [programa de desarrolladores de Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program) .</span><span class="sxs-lookup"><span data-stu-id="606be-113">If you don't currently have an Office 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="606be-114">Es *gratuita* durante 90 días y se renovará continuamente siempre que la use para la actividad de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="606be-114">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="606be-115">Si tiene una suscripción de Visual Studio *Enterprise* o *Professional* , ambos programas incluyen una suscripción gratuita al [desarrollador](https://aka.ms/MyVisualStudioBenefits)de Microsoft 365, activa durante la vida de su suscripción a Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="606be-115">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="606be-116">*Consulte* [configurar una suscripción de desarrollador de Microsoft 365](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span><span class="sxs-lookup"><span data-stu-id="606be-116">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>

## <a name="enable-microsoft-teams-for-your-organization"></a><span data-ttu-id="606be-117">Habilitación de Microsoft Teams para la organización</span><span class="sxs-lookup"><span data-stu-id="606be-117">Enable Microsoft Teams for your organization</span></span>

<span data-ttu-id="606be-118">Si Microsoft Teams no se ha habilitado para su organización, deberá hacerlo primero.</span><span class="sxs-lookup"><span data-stu-id="606be-118">If Microsoft Teams has not been enabled for your organization, you'll need to do that first.</span></span> <span data-ttu-id="606be-119">Eche un vistazo a nuestras instrucciones detalladas para [Habilitar Microsoft Teams en su organización](https://docs.microsoft.com/microsoftteams/enable-features-office-365).</span><span class="sxs-lookup"><span data-stu-id="606be-119">Take a look at our detailed guidance for [enabling Teams for your organization](https://docs.microsoft.com/microsoftteams/enable-features-office-365).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="606be-120">Habilitar las aplicaciones personalizadas de Teams y activar la carga de aplicaciones personalizadas</span><span class="sxs-lookup"><span data-stu-id="606be-120">Enable custom Teams apps and turn on custom app uploading</span></span>

<span data-ttu-id="606be-121">Active la transferencia local de aplicaciones personalizada para su inquilino de desarrollador de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="606be-121">Turn on custom app sideloading for your developer tenant as follows:</span></span>

1. <span data-ttu-id="606be-122">Inicie sesión en el [centro de administración de Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) con sus credenciales de administrador.</span><span class="sxs-lookup"><span data-stu-id="606be-122">Login to [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credential.</span></span> 

2. <span data-ttu-id="606be-123">Seleccione **Mostrar todos los**  -->  **equipos**.</span><span class="sxs-lookup"><span data-stu-id="606be-123">Select **Show All** --> **Teams**.</span></span> 

![imagen del menú de desbordamiento de la aplicación](~/assets/images/prepare-test-tenant/admin-center.png)

3. <span data-ttu-id="606be-125">Vaya a directivas de configuración global de aplicaciones de Microsoft **Teams**  -->  **Setup Policies**  -->  **(valor predeterminado para toda la organización)**</span><span class="sxs-lookup"><span data-stu-id="606be-125">Navigate to **Teams apps** --> **Setup Policies** --> **Global(Org-wide default)**</span></span>  

![imagen del menú de desbordamiento de la aplicación](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. <span data-ttu-id="606be-127">Alternar **cargar aplicaciones personalizadas** en la posición **activado** .</span><span class="sxs-lookup"><span data-stu-id="606be-127">Toggle **upload custom apps** to the **on** position.</span></span>

<span data-ttu-id="606be-128">Y eso es todo.</span><span class="sxs-lookup"><span data-stu-id="606be-128">That's it!</span></span> <span data-ttu-id="606be-129">El inquilino de prueba permitirá ahora la versión de prueba de aplicaciones personalizada.</span><span class="sxs-lookup"><span data-stu-id="606be-129">Your test tenant will now allow custom app sideloading.</span></span>

> [!Note] 
> <span data-ttu-id="606be-130">Puede tardar hasta 24 horas antes de que se habilite la transferencia local.</span><span class="sxs-lookup"><span data-stu-id="606be-130">It can take up to 24 hours before sideloading is enabled.</span></span> <span data-ttu-id="606be-131">Durante la versión provisional, puede usar **cargar \<your tenant> para** para probar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="606be-131">During interim, you can use **upload for \<your tenant>** to test your app.</span></span>

![imagen del menú de desbordamiento de la aplicación](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

<span data-ttu-id="606be-133">Para obtener información completa sobre cómo interactúa esta configuración *See*, vea [Administrar directivas y configuraciones de aplicaciones personalizadas en Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) y [Administrar directivas de configuración de aplicaciones en Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span><span class="sxs-lookup"><span data-stu-id="606be-133">For complete information on how these settings interact, *See*, [Manage custom app policies and settings in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) and [Manage app setup policies in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span></span>

---
title: Preparar el inquilino de Office 365
description: Introducción a teams en Office 365
keywords: Configurar la carga de equipos del inquilino de Office 365
ms.openlocfilehash: 62cd640196631f50c72762253ff1bd75a143337d
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676074"
---
# <a name="prepare-your-office-365-tenant"></a><span data-ttu-id="687db-104">Preparar el inquilino de Office 365</span><span class="sxs-lookup"><span data-stu-id="687db-104">Prepare your Office 365 tenant</span></span>

<span data-ttu-id="687db-105">Para desarrollar aplicaciones para Microsoft Teams, debe ser un [cliente de Office 365 con uno de los siguientes planes](https://products.office.com/business/compare-more-office-365-for-business-plans).</span><span class="sxs-lookup"><span data-stu-id="687db-105">To develop apps for Microsoft Teams, you need to be an [Office 365 customer with one of the following plans](https://products.office.com/business/compare-more-office-365-for-business-plans).</span></span>

* <span data-ttu-id="687db-106">Empresa Essentials</span><span class="sxs-lookup"><span data-stu-id="687db-106">Business Essentials</span></span>
* <span data-ttu-id="687db-107">Empresa Premium</span><span class="sxs-lookup"><span data-stu-id="687db-107">Business Premium</span></span>
* <span data-ttu-id="687db-108">Enterprise E1, E3 y E5</span><span class="sxs-lookup"><span data-stu-id="687db-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="687db-109">Developer</span><span class="sxs-lookup"><span data-stu-id="687db-109">Developer</span></span>
* <span data-ttu-id="687db-110">Educación, educación Plus y educación E5</span><span class="sxs-lookup"><span data-stu-id="687db-110">Education, Education Plus, and Education E5</span></span>

<span data-ttu-id="687db-111">Microsoft Teams también estará disponible para los clientes que compraron el plan E4 antes de su jubilación.</span><span class="sxs-lookup"><span data-stu-id="687db-111">Microsoft Teams will also be available to customers who purchased E4 prior to its retirement.</span></span>

## <a name="just-need-a-development-environment"></a><span data-ttu-id="687db-112">¿Solo necesita un entorno de desarrollo?</span><span class="sxs-lookup"><span data-stu-id="687db-112">Just need a development environment?</span></span>

<span data-ttu-id="687db-113">Si actualmente no tiene una cuenta de Office 365, puede registrarse en el programa de [desarrolladores de office 365](https://dev.office.com/devprogram) para obtener un 90 días *gratuita* (se puede renovar mientras lo use para la actividad de desarrollo) Office 365 Developer tenant.</span><span class="sxs-lookup"><span data-stu-id="687db-113">If you don't currently have an Office 365 account, you can sign up for the [Office 365 Developer program](https://dev.office.com/devprogram) to get a *free* 90 days (can be renewed for as long as you're using it for development activity) Office 365 Developer Tenant.</span></span> <span data-ttu-id="687db-114">Esta cuenta solo puede usarse con fines de prueba.</span><span class="sxs-lookup"><span data-stu-id="687db-114">This account can only be used for testing purposes.</span></span> <span data-ttu-id="687db-115">Vea más información sobre [Cómo configurar las cuentas de prueba](https://support.office.com/article/Add-users-individually-or-in-bulk-to-Office-365-Admin-Help-1970f7d6-03b5-442f-b385-5880b9c256ec?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="687db-115">See more information on [setting up your test accounts](https://support.office.com/article/Add-users-individually-or-in-bulk-to-Office-365-Admin-Help-1970f7d6-03b5-442f-b385-5880b9c256ec?ui=en-US&rs=en-US&ad=US).</span></span>

## <a name="enable-microsoft-teams-for-your-organization"></a><span data-ttu-id="687db-116">Habilitación de Microsoft Teams para la organización</span><span class="sxs-lookup"><span data-stu-id="687db-116">Enable Microsoft Teams for your organization</span></span>

<span data-ttu-id="687db-117">Si Microsoft Teams todavía no está habilitado para su organización, deberá hacerlo primero.</span><span class="sxs-lookup"><span data-stu-id="687db-117">If Microsoft Teams is not yet enabled for your organization, you'll need to do that first.</span></span> <span data-ttu-id="687db-118">Eche un vistazo a nuestras instrucciones detalladas para [Habilitar Microsoft Teams en su organización](/microsoftteams/how-to-roll-out-teams).</span><span class="sxs-lookup"><span data-stu-id="687db-118">Take a look at our detailed guidance for [enabling Teams for your organization](/microsoftteams/how-to-roll-out-teams).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="687db-119">Habilitar las aplicaciones personalizadas de Teams y activar la carga de aplicaciones personalizadas</span><span class="sxs-lookup"><span data-stu-id="687db-119">Enable custom Teams apps and turn on custom app uploading</span></span>

> <span data-ttu-id="687db-120">Nota: Si está usando una organización de desarrolladores de O365 para compilar la aplicación, esta configuración ya debe estar configurada para permitirle crear, cargar y probar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="687db-120">Note: If you're using an O365 Developer Organization to build your app, these settings should already be configured to allow you to build, upload and test your app.</span></span>

<span data-ttu-id="687db-121">Hay tres opciones de configuración relacionadas con la habilitación de aplicaciones personalizadas y la carga de aplicaciones personalizadas:</span><span class="sxs-lookup"><span data-stu-id="687db-121">There are three settings involved in enabling custom apps and custom app uploading:</span></span>

* <span data-ttu-id="687db-122">**Configuración de aplicación personalizada para toda** la organización: esta opción habilita o deshabilita las aplicaciones personalizadas para su organización.</span><span class="sxs-lookup"><span data-stu-id="687db-122">**Org-wide custom app setting** - This setting either enables or disables custom apps for your organization.</span></span> <span data-ttu-id="687db-123">Debe estar activada.</span><span class="sxs-lookup"><span data-stu-id="687db-123">It needs to be on.</span></span> 
* <span data-ttu-id="687db-124">**Configuración de la aplicación personalizada del equipo** : esta configuración es para cada equipo individual dentro de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="687db-124">**Team custom app setting** - This setting is for each individual team inside Microsoft Teams.</span></span> <span data-ttu-id="687db-125">Si quiere instalar la aplicación para un equipo específico, esto tendrá que estar activado para ese equipo.</span><span class="sxs-lookup"><span data-stu-id="687db-125">If you want to install your app for a specific team, this will need to be on for that team.</span></span>
* <span data-ttu-id="687db-126">**Directiva de aplicación personalizada de usuario** : este conjunto de opciones controla los permisos de un usuario individual.</span><span class="sxs-lookup"><span data-stu-id="687db-126">**User custom app policy** - This set of settings controls the permissions for an individual user.</span></span> <span data-ttu-id="687db-127">Deberá habilitar esto para los usuarios que quiera que carguen aplicaciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="687db-127">You'll need to enable this for individuals you want to upload custom apps.</span></span>

<span data-ttu-id="687db-128">Para obtener información completa sobre cómo interactúa esta configuración [, vea Manage Custom App policies and Settings in Microsoft Teams](/MicrosoftTeams/teams-custom-app-policies-and-settings).</span><span class="sxs-lookup"><span data-stu-id="687db-128">For complete information on how these settings interact see [Manage custom app policies and settings in Microsoft Teams](/MicrosoftTeams/teams-custom-app-policies-and-settings).</span></span>

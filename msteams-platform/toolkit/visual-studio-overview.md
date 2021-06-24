---
title: Crear aplicaciones con el Teams Toolkit y Visual Studio
description: Introducción a la creación de excelentes aplicaciones personalizadas directamente Visual Studio con el Microsoft Teams Toolkit
keywords: Kit de herramientas de visual studio de teams
localization_priority: Normal
ms.topic: overview
ms.author: johmil
ms.openlocfilehash: 6a0f466ba0d95312695be8b5460fc949e3f70811
ms.sourcegitcommit: 4ac93d69927791a8ccf678ca5ee83e63b51566b4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/23/2021
ms.locfileid: "53095517"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="fbc49-104">Crear aplicaciones con el Teams Toolkit y Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fbc49-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="fbc49-105">El kit de herramientas de Microsoft Teams le permite crear aplicaciones personalizadas de Teams directamente desde el entorno de desarrollo integrado (IDE) de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fbc49-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="fbc49-106">El kit de herramientas de Microsoft Teams le orienta en el proceso y le ofrece todo lo que necesita para crear, depurar e iniciar su aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="fbc49-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbc49-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fbc49-107">Prerequisites</span></span>

1. <span data-ttu-id="fbc49-108">[Habilitar la vista previa del desarrollador](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).</span><span class="sxs-lookup"><span data-stu-id="fbc49-108">[Enable developer preview](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).</span></span>

2. <span data-ttu-id="fbc49-109">Asegúrese de que el **<span>ASP.NET</span> y el** módulo de desarrollo web se han agregado a la instancia Visual Studio web.</span><span class="sxs-lookup"><span data-stu-id="fbc49-109">Make sure that the **<span>ASP.NET</span> and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="fbc49-110">Para obtener más información, [vea Modify Visual Studio by adding or removing workloads and components](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="fbc49-110">For more information, see [Modify Visual Studio by adding or removing workloads and components](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true).</span></span>

![Módulo de asp.net Visual studio](../assets/images/visual-studio-web-dev-module.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="fbc49-112">Instale el Teams Toolkit</span><span class="sxs-lookup"><span data-stu-id="fbc49-112">Install the Teams Toolkit</span></span>

<span data-ttu-id="fbc49-113">El Microsoft Teams Toolkit para Visual Studio está disponible para su descarga desde [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit) o directamente desde el menú **Extensiones** de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fbc49-113">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="use-the-toolkit"></a><span data-ttu-id="fbc49-114">Usar el kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="fbc49-114">Use the toolkit</span></span>

- [<span data-ttu-id="fbc49-115">Configurar un nuevo proyecto</span><span class="sxs-lookup"><span data-stu-id="fbc49-115">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="fbc49-116">Configurar la aplicación</span><span class="sxs-lookup"><span data-stu-id="fbc49-116">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="fbc49-117">Ejecute la aplicación en Teams</span><span class="sxs-lookup"><span data-stu-id="fbc49-117">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="fbc49-118">Valide su aplicación</span><span class="sxs-lookup"><span data-stu-id="fbc49-118">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="fbc49-119">Publicar la aplicación</span><span class="sxs-lookup"><span data-stu-id="fbc49-119">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="fbc49-120">Configurar un nuevo proyecto Teams proyecto</span><span class="sxs-lookup"><span data-stu-id="fbc49-120">Set up a new Teams project</span></span>

1. <span data-ttu-id="fbc49-121">Inicie Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="fbc49-121">Launch Visual Studio 2019.</span></span>
2. <span data-ttu-id="fbc49-122">Seleccione **Crear un nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="fbc49-122">Select **Create a new project**.</span></span>
3. <span data-ttu-id="fbc49-123">Busque la **Microsoft Teams y** seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="fbc49-123">Search for **Microsoft Teams App** and select **Next**.</span></span>
4. <span data-ttu-id="fbc49-124">En Configure **your new project**, escriba el nombre **Project**, **Location** y **Solution name**.</span><span class="sxs-lookup"><span data-stu-id="fbc49-124">In the **Configure your new project**, enter the **Project name**, **Location**, and **Solution name**.</span></span>
5. <span data-ttu-id="fbc49-125">Selecciona **Siguiente** para escribir un nombre para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fbc49-125">Select **Next** to enter a name for the app.</span></span>
6. <span data-ttu-id="fbc49-126">En la pantalla Información adicional, escribe **un** nombre de aplicación y un nombre de **desarrollador** o compañía para tu Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="fbc49-126">In the Additional Information screen, enter an **Application Name** and **Developer or Company name** for your Teams app.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="fbc49-127">Configurar la aplicación</span><span class="sxs-lookup"><span data-stu-id="fbc49-127">Configure your app</span></span>

<span data-ttu-id="fbc49-128">En su núcleo, la aplicación Teams abarca tres componentes:</span><span class="sxs-lookup"><span data-stu-id="fbc49-128">At its core, the Teams app embraces three components:</span></span>

- <span data-ttu-id="fbc49-129">El Microsoft Teams (web, de escritorio o móvil) donde los usuarios interactúan con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fbc49-129">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
- <span data-ttu-id="fbc49-130">Un servidor que responde a las solicitudes de contenido que se muestran en Teams.</span><span class="sxs-lookup"><span data-stu-id="fbc49-130">A server that responds to requests for content displayed in Teams.</span></span> <span data-ttu-id="fbc49-131">Por ejemplo, contenido de pestaña HTML o una tarjeta adaptable de bot.</span><span class="sxs-lookup"><span data-stu-id="fbc49-131">For example, HTML tab content or a bot adaptive card.</span></span>
- <span data-ttu-id="fbc49-132">Un Teams de la aplicación consta de tres archivos:</span><span class="sxs-lookup"><span data-stu-id="fbc49-132">A Teams app package consists of three files:</span></span>

    > [!div class="checklist"]
    >
    > - <span data-ttu-id="fbc49-133">El manifest.jsen</span><span class="sxs-lookup"><span data-stu-id="fbc49-133">The manifest.json</span></span>
    > - <span data-ttu-id="fbc49-134">Icono [de color para](../resources/schema/manifest-schema.md#icons) que la aplicación se muestre en el catálogo de aplicaciones públicas u de la organización.</span><span class="sxs-lookup"><span data-stu-id="fbc49-134">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog.</span></span>
    > - <span data-ttu-id="fbc49-135">Icono [de esquema para](../resources/schema/manifest-schema.md#icons) mostrar en la barra Teams actividad.</span><span class="sxs-lookup"><span data-stu-id="fbc49-135">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="fbc49-136">Cuando se instala una aplicación, el cliente Teams analiza el archivo de manifiesto para determinar la información necesaria, como el nombre de la aplicación y la dirección URL donde se encuentran los servicios.</span><span class="sxs-lookup"><span data-stu-id="fbc49-136">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="fbc49-137">Si aún no lo ha hecho, debe iniciar sesión en su cuenta de Microsoft 365 para continuar con el proceso de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="fbc49-137">If you have not done so already, you must sign in to your Microsoft 365 account to continue with the development process.</span></span>
>
> <span data-ttu-id="fbc49-138">Si no tiene una cuenta Microsoft 365, puede registrarse para una suscripción Microsoft 365 [Programa para desarrolladores.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="fbc49-138">If you do not have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="fbc49-139">Es gratuito durante 90 días y se renueva siempre que lo use para la actividad de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="fbc49-139">It's free for 90 days and renews as long as you are using it for development activity.</span></span> <span data-ttu-id="fbc49-140">Si tiene una suscripción Visual Studio Enterprise o Professional, ambos programas incluyen una suscripción Microsoft 365 desarrollador [gratuita,](https://aka.ms/MyVisualStudioBenefits)activa durante la vida de su Visual Studio suscripción.</span><span class="sxs-lookup"><span data-stu-id="fbc49-140">If you have a Visual Studio Enterprise or Professional subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="fbc49-141">Para obtener más información, vea [Configurar una Microsoft 365 de desarrollador](/office/developer-program/office-365-developer-program-get-started).</span><span class="sxs-lookup"><span data-stu-id="fbc49-141">For more information, see [set up a Microsoft 365 developer subscription](/office/developer-program/office-365-developer-program-get-started).</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="fbc49-142">Pasos de la configuración </span><span class="sxs-lookup"><span data-stu-id="fbc49-142">Configuration steps</span></span>

1. <span data-ttu-id="fbc49-143">Para configurar la aplicación, selecciona el menú **Project > TeamsFx > Configurar para SSO....**</span><span class="sxs-lookup"><span data-stu-id="fbc49-143">To configure your app, select the **Project > TeamsFx > Configure for SSO...** menu.</span></span>

<span data-ttu-id="fbc49-144">Cuando se le pida, inicie sesión en su cuenta microsoft que tenga un inquilino M365.</span><span class="sxs-lookup"><span data-stu-id="fbc49-144">When prompted, sign in to your Microsoft account that has an M365 tenant.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="fbc49-145">Instalar y ejecutar la aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="fbc49-145">Install and run your app locally</span></span>

<span data-ttu-id="fbc49-146">Presione F5 para iniciar la depuración.</span><span class="sxs-lookup"><span data-stu-id="fbc49-146">Press F5 to start debugging.</span></span> <span data-ttu-id="fbc49-147">El cuadro de diálogo de instalación de la aplicación aparece en el Teams cliente.</span><span class="sxs-lookup"><span data-stu-id="fbc49-147">The app installation dialog box appears in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="fbc49-148">Valide su aplicación</span><span class="sxs-lookup"><span data-stu-id="fbc49-148">Validate your app</span></span>

<span data-ttu-id="fbc49-149">El **Project > TeamsFx Validate > Teams manifest** permite comprobar que el paquete de la aplicación es válido.</span><span class="sxs-lookup"><span data-stu-id="fbc49-149">The **Project > TeamsFx Validate > Teams Manifest** menu allows you to check that your app package is valid.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="fbc49-150">Publicar la aplicación en Teams</span><span class="sxs-lookup"><span data-stu-id="fbc49-150">Publish your app to Teams</span></span>

<span data-ttu-id="fbc49-151">En el Portal de desarrolladores de [Teams,](https://dev.teams.microsoft.com/home)puedes cargar la aplicación en un equipo, enviar la aplicación a la tienda de aplicaciones personalizada de tu empresa para los usuarios de tu organización o enviar la aplicación a App Source para todos los usuarios Teams usuario.</span><span class="sxs-lookup"><span data-stu-id="fbc49-151">In the [Teams Developer Portal](https://dev.teams.microsoft.com/home), you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

- <span data-ttu-id="fbc49-152">El administrador de TI revisará estas entregas.</span><span class="sxs-lookup"><span data-stu-id="fbc49-152">Your IT admin will review these submissions.</span></span>
- <span data-ttu-id="fbc49-153">Puedes volver a la **página Publicar** para comprobar el estado del envío y saber si tu administrador de TI aprobó o rechazó la aplicación. Aquí también puedes enviar actualizaciones a la aplicación o cancelar cualquier envío activo actualmente.</span><span class="sxs-lookup"><span data-stu-id="fbc49-153">You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you can submit updates to your app or cancel any currently active submissions.</span></span>

## <a name="next-step"></a><span data-ttu-id="fbc49-154">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="fbc49-154">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fbc49-155">Crear y ejecutar la primera aplicación Microsoft Teams con Blazor</span><span class="sxs-lookup"><span data-stu-id="fbc49-155">Build and run your first Microsoft Teams app with Blazor</span></span>](../get-started/first-app-blazor.md)

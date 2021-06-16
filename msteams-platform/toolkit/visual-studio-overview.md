---
title: Crear aplicaciones con el Teams Toolkit y Visual Studio
description: Introducción a la creación de excelentes aplicaciones personalizadas directamente Visual Studio con el Microsoft Teams Toolkit
keywords: Kit de herramientas de visual studio de teams
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 996037f5bb1caaa2493e1eebe51039724822fef9
ms.sourcegitcommit: 9f499908437655d6ebdc6c4b3c3603ee220315b7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2021
ms.locfileid: "52949719"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="644fe-104">Crear aplicaciones con el Teams Toolkit y Visual Studio</span><span class="sxs-lookup"><span data-stu-id="644fe-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="644fe-105">El kit de herramientas de Microsoft Teams le permite crear aplicaciones personalizadas de Teams directamente desde el entorno de desarrollo integrado (IDE) de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="644fe-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="644fe-106">El kit de herramientas de Microsoft Teams le orienta en el proceso y le ofrece todo lo que necesita para crear, depurar e iniciar su aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="644fe-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="644fe-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="644fe-107">Prerequisites</span></span>

1. <span data-ttu-id="644fe-108">[Habilitar la vista previa del desarrollador](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).</span><span class="sxs-lookup"><span data-stu-id="644fe-108">[Enable developer preview](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).</span></span>

1. <span data-ttu-id="644fe-109">Asegúrese de que el **<span>ASP.NE</span>T y el** módulo de desarrollo web se han agregado a la instancia Visual Studio web.</span><span class="sxs-lookup"><span data-stu-id="644fe-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="644fe-110">Puede comprobar si sigue los pasos de la Visual Studio [agregando o](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) quitando cargas de trabajo y documentación de componentes.</span><span class="sxs-lookup"><span data-stu-id="644fe-110">You can check by following the steps in the [modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentation.</span></span>

![Módulo de asp.net Visual studio](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="644fe-112">Si quieres probar la aplicación implementandola desde Visual Studio, debes tener Servicios de Internet Information Server (IIS)) instalado en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="644fe-112">If you want to test your app by deploying it from Visual Studio, you must have Internet Information Services (IIS)) installed in your development environment.</span></span> <span data-ttu-id="644fe-113">Visual Studio no incluye IIS y no se incluye en la configuración predeterminada Windows 10, Windows 8 o Windows 7; sin embargo, puede descargar la versión más reciente del Centro [de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=48264).</span><span class="sxs-lookup"><span data-stu-id="644fe-113">Visual Studio does not include IIS and it is not included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![Vista de página de descarga de IIS](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="644fe-115">Instale el Teams Toolkit</span><span class="sxs-lookup"><span data-stu-id="644fe-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="644fe-116">El Microsoft Teams Toolkit para Visual Studio está disponible para su descarga desde [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) o directamente desde el menú **Extensiones** de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="644fe-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span> <span data-ttu-id="644fe-117">Desde el Visual Studio Marketplace también descargar [Teams Toolkit para Visual Studio 2019](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit).</span><span class="sxs-lookup"><span data-stu-id="644fe-117">From the Visual Studio Marketplace also download [Teams Toolkit for Visual Studio 2019](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit).</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="644fe-118">Uso del kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="644fe-118">Using the toolkit</span></span>

- [<span data-ttu-id="644fe-119">Configurar un nuevo proyecto</span><span class="sxs-lookup"><span data-stu-id="644fe-119">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="644fe-120">Configurar la aplicación</span><span class="sxs-lookup"><span data-stu-id="644fe-120">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="644fe-121">Empaquetar la aplicación</span><span class="sxs-lookup"><span data-stu-id="644fe-121">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="644fe-122">Instalar y ejecutar la aplicación en Teams</span><span class="sxs-lookup"><span data-stu-id="644fe-122">Install and run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="644fe-123">Valide su aplicación</span><span class="sxs-lookup"><span data-stu-id="644fe-123">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="644fe-124">Publicar la aplicación</span><span class="sxs-lookup"><span data-stu-id="644fe-124">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="644fe-125">Configurar un nuevo proyecto Teams proyecto</span><span class="sxs-lookup"><span data-stu-id="644fe-125">Set up a new Teams project</span></span>

![Teams kit de herramientas instalado](../assets/images/teamstoolkiticon.png)

1. <span data-ttu-id="644fe-127">Seleccione **Crear nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="644fe-127">Select **Create New Project**.</span></span>

    ![Crear un nuevo proyecto](../assets/images/createnewproject.png)

1. <span data-ttu-id="644fe-129">Elija la herramienta de inicio rápido **para Microsoft Teams app** y seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="644fe-129">Choose the quickstart tool for **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="644fe-130">En la **página Configurar el nuevo** proyecto, escriba el nombre **Project**, **Ubicación** y Nombre de **la solución**.</span><span class="sxs-lookup"><span data-stu-id="644fe-130">In the **Configure your new project** page, enter the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="644fe-131">Active la **casilla Colocar solución y proyecto en el mismo directorio.**</span><span class="sxs-lookup"><span data-stu-id="644fe-131">Select the **Place solution and project in the same directory** checkbox.</span></span>
1. <span data-ttu-id="644fe-132">En la ventana emergente Agregar **capacidades,** elija una o más funciones para la configuración del proyecto.</span><span class="sxs-lookup"><span data-stu-id="644fe-132">In the **Add Capabilities** pop-up window, choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="644fe-133">Seleccione el **botón** Siguiente para completar el proceso de configuración.</span><span class="sxs-lookup"><span data-stu-id="644fe-133">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="644fe-134">En la **ventana** emergente Agregar capacidades, elija las propiedades de cada funcionalidad seleccionada.</span><span class="sxs-lookup"><span data-stu-id="644fe-134">In the **Add Capabilities** pop-up window, choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="644fe-135">Seleccione **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="644fe-135">Select **Finish**.</span></span> <span data-ttu-id="644fe-136">Se **muestra Microsoft Teams Toolkit** página de aterrizaje.</span><span class="sxs-lookup"><span data-stu-id="644fe-136">The **Microsoft Teams Toolkit** landing page is shown.</span></span>

    ![Teams de aterrizaje del kit de herramientas](../assets/images/Teamstoolkitpage.png)

## <a name="configure-your-app"></a><span data-ttu-id="644fe-138">Configurar la aplicación</span><span class="sxs-lookup"><span data-stu-id="644fe-138">Configure your app</span></span>

<span data-ttu-id="644fe-139">En su núcleo, la aplicación Teams abarca tres componentes:</span><span class="sxs-lookup"><span data-stu-id="644fe-139">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="644fe-140">El Microsoft Teams web, de escritorio o móvil, donde los usuarios interactúan con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="644fe-140">The Microsoft Teams client including web, desktop, or mobile, where users interact with your app.</span></span>
  1. <span data-ttu-id="644fe-141">Un servidor que responde a solicitudes de contenido que se muestra en Teams, por ejemplo, contenido de pestaña HTML o una tarjeta adaptable de bot.</span><span class="sxs-lookup"><span data-stu-id="644fe-141">A server that responds to requests for content that is displayed in Teams, for example, HTML tab content or a bot adaptive card.</span></span>
  1. <span data-ttu-id="644fe-142">Un Teams de la aplicación consta de tres archivos:</span><span class="sxs-lookup"><span data-stu-id="644fe-142">A Teams app package consists of three files:</span></span>

      - <span data-ttu-id="644fe-143">El manifest.jsen</span><span class="sxs-lookup"><span data-stu-id="644fe-143">The manifest.json</span></span>
      - <span data-ttu-id="644fe-144">Icono [de color para](../resources/schema/manifest-schema.md#icons) que la aplicación se muestre en el catálogo de aplicaciones públicas u de la organización.</span><span class="sxs-lookup"><span data-stu-id="644fe-144">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog.</span></span>
      - <span data-ttu-id="644fe-145">Icono [de esquema para](../resources/schema/manifest-schema.md#icons) mostrar en la barra Teams actividad.</span><span class="sxs-lookup"><span data-stu-id="644fe-145">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="644fe-146">Cuando se instala una aplicación, el cliente Teams analiza el archivo de manifiesto para determinar la información necesaria, como el nombre de la aplicación y la dirección URL donde se encuentran los servicios.</span><span class="sxs-lookup"><span data-stu-id="644fe-146">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="644fe-147">Si aún no lo ha hecho, debe iniciar sesión en su cuenta de Microsoft 365 para continuar con el proceso de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="644fe-147">If you have not done so already, you must sign in to your Microsoft 365 account to continue with the development process.</span></span>
>
> <span data-ttu-id="644fe-148">Si no tiene una cuenta Microsoft 365, puede registrarse para una suscripción Microsoft 365 [Programa para desarrolladores.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="644fe-148">If you do not have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="644fe-149">Es gratuito durante 90 días y se renueva siempre que lo use para la actividad de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="644fe-149">It's free for 90 days and renews as long as you are using it for development activity.</span></span> <span data-ttu-id="644fe-150">Si tiene una suscripción Visual Studio Enterprise o Professional, ambos programas incluyen una suscripción Microsoft 365 desarrollador [gratuita,](https://aka.ms/MyVisualStudioBenefits)activa durante la vida de su Visual Studio suscripción.</span><span class="sxs-lookup"><span data-stu-id="644fe-150">If you have a Visual Studio Enterprise or Professional subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="644fe-151">Para obtener más información, vea [Configurar una Microsoft 365 de desarrollador](/office/developer-program/office-365-developer-program-get-started).</span><span class="sxs-lookup"><span data-stu-id="644fe-151">For more information, see [set up a Microsoft 365 developer subscription](/office/developer-program/office-365-developer-program-get-started).</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="644fe-152">Pasos de la configuración </span><span class="sxs-lookup"><span data-stu-id="644fe-152">Configuration steps</span></span>

1. <span data-ttu-id="644fe-153">Para configurar la aplicación, en la **Microsoft Teams Toolkit** de aterrizaje, seleccione **Editar paquete de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="644fe-153">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package**.</span></span>
1. <span data-ttu-id="644fe-154">En el menú desplegable Mis **entornos,** seleccione **desarrollo**.</span><span class="sxs-lookup"><span data-stu-id="644fe-154">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="644fe-155">En la **página Detalles de** la aplicación, edite los campos de propiedad de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="644fe-155">In the **App details** page, edit your app's property fields.</span></span>
    
    <span data-ttu-id="644fe-156">La edición de los campos de la página detalles de la aplicación actualiza el contenido del archivo manifest.jsque se enviará como parte del paquete de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="644fe-156">Editing the fields in the App details page updates the contents of the manifest.json file that will ship as part of the app package.</span></span> <span data-ttu-id="644fe-157">Para obtener más información, [vea Teams Toolkit manifest](https://aka.ms/teams-toolkit-manifest).</span><span class="sxs-lookup"><span data-stu-id="644fe-157">For more information, see [Teams Toolkit manifest](https://aka.ms/teams-toolkit-manifest).</span></span>

## <a name="package-your-app"></a><span data-ttu-id="644fe-158">Empaquetar la aplicación</span><span class="sxs-lookup"><span data-stu-id="644fe-158">Package your app</span></span>

<span data-ttu-id="644fe-159">Al modificar la página de **detalles de** la aplicación o actualizar el manifiesto **o** los archivos **.env** de la carpeta  **.publish** de la aplicación, se generará automáticamente el **Development.zip** archivo.</span><span class="sxs-lookup"><span data-stu-id="644fe-159">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="644fe-160">El Development.zip incluye tres archivos obligatorios, el **manifest.jsy** [dos iconos.](../concepts/build-and-test/apps-package.md#app-icons)</span><span class="sxs-lookup"><span data-stu-id="644fe-160">The Development.zip file includes three required files, the **manifest.json** and [two icons](../concepts/build-and-test/apps-package.md#app-icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="644fe-161">Instalar y ejecutar la aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="644fe-161">Install and run your app locally</span></span>

1. <span data-ttu-id="644fe-162">En el **menú desplegable Configuraciones de solución,** seleccione **Implementar** como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="644fe-162">From the **Solution Configurations** dropdown menu, select **Deploy** as shown in the following image:</span></span>

    ![Menú Configuraciones de solución](../assets/images/solution-configurations.png)

1. <span data-ttu-id="644fe-164">Seleccione el **IIS Express + Teams** botón.</span><span class="sxs-lookup"><span data-stu-id="644fe-164">Select the **IIS Express + Teams** button.</span></span>

    <span data-ttu-id="644fe-165">El cuadro de diálogo de instalación de la aplicación aparece en el Teams cliente.</span><span class="sxs-lookup"><span data-stu-id="644fe-165">The app installation dialog box appears in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="644fe-166">Valide su aplicación</span><span class="sxs-lookup"><span data-stu-id="644fe-166">Validate your app</span></span>

<span data-ttu-id="644fe-167">La **página Validar** te permite comprobar el paquete de la aplicación antes de enviar la aplicación a AppSource.</span><span class="sxs-lookup"><span data-stu-id="644fe-167">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="644fe-168">Simplemente cargue el paquete de manifiesto y la herramienta de validación comprobará la aplicación en todos los casos de prueba relacionados con el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="644fe-168">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="644fe-169">Para cada prueba con errores, la descripción proporciona un vínculo de documentación que le ayudará a corregir el error.</span><span class="sxs-lookup"><span data-stu-id="644fe-169">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="644fe-170">Para las pruebas difíciles de automatizar, la lista de comprobación **preliminar** detalla 7 de los casos de prueba con errores más comunes, así como un vínculo a una lista de comprobación de envío completa.</span><span class="sxs-lookup"><span data-stu-id="644fe-170">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="644fe-171">Publicar la aplicación en Teams</span><span class="sxs-lookup"><span data-stu-id="644fe-171">Publish your app to Teams</span></span>

* <span data-ttu-id="644fe-172">En la página principal del proyecto, puede cargar la aplicación a un equipo, enviarla a la tienda de aplicaciones personalizada de la organización para los usuarios de su organización o enviarla al origen de la aplicación para todos los usuarios de Teams.</span><span class="sxs-lookup"><span data-stu-id="644fe-172">On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

* <span data-ttu-id="644fe-173">El administrador de TI revisará estas entregas.</span><span class="sxs-lookup"><span data-stu-id="644fe-173">Your IT admin will review these submissions.</span></span>

* <span data-ttu-id="644fe-174">Puedes volver a la **página Publicar** para comprobar el estado del envío y saber si tu administrador de TI aprobó o rechazó la aplicación. Aquí también puedes enviar actualizaciones a la aplicación o cancelar cualquier envío activo actualmente.</span><span class="sxs-lookup"><span data-stu-id="644fe-174">You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you can submit updates to your app or cancel any currently active submissions.</span></span>

## <a name="next-step"></a><span data-ttu-id="644fe-175">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="644fe-175">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="644fe-176">Mantenimiento y soporte técnico de la aplicación publicada</span><span class="sxs-lookup"><span data-stu-id="644fe-176">Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>

---
title: Cree aplicaciones con el Microsoft Teams Toolkit y el Visual Studio
description: Comience a crear grandes aplicaciones personalizadas directamente dentro de Visual Studio con el Microsoft Teams Toolkit
keywords: equipo de herramientas de estudio visual
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: eb94a8de0355283344ebe890a6fa3a3050e243ea
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566554"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="22e2d-104">Cree aplicaciones con el Teams Toolkit y Visual Studio</span><span class="sxs-lookup"><span data-stu-id="22e2d-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="22e2d-105">El kit de herramientas de Microsoft Teams le permite crear aplicaciones personalizadas de Teams directamente desde el entorno de desarrollo integrado (IDE) de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="22e2d-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="22e2d-106">El kit de herramientas de Microsoft Teams le orienta en el proceso y le ofrece todo lo que necesita para crear, depurar e iniciar su aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="22e2d-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22e2d-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="22e2d-107">Prerequisites</span></span>

1. <span data-ttu-id="22e2d-108">[Habilite la vista previa del desarrollador.](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)</span><span class="sxs-lookup"><span data-stu-id="22e2d-108">[Enable developer preview](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).</span></span>

1. <span data-ttu-id="22e2d-109">Asegúrese de que el **<span>módulo de</span>desarrollo web y T de ASP.NE** se ha agregado a la instancia de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="22e2d-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="22e2d-110">Puede comprobar siguiendo los pasos descritos en la [Visual Studio Modificar agregando o quitando cargas de trabajo y](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentación de componentes.</span><span class="sxs-lookup"><span data-stu-id="22e2d-110">You can check by following the steps in the [Modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentation.</span></span>

![módulo de asp.net de estudio visual](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="22e2d-112">Si desea probar la aplicación implementándola desde Visual Studio, deberá tener IIS (Internet Information Services) instalado en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="22e2d-112">If you would like test your app by deploying it from Visual Studio, you'll need to have IIS (Internet Information Services) installed in your development environment.</span></span> <span data-ttu-id="22e2d-113">Visual Studio no incluye IIS y no se incluye en la configuración predeterminada de Windows 10, Windows 8 o Windows 7; sin embargo, puede descargar la última versión desde el Centro de [descarga de Microsoft.](https://www.microsoft.com/download/details.aspx?id=48264)</span><span class="sxs-lookup"><span data-stu-id="22e2d-113">Visual Studio does not include IIS and it isn't included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![Vista de página de descarga de IIS](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="22e2d-115">Instale la Teams Toolkit</span><span class="sxs-lookup"><span data-stu-id="22e2d-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="22e2d-116">El Microsoft Teams Toolkit para Visual Studio está disponible para su descarga desde [el Marketplace de Visual Studio](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) o directamente desde el menú **Extensiones** dentro de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="22e2d-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="22e2d-117">Uso del kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="22e2d-117">Using the toolkit</span></span>

- [<span data-ttu-id="22e2d-118">Establecer un nuevo proyecto</span><span class="sxs-lookup"><span data-stu-id="22e2d-118">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="22e2d-119">Configurar la aplicación</span><span class="sxs-lookup"><span data-stu-id="22e2d-119">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="22e2d-120">Empaqueta tu aplicación</span><span class="sxs-lookup"><span data-stu-id="22e2d-120">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="22e2d-121">Ejecute la aplicación en Teams</span><span class="sxs-lookup"><span data-stu-id="22e2d-121">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="22e2d-122">Valide su aplicación</span><span class="sxs-lookup"><span data-stu-id="22e2d-122">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="22e2d-123">Publicar la aplicación</span><span class="sxs-lookup"><span data-stu-id="22e2d-123">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="22e2d-124">Establecer un nuevo proyecto de Teams</span><span class="sxs-lookup"><span data-stu-id="22e2d-124">Set up a new Teams project</span></span>

1. <span data-ttu-id="22e2d-125">Seleccione **Crear un nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="22e2d-125">Select **Create a new project**.</span></span>
1. <span data-ttu-id="22e2d-126">Elija **Microsoft Teams App** y seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="22e2d-126">Choose **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="22e2d-127">Llegará a la pantalla **Configurar el nuevo proyecto** donde puede elegir el nombre **Project,** **ubicación** y nombre de **la solución.**</span><span class="sxs-lookup"><span data-stu-id="22e2d-127">You will arrive at the **Configure your new project** screen where you can choose the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="22e2d-128">Marque la casilla con la etiqueta **Colocar solución y proyecto en el mismo directorio**.</span><span class="sxs-lookup"><span data-stu-id="22e2d-128">Check the box labeled **Place solution and project in the same directory**.</span></span>
1. <span data-ttu-id="22e2d-129">Una ventana emergente con la etiqueta **Agregar capacidades** le permitirá elegir una o varias capacidades para la configuración del proyecto.</span><span class="sxs-lookup"><span data-stu-id="22e2d-129">A pop-up window labeled **Add Capabilities** will allow you to choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="22e2d-130">Seleccione el botón **Siguiente** para completar el proceso de configuración.</span><span class="sxs-lookup"><span data-stu-id="22e2d-130">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="22e2d-131">Una ventana emergente con la etiqueta **Agregar capacidades** le permitirá elegir las propiedades para cada capacidad seleccionada.</span><span class="sxs-lookup"><span data-stu-id="22e2d-131">A pop-up window labeled **Add Capabilities** will allow you to choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="22e2d-132">Seleccione **Finalizar** y aterrizará en la página de destino **Microsoft Teams Toolkit.**</span><span class="sxs-lookup"><span data-stu-id="22e2d-132">Select **Finish** and you will  land on the **Microsoft Teams Toolkit** landing page.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="22e2d-133">Configurar la aplicación</span><span class="sxs-lookup"><span data-stu-id="22e2d-133">Configure your app</span></span>

<span data-ttu-id="22e2d-134">En esencia, la aplicación Teams abarca tres componentes:</span><span class="sxs-lookup"><span data-stu-id="22e2d-134">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="22e2d-135">El cliente Microsoft Teams (web, de escritorio o móvil) donde los usuarios interactúan con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="22e2d-135">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="22e2d-136">Un servidor que responde a las solicitudes de contenido que se mostrarán en Teams, por ejemplo, contenido de la pestaña HTML o una tarjeta adaptable a bots.</span><span class="sxs-lookup"><span data-stu-id="22e2d-136">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="22e2d-137">Un paquete de Teams aplicación consta de tres archivos:</span><span class="sxs-lookup"><span data-stu-id="22e2d-137">A Teams app package consists of three files:</span></span>

      > [!div class="checklist"]
      >
      > - <span data-ttu-id="22e2d-138">El manifest.js</span><span class="sxs-lookup"><span data-stu-id="22e2d-138">The manifest.json</span></span>
      > - <span data-ttu-id="22e2d-139">Un [icono de color](../resources/schema/manifest-schema.md#icons) para que la aplicación se muestre en el catálogo de aplicaciones públicas u organizativas</span><span class="sxs-lookup"><span data-stu-id="22e2d-139">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
      > - <span data-ttu-id="22e2d-140">Icono [de contorno](../resources/schema/manifest-schema.md#icons) para mostrar en la barra de actividades Teams.</span><span class="sxs-lookup"><span data-stu-id="22e2d-140">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="22e2d-141">Cuando se instala una aplicación, el cliente Teams analiza el archivo de manifiesto para determinar la información necesaria, como el nombre de la aplicación y la dirección URL donde se encuentran los servicios.</span><span class="sxs-lookup"><span data-stu-id="22e2d-141">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="22e2d-142">Si aún no lo ha hecho, deberá iniciar sesión en su Microsoft 365 o cuenta para continuar con el proceso de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="22e2d-142">If you haven't done so already, you will need to sign in to your Microsoft 365  or account to continue with the development process.</span></span>
>
> <span data-ttu-id="22e2d-143">Si no tiene una cuenta Microsoft 365, puede registrarse para obtener una [suscripción Microsoft 365 Programa para desarrolladores.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="22e2d-143">If you don't have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="22e2d-144">Es *gratis* durante 90 días y se renovará continuamente siempre y cuando lo esté utilizando para la actividad de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="22e2d-144">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="22e2d-145">Si tienes una suscripción *Visual Studio Enterprise* o *Professional,* ambos programas incluyen una suscripción gratuita Microsoft 365 [para desarrolladores,](https://aka.ms/MyVisualStudioBenefits)activa durante toda la vida de tu suscripción Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="22e2d-145">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="22e2d-146">Para obtener más información, consulte [Configurar una suscripción Microsoft 365 desarrollador.](/office/developer-program/office-365-developer-program-get-started)</span><span class="sxs-lookup"><span data-stu-id="22e2d-146">For more information, See [Set up a Microsoft 365 developer subscription](/office/developer-program/office-365-developer-program-get-started).</span></span>
>

### <a name="configuration-steps"></a><span data-ttu-id="22e2d-147">Pasos de la configuración </span><span class="sxs-lookup"><span data-stu-id="22e2d-147">Configuration steps</span></span>

1. <span data-ttu-id="22e2d-148">Para configurar la aplicación, en la página de destino **Microsoft Teams Toolkit,** seleccione **Editar paquete de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="22e2d-148">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package**.</span></span>
1. <span data-ttu-id="22e2d-149">En el menú desplegable **Mis entornos,** seleccione **desarrollo.**</span><span class="sxs-lookup"><span data-stu-id="22e2d-149">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="22e2d-150">Aterrizarás en la página **detalles de** la aplicación donde puedes editar los campos de propiedades de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="22e2d-150">You will land on the **App details** page where you can edit your app's property fields.</span></span>
1. <span data-ttu-id="22e2d-151">La edición de los campos de la página Detalles de la aplicación actualiza el contenido de la manifest.jsen el archivo que, en última instancia, se enviará como parte del paquete de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="22e2d-151">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="22e2d-152">Más información</span><span class="sxs-lookup"><span data-stu-id="22e2d-152">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="22e2d-153">Empaqueta tu aplicación</span><span class="sxs-lookup"><span data-stu-id="22e2d-153">Package your app</span></span>

<span data-ttu-id="22e2d-154">La modificación de la página **de detalles** de la aplicación o la actualización de los archivos **de manifiesto** o **.env** en la carpeta **.publish** de la aplicación generará automáticamente el archivo **Development.zip.**</span><span class="sxs-lookup"><span data-stu-id="22e2d-154">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="22e2d-155">El archivo Development.zip incluye tres archivos necesarios: el **manifest.jsactivado** y [dos iconos.](../concepts/build-and-test/apps-package.md#app-icons)</span><span class="sxs-lookup"><span data-stu-id="22e2d-155">The Development.zip file includes three required files — the **manifest.json** and [two icons](../concepts/build-and-test/apps-package.md#app-icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="22e2d-156">Instale y ejecute la aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="22e2d-156">Install and run your app locally</span></span>

1. <span data-ttu-id="22e2d-157">En el menú desplegable **Configuraciones de soluciones,** seleccione **Implementar** como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="22e2d-157">From the **Solution Configurations** dropdown menu, select **Deploy** as shown in the following image:</span></span>

    ![Menú de configuraciones de soluciones](../assets/images/solution-configurations.png)

2. <span data-ttu-id="22e2d-159">Seleccione el botón **IIS Express + Teams.**</span><span class="sxs-lookup"><span data-stu-id="22e2d-159">Select the **IIS Express + Teams** button.</span></span>

1. <span data-ttu-id="22e2d-160">Teams se iniciará y el diálogo de instalación de la aplicación debe aparecer en el cliente Teams.</span><span class="sxs-lookup"><span data-stu-id="22e2d-160">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="22e2d-161">Valide su aplicación</span><span class="sxs-lookup"><span data-stu-id="22e2d-161">Validate your app</span></span>

<span data-ttu-id="22e2d-162">La página **Validar** le permite comprobar el paquete de la aplicación antes de enviar la aplicación a AppSource.</span><span class="sxs-lookup"><span data-stu-id="22e2d-162">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="22e2d-163">Simplemente cargue el paquete de manifiesto y la herramienta de validación comprobará su aplicación en todos los casos de prueba relacionados con el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="22e2d-163">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="22e2d-164">Para cada prueba con errores, la descripción proporciona un vínculo de documentación para ayudarle a corregir el error.</span><span class="sxs-lookup"><span data-stu-id="22e2d-164">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="22e2d-165">Para las pruebas que son difíciles de automatizar, la **lista de comprobación preliminar** detalla 7 de los casos de prueba fallidos más comunes, así como el enlace a una lista de comprobación de envío completa.</span><span class="sxs-lookup"><span data-stu-id="22e2d-165">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="22e2d-166">Publicar la aplicación en Teams</span><span class="sxs-lookup"><span data-stu-id="22e2d-166">Publish your app to Teams</span></span>

<span data-ttu-id="22e2d-167">✔ En la página principal del proyecto, puede cargar la aplicación en un equipo, enviar la aplicación a la tienda de aplicaciones personalizadas de su empresa para los usuarios de su organización o enviar la aplicación al origen de la aplicación para todos los usuarios Teams.</span><span class="sxs-lookup"><span data-stu-id="22e2d-167">✔ On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

<span data-ttu-id="22e2d-168">✔ su administrador de TI revisará estos envíos.</span><span class="sxs-lookup"><span data-stu-id="22e2d-168">✔ Your IT admin will review these submissions.</span></span>

<span data-ttu-id="22e2d-169">✔ Puede volver a la página **Publicar** para comprobar el estado de envío y obtener información sobre si la aplicación fue aprobada o rechazada por el administrador de TI. Aquí es también donde vendrás a enviar actualizaciones a tu aplicación o cancelar cualquier envío activo actualmente.</span><span class="sxs-lookup"><span data-stu-id="22e2d-169">✔  You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

## <a name="next-step"></a><span data-ttu-id="22e2d-170">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="22e2d-170">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="22e2d-171">Mantener y apoyar la aplicación publicada</span><span class="sxs-lookup"><span data-stu-id="22e2d-171">Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>

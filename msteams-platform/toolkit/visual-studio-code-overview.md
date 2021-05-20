---
title: Cree aplicaciones con el Microsoft Teams Toolkit y el Visual Studio Code
description: Comience a crear grandes aplicaciones personalizadas directamente dentro de Visual Studio Code con la Microsoft Teams Toolkit
keywords: equipos visual studio code toolkit
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: efd0962e9c4c0d64dbac47caf29b2e56907937b3
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566561"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a><span data-ttu-id="70390-104">Cree aplicaciones con el Teams Toolkit y Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="70390-104">Build apps with the Teams Toolkit and Visual Studio Code</span></span>

<span data-ttu-id="70390-105">El kit de herramientas de Microsoft Teams le permite crear aplicaciones personalizadas de Teams directamente desde el entorno de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="70390-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio Code environment.</span></span> <span data-ttu-id="70390-106">El kit de herramientas le orienta en el proceso y le ofrece todo lo que necesita para crear, depurar e iniciar su aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="70390-106">The toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="installing-the-teams-toolkit"></a><span data-ttu-id="70390-107">Instalación de la Teams Toolkit</span><span class="sxs-lookup"><span data-stu-id="70390-107">Installing the Teams Toolkit</span></span>

<span data-ttu-id="70390-108">El Microsoft Teams Toolkit para Visual Studio Code está disponible para su descarga desde [el Mercado de Visual Studio](https://aka.ms/teams-toolkit) o directamente como una extensión dentro de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="70390-108">The Microsoft Teams Toolkit for Visual Studio Code is available for download from the [Visual Studio Marketplace](https://aka.ms/teams-toolkit) or directly as an extension within Visual Studio Code.</span></span>

> [!TIP]
> <span data-ttu-id="70390-109">Después de la instalación, debería ver la Teams Toolkit en la barra de actividades Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="70390-109">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="70390-110">Si no es así, haga clic con el botón derecho en la barra de actividades y seleccione **Microsoft Teams** para anclar el kit de herramientas para facilitar el acceso.</span><span class="sxs-lookup"><span data-stu-id="70390-110">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="70390-111">Uso del kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="70390-111">Using the toolkit</span></span>

- [<span data-ttu-id="70390-112">Establecer un nuevo proyecto</span><span class="sxs-lookup"><span data-stu-id="70390-112">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="70390-113">Importar un proyecto existente</span><span class="sxs-lookup"><span data-stu-id="70390-113">Import an existing project</span></span>](#import-an-existing-teams-app-project)
- [<span data-ttu-id="70390-114">Configurar la aplicación</span><span class="sxs-lookup"><span data-stu-id="70390-114">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="70390-115">Empaqueta tu aplicación</span><span class="sxs-lookup"><span data-stu-id="70390-115">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="70390-116">Ejecute la aplicación localmente o en Teams</span><span class="sxs-lookup"><span data-stu-id="70390-116">Run your app locally or in Teams</span></span>](#run-your-app)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="70390-117">Establecer un nuevo proyecto de Teams</span><span class="sxs-lookup"><span data-stu-id="70390-117">Set up a new Teams project</span></span>

1. <span data-ttu-id="70390-118">Cree un área de trabajo o una carpeta para el proyecto en el entorno local.</span><span class="sxs-lookup"><span data-stu-id="70390-118">Create a workspace or folder for your project in your local environment.</span></span>
1. <span data-ttu-id="70390-119">En Visual Studio Code, seleccione el icono de Teams</span><span class="sxs-lookup"><span data-stu-id="70390-119">In Visual Studio Code, select the Teams icon</span></span> ![Icono de Teams](../assets/icons/favicon-16x16.png) <span data-ttu-id="70390-121">desde la barra de actividades en el lado izquierdo de la ventana.</span><span class="sxs-lookup"><span data-stu-id="70390-121">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="70390-122">Seleccione **Abrir el Microsoft Teams Toolkit** en el menú de comandos.</span><span class="sxs-lookup"><span data-stu-id="70390-122">Select **Open the Microsoft Teams Toolkit** from the command menu.</span></span>
1. <span data-ttu-id="70390-123">Seleccione **Crear una nueva aplicación de Teams** en el menú de comandos.</span><span class="sxs-lookup"><span data-stu-id="70390-123">Select **Create a new Teams app** from the command menu.</span></span>
1. <span data-ttu-id="70390-124">Cuando se le solicite, escriba el nombre del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="70390-124">When prompted, enter the name of the workspace .</span></span> <span data-ttu-id="70390-125">Esto se usará como el nombre de la carpeta donde residirá el proyecto y el nombre predeterminado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="70390-125">This will be used as both the name of the folder where your project will reside, and the default name of your app.</span></span>
1. <span data-ttu-id="70390-126">Pulse **Intro** y llegará a la pantalla **Agregar funcionalidades** para configurar las propiedades de la nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="70390-126">Press **Enter** and you will arrive at the **Add capabilities** screen configure the properties for your new app.</span></span>
1. <span data-ttu-id="70390-127">Seleccione el botón **Finalizar** para completar el proceso de configuración.</span><span class="sxs-lookup"><span data-stu-id="70390-127">Select the **Finish** button to complete the configuration process.</span></span>

## <a name="import-an-existing-teams-app-project"></a><span data-ttu-id="70390-128">Importar un proyecto de aplicación de Teams existente</span><span class="sxs-lookup"><span data-stu-id="70390-128">Import an existing Teams app project</span></span>

1. <span data-ttu-id="70390-129">En Visual Studio Code, seleccione el icono de Teams</span><span class="sxs-lookup"><span data-stu-id="70390-129">In Visual Studio Code, select the Teams icon</span></span> ![Icono de Teams](../assets/icons/favicon-16x16.png) <span data-ttu-id="70390-131">desde la barra de actividades en el lado izquierdo de la ventana.</span><span class="sxs-lookup"><span data-stu-id="70390-131">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="70390-132">Seleccione **Importar paquete** de aplicación en el menú de comandos.</span><span class="sxs-lookup"><span data-stu-id="70390-132">Select **Import app package** from the command menu.</span></span>
1. <span data-ttu-id="70390-133">Elija el archivo zip [del paquete de Teams aplicación](../concepts/build-and-test/apps-package.md) existente.</span><span class="sxs-lookup"><span data-stu-id="70390-133">Choose your existing [Teams app package](../concepts/build-and-test/apps-package.md) zip file.</span></span>
1. <span data-ttu-id="70390-134">Elija el botón **Seleccionar paquete de publicación.**</span><span class="sxs-lookup"><span data-stu-id="70390-134">Choose the **Select publishing package** button.</span></span> <span data-ttu-id="70390-135">La pestaña de configuración del kit de herramientas ahora debe rellenarse con los detalles de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="70390-135">The configuration tab of the toolkit should now be populated with your app's details.</span></span>
1. <span data-ttu-id="70390-136">En Visual Studio Code, seleccione   ->  **Agregar carpeta de archivos al área de trabajo** para agregar el directorio de código fuente al área de trabajo Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="70390-136">In Visual Studio Code, select **File** -> **Add Folder to Workspace** to add your source code directory to the Visual Studio Code workspace.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="70390-137">Configurar la aplicación</span><span class="sxs-lookup"><span data-stu-id="70390-137">Configure your app</span></span>

<span data-ttu-id="70390-138">En esencia, la aplicación Teams abarca tres componentes:</span><span class="sxs-lookup"><span data-stu-id="70390-138">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="70390-139">El cliente Microsoft Teams (web, de escritorio o móvil) donde los usuarios interactúan con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="70390-139">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="70390-140">Servidor que responde a las solicitudes de contenido que se mostrarán en Teams.</span><span class="sxs-lookup"><span data-stu-id="70390-140">A server that responds to requests for content that will be displayed in Teams.</span></span> <span data-ttu-id="70390-141">Por ejemplo, contenido de la pestaña HTML o una tarjeta adaptable a bots.</span><span class="sxs-lookup"><span data-stu-id="70390-141">For example, HTML tab content or a bot adaptive card.</span></span>
  1. <span data-ttu-id="70390-142">Un paquete de [aplicación](/concepts/build-and-test/apps-package.md) Teams que consta de tres archivos:</span><span class="sxs-lookup"><span data-stu-id="70390-142">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

      > [!div class="checklist"]
      >
      > - <span data-ttu-id="70390-143">El manifest.js.</span><span class="sxs-lookup"><span data-stu-id="70390-143">The manifest.json.</span></span> 
      > - <span data-ttu-id="70390-144">Icono [de color](../resources/schema/manifest-schema.md#icons) para que la aplicación se muestre en el catálogo de aplicaciones públicas u organizativas.</span><span class="sxs-lookup"><span data-stu-id="70390-144">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog.</span></span>
      > - <span data-ttu-id="70390-145">Icono [de contorno](../resources/schema/manifest-schema.md#icons) para mostrar en la barra de actividades Teams.</span><span class="sxs-lookup"><span data-stu-id="70390-145">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="70390-146">Cuando se instala una aplicación, el cliente Teams analiza el archivo de manifiesto para determinar la información necesaria, como el nombre de la aplicación y la dirección URL donde se encuentran los servicios.</span><span class="sxs-lookup"><span data-stu-id="70390-146">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="70390-147">Para configurar la aplicación, vaya a la pestaña **Microsoft Teams Toolkit** en Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="70390-147">To configure your app, navigate to the **Microsoft Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="70390-148">Seleccione **Editar paquete de aplicación** para ver la página Detalles de la **aplicación.**</span><span class="sxs-lookup"><span data-stu-id="70390-148">Select **Edit app package** to view the **App details** page.</span></span>
1. <span data-ttu-id="70390-149">La edición de los campos de la página Detalles de la aplicación actualiza el contenido de la manifest.jsen el archivo que, en última instancia, se enviará como parte del paquete de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="70390-149">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> <span data-ttu-id="70390-150">Para obtener más información, consulte [Editor de manifiestos de App Studio](https://aka.ms/teams-toolkit-manifest)</span><span class="sxs-lookup"><span data-stu-id="70390-150">For more information, See [App Studio manifest editor](https://aka.ms/teams-toolkit-manifest)</span></span>

## <a name="package-your-app"></a><span data-ttu-id="70390-151">Empaqueta tu aplicación</span><span class="sxs-lookup"><span data-stu-id="70390-151">Package your app</span></span>

<span data-ttu-id="70390-152">La modificación de la página de detalles de la **aplicación,** **el manifiesto** o los archivos **.env** en la carpeta **.publish** de la aplicación generará automáticamente el archivo **Development.zip.**</span><span class="sxs-lookup"><span data-stu-id="70390-152">Modifying the **app details** page, **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="70390-153">Deberá incluir dos [iconos](../concepts/build-and-test/apps-package.md#app-icons) en esa misma carpeta.</span><span class="sxs-lookup"><span data-stu-id="70390-153">You'll need to include [two icons](../concepts/build-and-test/apps-package.md#app-icons) in that same folder.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="70390-154">Instale y ejecute la aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="70390-154">Install and run your app locally</span></span>

## <a name="run-your-app"></a><span data-ttu-id="70390-155">Ejecute la aplicación</span><span class="sxs-lookup"><span data-stu-id="70390-155">Run your app</span></span>

### <a name="install-and-run-your-app-locally"></a><span data-ttu-id="70390-156">Instale y ejecute la aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="70390-156">Install and run your app locally</span></span>

<span data-ttu-id="70390-157">Consulte la página **principal Compilar y ejecutar** del proyecto para obtener instrucciones detalladas sobre cómo empaquetar y probar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="70390-157">Refer to the **Build and Run** content in your project homepage for detailed instructions on how to package and test your app.</span></span> <span data-ttu-id="70390-158">En general, debe instalar el servidor de la aplicación, ponerlo en ejecución y, a continuación, configurar una solución de tunelización para que Teams pueda acceder al contenido que se ejecuta desde localhost.</span><span class="sxs-lookup"><span data-stu-id="70390-158">In general, you need to install your app's server, get it running, then setup a tunneling solution so that Teams can access content running from localhost.</span></span>

### <a name="enable-development-from-localhost"></a><span data-ttu-id="70390-159">Habilitar el desarrollo desde localhost</span><span class="sxs-lookup"><span data-stu-id="70390-159">Enable development from localhost</span></span>

<span data-ttu-id="70390-160">Si desea depurar la aplicación basada en la pestaña en localhost mediante HTTPS, deberá indicar a su navegador que confíe en la aplicación desde la que se <https://localhost> sirve.</span><span class="sxs-lookup"><span data-stu-id="70390-160">If you wish to debug your tab based app on localhost using HTTPS, you will need to tell your browser to trust the app being served from <https://localhost>.</span></span> <span data-ttu-id="70390-161">Vaya a <https://localhost:3000/tab>.</span><span class="sxs-lookup"><span data-stu-id="70390-161">Navigate to <https://localhost:3000/tab>.</span></span> <span data-ttu-id="70390-162">Si ve una advertencia que indica que el sitio no es de confianza, elija la opción para continuar de todos modos.</span><span class="sxs-lookup"><span data-stu-id="70390-162">If you see a warning indicating that the site isn't trusted, choose the option to proceed anyway.</span></span> <span data-ttu-id="70390-163">La aplicación ahora debe ser accesible desde el cliente Teams.</span><span class="sxs-lookup"><span data-stu-id="70390-163">Your app should now be accessible from the Teams client.</span></span>

### <a name="run-your-app-in-teams"></a><span data-ttu-id="70390-164">Ejecute la aplicación en Teams</span><span class="sxs-lookup"><span data-stu-id="70390-164">Run your app in Teams</span></span>

<span data-ttu-id="70390-165">Requisitos previos: [habilite Teams modo de vista previa del desarrollador](https://aka.ms/teams-toolkit-enable-devpreview)</span><span class="sxs-lookup"><span data-stu-id="70390-165">Prerequisites: [Enable Teams developer preview mode](https://aka.ms/teams-toolkit-enable-devpreview)</span></span>

1. <span data-ttu-id="70390-166">Vaya a la barra de actividades en el lado izquierdo de la ventana de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="70390-166">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="70390-167">Seleccione el icono **Ejecutar** para mostrar la vista **Ejecutar y depurar.**</span><span class="sxs-lookup"><span data-stu-id="70390-167">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="70390-168">También puede utilizar el método abreviado de `Ctrl+Shift+D` teclado.</span><span class="sxs-lookup"><span data-stu-id="70390-168">You can also use the keyboard shortcut `Ctrl+Shift+D`.</span></span>

## <a name="next-step"></a><span data-ttu-id="70390-169">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="70390-169">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="70390-170">Mantener y apoyar la aplicación publicada</span><span class="sxs-lookup"><span data-stu-id="70390-170">Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)

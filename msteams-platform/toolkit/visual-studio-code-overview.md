---
title: Compilar aplicaciones con el kit de herramientas de Microsoft Teams y Visual Studio Code
description: Introducción a la creación de excelentes aplicaciones personalizadas directamente en Visual Studio Code con el kit de herramientas de Microsoft Teams
keywords: Teams Visual Studio Code Toolkit
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 350da030d15e72e2cad51c5967afab9b6f29fe9e
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604476"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a><span data-ttu-id="dbb94-104">Compilar aplicaciones con el kit de herramientas de Microsoft Teams y Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="dbb94-104">Build apps with the Teams Toolkit and Visual Studio Code</span></span>

<span data-ttu-id="dbb94-105">El kit de herramientas de Microsoft Teams le permite crear aplicaciones de Team personalizadas directamente en el entorno de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="dbb94-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio Code environment.</span></span> <span data-ttu-id="dbb94-106">El kit de herramientas le guiará por el proceso y le proporciona todo lo que necesita para crear, depurar e iniciar la aplicación de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="dbb94-106">The toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="installing-the-teams-toolkit"></a><span data-ttu-id="dbb94-107">Instalación de Team Toolkit</span><span class="sxs-lookup"><span data-stu-id="dbb94-107">Installing the Teams Toolkit</span></span>

<span data-ttu-id="dbb94-108">El kit de herramientas de Microsoft Teams para Visual Studio Code está disponible para su descarga desde [Visual Studio Marketplace](https://aka.ms/teams-toolkit) o directamente como una extensión de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="dbb94-108">The Microsoft Teams Toolkit for Visual Studio Code is available for download from the [Visual Studio Marketplace](https://aka.ms/teams-toolkit) or directly as an extension within Visual Studio Code.</span></span>

> [!TIP]
> <span data-ttu-id="dbb94-109">Después de la instalación, debería ver Team Toolkit en la barra de actividad del código de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dbb94-109">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="dbb94-110">Si no es así, haga clic con el botón derecho en la barra de actividad y seleccione **Microsoft Teams** para anclar el kit de herramientas para facilitar el acceso.</span><span class="sxs-lookup"><span data-stu-id="dbb94-110">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="dbb94-111">Uso del kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="dbb94-111">Using the toolkit</span></span>

- [<span data-ttu-id="dbb94-112">Configurar un nuevo proyecto</span><span class="sxs-lookup"><span data-stu-id="dbb94-112">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="dbb94-113">Importar un proyecto existente</span><span class="sxs-lookup"><span data-stu-id="dbb94-113">Import an existing project</span></span>](#import-an-existing-teams-app-project)
- [<span data-ttu-id="dbb94-114">Configurar la aplicación</span><span class="sxs-lookup"><span data-stu-id="dbb94-114">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="dbb94-115">Empaquetar la aplicación</span><span class="sxs-lookup"><span data-stu-id="dbb94-115">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="dbb94-116">Ejecutar la aplicación de forma local o en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="dbb94-116">Run your app locally or in Teams</span></span>](#run-your-app)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="dbb94-117">Configurar un nuevo proyecto de Teams</span><span class="sxs-lookup"><span data-stu-id="dbb94-117">Set up a new Teams project</span></span>

1. <span data-ttu-id="dbb94-118">Cree un área de trabajo o una carpeta para el proyecto en su entorno local.</span><span class="sxs-lookup"><span data-stu-id="dbb94-118">Create a workspace/folder for your project in your local environment.</span></span>
1. <span data-ttu-id="dbb94-119">En Visual Studio Code, seleccione el icono de Teams</span><span class="sxs-lookup"><span data-stu-id="dbb94-119">In Visual Studio Code, select the Teams icon</span></span> ![Icono de Teams](../assets/icons/favicon-16x16.png) <span data-ttu-id="dbb94-121">en la barra de actividades del lado izquierdo de la ventana.</span><span class="sxs-lookup"><span data-stu-id="dbb94-121">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="dbb94-122">Seleccione **Abrir Microsoft Teams Toolkit** desde el menú de comandos.</span><span class="sxs-lookup"><span data-stu-id="dbb94-122">Select **Open the Microsoft Teams Toolkit** from the command menu.</span></span>
1. <span data-ttu-id="dbb94-123">Seleccione **crear una nueva aplicación de Teams** desde el menú de comandos.</span><span class="sxs-lookup"><span data-stu-id="dbb94-123">Select **Create a new Teams app** from the command menu.</span></span>
1. <span data-ttu-id="dbb94-124">Cuando se le solicite, escriba el nombre del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="dbb94-124">When prompted, enter the name of the workspace .</span></span> <span data-ttu-id="dbb94-125">Se usará como el nombre de la carpeta en la que residirá el proyecto y el nombre predeterminado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dbb94-125">This will be used as both the name of the folder where your project will reside, and the default name of your app.</span></span>
1. <span data-ttu-id="dbb94-126">Presione **entrar** para que llegue a la pantalla **Agregar funcionalidad** , configure las propiedades de la nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="dbb94-126">Press **Enter** and you will arrive at the **Add capabilities** screen configure the properties for your new app.</span></span>
1. <span data-ttu-id="dbb94-127">Seleccione el botón **Finalizar** para completar el proceso de configuración.</span><span class="sxs-lookup"><span data-stu-id="dbb94-127">Select the **Finish** button to complete the configuration process.</span></span>

## <a name="import-an-existing-teams-app-project"></a><span data-ttu-id="dbb94-128">Importar un proyecto de aplicación de Teams existente</span><span class="sxs-lookup"><span data-stu-id="dbb94-128">Import an existing Teams app project</span></span>

1. <span data-ttu-id="dbb94-129">En Visual Studio Code, seleccione el icono de Teams</span><span class="sxs-lookup"><span data-stu-id="dbb94-129">In Visual Studio Code, select the Teams icon</span></span> ![Icono de Teams](../assets/icons/favicon-16x16.png) <span data-ttu-id="dbb94-131">en la barra de actividades del lado izquierdo de la ventana.</span><span class="sxs-lookup"><span data-stu-id="dbb94-131">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="dbb94-132">Seleccione **importar paquete de aplicaciones** en el menú comando.</span><span class="sxs-lookup"><span data-stu-id="dbb94-132">Select **Import app package** from the command menu.</span></span>
1. <span data-ttu-id="dbb94-133">Elija el archivo zip del paquete de aplicaciones de Microsoft [Teams](../concepts/build-and-test/apps-package.md) existente.</span><span class="sxs-lookup"><span data-stu-id="dbb94-133">Choose your existing [Teams app package](../concepts/build-and-test/apps-package.md) zip file.</span></span>
1. <span data-ttu-id="dbb94-134">Elija el botón **seleccionar paquete de publicación** .</span><span class="sxs-lookup"><span data-stu-id="dbb94-134">Choose the **Select publishing package** button.</span></span> <span data-ttu-id="dbb94-135">La pestaña de configuración del kit de herramientas ahora debe rellenarse con los detalles de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dbb94-135">The configuration tab of the toolkit should now be populated with your app's details.</span></span>
1. <span data-ttu-id="dbb94-136">En Visual Studio Code, seleccione **archivo**  ->  **Agregar carpeta al área de trabajo** para agregar el directorio de código fuente al área de trabajo de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="dbb94-136">In Visual Studio Code, select **File** -> **Add Folder to Workspace** to add your source code directory to the Visual Studio Code workspace.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="dbb94-137">Configurar la aplicación</span><span class="sxs-lookup"><span data-stu-id="dbb94-137">Configure your app</span></span>

<span data-ttu-id="dbb94-138">En esencia, la aplicación de Microsoft Teams adopta tres componentes:</span><span class="sxs-lookup"><span data-stu-id="dbb94-138">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="dbb94-139">El cliente de Microsoft Teams (Web, escritorio o móvil) donde los usuarios interactúan con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dbb94-139">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="dbb94-140">Un servidor que responde a las solicitudes de contenido que se mostrarán en Microsoft Teams, por ejemplo, contenido de la ficha HTML o una tarjeta adaptable de bot.</span><span class="sxs-lookup"><span data-stu-id="dbb94-140">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="dbb94-141">Un paquete de la [aplicación](/concepts/build-and-test/apps-package.md) teams que consta de tres archivos:</span><span class="sxs-lookup"><span data-stu-id="dbb94-141">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="dbb94-142">La manifest.jsen</span><span class="sxs-lookup"><span data-stu-id="dbb94-142">The manifest.json</span></span> 
  > - <span data-ttu-id="dbb94-143">Un [icono de color](../resources/schema/manifest-schema.md#icons) de la aplicación para que se muestre en el catálogo de aplicaciones públicas o de la organización</span><span class="sxs-lookup"><span data-stu-id="dbb94-143">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="dbb94-144">Un [icono de esquema](../resources/schema/manifest-schema.md#icons) para mostrar en la barra de actividad de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="dbb94-144">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="dbb94-145">Cuando se instala una aplicación, el cliente de Microsoft Teams analiza el archivo de manifiesto para determinar la información necesaria, como el nombre de la aplicación y la dirección URL en la que se encuentran los servicios.</span><span class="sxs-lookup"><span data-stu-id="dbb94-145">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="dbb94-146">Para configurar la aplicación, navegue a la pestaña **Microsoft Team Toolkit** en Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="dbb94-146">To configure your app, navigate to the **Microsoft Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="dbb94-147">Seleccione **Editar paquete** de la aplicación para ver la página de detalles de la **aplicación** .</span><span class="sxs-lookup"><span data-stu-id="dbb94-147">Select **Edit app package** to view the **App details** page.</span></span>
1. <span data-ttu-id="dbb94-148">Al editar los campos en la página de detalles de la aplicación, se actualiza el contenido del manifest.jsen el archivo que se entregará como parte del paquete de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dbb94-148">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> <span data-ttu-id="dbb94-149">*Consulte* [Editor de manifiesto de App Studio](https://aka.ms/teams-toolkit-manifest)</span><span class="sxs-lookup"><span data-stu-id="dbb94-149">*See* [App Studio manifest editor](https://aka.ms/teams-toolkit-manifest)</span></span>

## <a name="package-your-app"></a><span data-ttu-id="dbb94-150">Empaquetar la aplicación</span><span class="sxs-lookup"><span data-stu-id="dbb94-150">Package your app</span></span>

<span data-ttu-id="dbb94-151">Al modificar la página de detalles de la **aplicación** , el **manifiesto** o los archivos **. env** en la carpeta  **. Publish** de la aplicación, se generará automáticamente el archivo de **Development.zip** .</span><span class="sxs-lookup"><span data-stu-id="dbb94-151">Modifying the **app details** page, **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="dbb94-152">Deberá incluir [dos iconos](../concepts/build-and-test/apps-package.md#app-icons) en la misma carpeta.</span><span class="sxs-lookup"><span data-stu-id="dbb94-152">You'll need to include [two icons](../concepts/build-and-test/apps-package.md#app-icons) in that same folder.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="dbb94-153">Instalar y ejecutar la aplicación de forma local</span><span class="sxs-lookup"><span data-stu-id="dbb94-153">Install and run your app locally</span></span>

## <a name="run-your-app"></a><span data-ttu-id="dbb94-154">Ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="dbb94-154">Run your app</span></span>

### <a name="install-and-run-your-app-locally"></a><span data-ttu-id="dbb94-155">Instalar y ejecutar la aplicación de forma local</span><span class="sxs-lookup"><span data-stu-id="dbb94-155">Install and run your app locally</span></span>

<span data-ttu-id="dbb94-156">Para obtener instrucciones detalladas sobre cómo empaquetar y probar la aplicación, consulte la página de inicio *y ejecutar* contenido en la Página principal del proyecto.</span><span class="sxs-lookup"><span data-stu-id="dbb94-156">Refer to the \**Build and Run* content in your project homepage for detailed instructions on how to package and test your app.</span></span> <span data-ttu-id="dbb94-157">En general, debe instalar el servidor de la aplicación, ponerlo en ejecución y, a continuación, configurar una solución de tunelización para que Microsoft Teams pueda obtener acceso al contenido que se ejecuta desde localhost.</span><span class="sxs-lookup"><span data-stu-id="dbb94-157">In general, you need to install your app's server, get it running, then setup a tunneling solution so that Teams can access content running from localhost.</span></span>

### <a name="enable-development-from-localhost"></a><span data-ttu-id="dbb94-158">Habilitar el desarrollo desde localhost</span><span class="sxs-lookup"><span data-stu-id="dbb94-158">Enable development from localhost</span></span>

<span data-ttu-id="dbb94-159">Si desea depurar la aplicación basada en pestañas en localhost mediante HTTPS, tendrá que decirle al explorador que confíe en la aplicación a la que se atiende <https://localhost> .</span><span class="sxs-lookup"><span data-stu-id="dbb94-159">If you wish to debug your tab based app on localhost using HTTPS, you will need to tell your browser to trust the app being served from <https://localhost>.</span></span> <span data-ttu-id="dbb94-160">Vaya a <https://localhost:3000/tab>.</span><span class="sxs-lookup"><span data-stu-id="dbb94-160">Navigate to <https://localhost:3000/tab>.</span></span> <span data-ttu-id="dbb94-161">Si ve una advertencia que indica que el sitio no es de confianza, elija la opción para continuar de todos modos.</span><span class="sxs-lookup"><span data-stu-id="dbb94-161">If you see a warning indicating that the site isn't trusted, choose the option to proceed anyway.</span></span> <span data-ttu-id="dbb94-162">La aplicación ahora debería ser accesible desde el cliente de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="dbb94-162">Your app should now be accessible from the Teams client.</span></span>

### <a name="run-your-app-in-teams"></a><span data-ttu-id="dbb94-163">Ejecutar la aplicación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="dbb94-163">Run your app in Teams</span></span>

<span data-ttu-id="dbb94-164">Requisitos previos: [Habilitar el modo de vista previa para desarrolladores de Teams](https://aka.ms/teams-toolkit-enable-devpreview)</span><span class="sxs-lookup"><span data-stu-id="dbb94-164">Prerequisites: [Enable Teams developer preview mode](https://aka.ms/teams-toolkit-enable-devpreview)</span></span>

1. <span data-ttu-id="dbb94-165">Navegue a la barra de actividades en el lado izquierdo de la ventana de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="dbb94-165">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="dbb94-166">Seleccione el icono **Ejecutar** para mostrar la vista **Ejecutar y depurar** .</span><span class="sxs-lookup"><span data-stu-id="dbb94-166">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="dbb94-167">También puede usar el método abreviado de teclado `Ctrl+Shift+D` .</span><span class="sxs-lookup"><span data-stu-id="dbb94-167">You can also use the keyboard shortcut `Ctrl+Shift+D`.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dbb94-168">Siguiente paso: mantenimiento y soporte de la aplicación publicada</span><span class="sxs-lookup"><span data-stu-id="dbb94-168">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)

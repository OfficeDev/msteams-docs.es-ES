---
title: Crear aplicaciones con Microsoft Teams Toolkit y Visual Studio code
description: Introducción a la creación de excelentes aplicaciones personalizadas directamente en Visual Studio Code con Microsoft Teams Toolkit
keywords: Kit de herramientas de código visual studio de teams
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 59f2943f37856c42346b2ffad4e01d88910679ae
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020264"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a><span data-ttu-id="82631-104">Crear aplicaciones con Teams Toolkit y Visual Studio code</span><span class="sxs-lookup"><span data-stu-id="82631-104">Build apps with the Teams Toolkit and Visual Studio Code</span></span>

<span data-ttu-id="82631-105">El kit de herramientas de Microsoft Teams le permite crear aplicaciones personalizadas de Teams directamente desde el entorno de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="82631-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio Code environment.</span></span> <span data-ttu-id="82631-106">El kit de herramientas le orienta en el proceso y le ofrece todo lo que necesita para crear, depurar e iniciar su aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="82631-106">The toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="installing-the-teams-toolkit"></a><span data-ttu-id="82631-107">Instalación del kit de herramientas de Teams</span><span class="sxs-lookup"><span data-stu-id="82631-107">Installing the Teams Toolkit</span></span>

<span data-ttu-id="82631-108">Microsoft Teams Toolkit for Visual Studio Code está disponible para su descarga desde [Visual Studio Marketplace](https://aka.ms/teams-toolkit) o directamente como una extensión dentro de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="82631-108">The Microsoft Teams Toolkit for Visual Studio Code is available for download from the [Visual Studio Marketplace](https://aka.ms/teams-toolkit) or directly as an extension within Visual Studio Code.</span></span>

> [!TIP]
> <span data-ttu-id="82631-109">Después de la instalación, debería ver Teams Toolkit en la barra de Visual Studio de actividad Code.</span><span class="sxs-lookup"><span data-stu-id="82631-109">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="82631-110">Si no es así, haga clic con el botón secundario en la barra de actividades y seleccione **Microsoft Teams** para anclar el kit de herramientas para facilitar el acceso.</span><span class="sxs-lookup"><span data-stu-id="82631-110">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="82631-111">Uso del kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="82631-111">Using the toolkit</span></span>

- [<span data-ttu-id="82631-112">Configurar un nuevo proyecto</span><span class="sxs-lookup"><span data-stu-id="82631-112">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="82631-113">Importar un proyecto existente</span><span class="sxs-lookup"><span data-stu-id="82631-113">Import an existing project</span></span>](#import-an-existing-teams-app-project)
- [<span data-ttu-id="82631-114">Configurar la aplicación</span><span class="sxs-lookup"><span data-stu-id="82631-114">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="82631-115">Empaquetar la aplicación</span><span class="sxs-lookup"><span data-stu-id="82631-115">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="82631-116">Ejecutar la aplicación localmente o en Teams</span><span class="sxs-lookup"><span data-stu-id="82631-116">Run your app locally or in Teams</span></span>](#run-your-app)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="82631-117">Configurar un nuevo proyecto de Teams</span><span class="sxs-lookup"><span data-stu-id="82631-117">Set up a new Teams project</span></span>

1. <span data-ttu-id="82631-118">Cree un área de trabajo o carpeta para el proyecto en el entorno local.</span><span class="sxs-lookup"><span data-stu-id="82631-118">Create a workspace/folder for your project in your local environment.</span></span>
1. <span data-ttu-id="82631-119">En Visual Studio, seleccione el icono de Teams</span><span class="sxs-lookup"><span data-stu-id="82631-119">In Visual Studio Code, select the Teams icon</span></span> ![Icono de Teams](../assets/icons/favicon-16x16.png) <span data-ttu-id="82631-121">de la barra de actividades en el lado izquierdo de la ventana.</span><span class="sxs-lookup"><span data-stu-id="82631-121">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="82631-122">Seleccione **Abrir Microsoft Teams Toolkit en** el menú de comandos.</span><span class="sxs-lookup"><span data-stu-id="82631-122">Select **Open the Microsoft Teams Toolkit** from the command menu.</span></span>
1. <span data-ttu-id="82631-123">Selecciona **Crear una nueva aplicación de Teams** en el menú de comandos.</span><span class="sxs-lookup"><span data-stu-id="82631-123">Select **Create a new Teams app** from the command menu.</span></span>
1. <span data-ttu-id="82631-124">Cuando se le pida, escriba el nombre del área de trabajo .</span><span class="sxs-lookup"><span data-stu-id="82631-124">When prompted, enter the name of the workspace .</span></span> <span data-ttu-id="82631-125">Se usará como el nombre de la carpeta donde residirá el proyecto y el nombre predeterminado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="82631-125">This will be used as both the name of the folder where your project will reside, and the default name of your app.</span></span>
1. <span data-ttu-id="82631-126">Presiona **Entrar** y llegarás a la pantalla Agregar **capacidades** para configurar las propiedades de la nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="82631-126">Press **Enter** and you will arrive at the **Add capabilities** screen configure the properties for your new app.</span></span>
1. <span data-ttu-id="82631-127">Seleccione el **botón Finalizar** para completar el proceso de configuración.</span><span class="sxs-lookup"><span data-stu-id="82631-127">Select the **Finish** button to complete the configuration process.</span></span>

## <a name="import-an-existing-teams-app-project"></a><span data-ttu-id="82631-128">Importar un proyecto de aplicación de Teams existente</span><span class="sxs-lookup"><span data-stu-id="82631-128">Import an existing Teams app project</span></span>

1. <span data-ttu-id="82631-129">En Visual Studio, seleccione el icono de Teams</span><span class="sxs-lookup"><span data-stu-id="82631-129">In Visual Studio Code, select the Teams icon</span></span> ![Icono de Teams](../assets/icons/favicon-16x16.png) <span data-ttu-id="82631-131">de la barra de actividades en el lado izquierdo de la ventana.</span><span class="sxs-lookup"><span data-stu-id="82631-131">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="82631-132">Selecciona **Importar paquete de aplicación** en el menú de comandos.</span><span class="sxs-lookup"><span data-stu-id="82631-132">Select **Import app package** from the command menu.</span></span>
1. <span data-ttu-id="82631-133">Elige el archivo [zip del paquete de la](../concepts/build-and-test/apps-package.md) aplicación de Teams existente.</span><span class="sxs-lookup"><span data-stu-id="82631-133">Choose your existing [Teams app package](../concepts/build-and-test/apps-package.md) zip file.</span></span>
1. <span data-ttu-id="82631-134">Elija el **botón Seleccionar paquete de** publicación.</span><span class="sxs-lookup"><span data-stu-id="82631-134">Choose the **Select publishing package** button.</span></span> <span data-ttu-id="82631-135">La pestaña de configuración del kit de herramientas ahora debe rellenarse con los detalles de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="82631-135">The configuration tab of the toolkit should now be populated with your app's details.</span></span>
1. <span data-ttu-id="82631-136">En Visual Studio, seleccione Agregar carpeta de archivo al área de trabajo para agregar el directorio de código fuente al área de trabajo  ->   Visual Studio código.</span><span class="sxs-lookup"><span data-stu-id="82631-136">In Visual Studio Code, select **File** -> **Add Folder to Workspace** to add your source code directory to the Visual Studio Code workspace.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="82631-137">Configurar la aplicación</span><span class="sxs-lookup"><span data-stu-id="82631-137">Configure your app</span></span>

<span data-ttu-id="82631-138">En su núcleo, la aplicación teams abarca tres componentes:</span><span class="sxs-lookup"><span data-stu-id="82631-138">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="82631-139">Cliente de Microsoft Teams (web, de escritorio o móvil) donde los usuarios interactúan con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="82631-139">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="82631-140">Un servidor que responde a solicitudes de contenido que se mostrarán en Teams, por ejemplo, contenido de pestaña HTML o una tarjeta adaptable de bot.</span><span class="sxs-lookup"><span data-stu-id="82631-140">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="82631-141">Un paquete [de aplicación de](/concepts/build-and-test/apps-package.md) Teams que consta de tres archivos:</span><span class="sxs-lookup"><span data-stu-id="82631-141">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="82631-142">El manifest.jsen</span><span class="sxs-lookup"><span data-stu-id="82631-142">The manifest.json</span></span> 
  > - <span data-ttu-id="82631-143">Icono [de color para](../resources/schema/manifest-schema.md#icons) que la aplicación se muestre en el catálogo de aplicaciones públicas u de la organización</span><span class="sxs-lookup"><span data-stu-id="82631-143">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="82631-144">Icono [de esquema para](../resources/schema/manifest-schema.md#icons) mostrar en la barra de actividades de Teams.</span><span class="sxs-lookup"><span data-stu-id="82631-144">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="82631-145">Cuando se instala una aplicación, el cliente de Teams analiza el archivo de manifiesto para determinar la información necesaria, como el nombre de la aplicación y la dirección URL donde se encuentran los servicios.</span><span class="sxs-lookup"><span data-stu-id="82631-145">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="82631-146">Para configurar la aplicación, vaya a la pestaña **Microsoft Teams Toolkit** en Visual Studio Código.</span><span class="sxs-lookup"><span data-stu-id="82631-146">To configure your app, navigate to the **Microsoft Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="82631-147">Selecciona **Editar paquete de aplicación** para ver la página detalles de **la** aplicación.</span><span class="sxs-lookup"><span data-stu-id="82631-147">Select **Edit app package** to view the **App details** page.</span></span>
1. <span data-ttu-id="82631-148">La edición de los campos de la página detalles de la aplicación actualiza el contenido del archivo manifest.jsen que, en última instancia, se enviará como parte del paquete de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="82631-148">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> <span data-ttu-id="82631-149">*Consulta* [Editor de manifiestos de App Studio](https://aka.ms/teams-toolkit-manifest)</span><span class="sxs-lookup"><span data-stu-id="82631-149">*See* [App Studio manifest editor](https://aka.ms/teams-toolkit-manifest)</span></span>

## <a name="package-your-app"></a><span data-ttu-id="82631-150">Empaquetar la aplicación</span><span class="sxs-lookup"><span data-stu-id="82631-150">Package your app</span></span>

<span data-ttu-id="82631-151">La modificación de **los archivos** de **página,** manifiesto o **.env** de la carpeta  **.publish** de la aplicación generará automáticamente el **Development.zip** aplicación.</span><span class="sxs-lookup"><span data-stu-id="82631-151">Modifying the **app details** page, **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="82631-152">Tendrás que incluir dos [iconos](../concepts/build-and-test/apps-package.md#app-icons) en esa misma carpeta.</span><span class="sxs-lookup"><span data-stu-id="82631-152">You'll need to include [two icons](../concepts/build-and-test/apps-package.md#app-icons) in that same folder.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="82631-153">Instalar y ejecutar la aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="82631-153">Install and run your app locally</span></span>

## <a name="run-your-app"></a><span data-ttu-id="82631-154">Ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="82631-154">Run your app</span></span>

### <a name="install-and-run-your-app-locally"></a><span data-ttu-id="82631-155">Instalar y ejecutar la aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="82631-155">Install and run your app locally</span></span>

<span data-ttu-id="82631-156">Consulta \**Crear y ejecutar* contenido en la página principal del proyecto para obtener instrucciones detalladas sobre cómo empaquetar y probar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="82631-156">Refer to the \**Build and Run* content in your project homepage for detailed instructions on how to package and test your app.</span></span> <span data-ttu-id="82631-157">En general, debes instalar el servidor de la aplicación, ejecutarlo y, a continuación, configurar una solución de túnel para que Teams pueda tener acceso al contenido que se ejecuta desde localhost.</span><span class="sxs-lookup"><span data-stu-id="82631-157">In general, you need to install your app's server, get it running, then setup a tunneling solution so that Teams can access content running from localhost.</span></span>

### <a name="enable-development-from-localhost"></a><span data-ttu-id="82631-158">Habilitar el desarrollo desde localhost</span><span class="sxs-lookup"><span data-stu-id="82631-158">Enable development from localhost</span></span>

<span data-ttu-id="82631-159">Si quieres depurar la aplicación basada en pestañas en localhost con HTTPS, deberás decir a tu explorador que confíe en la aplicación desde <https://localhost> .</span><span class="sxs-lookup"><span data-stu-id="82631-159">If you wish to debug your tab based app on localhost using HTTPS, you will need to tell your browser to trust the app being served from <https://localhost>.</span></span> <span data-ttu-id="82631-160">Vaya a <https://localhost:3000/tab>.</span><span class="sxs-lookup"><span data-stu-id="82631-160">Navigate to <https://localhost:3000/tab>.</span></span> <span data-ttu-id="82631-161">Si ve una advertencia que indica que el sitio no es de confianza, elija la opción para continuar de todos modos.</span><span class="sxs-lookup"><span data-stu-id="82631-161">If you see a warning indicating that the site isn't trusted, choose the option to proceed anyway.</span></span> <span data-ttu-id="82631-162">La aplicación ahora debe ser accesible desde el cliente de Teams.</span><span class="sxs-lookup"><span data-stu-id="82631-162">Your app should now be accessible from the Teams client.</span></span>

### <a name="run-your-app-in-teams"></a><span data-ttu-id="82631-163">Ejecutar la aplicación en Teams</span><span class="sxs-lookup"><span data-stu-id="82631-163">Run your app in Teams</span></span>

<span data-ttu-id="82631-164">Requisitos previos: [Habilitar el modo de vista previa del desarrollador de Teams](https://aka.ms/teams-toolkit-enable-devpreview)</span><span class="sxs-lookup"><span data-stu-id="82631-164">Prerequisites: [Enable Teams developer preview mode](https://aka.ms/teams-toolkit-enable-devpreview)</span></span>

1. <span data-ttu-id="82631-165">Vaya a la barra de actividades en el lado izquierdo de la ventana Visual Studio Código.</span><span class="sxs-lookup"><span data-stu-id="82631-165">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="82631-166">Seleccione el **icono Ejecutar** para mostrar la vista **Ejecutar y** depurar.</span><span class="sxs-lookup"><span data-stu-id="82631-166">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="82631-167">También puede usar el método abreviado de teclado `Ctrl+Shift+D` .</span><span class="sxs-lookup"><span data-stu-id="82631-167">You can also use the keyboard shortcut `Ctrl+Shift+D`.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="82631-168">Paso siguiente: Mantener y admitir la aplicación publicada</span><span class="sxs-lookup"><span data-stu-id="82631-168">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)

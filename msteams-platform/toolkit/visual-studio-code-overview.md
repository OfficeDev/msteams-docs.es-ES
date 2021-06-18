---
title: Crear aplicaciones con Microsoft Teams Toolkit y Visual Studio code
description: Introducción a la creación de excelentes aplicaciones personalizadas directamente en Visual Studio Code con Microsoft Teams Toolkit
keywords: Kit de herramientas de código visual studio de teams
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: b2cfab5cb2ea2d727608b6ea3bbfec3271b2b039
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994143"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a><span data-ttu-id="3160e-104">Crear aplicaciones con Teams Toolkit y Visual Studio code</span><span class="sxs-lookup"><span data-stu-id="3160e-104">Build apps with the Teams Toolkit and Visual Studio Code</span></span>

<span data-ttu-id="3160e-105">Teams Toolkit for Visual Studio Code ayuda a los desarrolladores a crear e implementar aplicaciones de Teams con identidad integrada, acceso al almacenamiento en la nube, datos de Microsoft Graph y otros servicios en Azure y M365 con un enfoque de "configuración cero" para la experiencia del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="3160e-105">The Teams Toolkit for Visual Studio Code helps developers create and deploy Teams apps with integrated identity, access to cloud storage, data from Microsoft Graph, and other services in Azure and M365 with a “zero-configuration” approach to the developer experience.</span></span>  

<span data-ttu-id="3160e-106">También puede usar el kit de herramientas con Visual Studio o como una CLI (denominada `teamsfx` ).</span><span class="sxs-lookup"><span data-stu-id="3160e-106">You also can use the toolkit with Visual Studio or as a CLI (called `teamsfx`).</span></span>

## <a name="install-the-teams-toolkit-for-visual-studio-code"></a><span data-ttu-id="3160e-107">Instalar teams Toolkit for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="3160e-107">Install the Teams Toolkit for Visual Studio Code</span></span>

1. <span data-ttu-id="3160e-108">Abrir Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="3160e-108">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="3160e-109">Seleccione la vista Extensiones (**Ctrl+Mayús+X**  /  **,⇧-X** o **Ver > extensiones**).</span><span class="sxs-lookup"><span data-stu-id="3160e-109">Select the Extensions view (**Ctrl+Shift+X** / **⌘⇧-X** or **View > Extensions**).</span></span>
1. <span data-ttu-id="3160e-110">En el cuadro de búsqueda, escriba _Teams Toolkit_.</span><span class="sxs-lookup"><span data-stu-id="3160e-110">In the search box, enter _Teams Toolkit_.</span></span>
1. <span data-ttu-id="3160e-111">Seleccione el botón de instalación verde junto al Kit de herramientas de Teams.</span><span class="sxs-lookup"><span data-stu-id="3160e-111">Select on the green install button next to the Teams Toolkit.</span></span>

<span data-ttu-id="3160e-112">También puede encontrar el Kit de herramientas de Teams en [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).</span><span class="sxs-lookup"><span data-stu-id="3160e-112">You also can find the Teams Toolkit on the [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).</span></span>

<span data-ttu-id="3160e-113">La extensión de código de Visual Studio las siguientes herramientas se instalan cuando son necesarias.</span><span class="sxs-lookup"><span data-stu-id="3160e-113">The following tools are installed by the Visual Studio Code extension when they are needed.</span></span> <span data-ttu-id="3160e-114">Si ya está instalado, la versión instalada se usa en su lugar.</span><span class="sxs-lookup"><span data-stu-id="3160e-114">If already installed, the installed version is used instead.</span></span> <span data-ttu-id="3160e-115">Si usa Linux (incluido WSL), debe instalar estas herramientas antes de usar:</span><span class="sxs-lookup"><span data-stu-id="3160e-115">If using Linux (including WSL), you must install these tools before use:</span></span>

- [<span data-ttu-id="3160e-116">Azure Functions Core Tools</span><span class="sxs-lookup"><span data-stu-id="3160e-116">Azure Functions Core Tools</span></span>](/azure/azure-functions/functions-run-local)

    <span data-ttu-id="3160e-117">Azure Functions Core Tools se usa para ejecutar los componentes back-end localmente durante una ejecución de depuración local, incluidas las aplicaciones auxiliares de autenticación necesarias para ejecutar los servicios en Azure.</span><span class="sxs-lookup"><span data-stu-id="3160e-117">Azure Functions Core Tools is used to run any backend components locally during a local debug run, including the authentication helpers required when running your services in Azure.</span></span> <span data-ttu-id="3160e-118">Se instala en el directorio del proyecto mediante el npm `devDependencies` .</span><span class="sxs-lookup"><span data-stu-id="3160e-118">It is installed within the project directory using the npm `devDependencies`.</span></span>

- [<span data-ttu-id="3160e-119">SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="3160e-119">.NET SDK</span></span>](/dotnet/core/install/)

    <span data-ttu-id="3160e-120">El SDK de .NET se usa para instalar enlaces personalizados para la depuración local y las implementaciones de aplicaciones de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="3160e-120">The .NET SDK is used to install customized bindings for local debugging and Azure Functions app deployments.</span></span> <span data-ttu-id="3160e-121">Si no ha instalado el SDK de .NET 3.1 o posterior globalmente, se instalará la versión portátil.</span><span class="sxs-lookup"><span data-stu-id="3160e-121">If you have not installed the .NET 3.1 or later SDK globally, the portable version is installed.</span></span>

- [<span data-ttu-id="3160e-122">ngrok</span><span class="sxs-lookup"><span data-stu-id="3160e-122">ngrok</span></span>](https://ngrok.com/download)

    <span data-ttu-id="3160e-123">Algunas características de la aplicación de Teams (bots de conversación, extensiones de mensajería y webhooks entrantes) requieren conexiones entrantes.</span><span class="sxs-lookup"><span data-stu-id="3160e-123">Some Teams app features (conversational bots, messaging extensions, and incoming webhooks) require inbound connections.</span></span>  <span data-ttu-id="3160e-124">Debe exponer el sistema de desarrollo a Teams a través de un túnel.</span><span class="sxs-lookup"><span data-stu-id="3160e-124">You need to expose your development system to Teams through a tunnel.</span></span> <span data-ttu-id="3160e-125">No es necesario un túnel para las aplicaciones que solo incluyen pestañas.</span><span class="sxs-lookup"><span data-stu-id="3160e-125">A tunnel is not required for apps that only include tabs.</span></span>  <span data-ttu-id="3160e-126">Este paquete se instala en el directorio del proyecto (mediante npm `devDependencies` ).</span><span class="sxs-lookup"><span data-stu-id="3160e-126">This package is installed within the project directory (using npm `devDependencies`).</span></span>

## <a name="use-the-teams-toolkit-for-visual-studio-code"></a><span data-ttu-id="3160e-127">Usar el Kit de herramientas de Teams para Visual Studio código</span><span class="sxs-lookup"><span data-stu-id="3160e-127">Use the Teams Toolkit for Visual Studio Code</span></span>

- [<span data-ttu-id="3160e-128">Configurar un nuevo proyecto</span><span class="sxs-lookup"><span data-stu-id="3160e-128">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="3160e-129">Configurar la aplicación</span><span class="sxs-lookup"><span data-stu-id="3160e-129">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="3160e-130">Ejecutar la aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="3160e-130">Run your app locally</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="3160e-131">Publicar la aplicación</span><span class="sxs-lookup"><span data-stu-id="3160e-131">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="3160e-132">Configurar un nuevo proyecto de Teams</span><span class="sxs-lookup"><span data-stu-id="3160e-132">Set up a new Teams project</span></span>

<span data-ttu-id="3160e-133">Teams Toolkit puede crear aplicaciones de React hospedadas en elementos web de Azure o SPFx hospedados en su entorno de SharePoint M365.</span><span class="sxs-lookup"><span data-stu-id="3160e-133">The Teams Toolkit can create React apps that are hosted in Azure or SPFx web parts that are hosted on your M365 SharePoint environment.</span></span> <span data-ttu-id="3160e-134">Para crear una nueva aplicación de React que se va a hospedar en Azure:</span><span class="sxs-lookup"><span data-stu-id="3160e-134">To create a new React app to be hosted on Azure:</span></span>

1. <span data-ttu-id="3160e-135">Abra Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="3160e-135">Open Visual Studio code.</span></span>
1. <span data-ttu-id="3160e-136">Abra el Kit de herramientas de Teams. Para ello, seleccione el icono de Teams en la barra lateral:</span><span class="sxs-lookup"><span data-stu-id="3160e-136">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icono de Teams en la barra lateral de Visual Studio Code.":::

1. <span data-ttu-id="3160e-138">Seleccione **Crear nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="3160e-138">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Ubicación del vínculo Crear nuevo proyecto en la barra lateral del Kit de herramientas de Teams.":::

1. <span data-ttu-id="3160e-140">Seleccione **Crear una nueva aplicación de Teams**.</span><span class="sxs-lookup"><span data-stu-id="3160e-140">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Inicio del Asistente para crear un nuevo proyecto":::

1. <span data-ttu-id="3160e-142">En el **paso Seleccionar capacidades,** la **funcionalidad Tab** ya está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="3160e-142">On the **Select capabilities** step, the **Tab** capability is already selected.</span></span> <span data-ttu-id="3160e-143">También puede seleccionar opcionalmente **Bot** y **Messaging Extension**.</span><span class="sxs-lookup"><span data-stu-id="3160e-143">You can also optionally select **Bot** and **Messaging Extension**.</span></span>  <span data-ttu-id="3160e-144">Pulse **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3160e-144">Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Captura de pantalla que muestra cómo agregar funcionalidades a la nueva aplicación.":::

1. <span data-ttu-id="3160e-146">En el paso **Tipo de hospedaje del front-end**, seleccione **Azure**.</span><span class="sxs-lookup"><span data-stu-id="3160e-146">On the **Frontend hosting type** step, select **Azure**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Captura de pantalla que muestra cómo seleccionar el hospedaje para la nueva aplicación.":::

1. <span data-ttu-id="3160e-148">Opcionalmente, en el paso **Recursos de** nube, seleccione recursos en la nube que use la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3160e-148">Optionally, on the **Cloud resources** step, select cloud resources that your application uses.</span></span> <span data-ttu-id="3160e-149">Puede seleccionar el acceso CRUD (crear, leer, actualizar y eliminar) a una tabla SQL una API:</span><span class="sxs-lookup"><span data-stu-id="3160e-149">You can select CRUD (create, read, update, and delete) access to a SQL table or an API:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="Captura de pantalla que muestra cómo agregar recursos de nube para la nueva aplicación.":::

1. <span data-ttu-id="3160e-151">En el paso **Lenguaje de** programación, puede elegir **JavaScript** o **TypeScript**:</span><span class="sxs-lookup"><span data-stu-id="3160e-151">On the **Programming Language** step, you can choose **JavaScript** or **TypeScript**:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Captura de pantalla que muestra cómo seleccionar el lenguaje de programación.":::

1. <span data-ttu-id="3160e-153">Seleccione una carpeta de área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3160e-153">Select a workspace folder.</span></span> <span data-ttu-id="3160e-154">Se crea una carpeta dentro de la carpeta del área de trabajo para el proyecto que está creando.</span><span class="sxs-lookup"><span data-stu-id="3160e-154">A folder is created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="3160e-155">Escriba un nombre adecuado para la aplicación, como `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="3160e-155">Enter a suitable name for your app, like `helloworld`.</span></span> <span data-ttu-id="3160e-156">El nombre de la aplicación solo puede contener caracteres alfanuméricos.</span><span class="sxs-lookup"><span data-stu-id="3160e-156">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="3160e-157">Presione **Entrar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="3160e-157">Press **Enter** to continue.</span></span>

<span data-ttu-id="3160e-158">La aplicación de Teams se crea en unos segundos.</span><span class="sxs-lookup"><span data-stu-id="3160e-158">Your Teams app is created within a few seconds.</span></span> <span data-ttu-id="3160e-159">La aplicación scaffolded contiene código para controlar el inicio de sesión único con Azure Active Directory y el acceso a Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="3160e-159">The scaffolded app contains code to handle single sign-on with Azure Active Directory and access to the Microsoft Graph.</span></span>  <span data-ttu-id="3160e-160">Si seleccionó recursos de Azure, también estará disponible el código para esos recursos.</span><span class="sxs-lookup"><span data-stu-id="3160e-160">If you selected Azure resources, then the code for those resources is also available.</span></span>

<span data-ttu-id="3160e-161">Para obtener un recorrido por el proceso de creación y publicación de SPFx, vea el [tutorial de SPFx](../get-started/first-app-spfx.md).</span><span class="sxs-lookup"><span data-stu-id="3160e-161">For a walk-through of the SPFx creation and publication process, see the [SPFx tutorial](../get-started/first-app-spfx.md).</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="3160e-162">Configurar la aplicación</span><span class="sxs-lookup"><span data-stu-id="3160e-162">Configure your app</span></span>

<span data-ttu-id="3160e-163">En su núcleo, la aplicación teams abarca tres componentes:</span><span class="sxs-lookup"><span data-stu-id="3160e-163">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="3160e-164">Cliente de Microsoft Teams (web, de escritorio o móvil) donde los usuarios interactúan con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3160e-164">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="3160e-165">Un servidor que responde a las solicitudes de contenido que se muestran en Teams.</span><span class="sxs-lookup"><span data-stu-id="3160e-165">A server that responds to requests for content that is displayed in Teams.</span></span> <span data-ttu-id="3160e-166">Por ejemplo, contenido de pestaña HTML o una tarjeta adaptable de bot.</span><span class="sxs-lookup"><span data-stu-id="3160e-166">For example, HTML tab content or a bot Adaptive Card.</span></span>
  1. <span data-ttu-id="3160e-167">Un paquete de aplicación de Teams consta de tres archivos:</span><span class="sxs-lookup"><span data-stu-id="3160e-167">A Teams app package consists of three files:</span></span>

      > [!div class="checklist"]
      >
      > - <span data-ttu-id="3160e-168">El manifest.jsen.</span><span class="sxs-lookup"><span data-stu-id="3160e-168">The manifest.json.</span></span>
      > - <span data-ttu-id="3160e-169">Icono [de color para](../resources/schema/manifest-schema.md#icons) que la aplicación se muestre en el catálogo de aplicaciones públicas u de la organización.</span><span class="sxs-lookup"><span data-stu-id="3160e-169">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog.</span></span>
      > - <span data-ttu-id="3160e-170">Icono [de esquema para](../resources/schema/manifest-schema.md#icons) mostrar en la barra de actividades de Teams.</span><span class="sxs-lookup"><span data-stu-id="3160e-170">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="3160e-171">El manifiesto y los iconos se almacenan en la `.fx` carpeta del proyecto antes de cargarse en Teams.</span><span class="sxs-lookup"><span data-stu-id="3160e-171">The manifest and icons are stored in the `.fx` folder of your project prior to being uploaded to Teams.</span></span> <span data-ttu-id="3160e-172">Cuando se instala una aplicación, el cliente de Teams analiza el archivo de manifiesto para determinar la información necesaria, como el nombre de la aplicación y la dirección URL donde se encuentran los servicios.</span><span class="sxs-lookup"><span data-stu-id="3160e-172">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="3160e-173">Para configurar la aplicación, vaya a la pestaña **Kit de herramientas de Teams** en Visual Studio código.</span><span class="sxs-lookup"><span data-stu-id="3160e-173">To configure your app, navigate to the **Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="3160e-174">Seleccione **Editor de manifiestos** en la **sección** Proyecto.</span><span class="sxs-lookup"><span data-stu-id="3160e-174">Select **Manifest Editor** in the **Project** section.</span></span>

<span data-ttu-id="3160e-175">La edición de los campos de la página detalles de la aplicación actualiza el contenido del archivo manifest.jsque, en última instancia, se envía como parte del paquete de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3160e-175">Editing the fields in the App details page updates the contents of the manifest.json file that is ultimately shipped as part of the app package.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="3160e-176">Instalar y ejecutar la aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="3160e-176">Install and run your app locally</span></span>

<span data-ttu-id="3160e-177">Para crear y ejecutar la aplicación localmente:</span><span class="sxs-lookup"><span data-stu-id="3160e-177">To build and run your app locally:</span></span>

1. <span data-ttu-id="3160e-178">Desde Visual Studio Code, presione **F5** para ejecutar la aplicación en modo de depuración.</span><span class="sxs-lookup"><span data-stu-id="3160e-178">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="3160e-179">Al ejecutar la aplicación por primera vez, se descargan todas las dependencias y se compila la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3160e-179">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="3160e-180">Cuando se complete la compilación, se abrirá automáticamente una ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="3160e-180">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="3160e-181">Este proceso puede tardar entre 3 o 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="3160e-181">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="3160e-182">El kit de herramientas le pide que instale un certificado local si es necesario.</span><span class="sxs-lookup"><span data-stu-id="3160e-182">The toolkit prompts you to install a local certificate if required.</span></span> <span data-ttu-id="3160e-183">Este certificado permite a Teams cargar la aplicación desde `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="3160e-183">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="3160e-184">Seleccione Sí cuando aparezca el siguiente cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="3160e-184">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Captura de pantalla en la que se muestra la solicitud para instalar un certificado SSL para permitir que Teams cargue la aplicación desde localhost.":::

1. <span data-ttu-id="3160e-186">Se inicia el explorador web para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3160e-186">Your web browser is started to run the application.</span></span> <span data-ttu-id="3160e-187">Si se le pide que abra Microsoft Teams, seleccione Cancelar para permanecer en el explorador.</span><span class="sxs-lookup"><span data-stu-id="3160e-187">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="3160e-188">Es posible que también se le pida que cambie a la aplicación de Teams en otras ocasiones.</span><span class="sxs-lookup"><span data-stu-id="3160e-188">You may also be prompted to switch to the Teams application at other times.</span></span> <span data-ttu-id="3160e-189">Seleccione la aplicación web cuando esto suceda.</span><span class="sxs-lookup"><span data-stu-id="3160e-189">Select the web app when this happens.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Captura de pantalla que muestra cómo elegir la versión web de Teams al iniciarlo":::

1. <span data-ttu-id="3160e-191">Es posible que se le pida que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="3160e-191">You may be prompted to sign in.</span></span> <span data-ttu-id="3160e-192">Si es así, inicie sesión con su cuenta de M365.</span><span class="sxs-lookup"><span data-stu-id="3160e-192">If so, sign in with your M365 account.</span></span>
1. <span data-ttu-id="3160e-193">Cuando se le pida que instale la aplicación en Teams, presione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3160e-193">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="3160e-194">Tanto el back-end como el front-end están unidos al depurador Visual Studio código.</span><span class="sxs-lookup"><span data-stu-id="3160e-194">Both the backend and frontend are hooked into the Visual Studio Code debugger.</span></span>  <span data-ttu-id="3160e-195">Esto le permite establecer puntos de interrupción en cualquier lugar del código e inspeccionar el estado.</span><span class="sxs-lookup"><span data-stu-id="3160e-195">This allows you to set breakpoints anywhere in your code and inspect state.</span></span>  <span data-ttu-id="3160e-196">También puede usar cualquier herramienta de depuración front-end (como React Developer Tools) en el explorador.</span><span class="sxs-lookup"><span data-stu-id="3160e-196">You can also use any frontend debugging tools (such as the React Developer Tools) within the browser.</span></span>  <span data-ttu-id="3160e-197">Para obtener más información acerca de la depuración en Visual Studio code, revise [la documentación](https://code.visualstudio.com/Docs/editor/debugging).</span><span class="sxs-lookup"><span data-stu-id="3160e-197">For more information about debugging in Visual Studio Code, review [the documentation](https://code.visualstudio.com/Docs/editor/debugging).</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="3160e-198">Publicar la aplicación en Teams</span><span class="sxs-lookup"><span data-stu-id="3160e-198">Publish your app to Teams</span></span>

<span data-ttu-id="3160e-199">Antes de que otras personas la puedan usar, debes publicar la aplicación en el Portal de desarrolladores para Teams.</span><span class="sxs-lookup"><span data-stu-id="3160e-199">Before it can be used by other people, you must publish your app to the Developer Portal for Teams.</span></span>

1. <span data-ttu-id="3160e-200">Para publicar la aplicación, vaya a la pestaña **Kit de herramientas de Teams** en Visual Studio código.</span><span class="sxs-lookup"><span data-stu-id="3160e-200">To publish your app, navigate to the **Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="3160e-201">Seleccione **Publicar para Teams** en la **Project.**</span><span class="sxs-lookup"><span data-stu-id="3160e-201">Select **Publish to Teams** in the **Project** section.</span></span>

<span data-ttu-id="3160e-202">Si usa el hospedaje de Azure, debe haber aprovisionado e implementado en la nube.</span><span class="sxs-lookup"><span data-stu-id="3160e-202">If using Azure hosting, you must have provisioned and deployed to the cloud.</span></span> <span data-ttu-id="3160e-203">Para obtener un recorrido por el proceso de SPFx de publicación, vea el [SPFx tutorial](../get-started/first-app-spfx.md).</span><span class="sxs-lookup"><span data-stu-id="3160e-203">For a walk-through of the SPFx publication process, see the [SPFx tutorial](../get-started/first-app-spfx.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="3160e-204">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="3160e-204">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3160e-205">Mantenimiento y soporte técnico de la aplicación publicada</span><span class="sxs-lookup"><span data-stu-id="3160e-205">Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)

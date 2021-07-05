---
title: 'Introducción: crea la primera aplicación Teams con Blazor'
author: adrianhall
description: Cree rápidamente una aplicación de Microsoft Teams en la que se muestre un mensaje de "Hola a todos" con el Microsoft Teams Toolkit y .NET Blazor.
ms.author: adhal
ms.date: 04/27/2021
ms.topic: quickstart
ms.openlocfilehash: c14f55d014af120cab88044d31ee8600017e3c57
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254310"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-blazor"></a><span data-ttu-id="59932-104">Crear y ejecutar la primera aplicación Microsoft Teams con Blazor</span><span class="sxs-lookup"><span data-stu-id="59932-104">Build and run your first Microsoft Teams app with Blazor</span></span>

<span data-ttu-id="59932-105">En este tutorial, aprenderás a crear una nueva aplicación Microsoft Teams en .NET/Blazor que implemente una aplicación personal sencilla para extraer información de microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="59932-105">In this tutorial, you will learn how to create a new Microsoft Teams app in .NET/Blazor that implements a simple personal app to pull information from the Microsoft Graph.</span></span> <span data-ttu-id="59932-106">Por ejemplo, una *aplicación personal incluye* un conjunto de pestañas para uso individual.</span><span class="sxs-lookup"><span data-stu-id="59932-106">For example, a *personal app* includes a set of tabs for individual use.</span></span> <span data-ttu-id="59932-107">Durante el tutorial, aprenderás sobre la estructura de una aplicación Teams, cómo ejecutar una aplicación localmente y cómo implementar la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="59932-107">During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to Azure.</span></span>

<span data-ttu-id="59932-108">La aplicación que se crea muestra información básica del usuario para el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="59932-108">The app that is built displays basic user information for the current user.</span></span>  <span data-ttu-id="59932-109">Cuando se conceda permiso, la aplicación se conectará a Microsoft Graph como el usuario actual para obtener el perfil completo.</span><span class="sxs-lookup"><span data-stu-id="59932-109">When permission is granted, the app will connect to the Microsoft Graph as the current user to get the complete profile.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="59932-110">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="59932-110">Before you begin</span></span>

<span data-ttu-id="59932-111">Asegúrese de que el entorno de desarrollo está configurado instalando los requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="59932-111">Make sure your development environment is set up by installing the prerequisites.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="59932-112">Requisitos previos para la instalación</span><span class="sxs-lookup"><span data-stu-id="59932-112">Install prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="59932-113">Crear un proyecto</span><span class="sxs-lookup"><span data-stu-id="59932-113">Create your project</span></span>

<span data-ttu-id="59932-114">Use el Kit de herramientas de Teams para crear su primer proyecto:</span><span class="sxs-lookup"><span data-stu-id="59932-114">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="59932-115">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="59932-115">Visual Studio 2019</span></span>](#tab/vs)

1. <span data-ttu-id="59932-116">Abra Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="59932-116">Open Visual Studio 2019.</span></span>

1. <span data-ttu-id="59932-117">Seleccione **Crear un nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="59932-117">Select **Create a new project**.</span></span>

1. <span data-ttu-id="59932-118">Selecciona **Microsoft Teams app y,** a continuación, **selecciona Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="59932-118">Select **Microsoft Teams App**, then select **Next**.</span></span>  <span data-ttu-id="59932-119">Para ayudarle a encontrar la plantilla, use el tipo de **proyecto Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="59932-119">To help you find the template, use the project type **Microsoft Teams**.</span></span>

1. <span data-ttu-id="59932-120">Escriba un nombre y seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="59932-120">Enter a name and select **Next**.</span></span>

1. <span data-ttu-id="59932-121">Escriba el nombre de la aplicación y el nombre de la compañía.</span><span class="sxs-lookup"><span data-stu-id="59932-121">Enter the application name and company name.</span></span>

1. <span data-ttu-id="59932-122">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="59932-122">Select **Create**.</span></span>  <span data-ttu-id="59932-123">El nombre de la aplicación y el nombre de la compañía se muestran a los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="59932-123">The application name and company name are displayed to your end users.</span></span> <span data-ttu-id="59932-124">La aplicación Teams se creará en unos segundos.</span><span class="sxs-lookup"><span data-stu-id="59932-124">Your Teams app will be created within a few seconds.</span></span>  <span data-ttu-id="59932-125">Después de crear el proyecto, configure el inicio de sesión único con M365:</span><span class="sxs-lookup"><span data-stu-id="59932-125">After the project is created, set up single sign-on with M365:</span></span>

   1. <span data-ttu-id="59932-126">Seleccione **Project**  >  **Configuración de TeamsFx** para  >  **SSO...**.</span><span class="sxs-lookup"><span data-stu-id="59932-126">Select **Project** > **TeamsFx** > **Configure for SSO...**.</span></span>
   1. <span data-ttu-id="59932-127">Cuando se le pida, inicie sesión en su cuenta de administrador de M365.</span><span class="sxs-lookup"><span data-stu-id="59932-127">When prompted, sign in to your M365 administrator account.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="59932-128">Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="59932-128">Command line</span></span>](#tab/cli)

1. <span data-ttu-id="59932-129">Abra un terminal y seleccione el directorio donde desea crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="59932-129">Open a Terminal and select the directory where you wish to create the project.</span></span>

1. <span data-ttu-id="59932-130">Ejecute `dotnet new -i` para instalar la plantilla desde NuGet:</span><span class="sxs-lookup"><span data-stu-id="59932-130">Run `dotnet new -i` to install the template from NuGet:</span></span>

   ``` bash
   dotnet new --install Microsoft.TeamsFx.VisualStudio.ProjectTemplates::0.1.43-beta
   ```

   <span data-ttu-id="59932-131">Solo tiene que hacerlo la primera vez o al actualizar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="59932-131">You only need to do this the first time or when updating the template.</span></span> <span data-ttu-id="59932-132">Compruebe [NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/) la versión más reciente de este paquete.</span><span class="sxs-lookup"><span data-stu-id="59932-132">Check [NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/) for the latest version of this package.</span></span>

1. <span data-ttu-id="59932-133">Crear un directorio:</span><span class="sxs-lookup"><span data-stu-id="59932-133">Create a directory:</span></span>

   ``` bash
   mkdir helloworld
   ```

1. <span data-ttu-id="59932-134">Ejecute `dotnet new` para crear un nuevo proyecto:</span><span class="sxs-lookup"><span data-stu-id="59932-134">Run `dotnet new` to create a new project:</span></span>

   ``` bash
   dotnet new teamsapp --shortName my-teams-app --companyName "My Company"
   ```

1. <span data-ttu-id="59932-135">Después de scaffolding, configure el proyecto para Teams implementación:</span><span class="sxs-lookup"><span data-stu-id="59932-135">After scaffolding, configure the project for Teams deployment:</span></span>

   ``` bash
   teamsfx init
   ```

   <span data-ttu-id="59932-136">Ahora puede abrir la solución en Visual Studio para la depuración.</span><span class="sxs-lookup"><span data-stu-id="59932-136">You can now open the solution in Visual Studio for debugging.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="59932-137">Dar un paseo por el código fuente</span><span class="sxs-lookup"><span data-stu-id="59932-137">Take a tour of the source code</span></span>

<span data-ttu-id="59932-138">Si quiere omitir esta sección por ahora, puede [ejecutar la aplicación de forma local](#run-your-app-locally).</span><span class="sxs-lookup"><span data-stu-id="59932-138">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="59932-139">Después de Teams Toolkit configurar el proyecto, tienes los componentes para crear una aplicación personal básica para Teams.</span><span class="sxs-lookup"><span data-stu-id="59932-139">After the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams.</span></span> <span data-ttu-id="59932-140">Los directorios y archivos del proyecto se muestran en el área Explorador de soluciones de Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="59932-140">The project directories and files display in the Solution Explorer area of Visual Studio 2019.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/blazor-file-layout.png" alt-text="Captura de pantalla que muestra los archivos de proyecto de la aplicación para una aplicación personal en Visual Studio 2019.":::

- <span data-ttu-id="59932-142">Los iconos de aplicación se almacenan como archivos PNG en `color.png` y `outline.png`.</span><span class="sxs-lookup"><span data-stu-id="59932-142">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="59932-143">El manifiesto de la aplicación para publicar a través del Portal de desarrolladores para Teams se almacena en `Properties/manifest.json` .</span><span class="sxs-lookup"><span data-stu-id="59932-143">The app manifest for publishing through the Developer Portal for Teams is stored in `Properties/manifest.json`.</span></span>
- <span data-ttu-id="59932-144">Se proporciona un controlador back-end `Controllers/BackendController.cs` para ayudar con la autenticación.</span><span class="sxs-lookup"><span data-stu-id="59932-144">A backend controller is provided in `Controllers/BackendController.cs` for assisting with authentication.</span></span>

<span data-ttu-id="59932-145">Desde que creaste una aplicación de pestaña durante la instalación, Teams Toolkit scaffolding todo el código necesario para una pestaña básica como [un servidor de Blazor](/aspnet/core/blazor).</span><span class="sxs-lookup"><span data-stu-id="59932-145">Since you created a tab app during setup, the Teams Toolkit scaffolds all the necessary code for a basic tab as a [Blazor Server](/aspnet/core/blazor).</span></span>

- <span data-ttu-id="59932-146">`Pages/Tab.razor` es el punto de entrada de la aplicación front-end.</span><span class="sxs-lookup"><span data-stu-id="59932-146">`Pages/Tab.razor` is the front-end application's entry point.</span></span>
- <span data-ttu-id="59932-147">`TeamsFx.cs`y `JS/src/index.js` se usa para inicializar las comunicaciones con el Teams host.</span><span class="sxs-lookup"><span data-stu-id="59932-147">`TeamsFx.cs` and `JS/src/index.js` is used for initializing communications with the Teams host.</span></span>

<span data-ttu-id="59932-148">Puede agregar funcionalidad back-end agregando controladores ASP.NET Core adicionales a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="59932-148">You can add backend functionality by adding additional ASP.NET Core controllers to your application.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="59932-149">Ejecutar la aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="59932-149">Run your app locally</span></span>

<span data-ttu-id="59932-150">El Kit de herramientas de Teams le permite ejecutar la aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="59932-150">Teams Toolkit allows you to run your app locally.</span></span>  <span data-ttu-id="59932-151">Se compone de varias partes que son necesarias para proporcionar la infraestructura correcta que espera Teams:</span><span class="sxs-lookup"><span data-stu-id="59932-151">This consists of several parts that are necessary to provide the correct infrastructure that Teams expects:</span></span>

- <span data-ttu-id="59932-152">Una aplicación se registra con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="59932-152">An application is registered with Azure Active Directory.</span></span>  <span data-ttu-id="59932-153">Esta aplicación tiene permisos asociados a la ubicación desde la que se carga la aplicación y a cualquier recurso del back-end al que accede.</span><span class="sxs-lookup"><span data-stu-id="59932-153">This application has permissions associated with the location that the app is loaded from and any backend resources it accesses.</span></span>
- <span data-ttu-id="59932-154">Una API web se hospeda (a través de IIS Express) para ayudar con las tareas de autenticación, actuando como proxy entre la aplicación y Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="59932-154">A web API is hosted (via IIS Express) to assist with authentication tasks, acting as a proxy between the app and Azure Active Directory.</span></span>  
- <span data-ttu-id="59932-155">Se genera un manifiesto de aplicación y existe en el Portal de desarrolladores para Teams.</span><span class="sxs-lookup"><span data-stu-id="59932-155">An app manifest is generated and exists in the Developer Portal for Teams.</span></span>  <span data-ttu-id="59932-156">Teams usa el manifiesto de la aplicación para decir a los clientes conectados desde dónde cargar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="59932-156">Teams uses the app manifest to tell connected clients where to load the app from.</span></span>

<span data-ttu-id="59932-157">Una vez hecho esto, la aplicación se puede cargar en el Teams cliente.</span><span class="sxs-lookup"><span data-stu-id="59932-157">After this is done, the app can be loaded within the Teams client.</span></span>  <span data-ttu-id="59932-158">Usamos el cliente web de Teams para poder ver el código HTML, CSS y JavaScript en un entorno de desarrollo web estándar.</span><span class="sxs-lookup"><span data-stu-id="59932-158">We use the Teams web client so that we can see the HTML, CSS, and JavaScript code within a standard web development environment.</span></span>

<span data-ttu-id="59932-159">Para crear y ejecutar la aplicación localmente:</span><span class="sxs-lookup"><span data-stu-id="59932-159">To build and run your app locally:</span></span>


1. <span data-ttu-id="59932-160">Desde Visual Studio Code, presione la **tecla F5** para ejecutar la aplicación en modo de depuración.</span><span class="sxs-lookup"><span data-stu-id="59932-160">From Visual Studio Code, press the **F5** key to run your application in debug mode.</span></span>


1. <span data-ttu-id="59932-161">Si se solicita, instale el certificado SSL autofirmado para la depuración local.</span><span class="sxs-lookup"><span data-stu-id="59932-161">If requested, install the self-signed SSL certificate for local debugging.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Captura de pantalla en la que se muestra la solicitud para instalar un certificado SSL para permitir que Teams cargue la aplicación desde localhost.":::

1. <span data-ttu-id="59932-163">Se cargará Teams en un explorador web y se le pedirá que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="59932-163">Teams will be loaded in a web browser, and you will be prompted to sign in.</span></span> <span data-ttu-id="59932-164">Si se le pide que abra Microsoft Teams, seleccione Cancelar para permanecer en el explorador.</span><span class="sxs-lookup"><span data-stu-id="59932-164">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="59932-165">Inicie sesión con su cuenta de M365.</span><span class="sxs-lookup"><span data-stu-id="59932-165">Sign in with your M365 account.</span></span>

1. <span data-ttu-id="59932-166">Cuando se le pida que instale la aplicación en Teams, seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="59932-166">When prompted to install the app onto Teams, select **Add**.</span></span>

   <span data-ttu-id="59932-167">Ahora se mostrará su aplicación:</span><span class="sxs-lookup"><span data-stu-id="59932-167">Your app will now be displayed:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-completed-app.png" alt-text="Captura de pantalla de la aplicación completada":::

   <span data-ttu-id="59932-169">Puede realizar las actividades de depuración como si se tratase de cualquier otra aplicación web, como establecer puntos de interrupción.</span><span class="sxs-lookup"><span data-stu-id="59932-169">You can perform the debugging activities as if this were any other web application like setting breakpoints.</span></span> <span data-ttu-id="59932-170">La aplicación es compatible con "hot reloading".</span><span class="sxs-lookup"><span data-stu-id="59932-170">The app supports hot reloading.</span></span>  <span data-ttu-id="59932-171">Si cambia cualquier archivo dentro del proyecto, la página se volverá a cargar.</span><span class="sxs-lookup"><span data-stu-id="59932-171">If you change any file within the project, the page will be reloaded.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="59932-172">Vea lo que ocurre al ejecutar la aplicación localmente en el depurador.</span><span class="sxs-lookup"><span data-stu-id="59932-172">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="59932-173">Al presionar la tecla **F5,** el Teams Toolkit:</span><span class="sxs-lookup"><span data-stu-id="59932-173">When you press the **F5** key, the Teams Toolkit:</span></span>

1. <span data-ttu-id="59932-174">Registra la aplicación con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="59932-174">Registers your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="59932-175">Registra la aplicación para la "carga lateral" en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="59932-175">Registers your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="59932-176">Inicia el back-end de la aplicación ejecutándose localmente.</span><span class="sxs-lookup"><span data-stu-id="59932-176">Starts your application backend running locally.</span></span>
1. <span data-ttu-id="59932-177">Inicia la aplicación front-end hospedada localmente.</span><span class="sxs-lookup"><span data-stu-id="59932-177">Starts your application front-end hosted locally.</span></span>
1. <span data-ttu-id="59932-178">Inicia Microsoft Teams en un explorador web con un comando para indicar a Teams que cargue de lado la aplicación (la dirección URL está registrada dentro del manifiesto de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="59932-178">Starts Microsoft Teams in a web browser with a command to instruct Teams to side load the application (the URL is registered inside the application manifest).</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="59932-179">Vea cómo solucionar problemas comunes al ejecutar localmente la aplicación.</span><span class="sxs-lookup"><span data-stu-id="59932-179">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="59932-180">Para ejecutar correctamente la aplicación en Teams, debes tener una cuenta de desarrollo Microsoft 365 que permita la carga del lado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="59932-180">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app side loading.</span></span> <span data-ttu-id="59932-181">Para obtener más información sobre cómo abrir la cuenta, consulte [Requisitos previos](prerequisites.md#enable-sideloading).</span><span class="sxs-lookup"><span data-stu-id="59932-181">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

</details>

## <a name="deploy-your-app-to-azure"></a><span data-ttu-id="59932-182">Implementar la aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="59932-182">Deploy your app to Azure</span></span>

<span data-ttu-id="59932-183">La implementación consta de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="59932-183">Deployment consists of two steps:</span></span> 

1. <span data-ttu-id="59932-184">Se crean los recursos en la nube necesarios.</span><span class="sxs-lookup"><span data-stu-id="59932-184">Necessary cloud resources are created.</span></span> <span data-ttu-id="59932-185">Esto también se conoce como aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="59932-185">This is also known as provisioning.</span></span>
1. <span data-ttu-id="59932-186">Inicia la codificación y copia la aplicación en los recursos de nube creados.</span><span class="sxs-lookup"><span data-stu-id="59932-186">Start coding and copy your app into the created cloud resources.</span></span>

> <span data-ttu-id="59932-187">**Vista previa**</span><span class="sxs-lookup"><span data-stu-id="59932-187">**PREVIEW**</span></span>
>
> <span data-ttu-id="59932-188">La compatibilidad con aplicaciones de Blazor es nueva en Teams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="59932-188">Support for Blazor apps is new in Teams Toolkit.</span></span>  <span data-ttu-id="59932-189">El aprovisionamiento y la implementación se realizan con una combinación de Visual Studio 2019 y el Portal de desarrolladores para Teams.</span><span class="sxs-lookup"><span data-stu-id="59932-189">Provisioning and deployment are done with a combination of Visual Studio 2019 and the Developer Portal for Teams.</span></span>

## <a name="provision-and-deploy-your-app-to-azure-app-service"></a><span data-ttu-id="59932-190">Aprovisionar e implementar la aplicación en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="59932-190">Provision and deploy your app to Azure App Service</span></span>

1. <span data-ttu-id="59932-191">En el Explorador de soluciones, haga clic con el botón secundario en el nodo del proyecto y seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="59932-191">In Solution Explorer, right-click the project node and select **Publish**.</span></span> <span data-ttu-id="59932-192">También puede usar el elemento **de menú Generar**  >  **publicación.**</span><span class="sxs-lookup"><span data-stu-id="59932-192">You can also use the **Build** > **Publish** menu item.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish1.png" alt-text="Seleccione la operación Publicar en el proyecto":::

1. <span data-ttu-id="59932-194">En la **ventana Publicar,** **seleccione Azure** y selct **Next**.</span><span class="sxs-lookup"><span data-stu-id="59932-194">In the **Publish** window, select **Azure** and selct **Next**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish2.png" alt-text="Seleccionar Azure como destino de publicación":::

1. <span data-ttu-id="59932-196">Seleccione **Azure App Service (Windows)** y seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="59932-196">Select **Azure App Service (Windows)** and select **Next**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish3.png" alt-text="Seleccione Azure App Service como destino de publicación":::

1. <span data-ttu-id="59932-198">Seleccione **+** esta opción para crear una nueva instancia de App Service.</span><span class="sxs-lookup"><span data-stu-id="59932-198">Select **+** to create a new App Service instance.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish4.png" alt-text="Cree una nueva instancia.":::

1. <span data-ttu-id="59932-200">En el cuadro de diálogo Crear servicio de **aplicaciones (Windows),** se rellenan los campos de entrada **Nombre,** **Nombre** de **suscripción,** Grupo de recursos y **Plan** de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="59932-200">In the **Create App Service (Windows)** dialog, the **Name**, **Subscription name**, **Resource Group**, and **Hosting Plan** entry fields are populated.</span></span> <span data-ttu-id="59932-201">Si ya tienes un App Service en ejecución, se selecciona la configuración existente.</span><span class="sxs-lookup"><span data-stu-id="59932-201">If you have already got an App Service running, existing settings are selected.</span></span>  <span data-ttu-id="59932-202">Puede optar por crear un nuevo grupo de recursos y un plan de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="59932-202">You can opt to create a new resource group and hosting plan.</span></span>  <span data-ttu-id="59932-203">Cuando esté listo, seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="59932-203">When ready, select **Create**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish5.png" alt-text="Seleccionar plan de hospedaje y suscripción":::

1. <span data-ttu-id="59932-205">En el **cuadro de** diálogo Publicar, la instancia recién creada se ha seleccionado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="59932-205">In the **Publish** dialog, the newly created instance has been automatically selected.</span></span>  <span data-ttu-id="59932-206">Cuando esté listo, seleccione **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="59932-206">When ready, select **Finish**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish6.png" alt-text="Seleccione la nueva instancia.":::

1. <span data-ttu-id="59932-208">Seleccione el **icono Editar** (lápiz) junto al **Modo de** implementación y seleccione **Autocontenido**.</span><span class="sxs-lookup"><span data-stu-id="59932-208">Select the **Edit** (pencil) icon next to **Deployment Mode**, and select **Self-contained**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish8.png" alt-text="Seleccione modo de implementación independiente.":::

1. <span data-ttu-id="59932-210">Seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="59932-210">Select **Publish**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish7.png" alt-text="Publicar la aplicación en el servicio de aplicaciones":::

   <span data-ttu-id="59932-212">Visual Studio implementa la aplicación en Azure App Service y la aplicación web se carga en el explorador.</span><span class="sxs-lookup"><span data-stu-id="59932-212">Visual Studio deploys the app to your Azure App Service, and the web app loads in your browser.</span></span>  <span data-ttu-id="59932-213">Agregue `/tab` al final de la dirección URL para ver la página.</span><span class="sxs-lookup"><span data-stu-id="59932-213">Add `/tab` to the end of the URL to see your page.</span></span>

   <span data-ttu-id="59932-214">El panel **Publicar de propiedades** del proyecto muestra la dirección URL del sitio y otros detalles.</span><span class="sxs-lookup"><span data-stu-id="59932-214">The project properties **Publish** pane shows the site URL and other details.</span></span> <span data-ttu-id="59932-215">Anote la dirección URL del sitio.</span><span class="sxs-lookup"><span data-stu-id="59932-215">Make a note of the site URL.</span></span>

## <a name="create-an-environment-for-your-app"></a><span data-ttu-id="59932-216">Crear un entorno para la aplicación</span><span class="sxs-lookup"><span data-stu-id="59932-216">Create an environment for your app</span></span>

<span data-ttu-id="59932-217">El Portal para desarrolladores para Teams administra desde dónde se cargan las pestañas de la aplicación con un **entorno**.</span><span class="sxs-lookup"><span data-stu-id="59932-217">The Developer Portal for Teams manages where the tabs for your app are loaded from with an **Environment**.</span></span>  

<span data-ttu-id="59932-218">**Para crear un entorno:**</span><span class="sxs-lookup"><span data-stu-id="59932-218">**To create an environment:**</span></span>

1. <span data-ttu-id="59932-219">Abra el [Portal de desarrolladores para Teams](https://dev.teams.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="59932-219">Open the [Developer Portal for Teams](https://dev.teams.microsoft.com).</span></span>  <span data-ttu-id="59932-220">Inicie sesión con su cuenta administrativa M365.</span><span class="sxs-lookup"><span data-stu-id="59932-220">Sign in with your M365 administrative account.</span></span>

1. <span data-ttu-id="59932-221">En la barra lateral, selecciona **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="59932-221">From the sidebar, select **Apps**.</span></span>

1. <span data-ttu-id="59932-222">Si solo tienes una aplicación, se seleccionará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="59932-222">If you only have one app, it will be automatically selected.</span></span>  <span data-ttu-id="59932-223">Si no es así, selecciona la aplicación de la lista.</span><span class="sxs-lookup"><span data-stu-id="59932-223">If not, select your app from the list.</span></span>

1. <span data-ttu-id="59932-224">Seleccione **Entornos**.</span><span class="sxs-lookup"><span data-stu-id="59932-224">Select **Environments**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments1.png" alt-text="Seleccionar entornos":::

1. <span data-ttu-id="59932-226">Seleccione **Crear el primer entorno**.</span><span class="sxs-lookup"><span data-stu-id="59932-226">Select **Create your first environment**.</span></span>

1. <span data-ttu-id="59932-227">Escriba un nombre para el entorno y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="59932-227">Enter a name for your environment and select **Add**.</span></span> <span data-ttu-id="59932-228">Por ejemplo, `_Production_`.</span><span class="sxs-lookup"><span data-stu-id="59932-228">For example, `_Production_`.</span></span>

1. <span data-ttu-id="59932-229">Seleccione **Crear la primera variable de entorno**.</span><span class="sxs-lookup"><span data-stu-id="59932-229">Select **Create your first environment variable**.</span></span>

1. <span data-ttu-id="59932-230">Escriba `azure_app_url` para el **nombre**.</span><span class="sxs-lookup"><span data-stu-id="59932-230">Enter `azure_app_url` for the **Name**.</span></span>  <span data-ttu-id="59932-231">Escriba la dirección URL del sitio de Azure sin `https://` el valor **.**</span><span class="sxs-lookup"><span data-stu-id="59932-231">Enter your Azure site URL without the `https://` as the **Value**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments2.png" alt-text="Crear variable de entorno":::

   <span data-ttu-id="59932-233">Presione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="59932-233">Press **Add**.</span></span>

## <a name="update-the-app-manifest"></a><span data-ttu-id="59932-234">Actualizar el manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="59932-234">Update the app manifest</span></span>

<span data-ttu-id="59932-235">El manifiesto de la aplicación carga la pestaña desde una `localhost` dirección URL.</span><span class="sxs-lookup"><span data-stu-id="59932-235">The app manifest loads the tab from a `localhost` URL.</span></span>  <span data-ttu-id="59932-236">En esta sección, configurará el manifiesto de la aplicación para cargar la pestaña desde la dirección URL que aparece en el entorno que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="59932-236">In this section, you will configure the app manifest to load the tab from the URL listed within the environment you just created.</span></span>

1. <span data-ttu-id="59932-237">En la barra lateral, seleccione **Información básica**.</span><span class="sxs-lookup"><span data-stu-id="59932-237">From the sidebar, select **Basic information**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments3.png" alt-text="Seleccionar información básica":::

1. <span data-ttu-id="59932-239">Hay varios lugares dentro del manifiesto que enumera una `locahost:XXXXX` como parte de una dirección URL.</span><span class="sxs-lookup"><span data-stu-id="59932-239">There are several places within the manifest that list a `locahost:XXXXX` as part of a URL.</span></span>  <span data-ttu-id="59932-240">Reemplace todas las repeticiones por `{{azure_app_url}}` , incluidas las llaves.</span><span class="sxs-lookup"><span data-stu-id="59932-240">Replace all occurrences with `{{azure_app_url}}`, including the curly braces.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments4.png" alt-text="Ajustar la información básica del entorno":::

1. <span data-ttu-id="59932-242">Cuando haya finalizado, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="59932-242">When complete, select **Save**.</span></span>

1. <span data-ttu-id="59932-243">En la barra lateral, seleccione **Funcionalidades**.</span><span class="sxs-lookup"><span data-stu-id="59932-243">From the sidebar, select **Capabilities**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments5.png" alt-text="Seleccionar funcionalidades":::

1. <span data-ttu-id="59932-245">Seleccione **Ficha Personal**.</span><span class="sxs-lookup"><span data-stu-id="59932-245">Select **Personal Tab**.</span></span>
1. <span data-ttu-id="59932-246">Junto a la **pestaña Personal**, seleccione los puntos triples y, a continuación, **seleccione Editar**.</span><span class="sxs-lookup"><span data-stu-id="59932-246">Next to the **Personal Tab**, select the triple dots, then select **Edit**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments6.png" alt-text="Editar la configuración de pestañas personales":::

1. <span data-ttu-id="59932-248">Reemplace la dirección URL por la variable de entorno dentro de los campos **Dirección URL de contenido** y Dirección URL **del** sitio web.</span><span class="sxs-lookup"><span data-stu-id="59932-248">Replace the URL with the environment variable within the **Content Url** and **Website Url** fields.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments7.png" alt-text="Editar direcciones URL de pestañas personales":::

1. <span data-ttu-id="59932-250">Seleccione **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="59932-250">Select **Update**.</span></span>

1. <span data-ttu-id="59932-251">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="59932-251">Select **Save**.</span></span>

1. <span data-ttu-id="59932-252">En la barra lateral, seleccione **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="59932-252">From the sidebar, select **Single Sign-On**.</span></span>

1. <span data-ttu-id="59932-253">Reemplace el `localhost` URI de **id. de aplicación por** `{{azure_app_url}}` .</span><span class="sxs-lookup"><span data-stu-id="59932-253">Replace the `localhost` within the **Application ID URI** with `{{azure_app_url}}`.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments8.png" alt-text="Editar URI de id. de aplicación de inicio de sesión único":::

1. <span data-ttu-id="59932-255">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="59932-255">Select **Save**.</span></span>

1. <span data-ttu-id="59932-256">En la barra lateral, seleccione **Dominios**.</span><span class="sxs-lookup"><span data-stu-id="59932-256">From the sidebar, select **Domains**.</span></span>

1. <span data-ttu-id="59932-257">Seleccione **Agregar un dominio**.</span><span class="sxs-lookup"><span data-stu-id="59932-257">Select **Add a domain**.</span></span>

1. <span data-ttu-id="59932-258">Si `{{azure_app_url}}` no aparece como un dominio válido, agréelo como un dominio válido y, a continuación, seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="59932-258">If `{{azure_app_url}}` is not listed as a valid domain, add it as a valid domain, then select **Add**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments9.png" alt-text="Agregar un dominio":::

   <span data-ttu-id="59932-260">Ahora puedes usar la opción Vista previa **en Teams** en la parte superior de la página para iniciar la aplicación en Teams.</span><span class="sxs-lookup"><span data-stu-id="59932-260">You can now use the **Preview in Teams** option at the top of the page to launch your app within Teams.</span></span>

## <a name="see-also"></a><span data-ttu-id="59932-261">Vea también</span><span class="sxs-lookup"><span data-stu-id="59932-261">See also</span></span>

* [<span data-ttu-id="59932-262">Introducción a tutoriales</span><span class="sxs-lookup"><span data-stu-id="59932-262">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="59932-263">Crear una aplicación de bots de conversación</span><span class="sxs-lookup"><span data-stu-id="59932-263">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="59932-264">Crear una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="59932-264">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="59932-265">Muestras de código</span><span class="sxs-lookup"><span data-stu-id="59932-265">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)

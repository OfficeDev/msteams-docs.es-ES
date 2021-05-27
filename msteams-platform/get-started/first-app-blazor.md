---
title: 'Introducción: crea la primera aplicación Teams con Blazor'
author: adrianhall
description: Crea rápidamente una aplicación Microsoft Teams que muestre un "Hello, World!" con el Microsoft Teams Toolkit y .NET Blazor.
ms.author: adhal
ms.date: 04/27/2021
ms.topic: quickstart
ms.openlocfilehash: 6a9c7e008e2fb6d77c3314286b09d006bd468c37
ms.sourcegitcommit: 25c02757fe207cdff916ba63aa215f88e24e1d6f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/26/2021
ms.locfileid: "52667457"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-blazor"></a><span data-ttu-id="d8449-104">Crear y ejecutar la primera aplicación Microsoft Teams con Blazor</span><span class="sxs-lookup"><span data-stu-id="d8449-104">Build and run your first Microsoft Teams app with Blazor</span></span>

<span data-ttu-id="d8449-105">En este tutorial, crearás una nueva aplicación de Microsoft Teams en .NET/Blazor que implementa una aplicación personal sencilla para extraer información de microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="d8449-105">In this tutorial, you will create a new Microsoft Teams app in .NET/Blazor that implements a simple personal app to pull information from the Microsoft Graph.</span></span> <span data-ttu-id="d8449-106">(Una *aplicación personal* incluye un conjunto de pestañas con ámbito para uso individual).  Durante el tutorial, aprenderás sobre la estructura de una aplicación Teams, cómo ejecutar una aplicación localmente y cómo implementar la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="d8449-106">(A *personal app* includes a set of tabs scoped for individual use.)  During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to Azure.</span></span>

<span data-ttu-id="d8449-107">La aplicación que se ha creado muestra información básica del usuario para el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="d8449-107">The app that is built displays basic user information for the current user.</span></span>  <span data-ttu-id="d8449-108">Cuando se concede permiso, la aplicación se conectará a microsoft Graph como el usuario actual para obtener el perfil completo.</span><span class="sxs-lookup"><span data-stu-id="d8449-108">When permission is granted, the app will connect to the Microsoft Graph as the current user to get the complete profile.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d8449-109">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="d8449-109">Before you begin</span></span>

<span data-ttu-id="d8449-110">Asegúrese de que el entorno de desarrollo está configurado mediante la instalación de los [requisitos previos](prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="d8449-110">Make sure your development environment is set up by installing the [prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d8449-111">Requisitos previos para la instalación</span><span class="sxs-lookup"><span data-stu-id="d8449-111">Install prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="d8449-112">Crear el proyecto</span><span class="sxs-lookup"><span data-stu-id="d8449-112">Create your project</span></span>

<span data-ttu-id="d8449-113">Use el Teams Toolkit para crear el primer proyecto:</span><span class="sxs-lookup"><span data-stu-id="d8449-113">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="d8449-114">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="d8449-114">Visual Studio 2019</span></span>](#tab/vs)

1. <span data-ttu-id="d8449-115">Abra Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="d8449-115">Open Visual Studio 2019.</span></span>

1. <span data-ttu-id="d8449-116">Seleccione **Crear un nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="d8449-116">Select **Create a new project**.</span></span>

1. <span data-ttu-id="d8449-117">Seleccione **Microsoft Teams app y,** a continuación, presione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d8449-117">Select **Microsoft Teams App**, then press **Next**.</span></span>  <span data-ttu-id="d8449-118">Para ayudarle a encontrar la plantilla, use el tipo de **proyecto Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="d8449-118">To help you find the template, use the project type **Microsoft Teams**.</span></span>

1. <span data-ttu-id="d8449-119">Asigne un buen nombre al proyecto y a la solución y, a continuación, presione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d8449-119">Give the project and solution a good name, then press **Next**.</span></span>

1. <span data-ttu-id="d8449-120">Proporcione el nombre de la aplicación y el nombre de la compañía y, a continuación, presione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d8449-120">Provide the application name and company name, then press **Create**.</span></span>  <span data-ttu-id="d8449-121">El nombre de la aplicación y el nombre de la compañía se muestran a los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="d8449-121">The application name and company name are displayed to your end users.</span></span>

1. <span data-ttu-id="d8449-122">La Teams se creará en unos segundos.</span><span class="sxs-lookup"><span data-stu-id="d8449-122">Your Teams app will be created within a few seconds.</span></span>  <span data-ttu-id="d8449-123">Una vez creado el proyecto, configure el inicio de sesión único con M365:</span><span class="sxs-lookup"><span data-stu-id="d8449-123">Once the project is created, set up single sign-on with M365:</span></span>

   - <span data-ttu-id="d8449-124">Seleccione **Project**  >  **Configuración de TeamsFx** para  >  **SSO...**.</span><span class="sxs-lookup"><span data-stu-id="d8449-124">Select **Project** > **TeamsFx** > **Configure for SSO...**.</span></span>
   - <span data-ttu-id="d8449-125">Cuando se le pida, inicie sesión en su cuenta de administrador de M365.</span><span class="sxs-lookup"><span data-stu-id="d8449-125">When prompted, sign in to your M365 administrator account.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="d8449-126">Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="d8449-126">Command line</span></span>](#tab/cli)

1. <span data-ttu-id="d8449-127">Abra un terminal y seleccione el directorio donde desea crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="d8449-127">Open a Terminal and select the directory where you wish to create the project.</span></span>

1. <span data-ttu-id="d8449-128">Ejecute `dotnet new -i` para instalar la plantilla desde NuGet:</span><span class="sxs-lookup"><span data-stu-id="d8449-128">Run `dotnet new -i` to install the template from NuGet:</span></span>

   ``` bash
   dotnet new --install Microsoft.TeamsFx.VisualStudio.ProjectTemplates::0.1.43-beta
   ```

   <span data-ttu-id="d8449-129">Solo tiene que hacerlo la primera vez o al actualizar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="d8449-129">You only need to do this the first time or when updating the template.</span></span> <span data-ttu-id="d8449-130">Compruebe [NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/) la versión más reciente de este paquete.</span><span class="sxs-lookup"><span data-stu-id="d8449-130">Check [NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/) for the latest version of this package.</span></span>

1. <span data-ttu-id="d8449-131">Crear un directorio:</span><span class="sxs-lookup"><span data-stu-id="d8449-131">Create a directory:</span></span>

   ``` bash
   mkdir helloworld
   ```

1. <span data-ttu-id="d8449-132">Ejecute `dotnet new` para crear un nuevo proyecto:</span><span class="sxs-lookup"><span data-stu-id="d8449-132">Run `dotnet new` to create a new project:</span></span>

   ``` bash
   dotnet new teamsapp --shortName my-teams-app --companyName "My Company"
   ```

1. <span data-ttu-id="d8449-133">Una vez scaffolded, configure el proyecto para Teams implementación:</span><span class="sxs-lookup"><span data-stu-id="d8449-133">Once scaffolded, configure the project for Teams deployment:</span></span>

   ``` bash
   teamsfx init
   ```

<span data-ttu-id="d8449-134">Ahora puede abrir la solución en Visual Studio para la depuración.</span><span class="sxs-lookup"><span data-stu-id="d8449-134">You can now open the solution in Visual Studio for debugging.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="d8449-135">Realizar un recorrido por el código fuente</span><span class="sxs-lookup"><span data-stu-id="d8449-135">Take a tour of the source code</span></span>

<span data-ttu-id="d8449-136">Si quieres omitir esta sección por ahora, puedes [ejecutar la aplicación localmente.](#run-your-app-locally)</span><span class="sxs-lookup"><span data-stu-id="d8449-136">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="d8449-137">Una vez Teams Toolkit configurar el proyecto, tienes los componentes para crear una aplicación personal básica para Teams.</span><span class="sxs-lookup"><span data-stu-id="d8449-137">Once the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams.</span></span> <span data-ttu-id="d8449-138">Los directorios y archivos del proyecto se muestran en el área Explorador de soluciones de Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="d8449-138">The project directories and files display in the Solution Explorer area of Visual Studio 2019.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/blazor-file-layout.png" alt-text="Captura de pantalla que muestra los archivos de proyecto de la aplicación para una aplicación personal en Visual Studio 2019.":::

- <span data-ttu-id="d8449-140">Los iconos de la aplicación se almacenan como archivos PNG `color.png` en y `outline.png` .</span><span class="sxs-lookup"><span data-stu-id="d8449-140">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="d8449-141">El manifiesto de la aplicación para publicar a través del Portal de desarrolladores para Teams se almacena en `Properties/manifest.json` .</span><span class="sxs-lookup"><span data-stu-id="d8449-141">The app manifest for publishing through the Developer Portal for Teams is stored in `Properties/manifest.json`.</span></span>
- <span data-ttu-id="d8449-142">Se proporciona un controlador back-end `Controllers/BackendController.cs` para ayudar con la autenticación.</span><span class="sxs-lookup"><span data-stu-id="d8449-142">A backend controller is provided in `Controllers/BackendController.cs` for assisting with authentication.</span></span>

<span data-ttu-id="d8449-143">Desde que creaste una aplicación de pestaña durante la instalación, Teams Toolkit scaffolding todo el código necesario para una pestaña básica como [un servidor de Blazor](/aspnet/core/blazor).</span><span class="sxs-lookup"><span data-stu-id="d8449-143">Since you created a tab app during setup, the Teams Toolkit scaffolds all the necessary code for a basic tab as a [Blazor Server](/aspnet/core/blazor).</span></span>

- <span data-ttu-id="d8449-144">`Pages/Tab.razor` es el punto de entrada de la aplicación front-end.</span><span class="sxs-lookup"><span data-stu-id="d8449-144">`Pages/Tab.razor` is the front-end application's entry point.</span></span>
- <span data-ttu-id="d8449-145">`TeamsFx.cs`y `JS/src/index.js` se usa para inicializar las comunicaciones con el Teams host.</span><span class="sxs-lookup"><span data-stu-id="d8449-145">`TeamsFx.cs` and `JS/src/index.js` is used for initializing communications with the Teams host.</span></span>

<span data-ttu-id="d8449-146">Puede agregar funcionalidad back-end agregando controladores ASP.NET Core adicionales a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8449-146">You can add backend functionality by adding additional ASP.NET Core controllers to your application.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="d8449-147">Ejecutar la aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="d8449-147">Run your app locally</span></span>

<span data-ttu-id="d8449-148">Teams Toolkit permite ejecutar la aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="d8449-148">Teams Toolkit allows you to run your app locally.</span></span>  <span data-ttu-id="d8449-149">Se trata de varias partes necesarias para proporcionar la infraestructura correcta que Teams espera:</span><span class="sxs-lookup"><span data-stu-id="d8449-149">This consists of several parts that are necessary to provide the correct infrastructure that Teams expects:</span></span>

- <span data-ttu-id="d8449-150">Una aplicación está registrada con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d8449-150">An application is registered with Azure Active Directory.</span></span>  <span data-ttu-id="d8449-151">Esta aplicación tiene permisos asociados con la ubicación desde la que se carga la aplicación y los recursos back-end a los que tiene acceso.</span><span class="sxs-lookup"><span data-stu-id="d8449-151">This application has permissions associated with the location that the app is loaded from and any backend resources it accesses.</span></span>
- <span data-ttu-id="d8449-152">Una API web se hospeda (a través de IIS Express) para ayudar con las tareas de autenticación, actuando como proxy entre la aplicación y Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d8449-152">A web API is hosted (via IIS Express) to assist with authentication tasks, acting as a proxy between the app and Azure Active Directory.</span></span>  
- <span data-ttu-id="d8449-153">Se genera un manifiesto de aplicación y existe en el Portal de desarrolladores para Teams.</span><span class="sxs-lookup"><span data-stu-id="d8449-153">An app manifest is generated and exists in the Developer Portal for Teams.</span></span>  <span data-ttu-id="d8449-154">Teams el manifiesto de la aplicación para decir a los clientes conectados desde dónde cargar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8449-154">Teams uses the app manifest to tell connected clients where to load the app from.</span></span>

<span data-ttu-id="d8449-155">Una vez hecho esto, la aplicación se puede cargar en el Teams cliente.</span><span class="sxs-lookup"><span data-stu-id="d8449-155">Once this is done, the app can be loaded within the Teams client.</span></span>  <span data-ttu-id="d8449-156">Usamos el Teams web para que podamos ver el código HTML, CSS y JavaScript dentro de un entorno de desarrollo web estándar.</span><span class="sxs-lookup"><span data-stu-id="d8449-156">We use the Teams web client so that we can see the HTML, CSS, and JavaScript code within a standard web development environment.</span></span>

<span data-ttu-id="d8449-157">Para compilar y ejecutar la aplicación localmente:</span><span class="sxs-lookup"><span data-stu-id="d8449-157">To build and run your app locally:</span></span>

1. <span data-ttu-id="d8449-158">Desde Visual Studio Code, presione **F5** para ejecutar la aplicación en modo de depuración.</span><span class="sxs-lookup"><span data-stu-id="d8449-158">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

1. <span data-ttu-id="d8449-159">Si se solicita, instale el certificado SSL autofirmado para la depuración local.</span><span class="sxs-lookup"><span data-stu-id="d8449-159">If requested, install the self-signed SSL certificate for local debugging.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Captura de pantalla que muestra cómo se indica cómo instalar un certificado SSL para Teams cargar la aplicación desde localhost.":::

1. <span data-ttu-id="d8449-161">Teams se cargará en un explorador web y se le pedirá que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="d8449-161">Teams will be loaded in a web browser, and you will be prompted to sign in.</span></span> <span data-ttu-id="d8449-162">Si se le pide que abra Microsoft Teams, seleccione Cancelar para permanecer en el explorador.</span><span class="sxs-lookup"><span data-stu-id="d8449-162">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="d8449-163">Inicie sesión con su cuenta M365.</span><span class="sxs-lookup"><span data-stu-id="d8449-163">Sign in with your M365 account.</span></span>
1. <span data-ttu-id="d8449-164">Cuando se le pida que instale la aplicación en Teams, presione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d8449-164">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="d8449-165">Ahora se mostrará la aplicación:</span><span class="sxs-lookup"><span data-stu-id="d8449-165">Your app will now be displayed:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/blazor-completed-app.png" alt-text="Captura de pantalla de la aplicación completada":::

<span data-ttu-id="d8449-167">Puede realizar actividades de depuración normales como si se tratase de cualquier otra aplicación web (como establecer puntos de interrupción).</span><span class="sxs-lookup"><span data-stu-id="d8449-167">You can do normal debugging activities as if this were any other web application (such as setting breakpoints).</span></span> <span data-ttu-id="d8449-168">La aplicación admite la recarga en caliente.</span><span class="sxs-lookup"><span data-stu-id="d8449-168">The app supports hot reloading.</span></span>  <span data-ttu-id="d8449-169">Si cambia cualquier archivo dentro del proyecto, la página se volverá a cargar.</span><span class="sxs-lookup"><span data-stu-id="d8449-169">If you change any file within the project, the page will be reloaded.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="d8449-170">Obtén información sobre lo que sucede cuando ejecutas la aplicación localmente en el depurador.</span><span class="sxs-lookup"><span data-stu-id="d8449-170">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="d8449-171">Al presionar F5, el Teams Toolkit:</span><span class="sxs-lookup"><span data-stu-id="d8449-171">When you pressed F5, the Teams Toolkit:</span></span>

1. <span data-ttu-id="d8449-172">Registró la aplicación con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d8449-172">Registered your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="d8449-173">Registró la aplicación para la "carga lateral" en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d8449-173">Registered your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="d8449-174">Inició el back-end de la aplicación ejecutándose localmente.</span><span class="sxs-lookup"><span data-stu-id="d8449-174">Started your application backend running locally.</span></span>
1. <span data-ttu-id="d8449-175">Inició la aplicación front-end hospedada localmente.</span><span class="sxs-lookup"><span data-stu-id="d8449-175">Started your application front-end hosted locally.</span></span>
1. <span data-ttu-id="d8449-176">Se Microsoft Teams en un explorador web con un comando para indicar a Teams cargar de forma lateral la aplicación (la dirección URL está registrada dentro del manifiesto de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="d8449-176">Started Microsoft Teams in a web browser with a command to instruct Teams to side load the application (the URL is registered inside the application manifest).</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="d8449-177">Obtén información sobre cómo solucionar problemas comunes al ejecutar la aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="d8449-177">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="d8449-178">Para ejecutar correctamente la aplicación en Teams, debes tener una cuenta de desarrollo Microsoft 365 que permita la carga del lado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8449-178">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app side loading.</span></span> <span data-ttu-id="d8449-179">Para obtener más información sobre la apertura de cuentas, vea [Prerequisites](prerequisites.md#enable-sideloading).</span><span class="sxs-lookup"><span data-stu-id="d8449-179">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

</details>

## <a name="deploy-your-app-to-azure"></a><span data-ttu-id="d8449-180">Implementar la aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="d8449-180">Deploy your app to Azure</span></span>

<span data-ttu-id="d8449-181">La implementación consta de dos pasos.</span><span class="sxs-lookup"><span data-stu-id="d8449-181">Deployment consists of two steps.</span></span>  <span data-ttu-id="d8449-182">En primer lugar, se crean los recursos en la nube necesarios (también conocidos como aprovisionamiento) y, a continuación, el código que forma la aplicación se copia en los recursos de nube creados.</span><span class="sxs-lookup"><span data-stu-id="d8449-182">First, necessary cloud resources are created (also known as provisioning), then the code that makes up your app is copied into the created cloud resources.</span></span>

> <span data-ttu-id="d8449-183">**Vista previa**</span><span class="sxs-lookup"><span data-stu-id="d8449-183">**PREVIEW**</span></span>
>
> <span data-ttu-id="d8449-184">La compatibilidad con aplicaciones de Blazor es nueva en Teams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="d8449-184">Support for Blazor apps is new in Teams Toolkit.</span></span>  <span data-ttu-id="d8449-185">El aprovisionamiento y la implementación se realizan con una combinación de Visual Studio 2019 y el Portal de desarrolladores para Teams.</span><span class="sxs-lookup"><span data-stu-id="d8449-185">Provisioning and deployment are done with a combination of Visual Studio 2019 and the Developer Portal for Teams.</span></span>

## <a name="provision-and-deploy-your-app-to-azure-app-service"></a><span data-ttu-id="d8449-186">Aprovisionar e implementar la aplicación en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d8449-186">Provision and deploy your app to Azure App Service</span></span>

1. <span data-ttu-id="d8449-187">En el Explorador de soluciones, haga clic con el botón secundario en el nodo del proyecto y elija **Publicar** (o use el elemento **de** menú  >  **Generar publicación).**</span><span class="sxs-lookup"><span data-stu-id="d8449-187">In Solution Explorer, right-click the project node and choose **Publish** (or use the **Build** > **Publish** menu item).</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish1.png" alt-text="Seleccione la operación Publicar en el proyecto":::

1. <span data-ttu-id="d8449-189">En la **ventana Publicar,** seleccione **Azure**.</span><span class="sxs-lookup"><span data-stu-id="d8449-189">In the **Publish** window, select **Azure**.</span></span>  <span data-ttu-id="d8449-190">Presione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d8449-190">Press **Next**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish2.png" alt-text="Seleccionar Azure como destino de publicación":::

1. <span data-ttu-id="d8449-192">Seleccione **Azure App Service (Windows).**</span><span class="sxs-lookup"><span data-stu-id="d8449-192">Select **Azure App Service (Windows)**.</span></span>  <span data-ttu-id="d8449-193">Presione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d8449-193">Press **Next**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish3.png" alt-text="Seleccione Azure App Service como destino de publicación":::

1. <span data-ttu-id="d8449-195">Seleccione **+** esta opción para crear una nueva instancia de App Service.</span><span class="sxs-lookup"><span data-stu-id="d8449-195">Select **+** to create a new App Service instance.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish4.png" alt-text="Cree una nueva instancia.":::

1. <span data-ttu-id="d8449-197">En el cuadro de diálogo Crear servicio de **aplicaciones (Windows),** se rellenan los campos de entrada **Nombre,** **Nombre** de **suscripción,** Grupo de recursos y **Plan** de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="d8449-197">In the **Create App Service (Windows)** dialog, the **Name**, **Subscription name**, **Resource Group**, and **Hosting Plan** entry fields are populated.</span></span> <span data-ttu-id="d8449-198">Si ya tienes un App Service en ejecución, se seleccionará la configuración existente.</span><span class="sxs-lookup"><span data-stu-id="d8449-198">If you have already got an App Service running, existing settings will be selected.</span></span>  <span data-ttu-id="d8449-199">Puede optar por crear un nuevo grupo de recursos y un plan de hospedaje (recomendado).</span><span class="sxs-lookup"><span data-stu-id="d8449-199">You can opt to create a new resource group and hosting plan (Recommended).</span></span>  <span data-ttu-id="d8449-200">Cuando esté listo, seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d8449-200">When ready, select **Create**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish5.png" alt-text="Seleccionar plan de hospedaje y suscripción":::

1. <span data-ttu-id="d8449-202">En el **cuadro de** diálogo Publicar, la instancia recién creada se ha seleccionado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="d8449-202">In the **Publish** dialog, the newly created instance has been automatically selected.</span></span>  <span data-ttu-id="d8449-203">Cuando esté listo, seleccione **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="d8449-203">When ready, select **Finish**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish6.png" alt-text="Seleccione la nueva instancia.":::

1. <span data-ttu-id="d8449-205">Presione el **icono Editar** (lápiz) junto al Modo **de implementación** y, a continuación, **seleccione Autocontenido**.</span><span class="sxs-lookup"><span data-stu-id="d8449-205">Press the **Edit** (pencil) icon next to **Deployment Mode**, then select **Self-contained**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish8.png" alt-text="Seleccione modo de implementación independiente.":::

1. <span data-ttu-id="d8449-207">Seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="d8449-207">Select **Publish**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish7.png" alt-text="Publicar la aplicación en el servicio de aplicaciones":::

<span data-ttu-id="d8449-209">Visual Studio implementa la aplicación en Azure App Service y la aplicación web se carga en el explorador.</span><span class="sxs-lookup"><span data-stu-id="d8449-209">Visual Studio deploys the app to your Azure App Service, and the web app loads in your browser.</span></span>  <span data-ttu-id="d8449-210">Agregue `/tab` al final de la dirección URL para ver la página.</span><span class="sxs-lookup"><span data-stu-id="d8449-210">Add `/tab` to the end of the URL to see your page.</span></span>

<span data-ttu-id="d8449-211">El panel **Publicar de propiedades** del proyecto muestra la dirección URL del sitio y otros detalles.</span><span class="sxs-lookup"><span data-stu-id="d8449-211">The project properties **Publish** pane shows the site URL and other details.</span></span> <span data-ttu-id="d8449-212">Anote la dirección URL del sitio.</span><span class="sxs-lookup"><span data-stu-id="d8449-212">Make a note of the site URL.</span></span>

## <a name="create-an-environment-for-your-app"></a><span data-ttu-id="d8449-213">Crear un entorno para la aplicación</span><span class="sxs-lookup"><span data-stu-id="d8449-213">Create an environment for your app</span></span>

<span data-ttu-id="d8449-214">El Portal para desarrolladores para Teams administra desde dónde se cargan las pestañas de la aplicación con un **entorno**.</span><span class="sxs-lookup"><span data-stu-id="d8449-214">The Developer Portal for Teams manages where the tabs for your app are loaded from with an **Environment**.</span></span>  <span data-ttu-id="d8449-215">Para crear un entorno:</span><span class="sxs-lookup"><span data-stu-id="d8449-215">To create an environment:</span></span>

1. <span data-ttu-id="d8449-216">Abra el [Portal de desarrolladores para Teams](https://dev.teams.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="d8449-216">Open the [Developer Portal for Teams](https://dev.teams.microsoft.com).</span></span>  <span data-ttu-id="d8449-217">Inicie sesión con su cuenta administrativa M365.</span><span class="sxs-lookup"><span data-stu-id="d8449-217">Sign in with your M365 administrative account.</span></span>

1. <span data-ttu-id="d8449-218">En la barra lateral, selecciona **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d8449-218">From the sidebar, select **Apps**.</span></span>

1. <span data-ttu-id="d8449-219">Si solo tienes una aplicación, se seleccionará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="d8449-219">If you only have one app, it will be automatically selected.</span></span>  <span data-ttu-id="d8449-220">Si no es así, selecciona la aplicación de la lista.</span><span class="sxs-lookup"><span data-stu-id="d8449-220">If not, select your app from the list.</span></span>

1. <span data-ttu-id="d8449-221">Seleccione **Entornos**.</span><span class="sxs-lookup"><span data-stu-id="d8449-221">Select **Environments**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments1.png" alt-text="Seleccionar entornos":::

1. <span data-ttu-id="d8449-223">Seleccione **Crear el primer entorno**.</span><span class="sxs-lookup"><span data-stu-id="d8449-223">Select **Create your first environment**.</span></span>

1. <span data-ttu-id="d8449-224">Escriba un nombre para el entorno y, a continuación, **presione Agregar**; por ejemplo _Producción_.</span><span class="sxs-lookup"><span data-stu-id="d8449-224">Enter a name for your environment, then press **Add**; for example _Production_.</span></span>

1. <span data-ttu-id="d8449-225">Con el entorno recién creado seleccionado, presione **Crear la primera variable de entorno**.</span><span class="sxs-lookup"><span data-stu-id="d8449-225">With the newly created environment selected, press **Create your first environment variable**.</span></span>

1. <span data-ttu-id="d8449-226">Escriba `azure_app_url` para el **nombre**.</span><span class="sxs-lookup"><span data-stu-id="d8449-226">Enter `azure_app_url` for the **Name**.</span></span>  <span data-ttu-id="d8449-227">Escriba la dirección URL del sitio de Azure (sin `https://` la ) como **valor**.</span><span class="sxs-lookup"><span data-stu-id="d8449-227">Enter your Azure site URL (without the `https://`) as the **Value**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments2.png" alt-text="Crear variable de entorno":::

   <span data-ttu-id="d8449-229">Presione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d8449-229">Press **Add**.</span></span>

## <a name="update-the-app-manifest"></a><span data-ttu-id="d8449-230">Actualizar el manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="d8449-230">Update the app manifest</span></span>

<span data-ttu-id="d8449-231">El manifiesto de la aplicación está cargando la pestaña desde una `localhost` dirección URL.</span><span class="sxs-lookup"><span data-stu-id="d8449-231">The app manifest is loading the tab from a `localhost` URL.</span></span>  <span data-ttu-id="d8449-232">En esta sección, ajustará el manifiesto de la aplicación para cargar la pestaña desde la dirección URL que aparece en el entorno que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="d8449-232">In this section, you will adjust the app manifest to load the tab from the URL listed within the environment you just created.</span></span>

1. <span data-ttu-id="d8449-233">En la barra lateral, seleccione **Información básica**.</span><span class="sxs-lookup"><span data-stu-id="d8449-233">From the sidebar, select **Basic information**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments3.png" alt-text="Seleccionar información básica":::

1. <span data-ttu-id="d8449-235">Hay varios lugares dentro del manifiesto que enumera una `locahost:XXXXX` como parte de una dirección URL.</span><span class="sxs-lookup"><span data-stu-id="d8449-235">There are several places within the manifest that list a `locahost:XXXXX` as part of a URL.</span></span>  <span data-ttu-id="d8449-236">Reemplace todas las repeticiones `{{azure_app_url}}` con (incluidas las llaves).</span><span class="sxs-lookup"><span data-stu-id="d8449-236">Replace all occurrences with `{{azure_app_url}}` (including the curly braces).</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments4.png" alt-text="Ajustar la información básica del entorno":::

1. <span data-ttu-id="d8449-238">Cuando haya finalizado, presione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d8449-238">When complete, press **Save**.</span></span>

1. <span data-ttu-id="d8449-239">En la barra lateral, seleccione **Funcionalidades**.</span><span class="sxs-lookup"><span data-stu-id="d8449-239">From the sidebar, select **Capabilities**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments5.png" alt-text="Seleccionar funcionalidades":::

1. <span data-ttu-id="d8449-241">Seleccione **Ficha Personal**.</span><span class="sxs-lookup"><span data-stu-id="d8449-241">Select **Personal Tab**.</span></span>
1. <span data-ttu-id="d8449-242">Junto a la **pestaña Personal**, seleccione los puntos triples y, a continuación, **seleccione Editar**.</span><span class="sxs-lookup"><span data-stu-id="d8449-242">Next to the **Personal Tab**, select the triple dots, then select **Edit**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments6.png" alt-text="Editar la configuración de pestañas personales":::

1. <span data-ttu-id="d8449-244">Reemplace la dirección URL por la variable de entorno dentro de los campos **Dirección URL de contenido** y Dirección URL **del** sitio web.</span><span class="sxs-lookup"><span data-stu-id="d8449-244">Replace the URL with the environment variable within the **Content Url** and **Website Url** fields.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments7.png" alt-text="Editar direcciones URL de pestañas personales":::

1. <span data-ttu-id="d8449-246">Presione **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="d8449-246">Press **Update**.</span></span>

1. <span data-ttu-id="d8449-247">Presione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d8449-247">Press **Save**.</span></span>

1. <span data-ttu-id="d8449-248">En la barra lateral, seleccione **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="d8449-248">From the sidebar, select **Single Sign-On**.</span></span>

1. <span data-ttu-id="d8449-249">Reemplace el `localhost` URI de **id. de aplicación por** `{{azure_app_url}}` .</span><span class="sxs-lookup"><span data-stu-id="d8449-249">Replace the `localhost` within the **Application ID URI** with `{{azure_app_url}}`.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments8.png" alt-text="Editar URI de id. de aplicación de inicio de sesión único":::

1. <span data-ttu-id="d8449-251">Presione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d8449-251">Press **Save**.</span></span>

1. <span data-ttu-id="d8449-252">En la barra lateral, presione **Dominios**.</span><span class="sxs-lookup"><span data-stu-id="d8449-252">From the sidebar, press **Domains**.</span></span>

1. <span data-ttu-id="d8449-253">Presione **Agregar un dominio**.</span><span class="sxs-lookup"><span data-stu-id="d8449-253">Press **Add a domain**.</span></span>

1. <span data-ttu-id="d8449-254">Si `{{azure_app_url}}` no aparece como un dominio válido, agrégrelo como un dominio válido y, a continuación, presione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d8449-254">If `{{azure_app_url}}` is not listed as a valid domain, add it as a valid domain, then press **Add**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments9.png" alt-text="Agregar un dominio":::

<span data-ttu-id="d8449-256">Ahora puedes usar el botón Vista previa **en Teams** en la parte superior de la página para iniciar la aplicación en Teams.</span><span class="sxs-lookup"><span data-stu-id="d8449-256">You can now use the **Preview in Teams** button at the top of the page to launch your app within Teams.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8449-257">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d8449-257">Next steps</span></span>

<span data-ttu-id="d8449-258">Obtenga información sobre otros métodos para crear Teams aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="d8449-258">Learn about other methods for creating Teams apps:</span></span>

- [<span data-ttu-id="d8449-259">Crear una aplicación Teams con React</span><span class="sxs-lookup"><span data-stu-id="d8449-259">Create a Teams app with React</span></span>](first-app-react.md)
- <span data-ttu-id="d8449-260">[Crear una aplicación Teams como elemento SharePoint web](first-app-spfx.md) (No es necesario Azure)</span><span class="sxs-lookup"><span data-stu-id="d8449-260">[Create a Teams app as a SharePoint Web Part](first-app-spfx.md) (Azure not required)</span></span>
- [<span data-ttu-id="d8449-261">Crear una aplicación de bot conversacional</span><span class="sxs-lookup"><span data-stu-id="d8449-261">Create a conversational bot app</span></span>](first-app-bot.md)
- [<span data-ttu-id="d8449-262">Crear una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="d8449-262">Create a messaging extension</span></span>](first-message-extension.md)

---
title: 'Introducción: crea la primera aplicación Teams con SPFx'
author: zhenyasav
description: Obtenga información sobre cómo crear una pestaña personalizada con el SharePoint Framework
ms.author: zhenyasa
ms.date: 05/19/2021
ms.topic: quickstart
ms.openlocfilehash: 54886b47bbe70fed5dd1f010517e6c91d8d5a50d
ms.sourcegitcommit: 9cabeaed9baf96c8caeb1497f0bc37abdb787d22
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2021
ms.locfileid: "52646862"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-sharepoint-framework-spfx"></a><span data-ttu-id="52523-103">Compila y ejecuta la primera aplicación Microsoft Teams con SharePoint Framework (SPFx)</span><span class="sxs-lookup"><span data-stu-id="52523-103">Build and run your first Microsoft Teams app with SharePoint Framework (SPFx)</span></span>

<span data-ttu-id="52523-104">En este tutorial, crearás una nueva aplicación Microsoft Teams en SharePoint Framework (SPFx) que implemente una aplicación personal sencilla.</span><span class="sxs-lookup"><span data-stu-id="52523-104">In this tutorial, you will create a new Microsoft Teams app in SharePoint Framework (SPFx) that implements a simple personal app.</span></span> <span data-ttu-id="52523-105">(Una *aplicación personal* incluye un conjunto de pestañas con ámbito para uso individual). Durante el tutorial, aprenderás sobre la estructura de una aplicación Teams, cómo ejecutar la aplicación localmente y cómo implementar la aplicación en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="52523-105">(A *personal app* includes a set of tabs scoped for individual use.) During the tutorial, you will learn about the structure of a Teams app, how to run the app locally, and how to deploy the app to SharePoint.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="52523-106">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="52523-106">Before you begin</span></span>

<span data-ttu-id="52523-107">Asegúrese de que el entorno de desarrollo está configurado mediante la instalación de los [requisitos previos](prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="52523-107">Make sure your development environment is set up by installing the [prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="52523-108">Requisitos previos para la instalación</span><span class="sxs-lookup"><span data-stu-id="52523-108">Install prerequisites</span></span>](prerequisites.md)

## <a name="get-organized"></a><span data-ttu-id="52523-109">Organizarse</span><span class="sxs-lookup"><span data-stu-id="52523-109">Get organized</span></span>

<span data-ttu-id="52523-110">Además de los requisitos previos, también debe ser administrador de una colección SharePoint de sitios.</span><span class="sxs-lookup"><span data-stu-id="52523-110">In addition to the prerequisites, you also need to be an Administrator for a SharePoint Site Collection.</span></span>  <span data-ttu-id="52523-111">Aquí es donde implementará la aplicación para el hospedaje.</span><span class="sxs-lookup"><span data-stu-id="52523-111">This is where you will deploy your app for hosting.</span></span>  <span data-ttu-id="52523-112">Si usa un inquilino del programa para desarrolladores M365, use la cuenta de administrador que haya configurado al registrarse en el programa.</span><span class="sxs-lookup"><span data-stu-id="52523-112">If you are using an M365 developer program tenant, use the administrator account you set up when you registered for the program.</span></span>  

## <a name="create-your-project"></a><span data-ttu-id="52523-113">Crear el proyecto</span><span class="sxs-lookup"><span data-stu-id="52523-113">Create your project</span></span>

<span data-ttu-id="52523-114">Use el Teams Toolkit para crear el primer proyecto:</span><span class="sxs-lookup"><span data-stu-id="52523-114">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="52523-115">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="52523-115">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="52523-116">Abra Visual Studio código.</span><span class="sxs-lookup"><span data-stu-id="52523-116">Open Visual Studio code.</span></span>
1. <span data-ttu-id="52523-117">Abra el Teams Toolkit seleccionando el icono Teams en la barra lateral:</span><span class="sxs-lookup"><span data-stu-id="52523-117">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icono Teams en la barra lateral Visual Studio Code barra lateral.":::

1. <span data-ttu-id="52523-119">Seleccione **Crear nuevo Project**.</span><span class="sxs-lookup"><span data-stu-id="52523-119">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Ubicación del vínculo Create New Project en la barra lateral Teams Toolkit barra lateral.":::

1. <span data-ttu-id="52523-121">Selecciona **Crear una nueva Teams aplicación**.</span><span class="sxs-lookup"><span data-stu-id="52523-121">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Inicio del asistente para Crear Project":::

1. <span data-ttu-id="52523-123">En el **paso Seleccionar capacidades,** la **funcionalidad Tab** ya estará seleccionada.</span><span class="sxs-lookup"><span data-stu-id="52523-123">On the **Select capabilities** step, the **Tab** capability will already be selected.</span></span>  <span data-ttu-id="52523-124">Pulse **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="52523-124">Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Captura de pantalla que muestra cómo agregar funcionalidades a la nueva aplicación.":::

1. <span data-ttu-id="52523-126">En el **paso Tipo de hospedaje front-end,** seleccione SharePoint Framework **(SPFx).**</span><span class="sxs-lookup"><span data-stu-id="52523-126">On the **Frontend hosting type** step, select **SharePoint Framework (SPFx)**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Captura de pantalla que muestra cómo seleccionar el hospedaje de la nueva aplicación.":::

1. <span data-ttu-id="52523-128">En el **paso Marco,** seleccione **React**.</span><span class="sxs-lookup"><span data-stu-id="52523-128">On the **Framework** step, select **React**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-which-framework.png" alt-text="Seleccionar marco":::

1. <span data-ttu-id="52523-130">Cuando se le pida un **nombre de elemento web,** presione **Entrar** para aceptar el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="52523-130">When asked for a **Webpart Name**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="52523-131">Cuando se le pida la **descripción del elemento web,** presione **ENTRAR** para aceptar el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="52523-131">When asked for the **Webpart Description**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="52523-132">Cuando se le pida el **lenguaje de programación,** presione **ENTRAR** para aceptar el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="52523-132">When asked for the **Programming Language**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="52523-133">Seleccione una carpeta de área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="52523-133">Select a workspace folder.</span></span>  <span data-ttu-id="52523-134">Se creará una carpeta dentro de la carpeta del área de trabajo para el proyecto que está creando.</span><span class="sxs-lookup"><span data-stu-id="52523-134">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="52523-135">Escribe un nombre adecuado para la aplicación, como `helloworld` .</span><span class="sxs-lookup"><span data-stu-id="52523-135">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="52523-136">El nombre de la aplicación debe estar formado solo por caracteres alfanuméricos.</span><span class="sxs-lookup"><span data-stu-id="52523-136">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="52523-137">Presione **ENTRAR** para continuar.</span><span class="sxs-lookup"><span data-stu-id="52523-137">Press **Enter** to continue.</span></span>

<span data-ttu-id="52523-138">La Teams se creará en unos segundos.</span><span class="sxs-lookup"><span data-stu-id="52523-138">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="52523-139">Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="52523-139">Command line</span></span>](#tab/cli)

<span data-ttu-id="52523-140">Use la `teamsfx` CLI para crear el primer proyecto.</span><span class="sxs-lookup"><span data-stu-id="52523-140">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="52523-141">Comience desde la carpeta donde desea crear la carpeta del proyecto.</span><span class="sxs-lookup"><span data-stu-id="52523-141">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="52523-142">La CLI le guiará por algunas preguntas para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="52523-142">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="52523-143">Cada pregunta le dirá cómo responderla (por ejemplo, usar teclas de flecha para seleccionar una opción).</span><span class="sxs-lookup"><span data-stu-id="52523-143">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="52523-144">Cuando haya respondido a la pregunta, confirme su elección presionando **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="52523-144">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="52523-145">Selecciona **Crear una nueva Teams aplicación**.</span><span class="sxs-lookup"><span data-stu-id="52523-145">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="52523-146">Elija la **funcionalidad Tab.**</span><span class="sxs-lookup"><span data-stu-id="52523-146">Choose the **Tab** capability.</span></span>
1. <span data-ttu-id="52523-147">Seleccione **SharePoint Framework (SPFx) de** front-end.</span><span class="sxs-lookup"><span data-stu-id="52523-147">Select **SharePoint Framework (SPFx)** frontend hosting.</span></span>
1. <span data-ttu-id="52523-148">Seleccione **React** framework.</span><span class="sxs-lookup"><span data-stu-id="52523-148">Select **React** framework.</span></span>
1. <span data-ttu-id="52523-149">Presione **Entrar** para el **nombre del elemento web**.</span><span class="sxs-lookup"><span data-stu-id="52523-149">Press **Enter** for the **Webpart Name**.</span></span>
1. <span data-ttu-id="52523-150">Presione **ENTRAR** para la **descripción del elemento web**.</span><span class="sxs-lookup"><span data-stu-id="52523-150">Press **Enter** for the **Webpart Description**.</span></span>
1. <span data-ttu-id="52523-151">Presione **ENTRAR** para el **lenguaje de programación**.</span><span class="sxs-lookup"><span data-stu-id="52523-151">Press **Enter** for the **Programming Language**.</span></span>
1. <span data-ttu-id="52523-152">Presione **Entrar** para seleccionar la carpeta de área de trabajo predeterminada.</span><span class="sxs-lookup"><span data-stu-id="52523-152">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="52523-153">Escribe un nombre adecuado para la aplicación, como `helloworld` .</span><span class="sxs-lookup"><span data-stu-id="52523-153">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="52523-154">El nombre de la aplicación debe estar formado solo por caracteres alfanuméricos.</span><span class="sxs-lookup"><span data-stu-id="52523-154">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="52523-155">Una vez que se hayan contestado todas las preguntas, se creará el proyecto.</span><span class="sxs-lookup"><span data-stu-id="52523-155">Once all the questions have been answered, your project will be created.</span></span>

---

- [<span data-ttu-id="52523-156">Obtenga más información sobre el desarrollo para SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="52523-156">Learn more about developing for SharePoint Framework</span></span>](/sharepoint/dev/spfx/sharepoint-framework-overview)

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="52523-157">Realizar un recorrido por el código fuente</span><span class="sxs-lookup"><span data-stu-id="52523-157">Take a tour of the source code</span></span>

<span data-ttu-id="52523-158">Si quieres omitir esta sección por ahora, puedes [ejecutar la aplicación localmente.](#run-your-app-locally)</span><span class="sxs-lookup"><span data-stu-id="52523-158">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="52523-159">Una vez Teams Toolkit configurar el proyecto, tienes los componentes para crear una aplicación personal básica para Teams que se hospeda en el SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="52523-159">Once the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams that is hosted within the SharePoint Framework.</span></span>  <span data-ttu-id="52523-160">Los directorios y archivos del proyecto se muestran en el área Explorador de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="52523-160">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/app-project-files-spfx.png" alt-text="Captura de pantalla que muestra los archivos de proyecto de la aplicación para una aplicación personal en Visual Studio Code.":::

<span data-ttu-id="52523-162">El Toolkit crea automáticamente scaffolding en el directorio del proyecto en función de las capacidades que agregó durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="52523-162">The Toolkit automatically creates scaffolding for you in the project directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="52523-163">El Teams Toolkit mantiene su estado para la aplicación en el `.fx` directorio.</span><span class="sxs-lookup"><span data-stu-id="52523-163">The Teams Toolkit maintains its state for your app in the `.fx` directory.</span></span>  <span data-ttu-id="52523-164">Entre otros elementos de este directorio:</span><span class="sxs-lookup"><span data-stu-id="52523-164">Among other items in this directory:</span></span>

- <span data-ttu-id="52523-165">Los iconos de la aplicación se almacenan como archivos PNG `color.png` en y `outline.png` .</span><span class="sxs-lookup"><span data-stu-id="52523-165">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="52523-166">El manifiesto de la aplicación para publicar en el Portal de desarrolladores para Teams se almacena en `manifest.source.json` .</span><span class="sxs-lookup"><span data-stu-id="52523-166">The app manifest for publishing to Developer Portal for Teams is stored in `manifest.source.json`.</span></span>
- <span data-ttu-id="52523-167">La configuración que eligió al crear el proyecto se almacena en `settings.json` .</span><span class="sxs-lookup"><span data-stu-id="52523-167">The settings you chose when creating the project are stored in `settings.json`.</span></span>

<span data-ttu-id="52523-168">Dado que ha seleccionado un SPFx webpart, los siguientes archivos son relevantes para la interfaz de usuario:</span><span class="sxs-lookup"><span data-stu-id="52523-168">Since you selected an SPFx Webpart project, the following files are relevant to your UI:</span></span>

- <span data-ttu-id="52523-169">La carpeta `SPFx/src/webparts/{webpart}` contiene el SPFx webpart.</span><span class="sxs-lookup"><span data-stu-id="52523-169">The folder `SPFx/src/webparts/{webpart}` contains your SPFx webpart.</span></span>
- <span data-ttu-id="52523-170">El archivo `.vscode/launch.json` describe las configuraciones de depuración disponibles en la paleta de depuración.</span><span class="sxs-lookup"><span data-stu-id="52523-170">The file `.vscode/launch.json` describes the debugging configurations available in the debug palette.</span></span>

<span data-ttu-id="52523-171">Para obtener más información sobre SharePoint webparts para Teams, [consulte la SharePoint .](/sharepoint/dev/spfx/build-for-teams-overview)</span><span class="sxs-lookup"><span data-stu-id="52523-171">For more information about SharePoint Webparts for Teams, [refer to the SharePoint documentation](/sharepoint/dev/spfx/build-for-teams-overview).</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="52523-172">Ejecutar la aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="52523-172">Run your app locally</span></span>

<span data-ttu-id="52523-173">Teams Toolkit permite hospedar la aplicación localmente y ejecutarla a través de [SharePoint Framework Workbench](/sharepoint/dev/spfx/debug-in-vscode).</span><span class="sxs-lookup"><span data-stu-id="52523-173">Teams Toolkit allows you to host your app locally and run it through the [SharePoint Framework Workbench](/sharepoint/dev/spfx/debug-in-vscode).</span></span>

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a><span data-ttu-id="52523-174">Cree y ejecute la aplicación localmente en Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="52523-174">Build and run your app locally in Visual Studio Code</span></span>

<span data-ttu-id="52523-175">Para compilar y ejecutar la aplicación localmente:</span><span class="sxs-lookup"><span data-stu-id="52523-175">To build and run your app locally:</span></span>

1. <span data-ttu-id="52523-176">Desde Visual Studio Code, presione **F5**.</span><span class="sxs-lookup"><span data-stu-id="52523-176">From Visual Studio Code, press **F5**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-debug-local.png" alt-text="Captura de pantalla que muestra cómo iniciar una SPFx en un área de trabajo local.":::

   > [!NOTE]
   > <span data-ttu-id="52523-178">Cuando ejecutas la aplicación por primera vez, se descargan todas las dependencias y se compila la aplicación.</span><span class="sxs-lookup"><span data-stu-id="52523-178">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="52523-179">Una ventana del explorador se abre automáticamente y carga SharePoint Workbench cuando se completa la compilación.</span><span class="sxs-lookup"><span data-stu-id="52523-179">A browser window automatically opens and loads the SharePoint Workbench when the build is complete.</span></span>  <span data-ttu-id="52523-180">Esto puede tardar entre 3 y 5 minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="52523-180">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="52523-181">Una vez que se SharePoint Workbench.</span><span class="sxs-lookup"><span data-stu-id="52523-181">Once the SharePoint Workbench is loaded.</span></span>

   >[!NOTE]
   > <span data-ttu-id="52523-182">El Toolkit le pedirá que instale un certificado local si es necesario.</span><span class="sxs-lookup"><span data-stu-id="52523-182">The Toolkit will prompt you to install a local certificate if needed.</span></span> <span data-ttu-id="52523-183">Este certificado permite Teams cargar la aplicación desde `https://localhost` .</span><span class="sxs-lookup"><span data-stu-id="52523-183">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="52523-184">Seleccione Sí cuando aparezca el siguiente cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="52523-184">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Captura de pantalla que muestra cómo se indica cómo instalar un certificado SSL para Teams cargar la aplicación desde localhost.":::

1. <span data-ttu-id="52523-186">Presione uno de los **iconos Agregar elemento web** (+) para agregar el elemento web.</span><span class="sxs-lookup"><span data-stu-id="52523-186">Press one of the **Add Webpart** (+) icons to add your webpart.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart.png" alt-text="Captura de pantalla que muestra SPFx workbench que se ejecuta con el elemento emergente para agregar un elemento web que se muestra.":::

1. <span data-ttu-id="52523-188">Elija el elemento web en el menú.</span><span class="sxs-lookup"><span data-stu-id="52523-188">Choose your webpart from the menu.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart2.png" alt-text="Captura de pantalla que muestra SPFx workbench que se ejecuta con el elemento emergente para agregar una selección de elemento web.":::

<span data-ttu-id="52523-190">La aplicación debería estar ejecutándose.</span><span class="sxs-lookup"><span data-stu-id="52523-190">Your app should now be running.</span></span>  <span data-ttu-id="52523-191">Puede realizar actividades de depuración normales como si se tratase de otras SPFx webpart (como establecer puntos de interrupción).</span><span class="sxs-lookup"><span data-stu-id="52523-191">You can do normal debugging activities as if this were any other SPFx webpart (such as setting breakpoints).</span></span>

> [!TIP]
> <span data-ttu-id="52523-192">Intente colocar puntos de interrupción en el método de representación `SPFx/src/webparts/{webpart}/{webpart}.ts` y volver a cargar la ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="52523-192">Try placing breakpoints in the render method of `SPFx/src/webparts/{webpart}/{webpart}.ts` and reloading the browser window.</span></span> <span data-ttu-id="52523-193">VS Code se detendrá en puntos de interrupción en el código.</span><span class="sxs-lookup"><span data-stu-id="52523-193">VS Code will stop on breakpoints in your code.</span></span>

## <a name="deploy-your-app-to-sharepoint"></a><span data-ttu-id="52523-194">Implementar la aplicación en SharePoint</span><span class="sxs-lookup"><span data-stu-id="52523-194">Deploy your app to SharePoint</span></span>

<span data-ttu-id="52523-195">Asegúrate de que SharePoint catálogo de aplicaciones existe en la implementación.</span><span class="sxs-lookup"><span data-stu-id="52523-195">Ensure a SharePoint App Catalog exists in your deployment.</span></span>  <span data-ttu-id="52523-196">Si no existe, [cree uno](/sharepoint/use-app-catalog).</span><span class="sxs-lookup"><span data-stu-id="52523-196">If one does not exist, [create one](/sharepoint/use-app-catalog).</span></span>  <span data-ttu-id="52523-197">El catálogo de aplicaciones puede tardar hasta 15 minutos en crearse completamente.</span><span class="sxs-lookup"><span data-stu-id="52523-197">It may take up to 15 minutes for the app catalog to be fully created.</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="52523-198">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="52523-198">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="52523-199">Abra Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="52523-199">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="52523-200">Seleccione el Teams Toolkit de la barra lateral seleccionando el Teams.</span><span class="sxs-lookup"><span data-stu-id="52523-200">Select the Teams Toolkit from the sidebar by selecting the Teams icon.</span></span>
1. <span data-ttu-id="52523-201">Seleccione **Aprovisionar en la nube**.</span><span class="sxs-lookup"><span data-stu-id="52523-201">Select **Provision in the Cloud**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="Captura de pantalla que muestra los comandos de aprovisionamiento":::

1. <span data-ttu-id="52523-203">Puede supervisar el progreso viendo los cuadros de diálogo en la esquina inferior derecha.</span><span class="sxs-lookup"><span data-stu-id="52523-203">You can monitor the progress by watching the dialogs in the bottom right corner.</span></span>  <span data-ttu-id="52523-204">Después de unos segundos, verá el siguiente aviso:</span><span class="sxs-lookup"><span data-stu-id="52523-204">After a few seconds, you will see the following notice:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/provision-complete.png" alt-text="Captura de pantalla que muestra el cuadro de diálogo completado de aprovisionamiento.":::

1. <span data-ttu-id="52523-206">Una vez completado el aprovisionamiento, seleccione **Implementar en la nube.**</span><span class="sxs-lookup"><span data-stu-id="52523-206">Once provisioning is complete, select **Deploy to the cloud**.</span></span>

1. <span data-ttu-id="52523-207">Actualmente, la implementación automatizada no está disponible.</span><span class="sxs-lookup"><span data-stu-id="52523-207">Currently, automated deployment is not available.</span></span>  <span data-ttu-id="52523-208">Aparecerá un cuadro de diálogo que le pedirá que cree e implemente manualmente.</span><span class="sxs-lookup"><span data-stu-id="52523-208">A dialog will pop up prompting you to build and deploy manually.</span></span> <span data-ttu-id="52523-209">Presione **Compilar SharePoint paquete**.</span><span class="sxs-lookup"><span data-stu-id="52523-209">Press **Build SharePoint Package**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/build-sharepoint-package.png" alt-text="Captura de pantalla del cuadro de diálogo Compilar paquete de Sharepoint":::

# <a name="command-line"></a>[<span data-ttu-id="52523-211">Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="52523-211">Command line</span></span>](#tab/cli)

<span data-ttu-id="52523-212">En la ventana de terminal:</span><span class="sxs-lookup"><span data-stu-id="52523-212">In your terminal window:</span></span>

1. <span data-ttu-id="52523-213">Ejecute `teamsfx provision`.</span><span class="sxs-lookup"><span data-stu-id="52523-213">Run `teamsfx provision`.</span></span>

   ``` bash
   teamsfx provision
   ```

   <span data-ttu-id="52523-214">Es posible que se le pida que inicie sesión en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="52523-214">You may be prompted to log in to your Azure subscription.</span></span>  <span data-ttu-id="52523-215">Si es necesario, se le pedirá que seleccione una suscripción de Azure que se usará para los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="52523-215">If required, you will be prompted to select an Azure subscription to use for the Azure resources.</span></span>

   > [!NOTE]
   > <span data-ttu-id="52523-216">Siempre hay algunos recursos de Azure usados para hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="52523-216">There are always some Azure resources used for hosting your app.</span></span>

1. <span data-ttu-id="52523-217">Ejecute `teamsfx deploy`.</span><span class="sxs-lookup"><span data-stu-id="52523-217">Run `teamsfx deploy`.</span></span>

   ``` bash
   teamsfx deploy
   ```

1. <span data-ttu-id="52523-218">Cuando se le pida, **seleccione Compilar SharePoint paquete**.</span><span class="sxs-lookup"><span data-stu-id="52523-218">When prompted, select **Build SharePoint Package**.</span></span>

---

<span data-ttu-id="52523-219">El SharePoint se encuentra dentro `SPFx/sharepoint/solution` del proyecto.</span><span class="sxs-lookup"><span data-stu-id="52523-219">The SharePoint package is located in `SPFx/sharepoint/solution` within your project.</span></span>  <span data-ttu-id="52523-220">Upload el paquete a SharePoint:</span><span class="sxs-lookup"><span data-stu-id="52523-220">Upload the package to SharePoint:</span></span>

1. <span data-ttu-id="52523-221">Inicie sesión en la Consola de administración de M365 y, a continuación, vaya al catálogo SharePoint de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="52523-221">Log into the M365 Admin Console, then navigate to the SharePoint App Catalog.</span></span>

   - <span data-ttu-id="52523-222">Abra `https://admin.microsoft.com/AdminPortal/Home` .</span><span class="sxs-lookup"><span data-stu-id="52523-222">Open `https://admin.microsoft.com/AdminPortal/Home`.</span></span>
   - <span data-ttu-id="52523-223">En **Centros de administración,** seleccione el **SharePoint** de administración.</span><span class="sxs-lookup"><span data-stu-id="52523-223">Under **Admin centers**, select the **SharePoint** admin center.</span></span>
   - <span data-ttu-id="52523-224">Selecciona **Más características en** el menú de la barra lateral.</span><span class="sxs-lookup"><span data-stu-id="52523-224">Select **More features** from the sidebar menu.</span></span>
   - <span data-ttu-id="52523-225">Presione **Abrir en** **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="52523-225">Press **Open** under **Apps**.</span></span>
   - <span data-ttu-id="52523-226">Seleccione **Catálogo de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="52523-226">Select **App Catalog**.</span></span>

1. <span data-ttu-id="52523-227">Selecciona **Distribuir aplicaciones para SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="52523-227">Select **Distribute apps for SharePoint**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-distribute-apps.png" alt-text="Distribuir aplicaciones para SharePoint.":::

1. <span data-ttu-id="52523-229">Seleccione **Upload**.</span><span class="sxs-lookup"><span data-stu-id="52523-229">Select **Upload**.</span></span>

1. <span data-ttu-id="52523-230">Presione **Elegir archivo**.</span><span class="sxs-lookup"><span data-stu-id="52523-230">Press **Choose File**.</span></span>

1. <span data-ttu-id="52523-231">Busque el `{project}.sppkg` archivo, ubicado en la `SPFx/sharepoint/solution` carpeta dentro del proyecto.</span><span class="sxs-lookup"><span data-stu-id="52523-231">Locate your `{project}.sppkg` file, located in the `SPFx/sharepoint/solution` folder within your project.</span></span>  <span data-ttu-id="52523-232">Presione **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="52523-232">Press **Open**.</span></span>

1. <span data-ttu-id="52523-233">Pulse **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="52523-233">Press **OK**.</span></span>

1. <span data-ttu-id="52523-234">El SharePoint de implementación se iniciará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="52523-234">The SharePoint deployment process will automatically start.</span></span>  <span data-ttu-id="52523-235">Asegúrese **de que esta solución esté disponible para todos** los sitios de la organización y, a continuación, presione **Implementar**.</span><span class="sxs-lookup"><span data-stu-id="52523-235">Ensure **Make this solution available to all sites in the organization** is checked, then press **Deploy**.</span></span>

1. <span data-ttu-id="52523-236">Seleccione la **pestaña** ARCHIVOS.</span><span class="sxs-lookup"><span data-stu-id="52523-236">Select the **FILES** tab.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-appcatalog-filestab.png" alt-text="Seleccione la pestaña archivos en el catálogo SharePoint de aplicaciones.":::

1. <span data-ttu-id="52523-238">seleccione el paquete que implementó y, a continuación, presione **Sincronizar para Teams** en la cinta de opciones.</span><span class="sxs-lookup"><span data-stu-id="52523-238">select the package you deployed, then press **Sync to Teams** in the ribbon.</span></span>

    > [!Note]
    > <span data-ttu-id="52523-239">El proceso de sincronización Teams puede tardar un par de minutos.</span><span class="sxs-lookup"><span data-stu-id="52523-239">The Sync to Teams process can take a couple of minutes.</span></span>  <span data-ttu-id="52523-240">Verás un mensaje en el lado derecho del explorador que indica que la aplicación se ha sincronizado correctamente con Teams.</span><span class="sxs-lookup"><span data-stu-id="52523-240">You will see a message on the right-hand side of the browser indicating that the app has successfully synchronized to Teams.</span></span>

<span data-ttu-id="52523-241">Abra la Teams (o inicie sesión en `https://teams.microsoft.com` ).</span><span class="sxs-lookup"><span data-stu-id="52523-241">Open the Teams application (or sign in at `https://teams.microsoft.com`).</span></span>  <span data-ttu-id="52523-242">Presione el triple punto en la barra lateral y, a continuación, **seleccione Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="52523-242">Press the triple-dot on the sidebar, then select **All apps**.</span></span>  <span data-ttu-id="52523-243">La aplicación se colocará en las **aplicaciones creadas para tu categoría de** organización.</span><span class="sxs-lookup"><span data-stu-id="52523-243">The app will be placed in the **Apps built for your org** category.</span></span>  <span data-ttu-id="52523-244">Puedes agregar la aplicación desde allí.</span><span class="sxs-lookup"><span data-stu-id="52523-244">You can add the app from there.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/spfx-app-in-teams.png" alt-text="Captura de pantalla que muestra la aplicación en Teams":::

## <a name="next-steps"></a><span data-ttu-id="52523-246">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="52523-246">Next steps</span></span>

<span data-ttu-id="52523-247">Obtenga información sobre otros métodos para crear Teams aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="52523-247">Learn about other methods for creating Teams apps:</span></span>

- [<span data-ttu-id="52523-248">Crear una aplicación Teams con React</span><span class="sxs-lookup"><span data-stu-id="52523-248">Create a Teams app with React</span></span>](first-app-react.md)
- [<span data-ttu-id="52523-249">Crear una Teams con Blazor</span><span class="sxs-lookup"><span data-stu-id="52523-249">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
- [<span data-ttu-id="52523-250">Crear una aplicación de bot conversacional</span><span class="sxs-lookup"><span data-stu-id="52523-250">Create a conversational bot app</span></span>](first-app-bot.md)
- [<span data-ttu-id="52523-251">Crear una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="52523-251">Create a messaging extension</span></span>](first-message-extension.md)

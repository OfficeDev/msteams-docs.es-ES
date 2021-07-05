---
title: 'Introducción: crea la primera aplicación Teams con SPFx'
author: zhenyasav
description: Obtenga información sobre cómo crear una pestaña personalizada con el SharePoint Framework
ms.author: zhenyasa
ms.date: 05/19/2021
ms.topic: quickstart
ms.openlocfilehash: 4df2bb71837af520a2d2500a45b8605e5fae08b2
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254226"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-sharepoint-framework-spfx"></a><span data-ttu-id="9e239-103">Compila y ejecuta la primera aplicación Microsoft Teams con SharePoint Framework (SPFx)</span><span class="sxs-lookup"><span data-stu-id="9e239-103">Build and run your first Microsoft Teams app with SharePoint Framework (SPFx)</span></span>

<span data-ttu-id="9e239-104">En este tutorial, aprenderás a crear una nueva aplicación Microsoft Teams en SharePoint Framework SPFx que implemente una aplicación personal sencilla.</span><span class="sxs-lookup"><span data-stu-id="9e239-104">In this tutorial, you will learn how to create a new Microsoft Teams app in SharePoint Framework SPFx that implements a simple personal app.</span></span> <span data-ttu-id="9e239-105">Por ejemplo, una *aplicación personal incluye* un conjunto de pestañas para uso individual.</span><span class="sxs-lookup"><span data-stu-id="9e239-105">For example, a *personal app* includes a set of tabs for individual use.</span></span> <span data-ttu-id="9e239-106">Durante el tutorial, aprenderás sobre la estructura de una aplicación de Teams, cómo ejecutar una aplicación localmente y cómo implementar la aplicación en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9e239-106">During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to SharePoint.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9e239-107">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="9e239-107">Before you begin</span></span>

<span data-ttu-id="9e239-108">Asegúrese de que el entorno de desarrollo está configurado instalando los requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="9e239-108">Make sure your development environment is set up by installing the prerequisites.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9e239-109">Requisitos previos para la instalación</span><span class="sxs-lookup"><span data-stu-id="9e239-109">Install prerequisites</span></span>](prerequisites.md)

## <a name="get-organized"></a><span data-ttu-id="9e239-110">Organizarse</span><span class="sxs-lookup"><span data-stu-id="9e239-110">Get organized</span></span>

<span data-ttu-id="9e239-111">Además de los requisitos previos, también debe ser administrador de una colección SharePoint de sitios.</span><span class="sxs-lookup"><span data-stu-id="9e239-111">In addition to the prerequisites, you also need to be an Administrator for a SharePoint Site Collection.</span></span>  <span data-ttu-id="9e239-112">Aquí es donde implementará la aplicación para el hospedaje.</span><span class="sxs-lookup"><span data-stu-id="9e239-112">This is where you will deploy your app for hosting.</span></span>  <span data-ttu-id="9e239-113">Si usa un inquilino del programa para desarrolladores M365, use la cuenta de administrador que haya configurado al registrarse en el programa.</span><span class="sxs-lookup"><span data-stu-id="9e239-113">If you are using an M365 developer program tenant, use the administrator account you set up when you registered for the program.</span></span>  

## <a name="create-your-project"></a><span data-ttu-id="9e239-114">Crear un proyecto</span><span class="sxs-lookup"><span data-stu-id="9e239-114">Create your project</span></span>

<span data-ttu-id="9e239-115">Use el Kit de herramientas de Teams para crear su primer proyecto:</span><span class="sxs-lookup"><span data-stu-id="9e239-115">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="9e239-116">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9e239-116">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="9e239-117">Abra Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="9e239-117">Open Visual Studio code.</span></span>
1. <span data-ttu-id="9e239-118">Seleccione el Teams en la barra lateral para abrir el Teams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="9e239-118">Select the Teams icon in the sidebar to open the Teams Toolkit.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icono de Teams en la barra lateral de Visual Studio Code.":::

1. <span data-ttu-id="9e239-120">Seleccione **Crear nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="9e239-120">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Ubicación del vínculo Crear nuevo proyecto en la barra lateral del Kit de herramientas de Teams.":::

1. <span data-ttu-id="9e239-122">Seleccione **Crear una nueva aplicación de Teams**.</span><span class="sxs-lookup"><span data-stu-id="9e239-122">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Inicio del Asistente para crear un nuevo proyecto":::

1. <span data-ttu-id="9e239-124">En la **sección Seleccionar capacidades,** seleccione **Ficha** y seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9e239-124">In the **Select capabilities** section, select **Tab** and select **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Captura de pantalla que muestra cómo agregar funcionalidades a la nueva aplicación.":::

1. <span data-ttu-id="9e239-126">En la **sección Tipo de hospedaje front-end,** seleccione SharePoint Framework **(SPFx).**</span><span class="sxs-lookup"><span data-stu-id="9e239-126">In the **Frontend hosting type** section, select **SharePoint Framework (SPFx)**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Captura de pantalla que muestra cómo seleccionar el hospedaje para la nueva aplicación.":::

1. <span data-ttu-id="9e239-128">En la **sección Marco,** **seleccione React**.</span><span class="sxs-lookup"><span data-stu-id="9e239-128">In the **Framework** section, select **React**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-which-framework.png" alt-text="Seleccionar marco":::

1. <span data-ttu-id="9e239-130">Cuando se le pida un **nombre de elemento web,** presione **Entrar** para aceptar el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="9e239-130">When asked for a **Webpart Name**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="9e239-131">Cuando se le pida la **descripción del elemento web,** presione **ENTRAR** para aceptar el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="9e239-131">When asked for the **Webpart Description**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="9e239-132">Cuando se le pida el **lenguaje de programación,** presione **ENTRAR** para aceptar el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="9e239-132">When asked for the **Programming Language**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="9e239-133">Seleccione una carpeta de área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="9e239-133">Select a workspace folder.</span></span>  <span data-ttu-id="9e239-134">Se creará una carpeta dentro de la carpeta del área de trabajo para el proyecto que esté creando.</span><span class="sxs-lookup"><span data-stu-id="9e239-134">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="9e239-135">Escriba un nombre adecuado para la aplicación, como `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="9e239-135">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="9e239-136">El nombre de la aplicación solo puede contener caracteres alfanuméricos.</span><span class="sxs-lookup"><span data-stu-id="9e239-136">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="9e239-137">Presione **Entrar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="9e239-137">Press **Enter** to continue.</span></span>

   <span data-ttu-id="9e239-138">La aplicación Teams se creará en unos segundos.</span><span class="sxs-lookup"><span data-stu-id="9e239-138">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="9e239-139">Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="9e239-139">Command line</span></span>](#tab/cli)

<span data-ttu-id="9e239-140">Use la CLI de `teamsfx` para crear su primer proyecto:</span><span class="sxs-lookup"><span data-stu-id="9e239-140">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="9e239-141">Comience en la carpeta en la que quiera crear la carpeta del proyecto.</span><span class="sxs-lookup"><span data-stu-id="9e239-141">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="9e239-142">La CLI le guiará por varias preguntas para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="9e239-142">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="9e239-143">En cada pregunta se le indicará cómo responder (por ejemplo, usando las teclas de dirección para seleccionar una opción).</span><span class="sxs-lookup"><span data-stu-id="9e239-143">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="9e239-144">Cuando haya respondido a la pregunta, presione **Entrar** para confirmar la elección.</span><span class="sxs-lookup"><span data-stu-id="9e239-144">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="9e239-145">Seleccione **Crear una nueva aplicación de Teams**.</span><span class="sxs-lookup"><span data-stu-id="9e239-145">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="9e239-146">Seleccione **Tab**.</span><span class="sxs-lookup"><span data-stu-id="9e239-146">Select **Tab**.</span></span>
1. <span data-ttu-id="9e239-147">Seleccione **SharePoint Framework (SPFx) de** front-end.</span><span class="sxs-lookup"><span data-stu-id="9e239-147">Select **SharePoint Framework (SPFx)** frontend hosting.</span></span>
1. <span data-ttu-id="9e239-148">Seleccione **React** framework.</span><span class="sxs-lookup"><span data-stu-id="9e239-148">Select **React** framework.</span></span>
1. <span data-ttu-id="9e239-149">Presione **Entrar** para el **nombre del elemento web**.</span><span class="sxs-lookup"><span data-stu-id="9e239-149">Press **Enter** for the **Webpart Name**.</span></span>
1. <span data-ttu-id="9e239-150">Presione **ENTRAR** para la **descripción del elemento web**.</span><span class="sxs-lookup"><span data-stu-id="9e239-150">Press **Enter** for the **Webpart Description**.</span></span>
1. <span data-ttu-id="9e239-151">Presione **ENTRAR** para el **lenguaje de programación**.</span><span class="sxs-lookup"><span data-stu-id="9e239-151">Press **Enter** for the **Programming Language**.</span></span>
1. <span data-ttu-id="9e239-152">Presione **Entrar** para seleccionar la carpeta de área de trabajo predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9e239-152">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="9e239-153">Escriba un nombre adecuado para la aplicación, como `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="9e239-153">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="9e239-154">El nombre de la aplicación solo puede contener caracteres alfanuméricos.</span><span class="sxs-lookup"><span data-stu-id="9e239-154">The name of the app must consist only of alphanumeric characters.</span></span>

   <span data-ttu-id="9e239-155">Una vez contestadas todas las preguntas, se creará el proyecto.</span><span class="sxs-lookup"><span data-stu-id="9e239-155">After all the questions have been answered, your project will be created.</span></span>

---

- [<span data-ttu-id="9e239-156">Obtenga más información sobre el desarrollo para SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="9e239-156">Learn more about developing for SharePoint Framework</span></span>](/sharepoint/dev/spfx/sharepoint-framework-overview)

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="9e239-157">Dar un paseo por el código fuente</span><span class="sxs-lookup"><span data-stu-id="9e239-157">Take a tour of the source code</span></span>

<span data-ttu-id="9e239-158">Si quiere omitir esta sección por ahora, puede [ejecutar la aplicación de forma local](#run-your-app-locally).</span><span class="sxs-lookup"><span data-stu-id="9e239-158">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="9e239-159">Después de Teams Toolkit configurar el proyecto, tienes los componentes para crear una aplicación personal básica para Teams que se hospeda en el SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="9e239-159">After the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams that is hosted within the SharePoint Framework.</span></span>  <span data-ttu-id="9e239-160">Los archivos y directorios del proyecto se muestran en el área del Explorador de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="9e239-160">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/app-project-files-spfx.png" alt-text="Captura de pantalla que muestra los archivos de proyecto de la aplicación para una aplicación personal en Visual Studio Code.":::

<span data-ttu-id="9e239-162">El kit de herramientas crea automáticamente el scaffolding en el directorio del proyecto en función de las funcionalidades que ha agregado durante la configuración.</span><span class="sxs-lookup"><span data-stu-id="9e239-162">The Toolkit automatically creates scaffolding for you in the project directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="9e239-163">El Kit de herramientas de Teams mantiene el estado para la aplicación en el directorio `.fx`.</span><span class="sxs-lookup"><span data-stu-id="9e239-163">The Teams Toolkit maintains its state for your app in the `.fx` directory.</span></span>  <span data-ttu-id="9e239-164">Entre otros elementos de este directorio:</span><span class="sxs-lookup"><span data-stu-id="9e239-164">Among other items in this directory:</span></span>

- <span data-ttu-id="9e239-165">Los iconos de aplicación se almacenan como archivos PNG en `color.png` y `outline.png`.</span><span class="sxs-lookup"><span data-stu-id="9e239-165">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="9e239-166">El manifiesto de la aplicación para publicar en el Portal de desarrolladores para Teams se almacena en `manifest.source.json` .</span><span class="sxs-lookup"><span data-stu-id="9e239-166">The app manifest for publishing to Developer Portal for Teams is stored in `manifest.source.json`.</span></span>
- <span data-ttu-id="9e239-167">La configuración que eligió al crear el proyecto se almacena en `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="9e239-167">The settings you chose when creating the project are stored in `settings.json`.</span></span>

<span data-ttu-id="9e239-168">Dado que ha seleccionado un SPFx webpart, los siguientes archivos son relevantes para la interfaz de usuario:</span><span class="sxs-lookup"><span data-stu-id="9e239-168">Since you selected a SPFx Webpart project, the following files are relevant to your UI:</span></span>

- <span data-ttu-id="9e239-169">La carpeta `SPFx/src/webparts/{webpart}` contiene el SPFx webpart.</span><span class="sxs-lookup"><span data-stu-id="9e239-169">The folder `SPFx/src/webparts/{webpart}` contains your SPFx webpart.</span></span>
- <span data-ttu-id="9e239-170">El archivo `.vscode/launch.json` describe las configuraciones de depuración disponibles en la paleta de depuración.</span><span class="sxs-lookup"><span data-stu-id="9e239-170">The file `.vscode/launch.json` describes the debugging configurations available in the debug palette.</span></span>

<span data-ttu-id="9e239-171">Para obtener más información sobre SharePoint webparts para Teams, [consulte la SharePoint .](/sharepoint/dev/spfx/build-for-teams-overview)</span><span class="sxs-lookup"><span data-stu-id="9e239-171">For more information about SharePoint Webparts for Teams, [refer to the SharePoint documentation](/sharepoint/dev/spfx/build-for-teams-overview).</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="9e239-172">Ejecutar la aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="9e239-172">Run your app locally</span></span>

<span data-ttu-id="9e239-173">Teams Toolkit permite hospedar la aplicación localmente y ejecutarla a través de [SharePoint Framework Workbench](/sharepoint/dev/spfx/debug-in-vscode).</span><span class="sxs-lookup"><span data-stu-id="9e239-173">Teams Toolkit allows you to host your app locally and run it through the [SharePoint Framework Workbench](/sharepoint/dev/spfx/debug-in-vscode).</span></span>

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a><span data-ttu-id="9e239-174">Compilar y ejecutar la aplicación de forma local en Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9e239-174">Build and run your app locally in Visual Studio Code</span></span>

<span data-ttu-id="9e239-175">Para crear y ejecutar la aplicación localmente:</span><span class="sxs-lookup"><span data-stu-id="9e239-175">To build and run your app locally:</span></span>

1. <span data-ttu-id="9e239-176">Desde Visual Studio Code, presione la **tecla F5.**</span><span class="sxs-lookup"><span data-stu-id="9e239-176">From Visual Studio Code, press the **F5** key.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-debug-local.png" alt-text="Captura de pantalla que muestra cómo iniciar una SPFx en un área de trabajo local.":::

   > [!NOTE]
   > <span data-ttu-id="9e239-178">Al ejecutar la aplicación por primera vez, se descargan todas las dependencias y se compila la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9e239-178">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="9e239-179">Una ventana del explorador se abre automáticamente y carga SharePoint Workbench cuando se completa la compilación.</span><span class="sxs-lookup"><span data-stu-id="9e239-179">A browser window automatically opens and loads the SharePoint Workbench when the build is complete.</span></span>  <span data-ttu-id="9e239-180">Este proceso puede tardar entre 3 o 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="9e239-180">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="9e239-181">Después de cargar SharePoint Workbench.</span><span class="sxs-lookup"><span data-stu-id="9e239-181">After the SharePoint Workbench is loaded.</span></span>

   >[!NOTE]
   > <span data-ttu-id="9e239-182">El Kit de herramientas le pedirá que instale un certificado local si es necesario.</span><span class="sxs-lookup"><span data-stu-id="9e239-182">The Toolkit will prompt you to install a local certificate if needed.</span></span> <span data-ttu-id="9e239-183">Este certificado permite a Teams cargar la aplicación desde `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="9e239-183">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="9e239-184">Seleccione Sí cuando aparezca el siguiente cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="9e239-184">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Captura de pantalla en la que se muestra la solicitud para instalar un certificado SSL para permitir que Teams cargue la aplicación desde localhost.":::

1. <span data-ttu-id="9e239-186">Seleccione **Agregar elemento web + iconos** para agregar el elemento web.</span><span class="sxs-lookup"><span data-stu-id="9e239-186">Select **Add Webpart +** icons to add your webpart.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart.png" alt-text="Captura de pantalla que muestra SPFx workbench que se ejecuta con el elemento emergente para agregar un elemento web que se muestra.":::

1. <span data-ttu-id="9e239-188">Seleccione el elemento web en el menú.</span><span class="sxs-lookup"><span data-stu-id="9e239-188">Select your webpart from the menu.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart2.png" alt-text="Captura de pantalla que muestra SPFx workbench que se ejecuta con el elemento emergente para agregar una selección de elemento web.":::

   <span data-ttu-id="9e239-190">La aplicación debería estar ejecutándose.</span><span class="sxs-lookup"><span data-stu-id="9e239-190">Your app should now be running.</span></span>  <span data-ttu-id="9e239-191">Puede realizar actividades de depuración normales como si se tratase de otras SPFx webpart (como establecer puntos de interrupción).</span><span class="sxs-lookup"><span data-stu-id="9e239-191">You can do normal debugging activities as if this were any other SPFx webpart (such as setting breakpoints).</span></span>

   > [!TIP]
   > <span data-ttu-id="9e239-192">Intente colocar puntos de interrupción en el método de representación `SPFx/src/webparts/{webpart}/{webpart}.ts` y volver a cargar la ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="9e239-192">Try placing breakpoints in the render method of `SPFx/src/webparts/{webpart}/{webpart}.ts` and reloading the browser window.</span></span> <span data-ttu-id="9e239-193">VS Code se detendrá en puntos de interrupción en el código.</span><span class="sxs-lookup"><span data-stu-id="9e239-193">VS Code will stop on breakpoints in your code.</span></span>

## <a name="deploy-your-app-to-sharepoint"></a><span data-ttu-id="9e239-194">Implementar la aplicación en SharePoint</span><span class="sxs-lookup"><span data-stu-id="9e239-194">Deploy your app to SharePoint</span></span>

<span data-ttu-id="9e239-195">Asegúrate de que SharePoint catálogo de aplicaciones existe en la implementación.</span><span class="sxs-lookup"><span data-stu-id="9e239-195">Ensure a SharePoint App Catalog exists in your deployment.</span></span>  <span data-ttu-id="9e239-196">Si no existe, [cree uno](/sharepoint/use-app-catalog).</span><span class="sxs-lookup"><span data-stu-id="9e239-196">If one does not exist, [create one](/sharepoint/use-app-catalog).</span></span>  <span data-ttu-id="9e239-197">El catálogo de aplicaciones puede tardar hasta 15 minutos en crearse completamente.</span><span class="sxs-lookup"><span data-stu-id="9e239-197">It may take up to 15 minutes for the app catalog to be fully created.</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="9e239-198">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9e239-198">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="9e239-199">Abrir Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="9e239-199">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="9e239-200">Seleccione el Teams Toolkit de la barra lateral seleccionando el Teams.</span><span class="sxs-lookup"><span data-stu-id="9e239-200">Select the Teams Toolkit from the sidebar by selecting the Teams icon.</span></span>
1. <span data-ttu-id="9e239-201">Seleccione **Aprovisionar en la nube**.</span><span class="sxs-lookup"><span data-stu-id="9e239-201">Select **Provision in the Cloud**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="Captura de pantalla que muestra los comandos de aprovisionamiento":::

   <span data-ttu-id="9e239-203">Puede supervisar el progreso viendo los cuadros de diálogo en la esquina inferior derecha.</span><span class="sxs-lookup"><span data-stu-id="9e239-203">You can monitor the progress by watching the dialogs in the bottom right corner.</span></span>  <span data-ttu-id="9e239-204">Después de unos segundos, verá el siguiente aviso:</span><span class="sxs-lookup"><span data-stu-id="9e239-204">After a few seconds, you will see the following notice:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/provision-complete.png" alt-text="Captura de pantalla que muestra el cuadro de diálogo completado de aprovisionamiento.":::

1. <span data-ttu-id="9e239-206">Una vez completado el aprovisionamiento, seleccione **Implementar en la nube.**</span><span class="sxs-lookup"><span data-stu-id="9e239-206">After provisioning is complete, select **Deploy to the cloud**.</span></span>

1. <span data-ttu-id="9e239-207">Actualmente, la implementación automatizada no está disponible.</span><span class="sxs-lookup"><span data-stu-id="9e239-207">Currently, automated deployment is not available.</span></span>  <span data-ttu-id="9e239-208">Aparecerá un cuadro de diálogo que le pedirá que cree e implemente manualmente.</span><span class="sxs-lookup"><span data-stu-id="9e239-208">A dialog will pop up prompting you to build and deploy manually.</span></span> <span data-ttu-id="9e239-209">Seleccione **Compilar SharePoint paquete**.</span><span class="sxs-lookup"><span data-stu-id="9e239-209">Select **Build SharePoint Package**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/build-sharepoint-package.png" alt-text="Captura de pantalla del cuadro de diálogo Compilar paquete de Sharepoint":::

# <a name="command-line"></a>[<span data-ttu-id="9e239-211">Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="9e239-211">Command line</span></span>](#tab/cli)

<span data-ttu-id="9e239-212">En la ventana de terminal:</span><span class="sxs-lookup"><span data-stu-id="9e239-212">In your terminal window:</span></span>

1. <span data-ttu-id="9e239-213">Ejecute `teamsfx provision`.</span><span class="sxs-lookup"><span data-stu-id="9e239-213">Run `teamsfx provision`.</span></span>

   ``` bash
   teamsfx provision
   ```

   <span data-ttu-id="9e239-214">Es posible que se le pida que inicie sesión en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e239-214">You may be prompted to log in to your Azure subscription.</span></span>  <span data-ttu-id="9e239-215">Si es necesario, se le pedirá que seleccione una suscripción de Azure que se usará para los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e239-215">If required, you will be prompted to select an Azure subscription to use for the Azure resources.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9e239-216">Siempre hay algunos recursos de Azure usados para hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9e239-216">There are always some Azure resources used for hosting your app.</span></span>

1. <span data-ttu-id="9e239-217">Ejecute `teamsfx deploy`.</span><span class="sxs-lookup"><span data-stu-id="9e239-217">Run `teamsfx deploy`.</span></span>

   ``` bash
   teamsfx deploy
   ```

1. <span data-ttu-id="9e239-218">Cuando se le pida, **seleccione Compilar SharePoint paquete**.</span><span class="sxs-lookup"><span data-stu-id="9e239-218">When prompted, select **Build SharePoint Package**.</span></span>

---

<span data-ttu-id="9e239-219">El SharePoint se encuentra dentro `SPFx/sharepoint/solution` del proyecto.</span><span class="sxs-lookup"><span data-stu-id="9e239-219">The SharePoint package is located in `SPFx/sharepoint/solution` within your project.</span></span>  <span data-ttu-id="9e239-220">Upload el paquete a SharePoint:</span><span class="sxs-lookup"><span data-stu-id="9e239-220">Upload the package to SharePoint:</span></span>

1. <span data-ttu-id="9e239-221">Inicie sesión en la Consola de administración de M365 y, a continuación, vaya al catálogo SharePoint de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9e239-221">Log into the M365 Admin Console, then navigate to the SharePoint App Catalog.</span></span>

   1. <span data-ttu-id="9e239-222">Abra `https://admin.microsoft.com/AdminPortal/Home` .</span><span class="sxs-lookup"><span data-stu-id="9e239-222">Open `https://admin.microsoft.com/AdminPortal/Home`.</span></span>
   1. <span data-ttu-id="9e239-223">En **Centros de administración,** seleccione el **SharePoint** de administración.</span><span class="sxs-lookup"><span data-stu-id="9e239-223">Under **Admin centers**, select the **SharePoint** admin center.</span></span>
   1. <span data-ttu-id="9e239-224">Selecciona **Más características en** el menú de la barra lateral.</span><span class="sxs-lookup"><span data-stu-id="9e239-224">Select **More features** from the sidebar menu.</span></span>
   1. <span data-ttu-id="9e239-225">Presione **Abrir en** **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9e239-225">Press **Open** under **Apps**.</span></span>
   1. <span data-ttu-id="9e239-226">Seleccione **Catálogo de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9e239-226">Select **App Catalog**.</span></span>

1. <span data-ttu-id="9e239-227">Selecciona **Distribuir aplicaciones para SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="9e239-227">Select **Distribute apps for SharePoint**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-distribute-apps.png" alt-text="Distribuir aplicaciones para SharePoint.":::

1. <span data-ttu-id="9e239-229">Seleccione **Upload**.</span><span class="sxs-lookup"><span data-stu-id="9e239-229">Select **Upload**.</span></span>

1. <span data-ttu-id="9e239-230">Seleccione **Elegir archivo**.</span><span class="sxs-lookup"><span data-stu-id="9e239-230">Select **Choose File**.</span></span>

1. <span data-ttu-id="9e239-231">Busque el `{project}.sppkg` archivo en la carpeta dentro del `SPFx/sharepoint/solution` proyecto.</span><span class="sxs-lookup"><span data-stu-id="9e239-231">Locate your `{project}.sppkg` file in the `SPFx/sharepoint/solution` folder within your project.</span></span> <span data-ttu-id="9e239-232">Seleccione **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="9e239-232">Select **Open**.</span></span>

1. <span data-ttu-id="9e239-233">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9e239-233">Select **OK**.</span></span>

1. <span data-ttu-id="9e239-234">El SharePoint de implementación se iniciará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="9e239-234">The SharePoint deployment process will automatically start.</span></span> <span data-ttu-id="9e239-235">Compruebe que **esta solución esté disponible para todos los sitios de la** organización.</span><span class="sxs-lookup"><span data-stu-id="9e239-235">Verify that **Make this solution available to all sites in the organization** is selected.</span></span> <span data-ttu-id="9e239-236">A continuación, **seleccione Implementar**.</span><span class="sxs-lookup"><span data-stu-id="9e239-236">Then select **Deploy**.</span></span>

1. <span data-ttu-id="9e239-237">Seleccione la **pestaña** ARCHIVOS.</span><span class="sxs-lookup"><span data-stu-id="9e239-237">Select the **FILES** tab.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-appcatalog-filestab.png" alt-text="Seleccione la pestaña archivos en el catálogo SharePoint de aplicaciones.":::

1. <span data-ttu-id="9e239-239">seleccione el paquete que implementó y, a **continuación, seleccione Sincronizar para Teams** desde la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="9e239-239">select the package you deployed, then select **Sync to Teams** from the upper right corner.</span></span>

    > [!Note]
    > <span data-ttu-id="9e239-240">El proceso de sincronización Teams puede tardar un par de minutos.</span><span class="sxs-lookup"><span data-stu-id="9e239-240">The Sync to Teams process can take a couple of minutes.</span></span>  <span data-ttu-id="9e239-241">Verás un mensaje en el lado derecho del explorador que indica que la aplicación se ha sincronizado correctamente con Teams.</span><span class="sxs-lookup"><span data-stu-id="9e239-241">You will see a message on the right-hand side of the browser indicating that the app has successfully synchronized to Teams.</span></span>

   <span data-ttu-id="9e239-242">Abra la Teams (o inicie sesión en `https://teams.microsoft.com` ).</span><span class="sxs-lookup"><span data-stu-id="9e239-242">Open the Teams application (or sign in at `https://teams.microsoft.com`).</span></span>  <span data-ttu-id="9e239-243">Presione el triple punto en la barra lateral y, a continuación, **seleccione Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9e239-243">Press the triple-dot on the sidebar, then select **All apps**.</span></span>  <span data-ttu-id="9e239-244">La aplicación se colocará en las **aplicaciones creadas para tu categoría de** organización.</span><span class="sxs-lookup"><span data-stu-id="9e239-244">The app will be placed in the **Apps built for your org** category.</span></span>  <span data-ttu-id="9e239-245">Puedes agregar la aplicación desde allí.</span><span class="sxs-lookup"><span data-stu-id="9e239-245">You can add the app from there.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-app-in-teams.png" alt-text="Captura de pantalla que muestra la aplicación en Teams":::

## <a name="see-also"></a><span data-ttu-id="9e239-247">Vea también</span><span class="sxs-lookup"><span data-stu-id="9e239-247">See also</span></span>

* [<span data-ttu-id="9e239-248">Introducción a tutoriales</span><span class="sxs-lookup"><span data-stu-id="9e239-248">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="9e239-249">Crear una aplicación de bots de conversación</span><span class="sxs-lookup"><span data-stu-id="9e239-249">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="9e239-250">Crear una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="9e239-250">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="9e239-251">Muestras de código</span><span class="sxs-lookup"><span data-stu-id="9e239-251">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)

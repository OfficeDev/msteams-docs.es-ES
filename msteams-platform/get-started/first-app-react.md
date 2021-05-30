---
title: 'Introducción: creación de su primera aplicación de Teams con React'
author: adrianhall
description: Cree rápidamente una aplicación de Microsoft Teams en la que se muestre un mensaje de "Hola a todos" con el kit de herramientas de Microsoft Teams y React.
ms.author: adhal
ms.date: 05/18/2021
ms.topic: quickstart
ms.openlocfilehash: 4560e332834fec7b681a6b2babf3e881b5e472f7
ms.sourcegitcommit: 2c8b35899dd845acd66f1f927e40d99523c29a91
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/28/2021
ms.locfileid: "52698153"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-react"></a><span data-ttu-id="673ca-104">Compilar y ejecutar su primera aplicación de Microsoft Teams con React</span><span class="sxs-lookup"><span data-stu-id="673ca-104">Build and run your first Microsoft Teams app with React</span></span>

<span data-ttu-id="673ca-105">En este tutorial, creará una nueva aplicación de Microsoft Teams en React que implementa una aplicación personal simple para obtener información de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="673ca-105">In this tutorial, you will create a new Microsoft Teams app in React that implements a simple personal app to pull information from the Microsoft Graph.</span></span> <span data-ttu-id="673ca-106">(Una *aplicación personal* incluye un conjunto de pestañas con ámbito para uso individual). Durante el tutorial, aprenderá sobre la estructura de una aplicación de Teams, cómo ejecutar una aplicación localmente y cómo implementar la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="673ca-106">(A *personal app* includes a set of tabs scoped for individual use.) During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to Azure.</span></span>

<span data-ttu-id="673ca-107">La aplicación que se crea muestra información básica del usuario para el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="673ca-107">The app that is built displays basic user information for the current user.</span></span>  <span data-ttu-id="673ca-108">Cuando se conceda permiso, la aplicación se conectará a Microsoft Graph como el usuario actual para obtener el perfil completo.</span><span class="sxs-lookup"><span data-stu-id="673ca-108">When permission is granted, the app will connect to the Microsoft Graph as the current user to get the complete profile.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="673ca-109">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="673ca-109">Before you begin</span></span>

<span data-ttu-id="673ca-110">Instale los [requisitos previos](prerequisites.md) para garantizar que su entorno de desarrollo está configurado</span><span class="sxs-lookup"><span data-stu-id="673ca-110">Make sure your development environment is set up by installing the [prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="673ca-111">Requisitos previos para la instalación</span><span class="sxs-lookup"><span data-stu-id="673ca-111">Install prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="673ca-112">Crear un proyecto</span><span class="sxs-lookup"><span data-stu-id="673ca-112">Create your project</span></span>

<span data-ttu-id="673ca-113">Use el Kit de herramientas de Teams para crear su primer proyecto:</span><span class="sxs-lookup"><span data-stu-id="673ca-113">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="673ca-114">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="673ca-114">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="673ca-115">Abra Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="673ca-115">Open Visual Studio code.</span></span>
1. <span data-ttu-id="673ca-116">Abra el Kit de herramientas de Teams. Para ello, seleccione el icono de Teams en la barra lateral:</span><span class="sxs-lookup"><span data-stu-id="673ca-116">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icono de Teams en la barra lateral de Visual Studio Code.":::

1. <span data-ttu-id="673ca-118">Seleccione **Crear nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="673ca-118">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Ubicación del vínculo Crear nuevo proyecto en la barra lateral del Kit de herramientas de Teams.":::

1. <span data-ttu-id="673ca-120">Seleccione **Crear una nueva aplicación de Teams**.</span><span class="sxs-lookup"><span data-stu-id="673ca-120">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Inicio del Asistente para crear un nuevo proyecto":::

1. <span data-ttu-id="673ca-122">En el paso **Seleccionar funcionalidades**, ya estará seleccionada la funcionalidad de **Pestaña**.</span><span class="sxs-lookup"><span data-stu-id="673ca-122">On the **Select capabilities** step, the **Tab** capability will already be selected.</span></span>  <span data-ttu-id="673ca-123">Pulse **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="673ca-123">Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Captura de pantalla que muestra cómo agregar funcionalidades a la nueva aplicación.":::

1. <span data-ttu-id="673ca-125">En el paso **Tipo de hospedaje del front-end**, seleccione **Azure**.</span><span class="sxs-lookup"><span data-stu-id="673ca-125">On the **Frontend hosting type** step, select **Azure**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Captura de pantalla que muestra cómo seleccionar el hospedaje para la nueva aplicación.":::

1. <span data-ttu-id="673ca-127">En el paso **Recursos de nube**, pulse **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="673ca-127">On the **Cloud resources** step, press **OK**.</span></span>  <span data-ttu-id="673ca-128">No necesitamos recursos de nube adicionales para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="673ca-128">We do not need additional cloud resources for this tutorial.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="Captura de pantalla que muestra cómo agregar recursos de nube para la nueva aplicación.":::

1. <span data-ttu-id="673ca-130">En el paso **Lenguaje de programación**, seleccione **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="673ca-130">On the **Programming Language** step, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Captura de pantalla que muestra cómo seleccionar el lenguaje de programación.":::

1. <span data-ttu-id="673ca-132">Seleccione una carpeta de área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="673ca-132">Select a workspace folder.</span></span>  <span data-ttu-id="673ca-133">Se creará una carpeta dentro de la carpeta del área de trabajo para el proyecto que esté creando.</span><span class="sxs-lookup"><span data-stu-id="673ca-133">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="673ca-134">Escriba un nombre adecuado para la aplicación, como `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="673ca-134">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="673ca-135">El nombre de la aplicación solo puede contener caracteres alfanuméricos.</span><span class="sxs-lookup"><span data-stu-id="673ca-135">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="673ca-136">Presione **Entrar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="673ca-136">Press **Enter** to continue.</span></span>

<span data-ttu-id="673ca-137">La aplicación Teams se creará en unos segundos.</span><span class="sxs-lookup"><span data-stu-id="673ca-137">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="673ca-138">Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="673ca-138">Command line</span></span>](#tab/cli)

<span data-ttu-id="673ca-139">Use la CLI de `teamsfx` para crear su primer proyecto:</span><span class="sxs-lookup"><span data-stu-id="673ca-139">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="673ca-140">Comience en la carpeta en la que quiera crear la carpeta del proyecto.</span><span class="sxs-lookup"><span data-stu-id="673ca-140">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="673ca-141">La CLI le guiará por varias preguntas para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="673ca-141">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="673ca-142">En cada pregunta se le indicará cómo responder (por ejemplo, usando las teclas de dirección para seleccionar una opción).</span><span class="sxs-lookup"><span data-stu-id="673ca-142">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="673ca-143">Cuando haya respondido a la pregunta, presione **Entrar** para confirmar la elección.</span><span class="sxs-lookup"><span data-stu-id="673ca-143">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="673ca-144">Seleccione **Crear una nueva aplicación de Teams**.</span><span class="sxs-lookup"><span data-stu-id="673ca-144">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="673ca-145">Seleccione la funcionalidad de **Pestaña**.</span><span class="sxs-lookup"><span data-stu-id="673ca-145">Choose the **Tab** capability.</span></span>
1. <span data-ttu-id="673ca-146">Seleccione el hospedaje de front-end de **Azure**.</span><span class="sxs-lookup"><span data-stu-id="673ca-146">Select **Azure** frontend hosting.</span></span>
1. <span data-ttu-id="673ca-147">No seleccione ningún recurso de nube.</span><span class="sxs-lookup"><span data-stu-id="673ca-147">Do not select any cloud resources.</span></span>
1. <span data-ttu-id="673ca-148">Seleccione **JavaScript** como lenguaje de programación.</span><span class="sxs-lookup"><span data-stu-id="673ca-148">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="673ca-149">Presione **Entrar** para seleccionar la carpeta de área de trabajo predeterminada.</span><span class="sxs-lookup"><span data-stu-id="673ca-149">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="673ca-150">Escriba un nombre adecuado para la aplicación, como `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="673ca-150">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="673ca-151">El nombre de la aplicación solo puede contener caracteres alfanuméricos.</span><span class="sxs-lookup"><span data-stu-id="673ca-151">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="673ca-152">Una vez que haya respondido a todas las preguntas, se creará el proyecto.</span><span class="sxs-lookup"><span data-stu-id="673ca-152">Once all the questions have been answered, your project will be created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="673ca-153">Dar un paseo por el código fuente</span><span class="sxs-lookup"><span data-stu-id="673ca-153">Take a tour of the source code</span></span>

<span data-ttu-id="673ca-154">Si quiere omitir esta sección por ahora, puede [ejecutar la aplicación de forma local](#run-your-app-locally).</span><span class="sxs-lookup"><span data-stu-id="673ca-154">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="673ca-155">Una vez que el Kit de herramientas de Teams configure el proyecto, tendrá los componentes para crear una aplicación personal básica para Teams.</span><span class="sxs-lookup"><span data-stu-id="673ca-155">Once the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams.</span></span> <span data-ttu-id="673ca-156">Los archivos y directorios del proyecto se muestran en el área del Explorador de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="673ca-156">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/react-app-project.png" alt-text="Captura de pantalla que muestra los archivos de proyecto de la aplicación para una aplicación personal en Visual Studio Code.":::

<span data-ttu-id="673ca-158">El kit de herramientas crea automáticamente el scaffolding en el directorio del proyecto en función de las funcionalidades que ha agregado durante la configuración.</span><span class="sxs-lookup"><span data-stu-id="673ca-158">The Toolkit automatically creates scaffolding for you in the project directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="673ca-159">El Kit de herramientas de Teams mantiene el estado para la aplicación en el directorio `.fx`.</span><span class="sxs-lookup"><span data-stu-id="673ca-159">The Teams Toolkit maintains its state for your app in the `.fx` directory.</span></span>  <span data-ttu-id="673ca-160">Entre otros elementos de este directorio:</span><span class="sxs-lookup"><span data-stu-id="673ca-160">Among other items in this directory:</span></span>

- <span data-ttu-id="673ca-161">Los iconos de aplicación se almacenan como archivos PNG en `color.png` y `outline.png`.</span><span class="sxs-lookup"><span data-stu-id="673ca-161">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="673ca-162">El manifiesto de la aplicación para la publicación en el Portal de desarrolladores para Teams se almacena en `manifest.source.json`.</span><span class="sxs-lookup"><span data-stu-id="673ca-162">The app manifest for publishing to the Developer Portal for Teams is stored in `manifest.source.json`.</span></span>
- <span data-ttu-id="673ca-163">La configuración que eligió al crear el proyecto se almacena en `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="673ca-163">The settings you chose when creating the project are stored in `settings.json`.</span></span>

<span data-ttu-id="673ca-164">Después de seleccionar la funcionalidad de pestaña durante la configuración, el kit de herramientas de Microsoft Teams seleccionará todo el código necesario para crear una pestaña básica en el directorio `tabs`.</span><span class="sxs-lookup"><span data-stu-id="673ca-164">Since you selected the tab capability during setup, the Teams Toolkit scaffolds all the necessary code for a basic tab in the `tabs` directory.</span></span> <span data-ttu-id="673ca-165">En este directorio hay varios archivos importantes:</span><span class="sxs-lookup"><span data-stu-id="673ca-165">Within this directory there are several important files:</span></span>

- <span data-ttu-id="673ca-166">`tabs/src/index.jsx` es el punto de entrada de la aplicación front-end, donde el componente `App` principal se representa con `ReactDOM.render()`.</span><span class="sxs-lookup"><span data-stu-id="673ca-166">`tabs/src/index.jsx` is the front-end app's entry point, where the main `App` component is rendered with `ReactDOM.render()`.</span></span>
- <span data-ttu-id="673ca-167">`tabs/src/components/App.jsx` controla el enrutamiento de URL en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="673ca-167">`tabs/src/components/App.jsx` handles URL routing in your app.</span></span> <span data-ttu-id="673ca-168">Llama al [SDK del cliente de JavaScript de Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md) para establecer la comunicación entre la aplicación y Teams.</span><span class="sxs-lookup"><span data-stu-id="673ca-168">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>
- <span data-ttu-id="673ca-169">`tabs/src/components/Tab.jsx` contiene el código para implementar la interfaz de usuario de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="673ca-169">`tabs/src/components/Tab.jsx` contains the code to implement the UI of your app.</span></span>
- <span data-ttu-id="673ca-170">`tabs/src/components/TabConfig.jsx` contiene el código para implementar la interfaz de usuario que configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="673ca-170">`tabs/src/components/TabConfig.jsx` contains the code to implement the UI that configures your app.</span></span>

<span data-ttu-id="673ca-171">El tiempo de ejecución de Teams necesita varias pestañas, incluidos el aviso de privacidad, los términos de uso y las pestañas de configuración.</span><span class="sxs-lookup"><span data-stu-id="673ca-171">Several tabs are required by the Teams runtime, including the privacy notice, terms of use, and configuration tabs.</span></span>  <span data-ttu-id="673ca-172">El código del aviso de privacidad y los términos de uso se encuentran en el mismo directorio.</span><span class="sxs-lookup"><span data-stu-id="673ca-172">The code for the privacy notice and terms of use are located in the same directory.</span></span>

<span data-ttu-id="673ca-173">Al agregar funcionalidad de nube, se agregan directorios adicionales al proyecto.</span><span class="sxs-lookup"><span data-stu-id="673ca-173">When you add cloud functionality, additional directories are added to the project.</span></span>  <span data-ttu-id="673ca-174">En particular, el directorio `api` contiene el código para cualquier función de Azure que escriba.</span><span class="sxs-lookup"><span data-stu-id="673ca-174">Most notably, the `api` directory holds the code to any Azure Functions you write.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="673ca-175">Ejecutar la aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="673ca-175">Run your app locally</span></span>

<span data-ttu-id="673ca-176">El Kit de herramientas de Teams le permite ejecutar la aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="673ca-176">Teams Toolkit allows you to run your app locally.</span></span>  <span data-ttu-id="673ca-177">Se compone de varias partes que son necesarias para proporcionar la infraestructura correcta que espera Teams:</span><span class="sxs-lookup"><span data-stu-id="673ca-177">This consists of several parts that are necessary to provide the correct infrastructure that Teams expects:</span></span>

- <span data-ttu-id="673ca-178">Una aplicación se registra con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="673ca-178">An application is registered with Azure Active Directory.</span></span>  <span data-ttu-id="673ca-179">Esta aplicación tiene permisos asociados a la ubicación desde la que se carga la aplicación y a cualquier recurso del back-end al que accede.</span><span class="sxs-lookup"><span data-stu-id="673ca-179">This application has permissions associated with the location that the app is loaded from and any backend resources it accesses.</span></span>
- <span data-ttu-id="673ca-180">Una API web se hospeda para ayudar con las tareas de autenticación, actúa como un proxy entre la aplicación y Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="673ca-180">A web API is hosted to assist with authentication tasks, acting as a proxy between the app and Azure Active Directory.</span></span>  <span data-ttu-id="673ca-181">Esto lo ejecuta Azure Functions Core Tools.</span><span class="sxs-lookup"><span data-stu-id="673ca-181">This is run by Azure Functions Core Tools.</span></span>  <span data-ttu-id="673ca-182">Se puede acceder en la dirección URL `https://localhost:5000`.</span><span class="sxs-lookup"><span data-stu-id="673ca-182">It can be accessed at the URL `https://localhost:5000`.</span></span>
- <span data-ttu-id="673ca-183">Los recursos HTML, CSS y JavaScript que configuran el front-end de la aplicación se hospedan en un servicio local.</span><span class="sxs-lookup"><span data-stu-id="673ca-183">The HTML, CSS, and JavaScript resources that make up the front end of the app are hosted on a local service.</span></span> <span data-ttu-id="673ca-184">Se puede acceder en `https://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="673ca-184">It can be accessed at `https://localhost:3000`.</span></span>
- <span data-ttu-id="673ca-185">Se genera un manifiesto de aplicación y existe en el Portal de desarrolladores para Teams.</span><span class="sxs-lookup"><span data-stu-id="673ca-185">An app manifest is generated and exists in the Developer Portal for Teams.</span></span>  <span data-ttu-id="673ca-186">Teams usa el manifiesto de la aplicación para decir a los clientes conectados desde dónde cargar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="673ca-186">Teams uses the app manifest to tell connected clients where to load the app from.</span></span>

<span data-ttu-id="673ca-187">Una vez hecho, la aplicación se puede cargar en el cliente de Teams.</span><span class="sxs-lookup"><span data-stu-id="673ca-187">Once this is done, the app can be loaded within the Teams client.</span></span>  <span data-ttu-id="673ca-188">Usamos el cliente web de Teams para poder ver el código HTML, CSS y JavaScript en un entorno de desarrollo web estándar.</span><span class="sxs-lookup"><span data-stu-id="673ca-188">We use the Teams web client so that we can see the HTML, CSS, and JavaScript code within a standard web development environment.</span></span>

[!INCLUDE [Adjust your browser launch settings](~/includes/get-started/browser-private-launch.md)]

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a><span data-ttu-id="673ca-189">Compilar y ejecutar la aplicación de forma local en Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="673ca-189">Build and run your app locally in Visual Studio Code</span></span>

<span data-ttu-id="673ca-190">Para crear y ejecutar la aplicación localmente:</span><span class="sxs-lookup"><span data-stu-id="673ca-190">To build and run your app locally:</span></span>

1. <span data-ttu-id="673ca-191">Desde Visual Studio Code, presione **F5** para ejecutar la aplicación en modo de depuración.</span><span class="sxs-lookup"><span data-stu-id="673ca-191">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="673ca-192">Al ejecutar la aplicación por primera vez, se descargan todas las dependencias y se compila la aplicación.</span><span class="sxs-lookup"><span data-stu-id="673ca-192">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="673ca-193">Cuando se complete la compilación, se abrirá automáticamente una ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="673ca-193">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="673ca-194">Este proceso puede tardar entre 3 o 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="673ca-194">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="673ca-195">El Kit de herramientas le pedirá que instale un certificado local si es necesario.</span><span class="sxs-lookup"><span data-stu-id="673ca-195">The Toolkit will prompt you to install a local certificate if needed.</span></span> <span data-ttu-id="673ca-196">Este certificado permite a Teams cargar la aplicación desde `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="673ca-196">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="673ca-197">Seleccione Sí cuando aparezca el siguiente cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="673ca-197">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Captura de pantalla en la que se muestra la solicitud para instalar un certificado SSL para permitir que Teams cargue la aplicación desde localhost.":::

1. <span data-ttu-id="673ca-199">Se inicia el explorador web para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="673ca-199">Your web browser is started to run the application.</span></span> <span data-ttu-id="673ca-200">Si se le pide que abra Microsoft Teams, seleccione Cancelar para permanecer en el explorador.</span><span class="sxs-lookup"><span data-stu-id="673ca-200">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="673ca-201">Cuando se le pida, seleccione **Usar la aplicación web en su lugar**.</span><span class="sxs-lookup"><span data-stu-id="673ca-201">When prompted, select **Use the web app instead**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Captura de pantalla que muestra cómo elegir la versión web de Teams al iniciarlo":::

1. <span data-ttu-id="673ca-203">Es posible que se le pida que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="673ca-203">You may be prompted to sign in.</span></span>  <span data-ttu-id="673ca-204">Si es así, inicie sesión con su cuenta de M365.</span><span class="sxs-lookup"><span data-stu-id="673ca-204">If so, sign in with your M365 account.</span></span>
1. <span data-ttu-id="673ca-205">Cuando se le pida que instale la aplicación en Teams, presione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="673ca-205">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="673ca-206">Ahora se mostrará su aplicación:</span><span class="sxs-lookup"><span data-stu-id="673ca-206">Your app will now be displayed:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/react-finished-app.png" alt-text="Captura de pantalla de la aplicación completada":::

<span data-ttu-id="673ca-208">Puede realizar actividades de depuración normales como si se tratase de cualquier otra aplicación web (como establecer puntos de interrupción).</span><span class="sxs-lookup"><span data-stu-id="673ca-208">You can do normal debugging activities as if this were any other web application (such as setting breakpoints).</span></span> <span data-ttu-id="673ca-209">La aplicación es compatible con "hot reloading".</span><span class="sxs-lookup"><span data-stu-id="673ca-209">The app supports hot reloading.</span></span>  <span data-ttu-id="673ca-210">Si cambia cualquier archivo dentro del proyecto, la página se volverá a cargar.</span><span class="sxs-lookup"><span data-stu-id="673ca-210">If you change any file within the project, the page will be reloaded.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="673ca-211">Vea lo que ocurre al ejecutar la aplicación localmente en el depurador.</span><span class="sxs-lookup"><span data-stu-id="673ca-211">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="673ca-212">Cuando presionó F5, el Kit de herramientas de Teams:</span><span class="sxs-lookup"><span data-stu-id="673ca-212">When you pressed F5, the Teams Toolkit:</span></span>

1. <span data-ttu-id="673ca-213">Registró la aplicación con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="673ca-213">Registered your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="673ca-214">*Realizó la transferencia local* de la aplicación en Teams.</span><span class="sxs-lookup"><span data-stu-id="673ca-214">*Sideloaded* your app in Teams.</span></span>
1. <span data-ttu-id="673ca-215">Inició el back-end de la aplicación ejecutándose de forma local con [Azure Functions Core Tools](/azure/azure-functions/functions-run-local?#start).</span><span class="sxs-lookup"><span data-stu-id="673ca-215">Started your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="673ca-216">Inició el front-end de la aplicación hospedada localmente.</span><span class="sxs-lookup"><span data-stu-id="673ca-216">Started your application front-end hosted locally.</span></span>
1. <span data-ttu-id="673ca-217">Inició Microsoft Teams en un explorador web con un comando para indicar a Teams que transfiera localmente la aplicación desde `https://localhost:3000/tab` (la dirección URL está registrada dentro del manifiesto de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="673ca-217">Started Microsoft Teams in a web browser with a command to instruct Teams to side load the application from `https://localhost:3000/tab` (the URL is registered inside the application manifest).</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="673ca-218">Vea cómo solucionar problemas comunes al ejecutar localmente la aplicación.</span><span class="sxs-lookup"><span data-stu-id="673ca-218">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="673ca-219">Para ejecutar correctamente la aplicación en Teams, debe tener una cuenta de Teams que permita la instalación de prueba de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="673ca-219">To successfully run your app in Teams, you must have a Teams account that allows app sideloading.</span></span> <span data-ttu-id="673ca-220">Para más información sobre cómo abrir la cuenta, consulte [Requisitos previos](prerequisites.md#enable-sideloading).</span><span class="sxs-lookup"><span data-stu-id="673ca-220">For more information on account opening, see [prerequisites](prerequisites.md#enable-sideloading).</span></span>

</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="673ca-221">Vea lo que ocurre al implementar la aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="673ca-221">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="673ca-222">Antes de la implementación, la aplicación se ejecuta de forma local:</span><span class="sxs-lookup"><span data-stu-id="673ca-222">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="673ca-223">El back-end se ejecuta con _Azure Functions Core Tools_.</span><span class="sxs-lookup"><span data-stu-id="673ca-223">The backend runs using _Azure Functions Core Tools_.</span></span>
1. <span data-ttu-id="673ca-224">El punto de conexión HTTP de la aplicación, donde Microsoft Teams carga la aplicación, se ejecuta de forma local.</span><span class="sxs-lookup"><span data-stu-id="673ca-224">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="673ca-225">La implementación implica recursos de aprovisionamiento en una suscripción activa de Azure y la implementación (carga) del back-end y del código de front-end de la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="673ca-225">Deployment involves provisioning resources on an active Azure subscription and deploying (uploading) the backend and frontend code for the application to Azure.</span></span>

1. <span data-ttu-id="673ca-226">El back-end (si se configura) usa varios servicios de Azure, como Azure App Service y Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="673ca-226">The backend (if configured) uses a variety of Azure services, including Azure App Service and Azure Storage.</span></span>
1. <span data-ttu-id="673ca-227">La aplicación front-end se implementará en una cuenta de Azure Storage configurada para hospedaje web estático.</span><span class="sxs-lookup"><span data-stu-id="673ca-227">The frontend application will be deployed to an Azure Storage account configured for static web hosting.</span></span>

</details>

## <a name="next-steps"></a><span data-ttu-id="673ca-228">Siguientes pasos</span><span class="sxs-lookup"><span data-stu-id="673ca-228">Next steps</span></span>

<span data-ttu-id="673ca-229">Vea otros métodos para crear aplicaciones de Teams:</span><span class="sxs-lookup"><span data-stu-id="673ca-229">Learn about other methods for creating Teams apps:</span></span>

- [<span data-ttu-id="673ca-230">Crear una aplicación de Teams con Blazor</span><span class="sxs-lookup"><span data-stu-id="673ca-230">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
- <span data-ttu-id="673ca-231">[Crear una aplicación de Teams como elemento web de SharePoint](first-app-spfx.md) (no se necesita Azure)</span><span class="sxs-lookup"><span data-stu-id="673ca-231">[Create a Teams app as a SharePoint Web Part](first-app-spfx.md) (Azure not required)</span></span>
- [<span data-ttu-id="673ca-232">Crear una aplicación de bots de conversación</span><span class="sxs-lookup"><span data-stu-id="673ca-232">Create a conversational bot app</span></span>](first-app-bot.md)
- [<span data-ttu-id="673ca-233">Crear una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="673ca-233">Create a messaging extension</span></span>](first-message-extension.md)

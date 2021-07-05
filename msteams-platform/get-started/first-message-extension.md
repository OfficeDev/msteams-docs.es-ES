---
title: Cómo crear su primera extensión de mensajería
author: adrianhall
description: Cree una extensión de mensajería para Microsoft Teams con el Kit de herramientas de Teams.
ms.author: adhal
ms.date: 05/20/2021
ms.topic: quickstart
ms.openlocfilehash: 3566bc55c9995a8407b1344fbdb7d1548e210046
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254295"
---
# <a name="build-and-run-your-first-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="1f580-103">Crear y ejecutar la primera extensión de mensajería para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1f580-103">Build and run your first messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="1f580-104">En este tutorial, aprenderá *a* crear un comando de búsqueda para buscar datos externos e insertar los resultados en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="1f580-104">In this tutorial, you will learn how to create a *search command* to search for external data and insert the results into a message.</span></span> 

<span data-ttu-id="1f580-105">Hay dos tipos de extensiones de mensajería **Teams**:</span><span class="sxs-lookup"><span data-stu-id="1f580-105">There are two types of Teams **messaging extensions**:</span></span>

- <span data-ttu-id="1f580-106">[Los comandos de búsqueda](../messaging-extensions/how-to/search-commands/define-search-command.md) le permiten buscar sistemas externos e insertar los resultados de esa búsqueda en un mensaje con forma de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="1f580-106">[Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) allow you to search external systems and insert the results of that search into a message in the form of a card.</span></span>
- <span data-ttu-id="1f580-107">Los [comandos de acción](../messaging-extensions/how-to/action-commands/define-action-command.md) le permiten presentar a los usuarios una ventana emergente modal para recopilar o mostrar información y, a continuación, procesar su interacción y enviar información de nuevo a Teams.</span><span class="sxs-lookup"><span data-stu-id="1f580-107">[Action commands](../messaging-extensions/how-to/action-commands/define-action-command.md) allow you present your users with a modal popup to collect or display information, then process their interaction and send information back to Teams.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1f580-108">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="1f580-108">Before you begin</span></span>

<span data-ttu-id="1f580-109">Asegúrese de que el entorno de desarrollo está configurado mediante la instalación de los requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="1f580-109">Make sure your development environment is set up by installing the Prerequisites.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1f580-110">Requisitos previos de la instalación</span><span class="sxs-lookup"><span data-stu-id="1f580-110">Install Prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="1f580-111">Crear un proyecto</span><span class="sxs-lookup"><span data-stu-id="1f580-111">Create your project</span></span>

<span data-ttu-id="1f580-112">Use el Kit de herramientas de Teams para crear su primer proyecto:</span><span class="sxs-lookup"><span data-stu-id="1f580-112">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="1f580-113">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="1f580-113">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="1f580-114">Abrir Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="1f580-114">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="1f580-115">Seleccione el Teams en la barra lateral para abrir el Teams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="1f580-115">Select the Teams icon in the sidebar to open the Teams Toolkit.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icono de Teams en la barra lateral de Visual Studio Code.":::

1. <span data-ttu-id="1f580-117">Seleccione **Crear nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="1f580-117">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Ubicación del vínculo Crear nuevo proyecto en la barra lateral del Kit de herramientas de Teams.":::

1. <span data-ttu-id="1f580-119">Seleccione **Crear una nueva aplicación de Teams**.</span><span class="sxs-lookup"><span data-stu-id="1f580-119">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Inicio del Asistente para crear un nuevo proyecto":::

1. <span data-ttu-id="1f580-121">En la **sección Seleccionar capacidades,** seleccione **Extensión de mensaje**, anule la selección de **Tab** y **seleccione Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1f580-121">In the **Select capabilities** section, select **Message Extension**, deselect **Tab** and select **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-create-project-capabilities.png" alt-text="Captura de pantalla que muestra cómo agregar funcionalidades a la nueva aplicación.":::

1. <span data-ttu-id="1f580-123">En la **sección Registro del bot,** seleccione **Crear un nuevo registro de bot.**</span><span class="sxs-lookup"><span data-stu-id="1f580-123">In the **Bot registration** section, select **Create a new bot registration**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="Seleccione Crear un nuevo registro de bot":::

   > [!NOTE]
   > <span data-ttu-id="1f580-125">Las extensiones de mensajería dependen de los bots para proporcionar un diálogo entre el usuario y el código.</span><span class="sxs-lookup"><span data-stu-id="1f580-125">Messaging extensions rely on bots to provide a dialog between the user and your code.</span></span>

1. <span data-ttu-id="1f580-126">En la **sección Lenguaje de programación,** seleccione **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="1f580-126">In the **Programming Language** section, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Captura de pantalla que muestra cómo seleccionar el lenguaje de programación.":::

1. <span data-ttu-id="1f580-128">Seleccione una carpeta de área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="1f580-128">Select a workspace folder.</span></span>  <span data-ttu-id="1f580-129">Se creará una carpeta dentro de la carpeta del área de trabajo para el proyecto que esté creando.</span><span class="sxs-lookup"><span data-stu-id="1f580-129">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="1f580-130">Escriba un nombre adecuado para la aplicación, como `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="1f580-130">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="1f580-131">El nombre de la aplicación solo puede contener caracteres alfanuméricos.</span><span class="sxs-lookup"><span data-stu-id="1f580-131">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="1f580-132">Presione **Entrar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="1f580-132">Press **Enter** to continue.</span></span>

   <span data-ttu-id="1f580-133">La aplicación Teams se creará en unos segundos.</span><span class="sxs-lookup"><span data-stu-id="1f580-133">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="1f580-134">Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="1f580-134">Command line</span></span>](#tab/cli)

<span data-ttu-id="1f580-135">Use la CLI de `teamsfx` para crear su primer proyecto:</span><span class="sxs-lookup"><span data-stu-id="1f580-135">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="1f580-136">Comience en la carpeta en la que quiera crear la carpeta del proyecto.</span><span class="sxs-lookup"><span data-stu-id="1f580-136">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="1f580-137">La CLI le guiará por varias preguntas para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="1f580-137">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="1f580-138">En cada pregunta se le indicará cómo responder (por ejemplo, usando las teclas de dirección para seleccionar una opción).</span><span class="sxs-lookup"><span data-stu-id="1f580-138">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="1f580-139">Cuando haya respondido a la pregunta, presione **Entrar** para confirmar la elección.</span><span class="sxs-lookup"><span data-stu-id="1f580-139">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="1f580-140">Seleccione **Crear una nueva aplicación de Teams**.</span><span class="sxs-lookup"><span data-stu-id="1f580-140">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="1f580-141">Seleccione la **extensión de mensaje y** anule la selección de **tab**.</span><span class="sxs-lookup"><span data-stu-id="1f580-141">Select the **Message Extension** and deselect **Tab**.</span></span>
1. <span data-ttu-id="1f580-142">Seleccione **Crear un nuevo registro de bot**.</span><span class="sxs-lookup"><span data-stu-id="1f580-142">Select **Create a new bot registration**.</span></span>
1. <span data-ttu-id="1f580-143">Seleccione **JavaScript** como lenguaje de programación.</span><span class="sxs-lookup"><span data-stu-id="1f580-143">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="1f580-144">Presione **Entrar** para seleccionar la carpeta de área de trabajo predeterminada.</span><span class="sxs-lookup"><span data-stu-id="1f580-144">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="1f580-145">Escriba un nombre adecuado para la aplicación, como `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="1f580-145">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="1f580-146">El nombre de la aplicación solo puede contener caracteres alfanuméricos.</span><span class="sxs-lookup"><span data-stu-id="1f580-146">The name of the app must consist only of alphanumeric characters.</span></span>

   <span data-ttu-id="1f580-147">Una vez contestadas todas las preguntas, se crea el proyecto.</span><span class="sxs-lookup"><span data-stu-id="1f580-147">After all the questions have been answered, your project is created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="1f580-148">Dar un paseo por el código fuente</span><span class="sxs-lookup"><span data-stu-id="1f580-148">Take a tour of the source code</span></span>

<span data-ttu-id="1f580-149">Si quiere omitir esta sección por ahora, puede [ejecutar la aplicación de forma local](#run-your-app-locally).</span><span class="sxs-lookup"><span data-stu-id="1f580-149">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="1f580-150">Una extensión de mensajería usa [Bot Framework](https://docs.botframework.com) para permitir al usuario interactuar con el servicio a través de una conversación.</span><span class="sxs-lookup"><span data-stu-id="1f580-150">A messaging extension uses the [Bot Framework](https://docs.botframework.com) to allow the user to interact with your service via a conversation.</span></span>  <span data-ttu-id="1f580-151">Después del scaffolding, el proyecto tendrá el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="1f580-151">After scaffolding, your project will look like this:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-file-layout.png" alt-text="Distribución de archivos de un proyecto de bot.":::

<span data-ttu-id="1f580-153">El código bot se almacena en el directorio `bot`.</span><span class="sxs-lookup"><span data-stu-id="1f580-153">The bot code is stored in the `bot` directory.</span></span>  <span data-ttu-id="1f580-154">`bot/messageExtensionBot.js` es el punto de entrada principal de la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="1f580-154">The `bot/messageExtensionBot.js` is the main entry point for the messaging extension.</span></span>

> [!Tip]
> <span data-ttu-id="1f580-155">Familiarícese con los bots fuera de Teams antes de integrar su primer bot en Teams.</span><span class="sxs-lookup"><span data-stu-id="1f580-155">Familiarize yourself with bots outside of Teams before you integrate your first bot within Teams.</span></span>  <span data-ttu-id="1f580-156">Para encontrar más información sobre los bots, vea los tutoriales de [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="1f580-156">You can find more information about bots by reviewing the [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) tutorials.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="1f580-157">Ejecutar la aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="1f580-157">Run your app locally</span></span>

<span data-ttu-id="1f580-158">El Kit de herramientas de Teams le permite hospedar la aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="1f580-158">Teams Toolkit allows you to host your app locally.</span></span>  <span data-ttu-id="1f580-159">Para ello:</span><span class="sxs-lookup"><span data-stu-id="1f580-159">To do this:</span></span>

- <span data-ttu-id="1f580-160">Se registra una aplicación de Azure Active Directory en el inquilino de M365.</span><span class="sxs-lookup"><span data-stu-id="1f580-160">An Azure Active Directory Application is registered within the M365 tenant.</span></span>
- <span data-ttu-id="1f580-161">Se envía un manifiesto de la aplicación al Portal para desarrolladores de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1f580-161">An app manifest is submitted to the Developer Portal for Teams.</span></span>
- <span data-ttu-id="1f580-162">Se ejecuta localmente una API mediante Azure Functions Core Tools para admitir la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1f580-162">An API is run locally using Azure Functions Core Tools to support your app.</span></span>
- <span data-ttu-id="1f580-163">Se instala [ngrok](https://ngrok.io) y se usa para proporcionar un túnel entre Teams y la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="1f580-163">[ngrok](https://ngrok.io) is installed and used to provide a tunnel between Teams and your messaging extension.</span></span>

<span data-ttu-id="1f580-164">Para crear y ejecutar la aplicación localmente:</span><span class="sxs-lookup"><span data-stu-id="1f580-164">To build and run your app locally:</span></span>

1. <span data-ttu-id="1f580-165">Desde Visual Studio Code, presione la **tecla F5** para ejecutar la aplicación en modo de depuración.</span><span class="sxs-lookup"><span data-stu-id="1f580-165">From Visual Studio Code, press the **F5** key to run your application in debug mode.</span></span>

   > <span data-ttu-id="1f580-166">Al ejecutar la aplicación por primera vez, se descargan todas las dependencias y se compila la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1f580-166">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="1f580-167">Cuando se complete la compilación, se abrirá automáticamente una ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="1f580-167">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="1f580-168">Este proceso puede tardar entre 3 o 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="1f580-168">This can take 3-5 minutes to complete.</span></span>

1. <span data-ttu-id="1f580-169">Se cargará Teams en un explorador web y se le pedirá que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="1f580-169">Teams will be loaded in a web browser, and you will be prompted to sign in.</span></span> <span data-ttu-id="1f580-170">Si se le pide que abra Microsoft Teams, seleccione Cancelar para permanecer en el explorador.</span><span class="sxs-lookup"><span data-stu-id="1f580-170">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="1f580-171">Inicie sesión con su cuenta de M365.</span><span class="sxs-lookup"><span data-stu-id="1f580-171">Sign in with your M365 account.</span></span>

1. <span data-ttu-id="1f580-172">Selecciona **Agregar** para agregar la aplicación a tu cuenta.</span><span class="sxs-lookup"><span data-stu-id="1f580-172">Select **Add** to add the app to your account.</span></span>

   <span data-ttu-id="1f580-173">Después de cargar la aplicación, se te llevará directamente a un cuadro de diálogo de búsqueda:</span><span class="sxs-lookup"><span data-stu-id="1f580-173">After the app is loaded, you will be taken directly to a search dialog:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-completed-app.png" alt-text="Su extensión de mensajería basada en búsquedas en acción":::

   <span data-ttu-id="1f580-175">Escriba texto en el cuadro de búsqueda y, después, seleccione una de las opciones.</span><span class="sxs-lookup"><span data-stu-id="1f580-175">Type some text in the search box, then select one of the options.</span></span>  <span data-ttu-id="1f580-176">Se agregará una tarjeta adaptable al cuadro de entrada.</span><span class="sxs-lookup"><span data-stu-id="1f580-176">An adaptive card will be added to your input box.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="1f580-177">Vea lo que ocurre al ejecutar la aplicación localmente en el depurador.</span><span class="sxs-lookup"><span data-stu-id="1f580-177">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="1f580-178">Al presionar la tecla **F5,** el Teams Toolkit:</span><span class="sxs-lookup"><span data-stu-id="1f580-178">When you press the **F5** key, the Teams Toolkit:</span></span>

1. <span data-ttu-id="1f580-179">Registra la aplicación con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1f580-179">Registers your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="1f580-180">Registra la aplicación para la "carga lateral" en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1f580-180">Registers your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="1f580-181">Inicia el back-end de la aplicación que se ejecuta localmente [con Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span><span class="sxs-lookup"><span data-stu-id="1f580-181">Starts your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="1f580-182">Inicia un túnel ngrok para Teams comunicarse con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1f580-182">Starts an ngrok tunnel so Teams can communicate with your app.</span></span>
1. <span data-ttu-id="1f580-183">Inicia Microsoft Teams con un comando para indicar a Teams que desacargue la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1f580-183">Starts Microsoft Teams with a command to instruct Teams to sideload the application.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="1f580-184">Vea cómo solucionar problemas comunes al ejecutar localmente la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1f580-184">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="1f580-185">Para ejecutar correctamente la aplicación en Teams, debe tener una cuenta de desarrollo de Microsoft 365 que permita la instalación de prueba de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1f580-185">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="1f580-186">Para obtener más información sobre cómo abrir la cuenta, consulte [Requisitos previos](prerequisites.md#enable-sideloading).</span><span class="sxs-lookup"><span data-stu-id="1f580-186">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

> [!TIP]
> <span data-ttu-id="1f580-187">Antes de hacer la instalación de prueba de la aplicación, compruebe si hay algún problema con la [herramienta de validación de aplicaciones](https://dev.teams.microsoft.com/appvalidation.html), que se incluye en el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="1f580-187">Check for issues before sideloading your app, using the [app validation tool](https://dev.teams.microsoft.com/appvalidation.html), which is included in the toolkit.</span></span> <span data-ttu-id="1f580-188">Corrija los errores para hacer correctamente la instalación de prueba.</span><span class="sxs-lookup"><span data-stu-id="1f580-188">Fix the errors to successfully sideload the app.</span></span>
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary><span data-ttu-id="1f580-189">Vea lo que ocurre al implementar la aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="1f580-189">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="1f580-190">Antes de la implementación, la aplicación se ejecuta de forma local:</span><span class="sxs-lookup"><span data-stu-id="1f580-190">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="1f580-191">El back-end se ejecuta con _Azure Functions Core Tools_.</span><span class="sxs-lookup"><span data-stu-id="1f580-191">The backend runs using _Azure Functions Core Tools_.</span></span>
1. <span data-ttu-id="1f580-192">El punto de conexión HTTP de la aplicación, donde Microsoft Teams carga la aplicación, se ejecuta de forma local.</span><span class="sxs-lookup"><span data-stu-id="1f580-192">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="1f580-193">La implementación implica recursos de aprovisionamiento en una suscripción activa de Azure y la implementación (carga) del back-end y del código de front-end de la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="1f580-193">Deployment involves provisioning resources on an active Azure subscription and deploying (uploading) the backend and frontend code for the application to Azure.</span></span> <span data-ttu-id="1f580-194">El back-end usa varios servicios de Azure, como Azure App Service y Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="1f580-194">The backend uses a variety of Azure services, including Azure App Service and Azure Bot Service.</span></span>

</details>

## <a name="add-a-configuration-page-to-your-messaging-extension"></a><span data-ttu-id="1f580-195">Agregar una página de configuración a la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="1f580-195">Add a configuration page to your messaging extension</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="code-sample"></a><span data-ttu-id="1f580-196">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="1f580-196">Code sample</span></span>

<span data-ttu-id="1f580-197">El Teams configuración de autenticación de búsqueda para proyectos de ejemplo en GitHub, muestra cómo crear extensiones de mensajería que incluyen una página de configuración y autenticación de [servicio de bot.](https://github.com/microsoft/BotBuilder-Samples#teams-samples)</span><span class="sxs-lookup"><span data-stu-id="1f580-197">The Teams Search Auth Config for sample projects on GitHub, demonstrate how to create messaging extensions that include a configuration page and [Bot Service authentication](https://github.com/microsoft/BotBuilder-Samples#teams-samples).</span></span> <span data-ttu-id="1f580-198">Los ejemplos también muestran cómo crear extensiones de mensaje que acepten solicitudes de búsqueda y devuelvan los resultados después de que el usuario haya iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="1f580-198">The samples also demonstrate how to create message extensions that accept search requests and return the results after the user has signed in.</span></span>

| <span data-ttu-id="1f580-199">**Nombre de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="1f580-199">**Sample name**</span></span> | <span data-ttu-id="1f580-200">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="1f580-200">**Description**</span></span> | <span data-ttu-id="1f580-201">**.NET**</span><span class="sxs-lookup"><span data-stu-id="1f580-201">**.NET**</span></span> | <span data-ttu-id="1f580-202">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="1f580-202">**Node.js**</span></span> | <span data-ttu-id="1f580-203">**Python**</span><span class="sxs-lookup"><span data-stu-id="1f580-203">**Python**</span></span> |
|-----------------|-----------------|-------------|--------------|--------|
| <span data-ttu-id="1f580-204">Generador de bots</span><span class="sxs-lookup"><span data-stu-id="1f580-204">Bot builder</span></span> | <span data-ttu-id="1f580-205">Para crear extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="1f580-205">To create messaging extensions.</span></span> | [<span data-ttu-id="1f580-206">View</span><span class="sxs-lookup"><span data-stu-id="1f580-206">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) | [<span data-ttu-id="1f580-207">View</span><span class="sxs-lookup"><span data-stu-id="1f580-207">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config) | [<span data-ttu-id="1f580-208">View</span><span class="sxs-lookup"><span data-stu-id="1f580-208">View</span></span>]( https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |

## <a name="additional-code-sample"></a><span data-ttu-id="1f580-209">Ejemplo de código adicional</span><span class="sxs-lookup"><span data-stu-id="1f580-209">Additional code sample</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1f580-210">Ver más ejemplos de Bot Framework en GitHub</span><span class="sxs-lookup"><span data-stu-id="1f580-210">View more Bot Framework Samples on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-samples#messaging-extensions-samples-using-the-v4-sdk)

## <a name="see-also"></a><span data-ttu-id="1f580-211">Vea también</span><span class="sxs-lookup"><span data-stu-id="1f580-211">See also</span></span>

* [<span data-ttu-id="1f580-212">Introducción a tutoriales</span><span class="sxs-lookup"><span data-stu-id="1f580-212">Tutorials Overview</span></span>](code-samples.md) 
* [<span data-ttu-id="1f580-213">Crear una aplicación con React</span><span class="sxs-lookup"><span data-stu-id="1f580-213">Create an app using React</span></span>](first-app-react.md)
* [<span data-ttu-id="1f580-214">Crear una aplicación con Blazor</span><span class="sxs-lookup"><span data-stu-id="1f580-214">Create an app using Blazor</span></span>](first-app-blazor.md)
* [<span data-ttu-id="1f580-215">Crear una aplicación con SPFx</span><span class="sxs-lookup"><span data-stu-id="1f580-215">Create an app using SPFx</span></span>](first-app-spfx.md)
* [<span data-ttu-id="1f580-216">Crear una aplicación con C# o .NET</span><span class="sxs-lookup"><span data-stu-id="1f580-216">Create an app using C# or .NET</span></span>](get-started-dotnet-app-studio.md)
* [<span data-ttu-id="1f580-217">Crear una aplicación con Node.js</span><span class="sxs-lookup"><span data-stu-id="1f580-217">Create an app using Node.js</span></span>](get-started-nodejs-app-studio.md)
* [<span data-ttu-id="1f580-218">Crear una aplicación con el generador de Yeoman</span><span class="sxs-lookup"><span data-stu-id="1f580-218">Create an app using Yeoman generator</span></span>](get-started-yeoman.md)
* [<span data-ttu-id="1f580-219">Crear una aplicación de bots de conversación</span><span class="sxs-lookup"><span data-stu-id="1f580-219">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="1f580-220">Muestras de código</span><span class="sxs-lookup"><span data-stu-id="1f580-220">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)
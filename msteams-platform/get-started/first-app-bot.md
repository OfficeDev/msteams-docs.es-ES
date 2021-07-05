---
title: 'Introducción: Cree su primer bot de conversación'
author: adrianhall
description: Crear un bot de conversación para Microsoft Teams con el Kit de herramientas de Microsoft Teams.
ms.author: adhal
ms.date: 05/27/2021
ms.topic: quickstart
ms.openlocfilehash: 96bbddd99b6901a4b92e1e2f2dc98482c755dc66
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254254"
---
# <a name="build-your-first-conversational-bot-for-microsoft-teams"></a><span data-ttu-id="f1db4-103">Cree su primer bot de conversación para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f1db4-103">Build your first conversational bot for Microsoft Teams</span></span>

<span data-ttu-id="f1db4-104">En este tutorial, aprenderá a crear, ejecutar e implementar una aplicación de bot de Teams.</span><span class="sxs-lookup"><span data-stu-id="f1db4-104">In this tutorial, you will learn how to build, run, and deploy a Teams bot app.</span></span> <span data-ttu-id="f1db4-105">Un bot actúa como intermediario entre un usuario de Microsoft Teams y un servicio web.</span><span class="sxs-lookup"><span data-stu-id="f1db4-105">A bot acts as an intermediary between a Teams user and a web service.</span></span>  <span data-ttu-id="f1db4-106">Los usuarios pueden chatear con un bot para obtener información rápidamente, iniciar flujos de trabajo o cualquier otra cosa que el servicio web pueda hacer.</span><span class="sxs-lookup"><span data-stu-id="f1db4-106">Users can chat with a bot to quickly get information, initiate workflows, or anything else your web service can do.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="f1db4-107">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="f1db4-107">Before you begin</span></span>

<span data-ttu-id="f1db4-108">Asegúrese de que el entorno de desarrollo está configurado mediante la instalación de los requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="f1db4-108">Make sure your development environment is set up by installing the Prerequisites.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f1db4-109">Requisitos previos de la instalación</span><span class="sxs-lookup"><span data-stu-id="f1db4-109">Install Prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="f1db4-110">Crear un proyecto</span><span class="sxs-lookup"><span data-stu-id="f1db4-110">Create your project</span></span>

<span data-ttu-id="f1db4-111">Use el Kit de herramientas de Teams para crear su primer proyecto:</span><span class="sxs-lookup"><span data-stu-id="f1db4-111">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="f1db4-112">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="f1db4-112">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="f1db4-113">Abra Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f1db4-113">Open Visual Studio code.</span></span>
1. <span data-ttu-id="f1db4-114">Seleccione el Teams en la barra lateral para abrir el Teams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="f1db4-114">Select the Teams icon in the sidebar to open the Teams Toolkit.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icono de Teams en la barra lateral de Visual Studio Code.":::

1. <span data-ttu-id="f1db4-116">Seleccione **Crear nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="f1db4-116">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Ubicación del vínculo Crear nuevo proyecto en la barra lateral del Kit de herramientas de Teams.":::

1. <span data-ttu-id="f1db4-118">Seleccione **Crear una nueva aplicación de Teams**.</span><span class="sxs-lookup"><span data-stu-id="f1db4-118">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Inicio del Asistente para crear un nuevo proyecto":::

1. <span data-ttu-id="f1db4-120">En la **sección Seleccionar capacidades,** **seleccione Bot**, anule la selección de **Tab** y seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f1db4-120">In the **Select capabilities** section, select **Bot**, deselect **Tab** and select **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities-bot.png" alt-text="Captura de pantalla que muestra cómo agregar funcionalidades a la nueva aplicación.":::

1. <span data-ttu-id="f1db4-122">En la **sección Registro del bot,** seleccione **Crear un nuevo registro de bot.**</span><span class="sxs-lookup"><span data-stu-id="f1db4-122">In the **Bot registration** section, select **Create a new bot registration**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="Seleccione Crear un nuevo registro de bot":::

1. <span data-ttu-id="f1db4-124">En la **sección Lenguaje de programación,** seleccione **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="f1db4-124">In the **Programming Language** section, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Captura de pantalla que muestra cómo seleccionar el lenguaje de programación.":::

1. <span data-ttu-id="f1db4-126">Seleccione una carpeta de área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f1db4-126">Select a workspace folder.</span></span>  <span data-ttu-id="f1db4-127">Se creará una carpeta dentro de la carpeta del área de trabajo para el proyecto que esté creando.</span><span class="sxs-lookup"><span data-stu-id="f1db4-127">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="f1db4-128">Escriba un nombre adecuado para la aplicación, como `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="f1db4-128">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="f1db4-129">El nombre de la aplicación solo debe contener caracteres alfanuméricos.</span><span class="sxs-lookup"><span data-stu-id="f1db4-129">The name of the app must contain only alphanumeric characters.</span></span>  <span data-ttu-id="f1db4-130">Presione **Entrar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="f1db4-130">Press **Enter** to continue.</span></span>

<span data-ttu-id="f1db4-131">La aplicación Teams se creará en unos segundos.</span><span class="sxs-lookup"><span data-stu-id="f1db4-131">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="f1db4-132">Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="f1db4-132">Command line</span></span>](#tab/cli)

<span data-ttu-id="f1db4-133">Use la CLI de `teamsfx` para crear su primer proyecto:</span><span class="sxs-lookup"><span data-stu-id="f1db4-133">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="f1db4-134">Comience en la carpeta en la que quiera crear la carpeta del proyecto.</span><span class="sxs-lookup"><span data-stu-id="f1db4-134">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="f1db4-135">La CLI le guiará por varias preguntas para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="f1db4-135">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="f1db4-136">En cada pregunta se le indicará cómo responder (por ejemplo, usando las teclas de dirección para seleccionar una opción).</span><span class="sxs-lookup"><span data-stu-id="f1db4-136">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="f1db4-137">Cuando haya respondido a la pregunta, presione **Entrar** para confirmar la elección.</span><span class="sxs-lookup"><span data-stu-id="f1db4-137">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="f1db4-138">Seleccione **Crear una nueva aplicación de Teams**.</span><span class="sxs-lookup"><span data-stu-id="f1db4-138">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="f1db4-139">Seleccione **Bot** y anule la selección de **Tab**.</span><span class="sxs-lookup"><span data-stu-id="f1db4-139">Select **Bot** and deselect **Tab**.</span></span>
1. <span data-ttu-id="f1db4-140">Seleccione **Crear un nuevo registro de bot**.</span><span class="sxs-lookup"><span data-stu-id="f1db4-140">Select **Create a new bot registration**.</span></span>
1. <span data-ttu-id="f1db4-141">Seleccione **JavaScript** como lenguaje de programación.</span><span class="sxs-lookup"><span data-stu-id="f1db4-141">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="f1db4-142">Presione **Entrar** para seleccionar la carpeta de área de trabajo predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f1db4-142">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="f1db4-143">Escriba un nombre adecuado para la aplicación, como `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="f1db4-143">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="f1db4-144">El nombre de la aplicación solo puede contener caracteres alfanuméricos.</span><span class="sxs-lookup"><span data-stu-id="f1db4-144">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="f1db4-145">Una vez contestadas todas las preguntas, se crea el proyecto.</span><span class="sxs-lookup"><span data-stu-id="f1db4-145">After all the questions have been answered, your project is created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="f1db4-146">Dar un paseo por el código fuente</span><span class="sxs-lookup"><span data-stu-id="f1db4-146">Take a tour of the source code</span></span>

<span data-ttu-id="f1db4-147">Si quiere omitir esta sección por ahora, puede [ejecutar la aplicación de forma local](#run-your-app-locally).</span><span class="sxs-lookup"><span data-stu-id="f1db4-147">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="f1db4-148">Una extensión de mensajería usa [Bot Framework](https://docs.botframework.com) para permitir al usuario interactuar con el servicio a través de una conversación.</span><span class="sxs-lookup"><span data-stu-id="f1db4-148">A messaging extension uses the [Bot Framework](https://docs.botframework.com) to allow the user to interact with your service via a conversation.</span></span>  <span data-ttu-id="f1db4-149">Después del scaffolding, el proyecto tendrá el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="f1db4-149">After scaffolding, your project will look like this:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/bot-file-layout.png" alt-text="Distribución de archivos de un proyecto de bot.":::

<span data-ttu-id="f1db4-151">El código bot se almacena en el directorio `bot`.</span><span class="sxs-lookup"><span data-stu-id="f1db4-151">The bot code is stored in the `bot` directory.</span></span>  <span data-ttu-id="f1db4-152">El `bot/teamsBot.js` es el punto de entrada principal para el bot, y los cuadros de diálogo se almacenan en el directorio `dialogs`.</span><span class="sxs-lookup"><span data-stu-id="f1db4-152">The `bot/teamsBot.js` is the main entry point for the bot, and the dialogs are stored in the `dialogs` directory.</span></span>

> [!Tip]
> <span data-ttu-id="f1db4-153">Familiarícese con los bots fuera de Teams antes de integrar su primer bot en Teams.</span><span class="sxs-lookup"><span data-stu-id="f1db4-153">Familiarize yourself with bots outside of Teams before you integrate your first bot within Teams.</span></span>  <span data-ttu-id="f1db4-154">Para encontrar más información sobre los bots, vea los tutoriales de [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="f1db4-154">You can find more information about bots by reviewing the [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) tutorials.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="f1db4-155">Ejecutar la aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="f1db4-155">Run your app locally</span></span>

<span data-ttu-id="f1db4-156">El Kit de herramientas de Teams le permite hospedar la aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="f1db4-156">Teams Toolkit allows you to host your app locally.</span></span>  <span data-ttu-id="f1db4-157">Para ello:</span><span class="sxs-lookup"><span data-stu-id="f1db4-157">To do this:</span></span>

- <span data-ttu-id="f1db4-158">Se registra una aplicación de Azure Active Directory en el inquilino de M365.</span><span class="sxs-lookup"><span data-stu-id="f1db4-158">An Azure Active Directory Application is registered within the M365 tenant.</span></span>
- <span data-ttu-id="f1db4-159">Se envía un manifiesto de la aplicación al Centro para desarrolladores de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="f1db4-159">An app manifest is submitted to the Developer Center for Teams.</span></span>
- <span data-ttu-id="f1db4-160">Se ejecuta localmente una API mediante Azure Functions Core Tools para admitir la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f1db4-160">An API is run locally using Azure Functions Core Tools to support your app.</span></span>
- <span data-ttu-id="f1db4-161">Se instala [ngrok](https://ngrok.io) y se usa para proporcionar un túnel entre Teams y el código bot.</span><span class="sxs-lookup"><span data-stu-id="f1db4-161">[ngrok](https://ngrok.io) is installed and used to provide a tunnel between Teams and your bot code.</span></span>

<span data-ttu-id="f1db4-162">Para crear y ejecutar la aplicación localmente:</span><span class="sxs-lookup"><span data-stu-id="f1db4-162">To build and run your app locally:</span></span>

1. <span data-ttu-id="f1db4-163">Desde Visual Studio Code, presione la **tecla F5** para ejecutar la aplicación en modo de depuración.</span><span class="sxs-lookup"><span data-stu-id="f1db4-163">From Visual Studio Code, press the **F5** key to run your application in debug mode.</span></span>

   > <span data-ttu-id="f1db4-164">Al ejecutar la aplicación por primera vez, se descargan todas las dependencias y se compila la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f1db4-164">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="f1db4-165">Cuando se complete la compilación, se abrirá automáticamente una ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="f1db4-165">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="f1db4-166">Este proceso puede tardar entre 3 o 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="f1db4-166">This can take 3-5 minutes to complete.</span></span>

1. <span data-ttu-id="f1db4-167">El explorador web comienza a ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f1db4-167">Your web browser starts to run the app.</span></span> <span data-ttu-id="f1db4-168">Si se le pide que abra Teams escritorio, seleccione **Cancelar** para permanecer en el explorador.</span><span class="sxs-lookup"><span data-stu-id="f1db4-168">If prompted to open Teams desktop, select **Cancel** to remain in the browser.</span></span> <span data-ttu-id="f1db4-169">Es posible que también se le pida que cambie a Teams escritorio en otras ocasiones; seleccione la Teams web cuando esto suceda.</span><span class="sxs-lookup"><span data-stu-id="f1db4-169">You may also be prompted to switch to Teams desktop at other times; select the Teams web app when this happens.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Captura de pantalla que muestra cómo elegir la versión web de Teams al iniciarlo":::

1. <span data-ttu-id="f1db4-171">Es posible que se le pida que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="f1db4-171">You may be prompted to sign in.</span></span>  <span data-ttu-id="f1db4-172">Si es así, inicie sesión con su cuenta de M365.</span><span class="sxs-lookup"><span data-stu-id="f1db4-172">If so, sign in with your M365 account.</span></span>
1. <span data-ttu-id="f1db4-173">Cuando se le pida que instale la aplicación en Teams, seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f1db4-173">When prompted to install the app onto Teams, select **Add**.</span></span>

   <span data-ttu-id="f1db4-174">Después de cargar la aplicación, se te llevará directamente a una sesión de chat con el bot.</span><span class="sxs-lookup"><span data-stu-id="f1db4-174">After the app is loaded, you will be taken directly to a chat session with the bot.</span></span>  <span data-ttu-id="f1db4-175">Puede escribir `intro` para que se muestre una tarjeta de introducción, y `show` para que se muestren los detalles de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="f1db4-175">You can type `intro` to show an introduction card, and `show` to show your details from Microsoft Graph.</span></span>  <span data-ttu-id="f1db4-176">(Esto requerirá una aprobación de permisos adicional).</span><span class="sxs-lookup"><span data-stu-id="f1db4-176">(This will require an additional permissions approval).</span></span>

   <span data-ttu-id="f1db4-177">La depuración funciona según lo esperado, pruébelo.</span><span class="sxs-lookup"><span data-stu-id="f1db4-177">Debugging works as you normally would expect - try it yourself!</span></span> <span data-ttu-id="f1db4-178">Abra el archivo `bot/dialogs/rootDialog.js` y busque el método `triggerCommand(...)`.</span><span class="sxs-lookup"><span data-stu-id="f1db4-178">Open the `bot/dialogs/rootDialog.js` file and locate the `triggerCommand(...)` method.</span></span>  <span data-ttu-id="f1db4-179">Defina un punto de interrupción en el caso predeterminado.</span><span class="sxs-lookup"><span data-stu-id="f1db4-179">Set a breakpoint on the default case.</span></span>  <span data-ttu-id="f1db4-180">Escriba alguna cosa.</span><span class="sxs-lookup"><span data-stu-id="f1db4-180">Then type some text.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="f1db4-181">Vea lo que ocurre al ejecutar la aplicación localmente en el depurador.</span><span class="sxs-lookup"><span data-stu-id="f1db4-181">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="f1db4-182">Al presionar la tecla **F5,** el Teams Toolkit:</span><span class="sxs-lookup"><span data-stu-id="f1db4-182">When you press the **F5** key, the Teams Toolkit:</span></span>

1. <span data-ttu-id="f1db4-183">Registra la aplicación con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f1db4-183">Registers your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="f1db4-184">Registra la aplicación para la "carga lateral" en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="f1db4-184">Registers your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="f1db4-185">Inicia el back-end de la aplicación que se ejecuta localmente [con Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span><span class="sxs-lookup"><span data-stu-id="f1db4-185">Starts your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="f1db4-186">Inicia un túnel ngrok para Teams comunicarse con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f1db4-186">Starts an ngrok tunnel so Teams can communicate with your app.</span></span>
1. <span data-ttu-id="f1db4-187">Inicia Microsoft Teams con un comando para indicar a Teams que desacargue la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f1db4-187">Starts Microsoft Teams with a command to instruct Teams to sideload the application.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="f1db4-188">Vea cómo solucionar problemas comunes al ejecutar localmente la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f1db4-188">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="f1db4-189">Para ejecutar correctamente la aplicación en Teams, debe tener una cuenta de desarrollo de Microsoft 365 que permita la instalación de prueba de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f1db4-189">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="f1db4-190">Para obtener más información sobre cómo abrir la cuenta, consulte [Requisitos previos](prerequisites.md#enable-sideloading).</span><span class="sxs-lookup"><span data-stu-id="f1db4-190">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

> [!TIP]
> <span data-ttu-id="f1db4-191">Antes de hacer la instalación de prueba de la aplicación, compruebe si hay algún problema con la [herramienta de validación de aplicaciones](https://dev.teams.microsoft.com/appvalidation.html), que se incluye en el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="f1db4-191">Check for issues before sideloading your app, using the [app validation tool](https://dev.teams.microsoft.com/appvalidation.html), which is included in the toolkit.</span></span> <span data-ttu-id="f1db4-192">Corrija los errores para hacer correctamente la instalación de prueba.</span><span class="sxs-lookup"><span data-stu-id="f1db4-192">Fix the errors to successfully sideload the app.</span></span>
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary><span data-ttu-id="f1db4-193">Vea lo que ocurre al implementar la aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="f1db4-193">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="f1db4-194">Antes de la implementación, la aplicación se ejecuta de forma local:</span><span class="sxs-lookup"><span data-stu-id="f1db4-194">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="f1db4-195">El back-end se ejecuta con _Azure Functions Core Tools_.</span><span class="sxs-lookup"><span data-stu-id="f1db4-195">The backend runs using _Azure Functions Core Tools_.</span></span>
1. <span data-ttu-id="f1db4-196">El punto de conexión HTTP de la aplicación, donde Microsoft Teams carga la aplicación, se ejecuta de forma local.</span><span class="sxs-lookup"><span data-stu-id="f1db4-196">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

   <span data-ttu-id="f1db4-197">La implementación implica recursos de aprovisionamiento en una suscripción activa de Azure y la implementación (carga) del back-end y del código de front-end de la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="f1db4-197">Deployment involves provisioning resources on an active Azure subscription and deploying (uploading) the backend and frontend code for the application to Azure.</span></span> <span data-ttu-id="f1db4-198">El back-end usa varios servicios de Azure, como Azure App Service y Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="f1db4-198">The backend uses a variety of Azure services, including Azure App Service and Azure Bot Service.</span></span>

</details>

## <a name="see-also"></a><span data-ttu-id="f1db4-199">Vea también</span><span class="sxs-lookup"><span data-stu-id="f1db4-199">See also</span></span>

* [<span data-ttu-id="f1db4-200">Introducción a tutoriales</span><span class="sxs-lookup"><span data-stu-id="f1db4-200">Tutorials Overview</span></span>](code-samples.md) 
* [<span data-ttu-id="f1db4-201">Crear una aplicación con React</span><span class="sxs-lookup"><span data-stu-id="f1db4-201">Create an app using React</span></span>](first-app-react.md)
* [<span data-ttu-id="f1db4-202">Crear una aplicación con Blazor</span><span class="sxs-lookup"><span data-stu-id="f1db4-202">Create an app using Blazor</span></span>](first-app-blazor.md)
* [<span data-ttu-id="f1db4-203">Crear una aplicación con SPFx</span><span class="sxs-lookup"><span data-stu-id="f1db4-203">Create an app using SPFx</span></span>](first-app-spfx.md)
* [<span data-ttu-id="f1db4-204">Crear una aplicación con C# o .NET</span><span class="sxs-lookup"><span data-stu-id="f1db4-204">Create an app using C# or .NET</span></span>](get-started-dotnet-app-studio.md)
* [<span data-ttu-id="f1db4-205">Crear una aplicación con Node.js</span><span class="sxs-lookup"><span data-stu-id="f1db4-205">Create an app using Node.js</span></span>](get-started-nodejs-app-studio.md)
* [<span data-ttu-id="f1db4-206">Crear una aplicación con el generador de Yeoman</span><span class="sxs-lookup"><span data-stu-id="f1db4-206">Create an app using Yeoman generator</span></span>](get-started-yeoman.md)
* [<span data-ttu-id="f1db4-207">Crear una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="f1db4-207">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="f1db4-208">Muestras de código</span><span class="sxs-lookup"><span data-stu-id="f1db4-208">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)
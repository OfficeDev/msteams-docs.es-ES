---
title: Cómo crear su primera extensión de mensajería
author: adrianhall
description: Cree una extensión de mensajería para Microsoft Teams con el Kit de herramientas de Teams.
ms.author: adhal
ms.date: 05/20/2021
ms.topic: quickstart
ms.openlocfilehash: cb37bc97c3b9de8ce469728e4c1b0e09ba1c2942
ms.sourcegitcommit: 99b1f151e4e36a86c6a5d2ccbde01bf45b61f526
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2021
ms.locfileid: "53037638"
---
# <a name="build-and-run-your-first-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="b1e29-103">Crear y ejecutar la primera extensión de mensajería para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b1e29-103">Build and run your first messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="b1e29-104">Hay dos tipos de extensiones de mensajería **Teams**:</span><span class="sxs-lookup"><span data-stu-id="b1e29-104">There are two types of Teams **messaging extensions**:</span></span>

- <span data-ttu-id="b1e29-105">[Los comandos de búsqueda](../messaging-extensions/how-to/search-commands/define-search-command.md) le permiten buscar sistemas externos e insertar los resultados de esa búsqueda en un mensaje con forma de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="b1e29-105">[Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) allow you to search external systems and insert the results of that search into a message in the form of a card.</span></span>
- <span data-ttu-id="b1e29-106">Los [comandos de acción](../messaging-extensions/how-to/action-commands/define-action-command.md) le permiten presentar a los usuarios una ventana emergente modal para recopilar o mostrar información y, a continuación, procesar su interacción y enviar información de nuevo a Teams.</span><span class="sxs-lookup"><span data-stu-id="b1e29-106">[Action commands](../messaging-extensions/how-to/action-commands/define-action-command.md) allow you present your users with a modal popup to collect or display information, then process their interaction and send information back to Teams.</span></span>

<span data-ttu-id="b1e29-107">En este tutorial, creará un *comando de búsqueda* para buscar datos externos e insertar los resultados en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="b1e29-107">In this tutorial, you will create a *search command* to search for external data and insert the results into a message.</span></span>  

## <a name="before-you-begin"></a><span data-ttu-id="b1e29-108">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="b1e29-108">Before you begin</span></span>

<span data-ttu-id="b1e29-109">Instale los [requisitos previos](prerequisites.md) para garantizar que su entorno de desarrollo está configurado</span><span class="sxs-lookup"><span data-stu-id="b1e29-109">Make sure your development environment is set up by installing the [Prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b1e29-110">Requisitos previos de la instalación</span><span class="sxs-lookup"><span data-stu-id="b1e29-110">Install Prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="b1e29-111">Crear un proyecto</span><span class="sxs-lookup"><span data-stu-id="b1e29-111">Create your project</span></span>

<span data-ttu-id="b1e29-112">Use el Kit de herramientas de Teams para crear su primer proyecto:</span><span class="sxs-lookup"><span data-stu-id="b1e29-112">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="b1e29-113">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="b1e29-113">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="b1e29-114">Abrir Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="b1e29-114">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="b1e29-115">Abra el Kit de herramientas de Microsoft Teams. Para ello, seleccione el icono de Teams en la barra lateral:</span><span class="sxs-lookup"><span data-stu-id="b1e29-115">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icono de Teams en la barra lateral de Visual Studio Code.":::

1. <span data-ttu-id="b1e29-117">Seleccione **Crear nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="b1e29-117">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Ubicación del vínculo Crear nuevo proyecto en la barra lateral del Kit de herramientas de Teams.":::

1. <span data-ttu-id="b1e29-119">Seleccione **Crear una nueva aplicación de Teams**.</span><span class="sxs-lookup"><span data-stu-id="b1e29-119">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Inicio del Asistente para crear un nuevo proyecto":::

1. <span data-ttu-id="b1e29-121">En el paso **Seleccionar funcionalidades**, seleccione **Extensión de mensajería** y desmarque la opción **Pestaña**. Presione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b1e29-121">On the **Select capabilities** step, select **Message Extension** and deselect **Tab**.  Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-create-project-capabilities.png" alt-text="Captura de pantalla que muestra cómo agregar funcionalidades a la nueva aplicación.":::

1. <span data-ttu-id="b1e29-123">En el paso **Registro de bot**, seleccione **Crear un nuevo registro de bot**.</span><span class="sxs-lookup"><span data-stu-id="b1e29-123">On the **Bot registration** step, select **Create a new bot registration**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="Seleccione Crear un nuevo registro de bot":::

   > [!NOTE]
   > <span data-ttu-id="b1e29-125">Las extensiones de mensajería dependen de los bots para proporcionar un diálogo entre el usuario y el código.</span><span class="sxs-lookup"><span data-stu-id="b1e29-125">Messaging extensions rely on bots to provide a dialog between the user and your code.</span></span>

1. <span data-ttu-id="b1e29-126">En el paso **Lenguaje de programación**, seleccione **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="b1e29-126">On the **Programming Language** step, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Captura de pantalla que muestra cómo seleccionar el lenguaje de programación.":::

1. <span data-ttu-id="b1e29-128">Seleccione una carpeta de área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b1e29-128">Select a workspace folder.</span></span>  <span data-ttu-id="b1e29-129">Se creará una carpeta dentro de la carpeta del área de trabajo para el proyecto que esté creando.</span><span class="sxs-lookup"><span data-stu-id="b1e29-129">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="b1e29-130">Escriba un nombre adecuado para la aplicación, como `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="b1e29-130">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="b1e29-131">El nombre de la aplicación solo puede contener caracteres alfanuméricos.</span><span class="sxs-lookup"><span data-stu-id="b1e29-131">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="b1e29-132">Presione **Entrar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="b1e29-132">Press **Enter** to continue.</span></span>

<span data-ttu-id="b1e29-133">La aplicación Teams se creará en unos segundos.</span><span class="sxs-lookup"><span data-stu-id="b1e29-133">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="b1e29-134">Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="b1e29-134">Command line</span></span>](#tab/cli)

<span data-ttu-id="b1e29-135">Use la CLI de `teamsfx` para crear su primer proyecto:</span><span class="sxs-lookup"><span data-stu-id="b1e29-135">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="b1e29-136">Comience en la carpeta en la que quiera crear la carpeta del proyecto.</span><span class="sxs-lookup"><span data-stu-id="b1e29-136">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="b1e29-137">La CLI le guiará por varias preguntas para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="b1e29-137">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="b1e29-138">En cada pregunta se le indicará cómo responder (por ejemplo, usando las teclas de dirección para seleccionar una opción).</span><span class="sxs-lookup"><span data-stu-id="b1e29-138">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="b1e29-139">Cuando haya respondido a la pregunta, presione **Entrar** para confirmar la elección.</span><span class="sxs-lookup"><span data-stu-id="b1e29-139">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="b1e29-140">Seleccione **Crear una nueva aplicación de Teams**.</span><span class="sxs-lookup"><span data-stu-id="b1e29-140">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="b1e29-141">Seleccione la funcionalidad **Extensión de mensajería** y anule la selección de la funcionalidad **Pestaña**.</span><span class="sxs-lookup"><span data-stu-id="b1e29-141">Select the **Message Extension** capability and deselect the **Tab** capability.</span></span>
1. <span data-ttu-id="b1e29-142">Seleccione **Crear un nuevo registro de bot**.</span><span class="sxs-lookup"><span data-stu-id="b1e29-142">Select **Create a new bot registration**.</span></span>
1. <span data-ttu-id="b1e29-143">Seleccione **JavaScript** como lenguaje de programación.</span><span class="sxs-lookup"><span data-stu-id="b1e29-143">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="b1e29-144">Presione **Entrar** para seleccionar la carpeta de área de trabajo predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b1e29-144">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="b1e29-145">Escriba un nombre adecuado para la aplicación, como `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="b1e29-145">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="b1e29-146">El nombre de la aplicación solo puede contener caracteres alfanuméricos.</span><span class="sxs-lookup"><span data-stu-id="b1e29-146">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="b1e29-147">Una vez que haya respondido a todas las preguntas, se creará el proyecto.</span><span class="sxs-lookup"><span data-stu-id="b1e29-147">Once all the questions have been answered, your project will be created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="b1e29-148">Dar un paseo por el código fuente</span><span class="sxs-lookup"><span data-stu-id="b1e29-148">Take a tour of the source code</span></span>

<span data-ttu-id="b1e29-149">Si quiere omitir esta sección por ahora, puede [ejecutar la aplicación de forma local](#run-your-app-locally).</span><span class="sxs-lookup"><span data-stu-id="b1e29-149">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="b1e29-150">Una extensión de mensajería usa [Bot Framework](https://docs.botframework.com) para permitir al usuario interactuar con el servicio a través de una conversación.</span><span class="sxs-lookup"><span data-stu-id="b1e29-150">A messaging extension uses the [Bot Framework](https://docs.botframework.com) to allow the user to interact with your service via a conversation.</span></span>  <span data-ttu-id="b1e29-151">Después del scaffolding, el proyecto tendrá el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="b1e29-151">After scaffolding, your project will look like this:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-file-layout.png" alt-text="Distribución de archivos de un proyecto de bot.":::

<span data-ttu-id="b1e29-153">El código bot se almacena en el directorio `bot`.</span><span class="sxs-lookup"><span data-stu-id="b1e29-153">The bot code is stored in the `bot` directory.</span></span>  <span data-ttu-id="b1e29-154">`bot/messageExtensionBot.js` es el punto de entrada principal de la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="b1e29-154">The `bot/messageExtensionBot.js` is the main entry point for the messaging extension.</span></span>

> [!Tip]
> <span data-ttu-id="b1e29-155">Familiarícese con los bots fuera de Teams antes de integrar su primer bot en Teams.</span><span class="sxs-lookup"><span data-stu-id="b1e29-155">Familiarize yourself with bots outside of Teams before you integrate your first bot within Teams.</span></span>  <span data-ttu-id="b1e29-156">Para encontrar más información sobre los bots, vea los tutoriales de [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="b1e29-156">You can find more information about bots by reviewing the [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) tutorials.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="b1e29-157">Ejecutar la aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="b1e29-157">Run your app locally</span></span>

<span data-ttu-id="b1e29-158">El Kit de herramientas de Teams le permite hospedar la aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="b1e29-158">Teams Toolkit allows you to host your app locally.</span></span>  <span data-ttu-id="b1e29-159">Para ello:</span><span class="sxs-lookup"><span data-stu-id="b1e29-159">To do this:</span></span>

- <span data-ttu-id="b1e29-160">Se registra una aplicación de Azure Active Directory en el inquilino de M365.</span><span class="sxs-lookup"><span data-stu-id="b1e29-160">An Azure Active Directory Application is registered within the M365 tenant.</span></span>
- <span data-ttu-id="b1e29-161">Se envía un manifiesto de la aplicación al Portal para desarrolladores de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="b1e29-161">An app manifest is submitted to the Developer Portal for Teams.</span></span>
- <span data-ttu-id="b1e29-162">Se ejecuta localmente una API mediante Azure Functions Core Tools para admitir la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b1e29-162">An API is run locally using Azure Functions Core Tools to support your app.</span></span>
- <span data-ttu-id="b1e29-163">Se instala [ngrok](https://ngrok.io) y se usa para proporcionar un túnel entre Teams y la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="b1e29-163">[ngrok](https://ngrok.io) is installed and used to provide a tunnel between Teams and your messaging extension.</span></span>

<span data-ttu-id="b1e29-164">Para crear y ejecutar la aplicación localmente:</span><span class="sxs-lookup"><span data-stu-id="b1e29-164">To build and run your app locally:</span></span>

1. <span data-ttu-id="b1e29-165">Desde Visual Studio Code, presione **F5** para ejecutar la aplicación en modo de depuración.</span><span class="sxs-lookup"><span data-stu-id="b1e29-165">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="b1e29-166">Al ejecutar la aplicación por primera vez, se descargan todas las dependencias y se compila la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b1e29-166">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="b1e29-167">Cuando se complete la compilación, se abrirá automáticamente una ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="b1e29-167">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="b1e29-168">Este proceso puede tardar entre 3 o 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="b1e29-168">This can take 3-5 minutes to complete.</span></span>

1. <span data-ttu-id="b1e29-169">Se cargará Teams en un explorador web y se le pedirá que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="b1e29-169">Teams will be loaded in a web browser, and you will be prompted to sign in.</span></span> <span data-ttu-id="b1e29-170">Si se le pide que abra Microsoft Teams, seleccione Cancelar para permanecer en el explorador.</span><span class="sxs-lookup"><span data-stu-id="b1e29-170">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="b1e29-171">Inicie sesión con su cuenta de M365.</span><span class="sxs-lookup"><span data-stu-id="b1e29-171">Sign in with your M365 account.</span></span>

1. <span data-ttu-id="b1e29-172">Presione **Agregar** para agregar la aplicación a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="b1e29-172">Press **Add** to add the app to your account.</span></span>

<span data-ttu-id="b1e29-173">Una vez que se cargue la aplicación, se le redirigirá directamente a un diálogo de búsqueda:</span><span class="sxs-lookup"><span data-stu-id="b1e29-173">Once the app is loaded, you will be taken directly to a search dialog:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-completed-app.png" alt-text="Su extensión de mensajería basada en búsquedas en acción":::

<span data-ttu-id="b1e29-175">Escriba texto en el cuadro de búsqueda y, después, seleccione una de las opciones.</span><span class="sxs-lookup"><span data-stu-id="b1e29-175">Type some text in the search box, then select one of the options.</span></span>  <span data-ttu-id="b1e29-176">Se agregará una tarjeta adaptable al cuadro de entrada.</span><span class="sxs-lookup"><span data-stu-id="b1e29-176">An adaptive card will be added to your input box.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="b1e29-177">Vea lo que ocurre al ejecutar la aplicación localmente en el depurador.</span><span class="sxs-lookup"><span data-stu-id="b1e29-177">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="b1e29-178">Cuando presionó F5, el Kit de herramientas de Teams:</span><span class="sxs-lookup"><span data-stu-id="b1e29-178">When you pressed F5, the Teams Toolkit:</span></span>

1. <span data-ttu-id="b1e29-179">Registró la aplicación con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b1e29-179">Registered your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="b1e29-180">Registró la aplicación para la "instalación de prueba" en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="b1e29-180">Registered your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="b1e29-181">Inició el back-end de la aplicación ejecutándose de forma local con [Azure Functions Core Tools](/azure/azure-functions/functions-run-local?#start).</span><span class="sxs-lookup"><span data-stu-id="b1e29-181">Started your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="b1e29-182">Inició un túnel de ngrok para que Teams se comunique con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b1e29-182">Started an ngrok tunnel so Teams can communicate with your app.</span></span>
1. <span data-ttu-id="b1e29-183">Inició Microsoft Teams con un comando para indicar a Teams que haga la instalación de prueba de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b1e29-183">Started Microsoft Teams with a command to instruct Teams to sideload the application.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="b1e29-184">Vea cómo solucionar problemas comunes al ejecutar localmente la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b1e29-184">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="b1e29-185">Para ejecutar correctamente la aplicación en Teams, debe tener una cuenta de desarrollo de Microsoft 365 que permita la instalación de prueba de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b1e29-185">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="b1e29-186">Para obtener más información sobre cómo abrir la cuenta, consulte [Requisitos previos](prerequisites.md#enable-sideloading).</span><span class="sxs-lookup"><span data-stu-id="b1e29-186">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

> [!TIP]
> <span data-ttu-id="b1e29-187">Antes de hacer la instalación de prueba de la aplicación, compruebe si hay algún problema con la [herramienta de validación de aplicaciones](https://dev.teams.microsoft.com/appvalidation.html), que se incluye en el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="b1e29-187">Check for issues before sideloading your app, using the [app validation tool](https://dev.teams.microsoft.com/appvalidation.html), which is included in the toolkit.</span></span> <span data-ttu-id="b1e29-188">Corrija los errores para hacer correctamente la instalación de prueba.</span><span class="sxs-lookup"><span data-stu-id="b1e29-188">Fix the errors to successfully sideload the app.</span></span>
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary><span data-ttu-id="b1e29-189">Vea lo que ocurre al implementar la aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="b1e29-189">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="b1e29-190">Antes de la implementación, la aplicación se ejecuta de forma local:</span><span class="sxs-lookup"><span data-stu-id="b1e29-190">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="b1e29-191">El back-end se ejecuta con _Azure Functions Core Tools_.</span><span class="sxs-lookup"><span data-stu-id="b1e29-191">The backend runs using _Azure Functions Core Tools_.</span></span>
1. <span data-ttu-id="b1e29-192">El punto de conexión HTTP de la aplicación, donde Microsoft Teams carga la aplicación, se ejecuta de forma local.</span><span class="sxs-lookup"><span data-stu-id="b1e29-192">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="b1e29-193">La implementación implica recursos de aprovisionamiento en una suscripción activa de Azure y la implementación (carga) del back-end y del código de front-end de la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="b1e29-193">Deployment involves provisioning resources on an active Azure subscription and deploying (uploading) the backend and frontend code for the application to Azure.</span></span> <span data-ttu-id="b1e29-194">El back-end usa varios servicios de Azure, como Azure App Service y Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="b1e29-194">The backend uses a variety of Azure services, including Azure App Service and Azure Bot Service.</span></span>

</details>

## <a name="add-a-configuration-page-to-your-messaging-extension"></a><span data-ttu-id="b1e29-195">Agregar una página de configuración a la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="b1e29-195">Add a configuration page to your messaging extension</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="code-sample"></a><span data-ttu-id="b1e29-196">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="b1e29-196">Code sample</span></span>

<span data-ttu-id="b1e29-197">El Teams configuración de autenticación de búsqueda para proyectos de ejemplo en GitHub, muestra cómo crear extensiones de mensajería que incluyen una página de configuración y autenticación de [servicio de bot.](https://github.com/microsoft/BotBuilder-Samples#teams-samples)</span><span class="sxs-lookup"><span data-stu-id="b1e29-197">The Teams Search Auth Config for sample projects on GitHub, demonstrate how to create messaging extensions that include a configuration page and [Bot Service authentication](https://github.com/microsoft/BotBuilder-Samples#teams-samples).</span></span> <span data-ttu-id="b1e29-198">Los ejemplos también muestran cómo crear extensiones de mensaje que acepten solicitudes de búsqueda y devuelvan los resultados después de que el usuario haya iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="b1e29-198">The samples also demonstrate how to create message extensions that accept search requests and return the results after the user has signed in.</span></span>

| <span data-ttu-id="b1e29-199">**Nombre de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="b1e29-199">**Sample name**</span></span> | <span data-ttu-id="b1e29-200">**Description**</span><span class="sxs-lookup"><span data-stu-id="b1e29-200">**Description**</span></span> | <span data-ttu-id="b1e29-201">**.NET**</span><span class="sxs-lookup"><span data-stu-id="b1e29-201">**.NET**</span></span> | <span data-ttu-id="b1e29-202">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="b1e29-202">**Node.js**</span></span> | <span data-ttu-id="b1e29-203">**Python**</span><span class="sxs-lookup"><span data-stu-id="b1e29-203">**Python**</span></span> |
|-----------------|-----------------|-------------|--------------|--------|
| <span data-ttu-id="b1e29-204">Generador de bots</span><span class="sxs-lookup"><span data-stu-id="b1e29-204">Bot builder</span></span> | <span data-ttu-id="b1e29-205">Para crear extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="b1e29-205">To create messaging extensions.</span></span> | [<span data-ttu-id="b1e29-206">View</span><span class="sxs-lookup"><span data-stu-id="b1e29-206">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) | [<span data-ttu-id="b1e29-207">View</span><span class="sxs-lookup"><span data-stu-id="b1e29-207">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config) | [<span data-ttu-id="b1e29-208">View</span><span class="sxs-lookup"><span data-stu-id="b1e29-208">View</span></span>]( https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |

## <a name="additional-code-sample"></a><span data-ttu-id="b1e29-209">Ejemplo de código adicional</span><span class="sxs-lookup"><span data-stu-id="b1e29-209">Additional code sample</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b1e29-210">Ver más ejemplos de Bot Framework en GitHub</span><span class="sxs-lookup"><span data-stu-id="b1e29-210">View more Bot Framework Samples on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-samples#messaging-extensions-samples-using-the-v4-sdk)

## <a name="see-also"></a><span data-ttu-id="b1e29-211">Ver también</span><span class="sxs-lookup"><span data-stu-id="b1e29-211">See also</span></span>

- [<span data-ttu-id="b1e29-212">Crear una aplicación de Teams con React</span><span class="sxs-lookup"><span data-stu-id="b1e29-212">Create a Teams app with React</span></span>](first-app-react.md)
- [<span data-ttu-id="b1e29-213">Crear una aplicación de Teams con Blazor</span><span class="sxs-lookup"><span data-stu-id="b1e29-213">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
- <span data-ttu-id="b1e29-214">[Crear una aplicación de Teams como elemento web de SharePoint](first-app-spfx.md) (no se necesita Azure)</span><span class="sxs-lookup"><span data-stu-id="b1e29-214">[Create a Teams app as a SharePoint Web Part](first-app-spfx.md) (Azure not required)</span></span>
- [<span data-ttu-id="b1e29-215">Crear un bot de conversación</span><span class="sxs-lookup"><span data-stu-id="b1e29-215">Create a conversation bot</span></span>](first-app-bot.md)

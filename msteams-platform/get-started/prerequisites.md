---
title: 'Introducción: requisitos previos'
author: adrianhall
description: Obtén información sobre cómo empezar con el Microsoft Teams de aplicaciones y configurar el entorno.
ms.author: adhal
ms.date: 05/24/2021
ms.topic: quickstart
ms.openlocfilehash: 73d99f2bbbc69bf13242110a56e13e662655283c
ms.sourcegitcommit: 9cabeaed9baf96c8caeb1497f0bc37abdb787d22
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2021
ms.locfileid: "52646863"
---
# <a name="prerequisites-get-started-with-microsoft-teams-app-development"></a><span data-ttu-id="8df2d-103">Requisitos previos: Introducción al Microsoft Teams de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="8df2d-103">Prerequisites: Get started with Microsoft Teams app development</span></span>

<span data-ttu-id="8df2d-104">Antes de crear la primera Teams, debes instalar algunas herramientas y configurar el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="8df2d-104">Before your create your first Teams app, you must install a few tools and set up your development environment.</span></span>

## <a name="install-required-tools"></a><span data-ttu-id="8df2d-105">Instalar las herramientas necesarias</span><span class="sxs-lookup"><span data-stu-id="8df2d-105">Install required tools</span></span>

<span data-ttu-id="8df2d-106">Algunas de las herramientas que necesitas dependen de cómo prefieras crear tu Teams aplicación:</span><span class="sxs-lookup"><span data-stu-id="8df2d-106">Some of the tools you need depend on how you you prefer to build your Teams app:</span></span>

- <span data-ttu-id="8df2d-107">[Node.js](https://nodejs.org/en/download/) (use la versión más reciente de LTS de v14)</span><span class="sxs-lookup"><span data-stu-id="8df2d-107">[Node.js](https://nodejs.org/en/download/) (use the latest v14 LTS release)</span></span> 
- <span data-ttu-id="8df2d-108">Un explorador con herramientas de desarrollador, [como Microsoft Edge](https://www.microsoft.com/edge) (recomendado) o [Google Chrome](https://www.google.com/chrome/)</span><span class="sxs-lookup"><span data-stu-id="8df2d-108">A browser with developer tools - such as [Microsoft Edge](https://www.microsoft.com/edge) (recommended) or [Google Chrome](https://www.google.com/chrome/)</span></span>
- <span data-ttu-id="8df2d-109">Si está desarrollando con JavaScript, TypeScript o el SharePoint Framework (SPFx), instale [Visual Studio Code](https://code.visualstudio.com/download), versión 1.55 o posterior.</span><span class="sxs-lookup"><span data-stu-id="8df2d-109">If you're developing with JavaScript, TypeScript, or the SharePoint Framework (SPFx), install [Visual Studio Code](https://code.visualstudio.com/download), version 1.55 or later.</span></span>  
- <span data-ttu-id="8df2d-110">Si está desarrollando con .NET, instale Visual Studio [2019](https://visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="8df2d-110">If you're developing with .NET, install [Visual Studio 2019](https://visualstudio.com/download).</span></span>  <span data-ttu-id="8df2d-111">Asegúrese de instalar la carga ASP.NET **desarrollo web y web** o la carga de trabajo de desarrollo **multiplataforma de .NET Core.**</span><span class="sxs-lookup"><span data-stu-id="8df2d-111">Ensure you install the **ASP.NET and web development** or **.NET Core cross-platform development** workload.</span></span>

> [!WARNING]
> <span data-ttu-id="8df2d-112">Existen problemas conocidos con `npm@7` , empaquetados con node v15 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="8df2d-112">There are known issues with `npm@7`, packaged with Node v15 and later.</span></span> <span data-ttu-id="8df2d-113">Si tiene problemas para ejecutarse, asegúrese de que está `npm install` usando el nodo v14 (LTS)</span><span class="sxs-lookup"><span data-stu-id="8df2d-113">If you have problems running `npm install`, ensure you're using Node v14 (LTS)</span></span>

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="8df2d-114">Instale el Teams Toolkit</span><span class="sxs-lookup"><span data-stu-id="8df2d-114">Install the Teams Toolkit</span></span>

<span data-ttu-id="8df2d-115">El Teams Toolkit ayuda a simplificar el proceso de desarrollo con herramientas para aprovisionar e implementar recursos en la nube para tu aplicación, publicar en la Teams y mucho más.</span><span class="sxs-lookup"><span data-stu-id="8df2d-115">The Teams Toolkit helps simplify the development process with tools to provision and deploy cloud resources for your app, publish to the Teams store, and more.</span></span> <span data-ttu-id="8df2d-116">Puede usar el kit de herramientas con Visual Studio Code, Visual Studio o como una CLI (denominada `teamsfx` ).</span><span class="sxs-lookup"><span data-stu-id="8df2d-116">You can use the toolkit with Visual Studio Code, Visual Studio, or as a CLI (called `teamsfx`).</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="8df2d-117">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="8df2d-117">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="8df2d-118">Abrir Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8df2d-118">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="8df2d-119">Seleccione la vista Extensiones (**Ctrl+Mayús+X**  /  **,⇧-X** o **Ver > extensiones**).</span><span class="sxs-lookup"><span data-stu-id="8df2d-119">Select the Extensions view (**Ctrl+Shift+X** / **⌘⇧-X** or **View > Extensions**).</span></span>
1. <span data-ttu-id="8df2d-120">En el cuadro de búsqueda, _escriba Teams Toolkit_.</span><span class="sxs-lookup"><span data-stu-id="8df2d-120">In the search box, enter _Teams Toolkit_.</span></span>
1. <span data-ttu-id="8df2d-121">Seleccione el botón de instalación verde junto a la Teams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="8df2d-121">Select on the green install button next to the Teams Toolkit.</span></span>

<span data-ttu-id="8df2d-122">También puede encontrar el Teams Toolkit en el Visual Studio Code [Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).</span><span class="sxs-lookup"><span data-stu-id="8df2d-122">You also can find the Teams Toolkit on the [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).</span></span>

<span data-ttu-id="8df2d-123">La extensión de Visual Studio Code instalará las siguientes herramientas cuando sean necesarias.</span><span class="sxs-lookup"><span data-stu-id="8df2d-123">The following tools will be installed by the Visual Studio Code extension when they are needed.</span></span>  <span data-ttu-id="8df2d-124">Si ya está instalada, la versión instalada se usará en su lugar.</span><span class="sxs-lookup"><span data-stu-id="8df2d-124">If already installed, the installed version will be used instead.</span></span>  <span data-ttu-id="8df2d-125">Si usa Linux (incluido WSL), debe instalar estas herramientas antes de usar:</span><span class="sxs-lookup"><span data-stu-id="8df2d-125">If using Linux (including WSL), you must install these tools before use:</span></span>

- [<span data-ttu-id="8df2d-126">Azure Functions Core Tools</span><span class="sxs-lookup"><span data-stu-id="8df2d-126">Azure Functions Core Tools</span></span>](/azure/azure-functions/functions-run-local)

    <span data-ttu-id="8df2d-127">Azure Functions Core Tools se usa para ejecutar los componentes back-end localmente durante una ejecución de depuración local, incluidas las aplicaciones auxiliares de autenticación necesarias para ejecutar los servicios en Azure.</span><span class="sxs-lookup"><span data-stu-id="8df2d-127">Azure Functions Core Tools is used to run any backend components locally during a local debug run, including the authentication helpers required when running your services in Azure.</span></span>  <span data-ttu-id="8df2d-128">Se instala en el directorio del proyecto (mediante el npm `devDependencies` ).</span><span class="sxs-lookup"><span data-stu-id="8df2d-128">It is installed within the project directory (using the npm `devDependencies`).</span></span>

- [<span data-ttu-id="8df2d-129">SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="8df2d-129">.NET SDK</span></span>](/dotnet/core/install/)

    <span data-ttu-id="8df2d-130">El SDK de .NET se usa para instalar enlaces personalizados para la depuración local y las implementaciones de aplicaciones de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="8df2d-130">The .NET SDK is used to install customized bindings for local debugging and Azure Functions app deployments.</span></span>  <span data-ttu-id="8df2d-131">Si no ha instalado el SDK de .NET 3.1 (o posterior) globalmente, se instalará la versión portátil.</span><span class="sxs-lookup"><span data-stu-id="8df2d-131">If you have not installed the .NET 3.1 (or later) SDK globally, the portable version will be installed.</span></span>

- [<span data-ttu-id="8df2d-132">ngrok</span><span class="sxs-lookup"><span data-stu-id="8df2d-132">ngrok</span></span>](https://ngrok.com/download)

    <span data-ttu-id="8df2d-133">Algunas Teams de la aplicación (bots de conversación, extensiones de mensajería y webhooks entrantes) requieren conexiones entrantes.</span><span class="sxs-lookup"><span data-stu-id="8df2d-133">Some Teams app features (conversational bots, messaging extensions, and incoming webhooks) require inbound connections.</span></span>  <span data-ttu-id="8df2d-134">Debe exponer el sistema de desarrollo para Teams a través de un túnel.</span><span class="sxs-lookup"><span data-stu-id="8df2d-134">You need to expose your development system to Teams through a tunnel.</span></span>  <span data-ttu-id="8df2d-135">No es necesario un túnel para las aplicaciones que solo incluyen pestañas.</span><span class="sxs-lookup"><span data-stu-id="8df2d-135">A tunnel is not required for apps that only include tabs.</span></span>  <span data-ttu-id="8df2d-136">Este paquete se instala en el directorio del proyecto (mediante npm `devDependencies` ).</span><span class="sxs-lookup"><span data-stu-id="8df2d-136">This package is installed within the project directory (using npm `devDependencies`).</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="8df2d-137">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="8df2d-137">Visual Studio 2019</span></span>](#tab/vs)

<span data-ttu-id="8df2d-138">Puedes usar Visual Studio 2019 para desarrollar aplicaciones Teams con Blazor Server en .NET.</span><span class="sxs-lookup"><span data-stu-id="8df2d-138">You can use Visual Studio 2019 to develop Teams apps with Blazor Server in .NET.</span></span>  <span data-ttu-id="8df2d-139">Si no tienes la intención de desarrollar aplicaciones Teams en .NET, instala la Visual Studio Code de Teams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="8df2d-139">If you're not intending to develop Teams apps in .NET, install the Visual Studio Code version of Teams Toolkit.</span></span>

<span data-ttu-id="8df2d-140">Para instalar la Teams Toolkit extensión:</span><span class="sxs-lookup"><span data-stu-id="8df2d-140">To install the Teams Toolkit extension:</span></span>

1. <span data-ttu-id="8df2d-141">Abra Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="8df2d-141">Open Visual Studio 2019.</span></span>
1. <span data-ttu-id="8df2d-142">Seleccione **Extensiones Administrar**  >  **extensiones**.</span><span class="sxs-lookup"><span data-stu-id="8df2d-142">Select **Extensions** > **Manage Extensions**.</span></span>
1. <span data-ttu-id="8df2d-143">En el cuadro de búsqueda, _escriba Teams Toolkit_.</span><span class="sxs-lookup"><span data-stu-id="8df2d-143">In the search box, enter _Teams Toolkit_.</span></span>
1. <span data-ttu-id="8df2d-144">Seleccione la Teams Toolkit y seleccione **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="8df2d-144">Select the Teams Toolkit extension and select **Download**.</span></span>

<span data-ttu-id="8df2d-145">La extensión se descargará.</span><span class="sxs-lookup"><span data-stu-id="8df2d-145">The extension will be downloaded.</span></span>  <span data-ttu-id="8df2d-146">Cierre Visual Studio 2019 para instalar la extensión.</span><span class="sxs-lookup"><span data-stu-id="8df2d-146">Close Visual Studio 2019 to install the extension.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="8df2d-147">Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="8df2d-147">Command line</span></span>](#tab/cli)

<span data-ttu-id="8df2d-148">Para instalar la CLI de TeamsFx, use el administrador `npm` de paquetes:</span><span class="sxs-lookup"><span data-stu-id="8df2d-148">To install the TeamsFx CLI, use the `npm` package manager:</span></span>

``` bash
npm install -g @microsoft/teamsfx-cli
```

<span data-ttu-id="8df2d-149">Según la configuración, es posible que deba usar `sudo` para instalar la CLI:</span><span class="sxs-lookup"><span data-stu-id="8df2d-149">Depending on your configuration, you may need to use `sudo` to install the CLI:</span></span>

``` bash
sudo npm install -g --unsafe-perm @microsoft/teamsfx-cli
```

<span data-ttu-id="8df2d-150">Esto es más común en sistemas Linux y macOS.</span><span class="sxs-lookup"><span data-stu-id="8df2d-150">This is more common on Linux and macOS systems.</span></span>

<span data-ttu-id="8df2d-151">Asegúrese de agregar la caché global de npm a la ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="8df2d-151">Ensure you add the npm global cache to your PATH.</span></span>  <span data-ttu-id="8df2d-152">Normalmente, esto se realiza como parte del instalador Node.js instalación.</span><span class="sxs-lookup"><span data-stu-id="8df2d-152">This is normally done as part of the Node.js installer.</span></span>  

<span data-ttu-id="8df2d-153">Puede usar la CLI con el `teamsfx` comando.</span><span class="sxs-lookup"><span data-stu-id="8df2d-153">You can use the CLI with the `teamsfx` command.</span></span>  <span data-ttu-id="8df2d-154">Compruebe que el comando funciona ejecutando `teamsfx -h` .</span><span class="sxs-lookup"><span data-stu-id="8df2d-154">Verify that the command is working by running `teamsfx -h`.</span></span>

> [!CAUTION]
> <span data-ttu-id="8df2d-155">Para poder ejecutar TeamsFx en terminales de PowerShell, debe habilitar la directiva de ejecución "firmada remotamente" para PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8df2d-155">Before you can run TeamsFx in PowerShell terminals, you need to enable the "remote signed" execution policy for PowerShell.</span></span>  <span data-ttu-id="8df2d-156">Para obtener más información, consulte la [documentación de PowerShell](/powershell/module/microsoft.powershell.core/about/about_signing).</span><span class="sxs-lookup"><span data-stu-id="8df2d-156">For more information, refer to the [PowerShell documentation](/powershell/module/microsoft.powershell.core/about/about_signing).</span></span>

---

## <a name="install-optional-tools"></a><span data-ttu-id="8df2d-157">Instalar herramientas opcionales</span><span class="sxs-lookup"><span data-stu-id="8df2d-157">Install optional tools</span></span>

<span data-ttu-id="8df2d-158">Instalar herramientas de explorador para el desarrollo de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="8df2d-158">Install browser tools for app development.</span></span> <span data-ttu-id="8df2d-159">Por ejemplo, si la aplicación está escrita con React, puedes usar React Developer Tools:</span><span class="sxs-lookup"><span data-stu-id="8df2d-159">For instance, if your app is written with React, you can use React Developer Tools:</span></span>

- [<span data-ttu-id="8df2d-160">React Herramientas para desarrolladores para Chrome</span><span class="sxs-lookup"><span data-stu-id="8df2d-160">React Developer Tools for Chrome</span></span>](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

<span data-ttu-id="8df2d-161">Si desea obtener acceso a los datos almacenados en Azure o implementar un back-end basado en la nube para su aplicación Teams en Azure, instale estas herramientas:</span><span class="sxs-lookup"><span data-stu-id="8df2d-161">If you want to access data stored in Azure or deploy a cloud-based backend for your Teams app in Azure, install these tools:</span></span>

- [<span data-ttu-id="8df2d-162">Herramientas de Azure para Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="8df2d-162">Azure Tools for Visual Studio Code</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack)
- [<span data-ttu-id="8df2d-163">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8df2d-163">Azure CLI</span></span>](/cli/azure/install-azure-cli)

<span data-ttu-id="8df2d-164">Si trabaja con datos de microsoft Graph, debe obtener información y marcar el Explorador de Graph Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8df2d-164">If you work with Microsoft Graph data, you should learn about and bookmark the Microsoft Graph Explorer.</span></span> <span data-ttu-id="8df2d-165">Esta herramienta basada en explorador te permite consultar Microsoft Graph fuera de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="8df2d-165">This browser-based tool allows you to query Microsoft Graph outside of an app.</span></span>

- [<span data-ttu-id="8df2d-166">Explorador de Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="8df2d-166">Microsoft Graph Explorer</span></span>](https://developer.microsoft.com/graph/graph-explorer)

<span data-ttu-id="8df2d-167">Con el Portal de desarrolladores para Teams, puedes configurar, administrar y distribuir la aplicación Teams (incluida la organización o la Teams store).</span><span class="sxs-lookup"><span data-stu-id="8df2d-167">With the Developer Portal for Teams, you can configure, manage, and distribute your Teams app (including to your org or the Teams store).</span></span>

- [<span data-ttu-id="8df2d-168">Portal para desarrolladores de Teams</span><span class="sxs-lookup"><span data-stu-id="8df2d-168">Developer Portal for Teams</span></span>](https://dev.teams.microsoft.com/)

## <a name="enable-sideloading"></a><span data-ttu-id="8df2d-169">Habilitar la instalación local</span><span class="sxs-lookup"><span data-stu-id="8df2d-169">Enable sideloading</span></span>

<span data-ttu-id="8df2d-170">Durante el desarrollo, deberás cargar la aplicación Teams sin distribuirla.</span><span class="sxs-lookup"><span data-stu-id="8df2d-170">During development, you will need to load your app within Teams without distributing it.</span></span>  <span data-ttu-id="8df2d-171">Esto se conoce como "sideloading".</span><span class="sxs-lookup"><span data-stu-id="8df2d-171">This is known as "sideloading".</span></span>

1. <span data-ttu-id="8df2d-172">Si tienes una cuenta Teams, comprueba si puedes realizar la instalación local de aplicaciones en Teams:</span><span class="sxs-lookup"><span data-stu-id="8df2d-172">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>

    1. <span data-ttu-id="8df2d-173">En el Teams, seleccione **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8df2d-173">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="8df2d-174">Busque una opción para **Upload una aplicación personalizada**.</span><span class="sxs-lookup"><span data-stu-id="8df2d-174">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="~/assets/images/teams-toolkit-v2/upload-custom-app-closeup.png" alt-text="Ilustración que muestra dónde Teams puedes cargar una aplicación personalizada.":::

> [!NOTE]
> <span data-ttu-id="8df2d-176">Si aún no puedes realizar la instalación local de aplicaciones, habla con el Teams administrador.</span><span class="sxs-lookup"><span data-stu-id="8df2d-176">If you still can't sideload apps, talk to your Teams administrator.</span></span> <span data-ttu-id="8df2d-177">Consulta [Habilitar aplicaciones Teams personalizadas y activar la](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) carga de aplicaciones personalizadas para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="8df2d-177">See [enable custom Teams apps and turn on custom app uploading](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) for details.</span></span>

## <a name="get-a-free-teams-developer-tenant-optional"></a><span data-ttu-id="8df2d-178">Obtener un espacio empresarial Teams desarrollador (opcional)</span><span class="sxs-lookup"><span data-stu-id="8df2d-178">Get a free Teams developer tenant (optional)</span></span>

<span data-ttu-id="8df2d-179">Si no puede ver la opción de instalación local o no tiene una cuenta de Teams, puede obtener una cuenta de desarrollador Teams gratuita uniéndose al programa de desarrolladores M365.</span><span class="sxs-lookup"><span data-stu-id="8df2d-179">If you cannot see the sideload option, or you don't have a Teams account, you can get a free Teams developer account by joining the M365 developer program.</span></span>  <span data-ttu-id="8df2d-180">El proceso de registro tarda aproximadamente dos minutos.</span><span class="sxs-lookup"><span data-stu-id="8df2d-180">The registration process takes approximately two minutes.</span></span>

1. <span data-ttu-id="8df2d-181">Vaya al programa [Microsoft 365 desarrollador](https://developer.microsoft.com/microsoft-365/dev-program).</span><span class="sxs-lookup"><span data-stu-id="8df2d-181">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="8df2d-182">Selecciona **Unirse ahora** y sigue las instrucciones en pantalla.</span><span class="sxs-lookup"><span data-stu-id="8df2d-182">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="8df2d-183">Cuando llegue a la pantalla de bienvenida, seleccione **Configurar la suscripción de E5**.</span><span class="sxs-lookup"><span data-stu-id="8df2d-183">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="8df2d-184">Configurar la cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="8df2d-184">Set up your administrator account.</span></span> <span data-ttu-id="8df2d-185">Una vez que termines, deberías ver una pantalla como esta.</span><span class="sxs-lookup"><span data-stu-id="8df2d-185">Once you finish, you should see a screen like this.</span></span>

    :::image type="content" source="~/assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Ejemplo de lo que ve después de registrarse en el programa Microsoft 365 desarrollador.":::

1. <span data-ttu-id="8df2d-187">Inicie sesión en Teams la cuenta de administrador que acaba de configurar.</span><span class="sxs-lookup"><span data-stu-id="8df2d-187">Log in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="8df2d-188">Comprueba si ahora tienes la Upload **una opción de aplicación** personalizada.</span><span class="sxs-lookup"><span data-stu-id="8df2d-188">Verify if you now have the **Upload a custom app** option.</span></span>

## <a name="get-a-free-azure-account"></a><span data-ttu-id="8df2d-189">Obtener una cuenta gratuita de Azure</span><span class="sxs-lookup"><span data-stu-id="8df2d-189">Get a free Azure account</span></span>

<span data-ttu-id="8df2d-190">Si quieres hospedar la aplicación o acceder a recursos dentro de Azure, necesitarás una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="8df2d-190">If you wish to host your app or access resources within Azure, you will need an Azure subscription.</span></span>  <span data-ttu-id="8df2d-191">Puede crear [una cuenta gratuita antes](https://azure.microsoft.com/free/) de comenzar.</span><span class="sxs-lookup"><span data-stu-id="8df2d-191">You can [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="sign-in-to-your-microsoft-365-and-azure-accounts"></a><span data-ttu-id="8df2d-192">Iniciar sesión en las cuentas Microsoft 365 y Azure</span><span class="sxs-lookup"><span data-stu-id="8df2d-192">Sign in to your Microsoft 365 and Azure accounts</span></span>

<span data-ttu-id="8df2d-193">Necesitarás acceso a dos cuentas:</span><span class="sxs-lookup"><span data-stu-id="8df2d-193">You will need access to two accounts:</span></span>

- <span data-ttu-id="8df2d-194">Sus Microsoft 365 de cuenta.</span><span class="sxs-lookup"><span data-stu-id="8df2d-194">Your Microsoft 365 account credentials.</span></span> <span data-ttu-id="8df2d-195">Esta es la cuenta que usa para iniciar sesión en Teams.</span><span class="sxs-lookup"><span data-stu-id="8df2d-195">This is the account that you use to sign in to Teams.</span></span> <span data-ttu-id="8df2d-196">Si usa un inquilino del programa Microsoft 365 desarrollador, esta es la cuenta de administrador que estableció cuando se registró para el programa.</span><span class="sxs-lookup"><span data-stu-id="8df2d-196">If you're using an Microsoft 365 developer program tenant, this is the admin account you set up when you registered for the program.</span></span>
- - <span data-ttu-id="8df2d-197">Sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="8df2d-197">Your Azure credentials.</span></span> <span data-ttu-id="8df2d-198">Esta es la cuenta que usa para obtener acceso a Azure Portal y para aprovisionar nuevos recursos en la nube para admitir la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8df2d-198">This is the account that you use to access the Azure Portal and for provisioning new cloud resources to support your app.</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="8df2d-199">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="8df2d-199">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="8df2d-200">Abra Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="8df2d-200">Open Visual Studio Code</span></span>
1. <span data-ttu-id="8df2d-201">Selecciona el Teams en la barra lateral:</span><span class="sxs-lookup"><span data-stu-id="8df2d-201">Select the Teams icon in the sidebar:</span></span>

    :::image type="content" source="~/assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icono de Teams en la barra lateral de Visual Studio Code.":::

1. <span data-ttu-id="8df2d-203">Seleccione **Iniciar sesión en M365**.</span><span class="sxs-lookup"><span data-stu-id="8df2d-203">Select **Sign in to M365**.</span></span>

    :::image type="content" source="~/assets/images/teams-toolkit-v2/account-commands.png" alt-text="Ubicación de la sección Cuentas usada para iniciar sesión.":::

1. <span data-ttu-id="8df2d-205">El proceso de inicio de sesión empezará a usar el explorador web normal.</span><span class="sxs-lookup"><span data-stu-id="8df2d-205">The sign-in process will start using your normal web browser.</span></span>  <span data-ttu-id="8df2d-206">Complete el proceso de inicio de sesión de su cuenta M365.</span><span class="sxs-lookup"><span data-stu-id="8df2d-206">Complete the sign-in process for your M365 account.</span></span>  <span data-ttu-id="8df2d-207">Se le pedirá cuándo puede cerrar el explorador y volver a Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8df2d-207">You will be prompted when you can close the browser and return to Visual Studio Code.</span></span>
1. <span data-ttu-id="8df2d-208">Vuelva al Teams Toolkit dentro de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8df2d-208">Return to the Teams Toolkit within Visual Studio Code.</span></span>
1. <span data-ttu-id="8df2d-209">Seleccione **Iniciar sesión en Azure**.</span><span class="sxs-lookup"><span data-stu-id="8df2d-209">Select **Sign in to Azure**.</span></span>

    > [!TIP]
    > <span data-ttu-id="8df2d-210">Si tiene instalada la extensión cuenta de Azure y usa la misma cuenta, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="8df2d-210">If you have the Azure Account extension installed and are using the same account, you can skip this step.</span></span>  <span data-ttu-id="8df2d-211">Usarás automáticamente la misma cuenta que usas en otras extensiones.</span><span class="sxs-lookup"><span data-stu-id="8df2d-211">You will automatically use the same account as you are using in other extensions.</span></span>

1. <span data-ttu-id="8df2d-212">El proceso de inicio de sesión empezará a usar el explorador web normal.</span><span class="sxs-lookup"><span data-stu-id="8df2d-212">The sign-in process will start using your normal web browser.</span></span>  <span data-ttu-id="8df2d-213">Complete el proceso de inicio de sesión de su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="8df2d-213">Complete the sign-in process for your Azure account.</span></span>  <span data-ttu-id="8df2d-214">Se le pedirá cuándo puede cerrar el explorador y volver a Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8df2d-214">You will be prompted when you can close the browser and return to Visual Studio Code.</span></span>

<span data-ttu-id="8df2d-215">Cuando se complete, la **sección CUENTAS** de la barra lateral mostrará las dos cuentas por separado, junto con el número de suscripciones de Azure utilizables disponibles.</span><span class="sxs-lookup"><span data-stu-id="8df2d-215">When complete, the **ACCOUNTS** section of the sidebar will show the two accounts separately, together with the number of usable Azure subscriptions available to you.</span></span>  <span data-ttu-id="8df2d-216">Asegúrese de que tiene al menos una suscripción de Azure utilizable disponible.</span><span class="sxs-lookup"><span data-stu-id="8df2d-216">Ensure you have at least one usable Azure subscription available.</span></span>  <span data-ttu-id="8df2d-217">Si no es así, cerrar sesión y usar una cuenta diferente.</span><span class="sxs-lookup"><span data-stu-id="8df2d-217">If not, sign out and use a different account.</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="8df2d-218">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="8df2d-218">Visual Studio 2019</span></span>](#tab/vs)

<span data-ttu-id="8df2d-219">Visual Studio 2019 le pedirá que inicie sesión en cada servicio según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="8df2d-219">Visual Studio 2019 will prompt you to log in to each service as it is needed.</span></span>  <span data-ttu-id="8df2d-220">No es necesario que inicie sesión en sus cuentas de M365 y Azure por adelantado.</span><span class="sxs-lookup"><span data-stu-id="8df2d-220">You do not need to sign in to your M365 and Azure accounts in advance.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="8df2d-221">Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="8df2d-221">Command line</span></span>](#tab/cli)

1. <span data-ttu-id="8df2d-222">Inicie sesión en Microsoft 365 con la CLI de TeamsFx:</span><span class="sxs-lookup"><span data-stu-id="8df2d-222">Sign in to Microsoft 365 with the TeamsFx CLI:</span></span>

    ``` bash
    teamsfx account login m365
    ```

    <span data-ttu-id="8df2d-223">El proceso de inicio de sesión empezará a usar el explorador web normal.</span><span class="sxs-lookup"><span data-stu-id="8df2d-223">The sign-in process will start using your normal web browser.</span></span>  <span data-ttu-id="8df2d-224">Complete el proceso de inicio de sesión de su cuenta M365.</span><span class="sxs-lookup"><span data-stu-id="8df2d-224">Complete the sign-in process for your M365 account.</span></span>  <span data-ttu-id="8df2d-225">Se le pedirá cuándo puede cerrar el explorador.</span><span class="sxs-lookup"><span data-stu-id="8df2d-225">You will be prompted when you can close the browser.</span></span>

2. <span data-ttu-id="8df2d-226">Inicie sesión en Azure con la CLI de TeamsFx:</span><span class="sxs-lookup"><span data-stu-id="8df2d-226">Sign in to Azure with the TeamsFx CLI:</span></span>

    ``` bash
    teamsfx account login azure
    ```

    <span data-ttu-id="8df2d-227">El proceso de inicio de sesión empezará a usar el explorador web normal.</span><span class="sxs-lookup"><span data-stu-id="8df2d-227">The sign-in process will start using your normal web browser.</span></span>  <span data-ttu-id="8df2d-228">Complete el proceso de inicio de sesión de su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="8df2d-228">Complete the sign-in process for your Azure account.</span></span>  <span data-ttu-id="8df2d-229">Se le pedirá cuándo puede cerrar el explorador.</span><span class="sxs-lookup"><span data-stu-id="8df2d-229">You will be prompted when you can close the browser.</span></span>

<span data-ttu-id="8df2d-230">Los inicios de sesión de la cuenta se comparten Visual Studio Code la CLI de TeamsFx.</span><span class="sxs-lookup"><span data-stu-id="8df2d-230">The account logins are shared between Visual Studio Code and the TeamsFx CLI.</span></span>

---

## <a name="next-steps"></a><span data-ttu-id="8df2d-231">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8df2d-231">Next steps</span></span>

<span data-ttu-id="8df2d-232">Ahora que el entorno de desarrollo está configurado, puedes crear, crear e implementar la primera aplicación Teams desarrollo.</span><span class="sxs-lookup"><span data-stu-id="8df2d-232">Now that your development environment is configured, you can create, build, and deploy your first Teams app.</span></span>

- [<span data-ttu-id="8df2d-233">Crea la primera aplicación Teams con React</span><span class="sxs-lookup"><span data-stu-id="8df2d-233">Create your first Teams app using React</span></span>](first-app-react.md)
- [<span data-ttu-id="8df2d-234">Crear la primera aplicación Teams con Blazor</span><span class="sxs-lookup"><span data-stu-id="8df2d-234">Create your first Teams app with Blazor</span></span>](first-app-blazor.md)
- [<span data-ttu-id="8df2d-235">Crear la primera aplicación Teams con SharePoint Framework (SPFx)</span><span class="sxs-lookup"><span data-stu-id="8df2d-235">Create your first Teams app using SharePoint Framework (SPFx)</span></span>](first-app-spfx.md)
- [<span data-ttu-id="8df2d-236">Crear una aplicación de bots de conversación</span><span class="sxs-lookup"><span data-stu-id="8df2d-236">Create a conversational bot app</span></span>](first-app-bot.md)
- [<span data-ttu-id="8df2d-237">Crear una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="8df2d-237">Create a messaging extension</span></span>](first-message-extension.md)

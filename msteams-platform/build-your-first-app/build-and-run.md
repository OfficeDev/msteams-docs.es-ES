---
title: 'Introducción: compilar y ejecutar la primera aplicación'
author: heath-hamilton
description: Cree rápidamente una aplicación de Microsoft Teams que muestre un mensaje de "Hola a todos". con Microsoft Teams Toolkit.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 46a92f54cdbf68e28510c0bd4cc0b7018cfaae3c
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093953"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="77ab1-104">Crear y ejecutar la primera aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="77ab1-104">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="77ab1-105">Inicie el desarrollo de Microsoft Teams creando una pestaña personal que muestre "Hello, World!".</span><span class="sxs-lookup"><span data-stu-id="77ab1-105">Start Microsoft Teams development by building a personal tab that displays "Hello, World!".</span></span>
<span data-ttu-id="77ab1-106">Cree y ejecute su primera aplicación de Teams siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="77ab1-106">Build and run your first Teams app using the following steps:</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="77ab1-107">1. Crear el proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="77ab1-107">1. Create your app project</span></span>

<span data-ttu-id="77ab1-108">Use Microsoft Teams Toolkit en Visual Studio code para configurar su primer proyecto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="77ab1-108">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span> <span data-ttu-id="77ab1-109">Cree el proyecto de aplicación siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="77ab1-109">Create your app project using the following steps:</span></span>

1. In Visual Studio Code, select **Microsoft Teams** on the left Activity Bar and choose Create a new Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **app**.
1. <span data-ttu-id="77ab1-111">Cuando se le solicite, inicie sesión con su cuenta de desarrollo de Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="77ab1-111">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="77ab1-112">En la **pantalla Agregar funcionalidades,** seleccione **Pestaña** y, a **continuación, Siguiente.**</span><span class="sxs-lookup"><span data-stu-id="77ab1-112">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Captura de pantalla que muestra cómo configurar el proyecto de aplicación con Visual Studio Kit de herramientas de Code Teams.":::
1. <span data-ttu-id="77ab1-114">Escriba un nombre para su aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="77ab1-114">Enter a name for your Teams app.</span></span> <span data-ttu-id="77ab1-115">(Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de aplicación en el equipo local).</span><span class="sxs-lookup"><span data-stu-id="77ab1-115">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="77ab1-116">Comprueba solo la **opción de pestaña Personal** y selecciona **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="77ab1-116">Check only the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="77ab1-117">2. Comprender los componentes importantes del proyecto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="77ab1-117">2. Understand important app project components</span></span>

<span data-ttu-id="77ab1-118">Una vez que el kit de herramientas configura el proyecto, tiene los componentes para crear una pestaña personal básica para Teams.</span><span class="sxs-lookup"><span data-stu-id="77ab1-118">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="77ab1-119">Los archivos y directorios del proyecto se muestran en el área Explorador de Visual Studio código.</span><span class="sxs-lookup"><span data-stu-id="77ab1-119">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Captura de pantalla que muestra los archivos de proyecto de la aplicación para una pestaña personal en Visual Studio código.":::

### <a name="app-scaffolding"></a><span data-ttu-id="77ab1-121">Scaffolding de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="77ab1-121">App scaffolding</span></span>

<span data-ttu-id="77ab1-122">El kit de herramientas crea automáticamente scaffolding para ti en el directorio en función de las `src` funcionalidades que agregaste durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="77ab1-122">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="77ab1-123">Si creas una pestaña durante la instalación, por ejemplo, el archivo del directorio es importante porque controla la inicialización y el `App.js` `src/components` enrutamiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="77ab1-123">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="77ab1-124">Llama al SDK del cliente [de JavaScript](../tabs/how-to/using-teams-client-sdk.md) de Microsoft Teams para establecer la comunicación entre la aplicación y Teams.</span><span class="sxs-lookup"><span data-stu-id="77ab1-124">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-id"></a><span data-ttu-id="77ab1-125">Identificador de la aplicación</span><span class="sxs-lookup"><span data-stu-id="77ab1-125">App ID</span></span>

<span data-ttu-id="77ab1-126">Configure su aplicación con App Studio con el id. de aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="77ab1-126">Configure your app with App Studio using the Teams app ID.</span></span> <span data-ttu-id="77ab1-127">Busque el identificador en el `teamsAppId` objeto, que se encuentra en el archivo del `package.json` proyecto.</span><span class="sxs-lookup"><span data-stu-id="77ab1-127">Find the ID in the `teamsAppId` object, which is located in your project's `package.json` file.</span></span>

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="77ab1-128">3. Compilar y ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="77ab1-128">3. Build and run your app</span></span>

<span data-ttu-id="77ab1-129">Compila y ejecuta la aplicación localmente para ahorrar tiempo.</span><span class="sxs-lookup"><span data-stu-id="77ab1-129">Build and run your app locally to save time.</span></span> <span data-ttu-id="77ab1-130">Esta información también está disponible en el kit de `README` herramientas.</span><span class="sxs-lookup"><span data-stu-id="77ab1-130">This information is also available in the toolkit `README`.</span></span> <span data-ttu-id="77ab1-131">Compila y ejecuta la aplicación mediante los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="77ab1-131">Build and run your app using the following steps:</span></span>

1. <span data-ttu-id="77ab1-132">En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .</span><span class="sxs-lookup"><span data-stu-id="77ab1-132">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="77ab1-133">Ejecute `npm start` .</span><span class="sxs-lookup"><span data-stu-id="77ab1-133">Run `npm start`.</span></span>

<span data-ttu-id="77ab1-134">Una vez completado, se compila **correctamente.**</span><span class="sxs-lookup"><span data-stu-id="77ab1-134">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="77ab1-135">en el terminal.</span><span class="sxs-lookup"><span data-stu-id="77ab1-135">message in the terminal.</span></span> <span data-ttu-id="77ab1-136">La aplicación se está ejecutando en `https://localhost:3000` .</span><span class="sxs-lookup"><span data-stu-id="77ab1-136">Your app is running on `https://localhost:3000`.</span></span>

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="77ab1-137">4. Instalación local de la aplicación en Teams</span><span class="sxs-lookup"><span data-stu-id="77ab1-137">4. Sideload your app in Teams</span></span>

<span data-ttu-id="77ab1-138">La aplicación está lista para probarse en Teams.</span><span class="sxs-lookup"><span data-stu-id="77ab1-138">Your app is ready to test in Teams.</span></span> <span data-ttu-id="77ab1-139">Para ello, debe tener una cuenta de desarrollo de Microsoft 365 que permita la instalación de prueba de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="77ab1-139">To do this, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="77ab1-140">Para obtener más información sobre la apertura de cuentas, consulte [Cuenta de desarrollo de Teams.](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)</span><span class="sxs-lookup"><span data-stu-id="77ab1-140">For more information on account opening, see [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).</span></span> 

> [!TIP]
> <span data-ttu-id="77ab1-141">Comprueba si hay problemas antes de realizar la instalación de prueba de la aplicación, mediante la característica de validación [de App Studio,](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)que se incluye en el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="77ab1-141">Check for issues before sideloading your app, using the [validation feature in App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), which is included in the toolkit.</span></span> <span data-ttu-id="77ab1-142">Se solucionan los errores para que la aplicación se trascargue correctamente.</span><span class="sxs-lookup"><span data-stu-id="77ab1-142">Fix the errors to successfully sideload the app.</span></span>

<span data-ttu-id="77ab1-143">Haga una instalación de instalación local de la aplicación en Teams siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="77ab1-143">Sideload your app in Teams using the following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="77ab1-144">Para habilitar la instalación de instalación de local antes de realizar la instalación de local de la aplicación en Teams, siga los pasos descritos en [Turn on app sideloading](../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading).</span><span class="sxs-lookup"><span data-stu-id="77ab1-144">To enable sideloading before you sideload your app in Teams, follow the steps in [Turn on app sideloading](../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading).</span></span>

1. <span data-ttu-id="77ab1-145">Seleccione la **tecla F5** para iniciar un cliente web de Teams en Visual Studio código.</span><span class="sxs-lookup"><span data-stu-id="77ab1-145">Select the **F5** key to launch a Teams web client in Visual Studio Code.</span></span>
1. <span data-ttu-id="77ab1-146">Para mostrar el contenido de la aplicación en Teams, especifique que el lugar donde se ejecuta la aplicación ( `localhost` ) es de confianza:</span><span class="sxs-lookup"><span data-stu-id="77ab1-146">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="77ab1-147">Abra una nueva pestaña en la misma ventana del explorador (Google Chrome de forma predeterminada) que se abrió después de presionar **F5**.</span><span class="sxs-lookup"><span data-stu-id="77ab1-147">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="77ab1-148">Vaya a `https://localhost:3000/tab` la página y continúe.</span><span class="sxs-lookup"><span data-stu-id="77ab1-148">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="77ab1-149">Vuelva a Teams.</span><span class="sxs-lookup"><span data-stu-id="77ab1-149">Go back to Teams.</span></span> <span data-ttu-id="77ab1-150">En el cuadro de diálogo, **selecciona Agregar para instalar** la aplicación.</span><span class="sxs-lookup"><span data-stu-id="77ab1-150">In the dialog, select **Add for me** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Captura de pantalla que muestra un ejemplo de aplicación de pestaña personal &quot;Hello, World!&quot; que se ejecuta en Teams.":::

<span data-ttu-id="77ab1-152">🎉 Enhorabuena.</span><span class="sxs-lookup"><span data-stu-id="77ab1-152">🎉 Congratulations!</span></span> <span data-ttu-id="77ab1-153">La aplicación se está ejecutando en Teams.</span><span class="sxs-lookup"><span data-stu-id="77ab1-153">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="77ab1-154">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="77ab1-154">Next step</span></span>

<span data-ttu-id="77ab1-155">Expanda la pestaña personal que acaba de crear o cree otro tipo de aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="77ab1-155">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="77ab1-156">Agregar a la pestaña personal</span><span class="sxs-lookup"><span data-stu-id="77ab1-156">Add to your personal tab</span></span>](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="77ab1-157">Crear una pestaña de canal</span><span class="sxs-lookup"><span data-stu-id="77ab1-157">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="77ab1-158">Crear un bot</span><span class="sxs-lookup"><span data-stu-id="77ab1-158">Build a bot</span></span>](../build-your-first-app/build-bot.md)

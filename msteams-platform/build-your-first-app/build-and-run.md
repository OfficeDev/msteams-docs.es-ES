---
title: 'Introducción: compilar y ejecutar la primera aplicación'
author: heath-hamilton
description: Cree rápidamente una aplicación de Microsoft Teams que muestre un mensaje de "Hola a todos". con Microsoft Teams Toolkit.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: bc5d18dd887cbdbf56b8d6d013f53c21d1540370
ms.sourcegitcommit: 5687a901d48bcf2f5a3a086e0f703f854e8b9c21
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/11/2021
ms.locfileid: "49795471"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="459cd-104">Crear y ejecutar la primera aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="459cd-104">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="459cd-105">Puede acceder directamente al desarrollo de Microsoft Teams creando una pestaña personal que muestre "Hello, World!".</span><span class="sxs-lookup"><span data-stu-id="459cd-105">You can jump right into Microsoft Teams development by building a personal tab that displays "Hello, World!"</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="459cd-106">1. Crear el proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="459cd-106">1. Create your app project</span></span>

<span data-ttu-id="459cd-107">Use Microsoft Teams Toolkit en Visual Studio code para configurar su primer proyecto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="459cd-107">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. In Visual Studio Code, select **Microsoft Teams** on the left Activity Bar and choose Create a new Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **app**.
1. <span data-ttu-id="459cd-109">Cuando se le solicite, inicie sesión con su cuenta de desarrollo de Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="459cd-109">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="459cd-110">En la **pantalla Agregar funcionalidades,** seleccione **Pestaña** y, a **continuación, Siguiente.**</span><span class="sxs-lookup"><span data-stu-id="459cd-110">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Captura de pantalla que muestra cómo configurar el proyecto de aplicación con Visual Studio Kit de herramientas de Code Teams.":::
1. <span data-ttu-id="459cd-112">Escriba un nombre para su aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="459cd-112">Enter a name for your Teams app.</span></span> <span data-ttu-id="459cd-113">(Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de aplicación en el equipo local).</span><span class="sxs-lookup"><span data-stu-id="459cd-113">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="459cd-114">Comprueba solo la **opción de pestaña Personal** y selecciona **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="459cd-114">Check only the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="459cd-115">2. Comprender los componentes importantes del proyecto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="459cd-115">2. Understand important app project components</span></span>

<span data-ttu-id="459cd-116">Una vez que el kit de herramientas configura el proyecto, tiene los componentes para crear una pestaña personal básica para Teams.</span><span class="sxs-lookup"><span data-stu-id="459cd-116">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="459cd-117">Los archivos y directorios del proyecto se muestran en el área Explorador de Visual Studio código.</span><span class="sxs-lookup"><span data-stu-id="459cd-117">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Captura de pantalla que muestra los archivos de proyecto de la aplicación para una pestaña personal en Visual Studio código.":::

### <a name="app-scaffolding"></a><span data-ttu-id="459cd-119">Scaffolding de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="459cd-119">App scaffolding</span></span>

<span data-ttu-id="459cd-120">El kit de herramientas crea automáticamente scaffolding para ti en el directorio en función de las `src` funcionalidades que agregaste durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="459cd-120">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="459cd-121">Si creas una pestaña durante la instalación, por ejemplo, el archivo del directorio es importante porque controla la inicialización y el `App.js` `src/components` enrutamiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="459cd-121">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="459cd-122">Llama al SDK del cliente [de JavaScript](../tabs/how-to/using-teams-client-sdk.md) de Microsoft Teams para establecer la comunicación entre la aplicación y Teams.</span><span class="sxs-lookup"><span data-stu-id="459cd-122">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-id"></a><span data-ttu-id="459cd-123">Identificador de la aplicación</span><span class="sxs-lookup"><span data-stu-id="459cd-123">App ID</span></span>

<span data-ttu-id="459cd-124">El identificador de aplicación de Teams es necesario para configurar la aplicación con App Studio.</span><span class="sxs-lookup"><span data-stu-id="459cd-124">Your Teams app ID is needed to configure your app with App Studio.</span></span> <span data-ttu-id="459cd-125">Puede encontrar el identificador en el `teamsAppId` objeto, que se encuentra en el archivo del `package.json` proyecto.</span><span class="sxs-lookup"><span data-stu-id="459cd-125">You can find the ID in the `teamsAppId` object, which is located in your project's `package.json` file.</span></span>

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="459cd-126">3. Compilar y ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="459cd-126">3. Build and run your app</span></span>

<span data-ttu-id="459cd-127">En interés del tiempo, compilarás y ejecutarás la aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="459cd-127">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="459cd-128">(Esta información también está disponible en el kit de `README` herramientas).</span><span class="sxs-lookup"><span data-stu-id="459cd-128">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="459cd-129">En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .</span><span class="sxs-lookup"><span data-stu-id="459cd-129">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="459cd-130">Ejecute `npm start` .</span><span class="sxs-lookup"><span data-stu-id="459cd-130">Run `npm start`.</span></span>

<span data-ttu-id="459cd-131">Una vez completado, se compila **correctamente.**</span><span class="sxs-lookup"><span data-stu-id="459cd-131">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="459cd-132">en el terminal.</span><span class="sxs-lookup"><span data-stu-id="459cd-132">message in the terminal.</span></span> <span data-ttu-id="459cd-133">La aplicación se está ejecutando en `https://localhost:3000` .</span><span class="sxs-lookup"><span data-stu-id="459cd-133">Your app is running on `https://localhost:3000`.</span></span>

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="459cd-134">4. Instalación local de la aplicación en Teams</span><span class="sxs-lookup"><span data-stu-id="459cd-134">4. Sideload your app in Teams</span></span>

<span data-ttu-id="459cd-135">La aplicación está lista para probarse en Teams.</span><span class="sxs-lookup"><span data-stu-id="459cd-135">Your app is ready to test in Teams.</span></span> <span data-ttu-id="459cd-136">Para ello, debes tener una cuenta que permita la instalación de prueba de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="459cd-136">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="459cd-137">(Si no está seguro de que lo tiene, obtenga información sobre cómo obtener una cuenta [de desarrollo de Teams).](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)</span><span class="sxs-lookup"><span data-stu-id="459cd-137">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

> [!TIP]
> <span data-ttu-id="459cd-138">Antes de realizar la instalación de prueba de la aplicación, comprueba si hay problemas con la característica de validación de [App Studio,](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)que se incluye en el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="459cd-138">Before sideloading your app, check for issues using the [validation feature in App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), which is included in the toolkit.</span></span> <span data-ttu-id="459cd-139">Los errores deben corregirse para realizar una instalación de prueba correcta de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="459cd-139">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="459cd-140">En Visual Studio, presione la tecla **F5** para iniciar un cliente web de Teams.</span><span class="sxs-lookup"><span data-stu-id="459cd-140">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="459cd-141">Para mostrar el contenido de la aplicación en Teams, especifique que el lugar donde se ejecuta la aplicación ( `localhost` ) es de confianza:</span><span class="sxs-lookup"><span data-stu-id="459cd-141">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="459cd-142">Abra una nueva pestaña en la misma ventana del explorador (Google Chrome de forma predeterminada) que se abrió después de presionar **F5**.</span><span class="sxs-lookup"><span data-stu-id="459cd-142">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="459cd-143">Vaya a `https://localhost:3000/tab` la página y continúe.</span><span class="sxs-lookup"><span data-stu-id="459cd-143">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="459cd-144">Vuelva a Teams.</span><span class="sxs-lookup"><span data-stu-id="459cd-144">Go back to Teams.</span></span> <span data-ttu-id="459cd-145">En el cuadro de diálogo, **selecciona Agregar para instalar** la aplicación.</span><span class="sxs-lookup"><span data-stu-id="459cd-145">In the dialog, select **Add for me** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Captura de pantalla que muestra un ejemplo de aplicación de pestaña personal &quot;Hello, World!&quot; que se ejecuta en Teams.":::

<span data-ttu-id="459cd-147">🎉 Enhorabuena.</span><span class="sxs-lookup"><span data-stu-id="459cd-147">🎉 Congratulations!</span></span> <span data-ttu-id="459cd-148">La aplicación se está ejecutando en Teams.</span><span class="sxs-lookup"><span data-stu-id="459cd-148">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="459cd-149">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="459cd-149">Next step</span></span>

<span data-ttu-id="459cd-150">Expanda la pestaña personal que acaba de crear o cree otro tipo de aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="459cd-150">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="459cd-151">Agregar a la pestaña personal</span><span class="sxs-lookup"><span data-stu-id="459cd-151">Add to your personal tab</span></span>](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="459cd-152">Crear una pestaña de canal</span><span class="sxs-lookup"><span data-stu-id="459cd-152">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="459cd-153">Crear un bot</span><span class="sxs-lookup"><span data-stu-id="459cd-153">Build a bot</span></span>](../build-your-first-app/build-bot.md)

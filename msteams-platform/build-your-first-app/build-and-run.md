---
title: 'Introducción: creación y ejecución de la primera aplicación'
author: heath-hamilton
description: Cree rápidamente una aplicación de Microsoft teams que muestre un "Hola a todos". mensaje mediante el kit de herramientas de Microsoft Teams.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 2d357ef71bfc4c498b54d94f9d0717cf886df17d
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552482"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="62531-104">Crear y ejecutar su primera aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="62531-104">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="62531-105">Puede ir directamente a desarrollo de Microsoft Teams creando una pestaña personal que muestre "Hola a todos".</span><span class="sxs-lookup"><span data-stu-id="62531-105">You can jump right into Microsoft Teams development by building a personal tab that displays "Hello, World!"</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="62531-106">1. crear un proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="62531-106">1. Create your app project</span></span>

<span data-ttu-id="62531-107">Use el kit de herramientas de Microsoft Teams en Visual Studio Code para configurar su primer proyecto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="62531-107">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **crear una nueva aplicación de Teams**.
1. <span data-ttu-id="62531-109">Cuando se le solicite, inicie sesión con su cuenta de desarrollo de 365 de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="62531-109">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="62531-110">En la pantalla **Agregar funciones** , seleccione la **pestaña** **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="62531-110">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Captura de pantalla que muestra cómo configurar el proyecto de aplicación con Visual Studio Code Teams Toolkit.":::
1. <span data-ttu-id="62531-112">Escriba un nombre para la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="62531-112">Enter a name for your Teams app.</span></span> <span data-ttu-id="62531-113">(Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de la aplicación en el equipo local).</span><span class="sxs-lookup"><span data-stu-id="62531-113">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="62531-114">Compruebe solo la opción de la **pestaña personal** y seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="62531-114">Check only the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

> [!NOTE]

> <span data-ttu-id="62531-115">Para instalar el paquete de la aplicación después de crear un nuevo proyecto en el kit de herramientas, presione F5/ejecutar.</span><span class="sxs-lookup"><span data-stu-id="62531-115">To install your app package after creating a new project in the toolkit, press F5/run.</span></span> <span data-ttu-id="62531-116">Iniciará Chrome e instalará el paquete.</span><span class="sxs-lookup"><span data-stu-id="62531-116">It will launch Chrome and install your package.</span></span> <span data-ttu-id="62531-117">El paquete se almacena en App Studio y se instala mediante el `appId` .</span><span class="sxs-lookup"><span data-stu-id="62531-117">The package is stored in App Studio and installed using the `appId`.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="62531-118">2. comprender los componentes importantes del proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="62531-118">2. Understand important app project components</span></span>

<span data-ttu-id="62531-119">Una vez que el kit de herramientas configura el proyecto, tiene los componentes para crear una pestaña básica personal para Teams.</span><span class="sxs-lookup"><span data-stu-id="62531-119">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="62531-120">Los archivos y directorios del proyecto se muestran en el área del explorador de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="62531-120">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Captura de pantalla que muestra archivos de proyecto de aplicación para una pestaña personal en Visual Studio Code.":::

### <a name="app-scaffolding"></a><span data-ttu-id="62531-122">Scaffolding de la aplicación</span><span class="sxs-lookup"><span data-stu-id="62531-122">App scaffolding</span></span>

<span data-ttu-id="62531-123">El kit de herramientas crea automáticamente scaffolding en el `src` directorio en función de las funciones que agregó durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="62531-123">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="62531-124">Si crea una ficha durante la configuración, por ejemplo, el `App.js` archivo del `src/components` directorio es importante porque controla la inicialización y el enrutamiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="62531-124">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="62531-125">Llama al [SDK de Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md) para establecer la comunicación entre la aplicación y los equipos.</span><span class="sxs-lookup"><span data-stu-id="62531-125">It calls the [Microsoft Teams SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-id"></a><span data-ttu-id="62531-126">Identificador de la aplicación</span><span class="sxs-lookup"><span data-stu-id="62531-126">App ID</span></span>

<span data-ttu-id="62531-127">El identificador de aplicación de Teams es necesario para configurar la aplicación con App Studio.</span><span class="sxs-lookup"><span data-stu-id="62531-127">Your Teams app ID is needed to configure your app with App Studio.</span></span> <span data-ttu-id="62531-128">Puede encontrar el identificador en el `teamsAppId` objeto, que se encuentra en el archivo del proyecto `package.json` .</span><span class="sxs-lookup"><span data-stu-id="62531-128">You can find the ID in the `teamsAppId` object, which is located in your project's `package.json` file.</span></span>

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="62531-129">3. compilar y ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="62531-129">3. Build and run your app</span></span>

<span data-ttu-id="62531-130">En aras del tiempo, se creará y se ejecutará la aplicación de forma local.</span><span class="sxs-lookup"><span data-stu-id="62531-130">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="62531-131">(Esta información también está disponible en el kit de herramientas `README` ).</span><span class="sxs-lookup"><span data-stu-id="62531-131">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="62531-132">En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .</span><span class="sxs-lookup"><span data-stu-id="62531-132">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="62531-133">Ejecutar `npm start` .</span><span class="sxs-lookup"><span data-stu-id="62531-133">Run `npm start`.</span></span>

<span data-ttu-id="62531-134">Una vez completada la **compilación correctamente.**</span><span class="sxs-lookup"><span data-stu-id="62531-134">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="62531-135">mensaje en el terminal.</span><span class="sxs-lookup"><span data-stu-id="62531-135">message in the terminal.</span></span> <span data-ttu-id="62531-136">La aplicación se está ejecutando en `https://localhost:3000` .</span><span class="sxs-lookup"><span data-stu-id="62531-136">Your app is running on `https://localhost:3000`.</span></span>

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="62531-137">4. transferir localmente la aplicación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="62531-137">4. Sideload your app in Teams</span></span>

<span data-ttu-id="62531-138">La aplicación está lista para realizar pruebas en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="62531-138">Your app is ready to test in Teams.</span></span> <span data-ttu-id="62531-139">Para ello, debe tener una cuenta que permita la transferencia local de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="62531-139">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="62531-140">(Si no está seguro de ello, obtenga información sobre cómo obtener una cuenta de desarrollo de Microsoft [Teams](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)).</span><span class="sxs-lookup"><span data-stu-id="62531-140">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

> [!TIP]
> <span data-ttu-id="62531-141">Antes de transferir localmente la aplicación, compruebe si hay problemas con la [característica de validación en App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), que se incluye en el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="62531-141">Before sideloading your app, check for issues using the [validation feature in App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), which is included in the toolkit.</span></span> <span data-ttu-id="62531-142">Los errores deben corregirse para realizar una instalación de prueba de la aplicación correctamente.</span><span class="sxs-lookup"><span data-stu-id="62531-142">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="62531-143">En Visual Studio Code, presione la tecla **F5** para iniciar un cliente web de Teams.</span><span class="sxs-lookup"><span data-stu-id="62531-143">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="62531-144">Para mostrar el contenido de la aplicación en Teams, especifique que la aplicación en ejecución ( `localhost` ) sea de confianza:</span><span class="sxs-lookup"><span data-stu-id="62531-144">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="62531-145">Abrir una nueva pestaña en la misma ventana del explorador (Google Chrome de forma predeterminada) que se abre después de presionar **F5**.</span><span class="sxs-lookup"><span data-stu-id="62531-145">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="62531-146">Vaya a `https://localhost:3000/tab` la página y continúe con ella.</span><span class="sxs-lookup"><span data-stu-id="62531-146">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="62531-147">Vuelva a teams.</span><span class="sxs-lookup"><span data-stu-id="62531-147">Go back to Teams.</span></span> <span data-ttu-id="62531-148">En el cuadro de diálogo, seleccione **agregarme para** instalar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="62531-148">In the dialog, select **Add for me** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Captura de pantalla que muestra un ejemplo de la aplicación de pestaña personal ' Hello, World! ' en Teams.":::

<span data-ttu-id="62531-150">¡ Felicidades 🎉!</span><span class="sxs-lookup"><span data-stu-id="62531-150">🎉 Congratulations!</span></span> <span data-ttu-id="62531-151">La aplicación se está ejecutando en Teams.</span><span class="sxs-lookup"><span data-stu-id="62531-151">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="62531-152">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="62531-152">Next step</span></span>

<span data-ttu-id="62531-153">Amplíe en la pestaña personal que acaba de crear o compile otro tipo de aplicación de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="62531-153">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="62531-154">Agregar a la pestaña personal</span><span class="sxs-lookup"><span data-stu-id="62531-154">Add to your personal tab</span></span>](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="62531-155">Crear una pestaña de canal</span><span class="sxs-lookup"><span data-stu-id="62531-155">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="62531-156">Crear un bot</span><span class="sxs-lookup"><span data-stu-id="62531-156">Build a bot</span></span>](../build-your-first-app/build-bot.md)

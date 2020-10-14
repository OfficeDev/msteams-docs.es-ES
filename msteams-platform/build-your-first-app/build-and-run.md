---
title: 'Introducción: creación y ejecución de la primera aplicación'
author: heath-hamilton
description: Cree rápidamente una aplicación de Microsoft teams que muestre un "Hola a todos". mensaje mediante el kit de herramientas de Microsoft Teams.
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: quickstart
ms.openlocfilehash: 20c9eee14649cda23e1d682940f489e78cba24b9
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452648"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="d5ed1-104">Crear y ejecutar su primera aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d5ed1-104">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="d5ed1-105">Puede ir directamente a desarrollo de Microsoft Teams creando una pestaña personal que muestre "Hola a todos".</span><span class="sxs-lookup"><span data-stu-id="d5ed1-105">You can jump right into Microsoft Teams development by building a personal tab that displays "Hello, World!"</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="d5ed1-106">1. crear un proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="d5ed1-106">1. Create your app project</span></span>

<span data-ttu-id="d5ed1-107">Use el kit de herramientas de Microsoft Teams en Visual Studio Code para configurar su primer proyecto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-107">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **crear una nueva aplicación de Teams**.
:::image type="content" source="../assets/images/build-your-first-app/create-teams-app.png" alt-text="Captura de pantalla que muestra cómo crear una nueva aplicación con el kit de herramientas de Visual Studio Code Teams.":::
1. <span data-ttu-id="d5ed1-110">Escriba un nombre para la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-110">Enter a name for your Teams app.</span></span> <span data-ttu-id="d5ed1-111">(Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de la aplicación en el equipo local).</span><span class="sxs-lookup"><span data-stu-id="d5ed1-111">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="d5ed1-112">En la pantalla **Agregar funciones** , seleccione la **pestaña** **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-112">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Captura de pantalla que muestra cómo crear una nueva aplicación con el kit de herramientas de Visual Studio Code Teams.":::
1. <span data-ttu-id="d5ed1-114">Compruebe la opción de la **ficha personal** y seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-114">Check the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="d5ed1-115">2. comprender los componentes importantes del proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="d5ed1-115">2. Understand important app project components</span></span>

<span data-ttu-id="d5ed1-116">Una vez que el kit de herramientas configura el proyecto, tiene los componentes para crear una pestaña básica personal para Teams.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-116">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="d5ed1-117">Los archivos y directorios del proyecto se muestran en el área del explorador de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-117">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Captura de pantalla que muestra cómo crear una nueva aplicación con el kit de herramientas de Visual Studio Code Teams.":::

<span data-ttu-id="d5ed1-119">Dedique un momento a comprender algunos de los archivos principales con los que trabajan los desarrolladores de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-119">Let's take a moment to understand some of the key files Teams app developers work with.</span></span>

### <a name="app-manifest-manifestjson"></a><span data-ttu-id="d5ed1-120">Manifiesto de la aplicación ( `manifest.json` )</span><span class="sxs-lookup"><span data-stu-id="d5ed1-120">App manifest (`manifest.json`)</span></span>

<span data-ttu-id="d5ed1-121">Ubicado en el `.publish` directorio, el manifiesto de la aplicación es el punto de partida para cualquier proyecto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-121">Located in the `.publish` directory, the app manifest is the starting point for any app project.</span></span> <span data-ttu-id="d5ed1-122">El manifiesto define los atributos fundamentales de la aplicación y apunta a los recursos necesarios.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-122">The manifest defines your app's fundamental attributes and points to required resources.</span></span> <span data-ttu-id="d5ed1-123">Al instalar una aplicación, Microsoft Teams analiza el manifiesto para comprender cómo representar la aplicación en el cliente.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-123">When you install an app, Teams parses the manifest to understand how to render your app in the client.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="d5ed1-124">Scaffolding de la aplicación</span><span class="sxs-lookup"><span data-stu-id="d5ed1-124">App scaffolding</span></span>

<span data-ttu-id="d5ed1-125">El kit de herramientas crea automáticamente scaffolding en el `src` directorio en función de las funciones que agregó durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-125">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="d5ed1-126">Si crea una ficha durante la configuración, por ejemplo, el `App.js` archivo del `src/components` directorio es importante porque controla la inicialización y el enrutamiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-126">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="d5ed1-127">Llama al [SDK de Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md) para establecer la comunicación entre la aplicación y los equipos.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-127">It calls the [Microsoft Teams SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-package-developmentzip"></a><span data-ttu-id="d5ed1-128">Paquete de la aplicación ( `Development.zip` )</span><span class="sxs-lookup"><span data-stu-id="d5ed1-128">App package (`Development.zip`)</span></span>

<span data-ttu-id="d5ed1-129">Ubicado en el `.publish` directorio, necesita que el paquete de la aplicación [transfiera localmente la aplicación](../concepts/deploy-and-publish/overview.md#upload-your-app-directly) en Teams.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-129">Located in the `.publish` directory, you need the app package to [sideload your app](../concepts/deploy-and-publish/overview.md#upload-your-app-directly) in Teams.</span></span> <span data-ttu-id="d5ed1-130">El paquete también se usa cuando se [publica en el catálogo de aplicaciones de la organización](../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) o [AppSource](../concepts/deploy-and-publish/appsource/publish.md).</span><span class="sxs-lookup"><span data-stu-id="d5ed1-130">The package is also used when [publishing to your organization's app catalog](../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or [AppSource](../concepts/deploy-and-publish/appsource/publish.md).</span></span>

<span data-ttu-id="d5ed1-131">Estos son algunos detalles sobre los archivos del paquete de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="d5ed1-131">Here are some details about the app package files:</span></span>

|<span data-ttu-id="d5ed1-132">Nombre</span><span class="sxs-lookup"><span data-stu-id="d5ed1-132">Name</span></span>|<span data-ttu-id="d5ed1-133">Tipo</span><span class="sxs-lookup"><span data-stu-id="d5ed1-133">Type</span></span>|<span data-ttu-id="d5ed1-134">Size</span><span class="sxs-lookup"><span data-stu-id="d5ed1-134">Size</span></span>|<span data-ttu-id="d5ed1-135">Ubicación del manifiesto</span><span class="sxs-lookup"><span data-stu-id="d5ed1-135">Manifest location</span></span>|<span data-ttu-id="d5ed1-136">Nombre de archivo Toolkit</span><span class="sxs-lookup"><span data-stu-id="d5ed1-136">Toolkit filename</span></span>|
|---|---|:---:|:---:|-----|
|<span data-ttu-id="d5ed1-137">**Manifiesto de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="d5ed1-137">**App manifest**</span></span>|`.json`| <span data-ttu-id="d5ed1-138">—</span><span class="sxs-lookup"><span data-stu-id="d5ed1-138">—</span></span> | <span data-ttu-id="d5ed1-139">—</span><span class="sxs-lookup"><span data-stu-id="d5ed1-139">—</span></span> |`.publish/manifest.json`|
|<span data-ttu-id="d5ed1-140">**Logotipo-color**</span><span class="sxs-lookup"><span data-stu-id="d5ed1-140">**Color logo**</span></span>|`.png`|<span data-ttu-id="d5ed1-141">192 &times; 192 píxeles</span><span class="sxs-lookup"><span data-stu-id="d5ed1-141">192&times;192 pixels</span></span>|`icon.color`|`.publish/color.png`|
|<span data-ttu-id="d5ed1-142">**Logotipo de contorno**</span><span class="sxs-lookup"><span data-stu-id="d5ed1-142">**Outline logo**</span></span>|`.png`|<span data-ttu-id="d5ed1-143">32 &times; 32 píxeles</span><span class="sxs-lookup"><span data-stu-id="d5ed1-143">32&times;32 pixels</span></span>|`icon.outline`|`.publish/outline.png`|

## <a name="3-run-your-app"></a><span data-ttu-id="d5ed1-144">3. ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="d5ed1-144">3. Run your app</span></span>

<span data-ttu-id="d5ed1-145">En aras del tiempo, se creará y se ejecutará la aplicación de forma local.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-145">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="d5ed1-146">(Esta información también está disponible en el kit de herramientas `README` ).</span><span class="sxs-lookup"><span data-stu-id="d5ed1-146">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="d5ed1-147">En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .</span><span class="sxs-lookup"><span data-stu-id="d5ed1-147">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="d5ed1-148">Ejecutar `npm start` .</span><span class="sxs-lookup"><span data-stu-id="d5ed1-148">Run `npm start`.</span></span> <span data-ttu-id="d5ed1-149">Una vez completada la **compilación correctamente.**</span><span class="sxs-lookup"><span data-stu-id="d5ed1-149">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="d5ed1-150">mensaje en el terminal.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-150">message in the terminal.</span></span>
1. <span data-ttu-id="d5ed1-151">Abra un explorador y vaya a `https://localhost:3000` para ver una página web en blanco denominada **pestaña de Microsoft Teams**. (No se preocupe porque no puede ver ningún contenido en la página).</span><span class="sxs-lookup"><span data-stu-id="d5ed1-151">Open a browser and go to `https://localhost:3000` to view a blank webpage called **Microsoft Teams Tab**. (Don't worry that you can't see any content on the page.)</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/local-host-tab.png" alt-text="Captura de pantalla que muestra cómo crear una nueva aplicación con el kit de herramientas de Visual Studio Code Teams.":::

## <a name="4-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="d5ed1-153">4. configurar un túnel seguro a la aplicación</span><span class="sxs-lookup"><span data-stu-id="d5ed1-153">4. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="d5ed1-154">La aplicación está en funcionamiento en el servidor Web local.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-154">Your app is up and running on your local web server.</span></span> <span data-ttu-id="d5ed1-155">Para ejecutar la aplicación en Microsoft Teams, debe ser `localhost` accesible a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-155">To run your app in Teams, you must make your `localhost` accessible through HTTPS.</span></span>

<span data-ttu-id="d5ed1-156">Instale [ngrok](https://ngrok.com/download) si todavía no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-156">Install [ngrok](https://ngrok.com/download) if you haven't already.</span></span> <span data-ttu-id="d5ed1-157">Al ejecutar esta herramienta, se crean dos direcciones URL disponibles globalmente que apuntan a su servidor Web local ( `http://localhost:3000` ).</span><span class="sxs-lookup"><span data-stu-id="d5ed1-157">When you run this tool, you create two globally available URLs that point to your local web server (`http://localhost:3000`).</span></span> <span data-ttu-id="d5ed1-158">Necesita la dirección URL de reenvío que comienza con `HTTPS` .</span><span class="sxs-lookup"><span data-stu-id="d5ed1-158">You need the forwarding URL that begins with `HTTPS`.</span></span>

1. <span data-ttu-id="d5ed1-159">Abra un nuevo terminal y ejecute `ngrok http 3000` .</span><span class="sxs-lookup"><span data-stu-id="d5ed1-159">Open a new terminal and run `ngrok http 3000`.</span></span>
1. <span data-ttu-id="d5ed1-160">Copie la dirección URL HTTPS que ha proporcionado (vea el siguiente ejemplo).</span><span class="sxs-lookup"><span data-stu-id="d5ed1-160">Copy the HTTPS URL you're provided (see the following example).</span></span>
:::image type="content" source="../assets/images/build-your-first-app/ngrok-running.png" alt-text="Captura de pantalla que muestra cómo crear una nueva aplicación con el kit de herramientas de Visual Studio Code Teams.":::
1. <span data-ttu-id="d5ed1-162">En el `.publish` directorio, Abra `Development.env` .</span><span class="sxs-lookup"><span data-stu-id="d5ed1-162">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="d5ed1-163">Reemplace el `baseUrl0` valor por la dirección URL copiada.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-163">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="d5ed1-164">(Por ejemplo, cambie `baseUrl0=http://localhost:3000` a `baseUrl0=https://85528b2b3ba5.ngrok.io` ).</span><span class="sxs-lookup"><span data-stu-id="d5ed1-164">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ba5.ngrok.io`.)</span></span>

<span data-ttu-id="d5ed1-165">El manifiesto de la aplicación ahora apunta al lugar donde se hospeda la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-165">Your app manifest now points to where you're hosting the app.</span></span>

## <a name="5-sideload-your-app-in-teams"></a><span data-ttu-id="d5ed1-166">5. transferir localmente la aplicación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d5ed1-166">5. Sideload your app in Teams</span></span>

<span data-ttu-id="d5ed1-167">Una vez que la aplicación se ejecute y sea accesible a través de HTTPS, estará listo para cargarla a teams.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-167">With your app running and accessible via HTTPS, you're ready to upload it to Teams.</span></span>

> [!TIP]
> <span data-ttu-id="d5ed1-168">Antes de transferir localmente la aplicación, compruebe si hay problemas con la [característica de validación del kit de herramientas](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool).</span><span class="sxs-lookup"><span data-stu-id="d5ed1-168">Before sideloading your app, check for issues using the [toolkit's validation feature](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool).</span></span> <span data-ttu-id="d5ed1-169">Los errores deben corregirse para realizar una instalación de prueba de la aplicación correctamente.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-169">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="d5ed1-170">Inicie sesión en el cliente de Teams con su cuenta que permite la transferencia local de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-170">Log in to the Teams client with your account that allows app sideloading.</span></span> <span data-ttu-id="d5ed1-171">(Si no está seguro de ello, obtenga información sobre cómo obtener una cuenta de desarrollo de Microsoft [Teams](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)).</span><span class="sxs-lookup"><span data-stu-id="d5ed1-171">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>
1. <span data-ttu-id="d5ed1-172">Seleccione **aplicaciones**y, después, elija **cargar una aplicación personalizada**.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-172">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="d5ed1-173">Vaya a la carpeta de proyecto de la aplicación `.publish` y seleccione `Development.zip` .</span><span class="sxs-lookup"><span data-stu-id="d5ed1-173">Go to your app project `.publish` folder and select `Development.zip`.</span></span> <span data-ttu-id="d5ed1-174">Se muestra un modal de instalación.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-174">An installation modal displays.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/add-teams-app.png" alt-text="Captura de pantalla que muestra cómo crear una nueva aplicación con el kit de herramientas de Visual Studio Code Teams.":::
1. <span data-ttu-id="d5ed1-176">Seleccione **Agregar** para instalar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-176">Select **Add** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Captura de pantalla que muestra cómo crear una nueva aplicación con el kit de herramientas de Visual Studio Code Teams.":::

<span data-ttu-id="d5ed1-178">¡ Felicidades 🎉!</span><span class="sxs-lookup"><span data-stu-id="d5ed1-178">🎉 Congratulations!</span></span> <span data-ttu-id="d5ed1-179">La aplicación se está ejecutando en Teams.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-179">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="d5ed1-180">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="d5ed1-180">Next step</span></span>

<span data-ttu-id="d5ed1-181">Amplíe en la pestaña personal que acaba de crear o compile otro tipo de aplicación de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-181">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d5ed1-182">Agregar a la pestaña personal</span><span class="sxs-lookup"><span data-stu-id="d5ed1-182">Add to your personal tab</span></span>](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="d5ed1-183">Crear una pestaña de canal</span><span class="sxs-lookup"><span data-stu-id="d5ed1-183">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="d5ed1-184">Crear un bot</span><span class="sxs-lookup"><span data-stu-id="d5ed1-184">Build a bot</span></span>](../build-your-first-app/build-bot.md)

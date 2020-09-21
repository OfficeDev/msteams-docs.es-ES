---
title: Crear y ejecutar la aplicación primera aplicación Teams
author: heath-hamilton
ms.author: lajanuar
description: Ejecute su primera aplicación de Microsoft Teams.
ms.date: 08/31/2020
ms.topic: quickstart
ms.openlocfilehash: 441b70480d9c177e9c6140342df8c9ea29494a29
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964755"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="11462-103">Crear y ejecutar su primera aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="11462-103">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="11462-104">Puede pasar directamente al desarrollo en la plataforma de Microsoft Teams creando y ejecutando rápidamente una pestaña personal básica.</span><span class="sxs-lookup"><span data-stu-id="11462-104">You can jump right into developing on the Microsoft Teams platform by quickly building and running a basic personal tab.</span></span>

## <a name="create-your-app-project"></a><span data-ttu-id="11462-105">Crear el proyecto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="11462-105">Create your app project</span></span>

<span data-ttu-id="11462-106">Use el kit de herramientas de Microsoft Teams en Visual Studio Code para configurar su primer proyecto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="11462-106">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **crear una nueva aplicación de Teams**.
:::image type="content" source="../doc-links/images/create-teams-app.png" alt-text="crear imagen de aplicación de Teams":::
1. <span data-ttu-id="11462-109">Escriba un nombre para la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="11462-109">Enter a name for your Teams app.</span></span> <span data-ttu-id="11462-110">(Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de la aplicación en el equipo local).</span><span class="sxs-lookup"><span data-stu-id="11462-110">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="11462-111">En la pantalla **Agregar funciones** , seleccione la **pestaña** **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="11462-111">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../doc-links/images/choose-tab.png" alt-text="crear vista de imagen de la aplicación Teams":::
1. <span data-ttu-id="11462-113">Compruebe la opción de la **ficha personal** y seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="11462-113">Check the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="understand-important-app-project-components"></a><span data-ttu-id="11462-114">Comprender los componentes importantes del proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="11462-114">Understand important app project components</span></span>

<span data-ttu-id="11462-115">Una vez que el kit de herramientas configura el proyecto, tiene los componentes para crear una pestaña básica personal para Teams.</span><span class="sxs-lookup"><span data-stu-id="11462-115">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="11462-116">Los archivos y directorios del proyecto se muestran en el área del explorador de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="11462-116">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../doc-links/images/app-project-files.png" alt-text="Archivos de proyecto de aplicación en Visual Studio Code.":::

<span data-ttu-id="11462-118">Dedique tiempo a comprender algunos de los archivos clave en los que trabajan los desarrolladores de aplicaciones de Teams.</span><span class="sxs-lookup"><span data-stu-id="11462-118">Let's take time to understand some of the key files Teams app developers work with.</span></span>

### <a name="app-manifest-manifestjson"></a><span data-ttu-id="11462-119">Manifiesto de la aplicación ( `manifest.json` )</span><span class="sxs-lookup"><span data-stu-id="11462-119">App manifest (`manifest.json`)</span></span>

<span data-ttu-id="11462-120">Ubicado en el `.publish` directorio, el manifiesto de la aplicación es el punto de partida para cualquier proyecto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="11462-120">Located in the `.publish` directory, the app manifest is the starting point for any app project.</span></span> <span data-ttu-id="11462-121">El manifiesto define los atributos fundamentales de la aplicación y apunta a los recursos necesarios.</span><span class="sxs-lookup"><span data-stu-id="11462-121">The manifest defines your app's fundamental attributes and points to required resources.</span></span> <span data-ttu-id="11462-122">Al instalar una aplicación, Microsoft Teams analiza el manifiesto para comprender cómo representar la aplicación en el cliente.</span><span class="sxs-lookup"><span data-stu-id="11462-122">When you install an app, Teams parses the manifest to understand how to render your app in the client.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="11462-123">Scaffolding de la aplicación</span><span class="sxs-lookup"><span data-stu-id="11462-123">App scaffolding</span></span>

<span data-ttu-id="11462-124">El kit de herramientas crea automáticamente scaffolding en el `src` directorio en función de las funciones que agregó durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="11462-124">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="11462-125">Si crea una ficha durante la configuración, por ejemplo, el `App.js` archivo del `src/components` directorio es importante porque controla la inicialización y el enrutamiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="11462-125">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="11462-126">Llama al [SDK de Microsoft Teams](../../tabs/how-to/using-teams-client-sdk.md) para establecer la comunicación entre la aplicación y los equipos.</span><span class="sxs-lookup"><span data-stu-id="11462-126">It calls the [Microsoft Teams SDK](../../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-package-developmentzip"></a><span data-ttu-id="11462-127">Paquete de la aplicación ( `Development.zip` )</span><span class="sxs-lookup"><span data-stu-id="11462-127">App package (`Development.zip`)</span></span>

<span data-ttu-id="11462-128">Ubicado en el `.publish` directorio, necesita que el paquete de la aplicación [transfiera localmente la aplicación](../../concepts/deploy-and-publish/overview.md#upload-your-app-directly) en Teams.</span><span class="sxs-lookup"><span data-stu-id="11462-128">Located in the `.publish` directory, you need the app package to [sideload your app](../../concepts/deploy-and-publish/overview.md#upload-your-app-directly) in Teams.</span></span> <span data-ttu-id="11462-129">El paquete también se usa cuando se [publica en el catálogo de aplicaciones de la organización](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) o [AppSource](../../concepts/deploy-and-publish/appsource/publish.md).</span><span class="sxs-lookup"><span data-stu-id="11462-129">The package is also used when [publishing to your organization's app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or [AppSource](../../concepts/deploy-and-publish/appsource/publish.md).</span></span>

<span data-ttu-id="11462-130">Estos son algunos detalles sobre los archivos del paquete de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="11462-130">Here are some details about the app package files:</span></span>

|<span data-ttu-id="11462-131">Nombre</span><span class="sxs-lookup"><span data-stu-id="11462-131">Name</span></span>|<span data-ttu-id="11462-132">Tipo</span><span class="sxs-lookup"><span data-stu-id="11462-132">Type</span></span>|<span data-ttu-id="11462-133">Size</span><span class="sxs-lookup"><span data-stu-id="11462-133">Size</span></span>|<span data-ttu-id="11462-134">Ubicación del manifiesto</span><span class="sxs-lookup"><span data-stu-id="11462-134">Manifest location</span></span>|<span data-ttu-id="11462-135">Nombre de archivo Toolkit</span><span class="sxs-lookup"><span data-stu-id="11462-135">Toolkit filename</span></span>|
|---|---|:---:|:---:|-----|
|<span data-ttu-id="11462-136">**Manifiesto de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="11462-136">**App manifest**</span></span>|`.json`| <span data-ttu-id="11462-137">—</span><span class="sxs-lookup"><span data-stu-id="11462-137">—</span></span> | <span data-ttu-id="11462-138">—</span><span class="sxs-lookup"><span data-stu-id="11462-138">—</span></span> |`.publish/manifest.json`|
|<span data-ttu-id="11462-139">**Logotipo-color**</span><span class="sxs-lookup"><span data-stu-id="11462-139">**Color logo**</span></span>|`.png`|<span data-ttu-id="11462-140">192 &times; 192 píxeles</span><span class="sxs-lookup"><span data-stu-id="11462-140">192&times;192 pixels</span></span>|`icon.color`|`.publish/color.png`|
|<span data-ttu-id="11462-141">**Logotipo de contorno**</span><span class="sxs-lookup"><span data-stu-id="11462-141">**Outline logo**</span></span>|`.png`|<span data-ttu-id="11462-142">32 &times; 32 píxeles</span><span class="sxs-lookup"><span data-stu-id="11462-142">32&times;32 pixels</span></span>|`icon.outline`|`.publish/outline.png`|

## <a name="run-your-app"></a><span data-ttu-id="11462-143">Ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="11462-143">Run your app</span></span>

<span data-ttu-id="11462-144">En aras del tiempo, se creará y se ejecutará la aplicación de forma local.</span><span class="sxs-lookup"><span data-stu-id="11462-144">In the interest of time, you'll build and run your app locally.</span></span> <span data-ttu-id="11462-145">Las aplicaciones de Microsoft Teams en el nivel de producción se hospedan en la nube.</span><span class="sxs-lookup"><span data-stu-id="11462-145">Production-level Teams apps are hosted in the cloud.</span></span>

<span data-ttu-id="11462-146">(Esta información también está disponible en el kit de herramientas `README` ).</span><span class="sxs-lookup"><span data-stu-id="11462-146">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="11462-147">En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .</span><span class="sxs-lookup"><span data-stu-id="11462-147">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="11462-148">Ejecutar `npm start` .</span><span class="sxs-lookup"><span data-stu-id="11462-148">Run `npm start`.</span></span> <span data-ttu-id="11462-149">Una vez completada la **compilación correctamente.**</span><span class="sxs-lookup"><span data-stu-id="11462-149">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="11462-150">mensaje en el terminal.</span><span class="sxs-lookup"><span data-stu-id="11462-150">message in the terminal.</span></span>
1. <span data-ttu-id="11462-151">Abra un explorador y vaya a `https://localhost:3000` para ver una página web en blanco denominada **pestaña de Microsoft Teams**. (No se preocupe porque no puede ver ningún contenido en la página).</span><span class="sxs-lookup"><span data-stu-id="11462-151">Open a browser and go to `https://localhost:3000` to view a blank webpage called **Microsoft Teams Tab**. (Don't worry that you can't see any content on the page.)</span></span><br/>
   :::image type="content" source="../doc-links/images/local-host-tab.png" alt-text="Ver la aplicación en un explorador.":::

## <a name="set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="11462-153">Configurar un túnel seguro para la aplicación</span><span class="sxs-lookup"><span data-stu-id="11462-153">Set up a secure tunnel to your app</span></span>

<span data-ttu-id="11462-154">La aplicación está en funcionamiento en el servidor Web local.</span><span class="sxs-lookup"><span data-stu-id="11462-154">Your app is up and running on your local web server.</span></span> <span data-ttu-id="11462-155">Para ejecutar la aplicación en Microsoft Teams, debe ser `localhost` accesible a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="11462-155">To run your app in Teams, you must make your `localhost` accessible through HTTPS.</span></span>

<span data-ttu-id="11462-156">Instale [ngrok](https://ngrok.com/download) si todavía no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="11462-156">Install [ngrok](https://ngrok.com/download) if you haven't already.</span></span> <span data-ttu-id="11462-157">Al ejecutar esta herramienta, se crean dos direcciones URL disponibles globalmente que apuntan a su servidor Web local ( `http://localhost:3000` ).</span><span class="sxs-lookup"><span data-stu-id="11462-157">When you run this tool, you create two globally available URLs that point to your local web server (`http://localhost:3000`).</span></span> <span data-ttu-id="11462-158">Necesita la dirección URL de reenvío que comienza con `HTTPS` .</span><span class="sxs-lookup"><span data-stu-id="11462-158">You need the forwarding URL that begins with `HTTPS`.</span></span>

1. <span data-ttu-id="11462-159">Abra un nuevo terminal y ejecute `ngrok http 3000` .</span><span class="sxs-lookup"><span data-stu-id="11462-159">Open a new terminal and run `ngrok http 3000`.</span></span>
1. <span data-ttu-id="11462-160">Copie la dirección URL HTTPS que ha proporcionado (vea el siguiente ejemplo).</span><span class="sxs-lookup"><span data-stu-id="11462-160">Copy the HTTPS URL you're provided (see the following example).</span></span>
:::image type="content" source="../doc-links/images/ngrok-running.png" alt-text="imagen en ejecución ngrok":::
1. <span data-ttu-id="11462-162">En el `.publish` directorio, Abra `Development.env` .</span><span class="sxs-lookup"><span data-stu-id="11462-162">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="11462-163">Reemplace el `baseUrl0` valor por la dirección URL copiada.</span><span class="sxs-lookup"><span data-stu-id="11462-163">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="11462-164">(Por ejemplo, cambie `baseUrl0=http://localhost:3000` a `baseUrl0=https://85528b2b3ba5.ngrok.io` ).</span><span class="sxs-lookup"><span data-stu-id="11462-164">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ba5.ngrok.io`.)</span></span>

<span data-ttu-id="11462-165">El manifiesto de la aplicación ahora apunta al lugar donde se hospeda la aplicación.</span><span class="sxs-lookup"><span data-stu-id="11462-165">Your app manifest now points to where you're hosting the app.</span></span>

## <a name="sideload-your-app-in-teams"></a><span data-ttu-id="11462-166">Transferir localmente la aplicación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="11462-166">Sideload your app in Teams</span></span>

<span data-ttu-id="11462-167">Una vez que la aplicación se ejecute y sea accesible a través de HTTPS, estará listo para cargarla a teams.</span><span class="sxs-lookup"><span data-stu-id="11462-167">With your app running and accessible via HTTPS, you're ready to upload it to Teams.</span></span>

> [!TIP]
> <span data-ttu-id="11462-168">Antes de transferir localmente la aplicación, compruebe si hay problemas con la [característica de validación del kit de herramientas](../../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool).</span><span class="sxs-lookup"><span data-stu-id="11462-168">Before sideloading your app, check for issues using the [toolkit's validation feature](../../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool).</span></span> <span data-ttu-id="11462-169">Los errores deben corregirse para realizar una instalación de prueba de la aplicación correctamente.</span><span class="sxs-lookup"><span data-stu-id="11462-169">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="11462-170">Inicie sesión en el cliente de Teams con su cuenta que permite la transferencia local de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="11462-170">Log in to the Teams client with your account that allows app sideloading.</span></span> <span data-ttu-id="11462-171">(Si no está seguro de ello, obtenga información sobre cómo obtener una cuenta de desarrollo de Microsoft [Teams](../build-your-first-app/building-real-world-app.md#set-up-your-development-account)).</span><span class="sxs-lookup"><span data-stu-id="11462-171">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/building-real-world-app.md#set-up-your-development-account).)</span></span>
1. <span data-ttu-id="11462-172">Seleccione **aplicaciones**y, después, elija **cargar una aplicación personalizada**.</span><span class="sxs-lookup"><span data-stu-id="11462-172">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="11462-173">Vaya a la carpeta de proyecto de la aplicación `.publish` y seleccione `Development.zip` .</span><span class="sxs-lookup"><span data-stu-id="11462-173">Go to your app project `.publish` folder and select `Development.zip`.</span></span> <span data-ttu-id="11462-174">Se muestra un modal de instalación.</span><span class="sxs-lookup"><span data-stu-id="11462-174">An install modal displays.</span></span>
:::image type="content" source="../doc-links/images/add-teams-app.png" alt-text="Agregar aplicación de Teams":::
1. <span data-ttu-id="11462-176">Seleccione **Agregar** para instalar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="11462-176">Select **Add** to install your app.</span></span>
:::image type="content" source="../doc-links/images/tab-running.png" alt-text="Captura de pantalla que muestra un ejemplo de Hello, World! aplicación en Microsoft Teams.":::

<span data-ttu-id="11462-178">¡ Felicidades 🎉!</span><span class="sxs-lookup"><span data-stu-id="11462-178">🎉 Congratulations!</span></span> <span data-ttu-id="11462-179">La aplicación se está ejecutando en Teams.</span><span class="sxs-lookup"><span data-stu-id="11462-179">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="11462-180">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="11462-180">Next step</span></span>

<span data-ttu-id="11462-181">Amplíe en la pestaña personal que acaba de crear o compile otro tipo de aplicación de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="11462-181">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="11462-182">Agregar a la pestaña personal</span><span class="sxs-lookup"><span data-stu-id="11462-182">Add to your personal tab</span></span>](../build-your-first-app/add-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="11462-183">Crear una ficha de canal</span><span class="sxs-lookup"><span data-stu-id="11462-183">Build a channel tab</span></span>](../build-your-first-app/add-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="11462-184">Crear un bot</span><span class="sxs-lookup"><span data-stu-id="11462-184">Build a bot</span></span>](../build-your-first-app/add-bot.md)

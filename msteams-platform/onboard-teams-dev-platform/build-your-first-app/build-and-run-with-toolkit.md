---
title: Compilar y ejecutar la aplicación primera aplicación de Microsoft Teams
author: heath-hamilton
description: Ejecute su primera aplicación de Microsoft Teams.
ms.openlocfilehash: 98af8d8d6d89007e36c24bd34661ec21b33cbdf1
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652228"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="2ff2e-103">Crear y ejecutar su primera aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="2ff2e-103">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="2ff2e-104">Puede pasar directamente al desarrollo en la plataforma de Microsoft Teams creando y ejecutando rápidamente una aplicación básica.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-104">You can jump right into developing on the Microsoft Teams platform by quickly building and running a basic app.</span></span>

> [!NOTE]
> <span data-ttu-id="2ff2e-105">Resulta útil tener un conocimiento práctico de JavaScript (en concreto reaccionar) al seguir estos tutoriales.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-105">It's helpful to have working knowledge of JavaScript (specifically React) when following these tutorials.</span></span>

## <a name="set-up-your-development-account"></a><span data-ttu-id="2ff2e-106">Configurar la cuenta de desarrollo</span><span class="sxs-lookup"><span data-stu-id="2ff2e-106">Set up your development account</span></span>

<span data-ttu-id="2ff2e-107">Para compilar aplicaciones para Microsoft Teams, necesita una cuenta de teams que permita la transferencia local (es posible que la cuenta ya la proporcione).</span><span class="sxs-lookup"><span data-stu-id="2ff2e-107">To build apps for Teams, you need a Teams account that allows sideloading (your account may already provide this).</span></span> <span data-ttu-id="2ff2e-108">Si no es así, Regístrese para obtener una suscripción de desarrollador de Microsoft 365 para que pueda obtener un inquilino de prueba.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-108">If it doesn't, register for a Microsoft 365 developer subscription so you can get a test tenant.</span></span>

1. <span data-ttu-id="2ff2e-109">Compruebe si puede transferir aplicaciones en Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="2ff2e-109">Verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="2ff2e-110">En el cliente de Microsoft Teams, seleccione **aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-110">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="2ff2e-111">Busca una opción para **cargar una aplicación personalizada**.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-111">Look for an option to **Upload a custom app**.</span></span>
1. <span data-ttu-id="2ff2e-112">Si tiene esta opción, puede empezar a crear.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-112">If you have this option, you can start building.</span></span> <span data-ttu-id="2ff2e-113">Si no es así, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2ff2e-113">If not, do the following:</span></span>
    1. <span data-ttu-id="2ff2e-114">Regístrese para obtener una [suscripción de desarrollador de Microsoft 365](../doc-links/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="2ff2e-114">Register for a [Microsoft 365 developer subscription](../doc-links/prepare-your-o365-tenant.md).</span></span>
    1. <span data-ttu-id="2ff2e-115">[Habilite la transferencia local de aplicaciones personalizada](../doc-links/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) para su cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-115">[Enable custom app sideloading](../doc-links/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) for your test account.</span></span>

## <a name="get-your-development-tools"></a><span data-ttu-id="2ff2e-116">Obtener las herramientas de desarrollo</span><span class="sxs-lookup"><span data-stu-id="2ff2e-116">Get your development tools</span></span>

<span data-ttu-id="2ff2e-117">Puede crear aplicaciones de Teams con sus herramientas preferidas, pero esto es lo que necesita para empezar rápidamente con Visual Studio Code y el kit de herramientas de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-117">You can build Teams apps with your preferred tools, but here's what you need to get started quickly with Visual Studio Code and the Microsoft Teams Toolkit.</span></span>

1. <span data-ttu-id="2ff2e-118">Instale la versión más reciente de [Visual Studio Code](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="2ff2e-118">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span>
1. <span data-ttu-id="2ff2e-119">En Visual Studio Code, seleccione **extensions** ![ Visual Studio Toolkit View ](../doc-links/images/vs-code-extensions.png) en la barra de actividad izquierda e instale **Microsoft Teams Toolkit**.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-119">In Visual Studio Code, select **Extensions** ![visual studio toolkit view](../doc-links/images/vs-code-extensions.png) on the left Activity Bar and install the **Microsoft Teams Toolkit**.</span></span>
1. <span data-ttu-id="2ff2e-120">Instale [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="2ff2e-120">Install [Node.js](https://nodejs.org/en/).</span></span>

## <a name="create-an-app-project"></a><span data-ttu-id="2ff2e-121">Crear un proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="2ff2e-121">Create an app project</span></span>

<span data-ttu-id="2ff2e-122">El kit de herramientas de Microsoft Teams puede ayudarle a configurar su primer proyecto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-122">The Microsoft Teams Toolkit can help you set up your first app project.</span></span>

1. <span data-ttu-id="2ff2e-123">En Visual Studio Code, abra el kit de herramientas seleccionando el icono de Teams</span><span class="sxs-lookup"><span data-stu-id="2ff2e-123">In Visual Studio Code, open the toolkit by selecting the Teams icon</span></span> ![icono de Teams](../doc-links/images/favicon-16x16.png) <span data-ttu-id="2ff2e-125">en la barra de actividad izquierda.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-125">on the left Activity Bar.</span></span>
1. <span data-ttu-id="2ff2e-126">Seleccione **crear una nueva aplicación de Teams**.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-126">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="2ff2e-127">Cuando se le solicite, escriba un nombre para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-127">When prompted, enter a name for your app.</span></span> <span data-ttu-id="2ff2e-128">Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-128">This is the default name for your app and also the name of the project directory on your local machine.</span></span>
1. <span data-ttu-id="2ff2e-129">En la pantalla **Agregar funciones** , seleccione la **pestaña** **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-129">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
1. <span data-ttu-id="2ff2e-130">Compruebe la opción de la **ficha personal** y seleccione **Finalizar** para configurar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-130">Check the **Personal tab** option and select **Finish** to configure your project.</span></span>

![vista del kit de herramientas agregar pestañas](../doc-links/images/toolkit-add-tabs.PNG)

<span data-ttu-id="2ff2e-132">Una vez completada, tiene los componentes de scaffolding de la aplicación para crear una pestaña personal.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-132">Once complete, you have the app scaffolding components for building a personal tab.</span></span>

## <a name="run-your-app"></a><span data-ttu-id="2ff2e-133">Ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="2ff2e-133">Run your app</span></span>

<span data-ttu-id="2ff2e-134">Siga el `README.md` en su proyecto para compilar, ejecutar e implementar la aplicación en Teams.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-134">Follow the `README.md` in your project to build, run, and deploy your app to Teams.</span></span> <span data-ttu-id="2ff2e-135">En general, estas instrucciones le ayudarán a hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2ff2e-135">In general, these instructions help you do the following:</span></span>

* <span data-ttu-id="2ff2e-136">Hospedar la aplicación `localhost` .</span><span class="sxs-lookup"><span data-stu-id="2ff2e-136">Host your app on `localhost`.</span></span>
* <span data-ttu-id="2ff2e-137">[Configure un túnel seguro con ngrok](../doc-links/debug.md#locally-hosted) para que Microsoft Teams pueda acceder a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-137">[Set up a secure tunnel with ngrok](../doc-links/debug.md#locally-hosted) so that Teams can access your app.</span></span> <span data-ttu-id="2ff2e-138">(Instalar [ngrok](https://ngrok.com/download)).</span><span class="sxs-lookup"><span data-stu-id="2ff2e-138">(Install [ngrok](https://ngrok.com/download).)</span></span>
* <span data-ttu-id="2ff2e-139">[Transfiera localmente la aplicación](../doc-links/apps-upload.md) en el cliente de Microsoft Teams usando el `Development.zip` de la `.publish` carpeta.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-139">[Sideload your app](../doc-links/apps-upload.md) in the Teams client using the `Development.zip` in the `.publish` folder.</span></span>

<span data-ttu-id="2ff2e-140">Después de transferir localmente la aplicación, debe tener este aspecto en el cliente de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-140">Once you sideload your app, it should look like this in the Teams client.</span></span>

![Ficha de ejemplo Hello World](../doc-links/images/tab-running.png)

## <a name="important-app-project-files"></a><span data-ttu-id="2ff2e-142">Archivos de proyecto de aplicación importantes</span><span class="sxs-lookup"><span data-stu-id="2ff2e-142">Important app project files</span></span>

<span data-ttu-id="2ff2e-143">Con el proyecto de la aplicación y la configuración de scaffolding, dedique algún tiempo a comprender algunos de los archivos clave en los que trabajan los desarrolladores de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-143">With your app project and scaffolding set up, take some time to understand some of the key files Teams app developers work with.</span></span>

### <a name="app-manifest-manifestjson"></a><span data-ttu-id="2ff2e-144">Manifiesto de la aplicación ( `manifest.json` )</span><span class="sxs-lookup"><span data-stu-id="2ff2e-144">App manifest (`manifest.json`)</span></span>

<span data-ttu-id="2ff2e-145">Ubicado en el `.publish` directorio, el manifiesto de la aplicación es el punto de partida para cualquier proyecto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-145">Located in the `.publish` directory, the app manifest is the starting point for any app project.</span></span> <span data-ttu-id="2ff2e-146">El manifiesto define los atributos fundamentales de la aplicación y apunta a los recursos necesarios.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-146">The manifest defines your app's fundamental attributes and points to required resources.</span></span> <span data-ttu-id="2ff2e-147">Al instalar una aplicación, Microsoft Teams analiza el manifiesto para comprender cómo representar la aplicación en el cliente.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-147">When you install an app, Teams parses the manifest to understand how to render your app in the client.</span></span>

<span data-ttu-id="2ff2e-148">En los siguientes tutoriales, nos centraremos en las secciones del manifiesto de la aplicación para crear pestañas personales y de canal.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-148">In the following tutorials, you'll focus on the sections of the app manifest for building personal and channel tabs.</span></span>

### <a name="package-developmentzip"></a><span data-ttu-id="2ff2e-149">Package ( `Development.zip` )</span><span class="sxs-lookup"><span data-stu-id="2ff2e-149">Package (`Development.zip`)</span></span>

<span data-ttu-id="2ff2e-150">También se encuentra en el `.publish` directorio, necesita el paquete de la aplicación para [transferir localmente la aplicación](../../overview.md#how-can-you-share-your-teams-app) en Teams.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-150">Also located in the `.publish` directory, you need the app package to [sideload your app](../../overview.md#how-can-you-share-your-teams-app) in Teams.</span></span> <span data-ttu-id="2ff2e-151">También se usa cuando se [publica en el catálogo de aplicaciones de la organización](../../overview.md#how-can-you-share-your-teams-app) o [AppSource](../../concepts/deploy-and-publish/appsource/publish.md).</span><span class="sxs-lookup"><span data-stu-id="2ff2e-151">It's also used when [publishing to your organization's app catalog](../../overview.md#how-can-you-share-your-teams-app) or [AppSource](../../concepts/deploy-and-publish/appsource/publish.md).</span></span>

<span data-ttu-id="2ff2e-152">Estos son algunos detalles sobre los archivos del paquete de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="2ff2e-152">Here are some details about the app package files:</span></span>

|<span data-ttu-id="2ff2e-153">Nombre</span><span class="sxs-lookup"><span data-stu-id="2ff2e-153">Name</span></span>|<span data-ttu-id="2ff2e-154">Tipo</span><span class="sxs-lookup"><span data-stu-id="2ff2e-154">Type</span></span>|<span data-ttu-id="2ff2e-155">Size</span><span class="sxs-lookup"><span data-stu-id="2ff2e-155">Size</span></span>|<span data-ttu-id="2ff2e-156">Ubicación del manifiesto</span><span class="sxs-lookup"><span data-stu-id="2ff2e-156">Manifest location</span></span>|<span data-ttu-id="2ff2e-157">Nombre de archivo Toolkit</span><span class="sxs-lookup"><span data-stu-id="2ff2e-157">Toolkit filename</span></span>|
|---|---|:---:|:---:|-----|
|<span data-ttu-id="2ff2e-158">**Manifiesto de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="2ff2e-158">**App manifest**</span></span>|`.json`| <span data-ttu-id="2ff2e-159">—</span><span class="sxs-lookup"><span data-stu-id="2ff2e-159">—</span></span> | <span data-ttu-id="2ff2e-160">—</span><span class="sxs-lookup"><span data-stu-id="2ff2e-160">—</span></span> |`.publish/manifest.json`|
|<span data-ttu-id="2ff2e-161">**Logotipo-color**</span><span class="sxs-lookup"><span data-stu-id="2ff2e-161">**Color logo**</span></span>|`.png`|<span data-ttu-id="2ff2e-162">192 &times; 192 píxeles</span><span class="sxs-lookup"><span data-stu-id="2ff2e-162">192&times;192 pixels</span></span>|`icon.color`|`.publish/color.png`|
|<span data-ttu-id="2ff2e-163">**Logotipo de contorno**</span><span class="sxs-lookup"><span data-stu-id="2ff2e-163">**Outline logo**</span></span>|`.png`|<span data-ttu-id="2ff2e-164">32 &times; 32 píxeles</span><span class="sxs-lookup"><span data-stu-id="2ff2e-164">32&times;32 pixels</span></span>|`icon.outline`|`.publish/outline.png`|

### <a name="scaffolding-src"></a><span data-ttu-id="2ff2e-165">Scaffolding ( `src` )</span><span class="sxs-lookup"><span data-stu-id="2ff2e-165">Scaffolding (`src`)</span></span>

<span data-ttu-id="2ff2e-166">El kit de herramientas crea automáticamente scaffolding en el `src` directorio en función de las funciones que agregó durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-166">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="2ff2e-167">Aunque algunos archivos se crean sin importar el tipo de aplicación que tenga.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-167">Some files are created no matter what kind of app you have, though.</span></span> <span data-ttu-id="2ff2e-168">Por ejemplo, el `App.js` archivo en el `src/components` directorio es importante porque controla la inicialización y el enrutamiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-168">For example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="2ff2e-169">Lo más importante es que llama al [SDK de Microsoft Teams](../doc-links/using-teams-client-sdk.md) para establecer la comunicación entre la aplicación y los equipos.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-169">Most importantly, it calls the [Microsoft Teams SDK](../doc-links/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

<span data-ttu-id="2ff2e-170">Puede obtener más información sobre la técnica de scaffolding en los tutoriales para crear pestañas personales y de canal.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-170">You can learn more about scaffolding in the tutorials for creating personal and channel tabs.</span></span>

## <a name="next-step"></a><span data-ttu-id="2ff2e-171">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="2ff2e-171">Next step</span></span>

<span data-ttu-id="2ff2e-172">¡ Felicidades 🎉!</span><span class="sxs-lookup"><span data-stu-id="2ff2e-172">🎉 Congratulations!</span></span> <span data-ttu-id="2ff2e-173">Tiene una aplicación de Teams en ejecución.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-173">You have a running Teams app.</span></span> <span data-ttu-id="2ff2e-174">Seleccione el siguiente botón para obtener información sobre cómo agregar una característica real al mismo.</span><span class="sxs-lookup"><span data-stu-id="2ff2e-174">Select the following button to learn how to add a real-world feature to it.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2ff2e-175">Crear una pestaña personal</span><span class="sxs-lookup"><span data-stu-id="2ff2e-175">Build a personal tab</span></span>](add-personal-tab.md)

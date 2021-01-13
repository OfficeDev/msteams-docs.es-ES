---
title: 'Introducción: crear la primera introducción a la aplicación y los requisitos previos'
author: heath-hamilton
description: Obtenga información sobre cómo empezar a desarrollar aplicaciones de Microsoft Teams y configurar su entorno.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 4288efdbfada5f1a51fa1d4aeccdd6cdf9c64382
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797900"
---
# <a name="build-your-first-microsoft-teams-app-overview"></a><span data-ttu-id="0bcdc-103">Crear la primera introducción a la aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0bcdc-103">Build your first Microsoft Teams app overview</span></span>

<span data-ttu-id="0bcdc-104">En las **lecciones de introducción,** aprenderá a crear aplicaciones básicas de Teams.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-104">In the **get started** lessons, you learn how to create basic Teams apps.</span></span> <span data-ttu-id="0bcdc-105">Cada tutorial le guiará a través de cómo crear una aplicación de Teams sencilla y real, a la vez que le presenta herramientas comunes, conceptos fundamentales y características más avanzadas.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-105">Each tutorial walks through how to build a simple, real-world Teams app while introducing you to common tools, fundamental concepts, and more advanced features.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="0bcdc-106">Lo que aprenderás</span><span class="sxs-lookup"><span data-stu-id="0bcdc-106">What you'll learn</span></span>

<span data-ttu-id="0bcdc-107">Esta es una idea de lo que sabrá después de pasar por las lecciones.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-107">Here's an idea of what you'll know after going through the lessons.</span></span>

> [!div class="checklist"]
  >
  > * <span data-ttu-id="0bcdc-108">Empezar a trabajar rápidamente con el kit de herramientas de **Teams:** Microsoft Teams Toolkit para Visual Studio Code se encarga de crear el proyecto de aplicación y el scaffolding para que pueda tener una aplicación en ejecución en minutos.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-108">**Get up and running quickly with the Teams Toolkit**: The Microsoft Teams Toolkit for Visual Studio Code takes care of creating your app project and scaffolding so you can have a running app in minutes.</span></span>
  > * <span data-ttu-id="0bcdc-109">**Configurar la aplicación con App Studio:** especifique las funcionalidades y los servicios que usa la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-109">**Configure your app with App Studio**: Specify the capabilities and services your Teams app uses.</span></span>
  > * <span data-ttu-id="0bcdc-110">**Ámbito de la audiencia de la aplicación:** cree una aplicación de Teams para uso personal, colaboración o ambos.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-110">**Scope your app's audience**: Build a Teams app for personal use, collaboration, or both.</span></span>
> * <span data-ttu-id="0bcdc-111">**Obtenga experiencia con las herramientas y SDK de Teams:** personalice su aplicación con la ayuda del SDK del cliente de JavaScript de Teams.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-111">**Get experience with Teams tools and SDKs**: Customize your app with help from the Teams JavaScript client SDK.</span></span> <span data-ttu-id="0bcdc-112">Por ejemplo, cambie la combinación de colores de la aplicación para que coincida con el tema de Teams.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-112">For example, change your app's color scheme to match the Teams theme.</span></span> <span data-ttu-id="0bcdc-113">Además, obtenga información sobre las herramientas comunes para crear y administrar bots.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-113">Also, learn about common tools for creating and managing bots.</span></span>
  > * <span data-ttu-id="0bcdc-114">**Expande tu aplicación:** a lo largo de las lecciones, encontrarás temas relacionados que probablemente te interesen (como las directrices de autenticación y diseño).</span><span class="sxs-lookup"><span data-stu-id="0bcdc-114">**Expand on your app**: Throughout the lessons, you'll find related topics you're probably interested in (such as authentication and design guidelines).</span></span>

## <a name="teams-app-fundamentals"></a><span data-ttu-id="0bcdc-115">Aspectos básicos de la aplicación de Teams</span><span class="sxs-lookup"><span data-stu-id="0bcdc-115">Teams app fundamentals</span></span>

<span data-ttu-id="0bcdc-116">Antes de comenzar los tutoriales, debe saber lo siguiente sobre la creación de aplicaciones para Teams.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-116">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a><span data-ttu-id="0bcdc-117">Las aplicaciones pueden tener varias funcionalidades y puntos de entrada</span><span class="sxs-lookup"><span data-stu-id="0bcdc-117">Apps can have multiple capabilities and entry points</span></span>

<span data-ttu-id="0bcdc-118">Una aplicación de Teams está integrada por una o más funcionalidades de plataforma [(cómo](../concepts/capabilities-overview.md) la gente usa la aplicación) y puntos de entrada [(donde](../concepts/extensibility-points.md) las personas usan la aplicación).</span><span class="sxs-lookup"><span data-stu-id="0bcdc-118">A Teams app is made up of one or more [platform capabilities](../concepts/capabilities-overview.md) (how people use the app) and [entry points](../concepts/extensibility-points.md) (where people use the app).</span></span>

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="0bcdc-119">Teams no hospeda la aplicación</span><span class="sxs-lookup"><span data-stu-id="0bcdc-119">Teams doesn't host your app</span></span>

<span data-ttu-id="0bcdc-120">Una aplicación de Teams incluye las siguientes partes importantes:</span><span class="sxs-lookup"><span data-stu-id="0bcdc-120">A Teams app includes the following important pieces:</span></span>

* <span data-ttu-id="0bcdc-121">La lógica, el almacenamiento de datos y las llamadas API que potencian la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-121">The logic, data storage, and API calls that power your app.</span></span> <span data-ttu-id="0bcdc-122">Estos servicios no se hospedan en Teams y deben ser accesibles a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-122">These services are not hosted by Teams and must be accessible via HTTPS.</span></span>
* <span data-ttu-id="0bcdc-123">El cliente de Teams (web, de escritorio o móvil) donde los usuarios usan la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-123">The Teams client (web, desktop, or mobile) where people use your app.</span></span>
* <span data-ttu-id="0bcdc-124">El id. de la aplicación, que te permite configurar la aplicación con App Studio.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-124">Your app ID, which lets you configure your app with App Studio.</span></span>

## <a name="get-prerequisites"></a><span data-ttu-id="0bcdc-125">Obtener requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0bcdc-125">Get prerequisites</span></span>

<span data-ttu-id="0bcdc-126">Compruebe que tiene la cuenta adecuada para crear aplicaciones de Teams e instalar algunas herramientas de desarrollo recomendadas.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-126">Verify you have the right account for building Teams apps and install some recommended development tools.</span></span>

### <a name="set-up-your-development-account"></a><span data-ttu-id="0bcdc-127">Configurar la cuenta de desarrollo</span><span class="sxs-lookup"><span data-stu-id="0bcdc-127">Set up your development account</span></span>

<span data-ttu-id="0bcdc-128">Necesita una cuenta de Teams que permita la instalación de prueba de aplicaciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-128">You need a Teams account that allows custom app sideloading.</span></span> <span data-ttu-id="0bcdc-129">(Es posible que su cuenta ya lo proporcione).</span><span class="sxs-lookup"><span data-stu-id="0bcdc-129">(Your account may already provide this.)</span></span>

1. <span data-ttu-id="0bcdc-130">Si tiene una cuenta de Teams, compruebe si puede realizar la instalación de instalación de local de aplicaciones en Teams:</span><span class="sxs-lookup"><span data-stu-id="0bcdc-130">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="0bcdc-131">En el cliente de Teams, seleccione **Aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="0bcdc-131">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="0bcdc-132">Busque una opción para **cargar una aplicación personalizada.**</span><span class="sxs-lookup"><span data-stu-id="0bcdc-132">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Ilustración que muestra dónde puede cargar una aplicación personalizada en Teams.":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><span data-ttu-id="0bcdc-134"><b>Seleccione esta</b> opción si no puede ver la opción de instalación de local o si no tiene una cuenta de Teams.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-134"><b>Select here</b> if you can't see the sideload option or don't have a Teams account.</span></span></summary>

<span data-ttu-id="0bcdc-135">Puede obtener una cuenta de prueba gratuita de Teams que permita la instalación de prueba de aplicaciones uniéndose al programa de desarrolladores de Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-135">You can get a free Teams test account that allows app sideloading by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="0bcdc-136">(El proceso de registro tarda aproximadamente dos minutos).</span><span class="sxs-lookup"><span data-stu-id="0bcdc-136">(The registration process takes approximately two minutes.)</span></span>

1. <span data-ttu-id="0bcdc-137">Vaya al programa de desarrolladores de [Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="0bcdc-137">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="0bcdc-138">Seleccione **Unirse ahora** y siga las instrucciones en pantalla.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-138">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="0bcdc-139">Cuando llegue a la pantalla de bienvenida, seleccione **Configurar suscripción E5.**</span><span class="sxs-lookup"><span data-stu-id="0bcdc-139">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="0bcdc-140">Configure su cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-140">Set up your administrator account.</span></span> <span data-ttu-id="0bcdc-141">Una vez que termines, deberías ver una pantalla como esta.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-141">Once you finish, you should see a screen like this.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Ejemplo de lo que ve después de registrarse en el programa de desarrolladores de Microsoft 365.":::
1. <span data-ttu-id="0bcdc-143">Inicie sesión en Teams con la cuenta de administrador que acaba de configurar.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-143">Log in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="0bcdc-144">Comprueba si ahora tienes la opción **Cargar una aplicación** personalizada.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-144">Verify if you now have the **Upload a custom app** option.</span></span>

</details>

> [!Note]
> <span data-ttu-id="0bcdc-145">Si sigue sin poder realizar la instalación de instalación local de aplicaciones, vea habilitar aplicaciones personalizadas de Teams y activar la carga [de aplicaciones personalizadas.](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)</span><span class="sxs-lookup"><span data-stu-id="0bcdc-145">If you still can't sideload apps, see [enable custom Teams apps and turn on custom app uploading](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).</span></span>

### <a name="install-your-development-tools"></a><span data-ttu-id="0bcdc-146">Instalar las herramientas de desarrollo</span><span class="sxs-lookup"><span data-stu-id="0bcdc-146">Install your development tools</span></span>

<span data-ttu-id="0bcdc-147">Puede crear aplicaciones de Teams con sus herramientas preferidas, pero estas lecciones muestran cómo puede empezar rápidamente con Microsoft Teams Toolkit for Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-147">You can build Teams apps with your preferred tools, but these lessons show how you can get started quickly with the Microsoft Teams Toolkit for Visual Studio Code.</span></span>

<span data-ttu-id="0bcdc-148">Teams muestra el contenido de la aplicación solo a través de conexiones HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-148">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="0bcdc-149">Para depurar determinados tipos de aplicaciones localmente, como un bot, aprenderá a usar [ngrok](../concepts/build-and-test/debug.md#locally-hosted) para configurar un túnel seguro entre Teams y su aplicación.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-149">To debug certain types of apps locally, such as a bot, you'll learn how to use [ngrok to set up a secure tunnel](../concepts/build-and-test/debug.md#locally-hosted) between Teams and your app.</span></span> <span data-ttu-id="0bcdc-150">(Las aplicaciones de Teams de producción se hospedan en la nube).</span><span class="sxs-lookup"><span data-stu-id="0bcdc-150">(Production Teams apps are hosted in the cloud.)</span></span>

1. <span data-ttu-id="0bcdc-151">Instale [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="0bcdc-151">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="0bcdc-152">Instale [ngrok](https://ngrok.com/download) si tiene previsto crear un bot o una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-152">Install [ngrok](https://ngrok.com/download) if you plan to build a bot or messaging extension.</span></span>
1. <span data-ttu-id="0bcdc-153">Instale la versión más reciente [de Visual Studio código.](https://code.visualstudio.com/download)</span><span class="sxs-lookup"><span data-stu-id="0bcdc-153">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> <span data-ttu-id="0bcdc-154">(Es posible que las versiones anteriores no funcionen con el kit de herramientas).</span><span class="sxs-lookup"><span data-stu-id="0bcdc-154">(Earlier versions might not work with the toolkit.)</span></span>
1. En Visual Studio, seleccione **Extensiones** en la barra de actividades de la :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: izquierda e instale Microsoft Teams **Toolkit.**

    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Ilustración que muestra dónde en Visual Studio código puede instalar la extensión de Microsoft Teams Toolkit.":::

## <a name="about-the-tutorials"></a><span data-ttu-id="0bcdc-157">Acerca de los tutoriales</span><span class="sxs-lookup"><span data-stu-id="0bcdc-157">About the tutorials</span></span>

<span data-ttu-id="0bcdc-158">Puede empezar con cualquiera de las lecciones de **introducción a** Teams.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-158">You can start with any of the Teams **get started** lessons.</span></span> <span data-ttu-id="0bcdc-159">Si no estás seguro de dónde ir primero, sigue nuestra ruta de acceso fácil para principiantes y crea un "Hello, World!".</span><span class="sxs-lookup"><span data-stu-id="0bcdc-159">If you're not sure where to go first, follow our beginner friendly path and build a "Hello, World!"</span></span> <span data-ttu-id="0bcdc-160">app.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-160">app.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="Árbol de aptitudes que muestra las rutas de aprendizaje para las lecciones de &quot;introducción&quot; de Teams." border="false":::

## <a name="next-step"></a><span data-ttu-id="0bcdc-162">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="0bcdc-162">Next step</span></span>

<span data-ttu-id="0bcdc-163">Una vez configurada la cuenta y el entorno, puede empezar a crear.</span><span class="sxs-lookup"><span data-stu-id="0bcdc-163">Once you set up your account and environment, you can start building.</span></span>

### <a name="beginner-friendly-tutorial"></a><span data-ttu-id="0bcdc-164">Tutorial descriptivo para principiantes</span><span class="sxs-lookup"><span data-stu-id="0bcdc-164">Beginner friendly tutorial</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0bcdc-165">Crear una aplicación "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="0bcdc-165">Build a "Hello, World!" app</span></span>](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a><span data-ttu-id="0bcdc-166">Otros tutoriales</span><span class="sxs-lookup"><span data-stu-id="0bcdc-166">Other tutorials</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0bcdc-167">Crear un bot</span><span class="sxs-lookup"><span data-stu-id="0bcdc-167">Build a bot</span></span>](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="0bcdc-168">Crear una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="0bcdc-168">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)

---
title: 'Introducción: crear la primera introducción a la aplicación y los requisitos previos'
author: heath-hamilton
description: Obtén información sobre cómo empezar con el desarrollo de aplicaciones de Microsoft Teams y cómo configurar el entorno.
ms.author: lajanuar
localization_priority: Normal
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: d975383022089579a04317de73595106e7920c56
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019996"
---
# <a name="build-your-first-microsoft-teams-app-overview"></a><span data-ttu-id="e34ee-103">Crear la primera introducción a la aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e34ee-103">Build your first Microsoft Teams app overview</span></span>

<span data-ttu-id="e34ee-104">En las **lecciones de introducción,** aprenderás a crear aplicaciones básicas de Teams.</span><span class="sxs-lookup"><span data-stu-id="e34ee-104">In the **get started** lessons, you learn how to create basic Teams apps.</span></span> <span data-ttu-id="e34ee-105">Cada tutorial explica cómo crear una aplicación de Teams sencilla y real al mismo tiempo que te presenta herramientas comunes, conceptos fundamentales y características más avanzadas.</span><span class="sxs-lookup"><span data-stu-id="e34ee-105">Each tutorial walks through how to build a simple, real-world Teams app while introducing you to common tools, fundamental concepts, and more advanced features.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="e34ee-106">Lo que aprenderás</span><span class="sxs-lookup"><span data-stu-id="e34ee-106">What you'll learn</span></span>

<span data-ttu-id="e34ee-107">Esta es una idea de lo que sabrá después de pasar por las lecciones.</span><span class="sxs-lookup"><span data-stu-id="e34ee-107">Here's an idea of what you'll know after going through the lessons.</span></span>

> [!div class="checklist"]
  >
  > * <span data-ttu-id="e34ee-108">Descárgase y ejecutándose rápidamente con **Teams Toolkit:** Microsoft Teams Toolkit for Visual Studio Code se encarga de crear el proyecto de aplicación y el scaffolding para que pueda tener una aplicación en ejecución en minutos.</span><span class="sxs-lookup"><span data-stu-id="e34ee-108">**Get up and running quickly with the Teams Toolkit**: The Microsoft Teams Toolkit for Visual Studio Code takes care of creating your app project and scaffolding so you can have a running app in minutes.</span></span>
  > * <span data-ttu-id="e34ee-109">**Configurar la aplicación con App Studio:** especifica las funcionalidades y los servicios que usa la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="e34ee-109">**Configure your app with App Studio**: Specify the capabilities and services your Teams app uses.</span></span>
  > * <span data-ttu-id="e34ee-110">**Ámbito de la audiencia de la aplicación:** crear una aplicación de Teams para uso personal, colaboración o ambos.</span><span class="sxs-lookup"><span data-stu-id="e34ee-110">**Scope your app's audience**: Build a Teams app for personal use, collaboration, or both.</span></span>
> * <span data-ttu-id="e34ee-111">**Obtenga experiencia con las herramientas y SDK** de Teams: personalice la aplicación con la ayuda del SDK de cliente de JavaScript de Teams.</span><span class="sxs-lookup"><span data-stu-id="e34ee-111">**Get experience with Teams tools and SDKs**: Customize your app with help from the Teams JavaScript client SDK.</span></span> <span data-ttu-id="e34ee-112">Por ejemplo, cambia la combinación de colores de la aplicación para que coincida con el tema de Teams.</span><span class="sxs-lookup"><span data-stu-id="e34ee-112">For example, change your app's color scheme to match the Teams theme.</span></span> <span data-ttu-id="e34ee-113">Además, obtenga información sobre las herramientas comunes para crear y administrar bots.</span><span class="sxs-lookup"><span data-stu-id="e34ee-113">Also, learn about common tools for creating and managing bots.</span></span>
  > * <span data-ttu-id="e34ee-114">**Expande tu aplicación:** a lo largo de las lecciones, encontrarás temas relacionados que probablemente te interesen (como la autenticación y las directrices de diseño).</span><span class="sxs-lookup"><span data-stu-id="e34ee-114">**Expand on your app**: Throughout the lessons, you'll find related topics you're probably interested in (such as authentication and design guidelines).</span></span>

## <a name="teams-app-fundamentals"></a><span data-ttu-id="e34ee-115">Conceptos básicos de la aplicación de Teams</span><span class="sxs-lookup"><span data-stu-id="e34ee-115">Teams app fundamentals</span></span>

<span data-ttu-id="e34ee-116">Antes de comenzar los tutoriales, debes saber lo siguiente sobre cómo crear aplicaciones para Teams.</span><span class="sxs-lookup"><span data-stu-id="e34ee-116">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a><span data-ttu-id="e34ee-117">Las aplicaciones pueden tener varias funcionalidades y puntos de entrada</span><span class="sxs-lookup"><span data-stu-id="e34ee-117">Apps can have multiple capabilities and entry points</span></span>

<span data-ttu-id="e34ee-118">Una aplicación de Teams está integrada por una o más funcionalidades de plataforma [(cómo](../concepts/capabilities-overview.md) usan las personas la aplicación) y puntos de entrada [(donde](../concepts/extensibility-points.md) las personas usan la aplicación).</span><span class="sxs-lookup"><span data-stu-id="e34ee-118">A Teams app is made up of one or more [platform capabilities](../concepts/capabilities-overview.md) (how people use the app) and [entry points](../concepts/extensibility-points.md) (where people use the app).</span></span>

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="e34ee-119">Teams no hospeda la aplicación</span><span class="sxs-lookup"><span data-stu-id="e34ee-119">Teams doesn't host your app</span></span>

<span data-ttu-id="e34ee-120">Una aplicación de Teams incluye las siguientes partes importantes:</span><span class="sxs-lookup"><span data-stu-id="e34ee-120">A Teams app includes the following important pieces:</span></span>

* <span data-ttu-id="e34ee-121">La lógica, el almacenamiento de datos y las llamadas API que potencian la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e34ee-121">The logic, data storage, and API calls that power your app.</span></span> <span data-ttu-id="e34ee-122">Teams no hospeda estos servicios y deben ser accesibles a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e34ee-122">These services are not hosted by Teams and must be accessible via HTTPS.</span></span>
* <span data-ttu-id="e34ee-123">El cliente de Teams (web, de escritorio o móvil) donde los usuarios usan la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e34ee-123">The Teams client (web, desktop, or mobile) where people use your app.</span></span>
* <span data-ttu-id="e34ee-124">El identificador de la aplicación, que te permite configurar la aplicación con App Studio.</span><span class="sxs-lookup"><span data-stu-id="e34ee-124">Your app ID, which lets you configure your app with App Studio.</span></span>

## <a name="get-prerequisites"></a><span data-ttu-id="e34ee-125">Obtener requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e34ee-125">Get prerequisites</span></span>

<span data-ttu-id="e34ee-126">Comprueba que tienes la cuenta adecuada para crear aplicaciones de Teams e instalar algunas herramientas de desarrollo recomendadas.</span><span class="sxs-lookup"><span data-stu-id="e34ee-126">Verify you have the right account for building Teams apps and install some recommended development tools.</span></span>

### <a name="set-up-your-development-account"></a><span data-ttu-id="e34ee-127">Configurar la cuenta de desarrollo</span><span class="sxs-lookup"><span data-stu-id="e34ee-127">Set up your development account</span></span>

<span data-ttu-id="e34ee-128">Necesitas una cuenta de Teams que permita la instalación local de aplicaciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="e34ee-128">You need a Teams account that allows custom app sideloading.</span></span> <span data-ttu-id="e34ee-129">(Es posible que su cuenta ya lo proporcione).</span><span class="sxs-lookup"><span data-stu-id="e34ee-129">(Your account may already provide this.)</span></span>

1. <span data-ttu-id="e34ee-130">Si tienes una cuenta de Teams, comprueba si puedes realizar la instalación local de aplicaciones en Teams:</span><span class="sxs-lookup"><span data-stu-id="e34ee-130">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="e34ee-131">En el cliente de Teams, seleccione **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e34ee-131">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="e34ee-132">Busque una opción para **Cargar una aplicación personalizada.**</span><span class="sxs-lookup"><span data-stu-id="e34ee-132">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Ilustración que muestra dónde se puede cargar una aplicación personalizada en Teams.":::
    
    <span data-ttu-id="e34ee-134">Si no ves el botón, no tienes permiso para cargar aplicaciones personalizadas en tu organización. Puedes obtener esta característica al suscribirte a una suscripción gratuita para desarrolladores de Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="e34ee-134">If you don't see the button, you don't have permission to upload custom apps in your org. You can get this feature by signing up for a free Microsoft 365 developer subscription.</span></span>

<!-- markdownlint-disable MD033 -->
<details>

<summary><span data-ttu-id="e34ee-135"><b>Obtener la suscripción gratuita para desarrolladores de Microsoft 365</b></span><span class="sxs-lookup"><span data-stu-id="e34ee-135"><b>Get your free Microsoft 365 developer subscription</b></span></span></summary>

<span data-ttu-id="e34ee-136">Puedes obtener una cuenta de prueba gratuita de Teams que permite la instalación local de aplicaciones uniéndose al programa para desarrolladores de Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="e34ee-136">You can get a free Teams test account that allows app sideloading by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="e34ee-137">(El proceso de registro tarda aproximadamente dos minutos).</span><span class="sxs-lookup"><span data-stu-id="e34ee-137">(The registration process takes approximately two minutes.)</span></span>

1. <span data-ttu-id="e34ee-138">Vaya al programa para desarrolladores de [Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).</span><span class="sxs-lookup"><span data-stu-id="e34ee-138">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="e34ee-139">Selecciona **Unirse ahora** y sigue las instrucciones en pantalla.</span><span class="sxs-lookup"><span data-stu-id="e34ee-139">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="e34ee-140">Cuando llegue a la pantalla de bienvenida, seleccione **Configurar la suscripción de E5**.</span><span class="sxs-lookup"><span data-stu-id="e34ee-140">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="e34ee-141">Configurar la cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="e34ee-141">Set up your administrator account.</span></span> <span data-ttu-id="e34ee-142">Una vez que termines, deberías ver una pantalla como esta.</span><span class="sxs-lookup"><span data-stu-id="e34ee-142">Once you finish, you should see a screen like this.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Ejemplo de lo que ve después de registrarse en el programa para desarrolladores de Microsoft 365.":::
1. <span data-ttu-id="e34ee-144">Inicie sesión en Teams con la cuenta de administrador que acaba de configurar.</span><span class="sxs-lookup"><span data-stu-id="e34ee-144">Log in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="e34ee-145">Comprueba si ahora tienes la opción **Cargar una aplicación** personalizada.</span><span class="sxs-lookup"><span data-stu-id="e34ee-145">Verify if you now have the **Upload a custom app** option.</span></span>

</details>

> [!Note]
> <span data-ttu-id="e34ee-146">Si aún no puedes realizar la instalación local de aplicaciones, consulta Habilitar aplicaciones personalizadas de Teams y activar la carga [de aplicaciones personalizadas.](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)</span><span class="sxs-lookup"><span data-stu-id="e34ee-146">If you still can't sideload apps, see [enable custom Teams apps and turn on custom app uploading](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).</span></span>

### <a name="install-your-development-tools"></a><span data-ttu-id="e34ee-147">Instalar las herramientas de desarrollo</span><span class="sxs-lookup"><span data-stu-id="e34ee-147">Install your development tools</span></span>

<span data-ttu-id="e34ee-148">Puedes crear aplicaciones de Teams con tus herramientas preferidas, pero estas lecciones muestran cómo puedes empezar rápidamente con Microsoft Teams Toolkit for Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e34ee-148">You can build Teams apps with your preferred tools, but these lessons show how you can get started quickly with the Microsoft Teams Toolkit for Visual Studio Code.</span></span>

<span data-ttu-id="e34ee-149">Teams muestra el contenido de la aplicación solo a través de conexiones HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e34ee-149">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="e34ee-150">Para depurar ciertos tipos de aplicaciones localmente, como un bot, aprenderás a usar [ngrok](../concepts/build-and-test/debug.md#locally-hosted) para configurar un túnel seguro entre Teams y tu aplicación.</span><span class="sxs-lookup"><span data-stu-id="e34ee-150">To debug certain types of apps locally, such as a bot, you'll learn how to use [ngrok to set up a secure tunnel](../concepts/build-and-test/debug.md#locally-hosted) between Teams and your app.</span></span> <span data-ttu-id="e34ee-151">(Las aplicaciones de Production Teams se hospedan en la nube).</span><span class="sxs-lookup"><span data-stu-id="e34ee-151">(Production Teams apps are hosted in the cloud.)</span></span>

1. <span data-ttu-id="e34ee-152">Instale [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="e34ee-152">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="e34ee-153">Instale [ngrok](https://ngrok.com/download) si está creando un bot o una extensión de mensajería y [cree un túnel con ngrok](https://docs.microsoft.com/microsoftteams/platform/tutorials/get-started-dotnet-app-studio#tunnel-using-ngrok).</span><span class="sxs-lookup"><span data-stu-id="e34ee-153">Install [ngrok](https://ngrok.com/download) if you are building a bot or messaging extension and [create a tunnel using ngrok](https://docs.microsoft.com/microsoftteams/platform/tutorials/get-started-dotnet-app-studio#tunnel-using-ngrok).</span></span>
1. <span data-ttu-id="e34ee-154">Instale la versión más reciente [de Visual Studio Code](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="e34ee-154">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> <span data-ttu-id="e34ee-155">(Es posible que las versiones anteriores no funcionen con el kit de herramientas).</span><span class="sxs-lookup"><span data-stu-id="e34ee-155">(Earlier versions might not work with the toolkit.)</span></span>
1. En Visual Studio, seleccione **Extensiones en** la barra de actividades izquierda e instale Microsoft :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: Teams **Toolkit**.

    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Ilustración que muestra dónde en Visual Studio código puede instalar la extensión microsoft Teams Toolkit.":::

## <a name="about-the-tutorials"></a><span data-ttu-id="e34ee-158">Acerca de los tutoriales</span><span class="sxs-lookup"><span data-stu-id="e34ee-158">About the tutorials</span></span>

<span data-ttu-id="e34ee-159">Puedes empezar con cualquiera de las lecciones de introducción **de** Teams.</span><span class="sxs-lookup"><span data-stu-id="e34ee-159">You can start with any of the Teams **get started** lessons.</span></span> <span data-ttu-id="e34ee-160">Si no estás seguro de dónde ir primero, sigue nuestra ruta de acceso fácil para principiantes y crea un "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="e34ee-160">If you're not sure where to go first, follow our beginner friendly path and build a "Hello, World!"</span></span> <span data-ttu-id="e34ee-161">app.</span><span class="sxs-lookup"><span data-stu-id="e34ee-161">app.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="Árbol de aptitudes que muestra rutas de aprendizaje para las lecciones de &quot;introducción&quot; de Teams." border="false":::

## <a name="next-step"></a><span data-ttu-id="e34ee-163">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="e34ee-163">Next step</span></span>

<span data-ttu-id="e34ee-164">Una vez configurada la cuenta y el entorno, puede empezar a compilar.</span><span class="sxs-lookup"><span data-stu-id="e34ee-164">Once you set up your account and environment, you can start building.</span></span>

### <a name="beginner-friendly-tutorial"></a><span data-ttu-id="e34ee-165">Tutorial descriptivo para principiantes</span><span class="sxs-lookup"><span data-stu-id="e34ee-165">Beginner friendly tutorial</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e34ee-166">Crear una aplicación "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="e34ee-166">Build a "Hello, World!" app</span></span>](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a><span data-ttu-id="e34ee-167">Otros tutoriales</span><span class="sxs-lookup"><span data-stu-id="e34ee-167">Other tutorials</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e34ee-168">Crear un bot</span><span class="sxs-lookup"><span data-stu-id="e34ee-168">Build a bot</span></span>](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="e34ee-169">Crear una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="e34ee-169">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)

---
title: 'Introducción: compilar la primera introducción a la aplicación y requisitos previos'
author: heath-hamilton
description: Obtenga información sobre cómo empezar a trabajar con el desarrollo de aplicaciones de Microsoft Teams y configurar el entorno.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: e2e73e755c45fa3bff3b6320dfbf0999a575fe99
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346815"
---
# <a name="build-your-first-microsoft-teams-app-overview"></a><span data-ttu-id="058fe-103">Crear su primera información general de la aplicación Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="058fe-103">Build your first Microsoft Teams app overview</span></span>

<span data-ttu-id="058fe-104">En la lección **compilar la primera aplicación** , puede crear aplicaciones básicas de Teams.</span><span class="sxs-lookup"><span data-stu-id="058fe-104">In the **build your first app** lessons, you create basic Teams apps.</span></span> <span data-ttu-id="058fe-105">En cada tutorial se explica cómo crear una aplicación sencilla y real de Teams, a la vez que se presentan herramientas comunes, conceptos fundamentales y características más avanzadas.</span><span class="sxs-lookup"><span data-stu-id="058fe-105">Each tutorial walks through how to build a simple, real-world Teams app while introducing you to common tools, fundamental concepts, and more advanced features.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="058fe-106">Qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="058fe-106">What you'll learn</span></span>

<span data-ttu-id="058fe-107">Esta es una idea de lo que sabrá después de pasar por las lecciones.</span><span class="sxs-lookup"><span data-stu-id="058fe-107">Here's an idea of what you'll know after going through the lessons.</span></span>

> [!div class="checklist"]
  >
  > * <span data-ttu-id="058fe-108">**Póngase en marcha rápidamente con Team Toolkit**: el kit de herramientas de Microsoft Teams para Visual Studio Code se encarga de crear el proyecto de la aplicación y el scaffolding para que pueda tener una aplicación en ejecución en minutos.</span><span class="sxs-lookup"><span data-stu-id="058fe-108">**Get up and running quickly with the Teams Toolkit**: The Microsoft Teams Toolkit for Visual Studio Code takes care of creating your app project and scaffolding so you can have a running app in minutes.</span></span>
  > * <span data-ttu-id="058fe-109">**Configurar la aplicación con App Studio**: especificar las capacidades y los servicios que usa la aplicación de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="058fe-109">**Configure your app with App Studio**: Specify the capabilities and services your Teams app uses.</span></span>
  > * <span data-ttu-id="058fe-110">**Alcance la audiencia de la aplicación**: cree una aplicación de Microsoft Teams para uso personal, colaboración o ambos.</span><span class="sxs-lookup"><span data-stu-id="058fe-110">**Scope your app's audience**: Build a Teams app for personal use, collaboration, or both.</span></span>
  > * <span data-ttu-id="058fe-111">**Obtenga experiencia con las herramientas y los SDK** de Microsoft: Personalice la aplicación (por ejemplo, cambie su combinación de colores para que sea igual que la del tema de Microsoft Teams) con la ayuda del SDK de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="058fe-111">**Get experience with Teams tools and SDKs**: Customize your app (for example, change its color scheme to match the Teams theme) with help from the Teams JavaScript SDK.</span></span> <span data-ttu-id="058fe-112">Además, obtenga información sobre las herramientas comunes para crear y administrar bots.</span><span class="sxs-lookup"><span data-stu-id="058fe-112">Also, learn about common tools for creating and managing bots.</span></span>
  > * <span data-ttu-id="058fe-113">**Expandir en la aplicación**: en todas las lecciones, encontrará temas relacionados que probablemente le interesan (como las directrices de autenticación y de diseño).</span><span class="sxs-lookup"><span data-stu-id="058fe-113">**Expand on your app**: Throughout the lessons, you'll find related topics you're probably interested in (such as authentication and design guidelines).</span></span>

## <a name="teams-app-fundamentals"></a><span data-ttu-id="058fe-114">Conceptos básicos de las aplicaciones de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="058fe-114">Teams app fundamentals</span></span>

<span data-ttu-id="058fe-115">Antes de empezar con los tutoriales, debe conocer lo siguiente acerca de la creación de aplicaciones para Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="058fe-115">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a><span data-ttu-id="058fe-116">Las aplicaciones pueden tener varias capacidades y puntos de entrada</span><span class="sxs-lookup"><span data-stu-id="058fe-116">Apps can have multiple capabilities and entry points</span></span>

<span data-ttu-id="058fe-117">Una aplicación de Microsoft Teams se compone de una o varias [capacidades de plataforma](../concepts/capabilities-overview.md) (cómo los usuarios usan la aplicación) y [puntos de entrada](../concepts/extensibility-points.md) (donde los usuarios detectan la aplicación).</span><span class="sxs-lookup"><span data-stu-id="058fe-117">A Teams app is made up of one or more [platform capabilities](../concepts/capabilities-overview.md) (how people use the app) and [entry points](../concepts/extensibility-points.md) (where people discover the app).</span></span>

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="058fe-118">Microsoft Teams no hospeda la aplicación</span><span class="sxs-lookup"><span data-stu-id="058fe-118">Teams doesn't host your app</span></span>

<span data-ttu-id="058fe-119">Una aplicación de Microsoft Teams incluye los siguientes elementos importantes:</span><span class="sxs-lookup"><span data-stu-id="058fe-119">A Teams app includes the following important pieces:</span></span>

* <span data-ttu-id="058fe-120">La lógica, el almacenamiento de datos y las llamadas API que encienden la aplicación.</span><span class="sxs-lookup"><span data-stu-id="058fe-120">The logic, data storage, and API calls that power your app.</span></span> <span data-ttu-id="058fe-121">Estos servicios no se hospedan en Microsoft Teams y deben ser accesibles a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="058fe-121">These services are not hosted by Teams and must be accessible via HTTPS.</span></span>
* <span data-ttu-id="058fe-122">El cliente de Microsoft Teams (Web, escritorio o móvil) donde los usuarios usan la aplicación.</span><span class="sxs-lookup"><span data-stu-id="058fe-122">The Teams client (web, desktop, or mobile) where people use your app.</span></span>
* <span data-ttu-id="058fe-123">El identificador de la aplicación, que permite configurar la aplicación con App Studio.</span><span class="sxs-lookup"><span data-stu-id="058fe-123">Your app ID, which lets you configure your app with App Studio.</span></span>

## <a name="get-prerequisites"></a><span data-ttu-id="058fe-124">Obtener requisitos previos</span><span class="sxs-lookup"><span data-stu-id="058fe-124">Get prerequisites</span></span>

<span data-ttu-id="058fe-125">Compruebe que tiene la cuenta correcta para crear aplicaciones de Teams e instalar algunas herramientas de desarrollo recomendadas.</span><span class="sxs-lookup"><span data-stu-id="058fe-125">Verify you have the right account for building Teams apps and install some recommended development tools.</span></span>

### <a name="set-up-your-development-account"></a><span data-ttu-id="058fe-126">Configurar la cuenta de desarrollo</span><span class="sxs-lookup"><span data-stu-id="058fe-126">Set up your development account</span></span>

<span data-ttu-id="058fe-127">Necesita una cuenta de teams que permita la transferencia de una aplicación personalizada.</span><span class="sxs-lookup"><span data-stu-id="058fe-127">You need a Teams account that allows custom app sideloading.</span></span> <span data-ttu-id="058fe-128">(Es posible que la cuenta ya la proporcione).</span><span class="sxs-lookup"><span data-stu-id="058fe-128">(Your account may already provide this.)</span></span>

1. <span data-ttu-id="058fe-129">Si tiene una cuenta de Teams, compruebe si puede transferir aplicaciones en Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="058fe-129">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="058fe-130">En el cliente de Microsoft Teams, seleccione **aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="058fe-130">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="058fe-131">Busca una opción para **cargar una aplicación personalizada**.</span><span class="sxs-lookup"><span data-stu-id="058fe-131">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Ilustración en la que se muestra dónde en Teams puede cargar una aplicación personalizada.":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><span data-ttu-id="058fe-133"><b>Seleccione aquí</b> si no ve la opción de instalación de prueba o si no tiene una cuenta de Teams.</span><span class="sxs-lookup"><span data-stu-id="058fe-133"><b>Select here</b> if you can't see the sideload option or don't have a Teams account.</span></span></summary>

<span data-ttu-id="058fe-134">Puede obtener una cuenta gratuita de prueba de Microsoft teams que permite la transferencia de aplicaciones mediante la incorporación al programa de desarrolladores de Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="058fe-134">You can get a free Teams test account that allows app sideloading by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="058fe-135">(El proceso de registro dura aproximadamente dos minutos).</span><span class="sxs-lookup"><span data-stu-id="058fe-135">(The registration process takes approximately two minutes.)</span></span>

1. <span data-ttu-id="058fe-136">Vaya al [programa de desarrolladores de Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).</span><span class="sxs-lookup"><span data-stu-id="058fe-136">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="058fe-137">Seleccione **unirse ahora** y siga las instrucciones que aparecen en pantalla.</span><span class="sxs-lookup"><span data-stu-id="058fe-137">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="058fe-138">Cuando llegue a la pantalla de bienvenida, seleccione **configurar la suscripción a E5**.</span><span class="sxs-lookup"><span data-stu-id="058fe-138">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="058fe-139">Configure la cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="058fe-139">Set up your administrator account.</span></span> <span data-ttu-id="058fe-140">Una vez que haya terminado, debería ver una pantalla como esta.</span><span class="sxs-lookup"><span data-stu-id="058fe-140">Once you finish, you should see a screen like this.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Ejemplo de lo que ve después de registrarse para el programa de desarrolladores de Microsoft 365.":::
1. <span data-ttu-id="058fe-142">Inicie sesión en Teams con la cuenta de administrador que acaba de configurar.</span><span class="sxs-lookup"><span data-stu-id="058fe-142">Log in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="058fe-143">Compruebe si ahora tiene la opción **cargar una aplicación personalizada** .</span><span class="sxs-lookup"><span data-stu-id="058fe-143">Verify if you now have the **Upload a custom app** option.</span></span>

</details>

> [!Note]
> <span data-ttu-id="058fe-144">Si sigue sin poder transferir localmente aplicaciones, consulte [Habilitar aplicaciones personalizadas de Teams y activar la carga de aplicaciones personalizadas](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).</span><span class="sxs-lookup"><span data-stu-id="058fe-144">If you still can't sideload apps, refer to [Enable custom Teams apps and turn on custom app uploading](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).</span></span>

### <a name="install-your-development-tools"></a><span data-ttu-id="058fe-145">Instalar las herramientas de desarrollo</span><span class="sxs-lookup"><span data-stu-id="058fe-145">Install your development tools</span></span>

<span data-ttu-id="058fe-146">Puede crear aplicaciones de Teams con sus herramientas preferidas, pero estas lecciones muestran cómo puede empezar rápidamente con Microsoft Teams Toolkit para Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="058fe-146">You can build Teams apps with your preferred tools, but these lessons show how you can get started quickly with the Microsoft Teams Toolkit for Visual Studio Code.</span></span>

<span data-ttu-id="058fe-147">Teams muestra el contenido de la aplicación solo a través de conexiones HTTPS.</span><span class="sxs-lookup"><span data-stu-id="058fe-147">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="058fe-148">Para depurar determinados tipos de aplicaciones de forma local, como un bot, aprenderá a usar [ngrok para configurar un túnel seguro](../concepts/build-and-test/debug.md#locally-hosted) entre Microsoft Teams y la aplicación.</span><span class="sxs-lookup"><span data-stu-id="058fe-148">To debug certain types of apps locally, such as a bot, you'll learn how to use [ngrok to set up a secure tunnel](../concepts/build-and-test/debug.md#locally-hosted) between Teams and your app.</span></span> <span data-ttu-id="058fe-149">(Las aplicaciones de producción de Teams se hospedan en la nube).</span><span class="sxs-lookup"><span data-stu-id="058fe-149">(Production Teams apps are hosted in the cloud.)</span></span>

1. <span data-ttu-id="058fe-150">Instale [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="058fe-150">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="058fe-151">Instale [ngrok](https://ngrok.com/download) si tiene previsto crear una extensión de robot o de mensajería.</span><span class="sxs-lookup"><span data-stu-id="058fe-151">Install [ngrok](https://ngrok.com/download) if you plan to build a bot or messaging extension.</span></span>
1. <span data-ttu-id="058fe-152">Instale la versión más reciente de [Visual Studio Code](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="058fe-152">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> <span data-ttu-id="058fe-153">(Es posible que las versiones anteriores no funcionen con el kit de herramientas).</span><span class="sxs-lookup"><span data-stu-id="058fe-153">(Earlier versions might not work with the toolkit.)</span></span>
1. En Visual Studio Code, seleccione **extensiones** :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: en la barra de actividad izquierda e instale el **Kit de herramientas de Microsoft Teams**.

    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Ilustración que muestra dónde en Visual Studio Code puede instalar la extensión de Microsoft Teams Toolkit.":::

## <a name="about-the-tutorials"></a><span data-ttu-id="058fe-156">Acerca de los tutoriales</span><span class="sxs-lookup"><span data-stu-id="058fe-156">About the tutorials</span></span>

<span data-ttu-id="058fe-157">Puede empezar con cualquiera de los equipos **compilar sus primeras** lecciones de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="058fe-157">You can start with any of the Teams **build your first app** lessons.</span></span> <span data-ttu-id="058fe-158">Si no está seguro de dónde ir primero, siga nuestra ruta de acceso accesible para principiantes y cree un "Hola a todos".</span><span class="sxs-lookup"><span data-stu-id="058fe-158">If you're not sure where to go first, follow our beginner friendly path and build a "Hello, World!"</span></span> <span data-ttu-id="058fe-159">XXX.</span><span class="sxs-lookup"><span data-stu-id="058fe-159">app.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="Árbol de habilidades que muestra los caminos de aprendizaje para los tutoriales &quot;crear su primera aplicación&quot;." border="false":::

## <a name="next-step"></a><span data-ttu-id="058fe-161">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="058fe-161">Next step</span></span>

<span data-ttu-id="058fe-162">Una vez configurada la cuenta y el entorno, puede empezar a crear.</span><span class="sxs-lookup"><span data-stu-id="058fe-162">Once you set up your account and environment, you can start building.</span></span>

### <a name="beginner-friendly-tutorial"></a><span data-ttu-id="058fe-163">Tutorial práctico para principiante</span><span class="sxs-lookup"><span data-stu-id="058fe-163">Beginner friendly tutorial</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="058fe-164">Crear una aplicación "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="058fe-164">Build a "Hello, World!" app</span></span>](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a><span data-ttu-id="058fe-165">Otros tutoriales</span><span class="sxs-lookup"><span data-stu-id="058fe-165">Other tutorials</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="058fe-166">Crear un bot</span><span class="sxs-lookup"><span data-stu-id="058fe-166">Build a bot</span></span>](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="058fe-167">Crear una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="058fe-167">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)

---
title: 'Introducción: compilar la primera introducción a la aplicación y requisitos previos'
author: heath-hamilton
description: Obtenga información sobre cómo empezar a trabajar con el desarrollo de aplicaciones de Microsoft Teams y configurar el entorno.
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: quickstart
ms.openlocfilehash: c158b7ad925e05e4056769536f5e0d212763942a
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452606"
---
# <a name="build-your-first-microsoft-teams-app-overview"></a><span data-ttu-id="ad0c9-103">Crear su primera información general de la aplicación Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ad0c9-103">Build your first Microsoft Teams app overview</span></span>

<span data-ttu-id="ad0c9-104">En la lección **compilar la primera aplicación** , puede crear aplicaciones básicas de Teams.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-104">In the **build your first app** lessons, you create basic Teams apps.</span></span> <span data-ttu-id="ad0c9-105">En cada tutorial se explica cómo crear una aplicación sencilla y real de Teams, a la vez que se presentan herramientas comunes, conceptos fundamentales y características más avanzadas.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-105">Each tutorial walks through how to build a simple, real-world Teams app while introducing you to common tools, fundamental concepts, and more advanced features.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="ad0c9-106">Qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="ad0c9-106">What you'll learn</span></span>

<span data-ttu-id="ad0c9-107">Esta es una idea de lo que sabrá después de pasar por las lecciones.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-107">Here's an idea of what you'll know after going through the lessons.</span></span>

> [!div class="checklist"]
  >
  > * <span data-ttu-id="ad0c9-108">**Póngase en marcha rápidamente con Team Toolkit**: el kit de herramientas de Microsoft Teams para Visual Studio Code se encarga de crear el proyecto de la aplicación y el scaffolding para que pueda tener una aplicación en ejecución en minutos.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-108">**Get up and running quickly with the Teams Toolkit**: The Microsoft Teams Toolkit for Visual Studio Code takes care of creating your app project and scaffolding so you can have a running app in minutes.</span></span>
  > * <span data-ttu-id="ad0c9-109">**Definir la aplicación con el manifiesto**: el manifiesto de la aplicación es donde se especifican las capacidades y los servicios que usa la aplicación de su equipo.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-109">**Define your app with the manifest**: The app manifest is where you specify the capabilities and services your Teams app uses.</span></span>
  > * <span data-ttu-id="ad0c9-110">**Alcance la audiencia de la aplicación**: cree una aplicación de Microsoft Teams para uso personal, colaboración o ambos.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-110">**Scope your app's audience**: Build a Teams app for personal use, collaboration, or both.</span></span>
  > * <span data-ttu-id="ad0c9-111">**Obtener experiencia con Teams frameworks**: personalizar la aplicación (por ejemplo, cambiar su combinación de colores para que sea igual que el del tema de Microsoft Teams) con la ayuda del SDK de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-111">**Get experience with Teams frameworks**: Customize your app (for example, change its color scheme to match the Teams theme) with help from the Teams JavaScript SDK.</span></span> <span data-ttu-id="ad0c9-112">Además, obtenga información sobre las herramientas comunes para crear y administrar bots.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-112">Also, learn about common tools for creating and managing bots.</span></span>
  > * <span data-ttu-id="ad0c9-113">**Expandir en la aplicación**: en todas las lecciones, encontrará temas relacionados que probablemente le interesan (como las directrices de autenticación y de diseño).</span><span class="sxs-lookup"><span data-stu-id="ad0c9-113">**Expand on your app**: Throughout the lessons, you'll find related topics you're probably interested in (such as authentication and design guidelines).</span></span>

## <a name="teams-app-fundamentals"></a><span data-ttu-id="ad0c9-114">Conceptos básicos de las aplicaciones de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ad0c9-114">Teams app fundamentals</span></span>

<span data-ttu-id="ad0c9-115">Antes de empezar con los tutoriales, debe conocer lo siguiente acerca de la creación de aplicaciones para Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-115">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a><span data-ttu-id="ad0c9-116">Las aplicaciones pueden tener varias capacidades y puntos de entrada</span><span class="sxs-lookup"><span data-stu-id="ad0c9-116">Apps can have multiple capabilities and entry points</span></span>

<span data-ttu-id="ad0c9-117">Las aplicaciones de Microsoft Teams se componen de una o varias capacidades y [puntos de entrada](../concepts/extensibility-points.md)de la [plataforma](../concepts/capabilities-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="ad0c9-117">Teams apps are made up of one or more [platform capabilities](../concepts/capabilities-overview.md) and [entry points](../concepts/extensibility-points.md).</span></span> <span data-ttu-id="ad0c9-118">Puede presentar la aplicación mediante una serie de [componentes y convenciones](../concepts/extensibility-points.md#ui-components)de la interfaz de usuario específicos de Microsoft Teams, como tarjetas y módulos de tareas.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-118">You can present your app using a number of Teams-specific [UI components and conventions](../concepts/extensibility-points.md#ui-components), such as cards and task modules.</span></span>

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="ad0c9-119">Microsoft Teams no hospeda la aplicación</span><span class="sxs-lookup"><span data-stu-id="ad0c9-119">Teams doesn't host your app</span></span>

<span data-ttu-id="ad0c9-120">Una aplicación de Microsoft Teams incluye tres partes importantes:</span><span class="sxs-lookup"><span data-stu-id="ad0c9-120">A Teams app includes three important pieces:</span></span>

* <span data-ttu-id="ad0c9-121">La lógica, el almacenamiento de datos y las llamadas API que encienden la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-121">The logic, data storage, and API calls that power your app.</span></span> <span data-ttu-id="ad0c9-122">Estos servicios no se hospedan en Microsoft Teams y deben ser accesibles a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-122">These services are not hosted by Teams and must be accessible via HTTPS.</span></span>
* <span data-ttu-id="ad0c9-123">El cliente de Microsoft Teams (Web, escritorio o móvil) donde los usuarios usan la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-123">The Teams client (web, desktop, or mobile) where people use your app.</span></span>
* <span data-ttu-id="ad0c9-124">El paquete de la aplicación, que se usa para instalar la aplicación en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-124">Your app package, which you use to install the app in Teams.</span></span> <span data-ttu-id="ad0c9-125">Contiene metadatos de la aplicación y punteros a los servicios hospedados.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-125">It contains app metadata and pointers to your hosted services.</span></span>

## <a name="get-prerequisites"></a><span data-ttu-id="ad0c9-126">Obtener requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ad0c9-126">Get prerequisites</span></span>

<span data-ttu-id="ad0c9-127">Compruebe que tiene la cuenta correcta para crear aplicaciones de Teams e instalar algunas herramientas de desarrollo recomendadas.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-127">Verify you have the right account for building Teams apps and install some recommended development tools.</span></span>

### <a name="set-up-your-development-account"></a><span data-ttu-id="ad0c9-128">Configurar la cuenta de desarrollo</span><span class="sxs-lookup"><span data-stu-id="ad0c9-128">Set up your development account</span></span>

<span data-ttu-id="ad0c9-129">Necesita una cuenta de teams que permita la transferencia de una aplicación personalizada.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-129">You need a Teams account that allows custom app sideloading.</span></span> <span data-ttu-id="ad0c9-130">(Es posible que la cuenta ya la proporcione).</span><span class="sxs-lookup"><span data-stu-id="ad0c9-130">(Your account may already provide this.)</span></span>

1. <span data-ttu-id="ad0c9-131">Si tiene una cuenta de Teams, compruebe si puede transferir aplicaciones en Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="ad0c9-131">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="ad0c9-132">En el cliente de Microsoft Teams, seleccione **aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-132">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="ad0c9-133">Busca una opción para **cargar una aplicación personalizada**.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-133">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Ilustración en la que se muestra dónde en Teams puede cargar una aplicación personalizada.":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><span data-ttu-id="ad0c9-135"><b>Seleccione aquí</b> si no ve la opción de instalación de prueba o si no tiene una cuenta de Teams.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-135"><b>Select here</b> if you can't see the sideload option or don't have a Teams account.</span></span></summary>

<span data-ttu-id="ad0c9-136">Puede obtener una cuenta gratuita de prueba de Microsoft teams que permite la transferencia de aplicaciones mediante la incorporación al programa de desarrolladores de Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-136">You can get a free Teams test account that allows app sideloading by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="ad0c9-137">(El proceso de registro dura aproximadamente dos minutos).</span><span class="sxs-lookup"><span data-stu-id="ad0c9-137">(The registration process takes approximately two minutes.)</span></span>

1. <span data-ttu-id="ad0c9-138">Vaya al [programa de desarrolladores de Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).</span><span class="sxs-lookup"><span data-stu-id="ad0c9-138">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="ad0c9-139">Seleccione **unirse ahora** y siga las instrucciones que aparecen en pantalla.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-139">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="ad0c9-140">Cuando llegue a la pantalla de bienvenida, seleccione **configurar la suscripción a E5**.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-140">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="ad0c9-141">Configure la cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-141">Set up your administrator account.</span></span> <span data-ttu-id="ad0c9-142">Una vez que haya terminado, debería ver una pantalla como esta.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-142">Once you finish, you should see a screen like this.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Ilustración en la que se muestra dónde en Teams puede cargar una aplicación personalizada.":::
1. <span data-ttu-id="ad0c9-144">Inicie sesión en Teams con la cuenta de administrador que acaba de configurar.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-144">Log in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="ad0c9-145">Compruebe si ahora tiene la opción **cargar una aplicación personalizada** .</span><span class="sxs-lookup"><span data-stu-id="ad0c9-145">Verify if you now have the **Upload a custom app** option.</span></span>

</details>

### <a name="install-your-development-tools"></a><span data-ttu-id="ad0c9-146">Instalar las herramientas de desarrollo</span><span class="sxs-lookup"><span data-stu-id="ad0c9-146">Install your development tools</span></span>

<span data-ttu-id="ad0c9-147">Puede crear aplicaciones de Teams con sus herramientas preferidas, pero estas lecciones muestran cómo puede empezar rápidamente con Microsoft Teams Toolkit para Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-147">You can build Teams apps with your preferred tools, but these lessons show how you can get started quickly with the Microsoft Teams Toolkit for Visual Studio Code.</span></span>

<span data-ttu-id="ad0c9-148">Teams muestra el contenido de la aplicación solo a través de conexiones HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-148">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="ad0c9-149">Puesto que hospedará su primera aplicación localmente para ahorrar tiempo, aprenderá a usar [ngrok para configurar un túnel seguro](../concepts/build-and-test/debug.md#locally-hosted) entre Microsoft Teams y la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-149">Since you'll host your first app locally to save time, you'll learn how to use [ngrok to set up a secure tunnel](../concepts/build-and-test/debug.md#locally-hosted) between Teams and your app.</span></span> <span data-ttu-id="ad0c9-150">(Las aplicaciones de Microsoft Teams de nivel de producción se hospedan en la nube).</span><span class="sxs-lookup"><span data-stu-id="ad0c9-150">(Production-level Teams apps are hosted in the cloud.)</span></span>

1. <span data-ttu-id="ad0c9-151">Instale [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="ad0c9-151">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="ad0c9-152">Instale [ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="ad0c9-152">Install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="ad0c9-153">Instale la versión más reciente de [Visual Studio Code](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="ad0c9-153">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> <span data-ttu-id="ad0c9-154">(Es posible que las versiones anteriores no funcionen con el kit de herramientas).</span><span class="sxs-lookup"><span data-stu-id="ad0c9-154">(Earlier versions might not work with the toolkit.)</span></span>
1. En Visual Studio Code, seleccione **extensiones** :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: en la barra de actividad izquierda e instale el **Kit de herramientas de Microsoft Teams**.

    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Ilustración en la que se muestra dónde en Teams puede cargar una aplicación personalizada.":::

## <a name="about-the-tutorials"></a><span data-ttu-id="ad0c9-157">Acerca de los tutoriales</span><span class="sxs-lookup"><span data-stu-id="ad0c9-157">About the tutorials</span></span>

<span data-ttu-id="ad0c9-158">Puede empezar con cualquiera de los equipos **compilar sus primeras** lecciones de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-158">You can start with any of the Teams **build your first app** lessons.</span></span> <span data-ttu-id="ad0c9-159">Si no está seguro de dónde ir primero, siga nuestra ruta de acceso accesible para principiantes y cree un "Hola a todos".</span><span class="sxs-lookup"><span data-stu-id="ad0c9-159">If you're not sure where to go first, follow our beginner friendly path and build a "Hello, World!"</span></span> <span data-ttu-id="ad0c9-160">XXX.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-160">app.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="Ilustración en la que se muestra dónde en Teams puede cargar una aplicación personalizada." border="false":::

## <a name="next-step"></a><span data-ttu-id="ad0c9-162">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="ad0c9-162">Next step</span></span>

<span data-ttu-id="ad0c9-163">Una vez configurada la cuenta y el entorno, puede empezar a crear.</span><span class="sxs-lookup"><span data-stu-id="ad0c9-163">Once you set up your account and environment, you can start building.</span></span>

### <a name="beginner-friendly-tutorial"></a><span data-ttu-id="ad0c9-164">Tutorial práctico para principiante</span><span class="sxs-lookup"><span data-stu-id="ad0c9-164">Beginner friendly tutorial</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ad0c9-165">Crear una aplicación "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="ad0c9-165">Build a "Hello, World!" app</span></span>](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a><span data-ttu-id="ad0c9-166">Otros tutoriales</span><span class="sxs-lookup"><span data-stu-id="ad0c9-166">Other tutorials</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ad0c9-167">Crear un bot</span><span class="sxs-lookup"><span data-stu-id="ad0c9-167">Build a bot</span></span>](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="ad0c9-168">Crear una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="ad0c9-168">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)

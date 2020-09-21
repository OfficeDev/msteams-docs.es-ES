---
title: Empezar a compilar su primera aplicación de Microsoft Teams
author: heath-hamilton
ms.author: lajanuar
description: Información general y requisitos previos para crear su primera aplicación de Microsoft Teams
ms.openlocfilehash: 9392096a285a43d3a1f8bed5020e3464da0f7f18
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964764"
---
# <a name="get-started-building-your-first-teams-app"></a><span data-ttu-id="bf0ba-103">Empezar a compilar su primera aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="bf0ba-103">Get started building your first Teams app</span></span>

<span data-ttu-id="bf0ba-104">En la lección **compilar la primera aplicación** , puede crear aplicaciones básicas de Teams.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-104">In the **build your first app** lessons, you create basic Teams apps.</span></span> <span data-ttu-id="bf0ba-105">En cada tutorial se explica cómo crear una aplicación sencilla y real de Teams a la vez que se presentan herramientas comunes, conceptos fundamentales y otras características avanzadas.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-105">Each tutorial walks through how to build a simple, real-world Teams app while introducing you to common tools, fundamental concepts, and some more advanced features.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="bf0ba-106">Qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="bf0ba-106">What you'll learn</span></span>

<span data-ttu-id="bf0ba-107">Esta es una idea de lo que sabrá después de pasar por las lecciones.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-107">Here's an idea of what you'll know after going through the lessons.</span></span>

> [!div class="checklist"]
  >
  > * <span data-ttu-id="bf0ba-108">**Póngase en marcha rápidamente con Team Toolkit**: el kit de herramientas de Microsoft Teams para Visual Studio Code se encarga de crear el proyecto de la aplicación y el scaffolding para que pueda tener una aplicación en ejecución en minutos.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-108">**Get up and running quickly with the Teams Toolkit**: The Microsoft Teams Toolkit for Visual Studio Code takes care of creating your app project and scaffolding so you can have a running app in minutes.</span></span>
  > * <span data-ttu-id="bf0ba-109">**Definir la aplicación con el manifiesto**: el manifiesto de la aplicación es donde se especifican las capacidades y los servicios que usa la aplicación de su equipo.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-109">**Define your app with the manifest**: The app manifest is where you specify the capabilities and services your Teams app uses.</span></span>
  > * <span data-ttu-id="bf0ba-110">**Alcance la audiencia de la aplicación**: cree una aplicación de Microsoft Teams para uso personal, colaboración o ambos.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-110">**Scope your app's audience**: Build a Teams app for personal use, collaboration, or both.</span></span>
  > * <span data-ttu-id="bf0ba-111">**Obtener experiencia con Marcos**: Personalice la aplicación (por ejemplo, cambie su combinación de colores para que sea igual que el del tema de Microsoft Teams) con la ayuda del SDK de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-111">**Get experience with frameworks**: Customize your app (for example, change its color scheme to match the Teams theme) with help from the Teams JavaScript SDK.</span></span> <span data-ttu-id="bf0ba-112">Además, obtenga información sobre las herramientas comunes para crear y administrar bots.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-112">Also, learn about common tools for creating and managing bots.</span></span>
  > * <span data-ttu-id="bf0ba-113">**Expandir en la aplicación**: en todas las lecciones, encontrará temas relacionados que probablemente le interesan (como las directrices de autenticación y de diseño).</span><span class="sxs-lookup"><span data-stu-id="bf0ba-113">**Expand on your app**: Throughout the lessons, you'll find related topics you're probably interested in (such as authentication and design guidelines).</span></span>

## <a name="teams-app-fundamentals"></a><span data-ttu-id="bf0ba-114">Conceptos básicos de las aplicaciones de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="bf0ba-114">Teams app fundamentals</span></span>

<span data-ttu-id="bf0ba-115">Antes de empezar con los tutoriales, debe conocer lo siguiente acerca de la creación de aplicaciones para Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-115">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="apps-can-have-multiple-capabilities"></a><span data-ttu-id="bf0ba-116">Las aplicaciones pueden tener varias funcionalidades</span><span class="sxs-lookup"><span data-stu-id="bf0ba-116">Apps can have multiple capabilities</span></span>

<span data-ttu-id="bf0ba-117">Las aplicaciones de Microsoft Teams se componen de una o varias [capacidades de plataforma](../capabilities-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bf0ba-117">Teams apps are made up of one or more [platform capabilities](../capabilities-overview.md).</span></span> <span data-ttu-id="bf0ba-118">Puede mostrar estas funciones mediante una serie de [componentes y convenciones](../doc-links/teams-ui-conventions.md)de la interfaz de usuario específicos de Microsoft Teams, como tarjetas y módulos de tareas.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-118">You can display these capabilities using a number of Teams-specific [UI components and conventions](../doc-links/teams-ui-conventions.md), such as cards and task modules.</span></span>

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="bf0ba-119">Microsoft Teams no hospeda la aplicación</span><span class="sxs-lookup"><span data-stu-id="bf0ba-119">Teams doesn't host your app</span></span>

<span data-ttu-id="bf0ba-120">Una aplicación de Microsoft Teams incluye tres partes importantes:</span><span class="sxs-lookup"><span data-stu-id="bf0ba-120">A Teams app includes three important pieces:</span></span>

* <span data-ttu-id="bf0ba-121">La lógica, el almacenamiento de datos y las llamadas API que encienden la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-121">The logic, data storage, and API calls that power your app.</span></span> <span data-ttu-id="bf0ba-122">Estos servicios no se hospedan en Microsoft Teams y deben ser accesibles a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-122">These services are not hosted by Teams and must be accessible via HTTPS.</span></span>
* <span data-ttu-id="bf0ba-123">El cliente de Microsoft Teams (Web, escritorio o móvil) donde los usuarios usan la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-123">The Teams client (web, desktop, or mobile) where people use your app.</span></span>
* <span data-ttu-id="bf0ba-124">El paquete de la aplicación, que se usa para instalar la aplicación en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-124">Your app package, which you use to install the app in Teams.</span></span> <span data-ttu-id="bf0ba-125">Contiene metadatos de la aplicación y punteros a los servicios hospedados.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-125">It contains app metadata and pointers to your hosted services.</span></span>

## <a name="get-prerequisites"></a><span data-ttu-id="bf0ba-126">Obtener requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bf0ba-126">Get prerequisites</span></span>

<span data-ttu-id="bf0ba-127">Compruebe que tiene la cuenta correcta para crear aplicaciones de Teams e instalar algunas herramientas de desarrollo recomendadas.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-127">Verify you have the right account for building Teams apps and install some recommended development tools.</span></span>

### <a name="set-up-your-development-account"></a><span data-ttu-id="bf0ba-128">Configurar la cuenta de desarrollo</span><span class="sxs-lookup"><span data-stu-id="bf0ba-128">Set up your development account</span></span>

<span data-ttu-id="bf0ba-129">Necesita una cuenta de teams que permita la transferencia de una aplicación personalizada.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-129">You need a Teams account that allows custom app sideloading.</span></span> <span data-ttu-id="bf0ba-130">(Es posible que la cuenta ya la proporcione).</span><span class="sxs-lookup"><span data-stu-id="bf0ba-130">(Your account may already provide this.)</span></span>

1. <span data-ttu-id="bf0ba-131">Si tiene una cuenta de Teams, compruebe si puede transferir aplicaciones en Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="bf0ba-131">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="bf0ba-132">En el cliente de Microsoft Teams, seleccione **aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-132">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="bf0ba-133">Busca una opción para **cargar una aplicación personalizada**.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-133">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="../doc-links/images/upload-custom-app-closeup.png" alt-text="vista de opciones de instalación de prueba":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><span data-ttu-id="bf0ba-135"><b>Seleccione aquí</b> si no ve la opción de instalación de prueba o si no tiene una cuenta de Teams.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-135"><b>Select here</b> if you can't see the sideload option or don't have a Teams account.</span></span></summary>

<span data-ttu-id="bf0ba-136">Puede obtener una cuenta gratuita de prueba de Microsoft teams que permite la transferencia de aplicaciones mediante la incorporación al programa de desarrolladores de Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-136">You can get a free Teams test account that allows app sideloading by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="bf0ba-137">(El proceso de registro dura aproximadamente dos minutos).</span><span class="sxs-lookup"><span data-stu-id="bf0ba-137">(The registration process takes approximately two minutes.)</span></span>

1. <span data-ttu-id="bf0ba-138">Vaya al [programa de desarrolladores de Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).</span><span class="sxs-lookup"><span data-stu-id="bf0ba-138">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="bf0ba-139">Seleccione **unirse ahora** y siga las instrucciones que aparecen en pantalla.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-139">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="bf0ba-140">Cuando llegue a la pantalla de bienvenida, seleccione **configurar la suscripción a E5**.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-140">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="bf0ba-141">Configure la cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-141">Set up your administrator account.</span></span> <span data-ttu-id="bf0ba-142">Una vez que haya terminado, debería ver una pantalla como esta.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-142">Once you finish, you should see a screen like this.</span></span>
:::image type="content" source="../doc-links/images/dev-program-subscription.png" alt-text="vista de suscripción del programa dev":::
1. <span data-ttu-id="bf0ba-144">Inicie sesión en Teams con la cuenta de administrador que acaba de configurar.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-144">Log in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="bf0ba-145">Compruebe si ahora tiene la opción **cargar una aplicación personalizada** .</span><span class="sxs-lookup"><span data-stu-id="bf0ba-145">Verify if you now have the **Upload a custom app** option.</span></span>

</details>

### <a name="install-your-development-tools"></a><span data-ttu-id="bf0ba-146">Instalar las herramientas de desarrollo</span><span class="sxs-lookup"><span data-stu-id="bf0ba-146">Install your development tools</span></span>

<span data-ttu-id="bf0ba-147">Puede crear aplicaciones de Teams con sus herramientas preferidas, pero estas lecciones muestran cómo puede empezar rápidamente con Microsoft Teams Toolkit para Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-147">You can build Teams apps with your preferred tools, but these lessons show how you can get started quickly with the Microsoft Teams Toolkit for Visual Studio Code.</span></span>

<span data-ttu-id="bf0ba-148">Teams muestra el contenido de la aplicación solo a través de conexiones HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-148">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="bf0ba-149">Puesto que hospedará su primera aplicación localmente, aprenderá a usar [ngrok para configurar un túnel seguro](../doc-links/debug.md#locally-hosted) entre Microsoft Teams y su aplicación.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-149">Since you'll host your first app locally, you'll learn how to use [ngrok to set up a secure tunnel](../doc-links/debug.md#locally-hosted) between Teams and your app.</span></span>

1. <span data-ttu-id="bf0ba-150">Instale [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="bf0ba-150">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="bf0ba-151">Instale la versión más reciente de [Visual Studio Code](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="bf0ba-151">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> <span data-ttu-id="bf0ba-152">(Es posible que las versiones anteriores no funcionen con el kit de herramientas).</span><span class="sxs-lookup"><span data-stu-id="bf0ba-152">(Earlier versions might not work with the toolkit.)</span></span>
1. En Visual Studio Code, seleccione **extensiones** :::image type="icon" source="../doc-links/images/vs-code-extensions.png"::: en la barra de actividad izquierda e instale el **Kit de herramientas de Microsoft Teams**.
    :::image type="content" source="../doc-links/images/vsc-install-toolkit.png" alt-text="instalar vista de kit de herramientas":::
1. <span data-ttu-id="bf0ba-155">Instale [ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="bf0ba-155">Install [ngrok](https://ngrok.com/download).</span></span>

## <a name="next-step"></a><span data-ttu-id="bf0ba-156">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="bf0ba-156">Next step</span></span>

<span data-ttu-id="bf0ba-157">Una vez configurada la cuenta y el entorno, puede empezar a crear.</span><span class="sxs-lookup"><span data-stu-id="bf0ba-157">Once you set up your account and environment, you can start building.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bf0ba-158">Compilar y ejecutar la primera aplicación</span><span class="sxs-lookup"><span data-stu-id="bf0ba-158">Build and run your first app</span></span>](../build-your-first-app/build-and-run.md)

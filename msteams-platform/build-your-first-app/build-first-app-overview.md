---
title: 'Introducción: crear la primera introducción a la aplicación y los requisitos previos'
author: girliemac
description: Obtén información sobre cómo empezar a usar Microsoft Teams desarrollo de aplicaciones y configurar el entorno.
ms.author: timura
ms.date: 03/18/2021
ms.topic: quickstart
ms.openlocfilehash: dae942be9383ef1e0a931d238e6148651f334ef5
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565882"
---
# <a name="get-started-with-microsoft-teams-app-development"></a><span data-ttu-id="bf0c5-103">Introducción al desarrollo Microsoft Teams aplicaciones</span><span class="sxs-lookup"><span data-stu-id="bf0c5-103">Get started with Microsoft Teams app development</span></span>

<span data-ttu-id="bf0c5-104">Crea una aplicación sencilla para aprender los conceptos básicos de Teams desarrollo de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bf0c5-104">Build a simple app to learn the basics of Teams app development.</span></span> <span data-ttu-id="bf0c5-105">Una vez que veas "Hello, World!", prueba cualquiera de los otros artículos de introducción para obtener más información sobre herramientas comunes, conceptos fundamentales y características avanzadas.</span><span class="sxs-lookup"><span data-stu-id="bf0c5-105">Once you see "Hello, World!", try any of the other get started articles for more information on common tools, fundamental concepts, and advanced features.</span></span>



## <a name="what-youll-learn"></a><span data-ttu-id="bf0c5-106">Lo que aprenderás</span><span class="sxs-lookup"><span data-stu-id="bf0c5-106">What you'll learn</span></span>

* <span data-ttu-id="bf0c5-107">Se ejecuta rápidamente con el Teams Toolkit, una Visual Studio Code extensión.</span><span class="sxs-lookup"><span data-stu-id="bf0c5-107">Get up and running quickly with the Teams Toolkit, a Visual Studio Code extension.</span></span> 
* <span data-ttu-id="bf0c5-108">Configura la aplicación con App Studio.</span><span class="sxs-lookup"><span data-stu-id="bf0c5-108">Configure your app with App Studio.</span></span>
* <span data-ttu-id="bf0c5-109">Familiarícese con Teams y SDK para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="bf0c5-109">Get familiar with Teams developer tools and SDKs.</span></span>
* <span data-ttu-id="bf0c5-110">Ten en cuenta Teams conceptos de aplicación, como la autenticación y los procedimientos recomendados de diseño.</span><span class="sxs-lookup"><span data-stu-id="bf0c5-110">Consider important Teams app concepts, such as authentication and design best practices.</span></span>

<span data-ttu-id="bf0c5-111">Puedes crear una aplicación Teams con cualquier tecnología que prefieras, por ejemplo, la interfaz de línea de comandos (CLI).</span><span class="sxs-lookup"><span data-stu-id="bf0c5-111">You can build a Teams app using any technology of your choice, for example, command-line interface (CLI).</span></span> <span data-ttu-id="bf0c5-112">Sin embargo, estos artículos le ayudan a empezar con las siguientes herramientas y tecnologías recomendadas:</span><span class="sxs-lookup"><span data-stu-id="bf0c5-112">But, these articles help you get started with the following recommended tools and technologies:</span></span>

* <span data-ttu-id="bf0c5-113">Teams Toolkit, una Visual Studio Code extensión</span><span class="sxs-lookup"><span data-stu-id="bf0c5-113">Teams Toolkit, a Visual Studio Code extension</span></span>
* <span data-ttu-id="bf0c5-114">React.js para pestañas</span><span class="sxs-lookup"><span data-stu-id="bf0c5-114">React.js for tabs</span></span>
* <span data-ttu-id="bf0c5-115">Node.js para bots y extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="bf0c5-115">Node.js for bots and messaging extensions</span></span>


## <a name="teams-app-fundamentals"></a><span data-ttu-id="bf0c5-116">Teams fundamentales de la aplicación</span><span class="sxs-lookup"><span data-stu-id="bf0c5-116">Teams app fundamentals</span></span>

<span data-ttu-id="bf0c5-117">Puedes crear aplicaciones de Teams personalizadas para ti, personas de tu organización o personas de todo el mundo.</span><span class="sxs-lookup"><span data-stu-id="bf0c5-117">You can build custom Teams apps for yourself, people in your org, or people all over the world.</span></span> <span data-ttu-id="bf0c5-118">Antes de comenzar, debes comprender los siguientes conceptos fundamentales sobre el Teams de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="bf0c5-118">Before you begin, you should understand the following fundamental concepts about Teams app development:</span></span>

### <a name="common-app-use-cases"></a><span data-ttu-id="bf0c5-119">Casos comunes de uso de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="bf0c5-119">Common app use cases</span></span>

<span data-ttu-id="bf0c5-120">Algunos escenarios típicos con los que una aplicación Teams personalizada puede ayudar son:</span><span class="sxs-lookup"><span data-stu-id="bf0c5-120">Some typical scenarios that a custom Teams app can help with are:</span></span>

* <span data-ttu-id="bf0c5-121">Inserte contenido basado en web, como una aplicación web o parte de un sitio web, en el Teams cliente.</span><span class="sxs-lookup"><span data-stu-id="bf0c5-121">Embed web-based content, such as a web app or part of a website, in the Teams client.</span></span>
* <span data-ttu-id="bf0c5-122">Busque información rápidamente en otro sistema y adición a una Teams conversación.</span><span class="sxs-lookup"><span data-stu-id="bf0c5-122">Look up information quickly in another system and adding it to a Teams conversation.</span></span>
* <span data-ttu-id="bf0c5-123">Desencadenar flujos de trabajo y procesos directamente desde lo que se dice en una conversación.</span><span class="sxs-lookup"><span data-stu-id="bf0c5-123">Trigger workflows and processes directly from what's said in a conversation.</span></span>

### <a name="app-capabilities-and-tools"></a><span data-ttu-id="bf0c5-124">Herramientas y funcionalidades de la aplicación</span><span class="sxs-lookup"><span data-stu-id="bf0c5-124">App capabilities and tools</span></span>

<span data-ttu-id="bf0c5-125">Una aplicación está integrada por uno o más Teams capacidades y puntos de interacción del usuario.</span><span class="sxs-lookup"><span data-stu-id="bf0c5-125">An app is made up of one or more Teams capabilities and user interaction points.</span></span> <span data-ttu-id="bf0c5-126">El conjunto de herramientas de desarrollo variará en función de las capacidades que desee.</span><span class="sxs-lookup"><span data-stu-id="bf0c5-126">Your development toolset will vary depending on the capabilities you want.</span></span>

| <span data-ttu-id="bf0c5-127">**Funcionalidades de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="bf0c5-127">**App capabilities**</span></span>| <span data-ttu-id="bf0c5-128">**Puntos de interacción**</span><span class="sxs-lookup"><span data-stu-id="bf0c5-128">**Interaction points**</span></span> | <span data-ttu-id="bf0c5-129">**Herramientas recomendadas**</span><span class="sxs-lookup"><span data-stu-id="bf0c5-129">**Recommended tools**</span></span> | <span data-ttu-id="bf0c5-130">**SDK**</span><span class="sxs-lookup"><span data-stu-id="bf0c5-130">**SDKs**</span></span> | <span data-ttu-id="bf0c5-131">**Pilas de tecnología**</span><span class="sxs-lookup"><span data-stu-id="bf0c5-131">**Technology stacks**</span></span> |
|--------|--------|--------|--------|--------|
| <span data-ttu-id="bf0c5-132">Pestañas</span><span class="sxs-lookup"><span data-stu-id="bf0c5-132">Tabs</span></span> | <span data-ttu-id="bf0c5-133">Espacios donde los usuarios pueden interactuar con el contenido web incrustado en contextos personales y compartidos.</span><span class="sxs-lookup"><span data-stu-id="bf0c5-133">Spaces where users can interact with embedded web content in personal and shared contexts.</span></span> | <span data-ttu-id="bf0c5-134">VS Code con Teams Toolkit o generador de Yeoman</span><span class="sxs-lookup"><span data-stu-id="bf0c5-134">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="bf0c5-135">SDK para cliente de JavaScript en Teams</span><span class="sxs-lookup"><span data-stu-id="bf0c5-135">Teams JavaScript client SDK</span></span> | <span data-ttu-id="bf0c5-136">Tecnologías web generales (HTML, CSS y JavaScript) o React.js</span><span class="sxs-lookup"><span data-stu-id="bf0c5-136">General web technologies (HTML, CSS, and JavaScript) or React.js</span></span> |
| <span data-ttu-id="bf0c5-137">Bots</span><span class="sxs-lookup"><span data-stu-id="bf0c5-137">Bots</span></span> | <span data-ttu-id="bf0c5-138">Bots de chat que interactúan con usuarios en contextos personales y compartidos.</span><span class="sxs-lookup"><span data-stu-id="bf0c5-138">Chatbots that interact with users in personal and shared contexts.</span></span> | <span data-ttu-id="bf0c5-139">VS Code con Teams Toolkit o generador de Yeoman</span><span class="sxs-lookup"><span data-stu-id="bf0c5-139">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="bf0c5-140">Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="bf0c5-140">Bot Framework SDK</span></span> | <span data-ttu-id="bf0c5-141">Node.js, C# o Python</span><span class="sxs-lookup"><span data-stu-id="bf0c5-141">Node.js, C#, or Python</span></span> | 
| <span data-ttu-id="bf0c5-142">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="bf0c5-142">Messaging extensions</span></span> | <span data-ttu-id="bf0c5-143">Accesos directos para insertar contenido de la aplicación o actuar en un mensaje sin salir de la conversación.</span><span class="sxs-lookup"><span data-stu-id="bf0c5-143">Shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span> | <span data-ttu-id="bf0c5-144">VS Code con Teams Toolkit o generador de Yeoman</span><span class="sxs-lookup"><span data-stu-id="bf0c5-144">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="bf0c5-145">Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="bf0c5-145">Bot Framework SDK</span></span> | <span data-ttu-id="bf0c5-146">Node.js, C# o Python</span><span class="sxs-lookup"><span data-stu-id="bf0c5-146">Node.js, C#, or Python</span></span> |

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="bf0c5-147">Teams no hospeda la aplicación</span><span class="sxs-lookup"><span data-stu-id="bf0c5-147">Teams doesn't host your app</span></span>

<span data-ttu-id="bf0c5-148">Cuando un usuario instala la aplicación en Teams, solo instala un paquete de aplicación que contiene un archivo de configuración (también conocido como manifiesto de aplicación) y los iconos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bf0c5-148">When a user installs your app in Teams, they only install an app package that contains a configuration file (also known as an app manifest) and your app’s icons.</span></span> <span data-ttu-id="bf0c5-149">La lógica y el almacenamiento de datos de la aplicación se hospedan en otro lugar, como Azure Web Services o localhost durante el desarrollo.</span><span class="sxs-lookup"><span data-stu-id="bf0c5-149">Your app’s logic and data storage are hosted elsewhere, such as Azure Web Services or localhost during development.</span></span> <span data-ttu-id="bf0c5-150">Teams accede a estos recursos a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bf0c5-150">Teams accesses these resources via HTTPS.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="La ilustración que muestra la aplicación en Teams está apuntando a la lógica de la aplicación en el servidor en la nube.":::

## <a name="next-step"></a><span data-ttu-id="bf0c5-152">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="bf0c5-152">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bf0c5-153">Compilación y ejecución de la primera Teams aplicación</span><span class="sxs-lookup"><span data-stu-id="bf0c5-153">Build and run your first Teams app</span></span>](../build-your-first-app/build-and-run.md)

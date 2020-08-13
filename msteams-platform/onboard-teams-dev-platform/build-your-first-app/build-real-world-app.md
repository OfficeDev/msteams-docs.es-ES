---
title: Compilar la primera aplicación de Microsoft Teams
author: heath-hamilton
description: Tutorial para crear una aplicación de Microsoft Teams en el mundo real
ms.openlocfilehash: 4915dde4ef5a852f4fc5d1e4c83e3349db2eaf6b
ms.sourcegitcommit: 80bf79a952bb14cbc38c0bd1e3cf8a346158e28e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2020
ms.locfileid: "46655677"
---
# <a name="learn-how-to-build-your-first-teams-app"></a><span data-ttu-id="8e821-103">Obtenga información sobre cómo crear su primera aplicación de Teams</span><span class="sxs-lookup"><span data-stu-id="8e821-103">Learn how to build your first Teams app</span></span>

<span data-ttu-id="8e821-104">En **compilar la primera aplicación**, aprenderá a crear una aplicación básica de Teams a través de tutoriales.</span><span class="sxs-lookup"><span data-stu-id="8e821-104">In **Build your first app**, you learn how to create a basic Teams app through tutorials.</span></span> <span data-ttu-id="8e821-105">Las lecciones se compilan unas a otras, que le guiarán por cada paso de la creación de una aplicación sencilla y real de Teams.</span><span class="sxs-lookup"><span data-stu-id="8e821-105">The lessons build on each other, walking you through each step of creating a simple, real-world Teams app.</span></span> <span data-ttu-id="8e821-106">Le presentamos las herramientas comunes, conceptos fundamentales y vínculos útiles a lo largo del proceso.</span><span class="sxs-lookup"><span data-stu-id="8e821-106">We introduce you to common tools, fundamental concepts, and useful links along the way.</span></span>

<span data-ttu-id="8e821-107">Empezar? creando y ejecutando una "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="8e821-107">You'll start with creating and running a "Hello, World!"</span></span> <span data-ttu-id="8e821-108">aplicación de pestañas.</span><span class="sxs-lookup"><span data-stu-id="8e821-108">tab app.</span></span> <span data-ttu-id="8e821-109">A continuación, creará una interfaz de usuario sencilla y aprenderá a obtener un contexto útil con el SDK de JavaScript de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8e821-109">You'll then create some simple UI and learn how to get useful context with the Microsoft Teams Javascript SDK.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="8e821-110">Qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="8e821-110">What you'll learn</span></span>

> [!div class="checklist"]
  >
  > - <span data-ttu-id="8e821-111">**Póngase en marcha rápidamente con Team Toolkit**: el kit de herramientas de Microsoft Teams para Visual Studio Code se encarga de crear el proyecto de la aplicación y el scaffolding para que pueda tener una aplicación en ejecución en minutos.</span><span class="sxs-lookup"><span data-stu-id="8e821-111">**Get up and running quickly with the Teams Toolkit**: The Microsoft Teams Toolkit for Visual Studio Code takes care of creating your app project and scaffolding so you can have a running app in minutes.</span></span>
  > - <span data-ttu-id="8e821-112">**Definir la aplicación con el manifiesto**: el manifiesto es un plano en el que se especifican las capacidades y los servicios que usa la aplicación de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8e821-112">**Define your app with the manifest**: The manifest is a blueprint where you specify the capabilities and services your Teams app uses.</span></span>
  > - <span data-ttu-id="8e821-113">**Alcance su público**: puede crear una aplicación de Microsoft Teams para uso o colaboración personal.</span><span class="sxs-lookup"><span data-stu-id="8e821-113">**Scope your audience**: You can build a Teams app for personal use or collaboration.</span></span> <span data-ttu-id="8e821-114">En los tutoriales, aprenderá a crear una pestaña para usuarios individuales o a un grupo de personas en un canal o chat.</span><span class="sxs-lookup"><span data-stu-id="8e821-114">In the tutorials, you'll learn how build a tab for individual users or a group of people in a channel or chat.</span></span>
  > - <span data-ttu-id="8e821-115">**Usar Teams SDK para obtener contexto**: Aprenda a usar el SDK de JavaScript de Microsoft Teams para realizar cambios de tema o configurar la experiencia de configuración.</span><span class="sxs-lookup"><span data-stu-id="8e821-115">**Utilize Teams SDK to get context**: Learn how to use the Microsoft Teams JavaScript SDK to perform theme change or set up configuration experience</span></span>  
  > - <span data-ttu-id="8e821-116">**Amplíe en su aplicación**: a lo largo de los tutoriales, nos vinculamos a temas relacionados que probablemente le interesen (algunos de los cuales incluyen directrices de autenticación y de diseño).</span><span class="sxs-lookup"><span data-stu-id="8e821-116">**Expand on your app**: Throughout the tutorials, we link to related topics you're probably interested in (some of which include authentication and design guidelines).</span></span>

## <a name="teams-app-fundamentals"></a><span data-ttu-id="8e821-117">Conceptos básicos de las aplicaciones de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8e821-117">Teams app fundamentals</span></span>

<span data-ttu-id="8e821-118">Antes de empezar con los tutoriales, debe conocer lo siguiente acerca de la creación de aplicaciones para Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8e821-118">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="apps-can-have-multiple-capabilities"></a><span data-ttu-id="8e821-119">Las aplicaciones pueden tener varias funcionalidades</span><span class="sxs-lookup"><span data-stu-id="8e821-119">Apps can have multiple capabilities</span></span>

<span data-ttu-id="8e821-120">Las aplicaciones de Microsoft Teams se componen de una o varias [capacidades de plataforma](../capabilities-overview.md), como [fichas](../doc-links/what-are-tabs.md), [bots](../doc-links/what-are-bots.md ), [extensiones de mensajería](../doc-links/what-are-messaging-extensions.md)y [webhooks y conectores](../doc-links/what-are-webhooks-and-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="8e821-120">Teams apps are made up of one or more [platform capabilities](../capabilities-overview.md), including [tabs](../doc-links/what-are-tabs.md), [bots](../doc-links/what-are-bots.md ), [messaging extensions](../doc-links/what-are-messaging-extensions.md), and [webhooks and connectors](../doc-links/what-are-webhooks-and-connectors.md).</span></span> <span data-ttu-id="8e821-121">Las aplicaciones de Microsoft Teams también tienen muchas [convenciones y elementos](../doc-links/teams-ui-conventions.md)de la interfaz de usuario, como tarjetas, módulos de tareas y vínculos profundos, que puede usar para crear la mejor experiencia de usuario posible.</span><span class="sxs-lookup"><span data-stu-id="8e821-121">Teams apps also have many [UI conventions and elements](../doc-links/teams-ui-conventions.md), such as cards, task modules, and deep linking, you can use to build the best possible user experience.</span></span>

<span data-ttu-id="8e821-122">Para estos tutoriales, compilaremos solo las pestañas, pero puede Agregar un bot u otra función a la aplicación como desee.</span><span class="sxs-lookup"><span data-stu-id="8e821-122">For these tutorials, you'll build only tabs but can add a bot or other capability to your app as you like.</span></span>

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="8e821-123">Microsoft Teams no hospeda la aplicación</span><span class="sxs-lookup"><span data-stu-id="8e821-123">Teams doesn't host your app</span></span>  

<span data-ttu-id="8e821-124">Una aplicación de Microsoft Teams consta de tres partes principales:</span><span class="sxs-lookup"><span data-stu-id="8e821-124">A Teams app consists of three major pieces:</span></span>

1. <span data-ttu-id="8e821-125">El cliente de Microsoft Teams (Web, escritorio o móvil) donde los usuarios interactúan con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8e821-125">The Microsoft Teams client (web, desktop, or mobile) where users interact with your app.</span></span>
1. <span data-ttu-id="8e821-126">La aplicación, el servicio, el flujo de trabajo o el sitio web que realiza la lógica, el almacenamiento de datos y las llamadas API necesarias para potenciar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8e821-126">Your app, service, workflow, or website that performs the necessary logic, data storage, and API calls to power your app.</span></span>
1. <span data-ttu-id="8e821-127">El paquete de la aplicación, que se usa para instalar la aplicación en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8e821-127">Your app package, which you use to install the app in Teams.</span></span> <span data-ttu-id="8e821-128">Contiene los metadatos de la aplicación (nombre, iconos, etc.) y punteros a los servicios.</span><span class="sxs-lookup"><span data-stu-id="8e821-128">It contains app metadata (name, icons, etc.) and pointers to your services.</span></span>

## <a name="next-step"></a><span data-ttu-id="8e821-129">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="8e821-129">Next step</span></span>

<span data-ttu-id="8e821-130">Para ahora, vamos a empezar.</span><span class="sxs-lookup"><span data-stu-id="8e821-130">That's all for now, let's get started!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8e821-131">Compilar y ejecutar la primera aplicación</span><span class="sxs-lookup"><span data-stu-id="8e821-131">Build and run your first app</span></span>](build-and-run-with-toolkit.md)

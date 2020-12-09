---
title: Diseño de la aplicación personalizada
author: heath-hamilton
description: Obtenga información sobre cómo diseñar aplicaciones de Microsoft Teams. Los recursos incluyen el kit de IU de Microsoft Teams, procedimientos recomendados, ejemplos y mucho más.
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 0160a59ed4ebc51e900acbb5d74735ccae0b6083
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2020
ms.locfileid: "49606271"
---
# <a name="designing-your-microsoft-teams-app"></a><span data-ttu-id="3e003-104">Diseño de la aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3e003-104">Designing your Microsoft Teams app</span></span>

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Imagen conceptual que presenta las directrices de diseño de Microsoft Teams.":::

<span data-ttu-id="3e003-106">Tanto si es un diseñador, un jefe de producto, un programador o un fabricante con herramientas de bajo código, estas instrucciones pueden ayudarle a tomar rápidamente las decisiones de diseño adecuadas para su aplicación de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3e003-106">Whether you're a designer, product manager, developer, or maker using low-code tools, these guidelines can help you quickly make the right design decisions for your Microsoft Teams app.</span></span>

## <a name="teams-app-design-principles"></a><span data-ttu-id="3e003-107">Principios de diseño de aplicaciones de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3e003-107">Teams app design principles</span></span>

<span data-ttu-id="3e003-108">Las aplicaciones de Microsoft Teams ayudan a los usuarios a lograr más juntos.</span><span class="sxs-lookup"><span data-stu-id="3e003-108">Teams apps help people achieve more together.</span></span> <span data-ttu-id="3e003-109">Use estos principios para guiar el diseño.</span><span class="sxs-lookup"><span data-stu-id="3e003-109">Use these principles to guide your design.</span></span>

:::row:::
   :::column span="":::

### <a name="collaborative"></a><span data-ttu-id="3e003-110">Collaborative</span><span class="sxs-lookup"><span data-stu-id="3e003-110">Collaborative</span></span>

<span data-ttu-id="3e003-111">Las aplicaciones de Microsoft Teams ayudan a los usuarios a lograr más juntos.</span><span class="sxs-lookup"><span data-stu-id="3e003-111">Teams apps help people achieve more together.</span></span> <span data-ttu-id="3e003-112">Use estos principios para guiar el diseño.</span><span class="sxs-lookup"><span data-stu-id="3e003-112">Use these principles to guide your design.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a><span data-ttu-id="3e003-113">Iniciativa</span><span class="sxs-lookup"><span data-stu-id="3e003-113">Trustworthy</span></span>

<span data-ttu-id="3e003-114">La aplicación está protegida y es compatible.</span><span class="sxs-lookup"><span data-stu-id="3e003-114">The app is secure and compliant.</span></span> <span data-ttu-id="3e003-115">Los usuarios pueden encontrar fácilmente información sobre privacidad.</span><span class="sxs-lookup"><span data-stu-id="3e003-115">Users can easily find information about privacy.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a><span data-ttu-id="3e003-116">Globalmente inclusivo</span><span class="sxs-lookup"><span data-stu-id="3e003-116">Globally inclusive</span></span>

<span data-ttu-id="3e003-117">Las personas de todos los fondos, skillsets y disciplinas pueden usar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e003-117">People of all backgrounds, skillsets, and disciplines can use the app.</span></span> <span data-ttu-id="3e003-118">Es cultural, racial y social Awareo.</span><span class="sxs-lookup"><span data-stu-id="3e003-118">It’s culturally, racially, and socially aware.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="light"></a><span data-ttu-id="3e003-119">Leve</span><span class="sxs-lookup"><span data-stu-id="3e003-119">Light</span></span>

<span data-ttu-id="3e003-120">La aplicación se centra en los escenarios principales que se fusionan con los flujos de trabajo de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3e003-120">The app focuses on core scenarios that blend with Teams workflows.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a><span data-ttu-id="3e003-121">Nativo o distinto</span><span class="sxs-lookup"><span data-stu-id="3e003-121">Native or distinct</span></span>

<span data-ttu-id="3e003-122">La aplicación usa los componentes de diseño de equipos nativos o los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="3e003-122">The app uses native Teams design components or your own.</span></span> <span data-ttu-id="3e003-123">No hay ninguna combinación de combinaciones de colores, controles, etc.</span><span class="sxs-lookup"><span data-stu-id="3e003-123">There’s no blend of color schemes, controls, etc.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="useful"></a><span data-ttu-id="3e003-124">Result</span><span class="sxs-lookup"><span data-stu-id="3e003-124">Useful</span></span>

<span data-ttu-id="3e003-125">La aplicación se basa en un escenario en el que los usuarios deben hacer en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3e003-125">The app is based on a scenario people need to do in Teams.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a><span data-ttu-id="3e003-126">Fácil de usar</span><span class="sxs-lookup"><span data-stu-id="3e003-126">Easy to use</span></span>

<span data-ttu-id="3e003-127">La interfaz de usuario es fácil de entender, agradable en apariencia y tono, y hace que los usuarios sean más productivos.</span><span class="sxs-lookup"><span data-stu-id="3e003-127">The UI is easy to understand, pleasant in look and tone, and makes people more productive.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a><span data-ttu-id="3e003-128">Respuesta correcta</span><span class="sxs-lookup"><span data-stu-id="3e003-128">Responsive</span></span>

<span data-ttu-id="3e003-129">La aplicación es independiente del dispositivo y de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="3e003-129">The app is device and screen agnostic.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a><span data-ttu-id="3e003-130">Accesible</span><span class="sxs-lookup"><span data-stu-id="3e003-130">Accessible</span></span>

<span data-ttu-id="3e003-131">La aplicación cumple los requisitos de accesibilidad de Microsoft Teams en términos de contraste de color, alternativas de navegación y mucho más.</span><span class="sxs-lookup"><span data-stu-id="3e003-131">The app meets Teams accessibility requirements in terms of color contrast, navigation alternatives, and more.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a><span data-ttu-id="3e003-132">Bien descrito</span><span class="sxs-lookup"><span data-stu-id="3e003-132">Well described</span></span>

<span data-ttu-id="3e003-133">El texto, los iconos y las imágenes hacen que resulte claro para qué sirve la aplicación y cómo usarla.</span><span class="sxs-lookup"><span data-stu-id="3e003-133">Text, icons, and images make it clear what the app is for and how to use it.</span></span>

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a><span data-ttu-id="3e003-134">Crear una experiencia cohesiva</span><span class="sxs-lookup"><span data-stu-id="3e003-134">Creating a cohesive experience</span></span>

<span data-ttu-id="3e003-135">El diseño de una aplicación de Microsoft Teams es como el diseño de una aplicación web convencional, pero también un poco diferente.</span><span class="sxs-lookup"><span data-stu-id="3e003-135">Designing a Teams app is like designing a conventional web app—but also a little different.</span></span> <span data-ttu-id="3e003-136">Un diseño efectivo resalta los atributos únicos de la aplicación al ajustarse de forma natural con las características y contextos de Teams.</span><span class="sxs-lookup"><span data-stu-id="3e003-136">An effective design highlights your app's unique attributes while fitting naturally with Teams features and contexts.</span></span>

<span data-ttu-id="3e003-137">Estas instrucciones y recursos pueden ayudarle a golpear ese equilibrio.</span><span class="sxs-lookup"><span data-stu-id="3e003-137">These guidelines and resources can help you strike that balance.</span></span> <span data-ttu-id="3e003-138">Sabrá qué hacer y qué evitar al diseñar la aplicación de Microsoft Teams (como la navegación de varios niveles en una pestaña).</span><span class="sxs-lookup"><span data-stu-id="3e003-138">You'll know what to do and what to avoid when designing your Teams app (such as multi-level navigation in a tab).</span></span>

## <a name="planning-your-app"></a><span data-ttu-id="3e003-139">Planeación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="3e003-139">Planning your app</span></span>

<span data-ttu-id="3e003-140">Para diseñar una aplicación de Microsoft Teams de alta calidad, primero debe comprender lo que desea que haga la aplicación y cómo cree que los usuarios la usarán.</span><span class="sxs-lookup"><span data-stu-id="3e003-140">To design a high-quality Teams app, you must first understand what you want your app to do and how you think people will use it.</span></span> <span data-ttu-id="3e003-141">Si aún no lo ha hecho, dedique algún tiempo a [planear correctamente la aplicación](../../concepts/extensibility-points.md).</span><span class="sxs-lookup"><span data-stu-id="3e003-141">If you haven't already, take some time to properly [plan your app](../../concepts/extensibility-points.md).</span></span>

## <a name="design-fundamentals"></a><span data-ttu-id="3e003-142">Conceptos básicos sobre el diseño</span><span class="sxs-lookup"><span data-stu-id="3e003-142">Design fundamentals</span></span>

<span data-ttu-id="3e003-143">Obtenga información sobre los [conceptos básicos del diseño de aplicaciones de Microsoft Teams](design-teams-app-fundamentals.md), incluido el diseño, las combinaciones de colores y mucho más.</span><span class="sxs-lookup"><span data-stu-id="3e003-143">Learn the [fundamentals of Teams app design](design-teams-app-fundamentals.md), including layout, color schemes, and more.</span></span>

## <a name="basic-fluent-ui-components-for-teams"></a><span data-ttu-id="3e003-144">Componentes básicos de la interfaz de usuario Fluent para Teams</span><span class="sxs-lookup"><span data-stu-id="3e003-144">Basic Fluent UI components for Teams</span></span>

<span data-ttu-id="3e003-145">En función de la interfaz de usuario de Fluent, estos son los [elementos básicos para crear interfaces de equipo conocidas](design-teams-app-basic-ui-components.md).</span><span class="sxs-lookup"><span data-stu-id="3e003-145">Based on Fluent UI, these are the [core elements for creating familiar Teams interfaces](design-teams-app-basic-ui-components.md).</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="3e003-146">Capacidades de la aplicación</span><span class="sxs-lookup"><span data-stu-id="3e003-146">App capabilities</span></span>

<span data-ttu-id="3e003-147">Comprenda cómo los usuarios agregan, usan y administran las aplicaciones de Microsoft Teams para aprovechar al máximo cada una de las funciones de su diseño.</span><span class="sxs-lookup"><span data-stu-id="3e003-147">Understand how people add, use, and manage Teams apps to make the most of each capability in your design.</span></span>

* [<span data-ttu-id="3e003-148">Aplicaciones personales</span><span class="sxs-lookup"><span data-stu-id="3e003-148">Personal apps</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="3e003-149">Pestañas</span><span class="sxs-lookup"><span data-stu-id="3e003-149">Tabs</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="3e003-150">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="3e003-150">Messaging extensions</span></span>](../../messaging-extensions/design/messaging-extension-design.md)
* [<span data-ttu-id="3e003-151">Bots</span><span class="sxs-lookup"><span data-stu-id="3e003-151">Bots</span></span>](../../bots/design/bots.md)
* [<span data-ttu-id="3e003-152">Extensiones de reunión</span><span class="sxs-lookup"><span data-stu-id="3e003-152">Meeting extensions</span></span>](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [<span data-ttu-id="3e003-153">Módulos de tareas</span><span class="sxs-lookup"><span data-stu-id="3e003-153">Task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [<span data-ttu-id="3e003-154">Tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="3e003-154">Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="ui-templates"></a><span data-ttu-id="3e003-155">Plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="3e003-155">UI templates</span></span>

<span data-ttu-id="3e003-156">Cree rápidamente diseños complejos y de alta fidelidad con [plantillas para los casos de uso y los flujos de trabajo de los equipos comunes](design-teams-app-ui-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3e003-156">Quickly create complex, high-fidelity designs with [templates for common Teams use cases and workflows](design-teams-app-ui-templates.md).</span></span>

## <a name="get-started-with-the-microsoft-teams-ui-kit"></a><span data-ttu-id="3e003-157">Introducción al kit de la interfaz de usuario de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3e003-157">Get started with the Microsoft Teams UI Kit</span></span>

<span data-ttu-id="3e003-158">El kit de interfaz de usuario de Microsoft Teams tiene componentes, plantillas y ejemplos de la interfaz de usuario que puede arrastrar, colocar y modificar según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3e003-158">The Microsoft Teams UI Kit has UI components, templates, and examples that you can drag, drop, and modify as needed.</span></span> <span data-ttu-id="3e003-159">El kit de interfaz de usuario también incluye información completa sobre cómo las aplicaciones deben tener el aspecto y el comportamiento en diferentes escenarios de Teams.</span><span class="sxs-lookup"><span data-stu-id="3e003-159">The UI kit also includes comprehensive information about how apps should look and behave in different Teams scenarios.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3e003-160">Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="3e003-160">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="other-resources"></a><span data-ttu-id="3e003-161">Otros recursos</span><span class="sxs-lookup"><span data-stu-id="3e003-161">Other resources</span></span>

<span data-ttu-id="3e003-162">Para obtener más información, pruebe uno de los siguientes recursos.</span><span class="sxs-lookup"><span data-stu-id="3e003-162">To learn more, try one of the following resources.</span></span>

### <a name="fluent-ui"></a><span data-ttu-id="3e003-163">Interfaz de usuario Fluent</span><span class="sxs-lookup"><span data-stu-id="3e003-163">Fluent UI</span></span>

<span data-ttu-id="3e003-164">Obtenga ejemplos de código y detalles de implementación para los componentes basados en la interfaz de usuario fluida que se usan para crear experiencias de Teams.</span><span class="sxs-lookup"><span data-stu-id="3e003-164">Get code samples and implementation details for the Fluent UI-based components used to build Teams experiences.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3e003-165">Probar los componentes de la interfaz de usuario de Microsoft Teams (interfaz de usuario Fluent)</span><span class="sxs-lookup"><span data-stu-id="3e003-165">Try out Teams UI components (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a><span data-ttu-id="3e003-166">Diseñador de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="3e003-166">Adaptive Cards designer</span></span>

<span data-ttu-id="3e003-167">Diseñar tarjetas adaptables en una herramienta basada en Web.</span><span class="sxs-lookup"><span data-stu-id="3e003-167">Design Adaptive Cards in a web-based tool.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3e003-168">Pruebe el diseñador de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="3e003-168">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

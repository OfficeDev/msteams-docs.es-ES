---
title: Diseño de la aplicación personalizada
author: heath-hamilton
description: Obtén información sobre cómo diseñar Microsoft Teams aplicaciones. Los recursos incluyen el kit Microsoft Teams interfaz de usuario, procedimientos recomendados, ejemplos y mucho más.
localization_priority: Normal
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 19b8f8cbcbc52aa02ccd5d94f5bc4c088f2ae28a
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644878"
---
# <a name="designing-your-microsoft-teams-app"></a><span data-ttu-id="1aec9-104">Diseño de la Microsoft Teams aplicación</span><span class="sxs-lookup"><span data-stu-id="1aec9-104">Designing your Microsoft Teams app</span></span>

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Imagen conceptual que presenta las Microsoft Teams de diseño.":::

<span data-ttu-id="1aec9-106">Independientemente de si eres diseñador, jefe de producto, desarrollador o creador con herramientas de código bajo, estas directrices pueden ayudarte a tomar rápidamente las decisiones de diseño adecuadas para tu Microsoft Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="1aec9-106">Whether you're a designer, product manager, developer, or maker using low-code tools, these guidelines can help you quickly make the right design decisions for your Microsoft Teams app.</span></span>

## <a name="creating-a-cohesive-experience"></a><span data-ttu-id="1aec9-107">Creación de una experiencia cohesiva</span><span class="sxs-lookup"><span data-stu-id="1aec9-107">Creating a cohesive experience</span></span>

<span data-ttu-id="1aec9-108">Diseñar una aplicación Teams es como diseñar una aplicación web convencional, pero también un poco diferente.</span><span class="sxs-lookup"><span data-stu-id="1aec9-108">Designing a Teams app is like designing a conventional web app—but also a little different.</span></span> <span data-ttu-id="1aec9-109">Un diseño eficaz resalta los atributos únicos de la aplicación mientras se adapta de forma natural a Teams características y contextos.</span><span class="sxs-lookup"><span data-stu-id="1aec9-109">An effective design highlights your app's unique attributes while fitting naturally with Teams features and contexts.</span></span>

<span data-ttu-id="1aec9-110">Estas directrices y recursos pueden ayudarle a encontrar ese equilibrio.</span><span class="sxs-lookup"><span data-stu-id="1aec9-110">These guidelines and resources can help you strike that balance.</span></span> <span data-ttu-id="1aec9-111">Sabrás qué hacer y qué evitar al diseñar la aplicación Teams (como la navegación de varios niveles en una pestaña).</span><span class="sxs-lookup"><span data-stu-id="1aec9-111">You'll know what to do and what to avoid when designing your Teams app (such as multi-level navigation in a tab).</span></span>

## <a name="teams-app-design-principles"></a><span data-ttu-id="1aec9-112">Teams de diseño de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="1aec9-112">Teams app design principles</span></span>

<span data-ttu-id="1aec9-113">Teams aplicaciones ayudan a los usuarios a lograr más juntos.</span><span class="sxs-lookup"><span data-stu-id="1aec9-113">Teams apps help people achieve more together.</span></span> <span data-ttu-id="1aec9-114">Use estos principios para guiar el diseño.</span><span class="sxs-lookup"><span data-stu-id="1aec9-114">Use these principles to guide your design.</span></span>

:::row:::
   :::column span="":::

### <a name="collaborative"></a><span data-ttu-id="1aec9-115">Colaboración</span><span class="sxs-lookup"><span data-stu-id="1aec9-115">Collaborative</span></span>

<span data-ttu-id="1aec9-116">Teams aplicaciones ayudan a los usuarios a lograr más juntos.</span><span class="sxs-lookup"><span data-stu-id="1aec9-116">Teams apps help people achieve more together.</span></span> <span data-ttu-id="1aec9-117">Use estos principios para guiar el diseño.</span><span class="sxs-lookup"><span data-stu-id="1aec9-117">Use these principles to guide your design.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a><span data-ttu-id="1aec9-118">Confiable</span><span class="sxs-lookup"><span data-stu-id="1aec9-118">Trustworthy</span></span>

<span data-ttu-id="1aec9-119">La aplicación es segura y compatible.</span><span class="sxs-lookup"><span data-stu-id="1aec9-119">The app is secure and compliant.</span></span> <span data-ttu-id="1aec9-120">Los usuarios pueden encontrar fácilmente información sobre privacidad.</span><span class="sxs-lookup"><span data-stu-id="1aec9-120">Users can easily find information about privacy.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a><span data-ttu-id="1aec9-121">Globalmente inclusiva</span><span class="sxs-lookup"><span data-stu-id="1aec9-121">Globally inclusive</span></span>

<span data-ttu-id="1aec9-122">Las personas de todos los orígenes, conjuntos de aptitudes y disciplinas pueden usar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1aec9-122">People of all backgrounds, skillsets, and disciplines can use the app.</span></span> <span data-ttu-id="1aec9-123">Es cultural, racial y socialmente consciente.</span><span class="sxs-lookup"><span data-stu-id="1aec9-123">It’s culturally, racially, and socially aware.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="light"></a><span data-ttu-id="1aec9-124">Leve</span><span class="sxs-lookup"><span data-stu-id="1aec9-124">Light</span></span>

<span data-ttu-id="1aec9-125">La aplicación se centra en escenarios principales que se combinan con Teams flujos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="1aec9-125">The app focuses on core scenarios that blend with Teams workflows.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a><span data-ttu-id="1aec9-126">Nativo o distinto</span><span class="sxs-lookup"><span data-stu-id="1aec9-126">Native or distinct</span></span>

<span data-ttu-id="1aec9-127">La aplicación usa componentes Teams diseño nativos o propios.</span><span class="sxs-lookup"><span data-stu-id="1aec9-127">The app uses native Teams design components or your own.</span></span> <span data-ttu-id="1aec9-128">No hay una combinación de esquemas de color, controles, entre otras.</span><span class="sxs-lookup"><span data-stu-id="1aec9-128">There’s no blend of color schemes, controls, and so on.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="useful"></a><span data-ttu-id="1aec9-129">Útil</span><span class="sxs-lookup"><span data-stu-id="1aec9-129">Useful</span></span>

<span data-ttu-id="1aec9-130">La aplicación se basa en un escenario que los usuarios deben hacer en Teams.</span><span class="sxs-lookup"><span data-stu-id="1aec9-130">The app is based on a scenario people need to do in Teams.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a><span data-ttu-id="1aec9-131">Fácil de usar</span><span class="sxs-lookup"><span data-stu-id="1aec9-131">Easy to use</span></span>

<span data-ttu-id="1aec9-132">La interfaz de usuario es fácil de entender, agradable en apariencia y tono, y hace que las personas sean más productivas.</span><span class="sxs-lookup"><span data-stu-id="1aec9-132">The UI is easy to understand, pleasant in look and tone, and makes people more productive.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a><span data-ttu-id="1aec9-133">Respuesta correcta</span><span class="sxs-lookup"><span data-stu-id="1aec9-133">Responsive</span></span>

<span data-ttu-id="1aec9-134">La aplicación es independiente del dispositivo y la pantalla.</span><span class="sxs-lookup"><span data-stu-id="1aec9-134">The app is device and screen agnostic.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a><span data-ttu-id="1aec9-135">Accesible</span><span class="sxs-lookup"><span data-stu-id="1aec9-135">Accessible</span></span>

<span data-ttu-id="1aec9-136">La aplicación cumple Teams requisitos de accesibilidad en términos de contraste de color, alternativas de navegación y mucho más.</span><span class="sxs-lookup"><span data-stu-id="1aec9-136">The app meets Teams accessibility requirements in terms of color contrast, navigation alternatives, and more.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a><span data-ttu-id="1aec9-137">Bien descrito</span><span class="sxs-lookup"><span data-stu-id="1aec9-137">Well described</span></span>

<span data-ttu-id="1aec9-138">El texto, los iconos y las imágenes hacen que se aclare para qué está la aplicación y cómo usarla.</span><span class="sxs-lookup"><span data-stu-id="1aec9-138">Text, icons, and images make it clear what the app is for and how to use it.</span></span>

   :::column-end:::
:::row-end:::

## <a name="teams-design-system"></a><span data-ttu-id="1aec9-139">Teams de diseño</span><span class="sxs-lookup"><span data-stu-id="1aec9-139">Teams design system</span></span>

<span data-ttu-id="1aec9-140">Obtén información [sobre los aspectos Teams diseño de la aplicación,](design-teams-app-fundamentals.md)incluido el diseño, las esquemas de color y mucho más.</span><span class="sxs-lookup"><span data-stu-id="1aec9-140">Learn the [fundamentals of Teams app design](design-teams-app-fundamentals.md), including layout, color schemes, and more.</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="1aec9-141">Capacidades de la aplicación</span><span class="sxs-lookup"><span data-stu-id="1aec9-141">App capabilities</span></span>

<span data-ttu-id="1aec9-142">Comprender cómo las personas agregan, usan y administran Teams aplicaciones para aprovechar al máximo cada funcionalidad del diseño.</span><span class="sxs-lookup"><span data-stu-id="1aec9-142">Understand how people add, use, and manage Teams apps to make the most of each capability in your design.</span></span>

* [<span data-ttu-id="1aec9-143">Aplicaciones personales</span><span class="sxs-lookup"><span data-stu-id="1aec9-143">Personal apps</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="1aec9-144">Pestañas</span><span class="sxs-lookup"><span data-stu-id="1aec9-144">Tabs</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="1aec9-145">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="1aec9-145">Messaging extensions</span></span>](../../messaging-extensions/design/messaging-extension-design.md)
* [<span data-ttu-id="1aec9-146">Bots</span><span class="sxs-lookup"><span data-stu-id="1aec9-146">Bots</span></span>](../../bots/design/bots.md)
* [<span data-ttu-id="1aec9-147">Extensiones de reunión</span><span class="sxs-lookup"><span data-stu-id="1aec9-147">Meeting extensions</span></span>](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="ui-templates"></a><span data-ttu-id="1aec9-148">Plantillas de la interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="1aec9-148">UI templates</span></span>

<span data-ttu-id="1aec9-149">Cree rápidamente diseños complejos y de alta fidelidad con plantillas para Teams [casos de uso y flujos de trabajo](design-teams-app-ui-templates.md)comunes.</span><span class="sxs-lookup"><span data-stu-id="1aec9-149">Quickly create complex, high-fidelity designs with [templates for common Teams use cases and workflows](design-teams-app-ui-templates.md).</span></span>

## <a name="basic-ui-components"></a><span data-ttu-id="1aec9-150">Componentes básicos de la interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="1aec9-150">Basic UI components</span></span>

<span data-ttu-id="1aec9-151">Según la interfaz de usuario de Fluent, estos son [los](design-teams-app-basic-ui-components.md) elementos principales que puedes usar para crear experiencias Teams desde cero.</span><span class="sxs-lookup"><span data-stu-id="1aec9-151">Based on Fluent UI, these are the [core elements](design-teams-app-basic-ui-components.md) you can use to create Teams experiences from scratch.</span></span>

## <a name="tools-and-samples"></a><span data-ttu-id="1aec9-152">Herramientas y ejemplos</span><span class="sxs-lookup"><span data-stu-id="1aec9-152">Tools and samples</span></span>

<span data-ttu-id="1aec9-153">Las siguientes herramientas pueden ayudar a los diseñadores y desarrolladores a empezar:</span><span class="sxs-lookup"><span data-stu-id="1aec9-153">The following tools can help designers and developers get started:</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="1aec9-154">Kit de UI de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1aec9-154">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="1aec9-155">Diseña una aplicación Teams con componentes de interfaz de usuario, plantillas y ejemplos que puedas arrastrar, colocar y modificar según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="1aec9-155">Design a Teams app with UI components, templates, and examples that you can drag, drop, and modify as needed.</span></span> <span data-ttu-id="1aec9-156">El kit de interfaz de usuario también incluye información completa sobre cómo deben verse y comportarse las aplicaciones en diferentes Teams escenarios.</span><span class="sxs-lookup"><span data-stu-id="1aec9-156">The UI kit also includes comprehensive information about how apps should look and behave in different Teams scenarios.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1aec9-157">Obtener el kit de interfaz de usuario (Figma)</span><span class="sxs-lookup"><span data-stu-id="1aec9-157">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="1aec9-158">Microsoft Teams Biblioteca de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="1aec9-158">Microsoft Teams UI Library</span></span>

<span data-ttu-id="1aec9-159">Ver y probar plantillas de Teams de interfaz de usuario individuales y componentes relacionados en el explorador.</span><span class="sxs-lookup"><span data-stu-id="1aec9-159">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1aec9-160">Pruebe la biblioteca de interfaz de usuario (área de juegos)</span><span class="sxs-lookup"><span data-stu-id="1aec9-160">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="1aec9-161">Importe estas plantillas y componentes relacionados directamente en el proyecto Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="1aec9-161">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1aec9-162">Obtener la biblioteca de interfaz de usuario (GitHub)</span><span class="sxs-lookup"><span data-stu-id="1aec9-162">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="1aec9-163">Aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1aec9-163">Sample app</span></span>

<span data-ttu-id="1aec9-164">Puedes cargar una aplicación de ejemplo para ver cómo deben verse y comportarse las aplicaciones en el Teams cliente.</span><span class="sxs-lookup"><span data-stu-id="1aec9-164">You can upload a sample app to see how apps should look and behave in the Teams client.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1aec9-165">Obtener la aplicación de ejemplo (GitHub)</span><span class="sxs-lookup"><span data-stu-id="1aec9-165">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a><span data-ttu-id="1aec9-166">Otros recursos</span><span class="sxs-lookup"><span data-stu-id="1aec9-166">Other resources</span></span>

<span data-ttu-id="1aec9-167">Para obtener más información, pruebe uno de los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="1aec9-167">To learn more, try one of the following resources:</span></span>

### <a name="fluent-ui-documentation"></a><span data-ttu-id="1aec9-168">Documentación de la interfaz de usuario fluent</span><span class="sxs-lookup"><span data-stu-id="1aec9-168">Fluent UI documentation</span></span>

<span data-ttu-id="1aec9-169">Obtenga ejemplos de código y detalles de implementación para los componentes básicos de la interfaz de usuario fluent que se usan para crear Teams experiencias.</span><span class="sxs-lookup"><span data-stu-id="1aec9-169">Get code samples and implementation details for the basic Fluent UI components used to build Teams experiences.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1aec9-170">Probar Teams de interfaz de usuario (Fluent UI)</span><span class="sxs-lookup"><span data-stu-id="1aec9-170">Try Teams UI components (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a><span data-ttu-id="1aec9-171">Diseñador de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="1aec9-171">Adaptive Cards designer</span></span>

<span data-ttu-id="1aec9-172">Diseñar tarjetas adaptables en nuestra herramienta basada en web.</span><span class="sxs-lookup"><span data-stu-id="1aec9-172">Design Adaptive Cards in our web-based tool.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1aec9-173">Probar el diseñador de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="1aec9-173">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

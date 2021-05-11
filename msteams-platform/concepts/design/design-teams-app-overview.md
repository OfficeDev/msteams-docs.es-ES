---
title: Diseño de la aplicación personalizada
author: heath-hamilton
description: Obtén información sobre cómo diseñar Microsoft Teams aplicaciones. Los recursos incluyen el kit Microsoft Teams interfaz de usuario, procedimientos recomendados, ejemplos y mucho más.
localization_priority: Normal
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: ab311b6b9b8494308916ef602ee98785ab6de61e
ms.sourcegitcommit: 808a203fb963eeade3a8e32db88d64677e37df7a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2021
ms.locfileid: "52304029"
---
# <a name="designing-your-microsoft-teams-app"></a><span data-ttu-id="0e5b6-104">Diseño de la Microsoft Teams aplicación</span><span class="sxs-lookup"><span data-stu-id="0e5b6-104">Designing your Microsoft Teams app</span></span>

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Imagen conceptual que presenta las Microsoft Teams de diseño.":::

<span data-ttu-id="0e5b6-106">Independientemente de si eres diseñador, jefe de producto, desarrollador o creador con herramientas de código bajo, estas directrices pueden ayudarte a tomar rápidamente las decisiones de diseño adecuadas para tu Microsoft Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-106">Whether you're a designer, product manager, developer, or maker using low-code tools, these guidelines can help you quickly make the right design decisions for your Microsoft Teams app.</span></span>

## <a name="teams-app-design-principles"></a><span data-ttu-id="0e5b6-107">Teams de diseño de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="0e5b6-107">Teams app design principles</span></span>

<span data-ttu-id="0e5b6-108">Teams aplicaciones ayudan a los usuarios a lograr más juntos.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-108">Teams apps help people achieve more together.</span></span> <span data-ttu-id="0e5b6-109">Use estos principios para guiar el diseño.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-109">Use these principles to guide your design.</span></span>

:::row:::
   :::column span="":::

### <a name="collaborative"></a><span data-ttu-id="0e5b6-110">Colaboración</span><span class="sxs-lookup"><span data-stu-id="0e5b6-110">Collaborative</span></span>

<span data-ttu-id="0e5b6-111">Teams aplicaciones ayudan a los usuarios a lograr más juntos.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-111">Teams apps help people achieve more together.</span></span> <span data-ttu-id="0e5b6-112">Use estos principios para guiar el diseño.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-112">Use these principles to guide your design.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a><span data-ttu-id="0e5b6-113">Confiable</span><span class="sxs-lookup"><span data-stu-id="0e5b6-113">Trustworthy</span></span>

<span data-ttu-id="0e5b6-114">La aplicación es segura y compatible.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-114">The app is secure and compliant.</span></span> <span data-ttu-id="0e5b6-115">Los usuarios pueden encontrar fácilmente información sobre privacidad.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-115">Users can easily find information about privacy.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a><span data-ttu-id="0e5b6-116">Globalmente inclusiva</span><span class="sxs-lookup"><span data-stu-id="0e5b6-116">Globally inclusive</span></span>

<span data-ttu-id="0e5b6-117">Las personas de todos los orígenes, conjuntos de aptitudes y disciplinas pueden usar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-117">People of all backgrounds, skillsets, and disciplines can use the app.</span></span> <span data-ttu-id="0e5b6-118">Es cultural, racial y socialmente consciente.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-118">It’s culturally, racially, and socially aware.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="light"></a><span data-ttu-id="0e5b6-119">Leve</span><span class="sxs-lookup"><span data-stu-id="0e5b6-119">Light</span></span>

<span data-ttu-id="0e5b6-120">La aplicación se centra en escenarios principales que se combinan con Teams flujos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-120">The app focuses on core scenarios that blend with Teams workflows.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a><span data-ttu-id="0e5b6-121">Nativo o distinto</span><span class="sxs-lookup"><span data-stu-id="0e5b6-121">Native or distinct</span></span>

<span data-ttu-id="0e5b6-122">La aplicación usa componentes Teams diseño nativos o propios.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-122">The app uses native Teams design components or your own.</span></span> <span data-ttu-id="0e5b6-123">No hay combinación de esquemas de color, controles, etc.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-123">There’s no blend of color schemes, controls, etc.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="useful"></a><span data-ttu-id="0e5b6-124">Útil</span><span class="sxs-lookup"><span data-stu-id="0e5b6-124">Useful</span></span>

<span data-ttu-id="0e5b6-125">La aplicación se basa en un escenario que los usuarios deben hacer en Teams.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-125">The app is based on a scenario people need to do in Teams.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a><span data-ttu-id="0e5b6-126">Fácil de usar</span><span class="sxs-lookup"><span data-stu-id="0e5b6-126">Easy to use</span></span>

<span data-ttu-id="0e5b6-127">La interfaz de usuario es fácil de entender, agradable en apariencia y tono, y hace que las personas sean más productivas.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-127">The UI is easy to understand, pleasant in look and tone, and makes people more productive.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a><span data-ttu-id="0e5b6-128">Respuesta correcta</span><span class="sxs-lookup"><span data-stu-id="0e5b6-128">Responsive</span></span>

<span data-ttu-id="0e5b6-129">La aplicación es independiente del dispositivo y la pantalla.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-129">The app is device and screen agnostic.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a><span data-ttu-id="0e5b6-130">Accesible</span><span class="sxs-lookup"><span data-stu-id="0e5b6-130">Accessible</span></span>

<span data-ttu-id="0e5b6-131">La aplicación cumple Teams requisitos de accesibilidad en términos de contraste de color, alternativas de navegación y mucho más.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-131">The app meets Teams accessibility requirements in terms of color contrast, navigation alternatives, and more.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a><span data-ttu-id="0e5b6-132">Bien descrito</span><span class="sxs-lookup"><span data-stu-id="0e5b6-132">Well described</span></span>

<span data-ttu-id="0e5b6-133">El texto, los iconos y las imágenes hacen que se aclare para qué está la aplicación y cómo usarla.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-133">Text, icons, and images make it clear what the app is for and how to use it.</span></span>

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a><span data-ttu-id="0e5b6-134">Creación de una experiencia cohesiva</span><span class="sxs-lookup"><span data-stu-id="0e5b6-134">Creating a cohesive experience</span></span>

<span data-ttu-id="0e5b6-135">Diseñar una aplicación Teams es como diseñar una aplicación web convencional, pero también un poco diferente.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-135">Designing a Teams app is like designing a conventional web app—but also a little different.</span></span> <span data-ttu-id="0e5b6-136">Un diseño eficaz resalta los atributos únicos de la aplicación mientras se adapta de forma natural a Teams características y contextos.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-136">An effective design highlights your app's unique attributes while fitting naturally with Teams features and contexts.</span></span>

<span data-ttu-id="0e5b6-137">Estas directrices y recursos pueden ayudarle a encontrar ese equilibrio.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-137">These guidelines and resources can help you strike that balance.</span></span> <span data-ttu-id="0e5b6-138">Sabrás qué hacer y qué evitar al diseñar la aplicación Teams (como la navegación de varios niveles en una pestaña).</span><span class="sxs-lookup"><span data-stu-id="0e5b6-138">You'll know what to do and what to avoid when designing your Teams app (such as multi-level navigation in a tab).</span></span>

## <a name="planning-your-app"></a><span data-ttu-id="0e5b6-139">Planeación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="0e5b6-139">Planning your app</span></span>

<span data-ttu-id="0e5b6-140">Para diseñar una aplicación de Teams de alta calidad, primero debes comprender lo que quieres que haga tu aplicación y cómo crees que la usarán las personas.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-140">To design a high-quality Teams app, you must first understand what you want your app to do and how you think people will use it.</span></span> <span data-ttu-id="0e5b6-141">Si aún no lo has hecho, tómese un tiempo para [planear correctamente la aplicación](../../concepts/extensibility-points.md).</span><span class="sxs-lookup"><span data-stu-id="0e5b6-141">If you haven't already, take some time to properly [plan your app](../../concepts/extensibility-points.md).</span></span>

## <a name="design-fundamentals"></a><span data-ttu-id="0e5b6-142">Conceptos básicos de diseño</span><span class="sxs-lookup"><span data-stu-id="0e5b6-142">Design fundamentals</span></span>

<span data-ttu-id="0e5b6-143">Obtén información [sobre los aspectos Teams diseño de la aplicación,](design-teams-app-fundamentals.md)incluido el diseño, las esquemas de color y mucho más.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-143">Learn the [fundamentals of Teams app design](design-teams-app-fundamentals.md), including layout, color schemes, and more.</span></span>

## <a name="basic-fluent-ui-components-for-teams"></a><span data-ttu-id="0e5b6-144">Componentes básicos de la interfaz de usuario fluent para Teams</span><span class="sxs-lookup"><span data-stu-id="0e5b6-144">Basic Fluent UI components for Teams</span></span>

<span data-ttu-id="0e5b6-145">Basados en la interfaz de usuario fluent, estos son los elementos principales para crear interfaces [Teams familiares.](design-teams-app-basic-ui-components.md)</span><span class="sxs-lookup"><span data-stu-id="0e5b6-145">Based on Fluent UI, these are the [core elements for creating familiar Teams interfaces](design-teams-app-basic-ui-components.md).</span></span>

## <a name="ui-templates"></a><span data-ttu-id="0e5b6-146">Plantillas de la interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="0e5b6-146">UI templates</span></span>

<span data-ttu-id="0e5b6-147">Cree rápidamente diseños complejos y de alta fidelidad con plantillas para Teams [casos de uso y flujos de trabajo](design-teams-app-ui-templates.md)comunes.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-147">Quickly create complex, high-fidelity designs with [templates for common Teams use cases and workflows](design-teams-app-ui-templates.md).</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="0e5b6-148">Capacidades de la aplicación</span><span class="sxs-lookup"><span data-stu-id="0e5b6-148">App capabilities</span></span>

<span data-ttu-id="0e5b6-149">Comprender cómo las personas agregan, usan y administran Teams aplicaciones para aprovechar al máximo cada funcionalidad del diseño.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-149">Understand how people add, use, and manage Teams apps to make the most of each capability in your design.</span></span>

* [<span data-ttu-id="0e5b6-150">Aplicaciones personales</span><span class="sxs-lookup"><span data-stu-id="0e5b6-150">Personal apps</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="0e5b6-151">Pestañas</span><span class="sxs-lookup"><span data-stu-id="0e5b6-151">Tabs</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="0e5b6-152">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="0e5b6-152">Messaging extensions</span></span>](../../messaging-extensions/design/messaging-extension-design.md)
* [<span data-ttu-id="0e5b6-153">Bots</span><span class="sxs-lookup"><span data-stu-id="0e5b6-153">Bots</span></span>](../../bots/design/bots.md)
* [<span data-ttu-id="0e5b6-154">Extensiones de reunión</span><span class="sxs-lookup"><span data-stu-id="0e5b6-154">Meeting extensions</span></span>](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [<span data-ttu-id="0e5b6-155">Módulos de tareas</span><span class="sxs-lookup"><span data-stu-id="0e5b6-155">Task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [<span data-ttu-id="0e5b6-156">Tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="0e5b6-156">Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="app-customization"></a><span data-ttu-id="0e5b6-157">Personalización de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="0e5b6-157">App customization</span></span>

<span data-ttu-id="0e5b6-158">Comprenda cómo el Teams puede personalizar o cambiar el nombre de la aplicación en función de las necesidades de la organización.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-158">Understand how the Teams admin can customize or rebrand the app based on the organization's need.</span></span> <span data-ttu-id="0e5b6-159">Esta personalización se habilita si se define en `configurableProperties` el esquema de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-159">This customization is enabled if you define the `configurableProperties` in the manifest schema.</span></span> <span data-ttu-id="0e5b6-160">Para obtener más información, consulta [Personalizar aplicaciones en Microsoft Teams](/MicrosoftTeams/customize-apps).</span><span class="sxs-lookup"><span data-stu-id="0e5b6-160">For more information, see [Customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="0e5b6-161">La personalización de aplicaciones permite a los administradores cambiar la apariencia de las aplicaciones cargadas a través de bots, extensiones de mensajería, pestañas y conectores.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-161">App customization enables admins to change the look-and-feel of the apps loaded through bots, messaging extensions, tabs, and connectors.</span></span> <span data-ttu-id="0e5b6-162">Por ejemplo, si el administrador de Teams personaliza el nombre de una aplicación de *Contoso* a *Contoso Agent,* la aplicación aparecerá con el nuevo nombre *Agente contoso* para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-162">For example, if the Teams admin customizes the name of an app from *Contoso* to *Contoso Agent*, then the app will appear with the new name *Contoso Agent* to users.</span></span> <span data-ttu-id="0e5b6-163">Sin embargo, al agregar un conector a un chat, en la lista los conectores seguirán mostrándole el nombre de la aplicación como *Contoso*.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-163">However, while adding a connector to a chat, in the list the connectors will still show the name of the app as *Contoso*.</span></span>
> 
> <span data-ttu-id="0e5b6-164">Como práctica recomendada, debes proporcionar directrices de personalización para que los usuarios de la aplicación y los clientes puedan seguir al personalizar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-164">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> <span data-ttu-id="0e5b6-165">Para obtener más información, consulta [Personalizar aplicaciones en Microsoft Teams](/MicrosoftTeams/customize-apps).</span><span class="sxs-lookup"><span data-stu-id="0e5b6-165">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

## <a name="tools-and-samples"></a><span data-ttu-id="0e5b6-166">Herramientas y ejemplos</span><span class="sxs-lookup"><span data-stu-id="0e5b6-166">Tools and samples</span></span>

<span data-ttu-id="0e5b6-167">Las siguientes herramientas pueden ayudar a los diseñadores y desarrolladores a empezar:</span><span class="sxs-lookup"><span data-stu-id="0e5b6-167">The following tools can help designers and developers get started:</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="0e5b6-168">Kit de UI de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0e5b6-168">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="0e5b6-169">Diseña una aplicación Teams con componentes de interfaz de usuario, plantillas y ejemplos que puedas arrastrar, colocar y modificar según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-169">Design a Teams app with UI components, templates, and examples that you can drag, drop, and modify as needed.</span></span> <span data-ttu-id="0e5b6-170">El kit de interfaz de usuario también incluye información completa sobre cómo deben verse y comportarse las aplicaciones en diferentes Teams escenarios.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-170">The UI kit also includes comprehensive information about how apps should look and behave in different Teams scenarios.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0e5b6-171">Obtener el kit de interfaz de usuario (Figma)</span><span class="sxs-lookup"><span data-stu-id="0e5b6-171">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="0e5b6-172">Microsoft Teams Biblioteca de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="0e5b6-172">Microsoft Teams UI Library</span></span>

<span data-ttu-id="0e5b6-173">Ver y probar plantillas de Teams de interfaz de usuario individuales y componentes relacionados en el explorador.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-173">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0e5b6-174">Pruebe la biblioteca de interfaz de usuario (área de juegos)</span><span class="sxs-lookup"><span data-stu-id="0e5b6-174">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="0e5b6-175">Importe estas plantillas y componentes relacionados directamente en el proyecto Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-175">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0e5b6-176">Obtener la biblioteca de interfaz de usuario (GitHub)</span><span class="sxs-lookup"><span data-stu-id="0e5b6-176">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="0e5b6-177">Aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0e5b6-177">Sample app</span></span>

<span data-ttu-id="0e5b6-178">Instala una aplicación de ejemplo para ver cómo se ven y se comportan las plantillas de interfaz de usuario en Teams contextos.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-178">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0e5b6-179">Obtener la aplicación de ejemplo (GitHub)</span><span class="sxs-lookup"><span data-stu-id="0e5b6-179">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a><span data-ttu-id="0e5b6-180">Otros recursos</span><span class="sxs-lookup"><span data-stu-id="0e5b6-180">Other resources</span></span>

<span data-ttu-id="0e5b6-181">Para obtener más información, pruebe uno de los siguientes recursos.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-181">To learn more, try one of the following resources.</span></span>

### <a name="fluent-ui-documentation"></a><span data-ttu-id="0e5b6-182">Documentación de la interfaz de usuario fluent</span><span class="sxs-lookup"><span data-stu-id="0e5b6-182">Fluent UI documentation</span></span>

<span data-ttu-id="0e5b6-183">Obtenga ejemplos de código y detalles de implementación para los componentes basados en fluent ui que se usan para crear Teams experiencias.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-183">Get code samples and implementation details for the Fluent UI-based components used to build Teams experiences.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0e5b6-184">Probar Teams de interfaz de usuario (Fluent UI)</span><span class="sxs-lookup"><span data-stu-id="0e5b6-184">Try Teams UI components (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a><span data-ttu-id="0e5b6-185">Diseñador de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="0e5b6-185">Adaptive Cards designer</span></span>

<span data-ttu-id="0e5b6-186">Diseñar tarjetas adaptables en nuestra herramienta basada en web.</span><span class="sxs-lookup"><span data-stu-id="0e5b6-186">Design Adaptive Cards in our web-based tool.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0e5b6-187">Probar el diseñador de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="0e5b6-187">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

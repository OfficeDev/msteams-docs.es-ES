---
title: Diseño de la aplicación personalizada
author: heath-hamilton
description: Obtén información sobre cómo diseñar aplicaciones Microsoft Teams. Los recursos incluyen el kit de interfaz de usuario Microsoft Teams, procedimientos recomendados, ejemplos y mucho más.
localization_priority: Normal
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 2f21872bd8c37026528ff6fde282e8c433d5e052
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565119"
---
# <a name="designing-your-microsoft-teams-app"></a><span data-ttu-id="d45b4-104">Diseño de la aplicación Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d45b4-104">Designing your Microsoft Teams app</span></span>

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Imagen conceptual que introduce las directrices de diseño Microsoft Teams.":::

<span data-ttu-id="d45b4-106">Ya sea que sea diseñador, administrador de productos, desarrollador o creador que utilice herramientas de código bajo, estas directrices pueden ayudarle a tomar rápidamente las decisiones de diseño correctas para su aplicación Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d45b4-106">Whether you're a designer, product manager, developer, or maker using low-code tools, these guidelines can help you quickly make the right design decisions for your Microsoft Teams app.</span></span>

## <a name="teams-app-design-principles"></a><span data-ttu-id="d45b4-107">Teams principios de diseño de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d45b4-107">Teams app design principles</span></span>

<span data-ttu-id="d45b4-108">Teams aplicaciones ayudan a las personas a lograr más juntos.</span><span class="sxs-lookup"><span data-stu-id="d45b4-108">Teams apps help people achieve more together.</span></span> <span data-ttu-id="d45b4-109">Utilice estos principios para guiar su diseño.</span><span class="sxs-lookup"><span data-stu-id="d45b4-109">Use these principles to guide your design.</span></span>

:::row:::
   :::column span="":::

### <a name="collaborative"></a><span data-ttu-id="d45b4-110">colaborativo</span><span class="sxs-lookup"><span data-stu-id="d45b4-110">Collaborative</span></span>

<span data-ttu-id="d45b4-111">Teams aplicaciones ayudan a las personas a lograr más juntos.</span><span class="sxs-lookup"><span data-stu-id="d45b4-111">Teams apps help people achieve more together.</span></span> <span data-ttu-id="d45b4-112">Utilice estos principios para guiar su diseño.</span><span class="sxs-lookup"><span data-stu-id="d45b4-112">Use these principles to guide your design.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a><span data-ttu-id="d45b4-113">fidedigno</span><span class="sxs-lookup"><span data-stu-id="d45b4-113">Trustworthy</span></span>

<span data-ttu-id="d45b4-114">La aplicación es segura y compatible.</span><span class="sxs-lookup"><span data-stu-id="d45b4-114">The app is secure and compliant.</span></span> <span data-ttu-id="d45b4-115">Los usuarios pueden encontrar fácilmente información sobre la privacidad.</span><span class="sxs-lookup"><span data-stu-id="d45b4-115">Users can easily find information about privacy.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a><span data-ttu-id="d45b4-116">Globalmente inclusivo</span><span class="sxs-lookup"><span data-stu-id="d45b4-116">Globally inclusive</span></span>

<span data-ttu-id="d45b4-117">Personas de todos los orígenes, conjuntos de habilidades y disciplinas pueden usar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d45b4-117">People of all backgrounds, skillsets, and disciplines can use the app.</span></span> <span data-ttu-id="d45b4-118">Es cultural, racial y socialmente consciente.</span><span class="sxs-lookup"><span data-stu-id="d45b4-118">It’s culturally, racially, and socially aware.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="light"></a><span data-ttu-id="d45b4-119">Leve</span><span class="sxs-lookup"><span data-stu-id="d45b4-119">Light</span></span>

<span data-ttu-id="d45b4-120">La aplicación se centra en escenarios principales que se mezclan con flujos de trabajo Teams.</span><span class="sxs-lookup"><span data-stu-id="d45b4-120">The app focuses on core scenarios that blend with Teams workflows.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a><span data-ttu-id="d45b4-121">Nativo o distinto</span><span class="sxs-lookup"><span data-stu-id="d45b4-121">Native or distinct</span></span>

<span data-ttu-id="d45b4-122">La aplicación utiliza componentes de diseño Teams nativos o los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="d45b4-122">The app uses native Teams design components or your own.</span></span> <span data-ttu-id="d45b4-123">No hay una mezcla de esquemas de color, controles, etc.</span><span class="sxs-lookup"><span data-stu-id="d45b4-123">There’s no blend of color schemes, controls, and so on.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="useful"></a><span data-ttu-id="d45b4-124">útil</span><span class="sxs-lookup"><span data-stu-id="d45b4-124">Useful</span></span>

<span data-ttu-id="d45b4-125">La aplicación se basa en un escenario que las personas deben hacer en Teams.</span><span class="sxs-lookup"><span data-stu-id="d45b4-125">The app is based on a scenario people need to do in Teams.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a><span data-ttu-id="d45b4-126">Fácil de usar</span><span class="sxs-lookup"><span data-stu-id="d45b4-126">Easy to use</span></span>

<span data-ttu-id="d45b4-127">La interfaz de usuario es fácil de entender, agradable en apariencia y tono, y hace que la gente sea más productiva.</span><span class="sxs-lookup"><span data-stu-id="d45b4-127">The UI is easy to understand, pleasant in look and tone, and makes people more productive.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a><span data-ttu-id="d45b4-128">Respuesta correcta</span><span class="sxs-lookup"><span data-stu-id="d45b4-128">Responsive</span></span>

<span data-ttu-id="d45b4-129">La aplicación es independiente del dispositivo y la pantalla.</span><span class="sxs-lookup"><span data-stu-id="d45b4-129">The app is device and screen agnostic.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a><span data-ttu-id="d45b4-130">Accesible</span><span class="sxs-lookup"><span data-stu-id="d45b4-130">Accessible</span></span>

<span data-ttu-id="d45b4-131">La aplicación cumple Teams requisitos de accesibilidad en términos de contraste de color, alternativas de navegación y más.</span><span class="sxs-lookup"><span data-stu-id="d45b4-131">The app meets Teams accessibility requirements in terms of color contrast, navigation alternatives, and more.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a><span data-ttu-id="d45b4-132">Bien descrito</span><span class="sxs-lookup"><span data-stu-id="d45b4-132">Well described</span></span>

<span data-ttu-id="d45b4-133">El texto, los iconos y las imágenes dejan claro para qué sirve la aplicación y cómo usarla.</span><span class="sxs-lookup"><span data-stu-id="d45b4-133">Text, icons, and images make it clear what the app is for and how to use it.</span></span>

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a><span data-ttu-id="d45b4-134">Creación de una experiencia cohesiva</span><span class="sxs-lookup"><span data-stu-id="d45b4-134">Creating a cohesive experience</span></span>

<span data-ttu-id="d45b4-135">Diseñar una aplicación Teams es como diseñar una aplicación web convencional, pero también un poco diferente.</span><span class="sxs-lookup"><span data-stu-id="d45b4-135">Designing a Teams app is like designing a conventional web app—but also a little different.</span></span> <span data-ttu-id="d45b4-136">Un diseño eficaz resalta los atributos únicos de la aplicación mientras se ajusta de forma natural con Teams características y contextos.</span><span class="sxs-lookup"><span data-stu-id="d45b4-136">An effective design highlights your app's unique attributes while fitting naturally with Teams features and contexts.</span></span>

<span data-ttu-id="d45b4-137">Estas directrices y recursos pueden ayudarle a lograr ese equilibrio.</span><span class="sxs-lookup"><span data-stu-id="d45b4-137">These guidelines and resources can help you strike that balance.</span></span> <span data-ttu-id="d45b4-138">Sabrás qué hacer y qué evitar al diseñar tu aplicación de Teams (como la navegación de varios niveles en una pestaña).</span><span class="sxs-lookup"><span data-stu-id="d45b4-138">You'll know what to do and what to avoid when designing your Teams app (such as multi-level navigation in a tab).</span></span>

## <a name="planning-your-app"></a><span data-ttu-id="d45b4-139">Planificación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="d45b4-139">Planning your app</span></span>

<span data-ttu-id="d45b4-140">Para diseñar una aplicación de Teams de alta calidad, primero debe comprender lo que desea que haga la aplicación y cómo cree que la gente la usará.</span><span class="sxs-lookup"><span data-stu-id="d45b4-140">To design a high-quality Teams app, you must first understand what you want your app to do and how you think people will use it.</span></span> <span data-ttu-id="d45b4-141">Si aún no lo has hecho, tómate un tiempo para planificar correctamente [la aplicación.](../../concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="d45b4-141">If you haven't already, take some time to properly [plan your app](../../concepts/extensibility-points.md).</span></span>

## <a name="design-fundamentals"></a><span data-ttu-id="d45b4-142">Conceptos básicos de diseño</span><span class="sxs-lookup"><span data-stu-id="d45b4-142">Design fundamentals</span></span>

<span data-ttu-id="d45b4-143">Aprenda los [fundamentos del diseño de Teams aplicación,](design-teams-app-fundamentals.md)incluidos el diseño, los esquemas de color y mucho más.</span><span class="sxs-lookup"><span data-stu-id="d45b4-143">Learn the [fundamentals of Teams app design](design-teams-app-fundamentals.md), including layout, color schemes, and more.</span></span>

## <a name="basic-fluent-ui-components-for-teams"></a><span data-ttu-id="d45b4-144">Componentes básicos de la interfaz de usuario fluida para Teams</span><span class="sxs-lookup"><span data-stu-id="d45b4-144">Basic Fluent UI components for Teams</span></span>

<span data-ttu-id="d45b4-145">En función de fluent UI, estos son los [elementos principales para crear interfaces de Teams conocidas.](design-teams-app-basic-ui-components.md)</span><span class="sxs-lookup"><span data-stu-id="d45b4-145">Based on Fluent UI, these are the [core elements for creating familiar Teams interfaces](design-teams-app-basic-ui-components.md).</span></span>

## <a name="ui-templates"></a><span data-ttu-id="d45b4-146">Plantillas de la interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="d45b4-146">UI templates</span></span>

<span data-ttu-id="d45b4-147">Cree rápidamente diseños complejos y de alta fidelidad con [plantillas para casos de uso y flujos de trabajo comunes Teams.](design-teams-app-ui-templates.md)</span><span class="sxs-lookup"><span data-stu-id="d45b4-147">Quickly create complex, high-fidelity designs with [templates for common Teams use cases and workflows](design-teams-app-ui-templates.md).</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="d45b4-148">Capacidades de la aplicación</span><span class="sxs-lookup"><span data-stu-id="d45b4-148">App capabilities</span></span>

<span data-ttu-id="d45b4-149">Comprenda cómo las personas agregan, usan y administran aplicaciones Teams para aprovechar al máximo cada capacidad en su diseño.</span><span class="sxs-lookup"><span data-stu-id="d45b4-149">Understand how people add, use, and manage Teams apps to make the most of each capability in your design.</span></span>

* [<span data-ttu-id="d45b4-150">Aplicaciones personales</span><span class="sxs-lookup"><span data-stu-id="d45b4-150">Personal apps</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="d45b4-151">Pestañas</span><span class="sxs-lookup"><span data-stu-id="d45b4-151">Tabs</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="d45b4-152">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="d45b4-152">Messaging extensions</span></span>](../../messaging-extensions/design/messaging-extension-design.md)
* [<span data-ttu-id="d45b4-153">Bots</span><span class="sxs-lookup"><span data-stu-id="d45b4-153">Bots</span></span>](../../bots/design/bots.md)
* [<span data-ttu-id="d45b4-154">Extensiones de reunión</span><span class="sxs-lookup"><span data-stu-id="d45b4-154">Meeting extensions</span></span>](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [<span data-ttu-id="d45b4-155">Módulos de tareas</span><span class="sxs-lookup"><span data-stu-id="d45b4-155">Task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [<span data-ttu-id="d45b4-156">Tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="d45b4-156">Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="app-customization"></a><span data-ttu-id="d45b4-157">Personalización de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d45b4-157">App customization</span></span>

<span data-ttu-id="d45b4-158">Comprender cómo el administrador de Teams puede personalizar o cambiar el nombre de la aplicación en función de la necesidad de la organización.</span><span class="sxs-lookup"><span data-stu-id="d45b4-158">Understand how the Teams admin can customize or rebrand the app based on the organization's need.</span></span> <span data-ttu-id="d45b4-159">Esta personalización está habilitada si define el `configurableProperties` esquema de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="d45b4-159">This customization is enabled if you define the `configurableProperties` in the manifest schema.</span></span> <span data-ttu-id="d45b4-160">Para obtener más información, consulte [Personalizar aplicaciones en Microsoft Teams](/MicrosoftTeams/customize-apps).</span><span class="sxs-lookup"><span data-stu-id="d45b4-160">For more information, see [Customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="d45b4-161">La personalización de la aplicación permite a los administradores cambiar la apariencia de las aplicaciones cargadas a través de bots, extensiones de mensajería, pestañas y conectores.</span><span class="sxs-lookup"><span data-stu-id="d45b4-161">App customization enables admins to change the look-and-feel of the apps loaded through bots, messaging extensions, tabs, and connectors.</span></span> <span data-ttu-id="d45b4-162">Por ejemplo, si el administrador de Teams personaliza el nombre de una aplicación de *Contoso* al *Agente de Contoso,* la aplicación aparecerá con el nuevo nombre *Contoso Agent* para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="d45b4-162">For example, if the Teams admin customizes the name of an app from *Contoso* to *Contoso Agent*, then the app will appear with the new name *Contoso Agent* to users.</span></span> <span data-ttu-id="d45b4-163">Sin embargo, al agregar un conector a un chat, en la lista los conectores seguirán mostrando el nombre de la aplicación como *Contoso*.</span><span class="sxs-lookup"><span data-stu-id="d45b4-163">However, while adding a connector to a chat, in the list the connectors will still show the name of the app as *Contoso*.</span></span>
> 
> <span data-ttu-id="d45b4-164">Como práctica recomendada, debe proporcionar directrices de personalización para que los usuarios y clientes de la aplicación las sigan al personalizar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d45b4-164">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> <span data-ttu-id="d45b4-165">Para obtener más información, consulte [personalizar aplicaciones en Microsoft Teams](/MicrosoftTeams/customize-apps).</span><span class="sxs-lookup"><span data-stu-id="d45b4-165">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

## <a name="tools-and-samples"></a><span data-ttu-id="d45b4-166">Herramientas y ejemplos</span><span class="sxs-lookup"><span data-stu-id="d45b4-166">Tools and samples</span></span>

<span data-ttu-id="d45b4-167">Las siguientes herramientas pueden ayudar a los diseñadores y desarrolladores a empezar:</span><span class="sxs-lookup"><span data-stu-id="d45b4-167">The following tools can help designers and developers get started:</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="d45b4-168">Kit de UI de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d45b4-168">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="d45b4-169">Diseñe una aplicación Teams con componentes de interfaz de usuario, plantillas y ejemplos que pueda arrastrar, soltar y modificar según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d45b4-169">Design a Teams app with UI components, templates, and examples that you can drag, drop, and modify as needed.</span></span> <span data-ttu-id="d45b4-170">El kit de interfaz de usuario también incluye información completa sobre cómo deben verse y comportarse las aplicaciones en diferentes escenarios Teams.</span><span class="sxs-lookup"><span data-stu-id="d45b4-170">The UI kit also includes comprehensive information about how apps should look and behave in different Teams scenarios.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d45b4-171">Obtener el kit de interfaz de usuario (Figma)</span><span class="sxs-lookup"><span data-stu-id="d45b4-171">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="d45b4-172">Microsoft Teams Biblioteca de IU</span><span class="sxs-lookup"><span data-stu-id="d45b4-172">Microsoft Teams UI Library</span></span>

<span data-ttu-id="d45b4-173">Vea y pruebe plantillas de interfaz de usuario Teams individuales y componentes relacionados en el explorador.</span><span class="sxs-lookup"><span data-stu-id="d45b4-173">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d45b4-174">Pruebe la biblioteca de interfaz de usuario (área de juegos)</span><span class="sxs-lookup"><span data-stu-id="d45b4-174">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="d45b4-175">Importe estas plantillas y componentes relacionados directamente en el proyecto de aplicación Teams.</span><span class="sxs-lookup"><span data-stu-id="d45b4-175">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d45b4-176">Obtener la biblioteca de interfaz de usuario (GitHub)</span><span class="sxs-lookup"><span data-stu-id="d45b4-176">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="d45b4-177">Aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d45b4-177">Sample app</span></span>

<span data-ttu-id="d45b4-178">Instale una aplicación de ejemplo para ver cómo se ven y se comportan las plantillas de interfaz de usuario en contextos Teams.</span><span class="sxs-lookup"><span data-stu-id="d45b4-178">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d45b4-179">Obtener la aplicación de ejemplo (GitHub)</span><span class="sxs-lookup"><span data-stu-id="d45b4-179">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a><span data-ttu-id="d45b4-180">Otros recursos</span><span class="sxs-lookup"><span data-stu-id="d45b4-180">Other resources</span></span>

<span data-ttu-id="d45b4-181">Para obtener más información, pruebe uno de los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="d45b4-181">To learn more, try one of the following resources:</span></span>

### <a name="fluent-ui-documentation"></a><span data-ttu-id="d45b4-182">Documentación fluida de IU</span><span class="sxs-lookup"><span data-stu-id="d45b4-182">Fluent UI documentation</span></span>

<span data-ttu-id="d45b4-183">Obtenga ejemplos de código y detalles de implementación para los componentes basados en la interfaz de usuario de Fluent que se usan para crear experiencias Teams.</span><span class="sxs-lookup"><span data-stu-id="d45b4-183">Get code samples and implementation details for the Fluent UI-based components used to build Teams experiences.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d45b4-184">Probar componentes de interfaz de usuario Teams (INTERFAZ de usuario fluida)</span><span class="sxs-lookup"><span data-stu-id="d45b4-184">Try Teams UI components (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a><span data-ttu-id="d45b4-185">Diseñador de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="d45b4-185">Adaptive Cards designer</span></span>

<span data-ttu-id="d45b4-186">Diseña tarjetas adaptables en nuestra herramienta basada en web.</span><span class="sxs-lookup"><span data-stu-id="d45b4-186">Design Adaptive Cards in our web-based tool.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d45b4-187">Pruebe el diseñador de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="d45b4-187">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

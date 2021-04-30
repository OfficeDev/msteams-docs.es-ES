---
title: Pestañas en dispositivos móviles
description: Describe las directrices para diseñar pestañas que funcionan en dispositivos móviles.
ms.topic: conceptual
localization_priority: Normal
keywords: Las directrices de diseño de teams hacen referencia a las pestañas móviles de aplicaciones personales del marco de trabajo de teams
ms.openlocfilehash: b9f09ce2603ee2617b8b93ba2132b900c61f2c31
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088762"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="d2a15-104">Pestañas en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="d2a15-104">Tabs on mobile</span></span>

<span data-ttu-id="d2a15-105">Puedes incluir pestañas en Teams móviles, chats y aplicaciones personales.</span><span class="sxs-lookup"><span data-stu-id="d2a15-105">You can include tabs in Teams mobile channels, chats, and personal apps.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="d2a15-106">Acceso a pestañas personales</span><span class="sxs-lookup"><span data-stu-id="d2a15-106">Accessing personal tabs</span></span>

<span data-ttu-id="d2a15-107">Puedes acceder a pestañas personales en el cajón de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d2a15-107">You can access personal tabs in the app drawer.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Ilustración que muestra el Teams de aplicaciones móviles." border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="d2a15-109">Acceso a pestañas de canal</span><span class="sxs-lookup"><span data-stu-id="d2a15-109">Accessing channel tabs</span></span>

<span data-ttu-id="d2a15-110">Puedes acceder a las pestañas canal  y grupo seleccionando el botón Más en el canal o chat en el que se han agregado.</span><span class="sxs-lookup"><span data-stu-id="d2a15-110">You can access channel and group tabs by selecting the **More** button in the channel or chat in which they've been added.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Ilustración que muestra una Teams móvil." border="false":::

## <a name="design-considerations"></a><span data-ttu-id="d2a15-112">Consideraciones sobre diseño</span><span class="sxs-lookup"><span data-stu-id="d2a15-112">Design considerations</span></span>

<span data-ttu-id="d2a15-113">Nuestra plataforma móvil permite que las aplicaciones sean una experiencia envolvente con el contenido de la aplicación que toma toda la pantalla aparte de la navegación Teams navegación.</span><span class="sxs-lookup"><span data-stu-id="d2a15-113">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="d2a15-114">Para crear una experiencia envolvente que se adapte a Teams, siga estas directrices.</span><span class="sxs-lookup"><span data-stu-id="d2a15-114">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="d2a15-115">Diseño dinámico</span><span class="sxs-lookup"><span data-stu-id="d2a15-115">Responsive design</span></span>

<span data-ttu-id="d2a15-116">Dado que la pestaña se puede abrir en dispositivos con una amplia variedad de tamaños de pantalla, debe seguir los principios [de diseño](https://www.w3schools.com/html/html_responsive.asp) dinámico.</span><span class="sxs-lookup"><span data-stu-id="d2a15-116">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="d2a15-117">Todas las construcciones clave deben ser accesibles en dispositivos móviles y las vistas no deben distorsionarse.</span><span class="sxs-lookup"><span data-stu-id="d2a15-117">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="d2a15-118">Asegúrese de que cuando la pestaña se carga en un dispositivo móvil, todos los botones y vínculos son fácilmente accesibles mediante la navegación basada en los dedos.</span><span class="sxs-lookup"><span data-stu-id="d2a15-118">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="d2a15-119">Diseños</span><span class="sxs-lookup"><span data-stu-id="d2a15-119">Layouts</span></span>

<span data-ttu-id="d2a15-120">Es importante elegir el diseño correcto para la pestaña.</span><span class="sxs-lookup"><span data-stu-id="d2a15-120">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="d2a15-121">Debe tener en cuenta el tipo de información que está presentando y elegir un diseño que la organice para un consumo fácil.</span><span class="sxs-lookup"><span data-stu-id="d2a15-121">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="d2a15-122">A continuación se describen algunas opciones potenciales.</span><span class="sxs-lookup"><span data-stu-id="d2a15-122">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="d2a15-123">Lienzo único</span><span class="sxs-lookup"><span data-stu-id="d2a15-123">Single canvas</span></span>

<span data-ttu-id="d2a15-124">Este es un área grande donde se realiza el trabajo.</span><span class="sxs-lookup"><span data-stu-id="d2a15-124">This is one large area where work gets done.</span></span> <span data-ttu-id="d2a15-125">La Teams wiki sigue este patrón.</span><span class="sxs-lookup"><span data-stu-id="d2a15-125">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="d2a15-126">Si tienes una aplicación que no separa el contenido en componentes más pequeños, sería un buen ajuste.</span><span class="sxs-lookup"><span data-stu-id="d2a15-126">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Ilustración que muestra una Teams de lienzo único móvil." border="false":::

#### <a name="list"></a><span data-ttu-id="d2a15-128">Lista</span><span class="sxs-lookup"><span data-stu-id="d2a15-128">List</span></span>

<span data-ttu-id="d2a15-129">Las listas son excelentes para ordenar y filtrar grandes cantidades de datos y son excelentes para mantener las cosas más importantes en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="d2a15-129">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="d2a15-130">Es útil usar columnas que se pueden ordenar.</span><span class="sxs-lookup"><span data-stu-id="d2a15-130">It is helpful to use sortable columns.</span></span> <span data-ttu-id="d2a15-131">Las acciones se pueden agregar a cada elemento de lista en el menú de puntos suspensivos.</span><span class="sxs-lookup"><span data-stu-id="d2a15-131">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Ilustración que muestra una Teams de lista móvil." border="false":::

#### <a name="grid"></a><span data-ttu-id="d2a15-133">Cuadrícula</span><span class="sxs-lookup"><span data-stu-id="d2a15-133">Grid</span></span>

<span data-ttu-id="d2a15-134">Las cuadrículas son útiles para mostrar elementos que son altamente visuales.</span><span class="sxs-lookup"><span data-stu-id="d2a15-134">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="d2a15-135">Ayuda a incluir un filtro o un control de búsqueda en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="d2a15-135">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="Ilustración que muestra una Teams móvil con un diseño de cuadrícula." border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="d2a15-137">Pestañas con bots en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="d2a15-137">Tabs with bots on mobile</span></span>

<span data-ttu-id="d2a15-138">El siguiente ejemplo es una aplicación personal que tiene pestañas y un bot.</span><span class="sxs-lookup"><span data-stu-id="d2a15-138">The following example is a personal app that has tabs and a bot.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="Ilustración que muestra cómo se Teams móvil que tiene pestañas y un bot." border="false":::

## <a name="ui-components"></a><span data-ttu-id="d2a15-140">Componentes de la interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="d2a15-140">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="d2a15-141">Paletas de colores</span><span class="sxs-lookup"><span data-stu-id="d2a15-141">Color palettes</span></span>

<span data-ttu-id="d2a15-142">El uso de nuestra paleta neutra aprobada para fondos, notificaciones, texto y botones ayudará a tu aplicación a sentirse más como en casa en Teams.</span><span class="sxs-lookup"><span data-stu-id="d2a15-142">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="d2a15-143">Dado Teams móvil tiene dos temas de color (claro y oscuro), es una buena idea asegurarse de que la aplicación tenga un aspecto excelente en ambos.</span><span class="sxs-lookup"><span data-stu-id="d2a15-143">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="d2a15-144">Color claro</span><span class="sxs-lookup"><span data-stu-id="d2a15-144">Light color</span></span>

![paleta de colores claros](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="d2a15-146">Color oscuro</span><span class="sxs-lookup"><span data-stu-id="d2a15-146">Dark color</span></span>

![paleta de colores oscuros](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="d2a15-148">Botones y controles</span><span class="sxs-lookup"><span data-stu-id="d2a15-148">Buttons and controls</span></span>

<span data-ttu-id="d2a15-149">El estilo de los botones ayuda a comunicar el tipo de acción que desencadenan.</span><span class="sxs-lookup"><span data-stu-id="d2a15-149">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="d2a15-150">Mantenemos una amplia variedad de botones con formato para mostrar diferentes niveles de énfasis.</span><span class="sxs-lookup"><span data-stu-id="d2a15-150">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="d2a15-151">Los botones pueden tener texto, un icono o una combinación de texto y un icono.</span><span class="sxs-lookup"><span data-stu-id="d2a15-151">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="d2a15-152">Para comunicar diferentes niveles en una jerarquía, diseñamos botones principales y secundarios dentro de cada categoría.</span><span class="sxs-lookup"><span data-stu-id="d2a15-152">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="d2a15-153">Botones</span><span class="sxs-lookup"><span data-stu-id="d2a15-153">Buttons</span></span>

<span data-ttu-id="d2a15-154">Botones principales y secundarios.</span><span class="sxs-lookup"><span data-stu-id="d2a15-154">Primary and secondary buttons.</span></span>

![imagen de botones](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="d2a15-156">Controles de selección</span><span class="sxs-lookup"><span data-stu-id="d2a15-156">Selection controls</span></span>

<span data-ttu-id="d2a15-157">Botones de radio, casillas y alternancias.</span><span class="sxs-lookup"><span data-stu-id="d2a15-157">Radio buttons, checkboxes, and toggles.</span></span>

![controles de selección](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="d2a15-159">Chiclets y pastillas</span><span class="sxs-lookup"><span data-stu-id="d2a15-159">Chiclets and pills</span></span>

![chiclets y pastillas](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="d2a15-161">Tipografía</span><span class="sxs-lookup"><span data-stu-id="d2a15-161">Typography</span></span>

<span data-ttu-id="d2a15-162">La tipografía debe ser clara y con propósito.</span><span class="sxs-lookup"><span data-stu-id="d2a15-162">Typography should be clear and purposeful.</span></span> <span data-ttu-id="d2a15-163">Haga hincapié en la información importante y evite usar varias fuentes y tamaños para reducir la confusión.</span><span class="sxs-lookup"><span data-stu-id="d2a15-163">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="d2a15-164">Se recomienda usar el caso de oración y evitar el uso de todos los límites para la localización y legibilidad.</span><span class="sxs-lookup"><span data-stu-id="d2a15-164">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![tipografía móvil](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="d2a15-166">Campos y desplegables</span><span class="sxs-lookup"><span data-stu-id="d2a15-166">Fields and flyouts</span></span>

<span data-ttu-id="d2a15-167">Los campos son áreas donde los usuarios pueden introducir texto.</span><span class="sxs-lookup"><span data-stu-id="d2a15-167">Fields are areas where users can input text.</span></span> <span data-ttu-id="d2a15-168">Los paneles desplegables son más ligeros que los cuadros de diálogo y aparecen en el panel superior.</span><span class="sxs-lookup"><span data-stu-id="d2a15-168">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="d2a15-169">Enumerar controles</span><span class="sxs-lookup"><span data-stu-id="d2a15-169">List controls</span></span>

![controles de lista móvil](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="d2a15-171">Controles de campo</span><span class="sxs-lookup"><span data-stu-id="d2a15-171">Field controls</span></span>

![controles de campo móvil](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="d2a15-173">Consideraciones de desarrollador</span><span class="sxs-lookup"><span data-stu-id="d2a15-173">Developer considerations</span></span>

<span data-ttu-id="d2a15-174">Cuando crees una aplicación que incluya una pestaña, debes considerar (y probar) cómo funcionará la pestaña en los clientes de Android e iOS Microsoft Teams usuario.</span><span class="sxs-lookup"><span data-stu-id="d2a15-174">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="d2a15-175">En las secciones siguientes se describen algunos de los escenarios clave que debe tener en cuenta.</span><span class="sxs-lookup"><span data-stu-id="d2a15-175">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="authentication"></a><span data-ttu-id="d2a15-176">Autenticación</span><span class="sxs-lookup"><span data-stu-id="d2a15-176">Authentication</span></span>

<span data-ttu-id="d2a15-177">Para que la autenticación funcione en clientes móviles, debe actualizar Teams SDK de JavaScript a al menos la versión 1.4.1.</span><span class="sxs-lookup"><span data-stu-id="d2a15-177">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="d2a15-178">Ancho de banda bajo y conexiones intermitentes</span><span class="sxs-lookup"><span data-stu-id="d2a15-178">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="d2a15-179">Los clientes móviles necesitan funcionar regularmente con un ancho de banda bajo y conexiones intermitentes.</span><span class="sxs-lookup"><span data-stu-id="d2a15-179">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="d2a15-180">La aplicación debe controlar los tiempos de espera correctamente proporcionando un mensaje contextual al usuario.</span><span class="sxs-lookup"><span data-stu-id="d2a15-180">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="d2a15-181">También debe usar indicadores de progreso del usuario para proporcionar comentarios a los usuarios sobre los procesos de larga ejecución.</span><span class="sxs-lookup"><span data-stu-id="d2a15-181">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

> [!NOTE]
> <span data-ttu-id="d2a15-182">Las pestañas solo se habilitan en dispositivos móviles después de agregar la aplicación a una lista de permitidos, en función de la entrada del equipo de aprobación.</span><span class="sxs-lookup"><span data-stu-id="d2a15-182">Tabs are enabled on mobile only after the application is added to an allow list, based on the input of the approval team.</span></span> <span data-ttu-id="d2a15-183">Para comprobar la capacidad de respuesta de los dispositivos móviles, llegue a teamsubm@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="d2a15-183">To check mobile responsiveness, reach out to teamsubm@microsoft.com.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="d2a15-184">Pruebas en clientes móviles</span><span class="sxs-lookup"><span data-stu-id="d2a15-184">Testing on mobile clients</span></span>

<span data-ttu-id="d2a15-185">Debes validar que la pestaña funciona correctamente en dispositivos móviles de distintos tamaños y calidades.</span><span class="sxs-lookup"><span data-stu-id="d2a15-185">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="d2a15-186">Para dispositivos Android, puedes usar [DevTools](~/tabs/how-to/developer-tools.md) para depurar la pestaña mientras se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="d2a15-186">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="d2a15-187">Se recomienda probar en dispositivos de alto y bajo rendimiento, incluida una tableta.</span><span class="sxs-lookup"><span data-stu-id="d2a15-187">We recommend that you test on both high- and low-performance devices, including a tablet.</span></span>

### <a name="distribution"></a><span data-ttu-id="d2a15-188">Distribución</span><span class="sxs-lookup"><span data-stu-id="d2a15-188">Distribution</span></span>

<span data-ttu-id="d2a15-189">Las aplicaciones que aparecen en la Teams deben aprobarse para que el uso móvil funcione correctamente en el Teams móvil.</span><span class="sxs-lookup"><span data-stu-id="d2a15-189">Apps listed on the Teams store must be approved for mobile use to function properly in the Teams mobile client.</span></span> <span data-ttu-id="d2a15-190">La disponibilidad y el comportamiento de las pestañas depende de si la aplicación está aprobada.</span><span class="sxs-lookup"><span data-stu-id="d2a15-190">Tab availability and behavior depends on whether your app is approved.</span></span>

#### <a name="apps-on-teams-store-approved-for-mobile"></a><span data-ttu-id="d2a15-191">Aplicaciones en la Teams aprobadas para dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="d2a15-191">Apps on Teams store approved for mobile</span></span>

<span data-ttu-id="d2a15-192">En la tabla siguiente se describe la disponibilidad y el comportamiento de las pestañas cuando la aplicación aparece en la Teams y se aprueba para el uso móvil.</span><span class="sxs-lookup"><span data-stu-id="d2a15-192">The following table describes tab availability and behavior when the app is listed on the Teams store and approved for mobile use.</span></span>

|<span data-ttu-id="d2a15-193">Funcionalidad</span><span class="sxs-lookup"><span data-stu-id="d2a15-193">Capability</span></span>   |<span data-ttu-id="d2a15-194">¿Disponibilidad móvil?</span><span class="sxs-lookup"><span data-stu-id="d2a15-194">Mobile availability?</span></span>   |<span data-ttu-id="d2a15-195">Comportamiento móvil</span><span class="sxs-lookup"><span data-stu-id="d2a15-195">Mobile behavior</span></span>|
|----------|-----------|------------|
|<span data-ttu-id="d2a15-196">Canal</span><span class="sxs-lookup"><span data-stu-id="d2a15-196">Channel</span></span> <br /> <span data-ttu-id="d2a15-197">y ficha grupo</span><span class="sxs-lookup"><span data-stu-id="d2a15-197">and group tab</span></span>|<span data-ttu-id="d2a15-198">Sí</span><span class="sxs-lookup"><span data-stu-id="d2a15-198">Yes</span></span>|<span data-ttu-id="d2a15-199">La pestaña se abre en el Teams móvil mediante la configuración de la `contentUrl` aplicación.</span><span class="sxs-lookup"><span data-stu-id="d2a15-199">Tab opens in the Teams mobile client using your app's `contentUrl` configuration.</span></span>|
|<span data-ttu-id="d2a15-200">Aplicación personal</span><span class="sxs-lookup"><span data-stu-id="d2a15-200">Personal app</span></span>|<span data-ttu-id="d2a15-201">Sí</span><span class="sxs-lookup"><span data-stu-id="d2a15-201">Yes</span></span>|<span data-ttu-id="d2a15-202">Cada pestaña de la pestaña aplicación personal se abre en el Teams móvil mediante su configuración `contentUrl` respectiva.</span><span class="sxs-lookup"><span data-stu-id="d2a15-202">Each tab in the personal app tab opens in the Teams mobile client using its respective `contentUrl` configuration.</span></span>|

#### <a name="apps-on-teams-store-not-approved-for-mobile"></a><span data-ttu-id="d2a15-203">Aplicaciones en Teams no aprobadas para móviles</span><span class="sxs-lookup"><span data-stu-id="d2a15-203">Apps on Teams store not approved for mobile</span></span>

<span data-ttu-id="d2a15-204">En la tabla siguiente se describe la disponibilidad y el comportamiento de las pestañas cuando la aplicación se muestra en la Teams, pero no se aprueba para el uso móvil.</span><span class="sxs-lookup"><span data-stu-id="d2a15-204">The following table describes tab availability and behavior when the app is listed on the Teams store but not approved for mobile use.</span></span>

|<span data-ttu-id="d2a15-205">Funcionalidad</span><span class="sxs-lookup"><span data-stu-id="d2a15-205">Capability</span></span>   |<span data-ttu-id="d2a15-206">¿Disponibilidad móvil?</span><span class="sxs-lookup"><span data-stu-id="d2a15-206">Mobile availability?</span></span>|<span data-ttu-id="d2a15-207">Comportamiento móvil</span><span class="sxs-lookup"><span data-stu-id="d2a15-207">Mobile behavior</span></span>|
|----------|-----------|------------|
|<span data-ttu-id="d2a15-208">Pestaña Canal y grupo</span><span class="sxs-lookup"><span data-stu-id="d2a15-208">Channel and group tab</span></span>|<span data-ttu-id="d2a15-209">Sí</span><span class="sxs-lookup"><span data-stu-id="d2a15-209">Yes</span></span>|<span data-ttu-id="d2a15-210">La pestaña se abre en el explorador predeterminado del dispositivo en lugar del cliente móvil de Teams mediante la configuración de la aplicación (que también debe incluirse en la función del código `websiteUrl` `setSettings()` [fuente).](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions)</span><span class="sxs-lookup"><span data-stu-id="d2a15-210">Tab opens in the device's default browser instead of the Teams mobile client using your app's `websiteUrl` configuration (which also must be included in your source code's `setSettings()` [function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions)).</span></span> <span data-ttu-id="d2a15-211">Sin embargo, los usuarios aún pueden ver la pestaña  en el cliente móvil de Teams seleccionando Más junto a la aplicación y **seleccionando Abrir**, que desencadena la configuración de la `contentUrl` aplicación.</span><span class="sxs-lookup"><span data-stu-id="d2a15-211">However, users can still view the tab in the Teams mobile client by selecting **More** next to the app and choosing **Open**, which triggers your app’s `contentUrl` configuration.</span></span>|
|<span data-ttu-id="d2a15-212">Aplicación personal</span><span class="sxs-lookup"><span data-stu-id="d2a15-212">Personal app</span></span>|<span data-ttu-id="d2a15-213">No</span><span class="sxs-lookup"><span data-stu-id="d2a15-213">No</span></span>|<span data-ttu-id="d2a15-214">No aplicable</span><span class="sxs-lookup"><span data-stu-id="d2a15-214">Not applicable</span></span>|

#### <a name="apps-not-on-teams-store"></a><span data-ttu-id="d2a15-215">Aplicaciones que no están Teams tienda</span><span class="sxs-lookup"><span data-stu-id="d2a15-215">Apps not on Teams store</span></span>

<span data-ttu-id="d2a15-216">Si estás descargando localmente la aplicación o publicando en el catálogo de aplicaciones de una organización, el comportamiento de las pestañas será el mismo que las aplicaciones de la tienda Teams aprobadas por Microsoft para dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="d2a15-216">If you're sideloading your app or publishing to an org's app catalog, tab behavior will be the same as Teams store apps approved by Microsoft for mobile.</span></span>

---
title: Pestañas en dispositivos móviles
description: Describe las directrices para diseñar pestañas que funcionan en dispositivos móviles.
ms.topic: conceptual
keywords: Las directrices de diseño de teams hacen referencia a las pestañas móviles de aplicaciones personales del marco de trabajo de teams
ms.openlocfilehash: 72d1cf4623a9f4c1b5c993f1477f755b51d9fe64
ms.sourcegitcommit: 0e252159f53ff9b4452e0574b759bfe73cbf6c84
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2021
ms.locfileid: "51762028"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="dd40a-104">Pestañas en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="dd40a-104">Tabs on mobile</span></span>

> [!NOTE]
> <span data-ttu-id="dd40a-105">Si decide que la pestaña canal o grupo aparezca en los clientes móviles de Teams, la configuración debe tener un valor para la propiedad `setSettings()` `websiteUrl` (vea a continuación).</span><span class="sxs-lookup"><span data-stu-id="dd40a-105">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span>

<span data-ttu-id="dd40a-106">Las pestañas personalizadas pueden formar parte de un canal, un chat de grupo o una aplicación personal (aplicaciones que contienen pestañas estáticas o un bot de uno a uno).</span><span class="sxs-lookup"><span data-stu-id="dd40a-106">Custom tabs can be part of a channel, group chat, or personal app (apps that contain static tabs and/or a one-to-one bot).</span></span>

<span data-ttu-id="dd40a-107">Las aplicaciones personales están disponibles en clientes móviles en el cajón de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="dd40a-107">Personal apps are available on mobile clients in the app drawer.</span></span> <span data-ttu-id="dd40a-108">La aplicación solo se puede instalar desde un cliente de escritorio o web y puede tardar hasta 24 horas en aparecer en clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="dd40a-108">The app can only be installed from a desktop or web client, and can take up to 24 hours to appear on mobile clients.</span></span> <span data-ttu-id="dd40a-109">Como alternativa, puede aplicar una recarga en el cliente móvil al iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="dd40a-109">Alternatively, you can enforce a reload on the mobile client by signing out and in.</span></span> <span data-ttu-id="dd40a-110">Esto debería hacer que la aplicación móvil esté disponible de inmediato.</span><span class="sxs-lookup"><span data-stu-id="dd40a-110">This should make the mobile app available right away.</span></span>

<span data-ttu-id="dd40a-111">Las pestañas de canal también están disponibles en dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="dd40a-111">Channel tabs are also available on mobile.</span></span> <span data-ttu-id="dd40a-112">Actualmente, el comportamiento predeterminado es usar la pestaña `websiteUrl` para iniciarla en una ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="dd40a-112">The default behavior is currently to use your `websiteUrl` to launch your tab in a browser window.</span></span> <span data-ttu-id="dd40a-113">Sin embargo, se pueden cargar en un cliente móvil haciendo clic en el menú desbordamiento situado junto a la pestaña y seleccionando Abrir , que usará la pestaña para cargarla dentro del cliente móvil `...` de  `contentUrl` Teams.</span><span class="sxs-lookup"><span data-stu-id="dd40a-113">However, they can be loaded on a mobile client by clicking the `...` overflow menu next to the tab and choosing **Open**, which will use your `contentUrl` to load the tab inside the Teams mobile client.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="dd40a-114">Acceso a pestañas personales</span><span class="sxs-lookup"><span data-stu-id="dd40a-114">Accessing personal tabs</span></span>

<span data-ttu-id="dd40a-115">En la siguiente ilustración se muestra cómo acceder a una pestaña personal en el móvil.</span><span class="sxs-lookup"><span data-stu-id="dd40a-115">The following illustration shows how you access a personal tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Ilustración que muestra el cajón de la aplicación móvil de Teams." border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="dd40a-117">Acceso a pestañas de canal</span><span class="sxs-lookup"><span data-stu-id="dd40a-117">Accessing channel tabs</span></span>

<span data-ttu-id="dd40a-118">En la siguiente ilustración se muestra cómo obtener acceso a una pestaña de canal en el móvil.</span><span class="sxs-lookup"><span data-stu-id="dd40a-118">The following illustration shows how you access a channel tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Ilustración que muestra una pestaña móvil de Teams." border="false":::

## <a name="design-considerations"></a><span data-ttu-id="dd40a-120">Consideraciones sobre diseño</span><span class="sxs-lookup"><span data-stu-id="dd40a-120">Design considerations</span></span>

<span data-ttu-id="dd40a-121">Nuestra plataforma móvil permite que las aplicaciones sean una experiencia envolvente con el contenido de la aplicación que toma toda la pantalla aparte de la navegación principal de Teams.</span><span class="sxs-lookup"><span data-stu-id="dd40a-121">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="dd40a-122">Para crear una experiencia envolvente que se adapte a Teams, siga estas directrices.</span><span class="sxs-lookup"><span data-stu-id="dd40a-122">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="dd40a-123">Diseño dinámico</span><span class="sxs-lookup"><span data-stu-id="dd40a-123">Responsive design</span></span>

<span data-ttu-id="dd40a-124">Dado que la pestaña se puede abrir en dispositivos con una amplia variedad de tamaños de pantalla, debe seguir los principios [de diseño](https://www.w3schools.com/html/html_responsive.asp) dinámico.</span><span class="sxs-lookup"><span data-stu-id="dd40a-124">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="dd40a-125">Todas las construcciones clave deben ser accesibles en dispositivos móviles y las vistas no deben distorsionarse.</span><span class="sxs-lookup"><span data-stu-id="dd40a-125">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="dd40a-126">Asegúrese de que cuando la pestaña se carga en un dispositivo móvil, todos los botones y vínculos son fácilmente accesibles mediante la navegación basada en los dedos.</span><span class="sxs-lookup"><span data-stu-id="dd40a-126">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="dd40a-127">Diseños</span><span class="sxs-lookup"><span data-stu-id="dd40a-127">Layouts</span></span>

<span data-ttu-id="dd40a-128">Es importante elegir el diseño correcto para la pestaña.</span><span class="sxs-lookup"><span data-stu-id="dd40a-128">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="dd40a-129">Debe tener en cuenta el tipo de información que está presentando y elegir un diseño que la organice para un consumo fácil.</span><span class="sxs-lookup"><span data-stu-id="dd40a-129">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="dd40a-130">A continuación se describen algunas opciones potenciales.</span><span class="sxs-lookup"><span data-stu-id="dd40a-130">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="dd40a-131">Lienzo único</span><span class="sxs-lookup"><span data-stu-id="dd40a-131">Single canvas</span></span>

<span data-ttu-id="dd40a-132">Este es un área grande donde se realiza el trabajo.</span><span class="sxs-lookup"><span data-stu-id="dd40a-132">This is one large area where work gets done.</span></span> <span data-ttu-id="dd40a-133">La aplicación Wiki de Teams sigue este patrón.</span><span class="sxs-lookup"><span data-stu-id="dd40a-133">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="dd40a-134">Si tienes una aplicación que no separa el contenido en componentes más pequeños, sería un buen ajuste.</span><span class="sxs-lookup"><span data-stu-id="dd40a-134">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Ilustración que muestra una pestaña de lienzo único móvil de Teams." border="false":::

#### <a name="list"></a><span data-ttu-id="dd40a-136">Lista</span><span class="sxs-lookup"><span data-stu-id="dd40a-136">List</span></span>

<span data-ttu-id="dd40a-137">Las listas son excelentes para ordenar y filtrar grandes cantidades de datos y son excelentes para mantener las cosas más importantes en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="dd40a-137">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="dd40a-138">Es útil usar columnas que se pueden ordenar.</span><span class="sxs-lookup"><span data-stu-id="dd40a-138">It is helpful to use sortable columns.</span></span> <span data-ttu-id="dd40a-139">Las acciones se pueden agregar a cada elemento de lista en el menú de puntos suspensivos.</span><span class="sxs-lookup"><span data-stu-id="dd40a-139">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Ilustración que muestra una pestaña de lista móvil de Teams." border="false":::

#### <a name="grid"></a><span data-ttu-id="dd40a-141">Cuadrícula</span><span class="sxs-lookup"><span data-stu-id="dd40a-141">Grid</span></span>

<span data-ttu-id="dd40a-142">Las cuadrículas son útiles para mostrar elementos que son altamente visuales.</span><span class="sxs-lookup"><span data-stu-id="dd40a-142">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="dd40a-143">Ayuda a incluir un filtro o un control de búsqueda en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="dd40a-143">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="Ilustración que muestra una pestaña móvil de Teams con un diseño de cuadrícula." border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="dd40a-145">Pestañas con bots en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="dd40a-145">Tabs with bots on mobile</span></span>

<span data-ttu-id="dd40a-146">El siguiente ejemplo es una aplicación personal que tiene pestañas y un bot.</span><span class="sxs-lookup"><span data-stu-id="dd40a-146">The following example is a personal app that has tabs and a bot.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="Ilustración que muestra cómo la aplicación móvil de Teams que tiene pestañas y un bot." border="false":::

## <a name="ui-components"></a><span data-ttu-id="dd40a-148">Componentes de la interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="dd40a-148">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="dd40a-149">Paletas de colores</span><span class="sxs-lookup"><span data-stu-id="dd40a-149">Color palettes</span></span>

<span data-ttu-id="dd40a-150">El uso de nuestra paleta neutra aprobada para fondos, notificaciones, texto y botones ayudará a tu aplicación a sentirse más como en casa en Teams.</span><span class="sxs-lookup"><span data-stu-id="dd40a-150">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="dd40a-151">Dado que teams mobile tiene dos temas de color (claro y oscuro), es una buena idea asegurarse de que la aplicación tenga un aspecto excelente en ambos.</span><span class="sxs-lookup"><span data-stu-id="dd40a-151">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="dd40a-152">Color claro</span><span class="sxs-lookup"><span data-stu-id="dd40a-152">Light color</span></span>

![paleta de colores claros](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="dd40a-154">Color oscuro</span><span class="sxs-lookup"><span data-stu-id="dd40a-154">Dark color</span></span>

![paleta de colores oscuros](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="dd40a-156">Botones y controles</span><span class="sxs-lookup"><span data-stu-id="dd40a-156">Buttons and controls</span></span>

<span data-ttu-id="dd40a-157">El estilo de los botones ayuda a comunicar el tipo de acción que desencadenan.</span><span class="sxs-lookup"><span data-stu-id="dd40a-157">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="dd40a-158">Mantenemos una amplia variedad de botones con formato para mostrar diferentes niveles de énfasis.</span><span class="sxs-lookup"><span data-stu-id="dd40a-158">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="dd40a-159">Los botones pueden tener texto, un icono o una combinación de texto y un icono.</span><span class="sxs-lookup"><span data-stu-id="dd40a-159">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="dd40a-160">Para comunicar diferentes niveles en una jerarquía, diseñamos botones principales y secundarios dentro de cada categoría.</span><span class="sxs-lookup"><span data-stu-id="dd40a-160">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="dd40a-161">Botones</span><span class="sxs-lookup"><span data-stu-id="dd40a-161">Buttons</span></span>

<span data-ttu-id="dd40a-162">Botones principales y secundarios.</span><span class="sxs-lookup"><span data-stu-id="dd40a-162">Primary and secondary buttons.</span></span>

![imagen de botones](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="dd40a-164">Controles de selección</span><span class="sxs-lookup"><span data-stu-id="dd40a-164">Selection controls</span></span>

<span data-ttu-id="dd40a-165">Botones de radio, casillas y alternancias.</span><span class="sxs-lookup"><span data-stu-id="dd40a-165">Radio buttons, checkboxes, and toggles.</span></span>

![controles de selección](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="dd40a-167">Chiclets y pastillas</span><span class="sxs-lookup"><span data-stu-id="dd40a-167">Chiclets and pills</span></span>

![chiclets y pastillas](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="dd40a-169">Tipografía</span><span class="sxs-lookup"><span data-stu-id="dd40a-169">Typography</span></span>

<span data-ttu-id="dd40a-170">La tipografía debe ser clara y con propósito.</span><span class="sxs-lookup"><span data-stu-id="dd40a-170">Typography should be clear and purposeful.</span></span> <span data-ttu-id="dd40a-171">Haga hincapié en la información importante y evite usar varias fuentes y tamaños para reducir la confusión.</span><span class="sxs-lookup"><span data-stu-id="dd40a-171">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="dd40a-172">Se recomienda usar el caso de oración y evitar el uso de todos los límites para la localización y legibilidad.</span><span class="sxs-lookup"><span data-stu-id="dd40a-172">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![tipografía móvil](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="dd40a-174">Campos y desplegables</span><span class="sxs-lookup"><span data-stu-id="dd40a-174">Fields and flyouts</span></span>

<span data-ttu-id="dd40a-175">Los campos son áreas donde los usuarios pueden introducir texto.</span><span class="sxs-lookup"><span data-stu-id="dd40a-175">Fields are areas where users can input text.</span></span> <span data-ttu-id="dd40a-176">Los paneles desplegables son más ligeros que los cuadros de diálogo y aparecen en el panel superior.</span><span class="sxs-lookup"><span data-stu-id="dd40a-176">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="dd40a-177">Enumerar controles</span><span class="sxs-lookup"><span data-stu-id="dd40a-177">List controls</span></span>

![controles de lista móvil](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="dd40a-179">Controles de campo</span><span class="sxs-lookup"><span data-stu-id="dd40a-179">Field controls</span></span>

![controles de campo móvil](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="dd40a-181">Consideraciones de desarrollador</span><span class="sxs-lookup"><span data-stu-id="dd40a-181">Developer considerations</span></span>

<span data-ttu-id="dd40a-182">Cuando crees una aplicación que incluya una pestaña, debes considerar (y probar) cómo funcionará la pestaña en los clientes de Microsoft Teams de Android e iOS.</span><span class="sxs-lookup"><span data-stu-id="dd40a-182">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="dd40a-183">En las secciones siguientes se describen algunos de los escenarios clave que debe tener en cuenta.</span><span class="sxs-lookup"><span data-stu-id="dd40a-183">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="dd40a-184">Pruebas en clientes móviles</span><span class="sxs-lookup"><span data-stu-id="dd40a-184">Testing on mobile clients</span></span>

<span data-ttu-id="dd40a-185">Debes validar que la pestaña funciona correctamente en dispositivos móviles de distintos tamaños y calidades.</span><span class="sxs-lookup"><span data-stu-id="dd40a-185">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="dd40a-186">Para dispositivos Android, puedes usar [DevTools](~/tabs/how-to/developer-tools.md) para depurar la pestaña mientras se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="dd40a-186">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="dd40a-187">Se recomienda probar tanto en dispositivos de alto y bajo rendimiento, como en una tableta.</span><span class="sxs-lookup"><span data-stu-id="dd40a-187">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="authentication"></a><span data-ttu-id="dd40a-188">Autenticación</span><span class="sxs-lookup"><span data-stu-id="dd40a-188">Authentication</span></span>

<span data-ttu-id="dd40a-189">Para que la autenticación funcione en clientes móviles, debe actualizar el SDK de JavaScript de Teams a la versión 1.4.1 como mínimo.</span><span class="sxs-lookup"><span data-stu-id="dd40a-189">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="dd40a-190">Ancho de banda bajo y conexiones intermitentes</span><span class="sxs-lookup"><span data-stu-id="dd40a-190">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="dd40a-191">Los clientes móviles necesitan funcionar regularmente con un ancho de banda bajo y conexiones intermitentes.</span><span class="sxs-lookup"><span data-stu-id="dd40a-191">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="dd40a-192">La aplicación debe controlar los tiempos de espera correctamente proporcionando un mensaje contextual al usuario.</span><span class="sxs-lookup"><span data-stu-id="dd40a-192">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="dd40a-193">También debe usar indicadores de progreso del usuario para proporcionar comentarios a los usuarios sobre los procesos de larga ejecución.</span><span class="sxs-lookup"><span data-stu-id="dd40a-193">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

> [!NOTE]
> <span data-ttu-id="dd40a-194">Las pestañas solo se habilitan en dispositivos móviles después de agregar la aplicación a una lista de permitidos, en función de la entrada del equipo de aprobación.</span><span class="sxs-lookup"><span data-stu-id="dd40a-194">Tabs are enabled on mobile only after the application is added to an allow list, based on the input of the approval team.</span></span> <span data-ttu-id="dd40a-195">Para comprobar la capacidad de respuesta de los dispositivos móviles, llegue a teamsubm@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="dd40a-195">To check mobile responsiveness, reach out to teamsubm@microsoft.com.</span></span> 

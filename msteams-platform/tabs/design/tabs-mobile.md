---
title: Pestañas en dispositivos móviles
description: Describe las directrices para diseñar pestañas que funcionan en dispositivos móviles.
ms.topic: conceptual
keywords: Las directrices de diseño de teams hacen referencia a las pestañas móviles de aplicaciones personales del marco de trabajo
ms.openlocfilehash: 70ff46e446b146b134f34830e8867133cbeeca14
ms.sourcegitcommit: f74b74d5bed1df193e59f46121ada443fb57277b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093291"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="c297e-104">Pestañas en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="c297e-104">Tabs on mobile</span></span>

> [!NOTE]
> <span data-ttu-id="c297e-105">Si decide que la pestaña de canal o grupo aparezca en los clientes móviles de Teams, la configuración debe tener un valor para la propiedad `setSettings()` `websiteUrl` (vea a continuación).</span><span class="sxs-lookup"><span data-stu-id="c297e-105">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span>

<span data-ttu-id="c297e-106">Las pestañas personalizadas pueden formar parte de un canal, un chat en grupo o una aplicación personal (aplicaciones que contienen pestañas estáticas o un bot de uno a uno).</span><span class="sxs-lookup"><span data-stu-id="c297e-106">Custom tabs can be part of a channel, group chat, or personal app (apps that contain static tabs and/or a one-to-one bot).</span></span>

<span data-ttu-id="c297e-107">Las aplicaciones personales están disponibles en clientes móviles en el cajón de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c297e-107">Personal apps are available on mobile clients in the app drawer.</span></span> <span data-ttu-id="c297e-108">La aplicación solo se puede instalar desde un cliente de escritorio o web y puede tardar hasta 24 horas en aparecer en clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="c297e-108">The app can only be installed from a desktop or web client, and can take up to 24 hours to appear on mobile clients.</span></span>

<span data-ttu-id="c297e-109">Las pestañas de canal también están disponibles en dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="c297e-109">Channel tabs are also available on mobile.</span></span> <span data-ttu-id="c297e-110">Actualmente, el comportamiento predeterminado es usar la pestaña `websiteUrl` para iniciarla en una ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="c297e-110">The default behavior is currently to use your `websiteUrl` to launch your tab in a browser window.</span></span> <span data-ttu-id="c297e-111">Sin embargo, se pueden cargar en un cliente móvil haciendo clic en el menú de desbordamiento situado junto a la pestaña y eligiendo Abrir , que usará para cargar la pestaña dentro del cliente móvil `...` de  `contentUrl` Teams.</span><span class="sxs-lookup"><span data-stu-id="c297e-111">However, they can be loaded on a mobile client by clicking the `...` overflow menu next to the tab and choosing **Open**, which will use your `contentUrl` to load the tab inside the Teams mobile client.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="c297e-112">Acceso a pestañas personales</span><span class="sxs-lookup"><span data-stu-id="c297e-112">Accessing personal tabs</span></span>

<span data-ttu-id="c297e-113">En la siguiente ilustración se muestra cómo obtener acceso a una pestaña personal en un dispositivo móvil.</span><span class="sxs-lookup"><span data-stu-id="c297e-113">The following illustration shows how you access a personal tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Ilustración que muestra el cajón de la aplicación móvil de Teams." border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="c297e-115">Acceso a pestañas de canal</span><span class="sxs-lookup"><span data-stu-id="c297e-115">Accessing channel tabs</span></span>

<span data-ttu-id="c297e-116">En la siguiente ilustración se muestra cómo obtener acceso a una pestaña de canal en dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="c297e-116">The following illustration shows how you access a channel tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Ilustración que muestra una pestaña móvil de Teams." border="false":::

## <a name="design-considerations"></a><span data-ttu-id="c297e-118">Consideraciones sobre diseño</span><span class="sxs-lookup"><span data-stu-id="c297e-118">Design considerations</span></span>

<span data-ttu-id="c297e-119">Nuestra plataforma móvil permite que las aplicaciones sean una experiencia envolvente con el contenido de la aplicación que toma toda la pantalla, aparte de la navegación principal de Teams.</span><span class="sxs-lookup"><span data-stu-id="c297e-119">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="c297e-120">Para crear una experiencia envolvente que se ajuste a Teams, siga estas instrucciones.</span><span class="sxs-lookup"><span data-stu-id="c297e-120">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="c297e-121">Diseño dinámico</span><span class="sxs-lookup"><span data-stu-id="c297e-121">Responsive design</span></span>

<span data-ttu-id="c297e-122">Dado que la pestaña se puede abrir en dispositivos con una amplia gama de tamaños de pantalla, debe seguir los principios [de diseño dinámicos.](https://www.w3schools.com/html/html_responsive.asp)</span><span class="sxs-lookup"><span data-stu-id="c297e-122">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="c297e-123">Todas las construcciones clave deben ser accesibles en dispositivos móviles y las vistas no deben distorsionarse.</span><span class="sxs-lookup"><span data-stu-id="c297e-123">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="c297e-124">Asegúrate de que cuando la pestaña se carga en un dispositivo móvil, todos los botones y vínculos sean fácilmente accesibles mediante la navegación basada en el dedo.</span><span class="sxs-lookup"><span data-stu-id="c297e-124">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="c297e-125">Diseños</span><span class="sxs-lookup"><span data-stu-id="c297e-125">Layouts</span></span>

<span data-ttu-id="c297e-126">Es importante elegir el diseño correcto para la pestaña.</span><span class="sxs-lookup"><span data-stu-id="c297e-126">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="c297e-127">Debes tener en cuenta el tipo de información que presentas y elegir un diseño que la organice para facilitar el consumo.</span><span class="sxs-lookup"><span data-stu-id="c297e-127">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="c297e-128">A continuación se describen algunas opciones posibles.</span><span class="sxs-lookup"><span data-stu-id="c297e-128">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="c297e-129">Lienzo único</span><span class="sxs-lookup"><span data-stu-id="c297e-129">Single canvas</span></span>

<span data-ttu-id="c297e-130">Esta es una gran área donde se realiza el trabajo.</span><span class="sxs-lookup"><span data-stu-id="c297e-130">This is one large area where work gets done.</span></span> <span data-ttu-id="c297e-131">La aplicación wiki de Teams sigue este patrón.</span><span class="sxs-lookup"><span data-stu-id="c297e-131">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="c297e-132">Si tienes una aplicación que no separa el contenido en componentes más pequeños, sería una buena opción.</span><span class="sxs-lookup"><span data-stu-id="c297e-132">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Ilustración que muestra una pestaña de lienzo único móvil de Teams." border="false":::

#### <a name="list"></a><span data-ttu-id="c297e-134">Lista</span><span class="sxs-lookup"><span data-stu-id="c297e-134">List</span></span>

<span data-ttu-id="c297e-135">Las listas son excelentes para ordenar y filtrar grandes cantidades de datos y son excelentes para mantener lo más importante en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="c297e-135">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="c297e-136">Es útil usar columnas que se pueden ordenar.</span><span class="sxs-lookup"><span data-stu-id="c297e-136">It is helpful to use sortable columns.</span></span> <span data-ttu-id="c297e-137">Las acciones se pueden agregar a cada elemento de lista en el menú de puntos suspensivos.</span><span class="sxs-lookup"><span data-stu-id="c297e-137">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Ilustración que muestra una pestaña de lista móvil de Teams." border="false":::

#### <a name="grid"></a><span data-ttu-id="c297e-139">Cuadrícula</span><span class="sxs-lookup"><span data-stu-id="c297e-139">Grid</span></span>

<span data-ttu-id="c297e-140">Las cuadrículas son útiles para mostrar elementos que son altamente visuales.</span><span class="sxs-lookup"><span data-stu-id="c297e-140">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="c297e-141">Ayuda a incluir un filtro o control de búsqueda en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="c297e-141">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="Ilustración que muestra una pestaña móvil de Teams con un diseño de cuadrícula." border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="c297e-143">Pestañas con bots en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="c297e-143">Tabs with bots on mobile</span></span>

<span data-ttu-id="c297e-144">El siguiente ejemplo es una aplicación personal que tiene pestañas y un bot.</span><span class="sxs-lookup"><span data-stu-id="c297e-144">The following example is a personal app that has tabs and a bot.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="Ilustración que muestra cómo la aplicación móvil de Teams que tiene pestañas y un bot." border="false":::

## <a name="ui-components"></a><span data-ttu-id="c297e-146">Componentes de la interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="c297e-146">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="c297e-147">Paletas de colores</span><span class="sxs-lookup"><span data-stu-id="c297e-147">Color palettes</span></span>

<span data-ttu-id="c297e-148">Usar nuestra paleta neutra aprobada para fondos, notificaciones, texto y botones ayudará a su aplicación a sentirse más como en casa en Teams.</span><span class="sxs-lookup"><span data-stu-id="c297e-148">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="c297e-149">Dado que Teams para dispositivos móviles tiene dos temas de colores (claro y oscuro), es una buena idea asegurarse de que la aplicación tenga un aspecto excelente en ambos.</span><span class="sxs-lookup"><span data-stu-id="c297e-149">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="c297e-150">Color claro</span><span class="sxs-lookup"><span data-stu-id="c297e-150">Light color</span></span>

![paleta de colores claros](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="c297e-152">Color oscuro</span><span class="sxs-lookup"><span data-stu-id="c297e-152">Dark color</span></span>

![paleta de colores oscuros](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="c297e-154">Botones y controles</span><span class="sxs-lookup"><span data-stu-id="c297e-154">Buttons and controls</span></span>

<span data-ttu-id="c297e-155">El estilo de los botones ayuda a comunicar el tipo de acción que desencadenan.</span><span class="sxs-lookup"><span data-stu-id="c297e-155">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="c297e-156">Mantenemos una amplia gama de botones con formato para mostrar diferentes niveles de énfasis.</span><span class="sxs-lookup"><span data-stu-id="c297e-156">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="c297e-157">Los botones pueden tener texto, un icono o una combinación de texto y un icono.</span><span class="sxs-lookup"><span data-stu-id="c297e-157">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="c297e-158">Para comunicar distintos niveles en una jerarquía, hemos diseñado botones principales y secundarios dentro de cada categoría.</span><span class="sxs-lookup"><span data-stu-id="c297e-158">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="c297e-159">Botones</span><span class="sxs-lookup"><span data-stu-id="c297e-159">Buttons</span></span>

<span data-ttu-id="c297e-160">Botones principales y secundarios.</span><span class="sxs-lookup"><span data-stu-id="c297e-160">Primary and secondary buttons.</span></span>

![imagen de botones](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="c297e-162">Controles de selección</span><span class="sxs-lookup"><span data-stu-id="c297e-162">Selection controls</span></span>

<span data-ttu-id="c297e-163">Botones de radio, casillas y alternancias.</span><span class="sxs-lookup"><span data-stu-id="c297e-163">Radio buttons, checkboxes, and toggles.</span></span>

![controles de selección](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="c297e-165">Gotalets y receptaciones</span><span class="sxs-lookup"><span data-stu-id="c297e-165">Chiclets and pills</span></span>

![receptlets y receptaciones](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="c297e-167">Tipografía</span><span class="sxs-lookup"><span data-stu-id="c297e-167">Typography</span></span>

<span data-ttu-id="c297e-168">La tipografía debe ser clara y con propósito.</span><span class="sxs-lookup"><span data-stu-id="c297e-168">Typography should be clear and purposeful.</span></span> <span data-ttu-id="c297e-169">Enfatiza información importante y evita usar varias fuentes y tamaños para reducir la confusión.</span><span class="sxs-lookup"><span data-stu-id="c297e-169">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="c297e-170">Se recomienda usar el caso de oración y evitar el uso de todas las mayúsculas para localización y legibilidad.</span><span class="sxs-lookup"><span data-stu-id="c297e-170">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![tipografía móvil](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="c297e-172">Campos y menús desplegables</span><span class="sxs-lookup"><span data-stu-id="c297e-172">Fields and flyouts</span></span>

<span data-ttu-id="c297e-173">Los campos son áreas donde los usuarios pueden introducir texto.</span><span class="sxs-lookup"><span data-stu-id="c297e-173">Fields are areas where users can input text.</span></span> <span data-ttu-id="c297e-174">Los menús desplegables son más ligeros que los cuadros de diálogo y aparecen en el panel superior.</span><span class="sxs-lookup"><span data-stu-id="c297e-174">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="c297e-175">Enumerar controles</span><span class="sxs-lookup"><span data-stu-id="c297e-175">List controls</span></span>

![controles de lista móvil](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="c297e-177">Controles de campo</span><span class="sxs-lookup"><span data-stu-id="c297e-177">Field controls</span></span>

![controles de campo móvil](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="c297e-179">Consideraciones para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="c297e-179">Developer considerations</span></span>

<span data-ttu-id="c297e-180">Cuando cree una aplicación que incluya una pestaña, debe tener en cuenta (y probar) cómo funcionará la pestaña en los clientes de Microsoft Teams para Android e iOS.</span><span class="sxs-lookup"><span data-stu-id="c297e-180">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="c297e-181">En las secciones siguientes se describen algunos de los escenarios clave que debe tener en cuenta.</span><span class="sxs-lookup"><span data-stu-id="c297e-181">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="c297e-182">Pruebas en clientes móviles</span><span class="sxs-lookup"><span data-stu-id="c297e-182">Testing on mobile clients</span></span>

<span data-ttu-id="c297e-183">Debe validar que la pestaña funciona correctamente en dispositivos móviles de distintos tamaños y cualidades.</span><span class="sxs-lookup"><span data-stu-id="c297e-183">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="c297e-184">Para dispositivos Android, puedes usar [DevTools para](~/tabs/how-to/developer-tools.md) depurar la pestaña mientras se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="c297e-184">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="c297e-185">Te recomendamos que pruebes tanto en dispositivos de alto y bajo rendimiento, como en una tableta.</span><span class="sxs-lookup"><span data-stu-id="c297e-185">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="authentication"></a><span data-ttu-id="c297e-186">Autenticación</span><span class="sxs-lookup"><span data-stu-id="c297e-186">Authentication</span></span>

<span data-ttu-id="c297e-187">Para que la autenticación funcione en clientes móviles, debe actualizar el SDK de JavaScript de Teams a la versión 1.4.1 como mínimo.</span><span class="sxs-lookup"><span data-stu-id="c297e-187">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="c297e-188">Ancho de banda bajo y conexiones intermitentes</span><span class="sxs-lookup"><span data-stu-id="c297e-188">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="c297e-189">Los clientes móviles necesitan funcionar regularmente con ancho de banda bajo y conexiones intermitentes.</span><span class="sxs-lookup"><span data-stu-id="c297e-189">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="c297e-190">La aplicación debe controlar los tiempos de espera correctamente proporcionando un mensaje contextual al usuario.</span><span class="sxs-lookup"><span data-stu-id="c297e-190">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="c297e-191">También debe incluir indicadores de progreso del usuario para proporcionar comentarios a los usuarios sobre los procesos de larga ejecución.</span><span class="sxs-lookup"><span data-stu-id="c297e-191">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

> [!NOTE]
> <span data-ttu-id="c297e-192">Las pestañas se habilitan en dispositivos móviles solo después de agregar la aplicación a una lista de permitidos, según la entrada del equipo de aprobación.</span><span class="sxs-lookup"><span data-stu-id="c297e-192">Tabs are enabled on mobile only after the application is added to an allow list, based on the input of the approval team.</span></span> <span data-ttu-id="c297e-193">Para comprobar la capacidad de respuesta de los dispositivos móviles, teamsubm@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="c297e-193">To check mobile responsiveness, reach out to teamsubm@microsoft.com.</span></span> 
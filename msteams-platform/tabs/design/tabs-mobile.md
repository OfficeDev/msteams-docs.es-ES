---
title: Pestañas en dispositivos móviles
description: Describe las instrucciones para diseñar pestañas que funcionan en dispositivos móviles.
keywords: guías de diseño de Microsoft Teams referencia del marco de trabajo de aplicaciones móviles
ms.openlocfilehash: a1939465b04a1fe4b803efaf83402852ca536059
ms.sourcegitcommit: b51a4982842948336cfabedb63bdf8f72703585e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/25/2020
ms.locfileid: "48279780"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="fb73d-104">Pestañas en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="fb73d-104">Tabs on mobile</span></span>

> [!NOTE]
> <span data-ttu-id="fb73d-105">Si elige que la ficha canal/grupo aparezca en los clientes móviles de Teams, la `setSettings()` configuración debe tener un valor para la `websiteUrl` propiedad (vea a continuación).</span><span class="sxs-lookup"><span data-stu-id="fb73d-105">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span>

<span data-ttu-id="fb73d-106">Las pestañas personalizadas pueden formar parte de un canal, un chat en grupo o una aplicación personal (aplicaciones que contienen pestañas estáticas y/o un bot de uno a uno).</span><span class="sxs-lookup"><span data-stu-id="fb73d-106">Custom tabs can be part of a channel, group chat, or personal app (apps that contain static tabs and/or a one-to-one bot).</span></span>

<span data-ttu-id="fb73d-107">Las aplicaciones personales están disponibles en los clientes móviles en el cajón de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fb73d-107">Personal apps are available on mobile clients in the app drawer.</span></span> <span data-ttu-id="fb73d-108">La aplicación solo se puede instalar desde un cliente de escritorio o Web, y puede tardar hasta 24 horas en aparecer en los clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="fb73d-108">The app can only be installed from a desktop or web client, and can take up to 24 hours to appear on mobile clients.</span></span>

<span data-ttu-id="fb73d-109">Las pestañas de canal también están disponibles en dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="fb73d-109">Channel tabs are also available on mobile.</span></span> <span data-ttu-id="fb73d-110">El comportamiento predeterminado es usar actualmente el `websiteUrl` para iniciar la pestaña en una ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="fb73d-110">The default behavior is currently to use your `websiteUrl` to launch your tab in a browser window.</span></span> <span data-ttu-id="fb73d-111">Sin embargo, se pueden cargar en un cliente móvil haciendo clic en el `...` menú de desbordamiento situado junto a la pestaña y seleccionando **abrir**, que usará el `contentUrl` para cargar la pestaña en el cliente móvil de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="fb73d-111">However, they can be loaded on a mobile client by clicking the `...` overflow menu next to the tab and choosing **Open**, which will use your `contentUrl` to load the tab inside the Teams mobile client.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="fb73d-112">Obtener acceso a pestañas personales</span><span class="sxs-lookup"><span data-stu-id="fb73d-112">Accessing personal tabs</span></span>

<span data-ttu-id="fb73d-113">La siguiente ilustración muestra cómo tener acceso a una pestaña personal en dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="fb73d-113">The following illustration shows how you access a personal tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Ilustración que muestra el alimentador de la aplicación móvil de Microsoft Teams." border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="fb73d-115">Acceso a las pestañas de canal</span><span class="sxs-lookup"><span data-stu-id="fb73d-115">Accessing channel tabs</span></span>

<span data-ttu-id="fb73d-116">La siguiente ilustración muestra cómo tener acceso a una ficha de canal en dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="fb73d-116">The following illustration shows how you access a channel tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Ilustración que muestra una pestaña de Microsoft Teams Mobile." border="false":::

## <a name="design-considerations"></a><span data-ttu-id="fb73d-118">Consideraciones sobre diseño</span><span class="sxs-lookup"><span data-stu-id="fb73d-118">Design considerations</span></span>

<span data-ttu-id="fb73d-119">Nuestra plataforma móvil permite que las aplicaciones sean una experiencia envolvente con el contenido de la aplicación y que se ocupe de toda la pantalla, además de la navegación principal de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="fb73d-119">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="fb73d-120">Para crear una experiencia envolvente que se ajuste a los equipos, siga estas instrucciones.</span><span class="sxs-lookup"><span data-stu-id="fb73d-120">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="fb73d-121">Diseño dinámico</span><span class="sxs-lookup"><span data-stu-id="fb73d-121">Responsive design</span></span>

<span data-ttu-id="fb73d-122">Como la pestaña se puede abrir en dispositivos con una amplia variedad de tamaños de pantalla, debe seguir los principios de [diseño de capacidad de respuesta](https://www.w3schools.com/html/html_responsive.asp) .</span><span class="sxs-lookup"><span data-stu-id="fb73d-122">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="fb73d-123">Todas las construcciones de clave deben ser accesibles en dispositivos móviles y las vistas no se deben distorsionar.</span><span class="sxs-lookup"><span data-stu-id="fb73d-123">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="fb73d-124">Asegúrese de que, al cargar la pestaña en un dispositivo móvil, se puede acceder fácilmente a todos los botones y vínculos mediante la navegación basada en el dedo.</span><span class="sxs-lookup"><span data-stu-id="fb73d-124">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="fb73d-125">Diseños</span><span class="sxs-lookup"><span data-stu-id="fb73d-125">Layouts</span></span>

<span data-ttu-id="fb73d-126">Es importante elegir el diseño correcto para la ficha.</span><span class="sxs-lookup"><span data-stu-id="fb73d-126">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="fb73d-127">Debe tener en cuenta el tipo de información que está presentando y elegir un diseño que la organice para un consumo sencillo.</span><span class="sxs-lookup"><span data-stu-id="fb73d-127">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="fb73d-128">A continuación se describen algunas de las posibles opciones.</span><span class="sxs-lookup"><span data-stu-id="fb73d-128">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="fb73d-129">Lienzo único</span><span class="sxs-lookup"><span data-stu-id="fb73d-129">Single canvas</span></span>

<span data-ttu-id="fb73d-130">Este es un área de gran tamaño en la que se realiza el trabajo.</span><span class="sxs-lookup"><span data-stu-id="fb73d-130">This is one large area where work gets done.</span></span> <span data-ttu-id="fb73d-131">La aplicación wiki de Teams sigue este patrón.</span><span class="sxs-lookup"><span data-stu-id="fb73d-131">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="fb73d-132">Si tiene una aplicación que no separa el contenido en componentes más pequeños, sería una buena opción.</span><span class="sxs-lookup"><span data-stu-id="fb73d-132">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Ilustración que muestra una pestaña de lienzo único de Teams Mobile." border="false":::

#### <a name="list"></a><span data-ttu-id="fb73d-134">Lista</span><span class="sxs-lookup"><span data-stu-id="fb73d-134">List</span></span>

<span data-ttu-id="fb73d-135">Las listas son excelentes para ordenar y filtrar grandes cantidades de datos y son excelentes para conservar las cosas más importantes en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="fb73d-135">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="fb73d-136">Es útil usar columnas que se puedan ordenar.</span><span class="sxs-lookup"><span data-stu-id="fb73d-136">It is helpful to use sortable columns.</span></span> <span data-ttu-id="fb73d-137">Se pueden agregar acciones a cada elemento de lista en el menú de puntos suspensivos.</span><span class="sxs-lookup"><span data-stu-id="fb73d-137">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Ilustración que muestra una pestaña de la lista de Teams para móviles." border="false":::

#### <a name="grid"></a><span data-ttu-id="fb73d-139">Redes</span><span class="sxs-lookup"><span data-stu-id="fb73d-139">Grid</span></span>

<span data-ttu-id="fb73d-140">Las cuadrículas son útiles para mostrar elementos que son muy visuales.</span><span class="sxs-lookup"><span data-stu-id="fb73d-140">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="fb73d-141">Ayuda a incluir un filtro o control de búsqueda en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="fb73d-141">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="Ilustración que muestra una pestaña de Microsoft Teams Mobile con un diseño de cuadrícula." border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="fb73d-143">Pestañas con bots en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="fb73d-143">Tabs with bots on mobile</span></span>

<span data-ttu-id="fb73d-144">El siguiente ejemplo es una aplicación personal que tiene pestañas y un bot.</span><span class="sxs-lookup"><span data-stu-id="fb73d-144">The following example is a personal app that has tabs and a bot.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="Ilustración que muestra la aplicación de equipos móviles que tiene pestañas y un bot." border="false":::

## <a name="ui-components"></a><span data-ttu-id="fb73d-146">Componentes de la interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="fb73d-146">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="fb73d-147">Paletas de colores</span><span class="sxs-lookup"><span data-stu-id="fb73d-147">Color palettes</span></span>

<span data-ttu-id="fb73d-148">El uso de nuestra paleta neutra aprobada para fondos, notificaciones, texto y botones ayudará a que la aplicación se sienta más en casa en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="fb73d-148">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="fb73d-149">Como Teams Mobile tiene dos temas de color (claro y oscuro), es una buena idea asegurarse de que la aplicación tenga un aspecto excelente en ambos.</span><span class="sxs-lookup"><span data-stu-id="fb73d-149">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="fb73d-150">Color claro</span><span class="sxs-lookup"><span data-stu-id="fb73d-150">Light color</span></span>

![paleta de colores claros](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="fb73d-152">Color oscuro</span><span class="sxs-lookup"><span data-stu-id="fb73d-152">Dark color</span></span>

![paleta de colores oscuro](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="fb73d-154">Botones y controles</span><span class="sxs-lookup"><span data-stu-id="fb73d-154">Buttons and controls</span></span>

<span data-ttu-id="fb73d-155">La forma en que los botones están estilo ayuda a comunicar el tipo de acción que desencadenan.</span><span class="sxs-lookup"><span data-stu-id="fb73d-155">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="fb73d-156">Mantenemos una amplia gama de botones que tienen formato para mostrar distintos niveles de énfasis.</span><span class="sxs-lookup"><span data-stu-id="fb73d-156">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="fb73d-157">Los botones pueden tener texto, un icono o una combinación de texto y un icono.</span><span class="sxs-lookup"><span data-stu-id="fb73d-157">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="fb73d-158">Para comunicar distintos niveles de una jerarquía, se diseñaron botones principales y secundarios dentro de cada categoría.</span><span class="sxs-lookup"><span data-stu-id="fb73d-158">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="fb73d-159">Botones</span><span class="sxs-lookup"><span data-stu-id="fb73d-159">Buttons</span></span>

<span data-ttu-id="fb73d-160">Botones principal y secundario.</span><span class="sxs-lookup"><span data-stu-id="fb73d-160">Primary and secondary buttons.</span></span>

![imagen de botones](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="fb73d-162">Controles de selección</span><span class="sxs-lookup"><span data-stu-id="fb73d-162">Selection controls</span></span>

<span data-ttu-id="fb73d-163">Botones de opción, casillas de verificación y alternancias.</span><span class="sxs-lookup"><span data-stu-id="fb73d-163">Radio buttons, checkboxes, and toggles.</span></span>

![controles de selección](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="fb73d-165">Chiclets y píldoras</span><span class="sxs-lookup"><span data-stu-id="fb73d-165">Chiclets and pills</span></span>

![Chiclets y píldoras](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="fb73d-167">Tipografía</span><span class="sxs-lookup"><span data-stu-id="fb73d-167">Typography</span></span>

<span data-ttu-id="fb73d-168">La tipografía debe ser clara y intencionada.</span><span class="sxs-lookup"><span data-stu-id="fb73d-168">Typography should be clear and purposeful.</span></span> <span data-ttu-id="fb73d-169">Resalte la información importante y evite usar varias fuentes y tamaños para reducir la confusión.</span><span class="sxs-lookup"><span data-stu-id="fb73d-169">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="fb73d-170">Se recomienda usar el tipo de oración y evitar el uso de mayúsculas y minúsculas para la localización y la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="fb73d-170">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![tipografía móvil](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="fb73d-172">Campos y controles flotantes</span><span class="sxs-lookup"><span data-stu-id="fb73d-172">Fields and flyouts</span></span>

<span data-ttu-id="fb73d-173">Los campos son áreas en las que los usuarios pueden escribir texto.</span><span class="sxs-lookup"><span data-stu-id="fb73d-173">Fields are areas where users can input text.</span></span> <span data-ttu-id="fb73d-174">Los controles flotantes son más sencillos que los cuadros de diálogo y aparecen en el panel superior.</span><span class="sxs-lookup"><span data-stu-id="fb73d-174">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="fb73d-175">Enumerar controles</span><span class="sxs-lookup"><span data-stu-id="fb73d-175">List controls</span></span>

![controles de lista de dispositivos móviles](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="fb73d-177">Controles de campo</span><span class="sxs-lookup"><span data-stu-id="fb73d-177">Field controls</span></span>

![controles de campo de dispositivos móviles](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="fb73d-179">Consideraciones para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="fb73d-179">Developer considerations</span></span>

<span data-ttu-id="fb73d-180">Al crear una aplicación que incluya una pestaña, debe tener en cuenta (y probar) cómo funcionará la pestaña en los clientes de Android e iOS de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="fb73d-180">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="fb73d-181">En las secciones siguientes se describen algunos de los escenarios clave que debe tener en cuenta.</span><span class="sxs-lookup"><span data-stu-id="fb73d-181">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="fb73d-182">Pruebas en clientes móviles</span><span class="sxs-lookup"><span data-stu-id="fb73d-182">Testing on mobile clients</span></span>

<span data-ttu-id="fb73d-183">Debe validar que la pestaña funcione correctamente en dispositivos móviles de varios tamaños y cualidades.</span><span class="sxs-lookup"><span data-stu-id="fb73d-183">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="fb73d-184">Para dispositivos Android, puede usar [DevTools](~/tabs/how-to/developer-tools.md) para depurar la pestaña mientras se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="fb73d-184">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="fb73d-185">Le recomendamos que realice pruebas tanto en los dispositivos de rendimiento alto como en los de baja performance, así como en tabletas.</span><span class="sxs-lookup"><span data-stu-id="fb73d-185">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="authentication"></a><span data-ttu-id="fb73d-186">Autenticación</span><span class="sxs-lookup"><span data-stu-id="fb73d-186">Authentication</span></span>

<span data-ttu-id="fb73d-187">Para que la autenticación funcione en los clientes móviles, debe actualizar el SDK de Teams de JavaScript a la versión 1.4.1 como mínimo.</span><span class="sxs-lookup"><span data-stu-id="fb73d-187">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="fb73d-188">Bajo ancho de banda y conexiones intermitentes</span><span class="sxs-lookup"><span data-stu-id="fb73d-188">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="fb73d-189">Los clientes móviles necesitan tener que funcionar con frecuencia con ancho de banda bajo y conexiones intermitentes.</span><span class="sxs-lookup"><span data-stu-id="fb73d-189">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="fb73d-190">La aplicación debe controlar los tiempos de espera de forma adecuada al suministrar un mensaje contextual al usuario.</span><span class="sxs-lookup"><span data-stu-id="fb73d-190">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="fb73d-191">También debe indicar los indicadores de progreso del usuario para proporcionar comentarios a los usuarios sobre los procesos de ejecución prolongada.</span><span class="sxs-lookup"><span data-stu-id="fb73d-191">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

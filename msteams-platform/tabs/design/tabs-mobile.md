---
title: Pestañas en dispositivos móviles
description: Describe las instrucciones para diseñar pestañas que funcionan en dispositivos móviles.
keywords: guías de diseño de Microsoft Teams referencia del marco de trabajo de aplicaciones móviles
ms.openlocfilehash: d47039c245b8e262af6e1f60bc0c644dc7e65bd6
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/15/2020
ms.locfileid: "47819049"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="9277e-104">Pestañas en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="9277e-104">Tabs on mobile</span></span>

> [!NOTE]
> <span data-ttu-id="9277e-105">Si elige que la ficha canal/grupo aparezca en los clientes móviles de Teams, la `setSettings()` configuración debe tener un valor para la `websiteUrl` propiedad (vea a continuación).</span><span class="sxs-lookup"><span data-stu-id="9277e-105">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span>

<span data-ttu-id="9277e-106">Las pestañas personalizadas pueden formar parte de un canal, un chat en grupo o una aplicación personal (aplicaciones que contienen pestañas estáticas y/o un bot de uno a uno).</span><span class="sxs-lookup"><span data-stu-id="9277e-106">Custom tabs can be part of a channel, group chat, or personal app (apps that contain static tabs and/or a one-to-one bot).</span></span>

<span data-ttu-id="9277e-107">Las aplicaciones personales están disponibles en los clientes móviles en el cajón de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9277e-107">Personal apps are available on mobile clients in the App Drawer.</span></span> <span data-ttu-id="9277e-108">La aplicación solo se puede instalar desde un cliente de escritorio o Web, y puede tardar hasta 24 horas en aparecer en los clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="9277e-108">The app can only be installed from a desktop or web client, and can take up to 24 hours to appear on mobile clients.</span></span>

<span data-ttu-id="9277e-109">Las fichas grupo y canal también están disponibles en los clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="9277e-109">Group and channel tabs are available on mobile clients as well.</span></span> <span data-ttu-id="9277e-110">El comportamiento predeterminado es usar actualmente el `websiteUrl` para iniciar la pestaña en una ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="9277e-110">The default behavior is currently to use your `websiteUrl` to launch your tab in a browser window.</span></span> <span data-ttu-id="9277e-111">Sin embargo, se pueden cargar en un cliente móvil haciendo clic en el `...` menú de desbordamiento situado junto a la pestaña y seleccionando **abrir**, que usará el `contentUrl` para cargar la pestaña en el cliente móvil de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="9277e-111">However, they can be loaded on a mobile client by clicking the `...` overflow menu next to the tab and choosing **Open**, which will use your `contentUrl` to load the tab inside the Teams mobile client.</span></span>

![alimentador de aplicaciones móviles](../../assets/images/personal-app-mobile.png)

## <a name="developer-considerations-for-mobile-support"></a><span data-ttu-id="9277e-113">Consideraciones para desarrolladores para la compatibilidad con dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="9277e-113">Developer considerations for mobile support</span></span>

<span data-ttu-id="9277e-114">Al crear una aplicación que incluya una pestaña, debe tener en cuenta (y probar) cómo funcionará la pestaña en los clientes de Android e iOS de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="9277e-114">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="9277e-115">En las secciones siguientes se describen algunos de los escenarios clave que debe tener en cuenta.</span><span class="sxs-lookup"><span data-stu-id="9277e-115">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="9277e-116">Pruebas en clientes móviles</span><span class="sxs-lookup"><span data-stu-id="9277e-116">Testing on mobile clients</span></span>

<span data-ttu-id="9277e-117">Debe validar que la pestaña funcione correctamente en dispositivos móviles de varios tamaños y cualidades.</span><span class="sxs-lookup"><span data-stu-id="9277e-117">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="9277e-118">Para dispositivos Android, puede usar [DevTools](~/tabs/how-to/developer-tools.md) para depurar la pestaña mientras se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="9277e-118">For Android devices you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="9277e-119">Le recomendamos que realice pruebas tanto en los dispositivos de rendimiento alto como en los de baja performance, así como en tabletas.</span><span class="sxs-lookup"><span data-stu-id="9277e-119">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="9277e-120">Diseño dinámico</span><span class="sxs-lookup"><span data-stu-id="9277e-120">Responsive design</span></span>

<span data-ttu-id="9277e-121">Como la pestaña se puede abrir en dispositivos con una amplia variedad de tamaños de pantalla, debe seguir los principios de [diseño de capacidad de respuesta](https://www.w3schools.com/html/html_responsive.asp) .</span><span class="sxs-lookup"><span data-stu-id="9277e-121">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="9277e-122">Todas las construcciones de clave deben ser accesibles en dispositivos móviles y las vistas no se deben distorsionar.</span><span class="sxs-lookup"><span data-stu-id="9277e-122">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="9277e-123">Asegúrese de que, al cargar la pestaña en un dispositivo móvil, se puede acceder fácilmente a todos los botones y vínculos mediante la navegación basada en el dedo.</span><span class="sxs-lookup"><span data-stu-id="9277e-123">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="authentication"></a><span data-ttu-id="9277e-124">Autenticación</span><span class="sxs-lookup"><span data-stu-id="9277e-124">Authentication</span></span>

<span data-ttu-id="9277e-125">Para que la autenticación funcione en los clientes móviles, es necesario actualizar el SDK de Microsoft Team JS al menos a la versión 1.4.1.</span><span class="sxs-lookup"><span data-stu-id="9277e-125">For authentication to work on mobile clients, you must upgrade you Teams JS SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth--intermittent-connections"></a><span data-ttu-id="9277e-126">Poco ancho de banda & conexiones intermitentes</span><span class="sxs-lookup"><span data-stu-id="9277e-126">Low bandwidth & intermittent connections</span></span>

<span data-ttu-id="9277e-127">Los clientes móviles necesitan tener que funcionar con frecuencia con ancho de banda bajo y conexiones intermitentes.</span><span class="sxs-lookup"><span data-stu-id="9277e-127">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="9277e-128">La aplicación debe controlar los tiempos de espera de forma adecuada al suministrar un mensaje contextual al usuario.</span><span class="sxs-lookup"><span data-stu-id="9277e-128">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="9277e-129">También debe indicar los indicadores de progreso del usuario para proporcionar comentarios a los usuarios sobre los procesos de ejecución prolongada.</span><span class="sxs-lookup"><span data-stu-id="9277e-129">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

## <a name="design-considerations-for-mobile"></a><span data-ttu-id="9277e-130">Consideraciones de diseño para dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="9277e-130">Design considerations for mobile</span></span>

<span data-ttu-id="9277e-131">Nuestra plataforma móvil permite que las aplicaciones sean una experiencia envolvente con el contenido de la aplicación y que se ocupe de toda la pantalla, además de la navegación principal de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="9277e-131">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="9277e-132">Para crear una experiencia envolvente que se ajuste sin problemas en el cliente de Microsoft Teams, siga las instrucciones que se indican a continuación.</span><span class="sxs-lookup"><span data-stu-id="9277e-132">To create an immersive experience that fits seamlessly within the Microsoft Teams client, follow the guidelines below.</span></span>

### <a name="layouts"></a><span data-ttu-id="9277e-133">Diseños</span><span class="sxs-lookup"><span data-stu-id="9277e-133">Layouts</span></span>

<span data-ttu-id="9277e-134">Es importante elegir el diseño correcto para la ficha.</span><span class="sxs-lookup"><span data-stu-id="9277e-134">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="9277e-135">Debe tener en cuenta el tipo de información que está presentando y elegir un diseño que la organice para un consumo sencillo.</span><span class="sxs-lookup"><span data-stu-id="9277e-135">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="9277e-136">A continuación se describen algunas de las posibles opciones.</span><span class="sxs-lookup"><span data-stu-id="9277e-136">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="9277e-137">Lienzo único</span><span class="sxs-lookup"><span data-stu-id="9277e-137">Single canvas</span></span>

<span data-ttu-id="9277e-138">Este es un área de gran tamaño en la que se realiza el trabajo.</span><span class="sxs-lookup"><span data-stu-id="9277e-138">This is one large area where work gets done.</span></span> <span data-ttu-id="9277e-139">La aplicación wiki sigue este patrón.</span><span class="sxs-lookup"><span data-stu-id="9277e-139">The Wiki app follows this pattern.</span></span> <span data-ttu-id="9277e-140">Si tiene una aplicación que no separa el contenido en componentes más pequeños, sería una buena opción.</span><span class="sxs-lookup"><span data-stu-id="9277e-140">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

![diseño de un solo lienzo](~/assets/images/mobile-single-canvas.png)

#### <a name="list"></a><span data-ttu-id="9277e-142">Lista</span><span class="sxs-lookup"><span data-stu-id="9277e-142">List</span></span>

<span data-ttu-id="9277e-143">Las listas son excelentes para ordenar y filtrar grandes cantidades de datos y son excelentes para conservar las cosas más importantes en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="9277e-143">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="9277e-144">Es útil usar columnas que se puedan ordenar.</span><span class="sxs-lookup"><span data-stu-id="9277e-144">It is helpful to use sortable columns.</span></span> <span data-ttu-id="9277e-145">Se pueden agregar acciones a cada elemento de lista en el menú de puntos suspensivos.</span><span class="sxs-lookup"><span data-stu-id="9277e-145">Actions can be added to each list item under the ellipsis menu.</span></span>

![diseño de lista](~/assets/images/mobile-list.png)

#### <a name="grid"></a><span data-ttu-id="9277e-147">Redes</span><span class="sxs-lookup"><span data-stu-id="9277e-147">Grid</span></span>

<span data-ttu-id="9277e-148">Las cuadrículas son útiles para mostrar elementos que son muy visuales.</span><span class="sxs-lookup"><span data-stu-id="9277e-148">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="9277e-149">Ayuda a incluir un filtro o control de búsqueda en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="9277e-149">It helps to include a filter or search control at the top.</span></span>

![diseño de cuadrícula](~/assets/images/mobile-grid.png)

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="9277e-151">Pestañas con bots en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="9277e-151">Tabs with bots on mobile</span></span>

<span data-ttu-id="9277e-152">La siguiente es una aplicación personal de ejemplo que contiene dos pestañas estáticas y un bot.</span><span class="sxs-lookup"><span data-stu-id="9277e-152">The below is an example personal app that contains two static tabs and a bot.</span></span>

![pestañas y bots en dispositivos móviles](~/assets/images/mobile-tab-with-bot.png)

### <a name="ui-components"></a><span data-ttu-id="9277e-154">Componentes de UI</span><span class="sxs-lookup"><span data-stu-id="9277e-154">UI Components</span></span>

#### <a name="color-palettes"></a><span data-ttu-id="9277e-155">Paletas de colores</span><span class="sxs-lookup"><span data-stu-id="9277e-155">Color palettes</span></span>

<span data-ttu-id="9277e-156">El uso de nuestra paleta neutra aprobada para fondos, notificaciones, texto y botones ayudará a que la aplicación se sienta más en casa en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="9277e-156">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="9277e-157">Como Teams Mobile tiene dos temas de color (claro y oscuro), es una buena idea asegurarse de que la aplicación tenga un aspecto excelente en ambos.</span><span class="sxs-lookup"><span data-stu-id="9277e-157">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

##### <a name="light-color"></a><span data-ttu-id="9277e-158">Color claro</span><span class="sxs-lookup"><span data-stu-id="9277e-158">Light color</span></span>

![paleta de colores claros](~/assets/images/light-color.png)

##### <a name="dark-color"></a><span data-ttu-id="9277e-160">Color oscuro</span><span class="sxs-lookup"><span data-stu-id="9277e-160">Dark color</span></span>

![paleta de colores oscuro](~/assets/images/dark-color.png)

#### <a name="buttons-and-controls"></a><span data-ttu-id="9277e-162">Botones y controles</span><span class="sxs-lookup"><span data-stu-id="9277e-162">Buttons and controls</span></span>

<span data-ttu-id="9277e-163">La forma en que los botones están estilo ayuda a comunicar el tipo de acción que desencadenan.</span><span class="sxs-lookup"><span data-stu-id="9277e-163">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="9277e-164">Mantenemos una amplia gama de botones que tienen formato para mostrar distintos niveles de énfasis.</span><span class="sxs-lookup"><span data-stu-id="9277e-164">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="9277e-165">Los botones pueden tener texto, un icono o una combinación de texto y un icono.</span><span class="sxs-lookup"><span data-stu-id="9277e-165">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="9277e-166">Para comunicar distintos niveles de una jerarquía, se diseñaron botones principales y secundarios dentro de cada categoría.</span><span class="sxs-lookup"><span data-stu-id="9277e-166">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

![imagen de botones](~/assets/images/buttons.png)

![controles de selección](~/assets/images/selection-controls.png)

![Chiclets y píldoras](~/assets/images/chiclets-and-pills.png)

#### <a name="typography"></a><span data-ttu-id="9277e-170">Tipografía</span><span class="sxs-lookup"><span data-stu-id="9277e-170">Typography</span></span>

<span data-ttu-id="9277e-171">La tipografía debe ser clara y intencionada.</span><span class="sxs-lookup"><span data-stu-id="9277e-171">Typography should be clear and purposeful.</span></span> <span data-ttu-id="9277e-172">Resalte la información importante y evite usar varias fuentes y tamaños para reducir la confusión.</span><span class="sxs-lookup"><span data-stu-id="9277e-172">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="9277e-173">Se recomienda usar el tipo de oración y evitar el uso de mayúsculas y minúsculas para la localización y la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="9277e-173">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![tipografía móvil](~/assets/images/mobile-typography.png)

#### <a name="fields-and-flyouts"></a><span data-ttu-id="9277e-175">Campos y controles flotantes</span><span class="sxs-lookup"><span data-stu-id="9277e-175">Fields and Flyouts</span></span>

<span data-ttu-id="9277e-176">Los campos son áreas en las que los usuarios pueden escribir texto.</span><span class="sxs-lookup"><span data-stu-id="9277e-176">Fields are areas where users can input text.</span></span> <span data-ttu-id="9277e-177">Los controles flotantes son más sencillos que los cuadros de diálogo y aparecen en el panel superior.</span><span class="sxs-lookup"><span data-stu-id="9277e-177">Flyouts are more lightweight than dialogs, and appear from the top pane.</span></span>

##### <a name="list-controls"></a><span data-ttu-id="9277e-178">Enumerar controles</span><span class="sxs-lookup"><span data-stu-id="9277e-178">List controls</span></span>

![controles de lista de dispositivos móviles](~/assets/images/mobile-list-controls.png)

##### <a name="field-controls"></a><span data-ttu-id="9277e-180">Controles de campo</span><span class="sxs-lookup"><span data-stu-id="9277e-180">Field controls</span></span>

![controles de campo de dispositivos móviles](~/assets/images/mobile-field-controls.png)

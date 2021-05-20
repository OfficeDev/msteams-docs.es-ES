---
title: Diseñar la aplicación con plantillas de interfaz de usuario
author: heath-hamilton
description: Diseñe la aplicación más rápido con componentes, diseños y patrones de interfaz de usuario estandarizados que se ven normalmente en Microsoft Teams.
ms.author: lajanuar
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: 0cd5c6c4525e340f9aa53a78749211783880225a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566022"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a><span data-ttu-id="d42d9-103">Diseñar la aplicación Microsoft Teams con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="d42d9-103">Designing your Microsoft Teams app with UI templates</span></span>

<span data-ttu-id="d42d9-104">Diseña tu aplicación Microsoft Teams más rápido con plantillas de interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="d42d9-104">Design your Microsoft Teams app faster with UI templates.</span></span> <span data-ttu-id="d42d9-105">Las plantillas son una colección de componentes basados en la interfaz de usuario fluida que funcionan en casos comunes de uso Teams, lo que le da más tiempo para averiguar la mejor experiencia para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="d42d9-105">The templates are a collection of Fluent UI-based components that work across common Teams use cases, giving you more time to figure out the best experience for your users.</span></span>

## <a name="getting-started-with-tools-and-samples"></a><span data-ttu-id="d42d9-106">Introducción a herramientas y muestras</span><span class="sxs-lookup"><span data-stu-id="d42d9-106">Getting started with tools and samples</span></span>

<span data-ttu-id="d42d9-107">Los siguientes recursos pueden ayudarle a diseñar y desarrollar la aplicación mediante plantillas de interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="d42d9-107">The following resources can help you design and develop your app using UI templates.</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="d42d9-108">Kit de UI de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d42d9-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="d42d9-109">Grabe plantillas de interfaz de usuario para el diseño de la aplicación desde el Kit de interfaz de usuario de Microsoft Teams, que también incluye información amplia sobre el uso, anatomía, accesibilidad y prácticas recomendadas.</span><span class="sxs-lookup"><span data-stu-id="d42d9-109">Grab UI templates for your app design from the Microsoft Teams UI Kit, which also includes extensive information about usage, anatomy, accessibility, and best practices.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d42d9-110">Obtener el kit de interfaz de usuario (Figma)</span><span class="sxs-lookup"><span data-stu-id="d42d9-110">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="d42d9-111">Microsoft Teams Biblioteca de IU</span><span class="sxs-lookup"><span data-stu-id="d42d9-111">Microsoft Teams UI Library</span></span>

<span data-ttu-id="d42d9-112">Vea y pruebe plantillas de interfaz de usuario Teams individuales y componentes relacionados en el explorador.</span><span class="sxs-lookup"><span data-stu-id="d42d9-112">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d42d9-113">Pruebe la biblioteca de interfaz de usuario (área de juegos)</span><span class="sxs-lookup"><span data-stu-id="d42d9-113">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="d42d9-114">Importe estas plantillas y componentes relacionados directamente en el proyecto de aplicación Teams.</span><span class="sxs-lookup"><span data-stu-id="d42d9-114">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d42d9-115">Obtener la biblioteca de interfaz de usuario (GitHub)</span><span class="sxs-lookup"><span data-stu-id="d42d9-115">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="d42d9-116">Aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d42d9-116">Sample app</span></span>

<span data-ttu-id="d42d9-117">Instale una aplicación de ejemplo para ver cómo se ven y se comportan las plantillas de interfaz de usuario en contextos Teams.</span><span class="sxs-lookup"><span data-stu-id="d42d9-117">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d42d9-118">Obtener la aplicación de ejemplo (GitHub)</span><span class="sxs-lookup"><span data-stu-id="d42d9-118">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="list"></a><span data-ttu-id="d42d9-119">Lista</span><span class="sxs-lookup"><span data-stu-id="d42d9-119">List</span></span>

<span data-ttu-id="d42d9-120">Puede usar una lista para mostrar elementos relacionados en un formato escaneable y permitir a los usuarios realizar acciones en una lista completa o en elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="d42d9-120">You can use a list to display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de lista." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="d42d9-122">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="d42d9-122">Top use cases</span></span>

* <span data-ttu-id="d42d9-123">Mostrar datos</span><span class="sxs-lookup"><span data-stu-id="d42d9-123">Display data</span></span>
* <span data-ttu-id="d42d9-124">Acciones contextuales sobre el contenido de la aplicación</span><span class="sxs-lookup"><span data-stu-id="d42d9-124">Contextual actions on app content</span></span>

## <a name="dashboard"></a><span data-ttu-id="d42d9-125">Panel</span><span class="sxs-lookup"><span data-stu-id="d42d9-125">Dashboard</span></span>

<span data-ttu-id="d42d9-126">Un panel muestra diferentes tipos de contenido en una ubicación central (Teams aplicación personal o pestaña).</span><span class="sxs-lookup"><span data-stu-id="d42d9-126">A dashboard displays different types of content in a central location (Teams personal app or tab).</span></span> <span data-ttu-id="d42d9-127">Los usuarios deben poder personalizar al menos parte de lo que ven en un panel.</span><span class="sxs-lookup"><span data-stu-id="d42d9-127">Users should be able to customize at least some of what they see on a dashboard.</span></span>

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario del panel." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="d42d9-129">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="d42d9-129">Top use cases</span></span>

* <span data-ttu-id="d42d9-130">Analizar datos</span><span class="sxs-lookup"><span data-stu-id="d42d9-130">Analyze data</span></span>
* <span data-ttu-id="d42d9-131">Métricas del informe</span><span class="sxs-lookup"><span data-stu-id="d42d9-131">Report metrics</span></span>
* <span data-ttu-id="d42d9-132">Organizar diferentes información en un solo lugar</span><span class="sxs-lookup"><span data-stu-id="d42d9-132">Organize different information in one place</span></span>

## <a name="form"></a><span data-ttu-id="d42d9-133">Form</span><span class="sxs-lookup"><span data-stu-id="d42d9-133">Form</span></span>

<span data-ttu-id="d42d9-134">Los formularios se utilizan para recopilar, validar y enviar la entrada del usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="d42d9-134">Forms are used to collect, validate, and submit user input in a structured way.</span></span> <span data-ttu-id="d42d9-135">El etiquetado claro y las agrupaciones lógicas de los campos de entrada son fundamentales para una buena experiencia de usuario.</span><span class="sxs-lookup"><span data-stu-id="d42d9-135">Clear labeling and logical groupings of input fields are critical for a good user experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de formulario." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="d42d9-137">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="d42d9-137">Top use cases</span></span>

* <span data-ttu-id="d42d9-138">Iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="d42d9-138">Sign in</span></span>
* <span data-ttu-id="d42d9-139">Perfiles de usuario</span><span class="sxs-lookup"><span data-stu-id="d42d9-139">User profiles</span></span>
* <span data-ttu-id="d42d9-140">Configuración</span><span class="sxs-lookup"><span data-stu-id="d42d9-140">Settings</span></span>
* <span data-ttu-id="d42d9-141">Recopilación de entradas de usuario</span><span class="sxs-lookup"><span data-stu-id="d42d9-141">User input collection</span></span>

## <a name="sign-in"></a><span data-ttu-id="d42d9-142">Iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="d42d9-142">Sign in</span></span>

<span data-ttu-id="d42d9-143">Puede diseñar flujos de inicio de sesión de aplicaciones para diferentes contextos Teams y proveedores de identidades.</span><span class="sxs-lookup"><span data-stu-id="d42d9-143">You can design app sign-in flows for different Teams contexts and identity providers.</span></span> <span data-ttu-id="d42d9-144">En el ejemplo siguiente se incluye el inicio de sesión único (SSO), que se recomienda para la experiencia de autenticación más sencilla.</span><span class="sxs-lookup"><span data-stu-id="d42d9-144">The following example includes single sign-on (SSO), which we recommend for the simplest authentication experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="En el ejemplo se muestra un inicio de sesión en la plantilla de interfaz de usuario." border="false":::

### <a name="top-use-case"></a><span data-ttu-id="d42d9-146">Estuche de uso superior</span><span class="sxs-lookup"><span data-stu-id="d42d9-146">Top use case</span></span>

* <span data-ttu-id="d42d9-147">Autenticar usuarios</span><span class="sxs-lookup"><span data-stu-id="d42d9-147">Authenticate users</span></span>

## <a name="task-board"></a><span data-ttu-id="d42d9-148">Mesa de tareas</span><span class="sxs-lookup"><span data-stu-id="d42d9-148">Task board</span></span>

<span data-ttu-id="d42d9-149">Un tablero de tareas, a veces llamado tablero kanban o carriles de natación, es una colección de tarjetas que se utilizan a menudo para rastrear el estado de los artículos de trabajo o boletos.</span><span class="sxs-lookup"><span data-stu-id="d42d9-149">A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span> <span data-ttu-id="d42d9-150">También se puede utilizar para ordenar cualquier tipo de contenido en categorías.</span><span class="sxs-lookup"><span data-stu-id="d42d9-150">It can also be used to sort any type of content into categories.</span></span> <span data-ttu-id="d42d9-151">Puede editar y mover las tarjetas entre columnas.</span><span class="sxs-lookup"><span data-stu-id="d42d9-151">You can edit and move the cards between columns.</span></span>

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario del tablero de tareas." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="d42d9-153">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="d42d9-153">Top use cases</span></span>

* <span data-ttu-id="d42d9-154">administración de Project: Asignación de tareas y estado de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="d42d9-154">Project management: Assigning tasks and tracking status.</span></span>
* <span data-ttu-id="d42d9-155">Lluvia de ideas: Adición de ideas en diferentes categorías.</span><span class="sxs-lookup"><span data-stu-id="d42d9-155">Brainstorming: Adding ideas in different categories.</span></span>
* <span data-ttu-id="d42d9-156">Ejercicios de clasificación: Organización de cualquier tipo de información en cubos.</span><span class="sxs-lookup"><span data-stu-id="d42d9-156">Sorting exercises: Organizing any kind of information into buckets.</span></span>

## <a name="data-visualization"></a><span data-ttu-id="d42d9-157">Visualización de datos</span><span class="sxs-lookup"><span data-stu-id="d42d9-157">Data visualization</span></span>

<span data-ttu-id="d42d9-158">Puede utilizar diferentes tamaños de tarjeta (único, doble y completo) para apilar y organizar visualizaciones de datos en la misma página.</span><span class="sxs-lookup"><span data-stu-id="d42d9-158">You can use different card sizes (single, double, and full) to stack and organize data visualizations on the same page.</span></span> <span data-ttu-id="d42d9-159">Las tarjetas se escalan para ajustarse al diseño de columna y rellenar espacios en blanco.</span><span class="sxs-lookup"><span data-stu-id="d42d9-159">The cards scale to fit the column layout and fill in blank spaces.</span></span>

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de visualización de datos." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="d42d9-161">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="d42d9-161">Top use cases</span></span>

* <span data-ttu-id="d42d9-162">Mostrar información compleja</span><span class="sxs-lookup"><span data-stu-id="d42d9-162">Display complex information</span></span>
* <span data-ttu-id="d42d9-163">Crear un panel</span><span class="sxs-lookup"><span data-stu-id="d42d9-163">Create a dashboard</span></span>

## <a name="wizard"></a><span data-ttu-id="d42d9-164">Asistente</span><span class="sxs-lookup"><span data-stu-id="d42d9-164">Wizard</span></span>

<span data-ttu-id="d42d9-165">Un asistente guía a un usuario a través de varias pantallas para completar una tarea (como un proceso de configuración).</span><span class="sxs-lookup"><span data-stu-id="d42d9-165">A wizard guides a user through several screens to complete a task (such as a setup process).</span></span>

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario del asistente." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="d42d9-167">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="d42d9-167">Top use cases</span></span>

* <span data-ttu-id="d42d9-168">Instalación</span><span class="sxs-lookup"><span data-stu-id="d42d9-168">Setup</span></span>
* <span data-ttu-id="d42d9-169">Incorporación</span><span class="sxs-lookup"><span data-stu-id="d42d9-169">Onboarding</span></span>
* <span data-ttu-id="d42d9-170">Experiencias de primer año</span><span class="sxs-lookup"><span data-stu-id="d42d9-170">First-run experiences</span></span>

## <a name="empty-state"></a><span data-ttu-id="d42d9-171">Estado vacío</span><span class="sxs-lookup"><span data-stu-id="d42d9-171">Empty state</span></span>

<span data-ttu-id="d42d9-172">La plantilla de estado vacía se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.</span><span class="sxs-lookup"><span data-stu-id="d42d9-172">The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span> <span data-ttu-id="d42d9-173">Es altamente flexible: adáptalo para usar uno, unos pocos o todos los componentes del siguiente diseño.</span><span class="sxs-lookup"><span data-stu-id="d42d9-173">It’s highly flexible⁠—adapt it to use one, a few, or all of the components in the following design.</span></span>

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de estado vacía." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="d42d9-175">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="d42d9-175">Top use cases</span></span>

* <span data-ttu-id="d42d9-176">Iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="d42d9-176">Sign in</span></span>
* <span data-ttu-id="d42d9-177">Mensajes de bienvenida y experiencias de primera ejecución</span><span class="sxs-lookup"><span data-stu-id="d42d9-177">Welcome messages and first-run experiences</span></span>
* <span data-ttu-id="d42d9-178">Mensajes de éxito</span><span class="sxs-lookup"><span data-stu-id="d42d9-178">Success messages</span></span>
* <span data-ttu-id="d42d9-179">Mensajes de error</span><span class="sxs-lookup"><span data-stu-id="d42d9-179">Error messages</span></span>

## <a name="notification-bar"></a><span data-ttu-id="d42d9-180">Barra de notificaciones</span><span class="sxs-lookup"><span data-stu-id="d42d9-180">Notification bar</span></span>

<span data-ttu-id="d42d9-181">Una barra de notificaciones es un área dedicada para mostrar un breve e importante mensaje que no requiere que el usuario tome medidas inmediatas.</span><span class="sxs-lookup"><span data-stu-id="d42d9-181">A notification bar is a dedicated area for displaying a brief, important messages that do not require the user to take immediate action.</span></span> <span data-ttu-id="d42d9-182">Los colores e iconos de fondo específicos están asociados con tipos específicos de mensajes (véase más adelante).</span><span class="sxs-lookup"><span data-stu-id="d42d9-182">Specific background colors and icons are associated with specific types of messages (see below).</span></span>

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="En el ejemplo se muestran plantillas de barra de notificaciones." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="d42d9-184">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="d42d9-184">Top use cases</span></span>

* <span data-ttu-id="d42d9-185">Mensajes críticos, errores y advertencias</span><span class="sxs-lookup"><span data-stu-id="d42d9-185">Critical messages, errors, and warnings</span></span>
* <span data-ttu-id="d42d9-186">Mensajes de éxito</span><span class="sxs-lookup"><span data-stu-id="d42d9-186">Success messages</span></span>
* <span data-ttu-id="d42d9-187">Mensajes informativos o promocionales</span><span class="sxs-lookup"><span data-stu-id="d42d9-187">Informational or promotional messages</span></span>

## <a name="left-nav"></a><span data-ttu-id="d42d9-188">Nav izquierdo</span><span class="sxs-lookup"><span data-stu-id="d42d9-188">Left nav</span></span>

<span data-ttu-id="d42d9-189">Utilice el navegador izquierdo para examinar varias páginas dentro de la pestaña Teams. En el ejemplo siguiente, el navegador izquierdo está entre la lista de canales y el contenido de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="d42d9-189">Use the left nav to browse multiple pages within your Teams tab. In the following example, the left nav is between the channel list and tab content.</span></span>

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="El ejemplo muestra una plantilla de navegación izquierda." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="d42d9-191">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="d42d9-191">Top use cases</span></span>

* <span data-ttu-id="d42d9-192">Examine varias páginas dentro de una pestaña de Teams.</span><span class="sxs-lookup"><span data-stu-id="d42d9-192">Browse multiple pages within a Teams tab.</span></span>
* <span data-ttu-id="d42d9-193">Descompone aplicaciones complejas en varias páginas.</span><span class="sxs-lookup"><span data-stu-id="d42d9-193">Break down complex apps into multiple pages.</span></span>

## <a name="breadcrumb"></a><span data-ttu-id="d42d9-194">Ruta de navegación</span><span class="sxs-lookup"><span data-stu-id="d42d9-194">Breadcrumb</span></span>

<span data-ttu-id="d42d9-195">Las rutas de navegación son una ayuda de navegación que transmite la jerarquía de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d42d9-195">Breadcrumbs are a navigational aid that convey your app’s hierarchy.</span></span> <span data-ttu-id="d42d9-196">Ayudan a los usuarios a entender cómo la página que están viendo encaja en la experiencia general y ofrecen acceso con un solo clic a niveles más altos en esa jerarquía.</span><span class="sxs-lookup"><span data-stu-id="d42d9-196">They help users understand how the page they’re viewing fits into the overall experience and afford one-click access to higher levels in that hierarchy.</span></span>

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="En el ejemplo se muestra una plantilla de ruta de navegación." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="d42d9-198">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="d42d9-198">Top use cases</span></span>

* <span data-ttu-id="d42d9-199">Comunicar jerarquía</span><span class="sxs-lookup"><span data-stu-id="d42d9-199">Communicate hierarchy</span></span>
* <span data-ttu-id="d42d9-200">Navegación</span><span class="sxs-lookup"><span data-stu-id="d42d9-200">Navigation</span></span>

## <a name="toolbar"></a><span data-ttu-id="d42d9-201">Barra de herramientas</span><span class="sxs-lookup"><span data-stu-id="d42d9-201">Toolbar</span></span>

<span data-ttu-id="d42d9-202">Una barra de herramientas es un contenedor para agrupar un conjunto de controles.</span><span class="sxs-lookup"><span data-stu-id="d42d9-202">A toolbar is a container for grouping a set of controls.</span></span>

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="En el ejemplo se muestra una plantilla de barra de herramientas." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="d42d9-204">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="d42d9-204">Top use cases</span></span>

* <span data-ttu-id="d42d9-205">Acciones contextuales sobre el contenido de la aplicación</span><span class="sxs-lookup"><span data-stu-id="d42d9-205">Contextual actions on app content</span></span>
* <span data-ttu-id="d42d9-206">Filtro contextual y hallazgo</span><span class="sxs-lookup"><span data-stu-id="d42d9-206">Contextual filter and find</span></span>
* <span data-ttu-id="d42d9-207">Navegación y migas de pan</span><span class="sxs-lookup"><span data-stu-id="d42d9-207">Navigation and breadcrumbs</span></span>

## <a name="stage"></a><span data-ttu-id="d42d9-208">Etapa</span><span class="sxs-lookup"><span data-stu-id="d42d9-208">Stage</span></span>

<span data-ttu-id="d42d9-209">Stage ofrece una forma para que los usuarios abran una entidad, como una imagen, un archivo o un sitio web, en Teams en lugar de abrirla en otra aplicación o navegador.</span><span class="sxs-lookup"><span data-stu-id="d42d9-209">Stage offers a way for users to open an entity—like an image, file, or website—in Teams instead of opening it in another app or browser.</span></span> <span data-ttu-id="d42d9-210">El principal caso de uso de la etapa es la visualización; la superficie no debe utilizarse para interacciones complejas.</span><span class="sxs-lookup"><span data-stu-id="d42d9-210">The primary use case of stage is viewing; the surface should not be used for complex interactions.</span></span>

<span data-ttu-id="d42d9-211">(Nota de implementación: compile el escenario utilizando un [módulo de tareas](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)grande .)</span><span class="sxs-lookup"><span data-stu-id="d42d9-211">(Implementation note: Build your stage using a large [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).)</span></span>

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="En el ejemplo se muestra una plantilla de etapa." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="d42d9-213">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="d42d9-213">Top use cases</span></span>

* <span data-ttu-id="d42d9-214">Abra una entidad en Teams en lugar de otra aplicación o explorador.</span><span class="sxs-lookup"><span data-stu-id="d42d9-214">Open an entity in Teams instead of another app or browser.</span></span>
* <span data-ttu-id="d42d9-215">Medios destacados u otro contenido.</span><span class="sxs-lookup"><span data-stu-id="d42d9-215">Spotlight media or other content.</span></span>

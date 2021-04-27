---
title: Diseño de la aplicación con plantillas de interfaz de usuario
author: heath-hamilton
description: Diseña tu aplicación más rápido con componentes de interfaz de usuario estandarizados, diseños y patrones que se ven habitualmente en Microsoft Teams.
ms.author: lajanuar
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: d627ce3b29ffa071d0d7e238c572c7cb69fa4cd9
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020768"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a><span data-ttu-id="e5c07-103">Diseño de la aplicación de Microsoft Teams con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="e5c07-103">Designing your Microsoft Teams app with UI templates</span></span>

<span data-ttu-id="e5c07-104">Diseña tu aplicación de Microsoft Teams más rápido con plantillas de interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="e5c07-104">Design your Microsoft Teams app faster with UI templates.</span></span> <span data-ttu-id="e5c07-105">Las plantillas son una colección de componentes basados en fluent ui que funcionan en casos de uso comunes de Teams, lo que te da más tiempo para averiguar la mejor experiencia para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="e5c07-105">The templates are a collection of Fluent UI-based components that work across common Teams use cases, giving you more time to figure out the best experience for your users.</span></span>

## <a name="getting-started-with-tools-and-samples"></a><span data-ttu-id="e5c07-106">Introducción a herramientas y ejemplos</span><span class="sxs-lookup"><span data-stu-id="e5c07-106">Getting started with tools and samples</span></span>

<span data-ttu-id="e5c07-107">Los siguientes recursos pueden ayudarte a diseñar y desarrollar tu aplicación con plantillas de interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="e5c07-107">The following resources can help you design and develop your app using UI templates.</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="e5c07-108">Kit de UI de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e5c07-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="e5c07-109">Toma plantillas de interfaz de usuario para el diseño de la aplicación desde el Kit de interfaz de usuario de Microsoft Teams, que también incluye información extensa sobre el uso, la anatomía, la accesibilidad y los procedimientos recomendados.</span><span class="sxs-lookup"><span data-stu-id="e5c07-109">Grab UI templates for your app design from the Microsoft Teams UI Kit, which also includes extensive information about usage, anatomy, accessibility, and best practices.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e5c07-110">Obtener el kit de interfaz de usuario (Figma)</span><span class="sxs-lookup"><span data-stu-id="e5c07-110">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="e5c07-111">Biblioteca de interfaz de usuario de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e5c07-111">Microsoft Teams UI Library</span></span>

<span data-ttu-id="e5c07-112">Ver y probar plantillas de interfaz de usuario individuales de Teams y componentes relacionados en el explorador.</span><span class="sxs-lookup"><span data-stu-id="e5c07-112">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e5c07-113">Pruebe la biblioteca de interfaz de usuario (área de juegos)</span><span class="sxs-lookup"><span data-stu-id="e5c07-113">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="e5c07-114">Importe estas plantillas y componentes relacionados directamente en el proyecto de la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="e5c07-114">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e5c07-115">Obtener la biblioteca de interfaz de usuario (GitHub)</span><span class="sxs-lookup"><span data-stu-id="e5c07-115">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="e5c07-116">Aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e5c07-116">Sample app</span></span>

<span data-ttu-id="e5c07-117">Instala una aplicación de ejemplo para ver cómo se ven y se comportan las plantillas de interfaz de usuario en contextos de Teams.</span><span class="sxs-lookup"><span data-stu-id="e5c07-117">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e5c07-118">Obtener la aplicación de ejemplo (GitHub)</span><span class="sxs-lookup"><span data-stu-id="e5c07-118">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="list"></a><span data-ttu-id="e5c07-119">Lista</span><span class="sxs-lookup"><span data-stu-id="e5c07-119">List</span></span>

<span data-ttu-id="e5c07-120">Puede usar una lista para mostrar elementos relacionados en un formato analizable y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="e5c07-120">You can use a list to display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de lista." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="e5c07-122">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="e5c07-122">Top use cases</span></span>

* <span data-ttu-id="e5c07-123">Mostrar datos</span><span class="sxs-lookup"><span data-stu-id="e5c07-123">Display data</span></span>
* <span data-ttu-id="e5c07-124">Acciones contextuales en el contenido de la aplicación</span><span class="sxs-lookup"><span data-stu-id="e5c07-124">Contextual actions on app content</span></span>

## <a name="dashboard"></a><span data-ttu-id="e5c07-125">Panel</span><span class="sxs-lookup"><span data-stu-id="e5c07-125">Dashboard</span></span>

<span data-ttu-id="e5c07-126">Un panel muestra diferentes tipos de contenido en una ubicación central (pestaña o aplicación personal de Teams).</span><span class="sxs-lookup"><span data-stu-id="e5c07-126">A dashboard displays different types of content in a central location (Teams personal app or tab).</span></span> <span data-ttu-id="e5c07-127">Los usuarios deben poder personalizar al menos parte de lo que ven en un panel.</span><span class="sxs-lookup"><span data-stu-id="e5c07-127">Users should be able to customize at least some of what they see on a dashboard.</span></span>

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de panel." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="e5c07-129">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="e5c07-129">Top use cases</span></span>

* <span data-ttu-id="e5c07-130">Analizar datos</span><span class="sxs-lookup"><span data-stu-id="e5c07-130">Analyze data</span></span>
* <span data-ttu-id="e5c07-131">Métricas de informes</span><span class="sxs-lookup"><span data-stu-id="e5c07-131">Report metrics</span></span>
* <span data-ttu-id="e5c07-132">Organizar información diferente en un solo lugar</span><span class="sxs-lookup"><span data-stu-id="e5c07-132">Organize different information in one place</span></span>

## <a name="form"></a><span data-ttu-id="e5c07-133">Form</span><span class="sxs-lookup"><span data-stu-id="e5c07-133">Form</span></span>

<span data-ttu-id="e5c07-134">Los formularios se usan para recopilar, validar y enviar la entrada del usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="e5c07-134">Forms are used to collect, validate, and submit user input in a structured way.</span></span> <span data-ttu-id="e5c07-135">El etiquetado claro y las agrupaciones lógicas de campos de entrada son fundamentales para una buena experiencia del usuario.</span><span class="sxs-lookup"><span data-stu-id="e5c07-135">Clear labeling and logical groupings of input fields are critical for a good user experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de formulario." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="e5c07-137">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="e5c07-137">Top use cases</span></span>

* <span data-ttu-id="e5c07-138">Iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="e5c07-138">Sign in</span></span>
* <span data-ttu-id="e5c07-139">Perfiles de usuario</span><span class="sxs-lookup"><span data-stu-id="e5c07-139">User profiles</span></span>
* <span data-ttu-id="e5c07-140">Configuraciones</span><span class="sxs-lookup"><span data-stu-id="e5c07-140">Settings</span></span>
* <span data-ttu-id="e5c07-141">Colección de entrada de usuario</span><span class="sxs-lookup"><span data-stu-id="e5c07-141">User input collection</span></span>

## <a name="sign-in"></a><span data-ttu-id="e5c07-142">Iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="e5c07-142">Sign in</span></span>

<span data-ttu-id="e5c07-143">Puedes diseñar flujos de inicio de sesión de aplicaciones para diferentes contextos de Teams y proveedores de identidades.</span><span class="sxs-lookup"><span data-stu-id="e5c07-143">You can design app sign-in flows for different Teams contexts and identity providers.</span></span> <span data-ttu-id="e5c07-144">En el ejemplo siguiente se incluye el inicio de sesión único (SSO), que se recomienda para la experiencia de autenticación más sencilla.</span><span class="sxs-lookup"><span data-stu-id="e5c07-144">The following example includes single sign-on (SSO), which we recommend for the simplest authentication experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de inicio de sesión." border="false":::

### <a name="top-use-case"></a><span data-ttu-id="e5c07-146">Caso de uso superior</span><span class="sxs-lookup"><span data-stu-id="e5c07-146">Top use case</span></span>

* <span data-ttu-id="e5c07-147">Autenticar usuarios</span><span class="sxs-lookup"><span data-stu-id="e5c07-147">Authenticate users</span></span>

## <a name="task-board"></a><span data-ttu-id="e5c07-148">Panel de tareas</span><span class="sxs-lookup"><span data-stu-id="e5c07-148">Task board</span></span>

<span data-ttu-id="e5c07-149">Un panel de tareas, a veces denominado tablero de kanban o carriles de natación, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o los vales.</span><span class="sxs-lookup"><span data-stu-id="e5c07-149">A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span> <span data-ttu-id="e5c07-150">También se puede usar para ordenar cualquier tipo de contenido en categorías.</span><span class="sxs-lookup"><span data-stu-id="e5c07-150">It can also be used to sort any type of content into categories.</span></span> <span data-ttu-id="e5c07-151">Puede editar y mover las tarjetas entre columnas.</span><span class="sxs-lookup"><span data-stu-id="e5c07-151">You can edit and move the cards between columns.</span></span>

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario del panel de tareas." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="e5c07-153">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="e5c07-153">Top use cases</span></span>

* <span data-ttu-id="e5c07-154">Administración de proyectos.</span><span class="sxs-lookup"><span data-stu-id="e5c07-154">Project management.</span></span> <span data-ttu-id="e5c07-155">Asignación de tareas y estado de seguimiento</span><span class="sxs-lookup"><span data-stu-id="e5c07-155">Assigning tasks and tracking status</span></span>
* <span data-ttu-id="e5c07-156">Lluvia de ideas.</span><span class="sxs-lookup"><span data-stu-id="e5c07-156">Brainstorming.</span></span> <span data-ttu-id="e5c07-157">Agregar ideas en distintas categorías</span><span class="sxs-lookup"><span data-stu-id="e5c07-157">Adding ideas in different categories</span></span>
* <span data-ttu-id="e5c07-158">Ordenar ejercicios.</span><span class="sxs-lookup"><span data-stu-id="e5c07-158">Sorting exercises.</span></span> <span data-ttu-id="e5c07-159">Organizar cualquier tipo de información en cubos</span><span class="sxs-lookup"><span data-stu-id="e5c07-159">Organizing any kind of information into buckets</span></span>

## <a name="data-visualization"></a><span data-ttu-id="e5c07-160">Visualización de datos</span><span class="sxs-lookup"><span data-stu-id="e5c07-160">Data visualization</span></span>

<span data-ttu-id="e5c07-161">Puede usar diferentes tamaños de tarjeta (single, double y full) para apilar y organizar visualizaciones de datos en la misma página.</span><span class="sxs-lookup"><span data-stu-id="e5c07-161">You can use different card sizes (single, double, and full) to stack and organize data visualizations on the same page.</span></span> <span data-ttu-id="e5c07-162">Las tarjetas se escalan para ajustarse al diseño de columna y rellenar espacios en blanco.</span><span class="sxs-lookup"><span data-stu-id="e5c07-162">The cards scale to fit the column layout and fill in blank spaces.</span></span>

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de visualización de datos." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="e5c07-164">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="e5c07-164">Top use cases</span></span>

* <span data-ttu-id="e5c07-165">Mostrar información compleja</span><span class="sxs-lookup"><span data-stu-id="e5c07-165">Display complex information</span></span>
* <span data-ttu-id="e5c07-166">Crear un panel</span><span class="sxs-lookup"><span data-stu-id="e5c07-166">Create a dashboard</span></span>

## <a name="wizard"></a><span data-ttu-id="e5c07-167">Asistente</span><span class="sxs-lookup"><span data-stu-id="e5c07-167">Wizard</span></span>

<span data-ttu-id="e5c07-168">Un asistente guía a un usuario a través de varias pantallas para completar una tarea (como un proceso de instalación).</span><span class="sxs-lookup"><span data-stu-id="e5c07-168">A wizard guides a user through several screens to complete a task (such as a setup process).</span></span>

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de asistente." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="e5c07-170">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="e5c07-170">Top use cases</span></span>

* <span data-ttu-id="e5c07-171">Instalación</span><span class="sxs-lookup"><span data-stu-id="e5c07-171">Setup</span></span>
* <span data-ttu-id="e5c07-172">Incorporación</span><span class="sxs-lookup"><span data-stu-id="e5c07-172">Onboarding</span></span>
* <span data-ttu-id="e5c07-173">Experiencias de primera ejecución</span><span class="sxs-lookup"><span data-stu-id="e5c07-173">First-run experiences</span></span>

## <a name="empty-state"></a><span data-ttu-id="e5c07-174">Estado vacío</span><span class="sxs-lookup"><span data-stu-id="e5c07-174">Empty state</span></span>

<span data-ttu-id="e5c07-175">La plantilla de estado vacío se puede usar para muchos escenarios, como inicio de sesión, experiencias de primera ejecución, mensajes de error y mucho más.</span><span class="sxs-lookup"><span data-stu-id="e5c07-175">The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span> <span data-ttu-id="e5c07-176">Es muy flexible: adaptá para usar uno, unos pocos o todos los componentes del siguiente diseño.</span><span class="sxs-lookup"><span data-stu-id="e5c07-176">It’s highly flexible⁠—adapt it to use one, a few, or all of the components in the following design.</span></span>

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de estado vacía." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="e5c07-178">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="e5c07-178">Top use cases</span></span>

* <span data-ttu-id="e5c07-179">Iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="e5c07-179">Sign in</span></span>
* <span data-ttu-id="e5c07-180">Mensajes de bienvenida y experiencias de primera ejecución</span><span class="sxs-lookup"><span data-stu-id="e5c07-180">Welcome messages and first-run experiences</span></span>
* <span data-ttu-id="e5c07-181">Mensajes de éxito</span><span class="sxs-lookup"><span data-stu-id="e5c07-181">Success messages</span></span>
* <span data-ttu-id="e5c07-182">Mensajes de error</span><span class="sxs-lookup"><span data-stu-id="e5c07-182">Error messages</span></span>

## <a name="notification-bar"></a><span data-ttu-id="e5c07-183">Barra de notificaciones</span><span class="sxs-lookup"><span data-stu-id="e5c07-183">Notification bar</span></span>

<span data-ttu-id="e5c07-184">Una barra de notificaciones es un área dedicada para mostrar mensajes breves e importantes que no requieren que el usuario tome medidas inmediatas.</span><span class="sxs-lookup"><span data-stu-id="e5c07-184">A notification bar is a dedicated area for displaying a brief, important messages that do not require the user to take immediate action.</span></span> <span data-ttu-id="e5c07-185">Los iconos y los colores de fondo específicos están asociados con tipos específicos de mensajes (vea a continuación).</span><span class="sxs-lookup"><span data-stu-id="e5c07-185">Specific background colors and icons are associated with specific types of messages (see below).</span></span>

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="En el ejemplo se muestran las plantillas de la barra de notificaciones." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="e5c07-187">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="e5c07-187">Top use cases</span></span>

* <span data-ttu-id="e5c07-188">Mensajes críticos, errores y advertencias</span><span class="sxs-lookup"><span data-stu-id="e5c07-188">Critical messages, errors, and warnings</span></span>
* <span data-ttu-id="e5c07-189">Mensajes de éxito</span><span class="sxs-lookup"><span data-stu-id="e5c07-189">Success messages</span></span>
* <span data-ttu-id="e5c07-190">Mensajes informativos o promocionales</span><span class="sxs-lookup"><span data-stu-id="e5c07-190">Informational or promotional messages</span></span>

## <a name="left-nav"></a><span data-ttu-id="e5c07-191">Navegación izquierda</span><span class="sxs-lookup"><span data-stu-id="e5c07-191">Left nav</span></span>

<span data-ttu-id="e5c07-192">Use la navegación izquierda para examinar varias páginas dentro de la pestaña Teams. En el siguiente ejemplo, la navegación izquierda se encuentra entre la lista de canales y el contenido de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="e5c07-192">Use the left nav to browse multiple pages within your Teams tab. In the following example, the left nav is between the channel list and tab content.</span></span>

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="En el ejemplo se muestra una plantilla de navegación izquierda." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="e5c07-194">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="e5c07-194">Top use cases</span></span>

* <span data-ttu-id="e5c07-195">Examinar varias páginas dentro de una pestaña de Teams</span><span class="sxs-lookup"><span data-stu-id="e5c07-195">Browse multiple pages within a Teams tab</span></span>
* <span data-ttu-id="e5c07-196">Dividir aplicaciones complejas en varias páginas</span><span class="sxs-lookup"><span data-stu-id="e5c07-196">Break down complex apps into multiple pages</span></span>

## <a name="breadcrumb"></a><span data-ttu-id="e5c07-197">Ruta de navegación</span><span class="sxs-lookup"><span data-stu-id="e5c07-197">Breadcrumb</span></span>

<span data-ttu-id="e5c07-198">Las rutas de navegación son una ayuda de navegación que transmite la jerarquía de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e5c07-198">Breadcrumbs are a navigational aid that convey your app’s hierarchy.</span></span> <span data-ttu-id="e5c07-199">Ayudan a los usuarios a comprender cómo la página que están viendo se ajusta a la experiencia general y ofrecen acceso con un solo clic a niveles más altos de esa jerarquía.</span><span class="sxs-lookup"><span data-stu-id="e5c07-199">They help users understand how the page they’re viewing fits into the overall experience and afford one-click access to higher levels in that hierarchy.</span></span>

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="En el ejemplo se muestra una plantilla de ruta de navegación." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="e5c07-201">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="e5c07-201">Top use cases</span></span>

* <span data-ttu-id="e5c07-202">Jerarquía de comunicación</span><span class="sxs-lookup"><span data-stu-id="e5c07-202">Communicate hierarchy</span></span>
* <span data-ttu-id="e5c07-203">Navegación</span><span class="sxs-lookup"><span data-stu-id="e5c07-203">Navigation</span></span>

## <a name="toolbar"></a><span data-ttu-id="e5c07-204">Barra de herramientas</span><span class="sxs-lookup"><span data-stu-id="e5c07-204">Toolbar</span></span>

<span data-ttu-id="e5c07-205">Una barra de herramientas es un contenedor para agrupar un conjunto de controles.</span><span class="sxs-lookup"><span data-stu-id="e5c07-205">A toolbar is a container for grouping a set of controls.</span></span>

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="En el ejemplo se muestra una plantilla de barra de herramientas." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="e5c07-207">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="e5c07-207">Top use cases</span></span>

* <span data-ttu-id="e5c07-208">Acciones contextuales en el contenido de la aplicación</span><span class="sxs-lookup"><span data-stu-id="e5c07-208">Contextual actions on app content</span></span>
* <span data-ttu-id="e5c07-209">Filtro contextual y búsqueda</span><span class="sxs-lookup"><span data-stu-id="e5c07-209">Contextual filter and find</span></span>
* <span data-ttu-id="e5c07-210">Navegación y rutas de navegación</span><span class="sxs-lookup"><span data-stu-id="e5c07-210">Navigation and breadcrumbs</span></span>

## <a name="stage"></a><span data-ttu-id="e5c07-211">Etapa</span><span class="sxs-lookup"><span data-stu-id="e5c07-211">Stage</span></span>

<span data-ttu-id="e5c07-212">Stage ofrece una forma de que los usuarios abran una entidad (como una imagen, un archivo o un sitio web) en Teams en lugar de abrirlo en otra aplicación o explorador.</span><span class="sxs-lookup"><span data-stu-id="e5c07-212">Stage offers a way for users to open an entity—like an image, file, or website—in Teams instead of opening it in another app or browser.</span></span> <span data-ttu-id="e5c07-213">El caso de uso principal de la fase es la visualización; la superficie no debe usarse para interacciones complejas.</span><span class="sxs-lookup"><span data-stu-id="e5c07-213">The primary use case of stage is viewing; the surface should not be used for complex interactions.</span></span>

<span data-ttu-id="e5c07-214">(Nota de implementación: cree la fase con un módulo [de tareas grande](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).)</span><span class="sxs-lookup"><span data-stu-id="e5c07-214">(Implementation note: Build your stage using a large [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).)</span></span>

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="En el ejemplo se muestra una plantilla de fase." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="e5c07-216">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="e5c07-216">Top use cases</span></span>

* <span data-ttu-id="e5c07-217">Abrir una entidad en Teams en lugar de otra aplicación o explorador</span><span class="sxs-lookup"><span data-stu-id="e5c07-217">Open an entity in Teams instead of another app or browser</span></span>
* <span data-ttu-id="e5c07-218">Contenido multimedia destacado u otro contenido</span><span class="sxs-lookup"><span data-stu-id="e5c07-218">Spotlight media or other content</span></span>

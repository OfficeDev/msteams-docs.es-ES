---
title: Diseñar la aplicación con plantillas de interfaz de usuario
author: heath-hamilton
description: Diseñe su aplicación con mayor rapidez con componentes, diseños y patrones estandarizados de la interfaz de usuario que se ven habitualmente en Microsoft Teams.
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: b4d244bbf78ac85042d5caf8ec84afe42e79b3c7
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911929"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a><span data-ttu-id="1561f-103">Diseño de la aplicación de Microsoft Teams con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="1561f-103">Designing your Microsoft Teams app with UI templates</span></span>

<span data-ttu-id="1561f-104">Diseñe su aplicación de Microsoft Teams más rápido con plantillas de interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="1561f-104">Design your Microsoft Teams app faster with UI templates.</span></span> <span data-ttu-id="1561f-105">Las plantillas son una colección de componentes basados en la interfaz de usuario fluent que funcionan en casos de uso comunes de Teams, lo que le da más tiempo para averiguar la mejor experiencia para sus usuarios.</span><span class="sxs-lookup"><span data-stu-id="1561f-105">The templates are a collection of Fluent UI-based components that work across common Teams use cases, giving you more time to figure out the best experience for your users.</span></span>

## <a name="getting-started-with-tools-and-samples"></a><span data-ttu-id="1561f-106">Introducción a herramientas y ejemplos</span><span class="sxs-lookup"><span data-stu-id="1561f-106">Getting started with tools and samples</span></span>

<span data-ttu-id="1561f-107">Los siguientes recursos pueden ayudarte a diseñar y desarrollar tu aplicación mediante plantillas de interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="1561f-107">The following resources can help you design and develop your app using UI templates.</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="1561f-108">Kit de interfaz de usuario de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1561f-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="1561f-109">Obtener plantillas de interfaz de usuario para el diseño de la aplicación desde el Kit de interfaz de usuario de Microsoft Teams, que también incluye amplia información sobre el uso, anatomía, accesibilidad y procedimientos recomendados.</span><span class="sxs-lookup"><span data-stu-id="1561f-109">Grab UI templates for your app design from the Microsoft Teams UI Kit, which also includes extensive information about usage, anatomy, accessibility, and best practices.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1561f-110">Obtener el kit de interfaz de usuario (Figma)</span><span class="sxs-lookup"><span data-stu-id="1561f-110">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="1561f-111">Biblioteca de interfaz de usuario de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1561f-111">Microsoft Teams UI Library</span></span>

<span data-ttu-id="1561f-112">Ver y probar plantillas individuales de la interfaz de usuario de Teams y componentes relacionados en el explorador.</span><span class="sxs-lookup"><span data-stu-id="1561f-112">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1561f-113">Probar la biblioteca de la interfaz de usuario (área de prueba)</span><span class="sxs-lookup"><span data-stu-id="1561f-113">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="1561f-114">Importe estas plantillas y componentes relacionados directamente en su proyecto de aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="1561f-114">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1561f-115">Obtener la biblioteca de interfaz de usuario (GitHub)</span><span class="sxs-lookup"><span data-stu-id="1561f-115">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="1561f-116">Aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1561f-116">Sample app</span></span>

<span data-ttu-id="1561f-117">Instale una aplicación de ejemplo para ver el aspecto y el comportamiento de las plantillas de interfaz de usuario en los contextos de Teams.</span><span class="sxs-lookup"><span data-stu-id="1561f-117">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1561f-118">Obtener la aplicación de ejemplo (GitHub)</span><span class="sxs-lookup"><span data-stu-id="1561f-118">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="list"></a><span data-ttu-id="1561f-119">Lista</span><span class="sxs-lookup"><span data-stu-id="1561f-119">List</span></span>

<span data-ttu-id="1561f-120">Puede usar una lista para mostrar elementos relacionados en un formato que se pueda examinar y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="1561f-120">You can use a list to display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de lista." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="1561f-122">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="1561f-122">Top use cases</span></span>

* <span data-ttu-id="1561f-123">Mostrar datos</span><span class="sxs-lookup"><span data-stu-id="1561f-123">Display data</span></span>
* <span data-ttu-id="1561f-124">Acciones contextuales en el contenido de la aplicación</span><span class="sxs-lookup"><span data-stu-id="1561f-124">Contextual actions on app content</span></span>

## <a name="dashboard"></a><span data-ttu-id="1561f-125">Panel</span><span class="sxs-lookup"><span data-stu-id="1561f-125">Dashboard</span></span>

<span data-ttu-id="1561f-126">Un panel muestra diferentes tipos de contenido en una ubicación central (pestaña o aplicación personal de Teams).</span><span class="sxs-lookup"><span data-stu-id="1561f-126">A dashboard displays different types of content in a central location (Teams personal app or tab).</span></span> <span data-ttu-id="1561f-127">Los usuarios deben poder personalizar al menos parte de lo que ven en un panel.</span><span class="sxs-lookup"><span data-stu-id="1561f-127">Users should be able to customize at least some of what they see on a dashboard.</span></span>

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de panel." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="1561f-129">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="1561f-129">Top use cases</span></span>

* <span data-ttu-id="1561f-130">Analizar datos</span><span class="sxs-lookup"><span data-stu-id="1561f-130">Analyze data</span></span>
* <span data-ttu-id="1561f-131">Métricas de informes</span><span class="sxs-lookup"><span data-stu-id="1561f-131">Report metrics</span></span>
* <span data-ttu-id="1561f-132">Organizar información diferente en un solo lugar</span><span class="sxs-lookup"><span data-stu-id="1561f-132">Organize different information in one place</span></span>

## <a name="form"></a><span data-ttu-id="1561f-133">Form</span><span class="sxs-lookup"><span data-stu-id="1561f-133">Form</span></span>

<span data-ttu-id="1561f-134">Los formularios se usan para recopilar, validar y enviar entradas de usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="1561f-134">Forms are used to collect, validate, and submit user input in a structured way.</span></span> <span data-ttu-id="1561f-135">El etiquetado claro y las agrupaciones lógicas de campos de entrada son fundamentales para una buena experiencia del usuario.</span><span class="sxs-lookup"><span data-stu-id="1561f-135">Clear labeling and logical groupings of input fields are critical for a good user experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de formulario." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="1561f-137">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="1561f-137">Top use cases</span></span>

* <span data-ttu-id="1561f-138">Iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="1561f-138">Sign in</span></span>
* <span data-ttu-id="1561f-139">Perfiles de usuario</span><span class="sxs-lookup"><span data-stu-id="1561f-139">User profiles</span></span>
* <span data-ttu-id="1561f-140">Configuración</span><span class="sxs-lookup"><span data-stu-id="1561f-140">Settings</span></span>
* <span data-ttu-id="1561f-141">Colección de entradas de usuario</span><span class="sxs-lookup"><span data-stu-id="1561f-141">User input collection</span></span>

## <a name="sign-in"></a><span data-ttu-id="1561f-142">Iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="1561f-142">Sign in</span></span>

<span data-ttu-id="1561f-143">Puede diseñar flujos de inicio de sesión de aplicaciones para diferentes contextos de Teams y proveedores de identidades.</span><span class="sxs-lookup"><span data-stu-id="1561f-143">You can design app sign-in flows for different Teams contexts and identity providers.</span></span> <span data-ttu-id="1561f-144">En el siguiente ejemplo se incluye el inicio de sesión único (SSO), que se recomienda para la experiencia de autenticación más sencilla.</span><span class="sxs-lookup"><span data-stu-id="1561f-144">The following example includes single sign-on (SSO), which we recommend for the simplest authentication experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de inicio de sesión." border="false":::

### <a name="top-use-case"></a><span data-ttu-id="1561f-146">Caso de uso principal</span><span class="sxs-lookup"><span data-stu-id="1561f-146">Top use case</span></span>

* <span data-ttu-id="1561f-147">Autenticar usuarios</span><span class="sxs-lookup"><span data-stu-id="1561f-147">Authenticate users</span></span>

## <a name="task-board"></a><span data-ttu-id="1561f-148">Panel de tareas</span><span class="sxs-lookup"><span data-stu-id="1561f-148">Task board</span></span>

<span data-ttu-id="1561f-149">Un panel de tareas, a veces denominado tablero de kanban o pistas de nado, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o los vales.</span><span class="sxs-lookup"><span data-stu-id="1561f-149">A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span> <span data-ttu-id="1561f-150">También se puede usar para ordenar cualquier tipo de contenido en categorías.</span><span class="sxs-lookup"><span data-stu-id="1561f-150">It can also be used to sort any type of content into categories.</span></span> <span data-ttu-id="1561f-151">Puede editar y mover las tarjetas entre columnas.</span><span class="sxs-lookup"><span data-stu-id="1561f-151">You can edit and move the cards between columns.</span></span>

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario del panel de tareas." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="1561f-153">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="1561f-153">Top use cases</span></span>

* <span data-ttu-id="1561f-154">Administración de proyectos.</span><span class="sxs-lookup"><span data-stu-id="1561f-154">Project management.</span></span> <span data-ttu-id="1561f-155">Asignación de tareas y estado de seguimiento</span><span class="sxs-lookup"><span data-stu-id="1561f-155">Assigning tasks and tracking status</span></span>
* <span data-ttu-id="1561f-156">Lluvia de ideas.</span><span class="sxs-lookup"><span data-stu-id="1561f-156">Brainstorming.</span></span> <span data-ttu-id="1561f-157">Agregar ideas en distintas categorías</span><span class="sxs-lookup"><span data-stu-id="1561f-157">Adding ideas in different categories</span></span>
* <span data-ttu-id="1561f-158">Ejercicios de ordenación.</span><span class="sxs-lookup"><span data-stu-id="1561f-158">Sorting exercises.</span></span> <span data-ttu-id="1561f-159">Organizar cualquier tipo de información en cubos</span><span class="sxs-lookup"><span data-stu-id="1561f-159">Organizing any kind of information into buckets</span></span>

## <a name="data-visualization"></a><span data-ttu-id="1561f-160">Visualización de datos</span><span class="sxs-lookup"><span data-stu-id="1561f-160">Data visualization</span></span>

<span data-ttu-id="1561f-161">Puede usar distintos tamaños de tarjeta (único, doble y completo) para apilar y organizar visualizaciones de datos en la misma página.</span><span class="sxs-lookup"><span data-stu-id="1561f-161">You can use different card sizes (single, double, and full) to stack and organize data visualizations on the same page.</span></span> <span data-ttu-id="1561f-162">Las tarjetas se escalan para ajustarse al diseño de columna y rellenar espacios en blanco.</span><span class="sxs-lookup"><span data-stu-id="1561f-162">The cards scale to fit the column layout and fill in blank spaces.</span></span>

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de visualización de datos." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="1561f-164">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="1561f-164">Top use cases</span></span>

* <span data-ttu-id="1561f-165">Mostrar información compleja</span><span class="sxs-lookup"><span data-stu-id="1561f-165">Display complex information</span></span>
* <span data-ttu-id="1561f-166">Crear un panel</span><span class="sxs-lookup"><span data-stu-id="1561f-166">Create a dashboard</span></span>

## <a name="wizard"></a><span data-ttu-id="1561f-167">Asistente</span><span class="sxs-lookup"><span data-stu-id="1561f-167">Wizard</span></span>

<span data-ttu-id="1561f-168">Un asistente guía a un usuario a través de varias pantallas para completar una tarea (como un proceso de configuración).</span><span class="sxs-lookup"><span data-stu-id="1561f-168">A wizard guides a user through several screens to complete a task (such as a setup process).</span></span>

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de asistente." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="1561f-170">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="1561f-170">Top use cases</span></span>

* <span data-ttu-id="1561f-171">Instalación</span><span class="sxs-lookup"><span data-stu-id="1561f-171">Setup</span></span>
* <span data-ttu-id="1561f-172">Incorporación</span><span class="sxs-lookup"><span data-stu-id="1561f-172">Onboarding</span></span>
* <span data-ttu-id="1561f-173">Experiencias de primera ejecución</span><span class="sxs-lookup"><span data-stu-id="1561f-173">First-run experiences</span></span>

## <a name="empty-state"></a><span data-ttu-id="1561f-174">Estado vacío</span><span class="sxs-lookup"><span data-stu-id="1561f-174">Empty state</span></span>

<span data-ttu-id="1561f-175">La plantilla de estado vacía se puede usar para muchos escenarios, incluido el inicio de sesión, experiencias de primera ejecución, mensajes de error y mucho más.</span><span class="sxs-lookup"><span data-stu-id="1561f-175">The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span> <span data-ttu-id="1561f-176">Es muy flexible: adaptarlo para usar uno, algunos o todos los componentes del siguiente diseño.</span><span class="sxs-lookup"><span data-stu-id="1561f-176">It’s highly flexible⁠—adapt it to use one, a few, or all of the components in the following design.</span></span>

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de estado vacía." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="1561f-178">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="1561f-178">Top use cases</span></span>

* <span data-ttu-id="1561f-179">Iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="1561f-179">Sign in</span></span>
* <span data-ttu-id="1561f-180">Mensajes de bienvenida y experiencias de primera ejecución</span><span class="sxs-lookup"><span data-stu-id="1561f-180">Welcome messages and first-run experiences</span></span>
* <span data-ttu-id="1561f-181">Mensajes de éxito</span><span class="sxs-lookup"><span data-stu-id="1561f-181">Success messages</span></span>
* <span data-ttu-id="1561f-182">Mensajes de error</span><span class="sxs-lookup"><span data-stu-id="1561f-182">Error messages</span></span>

## <a name="notification-bar"></a><span data-ttu-id="1561f-183">Barra de notificaciones</span><span class="sxs-lookup"><span data-stu-id="1561f-183">Notification bar</span></span>

<span data-ttu-id="1561f-184">Una barra de notificaciones es un área dedicada para mostrar mensajes breves e importantes que no requieren que el usuario realice una acción inmediata.</span><span class="sxs-lookup"><span data-stu-id="1561f-184">A notification bar is a dedicated area for displaying a brief, important messages that do not require the user to take immediate action.</span></span> <span data-ttu-id="1561f-185">Los iconos y los colores de fondo específicos están asociados a tipos específicos de mensajes (consulta a continuación).</span><span class="sxs-lookup"><span data-stu-id="1561f-185">Specific background colors and icons are associated with specific types of messages (see below).</span></span>

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="En el ejemplo se muestran las plantillas de la barra de notificaciones." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="1561f-187">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="1561f-187">Top use cases</span></span>

* <span data-ttu-id="1561f-188">Mensajes críticos, errores y advertencias</span><span class="sxs-lookup"><span data-stu-id="1561f-188">Critical messages, errors, and warnings</span></span>
* <span data-ttu-id="1561f-189">Mensajes de éxito</span><span class="sxs-lookup"><span data-stu-id="1561f-189">Success messages</span></span>
* <span data-ttu-id="1561f-190">Mensajes informativos o promocionales</span><span class="sxs-lookup"><span data-stu-id="1561f-190">Informational or promotional messages</span></span>

## <a name="left-nav"></a><span data-ttu-id="1561f-191">Navegación izquierda</span><span class="sxs-lookup"><span data-stu-id="1561f-191">Left nav</span></span>

<span data-ttu-id="1561f-192">Use el panel de navegación izquierdo para examinar varias páginas dentro de la pestaña de Teams. En el siguiente ejemplo, el panel de navegación izquierdo se encuentra entre la lista de canales y el contenido de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="1561f-192">Use the left nav to browse multiple pages within your Teams tab. In the following example, the left nav is between the channel list and tab content.</span></span>

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="En el ejemplo se muestra una plantilla de navegación izquierda." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="1561f-194">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="1561f-194">Top use cases</span></span>

* <span data-ttu-id="1561f-195">Examinar varias páginas en una pestaña de Teams</span><span class="sxs-lookup"><span data-stu-id="1561f-195">Browse multiple pages within a Teams tab</span></span>
* <span data-ttu-id="1561f-196">Dividir aplicaciones complejas en varias páginas</span><span class="sxs-lookup"><span data-stu-id="1561f-196">Break down complex apps into multiple pages</span></span>

## <a name="breadcrumb"></a><span data-ttu-id="1561f-197">Ruta de navegación</span><span class="sxs-lookup"><span data-stu-id="1561f-197">Breadcrumb</span></span>

<span data-ttu-id="1561f-198">Las rutas de navegación son una ayuda de navegación que transmite la jerarquía de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1561f-198">Breadcrumbs are a navigational aid that convey your app’s hierarchy.</span></span> <span data-ttu-id="1561f-199">Ayudan a los usuarios a comprender cómo se ajusta la página que están viendo a la experiencia general y permiten el acceso de un solo clic a niveles superiores de esa jerarquía.</span><span class="sxs-lookup"><span data-stu-id="1561f-199">They help users understand how the page they’re viewing fits into the overall experience and afford one-click access to higher levels in that hierarchy.</span></span>

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="En el ejemplo se muestra una plantilla de ruta de navegación." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="1561f-201">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="1561f-201">Top use cases</span></span>

* <span data-ttu-id="1561f-202">Comunicar jerarquía</span><span class="sxs-lookup"><span data-stu-id="1561f-202">Communicate hierarchy</span></span>
* <span data-ttu-id="1561f-203">Navegación</span><span class="sxs-lookup"><span data-stu-id="1561f-203">Navigation</span></span>

## <a name="toolbar"></a><span data-ttu-id="1561f-204">Barra de herramientas</span><span class="sxs-lookup"><span data-stu-id="1561f-204">Toolbar</span></span>

<span data-ttu-id="1561f-205">Una barra de herramientas es un contenedor para agrupar un conjunto de controles.</span><span class="sxs-lookup"><span data-stu-id="1561f-205">A toolbar is a container for grouping a set of controls.</span></span>

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="En el ejemplo se muestra una plantilla de barra de herramientas." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="1561f-207">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="1561f-207">Top use cases</span></span>

* <span data-ttu-id="1561f-208">Acciones contextuales en el contenido de la aplicación</span><span class="sxs-lookup"><span data-stu-id="1561f-208">Contextual actions on app content</span></span>
* <span data-ttu-id="1561f-209">Filtro contextual y búsqueda</span><span class="sxs-lookup"><span data-stu-id="1561f-209">Contextual filter and find</span></span>
* <span data-ttu-id="1561f-210">Navegación y rutas de navegación</span><span class="sxs-lookup"><span data-stu-id="1561f-210">Navigation and breadcrumbs</span></span>

## <a name="stage"></a><span data-ttu-id="1561f-211">Etapa</span><span class="sxs-lookup"><span data-stu-id="1561f-211">Stage</span></span>

<span data-ttu-id="1561f-212">La fase ofrece a los usuarios una forma de abrir una entidad (como una imagen, un archivo o un sitio web) en Teams en lugar de abrirlo en otra aplicación o explorador.</span><span class="sxs-lookup"><span data-stu-id="1561f-212">Stage offers a way for users to open an entity—like an image, file, or website—in Teams instead of opening it in another app or browser.</span></span> <span data-ttu-id="1561f-213">El caso de uso principal de la fase es la visualización; la superficie no debe usarse para interacciones complejas.</span><span class="sxs-lookup"><span data-stu-id="1561f-213">The primary use case of stage is viewing; the surface should not be used for complex interactions.</span></span>

<span data-ttu-id="1561f-214">(Nota de implementación: cree la fase con un módulo [de tareas de gran tamaño).](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)</span><span class="sxs-lookup"><span data-stu-id="1561f-214">(Implementation note: Build your stage using a large [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).)</span></span>

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="En el ejemplo se muestra una plantilla de fase." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="1561f-216">Principales casos de uso</span><span class="sxs-lookup"><span data-stu-id="1561f-216">Top use cases</span></span>

* <span data-ttu-id="1561f-217">Abrir una entidad en Teams en lugar de otra aplicación o explorador</span><span class="sxs-lookup"><span data-stu-id="1561f-217">Open an entity in Teams instead of another app or browser</span></span>
* <span data-ttu-id="1561f-218">Contenido multimedia destacado u otro contenido</span><span class="sxs-lookup"><span data-stu-id="1561f-218">Spotlight media or other content</span></span>

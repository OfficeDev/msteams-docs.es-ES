---
title: Diseño de la aplicación con plantillas de interfaz de usuario
author: heath-hamilton
description: Diseña tu aplicación más rápido con componentes de interfaz de usuario estandarizados, diseños y patrones que se ven comúnmente en Microsoft Teams.
ms.author: lajanuar
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: 5026554070396dcc55390496b6754961e8e037bc
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644856"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a><span data-ttu-id="2ef9c-103">Diseñar la aplicación Microsoft Teams con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="2ef9c-103">Designing your Microsoft Teams app with UI templates</span></span>

<span data-ttu-id="2ef9c-104">Diseña tu aplicación Microsoft Teams más rápido con plantillas de interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-104">Design your Microsoft Teams app faster with UI templates.</span></span> <span data-ttu-id="2ef9c-105">Las plantillas son una colección de componentes basados en fluent ui que funcionan en casos de uso Teams comunes, lo que te da más tiempo para averiguar la mejor experiencia para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-105">The templates are a collection of Fluent UI-based components that work across common Teams use cases, giving you more time to figure out the best experience for your users.</span></span>

## <a name="getting-started-with-tools-and-samples"></a><span data-ttu-id="2ef9c-106">Introducción a herramientas y ejemplos</span><span class="sxs-lookup"><span data-stu-id="2ef9c-106">Getting started with tools and samples</span></span>

<span data-ttu-id="2ef9c-107">Los siguientes recursos pueden ayudarte a diseñar y desarrollar tu aplicación con plantillas de interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-107">The following resources can help you design and develop your app using UI templates.</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="2ef9c-108">Kit de UI de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="2ef9c-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="2ef9c-109">Toma plantillas de interfaz de usuario para el diseño de la aplicación desde el kit de interfaz de usuario de Microsoft Teams, que también incluye información extensa sobre el uso, la anatomía, la accesibilidad y los procedimientos recomendados.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-109">Grab UI templates for your app design from the Microsoft Teams UI Kit, which also includes extensive information about usage, anatomy, accessibility, and best practices.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2ef9c-110">Obtener el kit de interfaz de usuario (Figma)</span><span class="sxs-lookup"><span data-stu-id="2ef9c-110">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="2ef9c-111">Microsoft Teams Biblioteca de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="2ef9c-111">Microsoft Teams UI Library</span></span>

<span data-ttu-id="2ef9c-112">Ver y probar plantillas de Teams de interfaz de usuario individuales y componentes relacionados en el explorador.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-112">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2ef9c-113">Pruebe la biblioteca de interfaz de usuario (área de juegos)</span><span class="sxs-lookup"><span data-stu-id="2ef9c-113">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="2ef9c-114">Importe estas plantillas y componentes relacionados directamente en el proyecto Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-114">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2ef9c-115">Obtener la biblioteca de interfaz de usuario (GitHub)</span><span class="sxs-lookup"><span data-stu-id="2ef9c-115">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="2ef9c-116">Aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2ef9c-116">Sample app</span></span>

<span data-ttu-id="2ef9c-117">Instala una aplicación de ejemplo para ver cómo se ven y se comportan las plantillas de interfaz de usuario en Teams contextos.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-117">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2ef9c-118">Obtener la aplicación de ejemplo (GitHub)</span><span class="sxs-lookup"><span data-stu-id="2ef9c-118">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="dashboard"></a><span data-ttu-id="2ef9c-119">Panel</span><span class="sxs-lookup"><span data-stu-id="2ef9c-119">Dashboard</span></span>

<span data-ttu-id="2ef9c-120">Un panel muestra diferentes tipos de contenido en una ubicación central (Teams aplicación o pestaña personal).</span><span class="sxs-lookup"><span data-stu-id="2ef9c-120">A dashboard displays different types of content in a central location (Teams personal app or tab).</span></span> <span data-ttu-id="2ef9c-121">Los usuarios deben poder personalizar al menos parte de lo que ven en un panel.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-121">Users should be able to customize at least some of what they see on a dashboard.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="2ef9c-122">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="2ef9c-122">Top use cases</span></span>

* <span data-ttu-id="2ef9c-123">Analizar datos</span><span class="sxs-lookup"><span data-stu-id="2ef9c-123">Analyze data</span></span>
* <span data-ttu-id="2ef9c-124">Métricas de informes</span><span class="sxs-lookup"><span data-stu-id="2ef9c-124">Report metrics</span></span>
* <span data-ttu-id="2ef9c-125">Organizar información diferente en un solo lugar</span><span class="sxs-lookup"><span data-stu-id="2ef9c-125">Organize different information in one place</span></span>

# <a name="desktop"></a>[<span data-ttu-id="2ef9c-126">Escritorio</span><span class="sxs-lookup"><span data-stu-id="2ef9c-126">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de panel en el escritorio." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="2ef9c-128">Móvil</span><span class="sxs-lookup"><span data-stu-id="2ef9c-128">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-dashboard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de panel en el móvil." border="false":::

---

## <a name="data-visualization"></a><span data-ttu-id="2ef9c-130">Visualización de datos</span><span class="sxs-lookup"><span data-stu-id="2ef9c-130">Data visualization</span></span>

<span data-ttu-id="2ef9c-131">Puede usar diferentes tamaños de tarjeta (single, double y full) para apilar y organizar visualizaciones de datos en la misma página.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-131">You can use different card sizes (single, double, and full) to stack and organize data visualizations on the same page.</span></span> <span data-ttu-id="2ef9c-132">Las tarjetas se escalan para ajustarse al diseño de columna y rellenar espacios en blanco.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-132">The cards scale to fit the column layout and fill in blank spaces.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="2ef9c-133">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="2ef9c-133">Top use cases</span></span>

* <span data-ttu-id="2ef9c-134">Mostrar información compleja</span><span class="sxs-lookup"><span data-stu-id="2ef9c-134">Display complex information</span></span>
* <span data-ttu-id="2ef9c-135">Crear un panel</span><span class="sxs-lookup"><span data-stu-id="2ef9c-135">Create a dashboard</span></span>

# <a name="desktop"></a>[<span data-ttu-id="2ef9c-136">Escritorio</span><span class="sxs-lookup"><span data-stu-id="2ef9c-136">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de visualización de datos en el escritorio." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="2ef9c-138">Móvil</span><span class="sxs-lookup"><span data-stu-id="2ef9c-138">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-data-viz.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de visualización de datos en el móvil." border="false":::

---

## <a name="empty-state"></a><span data-ttu-id="2ef9c-140">Estado vacío</span><span class="sxs-lookup"><span data-stu-id="2ef9c-140">Empty state</span></span>

<span data-ttu-id="2ef9c-141">La plantilla de estado vacío se puede usar para muchos escenarios, como inicio de sesión, experiencias de primera ejecución, mensajes de error y mucho más.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-141">The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span> <span data-ttu-id="2ef9c-142">Es muy flexible: adaptá para usar uno, unos pocos o todos los componentes del siguiente diseño.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-142">It’s highly flexible⁠—adapt it to use one, a few, or all of the components in the following design.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="2ef9c-143">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="2ef9c-143">Top use cases</span></span>

* <span data-ttu-id="2ef9c-144">Iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="2ef9c-144">Sign in</span></span>
* <span data-ttu-id="2ef9c-145">Mensajes de bienvenida y experiencias de primera ejecución</span><span class="sxs-lookup"><span data-stu-id="2ef9c-145">Welcome messages and first-run experiences</span></span>
* <span data-ttu-id="2ef9c-146">Mensajes de éxito</span><span class="sxs-lookup"><span data-stu-id="2ef9c-146">Success messages</span></span>
* <span data-ttu-id="2ef9c-147">Mensajes de error</span><span class="sxs-lookup"><span data-stu-id="2ef9c-147">Error messages</span></span>

# <a name="desktop"></a>[<span data-ttu-id="2ef9c-148">Escritorio</span><span class="sxs-lookup"><span data-stu-id="2ef9c-148">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de estado vacía en el escritorio." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="2ef9c-150">Móvil</span><span class="sxs-lookup"><span data-stu-id="2ef9c-150">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-empty-state.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de estado vacía en el móvil." border="false":::

---

## <a name="filter"></a><span data-ttu-id="2ef9c-152">Filtro</span><span class="sxs-lookup"><span data-stu-id="2ef9c-152">Filter</span></span>

<span data-ttu-id="2ef9c-153">Un filtro le permite reducir la información que ve en función de los criterios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-153">A filter allows you to reduce the information you see based on the criteria selected.</span></span> <span data-ttu-id="2ef9c-154">Puede incluir filtros con tablas, listas, tarjetas y otros componentes que organizan el contenido.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-154">You can include filters with tables, lists, cards, and other components that organize content.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="2ef9c-155">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="2ef9c-155">Top use cases</span></span>

<span data-ttu-id="2ef9c-156">Organizar contenido en:</span><span class="sxs-lookup"><span data-stu-id="2ef9c-156">Organizing content in:</span></span>

* <span data-ttu-id="2ef9c-157">Listas</span><span class="sxs-lookup"><span data-stu-id="2ef9c-157">Lists</span></span>
* <span data-ttu-id="2ef9c-158">Tablas</span><span class="sxs-lookup"><span data-stu-id="2ef9c-158">Tables</span></span>
* <span data-ttu-id="2ef9c-159">Paneles</span><span class="sxs-lookup"><span data-stu-id="2ef9c-159">Dashboards</span></span>
* <span data-ttu-id="2ef9c-160">Visualización de datos</span><span class="sxs-lookup"><span data-stu-id="2ef9c-160">Data visualization</span></span>

:::image type="content" source="../../assets/images/ui-templates/filter.png" alt-text="En el ejemplo se muestra una plantilla de filtro." border="false":::

## <a name="form"></a><span data-ttu-id="2ef9c-162">Form</span><span class="sxs-lookup"><span data-stu-id="2ef9c-162">Form</span></span>

<span data-ttu-id="2ef9c-163">Los formularios se usan para recopilar, validar y enviar la entrada del usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-163">Forms are used to collect, validate, and submit user input in a structured way.</span></span> <span data-ttu-id="2ef9c-164">El etiquetado claro y las agrupaciones lógicas de campos de entrada son fundamentales para una buena experiencia del usuario.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-164">Clear labeling and logical groupings of input fields are critical for a good user experience.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="2ef9c-165">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="2ef9c-165">Top use cases</span></span>

* <span data-ttu-id="2ef9c-166">Iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="2ef9c-166">Sign in</span></span>
* <span data-ttu-id="2ef9c-167">Perfiles de usuario</span><span class="sxs-lookup"><span data-stu-id="2ef9c-167">User profiles</span></span>
* <span data-ttu-id="2ef9c-168">Configuración</span><span class="sxs-lookup"><span data-stu-id="2ef9c-168">Settings</span></span>
* <span data-ttu-id="2ef9c-169">Colección de entrada de usuario</span><span class="sxs-lookup"><span data-stu-id="2ef9c-169">User input collection</span></span>

# <a name="desktop"></a>[<span data-ttu-id="2ef9c-170">Escritorio</span><span class="sxs-lookup"><span data-stu-id="2ef9c-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de formulario en el escritorio." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="2ef9c-172">Móvil</span><span class="sxs-lookup"><span data-stu-id="2ef9c-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-form.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de formulario en el móvil." border="false":::

---

## <a name="list"></a><span data-ttu-id="2ef9c-174">Lista</span><span class="sxs-lookup"><span data-stu-id="2ef9c-174">List</span></span>

<span data-ttu-id="2ef9c-175">Puede usar una lista para mostrar elementos relacionados en un formato analizable y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-175">You can use a list to display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="2ef9c-176">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="2ef9c-176">Top use cases</span></span>

* <span data-ttu-id="2ef9c-177">Mostrar datos</span><span class="sxs-lookup"><span data-stu-id="2ef9c-177">Display data</span></span>
* <span data-ttu-id="2ef9c-178">Acciones contextuales en el contenido de la aplicación</span><span class="sxs-lookup"><span data-stu-id="2ef9c-178">Contextual actions on app content</span></span>

# <a name="desktop"></a>[<span data-ttu-id="2ef9c-179">Escritorio</span><span class="sxs-lookup"><span data-stu-id="2ef9c-179">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de lista en el escritorio." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="2ef9c-181">Móvil</span><span class="sxs-lookup"><span data-stu-id="2ef9c-181">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-list.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de lista en el móvil." border="false":::

---

## <a name="sign-in"></a><span data-ttu-id="2ef9c-183">Iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="2ef9c-183">Sign in</span></span>

<span data-ttu-id="2ef9c-184">Puedes diseñar flujos de inicio de sesión de aplicaciones para diferentes Teams contextos y proveedores de identidades.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-184">You can design app sign-in flows for different Teams contexts and identity providers.</span></span> <span data-ttu-id="2ef9c-185">En el ejemplo siguiente se incluye el inicio de sesión único (SSO), que se recomienda para la experiencia de autenticación más sencilla.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-185">The following example includes single sign-on (SSO), which we recommend for the simplest authentication experience.</span></span>

### <a name="top-use-case"></a><span data-ttu-id="2ef9c-186">Caso de uso superior</span><span class="sxs-lookup"><span data-stu-id="2ef9c-186">Top use case</span></span>

* <span data-ttu-id="2ef9c-187">Autenticar usuarios</span><span class="sxs-lookup"><span data-stu-id="2ef9c-187">Authenticate users</span></span>

# <a name="desktop"></a>[<span data-ttu-id="2ef9c-188">Escritorio</span><span class="sxs-lookup"><span data-stu-id="2ef9c-188">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de inicio de sesión en el escritorio." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="2ef9c-190">Móvil</span><span class="sxs-lookup"><span data-stu-id="2ef9c-190">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-sign-in.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de inicio de sesión en el móvil." border="false":::

---

## <a name="settings"></a><span data-ttu-id="2ef9c-192">Configuración</span><span class="sxs-lookup"><span data-stu-id="2ef9c-192">Settings</span></span>

<span data-ttu-id="2ef9c-193">Configuración pantallas son donde los usuarios pueden configurar sus preferencias con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-193">Settings screens are where users can configure their preferences with your app.</span></span> <span data-ttu-id="2ef9c-194">(Nota: Configuración es un contenedor para componentes de interfaz [de usuario básicos](~/concepts/design/design-teams-app-basic-ui-components.md).)</span><span class="sxs-lookup"><span data-stu-id="2ef9c-194">(Note: Settings is a container for [basic UI components](~/concepts/design/design-teams-app-basic-ui-components.md).)</span></span>

### <a name="top-use-case"></a><span data-ttu-id="2ef9c-195">Caso de uso superior</span><span class="sxs-lookup"><span data-stu-id="2ef9c-195">Top use case</span></span>

* <span data-ttu-id="2ef9c-196">Administrar características de la aplicación</span><span class="sxs-lookup"><span data-stu-id="2ef9c-196">Manage app features</span></span>

:::image type="content" source="../../assets/images/ui-templates/settings.png" alt-text="En el ejemplo se muestra una plantilla de configuración." border="false":::

## <a name="task-board"></a><span data-ttu-id="2ef9c-198">Panel de tareas</span><span class="sxs-lookup"><span data-stu-id="2ef9c-198">Task board</span></span>

<span data-ttu-id="2ef9c-199">Un panel de tareas, a veces denominado tablero de kanban o carriles de natación, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o los vales.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-199">A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span> <span data-ttu-id="2ef9c-200">También se puede usar para ordenar cualquier tipo de contenido en categorías.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-200">It can also be used to sort any type of content into categories.</span></span> <span data-ttu-id="2ef9c-201">Puede editar y mover las tarjetas entre columnas.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-201">You can edit and move the cards between columns.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="2ef9c-202">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="2ef9c-202">Top use cases</span></span>

* <span data-ttu-id="2ef9c-203">Administración de proyectos.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-203">Project management.</span></span> <span data-ttu-id="2ef9c-204">Asignación de tareas y estado de seguimiento</span><span class="sxs-lookup"><span data-stu-id="2ef9c-204">Assigning tasks and tracking status</span></span>
* <span data-ttu-id="2ef9c-205">Lluvia de ideas.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-205">Brainstorming.</span></span> <span data-ttu-id="2ef9c-206">Agregar ideas en distintas categorías</span><span class="sxs-lookup"><span data-stu-id="2ef9c-206">Adding ideas in different categories</span></span>
* <span data-ttu-id="2ef9c-207">Ordenar ejercicios.</span><span class="sxs-lookup"><span data-stu-id="2ef9c-207">Sorting exercises.</span></span> <span data-ttu-id="2ef9c-208">Organizar cualquier tipo de información en cubos</span><span class="sxs-lookup"><span data-stu-id="2ef9c-208">Organizing any kind of information into buckets</span></span>

# <a name="desktop"></a>[<span data-ttu-id="2ef9c-209">Escritorio</span><span class="sxs-lookup"><span data-stu-id="2ef9c-209">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario del panel de tareas en el escritorio." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="2ef9c-211">Móvil</span><span class="sxs-lookup"><span data-stu-id="2ef9c-211">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-task-board.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario del panel de tareas en el móvil." border="false":::

---

## <a name="wizard"></a><span data-ttu-id="2ef9c-213">Asistente</span><span class="sxs-lookup"><span data-stu-id="2ef9c-213">Wizard</span></span>

<span data-ttu-id="2ef9c-214">Un asistente guía a un usuario a través de varias pantallas para completar una tarea (como un proceso de instalación).</span><span class="sxs-lookup"><span data-stu-id="2ef9c-214">A wizard guides a user through several screens to complete a task (such as a setup process).</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="2ef9c-215">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="2ef9c-215">Top use cases</span></span>

* <span data-ttu-id="2ef9c-216">Instalación</span><span class="sxs-lookup"><span data-stu-id="2ef9c-216">Setup</span></span>
* <span data-ttu-id="2ef9c-217">Incorporación</span><span class="sxs-lookup"><span data-stu-id="2ef9c-217">Onboarding</span></span>
* <span data-ttu-id="2ef9c-218">Experiencias de primera ejecución</span><span class="sxs-lookup"><span data-stu-id="2ef9c-218">First-run experiences</span></span>

# <a name="desktop"></a>[<span data-ttu-id="2ef9c-219">Escritorio</span><span class="sxs-lookup"><span data-stu-id="2ef9c-219">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario del asistente en el escritorio." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="2ef9c-221">Móvil</span><span class="sxs-lookup"><span data-stu-id="2ef9c-221">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-wizard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de asistente en el móvil." border="false":::

---

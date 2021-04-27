---
title: Diseño de módulos de tareas
author: heath-hamilton
description: Aprende a diseñar módulos de tareas para aplicaciones de Teams y a obtener el Kit de interfaz de usuario de Microsoft Teams.
localization_priority: Normal
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 3502a705bfe1bf99a5dc0edff5c5a54265cc6ca1
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019548"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a><span data-ttu-id="44574-103">Diseño de módulos de tareas para la aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="44574-103">Designing task modules for your Microsoft Teams app</span></span>

<span data-ttu-id="44574-104">Puedes crear experiencias emergentes modales en tu aplicación de Teams con módulos de tareas.</span><span class="sxs-lookup"><span data-stu-id="44574-104">You can create modal popup experiences in your Teams app with task modules.</span></span> <span data-ttu-id="44574-105">Use esta funcionalidad para mostrar medios enriquecidos e información o completar una tarea compleja.</span><span class="sxs-lookup"><span data-stu-id="44574-105">Use this capability to display rich media and information or complete a complex task.</span></span>

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="En el ejemplo se muestra un módulo de tareas." border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="44574-107">Kit de UI de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="44574-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="44574-108">Puedes encontrar instrucciones de diseño de módulos de tareas más completas, incluidos los elementos que puedes agarrar y modificar según sea necesario, en el Kit de interfaz de usuario de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="44574-108">You can find more comprehensive task module design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="44574-109">Obtener el Kit de UI de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="44574-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a><span data-ttu-id="44574-110">Abrir un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="44574-110">Open a task module</span></span>

<span data-ttu-id="44574-111">Los módulos de tareas se pueden iniciar desde casi cualquier lugar de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="44574-111">Task modules can be launched from almost anywhere in your app.</span></span>

* <span data-ttu-id="44574-112">**Tab:** se puede iniciar un módulo de tareas desde cualquier vínculo dentro de una pestaña. Se usa en escenarios en los que desea que el usuario se centre en una interacción.</span><span class="sxs-lookup"><span data-stu-id="44574-112">**Tab**: A task module can be launched from any link within a tab. Use in scenarios where you want the user to focus on an interaction.</span></span>
* <span data-ttu-id="44574-113">**Bot:** se puede iniciar un módulo de tareas desde un vínculo dentro de un mensaje de bot.</span><span class="sxs-lookup"><span data-stu-id="44574-113">**Bot**: A task module can be launched from a link inside a bot message.</span></span>
* <span data-ttu-id="44574-114">**Tarjeta adaptable:** se puede iniciar un módulo de tareas desde una tarjeta adaptable (enviada con una extensión de mensajería o por un bot) cuando un usuario selecciona un botón.</span><span class="sxs-lookup"><span data-stu-id="44574-114">**Adaptive Card**: A task module can be launched from an Adaptive Card (sent with a messaging extension or by a bot) when a user selects a button.</span></span>
* <span data-ttu-id="44574-115">**Extensión de mensajería (comandos de acción):** las extensiones de mensajería permiten realizar una acción determinada en el contenido del mensaje.</span><span class="sxs-lookup"><span data-stu-id="44574-115">**Messaging extension (action commands)**: Messaging extensions allow you to take a particular action on message content.</span></span> <span data-ttu-id="44574-116">Al seleccionar una acción, se abre un módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="44574-116">Selecting an action opens a task module.</span></span>
* <span data-ttu-id="44574-117">**Extensión de mensajería (contexto del** cuadro de redacción): en el cuadro de redacción, puede diseñar una extensión de mensajería para abrir un módulo de tareas en lugar del control desplegable típico.</span><span class="sxs-lookup"><span data-stu-id="44574-117">**Messaging extension (compose box context)**: In the compose box, you can design a messaging extension to open a task module instead of the typical flyout.</span></span> <span data-ttu-id="44574-118">Reserve módulos de tareas para interacciones complejas, como completar un formulario.</span><span class="sxs-lookup"><span data-stu-id="44574-118">Reserve task modules for complex interactions, such as completing a form.</span></span>

## <a name="anatomy"></a><span data-ttu-id="44574-119">Anatomía</span><span class="sxs-lookup"><span data-stu-id="44574-119">Anatomy</span></span>

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un módulo de tareas." border="false":::

<span data-ttu-id="44574-121">Los módulos de tareas son superficies muy flexibles.</span><span class="sxs-lookup"><span data-stu-id="44574-121">Task modules are very flexible surfaces.</span></span> <span data-ttu-id="44574-122">Se pueden crear con iframes, lo que hace que se usen otras plantillas de interfaz de usuario para hospedar experiencias creadas por asociados.</span><span class="sxs-lookup"><span data-stu-id="44574-122">They can be built with iframes, pulling in other UI templates, to host partner-built experiences.</span></span> <span data-ttu-id="44574-123">Esto es preferible para la experiencia más pulida.</span><span class="sxs-lookup"><span data-stu-id="44574-123">This is preferred for the most polished experience.</span></span>

<span data-ttu-id="44574-124">También se pueden crear con el marco [de](../../task-modules-and-cards/cards/design-effective-cards.md) tarjeta adaptable, que puede ser una forma más sencilla y rápida de ejecutar escenarios comunes (como formularios).</span><span class="sxs-lookup"><span data-stu-id="44574-124">They can also be built with the [Adaptive Card](../../task-modules-and-cards/cards/design-effective-cards.md) framework, which can be a simpler and faster way to execute common scenarios (such as forms).</span></span>

|<span data-ttu-id="44574-125">Contador</span><span class="sxs-lookup"><span data-stu-id="44574-125">Counter</span></span>|<span data-ttu-id="44574-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="44574-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="44574-127">1</span><span class="sxs-lookup"><span data-stu-id="44574-127">1</span></span>|<span data-ttu-id="44574-128">**Icono de aplicación**</span><span class="sxs-lookup"><span data-stu-id="44574-128">**App icon**</span></span>|
|<span data-ttu-id="44574-129">2</span><span class="sxs-lookup"><span data-stu-id="44574-129">2</span></span>|<span data-ttu-id="44574-130">**Nombre de la** aplicación: nombre completo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="44574-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="44574-131">3</span><span class="sxs-lookup"><span data-stu-id="44574-131">3</span></span>|<span data-ttu-id="44574-132">**Encabezado:** haga que los encabezados sea claros y concisos.</span><span class="sxs-lookup"><span data-stu-id="44574-132">**Header**: Make headers clear and concise.</span></span> <span data-ttu-id="44574-133">Describa la tarea que desea que los usuarios completen.</span><span class="sxs-lookup"><span data-stu-id="44574-133">Describe the task you want users to complete.</span></span>
|<span data-ttu-id="44574-134">4 </span><span class="sxs-lookup"><span data-stu-id="44574-134">4</span></span>|<span data-ttu-id="44574-135">**Botón Cerrar:** permite a los usuarios encontrar el contenido de la aplicación que desean insertar.</span><span class="sxs-lookup"><span data-stu-id="44574-135">**Close button**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="44574-136">5 </span><span class="sxs-lookup"><span data-stu-id="44574-136">5</span></span>|<span data-ttu-id="44574-137">**iframe:** espacio dinámico que hospeda el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="44574-137">**iframe**: Responsive space that hosts your app content.</span></span>|
|<span data-ttu-id="44574-138">6 </span><span class="sxs-lookup"><span data-stu-id="44574-138">6</span></span>|<span data-ttu-id="44574-139">**Acciones (opcional):** botones relacionados con el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="44574-139">**Actions (optional)**: Buttons related to your app content.</span></span>|

## <a name="designing-with-ui-templates"></a><span data-ttu-id="44574-140">Diseño con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="44574-140">Designing with UI templates</span></span>

<span data-ttu-id="44574-141">Considere la posibilidad de usar plantillas para diseños comunes dentro de los módulos de tareas.</span><span class="sxs-lookup"><span data-stu-id="44574-141">Consider using templates for common layouts inside your task modules.</span></span> <span data-ttu-id="44574-142">Cada uno de ellos está hecho de componentes más pequeños para crear un diseño elegante y con capacidad de respuesta que se puede usar de forma personalizada para el escenario o con la apariencia de la marca.</span><span class="sxs-lookup"><span data-stu-id="44574-142">Each one is made up of smaller components to create an elegant, responsive design that can be used out of the box or customized for your scenario or with your brand look and feel.</span></span>

* <span data-ttu-id="44574-143">[Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato digitalizado y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="44574-143">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="44574-144">[Formulario:](../../concepts/design/design-teams-app-ui-templates.md#form)los formularios son para recopilar, validar y enviar la entrada del usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="44574-144">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="44574-145">[Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacío se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.</span><span class="sxs-lookup"><span data-stu-id="44574-145">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="examples"></a><span data-ttu-id="44574-146">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="44574-146">Examples</span></span>

### <a name="list"></a><span data-ttu-id="44574-147">Lista</span><span class="sxs-lookup"><span data-stu-id="44574-147">List</span></span>

<span data-ttu-id="44574-148">Las listas funcionan bien en un módulo de tareas porque son fáciles de examinar.</span><span class="sxs-lookup"><span data-stu-id="44574-148">Lists work nicely in a task module because they’re easy to scan.</span></span>

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="Lista de ejemplos en un módulo de tareas." border="false":::

### <a name="form"></a><span data-ttu-id="44574-150">Form</span><span class="sxs-lookup"><span data-stu-id="44574-150">Form</span></span>

<span data-ttu-id="44574-151">Los módulos de tareas son un excelente lugar para superficier formularios con entradas de usuario secuenciales y validación en línea.</span><span class="sxs-lookup"><span data-stu-id="44574-151">Task modules are a great place to surface forms with sequential user inputs and inline validation.</span></span> <span data-ttu-id="44574-152">Puedes aprovechar las tarjetas adaptables como una forma de insertar elementos de formulario.</span><span class="sxs-lookup"><span data-stu-id="44574-152">You can leverage Adaptive Cards as a way to embed form elements.</span></span>

:::image type="content" source="../../assets/images/task-module/form.png" alt-text="Formulario de ejemplo en un módulo de tareas." border="false":::

### <a name="sign-in"></a><span data-ttu-id="44574-154">Iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="44574-154">Sign in</span></span>

<span data-ttu-id="44574-155">Cree un flujo de inicio de sesión o registro centrado con una serie de módulos de tareas, lo que permite a los usuarios moverse fácilmente a través de pasos secuenciales.</span><span class="sxs-lookup"><span data-stu-id="44574-155">Create a focused sign in or sign-up flow with a series of task modules, letting users move easily through sequential steps.</span></span>

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="Ejemplo de experiencia de inicio de sesión en un módulo de tareas." border="false":::

### <a name="media"></a><span data-ttu-id="44574-157">Elementos multimedia</span><span class="sxs-lookup"><span data-stu-id="44574-157">Media</span></span>

<span data-ttu-id="44574-158">Insertar contenido multimedia en un módulo de tareas para una experiencia de visualización centrada.</span><span class="sxs-lookup"><span data-stu-id="44574-158">Embed media content in a task module for a focused viewing experience.</span></span>

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="Ejemplo de contenido multimedia en un módulo de tareas." border="false":::

### <a name="empty-state"></a><span data-ttu-id="44574-160">Estado vacío</span><span class="sxs-lookup"><span data-stu-id="44574-160">Empty state</span></span>

<span data-ttu-id="44574-161">Se usa para los mensajes de bienvenida, error y éxito.</span><span class="sxs-lookup"><span data-stu-id="44574-161">Use for welcome, error, and success messages.</span></span>

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="Estado vacío de ejemplo en un módulo de tareas." border="false":::

### <a name="image-gallery"></a><span data-ttu-id="44574-163">Galería de imágenes</span><span class="sxs-lookup"><span data-stu-id="44574-163">Image gallery</span></span>

<span data-ttu-id="44574-164">Inserte un carrusel de galería en un iframe.</span><span class="sxs-lookup"><span data-stu-id="44574-164">Embed a gallery carousel in an iframe.</span></span>

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="Galería de imágenes de ejemplo en un módulo de tareas." border="false":::

### <a name="poll"></a><span data-ttu-id="44574-166">Sondeo</span><span class="sxs-lookup"><span data-stu-id="44574-166">Poll</span></span>

<span data-ttu-id="44574-167">En este ejemplo se muestran los resultados del sondeo iniciados desde una tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="44574-167">This example shows poll results launched from an Adaptive Card.</span></span> <span data-ttu-id="44574-168">El sondeo también se puede colocar dentro de un módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="44574-168">The poll can be placed inside a task module, too.</span></span>

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="Sondeo de ejemplo en un módulo de tareas." border="false":::

## <a name="best-practices"></a><span data-ttu-id="44574-170">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="44574-170">Best practices</span></span>

### <a name="usability"></a><span data-ttu-id="44574-171">Facilidad de uso</span><span class="sxs-lookup"><span data-stu-id="44574-171">Usability</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado del módulo de tareas." border="false":::

#### <a name="do-use-one-task-module-at-a-time"></a><span data-ttu-id="44574-173">Hacer: Usar un módulo de tareas a la vez</span><span class="sxs-lookup"><span data-stu-id="44574-173">Do: Use one task module at a time</span></span>

<span data-ttu-id="44574-174">El objetivo es centrar al usuario en completar una tarea después de todo.</span><span class="sxs-lookup"><span data-stu-id="44574-174">The goal is to focus the user on completing a task after all!</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="En el ejemplo se muestra un procedimiento recomendado del módulo de tareas." border="false":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a><span data-ttu-id="44574-176">Don't: Pop a dialog on top of a task module</span><span class="sxs-lookup"><span data-stu-id="44574-176">Don't: Pop a dialog on top of a task module</span></span>

<span data-ttu-id="44574-177">Esto crea una experiencia de usuario confusa y desenfoque.</span><span class="sxs-lookup"><span data-stu-id="44574-177">This creates an unfocused, confusing user experience.</span></span>

   :::column-end:::
:::row-end:::

### <a name="responsive"></a><span data-ttu-id="44574-178">Respuesta correcta</span><span class="sxs-lookup"><span data-stu-id="44574-178">Responsive</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="En el ejemplo se muestra el procedimiento recomendado del módulo de tareas." border="false":::

#### <a name="do-make-sure-the-content-is-responsive"></a><span data-ttu-id="44574-180">Do: Make sure the content is responsive</span><span class="sxs-lookup"><span data-stu-id="44574-180">Do: Make sure the content is responsive</span></span>

<span data-ttu-id="44574-181">Aunque las tarjetas adaptables hospedadas en un módulo de tareas se representan correctamente en dispositivos móviles, si eliges usar un iframe para hospedar contenido de la aplicación, asegúrate de que la interfaz de usuario responda y funcione bien en todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="44574-181">While Adaptive Cards hosted in a task module render well on mobile devices, if you choose to use an iframe to host app content, make sure the UI is responsive and works well across devices.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="En el ejemplo se muestra un procedimiento recomendado del módulo de tareas." border="false":::

#### <a name="dont-use-horizontal-scroll-bars"></a><span data-ttu-id="44574-183">No usar: Usar barras de desplazamiento horizontales</span><span class="sxs-lookup"><span data-stu-id="44574-183">Don't: Use horizontal scroll bars</span></span>

<span data-ttu-id="44574-184">Es un procedimiento recomendado mantener el contenido centrado y no demasiado largo.</span><span class="sxs-lookup"><span data-stu-id="44574-184">It's a best practice to keep content focused and not too lengthy.</span></span> <span data-ttu-id="44574-185">Si es necesario un desplazamiento, desplácese verticalmente y no horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="44574-185">If a scroll is necessary, scroll vertically and not horizontally.</span></span>

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a><span data-ttu-id="44574-186">Simplicidad</span><span class="sxs-lookup"><span data-stu-id="44574-186">Simplicity</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="En el ejemplo se muestra el procedimiento recomendado del módulo de tareas." border="false":::

#### <a name="do-keep-it-short"></a><span data-ttu-id="44574-188">Do: Keep it short</span><span class="sxs-lookup"><span data-stu-id="44574-188">Do: Keep it short</span></span>

<span data-ttu-id="44574-189">Puedes crear fácilmente un asistente para varios pasos, pero eso no significa necesariamente que debas hacerlo.</span><span class="sxs-lookup"><span data-stu-id="44574-189">You can easily create a multi-step wizard, but that doesn't necessarily mean you should!</span></span> <span data-ttu-id="44574-190">Un módulo de tareas de varias pantallas puede ser problemático porque los mensajes entrantes distraen y tenta a los usuarios a salir.</span><span class="sxs-lookup"><span data-stu-id="44574-190">A multi-screen task module can be problematic because incoming messages are distracting and tempt users to exit.</span></span> <span data-ttu-id="44574-191">Si la tarea está realmente implicada, abre una página web completa en lugar de un módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="44574-191">If your task is really involved, pop out to a full webpage instead of a task module.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="Ilustración que muestra un procedimiento recomendado del módulo de tareas." border="false":::

#### <a name="dont-do-long-interactions"></a><span data-ttu-id="44574-193">No hacer: realizar interacciones largas</span><span class="sxs-lookup"><span data-stu-id="44574-193">Don't: Do long interactions</span></span>

<span data-ttu-id="44574-194">Intenta mantener tus interacciones cortas y hasta el punto.</span><span class="sxs-lookup"><span data-stu-id="44574-194">Try to keep your interactions short and to the point.</span></span>

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a><span data-ttu-id="44574-195">Mensajes de error</span><span class="sxs-lookup"><span data-stu-id="44574-195">Error messages</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="La ilustración muestra un procedimiento recomendado del módulo de tareas." border="false":::

#### <a name="do-use-inline-error-messages"></a><span data-ttu-id="44574-197">Hacer: usar mensajes de error en línea</span><span class="sxs-lookup"><span data-stu-id="44574-197">Do: Use inline error messages</span></span>

<span data-ttu-id="44574-198">Consulta la plantilla de interfaz de usuario de formularios para obtener instrucciones sobre el control de errores en línea.</span><span class="sxs-lookup"><span data-stu-id="44574-198">See the forms UI template for guidelines on inline error handling.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="La ilustración muestra un procedimiento recomendado del módulo de tareas." border="false":::

#### <a name="dont-put-error-messages-in-dialogs"></a><span data-ttu-id="44574-200">No: poner mensajes de error en cuadros de diálogo</span><span class="sxs-lookup"><span data-stu-id="44574-200">Don't: Put error messages in dialogs</span></span>

<span data-ttu-id="44574-201">No aparece un mensaje de error en un cuadro de diálogo encima de los módulos de tareas.</span><span class="sxs-lookup"><span data-stu-id="44574-201">Don't pop an error message in a dialog on top of a task modules.</span></span> <span data-ttu-id="44574-202">Crea una experiencia de usuario confusa.</span><span class="sxs-lookup"><span data-stu-id="44574-202">It creates a confusing user experience.</span></span>

   :::column-end:::
:::row-end:::

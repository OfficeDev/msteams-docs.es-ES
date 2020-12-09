---
title: Diseño de módulos de tareas
author: heath-hamilton
description: Obtenga información sobre cómo diseñar módulos de tareas para las aplicaciones de Teams y obtener el kit de IU de Microsoft Teams.
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 41584ecf58ca7718290e58e5845549e4579dac64
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2020
ms.locfileid: "49606416"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a><span data-ttu-id="21228-103">Diseño de módulos de tareas para su aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="21228-103">Designing task modules for your Microsoft Teams app</span></span>

<span data-ttu-id="21228-104">Puede crear experiencias de elemento emergente modal en la aplicación de Microsoft Teams con módulos de tareas.</span><span class="sxs-lookup"><span data-stu-id="21228-104">You can create modal popup experiences in your Teams app with task modules.</span></span> <span data-ttu-id="21228-105">Use esta funcionalidad para mostrar información y medios enriquecidos o para completar una tarea compleja.</span><span class="sxs-lookup"><span data-stu-id="21228-105">Use this capability to display rich media and information or complete a complex task.</span></span>

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="Ejemplo muestra un módulo de tarea." border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="21228-107">Kit de IU de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="21228-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="21228-108">Puede encontrar instrucciones de diseño de módulos de tareas más completas, incluidos elementos que puede captar y modificar según sea necesario, en el kit de interfaz de usuario de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="21228-108">You can find more comprehensive task module design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="21228-109">Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="21228-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a><span data-ttu-id="21228-110">Abrir un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="21228-110">Open a task module</span></span>

<span data-ttu-id="21228-111">Los módulos de tareas se pueden iniciar casi en cualquier lugar de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="21228-111">Task modules can be launched from almost anywhere in your app.</span></span>

* <span data-ttu-id="21228-112">**Tab**: se puede iniciar un módulo de tareas desde cualquier vínculo dentro de una pestaña o iframe.</span><span class="sxs-lookup"><span data-stu-id="21228-112">**Tab**: A task module can be launched from any link within a tab or iframe.</span></span> <span data-ttu-id="21228-113">Úsela en escenarios en los que desea que el usuario se Centre en una interacción.</span><span class="sxs-lookup"><span data-stu-id="21228-113">Use in scenarios where you want the user to focus on an interaction.</span></span>
* <span data-ttu-id="21228-114">**Bot**: un módulo de tarea puede iniciarse desde un vínculo dentro de un mensaje de bot.</span><span class="sxs-lookup"><span data-stu-id="21228-114">**Bot**: A task module can be launched from a link inside a bot message.</span></span>
* <span data-ttu-id="21228-115">**Tarjeta adaptable**: un módulo de tarea se puede iniciar desde una tarjeta adaptable (enviada con una extensión de mensajería o mediante un bot) cuando un usuario selecciona un botón.</span><span class="sxs-lookup"><span data-stu-id="21228-115">**Adaptive Card**: A task module can be launched from an Adaptive Card (sent with a messaging extension or by a bot) when a user selects a button.</span></span>
* <span data-ttu-id="21228-116">**Extensión de mensajería (comandos de acción)**: extensiones de mensajería le permite realizar una acción concreta en el contenido del mensaje.</span><span class="sxs-lookup"><span data-stu-id="21228-116">**Messaging extension (action commands)**: Messaging extensions allow you to take a particular action on message content.</span></span> <span data-ttu-id="21228-117">Al seleccionar una acción se abre un módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="21228-117">Selecting an action opens a task module.</span></span>
* <span data-ttu-id="21228-118">**Extensión de mensajería (contexto de cuadro de redacción)**: en el cuadro de redacción, puede diseñar una extensión de mensajería para abrir un módulo de tareas en lugar del flotante normal.</span><span class="sxs-lookup"><span data-stu-id="21228-118">**Messaging extension (compose box context)**: In the compose box, you can design a messaging extension to open a task module instead of the typical flyout.</span></span> <span data-ttu-id="21228-119">Reserve módulos de tareas para interacciones complejas, como rellenar un formulario.</span><span class="sxs-lookup"><span data-stu-id="21228-119">Reserve task modules for complex interactions, such as completing a form.</span></span>

## <a name="anatomy"></a><span data-ttu-id="21228-120">Anatomía</span><span class="sxs-lookup"><span data-stu-id="21228-120">Anatomy</span></span>

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un módulo de tareas." border="false":::

<span data-ttu-id="21228-122">Los módulos de tareas son superficies muy flexibles.</span><span class="sxs-lookup"><span data-stu-id="21228-122">Task modules are very flexible surfaces.</span></span> <span data-ttu-id="21228-123">Se pueden crear con iframes, al extraer en otras plantillas de interfaz de usuario, para hospedar experiencias creadas por asociados.</span><span class="sxs-lookup"><span data-stu-id="21228-123">They can be built with iframes, pulling in other UI templates, to host partner-built experiences.</span></span> <span data-ttu-id="21228-124">Esta es la preferida para la experiencia más pulida.</span><span class="sxs-lookup"><span data-stu-id="21228-124">This is preferred for the most polished experience.</span></span>

<span data-ttu-id="21228-125">También se pueden crear con el marco de [tarjeta adaptable](../../task-modules-and-cards/cards/design-effective-cards.md) , que puede ser una forma más sencilla y rápida de ejecutar escenarios comunes (como formularios).</span><span class="sxs-lookup"><span data-stu-id="21228-125">They can also be built with the [Adaptive Card](../../task-modules-and-cards/cards/design-effective-cards.md) framework, which can be a simpler and faster way to execute common scenarios (such as forms).</span></span>

|<span data-ttu-id="21228-126">Counter</span><span class="sxs-lookup"><span data-stu-id="21228-126">Counter</span></span>|<span data-ttu-id="21228-127">Descripción</span><span class="sxs-lookup"><span data-stu-id="21228-127">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="21228-128">1</span><span class="sxs-lookup"><span data-stu-id="21228-128">1</span></span>|<span data-ttu-id="21228-129">**Icono de aplicación**</span><span class="sxs-lookup"><span data-stu-id="21228-129">**App icon**</span></span>|
|<span data-ttu-id="21228-130">2 </span><span class="sxs-lookup"><span data-stu-id="21228-130">2</span></span>|<span data-ttu-id="21228-131">**Nombre** de la aplicación: nombre completo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="21228-131">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="21228-132">3 </span><span class="sxs-lookup"><span data-stu-id="21228-132">3</span></span>|<span data-ttu-id="21228-133">**Encabezado**: hacer que los encabezados sean claros y concisos.</span><span class="sxs-lookup"><span data-stu-id="21228-133">**Header**: Make headers clear and concise.</span></span> <span data-ttu-id="21228-134">Describa la tarea que desea que completen los usuarios.</span><span class="sxs-lookup"><span data-stu-id="21228-134">Describe the task you want users to complete.</span></span>
|<span data-ttu-id="21228-135">4 </span><span class="sxs-lookup"><span data-stu-id="21228-135">4</span></span>|<span data-ttu-id="21228-136">**Botón Cerrar**: permite a los usuarios buscar el contenido de la aplicación que quiera insertar.</span><span class="sxs-lookup"><span data-stu-id="21228-136">**Close button**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="21228-137">5 </span><span class="sxs-lookup"><span data-stu-id="21228-137">5</span></span>|<span data-ttu-id="21228-138">**iframe**: espacio de respuesta que hospeda el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="21228-138">**iframe**: Responsive space that hosts your app content.</span></span>|
|<span data-ttu-id="21228-139">6 </span><span class="sxs-lookup"><span data-stu-id="21228-139">6</span></span>|<span data-ttu-id="21228-140">**Acciones (opcional)**: botones relacionados con el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="21228-140">**Actions (optional)**: Buttons related to your app content.</span></span>|

## <a name="designing-with-ui-templates"></a><span data-ttu-id="21228-141">Diseño con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="21228-141">Designing with UI templates</span></span>

<span data-ttu-id="21228-142">Considere la posibilidad de usar plantillas para los diseños comunes dentro de los módulos de tareas.</span><span class="sxs-lookup"><span data-stu-id="21228-142">Consider using templates for common layouts inside your task modules.</span></span> <span data-ttu-id="21228-143">Cada uno de ellos consta de componentes más pequeños para crear un diseño elegante y dinámico que se puede usar de forma rápida o personalizada para su escenario o con la apariencia de la marca.</span><span class="sxs-lookup"><span data-stu-id="21228-143">Each one is made up of smaller components to create an elegant, responsive design that can be used out of the box or customized for your scenario or with your brand look and feel.</span></span>

* <span data-ttu-id="21228-144">[List](../../concepts/design/design-teams-app-ui-templates.md#list): lists puede mostrar elementos relacionados en un formato que se pueda analizar y permitir que los usuarios realicen acciones en una lista completa o en elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="21228-144">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="21228-145">[Formulario](../../concepts/design/design-teams-app-ui-templates.md#form): los formularios son para recopilar, validar y enviar entradas de usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="21228-145">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="21228-146">[Estado vacío](../../concepts/design/design-teams-app-ui-templates.md#empty-state): la plantilla de estado vacía se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error, etc.</span><span class="sxs-lookup"><span data-stu-id="21228-146">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="examples"></a><span data-ttu-id="21228-147">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="21228-147">Examples</span></span>

### <a name="list"></a><span data-ttu-id="21228-148">Lista</span><span class="sxs-lookup"><span data-stu-id="21228-148">List</span></span>

<span data-ttu-id="21228-149">Las listas funcionan bien en un módulo de tareas porque son fáciles de analizar.</span><span class="sxs-lookup"><span data-stu-id="21228-149">Lists work nicely in a task module because they’re easy to scan.</span></span>

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="Lista de ejemplo de un módulo de tareas." border="false":::

### <a name="form"></a><span data-ttu-id="21228-151">Form</span><span class="sxs-lookup"><span data-stu-id="21228-151">Form</span></span>

<span data-ttu-id="21228-152">Los módulos de tareas son un buen punto de partida para exponer formularios con entradas de usuario secuenciales y validación en línea.</span><span class="sxs-lookup"><span data-stu-id="21228-152">Task modules are a great place to surface forms with sequential user inputs and inline validation.</span></span> <span data-ttu-id="21228-153">Puede aprovechar las tarjetas adaptables como una forma de incrustar los elementos del formulario.</span><span class="sxs-lookup"><span data-stu-id="21228-153">You can leverage Adaptive Cards as a way to embed form elements.</span></span>

:::image type="content" source="../../assets/images/task-module/form.png" alt-text="Formulario de ejemplo en un módulo de tareas." border="false":::

### <a name="sign-in"></a><span data-ttu-id="21228-155">Iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="21228-155">Sign in</span></span>

<span data-ttu-id="21228-156">Crear un flujo de inicio de sesión o de inicio de sesión prioritarios con una serie de módulos de tareas, lo que permite a los usuarios desplazarse fácilmente a través de pasos secuenciales.</span><span class="sxs-lookup"><span data-stu-id="21228-156">Create a focused sign in or sign-up flow with a series of task modules, letting users move easily through sequential steps.</span></span>

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="Ejemplo de experiencia de inicio de sesión en un módulo de tareas." border="false":::

### <a name="media"></a><span data-ttu-id="21228-158">Audiovisual</span><span class="sxs-lookup"><span data-stu-id="21228-158">Media</span></span>

<span data-ttu-id="21228-159">Insertar contenido multimedia en un módulo de tareas para una experiencia de visualización específica.</span><span class="sxs-lookup"><span data-stu-id="21228-159">Embed media content in a task module for a focused viewing experience.</span></span>

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="Contenido multimedia de ejemplo en un módulo de tareas." border="false":::

### <a name="empty-state"></a><span data-ttu-id="21228-161">Estado vacío</span><span class="sxs-lookup"><span data-stu-id="21228-161">Empty state</span></span>

<span data-ttu-id="21228-162">Usar para los mensajes de bienvenida, error y operación correcta.</span><span class="sxs-lookup"><span data-stu-id="21228-162">Use for welcome, error, and success messages.</span></span>

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="Ejemplo de estado vacío en un módulo de tareas." border="false":::

### <a name="image-gallery"></a><span data-ttu-id="21228-164">Galería de imágenes</span><span class="sxs-lookup"><span data-stu-id="21228-164">Image gallery</span></span>

<span data-ttu-id="21228-165">Inserta un carrusel de Galería dentro de un iframe.</span><span class="sxs-lookup"><span data-stu-id="21228-165">Embed a gallery carousel inside an iframe.</span></span>

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="Galería de imágenes de ejemplo en un módulo de tareas." border="false":::

### <a name="poll"></a><span data-ttu-id="21228-167">Buscar</span><span class="sxs-lookup"><span data-stu-id="21228-167">Poll</span></span>

<span data-ttu-id="21228-168">En este ejemplo se muestran los resultados de sondeo iniciados desde una tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="21228-168">This example shows poll results launched from an Adaptive Card.</span></span>

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="Ejemplo de sondeo en un módulo de tareas." border="false":::

## <a name="best-practices"></a><span data-ttu-id="21228-170">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="21228-170">Best practices</span></span>

### <a name="usability"></a><span data-ttu-id="21228-171">Mejoras</span><span class="sxs-lookup"><span data-stu-id="21228-171">Usability</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de módulo de tareas." border="false":::

#### <a name="do-use-one-task-module-at-a-time"></a><span data-ttu-id="21228-173">Do: usar un módulo de tareas a la vez</span><span class="sxs-lookup"><span data-stu-id="21228-173">Do: Use one task module at a time</span></span>

<span data-ttu-id="21228-174">El objetivo es centrar al usuario en la finalización de una tarea después de todo.</span><span class="sxs-lookup"><span data-stu-id="21228-174">The goal is to focus the user on completing a task after all!</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de módulo de tareas." border="false":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a><span data-ttu-id="21228-176">No: mostrar un cuadro de diálogo en la parte superior de un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="21228-176">Don't: Pop a dialog on top of a task module</span></span>

<span data-ttu-id="21228-177">Esto crea una experiencia de usuario confusa y no enfocada.</span><span class="sxs-lookup"><span data-stu-id="21228-177">This creates an unfocused, confusing user experience.</span></span>

   :::column-end:::
:::row-end:::

### <a name="responsive"></a><span data-ttu-id="21228-178">Respuesta correcta</span><span class="sxs-lookup"><span data-stu-id="21228-178">Responsive</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de módulo de tareas." border="false":::

#### <a name="do-make-sure-the-content-is-responsive"></a><span data-ttu-id="21228-180">Haga lo siguiente: Asegúrese de que el contenido está respondiendo</span><span class="sxs-lookup"><span data-stu-id="21228-180">Do: Make sure the content is responsive</span></span>

<span data-ttu-id="21228-181">Aunque las tarjetas adaptables hospedadas en un módulo de tareas se presentan correctamente en dispositivos móviles, si decide usar un iframe para hospedar el contenido de la aplicación, asegúrese de que la interfaz de usuario responda correctamente y de que funcione en todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="21228-181">While Adaptive Cards hosted in a task module render well on mobile devices, if you choose to use an iframe to host app content, make sure the UI is responsive and works well across devices.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de módulo de tareas." border="false":::

#### <a name="dont-use-horizontal-scrollbars"></a><span data-ttu-id="21228-183">No: usar barras de desplazamiento horizontales</span><span class="sxs-lookup"><span data-stu-id="21228-183">Don't: Use horizontal scrollbars</span></span>

<span data-ttu-id="21228-184">Se recomienda mantener el contenido enfocado y no demasiado largo.</span><span class="sxs-lookup"><span data-stu-id="21228-184">It's a best practice to keep content focused and not too lengthy.</span></span> <span data-ttu-id="21228-185">Si es necesario un desplazamiento, desplácese verticalmente y no horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="21228-185">If a scroll is necessary, scroll vertically and not horizontally.</span></span>

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a><span data-ttu-id="21228-186">Simple</span><span class="sxs-lookup"><span data-stu-id="21228-186">Simplicity</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de módulo de tareas." border="false":::

#### <a name="do-keep-it-short"></a><span data-ttu-id="21228-188">Do: Keep it Short</span><span class="sxs-lookup"><span data-stu-id="21228-188">Do: Keep it short</span></span>

<span data-ttu-id="21228-189">Puede crear fácilmente un asistente de varios pasos, pero esto no significa necesariamente que debería.</span><span class="sxs-lookup"><span data-stu-id="21228-189">You can easily create a multi-step wizard, but that doesn't necessarily mean you should!</span></span> <span data-ttu-id="21228-190">Un módulo de tarea de varias pantallas puede ser problemático porque los mensajes entrantes distraen y tentan a los usuarios a salir.</span><span class="sxs-lookup"><span data-stu-id="21228-190">A multi-screen task module can be problematic because incoming messages are distracting and tempt users to exit.</span></span> <span data-ttu-id="21228-191">Si su tarea realmente está implicada, salga a una página web completa en lugar de a un módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="21228-191">If your task is really involved, pop out to a full webpage instead of a task module.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de módulo de tareas." border="false":::

#### <a name="dont-do-long-interactions"></a><span data-ttu-id="21228-193">No: realizar acciones largas</span><span class="sxs-lookup"><span data-stu-id="21228-193">Don't: Do long interactions</span></span>

<span data-ttu-id="21228-194">Intente mantener sus interacciones cortas y en el punto.</span><span class="sxs-lookup"><span data-stu-id="21228-194">Try to keep your interactions short and to the point.</span></span>

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a><span data-ttu-id="21228-195">Mensajes de error</span><span class="sxs-lookup"><span data-stu-id="21228-195">Error messages</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de módulo de tareas." border="false":::

#### <a name="do-use-inline-error-messages"></a><span data-ttu-id="21228-197">Do: usar mensajes de error en línea</span><span class="sxs-lookup"><span data-stu-id="21228-197">Do: Use inline error messages</span></span>

<span data-ttu-id="21228-198">Vea la plantilla de interfaz de usuario de formularios para obtener instrucciones sobre el tratamiento de errores en línea.</span><span class="sxs-lookup"><span data-stu-id="21228-198">See the forms UI template for guidelines on inline error handling.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de módulo de tareas." border="false":::

#### <a name="dont-put-error-messages-in-dialogs"></a><span data-ttu-id="21228-200">No: colocar mensajes de error en los cuadros de diálogo</span><span class="sxs-lookup"><span data-stu-id="21228-200">Don't: Put error messages in dialogs</span></span>

<span data-ttu-id="21228-201">No mostrar un mensaje de error en un cuadro de diálogo encima de los módulos de tareas.</span><span class="sxs-lookup"><span data-stu-id="21228-201">Don't pop an error message in a dialog on top of a task modules.</span></span> <span data-ttu-id="21228-202">Crea una experiencia de usuario confusa.</span><span class="sxs-lookup"><span data-stu-id="21228-202">It creates a confusing user experience.</span></span>

   :::column-end:::
:::row-end:::

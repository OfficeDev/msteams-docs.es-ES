---
title: Diseño de la extensión de la reunión
author: heath-hamilton
description: Obtenga información sobre cómo diseñar aplicaciones en reuniones de Microsoft Teams y obtener el kit de interfaz de usuario de Microsoft Teams.
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 3d18895626d5f2846d10e7145a622834d82b2e98
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2020
ms.locfileid: "49606367"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="f89a1-103">Diseño de la extensión de reunión de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f89a1-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="f89a1-104">Puede crear aplicaciones para que las reuniones sean más productivas.</span><span class="sxs-lookup"><span data-stu-id="f89a1-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="f89a1-105">Por ejemplo, solicite a los usuarios que completen una encuesta durante una llamada o envíen un recordatorio rápido que no interrumpa el flujo de la reunión.</span><span class="sxs-lookup"><span data-stu-id="f89a1-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="f89a1-106">Kit de IU de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f89a1-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="f89a1-107">Puede encontrar instrucciones de diseño más completas, incluidos elementos que puede captar y modificar según sea necesario, en el kit de interfaz de usuario de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="f89a1-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f89a1-108">Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="f89a1-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="f89a1-109">Agregar una extensión de reunión</span><span class="sxs-lookup"><span data-stu-id="f89a1-109">Add a meeting extension</span></span>

<span data-ttu-id="f89a1-110">Puede Agregar una extensión de reunión antes y durante las reuniones.</span><span class="sxs-lookup"><span data-stu-id="f89a1-110">You can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="f89a1-111">También puede disponer de una aplicación para una reunión específica directamente desde la tienda Teams (AppSource).</span><span class="sxs-lookup"><span data-stu-id="f89a1-111">You also can an app for a specific meeting directly from the Teams store (AppSource).</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="f89a1-112">Agregar antes de una reunión</span><span class="sxs-lookup"><span data-stu-id="f89a1-112">Add before a meeting</span></span>

<span data-ttu-id="f89a1-113">Antes de una reunión, los detalles de la reunión seleccionan **Agregar una pestaña +** para abrir el control flotante de la aplicación y buscar aplicaciones optimizadas para las reuniones.</span><span class="sxs-lookup"><span data-stu-id="f89a1-113">Before a meeting, the meeting details select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="Ejemplo se muestra cómo agregar una extensión de reunión antes de una reunión." border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="f89a1-115">Agregar durante una reunión</span><span class="sxs-lookup"><span data-stu-id="f89a1-115">Add during a meeting</span></span>

En una reunión, seleccione **más** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **Agregar una aplicación** y elija la aplicación que desee.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="Ejemplo se muestra cómo agregar una extensión de reunión durante una reunión." border="false":::

## <a name="before-a-meeting"></a><span data-ttu-id="f89a1-118">Antes de una reunión</span><span class="sxs-lookup"><span data-stu-id="f89a1-118">Before a meeting</span></span>

<span data-ttu-id="f89a1-119">Antes de la reunión, puede agregar contenido en la pestaña. En el ejemplo siguiente se muestra un borrador de una pregunta de encuesta que las personas responderán durante la llamada.</span><span class="sxs-lookup"><span data-stu-id="f89a1-119">Prior to your meeting, you can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="En el ejemplo se muestra cómo se muestra el contenido de la aplicación en los detalles de la reunión antes de una llamada." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="f89a1-121">Anatomía: pestaña reunión (antes y después de las reuniones)</span><span class="sxs-lookup"><span data-stu-id="f89a1-121">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="Ejemplo muestra la anatomía estructural de una pestaña de reunión antes y después de una reunión." border="false":::

|<span data-ttu-id="f89a1-123">Counter</span><span class="sxs-lookup"><span data-stu-id="f89a1-123">Counter</span></span>|<span data-ttu-id="f89a1-124">Descripción</span><span class="sxs-lookup"><span data-stu-id="f89a1-124">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="f89a1-125">1</span><span class="sxs-lookup"><span data-stu-id="f89a1-125">1</span></span>|<span data-ttu-id="f89a1-126">**Nombre de ficha**: etiqueta de navegación de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="f89a1-126">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="f89a1-127">2 </span><span class="sxs-lookup"><span data-stu-id="f89a1-127">2</span></span>|<span data-ttu-id="f89a1-128">**Desbordamiento de tabulación**: abre acciones de pestaña, como cambiar nombre y quitar.</span><span class="sxs-lookup"><span data-stu-id="f89a1-128">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="f89a1-129">3 </span><span class="sxs-lookup"><span data-stu-id="f89a1-129">3</span></span>|<span data-ttu-id="f89a1-130">**iframe**: muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f89a1-130">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="f89a1-131">Diseño con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="f89a1-131">Designing with UI templates</span></span>

<span data-ttu-id="f89a1-132">Use una de las siguientes plantillas de interfaz de usuario de Microsoft Teams para ayudar a diseñar la pestaña de la reunión:</span><span class="sxs-lookup"><span data-stu-id="f89a1-132">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="f89a1-133">[List](../../concepts/design/design-teams-app-ui-templates.md#list): lists puede mostrar elementos relacionados en un formato que se pueda analizar y permitir que los usuarios realicen acciones en una lista completa o en elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="f89a1-133">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="f89a1-134">[Panel de tareas](../../concepts/design/design-teams-app-ui-templates.md#task-board): un panel de tareas, a veces denominado tablero Kanban o carriles de nadar, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o vales.</span><span class="sxs-lookup"><span data-stu-id="f89a1-134">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="f89a1-135">[Panel](../../concepts/design/design-teams-app-ui-templates.md#dashboard): un panel es un lienzo que contiene varias tarjetas que proporcionan información general sobre datos o contenido.</span><span class="sxs-lookup"><span data-stu-id="f89a1-135">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="f89a1-136">[Formulario](../../concepts/design/design-teams-app-ui-templates.md#form): los formularios son para recopilar, validar y enviar entradas de usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="f89a1-136">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="f89a1-137">[Estado vacío](../../concepts/design/design-teams-app-ui-templates.md#empty-state): la plantilla de estado vacía se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error, etc.</span><span class="sxs-lookup"><span data-stu-id="f89a1-137">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="f89a1-138">Panel de [navegación izquierdo](../../concepts/design/design-teams-app-ui-templates.md#left-nav): la plantilla de navegación izquierda puede servir de ayuda si la pestaña requiere la navegación.</span><span class="sxs-lookup"><span data-stu-id="f89a1-138">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="f89a1-139">En general, debe mantener al mínimo la navegación por tabulaciones.</span><span class="sxs-lookup"><span data-stu-id="f89a1-139">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="f89a1-140">Usar una pestaña en la reunión</span><span class="sxs-lookup"><span data-stu-id="f89a1-140">Use an in-meeting tab</span></span>

<span data-ttu-id="f89a1-141">La pestaña en reunión es un lienzo para aumentar la colaboración durante las reuniones.</span><span class="sxs-lookup"><span data-stu-id="f89a1-141">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="f89a1-142">Los asistentes pueden ver e interactuar con el contenido de la aplicación en un espacio dedicado fuera de la fase de reunión a través de vistas compartidas o basadas en roles.</span><span class="sxs-lookup"><span data-stu-id="f89a1-142">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="f89a1-143">Casos de uso</span><span class="sxs-lookup"><span data-stu-id="f89a1-143">Use cases</span></span>

<span data-ttu-id="f89a1-144">Los usuarios pueden usar la ficha en la reunión para:</span><span class="sxs-lookup"><span data-stu-id="f89a1-144">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="f89a1-145">Proporcionar comentarios detallados (por ejemplo, evaluar un candidato de trabajo)</span><span class="sxs-lookup"><span data-stu-id="f89a1-145">Provide detailed feedback (for example, evaluate a job candidate)</span></span>
* <span data-ttu-id="f89a1-146">Crear rápidamente un sondeo, una encuesta o un elemento de tarea para los participantes de la reunión</span><span class="sxs-lookup"><span data-stu-id="f89a1-146">Quickly create a poll, survey, or task item for the meeting participants</span></span>
* <span data-ttu-id="f89a1-147">Mostrar notas relevantes para la reunión (por ejemplo, información sobre un responsable de ventas)</span><span class="sxs-lookup"><span data-stu-id="f89a1-147">Display notes relevant to the meeting (for example, information about a sales lead)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="Ejemplo muestra cómo puede presentar el contenido de sondeo en una pestaña en la reunión." border="false":::

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="f89a1-149">Anatomía: ficha en la reunión</span><span class="sxs-lookup"><span data-stu-id="f89a1-149">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="Ejemplo muestra la anatomía estructural de una pestaña en reunión." border="false":::

|<span data-ttu-id="f89a1-151">Counter</span><span class="sxs-lookup"><span data-stu-id="f89a1-151">Counter</span></span>|<span data-ttu-id="f89a1-152">Descripción</span><span class="sxs-lookup"><span data-stu-id="f89a1-152">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="f89a1-153">1</span><span class="sxs-lookup"><span data-stu-id="f89a1-153">1</span></span>|<span data-ttu-id="f89a1-154">**Icono de la aplicación (seleccionado)**: logotipo de aplicación transparente de 16 píxeles.</span><span class="sxs-lookup"><span data-stu-id="f89a1-154">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="f89a1-155">2 </span><span class="sxs-lookup"><span data-stu-id="f89a1-155">2</span></span>|<span data-ttu-id="f89a1-156">**Nombre de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="f89a1-156">**App name**</span></span>|
|<span data-ttu-id="f89a1-157">3 </span><span class="sxs-lookup"><span data-stu-id="f89a1-157">3</span></span>|<span data-ttu-id="f89a1-158">**Header**: incluye el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f89a1-158">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="f89a1-159">4 </span><span class="sxs-lookup"><span data-stu-id="f89a1-159">4</span></span>|<span data-ttu-id="f89a1-160">**Botón Cerrar**: descarta la pestaña. Use siempre el icono de cierre superior derecho en lugar de una acción en el pie de página.</span><span class="sxs-lookup"><span data-stu-id="f89a1-160">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="f89a1-161">5 </span><span class="sxs-lookup"><span data-stu-id="f89a1-161">5</span></span>|<span data-ttu-id="f89a1-162">**Barra de notificación**: las alertas de error se muestran directamente debajo del encabezado y disminuyen el contenido de iframe en 20 píxeles.</span><span class="sxs-lookup"><span data-stu-id="f89a1-162">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="f89a1-163">6 </span><span class="sxs-lookup"><span data-stu-id="f89a1-163">6</span></span>|<span data-ttu-id="f89a1-164">**iframe**: muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f89a1-164">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="f89a1-165">Spacing</span><span class="sxs-lookup"><span data-stu-id="f89a1-165">Spacing</span></span>

<span data-ttu-id="f89a1-166">Optimice la ficha en reunión para ajustar la periferia a la periferia dentro del área iframe de 280 píxeles de ancho.</span><span class="sxs-lookup"><span data-stu-id="f89a1-166">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="f89a1-167">Hay 20 píxeles de relleno a los lados izquierdo y derecho del iframe y entre el encabezado de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="f89a1-167">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="f89a1-168">El iframe es con sangrado completo en la parte inferior de la ficha.</span><span class="sxs-lookup"><span data-stu-id="f89a1-168">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="Ejemplo muestra las dimensiones del espacio de la pestaña en la reunión." border="false":::

### <a name="scrolling"></a><span data-ttu-id="f89a1-170">Desplazamiento</span><span class="sxs-lookup"><span data-stu-id="f89a1-170">Scrolling</span></span>

<span data-ttu-id="f89a1-171">El contenido de iframe debe desplazarse verticalmente.</span><span class="sxs-lookup"><span data-stu-id="f89a1-171">Iframe contents should scroll vertically.</span></span> <span data-ttu-id="f89a1-172">Solo puede ver el contenido al que se ha desplazado (nada anterior o posterior).</span><span class="sxs-lookup"><span data-stu-id="f89a1-172">You can only see the content you've scrolled to (nothing above or below).</span></span> <span data-ttu-id="f89a1-173">La barra de desplazamiento es parte del contenido iframe.</span><span class="sxs-lookup"><span data-stu-id="f89a1-173">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="Ejemplo muestra cómo se desplaza la pestaña en reunión." border="false":::

### <a name="navigation"></a><span data-ttu-id="f89a1-175">Navegación</span><span class="sxs-lookup"><span data-stu-id="f89a1-175">Navigation</span></span>

<span data-ttu-id="f89a1-176">Para los escenarios con capas de navegación o contenido pesado, se recomienda permitir que los usuarios naveguen a una capa secundaria.</span><span class="sxs-lookup"><span data-stu-id="f89a1-176">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="f89a1-177">Los usuarios deben poder volver a la capa anterior.</span><span class="sxs-lookup"><span data-stu-id="f89a1-177">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="Ejemplo muestra la navegación en reuniones." border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="f89a1-179">Usar un cuadro de diálogo en la reunión</span><span class="sxs-lookup"><span data-stu-id="f89a1-179">Use an in-meeting dialog</span></span>

<span data-ttu-id="f89a1-180">Los cuadros de diálogo en la reunión se muestran en la fase de reunión de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="f89a1-180">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="f89a1-181">Requieren la atención, la confirmación o la interacción del usuario, pero son sutiles y no interrumpen la reunión.</span><span class="sxs-lookup"><span data-stu-id="f89a1-181">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="f89a1-182">Debe usarlos con moderación y para escenarios claros y orientados a tareas.</span><span class="sxs-lookup"><span data-stu-id="f89a1-182">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="f89a1-183">Casos de uso</span><span class="sxs-lookup"><span data-stu-id="f89a1-183">Use cases</span></span>

<span data-ttu-id="f89a1-184">Los cuadros de diálogo en la reunión son desencadenados por un usuario (como el organizador de la reunión) que puede desear a los participantes:</span><span class="sxs-lookup"><span data-stu-id="f89a1-184">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="f89a1-185">Proporcionar comentarios breves</span><span class="sxs-lookup"><span data-stu-id="f89a1-185">Provide brief feedback</span></span>
* <span data-ttu-id="f89a1-186">Realizar una breve encuesta o sondeo</span><span class="sxs-lookup"><span data-stu-id="f89a1-186">Take a short survey or poll</span></span>
* <span data-ttu-id="f89a1-187">Enviar aprobaciones</span><span class="sxs-lookup"><span data-stu-id="f89a1-187">Submit approvals</span></span>
* <span data-ttu-id="f89a1-188">Recibir recordatorios</span><span class="sxs-lookup"><span data-stu-id="f89a1-188">Get reminders</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="Ejemplo se muestra cómo se puede usar un cuadro de diálogo en la reunión." border="false":::

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="f89a1-190">Anatomía: cuadro de diálogo en la reunión</span><span class="sxs-lookup"><span data-stu-id="f89a1-190">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="Ejemplo muestra la anatomía estructural de un cuadro de diálogo en la reunión." border="false":::

|<span data-ttu-id="f89a1-192">Counter</span><span class="sxs-lookup"><span data-stu-id="f89a1-192">Counter</span></span>|<span data-ttu-id="f89a1-193">Descripción</span><span class="sxs-lookup"><span data-stu-id="f89a1-193">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="f89a1-194">1</span><span class="sxs-lookup"><span data-stu-id="f89a1-194">1</span></span>|<span data-ttu-id="f89a1-195">**Header**: incluye el icono de la aplicación, el nombre, la cadena de acción y el icono de cierre.</span><span class="sxs-lookup"><span data-stu-id="f89a1-195">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="f89a1-196">2 </span><span class="sxs-lookup"><span data-stu-id="f89a1-196">2</span></span>|<span data-ttu-id="f89a1-197">**iframe**: muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f89a1-197">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="f89a1-198">Anatomía: encabezado de cuadro de diálogo en la reunión</span><span class="sxs-lookup"><span data-stu-id="f89a1-198">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="Ejemplo muestra la anatomía estructural de un encabezado de cuadro de diálogo en reunión." border="false":::

<span data-ttu-id="f89a1-200">Hay dos variantes de encabezado.</span><span class="sxs-lookup"><span data-stu-id="f89a1-200">There are two header variants.</span></span> <span data-ttu-id="f89a1-201">Si es posible, use la variante con el avatar para reforzar que el cuadro de diálogo procede de una persona.</span><span class="sxs-lookup"><span data-stu-id="f89a1-201">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="f89a1-202">Counter</span><span class="sxs-lookup"><span data-stu-id="f89a1-202">Counter</span></span>|<span data-ttu-id="f89a1-203">Descripción</span><span class="sxs-lookup"><span data-stu-id="f89a1-203">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="f89a1-204">1</span><span class="sxs-lookup"><span data-stu-id="f89a1-204">1</span></span>|<span data-ttu-id="f89a1-205">**Avatar**: persona que inicia el cuadro de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="f89a1-205">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="f89a1-206">2 </span><span class="sxs-lookup"><span data-stu-id="f89a1-206">2</span></span>|<span data-ttu-id="f89a1-207">**Icono de aplicación**</span><span class="sxs-lookup"><span data-stu-id="f89a1-207">**App icon**</span></span>|
|<span data-ttu-id="f89a1-208">3 </span><span class="sxs-lookup"><span data-stu-id="f89a1-208">3</span></span>|<span data-ttu-id="f89a1-209">**Nombre de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="f89a1-209">**App name**</span></span>|
|<span data-ttu-id="f89a1-210">4 </span><span class="sxs-lookup"><span data-stu-id="f89a1-210">4</span></span>|<span data-ttu-id="f89a1-211">**Botón Cerrar**: descarta el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f89a1-211">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="f89a1-212">5 </span><span class="sxs-lookup"><span data-stu-id="f89a1-212">5</span></span>|<span data-ttu-id="f89a1-213">**Cadena de acción**: normalmente describe quién inició el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f89a1-213">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior"></a><span data-ttu-id="f89a1-214">Comportamiento dinámico</span><span class="sxs-lookup"><span data-stu-id="f89a1-214">Responsive behavior</span></span>

<span data-ttu-id="f89a1-215">Los cuadros de diálogo en la reunión pueden variar en tamaño para tener en cuenta los distintos escenarios.</span><span class="sxs-lookup"><span data-stu-id="f89a1-215">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="f89a1-216">Asegúrese de mantener el relleno y los tamaños de los componentes.</span><span class="sxs-lookup"><span data-stu-id="f89a1-216">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="f89a1-217">**Width**: el ancho del iframe es un valor absoluto dentro del intervalo especificado.</span><span class="sxs-lookup"><span data-stu-id="f89a1-217">**Width**: The iframe width is an absolute value within the range you specify.</span></span>
* <span data-ttu-id="f89a1-218">**Height**: el alto del cuadro de diálogo viene determinado por el contenido en el iframe.</span><span class="sxs-lookup"><span data-stu-id="f89a1-218">**Height**: The height of the dialog is determined by the content in the iframe.</span></span> <span data-ttu-id="f89a1-219">El desplazamiento vertical toma el control del contenido que supera el alto máximo.</span><span class="sxs-lookup"><span data-stu-id="f89a1-219">Vertical scroll takes over for content that exceeds the maximum height.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="Ejemplo muestra el cuadro de diálogo en la reunión. Width: min--280 píxeles (248 píxeles iframe). Max--460 píxeles (428 píxeles iframe). Altura: 300 píxeles (iframe)." border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="f89a1-221">Después de una reunión</span><span class="sxs-lookup"><span data-stu-id="f89a1-221">After a meeting</span></span>

<span data-ttu-id="f89a1-222">Puede volver a una reunión después de finalizar y ver el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f89a1-222">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="f89a1-223">En este ejemplo, el organizador de la reunión puede mirar los resultados del sondeo en la pestaña **contoso** . (Nota: desde el punto de vista del diseño, no hay ninguna diferencia entre la experiencia de pestañas previa y posterior a la reunión).</span><span class="sxs-lookup"><span data-stu-id="f89a1-223">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="Ejemplo muestra una pestaña posterior a la reunión." border="false":::

## <a name="best-practices"></a><span data-ttu-id="f89a1-225">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="f89a1-225">Best practices</span></span>

### <a name="interactions"></a><span data-ttu-id="f89a1-226">Existentes</span><span class="sxs-lookup"><span data-stu-id="f89a1-226">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="f89a1-228">Do: limitar el número de interacciones</span><span class="sxs-lookup"><span data-stu-id="f89a1-228">Do: Limit the number of interactions</span></span>

<span data-ttu-id="f89a1-229">Para los cuadros de diálogo en la reunión, quite el contenido innecesario que no ayude a los usuarios a realizar algo rápidamente.</span><span class="sxs-lookup"><span data-stu-id="f89a1-229">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="f89a1-231">No: introducir elementos innecesarios</span><span class="sxs-lookup"><span data-stu-id="f89a1-231">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="f89a1-232">Un único cuadro de diálogo en reunión con varias interacciones puede distraerse de la llamada.</span><span class="sxs-lookup"><span data-stu-id="f89a1-232">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="f89a1-233">Diseño</span><span class="sxs-lookup"><span data-stu-id="f89a1-233">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="do-use-single-column-layouts"></a><span data-ttu-id="f89a1-235">Do: usar diseños de columna única</span><span class="sxs-lookup"><span data-stu-id="f89a1-235">Do: Use single-column layouts</span></span>

<span data-ttu-id="f89a1-236">Como los cuadros de diálogo están en el centro de la fase de reunión, la finalización de la tarea debería ser rápida y sencilla para evitar la frustración del usuario.</span><span class="sxs-lookup"><span data-stu-id="f89a1-236">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="f89a1-238">No: desorden el espacio</span><span class="sxs-lookup"><span data-stu-id="f89a1-238">Don't: Clutter the space</span></span>

<span data-ttu-id="f89a1-239">Un contenido denso o con gran estructura puede ser molesto y abrumador, especialmente durante una reunión.</span><span class="sxs-lookup"><span data-stu-id="f89a1-239">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="do-use-single-columns"></a><span data-ttu-id="f89a1-241">Do: usar columnas únicas</span><span class="sxs-lookup"><span data-stu-id="f89a1-241">Do: Use single columns</span></span>

<span data-ttu-id="f89a1-242">Dada la naturaleza estrecha de las pestañas de la reunión, se recomienda encarecidamente mostrar el contenido en una sola columna.</span><span class="sxs-lookup"><span data-stu-id="f89a1-242">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="f89a1-244">No: usar varias columnas</span><span class="sxs-lookup"><span data-stu-id="f89a1-244">Don't: Use multiple columns</span></span>

<span data-ttu-id="f89a1-245">Debido al espacio limitado de la pestaña en reunión, no se recomiendan los diseños con más de una columna.</span><span class="sxs-lookup"><span data-stu-id="f89a1-245">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="f89a1-246">Controles</span><span class="sxs-lookup"><span data-stu-id="f89a1-246">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="f89a1-248">Haga lo siguiente: alinear a la derecha la acción principal</span><span class="sxs-lookup"><span data-stu-id="f89a1-248">Do: Right align the primary action</span></span>

<span data-ttu-id="f89a1-249">Le recomendamos que positioining la acción más intensa para la ubicación más a la derecha.</span><span class="sxs-lookup"><span data-stu-id="f89a1-249">We recommend positioining the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="f89a1-251">No: acciones alineadas a la izquierda o al centro</span><span class="sxs-lookup"><span data-stu-id="f89a1-251">Don't: Left or center align actions</span></span>

<span data-ttu-id="f89a1-252">Esto se desvía del patrón de equipos estándar para la colocación de controles en un cuadro de diálogo y puede entrar en conflicto con un cuadro de diálogo detrás de uno superior.</span><span class="sxs-lookup"><span data-stu-id="f89a1-252">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scroll"></a><span data-ttu-id="f89a1-253">Scroll</span><span class="sxs-lookup"><span data-stu-id="f89a1-253">Scroll</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="f89a1-255">Hacer: desplazarse verticalmente</span><span class="sxs-lookup"><span data-stu-id="f89a1-255">Do: Scroll vertically</span></span>

<span data-ttu-id="f89a1-256">Le recomendamos que sitúe la acción más intensa visualmente en la posición más a la derecha.</span><span class="sxs-lookup"><span data-stu-id="f89a1-256">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="f89a1-258">No: desplazar horizontalmente</span><span class="sxs-lookup"><span data-stu-id="f89a1-258">Don't: Scroll horizontally</span></span>

<span data-ttu-id="f89a1-259">El desplazamiento horizontal no es un comportamiento esperado en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="f89a1-259">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="f89a1-260">Otros lienzos del entorno de la reunión se desplazan verticalmente.</span><span class="sxs-lookup"><span data-stu-id="f89a1-260">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="f89a1-261">Flujos de trabajo</span><span class="sxs-lookup"><span data-stu-id="f89a1-261">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="f89a1-263">Do: escenarios complejos de Surface en la pestaña en la reunión</span><span class="sxs-lookup"><span data-stu-id="f89a1-263">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="f89a1-264">Si la aplicación incluye varias tareas, se recomienda encarecidamente un diseño de una sola columna en una pestaña en la reunión.</span><span class="sxs-lookup"><span data-stu-id="f89a1-264">If your app includes multiple tasks, we strongly recommend a single-column layout in an in-meeting tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="dont-package-complex-scenarios-in-the-in-meeting-dialog"></a><span data-ttu-id="f89a1-266">No: empaquetar escenarios complejos en el cuadro de diálogo de la reunión</span><span class="sxs-lookup"><span data-stu-id="f89a1-266">Don't: Package complex scenarios in the in-meeting dialog</span></span>

<span data-ttu-id="f89a1-267">Los diálogos en la reunión están pensados para interacciones breves.</span><span class="sxs-lookup"><span data-stu-id="f89a1-267">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="f89a1-268">Creación de temas</span><span class="sxs-lookup"><span data-stu-id="f89a1-268">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="do-use-teams-color-tokens"></a><span data-ttu-id="f89a1-270">Do: usar tokens de color de Teams</span><span class="sxs-lookup"><span data-stu-id="f89a1-270">Do: Use Teams color tokens</span></span>

<span data-ttu-id="f89a1-271">Las reuniones de Microsoft Teams están optimizadas para el modo oscuro para ayudar a reducir el ruido visual y cognitivo para que los usuarios puedan centrarse en la discusión y en el contenido compartido.</span><span class="sxs-lookup"><span data-stu-id="f89a1-271">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="f89a1-272">Obtenga información sobre cómo usar <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">tokens de color (interfaz de usuario de Fluent)</a>.</span><span class="sxs-lookup"><span data-stu-id="f89a1-272">Learn about using <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a>.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="f89a1-274">No: incluir otro botón descartar</span><span class="sxs-lookup"><span data-stu-id="f89a1-274">Don't: Include another dismiss button</span></span>

<span data-ttu-id="f89a1-275">Ofrecer una opción para cerrar el contenido de la pestaña en la reunión puede causar problemas porque ya hay un botón en el encabezado para descartar la misma pestaña en la reunión.</span><span class="sxs-lookup"><span data-stu-id="f89a1-275">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="f89a1-276">Navegación</span><span class="sxs-lookup"><span data-stu-id="f89a1-276">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="f89a1-278">Do: tener un botón atrás</span><span class="sxs-lookup"><span data-stu-id="f89a1-278">Do: Have a back button</span></span>

<span data-ttu-id="f89a1-279">Si tiene más de una capa de navegación en una pestaña en la reunión, los usuarios deben poder volver a sus vistas anteriores.</span><span class="sxs-lookup"><span data-stu-id="f89a1-279">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="f89a1-281">No: incluir otro botón descartar</span><span class="sxs-lookup"><span data-stu-id="f89a1-281">Don't: Include another dismiss button</span></span>

<span data-ttu-id="f89a1-282">Ofrecer una opción para cerrar el contenido de la pestaña en la reunión puede causar problemas porque ya hay un botón en el encabezado para descartar la misma pestaña en la reunión.</span><span class="sxs-lookup"><span data-stu-id="f89a1-282">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="f89a1-284">PRECAUCIÓN: Evite los modales en la pestaña en la reunión.</span><span class="sxs-lookup"><span data-stu-id="f89a1-284">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="f89a1-285">Los modales (también conocidos como módulos de tareas) en la ficha in-Meeting ya estrecha pueden ajustar y oscurecer el contenido.</span><span class="sxs-lookup"><span data-stu-id="f89a1-285">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a><span data-ttu-id="f89a1-286">Validar el diseño</span><span class="sxs-lookup"><span data-stu-id="f89a1-286">Validate your design</span></span>

<span data-ttu-id="f89a1-287">Si planea publicar la aplicación en AppSource, debe comprender los problemas de diseño que suelen hacer que las aplicaciones fallen durante el envío.</span><span class="sxs-lookup"><span data-stu-id="f89a1-287">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f89a1-288">Comprobar las instrucciones de validación del diseño</span><span class="sxs-lookup"><span data-stu-id="f89a1-288">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)

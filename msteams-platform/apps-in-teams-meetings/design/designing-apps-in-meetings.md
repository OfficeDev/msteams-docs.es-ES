---
title: Diseño de la extensión de la reunión
author: heath-hamilton
description: Obtenga información sobre cómo diseñar aplicaciones en reuniones de Teams y obtener el kit de interfaz de usuario de Microsoft Teams.
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: c6e76356b698da4e32e279b0842ab2cc35254e99
ms.sourcegitcommit: 84f408aa2854aa7a5cefaa66ce9a373b19e0864a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2021
ms.locfileid: "49886761"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="1cd6a-103">Diseño de la extensión de reunión de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1cd6a-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="1cd6a-104">Puede crear aplicaciones para que las reuniones sean más productivas.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="1cd6a-105">Por ejemplo, pida a los usuarios que completen una encuesta durante una llamada o que envíen un aviso rápido que no interrumpa el flujo de la reunión.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="1cd6a-106">Kit de interfaz de usuario de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1cd6a-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="1cd6a-107">Puede encontrar instrucciones de diseño más completas, incluidos los elementos que puede tomar y modificar según sea necesario, en el Kit de interfaz de usuario de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1cd6a-108">Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="1cd6a-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="1cd6a-109">Agregar una extensión de reunión</span><span class="sxs-lookup"><span data-stu-id="1cd6a-109">Add a meeting extension</span></span>

<span data-ttu-id="1cd6a-110">Puede agregar una extensión de reunión antes y durante las reuniones.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-110">You can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="1cd6a-111">También puede agregar una aplicación para una reunión específica directamente desde la tienda de Teams (AppSource).</span><span class="sxs-lookup"><span data-stu-id="1cd6a-111">You also can add an app for a specific meeting directly from the Teams store (AppSource).</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="1cd6a-112">Agregar antes de una reunión</span><span class="sxs-lookup"><span data-stu-id="1cd6a-112">Add before a meeting</span></span>

<span data-ttu-id="1cd6a-113">En los detalles de la reunión, seleccione **Agregar una pestaña + para** abrir el control desplegable de la aplicación y buscar aplicaciones optimizadas para reuniones.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-113">In the meeting details, select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de reunión antes de una reunión." border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="1cd6a-115">Agregar durante una reunión</span><span class="sxs-lookup"><span data-stu-id="1cd6a-115">Add during a meeting</span></span>

En una reunión, seleccione **Más** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **agregar una aplicación** y elija la aplicación que desee.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de reunión durante una reunión." border="false":::

## <a name="before-a-meeting"></a><span data-ttu-id="1cd6a-118">Antes de una reunión</span><span class="sxs-lookup"><span data-stu-id="1cd6a-118">Before a meeting</span></span>

<span data-ttu-id="1cd6a-119">Antes de la reunión, puede agregar contenido en la pestaña. En el siguiente ejemplo se muestra un borrador de pregunta de encuesta que los usuarios responderán durante la llamada.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-119">Prior to your meeting, you can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="En el ejemplo se muestra cómo usar el contenido de la aplicación en los detalles de la reunión antes de una llamada." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="1cd6a-121">Anatomía: pestaña Reunión (antes y después de las reuniones)</span><span class="sxs-lookup"><span data-stu-id="1cd6a-121">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de una pestaña de reunión antes y después de una reunión." border="false":::

|<span data-ttu-id="1cd6a-123">Counter</span><span class="sxs-lookup"><span data-stu-id="1cd6a-123">Counter</span></span>|<span data-ttu-id="1cd6a-124">Descripción</span><span class="sxs-lookup"><span data-stu-id="1cd6a-124">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="1cd6a-125">1</span><span class="sxs-lookup"><span data-stu-id="1cd6a-125">1</span></span>|<span data-ttu-id="1cd6a-126">**Nombre de la pestaña:** etiqueta de navegación de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-126">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="1cd6a-127">2 </span><span class="sxs-lookup"><span data-stu-id="1cd6a-127">2</span></span>|<span data-ttu-id="1cd6a-128">**Desbordamiento de pestaña:** abre acciones de pestaña, como cambiar el nombre y quitar.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-128">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="1cd6a-129">3</span><span class="sxs-lookup"><span data-stu-id="1cd6a-129">3</span></span>|<span data-ttu-id="1cd6a-130">**iframe:** muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-130">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="1cd6a-131">Diseño con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="1cd6a-131">Designing with UI templates</span></span>

<span data-ttu-id="1cd6a-132">Use una de las siguientes plantillas de interfaz de usuario de Teams para ayudar a diseñar la pestaña de reunión:</span><span class="sxs-lookup"><span data-stu-id="1cd6a-132">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="1cd6a-133">[Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato digitalizado y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-133">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="1cd6a-134">[Panel de](../../concepts/design/design-teams-app-ui-templates.md#task-board)tareas: un panel de tareas, a veces denominado tablero de kanban o pistas de nado, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o vales.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-134">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="1cd6a-135">[Panel:](../../concepts/design/design-teams-app-ui-templates.md#dashboard)un panel es un lienzo que contiene varias tarjetas que proporcionan información general sobre datos o contenido.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-135">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="1cd6a-136">[Formulario:](../../concepts/design/design-teams-app-ui-templates.md#form)los formularios son para recopilar, validar y enviar entradas de usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-136">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="1cd6a-137">[Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacía se puede usar para muchos escenarios, incluido el inicio de sesión, experiencias de primera ejecución, mensajes de error y mucho más.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-137">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="1cd6a-138">[Navegación izquierda:](../../concepts/design/design-teams-app-ui-templates.md#left-nav)la plantilla de navegación izquierda puede ayudar si la pestaña requiere cierta navegación.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-138">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="1cd6a-139">En general, debes mantener la navegación mediante tabulación al mínimo.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-139">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="1cd6a-140">Usar una pestaña en la reunión</span><span class="sxs-lookup"><span data-stu-id="1cd6a-140">Use an in-meeting tab</span></span>

<span data-ttu-id="1cd6a-141">La pestaña en la reunión es un lienzo para aumentar la colaboración durante las reuniones.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-141">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="1cd6a-142">Los asistentes pueden ver e interactuar con el contenido de la aplicación en un espacio dedicado fuera de la fase de reunión a través de vistas compartidas o basadas en roles.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-142">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="1cd6a-143">Casos de uso</span><span class="sxs-lookup"><span data-stu-id="1cd6a-143">Use cases</span></span>

<span data-ttu-id="1cd6a-144">Los usuarios pueden usar la pestaña en la reunión para:</span><span class="sxs-lookup"><span data-stu-id="1cd6a-144">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="1cd6a-145">Proporcionar comentarios detallados (por ejemplo, evaluar un candidato de trabajo)</span><span class="sxs-lookup"><span data-stu-id="1cd6a-145">Provide detailed feedback (for example, evaluate a job candidate)</span></span>
* <span data-ttu-id="1cd6a-146">Crear rápidamente un sondeo, una encuesta o un elemento de tarea para los participantes de la reunión</span><span class="sxs-lookup"><span data-stu-id="1cd6a-146">Quickly create a poll, survey, or task item for the meeting participants</span></span>
* <span data-ttu-id="1cd6a-147">Mostrar notas relevantes para la reunión (por ejemplo, información sobre un responsable de ventas)</span><span class="sxs-lookup"><span data-stu-id="1cd6a-147">Display notes relevant to the meeting (for example, information about a sales lead)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="En el ejemplo se muestra cómo presentar contenido de sondeo en una pestaña de reunión." border="false":::

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="1cd6a-149">Anatomía: pestaña En la reunión</span><span class="sxs-lookup"><span data-stu-id="1cd6a-149">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de una pestaña en reunión." border="false":::

|<span data-ttu-id="1cd6a-151">Counter</span><span class="sxs-lookup"><span data-stu-id="1cd6a-151">Counter</span></span>|<span data-ttu-id="1cd6a-152">Descripción</span><span class="sxs-lookup"><span data-stu-id="1cd6a-152">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="1cd6a-153">1</span><span class="sxs-lookup"><span data-stu-id="1cd6a-153">1</span></span>|<span data-ttu-id="1cd6a-154">**Icono de aplicación (seleccionado):** logotipo de aplicación transparente de 16 píxeles.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-154">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="1cd6a-155">2 </span><span class="sxs-lookup"><span data-stu-id="1cd6a-155">2</span></span>|<span data-ttu-id="1cd6a-156">**Nombre de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="1cd6a-156">**App name**</span></span>|
|<span data-ttu-id="1cd6a-157">3</span><span class="sxs-lookup"><span data-stu-id="1cd6a-157">3</span></span>|<span data-ttu-id="1cd6a-158">**Encabezado:** incluye el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-158">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="1cd6a-159">4 </span><span class="sxs-lookup"><span data-stu-id="1cd6a-159">4</span></span>|<span data-ttu-id="1cd6a-160">**Botón Cerrar:** descarta la pestaña. Use siempre el icono de cierre superior derecho en lugar de una acción en el pie de página.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-160">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="1cd6a-161">5 </span><span class="sxs-lookup"><span data-stu-id="1cd6a-161">5</span></span>|<span data-ttu-id="1cd6a-162">**Barra de notificación:** las alertas de error se muestran directamente debajo del encabezado e insertan el contenido del iframe hacia abajo 20 píxeles.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-162">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="1cd6a-163">6 </span><span class="sxs-lookup"><span data-stu-id="1cd6a-163">6</span></span>|<span data-ttu-id="1cd6a-164">**iframe:** muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-164">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="1cd6a-165">Spacing</span><span class="sxs-lookup"><span data-stu-id="1cd6a-165">Spacing</span></span>

<span data-ttu-id="1cd6a-166">Optimiza la pestaña de la reunión para que se ajuste de un extremo a otro dentro del área de iframe de 280 píxeles.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-166">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="1cd6a-167">Hay 20 píxeles de espaciado interno en los lados izquierdo y derecho del iframe y entre el encabezado de pestaña.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-167">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="1cd6a-168">El iframe está a sangre completa en la parte inferior de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-168">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="En el ejemplo se muestran las dimensiones de espaciado de tabulación en reuniones." border="false":::

### <a name="scrolling"></a><span data-ttu-id="1cd6a-170">Desplazamiento</span><span class="sxs-lookup"><span data-stu-id="1cd6a-170">Scrolling</span></span>

<span data-ttu-id="1cd6a-171">El contenido del Iframe debe desplazarse verticalmente.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-171">Iframe contents should scroll vertically.</span></span> <span data-ttu-id="1cd6a-172">Solo puede ver el contenido al que se desplazó (nada por encima o por debajo).</span><span class="sxs-lookup"><span data-stu-id="1cd6a-172">You can only see the content you've scrolled to (nothing above or below).</span></span> <span data-ttu-id="1cd6a-173">La barra de desplazamiento forma parte del contenido del iframe.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-173">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="En el ejemplo se muestra cómo se desplaza la pestaña en la reunión." border="false":::

### <a name="navigation"></a><span data-ttu-id="1cd6a-175">Navegación</span><span class="sxs-lookup"><span data-stu-id="1cd6a-175">Navigation</span></span>

<span data-ttu-id="1cd6a-176">Para escenarios con capas de navegación o contenido intenso, se recomienda permitir a los usuarios navegar a una capa secundaria.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-176">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="1cd6a-177">Los usuarios deben poder volver a la capa anterior.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-177">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="En el ejemplo se muestra la navegación en la reunión." border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="1cd6a-179">Usar un cuadro de diálogo en la reunión</span><span class="sxs-lookup"><span data-stu-id="1cd6a-179">Use an in-meeting dialog</span></span>

<span data-ttu-id="1cd6a-180">Los cuadros de diálogo dentro de la reunión se muestran en la fase de reunión de Teams.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-180">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="1cd6a-181">Requieren la atención, confirmación o interacción de un usuario, pero son sutiles y no interrumpen la reunión.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-181">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="1cd6a-182">Debes usarlas con moderación y para escenarios orientados a tareas y ligeras.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-182">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="1cd6a-183">Casos de uso</span><span class="sxs-lookup"><span data-stu-id="1cd6a-183">Use cases</span></span>

<span data-ttu-id="1cd6a-184">Los cuadros de diálogo dentro de la reunión los desencadena un usuario (como el organizador de la reunión) que puede desear que los participantes:</span><span class="sxs-lookup"><span data-stu-id="1cd6a-184">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="1cd6a-185">Proporcionar comentarios breves</span><span class="sxs-lookup"><span data-stu-id="1cd6a-185">Provide brief feedback</span></span>
* <span data-ttu-id="1cd6a-186">Realizar una encuesta o sondeo breve</span><span class="sxs-lookup"><span data-stu-id="1cd6a-186">Take a short survey or poll</span></span>
* <span data-ttu-id="1cd6a-187">Enviar aprobaciones</span><span class="sxs-lookup"><span data-stu-id="1cd6a-187">Submit approvals</span></span>
* <span data-ttu-id="1cd6a-188">Recibir recordatorios</span><span class="sxs-lookup"><span data-stu-id="1cd6a-188">Get reminders</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="En el ejemplo se muestra cómo usar un cuadro de diálogo en la reunión." border="false":::

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="1cd6a-190">Anatomía: cuadro de diálogo en la reunión</span><span class="sxs-lookup"><span data-stu-id="1cd6a-190">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de un cuadro de diálogo en reunión." border="false":::

|<span data-ttu-id="1cd6a-192">Counter</span><span class="sxs-lookup"><span data-stu-id="1cd6a-192">Counter</span></span>|<span data-ttu-id="1cd6a-193">Descripción</span><span class="sxs-lookup"><span data-stu-id="1cd6a-193">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="1cd6a-194">1</span><span class="sxs-lookup"><span data-stu-id="1cd6a-194">1</span></span>|<span data-ttu-id="1cd6a-195">**Encabezado:** incluye el icono de la aplicación, el nombre, la cadena de acción y el icono de cierre.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-195">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="1cd6a-196">2 </span><span class="sxs-lookup"><span data-stu-id="1cd6a-196">2</span></span>|<span data-ttu-id="1cd6a-197">**iframe:** muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-197">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="1cd6a-198">Anatomía: encabezado del cuadro de diálogo En la reunión</span><span class="sxs-lookup"><span data-stu-id="1cd6a-198">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de un encabezado de cuadro de diálogo en reunión." border="false":::

<span data-ttu-id="1cd6a-200">Hay dos variantes de encabezado.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-200">There are two header variants.</span></span> <span data-ttu-id="1cd6a-201">Cuando sea posible, usa la variante con el avatar para reforzar que el cuadro de diálogo viene de una persona.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-201">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="1cd6a-202">Counter</span><span class="sxs-lookup"><span data-stu-id="1cd6a-202">Counter</span></span>|<span data-ttu-id="1cd6a-203">Descripción</span><span class="sxs-lookup"><span data-stu-id="1cd6a-203">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="1cd6a-204">1</span><span class="sxs-lookup"><span data-stu-id="1cd6a-204">1</span></span>|<span data-ttu-id="1cd6a-205">**Avatar:** persona que inicia el cuadro de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-205">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="1cd6a-206">2 </span><span class="sxs-lookup"><span data-stu-id="1cd6a-206">2</span></span>|<span data-ttu-id="1cd6a-207">**Icono de aplicación**</span><span class="sxs-lookup"><span data-stu-id="1cd6a-207">**App icon**</span></span>|
|<span data-ttu-id="1cd6a-208">3</span><span class="sxs-lookup"><span data-stu-id="1cd6a-208">3</span></span>|<span data-ttu-id="1cd6a-209">**Nombre de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="1cd6a-209">**App name**</span></span>|
|<span data-ttu-id="1cd6a-210">4 </span><span class="sxs-lookup"><span data-stu-id="1cd6a-210">4</span></span>|<span data-ttu-id="1cd6a-211">**Botón Cerrar:** descarta el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-211">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="1cd6a-212">5 </span><span class="sxs-lookup"><span data-stu-id="1cd6a-212">5</span></span>|<span data-ttu-id="1cd6a-213">**Cadena de acción:** normalmente describe quién inició el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-213">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior"></a><span data-ttu-id="1cd6a-214">Comportamiento dinámico</span><span class="sxs-lookup"><span data-stu-id="1cd6a-214">Responsive behavior</span></span>

<span data-ttu-id="1cd6a-215">Los cuadros de diálogo en reunión pueden variar en tamaño para tener en cuenta diferentes escenarios.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-215">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="1cd6a-216">Asegúrese de mantener el espaciado interno y los tamaños de los componentes.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-216">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="1cd6a-217">**Ancho:** el ancho del iframe es un valor absoluto dentro del intervalo especificado.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-217">**Width**: The iframe width is an absolute value within the range you specify.</span></span>
* <span data-ttu-id="1cd6a-218">**Alto:** el alto del cuadro de diálogo viene determinado por el contenido del iframe.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-218">**Height**: The height of the dialog is determined by the content in the iframe.</span></span> <span data-ttu-id="1cd6a-219">El desplazamiento vertical toma el control del contenido que supera el alto máximo.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-219">Vertical scroll takes over for content that exceeds the maximum height.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="En el ejemplo se muestra el cuadro de diálogo en la reunión. Ancho: mínimo: 280 píxeles (iframe de 248 píxeles). Máximo: 460 píxeles (iframe de 428 píxeles). Alto: 300 píxeles (iframe)." border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="1cd6a-221">Después de una reunión</span><span class="sxs-lookup"><span data-stu-id="1cd6a-221">After a meeting</span></span>

<span data-ttu-id="1cd6a-222">Puedes volver a una reunión después de que finalice y ver el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-222">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="1cd6a-223">En este ejemplo, el organizador de la reunión puede ver los resultados del sondeo en la pestaña **Contoso.** (Nota: Desde el punto de vista del diseño, no hay ninguna diferencia entre la experiencia de pestaña previa y posterior a la reunión).</span><span class="sxs-lookup"><span data-stu-id="1cd6a-223">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="En el ejemplo se muestra una pestaña posterior a la reunión." border="false":::

## <a name="best-practices"></a><span data-ttu-id="1cd6a-225">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="1cd6a-225">Best practices</span></span>

### <a name="interactions"></a><span data-ttu-id="1cd6a-226">Interacciones</span><span class="sxs-lookup"><span data-stu-id="1cd6a-226">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Ejemplo que muestra cómo limitar el número de interacciones." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="1cd6a-228">Hacer: Limitar el número de interacciones</span><span class="sxs-lookup"><span data-stu-id="1cd6a-228">Do: Limit the number of interactions</span></span>

<span data-ttu-id="1cd6a-229">Para los cuadros de diálogo en la reunión, quite el contenido innecesario que no ayude a los usuarios a lograr algo rápidamente.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-229">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Ejemplo que muestra cómo no introducir elementos innecesarios." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="1cd6a-231">No: introducir elementos innecesarios</span><span class="sxs-lookup"><span data-stu-id="1cd6a-231">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="1cd6a-232">Un solo cuadro de diálogo en la reunión con varias interacciones puede distraer la llamada.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-232">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="1cd6a-233">Diseño</span><span class="sxs-lookup"><span data-stu-id="1cd6a-233">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Ejemplo que muestra cómo debe usar un diseño de cuadro de diálogo de una sola columna." border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a><span data-ttu-id="1cd6a-235">Hacer: usar un diseño de cuadro de diálogo de una sola columna</span><span class="sxs-lookup"><span data-stu-id="1cd6a-235">Do: Use a single-column dialog layout</span></span>

<span data-ttu-id="1cd6a-236">Dado que los cuadros de diálogo están en el centro de la fase de reunión, la finalización de tareas debe ser rápida y sencilla para evitar la frustración del usuario.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-236">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Ejemplo que muestra que no debe abarrote el espacio de una extensión de reunión." border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="1cd6a-238">No: abarrote el espacio</span><span class="sxs-lookup"><span data-stu-id="1cd6a-238">Don't: Clutter the space</span></span>

<span data-ttu-id="1cd6a-239">El contenido densa o demasiado estructurado puede distraer y agobiar, especialmente durante una reunión.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-239">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Ejemplo que muestra un diseño de pestaña de una sola columna." border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a><span data-ttu-id="1cd6a-241">Hacer: usar un diseño de pestaña de una sola columna</span><span class="sxs-lookup"><span data-stu-id="1cd6a-241">Do: Use a single-column tab layout</span></span>

<span data-ttu-id="1cd6a-242">Dada la naturaleza estrecha de la pestaña en la reunión, recomendamos encarecidamente mostrar el contenido en una sola columna.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-242">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Ejemplo que muestra una pestaña con varias columnas." border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="1cd6a-244">No: Usar varias columnas</span><span class="sxs-lookup"><span data-stu-id="1cd6a-244">Don't: Use multiple columns</span></span>

<span data-ttu-id="1cd6a-245">Debido al espacio limitado de la pestaña en la reunión, no se recomiendan los diseños con más de una columna.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-245">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="1cd6a-246">Controles</span><span class="sxs-lookup"><span data-stu-id="1cd6a-246">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Ejemplo que muestra cómo alinear a la derecha los controles principales." border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="1cd6a-248">Hacer: alinear a la derecha la acción principal</span><span class="sxs-lookup"><span data-stu-id="1cd6a-248">Do: Right align the primary action</span></span>

<span data-ttu-id="1cd6a-249">Se recomienda colocar la acción más intensa visualmente en la ubicación más a la derecha.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-249">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Ejemplo que muestra cómo no debes alinear a la izquierda los controles principales." border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="1cd6a-251">No: acciones de alineación a la izquierda o al centro</span><span class="sxs-lookup"><span data-stu-id="1cd6a-251">Don't: Left or center align actions</span></span>

<span data-ttu-id="1cd6a-252">Esto se desvía del patrón estándar de Teams para la colocación de controles en un cuadro de diálogo y puede conflicto con un cuadro de diálogo detrás del superior.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-252">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scroll"></a><span data-ttu-id="1cd6a-253">Scroll</span><span class="sxs-lookup"><span data-stu-id="1cd6a-253">Scroll</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Ejemplo que muestra el desplazamiento vertical en una pestaña de reunión." border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="1cd6a-255">Hacer: desplazarse verticalmente</span><span class="sxs-lookup"><span data-stu-id="1cd6a-255">Do: Scroll vertically</span></span>

<span data-ttu-id="1cd6a-256">Los usuarios esperan un desplazamiento vertical en Teams (y en otros lugares).</span><span class="sxs-lookup"><span data-stu-id="1cd6a-256">Users expect vertical scrolling in Teams (and elsewhere).</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Ejemplo que muestra el desplazamiento horizontal en una pestaña de reunión." border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="1cd6a-258">No: desplazarse horizontalmente</span><span class="sxs-lookup"><span data-stu-id="1cd6a-258">Don't: Scroll horizontally</span></span>

<span data-ttu-id="1cd6a-259">El desplazamiento horizontal no es un comportamiento esperado en Teams.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-259">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="1cd6a-260">Otros lienzos del entorno de reuniones se desplazan verticalmente.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-260">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="1cd6a-261">Flujos de trabajo</span><span class="sxs-lookup"><span data-stu-id="1cd6a-261">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Ejemplo que muestra un escenario complejo en una pestaña de reunión." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="1cd6a-263">Hacer: Surface complex scenarios in the in-meeting tab</span><span class="sxs-lookup"><span data-stu-id="1cd6a-263">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="1cd6a-264">Si la aplicación incluye varias tareas, te recomendamos encarecidamente usar una pestaña de reunión con un diseño de una sola columna.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-264">If your app includes multiple tasks, we strongly recommend using an in-meeting tab with a single-column layout.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Ejemplo que muestra escenarios complejos en un cuadro de diálogo en la reunión." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a><span data-ttu-id="1cd6a-266">No: hacer complejos los cuadros de diálogo en la reunión</span><span class="sxs-lookup"><span data-stu-id="1cd6a-266">Don't: Make in-meeting dialogs complex</span></span>

<span data-ttu-id="1cd6a-267">Los cuadros de diálogo dentro de la reunión están diseñados para interacciones breves.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-267">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="1cd6a-268">Creación de temas</span><span class="sxs-lookup"><span data-stu-id="1cd6a-268">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Ejemplo que muestra una extensión de reunión con el tema oscuro." border="false":::

#### <a name="do-use-teams-color-tokens"></a><span data-ttu-id="1cd6a-270">Usar tokens de color de Teams</span><span class="sxs-lookup"><span data-stu-id="1cd6a-270">Do: Use Teams color tokens</span></span>

<span data-ttu-id="1cd6a-271">Las reuniones de Teams están optimizadas para el modo oscuro para ayudar a reducir el ruido visual y cognitiva para que los usuarios puedan centrarse en la discusión y el contenido compartido.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-271">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="1cd6a-272">Obtenga información sobre el <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">uso de tokens de color (ui. fluent).</a></span><span class="sxs-lookup"><span data-stu-id="1cd6a-272">Learn about using <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a>.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Ejemplo que muestra una extensión de reunión con un tema predeterminado (claro)." border="false":::

#### <a name="dont-hard-code-hex-values"></a><span data-ttu-id="1cd6a-274">No: valores hexadecimales de código duro</span><span class="sxs-lookup"><span data-stu-id="1cd6a-274">Don't: Hard code hex values</span></span>

<span data-ttu-id="1cd6a-275">Si no usa tokens de color de Teams, los diseños serán menos escalables y tardarán más tiempo en administrarse.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-275">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="1cd6a-276">Navegación</span><span class="sxs-lookup"><span data-stu-id="1cd6a-276">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Ejemplo que muestra una extensión de reunión con un botón Atrás." border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="1cd6a-278">Do: Have a Back button</span><span class="sxs-lookup"><span data-stu-id="1cd6a-278">Do: Have a back button</span></span>

<span data-ttu-id="1cd6a-279">Si tiene más de un nivel de navegación en una pestaña de reunión, los usuarios deben poder volver a sus vistas anteriores.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-279">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Ejemplo que muestra una extensión de reunión con dos botones de descarte." border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="1cd6a-281">No: incluir otro botón descartar</span><span class="sxs-lookup"><span data-stu-id="1cd6a-281">Don't: Include another dismiss button</span></span>

<span data-ttu-id="1cd6a-282">Proporcionar una opción para cerrar el contenido de la pestaña en la reunión puede causar problemas, ya que ya hay un botón en el encabezado para descartar la propia pestaña en la reunión.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-282">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Ejemplo que muestra modales (o módulos de tareas) en una pestaña de reunión." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="1cd6a-284">Precaución: evite los modales en la pestaña en la reunión</span><span class="sxs-lookup"><span data-stu-id="1cd6a-284">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="1cd6a-285">Las modalidades (también conocidas como módulos de tareas) en la pestaña de reunión ya estrecha podrían encapsular y ocultar el contenido.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-285">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a><span data-ttu-id="1cd6a-286">Validar el diseño</span><span class="sxs-lookup"><span data-stu-id="1cd6a-286">Validate your design</span></span>

<span data-ttu-id="1cd6a-287">Si tienes previsto publicar la aplicación en AppSource, debes comprender los problemas de diseño que normalmente provocan errores en las aplicaciones durante el envío.</span><span class="sxs-lookup"><span data-stu-id="1cd6a-287">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1cd6a-288">Comprobar las directrices de validación de diseño</span><span class="sxs-lookup"><span data-stu-id="1cd6a-288">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)

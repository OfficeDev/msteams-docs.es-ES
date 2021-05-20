---
title: Diseño de la extensión de su reunión
author: heath-hamilton
description: Obtén información sobre cómo diseñar aplicaciones en reuniones Teams y obtener el Kit de interfaz de usuario de Microsoft Teams.
ms.author: lajanuar
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 0a888c333305e9caafcd0bac0e5549bf08ead424
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566029"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="b1b11-103">Diseño de la extensión de la reunión de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b1b11-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="b1b11-104">Puede crear aplicaciones para que las reuniones sean más productivas.</span><span class="sxs-lookup"><span data-stu-id="b1b11-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="b1b11-105">Por ejemplo, pida a las personas que completen una encuesta durante una llamada o envíen un recordatorio rápido que no interrumpa el flujo de la reunión.</span><span class="sxs-lookup"><span data-stu-id="b1b11-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="b1b11-106">Kit de UI de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b1b11-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="b1b11-107">Puede encontrar directrices de diseño más completas, incluidos los elementos que puede capturar y modificar según sea necesario, en el Kit de interfaz de usuario de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="b1b11-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b1b11-108">Obtener el Kit de UI de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="b1b11-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="b1b11-109">Añadir una extensión de reunión</span><span class="sxs-lookup"><span data-stu-id="b1b11-109">Add a meeting extension</span></span>

<span data-ttu-id="b1b11-110">Puede agregar una extensión de reunión antes y durante las reuniones.</span><span class="sxs-lookup"><span data-stu-id="b1b11-110">You can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="b1b11-111">También puede agregar una aplicación para una reunión específica directamente desde la tienda Teams (AppSource).</span><span class="sxs-lookup"><span data-stu-id="b1b11-111">You also can add an app for a specific meeting directly from the Teams store (AppSource).</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="b1b11-112">Añadir antes de una reunión</span><span class="sxs-lookup"><span data-stu-id="b1b11-112">Add before a meeting</span></span>

<span data-ttu-id="b1b11-113">En los detalles de la reunión, seleccione **Agregar una pestaña +** para abrir el menú desplegable de la aplicación y buscar aplicaciones optimizadas para reuniones.</span><span class="sxs-lookup"><span data-stu-id="b1b11-113">In the meeting details, select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de reunión antes de una reunión." border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="b1b11-115">Añadir durante una reunión</span><span class="sxs-lookup"><span data-stu-id="b1b11-115">Add during a meeting</span></span>

En una reunión, selecciona **Más** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **agregar una aplicación** y elige la aplicación que quieras.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de reunión durante una reunión." border="false":::

## <a name="before-a-meeting"></a><span data-ttu-id="b1b11-118">Antes de una reunión</span><span class="sxs-lookup"><span data-stu-id="b1b11-118">Before a meeting</span></span>

<span data-ttu-id="b1b11-119">Antes de la reunión, puede agregar contenido en la pestaña. En el ejemplo siguiente se muestra un borrador de pregunta de encuesta que las personas responderán durante la llamada.</span><span class="sxs-lookup"><span data-stu-id="b1b11-119">Prior to your meeting, you can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="En el ejemplo se muestra cómo app content en los detalles de la reunión antes de una llamada." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="b1b11-121">Anatomía: pestaña Reunión (antes y después de las reuniones)</span><span class="sxs-lookup"><span data-stu-id="b1b11-121">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="El ejemplo muestra la anatomía estructural de una pestaña de reunión antes y después de una reunión." border="false":::

|<span data-ttu-id="b1b11-123">Contador</span><span class="sxs-lookup"><span data-stu-id="b1b11-123">Counter</span></span>|<span data-ttu-id="b1b11-124">Descripción</span><span class="sxs-lookup"><span data-stu-id="b1b11-124">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b1b11-125">1</span><span class="sxs-lookup"><span data-stu-id="b1b11-125">1</span></span>|<span data-ttu-id="b1b11-126">**Nombre de la pestaña**: Etiqueta de navegación para la pestaña.</span><span class="sxs-lookup"><span data-stu-id="b1b11-126">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="b1b11-127">2</span><span class="sxs-lookup"><span data-stu-id="b1b11-127">2</span></span>|<span data-ttu-id="b1b11-128">**Desbordamiento de tabulación:** abre acciones de tabulación, como cambiar el nombre y quitar.</span><span class="sxs-lookup"><span data-stu-id="b1b11-128">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="b1b11-129">3</span><span class="sxs-lookup"><span data-stu-id="b1b11-129">3</span></span>|<span data-ttu-id="b1b11-130">**iframe**: muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b1b11-130">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="b1b11-131">Diseño con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="b1b11-131">Designing with UI templates</span></span>

<span data-ttu-id="b1b11-132">Utilice una de las siguientes plantillas de interfaz de usuario Teams para ayudar a diseñar la pestaña de reunión:</span><span class="sxs-lookup"><span data-stu-id="b1b11-132">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="b1b11-133">[Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato escaneable y permitir a los usuarios realizar acciones en una lista completa o en elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="b1b11-133">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="b1b11-134">[Tablero de tareas](../../concepts/design/design-teams-app-ui-templates.md#task-board): Un tablero de tareas, a veces llamado tablero kanban o carriles de natación, es una colección de tarjetas que se utilizan a menudo para rastrear el estado de los artículos de trabajo o boletos.</span><span class="sxs-lookup"><span data-stu-id="b1b11-134">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="b1b11-135">[Panel](../../concepts/design/design-teams-app-ui-templates.md#dashboard): Un panel es un lienzo que contiene varias tarjetas que proporcionan una visión general de los datos o el contenido.</span><span class="sxs-lookup"><span data-stu-id="b1b11-135">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="b1b11-136">[Formulario](../../concepts/design/design-teams-app-ui-templates.md#form): Los formularios son para recopilar, validar y enviar la entrada del usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="b1b11-136">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="b1b11-137">[Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacía se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.</span><span class="sxs-lookup"><span data-stu-id="b1b11-137">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="b1b11-138">[Navegador izquierdo](../../concepts/design/design-teams-app-ui-templates.md#left-nav): La plantilla de navegación izquierda puede ayudar si la pestaña requiere un poco de navegación.</span><span class="sxs-lookup"><span data-stu-id="b1b11-138">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="b1b11-139">En general, debe mantener la navegación de la pestaña al mínimo.</span><span class="sxs-lookup"><span data-stu-id="b1b11-139">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="b1b11-140">Utilice una pestaña en la reunión</span><span class="sxs-lookup"><span data-stu-id="b1b11-140">Use an in-meeting tab</span></span>

<span data-ttu-id="b1b11-141">La pestaña en la reunión es un lienzo para aumentar la colaboración durante las reuniones.</span><span class="sxs-lookup"><span data-stu-id="b1b11-141">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="b1b11-142">Los asistentes pueden ver e interactuar con el contenido de la aplicación en un espacio dedicado fuera de la etapa de reunión a través de vistas compartidas o basadas en roles.</span><span class="sxs-lookup"><span data-stu-id="b1b11-142">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="b1b11-143">Casos de uso</span><span class="sxs-lookup"><span data-stu-id="b1b11-143">Use cases</span></span>

<span data-ttu-id="b1b11-144">La gente podría usar la pestaña en la reunión para:</span><span class="sxs-lookup"><span data-stu-id="b1b11-144">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="b1b11-145">Proporcione comentarios detallados.</span><span class="sxs-lookup"><span data-stu-id="b1b11-145">Provide detailed feedback.</span></span> <span data-ttu-id="b1b11-146">Por ejemplo, evalúe a un candidato de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b1b11-146">For example, evaluate a job candidate.</span></span>
* <span data-ttu-id="b1b11-147">Cree una encuesta, encuesta o elemento de tarea para los participantes de la reunión.</span><span class="sxs-lookup"><span data-stu-id="b1b11-147">Create a poll, survey, or task item for the meeting participants.</span></span>
* <span data-ttu-id="b1b11-148">Mostrar notas relevantes para la reunión.</span><span class="sxs-lookup"><span data-stu-id="b1b11-148">Display notes relevant to the meeting.</span></span> <span data-ttu-id="b1b11-149">Por ejemplo, información sobre un cliente potencial de ventas.</span><span class="sxs-lookup"><span data-stu-id="b1b11-149">For example, information about a sales lead.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="En el ejemplo se muestra cómo puede presentar contenido de sondeo en una pestaña de reunión." border="false":::

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="b1b11-151">Anatomía: pestaña en la reunión</span><span class="sxs-lookup"><span data-stu-id="b1b11-151">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="El ejemplo muestra la anatomía estructural de una pestaña en la reunión." border="false":::

|<span data-ttu-id="b1b11-153">Contador</span><span class="sxs-lookup"><span data-stu-id="b1b11-153">Counter</span></span>|<span data-ttu-id="b1b11-154">Descripción</span><span class="sxs-lookup"><span data-stu-id="b1b11-154">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b1b11-155">1</span><span class="sxs-lookup"><span data-stu-id="b1b11-155">1</span></span>|<span data-ttu-id="b1b11-156">**Icono de aplicación (seleccionado):** logotipo de aplicación transparente de 16 píxeles.</span><span class="sxs-lookup"><span data-stu-id="b1b11-156">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="b1b11-157">2</span><span class="sxs-lookup"><span data-stu-id="b1b11-157">2</span></span>|<span data-ttu-id="b1b11-158">**Nombre de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="b1b11-158">**App name**</span></span>|
|<span data-ttu-id="b1b11-159">3</span><span class="sxs-lookup"><span data-stu-id="b1b11-159">3</span></span>|<span data-ttu-id="b1b11-160">**Encabezado**: incluye el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b1b11-160">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="b1b11-161">4 </span><span class="sxs-lookup"><span data-stu-id="b1b11-161">4</span></span>|<span data-ttu-id="b1b11-162">**Botón Cerrar**: Descarta la pestaña. Utilice siempre el icono de cierre superior derecha en lugar de una acción en el pie de página.</span><span class="sxs-lookup"><span data-stu-id="b1b11-162">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="b1b11-163">5 </span><span class="sxs-lookup"><span data-stu-id="b1b11-163">5</span></span>|<span data-ttu-id="b1b11-164">**Barra de notificaciones:** las alertas de error se muestran directamente debajo del encabezado y empujan el contenido de iframe hacia abajo en 20 píxeles.</span><span class="sxs-lookup"><span data-stu-id="b1b11-164">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="b1b11-165">6 </span><span class="sxs-lookup"><span data-stu-id="b1b11-165">6</span></span>|<span data-ttu-id="b1b11-166">**iframe**: muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b1b11-166">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="b1b11-167">Spacing</span><span class="sxs-lookup"><span data-stu-id="b1b11-167">Spacing</span></span>

<span data-ttu-id="b1b11-168">Optimice su pestaña en la reunión para ajustar de borde a borde dentro del área de iframe de 280 píxeles de ancho.</span><span class="sxs-lookup"><span data-stu-id="b1b11-168">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="b1b11-169">Hay 20 píxeles de relleno en los lados izquierdo y derecho del iframe y entre el encabezado de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="b1b11-169">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="b1b11-170">El iframe está lleno de sangrado en la parte inferior de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="b1b11-170">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="En el ejemplo se muestran las dimensiones de espaciado de tabulación en la reunión." border="false":::

### <a name="scrolling"></a><span data-ttu-id="b1b11-172">desplazamiento</span><span class="sxs-lookup"><span data-stu-id="b1b11-172">Scrolling</span></span>

<span data-ttu-id="b1b11-173">El contenido de Iframe debe desplazarse verticalmente.</span><span class="sxs-lookup"><span data-stu-id="b1b11-173">Iframe contents should scroll vertically.</span></span> <span data-ttu-id="b1b11-174">Solo puedes ver el contenido al que te has desplazado (nada por encima o por debajo).</span><span class="sxs-lookup"><span data-stu-id="b1b11-174">You can only see the content you've scrolled to (nothing above or below).</span></span> <span data-ttu-id="b1b11-175">La barra de desplazamiento forma parte del contenido de iframe.</span><span class="sxs-lookup"><span data-stu-id="b1b11-175">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="En el ejemplo se muestra cómo se desplaza la pestaña en la reunión." border="false":::

### <a name="navigation"></a><span data-ttu-id="b1b11-177">Navegación</span><span class="sxs-lookup"><span data-stu-id="b1b11-177">Navigation</span></span>

<span data-ttu-id="b1b11-178">Para escenarios con capas de navegación o contenido pesado, se recomienda permitir a los usuarios navegar a una capa secundaria.</span><span class="sxs-lookup"><span data-stu-id="b1b11-178">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="b1b11-179">Los usuarios deben poder volver a la capa anterior.</span><span class="sxs-lookup"><span data-stu-id="b1b11-179">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="El ejemplo muestra la navegación en la reunión." border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="b1b11-181">Utilice un cuadro de diálogo en la reunión</span><span class="sxs-lookup"><span data-stu-id="b1b11-181">Use an in-meeting dialog</span></span>

<span data-ttu-id="b1b11-182">Los cuadros de diálogo en la reunión se muestran en la fase de Teams reunión.</span><span class="sxs-lookup"><span data-stu-id="b1b11-182">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="b1b11-183">Requieren la atención, confirmación o interacción de un usuario, pero son sutiles y no interrumpen la reunión.</span><span class="sxs-lookup"><span data-stu-id="b1b11-183">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="b1b11-184">Debe usarlos con moderación y para escenarios que estén orientados a la luz y a las tareas.</span><span class="sxs-lookup"><span data-stu-id="b1b11-184">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="b1b11-185">Casos de uso</span><span class="sxs-lookup"><span data-stu-id="b1b11-185">Use cases</span></span>

<span data-ttu-id="b1b11-186">Los cuadros de diálogo en la reunión son activados por un usuario (como el organizador de la reunión) que podría querer que los participantes:</span><span class="sxs-lookup"><span data-stu-id="b1b11-186">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="b1b11-187">Proporcionar breves comentarios</span><span class="sxs-lookup"><span data-stu-id="b1b11-187">Provide brief feedback</span></span>
* <span data-ttu-id="b1b11-188">Hacer una encuesta o encuesta corta</span><span class="sxs-lookup"><span data-stu-id="b1b11-188">Take a short survey or poll</span></span>
* <span data-ttu-id="b1b11-189">Presentar aprobaciones</span><span class="sxs-lookup"><span data-stu-id="b1b11-189">Submit approvals</span></span>
* <span data-ttu-id="b1b11-190">Recibir recordatorios</span><span class="sxs-lookup"><span data-stu-id="b1b11-190">Get reminders</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="En el ejemplo se muestra cómo puede utilizar un cuadro de diálogo en la reunión." border="false":::

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="b1b11-192">Anatomía: Diálogo en la reunión</span><span class="sxs-lookup"><span data-stu-id="b1b11-192">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="El ejemplo muestra la anatomía estructural de un cuadro de diálogo en la reunión." border="false":::

|<span data-ttu-id="b1b11-194">Contador</span><span class="sxs-lookup"><span data-stu-id="b1b11-194">Counter</span></span>|<span data-ttu-id="b1b11-195">Descripción</span><span class="sxs-lookup"><span data-stu-id="b1b11-195">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b1b11-196">1</span><span class="sxs-lookup"><span data-stu-id="b1b11-196">1</span></span>|<span data-ttu-id="b1b11-197">**Encabezado:** incluye icono de aplicación, nombre, cadena de acción e icono de cierre.</span><span class="sxs-lookup"><span data-stu-id="b1b11-197">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="b1b11-198">2</span><span class="sxs-lookup"><span data-stu-id="b1b11-198">2</span></span>|<span data-ttu-id="b1b11-199">**iframe**: muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b1b11-199">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="b1b11-200">Anatomía: encabezado del cuadro de diálogo en la reunión</span><span class="sxs-lookup"><span data-stu-id="b1b11-200">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de un encabezado de cuadro de diálogo en la reunión." border="false":::

<span data-ttu-id="b1b11-202">Hay dos variantes de encabezado.</span><span class="sxs-lookup"><span data-stu-id="b1b11-202">There are two header variants.</span></span> <span data-ttu-id="b1b11-203">Cuando sea posible, utilice la variante con el avatar para reforzar que el diálogo proviene de una persona.</span><span class="sxs-lookup"><span data-stu-id="b1b11-203">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="b1b11-204">Contador</span><span class="sxs-lookup"><span data-stu-id="b1b11-204">Counter</span></span>|<span data-ttu-id="b1b11-205">Descripción</span><span class="sxs-lookup"><span data-stu-id="b1b11-205">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b1b11-206">1</span><span class="sxs-lookup"><span data-stu-id="b1b11-206">1</span></span>|<span data-ttu-id="b1b11-207">**Avatar**: Persona que inicia el diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="b1b11-207">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="b1b11-208">2</span><span class="sxs-lookup"><span data-stu-id="b1b11-208">2</span></span>|<span data-ttu-id="b1b11-209">**Icono de aplicación**</span><span class="sxs-lookup"><span data-stu-id="b1b11-209">**App icon**</span></span>|
|<span data-ttu-id="b1b11-210">3</span><span class="sxs-lookup"><span data-stu-id="b1b11-210">3</span></span>|<span data-ttu-id="b1b11-211">**Nombre de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="b1b11-211">**App name**</span></span>|
|<span data-ttu-id="b1b11-212">4 </span><span class="sxs-lookup"><span data-stu-id="b1b11-212">4</span></span>|<span data-ttu-id="b1b11-213">**Botón Cerrar**: descarta el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b1b11-213">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="b1b11-214">5 </span><span class="sxs-lookup"><span data-stu-id="b1b11-214">5</span></span>|<span data-ttu-id="b1b11-215">**Cadena de acción:** normalmente describe quién inició el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b1b11-215">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior"></a><span data-ttu-id="b1b11-216">Comportamiento dinámico</span><span class="sxs-lookup"><span data-stu-id="b1b11-216">Responsive behavior</span></span>

<span data-ttu-id="b1b11-217">Los cuadros de diálogo en la reunión pueden variar en tamaño para tener en cuenta diferentes escenarios.</span><span class="sxs-lookup"><span data-stu-id="b1b11-217">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="b1b11-218">Asegúrese de mantener el relleno y los tamaños de componentes.</span><span class="sxs-lookup"><span data-stu-id="b1b11-218">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="b1b11-219">**Ancho**: puede especificar el ancho del iframe del cuadro de diálogo en cualquier lugar dentro del rango de tamaño admitido.</span><span class="sxs-lookup"><span data-stu-id="b1b11-219">**Width**: You can specify the width of the dialog's iframe anywhere within the supported size range.</span></span>
* <span data-ttu-id="b1b11-220">**Altura**: Puede especificar la altura del iframe del cuadro de diálogo en cualquier lugar dentro del rango de tamaño admitido.</span><span class="sxs-lookup"><span data-stu-id="b1b11-220">**Height**: You can specify the height of the dialog's iframe anywhere within the supported size range.</span></span> <span data-ttu-id="b1b11-221">También puede permitir que los usuarios se despplacen verticalmente si el contenido de la aplicación supera la altura máxima.</span><span class="sxs-lookup"><span data-stu-id="b1b11-221">You also can allow users to scroll vertically if your app content exceeds the maximum height.</span></span>

<span data-ttu-id="b1b11-222">Para implementar, especifique el ancho y la altura mediante la [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) clave.</span><span class="sxs-lookup"><span data-stu-id="b1b11-222">To implement, specify the width and height using the [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) key.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="En el ejemplo se muestra el cuadro de diálogo en la reunión. Ancho: Min--280 píxeles (iframe de 248 píxeles). Max-- 460 píxeles (iframe de 428 píxeles). Altura: 300 píxeles (iframe)." border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="b1b11-224">Después de una reunión</span><span class="sxs-lookup"><span data-stu-id="b1b11-224">After a meeting</span></span>

<span data-ttu-id="b1b11-225">Puede volver a una reunión una vez finalizada y ver el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b1b11-225">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="b1b11-226">En este ejemplo, el organizador de la reunión puede examinar los resultados de la encuesta en la pestaña **Contoso.** (Nota: Desde un punto de vista de diseño, no hay diferencia entre una experiencia de pestaña anterior y posterior a la reunión.)</span><span class="sxs-lookup"><span data-stu-id="b1b11-226">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="La ilustración de ejemplo muestra una pestaña posterior a la reunión." border="false":::

## <a name="best-practices"></a><span data-ttu-id="b1b11-228">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="b1b11-228">Best practices</span></span>

<span data-ttu-id="b1b11-229">Utilice estas recomendaciones para crear una experiencia de aplicación de calidad.</span><span class="sxs-lookup"><span data-stu-id="b1b11-229">Use these recommendations to create a quality app experience.</span></span>

### <a name="interactions"></a><span data-ttu-id="b1b11-230">Interacciones</span><span class="sxs-lookup"><span data-stu-id="b1b11-230">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Ejemplo que muestra cómo limitar el número de interacciones." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="b1b11-232">Hacer: Limitar el número de interacciones</span><span class="sxs-lookup"><span data-stu-id="b1b11-232">Do: Limit the number of interactions</span></span>

<span data-ttu-id="b1b11-233">Para los cuadros de diálogo en la reunión, elimine contenido innecesario que no ayude a los usuarios a lograr algo rápidamente.</span><span class="sxs-lookup"><span data-stu-id="b1b11-233">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Ejemplo que muestra cómo no introducir elementos innecesarios." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="b1b11-235">No: Introducir elementos innecesarios</span><span class="sxs-lookup"><span data-stu-id="b1b11-235">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="b1b11-236">Un único cuadro de diálogo en la reunión con varias interacciones puede distraer de la llamada.</span><span class="sxs-lookup"><span data-stu-id="b1b11-236">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="b1b11-237">Diseño</span><span class="sxs-lookup"><span data-stu-id="b1b11-237">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Ejemplo que muestra cómo debe usar un diseño de cuadro de diálogo de una sola columna." border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a><span data-ttu-id="b1b11-239">Hacer: Utilice un diseño de cuadro de diálogo de una sola columna</span><span class="sxs-lookup"><span data-stu-id="b1b11-239">Do: Use a single-column dialog layout</span></span>

<span data-ttu-id="b1b11-240">Dado que los cuadros de diálogo están en el centro de la fase de reunión, la finalización de la tarea debe ser rápida y sencilla para evitar la frustración del usuario.</span><span class="sxs-lookup"><span data-stu-id="b1b11-240">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Ejemplo que muestra que no debe saturar el espacio de una extensión de reunión." border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="b1b11-242">No: Abarrotar el espacio</span><span class="sxs-lookup"><span data-stu-id="b1b11-242">Don't: Clutter the space</span></span>

<span data-ttu-id="b1b11-243">El contenido denso o excesivamente estructurado puede distraer y ser abrumador, especialmente durante una reunión.</span><span class="sxs-lookup"><span data-stu-id="b1b11-243">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Ejemplo que muestra un diseño de tabulación de una sola columna." border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a><span data-ttu-id="b1b11-245">Hacer: Utilice un diseño de tabulación de una sola columna</span><span class="sxs-lookup"><span data-stu-id="b1b11-245">Do: Use a single-column tab layout</span></span>

<span data-ttu-id="b1b11-246">Dada la naturaleza estrecha de la pestaña en la reunión, se recomienda encarecidamente mostrar el contenido en una sola columna.</span><span class="sxs-lookup"><span data-stu-id="b1b11-246">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Ejemplo que muestra una pestaña con varias columnas." border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="b1b11-248">No: Usa varias columnas</span><span class="sxs-lookup"><span data-stu-id="b1b11-248">Don't: Use multiple columns</span></span>

<span data-ttu-id="b1b11-249">Debido al espacio limitado de la pestaña en la reunión, no se recomiendan diseños con más de una columna.</span><span class="sxs-lookup"><span data-stu-id="b1b11-249">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="b1b11-250">Controles</span><span class="sxs-lookup"><span data-stu-id="b1b11-250">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Ejemplo que muestra cómo alinear correctamente los controles primarios." border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="b1b11-252">Hacer: Alinee bien la acción principal</span><span class="sxs-lookup"><span data-stu-id="b1b11-252">Do: Right align the primary action</span></span>

<span data-ttu-id="b1b11-253">Recomendamos colocar la acción más pesada visualmente en la ubicación más correcta.</span><span class="sxs-lookup"><span data-stu-id="b1b11-253">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Ejemplo que muestra cómo no debe dejar alinear los controles primarios." border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="b1b11-255">No: Las acciones de alineación izquierda o central</span><span class="sxs-lookup"><span data-stu-id="b1b11-255">Don't: Left or center align actions</span></span>

<span data-ttu-id="b1b11-256">Esto se desvía del patrón de Teams estándar para la colocación del control en un cuadro de diálogo y puede entrar en conflicto con un cuadro de diálogo detrás del superior.</span><span class="sxs-lookup"><span data-stu-id="b1b11-256">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scroll"></a><span data-ttu-id="b1b11-257">Scroll</span><span class="sxs-lookup"><span data-stu-id="b1b11-257">Scroll</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Ejemplo que muestra el desplazamiento vertical en una pestaña de reunión." border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="b1b11-259">Hacer: Desplázate verticalmente</span><span class="sxs-lookup"><span data-stu-id="b1b11-259">Do: Scroll vertically</span></span>

<span data-ttu-id="b1b11-260">Los usuarios esperan desplazamiento vertical en Teams (y en otros lugares).</span><span class="sxs-lookup"><span data-stu-id="b1b11-260">Users expect vertical scrolling in Teams (and elsewhere).</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Ejemplo que muestra el desplazamiento horizontal en una pestaña de reunión." border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="b1b11-262">No: Desplázate horizontalmente</span><span class="sxs-lookup"><span data-stu-id="b1b11-262">Don't: Scroll horizontally</span></span>

<span data-ttu-id="b1b11-263">El desplazamiento horizontal no es un comportamiento esperado en Teams.</span><span class="sxs-lookup"><span data-stu-id="b1b11-263">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="b1b11-264">Otros lienzos del entorno de reuniones se desplazan verticalmente.</span><span class="sxs-lookup"><span data-stu-id="b1b11-264">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="b1b11-265">Flujos de trabajo</span><span class="sxs-lookup"><span data-stu-id="b1b11-265">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Ejemplo que muestra el escenario complejo en una pestaña de reunión." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="b1b11-267">Hacer: Escenarios complejos de Surface en la pestaña en la reunión</span><span class="sxs-lookup"><span data-stu-id="b1b11-267">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="b1b11-268">Si la aplicación incluye varias tareas, se recomienda encarecidamente usar una pestaña en la reunión con un diseño de una sola columna.</span><span class="sxs-lookup"><span data-stu-id="b1b11-268">If your app includes multiple tasks, we strongly recommend using an in-meeting tab with a single-column layout.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Ejemplo que muestra escenarios complejos en un cuadro de diálogo en la reunión." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a><span data-ttu-id="b1b11-270">No: Hacer que los diálogos en la reunión sean complejos</span><span class="sxs-lookup"><span data-stu-id="b1b11-270">Don't: Make in-meeting dialogs complex</span></span>

<span data-ttu-id="b1b11-271">Los cuadros de diálogo en la reunión están destinados a interacciones breves.</span><span class="sxs-lookup"><span data-stu-id="b1b11-271">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="b1b11-272">Creación de temas</span><span class="sxs-lookup"><span data-stu-id="b1b11-272">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Ejemplo que muestra una extensión de reunión con el tema oscuro." border="false":::

#### <a name="do-use-teams-color-tokens"></a><span data-ttu-id="b1b11-274">Hacer: Use tokens de color Teams</span><span class="sxs-lookup"><span data-stu-id="b1b11-274">Do: Use Teams color tokens</span></span>

<span data-ttu-id="b1b11-275">Teams reuniones están optimizadas para el modo oscuro para ayudar a reducir el ruido visual y cognitivo para que los usuarios puedan centrarse en la discusión y el contenido compartido.</span><span class="sxs-lookup"><span data-stu-id="b1b11-275">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="b1b11-276">Obtenga información sobre el uso de <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">tokens de color (FLUENT UI).</a></span><span class="sxs-lookup"><span data-stu-id="b1b11-276">Learn about using <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a>.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Ejemplo que muestra una extensión de reunión con un tema predeterminado (luz)." border="false":::

#### <a name="dont-hard-code-hex-values"></a><span data-ttu-id="b1b11-278">No: Valores hexagonal de código duro</span><span class="sxs-lookup"><span data-stu-id="b1b11-278">Don't: Hard code hex values</span></span>

<span data-ttu-id="b1b11-279">Si no usa tokens de color Teams, sus diseños serán menos escalables y tardarán más tiempo en administrarse.</span><span class="sxs-lookup"><span data-stu-id="b1b11-279">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="b1b11-280">Navegación</span><span class="sxs-lookup"><span data-stu-id="b1b11-280">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Ejemplo que muestra una extensión de reunión con un botón atrás." border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="b1b11-282">Hacer: Tener un botón atrás</span><span class="sxs-lookup"><span data-stu-id="b1b11-282">Do: Have a back button</span></span>

<span data-ttu-id="b1b11-283">Si tiene más de una capa de navegación en una pestaña en la reunión, los usuarios deben poder volver a sus vistas anteriores.</span><span class="sxs-lookup"><span data-stu-id="b1b11-283">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Ejemplo que muestra una extensión de reunión con dos botones de descarte." border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="b1b11-285">No: Incluya otro botón de descarte</span><span class="sxs-lookup"><span data-stu-id="b1b11-285">Don't: Include another dismiss button</span></span>

<span data-ttu-id="b1b11-286">Proporcionar una opción para cerrar el contenido de la pestaña en la reunión puede causar problemas, ya que ya hay un botón en el encabezado para descartar la propia pestaña en la reunión.</span><span class="sxs-lookup"><span data-stu-id="b1b11-286">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Ejemplo que muestra modales (o módulos de tareas) dentro de una pestaña en la reunión." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="b1b11-288">Precaución: Evite modales dentro de la pestaña en la reunión</span><span class="sxs-lookup"><span data-stu-id="b1b11-288">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="b1b11-289">Modals (también conocidos como módulos de tareas) en la pestaña ya estrecha en la reunión pueden encapsular y oscurecer el contenido.</span><span class="sxs-lookup"><span data-stu-id="b1b11-289">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

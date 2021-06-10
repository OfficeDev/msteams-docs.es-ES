---
title: Diseño de la extensión de reunión
author: heath-hamilton
description: Obtén información sobre cómo diseñar aplicaciones en Teams reuniones y obtener el kit Microsoft Teams interfaz de usuario.
ms.author: lajanuar
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 33b11a6dfc759fabd54ca2fe2c68978a5d5d1475
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644648"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="5963d-103">Diseño de la extensión Microsoft Teams reunión</span><span class="sxs-lookup"><span data-stu-id="5963d-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="5963d-104">Puedes crear aplicaciones para que las reuniones sean más productivas.</span><span class="sxs-lookup"><span data-stu-id="5963d-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="5963d-105">Por ejemplo, pida a los usuarios que completen una encuesta durante una llamada o envíen un aviso rápido que no interrumpa el flujo de la reunión.</span><span class="sxs-lookup"><span data-stu-id="5963d-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="5963d-106">Kit de UI de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="5963d-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="5963d-107">Puedes encontrar instrucciones de diseño más completas, incluidos los elementos que puedes agarrar y modificar según sea necesario, en el kit de interfaz Microsoft Teams usuario.</span><span class="sxs-lookup"><span data-stu-id="5963d-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5963d-108">Obtener el Kit de UI de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="5963d-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="5963d-109">Agregar una extensión de reunión</span><span class="sxs-lookup"><span data-stu-id="5963d-109">Add a meeting extension</span></span>

<span data-ttu-id="5963d-110">Los usuarios pueden agregar una extensión de reunión antes y durante las reuniones.</span><span class="sxs-lookup"><span data-stu-id="5963d-110">Users can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="5963d-111">También pueden agregar una aplicación para una reunión específica directamente desde Teams tienda.</span><span class="sxs-lookup"><span data-stu-id="5963d-111">They also can add an app for a specific meeting directly from the Teams store.</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="5963d-112">Agregar antes de una reunión</span><span class="sxs-lookup"><span data-stu-id="5963d-112">Add before a meeting</span></span>

<span data-ttu-id="5963d-113">En los detalles de la reunión, los usuarios pueden seleccionar **Agregar una** pestaña + para abrir el control desplegable de la aplicación y buscar aplicaciones optimizadas para reuniones.</span><span class="sxs-lookup"><span data-stu-id="5963d-113">In the meeting details, users can select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de reunión antes de una reunión." border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="5963d-115">Agregar durante una reunión</span><span class="sxs-lookup"><span data-stu-id="5963d-115">Add during a meeting</span></span>

# <a name="desktop"></a>[<span data-ttu-id="5963d-116">Escritorio</span><span class="sxs-lookup"><span data-stu-id="5963d-116">Desktop</span></span>](#tab/desktop)

En una reunión, los usuarios pueden seleccionar **Más** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **agregar una aplicación** y elegir la aplicación que desean.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de reunión durante una reunión." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="5963d-119">Móvil</span><span class="sxs-lookup"><span data-stu-id="5963d-119">Mobile</span></span>](#tab/mobile)

En una reunión, los usuarios pueden seleccionar **Más** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: y elegir la aplicación que desean.

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-add-during-meeting.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de reunión durante una reunión en el móvil." border="false":::

---

## <a name="before-a-meeting"></a><span data-ttu-id="5963d-122">Antes de una reunión</span><span class="sxs-lookup"><span data-stu-id="5963d-122">Before a meeting</span></span>

<span data-ttu-id="5963d-123">Antes de una reunión, los usuarios pueden agregar contenido en la pestaña. En el siguiente ejemplo se muestra un borrador de pregunta de encuesta que los usuarios responderán durante la llamada.</span><span class="sxs-lookup"><span data-stu-id="5963d-123">Prior to a meeting, users can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="En el ejemplo se muestra cómo usar el contenido de la aplicación en los detalles de la reunión antes de una llamada." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="5963d-125">Anatomía: pestaña Reunión (antes y después de las reuniones)</span><span class="sxs-lookup"><span data-stu-id="5963d-125">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de una pestaña de reunión antes y después de una reunión." border="false":::

|<span data-ttu-id="5963d-127">Contador</span><span class="sxs-lookup"><span data-stu-id="5963d-127">Counter</span></span>|<span data-ttu-id="5963d-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="5963d-128">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="5963d-129">1</span><span class="sxs-lookup"><span data-stu-id="5963d-129">1</span></span>|<span data-ttu-id="5963d-130">**Nombre de la pestaña:** etiqueta de navegación para la pestaña.</span><span class="sxs-lookup"><span data-stu-id="5963d-130">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="5963d-131">2</span><span class="sxs-lookup"><span data-stu-id="5963d-131">2</span></span>|<span data-ttu-id="5963d-132">**Desbordamiento de** tabulación: abre acciones de tabulación, como cambiar el nombre y quitar.</span><span class="sxs-lookup"><span data-stu-id="5963d-132">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="5963d-133">3</span><span class="sxs-lookup"><span data-stu-id="5963d-133">3</span></span>|<span data-ttu-id="5963d-134">**iframe:** muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5963d-134">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="5963d-135">Diseño con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="5963d-135">Designing with UI templates</span></span>

<span data-ttu-id="5963d-136">Usa una de las siguientes plantillas Teams interfaz de usuario para ayudar a diseñar la pestaña de reunión:</span><span class="sxs-lookup"><span data-stu-id="5963d-136">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="5963d-137">[Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato digitalizado y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="5963d-137">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="5963d-138">[Panel de](../../concepts/design/design-teams-app-ui-templates.md#task-board)tareas: un panel de tareas, a veces denominado tablero de kanban o carriles de natación, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o los vales.</span><span class="sxs-lookup"><span data-stu-id="5963d-138">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="5963d-139">[Panel:](../../concepts/design/design-teams-app-ui-templates.md#dashboard)un panel es un lienzo que contiene varias tarjetas que proporcionan información general sobre los datos o el contenido.</span><span class="sxs-lookup"><span data-stu-id="5963d-139">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="5963d-140">[Formulario:](../../concepts/design/design-teams-app-ui-templates.md#form)los formularios son para recopilar, validar y enviar la entrada del usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="5963d-140">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="5963d-141">[Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacío se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.</span><span class="sxs-lookup"><span data-stu-id="5963d-141">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="5963d-142">[Navegación izquierda:](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav)el componente de navegación izquierdo puede ayudar si la pestaña requiere algo de navegación.</span><span class="sxs-lookup"><span data-stu-id="5963d-142">[Left nav](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav): The left nav component can help if your tab requires some navigation.</span></span> <span data-ttu-id="5963d-143">En general, debe mantener la navegación al mínimo.</span><span class="sxs-lookup"><span data-stu-id="5963d-143">In general, you should keep navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="5963d-144">Usar una pestaña en la reunión</span><span class="sxs-lookup"><span data-stu-id="5963d-144">Use an in-meeting tab</span></span>

<span data-ttu-id="5963d-145">La pestaña en la reunión es un lienzo para aumentar la colaboración durante las reuniones.</span><span class="sxs-lookup"><span data-stu-id="5963d-145">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="5963d-146">Los asistentes pueden ver e interactuar con el contenido de la aplicación en un espacio dedicado fuera de la fase de reunión a través de vistas compartidas o basadas en roles.</span><span class="sxs-lookup"><span data-stu-id="5963d-146">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="5963d-147">Casos de uso</span><span class="sxs-lookup"><span data-stu-id="5963d-147">Use cases</span></span>

<span data-ttu-id="5963d-148">Las personas pueden usar la pestaña en la reunión para:</span><span class="sxs-lookup"><span data-stu-id="5963d-148">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="5963d-149">Proporcionar comentarios detallados.</span><span class="sxs-lookup"><span data-stu-id="5963d-149">Provide detailed feedback.</span></span> <span data-ttu-id="5963d-150">Por ejemplo, evalúe un candidato de trabajo.</span><span class="sxs-lookup"><span data-stu-id="5963d-150">For example, evaluate a job candidate.</span></span>
* <span data-ttu-id="5963d-151">Cree un sondeo, una encuesta o un elemento de tarea para los participantes de la reunión.</span><span class="sxs-lookup"><span data-stu-id="5963d-151">Create a poll, survey, or task item for the meeting participants.</span></span>
* <span data-ttu-id="5963d-152">Mostrar notas relevantes para la reunión.</span><span class="sxs-lookup"><span data-stu-id="5963d-152">Display notes relevant to the meeting.</span></span> <span data-ttu-id="5963d-153">Por ejemplo, información sobre un cliente potencial de ventas.</span><span class="sxs-lookup"><span data-stu-id="5963d-153">For example, information about a sales lead.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="5963d-154">Escritorio</span><span class="sxs-lookup"><span data-stu-id="5963d-154">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="En el ejemplo se muestra cómo se puede presentar contenido de sondeo en una pestaña en la reunión." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="5963d-156">Móvil</span><span class="sxs-lookup"><span data-stu-id="5963d-156">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-tab.png" alt-text="En el ejemplo se muestra cómo se puede presentar contenido de sondeo en una pestaña de reunión en el móvil." border="false":::

---

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="5963d-158">Anatomía: pestaña En la reunión</span><span class="sxs-lookup"><span data-stu-id="5963d-158">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de una pestaña en reunión." border="false":::

|<span data-ttu-id="5963d-160">Contador</span><span class="sxs-lookup"><span data-stu-id="5963d-160">Counter</span></span>|<span data-ttu-id="5963d-161">Descripción</span><span class="sxs-lookup"><span data-stu-id="5963d-161">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="5963d-162">1</span><span class="sxs-lookup"><span data-stu-id="5963d-162">1</span></span>|<span data-ttu-id="5963d-163">**Icono de aplicación (seleccionado):** logotipo de aplicación transparente de 16 píxeles.</span><span class="sxs-lookup"><span data-stu-id="5963d-163">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="5963d-164">2</span><span class="sxs-lookup"><span data-stu-id="5963d-164">2</span></span>|<span data-ttu-id="5963d-165">**Nombre de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="5963d-165">**App name**</span></span>|
|<span data-ttu-id="5963d-166">3</span><span class="sxs-lookup"><span data-stu-id="5963d-166">3</span></span>|<span data-ttu-id="5963d-167">**Encabezado:** incluye el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5963d-167">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="5963d-168">4 </span><span class="sxs-lookup"><span data-stu-id="5963d-168">4</span></span>|<span data-ttu-id="5963d-169">**Botón Cerrar:** descarta la pestaña. Use siempre el icono de cierre superior derecho en lugar de una acción en el pie de página.</span><span class="sxs-lookup"><span data-stu-id="5963d-169">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="5963d-170">5 </span><span class="sxs-lookup"><span data-stu-id="5963d-170">5</span></span>|<span data-ttu-id="5963d-171">**Barra de notificaciones:** las alertas de error se muestran directamente debajo del encabezado y presionan el contenido del iframe hacia abajo en 20 píxeles.</span><span class="sxs-lookup"><span data-stu-id="5963d-171">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="5963d-172">6 </span><span class="sxs-lookup"><span data-stu-id="5963d-172">6</span></span>|<span data-ttu-id="5963d-173">**iframe:** muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5963d-173">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="5963d-174">Spacing</span><span class="sxs-lookup"><span data-stu-id="5963d-174">Spacing</span></span>

<span data-ttu-id="5963d-175">Optimiza la pestaña en la reunión para que se ajuste de un extremo a otro dentro del área de iframe de 280 píxeles.</span><span class="sxs-lookup"><span data-stu-id="5963d-175">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="5963d-176">Hay 20 píxeles de relleno en los lados izquierdo y derecho del iframe y entre el encabezado de pestaña.</span><span class="sxs-lookup"><span data-stu-id="5963d-176">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="5963d-177">El iframe está sangrando hasta la parte inferior de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="5963d-177">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="En el ejemplo se muestran las dimensiones de espaciado de tabulación en la reunión." border="false":::

### <a name="scrolling"></a><span data-ttu-id="5963d-179">Desplazamiento</span><span class="sxs-lookup"><span data-stu-id="5963d-179">Scrolling</span></span>

<span data-ttu-id="5963d-180">El contenido de Iframe debe desplazarse verticalmente.</span><span class="sxs-lookup"><span data-stu-id="5963d-180">Iframe contents should scroll vertically.</span></span> <span data-ttu-id="5963d-181">Solo puede ver el contenido al que se desplazó (nada superior o inferior).</span><span class="sxs-lookup"><span data-stu-id="5963d-181">You can only see the content you've scrolled to (nothing above or below).</span></span> <span data-ttu-id="5963d-182">La barra de desplazamiento forma parte del contenido de iframe.</span><span class="sxs-lookup"><span data-stu-id="5963d-182">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="En el ejemplo se muestra cómo se desplaza la pestaña en la reunión." border="false":::

### <a name="navigation"></a><span data-ttu-id="5963d-184">Navegación</span><span class="sxs-lookup"><span data-stu-id="5963d-184">Navigation</span></span>

<span data-ttu-id="5963d-185">Para escenarios con capas de navegación o contenido intenso, se recomienda permitir a los usuarios navegar a una capa secundaria.</span><span class="sxs-lookup"><span data-stu-id="5963d-185">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="5963d-186">Los usuarios deben poder volver a la capa anterior.</span><span class="sxs-lookup"><span data-stu-id="5963d-186">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="En el ejemplo se muestra la navegación en la reunión." border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="5963d-188">Usar un cuadro de diálogo en la reunión</span><span class="sxs-lookup"><span data-stu-id="5963d-188">Use an in-meeting dialog</span></span>

<span data-ttu-id="5963d-189">Los cuadros de diálogo en la reunión se muestran en la Teams de reunión.</span><span class="sxs-lookup"><span data-stu-id="5963d-189">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="5963d-190">Requieren la atención, confirmación o interacción de un usuario, pero son sutiles y no interrumpen la reunión.</span><span class="sxs-lookup"><span data-stu-id="5963d-190">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="5963d-191">Debe usarlos con moderación y para escenarios orientados a tareas y ligeras.</span><span class="sxs-lookup"><span data-stu-id="5963d-191">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="5963d-192">Casos de uso</span><span class="sxs-lookup"><span data-stu-id="5963d-192">Use cases</span></span>

<span data-ttu-id="5963d-193">Los cuadros de diálogo en la reunión son desencadenados por un usuario (como el organizador de la reunión) que puede querer que los participantes:</span><span class="sxs-lookup"><span data-stu-id="5963d-193">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="5963d-194">Proporcionar comentarios breves</span><span class="sxs-lookup"><span data-stu-id="5963d-194">Provide brief feedback</span></span>
* <span data-ttu-id="5963d-195">Realizar una encuesta o sondeo breves</span><span class="sxs-lookup"><span data-stu-id="5963d-195">Take a short survey or poll</span></span>
* <span data-ttu-id="5963d-196">Enviar aprobaciones</span><span class="sxs-lookup"><span data-stu-id="5963d-196">Submit approvals</span></span>
* <span data-ttu-id="5963d-197">Recibir recordatorios</span><span class="sxs-lookup"><span data-stu-id="5963d-197">Get reminders</span></span>

# <a name="desktop"></a>[<span data-ttu-id="5963d-198">Escritorio</span><span class="sxs-lookup"><span data-stu-id="5963d-198">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="En el ejemplo se muestra cómo se puede usar un cuadro de diálogo en la reunión." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="5963d-200">Móvil</span><span class="sxs-lookup"><span data-stu-id="5963d-200">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-dialog.png" alt-text="En el ejemplo se muestra cómo se puede usar un cuadro de diálogo en la reunión en el móvil." border="false":::

---

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="5963d-202">Anatomía: cuadro de diálogo en la reunión</span><span class="sxs-lookup"><span data-stu-id="5963d-202">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de un cuadro de diálogo en reunión." border="false":::

|<span data-ttu-id="5963d-204">Contador</span><span class="sxs-lookup"><span data-stu-id="5963d-204">Counter</span></span>|<span data-ttu-id="5963d-205">Descripción</span><span class="sxs-lookup"><span data-stu-id="5963d-205">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="5963d-206">1</span><span class="sxs-lookup"><span data-stu-id="5963d-206">1</span></span>|<span data-ttu-id="5963d-207">**Encabezado:** incluye el icono de la aplicación, el nombre, la cadena de acción y el icono cerrar.</span><span class="sxs-lookup"><span data-stu-id="5963d-207">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="5963d-208">2</span><span class="sxs-lookup"><span data-stu-id="5963d-208">2</span></span>|<span data-ttu-id="5963d-209">**iframe:** muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5963d-209">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="5963d-210">Anatomía: encabezado del cuadro de diálogo En la reunión</span><span class="sxs-lookup"><span data-stu-id="5963d-210">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de un encabezado de cuadro de diálogo en reunión." border="false":::

<span data-ttu-id="5963d-212">Hay dos variantes de encabezado.</span><span class="sxs-lookup"><span data-stu-id="5963d-212">There are two header variants.</span></span> <span data-ttu-id="5963d-213">Cuando sea posible, usa la variante con el avatar para reforzar que el cuadro de diálogo viene de una persona.</span><span class="sxs-lookup"><span data-stu-id="5963d-213">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="5963d-214">Contador</span><span class="sxs-lookup"><span data-stu-id="5963d-214">Counter</span></span>|<span data-ttu-id="5963d-215">Descripción</span><span class="sxs-lookup"><span data-stu-id="5963d-215">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="5963d-216">1</span><span class="sxs-lookup"><span data-stu-id="5963d-216">1</span></span>|<span data-ttu-id="5963d-217">**Avatar:** persona que inicia el cuadro de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="5963d-217">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="5963d-218">2</span><span class="sxs-lookup"><span data-stu-id="5963d-218">2</span></span>|<span data-ttu-id="5963d-219">**Icono de aplicación**</span><span class="sxs-lookup"><span data-stu-id="5963d-219">**App icon**</span></span>|
|<span data-ttu-id="5963d-220">3</span><span class="sxs-lookup"><span data-stu-id="5963d-220">3</span></span>|<span data-ttu-id="5963d-221">**Nombre de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="5963d-221">**App name**</span></span>|
|<span data-ttu-id="5963d-222">4 </span><span class="sxs-lookup"><span data-stu-id="5963d-222">4</span></span>|<span data-ttu-id="5963d-223">**Botón Cerrar:** descarta el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5963d-223">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="5963d-224">5 </span><span class="sxs-lookup"><span data-stu-id="5963d-224">5</span></span>|<span data-ttu-id="5963d-225">**Cadena de acción:** normalmente describe quién inició el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5963d-225">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior"></a><span data-ttu-id="5963d-226">Comportamiento dinámico</span><span class="sxs-lookup"><span data-stu-id="5963d-226">Responsive behavior</span></span>

<span data-ttu-id="5963d-227">Los cuadros de diálogo en reunión pueden variar en tamaño para tener en cuenta diferentes escenarios.</span><span class="sxs-lookup"><span data-stu-id="5963d-227">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="5963d-228">Asegúrese de mantener el relleno y los tamaños de los componentes.</span><span class="sxs-lookup"><span data-stu-id="5963d-228">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="5963d-229">**Width:** puede especificar el ancho del iframe del cuadro de diálogo en cualquier lugar dentro del intervalo de tamaño admitido.</span><span class="sxs-lookup"><span data-stu-id="5963d-229">**Width**: You can specify the width of the dialog's iframe anywhere within the supported size range.</span></span>
* <span data-ttu-id="5963d-230">**Alto:** puede especificar el alto del iframe del cuadro de diálogo en cualquier lugar dentro del intervalo de tamaño admitido.</span><span class="sxs-lookup"><span data-stu-id="5963d-230">**Height**: You can specify the height of the dialog's iframe anywhere within the supported size range.</span></span> <span data-ttu-id="5963d-231">También puedes permitir que los usuarios se desplacen verticalmente si el contenido de la aplicación supera el alto máximo.</span><span class="sxs-lookup"><span data-stu-id="5963d-231">You also can allow users to scroll vertically if your app content exceeds the maximum height.</span></span>

<span data-ttu-id="5963d-232">Para implementar, especifique el ancho y el alto con la [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) clave.</span><span class="sxs-lookup"><span data-stu-id="5963d-232">To implement, specify the width and height using the [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) key.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="En el ejemplo se muestra el cuadro de diálogo en la reunión. Ancho: Min-280 píxeles (248 píxeles iframe). Máximo: 460 píxeles (428 píxeles de iframe). Alto: 300 píxeles (iframe)." border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="5963d-234">Después de una reunión</span><span class="sxs-lookup"><span data-stu-id="5963d-234">After a meeting</span></span>

<span data-ttu-id="5963d-235">Puedes volver a una reunión después de que finalice y ver el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5963d-235">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="5963d-236">En este ejemplo, el organizador de la reunión puede ver los resultados del sondeo en la pestaña **Contoso.** (Nota: Desde el punto de vista del diseño, no hay diferencia entre una experiencia de pestaña anterior y posterior a la reunión).</span><span class="sxs-lookup"><span data-stu-id="5963d-236">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="La ilustración de ejemplo muestra una pestaña posterior a la reunión." border="false":::

## <a name="best-practices"></a><span data-ttu-id="5963d-238">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="5963d-238">Best practices</span></span>

<span data-ttu-id="5963d-239">Usa estas recomendaciones para crear una experiencia de aplicación de calidad.</span><span class="sxs-lookup"><span data-stu-id="5963d-239">Use these recommendations to create a quality app experience.</span></span>

### <a name="interactions"></a><span data-ttu-id="5963d-240">Interacciones</span><span class="sxs-lookup"><span data-stu-id="5963d-240">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Ejemplo que muestra cómo limitar el número de interacciones." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="5963d-242">Hacer: limitar el número de interacciones</span><span class="sxs-lookup"><span data-stu-id="5963d-242">Do: Limit the number of interactions</span></span>

<span data-ttu-id="5963d-243">Para los cuadros de diálogo en la reunión, quite el contenido innecesario que no ayuda a los usuarios a lograr algo rápidamente.</span><span class="sxs-lookup"><span data-stu-id="5963d-243">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Ejemplo que muestra cómo no introducir elementos innecesarios." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="5963d-245">No: introducir elementos innecesarios</span><span class="sxs-lookup"><span data-stu-id="5963d-245">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="5963d-246">Un único cuadro de diálogo en la reunión con varias interacciones puede distraerse de la llamada.</span><span class="sxs-lookup"><span data-stu-id="5963d-246">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="5963d-247">Diseño</span><span class="sxs-lookup"><span data-stu-id="5963d-247">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Ejemplo que muestra cómo debe usar un diseño de cuadro de diálogo de una columna." border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a><span data-ttu-id="5963d-249">Hacer: Usar un diseño de cuadro de diálogo de una columna</span><span class="sxs-lookup"><span data-stu-id="5963d-249">Do: Use a single-column dialog layout</span></span>

<span data-ttu-id="5963d-250">Dado que los cuadros de diálogo están en el centro de la fase de reunión, la finalización de tareas debe ser rápida y sencilla para evitar la frustración del usuario.</span><span class="sxs-lookup"><span data-stu-id="5963d-250">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Ejemplo que muestra que no debe saturar el espacio de una extensión de reunión." border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="5963d-252">No: saturar el espacio</span><span class="sxs-lookup"><span data-stu-id="5963d-252">Don't: Clutter the space</span></span>

<span data-ttu-id="5963d-253">El contenido densa o demasiado estructurado puede ser molesto y abrumador, especialmente durante una reunión.</span><span class="sxs-lookup"><span data-stu-id="5963d-253">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Ejemplo que muestra un diseño de pestaña de una columna." border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a><span data-ttu-id="5963d-255">Hacer: Usar un diseño de pestaña de una columna</span><span class="sxs-lookup"><span data-stu-id="5963d-255">Do: Use a single-column tab layout</span></span>

<span data-ttu-id="5963d-256">Dada la naturaleza estrecha de la pestaña en la reunión, se recomienda encarecidamente mostrar el contenido en una sola columna.</span><span class="sxs-lookup"><span data-stu-id="5963d-256">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Ejemplo que muestra una pestaña con varias columnas." border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="5963d-258">No: usar varias columnas</span><span class="sxs-lookup"><span data-stu-id="5963d-258">Don't: Use multiple columns</span></span>

<span data-ttu-id="5963d-259">Debido al espacio limitado de la pestaña en la reunión, no se recomiendan diseños con más de una columna.</span><span class="sxs-lookup"><span data-stu-id="5963d-259">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="5963d-260">Controles</span><span class="sxs-lookup"><span data-stu-id="5963d-260">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Ejemplo que muestra cómo alinear correctamente los controles principales." border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="5963d-262">Hacer: alinear a la derecha la acción principal</span><span class="sxs-lookup"><span data-stu-id="5963d-262">Do: Right align the primary action</span></span>

<span data-ttu-id="5963d-263">Se recomienda colocar la acción más intensa visualmente en la ubicación más derecha.</span><span class="sxs-lookup"><span data-stu-id="5963d-263">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Ejemplo que muestra cómo no debe dejar alineados los controles principales." border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="5963d-265">No: acciones de alineación izquierda o central</span><span class="sxs-lookup"><span data-stu-id="5963d-265">Don't: Left or center align actions</span></span>

<span data-ttu-id="5963d-266">Esto se desvía del patrón de Teams estándar para la colocación de controles en un cuadro de diálogo y puede conflicto con un cuadro de diálogo detrás del superior.</span><span class="sxs-lookup"><span data-stu-id="5963d-266">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scroll"></a><span data-ttu-id="5963d-267">Scroll</span><span class="sxs-lookup"><span data-stu-id="5963d-267">Scroll</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Ejemplo que muestra el desplazamiento vertical en una pestaña en reunión." border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="5963d-269">Hacer: desplazarse verticalmente</span><span class="sxs-lookup"><span data-stu-id="5963d-269">Do: Scroll vertically</span></span>

<span data-ttu-id="5963d-270">Los usuarios esperan desplazamiento vertical en Teams (y en otros lugares).</span><span class="sxs-lookup"><span data-stu-id="5963d-270">Users expect vertical scrolling in Teams (and elsewhere).</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Ejemplo que muestra el desplazamiento horizontal en una pestaña en la reunión." border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="5963d-272">No: desplazarse horizontalmente</span><span class="sxs-lookup"><span data-stu-id="5963d-272">Don't: Scroll horizontally</span></span>

<span data-ttu-id="5963d-273">El desplazamiento horizontal no es un comportamiento esperado en Teams.</span><span class="sxs-lookup"><span data-stu-id="5963d-273">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="5963d-274">Otros lienzos del entorno de reunión se desplazan verticalmente.</span><span class="sxs-lookup"><span data-stu-id="5963d-274">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="5963d-275">Flujos de trabajo</span><span class="sxs-lookup"><span data-stu-id="5963d-275">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Ejemplo que muestra un escenario complejo en una pestaña de reunión." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="5963d-277">Hacer: escenarios complejos de Surface en la pestaña en reunión</span><span class="sxs-lookup"><span data-stu-id="5963d-277">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="5963d-278">Si la aplicación incluye varias tareas, recomendamos encarecidamente usar una pestaña en la reunión con un diseño de una sola columna.</span><span class="sxs-lookup"><span data-stu-id="5963d-278">If your app includes multiple tasks, we strongly recommend using an in-meeting tab with a single-column layout.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Ejemplo que muestra escenarios complejos en un cuadro de diálogo en la reunión." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a><span data-ttu-id="5963d-280">Don't: Hacer complejos los cuadros de diálogo en la reunión</span><span class="sxs-lookup"><span data-stu-id="5963d-280">Don't: Make in-meeting dialogs complex</span></span>

<span data-ttu-id="5963d-281">Los cuadros de diálogo en reunión están diseñados para interacciones breves.</span><span class="sxs-lookup"><span data-stu-id="5963d-281">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="5963d-282">Creación de temas</span><span class="sxs-lookup"><span data-stu-id="5963d-282">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Ejemplo que muestra una extensión de reunión con el tema oscuro." border="false":::

#### <a name="do-use-teams-color-tokens"></a><span data-ttu-id="5963d-284">Do: Use Teams tokens de color</span><span class="sxs-lookup"><span data-stu-id="5963d-284">Do: Use Teams color tokens</span></span>

<span data-ttu-id="5963d-285">Teams reuniones están optimizadas para el modo oscuro para ayudar a reducir el ruido visual y cognitivo para que los usuarios puedan centrarse en la discusión y el contenido compartido.</span><span class="sxs-lookup"><span data-stu-id="5963d-285">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="5963d-286">Obtenga información sobre <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">el uso de tokens de color (Fluent UI)</a>.</span><span class="sxs-lookup"><span data-stu-id="5963d-286">Learn about using <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a>.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Ejemplo que muestra una extensión de reunión con un tema predeterminado (claro)." border="false":::

#### <a name="dont-hard-code-hex-values"></a><span data-ttu-id="5963d-288">No: valores hexadecimales de código duro</span><span class="sxs-lookup"><span data-stu-id="5963d-288">Don't: Hard code hex values</span></span>

<span data-ttu-id="5963d-289">Si no usas tokens Teams de color, tus diseños serán menos escalables y tendrán más tiempo para administrar.</span><span class="sxs-lookup"><span data-stu-id="5963d-289">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="5963d-290">Navegación</span><span class="sxs-lookup"><span data-stu-id="5963d-290">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Ejemplo que muestra una extensión de reunión con un botón Atrás." border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="5963d-292">Hacer: Tener un botón atrás</span><span class="sxs-lookup"><span data-stu-id="5963d-292">Do: Have a back button</span></span>

<span data-ttu-id="5963d-293">Si tiene más de una capa de navegación en una pestaña de reunión, los usuarios deben poder volver a sus vistas anteriores.</span><span class="sxs-lookup"><span data-stu-id="5963d-293">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Ejemplo que muestra una extensión de reunión con dos botones de descarte." border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="5963d-295">No: incluir otro botón descartar</span><span class="sxs-lookup"><span data-stu-id="5963d-295">Don't: Include another dismiss button</span></span>

<span data-ttu-id="5963d-296">Proporcionar una opción para cerrar el contenido de la pestaña en la reunión puede causar problemas, ya que ya hay un botón en el encabezado para descartar la propia pestaña en la reunión.</span><span class="sxs-lookup"><span data-stu-id="5963d-296">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Ejemplo que muestra modales (o módulos de tareas) dentro de una pestaña en la reunión." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="5963d-298">Precaución: evite los modales dentro de la pestaña en la reunión</span><span class="sxs-lookup"><span data-stu-id="5963d-298">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="5963d-299">Los modales (también conocidos como módulos de tareas) en la pestaña ya estrecha en la reunión podrían ajustar y oscurecer el contenido.</span><span class="sxs-lookup"><span data-stu-id="5963d-299">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

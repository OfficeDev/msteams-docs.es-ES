---
title: Diseño de la extensión de reunión
author: heath-hamilton
description: Obtén información sobre cómo diseñar aplicaciones en Teams reuniones y obtener el kit Microsoft Teams interfaz de usuario.
ms.author: lajanuar
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 7196017f92bebb776d1b73680893ebfe3684a74c
ms.sourcegitcommit: 6e4d2c8e99426125f7b72b9640ee4a4b4f374401
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/24/2021
ms.locfileid: "53114352"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="ef75f-103">Diseño de la extensión Microsoft Teams reunión</span><span class="sxs-lookup"><span data-stu-id="ef75f-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="ef75f-104">Puedes crear aplicaciones para que las reuniones sean más productivas.</span><span class="sxs-lookup"><span data-stu-id="ef75f-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="ef75f-105">Por ejemplo, pida a los usuarios que completen una encuesta durante una llamada o envíen un aviso rápido que no interrumpa el flujo de la reunión.</span><span class="sxs-lookup"><span data-stu-id="ef75f-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="ef75f-106">Kit de interfaz de usuario de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ef75f-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="ef75f-107">Puedes encontrar instrucciones de diseño más completas, incluidos los elementos que puedes agarrar y modificar según sea necesario, en el kit de interfaz Microsoft Teams usuario.</span><span class="sxs-lookup"><span data-stu-id="ef75f-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ef75f-108">Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="ef75f-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="ef75f-109">Agregar una extensión de reunión</span><span class="sxs-lookup"><span data-stu-id="ef75f-109">Add a meeting extension</span></span>

<span data-ttu-id="ef75f-110">Los usuarios pueden agregar una extensión de reunión antes y durante las reuniones.</span><span class="sxs-lookup"><span data-stu-id="ef75f-110">Users can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="ef75f-111">También pueden agregar una aplicación para una reunión específica directamente desde Teams tienda.</span><span class="sxs-lookup"><span data-stu-id="ef75f-111">They also can add an app for a specific meeting directly from the Teams store.</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="ef75f-112">Agregar antes de una reunión</span><span class="sxs-lookup"><span data-stu-id="ef75f-112">Add before a meeting</span></span>

<span data-ttu-id="ef75f-113">En los detalles de la reunión, los usuarios pueden seleccionar **Agregar una** pestaña + para abrir el control desplegable de la aplicación y buscar aplicaciones optimizadas para reuniones.</span><span class="sxs-lookup"><span data-stu-id="ef75f-113">In the meeting details, users can select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de reunión antes de una reunión." border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="ef75f-115">Agregar durante una reunión</span><span class="sxs-lookup"><span data-stu-id="ef75f-115">Add during a meeting</span></span>

# <a name="desktop"></a>[<span data-ttu-id="ef75f-116">Escritorio</span><span class="sxs-lookup"><span data-stu-id="ef75f-116">Desktop</span></span>](#tab/desktop)

En una reunión, los usuarios pueden seleccionar **Más** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **agregar una aplicación** y elegir la aplicación que desean.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de reunión durante una reunión." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="ef75f-119">Móvil</span><span class="sxs-lookup"><span data-stu-id="ef75f-119">Mobile</span></span>](#tab/mobile)

En una reunión, los usuarios pueden seleccionar **Más** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: y elegir la aplicación que desean.

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-add-during-meeting.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de reunión durante una reunión en el móvil." border="false":::

---

## <a name="before-a-meeting"></a><span data-ttu-id="ef75f-122">Antes de una reunión</span><span class="sxs-lookup"><span data-stu-id="ef75f-122">Before a meeting</span></span>

<span data-ttu-id="ef75f-123">Antes de una reunión, los usuarios pueden agregar contenido en la pestaña. En el siguiente ejemplo se muestra un borrador de pregunta de encuesta que los usuarios responderán durante la llamada.</span><span class="sxs-lookup"><span data-stu-id="ef75f-123">Prior to a meeting, users can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="En el ejemplo se muestra cómo usar el contenido de la aplicación en los detalles de la reunión antes de una llamada." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="ef75f-125">Anatomía: pestaña Reunión (antes y después de las reuniones)</span><span class="sxs-lookup"><span data-stu-id="ef75f-125">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de una pestaña de reunión antes y después de una reunión." border="false":::

|<span data-ttu-id="ef75f-127">Contador</span><span class="sxs-lookup"><span data-stu-id="ef75f-127">Counter</span></span>|<span data-ttu-id="ef75f-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="ef75f-128">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="ef75f-129">1</span><span class="sxs-lookup"><span data-stu-id="ef75f-129">1</span></span>|<span data-ttu-id="ef75f-130">**Nombre de la pestaña:** etiqueta de navegación para la pestaña.</span><span class="sxs-lookup"><span data-stu-id="ef75f-130">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="ef75f-131">2 </span><span class="sxs-lookup"><span data-stu-id="ef75f-131">2</span></span>|<span data-ttu-id="ef75f-132">**Desbordamiento de** tabulación: abre acciones de tabulación, como cambiar el nombre y quitar.</span><span class="sxs-lookup"><span data-stu-id="ef75f-132">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="ef75f-133">3 </span><span class="sxs-lookup"><span data-stu-id="ef75f-133">3</span></span>|<span data-ttu-id="ef75f-134">**iframe:** muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ef75f-134">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="ef75f-135">Diseño con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="ef75f-135">Designing with UI templates</span></span>

<span data-ttu-id="ef75f-136">Usa una de las siguientes plantillas Teams interfaz de usuario para ayudar a diseñar la pestaña de reunión:</span><span class="sxs-lookup"><span data-stu-id="ef75f-136">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="ef75f-137">[Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato digitalizado y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="ef75f-137">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="ef75f-138">[Panel de](../../concepts/design/design-teams-app-ui-templates.md#task-board)tareas: un panel de tareas, a veces denominado tablero de kanban o carriles de natación, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o los vales.</span><span class="sxs-lookup"><span data-stu-id="ef75f-138">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="ef75f-139">[Panel:](../../concepts/design/design-teams-app-ui-templates.md#dashboard)un panel es un lienzo que contiene varias tarjetas que proporcionan información general sobre los datos o el contenido.</span><span class="sxs-lookup"><span data-stu-id="ef75f-139">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="ef75f-140">[Formulario:](../../concepts/design/design-teams-app-ui-templates.md#form)los formularios son para recopilar, validar y enviar la entrada del usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="ef75f-140">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="ef75f-141">[Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacío se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.</span><span class="sxs-lookup"><span data-stu-id="ef75f-141">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="ef75f-142">[Navegación izquierda:](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav)el componente de navegación izquierdo puede ayudar si la pestaña requiere algo de navegación.</span><span class="sxs-lookup"><span data-stu-id="ef75f-142">[Left nav](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav): The left nav component can help if your tab requires some navigation.</span></span> <span data-ttu-id="ef75f-143">En general, debe mantener la navegación al mínimo.</span><span class="sxs-lookup"><span data-stu-id="ef75f-143">In general, you should keep navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="ef75f-144">Usar una pestaña en la reunión</span><span class="sxs-lookup"><span data-stu-id="ef75f-144">Use an in-meeting tab</span></span>

<span data-ttu-id="ef75f-145">La pestaña en la reunión es un lienzo para aumentar la colaboración durante las reuniones.</span><span class="sxs-lookup"><span data-stu-id="ef75f-145">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="ef75f-146">Los asistentes pueden ver e interactuar con el contenido de la aplicación en un espacio dedicado fuera de la fase de reunión a través de vistas compartidas o basadas en roles.</span><span class="sxs-lookup"><span data-stu-id="ef75f-146">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="ef75f-147">Casos de uso</span><span class="sxs-lookup"><span data-stu-id="ef75f-147">Use cases</span></span>

<span data-ttu-id="ef75f-148">Las personas pueden usar la pestaña en la reunión para:</span><span class="sxs-lookup"><span data-stu-id="ef75f-148">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="ef75f-149">Proporcionar comentarios detallados.</span><span class="sxs-lookup"><span data-stu-id="ef75f-149">Provide detailed feedback.</span></span> <span data-ttu-id="ef75f-150">Por ejemplo, evalúe un candidato de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ef75f-150">For example, evaluate a job candidate.</span></span>
* <span data-ttu-id="ef75f-151">Cree un sondeo, una encuesta o un elemento de tarea para los participantes de la reunión.</span><span class="sxs-lookup"><span data-stu-id="ef75f-151">Create a poll, survey, or task item for the meeting participants.</span></span>
* <span data-ttu-id="ef75f-152">Mostrar notas relevantes para la reunión.</span><span class="sxs-lookup"><span data-stu-id="ef75f-152">Display notes relevant to the meeting.</span></span> <span data-ttu-id="ef75f-153">Por ejemplo, información sobre un cliente potencial de ventas.</span><span class="sxs-lookup"><span data-stu-id="ef75f-153">For example, information about a sales lead.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="ef75f-154">Escritorio</span><span class="sxs-lookup"><span data-stu-id="ef75f-154">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="En el ejemplo se muestra cómo se puede presentar contenido de sondeo en una pestaña en la reunión." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="ef75f-156">Móvil</span><span class="sxs-lookup"><span data-stu-id="ef75f-156">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-tab.png" alt-text="En el ejemplo se muestra cómo se puede presentar contenido de sondeo en una pestaña de reunión en el móvil." border="false":::

---

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="ef75f-158">Anatomía: pestaña En la reunión</span><span class="sxs-lookup"><span data-stu-id="ef75f-158">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de una pestaña en reunión." border="false":::

|<span data-ttu-id="ef75f-160">Contador</span><span class="sxs-lookup"><span data-stu-id="ef75f-160">Counter</span></span>|<span data-ttu-id="ef75f-161">Descripción</span><span class="sxs-lookup"><span data-stu-id="ef75f-161">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="ef75f-162">1</span><span class="sxs-lookup"><span data-stu-id="ef75f-162">1</span></span>|<span data-ttu-id="ef75f-163">**Icono de aplicación (seleccionado):** logotipo de aplicación transparente de 16 píxeles.</span><span class="sxs-lookup"><span data-stu-id="ef75f-163">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="ef75f-164">2 </span><span class="sxs-lookup"><span data-stu-id="ef75f-164">2</span></span>|<span data-ttu-id="ef75f-165">**Nombre de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="ef75f-165">**App name**</span></span>|
|<span data-ttu-id="ef75f-166">3 </span><span class="sxs-lookup"><span data-stu-id="ef75f-166">3</span></span>|<span data-ttu-id="ef75f-167">**Encabezado:** incluye el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ef75f-167">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="ef75f-168">4 </span><span class="sxs-lookup"><span data-stu-id="ef75f-168">4</span></span>|<span data-ttu-id="ef75f-169">**Botón Cerrar:** descarta la pestaña. Use siempre el icono de cierre superior derecho en lugar de una acción en el pie de página.</span><span class="sxs-lookup"><span data-stu-id="ef75f-169">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="ef75f-170">5 </span><span class="sxs-lookup"><span data-stu-id="ef75f-170">5</span></span>|<span data-ttu-id="ef75f-171">**Barra de notificaciones:** las alertas de error se muestran directamente debajo del encabezado y presionan el contenido del iframe hacia abajo en 20 píxeles.</span><span class="sxs-lookup"><span data-stu-id="ef75f-171">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="ef75f-172">6 </span><span class="sxs-lookup"><span data-stu-id="ef75f-172">6</span></span>|<span data-ttu-id="ef75f-173">**iframe:** muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ef75f-173">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="ef75f-174">Spacing</span><span class="sxs-lookup"><span data-stu-id="ef75f-174">Spacing</span></span>

<span data-ttu-id="ef75f-175">Optimiza la pestaña en la reunión para que se ajuste de un extremo a otro dentro del área de iframe de 280 píxeles.</span><span class="sxs-lookup"><span data-stu-id="ef75f-175">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="ef75f-176">Hay 20 píxeles de relleno en los lados izquierdo y derecho del iframe y entre el encabezado de pestaña.</span><span class="sxs-lookup"><span data-stu-id="ef75f-176">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="ef75f-177">El iframe está sangrando hasta la parte inferior de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="ef75f-177">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="En el ejemplo se muestran las dimensiones de espaciado de tabulación en la reunión." border="false":::

### <a name="scrolling"></a><span data-ttu-id="ef75f-179">Desplazamiento</span><span class="sxs-lookup"><span data-stu-id="ef75f-179">Scrolling</span></span>

<span data-ttu-id="ef75f-180">Recuerde lo siguiente si permite el desplazamiento:</span><span class="sxs-lookup"><span data-stu-id="ef75f-180">Remember the following if you allow scrolling:</span></span>

* <span data-ttu-id="ef75f-181">El contenido del iframe solo debe desplazarse verticalmente.</span><span class="sxs-lookup"><span data-stu-id="ef75f-181">Content in the iframe contents should only scroll vertically.</span></span>
* <span data-ttu-id="ef75f-182">Los usuarios solo deben ver el contenido al que se han desplazado (nada por encima o por debajo).</span><span class="sxs-lookup"><span data-stu-id="ef75f-182">Users should only see the content they've scrolled to (nothing above or below).</span></span> 
* <span data-ttu-id="ef75f-183">La barra de desplazamiento forma parte del contenido de iframe.</span><span class="sxs-lookup"><span data-stu-id="ef75f-183">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="En el ejemplo se muestra cómo se desplaza la pestaña en la reunión." border="false":::

### <a name="navigation"></a><span data-ttu-id="ef75f-185">Navegación</span><span class="sxs-lookup"><span data-stu-id="ef75f-185">Navigation</span></span>

<span data-ttu-id="ef75f-186">Para escenarios con capas de navegación o contenido intenso, se recomienda permitir a los usuarios navegar a una capa secundaria.</span><span class="sxs-lookup"><span data-stu-id="ef75f-186">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="ef75f-187">Los usuarios deben poder volver a la capa anterior.</span><span class="sxs-lookup"><span data-stu-id="ef75f-187">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="En el ejemplo se muestra la navegación en la reunión." border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="ef75f-189">Usar un cuadro de diálogo en la reunión</span><span class="sxs-lookup"><span data-stu-id="ef75f-189">Use an in-meeting dialog</span></span>

<span data-ttu-id="ef75f-190">Los cuadros de diálogo en la reunión se muestran en la Teams de reunión.</span><span class="sxs-lookup"><span data-stu-id="ef75f-190">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="ef75f-191">Requieren la atención, confirmación o interacción de un usuario, pero son sutiles y no interrumpen la reunión.</span><span class="sxs-lookup"><span data-stu-id="ef75f-191">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="ef75f-192">Debe usarlos con moderación y para escenarios orientados a tareas y ligeras.</span><span class="sxs-lookup"><span data-stu-id="ef75f-192">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="ef75f-193">Casos de uso</span><span class="sxs-lookup"><span data-stu-id="ef75f-193">Use cases</span></span>

<span data-ttu-id="ef75f-194">Los cuadros de diálogo en la reunión son desencadenados por un usuario (como el organizador de la reunión) que puede querer que los participantes:</span><span class="sxs-lookup"><span data-stu-id="ef75f-194">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="ef75f-195">Proporcionar comentarios breves</span><span class="sxs-lookup"><span data-stu-id="ef75f-195">Provide brief feedback</span></span>
* <span data-ttu-id="ef75f-196">Realizar una encuesta o sondeo breves</span><span class="sxs-lookup"><span data-stu-id="ef75f-196">Take a short survey or poll</span></span>
* <span data-ttu-id="ef75f-197">Enviar aprobaciones</span><span class="sxs-lookup"><span data-stu-id="ef75f-197">Submit approvals</span></span>
* <span data-ttu-id="ef75f-198">Recibir recordatorios</span><span class="sxs-lookup"><span data-stu-id="ef75f-198">Get reminders</span></span>

# <a name="desktop"></a>[<span data-ttu-id="ef75f-199">Escritorio</span><span class="sxs-lookup"><span data-stu-id="ef75f-199">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="En el ejemplo se muestra cómo se puede usar un cuadro de diálogo en la reunión." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="ef75f-201">Móvil</span><span class="sxs-lookup"><span data-stu-id="ef75f-201">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-dialog.png" alt-text="En el ejemplo se muestra cómo se puede usar un cuadro de diálogo en la reunión en el móvil." border="false":::

---

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="ef75f-203">Anatomía: cuadro de diálogo en la reunión</span><span class="sxs-lookup"><span data-stu-id="ef75f-203">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de un cuadro de diálogo en reunión." border="false":::

|<span data-ttu-id="ef75f-205">Contador</span><span class="sxs-lookup"><span data-stu-id="ef75f-205">Counter</span></span>|<span data-ttu-id="ef75f-206">Descripción</span><span class="sxs-lookup"><span data-stu-id="ef75f-206">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="ef75f-207">1</span><span class="sxs-lookup"><span data-stu-id="ef75f-207">1</span></span>|<span data-ttu-id="ef75f-208">**Encabezado:** incluye el icono de la aplicación, el nombre, la cadena de acción y el icono cerrar.</span><span class="sxs-lookup"><span data-stu-id="ef75f-208">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="ef75f-209">2 </span><span class="sxs-lookup"><span data-stu-id="ef75f-209">2</span></span>|<span data-ttu-id="ef75f-210">**iframe:** muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ef75f-210">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="ef75f-211">Anatomía: encabezado del cuadro de diálogo En la reunión</span><span class="sxs-lookup"><span data-stu-id="ef75f-211">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de un encabezado de cuadro de diálogo en reunión." border="false":::

<span data-ttu-id="ef75f-213">Hay dos variantes de encabezado.</span><span class="sxs-lookup"><span data-stu-id="ef75f-213">There are two header variants.</span></span> <span data-ttu-id="ef75f-214">Cuando sea posible, usa la variante con el avatar para reforzar que el cuadro de diálogo viene de una persona.</span><span class="sxs-lookup"><span data-stu-id="ef75f-214">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="ef75f-215">Contador</span><span class="sxs-lookup"><span data-stu-id="ef75f-215">Counter</span></span>|<span data-ttu-id="ef75f-216">Descripción</span><span class="sxs-lookup"><span data-stu-id="ef75f-216">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="ef75f-217">1</span><span class="sxs-lookup"><span data-stu-id="ef75f-217">1</span></span>|<span data-ttu-id="ef75f-218">**Avatar:** persona que inicia el cuadro de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="ef75f-218">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="ef75f-219">2 </span><span class="sxs-lookup"><span data-stu-id="ef75f-219">2</span></span>|<span data-ttu-id="ef75f-220">**Icono de aplicación**</span><span class="sxs-lookup"><span data-stu-id="ef75f-220">**App icon**</span></span>|
|<span data-ttu-id="ef75f-221">3 </span><span class="sxs-lookup"><span data-stu-id="ef75f-221">3</span></span>|<span data-ttu-id="ef75f-222">**Nombre de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="ef75f-222">**App name**</span></span>|
|<span data-ttu-id="ef75f-223">4 </span><span class="sxs-lookup"><span data-stu-id="ef75f-223">4</span></span>|<span data-ttu-id="ef75f-224">**Botón Cerrar:** descarta el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ef75f-224">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="ef75f-225">5 </span><span class="sxs-lookup"><span data-stu-id="ef75f-225">5</span></span>|<span data-ttu-id="ef75f-226">**Cadena de acción:** normalmente describe quién inició el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ef75f-226">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior-in-meeting-dialogs"></a><span data-ttu-id="ef75f-227">Comportamiento dinámico: cuadros de diálogo en la reunión</span><span class="sxs-lookup"><span data-stu-id="ef75f-227">Responsive behavior: In-meeting dialogs</span></span>

<span data-ttu-id="ef75f-228">Los cuadros de diálogo en reunión pueden variar en tamaño para tener en cuenta diferentes escenarios.</span><span class="sxs-lookup"><span data-stu-id="ef75f-228">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="ef75f-229">Asegúrese de mantener el relleno y los tamaños de los componentes.</span><span class="sxs-lookup"><span data-stu-id="ef75f-229">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="ef75f-230">**Width:** puede especificar el ancho del iframe del cuadro de diálogo en cualquier lugar dentro del intervalo de tamaño admitido.</span><span class="sxs-lookup"><span data-stu-id="ef75f-230">**Width**: You can specify the width of the dialog's iframe anywhere within the supported size range.</span></span>
* <span data-ttu-id="ef75f-231">**Alto:** puede especificar el alto del iframe del cuadro de diálogo en cualquier lugar dentro del intervalo de tamaño admitido.</span><span class="sxs-lookup"><span data-stu-id="ef75f-231">**Height**: You can specify the height of the dialog's iframe anywhere within the supported size range.</span></span> <span data-ttu-id="ef75f-232">También puedes permitir que los usuarios se desplacen verticalmente si el contenido de la aplicación supera el alto máximo.</span><span class="sxs-lookup"><span data-stu-id="ef75f-232">You also can allow users to scroll vertically if your app content exceeds the maximum height.</span></span>

<span data-ttu-id="ef75f-233">Para implementar, especifique el ancho y el alto con la [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) clave.</span><span class="sxs-lookup"><span data-stu-id="ef75f-233">To implement, specify the width and height using the [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) key.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="En el ejemplo se muestra el cuadro de diálogo en la reunión. Ancho: Min-280 píxeles (248 píxeles iframe). Máximo: 460 píxeles (428 píxeles de iframe). Alto: 300 píxeles (iframe)." border="false":::

## <a name="use-the-shared-meeting-stage"></a><span data-ttu-id="ef75f-235">Usar la fase de reunión compartida</span><span class="sxs-lookup"><span data-stu-id="ef75f-235">Use the shared meeting stage</span></span>

<span data-ttu-id="ef75f-236">La fase de reunión compartida ayuda a los participantes a interactuar y colaborar en el contenido de la aplicación en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="ef75f-236">Shared meeting stage helps meeting participants interact with and collaborate on app content in real-time.</span></span> <span data-ttu-id="ef75f-237">Por ejemplo, los usuarios pueden centrar su llamada en editar un documento, hacer una lluvia de ideas con una pizarra o revisar un panel.</span><span class="sxs-lookup"><span data-stu-id="ef75f-237">For example, users can focus their call on editing a document, brainstorming with a whiteboard, or reviewing a dashboard.</span></span>

<span data-ttu-id="ef75f-238">Las aplicaciones compartidas en la fase de reunión ocupan el mismo espacio que una pantalla compartida.</span><span class="sxs-lookup"><span data-stu-id="ef75f-238">Apps shared to the meeting stage occupy the same space as a shared screen.</span></span> <span data-ttu-id="ef75f-239">La fase se vuelve a reorientar para todos los participantes de la reunión.</span><span class="sxs-lookup"><span data-stu-id="ef75f-239">The stage reorients for all meeting participants.</span></span>

### <a name="use-cases"></a><span data-ttu-id="ef75f-240">Casos de uso</span><span class="sxs-lookup"><span data-stu-id="ef75f-240">Use cases</span></span>

<span data-ttu-id="ef75f-241">La fase de reunión compartida tiene que ver con la colaboración y la participación.</span><span class="sxs-lookup"><span data-stu-id="ef75f-241">The shared meeting stage is all about collaboration and participation.</span></span> <span data-ttu-id="ef75f-242">Estos son algunos escenarios de ejemplo que le ayudarán a empezar.</span><span class="sxs-lookup"><span data-stu-id="ef75f-242">Here are some example scenarios to help you get started.</span></span>

:::row:::
   :::column span="1":::

<span data-ttu-id="ef75f-243">**Editar y revisar:** profundizar en los paneles y planear con todos los usuarios de la llamada.</span><span class="sxs-lookup"><span data-stu-id="ef75f-243">**Edit and review**: Dive into dashboards and planning with everyone on the call.</span></span>

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-edit-review.png" alt-text="En el ejemplo se muestra un panel que se está revisando en la fase de reunión compartida." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

<span data-ttu-id="ef75f-245">**Pizarra:** dibujar e idear juntos en un lienzo compartido.</span><span class="sxs-lookup"><span data-stu-id="ef75f-245">**Whiteboard**: Draw and ideate together on a shared canvas.</span></span>

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-whiteboard.png" alt-text="En el ejemplo se muestra una pizarra en la fase de reunión compartida." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

<span data-ttu-id="ef75f-247">**Cuestionario:** Pruebe los conocimientos y obtenga información con materiales interactivos.</span><span class="sxs-lookup"><span data-stu-id="ef75f-247">**Quiz**: Test knowledge and gain insights with interactive materials.</span></span>

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-quiz.png" alt-text="En el ejemplo se muestra un cuestionario en la fase de reunión compartida." border="false":::

   :::column-end:::
:::row-end:::

### <a name="anatomy-shared-meeting-stage"></a><span data-ttu-id="ef75f-249">Anatomía: fase de reunión compartida</span><span class="sxs-lookup"><span data-stu-id="ef75f-249">Anatomy: Shared meeting stage</span></span>

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-anatomy.png" alt-text="La imagen muestra la anatomía de diseño de la fase de reunión compartida." border="false":::

|<span data-ttu-id="ef75f-251">Contador</span><span class="sxs-lookup"><span data-stu-id="ef75f-251">Counter</span></span>|<span data-ttu-id="ef75f-252">Descripción</span><span class="sxs-lookup"><span data-stu-id="ef75f-252">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="ef75f-253">1</span><span class="sxs-lookup"><span data-stu-id="ef75f-253">1</span></span>|<span data-ttu-id="ef75f-254">**Icono de la** aplicación: el icono resaltado indica que la pestaña en la reunión de la aplicación está abierta.</span><span class="sxs-lookup"><span data-stu-id="ef75f-254">**App icon**: The highlighted icon indicates the app's in-meeting tab is open.</span></span>|
|<span data-ttu-id="ef75f-255">2 </span><span class="sxs-lookup"><span data-stu-id="ef75f-255">2</span></span>|<span data-ttu-id="ef75f-256">**Botón Compartir a fase de reunión:** punto de entrada para compartir la aplicación a la fase de reunión.</span><span class="sxs-lookup"><span data-stu-id="ef75f-256">**Share to meeting stage button**: The entry point to share the app to the meeting stage.</span></span> <span data-ttu-id="ef75f-257">Muestra si configuras la aplicación para que use la fase de reunión compartida.</span><span class="sxs-lookup"><span data-stu-id="ef75f-257">Displays if you configure your app to use the shared meeting stage.</span></span>|
|<span data-ttu-id="ef75f-258">3 </span><span class="sxs-lookup"><span data-stu-id="ef75f-258">3</span></span>|<span data-ttu-id="ef75f-259">**iframe:** muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ef75f-259">**iframe**: Displays your app content.</span></span>|
|<span data-ttu-id="ef75f-260">4 </span><span class="sxs-lookup"><span data-stu-id="ef75f-260">4</span></span>|<span data-ttu-id="ef75f-261">**Botón Detener uso compartido:** deja de compartir la aplicación en la fase de reunión.</span><span class="sxs-lookup"><span data-stu-id="ef75f-261">**Stop sharing button**: Stops sharing the app to the meeting stage.</span></span> <span data-ttu-id="ef75f-262">Solo se muestra para el participante que inició el recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="ef75f-262">Displays only for the participant who started the share.</span></span>|
|<span data-ttu-id="ef75f-263">5 </span><span class="sxs-lookup"><span data-stu-id="ef75f-263">5</span></span>|<span data-ttu-id="ef75f-264">**Atribución del moderador:** muestra el nombre del participante que compartió la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ef75f-264">**Presenter attribution**: Displays the name of the participant who shared the app.</span></span>|

### <a name="responsive-behavior-shared-meeting-stage"></a><span data-ttu-id="ef75f-265">Comportamiento dinámico: fase de reunión compartida</span><span class="sxs-lookup"><span data-stu-id="ef75f-265">Responsive behavior: Shared meeting stage</span></span>

<span data-ttu-id="ef75f-266">Las aplicaciones compartidas en la fase de reunión varían en tamaño según el estado de la reunión y el modo en que el usuario cambia el tamaño de la ventana.</span><span class="sxs-lookup"><span data-stu-id="ef75f-266">Apps shared to the meeting stage vary in size based on the state of the meeting and how the user resizes the window.</span></span> <span data-ttu-id="ef75f-267">Mantenga el relleno y el diseño dinámico de la navegación y los controles tal como lo haría en un explorador.</span><span class="sxs-lookup"><span data-stu-id="ef75f-267">Maintain padding and the responsive layout of navigation and controls just as you would in a browser.</span></span>

* <span data-ttu-id="ef75f-268">**Panel lateral:** un usuario puede tener el panel lateral abierto en cualquier momento durante una reunión para chatear, ver la lista o usar una aplicación (es decir, pestaña en la reunión).</span><span class="sxs-lookup"><span data-stu-id="ef75f-268">**Side panel**: A user can have the side panel open at any time during a meeting to chat, view the roster, or use an app (i.e., in-meeting tab).</span></span> <span data-ttu-id="ef75f-269">La fase reorganiza dinámicamente cuando el panel está abierto.</span><span class="sxs-lookup"><span data-stu-id="ef75f-269">The stage dynamically rearranges when the panel is open.</span></span>
* <span data-ttu-id="ef75f-270">**Cuadrícula de vídeo y audio:** la cuadrícula de vídeo y audio siempre está visible para mostrar a los participantes de la reunión.</span><span class="sxs-lookup"><span data-stu-id="ef75f-270">**Video and audio grid**: The video and audio grid is always visible to show meeting participants.</span></span> <span data-ttu-id="ef75f-271">Cuando un usuario destaca o ancla a alguien en la reunión, esto aumenta el alto o el ancho de la cuadrícula de participantes en función de la orientación.</span><span class="sxs-lookup"><span data-stu-id="ef75f-271">When a user spotlights or pins someone in the meeting, this increases the height or width of the participant grid depending on the orientation.</span></span>

#### <a name="meeting-stage-without-side-panel"></a><span data-ttu-id="ef75f-272">Fase de reunión (sin panel lateral)</span><span class="sxs-lookup"><span data-stu-id="ef75f-272">Meeting stage (without side panel)</span></span>

<span data-ttu-id="ef75f-273">Cuando el panel lateral no está abierto, la fase de reunión es de 994 x 678 píxeles de forma predeterminada y puede tener un mínimo de 792 x 382 píxeles.</span><span class="sxs-lookup"><span data-stu-id="ef75f-273">When the side panel isn't open, the meeting stage is 994x678 pixels by default and can be a minimum 792x382 pixels.</span></span>

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-no-side-panel.png" alt-text="Imagen que muestra la capacidad de respuesta de la fase de reunión compartida con el panel lateral cerrado." border="false":::

#### <a name="meeting-stage-with-side-panel"></a><span data-ttu-id="ef75f-275">Fase de reunión (con panel lateral)</span><span class="sxs-lookup"><span data-stu-id="ef75f-275">Meeting stage (with side panel)</span></span>

<span data-ttu-id="ef75f-276">Cuando el panel lateral está abierto, la fase de reunión es de 918 x 540 píxeles de forma predeterminada y puede tener un mínimo de 472 x 382 píxeles.</span><span class="sxs-lookup"><span data-stu-id="ef75f-276">When the side panel is open, the meeting stage is 918x540 pixels by default and can be a minimum 472x382 pixels.</span></span>

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-with-side-panel.png" alt-text="Imagen que muestra la capacidad de respuesta de la fase de reunión compartida con el panel lateral abierto." border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="ef75f-278">Después de una reunión</span><span class="sxs-lookup"><span data-stu-id="ef75f-278">After a meeting</span></span>

<span data-ttu-id="ef75f-279">Puedes volver a una reunión después de que finalice y ver el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ef75f-279">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="ef75f-280">En este ejemplo, el organizador de la reunión puede ver los resultados del sondeo en la pestaña **Contoso.** (Nota: Desde el punto de vista del diseño, no hay diferencia entre una experiencia de pestaña anterior y posterior a la reunión).</span><span class="sxs-lookup"><span data-stu-id="ef75f-280">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="La ilustración de ejemplo muestra una pestaña posterior a la reunión." border="false":::

## <a name="best-practices"></a><span data-ttu-id="ef75f-282">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="ef75f-282">Best practices</span></span>

<span data-ttu-id="ef75f-283">Use estas recomendaciones para crear una experiencia de aplicación de calidad.</span><span class="sxs-lookup"><span data-stu-id="ef75f-283">Use these recommendations to create a quality app experience.</span></span>

### <a name="interactions"></a><span data-ttu-id="ef75f-284">Interacciones</span><span class="sxs-lookup"><span data-stu-id="ef75f-284">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Ejemplo que muestra cómo limitar el número de interacciones." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="ef75f-286">Hacer: limitar el número de interacciones</span><span class="sxs-lookup"><span data-stu-id="ef75f-286">Do: Limit the number of interactions</span></span>

<span data-ttu-id="ef75f-287">Para los cuadros de diálogo en la reunión, quite el contenido innecesario que no ayuda a los usuarios a lograr algo rápidamente.</span><span class="sxs-lookup"><span data-stu-id="ef75f-287">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Ejemplo que muestra cómo no introducir elementos innecesarios." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="ef75f-289">No: introducir elementos innecesarios</span><span class="sxs-lookup"><span data-stu-id="ef75f-289">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="ef75f-290">Un único cuadro de diálogo en la reunión con varias interacciones puede distraerse de la llamada.</span><span class="sxs-lookup"><span data-stu-id="ef75f-290">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-do.png" alt-text="Ejemplo que muestra cómo crear un entorno centrado." border="false":::

#### <a name="do-create-a-focused-environment"></a><span data-ttu-id="ef75f-292">Hacer: Crear un entorno centrado</span><span class="sxs-lookup"><span data-stu-id="ef75f-292">Do: Create a focused environment</span></span>

<span data-ttu-id="ef75f-293">Se recomienda mantener la experiencia de la aplicación en el ámbito de solo la fase de reunión.</span><span class="sxs-lookup"><span data-stu-id="ef75f-293">We recommend keeping your app’s experience scoped to just the meeting stage.</span></span> <span data-ttu-id="ef75f-294">Puede usar una pestaña en la reunión en el panel lateral como una vista secundaria privada para determinados escenarios.</span><span class="sxs-lookup"><span data-stu-id="ef75f-294">You can use an in-meeting tab in the side panel as a secondary, private view for certain scenarios.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-dont.png" alt-text="Ejemplo que muestra cómo no incluir superficies de competencia durante las reuniones." border="false":::

#### <a name="dont-include-competing-surfaces"></a><span data-ttu-id="ef75f-296">No: incluir superficies de competencia</span><span class="sxs-lookup"><span data-stu-id="ef75f-296">Don't: Include competing surfaces</span></span>

<span data-ttu-id="ef75f-297">La aplicación solo debe pedir a los usuarios que se centren en una sola superficie cada vez, ya sea que colabore en el escenario o responda a un cuadro de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="ef75f-297">Your app should only ask users to focus on a single surface a time, whether it's collaborating on the stage or responding to an in-meeting dialog.</span></span> <span data-ttu-id="ef75f-298">(Nota: No puedes mantener los cuadros de diálogo activados por otras aplicaciones mientras la aplicación está en el escenario).</span><span class="sxs-lookup"><span data-stu-id="ef75f-298">(Note: You can’t keep dialogs being triggered by other apps while your app is on the stage.)</span></span> 

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="ef75f-299">Diseño</span><span class="sxs-lookup"><span data-stu-id="ef75f-299">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Ejemplo que muestra cómo debe usar un diseño de cuadro de diálogo de una columna." border="false":::

#### <a name="do-use-a-one-column-dialog"></a><span data-ttu-id="ef75f-301">Hacer: usar un cuadro de diálogo de una columna</span><span class="sxs-lookup"><span data-stu-id="ef75f-301">Do: Use a one-column dialog</span></span>

<span data-ttu-id="ef75f-302">Dado que los cuadros de diálogo están en el centro de la fase de reunión, la finalización de tareas debe ser rápida y sencilla para evitar la frustración del usuario.</span><span class="sxs-lookup"><span data-stu-id="ef75f-302">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Ejemplo que muestra que no debe saturar el espacio de una extensión de reunión." border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="ef75f-304">No: saturar el espacio</span><span class="sxs-lookup"><span data-stu-id="ef75f-304">Don't: Clutter the space</span></span>

<span data-ttu-id="ef75f-305">El contenido densa o demasiado estructurado puede ser molesto y abrumador, especialmente durante una reunión.</span><span class="sxs-lookup"><span data-stu-id="ef75f-305">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Ejemplo que muestra un diseño de pestaña de una columna." border="false":::

#### <a name="do-use-a-one-column-tab"></a><span data-ttu-id="ef75f-307">Hacer: usar una pestaña de una columna</span><span class="sxs-lookup"><span data-stu-id="ef75f-307">Do: Use a one-column tab</span></span>

<span data-ttu-id="ef75f-308">Dada la naturaleza estrecha de la pestaña en la reunión, se recomienda encarecidamente mostrar el contenido en una sola columna.</span><span class="sxs-lookup"><span data-stu-id="ef75f-308">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Ejemplo que muestra una pestaña con varias columnas." border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="ef75f-310">No: usar varias columnas</span><span class="sxs-lookup"><span data-stu-id="ef75f-310">Don't: Use multiple columns</span></span>

<span data-ttu-id="ef75f-311">Debido al espacio limitado de la pestaña en la reunión, no se recomiendan diseños con más de una columna.</span><span class="sxs-lookup"><span data-stu-id="ef75f-311">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="ef75f-312">Controles</span><span class="sxs-lookup"><span data-stu-id="ef75f-312">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Ejemplo que muestra cómo alinear correctamente los controles principales." border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="ef75f-314">Hacer: alinear a la derecha la acción principal</span><span class="sxs-lookup"><span data-stu-id="ef75f-314">Do: Right align the primary action</span></span>

<span data-ttu-id="ef75f-315">Se recomienda colocar la acción más intensa visualmente en la ubicación más derecha.</span><span class="sxs-lookup"><span data-stu-id="ef75f-315">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Ejemplo que muestra cómo no debe dejar alineados los controles principales." border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="ef75f-317">No: acciones de alineación izquierda o central</span><span class="sxs-lookup"><span data-stu-id="ef75f-317">Don't: Left or center align actions</span></span>

<span data-ttu-id="ef75f-318">Esto se desvía del patrón de Teams estándar para la colocación de controles en un cuadro de diálogo y puede conflicto con un cuadro de diálogo detrás del superior.</span><span class="sxs-lookup"><span data-stu-id="ef75f-318">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scrolling"></a><span data-ttu-id="ef75f-319">Desplazamiento</span><span class="sxs-lookup"><span data-stu-id="ef75f-319">Scrolling</span></span>

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Ejemplo que muestra el desplazamiento vertical en una pestaña en reunión." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-do.png" alt-text="Ejemplo que muestra el desplazamiento vertical en la fase de reunión compartida." border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="ef75f-322">Hacer: desplazarse verticalmente</span><span class="sxs-lookup"><span data-stu-id="ef75f-322">Do: Scroll vertically</span></span>

<span data-ttu-id="ef75f-323">Los usuarios esperan desplazamiento vertical en Teams (y en otros lugares).</span><span class="sxs-lookup"><span data-stu-id="ef75f-323">Users expect vertical scrolling in Teams (and elsewhere).</span></span> <span data-ttu-id="ef75f-324">Esto puede no aplicarse si tiene un lienzo creativo, como una pizarra, que los usuarios pueden desplazar por los ejes x e y.</span><span class="sxs-lookup"><span data-stu-id="ef75f-324">This may not apply if you have a creative canvas, such as a whiteboard, which users can pan across the x and y axis.</span></span>

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Ejemplo que muestra el desplazamiento horizontal en una pestaña en la reunión." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-dont.png" alt-text="Ejemplo que muestra el desplazamiento horizontal en la fase de reunión compartida." border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="ef75f-327">No: desplazarse horizontalmente</span><span class="sxs-lookup"><span data-stu-id="ef75f-327">Don't: Scroll horizontally</span></span>

<span data-ttu-id="ef75f-328">El desplazamiento horizontal no es un comportamiento esperado en Teams (incluido el entorno de reunión).</span><span class="sxs-lookup"><span data-stu-id="ef75f-328">Horizontal scrolling isn’t an expected behavior in Teams (including the meeting environment).</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="ef75f-329">Flujos de trabajo</span><span class="sxs-lookup"><span data-stu-id="ef75f-329">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Ejemplo que muestra un escenario complejo en una pestaña de reunión." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="ef75f-331">Hacer: escenarios complejos de Surface en la pestaña en reunión</span><span class="sxs-lookup"><span data-stu-id="ef75f-331">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="ef75f-332">Si la aplicación incluye varias tareas, recomendamos encarecidamente usar una pestaña en la reunión con un diseño de una sola columna.</span><span class="sxs-lookup"><span data-stu-id="ef75f-332">If your app includes multiple tasks, we strongly recommend using an in-meeting tab with a single-column layout.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Ejemplo que muestra escenarios complejos en un cuadro de diálogo en la reunión." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a><span data-ttu-id="ef75f-334">Don't: Hacer complejos los cuadros de diálogo en la reunión</span><span class="sxs-lookup"><span data-stu-id="ef75f-334">Don't: Make in-meeting dialogs complex</span></span>

<span data-ttu-id="ef75f-335">Los cuadros de diálogo en reunión están diseñados para interacciones breves.</span><span class="sxs-lookup"><span data-stu-id="ef75f-335">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="ef75f-336">Creación de temas</span><span class="sxs-lookup"><span data-stu-id="ef75f-336">Theming</span></span>

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Ejemplo que muestra una extensión de reunión con el tema oscuro." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-do.png" alt-text="Otro ejemplo que muestra la extensión de reunión con el tema oscuro." border="false":::

#### <a name="do-focus-on-dark-theme"></a><span data-ttu-id="ef75f-339">Do: Focus on dark theme</span><span class="sxs-lookup"><span data-stu-id="ef75f-339">Do: Focus on dark theme</span></span>

<span data-ttu-id="ef75f-340">Teams reuniones están optimizadas para temas oscuros para ayudar a reducir el ruido visual y cognitivo para que los usuarios puedan centrarse en la discusión y el contenido compartido.</span><span class="sxs-lookup"><span data-stu-id="ef75f-340">Teams meetings are optimized for dark theme to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="ef75f-341">Ten en cuenta que ciertos tipos de aplicaciones (como pizarras y edición de documentos) no necesitan un lienzo oscuro.</span><span class="sxs-lookup"><span data-stu-id="ef75f-341">Keep in mind certain types of apps (such as whiteboarding and document editing) don't need a dark canvas.</span></span>

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Ejemplo que muestra una extensión de reunión con colores que no coinciden con el tema de la reunión." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-dont.png" alt-text="Otro ejemplo que muestra una extensión de reunión con colores que no coinciden con el tema de la reunión." border="false":::

#### <a name="dont-use-unfamiliar-colors"></a><span data-ttu-id="ef75f-344">No usar: usar colores desconocidos</span><span class="sxs-lookup"><span data-stu-id="ef75f-344">Don't: Use unfamiliar colors</span></span>

<span data-ttu-id="ef75f-345">Los colores que entren en conflicto con el entorno de reunión pueden ser molestos y parecer menos nativos de Teams.</span><span class="sxs-lookup"><span data-stu-id="ef75f-345">Colors that clash with the meeting environment may be distracting and appear less native to Teams.</span></span> <span data-ttu-id="ef75f-346">Obtenga información sobre la Teams [de color,](https://developer.microsoft.com/fluentui#/styles/web/colors/products)incluidos los neutros del tema de llamada.</span><span class="sxs-lookup"><span data-stu-id="ef75f-346">Learn about the Teams [color ramp](https://developer.microsoft.com/fluentui#/styles/web/colors/products), including call theme neutrals.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="ef75f-347">Navegación</span><span class="sxs-lookup"><span data-stu-id="ef75f-347">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Ejemplo que muestra una extensión de reunión con un botón Atrás." border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="ef75f-349">Hacer: Tener un botón atrás</span><span class="sxs-lookup"><span data-stu-id="ef75f-349">Do: Have a back button</span></span>

<span data-ttu-id="ef75f-350">Si tiene más de una capa de navegación en una pestaña de reunión, los usuarios deben poder volver a sus vistas anteriores.</span><span class="sxs-lookup"><span data-stu-id="ef75f-350">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Ejemplo que muestra una extensión de reunión con dos botones de descarte." border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="ef75f-352">No: incluir otro botón descartar</span><span class="sxs-lookup"><span data-stu-id="ef75f-352">Don't: Include another dismiss button</span></span>

<span data-ttu-id="ef75f-353">Proporcionar una opción para cerrar el contenido de la pestaña en la reunión puede causar problemas, ya que ya hay un botón en el encabezado para descartar la propia pestaña en la reunión.</span><span class="sxs-lookup"><span data-stu-id="ef75f-353">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Ejemplo que muestra modales (o módulos de tareas) dentro de una pestaña en la reunión." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="ef75f-355">Precaución: evite los modales dentro de la pestaña en la reunión</span><span class="sxs-lookup"><span data-stu-id="ef75f-355">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="ef75f-356">Los modales (también conocidos como módulos de tareas) en la pestaña ya estrecha en la reunión podrían ajustar y oscurecer el contenido.</span><span class="sxs-lookup"><span data-stu-id="ef75f-356">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

### <a name="responsive-behavior"></a><span data-ttu-id="ef75f-357">Comportamiento dinámico</span><span class="sxs-lookup"><span data-stu-id="ef75f-357">Responsive behavior</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-do.png" alt-text="Ejemplo que muestra cómo cambiar el tamaño de una extensión de reunión correctamente." border="false":::

#### <a name="do-resize-and-scale-your-app-responsively"></a><span data-ttu-id="ef75f-359">Do: Resize and scale your app responsively</span><span class="sxs-lookup"><span data-stu-id="ef75f-359">Do: Resize and scale your app responsively</span></span>

<span data-ttu-id="ef75f-360">El contenido de la aplicación debe cambiar el tamaño y condensarse dinámicamente en ventanas más pequeñas.</span><span class="sxs-lookup"><span data-stu-id="ef75f-360">App content should dynamically resize and condense in smaller windows.</span></span> <span data-ttu-id="ef75f-361">Mantén visible la navegación principal de la aplicación y los controles flotantes.</span><span class="sxs-lookup"><span data-stu-id="ef75f-361">Keep your app’s main navigation and any floating controls visible.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-dont.png" alt-text="Ejemplo que muestra cómo no cambiar el tamaño de una extensión de reunión correctamente." border="false":::

#### <a name="dont-crop-or-clip-primary-ui-components"></a><span data-ttu-id="ef75f-363">No: recortar o recortar componentes de interfaz de usuario principales</span><span class="sxs-lookup"><span data-stu-id="ef75f-363">Don't: Crop or clip primary UI components</span></span>

<span data-ttu-id="ef75f-364">La navegación flotante y los controles fuera de la pantalla y que requieren un desplazamiento para buscar pueden resultar confusos para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="ef75f-364">Floating navigation and controls off screen and requiring a scroll to find can be confusing for users.</span></span> <span data-ttu-id="ef75f-365">El contenido de la aplicación no debe desplazarse horizontalmente cuando no cabe en el iframe.</span><span class="sxs-lookup"><span data-stu-id="ef75f-365">Your app content shouldn’t scroll horizontally when it can't fit in the iframe.</span></span>

   :::column-end:::
:::row-end:::

## <a name="next-step"></a><span data-ttu-id="ef75f-366">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="ef75f-366">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ef75f-367">Configurar la aplicación para reuniones</span><span class="sxs-lookup"><span data-stu-id="ef75f-367">Configure your app for meetings</span></span>](~/apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md)

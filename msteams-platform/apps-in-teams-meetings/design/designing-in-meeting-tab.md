---
title: Diseñar una pestaña dentro de la reunión
author: heath-hamilton
description: Obtenga información sobre cómo diseñar eficazmente una pestaña en la reunión para Microsoft Teams.
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: fc10c5b60672d243ac2e330ce93b4e01c2e7a278
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346675"
---
# <a name="design-an-in-meeting-tab"></a><span data-ttu-id="16b71-103">Diseñar una pestaña dentro de la reunión</span><span class="sxs-lookup"><span data-stu-id="16b71-103">Design an in-meeting tab</span></span>

<span data-ttu-id="16b71-104">La pestaña en reunión es un lienzo para aumentar la colaboración durante las reuniones.</span><span class="sxs-lookup"><span data-stu-id="16b71-104">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="16b71-105">Según la funcionalidad de la pestaña Microsoft Teams, los asistentes pueden ver e interactuar con el contenido de la aplicación en un espacio dedicado fuera de la fase de reunión a través de vistas compartidas o basadas en roles.</span><span class="sxs-lookup"><span data-stu-id="16b71-105">Based on the Teams tab capability, attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

## <a name="use-cases"></a><span data-ttu-id="16b71-106">Casos de uso</span><span class="sxs-lookup"><span data-stu-id="16b71-106">Use cases</span></span>

<span data-ttu-id="16b71-107">Los usuarios pueden usar la ficha en la reunión para:</span><span class="sxs-lookup"><span data-stu-id="16b71-107">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="16b71-108">Proporcionar comentarios detallados (por ejemplo, evaluar un candidato de trabajo)</span><span class="sxs-lookup"><span data-stu-id="16b71-108">Provide detailed feedback (for example, evaluate a job candidate)</span></span>
* <span data-ttu-id="16b71-109">Crear rápidamente un sondeo, una encuesta o un elemento de tarea para los participantes de la reunión</span><span class="sxs-lookup"><span data-stu-id="16b71-109">Quickly create a poll, survey, or task item for the meeting participants</span></span>
* <span data-ttu-id="16b71-110">Mostrar notas relevantes para la reunión (por ejemplo, información sobre un responsable de ventas)</span><span class="sxs-lookup"><span data-stu-id="16b71-110">Display notes relevant to the meeting (for example, information about a sales lead)</span></span>

## <a name="example"></a><span data-ttu-id="16b71-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="16b71-111">Example</span></span>

<span data-ttu-id="16b71-112">El siguiente ejemplo muestra la pestaña en la reunión que muestra el contenido de la aplicación de la encuesta.</span><span class="sxs-lookup"><span data-stu-id="16b71-112">The following example shows the in-meeting tab displaying survey app content.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-organizer-view.png" alt-text="Ejemplo muestra el aspecto que puede tener la ficha reunión en la reunión desde el punto de vista del organizador de la reunión.":::

<span data-ttu-id="16b71-114"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Vea el escenario completo (Figma)</a></span><span class="sxs-lookup"><span data-stu-id="16b71-114"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See the full scenario (Figma)</a></span></span>

<span data-ttu-id="16b71-115"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Consulte otros ejemplos de casos de uso (Figma)</a></span><span class="sxs-lookup"><span data-stu-id="16b71-115"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See other example use cases (Figma)</a></span></span>

## <a name="anatomy"></a><span data-ttu-id="16b71-116">Anatomía</span><span class="sxs-lookup"><span data-stu-id="16b71-116">Anatomy</span></span>

<span data-ttu-id="16b71-117">La pestaña en la reunión muestra el contenido de la aplicación con las siguientes dimensiones:</span><span class="sxs-lookup"><span data-stu-id="16b71-117">The in-meeting tab displays your app content using the following dimensions:</span></span>

* <span data-ttu-id="16b71-118">**Width**: 280 píxeles para el área WebView.</span><span class="sxs-lookup"><span data-stu-id="16b71-118">**Width**: 280 pixels for the webview area.</span></span> <span data-ttu-id="16b71-119">Hay 20 píxeles de relleno en los lados izquierdo y derecho de la WebView.</span><span class="sxs-lookup"><span data-stu-id="16b71-119">There are 20 pixels of padding on the left and right sides of the webview.</span></span>
* <span data-ttu-id="16b71-120">**Altura**: sangrado completo hacia la parte inferior de la pestaña. Hay 20 píxeles de relleno entre el área WebView y el encabezado de pestaña.</span><span class="sxs-lookup"><span data-stu-id="16b71-120">**Height**: Full bleed to the bottom of the tab. There are 20 pixels of padding between the webview area and tab header.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una pestaña en la reunión de la extensión de reunión." border="false":::

1. <span data-ttu-id="16b71-122">**Icono** de la aplicación: el punto de entrada a la pestaña en reunión.</span><span class="sxs-lookup"><span data-stu-id="16b71-122">**App icon**: The entry point to the in-meeting tab.</span></span>
1. <span data-ttu-id="16b71-123">**Header**: incluye el nombre de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="16b71-123">**Header**: Includes the tab name.</span></span>
1. <span data-ttu-id="16b71-124">**Name**: el nombre de la instancia de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="16b71-124">**Name**: The name of the tab instance.</span></span>
1. <span data-ttu-id="16b71-125">**Dismiss**: descarta la pestaña. Use siempre el icono de cierre superior derecho en lugar de una acción en el pie de página.</span><span class="sxs-lookup"><span data-stu-id="16b71-125">**Dismiss**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>
1. <span data-ttu-id="16b71-126">**Vista WebView**: muestra todo el contenido de aplicaciones de terceros.</span><span class="sxs-lookup"><span data-stu-id="16b71-126">**Webview**: Displays all third-party app content.</span></span>

## <a name="behavior"></a><span data-ttu-id="16b71-127">Comportamiento</span><span class="sxs-lookup"><span data-stu-id="16b71-127">Behavior</span></span>

### <a name="scale"></a><span data-ttu-id="16b71-128">Scale</span><span class="sxs-lookup"><span data-stu-id="16b71-128">Scale</span></span>

<span data-ttu-id="16b71-129">Actualmente, el ancho de la pestaña en reunión es fijo.</span><span class="sxs-lookup"><span data-stu-id="16b71-129">Currently, the width of the in-meeting tab is fixed.</span></span>

### <a name="scrolling"></a><span data-ttu-id="16b71-130">Desplazamiento</span><span class="sxs-lookup"><span data-stu-id="16b71-130">Scrolling</span></span>

<span data-ttu-id="16b71-131">Esto es lo que debe saber sobre el desplazamiento en la pestaña en la reunión:</span><span class="sxs-lookup"><span data-stu-id="16b71-131">Here's what to know about scrolling in the in-meeting tab:</span></span>

* <span data-ttu-id="16b71-132">Solo debe poder desplazarse verticalmente.</span><span class="sxs-lookup"><span data-stu-id="16b71-132">You should only be able to scroll vertically.</span></span>
* <span data-ttu-id="16b71-133">Solo puede ver el contenido al que se ha desplazado (nada anterior o posterior).</span><span class="sxs-lookup"><span data-stu-id="16b71-133">You can only see the content you've scrolled to (nothing above or below).</span></span>
* <span data-ttu-id="16b71-134">La barra de desplazamiento es parte del contenido de WebView.</span><span class="sxs-lookup"><span data-stu-id="16b71-134">The scrollbar is part of the webview content.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-scroll.png" alt-text="Ilustración que muestra cómo funciona el desplazamiento del contenido de WebView en la pestaña en reunión." border="false":::

### <a name="navigation"></a><span data-ttu-id="16b71-136">Navegación</span><span class="sxs-lookup"><span data-stu-id="16b71-136">Navigation</span></span>

<span data-ttu-id="16b71-137">Para los escenarios con capas de navegación o contenido pesado, se recomienda permitir que los usuarios naveguen a una capa secundaria.</span><span class="sxs-lookup"><span data-stu-id="16b71-137">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="16b71-138">Los usuarios deben poder volver a la capa anterior.</span><span class="sxs-lookup"><span data-stu-id="16b71-138">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav.png" alt-text="Ilustración que muestra cómo funciona la navegación a una capa secundaria de la pestaña en reunión." border="false":::

## <a name="components"></a><span data-ttu-id="16b71-140">Componentes</span><span class="sxs-lookup"><span data-stu-id="16b71-140">Components</span></span>

<span data-ttu-id="16b71-141">Las pestañas en la reunión se crean principalmente con los siguientes componentes de la <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">interfaz de usuario (Figma)</a>, que se basan en el <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">sistema de diseño de Fluent</a>.</span><span class="sxs-lookup"><span data-stu-id="16b71-141">In-meeting tabs are built primarily with the following <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">UI components (Figma)</a>, which are based on the <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent Design System</a>.</span></span>

<span data-ttu-id="16b71-142">Componente</span><span class="sxs-lookup"><span data-stu-id="16b71-142">Component</span></span> | <span data-ttu-id="16b71-143">Instrucciones</span><span class="sxs-lookup"><span data-stu-id="16b71-143">Guidelines</span></span> | <span data-ttu-id="16b71-144">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="16b71-144">Example</span></span>
 - | - | -
<span data-ttu-id="16b71-145">Botón</span><span class="sxs-lookup"><span data-stu-id="16b71-145">Button</span></span> | <span data-ttu-id="16b71-146">Los botones principal y secundario pueden ser medios o pequeños.</span><span class="sxs-lookup"><span data-stu-id="16b71-146">Primary and secondary buttons can be medium or small</span></span> | <span data-ttu-id="16b71-147">Enviar una respuesta</span><span class="sxs-lookup"><span data-stu-id="16b71-147">Send a response</span></span>
<span data-ttu-id="16b71-148">Input</span><span class="sxs-lookup"><span data-stu-id="16b71-148">Input</span></span> | <span data-ttu-id="16b71-149">Campo para la entrada de breves usuarios.</span><span class="sxs-lookup"><span data-stu-id="16b71-149">Field for brief user input.</span></span> <span data-ttu-id="16b71-150">El texto de la etiqueta puede incluir un icono</span><span class="sxs-lookup"><span data-stu-id="16b71-150">Label text can include an icon</span></span>  | <span data-ttu-id="16b71-151">Escribir comentarios</span><span class="sxs-lookup"><span data-stu-id="16b71-151">Enter feedback</span></span>
<span data-ttu-id="16b71-152">Desplegable</span><span class="sxs-lookup"><span data-stu-id="16b71-152">Dropdown</span></span> | <span data-ttu-id="16b71-153">Seleccione una o más opciones de una lista.</span><span class="sxs-lookup"><span data-stu-id="16b71-153">Select one or more options from a list.</span></span> <span data-ttu-id="16b71-154">Puede incluir características de búsqueda y de selección múltiple</span><span class="sxs-lookup"><span data-stu-id="16b71-154">Can include search and multi-selection features</span></span> | <span data-ttu-id="16b71-155">Elegir un idioma</span><span class="sxs-lookup"><span data-stu-id="16b71-155">Choose a language</span></span>
<span data-ttu-id="16b71-156">Controles de selección</span><span class="sxs-lookup"><span data-stu-id="16b71-156">Selection controls</span></span> | <span data-ttu-id="16b71-157">Use casillas de verificación para varias opciones o botones de radio y conmute a opciones únicas.</span><span class="sxs-lookup"><span data-stu-id="16b71-157">Use checkboxes for multiple choices or radio buttons and toggles for single choices.</span></span> <span data-ttu-id="16b71-158">Para selecciones más detalladas, use un control deslizante.</span><span class="sxs-lookup"><span data-stu-id="16b71-158">For more detailed selections, use a slider</span></span> | <span data-ttu-id="16b71-159">Votar en un sondeo</span><span class="sxs-lookup"><span data-stu-id="16b71-159">Vote in a poll</span></span>
<span data-ttu-id="16b71-160">Alertas</span><span class="sxs-lookup"><span data-stu-id="16b71-160">Alerts</span></span> | <span data-ttu-id="16b71-161">Tanto si muestra un mensaje urgente, un estado de error o una advertencia, el mensaje debe ser corto y no interrumpir la tarea actual del usuario</span><span class="sxs-lookup"><span data-stu-id="16b71-161">Whether displaying an urgent message, error state, or warning, the message should be short and won't interrupt the user's current task</span></span> | <span data-ttu-id="16b71-162">Mostrar problema al enviar una respuesta</span><span class="sxs-lookup"><span data-stu-id="16b71-162">Display issue when submitting a response</span></span>

## <a name="theming"></a><span data-ttu-id="16b71-163">Creación de temas</span><span class="sxs-lookup"><span data-stu-id="16b71-163">Theming</span></span>

### <a name="colors"></a><span data-ttu-id="16b71-164">Colores</span><span class="sxs-lookup"><span data-stu-id="16b71-164">Colors</span></span>

<span data-ttu-id="16b71-165">Use la <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">combinación de colores recomendada (Figma)</a> para los fondos, los en primer plano y los Estados que transmiten.</span><span class="sxs-lookup"><span data-stu-id="16b71-165">Use the <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">recommended color scheme (Figma)</a> for backgrounds, foregrounds, and conveying states.</span></span>

### <a name="typography"></a><span data-ttu-id="16b71-166">Tipografía</span><span class="sxs-lookup"><span data-stu-id="16b71-166">Typography</span></span>

<span data-ttu-id="16b71-167">Use los <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">tamaños y pesos de fuente recomendados (Figma)</a> para títulos, texto principal y texto de metadatos.</span><span class="sxs-lookup"><span data-stu-id="16b71-167">Use the <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">recommended font sizes and weights (Figma)</a> for titles, body text, and metadata text.</span></span>

## <a name="best-practices"></a><span data-ttu-id="16b71-168">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="16b71-168">Best practices</span></span>

### <a name="responsiveness"></a><span data-ttu-id="16b71-169">Capacidad</span><span class="sxs-lookup"><span data-stu-id="16b71-169">Responsiveness</span></span>

<span data-ttu-id="16b71-170">Los diseños de pestañas en la reunión deben poder escalarse a varios tamaños.</span><span class="sxs-lookup"><span data-stu-id="16b71-170">In-meeting tab layouts should be able to scale to various sizes.</span></span> <span data-ttu-id="16b71-171">Tenga en cuenta el modo en que la pestaña se escalará y tomará la forma antes, durante y después de la reunión.</span><span class="sxs-lookup"><span data-stu-id="16b71-171">Consider how the tab will scale and take shape before, during, and after the meeting.</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-before-meeting.png" alt-text="Ilustración que muestra que el contenido de la pestaña en la reunión es similar a una pestaña de pantalla completa antes y después de una reunión." border="false":::

#### <a name="before-the-meeting"></a><span data-ttu-id="16b71-173">Antes de la reunión</span><span class="sxs-lookup"><span data-stu-id="16b71-173">Before the meeting</span></span>

<span data-ttu-id="16b71-174">Asegúrese de que el diseño de la pestaña se puede adaptar a un diseño derecho o izquierdo para diferentes idiomas y que los controles se mueven a las ubicaciones correctas.</span><span class="sxs-lookup"><span data-stu-id="16b71-174">Make sure your tab layout can adapt to a right or left layout for different languages and that controls move to the correct locations.</span></span> <span data-ttu-id="16b71-175">(Los diseños previos a la reunión también pueden aplicarse a los diseños posteriores a la reunión).</span><span class="sxs-lookup"><span data-stu-id="16b71-175">(Pre-meeting layouts can also apply to post-meeting layouts.)</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-during-meeting.png" alt-text="Ilustración que muestra cómo el contenido de la ficha anterior a la reunión se comprime en la pestaña en reunión durante una reunión." border="false":::

#### <a name="during-the-meeting"></a><span data-ttu-id="16b71-177">Durante la reunión</span><span class="sxs-lookup"><span data-stu-id="16b71-177">During the meeting</span></span>

<span data-ttu-id="16b71-178">El contenido de la pestaña se ajusta en el diseño y la ubicación de la pestaña en la reunión.</span><span class="sxs-lookup"><span data-stu-id="16b71-178">Tab content adjusts to the in-meeting tab layout and location.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="16b71-179">Creación de temas</span><span class="sxs-lookup"><span data-stu-id="16b71-179">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-theming-do.png" alt-text="Ilustración que muestra cómo diseñar la pestaña en reunión para el tema oscuro usado en reuniones de Microsoft Teams." border="false":::

#### <a name="do-design-for-a-dark-theme"></a><span data-ttu-id="16b71-181">Do: diseñar un tema oscuro</span><span class="sxs-lookup"><span data-stu-id="16b71-181">Do: Design for a dark theme</span></span>

<span data-ttu-id="16b71-182">Las reuniones de Microsoft Teams están optimizadas para el modo oscuro para ayudar a reducir el ruido visual y cognitivo para que los usuarios puedan centrarse en la discusión y en el contenido compartido.</span><span class="sxs-lookup"><span data-stu-id="16b71-182">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="16b71-183">La ficha en la reunión debe aplicar un tema oscuro y debe seguir las instrucciones de temas.</span><span class="sxs-lookup"><span data-stu-id="16b71-183">The in-meeting tab should apply a dark theme and should follow theming guidelines.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-theming-dont.png" alt-text="Ilustración que muestra que no se deben usar colores que no resultan favorables para el tema de Teams oscuro." border="false":::

#### <a name="dont-use-unfamiliar-colors"></a><span data-ttu-id="16b71-185">No: usar colores no habituales</span><span class="sxs-lookup"><span data-stu-id="16b71-185">Don't: Use unfamiliar colors</span></span>

<span data-ttu-id="16b71-186">Los colores que entran en conflicto con el entorno de la reunión pueden distraerse y mostrarse menos nativos de Teams.</span><span class="sxs-lookup"><span data-stu-id="16b71-186">Colors that clash with the meeting environment may be distracting and appear less native to Teams.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scrolling"></a><span data-ttu-id="16b71-187">Desplazamiento</span><span class="sxs-lookup"><span data-stu-id="16b71-187">Scrolling</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-scroll-do.png" alt-text="Ilustración que muestra solo se debe permitir el desplazamiento vertical en la pestaña en reunión." border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="16b71-189">Hacer: desplazarse verticalmente</span><span class="sxs-lookup"><span data-stu-id="16b71-189">Do: Scroll vertically</span></span>

<span data-ttu-id="16b71-190">Los usuarios anticipan los desplazamientos verticales en Teams (y en cualquier otro lugar).</span><span class="sxs-lookup"><span data-stu-id="16b71-190">Users anticipate vertical scrolling in Teams (and elsewhere).</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-scroll-dont.png" alt-text="Ilustración en la que se muestra que se muestra que no se permite el desplazamiento horizontal en la pestaña en reunión." border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="16b71-192">No: desplazar horizontalmente</span><span class="sxs-lookup"><span data-stu-id="16b71-192">Don't: Scroll horizontally</span></span>

<span data-ttu-id="16b71-193">El desplazamiento horizontal no es un comportamiento esperado en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="16b71-193">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="16b71-194">Otros lienzos del entorno de la reunión se desplazan verticalmente.</span><span class="sxs-lookup"><span data-stu-id="16b71-194">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="16b71-195">Diseño</span><span class="sxs-lookup"><span data-stu-id="16b71-195">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-layout-do.png" alt-text="Ilustración que muestra el diseño de columna única recomendada en la pestaña en reunión." border="false":::

#### <a name="do-single-columns"></a><span data-ttu-id="16b71-197">Do: columnas únicas</span><span class="sxs-lookup"><span data-stu-id="16b71-197">Do: Single columns</span></span>

<span data-ttu-id="16b71-198">Dada la naturaleza estrecha de las pestañas de la reunión, se recomienda encarecidamente mostrar el contenido en una sola columna.</span><span class="sxs-lookup"><span data-stu-id="16b71-198">Given the in-meeting tab’s narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-layout-dont.png" alt-text="Ilustración que muestra cómo no es ideal un diseño de dos columnas en la pestaña de la reunión." border="false":::

#### <a name="dont-multiple-columns"></a><span data-ttu-id="16b71-200">No: varias columnas</span><span class="sxs-lookup"><span data-stu-id="16b71-200">Don't: Multiple columns</span></span>

<span data-ttu-id="16b71-201">Debido al espacio limitado de la pestaña en reunión, no se recomiendan los diseños con más de una columna.</span><span class="sxs-lookup"><span data-stu-id="16b71-201">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="16b71-202">Navegación</span><span class="sxs-lookup"><span data-stu-id="16b71-202">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav-do.png" alt-text="Ilustración que muestra que siempre debe proporcionar un botón atrás si la aplicación de pestañas en la reunión tiene más de un nivel de navegación." border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="16b71-204">Do: tener un botón atrás</span><span class="sxs-lookup"><span data-stu-id="16b71-204">Do: Have a back button</span></span>

<span data-ttu-id="16b71-205">Si tiene más de una capa de navegación, los usuarios deben poder volver a su vista anterior.</span><span class="sxs-lookup"><span data-stu-id="16b71-205">If you have more than one layer of navigation, users must be able to go back to their previous view.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav-dont.png" alt-text="Ilustración que muestra que agregar otro botón cerrar en la pestaña de la reunión para la navegación es redundante y podría causar problemas." border="false":::

#### <a name="dont-include-another-close-button"></a><span data-ttu-id="16b71-207">No: incluir otro botón cerrar</span><span class="sxs-lookup"><span data-stu-id="16b71-207">Don't: Include another close button</span></span>

<span data-ttu-id="16b71-208">Ofrecer una opción para cerrar el contenido de la pestaña en la reunión puede causar problemas porque ya hay un botón cerrar en el encabezado para descartar la misma pestaña en la reunión.</span><span class="sxs-lookup"><span data-stu-id="16b71-208">Providing an option to close in-meeting tab content may cause issues since there’s already a close button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav-caution.png" alt-text="Ilustración que muestra que debe tener cuidado al usar modales (es decir, módulos de tareas) en la ficha en la reunión que se proporciona el espacio limitado." border="false":::

#### <a name="caution-using-dialogs-in-a-narrow-space"></a><span data-ttu-id="16b71-210">PRECAUCIÓN: uso de cuadros de diálogo en un espacio estrecho</span><span class="sxs-lookup"><span data-stu-id="16b71-210">Caution: Using dialogs in a narrow space</span></span>

<span data-ttu-id="16b71-211">Los cuadros de diálogo, como módulos de tareas, en la pestaña en la reunión ya estrecha pueden ajustar y oscurecer el contenido.</span><span class="sxs-lookup"><span data-stu-id="16b71-211">Dialogs, such as task modules, in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

## <a name="accessibility"></a><span data-ttu-id="16b71-212">Accesibilidad</span><span class="sxs-lookup"><span data-stu-id="16b71-212">Accessibility</span></span>

<span data-ttu-id="16b71-213">Para obtener información sobre la accesibilidad, vea <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.</span><span class="sxs-lookup"><span data-stu-id="16b71-213">For information on accessibility, see <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.</span></span>

## <a name="resources"></a><span data-ttu-id="16b71-214">Recursos</span><span class="sxs-lookup"><span data-stu-id="16b71-214">Resources</span></span>

* <span data-ttu-id="16b71-215"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Archivo Figma de extensiones de reunión de Microsoft Teams</a></span><span class="sxs-lookup"><span data-stu-id="16b71-215"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Microsoft Teams meeting extensions Figma file</a></span></span>
* [<span data-ttu-id="16b71-216">Instrucciones de diseño de pestañas</span><span class="sxs-lookup"><span data-stu-id="16b71-216">Tabs design guidelines</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="16b71-217">Directrices de diseño de pestañas para dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="16b71-217">Tabs design guidelines for mobile</span></span>](../../tabs/design/tabs-mobile.md)

## <a name="validate-your-design"></a><span data-ttu-id="16b71-218">Validar el diseño</span><span class="sxs-lookup"><span data-stu-id="16b71-218">Validate your design</span></span>

<span data-ttu-id="16b71-219">Si planea publicar la aplicación en AppSource, debe comprender los problemas de diseño que suelen hacer que las aplicaciones fallen durante el envío.</span><span class="sxs-lookup"><span data-stu-id="16b71-219">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="16b71-220">Comprobar las instrucciones de validación del diseño</span><span class="sxs-lookup"><span data-stu-id="16b71-220">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)

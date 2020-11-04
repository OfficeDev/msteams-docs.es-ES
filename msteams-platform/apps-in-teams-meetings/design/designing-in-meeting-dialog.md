---
title: Diseñar un diálogo dentro de la reunión
author: heath-hamilton
description: Obtenga información sobre cómo diseñar eficazmente un cuadro de diálogo en reunión para Microsoft Teams.
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: ded8793f6ea0a736e559e72afaf314608c0875fe
ms.sourcegitcommit: df9448681d2a81f1029aad5a5e1989cd438d1ae0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2020
ms.locfileid: "48877053"
---
# <a name="design-an-in-meeting-dialog"></a><span data-ttu-id="5e93d-103">Diseñar un diálogo dentro de la reunión</span><span class="sxs-lookup"><span data-stu-id="5e93d-103">Design an in-meeting dialog</span></span>

<span data-ttu-id="5e93d-104">Los cuadros de diálogo en la reunión se muestran en la fase de reunión de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="5e93d-104">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="5e93d-105">Requieren la atención, la confirmación o la interacción del usuario, pero son sutiles y no interrumpen la reunión.</span><span class="sxs-lookup"><span data-stu-id="5e93d-105">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span>

## <a name="use-cases"></a><span data-ttu-id="5e93d-106">Casos de uso</span><span class="sxs-lookup"><span data-stu-id="5e93d-106">Use cases</span></span>

<span data-ttu-id="5e93d-107">Los cuadros de diálogo en la reunión son desencadenados por un usuario (como el organizador de la reunión) que puede desear a los participantes:</span><span class="sxs-lookup"><span data-stu-id="5e93d-107">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="5e93d-108">Proporcionar comentarios breves</span><span class="sxs-lookup"><span data-stu-id="5e93d-108">Provide brief feedback</span></span>
* <span data-ttu-id="5e93d-109">Realizar una breve encuesta o sondeo</span><span class="sxs-lookup"><span data-stu-id="5e93d-109">Take a short survey or poll</span></span>
* <span data-ttu-id="5e93d-110">Enviar aprobaciones</span><span class="sxs-lookup"><span data-stu-id="5e93d-110">Submit approvals</span></span>
* <span data-ttu-id="5e93d-111">Recibir recordatorios</span><span class="sxs-lookup"><span data-stu-id="5e93d-111">Get reminders</span></span>

## <a name="example"></a><span data-ttu-id="5e93d-112">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="5e93d-112">Example</span></span>

<span data-ttu-id="5e93d-113">En el ejemplo siguiente se muestra el aspecto que puede tener el cuadro de diálogo en la reunión desde el punto de vista de un participante de la reunión.</span><span class="sxs-lookup"><span data-stu-id="5e93d-113">The following example shows what the in-meeting dialog might look like from a meeting participant's perspective.</span></span> <span data-ttu-id="5e93d-114">Como puede ver, el contenido y la tarea son ligeros.</span><span class="sxs-lookup"><span data-stu-id="5e93d-114">As you can see, the content and task are lightweight.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-participant-view.png" alt-text="Ejemplo muestra el aspecto que puede tener el cuadro de diálogo en la reunión desde el punto de vista de un participante de la reunión.":::

<span data-ttu-id="5e93d-116"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Vea el escenario completo (Figma)</a></span><span class="sxs-lookup"><span data-stu-id="5e93d-116"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See the full scenario (Figma)</a></span></span>

<span data-ttu-id="5e93d-117"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Consulte otros ejemplos de casos de uso (Figma)</a></span><span class="sxs-lookup"><span data-stu-id="5e93d-117"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See other example use cases (Figma)</a></span></span>

## <a name="anatomy"></a><span data-ttu-id="5e93d-118">Anatomía</span><span class="sxs-lookup"><span data-stu-id="5e93d-118">Anatomy</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-anatomy.png" alt-text="Anatomía de la interfaz de usuario de una vista de diálogo en la reunión." border="false":::

1. <span data-ttu-id="5e93d-120">**Icono de aplicación**</span><span class="sxs-lookup"><span data-stu-id="5e93d-120">**App icon**</span></span>
1. <span data-ttu-id="5e93d-121">**Nombre de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="5e93d-121">**App name**</span></span>
1. <span data-ttu-id="5e93d-122">**Cadena de acción**</span><span class="sxs-lookup"><span data-stu-id="5e93d-122">**Action string**</span></span>
1. <span data-ttu-id="5e93d-123">**Descartar icono:** Cierra un único cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5e93d-123">**Dismiss icon:** Closes a single dialog.</span></span> <span data-ttu-id="5e93d-124">Use siempre el icono de cierre superior derecho en lugar de una acción en el pie de página.</span><span class="sxs-lookup"><span data-stu-id="5e93d-124">Always use the upper-right close icon instead of an action in the footer.</span></span>
1. <span data-ttu-id="5e93d-125">**Vista WebView** : muestra todo el contenido de la aplicación de terceros y los botones (se recomiendan los botones estándar de Microsoft Teams).</span><span class="sxs-lookup"><span data-stu-id="5e93d-125">**Webview** : Displays all third-party app content and buttons (standard Teams buttons recommended).</span></span>

### <a name="sizing"></a><span data-ttu-id="5e93d-126">Evaluación</span><span class="sxs-lookup"><span data-stu-id="5e93d-126">Sizing</span></span>

<span data-ttu-id="5e93d-127">Los cuadros de diálogo en la reunión pueden variar en tamaño para tener en cuenta los diferentes casos de uso, pero siempre debe mantener el relleno y los tamaños de los componentes.</span><span class="sxs-lookup"><span data-stu-id="5e93d-127">In-meeting dialogs can vary in size to account for different use cases, but you must always maintain padding and component sizes.</span></span>

* <span data-ttu-id="5e93d-128">**Height** : el alto del cuadro de diálogo depende del contenido de la vista WebView.</span><span class="sxs-lookup"><span data-stu-id="5e93d-128">**Height** : The height of the dialog is determined by the content in the webview.</span></span> <span data-ttu-id="5e93d-129">El desplazamiento vertical toma el control del contenido que supera el alto máximo especificado.</span><span class="sxs-lookup"><span data-stu-id="5e93d-129">Vertical scroll takes over for content that exceeds the maximum height you specify.</span></span>
* <span data-ttu-id="5e93d-130">**Width** : el ancho de la vista WebView es un valor absoluto dentro del intervalo especificado.</span><span class="sxs-lookup"><span data-stu-id="5e93d-130">**Width** : The width of the webview is an absolute value within the range you specify.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-sizing.png" alt-text="Ilustración que muestra las dimensiones posibles de un cuadro de diálogo en la reunión. Height: el alto del cuadro de diálogo depende del contenido de la vista WebView. El desplazamiento vertical toma el control del contenido que supera la altura máxima (definido por el usuario). Min: ninguno. Máx: 400 píxeles (320 píxeles WebView). Width: el ancho de la vista WebView es un valor absoluto dentro del intervalo especificado. Min.: 288 píxeles (256 píxeles WebView). Máx: 468 píxeles (436 píxeles WebView)." border="false":::

## <a name="behavior"></a><span data-ttu-id="5e93d-132">Comportamiento</span><span class="sxs-lookup"><span data-stu-id="5e93d-132">Behavior</span></span>

<span data-ttu-id="5e93d-133">Vea comportamiento general del cuadro de diálogo de reunión en la reunión, como REST, carga, etc., en <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.</span><span class="sxs-lookup"><span data-stu-id="5e93d-133">See general in-meeting dialog behavior, such as rest, loading, and more, in <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.</span></span>

### <a name="position"></a><span data-ttu-id="5e93d-134">Position</span><span class="sxs-lookup"><span data-stu-id="5e93d-134">Position</span></span>

<span data-ttu-id="5e93d-135">Los diálogos en la reunión se alinean en el centro de la fase de reunión.</span><span class="sxs-lookup"><span data-stu-id="5e93d-135">In-meeting dialogs are aligned in the center of the meeting stage.</span></span> <span data-ttu-id="5e93d-136">No se pueden arrastrar y trabajar en el marco de las notificaciones de nivel de sistema de Teams.</span><span class="sxs-lookup"><span data-stu-id="5e93d-136">They can’t be dragged and work within the framework of Teams system-level notifications.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-position.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un cuadro de diálogo en la reunión." border="false":::

### <a name="aggregation"></a><span data-ttu-id="5e93d-138">Cronológica</span><span class="sxs-lookup"><span data-stu-id="5e93d-138">Aggregation</span></span>

<span data-ttu-id="5e93d-139">Solo se muestra un cuadro de diálogo a la vez, la clasificación de la pila de la última a la más reciente que se envía a la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="5e93d-139">Only one dialog displays at a time, stack ranking from last to most recent sent to the bottom.</span></span> <span data-ttu-id="5e93d-140">Una vez que se resuelve o se descarta un cuadro de diálogo, el siguiente se ocupa de su posición.</span><span class="sxs-lookup"><span data-stu-id="5e93d-140">Once a dialog is resolved or dismissed, the next one take its place.</span></span>

<span data-ttu-id="5e93d-141"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Vea un ejemplo (Figma)</a></span><span class="sxs-lookup"><span data-stu-id="5e93d-141"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See an example (Figma)</a></span></span>

### <a name="scrolling"></a><span data-ttu-id="5e93d-142">Desplazamiento</span><span class="sxs-lookup"><span data-stu-id="5e93d-142">Scrolling</span></span>

<span data-ttu-id="5e93d-143">El desplazamiento se produce en la parte de WebView de un cuadro de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="5e93d-143">Scrolling occurs in the webview portion of an in-meeting dialog.</span></span> <span data-ttu-id="5e93d-144">Recuerde lo siguiente sobre el desplazamiento:</span><span class="sxs-lookup"><span data-stu-id="5e93d-144">Remember the following about scrolling:</span></span>

* <span data-ttu-id="5e93d-145">Solo debe poder desplazarse verticalmente.</span><span class="sxs-lookup"><span data-stu-id="5e93d-145">You should only be able to scroll vertically.</span></span>
* <span data-ttu-id="5e93d-146">Solo puede ver el contenido al que se ha desplazado (nada anterior o posterior).</span><span class="sxs-lookup"><span data-stu-id="5e93d-146">You can only see the content you've scrolled to (nothing above or below).</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-scroll.png" alt-text="Ilustración que muestra cómo funciona el desplazamiento del contenido de WebView en el cuadro de diálogo de la reunión." border="false":::

### <a name="buttons"></a><span data-ttu-id="5e93d-148">Botones</span><span class="sxs-lookup"><span data-stu-id="5e93d-148">Buttons</span></span>

<span data-ttu-id="5e93d-149">Los botones de cuadro de diálogo en la reunión forman parte de la vista Web ([vea algunos ejemplos](#best-practices)).</span><span class="sxs-lookup"><span data-stu-id="5e93d-149">In-meeting dialog buttons are part of the webview ([see some examples](#best-practices)).</span></span>

<span data-ttu-id="5e93d-150">A diferencia de los componentes similares, los cuadros de diálogo en la reunión se desechan una vez que un usuario selecciona un botón.</span><span class="sxs-lookup"><span data-stu-id="5e93d-150">Unlike similar components, in-meeting dialogs are dismissed once a user selects a button.</span></span>

## <a name="components"></a><span data-ttu-id="5e93d-151">Componentes</span><span class="sxs-lookup"><span data-stu-id="5e93d-151">Components</span></span>

<span data-ttu-id="5e93d-152">Los cuadros de diálogo en la reunión se crean principalmente con los siguientes componentes de la <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">interfaz de usuario (Figma)</a>, que se basan en el <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">sistema de diseño de Fluent</a>.</span><span class="sxs-lookup"><span data-stu-id="5e93d-152">In-meeting dialogs are built primarily with the following <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">UI components (Figma)</a>, which are based on the <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent Design System</a>.</span></span>

<span data-ttu-id="5e93d-153">Componente</span><span class="sxs-lookup"><span data-stu-id="5e93d-153">Component</span></span> | <span data-ttu-id="5e93d-154">Instrucciones</span><span class="sxs-lookup"><span data-stu-id="5e93d-154">Guidelines</span></span> | <span data-ttu-id="5e93d-155">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="5e93d-155">Example</span></span>
 - | - | -
<span data-ttu-id="5e93d-156">Botón</span><span class="sxs-lookup"><span data-stu-id="5e93d-156">Button</span></span> | <span data-ttu-id="5e93d-157">Los botones principal y secundario pueden ser medios o pequeños.</span><span class="sxs-lookup"><span data-stu-id="5e93d-157">Primary and secondary buttons can be medium or small</span></span> | <span data-ttu-id="5e93d-158">Enviar una respuesta</span><span class="sxs-lookup"><span data-stu-id="5e93d-158">Send a response</span></span>
<span data-ttu-id="5e93d-159">Input</span><span class="sxs-lookup"><span data-stu-id="5e93d-159">Input</span></span> | <span data-ttu-id="5e93d-160">Campo para la entrada de breves usuarios.</span><span class="sxs-lookup"><span data-stu-id="5e93d-160">Field for brief user input.</span></span> <span data-ttu-id="5e93d-161">El texto de la etiqueta puede incluir un icono</span><span class="sxs-lookup"><span data-stu-id="5e93d-161">Label text can include an icon</span></span>  | <span data-ttu-id="5e93d-162">Escribir comentarios</span><span class="sxs-lookup"><span data-stu-id="5e93d-162">Enter feedback</span></span>
<span data-ttu-id="5e93d-163">Desplegable</span><span class="sxs-lookup"><span data-stu-id="5e93d-163">Dropdown</span></span> | <span data-ttu-id="5e93d-164">Seleccione una o más opciones de una lista.</span><span class="sxs-lookup"><span data-stu-id="5e93d-164">Select one or more options from a list.</span></span> <span data-ttu-id="5e93d-165">Puede incluir características de búsqueda y de selección múltiple</span><span class="sxs-lookup"><span data-stu-id="5e93d-165">Can include search and multi-selection features</span></span> | <span data-ttu-id="5e93d-166">Elegir un idioma</span><span class="sxs-lookup"><span data-stu-id="5e93d-166">Choose a language</span></span>
<span data-ttu-id="5e93d-167">Controles de selección</span><span class="sxs-lookup"><span data-stu-id="5e93d-167">Selection controls</span></span> | <span data-ttu-id="5e93d-168">Use casillas de verificación para varias opciones o botones de radio y conmute a opciones únicas.</span><span class="sxs-lookup"><span data-stu-id="5e93d-168">Use checkboxes for multiple choices or radio buttons and toggles for single choices.</span></span> <span data-ttu-id="5e93d-169">Para selecciones más detalladas, use un control deslizante.</span><span class="sxs-lookup"><span data-stu-id="5e93d-169">For more detailed selections, use a slider</span></span> | <span data-ttu-id="5e93d-170">Votar en un sondeo</span><span class="sxs-lookup"><span data-stu-id="5e93d-170">Vote in a poll</span></span>
<span data-ttu-id="5e93d-171">Alertas</span><span class="sxs-lookup"><span data-stu-id="5e93d-171">Alerts</span></span> | <span data-ttu-id="5e93d-172">Tanto si muestra un mensaje urgente, un estado de error o una advertencia, el mensaje debe ser corto y no interrumpir la tarea actual del usuario</span><span class="sxs-lookup"><span data-stu-id="5e93d-172">Whether displaying an urgent message, error state, or warning, the message should be short and won't interrupt the user's current task</span></span> | <span data-ttu-id="5e93d-173">Mostrar problema al enviar una respuesta</span><span class="sxs-lookup"><span data-stu-id="5e93d-173">Display issue when submitting a response</span></span>

## <a name="theming"></a><span data-ttu-id="5e93d-174">Creación de temas</span><span class="sxs-lookup"><span data-stu-id="5e93d-174">Theming</span></span>

### <a name="colors"></a><span data-ttu-id="5e93d-175">Colores</span><span class="sxs-lookup"><span data-stu-id="5e93d-175">Colors</span></span>

<span data-ttu-id="5e93d-176">Use la <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">combinación de colores recomendada (Figma)</a> para los fondos, los en primer plano y los Estados que transmiten.</span><span class="sxs-lookup"><span data-stu-id="5e93d-176">Use the <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">recommended color scheme (Figma)</a> for backgrounds, foregrounds, and conveying states.</span></span>

### <a name="typography"></a><span data-ttu-id="5e93d-177">Tipografía</span><span class="sxs-lookup"><span data-stu-id="5e93d-177">Typography</span></span>

<span data-ttu-id="5e93d-178">Use los <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">tamaños y pesos de fuente recomendados (Figma)</a> para títulos, texto principal y texto de metadatos.</span><span class="sxs-lookup"><span data-stu-id="5e93d-178">Use the <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">recommended font sizes and weights (Figma)</a> for titles, body text, and metadata text.</span></span>

## <a name="best-practices"></a><span data-ttu-id="5e93d-179">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="5e93d-179">Best practices</span></span>

<span data-ttu-id="5e93d-180">Aunque los cuadros de diálogo en la reunión pueden hacer que las llamadas sean más eficaces, también pueden descarrilar las llamadas si son demasiado molestas.</span><span class="sxs-lookup"><span data-stu-id="5e93d-180">While in-meeting dialogs can make calls more effective, they also can derail calls if too obtrusive.</span></span> <span data-ttu-id="5e93d-181">En general, use los cuadros de diálogo con moderación y siga estos procedimientos recomendados.</span><span class="sxs-lookup"><span data-stu-id="5e93d-181">In general, use the dialogs sparingly and follow these best practices.</span></span>

### <a name="navigation"></a><span data-ttu-id="5e93d-182">Navegación</span><span class="sxs-lookup"><span data-stu-id="5e93d-182">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-steps-do.png" alt-text="Ilustración que muestra cómo limitar el contenido del cuadro de diálogo de reunión en una sola pantalla para que los usuarios puedan centrarse en la reunión." border="false":::

#### <a name="do-keep-it-contained"></a><span data-ttu-id="5e93d-184">Do: Keep it contenida</span><span class="sxs-lookup"><span data-stu-id="5e93d-184">Do: Keep it contained</span></span>

<span data-ttu-id="5e93d-185">Limite el contenido del cuadro de diálogo de reunión a una sola pantalla para que los usuarios puedan centrarse en la reunión.</span><span class="sxs-lookup"><span data-stu-id="5e93d-185">Limit in-meeting dialog content to a single screen so users can focus on the meeting.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-steps-dont.png" alt-text="Ilustración que muestra cómo los cuadros de diálogo en la reunión no deben requerir que los usuarios naveguen por el contenido." border="false":::

#### <a name="dont-include-multiple-steps"></a><span data-ttu-id="5e93d-187">No: incluir varios pasos</span><span class="sxs-lookup"><span data-stu-id="5e93d-187">Don't: Include multiple steps</span></span>

<span data-ttu-id="5e93d-188">Los cuadros de diálogo en la reunión no deben requerir que los usuarios naveguen por el contenido.</span><span class="sxs-lookup"><span data-stu-id="5e93d-188">In-meeting dialogs shouldn't require users to navigate through content.</span></span>

   :::column-end:::
:::row-end:::

### <a name="interactions"></a><span data-ttu-id="5e93d-189">Existentes</span><span class="sxs-lookup"><span data-stu-id="5e93d-189">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-interactions-do.png" alt-text="Ilustración que muestra por qué debe quitar contenido innecesario que no ayude a los usuarios a realizar algo rápidamente." border="false":::

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-interactions-dont.png" alt-text="Otra ilustración que muestra por qué debe quitar contenido innecesario que no ayude a los usuarios a realizar algo rápidamente." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-tab-do.png" alt-text="Ilustración que muestra que, si necesita interacciones complejas, se recomienda que use una sola columna en el panel derecho de la reunión en su lugar." border="false":::

#### <a name="do-limit-number-of-interactions"></a><span data-ttu-id="5e93d-193">Do: limitar el número de interacciones</span><span class="sxs-lookup"><span data-stu-id="5e93d-193">Do: Limit number of interactions</span></span>

<span data-ttu-id="5e93d-194">Quite el contenido innecesario que no ayude a los usuarios a realizar algo rápidamente.</span><span class="sxs-lookup"><span data-stu-id="5e93d-194">Remove unnecessary content that doesn't help users accomplish something quickly.</span></span> <span data-ttu-id="5e93d-195">Si necesita interacciones complejas, se recomienda encarecidamente que, en su lugar, se muestre el contenido con una sola columna de la pestaña en reunión.</span><span class="sxs-lookup"><span data-stu-id="5e93d-195">If you need complex interactions, we strongly recommend displaying your content using a single column on the in-meeting tab instead.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-tab-dont.png" alt-text="Ilustración que muestra que demasiadas interacciones en el cuadro de diálogo de la reunión distrae de la reunión." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="5e93d-197">No: introducir elementos innecesarios</span><span class="sxs-lookup"><span data-stu-id="5e93d-197">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="5e93d-198">Es posible que pueda diseñar un único cuadro de diálogo en reunión con varias interacciones, pero demasiados pueden distraerse de la reunión.</span><span class="sxs-lookup"><span data-stu-id="5e93d-198">You may be able to design a single in-meeting dialog with multiple interactions, but too many can distract from the meeting.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="5e93d-199">Diseño</span><span class="sxs-lookup"><span data-stu-id="5e93d-199">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-layout-do.png" alt-text="Ilustración que muestra un diseño ideal para los cuadros de diálogo en reunión." border="false":::

#### <a name="do-use-single-column-layouts"></a><span data-ttu-id="5e93d-201">Do: usar diseños de columna única</span><span class="sxs-lookup"><span data-stu-id="5e93d-201">Do: Use single-column layouts</span></span>

<span data-ttu-id="5e93d-202">Como los cuadros de diálogo están en el centro de la fase de reunión, la finalización de la tarea debería ser rápida y sencilla para evitar la frustración del usuario.</span><span class="sxs-lookup"><span data-stu-id="5e93d-202">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-layout-dont.png" alt-text="Ilustración que muestra el diseño de los cuadros de diálogo en reunión que no se recomienda." border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="5e93d-204">No: desorden el espacio</span><span class="sxs-lookup"><span data-stu-id="5e93d-204">Don't: Clutter the space</span></span>

<span data-ttu-id="5e93d-205">Un contenido denso o con gran estructura puede ser molesto y abrumador, especialmente durante una reunión.</span><span class="sxs-lookup"><span data-stu-id="5e93d-205">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

### <a name="size"></a><span data-ttu-id="5e93d-206">Size</span><span class="sxs-lookup"><span data-stu-id="5e93d-206">Size</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-size-do.png" alt-text="Ilustración que muestra cómo el tamaño del cuadro de diálogo en la reunión siempre debe ser el mismo." border="false":::

#### <a name="do-keep-it-consistent"></a><span data-ttu-id="5e93d-208">Do: mantener la coherencia</span><span class="sxs-lookup"><span data-stu-id="5e93d-208">Do: Keep it consistent</span></span>

<span data-ttu-id="5e93d-209">Esto es importante porque los cuadros de diálogo en la reunión siempre se muestran en la misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="5e93d-209">This is important because in-meeting dialogs always display in the same location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-size-dont.png" alt-text="Ilustración que muestra cómo no se deben usar diferentes tamaños de cuadro de diálogo." border="false":::

#### <a name="dont-always-fit-to-the-content"></a><span data-ttu-id="5e93d-211">No: siempre se ajusta al contenido</span><span class="sxs-lookup"><span data-stu-id="5e93d-211">Don't: Always fit to the content</span></span>

<span data-ttu-id="5e93d-212">Es posible que esté intentando evitar el desplazamiento horizontal, pero varios tamaños de cuadro de diálogo en la reunión dentro de la misma aplicación son una experiencia incoherente.</span><span class="sxs-lookup"><span data-stu-id="5e93d-212">You may be trying to avoid horizontal scrolling, but multiple in-meeting dialog sizes within the same app is an inconsistent experience.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="5e93d-213">Controles</span><span class="sxs-lookup"><span data-stu-id="5e93d-213">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-controls-do.png" alt-text="Ilustración que muestra dónde situar botones en el cuadro de diálogo en reunión." border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="5e93d-215">Haga lo siguiente: alinear a la derecha la acción principal</span><span class="sxs-lookup"><span data-stu-id="5e93d-215">Do: Right align the primary action</span></span>

<span data-ttu-id="5e93d-216">Le recomendamos que sitúe la acción más intensa visualmente en la posición más a la derecha.</span><span class="sxs-lookup"><span data-stu-id="5e93d-216">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-controls-dont.png" alt-text="Ilustración que muestra dónde no desea situar botones en el cuadro de diálogo en reunión." border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="5e93d-218">No: acciones alineadas a la izquierda o al centro</span><span class="sxs-lookup"><span data-stu-id="5e93d-218">Don't: Left or center align actions</span></span>

<span data-ttu-id="5e93d-219">Esto se desvía del patrón de equipos estándar para la colocación de controles en un cuadro de diálogo y puede entrar en conflicto con un cuadro de diálogo detrás de uno superior.</span><span class="sxs-lookup"><span data-stu-id="5e93d-219">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

## <a name="accessibility"></a><span data-ttu-id="5e93d-220">Accesibilidad</span><span class="sxs-lookup"><span data-stu-id="5e93d-220">Accessibility</span></span>

<span data-ttu-id="5e93d-221">Para obtener información sobre la accesibilidad, vea <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.</span><span class="sxs-lookup"><span data-stu-id="5e93d-221">For information on accessibility, see <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.</span></span>

## <a name="resources"></a><span data-ttu-id="5e93d-222">Recursos</span><span class="sxs-lookup"><span data-stu-id="5e93d-222">Resources</span></span>

* <span data-ttu-id="5e93d-223"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Archivo Figma de extensiones de reunión de Microsoft Teams</a></span><span class="sxs-lookup"><span data-stu-id="5e93d-223"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Microsoft Teams meeting extensions Figma file</a></span></span>

## <a name="validate-your-design"></a><span data-ttu-id="5e93d-224">Validar el diseño</span><span class="sxs-lookup"><span data-stu-id="5e93d-224">Validate your design</span></span>

<span data-ttu-id="5e93d-225">Si planea publicar la aplicación en AppSource, debe comprender los problemas de diseño que suelen hacer que las aplicaciones fallen durante el envío.</span><span class="sxs-lookup"><span data-stu-id="5e93d-225">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5e93d-226">Comprobar las instrucciones de validación del diseño</span><span class="sxs-lookup"><span data-stu-id="5e93d-226">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)

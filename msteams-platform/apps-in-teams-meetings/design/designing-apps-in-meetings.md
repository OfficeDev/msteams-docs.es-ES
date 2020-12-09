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
# <a name="designing-your-microsoft-teams-meeting-extension"></a>Diseño de la extensión de reunión de Microsoft Teams

Puede crear aplicaciones para que las reuniones sean más productivas. Por ejemplo, solicite a los usuarios que completen una encuesta durante una llamada o envíen un recordatorio rápido que no interrumpa el flujo de la reunión.

## <a name="microsoft-teams-ui-kit"></a>Kit de IU de Microsoft Teams

Puede encontrar instrucciones de diseño más completas, incluidos elementos que puede captar y modificar según sea necesario, en el kit de interfaz de usuario de Microsoft Teams.

> [!div class="nextstepaction"]
> [Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>Agregar una extensión de reunión

Puede Agregar una extensión de reunión antes y durante las reuniones. También puede disponer de una aplicación para una reunión específica directamente desde la tienda Teams (AppSource).

### <a name="add-before-a-meeting"></a>Agregar antes de una reunión

Antes de una reunión, los detalles de la reunión seleccionan **Agregar una pestaña +** para abrir el control flotante de la aplicación y buscar aplicaciones optimizadas para las reuniones.

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="Ejemplo se muestra cómo agregar una extensión de reunión antes de una reunión." border="false":::

### <a name="add-during-a-meeting"></a>Agregar durante una reunión

En una reunión, seleccione **más** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **Agregar una aplicación** y elija la aplicación que desee.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="Ejemplo se muestra cómo agregar una extensión de reunión durante una reunión." border="false":::

## <a name="before-a-meeting"></a>Antes de una reunión

Antes de la reunión, puede agregar contenido en la pestaña. En el ejemplo siguiente se muestra un borrador de una pregunta de encuesta que las personas responderán durante la llamada.

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="En el ejemplo se muestra cómo se muestra el contenido de la aplicación en los detalles de la reunión antes de una llamada." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>Anatomía: pestaña reunión (antes y después de las reuniones)

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="Ejemplo muestra la anatomía estructural de una pestaña de reunión antes y después de una reunión." border="false":::

|Counter|Descripción|
|----------|-----------|
|1|**Nombre de ficha**: etiqueta de navegación de la pestaña.|
|2 |**Desbordamiento de tabulación**: abre acciones de pestaña, como cambiar nombre y quitar.|
|3 |**iframe**: muestra el contenido de la aplicación.|

### <a name="designing-with-ui-templates"></a>Diseño con plantillas de interfaz de usuario

Use una de las siguientes plantillas de interfaz de usuario de Microsoft Teams para ayudar a diseñar la pestaña de la reunión:

* [List](../../concepts/design/design-teams-app-ui-templates.md#list): lists puede mostrar elementos relacionados en un formato que se pueda analizar y permitir que los usuarios realicen acciones en una lista completa o en elementos individuales.
* [Panel de tareas](../../concepts/design/design-teams-app-ui-templates.md#task-board): un panel de tareas, a veces denominado tablero Kanban o carriles de nadar, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o vales.
* [Panel](../../concepts/design/design-teams-app-ui-templates.md#dashboard): un panel es un lienzo que contiene varias tarjetas que proporcionan información general sobre datos o contenido.
* [Formulario](../../concepts/design/design-teams-app-ui-templates.md#form): los formularios son para recopilar, validar y enviar entradas de usuario de forma estructurada.
* [Estado vacío](../../concepts/design/design-teams-app-ui-templates.md#empty-state): la plantilla de estado vacía se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error, etc.
* Panel de [navegación izquierdo](../../concepts/design/design-teams-app-ui-templates.md#left-nav): la plantilla de navegación izquierda puede servir de ayuda si la pestaña requiere la navegación. En general, debe mantener al mínimo la navegación por tabulaciones.

## <a name="use-an-in-meeting-tab"></a>Usar una pestaña en la reunión

La pestaña en reunión es un lienzo para aumentar la colaboración durante las reuniones. Los asistentes pueden ver e interactuar con el contenido de la aplicación en un espacio dedicado fuera de la fase de reunión a través de vistas compartidas o basadas en roles.

### <a name="use-cases"></a>Casos de uso

Los usuarios pueden usar la ficha en la reunión para:

* Proporcionar comentarios detallados (por ejemplo, evaluar un candidato de trabajo)
* Crear rápidamente un sondeo, una encuesta o un elemento de tarea para los participantes de la reunión
* Mostrar notas relevantes para la reunión (por ejemplo, información sobre un responsable de ventas)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="Ejemplo muestra cómo puede presentar el contenido de sondeo en una pestaña en la reunión." border="false":::

### <a name="anatomy-in-meeting-tab"></a>Anatomía: ficha en la reunión

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="Ejemplo muestra la anatomía estructural de una pestaña en reunión." border="false":::

|Counter|Descripción|
|----------|-----------|
|1|**Icono de la aplicación (seleccionado)**: logotipo de aplicación transparente de 16 píxeles.|
|2 |**Nombre de la aplicación**|
|3 |**Header**: incluye el nombre de la aplicación.|
|4 |**Botón Cerrar**: descarta la pestaña. Use siempre el icono de cierre superior derecho en lugar de una acción en el pie de página.|
|5 |**Barra de notificación**: las alertas de error se muestran directamente debajo del encabezado y disminuyen el contenido de iframe en 20 píxeles.|
|6 |**iframe**: muestra el contenido de la aplicación.|

### <a name="spacing"></a>Spacing

Optimice la ficha en reunión para ajustar la periferia a la periferia dentro del área iframe de 280 píxeles de ancho. Hay 20 píxeles de relleno a los lados izquierdo y derecho del iframe y entre el encabezado de la pestaña. El iframe es con sangrado completo en la parte inferior de la ficha.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="Ejemplo muestra las dimensiones del espacio de la pestaña en la reunión." border="false":::

### <a name="scrolling"></a>Desplazamiento

El contenido de iframe debe desplazarse verticalmente. Solo puede ver el contenido al que se ha desplazado (nada anterior o posterior). La barra de desplazamiento es parte del contenido iframe.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="Ejemplo muestra cómo se desplaza la pestaña en reunión." border="false":::

### <a name="navigation"></a>Navegación

Para los escenarios con capas de navegación o contenido pesado, se recomienda permitir que los usuarios naveguen a una capa secundaria. Los usuarios deben poder volver a la capa anterior.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="Ejemplo muestra la navegación en reuniones." border="false":::

## <a name="use-an-in-meeting-dialog"></a>Usar un cuadro de diálogo en la reunión

Los cuadros de diálogo en la reunión se muestran en la fase de reunión de Microsoft Teams. Requieren la atención, la confirmación o la interacción del usuario, pero son sutiles y no interrumpen la reunión. Debe usarlos con moderación y para escenarios claros y orientados a tareas.

### <a name="use-cases"></a>Casos de uso

Los cuadros de diálogo en la reunión son desencadenados por un usuario (como el organizador de la reunión) que puede desear a los participantes:

* Proporcionar comentarios breves
* Realizar una breve encuesta o sondeo
* Enviar aprobaciones
* Recibir recordatorios

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="Ejemplo se muestra cómo se puede usar un cuadro de diálogo en la reunión." border="false":::

### <a name="anatomy-in-meeting-dialog"></a>Anatomía: cuadro de diálogo en la reunión

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="Ejemplo muestra la anatomía estructural de un cuadro de diálogo en la reunión." border="false":::

|Counter|Descripción|
|----------|-----------|
|1|**Header**: incluye el icono de la aplicación, el nombre, la cadena de acción y el icono de cierre.|
|2 |**iframe**: muestra el contenido de la aplicación.|

### <a name="anatomy-in-meeting-dialog-header"></a>Anatomía: encabezado de cuadro de diálogo en la reunión

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="Ejemplo muestra la anatomía estructural de un encabezado de cuadro de diálogo en reunión." border="false":::

Hay dos variantes de encabezado. Si es posible, use la variante con el avatar para reforzar que el cuadro de diálogo procede de una persona.

|Counter|Descripción|
|----------|-----------|
|1|**Avatar**: persona que inicia el cuadro de diálogo en la reunión.|
|2 |**Icono de aplicación**|
|3 |**Nombre de la aplicación**|
|4 |**Botón Cerrar**: descarta el cuadro de diálogo.|
|5 |**Cadena de acción**: normalmente describe quién inició el cuadro de diálogo.|

### <a name="responsive-behavior"></a>Comportamiento dinámico

Los cuadros de diálogo en la reunión pueden variar en tamaño para tener en cuenta los distintos escenarios. Asegúrese de mantener el relleno y los tamaños de los componentes.

* **Width**: el ancho del iframe es un valor absoluto dentro del intervalo especificado.
* **Height**: el alto del cuadro de diálogo viene determinado por el contenido en el iframe. El desplazamiento vertical toma el control del contenido que supera el alto máximo.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="Ejemplo muestra el cuadro de diálogo en la reunión. Width: min--280 píxeles (248 píxeles iframe). Max--460 píxeles (428 píxeles iframe). Altura: 300 píxeles (iframe)." border="false":::

## <a name="after-a-meeting"></a>Después de una reunión

Puede volver a una reunión después de finalizar y ver el contenido de la aplicación. En este ejemplo, el organizador de la reunión puede mirar los resultados del sondeo en la pestaña **contoso** . (Nota: desde el punto de vista del diseño, no hay ninguna diferencia entre la experiencia de pestañas previa y posterior a la reunión).

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="Ejemplo muestra una pestaña posterior a la reunión." border="false":::

## <a name="best-practices"></a>Procedimientos recomendados

### <a name="interactions"></a>Existentes

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a>Do: limitar el número de interacciones

Para los cuadros de diálogo en la reunión, quite el contenido innecesario que no ayude a los usuarios a realizar algo rápidamente.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a>No: introducir elementos innecesarios

Un único cuadro de diálogo en reunión con varias interacciones puede distraerse de la llamada.

   :::column-end:::
:::row-end:::

### <a name="layout"></a>Diseño

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="do-use-single-column-layouts"></a>Do: usar diseños de columna única

Como los cuadros de diálogo están en el centro de la fase de reunión, la finalización de la tarea debería ser rápida y sencilla para evitar la frustración del usuario.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="dont-clutter-the-space"></a>No: desorden el espacio

Un contenido denso o con gran estructura puede ser molesto y abrumador, especialmente durante una reunión.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="do-use-single-columns"></a>Do: usar columnas únicas

Dada la naturaleza estrecha de las pestañas de la reunión, se recomienda encarecidamente mostrar el contenido en una sola columna.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="dont-use-multiple-columns"></a>No: usar varias columnas

Debido al espacio limitado de la pestaña en reunión, no se recomiendan los diseños con más de una columna.

   :::column-end:::
:::row-end:::

### <a name="controls"></a>Controles

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="do-right-align-the-primary-action"></a>Haga lo siguiente: alinear a la derecha la acción principal

Le recomendamos que positioining la acción más intensa para la ubicación más a la derecha.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="dont-left-or-center-align-actions"></a>No: acciones alineadas a la izquierda o al centro

Esto se desvía del patrón de equipos estándar para la colocación de controles en un cuadro de diálogo y puede entrar en conflicto con un cuadro de diálogo detrás de uno superior.

   :::column-end:::
:::row-end:::

### <a name="scroll"></a>Scroll

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="do-scroll-vertically"></a>Hacer: desplazarse verticalmente

Le recomendamos que sitúe la acción más intensa visualmente en la posición más a la derecha.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="dont-scroll-horizontally"></a>No: desplazar horizontalmente

El desplazamiento horizontal no es un comportamiento esperado en Microsoft Teams. Otros lienzos del entorno de la reunión se desplazan verticalmente.

   :::column-end:::
:::row-end:::

### <a name="workflows"></a>Flujos de trabajo

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a>Do: escenarios complejos de Surface en la pestaña en la reunión

Si la aplicación incluye varias tareas, se recomienda encarecidamente un diseño de una sola columna en una pestaña en la reunión.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="dont-package-complex-scenarios-in-the-in-meeting-dialog"></a>No: empaquetar escenarios complejos en el cuadro de diálogo de la reunión

Los diálogos en la reunión están pensados para interacciones breves.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Creación de temas

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="do-use-teams-color-tokens"></a>Do: usar tokens de color de Teams

Las reuniones de Microsoft Teams están optimizadas para el modo oscuro para ayudar a reducir el ruido visual y cognitivo para que los usuarios puedan centrarse en la discusión y en el contenido compartido. Obtenga información sobre cómo usar <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">tokens de color (interfaz de usuario de Fluent)</a>.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="dont-include-another-dismiss-button"></a>No: incluir otro botón descartar

Ofrecer una opción para cerrar el contenido de la pestaña en la reunión puede causar problemas porque ya hay un botón en el encabezado para descartar la misma pestaña en la reunión.

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>Navegación

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="do-have-a-back-button"></a>Do: tener un botón atrás

Si tiene más de una capa de navegación en una pestaña en la reunión, los usuarios deben poder volver a sus vistas anteriores.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="dont-include-another-dismiss-button"></a>No: incluir otro botón descartar

Ofrecer una opción para cerrar el contenido de la pestaña en la reunión puede causar problemas porque ya hay un botón en el encabezado para descartar la misma pestaña en la reunión.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de reunión." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a>PRECAUCIÓN: Evite los modales en la pestaña en la reunión.

Los modales (también conocidos como módulos de tareas) en la ficha in-Meeting ya estrecha pueden ajustar y oscurecer el contenido.

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a>Validar el diseño

Si planea publicar la aplicación en AppSource, debe comprender los problemas de diseño que suelen hacer que las aplicaciones fallen durante el envío.

> [!div class="nextstepaction"]
> [Comprobar las instrucciones de validación del diseño](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)

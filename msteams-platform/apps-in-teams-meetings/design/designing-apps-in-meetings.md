---
title: Diseño de la extensión de reunión
author: heath-hamilton
description: Obtén información sobre cómo diseñar aplicaciones en Teams reuniones y obtener el kit Microsoft Teams interfaz de usuario.
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
# <a name="designing-your-microsoft-teams-meeting-extension"></a>Diseño de la extensión Microsoft Teams reunión

Puedes crear aplicaciones para que las reuniones sean más productivas. Por ejemplo, pida a los usuarios que completen una encuesta durante una llamada o envíen un aviso rápido que no interrumpa el flujo de la reunión.

## <a name="microsoft-teams-ui-kit"></a>Kit de UI de Microsoft Teams

Puedes encontrar instrucciones de diseño más completas, incluidos los elementos que puedes agarrar y modificar según sea necesario, en el kit de interfaz Microsoft Teams usuario.

> [!div class="nextstepaction"]
> [Obtener el Kit de UI de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>Agregar una extensión de reunión

Puede agregar una extensión de reunión antes y durante las reuniones. También puedes agregar una aplicación para una reunión específica directamente desde Teams store (AppSource).

### <a name="add-before-a-meeting"></a>Agregar antes de una reunión

En los detalles de la reunión, selecciona **Agregar una pestaña + para** abrir el control desplegable de la aplicación y buscar aplicaciones optimizadas para reuniones.

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de reunión antes de una reunión." border="false":::

### <a name="add-during-a-meeting"></a>Agregar durante una reunión

En una reunión, selecciona **Más** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **agregar una aplicación** y elige la aplicación que quieras.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de reunión durante una reunión." border="false":::

## <a name="before-a-meeting"></a>Antes de una reunión

Antes de la reunión, puede agregar contenido en la pestaña. En el siguiente ejemplo se muestra un borrador de pregunta de encuesta que los usuarios responderán durante la llamada.

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="En el ejemplo se muestra cómo usar el contenido de la aplicación en los detalles de la reunión antes de una llamada." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>Anatomía: pestaña Reunión (antes y después de las reuniones)

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de una pestaña de reunión antes y después de una reunión." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Nombre de la pestaña:** etiqueta de navegación para la pestaña.|
|2|**Desbordamiento de** tabulación: abre acciones de tabulación, como cambiar el nombre y quitar.|
|3|**iframe:** muestra el contenido de la aplicación.|

### <a name="designing-with-ui-templates"></a>Diseño con plantillas de interfaz de usuario

Usa una de las siguientes plantillas Teams interfaz de usuario para ayudar a diseñar la pestaña de reunión:

* [Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato digitalizado y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.
* [Panel de](../../concepts/design/design-teams-app-ui-templates.md#task-board)tareas: un panel de tareas, a veces denominado tablero de kanban o carriles de natación, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o los vales.
* [Panel:](../../concepts/design/design-teams-app-ui-templates.md#dashboard)un panel es un lienzo que contiene varias tarjetas que proporcionan información general sobre los datos o el contenido.
* [Formulario:](../../concepts/design/design-teams-app-ui-templates.md#form)los formularios son para recopilar, validar y enviar la entrada del usuario de forma estructurada.
* [Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacío se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.
* [Navegación izquierda:](../../concepts/design/design-teams-app-ui-templates.md#left-nav)la plantilla de navegación izquierda puede ayudar si la pestaña requiere algo de navegación. En general, debe mantener la navegación por pestañas al mínimo.

## <a name="use-an-in-meeting-tab"></a>Usar una pestaña en la reunión

La pestaña en la reunión es un lienzo para aumentar la colaboración durante las reuniones. Los asistentes pueden ver e interactuar con el contenido de la aplicación en un espacio dedicado fuera de la fase de reunión a través de vistas compartidas o basadas en roles.

### <a name="use-cases"></a>Casos de uso

Las personas pueden usar la pestaña en la reunión para:

* Proporcionar comentarios detallados. Por ejemplo, evalúe un candidato de trabajo.
* Cree un sondeo, una encuesta o un elemento de tarea para los participantes de la reunión.
* Mostrar notas relevantes para la reunión. Por ejemplo, información sobre un cliente potencial de ventas.

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="En el ejemplo se muestra cómo se puede presentar contenido de sondeo en una pestaña en la reunión." border="false":::

### <a name="anatomy-in-meeting-tab"></a>Anatomía: pestaña En la reunión

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de una pestaña en reunión." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Icono de aplicación (seleccionado):** logotipo de aplicación transparente de 16 píxeles.|
|2|**Nombre de la aplicación**|
|3|**Encabezado:** incluye el nombre de la aplicación.|
|4 |**Botón Cerrar:** descarta la pestaña. Use siempre el icono de cierre superior derecho en lugar de una acción en el pie de página.|
|5 |**Barra de notificaciones:** las alertas de error se muestran directamente debajo del encabezado y presionan el contenido del iframe hacia abajo en 20 píxeles.|
|6 |**iframe:** muestra el contenido de la aplicación.|

### <a name="spacing"></a>Spacing

Optimiza la pestaña en la reunión para que se ajuste de un extremo a otro dentro del área de iframe de 280 píxeles. Hay 20 píxeles de relleno en los lados izquierdo y derecho del iframe y entre el encabezado de pestaña. El iframe está sangrando hasta la parte inferior de la pestaña.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="En el ejemplo se muestran las dimensiones de espaciado de tabulación en la reunión." border="false":::

### <a name="scrolling"></a>Desplazamiento

El contenido de Iframe debe desplazarse verticalmente. Solo puede ver el contenido al que se desplazó (nada superior o inferior). La barra de desplazamiento forma parte del contenido de iframe.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="En el ejemplo se muestra cómo se desplaza la pestaña en la reunión." border="false":::

### <a name="navigation"></a>Navegación

Para escenarios con capas de navegación o contenido intenso, se recomienda permitir a los usuarios navegar a una capa secundaria. Los usuarios deben poder volver a la capa anterior.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="En el ejemplo se muestra la navegación en la reunión." border="false":::

## <a name="use-an-in-meeting-dialog"></a>Usar un cuadro de diálogo en la reunión

Los cuadros de diálogo en la reunión se muestran en la Teams de reunión. Requieren la atención, confirmación o interacción de un usuario, pero son sutiles y no interrumpen la reunión. Debe usarlos con moderación y para escenarios orientados a tareas y ligeras.

### <a name="use-cases"></a>Casos de uso

Los cuadros de diálogo en la reunión son desencadenados por un usuario (como el organizador de la reunión) que puede querer que los participantes:

* Proporcionar comentarios breves
* Realizar una encuesta o sondeo breves
* Enviar aprobaciones
* Recibir recordatorios

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="En el ejemplo se muestra cómo se puede usar un cuadro de diálogo en la reunión." border="false":::

### <a name="anatomy-in-meeting-dialog"></a>Anatomía: cuadro de diálogo en la reunión

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de un cuadro de diálogo en reunión." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Encabezado:** incluye el icono de la aplicación, el nombre, la cadena de acción y el icono cerrar.|
|2|**iframe:** muestra el contenido de la aplicación.|

### <a name="anatomy-in-meeting-dialog-header"></a>Anatomía: encabezado del cuadro de diálogo En la reunión

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de un encabezado de cuadro de diálogo en reunión." border="false":::

Hay dos variantes de encabezado. Cuando sea posible, usa la variante con el avatar para reforzar que el cuadro de diálogo viene de una persona.

|Contador|Descripción|
|----------|-----------|
|1|**Avatar:** persona que inicia el cuadro de diálogo en la reunión.|
|2|**Icono de aplicación**|
|3|**Nombre de la aplicación**|
|4 |**Botón Cerrar:** descarta el cuadro de diálogo.|
|5 |**Cadena de acción:** normalmente describe quién inició el cuadro de diálogo.|

### <a name="responsive-behavior"></a>Comportamiento dinámico

Los cuadros de diálogo en reunión pueden variar en tamaño para tener en cuenta diferentes escenarios. Asegúrese de mantener el relleno y los tamaños de los componentes.

* **Width:** puede especificar el ancho del iframe del cuadro de diálogo en cualquier lugar dentro del intervalo de tamaño admitido.
* **Alto:** puede especificar el alto del iframe del cuadro de diálogo en cualquier lugar dentro del intervalo de tamaño admitido. También puedes permitir que los usuarios se desplacen verticalmente si el contenido de la aplicación supera el alto máximo.

Para implementar, especifique el ancho y el alto con la [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) clave.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="En el ejemplo se muestra el cuadro de diálogo en la reunión. Ancho: Min-280 píxeles (248 píxeles iframe). Máximo: 460 píxeles (428 píxeles de iframe). Alto: 300 píxeles (iframe)." border="false":::

## <a name="after-a-meeting"></a>Después de una reunión

Puedes volver a una reunión después de que finalice y ver el contenido de la aplicación. En este ejemplo, el organizador de la reunión puede ver los resultados del sondeo en la pestaña **Contoso.** (Nota: Desde el punto de vista del diseño, no hay diferencia entre una experiencia de pestaña anterior y posterior a la reunión).

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="La ilustración de ejemplo muestra una pestaña posterior a la reunión." border="false":::

## <a name="best-practices"></a>Procedimientos recomendados

Usa estas recomendaciones para crear una experiencia de aplicación de calidad.

### <a name="interactions"></a>Interacciones

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Ejemplo que muestra cómo limitar el número de interacciones." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a>Hacer: limitar el número de interacciones

Para los cuadros de diálogo en la reunión, quite el contenido innecesario que no ayuda a los usuarios a lograr algo rápidamente.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Ejemplo que muestra cómo no introducir elementos innecesarios." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a>No: introducir elementos innecesarios

Un único cuadro de diálogo en la reunión con varias interacciones puede distraerse de la llamada.

   :::column-end:::
:::row-end:::

### <a name="layout"></a>Diseño

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Ejemplo que muestra cómo debe usar un diseño de cuadro de diálogo de una columna." border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a>Hacer: Usar un diseño de cuadro de diálogo de una columna

Dado que los cuadros de diálogo están en el centro de la fase de reunión, la finalización de tareas debe ser rápida y sencilla para evitar la frustración del usuario.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Ejemplo que muestra que no debe saturar el espacio de una extensión de reunión." border="false":::

#### <a name="dont-clutter-the-space"></a>No: saturar el espacio

El contenido densa o demasiado estructurado puede ser molesto y abrumador, especialmente durante una reunión.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Ejemplo que muestra un diseño de pestaña de una columna." border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a>Hacer: Usar un diseño de pestaña de una columna

Dada la naturaleza estrecha de la pestaña en la reunión, se recomienda encarecidamente mostrar el contenido en una sola columna.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Ejemplo que muestra una pestaña con varias columnas." border="false":::

#### <a name="dont-use-multiple-columns"></a>No: usar varias columnas

Debido al espacio limitado de la pestaña en la reunión, no se recomiendan diseños con más de una columna.

   :::column-end:::
:::row-end:::

### <a name="controls"></a>Controles

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Ejemplo que muestra cómo alinear correctamente los controles principales." border="false":::

#### <a name="do-right-align-the-primary-action"></a>Hacer: alinear a la derecha la acción principal

Se recomienda colocar la acción más intensa visualmente en la ubicación más derecha.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Ejemplo que muestra cómo no debe dejar alineados los controles principales." border="false":::

#### <a name="dont-left-or-center-align-actions"></a>No: acciones de alineación izquierda o central

Esto se desvía del patrón de Teams estándar para la colocación de controles en un cuadro de diálogo y puede conflicto con un cuadro de diálogo detrás del superior.

   :::column-end:::
:::row-end:::

### <a name="scroll"></a>Scroll

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Ejemplo que muestra el desplazamiento vertical en una pestaña en reunión." border="false":::

#### <a name="do-scroll-vertically"></a>Hacer: desplazarse verticalmente

Los usuarios esperan desplazamiento vertical en Teams (y en otros lugares).

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Ejemplo que muestra el desplazamiento horizontal en una pestaña en la reunión." border="false":::

#### <a name="dont-scroll-horizontally"></a>No: desplazarse horizontalmente

El desplazamiento horizontal no es un comportamiento esperado en Teams. Otros lienzos del entorno de reunión se desplazan verticalmente.

   :::column-end:::
:::row-end:::

### <a name="workflows"></a>Flujos de trabajo

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Ejemplo que muestra un escenario complejo en una pestaña de reunión." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a>Hacer: escenarios complejos de Surface en la pestaña en reunión

Si la aplicación incluye varias tareas, recomendamos encarecidamente usar una pestaña en la reunión con un diseño de una sola columna.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Ejemplo que muestra escenarios complejos en un cuadro de diálogo en la reunión." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a>Don't: Hacer complejos los cuadros de diálogo en la reunión

Los cuadros de diálogo en reunión están diseñados para interacciones breves.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Creación de temas

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Ejemplo que muestra una extensión de reunión con el tema oscuro." border="false":::

#### <a name="do-use-teams-color-tokens"></a>Do: Use Teams tokens de color

Teams reuniones están optimizadas para el modo oscuro para ayudar a reducir el ruido visual y cognitivo para que los usuarios puedan centrarse en la discusión y el contenido compartido. Obtenga información sobre <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">el uso de tokens de color (Fluent UI)</a>.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Ejemplo que muestra una extensión de reunión con un tema predeterminado (claro)." border="false":::

#### <a name="dont-hard-code-hex-values"></a>No: valores hexadecimales de código duro

Si no usas tokens Teams de color, tus diseños serán menos escalables y tendrán más tiempo para administrar.

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>Navegación

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Ejemplo que muestra una extensión de reunión con un botón Atrás." border="false":::

#### <a name="do-have-a-back-button"></a>Hacer: Tener un botón atrás

Si tiene más de una capa de navegación en una pestaña de reunión, los usuarios deben poder volver a sus vistas anteriores.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Ejemplo que muestra una extensión de reunión con dos botones de descarte." border="false":::

#### <a name="dont-include-another-dismiss-button"></a>No: incluir otro botón descartar

Proporcionar una opción para cerrar el contenido de la pestaña en la reunión puede causar problemas, ya que ya hay un botón en el encabezado para descartar la propia pestaña en la reunión.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Ejemplo que muestra modales (o módulos de tareas) dentro de una pestaña en la reunión." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a>Precaución: evite los modales dentro de la pestaña en la reunión

Los modales (también conocidos como módulos de tareas) en la pestaña ya estrecha en la reunión podrían ajustar y oscurecer el contenido.

   :::column-end:::
:::row-end:::

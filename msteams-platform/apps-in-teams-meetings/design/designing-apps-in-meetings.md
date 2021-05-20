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
# <a name="designing-your-microsoft-teams-meeting-extension"></a>Diseño de la extensión de la reunión de Microsoft Teams

Puede crear aplicaciones para que las reuniones sean más productivas. Por ejemplo, pida a las personas que completen una encuesta durante una llamada o envíen un recordatorio rápido que no interrumpa el flujo de la reunión.

## <a name="microsoft-teams-ui-kit"></a>Kit de UI de Microsoft Teams

Puede encontrar directrices de diseño más completas, incluidos los elementos que puede capturar y modificar según sea necesario, en el Kit de interfaz de usuario de Microsoft Teams.

> [!div class="nextstepaction"]
> [Obtener el Kit de UI de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>Añadir una extensión de reunión

Puede agregar una extensión de reunión antes y durante las reuniones. También puede agregar una aplicación para una reunión específica directamente desde la tienda Teams (AppSource).

### <a name="add-before-a-meeting"></a>Añadir antes de una reunión

En los detalles de la reunión, seleccione **Agregar una pestaña +** para abrir el menú desplegable de la aplicación y buscar aplicaciones optimizadas para reuniones.

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de reunión antes de una reunión." border="false":::

### <a name="add-during-a-meeting"></a>Añadir durante una reunión

En una reunión, selecciona **Más** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **agregar una aplicación** y elige la aplicación que quieras.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de reunión durante una reunión." border="false":::

## <a name="before-a-meeting"></a>Antes de una reunión

Antes de la reunión, puede agregar contenido en la pestaña. En el ejemplo siguiente se muestra un borrador de pregunta de encuesta que las personas responderán durante la llamada.

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="En el ejemplo se muestra cómo app content en los detalles de la reunión antes de una llamada." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>Anatomía: pestaña Reunión (antes y después de las reuniones)

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="El ejemplo muestra la anatomía estructural de una pestaña de reunión antes y después de una reunión." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Nombre de la pestaña**: Etiqueta de navegación para la pestaña.|
|2|**Desbordamiento de tabulación:** abre acciones de tabulación, como cambiar el nombre y quitar.|
|3|**iframe**: muestra el contenido de la aplicación.|

### <a name="designing-with-ui-templates"></a>Diseño con plantillas de interfaz de usuario

Utilice una de las siguientes plantillas de interfaz de usuario Teams para ayudar a diseñar la pestaña de reunión:

* [Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato escaneable y permitir a los usuarios realizar acciones en una lista completa o en elementos individuales.
* [Tablero de tareas](../../concepts/design/design-teams-app-ui-templates.md#task-board): Un tablero de tareas, a veces llamado tablero kanban o carriles de natación, es una colección de tarjetas que se utilizan a menudo para rastrear el estado de los artículos de trabajo o boletos.
* [Panel](../../concepts/design/design-teams-app-ui-templates.md#dashboard): Un panel es un lienzo que contiene varias tarjetas que proporcionan una visión general de los datos o el contenido.
* [Formulario](../../concepts/design/design-teams-app-ui-templates.md#form): Los formularios son para recopilar, validar y enviar la entrada del usuario de forma estructurada.
* [Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacía se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.
* [Navegador izquierdo](../../concepts/design/design-teams-app-ui-templates.md#left-nav): La plantilla de navegación izquierda puede ayudar si la pestaña requiere un poco de navegación. En general, debe mantener la navegación de la pestaña al mínimo.

## <a name="use-an-in-meeting-tab"></a>Utilice una pestaña en la reunión

La pestaña en la reunión es un lienzo para aumentar la colaboración durante las reuniones. Los asistentes pueden ver e interactuar con el contenido de la aplicación en un espacio dedicado fuera de la etapa de reunión a través de vistas compartidas o basadas en roles.

### <a name="use-cases"></a>Casos de uso

La gente podría usar la pestaña en la reunión para:

* Proporcione comentarios detallados. Por ejemplo, evalúe a un candidato de trabajo.
* Cree una encuesta, encuesta o elemento de tarea para los participantes de la reunión.
* Mostrar notas relevantes para la reunión. Por ejemplo, información sobre un cliente potencial de ventas.

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="En el ejemplo se muestra cómo puede presentar contenido de sondeo en una pestaña de reunión." border="false":::

### <a name="anatomy-in-meeting-tab"></a>Anatomía: pestaña en la reunión

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="El ejemplo muestra la anatomía estructural de una pestaña en la reunión." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Icono de aplicación (seleccionado):** logotipo de aplicación transparente de 16 píxeles.|
|2|**Nombre de la aplicación**|
|3|**Encabezado**: incluye el nombre de la aplicación.|
|4 |**Botón Cerrar**: Descarta la pestaña. Utilice siempre el icono de cierre superior derecha en lugar de una acción en el pie de página.|
|5 |**Barra de notificaciones:** las alertas de error se muestran directamente debajo del encabezado y empujan el contenido de iframe hacia abajo en 20 píxeles.|
|6 |**iframe**: muestra el contenido de la aplicación.|

### <a name="spacing"></a>Spacing

Optimice su pestaña en la reunión para ajustar de borde a borde dentro del área de iframe de 280 píxeles de ancho. Hay 20 píxeles de relleno en los lados izquierdo y derecho del iframe y entre el encabezado de la pestaña. El iframe está lleno de sangrado en la parte inferior de la pestaña.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="En el ejemplo se muestran las dimensiones de espaciado de tabulación en la reunión." border="false":::

### <a name="scrolling"></a>desplazamiento

El contenido de Iframe debe desplazarse verticalmente. Solo puedes ver el contenido al que te has desplazado (nada por encima o por debajo). La barra de desplazamiento forma parte del contenido de iframe.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="En el ejemplo se muestra cómo se desplaza la pestaña en la reunión." border="false":::

### <a name="navigation"></a>Navegación

Para escenarios con capas de navegación o contenido pesado, se recomienda permitir a los usuarios navegar a una capa secundaria. Los usuarios deben poder volver a la capa anterior.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="El ejemplo muestra la navegación en la reunión." border="false":::

## <a name="use-an-in-meeting-dialog"></a>Utilice un cuadro de diálogo en la reunión

Los cuadros de diálogo en la reunión se muestran en la fase de Teams reunión. Requieren la atención, confirmación o interacción de un usuario, pero son sutiles y no interrumpen la reunión. Debe usarlos con moderación y para escenarios que estén orientados a la luz y a las tareas.

### <a name="use-cases"></a>Casos de uso

Los cuadros de diálogo en la reunión son activados por un usuario (como el organizador de la reunión) que podría querer que los participantes:

* Proporcionar breves comentarios
* Hacer una encuesta o encuesta corta
* Presentar aprobaciones
* Recibir recordatorios

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="En el ejemplo se muestra cómo puede utilizar un cuadro de diálogo en la reunión." border="false":::

### <a name="anatomy-in-meeting-dialog"></a>Anatomía: Diálogo en la reunión

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="El ejemplo muestra la anatomía estructural de un cuadro de diálogo en la reunión." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Encabezado:** incluye icono de aplicación, nombre, cadena de acción e icono de cierre.|
|2|**iframe**: muestra el contenido de la aplicación.|

### <a name="anatomy-in-meeting-dialog-header"></a>Anatomía: encabezado del cuadro de diálogo en la reunión

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de un encabezado de cuadro de diálogo en la reunión." border="false":::

Hay dos variantes de encabezado. Cuando sea posible, utilice la variante con el avatar para reforzar que el diálogo proviene de una persona.

|Contador|Descripción|
|----------|-----------|
|1|**Avatar**: Persona que inicia el diálogo en la reunión.|
|2|**Icono de aplicación**|
|3|**Nombre de la aplicación**|
|4 |**Botón Cerrar**: descarta el cuadro de diálogo.|
|5 |**Cadena de acción:** normalmente describe quién inició el cuadro de diálogo.|

### <a name="responsive-behavior"></a>Comportamiento dinámico

Los cuadros de diálogo en la reunión pueden variar en tamaño para tener en cuenta diferentes escenarios. Asegúrese de mantener el relleno y los tamaños de componentes.

* **Ancho**: puede especificar el ancho del iframe del cuadro de diálogo en cualquier lugar dentro del rango de tamaño admitido.
* **Altura**: Puede especificar la altura del iframe del cuadro de diálogo en cualquier lugar dentro del rango de tamaño admitido. También puede permitir que los usuarios se despplacen verticalmente si el contenido de la aplicación supera la altura máxima.

Para implementar, especifique el ancho y la altura mediante la [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) clave.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="En el ejemplo se muestra el cuadro de diálogo en la reunión. Ancho: Min--280 píxeles (iframe de 248 píxeles). Max-- 460 píxeles (iframe de 428 píxeles). Altura: 300 píxeles (iframe)." border="false":::

## <a name="after-a-meeting"></a>Después de una reunión

Puede volver a una reunión una vez finalizada y ver el contenido de la aplicación. En este ejemplo, el organizador de la reunión puede examinar los resultados de la encuesta en la pestaña **Contoso.** (Nota: Desde un punto de vista de diseño, no hay diferencia entre una experiencia de pestaña anterior y posterior a la reunión.)

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="La ilustración de ejemplo muestra una pestaña posterior a la reunión." border="false":::

## <a name="best-practices"></a>Procedimientos recomendados

Utilice estas recomendaciones para crear una experiencia de aplicación de calidad.

### <a name="interactions"></a>Interacciones

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Ejemplo que muestra cómo limitar el número de interacciones." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a>Hacer: Limitar el número de interacciones

Para los cuadros de diálogo en la reunión, elimine contenido innecesario que no ayude a los usuarios a lograr algo rápidamente.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Ejemplo que muestra cómo no introducir elementos innecesarios." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a>No: Introducir elementos innecesarios

Un único cuadro de diálogo en la reunión con varias interacciones puede distraer de la llamada.

   :::column-end:::
:::row-end:::

### <a name="layout"></a>Diseño

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Ejemplo que muestra cómo debe usar un diseño de cuadro de diálogo de una sola columna." border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a>Hacer: Utilice un diseño de cuadro de diálogo de una sola columna

Dado que los cuadros de diálogo están en el centro de la fase de reunión, la finalización de la tarea debe ser rápida y sencilla para evitar la frustración del usuario.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Ejemplo que muestra que no debe saturar el espacio de una extensión de reunión." border="false":::

#### <a name="dont-clutter-the-space"></a>No: Abarrotar el espacio

El contenido denso o excesivamente estructurado puede distraer y ser abrumador, especialmente durante una reunión.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Ejemplo que muestra un diseño de tabulación de una sola columna." border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a>Hacer: Utilice un diseño de tabulación de una sola columna

Dada la naturaleza estrecha de la pestaña en la reunión, se recomienda encarecidamente mostrar el contenido en una sola columna.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Ejemplo que muestra una pestaña con varias columnas." border="false":::

#### <a name="dont-use-multiple-columns"></a>No: Usa varias columnas

Debido al espacio limitado de la pestaña en la reunión, no se recomiendan diseños con más de una columna.

   :::column-end:::
:::row-end:::

### <a name="controls"></a>Controles

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Ejemplo que muestra cómo alinear correctamente los controles primarios." border="false":::

#### <a name="do-right-align-the-primary-action"></a>Hacer: Alinee bien la acción principal

Recomendamos colocar la acción más pesada visualmente en la ubicación más correcta.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Ejemplo que muestra cómo no debe dejar alinear los controles primarios." border="false":::

#### <a name="dont-left-or-center-align-actions"></a>No: Las acciones de alineación izquierda o central

Esto se desvía del patrón de Teams estándar para la colocación del control en un cuadro de diálogo y puede entrar en conflicto con un cuadro de diálogo detrás del superior.

   :::column-end:::
:::row-end:::

### <a name="scroll"></a>Scroll

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Ejemplo que muestra el desplazamiento vertical en una pestaña de reunión." border="false":::

#### <a name="do-scroll-vertically"></a>Hacer: Desplázate verticalmente

Los usuarios esperan desplazamiento vertical en Teams (y en otros lugares).

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Ejemplo que muestra el desplazamiento horizontal en una pestaña de reunión." border="false":::

#### <a name="dont-scroll-horizontally"></a>No: Desplázate horizontalmente

El desplazamiento horizontal no es un comportamiento esperado en Teams. Otros lienzos del entorno de reuniones se desplazan verticalmente.

   :::column-end:::
:::row-end:::

### <a name="workflows"></a>Flujos de trabajo

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Ejemplo que muestra el escenario complejo en una pestaña de reunión." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a>Hacer: Escenarios complejos de Surface en la pestaña en la reunión

Si la aplicación incluye varias tareas, se recomienda encarecidamente usar una pestaña en la reunión con un diseño de una sola columna.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Ejemplo que muestra escenarios complejos en un cuadro de diálogo en la reunión." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a>No: Hacer que los diálogos en la reunión sean complejos

Los cuadros de diálogo en la reunión están destinados a interacciones breves.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Creación de temas

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Ejemplo que muestra una extensión de reunión con el tema oscuro." border="false":::

#### <a name="do-use-teams-color-tokens"></a>Hacer: Use tokens de color Teams

Teams reuniones están optimizadas para el modo oscuro para ayudar a reducir el ruido visual y cognitivo para que los usuarios puedan centrarse en la discusión y el contenido compartido. Obtenga información sobre el uso de <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">tokens de color (FLUENT UI).</a>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Ejemplo que muestra una extensión de reunión con un tema predeterminado (luz)." border="false":::

#### <a name="dont-hard-code-hex-values"></a>No: Valores hexagonal de código duro

Si no usa tokens de color Teams, sus diseños serán menos escalables y tardarán más tiempo en administrarse.

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>Navegación

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Ejemplo que muestra una extensión de reunión con un botón atrás." border="false":::

#### <a name="do-have-a-back-button"></a>Hacer: Tener un botón atrás

Si tiene más de una capa de navegación en una pestaña en la reunión, los usuarios deben poder volver a sus vistas anteriores.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Ejemplo que muestra una extensión de reunión con dos botones de descarte." border="false":::

#### <a name="dont-include-another-dismiss-button"></a>No: Incluya otro botón de descarte

Proporcionar una opción para cerrar el contenido de la pestaña en la reunión puede causar problemas, ya que ya hay un botón en el encabezado para descartar la propia pestaña en la reunión.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Ejemplo que muestra modales (o módulos de tareas) dentro de una pestaña en la reunión." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a>Precaución: Evite modales dentro de la pestaña en la reunión

Modals (también conocidos como módulos de tareas) en la pestaña ya estrecha en la reunión pueden encapsular y oscurecer el contenido.

   :::column-end:::
:::row-end:::

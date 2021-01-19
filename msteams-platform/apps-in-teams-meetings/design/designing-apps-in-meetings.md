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
# <a name="designing-your-microsoft-teams-meeting-extension"></a>Diseño de la extensión de reunión de Microsoft Teams

Puede crear aplicaciones para que las reuniones sean más productivas. Por ejemplo, pida a los usuarios que completen una encuesta durante una llamada o que envíen un aviso rápido que no interrumpa el flujo de la reunión.

## <a name="microsoft-teams-ui-kit"></a>Kit de interfaz de usuario de Microsoft Teams

Puede encontrar instrucciones de diseño más completas, incluidos los elementos que puede tomar y modificar según sea necesario, en el Kit de interfaz de usuario de Microsoft Teams.

> [!div class="nextstepaction"]
> [Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>Agregar una extensión de reunión

Puede agregar una extensión de reunión antes y durante las reuniones. También puede agregar una aplicación para una reunión específica directamente desde la tienda de Teams (AppSource).

### <a name="add-before-a-meeting"></a>Agregar antes de una reunión

En los detalles de la reunión, seleccione **Agregar una pestaña + para** abrir el control desplegable de la aplicación y buscar aplicaciones optimizadas para reuniones.

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de reunión antes de una reunión." border="false":::

### <a name="add-during-a-meeting"></a>Agregar durante una reunión

En una reunión, seleccione **Más** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **agregar una aplicación** y elija la aplicación que desee.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de reunión durante una reunión." border="false":::

## <a name="before-a-meeting"></a>Antes de una reunión

Antes de la reunión, puede agregar contenido en la pestaña. En el siguiente ejemplo se muestra un borrador de pregunta de encuesta que los usuarios responderán durante la llamada.

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="En el ejemplo se muestra cómo usar el contenido de la aplicación en los detalles de la reunión antes de una llamada." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>Anatomía: pestaña Reunión (antes y después de las reuniones)

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de una pestaña de reunión antes y después de una reunión." border="false":::

|Counter|Descripción|
|----------|-----------|
|1|**Nombre de la pestaña:** etiqueta de navegación de la pestaña.|
|2 |**Desbordamiento de pestaña:** abre acciones de pestaña, como cambiar el nombre y quitar.|
|3|**iframe:** muestra el contenido de la aplicación.|

### <a name="designing-with-ui-templates"></a>Diseño con plantillas de interfaz de usuario

Use una de las siguientes plantillas de interfaz de usuario de Teams para ayudar a diseñar la pestaña de reunión:

* [Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato digitalizado y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.
* [Panel de](../../concepts/design/design-teams-app-ui-templates.md#task-board)tareas: un panel de tareas, a veces denominado tablero de kanban o pistas de nado, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o vales.
* [Panel:](../../concepts/design/design-teams-app-ui-templates.md#dashboard)un panel es un lienzo que contiene varias tarjetas que proporcionan información general sobre datos o contenido.
* [Formulario:](../../concepts/design/design-teams-app-ui-templates.md#form)los formularios son para recopilar, validar y enviar entradas de usuario de forma estructurada.
* [Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacía se puede usar para muchos escenarios, incluido el inicio de sesión, experiencias de primera ejecución, mensajes de error y mucho más.
* [Navegación izquierda:](../../concepts/design/design-teams-app-ui-templates.md#left-nav)la plantilla de navegación izquierda puede ayudar si la pestaña requiere cierta navegación. En general, debes mantener la navegación mediante tabulación al mínimo.

## <a name="use-an-in-meeting-tab"></a>Usar una pestaña en la reunión

La pestaña en la reunión es un lienzo para aumentar la colaboración durante las reuniones. Los asistentes pueden ver e interactuar con el contenido de la aplicación en un espacio dedicado fuera de la fase de reunión a través de vistas compartidas o basadas en roles.

### <a name="use-cases"></a>Casos de uso

Los usuarios pueden usar la pestaña en la reunión para:

* Proporcionar comentarios detallados (por ejemplo, evaluar un candidato de trabajo)
* Crear rápidamente un sondeo, una encuesta o un elemento de tarea para los participantes de la reunión
* Mostrar notas relevantes para la reunión (por ejemplo, información sobre un responsable de ventas)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="En el ejemplo se muestra cómo presentar contenido de sondeo en una pestaña de reunión." border="false":::

### <a name="anatomy-in-meeting-tab"></a>Anatomía: pestaña En la reunión

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de una pestaña en reunión." border="false":::

|Counter|Descripción|
|----------|-----------|
|1|**Icono de aplicación (seleccionado):** logotipo de aplicación transparente de 16 píxeles.|
|2 |**Nombre de la aplicación**|
|3|**Encabezado:** incluye el nombre de la aplicación.|
|4 |**Botón Cerrar:** descarta la pestaña. Use siempre el icono de cierre superior derecho en lugar de una acción en el pie de página.|
|5 |**Barra de notificación:** las alertas de error se muestran directamente debajo del encabezado e insertan el contenido del iframe hacia abajo 20 píxeles.|
|6 |**iframe:** muestra el contenido de la aplicación.|

### <a name="spacing"></a>Spacing

Optimiza la pestaña de la reunión para que se ajuste de un extremo a otro dentro del área de iframe de 280 píxeles. Hay 20 píxeles de espaciado interno en los lados izquierdo y derecho del iframe y entre el encabezado de pestaña. El iframe está a sangre completa en la parte inferior de la pestaña.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="En el ejemplo se muestran las dimensiones de espaciado de tabulación en reuniones." border="false":::

### <a name="scrolling"></a>Desplazamiento

El contenido del Iframe debe desplazarse verticalmente. Solo puede ver el contenido al que se desplazó (nada por encima o por debajo). La barra de desplazamiento forma parte del contenido del iframe.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="En el ejemplo se muestra cómo se desplaza la pestaña en la reunión." border="false":::

### <a name="navigation"></a>Navegación

Para escenarios con capas de navegación o contenido intenso, se recomienda permitir a los usuarios navegar a una capa secundaria. Los usuarios deben poder volver a la capa anterior.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="En el ejemplo se muestra la navegación en la reunión." border="false":::

## <a name="use-an-in-meeting-dialog"></a>Usar un cuadro de diálogo en la reunión

Los cuadros de diálogo dentro de la reunión se muestran en la fase de reunión de Teams. Requieren la atención, confirmación o interacción de un usuario, pero son sutiles y no interrumpen la reunión. Debes usarlas con moderación y para escenarios orientados a tareas y ligeras.

### <a name="use-cases"></a>Casos de uso

Los cuadros de diálogo dentro de la reunión los desencadena un usuario (como el organizador de la reunión) que puede desear que los participantes:

* Proporcionar comentarios breves
* Realizar una encuesta o sondeo breve
* Enviar aprobaciones
* Recibir recordatorios

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="En el ejemplo se muestra cómo usar un cuadro de diálogo en la reunión." border="false":::

### <a name="anatomy-in-meeting-dialog"></a>Anatomía: cuadro de diálogo en la reunión

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de un cuadro de diálogo en reunión." border="false":::

|Counter|Descripción|
|----------|-----------|
|1|**Encabezado:** incluye el icono de la aplicación, el nombre, la cadena de acción y el icono de cierre.|
|2 |**iframe:** muestra el contenido de la aplicación.|

### <a name="anatomy-in-meeting-dialog-header"></a>Anatomía: encabezado del cuadro de diálogo En la reunión

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de un encabezado de cuadro de diálogo en reunión." border="false":::

Hay dos variantes de encabezado. Cuando sea posible, usa la variante con el avatar para reforzar que el cuadro de diálogo viene de una persona.

|Counter|Descripción|
|----------|-----------|
|1|**Avatar:** persona que inicia el cuadro de diálogo en la reunión.|
|2 |**Icono de aplicación**|
|3|**Nombre de la aplicación**|
|4 |**Botón Cerrar:** descarta el cuadro de diálogo.|
|5 |**Cadena de acción:** normalmente describe quién inició el cuadro de diálogo.|

### <a name="responsive-behavior"></a>Comportamiento dinámico

Los cuadros de diálogo en reunión pueden variar en tamaño para tener en cuenta diferentes escenarios. Asegúrese de mantener el espaciado interno y los tamaños de los componentes.

* **Ancho:** el ancho del iframe es un valor absoluto dentro del intervalo especificado.
* **Alto:** el alto del cuadro de diálogo viene determinado por el contenido del iframe. El desplazamiento vertical toma el control del contenido que supera el alto máximo.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="En el ejemplo se muestra el cuadro de diálogo en la reunión. Ancho: mínimo: 280 píxeles (iframe de 248 píxeles). Máximo: 460 píxeles (iframe de 428 píxeles). Alto: 300 píxeles (iframe)." border="false":::

## <a name="after-a-meeting"></a>Después de una reunión

Puedes volver a una reunión después de que finalice y ver el contenido de la aplicación. En este ejemplo, el organizador de la reunión puede ver los resultados del sondeo en la pestaña **Contoso.** (Nota: Desde el punto de vista del diseño, no hay ninguna diferencia entre la experiencia de pestaña previa y posterior a la reunión).

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="En el ejemplo se muestra una pestaña posterior a la reunión." border="false":::

## <a name="best-practices"></a>Procedimientos recomendados

### <a name="interactions"></a>Interacciones

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Ejemplo que muestra cómo limitar el número de interacciones." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a>Hacer: Limitar el número de interacciones

Para los cuadros de diálogo en la reunión, quite el contenido innecesario que no ayude a los usuarios a lograr algo rápidamente.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Ejemplo que muestra cómo no introducir elementos innecesarios." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a>No: introducir elementos innecesarios

Un solo cuadro de diálogo en la reunión con varias interacciones puede distraer la llamada.

   :::column-end:::
:::row-end:::

### <a name="layout"></a>Diseño

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Ejemplo que muestra cómo debe usar un diseño de cuadro de diálogo de una sola columna." border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a>Hacer: usar un diseño de cuadro de diálogo de una sola columna

Dado que los cuadros de diálogo están en el centro de la fase de reunión, la finalización de tareas debe ser rápida y sencilla para evitar la frustración del usuario.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Ejemplo que muestra que no debe abarrote el espacio de una extensión de reunión." border="false":::

#### <a name="dont-clutter-the-space"></a>No: abarrote el espacio

El contenido densa o demasiado estructurado puede distraer y agobiar, especialmente durante una reunión.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Ejemplo que muestra un diseño de pestaña de una sola columna." border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a>Hacer: usar un diseño de pestaña de una sola columna

Dada la naturaleza estrecha de la pestaña en la reunión, recomendamos encarecidamente mostrar el contenido en una sola columna.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Ejemplo que muestra una pestaña con varias columnas." border="false":::

#### <a name="dont-use-multiple-columns"></a>No: Usar varias columnas

Debido al espacio limitado de la pestaña en la reunión, no se recomiendan los diseños con más de una columna.

   :::column-end:::
:::row-end:::

### <a name="controls"></a>Controles

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Ejemplo que muestra cómo alinear a la derecha los controles principales." border="false":::

#### <a name="do-right-align-the-primary-action"></a>Hacer: alinear a la derecha la acción principal

Se recomienda colocar la acción más intensa visualmente en la ubicación más a la derecha.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Ejemplo que muestra cómo no debes alinear a la izquierda los controles principales." border="false":::

#### <a name="dont-left-or-center-align-actions"></a>No: acciones de alineación a la izquierda o al centro

Esto se desvía del patrón estándar de Teams para la colocación de controles en un cuadro de diálogo y puede conflicto con un cuadro de diálogo detrás del superior.

   :::column-end:::
:::row-end:::

### <a name="scroll"></a>Scroll

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Ejemplo que muestra el desplazamiento vertical en una pestaña de reunión." border="false":::

#### <a name="do-scroll-vertically"></a>Hacer: desplazarse verticalmente

Los usuarios esperan un desplazamiento vertical en Teams (y en otros lugares).

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Ejemplo que muestra el desplazamiento horizontal en una pestaña de reunión." border="false":::

#### <a name="dont-scroll-horizontally"></a>No: desplazarse horizontalmente

El desplazamiento horizontal no es un comportamiento esperado en Teams. Otros lienzos del entorno de reuniones se desplazan verticalmente.

   :::column-end:::
:::row-end:::

### <a name="workflows"></a>Flujos de trabajo

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Ejemplo que muestra un escenario complejo en una pestaña de reunión." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a>Hacer: Surface complex scenarios in the in-meeting tab

Si la aplicación incluye varias tareas, te recomendamos encarecidamente usar una pestaña de reunión con un diseño de una sola columna.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Ejemplo que muestra escenarios complejos en un cuadro de diálogo en la reunión." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a>No: hacer complejos los cuadros de diálogo en la reunión

Los cuadros de diálogo dentro de la reunión están diseñados para interacciones breves.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Creación de temas

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Ejemplo que muestra una extensión de reunión con el tema oscuro." border="false":::

#### <a name="do-use-teams-color-tokens"></a>Usar tokens de color de Teams

Las reuniones de Teams están optimizadas para el modo oscuro para ayudar a reducir el ruido visual y cognitiva para que los usuarios puedan centrarse en la discusión y el contenido compartido. Obtenga información sobre el <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">uso de tokens de color (ui. fluent).</a>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Ejemplo que muestra una extensión de reunión con un tema predeterminado (claro)." border="false":::

#### <a name="dont-hard-code-hex-values"></a>No: valores hexadecimales de código duro

Si no usa tokens de color de Teams, los diseños serán menos escalables y tardarán más tiempo en administrarse.

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>Navegación

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Ejemplo que muestra una extensión de reunión con un botón Atrás." border="false":::

#### <a name="do-have-a-back-button"></a>Do: Have a Back button

Si tiene más de un nivel de navegación en una pestaña de reunión, los usuarios deben poder volver a sus vistas anteriores.

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
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Ejemplo que muestra modales (o módulos de tareas) en una pestaña de reunión." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a>Precaución: evite los modales en la pestaña en la reunión

Las modalidades (también conocidas como módulos de tareas) en la pestaña de reunión ya estrecha podrían encapsular y ocultar el contenido.

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a>Validar el diseño

Si tienes previsto publicar la aplicación en AppSource, debes comprender los problemas de diseño que normalmente provocan errores en las aplicaciones durante el envío.

> [!div class="nextstepaction"]
> [Comprobar las directrices de validación de diseño](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)

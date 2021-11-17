---
title: Diseño de la extensión de reunión
author: heath-hamilton
description: Obtén información sobre cómo diseñar aplicaciones en reuniones Teams y obtener el kit de interfaz de usuario de Microsoft Teams, la pestaña en la reunión y los casos de uso, el comportamiento dinámico y la fase de reunión compartida, y el tema y la navegación.
ms.author: lajanuar
ms.localizationpriority: medium
ms.topic: conceptual
keywords: Fase de reunión compartida de comportamiento dinámico de plantilla de kit de interfaz de usuario en la reunión
ms.openlocfilehash: d66dc257ae26a17519468cf11d1d0b5593ba9d33
ms.sourcegitcommit: 3dd69ae18bca8dd2e0666d09746a4012cd8c8e42
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2021
ms.locfileid: "61051199"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a>Diseño de la extensión Microsoft Teams reunión

Puedes crear aplicaciones para que las reuniones sean más productivas. Por ejemplo, pida a los usuarios que completen una encuesta durante una reunión o que envíen un aviso rápido que no interrumpa el flujo de la reunión.

## <a name="microsoft-teams-ui-kit"></a>Kit de UI de Microsoft Teams

Puedes encontrar instrucciones de diseño más completas, incluidos los elementos que puedes agarrar y modificar según sea necesario, en el kit de interfaz Microsoft Teams usuario.

> [!div class="nextstepaction"]
> [Obtener el Kit de UI de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>Agregar una extensión de reunión

Los usuarios pueden agregar una extensión de reunión antes y durante las reuniones. También pueden agregar una aplicación para una reunión específica directamente desde Teams tienda.

### <a name="add-before-a-meeting"></a>Agregar antes de una reunión

En los detalles de la reunión, los usuarios pueden seleccionar **Agregar una** pestaña + para abrir el control desplegable de la aplicación y buscar aplicaciones optimizadas para reuniones.

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de reunión antes de una reunión." border="false":::

### <a name="add-during-a-meeting"></a>Agregar durante una reunión

#### <a name="mobile"></a>Móvil

Una vez agregada la aplicación (por ejemplo, en el escritorio), los usuarios pueden acceder a la aplicación en una reunión seleccionando **Más** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: .

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-add-during-meeting.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de reunión durante una reunión en el móvil." border="false":::

#### <a name="desktop"></a>Escritorio

En una reunión, los usuarios pueden **seleccionar Más** agregar :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **una aplicación** y seleccionar la aplicación que desean.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de reunión durante una reunión." border="false":::

## <a name="before-a-meeting"></a>Antes de una reunión

Antes de una reunión, la aplicación está disponible para los usuarios en una pestaña. En el siguiente ejemplo se muestra un borrador de pregunta de encuesta que los usuarios responderán durante la reunión.

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="En el ejemplo se muestra cómo usar el contenido de la aplicación en los detalles de la reunión antes de una llamada." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>Anatomía: pestaña Reunión (antes y después de las reuniones)

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de una pestaña de reunión antes y después de una reunión." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Nombre de la pestaña**: etiqueta de navegación para la pestaña.|
|2|**Desbordamiento de pestaña**: abre acciones de pestaña, como cambiar el nombre y quitar.|
|3|**iframe**: muestra el contenido de la aplicación.|

### <a name="design-with-ui-templates"></a>Diseño con plantillas de interfaz de usuario

Usa una de las siguientes plantillas Teams interfaz de usuario para ayudar a diseñar la pestaña de reunión:

* [Lista](../../concepts/design/design-teams-app-ui-templates.md#list): Las listas pueden mostrar elementos relacionados en un formato digitalizado y permitir a los usuarios realizar acciones en una lista completa o en elementos individuales.
* [Panel de tareas](../../concepts/design/design-teams-app-ui-templates.md#task-board): un panel de tareas, a veces denominado panel kanban o carril, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o los vales.
* [Panel](../../concepts/design/design-teams-app-ui-templates.md#dashboard): un panel es un lienzo que contiene varias tarjetas que proporcionan información general sobre los datos o el contenido.
* [Formulario](../../concepts/design/design-teams-app-ui-templates.md#form): Los formularios son para recopilar, validar y enviar el input del usuario de forma estructurada.
* [Estado vacío](../../concepts/design/design-teams-app-ui-templates.md#empty-state): La plantilla de estado vacío se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.
* [Navegación izquierda](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav): el componente de navegación izquierda puede ayudar si la pestaña requiere algo de navegación. En general, debe mantener la navegación al mínimo.

## <a name="use-an-in-meeting-tab"></a>Usar una pestaña en la reunión

La pestaña en la reunión es un lienzo para aumentar la colaboración durante las reuniones. Los asistentes pueden ver e interactuar con el contenido de la aplicación en un espacio dedicado fuera de la fase de reunión a través de vistas compartidas o basadas en roles.

### <a name="use-cases"></a>Casos de uso

Las personas pueden usar la pestaña en la reunión para:

* Proporcionar comentarios detallados. Por ejemplo, evalúe un candidato de trabajo.
* Cree un sondeo, una encuesta o un elemento de tarea para los participantes de la reunión.
* Mostrar notas relevantes para la reunión. Por ejemplo, información sobre un cliente potencial de ventas.

#### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-tab.png" alt-text="En el ejemplo se muestra cómo se puede presentar contenido de sondeo en una pestaña de reunión en el móvil." border="false":::

#### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="En el ejemplo se muestra cómo se puede presentar contenido de sondeo en una pestaña en la reunión." border="false":::

### <a name="anatomy-in-meeting-tab"></a>Anatomía: pestaña En la reunión

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de una pestaña en reunión." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Icono de aplicación (seleccionado):** logotipo de aplicación transparente de 16 píxeles.|
|2|**Nombre de la aplicación**|
|3|**Encabezado:** incluye el nombre de la aplicación.|
|4|**Botón Cerrar:** descarta la pestaña. Use siempre el icono de cierre superior derecho en lugar de una acción en el pie de página.|
|5|**Barra de notificaciones:** las alertas de error se muestran directamente debajo del encabezado y presionan el contenido del iframe hacia abajo en 20 píxeles.|
|6 |**iframe**: muestra el contenido de la aplicación.|

### <a name="spacing"></a>Spacing

Optimiza la pestaña en la reunión para que se ajuste de un extremo a otro dentro del área de iframe de 280 píxeles. Hay 20 píxeles de relleno en los lados izquierdo y derecho del iframe y entre el encabezado de pestaña. El iframe está sangrando hasta la parte inferior de la pestaña.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="En el ejemplo se muestran las dimensiones de espaciado de tabulación en la reunión." border="false":::

### <a name="scrolling"></a>Desplazamiento

Recuerde lo siguiente si permite el desplazamiento:

* El contenido del iframe solo debe desplazarse verticalmente.
* Los usuarios solo deben ver el contenido al que se han desplazado (nada por encima o por debajo). 
* La barra de desplazamiento forma parte del contenido de iframe.

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

### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-dialog.png" alt-text="En el ejemplo se muestra cómo se puede usar un cuadro de diálogo en la reunión en el móvil." border="false":::

### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="En el ejemplo se muestra cómo se puede usar un cuadro de diálogo en la reunión." border="false":::

### <a name="anatomy-in-meeting-dialog"></a>Anatomía: cuadro de diálogo en la reunión

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de un cuadro de diálogo en reunión." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Encabezado:** incluye el icono de la aplicación, el nombre, la cadena de acción y el icono cerrar.|
|2|**iframe**: muestra el contenido de la aplicación.|

### <a name="anatomy-in-meeting-dialog-header"></a>Anatomía: encabezado del cuadro de diálogo En la reunión

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de un encabezado de cuadro de diálogo en reunión." border="false":::

Hay dos variantes de encabezado. Cuando sea posible, usa la variante con el avatar para reforzar que el cuadro de diálogo viene de una persona.

|Contador|Descripción|
|----------|-----------|
|1|**Avatar:** persona que inicia el cuadro de diálogo en la reunión.|
|2|**Icono de aplicación**|
|3|**Nombre de la aplicación**|
|4|**Botón Cerrar:** descarta el cuadro de diálogo.|
|5|**Cadena de acción:** normalmente describe quién inició el cuadro de diálogo.|

### <a name="responsive-behavior-in-meeting-dialogs"></a>Comportamiento dinámico: cuadros de diálogo en la reunión

Los cuadros de diálogo en reunión pueden variar en tamaño para tener en cuenta diferentes escenarios. Asegúrese de mantener el relleno y los tamaños de los componentes.

* **Width:** puede especificar el ancho del iframe del cuadro de diálogo en cualquier lugar dentro del intervalo de tamaño admitido.
* **Alto:** puede especificar el alto del iframe del cuadro de diálogo en cualquier lugar dentro del intervalo de tamaño admitido. También puedes permitir que los usuarios se desplacen verticalmente si el contenido de la aplicación supera el alto máximo.

Para implementar, especifique el ancho y el alto con la [`externalResourceUrl`](~/apps-in-teams-meetings/API-references.md#notificationsignal-api) clave.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="En el ejemplo se muestra el cuadro de diálogo en la reunión. Ancho: Min-280 píxeles (248 píxeles iframe). Máximo: 460 píxeles (428 píxeles de iframe). Alto: 300 píxeles (iframe)." border="false":::

## <a name="use-the-shared-meeting-stage"></a>Usar la fase de reunión compartida

La fase de reunión compartida ayuda a los participantes a interactuar y colaborar con el contenido de la aplicación en tiempo real. Por ejemplo, los usuarios pueden centrar su reunión en editar un documento, hacer una lluvia de ideas con una pizarra o revisar un panel.

Las aplicaciones compartidas en la fase de reunión ocupan el mismo espacio que una pantalla compartida. La fase se vuelve a reorientar para todos los participantes de la reunión.

> [!NOTE]
> Todos los usuarios que se reúnen pueden ver la aplicación cuando se comparten desde el escritorio. Actualmente, los usuarios móviles no pueden compartir contenido de la aplicación en la fase de reunión.
 
### <a name="use-cases"></a>Casos de uso

La fase de reunión compartida tiene que ver con la colaboración y la participación. Estos son algunos escenarios de ejemplo que le ayudarán a empezar.

:::row:::
   :::column span="1":::

**Editar y revisar:** profundizar en los paneles y la planeación con todos los usuarios de la reunión.

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-edit-review.png" alt-text="En el ejemplo se muestra un panel que se está revisando en la fase de reunión compartida." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

**Pizarra:** dibujar e idear juntos en un lienzo compartido.

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-whiteboard.png" alt-text="En el ejemplo se muestra una pizarra en la fase de reunión compartida." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

**Cuestionario:** Pruebe los conocimientos y obtenga información con materiales interactivos.

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-quiz.png" alt-text="En el ejemplo se muestra un cuestionario en la fase de reunión compartida." border="false":::

   :::column-end:::
:::row-end:::

### <a name="anatomy-shared-meeting-stage"></a>Anatomía: fase de reunión compartida

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-anatomy.png" alt-text="La imagen muestra la anatomía de diseño de la fase de reunión compartida." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Icono de la** aplicación: el icono resaltado indica que la pestaña en la reunión de la aplicación está abierta.|
|2|**Botón Compartir a fase de reunión:** punto de entrada para compartir la aplicación a la fase de reunión. Muestra si configuras la aplicación para que use la fase de reunión compartida.|
|3|**iframe**: muestra el contenido de la aplicación.|
|4|**Botón Detener uso compartido:** deja de compartir la aplicación en la fase de reunión. Solo se muestra para el participante que inició el recurso compartido.|
|5|**Atribución del moderador:** muestra el nombre del participante que compartió la aplicación.|

### <a name="responsive-behavior-shared-meeting-stage"></a>Comportamiento dinámico: fase de reunión compartida

Las aplicaciones compartidas en la fase de reunión varían en tamaño según el estado de la reunión y el modo en que el usuario cambia el tamaño de la ventana. Mantenga el relleno y el diseño dinámico de la navegación y los controles tal como lo haría en un explorador.

* **Panel lateral:** un usuario puede tener el panel lateral abierto en cualquier momento durante una reunión para chatear, ver la lista o usar una aplicación (es decir, pestaña en la reunión). La fase reorganiza dinámicamente cuando el panel está abierto.
* **Cuadrícula de vídeo y audio:** la cuadrícula de vídeo y audio siempre está visible para mostrar a los participantes de la reunión. Cuando un usuario destaca o ancla a alguien en la reunión, esto aumenta el alto o el ancho de la cuadrícula de participantes en función de la orientación.

#### <a name="meeting-stage-without-side-panel"></a>Fase de reunión (sin panel lateral)

Cuando el panel lateral no está abierto, la fase de reunión es de 994 x 678 píxeles de forma predeterminada y puede tener un mínimo de 792 x 382 píxeles.

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-no-side-panel.png" alt-text="Imagen que muestra la capacidad de respuesta de la fase de reunión compartida con el panel lateral cerrado." border="false":::

#### <a name="meeting-stage-with-side-panel"></a>Fase de reunión (con panel lateral)

Cuando el panel lateral está abierto, la fase de reunión es de 918 x 540 píxeles de forma predeterminada y puede tener un mínimo de 472 x 382 píxeles.

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-with-side-panel.png" alt-text="Imagen que muestra la capacidad de respuesta de la fase de reunión compartida con el panel lateral abierto." border="false":::

## <a name="after-a-meeting"></a>Después de una reunión

Puedes volver a una reunión después de que finalice y ver el contenido de la aplicación. En este ejemplo, el organizador de la reunión puede ver los resultados del sondeo en la pestaña **Contoso.** (Nota: Desde el punto de vista del diseño, no hay ninguna diferencia entre la experiencia de tabulación anterior y posterior a la reunión).

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="La ilustración de ejemplo muestra una pestaña posterior a la reunión." border="false":::

## <a name="best-practices"></a>Procedimientos recomendados

Use estas recomendaciones para crear una experiencia de aplicación de calidad.

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

Un único cuadro de diálogo en la reunión con varias interacciones puede distraer de la reunión.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-do.png" alt-text="Ejemplo que muestra cómo crear un entorno centrado." border="false":::

#### <a name="do-create-a-focused-environment"></a>Hacer: Crear un entorno centrado

Se recomienda mantener la experiencia de la aplicación en el ámbito de solo la fase de reunión. Puede usar una pestaña en la reunión en el panel lateral como una vista secundaria privada para determinados escenarios.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-dont.png" alt-text="Ejemplo que muestra cómo no incluir superficies de competencia durante las reuniones." border="false":::

#### <a name="dont-include-competing-surfaces"></a>No: incluir superficies de competencia

La aplicación solo debe pedir a los usuarios que se centren en una sola superficie cada vez, ya sea que colabore en el escenario o responda a un cuadro de diálogo en la reunión. (Nota: No puedes mantener los cuadros de diálogo activados por otras aplicaciones mientras la aplicación está en el escenario). 

   :::column-end:::
:::row-end:::

### <a name="layout"></a>Diseño

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Ejemplo que muestra cómo debe usar un diseño de cuadro de diálogo de una columna." border="false":::

#### <a name="do-use-a-one-column-dialog"></a>Hacer: usar un cuadro de diálogo de una columna

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

#### <a name="do-use-a-one-column-tab"></a>Hacer: usar una pestaña de una columna

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

### <a name="scrolling"></a>Desplazamiento

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Ejemplo que muestra el desplazamiento vertical en una pestaña en reunión." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-do.png" alt-text="Ejemplo que muestra el desplazamiento vertical en la fase de reunión compartida." border="false":::

#### <a name="do-scroll-vertically"></a>Hacer: desplazarse verticalmente

Los usuarios esperan desplazamiento vertical en Teams (y en otros lugares). Esto puede no aplicarse si tiene un lienzo creativo, como una pizarra, que los usuarios pueden desplazar por los ejes x e y.

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Ejemplo que muestra el desplazamiento horizontal en una pestaña en la reunión." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-dont.png" alt-text="Ejemplo que muestra el desplazamiento horizontal en la fase de reunión compartida." border="false":::

#### <a name="dont-scroll-horizontally"></a>No: desplazarse horizontalmente

El desplazamiento horizontal no es un comportamiento esperado en Teams (incluido el entorno de reunión).

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

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-do.png" alt-text="Otro ejemplo que muestra la extensión de reunión con el tema oscuro." border="false":::

#### <a name="do-focus-on-dark-theme"></a>Do: Focus on dark theme

Teams reuniones están optimizadas para temas oscuros para ayudar a reducir el ruido visual y cognitivo para que los usuarios puedan centrarse en la discusión y el contenido compartido. Ten en cuenta que ciertos tipos de aplicaciones (como pizarras y edición de documentos) no necesitan un lienzo oscuro.

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Ejemplo que muestra una extensión de reunión con colores que no coinciden con el tema de la reunión." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-dont.png" alt-text="Otro ejemplo que muestra una extensión de reunión con colores que no coinciden con el tema de la reunión." border="false":::

#### <a name="dont-use-unfamiliar-colors"></a>No usar: usar colores desconocidos

Los colores que entren en conflicto con el entorno de reunión pueden ser molestos y parecer menos nativos de Teams. Obtenga información sobre la Teams [de color,](https://developer.microsoft.com/fluentui#/styles/web/colors/products)incluidos los neutros del tema de llamada.

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

### <a name="responsive-behavior"></a>Comportamiento dinámico

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-do.png" alt-text="Ejemplo que muestra cómo cambiar el tamaño de una extensión de reunión correctamente." border="false":::

#### <a name="do-resize-and-scale-your-app-responsively"></a>Do: Resize and scale your app responsively

El contenido de la aplicación debe cambiar el tamaño y condensarse dinámicamente en ventanas más pequeñas. Mantén visible la navegación principal de la aplicación y los controles flotantes.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-dont.png" alt-text="Ejemplo que muestra cómo no cambiar el tamaño de una extensión de reunión correctamente." border="false":::

#### <a name="dont-crop-or-clip-primary-ui-components"></a>No: recortar o recortar componentes de interfaz de usuario principales

La navegación flotante y los controles fuera de la pantalla y que requieren un desplazamiento para buscar pueden resultar confusos para los usuarios. El contenido de la aplicación no debe desplazarse horizontalmente cuando no cabe en el iframe.

   :::column-end:::
:::row-end:::

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Configurar la aplicación para reuniones](~/apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md)

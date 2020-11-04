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
# <a name="design-an-in-meeting-dialog"></a>Diseñar un diálogo dentro de la reunión

Los cuadros de diálogo en la reunión se muestran en la fase de reunión de Microsoft Teams. Requieren la atención, la confirmación o la interacción del usuario, pero son sutiles y no interrumpen la reunión.

## <a name="use-cases"></a>Casos de uso

Los cuadros de diálogo en la reunión son desencadenados por un usuario (como el organizador de la reunión) que puede desear a los participantes:

* Proporcionar comentarios breves
* Realizar una breve encuesta o sondeo
* Enviar aprobaciones
* Recibir recordatorios

## <a name="example"></a>Ejemplo

En el ejemplo siguiente se muestra el aspecto que puede tener el cuadro de diálogo en la reunión desde el punto de vista de un participante de la reunión. Como puede ver, el contenido y la tarea son ligeros.

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-participant-view.png" alt-text="Ejemplo muestra el aspecto que puede tener el cuadro de diálogo en la reunión desde el punto de vista de un participante de la reunión.":::

<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Vea el escenario completo (Figma)</a>

<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Consulte otros ejemplos de casos de uso (Figma)</a>

## <a name="anatomy"></a>Anatomía

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-anatomy.png" alt-text="Anatomía de la interfaz de usuario de una vista de diálogo en la reunión." border="false":::

1. **Icono de aplicación**
1. **Nombre de la aplicación**
1. **Cadena de acción**
1. **Descartar icono:** Cierra un único cuadro de diálogo. Use siempre el icono de cierre superior derecho en lugar de una acción en el pie de página.
1. **Vista WebView** : muestra todo el contenido de la aplicación de terceros y los botones (se recomiendan los botones estándar de Microsoft Teams).

### <a name="sizing"></a>Evaluación

Los cuadros de diálogo en la reunión pueden variar en tamaño para tener en cuenta los diferentes casos de uso, pero siempre debe mantener el relleno y los tamaños de los componentes.

* **Height** : el alto del cuadro de diálogo depende del contenido de la vista WebView. El desplazamiento vertical toma el control del contenido que supera el alto máximo especificado.
* **Width** : el ancho de la vista WebView es un valor absoluto dentro del intervalo especificado.

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-sizing.png" alt-text="Ilustración que muestra las dimensiones posibles de un cuadro de diálogo en la reunión. Height: el alto del cuadro de diálogo depende del contenido de la vista WebView. El desplazamiento vertical toma el control del contenido que supera la altura máxima (definido por el usuario). Min: ninguno. Máx: 400 píxeles (320 píxeles WebView). Width: el ancho de la vista WebView es un valor absoluto dentro del intervalo especificado. Min.: 288 píxeles (256 píxeles WebView). Máx: 468 píxeles (436 píxeles WebView)." border="false":::

## <a name="behavior"></a>Comportamiento

Vea comportamiento general del cuadro de diálogo de reunión en la reunión, como REST, carga, etc., en <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.

### <a name="position"></a>Position

Los diálogos en la reunión se alinean en el centro de la fase de reunión. No se pueden arrastrar y trabajar en el marco de las notificaciones de nivel de sistema de Teams.

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-position.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un cuadro de diálogo en la reunión." border="false":::

### <a name="aggregation"></a>Cronológica

Solo se muestra un cuadro de diálogo a la vez, la clasificación de la pila de la última a la más reciente que se envía a la parte inferior. Una vez que se resuelve o se descarta un cuadro de diálogo, el siguiente se ocupa de su posición.

<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Vea un ejemplo (Figma)</a>

### <a name="scrolling"></a>Desplazamiento

El desplazamiento se produce en la parte de WebView de un cuadro de diálogo en la reunión. Recuerde lo siguiente sobre el desplazamiento:

* Solo debe poder desplazarse verticalmente.
* Solo puede ver el contenido al que se ha desplazado (nada anterior o posterior).

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-scroll.png" alt-text="Ilustración que muestra cómo funciona el desplazamiento del contenido de WebView en el cuadro de diálogo de la reunión." border="false":::

### <a name="buttons"></a>Botones

Los botones de cuadro de diálogo en la reunión forman parte de la vista Web ([vea algunos ejemplos](#best-practices)).

A diferencia de los componentes similares, los cuadros de diálogo en la reunión se desechan una vez que un usuario selecciona un botón.

## <a name="components"></a>Componentes

Los cuadros de diálogo en la reunión se crean principalmente con los siguientes componentes de la <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">interfaz de usuario (Figma)</a>, que se basan en el <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">sistema de diseño de Fluent</a>.

Componente | Instrucciones | Ejemplo
 - | - | -
Botón | Los botones principal y secundario pueden ser medios o pequeños. | Enviar una respuesta
Input | Campo para la entrada de breves usuarios. El texto de la etiqueta puede incluir un icono  | Escribir comentarios
Desplegable | Seleccione una o más opciones de una lista. Puede incluir características de búsqueda y de selección múltiple | Elegir un idioma
Controles de selección | Use casillas de verificación para varias opciones o botones de radio y conmute a opciones únicas. Para selecciones más detalladas, use un control deslizante. | Votar en un sondeo
Alertas | Tanto si muestra un mensaje urgente, un estado de error o una advertencia, el mensaje debe ser corto y no interrumpir la tarea actual del usuario | Mostrar problema al enviar una respuesta

## <a name="theming"></a>Creación de temas

### <a name="colors"></a>Colores

Use la <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">combinación de colores recomendada (Figma)</a> para los fondos, los en primer plano y los Estados que transmiten.

### <a name="typography"></a>Tipografía

Use los <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">tamaños y pesos de fuente recomendados (Figma)</a> para títulos, texto principal y texto de metadatos.

## <a name="best-practices"></a>Procedimientos recomendados

Aunque los cuadros de diálogo en la reunión pueden hacer que las llamadas sean más eficaces, también pueden descarrilar las llamadas si son demasiado molestas. En general, use los cuadros de diálogo con moderación y siga estos procedimientos recomendados.

### <a name="navigation"></a>Navegación

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-steps-do.png" alt-text="Ilustración que muestra cómo limitar el contenido del cuadro de diálogo de reunión en una sola pantalla para que los usuarios puedan centrarse en la reunión." border="false":::

#### <a name="do-keep-it-contained"></a>Do: Keep it contenida

Limite el contenido del cuadro de diálogo de reunión a una sola pantalla para que los usuarios puedan centrarse en la reunión.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-steps-dont.png" alt-text="Ilustración que muestra cómo los cuadros de diálogo en la reunión no deben requerir que los usuarios naveguen por el contenido." border="false":::

#### <a name="dont-include-multiple-steps"></a>No: incluir varios pasos

Los cuadros de diálogo en la reunión no deben requerir que los usuarios naveguen por el contenido.

   :::column-end:::
:::row-end:::

### <a name="interactions"></a>Existentes

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

#### <a name="do-limit-number-of-interactions"></a>Do: limitar el número de interacciones

Quite el contenido innecesario que no ayude a los usuarios a realizar algo rápidamente. Si necesita interacciones complejas, se recomienda encarecidamente que, en su lugar, se muestre el contenido con una sola columna de la pestaña en reunión.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-tab-dont.png" alt-text="Ilustración que muestra que demasiadas interacciones en el cuadro de diálogo de la reunión distrae de la reunión." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a>No: introducir elementos innecesarios

Es posible que pueda diseñar un único cuadro de diálogo en reunión con varias interacciones, pero demasiados pueden distraerse de la reunión.

   :::column-end:::
:::row-end:::

### <a name="layout"></a>Diseño

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-layout-do.png" alt-text="Ilustración que muestra un diseño ideal para los cuadros de diálogo en reunión." border="false":::

#### <a name="do-use-single-column-layouts"></a>Do: usar diseños de columna única

Como los cuadros de diálogo están en el centro de la fase de reunión, la finalización de la tarea debería ser rápida y sencilla para evitar la frustración del usuario.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-layout-dont.png" alt-text="Ilustración que muestra el diseño de los cuadros de diálogo en reunión que no se recomienda." border="false":::

#### <a name="dont-clutter-the-space"></a>No: desorden el espacio

Un contenido denso o con gran estructura puede ser molesto y abrumador, especialmente durante una reunión.

   :::column-end:::
:::row-end:::

### <a name="size"></a>Size

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-size-do.png" alt-text="Ilustración que muestra cómo el tamaño del cuadro de diálogo en la reunión siempre debe ser el mismo." border="false":::

#### <a name="do-keep-it-consistent"></a>Do: mantener la coherencia

Esto es importante porque los cuadros de diálogo en la reunión siempre se muestran en la misma ubicación.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-size-dont.png" alt-text="Ilustración que muestra cómo no se deben usar diferentes tamaños de cuadro de diálogo." border="false":::

#### <a name="dont-always-fit-to-the-content"></a>No: siempre se ajusta al contenido

Es posible que esté intentando evitar el desplazamiento horizontal, pero varios tamaños de cuadro de diálogo en la reunión dentro de la misma aplicación son una experiencia incoherente.

   :::column-end:::
:::row-end:::

### <a name="controls"></a>Controles

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-controls-do.png" alt-text="Ilustración que muestra dónde situar botones en el cuadro de diálogo en reunión." border="false":::

#### <a name="do-right-align-the-primary-action"></a>Haga lo siguiente: alinear a la derecha la acción principal

Le recomendamos que sitúe la acción más intensa visualmente en la posición más a la derecha.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-controls-dont.png" alt-text="Ilustración que muestra dónde no desea situar botones en el cuadro de diálogo en reunión." border="false":::

#### <a name="dont-left-or-center-align-actions"></a>No: acciones alineadas a la izquierda o al centro

Esto se desvía del patrón de equipos estándar para la colocación de controles en un cuadro de diálogo y puede entrar en conflicto con un cuadro de diálogo detrás de uno superior.

   :::column-end:::
:::row-end:::

## <a name="accessibility"></a>Accesibilidad

Para obtener información sobre la accesibilidad, vea <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.

## <a name="resources"></a>Recursos

* <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Archivo Figma de extensiones de reunión de Microsoft Teams</a>

## <a name="validate-your-design"></a>Validar el diseño

Si planea publicar la aplicación en AppSource, debe comprender los problemas de diseño que suelen hacer que las aplicaciones fallen durante el envío.

> [!div class="nextstepaction"]
> [Comprobar las instrucciones de validación del diseño](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)

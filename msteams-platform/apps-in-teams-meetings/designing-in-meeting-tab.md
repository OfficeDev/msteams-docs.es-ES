---
title: Diseño de una ficha en la reunión de Microsoft Teams
author: heath-hamilton
description: Instrucciones y procedimientos recomendados para diseñar la pestaña en la reunión de Microsoft Teams.
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: ec095654f4a0816478b1b32a45c931d74dbb3209
ms.sourcegitcommit: aabfd65a67e1889ec16f09476bc757dd4a46ec5b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/18/2020
ms.locfileid: "48098075"
---
# <a name="designing-an-in-meeting-tab"></a>Diseño de una pestaña en la reunión

La pestaña en reunión es un lienzo para aumentar la colaboración durante las reuniones. Según la funcionalidad de la pestaña Microsoft Teams, los asistentes pueden ver e interactuar con el contenido de la aplicación en un espacio dedicado fuera de la fase de reunión a través de vistas compartidas o basadas en roles.

## <a name="use-cases"></a>Casos de uso

Los usuarios pueden usar la ficha en la reunión para:

* Proporcionar comentarios detallados (por ejemplo, evaluar un candidato de trabajo)
* Crear rápidamente un sondeo, una encuesta o un elemento de tarea para los participantes de la reunión
* Mostrar notas relevantes para la reunión (por ejemplo, información sobre un responsable de ventas)

## <a name="example"></a>Ejemplo

El siguiente ejemplo muestra la pestaña en la reunión que muestra el contenido de la aplicación de la encuesta.

:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-organizer-view.png" alt-text="Ejemplo muestra el aspecto que puede tener la ficha reunión en la reunión desde el punto de vista del organizador de la reunión.":::

<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Vea el escenario completo (Figma)</a>

<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Consulte otros ejemplos de casos de uso (Figma)</a>

## <a name="anatomy"></a>Anatomía

La pestaña en la reunión muestra el contenido de la aplicación con las siguientes dimensiones:

* **Width**: 280 píxeles para el área WebView. Hay 20 píxeles de relleno en los lados izquierdo y derecho de la WebView.
* **Altura**: sangrado completo hacia la parte inferior de la pestaña. Hay 20 píxeles de relleno entre el área WebView y el encabezado de pestaña.

:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una pestaña en la reunión de la extensión de reunión." border="false":::

1. **Icono**de la aplicación: el punto de entrada a la pestaña en reunión.
1. **Header**: incluye el nombre de la pestaña.
1. **Name**: el nombre de la instancia de la pestaña.
1. **Dismiss**: descarta la pestaña. Use siempre el icono de cierre superior derecho en lugar de una acción en el pie de página.
1. **Vista WebView**: muestra todo el contenido de aplicaciones de terceros.

## <a name="behavior"></a>Comportamiento

### <a name="scale"></a>Scale

Actualmente, el ancho de la pestaña en reunión es fijo.

### <a name="scrolling"></a>Desplazamiento

Esto es lo que debe saber sobre el desplazamiento en la pestaña en la reunión:

* Solo debe poder desplazarse verticalmente.
* Solo puede ver el contenido al que se ha desplazado (nada anterior o posterior).
* La barra de desplazamiento es parte del contenido de WebView.

:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-scroll.png" alt-text="Ilustración que muestra cómo funciona el desplazamiento del contenido de WebView en la pestaña en reunión." border="false":::

### <a name="navigation"></a>Navegación

Para los escenarios con capas de navegación o contenido pesado, se recomienda permitir que los usuarios naveguen a una capa secundaria. Los usuarios deben poder volver a la capa anterior.

:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-nav.png" alt-text="Ilustración que muestra cómo funciona la navegación a una capa secundaria de la pestaña en reunión." border="false":::

## <a name="components"></a>Componentes

Las pestañas en la reunión se crean principalmente con los siguientes componentes de la <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">interfaz de usuario (Figma)</a>, que se basan en el <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">sistema de diseño de Fluent</a>.

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

### <a name="responsiveness"></a>Capacidad

Los diseños de pestañas en la reunión deben poder escalarse a varios tamaños. Tenga en cuenta el modo en que la pestaña se escalará y tomará la forma antes, durante y después de la reunión.

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-before-meeting.png" alt-text="Ilustración que muestra que el contenido de la pestaña en la reunión es similar a una pestaña de pantalla completa antes y después de una reunión." border="false":::

#### <a name="before-the-meeting"></a>Antes de la reunión

Asegúrese de que el diseño de la pestaña se puede adaptar a un diseño derecho o izquierdo para diferentes idiomas y que los controles se mueven a las ubicaciones correctas. (Los diseños previos a la reunión también pueden aplicarse a los diseños posteriores a la reunión).

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-during-meeting.png" alt-text="Ilustración que muestra cómo el contenido de la ficha anterior a la reunión se comprime en la pestaña en reunión durante una reunión." border="false":::

#### <a name="during-the-meeting"></a>Durante la reunión

El contenido de la pestaña se ajusta en el diseño y la ubicación de la pestaña en la reunión.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Creación de temas

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-theming-do.png" alt-text="Ilustración que muestra cómo diseñar la pestaña en reunión para el tema oscuro usado en reuniones de Microsoft Teams." border="false":::

#### <a name="do-design-for-a-dark-theme"></a>Do: diseñar un tema oscuro

Las reuniones de Microsoft Teams están optimizadas para el modo oscuro para ayudar a reducir el ruido visual y cognitivo para que los usuarios puedan centrarse en la discusión y en el contenido compartido.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-theming-dont.png" alt-text="Ilustración que muestra que no se deben usar colores que no resultan favorables para el tema de Teams oscuro." border="false":::

#### <a name="dont-use-unfamiliar-colors"></a>No: usar colores no habituales

Los colores que entran en conflicto con el entorno de la reunión pueden distraerse y mostrarse menos nativos de Teams.

   :::column-end:::
:::row-end:::

### <a name="scrolling"></a>Desplazamiento

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-scroll-do.png" alt-text="Ilustración que muestra solo se debe permitir el desplazamiento vertical en la pestaña en reunión." border="false":::

#### <a name="do-scroll-vertically"></a>Hacer: desplazarse verticalmente

Los usuarios anticipan los desplazamientos verticales en Teams (y en cualquier otro lugar).

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-scroll-dont.png" alt-text="Ilustración en la que se muestra que se muestra que no se permite el desplazamiento horizontal en la pestaña en reunión." border="false":::

#### <a name="dont-scroll-horizontally"></a>No: desplazar horizontalmente

El desplazamiento horizontal no es un comportamiento esperado en Microsoft Teams. Otros lienzos del entorno de la reunión se desplazan verticalmente.

   :::column-end:::
:::row-end:::

### <a name="layout"></a>Diseño

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-layout-do.png" alt-text="Ilustración que muestra el diseño de columna única recomendada en la pestaña en reunión." border="false":::

#### <a name="do-single-columns"></a>Do: columnas únicas

Dada la naturaleza estrecha de las pestañas de la reunión, se recomienda encarecidamente mostrar el contenido en una sola columna.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-layout-dont.png" alt-text="Ilustración que muestra cómo no es ideal un diseño de dos columnas en la pestaña de la reunión." border="false":::

#### <a name="dont-multiple-columns"></a>No: varias columnas

Debido al espacio limitado de la pestaña en reunión, no se recomiendan los diseños con más de una columna.

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>Navegación

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-nav-do.png" alt-text="Ilustración que muestra que siempre debe proporcionar un botón atrás si la aplicación de pestañas en la reunión tiene más de un nivel de navegación." border="false":::

#### <a name="do-have-a-back-button"></a>Do: tener un botón atrás

Si tiene más de una capa de navegación, los usuarios deben poder volver a su vista anterior.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-nav-dont.png" alt-text="Ilustración que muestra que agregar otro botón cerrar en la pestaña de la reunión para la navegación es redundante y podría causar problemas." border="false":::

#### <a name="dont-include-another-close-button"></a>No: incluir otro botón cerrar

Ofrecer una opción para cerrar el contenido de la pestaña en la reunión puede causar problemas porque ya hay un botón cerrar en el encabezado para descartar la misma pestaña en la reunión.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-nav-caution.png" alt-text="Ilustración que muestra que debe tener cuidado al usar modales (es decir, módulos de tareas) en la ficha en la reunión que se proporciona el espacio limitado." border="false":::

#### <a name="caution-using-dialogs-in-a-narrow-space"></a>PRECAUCIÓN: uso de cuadros de diálogo en un espacio estrecho

Los cuadros de diálogo, como módulos de tareas, en la pestaña en la reunión ya estrecha pueden ajustar y oscurecer el contenido.

   :::column-end:::
:::row-end:::

## <a name="accessibility"></a>Accesibilidad

Para obtener información sobre la accesibilidad, vea <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.

## <a name="resources"></a>Recursos

* <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Archivo Figma de extensiones de reunión de Microsoft Teams</a>
* [Instrucciones de diseño de pestañas](../tabs/design/tabs.md)
* [Directrices de diseño de pestañas para dispositivos móviles](../tabs/design/tabs-mobile.md)

## <a name="validate-your-design"></a>Validar el diseño

Si planea publicar la aplicación en AppSource, debe comprender los problemas de diseño que suelen hacer que las aplicaciones fallen durante el envío.

> [!div class="nextstepaction"]
> [Comprobar las instrucciones de validación del diseño](../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines)

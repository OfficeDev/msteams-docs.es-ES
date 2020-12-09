---
title: Diseño de tarjetas adaptables para la aplicación
description: Obtenga información sobre cómo diseñar tarjetas adaptables para Teams y obtener el kit de la interfaz de usuario de Microsoft Teams.
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: bd48846284620415cc8cadabc59f2ab7b61d5189
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604557"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a>Diseño de tarjetas adaptables para su aplicación de Microsoft Teams

Una tarjeta adaptable contiene un cuerpo de forma libre de elementos de tarjeta y un conjunto opcional de acciones. Las tarjetas adaptables son fragmentos de código accionables que puede Agregar a una conversación a través de un bot o una extensión de mensajería. Mediante el uso de texto, gráficos y botones, estas tarjetas proporcionan una comunicación enriquecida a la audiencia.

El marco de tarjeta adaptable se usa en muchos productos de Microsoft, incluidos Teams. Puede enviar tarjetas dentro de los mensajes a los usuarios a través de bots o extensiones de mensajería. Los usuarios pueden realizar acciones en las tarjetas cuando están presentes.

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="Ejemplo muestra una tarjeta adaptable." border="false":::

## <a name="microsoft-teams-ui-kit"></a>Kit de IU de Microsoft Teams

Puede encontrar directrices de diseño más completas para las tarjetas adaptables en Microsoft Teams, incluidos los elementos que puede captar y modificar según sea necesario, en el kit de interfaz de usuario de Microsoft Teams. El kit de la interfaz de usuario también cubre temas esenciales como temas de temas, accesibilidad y ajuste de tamaño.

> [!div class="nextstepaction"]
> [Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a>Diseñador de tarjetas adaptables

También puede empezar a diseñar sus tarjetas adaptables directamente en el explorador.

> [!div class="nextstepaction"]
> [Pruebe el diseñador de tarjetas adaptables](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a>Tipos de tarjetas adaptables

### <a name="hero"></a>Elemento principal

Nuestra tarjeta más grande. Use para compartir artículos o escenarios en los que una imagen indica la mayor parte del artículo.

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="Ejemplo muestra una tarjeta adaptable." border="false":::

### <a name="thumbnail"></a>Thumbnail

Usar para enviar un mensaje accionable sencillo.

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="Ejemplo muestra una tarjeta adaptable." border="false":::

### <a name="list"></a>Lista

Úselo en escenarios donde desea que el usuario seleccione un elemento de una lista, pero los elementos no necesitan mucha explicación.

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="Ejemplo muestra una tarjeta adaptable." border="false":::

### <a name="digest"></a>Digest

Se usa para resúmenes de noticias y entradas de redondeo. Nota: se recomienda usar la tarjeta en miniatura para un solo elemento de actualización o de noticias.

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="Ejemplo muestra una tarjeta adaptable." border="false":::

### <a name="media"></a>Audiovisual

Se usa cuando se desea combinar texto y medios, como audio o vídeo.

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="Ejemplo muestra una tarjeta adaptable." border="false":::

### <a name="people"></a>Contactos

Se usa mejor para transmitir con eficacia quién está implicado en una tarea.

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="Ejemplo muestra una tarjeta adaptable." border="false":::

### <a name="request-ticket"></a>Vale de solicitud

Usar para obtener entradas rápidas de un usuario para crear automáticamente una tarea o un vale.

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="Ejemplo muestra una tarjeta adaptable." border="false":::

### <a name="imageset"></a>ImageSet

Use para enviar varias miniaturas de imagen.

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="Ejemplo muestra una tarjeta adaptable." border="false":::

### <a name="actionset"></a>ActionSet

Use esta opción cuando quiera que el usuario seleccione un botón y, a continuación, reúna los datos proporcionados por el usuario desde la misma tarjeta.

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="Ejemplo muestra una tarjeta adaptable." border="false":::

### <a name="choiceset"></a>ChoiceSet

Usar para recopilar varias entradas del usuario.

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="Ejemplo muestra una tarjeta adaptable." border="false":::

## <a name="anatomy"></a>Anatomía

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una tarjeta adaptable." border="false":::

Las tarjetas adaptables tienen mucha flexibilidad. Pero, como mínimo, se recomienda incluir los siguientes componentes en cada tarjeta:

|Counter|Descripción|
|----------|-----------|
|A|**Header**: hacer que los encabezados sean claros y concisos, pero descriptivos.|
|B|**Copia del cuerpo**: Use para transmitir detalles que sean demasiado largos o que no sean lo suficientemente grandes como para incluirlos en el encabezado.|
|C|**Acciones principales**: como procedimiento recomendado, incluya las acciones principales de 1-3. Se permiten seis como máximo.|

## <a name="best-practices"></a>Procedimientos recomendados

### <a name="primary-and-secondary-actions"></a>Acciones principales y secundarias

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de tarjetas adaptables." border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a>Do: usar hasta seis acciones principales

Aunque las tarjetas adaptables pueden admitir seis acciones principales, la mayoría de las cartas no las necesitan. Las acciones deben ser claras, concisas y directas. Menos es más.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de tarjetas adaptables." border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a>No: usar más de seis acciones principales

Las tarjetas adaptables deben presentar contenido rápido y accionable. Muchas acciones pueden sobrecargar a un usuario.

   :::column-end:::
:::row-end:::

### <a name="frequency"></a>Frecuencia

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de tarjetas adaptables." border="false":::

#### <a name="do-be-concise"></a>Do: ser conciso

Es fácil enviar varias tarjetas a una conversación, pero una vez que las tarjetas se desplazan fuera de la vista, se vuelven menos útiles. Intente limitarse a los conceptos básicos. Esto es especialmente cierto en un canal en el que los usuarios tienen menos tolerancia para lo que perciben como "ruido".

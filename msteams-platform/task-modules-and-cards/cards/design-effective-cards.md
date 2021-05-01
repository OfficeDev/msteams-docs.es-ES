---
title: Diseño de tarjetas adaptables para la aplicación
description: Obtén información sobre cómo diseñar tarjetas adaptables para Teams y obtener el kit Microsoft Teams interfaz de usuario.
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 14ffff1264e716e04a1ffb5549b71a8b7ec5fc14
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101740"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a>Diseño de tarjetas adaptables para tu Microsoft Teams aplicación

Una tarjeta adaptable contiene un cuerpo de forma libre de elementos de tarjeta y un conjunto opcional de acciones. Las tarjetas adaptables son fragmentos de contenido que se pueden usar y que se pueden agregar a una conversación a través de un bot o una extensión de mensajería. Con texto, gráficos y botones, estas tarjetas proporcionan una comunicación enriquecte a tu audiencia.

El marco de la tarjeta adaptable se usa en muchos productos de Microsoft, incluidos Teams. Puedes enviar tarjetas dentro de mensajes a los usuarios a través de bots o extensiones de mensajería. Los usuarios pueden realizar acciones en las tarjetas cuando están presentes.

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="Ejemplo de introducción a una tarjeta adaptable." border="false":::

## <a name="microsoft-teams-ui-kit"></a>Kit de UI de Microsoft Teams

Puedes encontrar instrucciones de diseño más completas para las tarjetas adaptables en Teams, incluidos los elementos que puedes agarrar y modificar según sea necesario, en el kit de interfaz Microsoft Teams usuario. El kit de interfaz de usuario también trata temas esenciales como temas, accesibilidad y tamaño dinámico.

> [!div class="nextstepaction"]
> [Obtener el Kit de UI de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a>Diseñador de tarjetas adaptables

También puedes empezar a diseñar las tarjetas adaptables directamente en el explorador.

> [!div class="nextstepaction"]
> [Probar el diseñador de tarjetas adaptables](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a>Tipos de tarjetas adaptables

### <a name="hero"></a>Elemento principal

Nuestra tarjeta más grande. Se usa para compartir artículos o escenarios en los que una imagen cuenta la mayor parte del artículo.

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="En el ejemplo se muestra una tarjeta de héroe de tarjeta adaptable." border="false":::

### <a name="thumbnail"></a>Miniatura

Se usa para enviar un mensaje sencillo que puede usarse.

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="En el ejemplo se muestra una tarjeta en miniatura de tarjeta adaptable." border="false":::

### <a name="list"></a>Lista

Se usa en escenarios en los que desea que el usuario elija un elemento de una lista, pero los elementos no necesitan mucha explicación.

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="En el ejemplo se muestra una tarjeta de lista de tarjeta adaptable." border="false":::

### <a name="digest"></a>Digest

Se usa para resúmenes de noticias y publicaciones de redondear. Nota: Se recomienda la tarjeta en miniatura para una sola actualización o elemento de noticias.

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="En el ejemplo se muestra una tarjeta implícita de tarjeta adaptable." border="false":::

### <a name="media"></a>Elementos multimedia

Úsalo cuando quieras combinar texto y medios, como audio o vídeo.

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="En el ejemplo se muestra una tarjeta multimedia de tarjeta adaptable." border="false":::

### <a name="people"></a>Personas

Se usa mejor cuando se transmite de forma eficaz quién está implicado en una tarea.

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="En el ejemplo se muestra una tarjeta de personas de tarjeta adaptable." border="false":::

### <a name="request-ticket"></a>Ticket de solicitud

Se usa para obtener entradas rápidas de un usuario para crear automáticamente una tarea o vale.

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="En el ejemplo se muestra una tarjeta de vale de solicitud de tarjeta adaptable." border="false":::

### <a name="imageset"></a>ImageSet

Se usa para enviar varias miniaturas de imagen.

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de imágenes de tarjeta adaptable." border="false":::

### <a name="actionset"></a>ActionSet

Úselo cuando desee que el usuario seleccione un botón y, a continuación, recopila la entrada de usuario adicional de la misma tarjeta.

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de acciones de tarjeta adaptable." border="false":::

### <a name="choiceset"></a>ChoiceSet

Se usa para recopilar varias entradas del usuario.

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de opciones de tarjeta adaptable." border="false":::

## <a name="anatomy"></a>Anatomía

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="En el ejemplo se muestra una tarjeta de anatomía de tarjeta adaptable." border="false":::

Las tarjetas adaptables tienen mucha flexibilidad. Pero, como mínimo, se recomienda incluir los siguientes componentes en cada tarjeta:

|Contador|Descripción|
|----------|-----------|
|A|**Encabezado:** haga que los encabezados sea claros y concisos, pero descriptivos.|
|B|**Copia del cuerpo:** se usa para transmitir detalles que son demasiado largos o que no son lo suficientemente importantes como para incluirlos en el encabezado.|
|C|**Acciones principales:** Como práctica recomendada, incluya de 1 a 3 acciones principales. Se permite un máximo de seis.|

## <a name="best-practices"></a>Procedimientos recomendados

Usa estas recomendaciones para crear una experiencia de aplicación de calidad.

### <a name="primary-and-secondary-actions"></a>Acciones principales y secundarias

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="Procedimiento recomendado sobre cómo debe incluir solo un pequeño conjunto de acciones en una tarjeta adaptable." border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a>Hacer: usar hasta seis acciones principales

Aunque las tarjetas adaptables pueden admitir seis acciones principales, la mayoría de las tarjetas no lo necesitan. Las acciones deben ser claras, concisos y directas. Menos es más.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="Procedimiento recomendado sobre cómo no saturar a los usuarios con demasiadas acciones en una tarjeta adaptable." border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a>No usar más de seis acciones principales

Las tarjetas adaptables deben presentar contenido rápido y fácil de usar. Demasiadas acciones pueden saturar a un usuario.

   :::column-end:::
:::row-end:::

### <a name="frequency"></a>Frecuencia

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="Procedimiento recomendado sobre la frecuencia de la tarjeta adaptable." border="false":::

#### <a name="do-be-concise"></a>Hacer: ser conciso

Es fácil enviar varias tarjetas a una conversación, pero una vez que las tarjetas se desplacen fuera de la vista, se vuelven menos útiles. Intenta limitarte a lo esencial. Esto es especialmente cierto en un canal donde los usuarios tienen menos tolerancia a lo que perciben como "ruido".

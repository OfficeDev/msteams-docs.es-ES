---
title: Diseño de tarjetas adaptables para la aplicación
description: Obtén información sobre cómo diseñar tarjetas adaptables para Teams y obtener el kit Microsoft Teams interfaz de usuario.
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: b4d5f43268c7bd5afecb56d26eb0d49ed6c9002b
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630312"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a>Diseño de tarjetas adaptables para tu Microsoft Teams aplicación

Una tarjeta adaptable contiene un cuerpo de forma libre de elementos de tarjeta y un conjunto opcional de acciones. Las tarjetas adaptables son fragmentos de contenido que se pueden usar y que se pueden agregar a una conversación a través de un bot o una extensión de mensajería. Con texto, gráficos y botones, estas tarjetas proporcionan una comunicación enriquecte a tu audiencia.

El marco de la tarjeta adaptable se usa en muchos productos de Microsoft, incluidos Teams. Puedes enviar tarjetas dentro de mensajes a los usuarios a través de bots o extensiones de mensajería. Los usuarios también pueden realizar acciones en las tarjetas cuando están presentes.

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

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="En el ejemplo se muestra una tarjeta de héroe de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="En el ejemplo se muestra una tarjeta de héroe de tarjeta adaptable en el móvil." border="false":::

---

### <a name="thumbnail"></a>Miniatura

Se usa para enviar un mensaje sencillo que puede usarse.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="En el ejemplo se muestra una tarjeta en miniatura de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="En el ejemplo se muestra una tarjeta en miniatura de tarjeta adaptable en el móvil." border="false":::

---

### <a name="list"></a>Lista

Se usa en escenarios en los que desea que el usuario elija un elemento de una lista, pero los elementos no necesitan mucha explicación.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="En el ejemplo se muestra una tarjeta de lista de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="En el ejemplo se muestra una tarjeta de lista de tarjeta adaptable en el móvil." border="false":::

---
Use for news digests and round-up posts. Note: We recommend the thumbnail card for a single update or news item.
':::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="Example shows an Adaptive Card digest card." border="false"::': null
':::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="Example shows an Adaptive Card digest card on mobile." border="false"::': null
---

### <a name="media"></a>Elementos multimedia

Úsalo cuando quieras combinar texto y medios, como audio o vídeo.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="En el ejemplo se muestra una tarjeta multimedia de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="En el ejemplo se muestra una tarjeta multimedia de tarjeta adaptable en el móvil." border="false":::

---

### <a name="people"></a>Personas

Se usa mejor cuando se transmite de forma eficaz quién está implicado en una tarea.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="En el ejemplo se muestra una tarjeta de personas de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="En el ejemplo se muestra una tarjeta de personas de tarjeta adaptable en el móvil." border="false":::

---

### <a name="request-ticket"></a>Ticket de solicitud

Se usa para obtener entradas rápidas de un usuario para crear automáticamente una tarea o vale.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="En el ejemplo se muestra una tarjeta de vale de solicitud de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="En el ejemplo se muestra una tarjeta de vale de solicitud de tarjeta adaptable en el móvil." border="false":::

---

### <a name="image-set"></a>Conjunto de imágenes

Se usa para enviar varias miniaturas de imagen.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de imágenes de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de imágenes de tarjeta adaptable en el móvil." border="false":::

---

### <a name="action-set"></a>Conjunto de acciones

Úselo cuando desee que el usuario seleccione un botón y, a continuación, recopila la entrada de usuario adicional de la misma tarjeta.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de acciones de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de acciones de tarjeta adaptable en el móvil." border="false":::

---

### <a name="choice-set"></a>Conjunto de opciones

Se usa para recopilar varias entradas del usuario.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de opciones de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de opciones de tarjeta adaptable en el móvil." border="false":::

---

## <a name="anatomy"></a>Anatomía

Las tarjetas adaptables tienen mucha flexibilidad. Pero, como mínimo, se recomienda incluir los siguientes componentes en cada tarjeta.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="EExample muestra la anatomía de la tarjeta adaptable." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="En el ejemplo se muestra la anatomía de la tarjeta adaptable en el móvil." border="false":::

---

|Contador|Descripción|
|----------|-----------|
|A|**Encabezado:** haga que los encabezados sea claros y concisos.|
|B|**Copia del cuerpo:** transmita detalles que sean demasiado largos o que no sean lo suficientemente importantes como para incluirlos en el encabezado.|
|C|**Acciones principales:** Como práctica recomendada, incluya de 1 a 3 acciones principales. Puede tener hasta seis.|

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

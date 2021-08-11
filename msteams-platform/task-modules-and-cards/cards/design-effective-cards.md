---
title: Diseño de Tarjetas adaptables para la aplicación
description: Obtenga información sobre cómo diseñar Tarjetas adaptables para Teams y obtener el Kit de interfaz de usuario de Microsoft Teams.
localization_priority: Priority
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: ca7c38f112808f98ae1555e91f794f032e880c862a697e1218953d40cbb410aa
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2021
ms.locfileid: "57708586"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a>Diseño de Tarjetas adaptables para la aplicación de Microsoft Teams

Una tarjeta adaptable contiene un cuerpo de forma libre de elementos de tarjeta y un conjunto opcional de acciones. Tarjetas adaptables son fragmentos de contenido accionables que puede agregar a una conversación a través de un bot o una extensión de mensajería. Con texto, gráficos y botones, estas tarjetas proporcionan una comunicación enriquecida a la audiencia.

El marco de tarjeta adaptable se usa en muchos productos de Microsoft, incluido Teams. Puede enviar tarjetas dentro de mensajes a los usuarios a través de bots o extensiones de mensajería. Los usuarios también pueden realizar acciones en las tarjetas cuando estén presentes.

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="Ejemplo de información general de una tarjeta adaptable." border="false":::

## <a name="microsoft-teams-ui-kit"></a>Kit de UI de Microsoft Teams

En el Kit de UI de Microsoft Teams encontrará instrucciones de diseño de bot más completas, que incluyen elementos que puede usar y modificar como quiera. El kit de interfaz de usuario también trata temas esenciales como temas, accesibilidad y ajuste de tamaño con capacidad de respuesta.

> [!div class="nextstepaction"]
> [Obtener el Kit de UI de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a>Diseñador de tarjetas adaptables.

También puede empezar a diseñar el Tarjetas adaptables directamente en el explorador.

> [!div class="nextstepaction"]
> [Pruebe el diseñador de Tarjetas adaptables](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a>Tipos de Tarjetas adaptables

### <a name="hero"></a>Elemento principal

Nuestra tarjeta de mayor tamaño. Se usa para compartir artículos o escenarios en los que una imagen cuenta la mayor parte de la historia.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="En el ejemplo se muestra una tarjeta de imagen prominente de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="En el ejemplo se muestra una tarjeta de imagen prominente de tarjeta adaptable en dispositivos móviles." border="false":::

---

### <a name="thumbnail"></a>Miniatura

Se usa para enviar un mensaje sencillo que requiere acción.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="En el ejemplo se muestra una tarjeta en miniatura de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="En el ejemplo se muestra una tarjeta en miniatura de tarjeta adaptable en dispositivos móviles." border="false":::

---

### <a name="list"></a>Lista

Se usa en escenarios en los que desea que el usuario elija un elemento de una lista, pero los elementos no necesitan mucha explicación.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="En el ejemplo se muestra una tarjeta de lista de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="En el ejemplo se muestra una tarjeta de lista de tarjetas adaptables en dispositivos móviles." border="false":::

---
Use for news digests and round-up posts. Note: We recommend the thumbnail card for a single update or news item.
':::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="Example shows an Adaptive Card digest card." border="false"::': null
':::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="Example shows an Adaptive Card digest card on mobile." border="false"::': null
---

### <a name="media"></a>Multimedia

Úselo cuando quiera combinar texto y elementos multimedia, como audio o vídeo.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="En el ejemplo se muestra una tarjeta multimedia de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="En el ejemplo se muestra una tarjeta multimedia de tarjeta adaptable en dispositivos móviles." border="false":::

---

### <a name="people"></a>Contactos

Se recomienda cuando se transmite de forma eficaz quién está implicado en una tarea.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="En el ejemplo se muestra una tarjeta de contactos de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="En el ejemplo se muestra una tarjeta de contactos de tarjeta adaptable en dispositivos móviles." border="false":::

---

### <a name="request-ticket"></a>Solicitar vale

Se usa para obtener entradas rápidas de un usuario para crear automáticamente una tarea o un vale.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="En el ejemplo se muestra una tarjeta de vale de solicitud de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="En el ejemplo se muestra una tarjeta de vale de solicitud de tarjeta adaptable en dispositivos móviles." border="false":::

---

### <a name="image-set"></a>Imágenes

Se usa para enviar varias miniaturas de imagen.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de imágenes de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de imágenes de tarjeta adaptable en dispositivos móviles." border="false":::

---

### <a name="action-set"></a>Conjunto de acciones

Úselo cuando quiera que el usuario seleccione un botón y, a continuación, recopile la entrada adicional del usuario de la misma tarjeta.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de acciones de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de acciones de tarjeta adaptable en dispositivos móviles." border="false":::

---

### <a name="choice-set"></a>Conjunto de opciones

Se usa para recopilar varias entradas del usuario.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de opciones de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de opciones de tarjeta adaptable en dispositivos móviles." border="false":::

---

## <a name="anatomy"></a>Anatomía

Tarjetas adaptables tienen mucha flexibilidad. Pero, como mínimo, se recomienda incluir los siguientes componentes en cada tarjeta.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="EExample muestra la anatomía de la tarjeta adaptable." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="En el ejemplo se muestra la anatomía de la tarjeta adaptable en dispositivos móviles." border="false":::

---

|Contador|Descripción|
|----------|-----------|
|A|**Encabezado**: haga que los encabezados sean claros y concisos.|
|N|**copia del cuerpo**: transmita detalles que son demasiado largos o no son lo suficientemente importantes como para incluirlos en el encabezado.|
|C|**Acciones principales**: como procedimiento recomendado, incluya de 1 a 3 acciones principales. Puede tener hasta seis.|

## <a name="best-practices"></a>Procedimientos recomendados

Use estas recomendaciones para crear una experiencia de aplicación de calidad.

### <a name="primary-and-secondary-actions"></a>Acciones principales y secundarias

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="Procedimiento recomendado para incluir solo un pequeño conjunto de acciones en una tarjeta adaptable." border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a>Hacer: Usar hasta seis acciones principales

Aunque Tarjetas adaptables puede admitir seis acciones principales, la mayoría de las tarjetas no lo necesitan. Las acciones deben ser claras, concisas y directas. Menos es más.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="Procedimiento recomendado para no sobrecargar a los usuarios con demasiadas acciones en una tarjeta adaptable." border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a>No: Usar más de seis acciones principales

Tarjetas adaptables debe presentar contenido rápido y accionable. Demasiadas acciones pueden sobrecargar a un usuario.

   :::column-end:::
:::row-end:::

### <a name="frequency"></a>Frecuencia

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="Procedimiento recomendado sobre la frecuencia de la tarjeta adaptable." border="false":::

#### <a name="do-be-concise"></a>Do: Sea conciso

Es fácil enviar varias tarjetas a una conversación, pero una vez que las tarjetas se desplazan fuera de la vista, resultan menos útiles. Intente limitarse a lo esencial. Esto es especialmente cierto en un canal en el que los usuarios tienen menos tolerancia a lo que perciben como "ruido".

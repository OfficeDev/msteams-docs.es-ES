---
title: Referencia de directrices de diseño
description: Describe las instrucciones para usar los campos y los controles flotantes en las aplicaciones.
keywords: Directrices de diseño de Microsoft Teams campos de referencia de componentes y controles flotantes
ms.openlocfilehash: 0f62d38bf961ae79b05c599638cefb3c76f46ed4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676140"
---
# <a name="fields-and-flyouts"></a>Campos y controles flotantes

---

## <a name="fields"></a>Fields

Los campos son áreas en las que los usuarios pueden escribir texto.

### <a name="padding-and-size"></a>Relleno y tamaño

Los campos de texto de una línea son un alto fijo de 32 que coinciden con el alto de otros componentes. Algunos campos de texto, como los campos Description, pueden ser más altos verticalmente para permitir más texto.
[!include[Padding and size](~/includes/design/fields-image-padding.html)]

### <a name="states"></a>Miembros

Estos son los Estados de los campos de texto. Los campos de texto existen en distintos Estados. Tenemos diseños específicos dedicados a nueve escenarios posibles, entre los que se incluyen (de arriba a abajo): campo de texto, teclado en el foco y cursor dentro del campo, teclado en foco con el texto escrito, el tratamiento de errores se ha realizado correctamente; error en el control de errores, texto no cifrado campo (incluido un icono X), campo de búsqueda (incluido un icono de búsqueda), campo de carga y un campo deshabilitado.
[!include[Field states](~/includes/design/fields-image-states.html)]

### <a name="formatting-help-text-and-labels"></a>Dar formato al texto y las etiquetas de ayuda

Los campos pueden contener texto de marcador de posición para proporcionar un ejemplo del tipo de información necesaria. También pueden contener etiquetas que proporcionen al usuario más contexto. Dentro de un campo, el texto siempre debe justificarse a la izquierda. También se utiliza la grafía de oraciones en este caso.

Usamos la interfaz de usuario de Segoe regular en 12 PTO (Caption) y $app-Gray-02 para las etiquetas. Para el texto de ayuda, usamos Segoe UI regular en 14 PT (base) y $app-Gray-02.
[!include[Fields typography](~/includes/design/fields-image-typography.html)]

---

## <a name="flyouts"></a>Flota

Los controles flotantes son más sencillos que los cuadros de diálogo y se pueden desechar rápidamente. Pueden contener botones, campos y otros componentes.
[!include[Flyouts](~/includes/design/flyouts-image.html)]

### <a name="sizing-and-padding"></a>Tamaño y relleno

Se recomienda un relleno de 16px a la izquierda y derecha del contenido.
[!include[Flyouts size and padding](~/includes/design/flyouts-image-sizepadding.html)]

### <a name="placement"></a>Placement

Los controles flotantes son contextuales y deben colocarse por encima, por debajo o junto al elemento que lo ha desactivado.

### <a name="scrolling"></a>Desplazamiento

El encabezado permanece en su ubicación para dar contexto al contenido que se va a desplazar.
[!include[Flyouts scrolling](~/includes/design/flyouts-image-scrolling.html)]

## <a name="mobile"></a>Mobile

Los campos son cuadros de entrada de texto que aceptan la entrada de los usuarios. Los menús desplegables son ventanas emergentes horizontales que aparecen en el panel superior y se pueden usar para mostrar más detalles sobre un elemento.

### <a name="field-controls"></a>Controles de campo

[!include[Mobile fields](~/includes/design/fields-mobile-image.html)]

### <a name="flyout-menu-list-controls"></a>Controles de lista de menús desplegables

[!include[Mobile flyout menu controls](~/includes/design/flyout-menu-mobile-image.html)]

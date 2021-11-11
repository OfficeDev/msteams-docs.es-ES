---
title: Diseño de Tarjetas adaptables para la aplicación
description: Obtenga información sobre cómo diseñar Tarjetas adaptables para Teams y obtener el Kit de interfaz de usuario de Microsoft Teams.
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: b016df98d57b9a3f5fe03e6cf26b31ad2d7b8db9
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/10/2021
ms.locfileid: "60887967"
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

#### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="En el ejemplo se muestra una tarjeta de elemento principal de tarjeta adaptable en dispositivos móviles." border="false":::

#### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="En el ejemplo se muestra una tarjeta de elemento principal de tarjeta adaptable." border="false":::

### <a name="thumbnail"></a>Miniatura

Se usa para enviar un mensaje sencillo que requiere acción.

#### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="En el ejemplo se muestra una tarjeta miniatura de tarjeta adaptable en dispositivos móviles." border="false":::

#### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="En el ejemplo se muestra una tarjeta miniatura de tarjeta adaptable." border="false":::

### <a name="list"></a>Lista

Se usa en escenarios en los que desea que el usuario elija un elemento de una lista, pero los elementos no necesitan mucha explicación.

#### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="En el ejemplo se muestra una tarjeta de lista de tarjetas adaptables en dispositivos móviles." border="false":::

#### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="En el ejemplo se muestra una tarjeta de lista de tarjeta adaptable." border="false":::

### <a name="digest"></a>Digest

Se usa para resúmenes de noticias y publicaciones de redondear. Nota: Se recomienda la tarjeta miniatura para una sola actualización o elemento de noticias.

#### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="Ejemplo se muestra una tarjeta de resumen de tarjeta adaptable en dispositivos móviles." border="false":::

#### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="ejemplo se muestra una tarjeta de resumen de tarjeta adaptable." border="false":::

### <a name="media"></a>Multimedia

Úselo cuando quiera combinar texto y elementos multimedia, como audio o vídeo.

#### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="En el ejemplo se muestra una tarjeta multimedia de tarjeta adaptable en dispositivos móviles." border="false":::

#### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="En el ejemplo se muestra una tarjeta multimedia de tarjeta adaptable." border="false":::

### <a name="people"></a>Contactos

Se recomienda cuando se transmite de forma eficaz quién está implicado en una tarea.

#### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="En el ejemplo se muestra una tarjeta de contactos de tarjeta adaptable en dispositivos móviles." border="false":::

#### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="En el ejemplo se muestra una tarjeta de contactos de tarjeta adaptable." border="false":::

### <a name="request-ticket"></a>Solicitar vale

Se usa para obtener entradas rápidas de un usuario para crear automáticamente una tarea o un vale.

#### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="En el ejemplo se muestra una tarjeta de vale de solicitud de tarjeta adaptable en dispositivos móviles." border="false":::

#### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="En el ejemplo se muestra una tarjeta de vale de solicitud de tarjeta adaptable." border="false":::

### <a name="imageset"></a>ImageSet

Se usa para enviar varias miniaturas de imagen.

#### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de imágenes de tarjeta adaptable en dispositivos móviles." border="false":::

#### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de imágenes de tarjeta adaptable." border="false":::

### <a name="actionset"></a>ActionSet

Úselo cuando quiera que el usuario seleccione un botón y, a continuación, recopile la entrada adicional del usuario de la misma tarjeta.

#### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de acciones de tarjeta adaptable en dispositivos móviles." border="false":::

#### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de acciones de tarjeta adaptable." border="false":::

### <a name="choiceset"></a>ChoiceSet

Se usa para recopilar varias entradas del usuario.

#### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de opciones de tarjeta adaptable en dispositivos móviles." border="false":::

#### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de opciones de tarjeta adaptable." border="false":::

## <a name="anatomy"></a>Anatomía

Tarjetas adaptables tienen mucha flexibilidad. Pero, como mínimo, se recomienda incluir los siguientes componentes en cada tarjeta.

#### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="En el ejemplo se muestra la anatomía de la tarjeta adaptable en dispositivos móviles." border="false":::

|Contador|Descripción|
|----------|-----------|
|A|**Encabezado**: haga que los encabezados sean claros y concisos.|
|N|**copia del cuerpo**: transmita detalles que son demasiado largos o no son lo suficientemente importantes como para incluirlos en el encabezado.|
|C|**Acciones principales**: como procedimiento recomendado, incluya de 1 a 3 acciones principales. Puede tener hasta seis.|

#### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="En el ejemplo se muestra la anatomía de la tarjeta adaptable." border="false":::

|Contador|Descripción|
|----------|-----------|
|A|**Encabezado**: haga que los encabezados sean claros y concisos.|
|N|**copia del cuerpo**: transmita detalles que son demasiado largos o no son lo suficientemente importantes como para incluirlos en el encabezado.|
|C|**Acciones principales**: como procedimiento recomendado, incluya de 1 a 3 acciones principales. Puede tener hasta seis.|

## <a name="best-practices"></a>Procedimientos recomendados

Las tarjetas diseñadas para una pantalla estrecha se escalan bien en pantallas más anchas (lo contrario no es cierto). También debe suponer que los usuarios no solo verán las tarjetas en el escritorio.

### <a name="column-layouts"></a>Diseños de columna

Use [`ColumnSet`](https://adaptivecards.io/explorer/ColumnSet.html) para dar formato al contenido de la tarjeta en una tabla o cuadrícula. Hay varias opciones para dar formato al ancho de columna. Estas directrices le ayudan a comprender cuándo usar cada una de ellas.

* `"width": "auto"`: cambia el tamaño de cada columna del `ColumnSet` para ajustarse al contenido de la aplicación que incluya en esa columna.
   * **Hacer**: se usa cuando tiene contenido de ancho variable y no es necesario dar prioridad a una columna específica.
   * **Hacer**: para cada `TextBlock`, establezca `"wrap": true` ya que el texto no se ajusta de forma predeterminada.
   * **No hacer**: establezca `"width": "auto"` para cada contenedor de columnas. Por ejemplo, si tiene una entrada y un botón en paralelo, es posible que el botón se corte en algunas pantallas. En su lugar, establezca `auto` para la columna con botones y otro contenido que siempre debe estar completamente visible.
* `"width": "stretch"`: tamaño de las columnas según el `ColumnSet`width disponible. Cuando varias columnas usan el valor `"stretch"`, comparten igualmente el ancho disponible.
   * **Hacer**: se usa con una columna si todas las demás columnas tienen un ancho estático. Por ejemplo, tiene imágenes en miniatura en una columna de 50 píxeles de ancho.
* `"width": "<number>"`: Ajusta el tamaño de las columnas con una proporción del ancho `ColumnSet` disponible. Por ejemplo, si establece tres columnas con `"width": "1"`, `"width": "4"` y `"width": "5"`, las columnas ocuparán un 10, 40 y un 50 por ciento del ancho disponible.
* `"width": "<number>px"`: Ajusta tamaño de las columnas en un ancho de píxel específico. Este enfoque es útil al crear tablas.
   * **Hacer**: se usa cuando no es necesario cambiar el ancho de lo que se muestra (por ejemplo, números y porcentajes).
   * **No hacer**: supera accidentalmente el ancho de lo que puede mostrar la tarjeta. Recuerde que el ancho de pantalla disponible depende del dispositivo. Teams Mobile tampoco admite el desplazamiento horizontal como el escritorio de Teams.

#### <a name="example-knowing-when-to-stretch-columns"></a>Ejemplo: saber cuándo se deben ampliar las columnas

# <a name="design"></a>[Diseño](#tab/design)

**Hacer**: en esta pantalla, hay dos columnas en la parte inferior de la tarjeta. El ancho del componente de entrada se establece en `stretch`, mientras que el ancho del botón **Seleccionar** se establece en `auto`. Esto garantiza que el botón permanece completamente a la vista.

:::image type="content" source="~/assets/images/adaptive-cards/width-auto-do.png" alt-text="La imagen muestra cómo establecer el ancho de columna en Tarjetas adaptables.":::

**No hacer**: en esta pantalla, ambas columnas están`width`establecidas en `auto`. Esto hace que el botón **Seleccionar** de la derecha se corte ligeramente en comparación con la entrada.

:::image type="content" source="~/assets/images/adaptive-cards/width-auto-dont.png" alt-text="La imagen muestra cómo no establecer el ancho de columna en Tarjetas adaptables.":::

# <a name="code"></a>[Código](#tab/code)

Este es el código para implementar el ejemplo de diseño que debe seguir.

```json
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.2",
  "body": [
    {
      "type": "TextBlock",
      "text": "I wasn't able to identify the type of expense. Select from the list:",
      "wrap": true,
      "id": "typePrompt",
      "spacing": "Medium",
      "size": "Medium"
    },
    {
      "type": "ActionSet",
      "actions": [
        {
          "type": "Action.Submit",
          "title": "Phone Bill",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Phone Bill",
              "action": "Phone Bill"
            },
            "action": "Phone Bill"
          }
        },
        {
          "type": "Action.Submit",
          "title": "Taxi and Other Transportation",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Taxi and Other Transportation",
              "action": "Taxi and Other Transportation"
            },
            "action": "Taxi and Other Transportation"
          }
        },
        {
          "type": "Action.Submit",
          "title": "Entertainment_misc",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Entertainment_misc",
              "action": "Entertainment_misc"
            },
            "action": "Entertainment_misc"
          }
        },
        {
          "type": "Action.Submit",
          "title": "Car Rental",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Car Rental",
              "action": "Car Rental"
            },
            "action": "Car Rental"
          }
        },
        {
          "type": "Action.Submit",
          "title": "Airfare",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Airfare",
              "action": "Airfare"
            },
            "action": "Airfare"
          }
        }
      ],
      "spacing": "Medium"
    },
    {
      "type": "TextBlock",
      "text": "     ",
      "wrap": true
    },
    {
      "type": "ColumnSet",
      "columns": [
        {
          "type": "Column",
          "width": "stretch",
          "items": [
            {
              "type": "Input.ChoiceSet",
              "choices": [
                {
                  "title": "Meals",
                  "value": "Meals"
                },
                {
                  "title": "Parking/Tolls",
                  "value": "Parking/Tolls"
                },
                {
                  "title": "Accomodation",
                  "value": "Accomodation"
                },
                {
                  "title": "Fuel-Gas/Petrol/Diesel",
                  "value": "Fuel-Gas/Petrol/Diesel"
                },
                {
                  "title": "Hotel",
                  "value": "Hotel"
                },
                {
                  "title": "Meals - Employees Only",
                  "value": "Meals - Employees Only"
                },
                {
                  "title": "Accomodations",
                  "value": "Accomodations"
                },
                {
                  "title": "Misc.Expenses",
                  "value": "Misc.Expenses"
                },
                {
                  "title": "Please Categorize",
                  "value": "Please Categorize"
                }
              ],
              "placeholder": "All",
              "id": "expenseTypes",
              "value": "Meals - Employees Only"
            }
          ]
        },
        {
          "type": "Column",
          "width": "auto",
          "items": [
            {
              "type": "ActionSet",
              "actions": [
                {
                  "type": "Action.Submit",
                  "title": "Select",
                  "data": {
                    "msteams": {
                      "type": "messageBack",
                      "displayText": "Select",
                      "action": "applyType"
                    },
                    "action": "applyType"
                  }
                }
              ]
            }
          ]
        }
      ],
      "spacing": "ExtraLarge"
    }
  ]
}
```

---

#### <a name="example-using-fewer-columns"></a>Ejemplo: Uso de menos columnas

**Hacer**: los diseños tienden a mostrarse mejor en dispositivos móviles con menos columnas.

:::image type="content" source="~/assets/images/adaptive-cards/column-amount-do.png" alt-text="La imagen muestra la cantidad correcta de columnas en Tarjetas adaptables.":::

**No hacer**: el uso de demasiadas columnas puede saturar el contenido de la tarjeta en dispositivos móviles.

:::image type="content" source="~/assets/images/adaptive-cards/column-amount-dont.png" alt-text="La imagen muestra cuántas columnas pueden afectar negativamente al diseño de tarjeta adaptable.":::

#### <a name="example-fixed-width-has-its-place"></a>Ejemplo: el ancho fijo tiene su lugar

# <a name="design"></a>[Diseño](#tab/design)

Cuando no sea necesario cambiar el tamaño de algo que se muestra, establezca las columnas en un ancho de píxel específico. En este ejemplo se muestra la columna izquierda con un tamaño de 50 píxeles, mientras que las descripciones situadas junto a las miniaturas amplían la longitud de la tarjeta.

:::image type="content" source="~/assets/images/adaptive-cards/width-auto-do.png" alt-text="La imagen muestra cómo establecer el ancho de columna en Tarjetas adaptables.":::

# <a name="code"></a>[Código](#tab/code)

Este es el código para implementar el ejemplo de diseño.

```json
{
  "type": "AdaptiveCard",
  "version": "1.0",
  "body": [
    {
      "type": "TextBlock",
      "text": "Pick up where you left off?",
      "weight": "bolder"
    },
    {
      "type": "ColumnSet",
      "spacing": "medium",
      "columns": [
        {
          "type": "Column",
          "width": "50px",
          "items": [
            {
              "type": "Image",
              "url": "https://unsplash.it/80?image=1083",
              "size": "medium"
            }
          ]
        },
        {
          "type": "Column",
          "width": "stretch",
          "items": [
            {
              "type": "TextBlock",
              "text": "Silver Star Mountain Range"
            },
            {
              "type": "TextBlock",
              "text": "Maps",
              "isSubtle": true,
              "spacing": "none"
            }
          ]
        }
      ],
      "selectAction": {
        "type": "Action.OpenUrl",
        "url": "https://www.msn.com"
      }
    },
    {
      "type": "ColumnSet",
      "columns": [
        {
          "type": "Column",
          "width": "50px",
          "items": [
            {
              "type": "Image",
              "url": "https://unsplash.it/80?image=1082",
              "size": "medium"
            }
          ]
        },
        {
          "type": "Column",
          "width": "stretch",
          "style": "emphasis",
          "items": [
            {
              "type": "TextBlock",
              "text": "Kitchen Remodel for Homes"
            },
            {
              "type": "TextBlock",
              "text": "With EMPHASIS",
              "isSubtle": true,
              "spacing": "none"
            }
          ]
        }
      ],
      "selectAction": {
        "type": "Action.OpenUrl",
        "url": "https://www.AdaptiveCards.io"
      }
    },
    {
      "type": "ColumnSet",
      "columns": [
        {
          "type": "Column",
          "width": "50px",
          "items": [
            {
              "type": "Image",
              "url": "https://unsplash.it/80?image=1080",
              "size": "medium"
            }
          ]
        },
        {
          "type": "Column",
          "width": "stretch",
          "items": [
            {
              "type": "TextBlock",
              "text": "The Witcher: A Series"
            },
            {
              "type": "TextBlock",
              "text": "Netflix",
              "isSubtle": true,
              "spacing": "none"
            }
          ]
        }
      ],
      "selectAction": {
        "type": "Action.OpenUrl",
        "url": "https://www.outlook.com"
      }
    }
  ],
  "actions": [
    {
      "type": "Action.OpenUrl",
      "title": "Resume all",
      "url": "ms-cortana:resume-all"
    },
    {
      "type": "Action.OpenUrl",
      "title": "More activities",
      "url": "ms-cortana:more-activities"
    }
  ]
}
```

---

### <a name="text"></a>Text

Ya sea que este usando [`TextBlock`](https://adaptivecards.io/explorer/TextBlock.html), [`ColumnSet`](https://adaptivecards.io/explorer/ColumnSet.html), o [`Input.ChoiceSet`](https://adaptivecards.io/explorer/Input.ChoiceSet.html), establezca la `wrap` propiedad en `true` para que su texto de tarjeta no quede truncado en los dispositivos móviles.

#### <a name="example-making-sure-text-doesnt-truncate"></a>Ejemplo: Asegurarse de que el texto no se trunca

# <a name="design"></a>[Diseño](#tab/design)

**Hacer**: en esta pantalla, la tarjeta tiene una propiedad `wrap` establecida en `true`. Esto permite que el texto se ajuste a cualquier tamaño de pantalla.

:::image type="content" source="~/assets/images/adaptive-cards/text-wrap-true.png" alt-text="Imagen muestra cómo ajustar texto en Tarjetas adaptables.":::

**No hacer**: en esta pantalla, la tarjeta no usa la propiedad `wrap`, por lo que el texto se corta en una pantalla móvil.

:::image type="content" source="~/assets/images/adaptive-cards/text-wrap-false.png" alt-text="La imagen muestra lo que puede ocurrir si no ajusta texto en Tarjetas adaptables.":::

# <a name="code"></a>[Código](#tab/code)

Este es el código para implementar el ejemplo de diseño que debe seguir.

```json
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.0",
  "body": [
    {
      "type": "TextBlock",
      "text": "What cuisine do you want?"
    },
    {
      "type": "Input.ChoiceSet",
      "id": "myColor",
      "style": "compact",
      "isMultiSelect": false,
      "value": "1",
      "choices": [
        {
          "title": "Chineese",
          "value": "1"
        },
        {
          "title": "Indian",
          "value": "2"
        },
        {
          "title": "Italian",
          "value": "3"
        }
      ]
    },
    {
      "type": "TextBlock",
      "text": "Select the dishes that you like?"
    },
    {
      "type": "Input.ChoiceSet",
      "id": "myColor2",
      "style": "expanded",
      "wrap" : true,
      "isMultiSelect": false,
      "value": "1",
      "choices": [
        {
          "title": "Cauliflower with potatoes sautéed with garam masala",
          "wrap" : true,
          "value": "1"
        },
        {
          "title": "Patties of potato mixed with some vegetables fried",
          "wrap" : true,
          "value": "2"
        },
        {
          "title": "Green capsicum with potatoes sautéed with cumin seeds",
          "wrap" : true,
          "value": "3"
        }
      ]
    }
  ]
}
```

---

### <a name="containers"></a>Contenedores

Un `Container` permite agrupar un conjunto de elementos relacionados.

* **Hacer**: use la propiedad `style` para enfatizar un contenedor.
* **Hacer**: use la propiedad `selectAction` para asociar una acción a los demás elementos del contenedor.
* **Hacer**: use la propiedad `Action.ToggleVisibility` para contraer un grupo de elementos.
* **No hacer**: use contenedores por cualquier motivo distinto al mencionado anteriormente.

### <a name="images"></a>Imágenes

Siga estas instrucciones al incluir imágenes en las tarjetas.

* **Hacer**: diseña imágenes para pantallas con valores altos de PPP para evitar la pixelación. Es mejor mostrar una imagen de 100x100 píxeles a 50x50 píxeles que al revés.
* **Hacer**: si necesita controlar el tamaño exacto de las imágenes, use las propiedades `width` y `height`.
* **No hacer**: incluir relleno con las imágenes. Esto suele introducir problemas de espaciado y diseño no deseados.
* Con respecto al color de fondo:
   * **Hacer**: use fondos transparentes para que las imágenes se adapten a cualquier tema de Teams. 
   * **No hacer**: incluye un color de fondo fijo a menos que un color específico sea visible para los usuarios.
   * **No hacer**: Agrega un color de fondo a un `TextBlock` que afecta a la legibilidad. Por ejemplo, si el fondo es oscuro, use un color de texto más claro y viceversa.

### <a name="actions"></a>Acciones

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

## <a name="see-also"></a>Consulte también

* [Tarjetas y módulos de tareas](~/task-modules-and-cards/cards-and-task-modules.md)
* [Tarjetas y módulos de tareas admitidos en el bot de Teams](~/task-modules-and-cards/what-are-task-modules.md)
* [Trabajar con Acciones universales para tarjetas adaptables](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/work-with-universal-actions-for-adaptive-cards.md)
* [Responder a la acción de envío del módulo de tareas](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)
* [Vistas específicas de usuario](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/user-specific-views.md)

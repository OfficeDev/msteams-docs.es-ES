---
title: Búsqueda de punta de punta en tarjetas adaptables
author: Rajeshwari-v
description: Describe la búsqueda de punta de tipo con el control Input.ChoiceSet en tarjetas adaptables
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 95041b1a24ac083329a809b8a5989d77e2430e26
ms.sourcegitcommit: e45742fd2aa2ff5e5c15e8f7c20cc14fbef6d441
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2021
ms.locfileid: "61075586"
---
# <a name="typeahead-search-in-adaptive-cards"></a>Búsqueda de punta de punta en tarjetas adaptables

La funcionalidad de búsqueda typeahead en tarjetas adaptables proporciona una experiencia de búsqueda mejorada en `input.choiceset` el componente. Proporciona una lista de opciones para escribir texto en el campo de búsqueda. Puede incorporar la búsqueda de punta de tipo con tarjetas adaptables para buscar y seleccionar datos.

Puede usar la búsqueda de punta de tipo para las siguientes búsquedas:

* [Búsqueda estática](#static-typeahead-search)
* [Búsqueda dinámica](#dynamic-typeahead-search)

## <a name="static-typeahead-search"></a>Búsqueda de punta de tipo estática

La búsqueda de punta de tipo estática permite a los usuarios buscar desde los valores especificados en `input.choiceset` la carga de la tarjeta adaptable. La búsqueda de punta de tipo estática se puede usar para mostrar varias opciones al usuario. El tamaño de carga en la búsqueda estática aumenta con el número de opciones especificadas en la carga.
Cuando el usuario empieza a escribir los textos, las opciones se filtran, que coinciden parcialmente con la entrada. La lista desplegable resalta los caracteres de entrada que coinciden con la búsqueda.

En la siguiente imagen se muestra la búsqueda de punta de tipo estática:

![Búsqueda de punta de tipo estática](~/assets/images/Cards/static-typeahead-search.gif)

## <a name="dynamic-typeahead-search"></a>Búsqueda de punta de tipo dinámica

La búsqueda de punta de tipo dinámica es útil para buscar y seleccionar datos de grandes conjuntos de datos. Los conjuntos de datos se cargan dinámicamente desde el conjunto de datos especificado en la carga de la tarjeta. La funcionalidad de tipo delante ayuda a filtrar las opciones a medida que el usuario escribe.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

![Búsqueda de punta de tipo dinámica](~/assets/images/Cards/dynamic-typeahead-search-desktop.png)

![Imagen de búsqueda de tipo dinámico 2](~/assets/images/Cards/dynamic-typeahead-search-desktop-2.png)

# <a name="mobile"></a>[Móvil](#tab/mobile)

Los clientes móviles de Android e iOS admiten la búsqueda de punta de tipo en tarjetas adaptables.

**Escenario**

John es un empleado de la tienda que trabaja en una tienda comercial de Xbox. La tienda usa un bot para tomar nuevas solicitudes de compra de los clientes. Un cliente puede buscar en los miles de juegos disponibles. La búsqueda de punta de punta en tarjetas adaptables se usa para buscar y seleccionar las opciones de los clientes.

**Para usar la búsqueda de punta de tipo en tarjetas adaptables**

1. El usuario A abre el bot de la tienda.
1. El usuario A envía un comando al bot para una **nueva solicitud de cliente**. El bot responde con la tarjeta adaptable que tiene `Input.ChoiceSet` componente.
1. El usuario A usa la búsqueda de punta de tipo para buscar y seleccionar la información según la elección del cliente.

En la siguiente imagen se muestra la experiencia móvil de la búsqueda de punta de tipo:

![Búsqueda de punta de tipo estática](~/assets/images/Cards/static-typeahead-search.gif)

---

> [!NOTE]
> No puede obtener experiencias de tarjeta enriquecciones con búsqueda dinámica, como extensiones de mensajería basadas en consultas.

## <a name="implement-typeahead-search"></a>Implementar la búsqueda de punta de tipo

`Input.ChoiceSet` es uno de los componentes de entrada importantes de las tarjetas adaptables. Puede agregar un control de búsqueda de punta de tipo al `Input.ChoiceSet` componente para implementar la búsqueda de punta de tipo. Puede buscar y seleccionar la información necesaria con las siguientes selecciones:

* Desplegable, como selección expandida.
* Botón de radio, como una selección única.
* Casillas, como varias selecciones.

> [!NOTE]
> El `Input.ChoiceSet` control se basa en el estilo y las `isMultiSelect` propiedades.

### <a name="schema-properties"></a>Propiedades de esquema

Las propiedades siguientes son las nuevas adiciones al [`Input.ChoiceSet`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) esquema para habilitar la búsqueda de punta de tipo:

| Propiedad| Tipo | Necesario | Description |
|-----------|------|----------|-------------|
| style | Compact <br/> Expanded <br/> Filtered | No | Agrega estilo filtrado a la lista de validaciones admitidas para el tipo estático por delante.|
| choices.data | Data.Query | No | Habilita el tipo dinámico a medida que el usuario escribe, mediante la captura de un conjunto remoto de opciones de un back-end. |

### <a name="dataquery-definition"></a>Definición Data.Query

| Propiedad| Tipo | Necesario | Description |
|-----------|------|----------|-------------|
| tipo | Data.Query | Sí | Especifica que es un objeto Data.Query.|
| conjunto de datos | Cadena | Sí | Especifica el tipo de datos que se captura dinámicamente. |
| value | Cadena | No | Se rellena para la solicitud de invocación al bot con la entrada que el usuario proporcionó al `ChoiceSet` . |
| count | Número | No | Se rellena para la solicitud de invocación al bot para especificar el número de elementos que se deben devolver. El bot lo omite, si los usuarios desean enviar una cantidad diferente. | 
| skip | Número | No | Se rellena para la solicitud de invocación al bot para indicar que los usuarios desean paginar y avanzar en la lista. |

### <a name="example"></a>Ejemplo

La carga de ejemplo que contiene la búsqueda de punta de tipo estática y dinámica con una sola & opciones de selección múltiple de la siguiente manera:

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "columns": [
        {
          "width": "1",
          "items": [
            {
              "size": null,
              "url": "https://urlp.asm.skype.com/v1/url/content?url=https%3a%2f%2fi.imgur.com%2fhdOYxT8.png",
              "height": "auto",
              "type": "Image"
            }
          ],
          "type": "Column"
        },
        {
          "width": "2",
          "items": [
            {
              "size": "extraLarge",
              "text": "Game Purchase",
              "weight": "bolder",
              "wrap": true,
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "text": "Please fill out the below form to send a game purchase request.",
      "wrap": true,
      "type": "TextBlock"
    },
    {
      "columns": [
        {
          "width": "auto",
          "items": [
            {
              "text": "Game: ",
              "wrap": true,
              "height": "stretch",
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "stretch",
          "items": [
            {
              "choices": [
                {
                  "title": "Call of Duty",
                  "value": "call_of_duty"
                },
                {
                  "title": "Death's Door",
                  "value": "deaths_door"
                },
                {
                  "title": "Grand Theft Auto V",
                  "value": "grand_theft"
                },
                {
                  "title": "Minecraft",
                  "value": "minecraft"
                }
              ],
              "style": "filtered",
              "placeholder": "Search for a game",
              "id": "choiceGameSingle",
              "type": "Input.ChoiceSet"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "auto",
          "items": [
            {
              "text": "Multi-Game: ",
              "wrap": true,
              "height": "stretch",
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "stretch",
          "items": [
            {
              "choices": [
                {
                  "title": "Static Option 1",
                  "value": "static_option_1"
                },
                {
                  "title": "Static Option 2",
                  "value": "static_option_2"
                },
                {
                  "title": "Static Option 3",
                  "value": "static_option_3"
                }
              ],
              "isMultiSelect": true,
              "style": "filtered",
              "choices.data": {
                "type": "Data.Query",
                "dataset": "xbox"
              },
              "id": "choiceGameMulti",
              "type": "Input.ChoiceSet"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "auto",
          "items": [
            {
              "text": "Needed by: ",
              "wrap": true,
              "height": "stretch",
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        },
        {
          "width": "stretch",
          "items": [
            {
              "id": "choiceDate",
              "type": "Input.Date"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "text": "Buy and download digital games and content directly from your Xbox console, Windows 10 PC, or at Xbox.com.",
      "wrap": true,
      "type": "TextBlock"
    },
    {
      "text": "Earn points for what you already do on Xbox, then redeem your points on real rewards. Play more, get rewarded. Start earning today.",
      "wrap": true,
      "type": "TextBlock"
    }
  ],
  "actions": [
    {
      "data": {
        "msteams": {
          "type": "invoke",
          "value": {
            "type": "task/submit"
          }
        }
      },
      "title": "Request Purchase",
      "type": "Action.Submit"
    }
  ],
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "version": "1.2"
}
```

## <a name="see-also"></a>Vea también

* [Acciones universales para tarjetas adaptables](Universal-actions-for-adaptive-cards/Overview.md)
* [Módulos de tareas](../what-are-task-modules.md)
---
title: Búsqueda de escritura anticipada en Tarjetas adaptables
author: Rajeshwari-v
description: En este módulo, obtenga información sobre lo que es la búsqueda de typeahead en tarjetas adaptables con el control Input.ChoiceSet e implemente la búsqueda de typeahead.
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: 205da5ca0171182047ccd06f7f2926f731ceb94d
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143896"
---
# <a name="typeahead-search-in-adaptive-cards"></a>Búsqueda de escritura anticipada en Tarjetas adaptables

La funcionalidad de búsqueda de typeahead en tarjetas adaptables proporciona una experiencia de búsqueda mejorada en el `input.choiceset` componente. Proporciona una lista de opciones para escribir texto en el campo de búsqueda. Puede incorporar la búsqueda de typeahead con tarjetas adaptables para buscar y seleccionar datos.

Puede usar la búsqueda de typeahead para las siguientes búsquedas:

* [Búsqueda estática](#static-typeahead-search)
* [Búsqueda dinámica](#dynamic-typeahead-search)

## <a name="static-typeahead-search"></a>Búsqueda de encabezado de tipo estático

La búsqueda de encabezado de tipo estático permite a los usuarios buscar desde los valores especificados en `input.choiceset` la carga de la tarjeta adaptable. La búsqueda de encabezado de tipo estática se puede usar para mostrar varias opciones al usuario. El tamaño de carga en la búsqueda estática aumenta con el número de opciones especificadas en la carga.
A medida que el usuario comienza a escribir los textos, se filtran las opciones, que coinciden parcialmente con la entrada. La lista desplegable resalta los caracteres de entrada que coinciden con la búsqueda.

En la imagen siguiente se muestra la búsqueda de encabezado de tipo estática:

![Búsqueda de encabezado de tipo estático](~/assets/images/Cards/static-typeahead-search.gif)

## <a name="dynamic-typeahead-search"></a>Búsqueda dinámica de encabezados de tipo

La búsqueda dinámica de encabezados de tipo es útil para buscar y seleccionar datos de grandes conjuntos de datos. Los conjuntos de datos se cargan dinámicamente desde el conjunto de datos especificado en la carga de la tarjeta. La funcionalidad de tipo delante ayuda a filtrar las opciones como tipos de usuario.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/Cards/dynamic-typeahead-search-desktop.png" alt-text="Búsqueda dinámica de encabezados de tipo":::

:::image type="content" source="../../assets/images/Cards/dynamic-typeahead-search-desktop-2.png" alt-text="Búsqueda dinámica de tipoahead 2":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

Android y iOS clientes móviles admiten la búsqueda de typeahead en tarjetas adaptables.

**Escenario**

John es un empleado de la tienda que trabaja en una tienda minorista de Xbox. La tienda usa un bot para realizar nuevas solicitudes de compra de los clientes. Un cliente puede buscar en los miles de juegos disponibles. La búsqueda de typeahead en tarjetas adaptables se usa para buscar y seleccionar las opciones de los clientes.

**Para usar la búsqueda de typeahead en tarjetas adaptables**

1. El usuario A abre el bot de la tienda.
1. El usuario A envía un comando al bot para una **nueva solicitud de cliente**. El bot responde con la tarjeta adaptable que tiene `Input.ChoiceSet` el componente .
1. El usuario A usa la búsqueda de encabezados de tipo para buscar y seleccionar la información en función de la elección del cliente.

En la imagen siguiente se muestra la experiencia móvil de la búsqueda de typeahead:

![Búsqueda de encabezado de tipo estático](~/assets/images/Cards/static-typeahead-search.gif)

---

> [!NOTE]
> No puede obtener experiencias de tarjeta enriquecidas con búsqueda dinámica, como extensiones de mensajes basadas en consultas.

## <a name="implement-typeahead-search"></a>Implementación de la búsqueda de typeahead

`Input.ChoiceSet` es uno de los componentes de entrada importantes en tarjetas adaptables. Puede agregar un control de búsqueda typeahead al `Input.ChoiceSet` componente para implementar la búsqueda de typeahead. Puede buscar y seleccionar la información necesaria con las siguientes selecciones:

* Lista desplegable, como la selección expandida.
* Botón de radio, como selección única.
* Casillas, como varias selecciones.

> [!NOTE]
> El `Input.ChoiceSet` control se basa en el estilo y `isMultiSelect` las propiedades.

### <a name="schema-properties"></a>Propiedades de esquema

Las propiedades siguientes son las nuevas adiciones al esquema para habilitar la [`Input.ChoiceSet`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) búsqueda de typeahead:

| Propiedad| Tipo | Necesario | Descripción |
|-----------|------|----------|-------------|
| style | Compact <br/> Expanded <br/> Filtered | No | Agrega estilo filtrado a la lista de validaciones admitidas para el tipo estático de avance.|
| choices.data | Data.Query | No | Habilita el tipo de avance dinámico como tipos de usuario, capturando un conjunto remoto de opciones de un back-end. |

### <a name="dataquery-definition"></a>Definición de Data.Query

| Propiedad| Tipo | Necesario | Descripción |
|-----------|------|----------|-------------|
| tipo | Data.Query | Sí | Especifica que es un objeto Data.Query.|
| Dataset | Cadena | Sí | Especifica el tipo de datos que se capturan dinámicamente. |
| value | Cadena | No | Rellena la solicitud de invocación al bot con la entrada que el usuario proporcionó a `ChoiceSet`. |
| count | Número | No | Rellena la solicitud de invocación al bot para especificar el número de elementos que se deben devolver. El bot lo omite si los usuarios quieren enviar una cantidad diferente. |
| skip | Número | No | Rellena la solicitud de invocación al bot para indicar que los usuarios quieren paginar y avanzar en la lista. |

### <a name="example"></a>Ejemplo

La carga útil de ejemplo que contiene la búsqueda de encabezados de tipo estática y dinámica con una sola & opciones de selección múltiple como se indica a continuación:

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

## <a name="code-snippets-for-invoke-request-and-response"></a>Fragmentos de código para invocar solicitud y respuesta

### <a name="invoke-request"></a>Invocar solicitud

```json
{
    "name": "application/search",
    "type": "invoke",
    "value": {
        "queryText": "fluentui",
        "queryOptions": {
            "skip": 0,
            "top": 15
        },
        "dataset": "npm"
    },
    "locale": "en-US",
    "localTimezone": "America/Los_Angeles",
    // …. other fields
}
```

### <a name="response"></a>Respuesta

#### <a name="c"></a>[C#](#tab/csharp)

```csharp
protected override async Task<InvokeResponse> OnInvokeActivityAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    if (turnContext.Activity.Name == "application/search")
    {
 var packages = new[] {
   new { title = "A very extensive set of extension methods", value = "FluentAssertions" },
   new { title = "Fluent UI Library", value = "FluentUI" }};

 var searchResponseData = new
 {
     type = "application/vnd.microsoft.search.searchResponse",
     value = new
     {
  results = packages
     }
 };
 var jsonString = JsonConvert.SerializeObject(searchResponseData);
 JObject jsonData = JObject.Parse(jsonString);
 return new InvokeResponse()
 {
     Status = 200,
     Body = jsonData
 };
    }

    return null;
}
```

#### <a name="nodejs"></a>[Node.js](#tab/nodejs)

```nodejs
  async onInvokeActivity(context) {
    if (context._activity.name == 'application/search') {
      // let searchQuery = context._activity.value.queryText;  // This can be used to filter the results
      var successResult = {
        status: 200,
        body: {
          "type": "application/vnd.microsoft.search.searchResponse",
          "value": {
            "results": [
              {
                "value": "FluentAssertions",
                "title": "A very extensive set of extension methods"
              },
              {
                "value": "FluentUI",
                "title": "Fluent UI Library"
              }
            ]
          }
        }
      }

      return successResult;

    }
  }
```

#### <a name="json"></a>[JSON](#tab/json)

```json
{
    "status": 200,
    "body" : {
        "type": "application/vnd.microsoft.search.searchResponse",
        "value": {
           "results": [
                {
                    "value": "FluentAssertions",
                    "title": "A very extensive set of extension methods."
                },
                {
                    "value": "FluentUI",
                    "title": "Fluent UI Library"
                }
            ]
        }
    }
}
```

---

## <a name="code-sample"></a>Ejemplo de código

|**Ejemplo de nombre** | **Descripción** | **C#** | **Node.js** |
|----------------|-----------------|--------------|----------------|
| Control de búsqueda de typeahead en tarjetas adaptables | En el ejemplo se muestran las características del control de búsqueda de typeahead estático y dinámico en tarjetas adaptables. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-type-ahead-search-adaptive-cards/csharp) | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-type-ahead-search-adaptive-cards/nodejs) |

## <a name="see-also"></a>Consulte también

* [Acciones universales para tarjetas adaptables](Universal-actions-for-adaptive-cards/Overview.md)
* [Módulos de tareas](../what-are-task-modules.md)

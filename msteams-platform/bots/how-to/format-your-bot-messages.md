---
title: Dar formato a los mensajes de bot
author: clearab
description: Agregar formato enriquecido a los mensajes de bot
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: a11d01233481371c66562e0fa27ab805b06e9391
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675855"
---
# <a name="format-your-bot-messages"></a>Dar formato a los mensajes de bot

Puede establecer la propiedad opcional [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) para controlar cómo se representa el contenido de texto del mensaje.

Microsoft Teams admite las siguientes opciones de formato:

| VALOR TextFormat | Descripción |
| --- | --- |
| Plain | El texto debe tratarse como texto sin formato sin aplicar ningún formato.|
| Markdown | El texto debe tratarse como formato Markdown y representarse en el canal según corresponda. *Vea* [dar formato al contenido del texto](#formatting-text-content) para los estilos admitidos. |
| XML | El texto es marcado XML simple. *Vea* [dar formato al contenido del texto](#formatting-text-content) para los estilos admitidos. |

## <a name="formatting-text-content"></a>Formato de contenido de texto

Microsoft Teams admite un subconjunto de las etiquetas de formato de Markdown y XML (HTML).

Actualmente, se aplican las siguientes limitaciones:

* Los mensajes de solo texto no admiten el formato de tabla.
* Las tarjetas enriquecidas admiten el formato solo en la propiedad de texto, no en las propiedades de título o de subtítulo.
* Las tarjetas enriquecidas no admiten el formato de tablas o de Markdown.

## <a name="cross-platform-support"></a>Compatibilidad entre plataformas

Para asegurarse de que el formato funciona en todas las plataformas compatibles con Microsoft Teams, tenga en cuenta que algunos estilos no se admiten actualmente en todas las plataformas.

| Style                     | Mensajes de solo texto | Tarjetas enriquecidas (solo XML) |
| ---                       | :---: | :---: |
| bold                      | ✔ | ✖ |
| italic                    | ✔ | ✔ |
| encabezado (niveles 1&ndash;3) | ✖ | ✔ |
| Aplique             | ✖ | ✔ |
| regla horizontal           | ✖ | ✖ |
| lista sin ordenar            | ✖ | ✔ |
| Lista ordenada              | ✖ | ✔ |
| texto con formato previo         | ✔ | ✔ |
| blockquote                | ✔ | ✔ |
| hipervínculo                 | ✔ | ✔ |
| vínculo de imagen                | ✔ | ✖ |

## <a name="support-by-individual-platform"></a>Soporte por plataforma individual

La compatibilidad con el formato del texto varía en función del tipo de mensaje y de la plataforma.

### <a name="text-only-messages"></a>Mensajes de solo texto

| Style                     | Desktop | iOS | Android |
| ---                       | :---: | :---: | :---: |
| bold                      | ✔ | ✔ | ✔ |
| italic                    | ✔ | ✔ | ✔ |
| encabezado (niveles 1&ndash;3) | ✖ | ✖ | ✖ |
| Aplique             | ✔ | ✔ | ✖ |
| regla horizontal           | ✖ | ✖ | ✖ |
| lista sin ordenar            | ✔ | ✖ | ✖ |
| Lista ordenada              | ✔ | ✖ | ✖ |
| texto con formato previo         | ✔ | ✔ | ✔ |
| blockquote                | ✔ | ✔ | ✔ |
| hipervínculo                 | ✔ | ✔ | ✔ |
| vínculo de imagen                | ✔ | ✔ | ✔ |

### <a name="cards"></a>Tarjetas

Vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md) para la compatibilidad en tarjetas.

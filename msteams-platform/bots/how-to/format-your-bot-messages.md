---
title: Formatear los mensajes del bot
author: surbhigupta
description: Agregar formato enriquecido a los mensajes del bot
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 56a34edee372cc6c5bcc5808015783f04867f141
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068987"
---
# <a name="format-your-bot-messages"></a>Formatear los mensajes del bot

El formato de mensaje le permite sacar lo mejor de los mensajes de bot. Puedes dar formato a los mensajes del bot para que incluyan tarjetas enriquecciones que sean datos adjuntos que contengan elementos interactivos, como botones, texto, imágenes, audio, vídeo, entre otros.

## <a name="format-text-content"></a>Dar formato al contenido de texto

Para dar formato a los mensajes de bot, puede establecer la propiedad opcional para controlar cómo se representa el contenido de texto del mensaje [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) de bot.

Microsoft Teams admite las siguientes opciones de formato:

| `TextFormat` value | Descripción |
| --- | --- |
| plain | El texto debe tratarse como texto sin formato aplicado.|
| markdown | El texto debe tratarse como formato markdown y representarse en el canal según corresponda. |
| xml | El texto es un marcado XML simple. |

Teams admite un subconjunto de etiquetas de markdown y de formato XML o HTML.

Actualmente, las siguientes limitaciones se aplican al formato:

* Los mensajes de solo texto no admiten el formato de tabla.
* Las tarjetas enriquecciones solo admiten el formato en la propiedad de texto, no en las propiedades de título o subtítulo.
* Las tarjetas enriquecciones no admiten markdown ni formato de tabla.

Después de dar formato al contenido de texto, asegúrese de que el formato funciona en todas las plataformas admitidas por Microsoft Teams.

## <a name="cross-platform-support"></a>Compatibilidad entre plataformas

Actualmente, algunos estilos no se admiten en todas las plataformas. En la tabla siguiente se proporciona una lista de estilos y cuáles de estos estilos se admiten en mensajes de solo texto y tarjetas enriquecciones:

| Estilo                     | Mensajes de solo texto | Tarjetas enriquecciones: solo XML |
| ---                       | :---: | :---: |
| Negrita                      | ✔ | ✖ |
| Italic                    | ✔ | ✔ |
| Encabezado (niveles 1 &ndash; 3) | ✖ | ✔ |
| Tachado             | ✖ | ✔ |
| Regla horizontal           | ✖ | ✖ |
| Lista no ordenada            | ✖ | ✔ |
| Lista ordenada              | ✖ | ✔ |
| Texto con formato previo         | ✔ | ✔ |
| Blockquote                | ✔ | ✔ |
| Hipervínculo                 | ✔ | ✔ |
| Vínculo imagen                | ✔ | ✖ |

Después de comprobar la compatibilidad entre plataformas, asegúrese de que la compatibilidad con plataformas individuales también esté disponible.

## <a name="support-by-individual-platform"></a>Compatibilidad con plataformas individuales

La compatibilidad con el formato de texto varía según el tipo de mensaje y la plataforma.

### <a name="text-only-messages"></a>Mensajes de solo texto

En la tabla siguiente se proporciona una lista de estilos y cuáles de estos estilos se admiten en escritorio, iOS y Android:

| Estilo                     | Escritorio | iOS | Android |
| ---                       | :---: | :---: | :---: |
| Negrita                      | ✔ | ✔ | ✔ |
| Italic                    | ✔ | ✔ | ✔ |
| Encabezado (niveles 1 &ndash; 3) | ✖ | ✖ | ✖ |
| Tachado             | ✔ | ✔ | ✖ |
| Regla horizontal           | ✖ | ✖ | ✖ |
| Lista no ordenada            | ✔ | ✖ | ✖ |
| Lista ordenada              | ✔ | ✖ | ✖ |
| Texto con formato previo         | ✔ | ✔ | ✔ |
| Blockquote                | ✔ | ✔ | ✔ |
| Hipervínculo                 | ✔ | ✔ | ✔ |
| Vínculo imagen                | ✔ | ✔ | ✔ |

### <a name="cards"></a>Tarjetas

Para obtener compatibilidad con tarjetas, consulte [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Actualizar y eliminar mensajes de bot](~/bots/how-to/update-and-delete-bot-messages.md)

---
title: Formatear los mensajes del bot
author: surbhigupta
description: En este módulo, aprenderá a agregar formato y estilos enriquecidos a los mensajes del bot, como tachado, lista ordenada y desordenada, hipervínculo, vínculo de imagen, etc.
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: ae803ecb4ae971731d68eba44d08ad9c8b3d274c
ms.sourcegitcommit: 0c734a5809ad6eb36255c97f38589c67d0971741
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2022
ms.locfileid: "66830802"
---
# <a name="format-your-bot-messages"></a>Formatear los mensajes del bot

El formato de mensajes le permite sacar lo mejor de los mensajes del bot. Puede dar formato a los mensajes del bot para incluir tarjetas enriquecidas como datos adjuntos que contienen elementos interactivos, como botones, texto, imágenes, audio, vídeo, etc.

## <a name="format-text-content"></a>Formato de contenido de texto

Para dar formato a los mensajes del bot, puede establecer la propiedad opcional [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) para controlar cómo se representa el contenido de texto del mensaje de bot.

Microsoft Teams admite las siguientes opciones de formato:

| Valor `TextFormat` | Descripción |
| --- | --- |
| normal | El texto debe tratarse como texto sin formato sin aplicar ningún formato.|
| markdown | El texto debe tratarse como formato markdown y representarse en el canal según corresponda. |
| xml | El texto es una revisión de XML simple. |

Teams admite un subconjunto de etiquetas de formato Markdown y XML o HTML.

Actualmente, se aplican las siguientes limitaciones al formato:

* Los mensajes de solo texto no admiten el formato de tabla.
* Las tarjetas enriquecidas solo admiten el formato en la propiedad de texto, no en las propiedades de título o subtítulo.
* Las tarjetas enriquecidas no admiten el formato markdown o table.

Después de dar formato al contenido de texto, asegúrese de que el formato funciona en todas las plataformas compatibles con Teams.

## <a name="cross-platform-support"></a>Compatibilidad multiplataforma.

Algunos estilos no se admiten actualmente en todas las plataformas. En la tabla siguiente se proporciona una lista de estilos y cuáles de estos estilos se admiten en mensajes de solo texto y tarjetas enriquecidas:

| Estilo                     | Mensajes de solo texto | Tarjetas enriquecidas: solo XML |
| ---                       | :---: | :---: |
| Negrita                      | ✔️️ | ❌ |
| Italic                    | ✔️ | ✔️ |
| Encabezado (niveles 1&ndash;3) | ❌ | ✔️ |
| Tachado             | ❌ | ✔️ |
| Regla horizontal           | ❌ | ❌ |
| Lista no ordenada            | ❌ | ✔️ |
| Lista ordenada              | ❌ | ✔️ |
| Texto con formato previo         | ✔️ | ✔️ |
| Blockquote                | ✔️ | ✔️ |
| Hyperlink                 | ✔️ | ✔️ |
| Vínculo de imagen                | ❌ | ❌ |

Después de comprobar la compatibilidad multiplataforma, asegúrese de que la compatibilidad con plataformas individuales también está disponible.

## <a name="support-by-individual-platform"></a>Compatibilidad con plataformas individuales

La compatibilidad con el formato de texto varía según el tipo de mensaje y la plataforma.

### <a name="text-only-messages"></a>Mensajes de solo texto

En la tabla siguiente se proporciona una lista de estilos, que se admiten en el escritorio, iOS y Android:

| Estilo                     | Escritorio | iOS | Android |
| ---                       | :---: | :---: | :---: |
| Negrita                      | ✔️ | ✔️ | ✔️ |
| Italic                    | ✔️ | ✔️ | ✔️ |
| Encabezado (niveles 1&ndash;3) | ❌ | ❌ | ❌ |
| Tachado             | ✔️ | ✔️ | ❌ |
| Regla horizontal           | ❌ | ❌ | ❌ |
| Lista no ordenada            | ✔️ | ❌ | ❌ |
| Lista ordenada              | ✔️ | ❌ | ❌ |
| Texto con formato previo         | ✔️ | ✔️ | ✔️ |
| Blockquote                | ✔️ | ✔️ | ✔️ |
| Hyperlink                 | ✔️ | ✔️ | ✔️ |
| Vínculo de imagen                | ❌ | ❌ | ❌ |

### <a name="cards"></a>Tarjetas

Para obtener compatibilidad con tarjetas, consulte [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Actualizar y eliminar mensajes de bot](~/bots/how-to/update-and-delete-bot-messages.md)

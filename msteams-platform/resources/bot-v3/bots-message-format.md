---
title: Formato de mensaje de bot
description: En este módulo, aprenderá los detalles del formato de los mensajes del bot.
ms.topic: reference
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: 9121573dfa6f5c7a96f04ed16bcb0d41de0b5c34
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143336"
---
# <a name="message-formatting-for-bots"></a>Formato de mensajes para bots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Puede establecer la propiedad opcional [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) para controlar cómo se representa el contenido de texto del mensaje.

Microsoft Teams admite las siguientes opciones de formato:

| Valor de TextFormat | Descripción |
| --- | --- |
| normal | El texto debe tratarse como texto sin formato sin aplicar ningún formato. |
| markdown | El texto debe tratarse como formato Markdown y representarse en el canal según corresponda; vea [Dar formato al contenido de texto](#formatting-text-content) para los estilos admitidos. |
| xml | El texto es un marcado XML simple; vea [Dar formato al contenido de texto](#formatting-text-content) para los estilos admitidos. |

## <a name="formatting-text-content"></a>Dar formato al contenido del texto

Microsoft Teams admite un subconjunto de etiquetas de formato Markdown y XML (HTML).

Actualmente, se aplican las limitaciones siguientes:

* Los mensajes de solo texto no admiten el formato de tabla.
* Las tarjetas enriquecidas solo admiten el formato en la propiedad de texto, no en las propiedades de título o subtítulo.
* Las tarjetas enriquecidas no admiten markdown ni formato de tabla.

## <a name="cross-platform-support"></a>Compatibilidad multiplataforma.

Para asegurarse de que el formato funciona en todas las plataformas admitidas por Microsoft Teams, tenga en cuenta que algunos estilos no se admiten actualmente en todas las plataformas.

| Estilo                     | Mensajes de solo texto | Tarjetas enriquecidas (solo XML) |
| ---                       | :---: | :---: |
| bold                      | ✔️️ | ❌ |
| italic                    | ✔️ | ✔️ |
| encabezado (niveles 1&ndash;3) | ❌ | ✔️ |
| Tachado             | ❌ | ✔️ |
| regla horizontal           | ❌ | ❌ |
| lista desordenada            | ❌ | ✔️ |
| lista ordenada              | ❌ | ✔️ |
| texto con formato previo         | ✔️ | ✔️ |
| blockquote                | ✔️ | ✔️ |
| hipervínculo                 | ✔️ | ✔️ |
| vínculo de imagen                | ✔️ | ❌ |

## <a name="support-by-individual-platform"></a>Compatibilidad con plataformas individuales

La compatibilidad con el formato de texto varía según el tipo de mensaje y por plataforma.

### <a name="text-only-messages"></a>Mensajes de solo texto

| Estilo                     | Escritorio | iOS | Android |
| ---                       | :---: | :---: | :---: |
| bold                      | ✔️ | ✔️ | ✔️ |
| italic                    | ✔️ | ✔️ | ✔️ |
| encabezado (niveles 1&ndash;3) | ❌ | ❌ | ❌ |
| Tachado             | ✔️ | ✔️ | ❌ |
| regla horizontal           | ❌ | ❌ | ❌ |
| lista desordenada            | ✔️ | ❌ | ❌ |
| lista ordenada              | ✔️ | ❌ | ❌ |
| texto con formato previo         | ✔️ | ✔️ | ✔️ |
| blockquote                | ✔️ | ✔️ | ✔️ |
| hipervínculo                 | ✔️ | ✔️ | ✔️ |
| vínculo de imagen                | ✔️ | ✔️ | ✔️ |

### <a name="cards"></a>Tarjetas

Para obtener más información, vea [Formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md) para obtener soporte técnico en tarjetas.

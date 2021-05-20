---
title: Formato de mensaje bot
description: Describe los detalles del formato de los mensajes de bot
keywords: escenarios de equipos canaliza el mensaje del bot de conversación
ms.topic: reference
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: a9566331b259ba77f6770ff6394e8a788769af5d
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566477"
---
# <a name="message-formatting-for-bots"></a>Formato de mensaje para bots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Puede establecer la propiedad opcional [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) para controlar cómo se representa el contenido de texto del mensaje.

Microsoft Teams admite las siguientes opciones de formato:

| Valor TextFormat | Descripción |
| --- | --- |
| llanura | El texto debe tratarse como texto sin formato sin formato aplicado en absoluto. |
| markdown | El texto debe tratarse como formato markdown y representarse en el canal según corresponda; consulte [Formato del contenido de texto](#formatting-text-content) para los estilos admitidos. |
| XML | El texto es un marcado XML simple; consulte [Formato del contenido de texto](#formatting-text-content) para los estilos admitidos. |

## <a name="formatting-text-content"></a>Formato de contenido de texto

Microsoft Teams admite un subconjunto de etiquetas de formato Markdown y XML (HTML).

Actualmente, se aplican las siguientes limitaciones:

* Los mensajes de solo texto no admiten el formato de tabla.
* Las tarjetas enriquecidas solo admiten el formato en la propiedad de texto, no en las propiedades title o subtitle.
* Las tarjetas enriquecidas no admiten el formato Markdown o table.

## <a name="cross-platform-support"></a>Soporte multiplataforma

Para asegurarse de que el formato funciona en todas las plataformas compatibles con Microsoft Teams, tenga en cuenta que algunos estilos no son compatibles actualmente en todas las plataformas.

| Estilo                     | Mensajes solo de texto | Tarjetas enriquecidas (solo XML) |
| ---                       | :---: | :---: |
| bold                      | ✔ | ✖ |
| italic                    | ✔ | ✔ |
| encabezado (niveles 1 &ndash; 3) | ✖ | ✔ |
| tachado             | ✖ | ✔ |
| regla horizontal           | ✖ | ✖ |
| lista desordenada            | ✖ | ✔ |
| lista ordenada              | ✖ | ✔ |
| texto preformateado         | ✔ | ✔ |
| blockquote                | ✔ | ✔ |
| hipervínculo                 | ✔ | ✔ |
| enlace de imagen                | ✔ | ✖ |

## <a name="support-by-individual-platform"></a>Apoyo por plataforma individual

La compatibilidad con el formato de texto varía según el tipo de mensaje y por plataforma.

### <a name="text-only-messages"></a>Mensajes solo de texto

| Estilo                     | Desktop | iOS | Android |
| ---                       | :---: | :---: | :---: |
| bold                      | ✔ | ✔ | ✔ |
| italic                    | ✔ | ✔ | ✔ |
| encabezado (niveles 1 &ndash; 3) | ✖ | ✖ | ✖ |
| tachado             | ✔ | ✔ | ✖ |
| regla horizontal           | ✖ | ✖ | ✖ |
| lista desordenada            | ✔ | ✖ | ✖ |
| lista ordenada              | ✔ | ✖ | ✖ |
| texto preformateado         | ✔ | ✔ | ✔ |
| blockquote                | ✔ | ✔ | ✔ |
| hipervínculo                 | ✔ | ✔ | ✔ |
| enlace de imagen                | ✔ | ✔ | ✔ |

### <a name="cards"></a>Tarjetas

Para obtener más información, consulte [Formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md) para obtener soporte técnico en tarjetas.

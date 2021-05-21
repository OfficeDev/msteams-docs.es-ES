---
title: Formato de mensaje bot
description: Describe los detalles del formato de los mensajes de bot
keywords: Escenarios de teams canaliza el mensaje del bot de conversación
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

Puede establecer la propiedad opcional para controlar cómo se representa el contenido de texto [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) del mensaje.

Microsoft Teams admite las siguientes opciones de formato:

| Valor TextFormat | Descripción |
| --- | --- |
| plain | El texto debe tratarse como texto sin formato aplicado en absoluto. |
| markdown | El texto debe tratarse como formato Markdown y representarse en el canal según corresponda; vea [Formatting text content for](#formatting-text-content) supported styles. |
| xml | El texto es un marcado XML simple; vea [Formatting text content for](#formatting-text-content) supported styles. |

## <a name="formatting-text-content"></a>Formato del contenido de texto

Microsoft Teams admite un subconjunto de etiquetas de formato Markdown y XML (HTML).

Actualmente, se aplican las siguientes limitaciones:

* Los mensajes de solo texto no admiten el formato de tabla.
* Las tarjetas enriquecciones solo admiten el formato en la propiedad de texto, no en las propiedades de título o subtítulo.
* Las tarjetas enriquecciones no admiten Markdown ni el formato de tabla.

## <a name="cross-platform-support"></a>Compatibilidad entre plataformas

Para asegurarse de que el formato funciona en todas las plataformas admitidas por Microsoft Teams, tenga en cuenta que algunos estilos no se admiten actualmente en todas las plataformas.

| Estilo                     | Mensajes de solo texto | Tarjetas enriquecciones (solo XML) |
| ---                       | :---: | :---: |
| bold                      | ✔ | ✖ |
| italic                    | ✔ | ✔ |
| encabezado (niveles 1 &ndash; 3) | ✖ | ✔ |
| strikethrough             | ✖ | ✔ |
| regla horizontal           | ✖ | ✖ |
| lista sin ordenar            | ✖ | ✔ |
| lista ordenada              | ✖ | ✔ |
| texto con formato previo         | ✔ | ✔ |
| blockquote                | ✔ | ✔ |
| hipervínculo                 | ✔ | ✔ |
| vínculo de imagen                | ✔ | ✖ |

## <a name="support-by-individual-platform"></a>Compatibilidad con plataformas individuales

La compatibilidad con el formato de texto varía según el tipo de mensaje y por plataforma.

### <a name="text-only-messages"></a>Mensajes de solo texto

| Estilo                     | Desktop | iOS | Android |
| ---                       | :---: | :---: | :---: |
| bold                      | ✔ | ✔ | ✔ |
| italic                    | ✔ | ✔ | ✔ |
| encabezado (niveles 1 &ndash; 3) | ✖ | ✖ | ✖ |
| strikethrough             | ✔ | ✔ | ✖ |
| regla horizontal           | ✖ | ✖ | ✖ |
| lista sin ordenar            | ✔ | ✖ | ✖ |
| lista ordenada              | ✔ | ✖ | ✖ |
| texto con formato previo         | ✔ | ✔ | ✔ |
| blockquote                | ✔ | ✔ | ✔ |
| hipervínculo                 | ✔ | ✔ | ✔ |
| vínculo de imagen                | ✔ | ✔ | ✔ |

### <a name="cards"></a>Tarjetas

Para obtener más información, consulte [Formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md) para obtener soporte técnico en tarjetas.

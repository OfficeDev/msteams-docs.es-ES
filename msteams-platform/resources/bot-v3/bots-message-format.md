---
title: Formato de mensaje de bot
description: Describe los detalles de formato de los mensajes de bot
keywords: mensaje de robot de conversación de canales de escenarios de Teams
ms.date: 05/20/2019
ms.openlocfilehash: eb0d0303d2b414ff84beab73055be5f057fff11c
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676192"
---
# <a name="message-formatting-for-bots"></a>Formato de mensajes para bots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Puede establecer la propiedad opcional [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) para controlar cómo se representa el contenido de texto del mensaje.

Microsoft Teams admite las siguientes opciones de formato:

| VALOR TextFormat | Descripción |
| --- | --- |
| Plain | El texto debe tratarse como texto sin procesar sin aplicar ningún formato |
| Markdown | El texto debe tratarse como formato Markdown y representarse en el canal según corresponda; vea [dar formato al contenido de texto](#formatting-text-content) para estilos compatibles |
| XML | El texto es marcado XML sencillo; vea [dar formato al contenido de texto](#formatting-text-content) para estilos compatibles |

## <a name="formatting-text-content"></a>Formato de contenido de texto

Microsoft Teams admite un subconjunto de las etiquetas de formato de Markdown y XML (HTML).

Actualmente, se aplican las siguientes limitaciones:

* Los mensajes de solo texto no admiten el formato de tabla
* Las tarjetas enriquecidas admiten el formato solo en la propiedad de texto, no en las propiedades título o subtítulo
* Las tarjetas enriquecidas no admiten el formato de tablas o de Markdown

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

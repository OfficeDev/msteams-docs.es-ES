---
title: Formato de texto compatible en conversaciones
description: Describe la compatibilidad con el formato de texto en las conversaciones con bots
keywords: bots conversaciones mensajes
ms.topic: how-to
localization_priority: Normal
ms.date: 03/29/2018
ms.openlocfilehash: dfb91e18a2ad895ae5b48c905046a22449304fc6
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566750"
---
# <a name="formatting-bot-messages"></a>Dar formato a los mensajes de bots

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

* Los mensajes solo de texto no admiten el formato de tabla

Para obtener información sobre el formato en tarjetas, consulte [referencia de tarjeta Teams](~/task-modules-and-cards/cards/cards-reference.md).

### <a name="cross-platform-support"></a>Soporte multiplataforma

Para asegurarse de que el formato funciona en todas las plataformas compatibles con Microsoft Teams, tenga en cuenta que algunos estilos no son compatibles actualmente en todas las plataformas.

| Estilo                     | Mensajes solo de texto | Tarjetas (solo XML) |
|---------------------------|--------------------|------------------|
| bold                      | ✔                  | ✖                |
| italic                    | ✔                  | ✔                |
| encabezado (niveles 1 &ndash; 3) | ✖                  | ✔                |
| tachado             | ✖                  | ✔                |
| regla horizontal           | ✖                  | ✖                |
| lista desordenada            | ✖                  | ✔                |
| lista ordenada              | ✖                  | ✔                |
| texto preformateado         | ✔                  | ✔                |
| blockquote                | ✔                  | ✔                |
| hipervínculo                 | ✔                  | ✔                |
| enlace de imagen                | ✔                  | ✖                |

### <a name="support-by-individual-platform"></a>Apoyo por plataforma individual

La compatibilidad con el formato de texto varía según el tipo de mensaje y por plataforma.

#### <a name="text-only-messages"></a>Mensajes solo de texto

| Estilo                     | Desktop | iOS | Android |
|---------------------------|---------|-----|---------|
| bold                      | ✔       | ✔   | ✔       |
| italic                    | ✔       | ✔   | ✔       |
| encabezado (niveles 1 &ndash; 3) | ✖       | ✖   | ✖       |
| tachado             | ✔       | ✔   | ✖       |
| regla horizontal           | ✖       | ✖   | ✖       |
| lista desordenada            | ✔       | ✖   | ✖       |
| lista ordenada              | ✔       | ✖   | ✖       |
| texto preformateado         | ✔       | ✔   | ✔       |
| blockquote                | ✔       | ✔   | ✔       |
| hipervínculo                 | ✔       | ✔   | ✔       |
| enlace de imagen                | ✔       | ✔   | ✔       |

### <a name="examples-of-text-formatting"></a>Ejemplos de formato de texto

| Estilo | Ejemplo | Markdown | XML (HTML) |
| --- | --- | --- | --- |
| bold | **text** | `**text**` | `<strong>text</strong>` |
| italic | *text* | `*text*` | `<em>text</em>` |
| encabezado (niveles 1 &ndash; 3) | **Texto** | `### Text` | `<h3>Text</h3>` |
| tachado | ~~text~~ | `~~text~~` | `<strike>text</strike>` |
| lista desordenada | <ul><li>text</li><li>text</li></ul> | `* text`<br>`* text` | `<ul><li>text</li><li>text</li></ul>` |
| lista ordenada | <ol><li>text</li><li>text</li></ol> | `1. text`<br>`2. text` | `<ol><li>text</li><li>text</li></ol>` |
| texto preformateado | `text` | `` `text` `` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `>text` | `<blockquote>text</blockquote>` |
| hipervínculo | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` | `<a href="https://www.bing.com/">Bing</a>` |
| enlace de imagen | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `![Duck on a rock](http://aka.ms/Fo983c)` | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

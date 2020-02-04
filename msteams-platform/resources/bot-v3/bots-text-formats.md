---
title: Formato de texto compatible en conversaciones
description: Describe la compatibilidad de formato de texto en conversaciones de bot
keywords: mensajería de conversaciones de bots
ms.date: 03/29/2018
ms.openlocfilehash: cc6cba697a1f6907bfb13b94740e7bf9e92596da
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675741"
---
# <a name="formatting-bot-messages"></a>Mensajes de robot de formato

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Puede establecer la propiedad opcional [`TextFormat`](https://docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) para controlar cómo se representa el contenido de texto del mensaje.

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

Para obtener información sobre el formato en las tarjetas, consulte la referencia de la [tarjeta de Teams](~/task-modules-and-cards/cards/cards-reference.md).

### <a name="cross-platform-support"></a>Compatibilidad entre plataformas

Para asegurarse de que el formato funciona en todas las plataformas compatibles con Microsoft Teams, tenga en cuenta que algunos estilos no se admiten actualmente en todas las plataformas.

| Style                     | Mensajes de solo texto | Tarjetas (solo XML) |
|---------------------------|--------------------|------------------|
| bold                      | ✔                  | ✖                |
| italic                    | ✔                  | ✔                |
| encabezado (niveles 1&ndash;3) | ✖                  | ✔                |
| Aplique             | ✖                  | ✔                |
| regla horizontal           | ✖                  | ✖                |
| lista sin ordenar            | ✖                  | ✔                |
| Lista ordenada              | ✖                  | ✔                |
| texto con formato previo         | ✔                  | ✔                |
| blockquote                | ✔                  | ✔                |
| hipervínculo                 | ✔                  | ✔                |
| vínculo de imagen                | ✔                  | ✖                |

### <a name="support-by-individual-platform"></a>Soporte por plataforma individual

La compatibilidad con el formato del texto varía en función del tipo de mensaje y de la plataforma.

#### <a name="text-only-messages"></a>Mensajes de solo texto

| Style                     | Desktop | iOS | Android |
|---------------------------|---------|-----|---------|
| bold                      | ✔       | ✔   | ✔       |
| italic                    | ✔       | ✔   | ✔       |
| encabezado (niveles 1&ndash;3) | ✖       | ✖   | ✖       |
| Aplique             | ✔       | ✔   | ✖       |
| regla horizontal           | ✖       | ✖   | ✖       |
| lista sin ordenar            | ✔       | ✖   | ✖       |
| Lista ordenada              | ✔       | ✖   | ✖       |
| texto con formato previo         | ✔       | ✔   | ✔       |
| blockquote                | ✔       | ✔   | ✔       |
| hipervínculo                 | ✔       | ✔   | ✔       |
| vínculo de imagen                | ✔       | ✔   | ✔       |

### <a name="examples-of-text-formatting"></a>Ejemplos de formato de texto

| Style | Ejemplo | Markdown | XML (HTML) |
| --- | --- | --- | --- |
| bold | **text** | `**text**` | `<strong>text</strong>` |
| italic | *text* | `*text*` | `<em>text</em>` |
| encabezado (niveles 1&ndash;3) | **Text** | `### Text` | `<h3>Text</h3>` |
| Aplique | ~~text~~ | `~~text~~` | `<strike>text</strike>` |
| lista sin ordenar | <ul><li>text</li><li>text</li></ul> | `* text`<br>`* text` | `<ul><li>text</li><li>text</li></ul>` |
| Lista ordenada | <ol><li>text</li><li>text</li></ol> | `1. text`<br>`2. text` | `<ol><li>text</li><li>text</li></ol>` |
| texto con formato previo | `text` | `` `text` `` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `>text` | `<blockquote>text</blockquote>` |
| hipervínculo | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` | `<a href="https://www.bing.com/">Bing</a>` |
| vínculo de imagen | <img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img> | `![Duck on a rock](http://aka.ms/Fo983c)` | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

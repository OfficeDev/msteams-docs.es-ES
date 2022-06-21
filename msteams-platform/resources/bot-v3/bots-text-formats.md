---
title: Formato de texto admitido en las conversaciones
description: En este módulo, obtendrá información sobre la compatibilidad con el formato de texto en las conversaciones del bot y el formato del contenido de texto en Microsoft Teams
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 03/29/2018
ms.openlocfilehash: 0aea1472a323c0161567c4661c02956568cb2187
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189729"
---
# <a name="formatting-bot-messages"></a>Dar formato a los mensajes de bots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Puede establecer la propiedad opcional [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) para controlar cómo se representa el contenido de texto del mensaje.

Microsoft Teams admite las siguientes opciones de formato:

| Valor de TextFormat | Descripción |
| --- | --- |
| normal | El texto debe tratarse como texto sin formato sin aplicar ningún formato. |
| markdown | El texto debe tratarse como formato Markdown y representarse en el canal según corresponda; vea [Dar formato al contenido de texto](#formatting-text-content) para los estilos admitidos. |
| xml | El texto es un marcado XML simple; vea [Dar formato al contenido de texto](#formatting-text-content) para los estilos admitidos. |

## <a name="formatting-text-content"></a>Dar formato al contenido del texto

Teams admite un subconjunto de etiquetas de formato Markdown y XML (HTML).

Actualmente, se aplican las limitaciones siguientes:
* Los mensajes de solo texto no admiten el formato de tabla.

Para obtener información sobre el formato de las tarjetas, consulte [Teams Referencia de tarjeta](~/task-modules-and-cards/cards/cards-reference.md).

### <a name="cross-platform-support"></a>Compatibilidad multiplataforma.

Para asegurarse de que el formato funciona en todas las plataformas admitidas por Teams, tenga en cuenta que algunos estilos no se admiten actualmente en todas las plataformas.

| Estilo                     | Mensajes de solo texto | Tarjetas (solo XML) |
|---------------------------|--------------------|------------------|
| bold                      | ✔                  | ✖                |
| italic                    | ✔                  | ✔                |
| encabezado (niveles 1&ndash;3) | ✖                  | ✔                |
| Tachado             | ✖                  | ✔                |
| regla horizontal           | ✖                  | ✖                |
| lista desordenada            | ✖                  | ✔                |
| lista ordenada              | ✖                  | ✔                |
| texto con formato previo         | ✔                  | ✔                |
| blockquote                | ✔                  | ✔                |
| hipervínculo                 | ✔                  | ✔                |
| vínculo de imagen                | ✔                  | ✖                |

### <a name="support-by-individual-platform"></a>Compatibilidad con plataformas individuales

La compatibilidad con el formato de texto varía según el tipo de mensaje y por plataforma.

#### <a name="text-only-messages"></a>Mensajes de solo texto

| Estilo                     | Escritorio | iOS | Android |
|---------------------------|---------|-----|---------|
| bold                      | ✔       | ✔   | ✔       |
| italic                    | ✔       | ✔   | ✔       |
| encabezado (niveles 1&ndash;3) | ✖       | ✖   | ✖       |
| Tachado             | ✔       | ✔   | ✖       |
| regla horizontal           | ✖       | ✖   | ✖       |
| lista desordenada            | ✔       | ✖   | ✖       |
| lista ordenada              | ✔       | ✖   | ✖       |
| texto con formato previo         | ✔       | ✔   | ✔       |
| blockquote                | ✔       | ✔   | ✔       |
| hipervínculo                 | ✔       | ✔   | ✔       |
| vínculo de imagen                | ✔       | ✔   | ✔       |

### <a name="examples-of-text-formatting"></a>Ejemplos de formato de texto

| Estilo | Ejemplo | Markdown | XML (HTML) |
| --- | --- | --- | --- |
| bold | **text** | `**text**` | `<strong>text</strong>` |
| italic | *text* | `*text*` | `<em>text</em>` |
| encabezado (niveles 1&ndash;3) | **Texto** | `### Text` | `<h3>Text</h3>` |
| Tachado | ~~text~~ | `~~text~~` | `<strike>text</strike>` |
| lista desordenada | <ul><li>text</li><li>text</li></ul> | `* text`<br>`* text` | `<ul><li>text</li><li>text</li></ul>` |
| lista ordenada | <ol><li>text</li><li>text</li></ol> | `1. text`<br>`2. text` | `<ol><li>text</li><li>text</li></ol>` |
| texto con formato previo | `text` | `` `text` `` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `>text` | `<blockquote>text</blockquote>` |
| hipervínculo | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` | `<a href="https://www.bing.com/">Bing</a>` |
| vínculo de imagen | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `![Duck on a rock](http://aka.ms/Fo983c)` | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

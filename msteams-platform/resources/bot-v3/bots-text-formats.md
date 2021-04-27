---
title: Formato de texto admitido en conversaciones
description: Describe la compatibilidad con formato de texto en conversaciones de bots
keywords: mensajes de conversaciones de bots
ms.topic: how-to
localization_priority: Normal
ms.date: 03/29/2018
ms.openlocfilehash: 9e89e1171907929eebb9f9eb3809f4ab920583a4
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019751"
---
# <a name="formatting-bot-messages"></a>Dar formato a los mensajes de bots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Puede establecer la propiedad opcional para controlar cómo se representa el contenido de texto [`TextFormat`](https://docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) del mensaje.

Microsoft Teams admite las siguientes opciones de formato:

| Valor TextFormat | Descripción |
| --- | --- |
| plain | El texto debe tratarse como texto sin formato aplicado en absoluto |
| markdown | El texto debe tratarse como formato Markdown y representarse en el canal según corresponda; vea [Formatting text content for](#formatting-text-content) supported styles |
| xml | El texto es un marcado XML simple; vea [Formatting text content for](#formatting-text-content) supported styles |

## <a name="formatting-text-content"></a>Formato del contenido de texto

Microsoft Teams admite un subconjunto de etiquetas de formato Markdown y XML (HTML).

Actualmente, se aplican las siguientes limitaciones:

* Los mensajes de solo texto no admiten formato de tabla

Para obtener información sobre el formato de las tarjetas, vea [la referencia de tarjeta de Teams](~/task-modules-and-cards/cards/cards-reference.md).

### <a name="cross-platform-support"></a>Compatibilidad entre plataformas

Para asegurarse de que el formato funciona en todas las plataformas admitidas por Microsoft Teams, tenga en cuenta que algunos estilos no se admiten actualmente en todas las plataformas.

| Estilo                     | Mensajes de solo texto | Tarjetas (solo XML) |
|---------------------------|--------------------|------------------|
| bold                      | ✔                  | ✖                |
| italic                    | ✔                  | ✔                |
| encabezado (niveles 1 &ndash; 3) | ✖                  | ✔                |
| strikethrough             | ✖                  | ✔                |
| regla horizontal           | ✖                  | ✖                |
| lista sin ordenar            | ✖                  | ✔                |
| lista ordenada              | ✖                  | ✔                |
| texto con formato previo         | ✔                  | ✔                |
| blockquote                | ✔                  | ✔                |
| hipervínculo                 | ✔                  | ✔                |
| vínculo de imagen                | ✔                  | ✖                |

### <a name="support-by-individual-platform"></a>Compatibilidad con plataformas individuales

La compatibilidad con el formato de texto varía según el tipo de mensaje y por plataforma.

#### <a name="text-only-messages"></a>Mensajes de solo texto

| Estilo                     | Desktop | iOS | Android |
|---------------------------|---------|-----|---------|
| bold                      | ✔       | ✔   | ✔       |
| italic                    | ✔       | ✔   | ✔       |
| encabezado (niveles 1 &ndash; 3) | ✖       | ✖   | ✖       |
| strikethrough             | ✔       | ✔   | ✖       |
| regla horizontal           | ✖       | ✖   | ✖       |
| lista sin ordenar            | ✔       | ✖   | ✖       |
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
| encabezado (niveles 1 &ndash; 3) | **Text** | `### Text` | `<h3>Text</h3>` |
| strikethrough | ~~text~~ | `~~text~~` | `<strike>text</strike>` |
| lista sin ordenar | <ul><li>text</li><li>text</li></ul> | `* text`<br>`* text` | `<ul><li>text</li><li>text</li></ul>` |
| lista ordenada | <ol><li>text</li><li>text</li></ol> | `1. text`<br>`2. text` | `<ol><li>text</li><li>text</li></ol>` |
| texto con formato previo | `text` | `` `text` `` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `>text` | `<blockquote>text</blockquote>` |
| hipervínculo | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` | `<a href="https://www.bing.com/">Bing</a>` |
| vínculo de imagen | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `![Duck on a rock](http://aka.ms/Fo983c)` | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

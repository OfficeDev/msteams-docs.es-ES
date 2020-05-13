---
title: Formato del texto en las tarjetas
description: Describe el formato del texto de las tarjetas en Microsoft Teams
keywords: formato de las tarjetas de bots de Microsoft Teams
ms.date: 03/29/2018
ms.openlocfilehash: e857a1250593c135aa23ad38a571a5561bb91431
ms.sourcegitcommit: b9e8839858ea8e9e33fe5e20e14bbe86c75fd510
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/12/2020
ms.locfileid: "44210690"
---
# <a name="format-cards-in-teams"></a>Formato de tarjetas en Microsoft Teams

Puede Agregar formato de texto enriquecido a las tarjetas con Markdown o HTML, según el tipo de tarjeta.

Las tarjetas admiten el formato solo en la propiedad de texto, no en las propiedades de título o de subtítulo. El formato se puede especificar mediante un subconjunto de formato XML (HTML) o Markdown, según el tipo de tarjeta. Para las tarjetas adaptables actuales y futuras del desarrollo, se recomienda usar el formato Markdown.

La compatibilidad de formato es distinta entre los distintos tipos de tarjetas y la representación de la tarjeta puede variar ligeramente entre el escritorio y los clientes de los equipos móviles, así como los equipos en el explorador de escritorio.

Puede incluir una imagen incorporada en cualquier tarjeta de Teams. Imágenes a las que se les da formato `.png` , `.jpg` o `.gif` archivos y no deben exceder de 1024 × 1024 PX o 1 MB. GIF animado no es compatible oficialmente. *Consulte* [referencia de tarjetas](./cards-reference.md#inline-card-images)

## <a name="formatting-cards-with-markdown"></a>Tarjetas de formato con Markdown

Hay dos tipos de tarjetas que admiten Markdown en Microsoft Teams:

> [!div class="checklist"]
> * **Tarjetas adaptables**: Markdown se admite en el campo tarjeta adaptable `Textblock` , así como en `Fact.Title` y `Fact.Value` . No se admite HTML en tarjetas adaptables.
> * **Tarjetas de conector de O365**: MARKDOWN y HTML limitado son compatibles con las tarjetas de conector de Office 365 en los campos de texto.

# <a name="markdown-formatting-adaptive-cards"></a>[**Formato de Markdown: tarjetas adaptables**](#tab/adaptive-md)

 Los estilos admitidos `Textblock` para `Fact.Title` y `Fact.Value` son:

| Style | Ejemplo | Markdown |
| --- | --- | --- |
| bold | **Bold** | ```**Bold**``` |
| italic | _Italic_ | ```_Italic_``` |
| lista sin ordenar | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| Lista ordenada | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Hyperlinks |[Bing](https://www.bing.com/)| ```[Title](url)``` |

No se admiten las siguientes etiquetas Markdown:

* Encabezados
* Tablas
* Imágenes
* Texto con formato previo
* Blockquotes

> [!IMPORTANT]
> Las tarjetas adaptables no admiten el formato HTML.

### <a name="newlines-for-adaptive-cards"></a>Nuevas líneas para tarjetas adaptables

En las listas puede usar las `\r` `\n` secuencias de escape o de para las nuevas líneas. Usar `\n\n` en una lista hará que se aplique sangría al siguiente elemento de la lista. Si necesita más líneas en cualquier lugar del TextBlock, use `\n\n` .

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>Diferencias de escritorio y móviles para tarjetas adaptables

El formato es ligeramente distinto entre el escritorio y las versiones móviles de Teams.

En el escritorio, el formato de Markdown con tarjeta adaptable aparece como este en los exploradores Web y en la aplicación cliente de Teams:

![Formato Markdown de tarjeta adaptable en el cliente de escritorio](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

En iOS, el formato de Markdown con tarjeta adaptable tiene este aspecto:

![Formato Markdown de tarjeta adaptable en iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

En Android, el formato de Markdown con tarjeta adaptable tiene este aspecto:

![Formato Markdown de tarjeta adaptable en Android](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a>Más información sobre tarjetas adaptables

[Características de texto en tarjetas adaptables](/adaptive-cards/create/textfeatures) La fecha y las características de localización mencionadas en este tema no se admiten en Microsoft Teams.

### <a name="formatting-sample-for-adaptive-cards"></a>Ejemplo de formato para tarjetas adaptables

``` json
{
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
        {
            "type": "TextBlock",
            "text": "This is some **bold** text"
        },
        {
            "type": "TextBlock",
            "text": "This is some _italic_ text"
        },
        {
            "type": "TextBlock",
            "text": "- Bullet \r- List \r",
            "wrap": true
        },
        {
            "type": "TextBlock",
            "text": "1. Numbered\r2. List\r",
            "wrap": true
        },
        {
            "type": "TextBlock",
            "text": "Check out [Adaptive Cards](http://adaptivecards.io)"
        }
    ]
}
```

### <a name="mention-support-within-adaptive-cards-v12"></a>Mencione la compatibilidad en las tarjetas adaptables v 1.2

Las menciones basadas en tarjetas se admiten en clientes Web, de escritorio y móviles. Puede Agregar @ menciones en un cuerpo de tarjeta adaptable para bots y respuestas de extensiones de mensajería.  Para agregar @ menciones en las tarjetas, siga la misma lógica de notificación y representación que la de las [menciones basadas en mensajes en conversaciones de chat en el canal y en el grupo](../../bots/how-to/conversations/channel-and-group-conversations.md#working-with-mentions ).

Los bots y las extensiones de mensajería pueden incluir menciones dentro del contenido de la tarjeta en elementos [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) y [FactSet](https://adaptivecards.io/explorer/FactSet.html) .

> [!NOTE]
>Actualmente, [los elementos multimedia](https://adaptivecards.io/explorer/Media.html) no se admiten en las tarjetas adaptables v 1.2 en la plataforma de Microsoft Teams.

### <a name="constructing-mentions"></a>Creación de menciones

Para incluir una mención en una tarjeta adaptable, la aplicación debe incluir los siguientes elementos:

* `<at>username</at>`en los elementos de tarjeta adaptable admitidos
* El `mention` objeto dentro de una `msteams` propiedad en el contenido de la tarjeta, que incluye el identificador de usuario de Teams del usuario que se está mencionando

### <a name="sample-adaptive-card-with-a-mention"></a>Ejemplo de tarjeta adaptable con mención

``` json
{
  "contentType": "application/vnd.microsoft.card.adaptive",
  "content": {
    "type": "AdaptiveCard",
    "body": [
      {
        "type": "TextBlock",
        "text": "Hi <at>John Doe</at>"
      }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.0",
    "msteams": {
      "entities": [
        {
          "type": "mention",
          "text": "<at>John Doe</at>",
          "mentioned": {
            "id": "29:123124124124",
            "name": "John Doe"
          }
        }
      ]
    }
  }
}
```

# <a name="markdown-formatting-o365-connector-cards"></a>[**Formato de Markdown: tarjetas conector de O365**](#tab/connector-md)

Las tarjetas de conector admiten el formato HTML y Markdown limitados. La compatibilidad con HTML se describe en la última sección.

| Style | Ejemplo | Markdown |
| --- | --- | --- |
| bold | **text** | `**text**` |
| italic | *text* | `*text*` |
| encabezado (niveles 1 &ndash; 3) | **Text** | `### Text`|
| Aplique | ~~text~~ | `~~text~~` |
| lista sin ordenar | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| Lista ordenada | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| texto con formato previo | `text` | ``preformatted text`` |
| blockquote | Texto de >blockquote | `>blockquote text` |
| hipervínculo | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| vínculo de imagen |![Pato en una Rock](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

En las tarjetas conector, las líneas nuevas se representan para `\n\n` , pero no para `\n` o `\r` .

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a>Diferencias de escritorio y móviles para tarjetas de conector con Markdown

En el escritorio, el formato de Markdown para tarjetas de conectores tiene el siguiente aspecto:

![Formato de Markdown para tarjetas de conector en el cliente de escritorio](../../assets/images/cards/connector-desktop-markdown-combined.png)

En iOS, el formato de Markdown para tarjetas de conector tiene el siguiente aspecto:

![Formato de Markdown para tarjetas conector en el cliente iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

Problemas:

* El cliente iOS para Teams no representa imágenes en línea de Markdown o HTML en tarjetas conectoras.
* Blockquotes se representan como con sangría, pero sin fondo gris.

En Android, el formato de Markdown para tarjetas de conector tiene el siguiente aspecto:

![Formato de Markdown para tarjetas conector en el cliente de Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a>Ejemplo de formato para tarjetas conectoras de Markdown

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "summary": "Summary",
    "title": "Connector Card Markdown formatting",
    "sections": [
        {
            "text": "This is some **bold** text"
        },
        {
            "text": "This is some _italic_ text"
        },
        {
            "text": "# Header 1\r## Header 2\r### Header 3"
        },
        {
            "text": "- Bullet \r- List \r"
        },
        {
            "text": "1. Numbered\r1. List \r"
        },
        {
            "text": "Link: [Bing](https://www.bing.com)"
        },
        {
            "text": "embedded image link: ![Duck on a rock](http://aka.ms/Fo983c)"
        },
        {
            "text": "`preformatted text`"
        },
        {
            "text": "Newlines (backslash n, backslash n):\n\nline a\n\nline b\n\nline c"
        },
        {
            "text": ">This is a blockquote"
        }
     ]
  }
}

```

---

## <a name="formatting-cards-with-html"></a>Tarjetas de formato con HTML

# <a name="html-formatting-o365-connector-cards"></a>[**Formato HTML: tarjetas conector de O365**](#tab/connector-html)

Las tarjetas de conector admiten el formato HTML y Markdown limitados. Markdown se describe en la siguiente sección.

| Style | Ejemplo | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| encabezado (niveles 1 &ndash; 3) | **Text** | `<h3>Text</h3>` |
| Aplique | ~~text~~ | `<strike>text</strike>` |
| lista sin ordenar | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| Lista ordenada | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| texto con formato previo | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| hipervínculo | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| vínculo de imagen | <img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

En las tarjetas conector, las líneas nuevas se representan en HTML con la `<p>` etiqueta.

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a>Diferencias de escritorio y móviles para tarjetas de conector con HTML

En el escritorio, el formato HTML de las tarjetas conector tiene el siguiente aspecto:

![Formato HTML para tarjetas conector en el cliente de escritorio](../../assets/images/cards/Connector-desktop-html-combined.png)

En iOS, el formato HTML tiene el siguiente aspecto:

![Formato HTML para tarjetas conector en el cliente iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

Problemas:

* Las imágenes en línea no se representan en iOS con Markdown o HTML en tarjetas de conector.
* El texto con formato previo se representa pero no tiene un fondo gris.

En Android, el formato HTML es similar a este:

![Formato HTML para tarjetas conector en el cliente de Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a>Ejemplo de formato para tarjetas conector de HTML

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "summary": "Summary",
    "title": "Connector Card HTML formatting",
    "sections": [
        {
            "text": "This is some <strong>bold</strong> text"
        },
        {
            "text": "This is some <em>italic</em> text"
        },
        {
            "text": "This is some <strike>strikethrough</strike> text"
        },
        {
            "text": "<h1>Header 1</h1>\r<h2>Header 2</h2>\r <h3>Header 3</h3>"
        },
        {
            "text": "bullet list <ul><li>text</li><li>text</li></ul>"
        },
        {
            "text": "ordered list <ol><li>text</li><li>text</li></ol>"
        },
        {
            "text": "hyperlink <a href=\"https://www.bing.com/\">Bing</a>"
        },
        {
            "text": "embedded image <img src=\"http://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img>"
        },
        {
            "text": "preformatted text <pre>text</pre>"
        },
        {
            "text": "Paragraphs <p>Line a</p><p>Line b</p>"
        },
        {
            "text": "<blockquote>Blockquote text</blockquote>"
        }
     ]
  }
}

```

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[**Formato HTML: fichas de héroe y miniaturas**](#tab/simple-html)

Las etiquetas HTML son compatibles con tarjetas sencillas, como el héroe y la tarjeta en miniatura. No se admite Markdown.

| Style | Ejemplo | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| encabezado (niveles 1 &ndash; 3) | **Text** | `<h3>Text</h3>` |
| Aplique | ~~text~~ | `<strike>text</strike>` |
| lista sin ordenar | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| Lista ordenada | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| texto con formato previo | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| hipervínculo | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| vínculo de imagen |<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>Diferencias entre dispositivos móviles y de escritorio para tarjetas sencillas

Debido a las diferencias de resolución entre la plataforma de escritorio y la plataforma móvil, el formato es diferente entre el escritorio y la versión móvil de Teams.

En el escritorio, el formato HTML tiene un aspecto similar a este:

![Formato HTML en el cliente de escritorio](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

En iOS, el formato HTML tiene un aspecto similar a este:

![Formato HTML en el cliente de iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

Problemas:

* El formato de caracteres, como negrita y cursiva, no se representa en iOS.

En Android, el formato HTML tiene un aspecto similar a este:

![Formato HTML en el cliente de Android](../../assets/images/cards/card-formatting-xml-android-60.png)

El formato de caracteres, como negrita y cursiva, se muestra correctamente en Android.

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a>Ejemplo de formato para el formato HTML en tarjetas sencillas

Estas capturas de pantallas se crearon con Teams AppStudio, donde la propiedad Text de una tarjeta Hero se estableció en la siguiente cadena. Puede probar el formato en sus propias tarjetas modificando este código.

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"http://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---

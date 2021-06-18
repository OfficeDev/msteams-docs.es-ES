---
title: Formato de texto en tarjetas
description: Describe el formato de texto de tarjeta en Microsoft Teams
keywords: formato de tarjetas de bots de teams
localization_priority: Normal
ms.topic: reference
ms.date: 03/29/2018
ms.openlocfilehash: eead38b7f28ca740473a1df029e35b9ac624391d
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994171"
---
# <a name="format-cards-in-teams"></a>Dar formato a las tarjetas Teams

Puede agregar formato de texto enriquecido a las tarjetas mediante Markdown o HTML, según el tipo de tarjeta.

Las tarjetas solo admiten el formato en la propiedad de texto, no en las propiedades de título o subtítulo. El formato se puede especificar mediante un subconjunto de formato XML (HTML) o Markdown según el tipo de tarjeta. Se recomienda usar el formato Markdown para el desarrollo actual y futuro de tarjetas adaptables.

La compatibilidad con el formato difiere entre los distintos tipos de tarjeta y la representación de la tarjeta puede diferir ligeramente entre los clientes de escritorio y de Teams móviles, así como Teams en el explorador de escritorio.

Puedes incluir una imagen en línea con cualquier Teams tarjeta. Las imágenes con formato como , o archivos y no deben superar  `.png` `.jpg` los `.gif` 1024 ×1024 px o 1 MB. Gif animado no es compatible oficialmente. Para obtener más información, vea [Referencia de tarjetas](./cards-reference.md#inline-card-images).

## <a name="formatting-cards-with-markdown"></a>Formato de tarjetas con Markdown

Hay dos tipos de tarjeta que admiten Markdown en Teams:

> [!div class="checklist"]
> * **Tarjetas adaptables:** Markdown se admite en el campo Tarjeta `Textblock` adaptable, así como `Fact.Title` y `Fact.Value` . Html no se admite en tarjetas adaptables.
> * **Tarjetas de conector de O365:** Markdown y HTML limitado se admiten en Office 365 tarjetas de conector en los campos de texto.

# <a name="markdown-formatting-adaptive-cards"></a>[**Formato markdown: tarjetas adaptables**](#tab/adaptive-md)

 Los estilos admitidos `Textblock` para , `Fact.Title` y `Fact.Value` son:

| Estilo | Ejemplo | Markdown |
| --- | --- | --- |
| bold | **Bold** | ```**Bold**``` |
| italic | _Italic_ | ```_Italic_``` |
| lista sin ordenar | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| lista ordenada | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Hyperlinks |[Bing](https://www.bing.com/)| ```[Title](url)``` |

No se admiten las siguientes etiquetas Markdown:

* Encabezados
* Tablas
* Imágenes
* Texto con formato previo
* Blockquotes

> [!IMPORTANT]
> Las tarjetas adaptables no admiten formato HTML.

### <a name="newlines-for-adaptive-cards"></a>Líneas nuevas para tarjetas adaptables

En las listas puede usar las `\r` `\n` secuencias de escape o para las líneas nuevas. Si se usa en una lista, se aplica sangría al siguiente elemento `\n\n` de la lista. Si necesita líneas nuevas en otra parte del bloque de texto, use `\n\n` .

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>Diferencias de dispositivos móviles y de escritorio para tarjetas adaptables

El formato es ligeramente diferente entre el escritorio y las versiones móviles de Teams.

En el escritorio, el formato markdown de tarjeta adaptable aparece de esta forma en los exploradores web y en la Teams cliente:

![Formato markdown de tarjeta adaptable en el cliente de escritorio](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

En iOS, el formato markdown de tarjeta adaptable aparece de la siguiente forma:

![Formato markdown de tarjeta adaptable en iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

En Android, el formato de markdown de tarjeta adaptable aparece de la siguiente forma:

![Formato markdown de tarjeta adaptable en Android](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a>Más información sobre tarjetas adaptables

[Características de texto en tarjetas adaptables](/adaptive-cards/create/textfeatures) Las características de fecha y localización mencionadas en este tema no se admiten en Teams.

### <a name="formatting-sample-for-adaptive-cards"></a>Ejemplo de formato para tarjetas adaptables

``` json
{
    "$schema": "https://adaptivecards.io/schemas/adaptive-card.json",
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
            "text": "Check out [Adaptive Cards](https://adaptivecards.io)"
        }
    ]
}
```

### <a name="mention-support-within-adaptive-cards-v12"></a>Mencione la compatibilidad con tarjetas adaptables v1.2

Las menciones basadas en tarjetas se admiten en clientes web, de escritorio y móviles. Puede agregar menciones @ dentro de un cuerpo de tarjeta adaptable para bots y respuestas de extensión de mensajería. Para agregar menciones @ en tarjetas, siga la misma lógica de notificación y representación que las [menciones basadas](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)en mensajes en conversaciones de chat de canal y grupo.

Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.

> [!NOTE]
> * [Actualmente,](https://adaptivecards.io/explorer/Media.html) los elementos multimedia no se admiten en las tarjetas adaptables v1.2 en la Teams web.
> * Las menciones & equipo de canal no se admiten en los mensajes de bot.

#### <a name="constructing-mentions"></a>Menciones de construcción

Para incluir una mención en una tarjeta adaptable, la aplicación debe incluir los siguientes elementos:

* `<at>username</at>` en los elementos de tarjeta adaptable compatibles.
* El objeto dentro de una propiedad en el contenido de la tarjeta, que incluye el Teams de usuario `mention` `msteams` del usuario mencionado.
* El `userId` es único para el identificador del bot y un usuario en particular. Se puede usar para @mention un usuario determinado. Se `userId` puede recuperar mediante una de las opciones mencionadas en obtener el identificador de [usuario](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).

#### <a name="sample-adaptive-card-with-a-mention"></a>Tarjeta adaptable de ejemplo con una mención

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
    "$schema": "https://adaptivecards.io/schemas/adaptive-card.json",
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

### <a name="information-masking-in-adaptive-cards"></a>Enmascaramiento de información en tarjetas adaptables
Use la propiedad information masking para enmascarar información específica, como contraseña o información confidencial de los usuarios dentro del elemento de entrada de [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) tarjeta adaptable. 

> [!NOTE]
> La característica solo admite el enmascaramiento de información del lado [cliente,](../../build-your-first-app/build-bot.md)el texto de entrada enmascarado se envía como texto sin formato a la dirección del extremo https que se especificó durante la configuración del bot . 

#### <a name="sample-adaptive-card-with-masking-property"></a>Tarjeta adaptable de ejemplo con la propiedad masking

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
},
```

La siguiente imagen es un ejemplo de enmascaramiento de información en tarjetas adaptables:

![Imagen de información de enmascaramiento](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a>Tarjeta adaptable de ancho completo
Puede usar la propiedad para expandir el ancho de una tarjeta adaptable y `msteams` usar espacio de lienzo adicional. Para obtener información sobre cómo usar la propiedad, vea el siguiente ejemplo:

#### <a name="constructing-full-width-cards"></a>Construcción de tarjetas de ancho completo
Para que una tarjeta adaptable de ancho completo, el objeto de la propiedad en el contenido de la `width` `msteams` tarjeta debe establecerse en `Full` .
Además, la aplicación debe incluir los siguientes elementos:

#### <a name="sample-adaptive-card-with-full-width"></a>Tarjeta adaptable de ejemplo con ancho completo

``` json
{
    "type": "AdaptiveCard",
    "body": [{
        "type": "Container",
        "items": [{
            "type": "TextBlock",
            "text": "Digest card",
            "size": "Large",
            "weight": "Bolder"
        }]
    }],

    "msteams": {
        "width": "Full"
    },
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

Una tarjeta adaptable de ancho completo aparece de la siguiente manera: ![ Vista de tarjeta adaptable de ancho completo](../../assets/images/cards/full-width-adaptive-card.png)

Si no ha establecido la propiedad en Full , la vista predeterminada de la tarjeta adaptable aparece de la siguiente manera: Vista de tarjeta adaptable `width` de ancho  ![ pequeño](../../assets/images/cards/small-width-adaptive-card.png)

### <a name="typeahead-support"></a>Compatibilidad con Typeahead

Dentro del elemento de esquema, pedir a los usuarios que filtren y seleccionen a través de un número considerable de opciones puede ralentizar significativamente la finalización [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) de tareas. La compatibilidad con la punta de tipo dentro de las tarjetas adaptables puede simplificar la selección de entrada limitando o filtrando el conjunto de opciones de entrada cuando un usuario escribe la entrada. 

#### <a name="enable-typeahead-in-adaptive-cards"></a>Habilitar el cabezal de tipo en tarjetas adaptables

Para habilitar typeahead dentro del `Input.Choiceset` conjunto en y asegurarse de que está establecido en `style` `filtered` `isMultiSelect` `false` . 

#### <a name="sample-adaptive-card-with-typeahead-support"></a>Tarjeta adaptable de ejemplo con compatibilidad con membrete

``` json
{
   "type": "Input.ChoiceSet",
   "label": "Select a user",
   "isMultiSelect": false,
   "choices":  [
      { "title": "User 1", "value": "User1" },
      { "title": "User 2", "value": "User2" }
    ],
   "style": "filtered"
}
``` 

### <a name="stage-view-for-images-in-adaptive-cards"></a>Vista de fase para imágenes en tarjetas adaptables

En una tarjeta adaptable, puedes usar la propiedad para agregar la capacidad de mostrar imágenes en la vista de fase `msteams` de forma selectiva. Cuando los usuarios mantienen el mouse sobre las imágenes, verían un icono de expansión, para el que `allowExpand` el atributo está establecido en `true` . Para obtener información sobre cómo usar la propiedad, vea el siguiente ejemplo:

``` json
{
    "type": "AdaptiveCard",
     "body": [
          {
            "type": "Image",
            "url": "https://picsum.photos/200/200?image=110",
            "msTeams": {
              "allowExpand": true
            }
          },
     ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

Cuando los usuarios mantienen el mouse sobre la imagen, aparece un icono expandir en la esquina superior derecha de la imagen: ![ tarjeta adaptable con imagen expandible](../../assets/images/cards/adaptivecard-hover-expand-icon.png)

La imagen aparece en la vista de fase cuando el usuario selecciona el botón expandir: ![ Imagen expandida a vista de fase](../../assets/images/cards/adaptivecard-expand-image.png)

En la vista de fase, los usuarios pueden acercar y alejar la imagen. Puedes seleccionar qué imágenes de la tarjeta adaptable deben tener esta funcionalidad.

> [!NOTE]
> La funcionalidad acercar y alejar solo se aplica a los elementos de imagen (tipo Image) de una tarjeta adaptable.

> [!NOTE]
> Para Teams aplicaciones móviles, la funcionalidad de vista de fase para imágenes en tarjetas adaptables está disponible de forma predeterminada y los usuarios podrán ver imágenes de tarjeta adaptables en la vista de fase simplemente pulsando en la imagen, independientemente de si el atributo está presente o `allowExpand` no.

# <a name="markdown-formatting-o365-connector-cards"></a>[**Formato markdown: tarjetas de conector de O365**](#tab/connector-md)

Las tarjetas de conector admiten markdown limitado y formato HTML. La compatibilidad con HTML se describe en la última sección.

| Estilo | Ejemplo | Markdown |
| --- | --- | --- |
| bold | **text** | `**text**` |
| italic | *text* | `*text*` |
| encabezado (niveles 1 &ndash; 3) | **Texto** | `### Text`|
| strikethrough | ~~text~~ | `~~text~~` |
| lista sin ordenar | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| lista ordenada | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| texto con formato previo | `text` | ``preformatted text`` |
| blockquote | >texto de bloques | `>blockquote text` |
| hipervínculo | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| vínculo de imagen |![Agacharse en una roca](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

En las tarjetas de conector, las líneas nuevas se representan `\n\n` para , pero no para o `\n` `\r` .

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a>Diferencias de dispositivos móviles y de escritorio para tarjetas de conector con Markdown

En el escritorio, el formato markdown para tarjetas de conector tiene este aspecto:

![Formato markdown para tarjetas de conector en el cliente de escritorio](../../assets/images/cards/connector-desktop-markdown-combined.png)

En iOS, el formato markdown para tarjetas de conector tiene este aspecto:

![Formato markdown para tarjetas de conector en el cliente de iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

Problemas:

* El cliente de iOS para Teams no representa imágenes en línea markdown o HTML en tarjetas de conector.
* Las comillas bloques se representan como sangría pero sin un fondo gris.

En Android, el formato markdown para tarjetas de conector tiene este aspecto:

![Formato markdown para tarjetas de conector en el cliente Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a>Ejemplo de formato para tarjetas de conector de Markdown

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "https://schema.org/extensions",
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
            "text": "embedded image link: ![Duck on a rock](https://aka.ms/Fo983c)"
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

## <a name="formatting-cards-with-html"></a>Formato de tarjetas con HTML

# <a name="html-formatting-o365-connector-cards"></a>[**Formato HTML: tarjetas de conector de O365**](#tab/connector-html)

Las tarjetas de conector admiten markdown limitado y formato HTML. Markdown se describe en la sección siguiente.

| Estilo | Ejemplo | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| encabezado (niveles 1 &ndash; 3) | **Texto** | `<h3>Text</h3>` |
| strikethrough | ~~text~~ | `<strike>text</strike>` |
| lista sin ordenar | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| lista ordenada | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| texto con formato previo | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| hipervínculo | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| vínculo de imagen | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

En las tarjetas de conector, las líneas nuevas se representan en HTML mediante la `<p>` etiqueta.

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a>Diferencias de dispositivos móviles y de escritorio para tarjetas de conector con HTML

En el escritorio, el formato HTML de las tarjetas de conector tiene este aspecto:

![Formato HTML para tarjetas de conector en el cliente de escritorio](../../assets/images/cards/Connector-desktop-html-combined.png)

En iOS, el formato HTML tiene este aspecto:

![Formato HTML para tarjetas de conector en el cliente de iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

Problemas:

* Las imágenes en línea no se representan en iOS con Markdown o HTML en tarjetas de conector.
* El texto con formato previo se representa pero no tiene un fondo gris.

En Android, el formato HTML tiene este aspecto:

![Formato HTML para tarjetas de conector en el cliente Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a>Ejemplo de formato para tarjetas de conector HTML

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "https://schema.org/extensions",
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
            "text": "embedded image <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img>"
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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[**Formato HTML: tarjetas de miniatura y de héroe**](#tab/simple-html)

Las etiquetas HTML son compatibles con tarjetas sencillas, como la tarjeta de miniatura y la de héroe. Markdown no es compatible.

| Estilo | Ejemplo | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| encabezado (niveles 1 &ndash; 3) | **Texto** | `<h3>Text</h3>` |
| strikethrough | ~~text~~ | `<strike>text</strike>` |
| lista sin ordenar | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| lista ordenada | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| texto con formato previo | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| hipervínculo | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| vínculo de imagen |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>Diferencias de escritorio y móvil para tarjetas sencillas

Debido a las diferencias de resolución entre el escritorio y la plataforma móvil, el formato es diferente entre el escritorio y la versión móvil de Teams.

En el escritorio, el formato HTML aparece de la siguiente forma:

![Formato HTML en el cliente de escritorio](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

En iOS, el formato HTML aparece de la siguiente forma:

![Formato HTML en el cliente de iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

Problemas:

* El formato de caracteres como negrita y cursiva no se representa en iOS.

En Android, el formato HTML aparece de esta forma:

![Formato HTML en el cliente Android](../../assets/images/cards/card-formatting-xml-android-60.png)

El formato de caracteres como negrita y cursiva se muestra correctamente en Android.

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a>Ejemplo de formato para formato HTML en tarjetas sencillas

Estas capturas de pantalla se crearon Teams AppStudio, donde la propiedad de texto de una tarjeta principal se estableció en la siguiente cadena. Puedes probar el formato en tus propias tarjetas modificando este código.

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---

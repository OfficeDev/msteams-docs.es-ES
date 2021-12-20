---
title: Formato de texto en tarjetas
description: Describe el formato de texto de tarjeta en Microsoft Teams
keywords: formato de tarjetas de bots de teams
ms.localizationpriority: medium
ms.topic: reference
ms.date: 06/25/2021
ms.openlocfilehash: 0c012db1936907c15082ba12c4d681540483bb95
ms.sourcegitcommit: a2d7d2bdf4b056b35f29c6fdb315bc7dc28b6f6f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2021
ms.locfileid: "61569535"
---
# <a name="format-cards-in-microsoft-teams"></a>Dar formato a tarjetas en Microsoft Teams

Estas son las dos formas de agregar formato de texto enriquecido a las tarjetas:
* [Markdown](#format-cards-with-markdown)
* [HTML](#format-cards-with-html)

Las tarjetas solo admiten el formato en la propiedad de texto, no en las propiedades de título o subtítulo. El formato se puede especificar mediante un subconjunto de formato XML o HTML o Markdown, según el tipo de tarjeta. Para el desarrollo actual y futuro de tarjetas adaptables, se recomienda el formato markdown.

La compatibilidad con el formato difiere entre los tipos de tarjeta. La representación de la tarjeta puede diferir ligeramente entre el escritorio y los clientes Microsoft Teams móviles, así como Teams en el explorador de escritorio.

Puedes incluir una imagen en línea con cualquier Teams tarjeta. Las imágenes pueden tener formato como , o archivos y no deben superar `.png` `.jpg` los `.gif` 1024 ×1024 px o 1 MB. Gif animado no es compatible. Para obtener más información, vea [tipos de tarjetas](./cards-reference.md#inline-card-images).

Puedes dar formato a tarjetas adaptables y Office 365 connector con Markdown que incluyan ciertos estilos admitidos.

## <a name="format-cards-with-markdown"></a>Dar formato a tarjetas con Markdown

Los siguientes tipos de tarjeta admiten el formato Markdown en Teams:

* Tarjetas adaptables: Markdown se admite en el campo Tarjeta `Textblock` adaptable, así como `Fact.Title` en `Fact.Value` . Html no se admite en tarjetas adaptables.
* Office 365 connector: Markdown y HTML limitado se admiten en las Office 365 connector en los campos de texto.

Puedes usar líneas nuevas para tarjetas adaptables mediante `\r` o `\n` secuencias de escape para las líneas nuevas de las listas. El formato es diferente entre el escritorio y las versiones móviles de Teams para tarjetas adaptables. Las menciones basadas en tarjetas se admiten en clientes web, de escritorio y móviles. Puede usar la propiedad de enmascaramiento de información para enmascarar información específica, como contraseña o información confidencial de los usuarios dentro del elemento de entrada Tarjeta `Input.Text` adaptable. Puede expandir el ancho de una tarjeta adaptable mediante el `width` objeto. Puede habilitar la compatibilidad con typeahead en tarjetas adaptables y filtrar el conjunto de opciones de entrada a medida que el usuario escribe la entrada. Puede usar la propiedad `msteams` para agregar la capacidad de mostrar imágenes en la vista de fase de forma selectiva.

El formato es diferente entre el escritorio y las versiones móviles de Teams para tarjetas adaptables y tarjetas de conector. En esta sección, puede ir a través del ejemplo de formato Markdown para tarjetas adaptables y tarjetas de conector.

# <a name="markdown-format-for-adaptive-cards"></a>[Formato markdown para tarjetas adaptables](#tab/adaptive-md)

 En la tabla siguiente se proporcionan los estilos admitidos para `Textblock` `Fact.Title` , y `Fact.Value` :

| Estilo | Ejemplo | Markdown |
| --- | --- | --- |
| Negrita | **Bold** | ```**Bold**``` |
| Italic | _Italic_ | ```_Italic_``` |
| Lista no ordenada | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| Lista ordenada | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Hyperlinks |[Bing](https://www.bing.com/)| ```[Title](url)``` |

No se admiten las siguientes etiquetas Markdown:

* Encabezados
* Tablas
* Imágenes
* Texto con formato previo
* Blockquotes

### <a name="newlines-for-adaptive-cards"></a>Nuevas líneas para tarjetas adaptables

Puede usar las `\r` secuencias de `\n` escape o para las líneas nuevas de las listas. El uso en listas hace que se aplique sangría al siguiente elemento `\n\n` de la lista. Si necesita nuevas líneas en otra parte del TextBlock, use `\n\n` .

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>Diferencias de dispositivos móviles y de escritorio para tarjetas adaptables

En el escritorio, el formato de markdown de tarjeta adaptable aparece como se muestra en la siguiente imagen en los exploradores web y en la Teams cliente:

![Formato de markdown de tarjeta adaptable en el cliente de escritorio](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

En iOS, el formato de markdown de tarjeta adaptable aparece como se muestra en la siguiente imagen:

![Formato de markdown de tarjeta adaptable en iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

En Android, el formato de markdown de tarjeta adaptable aparece como se muestra en la siguiente imagen:

![Formato de markdown de tarjeta adaptable en Android](../../assets/images/cards/Adaptive-markdown-Android.png)

Para obtener más información, vea [características de texto en Tarjetas adaptables](/adaptive-cards/create/textfeatures).

> [!NOTE]
> Las características de fecha y localización mencionadas en esta sección no se admiten en Teams.

### <a name="adaptive-cards-format-sample"></a>Muestra de formato de tarjetas adaptables

El siguiente código muestra un ejemplo de formato de tarjetas adaptables:

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

### <a name="mention-support-within-adaptive-cards"></a>Mencionar compatibilidad con tarjetas adaptables 

Puedes agregar @mentions cuerpo de una tarjeta adaptable para bots y respuestas de extensión de mensajería. Para agregar @mentions tarjetas, siga la misma lógica de notificación y representación que las [menciones basadas](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)en mensajes en conversaciones de chat de canal y grupo.

Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.

> [!NOTE]
> * [Actualmente,](https://adaptivecards.io/explorer/Media.html) los elementos multimedia no se admiten en las tarjetas adaptables Teams plataforma.
> * Las menciones de canal y equipo no se admiten en los mensajes de bot.

Para incluir una mención en una tarjeta adaptable, la aplicación debe incluir los siguientes elementos:

* `<at>username</at>` en los elementos de tarjeta adaptable compatibles.
* El objeto dentro de una propiedad en el contenido de la tarjeta `mention` incluye el Teams de usuario del usuario `msteams` mencionado.
* El `userId` es único para el identificador del bot y un usuario en particular. Se puede usar para @mention un usuario determinado. Se `userId` puede recuperar mediante una de las opciones mencionadas en obtener el identificador de [usuario](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).

#### <a name="sample-adaptive-card-with-a-mention"></a>Tarjeta adaptable de ejemplo con una mención

El siguiente código muestra un ejemplo de tarjeta adaptable con una mención:

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

### <a name="aad-object-id-and-upn-in-user-mention"></a>AAD id. de objeto y UPN en mención de usuario 

Teams plataforma permite mencionar a los usuarios con su identificador de objeto AAD y el nombre de principio de usuario (UPN), además de los identificadores de mención existentes. Los bots con tarjetas adaptables y conectores con webhooks entrantes admiten los dos id. de mención del usuario. 

En la tabla siguiente se describen los id. de mención de usuario que se han admitido recientemente:

|IDs  | Capacidades de soporte técnico |   Description | Ejemplo |
|----------|--------|---------------|---------|
| AAD de objeto | Bot, conector |  AAD de objeto del usuario |  49c4641c-ab91-4248-aebb-6a7de286397b |
| UPN | Bot, conector | AAD UPN del usuario | john.smith@microsoft.com |

#### <a name="user-mention-in-bots-with-adaptive-cards"></a>Mención de usuario en bots con tarjetas adaptables 

Los bots admiten la mención de usuario AAD identificador de objeto y UPN, además de los identificadores existentes. La compatibilidad con dos nuevos IDs está disponible en bots para mensajes de texto, cuerpo de tarjetas adaptables y respuesta de extensión de mensajería. Bots support the mention IDs in conversation and `invoke` scenarios. El usuario obtiene la notificación de fuente de actividad cuando se @mentioned con los id. 

> [!NOTE]
> La actualización del esquema y los cambios en la interfaz de usuario y la experiencia de usuario no son necesarios para las menciones de usuario con tarjetas adaptables en bot.

##### <a name="example"></a>Ejemplo 

Ejemplo de mención de usuario en bots con tarjetas adaptables de la siguiente manera:

```json 
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "version": "1.0",
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Hi <at>Adele UPN</at>, <at>Adele AAD</at>"
    }
  ],
  "msteams": {
    "entities": [
      {
        "type": "mention",
        "text": "<at>Adele UPN</at>",
        "mentioned": {
          "id": "AdeleV@contoso.onmicrosoft.com",
          "name": "Adele Vance"
        }
      },
      {
        "type": "mention",
        "text": "<at>Adele AAD</at>",
        "mentioned": {
          "id": "87d349ed-44d7-43e1-9a83-5f2406dee5bd",
          "name": "Adele Vance"
        }
      }
    ]
  }
}
```

La siguiente imagen ilustra la mención del usuario con la tarjeta adaptable en bot:

![Mención de usuario en bot con tarjeta adaptable](~/assets/images/authentication/user-mention-in-bot.png)

#### <a name="user-mention-in-incoming-webhook-with-adaptive-cards"></a>Mención de usuario en Webhook entrante con tarjetas adaptables 

Los webhooks entrantes comienzan a admitir la mención de usuario en tarjetas adaptables con el AAD de objeto y UPN.

> [!NOTE]    
> * Habilite la mención de usuario en el esquema para webhooks entrantes para admitir AAD id. de objeto y UPN. 
> * Los cambios en la interfaz de usuario y la experiencia de usuario no son necesarios para las menciones de usuario con AAD id. de objeto y UPN.      
> * La notificación de fuente de actividad para Webhook entrante con mención de usuario estará disponible en la versión futura.

##### <a name="example"></a>Ejemplo 

Ejemplo de mención de usuario en Webhook entrante de la siguiente manera:

```json
{
    "type": "message",
    "attachments": [
        {
        "contentType": "application/vnd.microsoft.card.adaptive",
        "content": {
            "type": "AdaptiveCard",
            "body": [
                {
                    "type": "TextBlock",
                    "size": "Medium",
                    "weight": "Bolder",
                    "text": "Sample Adaptive Card with User Mention"
                },
                {
                    "type": "TextBlock",
                    "text": "Hi <at>Adele UPN</at>, <at>Adele AAD</at>"
                }
            ],
            "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
            "version": "1.0",
            "msteams": {
                "entities": [
                    {
                        "type": "mention",
                        "text": "<at>Adele UPN</at>",
                        "mentioned": {
                          "id": "AdeleV@contoso.onmicrosoft.com",
                          "name": "Adele Vance"
                        }
                      },
                      {
                        "type": "mention",
                        "text": "<at>Adele AAD</at>",
                        "mentioned": {
                          "id": "87d349ed-44d7-43e1-9a83-5f2406dee5bd",
                          "name": "Adele Vance"
                        }
                      }
                ]
            }
        }
    }]
}
```

La siguiente imagen ilustra la mención del usuario en webhook entrante:

![Mención de usuario en Webhook entrante](~/assets/images/authentication/user-mention-in-incoming-webhook.png)

### <a name="information-masking-in-adaptive-cards"></a>Enmascaramiento de información en tarjetas adaptables

Use la propiedad de enmascaramiento de información para enmascarar información específica, como contraseña o información confidencial de los usuarios dentro del elemento de entrada Tarjeta [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) adaptable.

> [!NOTE]
> La característica solo admite el enmascaramiento de información del lado cliente. El texto de entrada enmascarado se envía como texto sin formato a la dirección del extremo HTTPS que se especificó durante la [configuración del bot](../../build-your-first-app/build-bot.md#4-register-your-bot-endpoint).

Para enmascarar la información en tarjetas adaptables, agregue la propiedad para escribir `style` y establezca su valor en  `input.text` **Password**.

#### <a name="sample-adaptive-card-with-masking-property"></a>Tarjeta adaptable de ejemplo con la propiedad masking

El siguiente código muestra un ejemplo de la propiedad Adaptive Card with masking:

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

Puede usar la propiedad para expandir el ancho de una tarjeta adaptable y `msteams` usar espacio de lienzo adicional. En la siguiente sección se proporciona información sobre cómo usar la propiedad.

#### <a name="construct-full-width-cards"></a>Construir tarjetas de ancho completo

Para crear una tarjeta adaptable de ancho completo, el objeto de la propiedad en el contenido de la tarjeta `width` `msteams` debe establecerse en `Full` .

#### <a name="sample-adaptive-card-with-full-width"></a>Tarjeta adaptable de ejemplo con ancho completo

Para crear una tarjeta adaptable de ancho completo, la aplicación debe incluir los elementos del siguiente ejemplo de código:

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

La siguiente imagen muestra una tarjeta adaptable de ancho completo:

![Vista de tarjeta adaptable de ancho completo](../../assets/images/cards/full-width-adaptive-card.png)

La siguiente imagen muestra la vista predeterminada de la tarjeta adaptable cuando no se ha establecido la `width` propiedad en **Full**:

![Vista de tarjeta adaptable de ancho pequeño](../../assets/images/cards/small-width-adaptive-card.png)

### <a name="typeahead-support"></a>Compatibilidad con Typeahead

Dentro del elemento de esquema, pedir a los usuarios que filtren y seleccionen un número considerable de opciones puede ralentizar considerablemente la finalización [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) de las tareas. La compatibilidad con la punta de tipo dentro de las tarjetas adaptables puede simplificar la selección de entrada limitando o filtrando el conjunto de opciones de entrada a medida que el usuario escribe la entrada.

Para habilitar typeahead dentro del `Input.Choiceset` , establecido en y asegúrese está establecido en `style` `filtered` `isMultiSelect` `false` .

#### <a name="sample-adaptive-card-with-typeahead-support"></a>Tarjeta adaptable de ejemplo con compatibilidad con membrete

En el siguiente código se muestra un ejemplo de tarjeta adaptable con compatibilidad con punta de tipo:

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

En una tarjeta adaptable, puedes usar la propiedad para agregar la capacidad de mostrar imágenes en la vista de fase `msteams` de forma selectiva. Cuando los usuarios mantienen el mouse sobre las imágenes, pueden ver un icono de expansión, para el que `allowExpand` el atributo está establecido en `true` . Para obtener información sobre cómo usar la propiedad, vea el siguiente ejemplo:

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
          }
     ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

Cuando los usuarios mantienen el mouse sobre la imagen, aparece un icono expandir en la esquina superior derecha, como se muestra en la siguiente imagen:

![Tarjeta adaptable con imagen expandible](../../assets/images/cards/adaptivecard-hover-expand-icon.png)

La imagen aparece en la vista de fase cuando el usuario selecciona el icono expandir como se muestra en la siguiente imagen:

![Imagen expandida a vista de fase](../../assets/images/cards/adaptivecard-expand-image.png)

En la vista de fase, los usuarios pueden acercar y alejar la imagen. Puedes seleccionar las imágenes de la tarjeta adaptable que deben tener esta funcionalidad.

> [!NOTE]
> * La funcionalidad acercar y alejar solo se aplica a los elementos de imagen que son tipo de imagen en una tarjeta adaptable.
> * Para Teams móviles, la funcionalidad de vista de fase para imágenes en tarjetas adaptables está disponible de forma predeterminada. Los usuarios pueden ver imágenes de tarjeta adaptable en la vista de fase simplemente pulsando en la imagen, independientemente de si el `allowExpand` atributo está presente o no.

# <a name="markdown-format-for-office-365-connector-cards"></a>[Formato markdown para tarjetas Office 365 Connector](#tab/connector-md)

Las tarjetas de conector admiten markdown limitado y formato HTML.

| Estilo | Ejemplo | Markdown |
| --- | --- | --- |
| Negrita | **text** | `**text**` |
| Italic | *text* | `*text*` |
| Encabezado (niveles 1 &ndash; 3) | **Texto** | `### Text`|
| Tachado | ~~text~~ | `~~text~~` |
| Lista no ordenada | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| Lista ordenada | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Texto con formato previo | `text` | ``preformatted text`` |
| Blockquote | >texto de bloques | `>blockquote text` |
| Hipervínculo | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| Vínculo imagen |![Agacharse en una roca](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

En las tarjetas de conector, las líneas nuevas se representan `\n\n` para , pero no para o `\n` `\r` .

### <a name="mobile-and-desktop-differences-for-connector-cards"></a>Diferencias de escritorio y móvil para tarjetas de conector

En el escritorio, el formato markdown para tarjetas de conector aparece como se muestra en la siguiente imagen:

![Formato markdown para tarjetas de conector en el cliente de escritorio](../../assets/images/cards/connector-desktop-markdown-combined.png)

En iOS, el formato Markdown para tarjetas de conector aparece como se muestra en la siguiente imagen:

![Formato markdown para tarjetas de conector en el cliente de iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

Las tarjetas de conector que usan Markdown para iOS incluyen los siguientes problemas:

* El cliente de iOS para Teams no representa imágenes en línea markdown o HTML en tarjetas de conector.
* Las comillas bloques se representan como sangría pero sin un fondo gris.

En Android, el formato Markdown para tarjetas de conector aparece como se muestra en la siguiente imagen:

![Formato markdown para tarjetas de conector en el cliente Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="format-example-for-markdown-connector-cards"></a>Ejemplo de formato para tarjetas de conector de Markdown

El siguiente código muestra un ejemplo de formato para tarjetas de conector markdown:

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

## <a name="format-cards-with-html"></a>Dar formato a tarjetas con HTML

Los siguientes tipos de tarjeta admiten el formato HTML en Teams:

* Office 365 de conector: se admite el markdown limitado y el formato HTML en Office 365 connector.
* Tarjetas de miniatura y de héroe: las etiquetas HTML son compatibles con tarjetas sencillas, como las tarjetas de miniatura y de héroe.

El formato es diferente entre el escritorio y las versiones móviles de Teams para tarjetas Office 365 Connector y tarjetas sencillas. En esta sección, puede ir a través del ejemplo de formato HTML para tarjetas de conector y tarjetas sencillas.

# <a name="html-format-for-office-365-connector-cards"></a>[Formato HTML para tarjetas Office 365 Connector](#tab/connector-html)

Las tarjetas de conector admiten markdown limitado y formato HTML.

| Estilo | Ejemplo | HTML |
| --- | --- | --- |
| Negrita | **text** | `<strong>text</strong>` |
| Italic | *text* | `<em>text</em>` |
| Encabezado (niveles 1 &ndash; 3) | **Texto** | `<h3>Text</h3>` |
| Tachado | ~~text~~ | `<strike>text</strike>` |
| Lista no ordenada | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| Lista ordenada | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| Texto con formato previo | `text` | `<pre>text</pre>` |
| Blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| Hipervínculo | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| Vínculo imagen | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

En las tarjetas de conector, las líneas nuevas se representan en HTML mediante la `<p>` etiqueta.

### <a name="mobile-and-desktop-differences-for-connector-cards"></a>Diferencias de escritorio y móvil para tarjetas de conector

En el escritorio, el formato HTML para tarjetas de conector aparece como se muestra en la siguiente imagen:

![Formato HTML para tarjetas de conector en el cliente de escritorio](../../assets/images/cards/Connector-desktop-html-combined.png)

En iOS, el formato HTML aparece como se muestra en la siguiente imagen:

![Formato HTML para tarjetas de conector en el cliente de iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

Las tarjetas de conector que usan HTML para iOS incluyen los siguientes problemas:

* Las imágenes en línea no se representan en iOS con Markdown o HTML en tarjetas de conector.
* El texto con formato previo se representa pero no tiene un fondo gris.

En Android, el formato HTML aparece como se muestra en la siguiente imagen:

![Formato HTML para tarjetas de conector en el cliente Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="format-sample-for-html-connector-cards"></a>Ejemplo de formato para tarjetas de conector HTML

El siguiente código muestra un ejemplo de formato para tarjetas de conector HTML:

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

# <a name="html-format-for-hero-and-thumbnail-cards"></a>[Formato HTML para tarjetas de miniatura y de héroe](#tab/simple-html)

Las etiquetas HTML son compatibles con tarjetas sencillas, como las tarjetas de miniatura y de héroe. Markdown no es compatible.

| Estilo | Ejemplo | HTML |
| --- | --- | --- |
| Negrita | **text** | `<strong>text</strong>` |
| Italic | *text* | `<em>text</em>` |
| Encabezado (niveles 1 &ndash; 3) | **Texto** | `<h3>Text</h3>` |
| Tachado | ~~text~~ | `<strike>text</strike>` |
| Lista no ordenada | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| Lista ordenada | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| Texto con formato previo | `text` | `<pre>text</pre>` |
| Blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| Hipervínculo | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| Vínculo imagen |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>Diferencias de escritorio y móvil para tarjetas sencillas

Como hay diferencias de resolución entre la plataforma de escritorio y la plataforma móvil, el formato es diferente entre el escritorio y la versión móvil de Teams.

En el escritorio, el formato HTML aparece como se muestra en la siguiente imagen:

![Formato HTML en el cliente de escritorio](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

En iOS, el formato HTML aparece como se muestra en la siguiente imagen:

![Formato HTML en el cliente de iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

El formato de caracteres, como negrita y cursiva, no se representa en iOS.

En Android, el formato HTML aparece como se muestra en la siguiente imagen:

![Formato HTML en el cliente Android](../../assets/images/cards/card-formatting-xml-android-60.png)

El formato de caracteres, como negrita y cursiva, se muestra correctamente en Android.

### <a name="format-example-for-simple-cards"></a>Ejemplo de formato para tarjetas sencillas

Las imágenes de la sección anterior se crearon con Teams **App Studio**, donde la propiedad de texto de una tarjeta principal se establece en la siguiente cadena:

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

Puedes probar el formato en tus propias tarjetas modificando este código.

---

## <a name="see-also"></a>Consulte también

* [Acciones de tarjeta](./cards-actions.md)
* [Uso de módulos de tareas desde los bots](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* [Módulos de tareas](~/task-modules-and-cards/cards/cards-format.md)
* [Formatear los mensajes del bot](~/bots/how-to/format-your-bot-messages.md)

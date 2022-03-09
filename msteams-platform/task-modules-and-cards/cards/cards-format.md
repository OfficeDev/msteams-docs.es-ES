---
title: Formato de texto en tarjetas
description: Describe el formato de texto de tarjetas en Microsoft Teams
keywords: formato de tarjetas de bots de teams
ms.localizationpriority: high
ms.topic: reference
ms.date: 06/25/2021
ms.openlocfilehash: b0d171134b58606a2d9eefa81bf1b5c16d27138e
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2022
ms.locfileid: "63356444"
---
# <a name="format-cards-in-microsoft-teams"></a>Dar formato a tarjetas en Microsoft Teams

Las dos formas de agregar formato de texto enriquecido a las tarjetas son:
* [Markdown](#format-cards-with-markdown)
* [HTML](#format-cards-with-html)

Las tarjetas solo admiten el formato en la propiedad de texto, no en las propiedades de título o subtítulo. El formato se puede especificar mediante un subconjunto de formato XML, HTML o Markdown, según el tipo de tarjeta. Para el desarrollo actual y futuro de las tarjetas adaptables, se recomienda utilizar el formato Markdown.

El soporte del formato difiere entre los tipos de tarjetas. La representación de la tarjeta puede diferir ligeramente entre los clientes de Microsoft Teams de escritorio y de móvil, así como de Teams en el explorador de escritorio.

Puede incluir una imagen alineada en cualquier tarjeta de Teams. Los formatos de imagen admitidos son .png, .jpg o .gif. Mantenga las dimensiones dentro de 1024 x 1024 px y el tamaño del archivo menos de 1 MB. Las imágenes .gif animadas no son admitidas. Para obtener más información, consulte [tipos de tarjetas](./cards-reference.md#inline-card-images).

Puede dar formato a Tarjetas adaptables y a tarjetas de conector de Office 365 mediante Markdown que incluye determinados estilos admitidos.

## <a name="format-cards-with-markdown"></a>Dar formato a tarjetas mediante Markdown

Los siguientes tipos de tarjeta admiten dar formato mediante Markdown en Teams:

* Tarjetas adaptables: Markdown se admite en el campo `Textblock` de Tarjeta adaptable, así como `Fact.Title` y `Fact.Value`. No se admite HTML en Tarjetas adaptables.
* Tarjetas del conector de Office 365: se admiten Markdown y HTML limitado en las tarjetas del conector de Office 365 en los campos de texto.

Puede usar nuevas líneas para Tarjetas adaptables mediante secuencias de escape `\r` o `\n`para las nuevas líneas de las listas. El formato es diferente entre las versiones de escritorio y de móvil de Teams para Tarjetas adaptables. Las menciones basadas en tarjetas se admiten en clientes web, de escritorio y móviles. Puede usar la propiedad de enmascaramiento de información para enmascarar información específica, por ejemplo, contraseñas o información confidencial de los usuarios dentro del elemento de entrada `Input.Text` de la Tarjeta adaptable. Puede expandir el ancho de una Tarjeta adaptable mediante el objeto `width`. Puede habilitar la compatibilidad con TypeAhead en tarjetas adaptables y filtrar el conjunto de opciones de entrada a medida que el usuario escribe la entrada. Puede usar la propiedad `msteams` para agregar la funcionalidad de mostrar imágenes en la vista extendida de forma selectiva.

El formato es diferente entre las versiones de escritorio y de móvil de Teams para Tarjetas adaptables y tarjetas de conector. En esta sección, puede consultar el ejemplo de formato Markdown para Tarjetas adaptables y tarjetas de conector.

# <a name="markdown-format-for-adaptive-cards"></a>[Formato Markdown para Tarjetas adaptables](#tab/adaptive-md)

 La tabla siguiente proporciona los estilos admitidos para `Textblock`, `Fact.Title` y `Fact.Value`:

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

### <a name="newlines-for-adaptive-cards"></a>Nuevas líneas para Tarjetas adaptables

Puede usar las secuencias de escape `\r` o `\n` para las nuevas líneas de las listas. Si se utiliza `\n\n` en las listas, se aplica sangría al siguiente elemento de la lista. Si necesita nuevas líneas en cualquier otra parte del TextBlock, use `\n\n`.

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>Diferencias entre dispositivos móviles y de escritorio en Tarjetas adaptables

En el escritorio, el formato de Markdown de Tarjeta adaptable, aparece como se muestra en la siguiente imagen tanto en los exploradores web como en la aplicación cliente de Teams:

![Formato de Markdown de Tarjeta adaptable en el cliente de escritorio](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

En iOS, el formato de Markdown de Tarjeta adaptable aparece como se muestra en la siguiente imagen:

![Formato de Markdown de Tarjeta adaptable en iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

En Android, el formato de Markdown de Tarjeta adaptable aparece como se muestra en la siguiente imagen:

![Formato de Markdown de Tarjeta adaptable en Android](../../assets/images/cards/Adaptive-markdown-Android.png)

Para obtener más información, vea [características de texto en Tarjetas adaptables](/adaptive-cards/create/textfeatures).

> [!NOTE]
> Las características de fecha y localización mencionadas en esta sección, no se admiten en Teams.

### <a name="adaptive-cards-format-sample"></a>Muestra de formato de Tarjetas adaptables

El siguiente código muestra un ejemplo de formato de Tarjetas adaptables:

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

Las Tarjetas adaptables admiten emoji. El siguiente código muestra un ejemplo de Tarjetas adaptables con un emoji:

``` json
{ "$schema": "http://adaptivecards.io/schemas/adaptive-card.json", "type": "AdaptiveCard", "version": "1.0", "body": [ { "type": "Container", "items": [ { "type": "TextBlock", "text": "Publish Adaptive Card with emojis 🥰 ", "weight": "bolder", "size": "medium" }, ] }, ], }
```

:::image type="content" source="~/assets/images/cards/adaptive-card-emoji.png" alt-text="Tarjeta adaptable con un emoji" lightbox="../../assets/images/Cards/adaptive-card-emoji.png" border="true":::

### <a name="mention-support-within-adaptive-cards"></a>Compatibilidad de las menciones con las Tarjetas adaptables 

Puede agregar @menciones en el cuerpo de una Tarjeta adaptable para bots y respuestas de extensión de mensajería. Para agregar @menciones en las tarjetas, siga la misma lógica de notificación y representación que para las [menciones en conversaciones de chat y canales de grupo](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions) basadas en mensajes.

Los bots y las extensiones de mensajería pueden incluir menciones en el contenido de la tarjeta en [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) y elementos [FactSet](https://adaptivecards.io/explorer/FactSet.html).

> [!NOTE]
> * Actualmente, los [elementos multimedia](https://adaptivecards.io/explorer/Media.html) no se admiten en Tarjetas adaptables en la plataforma de Teams.
> * Las menciones de canal y equipo no se admiten en los mensajes de bot.

Para incluir una mención en una Tarjeta adaptable, la aplicación debe incluir los siguientes elementos:

* `<at>username</at>` en los elementos de Tarjeta adaptable compatibles.
* El objeto `mention` dentro de una propiedad `msteams` en el contenido de la tarjeta incluye el identificador de usuario de Teams del usuario que se menciona.
* El `userId` es único para el identificador de bot y un usuario en particular. Se puede usar para @mencionar a un usuario determinado. El `userId` se puede recuperar mediante una de las opciones mencionadas en [obtener el identificador de usuario](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).

#### <a name="sample-adaptive-card-with-a-mention"></a>Tarjeta adaptable de ejemplo con una mención

El siguiente código muestra un ejemplo de Tarjeta adaptable con mención:

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

### <a name="microsoft-azure-active-directory-azure-ad-object-id-and-upn-in-user-mention"></a>Id. de objeto de Microsoft Azure Active Directory (Azure AD) y UPN en la mención de usuario 

La plataforma de Teams permite mencionar a los usuarios con su Id. de objeto de Azure AD y su nombre principal de usuario (UPN), además de los identificadores de mención existentes. Los bots con Tarjetas adaptables y conectores con Webhooks entrantes admiten los dos id. de mención de usuario. 

En la tabla siguiente se describen los id. de mención de usuario que se han admitido recientemente:

|Identificadores  | Capacidades de compatibilidad |   Descripción | Ejemplo |
|----------|--------|---------------|---------|
| Id. de objeto de Azure AD | Bot, conector |  Id. de objeto del usuario de Azure AD |    49c4641c-ab91-4248-aebb-6a7de286397b |
| UPN | Bot, conector | UPN de usuario de Azure AD | john.smith@microsoft.com |

#### <a name="user-mention-in-bots-with-adaptive-cards"></a>Mención de usuario en bots con Tarjetas adaptables 

Los bots admiten la mención de usuario con el Id. de objeto de Azure AD y el UPN, además de los identificadores existentes. La compatibilidad con dos nuevos identificadores está disponible en bots para mensajes de texto, cuerpo de Tarjetas adaptables y respuesta de extensión de mensajería. Los bots admiten los id. de mención en escenarios de conversaciones y `invoke`. El usuario recibe una notificación de fuente de actividades cuando se le @menciona con los identificadores. 

> [!NOTE]
> La actualización del esquema y los cambios en la interfaz de usuario y la experiencia de usuario, no son necesarios para las menciones de usuario con Tarjetas adaptables en bot.

##### <a name="example"></a>Ejemplo 

Ejemplo de mención de usuario en bots con Tarjetas adaptables:

```json 
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "version": "1.0",
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Hi <at>Adele UPN</at>, <at>Adele Azure AD</at>"
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
        "text": "<at>Adele Azure AD</at>",
        "mentioned": {
          "id": "87d349ed-44d7-43e1-9a83-5f2406dee5bd",
          "name": "Adele Vance"
        }
      }
    ]
  }
}
```

La siguiente imagen ilustra la mención de usuario con la Tarjeta adaptable en bot:

![Mención de usuario en bot con Tarjeta adaptable](~/assets/images/authentication/user-mention-in-bot.png)

#### <a name="user-mention-in-incoming-webhook-with-adaptive-cards"></a>Mención de usuario en Webhook entrante con Tarjetas adaptables 

Los webhooks entrantes comienzan a admitir la mención de usuario en Tarjetas adaptables con el Id.de objeto de Azure AD y el UPN.

> [!NOTE]    
> * Habilite la mención de usuario en el esquema para que los webhooks entrantes admitan el Id. de objeto de Azure AD y el UPN. 
> * No se requieren cambios en la interfaz y/o experiencia de usuario para las menciones de usuario con el Id. de objeto de Azure AD y el UPN.      

##### <a name="example"></a>Ejemplo 

Ejemplo de mención de usuario en Webhook entrante:

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
                    "text": "Hi <at>Adele UPN</at>, <at>Adele Azure AD</at>"
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
                        "text": "<at>Adele Azure AD</at>",
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

La siguiente imagen ilustra la mención de usuario en Webhook entrante:

![Mención de usuario en Webhook entrante](~/assets/images/authentication/user-mention-in-incoming-webhook.png)

### <a name="information-masking-in-adaptive-cards"></a>Enmascaramiento de información en Tarjetas adaptables

Use la propiedad de enmascaramiento de información para enmascarar información específica, por ejemplo, contraseñas o información confidencial de los usuarios dentro del elemento de entrada [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) de la Tarjeta adaptable.

> [!NOTE]
> La función sólo admite el enmascaramiento de información del lado del cliente. El texto de entrada enmascarado se envía como texto claro a la dirección del punto final HTTPS que se especificó durante la [configuración del bot](../../build-your-first-app/build-bot.md#4-register-your-bot-endpoint).

Para enmascarar la información en Tarjetas adaptables, agregue la propiedad `style` al **tipo** `input.text` y establezca su valor en **contraseña**.

#### <a name="sample-adaptive-card-with-masking-property"></a>Tarjeta adaptable de ejemplo con propiedad de enmascaramiento

El código siguiente muestra un ejemplo de Tarjeta adaptable con propiedad de enmascaramiento:

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
},
```

La siguiente imagen es un ejemplo de enmascaramiento de la información en Tarjetas adaptables:

![Imagen de enmascaramiento de la información](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a>Tarjeta adaptable de ancho completo

Puede usar la propiedad `msteams` para expandir el ancho de una Tarjeta adaptable y usar espacio de lienzo adicional. En la siguiente sección se proporciona información sobre cómo usar la propiedad.

#### <a name="construct-full-width-cards"></a>Crear tarjetas de ancho completo

Para crear una Tarjeta adaptable de ancho completo, el objeto de la propiedad en el contenido de la tarjeta `width` `msteams` debe establecerse en `Full`.

#### <a name="sample-adaptive-card-with-full-width"></a>Tarjeta adaptable de ejemplo con ancho completo

Para crear una Tarjeta adaptable de ancho completo, la aplicación debe incluir los elementos del siguiente ejemplo de código:

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

La siguiente imagen muestra una Tarjeta adaptable de ancho completo:

![Vista de Tarjeta adaptable de ancho completo](../../assets/images/cards/full-width-adaptive-card.png)

La siguiente imagen muestra la vista predeterminada de la Tarjeta adaptable cuando no se ha establecido la propiedad `width` en **ancho completo**:

![Vista de Tarjeta adaptable de ancho pequeño](../../assets/images/cards/small-width-adaptive-card.png)

### <a name="typeahead-support"></a>Compatibilidad con TypeAhead

Dentro del elemento de esquema [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html), pedir a los usuarios que filtren y seleccionen un número considerable de opciones puede ralentizar de manera significativa la finalización de tareas. La compatibilidad con TypeAhead en Tarjetas adaptables puede simplificar la selección de entrada limitando o filtrando el conjunto de opciones de entrada a medida que el usuario escribe la entrada.

Para habilitar TypeAhead en `Input.Choiceset`, establezca `style` en `filtered` y asegúrese de que `isMultiSelect` está establecido en `false`.

#### <a name="sample-adaptive-card-with-typeahead-support"></a>Tarjeta adaptable de ejemplo con compatibilidad con TypeAhead

En el siguiente código se muestra un ejemplo de Tarjeta adaptable con compatibilidad con TypeAhead:

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

### <a name="stage-view-for-images-in-adaptive-cards"></a>Vista extendida para imágenes en Tarjetas adaptables

En una Tarjeta adaptable, puede usar la propiedad `msteams` para agregar la capacidad de mostrar imágenes en la vista extendida de forma selectiva. Cuando los usuarios mantienen el puntero sobre las imágenes, pueden ver un icono de expandir, para el que el atributo `allowExpand` está establecido en `true`. Para obtener información sobre cómo usar la propiedad, vea el siguiente ejemplo:

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

Cuando los usuarios mantienen el puntero sobre la imagen, aparece un icono de expandir en la esquina superior derecha, como se muestra en la siguiente imagen:

![Tarjeta adaptable con imagen expandible](../../assets/images/cards/adaptivecard-hover-expand-icon.png)

La imagen aparece en la vista extendida cuando el usuario selecciona el icono expandir como se muestra en la siguiente imagen:

![Imagen expandida a vista extendida](../../assets/images/cards/adaptivecard-expand-image.png)

En la vista extendida, los usuarios pueden acercar y alejar la imagen. Puede seleccionar las imágenes de la Tarjeta adaptable que han de llevar esta funcionalidad.

> [!NOTE]
> * La funcionalidad de acercar y alejar solo se aplica a los elementos de imagen que son tipo de imagen en una Tarjeta adaptable.
> * Para las aplicaciones móviles de Teams, la funcionalidad de vista extendida para imágenes en Tarjetas adaptables está disponible de forma predeterminada. Los usuarios pueden ver imágenes de Tarjeta adaptable en la vista extendida al pulsar en la imagen, independientemente de si el atributo `allowExpand` esté presente o no.

# <a name="markdown-format-for-office-365-connector-cards"></a>[Formato Markdown para tarjetas del conector de Office 365](#tab/connector-md)

Las tarjetas de conector admiten formato Markdown y HTML limitado.

| Estilo | Ejemplo | Markdown |
| --- | --- | --- |
| Negrita | **text** | `**text**` |
| Italic | *text* | `*text*` |
| Encabezado (niveles 1&ndash;3) | **Texto** | `### Text`|
| Tachado | ~~text~~ | `~~text~~` |
| Lista no ordenada | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| Lista ordenada | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Texto con formato previo | `text` | ``preformatted text`` |
| Blockquote | >texto de Blockquote | `>blockquote text` |
| Hyperlink | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| Vínculo de imagen |![Pato sobre una roca](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

En las tarjetas de conector, las líneas nuevas se representan para `\n\n`, pero no para `\n` o `\r`.

### <a name="mobile-and-desktop-differences-for-connector-cards"></a>Diferencias entre dispositivos móviles y de escritorio en tarjetas de conector

En el escritorio, el formato Markdown para tarjetas de conector aparece como se muestra en la siguiente imagen:

![Formato Markdown para tarjetas de conector en el cliente de escritorio](../../assets/images/cards/connector-desktop-markdown-combined.png)

En iOS, el formato Markdown para tarjetas de conector aparece como se muestra en la siguiente imagen:

![Formato Markdown para tarjetas de conector en el cliente de iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

Las tarjetas de conector que usan Markdown para iOS muestran los siguientes problemas:

* El cliente de iOS para Teams no representa imágenes alineadas de Markdown o HTML en tarjetas de conector.
* Los Blockquotes se representan como sangría pero sin un fondo gris.

En Android, el formato Markdown para tarjetas de conector aparece como se muestra en la siguiente imagen:

![Formato Markdown para tarjetas de conector en el cliente Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="format-example-for-markdown-connector-cards"></a>Ejemplo de formato para tarjetas de conector de Markdown

El siguiente código muestra un ejemplo de formato para tarjetas de conector Markdown:

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

* Tarjetas del conector de Office 365: en las tarjetas del conector de Office 365 se admite formato HTML y Markdown limitado.
* Tarjetas de miniatura y de elemento principal: las etiquetas HTML son compatibles con tarjetas sencillas, como las tarjetas de miniatura y de elemento principal.

El formato es diferente entre las versiones de escritorio y de móvil de Teams para tarjetas del conector de Office 365 y tarjetas sencillas. En esta sección, puede consultar el ejemplo de formato HTML para tarjetas de conector y tarjetas sencillas.

# <a name="html-format-for-office-365-connector-cards"></a>[Formato HTML para tarjetas del conector de Office 365](#tab/connector-html)

Las tarjetas de conector admiten formato Markdown y HTML limitado.

| Estilo | Ejemplo | HTML |
| --- | --- | --- |
| Negrita | **text** | `<strong>text</strong>` |
| Italic | *text* | `<em>text</em>` |
| Encabezado (niveles 1&ndash;3) | **Texto** | `<h3>Text</h3>` |
| Tachado | ~~text~~ | `<strike>text</strike>` |
| Lista no ordenada | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| Lista ordenada | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| Texto con formato previo | `text` | `<pre>text</pre>` |
| Blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| Hyperlink | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| Vínculo de imagen | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

En las tarjetas de conector, las líneas nuevas se representan en HTML mediante la etiqueta `<p>`.

### <a name="mobile-and-desktop-differences-for-connector-cards"></a>Diferencias entre dispositivos móviles y de escritorio en tarjetas de conector

En el escritorio, el formato HTML para tarjetas de conector aparece como se muestra en la siguiente imagen:

![Formato HTML para tarjetas de conector en el cliente de escritorio](../../assets/images/cards/Connector-desktop-html-combined.png)

En iOS, el formato HTML aparece como se muestra en la siguiente imagen:

![Formato HTML para tarjetas de conector en el cliente de iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

Las tarjetas de conector que usan HTML para iOS muestran los siguientes problemas:

* Las imágenes alineadas no se representan en iOS con Markdown o HTML en tarjetas de conector.
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

# <a name="html-format-for-hero-and-thumbnail-cards"></a>[Formato HTML para tarjetas de miniatura y de elemento principal](#tab/simple-html)

Las etiquetas HTML son compatibles con las tarjetas simples, como las tarjetas miniaturas y de elemento principal. No se admite Markdown.

| Estilo | Ejemplo | HTML |
| --- | --- | --- |
| Negrita | **text** | `<strong>text</strong>` |
| Italic | *text* | `<em>text</em>` |
| Encabezado (niveles 1&ndash;3) | **Texto** | `<h3>Text</h3>` |
| Tachado | ~~text~~ | `<strike>text</strike>` |
| Lista no ordenada | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| Lista ordenada | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| Texto con formato previo | `text` | `<pre>text</pre>` |
| Blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| Hyperlink | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| Vínculo de imagen |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>Diferencias entre dispositivos móviles y de escritorio en tarjetas sencillas

Dado que existen diferencias de resolución entre la plataforma móvil y de escritorio, el formato es diferente entre la versión de escritorio y la versión móvil de Teams.

En el escritorio, el formato HTML aparece como se muestra en la siguiente imagen:

![Formato HTML en el cliente de escritorio](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

En iOS, el formato HTML aparece como se muestra en la siguiente imagen:

![Formato HTML en el cliente de iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

El formato de caracteres, como negrita y cursiva, no se representa en iOS.

En Android, el formato HTML aparece como se muestra en la siguiente imagen:

![Formato HTML en el cliente Android](../../assets/images/cards/card-formatting-xml-android-60.png)

El formato de caracteres, como negrita y cursiva, se muestra correctamente en Android.

### <a name="format-example-for-simple-cards"></a>Ejemplo de formato para tarjetas sencillas

Las imágenes de la sección anterior se crearon con **App Studio** de Teams, donde la propiedad de texto de una tarjeta de elemento principal se establece en la siguiente cadena:

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

Puede probar el formato en sus tarjetas modificando este código.

---

## <a name="see-also"></a>Vea también

* [Acciones de tarjeta](./cards-actions.md)
* [Uso de módulos de tareas desde los bots](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* [Módulos de tareas](~/task-modules-and-cards/cards/cards-format.md)
* [Formatear los mensajes del bot](~/bots/how-to/format-your-bot-messages.md)

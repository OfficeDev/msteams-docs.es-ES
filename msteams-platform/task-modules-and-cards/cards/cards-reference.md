---
title: Referencia de tarjetas
description: Describe todas las tarjetas y las acciones de tarjetas disponibles para bots en Microsoft Teams.
keywords: referencia de tarjetas de bots
ms.openlocfilehash: 7bd1cbea0aec03913c9bce205ae68eedba284637
ms.sourcegitcommit: 1b909fb9ccf6cdd84ed0d8f9ea0463243a802a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "45434548"
---
# <a name="cards-reference"></a>Referencia de tarjetas

Las tarjetas que se enumeran en esta sección se admiten en bots para Teams. Se basan en tarjetas definidas por el marco de bot, pero Microsoft Teams no admite todas las tarjetas del marco de trabajo de Bot y ha agregado algunas de ellas. Las diferencias se denominan en las siguientes referencias.

## <a name="card-examples"></a>Ejemplos de tarjetas

Puede encontrar información adicional sobre cómo usar las tarjetas en la documentación del SDK de bot Builder (V3). También hay ejemplos de código disponibles en el repositorio Microsoft/BotBuilder-samples en GitHub.

* .NET
  * [Agregar tarjetas como datos adjuntos a los mensajes](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [Código de ejemplo de tarjetas (bot Builder V3)](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* Node.js
  * [Agregar tarjetas como datos adjuntos a los mensajes](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [Código de ejemplo de tarjetas (bot Builder V3)](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a>Tipos de tarjetas

En esta tabla se muestran los tipos de tarjetas disponibles.

| Tipo de tarjeta | Descripción |
| --- | --- |
| [Tarjeta adaptable](#adaptive-card) | Tarjeta altamente personalizable que puede contener cualquier combinación de texto, voz, imágenes, botones y campos de entrada. |
| [Tarjeta Hero](#hero-card) | Normalmente contiene una sola imagen grande, uno o más botones y una pequeña cantidad de texto. |
| [Tarjeta de lista](#list-card) | Una lista de desplazamiento de elementos. |
| [Tarjeta de conector de Office 365](#office-365-connector-card) | Diseño flexible con varias secciones, campos, imágenes y acciones. |
| [Tarjeta de recepción](#receipt-card) | Proporciona una confirmación al usuario. |
| [Tarjeta de inicio de sesión](#signin-card) | Permite que un bot solicite que un usuario inicie sesión. |
| [Tarjeta en miniatura](#thumbnail-card) | Normalmente contiene una sola imagen en miniatura, un texto breve y uno o más botones. |
| [Colecciones de tarjetas](#card-collections) | Se usa para devolver varios elementos en una sola respuesta |

## <a name="common-properties-for-all-cards"></a>Propiedades comunes de todas las tarjetas

### <a name="inline-card-images"></a>Imágenes de tarjetas en línea

La tarjeta puede contener una imagen incorporada incluyendo un vínculo a la imagen disponible públicamente. Por motivos de rendimiento, se recomienda hospedar la imagen en una red de entrega de contenido (CDN) pública.

Las imágenes se escalan hacia arriba o hacia abajo en el tamaño, a la vez que mantienen la relación de aspecto para cubrir el área de la imagen y, a continuación, se cortan del centro para obtener la relación de aspecto adecuada para la tarjeta.

Las imágenes deben ser como máximo 1024 × 1024 y 1 MB en formato PNG, JPEG o GIF; GIF animado no es compatible oficialmente.

| Propiedad | Tipo  | Descripción |
| --- | --- | --- |
| url | URL | Dirección URL HTTPS a la imagen |
| alt | Cadena | Descripción accesible de la imagen |

### <a name="buttons"></a>Botones

Los botones se muestran apilados en la parte inferior de la tarjeta. El texto del botón siempre está en una sola línea y se truncará si el texto supera el ancho del botón. No se mostrarán los botones adicionales que superen el número máximo que admite la tarjeta.

Consulte [acciones](~/task-modules-and-cards/cards/cards-actions.md) de la tarjeta para obtener más información.

### <a name="card-formatting"></a>Formato de tarjeta

Vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md) para obtener más información sobre el formato del texto en las tarjetas.

## <a name="adaptive-card"></a>Tarjeta adaptable

Una tarjeta personalizable que puede contener cualquier combinación de texto, voz, imágenes, botones y campos de entrada. *Vea* [tarjetas adaptables v 1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).

### <a name="support-for-adaptive-cards"></a>Compatibilidad con tarjetas adaptables

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

> [!NOTE]
> Actualmente, los elementos multimedia no se admiten en las tarjetas adaptables v 1.2 en la plataforma de Microsoft Teams.

### <a name="example-adaptive-card"></a>Tarjeta adaptable de ejemplo

![Ejemplo de tarjeta de tarjeta adaptable](~/assets/images/cards/adaptivecard.png)

```json
{
  "contentType": "application/vnd.microsoft.card.adaptive",
  "content": {
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
      {
        "type": "Container",
        "items": [
          {
            "type": "TextBlock",
            "text": "Publish Adaptive Card schema",
            "weight": "bolder",
            "size": "medium"
          },
          {
            "type": "ColumnSet",
            "columns": [
              {
                "type": "Column",
                "width": "auto",
                "items": [
                  {
                    "type": "Image",
                    "url": "https://pbs.twimg.com/profile_images/3647943215/d7f12830b3c17a5a9e4afcc370e3a37e_400x400.jpeg",
                    "size": "small",
                    "style": "person"
                  }
                ]
              },
              {
                "type": "Column",
                "width": "stretch",
                "items": [
                  {
                    "type": "TextBlock",
                    "text": "Matt Hidinger",
                    "weight": "bolder",
                    "wrap": true
                  },
                  {
                    "type": "TextBlock",
                    "spacing": "none",
                    "text": "Created {{DATE(2017-02-14T06:08:39Z, SHORT)}}",
                    "isSubtle": true,
                    "wrap": true
                  }
                ]
              }
            ]
          }
        ]
      },
      {
        "type": "Container",
        "items": [
          {
            "type": "TextBlock",
            "text": "Now that we have defined the main rules and features of the format, we need to produce a schema and publish it to GitHub. The schema will be the starting point of our reference documentation.",
            "wrap": true
          },
          {
            "type": "FactSet",
            "facts": [
              {
                "title": "Board:",
                "value": "Adaptive Card"
              },
              {
                "title": "List:",
                "value": "Backlog"
              },
              {
                "title": "Assigned to:",
                "value": "Matt Hidinger"
              },
              {
                "title": "Due date:",
                "value": "Not set"
              }
            ]
          }
        ]
      }
    ],
    "actions": [
      {
        "type": "Action.ShowCard",
        "title": "Set due date",
        "card": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Input.Date",
              "id": "dueDate"
            }
          ],
          "actions": [
            {
              "type": "Action.Submit",
              "title": "OK"
            }
          ]
        }
      },
      {
        "type": "Action.ShowCard",
        "title": "Comment",
        "card": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Input.Text",
              "id": "comment",
              "isMultiline": true,
              "placeholder": "Enter your comment"
            }
          ],
          "actions": [
            {
              "type": "Action.Submit",
              "title": "OK"
            }
          ]
        }
      }
    ]
  }  
}
```

#### <a name="for-more-information-on-adaptive-cards"></a>Para obtener más información sobre las tarjetas adaptables

* [Introducción a las tarjetas adaptables](/adaptive-cards/)
* [Acciones de tarjeta adaptable en Microsoft Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a>Tarjeta Hero

Una tarjeta que normalmente contiene una sola imagen grande, uno o más botones y texto.

### <a name="support-for-hero-cards"></a>Soporte para tarjetas de héroe

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="properties-of-a-hero-card"></a>Propiedades de una tarjeta Hero

| Propiedad | Tipo  | Description |
| --- | --- | --- |
| title | Texto enriquecido  | Título de la tarjeta. 2 líneas como máximo; formato no compatible actualmente |
| subtítulo | Texto enriquecido  | Subtítulo de la tarjeta. 2 líneas como máximo; formato no compatible actualmente |
| text | Texto enriquecido  | El texto aparece justo debajo del subtítulo; ver el formato de la [tarjeta](~/task-modules-and-cards/cards/cards-format.md) para las opciones de formato |
| incluidas | Matriz de imágenes | Imagen que se muestra en la parte superior de la tarjeta. Relación de aspecto 16:9 |
| situados | Matriz de objetos Action | Conjunto de acciones que se aplican a la tarjeta actual. Máximo de 6 |
| toque | Action (objeto) | Esta acción se activará cuando el usuario pulse en la tarjeta |
|

### <a name="example-hero-card"></a>Ejemplo de tarjeta de héroe

![Ejemplo de una tarjeta de héroe](~/assets/images/cards/hero.png)

```json
{
   "contentType": "application/vnd.microsoft.card.hero",
   "content": {
     "title": "Seattle Center Monorail",
     "subtitle": "Seattle Center Monorail",
     "text": "The Seattle Center Monorail is an elevated train line between Seattle Center (near the Space Needle) and downtown Seattle. It was built for the 1962 World's Fair. Its original two trains, completed in 1961, are still in service.",
     "images": [
       {
         "url":"https://upload.wikimedia.org/wikipedia/commons/thumb/4/49/Seattle_monorail01_2008-02-25.jpg/1024px-Seattle_monorail01_2008-02-25.jpg"
       }
     ],
    "buttons": [
      {
         "type": "openUrl",
         "title": "Official website",
         "value": "https://www.seattlemonorail.com"
       },
      {
        "type": "openUrl",
        "title": "Wikipeda page",
        "value": "https://en.wikipedia.org/wiki/Seattle_Center_Monorail"
       }
     ]
   }
}

```

### <a name="for-more-information-on-hero-cards"></a>Para obtener más información sobre las tarjetas de Heroes

Referencia de la estructura de bot:

* [Nodo de tarjeta Hero](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [Tarjeta de héroe C #](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0)

## <a name="list-card"></a>Tarjeta de lista

La tarjeta de lista se ha agregado por Microsoft Teams para proporcionar funciones que van más allá de lo que la colección de lista puede proporcionar. La tarjeta de lista proporciona una lista desplazable de elementos.

### <a name="support-for-list-cards"></a>Compatibilidad con tarjetas de lista

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ |✔ |
|

### <a name="properties-of-a-list-card"></a>Propiedades de una tarjeta de lista

| Propiedad | Tipo  | Description |
| --- | --- | --- |
| title | Texto enriquecido  | Título de la tarjeta. 2 líneas como máximo; formato no compatible actualmente |
| items | Matriz de elementos de lista  ||
| situados | Matriz de objetos Action | Conjunto de acciones que se aplican a la tarjeta actual. Máximo 6. No se representa en dispositivos móviles. |
|

### <a name="example-list-card"></a>Tarjeta de lista de ejemplo

```json
{
  "contentType": "application/vnd.microsoft.teams.card.list",
  "content": {
    "title": "Card title",
    "items": [
      {
        "type": "file",
        "id": "https://contoso.sharepoint.com/teams/new/Shared%20Documents/Report.xlsx",
        "title": "Report",
        "subtitle": "teams > new > design",
        "tap": {
          "type": "imBack",
          "value": "editOnline https://contoso.sharepoint.com/teams/new/Shared%20Documents/Report.xlsx"
        }
      },
      {
        "type": "resultItem",
        "icon": "https://cdn2.iconfinder.com/data/icons/social-icons-33/128/Trello-128.png",
        "title": "Trello title",
        "subtitle": "A Trello subtitle",
        "tap": {
          "type": "openUrl",
          "value": "http://trello.com"
        }
      },
      {
        "type": "section",
        "title": "Manager"
      },
      {
        "type": "person",
        "id": "JohnDoe@contoso.com",
        "title": "John Doe",
        "subtitle": "Manager",
        "tap": {
          "type": "imBack",
          "value": "whois JohnDoe@contoso.com"
        }
      }
    ],
    "buttons": [
      {
        "type": "imBack",
        "title": "Select",
        "value": "whois"
      }
    ]
  }
}
```

## <a name="office-365-connector-card"></a>Tarjeta de conector de Office 365

Compatible con Microsoft Teams, no con bot Framework.

La tarjeta de conexión de Office 365 proporciona un diseño flexible con varias secciones, campos, imágenes y acciones. Esta tarjeta encapsula una tarjeta de conector para que los bots puedan usarla. Vea la sección Notas para ver las diferencias entre las tarjetas de conector y la tarjeta de O365.

### <a name="support-for-office-365-connector-cards"></a>Compatibilidad con tarjetas de conector de Office 365

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✔ | ✖ |
|

### <a name="properties-of-the-office-365-connector-card"></a>Propiedades de la tarjeta de conector de Office 365

| Propiedad | Tipo  | Description |
| --- | --- | --- |
| title | Texto enriquecido  | Título de la tarjeta. 2 líneas como máximo; formato no compatible actualmente |
| summary | Texto enriquecido  | Resumen de la tarjeta. 2 líneas como máximo; formato no compatible actualmente |
| text | Texto enriquecido  | El texto aparece justo debajo del subtítulo; ver el formato de la [tarjeta](~/task-modules-and-cards/cards/cards-format.md) para las opciones de formato |
| themeColor | Cadena hexadecimal | color que reemplaza a la accentColor proporcionada desde el manifiesto de la aplicación |

### <a name="notes-on-the-office-365-connector-card"></a>Notas en la tarjeta de conector de Office 365

Las tarjetas de conexión de Office 365 funcionan correctamente en Microsoft Teams, incluidas [las acciones ActionCard](/outlook/actionable-messages/card-reference#actioncard-action).

Una diferencia importante entre el uso de tarjetas conectoras de un conector y el uso de tarjetas conector en el bot es el control de las acciones de la tarjeta.

* Para un conector, el extremo recibe la carga de la tarjeta a través de HTTP POST.
* Para un bot, la `HttpPOST` acción desencadena una `invoke` actividad que envía sólo el identificador y el cuerpo de la acción al bot.

Cada tarjeta de conector puede mostrar un máximo de 10 secciones y cada sección puede contener un máximo de 5 imágenes y 5 acciones.

> [!NOTE]
> No se mostrarán secciones, imágenes o acciones adicionales en un mensaje.

Todos los campos de texto admiten Markdown y HTML. Puede controlar qué secciones utilizan Markdown o HTML estableciendo la `markdown` propiedad en un mensaje. De forma predeterminada, `markdown` se establece en `true` ; si desea usar HTML en su lugar, establezca `markdown` en `false` .

Si especifica la `themeColor` propiedad, esta invalida la `accentColor` propiedad en el manifiesto de la aplicación.

Para especificar el estilo de representación de `activityImage` , puede establecer `activityImageType` lo siguiente:

| Valor | Descripción |
| --- | --- |
| `avatar` | Predeterminada se `activityImage` recortará como un círculo |
| `article` | `activityImage`se mostrará como un rectángulo y conservará su relación de aspecto. |

Para obtener más información acerca de las propiedades de la tarjeta de conector, consulte la referencia de la [tarjeta de mensaje accionable](/outlook/actionable-messages/card-reference). Las únicas propiedades de tarjeta de conector que Microsoft Teams no admite actualmente son las siguientes:

* `heroImage`
* `hideOriginalBody`
* `startGroup`(se trata siempre como `true` en Microsoft Teams)
* `originator`
* `correlationId`

### <a name="example-office-365-connector-card"></a>Ejemplo de tarjeta de conector de Office 365

```json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "summary": "John Doe commented on Trello",
    "title": "Project Tango",
    "sections": [
        {
            "activityTitle": "John Doe commented",
            "activitySubtitle": "On Project Tango",
            "activityText": "\"Here are the designs\"",
            "activityImage": "http://connectorsdemo.azurewebsites.net/images/MSC12_Oscar_002.jpg"
        },
        {
            "title": "Details",
            "facts": [
                {
                    "name": "Labels",
                    "value": "Designs, redlines"
                },
                {
                    "name": "Due date",
                    "value": "Dec 7, 2016"
                },
                {
                    "name": "Attachments",
                    "value": "[final.jpg](http://connectorsdemo.azurewebsites.net/images/WIN14_Jan_04.jpg)"
                }
            ]
        },
        {
            "title": "Images",
            "images": [
                {
                    "image":"http://connectorsdemo.azurewebsites.net/images/MicrosoftSurface_024_Cafe_OH-06315_VS_R1c.jpg"
                },
                {
                    "image":"http://connectorsdemo.azurewebsites.net/images/WIN12_Scene_01.jpg"
                },
                {
                    "image":"http://connectorsdemo.azurewebsites.net/images/WIN12_Anthony_02.jpg"
                }
            ]
        }
    ],
    "potentialAction": [
        {
            "@context": "http://schema.org",
            "@type": "ViewAction",
            "name": "View in Trello",
            "target": [
                "https://trello.com/c/1101/"
            ]
        }
    ]
  }
}
```

## <a name="receipt-card"></a>Tarjeta de recepción

Se admite en Microsoft Teams.

Tarjeta que permite a un bot proporcionar una confirmación al usuario. Normalmente, contiene la lista de elementos que se deben incluir en la recepción, la información total y fiscal y otro texto.

### <a name="support-for-receipts-cards"></a>Soporte para tarjetas de recepción

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="for-more-information-on-receipt-cards"></a>Para obtener más información sobre las tarjetas de recepción

Referencia de la estructura de bot:

* [Nodo tarjeta de recepción](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest)
* [Tarjeta de recepción C #](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0)

## <a name="signin-card"></a>Tarjeta de inicio de sesión

Tarjeta que permite a un bot solicitar que un usuario inicie sesión. Se admite en Teams de una forma ligeramente diferente a la que se encuentra en el marco de robots. La tarjeta de inicio de sesión de Microsoft Teams es similar a la tarjeta de inicio de sesión en el marco de bot, con la excepción de que la tarjeta de inicio de sesión de Teams solo admite dos acciones: `signin` y `openUrl` .

La *acción de inicio de sesión* se puede usar desde cualquier tarjeta en Teams, no solo desde la tarjeta de inicio de sesión. Para obtener más información sobre la autenticación, vea el tema sobre el [flujo de autenticación de Microsoft Teams para bots](~/bots/how-to/authentication/auth-flow-bot.md) .

### <a name="support-for-signin-cards"></a>Compatibilidad con tarjetas de inicio de sesión

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |
|

### <a name="for-more-information-on-signin-cards"></a>Para obtener más información sobre las tarjetas de inicio de sesión

Referencia de la estructura de bot:

* [Nodo de tarjeta de inicio de sesión](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest)
* [Tarjeta de inicio de sesión C #](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0)

## <a name="thumbnail-card"></a>Tarjeta en miniatura

Una tarjeta que normalmente contiene una sola imagen en miniatura, uno o más botones y texto.

### <a name="support-for-thumbnail-cards"></a>Compatibilidad con tarjetas de miniaturas

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

![Ejemplo de una tarjeta en miniatura](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a>Propiedades de una tarjeta en miniatura

| Propiedad | Tipo  | Description |
| --- | --- | --- |
| title | Texto enriquecido  | Título de la tarjeta. 2 líneas como máximo; formato no compatible actualmente |
| subtítulo | Texto enriquecido  | Subtítulo de la tarjeta. 2 líneas como máximo; formato no compatible actualmente |
| text | Texto enriquecido  | El texto aparece justo debajo del subtítulo; ver el formato de la [tarjeta](~/task-modules-and-cards/cards/cards-format.md) para las opciones de formato |
| incluidas | Matriz de imágenes | Imagen que se muestra en la parte superior de la tarjeta. Relación de aspecto 1:1 (cuadrado) |
| situados | Matriz de objetos Action | Conjunto de acciones que se aplican a la tarjeta actual. Máximo de 6 |
| toque | Action (objeto) | Esta acción se activará cuando el usuario pulse en la tarjeta |
|

### <a name="example-thumbnail-card"></a>Tarjeta de miniaturas de ejemplo

```json
{
  "contentType": "application/vnd.microsoft.card.thumbnail",
  "content": {
    "title": "Bender",
    "subtitle": "tale of a robot who dared to love",
    "text": "Bender Bending Rodríguez is a main character in the animated television series Futurama. He was created by series creators Matt Groening and David X. Cohen, and is voiced by John DiMaggio",
    "images": [
      {
        "url": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
        "alt": "Bender Rodríguez"
      }
    ],
    "buttons": [
      {
        "type": "imBack",
        "title": "Thumbs Up",
        "image": "http://moopz.com/assets_c/2012/06/emoji-thumbs-up-150-thumb-autox125-140616.jpg",
        "value": "I like it"
      },
      {
        "type": "imBack",
        "title": "Thumbs Down",
        "image": "http://yourfaceisstupid.com/wp-content/uploads/2014/08/thumbs-down.png",
        "value": "I don't like it"
      },
      {
        "type": "openUrl",
        "title": "I feel lucky",
        "image": "http://thumb9.shutterstock.com/photos/thumb_large/683806/148441982.jpg",
        "value": "https://www.bing.com/images/search?q=bender&qpvt=bender&qpvt=bender&qpvt=bender&FORM=IGRE"
      }
    ],
    "tap": {
      "type": "imBack",
      "value": "Tapped it!"
    }
  }
}
```

### <a name="for-more-information"></a>Más información

Referencia de la estructura de bot:

* [Nodo de tarjeta en miniatura](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest)
* [Tarjeta en miniatura C #](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0)

## <a name="card-collections"></a>Colecciones de tarjetas

Las colecciones de tarjetas se admiten en Microsoft Teams.

Las colecciones de tarjetas las proporciona el marco de bot: `builder.AttachmentLayout.carousel` y `builder.AttachmentLayout.list` . Estas colecciones pueden contener tarjetas adaptables, de héroe o de miniaturas.

## <a name="carousel-collection"></a>Colección carrusel

El [diseño carrusel](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0) muestra un carrusel de tarjetas, opcionalmente con botones de acción asociados.

### <a name="support-for-carousel-collections"></a>Compatibilidad con colecciones de carrusel

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |
|

> [!NOTE]
> Un carrusel puede mostrar un máximo de 10 tarjetas por mensaje.

### <a name="example-carousel-collection"></a>Colección de carrusel de ejemplo

![Ejemplo de un carrusel de tarjetas](~/assets/images/cards/carousel.png)

Las propiedades son las mismas que para el héroe o la tarjeta en miniatura.

### <a name="syntax-for-carousel-collections"></a>Sintaxis para colecciones de carrusel

`builder.AttachmentLayout.carousel`

## <a name="list-collection"></a>Colección List

### <a name="support-for-list-collections"></a>Compatibilidad con colecciones de listas

El diseño de lista muestra una lista apilada verticalmente de tarjetas, opcionalmente con botones de acción asociados.

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="example-list-collection"></a>Colección de lista de ejemplo

![Ejemplo de una lista de tarjetas](~/assets/images/cards/list.png)

Las propiedades son las mismas que para el héroe o la tarjeta en miniatura.

Una lista puede mostrar un máximo de 10 tarjetas por mensaje.

> [!NOTE]
> Algunas combinaciones de tarjetas de lista aún no se admiten en iOS y Android.

### <a name="syntax-for-list-collections"></a>Sintaxis para colecciones de listas

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a>Tarjetas no admitidas en Microsoft Teams

El marco de bot implementa las siguientes tarjetas, pero no son compatibles con Microsoft Teams.

* Tarjetas de animación
* Tarjetas de audio
* Tarjetas de vídeo

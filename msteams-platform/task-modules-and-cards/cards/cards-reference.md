---
title: Referencia de tarjetas
description: Describe todas las tarjetas y acciones de tarjeta disponibles para bots en Teams
keywords: Referencia de tarjetas bots
ms.topic: reference
ms.openlocfilehash: 839430baa5ce5e8950a21a1472036c6fd96f4edf
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911899"
---
# <a name="cards-reference"></a>Referencia de tarjetas

Las tarjetas enumeradas en esta sección son compatibles con bots para Microsoft Teams. Se basan en tarjetas definidas por Bot Framework, pero Teams no admite todas las tarjetas de Bot Framework y ha agregado algunas de sus propias tarjetas. Las diferencias se llaman en las referencias de este documento.

## <a name="card-examples"></a>Ejemplos de tarjetas

Puede encontrar información adicional sobre cómo usar tarjetas en la documentación del SDK de Bot Builder (v3). Los ejemplos de código también están disponibles en el repositorio de Microsoft/BotBuilder-Samples en GitHub.

* .NET
  * [Agregar tarjetas como datos adjuntos a los mensajes](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [Código de ejemplo de tarjetas (Bot Builder v3)](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* Node.js
  * [Agregar tarjetas como datos adjuntos a los mensajes](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [Código de ejemplo de tarjetas (Bot Builder v3)](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a>Tipos de tarjetas

En esta tabla se muestran los tipos de tarjetas disponibles:

| Tipo de tarjeta | Description |
| --- | --- |
| [Tarjeta adaptable](#adaptive-card) | Tarjeta altamente personalizable que puede contener cualquier combinación de texto, voz, imágenes, botones y campos de entrada. |
| [Tarjeta principal](#hero-card) | Normalmente contiene una sola imagen grande, uno o más botones y una pequeña cantidad de texto. |
| [Tarjeta de lista](#list-card) | Una lista de desplazamiento de elementos. |
| [Tarjeta de conector de Office 365](#office-365-connector-card) | Diseño flexible con varias secciones, campos, imágenes y acciones. |
| [Tarjeta de recibo](#receipt-card) | Proporciona una confirmación al usuario. |
| [Tarjeta de inicio de sesión](#signin-card) | Permite que un bot solicite que un usuario inicie sesión. |
| [Tarjeta en miniatura](#thumbnail-card) | Normalmente contiene una sola imagen en miniatura, texto corto y uno o más botones. |
| [Colecciones de tarjetas](#card-collections) | Se usa para devolver varios elementos en una sola respuesta. |

## <a name="common-properties-for-all-cards"></a>Propiedades comunes para todas las tarjetas

### <a name="inline-card-images"></a>Imágenes de tarjetas en línea

La tarjeta puede contener una imagen en línea incluyendo un vínculo a la imagen disponible públicamente. Por motivos de rendimiento, se recomienda encarecidamente hospedar la imagen en una red de entrega de contenido (CDN) pública.

Las imágenes se escalan hacia arriba o hacia abajo en tamaño mientras se mantiene la relación de aspecto para cubrir el área de la imagen y, a continuación, se recortan desde el centro para lograr la relación de aspecto adecuada para la tarjeta.

Las imágenes deben tener como máximo 1024×1024, en formato PNG, JPEG o GIF, y no se admite gif animado.

| Propiedad | Tipo  | Description |
| --- | --- | --- |
| url | URL | DIRECCIÓN URL HTTPS a la imagen |
| alt | Cadena | Descripción accesible de la imagen |

### <a name="buttons"></a>Botones

Los botones se muestran apilados en la parte inferior de la tarjeta. El texto del botón siempre está en una sola línea y se truncará si el texto supera el ancho del botón. No se mostrarán botones adicionales más allá del número máximo admitido por la tarjeta.

Vea [Acciones de tarjeta](~/task-modules-and-cards/cards/cards-actions.md) para obtener más información.

### <a name="card-formatting"></a>Formato de tarjeta

Consulta [Formato de tarjeta para](~/task-modules-and-cards/cards/cards-format.md) obtener más información sobre el formato de texto en las tarjetas.

## <a name="adaptive-card"></a>Tarjeta adaptable

Una tarjeta adaptable es una tarjeta personalizable que puede contener cualquier combinación de texto, voz, imágenes, botones y campos de entrada. Consulta [tarjetas adaptables v1.2.0.](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)

### <a name="support-for-adaptive-cards"></a>Compatibilidad con tarjetas adaptables

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

> [!NOTE]
> * La plataforma de Teams admite la versión 1.2 o anterior de las características de tarjeta adaptable.
> * Actualmente, los elementos multimedia no se admiten en la tarjeta adaptable v1.2 en la plataforma teams.

### <a name="example-of-an-adaptive-card"></a>Ejemplo de una tarjeta adaptable

![Ejemplo de una tarjeta adaptable](~/assets/images/cards/adaptivecard.png)

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

#### <a name="additional-information-on-adaptive-cards"></a>Información adicional sobre tarjetas adaptables

* [Introducción a las tarjetas adaptables](/adaptive-cards/)
* [Acciones de tarjeta adaptable en Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a>Tarjeta principal

Una tarjeta que normalmente contiene una sola imagen grande, uno o más botones y texto.

### <a name="support-for-hero-cards"></a>Compatibilidad con tarjetas de imagen principal

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="properties-of-a-hero-card"></a>Propiedades de una tarjeta principal

| Propiedad | Tipo  | Description |
| --- | --- | --- |
| title | Texto enriquecido  | Título de la tarjeta. Máximo de 2 líneas. |
| subtitle | Texto enriquecido  | Subtítulo de la tarjeta. Máximo de 2 líneas.|
| text | Texto enriquecido  | El texto aparece justo debajo del subtítulo; vea [Formato de tarjeta para](~/task-modules-and-cards/cards/cards-format.md) obtener más información sobre las opciones de formato. |
| imágenes | Matriz de imágenes | Imagen que se muestra en la parte superior de la tarjeta. Relación de aspecto 16:9. |
| botones | Matriz de objetos de acción | Conjunto de acciones aplicables a la tarjeta actual. Máximo 6. |
| pulsación | Action (objeto) | Esta acción se activará cuando el usuario pulse en la propia tarjeta. |

### <a name="example-of-a-hero-card"></a>Ejemplo de una tarjeta principal

![Ejemplo de una tarjeta principal](~/assets/images/cards/hero.png)

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

### <a name="additional-information-on-hero-cards"></a>Información adicional sobre las tarjetas de identificación principal

Referencia de Bot Framework:

* [Nodo de tarjeta principal](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [Tarjeta principal C #](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="list-card"></a>Tarjeta de lista

Teams ha agregado la tarjeta de lista para proporcionar funciones más allá de lo que puede proporcionar la colección de listas. La tarjeta de lista proporciona una lista de elementos de desplazamiento.

### <a name="support-for-list-cards"></a>Compatibilidad con tarjetas de lista

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ |✔ |

### <a name="properties-of-a-list-card"></a>Propiedades de una tarjeta de lista

| Propiedad | Tipo  | Description |
| --- | --- | --- |
| title | Texto enriquecido  | Título de la tarjeta. Máximo de 2 líneas.|
| items | Matriz de elementos de lista  ||
| botones | Matriz de objetos de acción | Conjunto de acciones aplicables a la tarjeta actual. Máximo 6. |

### <a name="example-of-a-list-card"></a>Ejemplo de una tarjeta de lista

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

La tarjeta del conector de Office 365 se admite en Teams, no en Bot Framework. Esta tarjeta proporciona un diseño flexible con varias secciones, campos, imágenes y acciones. Esta tarjeta encapsula una tarjeta de conector para que la puedan usar los bots. Vea la sección de notas para ver las diferencias entre las tarjetas de conector y la tarjeta O365.

### <a name="support-for-office-365-connector-cards"></a>Compatibilidad con tarjetas de conector de Office 365

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✔ | ✖ |

### <a name="properties-of-the-office-365-connector-card"></a>Propiedades de la tarjeta de conector de Office 365

| Propiedad | Tipo  | Description |
| --- | --- | --- |
| title | Texto enriquecido  | Título de la tarjeta. Máximo de 2 líneas. |
| summary | Texto enriquecido  | Resumen de la tarjeta. Máximo de 2 líneas. |
| text | Texto enriquecido  | El texto aparece justo debajo del subtítulo; vea [Formato de tarjeta para](~/task-modules-and-cards/cards/cards-format.md) obtener más información sobre las opciones de formato. |
| themeColor | Cadena HEX | Color que reemplaza el accentColor proporcionado desde el manifiesto de la aplicación. |

### <a name="notes-on-the-office-365-connector-card"></a>Notas en la tarjeta de conector de Office 365

Las tarjetas de conector de Office 365 funcionan correctamente en Microsoft Teams, incluidas [las acciones actionCard](/outlook/actionable-messages/card-reference#actioncard-action).

Una diferencia importante entre el uso de tarjetas de conector desde un conector y el uso de tarjetas de conector en el bot es el control de las acciones de tarjeta.

* Para un conector, el extremo recibe la carga de la tarjeta a través de HTTP POST.
* Para un bot, la acción desencadena una actividad que envía solo el identificador de acción `HttpPOST` y el cuerpo al `invoke` bot.

Cada tarjeta de conector puede mostrar un máximo de 10 secciones y cada sección puede contener un máximo de 5 imágenes y 5 acciones.

> [!NOTE]
> Las secciones, imágenes o acciones adicionales de un mensaje no aparecerán.

Todos los campos de texto admiten Markdown y HTML. Puede controlar qué secciones usan Markdown o HTML estableciendo la `markdown` propiedad en un mensaje. De forma predeterminada, `markdown` se establece en ; si desea usar HTML en su `true` lugar, establezca en `markdown` `false` .

Si especificas la `themeColor` propiedad, esta invalida la `accentColor` propiedad en el manifiesto de la aplicación.

Para especificar el estilo de representación `activityImage` para , puede establecer lo `activityImageType` siguiente:

| Valor | Description |
| --- | --- |
| `avatar` | Valor predeterminado; `activityImage` se recortará como un círculo. |
| `article` | `activityImage` se mostrará como un rectángulo y conservará su relación de aspecto. |

Para obtener todos los demás detalles acerca de las propiedades de la tarjeta de conector, vea la [referencia de tarjeta de mensaje que puede acción.](/outlook/actionable-messages/card-reference) Las únicas propiedades de tarjeta de conector que Microsoft Teams no admite actualmente son las siguientes:

* `heroImage`
* `hideOriginalBody`
* `startGroup` (siempre se trata como `true` en Teams)
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a>Ejemplo de una tarjeta de conector de Office 365

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

## <a name="receipt-card"></a>Tarjeta de recibo

Teams admite la tarjeta de recibo. Es una tarjeta que permite a un bot proporcionar un recibo al usuario. Normalmente contiene la lista de elementos que se deben incluir en el recibo, como los impuestos y la información total.

### <a name="support-for-receipt-cards"></a>Compatibilidad con tarjetas de recibo

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="example-of-a-receipt-card"></a>Ejemplo de una tarjeta de recibo

![Ejemplo de una tarjeta de recibo](~/assets/images/cards/receipt.png)

```json
{
  "contentType": "application/vnd.microsoft.card.receipt",
  "content": {
    "title": "John Doe",
    "facts": [
      {
        "key": "Order Number",
        "value": "1234"
      },
      {
        "key": "Payment Method",
        "value": "VISA 5555-****"
      }
    ],
    "items": [
      {
        "title": "Data Transfer",
        "image": {
          "url": "https://github.com/amido/azure-vector-icons/raw/master/renders/traffic-manager.png"
        },
        "price": "$ 38.45",
        "quantity": "368"
      },
      {
        "title": "App Service",
        "image": {
          "url": "https://github.com/amido/azure-vector-icons/raw/master/renders/cloud-service.png"
        },
        "price": "$ 45.00",
        "quantity": "720"
      }
    ],
    "total": "$ 90.95",
    "tax": "$ 7.50",
    "buttons": [
      {
        "type": "openUrl",
        "title": "More information",
        "image": "https://account.windowsazure.com/content/6.10.1.38-.8225.160809-1618/aux-pre/images/offer-icon-freetrial.png",
        "value": "https://azure.microsoft.com/en-us/pricing/"
      }
    ]
  }
}
```

### <a name="additional-information-on-receipt-cards"></a>Información adicional sobre las tarjetas de recibo

Referencia de Bot Framework:

* [Nodo de tarjeta de recibo](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [Tarjeta de recibo C #](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="signin-card"></a>Tarjeta de inicio de sesión

La tarjeta de inicio de sesión permite a un bot solicitar a un usuario que inicie sesión. Se admite en Teams de una forma ligeramente diferente a la que se encuentra en Bot Framework. La tarjeta de inicio de sesión en Teams es similar a la tarjeta de inicio de sesión en Bot Framework, excepto que la tarjeta de inicio de sesión en Teams solo admite dos acciones: `signin` y `openUrl` .

La *acción de inicio de* sesión se puede usar desde cualquier tarjeta de Teams, no solo desde la tarjeta de inicio de sesión. Para obtener más información sobre la autenticación, vea [el flujo de autenticación de Microsoft Teams para bots.](~/bots/how-to/authentication/auth-flow-bot.md)

### <a name="support-for-signin-cards"></a>Compatibilidad con tarjetas de inicio de sesión

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |

### <a name="additional-information-on-signin-cards"></a>Información adicional sobre las tarjetas de inicio de sesión

Referencia de Bot Framework:

* [Nodo de tarjeta de inicio de sesión](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [Tarjeta de inicio de sesión C #](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="thumbnail-card"></a>Tarjeta en miniatura

Una tarjeta que normalmente contiene una sola imagen en miniatura, uno o más botones y texto.

### <a name="support-for-thumbnail-cards"></a>Compatibilidad con tarjetas en miniatura

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

![Ejemplo de una tarjeta en miniatura](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a>Propiedades de una tarjeta en miniatura

| Propiedad | Tipo  | Description |
| --- | --- | --- |
| title | Texto enriquecido  | Título de la tarjeta. Máximo de 2 líneas.|
| subtitle | Texto enriquecido  | Subtítulo de la tarjeta. Máximo de 2 líneas.|
| text | Texto enriquecido  | El texto aparece justo debajo del subtítulo; vea [Formato de tarjeta para](~/task-modules-and-cards/cards/cards-format.md) obtener más información sobre las opciones de formato. |
| imágenes | Matriz de imágenes | Imagen que se muestra en la parte superior de la tarjeta. Relación de aspecto 1:1 (cuadrado). |
| botones | Matriz de objetos de acción | Conjunto de acciones aplicables a la tarjeta actual. Máximo 6. |
| pulsación | Action (objeto) | Esta acción se activará cuando el usuario pulse en la propia tarjeta. |

### <a name="example-of-a-thumbnail-card"></a>Ejemplo de una tarjeta en miniatura

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

### <a name="additional-information"></a>Información adicional

Referencia de Bot Framework:

* [Nodo de tarjeta en miniatura](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [Tarjeta en miniatura C #](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="card-collections"></a>Colecciones de tarjetas

Teams admite colecciones de tarjetas.

Colecciones de tarjetas: `builder.AttachmentLayout.carousel` y `builder.AttachmentLayout.list` . Estas colecciones contienen tarjetas adaptables, de imagen principal o en miniatura.

## <a name="carousel-collection"></a>Carrusel (colección)

El [diseño de carrusel](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true) muestra un carrusel de tarjetas, opcionalmente con botones de acción asociados.

### <a name="support-for-carousel-collections"></a>Compatibilidad con colecciones de carrusel

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |

> [!NOTE]
> Un carrusel puede mostrar un máximo de 10 tarjetas por mensaje.

### <a name="properties-of-a-carousel-card"></a>Propiedades de una tarjeta de carrusel

Las propiedades de una tarjeta de carrusel son las mismas que las de las tarjetas Hero y Thumbnail.

### <a name="example-of-a-carousel-collection"></a>Ejemplo de una colección de carrusel

![Ejemplo de un carrusel de tarjetas](~/assets/images/cards/carousel.png)

```json
{
 "attachmentLayout": "carousel",
 "attachments":[
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "extraLarge",
                "weight": "bolder",
                "text": "Welcome to Employee Connect",
                "height": "stretch"
              },
              {
                "type": "TextBlock",
                "size": "medium",
                "weight": "bolder",
                "text": "Add events to your calendar",
                "height": "stretch"
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "The bot can send \r\rnotification to remind \r\ryou about the latest \r\revents and trainings.",
                "wrap": true,
                "height": "stretch"
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    },
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.2",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "large",
                "weight": "bolder",
                "text": "Employee connect"
              },
              {
                "type": "TextBlock",
                "text": "The bot can send notifications \r\rto remind you about the latest \r\r events and trainings",
                "wrap": true,
                "maxWidth": 2
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    },
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "large",
                "weight": "bolder",
                "text": "Employee Connect final"
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "Create and manage your tasks",
                "wrap": true
              },
              {
                "type": "TextBlock",
                "text": "The app identifies all your pending tasks \r\r and helps you manage everything at \r\r one place.",
                "wrap": true
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "Try these commands \r\r- Pending Submissions \r\r- Pending Approvals- My Tools",
                "wrap": true,
                "height": "stretch"
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    }
  ]
}
```

### <a name="syntax-for-carousel-collections"></a>Sintaxis para colecciones de carrusel

`builder.AttachmentLayoutTypes.Carousel`

## <a name="list-collection"></a>Colección de listas

### <a name="support-for-list-collections"></a>Compatibilidad con colecciones de listas

El diseño de lista muestra una lista apilada verticalmente de tarjetas, opcionalmente con botones de acción asociados.

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="example-of-a-list-collection"></a>Ejemplo de una colección de listas

![Ejemplo de una lista de tarjetas](~/assets/images/cards/list.png)

Las propiedades son las mismas que para la tarjeta principal o en miniatura.

Una lista puede mostrar un máximo de 10 tarjetas por mensaje.

> [!NOTE]
> Algunas combinaciones de tarjetas de lista aún no se admiten en iOS y Android.

### <a name="syntax-for-list-collections"></a>Sintaxis para colecciones de listas

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a>Tarjetas no admitidas en Teams

Bot Framework implementa las siguientes tarjetas, pero Teams no las admite.

* Tarjetas de animación
* Tarjetas de audio
* Tarjetas de vídeo

---
title: Tipos de tarjetas
description: Describe todas las tarjetas y acciones de tarjeta disponibles para bots en Teams
localization_priority: Normal
keywords: referencia de tarjetas bots
ms.topic: reference
ms.openlocfilehash: 4c386b3e237f89345bf94bc8cfa23d7e46477de21da0e7a99eb63663b19446af
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2021
ms.locfileid: "57705510"
---
# <a name="types-of-cards"></a>Tipos de tarjetas

Adaptive, hero, list, Office 365 Connector, receipt, signin, and thumbnail cards and card collections are supported in bots for Microsoft Teams. Se basan en tarjetas definidas por Bot Framework, pero Teams no admite todas las tarjetas de Bot Framework y ha agregado algunas de sus propias.

Antes de identificar los distintos tipos de tarjeta, comprenda cómo crear una tarjeta de héroe, una tarjeta en miniatura o una tarjeta adaptable.

## <a name="create-a-hero-card-thumbnail-card-or-adaptive-card"></a>Crear una tarjeta de héroe, una tarjeta en miniatura o una tarjeta adaptable

**Para crear una tarjeta de héroe, una miniatura o una tarjeta adaptable desde App Studio**

1. Ve a **App Studio** desde Teams.
1. Seleccione **Editor de tarjetas**.
1. Seleccione **Crear una nueva tarjeta**.
1. Seleccione **Crear** para una de las tarjetas de **hero card**, Thumbnail **Card** o Adaptive **Card**. Los detalles de metadatos, los botones y los ejemplos de código json, csharp y node se muestran para esa tarjeta.

    ![Detalles de la tarjeta de héroe](~/assets/images/Cards/Herocarddetails.png)

1. Seleccione **Enviarme esta tarjeta**. La tarjeta se envía como un mensaje de chat.

## <a name="card-examples"></a>Ejemplos de tarjetas

Encontrará información adicional sobre cómo usar tarjetas en la documentación del SDK de Bot Builder v3. Los ejemplos de código también están disponibles en el **repositorio microsoft/BotBuilder-Samples** en GitHub. A continuación se muestran algunos ejemplos de tarjetas:

* .NET
  * [Agregar tarjetas como datos adjuntos a los mensajes](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).
  * [Código de ejemplo de tarjetas Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).

* Node.js
  * [Agregar tarjetas como datos adjuntos a los mensajes](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).
  * [Código de ejemplo de tarjetas Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).

## <a name="card-types"></a>Tipos de tarjeta

Puede identificar y usar diferentes tipos de tarjetas según los requisitos de la aplicación. En la tabla siguiente se muestran los tipos de tarjetas disponibles:

| Tipo de tarjeta | Descripción |
| --- | --- |
| [Tarjeta adaptable](#adaptive-card) | Esta tarjeta es altamente personalizable y puede contener cualquier combinación de texto, voz, imágenes, botones y campos de entrada. |
| [Tarjeta de héroe](#hero-card) | Esta tarjeta normalmente contiene una sola imagen grande, uno o varios botones y una pequeña cantidad de texto. |
| [Tarjeta de lista](#list-card) | Esta tarjeta contiene una lista de desplazamiento de elementos. |
| [Office 365 Tarjeta de conector](#office-365-connector-card) | Esta tarjeta tiene un diseño flexible con varias secciones, campos, imágenes y acciones. |
| [Tarjeta de recibo](#receipt-card) | Esta tarjeta proporciona un recibo al usuario. |
| [Tarjeta de inicio de sesión](#signin-card) | Esta tarjeta permite que un bot solicite que un usuario inicia sesión. |
| [Tarjeta miniatura](#thumbnail-card) | Esta tarjeta normalmente contiene una sola imagen en miniatura, texto corto y uno o más botones. |
| [Colecciones de tarjetas](#card-collections) | Esta colección de tarjetas se usa para devolver varios elementos en una sola respuesta. |

## <a name="features-that-support-different-card-types"></a>Características que admiten distintos tipos de tarjeta

| Tipo de tarjeta | Bots | Vistas previas de extensión de mensaje | Resultados de extensión de mensaje | Módulos de tareas | Webhooks salientes | Webhooks entrantes | Conectores de O365 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Tarjeta adaptable | ✔ | ✖ | ✔ | ✔ | ✔ | ✔ | ✖ |
| Tarjeta O365 Connector | ✔ | ✖ | ✔ | ✖ | ✔ | ✔ | ✔ |
| Tarjeta de héroe | ✔ | ✔ | ✔ | ✖ | ✔ | ✔ | ✖ |
| Tarjeta miniatura | ✔ | ✔ | ✔ | ✖ | ✔ | ✔ | ✖ |
| Tarjeta de lista | ✔ | ✖ | ✖ | ✖ | ✔ | ✔ | ✖ |
| Tarjeta de recibo | ✔ | ✖ | ✖ | ✖ | ✖ | ✔ | ✖ |
| Tarjeta de inicio de sesión | ✔ | ✖ | ✖ | ✖ | ✖ | ✖ | ✖ |

> [!NOTE]
> Para las tarjetas adaptables en webhooks entrantes, todos los elementos de esquema nativos de tarjeta adaptable, excepto `Action.Submit` , son totalmente compatibles. Las acciones admitidas [**son Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)y [**Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).

## <a name="common-properties-for-all-cards"></a>Propiedades comunes para todas las tarjetas

Puedes ir a través de algunas propiedades comunes que son aplicables a todas las tarjetas.

### <a name="inline-card-images"></a>Imágenes de tarjetas en línea

La tarjeta puede contener una imagen en línea al incluir un vínculo a la imagen disponible públicamente. Por motivos de rendimiento, se recomienda hospedar la imagen en un servidor público Content Delivery Network (CDN).

Las imágenes se escalan hacia arriba o hacia abajo en tamaño para mantener la relación de aspecto para cubrir el área de imagen. A continuación, las imágenes se recortan desde el centro para lograr la relación de aspecto adecuada para la tarjeta.

Las imágenes deben tener como máximo 1024×1024 y en formato PNG, JPEG o GIF. Gif animado no es compatible.

En la tabla siguiente se proporcionan las propiedades de las imágenes de tarjetas en línea:

| Propiedad | Tipo  | Descripción |
| --- | --- | --- |
| url | URL | DIRECCIÓN URL HTTPS a la imagen. |
| alt | Cadena | Descripción accesible de la imagen. |

> [!NOTE]
> Si una tarjeta incluye una dirección URL de imagen que se redirige antes de la imagen final, no se admite el redireccionamiento en la dirección URL de la imagen. Esto ocurre para las imágenes compartidas en la nube pública.

### <a name="buttons"></a>Botones

Los botones se muestran apilados en la parte inferior de la tarjeta. El texto del botón siempre está en una sola línea y se trunca si el texto supera el ancho del botón. No se muestran los botones adicionales que supere el número máximo admitido por la tarjeta.

Para obtener más información, vea [acciones de tarjeta](~/task-modules-and-cards/cards/cards-actions.md).

### <a name="card-formatting"></a>Formato de tarjeta

Para obtener más información sobre el formato de texto en tarjetas, vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).

Después de identificar las propiedades comunes de todas las tarjetas, ahora puedes trabajar con tarjetas adaptables, lo que te ayudará a aumentar la interacción y la eficacia agregando el contenido que se puede usar directamente en las aplicaciones que usas.

## <a name="adaptive-card"></a>Tarjeta adaptable

> [!VIDEO https://www.youtube-nocookie.com/embed/J12lKt717Ws]

Una tarjeta adaptable es una tarjeta personalizable que puede contener cualquier combinación de texto, voz, imágenes, botones y campos de entrada. Para obtener más información, vea [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).

### <a name="support-for-adaptive-cards"></a>Compatibilidad con tarjetas adaptables

En la tabla siguiente se proporcionan las características que admiten tarjetas adaptables:

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

> [!NOTE]
> * Teams plataforma admite v1.2 o versiones anteriores de características de tarjeta adaptable.
> * El estilo de acción positiva o destructiva no se admite en tarjetas adaptables en la Teams web.
> * Actualmente, los elementos multimedia no se admiten en la tarjeta adaptable en Teams plataforma.

### <a name="example-of-adaptive-card"></a>Ejemplo de tarjeta adaptable

![Ejemplo de una tarjeta adaptable](~/assets/images/cards/adaptivecard.png)

El código siguiente muestra un ejemplo de una tarjeta adaptable:

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

Referencia de Bot Framework:

* [Nodo de tarjetas adaptables](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [Tarjeta adaptable C #](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

Ahora puedes trabajar con una tarjeta de héroe, que es una tarjeta multipropósito que se usa para resaltar visualmente una selección de usuario potencial.

## <a name="hero-card"></a>Tarjeta de héroe

Una tarjeta que normalmente contiene una sola imagen grande, uno o varios botones y texto.

### <a name="support-for-hero-cards"></a>Compatibilidad con tarjetas de héroe

En la tabla siguiente se proporcionan las características que admiten tarjetas de héroe:

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="properties-of-a-hero-card"></a>Propiedades de una tarjeta de héroe

En la tabla siguiente se proporcionan las propiedades de una tarjeta de héroe:

| Propiedad | Tipo  | Description |
| --- | --- | --- |
| title | Texto enriquecido  | Título de la tarjeta. Máximo dos líneas. |
| subtitle | Texto enriquecido  | Subtítulo de la tarjeta. Máximo dos líneas.|
| text | Texto enriquecido  | El texto aparece debajo del subtítulo. Para ver las opciones de formato, vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md). |
| imágenes | Matriz de imágenes | Imagen que se muestra en la parte superior de la tarjeta. Relación de aspecto 16:9. |
| botones | Matriz de objetos de acción | Conjunto de acciones aplicables a la tarjeta actual. Máximo seis. |
| pulsación | Action (objeto) | Se activa cuando el usuario pulsa en la propia tarjeta. |

### <a name="example-of-a-hero-card"></a>Ejemplo de una tarjeta de héroe

![Ejemplo de una tarjeta de héroe](~/assets/images/cards/hero.png)

El siguiente código muestra un ejemplo de una tarjeta de héroe:

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

### <a name="additional-information-on-hero-cards"></a>Información adicional sobre tarjetas de héroe

Referencia de Bot Framework:

* [Tarjeta de Node.js](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [Tarjeta de héroe C #](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a>Tarjeta de lista

La tarjeta de lista se ha agregado Teams para proporcionar funciones más allá de lo que la colección de listas puede proporcionar. La tarjeta de lista proporciona una lista de desplazamiento de elementos.

### <a name="support-for-list-cards"></a>Compatibilidad con tarjetas de lista

En la tabla siguiente se proporcionan las características que admiten tarjetas de lista:

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ |✔ |

### <a name="properties-of-a-list-card"></a>Propiedades de una tarjeta de lista

En la tabla siguiente se proporcionan las propiedades de una tarjeta de lista:

| Propiedad | Tipo  | Description |
| --- | --- | --- |
| title | Texto enriquecido  | Título de la tarjeta. Máximo de 2 líneas.|
| elementos | Matriz de elementos de lista | Conjunto de elementos aplicables a la tarjeta.|
| botones | Matriz de objetos de acción | Conjunto de acciones aplicables a la tarjeta actual. Máximo 6. |

### <a name="example-of-a-list-card"></a>Ejemplo de una tarjeta de lista

El siguiente código muestra un ejemplo de una tarjeta de lista:

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

## <a name="office-365-connector-card"></a>Office 365 de conector

Puede trabajar con una tarjeta Office 365 Connector que proporciona un diseño flexible y es una excelente manera de obtener información útil. La Office 365 de conector se admite en Teams, no en Bot Framework. Esta tarjeta proporciona un diseño flexible con varias secciones, campos, imágenes y acciones. Esta tarjeta contiene una tarjeta de conector para que la puedan usar los bots. Para obtener más información sobre las diferencias entre las tarjetas de conector y la Office 365 connector, consulte Información adicional [sobre la Office 365 connector](#additional-information-on-the-office-365-connector-card).

### <a name="support-for-office-365-connector-cards"></a>Compatibilidad con tarjetas Office 365 Connector

En la tabla siguiente se proporcionan las características que admiten Office 365 de conector:

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✔ | ✖ |

### <a name="properties-of-the-office-365-connector-card"></a>Propiedades de la tarjeta Office 365 Connector

En la tabla siguiente se proporcionan las propiedades de la Office 365 de conector:

| Propiedad | Tipo  | Description |
| --- | --- | --- |
| title | Texto enriquecido  | Título de la tarjeta. Máximo dos líneas. |
| summary | Texto enriquecido  | Resumen de la tarjeta. Máximo dos líneas. |
| text | Texto enriquecido  | El texto aparece debajo del subtítulo. Para ver las opciones de formato, vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md). |
| themeColor | Cadena HEX | Color que invalida el `accentColor` proporcionado desde el manifiesto de la aplicación. |

### <a name="additional-information-on-the-office-365-connector-card"></a>Información adicional sobre la tarjeta Office 365 Connector

Office 365 Las tarjetas de conector funcionan correctamente Microsoft Teams, incluidas las [ `ActionCard` acciones](/outlook/actionable-messages/card-reference#actioncard-action).

La diferencia importante entre usar tarjetas de conector desde un conector y usar tarjetas de conector en el bot es el control de las acciones de tarjeta. En la tabla siguiente se muestra la diferencia:

| Connector | Bot |
| --- | --- |
| El extremo recibe la carga de la tarjeta a través de HTTP POST. | La acción desencadena una actividad que envía solo el identificador de acción `HttpPOST` y el cuerpo al `invoke` bot.|

Cada tarjeta de conector puede mostrar un máximo de diez secciones y cada sección puede contener un máximo de cinco imágenes y cinco acciones.

> [!NOTE]
> Las secciones, imágenes o acciones adicionales de un mensaje no aparecen.

Todos los campos de texto admiten Markdown y HTML. Puede controlar qué secciones usan Markdown o HTML estableciendo la `markdown` propiedad en un mensaje. De forma predeterminada, `markdown` se establece en `true` . Si quiere usar HTML en su lugar, establezca `markdown` en `false` .

Si especifica la `themeColor` propiedad, invalida la `accentColor` propiedad en el manifiesto de la aplicación.

Para especificar el estilo de representación `activityImage` para , puede `activityImageType` establecerlo como se muestra en la tabla siguiente:

| Valor | Descripción |
| --- | --- |
| `avatar` | Valor predeterminado, `activityImage` se recorta como un círculo. |
| `article` | `activityImage` se muestra como un rectángulo y conserva su relación de aspecto. |

Para obtener todos los demás detalles acerca de las propiedades de la tarjeta de conector, vea [referencia de tarjeta de mensaje que puede actuar.](/outlook/actionable-messages/card-reference) Las únicas propiedades de tarjeta de conector que Teams admite actualmente son las siguientes:

* `heroImage`
* `hideOriginalBody`
* `startGroup`siempre tratado como `true` en Teams
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a>Ejemplo de una tarjeta Office 365 Connector

El siguiente código muestra un ejemplo de una tarjeta Office 365 Connector:

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

Teams admite tarjeta de recibo. Es una tarjeta que permite a un bot proporcionar un recibo al usuario. Normalmente contiene la lista de elementos que se deben incluir en el recibo, como impuestos y la información total.

### <a name="support-for-receipt-cards"></a>Compatibilidad con tarjetas de recibo

En la tabla siguiente se proporcionan las características que admiten tarjetas de recibo:

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="example-of-a-receipt-card"></a>Ejemplo de una tarjeta de recibo

![Ejemplo de una tarjeta de recibo](~/assets/images/cards/receipt.png)

El siguiente código muestra un ejemplo de una tarjeta de recibo:

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

### <a name="additional-information-on-receipt-cards"></a>Información adicional sobre tarjetas de recibo

Referencia de Bot Framework:

* [Tarjeta de recibo Node.js](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [Tarjeta de recibo C #](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a>Tarjeta de inicio de sesión

La tarjeta de inicio de sesión en Teams es similar a la tarjeta de inicio de sesión en Bot Framework, excepto que la tarjeta de inicio de sesión en Teams solo admite dos `signin` acciones y `openUrl` .

La acción de inicio de sesión se puede usar desde cualquier tarjeta de Teams, no solo desde la tarjeta de inicio de sesión. Para obtener más información, [vea Teams de autenticación para bots](~/bots/how-to/authentication/auth-flow-bot.md).

### <a name="support-for-signin-cards"></a>Compatibilidad con tarjetas de inicio de sesión

En la tabla siguiente se proporcionan las características que admiten tarjetas de inicio de sesión:

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |

### <a name="additional-information-on-signin-cards"></a>Información adicional sobre tarjetas de inicio de sesión

Referencia de Bot Framework:

* [Tarjeta de inicio de sesión Node.js](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [Tarjeta de inicio de sesión C #](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a>Tarjeta miniatura

Puedes trabajar con una tarjeta en miniatura que se usa para enviar un mensaje sencillo que puede usarse. Una tarjeta que normalmente contiene una sola imagen en miniatura, uno o varios botones y texto.

### <a name="support-for-thumbnail-cards"></a>Compatibilidad con tarjetas en miniatura

En la tabla siguiente se proporcionan las características que admiten tarjetas en miniatura:

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

![Ejemplo de una tarjeta en miniatura](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a>Propiedades de una tarjeta en miniatura

En la tabla siguiente se proporcionan las propiedades de una tarjeta en miniatura:

| Propiedad | Tipo  | Description |
| --- | --- | --- |
| title | Texto enriquecido  | Título de la tarjeta. Máximo de 2 líneas.|
| subtitle | Texto enriquecido  | Subtítulo de la tarjeta. Máximo de 2 líneas.|
| text | Texto enriquecido  | El texto aparece debajo del subtítulo. Para ver las opciones de formato, vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md). |
| imágenes | Matriz de imágenes | Imagen que se muestra en la parte superior de la tarjeta. Relación de aspecto 1:1 cuadrado. |
| botones | Matriz de objetos de acción | Conjunto de acciones aplicables a la tarjeta actual. Máximo 6. |
| pulsación | Action (objeto) | Se activa cuando el usuario pulsa en la propia tarjeta. |

### <a name="example-of-a-thumbnail-card"></a>Ejemplo de una tarjeta en miniatura

El código siguiente muestra un ejemplo de una tarjeta en miniatura:

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

* [Tarjeta en miniatura Node.js](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [Tarjeta de miniatura C #](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a>Colecciones de tarjetas

Puede trabajar con colecciones de tarjetas que incluyen colecciones de carrusel y listas. Teams admite colecciones de tarjetas. Las colecciones de tarjetas `builder.AttachmentLayout.carousel` incluyen y `builder.AttachmentLayout.list` . Estas colecciones contienen tarjetas adaptables, de héroe o en miniatura.

### <a name="carousel-collection"></a>Colección Carousel

El [diseño del carrusel](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) muestra un carrusel de tarjetas, opcionalmente con botones de acción asociados.

#### <a name="support-for-carousel-collections"></a>Compatibilidad con colecciones de carrusel

En la tabla siguiente se proporcionan las características que admiten colecciones de carrusel:

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |

> [!NOTE]
> Un carrusel puede mostrar un máximo de diez tarjetas por mensaje.

#### <a name="properties-of-a-carousel-card"></a>Propiedades de una tarjeta de carrusel

Las propiedades de una tarjeta de carrusel son las mismas que las tarjetas de miniatura y de héroe.

#### <a name="example-of-a-carousel-collection"></a>Ejemplo de una colección de carrusel

![Ejemplo de un carrusel de tarjetas](~/assets/images/cards/carousel.png)

El código siguiente muestra un ejemplo de una colección de carrusel:

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

#### <a name="syntax-for-carousel-collections"></a>Sintaxis para colecciones de carrusel

`builder.AttachmentLayoutTypes.Carousel` es la sintaxis de las colecciones de carrusel.

### <a name="list-collection"></a>Colección List

El diseño de lista muestra una lista verticalmente apilada de tarjetas, opcionalmente con botones de acción asociados.

#### <a name="support-for-list-collections"></a>Compatibilidad con colecciones de listas

En la tabla siguiente se proporcionan las características que admiten colecciones de listas:

| Bots en Teams | Extensiones de mensajería  | Conectores | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

#### <a name="example-of-a-list-collection"></a>Ejemplo de una colección de listas

![Ejemplo de una lista de tarjetas](~/assets/images/cards/list.png)

Las propiedades de las colecciones de listas son las mismas que las tarjetas de miniatura o de héroe.

Una lista puede mostrar un máximo de diez tarjetas por mensaje.

> [!NOTE]
> Algunas combinaciones de tarjetas de lista aún no son compatibles con iOS y Android.

#### <a name="syntax-for-list-collections"></a>Sintaxis para colecciones de listas

`builder.AttachmentLayout.list` es la sintaxis de las colecciones de listas.

## <a name="cards-not-supported-in-teams"></a>No se admiten tarjetas en Teams

Bot Framework implementa las siguientes tarjetas, pero no son compatibles con Teams:

* Tarjetas de animación
* Tarjetas de audio
* Tarjetas de vídeo

## <a name="see-also"></a>Vea también

* [Módulos de tareas](~/task-modules-and-cards/what-are-task-modules.md)
* [Dar formato a tarjetas](~/task-modules-and-cards/cards/cards-format.md)

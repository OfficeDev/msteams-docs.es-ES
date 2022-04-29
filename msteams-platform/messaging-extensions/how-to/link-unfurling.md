---
title: Apertura de vínculos
author: surbhigupta
description: Aprenda a agregar la apertura de enlaces con la extensión de mensajería en una aplicación de Microsoft Teams con el manifiesto de la aplicación o manualmente usando ejemplos y ejemplos de código.
ms.localizationpriority: high
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: b172320f6f116026fe5ea4b45c9c74da6ff82f07
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111251"
---
# <a name="link-unfurling"></a>Apertura de vínculos

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

En este documento se explica cómo agregar vínculos abriéndose al manifiesto de la aplicación mediante App Studio y manualmente. Con la apertura de vínculos su aplicación puede registrarse para recibir una actividad `invoke` cuando se pegan las direcciones URL con un dominio en particular en el área de redacción de mensajes. El `invoke` contiene la dirección URL completa que se pegó en el área de redacción del mensaje y puede responder con una tarjeta que el usuario puede abrir, proporcionando información o acciones adicionales. Esto funciona de forma similar a un comando de búsqueda con la dirección URL que actúa como término de búsqueda.

> [!NOTE]
>
> * Actualmente, la apertura de enlaces no es compatible con clientes móviles.
> * El resultado de la apertura del enlace se almacena en caché durante 30 minutos.

La extensión de mensajes de Azure DevOps usa la apertura de vínculos para buscar direcciones URL pegadas en el área de redacción de mensajes que apuntan a un elemento de trabajo. En la siguiente imagen, un usuario ha pegado una URL para un elemento de trabajo en Azure DevOps, que la extensión del mensaje ha resuelto en una tarjeta:

![Ejemplo de apertura de vínculos](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a>Agregue el enlace que se abre al manifiesto de su aplicación

Para agregar una apertura de enlace al manifiesto de la aplicación, agregue una nueva matriz de `messageHandlers` a la sección `composeExtensions` del JSON del manifiesto de la aplicación. Puede agregar la matriz con la ayuda de App Studio o manualmente. Las listas de dominios pueden incluir caracteres comodín, por ejemplo, `*.example.com`. Coincide exactamente con un segmento del dominio; si necesita coincidir con `a.b.example.com`, use `*.*.example.com`.

> [!NOTE]
> No agregue dominios que no estén en el control, ya sea directamente o a través de caracteres comodín. Por ejemplo, `yourapp.onmicrosoft.com` es válido, pero `*.onmicrosoft.com` no es válido. Además, los dominios de nivel superior están prohibidos. Por ejemplo, `*.com`, `*.org`.

### <a name="add-link-unfurling-using-app-studio"></a>Agregar apertura de vínculo mediante App Studio

1. Abra **App Studio** en el cliente Microsoft Teams y seleccione la pestaña **Editor de manifiestos**.
1. Cargue el manifiesto de la aplicación.
1. En la página **Extensión de mensaje**, agregue el dominio que desea buscar en la sección **Controladores de mensajes**. En la imagen siguiente se explica el proceso:

    ![sección controladores de mensajes en App Studio](~/assets/images/link-unfurling.png)

### <a name="add-link-unfurling-manually"></a>Agregar la apertura de vínculos manualmente

Para permitir que la extensión de mensaje interactúe con los vínculos, primero debe agregar la matriz de `messageHandlers` al manifiesto de la aplicación. En el ejemplo siguiente se explica cómo agregar manualmente la apertura de vínculos:

```json
...
"composeExtensions": [
  {
    "botId": "abc123456-ab12-ab12-ab12-abcdef123456",
    "messageHandlers": [
      {
        "type": "link",
        "value": {
          "domains": [
            "*.trackeddomain.com"
          ]
        }
      }
    ]
  }
],
...
```

Para obtener un ejemplo de manifiesto completo, consulte [referencia de manifiesto](~/resources/schema/manifest-schema.md).

## <a name="handle-the-composeextensionquerylink-invoke"></a>Controlar la invocación de `composeExtension/queryLink`

Después de agregar el dominio al manifiesto de aplicación, debe actualizar el código del servicio web para controlar la solicitud de invocación. Use la dirección URL recibida para buscar en el servicio y crear una respuesta de tarjeta. Si responde con más de una tarjeta, solo se usa la primera respuesta de la tarjeta.

Se admiten los siguientes tipos de tarjeta:

* [Tarjeta miniatura](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Tarjeta de héroe](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Tarjeta conector de Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Tarjeta adaptable](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Para obtener más información, vea [Invocación de tipo de acción](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke).

### <a name="example"></a>Ejemplo

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsAppBasedLinkQueryAsync(ITurnContext<IInvokeActivity> turnContext, AppBasedLinkQuery query, CancellationToken cancellationToken)
{
    //You'll use the query.link value to search your service and create a card response
    var card = new HeroCard
    {
        Title = "Hero Card",
        Text = query.Url,
        Images = new List<CardImage> { new CardImage("https://raw.githubusercontent.com/microsoft/botframework-sdk/master/icon.png") },
    };

    var attachments = new MessagingExtensionAttachment(HeroCard.ContentType, null, card);
    var result = new MessagingExtensionResult(AttachmentLayoutTypes.List, "result", new[] { attachments }, null, "test unfurl");

    return new MessagingExtensionResponse(result);
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsLinkUnfurlingBot extends TeamsActivityHandler {
  handleTeamsAppBasedLinkQuery(context, query) {
    const attachment = CardFactory.thumbnailCard('Thumbnail Card',
      query.url,
      ['https://raw.githubusercontent.com/microsoft/botframework-sdk/master/icon.png']);

    const result = {
      attachmentLayout: 'list',
      type: 'result',
      attachments: [attachment]
    };

    const response = {
      composeExtension: result
    };
    return response;
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

A continuación se muestra un ejemplo del `invoke` enviado al bot:

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

A continuación se muestra un ejemplo de la respuesta:

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "attachments": [
      {
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage&quot;: &quot;https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value&quot;: &quot;[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        }
      }
    ]
  }
}
```

* * *

## <a name="step-by-step-guide"></a>Guía paso a paso

Siga la [guía paso a paso](../../sbs-botbuilder-linkunfurling.yml) para abrir vínculos en Teams mediante bot.

## <a name="see-also"></a>Consulte también

* [Tarjetas](~/task-modules-and-cards/what-are-cards.md)
* [Abra del vínculo de las pestañas y la Vista de fases](~/tabs/tabs-link-unfurling.md)
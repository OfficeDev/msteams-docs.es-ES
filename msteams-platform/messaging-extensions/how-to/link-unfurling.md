---
title: Vincular unfurling
author: clearab
description: Cómo realizar unfurling de vínculos con la extensión de mensajería en una aplicación de Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 5b20ea303a2c3d085651a53b01af4bb449d386de
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676210"
---
# <a name="link-unfurling"></a>Vincular unfurling

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Con unfurling de vínculos se puede registrar la aplicación para `invoke` recibir una actividad cuando se pegan direcciones URL con un dominio en particular en el área de mensaje de redacción. El `invoke` contendrá la dirección URL completa que se pegó en el área de mensaje de redacción y puede responder con una tarjeta que el usuario puede *unfurl*, lo que proporciona información o acciones adicionales. Esto funciona de manera muy similar a un [comando de búsqueda](~/messaging-extensions/how-to/search-commands/define-search-command.md), con la dirección URL que actúa como el término de búsqueda.

La extensión de mensajería de Azure DevOps usa el vínculo unfurling para buscar direcciones URL pegadas en el área de mensaje de redacción que apunta a un elemento de trabajo. En la siguiente captura de pantalla, un usuario ha pegado en una dirección URL de un elemento de trabajo en Azure DevOps que la extensión de mensajería se ha resuelto en una tarjeta.

![Ejemplo de vínculo unfurling](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a>Agregar vínculo unfurling al manifiesto de la aplicación

Para ello, agregará una nueva `messageHandlers` matriz a la `composeExtensions` sección del JSON del manifiesto de la aplicación. Puede hacerlo con la ayuda de App Studio, o bien manualmente. Las listas de dominios pueden incluir caracteres comodín, por `*.example.com`ejemplo. Esto coincide exactamente con un segmento del dominio; Si tiene que hacer coincidir `a.b.example.com` , `*.*.example.com`use.

### <a name="using-app-studio"></a>Uso de App Studio

1. En App Studio, en la pestaña Editor de manifiestos, cargue el manifiesto de la aplicación.
1. En la página **extensión de mensajería** , agregue el dominio que quiera buscar en la sección **controladores de mensajes** , como se muestra en la captura de pantalla siguiente.

![sección Controladores de mensajes en App Studio](~/assets/images/link-unfurling.png)

### <a name="manually"></a>Manualmente

Para habilitar la extensión de mensajería para que interactúe con los vínculos de esta forma, primero tendrá `messageHandlers` que agregar la matriz al manifiesto de la aplicación, como en el ejemplo siguiente. Este ejemplo no es el manifiesto completo, vea el manifiesto [referencia](~/resources/schema/manifest-schema.md) para obtener un ejemplo completo de manifiesto.

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

## <a name="handle-the-composeextensionquerylink-invoke"></a>Controlar la `composeExtension/queryLink` invocación

Una vez que haya agregado el dominio para escuchar en el manifiesto de la aplicación, deberá actualizar el código del servicio web para administrar la solicitud de invocación. Use la dirección URL que reciba para buscar en el servicio y crear una respuesta de tarjeta. Si responde con más de una tarjeta, solo se usará la primera.

Se admiten los siguientes tipos de tarjeta:

* [Tarjeta en miniatura](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Tarjeta Hero](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Tarjeta de conector de Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Tarjeta adaptable](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Consulte [¿Qué son las tarjetas](~/task-modules-and-cards/what-are-cards.md) para obtener información general).

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsAppBasedLinkQueryAsync(ITurnContext<IInvokeActivity> turnContext, AppBasedLinkQuery query, CancellationToken cancellationToken)
{
    //You'll use the query.link value to search your service and create a card response
    var heroCard = new ThumbnailCard
    {
        Title = "Thumbnail Card",
        Text = query.Url,
        Images = new List<CardImage> { new CardImage("https://raw.githubusercontent.com/microsoft/botframework-sdk/master/icon.png") },
    };

    var attachments = new MessagingExtensionAttachment(HeroCard.ContentType, null, heroCard);
    var result = new MessagingExtensionResult(AttachmentLayoutTypes.List, "result", new[] { attachments }, null, "test unfurl");

    return new MessagingExtensionResponse(result);
}
```

# <a name="javascriptnodejstabjavascript"></a>[JavaScript/node. js](#tab/javascript)

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

# <a name="jsontabjson"></a>[JSON](#tab/json)

Este es un ejemplo del que `invoke` se ha enviado a su bot.

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

A continuación se muestra un ejemplo de la respuesta.

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
              "activityImage": "https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value": "[Larry Brown](mailto:larryb@example.com)"
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

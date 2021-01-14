---
title: Apertura de vínculos
author: clearab
description: Cómo realizar el desenlazaje de vínculos con la extensión de mensajería en una aplicación de Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 0d488638e63b8ec78bfa5bed8cf6f4f037883fb1
ms.sourcegitcommit: bf61ae5ad2afa4efdb0311158184d0cbb9c40174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/13/2021
ms.locfileid: "49845640"
---
# <a name="link-unfurling"></a>Apertura de vínculos

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

> [!NOTE]
> Actualmente, la desafución de vínculos no se admite en los clientes móviles.

Con el desenlazaje de vínculos, la aplicación puede registrarse para recibir una actividad cuando las direcciones URL con un dominio determinado se pegan en el `invoke` área de redacción de mensajes. Contendrá la dirección URL completa pegada en el área de redacción de mensajes, y puede responder con una tarjeta que el usuario puede deshacer, proporcionando información o acciones `invoke` adicionales.  Esto funciona de forma muy similar a un comando [de búsqueda,](~/messaging-extensions/how-to/search-commands/define-search-command.md)con la dirección URL que actúa como término de búsqueda.

La extensión de mensajería de Azure DevOps usa el desenlace de vínculos para buscar direcciones URL pegadas en el área de redacción de mensajes que apunten a un elemento de trabajo. En la siguiente captura de pantalla, un usuario ha pegado una dirección URL de un elemento de trabajo en Azure DevOps que la extensión de mensajería ha resuelto en una tarjeta.

![Ejemplo de desenlazaje de vínculos](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a>Agregar un vínculo que se desenlameje al manifiesto de la aplicación

 Para agregar el desenlazaje de vínculos al manifiesto de la aplicación, agregue una nueva matriz a la sección del JSON del `messageHandlers` `composeExtensions` manifiesto de la aplicación. Puede agregar la matriz con la ayuda de App Studio o manualmente. Las listas de dominios pueden incluir caracteres comodín, por `*.example.com` ejemplo. Esto coincide exactamente con un segmento del dominio; si necesita hacer `a.b.example.com` coincidir, use `*.*.example.com` .

> [!NOTE]
> No agregue dominios que estén fuera de su control, ya sea directamente o a través de caracteres comodín. Por ejemplo, yourapp.onmicrosoft.com es válido, pero *.onmicrosoft.com no es válido. Además, los dominios de nivel superior están prohibidos. Por ejemplo, *.com, *.org.

### <a name="using-app-studio"></a>Usar App Studio

1. En App Studio, en la pestaña Editor de manifiestos, carga el manifiesto de la aplicación.
1. En la **página Extensión de** mensajería, agregue el  dominio que desea buscar en la sección Controladores de mensajes, como en la captura de pantalla siguiente.

![sección controladores de mensajes en App Studio](~/assets/images/link-unfurling.png)

### <a name="manually"></a>Manualmente

Para permitir que la extensión de mensajería interactúe con vínculos de esta forma, primero tendrá que agregar la matriz al manifiesto de la aplicación, como en `messageHandlers` el ejemplo siguiente. Este ejemplo no es el manifiesto completo, vea [la referencia del manifiesto](~/resources/schema/manifest-schema.md) para obtener un ejemplo de manifiesto completo.

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

Una vez que haya agregado el dominio para escuchar el manifiesto de la aplicación, tendrá que actualizar el código del servicio web para controlar la solicitud de invocación. Use la dirección URL que recibe para buscar en el servicio y crear una respuesta de tarjeta. Si responde con más de una tarjeta, solo se usará la primera.

Se admiten los siguientes tipos de tarjetas:

* [Tarjeta en miniatura](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Tarjeta principal](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Tarjeta de conector de Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Tarjeta adaptable](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Consulta [Qué son las tarjetas](~/task-modules-and-cards/what-are-cards.md) para obtener información general.

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

Este es un ejemplo del `invoke` bot enviado.

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

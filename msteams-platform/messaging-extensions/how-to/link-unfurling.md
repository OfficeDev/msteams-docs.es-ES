---
title: Apertura de vínculos
author: surbhigupta
description: Cómo realizar el despliegue de vínculos con la extensión de mensajería en una Microsoft Teams aplicación.
localization_priority: Normal
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 7713fe794c9d15453438cfe3e1bde0238bde9d8c
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068951"
---
# <a name="link-unfurling"></a>Apertura de vínculos

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Este documento te guía sobre cómo agregar la actualización de vínculos al manifiesto de la aplicación con App studio y manualmente. Con la apertura de vínculos su aplicación puede registrarse para recibir una actividad `invoke` cuando se pegan las direcciones URL con un dominio en particular en el área de redacción de mensajes. Contiene la dirección URL completa pegada en el área del mensaje de redacción y puede responder con una tarjeta que el usuario pueda deshacer, proporcionando información o `invoke` acciones adicionales. Esto funciona de forma similar a un comando de búsqueda con la dirección URL que actúa como término de búsqueda.

> [!NOTE]
> * Actualmente, la desafución de vínculos no se admite en clientes móviles.
> * El resultado de la descarga de vínculos se almacena en caché durante 30 minutos.

La Azure DevOps de mensajería usa la desamuestra de vínculos para buscar direcciones URL pegadas en el área de mensaje de redacción que apunten a un elemento de trabajo. En la siguiente imagen, un usuario ha pegado una dirección URL de un elemento de trabajo en Azure DevOps, que la extensión de mensajería ha resuelto en una tarjeta:

![Ejemplo de desafusado de vínculos](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a>Agregar la implementación de vínculos al manifiesto de la aplicación

Para agregar la implementación de vínculos al manifiesto de la aplicación, agrega una nueva matriz a la sección json del manifiesto `messageHandlers` `composeExtensions` de la aplicación. Puedes agregar la matriz con la ayuda de App Studio o manualmente. Las listas de dominios pueden incluir caracteres comodín, por ejemplo `*.example.com` . Esto coincide exactamente con un segmento del dominio; si necesita hacer `a.b.example.com` coincidir, use `*.*.example.com` .

> [!NOTE]
> No agregue dominios que no estén en su control, ya sea directamente o a través de caracteres comodín. Por ejemplo, `yourapp.onmicrosoft.com` es válido, pero `*.onmicrosoft.com` no es válido. Además, los dominios de nivel superior están prohibidos. Por ejemplo, `*.com` , `*.org` .

### <a name="add-link-unfurling-using-app-studio"></a>Agregar un despliegue de vínculos con App Studio

1. Abre **App Studio** desde el Microsoft Teams y selecciona la pestaña Editor **de** manifiestos.
1. Cargue el manifiesto de la aplicación.
1. En la **página Extensión de** mensajería, agregue el dominio que desea buscar en la sección Controladores **de** mensajes. En la siguiente imagen se explica el proceso:

    ![sección controladores de mensajes en App Studio](~/assets/images/link-unfurling.png)
    
### <a name="add-link-unfurling-manually"></a>Agregar la actualización manual de vínculos

Para habilitar la extensión de mensajería para que interactúe con vínculos, primero debes agregar la `messageHandlers` matriz al manifiesto de la aplicación. En el siguiente ejemplo se explica cómo agregar manualmente la actualización de vínculos: 


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

Para obtener un ejemplo de manifiesto completo, vea [referencia de manifiesto](~/resources/schema/manifest-schema.md).

## <a name="handle-the-composeextensionquerylink-invoke"></a>Controlar la `composeExtension/queryLink` invocación

Después de agregar el dominio al manifiesto de la aplicación, debes actualizar el código del servicio web para controlar la solicitud de invocación. Use la dirección URL recibida para buscar en el servicio y crear una respuesta de tarjeta. Si responde con más de una tarjeta, solo se usará la primera respuesta de tarjeta.

Se admiten los siguientes tipos de tarjeta:

* [Tarjeta miniatura](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Tarjeta de héroe](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365 Tarjeta de conector](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Tarjeta adaptable](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

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

A continuación se muestra un ejemplo `invoke` del bot enviado:

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

## <a name="see-also"></a>Consulte también 

* [Tarjetas](~/task-modules-and-cards/what-are-cards.md)
* [Expansión del vínculo de la pestaña y vista de fases](~/tabs/tabs-link-unfurling.md)

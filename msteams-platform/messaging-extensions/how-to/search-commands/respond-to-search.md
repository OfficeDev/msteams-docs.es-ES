---
title: Responder a consultas de comandos de búsqueda
author: surbhigupta
description: Obtenga información sobre cómo responder al comando de búsqueda desde una extensión de mensaje en una aplicación de Microsoft Teams. Comprenda cómo responder a la solicitud del usuario.
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: 97fe20097e98a015759ba030004fb8c0b3b5e3f9
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/02/2022
ms.locfileid: "68819950"
---
# <a name="respond-to-search-command"></a>Responder a consultas de comandos de búsqueda

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Una vez que el usuario envía el comando de búsqueda, el servicio web recibe un `composeExtension/query` mensaje de invocación que contiene un `value` objeto con los parámetros de búsqueda. Esta invocación se desencadena con las condiciones siguientes:

* A medida que los caracteres se escriben en el cuadro de búsqueda.
* `initialRun` se establece en true en el manifiesto de la aplicación, recibirá el mensaje de invocación en cuanto se invoque el comando de búsqueda. Para obtener más información, consulte [consulta predeterminada](#default-query).

Este documento le guía sobre cómo responder a las solicitudes de usuario en forma de tarjetas y vistas previas, y las condiciones en las que Microsoft Teams emite una consulta predeterminada.

Los parámetros de solicitud se encuentran en el `value` objeto de la solicitud, que incluye las siguientes propiedades:

| Nombre de propiedad | Objetivo |
|---|---|
| `commandId` | Nombre del comando invocado por el usuario, que coincide con uno de los comandos declarados en el manifiesto de la aplicación. |
| `parameters` | Matriz de parámetros. Cada objeto de parámetro contiene el nombre del parámetro, junto con el valor de parámetro proporcionado por el usuario. |
| `queryOptions` | Parámetros de paginación: <br>`skip`: omitir el recuento de esta consulta <br>`count`: número de elementos que se van a devolver. |

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
{
  //code to handle the query
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearch extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
  //code to handle the query
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

El código JSON siguiente se abrevia para resaltar las secciones más relevantes.

```json
{
  "type": "invoke",
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "searchKeywords",
        "value": "Toronto"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
...
}
```

* * *

## <a name="respond-to-user-requests"></a>Respuesta a las solicitudes de usuario

Cuando el usuario realiza una consulta, Microsoft Teams emite una solicitud HTTP sincrónica al servicio. En ese momento, el código tiene `5` segundos para proporcionar una respuesta HTTP a la solicitud. Durante este tiempo, el servicio puede realizar búsquedas adicionales o cualquier otra lógica de negocios necesaria para atender la solicitud.

El servicio debe responder con los resultados que coincidan con la consulta del usuario. La respuesta debe indicar un código de estado HTTP de `200 OK` y una aplicación o un objeto JSON válidos con las siguientes propiedades:

|Nombre de propiedad|Objetivo|
|---|---|
|`composeExtension`|Sobre de respuesta de nivel superior.|
|`composeExtension.type`|Tipo de respuesta. Se admiten los tipos siguientes: <br>`result`: muestra una lista de resultados de búsqueda <br>`auth`: solicita al usuario que se autentique <br>`config`: solicita al usuario que configure la extensión de mensaje. <br>`message`: muestra un mensaje de texto sin formato |
|`composeExtension.attachmentLayout`|Especifica el diseño de los datos adjuntos. Se usa para respuestas de tipo `result`. <br>Actualmente, se admiten los siguientes tipos: <br>`list`: lista de objetos de tarjeta que contienen campos de miniatura, título y texto <br>`grid`: una cuadrícula de imágenes en miniatura |
|`composeExtension.attachments`|Matriz de objetos de datos adjuntos válidos. Se usa para respuestas de tipo `result`. <br>Actualmente, se admiten los siguientes tipos: <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|Acciones sugeridas. Se usa para respuestas de tipo `auth` o `config`. |
|`composeExtension.text`|Mensaje que se va a mostrar. Se usa para respuestas de tipo `message`. |

### <a name="response-card-types-and-previews"></a>Tipos y vistas previas de tarjetas de respuesta

Teams admite los siguientes tipos de tarjetas:

* [Tarjeta miniatura](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Tarjeta de héroe](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Tarjeta conector de Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Tarjeta adaptable](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Para tener una mejor comprensión e información general sobre las tarjetas, vea [qué son las tarjetas](~/task-modules-and-cards/what-are-cards.md).

Para obtener información sobre cómo usar los tipos de miniaturas y tarjetas principales, consulte [Agregar tarjetas y acciones de tarjeta](~/task-modules-and-cards/cards/cards-actions.md).

Para obtener más información sobre la tarjeta Office 365 Connector, consulte Uso de [tarjetas de conector de Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).

La lista de resultados se muestra en la interfaz de usuario de Microsoft Teams con una vista previa de cada elemento. La vista previa se genera de una de las dos maneras siguientes:

* Uso de la `preview` propiedad dentro del `attachment` objeto . Los `preview` datos adjuntos solo pueden ser un héroe o una tarjeta en miniatura.
* Extracción de las propiedades básicas `title`, `text`y `image` del `attachment` objeto . Las propiedades básicas solo se usan si no se especifica la `preview` propiedad .

En el caso de la tarjeta hero o thumbnail, excepto la acción de invocación, no se admiten otras acciones, como el botón y la pulsación, en la tarjeta de vista previa.

Para enviar una tarjeta adaptable o una tarjeta de conector de Office 365, debe incluir una versión preliminar. La `preview` propiedad debe ser una tarjeta hero o thumbnail. Si no especifica la propiedad preview en el `attachment` objeto, no se genera una vista previa.

En el caso de las tarjetas hero y thumbnail, no es necesario especificar una propiedad de vista previa; de forma predeterminada, se genera una vista previa.

### <a name="response-example"></a>Ejemplo de respuesta

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken) 
{
  var text = query?.Parameters?[0]?.Value as string ?? string.Empty;

  //searches NuGet for a package
  var obj = JObject.Parse(await (new HttpClient()).GetStringAsync($"https://azuresearch-usnc.nuget.org/query?q=id:{text}&prerelease=true"));
  var packages = obj["data"].Select(item => (item["id"].ToString(), item["version"].ToString(), item["description"].ToString()));

  // We take every row of the results and wrap them in cards wrapped in in MessagingExtensionAttachment objects.
  // The Preview is optional, if it includes a Tap, that will trigger the OnTeamsMessagingExtensionSelectItemAsync event back on this bot.
  var attachments = packages.Select(package => new MessagingExtensionAttachment
      {
          ContentType = HeroCard.ContentType,
          Content = new HeroCard { Title = package.Item1 },
          Preview = new HeroCard { Title = package.Item1, Tap = new CardAction { Type = "invoke", Value = package } }.ToAttachment()
      })
      .ToList();

  // The list of MessagingExtensionAttachments must we wrapped in a MessagingExtensionResult wrapped in a MessagingExtensionResponse.
  return new MessagingExtensionResponse
  {
      ComposeExtension = new MessagingExtensionResult
      {
          Type = "result",
          AttachmentLayout = "list",
          Attachments = attachments
      }
  };
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearchBot extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
        const searchQuery = query.parameters[0].value;
        const response = await axios.get(`http://registry.npmjs.com/-/v1/search?${ querystring.stringify({ text: searchQuery, size: 8 }) }`);

        const attachments = [];
        response.data.objects.forEach(obj => {
            const heroCard = CardFactory.heroCard(obj.package.name);
            const preview = CardFactory.heroCard(obj.package.name);
            const attachment = { ...heroCard, preview };
            attachments.push(attachment);
        });

        return {
            composeExtension: {
                type: 'result',
                attachmentLayout: 'list',
                attachments: attachments
            }
        };
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

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
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        }
      },
      {
        "contentType": "application/vnd.microsoft.card.adaptive",
        "content": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Container",
              "items": [
                {
                  "type": "TextBlock",
                  "text": "Microsoft Corp (NASDAQ: MSFT)",
                  "size": "medium",
                  "isSubtle": true
                },
                {
                  "type": "TextBlock",
                  "text": "September 19, 4:00 PM EST",
                  "isSubtle": true
                }
              ]
            },
            {
              "type": "Container",
              "spacing": "none",
              "items": [
                {
                  "type": "ColumnSet",
                  "columns": [
                    {
                      "type": "Column",
                      "width": "stretch",
                      "items": [
                        {
                          "type": "TextBlock",
                          "text": "75.30",
                          "size": "extraLarge"
                        },
                        {
                          "type": "TextBlock",
                          "text": "▼ 0.20 (0.32%)",
                          "size": "small",
                          "color": "attention",
                          "spacing": "none"
                        }
                      ]
                    },
                    {
                      "type": "Column",
                      "width": "auto",
                      "items": [
                        {
                          "type": "FactSet",
                          "facts": [
                            {
                              "title": "Open",
                              "value": "62.24"
                            },
                            {
                              "title": "High",
                              "value": "62.98"
                            },
                            {
                              "title": "Low",
                              "value": "62.20"
                            }
                          ]
                        }
                      ]
                    }
                  ]
                }
              ]
            }
          ],
          "version": "1.0"
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "Microsoft Corp (NASDAQ: MSFT)",
            "text": "75.30 ▼ 0.20 (0.32%)"
          }
        }
      }
    ]
  }
}
```

* * *

### <a name="enable-and-handle-tap-actions"></a>Habilitación y control de acciones de pulsación

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override Task<MessagingExtensionResponse> OnTeamsMessagingExtensionSelectItemAsync(ITurnContext<IInvokeActivity> turnContext, JObject query, CancellationToken cancellationToken)
{
    // The Preview card's Tap should have a Value property assigned, this will be returned to the bot in this event. 
    var (packageId, version, description, projectUrl, iconUrl) = query.ToObject<(string, string, string, string, string)>();

    var card = new ThumbnailCard
    {
        Title = "Card Select Item",
        Subtitle = description
    };

    var attachment = new MessagingExtensionAttachment
    {
        ContentType = ThumbnailCard.ContentType,
        Content = card,
    };

    return Task.FromResult(new MessagingExtensionResponse
    {
        ComposeExtension = new MessagingExtensionResult
        {
            Type = "result",
            AttachmentLayout = "list",
            Attachments = new List<MessagingExtensionAttachment> { attachment }
        }
    });
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
async handleTeamsMessagingExtensionSelectItem(context, obj) {
        return {
            composeExtension: {
                  type: 'result',
                  attachmentLayout: 'list',
                  attachments: [CardFactory.thumbnailCard(obj.Item3)]
            }
        };
    } 
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "name": "composeExtension/selectItem",
    "type": "invoke",
    "value": {
        "Item1": "Package_Name",
        "Item2": "Version",
        "Item3": "Package Description"
    },
    .
    .
    .
}
```

* * *

> [!NOTE]
> `OnTeamsMessagingExtensionSelectItemAsync` no se desencadena en la aplicación de equipos móviles.

## <a name="default-query"></a>Consulta predeterminada

Si establece `initialRun` `true` en en el manifiesto, Microsoft Teams emite una consulta **predeterminada** cuando el usuario abre por primera vez la extensión de mensaje. El servicio puede responder a esta consulta con un conjunto de resultados rellenados previamente. Esto resulta útil cuando el comando de búsqueda requiere autenticación o configuración, y muestra elementos, favoritos o cualquier otra información que no dependa de la entrada del usuario.

La consulta predeterminada tiene la misma estructura que cualquier consulta de usuario normal, con el `name` campo establecido `initialRun` en y `value` establecido `true` en como se muestra en el objeto siguiente:

```json
{
  "type": "invoke",
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "initialRun",
        "value": "true"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  ⋮
}
```

## <a name="code-sample"></a>Ejemplo de código

| Ejemplo de nombre           | Descripción | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Acción de extensión de mensaje de Teams| Describe cómo definir comandos de acción, crear un módulo de tareas y responder a la acción de envío del módulo de tareas. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) |
|Búsqueda de extensión de mensaje de Teams   |  Describe cómo definir comandos de búsqueda y responder a búsquedas.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Adición de autenticación a una extensión de mensaje](~/messaging-extensions/how-to/add-authentication.md)

## <a name="see-also"></a>Vea también

* [Extensiones de mensajes](../../what-are-messaging-extensions.md)
* [Cree su primera aplicación de pestaña con JavaScript](../../../sbs-gs-javascript.yml)
* [composeExtensions](../../../resources/schema/manifest-schema.md#composeextensions)

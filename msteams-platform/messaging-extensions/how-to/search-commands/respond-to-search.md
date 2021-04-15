---
title: Responder al comando de búsqueda
author: clearab
description: Cómo responder al comando de búsqueda desde una extensión de mensajería en una aplicación de Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 2cc53796deddb47e8dbce86a5b02f4d80a1b91e0
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696195"
---
# <a name="respond-to-search-command"></a>Responder al comando de búsqueda

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Después de que el usuario envíe el comando de búsqueda, el servicio web recibe un mensaje de invocación `composeExtension/query` que contiene un objeto con los parámetros de `value` búsqueda. Esta invocación se desencadena con las siguientes condiciones:

* A medida que se introducen caracteres en el cuadro de búsqueda.
* `initialRun` se establece en true en el manifiesto de la aplicación, recibirá el mensaje de invocación en cuanto se invoque el comando de búsqueda. Para obtener más información, vea [consulta predeterminada](#default-query).

Este documento le guía sobre cómo responder a solicitudes de usuario en forma de tarjetas y vistas previas, y las condiciones en las que Microsoft Teams emite una consulta predeterminada.

Los parámetros de solicitud se encuentran en el `value` objeto de la solicitud, que incluye las siguientes propiedades:

| Nombre de propiedad | Objetivo |
|---|---|
| `commandId` | Nombre del comando invocado por el usuario, que coincide con uno de los comandos declarados en el manifiesto de la aplicación. |
| `parameters` | Matriz de parámetros. Cada objeto de parámetro contiene el nombre del parámetro, junto con el valor del parámetro proporcionado por el usuario. |
| `queryOptions` | Parámetros de paginación: <br>`skip`: Recuento de omitir para esta consulta <br>`count`: número de elementos que se devolverán. |

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

El JSON siguiente se abrevia para resaltar las secciones más relevantes.

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

## <a name="respond-to-user-requests"></a>Responder a solicitudes de usuario

Cuando el usuario realiza una consulta, Microsoft Teams emite una solicitud HTTP sincrónica al servicio. En ese momento, el código tiene `5` segundos para proporcionar una respuesta HTTP a la solicitud. Durante este tiempo, el servicio puede realizar búsquedas adicionales o cualquier otra lógica empresarial necesaria para atender la solicitud.

El servicio debe responder con los resultados que coincidan con la consulta del usuario. La respuesta debe indicar un código de estado HTTP y una aplicación válida `200 OK` o un objeto JSON con las siguientes propiedades:

|Nombre de propiedad|Objetivo|
|---|---|
|`composeExtension`|Sobre de respuesta de nivel superior.|
|`composeExtension.type`|Tipo de respuesta. Se admiten los siguientes tipos: <br>`result`: muestra una lista de resultados de búsqueda <br>`auth`: pide al usuario que se autentique <br>`config`: pide al usuario que configure la extensión de mensajería <br>`message`: muestra un mensaje de texto sin formato |
|`composeExtension.attachmentLayout`|Especifica el diseño de los datos adjuntos. Se usa para respuestas de tipo `result` . <br>Actualmente, se admiten los siguientes tipos: <br>`list`: una lista de objetos de tarjeta que contienen miniaturas, título y campos de texto <br>`grid`: una cuadrícula de imágenes en miniatura |
|`composeExtension.attachments`|Matriz de objetos de datos adjuntos válidos. Se usa para respuestas de tipo `result` . <br>Actualmente, se admiten los siguientes tipos: <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|Acciones sugeridas. Se usa para respuestas de tipo `auth` o `config` . |
|`composeExtension.text`|Mensaje que se mostrará. Se usa para respuestas de tipo `message` . |

### <a name="response-card-types-and-previews"></a>Tipos y vistas previas de tarjetas de respuesta

Teams admite los siguientes tipos de tarjeta:

* [Tarjeta miniatura](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Tarjeta de héroe](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Tarjeta de conector de Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Tarjeta adaptable](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Para tener una mejor comprensión e información general sobre las tarjetas, vea [qué son las tarjetas](~/task-modules-and-cards/what-are-cards.md).

Para obtener información sobre cómo usar los tipos de miniatura y de tarjeta de héroe, consulta [Agregar tarjetas y acciones de tarjeta](~/task-modules-and-cards/cards/cards-actions.md).

Para obtener información adicional acerca de la tarjeta del conector de Office 365, vea [Using Office 365 Connector cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).

La lista de resultados se muestra en la interfaz de usuario de Microsoft Teams con una vista previa de cada elemento. La vista previa se genera de una de las dos maneras:

* Uso de `preview` la propiedad dentro del `attachment` objeto. Los `preview` datos adjuntos solo pueden ser una tarjeta Hero o Thumbnail.
* Extraído de las propiedades `title` `text` básicas , y `image` de los datos adjuntos. Solo se usan si la `preview` propiedad no está establecida y estas propiedades están disponibles.

Puede mostrar una vista previa de una tarjeta adaptable o una tarjeta de Conector de Office 365 en la lista de resultados mediante su propiedad de vista previa. La propiedad preview no es necesaria si los resultados ya son tarjetas Hero o Thumbnail. Si usas los datos adjuntos de vista previa, debe ser una tarjeta hero o thumbnail. Si no se especifica ninguna propiedad de vista previa, se produce un error en la vista previa de la tarjeta y no se muestra nada.

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

## <a name="default-query"></a>Consulta predeterminada

Si se establece en en el manifiesto, Microsoft Teams emite una consulta predeterminada cuando el usuario abre por primera vez `initialRun` `true` la extensión de mensajería.  El servicio puede responder a esta consulta con un conjunto de resultados rellenados previamente. Esto resulta útil cuando el comando de búsqueda requiere autenticación o configuración, mostrando elementos vistos recientemente, favoritos o cualquier otra información que no dependa de la entrada del usuario.

La consulta predeterminada tiene la misma estructura que cualquier consulta de usuario normal, con el campo establecido en y establecido en como se muestra `name` `initialRun` en el siguiente `value` `true` objeto:

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

| Nombre de ejemplo           | Descripción | .NET    | Node.js   |   
|:---------------------|:--------------|:---------|:--------|
|Acción de extensión de mensajería de Teams| Describe cómo definir comandos de acción, crear módulo de tareas y responder a la acción de envío del módulo de tareas. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|Búsqueda de extensión de mensajería de Teams   |  Describe cómo definir comandos de búsqueda y responder a las búsquedas.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="see-also"></a>Consulte también

> [!div class="nextstepaction"]
> [Agregar configuración a una extensión de mensajería](~/messaging-extensions/how-to/add-configuration-page.md)
 
## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Agregar autenticación a una extensión de mensajería](~/messaging-extensions/how-to/add-authentication.md)




---
title: Comando responder a búsqueda
author: clearab
description: Cómo responder al comando de búsqueda desde una extensión de mensajería en una aplicación de Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: e8b40dd8f422ffbd2537e8fa76a38c15eb6208de
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676207"
---
# <a name="respond-to-the-search-command"></a>Responder al comando de búsqueda

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Su servicio web recibirá un `composeExtension/query` mensaje de invocación que `value` contiene un objeto con los parámetros de búsqueda. Se desencadena esta Invocación:

* A medida que se escriben caracteres en el cuadro de búsqueda.
* Si `initialRun` se establece en true en el manifiesto de la aplicación, recibirá el mensaje de invocación en cuanto se invoque el comando de búsqueda. Vea [consulta predeterminada](#default-query).

Los propios parámetros de la solicitud se encuentran `value` en el objeto de la solicitud, que incluye las siguientes propiedades:

| Nombre de la propiedad | Objetivo |
|---|---|
| `commandId` | Nombre del comando invocado por el usuario, que coincide con uno de los comandos declarados en el manifiesto de la aplicación. |
| `parameters` | Matriz de parámetros. Cada objeto Parameter contiene el nombre del parámetro, junto con el valor del parámetro proporcionado por el usuario. |
| `queryOptions` | Parámetros de paginación: <br>`skip`: recuento de omitidos para esta consulta <br>`count`: número de elementos que se devolverá |

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
{
  //code to handle the query
}
```

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node. js](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearch extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
  //code to handle the query
    }
}
```

# <a name="jsontabjson"></a>[JSON](#tab/json)

El JSON siguiente se acorta para resaltar las secciones más relevantes.

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

Cuando el usuario realiza una consulta, Microsoft Teams emite una solicitud HTTP sincrónica a su servicio. En ese momento, el código tiene 5 segundos para proporcionar una respuesta HTTP a la solicitud. Durante este tiempo, el servicio puede realizar búsquedas adicionales o cualquier otra lógica empresarial necesaria para atender la solicitud.

El servicio debe responder con los resultados que coincidan con la consulta de usuario. La respuesta debe indicar un código de Estado HTTP `200 OK` de y un objeto Application/JSON válido con el siguiente cuerpo:

|Nombre de la propiedad|Objetivo|
|---|---|
|`composeExtension`|Sobre de respuesta de nivel superior.|
|`composeExtension.type`|Tipo de respuesta. Se admiten los siguientes tipos: <br>`result`: muestra una lista de los resultados de la búsqueda <br>`auth`: pide al usuario que se autentique <br>`config`: pide al usuario que configure la extensión de mensajería. <br>`message`: muestra un mensaje de texto sin formato |
|`composeExtension.attachmentLayout`|Especifica el diseño de los datos adjuntos. Se usa para las respuestas `result`de tipo. <br>Actualmente se admiten los siguientes tipos: <br>`list`: una lista de objetos Card que contiene miniaturas, títulos y campos de texto <br>`grid`: una cuadrícula de imágenes en miniatura |
|`composeExtension.attachments`|Matriz de objetos Attachment válidos. Se usa para las respuestas `result`de tipo. <br>Actualmente se admiten los siguientes tipos: <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|Acciones sugeridas. Se usa para las respuestas `auth` de `config`tipo o. |
|`composeExtension.text`|Mensaje que se va a mostrar. Se usa para las respuestas `message`de tipo. |

### <a name="response-card-types-and-previews"></a>Tipos y vistas previas de las tarjetas de respuesta

Se admiten los siguientes tipos de datos adjuntos:

* [Tarjeta en miniatura](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Tarjeta Hero](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Tarjeta de conector de Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Tarjeta adaptable](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Consulte [¿Qué son las tarjetas](~/task-modules-and-cards/what-are-cards.md) para obtener información general).

Para obtener información sobre cómo usar los tipos de tarjetas en miniatura y Heroes, consulte [Add Cards and Card Actions](~/task-modules-and-cards/cards/cards-actions.md).

Para obtener documentación adicional sobre la tarjeta de conector de Office 365, consulte [using office 365 Connector Cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).

La lista de resultados se muestra en la interfaz de usuario de Microsoft Teams con una vista previa de cada elemento. La vista previa se genera de una de estas dos maneras:

* Uso de `preview` la propiedad en `attachment` el objeto. El `preview` archivo adjunto solo puede ser un héroe o una tarjeta de miniaturas.
* Se extraen de `title`las `text`propiedades Basic `image` , y de los datos adjuntos. Solo se usan si la `preview` propiedad no está establecida y estas propiedades están disponibles.

Puede mostrar una vista previa de una tarjeta adaptable o una tarjeta de conexión de Office 365 en la lista de resultados simplemente por su propiedad Preview. Esto no es necesario si los resultados ya son un héroe o tarjetas en miniatura. Si usa la vista previa de datos adjuntos, debe ser un héroe o una tarjeta en miniatura. Si no se especifica ninguna propiedad de vista previa, se producirá un error en la vista previa de la tarjeta y no se mostrará nada.

### <a name="response-example"></a>Ejemplo de respuesta

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node. js](#tab/typescript)

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

# <a name="jsontabjson"></a>[JSON](#tab/json)

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

Si establece `initialRun` en `true` en el manifiesto, Microsoft Teams emite una consulta "predeterminada" cuando el usuario abre por primera vez la extensión de mensajería. El servicio puede responder a esta consulta con un conjunto de resultados rellenados previamente. Esto puede ser útil si el comando de búsqueda requiere autenticación o configuración, Mostrar elementos vistos recientemente, favoritos o cualquier otra información que no dependa de los datos proporcionados por el usuario.

La consulta predeterminada tiene la misma estructura que cualquier consulta de usuario normal, con `name` el campo establecido `initialRun` en `value` y establecido `true` en como en el siguiente objeto.

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

## <a name="next-steps"></a>Pasos siguientes

Agregar autenticación o configuración

* [Adición de autenticación a una extensión de mensajería](~/messaging-extensions/how-to/add-authentication.md)
* [Agregar configuración a una extensión de mensajería](~/messaging-extensions/how-to/add-configuration-page.md)

Implementar configuración

* [Implementar el paquete de la aplicación](~/concepts/deploy-and-publish/apps-upload.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]

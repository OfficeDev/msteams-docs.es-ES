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
# <a name="respond-to-the-search-command"></a><span data-ttu-id="c1409-103">Responder al comando de búsqueda</span><span class="sxs-lookup"><span data-stu-id="c1409-103">Respond to the search command</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="c1409-104">Su servicio web recibirá un `composeExtension/query` mensaje de invocación que `value` contiene un objeto con los parámetros de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="c1409-104">Your web service will receive a `composeExtension/query` invoke message that contains a `value` object with the search parameters.</span></span> <span data-ttu-id="c1409-105">Se desencadena esta Invocación:</span><span class="sxs-lookup"><span data-stu-id="c1409-105">This invoke is triggered:</span></span>

* <span data-ttu-id="c1409-106">A medida que se escriben caracteres en el cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="c1409-106">As characters are entered into the search box.</span></span>
* <span data-ttu-id="c1409-107">Si `initialRun` se establece en true en el manifiesto de la aplicación, recibirá el mensaje de invocación en cuanto se invoque el comando de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="c1409-107">If `initialRun` is set to true in your app manifest, you'll receive the invoke message as soon as the search command is invoked.</span></span> <span data-ttu-id="c1409-108">Vea [consulta predeterminada](#default-query).</span><span class="sxs-lookup"><span data-stu-id="c1409-108">See [default query](#default-query).</span></span>

<span data-ttu-id="c1409-109">Los propios parámetros de la solicitud se encuentran `value` en el objeto de la solicitud, que incluye las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="c1409-109">The request parameters itself are found in the `value` object in the request, which includes the following properties:</span></span>

| <span data-ttu-id="c1409-110">Nombre de la propiedad</span><span class="sxs-lookup"><span data-stu-id="c1409-110">Property name</span></span> | <span data-ttu-id="c1409-111">Objetivo</span><span class="sxs-lookup"><span data-stu-id="c1409-111">Purpose</span></span> |
|---|---|
| `commandId` | <span data-ttu-id="c1409-112">Nombre del comando invocado por el usuario, que coincide con uno de los comandos declarados en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c1409-112">The name of the command invoked by the user, matching one of the commands declared in the app manifest.</span></span> |
| `parameters` | <span data-ttu-id="c1409-113">Matriz de parámetros.</span><span class="sxs-lookup"><span data-stu-id="c1409-113">Array of parameters.</span></span> <span data-ttu-id="c1409-114">Cada objeto Parameter contiene el nombre del parámetro, junto con el valor del parámetro proporcionado por el usuario.</span><span class="sxs-lookup"><span data-stu-id="c1409-114">Each parameter object contains the parameter name, along with the parameter value provided by the user.</span></span> |
| `queryOptions` | <span data-ttu-id="c1409-115">Parámetros de paginación:</span><span class="sxs-lookup"><span data-stu-id="c1409-115">Pagination parameters:</span></span> <br><span data-ttu-id="c1409-116">`skip`: recuento de omitidos para esta consulta</span><span class="sxs-lookup"><span data-stu-id="c1409-116">`skip`: skip count for this query</span></span> <br><span data-ttu-id="c1409-117">`count`: número de elementos que se devolverá</span><span class="sxs-lookup"><span data-stu-id="c1409-117">`count`: number of elements to return</span></span> |

# <a name="cnettabdotnet"></a>[<span data-ttu-id="c1409-118">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="c1409-118">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
{
  //code to handle the query
}
```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="c1409-119">TypeScript/node. js</span><span class="sxs-lookup"><span data-stu-id="c1409-119">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearch extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
  //code to handle the query
    }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="c1409-120">JSON</span><span class="sxs-lookup"><span data-stu-id="c1409-120">JSON</span></span>](#tab/json)

<span data-ttu-id="c1409-121">El JSON siguiente se acorta para resaltar las secciones más relevantes.</span><span class="sxs-lookup"><span data-stu-id="c1409-121">The JSON below is shortened to highlight the most relevant sections.</span></span>

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

## <a name="respond-to-user-requests"></a><span data-ttu-id="c1409-122">Responder a solicitudes de usuario</span><span class="sxs-lookup"><span data-stu-id="c1409-122">Respond to user requests</span></span>

<span data-ttu-id="c1409-123">Cuando el usuario realiza una consulta, Microsoft Teams emite una solicitud HTTP sincrónica a su servicio.</span><span class="sxs-lookup"><span data-stu-id="c1409-123">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service.</span></span> <span data-ttu-id="c1409-124">En ese momento, el código tiene 5 segundos para proporcionar una respuesta HTTP a la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c1409-124">At that point, your code has 5 seconds to provide an HTTP response to the request.</span></span> <span data-ttu-id="c1409-125">Durante este tiempo, el servicio puede realizar búsquedas adicionales o cualquier otra lógica empresarial necesaria para atender la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c1409-125">During this time, your service can perform additional lookup, or any other business logic needed to serve the request.</span></span>

<span data-ttu-id="c1409-126">El servicio debe responder con los resultados que coincidan con la consulta de usuario.</span><span class="sxs-lookup"><span data-stu-id="c1409-126">Your service should respond with the results matching the user query.</span></span> <span data-ttu-id="c1409-127">La respuesta debe indicar un código de Estado HTTP `200 OK` de y un objeto Application/JSON válido con el siguiente cuerpo:</span><span class="sxs-lookup"><span data-stu-id="c1409-127">The response must indicate an HTTP status code of `200 OK` and a valid application/json object with the following body:</span></span>

|<span data-ttu-id="c1409-128">Nombre de la propiedad</span><span class="sxs-lookup"><span data-stu-id="c1409-128">Property name</span></span>|<span data-ttu-id="c1409-129">Objetivo</span><span class="sxs-lookup"><span data-stu-id="c1409-129">Purpose</span></span>|
|---|---|
|`composeExtension`|<span data-ttu-id="c1409-130">Sobre de respuesta de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="c1409-130">Top-level response envelope.</span></span>|
|`composeExtension.type`|<span data-ttu-id="c1409-131">Tipo de respuesta.</span><span class="sxs-lookup"><span data-stu-id="c1409-131">Type of response.</span></span> <span data-ttu-id="c1409-132">Se admiten los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="c1409-132">The following types are supported:</span></span> <br><span data-ttu-id="c1409-133">`result`: muestra una lista de los resultados de la búsqueda</span><span class="sxs-lookup"><span data-stu-id="c1409-133">`result`: displays a list of search results</span></span> <br><span data-ttu-id="c1409-134">`auth`: pide al usuario que se autentique</span><span class="sxs-lookup"><span data-stu-id="c1409-134">`auth`: asks the user to authenticate</span></span> <br><span data-ttu-id="c1409-135">`config`: pide al usuario que configure la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="c1409-135">`config`: asks the user to set up the messaging extension</span></span> <br><span data-ttu-id="c1409-136">`message`: muestra un mensaje de texto sin formato</span><span class="sxs-lookup"><span data-stu-id="c1409-136">`message`: displays a plain text message</span></span> |
|`composeExtension.attachmentLayout`|<span data-ttu-id="c1409-137">Especifica el diseño de los datos adjuntos.</span><span class="sxs-lookup"><span data-stu-id="c1409-137">Specifies the layout of the attachments.</span></span> <span data-ttu-id="c1409-138">Se usa para las respuestas `result`de tipo.</span><span class="sxs-lookup"><span data-stu-id="c1409-138">Used for responses of type `result`.</span></span> <br><span data-ttu-id="c1409-139">Actualmente se admiten los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="c1409-139">Currently the following types are supported:</span></span> <br><span data-ttu-id="c1409-140">`list`: una lista de objetos Card que contiene miniaturas, títulos y campos de texto</span><span class="sxs-lookup"><span data-stu-id="c1409-140">`list`: a list of card objects containing thumbnail, title, and text fields</span></span> <br><span data-ttu-id="c1409-141">`grid`: una cuadrícula de imágenes en miniatura</span><span class="sxs-lookup"><span data-stu-id="c1409-141">`grid`: a grid of thumbnail images</span></span> |
|`composeExtension.attachments`|<span data-ttu-id="c1409-142">Matriz de objetos Attachment válidos.</span><span class="sxs-lookup"><span data-stu-id="c1409-142">Array of valid attachment objects.</span></span> <span data-ttu-id="c1409-143">Se usa para las respuestas `result`de tipo.</span><span class="sxs-lookup"><span data-stu-id="c1409-143">Used for responses of type `result`.</span></span> <br><span data-ttu-id="c1409-144">Actualmente se admiten los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="c1409-144">Currently the following types are supported:</span></span> <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|<span data-ttu-id="c1409-145">Acciones sugeridas.</span><span class="sxs-lookup"><span data-stu-id="c1409-145">Suggested actions.</span></span> <span data-ttu-id="c1409-146">Se usa para las respuestas `auth` de `config`tipo o.</span><span class="sxs-lookup"><span data-stu-id="c1409-146">Used for responses of type `auth` or `config`.</span></span> |
|`composeExtension.text`|<span data-ttu-id="c1409-147">Mensaje que se va a mostrar.</span><span class="sxs-lookup"><span data-stu-id="c1409-147">Message to display.</span></span> <span data-ttu-id="c1409-148">Se usa para las respuestas `message`de tipo.</span><span class="sxs-lookup"><span data-stu-id="c1409-148">Used for responses of type `message`.</span></span> |

### <a name="response-card-types-and-previews"></a><span data-ttu-id="c1409-149">Tipos y vistas previas de las tarjetas de respuesta</span><span class="sxs-lookup"><span data-stu-id="c1409-149">Response card types and previews</span></span>

<span data-ttu-id="c1409-150">Se admiten los siguientes tipos de datos adjuntos:</span><span class="sxs-lookup"><span data-stu-id="c1409-150">We support the following attachment types:</span></span>

* [<span data-ttu-id="c1409-151">Tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="c1409-151">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="c1409-152">Tarjeta Hero</span><span class="sxs-lookup"><span data-stu-id="c1409-152">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="c1409-153">Tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="c1409-153">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="c1409-154">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="c1409-154">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="c1409-155">Consulte [¿Qué son las tarjetas](~/task-modules-and-cards/what-are-cards.md) para obtener información general).</span><span class="sxs-lookup"><span data-stu-id="c1409-155">See [What are cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

<span data-ttu-id="c1409-156">Para obtener información sobre cómo usar los tipos de tarjetas en miniatura y Heroes, consulte [Add Cards and Card Actions](~/task-modules-and-cards/cards/cards-actions.md).</span><span class="sxs-lookup"><span data-stu-id="c1409-156">To learn how to use the thumbnail and hero card types, see [Add cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="c1409-157">Para obtener documentación adicional sobre la tarjeta de conector de Office 365, consulte [using office 365 Connector Cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span><span class="sxs-lookup"><span data-stu-id="c1409-157">For additional documentation regarding the Office 365 Connector card, see [Using Office 365 Connector cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="c1409-158">La lista de resultados se muestra en la interfaz de usuario de Microsoft Teams con una vista previa de cada elemento.</span><span class="sxs-lookup"><span data-stu-id="c1409-158">The result list is displayed in the Microsoft Teams UI with a preview of each item.</span></span> <span data-ttu-id="c1409-159">La vista previa se genera de una de estas dos maneras:</span><span class="sxs-lookup"><span data-stu-id="c1409-159">The preview is generated in one of two ways:</span></span>

* <span data-ttu-id="c1409-160">Uso de `preview` la propiedad en `attachment` el objeto.</span><span class="sxs-lookup"><span data-stu-id="c1409-160">Using the `preview` property within the `attachment` object.</span></span> <span data-ttu-id="c1409-161">El `preview` archivo adjunto solo puede ser un héroe o una tarjeta de miniaturas.</span><span class="sxs-lookup"><span data-stu-id="c1409-161">The `preview` attachment can only be a Hero or Thumbnail card.</span></span>
* <span data-ttu-id="c1409-162">Se extraen de `title`las `text`propiedades Basic `image` , y de los datos adjuntos.</span><span class="sxs-lookup"><span data-stu-id="c1409-162">Extracted from the basic `title`, `text`, and `image` properties of the attachment.</span></span> <span data-ttu-id="c1409-163">Solo se usan si la `preview` propiedad no está establecida y estas propiedades están disponibles.</span><span class="sxs-lookup"><span data-stu-id="c1409-163">These are used only if the `preview` property is not set and these properties are available.</span></span>

<span data-ttu-id="c1409-164">Puede mostrar una vista previa de una tarjeta adaptable o una tarjeta de conexión de Office 365 en la lista de resultados simplemente por su propiedad Preview.</span><span class="sxs-lookup"><span data-stu-id="c1409-164">You can display a preview of an Adaptive Card or Office 365 Connector card in the result list simply by its preview property.</span></span> <span data-ttu-id="c1409-165">Esto no es necesario si los resultados ya son un héroe o tarjetas en miniatura.</span><span class="sxs-lookup"><span data-stu-id="c1409-165">This is not necessary if the results are already hero or thumbnail cards.</span></span> <span data-ttu-id="c1409-166">Si usa la vista previa de datos adjuntos, debe ser un héroe o una tarjeta en miniatura.</span><span class="sxs-lookup"><span data-stu-id="c1409-166">If you use the preview attachment, it must be either a Hero or Thumbnail card.</span></span> <span data-ttu-id="c1409-167">Si no se especifica ninguna propiedad de vista previa, se producirá un error en la vista previa de la tarjeta y no se mostrará nada.</span><span class="sxs-lookup"><span data-stu-id="c1409-167">If no preview property is specified, the preview of the card will fail and nothing will be displayed.</span></span>

### <a name="response-example"></a><span data-ttu-id="c1409-168">Ejemplo de respuesta</span><span class="sxs-lookup"><span data-stu-id="c1409-168">Response example</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="c1409-169">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="c1409-169">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="c1409-170">TypeScript/node. js</span><span class="sxs-lookup"><span data-stu-id="c1409-170">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="c1409-171">JSON</span><span class="sxs-lookup"><span data-stu-id="c1409-171">JSON</span></span>](#tab/json)

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

## <a name="default-query"></a><span data-ttu-id="c1409-172">Consulta predeterminada</span><span class="sxs-lookup"><span data-stu-id="c1409-172">Default query</span></span>

<span data-ttu-id="c1409-173">Si establece `initialRun` en `true` en el manifiesto, Microsoft Teams emite una consulta "predeterminada" cuando el usuario abre por primera vez la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="c1409-173">If you set `initialRun` to `true` in the manifest, Microsoft Teams issues a "default" query when the user first opens the messaging extension.</span></span> <span data-ttu-id="c1409-174">El servicio puede responder a esta consulta con un conjunto de resultados rellenados previamente.</span><span class="sxs-lookup"><span data-stu-id="c1409-174">Your service can respond to this query with a set of pre-populated results.</span></span> <span data-ttu-id="c1409-175">Esto puede ser útil si el comando de búsqueda requiere autenticación o configuración, Mostrar elementos vistos recientemente, favoritos o cualquier otra información que no dependa de los datos proporcionados por el usuario.</span><span class="sxs-lookup"><span data-stu-id="c1409-175">This can be useful when your search command requires authentication or configuration, displaying recently viewed items, favorites, or any other information that is not dependent on user input.</span></span>

<span data-ttu-id="c1409-176">La consulta predeterminada tiene la misma estructura que cualquier consulta de usuario normal, con `name` el campo establecido `initialRun` en `value` y establecido `true` en como en el siguiente objeto.</span><span class="sxs-lookup"><span data-stu-id="c1409-176">The default query has the same structure as any regular user query, with the `name` field set to `initialRun` and `value` set to `true` as in the object below.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c1409-177">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c1409-177">Next Steps</span></span>

<span data-ttu-id="c1409-178">Agregar autenticación o configuración</span><span class="sxs-lookup"><span data-stu-id="c1409-178">Add authentication and/or configuration</span></span>

* [<span data-ttu-id="c1409-179">Adición de autenticación a una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="c1409-179">Add authentication to a messaging extension</span></span>](~/messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="c1409-180">Agregar configuración a una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="c1409-180">Add configuration to a messaging extension</span></span>](~/messaging-extensions/how-to/add-configuration-page.md)

<span data-ttu-id="c1409-181">Implementar configuración</span><span class="sxs-lookup"><span data-stu-id="c1409-181">Deploy configuration</span></span>

* [<span data-ttu-id="c1409-182">Implementar el paquete de la aplicación</span><span class="sxs-lookup"><span data-stu-id="c1409-182">Deploy your app package</span></span>](~/concepts/deploy-and-publish/apps-upload.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]

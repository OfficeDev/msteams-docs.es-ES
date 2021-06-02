---
title: Responder al comando de búsqueda
author: clearab
description: Cómo responder al comando de búsqueda desde una extensión de mensajería en una Microsoft Teams aplicación.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 15b48b135f656feeb3cfb28ffbe12852ddb66359
ms.sourcegitcommit: e50cdeb6b7f481e12911b2bb74a8da22af0bffac
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/01/2021
ms.locfileid: "52710637"
---
# <a name="respond-to-search-command"></a><span data-ttu-id="cbc1f-103">Responder al comando de búsqueda</span><span class="sxs-lookup"><span data-stu-id="cbc1f-103">Respond to search command</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="cbc1f-104">Después de que el usuario envíe el comando de búsqueda, el servicio web recibe un mensaje de invocación `composeExtension/query` que contiene un objeto con los parámetros de `value` búsqueda.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-104">After the user submits the search command, your web service receives a `composeExtension/query` invoke message that contains a `value` object with the search parameters.</span></span> <span data-ttu-id="cbc1f-105">Esta invocación se desencadena con las siguientes condiciones:</span><span class="sxs-lookup"><span data-stu-id="cbc1f-105">This invoke is triggered with the following conditions:</span></span>

* <span data-ttu-id="cbc1f-106">A medida que se introducen caracteres en el cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-106">As characters are entered into the search box.</span></span>
* <span data-ttu-id="cbc1f-107">`initialRun` se establece en true en el manifiesto de la aplicación, recibirá el mensaje de invocación en cuanto se invoque el comando de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-107">`initialRun` is set to true in your app manifest, you receive the invoke message as soon as the search command is invoked.</span></span> <span data-ttu-id="cbc1f-108">Para obtener más información, vea [consulta predeterminada](#default-query).</span><span class="sxs-lookup"><span data-stu-id="cbc1f-108">For more information, see [default query](#default-query).</span></span>

<span data-ttu-id="cbc1f-109">Este documento le guía sobre cómo responder a solicitudes de usuario en forma de tarjetas y vistas previas, y las condiciones en las que Microsoft Teams emite una consulta predeterminada.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-109">This document guides you on how to respond to user requests in the form of cards and previews, and the conditions under which Microsoft Teams issues a default query.</span></span>

<span data-ttu-id="cbc1f-110">Los parámetros de solicitud se encuentran en el `value` objeto de la solicitud, que incluye las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="cbc1f-110">The request parameters are found in the `value` object in the request, which includes the following properties:</span></span>

| <span data-ttu-id="cbc1f-111">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="cbc1f-111">Property name</span></span> | <span data-ttu-id="cbc1f-112">Objetivo</span><span class="sxs-lookup"><span data-stu-id="cbc1f-112">Purpose</span></span> |
|---|---|
| `commandId` | <span data-ttu-id="cbc1f-113">Nombre del comando invocado por el usuario, que coincide con uno de los comandos declarados en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-113">The name of the command invoked by the user, matching one of the commands declared in the app manifest.</span></span> |
| `parameters` | <span data-ttu-id="cbc1f-114">Matriz de parámetros.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-114">Array of parameters.</span></span> <span data-ttu-id="cbc1f-115">Cada objeto de parámetro contiene el nombre del parámetro, junto con el valor del parámetro proporcionado por el usuario.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-115">Each parameter object contains the parameter name, along with the parameter value provided by the user.</span></span> |
| `queryOptions` | <span data-ttu-id="cbc1f-116">Parámetros de paginación:</span><span class="sxs-lookup"><span data-stu-id="cbc1f-116">Pagination parameters:</span></span> <br><span data-ttu-id="cbc1f-117">`skip`: Recuento de omitir para esta consulta</span><span class="sxs-lookup"><span data-stu-id="cbc1f-117">`skip`: Skip count for this query</span></span> <br><span data-ttu-id="cbc1f-118">`count`: número de elementos que se devolverán.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-118">`count`: Number of elements to return.</span></span> |

# <a name="cnet"></a>[<span data-ttu-id="cbc1f-119">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="cbc1f-119">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
{
  //code to handle the query
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="cbc1f-120">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="cbc1f-120">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearch extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
  //code to handle the query
    }
}
```

# <a name="json"></a>[<span data-ttu-id="cbc1f-121">JSON</span><span class="sxs-lookup"><span data-stu-id="cbc1f-121">JSON</span></span>](#tab/json)

<span data-ttu-id="cbc1f-122">El JSON siguiente se abrevia para resaltar las secciones más relevantes.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-122">The JSON below is shortened to highlight the most relevant sections.</span></span>

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

## <a name="respond-to-user-requests"></a><span data-ttu-id="cbc1f-123">Responder a solicitudes de usuario</span><span class="sxs-lookup"><span data-stu-id="cbc1f-123">Respond to user requests</span></span>

<span data-ttu-id="cbc1f-124">Cuando el usuario realiza una consulta, Microsoft Teams emite una solicitud HTTP sincrónica al servicio.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-124">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service.</span></span> <span data-ttu-id="cbc1f-125">En ese momento, el código tiene `5` segundos para proporcionar una respuesta HTTP a la solicitud.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-125">At that point, your code has `5` seconds to provide an HTTP response to the request.</span></span> <span data-ttu-id="cbc1f-126">Durante este tiempo, el servicio puede realizar búsquedas adicionales o cualquier otra lógica empresarial necesaria para atender la solicitud.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-126">During this time, your service can perform additional lookup, or any other business logic needed to serve the request.</span></span>

<span data-ttu-id="cbc1f-127">El servicio debe responder con los resultados que coincidan con la consulta del usuario.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-127">Your service must respond with the results matching the user query.</span></span> <span data-ttu-id="cbc1f-128">La respuesta debe indicar un código de estado HTTP y una aplicación válida `200 OK` o un objeto JSON con las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="cbc1f-128">The response must indicate an HTTP status code of `200 OK` and a valid application or JSON object with the following properties:</span></span>

|<span data-ttu-id="cbc1f-129">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="cbc1f-129">Property name</span></span>|<span data-ttu-id="cbc1f-130">Objetivo</span><span class="sxs-lookup"><span data-stu-id="cbc1f-130">Purpose</span></span>|
|---|---|
|`composeExtension`|<span data-ttu-id="cbc1f-131">Sobre de respuesta de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-131">Top-level response envelope.</span></span>|
|`composeExtension.type`|<span data-ttu-id="cbc1f-132">Tipo de respuesta.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-132">Type of response.</span></span> <span data-ttu-id="cbc1f-133">Se admiten los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="cbc1f-133">The following types are supported:</span></span> <br><span data-ttu-id="cbc1f-134">`result`: muestra una lista de resultados de búsqueda</span><span class="sxs-lookup"><span data-stu-id="cbc1f-134">`result`: Displays a list of search results</span></span> <br><span data-ttu-id="cbc1f-135">`auth`: pide al usuario que se autentique</span><span class="sxs-lookup"><span data-stu-id="cbc1f-135">`auth`: Asks the user to authenticate</span></span> <br><span data-ttu-id="cbc1f-136">`config`: pide al usuario que configure la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="cbc1f-136">`config`: Asks the user to set up the messaging extension</span></span> <br><span data-ttu-id="cbc1f-137">`message`: muestra un mensaje de texto sin formato</span><span class="sxs-lookup"><span data-stu-id="cbc1f-137">`message`: Displays a plain text message</span></span> |
|`composeExtension.attachmentLayout`|<span data-ttu-id="cbc1f-138">Especifica el diseño de los datos adjuntos.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-138">Specifies the layout of the attachments.</span></span> <span data-ttu-id="cbc1f-139">Se usa para respuestas de tipo `result` .</span><span class="sxs-lookup"><span data-stu-id="cbc1f-139">Used for responses of type `result`.</span></span> <br><span data-ttu-id="cbc1f-140">Actualmente, se admiten los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="cbc1f-140">Currently, the following types are supported:</span></span> <br><span data-ttu-id="cbc1f-141">`list`: una lista de objetos de tarjeta que contienen miniaturas, título y campos de texto</span><span class="sxs-lookup"><span data-stu-id="cbc1f-141">`list`: A list of card objects containing thumbnail, title, and text fields</span></span> <br><span data-ttu-id="cbc1f-142">`grid`: una cuadrícula de imágenes en miniatura</span><span class="sxs-lookup"><span data-stu-id="cbc1f-142">`grid`: A grid of thumbnail images</span></span> |
|`composeExtension.attachments`|<span data-ttu-id="cbc1f-143">Matriz de objetos de datos adjuntos válidos.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-143">Array of valid attachment objects.</span></span> <span data-ttu-id="cbc1f-144">Se usa para respuestas de tipo `result` .</span><span class="sxs-lookup"><span data-stu-id="cbc1f-144">Used for responses of type `result`.</span></span> <br><span data-ttu-id="cbc1f-145">Actualmente, se admiten los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="cbc1f-145">Currently, the following types are supported:</span></span> <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|<span data-ttu-id="cbc1f-146">Acciones sugeridas.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-146">Suggested actions.</span></span> <span data-ttu-id="cbc1f-147">Se usa para respuestas de tipo `auth` o `config` .</span><span class="sxs-lookup"><span data-stu-id="cbc1f-147">Used for responses of type `auth` or `config`.</span></span> |
|`composeExtension.text`|<span data-ttu-id="cbc1f-148">Mensaje que se mostrará.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-148">Message to display.</span></span> <span data-ttu-id="cbc1f-149">Se usa para respuestas de tipo `message` .</span><span class="sxs-lookup"><span data-stu-id="cbc1f-149">Used for responses of type `message`.</span></span> |

### <a name="response-card-types-and-previews"></a><span data-ttu-id="cbc1f-150">Tipos y vistas previas de tarjetas de respuesta</span><span class="sxs-lookup"><span data-stu-id="cbc1f-150">Response card types and previews</span></span>

<span data-ttu-id="cbc1f-151">Teams admite los siguientes tipos de tarjeta:</span><span class="sxs-lookup"><span data-stu-id="cbc1f-151">Teams supports the following card types:</span></span>

* [<span data-ttu-id="cbc1f-152">Tarjeta miniatura</span><span class="sxs-lookup"><span data-stu-id="cbc1f-152">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="cbc1f-153">Tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="cbc1f-153">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="cbc1f-154">Office 365 Tarjeta de conector</span><span class="sxs-lookup"><span data-stu-id="cbc1f-154">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="cbc1f-155">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="cbc1f-155">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="cbc1f-156">Para tener una mejor comprensión e información general sobre las tarjetas, vea [qué son las tarjetas](~/task-modules-and-cards/what-are-cards.md).</span><span class="sxs-lookup"><span data-stu-id="cbc1f-156">To have a better understanding and overview on cards, see [what are cards](~/task-modules-and-cards/what-are-cards.md).</span></span>

<span data-ttu-id="cbc1f-157">Para obtener información sobre cómo usar los tipos de miniatura y de tarjeta de héroe, consulta [Agregar tarjetas y acciones de tarjeta](~/task-modules-and-cards/cards/cards-actions.md).</span><span class="sxs-lookup"><span data-stu-id="cbc1f-157">To learn how to use the thumbnail and hero card types, see [add cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="cbc1f-158">Para obtener información adicional acerca de la Office 365 Connector, vea [Using Office 365 Connector cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span><span class="sxs-lookup"><span data-stu-id="cbc1f-158">For additional information regarding the Office 365 Connector card, see [Using Office 365 Connector cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="cbc1f-159">La lista de resultados se muestra en la Microsoft Teams de usuario con una vista previa de cada elemento.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-159">The result list is displayed in the Microsoft Teams UI with a preview of each item.</span></span> <span data-ttu-id="cbc1f-160">La vista previa se genera de una de las dos maneras:</span><span class="sxs-lookup"><span data-stu-id="cbc1f-160">The preview is generated in one of the two ways:</span></span>

* <span data-ttu-id="cbc1f-161">Uso de `preview` la propiedad dentro del `attachment` objeto.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-161">Using the `preview` property within the `attachment` object.</span></span> <span data-ttu-id="cbc1f-162">Los `preview` datos adjuntos solo pueden ser una tarjeta Hero o Thumbnail.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-162">The `preview` attachment can only be a Hero or Thumbnail card.</span></span>
* <span data-ttu-id="cbc1f-163">Extraído de las propiedades `title` `text` básicas , y `image` de los datos adjuntos.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-163">Extracted from the basic `title`, `text`, and `image` properties of the attachment.</span></span> <span data-ttu-id="cbc1f-164">Solo se usan si la `preview` propiedad no está establecida y estas propiedades están disponibles.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-164">These are used only if the `preview` property is not set and these properties are available.</span></span>
* <span data-ttu-id="cbc1f-165">No se admiten en la tarjeta de vista previa el botón de la tarjeta De héroe o miniatura ni las acciones de pulsación, excepto invocar.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-165">The Hero or Thumbnail card button and tap actions, except invoke, are not supported in the preview card.</span></span>

<span data-ttu-id="cbc1f-166">Puede mostrar una vista previa de una tarjeta adaptable o una tarjeta Office 365 Connector en la lista de resultados mediante su propiedad de vista previa.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-166">You can display a preview of an Adaptive Card or Office 365 Connector card in the result list using its preview property.</span></span> <span data-ttu-id="cbc1f-167">La propiedad preview no es necesaria si los resultados ya son tarjetas Hero o Thumbnail.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-167">The preview property is not necessary if the results are already Hero or Thumbnail cards.</span></span> <span data-ttu-id="cbc1f-168">Si usas los datos adjuntos de vista previa, debe ser una tarjeta hero o thumbnail.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-168">If you use the preview attachment, it must be either a Hero or Thumbnail card.</span></span> <span data-ttu-id="cbc1f-169">Si no se especifica ninguna propiedad de vista previa, se produce un error en la vista previa de la tarjeta y no se muestra nada.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-169">If no preview property is specified, the preview of the card fails and nothing is displayed.</span></span>

### <a name="response-example"></a><span data-ttu-id="cbc1f-170">Ejemplo de respuesta</span><span class="sxs-lookup"><span data-stu-id="cbc1f-170">Response example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="cbc1f-171">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="cbc1f-171">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="cbc1f-172">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="cbc1f-172">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="cbc1f-173">JSON</span><span class="sxs-lookup"><span data-stu-id="cbc1f-173">JSON</span></span>](#tab/json)

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

## <a name="default-query"></a><span data-ttu-id="cbc1f-174">Consulta predeterminada</span><span class="sxs-lookup"><span data-stu-id="cbc1f-174">Default query</span></span>

<span data-ttu-id="cbc1f-175">Si se establece en en el manifiesto, Microsoft Teams una consulta predeterminada cuando el usuario abre por primera vez `initialRun` `true` la extensión de mensajería. </span><span class="sxs-lookup"><span data-stu-id="cbc1f-175">If you set `initialRun` to `true` in the manifest, Microsoft Teams issues a **default** query when the user first opens the messaging extension.</span></span> <span data-ttu-id="cbc1f-176">El servicio puede responder a esta consulta con un conjunto de resultados rellenados previamente.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-176">Your service can respond to this query with a set of pre-populated results.</span></span> <span data-ttu-id="cbc1f-177">Esto resulta útil cuando el comando de búsqueda requiere autenticación o configuración, mostrando elementos vistos recientemente, favoritos o cualquier otra información que no dependa de la entrada del usuario.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-177">This is useful when your search command requires authentication or configuration, displaying recently viewed items, favorites, or any other information that is not dependent on user input.</span></span>

<span data-ttu-id="cbc1f-178">La consulta predeterminada tiene la misma estructura que cualquier consulta de usuario normal, con el campo establecido en y establecido en como se muestra `name` `initialRun` en el siguiente `value` `true` objeto:</span><span class="sxs-lookup"><span data-stu-id="cbc1f-178">The default query has the same structure as any regular user query, with the `name` field set to `initialRun` and `value` set to `true` as shown in the following object:</span></span>

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

## <a name="code-sample"></a><span data-ttu-id="cbc1f-179">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="cbc1f-179">Code sample</span></span>

| <span data-ttu-id="cbc1f-180">Nombre de ejemplo</span><span class="sxs-lookup"><span data-stu-id="cbc1f-180">Sample Name</span></span>           | <span data-ttu-id="cbc1f-181">Descripción</span><span class="sxs-lookup"><span data-stu-id="cbc1f-181">Description</span></span> | <span data-ttu-id="cbc1f-182">.NET</span><span class="sxs-lookup"><span data-stu-id="cbc1f-182">.NET</span></span>    | <span data-ttu-id="cbc1f-183">Node.js</span><span class="sxs-lookup"><span data-stu-id="cbc1f-183">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="cbc1f-184">Teams extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="cbc1f-184">Teams messaging extension action</span></span>| <span data-ttu-id="cbc1f-185">Describe cómo definir comandos de acción, crear módulo de tareas y responder a la acción de envío del módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-185">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="cbc1f-186">View</span><span class="sxs-lookup"><span data-stu-id="cbc1f-186">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="cbc1f-187">View</span><span class="sxs-lookup"><span data-stu-id="cbc1f-187">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="cbc1f-188">Teams de extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="cbc1f-188">Teams messaging extension search</span></span>   |  <span data-ttu-id="cbc1f-189">Describe cómo definir comandos de búsqueda y responder a las búsquedas.</span><span class="sxs-lookup"><span data-stu-id="cbc1f-189">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="cbc1f-190">View</span><span class="sxs-lookup"><span data-stu-id="cbc1f-190">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="cbc1f-191">View</span><span class="sxs-lookup"><span data-stu-id="cbc1f-191">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="see-also"></a><span data-ttu-id="cbc1f-192">Ver también</span><span class="sxs-lookup"><span data-stu-id="cbc1f-192">See also</span></span>

[<span data-ttu-id="cbc1f-193">Agregar configuración a una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="cbc1f-193">Add configuration to a messaging extension</span></span>](~/get-started/first-message-extension.md)

## <a name="next-step"></a><span data-ttu-id="cbc1f-194">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="cbc1f-194">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cbc1f-195">Agregar autenticación a una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="cbc1f-195">Add authentication to a messaging extension</span></span>](~/messaging-extensions/how-to/add-authentication.md)




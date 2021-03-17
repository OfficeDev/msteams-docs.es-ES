---
title: Referencia de tarjetas
description: Describe todas las tarjetas y acciones de tarjeta disponibles para bots en Teams
keywords: referencia de tarjetas bots
ms.topic: reference
ms.openlocfilehash: 5cb289738f379dedf53f3a96a7dcff61b908e901
ms.sourcegitcommit: 1ce74ed167bb81bf09f7f6f8d518093efafb549e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/16/2021
ms.locfileid: "50827938"
---
# <a name="cards-reference"></a><span data-ttu-id="ec3fd-104">Referencia de tarjetas</span><span class="sxs-lookup"><span data-stu-id="ec3fd-104">Cards reference</span></span>

<span data-ttu-id="ec3fd-105">Las tarjetas enumeradas en esta sección se admiten en bots para Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-105">The cards listed in this section are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="ec3fd-106">Se basan en tarjetas definidas por Bot Framework, pero Teams no admite todas las tarjetas de Bot Framework y ha agregado algunas de sus propias.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span> <span data-ttu-id="ec3fd-107">Las diferencias se llaman en las referencias de este documento.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="ec3fd-108">Ejemplos de tarjetas</span><span class="sxs-lookup"><span data-stu-id="ec3fd-108">Card examples</span></span>

<span data-ttu-id="ec3fd-109">Encontrará información adicional sobre cómo usar tarjetas en la documentación del SDK de Bot Builder (v3).</span><span class="sxs-lookup"><span data-stu-id="ec3fd-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK (v3).</span></span> <span data-ttu-id="ec3fd-110">Los ejemplos de código también están disponibles en el repositorio de Microsoft/BotBuilder-Samples en GitHub.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="ec3fd-111">.NET</span><span class="sxs-lookup"><span data-stu-id="ec3fd-111">.NET</span></span>
  * [<span data-ttu-id="ec3fd-112">Agregar tarjetas como datos adjuntos a los mensajes</span><span class="sxs-lookup"><span data-stu-id="ec3fd-112">Add cards as attachments to messages</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)
  * [<span data-ttu-id="ec3fd-113">Código de ejemplo de tarjetas (Bot Builder v4)</span><span class="sxs-lookup"><span data-stu-id="ec3fd-113">Cards sample code (Bot Builder v4)</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards)

* <span data-ttu-id="ec3fd-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="ec3fd-114">Node.js</span></span>
  * [<span data-ttu-id="ec3fd-115">Agregar tarjetas como datos adjuntos a los mensajes</span><span class="sxs-lookup"><span data-stu-id="ec3fd-115">Add cards as attachments to messages</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
  * [<span data-ttu-id="ec3fd-116">Código de ejemplo de tarjetas (Bot Builder v4)</span><span class="sxs-lookup"><span data-stu-id="ec3fd-116">Cards sample code (Bot Builder v4)</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards)

## <a name="types-of-cards"></a><span data-ttu-id="ec3fd-117">Tipos de tarjetas</span><span class="sxs-lookup"><span data-stu-id="ec3fd-117">Types of cards</span></span>

<span data-ttu-id="ec3fd-118">En esta tabla se muestran los tipos de tarjetas disponibles:</span><span class="sxs-lookup"><span data-stu-id="ec3fd-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="ec3fd-119">Tipo de tarjeta</span><span class="sxs-lookup"><span data-stu-id="ec3fd-119">Card type</span></span> | <span data-ttu-id="ec3fd-120">Description</span><span class="sxs-lookup"><span data-stu-id="ec3fd-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="ec3fd-121">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="ec3fd-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="ec3fd-122">Tarjeta altamente personalizable que puede contener cualquier combinación de texto, voz, imágenes, botones y campos de entrada.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-122">Highly customizable card that can contain any combination of text, speech, images, buttons and input fields.</span></span> |
| [<span data-ttu-id="ec3fd-123">Tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="ec3fd-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="ec3fd-124">Normalmente contiene una sola imagen grande, uno o varios botones y una pequeña cantidad de texto.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-124">Typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="ec3fd-125">Tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="ec3fd-125">List card</span></span>](#list-card) | <span data-ttu-id="ec3fd-126">Una lista de desplazamiento de elementos.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-126">A scrolling list of items.</span></span> |
| [<span data-ttu-id="ec3fd-127">Tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="ec3fd-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="ec3fd-128">Diseño flexible con varias secciones, campos, imágenes y acciones.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-128">Flexible layout with multiple sections, fields, images and actions.</span></span> |
| [<span data-ttu-id="ec3fd-129">Tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="ec3fd-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="ec3fd-130">Proporciona un recibo al usuario.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-130">Provides a receipt to the user.</span></span> |
| [<span data-ttu-id="ec3fd-131">Tarjeta de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="ec3fd-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="ec3fd-132">Permite que un bot solicite que un usuario inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-132">Enables a bot to request that a user sign in.</span></span> |
| [<span data-ttu-id="ec3fd-133">Tarjeta miniatura</span><span class="sxs-lookup"><span data-stu-id="ec3fd-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="ec3fd-134">Normalmente contiene una sola imagen en miniatura, texto corto y uno o más botones.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-134">Typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="ec3fd-135">Colecciones de tarjetas</span><span class="sxs-lookup"><span data-stu-id="ec3fd-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="ec3fd-136">Se usa para devolver varios elementos en una sola respuesta.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-136">Used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="ec3fd-137">Propiedades comunes para todas las tarjetas</span><span class="sxs-lookup"><span data-stu-id="ec3fd-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="ec3fd-138">Imágenes de tarjetas en línea</span><span class="sxs-lookup"><span data-stu-id="ec3fd-138">Inline card images</span></span>

<span data-ttu-id="ec3fd-139">La tarjeta puede contener una imagen en línea al incluir un vínculo a la imagen disponible públicamente.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="ec3fd-140">Por motivos de rendimiento, se recomienda hospedar la imagen en una red pública de entrega de contenido (CDN).</span><span class="sxs-lookup"><span data-stu-id="ec3fd-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="ec3fd-141">Las imágenes se escalan hacia arriba o hacia abajo en tamaño mientras se mantiene la relación de aspecto para cubrir el área de imagen y, a continuación, recortadas desde el centro para lograr la relación de aspecto adecuada para la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area, and then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="ec3fd-142">Las imágenes deben tener como máximo 1024×1024, en formato PNG, JPEG o GIF, y gif animado no es compatible.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-142">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and animated GIF is not supported.</span></span>

| <span data-ttu-id="ec3fd-143">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ec3fd-143">Property</span></span> | <span data-ttu-id="ec3fd-144">Tipo</span><span class="sxs-lookup"><span data-stu-id="ec3fd-144">Type</span></span>  | <span data-ttu-id="ec3fd-145">Description</span><span class="sxs-lookup"><span data-stu-id="ec3fd-145">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ec3fd-146">url</span><span class="sxs-lookup"><span data-stu-id="ec3fd-146">url</span></span> | <span data-ttu-id="ec3fd-147">URL</span><span class="sxs-lookup"><span data-stu-id="ec3fd-147">URL</span></span> | <span data-ttu-id="ec3fd-148">DIRECCIÓN URL HTTPS a la imagen</span><span class="sxs-lookup"><span data-stu-id="ec3fd-148">HTTPS URL to the image</span></span> |
| <span data-ttu-id="ec3fd-149">alt</span><span class="sxs-lookup"><span data-stu-id="ec3fd-149">alt</span></span> | <span data-ttu-id="ec3fd-150">Cadena</span><span class="sxs-lookup"><span data-stu-id="ec3fd-150">String</span></span> | <span data-ttu-id="ec3fd-151">Descripción accesible de la imagen</span><span class="sxs-lookup"><span data-stu-id="ec3fd-151">Accessible description of the image</span></span> |

### <a name="buttons"></a><span data-ttu-id="ec3fd-152">Botones</span><span class="sxs-lookup"><span data-stu-id="ec3fd-152">Buttons</span></span>

<span data-ttu-id="ec3fd-153">Los botones se muestran apilados en la parte inferior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-153">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="ec3fd-154">El texto del botón siempre está en una sola línea y se truncará si el texto supera el ancho del botón.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-154">Button text is always on a single line and will be truncated if the text exceeds the button width.</span></span> <span data-ttu-id="ec3fd-155">No se mostrarán los botones adicionales que supere el número máximo admitido por la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-155">Any additional buttons beyond the maximum number supported by the card will not be shown.</span></span>

<span data-ttu-id="ec3fd-156">Consulta [Acciones de tarjeta](~/task-modules-and-cards/cards/cards-actions.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-156">See [Card Actions](~/task-modules-and-cards/cards/cards-actions.md) for more information.</span></span>

### <a name="card-formatting"></a><span data-ttu-id="ec3fd-157">Formato de tarjeta</span><span class="sxs-lookup"><span data-stu-id="ec3fd-157">Card formatting</span></span>

<span data-ttu-id="ec3fd-158">Consulta [Formato de tarjeta para](~/task-modules-and-cards/cards/cards-format.md) obtener más información sobre el formato de texto en las tarjetas.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-158">See [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for more information on text formatting in cards.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="ec3fd-159">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="ec3fd-159">Adaptive card</span></span>

<span data-ttu-id="ec3fd-160">Una tarjeta adaptable es una tarjeta personalizable que puede contener cualquier combinación de texto, voz, imágenes, botones y campos de entrada.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-160">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="ec3fd-161">Vea [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="ec3fd-161">See [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="ec3fd-162">Compatibilidad con tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="ec3fd-162">Support for adaptive cards</span></span>

| <span data-ttu-id="ec3fd-163">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="ec3fd-163">Bots in Teams</span></span> | <span data-ttu-id="ec3fd-164">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="ec3fd-164">Messaging extensions</span></span>  | <span data-ttu-id="ec3fd-165">Conectores</span><span class="sxs-lookup"><span data-stu-id="ec3fd-165">Connectors</span></span> | <span data-ttu-id="ec3fd-166">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="ec3fd-166">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ec3fd-167">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-167">✔</span></span> | <span data-ttu-id="ec3fd-168">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-168">✔</span></span> | <span data-ttu-id="ec3fd-169">✖</span><span class="sxs-lookup"><span data-stu-id="ec3fd-169">✖</span></span> | <span data-ttu-id="ec3fd-170">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-170">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="ec3fd-171">La plataforma de Teams admite v1.2 o versiones anteriores de características de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-171">Teams platform supports v1.2 or earlier of Adaptive card features.</span></span>
> * <span data-ttu-id="ec3fd-172">Actualmente, los elementos multimedia no se admiten en la tarjeta adaptable v1.2 en la plataforma de Teams.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-172">Media elements are currently not supported in Adaptive card v1.2 on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="ec3fd-173">Ejemplo de una tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="ec3fd-173">Example of an adaptive card</span></span>

![Ejemplo de una tarjeta adaptable](~/assets/images/cards/adaptivecard.png)

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="ec3fd-175">Información adicional sobre tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="ec3fd-175">Additional information on adaptive cards</span></span>

<span data-ttu-id="ec3fd-176">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="ec3fd-176">Bot Framework reference:</span></span>

* [<span data-ttu-id="ec3fd-177">Nodo de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="ec3fd-177">Adaptive cards Node</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="ec3fd-178">Tarjeta adaptable C #</span><span class="sxs-lookup"><span data-stu-id="ec3fd-178">Adaptive card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

## <a name="hero-card"></a><span data-ttu-id="ec3fd-179">Tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="ec3fd-179">Hero card</span></span>

<span data-ttu-id="ec3fd-180">Una tarjeta que normalmente contiene una sola imagen grande, uno o varios botones y texto.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-180">A card that typically contains a single large image, one or more buttons and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="ec3fd-181">Compatibilidad con tarjetas de héroe</span><span class="sxs-lookup"><span data-stu-id="ec3fd-181">Support for hero cards</span></span>

| <span data-ttu-id="ec3fd-182">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="ec3fd-182">Bots in Teams</span></span> | <span data-ttu-id="ec3fd-183">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="ec3fd-183">Messaging Extensions</span></span>  | <span data-ttu-id="ec3fd-184">Conectores</span><span class="sxs-lookup"><span data-stu-id="ec3fd-184">Connectors</span></span> | <span data-ttu-id="ec3fd-185">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="ec3fd-185">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ec3fd-186">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-186">✔</span></span> | <span data-ttu-id="ec3fd-187">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-187">✔</span></span> | <span data-ttu-id="ec3fd-188">✖</span><span class="sxs-lookup"><span data-stu-id="ec3fd-188">✖</span></span> | <span data-ttu-id="ec3fd-189">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-189">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="ec3fd-190">Propiedades de una tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="ec3fd-190">Properties of a hero card</span></span>

| <span data-ttu-id="ec3fd-191">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ec3fd-191">Property</span></span> | <span data-ttu-id="ec3fd-192">Tipo</span><span class="sxs-lookup"><span data-stu-id="ec3fd-192">Type</span></span>  | <span data-ttu-id="ec3fd-193">Description</span><span class="sxs-lookup"><span data-stu-id="ec3fd-193">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ec3fd-194">title</span><span class="sxs-lookup"><span data-stu-id="ec3fd-194">title</span></span> | <span data-ttu-id="ec3fd-195">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="ec3fd-195">Rich text</span></span> | <span data-ttu-id="ec3fd-196">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-196">Title of the card.</span></span> <span data-ttu-id="ec3fd-197">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-197">Maximum 2 lines.</span></span> |
| <span data-ttu-id="ec3fd-198">subtitle</span><span class="sxs-lookup"><span data-stu-id="ec3fd-198">subtitle</span></span> | <span data-ttu-id="ec3fd-199">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="ec3fd-199">Rich text</span></span> | <span data-ttu-id="ec3fd-200">Subtítulo de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-200">Subtitle of the card.</span></span> <span data-ttu-id="ec3fd-201">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-201">Maximum 2 lines.</span></span>|
| <span data-ttu-id="ec3fd-202">text</span><span class="sxs-lookup"><span data-stu-id="ec3fd-202">text</span></span> | <span data-ttu-id="ec3fd-203">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="ec3fd-203">Rich text</span></span> | <span data-ttu-id="ec3fd-204">El texto aparece debajo del subtítulo; vea [Formato de tarjeta para](~/task-modules-and-cards/cards/cards-format.md) las opciones de formato.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-204">Text appears under the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="ec3fd-205">imágenes</span><span class="sxs-lookup"><span data-stu-id="ec3fd-205">images</span></span> | <span data-ttu-id="ec3fd-206">Matriz de imágenes</span><span class="sxs-lookup"><span data-stu-id="ec3fd-206">Array of images</span></span> | <span data-ttu-id="ec3fd-207">Imagen mostrada en la parte superior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-207">Image displayed at top of card.</span></span> <span data-ttu-id="ec3fd-208">Relación de aspecto 16:9.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-208">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="ec3fd-209">botones</span><span class="sxs-lookup"><span data-stu-id="ec3fd-209">buttons</span></span> | <span data-ttu-id="ec3fd-210">Matriz de objetos de acción</span><span class="sxs-lookup"><span data-stu-id="ec3fd-210">Array of action objects</span></span> | <span data-ttu-id="ec3fd-211">Conjunto de acciones aplicables a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-211">Set of actions applicable to the current card.</span></span> <span data-ttu-id="ec3fd-212">Máximo 6.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-212">Maximum 6.</span></span> |
| <span data-ttu-id="ec3fd-213">pulsación</span><span class="sxs-lookup"><span data-stu-id="ec3fd-213">tap</span></span> | <span data-ttu-id="ec3fd-214">Action (objeto)</span><span class="sxs-lookup"><span data-stu-id="ec3fd-214">Action object</span></span> | <span data-ttu-id="ec3fd-215">Esta acción se activará cuando el usuario pulse en la propia tarjeta.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-215">This action will be activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="ec3fd-216">Ejemplo de una tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="ec3fd-216">Example of a hero card</span></span>

![Ejemplo de una tarjeta de héroe](~/assets/images/cards/hero.png)

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="ec3fd-218">Información adicional sobre tarjetas de héroe</span><span class="sxs-lookup"><span data-stu-id="ec3fd-218">Additional information on hero cards</span></span>

<span data-ttu-id="ec3fd-219">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="ec3fd-219">Bot Framework reference:</span></span>

* [<span data-ttu-id="ec3fd-220">Nodo de tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="ec3fd-220">Hero card Node</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="ec3fd-221">Tarjeta de héroe C #</span><span class="sxs-lookup"><span data-stu-id="ec3fd-221">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="ec3fd-222">Tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="ec3fd-222">List card</span></span>

<span data-ttu-id="ec3fd-223">Teams ha agregado la tarjeta de lista para proporcionar funciones más allá de lo que la colección de listas puede proporcionar.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-223">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="ec3fd-224">La tarjeta de lista proporciona una lista de desplazamiento de elementos.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-224">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="ec3fd-225">Compatibilidad con tarjetas de lista</span><span class="sxs-lookup"><span data-stu-id="ec3fd-225">Support for list cards</span></span>

| <span data-ttu-id="ec3fd-226">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="ec3fd-226">Bots in Teams</span></span> | <span data-ttu-id="ec3fd-227">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="ec3fd-227">Messaging extensions</span></span>  | <span data-ttu-id="ec3fd-228">Conectores</span><span class="sxs-lookup"><span data-stu-id="ec3fd-228">Connectors</span></span> | <span data-ttu-id="ec3fd-229">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="ec3fd-229">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ec3fd-230">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-230">✔</span></span> | <span data-ttu-id="ec3fd-231">✖</span><span class="sxs-lookup"><span data-stu-id="ec3fd-231">✖</span></span> | <span data-ttu-id="ec3fd-232">✖</span><span class="sxs-lookup"><span data-stu-id="ec3fd-232">✖</span></span> |<span data-ttu-id="ec3fd-233">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-233">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="ec3fd-234">Propiedades de una tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="ec3fd-234">Properties of a list card</span></span>

| <span data-ttu-id="ec3fd-235">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ec3fd-235">Property</span></span> | <span data-ttu-id="ec3fd-236">Tipo</span><span class="sxs-lookup"><span data-stu-id="ec3fd-236">Type</span></span>  | <span data-ttu-id="ec3fd-237">Description</span><span class="sxs-lookup"><span data-stu-id="ec3fd-237">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ec3fd-238">title</span><span class="sxs-lookup"><span data-stu-id="ec3fd-238">title</span></span> | <span data-ttu-id="ec3fd-239">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="ec3fd-239">Rich text</span></span> | <span data-ttu-id="ec3fd-240">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-240">Title of the card.</span></span> <span data-ttu-id="ec3fd-241">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-241">Maximum 2 lines.</span></span>|
| <span data-ttu-id="ec3fd-242">items</span><span class="sxs-lookup"><span data-stu-id="ec3fd-242">items</span></span> | <span data-ttu-id="ec3fd-243">Matriz de elementos de lista</span><span class="sxs-lookup"><span data-stu-id="ec3fd-243">Array of list items</span></span>  ||
| <span data-ttu-id="ec3fd-244">botones</span><span class="sxs-lookup"><span data-stu-id="ec3fd-244">buttons</span></span> | <span data-ttu-id="ec3fd-245">Matriz de objetos de acción</span><span class="sxs-lookup"><span data-stu-id="ec3fd-245">Array of action objects</span></span> | <span data-ttu-id="ec3fd-246">Conjunto de acciones aplicables a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-246">Set of actions applicable to the current card.</span></span> <span data-ttu-id="ec3fd-247">Máximo 6.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-247">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="ec3fd-248">Ejemplo de una tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="ec3fd-248">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="ec3fd-249">Tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="ec3fd-249">Office 365 connector card</span></span>

<span data-ttu-id="ec3fd-250">La tarjeta del conector de Office 365 se admite en Teams, no en Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-250">The Office 365 Connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="ec3fd-251">Esta tarjeta proporciona un diseño flexible con varias secciones, campos, imágenes y acciones.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-251">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="ec3fd-252">Esta tarjeta encapsula una tarjeta de conector para que la puedan usar los bots.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-252">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="ec3fd-253">Consulta la sección notas para ver las diferencias entre las tarjetas de conector y la tarjeta O365.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-253">See the notes section for differences between connector cards and the O365 card.</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="ec3fd-254">Compatibilidad con tarjetas de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="ec3fd-254">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="ec3fd-255">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="ec3fd-255">Bots in Teams</span></span> | <span data-ttu-id="ec3fd-256">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="ec3fd-256">Messaging extensions</span></span>  | <span data-ttu-id="ec3fd-257">Conectores</span><span class="sxs-lookup"><span data-stu-id="ec3fd-257">Connectors</span></span> | <span data-ttu-id="ec3fd-258">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="ec3fd-258">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ec3fd-259">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-259">✔</span></span> | <span data-ttu-id="ec3fd-260">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-260">✔</span></span> | <span data-ttu-id="ec3fd-261">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-261">✔</span></span> | <span data-ttu-id="ec3fd-262">✖</span><span class="sxs-lookup"><span data-stu-id="ec3fd-262">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="ec3fd-263">Propiedades de la tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="ec3fd-263">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="ec3fd-264">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ec3fd-264">Property</span></span> | <span data-ttu-id="ec3fd-265">Tipo</span><span class="sxs-lookup"><span data-stu-id="ec3fd-265">Type</span></span>  | <span data-ttu-id="ec3fd-266">Description</span><span class="sxs-lookup"><span data-stu-id="ec3fd-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ec3fd-267">title</span><span class="sxs-lookup"><span data-stu-id="ec3fd-267">title</span></span> | <span data-ttu-id="ec3fd-268">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="ec3fd-268">Rich text</span></span> | <span data-ttu-id="ec3fd-269">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-269">Title of the card.</span></span> <span data-ttu-id="ec3fd-270">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-270">Maximum 2 lines.</span></span> |
| <span data-ttu-id="ec3fd-271">summary</span><span class="sxs-lookup"><span data-stu-id="ec3fd-271">summary</span></span> | <span data-ttu-id="ec3fd-272">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="ec3fd-272">Rich text</span></span> | <span data-ttu-id="ec3fd-273">Resumen de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-273">Summary of the card.</span></span> <span data-ttu-id="ec3fd-274">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-274">Maximum 2 lines.</span></span> |
| <span data-ttu-id="ec3fd-275">text</span><span class="sxs-lookup"><span data-stu-id="ec3fd-275">text</span></span> | <span data-ttu-id="ec3fd-276">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="ec3fd-276">Rich text</span></span> | <span data-ttu-id="ec3fd-277">El texto aparece debajo del subtítulo; vea [Formato de tarjeta para](~/task-modules-and-cards/cards/cards-format.md) las opciones de formato.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-277">Text appears under the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="ec3fd-278">themeColor</span><span class="sxs-lookup"><span data-stu-id="ec3fd-278">themeColor</span></span> | <span data-ttu-id="ec3fd-279">Cadena HEX</span><span class="sxs-lookup"><span data-stu-id="ec3fd-279">HEX string</span></span> | <span data-ttu-id="ec3fd-280">Color que reemplaza el accentColor proporcionado desde el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-280">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="ec3fd-281">Notas sobre la tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="ec3fd-281">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="ec3fd-282">Las tarjetas de conector de Office 365 funcionan correctamente en Microsoft Teams, incluidas [las acciones actioncard](/outlook/actionable-messages/card-reference#actioncard-action).</span><span class="sxs-lookup"><span data-stu-id="ec3fd-282">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="ec3fd-283">Una diferencia importante entre el uso de tarjetas de conector desde un conector y el uso de tarjetas de conector en el bot es el control de las acciones de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-283">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="ec3fd-284">Para un conector, el extremo recibe la carga de la tarjeta a través de HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-284">For a connector, the endpoint receives the card payload through HTTP POST.</span></span>
* <span data-ttu-id="ec3fd-285">Para un bot, la acción desencadena una actividad que envía solo el identificador de acción `HttpPOST` y el cuerpo al `invoke` bot.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-285">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="ec3fd-286">Cada tarjeta de conector puede mostrar un máximo de 10 secciones y cada sección puede contener un máximo de 5 imágenes y 5 acciones.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-286">Each connector card can display a maximum of 10 sections, and each section can contain a maximum of 5 images and 5 actions.</span></span>

> [!NOTE]
> <span data-ttu-id="ec3fd-287">Las secciones, imágenes o acciones adicionales de un mensaje no aparecerán.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-287">Any additional sections, images, or actions in a message will not appear.</span></span>

<span data-ttu-id="ec3fd-288">Todos los campos de texto admiten Markdown y HTML.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-288">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="ec3fd-289">Puede controlar qué secciones usan Markdown o HTML estableciendo la `markdown` propiedad en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-289">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="ec3fd-290">De forma predeterminada, `markdown` se establece en ; si desea usar HTML en su `true` lugar, establezca en `markdown` `false` .</span><span class="sxs-lookup"><span data-stu-id="ec3fd-290">By default, `markdown` is set to `true`; if you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="ec3fd-291">Si especifica la `themeColor` propiedad, invalida la `accentColor` propiedad en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-291">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="ec3fd-292">Para especificar el estilo de representación `activityImage` para , puede establecer lo `activityImageType` siguiente:</span><span class="sxs-lookup"><span data-stu-id="ec3fd-292">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="ec3fd-293">Valor</span><span class="sxs-lookup"><span data-stu-id="ec3fd-293">Value</span></span> | <span data-ttu-id="ec3fd-294">Description</span><span class="sxs-lookup"><span data-stu-id="ec3fd-294">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="ec3fd-295">Valor predeterminado; `activityImage` se recortará como un círculo.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-295">Default; `activityImage` will be cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="ec3fd-296">`activityImage` se mostrará como un rectángulo y conservará su relación de aspecto.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-296">`activityImage` will be displayed as a rectangle and retain its aspect ratio.</span></span> |

<span data-ttu-id="ec3fd-297">Para obtener todos los demás detalles acerca de las propiedades de la tarjeta de conector, consulte [referencia de tarjeta de mensaje de acción.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="ec3fd-297">For all other details about connector card properties, see the [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="ec3fd-298">Las únicas propiedades de tarjeta de conector que Microsoft Teams no admite actualmente son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="ec3fd-298">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="ec3fd-299">`startGroup` (siempre tratado como `true` en Teams)</span><span class="sxs-lookup"><span data-stu-id="ec3fd-299">`startGroup` (always treated as `true` in Teams)</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="ec3fd-300">Ejemplo de una tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="ec3fd-300">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="ec3fd-301">Tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="ec3fd-301">Receipt card</span></span>

<span data-ttu-id="ec3fd-302">Teams admite tarjeta de recibo.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-302">Teams supports receipt card.</span></span> <span data-ttu-id="ec3fd-303">Es una tarjeta que permite a un bot proporcionar un recibo al usuario.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-303">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="ec3fd-304">Normalmente contiene la lista de elementos que se deben incluir en el recibo, como impuestos y la información total.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-304">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="ec3fd-305">Compatibilidad con tarjetas de recibo</span><span class="sxs-lookup"><span data-stu-id="ec3fd-305">Support for receipt cards</span></span>

| <span data-ttu-id="ec3fd-306">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="ec3fd-306">Bots in Teams</span></span> | <span data-ttu-id="ec3fd-307">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="ec3fd-307">Messaging extensions</span></span>  | <span data-ttu-id="ec3fd-308">Conectores</span><span class="sxs-lookup"><span data-stu-id="ec3fd-308">Connectors</span></span> | <span data-ttu-id="ec3fd-309">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="ec3fd-309">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ec3fd-310">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-310">✔</span></span> | <span data-ttu-id="ec3fd-311">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-311">✔</span></span> | <span data-ttu-id="ec3fd-312">✖</span><span class="sxs-lookup"><span data-stu-id="ec3fd-312">✖</span></span> | <span data-ttu-id="ec3fd-313">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-313">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="ec3fd-314">Ejemplo de una tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="ec3fd-314">Example of a receipt card</span></span>

![Ejemplo de una tarjeta de recibo](~/assets/images/cards/receipt.png)

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="ec3fd-316">Información adicional sobre tarjetas de recibo</span><span class="sxs-lookup"><span data-stu-id="ec3fd-316">Additional information on receipt cards</span></span>

<span data-ttu-id="ec3fd-317">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="ec3fd-317">Bot Framework reference:</span></span>

* [<span data-ttu-id="ec3fd-318">Nodo de tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="ec3fd-318">Receipt card Node</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="ec3fd-319">Tarjeta de recibo C #</span><span class="sxs-lookup"><span data-stu-id="ec3fd-319">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="ec3fd-320">Tarjeta de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="ec3fd-320">Signin card</span></span>

<span data-ttu-id="ec3fd-321">La tarjeta de inicio de sesión permite que un bot solicite a un usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-321">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="ec3fd-322">Se admite en Teams de una forma ligeramente diferente a la que se encuentra en Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-322">Supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="ec3fd-323">La tarjeta de inicio de sesión en Teams es similar a la tarjeta de inicio de sesión en Bot Framework, excepto que la tarjeta de inicio de sesión en Teams solo admite dos `signin` acciones: y `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="ec3fd-323">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="ec3fd-324">La **acción de inicio de** sesión se puede usar desde cualquier tarjeta de Teams, no solo desde la tarjeta de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-324">The **signin action** can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="ec3fd-325">Para obtener más información sobre la autenticación, vea [Flujo de autenticación de Microsoft Teams para bots](~/bots/how-to/authentication/auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="ec3fd-325">For more details on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="ec3fd-326">Compatibilidad con tarjetas de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="ec3fd-326">Support for Signin cards</span></span>

| <span data-ttu-id="ec3fd-327">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="ec3fd-327">Bots in Teams</span></span> | <span data-ttu-id="ec3fd-328">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="ec3fd-328">Messaging extensions</span></span>  | <span data-ttu-id="ec3fd-329">Conectores</span><span class="sxs-lookup"><span data-stu-id="ec3fd-329">Connectors</span></span> | <span data-ttu-id="ec3fd-330">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="ec3fd-330">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ec3fd-331">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-331">✔</span></span> | <span data-ttu-id="ec3fd-332">✖</span><span class="sxs-lookup"><span data-stu-id="ec3fd-332">✖</span></span> | <span data-ttu-id="ec3fd-333">✖</span><span class="sxs-lookup"><span data-stu-id="ec3fd-333">✖</span></span> | <span data-ttu-id="ec3fd-334">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-334">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="ec3fd-335">Información adicional sobre tarjetas de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="ec3fd-335">Additional information on signin cards</span></span>

<span data-ttu-id="ec3fd-336">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="ec3fd-336">Bot Framework reference:</span></span>

* [<span data-ttu-id="ec3fd-337">Nodo de tarjeta de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="ec3fd-337">Signin card Node</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="ec3fd-338">Tarjeta de inicio de sesión C #</span><span class="sxs-lookup"><span data-stu-id="ec3fd-338">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="ec3fd-339">Tarjeta miniatura</span><span class="sxs-lookup"><span data-stu-id="ec3fd-339">Thumbnail card</span></span>

<span data-ttu-id="ec3fd-340">Una tarjeta que normalmente contiene una sola imagen en miniatura, uno o varios botones y texto.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-340">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="ec3fd-341">Compatibilidad con tarjetas en miniatura</span><span class="sxs-lookup"><span data-stu-id="ec3fd-341">Support for thumbnail cards</span></span>

| <span data-ttu-id="ec3fd-342">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="ec3fd-342">Bots in Teams</span></span> | <span data-ttu-id="ec3fd-343">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="ec3fd-343">Messaging extensions</span></span>  | <span data-ttu-id="ec3fd-344">Conectores</span><span class="sxs-lookup"><span data-stu-id="ec3fd-344">Connectors</span></span> | <span data-ttu-id="ec3fd-345">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="ec3fd-345">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ec3fd-346">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-346">✔</span></span> | <span data-ttu-id="ec3fd-347">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-347">✔</span></span> | <span data-ttu-id="ec3fd-348">✖</span><span class="sxs-lookup"><span data-stu-id="ec3fd-348">✖</span></span> | <span data-ttu-id="ec3fd-349">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-349">✔</span></span> |

![Ejemplo de una tarjeta en miniatura](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="ec3fd-351">Propiedades de una tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="ec3fd-351">Properties of a thumbnail card</span></span>

| <span data-ttu-id="ec3fd-352">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ec3fd-352">Property</span></span> | <span data-ttu-id="ec3fd-353">Tipo</span><span class="sxs-lookup"><span data-stu-id="ec3fd-353">Type</span></span>  | <span data-ttu-id="ec3fd-354">Description</span><span class="sxs-lookup"><span data-stu-id="ec3fd-354">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ec3fd-355">title</span><span class="sxs-lookup"><span data-stu-id="ec3fd-355">title</span></span> | <span data-ttu-id="ec3fd-356">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="ec3fd-356">Rich text</span></span> | <span data-ttu-id="ec3fd-357">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-357">Title of the card.</span></span> <span data-ttu-id="ec3fd-358">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-358">Maximum 2 lines.</span></span>|
| <span data-ttu-id="ec3fd-359">subtitle</span><span class="sxs-lookup"><span data-stu-id="ec3fd-359">subtitle</span></span> | <span data-ttu-id="ec3fd-360">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="ec3fd-360">Rich text</span></span> | <span data-ttu-id="ec3fd-361">Subtítulo de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-361">Subtitle of the card.</span></span> <span data-ttu-id="ec3fd-362">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-362">Maximum 2 lines.</span></span>|
| <span data-ttu-id="ec3fd-363">text</span><span class="sxs-lookup"><span data-stu-id="ec3fd-363">text</span></span> | <span data-ttu-id="ec3fd-364">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="ec3fd-364">Rich text</span></span> | <span data-ttu-id="ec3fd-365">El texto aparece debajo del subtítulo; vea [Formato de tarjeta para](~/task-modules-and-cards/cards/cards-format.md) las opciones de formato.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-365">Text appears under the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="ec3fd-366">imágenes</span><span class="sxs-lookup"><span data-stu-id="ec3fd-366">images</span></span> | <span data-ttu-id="ec3fd-367">Matriz de imágenes</span><span class="sxs-lookup"><span data-stu-id="ec3fd-367">Array of images</span></span> | <span data-ttu-id="ec3fd-368">Imagen mostrada en la parte superior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-368">Image displayed at top of card.</span></span> <span data-ttu-id="ec3fd-369">Relación de aspecto 1:1 (cuadrado).</span><span class="sxs-lookup"><span data-stu-id="ec3fd-369">Aspect ratio 1:1 (square).</span></span> |
| <span data-ttu-id="ec3fd-370">botones</span><span class="sxs-lookup"><span data-stu-id="ec3fd-370">buttons</span></span> | <span data-ttu-id="ec3fd-371">Matriz de objetos de acción</span><span class="sxs-lookup"><span data-stu-id="ec3fd-371">Array of action objects</span></span> | <span data-ttu-id="ec3fd-372">Conjunto de acciones aplicables a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-372">Set of actions applicable to the current card.</span></span> <span data-ttu-id="ec3fd-373">Máximo 6.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-373">Maximum 6.</span></span> |
| <span data-ttu-id="ec3fd-374">pulsación</span><span class="sxs-lookup"><span data-stu-id="ec3fd-374">tap</span></span> | <span data-ttu-id="ec3fd-375">Action (objeto)</span><span class="sxs-lookup"><span data-stu-id="ec3fd-375">Action object</span></span> | <span data-ttu-id="ec3fd-376">Esta acción se activará cuando el usuario pulse en la propia tarjeta.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-376">This action will be activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="ec3fd-377">Ejemplo de una tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="ec3fd-377">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="ec3fd-378">Información adicional</span><span class="sxs-lookup"><span data-stu-id="ec3fd-378">Additional information</span></span>

<span data-ttu-id="ec3fd-379">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="ec3fd-379">Bot Framework reference:</span></span>

* [<span data-ttu-id="ec3fd-380">Nodo de tarjeta de miniatura</span><span class="sxs-lookup"><span data-stu-id="ec3fd-380">Thumbnail card Node</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="ec3fd-381">Tarjeta de miniatura C #</span><span class="sxs-lookup"><span data-stu-id="ec3fd-381">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="ec3fd-382">Colecciones de tarjetas</span><span class="sxs-lookup"><span data-stu-id="ec3fd-382">Card collections</span></span>

<span data-ttu-id="ec3fd-383">Teams admite colecciones de tarjetas.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-383">Teams supports Card collections.</span></span>

<span data-ttu-id="ec3fd-384">Colecciones de tarjetas: `builder.AttachmentLayout.carousel` y `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="ec3fd-384">Card collections: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="ec3fd-385">Estas colecciones contienen tarjetas adaptables, de héroe o en miniatura.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-385">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="ec3fd-386">Colección Carousel</span><span class="sxs-lookup"><span data-stu-id="ec3fd-386">Carousel collection</span></span>

<span data-ttu-id="ec3fd-387">El [diseño del carrusel](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) muestra un carrusel de tarjetas, opcionalmente con botones de acción asociados.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-387">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="ec3fd-388">Compatibilidad con colecciones de carrusel</span><span class="sxs-lookup"><span data-stu-id="ec3fd-388">Support for carousel collections</span></span>

| <span data-ttu-id="ec3fd-389">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="ec3fd-389">Bots in Teams</span></span> | <span data-ttu-id="ec3fd-390">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="ec3fd-390">Messaging extensions</span></span>  | <span data-ttu-id="ec3fd-391">Conectores</span><span class="sxs-lookup"><span data-stu-id="ec3fd-391">Connectors</span></span> | <span data-ttu-id="ec3fd-392">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="ec3fd-392">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ec3fd-393">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-393">✔</span></span> | <span data-ttu-id="ec3fd-394">✖</span><span class="sxs-lookup"><span data-stu-id="ec3fd-394">✖</span></span> | <span data-ttu-id="ec3fd-395">✖</span><span class="sxs-lookup"><span data-stu-id="ec3fd-395">✖</span></span> | <span data-ttu-id="ec3fd-396">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-396">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="ec3fd-397">Un carrusel puede mostrar un máximo de 10 tarjetas por mensaje.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-397">A carousel can display a maximum of 10 cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="ec3fd-398">Propiedades de una tarjeta de carrusel</span><span class="sxs-lookup"><span data-stu-id="ec3fd-398">Properties of a carousel card</span></span>

<span data-ttu-id="ec3fd-399">Las propiedades de una tarjeta carrusel son las mismas que las de las tarjetas Hero y Thumbnail.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-399">Properties of a Carousel card are same as those of the Hero and Thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="ec3fd-400">Ejemplo de una colección de carrusel</span><span class="sxs-lookup"><span data-stu-id="ec3fd-400">Example of a carousel collection</span></span>

![Ejemplo de un carrusel de tarjetas](~/assets/images/cards/carousel.png)

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="ec3fd-402">Sintaxis para colecciones de carrusel</span><span class="sxs-lookup"><span data-stu-id="ec3fd-402">Syntax for carousel collections</span></span>

`builder.AttachmentLayoutTypes.Carousel`

## <a name="list-collection"></a><span data-ttu-id="ec3fd-403">Colección List</span><span class="sxs-lookup"><span data-stu-id="ec3fd-403">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="ec3fd-404">Compatibilidad con colecciones de listas</span><span class="sxs-lookup"><span data-stu-id="ec3fd-404">Support for list collections</span></span>

<span data-ttu-id="ec3fd-405">El diseño de lista muestra una lista verticalmente apilada de tarjetas, opcionalmente con botones de acción asociados.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-405">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="ec3fd-406">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="ec3fd-406">Bots in Teams</span></span> | <span data-ttu-id="ec3fd-407">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="ec3fd-407">Messaging extensions</span></span>  | <span data-ttu-id="ec3fd-408">Conectores</span><span class="sxs-lookup"><span data-stu-id="ec3fd-408">Connectors</span></span> | <span data-ttu-id="ec3fd-409">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="ec3fd-409">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ec3fd-410">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-410">✔</span></span> | <span data-ttu-id="ec3fd-411">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-411">✔</span></span> | <span data-ttu-id="ec3fd-412">✖</span><span class="sxs-lookup"><span data-stu-id="ec3fd-412">✖</span></span> | <span data-ttu-id="ec3fd-413">✔</span><span class="sxs-lookup"><span data-stu-id="ec3fd-413">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="ec3fd-414">Ejemplo de una colección de listas</span><span class="sxs-lookup"><span data-stu-id="ec3fd-414">Example of a list collection</span></span>

![Ejemplo de una lista de tarjetas](~/assets/images/cards/list.png)

<span data-ttu-id="ec3fd-416">Las propiedades son las mismas que para la tarjeta de miniatura o de héroe.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-416">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="ec3fd-417">Una lista puede mostrar un máximo de 10 tarjetas por mensaje.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-417">A list can display a maximum of 10 cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="ec3fd-418">Algunas combinaciones de tarjetas de lista aún no son compatibles con iOS y Android.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-418">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="ec3fd-419">Sintaxis para colecciones de listas</span><span class="sxs-lookup"><span data-stu-id="ec3fd-419">Syntax for list collections</span></span>

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="ec3fd-420">Tarjetas no admitidas en Teams</span><span class="sxs-lookup"><span data-stu-id="ec3fd-420">Cards not supported in Teams</span></span>

<span data-ttu-id="ec3fd-421">Teams no admite las siguientes tarjetas.</span><span class="sxs-lookup"><span data-stu-id="ec3fd-421">The following cards are implemented by the Bot Framework, but are NOT supported by Teams.</span></span>

* <span data-ttu-id="ec3fd-422">Tarjetas de animación</span><span class="sxs-lookup"><span data-stu-id="ec3fd-422">Animation cards</span></span>
* <span data-ttu-id="ec3fd-423">Tarjetas de audio</span><span class="sxs-lookup"><span data-stu-id="ec3fd-423">Audio cards</span></span>
* <span data-ttu-id="ec3fd-424">Tarjetas de vídeo</span><span class="sxs-lookup"><span data-stu-id="ec3fd-424">Video cards</span></span>

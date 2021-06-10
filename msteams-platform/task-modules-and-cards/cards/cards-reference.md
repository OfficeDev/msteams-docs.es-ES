---
title: Referencia de tarjetas
description: Describe todas las tarjetas y acciones de tarjeta disponibles para bots en Teams
localization_priority: Normal
keywords: referencia de tarjetas bots
ms.topic: reference
ms.openlocfilehash: d3f0904326f951475c8a0d3e17daf720d9aad489
ms.sourcegitcommit: c59d90ae03eae32996db49f162855965b55c52fe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/26/2021
ms.locfileid: "52668865"
---
# <a name="cards-reference"></a><span data-ttu-id="17ce4-104">Referencia de tarjetas</span><span class="sxs-lookup"><span data-stu-id="17ce4-104">Cards reference</span></span>

<span data-ttu-id="17ce4-105">Las tarjetas enumeradas en este documento se admiten en bots para Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="17ce4-105">The cards listed in this document are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="17ce4-106">Se basan en tarjetas definidas por Bot Framework (BF), pero Teams no admite todas las tarjetas de Bot Framework y, en su lugar, se han agregado algunas Teams tarjetas.</span><span class="sxs-lookup"><span data-stu-id="17ce4-106">They are based on cards defined by the Bot Framework (BF), but Teams does not support all Bot Framework cards and instead some Teams cards have been added.</span></span> <span data-ttu-id="17ce4-107">Las diferencias se llaman en las referencias de este documento.</span><span class="sxs-lookup"><span data-stu-id="17ce4-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="17ce4-108">Ejemplos de tarjetas</span><span class="sxs-lookup"><span data-stu-id="17ce4-108">Card examples</span></span>

<span data-ttu-id="17ce4-109">Encontrará información adicional sobre cómo usar tarjetas en la documentación del SDK de Bot Builder v3.</span><span class="sxs-lookup"><span data-stu-id="17ce4-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="17ce4-110">Los ejemplos de código también están disponibles en el repositorio microsoft/BotBuilder-Samples en GitHub.</span><span class="sxs-lookup"><span data-stu-id="17ce4-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="17ce4-111">.NET</span><span class="sxs-lookup"><span data-stu-id="17ce4-111">.NET</span></span>
  * <span data-ttu-id="17ce4-112">[Agregar tarjetas como datos adjuntos a los mensajes](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="17ce4-112">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="17ce4-113">[Código de ejemplo de tarjetas Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="17ce4-113">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span></span>

* <span data-ttu-id="17ce4-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="17ce4-114">Node.js</span></span>
  * <span data-ttu-id="17ce4-115">[Agregar tarjetas como datos adjuntos a los mensajes](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="17ce4-115">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="17ce4-116">[Código de ejemplo de tarjetas Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="17ce4-116">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span></span>

## <a name="types-of-cards"></a><span data-ttu-id="17ce4-117">Tipos de tarjetas</span><span class="sxs-lookup"><span data-stu-id="17ce4-117">Types of cards</span></span>

<span data-ttu-id="17ce4-118">En esta tabla se muestran los tipos de tarjetas disponibles:</span><span class="sxs-lookup"><span data-stu-id="17ce4-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="17ce4-119">Tipo de tarjeta</span><span class="sxs-lookup"><span data-stu-id="17ce4-119">Card type</span></span> | <span data-ttu-id="17ce4-120">Descripción</span><span class="sxs-lookup"><span data-stu-id="17ce4-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="17ce4-121">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="17ce4-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="17ce4-122">Esta tarjeta es una tarjeta altamente personalizable que puede contener cualquier combinación de texto, voz, imágenes, botones y campos de entrada.</span><span class="sxs-lookup"><span data-stu-id="17ce4-122">This card is highly customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="17ce4-123">Tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="17ce4-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="17ce4-124">Esta tarjeta normalmente contiene una sola imagen grande, uno o varios botones y una pequeña cantidad de texto.</span><span class="sxs-lookup"><span data-stu-id="17ce4-124">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="17ce4-125">Tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="17ce4-125">List card</span></span>](#list-card) | <span data-ttu-id="17ce4-126">Esta tarjeta es una lista de desplazamiento de elementos.</span><span class="sxs-lookup"><span data-stu-id="17ce4-126">This card is a scrolling list of items.</span></span> |
| [<span data-ttu-id="17ce4-127">Office 365 de conector</span><span class="sxs-lookup"><span data-stu-id="17ce4-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="17ce4-128">Esta tarjeta tiene un diseño flexible con varias secciones, campos, imágenes y acciones.</span><span class="sxs-lookup"><span data-stu-id="17ce4-128">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="17ce4-129">Tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="17ce4-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="17ce4-130">Esta tarjeta proporciona un recibo al usuario.</span><span class="sxs-lookup"><span data-stu-id="17ce4-130">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="17ce4-131">Tarjeta de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="17ce4-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="17ce4-132">Esta tarjeta permite que un bot solicite que un usuario inicia sesión.</span><span class="sxs-lookup"><span data-stu-id="17ce4-132">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="17ce4-133">Tarjeta miniatura</span><span class="sxs-lookup"><span data-stu-id="17ce4-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="17ce4-134">Esta tarjeta normalmente contiene una sola imagen en miniatura, texto corto y uno o más botones.</span><span class="sxs-lookup"><span data-stu-id="17ce4-134">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="17ce4-135">Colecciones de tarjetas</span><span class="sxs-lookup"><span data-stu-id="17ce4-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="17ce4-136">Estas tarjetas se usan para devolver varios elementos en una sola respuesta.</span><span class="sxs-lookup"><span data-stu-id="17ce4-136">This cards is used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="17ce4-137">Propiedades comunes para todas las tarjetas</span><span class="sxs-lookup"><span data-stu-id="17ce4-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="17ce4-138">Imágenes de tarjetas en línea</span><span class="sxs-lookup"><span data-stu-id="17ce4-138">Inline card images</span></span>

<span data-ttu-id="17ce4-139">La tarjeta puede contener una imagen en línea al incluir un vínculo a la imagen disponible públicamente.</span><span class="sxs-lookup"><span data-stu-id="17ce4-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="17ce4-140">Por motivos de rendimiento, se recomienda hospedar la imagen en una red pública de entrega de contenido (CDN).</span><span class="sxs-lookup"><span data-stu-id="17ce4-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="17ce4-141">Las imágenes se escalan hacia arriba o hacia abajo en tamaño mientras se mantiene la relación de aspecto para cubrir el área de la imagen.</span><span class="sxs-lookup"><span data-stu-id="17ce4-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area.</span></span> <span data-ttu-id="17ce4-142">A continuación, las imágenes se recortan desde el centro para lograr la relación de aspecto adecuada para la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="17ce4-142">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="17ce4-143">Las imágenes deben tener como máximo 1024×1024, en formato PNG, JPEG o GIF, y no admiten GIF animados.</span><span class="sxs-lookup"><span data-stu-id="17ce4-143">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and do not support animated GIF.</span></span>

| <span data-ttu-id="17ce4-144">Propiedad</span><span class="sxs-lookup"><span data-stu-id="17ce4-144">Property</span></span> | <span data-ttu-id="17ce4-145">Tipo</span><span class="sxs-lookup"><span data-stu-id="17ce4-145">Type</span></span>  | <span data-ttu-id="17ce4-146">Descripción</span><span class="sxs-lookup"><span data-stu-id="17ce4-146">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="17ce4-147">url</span><span class="sxs-lookup"><span data-stu-id="17ce4-147">url</span></span> | <span data-ttu-id="17ce4-148">URL</span><span class="sxs-lookup"><span data-stu-id="17ce4-148">URL</span></span> | <span data-ttu-id="17ce4-149">DIRECCIÓN URL HTTPS a la imagen.</span><span class="sxs-lookup"><span data-stu-id="17ce4-149">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="17ce4-150">alt</span><span class="sxs-lookup"><span data-stu-id="17ce4-150">alt</span></span> | <span data-ttu-id="17ce4-151">Cadena</span><span class="sxs-lookup"><span data-stu-id="17ce4-151">String</span></span> | <span data-ttu-id="17ce4-152">Descripción accesible de la imagen.</span><span class="sxs-lookup"><span data-stu-id="17ce4-152">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="17ce4-153">Si una tarjeta incluye una dirección URL de imagen que pasa por un redireccionamiento antes de la imagen final, no se admite el redireccionamiento en la dirección URL de la imagen.</span><span class="sxs-lookup"><span data-stu-id="17ce4-153">If a card includes an image URL that goes through a redirect before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="17ce4-154">Esto ocurre para las imágenes compartidas en la nube pública.</span><span class="sxs-lookup"><span data-stu-id="17ce4-154">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="17ce4-155">Botones</span><span class="sxs-lookup"><span data-stu-id="17ce4-155">Buttons</span></span>

<span data-ttu-id="17ce4-156">Los botones se muestran apilados en la parte inferior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="17ce4-156">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="17ce4-157">El texto del botón siempre está en una sola línea y se trunca si el texto supera el ancho del botón.</span><span class="sxs-lookup"><span data-stu-id="17ce4-157">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="17ce4-158">No se muestran los botones adicionales que supere el número máximo admitido por la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="17ce4-158">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="17ce4-159">Para obtener más información, vea [acciones de tarjeta](~/task-modules-and-cards/cards/cards-actions.md).</span><span class="sxs-lookup"><span data-stu-id="17ce4-159">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="17ce4-160">Formato de tarjeta</span><span class="sxs-lookup"><span data-stu-id="17ce4-160">Card formatting</span></span>

<span data-ttu-id="17ce4-161">Para obtener más información sobre el formato de texto en tarjetas, vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="17ce4-161">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="17ce4-162">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="17ce4-162">Adaptive card</span></span>

<span data-ttu-id="17ce4-163">Una tarjeta adaptable es una tarjeta personalizable que puede contener cualquier combinación de texto, voz, imágenes, botones y campos de entrada.</span><span class="sxs-lookup"><span data-stu-id="17ce4-163">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="17ce4-164">Para obtener más información, [vea adaptive cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="17ce4-164">For more information, see [adaptive cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="17ce4-165">Compatibilidad con tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="17ce4-165">Support for adaptive cards</span></span>

| <span data-ttu-id="17ce4-166">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="17ce4-166">Bots in Teams</span></span> | <span data-ttu-id="17ce4-167">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="17ce4-167">Messaging extensions</span></span>  | <span data-ttu-id="17ce4-168">Conectores</span><span class="sxs-lookup"><span data-stu-id="17ce4-168">Connectors</span></span> | <span data-ttu-id="17ce4-169">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="17ce4-169">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="17ce4-170">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-170">✔</span></span> | <span data-ttu-id="17ce4-171">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-171">✔</span></span> | <span data-ttu-id="17ce4-172">✖</span><span class="sxs-lookup"><span data-stu-id="17ce4-172">✖</span></span> | <span data-ttu-id="17ce4-173">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-173">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="17ce4-174">Teams plataforma admite v1.2 o versiones anteriores de características de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="17ce4-174">Teams platform supports v1.2 or earlier of adaptive card features.</span></span>
> * <span data-ttu-id="17ce4-175">Actualmente, los elementos multimedia no se admiten en la tarjeta adaptable v1.2 en la Teams web.</span><span class="sxs-lookup"><span data-stu-id="17ce4-175">Media elements are currently not supported in adaptive card v1.2 on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="17ce4-176">Ejemplo de una tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="17ce4-176">Example of an adaptive card</span></span>

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="17ce4-178">Información adicional sobre tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="17ce4-178">Additional information on adaptive cards</span></span>

<span data-ttu-id="17ce4-179">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="17ce4-179">Bot Framework reference:</span></span>

* [<span data-ttu-id="17ce4-180">Tarjetas adaptables Node.js</span><span class="sxs-lookup"><span data-stu-id="17ce4-180">Adaptive cards Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="17ce4-181">Tarjeta adaptable C #</span><span class="sxs-lookup"><span data-stu-id="17ce4-181">Adaptive card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

## <a name="hero-card"></a><span data-ttu-id="17ce4-182">Tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="17ce4-182">Hero card</span></span>

<span data-ttu-id="17ce4-183">Una tarjeta que normalmente contiene una sola imagen grande, uno o varios botones y texto.</span><span class="sxs-lookup"><span data-stu-id="17ce4-183">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="17ce4-184">Compatibilidad con tarjetas de héroe</span><span class="sxs-lookup"><span data-stu-id="17ce4-184">Support for hero cards</span></span>

| <span data-ttu-id="17ce4-185">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="17ce4-185">Bots in Teams</span></span> | <span data-ttu-id="17ce4-186">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="17ce4-186">Messaging extensions</span></span>  | <span data-ttu-id="17ce4-187">Conectores</span><span class="sxs-lookup"><span data-stu-id="17ce4-187">Connectors</span></span> | <span data-ttu-id="17ce4-188">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="17ce4-188">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="17ce4-189">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-189">✔</span></span> | <span data-ttu-id="17ce4-190">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-190">✔</span></span> | <span data-ttu-id="17ce4-191">✖</span><span class="sxs-lookup"><span data-stu-id="17ce4-191">✖</span></span> | <span data-ttu-id="17ce4-192">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-192">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="17ce4-193">Propiedades de una tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="17ce4-193">Properties of a hero card</span></span>

| <span data-ttu-id="17ce4-194">Propiedad</span><span class="sxs-lookup"><span data-stu-id="17ce4-194">Property</span></span> | <span data-ttu-id="17ce4-195">Tipo</span><span class="sxs-lookup"><span data-stu-id="17ce4-195">Type</span></span>  | <span data-ttu-id="17ce4-196">Description</span><span class="sxs-lookup"><span data-stu-id="17ce4-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="17ce4-197">title</span><span class="sxs-lookup"><span data-stu-id="17ce4-197">title</span></span> | <span data-ttu-id="17ce4-198">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="17ce4-198">Rich text</span></span> | <span data-ttu-id="17ce4-199">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="17ce4-199">Title of the card.</span></span> <span data-ttu-id="17ce4-200">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="17ce4-200">Maximum 2 lines.</span></span> |
| <span data-ttu-id="17ce4-201">subtitle</span><span class="sxs-lookup"><span data-stu-id="17ce4-201">subtitle</span></span> | <span data-ttu-id="17ce4-202">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="17ce4-202">Rich text</span></span> | <span data-ttu-id="17ce4-203">Subtítulo de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="17ce4-203">Subtitle of the card.</span></span> <span data-ttu-id="17ce4-204">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="17ce4-204">Maximum 2 lines.</span></span>|
| <span data-ttu-id="17ce4-205">text</span><span class="sxs-lookup"><span data-stu-id="17ce4-205">text</span></span> | <span data-ttu-id="17ce4-206">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="17ce4-206">Rich text</span></span> | <span data-ttu-id="17ce4-207">El texto aparece debajo del subtítulo.</span><span class="sxs-lookup"><span data-stu-id="17ce4-207">Text appears under the subtitle.</span></span> <span data-ttu-id="17ce4-208">Para ver las opciones de formato, vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="17ce4-208">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="17ce4-209">imágenes</span><span class="sxs-lookup"><span data-stu-id="17ce4-209">images</span></span> | <span data-ttu-id="17ce4-210">Matriz de imágenes</span><span class="sxs-lookup"><span data-stu-id="17ce4-210">Array of images</span></span> | <span data-ttu-id="17ce4-211">Imagen que se muestra en la parte superior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="17ce4-211">Image displayed at the top of the card.</span></span> <span data-ttu-id="17ce4-212">Relación de aspecto 16:9.</span><span class="sxs-lookup"><span data-stu-id="17ce4-212">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="17ce4-213">botones</span><span class="sxs-lookup"><span data-stu-id="17ce4-213">buttons</span></span> | <span data-ttu-id="17ce4-214">Matriz de objetos de acción</span><span class="sxs-lookup"><span data-stu-id="17ce4-214">Array of action objects</span></span> | <span data-ttu-id="17ce4-215">Conjunto de acciones aplicables a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="17ce4-215">Set of actions applicable to the current card.</span></span> <span data-ttu-id="17ce4-216">Máximo 6.</span><span class="sxs-lookup"><span data-stu-id="17ce4-216">Maximum 6.</span></span> |
| <span data-ttu-id="17ce4-217">pulsación</span><span class="sxs-lookup"><span data-stu-id="17ce4-217">tap</span></span> | <span data-ttu-id="17ce4-218">Action (objeto)</span><span class="sxs-lookup"><span data-stu-id="17ce4-218">Action object</span></span> | <span data-ttu-id="17ce4-219">Se activa cuando el usuario pulsa en la propia tarjeta.</span><span class="sxs-lookup"><span data-stu-id="17ce4-219">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="17ce4-220">Ejemplo de una tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="17ce4-220">Example of a hero card</span></span>

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="17ce4-222">Información adicional sobre tarjetas de héroe</span><span class="sxs-lookup"><span data-stu-id="17ce4-222">Additional information on hero cards</span></span>

<span data-ttu-id="17ce4-223">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="17ce4-223">Bot Framework reference:</span></span>

* [<span data-ttu-id="17ce4-224">Tarjeta de Node.js</span><span class="sxs-lookup"><span data-stu-id="17ce4-224">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="17ce4-225">Tarjeta de héroe C #</span><span class="sxs-lookup"><span data-stu-id="17ce4-225">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="17ce4-226">Tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="17ce4-226">List card</span></span>

<span data-ttu-id="17ce4-227">La tarjeta de lista se ha agregado Teams para proporcionar funciones más allá de lo que la colección de listas puede proporcionar.</span><span class="sxs-lookup"><span data-stu-id="17ce4-227">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="17ce4-228">La tarjeta de lista proporciona una lista de desplazamiento de elementos.</span><span class="sxs-lookup"><span data-stu-id="17ce4-228">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="17ce4-229">Compatibilidad con tarjetas de lista</span><span class="sxs-lookup"><span data-stu-id="17ce4-229">Support for list cards</span></span>

| <span data-ttu-id="17ce4-230">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="17ce4-230">Bots in Teams</span></span> | <span data-ttu-id="17ce4-231">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="17ce4-231">Messaging extensions</span></span>  | <span data-ttu-id="17ce4-232">Conectores</span><span class="sxs-lookup"><span data-stu-id="17ce4-232">Connectors</span></span> | <span data-ttu-id="17ce4-233">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="17ce4-233">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="17ce4-234">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-234">✔</span></span> | <span data-ttu-id="17ce4-235">✖</span><span class="sxs-lookup"><span data-stu-id="17ce4-235">✖</span></span> | <span data-ttu-id="17ce4-236">✖</span><span class="sxs-lookup"><span data-stu-id="17ce4-236">✖</span></span> |<span data-ttu-id="17ce4-237">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-237">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="17ce4-238">Propiedades de una tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="17ce4-238">Properties of a list card</span></span>

| <span data-ttu-id="17ce4-239">Propiedad</span><span class="sxs-lookup"><span data-stu-id="17ce4-239">Property</span></span> | <span data-ttu-id="17ce4-240">Tipo</span><span class="sxs-lookup"><span data-stu-id="17ce4-240">Type</span></span>  | <span data-ttu-id="17ce4-241">Description</span><span class="sxs-lookup"><span data-stu-id="17ce4-241">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="17ce4-242">title</span><span class="sxs-lookup"><span data-stu-id="17ce4-242">title</span></span> | <span data-ttu-id="17ce4-243">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="17ce4-243">Rich text</span></span> | <span data-ttu-id="17ce4-244">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="17ce4-244">Title of the card.</span></span> <span data-ttu-id="17ce4-245">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="17ce4-245">Maximum 2 lines.</span></span>|
| <span data-ttu-id="17ce4-246">elementos</span><span class="sxs-lookup"><span data-stu-id="17ce4-246">items</span></span> | <span data-ttu-id="17ce4-247">Matriz de elementos de lista</span><span class="sxs-lookup"><span data-stu-id="17ce4-247">Array of list items</span></span> ||
| <span data-ttu-id="17ce4-248">botones</span><span class="sxs-lookup"><span data-stu-id="17ce4-248">buttons</span></span> | <span data-ttu-id="17ce4-249">Matriz de objetos de acción</span><span class="sxs-lookup"><span data-stu-id="17ce4-249">Array of action objects</span></span> | <span data-ttu-id="17ce4-250">Conjunto de acciones aplicables a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="17ce4-250">Set of actions applicable to the current card.</span></span> <span data-ttu-id="17ce4-251">Máximo 6.</span><span class="sxs-lookup"><span data-stu-id="17ce4-251">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="17ce4-252">Ejemplo de una tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="17ce4-252">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="17ce4-253">Office 365 de conector</span><span class="sxs-lookup"><span data-stu-id="17ce4-253">Office 365 connector card</span></span>

<span data-ttu-id="17ce4-254">La Office 365 de conector se admite en Teams, no en Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="17ce4-254">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="17ce4-255">Esta tarjeta proporciona un diseño flexible con varias secciones, campos, imágenes y acciones.</span><span class="sxs-lookup"><span data-stu-id="17ce4-255">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="17ce4-256">Esta tarjeta encapsula una tarjeta de conector para que la puedan usar los bots.</span><span class="sxs-lookup"><span data-stu-id="17ce4-256">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="17ce4-257">Para obtener más información sobre las diferencias entre las tarjetas de conector y la tarjeta O365, vea Notas en [la Office 365 de conector](#notes-on-the-office-365-connector-card).</span><span class="sxs-lookup"><span data-stu-id="17ce4-257">For differences between connector cards and the O365 card, see [Notes on the Office 365 connector card](#notes-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="17ce4-258">Compatibilidad con tarjetas Office 365 conector</span><span class="sxs-lookup"><span data-stu-id="17ce4-258">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="17ce4-259">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="17ce4-259">Bots in Teams</span></span> | <span data-ttu-id="17ce4-260">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="17ce4-260">Messaging extensions</span></span>  | <span data-ttu-id="17ce4-261">Conectores</span><span class="sxs-lookup"><span data-stu-id="17ce4-261">Connectors</span></span> | <span data-ttu-id="17ce4-262">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="17ce4-262">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="17ce4-263">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-263">✔</span></span> | <span data-ttu-id="17ce4-264">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-264">✔</span></span> | <span data-ttu-id="17ce4-265">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-265">✔</span></span> | <span data-ttu-id="17ce4-266">✖</span><span class="sxs-lookup"><span data-stu-id="17ce4-266">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="17ce4-267">Propiedades de la tarjeta Office 365 conector</span><span class="sxs-lookup"><span data-stu-id="17ce4-267">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="17ce4-268">Propiedad</span><span class="sxs-lookup"><span data-stu-id="17ce4-268">Property</span></span> | <span data-ttu-id="17ce4-269">Tipo</span><span class="sxs-lookup"><span data-stu-id="17ce4-269">Type</span></span>  | <span data-ttu-id="17ce4-270">Description</span><span class="sxs-lookup"><span data-stu-id="17ce4-270">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="17ce4-271">title</span><span class="sxs-lookup"><span data-stu-id="17ce4-271">title</span></span> | <span data-ttu-id="17ce4-272">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="17ce4-272">Rich text</span></span> | <span data-ttu-id="17ce4-273">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="17ce4-273">Title of the card.</span></span> <span data-ttu-id="17ce4-274">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="17ce4-274">Maximum 2 lines.</span></span> |
| <span data-ttu-id="17ce4-275">summary</span><span class="sxs-lookup"><span data-stu-id="17ce4-275">summary</span></span> | <span data-ttu-id="17ce4-276">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="17ce4-276">Rich text</span></span> | <span data-ttu-id="17ce4-277">Resumen de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="17ce4-277">Summary of the card.</span></span> <span data-ttu-id="17ce4-278">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="17ce4-278">Maximum 2 lines.</span></span> |
| <span data-ttu-id="17ce4-279">text</span><span class="sxs-lookup"><span data-stu-id="17ce4-279">text</span></span> | <span data-ttu-id="17ce4-280">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="17ce4-280">Rich text</span></span> | <span data-ttu-id="17ce4-281">El texto aparece debajo del subtítulo.</span><span class="sxs-lookup"><span data-stu-id="17ce4-281">Text appears under the subtitle.</span></span> <span data-ttu-id="17ce4-282">Para ver las opciones de formato, vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="17ce4-282">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="17ce4-283">themeColor</span><span class="sxs-lookup"><span data-stu-id="17ce4-283">themeColor</span></span> | <span data-ttu-id="17ce4-284">Cadena HEX</span><span class="sxs-lookup"><span data-stu-id="17ce4-284">HEX string</span></span> | <span data-ttu-id="17ce4-285">Color que reemplaza el accentColor proporcionado desde el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="17ce4-285">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="17ce4-286">Notas en la tarjeta Office 365 conector</span><span class="sxs-lookup"><span data-stu-id="17ce4-286">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="17ce4-287">Office 365 tarjetas de conector funcionan correctamente en Microsoft Teams, incluidas [las acciones ActionCard](/outlook/actionable-messages/card-reference#actioncard-action).</span><span class="sxs-lookup"><span data-stu-id="17ce4-287">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="17ce4-288">Una diferencia importante entre el uso de tarjetas de conector desde un conector y el uso de tarjetas de conector en el bot es el control de las acciones de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="17ce4-288">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="17ce4-289">Para un conector, el extremo recibe la carga de la tarjeta a través de HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="17ce4-289">For a connector, the endpoint receives the card payload through HTTP POST.</span></span>
* <span data-ttu-id="17ce4-290">Para un bot, la acción desencadena una actividad que envía solo el identificador de acción `HttpPOST` y el cuerpo al `invoke` bot.</span><span class="sxs-lookup"><span data-stu-id="17ce4-290">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="17ce4-291">Cada tarjeta de conector puede mostrar un máximo de diez secciones y cada sección puede contener un máximo de cinco imágenes y cinco acciones.</span><span class="sxs-lookup"><span data-stu-id="17ce4-291">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="17ce4-292">Las secciones, imágenes o acciones adicionales de un mensaje no aparecen.</span><span class="sxs-lookup"><span data-stu-id="17ce4-292">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="17ce4-293">Todos los campos de texto admiten markdown y HTML.</span><span class="sxs-lookup"><span data-stu-id="17ce4-293">All text fields support markdown and HTML.</span></span> <span data-ttu-id="17ce4-294">Puede controlar qué secciones usan markdown o HTML estableciendo la `markdown` propiedad en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="17ce4-294">You can control which sections use markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="17ce4-295">De forma predeterminada, `markdown` se establece en `true` .</span><span class="sxs-lookup"><span data-stu-id="17ce4-295">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="17ce4-296">Si quiere usar HTML en su lugar, establezca `markdown` en `false` .</span><span class="sxs-lookup"><span data-stu-id="17ce4-296">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="17ce4-297">Si especifica la `themeColor` propiedad, invalida la `accentColor` propiedad en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="17ce4-297">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="17ce4-298">Para especificar el estilo de representación `activityImage` para , puede establecer lo `activityImageType` siguiente:</span><span class="sxs-lookup"><span data-stu-id="17ce4-298">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="17ce4-299">Valor</span><span class="sxs-lookup"><span data-stu-id="17ce4-299">Value</span></span> | <span data-ttu-id="17ce4-300">Descripción</span><span class="sxs-lookup"><span data-stu-id="17ce4-300">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="17ce4-301">Valor predeterminado; `activityImage` se recorta como un círculo.</span><span class="sxs-lookup"><span data-stu-id="17ce4-301">Default; `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="17ce4-302">`activityImage` se muestra como un rectángulo y conserva su relación de aspecto.</span><span class="sxs-lookup"><span data-stu-id="17ce4-302">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="17ce4-303">Para obtener todos los demás detalles acerca de las propiedades de la tarjeta de conector, vea [referencia de tarjeta de mensaje que puede actuar.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="17ce4-303">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="17ce4-304">Las únicas propiedades de tarjeta de conector que Microsoft Teams admite actualmente son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="17ce4-304">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="17ce4-305">`startGroup`siempre tratado como `true` en Teams</span><span class="sxs-lookup"><span data-stu-id="17ce4-305">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="17ce4-306">Ejemplo de una tarjeta Office 365 conector</span><span class="sxs-lookup"><span data-stu-id="17ce4-306">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="17ce4-307">Tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="17ce4-307">Receipt card</span></span>

<span data-ttu-id="17ce4-308">Teams admite tarjeta de recibo.</span><span class="sxs-lookup"><span data-stu-id="17ce4-308">Teams supports receipt card.</span></span> <span data-ttu-id="17ce4-309">Es una tarjeta que permite a un bot proporcionar un recibo al usuario.</span><span class="sxs-lookup"><span data-stu-id="17ce4-309">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="17ce4-310">Normalmente contiene la lista de elementos que se deben incluir en el recibo, como impuestos y la información total.</span><span class="sxs-lookup"><span data-stu-id="17ce4-310">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="17ce4-311">Compatibilidad con tarjetas de recibo</span><span class="sxs-lookup"><span data-stu-id="17ce4-311">Support for receipt cards</span></span>

| <span data-ttu-id="17ce4-312">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="17ce4-312">Bots in Teams</span></span> | <span data-ttu-id="17ce4-313">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="17ce4-313">Messaging extensions</span></span>  | <span data-ttu-id="17ce4-314">Conectores</span><span class="sxs-lookup"><span data-stu-id="17ce4-314">Connectors</span></span> | <span data-ttu-id="17ce4-315">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="17ce4-315">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="17ce4-316">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-316">✔</span></span> | <span data-ttu-id="17ce4-317">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-317">✔</span></span> | <span data-ttu-id="17ce4-318">✖</span><span class="sxs-lookup"><span data-stu-id="17ce4-318">✖</span></span> | <span data-ttu-id="17ce4-319">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-319">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="17ce4-320">Ejemplo de una tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="17ce4-320">Example of a receipt card</span></span>

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="17ce4-322">Información adicional sobre tarjetas de recibo</span><span class="sxs-lookup"><span data-stu-id="17ce4-322">Additional information on receipt cards</span></span>

<span data-ttu-id="17ce4-323">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="17ce4-323">Bot Framework reference:</span></span>

* [<span data-ttu-id="17ce4-324">Tarjeta de recibo Node.js</span><span class="sxs-lookup"><span data-stu-id="17ce4-324">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="17ce4-325">Tarjeta de recibo C #</span><span class="sxs-lookup"><span data-stu-id="17ce4-325">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="17ce4-326">Tarjeta de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="17ce4-326">Signin card</span></span>

<span data-ttu-id="17ce4-327">La tarjeta de inicio de sesión permite que un bot solicite a un usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="17ce4-327">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="17ce4-328">Se admite en Teams forma ligeramente diferente a la que se encuentra en Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="17ce4-328">It is supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="17ce4-329">La tarjeta de inicio de sesión en Teams es similar a la tarjeta de inicio de sesión en Bot Framework, excepto que la tarjeta de inicio de sesión en Teams solo admite dos acciones: `signin` y `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="17ce4-329">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="17ce4-330">La acción de inicio de sesión se puede usar desde cualquier tarjeta de Teams, no solo desde la tarjeta de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="17ce4-330">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="17ce4-331">Para obtener más información sobre la autenticación, [vea Microsoft Teams de autenticación para bots](~/bots/how-to/authentication/auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="17ce4-331">For more information on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="17ce4-332">Compatibilidad con tarjetas de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="17ce4-332">Support for signin cards</span></span>

| <span data-ttu-id="17ce4-333">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="17ce4-333">Bots in Teams</span></span> | <span data-ttu-id="17ce4-334">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="17ce4-334">Messaging extensions</span></span>  | <span data-ttu-id="17ce4-335">Conectores</span><span class="sxs-lookup"><span data-stu-id="17ce4-335">Connectors</span></span> | <span data-ttu-id="17ce4-336">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="17ce4-336">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="17ce4-337">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-337">✔</span></span> | <span data-ttu-id="17ce4-338">✖</span><span class="sxs-lookup"><span data-stu-id="17ce4-338">✖</span></span> | <span data-ttu-id="17ce4-339">✖</span><span class="sxs-lookup"><span data-stu-id="17ce4-339">✖</span></span> | <span data-ttu-id="17ce4-340">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-340">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="17ce4-341">Información adicional sobre tarjetas de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="17ce4-341">Additional information on signin cards</span></span>

<span data-ttu-id="17ce4-342">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="17ce4-342">Bot Framework reference:</span></span>

* [<span data-ttu-id="17ce4-343">Tarjeta de inicio de sesión Node.js</span><span class="sxs-lookup"><span data-stu-id="17ce4-343">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="17ce4-344">Tarjeta de inicio de sesión C #</span><span class="sxs-lookup"><span data-stu-id="17ce4-344">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="17ce4-345">Tarjeta miniatura</span><span class="sxs-lookup"><span data-stu-id="17ce4-345">Thumbnail card</span></span>

<span data-ttu-id="17ce4-346">Una tarjeta que normalmente contiene una sola imagen en miniatura, uno o varios botones y texto.</span><span class="sxs-lookup"><span data-stu-id="17ce4-346">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="17ce4-347">Compatibilidad con tarjetas en miniatura</span><span class="sxs-lookup"><span data-stu-id="17ce4-347">Support for thumbnail cards</span></span>

| <span data-ttu-id="17ce4-348">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="17ce4-348">Bots in Teams</span></span> | <span data-ttu-id="17ce4-349">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="17ce4-349">Messaging extensions</span></span>  | <span data-ttu-id="17ce4-350">Conectores</span><span class="sxs-lookup"><span data-stu-id="17ce4-350">Connectors</span></span> | <span data-ttu-id="17ce4-351">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="17ce4-351">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="17ce4-352">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-352">✔</span></span> | <span data-ttu-id="17ce4-353">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-353">✔</span></span> | <span data-ttu-id="17ce4-354">✖</span><span class="sxs-lookup"><span data-stu-id="17ce4-354">✖</span></span> | <span data-ttu-id="17ce4-355">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-355">✔</span></span> |

![Ejemplo de una tarjeta en miniatura](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="17ce4-357">Propiedades de una tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="17ce4-357">Properties of a thumbnail card</span></span>

| <span data-ttu-id="17ce4-358">Propiedad</span><span class="sxs-lookup"><span data-stu-id="17ce4-358">Property</span></span> | <span data-ttu-id="17ce4-359">Tipo</span><span class="sxs-lookup"><span data-stu-id="17ce4-359">Type</span></span>  | <span data-ttu-id="17ce4-360">Description</span><span class="sxs-lookup"><span data-stu-id="17ce4-360">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="17ce4-361">title</span><span class="sxs-lookup"><span data-stu-id="17ce4-361">title</span></span> | <span data-ttu-id="17ce4-362">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="17ce4-362">Rich text</span></span> | <span data-ttu-id="17ce4-363">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="17ce4-363">Title of the card.</span></span> <span data-ttu-id="17ce4-364">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="17ce4-364">Maximum 2 lines.</span></span>|
| <span data-ttu-id="17ce4-365">subtitle</span><span class="sxs-lookup"><span data-stu-id="17ce4-365">subtitle</span></span> | <span data-ttu-id="17ce4-366">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="17ce4-366">Rich text</span></span> | <span data-ttu-id="17ce4-367">Subtítulo de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="17ce4-367">Subtitle of the card.</span></span> <span data-ttu-id="17ce4-368">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="17ce4-368">Maximum 2 lines.</span></span>|
| <span data-ttu-id="17ce4-369">text</span><span class="sxs-lookup"><span data-stu-id="17ce4-369">text</span></span> | <span data-ttu-id="17ce4-370">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="17ce4-370">Rich text</span></span> | <span data-ttu-id="17ce4-371">El texto aparece debajo del subtítulo.</span><span class="sxs-lookup"><span data-stu-id="17ce4-371">Text appears under the subtitle.</span></span> <span data-ttu-id="17ce4-372">Para ver las opciones de formato, vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="17ce4-372">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="17ce4-373">imágenes</span><span class="sxs-lookup"><span data-stu-id="17ce4-373">images</span></span> | <span data-ttu-id="17ce4-374">Matriz de imágenes</span><span class="sxs-lookup"><span data-stu-id="17ce4-374">Array of images</span></span> | <span data-ttu-id="17ce4-375">Imagen que se muestra en la parte superior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="17ce4-375">Image displayed at the top of the card.</span></span> <span data-ttu-id="17ce4-376">Relación de aspecto 1:1 cuadrado.</span><span class="sxs-lookup"><span data-stu-id="17ce4-376">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="17ce4-377">botones</span><span class="sxs-lookup"><span data-stu-id="17ce4-377">buttons</span></span> | <span data-ttu-id="17ce4-378">Matriz de objetos de acción</span><span class="sxs-lookup"><span data-stu-id="17ce4-378">Array of action objects</span></span> | <span data-ttu-id="17ce4-379">Conjunto de acciones aplicables a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="17ce4-379">Set of actions applicable to the current card.</span></span> <span data-ttu-id="17ce4-380">Máximo 6.</span><span class="sxs-lookup"><span data-stu-id="17ce4-380">Maximum 6.</span></span> |
| <span data-ttu-id="17ce4-381">pulsación</span><span class="sxs-lookup"><span data-stu-id="17ce4-381">tap</span></span> | <span data-ttu-id="17ce4-382">Action (objeto)</span><span class="sxs-lookup"><span data-stu-id="17ce4-382">Action object</span></span> | <span data-ttu-id="17ce4-383">Se activa cuando el usuario pulsa en la propia tarjeta.</span><span class="sxs-lookup"><span data-stu-id="17ce4-383">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="17ce4-384">Ejemplo de una tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="17ce4-384">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="17ce4-385">Información adicional</span><span class="sxs-lookup"><span data-stu-id="17ce4-385">Additional information</span></span>

<span data-ttu-id="17ce4-386">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="17ce4-386">Bot Framework reference:</span></span>

* [<span data-ttu-id="17ce4-387">Tarjeta en miniatura Node.js</span><span class="sxs-lookup"><span data-stu-id="17ce4-387">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="17ce4-388">Tarjeta de miniatura C #</span><span class="sxs-lookup"><span data-stu-id="17ce4-388">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="17ce4-389">Colecciones de tarjetas</span><span class="sxs-lookup"><span data-stu-id="17ce4-389">Card collections</span></span>

<span data-ttu-id="17ce4-390">Teams admite colecciones de tarjetas.</span><span class="sxs-lookup"><span data-stu-id="17ce4-390">Teams supports Card collections.</span></span>

<span data-ttu-id="17ce4-391">Las colecciones de tarjetas `builder.AttachmentLayout.carousel` incluyen y `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="17ce4-391">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="17ce4-392">Estas colecciones contienen tarjetas adaptables, de héroe o en miniatura.</span><span class="sxs-lookup"><span data-stu-id="17ce4-392">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="17ce4-393">Colección Carousel</span><span class="sxs-lookup"><span data-stu-id="17ce4-393">Carousel collection</span></span>

<span data-ttu-id="17ce4-394">El [diseño del carrusel](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) muestra un carrusel de tarjetas, opcionalmente con botones de acción asociados.</span><span class="sxs-lookup"><span data-stu-id="17ce4-394">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="17ce4-395">Compatibilidad con colecciones de carrusel</span><span class="sxs-lookup"><span data-stu-id="17ce4-395">Support for carousel collections</span></span>

| <span data-ttu-id="17ce4-396">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="17ce4-396">Bots in Teams</span></span> | <span data-ttu-id="17ce4-397">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="17ce4-397">Messaging extensions</span></span>  | <span data-ttu-id="17ce4-398">Conectores</span><span class="sxs-lookup"><span data-stu-id="17ce4-398">Connectors</span></span> | <span data-ttu-id="17ce4-399">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="17ce4-399">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="17ce4-400">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-400">✔</span></span> | <span data-ttu-id="17ce4-401">✖</span><span class="sxs-lookup"><span data-stu-id="17ce4-401">✖</span></span> | <span data-ttu-id="17ce4-402">✖</span><span class="sxs-lookup"><span data-stu-id="17ce4-402">✖</span></span> | <span data-ttu-id="17ce4-403">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-403">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="17ce4-404">Un carrusel puede mostrar un máximo de diez tarjetas por mensaje.</span><span class="sxs-lookup"><span data-stu-id="17ce4-404">A carousel can display a maximum of ten cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="17ce4-405">Propiedades de una tarjeta de carrusel</span><span class="sxs-lookup"><span data-stu-id="17ce4-405">Properties of a carousel card</span></span>

<span data-ttu-id="17ce4-406">Las propiedades de una tarjeta de carrusel son las mismas que las de las tarjetas de miniatura y de héroe.</span><span class="sxs-lookup"><span data-stu-id="17ce4-406">Properties of a carousel card are same as those of the hero and thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="17ce4-407">Ejemplo de una colección de carrusel</span><span class="sxs-lookup"><span data-stu-id="17ce4-407">Example of a carousel collection</span></span>

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="17ce4-409">Sintaxis para colecciones de carrusel</span><span class="sxs-lookup"><span data-stu-id="17ce4-409">Syntax for carousel collections</span></span>

<span data-ttu-id="17ce4-410">`builder.AttachmentLayoutTypes.Carousel` es la sintaxis de las colecciones de carrusel.</span><span class="sxs-lookup"><span data-stu-id="17ce4-410">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

## <a name="list-collection"></a><span data-ttu-id="17ce4-411">Colección List</span><span class="sxs-lookup"><span data-stu-id="17ce4-411">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="17ce4-412">Compatibilidad con colecciones de listas</span><span class="sxs-lookup"><span data-stu-id="17ce4-412">Support for list collections</span></span>

<span data-ttu-id="17ce4-413">El diseño de lista muestra una lista verticalmente apilada de tarjetas, opcionalmente con botones de acción asociados.</span><span class="sxs-lookup"><span data-stu-id="17ce4-413">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="17ce4-414">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="17ce4-414">Bots in Teams</span></span> | <span data-ttu-id="17ce4-415">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="17ce4-415">Messaging extensions</span></span>  | <span data-ttu-id="17ce4-416">Conectores</span><span class="sxs-lookup"><span data-stu-id="17ce4-416">Connectors</span></span> | <span data-ttu-id="17ce4-417">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="17ce4-417">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="17ce4-418">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-418">✔</span></span> | <span data-ttu-id="17ce4-419">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-419">✔</span></span> | <span data-ttu-id="17ce4-420">✖</span><span class="sxs-lookup"><span data-stu-id="17ce4-420">✖</span></span> | <span data-ttu-id="17ce4-421">✔</span><span class="sxs-lookup"><span data-stu-id="17ce4-421">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="17ce4-422">Ejemplo de una colección de listas</span><span class="sxs-lookup"><span data-stu-id="17ce4-422">Example of a list collection</span></span>

![Ejemplo de una lista de tarjetas](~/assets/images/cards/list.png)

<span data-ttu-id="17ce4-424">Las propiedades son las mismas que para la tarjeta de miniatura o de héroe.</span><span class="sxs-lookup"><span data-stu-id="17ce4-424">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="17ce4-425">Una lista puede mostrar un máximo de diez tarjetas por mensaje.</span><span class="sxs-lookup"><span data-stu-id="17ce4-425">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="17ce4-426">Algunas combinaciones de tarjetas de lista aún no son compatibles con iOS y Android.</span><span class="sxs-lookup"><span data-stu-id="17ce4-426">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="17ce4-427">Sintaxis para colecciones de listas</span><span class="sxs-lookup"><span data-stu-id="17ce4-427">Syntax for list collections</span></span>

<span data-ttu-id="17ce4-428">`builder.AttachmentLayout.list` es la sintaxis de las colecciones de listas.</span><span class="sxs-lookup"><span data-stu-id="17ce4-428">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="17ce4-429">No se admiten tarjetas en Teams</span><span class="sxs-lookup"><span data-stu-id="17ce4-429">Cards not supported in Teams</span></span>

<span data-ttu-id="17ce4-430">Bot Framework implementa las siguientes tarjetas, pero no son compatibles con Teams:</span><span class="sxs-lookup"><span data-stu-id="17ce4-430">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="17ce4-431">Tarjetas de animación</span><span class="sxs-lookup"><span data-stu-id="17ce4-431">Animation cards</span></span>
* <span data-ttu-id="17ce4-432">Tarjetas de audio</span><span class="sxs-lookup"><span data-stu-id="17ce4-432">Audio cards</span></span>
* <span data-ttu-id="17ce4-433">Tarjetas de vídeo</span><span class="sxs-lookup"><span data-stu-id="17ce4-433">Video cards</span></span>

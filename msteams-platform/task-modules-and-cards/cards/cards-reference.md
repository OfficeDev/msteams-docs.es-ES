---
title: Referencia de tarjetas
description: Describe todas las tarjetas y acciones de tarjeta disponibles para bots en Teams
localization_priority: Normal
keywords: referencia de tarjetas bots
ms.topic: reference
ms.openlocfilehash: 741980ea79dd23659dd2b8a240d767b8292ca251
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994388"
---
# <a name="cards-reference"></a><span data-ttu-id="a580d-104">Referencia de tarjetas</span><span class="sxs-lookup"><span data-stu-id="a580d-104">Cards reference</span></span>

<span data-ttu-id="a580d-105">Las tarjetas enumeradas en este documento se admiten en bots para Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a580d-105">The cards listed in this document are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="a580d-106">Se basan en tarjetas definidas por Bot Framework (BF), pero Teams no admite todas las tarjetas de Bot Framework y, en su lugar, se han agregado algunas Teams tarjetas.</span><span class="sxs-lookup"><span data-stu-id="a580d-106">They are based on cards defined by the Bot Framework (BF), but Teams does not support all Bot Framework cards and instead some Teams cards have been added.</span></span> <span data-ttu-id="a580d-107">Las diferencias se llaman en las referencias de este documento.</span><span class="sxs-lookup"><span data-stu-id="a580d-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="a580d-108">Ejemplos de tarjetas</span><span class="sxs-lookup"><span data-stu-id="a580d-108">Card examples</span></span>

<span data-ttu-id="a580d-109">Encontrará información adicional sobre cómo usar tarjetas en la documentación del SDK de Bot Builder v3.</span><span class="sxs-lookup"><span data-stu-id="a580d-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="a580d-110">Los ejemplos de código también están disponibles en el repositorio microsoft/BotBuilder-Samples en GitHub.</span><span class="sxs-lookup"><span data-stu-id="a580d-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="a580d-111">.NET</span><span class="sxs-lookup"><span data-stu-id="a580d-111">.NET</span></span>
  * <span data-ttu-id="a580d-112">[Agregar tarjetas como datos adjuntos a los mensajes](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="a580d-112">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="a580d-113">[Código de ejemplo de tarjetas Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="a580d-113">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span></span>

* <span data-ttu-id="a580d-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="a580d-114">Node.js</span></span>
  * <span data-ttu-id="a580d-115">[Agregar tarjetas como datos adjuntos a los mensajes](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="a580d-115">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="a580d-116">[Código de ejemplo de tarjetas Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="a580d-116">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span></span>

## <a name="types-of-cards"></a><span data-ttu-id="a580d-117">Tipos de tarjetas</span><span class="sxs-lookup"><span data-stu-id="a580d-117">Types of cards</span></span>

<span data-ttu-id="a580d-118">En esta tabla se muestran los tipos de tarjetas disponibles:</span><span class="sxs-lookup"><span data-stu-id="a580d-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="a580d-119">Tipo de tarjeta</span><span class="sxs-lookup"><span data-stu-id="a580d-119">Card type</span></span> | <span data-ttu-id="a580d-120">Descripción</span><span class="sxs-lookup"><span data-stu-id="a580d-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="a580d-121">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="a580d-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="a580d-122">Esta tarjeta es una tarjeta altamente personalizable que puede contener cualquier combinación de texto, voz, imágenes, botones y campos de entrada.</span><span class="sxs-lookup"><span data-stu-id="a580d-122">This card is highly customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="a580d-123">Tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="a580d-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="a580d-124">Esta tarjeta normalmente contiene una sola imagen grande, uno o varios botones y una pequeña cantidad de texto.</span><span class="sxs-lookup"><span data-stu-id="a580d-124">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="a580d-125">Tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="a580d-125">List card</span></span>](#list-card) | <span data-ttu-id="a580d-126">Esta tarjeta es una lista de desplazamiento de elementos.</span><span class="sxs-lookup"><span data-stu-id="a580d-126">This card is a scrolling list of items.</span></span> |
| [<span data-ttu-id="a580d-127">Office 365 de conector</span><span class="sxs-lookup"><span data-stu-id="a580d-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="a580d-128">Esta tarjeta tiene un diseño flexible con varias secciones, campos, imágenes y acciones.</span><span class="sxs-lookup"><span data-stu-id="a580d-128">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="a580d-129">Tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="a580d-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="a580d-130">Esta tarjeta proporciona un recibo al usuario.</span><span class="sxs-lookup"><span data-stu-id="a580d-130">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="a580d-131">Tarjeta de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="a580d-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="a580d-132">Esta tarjeta permite que un bot solicite que un usuario inicia sesión.</span><span class="sxs-lookup"><span data-stu-id="a580d-132">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="a580d-133">Tarjeta miniatura</span><span class="sxs-lookup"><span data-stu-id="a580d-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="a580d-134">Esta tarjeta normalmente contiene una sola imagen en miniatura, texto corto y uno o más botones.</span><span class="sxs-lookup"><span data-stu-id="a580d-134">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="a580d-135">Colecciones de tarjetas</span><span class="sxs-lookup"><span data-stu-id="a580d-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="a580d-136">Estas tarjetas se usan para devolver varios elementos en una sola respuesta.</span><span class="sxs-lookup"><span data-stu-id="a580d-136">This cards is used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="a580d-137">Propiedades comunes para todas las tarjetas</span><span class="sxs-lookup"><span data-stu-id="a580d-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="a580d-138">Imágenes de tarjetas en línea</span><span class="sxs-lookup"><span data-stu-id="a580d-138">Inline card images</span></span>

<span data-ttu-id="a580d-139">La tarjeta puede contener una imagen en línea al incluir un vínculo a la imagen disponible públicamente.</span><span class="sxs-lookup"><span data-stu-id="a580d-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="a580d-140">Por motivos de rendimiento, se recomienda hospedar la imagen en una red pública de entrega de contenido (CDN).</span><span class="sxs-lookup"><span data-stu-id="a580d-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="a580d-141">Las imágenes se escalan hacia arriba o hacia abajo en tamaño mientras se mantiene la relación de aspecto para cubrir el área de la imagen.</span><span class="sxs-lookup"><span data-stu-id="a580d-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area.</span></span> <span data-ttu-id="a580d-142">A continuación, las imágenes se recortan desde el centro para lograr la relación de aspecto adecuada para la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="a580d-142">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="a580d-143">Las imágenes deben tener como máximo 1024×1024, en formato PNG, JPEG o GIF, y no admiten GIF animados.</span><span class="sxs-lookup"><span data-stu-id="a580d-143">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and do not support animated GIF.</span></span>

| <span data-ttu-id="a580d-144">Propiedad</span><span class="sxs-lookup"><span data-stu-id="a580d-144">Property</span></span> | <span data-ttu-id="a580d-145">Tipo</span><span class="sxs-lookup"><span data-stu-id="a580d-145">Type</span></span>  | <span data-ttu-id="a580d-146">Descripción</span><span class="sxs-lookup"><span data-stu-id="a580d-146">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a580d-147">url</span><span class="sxs-lookup"><span data-stu-id="a580d-147">url</span></span> | <span data-ttu-id="a580d-148">URL</span><span class="sxs-lookup"><span data-stu-id="a580d-148">URL</span></span> | <span data-ttu-id="a580d-149">DIRECCIÓN URL HTTPS a la imagen.</span><span class="sxs-lookup"><span data-stu-id="a580d-149">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="a580d-150">alt</span><span class="sxs-lookup"><span data-stu-id="a580d-150">alt</span></span> | <span data-ttu-id="a580d-151">String</span><span class="sxs-lookup"><span data-stu-id="a580d-151">String</span></span> | <span data-ttu-id="a580d-152">Descripción accesible de la imagen.</span><span class="sxs-lookup"><span data-stu-id="a580d-152">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="a580d-153">Si una tarjeta incluye una dirección URL de imagen que pasa por un redireccionamiento antes de la imagen final, no se admite el redireccionamiento en la dirección URL de la imagen.</span><span class="sxs-lookup"><span data-stu-id="a580d-153">If a card includes an image URL that goes through a redirect before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="a580d-154">Esto ocurre para las imágenes compartidas en la nube pública.</span><span class="sxs-lookup"><span data-stu-id="a580d-154">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="a580d-155">Botones</span><span class="sxs-lookup"><span data-stu-id="a580d-155">Buttons</span></span>

<span data-ttu-id="a580d-156">Los botones se muestran apilados en la parte inferior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="a580d-156">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="a580d-157">El texto del botón siempre está en una sola línea y se trunca si el texto supera el ancho del botón.</span><span class="sxs-lookup"><span data-stu-id="a580d-157">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="a580d-158">No se muestran los botones adicionales que supere el número máximo admitido por la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="a580d-158">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="a580d-159">Para obtener más información, vea [acciones de tarjeta](~/task-modules-and-cards/cards/cards-actions.md).</span><span class="sxs-lookup"><span data-stu-id="a580d-159">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="a580d-160">Formato de tarjeta</span><span class="sxs-lookup"><span data-stu-id="a580d-160">Card formatting</span></span>

<span data-ttu-id="a580d-161">Para obtener más información sobre el formato de texto en tarjetas, vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="a580d-161">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="a580d-162">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="a580d-162">Adaptive card</span></span>

<span data-ttu-id="a580d-163">Una tarjeta adaptable es una tarjeta personalizable que puede contener cualquier combinación de texto, voz, imágenes, botones y campos de entrada.</span><span class="sxs-lookup"><span data-stu-id="a580d-163">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="a580d-164">Para obtener más información, [vea adaptive cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="a580d-164">For more information, see [adaptive cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="a580d-165">Compatibilidad con tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="a580d-165">Support for adaptive cards</span></span>

| <span data-ttu-id="a580d-166">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="a580d-166">Bots in Teams</span></span> | <span data-ttu-id="a580d-167">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="a580d-167">Messaging extensions</span></span>  | <span data-ttu-id="a580d-168">Conectores</span><span class="sxs-lookup"><span data-stu-id="a580d-168">Connectors</span></span> | <span data-ttu-id="a580d-169">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a580d-169">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a580d-170">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-170">✔</span></span> | <span data-ttu-id="a580d-171">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-171">✔</span></span> | <span data-ttu-id="a580d-172">✖</span><span class="sxs-lookup"><span data-stu-id="a580d-172">✖</span></span> | <span data-ttu-id="a580d-173">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-173">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="a580d-174">Teams plataforma admite v1.2 o versiones anteriores de características de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="a580d-174">Teams platform supports v1.2 or earlier of adaptive card features.</span></span>
> * <span data-ttu-id="a580d-175">El estilo de acción positiva o destructiva no se admite en tarjetas adaptables en la Teams web.</span><span class="sxs-lookup"><span data-stu-id="a580d-175">Positive or destructive action styling is not supported in Adaptive Cards on the Teams platform.</span></span>
> * <span data-ttu-id="a580d-176">Actualmente, los elementos multimedia no se admiten en tarjetas adaptables en la Teams web.</span><span class="sxs-lookup"><span data-stu-id="a580d-176">Media elements are currently not supported in Adaptive Cards on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="a580d-177">Ejemplo de una tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="a580d-177">Example of an adaptive card</span></span>

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="a580d-179">Información adicional sobre tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="a580d-179">Additional information on adaptive cards</span></span>

<span data-ttu-id="a580d-180">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="a580d-180">Bot Framework reference:</span></span>

* [<span data-ttu-id="a580d-181">Tarjetas adaptables Node.js</span><span class="sxs-lookup"><span data-stu-id="a580d-181">Adaptive cards Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="a580d-182">Tarjeta adaptable C #</span><span class="sxs-lookup"><span data-stu-id="a580d-182">Adaptive card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

## <a name="hero-card"></a><span data-ttu-id="a580d-183">Tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="a580d-183">Hero card</span></span>

<span data-ttu-id="a580d-184">Una tarjeta que normalmente contiene una sola imagen grande, uno o varios botones y texto.</span><span class="sxs-lookup"><span data-stu-id="a580d-184">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="a580d-185">Compatibilidad con tarjetas de héroe</span><span class="sxs-lookup"><span data-stu-id="a580d-185">Support for hero cards</span></span>

| <span data-ttu-id="a580d-186">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="a580d-186">Bots in Teams</span></span> | <span data-ttu-id="a580d-187">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="a580d-187">Messaging extensions</span></span>  | <span data-ttu-id="a580d-188">Conectores</span><span class="sxs-lookup"><span data-stu-id="a580d-188">Connectors</span></span> | <span data-ttu-id="a580d-189">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a580d-189">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a580d-190">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-190">✔</span></span> | <span data-ttu-id="a580d-191">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-191">✔</span></span> | <span data-ttu-id="a580d-192">✖</span><span class="sxs-lookup"><span data-stu-id="a580d-192">✖</span></span> | <span data-ttu-id="a580d-193">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-193">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="a580d-194">Propiedades de una tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="a580d-194">Properties of a hero card</span></span>

| <span data-ttu-id="a580d-195">Propiedad</span><span class="sxs-lookup"><span data-stu-id="a580d-195">Property</span></span> | <span data-ttu-id="a580d-196">Tipo</span><span class="sxs-lookup"><span data-stu-id="a580d-196">Type</span></span>  | <span data-ttu-id="a580d-197">Description</span><span class="sxs-lookup"><span data-stu-id="a580d-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a580d-198">title</span><span class="sxs-lookup"><span data-stu-id="a580d-198">title</span></span> | <span data-ttu-id="a580d-199">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="a580d-199">Rich text</span></span> | <span data-ttu-id="a580d-200">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="a580d-200">Title of the card.</span></span> <span data-ttu-id="a580d-201">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="a580d-201">Maximum 2 lines.</span></span> |
| <span data-ttu-id="a580d-202">subtitle</span><span class="sxs-lookup"><span data-stu-id="a580d-202">subtitle</span></span> | <span data-ttu-id="a580d-203">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="a580d-203">Rich text</span></span> | <span data-ttu-id="a580d-204">Subtítulo de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="a580d-204">Subtitle of the card.</span></span> <span data-ttu-id="a580d-205">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="a580d-205">Maximum 2 lines.</span></span>|
| <span data-ttu-id="a580d-206">text</span><span class="sxs-lookup"><span data-stu-id="a580d-206">text</span></span> | <span data-ttu-id="a580d-207">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="a580d-207">Rich text</span></span> | <span data-ttu-id="a580d-208">El texto aparece debajo del subtítulo.</span><span class="sxs-lookup"><span data-stu-id="a580d-208">Text appears under the subtitle.</span></span> <span data-ttu-id="a580d-209">Para ver las opciones de formato, vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="a580d-209">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="a580d-210">imágenes</span><span class="sxs-lookup"><span data-stu-id="a580d-210">images</span></span> | <span data-ttu-id="a580d-211">Matriz de imágenes</span><span class="sxs-lookup"><span data-stu-id="a580d-211">Array of images</span></span> | <span data-ttu-id="a580d-212">Imagen que se muestra en la parte superior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="a580d-212">Image displayed at the top of the card.</span></span> <span data-ttu-id="a580d-213">Relación de aspecto 16:9.</span><span class="sxs-lookup"><span data-stu-id="a580d-213">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="a580d-214">botones</span><span class="sxs-lookup"><span data-stu-id="a580d-214">buttons</span></span> | <span data-ttu-id="a580d-215">Matriz de objetos de acción</span><span class="sxs-lookup"><span data-stu-id="a580d-215">Array of action objects</span></span> | <span data-ttu-id="a580d-216">Conjunto de acciones aplicables a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="a580d-216">Set of actions applicable to the current card.</span></span> <span data-ttu-id="a580d-217">Máximo 6.</span><span class="sxs-lookup"><span data-stu-id="a580d-217">Maximum 6.</span></span> |
| <span data-ttu-id="a580d-218">pulsación</span><span class="sxs-lookup"><span data-stu-id="a580d-218">tap</span></span> | <span data-ttu-id="a580d-219">Action (objeto)</span><span class="sxs-lookup"><span data-stu-id="a580d-219">Action object</span></span> | <span data-ttu-id="a580d-220">Se activa cuando el usuario pulsa en la propia tarjeta.</span><span class="sxs-lookup"><span data-stu-id="a580d-220">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="a580d-221">Ejemplo de una tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="a580d-221">Example of a hero card</span></span>

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="a580d-223">Información adicional sobre tarjetas de héroe</span><span class="sxs-lookup"><span data-stu-id="a580d-223">Additional information on hero cards</span></span>

<span data-ttu-id="a580d-224">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="a580d-224">Bot Framework reference:</span></span>

* [<span data-ttu-id="a580d-225">Tarjeta de Node.js</span><span class="sxs-lookup"><span data-stu-id="a580d-225">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="a580d-226">Tarjeta de héroe C #</span><span class="sxs-lookup"><span data-stu-id="a580d-226">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="a580d-227">Tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="a580d-227">List card</span></span>

<span data-ttu-id="a580d-228">La tarjeta de lista se ha agregado Teams para proporcionar funciones más allá de lo que la colección de listas puede proporcionar.</span><span class="sxs-lookup"><span data-stu-id="a580d-228">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="a580d-229">La tarjeta de lista proporciona una lista de desplazamiento de elementos.</span><span class="sxs-lookup"><span data-stu-id="a580d-229">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="a580d-230">Compatibilidad con tarjetas de lista</span><span class="sxs-lookup"><span data-stu-id="a580d-230">Support for list cards</span></span>

| <span data-ttu-id="a580d-231">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="a580d-231">Bots in Teams</span></span> | <span data-ttu-id="a580d-232">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="a580d-232">Messaging extensions</span></span>  | <span data-ttu-id="a580d-233">Conectores</span><span class="sxs-lookup"><span data-stu-id="a580d-233">Connectors</span></span> | <span data-ttu-id="a580d-234">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a580d-234">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a580d-235">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-235">✔</span></span> | <span data-ttu-id="a580d-236">✖</span><span class="sxs-lookup"><span data-stu-id="a580d-236">✖</span></span> | <span data-ttu-id="a580d-237">✖</span><span class="sxs-lookup"><span data-stu-id="a580d-237">✖</span></span> |<span data-ttu-id="a580d-238">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-238">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="a580d-239">Propiedades de una tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="a580d-239">Properties of a list card</span></span>

| <span data-ttu-id="a580d-240">Propiedad</span><span class="sxs-lookup"><span data-stu-id="a580d-240">Property</span></span> | <span data-ttu-id="a580d-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="a580d-241">Type</span></span>  | <span data-ttu-id="a580d-242">Description</span><span class="sxs-lookup"><span data-stu-id="a580d-242">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a580d-243">title</span><span class="sxs-lookup"><span data-stu-id="a580d-243">title</span></span> | <span data-ttu-id="a580d-244">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="a580d-244">Rich text</span></span> | <span data-ttu-id="a580d-245">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="a580d-245">Title of the card.</span></span> <span data-ttu-id="a580d-246">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="a580d-246">Maximum 2 lines.</span></span>|
| <span data-ttu-id="a580d-247">elementos</span><span class="sxs-lookup"><span data-stu-id="a580d-247">items</span></span> | <span data-ttu-id="a580d-248">Matriz de elementos de lista</span><span class="sxs-lookup"><span data-stu-id="a580d-248">Array of list items</span></span> ||
| <span data-ttu-id="a580d-249">botones</span><span class="sxs-lookup"><span data-stu-id="a580d-249">buttons</span></span> | <span data-ttu-id="a580d-250">Matriz de objetos de acción</span><span class="sxs-lookup"><span data-stu-id="a580d-250">Array of action objects</span></span> | <span data-ttu-id="a580d-251">Conjunto de acciones aplicables a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="a580d-251">Set of actions applicable to the current card.</span></span> <span data-ttu-id="a580d-252">Máximo 6.</span><span class="sxs-lookup"><span data-stu-id="a580d-252">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="a580d-253">Ejemplo de una tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="a580d-253">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="a580d-254">Office 365 de conector</span><span class="sxs-lookup"><span data-stu-id="a580d-254">Office 365 connector card</span></span>

<span data-ttu-id="a580d-255">La Office 365 de conector se admite en Teams, no en Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="a580d-255">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="a580d-256">Esta tarjeta proporciona un diseño flexible con varias secciones, campos, imágenes y acciones.</span><span class="sxs-lookup"><span data-stu-id="a580d-256">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="a580d-257">Esta tarjeta encapsula una tarjeta de conector para que la puedan usar los bots.</span><span class="sxs-lookup"><span data-stu-id="a580d-257">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="a580d-258">Para obtener más información sobre las diferencias entre las tarjetas de conector y la tarjeta O365, vea Notas en [la Office 365 de conector](#notes-on-the-office-365-connector-card).</span><span class="sxs-lookup"><span data-stu-id="a580d-258">For differences between connector cards and the O365 card, see [Notes on the Office 365 connector card](#notes-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="a580d-259">Compatibilidad con tarjetas Office 365 conector</span><span class="sxs-lookup"><span data-stu-id="a580d-259">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="a580d-260">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="a580d-260">Bots in Teams</span></span> | <span data-ttu-id="a580d-261">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="a580d-261">Messaging extensions</span></span>  | <span data-ttu-id="a580d-262">Conectores</span><span class="sxs-lookup"><span data-stu-id="a580d-262">Connectors</span></span> | <span data-ttu-id="a580d-263">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a580d-263">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a580d-264">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-264">✔</span></span> | <span data-ttu-id="a580d-265">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-265">✔</span></span> | <span data-ttu-id="a580d-266">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-266">✔</span></span> | <span data-ttu-id="a580d-267">✖</span><span class="sxs-lookup"><span data-stu-id="a580d-267">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="a580d-268">Propiedades de la tarjeta Office 365 conector</span><span class="sxs-lookup"><span data-stu-id="a580d-268">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="a580d-269">Propiedad</span><span class="sxs-lookup"><span data-stu-id="a580d-269">Property</span></span> | <span data-ttu-id="a580d-270">Tipo</span><span class="sxs-lookup"><span data-stu-id="a580d-270">Type</span></span>  | <span data-ttu-id="a580d-271">Description</span><span class="sxs-lookup"><span data-stu-id="a580d-271">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a580d-272">title</span><span class="sxs-lookup"><span data-stu-id="a580d-272">title</span></span> | <span data-ttu-id="a580d-273">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="a580d-273">Rich text</span></span> | <span data-ttu-id="a580d-274">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="a580d-274">Title of the card.</span></span> <span data-ttu-id="a580d-275">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="a580d-275">Maximum 2 lines.</span></span> |
| <span data-ttu-id="a580d-276">summary</span><span class="sxs-lookup"><span data-stu-id="a580d-276">summary</span></span> | <span data-ttu-id="a580d-277">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="a580d-277">Rich text</span></span> | <span data-ttu-id="a580d-278">Resumen de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="a580d-278">Summary of the card.</span></span> <span data-ttu-id="a580d-279">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="a580d-279">Maximum 2 lines.</span></span> |
| <span data-ttu-id="a580d-280">text</span><span class="sxs-lookup"><span data-stu-id="a580d-280">text</span></span> | <span data-ttu-id="a580d-281">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="a580d-281">Rich text</span></span> | <span data-ttu-id="a580d-282">El texto aparece debajo del subtítulo.</span><span class="sxs-lookup"><span data-stu-id="a580d-282">Text appears under the subtitle.</span></span> <span data-ttu-id="a580d-283">Para ver las opciones de formato, vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="a580d-283">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="a580d-284">themeColor</span><span class="sxs-lookup"><span data-stu-id="a580d-284">themeColor</span></span> | <span data-ttu-id="a580d-285">Cadena HEX</span><span class="sxs-lookup"><span data-stu-id="a580d-285">HEX string</span></span> | <span data-ttu-id="a580d-286">Color que reemplaza el accentColor proporcionado desde el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a580d-286">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="a580d-287">Notas en la tarjeta Office 365 conector</span><span class="sxs-lookup"><span data-stu-id="a580d-287">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="a580d-288">Office 365 tarjetas de conector funcionan correctamente en Microsoft Teams, incluidas [las acciones ActionCard](/outlook/actionable-messages/card-reference#actioncard-action).</span><span class="sxs-lookup"><span data-stu-id="a580d-288">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="a580d-289">Una diferencia importante entre el uso de tarjetas de conector desde un conector y el uso de tarjetas de conector en el bot es el control de las acciones de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="a580d-289">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="a580d-290">Para un conector, el extremo recibe la carga de la tarjeta a través de HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="a580d-290">For a connector, the endpoint receives the card payload through HTTP POST.</span></span>
* <span data-ttu-id="a580d-291">Para un bot, la acción desencadena una actividad que envía solo el identificador de acción `HttpPOST` y el cuerpo al `invoke` bot.</span><span class="sxs-lookup"><span data-stu-id="a580d-291">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="a580d-292">Cada tarjeta de conector puede mostrar un máximo de diez secciones y cada sección puede contener un máximo de cinco imágenes y cinco acciones.</span><span class="sxs-lookup"><span data-stu-id="a580d-292">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="a580d-293">Las secciones, imágenes o acciones adicionales de un mensaje no aparecen.</span><span class="sxs-lookup"><span data-stu-id="a580d-293">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="a580d-294">Todos los campos de texto admiten markdown y HTML.</span><span class="sxs-lookup"><span data-stu-id="a580d-294">All text fields support markdown and HTML.</span></span> <span data-ttu-id="a580d-295">Puede controlar qué secciones usan markdown o HTML estableciendo la `markdown` propiedad en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="a580d-295">You can control which sections use markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="a580d-296">De forma predeterminada, `markdown` se establece en `true` .</span><span class="sxs-lookup"><span data-stu-id="a580d-296">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="a580d-297">Si quiere usar HTML en su lugar, establezca `markdown` en `false` .</span><span class="sxs-lookup"><span data-stu-id="a580d-297">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="a580d-298">Si especifica la `themeColor` propiedad, invalida la `accentColor` propiedad en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a580d-298">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="a580d-299">Para especificar el estilo de representación `activityImage` para , puede establecer lo `activityImageType` siguiente:</span><span class="sxs-lookup"><span data-stu-id="a580d-299">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="a580d-300">Valor</span><span class="sxs-lookup"><span data-stu-id="a580d-300">Value</span></span> | <span data-ttu-id="a580d-301">Descripción</span><span class="sxs-lookup"><span data-stu-id="a580d-301">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="a580d-302">Valor predeterminado; `activityImage` se recorta como un círculo.</span><span class="sxs-lookup"><span data-stu-id="a580d-302">Default; `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="a580d-303">`activityImage` se muestra como un rectángulo y conserva su relación de aspecto.</span><span class="sxs-lookup"><span data-stu-id="a580d-303">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="a580d-304">Para obtener todos los demás detalles acerca de las propiedades de la tarjeta de conector, vea [referencia de tarjeta de mensaje que puede actuar.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="a580d-304">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="a580d-305">Las únicas propiedades de tarjeta de conector que Microsoft Teams admite actualmente son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="a580d-305">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="a580d-306">`startGroup`siempre tratado como `true` en Teams</span><span class="sxs-lookup"><span data-stu-id="a580d-306">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="a580d-307">Ejemplo de una tarjeta Office 365 conector</span><span class="sxs-lookup"><span data-stu-id="a580d-307">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="a580d-308">Tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="a580d-308">Receipt card</span></span>

<span data-ttu-id="a580d-309">Teams admite tarjeta de recibo.</span><span class="sxs-lookup"><span data-stu-id="a580d-309">Teams supports receipt card.</span></span> <span data-ttu-id="a580d-310">Es una tarjeta que permite a un bot proporcionar un recibo al usuario.</span><span class="sxs-lookup"><span data-stu-id="a580d-310">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="a580d-311">Normalmente contiene la lista de elementos que se deben incluir en el recibo, como impuestos y la información total.</span><span class="sxs-lookup"><span data-stu-id="a580d-311">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="a580d-312">Compatibilidad con tarjetas de recibo</span><span class="sxs-lookup"><span data-stu-id="a580d-312">Support for receipt cards</span></span>

| <span data-ttu-id="a580d-313">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="a580d-313">Bots in Teams</span></span> | <span data-ttu-id="a580d-314">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="a580d-314">Messaging extensions</span></span>  | <span data-ttu-id="a580d-315">Conectores</span><span class="sxs-lookup"><span data-stu-id="a580d-315">Connectors</span></span> | <span data-ttu-id="a580d-316">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a580d-316">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a580d-317">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-317">✔</span></span> | <span data-ttu-id="a580d-318">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-318">✔</span></span> | <span data-ttu-id="a580d-319">✖</span><span class="sxs-lookup"><span data-stu-id="a580d-319">✖</span></span> | <span data-ttu-id="a580d-320">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-320">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="a580d-321">Ejemplo de una tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="a580d-321">Example of a receipt card</span></span>

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="a580d-323">Información adicional sobre tarjetas de recibo</span><span class="sxs-lookup"><span data-stu-id="a580d-323">Additional information on receipt cards</span></span>

<span data-ttu-id="a580d-324">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="a580d-324">Bot Framework reference:</span></span>

* [<span data-ttu-id="a580d-325">Tarjeta de recibo Node.js</span><span class="sxs-lookup"><span data-stu-id="a580d-325">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="a580d-326">Tarjeta de recibo C #</span><span class="sxs-lookup"><span data-stu-id="a580d-326">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="a580d-327">Tarjeta de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="a580d-327">Signin card</span></span>

<span data-ttu-id="a580d-328">La tarjeta de inicio de sesión permite que un bot solicite a un usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="a580d-328">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="a580d-329">Se admite en Teams forma ligeramente diferente a la que se encuentra en Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="a580d-329">It is supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="a580d-330">La tarjeta de inicio de sesión en Teams es similar a la tarjeta de inicio de sesión en Bot Framework, excepto que la tarjeta de inicio de sesión en Teams solo admite dos acciones: `signin` y `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="a580d-330">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="a580d-331">La acción de inicio de sesión se puede usar desde cualquier tarjeta de Teams, no solo desde la tarjeta de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="a580d-331">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="a580d-332">Para obtener más información sobre la autenticación, [vea Microsoft Teams de autenticación para bots](~/bots/how-to/authentication/auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="a580d-332">For more information on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="a580d-333">Compatibilidad con tarjetas de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="a580d-333">Support for signin cards</span></span>

| <span data-ttu-id="a580d-334">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="a580d-334">Bots in Teams</span></span> | <span data-ttu-id="a580d-335">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="a580d-335">Messaging extensions</span></span>  | <span data-ttu-id="a580d-336">Conectores</span><span class="sxs-lookup"><span data-stu-id="a580d-336">Connectors</span></span> | <span data-ttu-id="a580d-337">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a580d-337">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a580d-338">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-338">✔</span></span> | <span data-ttu-id="a580d-339">✖</span><span class="sxs-lookup"><span data-stu-id="a580d-339">✖</span></span> | <span data-ttu-id="a580d-340">✖</span><span class="sxs-lookup"><span data-stu-id="a580d-340">✖</span></span> | <span data-ttu-id="a580d-341">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-341">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="a580d-342">Información adicional sobre tarjetas de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="a580d-342">Additional information on signin cards</span></span>

<span data-ttu-id="a580d-343">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="a580d-343">Bot Framework reference:</span></span>

* [<span data-ttu-id="a580d-344">Tarjeta de inicio de sesión Node.js</span><span class="sxs-lookup"><span data-stu-id="a580d-344">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="a580d-345">Tarjeta de inicio de sesión C #</span><span class="sxs-lookup"><span data-stu-id="a580d-345">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="a580d-346">Tarjeta miniatura</span><span class="sxs-lookup"><span data-stu-id="a580d-346">Thumbnail card</span></span>

<span data-ttu-id="a580d-347">Una tarjeta que normalmente contiene una sola imagen en miniatura, uno o varios botones y texto.</span><span class="sxs-lookup"><span data-stu-id="a580d-347">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="a580d-348">Compatibilidad con tarjetas en miniatura</span><span class="sxs-lookup"><span data-stu-id="a580d-348">Support for thumbnail cards</span></span>

| <span data-ttu-id="a580d-349">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="a580d-349">Bots in Teams</span></span> | <span data-ttu-id="a580d-350">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="a580d-350">Messaging extensions</span></span>  | <span data-ttu-id="a580d-351">Conectores</span><span class="sxs-lookup"><span data-stu-id="a580d-351">Connectors</span></span> | <span data-ttu-id="a580d-352">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a580d-352">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a580d-353">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-353">✔</span></span> | <span data-ttu-id="a580d-354">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-354">✔</span></span> | <span data-ttu-id="a580d-355">✖</span><span class="sxs-lookup"><span data-stu-id="a580d-355">✖</span></span> | <span data-ttu-id="a580d-356">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-356">✔</span></span> |

![Ejemplo de una tarjeta en miniatura](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="a580d-358">Propiedades de una tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="a580d-358">Properties of a thumbnail card</span></span>

| <span data-ttu-id="a580d-359">Propiedad</span><span class="sxs-lookup"><span data-stu-id="a580d-359">Property</span></span> | <span data-ttu-id="a580d-360">Tipo</span><span class="sxs-lookup"><span data-stu-id="a580d-360">Type</span></span>  | <span data-ttu-id="a580d-361">Description</span><span class="sxs-lookup"><span data-stu-id="a580d-361">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a580d-362">title</span><span class="sxs-lookup"><span data-stu-id="a580d-362">title</span></span> | <span data-ttu-id="a580d-363">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="a580d-363">Rich text</span></span> | <span data-ttu-id="a580d-364">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="a580d-364">Title of the card.</span></span> <span data-ttu-id="a580d-365">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="a580d-365">Maximum 2 lines.</span></span>|
| <span data-ttu-id="a580d-366">subtitle</span><span class="sxs-lookup"><span data-stu-id="a580d-366">subtitle</span></span> | <span data-ttu-id="a580d-367">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="a580d-367">Rich text</span></span> | <span data-ttu-id="a580d-368">Subtítulo de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="a580d-368">Subtitle of the card.</span></span> <span data-ttu-id="a580d-369">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="a580d-369">Maximum 2 lines.</span></span>|
| <span data-ttu-id="a580d-370">text</span><span class="sxs-lookup"><span data-stu-id="a580d-370">text</span></span> | <span data-ttu-id="a580d-371">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="a580d-371">Rich text</span></span> | <span data-ttu-id="a580d-372">El texto aparece debajo del subtítulo.</span><span class="sxs-lookup"><span data-stu-id="a580d-372">Text appears under the subtitle.</span></span> <span data-ttu-id="a580d-373">Para ver las opciones de formato, vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="a580d-373">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="a580d-374">imágenes</span><span class="sxs-lookup"><span data-stu-id="a580d-374">images</span></span> | <span data-ttu-id="a580d-375">Matriz de imágenes</span><span class="sxs-lookup"><span data-stu-id="a580d-375">Array of images</span></span> | <span data-ttu-id="a580d-376">Imagen que se muestra en la parte superior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="a580d-376">Image displayed at the top of the card.</span></span> <span data-ttu-id="a580d-377">Relación de aspecto 1:1 cuadrado.</span><span class="sxs-lookup"><span data-stu-id="a580d-377">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="a580d-378">botones</span><span class="sxs-lookup"><span data-stu-id="a580d-378">buttons</span></span> | <span data-ttu-id="a580d-379">Matriz de objetos de acción</span><span class="sxs-lookup"><span data-stu-id="a580d-379">Array of action objects</span></span> | <span data-ttu-id="a580d-380">Conjunto de acciones aplicables a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="a580d-380">Set of actions applicable to the current card.</span></span> <span data-ttu-id="a580d-381">Máximo 6.</span><span class="sxs-lookup"><span data-stu-id="a580d-381">Maximum 6.</span></span> |
| <span data-ttu-id="a580d-382">pulsación</span><span class="sxs-lookup"><span data-stu-id="a580d-382">tap</span></span> | <span data-ttu-id="a580d-383">Action (objeto)</span><span class="sxs-lookup"><span data-stu-id="a580d-383">Action object</span></span> | <span data-ttu-id="a580d-384">Se activa cuando el usuario pulsa en la propia tarjeta.</span><span class="sxs-lookup"><span data-stu-id="a580d-384">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="a580d-385">Ejemplo de una tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="a580d-385">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="a580d-386">Información adicional</span><span class="sxs-lookup"><span data-stu-id="a580d-386">Additional information</span></span>

<span data-ttu-id="a580d-387">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="a580d-387">Bot Framework reference:</span></span>

* [<span data-ttu-id="a580d-388">Tarjeta en miniatura Node.js</span><span class="sxs-lookup"><span data-stu-id="a580d-388">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="a580d-389">Tarjeta de miniatura C #</span><span class="sxs-lookup"><span data-stu-id="a580d-389">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="a580d-390">Colecciones de tarjetas</span><span class="sxs-lookup"><span data-stu-id="a580d-390">Card collections</span></span>

<span data-ttu-id="a580d-391">Teams admite colecciones de tarjetas.</span><span class="sxs-lookup"><span data-stu-id="a580d-391">Teams supports Card collections.</span></span>

<span data-ttu-id="a580d-392">Las colecciones de tarjetas `builder.AttachmentLayout.carousel` incluyen y `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="a580d-392">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="a580d-393">Estas colecciones contienen tarjetas adaptables, de héroe o en miniatura.</span><span class="sxs-lookup"><span data-stu-id="a580d-393">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="a580d-394">Colección Carousel</span><span class="sxs-lookup"><span data-stu-id="a580d-394">Carousel collection</span></span>

<span data-ttu-id="a580d-395">El [diseño del carrusel](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) muestra un carrusel de tarjetas, opcionalmente con botones de acción asociados.</span><span class="sxs-lookup"><span data-stu-id="a580d-395">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="a580d-396">Compatibilidad con colecciones de carrusel</span><span class="sxs-lookup"><span data-stu-id="a580d-396">Support for carousel collections</span></span>

| <span data-ttu-id="a580d-397">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="a580d-397">Bots in Teams</span></span> | <span data-ttu-id="a580d-398">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="a580d-398">Messaging extensions</span></span>  | <span data-ttu-id="a580d-399">Conectores</span><span class="sxs-lookup"><span data-stu-id="a580d-399">Connectors</span></span> | <span data-ttu-id="a580d-400">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a580d-400">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a580d-401">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-401">✔</span></span> | <span data-ttu-id="a580d-402">✖</span><span class="sxs-lookup"><span data-stu-id="a580d-402">✖</span></span> | <span data-ttu-id="a580d-403">✖</span><span class="sxs-lookup"><span data-stu-id="a580d-403">✖</span></span> | <span data-ttu-id="a580d-404">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-404">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="a580d-405">Un carrusel puede mostrar un máximo de diez tarjetas por mensaje.</span><span class="sxs-lookup"><span data-stu-id="a580d-405">A carousel can display a maximum of ten cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="a580d-406">Propiedades de una tarjeta de carrusel</span><span class="sxs-lookup"><span data-stu-id="a580d-406">Properties of a carousel card</span></span>

<span data-ttu-id="a580d-407">Las propiedades de una tarjeta de carrusel son las mismas que las de las tarjetas de miniatura y de héroe.</span><span class="sxs-lookup"><span data-stu-id="a580d-407">Properties of a carousel card are same as those of the hero and thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="a580d-408">Ejemplo de una colección de carrusel</span><span class="sxs-lookup"><span data-stu-id="a580d-408">Example of a carousel collection</span></span>

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="a580d-410">Sintaxis para colecciones de carrusel</span><span class="sxs-lookup"><span data-stu-id="a580d-410">Syntax for carousel collections</span></span>

<span data-ttu-id="a580d-411">`builder.AttachmentLayoutTypes.Carousel` es la sintaxis de las colecciones de carrusel.</span><span class="sxs-lookup"><span data-stu-id="a580d-411">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

## <a name="list-collection"></a><span data-ttu-id="a580d-412">Colección List</span><span class="sxs-lookup"><span data-stu-id="a580d-412">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="a580d-413">Compatibilidad con colecciones de listas</span><span class="sxs-lookup"><span data-stu-id="a580d-413">Support for list collections</span></span>

<span data-ttu-id="a580d-414">El diseño de lista muestra una lista verticalmente apilada de tarjetas, opcionalmente con botones de acción asociados.</span><span class="sxs-lookup"><span data-stu-id="a580d-414">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="a580d-415">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="a580d-415">Bots in Teams</span></span> | <span data-ttu-id="a580d-416">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="a580d-416">Messaging extensions</span></span>  | <span data-ttu-id="a580d-417">Conectores</span><span class="sxs-lookup"><span data-stu-id="a580d-417">Connectors</span></span> | <span data-ttu-id="a580d-418">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a580d-418">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a580d-419">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-419">✔</span></span> | <span data-ttu-id="a580d-420">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-420">✔</span></span> | <span data-ttu-id="a580d-421">✖</span><span class="sxs-lookup"><span data-stu-id="a580d-421">✖</span></span> | <span data-ttu-id="a580d-422">✔</span><span class="sxs-lookup"><span data-stu-id="a580d-422">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="a580d-423">Ejemplo de una colección de listas</span><span class="sxs-lookup"><span data-stu-id="a580d-423">Example of a list collection</span></span>

![Ejemplo de una lista de tarjetas](~/assets/images/cards/list.png)

<span data-ttu-id="a580d-425">Las propiedades son las mismas que para la tarjeta de miniatura o de héroe.</span><span class="sxs-lookup"><span data-stu-id="a580d-425">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="a580d-426">Una lista puede mostrar un máximo de diez tarjetas por mensaje.</span><span class="sxs-lookup"><span data-stu-id="a580d-426">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="a580d-427">Algunas combinaciones de tarjetas de lista aún no son compatibles con iOS y Android.</span><span class="sxs-lookup"><span data-stu-id="a580d-427">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="a580d-428">Sintaxis para colecciones de listas</span><span class="sxs-lookup"><span data-stu-id="a580d-428">Syntax for list collections</span></span>

<span data-ttu-id="a580d-429">`builder.AttachmentLayout.list` es la sintaxis de las colecciones de listas.</span><span class="sxs-lookup"><span data-stu-id="a580d-429">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="a580d-430">No se admiten tarjetas en Teams</span><span class="sxs-lookup"><span data-stu-id="a580d-430">Cards not supported in Teams</span></span>

<span data-ttu-id="a580d-431">Bot Framework implementa las siguientes tarjetas, pero no son compatibles con Teams:</span><span class="sxs-lookup"><span data-stu-id="a580d-431">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="a580d-432">Tarjetas de animación</span><span class="sxs-lookup"><span data-stu-id="a580d-432">Animation cards</span></span>
* <span data-ttu-id="a580d-433">Tarjetas de audio</span><span class="sxs-lookup"><span data-stu-id="a580d-433">Audio cards</span></span>
* <span data-ttu-id="a580d-434">Tarjetas de vídeo</span><span class="sxs-lookup"><span data-stu-id="a580d-434">Video cards</span></span>

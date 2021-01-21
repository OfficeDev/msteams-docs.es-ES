---
title: Referencia de tarjetas
description: Describe todas las tarjetas y acciones de tarjeta disponibles para bots en Teams
keywords: Referencia de tarjetas bots
ms.topic: reference
ms.openlocfilehash: 839430baa5ce5e8950a21a1472036c6fd96f4edf
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911899"
---
# <a name="cards-reference"></a><span data-ttu-id="62c4b-104">Referencia de tarjetas</span><span class="sxs-lookup"><span data-stu-id="62c4b-104">Cards reference</span></span>

<span data-ttu-id="62c4b-105">Las tarjetas enumeradas en esta sección son compatibles con bots para Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="62c4b-105">The cards listed in this section are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="62c4b-106">Se basan en tarjetas definidas por Bot Framework, pero Teams no admite todas las tarjetas de Bot Framework y ha agregado algunas de sus propias tarjetas.</span><span class="sxs-lookup"><span data-stu-id="62c4b-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span> <span data-ttu-id="62c4b-107">Las diferencias se llaman en las referencias de este documento.</span><span class="sxs-lookup"><span data-stu-id="62c4b-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="62c4b-108">Ejemplos de tarjetas</span><span class="sxs-lookup"><span data-stu-id="62c4b-108">Card examples</span></span>

<span data-ttu-id="62c4b-109">Puede encontrar información adicional sobre cómo usar tarjetas en la documentación del SDK de Bot Builder (v3).</span><span class="sxs-lookup"><span data-stu-id="62c4b-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK (v3).</span></span> <span data-ttu-id="62c4b-110">Los ejemplos de código también están disponibles en el repositorio de Microsoft/BotBuilder-Samples en GitHub.</span><span class="sxs-lookup"><span data-stu-id="62c4b-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="62c4b-111">.NET</span><span class="sxs-lookup"><span data-stu-id="62c4b-111">.NET</span></span>
  * [<span data-ttu-id="62c4b-112">Agregar tarjetas como datos adjuntos a los mensajes</span><span class="sxs-lookup"><span data-stu-id="62c4b-112">Add cards as attachments to messages</span></span>](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [<span data-ttu-id="62c4b-113">Código de ejemplo de tarjetas (Bot Builder v3)</span><span class="sxs-lookup"><span data-stu-id="62c4b-113">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* <span data-ttu-id="62c4b-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="62c4b-114">Node.js</span></span>
  * [<span data-ttu-id="62c4b-115">Agregar tarjetas como datos adjuntos a los mensajes</span><span class="sxs-lookup"><span data-stu-id="62c4b-115">Add cards as attachments to messages</span></span>](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [<span data-ttu-id="62c4b-116">Código de ejemplo de tarjetas (Bot Builder v3)</span><span class="sxs-lookup"><span data-stu-id="62c4b-116">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a><span data-ttu-id="62c4b-117">Tipos de tarjetas</span><span class="sxs-lookup"><span data-stu-id="62c4b-117">Types of cards</span></span>

<span data-ttu-id="62c4b-118">En esta tabla se muestran los tipos de tarjetas disponibles:</span><span class="sxs-lookup"><span data-stu-id="62c4b-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="62c4b-119">Tipo de tarjeta</span><span class="sxs-lookup"><span data-stu-id="62c4b-119">Card type</span></span> | <span data-ttu-id="62c4b-120">Description</span><span class="sxs-lookup"><span data-stu-id="62c4b-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="62c4b-121">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="62c4b-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="62c4b-122">Tarjeta altamente personalizable que puede contener cualquier combinación de texto, voz, imágenes, botones y campos de entrada.</span><span class="sxs-lookup"><span data-stu-id="62c4b-122">Highly customizable card that can contain any combination of text, speech, images, buttons and input fields.</span></span> |
| [<span data-ttu-id="62c4b-123">Tarjeta principal</span><span class="sxs-lookup"><span data-stu-id="62c4b-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="62c4b-124">Normalmente contiene una sola imagen grande, uno o más botones y una pequeña cantidad de texto.</span><span class="sxs-lookup"><span data-stu-id="62c4b-124">Typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="62c4b-125">Tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="62c4b-125">List card</span></span>](#list-card) | <span data-ttu-id="62c4b-126">Una lista de desplazamiento de elementos.</span><span class="sxs-lookup"><span data-stu-id="62c4b-126">A scrolling list of items.</span></span> |
| [<span data-ttu-id="62c4b-127">Tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="62c4b-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="62c4b-128">Diseño flexible con varias secciones, campos, imágenes y acciones.</span><span class="sxs-lookup"><span data-stu-id="62c4b-128">Flexible layout with multiple sections, fields, images and actions.</span></span> |
| [<span data-ttu-id="62c4b-129">Tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="62c4b-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="62c4b-130">Proporciona una confirmación al usuario.</span><span class="sxs-lookup"><span data-stu-id="62c4b-130">Provides a receipt to the user.</span></span> |
| [<span data-ttu-id="62c4b-131">Tarjeta de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="62c4b-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="62c4b-132">Permite que un bot solicite que un usuario inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="62c4b-132">Enables a bot to request that a user sign in.</span></span> |
| [<span data-ttu-id="62c4b-133">Tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="62c4b-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="62c4b-134">Normalmente contiene una sola imagen en miniatura, texto corto y uno o más botones.</span><span class="sxs-lookup"><span data-stu-id="62c4b-134">Typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="62c4b-135">Colecciones de tarjetas</span><span class="sxs-lookup"><span data-stu-id="62c4b-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="62c4b-136">Se usa para devolver varios elementos en una sola respuesta.</span><span class="sxs-lookup"><span data-stu-id="62c4b-136">Used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="62c4b-137">Propiedades comunes para todas las tarjetas</span><span class="sxs-lookup"><span data-stu-id="62c4b-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="62c4b-138">Imágenes de tarjetas en línea</span><span class="sxs-lookup"><span data-stu-id="62c4b-138">Inline card images</span></span>

<span data-ttu-id="62c4b-139">La tarjeta puede contener una imagen en línea incluyendo un vínculo a la imagen disponible públicamente.</span><span class="sxs-lookup"><span data-stu-id="62c4b-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="62c4b-140">Por motivos de rendimiento, se recomienda encarecidamente hospedar la imagen en una red de entrega de contenido (CDN) pública.</span><span class="sxs-lookup"><span data-stu-id="62c4b-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="62c4b-141">Las imágenes se escalan hacia arriba o hacia abajo en tamaño mientras se mantiene la relación de aspecto para cubrir el área de la imagen y, a continuación, se recortan desde el centro para lograr la relación de aspecto adecuada para la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="62c4b-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area, and then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="62c4b-142">Las imágenes deben tener como máximo 1024×1024, en formato PNG, JPEG o GIF, y no se admite gif animado.</span><span class="sxs-lookup"><span data-stu-id="62c4b-142">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and animated GIF is not supported.</span></span>

| <span data-ttu-id="62c4b-143">Propiedad</span><span class="sxs-lookup"><span data-stu-id="62c4b-143">Property</span></span> | <span data-ttu-id="62c4b-144">Tipo</span><span class="sxs-lookup"><span data-stu-id="62c4b-144">Type</span></span>  | <span data-ttu-id="62c4b-145">Description</span><span class="sxs-lookup"><span data-stu-id="62c4b-145">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="62c4b-146">url</span><span class="sxs-lookup"><span data-stu-id="62c4b-146">url</span></span> | <span data-ttu-id="62c4b-147">URL</span><span class="sxs-lookup"><span data-stu-id="62c4b-147">URL</span></span> | <span data-ttu-id="62c4b-148">DIRECCIÓN URL HTTPS a la imagen</span><span class="sxs-lookup"><span data-stu-id="62c4b-148">HTTPS URL to the image</span></span> |
| <span data-ttu-id="62c4b-149">alt</span><span class="sxs-lookup"><span data-stu-id="62c4b-149">alt</span></span> | <span data-ttu-id="62c4b-150">Cadena</span><span class="sxs-lookup"><span data-stu-id="62c4b-150">String</span></span> | <span data-ttu-id="62c4b-151">Descripción accesible de la imagen</span><span class="sxs-lookup"><span data-stu-id="62c4b-151">Accessible description of the image</span></span> |

### <a name="buttons"></a><span data-ttu-id="62c4b-152">Botones</span><span class="sxs-lookup"><span data-stu-id="62c4b-152">Buttons</span></span>

<span data-ttu-id="62c4b-153">Los botones se muestran apilados en la parte inferior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="62c4b-153">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="62c4b-154">El texto del botón siempre está en una sola línea y se truncará si el texto supera el ancho del botón.</span><span class="sxs-lookup"><span data-stu-id="62c4b-154">Button text is always on a single line and will be truncated if the text exceeds the button width.</span></span> <span data-ttu-id="62c4b-155">No se mostrarán botones adicionales más allá del número máximo admitido por la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="62c4b-155">Any additional buttons beyond the maximum number supported by the card will not be shown.</span></span>

<span data-ttu-id="62c4b-156">Vea [Acciones de tarjeta](~/task-modules-and-cards/cards/cards-actions.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="62c4b-156">See [Card Actions](~/task-modules-and-cards/cards/cards-actions.md) for more information.</span></span>

### <a name="card-formatting"></a><span data-ttu-id="62c4b-157">Formato de tarjeta</span><span class="sxs-lookup"><span data-stu-id="62c4b-157">Card formatting</span></span>

<span data-ttu-id="62c4b-158">Consulta [Formato de tarjeta para](~/task-modules-and-cards/cards/cards-format.md) obtener más información sobre el formato de texto en las tarjetas.</span><span class="sxs-lookup"><span data-stu-id="62c4b-158">See [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for more information on text formatting in cards.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="62c4b-159">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="62c4b-159">Adaptive card</span></span>

<span data-ttu-id="62c4b-160">Una tarjeta adaptable es una tarjeta personalizable que puede contener cualquier combinación de texto, voz, imágenes, botones y campos de entrada.</span><span class="sxs-lookup"><span data-stu-id="62c4b-160">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="62c4b-161">Consulta [tarjetas adaptables v1.2.0.](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)</span><span class="sxs-lookup"><span data-stu-id="62c4b-161">See [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="62c4b-162">Compatibilidad con tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="62c4b-162">Support for adaptive cards</span></span>

| <span data-ttu-id="62c4b-163">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="62c4b-163">Bots in Teams</span></span> | <span data-ttu-id="62c4b-164">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="62c4b-164">Messaging extensions</span></span>  | <span data-ttu-id="62c4b-165">Conectores</span><span class="sxs-lookup"><span data-stu-id="62c4b-165">Connectors</span></span> | <span data-ttu-id="62c4b-166">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="62c4b-166">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="62c4b-167">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-167">✔</span></span> | <span data-ttu-id="62c4b-168">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-168">✔</span></span> | <span data-ttu-id="62c4b-169">✖</span><span class="sxs-lookup"><span data-stu-id="62c4b-169">✖</span></span> | <span data-ttu-id="62c4b-170">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-170">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="62c4b-171">La plataforma de Teams admite la versión 1.2 o anterior de las características de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="62c4b-171">Teams platform supports v1.2 or earlier of Adaptive card features.</span></span>
> * <span data-ttu-id="62c4b-172">Actualmente, los elementos multimedia no se admiten en la tarjeta adaptable v1.2 en la plataforma teams.</span><span class="sxs-lookup"><span data-stu-id="62c4b-172">Media elements are currently not supported in Adaptive card v1.2 on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="62c4b-173">Ejemplo de una tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="62c4b-173">Example of an adaptive card</span></span>

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="62c4b-175">Información adicional sobre tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="62c4b-175">Additional information on adaptive cards</span></span>

* [<span data-ttu-id="62c4b-176">Introducción a las tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="62c4b-176">Adaptive cards overview</span></span>](/adaptive-cards/)
* [<span data-ttu-id="62c4b-177">Acciones de tarjeta adaptable en Teams</span><span class="sxs-lookup"><span data-stu-id="62c4b-177">Adaptive card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a><span data-ttu-id="62c4b-178">Tarjeta principal</span><span class="sxs-lookup"><span data-stu-id="62c4b-178">Hero card</span></span>

<span data-ttu-id="62c4b-179">Una tarjeta que normalmente contiene una sola imagen grande, uno o más botones y texto.</span><span class="sxs-lookup"><span data-stu-id="62c4b-179">A card that typically contains a single large image, one or more buttons and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="62c4b-180">Compatibilidad con tarjetas de imagen principal</span><span class="sxs-lookup"><span data-stu-id="62c4b-180">Support for hero cards</span></span>

| <span data-ttu-id="62c4b-181">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="62c4b-181">Bots in Teams</span></span> | <span data-ttu-id="62c4b-182">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="62c4b-182">Messaging Extensions</span></span>  | <span data-ttu-id="62c4b-183">Conectores</span><span class="sxs-lookup"><span data-stu-id="62c4b-183">Connectors</span></span> | <span data-ttu-id="62c4b-184">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="62c4b-184">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="62c4b-185">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-185">✔</span></span> | <span data-ttu-id="62c4b-186">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-186">✔</span></span> | <span data-ttu-id="62c4b-187">✖</span><span class="sxs-lookup"><span data-stu-id="62c4b-187">✖</span></span> | <span data-ttu-id="62c4b-188">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-188">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="62c4b-189">Propiedades de una tarjeta principal</span><span class="sxs-lookup"><span data-stu-id="62c4b-189">Properties of a hero card</span></span>

| <span data-ttu-id="62c4b-190">Propiedad</span><span class="sxs-lookup"><span data-stu-id="62c4b-190">Property</span></span> | <span data-ttu-id="62c4b-191">Tipo</span><span class="sxs-lookup"><span data-stu-id="62c4b-191">Type</span></span>  | <span data-ttu-id="62c4b-192">Description</span><span class="sxs-lookup"><span data-stu-id="62c4b-192">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="62c4b-193">title</span><span class="sxs-lookup"><span data-stu-id="62c4b-193">title</span></span> | <span data-ttu-id="62c4b-194">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="62c4b-194">Rich text</span></span> | <span data-ttu-id="62c4b-195">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="62c4b-195">Title of the card.</span></span> <span data-ttu-id="62c4b-196">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="62c4b-196">Maximum 2 lines.</span></span> |
| <span data-ttu-id="62c4b-197">subtitle</span><span class="sxs-lookup"><span data-stu-id="62c4b-197">subtitle</span></span> | <span data-ttu-id="62c4b-198">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="62c4b-198">Rich text</span></span> | <span data-ttu-id="62c4b-199">Subtítulo de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="62c4b-199">Subtitle of the card.</span></span> <span data-ttu-id="62c4b-200">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="62c4b-200">Maximum 2 lines.</span></span>|
| <span data-ttu-id="62c4b-201">text</span><span class="sxs-lookup"><span data-stu-id="62c4b-201">text</span></span> | <span data-ttu-id="62c4b-202">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="62c4b-202">Rich text</span></span> | <span data-ttu-id="62c4b-203">El texto aparece justo debajo del subtítulo; vea [Formato de tarjeta para](~/task-modules-and-cards/cards/cards-format.md) obtener más información sobre las opciones de formato.</span><span class="sxs-lookup"><span data-stu-id="62c4b-203">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="62c4b-204">imágenes</span><span class="sxs-lookup"><span data-stu-id="62c4b-204">images</span></span> | <span data-ttu-id="62c4b-205">Matriz de imágenes</span><span class="sxs-lookup"><span data-stu-id="62c4b-205">Array of images</span></span> | <span data-ttu-id="62c4b-206">Imagen que se muestra en la parte superior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="62c4b-206">Image displayed at top of card.</span></span> <span data-ttu-id="62c4b-207">Relación de aspecto 16:9.</span><span class="sxs-lookup"><span data-stu-id="62c4b-207">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="62c4b-208">botones</span><span class="sxs-lookup"><span data-stu-id="62c4b-208">buttons</span></span> | <span data-ttu-id="62c4b-209">Matriz de objetos de acción</span><span class="sxs-lookup"><span data-stu-id="62c4b-209">Array of action objects</span></span> | <span data-ttu-id="62c4b-210">Conjunto de acciones aplicables a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="62c4b-210">Set of actions applicable to the current card.</span></span> <span data-ttu-id="62c4b-211">Máximo 6.</span><span class="sxs-lookup"><span data-stu-id="62c4b-211">Maximum 6.</span></span> |
| <span data-ttu-id="62c4b-212">pulsación</span><span class="sxs-lookup"><span data-stu-id="62c4b-212">tap</span></span> | <span data-ttu-id="62c4b-213">Action (objeto)</span><span class="sxs-lookup"><span data-stu-id="62c4b-213">Action object</span></span> | <span data-ttu-id="62c4b-214">Esta acción se activará cuando el usuario pulse en la propia tarjeta.</span><span class="sxs-lookup"><span data-stu-id="62c4b-214">This action will be activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="62c4b-215">Ejemplo de una tarjeta principal</span><span class="sxs-lookup"><span data-stu-id="62c4b-215">Example of a hero card</span></span>

![Ejemplo de una tarjeta principal](~/assets/images/cards/hero.png)

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="62c4b-217">Información adicional sobre las tarjetas de identificación principal</span><span class="sxs-lookup"><span data-stu-id="62c4b-217">Additional information on hero cards</span></span>

<span data-ttu-id="62c4b-218">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="62c4b-218">Bot Framework reference:</span></span>

* [<span data-ttu-id="62c4b-219">Nodo de tarjeta principal</span><span class="sxs-lookup"><span data-stu-id="62c4b-219">Hero card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [<span data-ttu-id="62c4b-220">Tarjeta principal C #</span><span class="sxs-lookup"><span data-stu-id="62c4b-220">Hero card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="62c4b-221">Tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="62c4b-221">List card</span></span>

<span data-ttu-id="62c4b-222">Teams ha agregado la tarjeta de lista para proporcionar funciones más allá de lo que puede proporcionar la colección de listas.</span><span class="sxs-lookup"><span data-stu-id="62c4b-222">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="62c4b-223">La tarjeta de lista proporciona una lista de elementos de desplazamiento.</span><span class="sxs-lookup"><span data-stu-id="62c4b-223">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="62c4b-224">Compatibilidad con tarjetas de lista</span><span class="sxs-lookup"><span data-stu-id="62c4b-224">Support for list cards</span></span>

| <span data-ttu-id="62c4b-225">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="62c4b-225">Bots in Teams</span></span> | <span data-ttu-id="62c4b-226">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="62c4b-226">Messaging extensions</span></span>  | <span data-ttu-id="62c4b-227">Conectores</span><span class="sxs-lookup"><span data-stu-id="62c4b-227">Connectors</span></span> | <span data-ttu-id="62c4b-228">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="62c4b-228">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="62c4b-229">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-229">✔</span></span> | <span data-ttu-id="62c4b-230">✖</span><span class="sxs-lookup"><span data-stu-id="62c4b-230">✖</span></span> | <span data-ttu-id="62c4b-231">✖</span><span class="sxs-lookup"><span data-stu-id="62c4b-231">✖</span></span> |<span data-ttu-id="62c4b-232">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-232">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="62c4b-233">Propiedades de una tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="62c4b-233">Properties of a list card</span></span>

| <span data-ttu-id="62c4b-234">Propiedad</span><span class="sxs-lookup"><span data-stu-id="62c4b-234">Property</span></span> | <span data-ttu-id="62c4b-235">Tipo</span><span class="sxs-lookup"><span data-stu-id="62c4b-235">Type</span></span>  | <span data-ttu-id="62c4b-236">Description</span><span class="sxs-lookup"><span data-stu-id="62c4b-236">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="62c4b-237">title</span><span class="sxs-lookup"><span data-stu-id="62c4b-237">title</span></span> | <span data-ttu-id="62c4b-238">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="62c4b-238">Rich text</span></span> | <span data-ttu-id="62c4b-239">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="62c4b-239">Title of the card.</span></span> <span data-ttu-id="62c4b-240">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="62c4b-240">Maximum 2 lines.</span></span>|
| <span data-ttu-id="62c4b-241">items</span><span class="sxs-lookup"><span data-stu-id="62c4b-241">items</span></span> | <span data-ttu-id="62c4b-242">Matriz de elementos de lista</span><span class="sxs-lookup"><span data-stu-id="62c4b-242">Array of list items</span></span>  ||
| <span data-ttu-id="62c4b-243">botones</span><span class="sxs-lookup"><span data-stu-id="62c4b-243">buttons</span></span> | <span data-ttu-id="62c4b-244">Matriz de objetos de acción</span><span class="sxs-lookup"><span data-stu-id="62c4b-244">Array of action objects</span></span> | <span data-ttu-id="62c4b-245">Conjunto de acciones aplicables a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="62c4b-245">Set of actions applicable to the current card.</span></span> <span data-ttu-id="62c4b-246">Máximo 6.</span><span class="sxs-lookup"><span data-stu-id="62c4b-246">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="62c4b-247">Ejemplo de una tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="62c4b-247">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="62c4b-248">Tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="62c4b-248">Office 365 connector card</span></span>

<span data-ttu-id="62c4b-249">La tarjeta del conector de Office 365 se admite en Teams, no en Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="62c4b-249">The Office 365 Connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="62c4b-250">Esta tarjeta proporciona un diseño flexible con varias secciones, campos, imágenes y acciones.</span><span class="sxs-lookup"><span data-stu-id="62c4b-250">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="62c4b-251">Esta tarjeta encapsula una tarjeta de conector para que la puedan usar los bots.</span><span class="sxs-lookup"><span data-stu-id="62c4b-251">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="62c4b-252">Vea la sección de notas para ver las diferencias entre las tarjetas de conector y la tarjeta O365.</span><span class="sxs-lookup"><span data-stu-id="62c4b-252">See the notes section for differences between connector cards and the O365 card.</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="62c4b-253">Compatibilidad con tarjetas de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="62c4b-253">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="62c4b-254">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="62c4b-254">Bots in Teams</span></span> | <span data-ttu-id="62c4b-255">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="62c4b-255">Messaging extensions</span></span>  | <span data-ttu-id="62c4b-256">Conectores</span><span class="sxs-lookup"><span data-stu-id="62c4b-256">Connectors</span></span> | <span data-ttu-id="62c4b-257">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="62c4b-257">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="62c4b-258">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-258">✔</span></span> | <span data-ttu-id="62c4b-259">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-259">✔</span></span> | <span data-ttu-id="62c4b-260">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-260">✔</span></span> | <span data-ttu-id="62c4b-261">✖</span><span class="sxs-lookup"><span data-stu-id="62c4b-261">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="62c4b-262">Propiedades de la tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="62c4b-262">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="62c4b-263">Propiedad</span><span class="sxs-lookup"><span data-stu-id="62c4b-263">Property</span></span> | <span data-ttu-id="62c4b-264">Tipo</span><span class="sxs-lookup"><span data-stu-id="62c4b-264">Type</span></span>  | <span data-ttu-id="62c4b-265">Description</span><span class="sxs-lookup"><span data-stu-id="62c4b-265">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="62c4b-266">title</span><span class="sxs-lookup"><span data-stu-id="62c4b-266">title</span></span> | <span data-ttu-id="62c4b-267">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="62c4b-267">Rich text</span></span> | <span data-ttu-id="62c4b-268">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="62c4b-268">Title of the card.</span></span> <span data-ttu-id="62c4b-269">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="62c4b-269">Maximum 2 lines.</span></span> |
| <span data-ttu-id="62c4b-270">summary</span><span class="sxs-lookup"><span data-stu-id="62c4b-270">summary</span></span> | <span data-ttu-id="62c4b-271">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="62c4b-271">Rich text</span></span> | <span data-ttu-id="62c4b-272">Resumen de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="62c4b-272">Summary of the card.</span></span> <span data-ttu-id="62c4b-273">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="62c4b-273">Maximum 2 lines.</span></span> |
| <span data-ttu-id="62c4b-274">text</span><span class="sxs-lookup"><span data-stu-id="62c4b-274">text</span></span> | <span data-ttu-id="62c4b-275">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="62c4b-275">Rich text</span></span> | <span data-ttu-id="62c4b-276">El texto aparece justo debajo del subtítulo; vea [Formato de tarjeta para](~/task-modules-and-cards/cards/cards-format.md) obtener más información sobre las opciones de formato.</span><span class="sxs-lookup"><span data-stu-id="62c4b-276">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="62c4b-277">themeColor</span><span class="sxs-lookup"><span data-stu-id="62c4b-277">themeColor</span></span> | <span data-ttu-id="62c4b-278">Cadena HEX</span><span class="sxs-lookup"><span data-stu-id="62c4b-278">HEX string</span></span> | <span data-ttu-id="62c4b-279">Color que reemplaza el accentColor proporcionado desde el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="62c4b-279">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="62c4b-280">Notas en la tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="62c4b-280">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="62c4b-281">Las tarjetas de conector de Office 365 funcionan correctamente en Microsoft Teams, incluidas [las acciones actionCard](/outlook/actionable-messages/card-reference#actioncard-action).</span><span class="sxs-lookup"><span data-stu-id="62c4b-281">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="62c4b-282">Una diferencia importante entre el uso de tarjetas de conector desde un conector y el uso de tarjetas de conector en el bot es el control de las acciones de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="62c4b-282">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="62c4b-283">Para un conector, el extremo recibe la carga de la tarjeta a través de HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="62c4b-283">For a connector, the endpoint receives the card payload via HTTP POST.</span></span>
* <span data-ttu-id="62c4b-284">Para un bot, la acción desencadena una actividad que envía solo el identificador de acción `HttpPOST` y el cuerpo al `invoke` bot.</span><span class="sxs-lookup"><span data-stu-id="62c4b-284">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="62c4b-285">Cada tarjeta de conector puede mostrar un máximo de 10 secciones y cada sección puede contener un máximo de 5 imágenes y 5 acciones.</span><span class="sxs-lookup"><span data-stu-id="62c4b-285">Each connector card can display a maximum of 10 sections, and each section can contain a maximum of 5 images and 5 actions.</span></span>

> [!NOTE]
> <span data-ttu-id="62c4b-286">Las secciones, imágenes o acciones adicionales de un mensaje no aparecerán.</span><span class="sxs-lookup"><span data-stu-id="62c4b-286">Any additional sections, images, or actions in a message will not appear.</span></span>

<span data-ttu-id="62c4b-287">Todos los campos de texto admiten Markdown y HTML.</span><span class="sxs-lookup"><span data-stu-id="62c4b-287">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="62c4b-288">Puede controlar qué secciones usan Markdown o HTML estableciendo la `markdown` propiedad en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="62c4b-288">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="62c4b-289">De forma predeterminada, `markdown` se establece en ; si desea usar HTML en su `true` lugar, establezca en `markdown` `false` .</span><span class="sxs-lookup"><span data-stu-id="62c4b-289">By default, `markdown` is set to `true`; if you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="62c4b-290">Si especificas la `themeColor` propiedad, esta invalida la `accentColor` propiedad en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="62c4b-290">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="62c4b-291">Para especificar el estilo de representación `activityImage` para , puede establecer lo `activityImageType` siguiente:</span><span class="sxs-lookup"><span data-stu-id="62c4b-291">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="62c4b-292">Valor</span><span class="sxs-lookup"><span data-stu-id="62c4b-292">Value</span></span> | <span data-ttu-id="62c4b-293">Description</span><span class="sxs-lookup"><span data-stu-id="62c4b-293">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="62c4b-294">Valor predeterminado; `activityImage` se recortará como un círculo.</span><span class="sxs-lookup"><span data-stu-id="62c4b-294">Default; `activityImage` will be cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="62c4b-295">`activityImage` se mostrará como un rectángulo y conservará su relación de aspecto.</span><span class="sxs-lookup"><span data-stu-id="62c4b-295">`activityImage` will be displayed as a rectangle and retain its aspect ratio.</span></span> |

<span data-ttu-id="62c4b-296">Para obtener todos los demás detalles acerca de las propiedades de la tarjeta de conector, vea la [referencia de tarjeta de mensaje que puede acción.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="62c4b-296">For all other details about connector card properties, see the [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="62c4b-297">Las únicas propiedades de tarjeta de conector que Microsoft Teams no admite actualmente son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="62c4b-297">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="62c4b-298">`startGroup` (siempre se trata como `true` en Teams)</span><span class="sxs-lookup"><span data-stu-id="62c4b-298">`startGroup` (always treated as `true` in Teams)</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="62c4b-299">Ejemplo de una tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="62c4b-299">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="62c4b-300">Tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="62c4b-300">Receipt card</span></span>

<span data-ttu-id="62c4b-301">Teams admite la tarjeta de recibo.</span><span class="sxs-lookup"><span data-stu-id="62c4b-301">Teams supports receipt card.</span></span> <span data-ttu-id="62c4b-302">Es una tarjeta que permite a un bot proporcionar un recibo al usuario.</span><span class="sxs-lookup"><span data-stu-id="62c4b-302">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="62c4b-303">Normalmente contiene la lista de elementos que se deben incluir en el recibo, como los impuestos y la información total.</span><span class="sxs-lookup"><span data-stu-id="62c4b-303">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="62c4b-304">Compatibilidad con tarjetas de recibo</span><span class="sxs-lookup"><span data-stu-id="62c4b-304">Support for receipt cards</span></span>

| <span data-ttu-id="62c4b-305">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="62c4b-305">Bots in Teams</span></span> | <span data-ttu-id="62c4b-306">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="62c4b-306">Messaging extensions</span></span>  | <span data-ttu-id="62c4b-307">Conectores</span><span class="sxs-lookup"><span data-stu-id="62c4b-307">Connectors</span></span> | <span data-ttu-id="62c4b-308">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="62c4b-308">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="62c4b-309">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-309">✔</span></span> | <span data-ttu-id="62c4b-310">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-310">✔</span></span> | <span data-ttu-id="62c4b-311">✖</span><span class="sxs-lookup"><span data-stu-id="62c4b-311">✖</span></span> | <span data-ttu-id="62c4b-312">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-312">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="62c4b-313">Ejemplo de una tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="62c4b-313">Example of a receipt card</span></span>

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="62c4b-315">Información adicional sobre las tarjetas de recibo</span><span class="sxs-lookup"><span data-stu-id="62c4b-315">Additional information on receipt cards</span></span>

<span data-ttu-id="62c4b-316">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="62c4b-316">Bot Framework reference:</span></span>

* [<span data-ttu-id="62c4b-317">Nodo de tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="62c4b-317">Receipt card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="62c4b-318">Tarjeta de recibo C #</span><span class="sxs-lookup"><span data-stu-id="62c4b-318">Receipt card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="62c4b-319">Tarjeta de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="62c4b-319">Signin card</span></span>

<span data-ttu-id="62c4b-320">La tarjeta de inicio de sesión permite a un bot solicitar a un usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="62c4b-320">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="62c4b-321">Se admite en Teams de una forma ligeramente diferente a la que se encuentra en Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="62c4b-321">Supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="62c4b-322">La tarjeta de inicio de sesión en Teams es similar a la tarjeta de inicio de sesión en Bot Framework, excepto que la tarjeta de inicio de sesión en Teams solo admite dos acciones: `signin` y `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="62c4b-322">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="62c4b-323">La *acción de inicio de* sesión se puede usar desde cualquier tarjeta de Teams, no solo desde la tarjeta de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="62c4b-323">The *signin action* can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="62c4b-324">Para obtener más información sobre la autenticación, vea [el flujo de autenticación de Microsoft Teams para bots.](~/bots/how-to/authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="62c4b-324">For more details on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="62c4b-325">Compatibilidad con tarjetas de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="62c4b-325">Support for Signin cards</span></span>

| <span data-ttu-id="62c4b-326">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="62c4b-326">Bots in Teams</span></span> | <span data-ttu-id="62c4b-327">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="62c4b-327">Messaging extensions</span></span>  | <span data-ttu-id="62c4b-328">Conectores</span><span class="sxs-lookup"><span data-stu-id="62c4b-328">Connectors</span></span> | <span data-ttu-id="62c4b-329">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="62c4b-329">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="62c4b-330">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-330">✔</span></span> | <span data-ttu-id="62c4b-331">✖</span><span class="sxs-lookup"><span data-stu-id="62c4b-331">✖</span></span> | <span data-ttu-id="62c4b-332">✖</span><span class="sxs-lookup"><span data-stu-id="62c4b-332">✖</span></span> | <span data-ttu-id="62c4b-333">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-333">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="62c4b-334">Información adicional sobre las tarjetas de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="62c4b-334">Additional information on signin cards</span></span>

<span data-ttu-id="62c4b-335">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="62c4b-335">Bot Framework reference:</span></span>

* [<span data-ttu-id="62c4b-336">Nodo de tarjeta de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="62c4b-336">Signin card Node</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="62c4b-337">Tarjeta de inicio de sesión C #</span><span class="sxs-lookup"><span data-stu-id="62c4b-337">Signin card C#</span></span>](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="62c4b-338">Tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="62c4b-338">Thumbnail card</span></span>

<span data-ttu-id="62c4b-339">Una tarjeta que normalmente contiene una sola imagen en miniatura, uno o más botones y texto.</span><span class="sxs-lookup"><span data-stu-id="62c4b-339">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="62c4b-340">Compatibilidad con tarjetas en miniatura</span><span class="sxs-lookup"><span data-stu-id="62c4b-340">Support for thumbnail cards</span></span>

| <span data-ttu-id="62c4b-341">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="62c4b-341">Bots in Teams</span></span> | <span data-ttu-id="62c4b-342">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="62c4b-342">Messaging extensions</span></span>  | <span data-ttu-id="62c4b-343">Conectores</span><span class="sxs-lookup"><span data-stu-id="62c4b-343">Connectors</span></span> | <span data-ttu-id="62c4b-344">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="62c4b-344">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="62c4b-345">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-345">✔</span></span> | <span data-ttu-id="62c4b-346">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-346">✔</span></span> | <span data-ttu-id="62c4b-347">✖</span><span class="sxs-lookup"><span data-stu-id="62c4b-347">✖</span></span> | <span data-ttu-id="62c4b-348">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-348">✔</span></span> |

![Ejemplo de una tarjeta en miniatura](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="62c4b-350">Propiedades de una tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="62c4b-350">Properties of a thumbnail card</span></span>

| <span data-ttu-id="62c4b-351">Propiedad</span><span class="sxs-lookup"><span data-stu-id="62c4b-351">Property</span></span> | <span data-ttu-id="62c4b-352">Tipo</span><span class="sxs-lookup"><span data-stu-id="62c4b-352">Type</span></span>  | <span data-ttu-id="62c4b-353">Description</span><span class="sxs-lookup"><span data-stu-id="62c4b-353">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="62c4b-354">title</span><span class="sxs-lookup"><span data-stu-id="62c4b-354">title</span></span> | <span data-ttu-id="62c4b-355">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="62c4b-355">Rich text</span></span> | <span data-ttu-id="62c4b-356">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="62c4b-356">Title of the card.</span></span> <span data-ttu-id="62c4b-357">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="62c4b-357">Maximum 2 lines.</span></span>|
| <span data-ttu-id="62c4b-358">subtitle</span><span class="sxs-lookup"><span data-stu-id="62c4b-358">subtitle</span></span> | <span data-ttu-id="62c4b-359">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="62c4b-359">Rich text</span></span> | <span data-ttu-id="62c4b-360">Subtítulo de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="62c4b-360">Subtitle of the card.</span></span> <span data-ttu-id="62c4b-361">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="62c4b-361">Maximum 2 lines.</span></span>|
| <span data-ttu-id="62c4b-362">text</span><span class="sxs-lookup"><span data-stu-id="62c4b-362">text</span></span> | <span data-ttu-id="62c4b-363">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="62c4b-363">Rich text</span></span> | <span data-ttu-id="62c4b-364">El texto aparece justo debajo del subtítulo; vea [Formato de tarjeta para](~/task-modules-and-cards/cards/cards-format.md) obtener más información sobre las opciones de formato.</span><span class="sxs-lookup"><span data-stu-id="62c4b-364">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="62c4b-365">imágenes</span><span class="sxs-lookup"><span data-stu-id="62c4b-365">images</span></span> | <span data-ttu-id="62c4b-366">Matriz de imágenes</span><span class="sxs-lookup"><span data-stu-id="62c4b-366">Array of images</span></span> | <span data-ttu-id="62c4b-367">Imagen que se muestra en la parte superior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="62c4b-367">Image displayed at top of card.</span></span> <span data-ttu-id="62c4b-368">Relación de aspecto 1:1 (cuadrado).</span><span class="sxs-lookup"><span data-stu-id="62c4b-368">Aspect ratio 1:1 (square).</span></span> |
| <span data-ttu-id="62c4b-369">botones</span><span class="sxs-lookup"><span data-stu-id="62c4b-369">buttons</span></span> | <span data-ttu-id="62c4b-370">Matriz de objetos de acción</span><span class="sxs-lookup"><span data-stu-id="62c4b-370">Array of action objects</span></span> | <span data-ttu-id="62c4b-371">Conjunto de acciones aplicables a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="62c4b-371">Set of actions applicable to the current card.</span></span> <span data-ttu-id="62c4b-372">Máximo 6.</span><span class="sxs-lookup"><span data-stu-id="62c4b-372">Maximum 6.</span></span> |
| <span data-ttu-id="62c4b-373">pulsación</span><span class="sxs-lookup"><span data-stu-id="62c4b-373">tap</span></span> | <span data-ttu-id="62c4b-374">Action (objeto)</span><span class="sxs-lookup"><span data-stu-id="62c4b-374">Action object</span></span> | <span data-ttu-id="62c4b-375">Esta acción se activará cuando el usuario pulse en la propia tarjeta.</span><span class="sxs-lookup"><span data-stu-id="62c4b-375">This action will be activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="62c4b-376">Ejemplo de una tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="62c4b-376">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="62c4b-377">Información adicional</span><span class="sxs-lookup"><span data-stu-id="62c4b-377">Additional information</span></span>

<span data-ttu-id="62c4b-378">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="62c4b-378">Bot Framework reference:</span></span>

* [<span data-ttu-id="62c4b-379">Nodo de tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="62c4b-379">Thumbnail card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="62c4b-380">Tarjeta en miniatura C #</span><span class="sxs-lookup"><span data-stu-id="62c4b-380">Thumbnail card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="62c4b-381">Colecciones de tarjetas</span><span class="sxs-lookup"><span data-stu-id="62c4b-381">Card collections</span></span>

<span data-ttu-id="62c4b-382">Teams admite colecciones de tarjetas.</span><span class="sxs-lookup"><span data-stu-id="62c4b-382">Teams supports Card collections.</span></span>

<span data-ttu-id="62c4b-383">Colecciones de tarjetas: `builder.AttachmentLayout.carousel` y `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="62c4b-383">Card collections: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="62c4b-384">Estas colecciones contienen tarjetas adaptables, de imagen principal o en miniatura.</span><span class="sxs-lookup"><span data-stu-id="62c4b-384">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="62c4b-385">Carrusel (colección)</span><span class="sxs-lookup"><span data-stu-id="62c4b-385">Carousel collection</span></span>

<span data-ttu-id="62c4b-386">El [diseño de carrusel](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true) muestra un carrusel de tarjetas, opcionalmente con botones de acción asociados.</span><span class="sxs-lookup"><span data-stu-id="62c4b-386">The [carousel layout](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="62c4b-387">Compatibilidad con colecciones de carrusel</span><span class="sxs-lookup"><span data-stu-id="62c4b-387">Support for carousel collections</span></span>

| <span data-ttu-id="62c4b-388">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="62c4b-388">Bots in Teams</span></span> | <span data-ttu-id="62c4b-389">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="62c4b-389">Messaging extensions</span></span>  | <span data-ttu-id="62c4b-390">Conectores</span><span class="sxs-lookup"><span data-stu-id="62c4b-390">Connectors</span></span> | <span data-ttu-id="62c4b-391">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="62c4b-391">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="62c4b-392">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-392">✔</span></span> | <span data-ttu-id="62c4b-393">✖</span><span class="sxs-lookup"><span data-stu-id="62c4b-393">✖</span></span> | <span data-ttu-id="62c4b-394">✖</span><span class="sxs-lookup"><span data-stu-id="62c4b-394">✖</span></span> | <span data-ttu-id="62c4b-395">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-395">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="62c4b-396">Un carrusel puede mostrar un máximo de 10 tarjetas por mensaje.</span><span class="sxs-lookup"><span data-stu-id="62c4b-396">A carousel can display a maximum of 10 cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="62c4b-397">Propiedades de una tarjeta de carrusel</span><span class="sxs-lookup"><span data-stu-id="62c4b-397">Properties of a carousel card</span></span>

<span data-ttu-id="62c4b-398">Las propiedades de una tarjeta de carrusel son las mismas que las de las tarjetas Hero y Thumbnail.</span><span class="sxs-lookup"><span data-stu-id="62c4b-398">Properties of a Carousel card are same as those of the Hero and Thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="62c4b-399">Ejemplo de una colección de carrusel</span><span class="sxs-lookup"><span data-stu-id="62c4b-399">Example of a carousel collection</span></span>

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="62c4b-401">Sintaxis para colecciones de carrusel</span><span class="sxs-lookup"><span data-stu-id="62c4b-401">Syntax for carousel collections</span></span>

`builder.AttachmentLayoutTypes.Carousel`

## <a name="list-collection"></a><span data-ttu-id="62c4b-402">Colección de listas</span><span class="sxs-lookup"><span data-stu-id="62c4b-402">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="62c4b-403">Compatibilidad con colecciones de listas</span><span class="sxs-lookup"><span data-stu-id="62c4b-403">Support for list collections</span></span>

<span data-ttu-id="62c4b-404">El diseño de lista muestra una lista apilada verticalmente de tarjetas, opcionalmente con botones de acción asociados.</span><span class="sxs-lookup"><span data-stu-id="62c4b-404">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="62c4b-405">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="62c4b-405">Bots in Teams</span></span> | <span data-ttu-id="62c4b-406">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="62c4b-406">Messaging extensions</span></span>  | <span data-ttu-id="62c4b-407">Conectores</span><span class="sxs-lookup"><span data-stu-id="62c4b-407">Connectors</span></span> | <span data-ttu-id="62c4b-408">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="62c4b-408">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="62c4b-409">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-409">✔</span></span> | <span data-ttu-id="62c4b-410">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-410">✔</span></span> | <span data-ttu-id="62c4b-411">✖</span><span class="sxs-lookup"><span data-stu-id="62c4b-411">✖</span></span> | <span data-ttu-id="62c4b-412">✔</span><span class="sxs-lookup"><span data-stu-id="62c4b-412">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="62c4b-413">Ejemplo de una colección de listas</span><span class="sxs-lookup"><span data-stu-id="62c4b-413">Example of a list collection</span></span>

![Ejemplo de una lista de tarjetas](~/assets/images/cards/list.png)

<span data-ttu-id="62c4b-415">Las propiedades son las mismas que para la tarjeta principal o en miniatura.</span><span class="sxs-lookup"><span data-stu-id="62c4b-415">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="62c4b-416">Una lista puede mostrar un máximo de 10 tarjetas por mensaje.</span><span class="sxs-lookup"><span data-stu-id="62c4b-416">A list can display a maximum of 10 cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="62c4b-417">Algunas combinaciones de tarjetas de lista aún no se admiten en iOS y Android.</span><span class="sxs-lookup"><span data-stu-id="62c4b-417">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="62c4b-418">Sintaxis para colecciones de listas</span><span class="sxs-lookup"><span data-stu-id="62c4b-418">Syntax for list collections</span></span>

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="62c4b-419">Tarjetas no admitidas en Teams</span><span class="sxs-lookup"><span data-stu-id="62c4b-419">Cards not supported in Teams</span></span>

<span data-ttu-id="62c4b-420">Bot Framework implementa las siguientes tarjetas, pero Teams no las admite.</span><span class="sxs-lookup"><span data-stu-id="62c4b-420">The following cards are implemented by the Bot Framework, but are NOT supported by Teams.</span></span>

* <span data-ttu-id="62c4b-421">Tarjetas de animación</span><span class="sxs-lookup"><span data-stu-id="62c4b-421">Animation cards</span></span>
* <span data-ttu-id="62c4b-422">Tarjetas de audio</span><span class="sxs-lookup"><span data-stu-id="62c4b-422">Audio cards</span></span>
* <span data-ttu-id="62c4b-423">Tarjetas de vídeo</span><span class="sxs-lookup"><span data-stu-id="62c4b-423">Video cards</span></span>

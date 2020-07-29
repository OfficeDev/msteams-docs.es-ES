---
title: Referencia de tarjetas
description: Describe todas las tarjetas y las acciones de tarjetas disponibles para bots en Microsoft Teams.
keywords: referencia de tarjetas de bots
ms.openlocfilehash: 7bd1cbea0aec03913c9bce205ae68eedba284637
ms.sourcegitcommit: 1b909fb9ccf6cdd84ed0d8f9ea0463243a802a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "45434548"
---
# <a name="cards-reference"></a><span data-ttu-id="5b61e-104">Referencia de tarjetas</span><span class="sxs-lookup"><span data-stu-id="5b61e-104">Cards Reference</span></span>

<span data-ttu-id="5b61e-105">Las tarjetas que se enumeran en esta sección se admiten en bots para Teams.</span><span class="sxs-lookup"><span data-stu-id="5b61e-105">The cards listed in this section are supported in bots for Teams.</span></span> <span data-ttu-id="5b61e-106">Se basan en tarjetas definidas por el marco de bot, pero Microsoft Teams no admite todas las tarjetas del marco de trabajo de Bot y ha agregado algunas de ellas.</span><span class="sxs-lookup"><span data-stu-id="5b61e-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span> <span data-ttu-id="5b61e-107">Las diferencias se denominan en las siguientes referencias.</span><span class="sxs-lookup"><span data-stu-id="5b61e-107">Differences are called out in the references below.</span></span>

## <a name="card-examples"></a><span data-ttu-id="5b61e-108">Ejemplos de tarjetas</span><span class="sxs-lookup"><span data-stu-id="5b61e-108">Card examples</span></span>

<span data-ttu-id="5b61e-109">Puede encontrar información adicional sobre cómo usar las tarjetas en la documentación del SDK de bot Builder (V3).</span><span class="sxs-lookup"><span data-stu-id="5b61e-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK (v3).</span></span> <span data-ttu-id="5b61e-110">También hay ejemplos de código disponibles en el repositorio Microsoft/BotBuilder-samples en GitHub.</span><span class="sxs-lookup"><span data-stu-id="5b61e-110">There are also code samples available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="5b61e-111">.NET</span><span class="sxs-lookup"><span data-stu-id="5b61e-111">.NET</span></span>
  * [<span data-ttu-id="5b61e-112">Agregar tarjetas como datos adjuntos a los mensajes</span><span class="sxs-lookup"><span data-stu-id="5b61e-112">Add cards as attachments to messages</span></span>](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [<span data-ttu-id="5b61e-113">Código de ejemplo de tarjetas (bot Builder V3)</span><span class="sxs-lookup"><span data-stu-id="5b61e-113">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* <span data-ttu-id="5b61e-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="5b61e-114">Node.js</span></span>
  * [<span data-ttu-id="5b61e-115">Agregar tarjetas como datos adjuntos a los mensajes</span><span class="sxs-lookup"><span data-stu-id="5b61e-115">Add cards as attachments to messages</span></span>](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [<span data-ttu-id="5b61e-116">Código de ejemplo de tarjetas (bot Builder V3)</span><span class="sxs-lookup"><span data-stu-id="5b61e-116">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a><span data-ttu-id="5b61e-117">Tipos de tarjetas</span><span class="sxs-lookup"><span data-stu-id="5b61e-117">Types of cards</span></span>

<span data-ttu-id="5b61e-118">En esta tabla se muestran los tipos de tarjetas disponibles.</span><span class="sxs-lookup"><span data-stu-id="5b61e-118">This table shows the types of cards available to you.</span></span>

| <span data-ttu-id="5b61e-119">Tipo de tarjeta</span><span class="sxs-lookup"><span data-stu-id="5b61e-119">Card Type</span></span> | <span data-ttu-id="5b61e-120">Descripción</span><span class="sxs-lookup"><span data-stu-id="5b61e-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="5b61e-121">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="5b61e-121">Adaptive Card</span></span>](#adaptive-card) | <span data-ttu-id="5b61e-122">Tarjeta altamente personalizable que puede contener cualquier combinación de texto, voz, imágenes, botones y campos de entrada.</span><span class="sxs-lookup"><span data-stu-id="5b61e-122">Highly customizable card that can contain any combination of text, speech, images, buttons and input fields.</span></span> |
| [<span data-ttu-id="5b61e-123">Tarjeta Hero</span><span class="sxs-lookup"><span data-stu-id="5b61e-123">Hero Card</span></span>](#hero-card) | <span data-ttu-id="5b61e-124">Normalmente contiene una sola imagen grande, uno o más botones y una pequeña cantidad de texto.</span><span class="sxs-lookup"><span data-stu-id="5b61e-124">Typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="5b61e-125">Tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="5b61e-125">List Card</span></span>](#list-card) | <span data-ttu-id="5b61e-126">Una lista de desplazamiento de elementos.</span><span class="sxs-lookup"><span data-stu-id="5b61e-126">A scrolling list of items.</span></span> |
| [<span data-ttu-id="5b61e-127">Tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="5b61e-127">Office 365 Connector Card</span></span>](#office-365-connector-card) | <span data-ttu-id="5b61e-128">Diseño flexible con varias secciones, campos, imágenes y acciones.</span><span class="sxs-lookup"><span data-stu-id="5b61e-128">Flexible layout with multiple sections, fields, images and actions.</span></span> |
| [<span data-ttu-id="5b61e-129">Tarjeta de recepción</span><span class="sxs-lookup"><span data-stu-id="5b61e-129">Receipt Card</span></span>](#receipt-card) | <span data-ttu-id="5b61e-130">Proporciona una confirmación al usuario.</span><span class="sxs-lookup"><span data-stu-id="5b61e-130">Provides a receipt to the user.</span></span> |
| [<span data-ttu-id="5b61e-131">Tarjeta de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="5b61e-131">Signin Card</span></span>](#signin-card) | <span data-ttu-id="5b61e-132">Permite que un bot solicite que un usuario inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="5b61e-132">Enables a bot to request that a user sign in.</span></span> |
| [<span data-ttu-id="5b61e-133">Tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="5b61e-133">Thumbnail Card</span></span>](#thumbnail-card) | <span data-ttu-id="5b61e-134">Normalmente contiene una sola imagen en miniatura, un texto breve y uno o más botones.</span><span class="sxs-lookup"><span data-stu-id="5b61e-134">Typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="5b61e-135">Colecciones de tarjetas</span><span class="sxs-lookup"><span data-stu-id="5b61e-135">Card Collections</span></span>](#card-collections) | <span data-ttu-id="5b61e-136">Se usa para devolver varios elementos en una sola respuesta</span><span class="sxs-lookup"><span data-stu-id="5b61e-136">Used to return multiple items in a single response</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="5b61e-137">Propiedades comunes de todas las tarjetas</span><span class="sxs-lookup"><span data-stu-id="5b61e-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="5b61e-138">Imágenes de tarjetas en línea</span><span class="sxs-lookup"><span data-stu-id="5b61e-138">Inline card images</span></span>

<span data-ttu-id="5b61e-139">La tarjeta puede contener una imagen incorporada incluyendo un vínculo a la imagen disponible públicamente.</span><span class="sxs-lookup"><span data-stu-id="5b61e-139">Your card can contain an inline image by including a link to your publicly available image.</span></span> <span data-ttu-id="5b61e-140">Por motivos de rendimiento, se recomienda hospedar la imagen en una red de entrega de contenido (CDN) pública.</span><span class="sxs-lookup"><span data-stu-id="5b61e-140">For performance purposes we highly recommend you host your image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="5b61e-141">Las imágenes se escalan hacia arriba o hacia abajo en el tamaño, a la vez que mantienen la relación de aspecto para cubrir el área de la imagen y, a continuación, se cortan del centro para obtener la relación de aspecto adecuada para la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="5b61e-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area, and then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="5b61e-142">Las imágenes deben ser como máximo 1024 × 1024 y 1 MB en formato PNG, JPEG o GIF; GIF animado no es compatible oficialmente.</span><span class="sxs-lookup"><span data-stu-id="5b61e-142">Images must be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not officially supported.</span></span>

| <span data-ttu-id="5b61e-143">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5b61e-143">Property</span></span> | <span data-ttu-id="5b61e-144">Tipo</span><span class="sxs-lookup"><span data-stu-id="5b61e-144">Type</span></span>  | <span data-ttu-id="5b61e-145">Descripción</span><span class="sxs-lookup"><span data-stu-id="5b61e-145">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5b61e-146">url</span><span class="sxs-lookup"><span data-stu-id="5b61e-146">url</span></span> | <span data-ttu-id="5b61e-147">URL</span><span class="sxs-lookup"><span data-stu-id="5b61e-147">URL</span></span> | <span data-ttu-id="5b61e-148">Dirección URL HTTPS a la imagen</span><span class="sxs-lookup"><span data-stu-id="5b61e-148">HTTPS URL to the image</span></span> |
| <span data-ttu-id="5b61e-149">alt</span><span class="sxs-lookup"><span data-stu-id="5b61e-149">alt</span></span> | <span data-ttu-id="5b61e-150">Cadena</span><span class="sxs-lookup"><span data-stu-id="5b61e-150">String</span></span> | <span data-ttu-id="5b61e-151">Descripción accesible de la imagen</span><span class="sxs-lookup"><span data-stu-id="5b61e-151">Accessible description of the image</span></span> |

### <a name="buttons"></a><span data-ttu-id="5b61e-152">Botones</span><span class="sxs-lookup"><span data-stu-id="5b61e-152">Buttons</span></span>

<span data-ttu-id="5b61e-153">Los botones se muestran apilados en la parte inferior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="5b61e-153">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="5b61e-154">El texto del botón siempre está en una sola línea y se truncará si el texto supera el ancho del botón.</span><span class="sxs-lookup"><span data-stu-id="5b61e-154">Button text is always on a single line and will be truncated if the text exceeds the button width.</span></span> <span data-ttu-id="5b61e-155">No se mostrarán los botones adicionales que superen el número máximo que admite la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="5b61e-155">Any additional buttons beyond the maximum number supported by the card will not be shown.</span></span>

<span data-ttu-id="5b61e-156">Consulte [acciones](~/task-modules-and-cards/cards/cards-actions.md) de la tarjeta para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="5b61e-156">See [Card Actions](~/task-modules-and-cards/cards/cards-actions.md) for more information.</span></span>

### <a name="card-formatting"></a><span data-ttu-id="5b61e-157">Formato de tarjeta</span><span class="sxs-lookup"><span data-stu-id="5b61e-157">Card Formatting</span></span>

<span data-ttu-id="5b61e-158">Vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md) para obtener más información sobre el formato del texto en las tarjetas.</span><span class="sxs-lookup"><span data-stu-id="5b61e-158">See [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for more information on text formatting in cards.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="5b61e-159">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="5b61e-159">Adaptive card</span></span>

<span data-ttu-id="5b61e-160">Una tarjeta personalizable que puede contener cualquier combinación de texto, voz, imágenes, botones y campos de entrada.</span><span class="sxs-lookup"><span data-stu-id="5b61e-160">A customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="5b61e-161">*Vea* [tarjetas adaptables v 1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="5b61e-161">*See* [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="5b61e-162">Compatibilidad con tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="5b61e-162">Support for Adaptive cards</span></span>

| <span data-ttu-id="5b61e-163">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="5b61e-163">Bots in Teams</span></span> | <span data-ttu-id="5b61e-164">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="5b61e-164">Messaging Extensions</span></span>  | <span data-ttu-id="5b61e-165">Conectores</span><span class="sxs-lookup"><span data-stu-id="5b61e-165">Connectors</span></span> | <span data-ttu-id="5b61e-166">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="5b61e-166">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5b61e-167">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-167">✔</span></span> | <span data-ttu-id="5b61e-168">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-168">✔</span></span> | <span data-ttu-id="5b61e-169">✖</span><span class="sxs-lookup"><span data-stu-id="5b61e-169">✖</span></span> | <span data-ttu-id="5b61e-170">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-170">✔</span></span> |
|

> [!NOTE]
> <span data-ttu-id="5b61e-171">Actualmente, los elementos multimedia no se admiten en las tarjetas adaptables v 1.2 en la plataforma de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="5b61e-171">Media elements are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>

### <a name="example-adaptive-card"></a><span data-ttu-id="5b61e-172">Tarjeta adaptable de ejemplo</span><span class="sxs-lookup"><span data-stu-id="5b61e-172">Example Adaptive card</span></span>

![Ejemplo de tarjeta de tarjeta adaptable](~/assets/images/cards/adaptivecard.png)

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

#### <a name="for-more-information-on-adaptive-cards"></a><span data-ttu-id="5b61e-174">Para obtener más información sobre las tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="5b61e-174">For more information on Adaptive cards</span></span>

* [<span data-ttu-id="5b61e-175">Introducción a las tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="5b61e-175">Adaptive Cards Overview</span></span>](/adaptive-cards/)
* [<span data-ttu-id="5b61e-176">Acciones de tarjeta adaptable en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="5b61e-176">Adaptive card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a><span data-ttu-id="5b61e-177">Tarjeta Hero</span><span class="sxs-lookup"><span data-stu-id="5b61e-177">Hero card</span></span>

<span data-ttu-id="5b61e-178">Una tarjeta que normalmente contiene una sola imagen grande, uno o más botones y texto.</span><span class="sxs-lookup"><span data-stu-id="5b61e-178">A card that typically contains a single large image, one or more buttons and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="5b61e-179">Soporte para tarjetas de héroe</span><span class="sxs-lookup"><span data-stu-id="5b61e-179">Support for Hero cards</span></span>

| <span data-ttu-id="5b61e-180">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="5b61e-180">Bots in Teams</span></span> | <span data-ttu-id="5b61e-181">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="5b61e-181">Messaging Extensions</span></span>  | <span data-ttu-id="5b61e-182">Conectores</span><span class="sxs-lookup"><span data-stu-id="5b61e-182">Connectors</span></span> | <span data-ttu-id="5b61e-183">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="5b61e-183">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5b61e-184">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-184">✔</span></span> | <span data-ttu-id="5b61e-185">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-185">✔</span></span> | <span data-ttu-id="5b61e-186">✖</span><span class="sxs-lookup"><span data-stu-id="5b61e-186">✖</span></span> | <span data-ttu-id="5b61e-187">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-187">✔</span></span> |
|

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="5b61e-188">Propiedades de una tarjeta Hero</span><span class="sxs-lookup"><span data-stu-id="5b61e-188">Properties of a Hero card</span></span>

| <span data-ttu-id="5b61e-189">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5b61e-189">Property</span></span> | <span data-ttu-id="5b61e-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="5b61e-190">Type</span></span>  | <span data-ttu-id="5b61e-191">Description</span><span class="sxs-lookup"><span data-stu-id="5b61e-191">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5b61e-192">title</span><span class="sxs-lookup"><span data-stu-id="5b61e-192">title</span></span> | <span data-ttu-id="5b61e-193">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="5b61e-193">Rich text</span></span> | <span data-ttu-id="5b61e-194">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="5b61e-194">Title of the card.</span></span> <span data-ttu-id="5b61e-195">2 líneas como máximo; formato no compatible actualmente</span><span class="sxs-lookup"><span data-stu-id="5b61e-195">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="5b61e-196">subtítulo</span><span class="sxs-lookup"><span data-stu-id="5b61e-196">subtitle</span></span> | <span data-ttu-id="5b61e-197">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="5b61e-197">Rich text</span></span> | <span data-ttu-id="5b61e-198">Subtítulo de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="5b61e-198">Subtitle of the card.</span></span> <span data-ttu-id="5b61e-199">2 líneas como máximo; formato no compatible actualmente</span><span class="sxs-lookup"><span data-stu-id="5b61e-199">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="5b61e-200">text</span><span class="sxs-lookup"><span data-stu-id="5b61e-200">text</span></span> | <span data-ttu-id="5b61e-201">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="5b61e-201">Rich text</span></span> | <span data-ttu-id="5b61e-202">El texto aparece justo debajo del subtítulo; ver el formato de la [tarjeta](~/task-modules-and-cards/cards/cards-format.md) para las opciones de formato</span><span class="sxs-lookup"><span data-stu-id="5b61e-202">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="5b61e-203">incluidas</span><span class="sxs-lookup"><span data-stu-id="5b61e-203">images</span></span> | <span data-ttu-id="5b61e-204">Matriz de imágenes</span><span class="sxs-lookup"><span data-stu-id="5b61e-204">Array of images</span></span> | <span data-ttu-id="5b61e-205">Imagen que se muestra en la parte superior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="5b61e-205">Image displayed at top of card.</span></span> <span data-ttu-id="5b61e-206">Relación de aspecto 16:9</span><span class="sxs-lookup"><span data-stu-id="5b61e-206">Aspect ratio 16:9</span></span> |
| <span data-ttu-id="5b61e-207">situados</span><span class="sxs-lookup"><span data-stu-id="5b61e-207">buttons</span></span> | <span data-ttu-id="5b61e-208">Matriz de objetos Action</span><span class="sxs-lookup"><span data-stu-id="5b61e-208">Array of action objects</span></span> | <span data-ttu-id="5b61e-209">Conjunto de acciones que se aplican a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="5b61e-209">Set of actions applicable to the current card.</span></span> <span data-ttu-id="5b61e-210">Máximo de 6</span><span class="sxs-lookup"><span data-stu-id="5b61e-210">Maximum 6</span></span> |
| <span data-ttu-id="5b61e-211">toque</span><span class="sxs-lookup"><span data-stu-id="5b61e-211">tap</span></span> | <span data-ttu-id="5b61e-212">Action (objeto)</span><span class="sxs-lookup"><span data-stu-id="5b61e-212">Action object</span></span> | <span data-ttu-id="5b61e-213">Esta acción se activará cuando el usuario pulse en la tarjeta</span><span class="sxs-lookup"><span data-stu-id="5b61e-213">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-hero-card"></a><span data-ttu-id="5b61e-214">Ejemplo de tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="5b61e-214">Example Hero card</span></span>

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

### <a name="for-more-information-on-hero-cards"></a><span data-ttu-id="5b61e-216">Para obtener más información sobre las tarjetas de Heroes</span><span class="sxs-lookup"><span data-stu-id="5b61e-216">For more information on Hero cards</span></span>

<span data-ttu-id="5b61e-217">Referencia de la estructura de bot:</span><span class="sxs-lookup"><span data-stu-id="5b61e-217">Bot Framework reference:</span></span>

* [<span data-ttu-id="5b61e-218">Nodo de tarjeta Hero</span><span class="sxs-lookup"><span data-stu-id="5b61e-218">Hero card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [<span data-ttu-id="5b61e-219">Tarjeta de héroe C #</span><span class="sxs-lookup"><span data-stu-id="5b61e-219">Hero card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0)

## <a name="list-card"></a><span data-ttu-id="5b61e-220">Tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="5b61e-220">List card</span></span>

<span data-ttu-id="5b61e-221">La tarjeta de lista se ha agregado por Microsoft Teams para proporcionar funciones que van más allá de lo que la colección de lista puede proporcionar.</span><span class="sxs-lookup"><span data-stu-id="5b61e-221">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="5b61e-222">La tarjeta de lista proporciona una lista desplazable de elementos.</span><span class="sxs-lookup"><span data-stu-id="5b61e-222">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="5b61e-223">Compatibilidad con tarjetas de lista</span><span class="sxs-lookup"><span data-stu-id="5b61e-223">Support for List cards</span></span>

| <span data-ttu-id="5b61e-224">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="5b61e-224">Bots in Teams</span></span> | <span data-ttu-id="5b61e-225">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="5b61e-225">Messaging Extensions</span></span>  | <span data-ttu-id="5b61e-226">Conectores</span><span class="sxs-lookup"><span data-stu-id="5b61e-226">Connectors</span></span> | <span data-ttu-id="5b61e-227">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="5b61e-227">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5b61e-228">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-228">✔</span></span> | <span data-ttu-id="5b61e-229">✖</span><span class="sxs-lookup"><span data-stu-id="5b61e-229">✖</span></span> | <span data-ttu-id="5b61e-230">✖</span><span class="sxs-lookup"><span data-stu-id="5b61e-230">✖</span></span> |<span data-ttu-id="5b61e-231">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-231">✔</span></span> |
|

### <a name="properties-of-a-list-card"></a><span data-ttu-id="5b61e-232">Propiedades de una tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="5b61e-232">Properties of a List card</span></span>

| <span data-ttu-id="5b61e-233">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5b61e-233">Property</span></span> | <span data-ttu-id="5b61e-234">Tipo</span><span class="sxs-lookup"><span data-stu-id="5b61e-234">Type</span></span>  | <span data-ttu-id="5b61e-235">Description</span><span class="sxs-lookup"><span data-stu-id="5b61e-235">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5b61e-236">title</span><span class="sxs-lookup"><span data-stu-id="5b61e-236">title</span></span> | <span data-ttu-id="5b61e-237">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="5b61e-237">Rich text</span></span> | <span data-ttu-id="5b61e-238">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="5b61e-238">Title of the card.</span></span> <span data-ttu-id="5b61e-239">2 líneas como máximo; formato no compatible actualmente</span><span class="sxs-lookup"><span data-stu-id="5b61e-239">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="5b61e-240">items</span><span class="sxs-lookup"><span data-stu-id="5b61e-240">items</span></span> | <span data-ttu-id="5b61e-241">Matriz de elementos de lista</span><span class="sxs-lookup"><span data-stu-id="5b61e-241">Array of list items</span></span>  ||
| <span data-ttu-id="5b61e-242">situados</span><span class="sxs-lookup"><span data-stu-id="5b61e-242">buttons</span></span> | <span data-ttu-id="5b61e-243">Matriz de objetos Action</span><span class="sxs-lookup"><span data-stu-id="5b61e-243">Array of action objects</span></span> | <span data-ttu-id="5b61e-244">Conjunto de acciones que se aplican a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="5b61e-244">Set of actions applicable to the current card.</span></span> <span data-ttu-id="5b61e-245">Máximo 6.</span><span class="sxs-lookup"><span data-stu-id="5b61e-245">Maximum 6.</span></span> <span data-ttu-id="5b61e-246">No se representa en dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="5b61e-246">Does not render on mobile.</span></span> |
|

### <a name="example-list-card"></a><span data-ttu-id="5b61e-247">Tarjeta de lista de ejemplo</span><span class="sxs-lookup"><span data-stu-id="5b61e-247">Example List card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="5b61e-248">Tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="5b61e-248">Office 365 connector card</span></span>

<span data-ttu-id="5b61e-249">Compatible con Microsoft Teams, no con bot Framework.</span><span class="sxs-lookup"><span data-stu-id="5b61e-249">Supported in Teams, not in Bot Framework.</span></span>

<span data-ttu-id="5b61e-250">La tarjeta de conexión de Office 365 proporciona un diseño flexible con varias secciones, campos, imágenes y acciones.</span><span class="sxs-lookup"><span data-stu-id="5b61e-250">The Office 365 Connector card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="5b61e-251">Esta tarjeta encapsula una tarjeta de conector para que los bots puedan usarla.</span><span class="sxs-lookup"><span data-stu-id="5b61e-251">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="5b61e-252">Vea la sección Notas para ver las diferencias entre las tarjetas de conector y la tarjeta de O365.</span><span class="sxs-lookup"><span data-stu-id="5b61e-252">See the notes section for differences between connector cards and the O365 card.</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="5b61e-253">Compatibilidad con tarjetas de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="5b61e-253">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="5b61e-254">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="5b61e-254">Bots in Teams</span></span> | <span data-ttu-id="5b61e-255">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="5b61e-255">Messaging Extensions</span></span>  | <span data-ttu-id="5b61e-256">Conectores</span><span class="sxs-lookup"><span data-stu-id="5b61e-256">Connectors</span></span> | <span data-ttu-id="5b61e-257">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="5b61e-257">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5b61e-258">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-258">✔</span></span> | <span data-ttu-id="5b61e-259">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-259">✔</span></span> | <span data-ttu-id="5b61e-260">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-260">✔</span></span> | <span data-ttu-id="5b61e-261">✖</span><span class="sxs-lookup"><span data-stu-id="5b61e-261">✖</span></span> |
|

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="5b61e-262">Propiedades de la tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="5b61e-262">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="5b61e-263">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5b61e-263">Property</span></span> | <span data-ttu-id="5b61e-264">Tipo</span><span class="sxs-lookup"><span data-stu-id="5b61e-264">Type</span></span>  | <span data-ttu-id="5b61e-265">Description</span><span class="sxs-lookup"><span data-stu-id="5b61e-265">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5b61e-266">title</span><span class="sxs-lookup"><span data-stu-id="5b61e-266">title</span></span> | <span data-ttu-id="5b61e-267">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="5b61e-267">Rich text</span></span> | <span data-ttu-id="5b61e-268">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="5b61e-268">Title of the card.</span></span> <span data-ttu-id="5b61e-269">2 líneas como máximo; formato no compatible actualmente</span><span class="sxs-lookup"><span data-stu-id="5b61e-269">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="5b61e-270">summary</span><span class="sxs-lookup"><span data-stu-id="5b61e-270">summary</span></span> | <span data-ttu-id="5b61e-271">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="5b61e-271">Rich text</span></span> | <span data-ttu-id="5b61e-272">Resumen de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="5b61e-272">Summary of the card.</span></span> <span data-ttu-id="5b61e-273">2 líneas como máximo; formato no compatible actualmente</span><span class="sxs-lookup"><span data-stu-id="5b61e-273">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="5b61e-274">text</span><span class="sxs-lookup"><span data-stu-id="5b61e-274">text</span></span> | <span data-ttu-id="5b61e-275">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="5b61e-275">Rich text</span></span> | <span data-ttu-id="5b61e-276">El texto aparece justo debajo del subtítulo; ver el formato de la [tarjeta](~/task-modules-and-cards/cards/cards-format.md) para las opciones de formato</span><span class="sxs-lookup"><span data-stu-id="5b61e-276">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="5b61e-277">themeColor</span><span class="sxs-lookup"><span data-stu-id="5b61e-277">themeColor</span></span> | <span data-ttu-id="5b61e-278">Cadena hexadecimal</span><span class="sxs-lookup"><span data-stu-id="5b61e-278">HEX string</span></span> | <span data-ttu-id="5b61e-279">color que reemplaza a la accentColor proporcionada desde el manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="5b61e-279">color that overrides the accentColor provided from the application manifest</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="5b61e-280">Notas en la tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="5b61e-280">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="5b61e-281">Las tarjetas de conexión de Office 365 funcionan correctamente en Microsoft Teams, incluidas [las acciones ActionCard](/outlook/actionable-messages/card-reference#actioncard-action).</span><span class="sxs-lookup"><span data-stu-id="5b61e-281">Office 365 Connector cards function properly on Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="5b61e-282">Una diferencia importante entre el uso de tarjetas conectoras de un conector y el uso de tarjetas conector en el bot es el control de las acciones de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="5b61e-282">One important difference between using Connector cards from a Connector and using Connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="5b61e-283">Para un conector, el extremo recibe la carga de la tarjeta a través de HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="5b61e-283">For a Connector, the endpoint receives the card payload via HTTP POST.</span></span>
* <span data-ttu-id="5b61e-284">Para un bot, la `HttpPOST` acción desencadena una `invoke` actividad que envía sólo el identificador y el cuerpo de la acción al bot.</span><span class="sxs-lookup"><span data-stu-id="5b61e-284">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="5b61e-285">Cada tarjeta de conector puede mostrar un máximo de 10 secciones y cada sección puede contener un máximo de 5 imágenes y 5 acciones.</span><span class="sxs-lookup"><span data-stu-id="5b61e-285">Each Connector card can display a maximum of 10 sections, and each section can contain a maximum of 5 images and 5 actions.</span></span>

> [!NOTE]
> <span data-ttu-id="5b61e-286">No se mostrarán secciones, imágenes o acciones adicionales en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="5b61e-286">Any additional sections, images, or actions in a message will not appear.</span></span>

<span data-ttu-id="5b61e-287">Todos los campos de texto admiten Markdown y HTML.</span><span class="sxs-lookup"><span data-stu-id="5b61e-287">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="5b61e-288">Puede controlar qué secciones utilizan Markdown o HTML estableciendo la `markdown` propiedad en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="5b61e-288">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="5b61e-289">De forma predeterminada, `markdown` se establece en `true` ; si desea usar HTML en su lugar, establezca `markdown` en `false` .</span><span class="sxs-lookup"><span data-stu-id="5b61e-289">By default, `markdown` is set to `true`; if you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="5b61e-290">Si especifica la `themeColor` propiedad, esta invalida la `accentColor` propiedad en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5b61e-290">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="5b61e-291">Para especificar el estilo de representación de `activityImage` , puede establecer `activityImageType` lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5b61e-291">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows.</span></span>

| <span data-ttu-id="5b61e-292">Valor</span><span class="sxs-lookup"><span data-stu-id="5b61e-292">Value</span></span> | <span data-ttu-id="5b61e-293">Descripción</span><span class="sxs-lookup"><span data-stu-id="5b61e-293">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="5b61e-294">Predeterminada se `activityImage` recortará como un círculo</span><span class="sxs-lookup"><span data-stu-id="5b61e-294">Default; `activityImage` will be cropped as a circle</span></span> |
| `article` | <span data-ttu-id="5b61e-295">`activityImage`se mostrará como un rectángulo y conservará su relación de aspecto.</span><span class="sxs-lookup"><span data-stu-id="5b61e-295">`activityImage` will be displayed as a rectangle and retain its aspect ratio</span></span> |

<span data-ttu-id="5b61e-296">Para obtener más información acerca de las propiedades de la tarjeta de conector, consulte la referencia de la [tarjeta de mensaje accionable](/outlook/actionable-messages/card-reference).</span><span class="sxs-lookup"><span data-stu-id="5b61e-296">For all other details about Connector card properties, see the [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="5b61e-297">Las únicas propiedades de tarjeta de conector que Microsoft Teams no admite actualmente son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="5b61e-297">The only Connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="5b61e-298">`startGroup`(se trata siempre como `true` en Microsoft Teams)</span><span class="sxs-lookup"><span data-stu-id="5b61e-298">`startGroup` (always treated as `true` in Teams)</span></span>
* `originator`
* `correlationId`

### <a name="example-office-365-connector-card"></a><span data-ttu-id="5b61e-299">Ejemplo de tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="5b61e-299">Example Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="5b61e-300">Tarjeta de recepción</span><span class="sxs-lookup"><span data-stu-id="5b61e-300">Receipt card</span></span>

<span data-ttu-id="5b61e-301">Se admite en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="5b61e-301">Supported in Teams.</span></span>

<span data-ttu-id="5b61e-302">Tarjeta que permite a un bot proporcionar una confirmación al usuario.</span><span class="sxs-lookup"><span data-stu-id="5b61e-302">A card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="5b61e-303">Normalmente, contiene la lista de elementos que se deben incluir en la recepción, la información total y fiscal y otro texto.</span><span class="sxs-lookup"><span data-stu-id="5b61e-303">It typically contains the list of items to include on the receipt, tax and total information, and other text.</span></span>

### <a name="support-for-receipts-cards"></a><span data-ttu-id="5b61e-304">Soporte para tarjetas de recepción</span><span class="sxs-lookup"><span data-stu-id="5b61e-304">Support for Receipts cards</span></span>

| <span data-ttu-id="5b61e-305">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="5b61e-305">Bots in Teams</span></span> | <span data-ttu-id="5b61e-306">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="5b61e-306">Messaging Extensions</span></span>  | <span data-ttu-id="5b61e-307">Conectores</span><span class="sxs-lookup"><span data-stu-id="5b61e-307">Connectors</span></span> | <span data-ttu-id="5b61e-308">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="5b61e-308">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5b61e-309">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-309">✔</span></span> | <span data-ttu-id="5b61e-310">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-310">✔</span></span> | <span data-ttu-id="5b61e-311">✖</span><span class="sxs-lookup"><span data-stu-id="5b61e-311">✖</span></span> | <span data-ttu-id="5b61e-312">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-312">✔</span></span> |
|

### <a name="for-more-information-on-receipt-cards"></a><span data-ttu-id="5b61e-313">Para obtener más información sobre las tarjetas de recepción</span><span class="sxs-lookup"><span data-stu-id="5b61e-313">For more information on Receipt cards</span></span>

<span data-ttu-id="5b61e-314">Referencia de la estructura de bot:</span><span class="sxs-lookup"><span data-stu-id="5b61e-314">Bot Framework reference:</span></span>

* [<span data-ttu-id="5b61e-315">Nodo tarjeta de recepción</span><span class="sxs-lookup"><span data-stu-id="5b61e-315">Receipt card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest)
* [<span data-ttu-id="5b61e-316">Tarjeta de recepción C #</span><span class="sxs-lookup"><span data-stu-id="5b61e-316">Receipt card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0)

## <a name="signin-card"></a><span data-ttu-id="5b61e-317">Tarjeta de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="5b61e-317">Signin card</span></span>

<span data-ttu-id="5b61e-318">Tarjeta que permite a un bot solicitar que un usuario inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="5b61e-318">A card that enables a bot to request that a user sign in.</span></span> <span data-ttu-id="5b61e-319">Se admite en Teams de una forma ligeramente diferente a la que se encuentra en el marco de robots.</span><span class="sxs-lookup"><span data-stu-id="5b61e-319">Supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="5b61e-320">La tarjeta de inicio de sesión de Microsoft Teams es similar a la tarjeta de inicio de sesión en el marco de bot, con la excepción de que la tarjeta de inicio de sesión de Teams solo admite dos acciones: `signin` y `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="5b61e-320">The signin card in Teams is similar to the signin card in the bot framework with the exception that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="5b61e-321">La *acción de inicio de sesión* se puede usar desde cualquier tarjeta en Teams, no solo desde la tarjeta de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="5b61e-321">The *signin action* can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="5b61e-322">Para obtener más información sobre la autenticación, vea el tema sobre el [flujo de autenticación de Microsoft Teams para bots](~/bots/how-to/authentication/auth-flow-bot.md) .</span><span class="sxs-lookup"><span data-stu-id="5b61e-322">See the topic [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md) for more details on authentication.</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="5b61e-323">Compatibilidad con tarjetas de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="5b61e-323">Support for Signin cards</span></span>

| <span data-ttu-id="5b61e-324">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="5b61e-324">Bots in Teams</span></span> | <span data-ttu-id="5b61e-325">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="5b61e-325">Messaging Extensions</span></span>  | <span data-ttu-id="5b61e-326">Conectores</span><span class="sxs-lookup"><span data-stu-id="5b61e-326">Connectors</span></span> | <span data-ttu-id="5b61e-327">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="5b61e-327">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5b61e-328">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-328">✔</span></span> | <span data-ttu-id="5b61e-329">✖</span><span class="sxs-lookup"><span data-stu-id="5b61e-329">✖</span></span> | <span data-ttu-id="5b61e-330">✖</span><span class="sxs-lookup"><span data-stu-id="5b61e-330">✖</span></span> | <span data-ttu-id="5b61e-331">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-331">✔</span></span> |
|

### <a name="for-more-information-on-signin-cards"></a><span data-ttu-id="5b61e-332">Para obtener más información sobre las tarjetas de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="5b61e-332">For more information on Signin cards</span></span>

<span data-ttu-id="5b61e-333">Referencia de la estructura de bot:</span><span class="sxs-lookup"><span data-stu-id="5b61e-333">Bot Framework reference:</span></span>

* [<span data-ttu-id="5b61e-334">Nodo de tarjeta de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="5b61e-334">Signin card Node</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest)
* [<span data-ttu-id="5b61e-335">Tarjeta de inicio de sesión C #</span><span class="sxs-lookup"><span data-stu-id="5b61e-335">Signin card C#</span></span>](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0)

## <a name="thumbnail-card"></a><span data-ttu-id="5b61e-336">Tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="5b61e-336">Thumbnail card</span></span>

<span data-ttu-id="5b61e-337">Una tarjeta que normalmente contiene una sola imagen en miniatura, uno o más botones y texto.</span><span class="sxs-lookup"><span data-stu-id="5b61e-337">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="5b61e-338">Compatibilidad con tarjetas de miniaturas</span><span class="sxs-lookup"><span data-stu-id="5b61e-338">Support for Thumbnail cards</span></span>

| <span data-ttu-id="5b61e-339">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="5b61e-339">Bots in Teams</span></span> | <span data-ttu-id="5b61e-340">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="5b61e-340">Messaging Extensions</span></span>  | <span data-ttu-id="5b61e-341">Conectores</span><span class="sxs-lookup"><span data-stu-id="5b61e-341">Connectors</span></span> | <span data-ttu-id="5b61e-342">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="5b61e-342">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5b61e-343">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-343">✔</span></span> | <span data-ttu-id="5b61e-344">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-344">✔</span></span> | <span data-ttu-id="5b61e-345">✖</span><span class="sxs-lookup"><span data-stu-id="5b61e-345">✖</span></span> | <span data-ttu-id="5b61e-346">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-346">✔</span></span> |
|

![Ejemplo de una tarjeta en miniatura](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="5b61e-348">Propiedades de una tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="5b61e-348">Properties of a Thumbnail card</span></span>

| <span data-ttu-id="5b61e-349">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5b61e-349">Property</span></span> | <span data-ttu-id="5b61e-350">Tipo</span><span class="sxs-lookup"><span data-stu-id="5b61e-350">Type</span></span>  | <span data-ttu-id="5b61e-351">Description</span><span class="sxs-lookup"><span data-stu-id="5b61e-351">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5b61e-352">title</span><span class="sxs-lookup"><span data-stu-id="5b61e-352">title</span></span> | <span data-ttu-id="5b61e-353">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="5b61e-353">Rich text</span></span> | <span data-ttu-id="5b61e-354">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="5b61e-354">Title of the card.</span></span> <span data-ttu-id="5b61e-355">2 líneas como máximo; formato no compatible actualmente</span><span class="sxs-lookup"><span data-stu-id="5b61e-355">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="5b61e-356">subtítulo</span><span class="sxs-lookup"><span data-stu-id="5b61e-356">subtitle</span></span> | <span data-ttu-id="5b61e-357">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="5b61e-357">Rich text</span></span> | <span data-ttu-id="5b61e-358">Subtítulo de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="5b61e-358">Subtitle of the card.</span></span> <span data-ttu-id="5b61e-359">2 líneas como máximo; formato no compatible actualmente</span><span class="sxs-lookup"><span data-stu-id="5b61e-359">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="5b61e-360">text</span><span class="sxs-lookup"><span data-stu-id="5b61e-360">text</span></span> | <span data-ttu-id="5b61e-361">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="5b61e-361">Rich text</span></span> | <span data-ttu-id="5b61e-362">El texto aparece justo debajo del subtítulo; ver el formato de la [tarjeta](~/task-modules-and-cards/cards/cards-format.md) para las opciones de formato</span><span class="sxs-lookup"><span data-stu-id="5b61e-362">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="5b61e-363">incluidas</span><span class="sxs-lookup"><span data-stu-id="5b61e-363">images</span></span> | <span data-ttu-id="5b61e-364">Matriz de imágenes</span><span class="sxs-lookup"><span data-stu-id="5b61e-364">Array of images</span></span> | <span data-ttu-id="5b61e-365">Imagen que se muestra en la parte superior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="5b61e-365">Image displayed at top of card.</span></span> <span data-ttu-id="5b61e-366">Relación de aspecto 1:1 (cuadrado)</span><span class="sxs-lookup"><span data-stu-id="5b61e-366">Aspect ratio 1:1 (square)</span></span> |
| <span data-ttu-id="5b61e-367">situados</span><span class="sxs-lookup"><span data-stu-id="5b61e-367">buttons</span></span> | <span data-ttu-id="5b61e-368">Matriz de objetos Action</span><span class="sxs-lookup"><span data-stu-id="5b61e-368">Array of action objects</span></span> | <span data-ttu-id="5b61e-369">Conjunto de acciones que se aplican a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="5b61e-369">Set of actions applicable to the current card.</span></span> <span data-ttu-id="5b61e-370">Máximo de 6</span><span class="sxs-lookup"><span data-stu-id="5b61e-370">Maximum 6</span></span> |
| <span data-ttu-id="5b61e-371">toque</span><span class="sxs-lookup"><span data-stu-id="5b61e-371">tap</span></span> | <span data-ttu-id="5b61e-372">Action (objeto)</span><span class="sxs-lookup"><span data-stu-id="5b61e-372">Action object</span></span> | <span data-ttu-id="5b61e-373">Esta acción se activará cuando el usuario pulse en la tarjeta</span><span class="sxs-lookup"><span data-stu-id="5b61e-373">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-thumbnail-card"></a><span data-ttu-id="5b61e-374">Tarjeta de miniaturas de ejemplo</span><span class="sxs-lookup"><span data-stu-id="5b61e-374">Example Thumbnail card</span></span>

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

### <a name="for-more-information"></a><span data-ttu-id="5b61e-375">Más información</span><span class="sxs-lookup"><span data-stu-id="5b61e-375">For more information</span></span>

<span data-ttu-id="5b61e-376">Referencia de la estructura de bot:</span><span class="sxs-lookup"><span data-stu-id="5b61e-376">Bot Framework reference:</span></span>

* [<span data-ttu-id="5b61e-377">Nodo de tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="5b61e-377">Thumbnail card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest)
* [<span data-ttu-id="5b61e-378">Tarjeta en miniatura C #</span><span class="sxs-lookup"><span data-stu-id="5b61e-378">Thumbnail card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0)

## <a name="card-collections"></a><span data-ttu-id="5b61e-379">Colecciones de tarjetas</span><span class="sxs-lookup"><span data-stu-id="5b61e-379">Card collections</span></span>

<span data-ttu-id="5b61e-380">Las colecciones de tarjetas se admiten en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="5b61e-380">Card collections are supported in Teams.</span></span>

<span data-ttu-id="5b61e-381">Las colecciones de tarjetas las proporciona el marco de bot: `builder.AttachmentLayout.carousel` y `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="5b61e-381">Card collections are provided by the Bot Framework: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="5b61e-382">Estas colecciones pueden contener tarjetas adaptables, de héroe o de miniaturas.</span><span class="sxs-lookup"><span data-stu-id="5b61e-382">These collections can contain Adaptive, Hero, or Thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="5b61e-383">Colección carrusel</span><span class="sxs-lookup"><span data-stu-id="5b61e-383">Carousel collection</span></span>

<span data-ttu-id="5b61e-384">El [diseño carrusel](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0) muestra un carrusel de tarjetas, opcionalmente con botones de acción asociados.</span><span class="sxs-lookup"><span data-stu-id="5b61e-384">The [carousel layout](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="5b61e-385">Compatibilidad con colecciones de carrusel</span><span class="sxs-lookup"><span data-stu-id="5b61e-385">Support for Carousel collections</span></span>

| <span data-ttu-id="5b61e-386">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="5b61e-386">Bots in Teams</span></span> | <span data-ttu-id="5b61e-387">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="5b61e-387">Messaging Extensions</span></span>  | <span data-ttu-id="5b61e-388">Conectores</span><span class="sxs-lookup"><span data-stu-id="5b61e-388">Connectors</span></span> | <span data-ttu-id="5b61e-389">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="5b61e-389">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5b61e-390">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-390">✔</span></span> | <span data-ttu-id="5b61e-391">✖</span><span class="sxs-lookup"><span data-stu-id="5b61e-391">✖</span></span> | <span data-ttu-id="5b61e-392">✖</span><span class="sxs-lookup"><span data-stu-id="5b61e-392">✖</span></span> | <span data-ttu-id="5b61e-393">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-393">✔</span></span> |
|

> [!NOTE]
> <span data-ttu-id="5b61e-394">Un carrusel puede mostrar un máximo de 10 tarjetas por mensaje.</span><span class="sxs-lookup"><span data-stu-id="5b61e-394">A carousel can display a maximum of 10 cards per message.</span></span>

### <a name="example-carousel-collection"></a><span data-ttu-id="5b61e-395">Colección de carrusel de ejemplo</span><span class="sxs-lookup"><span data-stu-id="5b61e-395">Example Carousel collection</span></span>

![Ejemplo de un carrusel de tarjetas](~/assets/images/cards/carousel.png)

<span data-ttu-id="5b61e-397">Las propiedades son las mismas que para el héroe o la tarjeta en miniatura.</span><span class="sxs-lookup"><span data-stu-id="5b61e-397">Properties are the same as for the hero or thumbnail card.</span></span>

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="5b61e-398">Sintaxis para colecciones de carrusel</span><span class="sxs-lookup"><span data-stu-id="5b61e-398">Syntax for Carousel collections</span></span>

`builder.AttachmentLayout.carousel`

## <a name="list-collection"></a><span data-ttu-id="5b61e-399">Colección List</span><span class="sxs-lookup"><span data-stu-id="5b61e-399">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="5b61e-400">Compatibilidad con colecciones de listas</span><span class="sxs-lookup"><span data-stu-id="5b61e-400">Support for List collections</span></span>

<span data-ttu-id="5b61e-401">El diseño de lista muestra una lista apilada verticalmente de tarjetas, opcionalmente con botones de acción asociados.</span><span class="sxs-lookup"><span data-stu-id="5b61e-401">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="5b61e-402">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="5b61e-402">Bots in Teams</span></span> | <span data-ttu-id="5b61e-403">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="5b61e-403">Messaging Extensions</span></span>  | <span data-ttu-id="5b61e-404">Conectores</span><span class="sxs-lookup"><span data-stu-id="5b61e-404">Connectors</span></span> | <span data-ttu-id="5b61e-405">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="5b61e-405">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5b61e-406">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-406">✔</span></span> | <span data-ttu-id="5b61e-407">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-407">✔</span></span> | <span data-ttu-id="5b61e-408">✖</span><span class="sxs-lookup"><span data-stu-id="5b61e-408">✖</span></span> | <span data-ttu-id="5b61e-409">✔</span><span class="sxs-lookup"><span data-stu-id="5b61e-409">✔</span></span> |
|

### <a name="example-list-collection"></a><span data-ttu-id="5b61e-410">Colección de lista de ejemplo</span><span class="sxs-lookup"><span data-stu-id="5b61e-410">Example List collection</span></span>

![Ejemplo de una lista de tarjetas](~/assets/images/cards/list.png)

<span data-ttu-id="5b61e-412">Las propiedades son las mismas que para el héroe o la tarjeta en miniatura.</span><span class="sxs-lookup"><span data-stu-id="5b61e-412">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="5b61e-413">Una lista puede mostrar un máximo de 10 tarjetas por mensaje.</span><span class="sxs-lookup"><span data-stu-id="5b61e-413">A list can display a maximum of 10 cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="5b61e-414">Algunas combinaciones de tarjetas de lista aún no se admiten en iOS y Android.</span><span class="sxs-lookup"><span data-stu-id="5b61e-414">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="5b61e-415">Sintaxis para colecciones de listas</span><span class="sxs-lookup"><span data-stu-id="5b61e-415">Syntax for List collections</span></span>

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="5b61e-416">Tarjetas no admitidas en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="5b61e-416">Cards not supported in Teams</span></span>

<span data-ttu-id="5b61e-417">El marco de bot implementa las siguientes tarjetas, pero no son compatibles con Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="5b61e-417">The following cards are implemented by the Bot Framework, but are NOT supported by Teams.</span></span>

* <span data-ttu-id="5b61e-418">Tarjetas de animación</span><span class="sxs-lookup"><span data-stu-id="5b61e-418">Animation cards</span></span>
* <span data-ttu-id="5b61e-419">Tarjetas de audio</span><span class="sxs-lookup"><span data-stu-id="5b61e-419">Audio cards</span></span>
* <span data-ttu-id="5b61e-420">Tarjetas de vídeo</span><span class="sxs-lookup"><span data-stu-id="5b61e-420">Video cards</span></span>

---
title: Referencia de tarjetas
description: Describe todas las tarjetas y acciones de tarjeta disponibles para bots en Teams
keywords: Referencia de las tarjetas bots
ms.openlocfilehash: 22a4faa932173387cbefe900e30106d063c49e50
ms.sourcegitcommit: 5739245903278d521ec920427248b6b48676e637
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/07/2021
ms.locfileid: "49778397"
---
# <a name="cards-reference"></a><span data-ttu-id="582db-104">Referencia de tarjetas</span><span class="sxs-lookup"><span data-stu-id="582db-104">Cards Reference</span></span>

<span data-ttu-id="582db-105">Las tarjetas que se enumeran en esta sección son compatibles con bots para Teams.</span><span class="sxs-lookup"><span data-stu-id="582db-105">The cards listed in this section are supported in bots for Teams.</span></span> <span data-ttu-id="582db-106">Se basan en tarjetas definidas por Bot Framework, pero Teams no admite todas las tarjetas de Bot Framework y ha agregado algunas de sus propias tarjetas.</span><span class="sxs-lookup"><span data-stu-id="582db-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span> <span data-ttu-id="582db-107">Las diferencias se indican en las siguientes referencias.</span><span class="sxs-lookup"><span data-stu-id="582db-107">Differences are called out in the references below.</span></span>

## <a name="card-examples"></a><span data-ttu-id="582db-108">Ejemplos de tarjetas</span><span class="sxs-lookup"><span data-stu-id="582db-108">Card examples</span></span>

<span data-ttu-id="582db-109">Puede encontrar información adicional sobre cómo usar tarjetas en la documentación del SDK de Bot Builder (v3).</span><span class="sxs-lookup"><span data-stu-id="582db-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK (v3).</span></span> <span data-ttu-id="582db-110">También hay ejemplos de código disponibles en el repositorio de Microsoft/BotBuilder-Samples en GitHub.</span><span class="sxs-lookup"><span data-stu-id="582db-110">There are also code samples available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="582db-111">.NET</span><span class="sxs-lookup"><span data-stu-id="582db-111">.NET</span></span>
  * [<span data-ttu-id="582db-112">Agregar tarjetas como datos adjuntos a los mensajes</span><span class="sxs-lookup"><span data-stu-id="582db-112">Add cards as attachments to messages</span></span>](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [<span data-ttu-id="582db-113">Código de ejemplo de tarjetas (Bot Builder v3)</span><span class="sxs-lookup"><span data-stu-id="582db-113">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* <span data-ttu-id="582db-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="582db-114">Node.js</span></span>
  * [<span data-ttu-id="582db-115">Agregar tarjetas como datos adjuntos a los mensajes</span><span class="sxs-lookup"><span data-stu-id="582db-115">Add cards as attachments to messages</span></span>](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [<span data-ttu-id="582db-116">Código de ejemplo de tarjetas (Bot Builder v3)</span><span class="sxs-lookup"><span data-stu-id="582db-116">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a><span data-ttu-id="582db-117">Tipos de tarjetas</span><span class="sxs-lookup"><span data-stu-id="582db-117">Types of cards</span></span>

<span data-ttu-id="582db-118">En esta tabla se muestran los tipos de tarjetas disponibles.</span><span class="sxs-lookup"><span data-stu-id="582db-118">This table shows the types of cards available to you.</span></span>

| <span data-ttu-id="582db-119">Tipo de tarjeta</span><span class="sxs-lookup"><span data-stu-id="582db-119">Card Type</span></span> | <span data-ttu-id="582db-120">Descripción</span><span class="sxs-lookup"><span data-stu-id="582db-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="582db-121">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="582db-121">Adaptive Card</span></span>](#adaptive-card) | <span data-ttu-id="582db-122">Tarjeta altamente personalizable que puede contener cualquier combinación de texto, voz, imágenes, botones y campos de entrada.</span><span class="sxs-lookup"><span data-stu-id="582db-122">Highly customizable card that can contain any combination of text, speech, images, buttons and input fields.</span></span> |
| [<span data-ttu-id="582db-123">Tarjeta principal</span><span class="sxs-lookup"><span data-stu-id="582db-123">Hero Card</span></span>](#hero-card) | <span data-ttu-id="582db-124">Normalmente contiene una sola imagen grande, uno o más botones y una pequeña cantidad de texto.</span><span class="sxs-lookup"><span data-stu-id="582db-124">Typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="582db-125">Tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="582db-125">List Card</span></span>](#list-card) | <span data-ttu-id="582db-126">Una lista de desplazamiento de elementos.</span><span class="sxs-lookup"><span data-stu-id="582db-126">A scrolling list of items.</span></span> |
| [<span data-ttu-id="582db-127">Tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="582db-127">Office 365 Connector Card</span></span>](#office-365-connector-card) | <span data-ttu-id="582db-128">Diseño flexible con varias secciones, campos, imágenes y acciones.</span><span class="sxs-lookup"><span data-stu-id="582db-128">Flexible layout with multiple sections, fields, images and actions.</span></span> |
| [<span data-ttu-id="582db-129">Tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="582db-129">Receipt Card</span></span>](#receipt-card) | <span data-ttu-id="582db-130">Proporciona una confirmación al usuario.</span><span class="sxs-lookup"><span data-stu-id="582db-130">Provides a receipt to the user.</span></span> |
| [<span data-ttu-id="582db-131">Tarjeta de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="582db-131">Signin Card</span></span>](#signin-card) | <span data-ttu-id="582db-132">Permite que un bot solicite que un usuario inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="582db-132">Enables a bot to request that a user sign in.</span></span> |
| [<span data-ttu-id="582db-133">Tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="582db-133">Thumbnail Card</span></span>](#thumbnail-card) | <span data-ttu-id="582db-134">Normalmente contiene una sola imagen en miniatura, texto corto y uno o más botones.</span><span class="sxs-lookup"><span data-stu-id="582db-134">Typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="582db-135">Colecciones de tarjetas</span><span class="sxs-lookup"><span data-stu-id="582db-135">Card Collections</span></span>](#card-collections) | <span data-ttu-id="582db-136">Se usa para devolver varios elementos en una sola respuesta</span><span class="sxs-lookup"><span data-stu-id="582db-136">Used to return multiple items in a single response</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="582db-137">Propiedades comunes para todas las tarjetas</span><span class="sxs-lookup"><span data-stu-id="582db-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="582db-138">Imágenes de tarjetas en línea</span><span class="sxs-lookup"><span data-stu-id="582db-138">Inline card images</span></span>

<span data-ttu-id="582db-139">La tarjeta puede contener una imagen en línea incluyendo un vínculo a la imagen disponible públicamente.</span><span class="sxs-lookup"><span data-stu-id="582db-139">Your card can contain an inline image by including a link to your publicly available image.</span></span> <span data-ttu-id="582db-140">Por motivos de rendimiento, se recomienda encarecidamente hospedar la imagen en una red de entrega de contenido (CDN) pública.</span><span class="sxs-lookup"><span data-stu-id="582db-140">For performance purposes we highly recommend you host your image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="582db-141">Las imágenes se escalan hacia arriba o hacia abajo en tamaño mientras se mantiene la relación de aspecto para cubrir el área de la imagen y, a continuación, se recortan desde el centro para lograr la relación de aspecto adecuada para la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="582db-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area, and then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="582db-142">Las imágenes deben tener como máximo 1024×1024 en formato PNG, JPEG o GIF; GIF animado no se admite oficialmente.</span><span class="sxs-lookup"><span data-stu-id="582db-142">Images must be at most 1024×1024 in PNG, JPEG, or GIF format; animated GIF is not officially supported.</span></span>

| <span data-ttu-id="582db-143">Propiedad</span><span class="sxs-lookup"><span data-stu-id="582db-143">Property</span></span> | <span data-ttu-id="582db-144">Tipo</span><span class="sxs-lookup"><span data-stu-id="582db-144">Type</span></span>  | <span data-ttu-id="582db-145">Descripción</span><span class="sxs-lookup"><span data-stu-id="582db-145">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="582db-146">url</span><span class="sxs-lookup"><span data-stu-id="582db-146">url</span></span> | <span data-ttu-id="582db-147">URL</span><span class="sxs-lookup"><span data-stu-id="582db-147">URL</span></span> | <span data-ttu-id="582db-148">DIRECCIÓN URL HTTPS a la imagen</span><span class="sxs-lookup"><span data-stu-id="582db-148">HTTPS URL to the image</span></span> |
| <span data-ttu-id="582db-149">alt</span><span class="sxs-lookup"><span data-stu-id="582db-149">alt</span></span> | <span data-ttu-id="582db-150">Cadena</span><span class="sxs-lookup"><span data-stu-id="582db-150">String</span></span> | <span data-ttu-id="582db-151">Descripción accesible de la imagen</span><span class="sxs-lookup"><span data-stu-id="582db-151">Accessible description of the image</span></span> |

### <a name="buttons"></a><span data-ttu-id="582db-152">Botones</span><span class="sxs-lookup"><span data-stu-id="582db-152">Buttons</span></span>

<span data-ttu-id="582db-153">Los botones se muestran apilados en la parte inferior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="582db-153">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="582db-154">El texto del botón siempre está en una sola línea y se truncará si el texto supera el ancho del botón.</span><span class="sxs-lookup"><span data-stu-id="582db-154">Button text is always on a single line and will be truncated if the text exceeds the button width.</span></span> <span data-ttu-id="582db-155">No se mostrarán botones adicionales más allá del número máximo admitido por la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="582db-155">Any additional buttons beyond the maximum number supported by the card will not be shown.</span></span>

<span data-ttu-id="582db-156">Vea [Acciones de tarjeta](~/task-modules-and-cards/cards/cards-actions.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="582db-156">See [Card Actions](~/task-modules-and-cards/cards/cards-actions.md) for more information.</span></span>

### <a name="card-formatting"></a><span data-ttu-id="582db-157">Formato de tarjeta</span><span class="sxs-lookup"><span data-stu-id="582db-157">Card Formatting</span></span>

<span data-ttu-id="582db-158">Consulta [Formato de tarjeta para](~/task-modules-and-cards/cards/cards-format.md) obtener más información sobre el formato de texto en las tarjetas.</span><span class="sxs-lookup"><span data-stu-id="582db-158">See [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for more information on text formatting in cards.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="582db-159">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="582db-159">Adaptive card</span></span>

<span data-ttu-id="582db-160">Tarjeta personalizable que puede contener cualquier combinación de texto, voz, imágenes, botones y campos de entrada.</span><span class="sxs-lookup"><span data-stu-id="582db-160">A customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="582db-161">*Consulta* [las tarjetas adaptables v1.2.0.](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)</span><span class="sxs-lookup"><span data-stu-id="582db-161">*See* [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="582db-162">Compatibilidad con tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="582db-162">Support for Adaptive cards</span></span>

| <span data-ttu-id="582db-163">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="582db-163">Bots in Teams</span></span> | <span data-ttu-id="582db-164">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="582db-164">Messaging Extensions</span></span>  | <span data-ttu-id="582db-165">Conectores</span><span class="sxs-lookup"><span data-stu-id="582db-165">Connectors</span></span> | <span data-ttu-id="582db-166">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="582db-166">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="582db-167">✔</span><span class="sxs-lookup"><span data-stu-id="582db-167">✔</span></span> | <span data-ttu-id="582db-168">✔</span><span class="sxs-lookup"><span data-stu-id="582db-168">✔</span></span> | <span data-ttu-id="582db-169">✖</span><span class="sxs-lookup"><span data-stu-id="582db-169">✖</span></span> | <span data-ttu-id="582db-170">✔</span><span class="sxs-lookup"><span data-stu-id="582db-170">✔</span></span> |
|

> [!NOTE]
> * <span data-ttu-id="582db-171">La plataforma de Teams admite la versión 1.2 o anterior de las características de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="582db-171">Teams platform supports v1.2 or earlier of Adaptive card features.</span></span>
> * <span data-ttu-id="582db-172">Actualmente, los elementos multimedia no se admiten en la tarjeta adaptable v1.2 en la plataforma teams.</span><span class="sxs-lookup"><span data-stu-id="582db-172">Media elements are currently not supported in Adaptive card v1.2 on the Teams platform.</span></span>
### <a name="example-adaptive-card"></a><span data-ttu-id="582db-173">Ejemplo de tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="582db-173">Example Adaptive card</span></span>

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

#### <a name="for-more-information-on-adaptive-cards"></a><span data-ttu-id="582db-175">Para obtener más información sobre las tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="582db-175">For more information on Adaptive cards</span></span>

* [<span data-ttu-id="582db-176">Introducción a las tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="582db-176">Adaptive Cards Overview</span></span>](/adaptive-cards/)
* [<span data-ttu-id="582db-177">Acciones de tarjeta adaptable en Teams</span><span class="sxs-lookup"><span data-stu-id="582db-177">Adaptive card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a><span data-ttu-id="582db-178">Tarjeta principal</span><span class="sxs-lookup"><span data-stu-id="582db-178">Hero card</span></span>

<span data-ttu-id="582db-179">Una tarjeta que normalmente contiene una sola imagen grande, uno o más botones y texto.</span><span class="sxs-lookup"><span data-stu-id="582db-179">A card that typically contains a single large image, one or more buttons and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="582db-180">Compatibilidad con tarjetas hero</span><span class="sxs-lookup"><span data-stu-id="582db-180">Support for Hero cards</span></span>

| <span data-ttu-id="582db-181">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="582db-181">Bots in Teams</span></span> | <span data-ttu-id="582db-182">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="582db-182">Messaging Extensions</span></span>  | <span data-ttu-id="582db-183">Conectores</span><span class="sxs-lookup"><span data-stu-id="582db-183">Connectors</span></span> | <span data-ttu-id="582db-184">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="582db-184">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="582db-185">✔</span><span class="sxs-lookup"><span data-stu-id="582db-185">✔</span></span> | <span data-ttu-id="582db-186">✔</span><span class="sxs-lookup"><span data-stu-id="582db-186">✔</span></span> | <span data-ttu-id="582db-187">✖</span><span class="sxs-lookup"><span data-stu-id="582db-187">✖</span></span> | <span data-ttu-id="582db-188">✔</span><span class="sxs-lookup"><span data-stu-id="582db-188">✔</span></span> |
|

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="582db-189">Propiedades de una tarjeta principal</span><span class="sxs-lookup"><span data-stu-id="582db-189">Properties of a Hero card</span></span>

| <span data-ttu-id="582db-190">Propiedad</span><span class="sxs-lookup"><span data-stu-id="582db-190">Property</span></span> | <span data-ttu-id="582db-191">Tipo</span><span class="sxs-lookup"><span data-stu-id="582db-191">Type</span></span>  | <span data-ttu-id="582db-192">Description</span><span class="sxs-lookup"><span data-stu-id="582db-192">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="582db-193">title</span><span class="sxs-lookup"><span data-stu-id="582db-193">title</span></span> | <span data-ttu-id="582db-194">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="582db-194">Rich text</span></span> | <span data-ttu-id="582db-195">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="582db-195">Title of the card.</span></span> <span data-ttu-id="582db-196">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="582db-196">Maximum 2 lines.</span></span> |
| <span data-ttu-id="582db-197">subtitle</span><span class="sxs-lookup"><span data-stu-id="582db-197">subtitle</span></span> | <span data-ttu-id="582db-198">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="582db-198">Rich text</span></span> | <span data-ttu-id="582db-199">Subtítulo de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="582db-199">Subtitle of the card.</span></span> <span data-ttu-id="582db-200">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="582db-200">Maximum 2 lines.</span></span>|
| <span data-ttu-id="582db-201">text</span><span class="sxs-lookup"><span data-stu-id="582db-201">text</span></span> | <span data-ttu-id="582db-202">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="582db-202">Rich text</span></span> | <span data-ttu-id="582db-203">El texto aparece justo debajo del subtítulo; ver [Formato de tarjeta para](~/task-modules-and-cards/cards/cards-format.md) las opciones de formato</span><span class="sxs-lookup"><span data-stu-id="582db-203">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="582db-204">imágenes</span><span class="sxs-lookup"><span data-stu-id="582db-204">images</span></span> | <span data-ttu-id="582db-205">Matriz de imágenes</span><span class="sxs-lookup"><span data-stu-id="582db-205">Array of images</span></span> | <span data-ttu-id="582db-206">Imagen que se muestra en la parte superior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="582db-206">Image displayed at top of card.</span></span> <span data-ttu-id="582db-207">Relación de aspecto 16:9</span><span class="sxs-lookup"><span data-stu-id="582db-207">Aspect ratio 16:9</span></span> |
| <span data-ttu-id="582db-208">buttons</span><span class="sxs-lookup"><span data-stu-id="582db-208">buttons</span></span> | <span data-ttu-id="582db-209">Matriz de objetos de acción</span><span class="sxs-lookup"><span data-stu-id="582db-209">Array of action objects</span></span> | <span data-ttu-id="582db-210">Conjunto de acciones aplicables a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="582db-210">Set of actions applicable to the current card.</span></span> <span data-ttu-id="582db-211">Máximo 6</span><span class="sxs-lookup"><span data-stu-id="582db-211">Maximum 6</span></span> |
| <span data-ttu-id="582db-212">pulsación</span><span class="sxs-lookup"><span data-stu-id="582db-212">tap</span></span> | <span data-ttu-id="582db-213">Action (objeto)</span><span class="sxs-lookup"><span data-stu-id="582db-213">Action object</span></span> | <span data-ttu-id="582db-214">Esta acción se activará cuando el usuario pulse en la propia tarjeta.</span><span class="sxs-lookup"><span data-stu-id="582db-214">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-hero-card"></a><span data-ttu-id="582db-215">Ejemplo de tarjeta principal</span><span class="sxs-lookup"><span data-stu-id="582db-215">Example Hero card</span></span>

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

### <a name="for-more-information-on-hero-cards"></a><span data-ttu-id="582db-217">Para obtener más información sobre las tarjetas hero</span><span class="sxs-lookup"><span data-stu-id="582db-217">For more information on Hero cards</span></span>

<span data-ttu-id="582db-218">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="582db-218">Bot Framework reference:</span></span>

* [<span data-ttu-id="582db-219">Nodo de tarjeta principal</span><span class="sxs-lookup"><span data-stu-id="582db-219">Hero card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [<span data-ttu-id="582db-220">Tarjeta principal C #</span><span class="sxs-lookup"><span data-stu-id="582db-220">Hero card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="582db-221">Tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="582db-221">List card</span></span>

<span data-ttu-id="582db-222">Teams ha agregado la tarjeta de lista para proporcionar funciones más allá de lo que puede proporcionar la colección de listas.</span><span class="sxs-lookup"><span data-stu-id="582db-222">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="582db-223">La tarjeta de lista proporciona una lista de elementos de desplazamiento.</span><span class="sxs-lookup"><span data-stu-id="582db-223">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="582db-224">Compatibilidad con tarjetas de lista</span><span class="sxs-lookup"><span data-stu-id="582db-224">Support for List cards</span></span>

| <span data-ttu-id="582db-225">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="582db-225">Bots in Teams</span></span> | <span data-ttu-id="582db-226">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="582db-226">Messaging Extensions</span></span>  | <span data-ttu-id="582db-227">Conectores</span><span class="sxs-lookup"><span data-stu-id="582db-227">Connectors</span></span> | <span data-ttu-id="582db-228">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="582db-228">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="582db-229">✔</span><span class="sxs-lookup"><span data-stu-id="582db-229">✔</span></span> | <span data-ttu-id="582db-230">✖</span><span class="sxs-lookup"><span data-stu-id="582db-230">✖</span></span> | <span data-ttu-id="582db-231">✖</span><span class="sxs-lookup"><span data-stu-id="582db-231">✖</span></span> |<span data-ttu-id="582db-232">✔</span><span class="sxs-lookup"><span data-stu-id="582db-232">✔</span></span> |
|

### <a name="properties-of-a-list-card"></a><span data-ttu-id="582db-233">Propiedades de una tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="582db-233">Properties of a List card</span></span>

| <span data-ttu-id="582db-234">Propiedad</span><span class="sxs-lookup"><span data-stu-id="582db-234">Property</span></span> | <span data-ttu-id="582db-235">Tipo</span><span class="sxs-lookup"><span data-stu-id="582db-235">Type</span></span>  | <span data-ttu-id="582db-236">Description</span><span class="sxs-lookup"><span data-stu-id="582db-236">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="582db-237">title</span><span class="sxs-lookup"><span data-stu-id="582db-237">title</span></span> | <span data-ttu-id="582db-238">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="582db-238">Rich text</span></span> | <span data-ttu-id="582db-239">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="582db-239">Title of the card.</span></span> <span data-ttu-id="582db-240">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="582db-240">Maximum 2 lines.</span></span>|
| <span data-ttu-id="582db-241">items</span><span class="sxs-lookup"><span data-stu-id="582db-241">items</span></span> | <span data-ttu-id="582db-242">Matriz de elementos de lista</span><span class="sxs-lookup"><span data-stu-id="582db-242">Array of list items</span></span>  ||
| <span data-ttu-id="582db-243">buttons</span><span class="sxs-lookup"><span data-stu-id="582db-243">buttons</span></span> | <span data-ttu-id="582db-244">Matriz de objetos de acción</span><span class="sxs-lookup"><span data-stu-id="582db-244">Array of action objects</span></span> | <span data-ttu-id="582db-245">Conjunto de acciones aplicables a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="582db-245">Set of actions applicable to the current card.</span></span> <span data-ttu-id="582db-246">Máximo 6.</span><span class="sxs-lookup"><span data-stu-id="582db-246">Maximum 6.</span></span> |

### <a name="example-list-card"></a><span data-ttu-id="582db-247">Ejemplo de tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="582db-247">Example List card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="582db-248">Tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="582db-248">Office 365 connector card</span></span>

<span data-ttu-id="582db-249">Se admite en Teams, no en Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="582db-249">Supported in Teams, not in Bot Framework.</span></span>

<span data-ttu-id="582db-250">La tarjeta del conector de Office 365 proporciona un diseño flexible con varias secciones, campos, imágenes y acciones.</span><span class="sxs-lookup"><span data-stu-id="582db-250">The Office 365 Connector card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="582db-251">Esta tarjeta encapsula una tarjeta de conector para que la puedan usar los bots.</span><span class="sxs-lookup"><span data-stu-id="582db-251">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="582db-252">Vea la sección de notas para ver las diferencias entre las tarjetas de conector y la tarjeta O365.</span><span class="sxs-lookup"><span data-stu-id="582db-252">See the notes section for differences between connector cards and the O365 card.</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="582db-253">Compatibilidad con tarjetas de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="582db-253">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="582db-254">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="582db-254">Bots in Teams</span></span> | <span data-ttu-id="582db-255">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="582db-255">Messaging Extensions</span></span>  | <span data-ttu-id="582db-256">Conectores</span><span class="sxs-lookup"><span data-stu-id="582db-256">Connectors</span></span> | <span data-ttu-id="582db-257">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="582db-257">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="582db-258">✔</span><span class="sxs-lookup"><span data-stu-id="582db-258">✔</span></span> | <span data-ttu-id="582db-259">✔</span><span class="sxs-lookup"><span data-stu-id="582db-259">✔</span></span> | <span data-ttu-id="582db-260">✔</span><span class="sxs-lookup"><span data-stu-id="582db-260">✔</span></span> | <span data-ttu-id="582db-261">✖</span><span class="sxs-lookup"><span data-stu-id="582db-261">✖</span></span> |
|

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="582db-262">Propiedades de la tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="582db-262">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="582db-263">Propiedad</span><span class="sxs-lookup"><span data-stu-id="582db-263">Property</span></span> | <span data-ttu-id="582db-264">Tipo</span><span class="sxs-lookup"><span data-stu-id="582db-264">Type</span></span>  | <span data-ttu-id="582db-265">Description</span><span class="sxs-lookup"><span data-stu-id="582db-265">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="582db-266">title</span><span class="sxs-lookup"><span data-stu-id="582db-266">title</span></span> | <span data-ttu-id="582db-267">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="582db-267">Rich text</span></span> | <span data-ttu-id="582db-268">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="582db-268">Title of the card.</span></span> <span data-ttu-id="582db-269">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="582db-269">Maximum 2 lines.</span></span> |
| <span data-ttu-id="582db-270">summary</span><span class="sxs-lookup"><span data-stu-id="582db-270">summary</span></span> | <span data-ttu-id="582db-271">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="582db-271">Rich text</span></span> | <span data-ttu-id="582db-272">Resumen de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="582db-272">Summary of the card.</span></span> <span data-ttu-id="582db-273">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="582db-273">Maximum 2 lines.</span></span> |
| <span data-ttu-id="582db-274">text</span><span class="sxs-lookup"><span data-stu-id="582db-274">text</span></span> | <span data-ttu-id="582db-275">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="582db-275">Rich text</span></span> | <span data-ttu-id="582db-276">El texto aparece justo debajo del subtítulo; ver [Formato de tarjeta para](~/task-modules-and-cards/cards/cards-format.md) las opciones de formato</span><span class="sxs-lookup"><span data-stu-id="582db-276">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="582db-277">themeColor</span><span class="sxs-lookup"><span data-stu-id="582db-277">themeColor</span></span> | <span data-ttu-id="582db-278">Cadena HEX</span><span class="sxs-lookup"><span data-stu-id="582db-278">HEX string</span></span> | <span data-ttu-id="582db-279">que reemplaza el accentColor proporcionado desde el manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="582db-279">color that overrides the accentColor provided from the application manifest</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="582db-280">Notas en la tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="582db-280">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="582db-281">Las tarjetas de conector de Office 365 funcionan correctamente en Microsoft Teams, incluidas [las acciones ActionCard](/outlook/actionable-messages/card-reference#actioncard-action).</span><span class="sxs-lookup"><span data-stu-id="582db-281">Office 365 Connector cards function properly on Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="582db-282">Una diferencia importante entre el uso de tarjetas de conector desde un conector y el uso de tarjetas de conector en el bot es el control de las acciones de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="582db-282">One important difference between using Connector cards from a Connector and using Connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="582db-283">Para un conector, el extremo recibe la carga de la tarjeta a través de HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="582db-283">For a Connector, the endpoint receives the card payload via HTTP POST.</span></span>
* <span data-ttu-id="582db-284">Para un bot, la acción desencadena una actividad que envía solo el identificador de acción `HttpPOST` y el cuerpo al `invoke` bot.</span><span class="sxs-lookup"><span data-stu-id="582db-284">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="582db-285">Cada tarjeta de conector puede mostrar un máximo de 10 secciones y cada sección puede contener un máximo de 5 imágenes y 5 acciones.</span><span class="sxs-lookup"><span data-stu-id="582db-285">Each Connector card can display a maximum of 10 sections, and each section can contain a maximum of 5 images and 5 actions.</span></span>

> [!NOTE]
> <span data-ttu-id="582db-286">Las secciones, imágenes o acciones adicionales de un mensaje no aparecerán.</span><span class="sxs-lookup"><span data-stu-id="582db-286">Any additional sections, images, or actions in a message will not appear.</span></span>

<span data-ttu-id="582db-287">Todos los campos de texto admiten Markdown y HTML.</span><span class="sxs-lookup"><span data-stu-id="582db-287">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="582db-288">Puede controlar qué secciones usan Markdown o HTML estableciendo la `markdown` propiedad en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="582db-288">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="582db-289">De forma predeterminada, `markdown` se establece en ; si desea usar HTML en su `true` lugar, establezca en `markdown` `false` .</span><span class="sxs-lookup"><span data-stu-id="582db-289">By default, `markdown` is set to `true`; if you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="582db-290">Si especificas la `themeColor` propiedad, esta invalida la `accentColor` propiedad en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="582db-290">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="582db-291">Para especificar el estilo de representación `activityImage` para , puede `activityImageType` establecerlo de la siguiente manera.</span><span class="sxs-lookup"><span data-stu-id="582db-291">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows.</span></span>

| <span data-ttu-id="582db-292">Valor</span><span class="sxs-lookup"><span data-stu-id="582db-292">Value</span></span> | <span data-ttu-id="582db-293">Descripción</span><span class="sxs-lookup"><span data-stu-id="582db-293">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="582db-294">Valor predeterminado; `activityImage` se recortará como un círculo</span><span class="sxs-lookup"><span data-stu-id="582db-294">Default; `activityImage` will be cropped as a circle</span></span> |
| `article` | <span data-ttu-id="582db-295">`activityImage` se mostrará como un rectángulo y conservará su relación de aspecto</span><span class="sxs-lookup"><span data-stu-id="582db-295">`activityImage` will be displayed as a rectangle and retain its aspect ratio</span></span> |

<span data-ttu-id="582db-296">Para obtener todos los demás detalles acerca de las propiedades de la tarjeta de conector, vea la [referencia de tarjeta de mensaje que puede acción.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="582db-296">For all other details about Connector card properties, see the [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="582db-297">Las únicas propiedades de tarjeta de conector que Microsoft Teams no admite actualmente son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="582db-297">The only Connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="582db-298">`startGroup` (siempre se trata como `true` en Teams)</span><span class="sxs-lookup"><span data-stu-id="582db-298">`startGroup` (always treated as `true` in Teams)</span></span>
* `originator`
* `correlationId`

### <a name="example-office-365-connector-card"></a><span data-ttu-id="582db-299">Ejemplo de tarjeta de conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="582db-299">Example Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="582db-300">Tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="582db-300">Receipt card</span></span>

<span data-ttu-id="582db-301">Compatible con Teams.</span><span class="sxs-lookup"><span data-stu-id="582db-301">Supported in Teams.</span></span>

<span data-ttu-id="582db-302">Tarjeta que permite a un bot proporcionar un recibo al usuario.</span><span class="sxs-lookup"><span data-stu-id="582db-302">A card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="582db-303">Normalmente contiene la lista de elementos que se deben incluir en el recibo, la información fiscal y total, y otro texto.</span><span class="sxs-lookup"><span data-stu-id="582db-303">It typically contains the list of items to include on the receipt, tax and total information, and other text.</span></span>

### <a name="support-for-receipts-cards"></a><span data-ttu-id="582db-304">Compatibilidad con tarjetas de recibos</span><span class="sxs-lookup"><span data-stu-id="582db-304">Support for Receipts cards</span></span>

| <span data-ttu-id="582db-305">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="582db-305">Bots in Teams</span></span> | <span data-ttu-id="582db-306">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="582db-306">Messaging Extensions</span></span>  | <span data-ttu-id="582db-307">Conectores</span><span class="sxs-lookup"><span data-stu-id="582db-307">Connectors</span></span> | <span data-ttu-id="582db-308">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="582db-308">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="582db-309">✔</span><span class="sxs-lookup"><span data-stu-id="582db-309">✔</span></span> | <span data-ttu-id="582db-310">✔</span><span class="sxs-lookup"><span data-stu-id="582db-310">✔</span></span> | <span data-ttu-id="582db-311">✖</span><span class="sxs-lookup"><span data-stu-id="582db-311">✖</span></span> | <span data-ttu-id="582db-312">✔</span><span class="sxs-lookup"><span data-stu-id="582db-312">✔</span></span> |
|

### <a name="for-more-information-on-receipt-cards"></a><span data-ttu-id="582db-313">Para obtener más información sobre las tarjetas de recibo</span><span class="sxs-lookup"><span data-stu-id="582db-313">For more information on Receipt cards</span></span>

<span data-ttu-id="582db-314">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="582db-314">Bot Framework reference:</span></span>

* [<span data-ttu-id="582db-315">Nodo de tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="582db-315">Receipt card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="582db-316">Tarjeta de recibo C #</span><span class="sxs-lookup"><span data-stu-id="582db-316">Receipt card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="582db-317">Tarjeta de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="582db-317">Signin card</span></span>

<span data-ttu-id="582db-318">Una tarjeta que permite a un bot solicitar que un usuario inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="582db-318">A card that enables a bot to request that a user sign in.</span></span> <span data-ttu-id="582db-319">Se admite en Teams de una forma ligeramente diferente a la que se encuentra en Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="582db-319">Supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="582db-320">La tarjeta de inicio de sesión en Teams es similar a la tarjeta de inicio de sesión en el marco del bot con la excepción de que la tarjeta de inicio de sesión en Teams solo admite dos acciones: `signin` y `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="582db-320">The signin card in Teams is similar to the signin card in the bot framework with the exception that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="582db-321">La *acción de inicio de* sesión se puede usar desde cualquier tarjeta de Teams, no solo desde la tarjeta de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="582db-321">The *signin action* can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="582db-322">Consulte el tema [Flujo de autenticación de Microsoft Teams para bots](~/bots/how-to/authentication/auth-flow-bot.md) para obtener más información sobre la autenticación.</span><span class="sxs-lookup"><span data-stu-id="582db-322">See the topic [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md) for more details on authentication.</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="582db-323">Compatibilidad con tarjetas de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="582db-323">Support for Signin cards</span></span>

| <span data-ttu-id="582db-324">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="582db-324">Bots in Teams</span></span> | <span data-ttu-id="582db-325">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="582db-325">Messaging Extensions</span></span>  | <span data-ttu-id="582db-326">Conectores</span><span class="sxs-lookup"><span data-stu-id="582db-326">Connectors</span></span> | <span data-ttu-id="582db-327">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="582db-327">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="582db-328">✔</span><span class="sxs-lookup"><span data-stu-id="582db-328">✔</span></span> | <span data-ttu-id="582db-329">✖</span><span class="sxs-lookup"><span data-stu-id="582db-329">✖</span></span> | <span data-ttu-id="582db-330">✖</span><span class="sxs-lookup"><span data-stu-id="582db-330">✖</span></span> | <span data-ttu-id="582db-331">✔</span><span class="sxs-lookup"><span data-stu-id="582db-331">✔</span></span> |
|

### <a name="for-more-information-on-signin-cards"></a><span data-ttu-id="582db-332">Para obtener más información sobre las tarjetas de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="582db-332">For more information on Signin cards</span></span>

<span data-ttu-id="582db-333">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="582db-333">Bot Framework reference:</span></span>

* [<span data-ttu-id="582db-334">Nodo de tarjeta de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="582db-334">Signin card Node</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="582db-335">Tarjeta de inicio de sesión C #</span><span class="sxs-lookup"><span data-stu-id="582db-335">Signin card C#</span></span>](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="582db-336">Tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="582db-336">Thumbnail card</span></span>

<span data-ttu-id="582db-337">Una tarjeta que normalmente contiene una sola imagen en miniatura, uno o más botones y texto.</span><span class="sxs-lookup"><span data-stu-id="582db-337">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="582db-338">Compatibilidad con tarjetas en miniatura</span><span class="sxs-lookup"><span data-stu-id="582db-338">Support for Thumbnail cards</span></span>

| <span data-ttu-id="582db-339">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="582db-339">Bots in Teams</span></span> | <span data-ttu-id="582db-340">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="582db-340">Messaging Extensions</span></span>  | <span data-ttu-id="582db-341">Conectores</span><span class="sxs-lookup"><span data-stu-id="582db-341">Connectors</span></span> | <span data-ttu-id="582db-342">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="582db-342">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="582db-343">✔</span><span class="sxs-lookup"><span data-stu-id="582db-343">✔</span></span> | <span data-ttu-id="582db-344">✔</span><span class="sxs-lookup"><span data-stu-id="582db-344">✔</span></span> | <span data-ttu-id="582db-345">✖</span><span class="sxs-lookup"><span data-stu-id="582db-345">✖</span></span> | <span data-ttu-id="582db-346">✔</span><span class="sxs-lookup"><span data-stu-id="582db-346">✔</span></span> |
|

![Ejemplo de una tarjeta en miniatura](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="582db-348">Propiedades de una tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="582db-348">Properties of a Thumbnail card</span></span>

| <span data-ttu-id="582db-349">Propiedad</span><span class="sxs-lookup"><span data-stu-id="582db-349">Property</span></span> | <span data-ttu-id="582db-350">Tipo</span><span class="sxs-lookup"><span data-stu-id="582db-350">Type</span></span>  | <span data-ttu-id="582db-351">Description</span><span class="sxs-lookup"><span data-stu-id="582db-351">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="582db-352">title</span><span class="sxs-lookup"><span data-stu-id="582db-352">title</span></span> | <span data-ttu-id="582db-353">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="582db-353">Rich text</span></span> | <span data-ttu-id="582db-354">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="582db-354">Title of the card.</span></span> <span data-ttu-id="582db-355">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="582db-355">Maximum 2 lines.</span></span>|
| <span data-ttu-id="582db-356">subtitle</span><span class="sxs-lookup"><span data-stu-id="582db-356">subtitle</span></span> | <span data-ttu-id="582db-357">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="582db-357">Rich text</span></span> | <span data-ttu-id="582db-358">Subtítulo de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="582db-358">Subtitle of the card.</span></span> <span data-ttu-id="582db-359">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="582db-359">Maximum 2 lines.</span></span>|
| <span data-ttu-id="582db-360">text</span><span class="sxs-lookup"><span data-stu-id="582db-360">text</span></span> | <span data-ttu-id="582db-361">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="582db-361">Rich text</span></span> | <span data-ttu-id="582db-362">El texto aparece justo debajo del subtítulo; ver [Formato de tarjeta para](~/task-modules-and-cards/cards/cards-format.md) las opciones de formato</span><span class="sxs-lookup"><span data-stu-id="582db-362">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="582db-363">imágenes</span><span class="sxs-lookup"><span data-stu-id="582db-363">images</span></span> | <span data-ttu-id="582db-364">Matriz de imágenes</span><span class="sxs-lookup"><span data-stu-id="582db-364">Array of images</span></span> | <span data-ttu-id="582db-365">Imagen que se muestra en la parte superior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="582db-365">Image displayed at top of card.</span></span> <span data-ttu-id="582db-366">Relación de aspecto 1:1 (cuadrado)</span><span class="sxs-lookup"><span data-stu-id="582db-366">Aspect ratio 1:1 (square)</span></span> |
| <span data-ttu-id="582db-367">buttons</span><span class="sxs-lookup"><span data-stu-id="582db-367">buttons</span></span> | <span data-ttu-id="582db-368">Matriz de objetos de acción</span><span class="sxs-lookup"><span data-stu-id="582db-368">Array of action objects</span></span> | <span data-ttu-id="582db-369">Conjunto de acciones aplicables a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="582db-369">Set of actions applicable to the current card.</span></span> <span data-ttu-id="582db-370">Máximo 6</span><span class="sxs-lookup"><span data-stu-id="582db-370">Maximum 6</span></span> |
| <span data-ttu-id="582db-371">pulsación</span><span class="sxs-lookup"><span data-stu-id="582db-371">tap</span></span> | <span data-ttu-id="582db-372">Action (objeto)</span><span class="sxs-lookup"><span data-stu-id="582db-372">Action object</span></span> | <span data-ttu-id="582db-373">Esta acción se activará cuando el usuario pulse en la propia tarjeta.</span><span class="sxs-lookup"><span data-stu-id="582db-373">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-thumbnail-card"></a><span data-ttu-id="582db-374">Ejemplo de tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="582db-374">Example Thumbnail card</span></span>

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

### <a name="for-more-information"></a><span data-ttu-id="582db-375">Más información</span><span class="sxs-lookup"><span data-stu-id="582db-375">For more information</span></span>

<span data-ttu-id="582db-376">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="582db-376">Bot Framework reference:</span></span>

* [<span data-ttu-id="582db-377">Nodo de tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="582db-377">Thumbnail card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="582db-378">Tarjeta en miniatura C #</span><span class="sxs-lookup"><span data-stu-id="582db-378">Thumbnail card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="582db-379">Colecciones de tarjetas</span><span class="sxs-lookup"><span data-stu-id="582db-379">Card collections</span></span>

<span data-ttu-id="582db-380">Las colecciones de tarjetas son compatibles con Teams.</span><span class="sxs-lookup"><span data-stu-id="582db-380">Card collections are supported in Teams.</span></span>

<span data-ttu-id="582db-381">Colecciones de tarjetas: `builder.AttachmentLayout.carousel` y `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="582db-381">Card collections: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="582db-382">Estas colecciones contienen tarjetas adaptables, principal o en miniatura.</span><span class="sxs-lookup"><span data-stu-id="582db-382">These collections contain Adaptive, Hero, or Thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="582db-383">Carrusel (colección)</span><span class="sxs-lookup"><span data-stu-id="582db-383">Carousel collection</span></span>

<span data-ttu-id="582db-384">El [diseño de carrusel](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true) muestra un carrusel de tarjetas, opcionalmente con botones de acción asociados.</span><span class="sxs-lookup"><span data-stu-id="582db-384">The [carousel layout](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="582db-385">Compatibilidad con colecciones de carrusel</span><span class="sxs-lookup"><span data-stu-id="582db-385">Support for Carousel collections</span></span>

| <span data-ttu-id="582db-386">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="582db-386">Bots in Teams</span></span> | <span data-ttu-id="582db-387">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="582db-387">Messaging Extensions</span></span>  | <span data-ttu-id="582db-388">Conectores</span><span class="sxs-lookup"><span data-stu-id="582db-388">Connectors</span></span> | <span data-ttu-id="582db-389">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="582db-389">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="582db-390">✔</span><span class="sxs-lookup"><span data-stu-id="582db-390">✔</span></span> | <span data-ttu-id="582db-391">✖</span><span class="sxs-lookup"><span data-stu-id="582db-391">✖</span></span> | <span data-ttu-id="582db-392">✖</span><span class="sxs-lookup"><span data-stu-id="582db-392">✖</span></span> | <span data-ttu-id="582db-393">✔</span><span class="sxs-lookup"><span data-stu-id="582db-393">✔</span></span> |
|

> [!NOTE]
> <span data-ttu-id="582db-394">Un carrusel puede mostrar un máximo de 10 tarjetas por mensaje.</span><span class="sxs-lookup"><span data-stu-id="582db-394">A carousel can display a maximum of 10 cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="582db-395">Propiedades de una tarjeta de carrusel</span><span class="sxs-lookup"><span data-stu-id="582db-395">Properties of a Carousel card</span></span>

<span data-ttu-id="582db-396">Las propiedades de una tarjeta de carrusel son las mismas que las de las tarjetas Hero y Thumbnail.</span><span class="sxs-lookup"><span data-stu-id="582db-396">Properties of a Carousel card are same as those of the Hero and Thumbnail cards.</span></span>

### <a name="example-carousel-collection"></a><span data-ttu-id="582db-397">Ejemplo de colección de carruseles</span><span class="sxs-lookup"><span data-stu-id="582db-397">Example Carousel collection</span></span>

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="582db-399">Sintaxis para colecciones de carrusel</span><span class="sxs-lookup"><span data-stu-id="582db-399">Syntax for Carousel collections</span></span>

`builder.AttachmentLayoutTypes.Carousel`

## <a name="list-collection"></a><span data-ttu-id="582db-400">Colección de listas</span><span class="sxs-lookup"><span data-stu-id="582db-400">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="582db-401">Compatibilidad con colecciones de listas</span><span class="sxs-lookup"><span data-stu-id="582db-401">Support for List collections</span></span>

<span data-ttu-id="582db-402">El diseño de lista muestra una lista apilada verticalmente de tarjetas, opcionalmente con botones de acción asociados.</span><span class="sxs-lookup"><span data-stu-id="582db-402">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="582db-403">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="582db-403">Bots in Teams</span></span> | <span data-ttu-id="582db-404">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="582db-404">Messaging Extensions</span></span>  | <span data-ttu-id="582db-405">Conectores</span><span class="sxs-lookup"><span data-stu-id="582db-405">Connectors</span></span> | <span data-ttu-id="582db-406">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="582db-406">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="582db-407">✔</span><span class="sxs-lookup"><span data-stu-id="582db-407">✔</span></span> | <span data-ttu-id="582db-408">✔</span><span class="sxs-lookup"><span data-stu-id="582db-408">✔</span></span> | <span data-ttu-id="582db-409">✖</span><span class="sxs-lookup"><span data-stu-id="582db-409">✖</span></span> | <span data-ttu-id="582db-410">✔</span><span class="sxs-lookup"><span data-stu-id="582db-410">✔</span></span> |
|

### <a name="example-list-collection"></a><span data-ttu-id="582db-411">Ejemplo de colección List</span><span class="sxs-lookup"><span data-stu-id="582db-411">Example List collection</span></span>

![Ejemplo de una lista de tarjetas](~/assets/images/cards/list.png)

<span data-ttu-id="582db-413">Las propiedades son las mismas que para la tarjeta principal o en miniatura.</span><span class="sxs-lookup"><span data-stu-id="582db-413">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="582db-414">Una lista puede mostrar un máximo de 10 tarjetas por mensaje.</span><span class="sxs-lookup"><span data-stu-id="582db-414">A list can display a maximum of 10 cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="582db-415">Algunas combinaciones de tarjetas de lista aún no se admiten en iOS y Android.</span><span class="sxs-lookup"><span data-stu-id="582db-415">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="582db-416">Sintaxis para colecciones de listas</span><span class="sxs-lookup"><span data-stu-id="582db-416">Syntax for List collections</span></span>

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="582db-417">Tarjetas no admitidas en Teams</span><span class="sxs-lookup"><span data-stu-id="582db-417">Cards not supported in Teams</span></span>

<span data-ttu-id="582db-418">Bot Framework implementa las siguientes tarjetas, pero Teams no las admite.</span><span class="sxs-lookup"><span data-stu-id="582db-418">The following cards are implemented by the Bot Framework, but are NOT supported by Teams.</span></span>

* <span data-ttu-id="582db-419">Tarjetas de animación</span><span class="sxs-lookup"><span data-stu-id="582db-419">Animation cards</span></span>
* <span data-ttu-id="582db-420">Tarjetas de audio</span><span class="sxs-lookup"><span data-stu-id="582db-420">Audio cards</span></span>
* <span data-ttu-id="582db-421">Tarjetas de vídeo</span><span class="sxs-lookup"><span data-stu-id="582db-421">Video cards</span></span>

---
title: Tipos de tarjetas
description: Describe todas las tarjetas y acciones de tarjeta disponibles para bots en Teams
localization_priority: Normal
keywords: referencia de tarjetas bots
ms.topic: reference
ms.openlocfilehash: be38454daac519530d0fdf10b5170e128219f6fc
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140500"
---
# <a name="types-of-cards"></a><span data-ttu-id="d92eb-104">Tipos de tarjetas</span><span class="sxs-lookup"><span data-stu-id="d92eb-104">Types of cards</span></span>

<span data-ttu-id="d92eb-105">Adaptive, hero, list, Office 365 Connector, receipt, signin, and thumbnail cards and card collections are supported in bots for Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d92eb-105">Adaptive, hero, list, Office 365 Connector, receipt, signin, and thumbnail cards and card collections are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="d92eb-106">Se basan en tarjetas definidas por Bot Framework, pero Teams no admite todas las tarjetas de Bot Framework y ha agregado algunas de sus propias.</span><span class="sxs-lookup"><span data-stu-id="d92eb-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span>

<span data-ttu-id="d92eb-107">Antes de identificar los distintos tipos de tarjeta, comprenda cómo crear una tarjeta de héroe, una tarjeta en miniatura o una tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="d92eb-107">Before you identify the different card types, understand how to create a a hero card, thumbnail card, or Adaptive Card.</span></span>

## <a name="create-a-hero-card-thumbnail-card-or-adaptive-card"></a><span data-ttu-id="d92eb-108">Crear una tarjeta de héroe, una tarjeta en miniatura o una tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="d92eb-108">Create a hero card, thumbnail card, or Adaptive Card</span></span>

<span data-ttu-id="d92eb-109">**Para crear una tarjeta de héroe, una miniatura o una tarjeta adaptable desde App Studio**</span><span class="sxs-lookup"><span data-stu-id="d92eb-109">**To create a hero card, thumbnail card, or Adaptive Card from App Studio**</span></span>

1. <span data-ttu-id="d92eb-110">Ve a **App Studio** desde Teams.</span><span class="sxs-lookup"><span data-stu-id="d92eb-110">Go to **App Studio** from Teams.</span></span>
1. <span data-ttu-id="d92eb-111">Seleccione **Editor de tarjetas**.</span><span class="sxs-lookup"><span data-stu-id="d92eb-111">Select **Card editor**.</span></span>
1. <span data-ttu-id="d92eb-112">Seleccione **Crear una nueva tarjeta**.</span><span class="sxs-lookup"><span data-stu-id="d92eb-112">Select **Create a new card**.</span></span>
1. <span data-ttu-id="d92eb-113">Seleccione **Crear** para una de las tarjetas de **hero card**, Thumbnail **Card** o Adaptive **Card**.</span><span class="sxs-lookup"><span data-stu-id="d92eb-113">Select **Create** for one of the cards from **Hero Card**, **Thumbnail Card**, or **Adaptive Card**.</span></span> <span data-ttu-id="d92eb-114">Los detalles de metadatos, los botones y los ejemplos de código json, csharp y node se muestran para esa tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d92eb-114">The metadata details, buttons, and json, csharp, and node code examples are shown for that card.</span></span>

    ![Detalles de la tarjeta de héroe](~/assets/images/Cards/Herocarddetails.png)

1. <span data-ttu-id="d92eb-116">Seleccione **Enviarme esta tarjeta**.</span><span class="sxs-lookup"><span data-stu-id="d92eb-116">Select **Send me this card**.</span></span> <span data-ttu-id="d92eb-117">La tarjeta se envía como un mensaje de chat.</span><span class="sxs-lookup"><span data-stu-id="d92eb-117">The card is sent to you as a chat message.</span></span>

## <a name="card-examples"></a><span data-ttu-id="d92eb-118">Ejemplos de tarjetas</span><span class="sxs-lookup"><span data-stu-id="d92eb-118">Card examples</span></span>

<span data-ttu-id="d92eb-119">Encontrará información adicional sobre cómo usar tarjetas en la documentación del SDK de Bot Builder v3.</span><span class="sxs-lookup"><span data-stu-id="d92eb-119">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="d92eb-120">Los ejemplos de código también están disponibles en el **repositorio microsoft/BotBuilder-Samples** en GitHub.</span><span class="sxs-lookup"><span data-stu-id="d92eb-120">Code samples are also available in the **Microsoft/BotBuilder-Samples** repository on GitHub.</span></span> <span data-ttu-id="d92eb-121">A continuación se muestran algunos ejemplos de tarjetas:</span><span class="sxs-lookup"><span data-stu-id="d92eb-121">Following are a few card examples:</span></span>

* <span data-ttu-id="d92eb-122">.NET</span><span class="sxs-lookup"><span data-stu-id="d92eb-122">.NET</span></span>
  * <span data-ttu-id="d92eb-123">[Agregar tarjetas como datos adjuntos a los mensajes](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="d92eb-123">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="d92eb-124">[Código de ejemplo de tarjetas Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="d92eb-124">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span></span>

* <span data-ttu-id="d92eb-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="d92eb-125">Node.js</span></span>
  * <span data-ttu-id="d92eb-126">[Agregar tarjetas como datos adjuntos a los mensajes](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="d92eb-126">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="d92eb-127">[Código de ejemplo de tarjetas Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="d92eb-127">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span></span>

## <a name="card-types"></a><span data-ttu-id="d92eb-128">Tipos de tarjeta</span><span class="sxs-lookup"><span data-stu-id="d92eb-128">Card types</span></span>

<span data-ttu-id="d92eb-129">Puede identificar y usar diferentes tipos de tarjetas según los requisitos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d92eb-129">You can identify and use different types of cards based on your application requirements.</span></span> <span data-ttu-id="d92eb-130">En la tabla siguiente se muestran los tipos de tarjetas disponibles:</span><span class="sxs-lookup"><span data-stu-id="d92eb-130">The following table shows the types of cards available to you:</span></span>

| <span data-ttu-id="d92eb-131">Tipo de tarjeta</span><span class="sxs-lookup"><span data-stu-id="d92eb-131">Card type</span></span> | <span data-ttu-id="d92eb-132">Descripción</span><span class="sxs-lookup"><span data-stu-id="d92eb-132">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="d92eb-133">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="d92eb-133">Adaptive Card</span></span>](#adaptive-card) | <span data-ttu-id="d92eb-134">Esta tarjeta es altamente personalizable y puede contener cualquier combinación de texto, voz, imágenes, botones y campos de entrada.</span><span class="sxs-lookup"><span data-stu-id="d92eb-134">This card is highly customizable and can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="d92eb-135">Tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="d92eb-135">Hero card</span></span>](#hero-card) | <span data-ttu-id="d92eb-136">Esta tarjeta normalmente contiene una sola imagen grande, uno o varios botones y una pequeña cantidad de texto.</span><span class="sxs-lookup"><span data-stu-id="d92eb-136">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="d92eb-137">Tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="d92eb-137">List card</span></span>](#list-card) | <span data-ttu-id="d92eb-138">Esta tarjeta contiene una lista de desplazamiento de elementos.</span><span class="sxs-lookup"><span data-stu-id="d92eb-138">This card contains a scrolling list of items.</span></span> |
| [<span data-ttu-id="d92eb-139">Office 365 Tarjeta de conector</span><span class="sxs-lookup"><span data-stu-id="d92eb-139">Office 365 Connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="d92eb-140">Esta tarjeta tiene un diseño flexible con varias secciones, campos, imágenes y acciones.</span><span class="sxs-lookup"><span data-stu-id="d92eb-140">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="d92eb-141">Tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="d92eb-141">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="d92eb-142">Esta tarjeta proporciona un recibo al usuario.</span><span class="sxs-lookup"><span data-stu-id="d92eb-142">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="d92eb-143">Tarjeta de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="d92eb-143">Signin card</span></span>](#signin-card) | <span data-ttu-id="d92eb-144">Esta tarjeta permite que un bot solicite que un usuario inicia sesión.</span><span class="sxs-lookup"><span data-stu-id="d92eb-144">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="d92eb-145">Tarjeta miniatura</span><span class="sxs-lookup"><span data-stu-id="d92eb-145">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="d92eb-146">Esta tarjeta normalmente contiene una sola imagen en miniatura, texto corto y uno o más botones.</span><span class="sxs-lookup"><span data-stu-id="d92eb-146">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="d92eb-147">Colecciones de tarjetas</span><span class="sxs-lookup"><span data-stu-id="d92eb-147">Card collections</span></span>](#card-collections) | <span data-ttu-id="d92eb-148">Esta colección de tarjetas se usa para devolver varios elementos en una sola respuesta.</span><span class="sxs-lookup"><span data-stu-id="d92eb-148">This card collection is used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="d92eb-149">Propiedades comunes para todas las tarjetas</span><span class="sxs-lookup"><span data-stu-id="d92eb-149">Common properties for all cards</span></span>

<span data-ttu-id="d92eb-150">Puedes ir a través de algunas propiedades comunes que son aplicables a todas las tarjetas.</span><span class="sxs-lookup"><span data-stu-id="d92eb-150">You can go through some common properties that are applicable to all cards.</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="d92eb-151">Imágenes de tarjetas en línea</span><span class="sxs-lookup"><span data-stu-id="d92eb-151">Inline card images</span></span>

<span data-ttu-id="d92eb-152">La tarjeta puede contener una imagen en línea al incluir un vínculo a la imagen disponible públicamente.</span><span class="sxs-lookup"><span data-stu-id="d92eb-152">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="d92eb-153">Por motivos de rendimiento, se recomienda hospedar la imagen en un servidor público Content Delivery Network (CDN).</span><span class="sxs-lookup"><span data-stu-id="d92eb-153">For performance purposes, it is highly recommended you host the image on a public Content Delivery Network (CDN).</span></span>

<span data-ttu-id="d92eb-154">Las imágenes se escalan hacia arriba o hacia abajo en tamaño para mantener la relación de aspecto para cubrir el área de imagen.</span><span class="sxs-lookup"><span data-stu-id="d92eb-154">Images are scaled up or down in size to maintain the aspect ratio for covering the image area.</span></span> <span data-ttu-id="d92eb-155">A continuación, las imágenes se recortan desde el centro para lograr la relación de aspecto adecuada para la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d92eb-155">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="d92eb-156">Las imágenes deben tener como máximo 1024×1024 y en formato PNG, JPEG o GIF.</span><span class="sxs-lookup"><span data-stu-id="d92eb-156">Images must be at most 1024×1024 and in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="d92eb-157">Gif animado no es compatible.</span><span class="sxs-lookup"><span data-stu-id="d92eb-157">Animated GIF is not supported.</span></span>

<span data-ttu-id="d92eb-158">En la tabla siguiente se proporcionan las propiedades de las imágenes de tarjetas en línea:</span><span class="sxs-lookup"><span data-stu-id="d92eb-158">The following table provides the properties of inline card images:</span></span>

| <span data-ttu-id="d92eb-159">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d92eb-159">Property</span></span> | <span data-ttu-id="d92eb-160">Tipo</span><span class="sxs-lookup"><span data-stu-id="d92eb-160">Type</span></span>  | <span data-ttu-id="d92eb-161">Descripción</span><span class="sxs-lookup"><span data-stu-id="d92eb-161">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d92eb-162">url</span><span class="sxs-lookup"><span data-stu-id="d92eb-162">url</span></span> | <span data-ttu-id="d92eb-163">URL</span><span class="sxs-lookup"><span data-stu-id="d92eb-163">URL</span></span> | <span data-ttu-id="d92eb-164">DIRECCIÓN URL HTTPS a la imagen.</span><span class="sxs-lookup"><span data-stu-id="d92eb-164">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="d92eb-165">alt</span><span class="sxs-lookup"><span data-stu-id="d92eb-165">alt</span></span> | <span data-ttu-id="d92eb-166">Cadena</span><span class="sxs-lookup"><span data-stu-id="d92eb-166">String</span></span> | <span data-ttu-id="d92eb-167">Descripción accesible de la imagen.</span><span class="sxs-lookup"><span data-stu-id="d92eb-167">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="d92eb-168">Si una tarjeta incluye una dirección URL de imagen que se redirige antes de la imagen final, no se admite el redireccionamiento en la dirección URL de la imagen.</span><span class="sxs-lookup"><span data-stu-id="d92eb-168">If a card includes an image URL that is redirected before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="d92eb-169">Esto ocurre para las imágenes compartidas en la nube pública.</span><span class="sxs-lookup"><span data-stu-id="d92eb-169">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="d92eb-170">Botones</span><span class="sxs-lookup"><span data-stu-id="d92eb-170">Buttons</span></span>

<span data-ttu-id="d92eb-171">Los botones se muestran apilados en la parte inferior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d92eb-171">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="d92eb-172">El texto del botón siempre está en una sola línea y se trunca si el texto supera el ancho del botón.</span><span class="sxs-lookup"><span data-stu-id="d92eb-172">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="d92eb-173">No se muestran los botones adicionales que supere el número máximo admitido por la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d92eb-173">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="d92eb-174">Para obtener más información, vea [acciones de tarjeta](~/task-modules-and-cards/cards/cards-actions.md).</span><span class="sxs-lookup"><span data-stu-id="d92eb-174">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="d92eb-175">Formato de tarjeta</span><span class="sxs-lookup"><span data-stu-id="d92eb-175">Card formatting</span></span>

<span data-ttu-id="d92eb-176">Para obtener más información sobre el formato de texto en tarjetas, vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="d92eb-176">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

<span data-ttu-id="d92eb-177">Después de identificar las propiedades comunes de todas las tarjetas, ahora puedes trabajar con tarjetas adaptables, lo que te ayudará a aumentar la interacción y la eficacia agregando el contenido que se puede usar directamente en las aplicaciones que usas.</span><span class="sxs-lookup"><span data-stu-id="d92eb-177">After identifying the common properties for all cards, you can now work with Adaptive Cards, which help you increase engagement and efficiency by adding your actionable content directly into the apps you use.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="d92eb-178">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="d92eb-178">Adaptive Card</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/J12lKt717Ws]

<span data-ttu-id="d92eb-179">Una tarjeta adaptable es una tarjeta personalizable que puede contener cualquier combinación de texto, voz, imágenes, botones y campos de entrada.</span><span class="sxs-lookup"><span data-stu-id="d92eb-179">An Adaptive Card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="d92eb-180">Para obtener más información, vea [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="d92eb-180">For more information, see [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="d92eb-181">Compatibilidad con tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="d92eb-181">Support for Adaptive Cards</span></span>

<span data-ttu-id="d92eb-182">En la tabla siguiente se proporcionan las características que admiten tarjetas adaptables:</span><span class="sxs-lookup"><span data-stu-id="d92eb-182">The following table provides the features that support Adaptive Cards:</span></span>

| <span data-ttu-id="d92eb-183">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="d92eb-183">Bots in Teams</span></span> | <span data-ttu-id="d92eb-184">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="d92eb-184">Messaging extensions</span></span>  | <span data-ttu-id="d92eb-185">Conectores</span><span class="sxs-lookup"><span data-stu-id="d92eb-185">Connectors</span></span> | <span data-ttu-id="d92eb-186">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="d92eb-186">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d92eb-187">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-187">✔</span></span> | <span data-ttu-id="d92eb-188">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-188">✔</span></span> | <span data-ttu-id="d92eb-189">✖</span><span class="sxs-lookup"><span data-stu-id="d92eb-189">✖</span></span> | <span data-ttu-id="d92eb-190">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-190">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="d92eb-191">Teams plataforma admite v1.2 o versiones anteriores de características de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="d92eb-191">Teams platform supports v1.2 or earlier of Adaptive Card features.</span></span>
> * <span data-ttu-id="d92eb-192">El estilo de acción positiva o destructiva no se admite en tarjetas adaptables en la Teams web.</span><span class="sxs-lookup"><span data-stu-id="d92eb-192">Positive or destructive action styling is not supported in Adaptive Cards on the Teams platform.</span></span>
> * <span data-ttu-id="d92eb-193">Actualmente, los elementos multimedia no se admiten en la tarjeta adaptable en Teams plataforma.</span><span class="sxs-lookup"><span data-stu-id="d92eb-193">Media elements are currently not supported in Adaptive Card on the Teams platform.</span></span>

### <a name="example-of-adaptive-card"></a><span data-ttu-id="d92eb-194">Ejemplo de tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="d92eb-194">Example of Adaptive Card</span></span>

![Ejemplo de una tarjeta adaptable](~/assets/images/cards/adaptivecard.png)

<span data-ttu-id="d92eb-196">El código siguiente muestra un ejemplo de una tarjeta adaptable:</span><span class="sxs-lookup"><span data-stu-id="d92eb-196">The following code shows an example of an Adaptive Card:</span></span>

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="d92eb-197">Información adicional sobre tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="d92eb-197">Additional information on Adaptive Cards</span></span>

<span data-ttu-id="d92eb-198">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="d92eb-198">Bot Framework reference:</span></span>

* [<span data-ttu-id="d92eb-199">Nodo de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="d92eb-199">Adaptive Cards Node</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="d92eb-200">Tarjeta adaptable C #</span><span class="sxs-lookup"><span data-stu-id="d92eb-200">Adaptive Card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

<span data-ttu-id="d92eb-201">Ahora puedes trabajar con una tarjeta de héroe, que es una tarjeta multipropósito que se usa para resaltar visualmente una selección de usuario potencial.</span><span class="sxs-lookup"><span data-stu-id="d92eb-201">You can now work with a hero card, which is a multipurpose card used to visually highlight a potential user selection.</span></span>

## <a name="hero-card"></a><span data-ttu-id="d92eb-202">Tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="d92eb-202">Hero card</span></span>

<span data-ttu-id="d92eb-203">Una tarjeta que normalmente contiene una sola imagen grande, uno o varios botones y texto.</span><span class="sxs-lookup"><span data-stu-id="d92eb-203">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="d92eb-204">Compatibilidad con tarjetas de héroe</span><span class="sxs-lookup"><span data-stu-id="d92eb-204">Support for hero cards</span></span>

<span data-ttu-id="d92eb-205">En la tabla siguiente se proporcionan las características que admiten tarjetas de héroe:</span><span class="sxs-lookup"><span data-stu-id="d92eb-205">The following table provides the features that support hero cards:</span></span>

| <span data-ttu-id="d92eb-206">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="d92eb-206">Bots in Teams</span></span> | <span data-ttu-id="d92eb-207">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="d92eb-207">Messaging extensions</span></span>  | <span data-ttu-id="d92eb-208">Conectores</span><span class="sxs-lookup"><span data-stu-id="d92eb-208">Connectors</span></span> | <span data-ttu-id="d92eb-209">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="d92eb-209">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d92eb-210">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-210">✔</span></span> | <span data-ttu-id="d92eb-211">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-211">✔</span></span> | <span data-ttu-id="d92eb-212">✖</span><span class="sxs-lookup"><span data-stu-id="d92eb-212">✖</span></span> | <span data-ttu-id="d92eb-213">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-213">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="d92eb-214">Propiedades de una tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="d92eb-214">Properties of a hero card</span></span>

<span data-ttu-id="d92eb-215">En la tabla siguiente se proporcionan las propiedades de una tarjeta de héroe:</span><span class="sxs-lookup"><span data-stu-id="d92eb-215">The following table provides the properties of a hero card:</span></span>

| <span data-ttu-id="d92eb-216">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d92eb-216">Property</span></span> | <span data-ttu-id="d92eb-217">Tipo</span><span class="sxs-lookup"><span data-stu-id="d92eb-217">Type</span></span>  | <span data-ttu-id="d92eb-218">Description</span><span class="sxs-lookup"><span data-stu-id="d92eb-218">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d92eb-219">title</span><span class="sxs-lookup"><span data-stu-id="d92eb-219">title</span></span> | <span data-ttu-id="d92eb-220">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="d92eb-220">Rich text</span></span> | <span data-ttu-id="d92eb-221">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d92eb-221">Title of the card.</span></span> <span data-ttu-id="d92eb-222">Máximo dos líneas.</span><span class="sxs-lookup"><span data-stu-id="d92eb-222">Maximum two lines.</span></span> |
| <span data-ttu-id="d92eb-223">subtitle</span><span class="sxs-lookup"><span data-stu-id="d92eb-223">subtitle</span></span> | <span data-ttu-id="d92eb-224">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="d92eb-224">Rich text</span></span> | <span data-ttu-id="d92eb-225">Subtítulo de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d92eb-225">Subtitle of the card.</span></span> <span data-ttu-id="d92eb-226">Máximo dos líneas.</span><span class="sxs-lookup"><span data-stu-id="d92eb-226">Maximum two lines.</span></span>|
| <span data-ttu-id="d92eb-227">text</span><span class="sxs-lookup"><span data-stu-id="d92eb-227">text</span></span> | <span data-ttu-id="d92eb-228">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="d92eb-228">Rich text</span></span> | <span data-ttu-id="d92eb-229">El texto aparece debajo del subtítulo.</span><span class="sxs-lookup"><span data-stu-id="d92eb-229">Text appears under the subtitle.</span></span> <span data-ttu-id="d92eb-230">Para ver las opciones de formato, vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="d92eb-230">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="d92eb-231">imágenes</span><span class="sxs-lookup"><span data-stu-id="d92eb-231">images</span></span> | <span data-ttu-id="d92eb-232">Matriz de imágenes</span><span class="sxs-lookup"><span data-stu-id="d92eb-232">Array of images</span></span> | <span data-ttu-id="d92eb-233">Imagen que se muestra en la parte superior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d92eb-233">Image displayed at the top of the card.</span></span> <span data-ttu-id="d92eb-234">Relación de aspecto 16:9.</span><span class="sxs-lookup"><span data-stu-id="d92eb-234">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="d92eb-235">botones</span><span class="sxs-lookup"><span data-stu-id="d92eb-235">buttons</span></span> | <span data-ttu-id="d92eb-236">Matriz de objetos de acción</span><span class="sxs-lookup"><span data-stu-id="d92eb-236">Array of action objects</span></span> | <span data-ttu-id="d92eb-237">Conjunto de acciones aplicables a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="d92eb-237">Set of actions applicable to the current card.</span></span> <span data-ttu-id="d92eb-238">Máximo seis.</span><span class="sxs-lookup"><span data-stu-id="d92eb-238">Maximum six.</span></span> |
| <span data-ttu-id="d92eb-239">pulsación</span><span class="sxs-lookup"><span data-stu-id="d92eb-239">tap</span></span> | <span data-ttu-id="d92eb-240">Action (objeto)</span><span class="sxs-lookup"><span data-stu-id="d92eb-240">Action object</span></span> | <span data-ttu-id="d92eb-241">Se activa cuando el usuario pulsa en la propia tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d92eb-241">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="d92eb-242">Ejemplo de una tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="d92eb-242">Example of a hero card</span></span>

![Ejemplo de una tarjeta de héroe](~/assets/images/cards/hero.png)

<span data-ttu-id="d92eb-244">El siguiente código muestra un ejemplo de una tarjeta de héroe:</span><span class="sxs-lookup"><span data-stu-id="d92eb-244">The following code shows an example of a hero card:</span></span>

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="d92eb-245">Información adicional sobre tarjetas de héroe</span><span class="sxs-lookup"><span data-stu-id="d92eb-245">Additional information on hero cards</span></span>

<span data-ttu-id="d92eb-246">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="d92eb-246">Bot Framework reference:</span></span>

* [<span data-ttu-id="d92eb-247">Tarjeta de Node.js</span><span class="sxs-lookup"><span data-stu-id="d92eb-247">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="d92eb-248">Tarjeta de héroe C #</span><span class="sxs-lookup"><span data-stu-id="d92eb-248">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="d92eb-249">Tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="d92eb-249">List card</span></span>

<span data-ttu-id="d92eb-250">La tarjeta de lista se ha agregado Teams para proporcionar funciones más allá de lo que la colección de listas puede proporcionar.</span><span class="sxs-lookup"><span data-stu-id="d92eb-250">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="d92eb-251">La tarjeta de lista proporciona una lista de desplazamiento de elementos.</span><span class="sxs-lookup"><span data-stu-id="d92eb-251">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="d92eb-252">Compatibilidad con tarjetas de lista</span><span class="sxs-lookup"><span data-stu-id="d92eb-252">Support for list cards</span></span>

<span data-ttu-id="d92eb-253">En la tabla siguiente se proporcionan las características que admiten tarjetas de lista:</span><span class="sxs-lookup"><span data-stu-id="d92eb-253">The following table provides the features that support list cards:</span></span>

| <span data-ttu-id="d92eb-254">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="d92eb-254">Bots in Teams</span></span> | <span data-ttu-id="d92eb-255">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="d92eb-255">Messaging extensions</span></span>  | <span data-ttu-id="d92eb-256">Conectores</span><span class="sxs-lookup"><span data-stu-id="d92eb-256">Connectors</span></span> | <span data-ttu-id="d92eb-257">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="d92eb-257">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d92eb-258">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-258">✔</span></span> | <span data-ttu-id="d92eb-259">✖</span><span class="sxs-lookup"><span data-stu-id="d92eb-259">✖</span></span> | <span data-ttu-id="d92eb-260">✖</span><span class="sxs-lookup"><span data-stu-id="d92eb-260">✖</span></span> |<span data-ttu-id="d92eb-261">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-261">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="d92eb-262">Propiedades de una tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="d92eb-262">Properties of a list card</span></span>

<span data-ttu-id="d92eb-263">En la tabla siguiente se proporcionan las propiedades de una tarjeta de lista:</span><span class="sxs-lookup"><span data-stu-id="d92eb-263">The following table provides the properties of a list card:</span></span>

| <span data-ttu-id="d92eb-264">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d92eb-264">Property</span></span> | <span data-ttu-id="d92eb-265">Tipo</span><span class="sxs-lookup"><span data-stu-id="d92eb-265">Type</span></span>  | <span data-ttu-id="d92eb-266">Description</span><span class="sxs-lookup"><span data-stu-id="d92eb-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d92eb-267">title</span><span class="sxs-lookup"><span data-stu-id="d92eb-267">title</span></span> | <span data-ttu-id="d92eb-268">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="d92eb-268">Rich text</span></span> | <span data-ttu-id="d92eb-269">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d92eb-269">Title of the card.</span></span> <span data-ttu-id="d92eb-270">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="d92eb-270">Maximum 2 lines.</span></span>|
| <span data-ttu-id="d92eb-271">elementos</span><span class="sxs-lookup"><span data-stu-id="d92eb-271">items</span></span> | <span data-ttu-id="d92eb-272">Matriz de elementos de lista</span><span class="sxs-lookup"><span data-stu-id="d92eb-272">Array of list items</span></span> | <span data-ttu-id="d92eb-273">Conjunto de elementos aplicables a la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d92eb-273">Set of items applicable to the card.</span></span>|
| <span data-ttu-id="d92eb-274">botones</span><span class="sxs-lookup"><span data-stu-id="d92eb-274">buttons</span></span> | <span data-ttu-id="d92eb-275">Matriz de objetos de acción</span><span class="sxs-lookup"><span data-stu-id="d92eb-275">Array of action objects</span></span> | <span data-ttu-id="d92eb-276">Conjunto de acciones aplicables a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="d92eb-276">Set of actions applicable to the current card.</span></span> <span data-ttu-id="d92eb-277">Máximo 6.</span><span class="sxs-lookup"><span data-stu-id="d92eb-277">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="d92eb-278">Ejemplo de una tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="d92eb-278">Example of a list card</span></span>

<span data-ttu-id="d92eb-279">El siguiente código muestra un ejemplo de una tarjeta de lista:</span><span class="sxs-lookup"><span data-stu-id="d92eb-279">The following code shows an example of a list card:</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="d92eb-280">Office 365 de conector</span><span class="sxs-lookup"><span data-stu-id="d92eb-280">Office 365 connector card</span></span>

<span data-ttu-id="d92eb-281">Puede trabajar con una tarjeta Office 365 Connector que proporciona un diseño flexible y es una excelente manera de obtener información útil.</span><span class="sxs-lookup"><span data-stu-id="d92eb-281">You can work with an Office 365 Connector card that provides a flexible layout and is a great way to get useful information.</span></span> <span data-ttu-id="d92eb-282">La Office 365 de conector se admite en Teams, no en Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="d92eb-282">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="d92eb-283">Esta tarjeta proporciona un diseño flexible con varias secciones, campos, imágenes y acciones.</span><span class="sxs-lookup"><span data-stu-id="d92eb-283">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="d92eb-284">Esta tarjeta contiene una tarjeta de conector para que la puedan usar los bots.</span><span class="sxs-lookup"><span data-stu-id="d92eb-284">This card contains a connector card so that it can be used by bots.</span></span> <span data-ttu-id="d92eb-285">Para obtener más información sobre las diferencias entre las tarjetas de conector y la Office 365 connector, consulte Información adicional [sobre la Office 365 connector](#additional-information-on-the-office-365-connector-card).</span><span class="sxs-lookup"><span data-stu-id="d92eb-285">For differences between connector cards and the Office 365 Connector card, see [Additional information on the Office 365 Connector card](#additional-information-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="d92eb-286">Compatibilidad con tarjetas Office 365 Connector</span><span class="sxs-lookup"><span data-stu-id="d92eb-286">Support for Office 365 Connector cards</span></span>

<span data-ttu-id="d92eb-287">En la tabla siguiente se proporcionan las características que admiten Office 365 de conector:</span><span class="sxs-lookup"><span data-stu-id="d92eb-287">The following table provides the features that support Office 365 Connector cards:</span></span>

| <span data-ttu-id="d92eb-288">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="d92eb-288">Bots in Teams</span></span> | <span data-ttu-id="d92eb-289">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="d92eb-289">Messaging extensions</span></span>  | <span data-ttu-id="d92eb-290">Conectores</span><span class="sxs-lookup"><span data-stu-id="d92eb-290">Connectors</span></span> | <span data-ttu-id="d92eb-291">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="d92eb-291">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d92eb-292">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-292">✔</span></span> | <span data-ttu-id="d92eb-293">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-293">✔</span></span> | <span data-ttu-id="d92eb-294">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-294">✔</span></span> | <span data-ttu-id="d92eb-295">✖</span><span class="sxs-lookup"><span data-stu-id="d92eb-295">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="d92eb-296">Propiedades de la tarjeta Office 365 Connector</span><span class="sxs-lookup"><span data-stu-id="d92eb-296">Properties of the Office 365 Connector card</span></span>

<span data-ttu-id="d92eb-297">En la tabla siguiente se proporcionan las propiedades de la Office 365 de conector:</span><span class="sxs-lookup"><span data-stu-id="d92eb-297">The following table provides the properties of the Office 365 connector card:</span></span>

| <span data-ttu-id="d92eb-298">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d92eb-298">Property</span></span> | <span data-ttu-id="d92eb-299">Tipo</span><span class="sxs-lookup"><span data-stu-id="d92eb-299">Type</span></span>  | <span data-ttu-id="d92eb-300">Description</span><span class="sxs-lookup"><span data-stu-id="d92eb-300">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d92eb-301">title</span><span class="sxs-lookup"><span data-stu-id="d92eb-301">title</span></span> | <span data-ttu-id="d92eb-302">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="d92eb-302">Rich text</span></span> | <span data-ttu-id="d92eb-303">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d92eb-303">Title of the card.</span></span> <span data-ttu-id="d92eb-304">Máximo dos líneas.</span><span class="sxs-lookup"><span data-stu-id="d92eb-304">Maximum two lines.</span></span> |
| <span data-ttu-id="d92eb-305">summary</span><span class="sxs-lookup"><span data-stu-id="d92eb-305">summary</span></span> | <span data-ttu-id="d92eb-306">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="d92eb-306">Rich text</span></span> | <span data-ttu-id="d92eb-307">Resumen de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d92eb-307">Summary of the card.</span></span> <span data-ttu-id="d92eb-308">Máximo dos líneas.</span><span class="sxs-lookup"><span data-stu-id="d92eb-308">Maximum two lines.</span></span> |
| <span data-ttu-id="d92eb-309">text</span><span class="sxs-lookup"><span data-stu-id="d92eb-309">text</span></span> | <span data-ttu-id="d92eb-310">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="d92eb-310">Rich text</span></span> | <span data-ttu-id="d92eb-311">El texto aparece debajo del subtítulo.</span><span class="sxs-lookup"><span data-stu-id="d92eb-311">Text appears under the subtitle.</span></span> <span data-ttu-id="d92eb-312">Para ver las opciones de formato, vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="d92eb-312">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="d92eb-313">themeColor</span><span class="sxs-lookup"><span data-stu-id="d92eb-313">themeColor</span></span> | <span data-ttu-id="d92eb-314">Cadena HEX</span><span class="sxs-lookup"><span data-stu-id="d92eb-314">HEX string</span></span> | <span data-ttu-id="d92eb-315">Color que invalida el `accentColor` proporcionado desde el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d92eb-315">Color that overrides the `accentColor` provided from the application manifest.</span></span> |

### <a name="additional-information-on-the-office-365-connector-card"></a><span data-ttu-id="d92eb-316">Información adicional sobre la tarjeta Office 365 Connector</span><span class="sxs-lookup"><span data-stu-id="d92eb-316">Additional information on the Office 365 Connector card</span></span>

<span data-ttu-id="d92eb-317">Office 365 Las tarjetas de conector funcionan correctamente Microsoft Teams, incluidas las [ `ActionCard` acciones](/outlook/actionable-messages/card-reference#actioncard-action).</span><span class="sxs-lookup"><span data-stu-id="d92eb-317">Office 365 Connector cards function properly in Microsoft Teams, including [`ActionCard` actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="d92eb-318">La diferencia importante entre usar tarjetas de conector desde un conector y usar tarjetas de conector en el bot es el control de las acciones de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d92eb-318">The important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span> <span data-ttu-id="d92eb-319">En la tabla siguiente se muestra la diferencia:</span><span class="sxs-lookup"><span data-stu-id="d92eb-319">The following table lists the difference:</span></span>

| <span data-ttu-id="d92eb-320">Conector</span><span class="sxs-lookup"><span data-stu-id="d92eb-320">Connector</span></span> | <span data-ttu-id="d92eb-321">Bot</span><span class="sxs-lookup"><span data-stu-id="d92eb-321">Bot</span></span> |
| --- | --- |
| <span data-ttu-id="d92eb-322">El extremo recibe la carga de la tarjeta a través de HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="d92eb-322">The endpoint receives the card payload through HTTP POST.</span></span> | <span data-ttu-id="d92eb-323">La acción desencadena una actividad que envía solo el identificador de acción `HttpPOST` y el cuerpo al `invoke` bot.</span><span class="sxs-lookup"><span data-stu-id="d92eb-323">The `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>|

<span data-ttu-id="d92eb-324">Cada tarjeta de conector puede mostrar un máximo de diez secciones y cada sección puede contener un máximo de cinco imágenes y cinco acciones.</span><span class="sxs-lookup"><span data-stu-id="d92eb-324">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="d92eb-325">Las secciones, imágenes o acciones adicionales de un mensaje no aparecen.</span><span class="sxs-lookup"><span data-stu-id="d92eb-325">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="d92eb-326">Todos los campos de texto admiten Markdown y HTML.</span><span class="sxs-lookup"><span data-stu-id="d92eb-326">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="d92eb-327">Puede controlar qué secciones usan Markdown o HTML estableciendo la `markdown` propiedad en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="d92eb-327">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="d92eb-328">De forma predeterminada, `markdown` se establece en `true` .</span><span class="sxs-lookup"><span data-stu-id="d92eb-328">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="d92eb-329">Si quiere usar HTML en su lugar, establezca `markdown` en `false` .</span><span class="sxs-lookup"><span data-stu-id="d92eb-329">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="d92eb-330">Si especifica la `themeColor` propiedad, invalida la `accentColor` propiedad en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d92eb-330">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="d92eb-331">Para especificar el estilo de representación `activityImage` para , puede `activityImageType` establecerlo como se muestra en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="d92eb-331">To specify the rendering style for `activityImage`, you can set `activityImageType` as shown in the following table:</span></span>

| <span data-ttu-id="d92eb-332">Valor</span><span class="sxs-lookup"><span data-stu-id="d92eb-332">Value</span></span> | <span data-ttu-id="d92eb-333">Descripción</span><span class="sxs-lookup"><span data-stu-id="d92eb-333">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="d92eb-334">Valor predeterminado, `activityImage` se recorta como un círculo.</span><span class="sxs-lookup"><span data-stu-id="d92eb-334">Default, `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="d92eb-335">`activityImage` se muestra como un rectángulo y conserva su relación de aspecto.</span><span class="sxs-lookup"><span data-stu-id="d92eb-335">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="d92eb-336">Para obtener todos los demás detalles acerca de las propiedades de la tarjeta de conector, vea [referencia de tarjeta de mensaje que puede actuar.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="d92eb-336">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="d92eb-337">Las únicas propiedades de tarjeta de conector que Teams admite actualmente son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="d92eb-337">The only connector card properties that Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="d92eb-338">`startGroup`siempre tratado como `true` en Teams</span><span class="sxs-lookup"><span data-stu-id="d92eb-338">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="d92eb-339">Ejemplo de una tarjeta Office 365 Connector</span><span class="sxs-lookup"><span data-stu-id="d92eb-339">Example of an Office 365 Connector card</span></span>

<span data-ttu-id="d92eb-340">El siguiente código muestra un ejemplo de una tarjeta Office 365 Connector:</span><span class="sxs-lookup"><span data-stu-id="d92eb-340">The following code shows an example of an Office 365 Connector card:</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="d92eb-341">Tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="d92eb-341">Receipt card</span></span>

<span data-ttu-id="d92eb-342">Teams admite tarjeta de recibo.</span><span class="sxs-lookup"><span data-stu-id="d92eb-342">Teams supports receipt card.</span></span> <span data-ttu-id="d92eb-343">Es una tarjeta que permite a un bot proporcionar un recibo al usuario.</span><span class="sxs-lookup"><span data-stu-id="d92eb-343">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="d92eb-344">Normalmente contiene la lista de elementos que se deben incluir en el recibo, como impuestos y la información total.</span><span class="sxs-lookup"><span data-stu-id="d92eb-344">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="d92eb-345">Compatibilidad con tarjetas de recibo</span><span class="sxs-lookup"><span data-stu-id="d92eb-345">Support for receipt cards</span></span>

<span data-ttu-id="d92eb-346">En la tabla siguiente se proporcionan las características que admiten tarjetas de recibo:</span><span class="sxs-lookup"><span data-stu-id="d92eb-346">The following table provides the features that support receipt cards:</span></span>

| <span data-ttu-id="d92eb-347">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="d92eb-347">Bots in Teams</span></span> | <span data-ttu-id="d92eb-348">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="d92eb-348">Messaging extensions</span></span>  | <span data-ttu-id="d92eb-349">Conectores</span><span class="sxs-lookup"><span data-stu-id="d92eb-349">Connectors</span></span> | <span data-ttu-id="d92eb-350">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="d92eb-350">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d92eb-351">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-351">✔</span></span> | <span data-ttu-id="d92eb-352">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-352">✔</span></span> | <span data-ttu-id="d92eb-353">✖</span><span class="sxs-lookup"><span data-stu-id="d92eb-353">✖</span></span> | <span data-ttu-id="d92eb-354">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-354">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="d92eb-355">Ejemplo de una tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="d92eb-355">Example of a receipt card</span></span>

![Ejemplo de una tarjeta de recibo](~/assets/images/cards/receipt.png)

<span data-ttu-id="d92eb-357">El siguiente código muestra un ejemplo de una tarjeta de recibo:</span><span class="sxs-lookup"><span data-stu-id="d92eb-357">The following code shows an example of a receipt card:</span></span>

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="d92eb-358">Información adicional sobre tarjetas de recibo</span><span class="sxs-lookup"><span data-stu-id="d92eb-358">Additional information on receipt cards</span></span>

<span data-ttu-id="d92eb-359">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="d92eb-359">Bot Framework reference:</span></span>

* [<span data-ttu-id="d92eb-360">Tarjeta de recibo Node.js</span><span class="sxs-lookup"><span data-stu-id="d92eb-360">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="d92eb-361">Tarjeta de recibo C #</span><span class="sxs-lookup"><span data-stu-id="d92eb-361">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="d92eb-362">Tarjeta de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="d92eb-362">Signin card</span></span>

<span data-ttu-id="d92eb-363">La tarjeta de inicio de sesión en Teams es similar a la tarjeta de inicio de sesión en Bot Framework, excepto que la tarjeta de inicio de sesión en Teams solo admite dos `signin` acciones y `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="d92eb-363">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions `signin` and `openUrl`.</span></span>

<span data-ttu-id="d92eb-364">La acción de inicio de sesión se puede usar desde cualquier tarjeta de Teams, no solo desde la tarjeta de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="d92eb-364">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="d92eb-365">Para obtener más información, [vea Teams de autenticación para bots](~/bots/how-to/authentication/auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="d92eb-365">For more information, see [Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="d92eb-366">Compatibilidad con tarjetas de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="d92eb-366">Support for signin cards</span></span>

<span data-ttu-id="d92eb-367">En la tabla siguiente se proporcionan las características que admiten tarjetas de inicio de sesión:</span><span class="sxs-lookup"><span data-stu-id="d92eb-367">The following table provides the features that support signin cards:</span></span>

| <span data-ttu-id="d92eb-368">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="d92eb-368">Bots in Teams</span></span> | <span data-ttu-id="d92eb-369">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="d92eb-369">Messaging extensions</span></span>  | <span data-ttu-id="d92eb-370">Conectores</span><span class="sxs-lookup"><span data-stu-id="d92eb-370">Connectors</span></span> | <span data-ttu-id="d92eb-371">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="d92eb-371">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d92eb-372">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-372">✔</span></span> | <span data-ttu-id="d92eb-373">✖</span><span class="sxs-lookup"><span data-stu-id="d92eb-373">✖</span></span> | <span data-ttu-id="d92eb-374">✖</span><span class="sxs-lookup"><span data-stu-id="d92eb-374">✖</span></span> | <span data-ttu-id="d92eb-375">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-375">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="d92eb-376">Información adicional sobre tarjetas de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="d92eb-376">Additional information on signin cards</span></span>

<span data-ttu-id="d92eb-377">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="d92eb-377">Bot Framework reference:</span></span>

* [<span data-ttu-id="d92eb-378">Tarjeta de inicio de sesión Node.js</span><span class="sxs-lookup"><span data-stu-id="d92eb-378">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="d92eb-379">Tarjeta de inicio de sesión C #</span><span class="sxs-lookup"><span data-stu-id="d92eb-379">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="d92eb-380">Tarjeta miniatura</span><span class="sxs-lookup"><span data-stu-id="d92eb-380">Thumbnail card</span></span>

<span data-ttu-id="d92eb-381">Puedes trabajar con una tarjeta en miniatura que se usa para enviar un mensaje sencillo que puede usarse.</span><span class="sxs-lookup"><span data-stu-id="d92eb-381">You can work with a thumbnail card that is used for sending a simple actionable message.</span></span> <span data-ttu-id="d92eb-382">Una tarjeta que normalmente contiene una sola imagen en miniatura, uno o varios botones y texto.</span><span class="sxs-lookup"><span data-stu-id="d92eb-382">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="d92eb-383">Compatibilidad con tarjetas en miniatura</span><span class="sxs-lookup"><span data-stu-id="d92eb-383">Support for thumbnail cards</span></span>

<span data-ttu-id="d92eb-384">En la tabla siguiente se proporcionan las características que admiten tarjetas en miniatura:</span><span class="sxs-lookup"><span data-stu-id="d92eb-384">The following table provides the features that support thumbnail cards:</span></span>

| <span data-ttu-id="d92eb-385">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="d92eb-385">Bots in Teams</span></span> | <span data-ttu-id="d92eb-386">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="d92eb-386">Messaging extensions</span></span>  | <span data-ttu-id="d92eb-387">Conectores</span><span class="sxs-lookup"><span data-stu-id="d92eb-387">Connectors</span></span> | <span data-ttu-id="d92eb-388">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="d92eb-388">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d92eb-389">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-389">✔</span></span> | <span data-ttu-id="d92eb-390">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-390">✔</span></span> | <span data-ttu-id="d92eb-391">✖</span><span class="sxs-lookup"><span data-stu-id="d92eb-391">✖</span></span> | <span data-ttu-id="d92eb-392">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-392">✔</span></span> |

![Ejemplo de una tarjeta en miniatura](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="d92eb-394">Propiedades de una tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="d92eb-394">Properties of a thumbnail card</span></span>

<span data-ttu-id="d92eb-395">En la tabla siguiente se proporcionan las propiedades de una tarjeta en miniatura:</span><span class="sxs-lookup"><span data-stu-id="d92eb-395">The following table provides the properties of a thumbnail card:</span></span>

| <span data-ttu-id="d92eb-396">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d92eb-396">Property</span></span> | <span data-ttu-id="d92eb-397">Tipo</span><span class="sxs-lookup"><span data-stu-id="d92eb-397">Type</span></span>  | <span data-ttu-id="d92eb-398">Description</span><span class="sxs-lookup"><span data-stu-id="d92eb-398">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d92eb-399">title</span><span class="sxs-lookup"><span data-stu-id="d92eb-399">title</span></span> | <span data-ttu-id="d92eb-400">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="d92eb-400">Rich text</span></span> | <span data-ttu-id="d92eb-401">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d92eb-401">Title of the card.</span></span> <span data-ttu-id="d92eb-402">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="d92eb-402">Maximum 2 lines.</span></span>|
| <span data-ttu-id="d92eb-403">subtitle</span><span class="sxs-lookup"><span data-stu-id="d92eb-403">subtitle</span></span> | <span data-ttu-id="d92eb-404">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="d92eb-404">Rich text</span></span> | <span data-ttu-id="d92eb-405">Subtítulo de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d92eb-405">Subtitle of the card.</span></span> <span data-ttu-id="d92eb-406">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="d92eb-406">Maximum 2 lines.</span></span>|
| <span data-ttu-id="d92eb-407">text</span><span class="sxs-lookup"><span data-stu-id="d92eb-407">text</span></span> | <span data-ttu-id="d92eb-408">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="d92eb-408">Rich text</span></span> | <span data-ttu-id="d92eb-409">El texto aparece debajo del subtítulo.</span><span class="sxs-lookup"><span data-stu-id="d92eb-409">Text appears under the subtitle.</span></span> <span data-ttu-id="d92eb-410">Para ver las opciones de formato, vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="d92eb-410">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="d92eb-411">imágenes</span><span class="sxs-lookup"><span data-stu-id="d92eb-411">images</span></span> | <span data-ttu-id="d92eb-412">Matriz de imágenes</span><span class="sxs-lookup"><span data-stu-id="d92eb-412">Array of images</span></span> | <span data-ttu-id="d92eb-413">Imagen que se muestra en la parte superior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d92eb-413">Image displayed at the top of the card.</span></span> <span data-ttu-id="d92eb-414">Relación de aspecto 1:1 cuadrado.</span><span class="sxs-lookup"><span data-stu-id="d92eb-414">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="d92eb-415">botones</span><span class="sxs-lookup"><span data-stu-id="d92eb-415">buttons</span></span> | <span data-ttu-id="d92eb-416">Matriz de objetos de acción</span><span class="sxs-lookup"><span data-stu-id="d92eb-416">Array of action objects</span></span> | <span data-ttu-id="d92eb-417">Conjunto de acciones aplicables a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="d92eb-417">Set of actions applicable to the current card.</span></span> <span data-ttu-id="d92eb-418">Máximo 6.</span><span class="sxs-lookup"><span data-stu-id="d92eb-418">Maximum 6.</span></span> |
| <span data-ttu-id="d92eb-419">pulsación</span><span class="sxs-lookup"><span data-stu-id="d92eb-419">tap</span></span> | <span data-ttu-id="d92eb-420">Action (objeto)</span><span class="sxs-lookup"><span data-stu-id="d92eb-420">Action object</span></span> | <span data-ttu-id="d92eb-421">Se activa cuando el usuario pulsa en la propia tarjeta.</span><span class="sxs-lookup"><span data-stu-id="d92eb-421">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="d92eb-422">Ejemplo de una tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="d92eb-422">Example of a thumbnail card</span></span>

<span data-ttu-id="d92eb-423">El código siguiente muestra un ejemplo de una tarjeta en miniatura:</span><span class="sxs-lookup"><span data-stu-id="d92eb-423">The following code shows an example of a thumbnail card:</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="d92eb-424">Información adicional</span><span class="sxs-lookup"><span data-stu-id="d92eb-424">Additional information</span></span>

<span data-ttu-id="d92eb-425">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="d92eb-425">Bot Framework reference:</span></span>

* [<span data-ttu-id="d92eb-426">Tarjeta en miniatura Node.js</span><span class="sxs-lookup"><span data-stu-id="d92eb-426">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="d92eb-427">Tarjeta de miniatura C #</span><span class="sxs-lookup"><span data-stu-id="d92eb-427">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="d92eb-428">Colecciones de tarjetas</span><span class="sxs-lookup"><span data-stu-id="d92eb-428">Card collections</span></span>

<span data-ttu-id="d92eb-429">Puede trabajar con colecciones de tarjetas que incluyen colecciones de carrusel y listas.</span><span class="sxs-lookup"><span data-stu-id="d92eb-429">You can work with card collections that include carousel and list collections.</span></span> <span data-ttu-id="d92eb-430">Teams admite colecciones de tarjetas.</span><span class="sxs-lookup"><span data-stu-id="d92eb-430">Teams supports card collections.</span></span> <span data-ttu-id="d92eb-431">Las colecciones de tarjetas `builder.AttachmentLayout.carousel` incluyen y `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="d92eb-431">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="d92eb-432">Estas colecciones contienen tarjetas adaptables, de héroe o en miniatura.</span><span class="sxs-lookup"><span data-stu-id="d92eb-432">These collections contain Adaptive, hero, or thumbnail cards.</span></span>

### <a name="carousel-collection"></a><span data-ttu-id="d92eb-433">Colección Carousel</span><span class="sxs-lookup"><span data-stu-id="d92eb-433">Carousel collection</span></span>

<span data-ttu-id="d92eb-434">El [diseño del carrusel](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) muestra un carrusel de tarjetas, opcionalmente con botones de acción asociados.</span><span class="sxs-lookup"><span data-stu-id="d92eb-434">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

#### <a name="support-for-carousel-collections"></a><span data-ttu-id="d92eb-435">Compatibilidad con colecciones de carrusel</span><span class="sxs-lookup"><span data-stu-id="d92eb-435">Support for carousel collections</span></span>

<span data-ttu-id="d92eb-436">En la tabla siguiente se proporcionan las características que admiten colecciones de carrusel:</span><span class="sxs-lookup"><span data-stu-id="d92eb-436">The following table provides the features that support carousel collections:</span></span>

| <span data-ttu-id="d92eb-437">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="d92eb-437">Bots in Teams</span></span> | <span data-ttu-id="d92eb-438">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="d92eb-438">Messaging extensions</span></span>  | <span data-ttu-id="d92eb-439">Conectores</span><span class="sxs-lookup"><span data-stu-id="d92eb-439">Connectors</span></span> | <span data-ttu-id="d92eb-440">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="d92eb-440">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d92eb-441">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-441">✔</span></span> | <span data-ttu-id="d92eb-442">✖</span><span class="sxs-lookup"><span data-stu-id="d92eb-442">✖</span></span> | <span data-ttu-id="d92eb-443">✖</span><span class="sxs-lookup"><span data-stu-id="d92eb-443">✖</span></span> | <span data-ttu-id="d92eb-444">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-444">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="d92eb-445">Un carrusel puede mostrar un máximo de diez tarjetas por mensaje.</span><span class="sxs-lookup"><span data-stu-id="d92eb-445">A carousel can display a maximum of ten cards per message.</span></span>

#### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="d92eb-446">Propiedades de una tarjeta de carrusel</span><span class="sxs-lookup"><span data-stu-id="d92eb-446">Properties of a carousel card</span></span>

<span data-ttu-id="d92eb-447">Las propiedades de una tarjeta de carrusel son las mismas que las tarjetas de miniatura y de héroe.</span><span class="sxs-lookup"><span data-stu-id="d92eb-447">Properties of a carousel card are same as the hero and thumbnail cards.</span></span>

#### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="d92eb-448">Ejemplo de una colección de carrusel</span><span class="sxs-lookup"><span data-stu-id="d92eb-448">Example of a carousel collection</span></span>

![Ejemplo de un carrusel de tarjetas](~/assets/images/cards/carousel.png)

<span data-ttu-id="d92eb-450">El código siguiente muestra un ejemplo de una colección de carrusel:</span><span class="sxs-lookup"><span data-stu-id="d92eb-450">The following code shows an example of a carousel collection:</span></span>

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

#### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="d92eb-451">Sintaxis para colecciones de carrusel</span><span class="sxs-lookup"><span data-stu-id="d92eb-451">Syntax for carousel collections</span></span>

<span data-ttu-id="d92eb-452">`builder.AttachmentLayoutTypes.Carousel` es la sintaxis de las colecciones de carrusel.</span><span class="sxs-lookup"><span data-stu-id="d92eb-452">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

### <a name="list-collection"></a><span data-ttu-id="d92eb-453">Colección List</span><span class="sxs-lookup"><span data-stu-id="d92eb-453">List collection</span></span>

<span data-ttu-id="d92eb-454">El diseño de lista muestra una lista verticalmente apilada de tarjetas, opcionalmente con botones de acción asociados.</span><span class="sxs-lookup"><span data-stu-id="d92eb-454">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

#### <a name="support-for-list-collections"></a><span data-ttu-id="d92eb-455">Compatibilidad con colecciones de listas</span><span class="sxs-lookup"><span data-stu-id="d92eb-455">Support for list collections</span></span>

<span data-ttu-id="d92eb-456">En la tabla siguiente se proporcionan las características que admiten colecciones de listas:</span><span class="sxs-lookup"><span data-stu-id="d92eb-456">The following table provides the features that support list collections:</span></span>

| <span data-ttu-id="d92eb-457">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="d92eb-457">Bots in Teams</span></span> | <span data-ttu-id="d92eb-458">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="d92eb-458">Messaging extensions</span></span>  | <span data-ttu-id="d92eb-459">Conectores</span><span class="sxs-lookup"><span data-stu-id="d92eb-459">Connectors</span></span> | <span data-ttu-id="d92eb-460">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="d92eb-460">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d92eb-461">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-461">✔</span></span> | <span data-ttu-id="d92eb-462">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-462">✔</span></span> | <span data-ttu-id="d92eb-463">✖</span><span class="sxs-lookup"><span data-stu-id="d92eb-463">✖</span></span> | <span data-ttu-id="d92eb-464">✔</span><span class="sxs-lookup"><span data-stu-id="d92eb-464">✔</span></span> |

#### <a name="example-of-a-list-collection"></a><span data-ttu-id="d92eb-465">Ejemplo de una colección de listas</span><span class="sxs-lookup"><span data-stu-id="d92eb-465">Example of a list collection</span></span>

![Ejemplo de una lista de tarjetas](~/assets/images/cards/list.png)

<span data-ttu-id="d92eb-467">Las propiedades de las colecciones de listas son las mismas que las tarjetas de miniatura o de héroe.</span><span class="sxs-lookup"><span data-stu-id="d92eb-467">Properties of list collections are same as the hero or thumbnail cards.</span></span>

<span data-ttu-id="d92eb-468">Una lista puede mostrar un máximo de diez tarjetas por mensaje.</span><span class="sxs-lookup"><span data-stu-id="d92eb-468">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="d92eb-469">Algunas combinaciones de tarjetas de lista aún no son compatibles con iOS y Android.</span><span class="sxs-lookup"><span data-stu-id="d92eb-469">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

#### <a name="syntax-for-list-collections"></a><span data-ttu-id="d92eb-470">Sintaxis para colecciones de listas</span><span class="sxs-lookup"><span data-stu-id="d92eb-470">Syntax for list collections</span></span>

<span data-ttu-id="d92eb-471">`builder.AttachmentLayout.list` es la sintaxis de las colecciones de listas.</span><span class="sxs-lookup"><span data-stu-id="d92eb-471">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="d92eb-472">No se admiten tarjetas en Teams</span><span class="sxs-lookup"><span data-stu-id="d92eb-472">Cards not supported in Teams</span></span>

<span data-ttu-id="d92eb-473">Bot Framework implementa las siguientes tarjetas, pero no son compatibles con Teams:</span><span class="sxs-lookup"><span data-stu-id="d92eb-473">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="d92eb-474">Tarjetas de animación</span><span class="sxs-lookup"><span data-stu-id="d92eb-474">Animation cards</span></span>
* <span data-ttu-id="d92eb-475">Tarjetas de audio</span><span class="sxs-lookup"><span data-stu-id="d92eb-475">Audio cards</span></span>
* <span data-ttu-id="d92eb-476">Tarjetas de vídeo</span><span class="sxs-lookup"><span data-stu-id="d92eb-476">Video cards</span></span>

## <a name="see-also"></a><span data-ttu-id="d92eb-477">Vea también</span><span class="sxs-lookup"><span data-stu-id="d92eb-477">See also</span></span>

* [<span data-ttu-id="d92eb-478">Módulos de tareas</span><span class="sxs-lookup"><span data-stu-id="d92eb-478">Task modules</span></span>](~/task-modules-and-cards/what-are-task-modules.md)
* [<span data-ttu-id="d92eb-479">Dar formato a tarjetas</span><span class="sxs-lookup"><span data-stu-id="d92eb-479">Format cards</span></span>](~/task-modules-and-cards/cards/cards-format.md)

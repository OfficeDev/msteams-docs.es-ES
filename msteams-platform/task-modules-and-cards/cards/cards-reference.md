---
title: Tipos de tarjetas
description: Describe todas las tarjetas y acciones de tarjeta disponibles para bots en Teams
localization_priority: Normal
keywords: referencia de tarjetas bots
ms.topic: reference
ms.openlocfilehash: d3b84344eccee7c2595b0e978c72d7e331b198cb
ms.sourcegitcommit: b1f9162a0bbcd276064ae9e4f1e8bccc06cb7035
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/07/2021
ms.locfileid: "53328075"
---
# <a name="types-of-cards"></a><span data-ttu-id="e48ea-104">Tipos de tarjetas</span><span class="sxs-lookup"><span data-stu-id="e48ea-104">Types of cards</span></span>

<span data-ttu-id="e48ea-105">Adaptive, hero, list, Office 365 Connector, receipt, signin, and thumbnail cards and card collections are supported in bots for Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="e48ea-105">Adaptive, hero, list, Office 365 Connector, receipt, signin, and thumbnail cards and card collections are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="e48ea-106">Se basan en tarjetas definidas por Bot Framework, pero Teams no admite todas las tarjetas de Bot Framework y ha agregado algunas de sus propias.</span><span class="sxs-lookup"><span data-stu-id="e48ea-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span>

<span data-ttu-id="e48ea-107">Antes de identificar los distintos tipos de tarjeta, comprenda cómo crear una tarjeta de héroe, una tarjeta en miniatura o una tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="e48ea-107">Before you identify the different card types, understand how to create a a hero card, thumbnail card, or Adaptive Card.</span></span>

## <a name="create-a-hero-card-thumbnail-card-or-adaptive-card"></a><span data-ttu-id="e48ea-108">Crear una tarjeta de héroe, una tarjeta en miniatura o una tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="e48ea-108">Create a hero card, thumbnail card, or Adaptive Card</span></span>

<span data-ttu-id="e48ea-109">**Para crear una tarjeta de héroe, una miniatura o una tarjeta adaptable desde App Studio**</span><span class="sxs-lookup"><span data-stu-id="e48ea-109">**To create a hero card, thumbnail card, or Adaptive Card from App Studio**</span></span>

1. <span data-ttu-id="e48ea-110">Ve a **App Studio** desde Teams.</span><span class="sxs-lookup"><span data-stu-id="e48ea-110">Go to **App Studio** from Teams.</span></span>
1. <span data-ttu-id="e48ea-111">Seleccione **Editor de tarjetas**.</span><span class="sxs-lookup"><span data-stu-id="e48ea-111">Select **Card editor**.</span></span>
1. <span data-ttu-id="e48ea-112">Seleccione **Crear una nueva tarjeta**.</span><span class="sxs-lookup"><span data-stu-id="e48ea-112">Select **Create a new card**.</span></span>
1. <span data-ttu-id="e48ea-113">Seleccione **Crear** para una de las tarjetas de **hero card**, Thumbnail **Card** o Adaptive **Card**.</span><span class="sxs-lookup"><span data-stu-id="e48ea-113">Select **Create** for one of the cards from **Hero Card**, **Thumbnail Card**, or **Adaptive Card**.</span></span> <span data-ttu-id="e48ea-114">Los detalles de metadatos, los botones y los ejemplos de código json, csharp y node se muestran para esa tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e48ea-114">The metadata details, buttons, and json, csharp, and node code examples are shown for that card.</span></span>

    ![Detalles de la tarjeta de héroe](~/assets/images/Cards/Herocarddetails.png)

1. <span data-ttu-id="e48ea-116">Seleccione **Enviarme esta tarjeta**.</span><span class="sxs-lookup"><span data-stu-id="e48ea-116">Select **Send me this card**.</span></span> <span data-ttu-id="e48ea-117">La tarjeta se envía como un mensaje de chat.</span><span class="sxs-lookup"><span data-stu-id="e48ea-117">The card is sent to you as a chat message.</span></span>

## <a name="card-examples"></a><span data-ttu-id="e48ea-118">Ejemplos de tarjetas</span><span class="sxs-lookup"><span data-stu-id="e48ea-118">Card examples</span></span>

<span data-ttu-id="e48ea-119">Encontrará información adicional sobre cómo usar tarjetas en la documentación del SDK de Bot Builder v3.</span><span class="sxs-lookup"><span data-stu-id="e48ea-119">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="e48ea-120">Los ejemplos de código también están disponibles en el **repositorio microsoft/BotBuilder-Samples** en GitHub.</span><span class="sxs-lookup"><span data-stu-id="e48ea-120">Code samples are also available in the **Microsoft/BotBuilder-Samples** repository on GitHub.</span></span> <span data-ttu-id="e48ea-121">A continuación se muestran algunos ejemplos de tarjetas:</span><span class="sxs-lookup"><span data-stu-id="e48ea-121">Following are a few card examples:</span></span>

* <span data-ttu-id="e48ea-122">.NET</span><span class="sxs-lookup"><span data-stu-id="e48ea-122">.NET</span></span>
  * <span data-ttu-id="e48ea-123">[Agregar tarjetas como datos adjuntos a los mensajes](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="e48ea-123">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="e48ea-124">[Código de ejemplo de tarjetas Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="e48ea-124">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span></span>

* <span data-ttu-id="e48ea-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="e48ea-125">Node.js</span></span>
  * <span data-ttu-id="e48ea-126">[Agregar tarjetas como datos adjuntos a los mensajes](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="e48ea-126">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="e48ea-127">[Código de ejemplo de tarjetas Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="e48ea-127">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span></span>

## <a name="card-types"></a><span data-ttu-id="e48ea-128">Tipos de tarjeta</span><span class="sxs-lookup"><span data-stu-id="e48ea-128">Card types</span></span>

<span data-ttu-id="e48ea-129">Puede identificar y usar diferentes tipos de tarjetas según los requisitos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e48ea-129">You can identify and use different types of cards based on your application requirements.</span></span> <span data-ttu-id="e48ea-130">En la tabla siguiente se muestran los tipos de tarjetas disponibles:</span><span class="sxs-lookup"><span data-stu-id="e48ea-130">The following table shows the types of cards available to you:</span></span>

| <span data-ttu-id="e48ea-131">Tipo de tarjeta</span><span class="sxs-lookup"><span data-stu-id="e48ea-131">Card type</span></span> | <span data-ttu-id="e48ea-132">Descripción</span><span class="sxs-lookup"><span data-stu-id="e48ea-132">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="e48ea-133">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="e48ea-133">Adaptive Card</span></span>](#adaptive-card) | <span data-ttu-id="e48ea-134">Esta tarjeta es altamente personalizable y puede contener cualquier combinación de texto, voz, imágenes, botones y campos de entrada.</span><span class="sxs-lookup"><span data-stu-id="e48ea-134">This card is highly customizable and can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="e48ea-135">Tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="e48ea-135">Hero card</span></span>](#hero-card) | <span data-ttu-id="e48ea-136">Esta tarjeta normalmente contiene una sola imagen grande, uno o varios botones y una pequeña cantidad de texto.</span><span class="sxs-lookup"><span data-stu-id="e48ea-136">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="e48ea-137">Tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="e48ea-137">List card</span></span>](#list-card) | <span data-ttu-id="e48ea-138">Esta tarjeta contiene una lista de desplazamiento de elementos.</span><span class="sxs-lookup"><span data-stu-id="e48ea-138">This card contains a scrolling list of items.</span></span> |
| [<span data-ttu-id="e48ea-139">Office 365 Tarjeta de conector</span><span class="sxs-lookup"><span data-stu-id="e48ea-139">Office 365 Connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="e48ea-140">Esta tarjeta tiene un diseño flexible con varias secciones, campos, imágenes y acciones.</span><span class="sxs-lookup"><span data-stu-id="e48ea-140">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="e48ea-141">Tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="e48ea-141">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="e48ea-142">Esta tarjeta proporciona un recibo al usuario.</span><span class="sxs-lookup"><span data-stu-id="e48ea-142">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="e48ea-143">Tarjeta de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="e48ea-143">Signin card</span></span>](#signin-card) | <span data-ttu-id="e48ea-144">Esta tarjeta permite que un bot solicite que un usuario inicia sesión.</span><span class="sxs-lookup"><span data-stu-id="e48ea-144">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="e48ea-145">Tarjeta miniatura</span><span class="sxs-lookup"><span data-stu-id="e48ea-145">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="e48ea-146">Esta tarjeta normalmente contiene una sola imagen en miniatura, texto corto y uno o más botones.</span><span class="sxs-lookup"><span data-stu-id="e48ea-146">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="e48ea-147">Colecciones de tarjetas</span><span class="sxs-lookup"><span data-stu-id="e48ea-147">Card collections</span></span>](#card-collections) | <span data-ttu-id="e48ea-148">Esta colección de tarjetas se usa para devolver varios elementos en una sola respuesta.</span><span class="sxs-lookup"><span data-stu-id="e48ea-148">This card collection is used to return multiple items in a single response.</span></span> |

## <a name="features-that-support-different-card-types"></a><span data-ttu-id="e48ea-149">Características que admiten distintos tipos de tarjeta</span><span class="sxs-lookup"><span data-stu-id="e48ea-149">Features that support different card types</span></span>

| <span data-ttu-id="e48ea-150">Tipo de tarjeta</span><span class="sxs-lookup"><span data-stu-id="e48ea-150">Card type</span></span> | <span data-ttu-id="e48ea-151">Bots</span><span class="sxs-lookup"><span data-stu-id="e48ea-151">Bots</span></span> | <span data-ttu-id="e48ea-152">Vistas previas de extensión de mensaje</span><span class="sxs-lookup"><span data-stu-id="e48ea-152">Message extension previews</span></span> | <span data-ttu-id="e48ea-153">Resultados de extensión de mensaje</span><span class="sxs-lookup"><span data-stu-id="e48ea-153">Message extension results</span></span> | <span data-ttu-id="e48ea-154">Módulos de tareas</span><span class="sxs-lookup"><span data-stu-id="e48ea-154">Task modules</span></span> | <span data-ttu-id="e48ea-155">Webhooks salientes</span><span class="sxs-lookup"><span data-stu-id="e48ea-155">Outgoing Webhooks</span></span> | <span data-ttu-id="e48ea-156">Webhooks entrantes</span><span class="sxs-lookup"><span data-stu-id="e48ea-156">Incoming Webhooks</span></span> | <span data-ttu-id="e48ea-157">Conectores de O365</span><span class="sxs-lookup"><span data-stu-id="e48ea-157">O365 Connectors</span></span> |
| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="e48ea-158">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="e48ea-158">Adaptive Card</span></span> | <span data-ttu-id="e48ea-159">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-159">✔</span></span> | <span data-ttu-id="e48ea-160">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-160">✖</span></span> | <span data-ttu-id="e48ea-161">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-161">✔</span></span> | <span data-ttu-id="e48ea-162">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-162">✔</span></span> | <span data-ttu-id="e48ea-163">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-163">✔</span></span> | <span data-ttu-id="e48ea-164">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-164">✔</span></span> | <span data-ttu-id="e48ea-165">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-165">✖</span></span> |
| <span data-ttu-id="e48ea-166">Tarjeta O365 Connector</span><span class="sxs-lookup"><span data-stu-id="e48ea-166">O365 Connector card</span></span> | <span data-ttu-id="e48ea-167">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-167">✔</span></span> | <span data-ttu-id="e48ea-168">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-168">✖</span></span> | <span data-ttu-id="e48ea-169">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-169">✔</span></span> | <span data-ttu-id="e48ea-170">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-170">✖</span></span> | <span data-ttu-id="e48ea-171">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-171">✔</span></span> | <span data-ttu-id="e48ea-172">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-172">✔</span></span> | <span data-ttu-id="e48ea-173">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-173">✔</span></span> |
| <span data-ttu-id="e48ea-174">Tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="e48ea-174">Hero card</span></span> | <span data-ttu-id="e48ea-175">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-175">✔</span></span> | <span data-ttu-id="e48ea-176">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-176">✔</span></span> | <span data-ttu-id="e48ea-177">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-177">✔</span></span> | <span data-ttu-id="e48ea-178">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-178">✖</span></span> | <span data-ttu-id="e48ea-179">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-179">✔</span></span> | <span data-ttu-id="e48ea-180">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-180">✔</span></span> | <span data-ttu-id="e48ea-181">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-181">✖</span></span> |
| <span data-ttu-id="e48ea-182">Tarjeta miniatura</span><span class="sxs-lookup"><span data-stu-id="e48ea-182">Thumbnail card</span></span> | <span data-ttu-id="e48ea-183">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-183">✔</span></span> | <span data-ttu-id="e48ea-184">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-184">✔</span></span> | <span data-ttu-id="e48ea-185">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-185">✔</span></span> | <span data-ttu-id="e48ea-186">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-186">✖</span></span> | <span data-ttu-id="e48ea-187">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-187">✔</span></span> | <span data-ttu-id="e48ea-188">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-188">✔</span></span> | <span data-ttu-id="e48ea-189">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-189">✖</span></span> |
| <span data-ttu-id="e48ea-190">Tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="e48ea-190">List card</span></span> | <span data-ttu-id="e48ea-191">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-191">✔</span></span> | <span data-ttu-id="e48ea-192">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-192">✖</span></span> | <span data-ttu-id="e48ea-193">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-193">✖</span></span> | <span data-ttu-id="e48ea-194">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-194">✖</span></span> | <span data-ttu-id="e48ea-195">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-195">✔</span></span> | <span data-ttu-id="e48ea-196">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-196">✔</span></span> | <span data-ttu-id="e48ea-197">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-197">✖</span></span> |
| <span data-ttu-id="e48ea-198">Tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="e48ea-198">Receipt card</span></span> | <span data-ttu-id="e48ea-199">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-199">✔</span></span> | <span data-ttu-id="e48ea-200">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-200">✖</span></span> | <span data-ttu-id="e48ea-201">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-201">✖</span></span> | <span data-ttu-id="e48ea-202">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-202">✖</span></span> | <span data-ttu-id="e48ea-203">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-203">✖</span></span> | <span data-ttu-id="e48ea-204">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-204">✔</span></span> | <span data-ttu-id="e48ea-205">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-205">✖</span></span> |
| <span data-ttu-id="e48ea-206">Tarjeta de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="e48ea-206">Signin card</span></span> | <span data-ttu-id="e48ea-207">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-207">✔</span></span> | <span data-ttu-id="e48ea-208">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-208">✖</span></span> | <span data-ttu-id="e48ea-209">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-209">✖</span></span> | <span data-ttu-id="e48ea-210">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-210">✖</span></span> | <span data-ttu-id="e48ea-211">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-211">✖</span></span> | <span data-ttu-id="e48ea-212">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-212">✖</span></span> | <span data-ttu-id="e48ea-213">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-213">✖</span></span> |

> [!NOTE]
> <span data-ttu-id="e48ea-214">Para las tarjetas adaptables en webhooks entrantes, todos los elementos de esquema nativos de tarjeta adaptable, excepto `Action.Submit` , son totalmente compatibles.</span><span class="sxs-lookup"><span data-stu-id="e48ea-214">For Adaptive Cards in Incoming Webhooks, all native Adaptive Card schema elements, except `Action.Submit`, are fully supported.</span></span> <span data-ttu-id="e48ea-215">Las acciones admitidas [**son Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)y [**Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span><span class="sxs-lookup"><span data-stu-id="e48ea-215">The supported actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html), and [**Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span></span>

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="e48ea-216">Propiedades comunes para todas las tarjetas</span><span class="sxs-lookup"><span data-stu-id="e48ea-216">Common properties for all cards</span></span>

<span data-ttu-id="e48ea-217">Puedes ir a través de algunas propiedades comunes que son aplicables a todas las tarjetas.</span><span class="sxs-lookup"><span data-stu-id="e48ea-217">You can go through some common properties that are applicable to all cards.</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="e48ea-218">Imágenes de tarjetas en línea</span><span class="sxs-lookup"><span data-stu-id="e48ea-218">Inline card images</span></span>

<span data-ttu-id="e48ea-219">La tarjeta puede contener una imagen en línea al incluir un vínculo a la imagen disponible públicamente.</span><span class="sxs-lookup"><span data-stu-id="e48ea-219">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="e48ea-220">Por motivos de rendimiento, se recomienda hospedar la imagen en un servidor público Content Delivery Network (CDN).</span><span class="sxs-lookup"><span data-stu-id="e48ea-220">For performance purposes, it is highly recommended you host the image on a public Content Delivery Network (CDN).</span></span>

<span data-ttu-id="e48ea-221">Las imágenes se escalan hacia arriba o hacia abajo en tamaño para mantener la relación de aspecto para cubrir el área de imagen.</span><span class="sxs-lookup"><span data-stu-id="e48ea-221">Images are scaled up or down in size to maintain the aspect ratio for covering the image area.</span></span> <span data-ttu-id="e48ea-222">A continuación, las imágenes se recortan desde el centro para lograr la relación de aspecto adecuada para la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e48ea-222">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="e48ea-223">Las imágenes deben tener como máximo 1024×1024 y en formato PNG, JPEG o GIF.</span><span class="sxs-lookup"><span data-stu-id="e48ea-223">Images must be at most 1024×1024 and in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="e48ea-224">Gif animado no es compatible.</span><span class="sxs-lookup"><span data-stu-id="e48ea-224">Animated GIF is not supported.</span></span>

<span data-ttu-id="e48ea-225">En la tabla siguiente se proporcionan las propiedades de las imágenes de tarjetas en línea:</span><span class="sxs-lookup"><span data-stu-id="e48ea-225">The following table provides the properties of inline card images:</span></span>

| <span data-ttu-id="e48ea-226">Propiedad</span><span class="sxs-lookup"><span data-stu-id="e48ea-226">Property</span></span> | <span data-ttu-id="e48ea-227">Tipo</span><span class="sxs-lookup"><span data-stu-id="e48ea-227">Type</span></span>  | <span data-ttu-id="e48ea-228">Descripción</span><span class="sxs-lookup"><span data-stu-id="e48ea-228">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e48ea-229">url</span><span class="sxs-lookup"><span data-stu-id="e48ea-229">url</span></span> | <span data-ttu-id="e48ea-230">URL</span><span class="sxs-lookup"><span data-stu-id="e48ea-230">URL</span></span> | <span data-ttu-id="e48ea-231">DIRECCIÓN URL HTTPS a la imagen.</span><span class="sxs-lookup"><span data-stu-id="e48ea-231">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="e48ea-232">alt</span><span class="sxs-lookup"><span data-stu-id="e48ea-232">alt</span></span> | <span data-ttu-id="e48ea-233">Cadena</span><span class="sxs-lookup"><span data-stu-id="e48ea-233">String</span></span> | <span data-ttu-id="e48ea-234">Descripción accesible de la imagen.</span><span class="sxs-lookup"><span data-stu-id="e48ea-234">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="e48ea-235">Si una tarjeta incluye una dirección URL de imagen que se redirige antes de la imagen final, no se admite el redireccionamiento en la dirección URL de la imagen.</span><span class="sxs-lookup"><span data-stu-id="e48ea-235">If a card includes an image URL that is redirected before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="e48ea-236">Esto ocurre para las imágenes compartidas en la nube pública.</span><span class="sxs-lookup"><span data-stu-id="e48ea-236">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="e48ea-237">Botones</span><span class="sxs-lookup"><span data-stu-id="e48ea-237">Buttons</span></span>

<span data-ttu-id="e48ea-238">Los botones se muestran apilados en la parte inferior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e48ea-238">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="e48ea-239">El texto del botón siempre está en una sola línea y se trunca si el texto supera el ancho del botón.</span><span class="sxs-lookup"><span data-stu-id="e48ea-239">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="e48ea-240">No se muestran los botones adicionales que supere el número máximo admitido por la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e48ea-240">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="e48ea-241">Para obtener más información, vea [acciones de tarjeta](~/task-modules-and-cards/cards/cards-actions.md).</span><span class="sxs-lookup"><span data-stu-id="e48ea-241">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="e48ea-242">Formato de tarjeta</span><span class="sxs-lookup"><span data-stu-id="e48ea-242">Card formatting</span></span>

<span data-ttu-id="e48ea-243">Para obtener más información sobre el formato de texto en tarjetas, vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="e48ea-243">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

<span data-ttu-id="e48ea-244">Después de identificar las propiedades comunes de todas las tarjetas, ahora puedes trabajar con tarjetas adaptables, lo que te ayudará a aumentar la interacción y la eficacia agregando el contenido que se puede usar directamente en las aplicaciones que usas.</span><span class="sxs-lookup"><span data-stu-id="e48ea-244">After identifying the common properties for all cards, you can now work with Adaptive Cards, which help you increase engagement and efficiency by adding your actionable content directly into the apps you use.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="e48ea-245">Tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="e48ea-245">Adaptive Card</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/J12lKt717Ws]

<span data-ttu-id="e48ea-246">Una tarjeta adaptable es una tarjeta personalizable que puede contener cualquier combinación de texto, voz, imágenes, botones y campos de entrada.</span><span class="sxs-lookup"><span data-stu-id="e48ea-246">An Adaptive Card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="e48ea-247">Para obtener más información, vea [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="e48ea-247">For more information, see [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="e48ea-248">Compatibilidad con tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="e48ea-248">Support for Adaptive Cards</span></span>

<span data-ttu-id="e48ea-249">En la tabla siguiente se proporcionan las características que admiten tarjetas adaptables:</span><span class="sxs-lookup"><span data-stu-id="e48ea-249">The following table provides the features that support Adaptive Cards:</span></span>

| <span data-ttu-id="e48ea-250">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="e48ea-250">Bots in Teams</span></span> | <span data-ttu-id="e48ea-251">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="e48ea-251">Messaging extensions</span></span>  | <span data-ttu-id="e48ea-252">Conectores</span><span class="sxs-lookup"><span data-stu-id="e48ea-252">Connectors</span></span> | <span data-ttu-id="e48ea-253">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="e48ea-253">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e48ea-254">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-254">✔</span></span> | <span data-ttu-id="e48ea-255">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-255">✔</span></span> | <span data-ttu-id="e48ea-256">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-256">✖</span></span> | <span data-ttu-id="e48ea-257">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-257">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="e48ea-258">Teams plataforma admite v1.2 o versiones anteriores de características de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="e48ea-258">Teams platform supports v1.2 or earlier of Adaptive Card features.</span></span>
> * <span data-ttu-id="e48ea-259">El estilo de acción positiva o destructiva no se admite en tarjetas adaptables en la Teams web.</span><span class="sxs-lookup"><span data-stu-id="e48ea-259">Positive or destructive action styling is not supported in Adaptive Cards on the Teams platform.</span></span>
> * <span data-ttu-id="e48ea-260">Actualmente, los elementos multimedia no se admiten en la tarjeta adaptable en Teams plataforma.</span><span class="sxs-lookup"><span data-stu-id="e48ea-260">Media elements are currently not supported in Adaptive Card on the Teams platform.</span></span>

### <a name="example-of-adaptive-card"></a><span data-ttu-id="e48ea-261">Ejemplo de tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="e48ea-261">Example of Adaptive Card</span></span>

![Ejemplo de una tarjeta adaptable](~/assets/images/cards/adaptivecard.png)

<span data-ttu-id="e48ea-263">El código siguiente muestra un ejemplo de una tarjeta adaptable:</span><span class="sxs-lookup"><span data-stu-id="e48ea-263">The following code shows an example of an Adaptive Card:</span></span>

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="e48ea-264">Información adicional sobre tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="e48ea-264">Additional information on Adaptive Cards</span></span>

<span data-ttu-id="e48ea-265">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="e48ea-265">Bot Framework reference:</span></span>

* [<span data-ttu-id="e48ea-266">Nodo de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="e48ea-266">Adaptive Cards Node</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="e48ea-267">Tarjeta adaptable C #</span><span class="sxs-lookup"><span data-stu-id="e48ea-267">Adaptive Card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

<span data-ttu-id="e48ea-268">Ahora puedes trabajar con una tarjeta de héroe, que es una tarjeta multipropósito que se usa para resaltar visualmente una selección de usuario potencial.</span><span class="sxs-lookup"><span data-stu-id="e48ea-268">You can now work with a hero card, which is a multipurpose card used to visually highlight a potential user selection.</span></span>

## <a name="hero-card"></a><span data-ttu-id="e48ea-269">Tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="e48ea-269">Hero card</span></span>

<span data-ttu-id="e48ea-270">Una tarjeta que normalmente contiene una sola imagen grande, uno o varios botones y texto.</span><span class="sxs-lookup"><span data-stu-id="e48ea-270">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="e48ea-271">Compatibilidad con tarjetas de héroe</span><span class="sxs-lookup"><span data-stu-id="e48ea-271">Support for hero cards</span></span>

<span data-ttu-id="e48ea-272">En la tabla siguiente se proporcionan las características que admiten tarjetas de héroe:</span><span class="sxs-lookup"><span data-stu-id="e48ea-272">The following table provides the features that support hero cards:</span></span>

| <span data-ttu-id="e48ea-273">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="e48ea-273">Bots in Teams</span></span> | <span data-ttu-id="e48ea-274">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="e48ea-274">Messaging extensions</span></span>  | <span data-ttu-id="e48ea-275">Conectores</span><span class="sxs-lookup"><span data-stu-id="e48ea-275">Connectors</span></span> | <span data-ttu-id="e48ea-276">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="e48ea-276">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e48ea-277">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-277">✔</span></span> | <span data-ttu-id="e48ea-278">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-278">✔</span></span> | <span data-ttu-id="e48ea-279">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-279">✖</span></span> | <span data-ttu-id="e48ea-280">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-280">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="e48ea-281">Propiedades de una tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="e48ea-281">Properties of a hero card</span></span>

<span data-ttu-id="e48ea-282">En la tabla siguiente se proporcionan las propiedades de una tarjeta de héroe:</span><span class="sxs-lookup"><span data-stu-id="e48ea-282">The following table provides the properties of a hero card:</span></span>

| <span data-ttu-id="e48ea-283">Propiedad</span><span class="sxs-lookup"><span data-stu-id="e48ea-283">Property</span></span> | <span data-ttu-id="e48ea-284">Tipo</span><span class="sxs-lookup"><span data-stu-id="e48ea-284">Type</span></span>  | <span data-ttu-id="e48ea-285">Description</span><span class="sxs-lookup"><span data-stu-id="e48ea-285">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e48ea-286">title</span><span class="sxs-lookup"><span data-stu-id="e48ea-286">title</span></span> | <span data-ttu-id="e48ea-287">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="e48ea-287">Rich text</span></span> | <span data-ttu-id="e48ea-288">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e48ea-288">Title of the card.</span></span> <span data-ttu-id="e48ea-289">Máximo dos líneas.</span><span class="sxs-lookup"><span data-stu-id="e48ea-289">Maximum two lines.</span></span> |
| <span data-ttu-id="e48ea-290">subtitle</span><span class="sxs-lookup"><span data-stu-id="e48ea-290">subtitle</span></span> | <span data-ttu-id="e48ea-291">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="e48ea-291">Rich text</span></span> | <span data-ttu-id="e48ea-292">Subtítulo de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e48ea-292">Subtitle of the card.</span></span> <span data-ttu-id="e48ea-293">Máximo dos líneas.</span><span class="sxs-lookup"><span data-stu-id="e48ea-293">Maximum two lines.</span></span>|
| <span data-ttu-id="e48ea-294">text</span><span class="sxs-lookup"><span data-stu-id="e48ea-294">text</span></span> | <span data-ttu-id="e48ea-295">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="e48ea-295">Rich text</span></span> | <span data-ttu-id="e48ea-296">El texto aparece debajo del subtítulo.</span><span class="sxs-lookup"><span data-stu-id="e48ea-296">Text appears under the subtitle.</span></span> <span data-ttu-id="e48ea-297">Para ver las opciones de formato, vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="e48ea-297">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="e48ea-298">imágenes</span><span class="sxs-lookup"><span data-stu-id="e48ea-298">images</span></span> | <span data-ttu-id="e48ea-299">Matriz de imágenes</span><span class="sxs-lookup"><span data-stu-id="e48ea-299">Array of images</span></span> | <span data-ttu-id="e48ea-300">Imagen que se muestra en la parte superior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e48ea-300">Image displayed at the top of the card.</span></span> <span data-ttu-id="e48ea-301">Relación de aspecto 16:9.</span><span class="sxs-lookup"><span data-stu-id="e48ea-301">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="e48ea-302">botones</span><span class="sxs-lookup"><span data-stu-id="e48ea-302">buttons</span></span> | <span data-ttu-id="e48ea-303">Matriz de objetos de acción</span><span class="sxs-lookup"><span data-stu-id="e48ea-303">Array of action objects</span></span> | <span data-ttu-id="e48ea-304">Conjunto de acciones aplicables a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="e48ea-304">Set of actions applicable to the current card.</span></span> <span data-ttu-id="e48ea-305">Máximo seis.</span><span class="sxs-lookup"><span data-stu-id="e48ea-305">Maximum six.</span></span> |
| <span data-ttu-id="e48ea-306">pulsación</span><span class="sxs-lookup"><span data-stu-id="e48ea-306">tap</span></span> | <span data-ttu-id="e48ea-307">Action (objeto)</span><span class="sxs-lookup"><span data-stu-id="e48ea-307">Action object</span></span> | <span data-ttu-id="e48ea-308">Se activa cuando el usuario pulsa en la propia tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e48ea-308">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="e48ea-309">Ejemplo de una tarjeta de héroe</span><span class="sxs-lookup"><span data-stu-id="e48ea-309">Example of a hero card</span></span>

![Ejemplo de una tarjeta de héroe](~/assets/images/cards/hero.png)

<span data-ttu-id="e48ea-311">El siguiente código muestra un ejemplo de una tarjeta de héroe:</span><span class="sxs-lookup"><span data-stu-id="e48ea-311">The following code shows an example of a hero card:</span></span>

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="e48ea-312">Información adicional sobre tarjetas de héroe</span><span class="sxs-lookup"><span data-stu-id="e48ea-312">Additional information on hero cards</span></span>

<span data-ttu-id="e48ea-313">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="e48ea-313">Bot Framework reference:</span></span>

* [<span data-ttu-id="e48ea-314">Tarjeta de Node.js</span><span class="sxs-lookup"><span data-stu-id="e48ea-314">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="e48ea-315">Tarjeta de héroe C #</span><span class="sxs-lookup"><span data-stu-id="e48ea-315">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="e48ea-316">Tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="e48ea-316">List card</span></span>

<span data-ttu-id="e48ea-317">La tarjeta de lista se ha agregado Teams para proporcionar funciones más allá de lo que la colección de listas puede proporcionar.</span><span class="sxs-lookup"><span data-stu-id="e48ea-317">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="e48ea-318">La tarjeta de lista proporciona una lista de desplazamiento de elementos.</span><span class="sxs-lookup"><span data-stu-id="e48ea-318">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="e48ea-319">Compatibilidad con tarjetas de lista</span><span class="sxs-lookup"><span data-stu-id="e48ea-319">Support for list cards</span></span>

<span data-ttu-id="e48ea-320">En la tabla siguiente se proporcionan las características que admiten tarjetas de lista:</span><span class="sxs-lookup"><span data-stu-id="e48ea-320">The following table provides the features that support list cards:</span></span>

| <span data-ttu-id="e48ea-321">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="e48ea-321">Bots in Teams</span></span> | <span data-ttu-id="e48ea-322">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="e48ea-322">Messaging extensions</span></span>  | <span data-ttu-id="e48ea-323">Conectores</span><span class="sxs-lookup"><span data-stu-id="e48ea-323">Connectors</span></span> | <span data-ttu-id="e48ea-324">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="e48ea-324">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e48ea-325">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-325">✔</span></span> | <span data-ttu-id="e48ea-326">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-326">✖</span></span> | <span data-ttu-id="e48ea-327">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-327">✖</span></span> |<span data-ttu-id="e48ea-328">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-328">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="e48ea-329">Propiedades de una tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="e48ea-329">Properties of a list card</span></span>

<span data-ttu-id="e48ea-330">En la tabla siguiente se proporcionan las propiedades de una tarjeta de lista:</span><span class="sxs-lookup"><span data-stu-id="e48ea-330">The following table provides the properties of a list card:</span></span>

| <span data-ttu-id="e48ea-331">Propiedad</span><span class="sxs-lookup"><span data-stu-id="e48ea-331">Property</span></span> | <span data-ttu-id="e48ea-332">Tipo</span><span class="sxs-lookup"><span data-stu-id="e48ea-332">Type</span></span>  | <span data-ttu-id="e48ea-333">Description</span><span class="sxs-lookup"><span data-stu-id="e48ea-333">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e48ea-334">title</span><span class="sxs-lookup"><span data-stu-id="e48ea-334">title</span></span> | <span data-ttu-id="e48ea-335">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="e48ea-335">Rich text</span></span> | <span data-ttu-id="e48ea-336">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e48ea-336">Title of the card.</span></span> <span data-ttu-id="e48ea-337">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="e48ea-337">Maximum 2 lines.</span></span>|
| <span data-ttu-id="e48ea-338">elementos</span><span class="sxs-lookup"><span data-stu-id="e48ea-338">items</span></span> | <span data-ttu-id="e48ea-339">Matriz de elementos de lista</span><span class="sxs-lookup"><span data-stu-id="e48ea-339">Array of list items</span></span> | <span data-ttu-id="e48ea-340">Conjunto de elementos aplicables a la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e48ea-340">Set of items applicable to the card.</span></span>|
| <span data-ttu-id="e48ea-341">botones</span><span class="sxs-lookup"><span data-stu-id="e48ea-341">buttons</span></span> | <span data-ttu-id="e48ea-342">Matriz de objetos de acción</span><span class="sxs-lookup"><span data-stu-id="e48ea-342">Array of action objects</span></span> | <span data-ttu-id="e48ea-343">Conjunto de acciones aplicables a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="e48ea-343">Set of actions applicable to the current card.</span></span> <span data-ttu-id="e48ea-344">Máximo 6.</span><span class="sxs-lookup"><span data-stu-id="e48ea-344">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="e48ea-345">Ejemplo de una tarjeta de lista</span><span class="sxs-lookup"><span data-stu-id="e48ea-345">Example of a list card</span></span>

<span data-ttu-id="e48ea-346">El siguiente código muestra un ejemplo de una tarjeta de lista:</span><span class="sxs-lookup"><span data-stu-id="e48ea-346">The following code shows an example of a list card:</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="e48ea-347">Office 365 de conector</span><span class="sxs-lookup"><span data-stu-id="e48ea-347">Office 365 connector card</span></span>

<span data-ttu-id="e48ea-348">Puede trabajar con una tarjeta Office 365 Connector que proporciona un diseño flexible y es una excelente manera de obtener información útil.</span><span class="sxs-lookup"><span data-stu-id="e48ea-348">You can work with an Office 365 Connector card that provides a flexible layout and is a great way to get useful information.</span></span> <span data-ttu-id="e48ea-349">La Office 365 de conector se admite en Teams, no en Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="e48ea-349">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="e48ea-350">Esta tarjeta proporciona un diseño flexible con varias secciones, campos, imágenes y acciones.</span><span class="sxs-lookup"><span data-stu-id="e48ea-350">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="e48ea-351">Esta tarjeta contiene una tarjeta de conector para que la puedan usar los bots.</span><span class="sxs-lookup"><span data-stu-id="e48ea-351">This card contains a connector card so that it can be used by bots.</span></span> <span data-ttu-id="e48ea-352">Para obtener más información sobre las diferencias entre las tarjetas de conector y la Office 365 connector, consulte Información adicional [sobre la Office 365 connector](#additional-information-on-the-office-365-connector-card).</span><span class="sxs-lookup"><span data-stu-id="e48ea-352">For differences between connector cards and the Office 365 Connector card, see [Additional information on the Office 365 Connector card](#additional-information-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="e48ea-353">Compatibilidad con tarjetas Office 365 Connector</span><span class="sxs-lookup"><span data-stu-id="e48ea-353">Support for Office 365 Connector cards</span></span>

<span data-ttu-id="e48ea-354">En la tabla siguiente se proporcionan las características que admiten Office 365 de conector:</span><span class="sxs-lookup"><span data-stu-id="e48ea-354">The following table provides the features that support Office 365 Connector cards:</span></span>

| <span data-ttu-id="e48ea-355">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="e48ea-355">Bots in Teams</span></span> | <span data-ttu-id="e48ea-356">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="e48ea-356">Messaging extensions</span></span>  | <span data-ttu-id="e48ea-357">Conectores</span><span class="sxs-lookup"><span data-stu-id="e48ea-357">Connectors</span></span> | <span data-ttu-id="e48ea-358">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="e48ea-358">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e48ea-359">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-359">✔</span></span> | <span data-ttu-id="e48ea-360">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-360">✔</span></span> | <span data-ttu-id="e48ea-361">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-361">✔</span></span> | <span data-ttu-id="e48ea-362">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-362">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="e48ea-363">Propiedades de la tarjeta Office 365 Connector</span><span class="sxs-lookup"><span data-stu-id="e48ea-363">Properties of the Office 365 Connector card</span></span>

<span data-ttu-id="e48ea-364">En la tabla siguiente se proporcionan las propiedades de la Office 365 de conector:</span><span class="sxs-lookup"><span data-stu-id="e48ea-364">The following table provides the properties of the Office 365 connector card:</span></span>

| <span data-ttu-id="e48ea-365">Propiedad</span><span class="sxs-lookup"><span data-stu-id="e48ea-365">Property</span></span> | <span data-ttu-id="e48ea-366">Tipo</span><span class="sxs-lookup"><span data-stu-id="e48ea-366">Type</span></span>  | <span data-ttu-id="e48ea-367">Description</span><span class="sxs-lookup"><span data-stu-id="e48ea-367">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e48ea-368">title</span><span class="sxs-lookup"><span data-stu-id="e48ea-368">title</span></span> | <span data-ttu-id="e48ea-369">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="e48ea-369">Rich text</span></span> | <span data-ttu-id="e48ea-370">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e48ea-370">Title of the card.</span></span> <span data-ttu-id="e48ea-371">Máximo dos líneas.</span><span class="sxs-lookup"><span data-stu-id="e48ea-371">Maximum two lines.</span></span> |
| <span data-ttu-id="e48ea-372">summary</span><span class="sxs-lookup"><span data-stu-id="e48ea-372">summary</span></span> | <span data-ttu-id="e48ea-373">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="e48ea-373">Rich text</span></span> | <span data-ttu-id="e48ea-374">Resumen de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e48ea-374">Summary of the card.</span></span> <span data-ttu-id="e48ea-375">Máximo dos líneas.</span><span class="sxs-lookup"><span data-stu-id="e48ea-375">Maximum two lines.</span></span> |
| <span data-ttu-id="e48ea-376">text</span><span class="sxs-lookup"><span data-stu-id="e48ea-376">text</span></span> | <span data-ttu-id="e48ea-377">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="e48ea-377">Rich text</span></span> | <span data-ttu-id="e48ea-378">El texto aparece debajo del subtítulo.</span><span class="sxs-lookup"><span data-stu-id="e48ea-378">Text appears under the subtitle.</span></span> <span data-ttu-id="e48ea-379">Para ver las opciones de formato, vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="e48ea-379">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="e48ea-380">themeColor</span><span class="sxs-lookup"><span data-stu-id="e48ea-380">themeColor</span></span> | <span data-ttu-id="e48ea-381">Cadena HEX</span><span class="sxs-lookup"><span data-stu-id="e48ea-381">HEX string</span></span> | <span data-ttu-id="e48ea-382">Color que invalida el `accentColor` proporcionado desde el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e48ea-382">Color that overrides the `accentColor` provided from the application manifest.</span></span> |

### <a name="additional-information-on-the-office-365-connector-card"></a><span data-ttu-id="e48ea-383">Información adicional sobre la tarjeta Office 365 Connector</span><span class="sxs-lookup"><span data-stu-id="e48ea-383">Additional information on the Office 365 Connector card</span></span>

<span data-ttu-id="e48ea-384">Office 365 Las tarjetas de conector funcionan correctamente Microsoft Teams, incluidas las [ `ActionCard` acciones](/outlook/actionable-messages/card-reference#actioncard-action).</span><span class="sxs-lookup"><span data-stu-id="e48ea-384">Office 365 Connector cards function properly in Microsoft Teams, including [`ActionCard` actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="e48ea-385">La diferencia importante entre usar tarjetas de conector desde un conector y usar tarjetas de conector en el bot es el control de las acciones de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e48ea-385">The important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span> <span data-ttu-id="e48ea-386">En la tabla siguiente se muestra la diferencia:</span><span class="sxs-lookup"><span data-stu-id="e48ea-386">The following table lists the difference:</span></span>

| <span data-ttu-id="e48ea-387">Connector</span><span class="sxs-lookup"><span data-stu-id="e48ea-387">Connector</span></span> | <span data-ttu-id="e48ea-388">Bot</span><span class="sxs-lookup"><span data-stu-id="e48ea-388">Bot</span></span> |
| --- | --- |
| <span data-ttu-id="e48ea-389">El extremo recibe la carga de la tarjeta a través de HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="e48ea-389">The endpoint receives the card payload through HTTP POST.</span></span> | <span data-ttu-id="e48ea-390">La acción desencadena una actividad que envía solo el identificador de acción `HttpPOST` y el cuerpo al `invoke` bot.</span><span class="sxs-lookup"><span data-stu-id="e48ea-390">The `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>|

<span data-ttu-id="e48ea-391">Cada tarjeta de conector puede mostrar un máximo de diez secciones y cada sección puede contener un máximo de cinco imágenes y cinco acciones.</span><span class="sxs-lookup"><span data-stu-id="e48ea-391">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="e48ea-392">Las secciones, imágenes o acciones adicionales de un mensaje no aparecen.</span><span class="sxs-lookup"><span data-stu-id="e48ea-392">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="e48ea-393">Todos los campos de texto admiten Markdown y HTML.</span><span class="sxs-lookup"><span data-stu-id="e48ea-393">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="e48ea-394">Puede controlar qué secciones usan Markdown o HTML estableciendo la `markdown` propiedad en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="e48ea-394">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="e48ea-395">De forma predeterminada, `markdown` se establece en `true` .</span><span class="sxs-lookup"><span data-stu-id="e48ea-395">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="e48ea-396">Si quiere usar HTML en su lugar, establezca `markdown` en `false` .</span><span class="sxs-lookup"><span data-stu-id="e48ea-396">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="e48ea-397">Si especifica la `themeColor` propiedad, invalida la `accentColor` propiedad en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e48ea-397">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="e48ea-398">Para especificar el estilo de representación `activityImage` para , puede `activityImageType` establecerlo como se muestra en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="e48ea-398">To specify the rendering style for `activityImage`, you can set `activityImageType` as shown in the following table:</span></span>

| <span data-ttu-id="e48ea-399">Valor</span><span class="sxs-lookup"><span data-stu-id="e48ea-399">Value</span></span> | <span data-ttu-id="e48ea-400">Descripción</span><span class="sxs-lookup"><span data-stu-id="e48ea-400">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="e48ea-401">Valor predeterminado, `activityImage` se recorta como un círculo.</span><span class="sxs-lookup"><span data-stu-id="e48ea-401">Default, `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="e48ea-402">`activityImage` se muestra como un rectángulo y conserva su relación de aspecto.</span><span class="sxs-lookup"><span data-stu-id="e48ea-402">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="e48ea-403">Para obtener todos los demás detalles acerca de las propiedades de la tarjeta de conector, vea [referencia de tarjeta de mensaje que puede actuar.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="e48ea-403">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="e48ea-404">Las únicas propiedades de tarjeta de conector que Teams admite actualmente son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="e48ea-404">The only connector card properties that Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="e48ea-405">`startGroup`siempre tratado como `true` en Teams</span><span class="sxs-lookup"><span data-stu-id="e48ea-405">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="e48ea-406">Ejemplo de una tarjeta Office 365 Connector</span><span class="sxs-lookup"><span data-stu-id="e48ea-406">Example of an Office 365 Connector card</span></span>

<span data-ttu-id="e48ea-407">El siguiente código muestra un ejemplo de una tarjeta Office 365 Connector:</span><span class="sxs-lookup"><span data-stu-id="e48ea-407">The following code shows an example of an Office 365 Connector card:</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="e48ea-408">Tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="e48ea-408">Receipt card</span></span>

<span data-ttu-id="e48ea-409">Teams admite tarjeta de recibo.</span><span class="sxs-lookup"><span data-stu-id="e48ea-409">Teams supports receipt card.</span></span> <span data-ttu-id="e48ea-410">Es una tarjeta que permite a un bot proporcionar un recibo al usuario.</span><span class="sxs-lookup"><span data-stu-id="e48ea-410">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="e48ea-411">Normalmente contiene la lista de elementos que se deben incluir en el recibo, como impuestos y la información total.</span><span class="sxs-lookup"><span data-stu-id="e48ea-411">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="e48ea-412">Compatibilidad con tarjetas de recibo</span><span class="sxs-lookup"><span data-stu-id="e48ea-412">Support for receipt cards</span></span>

<span data-ttu-id="e48ea-413">En la tabla siguiente se proporcionan las características que admiten tarjetas de recibo:</span><span class="sxs-lookup"><span data-stu-id="e48ea-413">The following table provides the features that support receipt cards:</span></span>

| <span data-ttu-id="e48ea-414">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="e48ea-414">Bots in Teams</span></span> | <span data-ttu-id="e48ea-415">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="e48ea-415">Messaging extensions</span></span>  | <span data-ttu-id="e48ea-416">Conectores</span><span class="sxs-lookup"><span data-stu-id="e48ea-416">Connectors</span></span> | <span data-ttu-id="e48ea-417">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="e48ea-417">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e48ea-418">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-418">✔</span></span> | <span data-ttu-id="e48ea-419">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-419">✔</span></span> | <span data-ttu-id="e48ea-420">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-420">✖</span></span> | <span data-ttu-id="e48ea-421">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-421">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="e48ea-422">Ejemplo de una tarjeta de recibo</span><span class="sxs-lookup"><span data-stu-id="e48ea-422">Example of a receipt card</span></span>

![Ejemplo de una tarjeta de recibo](~/assets/images/cards/receipt.png)

<span data-ttu-id="e48ea-424">El siguiente código muestra un ejemplo de una tarjeta de recibo:</span><span class="sxs-lookup"><span data-stu-id="e48ea-424">The following code shows an example of a receipt card:</span></span>

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="e48ea-425">Información adicional sobre tarjetas de recibo</span><span class="sxs-lookup"><span data-stu-id="e48ea-425">Additional information on receipt cards</span></span>

<span data-ttu-id="e48ea-426">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="e48ea-426">Bot Framework reference:</span></span>

* [<span data-ttu-id="e48ea-427">Tarjeta de recibo Node.js</span><span class="sxs-lookup"><span data-stu-id="e48ea-427">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="e48ea-428">Tarjeta de recibo C #</span><span class="sxs-lookup"><span data-stu-id="e48ea-428">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="e48ea-429">Tarjeta de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="e48ea-429">Signin card</span></span>

<span data-ttu-id="e48ea-430">La tarjeta de inicio de sesión en Teams es similar a la tarjeta de inicio de sesión en Bot Framework, excepto que la tarjeta de inicio de sesión en Teams solo admite dos `signin` acciones y `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="e48ea-430">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions `signin` and `openUrl`.</span></span>

<span data-ttu-id="e48ea-431">La acción de inicio de sesión se puede usar desde cualquier tarjeta de Teams, no solo desde la tarjeta de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="e48ea-431">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="e48ea-432">Para obtener más información, [vea Teams de autenticación para bots](~/bots/how-to/authentication/auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="e48ea-432">For more information, see [Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="e48ea-433">Compatibilidad con tarjetas de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="e48ea-433">Support for signin cards</span></span>

<span data-ttu-id="e48ea-434">En la tabla siguiente se proporcionan las características que admiten tarjetas de inicio de sesión:</span><span class="sxs-lookup"><span data-stu-id="e48ea-434">The following table provides the features that support signin cards:</span></span>

| <span data-ttu-id="e48ea-435">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="e48ea-435">Bots in Teams</span></span> | <span data-ttu-id="e48ea-436">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="e48ea-436">Messaging extensions</span></span>  | <span data-ttu-id="e48ea-437">Conectores</span><span class="sxs-lookup"><span data-stu-id="e48ea-437">Connectors</span></span> | <span data-ttu-id="e48ea-438">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="e48ea-438">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e48ea-439">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-439">✔</span></span> | <span data-ttu-id="e48ea-440">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-440">✖</span></span> | <span data-ttu-id="e48ea-441">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-441">✖</span></span> | <span data-ttu-id="e48ea-442">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-442">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="e48ea-443">Información adicional sobre tarjetas de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="e48ea-443">Additional information on signin cards</span></span>

<span data-ttu-id="e48ea-444">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="e48ea-444">Bot Framework reference:</span></span>

* [<span data-ttu-id="e48ea-445">Tarjeta de inicio de sesión Node.js</span><span class="sxs-lookup"><span data-stu-id="e48ea-445">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="e48ea-446">Tarjeta de inicio de sesión C #</span><span class="sxs-lookup"><span data-stu-id="e48ea-446">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="e48ea-447">Tarjeta miniatura</span><span class="sxs-lookup"><span data-stu-id="e48ea-447">Thumbnail card</span></span>

<span data-ttu-id="e48ea-448">Puedes trabajar con una tarjeta en miniatura que se usa para enviar un mensaje sencillo que puede usarse.</span><span class="sxs-lookup"><span data-stu-id="e48ea-448">You can work with a thumbnail card that is used for sending a simple actionable message.</span></span> <span data-ttu-id="e48ea-449">Una tarjeta que normalmente contiene una sola imagen en miniatura, uno o varios botones y texto.</span><span class="sxs-lookup"><span data-stu-id="e48ea-449">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="e48ea-450">Compatibilidad con tarjetas en miniatura</span><span class="sxs-lookup"><span data-stu-id="e48ea-450">Support for thumbnail cards</span></span>

<span data-ttu-id="e48ea-451">En la tabla siguiente se proporcionan las características que admiten tarjetas en miniatura:</span><span class="sxs-lookup"><span data-stu-id="e48ea-451">The following table provides the features that support thumbnail cards:</span></span>

| <span data-ttu-id="e48ea-452">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="e48ea-452">Bots in Teams</span></span> | <span data-ttu-id="e48ea-453">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="e48ea-453">Messaging extensions</span></span>  | <span data-ttu-id="e48ea-454">Conectores</span><span class="sxs-lookup"><span data-stu-id="e48ea-454">Connectors</span></span> | <span data-ttu-id="e48ea-455">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="e48ea-455">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e48ea-456">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-456">✔</span></span> | <span data-ttu-id="e48ea-457">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-457">✔</span></span> | <span data-ttu-id="e48ea-458">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-458">✖</span></span> | <span data-ttu-id="e48ea-459">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-459">✔</span></span> |

![Ejemplo de una tarjeta en miniatura](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="e48ea-461">Propiedades de una tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="e48ea-461">Properties of a thumbnail card</span></span>

<span data-ttu-id="e48ea-462">En la tabla siguiente se proporcionan las propiedades de una tarjeta en miniatura:</span><span class="sxs-lookup"><span data-stu-id="e48ea-462">The following table provides the properties of a thumbnail card:</span></span>

| <span data-ttu-id="e48ea-463">Propiedad</span><span class="sxs-lookup"><span data-stu-id="e48ea-463">Property</span></span> | <span data-ttu-id="e48ea-464">Tipo</span><span class="sxs-lookup"><span data-stu-id="e48ea-464">Type</span></span>  | <span data-ttu-id="e48ea-465">Description</span><span class="sxs-lookup"><span data-stu-id="e48ea-465">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e48ea-466">title</span><span class="sxs-lookup"><span data-stu-id="e48ea-466">title</span></span> | <span data-ttu-id="e48ea-467">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="e48ea-467">Rich text</span></span> | <span data-ttu-id="e48ea-468">Título de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e48ea-468">Title of the card.</span></span> <span data-ttu-id="e48ea-469">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="e48ea-469">Maximum 2 lines.</span></span>|
| <span data-ttu-id="e48ea-470">subtitle</span><span class="sxs-lookup"><span data-stu-id="e48ea-470">subtitle</span></span> | <span data-ttu-id="e48ea-471">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="e48ea-471">Rich text</span></span> | <span data-ttu-id="e48ea-472">Subtítulo de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e48ea-472">Subtitle of the card.</span></span> <span data-ttu-id="e48ea-473">Máximo de 2 líneas.</span><span class="sxs-lookup"><span data-stu-id="e48ea-473">Maximum 2 lines.</span></span>|
| <span data-ttu-id="e48ea-474">text</span><span class="sxs-lookup"><span data-stu-id="e48ea-474">text</span></span> | <span data-ttu-id="e48ea-475">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="e48ea-475">Rich text</span></span> | <span data-ttu-id="e48ea-476">El texto aparece debajo del subtítulo.</span><span class="sxs-lookup"><span data-stu-id="e48ea-476">Text appears under the subtitle.</span></span> <span data-ttu-id="e48ea-477">Para ver las opciones de formato, vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="e48ea-477">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="e48ea-478">imágenes</span><span class="sxs-lookup"><span data-stu-id="e48ea-478">images</span></span> | <span data-ttu-id="e48ea-479">Matriz de imágenes</span><span class="sxs-lookup"><span data-stu-id="e48ea-479">Array of images</span></span> | <span data-ttu-id="e48ea-480">Imagen que se muestra en la parte superior de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e48ea-480">Image displayed at the top of the card.</span></span> <span data-ttu-id="e48ea-481">Relación de aspecto 1:1 cuadrado.</span><span class="sxs-lookup"><span data-stu-id="e48ea-481">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="e48ea-482">botones</span><span class="sxs-lookup"><span data-stu-id="e48ea-482">buttons</span></span> | <span data-ttu-id="e48ea-483">Matriz de objetos de acción</span><span class="sxs-lookup"><span data-stu-id="e48ea-483">Array of action objects</span></span> | <span data-ttu-id="e48ea-484">Conjunto de acciones aplicables a la tarjeta actual.</span><span class="sxs-lookup"><span data-stu-id="e48ea-484">Set of actions applicable to the current card.</span></span> <span data-ttu-id="e48ea-485">Máximo 6.</span><span class="sxs-lookup"><span data-stu-id="e48ea-485">Maximum 6.</span></span> |
| <span data-ttu-id="e48ea-486">pulsación</span><span class="sxs-lookup"><span data-stu-id="e48ea-486">tap</span></span> | <span data-ttu-id="e48ea-487">Action (objeto)</span><span class="sxs-lookup"><span data-stu-id="e48ea-487">Action object</span></span> | <span data-ttu-id="e48ea-488">Se activa cuando el usuario pulsa en la propia tarjeta.</span><span class="sxs-lookup"><span data-stu-id="e48ea-488">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="e48ea-489">Ejemplo de una tarjeta en miniatura</span><span class="sxs-lookup"><span data-stu-id="e48ea-489">Example of a thumbnail card</span></span>

<span data-ttu-id="e48ea-490">El código siguiente muestra un ejemplo de una tarjeta en miniatura:</span><span class="sxs-lookup"><span data-stu-id="e48ea-490">The following code shows an example of a thumbnail card:</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="e48ea-491">Información adicional</span><span class="sxs-lookup"><span data-stu-id="e48ea-491">Additional information</span></span>

<span data-ttu-id="e48ea-492">Referencia de Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="e48ea-492">Bot Framework reference:</span></span>

* [<span data-ttu-id="e48ea-493">Tarjeta en miniatura Node.js</span><span class="sxs-lookup"><span data-stu-id="e48ea-493">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="e48ea-494">Tarjeta de miniatura C #</span><span class="sxs-lookup"><span data-stu-id="e48ea-494">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="e48ea-495">Colecciones de tarjetas</span><span class="sxs-lookup"><span data-stu-id="e48ea-495">Card collections</span></span>

<span data-ttu-id="e48ea-496">Puede trabajar con colecciones de tarjetas que incluyen colecciones de carrusel y listas.</span><span class="sxs-lookup"><span data-stu-id="e48ea-496">You can work with card collections that include carousel and list collections.</span></span> <span data-ttu-id="e48ea-497">Teams admite colecciones de tarjetas.</span><span class="sxs-lookup"><span data-stu-id="e48ea-497">Teams supports card collections.</span></span> <span data-ttu-id="e48ea-498">Las colecciones de tarjetas `builder.AttachmentLayout.carousel` incluyen y `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="e48ea-498">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="e48ea-499">Estas colecciones contienen tarjetas adaptables, de héroe o en miniatura.</span><span class="sxs-lookup"><span data-stu-id="e48ea-499">These collections contain Adaptive, hero, or thumbnail cards.</span></span>

### <a name="carousel-collection"></a><span data-ttu-id="e48ea-500">Colección Carousel</span><span class="sxs-lookup"><span data-stu-id="e48ea-500">Carousel collection</span></span>

<span data-ttu-id="e48ea-501">El [diseño del carrusel](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) muestra un carrusel de tarjetas, opcionalmente con botones de acción asociados.</span><span class="sxs-lookup"><span data-stu-id="e48ea-501">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

#### <a name="support-for-carousel-collections"></a><span data-ttu-id="e48ea-502">Compatibilidad con colecciones de carrusel</span><span class="sxs-lookup"><span data-stu-id="e48ea-502">Support for carousel collections</span></span>

<span data-ttu-id="e48ea-503">En la tabla siguiente se proporcionan las características que admiten colecciones de carrusel:</span><span class="sxs-lookup"><span data-stu-id="e48ea-503">The following table provides the features that support carousel collections:</span></span>

| <span data-ttu-id="e48ea-504">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="e48ea-504">Bots in Teams</span></span> | <span data-ttu-id="e48ea-505">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="e48ea-505">Messaging extensions</span></span>  | <span data-ttu-id="e48ea-506">Conectores</span><span class="sxs-lookup"><span data-stu-id="e48ea-506">Connectors</span></span> | <span data-ttu-id="e48ea-507">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="e48ea-507">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e48ea-508">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-508">✔</span></span> | <span data-ttu-id="e48ea-509">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-509">✖</span></span> | <span data-ttu-id="e48ea-510">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-510">✖</span></span> | <span data-ttu-id="e48ea-511">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-511">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="e48ea-512">Un carrusel puede mostrar un máximo de diez tarjetas por mensaje.</span><span class="sxs-lookup"><span data-stu-id="e48ea-512">A carousel can display a maximum of ten cards per message.</span></span>

#### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="e48ea-513">Propiedades de una tarjeta de carrusel</span><span class="sxs-lookup"><span data-stu-id="e48ea-513">Properties of a carousel card</span></span>

<span data-ttu-id="e48ea-514">Las propiedades de una tarjeta de carrusel son las mismas que las tarjetas de miniatura y de héroe.</span><span class="sxs-lookup"><span data-stu-id="e48ea-514">Properties of a carousel card are same as the hero and thumbnail cards.</span></span>

#### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="e48ea-515">Ejemplo de una colección de carrusel</span><span class="sxs-lookup"><span data-stu-id="e48ea-515">Example of a carousel collection</span></span>

![Ejemplo de un carrusel de tarjetas](~/assets/images/cards/carousel.png)

<span data-ttu-id="e48ea-517">El código siguiente muestra un ejemplo de una colección de carrusel:</span><span class="sxs-lookup"><span data-stu-id="e48ea-517">The following code shows an example of a carousel collection:</span></span>

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

#### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="e48ea-518">Sintaxis para colecciones de carrusel</span><span class="sxs-lookup"><span data-stu-id="e48ea-518">Syntax for carousel collections</span></span>

<span data-ttu-id="e48ea-519">`builder.AttachmentLayoutTypes.Carousel` es la sintaxis de las colecciones de carrusel.</span><span class="sxs-lookup"><span data-stu-id="e48ea-519">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

### <a name="list-collection"></a><span data-ttu-id="e48ea-520">Colección List</span><span class="sxs-lookup"><span data-stu-id="e48ea-520">List collection</span></span>

<span data-ttu-id="e48ea-521">El diseño de lista muestra una lista verticalmente apilada de tarjetas, opcionalmente con botones de acción asociados.</span><span class="sxs-lookup"><span data-stu-id="e48ea-521">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

#### <a name="support-for-list-collections"></a><span data-ttu-id="e48ea-522">Compatibilidad con colecciones de listas</span><span class="sxs-lookup"><span data-stu-id="e48ea-522">Support for list collections</span></span>

<span data-ttu-id="e48ea-523">En la tabla siguiente se proporcionan las características que admiten colecciones de listas:</span><span class="sxs-lookup"><span data-stu-id="e48ea-523">The following table provides the features that support list collections:</span></span>

| <span data-ttu-id="e48ea-524">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="e48ea-524">Bots in Teams</span></span> | <span data-ttu-id="e48ea-525">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="e48ea-525">Messaging extensions</span></span>  | <span data-ttu-id="e48ea-526">Conectores</span><span class="sxs-lookup"><span data-stu-id="e48ea-526">Connectors</span></span> | <span data-ttu-id="e48ea-527">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="e48ea-527">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e48ea-528">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-528">✔</span></span> | <span data-ttu-id="e48ea-529">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-529">✔</span></span> | <span data-ttu-id="e48ea-530">✖</span><span class="sxs-lookup"><span data-stu-id="e48ea-530">✖</span></span> | <span data-ttu-id="e48ea-531">✔</span><span class="sxs-lookup"><span data-stu-id="e48ea-531">✔</span></span> |

#### <a name="example-of-a-list-collection"></a><span data-ttu-id="e48ea-532">Ejemplo de una colección de listas</span><span class="sxs-lookup"><span data-stu-id="e48ea-532">Example of a list collection</span></span>

![Ejemplo de una lista de tarjetas](~/assets/images/cards/list.png)

<span data-ttu-id="e48ea-534">Las propiedades de las colecciones de listas son las mismas que las tarjetas de miniatura o de héroe.</span><span class="sxs-lookup"><span data-stu-id="e48ea-534">Properties of list collections are same as the hero or thumbnail cards.</span></span>

<span data-ttu-id="e48ea-535">Una lista puede mostrar un máximo de diez tarjetas por mensaje.</span><span class="sxs-lookup"><span data-stu-id="e48ea-535">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="e48ea-536">Algunas combinaciones de tarjetas de lista aún no son compatibles con iOS y Android.</span><span class="sxs-lookup"><span data-stu-id="e48ea-536">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

#### <a name="syntax-for-list-collections"></a><span data-ttu-id="e48ea-537">Sintaxis para colecciones de listas</span><span class="sxs-lookup"><span data-stu-id="e48ea-537">Syntax for list collections</span></span>

<span data-ttu-id="e48ea-538">`builder.AttachmentLayout.list` es la sintaxis de las colecciones de listas.</span><span class="sxs-lookup"><span data-stu-id="e48ea-538">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="e48ea-539">No se admiten tarjetas en Teams</span><span class="sxs-lookup"><span data-stu-id="e48ea-539">Cards not supported in Teams</span></span>

<span data-ttu-id="e48ea-540">Bot Framework implementa las siguientes tarjetas, pero no son compatibles con Teams:</span><span class="sxs-lookup"><span data-stu-id="e48ea-540">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="e48ea-541">Tarjetas de animación</span><span class="sxs-lookup"><span data-stu-id="e48ea-541">Animation cards</span></span>
* <span data-ttu-id="e48ea-542">Tarjetas de audio</span><span class="sxs-lookup"><span data-stu-id="e48ea-542">Audio cards</span></span>
* <span data-ttu-id="e48ea-543">Tarjetas de vídeo</span><span class="sxs-lookup"><span data-stu-id="e48ea-543">Video cards</span></span>

## <a name="see-also"></a><span data-ttu-id="e48ea-544">Vea también</span><span class="sxs-lookup"><span data-stu-id="e48ea-544">See also</span></span>

* [<span data-ttu-id="e48ea-545">Módulos de tareas</span><span class="sxs-lookup"><span data-stu-id="e48ea-545">Task modules</span></span>](~/task-modules-and-cards/what-are-task-modules.md)
* [<span data-ttu-id="e48ea-546">Dar formato a tarjetas</span><span class="sxs-lookup"><span data-stu-id="e48ea-546">Format cards</span></span>](~/task-modules-and-cards/cards/cards-format.md)

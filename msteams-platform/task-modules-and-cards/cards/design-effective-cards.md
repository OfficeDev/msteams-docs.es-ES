---
title: Diseño de Tarjetas adaptables para la aplicación
description: Obtenga información sobre cómo diseñar Tarjetas adaptables para Teams y obtener el Kit de interfaz de usuario de Microsoft Teams.
localization_priority: Priority
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 8e56928da44e22006feb59715c8bdbf821ec4c42
ms.sourcegitcommit: 99b1f151e4e36a86c6a5d2ccbde01bf45b61f526
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2021
ms.locfileid: "53037659"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a><span data-ttu-id="ce124-103">Diseño de Tarjetas adaptables para la aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ce124-103">Designing Adaptive Cards for your Microsoft Teams app</span></span>

<span data-ttu-id="ce124-104">Una tarjeta adaptable contiene un cuerpo de forma libre de elementos de tarjeta y un conjunto opcional de acciones.</span><span class="sxs-lookup"><span data-stu-id="ce124-104">An Adaptive Card contains a freeform body of card elements and optional set of actions.</span></span> <span data-ttu-id="ce124-105">Tarjetas adaptables son fragmentos de contenido accionables que puede agregar a una conversación a través de un bot o una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="ce124-105">Adaptive Cards are actionable snippets of content that you can add to a conversation through a bot or messaging extension.</span></span> <span data-ttu-id="ce124-106">Con texto, gráficos y botones, estas tarjetas proporcionan una comunicación enriquecida a la audiencia.</span><span class="sxs-lookup"><span data-stu-id="ce124-106">Using text, graphics, and buttons, these cards provide rich communication to your audience.</span></span>

<span data-ttu-id="ce124-107">El marco de tarjeta adaptable se usa en muchos productos de Microsoft, incluido Teams.</span><span class="sxs-lookup"><span data-stu-id="ce124-107">The Adaptive Card framework is used across many Microsoft products, including Teams.</span></span> <span data-ttu-id="ce124-108">Puede enviar tarjetas dentro de mensajes a los usuarios a través de bots o extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="ce124-108">You can send cards inside messages to users via bots or messaging extensions.</span></span> <span data-ttu-id="ce124-109">Los usuarios también pueden realizar acciones en las tarjetas cuando estén presentes.</span><span class="sxs-lookup"><span data-stu-id="ce124-109">Users can also take actions on cards when present.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="Ejemplo de información general de una tarjeta adaptable." border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="ce124-111">Kit de UI de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ce124-111">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="ce124-112">En el Kit de UI de Microsoft Teams encontrará instrucciones de diseño de bot más completas, que incluyen elementos que puede usar y modificar como quiera.</span><span class="sxs-lookup"><span data-stu-id="ce124-112">You can find more comprehensive design guidelines for Adaptive Cards in Teams, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="ce124-113">El kit de interfaz de usuario también trata temas esenciales como temas, accesibilidad y ajuste de tamaño con capacidad de respuesta.</span><span class="sxs-lookup"><span data-stu-id="ce124-113">The UI kit also covers essential topics such as theming, accessibility, and responsive sizing.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ce124-114">Obtener el Kit de UI de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="ce124-114">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a><span data-ttu-id="ce124-115">Diseñador de tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="ce124-115">Adaptive Cards designer</span></span>

<span data-ttu-id="ce124-116">También puede empezar a diseñar el Tarjetas adaptables directamente en el explorador.</span><span class="sxs-lookup"><span data-stu-id="ce124-116">You also can start designing your Adaptive Cards directly in the browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ce124-117">Pruebe el diseñador de Tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="ce124-117">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a><span data-ttu-id="ce124-118">Tipos de Tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="ce124-118">Types of Adaptive Cards</span></span>

### <a name="hero"></a><span data-ttu-id="ce124-119">Elemento principal</span><span class="sxs-lookup"><span data-stu-id="ce124-119">Hero</span></span>

<span data-ttu-id="ce124-120">Nuestra tarjeta más grande.</span><span class="sxs-lookup"><span data-stu-id="ce124-120">Our largest card.</span></span> <span data-ttu-id="ce124-121">Se usa para compartir artículos o escenarios en los que una imagen cuenta la mayor parte de la historia.</span><span class="sxs-lookup"><span data-stu-id="ce124-121">Use for sharing articles or scenarios where an image tells most of the story.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="ce124-122">Escritorio</span><span class="sxs-lookup"><span data-stu-id="ce124-122">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="En el ejemplo se muestra una tarjeta de imagen prominente de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="ce124-124">Móvil</span><span class="sxs-lookup"><span data-stu-id="ce124-124">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="En el ejemplo se muestra una tarjeta de imagen prominente de tarjeta adaptable en dispositivos móviles." border="false":::

---

### <a name="thumbnail"></a><span data-ttu-id="ce124-126">Miniatura</span><span class="sxs-lookup"><span data-stu-id="ce124-126">Thumbnail</span></span>

<span data-ttu-id="ce124-127">Se usa para enviar un mensaje sencillo que requiere acción.</span><span class="sxs-lookup"><span data-stu-id="ce124-127">Use for sending a simple actionable message.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="ce124-128">Escritorio</span><span class="sxs-lookup"><span data-stu-id="ce124-128">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="En el ejemplo se muestra una tarjeta en miniatura de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="ce124-130">Móvil</span><span class="sxs-lookup"><span data-stu-id="ce124-130">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="En el ejemplo se muestra una tarjeta en miniatura de tarjeta adaptable en dispositivos móviles." border="false":::

---

### <a name="list"></a><span data-ttu-id="ce124-132">Lista</span><span class="sxs-lookup"><span data-stu-id="ce124-132">List</span></span>

<span data-ttu-id="ce124-133">Se usa en escenarios en los que desea que el usuario elija un elemento de una lista, pero los elementos no necesitan mucha explicación.</span><span class="sxs-lookup"><span data-stu-id="ce124-133">Use in scenarios where you want the user to pick an item from a list, but the items don’t need a lot of explanation.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="ce124-134">Escritorio</span><span class="sxs-lookup"><span data-stu-id="ce124-134">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="En el ejemplo se muestra una tarjeta de lista de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="ce124-136">Móvil</span><span class="sxs-lookup"><span data-stu-id="ce124-136">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="En el ejemplo se muestra una tarjeta de lista de tarjetas adaptables en dispositivos móviles." border="false":::

---
Use for news digests and round-up posts. Note: We recommend the thumbnail card for a single update or news item.
':::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="Example shows an Adaptive Card digest card." border="false"::': null
':::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="Example shows an Adaptive Card digest card on mobile." border="false"::': null
---

### <a name="media"></a><span data-ttu-id="ce124-138">Multimedia</span><span class="sxs-lookup"><span data-stu-id="ce124-138">Media</span></span>

<span data-ttu-id="ce124-139">Úselo cuando quiera combinar texto y elementos multimedia, como audio o vídeo.</span><span class="sxs-lookup"><span data-stu-id="ce124-139">Use when you want to combine text and media, like audio or video.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="ce124-140">Escritorio</span><span class="sxs-lookup"><span data-stu-id="ce124-140">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="En el ejemplo se muestra una tarjeta multimedia de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="ce124-142">Móvil</span><span class="sxs-lookup"><span data-stu-id="ce124-142">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="En el ejemplo se muestra una tarjeta multimedia de tarjeta adaptable en dispositivos móviles." border="false":::

---

### <a name="people"></a><span data-ttu-id="ce124-144">Contactos</span><span class="sxs-lookup"><span data-stu-id="ce124-144">People</span></span>

<span data-ttu-id="ce124-145">Se recomienda cuando se transmite de forma eficaz quién está implicado en una tarea.</span><span class="sxs-lookup"><span data-stu-id="ce124-145">Best used when you to efficiently convey who's involved with a task.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="ce124-146">Escritorio</span><span class="sxs-lookup"><span data-stu-id="ce124-146">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="En el ejemplo se muestra una tarjeta de contactos de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="ce124-148">Móvil</span><span class="sxs-lookup"><span data-stu-id="ce124-148">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="En el ejemplo se muestra una tarjeta de contactos de tarjeta adaptable en dispositivos móviles." border="false":::

---

### <a name="request-ticket"></a><span data-ttu-id="ce124-150">Solicitar vale</span><span class="sxs-lookup"><span data-stu-id="ce124-150">Request ticket</span></span>

<span data-ttu-id="ce124-151">Se usa para obtener entradas rápidas de un usuario para crear automáticamente una tarea o un vale.</span><span class="sxs-lookup"><span data-stu-id="ce124-151">Use to get quick inputs from a user to automatically create a task or ticket.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="ce124-152">Escritorio</span><span class="sxs-lookup"><span data-stu-id="ce124-152">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="En el ejemplo se muestra una tarjeta de vale de solicitud de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="ce124-154">Móvil</span><span class="sxs-lookup"><span data-stu-id="ce124-154">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="En el ejemplo se muestra una tarjeta de vale de solicitud de tarjeta adaptable en dispositivos móviles." border="false":::

---

### <a name="image-set"></a><span data-ttu-id="ce124-156">Imágenes</span><span class="sxs-lookup"><span data-stu-id="ce124-156">Image set</span></span>

<span data-ttu-id="ce124-157">Se usa para enviar varias miniaturas de imagen.</span><span class="sxs-lookup"><span data-stu-id="ce124-157">Use to send multiple image thumbnails.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="ce124-158">Escritorio</span><span class="sxs-lookup"><span data-stu-id="ce124-158">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de imágenes de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="ce124-160">Móvil</span><span class="sxs-lookup"><span data-stu-id="ce124-160">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de imágenes de tarjeta adaptable en dispositivos móviles." border="false":::

---

### <a name="action-set"></a><span data-ttu-id="ce124-162">Conjunto de acciones</span><span class="sxs-lookup"><span data-stu-id="ce124-162">Action set</span></span>

<span data-ttu-id="ce124-163">Úselo cuando quiera que el usuario seleccione un botón y, a continuación, recopile la entrada adicional del usuario de la misma tarjeta.</span><span class="sxs-lookup"><span data-stu-id="ce124-163">Use when you want to the user to select a button, then gather addition user input from the same card.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="ce124-164">Escritorio</span><span class="sxs-lookup"><span data-stu-id="ce124-164">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de acciones de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="ce124-166">Móvil</span><span class="sxs-lookup"><span data-stu-id="ce124-166">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de acciones de tarjeta adaptable en dispositivos móviles." border="false":::

---

### <a name="choice-set"></a><span data-ttu-id="ce124-168">Conjunto de opciones</span><span class="sxs-lookup"><span data-stu-id="ce124-168">Choice set</span></span>

<span data-ttu-id="ce124-169">Se usa para recopilar varias entradas del usuario.</span><span class="sxs-lookup"><span data-stu-id="ce124-169">Use to gather multiple inputs from the user.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="ce124-170">Escritorio</span><span class="sxs-lookup"><span data-stu-id="ce124-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de opciones de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="ce124-172">Móvil</span><span class="sxs-lookup"><span data-stu-id="ce124-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de opciones de tarjeta adaptable en dispositivos móviles." border="false":::

---

## <a name="anatomy"></a><span data-ttu-id="ce124-174">Anatomía</span><span class="sxs-lookup"><span data-stu-id="ce124-174">Anatomy</span></span>

<span data-ttu-id="ce124-175">Tarjetas adaptables tienen mucha flexibilidad.</span><span class="sxs-lookup"><span data-stu-id="ce124-175">Adaptive Cards have a lot of flexibility.</span></span> <span data-ttu-id="ce124-176">Pero, como mínimo, se recomienda incluir los siguientes componentes en cada tarjeta.</span><span class="sxs-lookup"><span data-stu-id="ce124-176">But at minimum, we strongly suggest including the following components in every card.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="ce124-177">Escritorio</span><span class="sxs-lookup"><span data-stu-id="ce124-177">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="EExample muestra la anatomía de la tarjeta adaptable." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="ce124-179">Móvil</span><span class="sxs-lookup"><span data-stu-id="ce124-179">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="En el ejemplo se muestra la anatomía de la tarjeta adaptable en dispositivos móviles." border="false":::

---

|<span data-ttu-id="ce124-181">Contador</span><span class="sxs-lookup"><span data-stu-id="ce124-181">Counter</span></span>|<span data-ttu-id="ce124-182">Descripción</span><span class="sxs-lookup"><span data-stu-id="ce124-182">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="ce124-183">A</span><span class="sxs-lookup"><span data-stu-id="ce124-183">A</span></span>|<span data-ttu-id="ce124-184">**Encabezado**: haga que los encabezados sean claros y concisos.</span><span class="sxs-lookup"><span data-stu-id="ce124-184">**Header**: Make your headers clear and concise.</span></span>|
|<span data-ttu-id="ce124-185">N</span><span class="sxs-lookup"><span data-stu-id="ce124-185">B</span></span>|<span data-ttu-id="ce124-186">**copia del cuerpo**: transmita detalles que son demasiado largos o no son lo suficientemente importantes como para incluirlos en el encabezado.</span><span class="sxs-lookup"><span data-stu-id="ce124-186">**Body copy**: Convey details that are either too long or not important enough to include in the header.</span></span>|
|<span data-ttu-id="ce124-187">C</span><span class="sxs-lookup"><span data-stu-id="ce124-187">C</span></span>|<span data-ttu-id="ce124-188">**Acciones principales**: como procedimiento recomendado, incluya de 1 a 3 acciones principales.</span><span class="sxs-lookup"><span data-stu-id="ce124-188">**Primary actions**: As a best practice, include 1-3 primary actions.</span></span> <span data-ttu-id="ce124-189">Puede tener hasta seis.</span><span class="sxs-lookup"><span data-stu-id="ce124-189">You can have up to six.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="ce124-190">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="ce124-190">Best practices</span></span>

<span data-ttu-id="ce124-191">Use estas recomendaciones para crear una experiencia de aplicación de calidad.</span><span class="sxs-lookup"><span data-stu-id="ce124-191">Use these recommendations to create a quality app experience.</span></span>

### <a name="primary-and-secondary-actions"></a><span data-ttu-id="ce124-192">Acciones principales y secundarias</span><span class="sxs-lookup"><span data-stu-id="ce124-192">Primary and secondary actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="Procedimiento recomendado para incluir solo un pequeño conjunto de acciones en una tarjeta adaptable." border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a><span data-ttu-id="ce124-194">Hacer: Usar hasta seis acciones principales</span><span class="sxs-lookup"><span data-stu-id="ce124-194">Do: Use up to six primary actions</span></span>

<span data-ttu-id="ce124-195">Aunque Tarjetas adaptables puede admitir seis acciones principales, la mayoría de las tarjetas no lo necesitan.</span><span class="sxs-lookup"><span data-stu-id="ce124-195">While Adaptive Cards can support six primary actions, most cards don’t need that.</span></span> <span data-ttu-id="ce124-196">Las acciones deben ser claras, concisas y directas.</span><span class="sxs-lookup"><span data-stu-id="ce124-196">Actions should be clear, concise, and straight forward.</span></span> <span data-ttu-id="ce124-197">Menos es más.</span><span class="sxs-lookup"><span data-stu-id="ce124-197">Less is more.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="Procedimiento recomendado para no sobrecargar a los usuarios con demasiadas acciones en una tarjeta adaptable." border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a><span data-ttu-id="ce124-199">No: Usar más de seis acciones principales</span><span class="sxs-lookup"><span data-stu-id="ce124-199">Don't: Use more than six primary actions</span></span>

<span data-ttu-id="ce124-200">Tarjetas adaptables debe presentar contenido rápido y accionable.</span><span class="sxs-lookup"><span data-stu-id="ce124-200">Adaptive Cards should present quick, actionable content.</span></span> <span data-ttu-id="ce124-201">Demasiadas acciones pueden sobrecargar a un usuario.</span><span class="sxs-lookup"><span data-stu-id="ce124-201">Too many actions can overwhelm a user.</span></span>

   :::column-end:::
:::row-end:::

### <a name="frequency"></a><span data-ttu-id="ce124-202">Frecuencia</span><span class="sxs-lookup"><span data-stu-id="ce124-202">Frequency</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="Procedimiento recomendado sobre la frecuencia de la tarjeta adaptable." border="false":::

#### <a name="do-be-concise"></a><span data-ttu-id="ce124-204">Do: Sea conciso</span><span class="sxs-lookup"><span data-stu-id="ce124-204">Do: Be concise</span></span>

<span data-ttu-id="ce124-205">Es fácil enviar varias tarjetas a una conversación, pero una vez que las tarjetas se desplazan fuera de la vista, resultan menos útiles.</span><span class="sxs-lookup"><span data-stu-id="ce124-205">It's easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="ce124-206">Intente limitarse a lo esencial.</span><span class="sxs-lookup"><span data-stu-id="ce124-206">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="ce124-207">Esto es especialmente cierto en un canal en el que los usuarios tienen menos tolerancia a lo que perciben como "ruido".</span><span class="sxs-lookup"><span data-stu-id="ce124-207">This is especially true in a channel where users have less tolerance for what they perceive as "noise".</span></span>

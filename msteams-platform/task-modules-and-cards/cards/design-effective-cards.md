---
title: Diseño de tarjetas adaptables para la aplicación
description: Obtén información sobre cómo diseñar tarjetas adaptables para Teams y obtener el kit Microsoft Teams interfaz de usuario.
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: b4d5f43268c7bd5afecb56d26eb0d49ed6c9002b
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630312"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a><span data-ttu-id="3e76e-103">Diseño de tarjetas adaptables para tu Microsoft Teams aplicación</span><span class="sxs-lookup"><span data-stu-id="3e76e-103">Designing Adaptive Cards for your Microsoft Teams app</span></span>

<span data-ttu-id="3e76e-104">Una tarjeta adaptable contiene un cuerpo de forma libre de elementos de tarjeta y un conjunto opcional de acciones.</span><span class="sxs-lookup"><span data-stu-id="3e76e-104">An Adaptive Card contains a freeform body of card elements and optional set of actions.</span></span> <span data-ttu-id="3e76e-105">Las tarjetas adaptables son fragmentos de contenido que se pueden usar y que se pueden agregar a una conversación a través de un bot o una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="3e76e-105">Adaptive Cards are actionable snippets of content that you can add to a conversation through a bot or messaging extension.</span></span> <span data-ttu-id="3e76e-106">Con texto, gráficos y botones, estas tarjetas proporcionan una comunicación enriquecte a tu audiencia.</span><span class="sxs-lookup"><span data-stu-id="3e76e-106">Using text, graphics, and buttons, these cards provide rich communication to your audience.</span></span>

<span data-ttu-id="3e76e-107">El marco de la tarjeta adaptable se usa en muchos productos de Microsoft, incluidos Teams.</span><span class="sxs-lookup"><span data-stu-id="3e76e-107">The Adaptive Card framework is used across many Microsoft products, including Teams.</span></span> <span data-ttu-id="3e76e-108">Puedes enviar tarjetas dentro de mensajes a los usuarios a través de bots o extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="3e76e-108">You can send cards inside messages to users via bots or messaging extensions.</span></span> <span data-ttu-id="3e76e-109">Los usuarios también pueden realizar acciones en las tarjetas cuando están presentes.</span><span class="sxs-lookup"><span data-stu-id="3e76e-109">Users can also take actions on cards when present.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="Ejemplo de introducción a una tarjeta adaptable." border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="3e76e-111">Kit de UI de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3e76e-111">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="3e76e-112">Puedes encontrar instrucciones de diseño más completas para las tarjetas adaptables en Teams, incluidos los elementos que puedes agarrar y modificar según sea necesario, en el kit de interfaz Microsoft Teams usuario.</span><span class="sxs-lookup"><span data-stu-id="3e76e-112">You can find more comprehensive design guidelines for Adaptive Cards in Teams, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="3e76e-113">El kit de interfaz de usuario también trata temas esenciales como temas, accesibilidad y tamaño dinámico.</span><span class="sxs-lookup"><span data-stu-id="3e76e-113">The UI kit also covers essential topics such as theming, accessibility, and responsive sizing.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3e76e-114">Obtener el Kit de UI de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="3e76e-114">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a><span data-ttu-id="3e76e-115">Diseñador de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="3e76e-115">Adaptive Cards designer</span></span>

<span data-ttu-id="3e76e-116">También puedes empezar a diseñar las tarjetas adaptables directamente en el explorador.</span><span class="sxs-lookup"><span data-stu-id="3e76e-116">You also can start designing your Adaptive Cards directly in the browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3e76e-117">Probar el diseñador de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="3e76e-117">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a><span data-ttu-id="3e76e-118">Tipos de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="3e76e-118">Types of Adaptive Cards</span></span>

### <a name="hero"></a><span data-ttu-id="3e76e-119">Elemento principal</span><span class="sxs-lookup"><span data-stu-id="3e76e-119">Hero</span></span>

<span data-ttu-id="3e76e-120">Nuestra tarjeta más grande.</span><span class="sxs-lookup"><span data-stu-id="3e76e-120">Our largest card.</span></span> <span data-ttu-id="3e76e-121">Se usa para compartir artículos o escenarios en los que una imagen cuenta la mayor parte del artículo.</span><span class="sxs-lookup"><span data-stu-id="3e76e-121">Use for sharing articles or scenarios where an image tells most of the story.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3e76e-122">Escritorio</span><span class="sxs-lookup"><span data-stu-id="3e76e-122">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="En el ejemplo se muestra una tarjeta de héroe de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3e76e-124">Móvil</span><span class="sxs-lookup"><span data-stu-id="3e76e-124">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="En el ejemplo se muestra una tarjeta de héroe de tarjeta adaptable en el móvil." border="false":::

---

### <a name="thumbnail"></a><span data-ttu-id="3e76e-126">Miniatura</span><span class="sxs-lookup"><span data-stu-id="3e76e-126">Thumbnail</span></span>

<span data-ttu-id="3e76e-127">Se usa para enviar un mensaje sencillo que puede usarse.</span><span class="sxs-lookup"><span data-stu-id="3e76e-127">Use for sending a simple actionable message.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3e76e-128">Escritorio</span><span class="sxs-lookup"><span data-stu-id="3e76e-128">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="En el ejemplo se muestra una tarjeta en miniatura de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3e76e-130">Móvil</span><span class="sxs-lookup"><span data-stu-id="3e76e-130">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="En el ejemplo se muestra una tarjeta en miniatura de tarjeta adaptable en el móvil." border="false":::

---

### <a name="list"></a><span data-ttu-id="3e76e-132">Lista</span><span class="sxs-lookup"><span data-stu-id="3e76e-132">List</span></span>

<span data-ttu-id="3e76e-133">Se usa en escenarios en los que desea que el usuario elija un elemento de una lista, pero los elementos no necesitan mucha explicación.</span><span class="sxs-lookup"><span data-stu-id="3e76e-133">Use in scenarios where you want the user to pick an item from a list, but the items don’t need a lot of explanation.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3e76e-134">Escritorio</span><span class="sxs-lookup"><span data-stu-id="3e76e-134">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="En el ejemplo se muestra una tarjeta de lista de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3e76e-136">Móvil</span><span class="sxs-lookup"><span data-stu-id="3e76e-136">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="En el ejemplo se muestra una tarjeta de lista de tarjeta adaptable en el móvil." border="false":::

---
Use for news digests and round-up posts. Note: We recommend the thumbnail card for a single update or news item.
':::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="Example shows an Adaptive Card digest card." border="false"::': null
':::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="Example shows an Adaptive Card digest card on mobile." border="false"::': null
---

### <a name="media"></a><span data-ttu-id="3e76e-138">Elementos multimedia</span><span class="sxs-lookup"><span data-stu-id="3e76e-138">Media</span></span>

<span data-ttu-id="3e76e-139">Úsalo cuando quieras combinar texto y medios, como audio o vídeo.</span><span class="sxs-lookup"><span data-stu-id="3e76e-139">Use when you want to combine text and media, like audio or video.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3e76e-140">Escritorio</span><span class="sxs-lookup"><span data-stu-id="3e76e-140">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="En el ejemplo se muestra una tarjeta multimedia de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3e76e-142">Móvil</span><span class="sxs-lookup"><span data-stu-id="3e76e-142">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="En el ejemplo se muestra una tarjeta multimedia de tarjeta adaptable en el móvil." border="false":::

---

### <a name="people"></a><span data-ttu-id="3e76e-144">Personas</span><span class="sxs-lookup"><span data-stu-id="3e76e-144">People</span></span>

<span data-ttu-id="3e76e-145">Se usa mejor cuando se transmite de forma eficaz quién está implicado en una tarea.</span><span class="sxs-lookup"><span data-stu-id="3e76e-145">Best used when you to efficiently convey who's involved with a task.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3e76e-146">Escritorio</span><span class="sxs-lookup"><span data-stu-id="3e76e-146">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="En el ejemplo se muestra una tarjeta de personas de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3e76e-148">Móvil</span><span class="sxs-lookup"><span data-stu-id="3e76e-148">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="En el ejemplo se muestra una tarjeta de personas de tarjeta adaptable en el móvil." border="false":::

---

### <a name="request-ticket"></a><span data-ttu-id="3e76e-150">Ticket de solicitud</span><span class="sxs-lookup"><span data-stu-id="3e76e-150">Request ticket</span></span>

<span data-ttu-id="3e76e-151">Se usa para obtener entradas rápidas de un usuario para crear automáticamente una tarea o vale.</span><span class="sxs-lookup"><span data-stu-id="3e76e-151">Use to get quick inputs from a user to automatically create a task or ticket.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3e76e-152">Escritorio</span><span class="sxs-lookup"><span data-stu-id="3e76e-152">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="En el ejemplo se muestra una tarjeta de vale de solicitud de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3e76e-154">Móvil</span><span class="sxs-lookup"><span data-stu-id="3e76e-154">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="En el ejemplo se muestra una tarjeta de vale de solicitud de tarjeta adaptable en el móvil." border="false":::

---

### <a name="image-set"></a><span data-ttu-id="3e76e-156">Conjunto de imágenes</span><span class="sxs-lookup"><span data-stu-id="3e76e-156">Image set</span></span>

<span data-ttu-id="3e76e-157">Se usa para enviar varias miniaturas de imagen.</span><span class="sxs-lookup"><span data-stu-id="3e76e-157">Use to send multiple image thumbnails.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3e76e-158">Escritorio</span><span class="sxs-lookup"><span data-stu-id="3e76e-158">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de imágenes de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3e76e-160">Móvil</span><span class="sxs-lookup"><span data-stu-id="3e76e-160">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de imágenes de tarjeta adaptable en el móvil." border="false":::

---

### <a name="action-set"></a><span data-ttu-id="3e76e-162">Conjunto de acciones</span><span class="sxs-lookup"><span data-stu-id="3e76e-162">Action set</span></span>

<span data-ttu-id="3e76e-163">Úselo cuando desee que el usuario seleccione un botón y, a continuación, recopila la entrada de usuario adicional de la misma tarjeta.</span><span class="sxs-lookup"><span data-stu-id="3e76e-163">Use when you want to the user to select a button, then gather addition user input from the same card.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3e76e-164">Escritorio</span><span class="sxs-lookup"><span data-stu-id="3e76e-164">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de acciones de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3e76e-166">Móvil</span><span class="sxs-lookup"><span data-stu-id="3e76e-166">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de acciones de tarjeta adaptable en el móvil." border="false":::

---

### <a name="choice-set"></a><span data-ttu-id="3e76e-168">Conjunto de opciones</span><span class="sxs-lookup"><span data-stu-id="3e76e-168">Choice set</span></span>

<span data-ttu-id="3e76e-169">Se usa para recopilar varias entradas del usuario.</span><span class="sxs-lookup"><span data-stu-id="3e76e-169">Use to gather multiple inputs from the user.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3e76e-170">Escritorio</span><span class="sxs-lookup"><span data-stu-id="3e76e-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de opciones de tarjeta adaptable." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3e76e-172">Móvil</span><span class="sxs-lookup"><span data-stu-id="3e76e-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de opciones de tarjeta adaptable en el móvil." border="false":::

---

## <a name="anatomy"></a><span data-ttu-id="3e76e-174">Anatomía</span><span class="sxs-lookup"><span data-stu-id="3e76e-174">Anatomy</span></span>

<span data-ttu-id="3e76e-175">Las tarjetas adaptables tienen mucha flexibilidad.</span><span class="sxs-lookup"><span data-stu-id="3e76e-175">Adaptive Cards have a lot of flexibility.</span></span> <span data-ttu-id="3e76e-176">Pero, como mínimo, se recomienda incluir los siguientes componentes en cada tarjeta.</span><span class="sxs-lookup"><span data-stu-id="3e76e-176">But at minimum, we strongly suggest including the following components in every card.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3e76e-177">Escritorio</span><span class="sxs-lookup"><span data-stu-id="3e76e-177">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="EExample muestra la anatomía de la tarjeta adaptable." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3e76e-179">Móvil</span><span class="sxs-lookup"><span data-stu-id="3e76e-179">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="En el ejemplo se muestra la anatomía de la tarjeta adaptable en el móvil." border="false":::

---

|<span data-ttu-id="3e76e-181">Contador</span><span class="sxs-lookup"><span data-stu-id="3e76e-181">Counter</span></span>|<span data-ttu-id="3e76e-182">Descripción</span><span class="sxs-lookup"><span data-stu-id="3e76e-182">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="3e76e-183">A</span><span class="sxs-lookup"><span data-stu-id="3e76e-183">A</span></span>|<span data-ttu-id="3e76e-184">**Encabezado:** haga que los encabezados sea claros y concisos.</span><span class="sxs-lookup"><span data-stu-id="3e76e-184">**Header**: Make your headers clear and concise.</span></span>|
|<span data-ttu-id="3e76e-185">B</span><span class="sxs-lookup"><span data-stu-id="3e76e-185">B</span></span>|<span data-ttu-id="3e76e-186">**Copia del cuerpo:** transmita detalles que sean demasiado largos o que no sean lo suficientemente importantes como para incluirlos en el encabezado.</span><span class="sxs-lookup"><span data-stu-id="3e76e-186">**Body copy**: Convey details that are either too long or not important enough to include in the header.</span></span>|
|<span data-ttu-id="3e76e-187">C</span><span class="sxs-lookup"><span data-stu-id="3e76e-187">C</span></span>|<span data-ttu-id="3e76e-188">**Acciones principales:** Como práctica recomendada, incluya de 1 a 3 acciones principales.</span><span class="sxs-lookup"><span data-stu-id="3e76e-188">**Primary actions**: As a best practice, include 1-3 primary actions.</span></span> <span data-ttu-id="3e76e-189">Puede tener hasta seis.</span><span class="sxs-lookup"><span data-stu-id="3e76e-189">You can have up to six.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="3e76e-190">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="3e76e-190">Best practices</span></span>

<span data-ttu-id="3e76e-191">Usa estas recomendaciones para crear una experiencia de aplicación de calidad.</span><span class="sxs-lookup"><span data-stu-id="3e76e-191">Use these recommendations to create a quality app experience.</span></span>

### <a name="primary-and-secondary-actions"></a><span data-ttu-id="3e76e-192">Acciones principales y secundarias</span><span class="sxs-lookup"><span data-stu-id="3e76e-192">Primary and secondary actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="Procedimiento recomendado sobre cómo debe incluir solo un pequeño conjunto de acciones en una tarjeta adaptable." border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a><span data-ttu-id="3e76e-194">Hacer: usar hasta seis acciones principales</span><span class="sxs-lookup"><span data-stu-id="3e76e-194">Do: Use up to six primary actions</span></span>

<span data-ttu-id="3e76e-195">Aunque las tarjetas adaptables pueden admitir seis acciones principales, la mayoría de las tarjetas no lo necesitan.</span><span class="sxs-lookup"><span data-stu-id="3e76e-195">While Adaptive Cards can support six primary actions, most cards don’t need that.</span></span> <span data-ttu-id="3e76e-196">Las acciones deben ser claras, concisos y directas.</span><span class="sxs-lookup"><span data-stu-id="3e76e-196">Actions should be clear, concise, and straight forward.</span></span> <span data-ttu-id="3e76e-197">Menos es más.</span><span class="sxs-lookup"><span data-stu-id="3e76e-197">Less is more.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="Procedimiento recomendado sobre cómo no saturar a los usuarios con demasiadas acciones en una tarjeta adaptable." border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a><span data-ttu-id="3e76e-199">No usar más de seis acciones principales</span><span class="sxs-lookup"><span data-stu-id="3e76e-199">Don't: Use more than six primary actions</span></span>

<span data-ttu-id="3e76e-200">Las tarjetas adaptables deben presentar contenido rápido y fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="3e76e-200">Adaptive Cards should present quick, actionable content.</span></span> <span data-ttu-id="3e76e-201">Demasiadas acciones pueden saturar a un usuario.</span><span class="sxs-lookup"><span data-stu-id="3e76e-201">Too many actions can overwhelm a user.</span></span>

   :::column-end:::
:::row-end:::

### <a name="frequency"></a><span data-ttu-id="3e76e-202">Frecuencia</span><span class="sxs-lookup"><span data-stu-id="3e76e-202">Frequency</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="Procedimiento recomendado sobre la frecuencia de la tarjeta adaptable." border="false":::

#### <a name="do-be-concise"></a><span data-ttu-id="3e76e-204">Hacer: ser conciso</span><span class="sxs-lookup"><span data-stu-id="3e76e-204">Do: Be concise</span></span>

<span data-ttu-id="3e76e-205">Es fácil enviar varias tarjetas a una conversación, pero una vez que las tarjetas se desplacen fuera de la vista, se vuelven menos útiles.</span><span class="sxs-lookup"><span data-stu-id="3e76e-205">It's easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="3e76e-206">Intenta limitarte a lo esencial.</span><span class="sxs-lookup"><span data-stu-id="3e76e-206">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="3e76e-207">Esto es especialmente cierto en un canal donde los usuarios tienen menos tolerancia a lo que perciben como "ruido".</span><span class="sxs-lookup"><span data-stu-id="3e76e-207">This is especially true in a channel where users have less tolerance for what they perceive as "noise".</span></span>

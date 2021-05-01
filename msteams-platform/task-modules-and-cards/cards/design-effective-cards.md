---
title: Diseño de tarjetas adaptables para la aplicación
description: Obtén información sobre cómo diseñar tarjetas adaptables para Teams y obtener el kit Microsoft Teams interfaz de usuario.
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 14ffff1264e716e04a1ffb5549b71a8b7ec5fc14
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101740"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a><span data-ttu-id="a618a-103">Diseño de tarjetas adaptables para tu Microsoft Teams aplicación</span><span class="sxs-lookup"><span data-stu-id="a618a-103">Designing Adaptive Cards for your Microsoft Teams app</span></span>

<span data-ttu-id="a618a-104">Una tarjeta adaptable contiene un cuerpo de forma libre de elementos de tarjeta y un conjunto opcional de acciones.</span><span class="sxs-lookup"><span data-stu-id="a618a-104">An Adaptive Card contains a freeform body of card elements and optional set of actions.</span></span> <span data-ttu-id="a618a-105">Las tarjetas adaptables son fragmentos de contenido que se pueden usar y que se pueden agregar a una conversación a través de un bot o una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="a618a-105">Adaptive Cards are actionable snippets of content that you can add to a conversation through a bot or messaging extension.</span></span> <span data-ttu-id="a618a-106">Con texto, gráficos y botones, estas tarjetas proporcionan una comunicación enriquecte a tu audiencia.</span><span class="sxs-lookup"><span data-stu-id="a618a-106">Using text, graphics, and buttons, these cards provide rich communication to your audience.</span></span>

<span data-ttu-id="a618a-107">El marco de la tarjeta adaptable se usa en muchos productos de Microsoft, incluidos Teams.</span><span class="sxs-lookup"><span data-stu-id="a618a-107">The Adaptive Card framework is used across many Microsoft products, including Teams.</span></span> <span data-ttu-id="a618a-108">Puedes enviar tarjetas dentro de mensajes a los usuarios a través de bots o extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="a618a-108">You can send cards inside messages to users via bots or messaging extensions.</span></span> <span data-ttu-id="a618a-109">Los usuarios pueden realizar acciones en las tarjetas cuando están presentes.</span><span class="sxs-lookup"><span data-stu-id="a618a-109">Users can take actions on cards when present.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="Ejemplo de introducción a una tarjeta adaptable." border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="a618a-111">Kit de UI de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a618a-111">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="a618a-112">Puedes encontrar instrucciones de diseño más completas para las tarjetas adaptables en Teams, incluidos los elementos que puedes agarrar y modificar según sea necesario, en el kit de interfaz Microsoft Teams usuario.</span><span class="sxs-lookup"><span data-stu-id="a618a-112">You can find more comprehensive design guidelines for Adaptive Cards in Teams, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="a618a-113">El kit de interfaz de usuario también trata temas esenciales como temas, accesibilidad y tamaño dinámico.</span><span class="sxs-lookup"><span data-stu-id="a618a-113">The UI kit also covers essential topics such as theming, accessibility, and responsive sizing.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a618a-114">Obtener el Kit de UI de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="a618a-114">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a><span data-ttu-id="a618a-115">Diseñador de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="a618a-115">Adaptive Cards designer</span></span>

<span data-ttu-id="a618a-116">También puedes empezar a diseñar las tarjetas adaptables directamente en el explorador.</span><span class="sxs-lookup"><span data-stu-id="a618a-116">You also can start designing your Adaptive Cards directly in the browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a618a-117">Probar el diseñador de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="a618a-117">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a><span data-ttu-id="a618a-118">Tipos de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="a618a-118">Types of Adaptive Cards</span></span>

### <a name="hero"></a><span data-ttu-id="a618a-119">Elemento principal</span><span class="sxs-lookup"><span data-stu-id="a618a-119">Hero</span></span>

<span data-ttu-id="a618a-120">Nuestra tarjeta más grande.</span><span class="sxs-lookup"><span data-stu-id="a618a-120">Our largest card.</span></span> <span data-ttu-id="a618a-121">Se usa para compartir artículos o escenarios en los que una imagen cuenta la mayor parte del artículo.</span><span class="sxs-lookup"><span data-stu-id="a618a-121">Use for sharing articles or scenarios where an image tells most of the story.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="En el ejemplo se muestra una tarjeta de héroe de tarjeta adaptable." border="false":::

### <a name="thumbnail"></a><span data-ttu-id="a618a-123">Miniatura</span><span class="sxs-lookup"><span data-stu-id="a618a-123">Thumbnail</span></span>

<span data-ttu-id="a618a-124">Se usa para enviar un mensaje sencillo que puede usarse.</span><span class="sxs-lookup"><span data-stu-id="a618a-124">Use for sending a simple actionable message.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="En el ejemplo se muestra una tarjeta en miniatura de tarjeta adaptable." border="false":::

### <a name="list"></a><span data-ttu-id="a618a-126">Lista</span><span class="sxs-lookup"><span data-stu-id="a618a-126">List</span></span>

<span data-ttu-id="a618a-127">Se usa en escenarios en los que desea que el usuario elija un elemento de una lista, pero los elementos no necesitan mucha explicación.</span><span class="sxs-lookup"><span data-stu-id="a618a-127">Use in scenarios where you want the user to pick an item from a list, but the items don’t need a lot of explanation.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="En el ejemplo se muestra una tarjeta de lista de tarjeta adaptable." border="false":::

### <a name="digest"></a><span data-ttu-id="a618a-129">Digest</span><span class="sxs-lookup"><span data-stu-id="a618a-129">Digest</span></span>

<span data-ttu-id="a618a-130">Se usa para resúmenes de noticias y publicaciones de redondear.</span><span class="sxs-lookup"><span data-stu-id="a618a-130">Use for news digests and round-up posts.</span></span> <span data-ttu-id="a618a-131">Nota: Se recomienda la tarjeta en miniatura para una sola actualización o elemento de noticias.</span><span class="sxs-lookup"><span data-stu-id="a618a-131">Note: We recommend the thumbnail card for a single update or news item.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="En el ejemplo se muestra una tarjeta implícita de tarjeta adaptable." border="false":::

### <a name="media"></a><span data-ttu-id="a618a-133">Elementos multimedia</span><span class="sxs-lookup"><span data-stu-id="a618a-133">Media</span></span>

<span data-ttu-id="a618a-134">Úsalo cuando quieras combinar texto y medios, como audio o vídeo.</span><span class="sxs-lookup"><span data-stu-id="a618a-134">Use when you want to combine text and media, like audio or video.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="En el ejemplo se muestra una tarjeta multimedia de tarjeta adaptable." border="false":::

### <a name="people"></a><span data-ttu-id="a618a-136">Personas</span><span class="sxs-lookup"><span data-stu-id="a618a-136">People</span></span>

<span data-ttu-id="a618a-137">Se usa mejor cuando se transmite de forma eficaz quién está implicado en una tarea.</span><span class="sxs-lookup"><span data-stu-id="a618a-137">Best used when you to efficiently convey who's involved with a task.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="En el ejemplo se muestra una tarjeta de personas de tarjeta adaptable." border="false":::

### <a name="request-ticket"></a><span data-ttu-id="a618a-139">Ticket de solicitud</span><span class="sxs-lookup"><span data-stu-id="a618a-139">Request ticket</span></span>

<span data-ttu-id="a618a-140">Se usa para obtener entradas rápidas de un usuario para crear automáticamente una tarea o vale.</span><span class="sxs-lookup"><span data-stu-id="a618a-140">Use to get quick inputs from a user to automatically create a task or ticket.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="En el ejemplo se muestra una tarjeta de vale de solicitud de tarjeta adaptable." border="false":::

### <a name="imageset"></a><span data-ttu-id="a618a-142">ImageSet</span><span class="sxs-lookup"><span data-stu-id="a618a-142">ImageSet</span></span>

<span data-ttu-id="a618a-143">Se usa para enviar varias miniaturas de imagen.</span><span class="sxs-lookup"><span data-stu-id="a618a-143">Use to send multiple image thumbnails.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de imágenes de tarjeta adaptable." border="false":::

### <a name="actionset"></a><span data-ttu-id="a618a-145">ActionSet</span><span class="sxs-lookup"><span data-stu-id="a618a-145">ActionSet</span></span>

<span data-ttu-id="a618a-146">Úselo cuando desee que el usuario seleccione un botón y, a continuación, recopila la entrada de usuario adicional de la misma tarjeta.</span><span class="sxs-lookup"><span data-stu-id="a618a-146">Use when you want to the user to select a button, then gather addition user input from the same card.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de acciones de tarjeta adaptable." border="false":::

### <a name="choiceset"></a><span data-ttu-id="a618a-148">ChoiceSet</span><span class="sxs-lookup"><span data-stu-id="a618a-148">ChoiceSet</span></span>

<span data-ttu-id="a618a-149">Se usa para recopilar varias entradas del usuario.</span><span class="sxs-lookup"><span data-stu-id="a618a-149">Use to gather multiple inputs from the user.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="En el ejemplo se muestra una tarjeta de conjunto de opciones de tarjeta adaptable." border="false":::

## <a name="anatomy"></a><span data-ttu-id="a618a-151">Anatomía</span><span class="sxs-lookup"><span data-stu-id="a618a-151">Anatomy</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="En el ejemplo se muestra una tarjeta de anatomía de tarjeta adaptable." border="false":::

<span data-ttu-id="a618a-153">Las tarjetas adaptables tienen mucha flexibilidad.</span><span class="sxs-lookup"><span data-stu-id="a618a-153">Adaptive Cards have a lot of flexibility.</span></span> <span data-ttu-id="a618a-154">Pero, como mínimo, se recomienda incluir los siguientes componentes en cada tarjeta:</span><span class="sxs-lookup"><span data-stu-id="a618a-154">But at minimum, we strongly suggest including the following components in every card:</span></span>

|<span data-ttu-id="a618a-155">Contador</span><span class="sxs-lookup"><span data-stu-id="a618a-155">Counter</span></span>|<span data-ttu-id="a618a-156">Descripción</span><span class="sxs-lookup"><span data-stu-id="a618a-156">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a618a-157">A</span><span class="sxs-lookup"><span data-stu-id="a618a-157">A</span></span>|<span data-ttu-id="a618a-158">**Encabezado:** haga que los encabezados sea claros y concisos, pero descriptivos.</span><span class="sxs-lookup"><span data-stu-id="a618a-158">**Header**: Make headers clear and concise, yet descriptive.</span></span>|
|<span data-ttu-id="a618a-159">B</span><span class="sxs-lookup"><span data-stu-id="a618a-159">B</span></span>|<span data-ttu-id="a618a-160">**Copia del cuerpo:** se usa para transmitir detalles que son demasiado largos o que no son lo suficientemente importantes como para incluirlos en el encabezado.</span><span class="sxs-lookup"><span data-stu-id="a618a-160">**Body copy**: Use to convey detail that is either too long or not important enough to include in the header.</span></span>|
|<span data-ttu-id="a618a-161">C</span><span class="sxs-lookup"><span data-stu-id="a618a-161">C</span></span>|<span data-ttu-id="a618a-162">**Acciones principales:** Como práctica recomendada, incluya de 1 a 3 acciones principales.</span><span class="sxs-lookup"><span data-stu-id="a618a-162">**Primary actions**: As a best practice, include 1-3 primary actions.</span></span> <span data-ttu-id="a618a-163">Se permite un máximo de seis.</span><span class="sxs-lookup"><span data-stu-id="a618a-163">A maximum of six are allowed.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="a618a-164">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="a618a-164">Best practices</span></span>

<span data-ttu-id="a618a-165">Usa estas recomendaciones para crear una experiencia de aplicación de calidad.</span><span class="sxs-lookup"><span data-stu-id="a618a-165">Use these recommendations to create a quality app experience.</span></span>

### <a name="primary-and-secondary-actions"></a><span data-ttu-id="a618a-166">Acciones principales y secundarias</span><span class="sxs-lookup"><span data-stu-id="a618a-166">Primary and secondary actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="Procedimiento recomendado sobre cómo debe incluir solo un pequeño conjunto de acciones en una tarjeta adaptable." border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a><span data-ttu-id="a618a-168">Hacer: usar hasta seis acciones principales</span><span class="sxs-lookup"><span data-stu-id="a618a-168">Do: Use up to six primary actions</span></span>

<span data-ttu-id="a618a-169">Aunque las tarjetas adaptables pueden admitir seis acciones principales, la mayoría de las tarjetas no lo necesitan.</span><span class="sxs-lookup"><span data-stu-id="a618a-169">While Adaptive Cards can support six primary actions, most cards don’t need that.</span></span> <span data-ttu-id="a618a-170">Las acciones deben ser claras, concisos y directas.</span><span class="sxs-lookup"><span data-stu-id="a618a-170">Actions should be clear, concise, and straight forward.</span></span> <span data-ttu-id="a618a-171">Menos es más.</span><span class="sxs-lookup"><span data-stu-id="a618a-171">Less is more.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="Procedimiento recomendado sobre cómo no saturar a los usuarios con demasiadas acciones en una tarjeta adaptable." border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a><span data-ttu-id="a618a-173">No usar más de seis acciones principales</span><span class="sxs-lookup"><span data-stu-id="a618a-173">Don't: Use more than six primary actions</span></span>

<span data-ttu-id="a618a-174">Las tarjetas adaptables deben presentar contenido rápido y fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="a618a-174">Adaptive Cards should present quick, actionable content.</span></span> <span data-ttu-id="a618a-175">Demasiadas acciones pueden saturar a un usuario.</span><span class="sxs-lookup"><span data-stu-id="a618a-175">Too many actions can overwhelm a user.</span></span>

   :::column-end:::
:::row-end:::

### <a name="frequency"></a><span data-ttu-id="a618a-176">Frecuencia</span><span class="sxs-lookup"><span data-stu-id="a618a-176">Frequency</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="Procedimiento recomendado sobre la frecuencia de la tarjeta adaptable." border="false":::

#### <a name="do-be-concise"></a><span data-ttu-id="a618a-178">Hacer: ser conciso</span><span class="sxs-lookup"><span data-stu-id="a618a-178">Do: Be concise</span></span>

<span data-ttu-id="a618a-179">Es fácil enviar varias tarjetas a una conversación, pero una vez que las tarjetas se desplacen fuera de la vista, se vuelven menos útiles.</span><span class="sxs-lookup"><span data-stu-id="a618a-179">It's easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="a618a-180">Intenta limitarte a lo esencial.</span><span class="sxs-lookup"><span data-stu-id="a618a-180">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="a618a-181">Esto es especialmente cierto en un canal donde los usuarios tienen menos tolerancia a lo que perciben como "ruido".</span><span class="sxs-lookup"><span data-stu-id="a618a-181">This is especially true in a channel where users have less tolerance for what they perceive as "noise".</span></span>

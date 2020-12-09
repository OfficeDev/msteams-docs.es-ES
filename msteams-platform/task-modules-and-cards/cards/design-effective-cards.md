---
title: Diseño de tarjetas adaptables para la aplicación
description: Obtenga información sobre cómo diseñar tarjetas adaptables para Teams y obtener el kit de la interfaz de usuario de Microsoft Teams.
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: bd48846284620415cc8cadabc59f2ab7b61d5189
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604557"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a><span data-ttu-id="87278-103">Diseño de tarjetas adaptables para su aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="87278-103">Designing Adaptive Cards for your Microsoft Teams app</span></span>

<span data-ttu-id="87278-104">Una tarjeta adaptable contiene un cuerpo de forma libre de elementos de tarjeta y un conjunto opcional de acciones.</span><span class="sxs-lookup"><span data-stu-id="87278-104">An Adaptive Card contains a freeform body of card elements and optional set of actions.</span></span> <span data-ttu-id="87278-105">Las tarjetas adaptables son fragmentos de código accionables que puede Agregar a una conversación a través de un bot o una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="87278-105">Adaptive Cards are actionable snippets of content that you can add to a conversation through a bot or messaging extension.</span></span> <span data-ttu-id="87278-106">Mediante el uso de texto, gráficos y botones, estas tarjetas proporcionan una comunicación enriquecida a la audiencia.</span><span class="sxs-lookup"><span data-stu-id="87278-106">Using text, graphics, and buttons, these cards provide rich communication to your audience.</span></span>

<span data-ttu-id="87278-107">El marco de tarjeta adaptable se usa en muchos productos de Microsoft, incluidos Teams.</span><span class="sxs-lookup"><span data-stu-id="87278-107">The Adaptive Card framework is used across many Microsoft products, including Teams.</span></span> <span data-ttu-id="87278-108">Puede enviar tarjetas dentro de los mensajes a los usuarios a través de bots o extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="87278-108">You can send cards inside messages to users via bots or messaging extensions.</span></span> <span data-ttu-id="87278-109">Los usuarios pueden realizar acciones en las tarjetas cuando están presentes.</span><span class="sxs-lookup"><span data-stu-id="87278-109">Users can take actions on cards when present.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="Ejemplo muestra una tarjeta adaptable." border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="87278-111">Kit de IU de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="87278-111">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="87278-112">Puede encontrar directrices de diseño más completas para las tarjetas adaptables en Microsoft Teams, incluidos los elementos que puede captar y modificar según sea necesario, en el kit de interfaz de usuario de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="87278-112">You can find more comprehensive design guidelines for Adaptive Cards in Teams, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="87278-113">El kit de la interfaz de usuario también cubre temas esenciales como temas de temas, accesibilidad y ajuste de tamaño.</span><span class="sxs-lookup"><span data-stu-id="87278-113">The UI kit also covers essential topics such as theming, accessibility, and responsive sizing.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="87278-114">Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="87278-114">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a><span data-ttu-id="87278-115">Diseñador de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="87278-115">Adaptive Cards designer</span></span>

<span data-ttu-id="87278-116">También puede empezar a diseñar sus tarjetas adaptables directamente en el explorador.</span><span class="sxs-lookup"><span data-stu-id="87278-116">You also can start designing your Adaptive Cards directly in the browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="87278-117">Pruebe el diseñador de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="87278-117">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a><span data-ttu-id="87278-118">Tipos de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="87278-118">Types of Adaptive Cards</span></span>

### <a name="hero"></a><span data-ttu-id="87278-119">Elemento principal</span><span class="sxs-lookup"><span data-stu-id="87278-119">Hero</span></span>

<span data-ttu-id="87278-120">Nuestra tarjeta más grande.</span><span class="sxs-lookup"><span data-stu-id="87278-120">Our largest card.</span></span> <span data-ttu-id="87278-121">Use para compartir artículos o escenarios en los que una imagen indica la mayor parte del artículo.</span><span class="sxs-lookup"><span data-stu-id="87278-121">Use for sharing articles or scenarios where an image tells most of the story.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="Ejemplo muestra una tarjeta adaptable." border="false":::

### <a name="thumbnail"></a><span data-ttu-id="87278-123">Thumbnail</span><span class="sxs-lookup"><span data-stu-id="87278-123">Thumbnail</span></span>

<span data-ttu-id="87278-124">Usar para enviar un mensaje accionable sencillo.</span><span class="sxs-lookup"><span data-stu-id="87278-124">Use for sending a simple actionable message.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="Ejemplo muestra una tarjeta adaptable." border="false":::

### <a name="list"></a><span data-ttu-id="87278-126">Lista</span><span class="sxs-lookup"><span data-stu-id="87278-126">List</span></span>

<span data-ttu-id="87278-127">Úselo en escenarios donde desea que el usuario seleccione un elemento de una lista, pero los elementos no necesitan mucha explicación.</span><span class="sxs-lookup"><span data-stu-id="87278-127">Use in scenarios where you want the user to pick an item from a list, but the items don’t need a lot of explanation.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="Ejemplo muestra una tarjeta adaptable." border="false":::

### <a name="digest"></a><span data-ttu-id="87278-129">Digest</span><span class="sxs-lookup"><span data-stu-id="87278-129">Digest</span></span>

<span data-ttu-id="87278-130">Se usa para resúmenes de noticias y entradas de redondeo.</span><span class="sxs-lookup"><span data-stu-id="87278-130">Use for news digests and round-up posts.</span></span> <span data-ttu-id="87278-131">Nota: se recomienda usar la tarjeta en miniatura para un solo elemento de actualización o de noticias.</span><span class="sxs-lookup"><span data-stu-id="87278-131">Note: We recommend the thumbnail card for a single update or news item.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="Ejemplo muestra una tarjeta adaptable." border="false":::

### <a name="media"></a><span data-ttu-id="87278-133">Audiovisual</span><span class="sxs-lookup"><span data-stu-id="87278-133">Media</span></span>

<span data-ttu-id="87278-134">Se usa cuando se desea combinar texto y medios, como audio o vídeo.</span><span class="sxs-lookup"><span data-stu-id="87278-134">Use when you want to combine text and media, like audio or video.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="Ejemplo muestra una tarjeta adaptable." border="false":::

### <a name="people"></a><span data-ttu-id="87278-136">Contactos</span><span class="sxs-lookup"><span data-stu-id="87278-136">People</span></span>

<span data-ttu-id="87278-137">Se usa mejor para transmitir con eficacia quién está implicado en una tarea.</span><span class="sxs-lookup"><span data-stu-id="87278-137">Best used when you to efficiently convey who's involved with a task.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="Ejemplo muestra una tarjeta adaptable." border="false":::

### <a name="request-ticket"></a><span data-ttu-id="87278-139">Vale de solicitud</span><span class="sxs-lookup"><span data-stu-id="87278-139">Request ticket</span></span>

<span data-ttu-id="87278-140">Usar para obtener entradas rápidas de un usuario para crear automáticamente una tarea o un vale.</span><span class="sxs-lookup"><span data-stu-id="87278-140">Use to get quick inputs from a user to automatically create a task or ticket.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="Ejemplo muestra una tarjeta adaptable." border="false":::

### <a name="imageset"></a><span data-ttu-id="87278-142">ImageSet</span><span class="sxs-lookup"><span data-stu-id="87278-142">ImageSet</span></span>

<span data-ttu-id="87278-143">Use para enviar varias miniaturas de imagen.</span><span class="sxs-lookup"><span data-stu-id="87278-143">Use to send multiple image thumbnails.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="Ejemplo muestra una tarjeta adaptable." border="false":::

### <a name="actionset"></a><span data-ttu-id="87278-145">ActionSet</span><span class="sxs-lookup"><span data-stu-id="87278-145">ActionSet</span></span>

<span data-ttu-id="87278-146">Use esta opción cuando quiera que el usuario seleccione un botón y, a continuación, reúna los datos proporcionados por el usuario desde la misma tarjeta.</span><span class="sxs-lookup"><span data-stu-id="87278-146">Use when you want to the user to select a button, then gather addition user input from the same card.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="Ejemplo muestra una tarjeta adaptable." border="false":::

### <a name="choiceset"></a><span data-ttu-id="87278-148">ChoiceSet</span><span class="sxs-lookup"><span data-stu-id="87278-148">ChoiceSet</span></span>

<span data-ttu-id="87278-149">Usar para recopilar varias entradas del usuario.</span><span class="sxs-lookup"><span data-stu-id="87278-149">Use to gather multiple inputs from the user.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="Ejemplo muestra una tarjeta adaptable." border="false":::

## <a name="anatomy"></a><span data-ttu-id="87278-151">Anatomía</span><span class="sxs-lookup"><span data-stu-id="87278-151">Anatomy</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una tarjeta adaptable." border="false":::

<span data-ttu-id="87278-153">Las tarjetas adaptables tienen mucha flexibilidad.</span><span class="sxs-lookup"><span data-stu-id="87278-153">Adaptive Cards have a lot of flexibility.</span></span> <span data-ttu-id="87278-154">Pero, como mínimo, se recomienda incluir los siguientes componentes en cada tarjeta:</span><span class="sxs-lookup"><span data-stu-id="87278-154">But at a minimum, we strongly suggest including the following components in every card:</span></span>

|<span data-ttu-id="87278-155">Counter</span><span class="sxs-lookup"><span data-stu-id="87278-155">Counter</span></span>|<span data-ttu-id="87278-156">Descripción</span><span class="sxs-lookup"><span data-stu-id="87278-156">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="87278-157">A</span><span class="sxs-lookup"><span data-stu-id="87278-157">A</span></span>|<span data-ttu-id="87278-158">**Header**: hacer que los encabezados sean claros y concisos, pero descriptivos.</span><span class="sxs-lookup"><span data-stu-id="87278-158">**Header**: Make headers clear and concise, yet descriptive.</span></span>|
|<span data-ttu-id="87278-159">B</span><span class="sxs-lookup"><span data-stu-id="87278-159">B</span></span>|<span data-ttu-id="87278-160">**Copia del cuerpo**: Use para transmitir detalles que sean demasiado largos o que no sean lo suficientemente grandes como para incluirlos en el encabezado.</span><span class="sxs-lookup"><span data-stu-id="87278-160">**Body copy**: Use to convey detail that is either too long or not important enough to include in the header.</span></span>|
|<span data-ttu-id="87278-161">C</span><span class="sxs-lookup"><span data-stu-id="87278-161">C</span></span>|<span data-ttu-id="87278-162">**Acciones principales**: como procedimiento recomendado, incluya las acciones principales de 1-3.</span><span class="sxs-lookup"><span data-stu-id="87278-162">**Primary actions**: As a best practice, include 1-3 primary actions.</span></span> <span data-ttu-id="87278-163">Se permiten seis como máximo.</span><span class="sxs-lookup"><span data-stu-id="87278-163">A maximum of six are allowed.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="87278-164">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="87278-164">Best practices</span></span>

### <a name="primary-and-secondary-actions"></a><span data-ttu-id="87278-165">Acciones principales y secundarias</span><span class="sxs-lookup"><span data-stu-id="87278-165">Primary and secondary actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de tarjetas adaptables." border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a><span data-ttu-id="87278-167">Do: usar hasta seis acciones principales</span><span class="sxs-lookup"><span data-stu-id="87278-167">Do: Use up to six primary actions</span></span>

<span data-ttu-id="87278-168">Aunque las tarjetas adaptables pueden admitir seis acciones principales, la mayoría de las cartas no las necesitan.</span><span class="sxs-lookup"><span data-stu-id="87278-168">While Adaptive Cards can support six primary actions, most cards don’t need that.</span></span> <span data-ttu-id="87278-169">Las acciones deben ser claras, concisas y directas.</span><span class="sxs-lookup"><span data-stu-id="87278-169">Actions should be clear, concise, and straight forward.</span></span> <span data-ttu-id="87278-170">Menos es más.</span><span class="sxs-lookup"><span data-stu-id="87278-170">Less is more.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de tarjetas adaptables." border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a><span data-ttu-id="87278-172">No: usar más de seis acciones principales</span><span class="sxs-lookup"><span data-stu-id="87278-172">Don't: Use more than six primary actions</span></span>

<span data-ttu-id="87278-173">Las tarjetas adaptables deben presentar contenido rápido y accionable.</span><span class="sxs-lookup"><span data-stu-id="87278-173">Adaptive Cards should present quick, actionable content.</span></span> <span data-ttu-id="87278-174">Muchas acciones pueden sobrecargar a un usuario.</span><span class="sxs-lookup"><span data-stu-id="87278-174">Too many actions can overwhelm a user.</span></span>

   :::column-end:::
:::row-end:::

### <a name="frequency"></a><span data-ttu-id="87278-175">Frecuencia</span><span class="sxs-lookup"><span data-stu-id="87278-175">Frequency</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de tarjetas adaptables." border="false":::

#### <a name="do-be-concise"></a><span data-ttu-id="87278-177">Do: ser conciso</span><span class="sxs-lookup"><span data-stu-id="87278-177">Do: Be concise</span></span>

<span data-ttu-id="87278-178">Es fácil enviar varias tarjetas a una conversación, pero una vez que las tarjetas se desplazan fuera de la vista, se vuelven menos útiles.</span><span class="sxs-lookup"><span data-stu-id="87278-178">It's easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="87278-179">Intente limitarse a los conceptos básicos.</span><span class="sxs-lookup"><span data-stu-id="87278-179">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="87278-180">Esto es especialmente cierto en un canal en el que los usuarios tienen menos tolerancia para lo que perciben como "ruido".</span><span class="sxs-lookup"><span data-stu-id="87278-180">This is especially true in a channel where users have less tolerance for what they perceive as "noise".</span></span>

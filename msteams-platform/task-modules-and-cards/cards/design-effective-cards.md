---
title: Diseño de tarjetas eficaces
description: Describe las instrucciones de diseño para crear tarjetas
keywords: Directrices de diseño de Microsoft Teams tarjetas de marco de referencia adaptables ligeras
ms.openlocfilehash: 33ee0b59a3a5a1490d6e2106f8532094ed852598
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676151"
---
# <a name="designing-effective-cards"></a><span data-ttu-id="8c984-104">Diseño de tarjetas eficaces</span><span class="sxs-lookup"><span data-stu-id="8c984-104">Designing effective cards</span></span>

<span data-ttu-id="8c984-105">Las tarjetas son fragmentos de código accionables que puede Agregar a una conversación a través de un bot, un conector o una aplicación.</span><span class="sxs-lookup"><span data-stu-id="8c984-105">Cards are actionable snippets of content that you can add to a conversation through a bot, a connector, or app.</span></span> <span data-ttu-id="8c984-106">Mediante el uso de texto, gráficos y botones, las tarjetas le permiten comunicarse con una audiencia.</span><span class="sxs-lookup"><span data-stu-id="8c984-106">Using text, graphics, and buttons, cards allow you to communicate with an audience.</span></span>

<span data-ttu-id="8c984-107">Nuestro marco de tarjeta elimina la carga de diseñar una experiencia de usuario completamente funcional.</span><span class="sxs-lookup"><span data-stu-id="8c984-107">Our card framework eliminates the burden of designing a fully functional UX.</span></span> <span data-ttu-id="8c984-108">Hemos desarrollado varios tipos de tarjetas estándar y cada una se ajusta a las plataformas admitidas.</span><span class="sxs-lookup"><span data-stu-id="8c984-108">We developed several standard card types and each one fits within our supported platforms.</span></span> <span data-ttu-id="8c984-109">Esto significa que el diseño se ha realizado por completo y que no necesitará desarrollar distintas iteraciones de tarjeta entre plataformas.</span><span class="sxs-lookup"><span data-stu-id="8c984-109">This means layout is completely taken care of, and you won’t need to develop different card iterations across platforms.</span></span> <span data-ttu-id="8c984-110">En su lugar, puede centrarse en marcar el contenido.</span><span class="sxs-lookup"><span data-stu-id="8c984-110">Instead, you can focus on dialing in your content.</span></span>

---

## <a name="guidelines"></a><span data-ttu-id="8c984-111">Instrucciones</span><span class="sxs-lookup"><span data-stu-id="8c984-111">Guidelines</span></span>

<span data-ttu-id="8c984-112">Piense en una tarjeta como una respuesta a una pregunta de un usuario o una configuración.</span><span class="sxs-lookup"><span data-stu-id="8c984-112">Think of a card as a response to a user question or a setting.</span></span> <span data-ttu-id="8c984-113">Una tarjeta puede responder a una pregunta directa (como, por ejemplo, "¿cuántos errores abiertos tengo?") o a una condición (como, "enviar una lista de mis errores abiertos en 9 a.m. todos los días").</span><span class="sxs-lookup"><span data-stu-id="8c984-113">A card can respond to a direct question (like, “How many open bugs do I have?”) or to a condition (like, “Send a list of my open bugs at 9 am every day”).</span></span>

> [!TIP]
> <span data-ttu-id="8c984-114">Usar uno de los tipos de tarjetas estándar significa que ya sabrá que todas las respuestas se representarán de forma agradable en cada plataforma compatible.</span><span class="sxs-lookup"><span data-stu-id="8c984-114">Using one of our standard card types means you’ll already know that all your responses will render nicely across each supported platform.</span></span>

<span data-ttu-id="8c984-115">Una tarjeta puede incluir cualquiera de los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="8c984-115">A card could include any of the following elements:</span></span><br />

[!include[Card anatomy](~/includes/design/card-image-anatomy.html)]

1. <span data-ttu-id="8c984-116">**Texto sobre**: se usa mejor para los mensajes de chat.</span><span class="sxs-lookup"><span data-stu-id="8c984-116">**Envelope text**: Best used for chat messages.</span></span> <span data-ttu-id="8c984-117">Por ejemplo, si desea que un bot diga: "Esto es lo que me he encontrado".</span><span class="sxs-lookup"><span data-stu-id="8c984-117">For example, if you want a bot to say: “Here’s what I found!”</span></span> <span data-ttu-id="8c984-118">o "tiempo para el Resumen de noticias de 1:00", el mensaje se muestra mejor en el texto sobre.</span><span class="sxs-lookup"><span data-stu-id="8c984-118">or “Time for your 1:00 news digest”, that message is best displayed in envelope text.</span></span>

   <span data-ttu-id="8c984-119">El texto sobre es una excelente forma de inyectar un poco de personalidad en su servicio, simplemente Recuerde que debe mantenerlo relativamente corto.</span><span class="sxs-lookup"><span data-stu-id="8c984-119">Envelope text is a great way to inject a little personality into your service—just remember to keep it relatively short.</span></span>

2. <span data-ttu-id="8c984-120">**Título**: el título siempre será el texto más grande de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="8c984-120">**Title**: Your title will always be the largest text in your card.</span></span> <span data-ttu-id="8c984-121">También sirve como "enlace", por lo que debe intentar mantener el título corto, memorable y fácil de examinar.</span><span class="sxs-lookup"><span data-stu-id="8c984-121">It also serves as your “hook”, so try to keep the title short, memorable, and easy to scan.</span></span>

3. <span data-ttu-id="8c984-122">**Subtítulo**: se usa mejor para la atribución, las consignaciones o como una directiva secundaria.</span><span class="sxs-lookup"><span data-stu-id="8c984-122">**Subtitle**: Best used for attribution, taglines, or as a secondary directive.</span></span> <span data-ttu-id="8c984-123">Este componente aparece justo debajo del título.</span><span class="sxs-lookup"><span data-stu-id="8c984-123">This component appears just below your title.</span></span>

4. <span data-ttu-id="8c984-124">**Imagen**: la escala de las imágenes se ajusta a su contenedor.</span><span class="sxs-lookup"><span data-stu-id="8c984-124">**Image**: Images scale to fit their container.</span></span> <span data-ttu-id="8c984-125">Las tarjetas de Hero tienen un ancho máximo de 420px, las miniaturas tienen un ancho máximo de 100px y las vistas de lista solo permiten 32 en el modo de escritorio.</span><span class="sxs-lookup"><span data-stu-id="8c984-125">Hero cards have a max width of 420px, thumbnails have a max width of 100px, and list views only allow for 32px in desktop mode.</span></span>

5. <span data-ttu-id="8c984-126">**Text**: el mejor uso para texto sin formato en el cuerpo de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="8c984-126">**Text**: Best used for plain text in the body of your card.</span></span> <span data-ttu-id="8c984-127">La longitud máxima depende del tipo de tarjeta que haya seleccionado.</span><span class="sxs-lookup"><span data-stu-id="8c984-127">Your max length depends on the card type you’ve selected.</span></span>

6. <span data-ttu-id="8c984-128">**Botones**: se usa mejor para abrir páginas web, pestañas o contenido adicional de chat.</span><span class="sxs-lookup"><span data-stu-id="8c984-128">**Buttons**: Best used to open web pages, tabs, or additional chat content.</span></span> <span data-ttu-id="8c984-129">Asegúrese de mantener el texto del botón corto y en el punto.</span><span class="sxs-lookup"><span data-stu-id="8c984-129">Make sure to keep your button text short and to the point.</span></span>

   <span data-ttu-id="8c984-130">Puede incluir hasta 6 botones por tarjeta, pero recomendamos seguir una filosofía de "menor es más".</span><span class="sxs-lookup"><span data-stu-id="8c984-130">You can include up to 6 buttons per card, but we’d recommend following a ‘less is more’ philosophy here.</span></span>

7. <span data-ttu-id="8c984-131">**Pulse región**: es la región en la que se hace clic de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="8c984-131">**Tap region**: This is the clickable region of your card.</span></span> <span data-ttu-id="8c984-132">La mayoría de los usuarios querrán hacer clic en las imágenes de forma automática, así que pruebe y diseñe el texto para que sepan dónde deben puntear o haga clic.</span><span class="sxs-lookup"><span data-stu-id="8c984-132">Most users will want to click on images automatically, so try and craft your text so they know where they should tap or click.</span></span>

> [!TIP]
> <span data-ttu-id="8c984-133">No es necesario incluir todos los elementos de cada tarjeta que cree.</span><span class="sxs-lookup"><span data-stu-id="8c984-133">There’s no need to include every element in each card you create.</span></span> <span data-ttu-id="8c984-134">Permita que el contenido dicte sus elementos.</span><span class="sxs-lookup"><span data-stu-id="8c984-134">Let your content dictate your elements.</span></span>

---

## <a name="types-of-cards"></a><span data-ttu-id="8c984-135">Tipos de tarjetas</span><span class="sxs-lookup"><span data-stu-id="8c984-135">Types of cards</span></span>

### <a name="hero"></a><span data-ttu-id="8c984-136">Elemento principal</span><span class="sxs-lookup"><span data-stu-id="8c984-136">Hero</span></span>

<span data-ttu-id="8c984-137">Nuestra tarjeta más grande.</span><span class="sxs-lookup"><span data-stu-id="8c984-137">Our largest card.</span></span> <span data-ttu-id="8c984-138">Se usa mejor para artículos, descripciones largas o escenarios en los que la imagen está indicando la mayor parte del artículo.</span><span class="sxs-lookup"><span data-stu-id="8c984-138">Best used for articles, long descriptions, or scenarios where your image is telling most of the story.</span></span>

[!include[Card anatomy](~/includes/design/card-image-hero.html)]

### <a name="thumbnail"></a><span data-ttu-id="8c984-139">Thumbnail</span><span class="sxs-lookup"><span data-stu-id="8c984-139">Thumbnail</span></span>

<span data-ttu-id="8c984-140">Corta y agradable.</span><span class="sxs-lookup"><span data-stu-id="8c984-140">Short and sweet.</span></span> <span data-ttu-id="8c984-141">Estas tarjetas son ideales para respuestas breves o si desea devolver varias tarjetas a la vez para que el usuario pueda elegir entre varias opciones.</span><span class="sxs-lookup"><span data-stu-id="8c984-141">These cards are ideal for short answers, or if you want to return several cards at once so the user can choose from a bunch of options.</span></span> <span data-ttu-id="8c984-142">Creemos que estos son una estupenda manera de crear un vínculo profundo a otra pestaña o un servicio Web.</span><span class="sxs-lookup"><span data-stu-id="8c984-142">We think these are a great way to deep link to another tab or a web service.</span></span>

[!include[Card anatomy](~/includes/design/card-image-thumbnail.html)]

### <a name="sign-in"></a><span data-ttu-id="8c984-143">Iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="8c984-143">Sign in</span></span>

<span data-ttu-id="8c984-144">Algunos servicios requieren que los usuarios inicien sesión independientemente de la autenticación.</span><span class="sxs-lookup"><span data-stu-id="8c984-144">Some services require users to sign in independently of our authentication.</span></span> <span data-ttu-id="8c984-145">En ese caso, deberá presentar una tarjeta de inicio de sesión antes de que el usuario pueda conectarse a su servicio.</span><span class="sxs-lookup"><span data-stu-id="8c984-145">In that event, you would present a sign-in card before the user can connect to your service.</span></span>

[!include[Card anatomy](~/includes/design/card-image-signin.html)]

> [!TIP]
> <span data-ttu-id="8c984-146">Limite las repeticiones de una tarjeta de inicio de sesión adicional, ya que constituyen una rugosidad de velocidad significativa para los nuevos usuarios.</span><span class="sxs-lookup"><span data-stu-id="8c984-146">Limit the occurrences of an additional sign-in card since they pose a significant speed bump for new users.</span></span>

---

## <a name="card-collections"></a><span data-ttu-id="8c984-147">Colecciones de tarjetas</span><span class="sxs-lookup"><span data-stu-id="8c984-147">Card collections</span></span>

<span data-ttu-id="8c984-148">También tenemos tipos de tarjeta estándar que se usan mejor cuando desea presentar varias partes de contenido a la vez o en una sucesión rápida.</span><span class="sxs-lookup"><span data-stu-id="8c984-148">We also have standard card types that are best used when you want to present several pieces of content at once or in quick succession.</span></span> <span data-ttu-id="8c984-149">Para ello, tenemos un carrusel, un resumen, una lista y lo que llamamos "combinación de burbujas".</span><span class="sxs-lookup"><span data-stu-id="8c984-149">For that purpose, we have a carousel, a digest, a list, and what we call a ‘bubble merge’.</span></span>

### <a name="carousel"></a><span data-ttu-id="8c984-150">Carrusel</span><span class="sxs-lookup"><span data-stu-id="8c984-150">Carousel</span></span>

<span data-ttu-id="8c984-151">Se usa mejor para artículos, compras y examen de tarjetas.</span><span class="sxs-lookup"><span data-stu-id="8c984-151">Best used for articles, shopping, and browsing through cards.</span></span>

[!include[Card anatomy](~/includes/design/card-image-carousel.html)]

> [!TIP]
> <span data-ttu-id="8c984-152">El carrusel será el alto máximo de la tarjeta más grande.</span><span class="sxs-lookup"><span data-stu-id="8c984-152">The carousel will be the max height of your largest card.</span></span> <span data-ttu-id="8c984-153">Se recomienda usar el mismo tipo de tarjeta y los mismos campos de contenido en el mismo.</span><span class="sxs-lookup"><span data-stu-id="8c984-153">We recommend using the same card type and content fields throughout.</span></span>

### <a name="digest"></a><span data-ttu-id="8c984-154">Digest</span><span class="sxs-lookup"><span data-stu-id="8c984-154">Digest</span></span>

<span data-ttu-id="8c984-155">Se usa mejor para noticias, resúmenes y siempre que quiera que el usuario vea varias tarjetas a la vez.</span><span class="sxs-lookup"><span data-stu-id="8c984-155">Best used for news, digests, and whenever you want the user to view multiple cards at once.</span></span> <span data-ttu-id="8c984-156">Se recomienda usar tarjetas de miniaturas para los resúmenes.</span><span class="sxs-lookup"><span data-stu-id="8c984-156">We recommend using thumbnail cards for digests.</span></span>

[!include[Card anatomy](~/includes/design/card-image-digest.html)]

### <a name="lists"></a><span data-ttu-id="8c984-157">Listas</span><span class="sxs-lookup"><span data-stu-id="8c984-157">Lists</span></span>

<span data-ttu-id="8c984-158">Las listas son una buena forma de presentar un conjunto de objetos que se pueden analizar en un escenario "Elija uno de estos".</span><span class="sxs-lookup"><span data-stu-id="8c984-158">Lists are a great way to present a scannable set of objects in a “pick one of these” scenario.</span></span> <span data-ttu-id="8c984-159">Las listas se usan mejor para los elementos que no necesitan mucha explicación.</span><span class="sxs-lookup"><span data-stu-id="8c984-159">Lists are best used for items that don’t need a lot of explanation.</span></span>

[!include[Card anatomy](~/includes/design/card-image-list.html)]

### <a name="bubble-merge"></a><span data-ttu-id="8c984-160">Combinación de burbujas</span><span class="sxs-lookup"><span data-stu-id="8c984-160">Bubble merge</span></span>

<span data-ttu-id="8c984-161">Se pueden obtener efectos interesantes mediante el envío de un héroe y varias miniaturas en una sucesión rápida.</span><span class="sxs-lookup"><span data-stu-id="8c984-161">Some interesting effects can be achieved by sending one hero and several thumbnails in quick succession.</span></span> <span data-ttu-id="8c984-162">Recomendamos este enfoque cuando desee servir un resultado principal, pero incluya algunos elementos más relacionados.</span><span class="sxs-lookup"><span data-stu-id="8c984-162">We recommend this approach when you want to serve a main result but include a few more related items.</span></span>

[!include[Card anatomy](~/includes/design/card-image-bubble-merge.html)]

---

## <a name="best-practices"></a><span data-ttu-id="8c984-163">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="8c984-163">Best practices</span></span>

### <a name="keep-the-noise-down"></a><span data-ttu-id="8c984-164">Mantener el ruido hacia abajo</span><span class="sxs-lookup"><span data-stu-id="8c984-164">Keep the noise down</span></span>

<span data-ttu-id="8c984-165">Es fácil enviar varias tarjetas a una conversación, pero una vez que las tarjetas se desplazan fuera de la vista, se vuelven menos útiles.</span><span class="sxs-lookup"><span data-stu-id="8c984-165">It’s easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="8c984-166">Intente limitarse a los conceptos básicos.</span><span class="sxs-lookup"><span data-stu-id="8c984-166">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="8c984-167">Esto es especialmente cierto en un canal en el que los usuarios tienen menos tolerancia para lo que perciben como "ruido".</span><span class="sxs-lookup"><span data-stu-id="8c984-167">This is especially true in a channel where users have less tolerance for what they perceive as “noise”.</span></span>

### <a name="test-on-mobile"></a><span data-ttu-id="8c984-168">Probar en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="8c984-168">Test on mobile</span></span>

<span data-ttu-id="8c984-169">Los entornos móviles tienen limitaciones de espacio y ancho de banda, por lo que debe tener cuidado con la inclusión de imágenes de gran tamaño y conjuntos de datos de gran tamaño en listas y carruseles.</span><span class="sxs-lookup"><span data-stu-id="8c984-169">Mobile environments are space- and bandwidth-constrained, so be cautious about including oversized images and large data sets in lists and carousels.</span></span> <span data-ttu-id="8c984-170">Además, los anchos de los títulos y las longitudes del texto se truncarán en dispositivos móviles, por lo que es otro aspecto que debe tener en vista.</span><span class="sxs-lookup"><span data-stu-id="8c984-170">Also, title widths and text lengths will truncate on mobile, so that’s another thing to keep an eye on.</span></span>

### <a name="check-your-graphics"></a><span data-ttu-id="8c984-171">Comprobar los gráficos</span><span class="sxs-lookup"><span data-stu-id="8c984-171">Check your graphics</span></span>

<span data-ttu-id="8c984-172">Los gráficos van a escalarse, así que asegúrese de obtener una vista previa de ellos en todas las plataformas.</span><span class="sxs-lookup"><span data-stu-id="8c984-172">Graphics are going to scale, so be sure to preview them on all platforms.</span></span>

### <a name="avoid-including-text-in-a-graphic"></a><span data-ttu-id="8c984-173">Evitar incluir texto en un gráfico</span><span class="sxs-lookup"><span data-stu-id="8c984-173">Avoid including text in a graphic</span></span>

<span data-ttu-id="8c984-174">Todo lo que deba leer un usuario debe incluirse en un campo de texto.</span><span class="sxs-lookup"><span data-stu-id="8c984-174">Anything that needs to be read by a user should be included in a text field.</span></span> <span data-ttu-id="8c984-175">Una vez que se escala dinámicamente una imagen, cualquier texto que agregue a un gráfico puede volverse ininteligible.</span><span class="sxs-lookup"><span data-stu-id="8c984-175">Once an image is dynamically scaled, any text you add to a graphic may become unintelligible.</span></span>

### <a name="use-mentions-if-you-want-the-attention-of-specific-users"></a><span data-ttu-id="8c984-176">Use menciones si desea la atención de usuarios específicos</span><span class="sxs-lookup"><span data-stu-id="8c984-176">Use mentions if you want the attention of specific users</span></span>

> [!NOTE]
> <span data-ttu-id="8c984-177">Mencione que la compatibilidad en tarjetas solo se admite actualmente en [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="8c984-177">Mention support in cards is currently supported in [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="8c984-178">Las menciones son una excelente manera de notificar a usuarios específicos en un equipo o un chat en grupo.</span><span class="sxs-lookup"><span data-stu-id="8c984-178">Mentions are a great way to notify specific users in a Team or group chat.</span></span> <span data-ttu-id="8c984-179">Puede incluir una mención en tarjeta en escenarios como, una tarea que está asignada a un usuario o conceder prestigio a un compañero.</span><span class="sxs-lookup"><span data-stu-id="8c984-179">You can include a mention in card in scenarios like, a task thats assigned to a user or giving Kudos to a teammate.</span></span> <span data-ttu-id="8c984-180">Obtenga información sobre cómo incluir menciones en tarjetas en la [Página formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="8c984-180">Learn how to include mentions in cards in the [card formatting page](~/task-modules-and-cards/cards/cards-format.md).</span></span> 

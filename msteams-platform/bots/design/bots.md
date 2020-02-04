---
title: Directrices de diseño para bots
description: Describe las instrucciones para crear bots.
keywords: Directrices de diseño de Teams referencia de los bots del marco de trabajo hablando
ms.openlocfilehash: f59a1e9c280f27567692b4d10341db79d05c3464
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676126"
---
# <a name="start-talking-with-bots"></a><span data-ttu-id="85646-104">Empezar a hablar con bots</span><span class="sxs-lookup"><span data-stu-id="85646-104">Start talking with bots</span></span>

<span data-ttu-id="85646-105">Los bots son aplicaciones de conversación que realizan un conjunto de tareas estrecho o específico.</span><span class="sxs-lookup"><span data-stu-id="85646-105">Bots are conversational apps that perform a narrow or specific set of tasks.</span></span> <span data-ttu-id="85646-106">Le ofrecen la oportunidad de comunicarse con los usuarios, responder a sus preguntas y notificarles de forma proactiva sobre los cambios.</span><span class="sxs-lookup"><span data-stu-id="85646-106">They give you an opportunity to communicate with users, respond to their questions, and proactively notify them about changes.</span></span> <span data-ttu-id="85646-107">Son una buena forma de llegar.</span><span class="sxs-lookup"><span data-stu-id="85646-107">They’re a great way to reach out.</span></span>

---

## <a name="guidelines"></a><span data-ttu-id="85646-108">Instrucciones</span><span class="sxs-lookup"><span data-stu-id="85646-108">Guidelines</span></span>

### <a name="avatars"></a><span data-ttu-id="85646-109">Avatares</span><span class="sxs-lookup"><span data-stu-id="85646-109">Avatars</span></span>

<span data-ttu-id="85646-110">Los avatares de bot están formados como hexágonos para que los usuarios puedan saber rápidamente que están hablando con un bot en lugar de con una persona.</span><span class="sxs-lookup"><span data-stu-id="85646-110">Bot avatars in Teams are shaped like hexagons so people can quickly tell that they’re talking to a bot instead of a person.</span></span> <span data-ttu-id="85646-111">Enviará el Avatar como un cuadrado y lo recortaremos por usted.</span><span class="sxs-lookup"><span data-stu-id="85646-111">You’ll submit your avatar as a square and we’ll crop it for you.</span></span> <span data-ttu-id="85646-112">En lo que se refiere a los avatares, le recomendamos que el suyo pueda leerse a una distancia de 2 metros y con un contraste mayor.</span><span class="sxs-lookup"><span data-stu-id="85646-112">When it comes to avatars, we recommend making yours legible from 2 feet away and using a higher contrast.</span></span>

[!include[Avatar image](~/includes/design/bot-avatar-image.html)]

### <a name="buttons"></a><span data-ttu-id="85646-113">Botones</span><span class="sxs-lookup"><span data-stu-id="85646-113">Buttons</span></span>

<span data-ttu-id="85646-114">Admitimos hasta seis botones por tarjeta.</span><span class="sxs-lookup"><span data-stu-id="85646-114">We support up to six buttons per card.</span></span> <span data-ttu-id="85646-115">Sea conciso al escribir texto de botón y tenga en cuenta que la mayoría de los botones solo deben dirigirse a la tarea a mano.</span><span class="sxs-lookup"><span data-stu-id="85646-115">Be concise when writing button text, and keep in mind that most buttons should only address the task at hand.</span></span>

### <a name="graphics"></a><span data-ttu-id="85646-116">Gráficos</span><span class="sxs-lookup"><span data-stu-id="85646-116">Graphics</span></span>

<span data-ttu-id="85646-117">Los gráficos son una buena forma de decir un artículo, pero no todas las conversaciones de bot requieren gráficos, así que úselas para obtener el máximo impacto.</span><span class="sxs-lookup"><span data-stu-id="85646-117">Graphics are a good way to tell a story, but not all bot conversations require graphics, so use them for maximum impact.</span></span>

### <a name="responding-to-users-and-failing-gracefully"></a><span data-ttu-id="85646-118">Responder a los usuarios y conmutar por error</span><span class="sxs-lookup"><span data-stu-id="85646-118">Responding to users and failing gracefully</span></span>

<span data-ttu-id="85646-119">El bot también debe ser capaz de responder a cosas como "HI", "Help" y "gracias" mientras se toman errores y coloquialess comunes en la cuenta.</span><span class="sxs-lookup"><span data-stu-id="85646-119">Your bot should also be able to respond to things like 'Hi', 'Help', and 'Thanks' while taking common misspellings and colloquialisms into account.</span></span> <span data-ttu-id="85646-120">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="85646-120">For example:</span></span>

#### <a name="x2713-hello"></a><span data-ttu-id="85646-121">&#x2713; Hello</span><span class="sxs-lookup"><span data-stu-id="85646-121">&#x2713; Hello</span></span>

<span data-ttu-id="85646-122">`Hi` `how are you` `howdy`</span><span class="sxs-lookup"><span data-stu-id="85646-122">`Hi` `how are you` `howdy`</span></span>

#### <a name="x2713-help"></a><span data-ttu-id="85646-123">Ayuda de &#x2713;</span><span class="sxs-lookup"><span data-stu-id="85646-123">&#x2713; Help</span></span>

<span data-ttu-id="85646-124">`What do you do?` `How does this work?` `What the heck?`</span><span class="sxs-lookup"><span data-stu-id="85646-124">`What do you do?` `How does this work?` `What the heck?`</span></span>

#### <a name="x2713-thanks"></a><span data-ttu-id="85646-125">&#x2713; gracias</span><span class="sxs-lookup"><span data-stu-id="85646-125">&#x2713; Thanks</span></span>

<span data-ttu-id="85646-126">`Thank you` `thankyou` `thx`</span><span class="sxs-lookup"><span data-stu-id="85646-126">`Thank you` `thankyou` `thx`</span></span>

<span data-ttu-id="85646-127">El bot debe ser capaz de administrar los siguientes tipos de consultas y entradas:</span><span class="sxs-lookup"><span data-stu-id="85646-127">Your bot should be able to handle the following types of queries and inputs:</span></span>

* <span data-ttu-id="85646-128">**Preguntas reconocidas**: estas son las preguntas de "escenario de mejor caso" que debería anticipar de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="85646-128">**Recognized questions**: These are the “best case scenario” questions you’d anticipate from users.</span></span>
* <span data-ttu-id="85646-129">Personas **sin preguntas reconocidas**: consultas sobre funcionalidad no admitida, fragmentos aleatorios de información o cuándo alguien desea Curse en su bot.</span><span class="sxs-lookup"><span data-stu-id="85646-129">**Recognized non-questions**: Queries about unsupported functionality, random pieces of information, or when someone wants to curse at your bot.</span></span>
* <span data-ttu-id="85646-130">**Preguntas no reconocidas**: entradas ininteligibles (es decir, galimatías).</span><span class="sxs-lookup"><span data-stu-id="85646-130">**Unrecognized questions**: Unintelligible inputs (i.e., gibberish).</span></span>

<span data-ttu-id="85646-131">Ejemplos de tipos de personalidad y respuesta de bot:</span><span class="sxs-lookup"><span data-stu-id="85646-131">Examples of bot personality and response types:</span></span>

[!include[Bot responses](~/includes/design/bot-responses-table.html)]

> [!TIP]
> <span data-ttu-id="85646-132">Al escribir la secuencia de comandos de bot, pregúntese a sí mismo: "¿la compañía estará avergonzada si la respuesta es capturada y compartida?"</span><span class="sxs-lookup"><span data-stu-id="85646-132">When writing your bot script, ask yourself: “Will my company be embarrassed if a response is screen captured and shared?”</span></span>

### <a name="understanding-what-users-are-trying-to-say"></a><span data-ttu-id="85646-133">Descripción de lo que los usuarios intentan decir</span><span class="sxs-lookup"><span data-stu-id="85646-133">Understanding what users are trying to say</span></span>

#### <a name="use-a-thesaurus-for-synonyms"></a><span data-ttu-id="85646-134">Usar un diccionario de sinónimos para sinónimos</span><span class="sxs-lookup"><span data-stu-id="85646-134">Use a thesaurus for synonyms</span></span>

<span data-ttu-id="85646-135">Al recopilar una lluvia de ideas, use un diccionario de sinónimos y obtenga personas de tantos fondos diferentes como sea posible para ayudarle a generar diferentes interpretaciones de cada consulta.</span><span class="sxs-lookup"><span data-stu-id="85646-135">When brainstorming variants, use a thesaurus and get people from as many different backgrounds as possible to help you generate different interpretations of each query.</span></span>

#### <a name="make-use-of-telemetry-and-interviews"></a><span data-ttu-id="85646-136">Hacer uso de telemetría y entrevistas</span><span class="sxs-lookup"><span data-stu-id="85646-136">Make use of telemetry and interviews</span></span>

<span data-ttu-id="85646-137">Averigüe qué opinan los usuarios y cuál fue su intención al consultar a su bot.</span><span class="sxs-lookup"><span data-stu-id="85646-137">Find out what users are saying and what was their intent when querying your bot.</span></span> <span data-ttu-id="85646-138">Este será un proceso continuo a medida que se obtienen usuarios en distintas ubicaciones y tipos de compañías.</span><span class="sxs-lookup"><span data-stu-id="85646-138">This will be an ongoing process as you get users in different locations and types of companies.</span></span> <span data-ttu-id="85646-139">Puede ajustar el reconocimiento de idioma y la asignación de intenciones con idiomas que comprenden el servicio inteligente ([Luis](/azure/cognitive-services/luis/what-is-luis)).</span><span class="sxs-lookup"><span data-stu-id="85646-139">You can fine-tune language recognition and intent mapping with Language Understanding Intelligent Service ([LUIS](/azure/cognitive-services/luis/what-is-luis)).</span></span>

### <a name="how-often-should-you-use-your-bot-to-reach-out-to-a-user"></a><span data-ttu-id="85646-140">¿Con qué frecuencia debería usar el bot para ponerse en contacto con un usuario?</span><span class="sxs-lookup"><span data-stu-id="85646-140">How often should you use your bot to reach out to a user?</span></span>

#### <a name="x2713-when-a-state-has-changed"></a><span data-ttu-id="85646-141">&#x2713; cuando un Estado ha cambiado</span><span class="sxs-lookup"><span data-stu-id="85646-141">&#x2713; When a state has changed</span></span>

<span data-ttu-id="85646-142">Por ejemplo, si una asignación se marca como completada, cuando un error cambia, cuando hay nuevos medios sociales disponibles o cuando se ha completado un sondeo.</span><span class="sxs-lookup"><span data-stu-id="85646-142">For example, if an assignment is marked as complete, when a bug changes, when new social media is available, or when a poll has been completed.</span></span>

#### <a name="x2713-when-the-timing-is-right"></a><span data-ttu-id="85646-143">&#x2713; cuando el intervalo es el derecho</span><span class="sxs-lookup"><span data-stu-id="85646-143">&#x2713; When the timing is right</span></span>

<span data-ttu-id="85646-144">El bot puede actuar como un resumen diario y enviar una notificación al usuario o al canal en una frecuencia específica.</span><span class="sxs-lookup"><span data-stu-id="85646-144">Your bot can act like a daily digest, sending a notification to the user or channel at a specific frequency.</span></span>

<span data-ttu-id="85646-145">Deje el usuario en el control.</span><span class="sxs-lookup"><span data-stu-id="85646-145">Leave the user in control.</span></span> <span data-ttu-id="85646-146">Proporcionar la configuración de la notificación que incluya frecuencia y prioridad.</span><span class="sxs-lookup"><span data-stu-id="85646-146">Provide notification settings that include frequency and priority.</span></span>

[!include[Bot notification](~/includes/design/bot-notification-image.html)]

---

## <a name="using-tabs"></a><span data-ttu-id="85646-147">Uso de pestañas</span><span class="sxs-lookup"><span data-stu-id="85646-147">Using tabs</span></span>

<span data-ttu-id="85646-148">Las pestañas hacen que el bot sea mucho más funcional.</span><span class="sxs-lookup"><span data-stu-id="85646-148">Tabs make your bot much more functional.</span></span> <span data-ttu-id="85646-149">Con las pestañas, puede crear lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="85646-149">With tabs, you can create the following:</span></span>

### <a name="x2713-a-place-to-host-standing-queries"></a><span data-ttu-id="85646-150">&#x2713; un punto de hospedar consultas permanentes</span><span class="sxs-lookup"><span data-stu-id="85646-150">&#x2713; A place to host standing queries</span></span>

<span data-ttu-id="85646-151">En las conversaciones personales entre un bot y una sola persona, las pestañas pueden hospedar información y listas específicas del usuario.</span><span class="sxs-lookup"><span data-stu-id="85646-151">In personal conversations between a bot and a single person, tabs can house user-specific information and lists.</span></span> <span data-ttu-id="85646-152">También es un buen punto de partida para mantener las respuestas de robot en las preguntas más frecuentes (p + f), de modo que los usuarios no necesitan seguir preguntando.</span><span class="sxs-lookup"><span data-stu-id="85646-152">They’re also a good place to maintain bot responses to frequently-asked questions (FAQs) — so users don’t need to keep asking.</span></span>

### <a name="x2713-a-place-to-finish-a-conversation"></a><span data-ttu-id="85646-153">&#x2713; un punto para finalizar una conversación</span><span class="sxs-lookup"><span data-stu-id="85646-153">&#x2713; A place to finish a conversation</span></span>

<span data-ttu-id="85646-154">Puede crear un vínculo a una ficha desde una tarjeta.</span><span class="sxs-lookup"><span data-stu-id="85646-154">You can link to a tab from a card.</span></span> <span data-ttu-id="85646-155">Si el bot proporciona una respuesta que requiere algunos pasos más, puede vincular a una pestaña para completar la tarea o el flujo.</span><span class="sxs-lookup"><span data-stu-id="85646-155">If your bot provides an answer that requires a few more steps, it can link to a tab to complete the task or flow.</span></span>

### <a name="x2713-a-place-to-provide-some-help"></a><span data-ttu-id="85646-156">&#x2713; un espacio para proporcionar ayuda</span><span class="sxs-lookup"><span data-stu-id="85646-156">&#x2713; A place to provide some help</span></span>

<span data-ttu-id="85646-157">Agregue una pestaña que enseñe a los usuarios a comunicarse con su bot.</span><span class="sxs-lookup"><span data-stu-id="85646-157">Add a tab that educates users about how to communicate with your bot.</span></span> <span data-ttu-id="85646-158">Puede proporcionar algún contexto para lo que hace o las preguntas más frecuentes.</span><span class="sxs-lookup"><span data-stu-id="85646-158">You can provide some context for what it does or FAQs.</span></span>

![Proporciona ayuda](~/assets/images/framework/framework_bots_tbot-help.png)

> [!TIP]
> <span data-ttu-id="85646-160">La incorporación de partes de su sitio en una pestaña ayudará a alguien a mantener el contexto de una conversación mientras usa el servicio.</span><span class="sxs-lookup"><span data-stu-id="85646-160">Embedding parts of your site in a tab will help someone maintain the context of a conversation as they use your service.</span></span> <span data-ttu-id="85646-161">Elimina la necesidad de iniciar el servicio en un explorador y cambiar de una aplicación a otra.</span><span class="sxs-lookup"><span data-stu-id="85646-161">It removes the need to launch your service in a browser and switch back and forth between apps.</span></span>

---

## <a name="best-practices"></a><span data-ttu-id="85646-162">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="85646-162">Best practices</span></span>

### <a name="x2713-bots-arent-assistants"></a><span data-ttu-id="85646-163">Los bots de &#x2713; no son auxiliares</span><span class="sxs-lookup"><span data-stu-id="85646-163">&#x2713; Bots aren’t assistants</span></span>

<span data-ttu-id="85646-164">A diferencia de los agentes, por ejemplo, Cortana, los bots actúan como especialistas.</span><span class="sxs-lookup"><span data-stu-id="85646-164">Unlike agents, e.g., Cortana, bots act as specialists.</span></span>

### <a name="x2713-discourage-chitchat"></a><span data-ttu-id="85646-165">&#x2713; desaconsejar chitchat</span><span class="sxs-lookup"><span data-stu-id="85646-165">&#x2713; Discourage chitchat</span></span>

<span data-ttu-id="85646-166">A menos que el bot se haya creado para la conversación, busque formas de redirigir chitchat a la finalización de tareas.</span><span class="sxs-lookup"><span data-stu-id="85646-166">Unless your bot is built for conversation, find ways to redirect chitchat toward task completion.</span></span>

### <a name="x2713-introduce-some-personality"></a><span data-ttu-id="85646-167">&#x2713; introducen personalidad</span><span class="sxs-lookup"><span data-stu-id="85646-167">&#x2713; Introduce some personality</span></span>

<span data-ttu-id="85646-168">Mantenga la personalidad de la personalidad del bot con la voz del producto.</span><span class="sxs-lookup"><span data-stu-id="85646-168">Keep your bot personality consistent with the voice of your product.</span></span> <span data-ttu-id="85646-169">Piense en su robot como hablando de su empresa.</span><span class="sxs-lookup"><span data-stu-id="85646-169">Think of your bot as speaking for your company.</span></span>

### <a name="x2713-maintain-tone"></a><span data-ttu-id="85646-170">&#x2713; mantener tono</span><span class="sxs-lookup"><span data-stu-id="85646-170">&#x2713; Maintain tone</span></span>

<span data-ttu-id="85646-171">Determine si desea que el tono sea agradable y claro, "solo los hechos" o súper extraña.</span><span class="sxs-lookup"><span data-stu-id="85646-171">Determine whether you want your tone to be friendly and light, “just the facts”, or super quirky.</span></span>

### <a name="x2713-encourage-easy-task-flow"></a><span data-ttu-id="85646-172">&#x2713; animar el flujo de tareas sencillo</span><span class="sxs-lookup"><span data-stu-id="85646-172">&#x2713; Encourage easy task flow</span></span>

<span data-ttu-id="85646-173">Admite interacciones multiactivables, a la vez que permite preguntas completamente formadas.</span><span class="sxs-lookup"><span data-stu-id="85646-173">Support multi-turn interactions while still allowing for fully formed questions.</span></span> <span data-ttu-id="85646-174">La planeación del siguiente paso ayudará a los usuarios a pasar por los flujos de tareas de forma mucho más fácil.</span><span class="sxs-lookup"><span data-stu-id="85646-174">Anticipating the next step will help users get through task flows much easier.</span></span>

<span data-ttu-id="85646-175">Si un usuario realiza varios pasos para completar una tarea, permita que el bot los lleve a cabo a través de cada paso, pero el fin es que sugiera una ruta de acceso más rápida.</span><span class="sxs-lookup"><span data-stu-id="85646-175">If a user takes several steps to complete a task, allow your bot to take them through each step, but finish by having it suggest a quicker path.</span></span> <span data-ttu-id="85646-176">Por ejemplo, si un usuario ha tomado varias vueltas de conversación para establecer una reunión (especificando primero una reunión, e identifica con quién, a continuación, indicando la hora y, a continuación, indicando el día), finalice la conversación con la siguiente sugerencia: la próxima vez, intente preguntar si puede ' programar una reunión con Bob al 1:00 mañana '.</span><span class="sxs-lookup"><span data-stu-id="85646-176">For example, if a user has taken several conversational turns to set a meeting (by first specifying a meeting, then identifying with whom, then stating the time, then stating the day), finish the conversation with the following suggestion: Next time, try asking if you can ‘schedule a meeting with Bob at 1:00 tomorrow’.</span></span>
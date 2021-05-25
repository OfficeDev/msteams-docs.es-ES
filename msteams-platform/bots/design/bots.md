---
title: Cómo diseñar su bot
description: Obtenga información sobre cómo diseñar un bot para Teams y obtener el Kit de UI de Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 98e36bf55e61ef59261959021409d9e60d8542f5
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630121"
---
# <a name="designing-your-microsoft-teams-bot"></a><span data-ttu-id="01c2b-103">Diseño de un bot para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="01c2b-103">Designing your Microsoft Teams bot</span></span>

<span data-ttu-id="01c2b-104">Los bots son aplicaciones de conversación que realizan un conjunto específico de tareas.</span><span class="sxs-lookup"><span data-stu-id="01c2b-104">Bots are conversational apps that perform a specific set of tasks.</span></span> <span data-ttu-id="01c2b-105">Basándose en <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot Framework</a>, los bots se comunican con los usuarios, responden a sus preguntas y les notifican de forma proactiva sobre cambios y otros eventos.</span><span class="sxs-lookup"><span data-stu-id="01c2b-105">Based on the <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot Framework</a>, bots communicate with users, respond to their questions, and proactively notify them about changes and other events.</span></span> <span data-ttu-id="01c2b-106">Son una herramienta excelente de comunicación.</span><span class="sxs-lookup"><span data-stu-id="01c2b-106">They're a great way to reach out.</span></span>

<span data-ttu-id="01c2b-107">A modo de guía en el diseño de su aplicación, a continuación se describe e ilustra cómo pueden los usuarios agregar, usar y administrar bots en Teams.</span><span class="sxs-lookup"><span data-stu-id="01c2b-107">To guide your app design, the following information describes and illustrates how people can add, use, and manage bots in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="01c2b-108">Kit de UI de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="01c2b-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="01c2b-109">En el Kit de UI de Microsoft Teams encontrará instrucciones de diseño de bot más completas, que incluyen elementos que puede usar y modificar como quiera.</span><span class="sxs-lookup"><span data-stu-id="01c2b-109">You can find more comprehensive bot design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="01c2b-110">Obtener el Kit de UI de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="01c2b-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-bot"></a><span data-ttu-id="01c2b-111">Agregar un bot</span><span class="sxs-lookup"><span data-stu-id="01c2b-111">Add a bot</span></span>

<span data-ttu-id="01c2b-112">Los bots están disponibles para chats, canales y aplicaciones personales.</span><span class="sxs-lookup"><span data-stu-id="01c2b-112">Bots are available in chats, channels, and personal apps.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="01c2b-113">Escritorio</span><span class="sxs-lookup"><span data-stu-id="01c2b-113">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="01c2b-114">Los usuarios pueden agregar un bot de una de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="01c2b-114">Users can add a bot one of the following ways:</span></span>

* <span data-ttu-id="01c2b-115">Desde el Teams almacén.</span><span class="sxs-lookup"><span data-stu-id="01c2b-115">From the Teams store.</span></span>
* <span data-ttu-id="01c2b-116">En el menú desplegable de la aplicación, seleccione el icono **Más** en el lado izquierdo de Teams.</span><span class="sxs-lookup"><span data-stu-id="01c2b-116">Using the app flyout by selecting the **More** icon on the left side of Teams.</span></span>
* <span data-ttu-id="01c2b-117">Con una @mención en el nuevo cuadro de chat o redacción (en el siguiente ejemplo se muestra cómo puede hacerlo en un chat de grupo).</span><span class="sxs-lookup"><span data-stu-id="01c2b-117">With an @mention in the new chat or compose box (the following example shows how you can do this in a group chat).</span></span>

    :::image type="content" source="../../assets/images/bots/add-bot-chat-at-mention.png" alt-text="En el ejemplo se muestra cómo agregar un bot en un chat de grupo con una @mención." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="01c2b-119">Móvil</span><span class="sxs-lookup"><span data-stu-id="01c2b-119">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="01c2b-120">Los usuarios pueden obtener acceso a los bots que se agregaron en el escritorio con un @mention.</span><span class="sxs-lookup"><span data-stu-id="01c2b-120">Users can access bots that were added on desktop with an @mention.</span></span>

:::image type="content" source="../../assets/images/bots/mobile-access-bot-chat-at-mention.png" alt-text="En el ejemplo se muestra cómo obtener acceso a un bot móvil en un chat de grupo mediante un @mention." border="false":::

---

## <a name="introduce-a-bot"></a><span data-ttu-id="01c2b-122">La presentación del bot</span><span class="sxs-lookup"><span data-stu-id="01c2b-122">Introduce a bot</span></span>

<span data-ttu-id="01c2b-123">Es fundamental que el bot se presente y describa lo que puede hacer.</span><span class="sxs-lookup"><span data-stu-id="01c2b-123">It’s critical that your bot introduces itself and describes what it can do.</span></span> <span data-ttu-id="01c2b-124">Esta comunicación inicial ayuda a los usuarios a comprender qué pueden hacer con el bot, a conocer sus limitaciones y, lo que es más importante, a sentirse cómodos interactuando con él.</span><span class="sxs-lookup"><span data-stu-id="01c2b-124">This initial exchange helps people understand what to do with the bot, find out its limitations and, most importantly, get comfortable interacting with it.</span></span>

### <a name="welcome-message-in-a-one-on-one-chat"></a><span data-ttu-id="01c2b-125">Mensaje de bienvenida en un chat uno a uno</span><span class="sxs-lookup"><span data-stu-id="01c2b-125">Welcome message in a one-on-one chat</span></span>

<span data-ttu-id="01c2b-126">En contextos personales, los mensajes de bienvenida marcan el tono del bot.</span><span class="sxs-lookup"><span data-stu-id="01c2b-126">In personal contexts, welcome messages set your bot's tone.</span></span> <span data-ttu-id="01c2b-127">El mensaje incluye un saludo, lo que el bot puede hacer y algunas sugerencias sobre cómo interactuar.</span><span class="sxs-lookup"><span data-stu-id="01c2b-127">The message includes a greeting, what the bot can do, and some suggestions for how to interact.</span></span> <span data-ttu-id="01c2b-128">Por ejemplo, "Intente preguntarme sobre ...".</span><span class="sxs-lookup"><span data-stu-id="01c2b-128">For example, “Try asking me about …”.</span></span> <span data-ttu-id="01c2b-129">Cuando sea posible, estas sugerencias deben devolver respuestas almacenadas sin necesidad de iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="01c2b-129">If possible, these suggestions should return stored responses without having to sign in.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="01c2b-130">Escritorio</span><span class="sxs-lookup"><span data-stu-id="01c2b-130">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-personal-welcome.png" alt-text="El ejemplo muestra una introducción a un bot en una aplicación personal." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="01c2b-132">Móvil</span><span class="sxs-lookup"><span data-stu-id="01c2b-132">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-personal-welcome.png" alt-text="En el ejemplo se muestra una introducción de bot en una aplicación personal en el móvil." border="false":::

---

### <a name="welcome-message-in-channels-and-group-chats"></a><span data-ttu-id="01c2b-134">Mensaje de bienvenida en canales y chats de grupo</span><span class="sxs-lookup"><span data-stu-id="01c2b-134">Welcome message in channels and group chats</span></span>

<span data-ttu-id="01c2b-135">La introducción del bot debe ser ligeramente diferente en canales y chats de grupo en comparación con un espacio personal (como una aplicación personal).</span><span class="sxs-lookup"><span data-stu-id="01c2b-135">Your bot's introduction should be slightly different in channels and group chats compared to a personal space (like a personal app).</span></span> <span data-ttu-id="01c2b-136">En la vida real, si entra en una sala llena de gente, no dará la bienvenida a las personas que ya están allí sino que será usted quien se presente.</span><span class="sxs-lookup"><span data-stu-id="01c2b-136">In real life, if you entered a room full of people; you’d introduce yourself instead of welcoming everyone who’s already there.</span></span> <span data-ttu-id="01c2b-137">Lo mismo vale para el diseño de un bot.</span><span class="sxs-lookup"><span data-stu-id="01c2b-137">Carry that thinking into your bot design.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="01c2b-138">Escritorio</span><span class="sxs-lookup"><span data-stu-id="01c2b-138">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-group-welcome.png" alt-text="El ejemplo muestra una introducción a un bot en un contexto de colaboración." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="01c2b-140">Móvil</span><span class="sxs-lookup"><span data-stu-id="01c2b-140">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-group-welcome.png" alt-text="En el ejemplo se muestra una introducción de bot en un contexto de colaboración en dispositivos móviles." border="false":::

---

### <a name="bot-authentication-with-single-sign-on"></a><span data-ttu-id="01c2b-142">Autenticación de bot con inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="01c2b-142">Bot authentication with single sign-on</span></span>

<span data-ttu-id="01c2b-143">Cuando alguien envía un mensaje a un bot, es posible que deba iniciar sesión para acceder a todas sus características.</span><span class="sxs-lookup"><span data-stu-id="01c2b-143">When a person messages a bot, sign in may be required use all its features.</span></span> <span data-ttu-id="01c2b-144">El inicio de sesión único (SSO) puede simplificar el proceso de autenticación.</span><span class="sxs-lookup"><span data-stu-id="01c2b-144">You can simplify the authentication process using single sign-on (SSO).</span></span>

<span data-ttu-id="01c2b-145">No olvide que en el menú de comandos del bot (**¿Qué puedo hacer?**), también debe proporcionar un comando para cerrar sesión.</span><span class="sxs-lookup"><span data-stu-id="01c2b-145">Don’t forget: In the bot command menu (**What can I do?**), you must also provide a command to sign out.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="01c2b-146">Escritorio</span><span class="sxs-lookup"><span data-stu-id="01c2b-146">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-sso-example.png" alt-text="En el ejemplo se muestra un bot con un botón de inicio de sesión." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="01c2b-148">Móvil</span><span class="sxs-lookup"><span data-stu-id="01c2b-148">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-sso-example.png" alt-text="En el ejemplo se muestra un bot con un botón de inicio de sesión en el móvil." border="false":::

---

### <a name="tours"></a><span data-ttu-id="01c2b-150">Paseos</span><span class="sxs-lookup"><span data-stu-id="01c2b-150">Tours</span></span>

<span data-ttu-id="01c2b-151">Puede incluir un paseo con mensajes de bienvenida y para cuando el bot responda a un comando de "ayuda" o algo parecido.</span><span class="sxs-lookup"><span data-stu-id="01c2b-151">You can include a tour with welcome messages and if the bot responds to something like a “help” command.</span></span> <span data-ttu-id="01c2b-152">Un paseo es la forma más eficaz de describir lo que puede hacer su bot.</span><span class="sxs-lookup"><span data-stu-id="01c2b-152">A tour is the most effective way to describe what your bot can do.</span></span> <span data-ttu-id="01c2b-153">Si procede, también son excelentes para describir las otras características de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="01c2b-153">If applicable, they’re also great for describing your app’s other features.</span></span> <span data-ttu-id="01c2b-154">Por ejemplo, incluya capturas de pantalla de la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="01c2b-154">For example, include screenshots of your messaging extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="01c2b-155">Los viajes deben ser accesibles sin tener que iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="01c2b-155">Tours should be accessible without having to sign in.</span></span>

#### <a name="one-on-one-chats"></a><span data-ttu-id="01c2b-156">Chats uno a uno</span><span class="sxs-lookup"><span data-stu-id="01c2b-156">One-on-one chats</span></span>

<span data-ttu-id="01c2b-157">En una aplicación personal, un carrusel puede ofrecer información general eficaz sobre el bot y otras características de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="01c2b-157">In a personal app, a carousel can provide an effective overview of your bot and any other features of your app.</span></span> <span data-ttu-id="01c2b-158">Se recomienda incluir botones para permitir que los usuarios prueben comandos bot.</span><span class="sxs-lookup"><span data-stu-id="01c2b-158">Including buttons the let users try bot commands is encouraged.</span></span> <span data-ttu-id="01c2b-159">Por ejemplo, **Crear una tarea**.</span><span class="sxs-lookup"><span data-stu-id="01c2b-159">For example, **Create a task**.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="01c2b-160">Escritorio</span><span class="sxs-lookup"><span data-stu-id="01c2b-160">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-tour-personal.png" alt-text="El ejemplo muestra un paseo de bots en un chat uno a uno." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="01c2b-162">Móvil</span><span class="sxs-lookup"><span data-stu-id="01c2b-162">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-tour-personal.png" alt-text="En el ejemplo se muestra un recorrido por bots en un chat uno a uno en el móvil." border="false":::

---

#### <a name="channels-and-group-chats"></a><span data-ttu-id="01c2b-164">Canales y chats en grupo</span><span class="sxs-lookup"><span data-stu-id="01c2b-164">Channels and group chats</span></span>

<span data-ttu-id="01c2b-165">En canales y chats de grupo, los paseos deben abrirse en un modal (también denominado [módulo de tareas](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) para no interrumpir las conversaciones en curso).</span><span class="sxs-lookup"><span data-stu-id="01c2b-165">In channels and group chats, a tour should open in a modal (also known as a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) so it doesn’t interrupt ongoing conversations.</span></span> <span data-ttu-id="01c2b-166">Esto también le ofrece la opción de implementar vistas basadas en roles para su paseo.</span><span class="sxs-lookup"><span data-stu-id="01c2b-166">This also gives you the option to implement role-based views for your tour.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="01c2b-167">Escritorio</span><span class="sxs-lookup"><span data-stu-id="01c2b-167">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-tour-channel.png" alt-text="El ejemplo muestra un paseo de bots en un canal." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="01c2b-169">Móvil</span><span class="sxs-lookup"><span data-stu-id="01c2b-169">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-tour-channel.png" alt-text="En el ejemplo se muestra un recorrido por bots en un canal móvil." border="false":::

---

## <a name="chat-with-a-bot"></a><span data-ttu-id="01c2b-171">Chatear con un bot</span><span class="sxs-lookup"><span data-stu-id="01c2b-171">Chat with a bot</span></span>

<span data-ttu-id="01c2b-172">Los bots se integran directamente en el marco de mensajería de Team.</span><span class="sxs-lookup"><span data-stu-id="01c2b-172">Bots integrate directly into Team’s messaging framework.</span></span> <span data-ttu-id="01c2b-173">Los usuarios pueden chatear con un bot para obtener respuesta a sus preguntas o escribir comandos para que el bot realice un conjunto de tareas reducido o específico.</span><span class="sxs-lookup"><span data-stu-id="01c2b-173">Users can chat with a bot to get their questions answered or type commands to have the bot perform a narrow or specific set of tasks.</span></span> <span data-ttu-id="01c2b-174">Los bots pueden usar el chat para notificar a los usuarios frecuentemente de los cambios o actualizaciones que se realicen en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="01c2b-174">Bots can proactively notify users about changes or updates to your app via chat.</span></span>

### <a name="chat-with-a-bot-in-different-contexts"></a><span data-ttu-id="01c2b-175">Chatear con un bot en diferentes contextos</span><span class="sxs-lookup"><span data-stu-id="01c2b-175">Chat with a bot in different contexts</span></span>

<span data-ttu-id="01c2b-176">Puede usar bots en los siguientes contextos:</span><span class="sxs-lookup"><span data-stu-id="01c2b-176">You can use bots in the following contexts:</span></span>

* <span data-ttu-id="01c2b-177">**Aplicaciones personal**: en una aplicación personal, un bot tiene una pestaña de chat dedicada.</span><span class="sxs-lookup"><span data-stu-id="01c2b-177">**Personal apps**: In a personal app, a bot has a dedicated chat tab.</span></span>
* <span data-ttu-id="01c2b-178">**Chat uno a uno**: un usuario puede iniciar una conversación privada con un bot.</span><span class="sxs-lookup"><span data-stu-id="01c2b-178">**One-on-one chat**: A user can initiate a private conversation with a bot.</span></span> <span data-ttu-id="01c2b-179">Es la misma experiencia que usar un bot en una aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="01c2b-179">It's the same experience as using a bot in a personal app.</span></span>
* <span data-ttu-id="01c2b-180">**Chat de grupo**: los usuarios pueden interactuar con un bot en un chat de grupo si @mencionan el bot.</span><span class="sxs-lookup"><span data-stu-id="01c2b-180">**Group chat**: People can interact with a bot in a group chat by @mentioning the bot.</span></span>
* <span data-ttu-id="01c2b-181">**Canal**: los usuarios pueden interactuar con un bot en un canal.</span><span class="sxs-lookup"><span data-stu-id="01c2b-181">**Channel**: People can interact with a bot in a channel.</span></span> <span data-ttu-id="01c2b-182">Para ello, deben @mencionar el nombre del bot en el cuadro para redactar.</span><span class="sxs-lookup"><span data-stu-id="01c2b-182">by @mentioning the bot name in the compose box.</span></span> <span data-ttu-id="01c2b-183">Recuerde que, en este contexto, el bot está disponible para todo el equipo, no solo para el canal.</span><span class="sxs-lookup"><span data-stu-id="01c2b-183">Remember, in this context, the bot is available to the entire team, not just the channel.</span></span>

### <a name="anatomy"></a><span data-ttu-id="01c2b-184">Anatomía</span><span class="sxs-lookup"><span data-stu-id="01c2b-184">Anatomy</span></span>

# <a name="desktop"></a>[<span data-ttu-id="01c2b-185">Escritorio</span><span class="sxs-lookup"><span data-stu-id="01c2b-185">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-anatomy.png" alt-text="El ejemplo muestra el sistema estructural de un bot." border="false":::

|<span data-ttu-id="01c2b-187">Contador</span><span class="sxs-lookup"><span data-stu-id="01c2b-187">Counter</span></span>|<span data-ttu-id="01c2b-188">Descripción</span><span class="sxs-lookup"><span data-stu-id="01c2b-188">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="01c2b-189">1</span><span class="sxs-lookup"><span data-stu-id="01c2b-189">1</span></span>|<span data-ttu-id="01c2b-190">**Icono y nombre de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="01c2b-190">**App name and icon**</span></span>|
|<span data-ttu-id="01c2b-191">2</span><span class="sxs-lookup"><span data-stu-id="01c2b-191">2</span></span>|<span data-ttu-id="01c2b-192">**Pestaña de chat**: abre el espacio para hablar con el bot (aplicable solo a las aplicaciones personales).</span><span class="sxs-lookup"><span data-stu-id="01c2b-192">**Chat tab**: Opens the space to talk with your bot (applicable only to personal apps).</span></span>|
|<span data-ttu-id="01c2b-193">3</span><span class="sxs-lookup"><span data-stu-id="01c2b-193">3</span></span>|<span data-ttu-id="01c2b-194">**Pestañas personalizadas**: abren otro contenido relacionado con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="01c2b-194">**Custom tabs**: Opens other content related to your app.</span></span>|
|<span data-ttu-id="01c2b-195">4 </span><span class="sxs-lookup"><span data-stu-id="01c2b-195">4</span></span>|<span data-ttu-id="01c2b-196">**Pestañas Acerca de**: muestran información básica sobre la aplicación.</span><span class="sxs-lookup"><span data-stu-id="01c2b-196">**About tab**: Displays basic information about your app.</span></span>|
|<span data-ttu-id="01c2b-197">5 </span><span class="sxs-lookup"><span data-stu-id="01c2b-197">5</span></span>|<span data-ttu-id="01c2b-198">**Burbujas de chat**: las conversaciones de bot usan el marco de mensajería de Teams.</span><span class="sxs-lookup"><span data-stu-id="01c2b-198">**Chat bubble**: Bot conversations use the Teams messaging framework.</span></span>|
|<span data-ttu-id="01c2b-199">6 </span><span class="sxs-lookup"><span data-stu-id="01c2b-199">6</span></span>|<span data-ttu-id="01c2b-200">**Tarjeta adaptable:** si las respuestas del bot incluyen tarjetas adaptables, la tarjeta ocupa todo el ancho de la burbuja de chat.</span><span class="sxs-lookup"><span data-stu-id="01c2b-200">**Adaptive Card**: If your bot's responses include Adaptive Cards, the card takes up the full width of the chat bubble.</span></span>|
|<span data-ttu-id="01c2b-201">7 </span><span class="sxs-lookup"><span data-stu-id="01c2b-201">7</span></span>|<span data-ttu-id="01c2b-202">**Menú de comandos**: muestra los comandos estándar de su bot (definidos por usted).</span><span class="sxs-lookup"><span data-stu-id="01c2b-202">**Command menu**: Displays your bot's standard commands (defined by you).</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="01c2b-203">Móvil</span><span class="sxs-lookup"><span data-stu-id="01c2b-203">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de un bot móvil." border="false":::

|<span data-ttu-id="01c2b-205">Contador</span><span class="sxs-lookup"><span data-stu-id="01c2b-205">Counter</span></span>|<span data-ttu-id="01c2b-206">Descripción</span><span class="sxs-lookup"><span data-stu-id="01c2b-206">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="01c2b-207">1</span><span class="sxs-lookup"><span data-stu-id="01c2b-207">1</span></span>|<span data-ttu-id="01c2b-208">**Icono y nombre de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="01c2b-208">**App name and icon**</span></span>|
|<span data-ttu-id="01c2b-209">2</span><span class="sxs-lookup"><span data-stu-id="01c2b-209">2</span></span>|<span data-ttu-id="01c2b-210">**Pestaña de chat**: abre el espacio para hablar con el bot (aplicable solo a las aplicaciones personales).</span><span class="sxs-lookup"><span data-stu-id="01c2b-210">**Chat tab**: Opens the space to talk with your bot (applicable only to personal apps).</span></span>|
|<span data-ttu-id="01c2b-211">3</span><span class="sxs-lookup"><span data-stu-id="01c2b-211">3</span></span>|<span data-ttu-id="01c2b-212">**Pestañas personalizadas**: abren otro contenido relacionado con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="01c2b-212">**Custom tabs**: Opens other content related to your app.</span></span>|
|<span data-ttu-id="01c2b-213">4 </span><span class="sxs-lookup"><span data-stu-id="01c2b-213">4</span></span>|<span data-ttu-id="01c2b-214">**Burbujas de chat**: las conversaciones de bot usan el marco de mensajería de Teams.</span><span class="sxs-lookup"><span data-stu-id="01c2b-214">**Chat bubble**: Bot conversations use the Teams messaging framework.</span></span>|
|<span data-ttu-id="01c2b-215">5 </span><span class="sxs-lookup"><span data-stu-id="01c2b-215">5</span></span>|<span data-ttu-id="01c2b-216">**Tarjeta adaptable:** si las respuestas del bot incluyen tarjetas adaptables, la tarjeta ocupa todo el ancho de la burbuja de chat.</span><span class="sxs-lookup"><span data-stu-id="01c2b-216">**Adaptive Card**: If your bot's responses include Adaptive Cards, the card takes up the full width of the chat bubble.</span></span>|

---

### <a name="command-menu"></a><span data-ttu-id="01c2b-217">Menú de comandos</span><span class="sxs-lookup"><span data-stu-id="01c2b-217">Command menu</span></span>

<span data-ttu-id="01c2b-218">En el menú de comandos se proporciona una lista de palabras o frases que quiere que el bot siempre responda.</span><span class="sxs-lookup"><span data-stu-id="01c2b-218">The command menu provides a list of words or phrases you want your bot to always respond to.</span></span> <span data-ttu-id="01c2b-219">El menú de comandos se muestra encima del cuadro de redacción cuando alguien habla con un bot.</span><span class="sxs-lookup"><span data-stu-id="01c2b-219">The command menu displays above the compose box when someone is conversing with a bot.</span></span> <span data-ttu-id="01c2b-220">Cuando se selecciona un comando, este se inserta en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="01c2b-220">When a command is selected, it gets inserted into a message.</span></span>

<span data-ttu-id="01c2b-221">La lista de comandos debería ser breve.</span><span class="sxs-lookup"><span data-stu-id="01c2b-221">The list of commands should be brief.</span></span> <span data-ttu-id="01c2b-222">El menú solo está pensado para resaltar las características principales del bot.</span><span class="sxs-lookup"><span data-stu-id="01c2b-222">The menu is only meant to highlight your bot’s primary features.</span></span> <span data-ttu-id="01c2b-223">Además, los comandos deben ser concisos.</span><span class="sxs-lookup"><span data-stu-id="01c2b-223">Keep commands concise, too.</span></span> <span data-ttu-id="01c2b-224">Por ejemplo, cree un comando llamado **Ayuda** en lugar de **¿Puede ayudarme, por favor?**</span><span class="sxs-lookup"><span data-stu-id="01c2b-224">For example, create a command called **Help** instead of **Can you please help me**?</span></span>
<span data-ttu-id="01c2b-225">El menú de comandos siempre debe estar disponible independientemente del estado de la conversación.</span><span class="sxs-lookup"><span data-stu-id="01c2b-225">The command menu must always be available regardless of the state of the conversation.</span></span>

:::image type="content" source="../../assets/images/bots/bot-command-menu.png" alt-text="En el ejemplo se muestra el menú de comandos de un bot." border="false":::

## <a name="understand-what-people-are-saying"></a><span data-ttu-id="01c2b-227">Entender qué dice la gente</span><span class="sxs-lookup"><span data-stu-id="01c2b-227">Understand what people are saying</span></span>

<span data-ttu-id="01c2b-228">Use un diccionario de sinónimos y la ayuda de personas tan diversas como le sea posible encontrar para ayudarle a generar distintas formulaciones de consultas estándar.</span><span class="sxs-lookup"><span data-stu-id="01c2b-228">Use a thesaurus and get people from as many different backgrounds as possible to help you generate different interpretations of standard queries.</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-hello.png" alt-text="Ilustración que muestra cómo un bot puede interpretar &quot;Hola&quot;." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-help.png" alt-text="Ilustración que muestra cómo un bot puede interpretar &quot;Ayuda&quot;." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-thanks.png" alt-text="Ilustración que muestra cómo un bot puede interpretar &quot;Gracias&quot;." border="false":::
   :::column-end:::
:::row-end:::

### <a name="extract-intent-and-data-from-messages"></a><span data-ttu-id="01c2b-232">Extraer la intención y los datos de los mensajes</span><span class="sxs-lookup"><span data-stu-id="01c2b-232">Extract intent and data from messages</span></span>

<span data-ttu-id="01c2b-233">Diseñe el bot para reconocer la intención del usuario. La idea es capturar lo que alguien quiere de un bot como respuesta a un mensaje o una consulta.</span><span class="sxs-lookup"><span data-stu-id="01c2b-233">Design your bot to recognize intent, which captures what someone wants from a bot in response to a message or query.</span></span> <span data-ttu-id="01c2b-234">La intención clasifica un mensaje o consulta como una acción única con uno o varios objetos de datos afectados por la acción.</span><span class="sxs-lookup"><span data-stu-id="01c2b-234">Intent classifies a message or query as a single action with one or more data objects that are affected by the action.</span></span> 

<span data-ttu-id="01c2b-235">En los ejemplos siguientes se describen la intención del usuario y los datos de los mensajes enviados a bots:</span><span class="sxs-lookup"><span data-stu-id="01c2b-235">The following examples outline the user intent and data in messages sent to bots:</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-1.png" alt-text="Ejemplo que muestra la frase &quot;Reservar un vuelo a Seattle&quot;. La intención del usuario es &quot;reservar un vuelo&quot; y los datos son &quot;Seattle&quot;." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-2.png" alt-text="Ejemplo que muestra la frase &quot;Cuándo abre la tienda&quot;. La intención del usuario es &quot;cuándo&quot; y los datos son &quot;abrir&quot;." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-3.png" alt-text="Ejemplo con la frase &quot;Concertar una reunión a la 13:00 con Bob en el área de distribución&quot;. La intención del usuario es &quot;programar una reunión&quot; y los datos son &quot;13:00&quot; y &quot;Bob en el área de distribución&quot;." border="false":::
   :::column-end:::
:::row-end:::

### <a name="analyze-and-improve"></a><span data-ttu-id="01c2b-239">Analizar y mejorar</span><span class="sxs-lookup"><span data-stu-id="01c2b-239">Analyze and improve</span></span>

<span data-ttu-id="01c2b-240">Descubra qué dicen los usuarios al chatear con el bot.</span><span class="sxs-lookup"><span data-stu-id="01c2b-240">Learn what users say when chatting with your bot.</span></span> <span data-ttu-id="01c2b-241">Este será un proceso iterativo que evoluciona continuamente a medida que su base de usuarios crece en distintas ubicaciones y organizaciones.</span><span class="sxs-lookup"><span data-stu-id="01c2b-241">This will be an ongoing, iterative process as your user base grows in different locations and orgs.</span></span> <span data-ttu-id="01c2b-242">Puede ajustar la asignación de intenciones y el reconocimiento de idiomas del bot con Microsoft Language Understanding (LUIS).</span><span class="sxs-lookup"><span data-stu-id="01c2b-242">You can tune your bot's language recognition and intent mapping with Microsoft Language Understanding (LUIS).</span></span>

* <span data-ttu-id="01c2b-243">[Descripción de LUIS](/azure/cognitive-services/luis/artificial-intelligence): descubra cómo LUIS usa la IA para aplicar métodos de comprensión del lenguaje natural (NLU) con los datos de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="01c2b-243">[Understanding LUIS](/azure/cognitive-services/luis/artificial-intelligence): Find out how LUIS uses AI to provide natural language understanding (NLU) to your app data.</span></span>
* <span data-ttu-id="01c2b-244">[Integración con LUIS](https://www.luis.ai/): agregue capacidades de lenguaje natural al bot mientras evita el proceso complejo de crear modelos de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="01c2b-244">[Integrating with LUIS](https://www.luis.ai/): Add natural language capabilities to your bot without the complex process of creating machine learning models.</span></span>

## <a name="use-cases"></a><span data-ttu-id="01c2b-245">Casos de uso</span><span class="sxs-lookup"><span data-stu-id="01c2b-245">Use cases</span></span>

### <a name="simple-queries"></a><span data-ttu-id="01c2b-246">Consultas sencillas</span><span class="sxs-lookup"><span data-stu-id="01c2b-246">Simple queries</span></span>

<span data-ttu-id="01c2b-247">Cuando reciben una consulta, los bots pueden proporcionar una coincidencia exacta o un grupo de coincidencias relacionadas para ayudar con la desambiguación.</span><span class="sxs-lookup"><span data-stu-id="01c2b-247">Bots can deliver an exact match to a query or a group of related matches to help with disambiguation.</span></span> <span data-ttu-id="01c2b-248">En el caso de las coincidencias relacionadas, agrupe el contenido con una tarjeta de lista.</span><span class="sxs-lookup"><span data-stu-id="01c2b-248">For related matches, group the content using a list card.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="01c2b-249">Escritorio</span><span class="sxs-lookup"><span data-stu-id="01c2b-249">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-simple-query.png" alt-text="El ejemplo muestra una interacción de consulta simple con un bot." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="01c2b-251">Móvil</span><span class="sxs-lookup"><span data-stu-id="01c2b-251">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-simple-query.png" alt-text="En el ejemplo se muestra una interacción de consulta sencilla con un bot en el móvil." border="false":::

---

### <a name="multi-turn-interactions"></a><span data-ttu-id="01c2b-253">Interacciones de varios turnos</span><span class="sxs-lookup"><span data-stu-id="01c2b-253">Multi-turn interactions</span></span>

<span data-ttu-id="01c2b-254">Su bot no solo debe poder admitir solicitudes y preguntas completas, sino también lidiar con interacciones de varios turnos.</span><span class="sxs-lookup"><span data-stu-id="01c2b-254">While your bot can support complete requests and questions, it should also be able to handle multi-turn interactions.</span></span> <span data-ttu-id="01c2b-255">Anticipar los posibles pasos siguientes facilita mucho a los usuarios completar el flujo de tareas (les evita elaborar una solicitud exhaustiva).</span><span class="sxs-lookup"><span data-stu-id="01c2b-255">Anticipating possible next steps makes it much easier for people to a complete task flow (rather than expecting them to craft a comprehensive request).</span></span>

<span data-ttu-id="01c2b-256">En los ejemplos siguientes, el bot responde a cada mensaje con opciones para lo que podría querer hacer a continuación.</span><span class="sxs-lookup"><span data-stu-id="01c2b-256">In the following examples, the bot responds to each message with options for what might want to do next.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="01c2b-257">Escritorio</span><span class="sxs-lookup"><span data-stu-id="01c2b-257">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-multi-turn.png" alt-text="El ejemplo muestra una interacción multiturno con un bot." border="false":::


# <a name="mobile"></a>[<span data-ttu-id="01c2b-259">Móvil</span><span class="sxs-lookup"><span data-stu-id="01c2b-259">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-multi-turn.png" alt-text="En el ejemplo se muestra una interacción de varios turnos con un bot en el móvil." border="false":::


---

### <a name="reach-out-to-users"></a><span data-ttu-id="01c2b-261">Llegue a sus usuarios</span><span class="sxs-lookup"><span data-stu-id="01c2b-261">Reach out to users</span></span>

<span data-ttu-id="01c2b-262">Con la mensajería dinámica, el bot puede actuar como un boletín que envía notificaciones relevantes a un canal, chat de grupo o usuario con una frecuencia específica.</span><span class="sxs-lookup"><span data-stu-id="01c2b-262">With proactive messaging, your bot can act like a digest that sends notifications relevant to an individual, group chat, or channel at a specific frequency.</span></span> <span data-ttu-id="01c2b-263">Un bot puede enviar un mensaje cuando se ha hecho cambios en un documento o cuando se cierra un elemento de trabajo.</span><span class="sxs-lookup"><span data-stu-id="01c2b-263">A bot may send a message when something has changed in a document or a work item is closed.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="01c2b-264">Escritorio</span><span class="sxs-lookup"><span data-stu-id="01c2b-264">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="01c2b-265">En el ejemplo siguiente, el usuario recibe una notificación del sistema que indica que un bot les ha mensaje en otro canal.</span><span class="sxs-lookup"><span data-stu-id="01c2b-265">In the following example, the user gets a toast notification that a bot messaged them in another channel.</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message-toast.png" alt-text="En el ejemplo se muestra una notificación del sistema en la que un bot informa de forma dinámica a un usuario desde otro canal." border="false":::

<span data-ttu-id="01c2b-267">Ahora, en ese canal, el usuario puede leer su mensaje del bot.</span><span class="sxs-lookup"><span data-stu-id="01c2b-267">Now in that channel, the user can read their message from the bot.</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message.png" alt-text="El ejemplo muestra a un usuario que observa el mensaje dinámico del bot." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="01c2b-269">Móvil</span><span class="sxs-lookup"><span data-stu-id="01c2b-269">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="01c2b-270">En el siguiente ejemplo, el usuario recibe una notificación de que un bot les envía un mensaje en otro canal.</span><span class="sxs-lookup"><span data-stu-id="01c2b-270">In the following example, the user gets a notification that a bot messaged them in another channel.</span></span>

:::image type="content" source="../../assets/images/bots/mobile-bot-proactive-message-toast.png" alt-text="En el ejemplo se muestra una notificación del sistema de un bot que mensajería proactivamente a un usuario desde otro canal en el móvil." border="false":::

<span data-ttu-id="01c2b-272">Ahora, en ese canal, el usuario puede leer su mensaje del bot.</span><span class="sxs-lookup"><span data-stu-id="01c2b-272">Now in that channel, the user can read their message from the bot.</span></span>

:::image type="content" source="../../assets/images/bots/mobile-bot-proactive-message.png" alt-text="En el ejemplo se muestra al usuario mirando el mensaje proactivo del bot en el móvil." border="false":::

---

### <a name="use-tabs-with-bots"></a><span data-ttu-id="01c2b-274">Usar pestañas con bots</span><span class="sxs-lookup"><span data-stu-id="01c2b-274">Use tabs with bots</span></span>

<span data-ttu-id="01c2b-275">En las aplicaciones personales, una pestaña puede complementar lo que el bot puede hacer.</span><span class="sxs-lookup"><span data-stu-id="01c2b-275">In personal apps, a tab can complement what your bot can do.</span></span> <span data-ttu-id="01c2b-276">Por ejemplo, si el bot puede crear elementos de trabajo, sería útil mostrar todos esos elementos en una ubicación central dentro de una pestaña. Más información sobre las [pestañas de diseño](../../tabs/design/tabs.md).</span><span class="sxs-lookup"><span data-stu-id="01c2b-276">For example, if your bot can create work items, it would be nice to show all those items in a central location inside a tab. See more about [designing tabs](../../tabs/design/tabs.md).</span></span>

# <a name="desktop"></a>[<span data-ttu-id="01c2b-277">Escritorio</span><span class="sxs-lookup"><span data-stu-id="01c2b-277">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-with-tab.png" alt-text="El ejemplo muestra cómo una pestaña puede ayudar a organizar el contenido del bot." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="01c2b-279">Móvil</span><span class="sxs-lookup"><span data-stu-id="01c2b-279">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-with-tab.png" alt-text="En un ejemplo se muestra cómo una pestaña puede ayudar a organizar el contenido del bot en el móvil." border="false":::

---

## <a name="manage-a-bot"></a><span data-ttu-id="01c2b-281">Administrar un bot</span><span class="sxs-lookup"><span data-stu-id="01c2b-281">Manage a bot</span></span>

<span data-ttu-id="01c2b-282">Los usuarios deberían poder cambiar la configuración de un bot.</span><span class="sxs-lookup"><span data-stu-id="01c2b-282">Users should be able to change a bot's settings.</span></span> <span data-ttu-id="01c2b-283">Puede proporcionar esta funcionalidad con comandos de bot, pero normalmente es más eficaz incluir toda la configuración en un [módulo de tareas](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (como se muestra en el siguiente ejemplo).</span><span class="sxs-lookup"><span data-stu-id="01c2b-283">You can provide this functionality with bot commands, but it's usually more efficient to include all settings in a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (as shown in the following example).</span></span>

:::image type="content" source="../../assets/images/bots/manage-bot-task-module.png" alt-text="Un ejemplo muestra un módulo de tareas para configurar las opciones de un bot." border="false":::

## <a name="best-practices"></a><span data-ttu-id="01c2b-285">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="01c2b-285">Best practices</span></span>

<span data-ttu-id="01c2b-286">Usa estas recomendaciones para crear una experiencia de aplicación de calidad.</span><span class="sxs-lookup"><span data-stu-id="01c2b-286">Use these recommendations to create a quality app experience.</span></span>

### <a name="content"></a><span data-ttu-id="01c2b-287">Content</span><span class="sxs-lookup"><span data-stu-id="01c2b-287">Content</span></span>

:::image type="content" source="../../assets/images/bots/bot-content-persona-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot para establecer una persona clara." border="false":::

#### <a name="do-establish-a-clear-persona"></a><span data-ttu-id="01c2b-289">Práctica recomendada: cree un rol coherente para el bot</span><span class="sxs-lookup"><span data-stu-id="01c2b-289">Do: Establish a clear persona</span></span>

<span data-ttu-id="01c2b-290">¿Quiere que el tono del bot sea descriptivo y claro (que simplemente dé información) o que sea más simpático?</span><span class="sxs-lookup"><span data-stu-id="01c2b-290">Is your bot's tone friendly and light, “just the facts”, or super quirky?</span></span> <span data-ttu-id="01c2b-291">¿Cómo debe responder en distintos escenarios?</span><span class="sxs-lookup"><span data-stu-id="01c2b-291">How should it respond in different scenarios?</span></span> <span data-ttu-id="01c2b-292">Planear y documentar el rol del bot facilita la escritura de respuestas que parezcan naturales y cohesivas.</span><span class="sxs-lookup"><span data-stu-id="01c2b-292">Planning and documenting your bot's persona makes it easier to write responses that seem natural and cohesive.</span></span>

<span data-ttu-id="01c2b-293">Encontrará más información sobre cómo escribir para los bots en el <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Kit de UI de Microsoft Teams (Figma).</a></span><span class="sxs-lookup"><span data-stu-id="01c2b-293">See more about writing for bots in the <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft Teams UI Kit (Figma).</a></span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-do.png" alt-text="Ejemplo que muestra para transmitir claramente lo que el bot puede hacer." border="false":::

#### <a name="do-clearly-convey-what-your-bot-can-do"></a><span data-ttu-id="01c2b-295">Práctica recomendada: transmita claramente qué puede hacer el bot</span><span class="sxs-lookup"><span data-stu-id="01c2b-295">Do: Clearly convey what your bot can do</span></span>

<span data-ttu-id="01c2b-296">Los mensajes de bienvenida y los paseos ayudan a los usuarios a comprender qué pueden hacer con el bot.</span><span class="sxs-lookup"><span data-stu-id="01c2b-296">Welcome messages and tours help people understand what they can do with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-dont.png" alt-text="Ejemplo que muestra que no oscurece las características del bot." border="false":::

#### <a name="dont-obscure-your-bots-features"></a><span data-ttu-id="01c2b-298">Práctica a evitar: ocultar las características del bot</span><span class="sxs-lookup"><span data-stu-id="01c2b-298">Don't: Obscure your bot's features</span></span>

<span data-ttu-id="01c2b-299">Las primeras impresiones son importantes.</span><span class="sxs-lookup"><span data-stu-id="01c2b-299">First impressions matter.</span></span> <span data-ttu-id="01c2b-300">Es probable que los usuarios se confundan o sientan sospechas cuando vean un mensaje de inicio de sesión indefinido.</span><span class="sxs-lookup"><span data-stu-id="01c2b-300">People will likely be confused or suspicious when presented with a nondescript sign-in message.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-do.png" alt-text="El ejemplo que muestra el bot debe reconocer que no hay preguntas." border="false":::

#### <a name="do-recognize-non-questions"></a><span data-ttu-id="01c2b-302">Práctica recomendada: que el bot reconozca mensajes que no son preguntas</span><span class="sxs-lookup"><span data-stu-id="01c2b-302">Do: Recognize non-questions</span></span>

<span data-ttu-id="01c2b-303">El bot debería poder responder a mensajes como "Hola", "Ayuda" y "Gracias", así como sus variaciones coloquiales y las versiones con faltas de ortografía.</span><span class="sxs-lookup"><span data-stu-id="01c2b-303">Your bot should be able to respond to messages like "Hi", "Help", and "Thanks" while also accounting for common misspellings and colloquialisms.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-dont.png" alt-text="Ejemplo que muestra que debe evitar respuestas torpes a mensajes de bot simples." border="false":::

#### <a name="dont-miss-out-on-opportunities-to-delight"></a><span data-ttu-id="01c2b-305">Práctica a evitar: perder oportunidades para una charla agradable</span><span class="sxs-lookup"><span data-stu-id="01c2b-305">Don't: Miss out on opportunities to delight</span></span>

<span data-ttu-id="01c2b-306">Algunas personas esperan que las conversaciones fluyan de forma natural como lo harían con una persona.</span><span class="sxs-lookup"><span data-stu-id="01c2b-306">Some people expect conversations to flow naturally like they would with a real person.</span></span> <span data-ttu-id="01c2b-307">Intente evitar respuestas torpes a mensajes sencillos.</span><span class="sxs-lookup"><span data-stu-id="01c2b-307">Try to avoid clumsy responses to simple messages.</span></span>

   :::column-end:::
:::row-end:::

### <a name="troubleshooting"></a><span data-ttu-id="01c2b-308">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="01c2b-308">Troubleshooting</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-do.png" alt-text="Ejemplo que muestra bots debe ayudar a los usuarios a comprender cómo usar bots." border="false":::

#### <a name="do-provide-help"></a><span data-ttu-id="01c2b-310">Práctica recomendada: proporcione ayuda</span><span class="sxs-lookup"><span data-stu-id="01c2b-310">Do: Provide help</span></span>

<span data-ttu-id="01c2b-311">Si el bot no puede satisfacer una solicitud, dé al usuario una manera de aprender por sí mismo a interactuar con el bot.</span><span class="sxs-lookup"><span data-stu-id="01c2b-311">If your bot can’t satisfy a request, provide ways for a user to educate themselves about interacting with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-dont.png" alt-text="Ejemplo que muestra que el bot no debe varár a los usuarios." border="false":::

#### <a name="dont-leave-users-stranded"></a><span data-ttu-id="01c2b-313">Práctica a evitar: dejar a los usuarios sin ayuda</span><span class="sxs-lookup"><span data-stu-id="01c2b-313">Don't: Leave users stranded</span></span>

<span data-ttu-id="01c2b-314">Los usuarios abandonarán rápidamente el bot si no pueden solucionar problemas con él.</span><span class="sxs-lookup"><span data-stu-id="01c2b-314">People will quickly abandon your bot if they can’t troubleshoot issues.</span></span>

   :::column-end:::
:::row-end:::

### <a name="complex-interactions"></a><span data-ttu-id="01c2b-315">Interacciones complejas</span><span class="sxs-lookup"><span data-stu-id="01c2b-315">Complex interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-do.png" alt-text="Ejemplo que muestra que puede usar módulos de tareas o pestañas con el bot para interacciones complejas." border="false":::

#### <a name="do-use-task-modules-or-tabs"></a><span data-ttu-id="01c2b-317">Práctica recomendada: use pestañas o módulos de tareas</span><span class="sxs-lookup"><span data-stu-id="01c2b-317">Do: Use task modules or tabs</span></span>

<span data-ttu-id="01c2b-318">Si su bot proporciona una respuesta que requiere pasos adicionales, puede vincular a un módulo de tareas o a una pestaña para completar la tarea o el flujo.</span><span class="sxs-lookup"><span data-stu-id="01c2b-318">If your bot provides an answer that requires a few more steps, you can link to a task module or tab to complete the task or flow.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-dont.png" alt-text="Ejemplo que muestra cómo el bot debe evitar interacciones en varios turnos." border="false":::

#### <a name="dont-make-multi-turn-interactions-tedious"></a><span data-ttu-id="01c2b-320">Práctica a evitar: hacer interacciones multiuso tediosas</span><span class="sxs-lookup"><span data-stu-id="01c2b-320">Don't: Make multi-turn interactions tedious</span></span>

<span data-ttu-id="01c2b-321">Una conversación extensa para completar una tarea simple ralentiza y complica el proceso.</span><span class="sxs-lookup"><span data-stu-id="01c2b-321">An extensive conversation to complete a single task is slow and overly complex.</span></span> <span data-ttu-id="01c2b-322">También obliga al desarrollador a tener en cuenta cambios de estado (por ejemplo, tiempos de espera para la conversación o el envío de un mensaje de cancelación).</span><span class="sxs-lookup"><span data-stu-id="01c2b-322">It also requires the developer to account for state changes (such as the conversation timing out or you sending a “Cancel” message).</span></span>

   :::column-end:::
:::row-end:::

### <a name="privacy"></a><span data-ttu-id="01c2b-323">Privacidad</span><span class="sxs-lookup"><span data-stu-id="01c2b-323">Privacy</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-do.png" alt-text="Ejemplo que muestra cómo los bots solo deben mostrar información privada en un contexto personal." border="false":::

#### <a name="do-only-show-sensitive-info-in-a-personal-context"></a><span data-ttu-id="01c2b-325">Práctica recomendada: muestre información confidencial solo en un contexto personal</span><span class="sxs-lookup"><span data-stu-id="01c2b-325">Do: Only show sensitive info in a personal context</span></span>

<span data-ttu-id="01c2b-326">Si el bot está en un chat o canal de grupo, le recomendamos que dirija a los usuarios a una ubicación privada (por ejemplo, un módulo de tareas, una pestaña o un explorador) para ver la información confidencial.</span><span class="sxs-lookup"><span data-stu-id="01c2b-326">If your bot is in a group chat or channel, we recommend directing users to a private location (such as a task module, tab, or browser) to view sensitive information.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-dont.png" alt-text="Ejemplo que muestra cómo los bots no deben revelar información confidencial a un grupo o personas." border="false":::

#### <a name="dont-some-content-isnt-meant-to-be-seen-by-everyone"></a><span data-ttu-id="01c2b-328">Práctica a evitar: presentar a todo el mundo contenido confidencial</span><span class="sxs-lookup"><span data-stu-id="01c2b-328">Don't: Some content isn’t meant to be seen by everyone</span></span>

<span data-ttu-id="01c2b-329">El bot no debería revelar información confidencial a un grupo de personas.</span><span class="sxs-lookup"><span data-stu-id="01c2b-329">Your bot shouldn’t reveal sensitive information to a group of people.</span></span>

   :::column-end:::
:::row-end:::

## <a name="see-also"></a><span data-ttu-id="01c2b-330">Vea también</span><span class="sxs-lookup"><span data-stu-id="01c2b-330">See also</span></span>

<span data-ttu-id="01c2b-331">A continuación, tiene guías adicionales que le pueden ayudar con el diseño del bot:</span><span class="sxs-lookup"><span data-stu-id="01c2b-331">These other guidelines may help with your bot design:</span></span>

* [<span data-ttu-id="01c2b-332">Diseño de su aplicación personal</span><span class="sxs-lookup"><span data-stu-id="01c2b-332">Designing your personal app</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="01c2b-333">Diseño de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="01c2b-333">Designing Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)
* [<span data-ttu-id="01c2b-334">Diseño de módulos de tareas</span><span class="sxs-lookup"><span data-stu-id="01c2b-334">Designing task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)

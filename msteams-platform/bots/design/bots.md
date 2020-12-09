---
title: Diseño de un bot
description: Obtenga información sobre cómo diseñar un bot de Teams y obtener el kit de interfaz de usuario de Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: d1a7470f4986de22ecca7071823b620cb0234abb
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605496"
---
# <a name="designing-your-microsoft-teams-bot"></a><span data-ttu-id="292c2-103">Diseño de un bot de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="292c2-103">Designing your Microsoft Teams bot</span></span>

<span data-ttu-id="292c2-104">Los bots son aplicaciones de conversación que realizan un conjunto específico de tareas.</span><span class="sxs-lookup"><span data-stu-id="292c2-104">Bots are conversational apps that perform a specific set of tasks.</span></span> <span data-ttu-id="292c2-105">Basado en <a href="https://dev.botframework.com/" target="_blank">Microsoft bot Framework</a>, los bots se comunican con los usuarios, responden a sus preguntas y les notifican de forma proactiva sobre los cambios y otros eventos.</span><span class="sxs-lookup"><span data-stu-id="292c2-105">Based on the <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot Framework</a>, bots communicate with users, respond to their questions, and proactively notify them about changes and other events.</span></span> <span data-ttu-id="292c2-106">Son una buena forma de llegar.</span><span class="sxs-lookup"><span data-stu-id="292c2-106">They're a great way to reach out.</span></span>

<span data-ttu-id="292c2-107">Para guiar el diseño de la aplicación, la siguiente información describe e ilustra cómo los usuarios pueden agregar, usar y administrar bots en Teams.</span><span class="sxs-lookup"><span data-stu-id="292c2-107">To guide your app design, the following information describes and illustrates how people can add, use, and manage bots in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="292c2-108">Kit de IU de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="292c2-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="292c2-109">Puede encontrar pautas de diseño de bot más completas, incluidos los elementos que puede captar y modificar según sea necesario, en el kit de interfaz de usuario de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="292c2-109">You can find more comprehensive bot design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="292c2-110">Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="292c2-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-bot"></a><span data-ttu-id="292c2-111">Agregar un bot</span><span class="sxs-lookup"><span data-stu-id="292c2-111">Add a bot</span></span>

<span data-ttu-id="292c2-112">Los bots están disponibles en chats, canales y aplicaciones personales.</span><span class="sxs-lookup"><span data-stu-id="292c2-112">Bots are available in chats, channels, and personal apps.</span></span> <span data-ttu-id="292c2-113">Puede Agregar un bot de una de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="292c2-113">You can add a bot one of the following ways:</span></span>

* <span data-ttu-id="292c2-114">De la tienda Teams (AppSource).</span><span class="sxs-lookup"><span data-stu-id="292c2-114">From the Teams store (AppSource).</span></span>
* <span data-ttu-id="292c2-115">Mediante el control flotante de la aplicación seleccionando el icono **más** en el lado izquierdo de Teams.</span><span class="sxs-lookup"><span data-stu-id="292c2-115">Using the app flyout by selecting the **More** icon on the left side of Teams.</span></span>
* <span data-ttu-id="292c2-116">Con una @mention en el cuadro nuevo chat o redacción (en el ejemplo siguiente, se muestra cómo puede hacerlo en un chat en grupo).</span><span class="sxs-lookup"><span data-stu-id="292c2-116">With an @mention in the new chat or compose box (the following example shows how you can do this in a group chat).</span></span>

:::image type="content" source="../../assets/images/bots/add-bot-chat-at-mention.png" alt-text="En el ejemplo se muestra cómo agregar un bot en un chat de grupo mediante un @mention." border="false":::

## <a name="introduce-a-bot"></a><span data-ttu-id="292c2-118">Presentar un bot</span><span class="sxs-lookup"><span data-stu-id="292c2-118">Introduce a bot</span></span>

<span data-ttu-id="292c2-119">Es fundamental que el bot se presente a sí mismo y describa lo que puede hacer.</span><span class="sxs-lookup"><span data-stu-id="292c2-119">It’s critical that your bot introduces itself and describes what it can do.</span></span> <span data-ttu-id="292c2-120">Este intercambio inicial ayuda a los usuarios a comprender qué hacer con el bot, descubrir sus limitaciones y, lo que es más importante, familiarizarse con la interacción con él.</span><span class="sxs-lookup"><span data-stu-id="292c2-120">This initial exchange helps people understand what to do with the bot, find out its limitations and, most importantly, get comfortable interacting with it.</span></span>

### <a name="welcome-message-in-a-one-on-one-chat"></a><span data-ttu-id="292c2-121">Mensaje de bienvenida en un chat de uno a uno</span><span class="sxs-lookup"><span data-stu-id="292c2-121">Welcome message in a one-on-one chat</span></span>

<span data-ttu-id="292c2-122">En los contextos personales, los mensajes de bienvenida establecen el tono de la bot.</span><span class="sxs-lookup"><span data-stu-id="292c2-122">In personal contexts, welcome messages set your bot's tone.</span></span> <span data-ttu-id="292c2-123">El mensaje incluye un saludo, lo que el bot puede hacer y algunas sugerencias para interactuar (por ejemplo, "preguntarme sobre...").</span><span class="sxs-lookup"><span data-stu-id="292c2-123">The message includes a greeting, what the bot can do, and some suggestions for how to interact (for example, “Try asking me about …”).</span></span> <span data-ttu-id="292c2-124">Si es posible, estas sugerencias deben devolver respuestas almacenadas sin tener que iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="292c2-124">If possible, these suggestions should return stored responses without having to sign in.</span></span>

:::image type="content" source="../../assets/images/bots/bot-personal-welcome.png" alt-text="Ejemplo muestra una introducción a un bot en una aplicación personal." border="false":::

### <a name="introductions-in-group-chats-and-channels"></a><span data-ttu-id="292c2-126">Introducciones en chats y canales de grupo</span><span class="sxs-lookup"><span data-stu-id="292c2-126">Introductions in group chats and channels</span></span>

<span data-ttu-id="292c2-127">La introducción de la utilidad debe ser ligeramente diferente en los chats de grupo y en los canales, en comparación con un contexto personal (como una aplicación personal).</span><span class="sxs-lookup"><span data-stu-id="292c2-127">Your bot's introduction should be slightly little different in group chats and channels compared to a personal context (like a personal app).</span></span> <span data-ttu-id="292c2-128">En la vida real, si ha entrado en un salón lleno de personas; se introdujo en lugar de la bienvenida a todos los usuarios que ya están allí.</span><span class="sxs-lookup"><span data-stu-id="292c2-128">In real life, if you entered a room full of people; you’d introduce yourself instead of welcoming everyone who’s already there.</span></span> <span data-ttu-id="292c2-129">Lleve a cabo este pensamiento en el diseño de bot.</span><span class="sxs-lookup"><span data-stu-id="292c2-129">Carry that thinking into your bot design.</span></span>

:::image type="content" source="../../assets/images/bots/bot-group-welcome.png" alt-text="Ejemplo muestra una introducción de bot en un contexto de colaboración." border="false":::

### <a name="bot-authentication-with-single-sign-on"></a><span data-ttu-id="292c2-131">Autenticación de bot con inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="292c2-131">Bot authentication with single sign-on</span></span>

<span data-ttu-id="292c2-132">Cuando una persona mensaje un bot, puede que sea necesario iniciar sesión use todas sus características.</span><span class="sxs-lookup"><span data-stu-id="292c2-132">When a person messages a bot, sign in may be required use all its features.</span></span> <span data-ttu-id="292c2-133">Puede simplificar el proceso de autenticación con el inicio de sesión único (SSO).</span><span class="sxs-lookup"><span data-stu-id="292c2-133">You can simplify the authentication process using single sign-on (SSO).</span></span>

<span data-ttu-id="292c2-134">No se olvide: en el menú de comandos de Bot (**¿Qué puedo hacer?**), también debe proporcionar un comando para cerrar la sesión.</span><span class="sxs-lookup"><span data-stu-id="292c2-134">Don’t forget: In the bot command menu (**What can I do?**), you must also provide a command to sign out.</span></span>

:::image type="content" source="../../assets/images/bots/bot-sso-example.png" alt-text="Ejemplo muestra un bot con un botón de inicio de sesión." border="false":::

### <a name="tours"></a><span data-ttu-id="292c2-136">Viajes</span><span class="sxs-lookup"><span data-stu-id="292c2-136">Tours</span></span>

<span data-ttu-id="292c2-137">Puede incluir un paseo con mensajes de bienvenida y si el bot responde a algo como un comando "ayuda".</span><span class="sxs-lookup"><span data-stu-id="292c2-137">You can include a tour with welcome messages and if the bot responds to something like a “help” command.</span></span> <span data-ttu-id="292c2-138">Un paseo es la forma más eficaz de describir lo que puede hacer el bot.</span><span class="sxs-lookup"><span data-stu-id="292c2-138">A tour is the most effective way to describe what your bot can do.</span></span> <span data-ttu-id="292c2-139">Si es aplicable, también son excelentes para describir otras características de la aplicación (por ejemplo, incluir capturas de pantallas de la extensión de mensajería).</span><span class="sxs-lookup"><span data-stu-id="292c2-139">If applicable, they’re also great for describing your app’s other features (for example, include screenshots of your messaging extension).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="292c2-140">Los paseos deben ser accesibles sin tener que iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="292c2-140">Tours should be accessible without having to sign in.</span></span>

#### <a name="one-on-one-chats"></a><span data-ttu-id="292c2-141">Chats uno a uno</span><span class="sxs-lookup"><span data-stu-id="292c2-141">One-on-one chats</span></span>

<span data-ttu-id="292c2-142">En una aplicación personal, un carrusel puede proporcionar una introducción eficaz a su bot y otras características de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="292c2-142">In a personal app, a carousel can provide an effective overview of your bot and any other features of your app.</span></span> <span data-ttu-id="292c2-143">Incluir botones el procedimiento para que los usuarios prueben comandos de Bot (por ejemplo, **crear una tarea**).</span><span class="sxs-lookup"><span data-stu-id="292c2-143">Including buttons the let users try bot commands is encouraged (for example, **Create a task**).</span></span>

:::image type="content" source="../../assets/images/bots/bot-tour-personal.png" alt-text="Ejemplo muestra un paseo de bot en un chat de uno a uno." border="false":::

#### <a name="channels-and-group-chats"></a><span data-ttu-id="292c2-145">Canales y chats de grupo</span><span class="sxs-lookup"><span data-stu-id="292c2-145">Channels and group chats</span></span>

<span data-ttu-id="292c2-146">En los canales y los chats de grupos, un tour debe abrirse en un modal (también conocido como [módulo de tareas](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) , por lo que no interrumpe las conversaciones en curso).</span><span class="sxs-lookup"><span data-stu-id="292c2-146">In channels and group chats, a tour should open in a modal (also known as a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) so it doesn’t interrupt ongoing conversations.</span></span> <span data-ttu-id="292c2-147">Esto también le ofrece la opción de implementar vistas basadas en roles para su tour.</span><span class="sxs-lookup"><span data-stu-id="292c2-147">This also gives you the option to implement role-based views for your tour.</span></span>

:::image type="content" source="../../assets/images/bots/bot-tour-channel.png" alt-text="Ejemplo muestra un paseo de bot en un canal." border="false":::

## <a name="chat-with-a-bot"></a><span data-ttu-id="292c2-149">Chatear con un bot</span><span class="sxs-lookup"><span data-stu-id="292c2-149">Chat with a bot</span></span>

<span data-ttu-id="292c2-150">Los bots se integran directamente en el marco de mensajería del equipo.</span><span class="sxs-lookup"><span data-stu-id="292c2-150">Bots integrate directly into Team’s messaging framework.</span></span> <span data-ttu-id="292c2-151">Los usuarios pueden chatear con un bot para obtener respuestas a sus preguntas o escribir comandos para hacer que el bot realice un conjunto de tareas limitado o específico.</span><span class="sxs-lookup"><span data-stu-id="292c2-151">Users can chat with a bot to get their questions answered or type commands to have the bot perform a narrow or specific set of tasks.</span></span> <span data-ttu-id="292c2-152">Los bots pueden notificar de forma proactiva a los usuarios sobre cambios o actualizaciones de la aplicación mediante chat.</span><span class="sxs-lookup"><span data-stu-id="292c2-152">Bots can proactively notify users about changes or updates to your app via chat.</span></span>

### <a name="chat-with-a-bot-in-different-contexts"></a><span data-ttu-id="292c2-153">Chatear con un bot en diferentes contextos</span><span class="sxs-lookup"><span data-stu-id="292c2-153">Chat with a bot in different contexts</span></span>

<span data-ttu-id="292c2-154">Puede usar bots en los siguientes contextos:</span><span class="sxs-lookup"><span data-stu-id="292c2-154">You can use bots in the following contexts:</span></span>

* <span data-ttu-id="292c2-155">**Aplicaciones personales**: en una aplicación personal, un bot tiene una pestaña dedicada de chat.</span><span class="sxs-lookup"><span data-stu-id="292c2-155">**Personal apps**: In a personal app, a bot has a dedicated chat tab.</span></span>
* <span data-ttu-id="292c2-156">**Chat de uno en uno**: un usuario puede iniciar una conversación privada con un bot.</span><span class="sxs-lookup"><span data-stu-id="292c2-156">**One-on-one chat**: A user can initiate a private conversation with a bot.</span></span> <span data-ttu-id="292c2-157">Tiene la misma experiencia que el uso de un bot en una aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="292c2-157">It's the same experience as using a bot in a personal app.</span></span>
* <span data-ttu-id="292c2-158">**Chat en grupo**: los usuarios pueden interactuar con un bot en un chat grupal por @mentioning el bot.</span><span class="sxs-lookup"><span data-stu-id="292c2-158">**Group chat**: People can interact with a bot in a group chat by @mentioning the bot.</span></span>
* <span data-ttu-id="292c2-159">**Canal**: los usuarios pueden interactuar con un bot en un canal.</span><span class="sxs-lookup"><span data-stu-id="292c2-159">**Channel**: People can interact with a bot in a channel.</span></span> <span data-ttu-id="292c2-160">@mentioning el nombre del bot en el cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="292c2-160">by @mentioning the bot name in the compose box.</span></span> <span data-ttu-id="292c2-161">Recuerde que, en este contexto, el bot está disponible para todo el equipo, no solo para el canal.</span><span class="sxs-lookup"><span data-stu-id="292c2-161">Remember, in this context, the bot is available to the entire team, not just the channel.</span></span>

### <a name="anatomy"></a><span data-ttu-id="292c2-162">Anatomía</span><span class="sxs-lookup"><span data-stu-id="292c2-162">Anatomy</span></span>

:::image type="content" source="../../assets/images/bots/bot-anatomy.png" alt-text="Ejemplo muestra una anatomía estructural de un bot." border="false":::

|<span data-ttu-id="292c2-164">Counter</span><span class="sxs-lookup"><span data-stu-id="292c2-164">Counter</span></span>|<span data-ttu-id="292c2-165">Descripción</span><span class="sxs-lookup"><span data-stu-id="292c2-165">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="292c2-166">1</span><span class="sxs-lookup"><span data-stu-id="292c2-166">1</span></span>|<span data-ttu-id="292c2-167">**Nombre y icono de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="292c2-167">**App name and icon**</span></span>|
|<span data-ttu-id="292c2-168">2 </span><span class="sxs-lookup"><span data-stu-id="292c2-168">2</span></span>|<span data-ttu-id="292c2-169">**Pestaña chat**: abre el espacio para hablar con el bot (aplicable solo a las aplicaciones personales).</span><span class="sxs-lookup"><span data-stu-id="292c2-169">**Chat tab**: Opens the space to talk with your bot (applicable only to personal apps).</span></span>|
|<span data-ttu-id="292c2-170">3 </span><span class="sxs-lookup"><span data-stu-id="292c2-170">3</span></span>|<span data-ttu-id="292c2-171">**Pestañas personalizadas**: abre otro contenido relacionado con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="292c2-171">**Custom tabs**: Opens other content related to your app.</span></span>|
|<span data-ttu-id="292c2-172">4 </span><span class="sxs-lookup"><span data-stu-id="292c2-172">4</span></span>|<span data-ttu-id="292c2-173">**Ficha acerca** de: muestra información básica sobre la aplicación.</span><span class="sxs-lookup"><span data-stu-id="292c2-173">**About tab**: Displays basic information about your app.</span></span>|
|<span data-ttu-id="292c2-174">5 </span><span class="sxs-lookup"><span data-stu-id="292c2-174">5</span></span>|<span data-ttu-id="292c2-175">**Burbuja de chat**: conversaciones de robot use el marco de mensajería de Teams.</span><span class="sxs-lookup"><span data-stu-id="292c2-175">**Chat bubble**: Bot conversations use the Teams messaging framework.</span></span>|
|<span data-ttu-id="292c2-176">6 </span><span class="sxs-lookup"><span data-stu-id="292c2-176">6</span></span>|<span data-ttu-id="292c2-177">**Tarjeta adaptable**: si las respuestas de su bot incluyen tarjetas adaptables, la tarjeta ocupa todo el ancho de la burbuja de chat.</span><span class="sxs-lookup"><span data-stu-id="292c2-177">**Adaptive Card**: If your bot’s responses include Adaptive Cards, the card takes up the full width of the chat bubble.</span></span>|
|<span data-ttu-id="292c2-178">7 </span><span class="sxs-lookup"><span data-stu-id="292c2-178">7</span></span>|<span data-ttu-id="292c2-179">**Menú de comandos**: muestra los comandos estándar del bot (definidos por el usuario).</span><span class="sxs-lookup"><span data-stu-id="292c2-179">**Command menu**: Displays your bot's standard commands (defined by you).</span></span>

### <a name="command-menu"></a><span data-ttu-id="292c2-180">Menú de comandos</span><span class="sxs-lookup"><span data-stu-id="292c2-180">Command menu</span></span>

<span data-ttu-id="292c2-181">El menú comando proporciona una lista de palabras o frases a las que desea que el bot responda siempre.</span><span class="sxs-lookup"><span data-stu-id="292c2-181">The command menu provides a list of words or phrases you want your bot to always respond to.</span></span> <span data-ttu-id="292c2-182">El menú comando se muestra encima del cuadro de redacción cuando alguien está conversando con un bot.</span><span class="sxs-lookup"><span data-stu-id="292c2-182">The command menu displays above the compose box when someone is conversing with a bot.</span></span> <span data-ttu-id="292c2-183">Cuando se selecciona un comando, se inserta en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="292c2-183">When a command is selected, it gets inserted into a message.</span></span>

<span data-ttu-id="292c2-184">La lista de comandos debe ser breve.</span><span class="sxs-lookup"><span data-stu-id="292c2-184">The list of commands should be brief.</span></span> <span data-ttu-id="292c2-185">El menú solo está destinado a resaltar las características principales del bot.</span><span class="sxs-lookup"><span data-stu-id="292c2-185">The menu is only meant to highlight your bot’s primary features.</span></span> <span data-ttu-id="292c2-186">Mantener también los comandos concisos.</span><span class="sxs-lookup"><span data-stu-id="292c2-186">Keep commands concise, too.</span></span> <span data-ttu-id="292c2-187">Por ejemplo, cree un comando llamado **ayuda** en lugar de, **por lo que puede ayudarme**?</span><span class="sxs-lookup"><span data-stu-id="292c2-187">For example, create a command called **Help** instead of **Can you please help me**?</span></span>
<span data-ttu-id="292c2-188">El menú de comandos debe estar siempre disponible independientemente del estado de la conversación.</span><span class="sxs-lookup"><span data-stu-id="292c2-188">The command menu must always be available regardless of the state of the conversation.</span></span>

:::image type="content" source="../../assets/images/bots/bot-command-menu.png" alt-text="Ejemplo muestra el menú de comandos de un bot." border="false":::

## <a name="understand-what-people-are-saying"></a><span data-ttu-id="292c2-190">Conocer lo que dicen los usuarios</span><span class="sxs-lookup"><span data-stu-id="292c2-190">Understand what people are saying</span></span>

<span data-ttu-id="292c2-191">Use un diccionario de sinónimos y obtenga personas de tantos fondos diferentes como sea posible para ayudarle a generar diferentes interpretaciones de consultas estándar.</span><span class="sxs-lookup"><span data-stu-id="292c2-191">Use a thesaurus and get people from as many different backgrounds as possible to help you generate different interpretations of standard queries.</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-hello.png" alt-text="Ilustración que muestra cómo un bot puede interpretar ' Hello '." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-help.png" alt-text="Ilustración que muestra cómo un bot puede interpretar &quot;ayuda&quot;." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-thanks.png" alt-text="Ilustración que muestra cómo un bot puede interpretar &quot;gracias&quot;." border="false":::
   :::column-end:::
:::row-end:::

### <a name="extract-intent-and-data-from-messages"></a><span data-ttu-id="292c2-195">Extraer el propósito y los datos de los mensajes</span><span class="sxs-lookup"><span data-stu-id="292c2-195">Extract intent and data from messages</span></span>

<span data-ttu-id="292c2-196">Diseñar el bot para que reconozca la intención, que captura lo que alguien quiere desde un bot en respuesta a un mensaje o consulta.</span><span class="sxs-lookup"><span data-stu-id="292c2-196">Design your bot to recognize intent, which captures what someone wants from a bot in response to a message or query.</span></span> <span data-ttu-id="292c2-197">Intención clasifica un mensaje o una consulta como una sola acción con uno o varios objetos de datos que se ven afectados por la acción.</span><span class="sxs-lookup"><span data-stu-id="292c2-197">Intent classifies a message or query as a single action with one or more data objects that are affected by the action.</span></span> 

<span data-ttu-id="292c2-198">En los ejemplos siguientes se describen la intención del usuario y los datos de los mensajes enviados a los bots.</span><span class="sxs-lookup"><span data-stu-id="292c2-198">The following examples outline the user intent and data in messages sent to bots.</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-1.png" alt-text="Ejemplo que muestra que en la oración ' reservar un vuelo para Seattle ', la intención del usuario es ' libro a vuelo ' y datos es ' Seattle '." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-2.png" alt-text="Ejemplo que muestra en la oración ' ¿Cuándo está abierto el almacén? ', el intento del usuario es ' When ' y los datos son ' Open '." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-3.png" alt-text="Ejemplo que muestra en la oración ' programar una reunión a las 13:00 con Bob en distribución ', la intención del usuario es &quot;programar una reunión&quot; y los datos son ' 13:00 ' y ' Bob en distribución '." border="false":::
   :::column-end:::
:::row-end:::

### <a name="analyze-and-improve"></a><span data-ttu-id="292c2-202">Analizar y mejorar</span><span class="sxs-lookup"><span data-stu-id="292c2-202">Analyze and improve</span></span>

<span data-ttu-id="292c2-203">Obtenga información sobre lo que dicen los usuarios al chatear con el bot.</span><span class="sxs-lookup"><span data-stu-id="292c2-203">Learn what users say when chatting with your bot.</span></span> <span data-ttu-id="292c2-204">Este será un proceso iterativo continuo a medida que crece la base de usuarios en distintas ubicaciones y organizaciones.</span><span class="sxs-lookup"><span data-stu-id="292c2-204">This will be an ongoing, iterative process as your user base grows in different locations and orgs.</span></span> <span data-ttu-id="292c2-205">Puede ajustar el reconocimiento de idioma y la asignación de intenciones de bot con la descripción de idioma de Microsoft (LUIS).</span><span class="sxs-lookup"><span data-stu-id="292c2-205">You can tune your bot's language recognition and intent mapping with Microsoft Language Understanding (LUIS).</span></span>

* <span data-ttu-id="292c2-206">[Descripción de Luis](https://docs.microsoft.com/azure/cognitive-services/luis/artificial-intelligence): Descubra cómo Luis usa AI para proporcionar una comprensión de lenguaje natural (NLU) a los datos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="292c2-206">[Understanding LUIS](https://docs.microsoft.com/azure/cognitive-services/luis/artificial-intelligence): Find out how LUIS uses AI to provide natural language understanding (NLU) to your app data.</span></span>
* <span data-ttu-id="292c2-207">[Integración con Luis](https://www.luis.ai/): Agregue capacidades de lenguaje natural a su bot sin el complejo proceso de crear modelos de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="292c2-207">[Integrating with LUIS](https://www.luis.ai/): Add natural language capabilities to your bot without the complex process of creating machine learning models.</span></span>

## <a name="use-cases"></a><span data-ttu-id="292c2-208">Casos de uso</span><span class="sxs-lookup"><span data-stu-id="292c2-208">Use cases</span></span>

### <a name="simple-queries"></a><span data-ttu-id="292c2-209">Consultas sencillas</span><span class="sxs-lookup"><span data-stu-id="292c2-209">Simple queries</span></span>

<span data-ttu-id="292c2-210">Los bots pueden proporcionar una coincidencia exacta a una consulta o grupo de coincidencias relacionadas para ayudar con la anulación de ambigüedades.</span><span class="sxs-lookup"><span data-stu-id="292c2-210">Bots can deliver an exact match to a query or a group of related matches to help with disambiguation.</span></span> <span data-ttu-id="292c2-211">Para obtener coincidencias relacionadas, agrupe el contenido con una tarjeta de lista.</span><span class="sxs-lookup"><span data-stu-id="292c2-211">For related matches, group the content using a list card.</span></span>

:::image type="content" source="../../assets/images/bots/bot-simple-query.png" alt-text="Ejemplo muestra una interacción de consulta simple con un bot." border="false":::

### <a name="multi-turn-interactions"></a><span data-ttu-id="292c2-213">Interacciones de múltiples torneados</span><span class="sxs-lookup"><span data-stu-id="292c2-213">Multi-turn interactions</span></span>

<span data-ttu-id="292c2-214">Aunque el bot puede admitir solicitudes y preguntas completas, también debe ser capaz de controlar las interacciones de varios turnos.</span><span class="sxs-lookup"><span data-stu-id="292c2-214">While your bot can support complete requests and questions, it should also be able to handle multi-turn interactions.</span></span> <span data-ttu-id="292c2-215">Anticiparse a los posibles pasos siguientes hace que sea mucho más fácil para los usuarios realizar un flujo de tareas completo (en lugar de esperar que se diseñe una solicitud completa).</span><span class="sxs-lookup"><span data-stu-id="292c2-215">Anticipating possible next steps makes it much easier for people to a complete task flow (rather than expecting them to craft a comprehensive request).</span></span>

<span data-ttu-id="292c2-216">En el siguiente ejemplo, el bot responde a cada mensaje con opciones para lo que es posible que quiera hacer a continuación.</span><span class="sxs-lookup"><span data-stu-id="292c2-216">In the following example, the bot responds to each message with options for what might want to do next.</span></span>

:::image type="content" source="../../assets/images/bots/bot-multi-turn.png" alt-text="Ejemplo muestra una interacción de varios turnos con un bot." border="false":::

### <a name="reach-out-to-users"></a><span data-ttu-id="292c2-218">Ponerse en contacto con los usuarios</span><span class="sxs-lookup"><span data-stu-id="292c2-218">Reach out to users</span></span>

<span data-ttu-id="292c2-219">Con la mensajería proactiva, el bot puede actuar como un resumen que envía las notificaciones relevantes a un individuo, un chat en grupo o un canal a una frecuencia específica.</span><span class="sxs-lookup"><span data-stu-id="292c2-219">With proactive messaging, your bot can act like a digest that sends notifications relevant to an individual, group chat, or channel at a specific frequency.</span></span> <span data-ttu-id="292c2-220">Un bot puede enviar un mensaje cuando algo ha cambiado en un documento o se cierra un elemento de trabajo.</span><span class="sxs-lookup"><span data-stu-id="292c2-220">A bot may send a message when something has changed in a document or a work item is closed.</span></span>

<span data-ttu-id="292c2-221">En el siguiente ejemplo, un usuario recibe una notificación del sistema que un bot ha puesto en un mensaje en otro canal.</span><span class="sxs-lookup"><span data-stu-id="292c2-221">In the following example, a user gets a toast notification that a bot messaged them in another channel.</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message-toast.png" alt-text="Ejemplo muestra que una notificación de un bot es una mensajería proactiva de un usuario de otro canal." border="false":::

<span data-ttu-id="292c2-223">Ahora, en ese canal, el usuario puede leer su mensaje desde el bot.</span><span class="sxs-lookup"><span data-stu-id="292c2-223">Now in that channel, the user can read their message from the bot.</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message.png" alt-text="Ejemplo muestra el usuario que mira el mensaje proactivo del bot." border="false":::

### <a name="use-tabs-with-bots"></a><span data-ttu-id="292c2-225">Usar pestañas con bots</span><span class="sxs-lookup"><span data-stu-id="292c2-225">Use tabs with bots</span></span>

<span data-ttu-id="292c2-226">Una pestaña puede hacer que el bot sea más fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="292c2-226">A tab can make your bot easier to use.</span></span> <span data-ttu-id="292c2-227">Por ejemplo, si el bot puede crear elementos de trabajo, sería estupendo Mostrar todos esos elementos en una ubicación central dentro de una pestaña. Vea más información sobre el [diseño de pestañas](../../tabs/design/tabs.md).</span><span class="sxs-lookup"><span data-stu-id="292c2-227">For example, if your bot can create work items, it would be nice to show all those items in a central location inside a tab. See more about [designing tabs](../../tabs/design/tabs.md).</span></span>

:::image type="content" source="../../assets/images/bots/bot-with-tab.png" alt-text="Ejemplo muestra cómo una pestaña puede ayudar a organizar el contenido de los robots." border="false":::

## <a name="manage-a-bot"></a><span data-ttu-id="292c2-229">Administrar un bot</span><span class="sxs-lookup"><span data-stu-id="292c2-229">Manage a bot</span></span>

<span data-ttu-id="292c2-230">Los usuarios deben poder cambiar la configuración de un bot.</span><span class="sxs-lookup"><span data-stu-id="292c2-230">Users should be able to change a bot's settings.</span></span> <span data-ttu-id="292c2-231">Puede proporcionar esta funcionalidad con comandos de bot, pero normalmente es más eficaz incluir toda la configuración en un [módulo de tareas](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (como se muestra en el ejemplo siguiente).</span><span class="sxs-lookup"><span data-stu-id="292c2-231">You can provide this functionality with bot commands, but it's usually more efficient to include all settings in a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (as shown in the following example).</span></span>

:::image type="content" source="../../assets/images/bots/manage-bot-task-module.png" alt-text="Ejemplo muestra un módulo de tareas para configurar las opciones de un bot." border="false":::

## <a name="best-practices"></a><span data-ttu-id="292c2-233">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="292c2-233">Best practices</span></span>

### <a name="content"></a><span data-ttu-id="292c2-234">Contenido</span><span class="sxs-lookup"><span data-stu-id="292c2-234">Content</span></span>

:::image type="content" source="../../assets/images/bots/bot-content-persona-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot." border="false":::

#### <a name="do-establish-a-clear-persona"></a><span data-ttu-id="292c2-236">Do: establecer un rol claro</span><span class="sxs-lookup"><span data-stu-id="292c2-236">Do: Establish a clear persona</span></span>

<span data-ttu-id="292c2-237">¿La luz y el tono de su bot, "solo los hechos" o la anomalía?</span><span class="sxs-lookup"><span data-stu-id="292c2-237">Is your bot's tone friendly and light, “just the facts”, or super quirky?</span></span> <span data-ttu-id="292c2-238">¿Cómo debe responder en escenarios diferentes?</span><span class="sxs-lookup"><span data-stu-id="292c2-238">How should it respond in different scenarios?</span></span> <span data-ttu-id="292c2-239">La planeación y documentación del rol de un bot facilita la escritura de respuestas que parecen naturales y coherentes.</span><span class="sxs-lookup"><span data-stu-id="292c2-239">Planning and documenting your bot's persona makes it easier to write responses that seem natural and cohesive.</span></span>

<span data-ttu-id="292c2-240">Vea más información sobre cómo escribir para bots en el <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Kit de interfaz de usuario de Microsoft Teams (Figma).</a></span><span class="sxs-lookup"><span data-stu-id="292c2-240">See more about writing for bots in the <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft Teams UI Kit (Figma).</a></span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot." border="false":::

#### <a name="do-clearly-convey-what-your-bot-can-do"></a><span data-ttu-id="292c2-242">Do: transmitir claramente lo que puede hacer su bot</span><span class="sxs-lookup"><span data-stu-id="292c2-242">Do: Clearly convey what your bot can do</span></span>

<span data-ttu-id="292c2-243">Los mensajes de bienvenida y los paseos ayudan a los usuarios a comprender lo que pueden hacer con el bot.</span><span class="sxs-lookup"><span data-stu-id="292c2-243">Welcome messages and tours help people understand what they can do with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot." border="false":::

#### <a name="dont-obscure-your-bots-features"></a><span data-ttu-id="292c2-245">No: ocultar las características de la bot</span><span class="sxs-lookup"><span data-stu-id="292c2-245">Don't: Obscure your bot's features</span></span>

<span data-ttu-id="292c2-246">Primera impresión importa.</span><span class="sxs-lookup"><span data-stu-id="292c2-246">First impressions matter.</span></span> <span data-ttu-id="292c2-247">Es probable que los usuarios sean confusos o sospechosos cuando se les presente un mensaje de inicio de sesión de nondescript.</span><span class="sxs-lookup"><span data-stu-id="292c2-247">People will likely be confused or suspicious when presented with a nondescript sign-in message.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot." border="false":::

#### <a name="do-recognize-non-questions"></a><span data-ttu-id="292c2-249">Do: reconocer no preguntas</span><span class="sxs-lookup"><span data-stu-id="292c2-249">Do: Recognize non-questions</span></span>

<span data-ttu-id="292c2-250">El bot debe ser capaz de responder a mensajes como "HI", "Help" y "Agradecimientos", además de tener en cuenta los errores y coloquialess comunes.</span><span class="sxs-lookup"><span data-stu-id="292c2-250">Your bot should be able to respond to messages like "Hi", "Help", and "Thanks" while also accounting for common misspellings and colloquialisms.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot." border="false":::

#### <a name="dont-miss-out-on-opportunities-to-delight"></a><span data-ttu-id="292c2-252">No: no se pierdan las oportunidades de alegría</span><span class="sxs-lookup"><span data-stu-id="292c2-252">Don't: Miss out on opportunities to delight</span></span>

<span data-ttu-id="292c2-253">Algunos usuarios esperan que las conversaciones fluyan naturalmente como lo harían con una persona real.</span><span class="sxs-lookup"><span data-stu-id="292c2-253">Some people expect conversations to flow naturally like they would with a real person.</span></span> <span data-ttu-id="292c2-254">Intente evitar las respuestas más difíciles a los mensajes sencillos.</span><span class="sxs-lookup"><span data-stu-id="292c2-254">Try to avoid clumsy responses to simple messages.</span></span>

   :::column-end:::
:::row-end:::

### <a name="troubleshooting"></a><span data-ttu-id="292c2-255">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="292c2-255">Troubleshooting</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot." border="false":::

#### <a name="do-provide-help"></a><span data-ttu-id="292c2-257">Do: proporcionar ayuda</span><span class="sxs-lookup"><span data-stu-id="292c2-257">Do: Provide help</span></span>

<span data-ttu-id="292c2-258">Si el bot no puede satisfacer una solicitud, proporcione medios para que un usuario se enseñe a interactuar con el bot.</span><span class="sxs-lookup"><span data-stu-id="292c2-258">If your bot can’t satisfy a request, provide ways for a user to educate themselves about interacting with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot." border="false":::

#### <a name="dont-leave-users-stranded"></a><span data-ttu-id="292c2-260">No: dejar a los usuarios en desuso</span><span class="sxs-lookup"><span data-stu-id="292c2-260">Don't: Leave users stranded</span></span>

<span data-ttu-id="292c2-261">Los usuarios abandonarán rápidamente el bot si no pueden solucionar los problemas.</span><span class="sxs-lookup"><span data-stu-id="292c2-261">People will quickly abandon your bot if they can’t troubleshoot issues.</span></span>

   :::column-end:::
:::row-end:::

### <a name="complex-interactions"></a><span data-ttu-id="292c2-262">Interacciones complejas</span><span class="sxs-lookup"><span data-stu-id="292c2-262">Complex interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot." border="false":::

#### <a name="do-use-task-modules-or-tabs"></a><span data-ttu-id="292c2-264">Do: usar módulos de tareas o pestañas</span><span class="sxs-lookup"><span data-stu-id="292c2-264">Do: Use task modules or tabs</span></span>

<span data-ttu-id="292c2-265">Si el bot proporciona una respuesta que requiere algunos pasos más, puede vincular a un módulo de tarea o a una pestaña para completar la tarea o el flujo.</span><span class="sxs-lookup"><span data-stu-id="292c2-265">If your bot provides an answer that requires a few more steps, you can link to a task module or tab to complete the task or flow.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot." border="false":::

#### <a name="dont-make-multi-turn-interactions-tedious"></a><span data-ttu-id="292c2-267">No: hacer que las interacciones de varios turnos sean tediosas</span><span class="sxs-lookup"><span data-stu-id="292c2-267">Don't: Make multi-turn interactions tedious</span></span>

<span data-ttu-id="292c2-268">Una conversación extensa para completar una tarea única es lenta y demasiado compleja.</span><span class="sxs-lookup"><span data-stu-id="292c2-268">An extensive conversation to complete a single task is slow and overly complex.</span></span> <span data-ttu-id="292c2-269">También se requiere que el desarrollador tenga en cuenta los cambios de estado (por ejemplo, el tiempo de espera de la conversación o el envío de un mensaje de "cancelación").</span><span class="sxs-lookup"><span data-stu-id="292c2-269">It also requires the developer to account for state changes (such as the conversation timing out or you sending a “Cancel” message).</span></span>

   :::column-end:::
:::row-end:::

### <a name="privacy"></a><span data-ttu-id="292c2-270">Privacidad</span><span class="sxs-lookup"><span data-stu-id="292c2-270">Privacy</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot." border="false":::

#### <a name="do-only-show-sensitive-info-in-a-personal-context"></a><span data-ttu-id="292c2-272">Do: mostrar solo información confidencial en un contexto personal</span><span class="sxs-lookup"><span data-stu-id="292c2-272">Do: Only show sensitive info in a personal context</span></span>

<span data-ttu-id="292c2-273">Si el bot está en un canal o en un chat de grupo, se recomienda dirigir a los usuarios a una ubicación privada (como un módulo de tareas, una ficha o un explorador) para ver la información confidencial.</span><span class="sxs-lookup"><span data-stu-id="292c2-273">If your bot is in a group chat or channel, we recommend directing users to a private location (such as a task module, tab, or browser) to view sensitive information.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de bot." border="false":::

#### <a name="dont-some-content-isnt-meant-to-be-seen-by-everyone"></a><span data-ttu-id="292c2-275">No: algún contenido no está diseñado para ser visto por todos los usuarios</span><span class="sxs-lookup"><span data-stu-id="292c2-275">Don't: Some content isn’t meant to be seen by everyone</span></span>

<span data-ttu-id="292c2-276">El bot no debe revelar información confidencial a un grupo de personas.</span><span class="sxs-lookup"><span data-stu-id="292c2-276">Your bot shouldn’t reveal sensitive information to a group of people.</span></span>

   :::column-end:::
:::row-end:::

## <a name="learn-more"></a><span data-ttu-id="292c2-277">Más información</span><span class="sxs-lookup"><span data-stu-id="292c2-277">Learn more</span></span>

<span data-ttu-id="292c2-278">Estas otras instrucciones pueden ayudarle con el diseño de su bot:</span><span class="sxs-lookup"><span data-stu-id="292c2-278">These other guidelines may help with your bot design:</span></span>

* [<span data-ttu-id="292c2-279">Diseño de la aplicación personal</span><span class="sxs-lookup"><span data-stu-id="292c2-279">Designing your personal app</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="292c2-280">Diseño de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="292c2-280">Designing Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)
* [<span data-ttu-id="292c2-281">Diseño de módulos de tareas</span><span class="sxs-lookup"><span data-stu-id="292c2-281">Designing task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)

## <a name="validate-your-design"></a><span data-ttu-id="292c2-282">Validar el diseño</span><span class="sxs-lookup"><span data-stu-id="292c2-282">Validate your design</span></span>

<span data-ttu-id="292c2-283">Si planea publicar la aplicación en AppSource, debe comprender los problemas de diseño que suelen hacer que las aplicaciones fallen durante el envío.</span><span class="sxs-lookup"><span data-stu-id="292c2-283">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="292c2-284">Comprobar las instrucciones de validación del diseño</span><span class="sxs-lookup"><span data-stu-id="292c2-284">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)

---
title: Diseño de la extensión de mensajería
description: Obtén información sobre cómo diseñar una Teams de mensajería y obtener el kit Microsoft Teams interfaz de usuario.
keywords: Recomendaciones sobre extensiones de mensajería de referencia de directrices de diseño de teams
author: heath-hamilton
localization_priority: Normal
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: fd870d8e10ef74c36f8f6d145d48980f53e9303c
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631075"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a><span data-ttu-id="3f601-104">Diseño de la extensión Microsoft Teams de mensajería</span><span class="sxs-lookup"><span data-stu-id="3f601-104">Designing your Microsoft Teams messaging extension</span></span>

<span data-ttu-id="3f601-105">Las extensiones de mensajería son métodos abreviados para insertar contenido de la aplicación o actuar en un mensaje sin salir de la conversación.</span><span class="sxs-lookup"><span data-stu-id="3f601-105">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span>
<span data-ttu-id="3f601-106">Para guiar el diseño de la aplicación, la siguiente información describe e ilustra cómo los usuarios pueden agregar, usar y administrar extensiones de mensajería en Teams.</span><span class="sxs-lookup"><span data-stu-id="3f601-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage messaging extensions in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="3f601-107">Kit de UI de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3f601-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="3f601-108">Puedes encontrar instrucciones completas de diseño de extensión de mensajería, incluidos los elementos que puedes agarrar y modificar según sea necesario, en el kit de interfaz Microsoft Teams de usuario.</span><span class="sxs-lookup"><span data-stu-id="3f601-108">You can find comprehensive messaging extension design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3f601-109">Obtener el Kit de UI de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="3f601-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a><span data-ttu-id="3f601-110">Agregar una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="3f601-110">Add a messaging extension</span></span>

<span data-ttu-id="3f601-111">Puede agregar una extensión de mensajería en los siguientes Teams contextos:</span><span class="sxs-lookup"><span data-stu-id="3f601-111">You can add a messaging extension in the following Teams contexts:</span></span>

* <span data-ttu-id="3f601-112">Desde el Teams almacén.</span><span class="sxs-lookup"><span data-stu-id="3f601-112">From the Teams store.</span></span>
* <span data-ttu-id="3f601-113">En un canal, chat o reunión (antes, durante y después) cerca del cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="3f601-113">In a channel, chat, or meeting (before, during, and after) near the compose box.</span></span> <span data-ttu-id="3f601-114">Vale la pena tener en cuenta que si agregas una extensión de mensajería en uno de estos lugares, solo puedes usarla en ese contexto.</span><span class="sxs-lookup"><span data-stu-id="3f601-114">It's worth noting if you add a messaging extension in one of these places, only you can use it in that context.</span></span>

<span data-ttu-id="3f601-115">En el ejemplo siguiente se muestra cómo agregar una extensión de mensajería en un canal:</span><span class="sxs-lookup"><span data-stu-id="3f601-115">The following example shows how you add a messaging extension in a channel:</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3f601-116">Escritorio</span><span class="sxs-lookup"><span data-stu-id="3f601-116">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de mensajería cerca del cuadro de redacción de un canal." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3f601-118">Móvil</span><span class="sxs-lookup"><span data-stu-id="3f601-118">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-add-in-channel.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de mensajería cerca del cuadro de redacción en un canal en el móvil." border="false":::

---

## <a name="set-up-a-messaging-extension"></a><span data-ttu-id="3f601-120">Configurar una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="3f601-120">Set up a messaging extension</span></span>

<span data-ttu-id="3f601-121">La autenticación no es obligatoria, pero si la aplicación es algo parecido a una herramienta de seguimiento de vales, es posible que necesites que las personas inicien sesión para usar la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="3f601-121">Authentication isn't mandatory, but if your app is something like a ticket tracking tool, you may need people to sign in to use the messaging extension.</span></span>

<span data-ttu-id="3f601-122">Para obtener coherencia Teams aplicaciones, no puedes personalizar la pantalla de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="3f601-122">For consistency across Teams apps, you can't customize the sign-in screen.</span></span> <span data-ttu-id="3f601-123">Si usa la autenticación de inicio de sesión único (SSO), los usuarios iniciarán sesión automáticamente.</span><span class="sxs-lookup"><span data-stu-id="3f601-123">If you use single sign-on (SSO) authentication, users are signed in automatically.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3f601-124">Escritorio</span><span class="sxs-lookup"><span data-stu-id="3f601-124">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="En el ejemplo se muestra la pantalla de configuración de extensión de mensajería con un botón de inicio de sesión." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3f601-126">Móvil</span><span class="sxs-lookup"><span data-stu-id="3f601-126">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-set-up.png" alt-text="En el ejemplo se muestra la pantalla de configuración de extensión de mensajería con un botón de inicio de sesión en el móvil." border="false":::

---

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="3f601-128">Tipos de extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="3f601-128">Types of messaging extensions</span></span>

<span data-ttu-id="3f601-129">Las extensiones de mensajería pueden tener comandos de búsqueda, comandos de acción o ambos.</span><span class="sxs-lookup"><span data-stu-id="3f601-129">Messaging extensions can have search commands, action commands, or both.</span></span> <span data-ttu-id="3f601-130">Los comandos dependen de las características de la aplicación y de cómo se ajustan a Teams casos de uso.</span><span class="sxs-lookup"><span data-stu-id="3f601-130">Your commands depend on your app's features and how those fit within Teams use cases.</span></span>

### <a name="search-commands"></a><span data-ttu-id="3f601-131">Comandos de búsqueda</span><span class="sxs-lookup"><span data-stu-id="3f601-131">Search commands</span></span>

<span data-ttu-id="3f601-132">Con los comandos de búsqueda, los usuarios pueden usar la extensión de mensajería para buscar rápidamente contenido externo e insertarlo en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="3f601-132">With search commands, people can use your messaging extension to quickly find external content and insert into a message.</span></span> <span data-ttu-id="3f601-133">Los comandos de búsqueda normalmente están disponibles en el cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="3f601-133">Search commands are commonly made available in the compose box.</span></span> <span data-ttu-id="3f601-134">Por ejemplo, puede iniciar o agregar a una discusión compartiendo un fragmento de contenido, sin salir de Teams.</span><span class="sxs-lookup"><span data-stu-id="3f601-134">For example, you can start or add to a discussion by sharing a piece of content—without ever leaving Teams.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3f601-135">Escritorio</span><span class="sxs-lookup"><span data-stu-id="3f601-135">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="En el ejemplo se muestra una extensión de mensajería basada en búsqueda iniciada desde el cuadro de redacción." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3f601-137">Móvil</span><span class="sxs-lookup"><span data-stu-id="3f601-137">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-search-command-type.png" alt-text="En el ejemplo se muestra una extensión de mensajería basada en búsqueda iniciada desde el cuadro de redacción en el móvil." border="false":::

---

#### <a name="compose-box-layout-options"></a><span data-ttu-id="3f601-139">Opciones de diseño de cuadro de redacción</span><span class="sxs-lookup"><span data-stu-id="3f601-139">Compose box layout options</span></span>

<span data-ttu-id="3f601-140">Tiene algunas opciones para mostrar los resultados de búsqueda de extensión de mensajería, incluidas [las vistas de lista y cuadrícula.](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)</span><span class="sxs-lookup"><span data-stu-id="3f601-140">You have some options for displaying messaging extension search results, including [list and grid views](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="Ilustraciones que muestran las opciones de diseño para los resultados de búsqueda de extensión de mensajería." border="false":::

### <a name="action-commands"></a><span data-ttu-id="3f601-142">Comandos de acción</span><span class="sxs-lookup"><span data-stu-id="3f601-142">Action commands</span></span>

<span data-ttu-id="3f601-143">Los comandos action permiten a los usuarios desencadenar acciones y procesar solicitudes en servicios externos dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="3f601-143">Action commands allow people to trigger actions and process requests in external services within Teams.</span></span> <span data-ttu-id="3f601-144">Por ejemplo, si la aplicación realiza un seguimiento de los pedidos, un usuario podría crear un nuevo pedido con el contenido del mensaje de un compañero desde el chat.</span><span class="sxs-lookup"><span data-stu-id="3f601-144">For example, if your app tracks orders, a user could create a new order using the contents of a colleague’s message from right inside their chat.</span></span>

<span data-ttu-id="3f601-145">Con frecuencia, las extensiones de mensajería basadas en acciones requieren que los usuarios completen un formulario o algún otro tipo de configuración dentro de un modal.</span><span class="sxs-lookup"><span data-stu-id="3f601-145">Action-based messaging extensions frequently require users to complete a form or some other kind of configuration within a modal.</span></span> <span data-ttu-id="3f601-146">Puede crear estas experiencias con [módulos de tareas](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span><span class="sxs-lookup"><span data-stu-id="3f601-146">You can create these experiences with [task modules](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="open-a-messaging-extension"></a><span data-ttu-id="3f601-147">Abrir una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="3f601-147">Open a messaging extension</span></span>

<span data-ttu-id="3f601-148">El cuadro de redacción y los mensajes o publicaciones son los contextos principales donde los usuarios usan extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="3f601-148">The compose box and messages or posts are the primary contexts where people use messaging extensions.</span></span>

### <a name="from-the-compose-box"></a><span data-ttu-id="3f601-149">Desde el cuadro de redacción</span><span class="sxs-lookup"><span data-stu-id="3f601-149">From the compose box</span></span>

<span data-ttu-id="3f601-150">Una vez agregado, los usuarios pueden abrir la extensión de mensajería seleccionando el icono de la aplicación debajo del cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="3f601-150">Once added, users can open your messaging extension by selecting your app icon below the compose box.</span></span> <span data-ttu-id="3f601-151">En estos ejemplos, la extensión tiene comandos de búsqueda y acción.</span><span class="sxs-lookup"><span data-stu-id="3f601-151">In these examples, the extension has search and action commands.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3f601-152">Escritorio</span><span class="sxs-lookup"><span data-stu-id="3f601-152">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="En el ejemplo se muestra cómo abrir una extensión de mensajería desde el cuadro de redacción." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3f601-154">Móvil</span><span class="sxs-lookup"><span data-stu-id="3f601-154">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-compose-box.png" alt-text="En el ejemplo se muestra cómo abrir una extensión de mensajería desde el cuadro de redacción en el móvil." border="false":::

---

### <a name="from-a-chat-message-or-channel-post"></a><span data-ttu-id="3f601-156">Desde un mensaje de chat o una publicación de canal</span><span class="sxs-lookup"><span data-stu-id="3f601-156">From a chat message or channel post</span></span>

Una vez agregado, los usuarios pueden seleccionar el icono **Más** en el mensaje de chat o la publicación del canal para buscar los comandos de acción :::image type="icon" source="../../assets/icons/teams-client-more.png"::: de la extensión. <span data-ttu-id="3f601-158">La extensión puede aparecer en **Más acciones basadas** en el uso.</span><span class="sxs-lookup"><span data-stu-id="3f601-158">Your extension may be listed under **More actions** based on usage.</span></span>

> [!NOTE]
> <span data-ttu-id="3f601-159">La compatibilidad con más acciones de un mensaje de chat o una publicación de canal no está disponible en Microsoft Teams plataforma móvil.</span><span class="sxs-lookup"><span data-stu-id="3f601-159">Support for more actions from a chat message or channel post is not available on Microsoft Teams mobile platform.</span></span> 

#### <a name="chat-message"></a><span data-ttu-id="3f601-160">Mensaje de chat</span><span class="sxs-lookup"><span data-stu-id="3f601-160">Chat message</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3f601-161">Escritorio</span><span class="sxs-lookup"><span data-stu-id="3f601-161">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="En el ejemplo se muestra cómo abrir una extensión de mensajería desde un mensaje de chat." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3f601-163">Móvil</span><span class="sxs-lookup"><span data-stu-id="3f601-163">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-chat-post.png" alt-text="En el ejemplo se muestra cómo abrir una extensión de mensajería desde una publicación de chat en el móvil." border="false":::

---
':::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false"::': null
':::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false"::': null
---

## <a name="use-a-messaging-extension"></a><span data-ttu-id="3f601-165">Usar una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="3f601-165">Use a messaging extension</span></span>

<span data-ttu-id="3f601-166">En los siguientes escenarios se muestran las formas principales en que los usuarios usan extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="3f601-166">The following scenarios show the primary ways people use messaging extensions.</span></span>

### <a name="insert-content-into-a-message"></a><span data-ttu-id="3f601-167">Insertar contenido en un mensaje</span><span class="sxs-lookup"><span data-stu-id="3f601-167">Insert content into a message</span></span>

<span data-ttu-id="3f601-168">**1. Seleccione una extensión de mensajería**.</span><span class="sxs-lookup"><span data-stu-id="3f601-168">**1. Select a messaging extension**.</span></span> <span data-ttu-id="3f601-169">Los usuarios pueden buscar el contenido que desean compartir desde el cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="3f601-169">Users can search for the content they want to share from the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3f601-170">Escritorio</span><span class="sxs-lookup"><span data-stu-id="3f601-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="En el ejemplo se muestra un usuario que busca contenido para insertar desde el cuadro de redacción." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3f601-172">Móvil</span><span class="sxs-lookup"><span data-stu-id="3f601-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-search.png" alt-text="En el ejemplo se muestra un usuario que busca contenido para insertar desde el cuadro de redacción en el móvil." border="false":::

---

<span data-ttu-id="3f601-174">**2. Insertar contenido**.</span><span class="sxs-lookup"><span data-stu-id="3f601-174">**2. Insert content**.</span></span> <span data-ttu-id="3f601-175">Una vez publicado, otros usuarios pueden responder o seleccionar el contenido para ver más información en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3f601-175">Once posted, others can reply or select the content to see more information in your app.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3f601-176">Escritorio</span><span class="sxs-lookup"><span data-stu-id="3f601-176">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="En el ejemplo se muestra un usuario que publica contenido en una conversación de canal." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3f601-178">Móvil</span><span class="sxs-lookup"><span data-stu-id="3f601-178">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-posted.png" alt-text="En el ejemplo se muestra un usuario que publica contenido en una conversación de canal en el móvil." border="false":::

---

### <a name="take-action-on-a-message"></a><span data-ttu-id="3f601-180">Realizar acciones en un mensaje</span><span class="sxs-lookup"><span data-stu-id="3f601-180">Take action on a message</span></span>

<span data-ttu-id="3f601-181">**1. Seleccione una extensión de mensajería**.</span><span class="sxs-lookup"><span data-stu-id="3f601-181">**1. Select a messaging extension**.</span></span> <span data-ttu-id="3f601-182">La aplicación puede incluir uno o varios comandos de acción.</span><span class="sxs-lookup"><span data-stu-id="3f601-182">Your app can include one or more action commands.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3f601-183">Escritorio</span><span class="sxs-lookup"><span data-stu-id="3f601-183">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="En el ejemplo se muestra un usuario que selecciona un comando de acción de extensión de mensajería." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3f601-185">Móvil</span><span class="sxs-lookup"><span data-stu-id="3f601-185">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-select-action-command.png" alt-text="En el ejemplo se muestra un usuario que selecciona un comando de acción de extensión de mensajería en el móvil." border="false":::

---

<span data-ttu-id="3f601-187">**2. Complete la acción**.</span><span class="sxs-lookup"><span data-stu-id="3f601-187">**2. Complete the action**.</span></span> <span data-ttu-id="3f601-188">La aplicación puede recibir y procesar cualquier contenido o datos enviados por la acción del mensaje.</span><span class="sxs-lookup"><span data-stu-id="3f601-188">Your app can receive and process any content or data sent by the message action.</span></span> <span data-ttu-id="3f601-189">Esto permite a los usuarios permanecer en su conversación y, en el ejemplo siguiente, no preocuparse por escribir información directamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3f601-189">This allows users to remain in their conversation and, the following example, not worry about entering information directly in your app.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3f601-190">Escritorio</span><span class="sxs-lookup"><span data-stu-id="3f601-190">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="Ejemplo sobre cómo realizar acciones en un mensaje." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3f601-192">Móvil</span><span class="sxs-lookup"><span data-stu-id="3f601-192">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-complete-action-command.png" alt-text="Ejemplo sobre cómo realizar acciones en un mensaje en el móvil." border="false":::

---

### <a name="preview-links"></a><span data-ttu-id="3f601-194">Vínculos de vista previa</span><span class="sxs-lookup"><span data-stu-id="3f601-194">Preview links</span></span>

<span data-ttu-id="3f601-195">Las extensiones de mensajería también permiten insertar vínculos enriquecidos desde una dirección URL reconocida en un mensaje (esta funcionalidad se denomina desafugüe [de vínculos](../../messaging-extensions/how-to/link-unfurling.md)).)</span><span class="sxs-lookup"><span data-stu-id="3f601-195">Messaging extensions also allow you to insert rich links from a recognized URL into a message (this capability is called [link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)</span></span>

<span data-ttu-id="3f601-196">**1. Pegue un vínculo reconocido en** el cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="3f601-196">**1. Paste a recognized link** in the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3f601-197">Escritorio</span><span class="sxs-lookup"><span data-stu-id="3f601-197">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="En el ejemplo se muestra a un usuario pegando un vínculo en el cuadro de compost." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3f601-199">Móvil</span><span class="sxs-lookup"><span data-stu-id="3f601-199">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-paste-preview-link.png" alt-text="En el ejemplo se muestra a un usuario pegando un vínculo en el cuadro de compost en el móvil." border="false":::

---

<span data-ttu-id="3f601-201">**2. Insertar contenido**.</span><span class="sxs-lookup"><span data-stu-id="3f601-201">**2. Insert content**.</span></span> <span data-ttu-id="3f601-202">Si la aplicación reconoce la dirección URL en el cuadro de redacción, representa el vínculo como una tarjeta que proporciona una vista previa con contenido enriquecido del contenido web.</span><span class="sxs-lookup"><span data-stu-id="3f601-202">If your app recognizes the URL in the compose box, it renders the link as a card that provides a content-rich preview of the web content.</span></span> <span data-ttu-id="3f601-203">(Vea [Directrices de diseño de tarjetas adaptables](../../task-modules-and-cards/cards/design-effective-cards.md) para obtener más información).</span><span class="sxs-lookup"><span data-stu-id="3f601-203">(See [Adaptive Cards design guidelines](../../task-modules-and-cards/cards/design-effective-cards.md) for more information.)</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3f601-204">Escritorio</span><span class="sxs-lookup"><span data-stu-id="3f601-204">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="En un ejemplo se muestra cómo la dirección URL, ya que la reconoce la aplicación, incluye contenido enriquecido en el cuadro de redacción." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3f601-206">Móvil</span><span class="sxs-lookup"><span data-stu-id="3f601-206">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-preview-link.png" alt-text="En un ejemplo se muestra cómo la dirección URL, ya que la reconoce la aplicación, incluye contenido enriquecido en el cuadro de redacción en el móvil." border="false":::

---

## <a name="manage-a-messaging-extension"></a><span data-ttu-id="3f601-208">Administrar una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="3f601-208">Manage a messaging extension</span></span>

<span data-ttu-id="3f601-209">Al hacer clic con el botón secundario en el icono, los usuarios pueden anclar, quitar o configurar la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="3f601-209">By right clicking your icon, users can pin, remove, or configure your messaging extension.</span></span>

## <a name="anatomy"></a><span data-ttu-id="3f601-210">Anatomía</span><span class="sxs-lookup"><span data-stu-id="3f601-210">Anatomy</span></span>

### <a name="messaging-extension-in-the-compose-box"></a><span data-ttu-id="3f601-211">Extensión de mensajería en el cuadro de redacción</span><span class="sxs-lookup"><span data-stu-id="3f601-211">Messaging extension in the compose box</span></span>

<span data-ttu-id="3f601-212">El siguiente ejemplo es una extensión de mensajería abierta desde el cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="3f601-212">The following example is a messaging extension opened from the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3f601-213">Escritorio</span><span class="sxs-lookup"><span data-stu-id="3f601-213">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una extensión de mensajería en el cuadro de redacción." border="false":::

|<span data-ttu-id="3f601-215">Contador</span><span class="sxs-lookup"><span data-stu-id="3f601-215">Counter</span></span>|<span data-ttu-id="3f601-216">Descripción</span><span class="sxs-lookup"><span data-stu-id="3f601-216">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="3f601-217">1</span><span class="sxs-lookup"><span data-stu-id="3f601-217">1</span></span>|<span data-ttu-id="3f601-218">**Logotipo de la aplicación:** icono de color del logotipo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3f601-218">**App logo**: Color icon of your app logo.</span></span>|
|<span data-ttu-id="3f601-219">2</span><span class="sxs-lookup"><span data-stu-id="3f601-219">2</span></span>|<span data-ttu-id="3f601-220">**Nombre de la** aplicación: nombre completo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3f601-220">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="3f601-221">3</span><span class="sxs-lookup"><span data-stu-id="3f601-221">3</span></span>|<span data-ttu-id="3f601-222">**Icono de menú Comandos de acción (opcional):** abre una lista de comandos de acción para la extensión de mensajería (si especifica alguno).</span><span class="sxs-lookup"><span data-stu-id="3f601-222">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="3f601-223">4 </span><span class="sxs-lookup"><span data-stu-id="3f601-223">4</span></span>|<span data-ttu-id="3f601-224">**Cuadro de búsqueda:** permite a los usuarios encontrar el contenido de la aplicación que desean insertar.</span><span class="sxs-lookup"><span data-stu-id="3f601-224">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="3f601-225">5 </span><span class="sxs-lookup"><span data-stu-id="3f601-225">5</span></span>|<span data-ttu-id="3f601-226">**Menú Tab (opcional):** proporciona varias categorías de contenido.</span><span class="sxs-lookup"><span data-stu-id="3f601-226">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="3f601-227">6 </span><span class="sxs-lookup"><span data-stu-id="3f601-227">6</span></span>|<span data-ttu-id="3f601-228">**Menú Comandos de acción (opcional):** muestra una lista de comandos de acción (si especifica alguno).</span><span class="sxs-lookup"><span data-stu-id="3f601-228">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="3f601-229">7 </span><span class="sxs-lookup"><span data-stu-id="3f601-229">7</span></span>|<span data-ttu-id="3f601-230">**Contenido de la** aplicación: principalmente para mostrar los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="3f601-230">**App content**: Primarily to display search results.</span></span> <span data-ttu-id="3f601-231">El ejemplo aquí es usar el diseño de lista (el diseño de cuadrícula es otra opción).</span><span class="sxs-lookup"><span data-stu-id="3f601-231">The example here is using the list layout (grid layout is another option).</span></span>|
|<span data-ttu-id="3f601-232">8 </span><span class="sxs-lookup"><span data-stu-id="3f601-232">8</span></span>|<span data-ttu-id="3f601-233">**Logotipo de la** aplicación: icono de esquema del logotipo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3f601-233">**App logo**: Outline icon of your app logo.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="3f601-234">Móvil</span><span class="sxs-lookup"><span data-stu-id="3f601-234">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-anatomy-compose.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una extensión de mensajería en el cuadro de redacción del móvil." border="false":::

|<span data-ttu-id="3f601-236">Contador</span><span class="sxs-lookup"><span data-stu-id="3f601-236">Counter</span></span>|<span data-ttu-id="3f601-237">Descripción</span><span class="sxs-lookup"><span data-stu-id="3f601-237">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="3f601-238">1</span><span class="sxs-lookup"><span data-stu-id="3f601-238">1</span></span>|<span data-ttu-id="3f601-239">**Nombre de la** aplicación: nombre completo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3f601-239">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="3f601-240">2</span><span class="sxs-lookup"><span data-stu-id="3f601-240">2</span></span>|<span data-ttu-id="3f601-241">**Icono de menú Comandos de acción (opcional):** abre una lista de comandos de acción para la extensión de mensajería (si especifica alguno).</span><span class="sxs-lookup"><span data-stu-id="3f601-241">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="3f601-242">3</span><span class="sxs-lookup"><span data-stu-id="3f601-242">3</span></span>|<span data-ttu-id="3f601-243">**Cuadro de búsqueda:** permite a los usuarios encontrar el contenido de la aplicación que desean insertar.</span><span class="sxs-lookup"><span data-stu-id="3f601-243">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="3f601-244">4 </span><span class="sxs-lookup"><span data-stu-id="3f601-244">4</span></span>|<span data-ttu-id="3f601-245">**Menú Tab (opcional):** proporciona varias categorías de contenido.</span><span class="sxs-lookup"><span data-stu-id="3f601-245">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="3f601-246">5 </span><span class="sxs-lookup"><span data-stu-id="3f601-246">5</span></span>|<span data-ttu-id="3f601-247">**Menú Comandos de acción (opcional):** muestra una lista de comandos de acción (si especifica alguno).</span><span class="sxs-lookup"><span data-stu-id="3f601-247">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="3f601-248">6 </span><span class="sxs-lookup"><span data-stu-id="3f601-248">6</span></span>|<span data-ttu-id="3f601-249">**Contenido de la** aplicación: principalmente para mostrar los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="3f601-249">**App content**: Primarily to display search results.</span></span>|

---

### <a name="messaging-extension-management-menu"></a><span data-ttu-id="3f601-250">Menú administración de extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="3f601-250">Messaging extension management menu</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un menú de administración de extensiones de mensajería." border="false":::

|<span data-ttu-id="3f601-252">Contador</span><span class="sxs-lookup"><span data-stu-id="3f601-252">Counter</span></span>|<span data-ttu-id="3f601-253">Descripción</span><span class="sxs-lookup"><span data-stu-id="3f601-253">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="3f601-254">1</span><span class="sxs-lookup"><span data-stu-id="3f601-254">1</span></span>|<span data-ttu-id="3f601-255">**Desanclar:** disponible si el usuario ha anclado la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3f601-255">**Unpin**: Available if the user has pinned your app.</span></span>|
|<span data-ttu-id="3f601-256">2</span><span class="sxs-lookup"><span data-stu-id="3f601-256">2</span></span>|<span data-ttu-id="3f601-257">**Quitar:** quita la extensión de mensajería del canal, chat o reunión.</span><span class="sxs-lookup"><span data-stu-id="3f601-257">**Remove**: Removes the messaging extension from the channel, chat, or meeting.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="3f601-258">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="3f601-258">Best practices</span></span>

<span data-ttu-id="3f601-259">Usa estas recomendaciones para crear una experiencia de aplicación de calidad.</span><span class="sxs-lookup"><span data-stu-id="3f601-259">Use these recommendations to create a quality app experience.</span></span>

### <a name="setup-and-general-usage"></a><span data-ttu-id="3f601-260">Configuración y uso general</span><span class="sxs-lookup"><span data-stu-id="3f601-260">Setup and general usage</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="Ejemplo sobre configuración y uso general." border="false":::

#### <a name="do-integrate-with-single-sign-on"></a><span data-ttu-id="3f601-262">Hacer: integrar con el inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="3f601-262">Do: Integrate with single-sign on</span></span>

<span data-ttu-id="3f601-263">SSO hace que el proceso de inicio de sesión sea más fácil, rápido y seguro.</span><span class="sxs-lookup"><span data-stu-id="3f601-263">SSO makes the sign-in process easier, faster, and secure.</span></span> <span data-ttu-id="3f601-264">Además, si un usuario ya ha iniciado sesión en la aplicación personal, no tiene que volver a iniciar sesión para tener acceso a la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="3f601-264">Also, if a user has already signed in to your personal app, they don’t have to also sign in again to access the messaging extension.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="Ejemplo de integración con inicio de sesión único." border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a><span data-ttu-id="3f601-266">No: alejar a los usuarios de la conversación</span><span class="sxs-lookup"><span data-stu-id="3f601-266">Don't: Take users away from the conversation</span></span>

<span data-ttu-id="3f601-267">Las extensiones de mensajería son métodos abreviados que se supone reducen el cambio de contexto.</span><span class="sxs-lookup"><span data-stu-id="3f601-267">Messaging extensions are shortcuts that are supposed reduce context switching.</span></span> <span data-ttu-id="3f601-268">La extensión no debe, por ejemplo, dirigir a los usuarios a una página web fuera de Teams.</span><span class="sxs-lookup"><span data-stu-id="3f601-268">Your extension should not, for example, direct users to a webpage outside Teams.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a><span data-ttu-id="3f601-269">Hacer: Resaltar la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="3f601-269">Do: Highlight your messaging extension</span></span>

<span data-ttu-id="3f601-270">Las extensiones de mensajería no siempre son fáciles de encontrar.</span><span class="sxs-lookup"><span data-stu-id="3f601-270">Messaging extensions aren't always easy to find.</span></span> <span data-ttu-id="3f601-271">Incluye capturas de pantalla de cómo usarlo en la página de detalles de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3f601-271">Include screenshots of how to use it in your app details page.</span></span> <span data-ttu-id="3f601-272">Si la aplicación también incluye un bot, puedes incluir documentación de ayuda de extensión de mensajería en un recorrido de bienvenida del bot.</span><span class="sxs-lookup"><span data-stu-id="3f601-272">If your app also includes a bot, you can include messaging extension help documentation in a bot welcome tour.</span></span>

### <a name="templating"></a><span data-ttu-id="3f601-273">Templating</span><span class="sxs-lookup"><span data-stu-id="3f601-273">Templating</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="Ejemplo de templating." border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a><span data-ttu-id="3f601-275">Do: Let Teams handle some of the design work if possible</span><span class="sxs-lookup"><span data-stu-id="3f601-275">Do: Let Teams handle some of the design work if possible</span></span>

<span data-ttu-id="3f601-276">Si tiene sentido para los casos de uso, considere la posibilidad de crear una extensión de mensajería basada en búsquedas.</span><span class="sxs-lookup"><span data-stu-id="3f601-276">If it makes sense for your use cases, consider creating a search-based messaging extension.</span></span> <span data-ttu-id="3f601-277">Teams representa estos tipos de extensiones con tema y accesibilidad integrados.</span><span class="sxs-lookup"><span data-stu-id="3f601-277">Teams renders these types of extensions with built-in theming and accessibility.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="Ejemplo sobre cómo controlar el trabajo de diseño." border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a><span data-ttu-id="3f601-279">No: insertar toda la aplicación en un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="3f601-279">Don't: Embed your entire app in a task module</span></span>

<span data-ttu-id="3f601-280">Si la extensión de mensajería requiere comandos de acción, mantenga el módulo de tareas sencillo y muestre solo los componentes necesarios para completar la acción.</span><span class="sxs-lookup"><span data-stu-id="3f601-280">If your messaging extension requires action commands, keep the task module simple and display only the components required to complete the action.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="3f601-281">Creación de temas</span><span class="sxs-lookup"><span data-stu-id="3f601-281">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="Ejemplo en el uso de los mismos." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="3f601-283">Hacer: aprovechar las ventajas de Teams de color</span><span class="sxs-lookup"><span data-stu-id="3f601-283">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="3f601-284">Cada Teams tema tiene su propia combinación de colores.</span><span class="sxs-lookup"><span data-stu-id="3f601-284">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="3f601-285">Para controlar los cambios de tema automáticamente, usa <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">tokens de color (Fluent UI)</a> en el diseño.</span><span class="sxs-lookup"><span data-stu-id="3f601-285">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="Ejemplo en tokens de color." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="3f601-287">No: valores de color de código duro</span><span class="sxs-lookup"><span data-stu-id="3f601-287">Don't: Hard code color values</span></span>

<span data-ttu-id="3f601-288">Si no usas tokens Teams de color, tus diseños serán menos escalables y tendrán más tiempo para administrar.</span><span class="sxs-lookup"><span data-stu-id="3f601-288">If you don't use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="actions"></a><span data-ttu-id="3f601-289">Acciones</span><span class="sxs-lookup"><span data-stu-id="3f601-289">Actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="Ejemplo de acciones." border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a><span data-ttu-id="3f601-291">Hacer: incluir comandos de acción que tienen sentido en contexto</span><span class="sxs-lookup"><span data-stu-id="3f601-291">Do: Include action commands that make sense in context</span></span>

<span data-ttu-id="3f601-292">Las acciones del mensaje deben estar relacionadas con lo que un usuario está viendo.</span><span class="sxs-lookup"><span data-stu-id="3f601-292">Message actions should relate to what a user is looking at.</span></span> <span data-ttu-id="3f601-293">Por ejemplo, proporcione a los usuarios un acceso directo para crear un problema o elemento de trabajo con el texto de la publicación de alguien.</span><span class="sxs-lookup"><span data-stu-id="3f601-293">For example, provide users a shortcut for creating an issue or work item using the text in someone’s post.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="Ejemplo de comandos de acción." border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a><span data-ttu-id="3f601-295">No: incluir comandos de acciones que no son contextuales</span><span class="sxs-lookup"><span data-stu-id="3f601-295">Don't: Include actions commands that aren't contextual</span></span>

<span data-ttu-id="3f601-296">Una acción de mensaje **para ver el panel** probablemente parecería desconectada de la mayoría de las conversaciones.</span><span class="sxs-lookup"><span data-stu-id="3f601-296">A message action to **View your dashboard** would probably seem disconnected from most conversations.</span></span>

   :::column-end:::
:::row-end:::

### <a name="searches"></a><span data-ttu-id="3f601-297">Búsquedas</span><span class="sxs-lookup"><span data-stu-id="3f601-297">Searches</span></span>

#### <a name="do-show-search-results-while-typing"></a><span data-ttu-id="3f601-298">Hacer: mostrar resultados de búsqueda al escribir</span><span class="sxs-lookup"><span data-stu-id="3f601-298">Do: Show search results while typing</span></span>

<span data-ttu-id="3f601-299">Proporcionar resultados de búsqueda sugeridos mientras los usuarios escriben.</span><span class="sxs-lookup"><span data-stu-id="3f601-299">Provide suggested search results while users type.</span></span> <span data-ttu-id="3f601-300">Es posible que encuentren el contenido que necesitan más rápido con una cantidad mínima de caracteres.</span><span class="sxs-lookup"><span data-stu-id="3f601-300">They may find the content they need faster with minimal amount of characters.</span></span>

#### <a name="dont-require-users-to-submit-a-query"></a><span data-ttu-id="3f601-301">No: requerir que los usuarios envíen una consulta</span><span class="sxs-lookup"><span data-stu-id="3f601-301">Don't: Require users to submit a query</span></span>

<span data-ttu-id="3f601-302">Puedes hacer que los usuarios presionen una tecla o seleccione un botón para enviar consultas a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3f601-302">You can make users press a key or select a button to send queries to your app.</span></span> <span data-ttu-id="3f601-303">Aunque esto puede ser más fácil en el servicio de servicios de aplicaciones, es posible que los usuarios se confundan de que no ven resultados de búsqueda en tiempo real mientras escriben.</span><span class="sxs-lookup"><span data-stu-id="3f601-303">While that may be easier on your app services service, people may be confused that they're not seeing real-time search results as they type.</span></span>

#### <a name="do-consider-zero-term-queries"></a><span data-ttu-id="3f601-304">Do: Consider zero-term queries</span><span class="sxs-lookup"><span data-stu-id="3f601-304">Do: Consider zero-term queries</span></span>

<span data-ttu-id="3f601-305">Por ejemplo, antes de que un usuario escriba algo en el cuadro de búsqueda, muestre lo que ha visto por última vez en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3f601-305">For example, before a user writes anything in the search box, display what they last viewed on your app.</span></span> <span data-ttu-id="3f601-306">Es posible que quieran insertar ese contenido en su conversación.</span><span class="sxs-lookup"><span data-stu-id="3f601-306">It's possible that they want to insert that content into their conversation.</span></span>

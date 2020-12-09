---
title: Diseño de la extensión de mensajería
description: Obtenga información sobre cómo diseñar una extensión de mensajería de Teams y obtener el kit de interfaz de usuario de Microsoft Teams.
keywords: Directrices de diseño de Microsoft Teams referencia sugerencias de extensiones de mensajería procedimientos recomendados
author: heath-hamilton
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: ad628bdaa46058aed4acdcea1a224c7ebfe40f89
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604917"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a><span data-ttu-id="b99a1-104">Diseño de la extensión de mensajería de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b99a1-104">Designing your Microsoft Teams messaging extension</span></span>

<span data-ttu-id="b99a1-105">Las extensiones de mensajería son accesos directos para insertar contenido de aplicaciones o actuar en un mensaje sin navegar fuera de la conversación.</span><span class="sxs-lookup"><span data-stu-id="b99a1-105">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span>

<span data-ttu-id="b99a1-106">Para guiar el diseño de la aplicación, la siguiente información describe e ilustra cómo los usuarios pueden agregar, usar y administrar las extensiones de mensajería en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="b99a1-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage messaging extensions in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="b99a1-107">Kit de IU de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b99a1-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="b99a1-108">Puede encontrar instrucciones detalladas para el diseño de extensiones de mensajería, incluidos los elementos que puede captar y modificar según sea necesario, en el kit de interfaz de usuario de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="b99a1-108">You can find comprehensive messaging extension design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b99a1-109">Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="b99a1-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a><span data-ttu-id="b99a1-110">Agregar una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="b99a1-110">Add a messaging extension</span></span>

<span data-ttu-id="b99a1-111">Puede Agregar una extensión de mensajería en los siguientes contextos de Teams:</span><span class="sxs-lookup"><span data-stu-id="b99a1-111">You can add a messaging extension in the following Teams contexts:</span></span>

* <span data-ttu-id="b99a1-112">De la tienda Teams (AppSource).</span><span class="sxs-lookup"><span data-stu-id="b99a1-112">From the Teams store (AppSource).</span></span>
* <span data-ttu-id="b99a1-113">En un canal, un chat o una reunión (antes, durante y después) cerca del cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="b99a1-113">In a channel, chat, or meeting (before, during, and after) near the compose box.</span></span> <span data-ttu-id="b99a1-114">Merece la pena resaltar si agrega una extensión de mensajería en uno de estos lugares, solo puede usarla en ese contexto.</span><span class="sxs-lookup"><span data-stu-id="b99a1-114">It's worth noting if you add a messaging extension in one of these places, only you can use it in that context.</span></span>

<span data-ttu-id="b99a1-115">En el ejemplo siguiente se muestra cómo agregar una extensión de mensajería en un canal.</span><span class="sxs-lookup"><span data-stu-id="b99a1-115">The following example shows how you add a messaging extension in a channel.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de mensajería cerca del cuadro de redacción en un canal." border="false":::

## <a name="set-up-a-messaging-extension"></a><span data-ttu-id="b99a1-117">Configurar una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="b99a1-117">Set up a messaging extension</span></span>

<span data-ttu-id="b99a1-118">La autenticación no es obligatoria, pero si la aplicación es similar a una herramienta de seguimiento de vales, es posible que necesite que los usuarios inicien sesión para usar la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="b99a1-118">Authentication isn't mandatory, but if your app is something like a ticket tracking tool, you may need people to sign in to use the messaging extension.</span></span>

<span data-ttu-id="b99a1-119">Por coherencia entre las aplicaciones de Microsoft Teams, no se puede personalizar la pantalla de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="b99a1-119">For consistency across Teams apps, you can't customize the sign-in screen.</span></span> <span data-ttu-id="b99a1-120">Si usa la autenticación de inicio de sesión único (SSO), los usuarios inician sesión automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b99a1-120">If you use single sign-on (SSO) authentication, users are signed in automatically.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="Ejemplo muestra la pantalla de configuración de extensiones de mensajería con un botón de inicio de sesión." border="false":::

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="b99a1-122">Tipos de extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="b99a1-122">Types of messaging extensions</span></span>

<span data-ttu-id="b99a1-123">Las extensiones de mensajería pueden tener comandos de búsqueda, comandos de acción o ambos.</span><span class="sxs-lookup"><span data-stu-id="b99a1-123">Messaging extensions can have search commands, action commands, or both.</span></span> <span data-ttu-id="b99a1-124">Los comandos dependen de las características de la aplicación y de cómo se ajusten a los casos de uso de Teams.</span><span class="sxs-lookup"><span data-stu-id="b99a1-124">Your commands depend on your app's features and how those fit within Teams use cases.</span></span>

### <a name="search-commands"></a><span data-ttu-id="b99a1-125">Comandos de búsqueda</span><span class="sxs-lookup"><span data-stu-id="b99a1-125">Search commands</span></span>

<span data-ttu-id="b99a1-126">Con los comandos de búsqueda, los usuarios pueden usar su extensión de mensajería para encontrar rápidamente contenido externo e insertarlo en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="b99a1-126">With search commands, people can use your messaging extension to quickly find external content and insert into a message.</span></span> <span data-ttu-id="b99a1-127">Los comandos de búsqueda suelen estar disponibles en el cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="b99a1-127">Search commands are commonly made available in the compose box.</span></span> <span data-ttu-id="b99a1-128">Por ejemplo, puede empezar o agregar una discusión compartiendo una parte del contenido, sin dejar de tener los equipos.</span><span class="sxs-lookup"><span data-stu-id="b99a1-128">For example, you can start or add to a discussion by sharing a piece of content—without ever leaving Teams.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="Ejemplo muestra una extensión de mensajería basada en búsquedas iniciada desde el cuadro de redacción." border="false":::

#### <a name="compose-box-layout-options"></a><span data-ttu-id="b99a1-130">Opciones de diseño del cuadro de redacción</span><span class="sxs-lookup"><span data-stu-id="b99a1-130">Compose box layout options</span></span>

<span data-ttu-id="b99a1-131">Tiene algunas opciones para mostrar los resultados de la búsqueda de extensiones de mensajería, incluidas las [vistas de lista y cuadrícula](../../messaging-Ask about extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span><span class="sxs-lookup"><span data-stu-id="b99a1-131">You have some options for displaying messaging extension search results, including [list and grid views](../../messaging-Ask about extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="Ilustraciones que muestran las opciones de diseño para los resultados de la búsqueda de extensiones de mensajería." border="false":::

### <a name="action-commands"></a><span data-ttu-id="b99a1-133">Comandos de acción</span><span class="sxs-lookup"><span data-stu-id="b99a1-133">Action commands</span></span>

<span data-ttu-id="b99a1-134">Los comandos de acción permiten a los usuarios desencadenar acciones y procesar solicitudes en servicios externos dentro de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="b99a1-134">Action commands allow people to trigger actions and process requests in external services within Teams.</span></span> <span data-ttu-id="b99a1-135">Por ejemplo, si la aplicación realiza un seguimiento de pedidos, un usuario puede crear un nuevo pedido con el contenido de un mensaje de un colega desde el interior de su chat.</span><span class="sxs-lookup"><span data-stu-id="b99a1-135">For example, if your app tracks orders, a user could create a new order using the contents of a colleague’s message from right inside their chat.</span></span>

<span data-ttu-id="b99a1-136">Las extensiones de mensajería basadas en acciones suelen requerir que los usuarios completen un formulario o algún otro tipo de configuración dentro de un modal.</span><span class="sxs-lookup"><span data-stu-id="b99a1-136">Action-based messaging extensions frequently require users to complete a form or some other kind of configuration within a modal.</span></span> <span data-ttu-id="b99a1-137">Puede crear estas experiencias con [módulos de tareas](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span><span class="sxs-lookup"><span data-stu-id="b99a1-137">You can create these experiences with [task modules](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="open-a-messaging-extension"></a><span data-ttu-id="b99a1-138">Abrir una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="b99a1-138">Open a messaging extension</span></span>

<span data-ttu-id="b99a1-139">El cuadro de redacción y los mensajes/publicaciones son los contextos principales en los que los usuarios usan extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="b99a1-139">The compose box and messages/posts are the primary contexts where people use messaging extensions.</span></span>

### <a name="from-the-compose-box"></a><span data-ttu-id="b99a1-140">Desde el cuadro de redacción</span><span class="sxs-lookup"><span data-stu-id="b99a1-140">From the compose box</span></span>

<span data-ttu-id="b99a1-141">Una vez agregados, los usuarios pueden abrir la extensión de mensajería seleccionando el icono de la aplicación debajo del cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="b99a1-141">Once added, users can open your messaging extension by selecting your app icon below the compose box.</span></span> <span data-ttu-id="b99a1-142">En este ejemplo, la extensión tiene los comandos de búsqueda y de acción.</span><span class="sxs-lookup"><span data-stu-id="b99a1-142">In this example, the extension has search and action commands.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="En el ejemplo se muestra cómo abrir una extensión de mensajería desde el cuadro de redacción." border="false":::

### <a name="from-a-chat-message-or-channel-post"></a><span data-ttu-id="b99a1-144">Desde un mensaje de chat o una publicación de canal</span><span class="sxs-lookup"><span data-stu-id="b99a1-144">From a chat message or channel post</span></span>

Una vez agregados, los usuarios pueden seleccionar el icono **más** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: en el mensaje de chat o la entrada de canal para buscar los comandos de acción de la extensión. <span data-ttu-id="b99a1-146">La extensión puede aparecer en **más acciones** en función del uso.</span><span class="sxs-lookup"><span data-stu-id="b99a1-146">Your extension may be listed under **More actions** based on usage.</span></span>

#### <a name="chat-message"></a><span data-ttu-id="b99a1-147">Mensaje de chat</span><span class="sxs-lookup"><span data-stu-id="b99a1-147">Chat message</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="En este ejemplo, se muestra cómo abrir una extensión de mensajería desde un mensaje de chat." border="false":::

#### <a name="channel-post"></a><span data-ttu-id="b99a1-149">Entrada de canal</span><span class="sxs-lookup"><span data-stu-id="b99a1-149">Channel post</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="En este ejemplo, se muestra cómo abrir una extensión de mensajería desde una publicación de canal." border="false":::

## <a name="use-a-messaging-extension"></a><span data-ttu-id="b99a1-151">Usar una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="b99a1-151">Use a messaging extension</span></span>

<span data-ttu-id="b99a1-152">Los siguientes escenarios muestran las principales formas en las que los usuarios usan las extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="b99a1-152">The following scenarios show the primary ways people use messaging extensions.</span></span>

### <a name="insert-content-into-a-message"></a><span data-ttu-id="b99a1-153">Insertar contenido en un mensaje</span><span class="sxs-lookup"><span data-stu-id="b99a1-153">Insert content into a message</span></span>

<span data-ttu-id="b99a1-154">**1. Seleccione una extensión de mensajería**.</span><span class="sxs-lookup"><span data-stu-id="b99a1-154">**1. Select a messaging extension**.</span></span> <span data-ttu-id="b99a1-155">Los usuarios pueden buscar el contenido que desean compartir desde el cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="b99a1-155">Users can search for the content they want to share from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="Ejemplo muestra un usuario que busca contenido para insertar desde el cuadro de redacción." border="false":::

<span data-ttu-id="b99a1-157">**2. Insertar contenido**.</span><span class="sxs-lookup"><span data-stu-id="b99a1-157">**2. Insert content**.</span></span> <span data-ttu-id="b99a1-158">Una vez publicada, otros usuarios pueden responder o seleccionar el contenido para ver más información en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b99a1-158">Once posted, others can reply or select the content to see more information in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="Ejemplo muestra un contenido de envío de usuario a una conversación de canal." border="false":::

### <a name="take-action-on-a-message"></a><span data-ttu-id="b99a1-160">Realizar acciones en un mensaje</span><span class="sxs-lookup"><span data-stu-id="b99a1-160">Take action on a message</span></span>

<span data-ttu-id="b99a1-161">**1. Seleccione una extensión de mensajería**.</span><span class="sxs-lookup"><span data-stu-id="b99a1-161">**1. Select a messaging extension**.</span></span> <span data-ttu-id="b99a1-162">La aplicación puede incluir uno o varios comandos de acción.</span><span class="sxs-lookup"><span data-stu-id="b99a1-162">Your app can include one or more action commands.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="Ejemplo muestra un usuario seleccionando un comando de acción de extensión de mensajería." border="false":::

<span data-ttu-id="b99a1-164">**2. Complete la acción**.</span><span class="sxs-lookup"><span data-stu-id="b99a1-164">**2. Complete the action**.</span></span> <span data-ttu-id="b99a1-165">La aplicación puede recibir y procesar cualquier contenido o datos enviados por la acción del mensaje.</span><span class="sxs-lookup"><span data-stu-id="b99a1-165">Your app can receive and process any content or data sent by the message action.</span></span> <span data-ttu-id="b99a1-166">Esto permite a los usuarios permanecer en su conversación y, en el siguiente ejemplo, no se preocupe de escribir información directamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b99a1-166">This allows users to remain in their conversation and, the following example, not worry about entering information directly in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="Ejemplo muestra un usuario que busca contenido para insertar desde el cuadro de redacción." border="false":::

### <a name="preview-links"></a><span data-ttu-id="b99a1-168">Vista previa de vínculos</span><span class="sxs-lookup"><span data-stu-id="b99a1-168">Preview links</span></span>

<span data-ttu-id="b99a1-169">Las extensiones de mensajería también permiten insertar vínculos enriquecidos desde una dirección URL reconocida en un mensaje (esta capacidad se denomina [vínculo unfurling](../../messaging-extensions/how-to/link-unfurling.md)).</span><span class="sxs-lookup"><span data-stu-id="b99a1-169">Messaging extensions also allow you to insert rich links from a recognized URL into a message (this capability is called [link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)</span></span>

<span data-ttu-id="b99a1-170">**1. Pegue un vínculo reconocido** en el cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="b99a1-170">**1. Paste a recognized link** in the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="Ejemplo muestra un usuario que pega un vínculo en el cuadro compost." border="false":::

<span data-ttu-id="b99a1-172">**2. Insertar contenido**.</span><span class="sxs-lookup"><span data-stu-id="b99a1-172">**2. Insert content**.</span></span> <span data-ttu-id="b99a1-173">Si la aplicación reconoce la dirección URL en el cuadro de redacción, representa el vínculo como una tarjeta que proporciona una vista previa de contenido enriquecido del contenido Web.</span><span class="sxs-lookup"><span data-stu-id="b99a1-173">If your app recognizes the URL in the compose box, it renders the link as a card that provides a content-rich preview of the web content.</span></span> <span data-ttu-id="b99a1-174">(Vea [directrices de diseño de tarjetas adaptables](../../task-modules-and-cards/cards/design-effective-cards.md) para obtener más información).</span><span class="sxs-lookup"><span data-stu-id="b99a1-174">(See [Adaptive Cards design guidelines](../../task-modules-and-cards/cards/design-effective-cards.md) for more information.)</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="En el ejemplo se muestra el modo en que la dirección URL, ya que la aplicación la reconoce, incluye contenido enriquecido en el cuadro de redacción." border="false":::

## <a name="manage-a-messaging-extension"></a><span data-ttu-id="b99a1-176">Administrar una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="b99a1-176">Manage a messaging extension</span></span>

<span data-ttu-id="b99a1-177">Al hacer clic con el botón secundario en el icono, los usuarios pueden anclar, quitar o configurar su extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="b99a1-177">By right clicking your icon, users can pin, remove, or configure your messaging extension.</span></span>

## <a name="anatomy"></a><span data-ttu-id="b99a1-178">Anatomía</span><span class="sxs-lookup"><span data-stu-id="b99a1-178">Anatomy</span></span>

### <a name="messaging-extension-in-the-compose-box"></a><span data-ttu-id="b99a1-179">Extensión de mensajería en el cuadro de redacción</span><span class="sxs-lookup"><span data-stu-id="b99a1-179">Messaging extension in the compose box</span></span>

<span data-ttu-id="b99a1-180">El siguiente ejemplo es una extensión de mensajería abierta desde el cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="b99a1-180">The following example is a messaging extension opened from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una extensión de mensajería en el cuadro de redacción." border="false":::

|<span data-ttu-id="b99a1-182">Counter</span><span class="sxs-lookup"><span data-stu-id="b99a1-182">Counter</span></span>|<span data-ttu-id="b99a1-183">Descripción</span><span class="sxs-lookup"><span data-stu-id="b99a1-183">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b99a1-184">1</span><span class="sxs-lookup"><span data-stu-id="b99a1-184">1</span></span>|<span data-ttu-id="b99a1-185">**Logotipo** de la aplicación: icono de color del logotipo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b99a1-185">**App logo**: Color icon of your app logo.</span></span>|
|<span data-ttu-id="b99a1-186">2 </span><span class="sxs-lookup"><span data-stu-id="b99a1-186">2</span></span>|<span data-ttu-id="b99a1-187">**Nombre** de la aplicación: nombre completo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b99a1-187">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="b99a1-188">3 </span><span class="sxs-lookup"><span data-stu-id="b99a1-188">3</span></span>|<span data-ttu-id="b99a1-189">**Icono de menú comandos de acción (opcional)**: abre una lista de comandos de acción para la extensión de mensajería (si se especifica alguno).</span><span class="sxs-lookup"><span data-stu-id="b99a1-189">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="b99a1-190">4 </span><span class="sxs-lookup"><span data-stu-id="b99a1-190">4</span></span>|<span data-ttu-id="b99a1-191">**Cuadro de búsqueda**: permite a los usuarios buscar el contenido de la aplicación que quiera insertar.</span><span class="sxs-lookup"><span data-stu-id="b99a1-191">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="b99a1-192">5 </span><span class="sxs-lookup"><span data-stu-id="b99a1-192">5</span></span>|<span data-ttu-id="b99a1-193">**Menú de pestaña (opcional)**: proporciona varias categorías de contenido.</span><span class="sxs-lookup"><span data-stu-id="b99a1-193">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="b99a1-194">6 </span><span class="sxs-lookup"><span data-stu-id="b99a1-194">6</span></span>|<span data-ttu-id="b99a1-195">**Menú de comandos de acción (opcional)**: muestra la lista de comandos de acción (si especifica alguno).</span><span class="sxs-lookup"><span data-stu-id="b99a1-195">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="b99a1-196">7 </span><span class="sxs-lookup"><span data-stu-id="b99a1-196">7</span></span>|<span data-ttu-id="b99a1-197">**Contenido** de la aplicación: principalmente para mostrar los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="b99a1-197">**App content**: Primarily to display search results.</span></span> <span data-ttu-id="b99a1-198">El ejemplo que se muestra aquí está usando el diseño de lista (el diseño de cuadrícula es otra opción).</span><span class="sxs-lookup"><span data-stu-id="b99a1-198">The example here is using the list layout (grid layout is another option).</span></span>|
|<span data-ttu-id="b99a1-199">8 </span><span class="sxs-lookup"><span data-stu-id="b99a1-199">8</span></span>|<span data-ttu-id="b99a1-200">**Logotipo** de la aplicación: icono de esquema del logotipo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b99a1-200">**App logo**: Outline icon of your app logo.</span></span>|

### <a name="messaging-extension-management-menu"></a><span data-ttu-id="b99a1-201">Menú de administración de extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="b99a1-201">Messaging extension management menu</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un menú de administración de extensiones de mensajería." border="false":::

|<span data-ttu-id="b99a1-203">Counter</span><span class="sxs-lookup"><span data-stu-id="b99a1-203">Counter</span></span>|<span data-ttu-id="b99a1-204">Descripción</span><span class="sxs-lookup"><span data-stu-id="b99a1-204">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b99a1-205">1</span><span class="sxs-lookup"><span data-stu-id="b99a1-205">1</span></span>|<span data-ttu-id="b99a1-206">**Desanclar**: disponible si el usuario ha anclado la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b99a1-206">**Unpin**: Available if the user has pinned your app.</span></span>|
|<span data-ttu-id="b99a1-207">2 </span><span class="sxs-lookup"><span data-stu-id="b99a1-207">2</span></span>|<span data-ttu-id="b99a1-208">**Quitar**: quita la extensión de mensajería del canal, el chat o la reunión.</span><span class="sxs-lookup"><span data-stu-id="b99a1-208">**Remove**: Removes the messaging extension from the channel, chat, or meeting.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="b99a1-209">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="b99a1-209">Best practices</span></span>

### <a name="setup-and-general-usage"></a><span data-ttu-id="b99a1-210">Configuración y uso general</span><span class="sxs-lookup"><span data-stu-id="b99a1-210">Setup and general usage</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de mensajería." border="false":::

#### <a name="do-integrate-with-single-sign-on"></a><span data-ttu-id="b99a1-212">Do: integrar con inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="b99a1-212">Do: Integrate with single-sign on</span></span>

<span data-ttu-id="b99a1-213">SSO hace que el proceso de inicio de sesión sea más fácil, rápido y seguro.</span><span class="sxs-lookup"><span data-stu-id="b99a1-213">SSO makes the sign-in process easier, faster, and secure.</span></span> <span data-ttu-id="b99a1-214">Además, si un usuario ya ha iniciado sesión en su aplicación personal, tampoco tendrá que volver a iniciar sesión para obtener acceso a la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="b99a1-214">Also, if a user has already signed in to your personal app, they don’t have to also sign in again to access the messaging extension.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de mensajería." border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a><span data-ttu-id="b99a1-216">No: alejar a los usuarios de la conversación</span><span class="sxs-lookup"><span data-stu-id="b99a1-216">Don't: Take users away from the conversation</span></span>

<span data-ttu-id="b99a1-217">Las extensiones de mensajería son accesos directos que se supone que reducen el cambio de contexto.</span><span class="sxs-lookup"><span data-stu-id="b99a1-217">Messaging extensions are shortcuts that are supposed reduce context switching.</span></span> <span data-ttu-id="b99a1-218">Por ejemplo, la extensión no debe dirigir a los usuarios a una página web fuera de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="b99a1-218">Your extension should not, for example, direct users to a webpage outside Teams.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a><span data-ttu-id="b99a1-219">Haga lo siguiente: resalte su extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="b99a1-219">Do: Highlight your messaging extension</span></span>

<span data-ttu-id="b99a1-220">Las extensiones de mensajería no siempre son fáciles de encontrar.</span><span class="sxs-lookup"><span data-stu-id="b99a1-220">Messaging extensions aren't always easy to find.</span></span> <span data-ttu-id="b99a1-221">Incluya capturas de pantallas sobre cómo usarla en la página de detalles de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b99a1-221">Include screenshots of how to use it in your app details page.</span></span> <span data-ttu-id="b99a1-222">Si la aplicación también incluye un bot, puede incluir la documentación de la ayuda de la extensión de mensajería en un paseo de bienvenida de bot.</span><span class="sxs-lookup"><span data-stu-id="b99a1-222">If your app also includes a bot, you can include messaging extension help documentation in a bot welcome tour.</span></span>

### <a name="templating"></a><span data-ttu-id="b99a1-223">Contempla</span><span class="sxs-lookup"><span data-stu-id="b99a1-223">Templating</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de mensajería." border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a><span data-ttu-id="b99a1-225">Do: permitir que Microsoft Teams administre algunos de los trabajos de diseño si es posible</span><span class="sxs-lookup"><span data-stu-id="b99a1-225">Do: Let Teams handle some of the design work if possible</span></span>

<span data-ttu-id="b99a1-226">Si tiene sentido para los casos de uso, considere la posibilidad de crear una extensión de mensajería basada en búsquedas.</span><span class="sxs-lookup"><span data-stu-id="b99a1-226">If it makes sense for your use cases, consider creating a search-based messaging extension.</span></span> <span data-ttu-id="b99a1-227">Teams representa estos tipos de extensiones con temas y accesibilidad integrados.</span><span class="sxs-lookup"><span data-stu-id="b99a1-227">Teams renders these types of extensions with built-in theming and accessibility.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de mensajería." border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a><span data-ttu-id="b99a1-229">No: incruste toda la aplicación en un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="b99a1-229">Don't: Embed your entire app in a task module</span></span>

<span data-ttu-id="b99a1-230">Si su extensión de mensajería requiere comandos de acción, mantenga el módulo de tareas sencillo y muestre sólo los componentes necesarios para completar la acción.</span><span class="sxs-lookup"><span data-stu-id="b99a1-230">If your messaging extension requires action commands, keep the task module simple and display only the components required to complete the action.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="b99a1-231">Creación de temas</span><span class="sxs-lookup"><span data-stu-id="b99a1-231">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de mensajería." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="b99a1-233">Do: aprovechar las ventajas de los tokens de color de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b99a1-233">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="b99a1-234">Cada tema de Teams tiene su propia combinación de colores.</span><span class="sxs-lookup"><span data-stu-id="b99a1-234">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="b99a1-235">Para controlar automáticamente los cambios de tema, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">tokens de color (interfaz de usuario de Fluent)</a> en el diseño.</span><span class="sxs-lookup"><span data-stu-id="b99a1-235">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de mensajería." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="b99a1-237">No: valores de color de código duro</span><span class="sxs-lookup"><span data-stu-id="b99a1-237">Don't: Hard code color values</span></span>

<span data-ttu-id="b99a1-238">Si no usa los tokens de color de Teams, los diseños serán menos escalables y tendrán más tiempo para administrarlos.</span><span class="sxs-lookup"><span data-stu-id="b99a1-238">If you don't use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="actions"></a><span data-ttu-id="b99a1-239">Acciones</span><span class="sxs-lookup"><span data-stu-id="b99a1-239">Actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de mensajería." border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a><span data-ttu-id="b99a1-241">Do: incluir comandos de acción que tienen sentido en el contexto</span><span class="sxs-lookup"><span data-stu-id="b99a1-241">Do: Include action commands that make sense in context</span></span>

<span data-ttu-id="b99a1-242">Las acciones del mensaje deben estar relacionadas con lo que el usuario está viendo.</span><span class="sxs-lookup"><span data-stu-id="b99a1-242">Message actions should relate to what a user is looking at.</span></span> <span data-ttu-id="b99a1-243">Por ejemplo, proporcione a los usuarios un acceso directo para crear un problema o elemento de trabajo mediante el texto de la publicación de alguien.</span><span class="sxs-lookup"><span data-stu-id="b99a1-243">For example, provide users a shortcut for creating an issue or work item using the text in someone’s post.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de extensión de mensajería." border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a><span data-ttu-id="b99a1-245">No: incluir comandos de acciones que no contengan contextuales</span><span class="sxs-lookup"><span data-stu-id="b99a1-245">Don't: Include actions commands that aren't contextual</span></span>

<span data-ttu-id="b99a1-246">Es probable que una acción de mensaje para **ver el panel** parezca desconectada de la mayoría de las conversaciones.</span><span class="sxs-lookup"><span data-stu-id="b99a1-246">A message action to **View your dashboard** would probably seem disconnected from most conversations.</span></span>

   :::column-end:::
:::row-end:::

### <a name="searches"></a><span data-ttu-id="b99a1-247">Buscar</span><span class="sxs-lookup"><span data-stu-id="b99a1-247">Searches</span></span>

#### <a name="do-show-search-results-while-typing"></a><span data-ttu-id="b99a1-248">Do: mostrar los resultados de la búsqueda al escribir</span><span class="sxs-lookup"><span data-stu-id="b99a1-248">Do: Show search results while typing</span></span>

<span data-ttu-id="b99a1-249">Proporcionar resultados de búsqueda sugeridos mientras los usuarios escriben.</span><span class="sxs-lookup"><span data-stu-id="b99a1-249">Provide suggested search results while users type.</span></span> <span data-ttu-id="b99a1-250">Es posible que encuentren el contenido que necesitan más rápidamente con una cantidad de caracteres mínima.</span><span class="sxs-lookup"><span data-stu-id="b99a1-250">They may find the content they need faster with minimal amount of characters.</span></span>

#### <a name="dont-require-users-to-submit-a-query"></a><span data-ttu-id="b99a1-251">No: requerir que los usuarios envíen una consulta</span><span class="sxs-lookup"><span data-stu-id="b99a1-251">Don't: Require users to submit a query</span></span>

<span data-ttu-id="b99a1-252">Puede hacer que los usuarios presionen una tecla o seleccionar un botón para enviar consultas a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b99a1-252">You can make users press a key or select a button to send queries to your app.</span></span> <span data-ttu-id="b99a1-253">Aunque es posible que sea más fácil en el servicio de servicios de la aplicación, se puede confundir a los usuarios que no ven los resultados de la búsqueda en tiempo real a medida que escriben.</span><span class="sxs-lookup"><span data-stu-id="b99a1-253">While that may be easier on your app services service, people may be confused that they're not seeing real-time search results as they type.</span></span>

#### <a name="do-consider-zero-term-queries"></a><span data-ttu-id="b99a1-254">Do: considerar consultas a cero términos</span><span class="sxs-lookup"><span data-stu-id="b99a1-254">Do: Consider zero-term queries</span></span>

<span data-ttu-id="b99a1-255">Por ejemplo, antes de que un usuario escriba algo en el cuadro de búsqueda, mostrar lo que se vio por última vez en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b99a1-255">For example, before a user writes anything in the search box, display what they last viewed on your app.</span></span> <span data-ttu-id="b99a1-256">Es posible que quieran insertar ese contenido en la conversación.</span><span class="sxs-lookup"><span data-stu-id="b99a1-256">It's possible that they want to insert that content into their conversation.</span></span>

## <a name="validate-your-design"></a><span data-ttu-id="b99a1-257">Validar el diseño</span><span class="sxs-lookup"><span data-stu-id="b99a1-257">Validate your design</span></span>

<span data-ttu-id="b99a1-258">Si planea publicar la aplicación en AppSource, debe comprender los problemas de diseño que suelen hacer que las aplicaciones fallen durante el envío.</span><span class="sxs-lookup"><span data-stu-id="b99a1-258">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b99a1-259">Comprobar las instrucciones de validación del diseño</span><span class="sxs-lookup"><span data-stu-id="b99a1-259">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)

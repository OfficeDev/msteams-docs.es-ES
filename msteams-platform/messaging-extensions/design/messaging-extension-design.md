---
title: Diseño de la extensión de mensajería
description: Aprende a diseñar una extensión de mensajería de Teams y a obtener el Kit de interfaz de usuario de Microsoft Teams.
keywords: Recomendaciones sobre extensiones de mensajería de referencia de directrices de diseño de teams
author: heath-hamilton
localization_priority: Normal
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: e3e4197e461f6d13f0c45ba2ce8bfb93b01b5e0f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020726"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a><span data-ttu-id="c607d-104">Diseño de la extensión de mensajería de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c607d-104">Designing your Microsoft Teams messaging extension</span></span>

<span data-ttu-id="c607d-105">Las extensiones de mensajería son métodos abreviados para insertar contenido de la aplicación o actuar en un mensaje sin salir de la conversación.</span><span class="sxs-lookup"><span data-stu-id="c607d-105">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span>
<span data-ttu-id="c607d-106">Para guiar el diseño de la aplicación, la siguiente información describe e ilustra cómo los usuarios pueden agregar, usar y administrar extensiones de mensajería en Teams.</span><span class="sxs-lookup"><span data-stu-id="c607d-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage messaging extensions in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="c607d-107">Kit de UI de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c607d-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="c607d-108">Puedes encontrar instrucciones completas de diseño de extensión de mensajería, incluidos los elementos que puedes agarrar y modificar según sea necesario, en el Kit de interfaz de usuario de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c607d-108">You can find comprehensive messaging extension design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c607d-109">Obtener el Kit de UI de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="c607d-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a><span data-ttu-id="c607d-110">Agregar una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="c607d-110">Add a messaging extension</span></span>

<span data-ttu-id="c607d-111">Puede agregar una extensión de mensajería en los siguientes contextos de Teams:</span><span class="sxs-lookup"><span data-stu-id="c607d-111">You can add a messaging extension in the following Teams contexts:</span></span>

* <span data-ttu-id="c607d-112">En la tienda de Teams (AppSource)</span><span class="sxs-lookup"><span data-stu-id="c607d-112">From the Teams store (AppSource).</span></span>
* <span data-ttu-id="c607d-113">En un canal, chat o reunión (antes, durante y después) cerca del cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="c607d-113">In a channel, chat, or meeting (before, during, and after) near the compose box.</span></span> <span data-ttu-id="c607d-114">Vale la pena tener en cuenta que si agregas una extensión de mensajería en uno de estos lugares, solo puedes usarla en ese contexto.</span><span class="sxs-lookup"><span data-stu-id="c607d-114">It's worth noting if you add a messaging extension in one of these places, only you can use it in that context.</span></span>

<span data-ttu-id="c607d-115">En el ejemplo siguiente se muestra cómo agregar una extensión de mensajería en un canal.</span><span class="sxs-lookup"><span data-stu-id="c607d-115">The following example shows how you add a messaging extension in a channel.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de mensajería cerca del cuadro de redacción de un canal." border="false":::

## <a name="set-up-a-messaging-extension"></a><span data-ttu-id="c607d-117">Configurar una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="c607d-117">Set up a messaging extension</span></span>

<span data-ttu-id="c607d-118">La autenticación no es obligatoria, pero si la aplicación es algo parecido a una herramienta de seguimiento de vales, es posible que necesites que las personas inicien sesión para usar la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="c607d-118">Authentication isn't mandatory, but if your app is something like a ticket tracking tool, you may need people to sign in to use the messaging extension.</span></span>

<span data-ttu-id="c607d-119">Para obtener coherencia en todas las aplicaciones de Teams, no puedes personalizar la pantalla de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="c607d-119">For consistency across Teams apps, you can't customize the sign-in screen.</span></span> <span data-ttu-id="c607d-120">Si usa la autenticación de inicio de sesión único (SSO), los usuarios iniciarán sesión automáticamente.</span><span class="sxs-lookup"><span data-stu-id="c607d-120">If you use single sign-on (SSO) authentication, users are signed in automatically.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="En el ejemplo se muestra la pantalla de configuración de extensión de mensajería con un botón de inicio de sesión." border="false":::

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="c607d-122">Tipos de extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="c607d-122">Types of messaging extensions</span></span>

<span data-ttu-id="c607d-123">Las extensiones de mensajería pueden tener comandos de búsqueda, comandos de acción o ambos.</span><span class="sxs-lookup"><span data-stu-id="c607d-123">Messaging extensions can have search commands, action commands, or both.</span></span> <span data-ttu-id="c607d-124">Los comandos dependen de las características de la aplicación y de cómo se ajustan a los casos de uso de Teams.</span><span class="sxs-lookup"><span data-stu-id="c607d-124">Your commands depend on your app's features and how those fit within Teams use cases.</span></span>

### <a name="search-commands"></a><span data-ttu-id="c607d-125">Comandos de búsqueda</span><span class="sxs-lookup"><span data-stu-id="c607d-125">Search commands</span></span>

<span data-ttu-id="c607d-126">Con los comandos de búsqueda, los usuarios pueden usar la extensión de mensajería para buscar rápidamente contenido externo e insertarlo en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="c607d-126">With search commands, people can use your messaging extension to quickly find external content and insert into a message.</span></span> <span data-ttu-id="c607d-127">Los comandos de búsqueda normalmente están disponibles en el cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="c607d-127">Search commands are commonly made available in the compose box.</span></span> <span data-ttu-id="c607d-128">Por ejemplo, puede iniciar o agregar a una discusión compartiendo un fragmento de contenido, sin salir nunca de Teams.</span><span class="sxs-lookup"><span data-stu-id="c607d-128">For example, you can start or add to a discussion by sharing a piece of content—without ever leaving Teams.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="En el ejemplo se muestra una extensión de mensajería basada en búsqueda iniciada desde el cuadro de redacción." border="false":::

#### <a name="compose-box-layout-options"></a><span data-ttu-id="c607d-130">Opciones de diseño de cuadro de redacción</span><span class="sxs-lookup"><span data-stu-id="c607d-130">Compose box layout options</span></span>

<span data-ttu-id="c607d-131">Tiene algunas opciones para mostrar los resultados de búsqueda de extensión de mensajería, incluidas [las vistas de lista y cuadrícula.](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)</span><span class="sxs-lookup"><span data-stu-id="c607d-131">You have some options for displaying messaging extension search results, including [list and grid views](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="Ilustraciones que muestran las opciones de diseño para los resultados de búsqueda de extensión de mensajería." border="false":::

### <a name="action-commands"></a><span data-ttu-id="c607d-133">Comandos de acción</span><span class="sxs-lookup"><span data-stu-id="c607d-133">Action commands</span></span>

<span data-ttu-id="c607d-134">Los comandos de acción permiten a los usuarios desencadenar acciones y procesar solicitudes en servicios externos dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="c607d-134">Action commands allow people to trigger actions and process requests in external services within Teams.</span></span> <span data-ttu-id="c607d-135">Por ejemplo, si la aplicación realiza un seguimiento de los pedidos, un usuario podría crear un nuevo pedido con el contenido del mensaje de un compañero desde el chat.</span><span class="sxs-lookup"><span data-stu-id="c607d-135">For example, if your app tracks orders, a user could create a new order using the contents of a colleague’s message from right inside their chat.</span></span>

<span data-ttu-id="c607d-136">Con frecuencia, las extensiones de mensajería basadas en acciones requieren que los usuarios completen un formulario o algún otro tipo de configuración dentro de un modal.</span><span class="sxs-lookup"><span data-stu-id="c607d-136">Action-based messaging extensions frequently require users to complete a form or some other kind of configuration within a modal.</span></span> <span data-ttu-id="c607d-137">Puede crear estas experiencias con [módulos de tareas](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span><span class="sxs-lookup"><span data-stu-id="c607d-137">You can create these experiences with [task modules](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="open-a-messaging-extension"></a><span data-ttu-id="c607d-138">Abrir una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="c607d-138">Open a messaging extension</span></span>

<span data-ttu-id="c607d-139">El cuadro de redacción y los mensajes/publicaciones son los contextos principales donde los usuarios usan extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="c607d-139">The compose box and messages/posts are the primary contexts where people use messaging extensions.</span></span>

### <a name="from-the-compose-box"></a><span data-ttu-id="c607d-140">Desde el cuadro de redacción</span><span class="sxs-lookup"><span data-stu-id="c607d-140">From the compose box</span></span>

<span data-ttu-id="c607d-141">Una vez agregado, los usuarios pueden abrir la extensión de mensajería seleccionando el icono de la aplicación debajo del cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="c607d-141">Once added, users can open your messaging extension by selecting your app icon below the compose box.</span></span> <span data-ttu-id="c607d-142">En este ejemplo, la extensión tiene comandos de búsqueda y acción.</span><span class="sxs-lookup"><span data-stu-id="c607d-142">In this example, the extension has search and action commands.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="En el ejemplo se muestra cómo abrir una extensión de mensajería desde el cuadro de redacción." border="false":::

### <a name="from-a-chat-message-or-channel-post"></a><span data-ttu-id="c607d-144">Desde un mensaje de chat o una publicación de canal</span><span class="sxs-lookup"><span data-stu-id="c607d-144">From a chat message or channel post</span></span>

Una vez agregado, los usuarios pueden seleccionar el icono **Más** en el mensaje de chat o la publicación del canal para buscar los comandos de acción :::image type="icon" source="../../assets/icons/teams-client-more.png"::: de la extensión. <span data-ttu-id="c607d-146">La extensión puede aparecer en **Más acciones basadas** en el uso.</span><span class="sxs-lookup"><span data-stu-id="c607d-146">Your extension may be listed under **More actions** based on usage.</span></span>

> [!NOTE]
> <span data-ttu-id="c607d-147">La compatibilidad con más acciones de un mensaje de chat o una publicación de canal no está disponible en la plataforma móvil de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c607d-147">Support for more actions from a chat message or channel post is not available on Microsoft Teams mobile platform.</span></span> 

#### <a name="chat-message"></a><span data-ttu-id="c607d-148">Mensaje de chat</span><span class="sxs-lookup"><span data-stu-id="c607d-148">Chat message</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="En el ejemplo se muestra cómo abrir una extensión de mensajería desde un mensaje de chat." border="false":::

#### <a name="channel-post"></a><span data-ttu-id="c607d-150">Publicación del canal</span><span class="sxs-lookup"><span data-stu-id="c607d-150">Channel post</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="En el ejemplo se muestra cómo abrir una extensión de mensajería desde una publicación de canal." border="false":::

## <a name="use-a-messaging-extension"></a><span data-ttu-id="c607d-152">Usar una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="c607d-152">Use a messaging extension</span></span>

<span data-ttu-id="c607d-153">En los siguientes escenarios se muestran las formas principales en que los usuarios usan extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="c607d-153">The following scenarios show the primary ways people use messaging extensions.</span></span>

### <a name="insert-content-into-a-message"></a><span data-ttu-id="c607d-154">Insertar contenido en un mensaje</span><span class="sxs-lookup"><span data-stu-id="c607d-154">Insert content into a message</span></span>

<span data-ttu-id="c607d-155">**1. Seleccione una extensión de mensajería**.</span><span class="sxs-lookup"><span data-stu-id="c607d-155">**1. Select a messaging extension**.</span></span> <span data-ttu-id="c607d-156">Los usuarios pueden buscar el contenido que desean compartir desde el cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="c607d-156">Users can search for the content they want to share from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="En el ejemplo se muestra un usuario que busca contenido para insertar desde el cuadro de redacción." border="false":::

<span data-ttu-id="c607d-158">**2. Insertar contenido**.</span><span class="sxs-lookup"><span data-stu-id="c607d-158">**2. Insert content**.</span></span> <span data-ttu-id="c607d-159">Una vez publicado, otros usuarios pueden responder o seleccionar el contenido para ver más información en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c607d-159">Once posted, others can reply or select the content to see more information in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="En el ejemplo se muestra un usuario que publica contenido en una conversación de canal." border="false":::

### <a name="take-action-on-a-message"></a><span data-ttu-id="c607d-161">Realizar acciones en un mensaje</span><span class="sxs-lookup"><span data-stu-id="c607d-161">Take action on a message</span></span>

<span data-ttu-id="c607d-162">**1. Seleccione una extensión de mensajería**.</span><span class="sxs-lookup"><span data-stu-id="c607d-162">**1. Select a messaging extension**.</span></span> <span data-ttu-id="c607d-163">La aplicación puede incluir uno o varios comandos de acción.</span><span class="sxs-lookup"><span data-stu-id="c607d-163">Your app can include one or more action commands.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="En el ejemplo se muestra un usuario que selecciona un comando de acción de extensión de mensajería." border="false":::

<span data-ttu-id="c607d-165">**2. Complete la acción**.</span><span class="sxs-lookup"><span data-stu-id="c607d-165">**2. Complete the action**.</span></span> <span data-ttu-id="c607d-166">La aplicación puede recibir y procesar cualquier contenido o datos enviados por la acción del mensaje.</span><span class="sxs-lookup"><span data-stu-id="c607d-166">Your app can receive and process any content or data sent by the message action.</span></span> <span data-ttu-id="c607d-167">Esto permite a los usuarios permanecer en su conversación y, en el ejemplo siguiente, no preocuparse por escribir información directamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c607d-167">This allows users to remain in their conversation and, the following example, not worry about entering information directly in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="Ejemplo sobre cómo realizar acciones en un mensaje." border="false":::

### <a name="preview-links"></a><span data-ttu-id="c607d-169">Vínculos de vista previa</span><span class="sxs-lookup"><span data-stu-id="c607d-169">Preview links</span></span>

<span data-ttu-id="c607d-170">Las extensiones de mensajería también permiten insertar vínculos enriquecidos desde una dirección URL reconocida en un mensaje (esta funcionalidad se denomina desafugüe [de vínculos](../../messaging-extensions/how-to/link-unfurling.md)).)</span><span class="sxs-lookup"><span data-stu-id="c607d-170">Messaging extensions also allow you to insert rich links from a recognized URL into a message (this capability is called [link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)</span></span>

<span data-ttu-id="c607d-171">**1. Pegue un vínculo reconocido en** el cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="c607d-171">**1. Paste a recognized link** in the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="En el ejemplo se muestra a un usuario pegando un vínculo en el cuadro de compost." border="false":::

<span data-ttu-id="c607d-173">**2. Insertar contenido**.</span><span class="sxs-lookup"><span data-stu-id="c607d-173">**2. Insert content**.</span></span> <span data-ttu-id="c607d-174">Si la aplicación reconoce la dirección URL en el cuadro de redacción, representa el vínculo como una tarjeta que proporciona una vista previa con contenido enriquecido del contenido web.</span><span class="sxs-lookup"><span data-stu-id="c607d-174">If your app recognizes the URL in the compose box, it renders the link as a card that provides a content-rich preview of the web content.</span></span> <span data-ttu-id="c607d-175">(Vea [Directrices de diseño de tarjetas adaptables](../../task-modules-and-cards/cards/design-effective-cards.md) para obtener más información).</span><span class="sxs-lookup"><span data-stu-id="c607d-175">(See [Adaptive Cards design guidelines](../../task-modules-and-cards/cards/design-effective-cards.md) for more information.)</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="En un ejemplo se muestra cómo la dirección URL, ya que la reconoce la aplicación, incluye contenido enriquecido en el cuadro de redacción." border="false":::

## <a name="manage-a-messaging-extension"></a><span data-ttu-id="c607d-177">Administrar una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="c607d-177">Manage a messaging extension</span></span>

<span data-ttu-id="c607d-178">Al hacer clic con el botón secundario en el icono, los usuarios pueden anclar, quitar o configurar la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="c607d-178">By right clicking your icon, users can pin, remove, or configure your messaging extension.</span></span>

## <a name="anatomy"></a><span data-ttu-id="c607d-179">Anatomía</span><span class="sxs-lookup"><span data-stu-id="c607d-179">Anatomy</span></span>

### <a name="messaging-extension-in-the-compose-box"></a><span data-ttu-id="c607d-180">Extensión de mensajería en el cuadro de redacción</span><span class="sxs-lookup"><span data-stu-id="c607d-180">Messaging extension in the compose box</span></span>

<span data-ttu-id="c607d-181">El siguiente ejemplo es una extensión de mensajería abierta desde el cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="c607d-181">The following example is a messaging extension opened from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una extensión de mensajería en el cuadro de redacción." border="false":::

|<span data-ttu-id="c607d-183">Contador</span><span class="sxs-lookup"><span data-stu-id="c607d-183">Counter</span></span>|<span data-ttu-id="c607d-184">Descripción</span><span class="sxs-lookup"><span data-stu-id="c607d-184">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="c607d-185">1</span><span class="sxs-lookup"><span data-stu-id="c607d-185">1</span></span>|<span data-ttu-id="c607d-186">**Logotipo de la aplicación:** icono de color del logotipo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c607d-186">**App logo**: Color icon of your app logo.</span></span>|
|<span data-ttu-id="c607d-187">2</span><span class="sxs-lookup"><span data-stu-id="c607d-187">2</span></span>|<span data-ttu-id="c607d-188">**Nombre de la** aplicación: nombre completo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c607d-188">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="c607d-189">3</span><span class="sxs-lookup"><span data-stu-id="c607d-189">3</span></span>|<span data-ttu-id="c607d-190">**Icono de menú Comandos de acción (opcional):** abre una lista de comandos de acción para la extensión de mensajería (si especifica alguno).</span><span class="sxs-lookup"><span data-stu-id="c607d-190">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="c607d-191">4 </span><span class="sxs-lookup"><span data-stu-id="c607d-191">4</span></span>|<span data-ttu-id="c607d-192">**Cuadro de búsqueda:** permite a los usuarios encontrar el contenido de la aplicación que desean insertar.</span><span class="sxs-lookup"><span data-stu-id="c607d-192">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="c607d-193">5 </span><span class="sxs-lookup"><span data-stu-id="c607d-193">5</span></span>|<span data-ttu-id="c607d-194">**Menú Tab (opcional):** proporciona varias categorías de contenido.</span><span class="sxs-lookup"><span data-stu-id="c607d-194">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="c607d-195">6 </span><span class="sxs-lookup"><span data-stu-id="c607d-195">6</span></span>|<span data-ttu-id="c607d-196">**Menú Comandos de acción (opcional):** muestra una lista de comandos de acción (si especifica alguno).</span><span class="sxs-lookup"><span data-stu-id="c607d-196">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="c607d-197">7 </span><span class="sxs-lookup"><span data-stu-id="c607d-197">7</span></span>|<span data-ttu-id="c607d-198">**Contenido de la** aplicación: principalmente para mostrar los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="c607d-198">**App content**: Primarily to display search results.</span></span> <span data-ttu-id="c607d-199">El ejemplo aquí es usar el diseño de lista (el diseño de cuadrícula es otra opción).</span><span class="sxs-lookup"><span data-stu-id="c607d-199">The example here is using the list layout (grid layout is another option).</span></span>|
|<span data-ttu-id="c607d-200">8 </span><span class="sxs-lookup"><span data-stu-id="c607d-200">8</span></span>|<span data-ttu-id="c607d-201">**Logotipo de la** aplicación: icono de esquema del logotipo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c607d-201">**App logo**: Outline icon of your app logo.</span></span>|

### <a name="messaging-extension-management-menu"></a><span data-ttu-id="c607d-202">Menú administración de extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="c607d-202">Messaging extension management menu</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un menú de administración de extensiones de mensajería." border="false":::

|<span data-ttu-id="c607d-204">Contador</span><span class="sxs-lookup"><span data-stu-id="c607d-204">Counter</span></span>|<span data-ttu-id="c607d-205">Descripción</span><span class="sxs-lookup"><span data-stu-id="c607d-205">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="c607d-206">1</span><span class="sxs-lookup"><span data-stu-id="c607d-206">1</span></span>|<span data-ttu-id="c607d-207">**Desanclar:** disponible si el usuario ha anclado la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c607d-207">**Unpin**: Available if the user has pinned your app.</span></span>|
|<span data-ttu-id="c607d-208">2</span><span class="sxs-lookup"><span data-stu-id="c607d-208">2</span></span>|<span data-ttu-id="c607d-209">**Quitar:** quita la extensión de mensajería del canal, chat o reunión.</span><span class="sxs-lookup"><span data-stu-id="c607d-209">**Remove**: Removes the messaging extension from the channel, chat, or meeting.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="c607d-210">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="c607d-210">Best practices</span></span>

### <a name="setup-and-general-usage"></a><span data-ttu-id="c607d-211">Configuración y uso general</span><span class="sxs-lookup"><span data-stu-id="c607d-211">Setup and general usage</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="Ejemplo sobre configuración y uso general." border="false":::

#### <a name="do-integrate-with-single-sign-on"></a><span data-ttu-id="c607d-213">Hacer: integrar con el inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="c607d-213">Do: Integrate with single-sign on</span></span>

<span data-ttu-id="c607d-214">SSO hace que el proceso de inicio de sesión sea más fácil, rápido y seguro.</span><span class="sxs-lookup"><span data-stu-id="c607d-214">SSO makes the sign-in process easier, faster, and secure.</span></span> <span data-ttu-id="c607d-215">Además, si un usuario ya ha iniciado sesión en la aplicación personal, no tiene que volver a iniciar sesión para tener acceso a la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="c607d-215">Also, if a user has already signed in to your personal app, they don’t have to also sign in again to access the messaging extension.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="Ejemplo de integración con inicio de sesión único." border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a><span data-ttu-id="c607d-217">No: alejar a los usuarios de la conversación</span><span class="sxs-lookup"><span data-stu-id="c607d-217">Don't: Take users away from the conversation</span></span>

<span data-ttu-id="c607d-218">Las extensiones de mensajería son métodos abreviados que se supone reducen el cambio de contexto.</span><span class="sxs-lookup"><span data-stu-id="c607d-218">Messaging extensions are shortcuts that are supposed reduce context switching.</span></span> <span data-ttu-id="c607d-219">La extensión no debe, por ejemplo, dirigir a los usuarios a una página web fuera de Teams.</span><span class="sxs-lookup"><span data-stu-id="c607d-219">Your extension should not, for example, direct users to a webpage outside Teams.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a><span data-ttu-id="c607d-220">Hacer: Resaltar la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="c607d-220">Do: Highlight your messaging extension</span></span>

<span data-ttu-id="c607d-221">Las extensiones de mensajería no siempre son fáciles de encontrar.</span><span class="sxs-lookup"><span data-stu-id="c607d-221">Messaging extensions aren't always easy to find.</span></span> <span data-ttu-id="c607d-222">Incluye capturas de pantalla de cómo usarlo en la página de detalles de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c607d-222">Include screenshots of how to use it in your app details page.</span></span> <span data-ttu-id="c607d-223">Si la aplicación también incluye un bot, puedes incluir documentación de ayuda de extensión de mensajería en un recorrido de bienvenida del bot.</span><span class="sxs-lookup"><span data-stu-id="c607d-223">If your app also includes a bot, you can include messaging extension help documentation in a bot welcome tour.</span></span>

### <a name="templating"></a><span data-ttu-id="c607d-224">Templating</span><span class="sxs-lookup"><span data-stu-id="c607d-224">Templating</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="Ejemplo de templating." border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a><span data-ttu-id="c607d-226">Hacer: permitir que Teams controle parte del trabajo de diseño si es posible</span><span class="sxs-lookup"><span data-stu-id="c607d-226">Do: Let Teams handle some of the design work if possible</span></span>

<span data-ttu-id="c607d-227">Si tiene sentido para los casos de uso, considere la posibilidad de crear una extensión de mensajería basada en búsquedas.</span><span class="sxs-lookup"><span data-stu-id="c607d-227">If it makes sense for your use cases, consider creating a search-based messaging extension.</span></span> <span data-ttu-id="c607d-228">Teams representa estos tipos de extensiones con tema y accesibilidad integrados.</span><span class="sxs-lookup"><span data-stu-id="c607d-228">Teams renders these types of extensions with built-in theming and accessibility.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="Ejemplo sobre cómo controlar el trabajo de diseño." border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a><span data-ttu-id="c607d-230">No: insertar toda la aplicación en un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="c607d-230">Don't: Embed your entire app in a task module</span></span>

<span data-ttu-id="c607d-231">Si la extensión de mensajería requiere comandos de acción, mantenga el módulo de tareas sencillo y muestre solo los componentes necesarios para completar la acción.</span><span class="sxs-lookup"><span data-stu-id="c607d-231">If your messaging extension requires action commands, keep the task module simple and display only the components required to complete the action.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="c607d-232">Creación de temas</span><span class="sxs-lookup"><span data-stu-id="c607d-232">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="Ejemplo en el uso de los mismos." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="c607d-234">Hacer: Aprovechar los tokens de color de Teams</span><span class="sxs-lookup"><span data-stu-id="c607d-234">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="c607d-235">Cada tema de Teams tiene su propia combinación de colores.</span><span class="sxs-lookup"><span data-stu-id="c607d-235">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="c607d-236">Para controlar los cambios de tema automáticamente, usa <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">tokens de color (Fluent UI)</a> en el diseño.</span><span class="sxs-lookup"><span data-stu-id="c607d-236">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="Ejemplo en tokens de color." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="c607d-238">No: valores de color de código duro</span><span class="sxs-lookup"><span data-stu-id="c607d-238">Don't: Hard code color values</span></span>

<span data-ttu-id="c607d-239">Si no usa tokens de color de Teams, sus diseños serán menos escalables y tendrán más tiempo para administrar.</span><span class="sxs-lookup"><span data-stu-id="c607d-239">If you don't use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="actions"></a><span data-ttu-id="c607d-240">Acciones</span><span class="sxs-lookup"><span data-stu-id="c607d-240">Actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="Ejemplo de acciones." border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a><span data-ttu-id="c607d-242">Hacer: incluir comandos de acción que tienen sentido en contexto</span><span class="sxs-lookup"><span data-stu-id="c607d-242">Do: Include action commands that make sense in context</span></span>

<span data-ttu-id="c607d-243">Las acciones del mensaje deben estar relacionadas con lo que un usuario está viendo.</span><span class="sxs-lookup"><span data-stu-id="c607d-243">Message actions should relate to what a user is looking at.</span></span> <span data-ttu-id="c607d-244">Por ejemplo, proporcione a los usuarios un acceso directo para crear un problema o elemento de trabajo con el texto de la publicación de alguien.</span><span class="sxs-lookup"><span data-stu-id="c607d-244">For example, provide users a shortcut for creating an issue or work item using the text in someone’s post.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="Ejemplo de comandos de acción." border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a><span data-ttu-id="c607d-246">No: incluir comandos de acciones que no son contextuales</span><span class="sxs-lookup"><span data-stu-id="c607d-246">Don't: Include actions commands that aren't contextual</span></span>

<span data-ttu-id="c607d-247">Una acción de mensaje **para ver el panel** probablemente parecería desconectada de la mayoría de las conversaciones.</span><span class="sxs-lookup"><span data-stu-id="c607d-247">A message action to **View your dashboard** would probably seem disconnected from most conversations.</span></span>

   :::column-end:::
:::row-end:::

### <a name="searches"></a><span data-ttu-id="c607d-248">Búsquedas</span><span class="sxs-lookup"><span data-stu-id="c607d-248">Searches</span></span>

#### <a name="do-show-search-results-while-typing"></a><span data-ttu-id="c607d-249">Hacer: mostrar resultados de búsqueda al escribir</span><span class="sxs-lookup"><span data-stu-id="c607d-249">Do: Show search results while typing</span></span>

<span data-ttu-id="c607d-250">Proporcionar resultados de búsqueda sugeridos mientras los usuarios escriben.</span><span class="sxs-lookup"><span data-stu-id="c607d-250">Provide suggested search results while users type.</span></span> <span data-ttu-id="c607d-251">Es posible que encuentren el contenido que necesitan más rápido con una cantidad mínima de caracteres.</span><span class="sxs-lookup"><span data-stu-id="c607d-251">They may find the content they need faster with minimal amount of characters.</span></span>

#### <a name="dont-require-users-to-submit-a-query"></a><span data-ttu-id="c607d-252">No: requerir que los usuarios envíen una consulta</span><span class="sxs-lookup"><span data-stu-id="c607d-252">Don't: Require users to submit a query</span></span>

<span data-ttu-id="c607d-253">Puedes hacer que los usuarios presionen una tecla o seleccione un botón para enviar consultas a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c607d-253">You can make users press a key or select a button to send queries to your app.</span></span> <span data-ttu-id="c607d-254">Aunque esto puede ser más fácil en el servicio de servicios de aplicaciones, es posible que los usuarios se confundan de que no ven resultados de búsqueda en tiempo real mientras escriben.</span><span class="sxs-lookup"><span data-stu-id="c607d-254">While that may be easier on your app services service, people may be confused that they're not seeing real-time search results as they type.</span></span>

#### <a name="do-consider-zero-term-queries"></a><span data-ttu-id="c607d-255">Do: Consider zero-term queries</span><span class="sxs-lookup"><span data-stu-id="c607d-255">Do: Consider zero-term queries</span></span>

<span data-ttu-id="c607d-256">Por ejemplo, antes de que un usuario escriba algo en el cuadro de búsqueda, muestre lo que ha visto por última vez en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c607d-256">For example, before a user writes anything in the search box, display what they last viewed on your app.</span></span> <span data-ttu-id="c607d-257">Es posible que quieran insertar ese contenido en su conversación.</span><span class="sxs-lookup"><span data-stu-id="c607d-257">It's possible that they want to insert that content into their conversation.</span></span>

## <a name="validate-your-design"></a><span data-ttu-id="c607d-258">Valide su diseño</span><span class="sxs-lookup"><span data-stu-id="c607d-258">Validate your design</span></span>

<span data-ttu-id="c607d-259">Si tiene previsto publicar la aplicación en AppSource, debe comprender los problemas de diseño que habitualmente provocan errores en las aplicaciones durante el envío.</span><span class="sxs-lookup"><span data-stu-id="c607d-259">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c607d-260">Comprobar las instrucciones de validación de diseño</span><span class="sxs-lookup"><span data-stu-id="c607d-260">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)

---
title: Diseño de la extensión de mensajería
description: Obtén información sobre cómo diseñar una extensión de mensajería Teams y obtener el kit de interfaz de usuario de Microsoft Teams.
keywords: directrices de diseño de equipos de referencia extensiones de mensajería consejos mejores prácticas
author: heath-hamilton
localization_priority: Normal
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: ed1f0f2eb2ce8d429a8a780bd2c4c4eb421d6d54
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566218"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a><span data-ttu-id="d8211-104">Diseño de la extensión de mensajería Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d8211-104">Designing your Microsoft Teams messaging extension</span></span>

<span data-ttu-id="d8211-105">Las extensiones de mensajería son accesos directos para insertar contenido de la aplicación o actuar en un mensaje sin navegar lejos de la conversación.</span><span class="sxs-lookup"><span data-stu-id="d8211-105">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span>
<span data-ttu-id="d8211-106">Para guiar el diseño de la aplicación, la siguiente información describe e ilustra cómo las personas pueden agregar, usar y administrar extensiones de mensajería en Teams.</span><span class="sxs-lookup"><span data-stu-id="d8211-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage messaging extensions in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="d8211-107">Kit de UI de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d8211-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="d8211-108">Puede encontrar directrices completas de diseño de extensiones de mensajería, incluidos los elementos que puede capturar y modificar según sea necesario, en el Kit de interfaz de usuario de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d8211-108">You can find comprehensive messaging extension design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d8211-109">Obtener el Kit de UI de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="d8211-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a><span data-ttu-id="d8211-110">Añadir una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="d8211-110">Add a messaging extension</span></span>

<span data-ttu-id="d8211-111">Puede agregar una extensión de mensajería en los siguientes contextos de Teams:</span><span class="sxs-lookup"><span data-stu-id="d8211-111">You can add a messaging extension in the following Teams contexts:</span></span>

* <span data-ttu-id="d8211-112">En la tienda de Teams (AppSource)</span><span class="sxs-lookup"><span data-stu-id="d8211-112">From the Teams store (AppSource).</span></span>
* <span data-ttu-id="d8211-113">En un canal, chatea o reúne (antes, durante y después) cerca del cuadro de composición.</span><span class="sxs-lookup"><span data-stu-id="d8211-113">In a channel, chat, or meeting (before, during, and after) near the compose box.</span></span> <span data-ttu-id="d8211-114">Vale la pena señalar si agrega una extensión de mensajería en uno de estos lugares, solo usted puede usarlo en ese contexto.</span><span class="sxs-lookup"><span data-stu-id="d8211-114">It's worth noting if you add a messaging extension in one of these places, only you can use it in that context.</span></span>

<span data-ttu-id="d8211-115">En el ejemplo siguiente se muestra cómo agregar una extensión de mensajería en un canal:</span><span class="sxs-lookup"><span data-stu-id="d8211-115">The following example shows how you add a messaging extension in a channel:</span></span>

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de mensajería cerca del cuadro de composición en un canal." border="false":::

## <a name="set-up-a-messaging-extension"></a><span data-ttu-id="d8211-117">Configurar una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="d8211-117">Set up a messaging extension</span></span>

<span data-ttu-id="d8211-118">La autenticación no es obligatoria, pero si la aplicación es algo así como una herramienta de seguimiento de vales, es posible que necesite que las personas inicien sesión para usar la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="d8211-118">Authentication isn't mandatory, but if your app is something like a ticket tracking tool, you may need people to sign in to use the messaging extension.</span></span>

<span data-ttu-id="d8211-119">Para obtener coherencia entre Teams aplicaciones, no puede personalizar la pantalla de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="d8211-119">For consistency across Teams apps, you can't customize the sign-in screen.</span></span> <span data-ttu-id="d8211-120">Si utiliza la autenticación de inicio de sesión único (SSO), los usuarios inician sesión automáticamente.</span><span class="sxs-lookup"><span data-stu-id="d8211-120">If you use single sign-on (SSO) authentication, users are signed in automatically.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="En el ejemplo se muestra la pantalla de configuración de la extensión de mensajería con un botón de inicio de sesión." border="false":::

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="d8211-122">Tipos de extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="d8211-122">Types of messaging extensions</span></span>

<span data-ttu-id="d8211-123">Las extensiones de mensajería pueden tener comandos de búsqueda, comandos de acción o ambos.</span><span class="sxs-lookup"><span data-stu-id="d8211-123">Messaging extensions can have search commands, action commands, or both.</span></span> <span data-ttu-id="d8211-124">Los comandos dependen de las características de la aplicación y de cómo se ajusten en Teams casos de uso.</span><span class="sxs-lookup"><span data-stu-id="d8211-124">Your commands depend on your app's features and how those fit within Teams use cases.</span></span>

### <a name="search-commands"></a><span data-ttu-id="d8211-125">Comandos de búsqueda</span><span class="sxs-lookup"><span data-stu-id="d8211-125">Search commands</span></span>

<span data-ttu-id="d8211-126">Con los comandos de búsqueda, las personas pueden usar la extensión de mensajería para encontrar rápidamente contenido externo e insertarlo en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="d8211-126">With search commands, people can use your messaging extension to quickly find external content and insert into a message.</span></span> <span data-ttu-id="d8211-127">Los comandos de búsqueda suelen estar disponibles en el cuadro de composición.</span><span class="sxs-lookup"><span data-stu-id="d8211-127">Search commands are commonly made available in the compose box.</span></span> <span data-ttu-id="d8211-128">Por ejemplo, puede iniciar o agregar a una discusión compartiendo un fragmento de contenido, sin salir nunca de Teams.</span><span class="sxs-lookup"><span data-stu-id="d8211-128">For example, you can start or add to a discussion by sharing a piece of content—without ever leaving Teams.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="En el ejemplo se muestra una extensión de mensajería basada en búsqueda iniciada desde el cuadro de composición." border="false":::

#### <a name="compose-box-layout-options"></a><span data-ttu-id="d8211-130">Opciones de diseño de cuadro de composición</span><span class="sxs-lookup"><span data-stu-id="d8211-130">Compose box layout options</span></span>

<span data-ttu-id="d8211-131">Tiene algunas opciones para mostrar los resultados de búsqueda de extensiones de mensajería, incluidas [las vistas de lista y cuadrícula.](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)</span><span class="sxs-lookup"><span data-stu-id="d8211-131">You have some options for displaying messaging extension search results, including [list and grid views](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="Ilustraciones que muestran opciones de diseño para los resultados de búsqueda de extensiones de mensajería." border="false":::

### <a name="action-commands"></a><span data-ttu-id="d8211-133">Comandos de acción</span><span class="sxs-lookup"><span data-stu-id="d8211-133">Action commands</span></span>

<span data-ttu-id="d8211-134">Los comandos de acción permiten a las personas desencadenar acciones y procesar solicitudes en servicios externos dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="d8211-134">Action commands allow people to trigger actions and process requests in external services within Teams.</span></span> <span data-ttu-id="d8211-135">Por ejemplo, si la aplicación realiza un seguimiento de los pedidos, un usuario podría crear un nuevo pedido utilizando el contenido del mensaje de un colega desde el interior de su chat.</span><span class="sxs-lookup"><span data-stu-id="d8211-135">For example, if your app tracks orders, a user could create a new order using the contents of a colleague’s message from right inside their chat.</span></span>

<span data-ttu-id="d8211-136">Las extensiones de mensajería basadas en acciones con frecuencia requieren que los usuarios completen un formulario o algún otro tipo de configuración dentro de un modal.</span><span class="sxs-lookup"><span data-stu-id="d8211-136">Action-based messaging extensions frequently require users to complete a form or some other kind of configuration within a modal.</span></span> <span data-ttu-id="d8211-137">Puede crear estas experiencias con [módulos de tareas.](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)</span><span class="sxs-lookup"><span data-stu-id="d8211-137">You can create these experiences with [task modules](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="open-a-messaging-extension"></a><span data-ttu-id="d8211-138">Abrir una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="d8211-138">Open a messaging extension</span></span>

<span data-ttu-id="d8211-139">El cuadro de composición y los mensajes o publicaciones son los contextos principales donde las personas usan extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="d8211-139">The compose box and messages or posts are the primary contexts where people use messaging extensions.</span></span>

### <a name="from-the-compose-box"></a><span data-ttu-id="d8211-140">Desde la caja de composa</span><span class="sxs-lookup"><span data-stu-id="d8211-140">From the compose box</span></span>

<span data-ttu-id="d8211-141">Una vez agregado, los usuarios pueden abrir la extensión de mensajería seleccionando el icono de la aplicación debajo del cuadro de composición.</span><span class="sxs-lookup"><span data-stu-id="d8211-141">Once added, users can open your messaging extension by selecting your app icon below the compose box.</span></span> <span data-ttu-id="d8211-142">En este ejemplo, la extensión tiene comandos de búsqueda y acción:</span><span class="sxs-lookup"><span data-stu-id="d8211-142">In this example, the extension has search and action commands:</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="En el ejemplo se muestra cómo abrir una extensión de mensajería desde el cuadro de composición." border="false":::

### <a name="from-a-chat-message-or-channel-post"></a><span data-ttu-id="d8211-144">Desde un mensaje de chat o una publicación de canal</span><span class="sxs-lookup"><span data-stu-id="d8211-144">From a chat message or channel post</span></span>

Una vez agregado, los usuarios pueden seleccionar el icono **Más** en el mensaje de chat o la publicación de canal para encontrar los :::image type="icon" source="../../assets/icons/teams-client-more.png"::: comandos de acción de la extensión. <span data-ttu-id="d8211-146">Su extensión puede aparecer en **Más acciones** basadas en el uso.</span><span class="sxs-lookup"><span data-stu-id="d8211-146">Your extension may be listed under **More actions** based on usage.</span></span>

> [!NOTE]
> <span data-ttu-id="d8211-147">El soporte para más acciones de un mensaje de chat o una publicación de canal no está disponible en Microsoft Teams plataforma móvil.</span><span class="sxs-lookup"><span data-stu-id="d8211-147">Support for more actions from a chat message or channel post is not available on Microsoft Teams mobile platform.</span></span> 

#### <a name="chat-message"></a><span data-ttu-id="d8211-148">Mensaje de chat</span><span class="sxs-lookup"><span data-stu-id="d8211-148">Chat message</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="En el ejemplo se muestra cómo abrir una extensión de mensajería desde un mensaje de chat." border="false":::

#### <a name="channel-post"></a><span data-ttu-id="d8211-150">Publicación de canal</span><span class="sxs-lookup"><span data-stu-id="d8211-150">Channel post</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="En el ejemplo se muestra cómo abrir una extensión de mensajería desde una publicación de canal." border="false":::

## <a name="use-a-messaging-extension"></a><span data-ttu-id="d8211-152">Usar una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="d8211-152">Use a messaging extension</span></span>

<span data-ttu-id="d8211-153">Los siguientes escenarios muestran las formas principales en que las personas usan extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="d8211-153">The following scenarios show the primary ways people use messaging extensions.</span></span>

### <a name="insert-content-into-a-message"></a><span data-ttu-id="d8211-154">Insertar contenido en un mensaje</span><span class="sxs-lookup"><span data-stu-id="d8211-154">Insert content into a message</span></span>

<span data-ttu-id="d8211-155">**1. Seleccione una extensión de mensajería**.</span><span class="sxs-lookup"><span data-stu-id="d8211-155">**1. Select a messaging extension**.</span></span> <span data-ttu-id="d8211-156">Los usuarios pueden buscar el contenido que desean compartir desde el cuadro de composición.</span><span class="sxs-lookup"><span data-stu-id="d8211-156">Users can search for the content they want to share from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="En el ejemplo se muestra a un usuario que busca contenido para insertar desde el cuadro de composición." border="false":::

<span data-ttu-id="d8211-158">**2. Inserte contenido**.</span><span class="sxs-lookup"><span data-stu-id="d8211-158">**2. Insert content**.</span></span> <span data-ttu-id="d8211-159">Una vez publicado, otros pueden responder o seleccionar el contenido para ver más información en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8211-159">Once posted, others can reply or select the content to see more information in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="En el ejemplo se muestra un usuario que publica contenido en una conversación de canal." border="false":::

### <a name="take-action-on-a-message"></a><span data-ttu-id="d8211-161">Tomar medidas en un mensaje</span><span class="sxs-lookup"><span data-stu-id="d8211-161">Take action on a message</span></span>

<span data-ttu-id="d8211-162">**1. Seleccione una extensión de mensajería**.</span><span class="sxs-lookup"><span data-stu-id="d8211-162">**1. Select a messaging extension**.</span></span> <span data-ttu-id="d8211-163">La aplicación puede incluir uno o varios comandos de acción.</span><span class="sxs-lookup"><span data-stu-id="d8211-163">Your app can include one or more action commands.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="En el ejemplo se muestra a un usuario que selecciona un comando de acción de extensión de mensajería." border="false":::

<span data-ttu-id="d8211-165">**2. Complete la acción**.</span><span class="sxs-lookup"><span data-stu-id="d8211-165">**2. Complete the action**.</span></span> <span data-ttu-id="d8211-166">La aplicación puede recibir y procesar cualquier contenido o datos enviados por la acción del mensaje.</span><span class="sxs-lookup"><span data-stu-id="d8211-166">Your app can receive and process any content or data sent by the message action.</span></span> <span data-ttu-id="d8211-167">Esto permite a los usuarios permanecer en su conversación y, en el siguiente ejemplo, no preocuparse por introducir información directamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8211-167">This allows users to remain in their conversation and, the following example, not worry about entering information directly in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="Ejemplo sobre cómo tomar medidas en un mensaje." border="false":::

### <a name="preview-links"></a><span data-ttu-id="d8211-169">Enlaces de vista previa</span><span class="sxs-lookup"><span data-stu-id="d8211-169">Preview links</span></span>

<span data-ttu-id="d8211-170">Las extensiones de mensajería también le permiten insertar vínculos enriquecidos desde una dirección URL reconocida en un mensaje (esta funcionalidad se denomina [despliegue de vínculos](../../messaging-extensions/how-to/link-unfurling.md).)</span><span class="sxs-lookup"><span data-stu-id="d8211-170">Messaging extensions also allow you to insert rich links from a recognized URL into a message (this capability is called [link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)</span></span>

<span data-ttu-id="d8211-171">**1. Pegue un enlace reconocido** en el cuadro de composición.</span><span class="sxs-lookup"><span data-stu-id="d8211-171">**1. Paste a recognized link** in the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="En el ejemplo se muestra a un usuario pegando un vínculo en el cuadro de compost." border="false":::

<span data-ttu-id="d8211-173">**2. Inserte contenido**.</span><span class="sxs-lookup"><span data-stu-id="d8211-173">**2. Insert content**.</span></span> <span data-ttu-id="d8211-174">Si la aplicación reconoce la dirección URL en el cuadro de composición, representa el vínculo como una tarjeta que proporciona una vista previa enriquecida con contenido del contenido web.</span><span class="sxs-lookup"><span data-stu-id="d8211-174">If your app recognizes the URL in the compose box, it renders the link as a card that provides a content-rich preview of the web content.</span></span> <span data-ttu-id="d8211-175">(Consulte [directrices de diseño de tarjetas adaptables](../../task-modules-and-cards/cards/design-effective-cards.md) para obtener más información.)</span><span class="sxs-lookup"><span data-stu-id="d8211-175">(See [Adaptive Cards design guidelines](../../task-modules-and-cards/cards/design-effective-cards.md) for more information.)</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="En el ejemplo se muestra cómo la dirección URL, ya que la reconoce la aplicación, incluye contenido enriquecido en el cuadro de composición." border="false":::

## <a name="manage-a-messaging-extension"></a><span data-ttu-id="d8211-177">Administrar una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="d8211-177">Manage a messaging extension</span></span>

<span data-ttu-id="d8211-178">Al hacer clic con el botón derecho en el icono, los usuarios pueden anclar, quitar o configurar la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="d8211-178">By right clicking your icon, users can pin, remove, or configure your messaging extension.</span></span>

## <a name="anatomy"></a><span data-ttu-id="d8211-179">Anatomía</span><span class="sxs-lookup"><span data-stu-id="d8211-179">Anatomy</span></span>

### <a name="messaging-extension-in-the-compose-box"></a><span data-ttu-id="d8211-180">Extensión de mensajería en el cuadro de composición</span><span class="sxs-lookup"><span data-stu-id="d8211-180">Messaging extension in the compose box</span></span>

<span data-ttu-id="d8211-181">En el ejemplo siguiente se abre una extensión de mensajería desde el cuadro de composición.</span><span class="sxs-lookup"><span data-stu-id="d8211-181">The following example is a messaging extension opened from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una extensión de mensajería en el cuadro de composición." border="false":::

|<span data-ttu-id="d8211-183">Contador</span><span class="sxs-lookup"><span data-stu-id="d8211-183">Counter</span></span>|<span data-ttu-id="d8211-184">Descripción</span><span class="sxs-lookup"><span data-stu-id="d8211-184">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d8211-185">1</span><span class="sxs-lookup"><span data-stu-id="d8211-185">1</span></span>|<span data-ttu-id="d8211-186">**Logotipo de la aplicación**: Icono de color del logotipo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8211-186">**App logo**: Color icon of your app logo.</span></span>|
|<span data-ttu-id="d8211-187">2</span><span class="sxs-lookup"><span data-stu-id="d8211-187">2</span></span>|<span data-ttu-id="d8211-188">**Nombre de la aplicación**: Nombre completo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8211-188">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="d8211-189">3</span><span class="sxs-lookup"><span data-stu-id="d8211-189">3</span></span>|<span data-ttu-id="d8211-190">Icono de menú comandos de **acción (opcional):** abre una lista de comandos de acción para la extensión de mensajería (si especifica alguno).</span><span class="sxs-lookup"><span data-stu-id="d8211-190">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="d8211-191">4 </span><span class="sxs-lookup"><span data-stu-id="d8211-191">4</span></span>|<span data-ttu-id="d8211-192">**Cuadro de búsqueda**: Permite a los usuarios encontrar el contenido de la aplicación que desean insertar.</span><span class="sxs-lookup"><span data-stu-id="d8211-192">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="d8211-193">5 </span><span class="sxs-lookup"><span data-stu-id="d8211-193">5</span></span>|<span data-ttu-id="d8211-194">**Menú de pestañas (opcional):** proporciona varias categorías de contenido.</span><span class="sxs-lookup"><span data-stu-id="d8211-194">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="d8211-195">6 </span><span class="sxs-lookup"><span data-stu-id="d8211-195">6</span></span>|<span data-ttu-id="d8211-196">**Menú comandos de acción (opcional):** muestra la lista de comandos de acción (si especifica alguno).</span><span class="sxs-lookup"><span data-stu-id="d8211-196">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="d8211-197">7 </span><span class="sxs-lookup"><span data-stu-id="d8211-197">7</span></span>|<span data-ttu-id="d8211-198">**Contenido de la aplicación:** principalmente para mostrar los resultados de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="d8211-198">**App content**: Primarily to display search results.</span></span> <span data-ttu-id="d8211-199">El ejemplo aquí es el uso del diseño de lista (el diseño de cuadrícula es otra opción).</span><span class="sxs-lookup"><span data-stu-id="d8211-199">The example here is using the list layout (grid layout is another option).</span></span>|
|<span data-ttu-id="d8211-200">8 </span><span class="sxs-lookup"><span data-stu-id="d8211-200">8</span></span>|<span data-ttu-id="d8211-201">**Logotipo de la aplicación**: Icono de contorno del logotipo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8211-201">**App logo**: Outline icon of your app logo.</span></span>|

### <a name="messaging-extension-management-menu"></a><span data-ttu-id="d8211-202">Menú de gestión de extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="d8211-202">Messaging extension management menu</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un menú de administración de extensiones de mensajería." border="false":::

|<span data-ttu-id="d8211-204">Contador</span><span class="sxs-lookup"><span data-stu-id="d8211-204">Counter</span></span>|<span data-ttu-id="d8211-205">Descripción</span><span class="sxs-lookup"><span data-stu-id="d8211-205">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d8211-206">1</span><span class="sxs-lookup"><span data-stu-id="d8211-206">1</span></span>|<span data-ttu-id="d8211-207">**Unpin**: Disponible si el usuario ha anclado la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8211-207">**Unpin**: Available if the user has pinned your app.</span></span>|
|<span data-ttu-id="d8211-208">2</span><span class="sxs-lookup"><span data-stu-id="d8211-208">2</span></span>|<span data-ttu-id="d8211-209">**Eliminar**: Elimina la extensión de mensajería del canal, chat o reunión.</span><span class="sxs-lookup"><span data-stu-id="d8211-209">**Remove**: Removes the messaging extension from the channel, chat, or meeting.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="d8211-210">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="d8211-210">Best practices</span></span>

<span data-ttu-id="d8211-211">Utilice estas recomendaciones para crear una experiencia de aplicación de calidad.</span><span class="sxs-lookup"><span data-stu-id="d8211-211">Use these recommendations to create a quality app experience.</span></span>

### <a name="setup-and-general-usage"></a><span data-ttu-id="d8211-212">Configuración y uso general</span><span class="sxs-lookup"><span data-stu-id="d8211-212">Setup and general usage</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="Ejemplo sobre la configuración y el uso general." border="false":::

#### <a name="do-integrate-with-single-sign-on"></a><span data-ttu-id="d8211-214">Hacer: Integre con el inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="d8211-214">Do: Integrate with single-sign on</span></span>

<span data-ttu-id="d8211-215">SSO hace que el proceso de inicio de sesión sea más fácil, rápido y seguro.</span><span class="sxs-lookup"><span data-stu-id="d8211-215">SSO makes the sign-in process easier, faster, and secure.</span></span> <span data-ttu-id="d8211-216">Además, si un usuario ya ha iniciado sesión en su aplicación personal, no tiene que volver a iniciar sesión para acceder a la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="d8211-216">Also, if a user has already signed in to your personal app, they don’t have to also sign in again to access the messaging extension.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="Ejemplo sobre la integración con el inicio de sesión único." border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a><span data-ttu-id="d8211-218">No: Alejar a los usuarios de la conversación</span><span class="sxs-lookup"><span data-stu-id="d8211-218">Don't: Take users away from the conversation</span></span>

<span data-ttu-id="d8211-219">Las extensiones de mensajería son accesos directos que se supone reducen el cambio de contexto.</span><span class="sxs-lookup"><span data-stu-id="d8211-219">Messaging extensions are shortcuts that are supposed reduce context switching.</span></span> <span data-ttu-id="d8211-220">La extensión no debe, por ejemplo, dirigir a los usuarios a una página web fuera de Teams.</span><span class="sxs-lookup"><span data-stu-id="d8211-220">Your extension should not, for example, direct users to a webpage outside Teams.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a><span data-ttu-id="d8211-221">Hacer: Resalte su extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="d8211-221">Do: Highlight your messaging extension</span></span>

<span data-ttu-id="d8211-222">Las extensiones de mensajería no siempre son fáciles de encontrar.</span><span class="sxs-lookup"><span data-stu-id="d8211-222">Messaging extensions aren't always easy to find.</span></span> <span data-ttu-id="d8211-223">Incluya capturas de pantalla de cómo usarlo en la página de detalles de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8211-223">Include screenshots of how to use it in your app details page.</span></span> <span data-ttu-id="d8211-224">Si la aplicación también incluye un bot, puede incluir documentación de ayuda de extensión de mensajería en un recorrido de bienvenida a bots.</span><span class="sxs-lookup"><span data-stu-id="d8211-224">If your app also includes a bot, you can include messaging extension help documentation in a bot welcome tour.</span></span>

### <a name="templating"></a><span data-ttu-id="d8211-225">Tentador</span><span class="sxs-lookup"><span data-stu-id="d8211-225">Templating</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="Ejemplo sobre la templación." border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a><span data-ttu-id="d8211-227">Hacer: Deje que Teams maneje parte del trabajo de diseño si es posible</span><span class="sxs-lookup"><span data-stu-id="d8211-227">Do: Let Teams handle some of the design work if possible</span></span>

<span data-ttu-id="d8211-228">Si tiene sentido para los casos de uso, considere la posibilidad de crear una extensión de mensajería basada en búsqueda.</span><span class="sxs-lookup"><span data-stu-id="d8211-228">If it makes sense for your use cases, consider creating a search-based messaging extension.</span></span> <span data-ttu-id="d8211-229">Teams representa estos tipos de extensiones con temática y accesibilidad integradas.</span><span class="sxs-lookup"><span data-stu-id="d8211-229">Teams renders these types of extensions with built-in theming and accessibility.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="Ejemplo sobre el trabajo de diseño de manipulación." border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a><span data-ttu-id="d8211-231">No: Incrusta toda la aplicación en un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="d8211-231">Don't: Embed your entire app in a task module</span></span>

<span data-ttu-id="d8211-232">Si la extensión de mensajería requiere comandos de acción, mantenga el módulo de tareas simple y muestre solo los componentes necesarios para completar la acción.</span><span class="sxs-lookup"><span data-stu-id="d8211-232">If your messaging extension requires action commands, keep the task module simple and display only the components required to complete the action.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="d8211-233">Creación de temas</span><span class="sxs-lookup"><span data-stu-id="d8211-233">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="Ejemplo sobre el uso de temática." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="d8211-235">Hacer: Aproveche Teams tokens de color</span><span class="sxs-lookup"><span data-stu-id="d8211-235">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="d8211-236">Cada tema Teams tiene su propio esquema de color.</span><span class="sxs-lookup"><span data-stu-id="d8211-236">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="d8211-237">Para controlar los cambios de tema automáticamente, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">tokens de color (interfaz de usuario fluida)</a> en el diseño.</span><span class="sxs-lookup"><span data-stu-id="d8211-237">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="Ejemplo sobre tokens de color." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="d8211-239">No: Valores de color de código duro</span><span class="sxs-lookup"><span data-stu-id="d8211-239">Don't: Hard code color values</span></span>

<span data-ttu-id="d8211-240">Si no usa tokens de color Teams, sus diseños serán menos escalables y tardarán más tiempo en administrarse.</span><span class="sxs-lookup"><span data-stu-id="d8211-240">If you don't use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="actions"></a><span data-ttu-id="d8211-241">Acciones</span><span class="sxs-lookup"><span data-stu-id="d8211-241">Actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="Ejemplo sobre acciones." border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a><span data-ttu-id="d8211-243">Hacer: Incluya comandos de acción que tienen sentido en contexto</span><span class="sxs-lookup"><span data-stu-id="d8211-243">Do: Include action commands that make sense in context</span></span>

<span data-ttu-id="d8211-244">Las acciones de mensaje deben relacionarse con lo que un usuario está mirando.</span><span class="sxs-lookup"><span data-stu-id="d8211-244">Message actions should relate to what a user is looking at.</span></span> <span data-ttu-id="d8211-245">Por ejemplo, proporcione a los usuarios un acceso directo para crear un problema o elemento de trabajo mediante el texto de la publicación de alguien.</span><span class="sxs-lookup"><span data-stu-id="d8211-245">For example, provide users a shortcut for creating an issue or work item using the text in someone’s post.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="Ejemplo sobre comandos de acción." border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a><span data-ttu-id="d8211-247">No: incluya comandos de acciones que no sean contextuales</span><span class="sxs-lookup"><span data-stu-id="d8211-247">Don't: Include actions commands that aren't contextual</span></span>

<span data-ttu-id="d8211-248">Una acción de mensaje para **Ver el panel** probablemente parecería desconectada de la mayoría de las conversaciones.</span><span class="sxs-lookup"><span data-stu-id="d8211-248">A message action to **View your dashboard** would probably seem disconnected from most conversations.</span></span>

   :::column-end:::
:::row-end:::

### <a name="searches"></a><span data-ttu-id="d8211-249">Búsquedas</span><span class="sxs-lookup"><span data-stu-id="d8211-249">Searches</span></span>

#### <a name="do-show-search-results-while-typing"></a><span data-ttu-id="d8211-250">Hacer: Mostrar los resultados de búsqueda mientras escribe</span><span class="sxs-lookup"><span data-stu-id="d8211-250">Do: Show search results while typing</span></span>

<span data-ttu-id="d8211-251">Proporcione los resultados de búsqueda sugeridos mientras los usuarios escriben.</span><span class="sxs-lookup"><span data-stu-id="d8211-251">Provide suggested search results while users type.</span></span> <span data-ttu-id="d8211-252">Pueden encontrar el contenido que necesitan más rápido con una cantidad mínima de caracteres.</span><span class="sxs-lookup"><span data-stu-id="d8211-252">They may find the content they need faster with minimal amount of characters.</span></span>

#### <a name="dont-require-users-to-submit-a-query"></a><span data-ttu-id="d8211-253">No: requiere que los usuarios envíen una consulta</span><span class="sxs-lookup"><span data-stu-id="d8211-253">Don't: Require users to submit a query</span></span>

<span data-ttu-id="d8211-254">Puede hacer que los usuarios presionen una tecla o seleccionen un botón para enviar consultas a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8211-254">You can make users press a key or select a button to send queries to your app.</span></span> <span data-ttu-id="d8211-255">Aunque eso puede ser más fácil en el servicio de servicios de aplicaciones, es posible que las personas se confundan con que no están viendo los resultados de búsqueda en tiempo real a medida que escriben.</span><span class="sxs-lookup"><span data-stu-id="d8211-255">While that may be easier on your app services service, people may be confused that they're not seeing real-time search results as they type.</span></span>

#### <a name="do-consider-zero-term-queries"></a><span data-ttu-id="d8211-256">Hacer: Considere consultas de términos cero</span><span class="sxs-lookup"><span data-stu-id="d8211-256">Do: Consider zero-term queries</span></span>

<span data-ttu-id="d8211-257">Por ejemplo, antes de que un usuario escriba algo en el cuadro de búsqueda, muestra lo que vio por última vez en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8211-257">For example, before a user writes anything in the search box, display what they last viewed on your app.</span></span> <span data-ttu-id="d8211-258">Es posible que quieran insertar ese contenido en su conversación.</span><span class="sxs-lookup"><span data-stu-id="d8211-258">It's possible that they want to insert that content into their conversation.</span></span>

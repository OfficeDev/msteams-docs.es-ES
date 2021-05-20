---
title: Diseño de su pestaña para escritorio y web
description: Obtén información sobre cómo diseñar una pestaña de Teams (escritorio y web) y obtener el Kit de interfaz de usuario Microsoft Teams.
author: heath-hamilton
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: baa17cd97ff4e2cad91615dced5c4e4cf5e533c8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566883"
---
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a><span data-ttu-id="a7591-103">Diseñar su pestaña para Microsoft Teams escritorio y web</span><span class="sxs-lookup"><span data-stu-id="a7591-103">Designing your tab for Microsoft Teams desktop and web</span></span>

<span data-ttu-id="a7591-104">Una pestaña es un lienzo grande para su contenido.</span><span class="sxs-lookup"><span data-stu-id="a7591-104">A tab is a large canvas for your content.</span></span> <span data-ttu-id="a7591-105">Para guiar el diseño de la aplicación, la siguiente información describe e ilustra cómo las personas pueden agregar, usar y administrar pestañas en Teams.</span><span class="sxs-lookup"><span data-stu-id="a7591-105">To guide your app design, the following information describes and illustrates how people can add, use, and manage tabs in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="a7591-106">Kit de UI de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a7591-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="a7591-107">Puede encontrar directrices completas de diseño de pestañas, incluidos los elementos que puede capturar y modificar según sea necesario, en el Kit de interfaz de usuario de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a7591-107">You can find comprehensive tab design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="a7591-108">El kit de interfaz de usuario también tiene temas esenciales como la accesibilidad y el tamaño adaptable que no se tratan aquí.</span><span class="sxs-lookup"><span data-stu-id="a7591-108">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a7591-109">Obtener el Kit de UI de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="a7591-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a><span data-ttu-id="a7591-110">Agregar una pestaña</span><span class="sxs-lookup"><span data-stu-id="a7591-110">Add a tab</span></span>

<span data-ttu-id="a7591-111">Puede agregar una pestaña desde la tienda de Teams (AppSource) o en uno de los contextos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a7591-111">You can add a tab from the Teams store (AppSource) or in one of the following contexts:</span></span>

* <span data-ttu-id="a7591-112">Chat</span><span class="sxs-lookup"><span data-stu-id="a7591-112">Chat</span></span>
* <span data-ttu-id="a7591-113">Canal</span><span class="sxs-lookup"><span data-stu-id="a7591-113">Channel</span></span>
* <span data-ttu-id="a7591-114">Reunión (antes, durante o después de la reunión)</span><span class="sxs-lookup"><span data-stu-id="a7591-114">Meeting (before, during, or after the meeting)</span></span>

<span data-ttu-id="a7591-115">En el ejemplo siguiente se muestra cómo se agrega una pestaña en un canal:</span><span class="sxs-lookup"><span data-stu-id="a7591-115">The following example shows how a tab is added in a channel:</span></span>

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="En el ejemplo se muestra una pestaña que se agrega en un canal." border="false":::

## <a name="set-up-a-tab"></a><span data-ttu-id="a7591-117">Configurar una pestaña</span><span class="sxs-lookup"><span data-stu-id="a7591-117">Set up a tab</span></span>

<span data-ttu-id="a7591-118">Hay un proceso de configuración corto para agregar una aplicación como canal, chat o pestaña de reunión. La experiencia depende en gran medida de usted.</span><span class="sxs-lookup"><span data-stu-id="a7591-118">There's a short setup process to add an app as a channel, chat, or meeting tab. The experience is largely up to you.</span></span> <span data-ttu-id="a7591-119">Por ejemplo, podría tener una descripción de cómo usar la aplicación y alguna configuración opcional.</span><span class="sxs-lookup"><span data-stu-id="a7591-119">For example, you could have a description of how to use the app and some optional settings.</span></span> <span data-ttu-id="a7591-120">Incluya un paso de inicio de sesión aquí si necesita autenticar usuarios.</span><span class="sxs-lookup"><span data-stu-id="a7591-120">Include a sign-in step here if you need to authenticate users.</span></span>

### <a name="tab-configuration-modal"></a><span data-ttu-id="a7591-121">Configuración de pestañas modal</span><span class="sxs-lookup"><span data-stu-id="a7591-121">Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="El ejemplo muestra una configuración de tabulación modal." border="false":::

### <a name="anatomy-tab-configuration-modal"></a><span data-ttu-id="a7591-123">Anatomía: Configuración de pestañas modal</span><span class="sxs-lookup"><span data-stu-id="a7591-123">Anatomy: Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una configuración de pestaña modal." border="false":::

|<span data-ttu-id="a7591-125">Contador</span><span class="sxs-lookup"><span data-stu-id="a7591-125">Counter</span></span>|<span data-ttu-id="a7591-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="a7591-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a7591-127">1</span><span class="sxs-lookup"><span data-stu-id="a7591-127">1</span></span>|<span data-ttu-id="a7591-128">**Logotipo de la aplicación**: Logotipo de la aplicación a todo color de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="a7591-128">**App logo**: Full color app logo of your app.</span></span>|
|<span data-ttu-id="a7591-129">2</span><span class="sxs-lookup"><span data-stu-id="a7591-129">2</span></span>|<span data-ttu-id="a7591-130">**Nombre de la aplicación**: Nombre completo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a7591-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="a7591-131">3</span><span class="sxs-lookup"><span data-stu-id="a7591-131">3</span></span>|<span data-ttu-id="a7591-132">**iframe**: Espacio responsivo para el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a7591-132">**iframe**: Responsive space for your app’s content.</span></span> <span data-ttu-id="a7591-133">Por ejemplo, la configuración de la pestaña o la autenticación.</span><span class="sxs-lookup"><span data-stu-id="a7591-133">For example, tab settings or authentication.</span></span>|
|<span data-ttu-id="a7591-134">4 </span><span class="sxs-lookup"><span data-stu-id="a7591-134">4</span></span>|<span data-ttu-id="a7591-135">**Acerca del vínculo:** abre un cuadro de diálogo que muestra más información sobre la aplicación, como una descripción completa, los permisos requeridos por la aplicación y los vínculos a su política de privacidad y términos de servicio.</span><span class="sxs-lookup"><span data-stu-id="a7591-135">**About link**: Opens a dialog showing more information about the app, such as a full description, permissions required by the app, and links to your privacy policy and terms of service.</span></span>
|<span data-ttu-id="a7591-136">5 </span><span class="sxs-lookup"><span data-stu-id="a7591-136">5</span></span>|<span data-ttu-id="a7591-137">**Botón Cerrar**: Cierra el modal.</span><span class="sxs-lookup"><span data-stu-id="a7591-137">**Close button**: Closes the modal.</span></span>|
|<span data-ttu-id="a7591-138">6 </span><span class="sxs-lookup"><span data-stu-id="a7591-138">6</span></span>|<span data-ttu-id="a7591-139">**Notificar a los miembros** del equipo opción : El modal pregunta si desea crear una publicación que informe a otros de que agregó una pestaña.</span><span class="sxs-lookup"><span data-stu-id="a7591-139">**Notify team members option**: The modal asks if you want to create a post letting others know you added a tab.</span></span>|
|<span data-ttu-id="a7591-140">7 </span><span class="sxs-lookup"><span data-stu-id="a7591-140">7</span></span>|<span data-ttu-id="a7591-141">**Botón Atrás**: Va al paso anterior en función de dónde se abrió el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a7591-141">**Back button**: Goes to the previous step based on where the dialog opened.</span></span>|
|<span data-ttu-id="a7591-142">8 </span><span class="sxs-lookup"><span data-stu-id="a7591-142">8</span></span>|<span data-ttu-id="a7591-143">**Botón Guardar**: Completa la configuración de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="a7591-143">**Save button**: Completes tab setup.</span></span>|

### <a name="tab-authentication-with-single-sign-on"></a><span data-ttu-id="a7591-144">Autenticación de pestañas con inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="a7591-144">Tab authentication with single sign-on</span></span>

<span data-ttu-id="a7591-145">Puede agregar un paso en el que los usuarios primero deben iniciar sesión con sus credenciales de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a7591-145">You can add a step in which users must first sign in with their Microsoft credentials.</span></span> <span data-ttu-id="a7591-146">Este método de autenticación se denomina inicio de sesión único (SSO).</span><span class="sxs-lookup"><span data-stu-id="a7591-146">This authentication method is called single sign-on (SSO).</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="El ejemplo muestra una pantalla de autenticación de pestañas." border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a><span data-ttu-id="a7591-148">Diseño de una configuración de pestañas con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="a7591-148">Designing a tab setup with UI templates</span></span>

<span data-ttu-id="a7591-149">Utilice una de las siguientes plantillas de interfaz de usuario Teams para ayudar a diseñar la experiencia de configuración de la pestaña:</span><span class="sxs-lookup"><span data-stu-id="a7591-149">Use one of the following Teams UI templates to help design your tab setup experience:</span></span>

* <span data-ttu-id="a7591-150">[Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato escaneable y permitir a los usuarios realizar acciones en una lista completa o en elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="a7591-150">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="a7591-151">[Formulario](../../concepts/design/design-teams-app-ui-templates.md#form): Los formularios son para recopilar, validar y enviar la entrada del usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="a7591-151">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="a7591-152">[Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacía se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.</span><span class="sxs-lookup"><span data-stu-id="a7591-152">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="view-a-tab"></a><span data-ttu-id="a7591-153">Ver una pestaña</span><span class="sxs-lookup"><span data-stu-id="a7591-153">View a tab</span></span>

<span data-ttu-id="a7591-154">Las pestañas proporcionan una experiencia web a pantalla completa en Teams donde puede mostrar contenido colaborativo ,como tableros de tareas y paneles, e información importante.</span><span class="sxs-lookup"><span data-stu-id="a7591-154">Tabs provide a full-screen web experience in Teams where you can display collaborative content—such task boards and dashboards—and important information.</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="En el ejemplo se muestra una pestaña con un tablero de tareas." border="false":::

### <a name="anatomy-tab"></a><span data-ttu-id="a7591-156">Anatomía: Pestaña</span><span class="sxs-lookup"><span data-stu-id="a7591-156">Anatomy: Tab</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una pestaña." border="false":::

|<span data-ttu-id="a7591-158">Contador</span><span class="sxs-lookup"><span data-stu-id="a7591-158">Counter</span></span>|<span data-ttu-id="a7591-159">Descripción</span><span class="sxs-lookup"><span data-stu-id="a7591-159">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a7591-160">1</span><span class="sxs-lookup"><span data-stu-id="a7591-160">1</span></span>|<span data-ttu-id="a7591-161">**Nombre de la pestaña**: Etiqueta de navegación para la pestaña.</span><span class="sxs-lookup"><span data-stu-id="a7591-161">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="a7591-162">2</span><span class="sxs-lookup"><span data-stu-id="a7591-162">2</span></span>|<span data-ttu-id="a7591-163">**Desbordamiento de tabulación:** abre acciones de tabulación, como cambiar el nombre y quitar.</span><span class="sxs-lookup"><span data-stu-id="a7591-163">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="a7591-164">3</span><span class="sxs-lookup"><span data-stu-id="a7591-164">3</span></span>|<span data-ttu-id="a7591-165">**Chat de pestañas**: Abre un hilo de chat a la derecha, lo que permite a los usuarios tener una conversación junto al contenido.</span><span class="sxs-lookup"><span data-stu-id="a7591-165">**Tab chat**: Opens a chat thread on the right, allowing users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="a7591-166">4 </span><span class="sxs-lookup"><span data-stu-id="a7591-166">4</span></span>|<span data-ttu-id="a7591-167">**iframe**: Muestra el contenido de tu pestaña.</span><span class="sxs-lookup"><span data-stu-id="a7591-167">**iframe**: Displays your tab’s content.</span></span>

### <a name="designing-a-tab-with-ui-templates"></a><span data-ttu-id="a7591-168">Diseño de una pestaña con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="a7591-168">Designing a tab with UI templates</span></span>

<span data-ttu-id="a7591-169">Utilice una de las siguientes plantillas de interfaz de usuario Teams para ayudar a diseñar la experiencia de la pestaña:</span><span class="sxs-lookup"><span data-stu-id="a7591-169">Use one of the following Teams UI templates to help design your tab experience:</span></span>

* <span data-ttu-id="a7591-170">[Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato escaneable y permitir a los usuarios realizar acciones en una lista completa o en elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="a7591-170">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="a7591-171">[Tablero de tareas](../../concepts/design/design-teams-app-ui-templates.md#task-board): Un tablero de tareas, a veces llamado tablero kanban o carriles de natación, es una colección de tarjetas que se utilizan a menudo para rastrear el estado de los artículos de trabajo o boletos.</span><span class="sxs-lookup"><span data-stu-id="a7591-171">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="a7591-172">[Panel](../../concepts/design/design-teams-app-ui-templates.md#dashboard): Un panel es un lienzo que contiene varias tarjetas que proporcionan una visión general de los datos o el contenido.</span><span class="sxs-lookup"><span data-stu-id="a7591-172">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="a7591-173">[Formulario](../../concepts/design/design-teams-app-ui-templates.md#form): Los formularios son para recopilar, validar y enviar la entrada del usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="a7591-173">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="a7591-174">[Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacía se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.</span><span class="sxs-lookup"><span data-stu-id="a7591-174">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="a7591-175">[Navegador izquierdo](../../concepts/design/design-teams-app-ui-templates.md#left-nav): La plantilla de navegación izquierda puede ayudar si la pestaña requiere un poco de navegación.</span><span class="sxs-lookup"><span data-stu-id="a7591-175">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="a7591-176">En general, debe mantener la navegación de la pestaña al mínimo.</span><span class="sxs-lookup"><span data-stu-id="a7591-176">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-tab-to-collaborate"></a><span data-ttu-id="a7591-177">Utilice una pestaña para colaborar</span><span class="sxs-lookup"><span data-stu-id="a7591-177">Use a tab to collaborate</span></span>

<span data-ttu-id="a7591-178">Las pestañas ayudan a facilitar las conversaciones sobre el contenido en una ubicación central.</span><span class="sxs-lookup"><span data-stu-id="a7591-178">Tabs help facilitate conversations about content in a central location.</span></span>

### <a name="thread-discussion"></a><span data-ttu-id="a7591-179">Discusión de hilos</span><span class="sxs-lookup"><span data-stu-id="a7591-179">Thread discussion</span></span>

<span data-ttu-id="a7591-180">Los usuarios pueden publicar automáticamente en un canal o chat una vez que hayan agregado una nueva pestaña. Esto no solo notifica a los miembros del equipo del nuevo contenido y proporciona un enlace a la pestaña, sino que permite a las personas empezar a hablar de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="a7591-180">Users can automatically post to a channel or chat once they’ve added a new tab. This not only notifies team members of the new content and provides a link to tab, it allows people to start talking about the tab.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="En el ejemplo se muestra una pestaña que se describe en un subproceso de canal." border="false":::

### <a name="side-by-side-discussion"></a><span data-ttu-id="a7591-182">Discusión en paralelo</span><span class="sxs-lookup"><span data-stu-id="a7591-182">Side-by-side discussion</span></span>

<span data-ttu-id="a7591-183">Los usuarios pueden tener una conversación a continuación mientras ven el contenido de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="a7591-183">Users can have a conversation next while viewing the tab’s content.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="El ejemplo muestra una pestaña con un chat abierto en el lado derecho." border="false":::

### <a name="permissions-and-role-based-views"></a><span data-ttu-id="a7591-185">Permisos y vistas basadas en roles</span><span class="sxs-lookup"><span data-stu-id="a7591-185">Permissions and role-based views</span></span>

<span data-ttu-id="a7591-186">La experiencia de la pestaña puede ser diferente para los usuarios en función de sus permisos.</span><span class="sxs-lookup"><span data-stu-id="a7591-186">The tab experience may be different for users depending on their permissions.</span></span> <span data-ttu-id="a7591-187">Por ejemplo, un usuario puede acceder a la pestaña sin tener que iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="a7591-187">For example, one user can access the tab without having to sign in.</span></span> <span data-ttu-id="a7591-188">Otro usuario, sin embargo, debe firmar y verá contenido ligeramente diferente.</span><span class="sxs-lookup"><span data-stu-id="a7591-188">Another user, however, must sign and will see slightly different content.</span></span>

## <a name="manage-a-tab"></a><span data-ttu-id="a7591-189">Administrar una pestaña</span><span class="sxs-lookup"><span data-stu-id="a7591-189">Manage a tab</span></span>

<span data-ttu-id="a7591-190">Puede incluir opciones para cambiar el nombre, quitar o modificar una pestaña.</span><span class="sxs-lookup"><span data-stu-id="a7591-190">You can include options to rename, remove, or modify a tab.</span></span>

### <a name="anatomy-tab-menu"></a><span data-ttu-id="a7591-191">Anatomía: Menú tabulador</span><span class="sxs-lookup"><span data-stu-id="a7591-191">Anatomy: Tab menu</span></span>

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un menú de pestañas." border="false":::

|<span data-ttu-id="a7591-193">Contador</span><span class="sxs-lookup"><span data-stu-id="a7591-193">Counter</span></span>|<span data-ttu-id="a7591-194">Descripción</span><span class="sxs-lookup"><span data-stu-id="a7591-194">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a7591-195">1</span><span class="sxs-lookup"><span data-stu-id="a7591-195">1</span></span>|<span data-ttu-id="a7591-196">**Configuración:**(Opcional) Permite a los usuarios modificar la configuración de una pestaña después de agregarla.</span><span class="sxs-lookup"><span data-stu-id="a7591-196">**Settings**: (Optional) Allows users to modify a tab’s settings after it’s been added.</span></span>|
|<span data-ttu-id="a7591-197">2</span><span class="sxs-lookup"><span data-stu-id="a7591-197">2</span></span>|<span data-ttu-id="a7591-198">**Cambiar nombre:** permite a los usuarios dar a la pestaña un nombre más significativo para el equipo.</span><span class="sxs-lookup"><span data-stu-id="a7591-198">**Rename**: Allows users to give the tab a name that’s more meaningful to the team.</span></span>|
|<span data-ttu-id="a7591-199">3</span><span class="sxs-lookup"><span data-stu-id="a7591-199">3</span></span>|<span data-ttu-id="a7591-200">**Eliminar**: Elimina la pestaña del canal, chat o reunión.</span><span class="sxs-lookup"><span data-stu-id="a7591-200">**Remove**: Removes the tab from the channel, chat, or meeting.</span></span>|

## <a name="tab-notifications-and-deep-linking"></a><span data-ttu-id="a7591-201">Notificaciones de pestañas y vinculación profunda</span><span class="sxs-lookup"><span data-stu-id="a7591-201">Tab notifications and deep linking</span></span>

<span data-ttu-id="a7591-202">Puede enviar un mensaje con un vínculo profundo a su pestaña. Por ejemplo, una tarjeta muestra un resumen de los datos de error que un usuario puede seleccionar para ver todo el error en una pestaña. Enviar mensajes sobre la actividad de las pestañas aumenta el conocimiento sin notificar explícitamente a todos (es decir, la actividad sin ruido).</span><span class="sxs-lookup"><span data-stu-id="a7591-202">You can send a message with a deep link to your tab. For example, a card shows a summary of bug data a user can select to see the entire bug in a tab. Sending messages about tab activity increases awareness without explicitly notifying everyone (i.e., activity without noise).</span></span> <span data-ttu-id="a7591-203">También puede @mention usuarios específicos si es necesario.</span><span class="sxs-lookup"><span data-stu-id="a7591-203">You also can @mention specific users if needed.</span></span>

<span data-ttu-id="a7591-204">Notifique a los usuarios de la actividad de la pestaña de una de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="a7591-204">Notify users of tab activity one of the following ways:</span></span>

* <span data-ttu-id="a7591-205">**Bot**: Este método es preferido especialmente si el subproceso de tabulación está dirigido.</span><span class="sxs-lookup"><span data-stu-id="a7591-205">**Bot**: This method is preferred especially if the tab thread is targeted.</span></span> <span data-ttu-id="a7591-206">La conversación enhebrada de la pestaña se mueve a la vista como recientemente activa.</span><span class="sxs-lookup"><span data-stu-id="a7591-206">The tab’s threaded conversation is moved into view as recently active.</span></span> <span data-ttu-id="a7591-207">Este método también permite cierta sofisticación en la forma en que se envía la notificación.</span><span class="sxs-lookup"><span data-stu-id="a7591-207">This method also allows for some sophistication in how the notification is sent.</span></span>
* <span data-ttu-id="a7591-208">**Mensaje**: Aparece un mensaje en la fuente de actividad del usuario con un [vínculo profundo a la pestaña](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="a7591-208">**Message**: A message shows up in the user’s activity feed with a [deep link to the tab](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span></span>

## <a name="best-practices"></a><span data-ttu-id="a7591-209">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="a7591-209">Best practices</span></span>

<span data-ttu-id="a7591-210">Utilice estas recomendaciones para crear una experiencia de aplicación de calidad:</span><span class="sxs-lookup"><span data-stu-id="a7591-210">Use these recommendations to create a quality app experience:</span></span>

### <a name="collaboration"></a><span data-ttu-id="a7591-211">Colaboración</span><span class="sxs-lookup"><span data-stu-id="a7591-211">Collaboration</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="La ilustración muestra qué hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="do-facilitate-conversation"></a><span data-ttu-id="a7591-213">Hacer: Facilitar la conversación</span><span class="sxs-lookup"><span data-stu-id="a7591-213">Do: Facilitate conversation</span></span>

<span data-ttu-id="a7591-214">Incluya contenido y componentes de los que las personas puedan hablar.</span><span class="sxs-lookup"><span data-stu-id="a7591-214">Include content and components people can talk about.</span></span> <span data-ttu-id="a7591-215">Si no encaja en el contexto de un chat, canal o reunión, no pertenece a tu pestaña.</span><span class="sxs-lookup"><span data-stu-id="a7591-215">If it doesn’t fit within the context of a chat, channel, or meeting, it doesn’t belong in your tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="En el ejemplo se muestra qué no hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a><span data-ttu-id="a7591-217">No: Trata tu pestaña como cualquier otra página web</span><span class="sxs-lookup"><span data-stu-id="a7591-217">Don't: Treat your tab like any other webpage</span></span>

<span data-ttu-id="a7591-218">Una pestaña no es una página web que alguien pueda ver una vez.</span><span class="sxs-lookup"><span data-stu-id="a7591-218">A tab isn’t a webpage someone might view once.</span></span> <span data-ttu-id="a7591-219">Una pestaña debe mostrar su contenido más importante y relevante que las personas necesitan para lograr algo juntos.</span><span class="sxs-lookup"><span data-stu-id="a7591-219">A tab should display your most important, relevant content that people need to accomplish something together.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="a7591-220">Navegación</span><span class="sxs-lookup"><span data-stu-id="a7591-220">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="Ejemplo que muestra qué hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="do-limit-tasks-and-data"></a><span data-ttu-id="a7591-222">Hacer: Limitar tareas y datos</span><span class="sxs-lookup"><span data-stu-id="a7591-222">Do: Limit tasks and data</span></span>

<span data-ttu-id="a7591-223">Las pestañas funcionan mejor cuando abordan necesidades específicas.</span><span class="sxs-lookup"><span data-stu-id="a7591-223">Tabs work best when they address specific needs.</span></span> <span data-ttu-id="a7591-224">Incluya un conjunto limitado de tareas y datos relevantes para el equipo o grupo.</span><span class="sxs-lookup"><span data-stu-id="a7591-224">Include a limited set of tasks and data relevant to the team or group.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="Ilustración que muestra qué no hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="dont-embed-your-entire-app"></a><span data-ttu-id="a7591-226">No: Incrustar toda la aplicación</span><span class="sxs-lookup"><span data-stu-id="a7591-226">Don't: Embed your entire app</span></span>

<span data-ttu-id="a7591-227">El uso de una pestaña para mostrar una aplicación completa con navegación de varios niveles e interacciones complejas conduce a la sobrecarga de información.</span><span class="sxs-lookup"><span data-stu-id="a7591-227">Using a tab to display an entire app with multi-level navigation and complex interactions leads to information overload.</span></span>

   :::column-end:::
:::row-end:::

### <a name="setup"></a><span data-ttu-id="a7591-228">Instalación</span><span class="sxs-lookup"><span data-stu-id="a7591-228">Setup</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="Ilustración que muestra qué hacer con el diseño de configuración de pestañas." border="false":::

#### <a name="do-keep-it-simple"></a><span data-ttu-id="a7591-230">Hacer: Mantenlo simple</span><span class="sxs-lookup"><span data-stu-id="a7591-230">Do: Keep it simple</span></span>

<span data-ttu-id="a7591-231">Si la aplicación requiere autenticación, intente integrar el inicio de sesión único (SSO) de Microsoft para obtener una experiencia de inicio de sesión más fluida.</span><span class="sxs-lookup"><span data-stu-id="a7591-231">If your app requires authentication, try integrating Microsoft single sign-on (SSO) for a more seamless sign-in experience.</span></span> <span data-ttu-id="a7591-232">Además, solo incluya información esencial y pasos para agregar la pestaña.</span><span class="sxs-lookup"><span data-stu-id="a7591-232">Also, only include essential information and steps to add the tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="Ilustración que muestra qué no hacer con el diseño de configuración de pestañas." border="false":::

#### <a name="dont-have-too-many-steps"></a><span data-ttu-id="a7591-234">No: Tener demasiados pasos</span><span class="sxs-lookup"><span data-stu-id="a7591-234">Don't: Have too many steps</span></span>

<span data-ttu-id="a7591-235">Elimine los pasos innecesarios para agregar una pestaña.</span><span class="sxs-lookup"><span data-stu-id="a7591-235">Remove any unnecessary steps for adding a tab.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="a7591-236">Creación de temas</span><span class="sxs-lookup"><span data-stu-id="a7591-236">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="Ilustración que muestra qué hacer con el temática de pestañas." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="a7591-238">Hacer: Aproveche Teams tokens de color</span><span class="sxs-lookup"><span data-stu-id="a7591-238">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="a7591-239">Cada tema Teams tiene su propio esquema de color.</span><span class="sxs-lookup"><span data-stu-id="a7591-239">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="a7591-240">Para controlar los cambios de tema automáticamente, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">tokens de color (interfaz de usuario fluida)</a> en el diseño.</span><span class="sxs-lookup"><span data-stu-id="a7591-240">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="Ilustración que muestra qué no hacer con el temática de pestañas." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="a7591-242">No: Valores de color de código duro</span><span class="sxs-lookup"><span data-stu-id="a7591-242">Don't: Hard code color values</span></span>

<span data-ttu-id="a7591-243">Si no usa tokens de color Teams, sus diseños serán menos escalables y tardarán más tiempo en administrarse.</span><span class="sxs-lookup"><span data-stu-id="a7591-243">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

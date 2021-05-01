---
title: Diseño de la pestaña para escritorio y web
description: Obtén información sobre cómo diseñar una Teams (escritorio y web) y obtener el kit Microsoft Teams interfaz de usuario.
author: heath-hamilton
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 9dc5489f4a6a4c6f0e1188250a9e2a9bc5793690
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101852"
---
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a><span data-ttu-id="dcba8-103">Diseño de la pestaña para Microsoft Teams escritorio y web</span><span class="sxs-lookup"><span data-stu-id="dcba8-103">Designing your tab for Microsoft Teams desktop and web</span></span>

<span data-ttu-id="dcba8-104">Una pestaña es un lienzo grande para el contenido.</span><span class="sxs-lookup"><span data-stu-id="dcba8-104">A tab is a large canvas for your content.</span></span> <span data-ttu-id="dcba8-105">Para guiar el diseño de la aplicación, la siguiente información describe e ilustra cómo los usuarios pueden agregar, usar y administrar pestañas en Teams.</span><span class="sxs-lookup"><span data-stu-id="dcba8-105">To guide your app design, the following information describes and illustrates how people can add, use, and manage tabs in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="dcba8-106">Kit de UI de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="dcba8-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="dcba8-107">Puedes encontrar instrucciones completas de diseño de pestañas, incluidos los elementos que puedes agarrar y modificar según sea necesario, en el kit de interfaz Microsoft Teams usuario.</span><span class="sxs-lookup"><span data-stu-id="dcba8-107">You can find comprehensive tab design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="dcba8-108">El kit de interfaz de usuario también tiene temas esenciales, como la accesibilidad y el tamaño dinámico que no se tratan aquí.</span><span class="sxs-lookup"><span data-stu-id="dcba8-108">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dcba8-109">Obtener el Kit de UI de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="dcba8-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a><span data-ttu-id="dcba8-110">Agregar una pestaña</span><span class="sxs-lookup"><span data-stu-id="dcba8-110">Add a tab</span></span>

<span data-ttu-id="dcba8-111">Puedes agregar una pestaña desde el almacén Teams (AppSource) o en uno de los siguientes contextos:</span><span class="sxs-lookup"><span data-stu-id="dcba8-111">You can add a tab from the Teams store (AppSource) or in one of the following contexts:</span></span>

* <span data-ttu-id="dcba8-112">Chat</span><span class="sxs-lookup"><span data-stu-id="dcba8-112">Chat</span></span>
* <span data-ttu-id="dcba8-113">Canal</span><span class="sxs-lookup"><span data-stu-id="dcba8-113">Channel</span></span>
* <span data-ttu-id="dcba8-114">Reunión (antes, durante o después de la reunión)</span><span class="sxs-lookup"><span data-stu-id="dcba8-114">Meeting (before, during, or after the meeting)</span></span>

<span data-ttu-id="dcba8-115">En el ejemplo siguiente se muestra cómo se agrega una pestaña en un canal.</span><span class="sxs-lookup"><span data-stu-id="dcba8-115">The following example shows how a tab is added in a channel.</span></span>

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="En el ejemplo se muestra una pestaña que se agrega en un canal." border="false":::

## <a name="set-up-a-tab"></a><span data-ttu-id="dcba8-117">Configurar una pestaña</span><span class="sxs-lookup"><span data-stu-id="dcba8-117">Set up a tab</span></span>

<span data-ttu-id="dcba8-118">Hay un breve proceso de configuración para agregar una aplicación como un canal, chat o pestaña de reunión. La experiencia está en gran medida a su medida.</span><span class="sxs-lookup"><span data-stu-id="dcba8-118">There's a short setup process to add an app as a channel, chat, or meeting tab. The experience is largely up to you.</span></span> <span data-ttu-id="dcba8-119">Por ejemplo, podrías tener una descripción de cómo usar la aplicación y algunas opciones de configuración opcionales.</span><span class="sxs-lookup"><span data-stu-id="dcba8-119">For example, you could have a description of how to use the app and some optional settings.</span></span> <span data-ttu-id="dcba8-120">Incluye un paso de inicio de sesión aquí si necesitas autenticar usuarios.</span><span class="sxs-lookup"><span data-stu-id="dcba8-120">Include a sign-in step here if you need to authenticate users.</span></span>

### <a name="tab-configuration-modal"></a><span data-ttu-id="dcba8-121">Modal de configuración de tabulación</span><span class="sxs-lookup"><span data-stu-id="dcba8-121">Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="En el ejemplo se muestra un modal de configuración de tabulación." border="false":::

### <a name="anatomy-tab-configuration-modal"></a><span data-ttu-id="dcba8-123">Anatomía: modal de configuración de tabulación</span><span class="sxs-lookup"><span data-stu-id="dcba8-123">Anatomy: Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un modal de configuración de tabulación." border="false":::

|<span data-ttu-id="dcba8-125">Contador</span><span class="sxs-lookup"><span data-stu-id="dcba8-125">Counter</span></span>|<span data-ttu-id="dcba8-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="dcba8-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="dcba8-127">1</span><span class="sxs-lookup"><span data-stu-id="dcba8-127">1</span></span>|<span data-ttu-id="dcba8-128">**Logotipo de la** aplicación: logotipo de aplicación a todo color de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dcba8-128">**App logo**: Full color app logo of your app.</span></span>|
|<span data-ttu-id="dcba8-129">2</span><span class="sxs-lookup"><span data-stu-id="dcba8-129">2</span></span>|<span data-ttu-id="dcba8-130">**Nombre de la** aplicación: nombre completo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dcba8-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="dcba8-131">3</span><span class="sxs-lookup"><span data-stu-id="dcba8-131">3</span></span>|<span data-ttu-id="dcba8-132">**iframe:** espacio dinámico para el contenido de la aplicación (por ejemplo, configuración de pestañas o autenticación).</span><span class="sxs-lookup"><span data-stu-id="dcba8-132">**iframe**: Responsive space for your app’s content (for example, tab settings or authentication).</span></span>|
|<span data-ttu-id="dcba8-133">4 </span><span class="sxs-lookup"><span data-stu-id="dcba8-133">4</span></span>|<span data-ttu-id="dcba8-134">**Acerca del vínculo:** abre un cuadro de diálogo que muestra más información sobre la aplicación, como una descripción completa, los permisos requeridos por la aplicación y los vínculos a la directiva de privacidad y los términos de servicio.</span><span class="sxs-lookup"><span data-stu-id="dcba8-134">**About link**: Opens a dialog showing more information about the app, such as a full description, permissions required by the app, and links to your privacy policy and terms of service.</span></span>
|<span data-ttu-id="dcba8-135">5 </span><span class="sxs-lookup"><span data-stu-id="dcba8-135">5</span></span>|<span data-ttu-id="dcba8-136">**Botón Cerrar:** cierra el modal.</span><span class="sxs-lookup"><span data-stu-id="dcba8-136">**Close button**: Closes the modal.</span></span>|
|<span data-ttu-id="dcba8-137">6 </span><span class="sxs-lookup"><span data-stu-id="dcba8-137">6</span></span>|<span data-ttu-id="dcba8-138">**Notificar a los miembros del equipo** opción: el modal pregunta si desea crear una publicación para que otros sepan que agregó una pestaña.</span><span class="sxs-lookup"><span data-stu-id="dcba8-138">**Notify team members option**: The modal asks if you want to create a post letting others know you added a tab.</span></span>|
|<span data-ttu-id="dcba8-139">7 </span><span class="sxs-lookup"><span data-stu-id="dcba8-139">7</span></span>|<span data-ttu-id="dcba8-140">**Botón Atrás:** va al paso anterior en función de dónde se abrió el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dcba8-140">**Back button**: Goes to the previous step based on where the dialog opened.</span></span>|
|<span data-ttu-id="dcba8-141">8 </span><span class="sxs-lookup"><span data-stu-id="dcba8-141">8</span></span>|<span data-ttu-id="dcba8-142">**Botón Guardar:** completa la configuración de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="dcba8-142">**Save button**: Completes tab setup.</span></span>|

### <a name="tab-authentication-with-single-sign-on"></a><span data-ttu-id="dcba8-143">Autenticación de tabulación con inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="dcba8-143">Tab authentication with single sign-on</span></span>

<span data-ttu-id="dcba8-144">Puede agregar un paso en el que los usuarios primero deben iniciar sesión con sus credenciales de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dcba8-144">You can add a step in which users must first sign in with their Microsoft credentials.</span></span> <span data-ttu-id="dcba8-145">Este método de autenticación se denomina inicio de sesión único (SSO).</span><span class="sxs-lookup"><span data-stu-id="dcba8-145">This authentication method is called single sign-on (SSO).</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="En el ejemplo se muestra una pantalla de autenticación de tabulación." border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a><span data-ttu-id="dcba8-147">Diseño de una configuración de pestaña con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="dcba8-147">Designing a tab setup with UI templates</span></span>

<span data-ttu-id="dcba8-148">Usa una de las siguientes plantillas Teams interfaz de usuario para ayudar a diseñar la experiencia de configuración de pestañas:</span><span class="sxs-lookup"><span data-stu-id="dcba8-148">Use one of the following Teams UI templates to help design your tab setup experience:</span></span>

* <span data-ttu-id="dcba8-149">[Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato digitalizado y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="dcba8-149">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="dcba8-150">[Formulario:](../../concepts/design/design-teams-app-ui-templates.md#form)los formularios son para recopilar, validar y enviar la entrada del usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="dcba8-150">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="dcba8-151">[Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacío se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.</span><span class="sxs-lookup"><span data-stu-id="dcba8-151">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="view-a-tab"></a><span data-ttu-id="dcba8-152">Ver una pestaña</span><span class="sxs-lookup"><span data-stu-id="dcba8-152">View a tab</span></span>

<span data-ttu-id="dcba8-153">Las pestañas proporcionan una experiencia web a pantalla completa en Teams donde puede mostrar contenido de colaboración (como paneles de tareas y paneles) e información importante.</span><span class="sxs-lookup"><span data-stu-id="dcba8-153">Tabs provide a full-screen web experience in Teams where you can display collaborative content—such task boards and dashboards—and important information.</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="En el ejemplo se muestra una pestaña con un panel de tareas." border="false":::

### <a name="anatomy-tab"></a><span data-ttu-id="dcba8-155">Anatomía: Ficha</span><span class="sxs-lookup"><span data-stu-id="dcba8-155">Anatomy: Tab</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una pestaña." border="false":::

|<span data-ttu-id="dcba8-157">Contador</span><span class="sxs-lookup"><span data-stu-id="dcba8-157">Counter</span></span>|<span data-ttu-id="dcba8-158">Descripción</span><span class="sxs-lookup"><span data-stu-id="dcba8-158">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="dcba8-159">1</span><span class="sxs-lookup"><span data-stu-id="dcba8-159">1</span></span>|<span data-ttu-id="dcba8-160">**Nombre de la pestaña:** etiqueta de navegación para la pestaña.</span><span class="sxs-lookup"><span data-stu-id="dcba8-160">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="dcba8-161">2</span><span class="sxs-lookup"><span data-stu-id="dcba8-161">2</span></span>|<span data-ttu-id="dcba8-162">**Desbordamiento de** tabulación: abre acciones de tabulación, como cambiar el nombre y quitar.</span><span class="sxs-lookup"><span data-stu-id="dcba8-162">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="dcba8-163">3</span><span class="sxs-lookup"><span data-stu-id="dcba8-163">3</span></span>|<span data-ttu-id="dcba8-164">**Chat de pestaña:** abre un subproceso de chat a la derecha, lo que permite a los usuarios tener una conversación junto al contenido.</span><span class="sxs-lookup"><span data-stu-id="dcba8-164">**Tab chat**: Opens a chat thread on the right, allowing users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="dcba8-165">4 </span><span class="sxs-lookup"><span data-stu-id="dcba8-165">4</span></span>|<span data-ttu-id="dcba8-166">**iframe:** muestra el contenido de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="dcba8-166">**iframe**: Displays your tab’s content.</span></span>

### <a name="designing-a-tab-with-ui-templates"></a><span data-ttu-id="dcba8-167">Diseño de una pestaña con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="dcba8-167">Designing a tab with UI templates</span></span>

<span data-ttu-id="dcba8-168">Usa una de las siguientes plantillas Teams interfaz de usuario para ayudar a diseñar la experiencia de pestaña:</span><span class="sxs-lookup"><span data-stu-id="dcba8-168">Use one of the following Teams UI templates to help design your tab experience:</span></span>

* <span data-ttu-id="dcba8-169">[Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato digitalizado y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="dcba8-169">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="dcba8-170">[Panel de](../../concepts/design/design-teams-app-ui-templates.md#task-board)tareas: un panel de tareas, a veces denominado tablero de kanban o carriles de natación, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o los vales.</span><span class="sxs-lookup"><span data-stu-id="dcba8-170">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="dcba8-171">[Panel:](../../concepts/design/design-teams-app-ui-templates.md#dashboard)un panel es un lienzo que contiene varias tarjetas que proporcionan información general sobre los datos o el contenido.</span><span class="sxs-lookup"><span data-stu-id="dcba8-171">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="dcba8-172">[Formulario:](../../concepts/design/design-teams-app-ui-templates.md#form)los formularios son para recopilar, validar y enviar la entrada del usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="dcba8-172">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="dcba8-173">[Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacío se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.</span><span class="sxs-lookup"><span data-stu-id="dcba8-173">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="dcba8-174">[Navegación izquierda:](../../concepts/design/design-teams-app-ui-templates.md#left-nav)la plantilla de navegación izquierda puede ayudar si la pestaña requiere algo de navegación.</span><span class="sxs-lookup"><span data-stu-id="dcba8-174">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="dcba8-175">En general, debe mantener la navegación por pestañas al mínimo.</span><span class="sxs-lookup"><span data-stu-id="dcba8-175">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-tab-to-collaborate"></a><span data-ttu-id="dcba8-176">Usar una pestaña para colaborar</span><span class="sxs-lookup"><span data-stu-id="dcba8-176">Use a tab to collaborate</span></span>

<span data-ttu-id="dcba8-177">Las pestañas ayudan a facilitar las conversaciones sobre el contenido en una ubicación central.</span><span class="sxs-lookup"><span data-stu-id="dcba8-177">Tabs help facilitate conversations about content in a central location.</span></span>

### <a name="thread-discussion"></a><span data-ttu-id="dcba8-178">Discusión de subprocesos</span><span class="sxs-lookup"><span data-stu-id="dcba8-178">Thread discussion</span></span>

<span data-ttu-id="dcba8-179">Los usuarios pueden publicar automáticamente en un canal o chat una vez que han agregado una nueva pestaña. Esto no solo notifica a los miembros del equipo del nuevo contenido y proporciona un vínculo a la pestaña, sino que permite a los usuarios empezar a hablar sobre la pestaña.</span><span class="sxs-lookup"><span data-stu-id="dcba8-179">Users can automatically post to a channel or chat once they’ve added a new tab. This not only notifies team members of the new content and provides a link to tab, it allows people to start talking about the tab.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="En el ejemplo se muestra una pestaña que se está analizando en un subproceso de canal." border="false":::

### <a name="side-by-side-discussion"></a><span data-ttu-id="dcba8-181">Discusión en paralelo</span><span class="sxs-lookup"><span data-stu-id="dcba8-181">Side-by-side discussion</span></span>

<span data-ttu-id="dcba8-182">Los usuarios pueden tener una conversación a continuación mientras ven el contenido de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="dcba8-182">Users can have a conversation next while viewing the tab’s content.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="En el ejemplo se muestra una pestaña con un chat abierto en el lado derecho." border="false":::

### <a name="permissions-and-role-based-views"></a><span data-ttu-id="dcba8-184">Permisos y vistas basadas en roles</span><span class="sxs-lookup"><span data-stu-id="dcba8-184">Permissions and role-based views</span></span>

<span data-ttu-id="dcba8-185">La experiencia de pestaña puede ser diferente para los usuarios en función de sus permisos.</span><span class="sxs-lookup"><span data-stu-id="dcba8-185">The tab experience may be different for users depending on their permissions.</span></span> <span data-ttu-id="dcba8-186">Por ejemplo, un usuario puede tener acceso a la pestaña sin tener que iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="dcba8-186">For example, one user can access the tab without having to sign in.</span></span> <span data-ttu-id="dcba8-187">Sin embargo, otro usuario debe firmar y verá contenido ligeramente diferente.</span><span class="sxs-lookup"><span data-stu-id="dcba8-187">Another user, however, must sign and will see slightly different content.</span></span>

## <a name="manage-a-tab"></a><span data-ttu-id="dcba8-188">Administrar una pestaña</span><span class="sxs-lookup"><span data-stu-id="dcba8-188">Manage a tab</span></span>

<span data-ttu-id="dcba8-189">Puede incluir opciones para cambiar el nombre, quitar o modificar una pestaña.</span><span class="sxs-lookup"><span data-stu-id="dcba8-189">You can include options to rename, remove, or modify a tab.</span></span>

### <a name="anatomy-tab-menu"></a><span data-ttu-id="dcba8-190">Anatomía: menú De pestaña</span><span class="sxs-lookup"><span data-stu-id="dcba8-190">Anatomy: Tab menu</span></span>

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un menú de pestaña." border="false":::

|<span data-ttu-id="dcba8-192">Contador</span><span class="sxs-lookup"><span data-stu-id="dcba8-192">Counter</span></span>|<span data-ttu-id="dcba8-193">Descripción</span><span class="sxs-lookup"><span data-stu-id="dcba8-193">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="dcba8-194">1</span><span class="sxs-lookup"><span data-stu-id="dcba8-194">1</span></span>|<span data-ttu-id="dcba8-195">**Configuración**: (opcional) Permite a los usuarios modificar la configuración de una pestaña después de agregarla.</span><span class="sxs-lookup"><span data-stu-id="dcba8-195">**Settings**: (Optional) Allows users to modify a tab’s settings after it’s been added.</span></span>|
|<span data-ttu-id="dcba8-196">2</span><span class="sxs-lookup"><span data-stu-id="dcba8-196">2</span></span>|<span data-ttu-id="dcba8-197">**Cambiar** nombre: permite a los usuarios dar a la pestaña un nombre que sea más significativo para el equipo.</span><span class="sxs-lookup"><span data-stu-id="dcba8-197">**Rename**: Allows users to give the tab a name that’s more meaningful to the team.</span></span>|
|<span data-ttu-id="dcba8-198">3</span><span class="sxs-lookup"><span data-stu-id="dcba8-198">3</span></span>|<span data-ttu-id="dcba8-199">**Quitar:** quita la pestaña del canal, chat o reunión.</span><span class="sxs-lookup"><span data-stu-id="dcba8-199">**Remove**: Removes the tab from the channel, chat, or meeting.</span></span>|

## <a name="tab-notifications-and-deep-linking"></a><span data-ttu-id="dcba8-200">Notificaciones de tabulación y vinculación profunda</span><span class="sxs-lookup"><span data-stu-id="dcba8-200">Tab notifications and deep linking</span></span>

<span data-ttu-id="dcba8-201">Puede enviar un mensaje con un vínculo profundo a la pestaña. Por ejemplo, una tarjeta muestra un resumen de los datos de errores que un usuario puede seleccionar para ver el error completo en una pestaña. El envío de mensajes sobre la actividad de tabulación aumenta el conocimiento sin notificar explícitamente a todos (es decir, actividad sin ruido).</span><span class="sxs-lookup"><span data-stu-id="dcba8-201">You can send a message with a deep link to your tab. For example, a card shows a summary of bug data a user can select to see the entire bug in a tab. Sending messages about tab activity increases awareness without explicitly notifying everyone (i.e., activity without noise).</span></span> <span data-ttu-id="dcba8-202">También puede usar @mention usuarios específicos si es necesario.</span><span class="sxs-lookup"><span data-stu-id="dcba8-202">You also can @mention specific users if needed.</span></span>

<span data-ttu-id="dcba8-203">Notificar a los usuarios sobre la actividad de tabulación de una de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="dcba8-203">Notify users of tab activity one of the following ways:</span></span>

* <span data-ttu-id="dcba8-204">**Bot:** este método se prefiere especialmente si el subproceso de tabulación está dirigido.</span><span class="sxs-lookup"><span data-stu-id="dcba8-204">**Bot**: This method is preferred especially if the tab thread is targeted.</span></span> <span data-ttu-id="dcba8-205">La conversación enhebrada de la pestaña se mueve a la vista como activa recientemente.</span><span class="sxs-lookup"><span data-stu-id="dcba8-205">The tab’s threaded conversation is moved into view as recently active.</span></span> <span data-ttu-id="dcba8-206">Este método también permite cierta sofisticación en la forma en que se envía la notificación.</span><span class="sxs-lookup"><span data-stu-id="dcba8-206">This method also allows for some sophistication in how the notification is sent.</span></span>
* <span data-ttu-id="dcba8-207">**Mensaje:** aparece un mensaje en la fuente de actividad del usuario con un vínculo profundo a [la pestaña](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="dcba8-207">**Message**: A message shows up in the user’s activity feed with a [deep link to the tab](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span></span>

## <a name="best-practices"></a><span data-ttu-id="dcba8-208">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="dcba8-208">Best practices</span></span>

<span data-ttu-id="dcba8-209">Usa estas recomendaciones para crear una experiencia de aplicación de calidad.</span><span class="sxs-lookup"><span data-stu-id="dcba8-209">Use these recommendations to create a quality app experience.</span></span>

### <a name="collaboration"></a><span data-ttu-id="dcba8-210">Colaboración</span><span class="sxs-lookup"><span data-stu-id="dcba8-210">Collaboration</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="La ilustración muestra qué hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="do-facilitate-conversation"></a><span data-ttu-id="dcba8-212">Hacer: facilitar la conversación</span><span class="sxs-lookup"><span data-stu-id="dcba8-212">Do: Facilitate conversation</span></span>

<span data-ttu-id="dcba8-213">Incluir contenido y componentes de los que los usuarios puedan hablar.</span><span class="sxs-lookup"><span data-stu-id="dcba8-213">Include content and components people can talk about.</span></span> <span data-ttu-id="dcba8-214">Si no cabe en el contexto de un chat, canal o reunión, no pertenece a la pestaña.</span><span class="sxs-lookup"><span data-stu-id="dcba8-214">If it doesn’t fit within the context of a chat, channel, or meeting, it doesn’t belong in your tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="En el ejemplo se muestra lo que no se debe hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a><span data-ttu-id="dcba8-216">No: trate la pestaña como cualquier otra página web</span><span class="sxs-lookup"><span data-stu-id="dcba8-216">Don't: Treat your tab like any other webpage</span></span>

<span data-ttu-id="dcba8-217">Una pestaña no es una página web que alguien pueda ver una vez.</span><span class="sxs-lookup"><span data-stu-id="dcba8-217">A tab isn’t a webpage someone might view once.</span></span> <span data-ttu-id="dcba8-218">Una pestaña debe mostrar el contenido más importante y relevante que los usuarios necesitan para lograr algo juntos.</span><span class="sxs-lookup"><span data-stu-id="dcba8-218">A tab should display your most important, relevant content that people need to accomplish something together.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="dcba8-219">Navegación</span><span class="sxs-lookup"><span data-stu-id="dcba8-219">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="Ejemplo que muestra qué hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="do-limit-tasks-and-data"></a><span data-ttu-id="dcba8-221">Hacer: limitar tareas y datos</span><span class="sxs-lookup"><span data-stu-id="dcba8-221">Do: Limit tasks and data</span></span>

<span data-ttu-id="dcba8-222">Las pestañas funcionan mejor cuando se abordan necesidades específicas.</span><span class="sxs-lookup"><span data-stu-id="dcba8-222">Tabs work best when they address specific needs.</span></span> <span data-ttu-id="dcba8-223">Incluya un conjunto limitado de tareas y datos relevantes para el equipo o grupo.</span><span class="sxs-lookup"><span data-stu-id="dcba8-223">Include a limited set of tasks and data relevant to the team or group.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="Ilustración que muestra qué no hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="dont-embed-your-entire-app"></a><span data-ttu-id="dcba8-225">No: insertar toda la aplicación</span><span class="sxs-lookup"><span data-stu-id="dcba8-225">Don't: Embed your entire app</span></span>

<span data-ttu-id="dcba8-226">El uso de una pestaña para mostrar una aplicación completa con navegación de varios niveles e interacciones complejas conduce a una sobrecarga de información.</span><span class="sxs-lookup"><span data-stu-id="dcba8-226">Using a tab to display an entire app with multi-level navigation and complex interactions leads to information overload.</span></span>

   :::column-end:::
:::row-end:::

### <a name="setup"></a><span data-ttu-id="dcba8-227">Instalación</span><span class="sxs-lookup"><span data-stu-id="dcba8-227">Setup</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="Ilustración que muestra qué hacer con el diseño de configuración de pestañas." border="false":::

#### <a name="do-keep-it-simple"></a><span data-ttu-id="dcba8-229">Do: Keep it simple</span><span class="sxs-lookup"><span data-stu-id="dcba8-229">Do: Keep it simple</span></span>

<span data-ttu-id="dcba8-230">Si la aplicación requiere autenticación, intenta integrar el inicio de sesión único (SSO) de Microsoft para una experiencia de inicio de sesión más fluida.</span><span class="sxs-lookup"><span data-stu-id="dcba8-230">If your app requires authentication, try integrating Microsoft single sign-on (SSO) for a more seamless sign-in experience.</span></span> <span data-ttu-id="dcba8-231">Además, solo incluya información esencial y pasos para agregar la pestaña.</span><span class="sxs-lookup"><span data-stu-id="dcba8-231">Also, only include essential information and steps to add the tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="Ilustración que muestra qué no hacer con el diseño de configuración de pestañas." border="false":::

#### <a name="dont-have-too-many-steps"></a><span data-ttu-id="dcba8-233">No: tener demasiados pasos</span><span class="sxs-lookup"><span data-stu-id="dcba8-233">Don't: Have too many steps</span></span>

<span data-ttu-id="dcba8-234">Quite los pasos innecesarios para agregar una pestaña.</span><span class="sxs-lookup"><span data-stu-id="dcba8-234">Remove any unnecessary steps for adding a tab.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="dcba8-235">Creación de temas</span><span class="sxs-lookup"><span data-stu-id="dcba8-235">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="Ilustración que muestra qué hacer con el tema de tabulación." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="dcba8-237">Hacer: aprovechar las ventajas de Teams de color</span><span class="sxs-lookup"><span data-stu-id="dcba8-237">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="dcba8-238">Cada Teams tema tiene su propia combinación de colores.</span><span class="sxs-lookup"><span data-stu-id="dcba8-238">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="dcba8-239">Para controlar los cambios de tema automáticamente, usa <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">tokens de color (Fluent UI)</a> en el diseño.</span><span class="sxs-lookup"><span data-stu-id="dcba8-239">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="Ilustración que muestra lo que no se debe hacer con el tema de tabulación." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="dcba8-241">No: valores de color de código duro</span><span class="sxs-lookup"><span data-stu-id="dcba8-241">Don't: Hard code color values</span></span>

<span data-ttu-id="dcba8-242">Si no usas tokens Teams de color, tus diseños serán menos escalables y tendrán más tiempo para administrar.</span><span class="sxs-lookup"><span data-stu-id="dcba8-242">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

---
title: Diseño de la pestaña para escritorio y Web
description: Obtenga información sobre cómo diseñar una pestaña de Microsoft Teams (escritorio y Web) y obtener el kit de interfaz de usuario de Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 692a21c78dc86cbca5bf248e55d0332bd71c6b92
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604704"
---
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a><span data-ttu-id="0abe2-103">Diseño de la pestaña para escritorio y Web de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0abe2-103">Designing your tab for Microsoft Teams desktop and web</span></span>

<span data-ttu-id="0abe2-104">Una pestaña es un gran lienzo para contenido que facilita la colaboración.</span><span class="sxs-lookup"><span data-stu-id="0abe2-104">A tab is a large canvas for content that facilitates collaboration.</span></span> <span data-ttu-id="0abe2-105">Para guiar el diseño de la aplicación, la siguiente información describe e ilustra cómo los usuarios pueden agregar, usar y administrar pestañas en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0abe2-105">To guide your app design, the following information describes and illustrates how people can add, use, and manage tabs in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="0abe2-106">Kit de IU de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0abe2-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="0abe2-107">Puede encontrar instrucciones detalladas para el diseño de pestañas, incluidos los elementos que puede captar y modificar según sea necesario, en el kit de interfaz de usuario de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0abe2-107">You can find comprehensive tab design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="0abe2-108">El kit de UI también tiene temas esenciales, como la accesibilidad y el tamaño de respuesta, que no se cubren aquí.</span><span class="sxs-lookup"><span data-stu-id="0abe2-108">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0abe2-109">Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="0abe2-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a><span data-ttu-id="0abe2-110">Agregar una pestaña</span><span class="sxs-lookup"><span data-stu-id="0abe2-110">Add a tab</span></span>

<span data-ttu-id="0abe2-111">Puede Agregar una pestaña desde el almacén de Microsoft Teams (AppSource) o en uno de los siguientes contextos:</span><span class="sxs-lookup"><span data-stu-id="0abe2-111">You can add a tab from the Teams store (AppSource) or in one of the following contexts:</span></span>

* <span data-ttu-id="0abe2-112">Chat</span><span class="sxs-lookup"><span data-stu-id="0abe2-112">Chat</span></span>
* <span data-ttu-id="0abe2-113">Canal</span><span class="sxs-lookup"><span data-stu-id="0abe2-113">Channel</span></span>
* <span data-ttu-id="0abe2-114">Reunión (antes, durante o después de la reunión)</span><span class="sxs-lookup"><span data-stu-id="0abe2-114">Meeting (before, during, or after the meeting)</span></span>

<span data-ttu-id="0abe2-115">En el siguiente ejemplo se muestra cómo se agrega una pestaña en un canal.</span><span class="sxs-lookup"><span data-stu-id="0abe2-115">The following example shows how a tab is added in a channel.</span></span>

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="Ejemplo muestra una pestaña agregada en un canal." border="false":::

## <a name="set-up-a-tab"></a><span data-ttu-id="0abe2-117">Configurar una pestaña</span><span class="sxs-lookup"><span data-stu-id="0abe2-117">Set up a tab</span></span>

<span data-ttu-id="0abe2-118">Hay un proceso de instalación breve para agregar una aplicación como una pestaña de canal, chat o reunión. La experiencia depende en gran medida del usuario.</span><span class="sxs-lookup"><span data-stu-id="0abe2-118">There's a short setup process to add an app as a channel, chat, or meeting tab. The experience is largely up to you.</span></span> <span data-ttu-id="0abe2-119">Por ejemplo, puede tener una descripción de cómo usar la aplicación y algunos parámetros opcionales.</span><span class="sxs-lookup"><span data-stu-id="0abe2-119">For example, you could have a description of how to use the app and some optional settings.</span></span> <span data-ttu-id="0abe2-120">Incluya un paso de inicio de sesión aquí si necesita autenticar usuarios.</span><span class="sxs-lookup"><span data-stu-id="0abe2-120">Include a sign-in step here if you need to authenticate users.</span></span>

### <a name="tab-configuration-modal"></a><span data-ttu-id="0abe2-121">Ficha modal de configuración</span><span class="sxs-lookup"><span data-stu-id="0abe2-121">Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="Ejemplo muestra un modal de configuración de ficha." border="false":::

### <a name="anatomy-tab-configuration-modal"></a><span data-ttu-id="0abe2-123">Anatomía: configuración de pestaña modal</span><span class="sxs-lookup"><span data-stu-id="0abe2-123">Anatomy: Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un modal de configuración de ficha." border="false":::

|<span data-ttu-id="0abe2-125">Counter</span><span class="sxs-lookup"><span data-stu-id="0abe2-125">Counter</span></span>|<span data-ttu-id="0abe2-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="0abe2-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="0abe2-127">1</span><span class="sxs-lookup"><span data-stu-id="0abe2-127">1</span></span>|<span data-ttu-id="0abe2-128">**Logotipo** de la aplicación: logotipo de aplicación a todo color de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0abe2-128">**App logo**: Full color app logo of your app.</span></span>|
|<span data-ttu-id="0abe2-129">2 </span><span class="sxs-lookup"><span data-stu-id="0abe2-129">2</span></span>|<span data-ttu-id="0abe2-130">**Nombre** de la aplicación: nombre completo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0abe2-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="0abe2-131">3 </span><span class="sxs-lookup"><span data-stu-id="0abe2-131">3</span></span>|<span data-ttu-id="0abe2-132">**iframe**: espacio de respuesta para el contenido de la aplicación (por ejemplo, la configuración de la pestaña o la autenticación).</span><span class="sxs-lookup"><span data-stu-id="0abe2-132">**iframe**: Responsive space for your app’s content (for example, tab settings or authentication).</span></span>|
|<span data-ttu-id="0abe2-133">4 </span><span class="sxs-lookup"><span data-stu-id="0abe2-133">4</span></span>|<span data-ttu-id="0abe2-134">**Acerca del vínculo**: abre un cuadro de diálogo que muestra más información sobre la aplicación, como una descripción completa, los permisos requeridos por la aplicación y los vínculos a la Directiva de privacidad y los términos de servicio.</span><span class="sxs-lookup"><span data-stu-id="0abe2-134">**About link**: Opens a dialog showing more information about the app, such as a full description, permissions required by the app, and links to your privacy policy and terms of service.</span></span>
|<span data-ttu-id="0abe2-135">5 </span><span class="sxs-lookup"><span data-stu-id="0abe2-135">5</span></span>|<span data-ttu-id="0abe2-136">**Botón Cerrar**: cierra el modal.</span><span class="sxs-lookup"><span data-stu-id="0abe2-136">**Close button**: Closes the modal.</span></span>|
|<span data-ttu-id="0abe2-137">6 </span><span class="sxs-lookup"><span data-stu-id="0abe2-137">6</span></span>|<span data-ttu-id="0abe2-138">**Opción notificar a los integrantes del equipo**: el modal le preguntará si desea crear una publicación que permita a otros usuarios saber que ha agregado una pestaña.</span><span class="sxs-lookup"><span data-stu-id="0abe2-138">**Notify team members option**: The modal asks if you want to create a post letting others know you added a tab.</span></span>|
|<span data-ttu-id="0abe2-139">7 </span><span class="sxs-lookup"><span data-stu-id="0abe2-139">7</span></span>|<span data-ttu-id="0abe2-140">**Botón atrás**: se dirige al paso anterior en función de dónde se abrió el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0abe2-140">**Back button**: Goes to the previous step based on where the dialog opened.</span></span>|
|<span data-ttu-id="0abe2-141">8 </span><span class="sxs-lookup"><span data-stu-id="0abe2-141">8</span></span>|<span data-ttu-id="0abe2-142">**Botón Guardar**: completa la configuración de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="0abe2-142">**Save button**: Completes tab setup.</span></span>|

### <a name="tab-authentication-with-single-sign-on"></a><span data-ttu-id="0abe2-143">Autenticación de pestaña con inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="0abe2-143">Tab authentication with single sign-on</span></span>

<span data-ttu-id="0abe2-144">Puede Agregar un paso en el que los usuarios primero deban iniciar sesión con sus credenciales de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0abe2-144">You can add a step in which users must first sign in with their Microsoft credentials.</span></span> <span data-ttu-id="0abe2-145">Este método de autenticación se denomina inicio de sesión único (SSO).</span><span class="sxs-lookup"><span data-stu-id="0abe2-145">This authentication method is called single sign-on (SSO).</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="Ejemplo muestra una pantalla de autenticación de pestañas." border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a><span data-ttu-id="0abe2-147">Diseño de una configuración de pestaña con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="0abe2-147">Designing a tab setup with UI templates</span></span>

<span data-ttu-id="0abe2-148">Use una de las siguientes plantillas de interfaz de usuario de Microsoft Teams para ayudar a diseñar su experiencia de configuración de pestañas:</span><span class="sxs-lookup"><span data-stu-id="0abe2-148">Use one of the following Teams UI templates to help design your tab setup experience:</span></span>

* <span data-ttu-id="0abe2-149">[List](../../concepts/design/design-teams-app-ui-templates.md#list): lists puede mostrar elementos relacionados en un formato que se pueda analizar y permitir que los usuarios realicen acciones en una lista completa o en elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="0abe2-149">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="0abe2-150">[Formulario](../../concepts/design/design-teams-app-ui-templates.md#form): los formularios son para recopilar, validar y enviar entradas de usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="0abe2-150">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="0abe2-151">[Estado vacío](../../concepts/design/design-teams-app-ui-templates.md#empty-state): la plantilla de estado vacía se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error, etc.</span><span class="sxs-lookup"><span data-stu-id="0abe2-151">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="view-a-tab"></a><span data-ttu-id="0abe2-152">Ver una pestaña</span><span class="sxs-lookup"><span data-stu-id="0abe2-152">View a tab</span></span>

<span data-ttu-id="0abe2-153">Las pestañas proporcionan una experiencia web de pantalla completa en Teams donde puede mostrar contenido de colaboración (como paneles y paneles de tareas) e información importante.</span><span class="sxs-lookup"><span data-stu-id="0abe2-153">Tabs provide a full-screen web experience in Teams where you can display collaborative content—such task boards and dashboards—and important information.</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="Ejemplo muestra una pestaña con un panel de tareas." border="false":::

### <a name="anatomy-tab"></a><span data-ttu-id="0abe2-155">Anatomía: pestaña</span><span class="sxs-lookup"><span data-stu-id="0abe2-155">Anatomy: Tab</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una pestaña." border="false":::

|<span data-ttu-id="0abe2-157">Counter</span><span class="sxs-lookup"><span data-stu-id="0abe2-157">Counter</span></span>|<span data-ttu-id="0abe2-158">Descripción</span><span class="sxs-lookup"><span data-stu-id="0abe2-158">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="0abe2-159">1</span><span class="sxs-lookup"><span data-stu-id="0abe2-159">1</span></span>|<span data-ttu-id="0abe2-160">**Nombre de ficha**: etiqueta de navegación de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="0abe2-160">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="0abe2-161">2 </span><span class="sxs-lookup"><span data-stu-id="0abe2-161">2</span></span>|<span data-ttu-id="0abe2-162">**Desbordamiento de tabulación**: abre acciones de pestaña, como cambiar nombre y quitar.</span><span class="sxs-lookup"><span data-stu-id="0abe2-162">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="0abe2-163">3 </span><span class="sxs-lookup"><span data-stu-id="0abe2-163">3</span></span>|<span data-ttu-id="0abe2-164">**Chat de pestañas**: abre un hilo de chat a la derecha, lo que permite a los usuarios tener una conversación junto al contenido.</span><span class="sxs-lookup"><span data-stu-id="0abe2-164">**Tab chat**: Opens a chat thread on the right, allowing users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="0abe2-165">4 </span><span class="sxs-lookup"><span data-stu-id="0abe2-165">4</span></span>|<span data-ttu-id="0abe2-166">**iframe**: muestra el contenido de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="0abe2-166">**iframe**: Displays your tab’s content.</span></span>

### <a name="designing-a-tab-with-ui-templates"></a><span data-ttu-id="0abe2-167">Diseño de una pestaña con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="0abe2-167">Designing a tab with UI templates</span></span>

<span data-ttu-id="0abe2-168">Use una de las siguientes plantillas de interfaz de usuario de Microsoft Teams para ayudar a diseñar su experiencia de pestañas:</span><span class="sxs-lookup"><span data-stu-id="0abe2-168">Use one of the following Teams UI templates to help design your tab experience:</span></span>

* <span data-ttu-id="0abe2-169">[List](../../concepts/design/design-teams-app-ui-templates.md#list): lists puede mostrar elementos relacionados en un formato que se pueda analizar y permitir que los usuarios realicen acciones en una lista completa o en elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="0abe2-169">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="0abe2-170">[Panel de tareas](../../concepts/design/design-teams-app-ui-templates.md#task-board): un panel de tareas, a veces denominado tablero Kanban o carriles de nadar, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o vales.</span><span class="sxs-lookup"><span data-stu-id="0abe2-170">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="0abe2-171">[Panel](../../concepts/design/design-teams-app-ui-templates.md#dashboard): un panel es un lienzo que contiene varias tarjetas que proporcionan información general sobre datos o contenido.</span><span class="sxs-lookup"><span data-stu-id="0abe2-171">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="0abe2-172">[Formulario](../../concepts/design/design-teams-app-ui-templates.md#form): los formularios son para recopilar, validar y enviar entradas de usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="0abe2-172">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="0abe2-173">[Estado vacío](../../concepts/design/design-teams-app-ui-templates.md#empty-state): la plantilla de estado vacía se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error, etc.</span><span class="sxs-lookup"><span data-stu-id="0abe2-173">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="0abe2-174">Panel de [navegación izquierdo](../../concepts/design/design-teams-app-ui-templates.md#left-nav): la plantilla de navegación izquierda puede servir de ayuda si la pestaña requiere la navegación.</span><span class="sxs-lookup"><span data-stu-id="0abe2-174">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="0abe2-175">En general, debe mantener al mínimo la navegación por tabulaciones.</span><span class="sxs-lookup"><span data-stu-id="0abe2-175">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-tab-to-collaborate"></a><span data-ttu-id="0abe2-176">Usar una pestaña para colaborar</span><span class="sxs-lookup"><span data-stu-id="0abe2-176">Use a tab to collaborate</span></span>

<span data-ttu-id="0abe2-177">Las pestañas ayudan a facilitar las conversaciones sobre el contenido en una ubicación central.</span><span class="sxs-lookup"><span data-stu-id="0abe2-177">Tabs help facilitate conversations about content in a central location.</span></span>

### <a name="thread-discussion"></a><span data-ttu-id="0abe2-178">Discusión de subprocesos</span><span class="sxs-lookup"><span data-stu-id="0abe2-178">Thread discussion</span></span>

<span data-ttu-id="0abe2-179">Los usuarios pueden publicar automáticamente en un canal o un chat una vez que haya agregado una nueva pestaña. Esto no solo notifica a los miembros del equipo el contenido nuevo y proporciona un vínculo a la pestaña, permite a los usuarios empezar a hablar sobre la ficha.</span><span class="sxs-lookup"><span data-stu-id="0abe2-179">Users can automatically post to a channel or chat once they’ve added a new tab. This not only notifies team members of the new content and provides a link to tab, it allows people to start talking about the tab.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="Ejemplo muestra una pestaña que se está discutiendo en un subproceso de canal." border="false":::

### <a name="side-by-side-discussion"></a><span data-ttu-id="0abe2-181">Discusión en paralelo</span><span class="sxs-lookup"><span data-stu-id="0abe2-181">Side-by-side discussion</span></span>

<span data-ttu-id="0abe2-182">Los usuarios pueden tener una conversación junto al ver el contenido de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="0abe2-182">Users can have a conversation next while viewing the tab’s content.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="Ejemplo muestra una pestaña con un chat abierto en el lado derecho." border="false":::

### <a name="permissions-and-role-based-views"></a><span data-ttu-id="0abe2-184">Permisos y vistas basadas en roles</span><span class="sxs-lookup"><span data-stu-id="0abe2-184">Permissions and role-based views</span></span>

<span data-ttu-id="0abe2-185">La experiencia de la pestaña puede ser diferente para los usuarios en función de sus permisos.</span><span class="sxs-lookup"><span data-stu-id="0abe2-185">The tab experience may be different for users depending on their permissions.</span></span> <span data-ttu-id="0abe2-186">Por ejemplo, un usuario puede tener acceso a la pestaña sin tener que iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="0abe2-186">For example, one user can access the tab without having to sign in.</span></span> <span data-ttu-id="0abe2-187">Sin embargo, otro usuario debe firmar y verá contenido ligeramente distinto.</span><span class="sxs-lookup"><span data-stu-id="0abe2-187">Another user, however, must sign and will see slightly different content.</span></span>

## <a name="manage-a-tab"></a><span data-ttu-id="0abe2-188">Administrar una pestaña</span><span class="sxs-lookup"><span data-stu-id="0abe2-188">Manage a tab</span></span>

<span data-ttu-id="0abe2-189">Puede incluir opciones para cambiar el nombre de una pestaña, quitarla o modificarla.</span><span class="sxs-lookup"><span data-stu-id="0abe2-189">You can include options to rename, remove, or modify a tab.</span></span>

### <a name="anatomy-tab-menu"></a><span data-ttu-id="0abe2-190">Anatomía: menú de pestañas</span><span class="sxs-lookup"><span data-stu-id="0abe2-190">Anatomy: Tab menu</span></span>

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un menú de pestañas." border="false":::

|<span data-ttu-id="0abe2-192">Counter</span><span class="sxs-lookup"><span data-stu-id="0abe2-192">Counter</span></span>|<span data-ttu-id="0abe2-193">Descripción</span><span class="sxs-lookup"><span data-stu-id="0abe2-193">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="0abe2-194">1</span><span class="sxs-lookup"><span data-stu-id="0abe2-194">1</span></span>|<span data-ttu-id="0abe2-195">**Settings**: (opcional) permite a los usuarios modificar la configuración de una pestaña una vez que se ha agregado.</span><span class="sxs-lookup"><span data-stu-id="0abe2-195">**Settings**: (Optional) Allows users to modify a tab’s settings after it’s been added.</span></span>|
|<span data-ttu-id="0abe2-196">2 </span><span class="sxs-lookup"><span data-stu-id="0abe2-196">2</span></span>|<span data-ttu-id="0abe2-197">**Rename**: permite a los usuarios asignar a la ficha un nombre que sea más significativo para el equipo.</span><span class="sxs-lookup"><span data-stu-id="0abe2-197">**Rename**: Allows users to give the tab a name that’s more meaningful to the team.</span></span>|
|<span data-ttu-id="0abe2-198">3 </span><span class="sxs-lookup"><span data-stu-id="0abe2-198">3</span></span>|<span data-ttu-id="0abe2-199">**Quitar**: quita la pestaña del canal, el chat o la reunión.</span><span class="sxs-lookup"><span data-stu-id="0abe2-199">**Remove**: Removes the tab from the channel, chat, or meeting.</span></span>|

## <a name="tab-notifications-and-deep-linking"></a><span data-ttu-id="0abe2-200">Notificaciones de tabulación y vínculos profundos</span><span class="sxs-lookup"><span data-stu-id="0abe2-200">Tab notifications and deep linking</span></span>

<span data-ttu-id="0abe2-201">Puede enviar un mensaje con un vínculo profundo a su ficha. Por ejemplo, una tarjeta muestra un resumen de los datos de los errores que un usuario puede seleccionar para ver el error completo en una ficha. El envío de mensajes sobre la actividad de la pestaña aumenta el conocimiento sin notificar explícitamente a todos los usuarios (es decir, actividades sin ruido).</span><span class="sxs-lookup"><span data-stu-id="0abe2-201">You can send a message with a deep link to your tab. For example, a card shows a summary of bug data a user can select to see the entire bug in a tab. Sending messages about tab activity increases awareness without explicitly notifying everyone (i.e., activity without noise).</span></span> <span data-ttu-id="0abe2-202">También puede @mention usuarios específicos si es necesario.</span><span class="sxs-lookup"><span data-stu-id="0abe2-202">You also can @mention specific users if needed.</span></span>

<span data-ttu-id="0abe2-203">Notifique a los usuarios la actividad de tabulación de una de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="0abe2-203">Notify users of tab activity one of the following ways:</span></span>

* <span data-ttu-id="0abe2-204">**Bot**: este método es preferible especialmente si el subproceso de la pestaña es de destino.</span><span class="sxs-lookup"><span data-stu-id="0abe2-204">**Bot**: This method is preferred especially if the tab thread is targeted.</span></span> <span data-ttu-id="0abe2-205">La conversación encadenada de la pestaña se mueve a la vista como activa recientemente.</span><span class="sxs-lookup"><span data-stu-id="0abe2-205">The tab’s threaded conversation is moved into view as recently active.</span></span> <span data-ttu-id="0abe2-206">Este método también permite una sofisticación en el modo en que se envía la notificación.</span><span class="sxs-lookup"><span data-stu-id="0abe2-206">This method also allows for some sophistication in how the notification is sent.</span></span>
* <span data-ttu-id="0abe2-207">**Mensaje**: un mensaje se muestra en la fuente de actividades del usuario con un [vínculo profundo a la ficha](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="0abe2-207">**Message**: A message shows up in the user’s activity feed with a [deep link to the tab](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span></span>

## <a name="best-practices"></a><span data-ttu-id="0abe2-208">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="0abe2-208">Best practices</span></span>

### <a name="collaboration"></a><span data-ttu-id="0abe2-209">Colaboración</span><span class="sxs-lookup"><span data-stu-id="0abe2-209">Collaboration</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="Ilustración que muestra qué se debe hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="do-facilitate-conversation"></a><span data-ttu-id="0abe2-211">Hacer: facilitar la conversación</span><span class="sxs-lookup"><span data-stu-id="0abe2-211">Do: Facilitate conversation</span></span>

<span data-ttu-id="0abe2-212">Incluir contenido y componentes sobre los que pueden hablar los usuarios.</span><span class="sxs-lookup"><span data-stu-id="0abe2-212">Include content and components people can talk about.</span></span> <span data-ttu-id="0abe2-213">Si no encaja en el contexto de un chat, canal o reunión, no pertenece a la pestaña.</span><span class="sxs-lookup"><span data-stu-id="0abe2-213">If it doesn’t fit within the context of a chat, channel, or meeting, it doesn’t belong in your tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="Ilustración que muestra lo que no se hace con el diseño de navegación de pestañas." border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a><span data-ttu-id="0abe2-215">No: tratar la pestaña como cualquier otra página web</span><span class="sxs-lookup"><span data-stu-id="0abe2-215">Don't: Treat your tab like any other webpage</span></span>

<span data-ttu-id="0abe2-216">Una pestaña no es una página web que alguien pueda ver una vez.</span><span class="sxs-lookup"><span data-stu-id="0abe2-216">A tab isn’t a webpage someone might view once.</span></span> <span data-ttu-id="0abe2-217">Una pestaña debe mostrar su contenido más importante y relevante que los usuarios necesitan para realizar algo juntos.</span><span class="sxs-lookup"><span data-stu-id="0abe2-217">A tab should display your most important, relevant content that people need to accomplish something together.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="0abe2-218">Navegación</span><span class="sxs-lookup"><span data-stu-id="0abe2-218">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="Ilustración que muestra qué se debe hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="do-limit-tasks-and-data"></a><span data-ttu-id="0abe2-220">Do: limitar tareas y datos</span><span class="sxs-lookup"><span data-stu-id="0abe2-220">Do: Limit tasks and data</span></span>

<span data-ttu-id="0abe2-221">Las pestañas funcionan mejor cuando se redireccionan a necesidades específicas.</span><span class="sxs-lookup"><span data-stu-id="0abe2-221">Tabs work best when they address specific needs.</span></span> <span data-ttu-id="0abe2-222">Incluya un conjunto limitado de tareas y datos relevantes para el equipo o grupo.</span><span class="sxs-lookup"><span data-stu-id="0abe2-222">Include a limited set of tasks and data relevant to the team or group.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="Ilustración que muestra lo que no se hace con el diseño de navegación de pestañas." border="false":::

#### <a name="dont-embed-your-entire-app"></a><span data-ttu-id="0abe2-224">No: incruste la aplicación completa</span><span class="sxs-lookup"><span data-stu-id="0abe2-224">Don't: Embed your entire app</span></span>

<span data-ttu-id="0abe2-225">Usar una pestaña para mostrar una aplicación completa con navegación de varios niveles y interacciones complejas conduce a la sobrecarga de información.</span><span class="sxs-lookup"><span data-stu-id="0abe2-225">Using a tab to display an entire app with multi-level navigation and complex interactions leads to information overload.</span></span>

   :::column-end:::
:::row-end:::

### <a name="setup"></a><span data-ttu-id="0abe2-226">Instalación</span><span class="sxs-lookup"><span data-stu-id="0abe2-226">Setup</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="Ilustración que muestra qué se debe hacer con el diseño de la configuración de pestañas." border="false":::

#### <a name="do-keep-it-simple"></a><span data-ttu-id="0abe2-228">Do: simple</span><span class="sxs-lookup"><span data-stu-id="0abe2-228">Do: Keep it simple</span></span>

<span data-ttu-id="0abe2-229">Si la aplicación requiere autenticación, intente integrar el inicio de sesión único (SSO) de Microsoft para obtener una experiencia de inicio de sesión más fluida.</span><span class="sxs-lookup"><span data-stu-id="0abe2-229">If your app requires authentication, try integrating Microsoft single sign-on (SSO) for a more seamless sign-in experience.</span></span> <span data-ttu-id="0abe2-230">Además, solo incluya información esencial y pasos para agregar la pestaña.</span><span class="sxs-lookup"><span data-stu-id="0abe2-230">Also, only include essential information and steps to add the tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="Ilustración que muestra lo que no se hace con el diseño de la configuración de pestañas." border="false":::

#### <a name="dont-have-too-many-steps"></a><span data-ttu-id="0abe2-232">No: tener demasiados pasos</span><span class="sxs-lookup"><span data-stu-id="0abe2-232">Don't: Have too many steps</span></span>

<span data-ttu-id="0abe2-233">Quite los pasos innecesarios para agregar una tabulación.</span><span class="sxs-lookup"><span data-stu-id="0abe2-233">Remove any unnecessary steps for adding a tab.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="0abe2-234">Creación de temas</span><span class="sxs-lookup"><span data-stu-id="0abe2-234">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="Ilustración que muestra qué se debe hacer con los temas de la ficha." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="0abe2-236">Do: aprovechar las ventajas de los tokens de color de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0abe2-236">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="0abe2-237">Cada tema de Teams tiene su propia combinación de colores.</span><span class="sxs-lookup"><span data-stu-id="0abe2-237">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="0abe2-238">Para controlar automáticamente los cambios de tema, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">tokens de color (interfaz de usuario de Fluent)</a> en el diseño.</span><span class="sxs-lookup"><span data-stu-id="0abe2-238">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="Ilustración que muestra lo que no se hace con el tabulador." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="0abe2-240">No: valores de color de código duro</span><span class="sxs-lookup"><span data-stu-id="0abe2-240">Don't: Hard code color values</span></span>

<span data-ttu-id="0abe2-241">Si no usa los tokens de color de Teams, los diseños serán menos escalables y tendrán más tiempo para administrarlos.</span><span class="sxs-lookup"><span data-stu-id="0abe2-241">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a><span data-ttu-id="0abe2-242">Validar el diseño</span><span class="sxs-lookup"><span data-stu-id="0abe2-242">Validate your design</span></span>

<span data-ttu-id="0abe2-243">Si planea publicar la aplicación en AppSource, debe comprender los problemas de diseño que suelen hacer que las aplicaciones fallen durante el envío.</span><span class="sxs-lookup"><span data-stu-id="0abe2-243">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0abe2-244">Comprobar las instrucciones de validación del diseño</span><span class="sxs-lookup"><span data-stu-id="0abe2-244">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)

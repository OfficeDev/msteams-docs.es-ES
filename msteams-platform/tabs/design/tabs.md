---
title: Pestañas de diseño para escritorio, web y móvil
description: Aprende a diseñar una pestaña Teams para escritorio, web y móvil, y obtén el kit Microsoft Teams interfaz de usuario.
author: heath-hamilton
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: f1823a064cd182d0271aa97bef58ec724c7819b3
ms.sourcegitcommit: 33a43c61f27ae750776616b2cf90159455d8ba6c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2021
ms.locfileid: "52721846"
---
# <a name="design-your-tab-for-microsoft-teams"></a><span data-ttu-id="7fc0f-103">Diseñe la pestaña para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="7fc0f-103">Design your tab for Microsoft Teams</span></span>

<span data-ttu-id="7fc0f-104">Una pestaña es un lienzo grande para el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-104">A tab is a large canvas for your app content.</span></span> <span data-ttu-id="7fc0f-105">Para guiar el diseño de la aplicación, la siguiente información describe e ilustra cómo los usuarios pueden agregar, usar y administrar pestañas en Teams.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-105">To guide your app design, the following information describes and illustrates how people can add, use, and manage tabs in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="7fc0f-106">Kit de UI de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="7fc0f-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="7fc0f-107">Puedes encontrar instrucciones completas de diseño de pestañas, incluidos los elementos que puedes agarrar y modificar según sea necesario, en el kit de interfaz Microsoft Teams usuario.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-107">You can find comprehensive tab design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="7fc0f-108">El kit de interfaz de usuario también tiene temas esenciales, como la accesibilidad y el tamaño dinámico que no se tratan aquí.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-108">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7fc0f-109">Obtener el Kit de UI de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="7fc0f-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a><span data-ttu-id="7fc0f-110">Agregar una pestaña</span><span class="sxs-lookup"><span data-stu-id="7fc0f-110">Add a tab</span></span>

<span data-ttu-id="7fc0f-111">Puedes agregar una pestaña desde el almacén Teams (AppSource) o en uno de los siguientes contextos:</span><span class="sxs-lookup"><span data-stu-id="7fc0f-111">You can add a tab from the Teams store (AppSource) or in one of the following contexts:</span></span>

* <span data-ttu-id="7fc0f-112">Chat</span><span class="sxs-lookup"><span data-stu-id="7fc0f-112">Chat</span></span>
* <span data-ttu-id="7fc0f-113">Canal</span><span class="sxs-lookup"><span data-stu-id="7fc0f-113">Channel</span></span>
* <span data-ttu-id="7fc0f-114">Reunión (antes, durante o después de la reunión)</span><span class="sxs-lookup"><span data-stu-id="7fc0f-114">Meeting (before, during, or after the meeting)</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7fc0f-115">Escritorio</span><span class="sxs-lookup"><span data-stu-id="7fc0f-115">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="7fc0f-116">En el ejemplo siguiente se muestra cómo los usuarios pueden agregar una pestaña en un canal.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-116">The following example shows how users can add a tab in a channel.</span></span>

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="En el ejemplo se muestra una pestaña que se agrega en un canal." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7fc0f-118">Móvil</span><span class="sxs-lookup"><span data-stu-id="7fc0f-118">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="7fc0f-119">Los usuarios pueden acceder a  las pestañas seleccionando el botón Más en el canal (ejemplo a continuación) o chat en el que se han agregado.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-119">Users can access tabs by selecting the **More** button in the channel (example below) or chat in which they've been added.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-design-access-tab.png" alt-text="En el ejemplo se muestra una pestaña móvil que se agrega en un canal." border="false":::

---

## <a name="set-up-a-tab"></a><span data-ttu-id="7fc0f-121">Configurar una pestaña</span><span class="sxs-lookup"><span data-stu-id="7fc0f-121">Set up a tab</span></span>

<span data-ttu-id="7fc0f-122">Hay un breve proceso de configuración para agregar una aplicación como un canal, chat o pestaña de reunión. La experiencia está en gran medida a su medida.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-122">There's a short setup process to add an app as a channel, chat, or meeting tab. The experience is largely up to you.</span></span> <span data-ttu-id="7fc0f-123">Por ejemplo, podrías tener una descripción de cómo usar la aplicación y algunas opciones de configuración opcionales.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-123">For example, you could have a description of how to use the app and some optional settings.</span></span> <span data-ttu-id="7fc0f-124">Incluye un paso de inicio de sesión aquí si necesitas autenticar usuarios.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-124">Include a sign-in step here if you need to authenticate users.</span></span>

### <a name="tab-configuration-dialog"></a><span data-ttu-id="7fc0f-125">Cuadro de diálogo de configuración de tabulación</span><span class="sxs-lookup"><span data-stu-id="7fc0f-125">Tab configuration dialog</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="En el ejemplo se muestra un modal de configuración de tabulación." border="false":::

### <a name="anatomy-tab-configuration-dialog"></a><span data-ttu-id="7fc0f-127">Anatomía: cuadro de diálogo de configuración de tabulación</span><span class="sxs-lookup"><span data-stu-id="7fc0f-127">Anatomy: Tab configuration dialog</span></span>

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un modal de configuración de tabulación." border="false":::

|<span data-ttu-id="7fc0f-129">Contador</span><span class="sxs-lookup"><span data-stu-id="7fc0f-129">Counter</span></span>|<span data-ttu-id="7fc0f-130">Descripción</span><span class="sxs-lookup"><span data-stu-id="7fc0f-130">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="7fc0f-131">1</span><span class="sxs-lookup"><span data-stu-id="7fc0f-131">1</span></span>|<span data-ttu-id="7fc0f-132">**Logotipo de la** aplicación: logotipo de aplicación a todo color de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-132">**App logo**: Full color app logo of your app.</span></span>|
|<span data-ttu-id="7fc0f-133">2</span><span class="sxs-lookup"><span data-stu-id="7fc0f-133">2</span></span>|<span data-ttu-id="7fc0f-134">**Nombre de la** aplicación: nombre completo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-134">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="7fc0f-135">3</span><span class="sxs-lookup"><span data-stu-id="7fc0f-135">3</span></span>|<span data-ttu-id="7fc0f-136">**iframe:** espacio dinámico para el contenido de la aplicación (por ejemplo, configuración de pestañas o autenticación).</span><span class="sxs-lookup"><span data-stu-id="7fc0f-136">**iframe**: Responsive space for your app’s content (for example, tab settings or authentication).</span></span>|
|<span data-ttu-id="7fc0f-137">4 </span><span class="sxs-lookup"><span data-stu-id="7fc0f-137">4</span></span>|<span data-ttu-id="7fc0f-138">**Acerca del vínculo:** abre un cuadro de diálogo que muestra más información sobre la aplicación, como una descripción completa, los permisos requeridos por la aplicación y los vínculos a la directiva de privacidad y los términos de servicio.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-138">**About link**: Opens a dialog showing more information about the app, such as a full description, permissions required by the app, and links to your privacy policy and terms of service.</span></span>|
|<span data-ttu-id="7fc0f-139">5 </span><span class="sxs-lookup"><span data-stu-id="7fc0f-139">5</span></span>|<span data-ttu-id="7fc0f-140">**Botón Cerrar:** cierra el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-140">**Close button**: Closes the dialog.</span></span>|
|<span data-ttu-id="7fc0f-141">6 </span><span class="sxs-lookup"><span data-stu-id="7fc0f-141">6</span></span>|<span data-ttu-id="7fc0f-142">**Opción Notificar a los miembros del** equipo: el cuadro de diálogo pregunta a los usuarios si quieren crear una publicación para que otros sepan que agregaron una pestaña.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-142">**Notify team members option**: The dialog asks users if they want to create a post letting others know they added a tab.</span></span>|
|<span data-ttu-id="7fc0f-143">7 </span><span class="sxs-lookup"><span data-stu-id="7fc0f-143">7</span></span>|<span data-ttu-id="7fc0f-144">**Botón Atrás:** va al paso anterior en función de dónde se abrió el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-144">**Back button**: Goes to the previous step based on where the dialog opened.</span></span>|
|<span data-ttu-id="7fc0f-145">8 </span><span class="sxs-lookup"><span data-stu-id="7fc0f-145">8</span></span>|<span data-ttu-id="7fc0f-146">**Botón Guardar:** completa la configuración de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-146">**Save button**: Completes tab setup.</span></span>|

### <a name="tab-authentication-with-single-sign-on"></a><span data-ttu-id="7fc0f-147">Autenticación de tabulación con inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="7fc0f-147">Tab authentication with single sign-on</span></span>

<span data-ttu-id="7fc0f-148">Puede agregar un paso en el que los usuarios primero deben iniciar sesión con sus credenciales de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-148">You can add a step in which users must first sign in with their Microsoft credentials.</span></span> <span data-ttu-id="7fc0f-149">Este método de autenticación se denomina inicio de sesión único (SSO).</span><span class="sxs-lookup"><span data-stu-id="7fc0f-149">This authentication method is called single sign-on (SSO).</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="En el ejemplo se muestra una pantalla de autenticación de tabulación." border="false":::

### <a name="design-a-tab-setup-with-ui-templates"></a><span data-ttu-id="7fc0f-151">Diseñar una configuración de pestaña con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="7fc0f-151">Design a tab setup with UI templates</span></span>

<span data-ttu-id="7fc0f-152">Usa una de las siguientes plantillas Teams interfaz de usuario para ayudar a diseñar la experiencia de configuración de pestañas:</span><span class="sxs-lookup"><span data-stu-id="7fc0f-152">Use one of the following Teams UI templates to help design your tab setup experience:</span></span>

* <span data-ttu-id="7fc0f-153">[Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato digitalizado y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-153">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="7fc0f-154">[Formulario:](../../concepts/design/design-teams-app-ui-templates.md#form)los formularios son para recopilar, validar y enviar la entrada del usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-154">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="7fc0f-155">[Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacío se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-155">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="view-a-tab"></a><span data-ttu-id="7fc0f-156">Ver una pestaña</span><span class="sxs-lookup"><span data-stu-id="7fc0f-156">View a tab</span></span>

<span data-ttu-id="7fc0f-157">Las pestañas proporcionan una experiencia web a pantalla completa en Teams donde puede mostrar contenido de colaboración (como paneles de tareas y paneles) e información importante.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-157">Tabs provide a full-screen web experience in Teams where you can display collaborative content—such task boards and dashboards—and important information.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7fc0f-158">Escritorio</span><span class="sxs-lookup"><span data-stu-id="7fc0f-158">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="En el ejemplo se muestra una pestaña con un panel de tareas." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7fc0f-160">Móvil</span><span class="sxs-lookup"><span data-stu-id="7fc0f-160">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-view-tab.png" alt-text="En el ejemplo se muestra una pestaña móvil con un panel de tareas." border="false":::

---

### <a name="anatomy-tab"></a><span data-ttu-id="7fc0f-162">Anatomía: Ficha</span><span class="sxs-lookup"><span data-stu-id="7fc0f-162">Anatomy: Tab</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7fc0f-163">Escritorio</span><span class="sxs-lookup"><span data-stu-id="7fc0f-163">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una pestaña." border="false":::

|<span data-ttu-id="7fc0f-165">Contador</span><span class="sxs-lookup"><span data-stu-id="7fc0f-165">Counter</span></span>|<span data-ttu-id="7fc0f-166">Descripción</span><span class="sxs-lookup"><span data-stu-id="7fc0f-166">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="7fc0f-167">1</span><span class="sxs-lookup"><span data-stu-id="7fc0f-167">1</span></span>|<span data-ttu-id="7fc0f-168">**Nombre de la pestaña:** etiqueta de navegación para la pestaña.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-168">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="7fc0f-169">2</span><span class="sxs-lookup"><span data-stu-id="7fc0f-169">2</span></span>|<span data-ttu-id="7fc0f-170">**Desbordamiento de** tabulación: abre acciones de tabulación, como cambiar el nombre y quitar.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-170">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="7fc0f-171">3</span><span class="sxs-lookup"><span data-stu-id="7fc0f-171">3</span></span>|<span data-ttu-id="7fc0f-172">**Chat de pestañas:** abre un chat a la derecha, lo que permite a los usuarios tener una conversación junto al contenido.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-172">**Tab chat**: Opens a chat to the right, allowing users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="7fc0f-173">4 </span><span class="sxs-lookup"><span data-stu-id="7fc0f-173">4</span></span>|<span data-ttu-id="7fc0f-174">**iframe:** muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-174">**iframe**: Displays your app content.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="7fc0f-175">Móvil</span><span class="sxs-lookup"><span data-stu-id="7fc0f-175">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-view-tab-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una pestaña." border="false":::

|<span data-ttu-id="7fc0f-177">Contador</span><span class="sxs-lookup"><span data-stu-id="7fc0f-177">Counter</span></span>|<span data-ttu-id="7fc0f-178">Descripción</span><span class="sxs-lookup"><span data-stu-id="7fc0f-178">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="7fc0f-179">1</span><span class="sxs-lookup"><span data-stu-id="7fc0f-179">1</span></span>|<span data-ttu-id="7fc0f-180">**Nombre de la pestaña:** etiqueta de navegación para la pestaña.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-180">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="7fc0f-181">2</span><span class="sxs-lookup"><span data-stu-id="7fc0f-181">2</span></span>|<span data-ttu-id="7fc0f-182">**Chat de pestaña:** abre un chat que permite a los usuarios tener una conversación junto al contenido.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-182">**Tab chat**: Opens a chat that allows users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="7fc0f-183">3</span><span class="sxs-lookup"><span data-stu-id="7fc0f-183">3</span></span>|<span data-ttu-id="7fc0f-184">**webview:** muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-184">**webview**: Displays your app content.</span></span>|

---

### <a name="designing-a-tab-with-ui-templates-and-advanced-components"></a><span data-ttu-id="7fc0f-185">Diseño de una pestaña con plantillas de interfaz de usuario y componentes avanzados</span><span class="sxs-lookup"><span data-stu-id="7fc0f-185">Designing a tab with UI templates and advanced components</span></span>

<span data-ttu-id="7fc0f-186">Use una de las siguientes plantillas Teams y componentes para ayudar a diseñar la experiencia de pestaña:</span><span class="sxs-lookup"><span data-stu-id="7fc0f-186">Use one of the following Teams templates and components to help design your tab experience:</span></span>

* <span data-ttu-id="7fc0f-187">[Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato digitalizado y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-187">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="7fc0f-188">[Panel de](../../concepts/design/design-teams-app-ui-templates.md#task-board)tareas: un panel de tareas, a veces denominado tablero de kanban o carriles de natación, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o los vales.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-188">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="7fc0f-189">[Panel:](../../concepts/design/design-teams-app-ui-templates.md#dashboard)un panel es un lienzo que contiene varias tarjetas que proporcionan información general sobre los datos o el contenido.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-189">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="7fc0f-190">[Formulario:](../../concepts/design/design-teams-app-ui-templates.md#form)los formularios son para recopilar, validar y enviar la entrada del usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-190">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="7fc0f-191">[Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacío se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-191">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="7fc0f-192">[Navegación izquierda:](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav)el componente de navegación izquierdo puede ayudar si la pestaña requiere algo de navegación.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-192">[Left nav](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav): The left nav component can help if your tab requires some navigation.</span></span> <span data-ttu-id="7fc0f-193">En general, debe mantener la navegación por pestañas al mínimo.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-193">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-tab-to-collaborate"></a><span data-ttu-id="7fc0f-194">Usar una pestaña para colaborar</span><span class="sxs-lookup"><span data-stu-id="7fc0f-194">Use a tab to collaborate</span></span>

<span data-ttu-id="7fc0f-195">Las pestañas ayudan a facilitar las conversaciones sobre el contenido en una ubicación central.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-195">Tabs help facilitate conversations about content in a central location.</span></span>

### <a name="thread-discussion"></a><span data-ttu-id="7fc0f-196">Discusión de subprocesos</span><span class="sxs-lookup"><span data-stu-id="7fc0f-196">Thread discussion</span></span>

<span data-ttu-id="7fc0f-197">Los usuarios pueden publicar automáticamente en un canal o chat una vez que han agregado una nueva pestaña. Esto no solo notifica a los miembros del equipo del nuevo contenido y proporciona un vínculo a la pestaña, sino que permite a los usuarios empezar a hablar sobre la pestaña.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-197">Users can automatically post to a channel or chat once they’ve added a new tab. This not only notifies team members of the new content and provides a link to tab, it allows people to start talking about the tab.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7fc0f-198">Escritorio</span><span class="sxs-lookup"><span data-stu-id="7fc0f-198">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="En el ejemplo se muestra una pestaña que se está analizando en un subproceso de canal." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7fc0f-200">Móvil</span><span class="sxs-lookup"><span data-stu-id="7fc0f-200">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-use-tab-channel.png" alt-text="En el ejemplo se muestra una pestaña móvil que se está analizando en un subproceso de canal." border="false":::

---

### <a name="tab-chat"></a><span data-ttu-id="7fc0f-202">Chat de pestañas</span><span class="sxs-lookup"><span data-stu-id="7fc0f-202">Tab chat</span></span>

<span data-ttu-id="7fc0f-203">Los usuarios pueden tener una conversación junto al contenido de la pestaña que están viendo.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-203">Users can have a conversation next to the tab content they're viewing.</span></span> <span data-ttu-id="7fc0f-204">En el escritorio, el chat se abre al lado del contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-204">On desktop, the chat opens to the side of the app content.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7fc0f-205">Escritorio</span><span class="sxs-lookup"><span data-stu-id="7fc0f-205">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="En el ejemplo se muestra una pestaña con un chat abierto en el lado derecho." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7fc0f-207">Móvil</span><span class="sxs-lookup"><span data-stu-id="7fc0f-207">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-use-tab-side-chat.png" alt-text="En el ejemplo se muestra una pestaña móvil con un área de chat en contexto." border="false":::

---

### <a name="permissions-and-role-based-views"></a><span data-ttu-id="7fc0f-209">Permisos y vistas basadas en roles</span><span class="sxs-lookup"><span data-stu-id="7fc0f-209">Permissions and role-based views</span></span>

<span data-ttu-id="7fc0f-210">La experiencia de pestaña puede ser diferente para los usuarios en función de sus permisos.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-210">The tab experience may be different for users depending on their permissions.</span></span> <span data-ttu-id="7fc0f-211">Por ejemplo, un usuario puede tener acceso a la pestaña sin tener que iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-211">For example, one user can access the tab without having to sign in.</span></span> <span data-ttu-id="7fc0f-212">Sin embargo, otro usuario debe iniciar sesión y ver contenido ligeramente diferente.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-212">Another user, however, must sign in and see slightly different content.</span></span>

## <a name="manage-a-tab"></a><span data-ttu-id="7fc0f-213">Administrar una pestaña</span><span class="sxs-lookup"><span data-stu-id="7fc0f-213">Manage a tab</span></span>

<span data-ttu-id="7fc0f-214">Puede incluir opciones para cambiar el nombre, quitar o modificar una pestaña.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-214">You can include options to rename, remove, or modify a tab.</span></span>

### <a name="anatomy-tab-menu"></a><span data-ttu-id="7fc0f-215">Anatomía: menú De pestaña</span><span class="sxs-lookup"><span data-stu-id="7fc0f-215">Anatomy: Tab menu</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7fc0f-216">Escritorio</span><span class="sxs-lookup"><span data-stu-id="7fc0f-216">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un menú de pestaña." border="false":::

|<span data-ttu-id="7fc0f-218">Contador</span><span class="sxs-lookup"><span data-stu-id="7fc0f-218">Counter</span></span>|<span data-ttu-id="7fc0f-219">Descripción</span><span class="sxs-lookup"><span data-stu-id="7fc0f-219">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="7fc0f-220">1</span><span class="sxs-lookup"><span data-stu-id="7fc0f-220">1</span></span>|<span data-ttu-id="7fc0f-221">**Configuración**: (opcional) Permite a los usuarios modificar la configuración de una pestaña después de agregarla.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-221">**Settings**: (Optional) Allows users to modify a tab’s settings after it’s been added.</span></span>|
|<span data-ttu-id="7fc0f-222">2</span><span class="sxs-lookup"><span data-stu-id="7fc0f-222">2</span></span>|<span data-ttu-id="7fc0f-223">**Cambiar** nombre: los usuarios pueden dar a la pestaña un nombre que sea significativo para el canal, chat o reunión.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-223">**Rename**: Users can give the tab a name that’s meaningful to the channel, chat, or meeting.</span></span>|
|<span data-ttu-id="7fc0f-224">3</span><span class="sxs-lookup"><span data-stu-id="7fc0f-224">3</span></span>|<span data-ttu-id="7fc0f-225">**Quitar:** quita la pestaña del canal, chat o reunión.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-225">**Remove**: Removes the tab from the channel, chat, or meeting.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="7fc0f-226">Móvil</span><span class="sxs-lookup"><span data-stu-id="7fc0f-226">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-manage-tab-menu-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un menú de pestaña móvil." border="false":::

|<span data-ttu-id="7fc0f-228">Contador</span><span class="sxs-lookup"><span data-stu-id="7fc0f-228">Counter</span></span>|<span data-ttu-id="7fc0f-229">Descripción</span><span class="sxs-lookup"><span data-stu-id="7fc0f-229">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="7fc0f-230">1</span><span class="sxs-lookup"><span data-stu-id="7fc0f-230">1</span></span>|<span data-ttu-id="7fc0f-231">**Abrir en el explorador:** abre la aplicación en el explorador predeterminado del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-231">**Open in browser**: Opens the app in the device’s default browser.</span></span>|
|<span data-ttu-id="7fc0f-232">2</span><span class="sxs-lookup"><span data-stu-id="7fc0f-232">2</span></span>|<span data-ttu-id="7fc0f-233">**Vínculo Copiar:** los usuarios pueden copiar y compartir un vínculo a la pestaña.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-233">**Copy link**: Users can copy and share a link to the tab.</span></span>|
|<span data-ttu-id="7fc0f-234">3</span><span class="sxs-lookup"><span data-stu-id="7fc0f-234">3</span></span>|<span data-ttu-id="7fc0f-235">**Configuración**: (opcional) Modificar la configuración de una pestaña después de agregarla.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-235">**Settings**: (Optional) Modify a tab’s settings after it's been added.</span></span>|
|<span data-ttu-id="7fc0f-236">4 </span><span class="sxs-lookup"><span data-stu-id="7fc0f-236">4</span></span>|<span data-ttu-id="7fc0f-237">**Cambiar** nombre: los usuarios pueden dar a la pestaña un nombre que sea significativo para el canal, chat o reunión.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-237">**Rename**: Users can give the tab a name that's meaningful to the channel, chat, or meeting.</span></span>|
|<span data-ttu-id="7fc0f-238">5 </span><span class="sxs-lookup"><span data-stu-id="7fc0f-238">5</span></span>|<span data-ttu-id="7fc0f-239">**Eliminar:** quita la pestaña del canal, chat o reunión.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-239">**Delete**: Removes the tab from the channel, chat, or meeting.</span></span>|

---

## <a name="tab-notifications-and-deep-linking"></a><span data-ttu-id="7fc0f-240">Notificaciones de tabulación y vinculación profunda</span><span class="sxs-lookup"><span data-stu-id="7fc0f-240">Tab notifications and deep linking</span></span>

<span data-ttu-id="7fc0f-241">Puede enviar un mensaje con un vínculo profundo a la pestaña. Por ejemplo, una tarjeta muestra un resumen de los datos de errores que un usuario puede seleccionar para ver el error completo en una pestaña. El envío de mensajes sobre la actividad de tabulación aumenta el conocimiento sin notificar explícitamente a todos (es decir, actividad sin ruido).</span><span class="sxs-lookup"><span data-stu-id="7fc0f-241">You can send a message with a deep link to your tab. For example, a card shows a summary of bug data a user can select to see the entire bug in a tab. Sending messages about tab activity increases awareness without explicitly notifying everyone (i.e., activity without noise).</span></span> <span data-ttu-id="7fc0f-242">También puede usar @mention usuarios específicos si es necesario.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-242">You also can @mention specific users if needed.</span></span>

<span data-ttu-id="7fc0f-243">Notificar a los usuarios sobre la actividad de tabulación de una de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="7fc0f-243">Notify users of tab activity one of the following ways:</span></span>

* <span data-ttu-id="7fc0f-244">**Bot:** este método se prefiere especialmente si el subproceso de tabulación está dirigido.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-244">**Bot**: This method is preferred especially if the tab thread is targeted.</span></span> <span data-ttu-id="7fc0f-245">La conversación enhebrada de la pestaña se mueve a la vista como activa recientemente.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-245">The tab’s threaded conversation is moved into view as recently active.</span></span> <span data-ttu-id="7fc0f-246">Este método también permite cierta sofisticación en la forma en que se envía la notificación.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-246">This method also allows for some sophistication in how the notification is sent.</span></span>
* <span data-ttu-id="7fc0f-247">**Mensaje:** aparece un mensaje en la fuente de actividad del usuario con un vínculo profundo a [la pestaña](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="7fc0f-247">**Message**: A message shows up in the user’s activity feed with a [deep link to the tab](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span></span>

## <a name="best-practices"></a><span data-ttu-id="7fc0f-248">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="7fc0f-248">Best practices</span></span>

<span data-ttu-id="7fc0f-249">Usa estas recomendaciones para crear una experiencia de aplicación de calidad:</span><span class="sxs-lookup"><span data-stu-id="7fc0f-249">Use these recommendations to create a quality app experience:</span></span>

### <a name="collaboration"></a><span data-ttu-id="7fc0f-250">Colaboración</span><span class="sxs-lookup"><span data-stu-id="7fc0f-250">Collaboration</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="La ilustración muestra qué hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="do-facilitate-conversation"></a><span data-ttu-id="7fc0f-252">Hacer: facilitar la conversación</span><span class="sxs-lookup"><span data-stu-id="7fc0f-252">Do: Facilitate conversation</span></span>

<span data-ttu-id="7fc0f-253">Incluir contenido y componentes de los que los usuarios puedan hablar.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-253">Include content and components people can talk about.</span></span> <span data-ttu-id="7fc0f-254">Si no cabe en el contexto de un chat, canal o reunión, no pertenece a la pestaña.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-254">If it doesn’t fit within the context of a chat, channel, or meeting, it doesn’t belong in your tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="En el ejemplo se muestra lo que no se debe hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a><span data-ttu-id="7fc0f-256">No: trate la pestaña como cualquier otra página web</span><span class="sxs-lookup"><span data-stu-id="7fc0f-256">Don't: Treat your tab like any other webpage</span></span>

<span data-ttu-id="7fc0f-257">Una pestaña no es una página web que alguien pueda ver una vez.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-257">A tab isn’t a webpage someone might view once.</span></span> <span data-ttu-id="7fc0f-258">Una pestaña debe mostrar el contenido más importante y relevante que los usuarios necesitan para lograr algo juntos.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-258">A tab should display your most important, relevant content that people need to accomplish something together.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="7fc0f-259">Navegación</span><span class="sxs-lookup"><span data-stu-id="7fc0f-259">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="Ejemplo que muestra qué hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="do-limit-tasks-and-data"></a><span data-ttu-id="7fc0f-261">Hacer: limitar tareas y datos</span><span class="sxs-lookup"><span data-stu-id="7fc0f-261">Do: Limit tasks and data</span></span>

<span data-ttu-id="7fc0f-262">Las pestañas funcionan mejor cuando se abordan necesidades específicas.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-262">Tabs work best when they address specific needs.</span></span> <span data-ttu-id="7fc0f-263">Incluya un conjunto limitado de tareas y datos relevantes para el equipo o grupo.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-263">Include a limited set of tasks and data relevant to the team or group.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="Ilustración que muestra qué no hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="dont-embed-your-entire-app"></a><span data-ttu-id="7fc0f-265">No: insertar toda la aplicación</span><span class="sxs-lookup"><span data-stu-id="7fc0f-265">Don't: Embed your entire app</span></span>

<span data-ttu-id="7fc0f-266">El uso de una pestaña para mostrar una aplicación completa con navegación de varios niveles e interacciones complejas conduce a una sobrecarga de información.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-266">Using a tab to display an entire app with multi-level navigation and complex interactions leads to information overload.</span></span>

   :::column-end:::
:::row-end:::

### <a name="setup"></a><span data-ttu-id="7fc0f-267">Instalación</span><span class="sxs-lookup"><span data-stu-id="7fc0f-267">Setup</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="Ilustración que muestra qué hacer con el diseño de configuración de pestañas." border="false":::

#### <a name="do-keep-it-simple"></a><span data-ttu-id="7fc0f-269">Do: Keep it simple</span><span class="sxs-lookup"><span data-stu-id="7fc0f-269">Do: Keep it simple</span></span>

<span data-ttu-id="7fc0f-270">Si la aplicación requiere autenticación, intenta integrar el inicio de sesión único (SSO) de Microsoft para una experiencia de inicio de sesión más fluida.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-270">If your app requires authentication, try integrating Microsoft single sign-on (SSO) for a more seamless sign-in experience.</span></span> <span data-ttu-id="7fc0f-271">Además, solo incluya información esencial y pasos para agregar la pestaña.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-271">Also, only include essential information and steps to add the tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="Ilustración que muestra qué no hacer con el diseño de configuración de pestañas." border="false":::

#### <a name="dont-have-too-many-steps"></a><span data-ttu-id="7fc0f-273">No: tener demasiados pasos</span><span class="sxs-lookup"><span data-stu-id="7fc0f-273">Don't: Have too many steps</span></span>

<span data-ttu-id="7fc0f-274">Quite los pasos innecesarios para agregar una pestaña.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-274">Remove any unnecessary steps for adding a tab.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="7fc0f-275">Creación de temas</span><span class="sxs-lookup"><span data-stu-id="7fc0f-275">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="Ilustración que muestra qué hacer con el tema de tabulación." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="7fc0f-277">Hacer: aprovechar las ventajas de Teams de color</span><span class="sxs-lookup"><span data-stu-id="7fc0f-277">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="7fc0f-278">Cada Teams tema tiene su propia combinación de colores.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-278">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="7fc0f-279">Para controlar los cambios de tema automáticamente, usa <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">tokens de color (Fluent UI)</a> en el diseño.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-279">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="Ilustración que muestra lo que no se debe hacer con el tema de tabulación." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="7fc0f-281">No: valores de color de código duro</span><span class="sxs-lookup"><span data-stu-id="7fc0f-281">Don't: Hard code color values</span></span>

<span data-ttu-id="7fc0f-282">Si no usas tokens Teams de color, tus diseños serán menos escalables y tendrán más tiempo para administrar.</span><span class="sxs-lookup"><span data-stu-id="7fc0f-282">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

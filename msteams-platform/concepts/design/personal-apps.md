---
title: Diseño de su aplicación personal
description: Aprende a diseñar una aplicación Teams personal y obtener el kit Microsoft Teams interfaz de usuario.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 83fad746d71dd196f6efa6526f5c6c28ceac9e20
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644896"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a><span data-ttu-id="a3a69-103">Diseñar tu aplicación personal para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a3a69-103">Designing your personal app for Microsoft Teams</span></span>

<span data-ttu-id="a3a69-104">Una aplicación personal puede ser un bot, un área de trabajo privada o ambos.</span><span class="sxs-lookup"><span data-stu-id="a3a69-104">A personal app can be a bot, private workspace, or both.</span></span> <span data-ttu-id="a3a69-105">A veces funciona como un lugar para crear o ver contenido, otras veces ofrece al usuario una vista visual de todo lo que es suyo cuando la aplicación se ha configurado como una pestaña en varios canales.</span><span class="sxs-lookup"><span data-stu-id="a3a69-105">Sometimes it functions like a place to create or view content, other times it offers the user a bird’s eye view of everything that's theirs when the app has been configured as a tab in multiple channels.</span></span>

<span data-ttu-id="a3a69-106">Para guiar el diseño de la aplicación, la siguiente información describe e ilustra cómo las personas pueden agregar, usar y administrar aplicaciones personales en Teams.</span><span class="sxs-lookup"><span data-stu-id="a3a69-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage personal apps in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="a3a69-107">Kit de UI de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a3a69-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="a3a69-108">Puedes encontrar instrucciones completas de diseño de aplicaciones personales, incluidos los elementos que puedes agarrar y modificar según sea necesario, en el kit de interfaz Microsoft Teams usuario.</span><span class="sxs-lookup"><span data-stu-id="a3a69-108">You can find comprehensive personal app design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="a3a69-109">El kit de interfaz de usuario también tiene temas esenciales, como la accesibilidad y el tamaño dinámico que no se tratan aquí.</span><span class="sxs-lookup"><span data-stu-id="a3a69-109">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a3a69-110">Obtener el Kit de UI de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="a3a69-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a><span data-ttu-id="a3a69-111">Agregar una aplicación personal</span><span class="sxs-lookup"><span data-stu-id="a3a69-111">Add a personal app</span></span>

<span data-ttu-id="a3a69-112">Puedes agregar una aplicación personal desde la tienda Teams (AppSource) o el  menú desplegable de la aplicación seleccionando el icono Más en el lado izquierdo de Teams (que se muestra en el ejemplo siguiente).</span><span class="sxs-lookup"><span data-stu-id="a3a69-112">You can add a personal app from the Teams store (AppSource) or the app flyout by selecting the **More** icon on the left side of Teams (shown in the following example).</span></span>

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="En el ejemplo se muestra cómo agregar una aplicación personal desde el menú desplegable de la aplicación." border="false":::

## <a name="use-a-personal-app-private-workspace"></a><span data-ttu-id="a3a69-114">Usar una aplicación personal (área de trabajo privada)</span><span class="sxs-lookup"><span data-stu-id="a3a69-114">Use a personal app (private workspace)</span></span>

<span data-ttu-id="a3a69-115">Con un área de trabajo privada, puedes ver contenido de la aplicación que sea significativo para ti en una ubicación central sin salir de Teams.</span><span class="sxs-lookup"><span data-stu-id="a3a69-115">With a private workspace, you can view app content that's meaningful to you in a central location without leaving Teams.</span></span>

<span data-ttu-id="a3a69-116">(Nota de implementación: el área de trabajo privada se basa en la funcionalidad [*de tabulación*](../../build-your-first-app/build-personal-tab.md) personal).</span><span class="sxs-lookup"><span data-stu-id="a3a69-116">(Implementation note: The private workspace is based on the [*personal tab*](../../build-your-first-app/build-personal-tab.md) capability.)</span></span>

### <a name="anatomy-personal-app-private-workspace"></a><span data-ttu-id="a3a69-117">Anatomía: aplicación personal (área de trabajo privada)</span><span class="sxs-lookup"><span data-stu-id="a3a69-117">Anatomy: Personal app (private workspace)</span></span>

# <a name="desktop"></a>[<span data-ttu-id="a3a69-118">Escritorio</span><span class="sxs-lookup"><span data-stu-id="a3a69-118">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="En el ejemplo se muestra la anatomía del componente de la pestaña personal." border="false":::

|<span data-ttu-id="a3a69-120">Contador</span><span class="sxs-lookup"><span data-stu-id="a3a69-120">Counter</span></span>|<span data-ttu-id="a3a69-121">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3a69-121">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a3a69-122">A</span><span class="sxs-lookup"><span data-stu-id="a3a69-122">A</span></span>|<span data-ttu-id="a3a69-123">**Atribución de la aplicación:** el logotipo y el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3a69-123">**App attribution**: Your app logo and name.</span></span>|
|<span data-ttu-id="a3a69-124">B</span><span class="sxs-lookup"><span data-stu-id="a3a69-124">B</span></span>|<span data-ttu-id="a3a69-125">**Pestañas:** proporciona navegación para tu aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="a3a69-125">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="a3a69-126">C</span><span class="sxs-lookup"><span data-stu-id="a3a69-126">C</span></span>|<span data-ttu-id="a3a69-127">**Vista emergente:** inserta el contenido de la aplicación desde una ventana primaria a una ventana secundaria independiente.</span><span class="sxs-lookup"><span data-stu-id="a3a69-127">**Popout view**: Pushes your app content from a parent window to a standalone child window.</span></span>|
|<span data-ttu-id="a3a69-128">D</span><span class="sxs-lookup"><span data-stu-id="a3a69-128">D</span></span>|<span data-ttu-id="a3a69-129">**Más menú:** incluye información y opciones de aplicación adicionales.</span><span class="sxs-lookup"><span data-stu-id="a3a69-129">**More menu**: Includes additional app options and information.</span></span> <span data-ttu-id="a3a69-130">(También puede crear una **Configuración** una pestaña).</span><span class="sxs-lookup"><span data-stu-id="a3a69-130">(You could alternatively make **Settings** a tab.)</span></span>|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de la pestaña personal." border="false":::

|<span data-ttu-id="a3a69-132">Contador</span><span class="sxs-lookup"><span data-stu-id="a3a69-132">Counter</span></span>|<span data-ttu-id="a3a69-133">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3a69-133">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a3a69-134">A</span><span class="sxs-lookup"><span data-stu-id="a3a69-134">A</span></span>|<span data-ttu-id="a3a69-135">**Pestañas:** proporciona navegación para tu aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="a3a69-135">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="a3a69-136">1</span><span class="sxs-lookup"><span data-stu-id="a3a69-136">1</span></span>|<span data-ttu-id="a3a69-137">**iframe:** muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3a69-137">**iframe**: Displays your app content.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="a3a69-138">Móvil</span><span class="sxs-lookup"><span data-stu-id="a3a69-138">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-component-anatomy.png" alt-text="En el ejemplo se muestra la anatomía del componente de la pestaña personal." border="false":::

|<span data-ttu-id="a3a69-140">Contador</span><span class="sxs-lookup"><span data-stu-id="a3a69-140">Counter</span></span>|<span data-ttu-id="a3a69-141">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3a69-141">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a3a69-142">A</span><span class="sxs-lookup"><span data-stu-id="a3a69-142">A</span></span>|<span data-ttu-id="a3a69-143">**Atribución de la aplicación:** el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3a69-143">**App attribution**: Your app name.</span></span>|
|<span data-ttu-id="a3a69-144">B</span><span class="sxs-lookup"><span data-stu-id="a3a69-144">B</span></span>|<span data-ttu-id="a3a69-145">**Pestañas:** proporciona navegación para tu aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="a3a69-145">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="a3a69-146">C</span><span class="sxs-lookup"><span data-stu-id="a3a69-146">C</span></span>|<span data-ttu-id="a3a69-147">**Más menú:** incluye información y opciones de aplicación adicionales.</span><span class="sxs-lookup"><span data-stu-id="a3a69-147">**More menu**: Includes additional app options and information.</span></span>|
|<span data-ttu-id="a3a69-148">D</span><span class="sxs-lookup"><span data-stu-id="a3a69-148">D</span></span>|<span data-ttu-id="a3a69-149">**Navegación principal:** proporciona navegación a la aplicación otras características Teams principales.</span><span class="sxs-lookup"><span data-stu-id="a3a69-149">**Primary navigation**: Provides navigation to your app other main Teams features.</span></span>|

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-structural-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de la pestaña personal." border="false":::

|<span data-ttu-id="a3a69-151">Contador</span><span class="sxs-lookup"><span data-stu-id="a3a69-151">Counter</span></span>|<span data-ttu-id="a3a69-152">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3a69-152">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a3a69-153">A</span><span class="sxs-lookup"><span data-stu-id="a3a69-153">A</span></span>|<span data-ttu-id="a3a69-154">**Pestañas:** proporciona navegación para tu aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="a3a69-154">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="a3a69-155">1</span><span class="sxs-lookup"><span data-stu-id="a3a69-155">1</span></span>|<span data-ttu-id="a3a69-156">**webview:** muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3a69-156">**webview**: Displays your app content.</span></span>|

---

### <a name="designing-with-ui-templates-and-advanced-components"></a><span data-ttu-id="a3a69-157">Diseño con plantillas de interfaz de usuario y componentes avanzados</span><span class="sxs-lookup"><span data-stu-id="a3a69-157">Designing with UI templates and advanced components</span></span>

<span data-ttu-id="a3a69-158">Use una de las siguientes plantillas Teams y componentes para ayudar a diseñar la pestaña personal:</span><span class="sxs-lookup"><span data-stu-id="a3a69-158">Use one of the following Teams templates and components to help design your personal tab:</span></span>

* <span data-ttu-id="a3a69-159">[Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato digitalizado y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="a3a69-159">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="a3a69-160">[Panel de](../../concepts/design/design-teams-app-ui-templates.md#task-board)tareas: un panel de tareas, a veces denominado tablero de kanban o carriles de natación, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o los vales.</span><span class="sxs-lookup"><span data-stu-id="a3a69-160">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="a3a69-161">[Panel:](../../concepts/design/design-teams-app-ui-templates.md#dashboard)un panel es un lienzo que contiene varias tarjetas que proporcionan información general sobre los datos o el contenido.</span><span class="sxs-lookup"><span data-stu-id="a3a69-161">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="a3a69-162">[Formulario:](../../concepts/design/design-teams-app-ui-templates.md#form)los formularios son para recopilar, validar y enviar la entrada del usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="a3a69-162">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="a3a69-163">[Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacío se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.</span><span class="sxs-lookup"><span data-stu-id="a3a69-163">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="a3a69-164">[Navegación izquierda:](~/concepts/design/design-teams-app-advanced-ui-components.md#left-nav)el componente de navegación izquierdo puede ayudar si la aplicación personal requiere algo de navegación.</span><span class="sxs-lookup"><span data-stu-id="a3a69-164">[Left nav](~/concepts/design/design-teams-app-advanced-ui-components.md#left-nav): The left nav component can help if your personal app requires some navigation.</span></span> <span data-ttu-id="a3a69-165">En general, debe mantener la navegación al mínimo.</span><span class="sxs-lookup"><span data-stu-id="a3a69-165">In general, you should keep navigation to a minimum.</span></span>

## <a name="use-a-personal-app-bot"></a><span data-ttu-id="a3a69-166">Usar una aplicación personal (bot)</span><span class="sxs-lookup"><span data-stu-id="a3a69-166">Use a personal app (bot)</span></span>

<span data-ttu-id="a3a69-167">Las aplicaciones personales pueden incluir un bot para conversaciones uno a uno y notificaciones privadas (por ejemplo, cuando un compañero publica un comentario en la mesa de trabajo).</span><span class="sxs-lookup"><span data-stu-id="a3a69-167">Personal apps can include a bot for one-on-one conversations and private notifications (for instance, when a colleague posts a comment on your artboard).</span></span> <span data-ttu-id="a3a69-168">El bot está disponible en una pestaña especificada.</span><span class="sxs-lookup"><span data-stu-id="a3a69-168">The bot is available in a tab you specify.</span></span>

### <a name="anatomy-personal-app-bot"></a><span data-ttu-id="a3a69-169">Anatomía: aplicación personal (bot)</span><span class="sxs-lookup"><span data-stu-id="a3a69-169">Anatomy: Personal app (bot)</span></span>

# <a name="desktop"></a>[<span data-ttu-id="a3a69-170">Escritorio</span><span class="sxs-lookup"><span data-stu-id="a3a69-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="En el ejemplo se muestra la anatomía del componente de bot personal." border="false":::

|<span data-ttu-id="a3a69-172">Contador</span><span class="sxs-lookup"><span data-stu-id="a3a69-172">Counter</span></span>|<span data-ttu-id="a3a69-173">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3a69-173">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a3a69-174">A</span><span class="sxs-lookup"><span data-stu-id="a3a69-174">A</span></span>|<span data-ttu-id="a3a69-175">**Ficha Bot:** Por ejemplo, incluya una **pestaña Chat** para obtener acceso a las conversaciones y notificaciones del bot.</span><span class="sxs-lookup"><span data-stu-id="a3a69-175">**Bot tab**: For example, include a **Chat** tab to access bot conversations and notifications.</span></span>|
|<span data-ttu-id="a3a69-176">B</span><span class="sxs-lookup"><span data-stu-id="a3a69-176">B</span></span>|<span data-ttu-id="a3a69-177">**Mensaje de bot:** los bots suelen enviar mensajes y notificaciones en forma de tarjeta (como una tarjeta adaptable).</span><span class="sxs-lookup"><span data-stu-id="a3a69-177">**Bot message**: Bots often send messages and notifications in the form of a card (such as an Adaptive Card).</span></span>|
|<span data-ttu-id="a3a69-178">C</span><span class="sxs-lookup"><span data-stu-id="a3a69-178">C</span></span>|<span data-ttu-id="a3a69-179">**Cuadro Redacción:** campo de entrada para enviar mensajes al bot.</span><span class="sxs-lookup"><span data-stu-id="a3a69-179">**Compose box**: Input field for sending messages to the bot.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="a3a69-180">Móvil</span><span class="sxs-lookup"><span data-stu-id="a3a69-180">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-bot-anatomy.png" alt-text="En el ejemplo se muestra la anatomía del componente de bot personal." border="false":::

|<span data-ttu-id="a3a69-182">Contador</span><span class="sxs-lookup"><span data-stu-id="a3a69-182">Counter</span></span>|<span data-ttu-id="a3a69-183">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3a69-183">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a3a69-184">A</span><span class="sxs-lookup"><span data-stu-id="a3a69-184">A</span></span>|<span data-ttu-id="a3a69-185">**Punto de entrada del bot:** punto de entrada para que los usuarios accedan a la característica bot en la aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="a3a69-185">**Bot entry point**: Entry point for users to access the bot feature in your personal app.</span></span>|
|<span data-ttu-id="a3a69-186">B</span><span class="sxs-lookup"><span data-stu-id="a3a69-186">B</span></span>|<span data-ttu-id="a3a69-187">**Botón Atrás:** lleva a los usuarios de vuelta al área de trabajo privada.</span><span class="sxs-lookup"><span data-stu-id="a3a69-187">**Back button**: Takes users back to the private workspace.</span></span>|
|<span data-ttu-id="a3a69-188">C</span><span class="sxs-lookup"><span data-stu-id="a3a69-188">C</span></span>|<span data-ttu-id="a3a69-189">**Mensaje de bot:** los bots suelen enviar mensajes y notificaciones en forma de tarjeta (como una tarjeta adaptable).</span><span class="sxs-lookup"><span data-stu-id="a3a69-189">**Bot message**: Bots often send messages and notifications in the form of a card (such as an Adaptive Card).</span></span>|
|<span data-ttu-id="a3a69-190">D</span><span class="sxs-lookup"><span data-stu-id="a3a69-190">D</span></span>|<span data-ttu-id="a3a69-191">**Cuadro Redacción:** campo de entrada para enviar mensajes al bot.</span><span class="sxs-lookup"><span data-stu-id="a3a69-191">**Compose box**: Input field for sending messages to the bot.</span></span>|

---

## <a name="manage-a-personal-tab"></a><span data-ttu-id="a3a69-192">Administrar una pestaña personal</span><span class="sxs-lookup"><span data-stu-id="a3a69-192">Manage a personal tab</span></span>

<span data-ttu-id="a3a69-193">En el lado izquierdo de Teams, los usuarios pueden hacer clic con el botón secundario en la aplicación personal para anclar, quitar y configurar otras opciones de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3a69-193">On the left side of Teams, users can right click the personal app to pin, remove, and configure other app options.</span></span>

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="En el ejemplo se muestran las opciones para administrar una aplicación personal." border="false":::

## <a name="best-practices"></a><span data-ttu-id="a3a69-195">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="a3a69-195">Best practices</span></span>

<span data-ttu-id="a3a69-196">Usa estas recomendaciones para crear una experiencia de aplicación de calidad.</span><span class="sxs-lookup"><span data-stu-id="a3a69-196">Use these recommendations to create a quality app experience.</span></span>

### <a name="tab-priority"></a><span data-ttu-id="a3a69-197">Prioridad de tabulación</span><span class="sxs-lookup"><span data-stu-id="a3a69-197">Tab priority</span></span>

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a><span data-ttu-id="a3a69-198">Hacer: mostrar el contenido más relevante en la primera pestaña</span><span class="sxs-lookup"><span data-stu-id="a3a69-198">Do: Show the most relevant content in the first tab</span></span>

<span data-ttu-id="a3a69-199">Con el tamaño dinámico, las pestañas de la derecha pueden truncarse o quedar fuera de la vista.</span><span class="sxs-lookup"><span data-stu-id="a3a69-199">With responsive sizing, tabs on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="En el ejemplo se muestra una aplicación personal que muestra el contenido más relevante en la primera pestaña." border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a><span data-ttu-id="a3a69-201">Don't: Lead with secondary content or metadata</span><span class="sxs-lookup"><span data-stu-id="a3a69-201">Don’t: Lead with secondary content or metadata</span></span>

<span data-ttu-id="a3a69-202">Al igual que una aplicación web estándar, la navegación por pestañas debe avanzar en un orden que ayude a dar sentido a las características principales de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3a69-202">Like a standard web app, tab navigation should progress in an order that helps make sense of your app’s primary features.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="En el ejemplo se muestra una aplicación personal que lleva contenido o metadatos secundarios." border="false":::

### <a name="tab-hierarchy"></a><span data-ttu-id="a3a69-204">Jerarquía de tabulaciones</span><span class="sxs-lookup"><span data-stu-id="a3a69-204">Tab hierarchy</span></span>

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a><span data-ttu-id="a3a69-205">Hacer: las pestañas deben ser de igual jerarquía y representar páginas clave de la aplicación</span><span class="sxs-lookup"><span data-stu-id="a3a69-205">Do: Tabs should be of equal hierarchy and represent key app pages</span></span>

<span data-ttu-id="a3a69-206">Las pestañas deben clasificar las características y el contenido principales de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3a69-206">Your tabs should categorize your app’s primary features and content.</span></span> <span data-ttu-id="a3a69-207">Con el tamaño dinámico, el contenido de la derecha puede truncarse o quedar fuera de la vista.</span><span class="sxs-lookup"><span data-stu-id="a3a69-207">With responsive sizing, content on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="En el ejemplo se muestra una aplicación personal con pestañas de igual jerarquía." border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a><span data-ttu-id="a3a69-209">No: incluir diferentes niveles de jerarquía</span><span class="sxs-lookup"><span data-stu-id="a3a69-209">Don't: Include different levels of hierarchy</span></span>

<span data-ttu-id="a3a69-210">El contenido debe avanzar en un orden lógico que ayude a los usuarios a entenderlo.</span><span class="sxs-lookup"><span data-stu-id="a3a69-210">Your content should progress in a logical order that helps users make sense of it.</span></span> <span data-ttu-id="a3a69-211">Si tiene dos pestañas estrechamente relacionadas, considere la posibilidad de combinarlas en una pestaña.</span><span class="sxs-lookup"><span data-stu-id="a3a69-211">If you have two tabs that are closely related, consider combining them into one tab.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="En el ejemplo se muestra una aplicación personal con diferentes niveles de jerarquía." border="false":::

### <a name="first-run-experience"></a><span data-ttu-id="a3a69-213">Experiencia de primera ejecución</span><span class="sxs-lookup"><span data-stu-id="a3a69-213">First-run experience</span></span>

#### <a name="do-include-a-first-run-experience"></a><span data-ttu-id="a3a69-214">Do: Include a first-run experience</span><span class="sxs-lookup"><span data-stu-id="a3a69-214">Do: Include a first-run experience</span></span>

<span data-ttu-id="a3a69-215">Debería haber al menos una pantalla de bienvenida la primera vez que uses una aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="a3a69-215">There should be at least a welcome screen the first time you use a personal app.</span></span> <span data-ttu-id="a3a69-216">En el caso de los bots, describa lo que el bot puede hacer y proporcione acciones rápidas, como un botón de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="a3a69-216">For bots, describe what your bot can do and provide quick actions, such as a sign-in button.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="En el ejemplo se muestra qué hacer durante la primera ejecución de una aplicación personal." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="Otro ejemplo muestra qué hacer durante la primera ejecución de una aplicación personal." border="false":::

#### <a name="dont-start-with-a-blank-screen"></a><span data-ttu-id="a3a69-219">Don't: Start with a blank screen</span><span class="sxs-lookup"><span data-stu-id="a3a69-219">Don't: Start with a blank screen</span></span>

<span data-ttu-id="a3a69-220">Es posible que los usuarios se confundan si no se muestra nada la primera vez que ejecutan la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3a69-220">Users might be confused if nothing displays the first time they run your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="En el ejemplo se muestra lo que no se debe hacer durante la primera ejecución de una aplicación personal." border="false":::

### <a name="personalized-content"></a><span data-ttu-id="a3a69-222">Contenido personalizado</span><span class="sxs-lookup"><span data-stu-id="a3a69-222">Personalized content</span></span>

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a><span data-ttu-id="a3a69-223">Hacer: agregar contenido de aplicación relevante para un usuario</span><span class="sxs-lookup"><span data-stu-id="a3a69-223">Do: Aggregate app content relevant to a user</span></span>

<span data-ttu-id="a3a69-224">Tanto si se trata de una pestaña personal como de un bot, muestra contenido relacionado solo con la actividad de un usuario en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3a69-224">Whether it's a personal tab or bot, display content related to only a user's activity in your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="En el ejemplo se muestra qué hacer con una aplicación personal y contenido personalizado." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="Otro ejemplo muestra qué hacer con una aplicación personal y contenido personalizado." border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a><span data-ttu-id="a3a69-227">No: mostrar contenido demasiado amplio o no relacionado</span><span class="sxs-lookup"><span data-stu-id="a3a69-227">Don’t: Show unrelated or overly broad content</span></span>

<span data-ttu-id="a3a69-228">En contextos personales, no muestre contenido para equipos de los que un usuario no forma parte.</span><span class="sxs-lookup"><span data-stu-id="a3a69-228">In personal contexts, don’t display content for teams a user isn't part of.</span></span> <span data-ttu-id="a3a69-229">El contenido del bot personal debe centrarse en el individuo, no en un grupo.</span><span class="sxs-lookup"><span data-stu-id="a3a69-229">Personal bot content should focus on the individual—not a group.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="En el ejemplo se muestra qué no hacer con una aplicación personal y contenido personalizado." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="Otro ejemplo muestra qué no hacer con una aplicación personal y contenido personalizado." border="false":::

### <a name="complex-app-features"></a><span data-ttu-id="a3a69-232">Características complejas de la aplicación</span><span class="sxs-lookup"><span data-stu-id="a3a69-232">Complex app features</span></span>

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a><span data-ttu-id="a3a69-233">Hacer: permitir que los usuarios accedan a características complejas en un explorador</span><span class="sxs-lookup"><span data-stu-id="a3a69-233">Do: Allow users to access complex features in a browser</span></span>

<span data-ttu-id="a3a69-234">La aplicación debe centrarse en las tareas principales Teams, pero aún puedes ver la aplicación completa e independiente en un explorador.</span><span class="sxs-lookup"><span data-stu-id="a3a69-234">Your app should focus on core tasks in Teams, but you can still view the full, standalone app in a browser.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="En el ejemplo se muestra cómo controlar las características complejas de la aplicación con una aplicación personal." border="false":::

#### <a name="dont-include-your-entire-app"></a><span data-ttu-id="a3a69-236">No: incluir toda la aplicación</span><span class="sxs-lookup"><span data-stu-id="a3a69-236">Don’t: Include your entire app</span></span>

<span data-ttu-id="a3a69-237">A menos que creaste la aplicación específicamente para Teams, probablemente tienes características que no tienen sentido en una herramienta de colaboración.</span><span class="sxs-lookup"><span data-stu-id="a3a69-237">Unless you created your app specifically for Teams, you probably have features that don’t make sense in a collaboration tool.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="En el ejemplo se muestra cómo no controlar las características complejas de la aplicación con una aplicación personal." border="false":::

## <a name="see-also"></a><span data-ttu-id="a3a69-239">Consulte también</span><span class="sxs-lookup"><span data-stu-id="a3a69-239">See also</span></span>

<span data-ttu-id="a3a69-240">Estas otras directrices de diseño pueden ayudar en función del ámbito de la aplicación personal:</span><span class="sxs-lookup"><span data-stu-id="a3a69-240">These other design guidelines may help depending on the scope of your personal app:</span></span>

* [<span data-ttu-id="a3a69-241">Diseño de la pestaña</span><span class="sxs-lookup"><span data-stu-id="a3a69-241">Designing your tab</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="a3a69-242">Diseño del bot</span><span class="sxs-lookup"><span data-stu-id="a3a69-242">Designing you bot</span></span>](../../bots/design/bots.md)

---
title: Diseño de su aplicación personal
description: Aprende a diseñar una aplicación Teams personal y obtener el kit Microsoft Teams interfaz de usuario.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: b3f08c39a7900b80fb46d167fae8d9e8bdbcc574
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101558"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a><span data-ttu-id="696a9-103">Diseñar tu aplicación personal para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="696a9-103">Designing your personal app for Microsoft Teams</span></span>

<span data-ttu-id="696a9-104">Una aplicación personal puede ser un bot, un área de trabajo privada o ambos.</span><span class="sxs-lookup"><span data-stu-id="696a9-104">A personal app can be a bot, private workspace, or both.</span></span> <span data-ttu-id="696a9-105">A veces funciona como un lugar para crear o ver contenido, otras veces ofrece al usuario una vista visual de todo lo que es suyo cuando la aplicación se ha configurado como una pestaña en varios canales.</span><span class="sxs-lookup"><span data-stu-id="696a9-105">Sometimes it functions like a place to create or view content, other times it offers the user a bird’s eye view of everything that's theirs when the app has been configured as a tab in multiple channels.</span></span>

<span data-ttu-id="696a9-106">Para guiar el diseño de la aplicación, la siguiente información describe e ilustra cómo las personas pueden agregar, usar y administrar aplicaciones personales en Teams.</span><span class="sxs-lookup"><span data-stu-id="696a9-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage personal apps in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="696a9-107">Kit de UI de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="696a9-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="696a9-108">Puedes encontrar instrucciones completas de diseño de aplicaciones personales, incluidos los elementos que puedes agarrar y modificar según sea necesario, en el kit de interfaz Microsoft Teams usuario.</span><span class="sxs-lookup"><span data-stu-id="696a9-108">You can find comprehensive personal app design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="696a9-109">El kit de interfaz de usuario también tiene temas esenciales, como la accesibilidad y el tamaño dinámico que no se tratan aquí.</span><span class="sxs-lookup"><span data-stu-id="696a9-109">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="696a9-110">Obtener el Kit de UI de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="696a9-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a><span data-ttu-id="696a9-111">Agregar una aplicación personal</span><span class="sxs-lookup"><span data-stu-id="696a9-111">Add a personal app</span></span>

<span data-ttu-id="696a9-112">Puedes agregar una aplicación personal desde la tienda Teams (AppSource) o el  menú desplegable de la aplicación seleccionando el icono Más en el lado izquierdo de Teams (que se muestra en el ejemplo siguiente).</span><span class="sxs-lookup"><span data-stu-id="696a9-112">You can add a personal app from the Teams store (AppSource) or the app flyout by selecting the **More** icon on the left side of Teams (shown in the following example).</span></span>

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="En el ejemplo se muestra cómo agregar una aplicación personal desde el menú desplegable de la aplicación." border="false":::

## <a name="use-a-personal-app-private-workspace"></a><span data-ttu-id="696a9-114">Usar una aplicación personal (área de trabajo privada)</span><span class="sxs-lookup"><span data-stu-id="696a9-114">Use a personal app (private workspace)</span></span>

<span data-ttu-id="696a9-115">Con un área de trabajo privada, puedes ver contenido de la aplicación que sea significativo para ti en una ubicación central sin salir de Teams.</span><span class="sxs-lookup"><span data-stu-id="696a9-115">With a private workspace, you can view app content that's meaningful to you in a central location without leaving Teams.</span></span>

<span data-ttu-id="696a9-116">(Nota de implementación: el área de trabajo privada se basa en la funcionalidad [*de tabulación*](../../build-your-first-app/build-personal-tab.md) personal).</span><span class="sxs-lookup"><span data-stu-id="696a9-116">(Implementation note: The private workspace is based on the [*personal tab*](../../build-your-first-app/build-personal-tab.md) capability.)</span></span>

### <a name="anatomy-personal-app-private-workspace"></a><span data-ttu-id="696a9-117">Anatomía: aplicación personal (área de trabajo privada)</span><span class="sxs-lookup"><span data-stu-id="696a9-117">Anatomy: Personal app (private workspace)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="En el ejemplo se muestra la anatomía del componente de la pestaña personal." border="false":::

|<span data-ttu-id="696a9-119">Contador</span><span class="sxs-lookup"><span data-stu-id="696a9-119">Counter</span></span>|<span data-ttu-id="696a9-120">Descripción</span><span class="sxs-lookup"><span data-stu-id="696a9-120">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="696a9-121">A</span><span class="sxs-lookup"><span data-stu-id="696a9-121">A</span></span>|<span data-ttu-id="696a9-122">**Atribución de la aplicación:** el logotipo y el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="696a9-122">**App attribution**: Your app logo and name.</span></span>|
|<span data-ttu-id="696a9-123">B</span><span class="sxs-lookup"><span data-stu-id="696a9-123">B</span></span>|<span data-ttu-id="696a9-124">**Pestañas:** proporciona navegación para tu aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="696a9-124">**Tabs**: Provides navigation for your personal app.</span></span> <span data-ttu-id="696a9-125">Por ejemplo, incluya una **pestaña Acerca o** **Ayuda.**</span><span class="sxs-lookup"><span data-stu-id="696a9-125">For example, include an **About** or **Help** tab.</span></span>|
|<span data-ttu-id="696a9-126">C</span><span class="sxs-lookup"><span data-stu-id="696a9-126">C</span></span>|<span data-ttu-id="696a9-127">**Vista emergente:** inserta el contenido de la aplicación desde una ventana primaria a una ventana secundaria independiente.</span><span class="sxs-lookup"><span data-stu-id="696a9-127">**Popout view**: Pushes your app content from a parent window to a standalone child window.</span></span>|
|<span data-ttu-id="696a9-128">D</span><span class="sxs-lookup"><span data-stu-id="696a9-128">D</span></span>|<span data-ttu-id="696a9-129">**Más menú:** incluye información y opciones adicionales de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="696a9-129">**More menu**: Includes additional app information and options.</span></span> <span data-ttu-id="696a9-130">(También puede crear una **Configuración** una pestaña).</span><span class="sxs-lookup"><span data-stu-id="696a9-130">(You could alternatively make **Settings** a tab.)</span></span>|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de la pestaña personal." border="false":::

|<span data-ttu-id="696a9-132">Contador</span><span class="sxs-lookup"><span data-stu-id="696a9-132">Counter</span></span>|<span data-ttu-id="696a9-133">Descripción</span><span class="sxs-lookup"><span data-stu-id="696a9-133">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="696a9-134">A</span><span class="sxs-lookup"><span data-stu-id="696a9-134">A</span></span>|<span data-ttu-id="696a9-135">**Pestañas:** proporciona navegación para tu aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="696a9-135">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="696a9-136">1</span><span class="sxs-lookup"><span data-stu-id="696a9-136">1</span></span>|<span data-ttu-id="696a9-137">**iframe:** muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="696a9-137">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="696a9-138">Diseño con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="696a9-138">Designing with UI templates</span></span>

<span data-ttu-id="696a9-139">Usa una de las siguientes plantillas Teams interfaz de usuario para ayudar a diseñar tu pestaña personal:</span><span class="sxs-lookup"><span data-stu-id="696a9-139">Use one of the following Teams UI templates to help design your personal tab:</span></span>

* <span data-ttu-id="696a9-140">[Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato digitalizado y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="696a9-140">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="696a9-141">[Panel de](../../concepts/design/design-teams-app-ui-templates.md#task-board)tareas: un panel de tareas, a veces denominado tablero de kanban o carriles de natación, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o los vales.</span><span class="sxs-lookup"><span data-stu-id="696a9-141">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="696a9-142">[Panel:](../../concepts/design/design-teams-app-ui-templates.md#dashboard)un panel es un lienzo que contiene varias tarjetas que proporcionan información general sobre los datos o el contenido.</span><span class="sxs-lookup"><span data-stu-id="696a9-142">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="696a9-143">[Formulario:](../../concepts/design/design-teams-app-ui-templates.md#form)los formularios son para recopilar, validar y enviar la entrada del usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="696a9-143">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="696a9-144">[Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacío se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.</span><span class="sxs-lookup"><span data-stu-id="696a9-144">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="696a9-145">[Navegación izquierda:](../../concepts/design/design-teams-app-ui-templates.md#left-nav)la plantilla de navegación izquierda puede ayudar si la pestaña requiere algo de navegación.</span><span class="sxs-lookup"><span data-stu-id="696a9-145">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="696a9-146">En general, debe mantener la navegación por pestañas al mínimo.</span><span class="sxs-lookup"><span data-stu-id="696a9-146">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-personal-app-bot"></a><span data-ttu-id="696a9-147">Usar una aplicación personal (bot)</span><span class="sxs-lookup"><span data-stu-id="696a9-147">Use a personal app (bot)</span></span>

<span data-ttu-id="696a9-148">Las aplicaciones personales pueden incluir un bot para conversaciones uno a uno y notificaciones privadas (por ejemplo, cuando un compañero publica un comentario en la mesa de trabajo).</span><span class="sxs-lookup"><span data-stu-id="696a9-148">Personal apps can include a bot for one-on-one conversations and private notifications (for instance, when a colleague posts a comment on your artboard).</span></span> <span data-ttu-id="696a9-149">El bot está disponible en una pestaña especificada.</span><span class="sxs-lookup"><span data-stu-id="696a9-149">The bot is available in a tab you specify.</span></span>

### <a name="anatomy-personal-app-bot"></a><span data-ttu-id="696a9-150">Anatomía: aplicación personal (bot)</span><span class="sxs-lookup"><span data-stu-id="696a9-150">Anatomy: Personal app (bot)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="En el ejemplo se muestra la anatomía del componente de bot personal." border="false":::

|<span data-ttu-id="696a9-152">Contador</span><span class="sxs-lookup"><span data-stu-id="696a9-152">Counter</span></span>|<span data-ttu-id="696a9-153">Descripción</span><span class="sxs-lookup"><span data-stu-id="696a9-153">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="696a9-154">A</span><span class="sxs-lookup"><span data-stu-id="696a9-154">A</span></span>|<span data-ttu-id="696a9-155">**Ficha Bot:** Por ejemplo, incluya una **pestaña Chat** para obtener acceso a las conversaciones y notificaciones del bot.</span><span class="sxs-lookup"><span data-stu-id="696a9-155">**Bot tab**: For example, include a **Chat** tab to access bot conversations and notifications.</span></span>|
|<span data-ttu-id="696a9-156">B</span><span class="sxs-lookup"><span data-stu-id="696a9-156">B</span></span>|<span data-ttu-id="696a9-157">**Mensaje de bot:** los bots suelen enviar mensajes y notificaciones en forma de tarjeta (como una tarjeta adaptable).</span><span class="sxs-lookup"><span data-stu-id="696a9-157">**Bot message**: Bots often send messages and notifications in the form of a card (such as an Adaptive Card).</span></span>|
|<span data-ttu-id="696a9-158">C</span><span class="sxs-lookup"><span data-stu-id="696a9-158">C</span></span>|<span data-ttu-id="696a9-159">**Cuadro Redacción:** campo de entrada para enviar mensajes al bot.</span><span class="sxs-lookup"><span data-stu-id="696a9-159">**Compose box**: Input field for sending messages to the bot.</span></span>|

## <a name="manage-a-personal-tab"></a><span data-ttu-id="696a9-160">Administrar una pestaña personal</span><span class="sxs-lookup"><span data-stu-id="696a9-160">Manage a personal tab</span></span>

<span data-ttu-id="696a9-161">En el lado izquierdo de Teams, los usuarios pueden hacer clic con el botón secundario en la aplicación personal para anclar, quitar y configurar otras opciones de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="696a9-161">On the left side of Teams, users can right click the personal app to pin, remove, and configure other app options.</span></span>

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="En el ejemplo se muestran las opciones para administrar una aplicación personal." border="false":::

## <a name="best-practices"></a><span data-ttu-id="696a9-163">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="696a9-163">Best practices</span></span>

<span data-ttu-id="696a9-164">Usa estas recomendaciones para crear una experiencia de aplicación de calidad.</span><span class="sxs-lookup"><span data-stu-id="696a9-164">Use these recommendations to create a quality app experience.</span></span>

### <a name="tab-priority"></a><span data-ttu-id="696a9-165">Prioridad de tabulación</span><span class="sxs-lookup"><span data-stu-id="696a9-165">Tab priority</span></span>

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a><span data-ttu-id="696a9-166">Hacer: mostrar el contenido más relevante en la primera pestaña</span><span class="sxs-lookup"><span data-stu-id="696a9-166">Do: Show the most relevant content in the first tab</span></span>

<span data-ttu-id="696a9-167">Con el tamaño dinámico, las pestañas de la derecha pueden truncarse o quedar fuera de la vista.</span><span class="sxs-lookup"><span data-stu-id="696a9-167">With responsive sizing, tabs on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="En el ejemplo se muestra una aplicación personal que muestra el contenido más relevante en la primera pestaña." border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a><span data-ttu-id="696a9-169">Don't: Lead with secondary content or metadata</span><span class="sxs-lookup"><span data-stu-id="696a9-169">Don’t: Lead with secondary content or metadata</span></span>

<span data-ttu-id="696a9-170">Al igual que una aplicación web estándar, la navegación por pestañas debe avanzar en un orden que ayude a dar sentido a las características principales de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="696a9-170">Like a standard web app, tab navigation should progress in an order that helps make sense of your app’s primary features.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="En el ejemplo se muestra una aplicación personal que lleva contenido o metadatos secundarios." border="false":::

### <a name="tab-hierarchy"></a><span data-ttu-id="696a9-172">Jerarquía de tabulaciones</span><span class="sxs-lookup"><span data-stu-id="696a9-172">Tab hierarchy</span></span>

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a><span data-ttu-id="696a9-173">Hacer: las pestañas deben ser de igual jerarquía y representar páginas clave de la aplicación</span><span class="sxs-lookup"><span data-stu-id="696a9-173">Do: Tabs should be of equal hierarchy and represent key app pages</span></span>

<span data-ttu-id="696a9-174">Las pestañas deben clasificar las características y el contenido principales de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="696a9-174">Your tabs should categorize your app’s primary features and content.</span></span> <span data-ttu-id="696a9-175">Con el tamaño dinámico, el contenido de la derecha puede truncarse o quedar fuera de la vista.</span><span class="sxs-lookup"><span data-stu-id="696a9-175">With responsive sizing, content on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="En el ejemplo se muestra una aplicación personal con pestañas de igual jerarquía." border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a><span data-ttu-id="696a9-177">No: incluir diferentes niveles de jerarquía</span><span class="sxs-lookup"><span data-stu-id="696a9-177">Don't: Include different levels of hierarchy</span></span>

<span data-ttu-id="696a9-178">El contenido debe avanzar en un orden lógico que ayude a los usuarios a entenderlo.</span><span class="sxs-lookup"><span data-stu-id="696a9-178">Your content should progress in a logical order that helps users make sense of it.</span></span> <span data-ttu-id="696a9-179">Si tiene dos pestañas estrechamente relacionadas, considere la posibilidad de combinarlas en una pestaña.</span><span class="sxs-lookup"><span data-stu-id="696a9-179">If you have two tabs that are closely related, consider combining them into one tab.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="En el ejemplo se muestra una aplicación personal con diferentes niveles de jerarquía." border="false":::

### <a name="first-run-experience"></a><span data-ttu-id="696a9-181">Experiencia de primera ejecución</span><span class="sxs-lookup"><span data-stu-id="696a9-181">First-run experience</span></span>

#### <a name="do-include-a-first-run-experience"></a><span data-ttu-id="696a9-182">Do: Include a first-run experience</span><span class="sxs-lookup"><span data-stu-id="696a9-182">Do: Include a first-run experience</span></span>

<span data-ttu-id="696a9-183">Debería haber al menos una pantalla de bienvenida la primera vez que uses una aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="696a9-183">There should be at least a welcome screen the first time you use a personal app.</span></span> <span data-ttu-id="696a9-184">En el caso de los bots, describa lo que el bot puede hacer y proporcione acciones rápidas, como un botón de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="696a9-184">For bots, describe what your bot can do and provide quick actions, such as a sign-in button.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="En el ejemplo se muestra qué hacer durante la primera ejecución de una aplicación personal." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="Otro ejemplo muestra qué hacer durante la primera ejecución de una aplicación personal." border="false":::

#### <a name="dont-start-with-a-blank-screen"></a><span data-ttu-id="696a9-187">Don't: Start with a blank screen</span><span class="sxs-lookup"><span data-stu-id="696a9-187">Don't: Start with a blank screen</span></span>

<span data-ttu-id="696a9-188">Es posible que los usuarios se confundan si no se muestra nada la primera vez que ejecutan la aplicación.</span><span class="sxs-lookup"><span data-stu-id="696a9-188">Users might be confused if nothing displays the first time they run your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="En el ejemplo se muestra lo que no se debe hacer durante la primera ejecución de una aplicación personal." border="false":::

### <a name="personalized-content"></a><span data-ttu-id="696a9-190">Contenido personalizado</span><span class="sxs-lookup"><span data-stu-id="696a9-190">Personalized content</span></span>

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a><span data-ttu-id="696a9-191">Hacer: agregar contenido de aplicación relevante para un usuario</span><span class="sxs-lookup"><span data-stu-id="696a9-191">Do: Aggregate app content relevant to a user</span></span>

<span data-ttu-id="696a9-192">Tanto si se trata de una pestaña personal como de un bot, muestra contenido relacionado solo con la actividad de un usuario en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="696a9-192">Whether it's a personal tab or bot, display content related to only a user's activity in your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="En el ejemplo se muestra qué hacer con una aplicación personal y contenido personalizado." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="Otro ejemplo muestra qué hacer con una aplicación personal y contenido personalizado." border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a><span data-ttu-id="696a9-195">No: mostrar contenido demasiado amplio o no relacionado</span><span class="sxs-lookup"><span data-stu-id="696a9-195">Don’t: Show unrelated or overly broad content</span></span>

<span data-ttu-id="696a9-196">En contextos personales, no muestre contenido para equipos de los que un usuario no forma parte.</span><span class="sxs-lookup"><span data-stu-id="696a9-196">In personal contexts, don’t display content for teams a user isn't part of.</span></span> <span data-ttu-id="696a9-197">El contenido del bot personal debe centrarse en el individuo, no en un grupo.</span><span class="sxs-lookup"><span data-stu-id="696a9-197">Personal bot content should focus on the individual—not a group.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="En el ejemplo se muestra qué no hacer con una aplicación personal y contenido personalizado." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="Otro ejemplo muestra qué no hacer con una aplicación personal y contenido personalizado." border="false":::

### <a name="complex-app-features"></a><span data-ttu-id="696a9-200">Características complejas de la aplicación</span><span class="sxs-lookup"><span data-stu-id="696a9-200">Complex app features</span></span>

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a><span data-ttu-id="696a9-201">Hacer: permitir que los usuarios accedan a características complejas en un explorador</span><span class="sxs-lookup"><span data-stu-id="696a9-201">Do: Allow users to access complex features in a browser</span></span>

<span data-ttu-id="696a9-202">La aplicación debe centrarse en las tareas principales Teams, pero aún puedes ver la aplicación completa e independiente en un explorador.</span><span class="sxs-lookup"><span data-stu-id="696a9-202">Your app should focus on core tasks in Teams, but you can still view the full, standalone app in a browser.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="En el ejemplo se muestra cómo controlar las características complejas de la aplicación con una aplicación personal." border="false":::

#### <a name="dont-include-your-entire-app"></a><span data-ttu-id="696a9-204">No: incluir toda la aplicación</span><span class="sxs-lookup"><span data-stu-id="696a9-204">Don’t: Include your entire app</span></span>

<span data-ttu-id="696a9-205">A menos que creaste la aplicación específicamente para Teams, probablemente tienes características que no tienen sentido en una herramienta de colaboración.</span><span class="sxs-lookup"><span data-stu-id="696a9-205">Unless you created your app specifically for Teams, you probably have features that don’t make sense in a collaboration tool.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="En el ejemplo se muestra cómo no controlar las características complejas de la aplicación con una aplicación personal." border="false":::

## <a name="see-also"></a><span data-ttu-id="696a9-207">Vea también</span><span class="sxs-lookup"><span data-stu-id="696a9-207">See also</span></span>

<span data-ttu-id="696a9-208">Estas otras directrices de diseño pueden ayudar en función del ámbito de la aplicación personal:</span><span class="sxs-lookup"><span data-stu-id="696a9-208">These other design guidelines may help depending on the scope of your personal app:</span></span>

* [<span data-ttu-id="696a9-209">Diseño de la pestaña</span><span class="sxs-lookup"><span data-stu-id="696a9-209">Designing your tab</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="696a9-210">Diseño del bot</span><span class="sxs-lookup"><span data-stu-id="696a9-210">Designing you bot</span></span>](../../bots/design/bots.md)

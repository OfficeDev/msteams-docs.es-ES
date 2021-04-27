---
title: Diseño de su aplicación personal
description: Aprende a diseñar una aplicación personal de Teams y a obtener el Kit de interfaz de usuario de Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 8302f3768034014ef5a446effeee0603afe4a5f4
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020761"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a><span data-ttu-id="92a4f-103">Diseño de la aplicación personal para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="92a4f-103">Designing your personal app for Microsoft Teams</span></span>

<span data-ttu-id="92a4f-104">Una aplicación personal puede ser un bot, un área de trabajo privada o ambos.</span><span class="sxs-lookup"><span data-stu-id="92a4f-104">A personal app can be a bot, private workspace, or both.</span></span> <span data-ttu-id="92a4f-105">A veces funciona como un lugar para crear o ver contenido, otras veces ofrece al usuario una vista visual de todo lo que es suyo cuando la aplicación se ha configurado como una pestaña en varios canales.</span><span class="sxs-lookup"><span data-stu-id="92a4f-105">Sometimes it functions like a place to create or view content, other times it offers the user a bird’s eye view of everything that's theirs when the app has been configured as a tab in multiple channels.</span></span>

<span data-ttu-id="92a4f-106">Para guiar el diseño de la aplicación, la siguiente información describe e ilustra cómo las personas pueden agregar, usar y administrar aplicaciones personales en Teams.</span><span class="sxs-lookup"><span data-stu-id="92a4f-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage personal apps in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="92a4f-107">Kit de UI de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="92a4f-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="92a4f-108">Puedes encontrar instrucciones completas de diseño de aplicaciones personales, incluidos los elementos que puedes agarrar y modificar según sea necesario, en el Kit de interfaz de usuario de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="92a4f-108">You can find comprehensive personal app design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="92a4f-109">El kit de interfaz de usuario también tiene temas esenciales, como la accesibilidad y el tamaño dinámico que no se tratan aquí.</span><span class="sxs-lookup"><span data-stu-id="92a4f-109">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="92a4f-110">Obtener el Kit de UI de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="92a4f-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a><span data-ttu-id="92a4f-111">Agregar una aplicación personal</span><span class="sxs-lookup"><span data-stu-id="92a4f-111">Add a personal app</span></span>

<span data-ttu-id="92a4f-112">Puedes agregar una aplicación personal desde la Tienda Teams (AppSource)  o el menú desplegable de la aplicación seleccionando el icono Más a la izquierda de Teams (que se muestra en el siguiente ejemplo).</span><span class="sxs-lookup"><span data-stu-id="92a4f-112">You can add a personal app from the Teams store (AppSource) or the app flyout by selecting the **More** icon on the left side of Teams (shown in the following example).</span></span>

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="En el ejemplo se muestra cómo agregar una aplicación personal desde el menú desplegable de la aplicación." border="false":::

## <a name="use-a-personal-app-private-workspace"></a><span data-ttu-id="92a4f-114">Usar una aplicación personal (área de trabajo privada)</span><span class="sxs-lookup"><span data-stu-id="92a4f-114">Use a personal app (private workspace)</span></span>

<span data-ttu-id="92a4f-115">Con un área de trabajo privada, puedes ver contenido de la aplicación que sea significativo para ti en una ubicación central sin salir de Teams.</span><span class="sxs-lookup"><span data-stu-id="92a4f-115">With a private workspace, you can view app content that's meaningful to you in a central location without leaving Teams.</span></span>

<span data-ttu-id="92a4f-116">(Nota de implementación: el área de trabajo privada se basa en la funcionalidad [*de tabulación*](../../build-your-first-app/build-personal-tab.md) personal).</span><span class="sxs-lookup"><span data-stu-id="92a4f-116">(Implementation note: The private workspace is based on the [*personal tab*](../../build-your-first-app/build-personal-tab.md) capability.)</span></span>

### <a name="anatomy-personal-app-private-workspace"></a><span data-ttu-id="92a4f-117">Anatomía: aplicación personal (área de trabajo privada)</span><span class="sxs-lookup"><span data-stu-id="92a4f-117">Anatomy: Personal app (private workspace)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="En el ejemplo se muestra la anatomía del componente de la pestaña personal." border="false":::

|<span data-ttu-id="92a4f-119">Contador</span><span class="sxs-lookup"><span data-stu-id="92a4f-119">Counter</span></span>|<span data-ttu-id="92a4f-120">Descripción</span><span class="sxs-lookup"><span data-stu-id="92a4f-120">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="92a4f-121">A</span><span class="sxs-lookup"><span data-stu-id="92a4f-121">A</span></span>|<span data-ttu-id="92a4f-122">**Atribución de la aplicación:** el logotipo y el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="92a4f-122">**App attribution**: Your app logo and name.</span></span>|
|<span data-ttu-id="92a4f-123">B</span><span class="sxs-lookup"><span data-stu-id="92a4f-123">B</span></span>|<span data-ttu-id="92a4f-124">**Pestañas:** proporciona navegación para tu aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="92a4f-124">**Tabs**: Provides navigation for your personal app.</span></span> <span data-ttu-id="92a4f-125">Por ejemplo, incluya una **pestaña Acerca o** **Ayuda.**</span><span class="sxs-lookup"><span data-stu-id="92a4f-125">For example, include an **About** or **Help** tab.</span></span>|
|<span data-ttu-id="92a4f-126">C</span><span class="sxs-lookup"><span data-stu-id="92a4f-126">C</span></span>|<span data-ttu-id="92a4f-127">**Vista emergente:** inserta el contenido de la aplicación desde una ventana primaria a una ventana secundaria independiente.</span><span class="sxs-lookup"><span data-stu-id="92a4f-127">**Popout view**: Pushes your app content from a parent window to a standalone child window.</span></span>|
|<span data-ttu-id="92a4f-128">D</span><span class="sxs-lookup"><span data-stu-id="92a4f-128">D</span></span>|<span data-ttu-id="92a4f-129">**Más menú:** incluye información y opciones adicionales de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="92a4f-129">**More menu**: Includes additional app information and options.</span></span> <span data-ttu-id="92a4f-130">(También puede hacer que **Configuración** sea una pestaña).</span><span class="sxs-lookup"><span data-stu-id="92a4f-130">(You could alternatively make **Settings** a tab.)</span></span>|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de la pestaña personal." border="false":::

|<span data-ttu-id="92a4f-132">Contador</span><span class="sxs-lookup"><span data-stu-id="92a4f-132">Counter</span></span>|<span data-ttu-id="92a4f-133">Descripción</span><span class="sxs-lookup"><span data-stu-id="92a4f-133">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="92a4f-134">A</span><span class="sxs-lookup"><span data-stu-id="92a4f-134">A</span></span>|<span data-ttu-id="92a4f-135">**Pestañas:** proporciona navegación para tu aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="92a4f-135">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="92a4f-136">1</span><span class="sxs-lookup"><span data-stu-id="92a4f-136">1</span></span>|<span data-ttu-id="92a4f-137">**iframe:** muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="92a4f-137">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="92a4f-138">Diseño con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="92a4f-138">Designing with UI templates</span></span>

<span data-ttu-id="92a4f-139">Usa una de las siguientes plantillas de interfaz de usuario de Teams para ayudar a diseñar tu pestaña personal:</span><span class="sxs-lookup"><span data-stu-id="92a4f-139">Use one of the following Teams UI templates to help design your personal tab:</span></span>

* <span data-ttu-id="92a4f-140">[Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato digitalizado y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="92a4f-140">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="92a4f-141">[Panel de](../../concepts/design/design-teams-app-ui-templates.md#task-board)tareas: un panel de tareas, a veces denominado tablero de kanban o carriles de natación, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o los vales.</span><span class="sxs-lookup"><span data-stu-id="92a4f-141">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="92a4f-142">[Panel:](../../concepts/design/design-teams-app-ui-templates.md#dashboard)un panel es un lienzo que contiene varias tarjetas que proporcionan información general sobre los datos o el contenido.</span><span class="sxs-lookup"><span data-stu-id="92a4f-142">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="92a4f-143">[Formulario:](../../concepts/design/design-teams-app-ui-templates.md#form)los formularios son para recopilar, validar y enviar la entrada del usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="92a4f-143">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="92a4f-144">[Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacío se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.</span><span class="sxs-lookup"><span data-stu-id="92a4f-144">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="92a4f-145">[Navegación izquierda:](../../concepts/design/design-teams-app-ui-templates.md#left-nav)la plantilla de navegación izquierda puede ayudar si la pestaña requiere algo de navegación.</span><span class="sxs-lookup"><span data-stu-id="92a4f-145">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="92a4f-146">En general, debe mantener la navegación por pestañas al mínimo.</span><span class="sxs-lookup"><span data-stu-id="92a4f-146">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-personal-app-bot"></a><span data-ttu-id="92a4f-147">Usar una aplicación personal (bot)</span><span class="sxs-lookup"><span data-stu-id="92a4f-147">Use a personal app (bot)</span></span>

<span data-ttu-id="92a4f-148">Las aplicaciones personales pueden incluir un bot para conversaciones uno a uno y notificaciones privadas (por ejemplo, cuando un compañero publica un comentario en la mesa de trabajo).</span><span class="sxs-lookup"><span data-stu-id="92a4f-148">Personal apps can include a bot for one-on-one conversations and private notifications (for instance, when a colleague posts a comment on your artboard).</span></span> <span data-ttu-id="92a4f-149">El bot está disponible en una pestaña especificada.</span><span class="sxs-lookup"><span data-stu-id="92a4f-149">The bot is available in a tab you specify.</span></span>

### <a name="anatomy-personal-app-bot"></a><span data-ttu-id="92a4f-150">Anatomía: aplicación personal (bot)</span><span class="sxs-lookup"><span data-stu-id="92a4f-150">Anatomy: Personal app (bot)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="En el ejemplo se muestra la anatomía del componente de bot personal." border="false":::

|<span data-ttu-id="92a4f-152">Contador</span><span class="sxs-lookup"><span data-stu-id="92a4f-152">Counter</span></span>|<span data-ttu-id="92a4f-153">Descripción</span><span class="sxs-lookup"><span data-stu-id="92a4f-153">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="92a4f-154">A</span><span class="sxs-lookup"><span data-stu-id="92a4f-154">A</span></span>|<span data-ttu-id="92a4f-155">**Ficha Bot:** Por ejemplo, incluya una **pestaña Chat** para obtener acceso a las conversaciones y notificaciones del bot.</span><span class="sxs-lookup"><span data-stu-id="92a4f-155">**Bot tab**: For example, include a **Chat** tab to access bot conversations and notifications.</span></span>|
|<span data-ttu-id="92a4f-156">B</span><span class="sxs-lookup"><span data-stu-id="92a4f-156">B</span></span>|<span data-ttu-id="92a4f-157">**Mensaje de bot:** los bots suelen enviar mensajes y notificaciones en forma de tarjeta (como una tarjeta adaptable).</span><span class="sxs-lookup"><span data-stu-id="92a4f-157">**Bot message**: Bots often send messages and notifications in the form of a card (such as an Adaptive Card).</span></span>|
|<span data-ttu-id="92a4f-158">C</span><span class="sxs-lookup"><span data-stu-id="92a4f-158">C</span></span>|<span data-ttu-id="92a4f-159">**Cuadro Redacción:** campo de entrada para enviar mensajes al bot.</span><span class="sxs-lookup"><span data-stu-id="92a4f-159">**Compose box**: Input field for sending messages to the bot.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="92a4f-160">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="92a4f-160">Best practices</span></span>

### <a name="tab-priority"></a><span data-ttu-id="92a4f-161">Prioridad de tabulación</span><span class="sxs-lookup"><span data-stu-id="92a4f-161">Tab priority</span></span>

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a><span data-ttu-id="92a4f-162">Hacer: mostrar el contenido más relevante en la primera pestaña</span><span class="sxs-lookup"><span data-stu-id="92a4f-162">Do: Show the most relevant content in the first tab</span></span>

<span data-ttu-id="92a4f-163">Con el tamaño dinámico, las pestañas de la derecha pueden truncarse o quedar fuera de la vista.</span><span class="sxs-lookup"><span data-stu-id="92a4f-163">With responsive sizing, tabs on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="En el ejemplo se muestra un procedimiento recomendado de aplicación personal." border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a><span data-ttu-id="92a4f-165">Don't: Lead with secondary content or metadata</span><span class="sxs-lookup"><span data-stu-id="92a4f-165">Don’t: Lead with secondary content or metadata</span></span>

<span data-ttu-id="92a4f-166">Al igual que una aplicación web estándar, la navegación por pestañas debe avanzar en un orden que ayude a dar sentido a las características principales de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="92a4f-166">Like a standard web app, tab navigation should progress in an order that helps make sense of your app’s primary features.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="Ejemplo de procedimiento recomendado de una aplicación personal." border="false":::

### <a name="tab-hierarchy"></a><span data-ttu-id="92a4f-168">Jerarquía de tabulaciones</span><span class="sxs-lookup"><span data-stu-id="92a4f-168">Tab hierarchy</span></span>

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a><span data-ttu-id="92a4f-169">Hacer: las pestañas deben ser de igual jerarquía y representar páginas clave de la aplicación</span><span class="sxs-lookup"><span data-stu-id="92a4f-169">Do: Tabs should be of equal hierarchy and represent key app pages</span></span>

<span data-ttu-id="92a4f-170">Las pestañas deben clasificar las características y el contenido principales de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="92a4f-170">Your tabs should categorize your app’s primary features and content.</span></span> <span data-ttu-id="92a4f-171">Con el tamaño dinámico, el contenido de la derecha puede truncarse o quedar fuera de la vista.</span><span class="sxs-lookup"><span data-stu-id="92a4f-171">With responsive sizing, content on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="En el ejemplo se muestran los procedimientos recomendados de la aplicación personal." border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a><span data-ttu-id="92a4f-173">No: incluir diferentes niveles de jerarquía</span><span class="sxs-lookup"><span data-stu-id="92a4f-173">Don't: Include different levels of hierarchy</span></span>

<span data-ttu-id="92a4f-174">El contenido debe avanzar en un orden lógico que ayude a los usuarios a entenderlo.</span><span class="sxs-lookup"><span data-stu-id="92a4f-174">Your content should progress in a logical order that helps users make sense of it.</span></span> <span data-ttu-id="92a4f-175">Si tiene dos pestañas estrechamente relacionadas, considere la posibilidad de combinarlas en una pestaña.</span><span class="sxs-lookup"><span data-stu-id="92a4f-175">If you have two tabs that are closely related, consider combining them into one tab.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="En el ejemplo se muestra un procedimiento recomendado de aplicación personal." border="false":::

### <a name="first-run-experience"></a><span data-ttu-id="92a4f-177">Experiencia de primera ejecución</span><span class="sxs-lookup"><span data-stu-id="92a4f-177">First-run experience</span></span>

#### <a name="do-include-a-first-run-experience"></a><span data-ttu-id="92a4f-178">Do: Include a first-run experience</span><span class="sxs-lookup"><span data-stu-id="92a4f-178">Do: Include a first-run experience</span></span>

<span data-ttu-id="92a4f-179">Debería haber al menos una pantalla de bienvenida la primera vez que uses una aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="92a4f-179">There should be at least a welcome screen the first time you use a personal app.</span></span> <span data-ttu-id="92a4f-180">En el caso de los bots, describa lo que el bot puede hacer y proporcione acciones rápidas, como un botón de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="92a4f-180">For bots, describe what your bot can do and provide quick actions, such as a sign-in button.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="La ilustración muestra un procedimiento recomendado de la aplicación personal." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="Ilustración de los procedimientos recomendados de una aplicación personal." border="false":::

#### <a name="dont-start-with-a-blank-screen"></a><span data-ttu-id="92a4f-183">Don't: Start with a blank screen</span><span class="sxs-lookup"><span data-stu-id="92a4f-183">Don't: Start with a blank screen</span></span>

<span data-ttu-id="92a4f-184">Es posible que los usuarios se confundan si no se muestra nada la primera vez que ejecutan la aplicación.</span><span class="sxs-lookup"><span data-stu-id="92a4f-184">Users might be confused if nothing displays the first time they run your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="La ilustración muestra un procedimiento recomendado de la aplicación personal." border="false":::

### <a name="personalized-content"></a><span data-ttu-id="92a4f-186">Contenido personalizado</span><span class="sxs-lookup"><span data-stu-id="92a4f-186">Personalized content</span></span>

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a><span data-ttu-id="92a4f-187">Hacer: agregar contenido de aplicación relevante para un usuario</span><span class="sxs-lookup"><span data-stu-id="92a4f-187">Do: Aggregate app content relevant to a user</span></span>

<span data-ttu-id="92a4f-188">Tanto si se trata de una pestaña personal como de un bot, muestra contenido relacionado solo con la actividad de un usuario en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="92a4f-188">Whether it's a personal tab or bot, display content related to only a user's activity in your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="El ejemplo proporciona un procedimiento recomendado de aplicación personal." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="En el ejemplo se muestra un procedimiento recomendado de aplicación personal." border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a><span data-ttu-id="92a4f-191">No: mostrar contenido demasiado amplio o no relacionado</span><span class="sxs-lookup"><span data-stu-id="92a4f-191">Don’t: Show unrelated or overly broad content</span></span>

<span data-ttu-id="92a4f-192">En contextos personales, no muestre contenido para equipos de los que un usuario no forma parte.</span><span class="sxs-lookup"><span data-stu-id="92a4f-192">In personal contexts, don’t display content for teams a user isn't part of.</span></span> <span data-ttu-id="92a4f-193">El contenido del bot personal debe centrarse en el individuo, no en un grupo.</span><span class="sxs-lookup"><span data-stu-id="92a4f-193">Personal bot content should focus on the individual—not a group.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="Reveald es un ejemplo de un procedimiento recomendado de aplicación personal." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="Muestra un procedimiento recomendado de aplicación personal." border="false":::

### <a name="complex-app-features"></a><span data-ttu-id="92a4f-196">Características complejas de la aplicación</span><span class="sxs-lookup"><span data-stu-id="92a4f-196">Complex app features</span></span>

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a><span data-ttu-id="92a4f-197">Hacer: permitir que los usuarios accedan a características complejas en un explorador</span><span class="sxs-lookup"><span data-stu-id="92a4f-197">Do: Allow users to access complex features in a browser</span></span>

<span data-ttu-id="92a4f-198">La aplicación debe centrarse en las tareas principales de Teams, pero aún puedes ver la aplicación completa e independiente en un explorador.</span><span class="sxs-lookup"><span data-stu-id="92a4f-198">Your app should focus on core tasks in Teams, but you can still view the full, standalone app in a browser.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="El ejemplo muestra los procedimientos recomendados de la aplicación personal." border="false":::

#### <a name="dont-include-your-entire-app"></a><span data-ttu-id="92a4f-200">No: incluir toda la aplicación</span><span class="sxs-lookup"><span data-stu-id="92a4f-200">Don’t: Include your entire app</span></span>

<span data-ttu-id="92a4f-201">A menos que creaste la aplicación específicamente para Teams, probablemente tienes características que no tienen sentido en una herramienta de colaboración.</span><span class="sxs-lookup"><span data-stu-id="92a4f-201">Unless you created your app specifically for Teams, you probably have features that don’t make sense in a collaboration tool.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="La ilustración proporciona prácticas recomendadas de la aplicación personal." border="false":::

## <a name="manage-a-personal-tab"></a><span data-ttu-id="92a4f-203">Administrar una pestaña personal</span><span class="sxs-lookup"><span data-stu-id="92a4f-203">Manage a personal tab</span></span>

<span data-ttu-id="92a4f-204">En el lado izquierdo de Teams, los usuarios pueden hacer clic con el botón secundario en la aplicación personal para anclar, quitar y configurar otras opciones de aplicación.</span><span class="sxs-lookup"><span data-stu-id="92a4f-204">On the left side of Teams, users can right click the personal app to pin, remove, and configure other app options.</span></span>

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="En el ejemplo se muestran las opciones para administrar una aplicación personal." border="false":::

## <a name="learn-more"></a><span data-ttu-id="92a4f-206">Más información</span><span class="sxs-lookup"><span data-stu-id="92a4f-206">Learn more</span></span>

<span data-ttu-id="92a4f-207">Estas otras directrices de diseño pueden ayudar en función del ámbito de la aplicación personal:</span><span class="sxs-lookup"><span data-stu-id="92a4f-207">These other design guidelines may help depending on the scope of your personal app:</span></span>

* [<span data-ttu-id="92a4f-208">Diseño de la pestaña</span><span class="sxs-lookup"><span data-stu-id="92a4f-208">Designing your tab</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="92a4f-209">Diseño del bot</span><span class="sxs-lookup"><span data-stu-id="92a4f-209">Designing you bot</span></span>](../../bots/design/bots.md)

## <a name="validate-your-design"></a><span data-ttu-id="92a4f-210">Valide su diseño</span><span class="sxs-lookup"><span data-stu-id="92a4f-210">Validate your design</span></span>

<span data-ttu-id="92a4f-211">Si tiene previsto publicar la aplicación en AppSource, debe comprender los problemas de diseño que habitualmente provocan errores en las aplicaciones durante el envío.</span><span class="sxs-lookup"><span data-stu-id="92a4f-211">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="92a4f-212">Comprobar las instrucciones de validación de diseño</span><span class="sxs-lookup"><span data-stu-id="92a4f-212">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)

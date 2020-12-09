---
title: Diseño de la aplicación personal
description: Obtenga información sobre cómo diseñar una aplicación personal de Microsoft Teams y obtener el kit de interfaz de usuario de Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 971071be9f345815f5461646d7970efdf05fd5c4
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605023"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a><span data-ttu-id="2ed3e-103">Diseño de la aplicación personal para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="2ed3e-103">Designing your personal app for Microsoft Teams</span></span>

<span data-ttu-id="2ed3e-104">Una aplicación personal puede ser un bot, un área de trabajo privada o ambos.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-104">A personal app can be a bot, private workspace, or both.</span></span> <span data-ttu-id="2ed3e-105">A veces, funciona como un espacio para crear o ver contenido, otras veces ofrece al usuario una vista de pájaro de todo lo que es cuando la aplicación se ha configurado como una pestaña en varios canales.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-105">Sometimes it functions like a place to create or view content, other times it offers the user a bird’s eye view of everything that’s theirs when the app has been configured as a tab in multiple channels.</span></span>

<span data-ttu-id="2ed3e-106">Para guiar el diseño de la aplicación, la siguiente información describe e ilustra cómo los usuarios pueden agregar, usar y administrar aplicaciones personales en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage personal apps in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="2ed3e-107">Kit de IU de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="2ed3e-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="2ed3e-108">Puede encontrar instrucciones completas para el diseño de aplicaciones personales, incluidos los elementos que puede captar y modificar según sea necesario, en el kit de interfaz de usuario de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-108">You can find comprehensive personal app design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="2ed3e-109">El kit de UI también tiene temas esenciales, como la accesibilidad y el tamaño de respuesta, que no se cubren aquí.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-109">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2ed3e-110">Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="2ed3e-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a><span data-ttu-id="2ed3e-111">Agregar una aplicación personal</span><span class="sxs-lookup"><span data-stu-id="2ed3e-111">Add a personal app</span></span>

<span data-ttu-id="2ed3e-112">Puede Agregar una aplicación personal desde el almacén de Microsoft Teams (AppSource) o desde el flotante de aplicaciones seleccionando el icono **más** en el lado izquierdo de Teams (que se muestra en el ejemplo siguiente).</span><span class="sxs-lookup"><span data-stu-id="2ed3e-112">You can add a personal app from the Teams store (AppSource) or the app flyout by selecting the **More** icon on the left side of Teams (shown in the following example).</span></span>

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="En el ejemplo se muestra cómo agregar una aplicación personal desde el control flotante de la aplicación." border="false":::

## <a name="use-a-personal-app-private-workspace"></a><span data-ttu-id="2ed3e-114">Usar una aplicación personal (área de trabajo privada)</span><span class="sxs-lookup"><span data-stu-id="2ed3e-114">Use a personal app (private workspace)</span></span>

<span data-ttu-id="2ed3e-115">Con un área de trabajo privada, puede ver el contenido de la aplicación que es significativo para usted en una ubicación central sin salir de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-115">With a private workspace, you can view app content that's meaningful to you in a central location without leaving Teams.</span></span>

<span data-ttu-id="2ed3e-116">(Nota de implementación: el área de trabajo privada se basa en la capacidad de la [*pestaña personal*](../../build-your-first-app/build-personal-tab.md) ).</span><span class="sxs-lookup"><span data-stu-id="2ed3e-116">(Implementation note: The private workspace is based on the [*personal tab*](../../build-your-first-app/build-personal-tab.md) capability.)</span></span>

### <a name="anatomy-personal-app-private-workspace"></a><span data-ttu-id="2ed3e-117">Anatomía: aplicación personal (área de trabajo privada)</span><span class="sxs-lookup"><span data-stu-id="2ed3e-117">Anatomy: Personal app (private workspace)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="Ejemplo muestra anatomía de componentes de la pestaña personal." border="false":::

|<span data-ttu-id="2ed3e-119">Counter</span><span class="sxs-lookup"><span data-stu-id="2ed3e-119">Counter</span></span>|<span data-ttu-id="2ed3e-120">Descripción</span><span class="sxs-lookup"><span data-stu-id="2ed3e-120">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="2ed3e-121">A</span><span class="sxs-lookup"><span data-stu-id="2ed3e-121">A</span></span>|<span data-ttu-id="2ed3e-122">**Atribución de aplicaciones**: el logotipo y el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-122">**App attribution**: Your app logo and name.</span></span>|
|<span data-ttu-id="2ed3e-123">B</span><span class="sxs-lookup"><span data-stu-id="2ed3e-123">B</span></span>|<span data-ttu-id="2ed3e-124">**Pestañas**: proporciona navegación para su aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-124">**Tabs**: Provides navigation for your personal app.</span></span> <span data-ttu-id="2ed3e-125">Por ejemplo, incluya una ficha **acerca de** o **ayuda** .</span><span class="sxs-lookup"><span data-stu-id="2ed3e-125">For example, include an **About** or **Help** tab.</span></span>|
|<span data-ttu-id="2ed3e-126">C</span><span class="sxs-lookup"><span data-stu-id="2ed3e-126">C</span></span>|<span data-ttu-id="2ed3e-127">**Vista emergente**: inserta el contenido de la aplicación desde una ventana primaria en una ventana secundaria independiente.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-127">**Popout view**: Pushes your app content from a parent window to a standalone child window.</span></span>|
|<span data-ttu-id="2ed3e-128">D</span><span class="sxs-lookup"><span data-stu-id="2ed3e-128">D</span></span>|<span data-ttu-id="2ed3e-129">**Menú más**: incluye información adicional de la aplicación y opciones.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-129">**More menu**: Includes additional app information and options.</span></span> <span data-ttu-id="2ed3e-130">(También puede hacer que la **configuración** sea una pestaña.)</span><span class="sxs-lookup"><span data-stu-id="2ed3e-130">(You could alternatively make **Settings** a tab.)</span></span>|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="Ejemplo muestra anatomía estructural de la pestaña personal." border="false":::

|<span data-ttu-id="2ed3e-132">Counter</span><span class="sxs-lookup"><span data-stu-id="2ed3e-132">Counter</span></span>|<span data-ttu-id="2ed3e-133">Descripción</span><span class="sxs-lookup"><span data-stu-id="2ed3e-133">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="2ed3e-134">A</span><span class="sxs-lookup"><span data-stu-id="2ed3e-134">A</span></span>|<span data-ttu-id="2ed3e-135">**Pestañas**: proporciona navegación para su aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-135">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="2ed3e-136">1 </span><span class="sxs-lookup"><span data-stu-id="2ed3e-136">1</span></span>|<span data-ttu-id="2ed3e-137">**iframe**: muestra el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-137">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="2ed3e-138">Diseño con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="2ed3e-138">Designing with UI templates</span></span>

<span data-ttu-id="2ed3e-139">Use una de las siguientes plantillas de interfaz de usuario de Microsoft Teams para ayudar a diseñar su pestaña personal:</span><span class="sxs-lookup"><span data-stu-id="2ed3e-139">Use one of the following Teams UI templates to help design your personal tab:</span></span>

* <span data-ttu-id="2ed3e-140">[List](../../concepts/design/design-teams-app-ui-templates.md#list): lists puede mostrar elementos relacionados en un formato que se pueda analizar y permitir que los usuarios realicen acciones en una lista completa o en elementos individuales.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-140">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="2ed3e-141">[Panel de tareas](../../concepts/design/design-teams-app-ui-templates.md#task-board): un panel de tareas, a veces denominado tablero Kanban o carriles de nadar, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o vales.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-141">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="2ed3e-142">[Panel](../../concepts/design/design-teams-app-ui-templates.md#dashboard): un panel es un lienzo que contiene varias tarjetas que proporcionan información general sobre datos o contenido.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-142">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="2ed3e-143">[Formulario](../../concepts/design/design-teams-app-ui-templates.md#form): los formularios son para recopilar, validar y enviar entradas de usuario de forma estructurada.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-143">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="2ed3e-144">[Estado vacío](../../concepts/design/design-teams-app-ui-templates.md#empty-state): la plantilla de estado vacía se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error, etc.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-144">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="2ed3e-145">Panel de [navegación izquierdo](../../concepts/design/design-teams-app-ui-templates.md#left-nav): la plantilla de navegación izquierda puede servir de ayuda si la pestaña requiere la navegación.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-145">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="2ed3e-146">En general, debe mantener al mínimo la navegación por tabulaciones.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-146">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-personal-app-bot"></a><span data-ttu-id="2ed3e-147">Usar una aplicación personal (bot)</span><span class="sxs-lookup"><span data-stu-id="2ed3e-147">Use a personal app (bot)</span></span>

<span data-ttu-id="2ed3e-148">Las aplicaciones personales pueden incluir un bot para las conversaciones de uno en uno y las notificaciones privadas (por ejemplo, cuando un compañero publica un Comentario en la mesa de mesas).</span><span class="sxs-lookup"><span data-stu-id="2ed3e-148">Personal apps can include a bot for one-on-one conversations and private notifications (for instance, when a colleague posts a comment on your artboard).</span></span> <span data-ttu-id="2ed3e-149">El bot está disponible en la ficha que especifique.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-149">The bot is available in a tab you specify.</span></span>

### <a name="anatomy-personal-app-bot"></a><span data-ttu-id="2ed3e-150">Anatomía: aplicación personal (bot)</span><span class="sxs-lookup"><span data-stu-id="2ed3e-150">Anatomy: Personal app (bot)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="Ejemplo que muestra la anatomía del componente de bot personal." border="false":::

|<span data-ttu-id="2ed3e-152">Counter</span><span class="sxs-lookup"><span data-stu-id="2ed3e-152">Counter</span></span>|<span data-ttu-id="2ed3e-153">Descripción</span><span class="sxs-lookup"><span data-stu-id="2ed3e-153">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="2ed3e-154">A</span><span class="sxs-lookup"><span data-stu-id="2ed3e-154">A</span></span>|<span data-ttu-id="2ed3e-155">**Ficha bot**: por ejemplo, incluye una ficha **chat** para tener acceso a conversaciones y notificaciones de bot.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-155">**Bot tab**: For example, include a **Chat** tab to access bot conversations and notifications.</span></span>|
|<span data-ttu-id="2ed3e-156">B</span><span class="sxs-lookup"><span data-stu-id="2ed3e-156">B</span></span>|<span data-ttu-id="2ed3e-157">**Mensaje de bot**: los bots suelen enviar mensajes y notificaciones en forma de una tarjeta (como una tarjeta adaptable).</span><span class="sxs-lookup"><span data-stu-id="2ed3e-157">**Bot message**: Bots often send messages and notifications in the form of a card (such as an Adaptive Card).</span></span>|
|<span data-ttu-id="2ed3e-158">C</span><span class="sxs-lookup"><span data-stu-id="2ed3e-158">C</span></span>|<span data-ttu-id="2ed3e-159">**Cuadro de redacción**: campo de entrada para enviar mensajes al bot.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-159">**Compose box**: Input field for sending messages to the bot.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="2ed3e-160">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="2ed3e-160">Best practices</span></span>

### <a name="tab-priority"></a><span data-ttu-id="2ed3e-161">Prioridad de la pestaña</span><span class="sxs-lookup"><span data-stu-id="2ed3e-161">Tab priority</span></span>

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a><span data-ttu-id="2ed3e-162">Do: mostrar el contenido más relevante en la primera pestaña</span><span class="sxs-lookup"><span data-stu-id="2ed3e-162">Do: Show the most relevant content in the first tab</span></span>

<span data-ttu-id="2ed3e-163">Con el tamaño de capacidad de respuesta, las pestañas de la derecha se truncan o desaesn.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-163">With responsive sizing, tabs on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a><span data-ttu-id="2ed3e-165">No: lidere con contenido o metadatos secundarios</span><span class="sxs-lookup"><span data-stu-id="2ed3e-165">Don’t: Lead with secondary content or metadata</span></span>

<span data-ttu-id="2ed3e-166">Al igual que una aplicación web estándar, la navegación por pestaña debe progresar en un orden que ayude a comprender las características principales de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-166">Like a standard web app, tab navigation should progress in an order that helps make sense of your app’s primary features.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

### <a name="tab-hierarchy"></a><span data-ttu-id="2ed3e-168">Jerarquía de pestañas</span><span class="sxs-lookup"><span data-stu-id="2ed3e-168">Tab hierarchy</span></span>

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a><span data-ttu-id="2ed3e-169">Do: las pestañas deben ser de la misma jerarquía y representan páginas de aplicaciones clave</span><span class="sxs-lookup"><span data-stu-id="2ed3e-169">Do: Tabs should be of equal hierarchy and represent key app pages</span></span>

<span data-ttu-id="2ed3e-170">Las pestañas deben categorizar el contenido y las características principales de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-170">Your tabs should categorize your app’s primary features and content.</span></span> <span data-ttu-id="2ed3e-171">Con el tamaño de capacidad de respuesta, el contenido de la derecha puede truncarse o quedar fuera de la vista.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-171">With responsive sizing, content on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a><span data-ttu-id="2ed3e-173">No: incluir distintos niveles de jerarquía</span><span class="sxs-lookup"><span data-stu-id="2ed3e-173">Don't: Include different levels of hierarchy</span></span>

<span data-ttu-id="2ed3e-174">El contenido debe progresar en un orden lógico que ayude a los usuarios a tener sentido.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-174">Your content should progress in a logical order that helps users make sense of it.</span></span> <span data-ttu-id="2ed3e-175">Si tiene dos pestañas estrechamente relacionadas, considere la posibilidad de combinarlas en una pestaña.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-175">If you have two tabs that are closely related, consider combining them into one tab.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

### <a name="first-run-experience"></a><span data-ttu-id="2ed3e-177">Experiencia de primera ejecución</span><span class="sxs-lookup"><span data-stu-id="2ed3e-177">First-run experience</span></span>

#### <a name="do-include-a-first-run-experience"></a><span data-ttu-id="2ed3e-178">Do: incluir una experiencia de primera ejecución</span><span class="sxs-lookup"><span data-stu-id="2ed3e-178">Do: Include a first-run experience</span></span>

<span data-ttu-id="2ed3e-179">Debe haber al menos una pantalla de bienvenida la primera vez que use una aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-179">There should be at least a welcome screen the first time you use a personal app.</span></span> <span data-ttu-id="2ed3e-180">Para los bots, describa lo que puede hacer el bot y proporcione acciones rápidas, como un botón de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-180">For bots, describe what your bot can do and provide quick actions, such as a sign-in button.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

#### <a name="dont-start-with-a-blank-screen"></a><span data-ttu-id="2ed3e-183">No: empezar con una pantalla en blanco</span><span class="sxs-lookup"><span data-stu-id="2ed3e-183">Don't: Start with a blank screen</span></span>

<span data-ttu-id="2ed3e-184">Los usuarios podrían confundirse si no aparece nada la primera vez que ejecutan la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-184">Users might be confused if nothing displays the first time they run your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

### <a name="personalized-content"></a><span data-ttu-id="2ed3e-186">Contenido personalizado</span><span class="sxs-lookup"><span data-stu-id="2ed3e-186">Personalized content</span></span>

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a><span data-ttu-id="2ed3e-187">Hacer: agregar contenido de aplicaciones relevante para un usuario</span><span class="sxs-lookup"><span data-stu-id="2ed3e-187">Do: Aggregate app content relevant to a user</span></span>

<span data-ttu-id="2ed3e-188">Ya sea una pestaña personal o un bot, mostrar contenido relacionado solo con la actividad del usuario en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-188">Whether it's a personal tab or bot, display content related to only a user's activity in your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a><span data-ttu-id="2ed3e-191">No: mostrar contenido no relacionado o demasiado amplio</span><span class="sxs-lookup"><span data-stu-id="2ed3e-191">Don’t: Show unrelated or overly broad content</span></span>

<span data-ttu-id="2ed3e-192">En los contextos personales, no se muestra el contenido de los equipos de los que no forma parte el usuario.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-192">In personal contexts, don’t display content for teams a user isn't part of.</span></span> <span data-ttu-id="2ed3e-193">El contenido del bot personal debe centrarse en el individuo (no en un grupo).</span><span class="sxs-lookup"><span data-stu-id="2ed3e-193">Personal bot content should focus on the individual—not a group.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

### <a name="complex-app-features"></a><span data-ttu-id="2ed3e-196">Características complejas de la aplicación</span><span class="sxs-lookup"><span data-stu-id="2ed3e-196">Complex app features</span></span>

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a><span data-ttu-id="2ed3e-197">Do: permitir a los usuarios el acceso a características complejas en un explorador</span><span class="sxs-lookup"><span data-stu-id="2ed3e-197">Do: Allow users to access complex features in a browser</span></span>

<span data-ttu-id="2ed3e-198">La aplicación debe centrarse en las tareas principales de Microsoft Teams, pero todavía puede ver la aplicación independiente completa en un explorador.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-198">Your app should focus on core tasks in Teams, but you can still view the full, standalone app in a browser.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

#### <a name="dont-include-your-entire-app"></a><span data-ttu-id="2ed3e-200">No: incluir toda la aplicación</span><span class="sxs-lookup"><span data-stu-id="2ed3e-200">Don’t: Include your entire app</span></span>

<span data-ttu-id="2ed3e-201">A menos que haya creado la aplicación específicamente para Teams, probablemente tiene características que no tienen sentido en una herramienta de colaboración.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-201">Unless you created your app specifically for Teams, you probably have features that don’t make sense in a collaboration tool.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

## <a name="manage-a-personal-tab"></a><span data-ttu-id="2ed3e-203">Administrar una pestaña personal</span><span class="sxs-lookup"><span data-stu-id="2ed3e-203">Manage a personal tab</span></span>

<span data-ttu-id="2ed3e-204">En la parte izquierda de Microsoft Teams, los usuarios pueden hacer clic con el botón derecho en la aplicación personal para anclar, quitar y configurar otras opciones de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-204">On the left side of Teams, users can right click the personal app to pin, remove, and configure other app options.</span></span>

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="Ejemplo muestra opciones para administrar una aplicación personal." border="false":::

## <a name="learn-more"></a><span data-ttu-id="2ed3e-206">Más información</span><span class="sxs-lookup"><span data-stu-id="2ed3e-206">Learn more</span></span>

<span data-ttu-id="2ed3e-207">Estas otras instrucciones de diseño pueden ayudarle en función del ámbito de su aplicación personal:</span><span class="sxs-lookup"><span data-stu-id="2ed3e-207">These other design guidelines may help depending on the scope of your personal app:</span></span>

* [<span data-ttu-id="2ed3e-208">Diseño de la pestaña</span><span class="sxs-lookup"><span data-stu-id="2ed3e-208">Designing your tab</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="2ed3e-209">Diseño de bot</span><span class="sxs-lookup"><span data-stu-id="2ed3e-209">Designing you bot</span></span>](../../bots/design/bots.md)

## <a name="validate-your-design"></a><span data-ttu-id="2ed3e-210">Validar el diseño</span><span class="sxs-lookup"><span data-stu-id="2ed3e-210">Validate your design</span></span>

<span data-ttu-id="2ed3e-211">Si planea publicar la aplicación en AppSource, debe comprender los problemas de diseño que suelen hacer que las aplicaciones fallen durante el envío.</span><span class="sxs-lookup"><span data-stu-id="2ed3e-211">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2ed3e-212">Comprobar las instrucciones de validación del diseño</span><span class="sxs-lookup"><span data-stu-id="2ed3e-212">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)

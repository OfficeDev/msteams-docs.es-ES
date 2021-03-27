---
title: Aplicaciones en reuniones de Teams
author: laujan
description: información general sobre las aplicaciones en reuniones de Teams basadas en el rol de participante y usuario
ms.topic: overview
ms.author: lajanuar
keywords: API de roles de participantes de reuniones de aplicaciones de teams
ms.openlocfilehash: ac4e270090dd89d370d37de88b8cba552b77a5cb
ms.sourcegitcommit: 3727fc58e84b6f1752612884c2e0b25e207fb56e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/26/2021
ms.locfileid: "51382341"
---
# <a name="apps-in-teams-meetings"></a><span data-ttu-id="fc1ee-104">Aplicaciones en reuniones de Teams</span><span class="sxs-lookup"><span data-stu-id="fc1ee-104">Apps in Teams meetings</span></span>

<span data-ttu-id="fc1ee-105">Las reuniones permiten la colaboración, la asociación, la comunicación informada y los comentarios compartidos en un foro inclusivo y activo.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-105">Meetings enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="fc1ee-106">La aplicación de reunión puede ofrecer una experiencia de usuario para cada fase del ciclo de vida de la reunión, incluida la experiencia de la aplicación previa, en la reunión y posterior a la reunión, según el estado del asistente.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-106">The meeting app can deliver a user experience for each stage of the meeting lifecycle including pre-meeting, in-meeting and post-meeting app experience, depending on the attendee's status.</span></span>

<span data-ttu-id="fc1ee-107">Los usuarios finales de Teams pueden acceder a las aplicaciones durante las reuniones mediante la galería de pestañas, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fc1ee-107">Teams end-users can access apps during meetings using the tab gallery, for example:</span></span>

* <span data-ttu-id="fc1ee-108">Preescalo de un panel de Kanban</span><span class="sxs-lookup"><span data-stu-id="fc1ee-108">Pre-stage a Kanban board</span></span>
* <span data-ttu-id="fc1ee-109">Iniciar un cuadro de diálogo de acción en la reunión</span><span class="sxs-lookup"><span data-stu-id="fc1ee-109">Launch an in-meeting actionable dialog</span></span>
* <span data-ttu-id="fc1ee-110">Crear un sondeo posterior a la reunión</span><span class="sxs-lookup"><span data-stu-id="fc1ee-110">Create a post-meeting poll</span></span>

<span data-ttu-id="fc1ee-111">La extensibilidad de la aplicación de reunión de Teams se basa en los siguientes conceptos:</span><span class="sxs-lookup"><span data-stu-id="fc1ee-111">Teams’ meeting app extensibility is based on the following concepts:</span></span>

<span data-ttu-id="fc1ee-112">✔ ciclo de vida de la reunión tiene fases como antes, durante y después del período de tiempo de la reunión.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-112">✔ Meeting lifecycle has stages such as before, during, and after meeting time frame.</span></span>  
<span data-ttu-id="fc1ee-113">✔ roles de participante en una reunión, como organizador de la reunión, moderador o asistente.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-113">✔ Participant roles in a meeting such as meeting organizer, presenter, or attendee.</span></span>  
<span data-ttu-id="fc1ee-114">✔ usuarios en una reunión, como el usuario de Teams en el inquilino, invitado, federado o anónimo.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-114">✔ User types in a meeting such as in-tenant, guest, federated, or anonymous Teams user.</span></span>

<span data-ttu-id="fc1ee-115">En este artículo se describe información sobre el ciclo de vida de la reunión y cómo integrar pestañas, bots y extensiones de mensajería en la reunión.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-115">This article covers information about the meeting lifecycle and how to integrate tabs, bots, and messaging extensions in your meeting.</span></span> <span data-ttu-id="fc1ee-116">También permite identificar roles de participantes y también usar diferentes tipos de usuario para realizar tareas.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-116">It also enables you to identify participant roles and also use different user types to perform tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="fc1ee-117">Para trabajar con las características de extensibilidad de la aplicación de reunión, debe tener los permisos adecuados.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-117">To work with the meeting app extensibility features, you must have the appropriate permissions.</span></span>

### <a name="meeting-lifecycle"></a><span data-ttu-id="fc1ee-118">Ciclo de vida de la reunión</span><span class="sxs-lookup"><span data-stu-id="fc1ee-118">Meeting lifecycle</span></span>

<span data-ttu-id="fc1ee-119">El ciclo de vida de la reunión consiste en la experiencia de la aplicación previa a la reunión, en la reunión y posterior a la reunión.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-119">Meeting lifecycle consists of pre-meeting, in-meeting, and post-meeting app experience.</span></span> <span data-ttu-id="fc1ee-120">Puede integrar pestañas, bots y extensiones de mensajería en cada fase del ciclo de vida de la reunión.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-120">You can integrate tabs, bots, and messaging extensions in each stage of the meeting lifecycle.</span></span>

## <a name="integrate-tabs-into-the-meeting-lifecycle"></a><span data-ttu-id="fc1ee-121">Integrar pestañas en el ciclo de vida de la reunión</span><span class="sxs-lookup"><span data-stu-id="fc1ee-121">Integrate tabs into the meeting lifecycle</span></span>

<span data-ttu-id="fc1ee-122">Las pestañas permiten a los miembros del equipo tener acceso a servicios y contenido en un espacio específico dentro de un canal o chat.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-122">Tabs allow team members to access services and content in a specific space within a channel or chat.</span></span> <span data-ttu-id="fc1ee-123">Esto permite al equipo trabajar directamente con pestañas y tener conversaciones sobre las herramientas y los datos disponibles en las pestañas.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-123">This lets the team work directly with tabs and have conversations about the tools and data available within tabs.</span></span> <span data-ttu-id="fc1ee-124">En la reunión de Teams, los usuarios pueden agregar una pestaña seleccionando más</span><span class="sxs-lookup"><span data-stu-id="fc1ee-124">In Teams meeting, users can add a tab by selecting plus</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="fc1ee-125">, y elegir la aplicación que quieren instalar como pestaña.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-125">, and choosing the app that they want to install as a tab.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fc1ee-126">Si has integrado una pestaña con la reunión, la aplicación debe seguir el flujo de autenticación de inicio de sesión único [(SSO)](../tabs/how-to/authentication/auth-aad-sso.md) de Teams para las pestañas.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-126">If you have integrated a tab with your meeting, then your app must follow the Teams [single sign-on (SSO) authentication flow](../tabs/how-to/authentication/auth-aad-sso.md) for tabs.</span></span>

> [!NOTE]
> * <span data-ttu-id="fc1ee-127">Los clientes móviles solo admiten pestañas en fases de reunión previas y posteriores.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-127">Mobile clients support tabs only in pre and post meeting stages.</span></span> <span data-ttu-id="fc1ee-128">Las experiencias en la reunión que son el cuadro de diálogo y el panel en la reunión actualmente no están disponibles en dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-128">The in-meeting experiences that is in-meeting dialog and panel are currently not available on mobile.</span></span>
> * <span data-ttu-id="fc1ee-129">Las aplicaciones solo se admiten en reuniones privadas programadas.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-129">Apps are supported only in private scheduled meetings.</span></span>

### <a name="pre-meeting-app-experience"></a><span data-ttu-id="fc1ee-130">Experiencia de la aplicación previa a la reunión</span><span class="sxs-lookup"><span data-stu-id="fc1ee-130">Pre-meeting app experience</span></span>

<span data-ttu-id="fc1ee-131">**Experiencia previa a la reunión:**</span><span class="sxs-lookup"><span data-stu-id="fc1ee-131">**Pre-meeting experience:**</span></span>

![experiencia previa a la reunión](../assets/images/apps-in-meetings/PreMeeting.png)

<span data-ttu-id="fc1ee-133">**Pestaña Antes de la reunión:**</span><span class="sxs-lookup"><span data-stu-id="fc1ee-133">**Pre-meeting tab:**</span></span>

![vista de pestaña previa a la reunión](../assets/images/apps-in-meetings/PreMeetingTab.png)

<span data-ttu-id="fc1ee-135">✔ usuarios con permisos son usuarios que pueden agregar aplicaciones a una reunión durante diferentes etapas del ciclo de vida de la reunión.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-135">✔ Permissioned users are users who can add apps to a meeting during different stages of the meeting lifecycle.</span></span> <span data-ttu-id="fc1ee-136">Estos usuarios pueden agregar aplicaciones a una reunión a través de la galería de pestañas de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="fc1ee-136">These users can add apps to a meeting through the tab gallery in two ways:</span></span>

   * <span data-ttu-id="fc1ee-137">Mediante la **pestaña Detalles** del formulario de programación de Teams.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-137">Using the **Details** tab on the Teams scheduling form.</span></span>

   * <span data-ttu-id="fc1ee-138">Uso de la **pestaña Chat de** reunión en una reunión existente.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-138">Using the meeting **Chat** tab in an existing meeting.</span></span>

<span data-ttu-id="fc1ee-139">✔ las aplicaciones tab son **accesibles** en las páginas detalles de reuniones y **chats** con un botón más ➕ sesión.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-139">✔ Tab apps are accessible in meetings **Details** and **Chats** pages using a plus ➕ button.</span></span>

<span data-ttu-id="fc1ee-140">✔ diseño de tabulación debe estar en un estado organizado si hay más de diez sondeos o encuestas.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-140">✔ Tab layout must be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="in-meeting-app-experience"></a><span data-ttu-id="fc1ee-141">Experiencia de la aplicación en la reunión</span><span class="sxs-lookup"><span data-stu-id="fc1ee-141">In-meeting app experience</span></span>

<span data-ttu-id="fc1ee-142">✔ las aplicaciones de reunión se hospedan en la barra superior superior de la ventana de chat y como experiencia de pestaña en la reunión mediante la pestaña en la reunión. Cuando los usuarios agregan una pestaña a una reunión a través de la galería de pestañas, se muestran las aplicaciones que se **encuentran durante las experiencias** de reunión.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-142">✔ Meeting apps are hosted in the top upper bar of the chat window and as in-meeting tab experience using the in-meeting tab. When users add a tab to a meeting through the tab gallery, apps that are **during meeting** experiences are shown.</span></span>

<span data-ttu-id="fc1ee-143">✔ usuarios con permisos pueden agregar aplicaciones mientras están en la reunión.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-143">✔ Permissioned users can add apps while in the meeting.</span></span>

<span data-ttu-id="fc1ee-144">✔ Cuando se carga en el contexto de una reunión, las aplicaciones pueden aprovechar el SDK de cliente de Teams para obtener acceso a , y representar `meetingId` `userMri` `frameContext` adecuadamente la experiencia.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-144">✔ When loaded in the context of a meeting, apps can leverage the Teams Client SDK to access the `meetingId`, `userMri`, and `frameContext` to appropriately render the experience.</span></span>

<span data-ttu-id="fc1ee-145">✔ exportar un resultado de una encuesta o sondeo notifica a los usuarios que los resultados se descargaron correctamente.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-145">✔ Exporting a result of a survey or poll notifies the users that the results successfully downloaded.</span></span>

<span data-ttu-id="fc1ee-146">✔ Una aplicación está visible en una reunión de Teams en el panel lateral o en el cuadro de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-146">✔ An app is visible in a Teams meeting in the side panel or the in-meeting dialog box.</span></span> <span data-ttu-id="fc1ee-147">Use el cuadro de diálogo en la reunión para mostrar el contenido que se puede usar para los participantes de la reunión.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-147">Use the in-meeting dialog to showcase actionable content for meeting participants.</span></span> <span data-ttu-id="fc1ee-148">*Consulta* [Crear aplicaciones para reuniones de Teams](create-apps-for-teams-meetings.md).</span><span class="sxs-lookup"><span data-stu-id="fc1ee-148">*See* [Create Apps for Teams meetings](create-apps-for-teams-meetings.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="fc1ee-149">El manifiesto de la aplicación especifica que la pestaña está optimizada para [el panel lateral,](create-apps-for-teams-meetings.md#during-a-meeting)que es donde se muestra.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-149">Your app manifest specifies that your tab is [optimized for side panel](create-apps-for-teams-meetings.md#during-a-meeting), that is where it is displayed.</span></span> <span data-ttu-id="fc1ee-150">También puede formar parte de una experiencia de bandeja de uso compartido, sujeto a las directrices de diseño especificadas.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-150">It can also be part of a share-tray experience, subject to specified design guidelines.</span></span>

<span data-ttu-id="fc1ee-151">Las siguientes imágenes muestran la aplicación como un cuadro de diálogo en la reunión y como un panel lateral independiente:</span><span class="sxs-lookup"><span data-stu-id="fc1ee-151">The following images display the app as an in-meeting dialog box and as a separate side panel:</span></span>

![Experiencia en la reunión](../assets/images/apps-in-meetings/in-meeting-experience.png)

![Vista de cuadro de diálogo en la reunión](../assets/images/apps-in-meetings/in-meeting-dialog.png)

#### <a name="in-meeting-actionable-dialog-for-users"></a><span data-ttu-id="fc1ee-154">Cuadro de diálogo que puede actuar en la reunión para los usuarios</span><span class="sxs-lookup"><span data-stu-id="fc1ee-154">In-meeting actionable dialog for users</span></span>

![Vista de cuadro de diálogo](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a><span data-ttu-id="fc1ee-156">Experiencia de aplicación posterior a la reunión</span><span class="sxs-lookup"><span data-stu-id="fc1ee-156">Post-meeting app experience</span></span>

![Vista posterior a la reunión](../assets/images/apps-in-meetings/PostMeeting.png)

<span data-ttu-id="fc1ee-158">✔ El escenario de la aplicación posterior a la reunión es similar a la experiencia actual posterior a la reunión con la ventaja añadida de tener pestañas que existen en la superficie.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-158">✔ The post-meeting app scenario is similar to the current post-meeting experience with the added benefit of having tabs that exist within the surface.</span></span>

<span data-ttu-id="fc1ee-159">✔ usuarios con permiso pueden agregar aplicaciones desde la  galería de pestañas a una reunión mediante la pestaña Detalles del formulario de programación de Teams y la pestaña **Chat** de reunión en una reunión existente.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-159">✔ Permissioned users can add apps from the tab gallery to a meeting using the **Details** tab on the Teams scheduling form and the meeting **Chat** tab in an existing meeting.</span></span>

<span data-ttu-id="fc1ee-160">✔ diseño de tabulación debe organizarse cuando haya más de diez sondeos o encuestas.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-160">✔  Tab layout must be organized when there are more than ten polls or surveys.</span></span>

### <a name="integrate-bots-into-the-meeting-lifecycle"></a><span data-ttu-id="fc1ee-161">Integrar bots en el ciclo de vida de la reunión</span><span class="sxs-lookup"><span data-stu-id="fc1ee-161">Integrate bots into the meeting lifecycle</span></span>

<span data-ttu-id="fc1ee-162">Para la implementación del bot, comience [con la compilación de un bot](../build-your-first-app/build-bot.md) y, a continuación, continúe con crear aplicaciones para reuniones de [Teams.](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)</span><span class="sxs-lookup"><span data-stu-id="fc1ee-162">For bot implementation, start with [build a bot](../build-your-first-app/build-bot.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference).</span></span>

### <a name="integrate-messaging-extensions-into-the-meeting-lifecycle"></a><span data-ttu-id="fc1ee-163">Integrar extensiones de mensajería en el ciclo de vida de la reunión</span><span class="sxs-lookup"><span data-stu-id="fc1ee-163">Integrate messaging extensions into the meeting lifecycle</span></span>

<span data-ttu-id="fc1ee-164">Para la implementación de extensión de mensajería, comience [con la compilación](../messaging-extensions/how-to/create-messaging-extension.md) de una extensión de mensajería y, a continuación, continúe con [crear aplicaciones para reuniones de Teams.](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)</span><span class="sxs-lookup"><span data-stu-id="fc1ee-164">For messaging extension implementation, start with [build a messaging extension](../messaging-extensions/how-to/create-messaging-extension.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference).</span></span>

## <a name="participant-roles-and-user-types-in-a-meeting"></a><span data-ttu-id="fc1ee-165">Roles de participante y tipos de usuario en una reunión</span><span class="sxs-lookup"><span data-stu-id="fc1ee-165">Participant roles and user types in a meeting</span></span>

![Participantes en una reunión](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a><span data-ttu-id="fc1ee-167">Roles de participante</span><span class="sxs-lookup"><span data-stu-id="fc1ee-167">Participant roles</span></span>

<span data-ttu-id="fc1ee-168">La configuración predeterminada de los participantes la determina el administrador de TI de una organización.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-168">Default participant settings are determined by an organization's IT administrator.</span></span> <span data-ttu-id="fc1ee-169">Los siguientes son los roles de participante en una reunión:</span><span class="sxs-lookup"><span data-stu-id="fc1ee-169">The following are the participant roles in a meeting:</span></span>

* <span data-ttu-id="fc1ee-170">**Organizador:** el organizador programa una reunión, establece las opciones de reunión, asigna roles de reunión e inicia la reunión.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-170">**Organizer**: The organizer schedules a meeting, sets the meeting options, assigns meeting roles, and starts the meeting.</span></span> <span data-ttu-id="fc1ee-171">Solo los usuarios con una cuenta M365 con una licencia de Teams pueden ser organizadores y controlar los permisos de los asistentes.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-171">Only users with a M365 account with a Teams license can be organizers and control attendee permissions.</span></span> <span data-ttu-id="fc1ee-172">Un organizador de la reunión puede cambiar la configuración de una reunión específica.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-172">A meeting organizer can change the settings for a specific meeting.</span></span> <span data-ttu-id="fc1ee-173">Los organizadores pueden realizar estos cambios en la página web **Opciones de** reunión.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-173">Organizers can make these changes on the **Meeting options** web page.</span></span>
* <span data-ttu-id="fc1ee-174">**Moderador:** los moderadores tienen las mismas capacidades que el organizador.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-174">**Presenter**: Presenters have the same capabilities as organizer.</span></span> <span data-ttu-id="fc1ee-175">Sin embargo, un moderador no puede quitar un organizador de la sesión ni modificar las opciones de reunión para la sesión.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-175">However, a presenter cannot remove an organizer from the session or modify meeting options for the session.</span></span> <span data-ttu-id="fc1ee-176">De forma predeterminada, los participantes que se unen a una reunión tienen el rol de moderador.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-176">By default, participants joining a meeting have the presenter role.</span></span>
* <span data-ttu-id="fc1ee-177">**Asistente:** un asistente es un usuario al que se ha invitado a asistir a una reunión pero que no está autorizado a actuar como moderador.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-177">**Attendee**: An attendee is a user who has been invited to attend a meeting but who is not authorized to act as a presenter.</span></span> <span data-ttu-id="fc1ee-178">Los asistentes pueden interactuar con otros miembros de la reunión, pero no pueden administrar la configuración de la reunión ni compartir contenido.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-178">Attendees can interact with other meeting members but cannot manage any of the meeting settings or share content.</span></span>

<span data-ttu-id="fc1ee-179">Solo un organizador o moderador puede agregar, quitar o desinstalar aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-179">Only an organizer or presenter can add, remove, or uninstall apps.</span></span> <span data-ttu-id="fc1ee-180">Solo el organizador o moderador puede crear sondeos en una reunión.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-180">Only organizer or presenter can create polls in a meeting.</span></span>

<span data-ttu-id="fc1ee-181">Para obtener más información, vea [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span><span class="sxs-lookup"><span data-stu-id="fc1ee-181">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

<span data-ttu-id="fc1ee-182">Puede acceder a la  **página Opciones de reunión** de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="fc1ee-182">You can access the  **Meeting options** page as follows:</span></span>

* <span data-ttu-id="fc1ee-183">En Teams, vaya al **logotipo del** ![ calendario ](../assets/images/apps-in-meetings/calendar-logo.png) calendario, seleccione una reunión y, a continuación, **Opciones de reunión.**</span><span class="sxs-lookup"><span data-stu-id="fc1ee-183">In Teams, go to **Calendar** ![calendar logo](../assets/images/apps-in-meetings/calendar-logo.png), select a meeting, and then **Meeting options**.</span></span>

* <span data-ttu-id="fc1ee-184">En una invitación a una reunión, seleccione **Opciones de reunión**.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-184">In a meeting invitation, select **Meeting options**.</span></span>

* <span data-ttu-id="fc1ee-185">Durante una reunión, seleccione **Mostrar participantes** ![ mostrar el icono de participantes en los controles ](../assets/images/apps-in-meetings/show-participants.png) de la reunión.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-185">During a meeting, select **Show participants** ![show participants icon](../assets/images/apps-in-meetings/show-participants.png) in the meeting controls.</span></span> <span data-ttu-id="fc1ee-186">A continuación, encima de la lista de participantes, elija **Administrar permisos**.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-186">Then, above the list of participants, choose **Manage permissions**.</span></span>

### <a name="user-types"></a><span data-ttu-id="fc1ee-187">Tipos de usuario</span><span class="sxs-lookup"><span data-stu-id="fc1ee-187">User types</span></span>

> [!NOTE]
> <span data-ttu-id="fc1ee-188">Los usuarios con tipos de usuario específicos asignados pueden unirse a reuniones y asumir uno de los roles de participante que se describen en [roles de participante.](#participant-roles)</span><span class="sxs-lookup"><span data-stu-id="fc1ee-188">Users with specific user types assigned to them can join meetings and assume one of the participant roles described in [participant roles](#participant-roles).</span></span> <span data-ttu-id="fc1ee-189">El tipo de usuario no se incluye en la API **getParticipantRole.**</span><span class="sxs-lookup"><span data-stu-id="fc1ee-189">The user type is not included in the **getParticipantRole** API.</span></span>

<span data-ttu-id="fc1ee-190">Los siguientes tipos de usuario identifican lo que cada usuario puede hacer y a lo que puede acceder:</span><span class="sxs-lookup"><span data-stu-id="fc1ee-190">The following user types identify what each user can do and what they can access:</span></span>

* <span data-ttu-id="fc1ee-191">**In-tenant:** los usuarios del espacio empresarial pertenecen a la organización y tienen credenciales en Azure Active Directory (AAD) para el inquilino.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-191">**In-tenant**: In-tenant users belong to the organization and have credentials in Azure Active Directory (AAD) for the tenant.</span></span> <span data-ttu-id="fc1ee-192">Normalmente son empleados a tiempo completo, in situ o remotos.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-192">They are usually full-time, onsite, or remote employees.</span></span> <span data-ttu-id="fc1ee-193">Un usuario en el espacio empresarial puede ser organizador, moderador o asistente.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-193">An in-tenant user can be an organizer, presenter, or attendee.</span></span>
* <span data-ttu-id="fc1ee-194">**Invitado:** un invitado es un participante de otra organización invitado a tener acceso a Teams u otros recursos en el inquilino de la organización.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-194">**Guest**: A guest is a participant from another organization invited to access Teams or other resources in the organization's tenant.</span></span> <span data-ttu-id="fc1ee-195">Los invitados se agregan al AAD de la organización y tienen las mismas capacidades de Teams que un miembro nativo del equipo con acceso a chats de equipo, reuniones y archivos.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-195">Guests are added to your organization’s AAD and have the same Teams capabilities as a native team member with access to team chats, meetings, and files.</span></span> <span data-ttu-id="fc1ee-196">Un usuario invitado puede ser organizador, moderador o asistente.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-196">A guest user can be an organizer, presenter, or attendee.</span></span> <span data-ttu-id="fc1ee-197">Para obtener más información, vea [acceso de invitado en Teams](/microsoftteams/guest-access).</span><span class="sxs-lookup"><span data-stu-id="fc1ee-197">For more information, see [guest access in Teams](/microsoftteams/guest-access).</span></span>
* <span data-ttu-id="fc1ee-198">**Federado o externo:** un usuario federado es un usuario externo de Teams en otra organización al que se ha invitado a unirse a una reunión.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-198">**Federated or external**: A federated user is an external Teams user in another organization who has been invited to join a meeting.</span></span> <span data-ttu-id="fc1ee-199">Estos usuarios tienen credenciales válidas con socios federados y están autorizados por Teams.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-199">These users have valid credentials with federated partners and are authorized by Teams.</span></span> <span data-ttu-id="fc1ee-200">No tienen acceso a los equipos ni a otros recursos compartidos de la organización.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-200">They do not have access to your teams or other shared resources from your organization.</span></span> <span data-ttu-id="fc1ee-201">El acceso de invitado es una mejor opción para que los usuarios externos tengan acceso a equipos y canales.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-201">Guest access is a better option for external users to have access to teams and channels.</span></span> <span data-ttu-id="fc1ee-202">Para obtener más información, vea [manage external access in Teams](/microsoftteams/manage-external-access).</span><span class="sxs-lookup"><span data-stu-id="fc1ee-202">For more information, see [manage external access in Teams](/microsoftteams/manage-external-access).</span></span>
* <span data-ttu-id="fc1ee-203">**Anónimo:** los usuarios anónimos no tienen una identidad de AAD y no están federados con un inquilino.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-203">**Anonymous**: Anonymous users do not have an AAD identity and are not federated with a tenant.</span></span> <span data-ttu-id="fc1ee-204">El participante anónimo es como un usuario externo, pero su identidad no se proyecta en la reunión.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-204">The anonymous participant is like an external user, but their identity is not projected in the meeting.</span></span> <span data-ttu-id="fc1ee-205">Los usuarios anónimos no pueden acceder a aplicaciones en una ventana de reunión.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-205">Anonymous users are not able to access apps in a meeting window.</span></span> <span data-ttu-id="fc1ee-206">Un usuario anónimo no puede ser un organizador, pero puede ser moderador o asistente.</span><span class="sxs-lookup"><span data-stu-id="fc1ee-206">An anonymous user cannot be an organizer but can be a presenter or attendee.</span></span>

## <a name="see-also"></a><span data-ttu-id="fc1ee-207">Vea también</span><span class="sxs-lookup"><span data-stu-id="fc1ee-207">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fc1ee-208">Tab</span><span class="sxs-lookup"><span data-stu-id="fc1ee-208">Tab</span></span>](../tabs/what-are-tabs.md#how-do-tabs-work)

> [!div class="nextstepaction"]
> [<span data-ttu-id="fc1ee-209">Bot</span><span class="sxs-lookup"><span data-stu-id="fc1ee-209">Bot</span></span>](../bots/what-are-bots.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="fc1ee-210">Extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="fc1ee-210">Messaging extension</span></span>](../messaging-extensions/what-are-messaging-extensions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="fc1ee-211">Diseño de la aplicación</span><span class="sxs-lookup"><span data-stu-id="fc1ee-211">Design your app</span></span>](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="next-steps"></a><span data-ttu-id="fc1ee-212">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fc1ee-212">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fc1ee-213">Crear una aplicación</span><span class="sxs-lookup"><span data-stu-id="fc1ee-213">Build your app</span></span>](create-apps-for-teams-meetings.md)

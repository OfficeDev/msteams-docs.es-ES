---
title: Aplicaciones en reuniones de Teams
author: laujan
description: información general sobre las aplicaciones en reuniones de Teams basadas en el rol de participante y usuario
ms.topic: overview
ms.author: lajanuar
keywords: API de roles de participantes de reuniones de aplicaciones de teams
ms.openlocfilehash: 51fe2e0ebdaa56197bbebd1e5dbcf90698fb1f92
ms.sourcegitcommit: 23ed7edf145df10dcfba15c43978eae9e0d451a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2021
ms.locfileid: "50753556"
---
# <a name="apps-in-teams-meetings"></a><span data-ttu-id="76a20-104">Aplicaciones en reuniones de Teams</span><span class="sxs-lookup"><span data-stu-id="76a20-104">Apps in Teams meetings</span></span>

<span data-ttu-id="76a20-105">Las reuniones son clave para la productividad en Teams.</span><span class="sxs-lookup"><span data-stu-id="76a20-105">Meetings are key to productivity in Teams.</span></span> <span data-ttu-id="76a20-106">Habilitan la colaboración, la asociación, la comunicación informada y los comentarios compartidos en un foro inclusivo y activo.</span><span class="sxs-lookup"><span data-stu-id="76a20-106">They enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="76a20-107">Como desarrollador, puede crear aplicaciones configurables [](../messaging-extensions/what-are-messaging-extensions.md) de [pestaña,](../tabs/what-are-tabs.md#how-do-tabs-work) [bot](../bots/what-are-bots.md)y extensión de mensajes para mejorar y enriquecer una experiencia de reunión de Teams.</span><span class="sxs-lookup"><span data-stu-id="76a20-107">As a developer, you can create [configurable tab](../tabs/what-are-tabs.md#how-do-tabs-work), [bot](../bots/what-are-bots.md), and [message extension](../messaging-extensions/what-are-messaging-extensions.md) applications to enhance and enrich a Teams meeting experience.</span></span> <span data-ttu-id="76a20-108">Los usuarios de reuniones pueden acceder a las aplicaciones, a través de la galería de pestañas, para habilitar escenarios relevantes, como la preconfigurización de un panel de Kanban, el inicio de un cuadro de diálogo de acción en la reunión o la creación de un sondeo posterior a la reunión.</span><span class="sxs-lookup"><span data-stu-id="76a20-108">Meeting users can access apps, via the tab gallery, to enable relevant scenarios such as pre-staging a Kanban board, launching an in-meeting actionable dialog, or creating a post-meeting poll.</span></span> <span data-ttu-id="76a20-109">La aplicación de reunión puede ofrecer una experiencia de usuario para cada fase del ciclo de vida de la reunión en función del estado de los asistentes.</span><span class="sxs-lookup"><span data-stu-id="76a20-109">Your meeting app can deliver a user experience for each stage of the meeting lifecycle based upon attendee status.</span></span>

<span data-ttu-id="76a20-110">La extensibilidad de la aplicación de reuniones de Teams se centra en tres conceptos:</span><span class="sxs-lookup"><span data-stu-id="76a20-110">Teams’ meeting app extensibility centers on three concepts:</span></span>

<span data-ttu-id="76a20-111">✔ ciclo **de vida de la** reunión: antes, durante y después del período de tiempo de reunión.</span><span class="sxs-lookup"><span data-stu-id="76a20-111">✔ **Meeting lifecycle** — before, during, and after meeting time frame.</span></span>  
<span data-ttu-id="76a20-112">✔ de **participante:** organizador de la reunión, moderador o asistente.</span><span class="sxs-lookup"><span data-stu-id="76a20-112">✔ **Participant role** — meeting organizer, presenter, or attendee.</span></span>  
<span data-ttu-id="76a20-113">✔ **usuario:** usuario de Teams en el inquilino, invitado, federado o anónimo.</span><span class="sxs-lookup"><span data-stu-id="76a20-113">✔ **User type** — in-tenant, guest, federated, or anonymous Teams user.</span></span>

<!-- markdownlint-disable MD001 -->
### <a name="meeting-lifecycle-scenarios"></a><span data-ttu-id="76a20-114">Escenarios de ciclo de vida de reuniones</span><span class="sxs-lookup"><span data-stu-id="76a20-114">Meeting lifecycle scenarios</span></span>

## <a name="tabs"></a><span data-ttu-id="76a20-115">Pestañas</span><span class="sxs-lookup"><span data-stu-id="76a20-115">Tabs</span></span>

> [!IMPORTANT]
> <span data-ttu-id="76a20-116">Al igual que con todas las aplicaciones de pestaña, la aplicación tendrá que seguir el flujo de autenticación [de SSO de](../tabs/how-to/authentication/auth-aad-sso.md) Teams para las pestañas.</span><span class="sxs-lookup"><span data-stu-id="76a20-116">As with all tab applications, Your app will need to follow the Teams [SSO authentication flow](../tabs/how-to/authentication/auth-aad-sso.md) for tabs.</span></span>

> [!NOTE]
> * <span data-ttu-id="76a20-117">Los clientes móviles solo admiten pestañas en superficies previas a la reunión y posteriores a la reunión.</span><span class="sxs-lookup"><span data-stu-id="76a20-117">Mobile clients support tabs only in pre-meeting and post-meeting surfaces.</span></span> <span data-ttu-id="76a20-118">Las experiencias en la reunión, como el cuadro de diálogo en la reunión y el panel en móvil, estarán disponibles próximamente.</span><span class="sxs-lookup"><span data-stu-id="76a20-118">The in-meeting experiences, such as in-meeting dialog and panel on mobile will be available soon.</span></span>
> * <span data-ttu-id="76a20-119">Las aplicaciones solo se admiten en reuniones privadas programadas.</span><span class="sxs-lookup"><span data-stu-id="76a20-119">Apps are supported only in private scheduled meetings.</span></span>

### <a name="pre-meeting-app-experience"></a><span data-ttu-id="76a20-120">Experiencia de la aplicación previa a la reunión</span><span class="sxs-lookup"><span data-stu-id="76a20-120">Pre-meeting app experience</span></span>

<span data-ttu-id="76a20-121">**Experiencia previa a la reunión:**</span><span class="sxs-lookup"><span data-stu-id="76a20-121">**Pre-meeting experience:**</span></span>

![experiencia previa a la reunión](../assets/images/apps-in-meetings/PreMeeting.png)

<span data-ttu-id="76a20-123">**Pestaña Antes de la reunión:**</span><span class="sxs-lookup"><span data-stu-id="76a20-123">**Pre-meeting tab:**</span></span>

![vista de pestaña previa a la reunión](../assets/images/apps-in-meetings/PreMeetingTab.png)

<span data-ttu-id="76a20-125">✔ usuarios con permiso pueden agregar aplicaciones a una reunión a través de la galería de pestañas de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="76a20-125">✔ Permissioned users can add apps to a meeting via the tab gallery in two ways:</span></span>

<span data-ttu-id="76a20-126">&emsp;&emsp;&#9679; a través de la **pestaña Detalles** del formulario de programación de Teams.</span><span class="sxs-lookup"><span data-stu-id="76a20-126">&emsp;&emsp;&#9679; Via the **Details** tab on the Teams scheduling form.</span></span>

<span data-ttu-id="76a20-127">&emsp;&emsp;&#9679; a través de la **pestaña Chat de** reunión en una reunión existente.</span><span class="sxs-lookup"><span data-stu-id="76a20-127">&emsp;&emsp;&#9679;  Via the meeting **Chat** tab in an existing meeting.</span></span></br> </br>

<span data-ttu-id="76a20-128">✔ de pestañas son **accesibles** en las páginas detalles y **chats** de reuniones con un icono más (➕) button.|</span><span class="sxs-lookup"><span data-stu-id="76a20-128">✔ Tab apps are accessible in meetings **Details** and **Chats** pages using a plus icon (➕) button.|</span></span>

<span data-ttu-id="76a20-129">✔ diseño de tabulación debe estar en un estado organizado si hay más de diez sondeos o encuestas.</span><span class="sxs-lookup"><span data-stu-id="76a20-129">✔  Tab layout should be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="in-meeting-app-experience"></a><span data-ttu-id="76a20-130">Experiencia de la aplicación en la reunión</span><span class="sxs-lookup"><span data-stu-id="76a20-130">In-meeting app experience</span></span>

<span data-ttu-id="76a20-131">✔ las aplicaciones de reunión se hospedarán en la barra superior superior de la ventana de chat y como experiencia de pestaña en la reunión a través de la pestaña en la reunión. Cuando los usuarios agregan una pestaña a una  reunión a través de la galería de pestañas, se mostrarán las aplicaciones que se encuentran durante las experiencias de reunión.</span><span class="sxs-lookup"><span data-stu-id="76a20-131">✔ Meeting apps will be hosted in the top upper bar of the chat window and as in-meeting tab experience via the in-meeting tab. When users add a tab to a meeting through the tab gallery, apps that are **during meeting** experiences will be surfaced.</span></span>

<span data-ttu-id="76a20-132">✔ usuarios con permisos pueden agregar aplicaciones mientras están en la reunión.</span><span class="sxs-lookup"><span data-stu-id="76a20-132">✔ Permissioned users can add apps while in the meeting.</span></span>

<span data-ttu-id="76a20-133">✔ Cuando se carga en el contexto de una reunión, las aplicaciones podrán aprovechar el SDK de cliente de Teams para obtener acceso a , y representar adecuadamente `meetingId` `userMri` la `frameContext` experiencia.</span><span class="sxs-lookup"><span data-stu-id="76a20-133">✔ When loaded in the context of a meeting, apps will be able to leverage the Teams Client SDK to access the `meetingId`, `userMri`, and `frameContext` to appropriately render the experience.</span></span>

<span data-ttu-id="76a20-134">✔ exportar un resultado de una encuesta o sondeos debe notificar a los usuarios que indiquen "los resultados se descargaron correctamente".</span><span class="sxs-lookup"><span data-stu-id="76a20-134">✔ Exporting a result of a survey or polls should notify the users stating, ‘results successfully downloaded’.</span></span>

<span data-ttu-id="76a20-135">✔ para que una aplicación esté visible en una reunión de Teams en dos áreas:</span><span class="sxs-lookup"><span data-stu-id="76a20-135">✔ For an app to be visible in a Teams meeting in two areas:</span></span>

<span data-ttu-id="76a20-136">&emsp;&emsp;&#9679; panel **lateral**.</span><span class="sxs-lookup"><span data-stu-id="76a20-136">&emsp;&emsp;&#9679; **Side panel**.</span></span> </br>

> [!NOTE]
> <span data-ttu-id="76a20-137">Si el _manifiesto de la_ aplicación especifica que la pestaña está optimizada para el panel [lateral,](create-apps-for-teams-meetings.md#during-a-meeting)es donde se mostrará.</span><span class="sxs-lookup"><span data-stu-id="76a20-137">If your _app manifest_ specifies that your tab is [optimized for side panel](create-apps-for-teams-meetings.md#during-a-meeting), that is where it will be displayed.</span></span> <span data-ttu-id="76a20-138">También puede formar parte de una experiencia de bandeja de uso compartido, sujeto a las directrices de diseño especificadas.</span><span class="sxs-lookup"><span data-stu-id="76a20-138">It can also be part of a share-tray experience, subject to specified design guidelines.</span></span>

<span data-ttu-id="76a20-139">&emsp;&emsp;&#9679; diálogo **En la reunión**.</span><span class="sxs-lookup"><span data-stu-id="76a20-139">&emsp;&emsp;&#9679; **In-meeting dialog**.</span></span> <span data-ttu-id="76a20-140">Use el cuadro de diálogo en la reunión para mostrar el contenido que se puede usar para los participantes de la reunión.</span><span class="sxs-lookup"><span data-stu-id="76a20-140">Use the in-meeting dialog to showcase actionable content for meeting participants.</span></span> <span data-ttu-id="76a20-141">*Consulta* [Crear aplicaciones para reuniones de Teams](create-apps-for-teams-meetings.md).</span><span class="sxs-lookup"><span data-stu-id="76a20-141">*See* [Create Apps for Teams meetings](create-apps-for-teams-meetings.md).</span></span>

<span data-ttu-id="76a20-142">**Experiencia en la reunión:**</span><span class="sxs-lookup"><span data-stu-id="76a20-142">**In-meeting experience:**</span></span>

![experiencia en la reunión](../assets/images/apps-in-meetings/in-meeting-experience.png)

![Vista de cuadro de diálogo en la reunión](../assets/images/apps-in-meetings/in-meeting-dialog.png)

<span data-ttu-id="76a20-145">**Cuadro de diálogo que puede actuar en la reunión para los usuarios:**</span><span class="sxs-lookup"><span data-stu-id="76a20-145">**In-meeting actionable dialog for users:**</span></span>

![vista de cuadro de diálogo](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a><span data-ttu-id="76a20-147">Experiencia de aplicación posterior a la reunión</span><span class="sxs-lookup"><span data-stu-id="76a20-147">Post-meeting app experience</span></span>

<span data-ttu-id="76a20-148">**Experiencia posterior a la reunión:**</span><span class="sxs-lookup"><span data-stu-id="76a20-148">**Post-meeting experience:**</span></span>

![vista posterior a la reunión](../assets/images/apps-in-meetings/PostMeeting.png)

<span data-ttu-id="76a20-150">✔ El escenario de la aplicación posterior a la reunión es similar a la experiencia actual posterior a la reunión con la ventaja añadida de tener pestañas que existen en la superficie.</span><span class="sxs-lookup"><span data-stu-id="76a20-150">✔ The post-meeting app scenario is similar to the current post-meeting experience with the added benefit of having tabs that exist within the surface.</span></span> 

<span data-ttu-id="76a20-151">✔ usuarios con permisos pueden agregar aplicaciones desde la galería  de pestañas a una reunión mediante la pestaña Detalles del formulario de programación de Teams y la pestaña **Chat** de reunión en una reunión existente.</span><span class="sxs-lookup"><span data-stu-id="76a20-151">✔ Permissioned users can add apps from the tab gallery to a meeting via the **Details** tab on the Teams scheduling form and the meeting **Chat** tab in an existing meeting.</span></span>

<span data-ttu-id="76a20-152">✔ diseño de tabulación debe estar en un estado organizado si hay más de diez sondeos o encuestas.</span><span class="sxs-lookup"><span data-stu-id="76a20-152">✔  Tab layout should be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="bots"></a><span data-ttu-id="76a20-153">Bots</span><span class="sxs-lookup"><span data-stu-id="76a20-153">Bots</span></span>

<span data-ttu-id="76a20-154">Para la implementación del bot, comience [con la compilación de un bot](../build-your-first-app/build-bot.md) y, a continuación, continúe con crear aplicaciones para reuniones de [Teams.](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)</span><span class="sxs-lookup"><span data-stu-id="76a20-154">For bot implementation, start with [build a bot](../build-your-first-app/build-bot.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference).</span></span>

### <a name="messaging-extensions"></a><span data-ttu-id="76a20-155">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="76a20-155">Messaging extensions</span></span>

<span data-ttu-id="76a20-156">Para la implementación de extensión de mensajería, comience [con la compilación](../messaging-extensions/how-to/create-messaging-extension.md) de una extensión de mensajería y, a continuación, continúe con [crear aplicaciones para reuniones de Teams.](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)</span><span class="sxs-lookup"><span data-stu-id="76a20-156">For messaging extension implementation, start with [build a messaging extension](../messaging-extensions/how-to/create-messaging-extension.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference).</span></span>

## <a name="participant-roles-and-user-types-in-a-meeting"></a><span data-ttu-id="76a20-157">Roles de participante y tipos de usuario en una reunión</span><span class="sxs-lookup"><span data-stu-id="76a20-157">Participant roles and user types in a meeting</span></span>

![Participantes en una reunión](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a><span data-ttu-id="76a20-159">Roles de participante</span><span class="sxs-lookup"><span data-stu-id="76a20-159">Participant roles</span></span>

<span data-ttu-id="76a20-160">Puedes diseñar la aplicación con autorización específica del participante.</span><span class="sxs-lookup"><span data-stu-id="76a20-160">You can design your app with participant-specific authorization.</span></span> <span data-ttu-id="76a20-161">Por ejemplo, quizás solo un organizador o moderador puede crear un sondeo en reuniones.</span><span class="sxs-lookup"><span data-stu-id="76a20-161">For example, perhaps only an organizer and/or presenter can create a poll in meetings.</span></span> <span data-ttu-id="76a20-162">Aunque la configuración predeterminada de los participantes la determina el administrador de TI de una organización, es posible que un organizador de la reunión quiera cambiar la configuración de una reunión específica.</span><span class="sxs-lookup"><span data-stu-id="76a20-162">Although default participant settings are determined by an organization's IT administrator, a meeting organizer may want to change the settings for a specific meeting.</span></span> <span data-ttu-id="76a20-163">Los organizadores pueden realizar estos cambios en la página web Opciones de reunión.</span><span class="sxs-lookup"><span data-stu-id="76a20-163">Organizers can make these changes on the Meeting options web page.</span></span>

1. <span data-ttu-id="76a20-164">**Organizador**.</span><span class="sxs-lookup"><span data-stu-id="76a20-164">**Organizer**.</span></span> <span data-ttu-id="76a20-165">El organizador programa una reunión, establece las opciones de reunión, asigna roles de reunión e inicia la reunión.</span><span class="sxs-lookup"><span data-stu-id="76a20-165">The organizer schedules a meeting, sets the meeting options, assigns meeting roles, and starts the meeting.</span></span> <span data-ttu-id="76a20-166">Solo los usuarios con una cuenta M365 (que posee una licencia de Teams) pueden ser organizadores y controlar los permisos de los asistentes.</span><span class="sxs-lookup"><span data-stu-id="76a20-166">Only users with a M365 account (possessing a Teams license) can be organizers and control attendee permissions.</span></span>
1. <span data-ttu-id="76a20-167">**Moderador**.</span><span class="sxs-lookup"><span data-stu-id="76a20-167">**Presenter**.</span></span> <span data-ttu-id="76a20-168">Los presentadores tienen casi las mismas capacidades que el organizador; sin embargo, un moderador no puede quitar un organizador de la sesión ni modificar las opciones de reunión para la sesión.</span><span class="sxs-lookup"><span data-stu-id="76a20-168">Presenters have nearly the same capabilities as organizer; however, a presenter cannot remove an organizer from the session or modify meeting options for the session.</span></span> <span data-ttu-id="76a20-169">De forma predeterminada, los participantes que se unen a una reunión tienen el rol de moderador.</span><span class="sxs-lookup"><span data-stu-id="76a20-169">By default, participants joining a meeting have the presenter role.</span></span>
1. <span data-ttu-id="76a20-170">**Attendee**.</span><span class="sxs-lookup"><span data-stu-id="76a20-170">**Attendee**.</span></span> <span data-ttu-id="76a20-171">Un asistente es un usuario al que se ha invitado a asistir a una reunión pero que no está autorizado a actuar como moderador.</span><span class="sxs-lookup"><span data-stu-id="76a20-171">An attendee is a user who has been invited to attend a meeting but who is not authorized to act as a presenter.</span></span> <span data-ttu-id="76a20-172">Los asistentes pueden interactuar con otros miembros de la reunión, pero no pueden administrar la configuración de la reunión ni compartir contenido.</span><span class="sxs-lookup"><span data-stu-id="76a20-172">Attendees can interact with other meeting members but cannot manage any of the meeting settings or share content.</span></span>

<span data-ttu-id="76a20-173">_Ver_ [ **Roles en una reunión de Teams**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="76a20-173">_See_ [**Roles in a Teams meeting**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span></span>

<span data-ttu-id="76a20-174">Puede acceder a la  **página Opciones de reunión** de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="76a20-174">You can access the  **Meeting options** page as follows:</span></span>

<span data-ttu-id="76a20-175">&#11200; En Teams, vaya  al logotipo del ![ calendario ](../assets/images/apps-in-meetings/calendar-logo.png) calendario, seleccione una reunión y, a continuación, **Opciones de reunión.**</span><span class="sxs-lookup"><span data-stu-id="76a20-175">&#11200; In Teams, go to **Calendar** ![calendar logo](../assets/images/apps-in-meetings/calendar-logo.png), select a meeting, and then **Meeting options**.</span></span>

<span data-ttu-id="76a20-176">&#11200; En una invitación a una reunión, seleccione **Opciones de reunión**.</span><span class="sxs-lookup"><span data-stu-id="76a20-176">&#11200; In a meeting invitation, select **Meeting options**.</span></span>

<span data-ttu-id="76a20-177">&#11200; Durante una reunión, seleccione **Mostrar participantes** ![ mostrar el icono de participantes en los controles ](../assets/images/apps-in-meetings/show-participants.png) de la reunión.</span><span class="sxs-lookup"><span data-stu-id="76a20-177">&#11200; During a meeting, select **Show participants** ![show participants icon](../assets/images/apps-in-meetings/show-participants.png) in the meeting controls.</span></span> <span data-ttu-id="76a20-178">A continuación, encima de la lista de participantes, elija **Administrar permisos**.</span><span class="sxs-lookup"><span data-stu-id="76a20-178">Then, above the list of participants, choose **Manage permissions**.</span></span>

### <a name="user-types"></a><span data-ttu-id="76a20-179">Tipos de usuario</span><span class="sxs-lookup"><span data-stu-id="76a20-179">User types</span></span>

> [!NOTE]
> <span data-ttu-id="76a20-180">Los tipos de usuario pueden unirse a reuniones y asumir uno de los roles de participante descritos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="76a20-180">User types can join meetings and assume one of the participant roles described above.</span></span> <span data-ttu-id="76a20-181">El tipo user no se expone como parte de la API **getParticipantRole.**</span><span class="sxs-lookup"><span data-stu-id="76a20-181">The User type is not exposed as part of the **getParticipantRole** API.</span></span>

1. <span data-ttu-id="76a20-182">**In-tenant**.</span><span class="sxs-lookup"><span data-stu-id="76a20-182">**In-tenant**.</span></span> <span data-ttu-id="76a20-183">Estos usuarios pertenecen a la organización y tienen credenciales en Azure Active Directory para el inquilino.</span><span class="sxs-lookup"><span data-stu-id="76a20-183">These users belong to the organization and have credentials in Azure Active Directory for the tenant.</span></span> <span data-ttu-id="76a20-184">Normalmente son empleados a tiempo completo, in situ o remotos.</span><span class="sxs-lookup"><span data-stu-id="76a20-184">They are usually full-time, onsite or remote employees.</span></span>
1. <span data-ttu-id="76a20-185">**Invitado**.</span><span class="sxs-lookup"><span data-stu-id="76a20-185">**Guest**.</span></span> <span data-ttu-id="76a20-186">Un invitado es un participante de otra organización que ha sido invitado a tener acceso a Teams u otros recursos en el inquilino de la organización.</span><span class="sxs-lookup"><span data-stu-id="76a20-186">A guest is a participant from another organization who has been invited to access Teams or other resources in your organization's tenant.</span></span> <span data-ttu-id="76a20-187">Los invitados se agregan a Active Directory de la organización y pueden tener casi todas las mismas capacidades de Teams que un miembro nativo del equipo con acceso total a chats de equipo, reuniones y archivos.</span><span class="sxs-lookup"><span data-stu-id="76a20-187">Guests are added to your organization’s Active Directory and can be given nearly all the same Teams capabilities as a native team member with full access to team chats, meetings, and files.</span></span> <span data-ttu-id="76a20-188">_Consulta_ [Acceso de invitados en Microsoft Teams](/microsoftteams/guest-access)</span><span class="sxs-lookup"><span data-stu-id="76a20-188">_See_ [Guest access in Microsoft Teams](/microsoftteams/guest-access)</span></span>
1. <span data-ttu-id="76a20-189">**Federado/externo**.</span><span class="sxs-lookup"><span data-stu-id="76a20-189">**Federated/External**.</span></span> <span data-ttu-id="76a20-190">Un usuario federado es un usuario externo de Teams en otra organización al que se ha invitado a unirse a una reunión.</span><span class="sxs-lookup"><span data-stu-id="76a20-190">A federated user is an external Teams user in another organization who has been invited to join a meeting.</span></span> <span data-ttu-id="76a20-191">Dado que estos usuarios tienen credenciales válidas con socios federados, Teams los trata como autenticados, pero no tienen acceso a los equipos u otros recursos compartidos de la organización.</span><span class="sxs-lookup"><span data-stu-id="76a20-191">Since these users have valid credentials with federated partners, they are treated as authenticated by Teams but do not have access to your teams or other shared resources from your organization.</span></span> <span data-ttu-id="76a20-192">Si desea que los usuarios externos tengan acceso a equipos y canales, el acceso de invitado puede ser una mejor opción.</span><span class="sxs-lookup"><span data-stu-id="76a20-192">If you want external users to have access to teams and channels, guest access might be a better option.</span></span> <span data-ttu-id="76a20-193">_Consulta Administrar_ [el acceso externo en Microsoft Teams](/microsoftteams/manage-external-access)</span><span class="sxs-lookup"><span data-stu-id="76a20-193">_See_ [Manage external access in Microsoft Teams](/microsoftteams/manage-external-access)</span></span>
1. <span data-ttu-id="76a20-194">**Anónimo**.</span><span class="sxs-lookup"><span data-stu-id="76a20-194">**Anonymous**.</span></span> <span data-ttu-id="76a20-195">Los usuarios anónimos no tienen una identidad de Active Directory y no están federados con un inquilino.</span><span class="sxs-lookup"><span data-stu-id="76a20-195">Anonymous users do not have an Active Directory identity and are not federated with a tenant.</span></span> <span data-ttu-id="76a20-196">El participante anónimo es como un usuario externo, pero su identidad no se proyecta en la reunión.</span><span class="sxs-lookup"><span data-stu-id="76a20-196">The anonymous participant is like an external user, but their identity is not projected into the meeting.</span></span> <span data-ttu-id="76a20-197">Los usuarios anónimos no podrán acceder a las aplicaciones en una ventana de reunión.</span><span class="sxs-lookup"><span data-stu-id="76a20-197">Anonymous users will not be able to access apps in a meeting window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76a20-198">Siguientes pasos</span><span class="sxs-lookup"><span data-stu-id="76a20-198">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="76a20-199">Diseño de la aplicación</span><span class="sxs-lookup"><span data-stu-id="76a20-199">Design your app</span></span>](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="76a20-200">Crear una aplicación</span><span class="sxs-lookup"><span data-stu-id="76a20-200">Build your app</span></span>](create-apps-for-teams-meetings.md)

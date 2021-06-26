---
title: Habilitar y configurar las aplicaciones para Teams reuniones
author: surbhigupta
description: Habilitar y configurar las aplicaciones para Teams reuniones
ms.topic: conceptual
ms.openlocfilehash: c123cc5cf15a7d0af64e2de16e96a673a2e4435c
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2021
ms.locfileid: "53139973"
---
# <a name="enable-and-configure-your-apps-for-teams-meetings"></a><span data-ttu-id="a7200-103">Habilitar y configurar las aplicaciones para Teams reuniones</span><span class="sxs-lookup"><span data-stu-id="a7200-103">Enable and configure your apps for Teams meetings</span></span>

<span data-ttu-id="a7200-104">Cada equipo tiene una forma diferente de comunicar y colaborar tareas.</span><span class="sxs-lookup"><span data-stu-id="a7200-104">Every team has a different way of communicating and collaborating tasks.</span></span> <span data-ttu-id="a7200-105">Puedes lograr estas distintas tareas personalizando Teams aplicaciones para reuniones.</span><span class="sxs-lookup"><span data-stu-id="a7200-105">You can achieve these different tasks by customizing Teams with apps for meetings.</span></span> <span data-ttu-id="a7200-106">Para personalizar y lograr diferentes tareas, debes habilitar las aplicaciones para reuniones Teams y configurar las aplicaciones para que estén disponibles en el ámbito de la reunión dentro del manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a7200-106">To customize and to achieve different tasks, you must enable your apps for Teams meetings and configure your apps to be available in meeting scope within their app manifest.</span></span>

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="a7200-107">Habilitar la aplicación para Teams reuniones</span><span class="sxs-lookup"><span data-stu-id="a7200-107">Enable your app for Teams meetings</span></span>

<span data-ttu-id="a7200-108">Para habilitar la aplicación para Teams reuniones, debes actualizar el manifiesto de la aplicación y usar las propiedades de contexto para determinar dónde debe aparecer la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a7200-108">To enable your app for Teams meetings, you must update your app manifest and use the context properties to determine where your app must appear.</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="a7200-109">Actualizar el manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="a7200-109">Update your app manifest</span></span>

<span data-ttu-id="a7200-110">Las funcionalidades de la aplicación reuniones se declaran en el manifiesto de la aplicación mediante `configurableTabs` las `scopes` matrices , `context` y.</span><span class="sxs-lookup"><span data-stu-id="a7200-110">The meetings app capabilities are declared in your app manifest using the `configurableTabs`, `scopes`, and `context` arrays.</span></span> <span data-ttu-id="a7200-111">El ámbito define a quién y el contexto define dónde está disponible la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a7200-111">Scope defines to whom and context defines where your app is available.</span></span>

> [!NOTE]
> * <span data-ttu-id="a7200-112">Intente actualizar el manifiesto de la aplicación con el [esquema de manifiesto](../resources/schema/manifest-schema-dev-preview.md).</span><span class="sxs-lookup"><span data-stu-id="a7200-112">Try updating your app manifest with the [manifest schema](../resources/schema/manifest-schema-dev-preview.md).</span></span>
> * <span data-ttu-id="a7200-113">Las aplicaciones de las reuniones requieren ámbito groupchat.</span><span class="sxs-lookup"><span data-stu-id="a7200-113">Apps in meetings require groupchat scope.</span></span> <span data-ttu-id="a7200-114">El ámbito de equipo solo funciona para pestañas en canales.</span><span class="sxs-lookup"><span data-stu-id="a7200-114">The team scope works for tabs in channels only.</span></span>

<span data-ttu-id="a7200-115">El manifiesto de la aplicación debe incluir el siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="a7200-115">The app manifest must include the following code snippet:</span></span>

```json

"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "team",
        "groupchat"
      ],
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```

> [!NOTE]
> <span data-ttu-id="a7200-116">`meetingStage` actualmente solo está disponible en [versión preliminar del](../resources/dev-preview/developer-preview-intro.md) desarrollador.</span><span class="sxs-lookup"><span data-stu-id="a7200-116">`meetingStage` is currently available in [developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

### <a name="context-property"></a><span data-ttu-id="a7200-117">Context (propiedad)</span><span class="sxs-lookup"><span data-stu-id="a7200-117">Context property</span></span>

<span data-ttu-id="a7200-118">La propiedad determina lo que debe mostrarse cuando un usuario invoca una aplicación en una reunión en función del lugar en el que el usuario `context` invoca la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a7200-118">The `context` property determines what must be shown when a user invokes an app in a meeting depending on where the user invokes the app.</span></span> <span data-ttu-id="a7200-119">La pestaña y las propiedades te permiten determinar dónde debe aparecer `context` `scopes` la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a7200-119">The tab `context` and `scopes` properties enable you to determine where your app must appear.</span></span> <span data-ttu-id="a7200-120">Las pestañas del `team` ámbito or pueden tener más de un `groupchat` contexto.</span><span class="sxs-lookup"><span data-stu-id="a7200-120">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="a7200-121">Estos son los valores de la propiedad desde `context` la que puede usar todos o algunos de los valores:</span><span class="sxs-lookup"><span data-stu-id="a7200-121">Following are the values for the `context` property from which you can use all or some of the values:</span></span>

|<span data-ttu-id="a7200-122">Valor</span><span class="sxs-lookup"><span data-stu-id="a7200-122">Value</span></span>|<span data-ttu-id="a7200-123">Descripción</span><span class="sxs-lookup"><span data-stu-id="a7200-123">Description</span></span>|
|---|---|
| <span data-ttu-id="a7200-124">**channelTab**</span><span class="sxs-lookup"><span data-stu-id="a7200-124">**channelTab**</span></span> | <span data-ttu-id="a7200-125">Pestaña en el encabezado de un canal de grupo.</span><span class="sxs-lookup"><span data-stu-id="a7200-125">A tab in the header of a team channel.</span></span> |
| <span data-ttu-id="a7200-126">**privateChatTab**</span><span class="sxs-lookup"><span data-stu-id="a7200-126">**privateChatTab**</span></span> | <span data-ttu-id="a7200-127">Pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios, no en el contexto de un equipo o reunión.</span><span class="sxs-lookup"><span data-stu-id="a7200-127">A tab in the header of a group chat between a set of users, not in the context of a team or meeting.</span></span> |
| <span data-ttu-id="a7200-128">**meetingChatTab**</span><span class="sxs-lookup"><span data-stu-id="a7200-128">**meetingChatTab**</span></span> | <span data-ttu-id="a7200-129">Pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios en el contexto de una reunión programada.</span><span class="sxs-lookup"><span data-stu-id="a7200-129">A tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span> |
| <span data-ttu-id="a7200-130">**meetingDetailsTab**</span><span class="sxs-lookup"><span data-stu-id="a7200-130">**meetingDetailsTab**</span></span> | <span data-ttu-id="a7200-131">Pestaña en el encabezado de la vista de detalles de la reunión del calendario.</span><span class="sxs-lookup"><span data-stu-id="a7200-131">A tab in the header of the meeting details view of the calendar.</span></span> |
| <span data-ttu-id="a7200-132">**meetingSidePanel**</span><span class="sxs-lookup"><span data-stu-id="a7200-132">**meetingSidePanel**</span></span> | <span data-ttu-id="a7200-133">Un panel en la reunión abierto a través de la barra unificada (barra U).</span><span class="sxs-lookup"><span data-stu-id="a7200-133">An in-meeting panel opened through the unified bar (U-bar).</span></span> |
| <span data-ttu-id="a7200-134">**meetingStage**</span><span class="sxs-lookup"><span data-stu-id="a7200-134">**meetingStage**</span></span> | <span data-ttu-id="a7200-135">Una aplicación de meetingSidePanel se puede compartir en la fase de reunión.</span><span class="sxs-lookup"><span data-stu-id="a7200-135">An app from the meetingSidePanel can be shared to the meeting stage.</span></span> |

> [!NOTE]
> <span data-ttu-id="a7200-136">`Context` actualmente no se admite en clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="a7200-136">`Context` property is currently not supported on mobile clients.</span></span>

<span data-ttu-id="a7200-137">Después de habilitar la aplicación para Teams reuniones, debes configurar la aplicación antes de una reunión, durante una reunión y después de una reunión.</span><span class="sxs-lookup"><span data-stu-id="a7200-137">After you enable your app for Teams meetings, you must configure your app before a meeting, during a meeting, and after a meeting.</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="a7200-138">Configurar la aplicación para escenarios de reunión</span><span class="sxs-lookup"><span data-stu-id="a7200-138">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="a7200-139">Para que la aplicación esté visible en la galería de pestañas, debe admitir pestañas configurables y el ámbito de chat de grupo.</span><span class="sxs-lookup"><span data-stu-id="a7200-139">For your app to be visible in the tab gallery, it must support configurable tabs and the group chat scope.</span></span>
> * <span data-ttu-id="a7200-140">Los clientes móviles solo admiten pestañas en fases de reunión previas y posteriores.</span><span class="sxs-lookup"><span data-stu-id="a7200-140">Mobile clients support tabs only in pre and post meeting stages.</span></span>
> * <span data-ttu-id="a7200-141">Las experiencias en la reunión que es el cuadro de diálogo y la pestaña en la reunión actualmente no se admiten en clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="a7200-141">The in-meeting experiences that is in-meeting dialog box and tab is currently not supported on mobile clients.</span></span> <span data-ttu-id="a7200-142">Para obtener más información, consulta [instrucciones para pestañas en el móvil](../tabs/design/tabs-mobile.md) al crear las pestañas para móviles.</span><span class="sxs-lookup"><span data-stu-id="a7200-142">For more information, see [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) while creating your tabs for mobile.</span></span>

<span data-ttu-id="a7200-143">Teams reuniones proporciona una experiencia de colaboración única para su organización.</span><span class="sxs-lookup"><span data-stu-id="a7200-143">Teams meetings provides a unique collaborative experience for your organization.</span></span> <span data-ttu-id="a7200-144">Proporciona la oportunidad de configurar la aplicación para diferentes escenarios de reunión.</span><span class="sxs-lookup"><span data-stu-id="a7200-144">It provides the opportunity to configure your app for different meeting scenarios.</span></span> <span data-ttu-id="a7200-145">Puedes configurar las aplicaciones para mejorar la experiencia de la reunión en función del rol de participante o el tipo de usuario.</span><span class="sxs-lookup"><span data-stu-id="a7200-145">You can configure your apps to enhance the meeting experience based on participant role or user type.</span></span> <span data-ttu-id="a7200-146">Ahora puede identificar qué acciones se pueden realizar en los siguientes escenarios de reunión:</span><span class="sxs-lookup"><span data-stu-id="a7200-146">Now you can identify what actions can be taken in the following meeting scenarios:</span></span>

* [<span data-ttu-id="a7200-147">Antes de una reunión</span><span class="sxs-lookup"><span data-stu-id="a7200-147">Before a meeting</span></span>](#before-a-meeting)
* [<span data-ttu-id="a7200-148">Durante una reunión</span><span class="sxs-lookup"><span data-stu-id="a7200-148">During a meeting</span></span>](#during-a-meeting)
* [<span data-ttu-id="a7200-149">Después de una reunión</span><span class="sxs-lookup"><span data-stu-id="a7200-149">After a meeting</span></span>](#after-a-meeting)

### <a name="before-a-meeting"></a><span data-ttu-id="a7200-150">Antes de una reunión</span><span class="sxs-lookup"><span data-stu-id="a7200-150">Before a meeting</span></span>

<span data-ttu-id="a7200-151">Antes de una reunión, los usuarios pueden agregar pestañas, bots y extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="a7200-151">Before a meeting, users can add tabs, bots, and messaging extensions.</span></span> <span data-ttu-id="a7200-152">Los usuarios con roles de organizador y moderador pueden agregar pestañas a una reunión.</span><span class="sxs-lookup"><span data-stu-id="a7200-152">Users with organizer and presenter roles can add tabs to a meeting.</span></span>

<span data-ttu-id="a7200-153">**Para agregar una pestaña a una reunión**</span><span class="sxs-lookup"><span data-stu-id="a7200-153">**To add a tab to a meeting**</span></span>

1. <span data-ttu-id="a7200-154">En el calendario, seleccione una reunión a la que desee agregar una pestaña.</span><span class="sxs-lookup"><span data-stu-id="a7200-154">In your calendar, select a meeting to which you want to add a tab.</span></span>
1. <span data-ttu-id="a7200-155">Seleccione la **pestaña Detalles** y seleccione</span><span class="sxs-lookup"><span data-stu-id="a7200-155">Select the **Details** tab and select</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="a7200-156">.</span><span class="sxs-lookup"><span data-stu-id="a7200-156">.</span></span>

    ![Experiencia previa a la reunión](../assets/images/apps-in-meetings/PreMeeting.png)

1. <span data-ttu-id="a7200-158">En la galería de pestañas que aparece, selecciona la aplicación que quieres agregar y sigue los pasos según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a7200-158">In the tab gallery that appears, select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="a7200-159">La aplicación se instala como una pestaña.</span><span class="sxs-lookup"><span data-stu-id="a7200-159">The app is installed as a tab.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a7200-160">Actualmente, en la pestaña reuniones, no se admite la obtención de detalles de la reunión y la información de los participantes.</span><span class="sxs-lookup"><span data-stu-id="a7200-160">Currently, in meetings tab, getting meeting details and participant information is not supported.</span></span>

<span data-ttu-id="a7200-161">**Para agregar una extensión de mensajería a una reunión**</span><span class="sxs-lookup"><span data-stu-id="a7200-161">**To add a messaging extension to a meeting**</span></span>

1. <span data-ttu-id="a7200-162">Seleccione los puntos suspensivos &#x25CF;&#x25CF;&#x25CF; ubicados en el área del mensaje de redacción en el chat.</span><span class="sxs-lookup"><span data-stu-id="a7200-162">Select the ellipses &#x25CF;&#x25CF;&#x25CF; located in the compose message area in the chat.</span></span>
1. <span data-ttu-id="a7200-163">Selecciona la aplicación que quieras agregar y sigue los pasos según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a7200-163">Select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="a7200-164">La aplicación se instala como una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="a7200-164">The app is installed as a messaging extension.</span></span>

<span data-ttu-id="a7200-165">**Para agregar un bot a una reunión**</span><span class="sxs-lookup"><span data-stu-id="a7200-165">**To add a bot to a meeting**</span></span>

<span data-ttu-id="a7200-166">En un chat de reunión, escriba la **@** clave y seleccione Obtener **bots**.</span><span class="sxs-lookup"><span data-stu-id="a7200-166">In a meeting chat, enter the **@** key and select **Get bots**.</span></span>

> [!NOTE]
> * <span data-ttu-id="a7200-167">La identidad del usuario debe confirmarse con [tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="a7200-167">The user identity must be confirmed using [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="a7200-168">Después de la autenticación, la aplicación puede recuperar el rol de usuario mediante la `GetParticipant` API.</span><span class="sxs-lookup"><span data-stu-id="a7200-168">After authentication, the app can retrieve the user role using the `GetParticipant` API.</span></span>
> * <span data-ttu-id="a7200-169">En función del rol de usuario, la aplicación tiene la capacidad de proporcionar experiencias específicas del rol.</span><span class="sxs-lookup"><span data-stu-id="a7200-169">Based on the user role, the app has the capability to provide role specific experiences.</span></span> <span data-ttu-id="a7200-170">Por ejemplo, una aplicación de sondeo solo permite a los organizadores y presentadores crear un nuevo sondeo.</span><span class="sxs-lookup"><span data-stu-id="a7200-170">For example, a polling app allows only organizers and presenters to create a new poll.</span></span>
> * <span data-ttu-id="a7200-171">Las asignaciones de roles se pueden cambiar mientras se está en curso una reunión.</span><span class="sxs-lookup"><span data-stu-id="a7200-171">Role assignments can be changed while a meeting is in progress.</span></span> <span data-ttu-id="a7200-172">Para obtener más información, vea [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span><span class="sxs-lookup"><span data-stu-id="a7200-172">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

### <a name="during-a-meeting"></a><span data-ttu-id="a7200-173">Durante una reunión</span><span class="sxs-lookup"><span data-stu-id="a7200-173">During a meeting</span></span>

<span data-ttu-id="a7200-174">Durante una reunión, puedes usar el meetingSidePanel o el cuadro de diálogo en la reunión para crear experiencias únicas para tus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a7200-174">During a meeting, you can use the meetingSidePanel or the in-meeting dialog box to build unique experiences for your apps.</span></span>

#### <a name="meetingsidepanel"></a><span data-ttu-id="a7200-175">meetingSidePanel</span><span class="sxs-lookup"><span data-stu-id="a7200-175">meetingSidePanel</span></span>

<span data-ttu-id="a7200-176">Con meetingSidePanel, puede personalizar las experiencias de una reunión que permitan a los organizadores y presentadores tener un conjunto diferente de vistas y acciones.</span><span class="sxs-lookup"><span data-stu-id="a7200-176">With the meetingSidePanel, you can customize experiences in a meeting that enable organizers and presenters to have different set of views and actions.</span></span> <span data-ttu-id="a7200-177">En el manifiesto de la aplicación, debes agregar meetingSidePanel a la matriz de contexto.</span><span class="sxs-lookup"><span data-stu-id="a7200-177">In your app manifest, you must add meetingSidePanel to the context array.</span></span> <span data-ttu-id="a7200-178">En la reunión y en todos los escenarios, la aplicación se representa en una pestaña en la reunión que tiene 320 píxeles de ancho.</span><span class="sxs-lookup"><span data-stu-id="a7200-178">In the meeting and in all scenarios, the app is rendered in an in-meeting tab that is 320 pixels in width.</span></span> <span data-ttu-id="a7200-179">Para obtener más información, vea [FrameContext interface](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="a7200-179">For more information, see [FrameContext interface](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true).</span></span>

<span data-ttu-id="a7200-180">Para usar la `userContext` API para enrutar las solicitudes en consecuencia, [vea Teams SDK](../tabs/how-to/access-teams-context.md#user-context).</span><span class="sxs-lookup"><span data-stu-id="a7200-180">To use the `userContext` API to route requests accordingly, see [Teams SDK](../tabs/how-to/access-teams-context.md#user-context).</span></span> <span data-ttu-id="a7200-181">Para obtener más información, [vea Teams de autenticación para pestañas](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="a7200-181">For more information, see [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="a7200-182">El flujo de autenticación para pestañas es muy similar al flujo de autenticación para sitios web.</span><span class="sxs-lookup"><span data-stu-id="a7200-182">Authentication flow for tabs is very similar to the authentication flow for websites.</span></span> <span data-ttu-id="a7200-183">Por lo tanto, las pestañas pueden usar OAuth 2.0 directamente.</span><span class="sxs-lookup"><span data-stu-id="a7200-183">So tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="a7200-184">Para obtener más información, vea Plataforma de identidad de Microsoft y flujo de código de autorización [de OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span><span class="sxs-lookup"><span data-stu-id="a7200-184">For more information, see [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="a7200-185">La extensión de mensajería funciona según lo esperado cuando un usuario está en una vista en la reunión y el usuario puede publicar tarjetas de extensión de mensajes de redacción.</span><span class="sxs-lookup"><span data-stu-id="a7200-185">Messaging extension works as expected when a user is in an in-meeting view, and the user can post compose message extension cards.</span></span> <span data-ttu-id="a7200-186">AppName en la reunión es una información sobre herramientas que indica el nombre de la aplicación en la barra U de la reunión.</span><span class="sxs-lookup"><span data-stu-id="a7200-186">AppName in-meeting is a tooltip that states the app name in-meeting U-bar.</span></span>

> [!NOTE]
> <span data-ttu-id="a7200-187">Use la versión 1.7.0 o posterior de [Teams SDK,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)ya que las versiones anteriores no admiten el panel lateral.</span><span class="sxs-lookup"><span data-stu-id="a7200-187">Use version 1.7.0 or higher of [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), as versions prior to it do not support the side panel.</span></span>

#### <a name="in-meeting-dialog-box"></a><span data-ttu-id="a7200-188">Cuadro de diálogo En la reunión</span><span class="sxs-lookup"><span data-stu-id="a7200-188">In-meeting dialog box</span></span>

<span data-ttu-id="a7200-189">El cuadro de diálogo en la reunión se puede usar para interactuar con los participantes durante la reunión y recopilar información o comentarios durante la reunión.</span><span class="sxs-lookup"><span data-stu-id="a7200-189">The in-meeting dialog box can be used to engage participants during the meeting and collect information or feedback during the meeting.</span></span> <span data-ttu-id="a7200-190">Use la API para indicar que se debe desencadenar [`NotificationSignal`](create-apps-for-teams-meetings.md#notificationsignal-api) una notificación de burbuja.</span><span class="sxs-lookup"><span data-stu-id="a7200-190">Use the [`NotificationSignal`](create-apps-for-teams-meetings.md#notificationsignal-api) API to signal that a bubble notification must be triggered.</span></span> <span data-ttu-id="a7200-191">Como parte de la carga de solicitud de notificación, incluya la dirección URL donde se hospeda el contenido que se va a mostrar.</span><span class="sxs-lookup"><span data-stu-id="a7200-191">As part of the notification request payload, include the URL where the content to be shown is hosted.</span></span>

<span data-ttu-id="a7200-192">El cuadro de diálogo en la reunión no debe usar el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="a7200-192">In-meeting dialog must not use task module.</span></span> <span data-ttu-id="a7200-193">El módulo de tareas no se invoca en un chat de reunión.</span><span class="sxs-lookup"><span data-stu-id="a7200-193">Task module is not invoked in a meeting chat.</span></span> <span data-ttu-id="a7200-194">Se usa una dirección URL de recurso externo para mostrar una burbuja de contenido en una reunión.</span><span class="sxs-lookup"><span data-stu-id="a7200-194">An external resource URL is used to display content bubble in a meeting.</span></span> <span data-ttu-id="a7200-195">Puede usar el método `submitTask` para enviar datos en un chat de reunión.</span><span class="sxs-lookup"><span data-stu-id="a7200-195">You can use the `submitTask` method to submit data in a meeting chat.</span></span>

> [!NOTE]
> * <span data-ttu-id="a7200-196">Debe invocar la [función submitTask() para](../task-modules-and-cards/task-modules/task-modules-bots.md#submit-the-result-of-a-task-module) descartarla automáticamente después de que un usuario realiza una acción en la vista web.</span><span class="sxs-lookup"><span data-stu-id="a7200-196">You must invoke the [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submit-the-result-of-a-task-module) function to dismiss automatically after a user takes an action in the web view.</span></span> <span data-ttu-id="a7200-197">Este es un requisito para el envío de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a7200-197">This is a requirement for app submission.</span></span> <span data-ttu-id="a7200-198">Para obtener más información, [vea Teams módulo de tareas del SDK](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="a7200-198">For more information, see [Teams SDK task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
> * <span data-ttu-id="a7200-199">Si quieres que la aplicación admita usuarios anónimos, la carga inicial de la solicitud de invocación debe basarse en los metadatos de solicitud del objeto, no en `from.id` `from` los `from.aadObjectId` metadatos de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="a7200-199">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id` request metadata in the `from` object, not the `from.aadObjectId` request metadata.</span></span> <span data-ttu-id="a7200-200">`from.id`es el identificador de usuario `from.aadObjectId` y es el Azure Active Directory (AAD) del usuario.</span><span class="sxs-lookup"><span data-stu-id="a7200-200">`from.id` is the user ID and `from.aadObjectId` is the Azure Active Directory (AAD) ID of the user.</span></span> <span data-ttu-id="a7200-201">Para obtener más información, vea [using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) y create and send the task [module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span><span class="sxs-lookup"><span data-stu-id="a7200-201">For more information, see [using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

#### <a name="shared-meeting-stage"></a><span data-ttu-id="a7200-202">Fase de reunión compartida</span><span class="sxs-lookup"><span data-stu-id="a7200-202">Shared meeting stage</span></span>

> [!NOTE]
> * <span data-ttu-id="a7200-203">Esta funcionalidad está disponible actualmente solo en [la versión preliminar del](../resources/dev-preview/developer-preview-intro.md) desarrollador.</span><span class="sxs-lookup"><span data-stu-id="a7200-203">This capability is currently available in [developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="a7200-204">La fase de reunión compartida permite a los participantes de la reunión interactuar y colaborar en el contenido de la aplicación en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="a7200-204">Shared meeting stage allows meeting participants to interact with and collaborate on app content in real-time.</span></span>

<span data-ttu-id="a7200-205">El contexto necesario está `meetingStage` en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a7200-205">The required context is `meetingStage` in the app manifest.</span></span> <span data-ttu-id="a7200-206">Un requisito previo para ello es tener el `meetingSidePanel` contexto.</span><span class="sxs-lookup"><span data-stu-id="a7200-206">A prerequisite for this is to have the `meetingSidePanel` context.</span></span> <span data-ttu-id="a7200-207">Esto habilita **Compartir** en el meetingSidePanel.</span><span class="sxs-lookup"><span data-stu-id="a7200-207">This enables **Share** in the meetingSidePanel.</span></span>

![Compartir en fase durante la experiencia de reunión](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

<span data-ttu-id="a7200-209">Para habilitar la fase de reunión compartida, configure el manifiesto de la aplicación de este modo:</span><span class="sxs-lookup"><span data-stu-id="a7200-209">To enable shared meeting stage, configure your app manifest like this:</span></span>

```json
"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "groupchat"
      ],
      "context":[
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```

<span data-ttu-id="a7200-210">Vea cómo diseñar [una experiencia de fase de reunión compartida.](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)</span><span class="sxs-lookup"><span data-stu-id="a7200-210">See how to [design a shared meeting stage experience](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md).</span></span>

### <a name="after-a-meeting"></a><span data-ttu-id="a7200-211">Después de una reunión</span><span class="sxs-lookup"><span data-stu-id="a7200-211">After a meeting</span></span>

<span data-ttu-id="a7200-212">Las configuraciones después y [antes de las reuniones](#before-a-meeting) son las mismas.</span><span class="sxs-lookup"><span data-stu-id="a7200-212">The configurations after and [before meetings](#before-a-meeting) are the same.</span></span>

## <a name="code-sample"></a><span data-ttu-id="a7200-213">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="a7200-213">Code sample</span></span>

|<span data-ttu-id="a7200-214">Nombre de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a7200-214">Sample name</span></span> | <span data-ttu-id="a7200-215">Descripción</span><span class="sxs-lookup"><span data-stu-id="a7200-215">Description</span></span> | <span data-ttu-id="a7200-216">Muestra</span><span class="sxs-lookup"><span data-stu-id="a7200-216">Sample</span></span> |
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="a7200-217">Aplicación de reunión</span><span class="sxs-lookup"><span data-stu-id="a7200-217">Meeting app</span></span> | <span data-ttu-id="a7200-218">Muestra cómo usar la aplicación Generador de tokens de reunión para solicitar un token, que se genera secuencialmente para que cada participante tenga una oportunidad equitativa de colaborar en una reunión.</span><span class="sxs-lookup"><span data-stu-id="a7200-218">Demonstrates how to use the Meeting Token Generator app to request a token, which is generated sequentially so that each participant has a fair opportunity to contribute in a meeting.</span></span> <span data-ttu-id="a7200-219">Esto puede ser útil en situaciones como reuniones de scrum y preguntas&sesiones A.</span><span class="sxs-lookup"><span data-stu-id="a7200-219">This can be useful in situations like scrum meetings and Q&A sessions.</span></span> | [<span data-ttu-id="a7200-220">View</span><span class="sxs-lookup"><span data-stu-id="a7200-220">View</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token) |

## <a name="see-also"></a><span data-ttu-id="a7200-221">Vea también</span><span class="sxs-lookup"><span data-stu-id="a7200-221">See also</span></span>

* [<span data-ttu-id="a7200-222">Directrices de diseño de cuadros de diálogo en la reunión</span><span class="sxs-lookup"><span data-stu-id="a7200-222">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [<span data-ttu-id="a7200-223">Teams de autenticación para pestañas</span><span class="sxs-lookup"><span data-stu-id="a7200-223">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)

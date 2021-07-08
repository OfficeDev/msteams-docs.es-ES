---
title: Requisitos previos y referencias de API para las aplicaciones en las reuniones de Teams
author: surbhigupta
description: Trabajar con aplicaciones para Teams reuniones
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: API de roles de participantes de reuniones de aplicaciones de teams
ms.openlocfilehash: bc13fa7b8c3af9a7c48463eab7198e908164ffbe
ms.sourcegitcommit: 0a775ae12419f3bc7484e557f4b4ae815bab64ec
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/08/2021
ms.locfileid: "53333690"
---
# <a name="prerequisites-and-api-references-for-apps-in-teams-meetings"></a><span data-ttu-id="3346b-104">Requisitos previos y referencias de API para las aplicaciones en las reuniones de Teams</span><span class="sxs-lookup"><span data-stu-id="3346b-104">Prerequisites and API references for apps in Teams meetings</span></span>

<span data-ttu-id="3346b-105">Para expandir las capacidades de tus aplicaciones en todo el ciclo de vida de la reunión, Teams te permite trabajar con aplicaciones para Teams reuniones.</span><span class="sxs-lookup"><span data-stu-id="3346b-105">To expand the capabilities of your apps across the meeting lifecycle, Teams enables you to work with apps for Teams meetings.</span></span> <span data-ttu-id="3346b-106">Debes pasar por los requisitos previos y puedes usar las referencias a la API de aplicaciones de reunión para mejorar la experiencia de la reunión.</span><span class="sxs-lookup"><span data-stu-id="3346b-106">You must  go through the prerequisites and you can use the meeting apps API references to enhance the meeting experience.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3346b-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3346b-107">Prerequisites</span></span>

<span data-ttu-id="3346b-108">Antes de trabajar con aplicaciones para Teams reuniones, debes comprender lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3346b-108">Before you work with apps for Teams meetings, you must have an understanding of the following:</span></span>

* <span data-ttu-id="3346b-109">Debes tener conocimientos sobre cómo desarrollar Teams aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3346b-109">You must have knowledge of how to develop Teams apps.</span></span> <span data-ttu-id="3346b-110">Para obtener más información, [consulta Teams desarrollo de aplicaciones](../overview.md).</span><span class="sxs-lookup"><span data-stu-id="3346b-110">For more information, see [Teams app development](../overview.md).</span></span>

* <span data-ttu-id="3346b-111">Debes actualizar el manifiesto Teams aplicación para indicar que la aplicación está disponible para reuniones.</span><span class="sxs-lookup"><span data-stu-id="3346b-111">You must update the Teams app manifest to indicate that the app is available for meetings.</span></span> <span data-ttu-id="3346b-112">Para obtener más información, consulta [manifiesto de la aplicación](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest).</span><span class="sxs-lookup"><span data-stu-id="3346b-112">For more information, see [app manifest](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest).</span></span>

* <span data-ttu-id="3346b-113">La aplicación debe admitir pestañas configurables en el ámbito groupchat, para que la aplicación funcione en el ciclo de vida de la reunión como pestaña. Para obtener más información, [vea groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) y [build a group tab](../build-your-first-app/build-channel-tab.md).</span><span class="sxs-lookup"><span data-stu-id="3346b-113">Your app must support configurable tabs in the groupchat scope, for your app to function in the meeting lifecycle as a tab. For more information, see [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md).</span></span>

* <span data-ttu-id="3346b-114">Debe cumplir las directrices generales Teams de diseño de pestañas para escenarios previos y posteriores a la reunión.</span><span class="sxs-lookup"><span data-stu-id="3346b-114">You must adhere to general Teams tab design guidelines for pre and post-meeting scenarios.</span></span> <span data-ttu-id="3346b-115">Para obtener experiencias durante las reuniones, consulte las directrices de diseño de la pestaña en la reunión y del cuadro de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="3346b-115">For experiences during meetings, refer to the in-meeting tab and in-meeting dialog design guidelines.</span></span> <span data-ttu-id="3346b-116">Para obtener más información, [vea Teams de](../tabs/design/tabs.md)diseño de pestañas, directrices de diseño de pestañas en la reunión y directrices de diseño de cuadros de diálogo en la [reunión.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)</span><span class="sxs-lookup"><span data-stu-id="3346b-116">For more information, see [Teams tab design guidelines](../tabs/design/tabs.md), [in-meeting tab design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab), and [in-meeting dialog design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

* <span data-ttu-id="3346b-117">Debes admitir el ámbito para habilitar la aplicación en `groupchat` chats previos y posteriores a la reunión.</span><span class="sxs-lookup"><span data-stu-id="3346b-117">You must support the `groupchat` scope to enable your app in pre-meeting and post-meeting chats.</span></span> <span data-ttu-id="3346b-118">Con la experiencia de la aplicación previa a la reunión, puedes encontrar y agregar aplicaciones de reunión y realizar tareas previas a la reunión.</span><span class="sxs-lookup"><span data-stu-id="3346b-118">With the pre-meeting app experience, you can find and add meeting apps and perform pre-meeting tasks.</span></span> <span data-ttu-id="3346b-119">Con la experiencia de la aplicación posterior a la reunión, puedes ver los resultados de la reunión, como los resultados de encuestas o los comentarios.</span><span class="sxs-lookup"><span data-stu-id="3346b-119">With post-meeting app experience, you can view the results of the meeting, such as poll survey results or feedback.</span></span>

* <span data-ttu-id="3346b-120">Los parámetros de dirección URL de la API de reunión deben `meetingId` `userId` tener , y `tenantId` .</span><span class="sxs-lookup"><span data-stu-id="3346b-120">Meeting API URL parameters must have `meetingId`, `userId`, and `tenantId`.</span></span> <span data-ttu-id="3346b-121">Están disponibles como parte de la actividad del SDK Teams cliente y el bot.</span><span class="sxs-lookup"><span data-stu-id="3346b-121">These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="3346b-122">Además, puede recuperar información confiable para el identificador de usuario y el identificador de inquilino mediante la [autenticación de SSO de tabulación.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="3346b-122">In addition, you can retrieve reliable information for user ID and tenant ID using [tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="3346b-123">La `GetParticipant` API debe tener un registro de bot y un identificador para generar tokens de autenticación.</span><span class="sxs-lookup"><span data-stu-id="3346b-123">The `GetParticipant` API must have a bot registration and ID to generate auth tokens.</span></span> <span data-ttu-id="3346b-124">Para obtener más información, vea [bot registration and ID](../build-your-first-app/build-bot.md).</span><span class="sxs-lookup"><span data-stu-id="3346b-124">For more information, see [bot registration and ID](../build-your-first-app/build-bot.md).</span></span>

* <span data-ttu-id="3346b-125">Para que la aplicación se actualice en tiempo real, debe estar actualizada en función de las actividades de eventos de la reunión.</span><span class="sxs-lookup"><span data-stu-id="3346b-125">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="3346b-126">Estos eventos pueden estar dentro del cuadro de diálogo en la reunión y otras etapas a lo largo del ciclo de vida de la reunión.</span><span class="sxs-lookup"><span data-stu-id="3346b-126">These events can be within the in-meeting dialog box and other stages across the meeting lifecycle.</span></span> <span data-ttu-id="3346b-127">Para el cuadro de diálogo en la reunión, vea el parámetro de `bot Id` finalización en `NotificationSignal` la API.</span><span class="sxs-lookup"><span data-stu-id="3346b-127">For the in-meeting dialog box, see completion `bot Id` parameter in `NotificationSignal` API.</span></span>

* <span data-ttu-id="3346b-128">La API de detalles de la reunión debe tener un registro del bot y un identificador de bot.</span><span class="sxs-lookup"><span data-stu-id="3346b-128">Meeting Details API must have a bot registration and bot ID.</span></span> <span data-ttu-id="3346b-129">Requiere bot SDK para obtener `TurnContext` .</span><span class="sxs-lookup"><span data-stu-id="3346b-129">It requires Bot SDK to get `TurnContext`.</span></span>

* <span data-ttu-id="3346b-130">Para eventos de reunión en tiempo real, debe estar familiarizado con el objeto disponible a través `TurnContext` del SDK de bot.</span><span class="sxs-lookup"><span data-stu-id="3346b-130">For real-time meeting events, you must be familiar with the `TurnContext` object available through the Bot SDK.</span></span> <span data-ttu-id="3346b-131">El `Activity` objeto en contiene la carga con la hora de inicio y finalización `TurnContext` real.</span><span class="sxs-lookup"><span data-stu-id="3346b-131">The `Activity` object in `TurnContext` contains the payload with the actual start and end time.</span></span> <span data-ttu-id="3346b-132">Los eventos de reunión en tiempo real requieren un identificador de bot registrado de Teams plataforma.</span><span class="sxs-lookup"><span data-stu-id="3346b-132">Real-time meeting events require a registered bot ID from the Teams platform.</span></span>

<span data-ttu-id="3346b-133">Una vez que haya pasado por los requisitos previos, puede usar las referencias de api de aplicaciones de reunión , , y la API de detalles de reunión que le permiten tener acceso a la información mediante atributos y mostrar contenido `GetUserContext` `GetParticipant` `NotificationSignal` relevante.</span><span class="sxs-lookup"><span data-stu-id="3346b-133">After you have gone through the prerequisites, you can use the meeting apps API references `GetUserContext`, `GetParticipant`, `NotificationSignal`, and Meeting Details API that enable you to access information using attributes and display relevant content.</span></span>

## <a name="meeting-apps-api-references"></a><span data-ttu-id="3346b-134">Referencias de API de aplicaciones de reunión</span><span class="sxs-lookup"><span data-stu-id="3346b-134">Meeting apps API references</span></span>

<span data-ttu-id="3346b-135">Las nuevas extensibilidades de reuniones le proporcionan API que transforman la experiencia de la reunión.</span><span class="sxs-lookup"><span data-stu-id="3346b-135">The new meeting extensibilities provide you with APIs that transform the meeting experience.</span></span> <span data-ttu-id="3346b-136">Con esta nueva funcionalidad, puedes crear aplicaciones o integrar aplicaciones existentes en el ciclo de vida de la reunión.</span><span class="sxs-lookup"><span data-stu-id="3346b-136">With this new capability, you can build apps or integrate existing apps within the meeting lifecycle.</span></span> <span data-ttu-id="3346b-137">Puedes usar las API para que la aplicación conozca la reunión.</span><span class="sxs-lookup"><span data-stu-id="3346b-137">You can use the APIs to make your app aware of the meeting.</span></span> <span data-ttu-id="3346b-138">Puede elegir qué API desea usar para mejorar la experiencia de la reunión.</span><span class="sxs-lookup"><span data-stu-id="3346b-138">You can choose which APIs you want to use to enhance the meeting experience.</span></span>

<span data-ttu-id="3346b-139">En la tabla siguiente se proporciona una lista de estas API:</span><span class="sxs-lookup"><span data-stu-id="3346b-139">The following table provides a list of these APIs:</span></span>

|<span data-ttu-id="3346b-140">API</span><span class="sxs-lookup"><span data-stu-id="3346b-140">API</span></span>|<span data-ttu-id="3346b-141">Descripción</span><span class="sxs-lookup"><span data-stu-id="3346b-141">Description</span></span>|<span data-ttu-id="3346b-142">Solicitud</span><span class="sxs-lookup"><span data-stu-id="3346b-142">Request</span></span>|<span data-ttu-id="3346b-143">Origen</span><span class="sxs-lookup"><span data-stu-id="3346b-143">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="3346b-144">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="3346b-144">**GetUserContext**</span></span>| <span data-ttu-id="3346b-145">Esta API le permite obtener información contextual para mostrar contenido relevante en una Teams pestaña.</span><span class="sxs-lookup"><span data-stu-id="3346b-145">This API enables you to get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="3346b-146">_**microsoftTeams.getContext( ( ) => { /*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="3346b-146">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="3346b-147">Microsoft Teams SDK de cliente</span><span class="sxs-lookup"><span data-stu-id="3346b-147">Microsoft Teams Client SDK</span></span>|
|<span data-ttu-id="3346b-148">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="3346b-148">**GetParticipant**</span></span>| <span data-ttu-id="3346b-149">Esta API permite que un bot obtenga información de los participantes mediante el identificador de reunión y el identificador de participante.</span><span class="sxs-lookup"><span data-stu-id="3346b-149">This API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> |<span data-ttu-id="3346b-150">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="3346b-150">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="3346b-151">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="3346b-151">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="3346b-152">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="3346b-152">**NotificationSignal**</span></span> | <span data-ttu-id="3346b-153">Esta API le permite proporcionar señales de reunión que se entregan mediante la API de notificación de conversación existente para el chat de bots de usuario.</span><span class="sxs-lookup"><span data-stu-id="3346b-153">This API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="3346b-154">Le permite señalar en función de la acción del usuario que muestra un cuadro de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="3346b-154">It allows you to signal based on user action that shows an in-meeting dialog box.</span></span> |<span data-ttu-id="3346b-155">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="3346b-155">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="3346b-156">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="3346b-156">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="3346b-157">**Detalles de la reunión**</span><span class="sxs-lookup"><span data-stu-id="3346b-157">**Meeting Details**</span></span> | <span data-ttu-id="3346b-158">Esta API le permite obtener metadatos estáticos de reunión.</span><span class="sxs-lookup"><span data-stu-id="3346b-158">This API enables you to get static meeting metadata.</span></span> |<span data-ttu-id="3346b-159">**GET** _**/v1/meetings/{meetingId}**_</span><span class="sxs-lookup"><span data-stu-id="3346b-159">**GET** _**/v1/meetings/{meetingId}**_</span></span>| <span data-ttu-id="3346b-160">Bot SDK</span><span class="sxs-lookup"><span data-stu-id="3346b-160">Bot SDK</span></span> |

### <a name="getusercontext-api"></a><span data-ttu-id="3346b-161">GetUserContext API</span><span class="sxs-lookup"><span data-stu-id="3346b-161">GetUserContext API</span></span>

<span data-ttu-id="3346b-162">Para identificar y recuperar información contextual para el contenido de la pestaña, vea [Obtener contexto para su Teams pestaña](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library). se usa en una pestaña al ejecutarse en el contexto de la reunión y `meetingId` se agrega para la carga de respuesta.</span><span class="sxs-lookup"><span data-stu-id="3346b-162">To identify and retrieve contextual information for your tab content, see [get context for your Teams tab](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library). `meetingId` is used by a tab when running in the meeting context and is added for the response payload.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="3346b-163">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="3346b-163">GetParticipant API</span></span>

> [!NOTE]
> * <span data-ttu-id="3346b-164">No almacenar en caché los roles de los participantes, ya que el organizador de la reunión puede cambiar los roles en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="3346b-164">Do not cache participant roles since the meeting organizer can change the roles any time.</span></span>
> * <span data-ttu-id="3346b-165">Teams actualmente no admite listas de distribución grandes ni tamaños de lista de más de 350 participantes para la `GetParticipant` API.</span><span class="sxs-lookup"><span data-stu-id="3346b-165">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

<span data-ttu-id="3346b-166">La `GetParticipant` API permite que un bot obtenga información de los participantes mediante el identificador de reunión y el identificador de participante.</span><span class="sxs-lookup"><span data-stu-id="3346b-166">The `GetParticipant` API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> <span data-ttu-id="3346b-167">La API incluye parámetros de consulta, ejemplos y códigos de respuesta.</span><span class="sxs-lookup"><span data-stu-id="3346b-167">The API includes query parameters, examples, and response codes.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="3346b-168">Parámetros de consulta</span><span class="sxs-lookup"><span data-stu-id="3346b-168">Query parameters</span></span>

<span data-ttu-id="3346b-169">La `GetParticipant` API incluye los siguientes parámetros de consulta:</span><span class="sxs-lookup"><span data-stu-id="3346b-169">The `GetParticipant` API includes the following query parameters:</span></span>

|<span data-ttu-id="3346b-170">Valor</span><span class="sxs-lookup"><span data-stu-id="3346b-170">Value</span></span>|<span data-ttu-id="3346b-171">Tipo</span><span class="sxs-lookup"><span data-stu-id="3346b-171">Type</span></span>|<span data-ttu-id="3346b-172">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="3346b-172">Required</span></span>|<span data-ttu-id="3346b-173">Descripción</span><span class="sxs-lookup"><span data-stu-id="3346b-173">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="3346b-174">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="3346b-174">**meetingId**</span></span>| <span data-ttu-id="3346b-175">Cadena</span><span class="sxs-lookup"><span data-stu-id="3346b-175">String</span></span> | <span data-ttu-id="3346b-176">Sí</span><span class="sxs-lookup"><span data-stu-id="3346b-176">Yes</span></span> | <span data-ttu-id="3346b-177">El identificador de reunión está disponible a través de Bot Invoke y Teams CLIENT SDK.</span><span class="sxs-lookup"><span data-stu-id="3346b-177">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="3346b-178">**participantId**</span><span class="sxs-lookup"><span data-stu-id="3346b-178">**participantId**</span></span>| <span data-ttu-id="3346b-179">Cadena</span><span class="sxs-lookup"><span data-stu-id="3346b-179">String</span></span> | <span data-ttu-id="3346b-180">Sí</span><span class="sxs-lookup"><span data-stu-id="3346b-180">Yes</span></span> | <span data-ttu-id="3346b-181">El identificador de participante es el identificador de usuario.</span><span class="sxs-lookup"><span data-stu-id="3346b-181">The participant ID is the user ID.</span></span> <span data-ttu-id="3346b-182">Está disponible en TAB SSO, Bot Invoke y Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="3346b-182">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="3346b-183">Se recomienda obtener un identificador de participante del SSO de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="3346b-183">It is recommended to get a participant ID from the Tab SSO.</span></span> |
|<span data-ttu-id="3346b-184">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="3346b-184">**tenantId**</span></span>| <span data-ttu-id="3346b-185">Cadena</span><span class="sxs-lookup"><span data-stu-id="3346b-185">String</span></span> | <span data-ttu-id="3346b-186">Sí</span><span class="sxs-lookup"><span data-stu-id="3346b-186">Yes</span></span> | <span data-ttu-id="3346b-187">El identificador de inquilino es necesario para los usuarios del espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="3346b-187">The tenant ID is required for the tenant users.</span></span> <span data-ttu-id="3346b-188">Está disponible en TAB SSO, Bot Invoke y Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="3346b-188">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="3346b-189">Se recomienda obtener un identificador de inquilino del SSO de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="3346b-189">It is recommended to get a tenant ID from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="3346b-190">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="3346b-190">Example</span></span>

<span data-ttu-id="3346b-191">La `GetParticipant` API incluye los siguientes ejemplos:</span><span class="sxs-lookup"><span data-stu-id="3346b-191">The `GetParticipant` API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="3346b-192">C#</span><span class="sxs-lookup"><span data-stu-id="3346b-192">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  TeamsMeetingParticipant participant = await TeamsInfo.GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourParticipantTenantId").ConfigureAwait(false);
  TeamsChannelAccount member = participant.User;
  MeetingParticipantInfo meetingInfo = participant.Meeting;
  ConversationAccount conversation = participant.Conversation;

  await turnContext.SendActivityAsync(MessageFactory.Text($"The participant role is: {meetingInfo.Role}"), cancellationToken);
}

```

# <a name="javascript"></a>[<span data-ttu-id="3346b-193">JavaScript</span><span class="sxs-lookup"><span data-stu-id="3346b-193">JavaScript</span></span>](#tab/javascript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            TeamsMeetingParticipant participant = getMeetingParticipant(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
            let member = participant.user;
            let meetingInfo = participant.meeting;
            let conversation = participant.conversation;
            
            await context.sendActivity(`The participant role is: '${meetingInfo.role}'`);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="3346b-194">JSON</span><span class="sxs-lookup"><span data-stu-id="3346b-194">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

---

<span data-ttu-id="3346b-195">El cuerpo de la respuesta JSON `GetParticipant` para la API es:</span><span class="sxs-lookup"><span data-stu-id="3346b-195">The JSON response body for `GetParticipant` API is:</span></span>

```json
{
   "user":{
      "id":"29:1JKiJGPAX9TTxtGxhVo0wLx_zwzo-gG8Z-X03306vBwi9p-xMTEbDXsT6KH7-0kkTS8cD-2zkrsoV6f5WJ6_aYw",
      "aadObjectId":"e236c4bf-88b1-4f3a-b1d7-8891dfc332b5",
      "name":"Bob Young",
      "givenName":"Bob",
      "surname":"Young",
      "email":"Bob.young@microsoft.com",
      "userPrincipalName":"Bob.young@microsoft.com",
      "tenantId":"2fe477ab-0efc-4dfd-bde2-484374e2c373",
      "userRole":"user"
   },
   "meeting":{
      "role ":"Presenter",
      "inMeeting":true
   },
   "conversation":{
      "id":"<conversation id>",
      "isGroup":true
   }
}
```

#### <a name="response-codes"></a><span data-ttu-id="3346b-196">Códigos de respuesta</span><span class="sxs-lookup"><span data-stu-id="3346b-196">Response codes</span></span>

<span data-ttu-id="3346b-197">La `GetParticipant` API devuelve los siguientes códigos de respuesta:</span><span class="sxs-lookup"><span data-stu-id="3346b-197">The `GetParticipant` API returns the following response codes:</span></span>

|<span data-ttu-id="3346b-198">Código de respuesta</span><span class="sxs-lookup"><span data-stu-id="3346b-198">Response code</span></span>|<span data-ttu-id="3346b-199">Descripción</span><span class="sxs-lookup"><span data-stu-id="3346b-199">Description</span></span>|
|---|---|
| <span data-ttu-id="3346b-200">**403**</span><span class="sxs-lookup"><span data-stu-id="3346b-200">**403**</span></span> | <span data-ttu-id="3346b-201">La aplicación no puede obtener información de los participantes.</span><span class="sxs-lookup"><span data-stu-id="3346b-201">The app is not allowed to get participant information.</span></span> <span data-ttu-id="3346b-202">Esta es la respuesta de error más común y se desencadena si la aplicación no está instalada en la reunión.</span><span class="sxs-lookup"><span data-stu-id="3346b-202">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="3346b-203">Por ejemplo, si la aplicación está deshabilitada por el administrador del espacio empresarial o bloqueada durante la migración del sitio en directo.</span><span class="sxs-lookup"><span data-stu-id="3346b-203">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>|
| <span data-ttu-id="3346b-204">**200**</span><span class="sxs-lookup"><span data-stu-id="3346b-204">**200**</span></span> | <span data-ttu-id="3346b-205">La información del participante se recupera correctamente.</span><span class="sxs-lookup"><span data-stu-id="3346b-205">The participant information is successfully retrieved.</span></span>|
| <span data-ttu-id="3346b-206">**401**</span><span class="sxs-lookup"><span data-stu-id="3346b-206">**401**</span></span> | <span data-ttu-id="3346b-207">La aplicación responde con un token no válido.</span><span class="sxs-lookup"><span data-stu-id="3346b-207">The app responds with an invalid token.</span></span>|
| <span data-ttu-id="3346b-208">**404**</span><span class="sxs-lookup"><span data-stu-id="3346b-208">**404**</span></span> | <span data-ttu-id="3346b-209">La reunión ha expirado o no se encuentra el participante.</span><span class="sxs-lookup"><span data-stu-id="3346b-209">The meeting has either expired or participant cannot be found.</span></span>|

### <a name="notificationsignal-api"></a><span data-ttu-id="3346b-210">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="3346b-210">NotificationSignal API</span></span>

<span data-ttu-id="3346b-211">Todos los usuarios de una reunión reciben las notificaciones enviadas a través de la `NotificationSignal` API.</span><span class="sxs-lookup"><span data-stu-id="3346b-211">All users in a meeting receive the notifications sent through the `NotificationSignal` API.</span></span>

> [!NOTE]
> * <span data-ttu-id="3346b-212">Cuando se invoca un cuadro de diálogo en la reunión, el contenido se presenta como un mensaje de chat.</span><span class="sxs-lookup"><span data-stu-id="3346b-212">When an in-meeting dialog box is invoked, the content is presented as a chat message.</span></span>
> * <span data-ttu-id="3346b-213">Actualmente, no se admite el envío de notificaciones dirigidas.</span><span class="sxs-lookup"><span data-stu-id="3346b-213">Currently, sending targeted notifications is not supported.</span></span>

<span data-ttu-id="3346b-214">`NotificationSignal` La API le permite proporcionar señales de reunión que se entregan mediante la API de notificación de conversación existente para el chat de bots de usuario.</span><span class="sxs-lookup"><span data-stu-id="3346b-214">`NotificationSignal` API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="3346b-215">Esta API le permite señalar en función de la acción del usuario que muestra un cuadro de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="3346b-215">This API allows you to signal based on user action that shows an in-meeting dialog box.</span></span> <span data-ttu-id="3346b-216">La API incluye parámetros de consulta, ejemplos y códigos de respuesta.</span><span class="sxs-lookup"><span data-stu-id="3346b-216">The API includes query parameter, examples, and response codes.</span></span>

#### <a name="query-parameter"></a><span data-ttu-id="3346b-217">Parámetro de consulta</span><span class="sxs-lookup"><span data-stu-id="3346b-217">Query parameter</span></span>

<span data-ttu-id="3346b-218">La `NotificationSignal` API incluye el siguiente parámetro de consulta:</span><span class="sxs-lookup"><span data-stu-id="3346b-218">The `NotificationSignal` API includes the following query parameter:</span></span>

|<span data-ttu-id="3346b-219">Valor</span><span class="sxs-lookup"><span data-stu-id="3346b-219">Value</span></span>|<span data-ttu-id="3346b-220">Tipo</span><span class="sxs-lookup"><span data-stu-id="3346b-220">Type</span></span>|<span data-ttu-id="3346b-221">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="3346b-221">Required</span></span>|<span data-ttu-id="3346b-222">Descripción</span><span class="sxs-lookup"><span data-stu-id="3346b-222">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="3346b-223">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="3346b-223">**conversationId**</span></span>| <span data-ttu-id="3346b-224">Cadena</span><span class="sxs-lookup"><span data-stu-id="3346b-224">String</span></span> | <span data-ttu-id="3346b-225">Sí</span><span class="sxs-lookup"><span data-stu-id="3346b-225">Yes</span></span> | <span data-ttu-id="3346b-226">El identificador de conversación está disponible como parte de Bot Invoke.</span><span class="sxs-lookup"><span data-stu-id="3346b-226">The conversation identifier is available as part of Bot Invoke.</span></span> |

#### <a name="examples"></a><span data-ttu-id="3346b-227">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="3346b-227">Examples</span></span>

<span data-ttu-id="3346b-228">Se `Bot ID` declara en el manifiesto y el bot recibe un objeto result.</span><span class="sxs-lookup"><span data-stu-id="3346b-228">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span>

> [!NOTE]
> * <span data-ttu-id="3346b-229">El `completionBotId` parámetro de la es opcional en el ejemplo de carga `externalResourceUrl` solicitada.</span><span class="sxs-lookup"><span data-stu-id="3346b-229">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="3346b-230">`Bot ID` se declara en el manifiesto y el bot recibe un objeto result.</span><span class="sxs-lookup"><span data-stu-id="3346b-230">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="3346b-231">Los `externalResourceUrl` parámetros de ancho y alto deben estar en píxeles.</span><span class="sxs-lookup"><span data-stu-id="3346b-231">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="3346b-232">Para asegurarse de que las dimensiones están dentro de los límites permitidos, vea [directrices de diseño](design/designing-apps-in-meetings.md).</span><span class="sxs-lookup"><span data-stu-id="3346b-232">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="3346b-233">La dirección URL es la página cargada como una en el cuadro de diálogo `<iframe>` en la reunión.</span><span class="sxs-lookup"><span data-stu-id="3346b-233">The URL is the page loaded as an `<iframe>` in the in-meeting dialog box.</span></span> <span data-ttu-id="3346b-234">El dominio debe estar en la matriz de la aplicación `validDomains` en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3346b-234">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

<span data-ttu-id="3346b-235">La `NotificationSignal` API incluye los siguientes ejemplos:</span><span class="sxs-lookup"><span data-stu-id="3346b-235">The `NotificationSignal` API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="3346b-236">C#</span><span class="sxs-lookup"><span data-stu-id="3346b-236">C#</span></span>](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");
activity.TeamsNotifyUser(true, "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID");
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[<span data-ttu-id="3346b-237">JavaScript</span><span class="sxs-lookup"><span data-stu-id="3346b-237">JavaScript</span></span>](#tab/javascript)

```javascript

const replyActivity = MessageFactory.text('Hi'); // this could be an adaptive card instead
replyActivity.channelData = {
    notification: {
        alertInMeeting: true,
        externalResourceUrl: 'https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID’
    }
};
await context.sendActivity(replyActivity);
```

# <a name="json"></a>[<span data-ttu-id="3346b-238">JSON</span><span class="sxs-lookup"><span data-stu-id="3346b-238">JSON</span></span>](#tab/json)

```http
POST /v3/conversations/{conversationId}/activities

{
    "type": "message",
    "text": "John Phillips assigned you a weekly todo",
    "summary": "Don't forget to meet with Marketing next week",
    "channelData": {
        "notification": {
            "alertInMeeting": true,
            "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
        }
    },
    "replyToId": "1493070356924"
}
```

---

#### <a name="response-codes"></a><span data-ttu-id="3346b-239">Códigos de respuesta</span><span class="sxs-lookup"><span data-stu-id="3346b-239">Response codes</span></span>

<span data-ttu-id="3346b-240">La `NotificationSignal` API incluye los siguientes códigos de respuesta:</span><span class="sxs-lookup"><span data-stu-id="3346b-240">The `NotificationSignal` API includes the following response codes:</span></span>

|<span data-ttu-id="3346b-241">Código de respuesta</span><span class="sxs-lookup"><span data-stu-id="3346b-241">Response code</span></span>|<span data-ttu-id="3346b-242">Descripción</span><span class="sxs-lookup"><span data-stu-id="3346b-242">Description</span></span>|
|---|---|
| <span data-ttu-id="3346b-243">**201**</span><span class="sxs-lookup"><span data-stu-id="3346b-243">**201**</span></span> | <span data-ttu-id="3346b-244">La actividad con señal se envía correctamente.</span><span class="sxs-lookup"><span data-stu-id="3346b-244">The activity with signal is successfully sent.</span></span> |
| <span data-ttu-id="3346b-245">**401**</span><span class="sxs-lookup"><span data-stu-id="3346b-245">**401**</span></span> | <span data-ttu-id="3346b-246">La aplicación responde con un token no válido.</span><span class="sxs-lookup"><span data-stu-id="3346b-246">The app responds with an invalid token.</span></span> |
| <span data-ttu-id="3346b-247">**403**</span><span class="sxs-lookup"><span data-stu-id="3346b-247">**403**</span></span> | <span data-ttu-id="3346b-248">La aplicación no puede enviar la señal.</span><span class="sxs-lookup"><span data-stu-id="3346b-248">The app is unable to send the signal.</span></span> <span data-ttu-id="3346b-249">Esto puede ocurrir debido a diversos motivos, como que el administrador de inquilinos deshabilita la aplicación, la aplicación se bloquea durante la migración del sitio en directo, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="3346b-249">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="3346b-250">En este caso, la carga contiene un mensaje de error detallado.</span><span class="sxs-lookup"><span data-stu-id="3346b-250">In this case, the payload contains a detailed error message.</span></span> |
| <span data-ttu-id="3346b-251">**404**</span><span class="sxs-lookup"><span data-stu-id="3346b-251">**404**</span></span> | <span data-ttu-id="3346b-252">El chat de reunión no existe.</span><span class="sxs-lookup"><span data-stu-id="3346b-252">The meeting chat does not exist.</span></span> |

### <a name="meeting-details-api"></a><span data-ttu-id="3346b-253">API de detalles de reunión</span><span class="sxs-lookup"><span data-stu-id="3346b-253">Meeting Details API</span></span>

> [!NOTE]
> <span data-ttu-id="3346b-254">Esta característica está disponible actualmente solo en [la versión preliminar del desarrollador](../resources/dev-preview/developer-preview-intro.md) público.</span><span class="sxs-lookup"><span data-stu-id="3346b-254">This feature is currently available in [public developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="3346b-255">La API de detalles de la reunión permite a la aplicación obtener metadatos estáticos de la reunión.</span><span class="sxs-lookup"><span data-stu-id="3346b-255">The Meeting Details API enables your app to get static meeting metadata.</span></span> <span data-ttu-id="3346b-256">Estos son puntos de datos que no cambian dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="3346b-256">These are data points that do not change dynamically.</span></span>
<span data-ttu-id="3346b-257">La API está disponible a través de Bot Services.</span><span class="sxs-lookup"><span data-stu-id="3346b-257">The API is available through Bot Services.</span></span>

#### <a name="prerequisite"></a><span data-ttu-id="3346b-258">Requisito previo</span><span class="sxs-lookup"><span data-stu-id="3346b-258">Prerequisite</span></span>

<span data-ttu-id="3346b-259">Para usar la API de detalles de reunión, debe obtener permisos de RSC.</span><span class="sxs-lookup"><span data-stu-id="3346b-259">To use the Meeting Details API, you must obtain RSC permissions.</span></span> <span data-ttu-id="3346b-260">Use el siguiente ejemplo para configurar la propiedad del manifiesto de la `webApplicationInfo` aplicación:</span><span class="sxs-lookup"><span data-stu-id="3346b-260">Use the following example to configure your app manifest's `webApplicationInfo` property:</span></span>

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```
 
#### <a name="query-parameter"></a><span data-ttu-id="3346b-261">Parámetro de consulta</span><span class="sxs-lookup"><span data-stu-id="3346b-261">Query parameter</span></span>

<span data-ttu-id="3346b-262">La API de detalles de reunión incluye el siguiente parámetro de consulta:</span><span class="sxs-lookup"><span data-stu-id="3346b-262">The Meeting Details API includes the following query parameter:</span></span>

|<span data-ttu-id="3346b-263">Valor</span><span class="sxs-lookup"><span data-stu-id="3346b-263">Value</span></span>|<span data-ttu-id="3346b-264">Tipo</span><span class="sxs-lookup"><span data-stu-id="3346b-264">Type</span></span>|<span data-ttu-id="3346b-265">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="3346b-265">Required</span></span>|<span data-ttu-id="3346b-266">Descripción</span><span class="sxs-lookup"><span data-stu-id="3346b-266">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="3346b-267">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="3346b-267">**meetingId**</span></span>| <span data-ttu-id="3346b-268">Cadena</span><span class="sxs-lookup"><span data-stu-id="3346b-268">String</span></span> | <span data-ttu-id="3346b-269">Sí</span><span class="sxs-lookup"><span data-stu-id="3346b-269">Yes</span></span> | <span data-ttu-id="3346b-270">El identificador de reunión está disponible a través de Bot Invoke y Teams CLIENT SDK.</span><span class="sxs-lookup"><span data-stu-id="3346b-270">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span> |

#### <a name="example"></a><span data-ttu-id="3346b-271">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="3346b-271">Example</span></span>

<span data-ttu-id="3346b-272">La API de detalles de la reunión incluye los siguientes ejemplos:</span><span class="sxs-lookup"><span data-stu-id="3346b-272">The Meeting Details API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="3346b-273">C#</span><span class="sxs-lookup"><span data-stu-id="3346b-273">C#</span></span>](#tab/dotnet)

```csharp
var connectorClient = turnContext.TurnState.Get<IConnectorClient>();
var creds = connectorClient.Credentials as AppCredentials;
var bearerToken = await creds.GetTokenAsync().ConfigureAwait(false);
var request = new HttpRequestMessage(HttpMethod.Get, new Uri(new Uri(connectorClient.BaseUri.OriginalString), $"v1/meetings/{meetingId}"));
request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
HttpResponseMessage response = await (connectorClient as ServiceClient<ConnectorClient>).HttpClient.SendAsync(request, CancellationToken.None).ConfigureAwait(false);
string content;
if (response.Content != null)
{
    content = await response.Content.ReadAsStringAsync().ConfigureAwait(false);
}
```

# <a name="javascript"></a>[<span data-ttu-id="3346b-274">JavaScript</span><span class="sxs-lookup"><span data-stu-id="3346b-274">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="3346b-275">No disponible</span><span class="sxs-lookup"><span data-stu-id="3346b-275">Not available</span></span>

# <a name="json"></a>[<span data-ttu-id="3346b-276">JSON</span><span class="sxs-lookup"><span data-stu-id="3346b-276">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}
```

---

<span data-ttu-id="3346b-277">El cuerpo de la respuesta JSON para la API de detalles de reunión es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="3346b-277">The JSON response body for Meeting Details API is as follows:</span></span>

```json
{ 
   "details": { 
        "id": "meeting ID", 
        "msGraphResourceId": "", 
        "scheduledStartTime": "2020-08-21T02:30:00+00:00", 
        "scheduledEndTime": "2020-08-21T03:00:00+00:00", 
        "joinUrl": "https://teams.microsoft.com/l/xx", 
        "title": "All Hands", 
        "type": "Scheduled" 
    }, 
    "conversation": { 
            "isGroup": true, 
            “conversationType”: “groupchat”, 
            "id": "meeting chat ID" 
    }, 
    "organizer": { 
        "id": "<organizer user ID>", 
        "aadObjectId": "<AAD ID>", 
        "tenantId": "<Tenant ID>" 
    }
} 
```

## <a name="real-time-teams-meeting-events"></a><span data-ttu-id="3346b-278">Eventos de reuniones Teams en tiempo real</span><span class="sxs-lookup"><span data-stu-id="3346b-278">Real-time Teams meeting events</span></span>

> [!NOTE]
> <span data-ttu-id="3346b-279">Esta característica está disponible actualmente solo en [la versión preliminar del desarrollador](../resources/dev-preview/developer-preview-intro.md) público.</span><span class="sxs-lookup"><span data-stu-id="3346b-279">This feature is currently available in [public developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="3346b-280">El usuario puede recibir eventos de reunión en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="3346b-280">The user can receive real-time meeting events.</span></span> <span data-ttu-id="3346b-281">Tan pronto como cualquier aplicación está asociada a una reunión, el inicio real de la reunión y la hora de finalización de la reunión se comparten con el bot.</span><span class="sxs-lookup"><span data-stu-id="3346b-281">As soon as any app is associated with a meeting, the actual meeting start and meeting end time are shared with the bot.</span></span>

<span data-ttu-id="3346b-282">La hora real de inicio y finalización de una reunión es diferente de la hora de inicio y finalización programada.</span><span class="sxs-lookup"><span data-stu-id="3346b-282">Actual start and end time of a meeting are different from the scheduled start and end time.</span></span> <span data-ttu-id="3346b-283">La API de detalles de la reunión proporciona la hora de inicio y finalización programadas, mientras que el evento proporciona la hora real de inicio y finalización.</span><span class="sxs-lookup"><span data-stu-id="3346b-283">The meeting details API provides the scheduled start and end time while the event provides the actual start and end time.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="3346b-284">Requisito previo</span><span class="sxs-lookup"><span data-stu-id="3346b-284">Prerequisite</span></span>

<span data-ttu-id="3346b-285">El manifiesto de la aplicación debe tener la `webApplicationInfo` propiedad para recibir los eventos de inicio y finalización de la reunión.</span><span class="sxs-lookup"><span data-stu-id="3346b-285">Your app manifest must have the `webApplicationInfo` property to receive the meeting start and end events.</span></span> <span data-ttu-id="3346b-286">Use el siguiente ejemplo para configurar el manifiesto:</span><span class="sxs-lookup"><span data-stu-id="3346b-286">Use the following example to configure your manifest:</span></span>

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

### <a name="example-of-meeting-start-event-payload"></a><span data-ttu-id="3346b-287">Ejemplo de carga del evento de inicio de reunión</span><span class="sxs-lookup"><span data-stu-id="3346b-287">Example of meeting start event payload</span></span>

<span data-ttu-id="3346b-288">El código siguiente proporciona un ejemplo de carga del evento de inicio de reunión:</span><span class="sxs-lookup"><span data-stu-id="3346b-288">The following code provides an example of meeting start event payload:</span></span>

```json
{ 
    "name": "application/vnd.microsoft.meetingStart", 
    "type": "event", 
    "timestamp": "2021-04-29T16:10:41.1252256Z", 
    "id": "123", 
    "channelId": "msteams", 
    "serviceUrl": "https://microsoft.com", 
    "from": { 
        "id": "userID", 
        "aadObjectId": "aadOnjectId" 
    }, 
    "conversation": { 
        "isGroup": true, 
        "tenantId": "tenantId", 
        "id": "thread id" 
    }, 
    "recipient": { 
        "id": "user Id", 
        "name": "user name" 
    }, 
    "entities": [ 
        { 
            "locale": "en-US", 
            "country": "US", 
            "type": "clientInfo" 
        } 
    ], 
    "channelData": { 
        "tenant": { 
            "id": "channel id" 
        }, 
        "source": null, 
        "meeting": { 
            "id": "meeting id" 
        } 
    }, 
    "value": { 
        "MeetingType": "Scheduled", 
        "Title": "Meeting Start/End Event", 
        "Id":"meeting id", 
        "JoinUrl": "url" 
        "StartTime": "2021-04-29T16:17:17.4388966Z" 
    }, 
    "locale": "en-US" 
}
```

### <a name="example-of-meeting-end-event-payload"></a><span data-ttu-id="3346b-289">Ejemplo de carga del evento de fin de reunión</span><span class="sxs-lookup"><span data-stu-id="3346b-289">Example of meeting end event payload</span></span>

<span data-ttu-id="3346b-290">El código siguiente proporciona un ejemplo de carga del evento de fin de reunión:</span><span class="sxs-lookup"><span data-stu-id="3346b-290">The following code provides an example of meeting end event payload:</span></span>

```json
{ 
    "name": "application/vnd.microsoft.meetingEnd", 
    "type": "event", 
    "timestamp": "2021-04-29T16:17:17.4388966Z", 
    "id": "123", 
    "channelId": "msteams", 
    "serviceUrl": "https://microsoft.com", 
    "from": { 
        "id": "user id", 
        "aadObjectId": "aadObjectId" 
    }, 
    "conversation": { 
        "isGroup": true, 
        "tenantId": "tenantId", 
        "id": "thread id" 
    }, 
    "recipient": { 
        "id": "user id", 
        "name": "user name" 
    }, 
    "entities": [ 
        { 
            "locale": "en-US", 
            "country": "US", 
            "type": "clientInfo" 
        } 
    ], 
    "channelData": { 
        "tenant": { 
            "id": "channel id" 
        }, 
        "source": null, 
        "meeting": { 
            "id": "meeting Id" 
        } 
    }, 
    "value": { 
        "MeetingType": "Scheduled", 
        "Title": "Meeting Start/End Event in Canary", 
        "Id": "19:meeting_NTM3ZDJjOTUtZGRhOS00MzYxLTk5NDAtMzY4M2IzZWFjZGE1@thread.v2", 
        "JoinUrl": "url", 
        "EndTime": "2021-04-29T16:17:17.4388966Z" 
    }, 
    "locale": "en-US" 
}
```

### <a name="example-of-getting-metadata-of-a-meeting"></a><span data-ttu-id="3346b-291">Ejemplo de obtener metadatos de una reunión</span><span class="sxs-lookup"><span data-stu-id="3346b-291">Example of getting metadata of a meeting</span></span>

<span data-ttu-id="3346b-292">El bot recibe el evento a través del `OnEventActivityAsync` controlador.</span><span class="sxs-lookup"><span data-stu-id="3346b-292">Your bot receives the event through the `OnEventActivityAsync` handler.</span></span>

<span data-ttu-id="3346b-293">Para deserializar la carga json, se introduce un objeto de modelo para obtener los metadatos de una reunión.</span><span class="sxs-lookup"><span data-stu-id="3346b-293">To deserialize the json payload, a model object is introduced to get the metadata of a meeting.</span></span> <span data-ttu-id="3346b-294">Los metadatos de una reunión residen en la `value` propiedad de la carga del evento.</span><span class="sxs-lookup"><span data-stu-id="3346b-294">The metadata of a meeting resides in the `value` property in the event payload.</span></span> <span data-ttu-id="3346b-295">Se `MeetingStartEndEventvalue` crea el objeto model, cuyas variables de miembro corresponden a las claves de la propiedad en la carga del `value` evento.</span><span class="sxs-lookup"><span data-stu-id="3346b-295">The `MeetingStartEndEventvalue` model object is created, whose member variables correspond to the keys under the `value` property in the event payload.</span></span>

<span data-ttu-id="3346b-296">El código siguiente muestra cómo capturar los metadatos de una reunión que es , , , , y desde un evento de inicio y finalización de `MeetingType` `Title` la `Id` `JoinUrl` `StartTime` `EndTime` reunión:</span><span class="sxs-lookup"><span data-stu-id="3346b-296">The following code shows how to capture the metadata of a meeting that is `MeetingType`, `Title`, `Id`, `JoinUrl`, `StartTime`, and `EndTime` from a meeting start and end event:</span></span>

```csharp
protected override async Task OnEventActivityAsync(
ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    // Event Name is either 'application/vnd.microsoft.meetingStart' or 'application/vnd.microsoft.meetingEnd'
    var meetingEventName = turnContext.Activity.Name;
    // Value contains meeting information (ex: meeting type, start time, etc).
    var meetingEventInfo = turnContext.Activity.Value as JObject; 
    var meetingEventInfoObject =
meetingEventInfo.ToObject<MeetingStartEndEventValue>();
    // Create a very simple adaptive card with meeting information
var attachmentCard = createMeetingStartOrEndEventAttachment(meetingEventName,
meetingEventInfoObject);
    await turnContext.SendActivityAsync(MessageFactory.Attachment(attachmentCard));
}
```

<span data-ttu-id="3346b-297">MeetingStartEndEventvalue.cs incluye el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="3346b-297">The MeetingStartEndEventvalue.cs includes the following code:</span></span>

```csharp
public class MeetingStartEndEventValue
{
    public string Id { get; set; }
    public string Title { get; set; }
    public string MeetingType { get; set; }
    public string JoinUrl { get; set; }
    public string StartTime { get; set; }
    public string EndTime { get; set; }
}
```

## <a name="code-sample"></a><span data-ttu-id="3346b-298">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="3346b-298">Code sample</span></span>

|<span data-ttu-id="3346b-299">Nombre de ejemplo</span><span class="sxs-lookup"><span data-stu-id="3346b-299">Sample name</span></span> | <span data-ttu-id="3346b-300">Descripción</span><span class="sxs-lookup"><span data-stu-id="3346b-300">Description</span></span> | <span data-ttu-id="3346b-301">.NET</span><span class="sxs-lookup"><span data-stu-id="3346b-301">.NET</span></span> | <span data-ttu-id="3346b-302">Node.js</span><span class="sxs-lookup"><span data-stu-id="3346b-302">Node.js</span></span> |
|----------------|-----------------|--------------|--------------|
| <span data-ttu-id="3346b-303">Extensibilidad de reuniones</span><span class="sxs-lookup"><span data-stu-id="3346b-303">Meetings extensibility</span></span> | <span data-ttu-id="3346b-304">Microsoft Teams extensibilidad de reunión para pasar tokens.</span><span class="sxs-lookup"><span data-stu-id="3346b-304">Microsoft Teams meeting extensibility sample for passing tokens.</span></span> | [<span data-ttu-id="3346b-305">View</span><span class="sxs-lookup"><span data-stu-id="3346b-305">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [<span data-ttu-id="3346b-306">View</span><span class="sxs-lookup"><span data-stu-id="3346b-306">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| <span data-ttu-id="3346b-307">Bot de burbuja de contenido de reunión</span><span class="sxs-lookup"><span data-stu-id="3346b-307">Meeting content bubble bot</span></span> | <span data-ttu-id="3346b-308">Microsoft Teams de extensibilidad de reuniones para interactuar con el bot de burbujas de contenido en una reunión.</span><span class="sxs-lookup"><span data-stu-id="3346b-308">Microsoft Teams meeting extensibility sample for interacting with content bubble bot in a meeting.</span></span> | [<span data-ttu-id="3346b-309">View</span><span class="sxs-lookup"><span data-stu-id="3346b-309">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [<span data-ttu-id="3346b-310">View</span><span class="sxs-lookup"><span data-stu-id="3346b-310">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| <span data-ttu-id="3346b-311">MeetingSidePanel</span><span class="sxs-lookup"><span data-stu-id="3346b-311">Meeting meetingSidePanel</span></span> | <span data-ttu-id="3346b-312">Microsoft Teams extensibilidad de reuniones para interactuar con el panel lateral en la reunión.</span><span class="sxs-lookup"><span data-stu-id="3346b-312">Microsoft Teams meeting extensibility sample for interacting with the side panel in-meeting.</span></span> | [<span data-ttu-id="3346b-313">View</span><span class="sxs-lookup"><span data-stu-id="3346b-313">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [<span data-ttu-id="3346b-314">View</span><span class="sxs-lookup"><span data-stu-id="3346b-314">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|
| <span data-ttu-id="3346b-315">Ficha Detalles en reunión</span><span class="sxs-lookup"><span data-stu-id="3346b-315">Details Tab in Meeting</span></span> | <span data-ttu-id="3346b-316">Microsoft Teams de extensibilidad de reuniones para iterar con la pestaña Detalles en la reunión.</span><span class="sxs-lookup"><span data-stu-id="3346b-316">Microsoft Teams meeting extensibility sample for iteracting with Details Tab in-meeting.</span></span> | [<span data-ttu-id="3346b-317">View</span><span class="sxs-lookup"><span data-stu-id="3346b-317">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/csharp) | [<span data-ttu-id="3346b-318">View</span><span class="sxs-lookup"><span data-stu-id="3346b-318">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/nodejs)|

## <a name="see-also"></a><span data-ttu-id="3346b-319">Vea también</span><span class="sxs-lookup"><span data-stu-id="3346b-319">See also</span></span>

* [<span data-ttu-id="3346b-320">Directrices de diseño de cuadros de diálogo en la reunión</span><span class="sxs-lookup"><span data-stu-id="3346b-320">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [<span data-ttu-id="3346b-321">Teams de autenticación para pestañas</span><span class="sxs-lookup"><span data-stu-id="3346b-321">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)
* [<span data-ttu-id="3346b-322">Aplicaciones para Teams reuniones</span><span class="sxs-lookup"><span data-stu-id="3346b-322">Apps for Teams meetings</span></span>](teams-apps-in-meetings.md)

## <a name="next-step"></a><span data-ttu-id="3346b-323">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="3346b-323">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3346b-324">Habilitar y configurar las aplicaciones para Teams reuniones</span><span class="sxs-lookup"><span data-stu-id="3346b-324">Enable and configure your apps for Teams meetings</span></span>](enable-and-configure-your-app-for-teams-meetings.md)

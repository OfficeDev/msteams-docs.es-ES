---
title: Crear aplicaciones para reuniones de equipos
author: laujan
description: crear aplicaciones para reuniones de equipos
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: equipos aplicaciones reuniones usuario participante rol api
ms.openlocfilehash: 84d0f5564d7e8e6e34dde1f3d59cc6e7a68d3332
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565917"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="539c8-104">Crear aplicaciones para reuniones de Teams</span><span class="sxs-lookup"><span data-stu-id="539c8-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="539c8-105">Requisitos previos y consideraciones</span><span class="sxs-lookup"><span data-stu-id="539c8-105">Prerequisites and considerations</span></span>

<span data-ttu-id="539c8-106">Antes de crear aplicaciones para reuniones Teams, debe tener una comprensión de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="539c8-106">Before you create apps for Teams meetings, you must have an understanding of the following:</span></span>

* <span data-ttu-id="539c8-107">Debe tener conocimiento de cómo desarrollar aplicaciones Teams.</span><span class="sxs-lookup"><span data-stu-id="539c8-107">You must have knowledge of how to develop Teams apps.</span></span> <span data-ttu-id="539c8-108">Para obtener más información, consulte [Teams desarrollo de aplicaciones.](../overview.md)</span><span class="sxs-lookup"><span data-stu-id="539c8-108">For more information, see [Teams app development](../overview.md).</span></span>

* <span data-ttu-id="539c8-109">Debe actualizar el manifiesto de Teams aplicación para indicar que la aplicación está disponible para reuniones.</span><span class="sxs-lookup"><span data-stu-id="539c8-109">You must update the Teams app manifest to indicate that the app is available for meetings.</span></span> <span data-ttu-id="539c8-110">Para obtener más información, consulte [manifiesto de aplicación](#update-your-app-manifest).</span><span class="sxs-lookup"><span data-stu-id="539c8-110">For more information, see [app manifest](#update-your-app-manifest).</span></span>

* <span data-ttu-id="539c8-111">Para que la aplicación funcione en el ciclo de vida de la reunión como una pestaña, debe admitir pestañas configurables en el ámbito de groupchat.</span><span class="sxs-lookup"><span data-stu-id="539c8-111">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the groupchat scope.</span></span> <span data-ttu-id="539c8-112">Para obtener más información, vea [ámbito de groupchat](../resources/schema/manifest-schema.md#configurabletabs) y [cree una pestaña de grupo.](../build-your-first-app/build-channel-tab.md)</span><span class="sxs-lookup"><span data-stu-id="539c8-112">For more information, see [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md).</span></span>

* <span data-ttu-id="539c8-113">Debe cumplir con las directrices generales de diseño de pestañas Teams para escenarios previos y posteriores a la reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-113">You must adhere to general Teams tab design guidelines for pre- and post-meeting scenarios.</span></span> <span data-ttu-id="539c8-114">Para obtener experiencias durante las reuniones, consulte la pestaña en la reunión y las directrices de diseño del cuadro de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-114">For experiences during meetings, refer to the in-meeting tab and in-meeting dialog design guidelines.</span></span> <span data-ttu-id="539c8-115">Para obtener más información, consulte [directrices de diseño de pestañas Teams,](../tabs/design/tabs.md)directrices de diseño de [pestañas en la reunión](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) y directrices de diseño de cuadro de diálogo en [reunión.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)</span><span class="sxs-lookup"><span data-stu-id="539c8-115">For more information, see [Teams tab design guidelines](../tabs/design/tabs.md), [in-meeting tab design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) and [in-meeting dialog design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

* <span data-ttu-id="539c8-116">Debes admitir el `groupchat` ámbito para habilitar la aplicación en chats previos a la reunión y después de la reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-116">You must support the `groupchat` scope to enable your app in pre-meeting and post-meeting chats.</span></span> <span data-ttu-id="539c8-117">Con la experiencia de la aplicación previa a la reunión, puede encontrar y agregar aplicaciones de reunión y realizar tareas previas a la reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-117">With the pre-meeting app experience, you can find and add meeting apps and perform pre-meeting tasks.</span></span> <span data-ttu-id="539c8-118">Con la experiencia de la aplicación posterior a la reunión, puede ver los resultados de la reunión, como los resultados de la encuesta de encuestas o los comentarios.</span><span class="sxs-lookup"><span data-stu-id="539c8-118">With post-meeting app experience, you can view the results of the meeting, such as poll survey results or feedback.</span></span>

* <span data-ttu-id="539c8-119">Los parámetros de url de la API de reunión deben tener `meetingId` `userId` , y `tenantId` .</span><span class="sxs-lookup"><span data-stu-id="539c8-119">Meeting API URL parameters must have `meetingId`, `userId`, and `tenantId`.</span></span> <span data-ttu-id="539c8-120">Estos están disponibles como parte de la actividad de Teams SDK y bot de cliente.</span><span class="sxs-lookup"><span data-stu-id="539c8-120">These are available as part of the Teams client SDK and bot activity.</span></span> <span data-ttu-id="539c8-121">Además, se puede recuperar información confiable para el ID de usuario y el identificador de inquilino mediante [la autenticación de SSO de tabulación.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="539c8-121">In addition, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="539c8-122">La `GetParticipant` API debe tener un registro de bots y un identificador para generar tokens de autenticación.</span><span class="sxs-lookup"><span data-stu-id="539c8-122">The `GetParticipant` API must have a bot registration and ID to generate auth tokens.</span></span> <span data-ttu-id="539c8-123">Para obtener más información, consulte [registro e ID de bot.](../build-your-first-app/build-bot.md)</span><span class="sxs-lookup"><span data-stu-id="539c8-123">For more information, see [bot registration and ID](../build-your-first-app/build-bot.md).</span></span>

* <span data-ttu-id="539c8-124">Para que la aplicación se actualice en tiempo real, debe estar actualizada en función de las actividades de eventos de la reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-124">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="539c8-125">Estos eventos pueden estar dentro del cuadro de diálogo en la reunión y otras etapas a lo largo del ciclo de vida de la reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-125">These events can be within the in-meeting dialog box and other stages across the meeting lifecycle.</span></span> <span data-ttu-id="539c8-126">Para el cuadro de diálogo en la reunión, vea parámetro de finalización `bot Id` en `Notification Signal API` .</span><span class="sxs-lookup"><span data-stu-id="539c8-126">For the in-meeting dialog box, see completion `bot Id` parameter in `Notification Signal API`.</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="539c8-127">Referencia api de aplicaciones de reunión</span><span class="sxs-lookup"><span data-stu-id="539c8-127">Meeting apps API reference</span></span>

|<span data-ttu-id="539c8-128">API</span><span class="sxs-lookup"><span data-stu-id="539c8-128">API</span></span>|<span data-ttu-id="539c8-129">Descripción</span><span class="sxs-lookup"><span data-stu-id="539c8-129">Description</span></span>|<span data-ttu-id="539c8-130">Solicitud</span><span class="sxs-lookup"><span data-stu-id="539c8-130">Request</span></span>|<span data-ttu-id="539c8-131">Origen</span><span class="sxs-lookup"><span data-stu-id="539c8-131">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="539c8-132">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="539c8-132">**GetUserContext**</span></span>| <span data-ttu-id="539c8-133">Esta API le permite obtener información contextual para mostrar contenido relevante en una pestaña de Teams.</span><span class="sxs-lookup"><span data-stu-id="539c8-133">This API enables you to get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="539c8-134">_**microsoftTeams.getContext( ( ) => { /*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="539c8-134">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="539c8-135">MICROSOFT TEAMS SDK de cliente</span><span class="sxs-lookup"><span data-stu-id="539c8-135">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="539c8-136">**ObtenerParticipant**</span><span class="sxs-lookup"><span data-stu-id="539c8-136">**GetParticipant**</span></span>| <span data-ttu-id="539c8-137">Esta API permite a un bot obtener información de los participantes mediante el ID de reunión y el ID de participante.</span><span class="sxs-lookup"><span data-stu-id="539c8-137">This API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> |<span data-ttu-id="539c8-138">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="539c8-138">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="539c8-139">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="539c8-139">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="539c8-140">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="539c8-140">**NotificationSignal**</span></span> | <span data-ttu-id="539c8-141">Esta API le permite proporcionar señales de reunión que se entregan mediante la API de notificación de conversación existente para el chat de bot de usuario.</span><span class="sxs-lookup"><span data-stu-id="539c8-141">This API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="539c8-142">Le permite realizar una señal basada en la acción del usuario que muestra un cuadro de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-142">It allows you to signal based on user action that shows an in-meeting dialog box.</span></span> |<span data-ttu-id="539c8-143">**POST** _**/v3/conversaciones/{conversationId}/actividades**_</span><span class="sxs-lookup"><span data-stu-id="539c8-143">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="539c8-144">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="539c8-144">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="539c8-145">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="539c8-145">GetUserContext</span></span>

<span data-ttu-id="539c8-146">Para identificar y recuperar información contextual para el contenido de la pestaña, consulte [obtener contexto para la pestaña Teams](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). `meetingId`se utiliza mediante una pestaña cuando se ejecuta en el contexto de reunión y se agrega para la carga de respuesta.</span><span class="sxs-lookup"><span data-stu-id="539c8-146">To identify and retrieve contextual information for your tab content, see [get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). `meetingId` is used by a tab when running in the meeting context and is added for the response payload.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="539c8-147">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="539c8-147">GetParticipant API</span></span>

> [!NOTE]
> * <span data-ttu-id="539c8-148">No almacene en caché los roles de participante, ya que el organizador de la reunión puede cambiar un rol en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="539c8-148">Do not cache participant roles since the meeting organizer can change a role any time.</span></span>
> * <span data-ttu-id="539c8-149">Teams actualmente no admite grandes listas de distribución o tamaños de lista de más de 350 participantes para la `GetParticipant` API.</span><span class="sxs-lookup"><span data-stu-id="539c8-149">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="539c8-150">Parámetros de consulta</span><span class="sxs-lookup"><span data-stu-id="539c8-150">Query parameters</span></span>

|<span data-ttu-id="539c8-151">Valor</span><span class="sxs-lookup"><span data-stu-id="539c8-151">Value</span></span>|<span data-ttu-id="539c8-152">Tipo</span><span class="sxs-lookup"><span data-stu-id="539c8-152">Type</span></span>|<span data-ttu-id="539c8-153">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="539c8-153">Required</span></span>|<span data-ttu-id="539c8-154">Descripción</span><span class="sxs-lookup"><span data-stu-id="539c8-154">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="539c8-155">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="539c8-155">**meetingId**</span></span>| <span data-ttu-id="539c8-156">string</span><span class="sxs-lookup"><span data-stu-id="539c8-156">string</span></span> | <span data-ttu-id="539c8-157">Sí</span><span class="sxs-lookup"><span data-stu-id="539c8-157">Yes</span></span> | <span data-ttu-id="539c8-158">El identificador de reunión está disponible a través de Bot Invoke y Teams SDK de cliente.</span><span class="sxs-lookup"><span data-stu-id="539c8-158">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="539c8-159">**participantId**</span><span class="sxs-lookup"><span data-stu-id="539c8-159">**participantId**</span></span>| <span data-ttu-id="539c8-160">string</span><span class="sxs-lookup"><span data-stu-id="539c8-160">string</span></span> | <span data-ttu-id="539c8-161">Sí</span><span class="sxs-lookup"><span data-stu-id="539c8-161">Yes</span></span> | <span data-ttu-id="539c8-162">El ID de participante es el ID de usuario.</span><span class="sxs-lookup"><span data-stu-id="539c8-162">The participant ID is the user ID.</span></span> <span data-ttu-id="539c8-163">Está disponible en Tab SSO, Bot Invoke y Teams SDK de cliente.</span><span class="sxs-lookup"><span data-stu-id="539c8-163">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="539c8-164">Se recomienda obtener un ID de participante de la pestaña SSO.</span><span class="sxs-lookup"><span data-stu-id="539c8-164">It is recommended to get a participant ID from the Tab SSO.</span></span> |
|<span data-ttu-id="539c8-165">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="539c8-165">**tenantId**</span></span>| <span data-ttu-id="539c8-166">string</span><span class="sxs-lookup"><span data-stu-id="539c8-166">string</span></span> | <span data-ttu-id="539c8-167">Sí</span><span class="sxs-lookup"><span data-stu-id="539c8-167">Yes</span></span> | <span data-ttu-id="539c8-168">El identificador de inquilino es necesario para los usuarios de inquilino.</span><span class="sxs-lookup"><span data-stu-id="539c8-168">The tenant ID is required for the tenant users.</span></span> <span data-ttu-id="539c8-169">Está disponible en Tab SSO, Bot Invoke y Teams SDK de cliente.</span><span class="sxs-lookup"><span data-stu-id="539c8-169">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="539c8-170">Se recomienda obtener un identificador de inquilino de la pestaña SSO.</span><span class="sxs-lookup"><span data-stu-id="539c8-170">It is recommended to get a tenant ID from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="539c8-171">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="539c8-171">Example</span></span>

# <a name="c"></a>[<span data-ttu-id="539c8-172">C#</span><span class="sxs-lookup"><span data-stu-id="539c8-172">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  TeamsMeetingParticipant participant = GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
  TeamsChannelAccount member = participant.User;
  MeetingParticipantInfo meetingInfo = participant.Meeting;
  ConversationAccount conversation = participant.Conversation;

  await turnContext.SendActivityAsync(MessageFactory.Text($"The participant role is: {meetingInfo.Role}"), cancellationToken);
}

```

# <a name="javascript"></a>[<span data-ttu-id="539c8-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="539c8-173">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="539c8-174">JSON</span><span class="sxs-lookup"><span data-stu-id="539c8-174">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

* * *

<span data-ttu-id="539c8-175">El cuerpo de respuesta JSON de `GetParticipant` la API es:</span><span class="sxs-lookup"><span data-stu-id="539c8-175">The JSON response body for `GetParticipant` API is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="539c8-176">Códigos de respuesta</span><span class="sxs-lookup"><span data-stu-id="539c8-176">Response codes</span></span>

|<span data-ttu-id="539c8-177">Código de respuesta</span><span class="sxs-lookup"><span data-stu-id="539c8-177">Response code</span></span>|<span data-ttu-id="539c8-178">Descripción</span><span class="sxs-lookup"><span data-stu-id="539c8-178">Description</span></span>|
|---|---|
| <span data-ttu-id="539c8-179">**403**</span><span class="sxs-lookup"><span data-stu-id="539c8-179">**403**</span></span> | <span data-ttu-id="539c8-180">La aplicación no está permitida para obtener información del participante.</span><span class="sxs-lookup"><span data-stu-id="539c8-180">The app is not allowed to get participant information.</span></span> <span data-ttu-id="539c8-181">Esta es la respuesta de error más común y se desencadena si la aplicación no está instalada en la reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-181">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="539c8-182">Por ejemplo, si la aplicación está deshabilitada por el administrador del inquilino o se bloquea durante la migración al sitio en vivo.</span><span class="sxs-lookup"><span data-stu-id="539c8-182">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>|
| <span data-ttu-id="539c8-183">**200**</span><span class="sxs-lookup"><span data-stu-id="539c8-183">**200**</span></span> | <span data-ttu-id="539c8-184">La información del participante se recupera correctamente.</span><span class="sxs-lookup"><span data-stu-id="539c8-184">The participant information is successfully retrieved.</span></span>|
| <span data-ttu-id="539c8-185">**401**</span><span class="sxs-lookup"><span data-stu-id="539c8-185">**401**</span></span> | <span data-ttu-id="539c8-186">La aplicación responde con un token no válido.</span><span class="sxs-lookup"><span data-stu-id="539c8-186">The app responds with an invalid token.</span></span>|
| <span data-ttu-id="539c8-187">**404**</span><span class="sxs-lookup"><span data-stu-id="539c8-187">**404**</span></span> | <span data-ttu-id="539c8-188">La reunión ha expirado o no se puede encontrar a ningún participante.</span><span class="sxs-lookup"><span data-stu-id="539c8-188">The meeting has either expired or participant cannot be found.</span></span>|
| <span data-ttu-id="539c8-189">**500**</span><span class="sxs-lookup"><span data-stu-id="539c8-189">**500**</span></span> | <span data-ttu-id="539c8-190">La reunión ha expirado más de 60 días desde que terminó la reunión o el participante no tiene permisos basados en su rol.</span><span class="sxs-lookup"><span data-stu-id="539c8-190">The meeting has either expired more than 60 days since the meeting ended or the participant does not have permissions based on their role.</span></span>|

### <a name="notificationsignal-api"></a><span data-ttu-id="539c8-191">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="539c8-191">NotificationSignal API</span></span>

<span data-ttu-id="539c8-192">Todos los usuarios de una reunión reciben las notificaciones enviadas a través de la `NotificationSignal` API.</span><span class="sxs-lookup"><span data-stu-id="539c8-192">All users in a meeting receive the notifications sent through the `NotificationSignal` API.</span></span>

> [!NOTE]
> * <span data-ttu-id="539c8-193">Cuando se invoca un cuadro de diálogo en la reunión, el contenido se presenta como un mensaje de chat.</span><span class="sxs-lookup"><span data-stu-id="539c8-193">When an in-meeting dialog box is invoked, the content is presented as a chat message.</span></span>
> * <span data-ttu-id="539c8-194">Actualmente, no se admite el envío de notificaciones dirigidas.</span><span class="sxs-lookup"><span data-stu-id="539c8-194">Currently, sending targeted notifications is not supported.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="539c8-195">Parámetros de consulta</span><span class="sxs-lookup"><span data-stu-id="539c8-195">Query parameters</span></span>

|<span data-ttu-id="539c8-196">Valor</span><span class="sxs-lookup"><span data-stu-id="539c8-196">Value</span></span>|<span data-ttu-id="539c8-197">Tipo</span><span class="sxs-lookup"><span data-stu-id="539c8-197">Type</span></span>|<span data-ttu-id="539c8-198">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="539c8-198">Required</span></span>|<span data-ttu-id="539c8-199">Descripción</span><span class="sxs-lookup"><span data-stu-id="539c8-199">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="539c8-200">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="539c8-200">**conversationId**</span></span>| <span data-ttu-id="539c8-201">string</span><span class="sxs-lookup"><span data-stu-id="539c8-201">string</span></span> | <span data-ttu-id="539c8-202">Sí</span><span class="sxs-lookup"><span data-stu-id="539c8-202">Yes</span></span> | <span data-ttu-id="539c8-203">El identificador de conversación está disponible como parte de la invocación de bot.</span><span class="sxs-lookup"><span data-stu-id="539c8-203">The conversation identifier is available as part of bot invoke.</span></span> |

#### <a name="example"></a><span data-ttu-id="539c8-204">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="539c8-204">Example</span></span>

<span data-ttu-id="539c8-205">Se `Bot ID` declara en el manifiesto y el bot recibe un objeto de resultado.</span><span class="sxs-lookup"><span data-stu-id="539c8-205">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span>

> [!NOTE]
> * <span data-ttu-id="539c8-206">El `completionBotId` parámetro de la es opcional en el ejemplo de carga útil `externalResourceUrl` solicitado.</span><span class="sxs-lookup"><span data-stu-id="539c8-206">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="539c8-207">`Bot ID` se declara en el manifiesto y el bot recibe un objeto de resultado.</span><span class="sxs-lookup"><span data-stu-id="539c8-207">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="539c8-208">Los `externalResourceUrl` parámetros de anchura y altura deben estar en píxeles.</span><span class="sxs-lookup"><span data-stu-id="539c8-208">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="539c8-209">Para asegurarse de que las dimensiones están dentro de los límites [permitidos,](design/designing-apps-in-meetings.md)consulte las directrices de diseño .</span><span class="sxs-lookup"><span data-stu-id="539c8-209">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="539c8-210">La dirección URL es la página cargada como una `<iframe>` en el cuadro de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-210">The URL is the page loaded as an `<iframe>` in the in-meeting dialog box.</span></span> <span data-ttu-id="539c8-211">El dominio debe estar en la matriz de la aplicación en el manifiesto de `validDomains` la aplicación.</span><span class="sxs-lookup"><span data-stu-id="539c8-211">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

# <a name="c"></a>[<span data-ttu-id="539c8-212">C#</span><span class="sxs-lookup"><span data-stu-id="539c8-212">C#</span></span>](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");

activity.ChannelData = new TeamsChannelData
  {
    Notification = new NotificationInfo()
                    {
                        AlertInMeeting = true,
                        ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
                    }
  };
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[<span data-ttu-id="539c8-213">JavaScript</span><span class="sxs-lookup"><span data-stu-id="539c8-213">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="539c8-214">JSON</span><span class="sxs-lookup"><span data-stu-id="539c8-214">JSON</span></span>](#tab/json)

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

* * *

#### <a name="response-codes"></a><span data-ttu-id="539c8-215">Códigos de respuesta</span><span class="sxs-lookup"><span data-stu-id="539c8-215">Response codes</span></span>

|<span data-ttu-id="539c8-216">Código de respuesta</span><span class="sxs-lookup"><span data-stu-id="539c8-216">Response code</span></span>|<span data-ttu-id="539c8-217">Descripción</span><span class="sxs-lookup"><span data-stu-id="539c8-217">Description</span></span>|
|---|---|
| <span data-ttu-id="539c8-218">**201**</span><span class="sxs-lookup"><span data-stu-id="539c8-218">**201**</span></span> | <span data-ttu-id="539c8-219">La actividad con señal se envía correctamente.</span><span class="sxs-lookup"><span data-stu-id="539c8-219">The activity with signal is successfully sent.</span></span> |
| <span data-ttu-id="539c8-220">**401**</span><span class="sxs-lookup"><span data-stu-id="539c8-220">**401**</span></span> | <span data-ttu-id="539c8-221">La aplicación responde con un token no válido.</span><span class="sxs-lookup"><span data-stu-id="539c8-221">The app responds with an invalid token.</span></span> |
| <span data-ttu-id="539c8-222">**403**</span><span class="sxs-lookup"><span data-stu-id="539c8-222">**403**</span></span> | <span data-ttu-id="539c8-223">La aplicación no puede enviar la señal.</span><span class="sxs-lookup"><span data-stu-id="539c8-223">The app is unable to send the signal.</span></span> <span data-ttu-id="539c8-224">Esto puede suceder debido a varias razones, como que el administrador del inquilino deshabilita la aplicación, la aplicación se bloquea durante la migración del sitio en vivo, etc.</span><span class="sxs-lookup"><span data-stu-id="539c8-224">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="539c8-225">En este caso, la carga útil contiene un mensaje de error detallado.</span><span class="sxs-lookup"><span data-stu-id="539c8-225">In this case, the payload contains a detailed error message.</span></span> |
| <span data-ttu-id="539c8-226">**404**</span><span class="sxs-lookup"><span data-stu-id="539c8-226">**404**</span></span> | <span data-ttu-id="539c8-227">El chat de la reunión no existe.</span><span class="sxs-lookup"><span data-stu-id="539c8-227">The meeting chat does not exist.</span></span> |

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="539c8-228">Habilite la aplicación para reuniones Teams</span><span class="sxs-lookup"><span data-stu-id="539c8-228">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="539c8-229">Actualiza el manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="539c8-229">Update your app manifest</span></span>

<span data-ttu-id="539c8-230">Las funcionalidades de la aplicación de reuniones se declaran en el manifiesto de la aplicación mediante el `configurableTabs` `scopes` archivo y las `context` matrices.</span><span class="sxs-lookup"><span data-stu-id="539c8-230">The meetings app capabilities are declared in your app manifest using the `configurableTabs`, `scopes`, and `context` arrays.</span></span> <span data-ttu-id="539c8-231">El ámbito define a quién y el contexto definen dónde está disponible la aplicación.</span><span class="sxs-lookup"><span data-stu-id="539c8-231">Scope defines to whom and context defines where your app is available.</span></span>

> [!NOTE]
> <span data-ttu-id="539c8-232">Intente actualizar el manifiesto de la aplicación con el [esquema de manifiesto.](../resources/schema/manifest-schema-dev-preview.md)</span><span class="sxs-lookup"><span data-stu-id="539c8-232">Try updating your app manifest with the [manifest schema](../resources/schema/manifest-schema-dev-preview.md).</span></span>
> <span data-ttu-id="539c8-233">Las aplicaciones en las reuniones necesitan ámbito *de groupchat.*</span><span class="sxs-lookup"><span data-stu-id="539c8-233">Apps in meetings need *groupchat* scope.</span></span> <span data-ttu-id="539c8-234">El ámbito del *equipo* solo funciona para pestañas en canales.</span><span class="sxs-lookup"><span data-stu-id="539c8-234">The *team* scope works for tabs in channels only.</span></span>

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
> <span data-ttu-id="539c8-235">`meetingStage` actualmente solo está disponible en la versión preliminar del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="539c8-235">`meetingStage` is currently available in developer preview only.</span></span>

### <a name="context-property"></a><span data-ttu-id="539c8-236">Propiedad context</span><span class="sxs-lookup"><span data-stu-id="539c8-236">Context property</span></span>

<span data-ttu-id="539c8-237">La pestaña `context` y las propiedades le permiten determinar dónde debe aparecer la `scopes` aplicación.</span><span class="sxs-lookup"><span data-stu-id="539c8-237">The tab `context` and `scopes` properties enable you to determine where your app must appear.</span></span> <span data-ttu-id="539c8-238">Las pestañas del ámbito o de la `team` extensión pueden tener más de un `groupchat` contexto.</span><span class="sxs-lookup"><span data-stu-id="539c8-238">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="539c8-239">A continuación se presentan los valores de la propiedad desde la `context` que puede utilizar todos o algunos de los valores:</span><span class="sxs-lookup"><span data-stu-id="539c8-239">Following are the values for the `context` property from which you can use all or some of the values:</span></span>

|<span data-ttu-id="539c8-240">Valor</span><span class="sxs-lookup"><span data-stu-id="539c8-240">Value</span></span>|<span data-ttu-id="539c8-241">Descripción</span><span class="sxs-lookup"><span data-stu-id="539c8-241">Description</span></span>|
|---|---|
| <span data-ttu-id="539c8-242">**channelTab**</span><span class="sxs-lookup"><span data-stu-id="539c8-242">**channelTab**</span></span> | <span data-ttu-id="539c8-243">Una pestaña en el encabezado de un canal de equipo.</span><span class="sxs-lookup"><span data-stu-id="539c8-243">A tab in the header of a team channel.</span></span> |
| <span data-ttu-id="539c8-244">**privateChatTab**</span><span class="sxs-lookup"><span data-stu-id="539c8-244">**privateChatTab**</span></span> | <span data-ttu-id="539c8-245">Pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios que no están en el contexto de un equipo o una reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-245">A tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span> |
| <span data-ttu-id="539c8-246">**reuniónChatTab**</span><span class="sxs-lookup"><span data-stu-id="539c8-246">**meetingChatTab**</span></span> | <span data-ttu-id="539c8-247">Pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios en el contexto de una reunión programada.</span><span class="sxs-lookup"><span data-stu-id="539c8-247">A tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span> |
| <span data-ttu-id="539c8-248">**reuniónDetailsTab**</span><span class="sxs-lookup"><span data-stu-id="539c8-248">**meetingDetailsTab**</span></span> | <span data-ttu-id="539c8-249">Una pestaña en el encabezado de la vista de detalles de la reunión del calendario.</span><span class="sxs-lookup"><span data-stu-id="539c8-249">A tab in the header of the meeting details view of the calendar.</span></span> |
| <span data-ttu-id="539c8-250">**reuniónSidePanel**</span><span class="sxs-lookup"><span data-stu-id="539c8-250">**meetingSidePanel**</span></span> | <span data-ttu-id="539c8-251">Se abrió un panel en la reunión a través de la barra unificada (U-bar).</span><span class="sxs-lookup"><span data-stu-id="539c8-251">An in-meeting panel opened via the unified bar (U-bar).</span></span> |
| <span data-ttu-id="539c8-252">**reuniónStage**</span><span class="sxs-lookup"><span data-stu-id="539c8-252">**meetingStage**</span></span> | <span data-ttu-id="539c8-253">Una aplicación del sidepanel se puede compartir en la etapa de reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-253">An app from the sidepanel can be shared to the meeting stage.</span></span> |

> [!NOTE]
> <span data-ttu-id="539c8-254">`Context` propiedad actualmente no es compatible con los clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="539c8-254">`Context` property is currently not supported on mobile clients.</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="539c8-255">Configure la aplicación para escenarios de reunión</span><span class="sxs-lookup"><span data-stu-id="539c8-255">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="539c8-256">Para que la aplicación esté visible en la galería de pestañas, debe admitir pestañas configurables y el ámbito de chat de grupo.</span><span class="sxs-lookup"><span data-stu-id="539c8-256">For your app to be visible in the tab gallery it must support configurable tabs and the group chat scope.</span></span>
> * <span data-ttu-id="539c8-257">Los clientes móviles solo admiten pestañas en etapas previas y posteriores a la reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-257">Mobile clients support tabs only in pre and post meeting stages.</span></span>
> * <span data-ttu-id="539c8-258">Las experiencias en la reunión que se encuentran en el cuadro de diálogo y la pestaña en la reunión actualmente no se admiten en los clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="539c8-258">The in-meeting experiences that is in-meeting dialog box and tab is currently not supported on mobile clients.</span></span> <span data-ttu-id="539c8-259">Para obtener más información, consulte [instrucciones para pestañas en dispositivos móviles](../tabs/design/tabs-mobile.md) al crear las pestañas para dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="539c8-259">For more information, see [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span>

### <a name="before-a-meeting"></a><span data-ttu-id="539c8-260">Antes de una reunión</span><span class="sxs-lookup"><span data-stu-id="539c8-260">Before a meeting</span></span>

<span data-ttu-id="539c8-261">Antes de una reunión, los usuarios pueden agregar pestañas, bots y extensiones de mensajería a una reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-261">Before a meeting, users can add tabs, bots and messaging extensions to a meeting.</span></span> <span data-ttu-id="539c8-262">Los usuarios con roles de organizador y presentador pueden agregar pestañas a una reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-262">Users with organizer and presenter roles can add tabs to a meeting.</span></span>

<span data-ttu-id="539c8-263">**Para agregar una pestaña a una reunión**</span><span class="sxs-lookup"><span data-stu-id="539c8-263">**To add a tab to a meeting**</span></span>

1. <span data-ttu-id="539c8-264">En tu calendario, selecciona una reunión a la que quieras añadir una pestaña.</span><span class="sxs-lookup"><span data-stu-id="539c8-264">In your calendar, select a meeting to which you want to add a tab.</span></span>
1. <span data-ttu-id="539c8-265">Seleccione la pestaña **Detalles** y seleccione más</span><span class="sxs-lookup"><span data-stu-id="539c8-265">Select the **Details** tab and select plus</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="539c8-266">.</span><span class="sxs-lookup"><span data-stu-id="539c8-266">.</span></span> <span data-ttu-id="539c8-267">Aparece la galería de pestañas.</span><span class="sxs-lookup"><span data-stu-id="539c8-267">The tab gallery appears.</span></span>

    ![Experiencia previa a la reunión](../assets/images/apps-in-meetings/PreMeeting.png)

1. <span data-ttu-id="539c8-269">En la galería de pestañas, seleccione la aplicación que desea agregar y siga los pasos necesarios.</span><span class="sxs-lookup"><span data-stu-id="539c8-269">In the tab gallery, select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="539c8-270">La aplicación se instala como una pestaña.</span><span class="sxs-lookup"><span data-stu-id="539c8-270">The app is installed as a tab.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="539c8-271">Actualmente, en la pestaña reuniones, no se admiten los detalles de la reunión ni la información de los participantes.</span><span class="sxs-lookup"><span data-stu-id="539c8-271">Currently, in meetings tab, getting meeting details and participant information is not supported.</span></span>

<span data-ttu-id="539c8-272">**Para agregar una extensión de mensajería a una reunión**</span><span class="sxs-lookup"><span data-stu-id="539c8-272">**To add a messaging extension to a meeting**</span></span>

1. <span data-ttu-id="539c8-273">Seleccione los puntos suspensivos o el menú de desbordamiento &#x25CF;&#x25CF;&#x25CF; ubicado en el área de mensaje de composición en el chat.</span><span class="sxs-lookup"><span data-stu-id="539c8-273">Select the ellipses or overflow menu &#x25CF;&#x25CF;&#x25CF; located in the compose message area in the chat.</span></span>
1. <span data-ttu-id="539c8-274">Seleccione la aplicación que desea agregar y siga los pasos necesarios.</span><span class="sxs-lookup"><span data-stu-id="539c8-274">Select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="539c8-275">La aplicación se instala como una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="539c8-275">The app is installed as a messaging extension.</span></span>

<span data-ttu-id="539c8-276">**Para agregar un bot a una reunión**</span><span class="sxs-lookup"><span data-stu-id="539c8-276">**To add a bot to a meeting**</span></span>

<span data-ttu-id="539c8-277">En un chat de reunión, escriba la **@** clave y seleccione Obtener **bots**.</span><span class="sxs-lookup"><span data-stu-id="539c8-277">In a meeting chat enter the **@** key and select **Get bots**.</span></span>

> [!NOTE]
> * <span data-ttu-id="539c8-278">La identidad del usuario debe confirmarse mediante [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="539c8-278">The user identity must be confirmed using [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="539c8-279">Después de la autenticación, la aplicación puede recuperar el rol de usuario mediante la `GetParticipant` API.</span><span class="sxs-lookup"><span data-stu-id="539c8-279">After authentication, the app can retrieve the user role using the `GetParticipant` API.</span></span>
> * <span data-ttu-id="539c8-280">En función del rol de usuario, la aplicación tiene la capacidad de proporcionar experiencias específicas de roles.</span><span class="sxs-lookup"><span data-stu-id="539c8-280">Based on the user role, the app has the capability to provide role specific experiences.</span></span> <span data-ttu-id="539c8-281">Por ejemplo, una aplicación de sondeo solo permite a los organizadores y presentadores crear una nueva encuesta.</span><span class="sxs-lookup"><span data-stu-id="539c8-281">For example, a polling app allows only organizers and presenters to create a new poll.</span></span>
> * <span data-ttu-id="539c8-282">Las asignaciones de roles se pueden cambiar mientras se está celebrando una reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-282">Role assignments can be changed while a meeting is in progress.</span></span> <span data-ttu-id="539c8-283">Para obtener más información, consulte [roles en una reunión Teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span><span class="sxs-lookup"><span data-stu-id="539c8-283">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

### <a name="during-a-meeting"></a><span data-ttu-id="539c8-284">Durante una reunión</span><span class="sxs-lookup"><span data-stu-id="539c8-284">During a meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="539c8-285">sidePanel</span><span class="sxs-lookup"><span data-stu-id="539c8-285">sidePanel</span></span>

<span data-ttu-id="539c8-286">Con sidePanel, puede personalizar experiencias en una reunión que permitan a los organizadores y presentadores tener diferentes conjunto de vistas y acciones.</span><span class="sxs-lookup"><span data-stu-id="539c8-286">With the sidePanel, you can customize experiences in a meeting that enable organizers and presenters to have different set of views and actions.</span></span> <span data-ttu-id="539c8-287">En el manifiesto de la aplicación, debe agregar sidePanel a la matriz de contexto.</span><span class="sxs-lookup"><span data-stu-id="539c8-287">In your app manifest, you must add sidePanel to the context array.</span></span> <span data-ttu-id="539c8-288">En la reunión y en todos los escenarios, la aplicación se representa en una pestaña en la reunión que tiene 320 píxeles de ancho.</span><span class="sxs-lookup"><span data-stu-id="539c8-288">In the meeting and in all scenarios, the app is rendered in an in-meeting tab that is 320 pixels in width.</span></span> <span data-ttu-id="539c8-289">Para obtener más información, consulte [interfaz FrameContext](/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
).</span><span class="sxs-lookup"><span data-stu-id="539c8-289">For more information, see [FrameContext interface](/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
).</span></span>

<span data-ttu-id="539c8-290">Para usar la `userContext` API para enrutar las solicitudes en consecuencia, consulte [Teams SDK](../tabs/how-to/access-teams-context.md#user-context).</span><span class="sxs-lookup"><span data-stu-id="539c8-290">To use the `userContext` API to route requests accordingly, see [Teams SDK](../tabs/how-to/access-teams-context.md#user-context).</span></span> <span data-ttu-id="539c8-291">Consulte [Teams flujo de autenticación para las pestañas](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="539c8-291">See [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="539c8-292">El flujo de autenticación para las pestañas es muy similar al flujo de autenticación para los sitios web.</span><span class="sxs-lookup"><span data-stu-id="539c8-292">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="539c8-293">Así que las pestañas pueden usar OAuth 2.0 directamente.</span><span class="sxs-lookup"><span data-stu-id="539c8-293">So tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="539c8-294">Consulte, [Plataforma de identidad de Microsoft y flujo de código de autorización de OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span><span class="sxs-lookup"><span data-stu-id="539c8-294">See, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="539c8-295">La extensión de mensajería funciona según lo esperado cuando un usuario está en una vista en la reunión y el usuario puede publicar tarjetas de extensión de mensaje de composición.</span><span class="sxs-lookup"><span data-stu-id="539c8-295">Messaging extension works as expected when a user is in an in-meeting view and the user can post compose message extension cards.</span></span> <span data-ttu-id="539c8-296">AppName in-meeting es una información sobre herramientas que indica el nombre de la aplicación en la barra en U de reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-296">AppName in-meeting is a tooltip that states the app name in-meeting U-bar.</span></span>

> [!NOTE]
> <span data-ttu-id="539c8-297">Utilice la versión 1.7.0 o superior de [Teams SDK,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)ya que las versiones anteriores no admiten el panel lateral.</span><span class="sxs-lookup"><span data-stu-id="539c8-297">Use version 1.7.0 or higher of [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), as versions prior to it do not support the side panel.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="539c8-298">Diálogo en la reunión</span><span class="sxs-lookup"><span data-stu-id="539c8-298">In-meeting dialog</span></span>

<span data-ttu-id="539c8-299">El cuadro de diálogo en la reunión se puede utilizar para atraer a los participantes durante la reunión y recopilar información o comentarios durante la reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-299">The in-meeting dialog box can be used to engage participants during the meeting and collect information or feedback during the meeting.</span></span> <span data-ttu-id="539c8-300">Utilice la [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API para indicar que se debe desencadenar una notificación de burbujas.</span><span class="sxs-lookup"><span data-stu-id="539c8-300">Use the [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification must be triggered.</span></span> <span data-ttu-id="539c8-301">Como parte de la carga de solicitud de notificación, incluya la dirección URL donde se hospeda el contenido que se va a mostrar.</span><span class="sxs-lookup"><span data-stu-id="539c8-301">As part of the notification request payload, include the URL where the content to be shown is hosted.</span></span>

<span data-ttu-id="539c8-302">El cuadro de diálogo en la reunión no debe usar el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="539c8-302">In-meeting dialog must not use task module.</span></span> <span data-ttu-id="539c8-303">El módulo de tareas no se invoca en un chat de reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-303">Task module is not invoked in a meeting chat.</span></span> <span data-ttu-id="539c8-304">Se utiliza una dirección URL de recursos externos para mostrar la burbuja de contenido en una reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-304">An external resource URL is used to display content bubble in a meeting.</span></span> <span data-ttu-id="539c8-305">Puede utilizar el `submitTask` método para enviar datos en un chat de reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-305">You can use the `submitTask` method to submit data in a meeting chat.</span></span>

> [!NOTE]
> * <span data-ttu-id="539c8-306">Debe invocar la función [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) para descartarla automáticamente después de que un usuario realice una acción en la vista web.</span><span class="sxs-lookup"><span data-stu-id="539c8-306">You must invoke the [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to dismiss automatically after a user takes an action in the web-view.</span></span> <span data-ttu-id="539c8-307">Este es un requisito para el envío de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="539c8-307">This is a requirement for app submission.</span></span> <span data-ttu-id="539c8-308">Para obtener más información, consulte [Teams módulo de tareas del SDK](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="539c8-308">For more information, see [Teams SDK task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
> * <span data-ttu-id="539c8-309">Si desea que la aplicación admita usuarios anónimos, la carga inicial de la solicitud de invocación debe basarse en los `from.id` metadatos de solicitud en el objeto, no en los metadatos de la `from` `from.aadObjectId` solicitud.</span><span class="sxs-lookup"><span data-stu-id="539c8-309">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id` request metadata in the `from` object, not the `from.aadObjectId` request metadata.</span></span> <span data-ttu-id="539c8-310">`from.id`es el ID de usuario y `from.aadObjectId` es el ID de Azure Active Directory (AAD) del usuario.</span><span class="sxs-lookup"><span data-stu-id="539c8-310">`from.id` is the user ID and `from.aadObjectId` is the Azure Active Directory (AAD) ID of the user.</span></span> <span data-ttu-id="539c8-311">Para obtener más información, consulte [uso de módulos de tareas en pestañas](../task-modules-and-cards/task-modules/task-modules-tabs.md) y cree y envíe el módulo de [tareas.](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)</span><span class="sxs-lookup"><span data-stu-id="539c8-311">For more information, see [using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

#### <a name="share-to-stage"></a><span data-ttu-id="539c8-312">Compartir al escenario</span><span class="sxs-lookup"><span data-stu-id="539c8-312">Share to stage</span></span> 

> [!NOTE]
> * <span data-ttu-id="539c8-313">Esta funcionalidad solo está disponible actualmente en la versión preliminar del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="539c8-313">This capability is currently available in developer preview only.</span></span>
> * <span data-ttu-id="539c8-314">Para usar esta característica, la aplicación debe admitir un sidepanel en la reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-314">To use this feature, the app must support an in-meeting sidepanel.</span></span>


<span data-ttu-id="539c8-315">Esta funcionalidad ofrece a los desarrolladores la capacidad de compartir una aplicación en la fase de reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-315">This capability gives developers the ability to share an app to the meeting stage.</span></span> <span data-ttu-id="539c8-316">Al permitir compartir en la etapa de reunión, los participantes de la reunión pueden colaborar en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="539c8-316">By enabling share to the meeting stage, meeting participants can collaborate in real-time.</span></span> 

<span data-ttu-id="539c8-317">El contexto necesario está `meetingStage` en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="539c8-317">The required context is `meetingStage` in the app manifest.</span></span> <span data-ttu-id="539c8-318">Un requisito previo para esto es tener el `meetingSidePanel` contexto.</span><span class="sxs-lookup"><span data-stu-id="539c8-318">A prerequisite for this is to have the `meetingSidePanel` context.</span></span> <span data-ttu-id="539c8-319">Esto habilita el botón **Compartir** en el sidepanel como se despecita en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="539c8-319">This enables the **Share** button in the sidepanel as depecited in the following image:</span></span>

  ![experiencia share_to_stage_during_meeting](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

<span data-ttu-id="539c8-321">El cambio de manifiesto que se necesita para habilitar esta funcionalidad es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="539c8-321">The manifest change that is needed to enable this capability is as follows:</span></span> 

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



### <a name="after-a-meeting"></a><span data-ttu-id="539c8-322">Después de una reunión</span><span class="sxs-lookup"><span data-stu-id="539c8-322">After a meeting</span></span>

<span data-ttu-id="539c8-323">Las configuraciones posteriores a la reunión y a la reunión previa son equivalentes.</span><span class="sxs-lookup"><span data-stu-id="539c8-323">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="code-sample"></a><span data-ttu-id="539c8-324">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="539c8-324">Code sample</span></span>

|<span data-ttu-id="539c8-325">Nombre de la muestra</span><span class="sxs-lookup"><span data-stu-id="539c8-325">Sample name</span></span> | <span data-ttu-id="539c8-326">Descripción</span><span class="sxs-lookup"><span data-stu-id="539c8-326">Description</span></span> | <span data-ttu-id="539c8-327">.NET</span><span class="sxs-lookup"><span data-stu-id="539c8-327">.NET</span></span> | <span data-ttu-id="539c8-328">Node.js</span><span class="sxs-lookup"><span data-stu-id="539c8-328">Node.js</span></span> |
|----------------|-----------------|--------------|--------------|
| <span data-ttu-id="539c8-329">Extensibilidad de las reuniones</span><span class="sxs-lookup"><span data-stu-id="539c8-329">Meetings extensibility</span></span> | <span data-ttu-id="539c8-330">Microsoft Teams ejemplo de extensibilidad de reuniones para pasar tokens.</span><span class="sxs-lookup"><span data-stu-id="539c8-330">Microsoft Teams meeting extensibility sample for passing tokens.</span></span> | [<span data-ttu-id="539c8-331">View</span><span class="sxs-lookup"><span data-stu-id="539c8-331">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [<span data-ttu-id="539c8-332">View</span><span class="sxs-lookup"><span data-stu-id="539c8-332">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| <span data-ttu-id="539c8-333">Bot de burbuja de contenido de reunión</span><span class="sxs-lookup"><span data-stu-id="539c8-333">Meeting content bubble bot</span></span> | <span data-ttu-id="539c8-334">Microsoft Teams ejemplo de extensibilidad de reunión para interactuar con el bot de burbuja de contenido en una reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-334">Microsoft Teams meeting extensibility sample for interacting with content bubble bot in a meeting.</span></span> | [<span data-ttu-id="539c8-335">View</span><span class="sxs-lookup"><span data-stu-id="539c8-335">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [<span data-ttu-id="539c8-336">View</span><span class="sxs-lookup"><span data-stu-id="539c8-336">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| <span data-ttu-id="539c8-337">Reunión SidePanel</span><span class="sxs-lookup"><span data-stu-id="539c8-337">Meeting SidePanel</span></span> | <span data-ttu-id="539c8-338">Microsoft Teams ejemplo de extensibilidad de reuniones para su iteración con el panel lateral en la reunión.</span><span class="sxs-lookup"><span data-stu-id="539c8-338">Microsoft Teams meeting extensibility sample for iteracting with the side panel in-meeting.</span></span> | [<span data-ttu-id="539c8-339">View</span><span class="sxs-lookup"><span data-stu-id="539c8-339">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |

## <a name="see-also"></a><span data-ttu-id="539c8-340">Vea también</span><span class="sxs-lookup"><span data-stu-id="539c8-340">See also</span></span>

* [<span data-ttu-id="539c8-341">Directrices de diseño de diálogos en la reunión</span><span class="sxs-lookup"><span data-stu-id="539c8-341">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [<span data-ttu-id="539c8-342">Teams flujo de autenticación para pestañas</span><span class="sxs-lookup"><span data-stu-id="539c8-342">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)

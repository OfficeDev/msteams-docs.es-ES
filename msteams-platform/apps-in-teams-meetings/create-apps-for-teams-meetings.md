---
title: Crear aplicaciones para reuniones de equipos
author: laujan
description: crear aplicaciones para reuniones de teams
ms.topic: conceptual
ms.author: lajanuar
keywords: API de roles de participantes de reuniones de aplicaciones de teams
ms.openlocfilehash: ba00a2dc78cefb167f1bef8507f32dad5e38452c
ms.sourcegitcommit: e78c9f51c4538212c53bb6c6a45a09d994896f09
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/05/2021
ms.locfileid: "51585851"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="1fe6e-104">Crear aplicaciones para reuniones de Teams</span><span class="sxs-lookup"><span data-stu-id="1fe6e-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="1fe6e-105">Requisitos previos y consideraciones</span><span class="sxs-lookup"><span data-stu-id="1fe6e-105">Prerequisites and considerations</span></span>

<span data-ttu-id="1fe6e-106">Antes de crear aplicaciones para reuniones de Teams, debes comprender lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1fe6e-106">Before you create apps for Teams meetings, you must have an understanding of the following:</span></span>

* <span data-ttu-id="1fe6e-107">Debes tener conocimientos sobre cómo desarrollar aplicaciones de Teams.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-107">You must have knowledge of how to develop Teams apps.</span></span> <span data-ttu-id="1fe6e-108">Para obtener más información, consulta [Desarrollo de aplicaciones de Teams.](../overview.md)</span><span class="sxs-lookup"><span data-stu-id="1fe6e-108">For more information, see [Teams app development](../overview.md).</span></span>

* <span data-ttu-id="1fe6e-109">Debes actualizar el manifiesto de la aplicación de Teams para indicar que la aplicación está disponible para reuniones.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-109">You must update the Teams app manifest to indicate that the app is available for meetings.</span></span> <span data-ttu-id="1fe6e-110">Para obtener más información, consulta [manifiesto de la aplicación](#update-your-app-manifest).</span><span class="sxs-lookup"><span data-stu-id="1fe6e-110">For more information, see [app manifest](#update-your-app-manifest).</span></span>

* <span data-ttu-id="1fe6e-111">Para que la aplicación funcione en el ciclo de vida de la reunión como una pestaña, debe admitir pestañas configurables en el ámbito de groupchat.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-111">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the groupchat scope.</span></span> <span data-ttu-id="1fe6e-112">Para obtener más información, [vea groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) y [build a group tab](../build-your-first-app/build-channel-tab.md).</span><span class="sxs-lookup"><span data-stu-id="1fe6e-112">For more information, see [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md).</span></span>

* <span data-ttu-id="1fe6e-113">Debe cumplir las directrices generales de diseño de pestañas de Teams para escenarios previos y posteriores a la reunión.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-113">You must adhere to general Teams tab design guidelines for pre- and post-meeting scenarios.</span></span> <span data-ttu-id="1fe6e-114">Para obtener experiencias durante las reuniones, consulte las directrices de diseño de la pestaña en la reunión y del cuadro de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-114">For experiences during meetings, refer to the in-meeting tab and in-meeting dialog design guidelines.</span></span> <span data-ttu-id="1fe6e-115">Para obtener más información, vea Directrices de diseño [de pestañas](../tabs/design/tabs.md)de Teams, directrices de diseño de [pestañas](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) en la reunión y directrices de diseño de [cuadros de diálogo en la reunión.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)</span><span class="sxs-lookup"><span data-stu-id="1fe6e-115">For more information, see [Teams tab design guidelines](../tabs/design/tabs.md), [in-meeting tab design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) and [in-meeting dialog design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

* <span data-ttu-id="1fe6e-116">Debes admitir el ámbito para habilitar la aplicación en `groupchat` chats previos y posteriores a la reunión.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-116">You must support the `groupchat` scope to enable your app in pre-meeting and post-meeting chats.</span></span> <span data-ttu-id="1fe6e-117">Con la experiencia de la aplicación previa a la reunión, puedes encontrar y agregar aplicaciones de reunión y realizar tareas previas a la reunión.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-117">With the pre-meeting app experience, you can find and add meeting apps and perform pre-meeting tasks.</span></span> <span data-ttu-id="1fe6e-118">Con la experiencia de la aplicación posterior a la reunión, puedes ver los resultados de la reunión, como los resultados de encuestas o los comentarios.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-118">With post-meeting app experience, you can view the results of the meeting, such as poll survey results or feedback.</span></span>

* <span data-ttu-id="1fe6e-119">Los parámetros de dirección URL de la API de reunión deben `meetingId` `userId` tener , y `tenantId` .</span><span class="sxs-lookup"><span data-stu-id="1fe6e-119">Meeting API URL parameters must have `meetingId`, `userId`, and `tenantId`.</span></span> <span data-ttu-id="1fe6e-120">Están disponibles como parte del SDK de cliente de Teams y la actividad del bot.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-120">These are available as part of the Teams client SDK and bot activity.</span></span> <span data-ttu-id="1fe6e-121">Además, se puede recuperar información confiable para el identificador de usuario y el identificador de inquilino mediante la autenticación [de SSO de tabulación.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="1fe6e-121">In addition, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="1fe6e-122">La `GetParticipant` API debe tener un registro de bot y un identificador para generar tokens de autenticación.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-122">The `GetParticipant` API must have a bot registration and ID to generate auth tokens.</span></span> <span data-ttu-id="1fe6e-123">Para obtener más información, vea [bot registration and ID](../build-your-first-app/build-bot.md).</span><span class="sxs-lookup"><span data-stu-id="1fe6e-123">For more information, see [bot registration and ID](../build-your-first-app/build-bot.md).</span></span>

* <span data-ttu-id="1fe6e-124">Para que la aplicación se actualice en tiempo real, debe estar actualizada en función de las actividades de eventos de la reunión.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-124">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="1fe6e-125">Estos eventos pueden estar dentro del cuadro de diálogo en la reunión y otras etapas a lo largo del ciclo de vida de la reunión.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-125">These events can be within the in-meeting dialog box and other stages across the meeting lifecycle.</span></span> <span data-ttu-id="1fe6e-126">Para el cuadro de diálogo en la reunión, vea el `bot Id` parámetro de finalización en `Notification Signal API` .</span><span class="sxs-lookup"><span data-stu-id="1fe6e-126">For the in-meeting dialog box, see completion `bot Id` parameter in `Notification Signal API`.</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="1fe6e-127">Referencia de api de aplicaciones de reunión</span><span class="sxs-lookup"><span data-stu-id="1fe6e-127">Meeting apps API reference</span></span>

|<span data-ttu-id="1fe6e-128">API</span><span class="sxs-lookup"><span data-stu-id="1fe6e-128">API</span></span>|<span data-ttu-id="1fe6e-129">Descripción</span><span class="sxs-lookup"><span data-stu-id="1fe6e-129">Description</span></span>|<span data-ttu-id="1fe6e-130">Solicitud</span><span class="sxs-lookup"><span data-stu-id="1fe6e-130">Request</span></span>|<span data-ttu-id="1fe6e-131">Origen</span><span class="sxs-lookup"><span data-stu-id="1fe6e-131">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="1fe6e-132">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-132">**GetUserContext**</span></span>| <span data-ttu-id="1fe6e-133">Esta API le permite obtener información contextual para mostrar contenido relevante en una pestaña de Teams.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-133">This API enables you to get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="1fe6e-134">_**microsoftTeams.getContext( ( ) => { /*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="1fe6e-134">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="1fe6e-135">SDK de cliente de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1fe6e-135">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="1fe6e-136">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-136">**GetParticipant**</span></span>| <span data-ttu-id="1fe6e-137">Esta API permite que un bot obtenga información de los participantes mediante el identificador de reunión y el identificador de participante.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-137">This API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> |<span data-ttu-id="1fe6e-138">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="1fe6e-138">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="1fe6e-139">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="1fe6e-139">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="1fe6e-140">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-140">**NotificationSignal**</span></span> | <span data-ttu-id="1fe6e-141">Esta API le permite proporcionar señales de reunión que se entregan mediante la API de notificación de conversación existente para el chat de bots de usuario.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-141">This API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="1fe6e-142">Le permite señalar en función de la acción del usuario que muestra un cuadro de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-142">It allows you to signal based on user action that shows an in-meeting dialog box.</span></span> |<span data-ttu-id="1fe6e-143">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="1fe6e-143">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="1fe6e-144">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="1fe6e-144">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="1fe6e-145">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="1fe6e-145">GetUserContext</span></span>

<span data-ttu-id="1fe6e-146">Para identificar y recuperar información contextual del contenido de la pestaña, vea [Obtener contexto para la pestaña Teams](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). se usa en una pestaña al ejecutarse en el contexto de la reunión y `meetingId` se agrega para la carga de respuesta.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-146">To identify and retrieve contextual information for your tab content, see [get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). `meetingId` is used by a tab when running in the meeting context and is added for the response payload.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="1fe6e-147">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="1fe6e-147">GetParticipant API</span></span>

> [!NOTE]
> * <span data-ttu-id="1fe6e-148">No almacenar en caché los roles de los participantes, ya que el organizador de la reunión puede cambiar un rol en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-148">Do not cache participant roles since the meeting organizer can change a role any time.</span></span>
> * <span data-ttu-id="1fe6e-149">Actualmente, Teams no admite listas de distribución grandes ni tamaños de lista de más de 350 participantes para la `GetParticipant` API.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-149">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="1fe6e-150">Parámetros de consulta</span><span class="sxs-lookup"><span data-stu-id="1fe6e-150">Query parameters</span></span>

|<span data-ttu-id="1fe6e-151">Valor</span><span class="sxs-lookup"><span data-stu-id="1fe6e-151">Value</span></span>|<span data-ttu-id="1fe6e-152">Tipo</span><span class="sxs-lookup"><span data-stu-id="1fe6e-152">Type</span></span>|<span data-ttu-id="1fe6e-153">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1fe6e-153">Required</span></span>|<span data-ttu-id="1fe6e-154">Descripción</span><span class="sxs-lookup"><span data-stu-id="1fe6e-154">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="1fe6e-155">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-155">**meetingId**</span></span>| <span data-ttu-id="1fe6e-156">string</span><span class="sxs-lookup"><span data-stu-id="1fe6e-156">string</span></span> | <span data-ttu-id="1fe6e-157">Sí</span><span class="sxs-lookup"><span data-stu-id="1fe6e-157">Yes</span></span> | <span data-ttu-id="1fe6e-158">El identificador de reunión está disponible a través de Bot Invoke y el SDK de cliente de Teams.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-158">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="1fe6e-159">**participantId**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-159">**participantId**</span></span>| <span data-ttu-id="1fe6e-160">string</span><span class="sxs-lookup"><span data-stu-id="1fe6e-160">string</span></span> | <span data-ttu-id="1fe6e-161">Sí</span><span class="sxs-lookup"><span data-stu-id="1fe6e-161">Yes</span></span> | <span data-ttu-id="1fe6e-162">El identificador de participante es el identificador de usuario.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-162">The participant ID is the user ID.</span></span> <span data-ttu-id="1fe6e-163">Está disponible en TAB SSO, Bot Invoke y Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-163">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="1fe6e-164">Se recomienda obtener un identificador de participante del SSO de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-164">It is recommended to get a participant ID from the Tab SSO.</span></span> |
|<span data-ttu-id="1fe6e-165">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-165">**tenantId**</span></span>| <span data-ttu-id="1fe6e-166">string</span><span class="sxs-lookup"><span data-stu-id="1fe6e-166">string</span></span> | <span data-ttu-id="1fe6e-167">Sí</span><span class="sxs-lookup"><span data-stu-id="1fe6e-167">Yes</span></span> | <span data-ttu-id="1fe6e-168">El identificador de inquilino es necesario para los usuarios del espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-168">The tenant ID is required for the tenant users.</span></span> <span data-ttu-id="1fe6e-169">Está disponible en TAB SSO, Bot Invoke y Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-169">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="1fe6e-170">Se recomienda obtener un identificador de inquilino del SSO de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-170">It is recommended to get a tenant ID from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="1fe6e-171">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1fe6e-171">Example</span></span>

# <a name="c"></a>[<span data-ttu-id="1fe6e-172">C#</span><span class="sxs-lookup"><span data-stu-id="1fe6e-172">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="1fe6e-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="1fe6e-173">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="1fe6e-174">JSON</span><span class="sxs-lookup"><span data-stu-id="1fe6e-174">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

* * *

<span data-ttu-id="1fe6e-175">El cuerpo de la respuesta JSON `GetParticipant` para la API es:</span><span class="sxs-lookup"><span data-stu-id="1fe6e-175">The JSON response body for `GetParticipant` API is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="1fe6e-176">Códigos de respuesta</span><span class="sxs-lookup"><span data-stu-id="1fe6e-176">Response codes</span></span>

|<span data-ttu-id="1fe6e-177">Código de respuesta</span><span class="sxs-lookup"><span data-stu-id="1fe6e-177">Response code</span></span>|<span data-ttu-id="1fe6e-178">Descripción</span><span class="sxs-lookup"><span data-stu-id="1fe6e-178">Description</span></span>|
|---|---|
| <span data-ttu-id="1fe6e-179">**403**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-179">**403**</span></span> | <span data-ttu-id="1fe6e-180">La aplicación no puede obtener información de los participantes.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-180">The app is not allowed to get participant information.</span></span> <span data-ttu-id="1fe6e-181">Esta es la respuesta de error más común y se desencadena si la aplicación no está instalada en la reunión.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-181">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="1fe6e-182">Por ejemplo, si la aplicación está deshabilitada por el administrador del espacio empresarial o bloqueada durante la migración del sitio en directo.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-182">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>|
| <span data-ttu-id="1fe6e-183">**200**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-183">**200**</span></span> | <span data-ttu-id="1fe6e-184">La información del participante se recupera correctamente.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-184">The participant information is successfully retrieved.</span></span>|
| <span data-ttu-id="1fe6e-185">**401**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-185">**401**</span></span> | <span data-ttu-id="1fe6e-186">La aplicación responde con un token no válido.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-186">The app responds with an invalid token.</span></span>|
| <span data-ttu-id="1fe6e-187">**404**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-187">**404**</span></span> | <span data-ttu-id="1fe6e-188">La reunión ha expirado o no se encuentra el participante.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-188">The meeting has either expired or participant cannot be found.</span></span>|
| <span data-ttu-id="1fe6e-189">**500**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-189">**500**</span></span> | <span data-ttu-id="1fe6e-190">La reunión ha expirado más de 60 días desde que finalizó la reunión o el participante no tiene permisos en función de su rol.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-190">The meeting has either expired more than 60 days since the meeting ended or the participant does not have permissions based on their role.</span></span>|

### <a name="notificationsignal-api"></a><span data-ttu-id="1fe6e-191">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="1fe6e-191">NotificationSignal API</span></span>

<span data-ttu-id="1fe6e-192">Todos los usuarios de una reunión reciben las notificaciones enviadas a través de la `NotificationSignal` API.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-192">All users in a meeting receive the notifications sent through the `NotificationSignal` API.</span></span>

> [!NOTE]
> * <span data-ttu-id="1fe6e-193">Cuando se invoca un cuadro de diálogo en la reunión, el contenido se presenta como un mensaje de chat.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-193">When an in-meeting dialog box is invoked, the content is presented as a chat message.</span></span>
> * <span data-ttu-id="1fe6e-194">Actualmente, no se admite el envío de notificaciones dirigidas.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-194">Currently, sending targeted notifications is not supported.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="1fe6e-195">Parámetros de consulta</span><span class="sxs-lookup"><span data-stu-id="1fe6e-195">Query parameters</span></span>

|<span data-ttu-id="1fe6e-196">Valor</span><span class="sxs-lookup"><span data-stu-id="1fe6e-196">Value</span></span>|<span data-ttu-id="1fe6e-197">Tipo</span><span class="sxs-lookup"><span data-stu-id="1fe6e-197">Type</span></span>|<span data-ttu-id="1fe6e-198">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1fe6e-198">Required</span></span>|<span data-ttu-id="1fe6e-199">Descripción</span><span class="sxs-lookup"><span data-stu-id="1fe6e-199">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="1fe6e-200">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-200">**conversationId**</span></span>| <span data-ttu-id="1fe6e-201">string</span><span class="sxs-lookup"><span data-stu-id="1fe6e-201">string</span></span> | <span data-ttu-id="1fe6e-202">Sí</span><span class="sxs-lookup"><span data-stu-id="1fe6e-202">Yes</span></span> | <span data-ttu-id="1fe6e-203">El identificador de conversación está disponible como parte de la invocación de bot</span><span class="sxs-lookup"><span data-stu-id="1fe6e-203">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="example"></a><span data-ttu-id="1fe6e-204">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1fe6e-204">Example</span></span>

<span data-ttu-id="1fe6e-205">Se `Bot ID` declara en el manifiesto y el bot recibe un objeto result.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-205">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span>

> [!NOTE]
> * <span data-ttu-id="1fe6e-206">El `completionBotId` parámetro de la es opcional en el ejemplo de carga `externalResourceUrl` solicitada.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-206">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="1fe6e-207">`Bot ID` se declara en el manifiesto y el bot recibe un objeto result.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-207">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="1fe6e-208">Los `externalResourceUrl` parámetros de ancho y alto deben estar en píxeles.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-208">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="1fe6e-209">Para asegurarse de que las dimensiones están dentro de los límites permitidos, vea [directrices de diseño](design/designing-apps-in-meetings.md).</span><span class="sxs-lookup"><span data-stu-id="1fe6e-209">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="1fe6e-210">La dirección URL es la página cargada como una en el cuadro de diálogo `<iframe>` en la reunión.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-210">The URL is the page loaded as an `<iframe>` in the in-meeting dialog box.</span></span> <span data-ttu-id="1fe6e-211">El dominio debe estar en la matriz de la aplicación `validDomains` en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-211">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

# <a name="c"></a>[<span data-ttu-id="1fe6e-212">C#</span><span class="sxs-lookup"><span data-stu-id="1fe6e-212">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="1fe6e-213">JavaScript</span><span class="sxs-lookup"><span data-stu-id="1fe6e-213">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="1fe6e-214">JSON</span><span class="sxs-lookup"><span data-stu-id="1fe6e-214">JSON</span></span>](#tab/json)

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

#### <a name="response-codes"></a><span data-ttu-id="1fe6e-215">Códigos de respuesta</span><span class="sxs-lookup"><span data-stu-id="1fe6e-215">Response codes</span></span>

|<span data-ttu-id="1fe6e-216">Código de respuesta</span><span class="sxs-lookup"><span data-stu-id="1fe6e-216">Response code</span></span>|<span data-ttu-id="1fe6e-217">Descripción</span><span class="sxs-lookup"><span data-stu-id="1fe6e-217">Description</span></span>|
|---|---|
| <span data-ttu-id="1fe6e-218">**201**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-218">**201**</span></span> | <span data-ttu-id="1fe6e-219">La actividad con señal se envía correctamente</span><span class="sxs-lookup"><span data-stu-id="1fe6e-219">The activity with signal is successfully sent</span></span> |
| <span data-ttu-id="1fe6e-220">**401**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-220">**401**</span></span> | <span data-ttu-id="1fe6e-221">La aplicación responde con un token no válido.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-221">The app responds with an invalid token.</span></span> |
| <span data-ttu-id="1fe6e-222">**403**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-222">**403**</span></span> | <span data-ttu-id="1fe6e-223">La aplicación no puede enviar la señal.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-223">The app is unable to send the signal.</span></span> <span data-ttu-id="1fe6e-224">Esto puede ocurrir debido a diversos motivos, como que el administrador de inquilinos deshabilita la aplicación, la aplicación se bloquea durante la migración del sitio en directo, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-224">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="1fe6e-225">En este caso, la carga contiene un mensaje de error detallado.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-225">In this case, the payload contains a detailed error message.</span></span> |
| <span data-ttu-id="1fe6e-226">**404**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-226">**404**</span></span> | <span data-ttu-id="1fe6e-227">El chat de reunión no existe.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-227">The meeting chat does not exist.</span></span> |

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="1fe6e-228">Habilitar la aplicación para reuniones de Teams</span><span class="sxs-lookup"><span data-stu-id="1fe6e-228">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="1fe6e-229">Actualizar el manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="1fe6e-229">Update your app manifest</span></span>

<span data-ttu-id="1fe6e-230">Las funcionalidades de la aplicación reuniones se declaran en el manifiesto de la aplicación mediante `configurableTabs` las `scopes` matrices , `context` y.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-230">The meetings app capabilities are declared in your app manifest using the `configurableTabs`, `scopes`, and `context` arrays.</span></span> <span data-ttu-id="1fe6e-231">El ámbito define a quién y el contexto define dónde está disponible la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-231">Scope defines to whom and context defines where your app is available.</span></span>

> [!NOTE]
> <span data-ttu-id="1fe6e-232">Intente actualizar el manifiesto de la aplicación con el [esquema de manifiesto](../resources/schema/manifest-schema-dev-preview.md).</span><span class="sxs-lookup"><span data-stu-id="1fe6e-232">Try updating your app manifest with the [manifest schema](../resources/schema/manifest-schema-dev-preview.md).</span></span>
> <span data-ttu-id="1fe6e-233">Las aplicaciones de las reuniones necesitan *ámbito groupchat.*</span><span class="sxs-lookup"><span data-stu-id="1fe6e-233">Apps in meetings need *groupchat* scope.</span></span> <span data-ttu-id="1fe6e-234">El *ámbito de* equipo solo funciona para pestañas en canales.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-234">The *team* scope works for tabs in channels only.</span></span>

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
> <span data-ttu-id="1fe6e-235">`meetingStage` actualmente solo está disponible en versión preliminar del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-235">`meetingStage` is currently available in developer preview only.</span></span>

### <a name="context-property"></a><span data-ttu-id="1fe6e-236">Context (propiedad)</span><span class="sxs-lookup"><span data-stu-id="1fe6e-236">Context property</span></span>

<span data-ttu-id="1fe6e-237">La pestaña y las propiedades te permiten determinar dónde debe aparecer `context` `scopes` la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-237">The tab `context` and `scopes` properties enable you to determine where your app must appear.</span></span> <span data-ttu-id="1fe6e-238">Las pestañas del `team` ámbito or pueden tener más de un `groupchat` contexto.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-238">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="1fe6e-239">Estos son los valores de la propiedad desde `context` la que puede usar todos o algunos de los valores:</span><span class="sxs-lookup"><span data-stu-id="1fe6e-239">Following are the values for the `context` property from which you can use all or some of the values:</span></span>

|<span data-ttu-id="1fe6e-240">Valor</span><span class="sxs-lookup"><span data-stu-id="1fe6e-240">Value</span></span>|<span data-ttu-id="1fe6e-241">Descripción</span><span class="sxs-lookup"><span data-stu-id="1fe6e-241">Description</span></span>|
|---|---|
| <span data-ttu-id="1fe6e-242">**channelTab**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-242">**channelTab**</span></span> | <span data-ttu-id="1fe6e-243">Pestaña en el encabezado de un canal de grupo.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-243">A tab in the header of a team channel.</span></span> |
| <span data-ttu-id="1fe6e-244">**privateChatTab**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-244">**privateChatTab**</span></span> | <span data-ttu-id="1fe6e-245">Pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios que no se encuentra en el contexto de un equipo o reunión.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-245">A tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span> |
| <span data-ttu-id="1fe6e-246">**meetingChatTab**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-246">**meetingChatTab**</span></span> | <span data-ttu-id="1fe6e-247">Pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios en el contexto de una reunión programada.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-247">A tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span> |
| <span data-ttu-id="1fe6e-248">**meetingDetailsTab**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-248">**meetingDetailsTab**</span></span> | <span data-ttu-id="1fe6e-249">Pestaña en el encabezado de la vista de detalles de la reunión del calendario.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-249">A tab in the header of the meeting details view of the calendar.</span></span> |
| <span data-ttu-id="1fe6e-250">**meetingSidePanel**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-250">**meetingSidePanel**</span></span> | <span data-ttu-id="1fe6e-251">Un panel en la reunión abierto a través de la barra unificada (barra U).</span><span class="sxs-lookup"><span data-stu-id="1fe6e-251">An in-meeting panel opened via the unified bar (U-bar).</span></span> |
| <span data-ttu-id="1fe6e-252">**meetingStage**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-252">**meetingStage**</span></span> | <span data-ttu-id="1fe6e-253">Una aplicación del panel lateral se puede compartir en la fase de reunión.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-253">An app from the sidepanel can be shared to the meeting stage.</span></span> |

> [!NOTE]
> <span data-ttu-id="1fe6e-254">`Context` actualmente no se admite en clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-254">`Context` property is currently not supported on mobile clients.</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="1fe6e-255">Configurar la aplicación para escenarios de reunión</span><span class="sxs-lookup"><span data-stu-id="1fe6e-255">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="1fe6e-256">Para que la aplicación esté visible en la galería de pestañas, debe admitir pestañas configurables y el ámbito de chat de grupo.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-256">For your app to be visible in the tab gallery it must support configurable tabs and the group chat scope.</span></span>
> * <span data-ttu-id="1fe6e-257">Los clientes móviles solo admiten pestañas en fases de reunión previas y posteriores.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-257">Mobile clients support tabs only in pre and post meeting stages.</span></span>
> * <span data-ttu-id="1fe6e-258">Las experiencias en la reunión que es el cuadro de diálogo y la pestaña en la reunión actualmente no se admiten en clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-258">The in-meeting experiences that is in-meeting dialog box and tab is currently not supported on mobile clients.</span></span> <span data-ttu-id="1fe6e-259">Para obtener más información, consulta [las instrucciones para las pestañas en el móvil](../tabs/design/tabs-mobile.md) al crear las pestañas para móviles.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-259">For more information, see [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span>

### <a name="before-a-meeting"></a><span data-ttu-id="1fe6e-260">Antes de una reunión</span><span class="sxs-lookup"><span data-stu-id="1fe6e-260">Before a meeting</span></span>

<span data-ttu-id="1fe6e-261">Antes de una reunión, los usuarios pueden agregar pestañas, bots y extensiones de mensajería a una reunión.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-261">Before a meeting, users can add tabs, bots and messaging extensions to a meeting.</span></span> <span data-ttu-id="1fe6e-262">Los usuarios con roles de organizador y moderador pueden agregar pestañas a una reunión.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-262">Users with organizer and presenter roles can add tabs to a meeting.</span></span>

<span data-ttu-id="1fe6e-263">**Para agregar una pestaña a una reunión**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-263">**To add a tab to a meeting**</span></span>

1. <span data-ttu-id="1fe6e-264">En el calendario, seleccione una reunión a la que desee agregar una pestaña.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-264">In your calendar, select a meeting to which you want to add a tab.</span></span>
1. <span data-ttu-id="1fe6e-265">Seleccione la **pestaña Detalles** y seleccione más</span><span class="sxs-lookup"><span data-stu-id="1fe6e-265">Select the **Details** tab and select plus</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="1fe6e-266">.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-266">.</span></span> <span data-ttu-id="1fe6e-267">Aparece la galería de pestañas.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-267">The tab gallery appears.</span></span>

    ![Experiencia previa a la reunión](../assets/images/apps-in-meetings/PreMeeting.png)

1. <span data-ttu-id="1fe6e-269">En la galería de pestañas, selecciona la aplicación que quieras agregar y sigue los pasos según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-269">In the tab gallery, select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="1fe6e-270">La aplicación se instala como una pestaña.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-270">The app is installed as a tab.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="1fe6e-271">Actualmente, en la pestaña reuniones, no se admite la obtención de detalles de la reunión y la información de los participantes.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-271">Currently, in meetings tab, getting meeting details and participant information is not supported.</span></span>

<span data-ttu-id="1fe6e-272">**Para agregar una extensión de mensajería a una reunión**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-272">**To add a messaging extension to a meeting**</span></span>

1. <span data-ttu-id="1fe6e-273">Seleccione los puntos suspensivos o el menú de desbordamiento &#x25CF;&#x25CF;&#x25CF; ubicado en el área del mensaje de redacción en el chat.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-273">Select the ellipses or overflow menu &#x25CF;&#x25CF;&#x25CF; located in the compose message area in the chat.</span></span>
1. <span data-ttu-id="1fe6e-274">Selecciona la aplicación que quieras agregar y sigue los pasos según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-274">Select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="1fe6e-275">La aplicación se instala como una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-275">The app is installed as a messaging extension.</span></span>

<span data-ttu-id="1fe6e-276">**Para agregar un bot a una reunión**</span><span class="sxs-lookup"><span data-stu-id="1fe6e-276">**To add a bot to a meeting**</span></span>

<span data-ttu-id="1fe6e-277">En un chat de reunión, escriba la **@** clave y seleccione Obtener **bots**.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-277">In a meeting chat enter the **@** key and select **Get bots**.</span></span>

> [!NOTE]
> * <span data-ttu-id="1fe6e-278">La identidad del usuario debe confirmarse con [tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="1fe6e-278">The user identity must be confirmed using [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="1fe6e-279">Después de la autenticación, la aplicación puede recuperar el rol de usuario mediante la `GetParticipant` API.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-279">After authentication, the app can retrieve the user role using the `GetParticipant` API.</span></span>
> * <span data-ttu-id="1fe6e-280">En función del rol de usuario, la aplicación tiene la capacidad de proporcionar experiencias específicas del rol.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-280">Based on the user role, the app has the capability to provide role specific experiences.</span></span> <span data-ttu-id="1fe6e-281">Por ejemplo, una aplicación de sondeo solo permite a los organizadores y presentadores crear un nuevo sondeo.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-281">For example, a polling app allows only organizers and presenters to create a new poll.</span></span>
> * <span data-ttu-id="1fe6e-282">Las asignaciones de roles se pueden cambiar mientras se está en curso una reunión.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-282">Role assignments can be changed while a meeting is in progress.</span></span> <span data-ttu-id="1fe6e-283">Para obtener más información, vea [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span><span class="sxs-lookup"><span data-stu-id="1fe6e-283">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

### <a name="during-a-meeting"></a><span data-ttu-id="1fe6e-284">Durante una reunión</span><span class="sxs-lookup"><span data-stu-id="1fe6e-284">During a meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="1fe6e-285">sidePanel</span><span class="sxs-lookup"><span data-stu-id="1fe6e-285">sidePanel</span></span>

<span data-ttu-id="1fe6e-286">Con sidePanel, puede personalizar experiencias en una reunión que permita a los organizadores y presentadores tener un conjunto diferente de vistas y acciones.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-286">With the sidePanel, you can customize experiences in a meeting that enable organizers and presenters to have different set of views and actions.</span></span> <span data-ttu-id="1fe6e-287">En el manifiesto de la aplicación, debes agregar sidePanel a la matriz de contexto.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-287">In your app manifest, you must add sidePanel to the context array.</span></span> <span data-ttu-id="1fe6e-288">En la reunión y en todos los escenarios, la aplicación se representa en una pestaña en la reunión que tiene 320 píxeles de ancho.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-288">In the meeting and in all scenarios, the app is rendered in an in-meeting tab that is 320 pixels in width.</span></span> <span data-ttu-id="1fe6e-289">Para obtener más información, vea [FrameContext interface](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
).</span><span class="sxs-lookup"><span data-stu-id="1fe6e-289">For more information, see [FrameContext interface](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
).</span></span>

<span data-ttu-id="1fe6e-290">Para usar la `userContext` API para enrutar las solicitudes en consecuencia, vea [Sdk de Teams](../tabs/how-to/access-teams-context.md#user-context).</span><span class="sxs-lookup"><span data-stu-id="1fe6e-290">To use the `userContext` API to route requests accordingly, see [Teams SDK](../tabs/how-to/access-teams-context.md#user-context).</span></span> <span data-ttu-id="1fe6e-291">Consulte [Flujo de autenticación de Teams para las pestañas](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="1fe6e-291">See [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="1fe6e-292">El flujo de autenticación para pestañas es muy similar al flujo de autenticación para sitios web.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-292">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="1fe6e-293">Por lo tanto, las pestañas pueden usar OAuth 2.0 directamente.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-293">So tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="1fe6e-294">Vea, Plataforma de identidades de Microsoft y flujo de código de autorización de [OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span><span class="sxs-lookup"><span data-stu-id="1fe6e-294">See, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="1fe6e-295">La extensión de mensajería funciona según lo esperado cuando un usuario está en una vista en la reunión y el usuario puede publicar tarjetas de extensión de mensaje de redacción.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-295">Messaging extension works as expected when a user is in an in-meeting view and the user can post compose message extension cards.</span></span> <span data-ttu-id="1fe6e-296">AppName en la reunión es una información sobre herramientas que indica el nombre de la aplicación en la barra U de la reunión.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-296">AppName in-meeting is a tooltip that states the app name in-meeting U-bar.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="1fe6e-297">Diálogo en la reunión</span><span class="sxs-lookup"><span data-stu-id="1fe6e-297">In-meeting dialog</span></span>

<span data-ttu-id="1fe6e-298">El cuadro de diálogo en la reunión se puede usar para interactuar con los participantes durante la reunión y recopilar información o comentarios durante la reunión.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-298">The in-meeting dialog box can be used to engage participants during the meeting and collect information or feedback during the meeting.</span></span> <span data-ttu-id="1fe6e-299">Use la API para indicar que se debe desencadenar [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) una notificación de burbuja.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-299">Use the [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification must be triggered.</span></span> <span data-ttu-id="1fe6e-300">Como parte de la carga de solicitud de notificación, incluya la dirección URL donde se hospeda el contenido que se va a mostrar.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-300">As part of the notification request payload, include the URL where the content to be shown is hosted.</span></span>

<span data-ttu-id="1fe6e-301">El cuadro de diálogo en la reunión no debe usar el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-301">In-meeting dialog must not use task module.</span></span> <span data-ttu-id="1fe6e-302">El módulo de tareas no se invoca en un chat de reunión.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-302">Task module is not invoked in a meeting chat.</span></span> <span data-ttu-id="1fe6e-303">Se usa una dirección URL de recurso externo para mostrar una burbuja de contenido en una reunión.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-303">An external resource URL is used to display content bubble in a meeting.</span></span> <span data-ttu-id="1fe6e-304">Puede usar el método `submitTask` para enviar datos en un chat de reunión.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-304">You can use the `submitTask` method to submit data in a meeting chat.</span></span>

> [!NOTE]
> * <span data-ttu-id="1fe6e-305">Debe invocar la [función submitTask() para](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) descartarla automáticamente después de que un usuario realiza una acción en la vista web.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-305">You must invoke the [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to dismiss automatically after a user takes an action in the web-view.</span></span> <span data-ttu-id="1fe6e-306">Este es un requisito para el envío de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-306">This is a requirement for app submission.</span></span> <span data-ttu-id="1fe6e-307">Para obtener más información, vea [Módulo de tareas del SDK de Teams](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="1fe6e-307">For more information, see [Teams SDK task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
> * <span data-ttu-id="1fe6e-308">Si quieres que la aplicación admita usuarios anónimos, la carga inicial de la solicitud de invocación debe basarse en los metadatos de solicitud del objeto, no en `from.id` `from` los `from.aadObjectId` metadatos de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-308">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id` request metadata in the `from` object, not the `from.aadObjectId` request metadata.</span></span> <span data-ttu-id="1fe6e-309">`from.id` es el identificador de usuario y es el identificador de `from.aadObjectId` Azure Active Directory (AAD) del usuario.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-309">`from.id` is the user ID and `from.aadObjectId` is the Azure Active Directory (AAD) ID of the user.</span></span> <span data-ttu-id="1fe6e-310">Para obtener más información, vea [using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) y create and send the task [module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span><span class="sxs-lookup"><span data-stu-id="1fe6e-310">For more information, see [using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

#### <a name="share-to-stage"></a><span data-ttu-id="1fe6e-311">Compartir en fase</span><span class="sxs-lookup"><span data-stu-id="1fe6e-311">Share to stage</span></span> 

> [!NOTE]
> <span data-ttu-id="1fe6e-312">Esta funcionalidad solo se puede obtener en la vista previa de desarrollo de insider</span><span class="sxs-lookup"><span data-stu-id="1fe6e-312">This capability is avaialable only in insider dev preview</span></span>


<span data-ttu-id="1fe6e-313">Esta funcionalidad ofrece a los desarrolladores la capacidad de compartir una aplicación en la fase de reunión.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-313">This capability gives developers the ability to share an app to the meeting stage.</span></span> <span data-ttu-id="1fe6e-314">Al habilitar el recurso compartido en la fase de reunión, los participantes de la reunión pueden colaborar en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-314">By enabling share to the meeting stage, meeting participants can collaborate in real-time.</span></span> 

<span data-ttu-id="1fe6e-315">El contexto necesario es meetingStage en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-315">The required context is meetingStage in the app manifest.</span></span> <span data-ttu-id="1fe6e-316">Un requisito previo para esto es tener el contexto meetingSidePanel.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-316">A pre-requisite for this is to have the meetingSidePanel context.</span></span> <span data-ttu-id="1fe6e-317">Esto habilitará el botón "Compartir" en el panel lateral como se indica a continuación</span><span class="sxs-lookup"><span data-stu-id="1fe6e-317">This will enable the "Share" button in the sidepanel as depecited below</span></span>



### <a name="after-a-meeting"></a><span data-ttu-id="1fe6e-318">Después de una reunión</span><span class="sxs-lookup"><span data-stu-id="1fe6e-318">After a meeting</span></span>

<span data-ttu-id="1fe6e-319">Las configuraciones posteriores a la reunión y previas a la reunión son equivalentes.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-319">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="code-sample"></a><span data-ttu-id="1fe6e-320">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="1fe6e-320">Code sample</span></span>

|<span data-ttu-id="1fe6e-321">Nombre de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1fe6e-321">Sample name</span></span> | <span data-ttu-id="1fe6e-322">Descripción</span><span class="sxs-lookup"><span data-stu-id="1fe6e-322">Description</span></span> | <span data-ttu-id="1fe6e-323">C#</span><span class="sxs-lookup"><span data-stu-id="1fe6e-323">C#</span></span> |
|----------------|-----------------|--------------|
| <span data-ttu-id="1fe6e-324">Extensibilidad de reuniones</span><span class="sxs-lookup"><span data-stu-id="1fe6e-324">Meetings extensibility</span></span> | <span data-ttu-id="1fe6e-325">Ejemplo de extensibilidad de reuniones de Microsoft Teams para pasar tokens.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-325">Microsoft Teams meeting extensibility sample for passing tokens.</span></span> | [<span data-ttu-id="1fe6e-326">View</span><span class="sxs-lookup"><span data-stu-id="1fe6e-326">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) |
| <span data-ttu-id="1fe6e-327">Bot de burbuja de contenido de reunión</span><span class="sxs-lookup"><span data-stu-id="1fe6e-327">Meeting content bubble bot</span></span> | <span data-ttu-id="1fe6e-328">Ejemplo de extensibilidad de reuniones de Microsoft Teams para interactuar con el bot de burbujas de contenido en una reunión.</span><span class="sxs-lookup"><span data-stu-id="1fe6e-328">Microsoft Teams meeting extensibility sample for interacting with content bubble bot in a meeting.</span></span> | [<span data-ttu-id="1fe6e-329">View</span><span class="sxs-lookup"><span data-stu-id="1fe6e-329">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |

## <a name="see-also"></a><span data-ttu-id="1fe6e-330">Vea también</span><span class="sxs-lookup"><span data-stu-id="1fe6e-330">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1fe6e-331">Directrices de diseño de cuadros de diálogo en la reunión</span><span class="sxs-lookup"><span data-stu-id="1fe6e-331">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
> [!div class="nextstepaction"]
> [<span data-ttu-id="1fe6e-332">Flujo de autenticación de Teams para pestañas</span><span class="sxs-lookup"><span data-stu-id="1fe6e-332">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)

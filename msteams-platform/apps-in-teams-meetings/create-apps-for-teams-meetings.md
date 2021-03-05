---
title: Crear aplicaciones para reuniones de equipos
author: laujan
description: crear aplicaciones para reuniones de teams
ms.topic: conceptual
ms.author: lajanuar
keywords: API de roles de participantes de reuniones de aplicaciones de teams
ms.openlocfilehash: bd0f53ae34a23bdbbdc2e6f3992c7dd0836e9f28
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449496"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="b0112-104">Crear aplicaciones para reuniones de Teams</span><span class="sxs-lookup"><span data-stu-id="b0112-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="b0112-105">Requisitos previos y consideraciones</span><span class="sxs-lookup"><span data-stu-id="b0112-105">Prerequisites and considerations</span></span>

* <span data-ttu-id="b0112-106">Las aplicaciones de las reuniones requieren conocimientos básicos sobre el [desarrollo de aplicaciones de Teams.](../overview.md)</span><span class="sxs-lookup"><span data-stu-id="b0112-106">Apps in meetings require some basic knowledge of [Teams app development](../overview.md).</span></span> <span data-ttu-id="b0112-107">Una aplicación de una reunión puede incluir [](../messaging-extensions/what-are-messaging-extensions.md) [pestañas,](../tabs/what-are-tabs.md) [bots](../bots/what-are-bots.md)y características de extensiones de mensajería y requerirá actualizaciones del manifiesto de la aplicación [de](#update-your-app-manifest) Teams para indicar que la aplicación está disponible para reuniones</span><span class="sxs-lookup"><span data-stu-id="b0112-107">An app in a meeting can comprise of [tabs](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md), and [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md) features and will require updates to the Teams [app manifest](#update-your-app-manifest) to indicate that the app is available for meetings</span></span>

* <span data-ttu-id="b0112-108">Para que la aplicación funcione en el ciclo de vida de la reunión como una pestaña, debe admitir pestañas configurables en el ámbito [de groupchat](../resources/schema/manifest-schema.md#configurabletabs) (consulta cómo crear [una pestaña de grupo).](../build-your-first-app/build-channel-tab.md)</span><span class="sxs-lookup"><span data-stu-id="b0112-108">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) (see how to [build a group tab](../build-your-first-app/build-channel-tab.md)).</span></span> <span data-ttu-id="b0112-109">La compatibilidad con `groupchat` el ámbito habilitará la aplicación en [chats](teams-apps-in-meetings.md#pre-meeting-app-experience) previos y posteriores [a la](teams-apps-in-meetings.md#post-meeting-app-experience) reunión.</span><span class="sxs-lookup"><span data-stu-id="b0112-109">Supporting the `groupchat` scope will enable your app in [pre-meeting](teams-apps-in-meetings.md#pre-meeting-app-experience) and [post-meeting](teams-apps-in-meetings.md#post-meeting-app-experience) chats.</span></span>

* <span data-ttu-id="b0112-110">Los parámetros de dirección URL de la API de reunión pueden requerir , y el tenantId Están disponibles como parte de la actividad de bot y `meetingId` SDK de cliente de `userId` Teams. [](/onedrive/find-your-office-365-tenant-id)</span><span class="sxs-lookup"><span data-stu-id="b0112-110">Meeting API URL parameters may require `meetingId`, `userId`, and the [tenantId](/onedrive/find-your-office-365-tenant-id) These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="b0112-111">Además, se puede recuperar información confiable para el identificador de usuario y el identificador de inquilino mediante la autenticación [de SSO de tabulación.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="b0112-111">Additionally, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="b0112-112">Algunas API de reunión, como , requieren un `GetParticipant` registro de bot y un identificador [para](../build-your-first-app/build-bot.md) generar tokens de autenticación.</span><span class="sxs-lookup"><span data-stu-id="b0112-112">Some meeting APIs, such as `GetParticipant`, require a [bot registration and ID](../build-your-first-app/build-bot.md) to generate auth tokens.</span></span>

* <span data-ttu-id="b0112-113">Debe cumplir las directrices generales [de diseño de pestañas de Teams](../tabs/design/tabs.md) para escenarios previos y posteriores a la reunión.</span><span class="sxs-lookup"><span data-stu-id="b0112-113">You must adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios.</span></span> <span data-ttu-id="b0112-114">Para obtener experiencias durante las reuniones, consulte las directrices de diseño de [la](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) pestaña en la reunión y [del cuadro de diálogo](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) en la reunión.</span><span class="sxs-lookup"><span data-stu-id="b0112-114">For experiences during meetings, refer to the [in-meeting tab](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) and [in-meeting dialog](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) design guidelines.</span></span>

* <span data-ttu-id="b0112-115">Para que la aplicación se actualice en tiempo real, debe estar actualizada en función de las actividades de eventos de la reunión.</span><span class="sxs-lookup"><span data-stu-id="b0112-115">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="b0112-116">Estos eventos pueden estar dentro del cuadro de diálogo en la reunión (consulte el parámetro de finalización en ) y otras superficies a lo largo `bot Id` del ciclo de vida de la `Notification Signal API` reunión</span><span class="sxs-lookup"><span data-stu-id="b0112-116">These events can be within the in-meeting dialog (refer to completion `bot Id` parameter in `Notification Signal API`) and other surfaces across the meeting lifecycle</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="b0112-117">Referencia de api de aplicaciones de reunión</span><span class="sxs-lookup"><span data-stu-id="b0112-117">Meeting apps API reference</span></span>

|<span data-ttu-id="b0112-118">API</span><span class="sxs-lookup"><span data-stu-id="b0112-118">API</span></span>|<span data-ttu-id="b0112-119">Descripción</span><span class="sxs-lookup"><span data-stu-id="b0112-119">Description</span></span>|<span data-ttu-id="b0112-120">Solicitud</span><span class="sxs-lookup"><span data-stu-id="b0112-120">Request</span></span>|<span data-ttu-id="b0112-121">Origen</span><span class="sxs-lookup"><span data-stu-id="b0112-121">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="b0112-122">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="b0112-122">**GetUserContext**</span></span>| <span data-ttu-id="b0112-123">Obtenga información contextual para mostrar contenido relevante en una pestaña de Teams.</span><span class="sxs-lookup"><span data-stu-id="b0112-123">Get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="b0112-124">_**microsoftTeams.getContext( ( ) => { /*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="b0112-124">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="b0112-125">SDK de cliente de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b0112-125">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="b0112-126">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="b0112-126">**GetParticipant**</span></span>|<span data-ttu-id="b0112-127">Esta API permite que un bot obtenga información del participante mediante el identificador de reunión y el identificador de participante.</span><span class="sxs-lookup"><span data-stu-id="b0112-127">This API allows a bot to fetch a participant information by meeting id and participant id.</span></span>|<span data-ttu-id="b0112-128">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="b0112-128">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="b0112-129">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="b0112-129">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="b0112-130">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="b0112-130">**NotificationSignal**</span></span> |<span data-ttu-id="b0112-131">Las señales de reunión se entregarán con la siguiente API de notificación de conversación existente (para el chat de bots de usuario).</span><span class="sxs-lookup"><span data-stu-id="b0112-131">Meeting signals will be delivered using the following existing conversation notification API (for user-bot chat).</span></span> <span data-ttu-id="b0112-132">Esta API permite a los desarrolladores señalar en función de la acción del usuario final para mostrar una burbuja de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="b0112-132">This API allows developers to signal based on end-user action to show-case an in-meeting dialog bubble.</span></span>|<span data-ttu-id="b0112-133">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="b0112-133">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="b0112-134">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="b0112-134">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="b0112-135">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="b0112-135">GetUserContext</span></span>

<span data-ttu-id="b0112-136">Consulte nuestra documentación [de la](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) pestaña Obtener contexto de Teams para obtener instrucciones sobre cómo identificar y recuperar información contextual para el contenido de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="b0112-136">Please refer to our [Get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and  retrieving contextual information for your tab content.</span></span> <span data-ttu-id="b0112-137">Como parte de la extensibilidad de reuniones, se ha agregado un nuevo valor para la carga de respuesta:</span><span class="sxs-lookup"><span data-stu-id="b0112-137">As part of meetings extensibility, a new value has been added for the response payload:</span></span>

<span data-ttu-id="b0112-138">✔ **meetingId:** usado por una pestaña al ejecutarse en el contexto de la reunión.</span><span class="sxs-lookup"><span data-stu-id="b0112-138">✔ **meetingId**: used by a tab when running in the meeting context.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="b0112-139">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="b0112-139">GetParticipant API</span></span>

> [!NOTE]
>
> * <span data-ttu-id="b0112-140">No almacenar en caché los roles de participantes, ya que el organizador de la reunión puede cambiar un rol en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="b0112-140">Do not cache participant roles since the meeting organizer can change a role at any point in time.</span></span>
>
> * <span data-ttu-id="b0112-141">Actualmente, Teams no admite listas de distribución grandes ni tamaños de lista de más de 350 participantes para la `GetParticipant` API.</span><span class="sxs-lookup"><span data-stu-id="b0112-141">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="b0112-142">Parámetros de consulta</span><span class="sxs-lookup"><span data-stu-id="b0112-142">Query parameters</span></span>

|<span data-ttu-id="b0112-143">Valor</span><span class="sxs-lookup"><span data-stu-id="b0112-143">Value</span></span>|<span data-ttu-id="b0112-144">Tipo</span><span class="sxs-lookup"><span data-stu-id="b0112-144">Type</span></span>|<span data-ttu-id="b0112-145">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="b0112-145">Required</span></span>|<span data-ttu-id="b0112-146">Descripción</span><span class="sxs-lookup"><span data-stu-id="b0112-146">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="b0112-147">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="b0112-147">**meetingId**</span></span>| <span data-ttu-id="b0112-148">string</span><span class="sxs-lookup"><span data-stu-id="b0112-148">string</span></span> | <span data-ttu-id="b0112-149">Sí</span><span class="sxs-lookup"><span data-stu-id="b0112-149">Yes</span></span> | <span data-ttu-id="b0112-150">El identificador de reunión está disponible a través de Bot Invoke y el SDK de cliente de Teams.</span><span class="sxs-lookup"><span data-stu-id="b0112-150">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="b0112-151">**participantId**</span><span class="sxs-lookup"><span data-stu-id="b0112-151">**participantId**</span></span>| <span data-ttu-id="b0112-152">string</span><span class="sxs-lookup"><span data-stu-id="b0112-152">string</span></span> | <span data-ttu-id="b0112-153">Sí</span><span class="sxs-lookup"><span data-stu-id="b0112-153">Yes</span></span> | <span data-ttu-id="b0112-154">El participantId es el identificador de usuario.</span><span class="sxs-lookup"><span data-stu-id="b0112-154">The participantId is the user ID.</span></span> <span data-ttu-id="b0112-155">Está disponible en TAB SSO, Bot Invoke y Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="b0112-155">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="b0112-156">Es muy recomendable obtener un participantId desde la pestaña SSO.</span><span class="sxs-lookup"><span data-stu-id="b0112-156">It is highly recommended to get a participantId from the Tab SSO.</span></span> |
|<span data-ttu-id="b0112-157">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="b0112-157">**tenantId**</span></span>| <span data-ttu-id="b0112-158">string</span><span class="sxs-lookup"><span data-stu-id="b0112-158">string</span></span> | <span data-ttu-id="b0112-159">Sí</span><span class="sxs-lookup"><span data-stu-id="b0112-159">Yes</span></span> | <span data-ttu-id="b0112-160">El tenantId es necesario para los usuarios del espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="b0112-160">The tenantId is required for the tenant users.</span></span> <span data-ttu-id="b0112-161">Está disponible en TAB SSO, Bot Invoke y Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="b0112-161">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="b0112-162">Es muy recomendable obtener un tenantId del SSO de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="b0112-162">It is highly recommended to get a tenantId from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="b0112-163">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="b0112-163">Example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="b0112-164">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="b0112-164">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="b0112-165">JavaScript</span><span class="sxs-lookup"><span data-stu-id="b0112-165">JavaScript</span></span>](#tab/javascript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            TeamsMeetingParticipant participant = GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
            let member = participant.user;
            let meetingInfo = participant.meeting;
            let conversation = participant.conversation;
            
            await context.sendActivity(`The participant role is: '${meetingInfo.role}'`);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="b0112-166">JSON</span><span class="sxs-lookup"><span data-stu-id="b0112-166">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

<span data-ttu-id="b0112-167">El cuerpo de la respuesta es:</span><span class="sxs-lookup"><span data-stu-id="b0112-167">The response body is:</span></span>

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

* * *

#### <a name="response-codes"></a><span data-ttu-id="b0112-168">Códigos de respuesta</span><span class="sxs-lookup"><span data-stu-id="b0112-168">Response codes</span></span>

* <span data-ttu-id="b0112-169">**403:** La aplicación no puede obtener información de los participantes.</span><span class="sxs-lookup"><span data-stu-id="b0112-169">**403**: The app is not allowed to get participant information.</span></span> <span data-ttu-id="b0112-170">Esta es la respuesta de error más común y se desencadena si la aplicación no está instalada en la reunión.</span><span class="sxs-lookup"><span data-stu-id="b0112-170">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="b0112-171">Por ejemplo, si la aplicación está deshabilitada por el administrador de inquilinos o bloqueada durante la mitigación de livesite.</span><span class="sxs-lookup"><span data-stu-id="b0112-171">For example, if the app is disabled by tenant admin or blocked during livesite mitigation.</span></span>
* <span data-ttu-id="b0112-172">**200**: Información de los participantes recuperada correctamente.</span><span class="sxs-lookup"><span data-stu-id="b0112-172">**200**: Participant information successfully retrieved.</span></span>
* <span data-ttu-id="b0112-173">**401**: Token no válido.</span><span class="sxs-lookup"><span data-stu-id="b0112-173">**401**: Invalid token.</span></span>
* <span data-ttu-id="b0112-174">**404**: No se puede encontrar el participante.</span><span class="sxs-lookup"><span data-stu-id="b0112-174">**404**: Participant cannot be found.</span></span>
* <span data-ttu-id="b0112-175">**500:** La reunión ha expirado (más de 60 días desde que finalizó la reunión) o el participante no tiene permisos en función de su rol.</span><span class="sxs-lookup"><span data-stu-id="b0112-175">**500**: The meeting has either expired (more than 60 days since the meeting ended) or the participant does not have permissions based on their role.</span></span>


<span data-ttu-id="b0112-176">**Próximamente**</span><span class="sxs-lookup"><span data-stu-id="b0112-176">**Coming Soon**</span></span>

* <span data-ttu-id="b0112-177">**404:** La reunión ha expirado o no se encuentra el participante.</span><span class="sxs-lookup"><span data-stu-id="b0112-177">**404**: The meeting has either expired or participant cannot be found.</span></span>


### <a name="notificationsignal-api"></a><span data-ttu-id="b0112-178">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="b0112-178">NotificationSignal API</span></span>

<span data-ttu-id="b0112-179">Todos los usuarios de una reunión reciben las notificaciones enviadas a través de la API NotificationSignal.</span><span class="sxs-lookup"><span data-stu-id="b0112-179">All users in a meeting receive the notifications sent through the NotificationSignal API.</span></span>

> [!NOTE]
> <span data-ttu-id="b0112-180">Actualmente, no se admite el envío de notificaciones dirigidas.</span><span class="sxs-lookup"><span data-stu-id="b0112-180">Currently, sending targetted notifications is not supported.</span></span>
> <span data-ttu-id="b0112-181">Cuando se invoca un cuadro de diálogo en la reunión, también se presentará el mismo contenido como mensaje de chat.</span><span class="sxs-lookup"><span data-stu-id="b0112-181">When an in-meeting dialog is invoked, the same content will also be presented as a chat message.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="b0112-182">Parámetros de consulta</span><span class="sxs-lookup"><span data-stu-id="b0112-182">Query parameters</span></span>

|<span data-ttu-id="b0112-183">Valor</span><span class="sxs-lookup"><span data-stu-id="b0112-183">Value</span></span>|<span data-ttu-id="b0112-184">Tipo</span><span class="sxs-lookup"><span data-stu-id="b0112-184">Type</span></span>|<span data-ttu-id="b0112-185">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="b0112-185">Required</span></span>|<span data-ttu-id="b0112-186">Descripción</span><span class="sxs-lookup"><span data-stu-id="b0112-186">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="b0112-187">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="b0112-187">**conversationId**</span></span>| <span data-ttu-id="b0112-188">string</span><span class="sxs-lookup"><span data-stu-id="b0112-188">string</span></span> | <span data-ttu-id="b0112-189">Sí</span><span class="sxs-lookup"><span data-stu-id="b0112-189">Yes</span></span> | <span data-ttu-id="b0112-190">El identificador de conversación está disponible como parte de la invocación de bot</span><span class="sxs-lookup"><span data-stu-id="b0112-190">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="example"></a><span data-ttu-id="b0112-191">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="b0112-191">Example</span></span>

<span data-ttu-id="b0112-192">Se `Bot ID` declara en el manifiesto y el bot recibe un objeto result.</span><span class="sxs-lookup"><span data-stu-id="b0112-192">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span> <span data-ttu-id="b0112-193">En el siguiente ejemplo, el `completionBotId` parámetro del es opcional en la carga `externalResourceUrl` solicitada:</span><span class="sxs-lookup"><span data-stu-id="b0112-193">In the following example, the `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload:</span></span>

> [!NOTE]
> * <span data-ttu-id="b0112-194">Los `externalResourceUrl` parámetros de ancho y alto deben estar en píxeles.</span><span class="sxs-lookup"><span data-stu-id="b0112-194">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="b0112-195">Para asegurarse de que las dimensiones están dentro de los límites permitidos, vea [directrices de diseño](design/designing-apps-in-meetings.md).</span><span class="sxs-lookup"><span data-stu-id="b0112-195">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="b0112-196">La dirección URL es la página cargada como una `<iframe>` en el cuadro de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="b0112-196">The URL is the page loaded as an `<iframe>` in the in-meeting dialog.</span></span> <span data-ttu-id="b0112-197">El dominio debe estar en la matriz de la aplicación `validDomains` en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b0112-197">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="b0112-198">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="b0112-198">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="b0112-199">JavaScript</span><span class="sxs-lookup"><span data-stu-id="b0112-199">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="b0112-200">JSON</span><span class="sxs-lookup"><span data-stu-id="b0112-200">JSON</span></span>](#tab/json)

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

#### <a name="response-codes"></a><span data-ttu-id="b0112-201">Códigos de respuesta</span><span class="sxs-lookup"><span data-stu-id="b0112-201">Response Codes</span></span>

* <span data-ttu-id="b0112-202">**201:** La actividad con señal se envía correctamente.</span><span class="sxs-lookup"><span data-stu-id="b0112-202">**201**: Activity with signal is successfully sent.</span></span> 
* <span data-ttu-id="b0112-203">**401**: Token no válido.</span><span class="sxs-lookup"><span data-stu-id="b0112-203">**401**: Invalid token.</span></span>
* <span data-ttu-id="b0112-204">**403:** La aplicación no puede enviar la señal.</span><span class="sxs-lookup"><span data-stu-id="b0112-204">**403**: The app is unable to send the signal.</span></span> <span data-ttu-id="b0112-205">Esto puede ocurrir debido a diversos motivos, como que el administrador de inquilinos deshabilita la aplicación, la aplicación se bloquea durante la migración del sitio en directo, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="b0112-205">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="b0112-206">En este caso, la carga contiene un mensaje de error detallado.</span><span class="sxs-lookup"><span data-stu-id="b0112-206">In this case, the payload contains a detailed error message.</span></span> 
* <span data-ttu-id="b0112-207">**404**: El chat de reunión no existe.</span><span class="sxs-lookup"><span data-stu-id="b0112-207">**404**: Meeting chat does not exist.</span></span>
 

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="b0112-208">Habilitar la aplicación para reuniones de Teams</span><span class="sxs-lookup"><span data-stu-id="b0112-208">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="b0112-209">Actualizar el manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="b0112-209">Update your app manifest</span></span>

<span data-ttu-id="b0112-210">Las funcionalidades de la aplicación de reuniones se declaran en el manifiesto de la aplicación a través de los  ->  **ámbitos configurableTabs** y las **matrices de** contexto.</span><span class="sxs-lookup"><span data-stu-id="b0112-210">The meetings app capabilities are declared in your app manifest through the **configurableTabs** -> **scopes** and **context** arrays.</span></span> <span data-ttu-id="b0112-211">*El* ámbito define a quién y *el contexto* define dónde estará disponible la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b0112-211">*Scope* defines to whom and *context* defines where your app will be available.</span></span>

> [!NOTE]
> <span data-ttu-id="b0112-212">Usa el [esquema de manifiesto vista previa del desarrollador](../resources/schema/manifest-schema-dev-preview.md) para probar esto en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b0112-212">Please use [Developer Preview manifest schema](../resources/schema/manifest-schema-dev-preview.md) to try this in your app manifest.</span></span>

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
        "meetingSidePanel"
     ]
    }
  ]
```

### <a name="context-property"></a><span data-ttu-id="b0112-213">Context (propiedad)</span><span class="sxs-lookup"><span data-stu-id="b0112-213">Context property</span></span>

<span data-ttu-id="b0112-214">La pestaña `context` y las propiedades funcionan en armonía para permitirte determinar dónde quieres que aparezca la `scopes` aplicación.</span><span class="sxs-lookup"><span data-stu-id="b0112-214">The tab `context` and `scopes` properties work in harmony to allow you to determine where you want your app to appear.</span></span> <span data-ttu-id="b0112-215">Las pestañas del `team` ámbito or pueden tener más de un `groupchat` contexto.</span><span class="sxs-lookup"><span data-stu-id="b0112-215">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="b0112-216">Los valores posibles para la propiedad context son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="b0112-216">The possible values for the context property are as follows:</span></span>

* <span data-ttu-id="b0112-217">**channelTab:** una pestaña en el encabezado de un canal de grupo.</span><span class="sxs-lookup"><span data-stu-id="b0112-217">**channelTab**: a tab in the header of a team channel.</span></span>
* <span data-ttu-id="b0112-218">**privateChatTab:** una pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios que no se encuentra en el contexto de un equipo o reunión.</span><span class="sxs-lookup"><span data-stu-id="b0112-218">**privateChatTab**: a tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span>
* <span data-ttu-id="b0112-219">**meetingChatTab:** una pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios en el contexto de una reunión programada.</span><span class="sxs-lookup"><span data-stu-id="b0112-219">**meetingChatTab**: a tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span>
* <span data-ttu-id="b0112-220">**meetingDetailsTab:** una pestaña en el encabezado de la vista de detalles de la reunión del calendario.</span><span class="sxs-lookup"><span data-stu-id="b0112-220">**meetingDetailsTab**: a tab in the header of the meeting details view of the calendar.</span></span>
* <span data-ttu-id="b0112-221">**meetingSidePanel:** un panel en la reunión abierto a través de la barra unificada (u-bar).</span><span class="sxs-lookup"><span data-stu-id="b0112-221">**meetingSidePanel**: an in-meeting panel opened via the unified bar (u-bar).</span></span>

> [!NOTE]
> <span data-ttu-id="b0112-222">La propiedad "Context" actualmente no es compatible y, por lo tanto, se omitirá en clientes móviles</span><span class="sxs-lookup"><span data-stu-id="b0112-222">"Context" property is currently not supported and thus will be ignored on mobile clients</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="b0112-223">Configurar la aplicación para escenarios de reunión</span><span class="sxs-lookup"><span data-stu-id="b0112-223">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="b0112-224">Para que la aplicación esté visible en la galería de pestañas, debe admitir **pestañas configurables** y el ámbito **de chat de grupo.**</span><span class="sxs-lookup"><span data-stu-id="b0112-224">For your app to be visible in the tab gallery it needs to **support configurable tabs** and the **group chat scope**.</span></span>
>
> * <span data-ttu-id="b0112-225">Los clientes móviles solo admiten pestañas en superficies de reunión previas y posteriores.</span><span class="sxs-lookup"><span data-stu-id="b0112-225">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="b0112-226">Las experiencias en la reunión (cuadro de diálogo y pestaña en la reunión) en el móvil estarán disponibles próximamente.</span><span class="sxs-lookup"><span data-stu-id="b0112-226">The in-meeting experiences (in-meeting dialog and tab) on mobile will be available soon.</span></span> <span data-ttu-id="b0112-227">Siga las [instrucciones para las pestañas en el móvil](../tabs/design/tabs-mobile.md) al crear las pestañas para dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="b0112-227">Follow the [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span>

### <a name="before-a-meeting"></a><span data-ttu-id="b0112-228">Antes de una reunión</span><span class="sxs-lookup"><span data-stu-id="b0112-228">Before a meeting</span></span>

<span data-ttu-id="b0112-229">Los usuarios con roles de organizador y/o moderador agregan pestañas a una reunión con el botón más ➕ en las páginas **de** detalles del chat y la **reunión.**</span><span class="sxs-lookup"><span data-stu-id="b0112-229">Users with organizer and/or presenter roles add tabs to a meeting using the plus ➕ button in the meeting **Chat** and meeting **details** pages.</span></span> <span data-ttu-id="b0112-230">Las extensiones de mensajería se agregan a través del menú puntos suspensivos/desbordamiento &#x25CF;&#x25CF;&#x25CF; se encuentra debajo del área del mensaje de redacción en el chat.</span><span class="sxs-lookup"><span data-stu-id="b0112-230">Messaging extensions are added to via the ellipses/overflow menu &#x25CF;&#x25CF;&#x25CF; located beneath the compose message area in the chat.</span></span> <span data-ttu-id="b0112-231">Los bots se agregan a un chat de reunión con la tecla " " y **@** **seleccionando Obtener bots**.</span><span class="sxs-lookup"><span data-stu-id="b0112-231">Bots are added to a meeting chat using the "**@**" key and selecting **Get bots**.</span></span>

<span data-ttu-id="b0112-232">✔ La identidad del usuario *debe* confirmarse a través de [tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="b0112-232">✔ The user identity *must* be confirmed via [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="b0112-233">Después de esta autenticación, la aplicación puede recuperar el rol de usuario a través de la API GetParticipant.</span><span class="sxs-lookup"><span data-stu-id="b0112-233">Following this authentication, the app can retrieve the user role via the GetParticipant API.</span></span>

 <span data-ttu-id="b0112-234">✔ en función del rol de usuario, la aplicación ahora tendrá la capacidad de presentar experiencias específicas del rol.</span><span class="sxs-lookup"><span data-stu-id="b0112-234">✔ Based on the user role, the app will now have the capability to present role specific experiences.</span></span> <span data-ttu-id="b0112-235">Por ejemplo, una aplicación de sondeo solo puede permitir que los organizadores y los presentadores creen un sondeo nuevo.</span><span class="sxs-lookup"><span data-stu-id="b0112-235">For example, a polling app can allow only organizers and presenters to create a new poll.</span></span>

> <span data-ttu-id="b0112-236">**NOTA:** Las asignaciones de roles se pueden cambiar mientras se está en curso una reunión.</span><span class="sxs-lookup"><span data-stu-id="b0112-236">**NOTE**: Role assignments can be changed while a meeting is in progress.</span></span>  <span data-ttu-id="b0112-237">*Consulte* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span><span class="sxs-lookup"><span data-stu-id="b0112-237">*See* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span> 

### <a name="during-a-meeting"></a><span data-ttu-id="b0112-238">Durante una reunión</span><span class="sxs-lookup"><span data-stu-id="b0112-238">During a meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="b0112-239">**sidePanel**</span><span class="sxs-lookup"><span data-stu-id="b0112-239">**sidePanel**</span></span>

<span data-ttu-id="b0112-240">✔ En el manifiesto de la aplicación, **agregue sidePanel** a la matriz **de** contexto como se describió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b0112-240">✔ In your app manifest add **sidePanel** to the **context** array as described above.</span></span>

<span data-ttu-id="b0112-241">✔ En la reunión, así como en todos los escenarios, la aplicación se representará en una pestaña en la reunión con un ancho de 320 píxeles.</span><span class="sxs-lookup"><span data-stu-id="b0112-241">✔ In the meeting as well as in all scenarios, the app will be rendered in an in-meeting tab that is 320px in width.</span></span> <span data-ttu-id="b0112-242">La pestaña debe estar optimizada para esto.</span><span class="sxs-lookup"><span data-stu-id="b0112-242">Your tab must be optimized for this.</span></span> <span data-ttu-id="b0112-243">*Vea* la [interfaz , FrameContext](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span><span class="sxs-lookup"><span data-stu-id="b0112-243">*See*, [FrameContext interface](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span></span>

<span data-ttu-id="b0112-244">✔Referir al SDK de [Teams](../tabs/how-to/access-teams-context.md#user-context) para usar la API **userContext** para enrutar las solicitudes en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="b0112-244">✔Refer to the [Teams SDK](../tabs/how-to/access-teams-context.md#user-context) to use the **userContext** API to route requests accordingly.</span></span>

<span data-ttu-id="b0112-245">✔ consulte el flujo de [autenticación de Teams para las pestañas](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="b0112-245">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="b0112-246">El flujo de autenticación para pestañas es muy similar al flujo de autenticación para sitios web.</span><span class="sxs-lookup"><span data-stu-id="b0112-246">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="b0112-247">Por lo tanto, las pestañas pueden usar OAuth 2.0 directamente.</span><span class="sxs-lookup"><span data-stu-id="b0112-247">Thus, tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="b0112-248">*Vea también*, Plataforma de identidades de Microsoft y Flujo de código de autorización [de OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span><span class="sxs-lookup"><span data-stu-id="b0112-248">*See also*, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="b0112-249">✔ extensión de mensaje debe funcionar como se esperaba cuando un usuario está en una vista en la reunión y debe poder publicar tarjetas de extensión de mensaje de redacción.</span><span class="sxs-lookup"><span data-stu-id="b0112-249">✔ Message extension should work as expected when a user is in an in-meeting view and should be able to post compose message extension cards.</span></span>

<span data-ttu-id="b0112-250">✔ AppName en la reunión: la información sobre herramientas debe mostrar el nombre de la aplicación en la barra U de la reunión.</span><span class="sxs-lookup"><span data-stu-id="b0112-250">✔ AppName in-meeting - Tooltip should state the app name in-meeting U-bar.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="b0112-251">**Diálogo en la reunión**</span><span class="sxs-lookup"><span data-stu-id="b0112-251">**In-meeting dialog**</span></span>

<span data-ttu-id="b0112-252">✔ Debe cumplir las directrices de diseño del cuadro de [diálogo en la reunión.](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)</span><span class="sxs-lookup"><span data-stu-id="b0112-252">✔ You must adhere to the [in-meeting dialog design guidelines](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

<span data-ttu-id="b0112-253">✔ consulte el flujo de [autenticación de Teams para las pestañas](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="b0112-253">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="b0112-254">✔ use la [API NotificationSignal](create-apps-for-teams-meetings.md#notificationsignal-api) para indicar que es necesario desencadenar una notificación de burbuja.</span><span class="sxs-lookup"><span data-stu-id="b0112-254">✔ Use the [NotificationSignal API](create-apps-for-teams-meetings.md#notificationsignal-api) to signal that a bubble notification needs to be triggered.</span></span>

<span data-ttu-id="b0112-255">✔ Como parte de la carga de la solicitud de notificación, incluya la dirección URL donde se hospeda el contenido que se va a mostrar.</span><span class="sxs-lookup"><span data-stu-id="b0112-255">✔ As part of the notification request payload, include the URL where the content to be showcased is hosted.</span></span>

<span data-ttu-id="b0112-256">✔ cuadro de diálogo En la reunión no debe usar el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="b0112-256">✔ In-meeting dialog must not use task module.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="b0112-257">Estas notificaciones son persistentes en la naturaleza.</span><span class="sxs-lookup"><span data-stu-id="b0112-257">These notifications are persistent in nature.</span></span> <span data-ttu-id="b0112-258">Debe invocar la [**función submitTask() para**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) descartar automáticamente después de que un usuario realiza una acción en la vista web.</span><span class="sxs-lookup"><span data-stu-id="b0112-258">You must invoke the [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to auto-dismiss after a user takes an action in the web-view.</span></span> <span data-ttu-id="b0112-259">Este es un requisito para el envío de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b0112-259">This is a requirement for app submission.</span></span> <span data-ttu-id="b0112-260">*Vea también*, [Sdk de Teams: módulo de tareas](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="b0112-260">*See also*, [Teams SDK: task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
>
> * <span data-ttu-id="b0112-261">Si quieres que la aplicación admita usuarios anónimos, la carga inicial de la solicitud de invocación debe basarse en los metadatos de solicitud (id. del usuario) del objeto, no en los metadatos de solicitud (id. de Azure Active Directory del `from.id` `from` `from.aadObjectId` usuario).</span><span class="sxs-lookup"><span data-stu-id="b0112-261">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id`  (ID of the user) request metadata in the `from` object, not the `from.aadObjectId` (Azure Active Directory ID of the user) request metadata.</span></span> <span data-ttu-id="b0112-262">*Consulte* [Uso de módulos de tareas en pestañas](../task-modules-and-cards/task-modules/task-modules-tabs.md) y Crear y enviar el módulo de [tareas](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span><span class="sxs-lookup"><span data-stu-id="b0112-262">*See* [Using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [Create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

### <a name="after-a-meeting"></a><span data-ttu-id="b0112-263">Después de una reunión</span><span class="sxs-lookup"><span data-stu-id="b0112-263">After a meeting</span></span>

<span data-ttu-id="b0112-264">Las configuraciones posteriores a la reunión y previas a la reunión son equivalentes.</span><span class="sxs-lookup"><span data-stu-id="b0112-264">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="meeting-app-sample"></a><span data-ttu-id="b0112-265">Ejemplo de aplicación de reunión</span><span class="sxs-lookup"><span data-stu-id="b0112-265">Meeting app sample</span></span>

 > [!div class="nextstepaction"]
> [<span data-ttu-id="b0112-266">Aplicación generador de tokens de reunión</span><span class="sxs-lookup"><span data-stu-id="b0112-266">Meeting token generator app</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)

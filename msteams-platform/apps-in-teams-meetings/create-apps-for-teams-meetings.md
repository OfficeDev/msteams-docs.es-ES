---
title: Crear aplicaciones para reuniones de equipos
author: laujan
description: crear aplicaciones para reuniones de teams
ms.topic: conceptual
ms.author: lajanuar
keywords: API de roles de participantes de usuario de reuniones de aplicaciones de teams
ms.openlocfilehash: 7f6d8fec735aa21033c6bcb2462c20458634f10a
ms.sourcegitcommit: 843da1730443ff8474a05295f60a6b376ed140da
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2021
ms.locfileid: "50073099"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="8cfe7-104">Crear aplicaciones para reuniones de Teams</span><span class="sxs-lookup"><span data-stu-id="8cfe7-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="8cfe7-105">Requisitos previos y consideraciones</span><span class="sxs-lookup"><span data-stu-id="8cfe7-105">Prerequisites and considerations</span></span>

* <span data-ttu-id="8cfe7-106">Las aplicaciones en reuniones requieren algunos conocimientos básicos sobre el [desarrollo de aplicaciones de Teams.](../overview.md)</span><span class="sxs-lookup"><span data-stu-id="8cfe7-106">Apps in meetings require some basic knowledge of [Teams app development](../overview.md).</span></span> <span data-ttu-id="8cfe7-107">Una aplicación de una reunión puede incluir [](../messaging-extensions/what-are-messaging-extensions.md) [pestañas,](../tabs/what-are-tabs.md) [bots](../bots/what-are-bots.md)y características de extensiones de mensajería, y requerirá actualizaciones en el manifiesto de la aplicación [de](#update-your-app-manifest) Teams para indicar que la aplicación está disponible para reuniones</span><span class="sxs-lookup"><span data-stu-id="8cfe7-107">An app in a meeting can comprise of [tabs](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md), and [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md) features and will require updates to the Teams [app manifest](#update-your-app-manifest) to indicate that the app is available for meetings</span></span>

* <span data-ttu-id="8cfe7-108">Para que la aplicación funcione en el ciclo de vida de la reunión como una pestaña, debe admitir pestañas configurables en el ámbito [groupchat](../resources/schema/manifest-schema.md#configurabletabs) (consulta cómo crear una [pestaña de grupo).](../build-your-first-app/build-channel-tab.md)</span><span class="sxs-lookup"><span data-stu-id="8cfe7-108">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) (see how to [build a group tab](../build-your-first-app/build-channel-tab.md)).</span></span> <span data-ttu-id="8cfe7-109">La compatibilidad con `groupchat` el ámbito habilitará la aplicación en [chats](teams-apps-in-meetings.md#pre-meeting-app-experience) previos a la reunión y posteriores a [la](teams-apps-in-meetings.md#post-meeting-app-experience) reunión.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-109">Supporting the `groupchat` scope will enable your app in [pre-meeting](teams-apps-in-meetings.md#pre-meeting-app-experience) and [post-meeting](teams-apps-in-meetings.md#post-meeting-app-experience) chats.</span></span>

* <span data-ttu-id="8cfe7-110">Los parámetros de dirección URL de la API de reunión pueden requerir y tenantId están disponibles como parte del SDK de cliente de Teams y la actividad `meetingId` `userId` de bots. [](/onedrive/find-your-office-365-tenant-id)</span><span class="sxs-lookup"><span data-stu-id="8cfe7-110">Meeting API URL parameters may require `meetingId`, `userId`, and the [tenantId](/onedrive/find-your-office-365-tenant-id) These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="8cfe7-111">Además, se puede recuperar información confiable para el identificador de usuario y el identificador de inquilino mediante la autenticación [sso de pestaña.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="8cfe7-111">Additionally, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="8cfe7-112">Algunas API de reunión, como , requieren un registro de bot y `GetParticipant` [un identificador](../build-your-first-app/build-bot.md) para generar tokens de autenticación.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-112">Some meeting APIs, such as `GetParticipant`, require a [bot registration and ID](../build-your-first-app/build-bot.md) to generate auth tokens.</span></span>

* <span data-ttu-id="8cfe7-113">Debe cumplir con las directrices generales [de diseño de pestañas de Teams](../tabs/design/tabs.md) para escenarios previos y posteriores a la reunión.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-113">You must adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios.</span></span> <span data-ttu-id="8cfe7-114">Para obtener experiencias durante las reuniones, consulte las directrices de [diseño](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) de la pestaña en la reunión y del cuadro [de diálogo](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) en la reunión.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-114">For experiences during meetings, refer to the [in-meeting tab](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) and [in-meeting dialog](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) design guidelines.</span></span>

* <span data-ttu-id="8cfe7-115">Para que la aplicación se actualice en tiempo real, debe estar actualizada en función de las actividades del evento en la reunión.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-115">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="8cfe7-116">Estos eventos pueden estar dentro del cuadro de diálogo en la reunión (consulte el parámetro de finalización en ) y `bot Id` otras superficies durante el ciclo `Notification Signal API` de vida de la reunión</span><span class="sxs-lookup"><span data-stu-id="8cfe7-116">These events can be within the in-meeting dialog (refer to completion `bot Id` parameter in `Notification Signal API`) and other surfaces across the meeting lifecycle</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="8cfe7-117">Referencia de API de aplicaciones de reunión</span><span class="sxs-lookup"><span data-stu-id="8cfe7-117">Meeting apps API reference</span></span>

|<span data-ttu-id="8cfe7-118">API</span><span class="sxs-lookup"><span data-stu-id="8cfe7-118">API</span></span>|<span data-ttu-id="8cfe7-119">Descripción</span><span class="sxs-lookup"><span data-stu-id="8cfe7-119">Description</span></span>|<span data-ttu-id="8cfe7-120">Solicitud</span><span class="sxs-lookup"><span data-stu-id="8cfe7-120">Request</span></span>|<span data-ttu-id="8cfe7-121">Origen</span><span class="sxs-lookup"><span data-stu-id="8cfe7-121">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="8cfe7-122">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="8cfe7-122">**GetUserContext**</span></span>| <span data-ttu-id="8cfe7-123">Obtenga información contextual para mostrar contenido relevante en una pestaña de Teams.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-123">Get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="8cfe7-124">_**microsoftTeams.getContext( ( ) => { /*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="8cfe7-124">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="8cfe7-125">SDK de cliente de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8cfe7-125">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="8cfe7-126">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="8cfe7-126">**GetParticipant**</span></span>|<span data-ttu-id="8cfe7-127">Esta API permite que un bot obtenga información de un participante por identificador de reunión e identificador de participante.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-127">This API allows a bot to fetch a participant information by meeting id and participant id.</span></span>|<span data-ttu-id="8cfe7-128">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="8cfe7-128">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="8cfe7-129">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="8cfe7-129">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="8cfe7-130">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="8cfe7-130">**NotificationSignal**</span></span> |<span data-ttu-id="8cfe7-131">Las señales de reunión se entregarán mediante la siguiente API de notificación de conversación existente (para chat de bot de usuario).</span><span class="sxs-lookup"><span data-stu-id="8cfe7-131">Meeting signals will be delivered using the following existing conversation notification API (for user-bot chat).</span></span> <span data-ttu-id="8cfe7-132">Esta API permite a los desarrolladores señalar en función de la acción del usuario final para mostrar en caso de que se muestre una burbuja de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-132">This API allows developers to signal based on end-user action to show-case an in-meeting dialog bubble.</span></span>|<span data-ttu-id="8cfe7-133">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="8cfe7-133">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="8cfe7-134">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="8cfe7-134">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="8cfe7-135">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="8cfe7-135">GetUserContext</span></span>

<span data-ttu-id="8cfe7-136">Consulte nuestro artículo Obtener contexto para la documentación de la [pestaña de Teams](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) para obtener instrucciones sobre cómo identificar y recuperar información contextual para el contenido de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-136">Please refer to our [Get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and  retrieving contextual information for your tab content.</span></span> <span data-ttu-id="8cfe7-137">Como parte de la extensibilidad de reuniones, se ha agregado un nuevo valor para la carga de respuesta:</span><span class="sxs-lookup"><span data-stu-id="8cfe7-137">As part of meetings extensibility, a new value has been added for the response payload:</span></span>

<span data-ttu-id="8cfe7-138">✔ **meetingId:** se usa en una pestaña cuando se ejecuta en el contexto de la reunión.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-138">✔ **meetingId**: used by a tab when running in the meeting context.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="8cfe7-139">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="8cfe7-139">GetParticipant API</span></span>

> [!NOTE]
>
> * <span data-ttu-id="8cfe7-140">No almacenar en caché los roles de los participantes, ya que el organizador de la reunión puede cambiar un rol en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-140">Do not cache participant roles since the meeting organizer can change a role at any point in time.</span></span>
>
> * <span data-ttu-id="8cfe7-141">Actualmente, Teams no admite listas de distribución grandes ni tamaños de lista de más de 350 participantes para la `GetParticipant` API.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-141">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="8cfe7-142">Parámetros de consulta</span><span class="sxs-lookup"><span data-stu-id="8cfe7-142">Query parameters</span></span>

|<span data-ttu-id="8cfe7-143">Valor</span><span class="sxs-lookup"><span data-stu-id="8cfe7-143">Value</span></span>|<span data-ttu-id="8cfe7-144">Tipo</span><span class="sxs-lookup"><span data-stu-id="8cfe7-144">Type</span></span>|<span data-ttu-id="8cfe7-145">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8cfe7-145">Required</span></span>|<span data-ttu-id="8cfe7-146">Descripción</span><span class="sxs-lookup"><span data-stu-id="8cfe7-146">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="8cfe7-147">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="8cfe7-147">**meetingId**</span></span>| <span data-ttu-id="8cfe7-148">string</span><span class="sxs-lookup"><span data-stu-id="8cfe7-148">string</span></span> | <span data-ttu-id="8cfe7-149">Sí</span><span class="sxs-lookup"><span data-stu-id="8cfe7-149">Yes</span></span> | <span data-ttu-id="8cfe7-150">El identificador de reunión está disponible a través de Bot Invoke y el SDK de cliente de Teams.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-150">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="8cfe7-151">**participantId**</span><span class="sxs-lookup"><span data-stu-id="8cfe7-151">**participantId**</span></span>| <span data-ttu-id="8cfe7-152">string</span><span class="sxs-lookup"><span data-stu-id="8cfe7-152">string</span></span> | <span data-ttu-id="8cfe7-153">Sí</span><span class="sxs-lookup"><span data-stu-id="8cfe7-153">Yes</span></span> | <span data-ttu-id="8cfe7-154">El participantId es el identificador de usuario.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-154">The participantId is the user ID.</span></span> <span data-ttu-id="8cfe7-155">Está disponible en sso de pestaña, invocación de bot y SDK de cliente de Teams.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-155">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="8cfe7-156">Se recomienda encarecidamente obtener un participantId del SSO de pestaña.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-156">It is highly recommended to get a participantId from the Tab SSO.</span></span> |
|<span data-ttu-id="8cfe7-157">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="8cfe7-157">**tenantId**</span></span>| <span data-ttu-id="8cfe7-158">string</span><span class="sxs-lookup"><span data-stu-id="8cfe7-158">string</span></span> | <span data-ttu-id="8cfe7-159">Sí</span><span class="sxs-lookup"><span data-stu-id="8cfe7-159">Yes</span></span> | <span data-ttu-id="8cfe7-160">El tenantId es necesario para los usuarios del espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-160">The tenantId is required for the tenant users.</span></span> <span data-ttu-id="8cfe7-161">Está disponible en sso de pestaña, invocación de bot y SDK de cliente de Teams.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-161">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="8cfe7-162">Se recomienda encarecidamente obtener un tenantId del SSO de pestaña.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-162">It is highly recommended to get a tenantId from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="8cfe7-163">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8cfe7-163">Example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8cfe7-164">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8cfe7-164">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="8cfe7-165">JavaScript</span><span class="sxs-lookup"><span data-stu-id="8cfe7-165">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="8cfe7-166">JSON</span><span class="sxs-lookup"><span data-stu-id="8cfe7-166">JSON</span></span>](#tab/json)

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

<span data-ttu-id="8cfe7-167">El cuerpo de la respuesta es:</span><span class="sxs-lookup"><span data-stu-id="8cfe7-167">The response body is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="8cfe7-168">Códigos de respuesta</span><span class="sxs-lookup"><span data-stu-id="8cfe7-168">Response codes</span></span>

* <span data-ttu-id="8cfe7-169">**403**: La aplicación no puede obtener información de participantes.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-169">**403**: The app is not allowed to get participant information.</span></span>  <span data-ttu-id="8cfe7-170">Esta es la respuesta de error más común y se desencadena si la aplicación no está instalada en la reunión.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-170">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="8cfe7-171">Por ejemplo, si la aplicación está deshabilitada por el administrador de inquilinos o bloqueada durante la migración de sitios en directo.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-171">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>
* <span data-ttu-id="8cfe7-172">**200**: La información de los participantes se recuperó correctamente.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-172">**200**: Participant information successfully retrieved.</span></span>
* <span data-ttu-id="8cfe7-173">**401**: Token no válido.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-173">**401**: Invalid token.</span></span>
* <span data-ttu-id="8cfe7-174">**404**: No se encuentra el participante.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-174">**404**: Participant cannot be found.</span></span>
* <span data-ttu-id="8cfe7-175">**500**: La reunión ha expirado (más de 60 días desde que finalizó la reunión) o el participante no tiene permisos en función de su rol.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-175">**500**: The meeting has either expired (more than 60 days since the meeting ended) or the participant does not have permissions based on their role.</span></span>


<span data-ttu-id="8cfe7-176">**Próximamente**</span><span class="sxs-lookup"><span data-stu-id="8cfe7-176">**Coming Soon**</span></span>

* <span data-ttu-id="8cfe7-177">**404**: La reunión ha expirado o no se encuentra el participante.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-177">**404**: The meeting has either expired or participant cannot be found.</span></span>


### <a name="notificationsignal-api"></a><span data-ttu-id="8cfe7-178">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="8cfe7-178">NotificationSignal API</span></span>

> [!NOTE]
> <span data-ttu-id="8cfe7-179">Cuando se invoca un cuadro de diálogo en la reunión, también se presentará el mismo contenido como mensaje de chat.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-179">When an in-meeting dialog is invoked, the same content will also be presented as a chat message.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="8cfe7-180">Parámetros de consulta</span><span class="sxs-lookup"><span data-stu-id="8cfe7-180">Query parameters</span></span>

|<span data-ttu-id="8cfe7-181">Valor</span><span class="sxs-lookup"><span data-stu-id="8cfe7-181">Value</span></span>|<span data-ttu-id="8cfe7-182">Tipo</span><span class="sxs-lookup"><span data-stu-id="8cfe7-182">Type</span></span>|<span data-ttu-id="8cfe7-183">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8cfe7-183">Required</span></span>|<span data-ttu-id="8cfe7-184">Descripción</span><span class="sxs-lookup"><span data-stu-id="8cfe7-184">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="8cfe7-185">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="8cfe7-185">**conversationId**</span></span>| <span data-ttu-id="8cfe7-186">string</span><span class="sxs-lookup"><span data-stu-id="8cfe7-186">string</span></span> | <span data-ttu-id="8cfe7-187">Sí</span><span class="sxs-lookup"><span data-stu-id="8cfe7-187">Yes</span></span> | <span data-ttu-id="8cfe7-188">El identificador de conversación está disponible como parte de la invocación de bot</span><span class="sxs-lookup"><span data-stu-id="8cfe7-188">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="example"></a><span data-ttu-id="8cfe7-189">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8cfe7-189">Example</span></span>

> [!NOTE]
>
<span data-ttu-id="8cfe7-190">El `completionBotId` parámetro del parámetro es opcional en el ejemplo de carga `externalResourceUrl` solicitada.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-190">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="8cfe7-191">`Bot ID` se declara en el manifiesto y el bot recibe un objeto de resultado.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-191">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="8cfe7-192">Los parámetros de ancho y alto externalResourceUrl deben estar en píxeles.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-192">The externalResourceUrl width and height parameters must be in pixels.</span></span> <span data-ttu-id="8cfe7-193">Consulte las [directrices de diseño](design/designing-apps-in-meetings.md) para asegurarse de que las dimensiones se encuentran dentro de los límites permitidos.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-193">Refer to the [design guidelines](design/designing-apps-in-meetings.md) to ensure the dimensions are within the allowed limits.</span></span>
> * <span data-ttu-id="8cfe7-194">La dirección URL es la página cargada como un `<iframe>` cuadro de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-194">The URL is the page loaded as an `<iframe>` in the in-meeting dialog.</span></span> <span data-ttu-id="8cfe7-195">El dominio debe estar en la matriz de la `validDomains` aplicación en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-195">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8cfe7-196">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8cfe7-196">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="8cfe7-197">JavaScript</span><span class="sxs-lookup"><span data-stu-id="8cfe7-197">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="8cfe7-198">JSON</span><span class="sxs-lookup"><span data-stu-id="8cfe7-198">JSON</span></span>](#tab/json)

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

#### <a name="response-codes"></a><span data-ttu-id="8cfe7-199">Códigos de respuesta</span><span class="sxs-lookup"><span data-stu-id="8cfe7-199">Response Codes</span></span>

* <span data-ttu-id="8cfe7-200">**201:** la actividad con señal se envía correctamente</span><span class="sxs-lookup"><span data-stu-id="8cfe7-200">**201**: activity with signal is successfully sent</span></span>  
* <span data-ttu-id="8cfe7-201">**401**: token no válido</span><span class="sxs-lookup"><span data-stu-id="8cfe7-201">**401**: invalid token</span></span>  
* <span data-ttu-id="8cfe7-202">**201**: La actividad con señal se envía correctamente.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-202">**201**: Activity with signal is successfully sent.</span></span> 
* <span data-ttu-id="8cfe7-203">**401**: Token no válido.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-203">**401**: Invalid token.</span></span>
* <span data-ttu-id="8cfe7-204">**403**: La aplicación no puede enviar la señal.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-204">**403**: The app is unable to send the signal.</span></span> <span data-ttu-id="8cfe7-205">Esto puede ocurrir debido a diversos motivos, como que el administrador de inquilinos deshabilite la aplicación, la aplicación se bloquee durante la migración de sitios en directo, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-205">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="8cfe7-206">En este caso, la carga contiene un mensaje de error detallado.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-206">In this case, the payload contains a detailed error message.</span></span> 
* <span data-ttu-id="8cfe7-207">**404**: El chat de la reunión no existe.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-207">**404**: Meeting chat doesn't exist.</span></span>
 

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="8cfe7-208">Habilitar la aplicación para reuniones de Teams</span><span class="sxs-lookup"><span data-stu-id="8cfe7-208">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="8cfe7-209">Actualizar el manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="8cfe7-209">Update your app manifest</span></span>

<span data-ttu-id="8cfe7-210">Las funcionalidades de la aplicación de reuniones se declaran en el manifiesto de la aplicación a través de los  ->  **ámbitos configurableTabs** y matrices de contexto. </span><span class="sxs-lookup"><span data-stu-id="8cfe7-210">The meetings app capabilities are declared in your app manifest via the **configurableTabs** -> **scopes** and **context** arrays.</span></span> <span data-ttu-id="8cfe7-211">*El* ámbito define a quién y *el contexto* define dónde estará disponible la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-211">*Scope* defines to whom and *context* defines where your app will be available.</span></span>

> [!NOTE]
> <span data-ttu-id="8cfe7-212">Usa el esquema [de manifiesto de Developer Preview](../resources/schema/manifest-schema-dev-preview.md) para probar esto en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-212">Please use [Developer Preview manifest schema](../resources/schema/manifest-schema-dev-preview.md) to try this in your app manifest.</span></span>

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

### <a name="context-property"></a><span data-ttu-id="8cfe7-213">Context (propiedad)</span><span class="sxs-lookup"><span data-stu-id="8cfe7-213">Context property</span></span>

<span data-ttu-id="8cfe7-214">La pestaña `context` y las propiedades funcionan en armonía para permitirte determinar dónde quieres que aparezca la `scopes` aplicación.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-214">The tab `context` and `scopes` properties work in harmony to allow you to determine where you want your app to appear.</span></span> <span data-ttu-id="8cfe7-215">Las pestañas del `team` ámbito o pueden tener más de un `groupchat` contexto.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-215">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="8cfe7-216">Los valores posibles para la propiedad context son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="8cfe7-216">The possible values for the context property are as follows:</span></span>

* <span data-ttu-id="8cfe7-217">**channelTab:** una pestaña en el encabezado de un canal de equipo.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-217">**channelTab**: a tab in the header of a team channel.</span></span>
* <span data-ttu-id="8cfe7-218">**privateChatTab:** una pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios que no se encuentra en el contexto de un equipo o reunión.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-218">**privateChatTab**: a tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span>
* <span data-ttu-id="8cfe7-219">**meetingChatTab:** una pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios en el contexto de una reunión programada.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-219">**meetingChatTab**: a tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span>
* <span data-ttu-id="8cfe7-220">**meetingDetailsTab:** una pestaña en el encabezado de la vista de detalles de la reunión del calendario.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-220">**meetingDetailsTab**: a tab in the header of the meeting details view of the calendar.</span></span>
* <span data-ttu-id="8cfe7-221">**meetingSidePanel:** un panel en la reunión abierto a través de la barra unificada (barra u).</span><span class="sxs-lookup"><span data-stu-id="8cfe7-221">**meetingSidePanel**: an in-meeting panel opened via the unified bar (u-bar).</span></span>

> [!NOTE]
> <span data-ttu-id="8cfe7-222">La propiedad "Context" no se admite actualmente y, por lo tanto, se omitirá en los clientes móviles</span><span class="sxs-lookup"><span data-stu-id="8cfe7-222">"Context" property is currently not supported and thus will be ignored on mobile clients</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="8cfe7-223">Configurar la aplicación para escenarios de reuniones</span><span class="sxs-lookup"><span data-stu-id="8cfe7-223">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="8cfe7-224">Para que la aplicación esté visible en la galería de pestañas, necesita admitir **pestañas configurables** y el ámbito **de chat en grupo.**</span><span class="sxs-lookup"><span data-stu-id="8cfe7-224">For your app to be visible in the tab gallery it needs to **support configurable tabs** and the **group chat scope**.</span></span>
>
> * <span data-ttu-id="8cfe7-225">Los clientes móviles solo admiten pestañas en superficies de reuniones previas y posteriores.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-225">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="8cfe7-226">Las experiencias en la reunión (cuadro de diálogo y pestaña en la reunión) en dispositivos móviles estarán disponibles próximamente.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-226">The in-meeting experiences (in-meeting dialog and tab) on mobile will be available soon.</span></span> <span data-ttu-id="8cfe7-227">Siga las [instrucciones para pestañas en dispositivos móviles](../tabs/design/tabs-mobile.md) al crear las pestañas para móviles.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-227">Follow the [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span>

### <a name="before-a-meeting"></a><span data-ttu-id="8cfe7-228">Antes de una reunión</span><span class="sxs-lookup"><span data-stu-id="8cfe7-228">Before a meeting</span></span>

<span data-ttu-id="8cfe7-229">Los usuarios con roles de organizador y/o moderador agregan pestañas a una reunión con el botón más ➕ en las páginas **de** detalles de chat y **reunión.**</span><span class="sxs-lookup"><span data-stu-id="8cfe7-229">Users with organizer and/or presenter roles add tabs to a meeting using the plus ➕ button in the meeting **Chat** and meeting **details** pages.</span></span> <span data-ttu-id="8cfe7-230">Las extensiones de mensajería se agregan a través del menú de puntos suspensivos o desbordamiento &#x25CF;&#x25CF;&#x25CF; situado debajo del área de redacción de mensajes en el chat.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-230">Messaging extensions are added to via the ellipses/overflow menu &#x25CF;&#x25CF;&#x25CF; located beneath the compose message area in the chat.</span></span> <span data-ttu-id="8cfe7-231">Bots are added to a meeting chat using the **@** " " key and selecting Get **bots**.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-231">Bots are added to a meeting chat using the "**@**" key and selecting **Get bots**.</span></span>

<span data-ttu-id="8cfe7-232">✔ la identidad del usuario *debe* confirmarse a través de [SSO de pestañas.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="8cfe7-232">✔ The user identity *must* be confirmed via [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="8cfe7-233">Después de esta autenticación, la aplicación puede recuperar el rol de usuario a través de la API GetParticipant.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-233">Following this authentication, the app can retrieve the user role via the GetParticipant API.</span></span>

 <span data-ttu-id="8cfe7-234">✔ en función del rol de usuario, la aplicación ahora tendrá la capacidad de presentar experiencias específicas de roles.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-234">✔ Based on the user role, the app will now have the capability to present role specific experiences.</span></span> <span data-ttu-id="8cfe7-235">Por ejemplo, una aplicación de sondeo solo puede permitir a los organizadores y presentadores crear un nuevo sondeo.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-235">For example, a polling app can allow only organizers and presenters to create a new poll.</span></span>

> <span data-ttu-id="8cfe7-236">**NOTA:** Las asignaciones de roles se pueden cambiar mientras hay una reunión en curso.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-236">**NOTE**: Role assignments can be changed while a meeting is in progress.</span></span>  <span data-ttu-id="8cfe7-237">*Vea* [Roles en una reunión de Teams.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="8cfe7-237">*See* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span> 

### <a name="during-a-meeting"></a><span data-ttu-id="8cfe7-238">Durante una reunión</span><span class="sxs-lookup"><span data-stu-id="8cfe7-238">During a meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="8cfe7-239">**sidePanel**</span><span class="sxs-lookup"><span data-stu-id="8cfe7-239">**sidePanel**</span></span>

<span data-ttu-id="8cfe7-240">✔ en el manifiesto de la aplicación, **agrega sidePanel** a **la** matriz de contexto como se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-240">✔ In your app manifest add **sidePanel** to the **context** array as described above.</span></span>

<span data-ttu-id="8cfe7-241">✔ en la reunión, así como en todos los escenarios, la aplicación se representará en una pestaña de reunión de 320 píxeles de ancho.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-241">✔ In the meeting as well as in all scenarios, the app will be rendered in an in-meeting tab that is 320px in width.</span></span> <span data-ttu-id="8cfe7-242">La pestaña debe estar optimizada para esto.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-242">Your tab must be optimized for this.</span></span> <span data-ttu-id="8cfe7-243">*Consulta la* interfaz [, FrameContext](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span><span class="sxs-lookup"><span data-stu-id="8cfe7-243">*See*, [FrameContext interface](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span></span>

<span data-ttu-id="8cfe7-244">✔referir al SDK de [Teams](../tabs/how-to/access-teams-context.md#user-context) para usar la API **userContext** para enrutar las solicitudes en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-244">✔Refer to the [Teams SDK](../tabs/how-to/access-teams-context.md#user-context) to use the **userContext** API to route requests accordingly.</span></span>

<span data-ttu-id="8cfe7-245">✔ consulte el flujo de [autenticación de Teams para ver las pestañas.](../tabs/how-to/authentication/auth-flow-tab.md)</span><span class="sxs-lookup"><span data-stu-id="8cfe7-245">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="8cfe7-246">El flujo de autenticación para pestañas es muy similar al flujo de autenticación para sitios web.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-246">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="8cfe7-247">Por lo tanto, las pestañas pueden usar OAuth 2.0 directamente.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-247">Thus, tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="8cfe7-248">*Vea también ,* plataforma de identidad de Microsoft y flujo de código de autorización de [OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span><span class="sxs-lookup"><span data-stu-id="8cfe7-248">*See also*, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="8cfe7-249">✔ extensión de mensaje debe funcionar según lo esperado cuando un usuario está en una vista en la reunión y debe poder publicar tarjetas de extensión de mensaje de redacción.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-249">✔ Message extension should work as expected when a user is in an in-meeting view and should be able to post compose message extension cards.</span></span>

<span data-ttu-id="8cfe7-250">✔ AppName en la reunión: la información sobre herramientas debe mostrar el nombre de la aplicación en la barra U de la reunión.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-250">✔ AppName in-meeting - Tooltip should state the app name in-meeting U-bar.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="8cfe7-251">**Diálogo en la reunión**</span><span class="sxs-lookup"><span data-stu-id="8cfe7-251">**In-meeting dialog**</span></span>

<span data-ttu-id="8cfe7-252">✔ debe cumplir las directrices de diseño del cuadro de [diálogo en la reunión.](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)</span><span class="sxs-lookup"><span data-stu-id="8cfe7-252">✔ You must adhere to the [in-meeting dialog design guidelines](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

<span data-ttu-id="8cfe7-253">✔ consulte el flujo de [autenticación de Teams para ver las pestañas.](../tabs/how-to/authentication/auth-flow-tab.md)</span><span class="sxs-lookup"><span data-stu-id="8cfe7-253">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="8cfe7-254">✔ usar la [API NotificationSignal para](create-apps-for-teams-meetings.md#notificationsignal-api) indicar que es necesario desencadenar una notificación de burbuja.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-254">✔ Use the [NotificationSignal API](create-apps-for-teams-meetings.md#notificationsignal-api) to signal that a bubble notification needs to be triggered.</span></span>

<span data-ttu-id="8cfe7-255">✔ como parte de la carga de la solicitud de notificación, incluya la dirección URL donde se hospeda el contenido que se va a presentar.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-255">✔ As part of the notification request payload, include the URL where the content to be showcased is hosted.</span></span>

<span data-ttu-id="8cfe7-256">✔ cuadro de diálogo En reunión no debe usar el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-256">✔ In-meeting dialog must not use task module.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="8cfe7-257">Estas notificaciones son persistentes por naturaleza.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-257">These notifications are persistent in nature.</span></span> <span data-ttu-id="8cfe7-258">Debe invocar la función [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) para descartar automáticamente después de que un usuario realiza una acción en la vista web.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-258">You must invoke the [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to auto-dismiss after a user takes an action in the web-view.</span></span> <span data-ttu-id="8cfe7-259">Este es un requisito para el envío de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-259">This is a requirement for app submission.</span></span> <span data-ttu-id="8cfe7-260">*Vea también*, [SDK de Teams: módulo de tareas.](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="8cfe7-260">*See also*, [Teams SDK: task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
>
> * <span data-ttu-id="8cfe7-261">Si desea que la aplicación admita usuarios anónimos, la carga inicial de la solicitud de invocación debe basarse en los metadatos de solicitud (id. del usuario) en el objeto, no en los metadatos de solicitud (id. de Azure Active Directory del `from.id` `from` `from.aadObjectId` usuario).</span><span class="sxs-lookup"><span data-stu-id="8cfe7-261">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id`  (ID of the user) request metadata in the `from` object, not the `from.aadObjectId` (Azure Active Directory ID of the user) request metadata.</span></span> <span data-ttu-id="8cfe7-262">*Vea* [Usar módulos de tareas en pestañas](../task-modules-and-cards/task-modules/task-modules-tabs.md) [y Crear y enviar el módulo de tareas.](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)</span><span class="sxs-lookup"><span data-stu-id="8cfe7-262">*See* [Using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [Create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

### <a name="after-a-meeting"></a><span data-ttu-id="8cfe7-263">Después de una reunión</span><span class="sxs-lookup"><span data-stu-id="8cfe7-263">After a meeting</span></span>

<span data-ttu-id="8cfe7-264">Las configuraciones posteriores a la reunión y previas a la reunión son equivalentes.</span><span class="sxs-lookup"><span data-stu-id="8cfe7-264">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="meeting-app-sample"></a><span data-ttu-id="8cfe7-265">Ejemplo de aplicación de reunión</span><span class="sxs-lookup"><span data-stu-id="8cfe7-265">Meeting app sample</span></span>

 > [!div class="nextstepaction"]
> [<span data-ttu-id="8cfe7-266">Aplicación generador de tokens de reunión</span><span class="sxs-lookup"><span data-stu-id="8cfe7-266">Meeting token generator app</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)

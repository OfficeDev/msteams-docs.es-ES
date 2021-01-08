---
title: Crear aplicaciones para reuniones de equipos
author: laujan
description: creación de aplicaciones para reuniones de Microsoft Teams
ms.topic: conceptual
ms.author: lajanuar
keywords: API de las aplicaciones de Microsoft Teams rol de participante de usuario
ms.openlocfilehash: e768c2dc6722d006c89927adfe60e03243a076d0
ms.sourcegitcommit: f0dfae429385ef02f61896ad49172c4803ef6622
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/31/2020
ms.locfileid: "49740874"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="40a37-104">Crear aplicaciones para reuniones de Teams</span><span class="sxs-lookup"><span data-stu-id="40a37-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="40a37-105">Requisitos previos y consideraciones</span><span class="sxs-lookup"><span data-stu-id="40a37-105">Prerequisites and considerations</span></span>

1. <span data-ttu-id="40a37-106">Las aplicaciones en las reuniones necesitan conocimientos básicos del desarrollo de aplicaciones de Microsoft [Teams](../overview.md).</span><span class="sxs-lookup"><span data-stu-id="40a37-106">Apps in meetings require some basic knowledge of [Teams app development](../overview.md).</span></span> <span data-ttu-id="40a37-107">Una aplicación en una reunión puede estar formada por [pestañas](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md)y características de [extensiones de mensajería](../messaging-extensions/what-are-messaging-extensions.md) y necesitará actualizaciones en el manifiesto de la [aplicación](#update-your-app-manifest) de Microsoft Teams para indicar que la aplicación está disponible para las reuniones.</span><span class="sxs-lookup"><span data-stu-id="40a37-107">An app in a meeting can comprise of [tabs](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md), and [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md) features and will require updates to the Teams [app manifest](#update-your-app-manifest) to indicate that the app is available for meetings</span></span>

1. <span data-ttu-id="40a37-108">Para que la aplicación funcione en el ciclo de vida de la reunión como una pestaña, debe admitir pestañas configurables en el [ámbito Groupchat](../resources/schema/manifest-schema.md#configurabletabs).</span><span class="sxs-lookup"><span data-stu-id="40a37-108">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs).</span></span> <span data-ttu-id="40a37-109">*Consulte* [ampliar la aplicación de Microsoft Teams con una pestaña personalizada](../tabs/how-to/add-tab.md). Admitir el `groupchat` ámbito habilitará la aplicación en chats [anteriores](teams-apps-in-meetings.md#pre-meeting-app-experience) y [posteriores](teams-apps-in-meetings.md#post-meeting-app-experience) a la reunión.</span><span class="sxs-lookup"><span data-stu-id="40a37-109">*See* [Extend your Teams app with a custom tab](../tabs/how-to/add-tab.md). Supporting the `groupchat` scope will enable your app in [pre-meeting](teams-apps-in-meetings.md#pre-meeting-app-experience) and [post-meeting](teams-apps-in-meetings.md#post-meeting-app-experience) chats.</span></span>

1. <span data-ttu-id="40a37-110">Los parámetros de dirección URL `meetingId` de la API de la reunión pueden requerir, `userId` y el [tenantId](/onedrive/find-your-office-365-tenant-id) , están disponibles como parte de la actividad del SDK del cliente de Microsoft Teams y del bot.</span><span class="sxs-lookup"><span data-stu-id="40a37-110">Meeting API URL parameters may require `meetingId`, `userId`, and the [tenantId](/onedrive/find-your-office-365-tenant-id) These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="40a37-111">Además, se puede recuperar información fiable sobre el identificador de usuario y el identificador de inquilino mediante la [autenticación SSO de pestañas](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="40a37-111">Additionally, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

1. <span data-ttu-id="40a37-112">Algunas API de reunión, como `GetParticipant` requerirán un [registro de Bot y un identificador de aplicación de bot](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) para generar tokens de autenticación.</span><span class="sxs-lookup"><span data-stu-id="40a37-112">Some meeting APIs, such as `GetParticipant` will require a [bot registration and bot app ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) to generate auth tokens.</span></span>

1. <span data-ttu-id="40a37-113">Como desarrollador, debe adherirse a las directrices generales de [diseño de pestañas de Microsoft Teams](../tabs/design/tabs.md) para los escenarios anteriores y posteriores a la reunión, así como las directrices de [diálogo en reunión](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) para los diálogos que se desencadenan durante la reunión de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="40a37-113">As a developer, you must adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios as well as the [in-meeting dialog guidelines](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) for in-meeting dialog triggered during a Teams meeting.</span></span>

1. <span data-ttu-id="40a37-114">Tenga en cuenta que para que su aplicación se actualice en tiempo real, debe estar actualizada en función de las actividades de eventos de la reunión.</span><span class="sxs-lookup"><span data-stu-id="40a37-114">Please note that in order for your app to be updated in real-time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="40a37-115">Estos eventos pueden estar en el cuadro de diálogo de la reunión (consulte parámetro de finalización `bot Id` en `Notification Signal API` ) y otras superficies en el ciclo de vida de la reunión.</span><span class="sxs-lookup"><span data-stu-id="40a37-115">These events can be within the in-meeting dialog (refer to completion `bot Id` parameter in `Notification Signal API`) and other surfaces across the meeting lifecycle</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="40a37-116">Referencia de API de las aplicaciones de reunión</span><span class="sxs-lookup"><span data-stu-id="40a37-116">Meeting apps API reference</span></span>

|<span data-ttu-id="40a37-117">API</span><span class="sxs-lookup"><span data-stu-id="40a37-117">API</span></span>|<span data-ttu-id="40a37-118">Descripción</span><span class="sxs-lookup"><span data-stu-id="40a37-118">Description</span></span>|<span data-ttu-id="40a37-119">Solicitud</span><span class="sxs-lookup"><span data-stu-id="40a37-119">Request</span></span>|<span data-ttu-id="40a37-120">Origen</span><span class="sxs-lookup"><span data-stu-id="40a37-120">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="40a37-121">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="40a37-121">**GetUserContext**</span></span>| <span data-ttu-id="40a37-122">Obtener información contextual para mostrar contenido relevante en una pestaña de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="40a37-122">Get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="40a37-123">_**Microsoft Teams. getContext (() => {/*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="40a37-123">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="40a37-124">SDK del cliente de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="40a37-124">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="40a37-125">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="40a37-125">**GetParticipant**</span></span>|<span data-ttu-id="40a37-126">Esta API permite que un bot obtenga información de un participante por el identificador de la reunión y el identificador del participante.</span><span class="sxs-lookup"><span data-stu-id="40a37-126">This API allows a bot to fetch a participant information by meeting id and participant id.</span></span>|<span data-ttu-id="40a37-127">**Get** _**/v1/Meetings/{meetingId}/participants/{participantId}? tenantid = {tenantid}**_</span><span class="sxs-lookup"><span data-stu-id="40a37-127">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="40a37-128">SDK de Microsoft bot Framework</span><span class="sxs-lookup"><span data-stu-id="40a37-128">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="40a37-129">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="40a37-129">**NotificationSignal**</span></span> |<span data-ttu-id="40a37-130">Las señales de reunión se entregarán con la siguiente API de notificación de conversación existente (para el chat de bot? o del usuario).</span><span class="sxs-lookup"><span data-stu-id="40a37-130">Meeting signals will be delivered using the following existing conversation notification API (for user-bot chat).</span></span> <span data-ttu-id="40a37-131">Esta API permite que los desarrolladores señalen según la acción del usuario final para mostrar-caso de un burbuja de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="40a37-131">This API allows developers to signal based on end-user action to show-case an in-meeting dialog bubble.</span></span>|<span data-ttu-id="40a37-132">**Publicar** _**/V3/Conversations/{conversationId}/Activities**_</span><span class="sxs-lookup"><span data-stu-id="40a37-132">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="40a37-133">SDK de Microsoft bot Framework</span><span class="sxs-lookup"><span data-stu-id="40a37-133">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="40a37-134">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="40a37-134">GetUserContext</span></span>

<span data-ttu-id="40a37-135">Consulte nuestro [contexto de obtención de la documentación de la pestaña de Microsoft Teams](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) para obtener instrucciones sobre cómo identificar y recuperar información contextual para el contenido de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="40a37-135">Please refer to our [Get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and  retrieving contextual information for your tab content.</span></span> <span data-ttu-id="40a37-136">Como parte de la extensibilidad de las reuniones, se ha agregado un nuevo valor a la carga de respuesta:</span><span class="sxs-lookup"><span data-stu-id="40a37-136">As part of meetings extensibility, a new value has been added for the response payload:</span></span>

<span data-ttu-id="40a37-137">✔ **meetingId**: usada por una tabulación cuando se ejecuta en el contexto de la reunión.</span><span class="sxs-lookup"><span data-stu-id="40a37-137">✔ **meetingId**: used by a tab when running in the meeting context.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="40a37-138">API de GetParticipant</span><span class="sxs-lookup"><span data-stu-id="40a37-138">GetParticipant API</span></span>

> [!NOTE]
>
> * <span data-ttu-id="40a37-139">No almacene en caché roles de participantes, ya que el organizador de la reunión puede cambiar un rol en cualquier punto en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="40a37-139">Do not cache participant roles since the meeting organizer can change a role at any point in time.</span></span>
>
> * <span data-ttu-id="40a37-140">Actualmente, Microsoft Teams no admite listas de distribución de gran tamaño o tamaños de lista de más de 350 participantes para la `GetParticipant` API.</span><span class="sxs-lookup"><span data-stu-id="40a37-140">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="40a37-141">Parámetros de consulta</span><span class="sxs-lookup"><span data-stu-id="40a37-141">Query parameters</span></span>

|<span data-ttu-id="40a37-142">Valor</span><span class="sxs-lookup"><span data-stu-id="40a37-142">Value</span></span>|<span data-ttu-id="40a37-143">Tipo</span><span class="sxs-lookup"><span data-stu-id="40a37-143">Type</span></span>|<span data-ttu-id="40a37-144">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="40a37-144">Required</span></span>|<span data-ttu-id="40a37-145">Descripción</span><span class="sxs-lookup"><span data-stu-id="40a37-145">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="40a37-146">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="40a37-146">**meetingId**</span></span>| <span data-ttu-id="40a37-147">string</span><span class="sxs-lookup"><span data-stu-id="40a37-147">string</span></span> | <span data-ttu-id="40a37-148">Sí</span><span class="sxs-lookup"><span data-stu-id="40a37-148">Yes</span></span> | <span data-ttu-id="40a37-149">El identificador de la reunión está disponible a través de la invocación de bot? o Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="40a37-149">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="40a37-150">**participantId**</span><span class="sxs-lookup"><span data-stu-id="40a37-150">**participantId**</span></span>| <span data-ttu-id="40a37-151">string</span><span class="sxs-lookup"><span data-stu-id="40a37-151">string</span></span> | <span data-ttu-id="40a37-152">Sí</span><span class="sxs-lookup"><span data-stu-id="40a37-152">Yes</span></span> | <span data-ttu-id="40a37-153">ParticipantId es el identificador de usuario.</span><span class="sxs-lookup"><span data-stu-id="40a37-153">The participantId is the user ID.</span></span> <span data-ttu-id="40a37-154">Está disponible en el SSO del cliente de pestañas, Bot invocación y el SDK del cliente de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="40a37-154">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="40a37-155">Se recomienda encarecidamente obtener un participantId desde el SSO de pestaña.</span><span class="sxs-lookup"><span data-stu-id="40a37-155">It is highly recommended to get a participantId from the Tab SSO.</span></span> |
|<span data-ttu-id="40a37-156">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="40a37-156">**tenantId**</span></span>| <span data-ttu-id="40a37-157">string</span><span class="sxs-lookup"><span data-stu-id="40a37-157">string</span></span> | <span data-ttu-id="40a37-158">Sí</span><span class="sxs-lookup"><span data-stu-id="40a37-158">Yes</span></span> | <span data-ttu-id="40a37-159">El tenantId es necesario para los usuarios del inquilino.</span><span class="sxs-lookup"><span data-stu-id="40a37-159">The tenantId is required for the tenant users.</span></span> <span data-ttu-id="40a37-160">Está disponible en el SSO del cliente de pestañas, Bot invocación y el SDK del cliente de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="40a37-160">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="40a37-161">Se recomienda encarecidamente obtener un tenantId desde el SSO de pestaña.</span><span class="sxs-lookup"><span data-stu-id="40a37-161">It is highly recommended to get a tenantId from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="40a37-162">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="40a37-162">Example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="40a37-163">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="40a37-163">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="40a37-164">JavaScript</span><span class="sxs-lookup"><span data-stu-id="40a37-164">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="40a37-165">JSON</span><span class="sxs-lookup"><span data-stu-id="40a37-165">JSON</span></span>](#tab/json)

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

<span data-ttu-id="40a37-166">El cuerpo de la respuesta es:</span><span class="sxs-lookup"><span data-stu-id="40a37-166">The response body is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="40a37-167">Códigos de respuesta</span><span class="sxs-lookup"><span data-stu-id="40a37-167">Response codes</span></span>

* <span data-ttu-id="40a37-168">**403**: la aplicación no tiene permiso para obtener información sobre los participantes.</span><span class="sxs-lookup"><span data-stu-id="40a37-168">**403**: The app is not allowed to get participant information.</span></span>  <span data-ttu-id="40a37-169">Esta es la respuesta de error más común y se desencadena si la aplicación no está instalada en la reunión.</span><span class="sxs-lookup"><span data-stu-id="40a37-169">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="40a37-170">Por ejemplo, si la aplicación está deshabilitada por el administrador de inquilinos o se bloquea durante la migración de sitios activos.</span><span class="sxs-lookup"><span data-stu-id="40a37-170">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>
* <span data-ttu-id="40a37-171">**200**: la información del participante se recuperó correctamente.</span><span class="sxs-lookup"><span data-stu-id="40a37-171">**200**: Participant information successfully retrieved.</span></span>
* <span data-ttu-id="40a37-172">**401**: token no válido.</span><span class="sxs-lookup"><span data-stu-id="40a37-172">**401**: Invalid token.</span></span>
* <span data-ttu-id="40a37-173">**404**: no se encuentra el participante.</span><span class="sxs-lookup"><span data-stu-id="40a37-173">**404**: Participant cannot be found.</span></span>
* <span data-ttu-id="40a37-174">**500**: la reunión ha expirado (más de 60 días desde la finalización de la reunión) o el participante no tiene permisos basados en su rol.</span><span class="sxs-lookup"><span data-stu-id="40a37-174">**500**: The meeting has either expired (more than 60 days since the meeting ended) or the participant does not have permissions based on their role.</span></span>


<span data-ttu-id="40a37-175">**Próximamente**</span><span class="sxs-lookup"><span data-stu-id="40a37-175">**Coming Soon**</span></span>

* <span data-ttu-id="40a37-176">**404**: la reunión ha expirado o el participante no se encuentra.</span><span class="sxs-lookup"><span data-stu-id="40a37-176">**404**: The meeting has either expired or participant cannot be found.</span></span>


### <a name="notificationsignal-api"></a><span data-ttu-id="40a37-177">API de NotificationSignal</span><span class="sxs-lookup"><span data-stu-id="40a37-177">NotificationSignal API</span></span>

> [!NOTE]
> <span data-ttu-id="40a37-178">Cuando se invoca un cuadro de diálogo en la reunión, el mismo contenido también se presentará como un mensaje de chat.</span><span class="sxs-lookup"><span data-stu-id="40a37-178">When an in-meeting dialog is invoked, the same content will also be presented as a chat message.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="40a37-179">Parámetros de consulta</span><span class="sxs-lookup"><span data-stu-id="40a37-179">Query parameters</span></span>

|<span data-ttu-id="40a37-180">Valor</span><span class="sxs-lookup"><span data-stu-id="40a37-180">Value</span></span>|<span data-ttu-id="40a37-181">Tipo</span><span class="sxs-lookup"><span data-stu-id="40a37-181">Type</span></span>|<span data-ttu-id="40a37-182">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="40a37-182">Required</span></span>|<span data-ttu-id="40a37-183">Descripción</span><span class="sxs-lookup"><span data-stu-id="40a37-183">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="40a37-184">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="40a37-184">**conversationId**</span></span>| <span data-ttu-id="40a37-185">string</span><span class="sxs-lookup"><span data-stu-id="40a37-185">string</span></span> | <span data-ttu-id="40a37-186">Sí</span><span class="sxs-lookup"><span data-stu-id="40a37-186">Yes</span></span> | <span data-ttu-id="40a37-187">El identificador de conversación está disponible como parte de la invocación de bot</span><span class="sxs-lookup"><span data-stu-id="40a37-187">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="example"></a><span data-ttu-id="40a37-188">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="40a37-188">Example</span></span>

> [!NOTE]
>
<span data-ttu-id="40a37-189">El `completionBotId` parámetro de `externalResourceUrl` es opcional en el ejemplo de carga solicitada.</span><span class="sxs-lookup"><span data-stu-id="40a37-189">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="40a37-190">`Bot ID` se declara en el manifiesto y el bot recibe un objeto de resultado.</span><span class="sxs-lookup"><span data-stu-id="40a37-190">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="40a37-191">Los parámetros width y height de externalResourceUrl deben estar en píxeles.</span><span class="sxs-lookup"><span data-stu-id="40a37-191">The externalResourceUrl width and height parameters must be in pixels.</span></span> <span data-ttu-id="40a37-192">Consulte las [directrices de diseño](design/designing-apps-in-meetings.md) para asegurarse de que las dimensiones están dentro de los límites permitidos.</span><span class="sxs-lookup"><span data-stu-id="40a37-192">Refer to the [design guidelines](design/designing-apps-in-meetings.md) to ensure the dimensions are within the allowed limits.</span></span>
> * <span data-ttu-id="40a37-193">La dirección URL es la página que se carga como una `<iframe>` en el cuadro de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="40a37-193">The URL is the page loaded as an `<iframe>` in the in-meeting dialog.</span></span> <span data-ttu-id="40a37-194">El dominio debe estar en la matriz de la aplicación `validDomains` en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="40a37-194">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="40a37-195">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="40a37-195">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="40a37-196">JavaScript</span><span class="sxs-lookup"><span data-stu-id="40a37-196">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="40a37-197">JSON</span><span class="sxs-lookup"><span data-stu-id="40a37-197">JSON</span></span>](#tab/json)

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

#### <a name="response-codes"></a><span data-ttu-id="40a37-198">Códigos de respuesta</span><span class="sxs-lookup"><span data-stu-id="40a37-198">Response Codes</span></span>

* <span data-ttu-id="40a37-199">**201**: la actividad con señal se ha enviado correctamente</span><span class="sxs-lookup"><span data-stu-id="40a37-199">**201**: activity with signal is successfully sent</span></span>  
* <span data-ttu-id="40a37-200">**401**: token no válido</span><span class="sxs-lookup"><span data-stu-id="40a37-200">**401**: invalid token</span></span>  
* <span data-ttu-id="40a37-201">**201**: la actividad con señal se ha enviado correctamente.</span><span class="sxs-lookup"><span data-stu-id="40a37-201">**201**: Activity with signal is successfully sent.</span></span> 
* <span data-ttu-id="40a37-202">**401**: token no válido.</span><span class="sxs-lookup"><span data-stu-id="40a37-202">**401**: Invalid token.</span></span>
* <span data-ttu-id="40a37-203">**403**: la aplicación no puede enviar la señal.</span><span class="sxs-lookup"><span data-stu-id="40a37-203">**403**: The app is unable to send the signal.</span></span> <span data-ttu-id="40a37-204">Esto puede ocurrir debido a diversos motivos como, por ejemplo, que el administrador del espacio empresarial deshabilita la aplicación, la aplicación se bloquea durante la migración de sitios activos y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="40a37-204">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="40a37-205">En este caso, la carga contiene un mensaje de error detallado.</span><span class="sxs-lookup"><span data-stu-id="40a37-205">In this case, the payload contains a detailed error message.</span></span> 
* <span data-ttu-id="40a37-206">**404**: el chat de reuniones no existe.</span><span class="sxs-lookup"><span data-stu-id="40a37-206">**404**: Meeting chat doesn't exist.</span></span>
 

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="40a37-207">Habilitar la aplicación para reuniones de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="40a37-207">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="40a37-208">Actualizar el manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="40a37-208">Update your app manifest</span></span>

<span data-ttu-id="40a37-209">Las funcionalidades de la aplicación reuniones se declaran en el manifiesto de la aplicación a través de los  ->  **ámbitos** configurableTabs y los matrices de **contexto** .</span><span class="sxs-lookup"><span data-stu-id="40a37-209">The meetings app capabilities are declared in your app manifest via the **configurableTabs** -> **scopes** and **context** arrays.</span></span> <span data-ttu-id="40a37-210">*Scope* define quién y *Context* define dónde estará disponible la aplicación.</span><span class="sxs-lookup"><span data-stu-id="40a37-210">*Scope* defines to whom and *context* defines where your app will be available.</span></span>

> [!NOTE]
> <span data-ttu-id="40a37-211">Use el [esquema del manifiesto de vista previa de desarrollador](../resources/schema/manifest-schema-dev-preview.md) para probar esto en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="40a37-211">Please use [Developer Preview manifest schema](../resources/schema/manifest-schema-dev-preview.md) to try this in your app manifest.</span></span>

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

### <a name="context-property"></a><span data-ttu-id="40a37-212">Propiedad context</span><span class="sxs-lookup"><span data-stu-id="40a37-212">Context property</span></span>

<span data-ttu-id="40a37-213">La pestaña `context` y `scopes` las propiedades funcionan en armonía para permitirle determinar dónde quiere que aparezca la aplicación.</span><span class="sxs-lookup"><span data-stu-id="40a37-213">The tab `context` and `scopes` properties work in harmony to allow you to determine where you want your app to appear.</span></span> <span data-ttu-id="40a37-214">Las pestañas `team` del `groupchat` ámbito o pueden tener más de un contexto.</span><span class="sxs-lookup"><span data-stu-id="40a37-214">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="40a37-215">Los valores posibles para la propiedad context son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="40a37-215">The possible values for the context property are as follows:</span></span>

* <span data-ttu-id="40a37-216">**channelTab**: una pestaña en el encabezado de un canal de equipo.</span><span class="sxs-lookup"><span data-stu-id="40a37-216">**channelTab**: a tab in the header of a team channel.</span></span>
* <span data-ttu-id="40a37-217">**privateChatTab**: una pestaña en el encabezado de un grupo de chats entre un conjunto de usuarios que no están en el contexto de un equipo o una reunión.</span><span class="sxs-lookup"><span data-stu-id="40a37-217">**privateChatTab**: a tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span>
* <span data-ttu-id="40a37-218">**meetingChatTab**: una pestaña en el encabezado de un grupo de chats entre un conjunto de usuarios en el contexto de una reunión programada.</span><span class="sxs-lookup"><span data-stu-id="40a37-218">**meetingChatTab**: a tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span>
* <span data-ttu-id="40a37-219">**meetingDetailsTab**: una pestaña en el encabezado de la vista de detalles de la reunión del calendario.</span><span class="sxs-lookup"><span data-stu-id="40a37-219">**meetingDetailsTab**: a tab in the header of the meeting details view of the calendar.</span></span>
* <span data-ttu-id="40a37-220">**meetingSidePanel**: un panel en reunión que se abre a través de la barra unificada (barra u).</span><span class="sxs-lookup"><span data-stu-id="40a37-220">**meetingSidePanel**: an in-meeting panel opened via the unified bar (u-bar).</span></span>

> [!NOTE]
> <span data-ttu-id="40a37-221">La propiedad "context" actualmente no se admite y, por lo tanto, se omitirá en clientes móviles</span><span class="sxs-lookup"><span data-stu-id="40a37-221">"Context" property is currently not supported and thus will be ignored on mobile clients</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="40a37-222">Configurar la aplicación para escenarios de reuniones</span><span class="sxs-lookup"><span data-stu-id="40a37-222">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="40a37-223">Para que la aplicación esté visible en la galería de pestañas, necesita **admitir las pestañas configurables** y el **ámbito de chat en grupo**.</span><span class="sxs-lookup"><span data-stu-id="40a37-223">For your app to be visible in the tab gallery it needs to **support configurable tabs** and the **group chat scope**.</span></span>
>
> * <span data-ttu-id="40a37-224">Los clientes móviles solo admiten fichas en las superficies anteriores y posteriores a la reunión.</span><span class="sxs-lookup"><span data-stu-id="40a37-224">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="40a37-225">Las experiencias en reunión (pestaña y cuadro de diálogo en reunión) en dispositivos móviles estarán disponibles próximamente.</span><span class="sxs-lookup"><span data-stu-id="40a37-225">The in-meeting experiences (in-meeting dialog and tab) on mobile will be available soon.</span></span> <span data-ttu-id="40a37-226">Siga las [instrucciones para las pestañas de dispositivos móviles](../tabs/design/tabs-mobile.md) al crear las pestañas para dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="40a37-226">Follow the [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span>

### <a name="before-a-meeting"></a><span data-ttu-id="40a37-227">Antes de una reunión</span><span class="sxs-lookup"><span data-stu-id="40a37-227">Before a meeting</span></span>

<span data-ttu-id="40a37-228">Los usuarios con roles de organizador o moderador agregan pestañas a una reunión con el botón más ➕ de las páginas de **chat** de reuniones y **detalles** de reuniones.</span><span class="sxs-lookup"><span data-stu-id="40a37-228">Users with organizer and/or presenter roles add tabs to a meeting using the plus ➕ button in the meeting **Chat** and meeting **details** pages.</span></span> <span data-ttu-id="40a37-229">Las extensiones de mensajería se agregan a a través del menú de puntos suspensivos/desbordamiento &#x25CF;&#x25CF;&#x25CF; situada debajo del área redactar mensaje en el chat.</span><span class="sxs-lookup"><span data-stu-id="40a37-229">Messaging extensions are added to via the ellipses/overflow menu &#x25CF;&#x25CF;&#x25CF; located beneath the compose message area in the chat.</span></span> <span data-ttu-id="40a37-230">Los bots se agregan a un chat mediante la **@** clave "" y seleccionando **obtener bots**.</span><span class="sxs-lookup"><span data-stu-id="40a37-230">Bots are added to a meeting chat using the "**@**" key and selecting **Get bots**.</span></span>

<span data-ttu-id="40a37-231">✔ La identidad del usuario *debe* confirmarse mediante el [SSO de pestañas](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="40a37-231">✔ The user identity *must* be confirmed via [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="40a37-232">Tras esta autenticación, la aplicación puede recuperar el rol de usuario a través de la API de GetParticipant.</span><span class="sxs-lookup"><span data-stu-id="40a37-232">Following this authentication, the app can retrieve the user role via the GetParticipant API.</span></span>

 <span data-ttu-id="40a37-233">✔ Basándose en el rol de usuario, la aplicación ahora tendrá la capacidad de presentar experiencias específicas de roles.</span><span class="sxs-lookup"><span data-stu-id="40a37-233">✔ Based on the user role, the app will now have the capability to present role specific experiences.</span></span> <span data-ttu-id="40a37-234">Por ejemplo, una aplicación de sondeo puede permitir que solo los organizadores y los moderadores creen un nuevo sondeo.</span><span class="sxs-lookup"><span data-stu-id="40a37-234">For example, a polling app can allow only organizers and presenters to create a new poll.</span></span>

> <span data-ttu-id="40a37-235">**Nota**: las asignaciones de roles se pueden cambiar mientras una reunión está en curso.</span><span class="sxs-lookup"><span data-stu-id="40a37-235">**NOTE**: Role assignments can be changed while a meeting is in progress.</span></span>  <span data-ttu-id="40a37-236">*Vea* [roles en una reunión de Microsoft Teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span><span class="sxs-lookup"><span data-stu-id="40a37-236">*See* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span> 

### <a name="during-a-meeting"></a><span data-ttu-id="40a37-237">Durante una reunión</span><span class="sxs-lookup"><span data-stu-id="40a37-237">During a meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="40a37-238">**sidePanel**</span><span class="sxs-lookup"><span data-stu-id="40a37-238">**sidePanel**</span></span>

<span data-ttu-id="40a37-239">✔ En el manifiesto de la aplicación, agregue **sidePanel** a la matriz de **contexto** , como se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="40a37-239">✔ In your app manifest add **sidePanel** to the **context** array as described above.</span></span>

<span data-ttu-id="40a37-240">✔ En la reunión y en todos los escenarios, la aplicación se representará en una pestaña en la reunión que se 320 PX en ancho.</span><span class="sxs-lookup"><span data-stu-id="40a37-240">✔ In the meeting as well as in all scenarios, the app will be rendered in an in-meeting tab that is 320px in width.</span></span> <span data-ttu-id="40a37-241">La pestaña debe estar optimizada para esto.</span><span class="sxs-lookup"><span data-stu-id="40a37-241">Your tab must be optimized for this.</span></span> <span data-ttu-id="40a37-242">*Consulte* la [interfaz FrameContext](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span><span class="sxs-lookup"><span data-stu-id="40a37-242">*See*, [FrameContext interface](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span></span>

<span data-ttu-id="40a37-243">✔ Consulte el SDK de Microsoft [Teams](../tabs/how-to/access-teams-context.md#user-context) para usar la API de **userContext** para enrutar las solicitudes en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="40a37-243">✔Refer to the [Teams SDK](../tabs/how-to/access-teams-context.md#user-context) to use the **userContext** API to route requests accordingly.</span></span>

<span data-ttu-id="40a37-244">✔ Consulte el [flujo de autenticación de Teams para pestañas](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="40a37-244">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="40a37-245">El flujo de autenticación para pestañas es muy similar al flujo de autenticación de los sitios Web.</span><span class="sxs-lookup"><span data-stu-id="40a37-245">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="40a37-246">Por lo tanto, las pestañas pueden usar OAuth 2,0 directamente.</span><span class="sxs-lookup"><span data-stu-id="40a37-246">Thus, tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="40a37-247">*Vea también* el [flujo de código de autorización de Microsoft Identity platform y OAuth 2,0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span><span class="sxs-lookup"><span data-stu-id="40a37-247">*See also*, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="40a37-248">✔ Extensión de mensaje debe funcionar como se esperaba cuando un usuario está en una vista en la reunión y debe poder publicar tarjetas de extensión de mensaje de redacción.</span><span class="sxs-lookup"><span data-stu-id="40a37-248">✔ Message extension should work as expected when a user is in an in-meeting view and should be able to post compose message extension cards.</span></span>

<span data-ttu-id="40a37-249">✔ AppName en-reunión-información sobre herramientas debe indicar el nombre de la aplicación en la barra U-Meeting.</span><span class="sxs-lookup"><span data-stu-id="40a37-249">✔ AppName in-meeting - Tooltip should state the app name in-meeting U-bar.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="40a37-250">**Diálogo en la reunión**</span><span class="sxs-lookup"><span data-stu-id="40a37-250">**In-meeting dialog**</span></span>

<span data-ttu-id="40a37-251">✔ Debe adherirse a las [instrucciones de diseño del cuadro de diálogo en reunión](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span><span class="sxs-lookup"><span data-stu-id="40a37-251">✔ You must adhere to the [in-meeting dialog design guidelines](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

<span data-ttu-id="40a37-252">✔ Consulte el [flujo de autenticación de Teams para pestañas](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="40a37-252">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="40a37-253">✔ Usar la API de [notificación](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) para indicar que se debe desencadenar una notificación de burbuja.</span><span class="sxs-lookup"><span data-stu-id="40a37-253">✔ Use the [notification](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification needs to be triggered.</span></span>

<span data-ttu-id="40a37-254">✔ Como parte de la carga de la solicitud de notificación, incluya la dirección URL donde se hospeda el contenido que se va a mostrar.</span><span class="sxs-lookup"><span data-stu-id="40a37-254">✔ As part of the notification request payload, include the URL where the content to be showcased is hosted.</span></span>

<span data-ttu-id="40a37-255">✔ Cuadro de diálogo de reunión no debe usar el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="40a37-255">✔ In-meeting dialog must not use task module.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="40a37-256">Estas notificaciones son persistentes en su naturaleza.</span><span class="sxs-lookup"><span data-stu-id="40a37-256">These notifications are persistent in nature.</span></span> <span data-ttu-id="40a37-257">Debe invocar la función [**submitTask ()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) para descartar automáticamente una vez que un usuario realiza una acción en la vista Web.</span><span class="sxs-lookup"><span data-stu-id="40a37-257">You must invoke the [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to auto-dismiss after a user takes an action in the web-view.</span></span> <span data-ttu-id="40a37-258">Este es un requisito para el envío de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="40a37-258">This is a requirement for app submission.</span></span> <span data-ttu-id="40a37-259">*Vea también*, [Teams SDK: módulo de tareas](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="40a37-259">*See also*, [Teams SDK: task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
>
> * <span data-ttu-id="40a37-260">Si quiere que la aplicación admita usuarios anónimos, su carga de solicitud de invocación inicial debe basarse en el `from.id`  objeto (ID del usuario) request Metadata in the `from` Object, no el `from.aadObjectId` (ID de Azure Active Directory del usuario) request Metadata.</span><span class="sxs-lookup"><span data-stu-id="40a37-260">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id`  (ID of the user) request metadata in the `from` object, not the `from.aadObjectId` (Azure Active Directory ID of the user) request metadata.</span></span> <span data-ttu-id="40a37-261">*Consulte* [using Task modules in Tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) y [Create and Send The Task Module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span><span class="sxs-lookup"><span data-stu-id="40a37-261">*See* [Using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [Create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

### <a name="after-a-meeting"></a><span data-ttu-id="40a37-262">Después de una reunión</span><span class="sxs-lookup"><span data-stu-id="40a37-262">After a meeting</span></span>

<span data-ttu-id="40a37-263">Las configuraciones posteriores a la reunión y antes de la reunión son equivalentes.</span><span class="sxs-lookup"><span data-stu-id="40a37-263">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="meeting-app-sample"></a><span data-ttu-id="40a37-264">Ejemplo de aplicación de reunión</span><span class="sxs-lookup"><span data-stu-id="40a37-264">Meeting app sample</span></span>

 > [!div class="nextstepaction"]
> [<span data-ttu-id="40a37-265">Aplicación de generador de tokens de reunión</span><span class="sxs-lookup"><span data-stu-id="40a37-265">Meeting token generator app</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)

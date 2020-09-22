---
title: Creación de aplicaciones para reuniones de Microsoft Teams
author: laujan
description: creación de aplicaciones para reuniones de Microsoft Teams
ms.topic: conceptual
ms.author: lajanuar
keywords: API de las aplicaciones de Microsoft Teams rol de participante de usuario
ms.openlocfilehash: 83e0a5b53e363a090935b4afa9840dd96c5f7381
ms.sourcegitcommit: b01986739a05c65094618fbe76aeb53d038b1c74
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/22/2020
ms.locfileid: "48182036"
---
# <a name="create-apps-for-teams-meetings-preview"></a><span data-ttu-id="66214-104">Creación de aplicaciones para reuniones de Microsoft Teams (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="66214-104">Create apps for Teams meetings (Preview)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="66214-105">Las características incluidas en Microsoft Teams Preview se proporcionan solo para fines de acceso anticipado, pruebas y comentarios.</span><span class="sxs-lookup"><span data-stu-id="66214-105">Features included in Microsoft Teams preview are provided for early-access, testing, and feedback purposes only.</span></span> <span data-ttu-id="66214-106">Pueden sufrir cambios antes de que estén disponibles en la versión pública y no deben usarse en las aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="66214-106">They may undergo changes before becoming available in the public release and should not be used in production applications.</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="66214-107">Requisitos previos y consideraciones</span><span class="sxs-lookup"><span data-stu-id="66214-107">Prerequisites and considerations</span></span>

1. <span data-ttu-id="66214-108">Las aplicaciones en las reuniones necesitan conocimientos básicos del desarrollo de aplicaciones de Microsoft [Teams](../overview.md).</span><span class="sxs-lookup"><span data-stu-id="66214-108">Apps in meetings require some basic knowledge of [Teams app development](../overview.md).</span></span> <span data-ttu-id="66214-109">Una aplicación en una reunión puede estar formada por [pestañas](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md)y características de [extensiones de mensajería](../messaging-extensions/what-are-messaging-extensions.md) y necesitará actualizaciones en el manifiesto de la [aplicación](#update-your-app-manifest) de Microsoft Teams para indicar que la aplicación está disponible para las reuniones.</span><span class="sxs-lookup"><span data-stu-id="66214-109">An app in a meeting can comprise of [tabs](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md), and [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md) features and will require updates to the Teams [app manifest](#update-your-app-manifest) to indicate that the app is available for meetings</span></span>

1. <span data-ttu-id="66214-110">Para que la aplicación funcione en el ciclo de vida de la reunión como una pestaña, debe admitir pestañas configurables en el [ámbito Groupchat](../resources/schema/manifest-schema.md#configurabletabs).</span><span class="sxs-lookup"><span data-stu-id="66214-110">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs).</span></span> <span data-ttu-id="66214-111">*Consulte* [ampliar la aplicación de Microsoft Teams con una pestaña personalizada](../tabs/how-to/add-tab.md). Admitir el `groupchat` ámbito habilitará la aplicación en chats [anteriores](teams-apps-in-meetings.md#pre-meeting-app-experience) y [posteriores](teams-apps-in-meetings.md#post-meeting-app-experience) a la reunión.</span><span class="sxs-lookup"><span data-stu-id="66214-111">*See* [Extend your Teams app with a custom tab](../tabs/how-to/add-tab.md). Supporting the `groupchat` scope will enable your app in [pre-meeting](teams-apps-in-meetings.md#pre-meeting-app-experience) and [post-meeting](teams-apps-in-meetings.md#post-meeting-app-experience) chats.</span></span>

1. <span data-ttu-id="66214-112">Los parámetros de dirección URL `meetingId` de la API de la reunión pueden requerir, `userId` y el [tenantId](/onedrive/find-your-office-365-tenant-id) , están disponibles como parte de la actividad del SDK del cliente de Microsoft Teams y del bot.</span><span class="sxs-lookup"><span data-stu-id="66214-112">Meeting API URL parameters may require `meetingId`, `userId`, and the [tenantId](/onedrive/find-your-office-365-tenant-id) These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="66214-113">Además, se puede recuperar información fiable sobre el identificador de usuario y el identificador de inquilino mediante la [autenticación SSO de pestañas](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="66214-113">Additionally, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

1. <span data-ttu-id="66214-114">Algunas API de reunión, como `GetParticipant` requerirán un [registro de Bot y un identificador de aplicación de bot](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) para generar tokens de autenticación.</span><span class="sxs-lookup"><span data-stu-id="66214-114">Some meeting APIs, such as `GetParticipant` will require a [bot registration and bot app ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) to generate auth tokens.</span></span>

1. <span data-ttu-id="66214-115">Los desarrolladores deben adherirse a las directrices generales de diseño de la pestaña de Microsoft [Teams](../tabs/design/tabs.md) para los escenarios anteriores y posteriores a la reunión, así como las [directrices de diálogo en reunión](designing-in-meeting-dialog.md) para los diálogos que se desencadenan durante la reunión de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="66214-115">Developers must adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios as well as the [in-meeting dialog guidelines](designing-in-meeting-dialog.md) for in-meeting dialog triggered during a Teams meeting.</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="66214-116">Referencia de API de las aplicaciones de reunión</span><span class="sxs-lookup"><span data-stu-id="66214-116">Meeting apps API reference</span></span>

|<span data-ttu-id="66214-117">API</span><span class="sxs-lookup"><span data-stu-id="66214-117">API</span></span>|<span data-ttu-id="66214-118">Descripción</span><span class="sxs-lookup"><span data-stu-id="66214-118">Description</span></span>|<span data-ttu-id="66214-119">Solicitud</span><span class="sxs-lookup"><span data-stu-id="66214-119">Request</span></span>|<span data-ttu-id="66214-120">Origen</span><span class="sxs-lookup"><span data-stu-id="66214-120">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="66214-121">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="66214-121">**GetUserContext**</span></span>| <span data-ttu-id="66214-122">Obtener información contextual para mostrar contenido relevante en una pestaña de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="66214-122">Get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="66214-123">_**Microsoft Teams. getContext (() => {/*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="66214-123">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="66214-124">SDK del cliente de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="66214-124">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="66214-125">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="66214-125">**GetParticipant**</span></span>|<span data-ttu-id="66214-126">Esta API permite que un bot obtenga información de un participante por el identificador de la reunión y el identificador del participante.</span><span class="sxs-lookup"><span data-stu-id="66214-126">This API allows a bot to fetch a participant information by meeting id and participant id.</span></span>|<span data-ttu-id="66214-127">**Get** _ **/v1/Meetings/{meetingId}/participants/{participantId}? tenantid = {tenantid}**_</span><span class="sxs-lookup"><span data-stu-id="66214-127">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="66214-128">SDK de Microsoft bot Framework</span><span class="sxs-lookup"><span data-stu-id="66214-128">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="66214-129">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="66214-129">**NotificationSignal**</span></span> |<span data-ttu-id="66214-130">Las señales de reunión se entregarán con la siguiente API de notificación de conversación existente (para el chat de bot? o del usuario).</span><span class="sxs-lookup"><span data-stu-id="66214-130">Meeting signals will be delivered using the following existing conversation notification API (for user-bot chat).</span></span> <span data-ttu-id="66214-131">Esta API permite que los desarrolladores señalen según la acción del usuario final para mostrar-caso de un burbuja de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="66214-131">This API allows developers to signal based on end-user action to show-case an in-meeting dialog bubble.</span></span>|<span data-ttu-id="66214-132">**Publicar** _ **/V3/Conversations/{conversationId}/Activities**_</span><span class="sxs-lookup"><span data-stu-id="66214-132">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="66214-133">SDK de Microsoft bot Framework</span><span class="sxs-lookup"><span data-stu-id="66214-133">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="66214-134">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="66214-134">GetUserContext</span></span>

<span data-ttu-id="66214-135">Consulte nuestro [contexto de obtención de la documentación de la pestaña de Microsoft Teams](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) para obtener instrucciones sobre cómo identificar y recuperar información contextual para el contenido de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="66214-135">Please refer to our [Get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and  retrieving contextual information for your tab content.</span></span> <span data-ttu-id="66214-136">Como parte de la extensibilidad de las reuniones, se ha agregado un nuevo valor a la carga de respuesta:</span><span class="sxs-lookup"><span data-stu-id="66214-136">As part of meetings extensibility, a new value has been added for the response payload:</span></span>

<span data-ttu-id="66214-137">✔ **meetingId**: usada por una tabulación cuando se ejecuta en el contexto de la reunión.</span><span class="sxs-lookup"><span data-stu-id="66214-137">✔ **meetingId**: used by a tab when running in the meeting context.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="66214-138">API de GetParticipant</span><span class="sxs-lookup"><span data-stu-id="66214-138">GetParticipant API</span></span>

> [!NOTE]
>
> * <span data-ttu-id="66214-139">No almacene en caché roles de participantes, ya que el organizador de la reunión puede cambiar un rol en cualquier punto en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="66214-139">Do not cache participant roles since the meeting organizer can change a role at any point in time.</span></span>
>
> * <span data-ttu-id="66214-140">Actualmente, Microsoft Teams no admite listas de distribución de gran tamaño o tamaños de lista de más de 350 participantes para la `GetParticipant` API.</span><span class="sxs-lookup"><span data-stu-id="66214-140">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>
>
> * <span data-ttu-id="66214-141">La compatibilidad con bot Framework SDK estará disponible próximamente.</span><span class="sxs-lookup"><span data-stu-id="66214-141">Support for the Bot Framework SDK is coming soon.</span></span>

#### <a name="request"></a><span data-ttu-id="66214-142">Solicitud</span><span class="sxs-lookup"><span data-stu-id="66214-142">Request</span></span>

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

<span data-ttu-id="66214-143">*Vea* la [referencia de la API de bot Framework](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="66214-143">*See* the [Bot Framework API reference](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<!-- markdownlint-disable MD025 -->

<span data-ttu-id="66214-144">**Ejemplo de C#**</span><span class="sxs-lookup"><span data-stu-id="66214-144">**C# Example**</span></span>

```csharp
string meetingId = "meetingid?";
string participantId = "participantidhere";
var connectorClient = turnContext.TurnState.Get<IConnectorClient>();
var creds = connectorClient.Credentials as AppCredentials;
var bearerToken = await creds.GetTokenAsync().ConfigureAwait(false);
var request = new HttpRequestMessage();
request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
request.Method = new HttpMethod("GET");
request.RequestUri = new System.Uri(Path.Combine(connectorClient.BaseUri.OriginalString, $"/meetings/{meetingId}/participants/{participantId}"));
HttpResponseMessage response = await (connectorClient as ServiceClient<ConnectorClient>).HttpClient.SendAsync(request, cancellationToken).ConfigureAwait(false);
if (response.StatusCode == System.Net.HttpStatusCode.OK)
{
    var content = await response.Content.ReadAsStringAsync().ConfigureAwait(false);
    var theObject = Rest.Serialization.SafeJsonConvert.DeserializeObject<WhateverObjectIsReturned>(content, connectorClient.DeserializationSettings);
```

* * *
<!-- markdownlint-disable MD001 -->

#### <a name="query-parameters"></a><span data-ttu-id="66214-145">Parámetros de consulta</span><span class="sxs-lookup"><span data-stu-id="66214-145">Query parameters</span></span>

<span data-ttu-id="66214-146">**meetingId**.</span><span class="sxs-lookup"><span data-stu-id="66214-146">**meetingId**.</span></span> <span data-ttu-id="66214-147">El identificador de la reunión es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="66214-147">The meeting identifier is required.</span></span>  
<span data-ttu-id="66214-148">**participantId**.</span><span class="sxs-lookup"><span data-stu-id="66214-148">**participantId**.</span></span> <span data-ttu-id="66214-149">El identificador del participante es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="66214-149">The participant identifier is required.</span></span>  
<span data-ttu-id="66214-150">**tenantId**.</span><span class="sxs-lookup"><span data-stu-id="66214-150">**tenantId**.</span></span> <span data-ttu-id="66214-151">[Identificador de inquilino](/onedrive/find-your-office-365-tenant-id) del participante.</span><span class="sxs-lookup"><span data-stu-id="66214-151">[Tenant id](/onedrive/find-your-office-365-tenant-id) of the participant.</span></span> <span data-ttu-id="66214-152">Necesario para el usuario del inquilino.</span><span class="sxs-lookup"><span data-stu-id="66214-152">Required for tenant user.</span></span>

#### <a name="response-payload"></a><span data-ttu-id="66214-153">Carga de respuesta</span><span class="sxs-lookup"><span data-stu-id="66214-153">Response Payload</span></span>
<!-- markdownlint-disable MD036 -->

<span data-ttu-id="66214-154">**Ejemplo 1**</span><span class="sxs-lookup"><span data-stu-id="66214-154">**Example 1**</span></span>

```json
{
    "meetingRole":"Presenter",
    "conversation":{
            "isGroup": true,
            "id": "19:meeting_NDQxMzg1YjUtMGIzNC00Yjc1LWFmYWYtYzk1MGY2MTMwNjE0@thread.v2"
        }
}
```

<span data-ttu-id="66214-155">**meetingRole** puede ser *Organizer*, *Presenter*o *Attendee*.</span><span class="sxs-lookup"><span data-stu-id="66214-155">**meetingRole** can be *Organizer*, *Presenter*, or *Attendee*.</span></span>

<span data-ttu-id="66214-156">**Ejemplo 2**</span><span class="sxs-lookup"><span data-stu-id="66214-156">**Example 2**</span></span>

```json
{
    "meetingRole": "Attendee",
    "conversation": {
        "isGroup": true,
        "id": "19:meeting_OWIyYWVhZWMtM2ExMi00ZTc2LTg0OGEtYWNhMTM4MmZlZTNj@thread.v2"
        }
}
```

#### <a name="response-codes"></a><span data-ttu-id="66214-157">Códigos de respuesta</span><span class="sxs-lookup"><span data-stu-id="66214-157">Response Codes</span></span>

<span data-ttu-id="66214-158">**403**: la aplicación no tiene permiso para obtener información sobre los participantes.</span><span class="sxs-lookup"><span data-stu-id="66214-158">**403**: the app is not allowed to get participant information.</span></span> <span data-ttu-id="66214-159">Esta será la respuesta de error más común y se desencadenará cuando la aplicación no se instale en la reunión, por ejemplo, cuando la aplicación está deshabilitada por el administrador de inquilinos o bloqueada durante la mitigación del sitio activo.</span><span class="sxs-lookup"><span data-stu-id="66214-159">This will be the most common error response and is triggered when the app is not installed in the meeting such as when the app is disabled by tenant admin or blocked during live site mitigation.</span></span>  
<span data-ttu-id="66214-160">**200**: la información del participante se recuperó correctamente</span><span class="sxs-lookup"><span data-stu-id="66214-160">**200**: participant information successfully retrieved</span></span>  
<span data-ttu-id="66214-161">**401**: token no válido</span><span class="sxs-lookup"><span data-stu-id="66214-161">**401**: invalid token</span></span>  
<span data-ttu-id="66214-162">**404**: la reunión no existe o el participante no se encuentra.</span><span class="sxs-lookup"><span data-stu-id="66214-162">**404**: the meeting doesn't exist or participant can’t be found.</span></span>

<!-- markdownlint-disable MD024 -->
### <a name="notificationsignal-api"></a><span data-ttu-id="66214-163">API de NotificationSignal</span><span class="sxs-lookup"><span data-stu-id="66214-163">NotificationSignal API</span></span>

> [!NOTE]
> <span data-ttu-id="66214-164">Cuando se invoca un cuadro de diálogo en la reunión, el mismo contenido también se presentará como un mensaje de chat.</span><span class="sxs-lookup"><span data-stu-id="66214-164">When an in-meeting dialog is invoked, the same content will also be presented as a chat message.</span></span>

#### <a name="request"></a><span data-ttu-id="66214-165">Solicitud</span><span class="sxs-lookup"><span data-stu-id="66214-165">Request</span></span>

```http
POST /v3/conversations/{conversationId}/activities
```

#### <a name="query-parameters"></a><span data-ttu-id="66214-166">Parámetros de consulta</span><span class="sxs-lookup"><span data-stu-id="66214-166">Query parameters</span></span>

<span data-ttu-id="66214-167">**conversationId**: el identificador de la conversación.</span><span class="sxs-lookup"><span data-stu-id="66214-167">**conversationId**: The conversation identifier.</span></span> <span data-ttu-id="66214-168">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="66214-168">Required</span></span>

#### <a name="request-payload"></a><span data-ttu-id="66214-169">Carga de solicitud</span><span class="sxs-lookup"><span data-stu-id="66214-169">Request Payload</span></span>

# <a name="json"></a>[<span data-ttu-id="66214-170">JSON</span><span class="sxs-lookup"><span data-stu-id="66214-170">JSON</span></span>](#tab/json)

```json
{
    "type": "message",
    "text": "John Phillips assigned you a weekly todo",
    "summary": "Don't forget to meet with Marketing next week",
    "channelData": {
    "notification": {
    "alert": true,
    "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=&height=&width=&title=<TaskInfo.title>"
    }
},
    "replyToId": "1493070356924"
    }
```

# <a name="cnet"></a>[<span data-ttu-id="66214-171">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="66214-171">C#/.NET</span></span>](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");
MeetingNotification notification = new MeetingNotification
{
    AlertInMeeting = true,
    ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=&height=&width=&title=<TaskInfo.title>"
};
activity.ChannelData = new TeamsChannelData
{
    Notification = notification
};
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[<span data-ttu-id="66214-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="66214-172">JavaScript</span></span>](#tab/javascript)

```javascript

const replyActivity = MessageFactory.text('Hi'); // this could be an adaptive card instead
        replyActivity.channelData = {
            notification: {
                alertInMeeting: true,
                externalResourceUrl: 'https://teams.microsoft.com/l/bubble/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>’
            }
        };
        await context.sendActivity(replyActivity);
```

* * *

> [!IMPORTANT]
> <span data-ttu-id="66214-173">La dirección URL de la burbuja de contenido (URL de taskInfo) debe incluirse en la lista de [dominios válidos](../resources/schema/manifest-schema.md#validdomains) que se incluye en el manifiesto de la aplicación Teams.</span><span class="sxs-lookup"><span data-stu-id="66214-173">The URL in the content bubble (taskInfo URL) must be included in the [valid domains](../resources/schema/manifest-schema.md#validdomains) list included in the Teams app manifest.</span></span>

#### <a name="response-codes"></a><span data-ttu-id="66214-174">Códigos de respuesta</span><span class="sxs-lookup"><span data-stu-id="66214-174">Response Codes</span></span>

<span data-ttu-id="66214-175">**201**: la actividad con señal se ha enviado correctamente</span><span class="sxs-lookup"><span data-stu-id="66214-175">**201**: activity with signal is successfully sent</span></span>  
<span data-ttu-id="66214-176">**401**: token no válido</span><span class="sxs-lookup"><span data-stu-id="66214-176">**401**: invalid token</span></span>  
<span data-ttu-id="66214-177">**403**: la aplicación no puede enviar la señal.</span><span class="sxs-lookup"><span data-stu-id="66214-177">**403**: the app is not allowed to send the signal.</span></span> <span data-ttu-id="66214-178">En este caso, la carga debe contener un mensaje de error más detallado.</span><span class="sxs-lookup"><span data-stu-id="66214-178">In this case, the payload should contain more detail error message.</span></span> <span data-ttu-id="66214-179">Puede haber varios motivos: la aplicación está deshabilitada por el administrador de inquilinos, bloqueada durante la mitigación de sitios activos, etc.</span><span class="sxs-lookup"><span data-stu-id="66214-179">There can be many reasons: app disabled by tenant admin, blocked during live site mitigation, etc.</span></span>  
<span data-ttu-id="66214-180">**404**: el chat de reuniones no existe</span><span class="sxs-lookup"><span data-stu-id="66214-180">**404**: meeting chat doesn't exist</span></span>  

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="66214-181">Habilitar la aplicación para reuniones de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="66214-181">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="66214-182">Actualizar el manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="66214-182">Update your app manifest</span></span>

<span data-ttu-id="66214-183">Las funcionalidades de la aplicación reuniones se declaran en el **configurableTabs**manifiesto de la aplicación a través de los  ->  **ámbitos** configurableTabs y los matrices de **contexto** .</span><span class="sxs-lookup"><span data-stu-id="66214-183">The meetings app capabilities are declared in your app manifest via the **configurableTabs** -> **scopes** and **context** arrays.</span></span> <span data-ttu-id="66214-184">*Scope* define quién y *Context* define dónde estará disponible la aplicación.</span><span class="sxs-lookup"><span data-stu-id="66214-184">*Scope* defines to whom and *context* defines where your app will be available.</span></span>

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

### <a name="context-property"></a><span data-ttu-id="66214-185">Propiedad context</span><span class="sxs-lookup"><span data-stu-id="66214-185">Context property</span></span>

<span data-ttu-id="66214-186">La pestaña `context` y `scopes` las propiedades funcionan en armonía para permitirle determinar dónde quiere que aparezca la aplicación.</span><span class="sxs-lookup"><span data-stu-id="66214-186">The tab `context` and `scopes` properties work in harmony to allow you to determine where you want your app to appear.</span></span> <span data-ttu-id="66214-187">Aunque las pestañas en el `personal` ámbito solo pueden tener un contexto, es decir, `personalTab` o las  `team` `groupchat` pestañas con ámbito pueden tener más de un contexto.</span><span class="sxs-lookup"><span data-stu-id="66214-187">While tabs in the `personal` scope can only have one context, i.e., `personalTab`,  `team` or `groupchat` scoped tabs can have more than one context.</span></span> <span data-ttu-id="66214-188">Los valores posibles para la propiedad context son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="66214-188">The possible values for the context property are as follows:</span></span>

* <span data-ttu-id="66214-189">**channelTab**: una pestaña en el encabezado de un canal de equipo.</span><span class="sxs-lookup"><span data-stu-id="66214-189">**channelTab**: a tab in the header of a team channel.</span></span>
* <span data-ttu-id="66214-190">**privateChatTab**: una pestaña en el encabezado de un grupo de chats entre un conjunto de usuarios que no están en el contexto de un equipo o una reunión.</span><span class="sxs-lookup"><span data-stu-id="66214-190">**privateChatTab**: a tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span>
* <span data-ttu-id="66214-191">**meetingChatTab**: una pestaña en el encabezado de un grupo de chats entre un conjunto de usuarios en el contexto de una reunión programada.</span><span class="sxs-lookup"><span data-stu-id="66214-191">**meetingChatTab**: a tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span>
* <span data-ttu-id="66214-192">**meetingDetailsTab**: una pestaña en el encabezado de la vista de detalles de la reunión del calendario.</span><span class="sxs-lookup"><span data-stu-id="66214-192">**meetingDetailsTab**: a tab in the header of the meeting details view of the calendar.</span></span>
* <span data-ttu-id="66214-193">**meetingSidePanel**: un panel en reunión que se abre a través de la barra unificada (barra u).</span><span class="sxs-lookup"><span data-stu-id="66214-193">**meetingSidePanel**: an in-meeting panel opened via the unified bar (u-bar).</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="66214-194">Configurar la aplicación para escenarios de reuniones</span><span class="sxs-lookup"><span data-stu-id="66214-194">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> <span data-ttu-id="66214-195">Para que la aplicación esté visible en la galería de pestañas, necesita **admitir las pestañas configurables** y el **ámbito de chat en grupo**.</span><span class="sxs-lookup"><span data-stu-id="66214-195">For your app to be visible in the tab gallery it needs to **support configurable tabs** and the **group chat scope**.</span></span>

### <a name="pre-meeting"></a><span data-ttu-id="66214-196">Reunión previa</span><span class="sxs-lookup"><span data-stu-id="66214-196">Pre-meeting</span></span>

<span data-ttu-id="66214-197">Los usuarios con roles de organizador o moderador agregan pestañas a una reunión con el botón más ➕ de las páginas de **chat** de reuniones y **detalles** de reuniones.</span><span class="sxs-lookup"><span data-stu-id="66214-197">Users with organizer and/or presenter roles add tabs to a meeting using the plus ➕ button in the meeting **Chat** and meeting **details** pages.</span></span> <span data-ttu-id="66214-198">Las extensiones de mensajería se agregan a a través del menú de puntos suspensivos/desbordamiento &#x25CF;&#x25CF;&#x25CF; situada debajo del área redactar mensaje en el chat.</span><span class="sxs-lookup"><span data-stu-id="66214-198">Messaging extensions are added to via the ellipses/overflow menu &#x25CF;&#x25CF;&#x25CF; located beneath the compose message area in the chat.</span></span> <span data-ttu-id="66214-199">Los bots se agregan a un chat mediante la **@** clave "" y seleccionando **obtener bots**.</span><span class="sxs-lookup"><span data-stu-id="66214-199">Bots are added to a meeting chat using the "**@**" key and selecting **Get bots**.</span></span>

<span data-ttu-id="66214-200">✔ La identidad del usuario *debe* confirmarse mediante el [SSO de pestañas](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="66214-200">✔ The user identity *must* be confirmed via [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="66214-201">Tras esta autenticación, la aplicación puede recuperar el rol de usuario a través de la API de GetParticipant.</span><span class="sxs-lookup"><span data-stu-id="66214-201">Following this authentication, the app can retrieve the user role via the GetParticipant API.</span></span>

 <span data-ttu-id="66214-202">✔ Basándose en el rol de usuario, la aplicación ahora tendrá la capacidad de presentar experiencias específicas de roles.</span><span class="sxs-lookup"><span data-stu-id="66214-202">✔ Based on the user role, the app will now have the capability to present role specific experiences.</span></span> <span data-ttu-id="66214-203">Por ejemplo, una aplicación de sondeo puede permitir que solo los organizadores y los moderadores creen un nuevo sondeo.</span><span class="sxs-lookup"><span data-stu-id="66214-203">For example, a polling app can allow only organizers and presenters to create a new poll.</span></span>

> <span data-ttu-id="66214-204">**Nota**: las asignaciones de roles se pueden cambiar mientras una reunión está en curso.</span><span class="sxs-lookup"><span data-stu-id="66214-204">**NOTE**: Role assignments can be changed while a meeting is in progress.</span></span>  <span data-ttu-id="66214-205">*Vea* [roles en una reunión de Microsoft Teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span><span class="sxs-lookup"><span data-stu-id="66214-205">*See* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span> 

### <a name="in-meeting"></a><span data-ttu-id="66214-206">En reunión</span><span class="sxs-lookup"><span data-stu-id="66214-206">In-meeting</span></span>

#### <a name="side-panel"></a><span data-ttu-id="66214-207">**panel lateral**</span><span class="sxs-lookup"><span data-stu-id="66214-207">**side-panel**</span></span>

<span data-ttu-id="66214-208">✔ En el manifiesto de la aplicación agregue **sidePanel** a la matriz **meetingSurfaces** como se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="66214-208">✔ In your app manifest add **sidePanel** to the **meetingSurfaces** array as described above.</span></span>

<span data-ttu-id="66214-209">✔ En la reunión y en todos los escenarios, la aplicación se representará en una pestaña en la reunión que se 320 PX en ancho.</span><span class="sxs-lookup"><span data-stu-id="66214-209">✔ In the meeting as well as in all scenarios, the app will be rendered in an in-meeting tab that is 320px in width.</span></span> <span data-ttu-id="66214-210">La pestaña debe estar optimizada para esto.</span><span class="sxs-lookup"><span data-stu-id="66214-210">Your tab must be optimized for this.</span></span> <span data-ttu-id="66214-211">*Consulte*la [interfaz FrameContext](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="66214-211">*See*, [FrameContext interface](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)</span></span>

<span data-ttu-id="66214-212">✔ Consulte el SDK de Microsoft [Teams](../tabs/how-to/access-teams-context.md#user-context) para usar la API de **userContext** para enrutar las solicitudes en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="66214-212">✔Refer to the [Teams SDK](../tabs/how-to/access-teams-context.md#user-context) to use the **userContext** API to route requests accordingly.</span></span>

<span data-ttu-id="66214-213">✔ Consulte el [flujo de autenticación de Teams para pestañas](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="66214-213">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="66214-214">El flujo de autenticación para pestañas es muy similar al flujo de autenticación de los sitios Web.</span><span class="sxs-lookup"><span data-stu-id="66214-214">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="66214-215">Por lo tanto, las pestañas pueden usar OAuth 2,0 directamente.</span><span class="sxs-lookup"><span data-stu-id="66214-215">Thus, tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="66214-216">*Vea también*el [flujo de código de autorización de Microsoft Identity platform y OAuth 2,0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span><span class="sxs-lookup"><span data-stu-id="66214-216">*See also*, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="66214-217">**cuadro de diálogo en la reunión**</span><span class="sxs-lookup"><span data-stu-id="66214-217">**in-meeting dialog**</span></span>

<span data-ttu-id="66214-218">✔ Debe adherirse a las [instrucciones de diseño del cuadro de diálogo en reunión](designing-in-meeting-dialog.md).</span><span class="sxs-lookup"><span data-stu-id="66214-218">✔ You must adhere to the [in-meeting dialog design guidelines](designing-in-meeting-dialog.md).</span></span>

<span data-ttu-id="66214-219">✔ Consulte el [flujo de autenticación de Teams para pestañas](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="66214-219">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="66214-220">✔ Usar la API de [notificación](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) para indicar que se debe desencadenar una notificación de burbuja.</span><span class="sxs-lookup"><span data-stu-id="66214-220">✔ Use the [notification](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification needs to be triggered.</span></span>

<span data-ttu-id="66214-221">✔ Como parte de la carga de la solicitud de notificación, incluya la dirección URL donde se hospeda el contenido que se va a mostrar.</span><span class="sxs-lookup"><span data-stu-id="66214-221">✔ As part of the notification request payload, include the URL where the content to be showcased is hosted.</span></span>

> [!NOTE]
> <span data-ttu-id="66214-222">Estas notificaciones son persistentes en su naturaleza.</span><span class="sxs-lookup"><span data-stu-id="66214-222">These notifications are persistent in nature.</span></span> <span data-ttu-id="66214-223">Debe invocar la función [**submitTask ()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) para descartar automáticamente una vez que un usuario realiza una acción en la vista Web.</span><span class="sxs-lookup"><span data-stu-id="66214-223">You must invoke the [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to auto-dismiss after a user takes an action in the web-view.</span></span> <span data-ttu-id="66214-224">Este es un requisito para el envío de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="66214-224">This is a requirement for app submission.</span></span> <span data-ttu-id="66214-225">*Vea también*, [Teams SDK: módulo de tareas](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="66214-225">*See also*, [Teams SDK: task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>

### <a name="post-meeting"></a><span data-ttu-id="66214-226">Después de la reunión</span><span class="sxs-lookup"><span data-stu-id="66214-226">Post-meeting</span></span>

<span data-ttu-id="66214-227">Las configuraciones posteriores a la reunión y antes de la reunión son equivalentes.</span><span class="sxs-lookup"><span data-stu-id="66214-227">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="meeting-app-sample"></a><span data-ttu-id="66214-228">Ejemplo de aplicación de reunión</span><span class="sxs-lookup"><span data-stu-id="66214-228">Meeting app sample</span></span>

 > [!div class="nextstepaction"]
> [<span data-ttu-id="66214-229">Aplicación de generador de tokens de reunión</span><span class="sxs-lookup"><span data-stu-id="66214-229">Meeting token generator app</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)

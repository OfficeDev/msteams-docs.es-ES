---
title: Crear aplicaciones para reuniones de equipos
author: laujan
description: creación de aplicaciones para reuniones de Microsoft Teams
ms.topic: conceptual
ms.author: lajanuar
keywords: API de las aplicaciones de Microsoft Teams rol de participante de usuario
ms.openlocfilehash: cf42d660c9b4a82f8e28d4d4379194c1bcc681e1
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796172"
---
# <a name="create-apps-for-teams-meetings-developer-preview"></a><span data-ttu-id="64f59-104">Creación de aplicaciones para reuniones de Microsoft Teams (vista previa para desarrolladores)</span><span class="sxs-lookup"><span data-stu-id="64f59-104">Create apps for Teams meetings (Developer Preview)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="64f59-105">Las características incluidas en Microsoft Teams Developer Preview se proporcionan solo para fines de acceso anticipado, pruebas y comentarios.</span><span class="sxs-lookup"><span data-stu-id="64f59-105">Features included in Microsoft Teams Developer Preview are provided for early-access, testing, and feedback purposes only.</span></span> <span data-ttu-id="64f59-106">Pueden sufrir cambios antes de que estén disponibles en la versión pública y no deben usarse en las aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="64f59-106">They may undergo changes before becoming available in the public release and should not be used in production applications.</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="64f59-107">Requisitos previos y consideraciones</span><span class="sxs-lookup"><span data-stu-id="64f59-107">Prerequisites and considerations</span></span>

1. <span data-ttu-id="64f59-108">Las aplicaciones en las reuniones necesitan conocimientos básicos del desarrollo de aplicaciones de Microsoft [Teams](../overview.md).</span><span class="sxs-lookup"><span data-stu-id="64f59-108">Apps in meetings require some basic knowledge of [Teams app development](../overview.md).</span></span> <span data-ttu-id="64f59-109">Una aplicación en una reunión puede estar formada por [pestañas](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md)y características de [extensiones de mensajería](../messaging-extensions/what-are-messaging-extensions.md) y necesitará actualizaciones en el manifiesto de la [aplicación](#update-your-app-manifest) de Microsoft Teams para indicar que la aplicación está disponible para las reuniones.</span><span class="sxs-lookup"><span data-stu-id="64f59-109">An app in a meeting can comprise of [tabs](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md), and [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md) features and will require updates to the Teams [app manifest](#update-your-app-manifest) to indicate that the app is available for meetings</span></span>

1. <span data-ttu-id="64f59-110">Para que la aplicación funcione en el ciclo de vida de la reunión como una pestaña, debe admitir pestañas configurables en el [ámbito Groupchat](../resources/schema/manifest-schema.md#configurabletabs).</span><span class="sxs-lookup"><span data-stu-id="64f59-110">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs).</span></span> <span data-ttu-id="64f59-111">*Consulte* [ampliar la aplicación de Microsoft Teams con una pestaña personalizada](../tabs/how-to/add-tab.md). Admitir el `groupchat` ámbito habilitará la aplicación en chats [anteriores](teams-apps-in-meetings.md#pre-meeting-app-experience) y [posteriores](teams-apps-in-meetings.md#post-meeting-app-experience) a la reunión.</span><span class="sxs-lookup"><span data-stu-id="64f59-111">*See* [Extend your Teams app with a custom tab](../tabs/how-to/add-tab.md). Supporting the `groupchat` scope will enable your app in [pre-meeting](teams-apps-in-meetings.md#pre-meeting-app-experience) and [post-meeting](teams-apps-in-meetings.md#post-meeting-app-experience) chats.</span></span>

1. <span data-ttu-id="64f59-112">Los parámetros de dirección URL `meetingId` de la API de la reunión pueden requerir, `userId` y el [tenantId](/onedrive/find-your-office-365-tenant-id) , están disponibles como parte de la actividad del SDK del cliente de Microsoft Teams y del bot.</span><span class="sxs-lookup"><span data-stu-id="64f59-112">Meeting API URL parameters may require `meetingId`, `userId`, and the [tenantId](/onedrive/find-your-office-365-tenant-id) These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="64f59-113">Además, se puede recuperar información fiable sobre el identificador de usuario y el identificador de inquilino mediante la [autenticación SSO de pestañas](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="64f59-113">Additionally, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

1. <span data-ttu-id="64f59-114">Algunas API de reunión, como `GetParticipant` requerirán un [registro de Bot y un identificador de aplicación de bot](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) para generar tokens de autenticación.</span><span class="sxs-lookup"><span data-stu-id="64f59-114">Some meeting APIs, such as `GetParticipant` will require a [bot registration and bot app ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) to generate auth tokens.</span></span>

1. <span data-ttu-id="64f59-115">Los desarrolladores deben adherirse a las directrices generales de diseño de la pestaña de Microsoft [Teams](../tabs/design/tabs.md) para los escenarios anteriores y posteriores a la reunión, así como las [directrices de diálogo en reunión](design/designing-in-meeting-dialog.md) para los diálogos que se desencadenan durante la reunión de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="64f59-115">Developers must adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios as well as the [in-meeting dialog guidelines](design/designing-in-meeting-dialog.md) for in-meeting dialog triggered during a Teams meeting.</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="64f59-116">Referencia de API de las aplicaciones de reunión</span><span class="sxs-lookup"><span data-stu-id="64f59-116">Meeting apps API reference</span></span>

|<span data-ttu-id="64f59-117">API</span><span class="sxs-lookup"><span data-stu-id="64f59-117">API</span></span>|<span data-ttu-id="64f59-118">Descripción</span><span class="sxs-lookup"><span data-stu-id="64f59-118">Description</span></span>|<span data-ttu-id="64f59-119">Solicitud</span><span class="sxs-lookup"><span data-stu-id="64f59-119">Request</span></span>|<span data-ttu-id="64f59-120">Origen</span><span class="sxs-lookup"><span data-stu-id="64f59-120">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="64f59-121">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="64f59-121">**GetUserContext**</span></span>| <span data-ttu-id="64f59-122">Obtener información contextual para mostrar contenido relevante en una pestaña de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="64f59-122">Get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="64f59-123">_**Microsoft Teams. getContext (() => {/ *...* / } )**_</span><span class="sxs-lookup"><span data-stu-id="64f59-123">_**microsoftTeams.getContext( ( ) => {  / *...* / } )**_</span></span>|<span data-ttu-id="64f59-124">SDK del cliente de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="64f59-124">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="64f59-125">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="64f59-125">**GetParticipant**</span></span>|<span data-ttu-id="64f59-126">Esta API permite que un bot obtenga información de un participante por el identificador de la reunión y el identificador del participante.</span><span class="sxs-lookup"><span data-stu-id="64f59-126">This API allows a bot to fetch a participant information by meeting id and participant id.</span></span>|<span data-ttu-id="64f59-127">**Get** _**/v1/Meetings/{meetingId}/participants/{participantId}? tenantid = {tenantid}**_</span><span class="sxs-lookup"><span data-stu-id="64f59-127">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="64f59-128">SDK de Microsoft bot Framework</span><span class="sxs-lookup"><span data-stu-id="64f59-128">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="64f59-129">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="64f59-129">**NotificationSignal**</span></span> |<span data-ttu-id="64f59-130">Las señales de reunión se entregarán con la siguiente API de notificación de conversación existente (para el chat de bot? o del usuario).</span><span class="sxs-lookup"><span data-stu-id="64f59-130">Meeting signals will be delivered using the following existing conversation notification API (for user-bot chat).</span></span> <span data-ttu-id="64f59-131">Esta API permite que los desarrolladores señalen según la acción del usuario final para mostrar-caso de un burbuja de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="64f59-131">This API allows developers to signal based on end-user action to show-case an in-meeting dialog bubble.</span></span>|<span data-ttu-id="64f59-132">**Publicar** _**/V3/Conversations/{conversationId}/Activities**_</span><span class="sxs-lookup"><span data-stu-id="64f59-132">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="64f59-133">SDK de Microsoft bot Framework</span><span class="sxs-lookup"><span data-stu-id="64f59-133">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="64f59-134">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="64f59-134">GetUserContext</span></span>

<span data-ttu-id="64f59-135">Consulte nuestro [contexto de obtención de la documentación de la pestaña de Microsoft Teams](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) para obtener instrucciones sobre cómo identificar y recuperar información contextual para el contenido de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="64f59-135">Please refer to our [Get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and  retrieving contextual information for your tab content.</span></span> <span data-ttu-id="64f59-136">Como parte de la extensibilidad de las reuniones, se ha agregado un nuevo valor a la carga de respuesta:</span><span class="sxs-lookup"><span data-stu-id="64f59-136">As part of meetings extensibility, a new value has been added for the response payload:</span></span>

<span data-ttu-id="64f59-137">✔ **meetingId** : usada por una tabulación cuando se ejecuta en el contexto de la reunión.</span><span class="sxs-lookup"><span data-stu-id="64f59-137">✔ **meetingId** : used by a tab when running in the meeting context.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="64f59-138">API de GetParticipant</span><span class="sxs-lookup"><span data-stu-id="64f59-138">GetParticipant API</span></span>

> [!NOTE]
>
> * <span data-ttu-id="64f59-139">No almacene en caché roles de participantes, ya que el organizador de la reunión puede cambiar un rol en cualquier punto en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="64f59-139">Do not cache participant roles since the meeting organizer can change a role at any point in time.</span></span>
>
> * <span data-ttu-id="64f59-140">Actualmente, Microsoft Teams no admite listas de distribución de gran tamaño o tamaños de lista de más de 350 participantes para la `GetParticipant` API.</span><span class="sxs-lookup"><span data-stu-id="64f59-140">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>
>
> * <span data-ttu-id="64f59-141">La compatibilidad con bot Framework SDK estará disponible próximamente.</span><span class="sxs-lookup"><span data-stu-id="64f59-141">Support for the Bot Framework SDK is coming soon.</span></span>

#### <a name="request"></a><span data-ttu-id="64f59-142">Solicitud</span><span class="sxs-lookup"><span data-stu-id="64f59-142">Request</span></span>

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

<span data-ttu-id="64f59-143">*Vea* la [referencia de la API de bot Framework](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="64f59-143">*See* the [Bot Framework API reference](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<!-- markdownlint-disable MD025 -->

<span data-ttu-id="64f59-144">**Ejemplo de C#**</span><span class="sxs-lookup"><span data-stu-id="64f59-144">**C# Example**</span></span>

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
}
```

* * *
<!-- markdownlint-disable MD001 -->

#### <a name="query-parameters"></a><span data-ttu-id="64f59-145">Parámetros de consulta</span><span class="sxs-lookup"><span data-stu-id="64f59-145">Query parameters</span></span>

|<span data-ttu-id="64f59-146">Valor</span><span class="sxs-lookup"><span data-stu-id="64f59-146">Value</span></span>|<span data-ttu-id="64f59-147">Tipo</span><span class="sxs-lookup"><span data-stu-id="64f59-147">Type</span></span>|<span data-ttu-id="64f59-148">Necesario</span><span class="sxs-lookup"><span data-stu-id="64f59-148">Required</span></span>|<span data-ttu-id="64f59-149">Descripción</span><span class="sxs-lookup"><span data-stu-id="64f59-149">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="64f59-150">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="64f59-150">**meetingId**</span></span>| <span data-ttu-id="64f59-151">string</span><span class="sxs-lookup"><span data-stu-id="64f59-151">string</span></span> | <span data-ttu-id="64f59-152">Sí</span><span class="sxs-lookup"><span data-stu-id="64f59-152">Yes</span></span> | <span data-ttu-id="64f59-153">El identificador de la reunión está disponible a través de la invocación de bots y Team Client SDK.</span><span class="sxs-lookup"><span data-stu-id="64f59-153">The meeting identifier is available via Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="64f59-154">**participantId**</span><span class="sxs-lookup"><span data-stu-id="64f59-154">**participantId**</span></span>| <span data-ttu-id="64f59-155">string</span><span class="sxs-lookup"><span data-stu-id="64f59-155">string</span></span> | <span data-ttu-id="64f59-156">Sí</span><span class="sxs-lookup"><span data-stu-id="64f59-156">Yes</span></span> | <span data-ttu-id="64f59-157">Este campo es el identificador de usuario y está disponible en la pestaña SSO, Bot invocación y el SDK del cliente de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="64f59-157">This field is the User ID and it is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="64f59-158">El SSO de pestaña es muy recomendable</span><span class="sxs-lookup"><span data-stu-id="64f59-158">Tab SSO is highly recommended</span></span>|
|<span data-ttu-id="64f59-159">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="64f59-159">**tenantId**</span></span>| <span data-ttu-id="64f59-160">string</span><span class="sxs-lookup"><span data-stu-id="64f59-160">string</span></span> | <span data-ttu-id="64f59-161">Sí</span><span class="sxs-lookup"><span data-stu-id="64f59-161">Yes</span></span> | <span data-ttu-id="64f59-162">Esto es necesario para los usuarios del inquilino.</span><span class="sxs-lookup"><span data-stu-id="64f59-162">This required for tenant users.</span></span> <span data-ttu-id="64f59-163">Está disponible en el SSO del cliente de pestañas, Bot invocación y el SDK del cliente de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="64f59-163">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="64f59-164">El SSO de pestaña es muy recomendable</span><span class="sxs-lookup"><span data-stu-id="64f59-164">Tab SSO is highly recommended</span></span>|

#### <a name="response-payload"></a><span data-ttu-id="64f59-165">Carga de respuesta</span><span class="sxs-lookup"><span data-stu-id="64f59-165">Response Payload</span></span>
<!-- markdownlint-disable MD036 -->

<span data-ttu-id="64f59-166">el **rol** de "reunión" puede ser *organizador* , *moderador* o *Asistente* .</span><span class="sxs-lookup"><span data-stu-id="64f59-166">**role** under "meeting" can be *Organizer* , *Presenter* , or *Attendee* .</span></span>

<span data-ttu-id="64f59-167">**Ejemplo 1**</span><span class="sxs-lookup"><span data-stu-id="64f59-167">**Example 1**</span></span>

```json
{
  "user":
  {
      "id": "29:1JKiJGPAX9TTxtGxhVo0wLx_zwzo-gG8Z-X03306vBwi9p-xMTEbDXsT6KH7-0kkTS8cD-2zkrsoV6f5WJ6_aYw",
      "aadObjectId": "6aebbad0-e5a5-424a-834a-20fb051f3c1a",
      "name": "Allan Deyoung",
      "givenName": "Allan",
      "surname": "Deyoung",
      "email": "Allan.Deyoung@microsoft.com",
      "userPrincipalName": "Allan.Deyoung@microsoft.com",
      "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
      "userRole": "user"
  },
  "meeting":
  {
      "role ": "Presenter",
      "inMeeting":true
  },
  "conversation":
  {
      "id": "<conversation id>"
  }
}
```
#### <a name="response-codes"></a><span data-ttu-id="64f59-168">Códigos de respuesta</span><span class="sxs-lookup"><span data-stu-id="64f59-168">Response Codes</span></span>

<span data-ttu-id="64f59-169">**403** : la aplicación no tiene permiso para obtener información sobre los participantes.</span><span class="sxs-lookup"><span data-stu-id="64f59-169">**403** : the app is not allowed to get participant information.</span></span> <span data-ttu-id="64f59-170">Esta será la respuesta de error más común y se desencadenará cuando la aplicación no se instale en la reunión, por ejemplo, cuando la aplicación está deshabilitada por el administrador de inquilinos o bloqueada durante la mitigación del sitio activo.</span><span class="sxs-lookup"><span data-stu-id="64f59-170">This will be the most common error response and is triggered when the app is not installed in the meeting such as when the app is disabled by tenant admin or blocked during live site mitigation.</span></span>  
<span data-ttu-id="64f59-171">**200** : la información del participante se recuperó correctamente</span><span class="sxs-lookup"><span data-stu-id="64f59-171">**200** : participant information successfully retrieved</span></span>  
<span data-ttu-id="64f59-172">**401** : token no válido</span><span class="sxs-lookup"><span data-stu-id="64f59-172">**401** : invalid token</span></span>  
<span data-ttu-id="64f59-173">**404** : la reunión no existe o el participante no se encuentra.</span><span class="sxs-lookup"><span data-stu-id="64f59-173">**404** : the meeting doesn't exist or participant can’t be found.</span></span>

<!-- markdownlint-disable MD024 -->
### <a name="notificationsignal-api"></a><span data-ttu-id="64f59-174">API de NotificationSignal</span><span class="sxs-lookup"><span data-stu-id="64f59-174">NotificationSignal API</span></span>

> [!NOTE]
> <span data-ttu-id="64f59-175">Cuando se invoca un cuadro de diálogo en la reunión, el mismo contenido también se presentará como un mensaje de chat.</span><span class="sxs-lookup"><span data-stu-id="64f59-175">When an in-meeting dialog is invoked, the same content will also be presented as a chat message.</span></span>

#### <a name="request"></a><span data-ttu-id="64f59-176">Solicitud</span><span class="sxs-lookup"><span data-stu-id="64f59-176">Request</span></span>

```http
POST /v3/conversations/{conversationId}/activities
```

#### <a name="query-parameters"></a><span data-ttu-id="64f59-177">Parámetros de consulta</span><span class="sxs-lookup"><span data-stu-id="64f59-177">Query parameters</span></span>

|<span data-ttu-id="64f59-178">Valor</span><span class="sxs-lookup"><span data-stu-id="64f59-178">Value</span></span>|<span data-ttu-id="64f59-179">Tipo</span><span class="sxs-lookup"><span data-stu-id="64f59-179">Type</span></span>|<span data-ttu-id="64f59-180">Necesario</span><span class="sxs-lookup"><span data-stu-id="64f59-180">Required</span></span>|<span data-ttu-id="64f59-181">Descripción</span><span class="sxs-lookup"><span data-stu-id="64f59-181">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="64f59-182">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="64f59-182">**conversationId**</span></span>| <span data-ttu-id="64f59-183">string</span><span class="sxs-lookup"><span data-stu-id="64f59-183">string</span></span> | <span data-ttu-id="64f59-184">Sí</span><span class="sxs-lookup"><span data-stu-id="64f59-184">Yes</span></span> | <span data-ttu-id="64f59-185">El identificador de conversación está disponible como parte de la invocación de bot</span><span class="sxs-lookup"><span data-stu-id="64f59-185">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="request-payload"></a><span data-ttu-id="64f59-186">Carga de solicitud</span><span class="sxs-lookup"><span data-stu-id="64f59-186">Request Payload</span></span>

> [!NOTE]
>
> <span data-ttu-id="64f59-187">El completionBotId de externalResourceUrl en la carga de la solicitud siguiente es un parámetro opcional.</span><span class="sxs-lookup"><span data-stu-id="64f59-187">The completionBotId in the externalResourceUrl in the requeste payload below is an optional parameter.</span></span> <span data-ttu-id="64f59-188">Se trata del identificador de bot que se declara en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="64f59-188">It is the Bot ID that is declared in the manifest.</span></span> <span data-ttu-id="64f59-189">El bot recibirá un objeto de resultado.</span><span class="sxs-lookup"><span data-stu-id="64f59-189">The bot will receive a result object.</span></span>

# <a name="json"></a>[<span data-ttu-id="64f59-190">JSON</span><span class="sxs-lookup"><span data-stu-id="64f59-190">JSON</span></span>](#tab/json)

```json
{
    "type": "message",
    "text": "John Phillips assigned you a weekly todo",
    "summary": "Don't forget to meet with Marketing next week",
    "channelData": {
        "notification": {
            "alertInMeeting": true,
            "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID"
        }
    },
    "replyToId": "1493070356924"
}
```

# <a name="cnet"></a>[<span data-ttu-id="64f59-191">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="64f59-191">C#/.NET</span></span>](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");
MeetingNotification notification = new MeetingNotification
  {
    AlertInMeeting = true,
    ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID"
  };
activity.ChannelData = new TeamsChannelData
  {
    Notification = notification
  };
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[<span data-ttu-id="64f59-192">JavaScript</span><span class="sxs-lookup"><span data-stu-id="64f59-192">JavaScript</span></span>](#tab/javascript)

```javascript

const replyActivity = MessageFactory.text('Hi'); // this could be an adaptive card instead
replyActivity.channelData = {
    notification: {
        alertInMeeting: true,
        externalResourceUrl: 'https://teams.microsoft.com/l/bubble/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID’
    }
};
await context.sendActivity(replyActivity);
```

* * *

> [!IMPORTANT]
> <span data-ttu-id="64f59-193">La dirección URL de la burbuja de contenido (URL de taskInfo) debe incluirse en la lista de [dominios válidos](../resources/schema/manifest-schema.md#validdomains) que se incluye en el manifiesto de la aplicación Teams.</span><span class="sxs-lookup"><span data-stu-id="64f59-193">The URL in the content bubble (taskInfo URL) must be included in the [valid domains](../resources/schema/manifest-schema.md#validdomains) list included in the Teams app manifest.</span></span>

#### <a name="response-codes"></a><span data-ttu-id="64f59-194">Códigos de respuesta</span><span class="sxs-lookup"><span data-stu-id="64f59-194">Response Codes</span></span>

<span data-ttu-id="64f59-195">**201** : la actividad con señal se ha enviado correctamente</span><span class="sxs-lookup"><span data-stu-id="64f59-195">**201** : activity with signal is successfully sent</span></span>  
<span data-ttu-id="64f59-196">**401** : token no válido</span><span class="sxs-lookup"><span data-stu-id="64f59-196">**401** : invalid token</span></span>  
<span data-ttu-id="64f59-197">**403** : la aplicación no puede enviar la señal.</span><span class="sxs-lookup"><span data-stu-id="64f59-197">**403** : the app is not allowed to send the signal.</span></span> <span data-ttu-id="64f59-198">En este caso, la carga debe contener un mensaje de error más detallado.</span><span class="sxs-lookup"><span data-stu-id="64f59-198">In this case, the payload should contain more detail error message.</span></span> <span data-ttu-id="64f59-199">Puede haber varios motivos: la aplicación está deshabilitada por el administrador de inquilinos, bloqueada durante la mitigación de sitios activos, etc.</span><span class="sxs-lookup"><span data-stu-id="64f59-199">There can be many reasons: app disabled by tenant admin, blocked during live site mitigation, etc.</span></span>  
<span data-ttu-id="64f59-200">**404** : el chat de reuniones no existe</span><span class="sxs-lookup"><span data-stu-id="64f59-200">**404** : meeting chat doesn't exist</span></span>  

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="64f59-201">Habilitar la aplicación para reuniones de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="64f59-201">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="64f59-202">Actualizar el manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="64f59-202">Update your app manifest</span></span>

<span data-ttu-id="64f59-203">Las funcionalidades de la aplicación reuniones se declaran en el **configurableTabs** manifiesto de la aplicación a través de los  ->  **ámbitos** configurableTabs y los matrices de **contexto** .</span><span class="sxs-lookup"><span data-stu-id="64f59-203">The meetings app capabilities are declared in your app manifest via the **configurableTabs** -> **scopes** and **context** arrays.</span></span> <span data-ttu-id="64f59-204">*Scope* define quién y *Context* define dónde estará disponible la aplicación.</span><span class="sxs-lookup"><span data-stu-id="64f59-204">*Scope* defines to whom and *context* defines where your app will be available.</span></span>

> [!NOTE]
> * <span data-ttu-id="64f59-205">Use el [esquema del manifiesto de vista previa de desarrollador](../resources/schema/manifest-schema-dev-preview.md) para probar esto en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="64f59-205">Please use [Developer Preview manifest schema](../resources/schema/manifest-schema-dev-preview.md) to try this in your app manifest.</span></span>

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

### <a name="context-property"></a><span data-ttu-id="64f59-206">Propiedad context</span><span class="sxs-lookup"><span data-stu-id="64f59-206">Context property</span></span>

<span data-ttu-id="64f59-207">La pestaña `context` y `scopes` las propiedades funcionan en armonía para permitirle determinar dónde quiere que aparezca la aplicación.</span><span class="sxs-lookup"><span data-stu-id="64f59-207">The tab `context` and `scopes` properties work in harmony to allow you to determine where you want your app to appear.</span></span> <span data-ttu-id="64f59-208">Las pestañas `team` del `groupchat` ámbito o pueden tener más de un contexto.</span><span class="sxs-lookup"><span data-stu-id="64f59-208">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="64f59-209">Los valores posibles para la propiedad context son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="64f59-209">The possible values for the context property are as follows:</span></span>

* <span data-ttu-id="64f59-210">**channelTab** : una pestaña en el encabezado de un canal de equipo.</span><span class="sxs-lookup"><span data-stu-id="64f59-210">**channelTab** : a tab in the header of a team channel.</span></span>
* <span data-ttu-id="64f59-211">**privateChatTab** : una pestaña en el encabezado de un grupo de chats entre un conjunto de usuarios que no están en el contexto de un equipo o una reunión.</span><span class="sxs-lookup"><span data-stu-id="64f59-211">**privateChatTab** : a tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span>
* <span data-ttu-id="64f59-212">**meetingChatTab** : una pestaña en el encabezado de un grupo de chats entre un conjunto de usuarios en el contexto de una reunión programada.</span><span class="sxs-lookup"><span data-stu-id="64f59-212">**meetingChatTab** : a tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span>
* <span data-ttu-id="64f59-213">**meetingDetailsTab** : una pestaña en el encabezado de la vista de detalles de la reunión del calendario.</span><span class="sxs-lookup"><span data-stu-id="64f59-213">**meetingDetailsTab** : a tab in the header of the meeting details view of the calendar.</span></span>
* <span data-ttu-id="64f59-214">**meetingSidePanel** : un panel en reunión que se abre a través de la barra unificada (barra u).</span><span class="sxs-lookup"><span data-stu-id="64f59-214">**meetingSidePanel** : an in-meeting panel opened via the unified bar (u-bar).</span></span>

> [!NOTE]
> <span data-ttu-id="64f59-215">La propiedad "context" actualmente no se admite y, por lo tanto, se omitirá en clientes móviles</span><span class="sxs-lookup"><span data-stu-id="64f59-215">"Context" property is currently not supported and thus will be ignored on mobile clients</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="64f59-216">Configurar la aplicación para escenarios de reuniones</span><span class="sxs-lookup"><span data-stu-id="64f59-216">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="64f59-217">Para que la aplicación esté visible en la galería de pestañas, necesita **admitir las pestañas configurables** y el **ámbito de chat en grupo** .</span><span class="sxs-lookup"><span data-stu-id="64f59-217">For your app to be visible in the tab gallery it needs to **support configurable tabs** and the **group chat scope** .</span></span>
>
> * <span data-ttu-id="64f59-218">Los clientes móviles solo admiten fichas en las superficies anteriores y posteriores a la reunión.</span><span class="sxs-lookup"><span data-stu-id="64f59-218">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="64f59-219">Pronto estarán disponibles las experiencias en reunión (el panel y el cuadro de diálogo en reunión) en dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="64f59-219">The In-meeting experiences (in-meeting dialog and panel) on mobile will be available soon.</span></span> <span data-ttu-id="64f59-220">Siga las [instrucciones para las pestañas de dispositivos móviles](../tabs/design/tabs-mobile.md) al crear las pestañas para dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="64f59-220">Follow the [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span> 

### <a name="pre-meeting"></a><span data-ttu-id="64f59-221">Reunión previa</span><span class="sxs-lookup"><span data-stu-id="64f59-221">Pre-meeting</span></span>

<span data-ttu-id="64f59-222">Los usuarios con roles de organizador o moderador agregan pestañas a una reunión con el botón más ➕ de las páginas de **chat** de reuniones y **detalles** de reuniones.</span><span class="sxs-lookup"><span data-stu-id="64f59-222">Users with organizer and/or presenter roles add tabs to a meeting using the plus ➕ button in the meeting **Chat** and meeting **details** pages.</span></span> <span data-ttu-id="64f59-223">Las extensiones de mensajería se agregan a a través del menú de puntos suspensivos/desbordamiento &#x25CF;&#x25CF;&#x25CF; situada debajo del área redactar mensaje en el chat.</span><span class="sxs-lookup"><span data-stu-id="64f59-223">Messaging extensions are added to via the ellipses/overflow menu &#x25CF;&#x25CF;&#x25CF; located beneath the compose message area in the chat.</span></span> <span data-ttu-id="64f59-224">Los bots se agregan a un chat mediante la **@** clave "" y seleccionando **obtener bots** .</span><span class="sxs-lookup"><span data-stu-id="64f59-224">Bots are added to a meeting chat using the " **@** " key and selecting **Get bots** .</span></span>

<span data-ttu-id="64f59-225">✔ La identidad del usuario *debe* confirmarse mediante el [SSO de pestañas](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="64f59-225">✔ The user identity *must* be confirmed via [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="64f59-226">Tras esta autenticación, la aplicación puede recuperar el rol de usuario a través de la API de GetParticipant.</span><span class="sxs-lookup"><span data-stu-id="64f59-226">Following this authentication, the app can retrieve the user role via the GetParticipant API.</span></span>

 <span data-ttu-id="64f59-227">✔ Basándose en el rol de usuario, la aplicación ahora tendrá la capacidad de presentar experiencias específicas de roles.</span><span class="sxs-lookup"><span data-stu-id="64f59-227">✔ Based on the user role, the app will now have the capability to present role specific experiences.</span></span> <span data-ttu-id="64f59-228">Por ejemplo, una aplicación de sondeo puede permitir que solo los organizadores y los moderadores creen un nuevo sondeo.</span><span class="sxs-lookup"><span data-stu-id="64f59-228">For example, a polling app can allow only organizers and presenters to create a new poll.</span></span>

> <span data-ttu-id="64f59-229">**Nota** : las asignaciones de roles se pueden cambiar mientras una reunión está en curso.</span><span class="sxs-lookup"><span data-stu-id="64f59-229">**NOTE** : Role assignments can be changed while a meeting is in progress.</span></span>  <span data-ttu-id="64f59-230">*Vea* [roles en una reunión de Microsoft Teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span><span class="sxs-lookup"><span data-stu-id="64f59-230">*See* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span> 

### <a name="in-meeting"></a><span data-ttu-id="64f59-231">En reunión</span><span class="sxs-lookup"><span data-stu-id="64f59-231">In-meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="64f59-232">**sidePanel**</span><span class="sxs-lookup"><span data-stu-id="64f59-232">**sidePanel**</span></span>

<span data-ttu-id="64f59-233">✔ En el manifiesto de la aplicación, agregue **sidePanel** a la matriz de **contexto** , como se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="64f59-233">✔ In your app manifest add **sidePanel** to the **context** array as described above.</span></span>

<span data-ttu-id="64f59-234">✔ En la reunión y en todos los escenarios, la aplicación se representará en una pestaña en la reunión que se 320 PX en ancho.</span><span class="sxs-lookup"><span data-stu-id="64f59-234">✔ In the meeting as well as in all scenarios, the app will be rendered in an in-meeting tab that is 320px in width.</span></span> <span data-ttu-id="64f59-235">La pestaña debe estar optimizada para esto.</span><span class="sxs-lookup"><span data-stu-id="64f59-235">Your tab must be optimized for this.</span></span> <span data-ttu-id="64f59-236">*Consulte* la [interfaz FrameContext](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="64f59-236">*See* , [FrameContext interface](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)</span></span>

<span data-ttu-id="64f59-237">✔ Consulte el SDK de Microsoft [Teams](../tabs/how-to/access-teams-context.md#user-context) para usar la API de **userContext** para enrutar las solicitudes en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="64f59-237">✔Refer to the [Teams SDK](../tabs/how-to/access-teams-context.md#user-context) to use the **userContext** API to route requests accordingly.</span></span>

<span data-ttu-id="64f59-238">✔ Consulte el [flujo de autenticación de Teams para pestañas](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="64f59-238">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="64f59-239">El flujo de autenticación para pestañas es muy similar al flujo de autenticación de los sitios Web.</span><span class="sxs-lookup"><span data-stu-id="64f59-239">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="64f59-240">Por lo tanto, las pestañas pueden usar OAuth 2,0 directamente.</span><span class="sxs-lookup"><span data-stu-id="64f59-240">Thus, tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="64f59-241">*Vea también* el [flujo de código de autorización de Microsoft Identity platform y OAuth 2,0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span><span class="sxs-lookup"><span data-stu-id="64f59-241">*See also* , [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="64f59-242">**cuadro de diálogo en la reunión**</span><span class="sxs-lookup"><span data-stu-id="64f59-242">**in-meeting dialog**</span></span>

<span data-ttu-id="64f59-243">✔ Debe adherirse a las [instrucciones de diseño del cuadro de diálogo en reunión](design/designing-in-meeting-dialog.md).</span><span class="sxs-lookup"><span data-stu-id="64f59-243">✔ You must adhere to the [in-meeting dialog design guidelines](design/designing-in-meeting-dialog.md).</span></span>

<span data-ttu-id="64f59-244">✔ Consulte el [flujo de autenticación de Teams para pestañas](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="64f59-244">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="64f59-245">✔ Usar la API de [notificación](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) para indicar que se debe desencadenar una notificación de burbuja.</span><span class="sxs-lookup"><span data-stu-id="64f59-245">✔ Use the [notification](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification needs to be triggered.</span></span>

<span data-ttu-id="64f59-246">✔ Como parte de la carga de la solicitud de notificación, incluya la dirección URL donde se hospeda el contenido que se va a mostrar.</span><span class="sxs-lookup"><span data-stu-id="64f59-246">✔ As part of the notification request payload, include the URL where the content to be showcased is hosted.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="64f59-247">Estas notificaciones son persistentes en su naturaleza.</span><span class="sxs-lookup"><span data-stu-id="64f59-247">These notifications are persistent in nature.</span></span> <span data-ttu-id="64f59-248">Debe invocar la función [**submitTask ()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) para descartar automáticamente una vez que un usuario realiza una acción en la vista Web.</span><span class="sxs-lookup"><span data-stu-id="64f59-248">You must invoke the [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to auto-dismiss after a user takes an action in the web-view.</span></span> <span data-ttu-id="64f59-249">Este es un requisito para el envío de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="64f59-249">This is a requirement for app submission.</span></span> <span data-ttu-id="64f59-250">*Vea también* , [Teams SDK: módulo de tareas](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="64f59-250">*See also* , [Teams SDK: task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
>
> * <span data-ttu-id="64f59-251">Si quiere que la aplicación admita usuarios anónimos, su carga de solicitud de invocación inicial debe basarse en el `from.id`  objeto (ID del usuario) request Metadata in the `from` Object, no el `from.aadObjectId` (ID de Azure Active Directory del usuario) request Metadata.</span><span class="sxs-lookup"><span data-stu-id="64f59-251">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id`  (ID of the user) request metadata in the `from` object, not the `from.aadObjectId` (Azure Active Directory ID of the user) request metadata.</span></span> <span data-ttu-id="64f59-252">*Consulte* [using Task modules in Tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) y [Create and Send The Task Module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span><span class="sxs-lookup"><span data-stu-id="64f59-252">*See* [Using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [Create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

### <a name="post-meeting"></a><span data-ttu-id="64f59-253">Después de la reunión</span><span class="sxs-lookup"><span data-stu-id="64f59-253">Post-meeting</span></span>

<span data-ttu-id="64f59-254">Las configuraciones posteriores a la reunión y antes de la reunión son equivalentes.</span><span class="sxs-lookup"><span data-stu-id="64f59-254">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="meeting-app-sample"></a><span data-ttu-id="64f59-255">Ejemplo de aplicación de reunión</span><span class="sxs-lookup"><span data-stu-id="64f59-255">Meeting app sample</span></span>

 > [!div class="nextstepaction"]
> [<span data-ttu-id="64f59-256">Aplicación de generador de tokens de reunión</span><span class="sxs-lookup"><span data-stu-id="64f59-256">Meeting token generator app</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)

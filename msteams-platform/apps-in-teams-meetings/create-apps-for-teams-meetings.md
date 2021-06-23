---
title: Requisitos previos y referencias de API para las aplicaciones en las reuniones de Teams
author: surbhigupta
description: Trabajar con aplicaciones para Teams reuniones
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: API de roles de participantes de reuniones de aplicaciones de teams
ms.openlocfilehash: e6d1c442f77f4d271c43d866c819d65697262b6b
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068562"
---
# <a name="prerequisites-and-api-references-for-apps-in-teams-meetings"></a><span data-ttu-id="cfe4c-104">Requisitos previos y referencias de API para las aplicaciones en las reuniones de Teams</span><span class="sxs-lookup"><span data-stu-id="cfe4c-104">Prerequisites and API references for apps in Teams meetings</span></span>

<span data-ttu-id="cfe4c-105">Para expandir las capacidades de tus aplicaciones en todo el ciclo de vida de la reunión, Teams te permite trabajar con aplicaciones para Teams reuniones.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-105">To expand the capabilities of your apps across the meeting lifecycle, Teams enables you to work with apps for Teams meetings.</span></span> <span data-ttu-id="cfe4c-106">Debes pasar por los requisitos previos y puedes usar las referencias a la API de aplicaciones de reunión para mejorar la experiencia de la reunión.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-106">You must  go through the prerequisites and you can use the meeting apps API references to enhance the meeting experience.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cfe4c-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cfe4c-107">Prerequisites</span></span>

<span data-ttu-id="cfe4c-108">Antes de trabajar con aplicaciones para Teams reuniones, debes comprender lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cfe4c-108">Before you work with apps for Teams meetings, you must have an understanding of the following:</span></span>

* <span data-ttu-id="cfe4c-109">Debes tener conocimientos sobre cómo desarrollar Teams aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-109">You must have knowledge of how to develop Teams apps.</span></span> <span data-ttu-id="cfe4c-110">Para obtener más información, [consulta Teams desarrollo de aplicaciones](../overview.md).</span><span class="sxs-lookup"><span data-stu-id="cfe4c-110">For more information, see [Teams app development](../overview.md).</span></span>

* <span data-ttu-id="cfe4c-111">Debes actualizar el manifiesto Teams aplicación para indicar que la aplicación está disponible para reuniones.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-111">You must update the Teams app manifest to indicate that the app is available for meetings.</span></span> <span data-ttu-id="cfe4c-112">Para obtener más información, consulta [manifiesto de la aplicación](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest).</span><span class="sxs-lookup"><span data-stu-id="cfe4c-112">For more information, see [app manifest](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest).</span></span>

* <span data-ttu-id="cfe4c-113">La aplicación debe admitir pestañas configurables en el ámbito groupchat, para que la aplicación funcione en el ciclo de vida de la reunión como pestaña. Para obtener más información, [vea groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) y [build a group tab](../build-your-first-app/build-channel-tab.md).</span><span class="sxs-lookup"><span data-stu-id="cfe4c-113">Your app must support configurable tabs in the groupchat scope, for your app to function in the meeting lifecycle as a tab. For more information, see [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md).</span></span>

* <span data-ttu-id="cfe4c-114">Debe cumplir las directrices generales Teams de diseño de pestañas para escenarios previos y posteriores a la reunión.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-114">You must adhere to general Teams tab design guidelines for pre and post-meeting scenarios.</span></span> <span data-ttu-id="cfe4c-115">Para obtener experiencias durante las reuniones, consulte las directrices de diseño de la pestaña en la reunión y del cuadro de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-115">For experiences during meetings, refer to the in-meeting tab and in-meeting dialog design guidelines.</span></span> <span data-ttu-id="cfe4c-116">Para obtener más información, [vea Teams de](../tabs/design/tabs.md)diseño de pestañas, directrices de diseño de pestañas en la reunión y directrices de diseño de cuadros de diálogo en la [reunión.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)</span><span class="sxs-lookup"><span data-stu-id="cfe4c-116">For more information, see [Teams tab design guidelines](../tabs/design/tabs.md), [in-meeting tab design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab), and [in-meeting dialog design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

* <span data-ttu-id="cfe4c-117">Debes admitir el ámbito para habilitar la aplicación en `groupchat` chats previos y posteriores a la reunión.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-117">You must support the `groupchat` scope to enable your app in pre-meeting and post-meeting chats.</span></span> <span data-ttu-id="cfe4c-118">Con la experiencia de la aplicación previa a la reunión, puedes encontrar y agregar aplicaciones de reunión y realizar tareas previas a la reunión.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-118">With the pre-meeting app experience, you can find and add meeting apps and perform pre-meeting tasks.</span></span> <span data-ttu-id="cfe4c-119">Con la experiencia de la aplicación posterior a la reunión, puedes ver los resultados de la reunión, como los resultados de encuestas o los comentarios.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-119">With post-meeting app experience, you can view the results of the meeting, such as poll survey results or feedback.</span></span>

* <span data-ttu-id="cfe4c-120">Los parámetros de dirección URL de la API de reunión deben `meetingId` `userId` tener , y `tenantId` .</span><span class="sxs-lookup"><span data-stu-id="cfe4c-120">Meeting API URL parameters must have `meetingId`, `userId`, and `tenantId`.</span></span> <span data-ttu-id="cfe4c-121">Están disponibles como parte de la actividad del SDK Teams cliente y el bot.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-121">These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="cfe4c-122">Además, puede recuperar información confiable para el identificador de usuario y el identificador de inquilino mediante la [autenticación de SSO de tabulación.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="cfe4c-122">In addition, you can retrieve reliable information for user ID and tenant ID using [tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="cfe4c-123">La `GetParticipant` API debe tener un registro de bot y un identificador para generar tokens de autenticación.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-123">The `GetParticipant` API must have a bot registration and ID to generate auth tokens.</span></span> <span data-ttu-id="cfe4c-124">Para obtener más información, vea [bot registration and ID](../build-your-first-app/build-bot.md).</span><span class="sxs-lookup"><span data-stu-id="cfe4c-124">For more information, see [bot registration and ID](../build-your-first-app/build-bot.md).</span></span>

* <span data-ttu-id="cfe4c-125">Para que la aplicación se actualice en tiempo real, debe estar actualizada en función de las actividades de eventos de la reunión.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-125">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="cfe4c-126">Estos eventos pueden estar dentro del cuadro de diálogo en la reunión y otras etapas a lo largo del ciclo de vida de la reunión.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-126">These events can be within the in-meeting dialog box and other stages across the meeting lifecycle.</span></span> <span data-ttu-id="cfe4c-127">Para el cuadro de diálogo en la reunión, vea el parámetro de `bot Id` finalización en `NotificationSignal` la API.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-127">For the in-meeting dialog box, see completion `bot Id` parameter in `NotificationSignal` API.</span></span>

<span data-ttu-id="cfe4c-128">Una vez que haya pasado por los requisitos previos, puede usar las referencias de api de aplicaciones de reunión , y eso le permite tener acceso a la información mediante atributos y mostrar `GetUserContext` `GetParticipant` contenido `NotificationSignal` relevante.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-128">After you have gone through the prerequisites, you can use the meeting apps API references `GetUserContext`, `GetParticipant`, and `NotificationSignal` that enable you to access information using attributes and display relevant content.</span></span>

## <a name="meeting-apps-api-references"></a><span data-ttu-id="cfe4c-129">Referencias de API de aplicaciones de reunión</span><span class="sxs-lookup"><span data-stu-id="cfe4c-129">Meeting apps API references</span></span>

<span data-ttu-id="cfe4c-130">Las nuevas extensibilidades de reuniones le proporcionan API que transforman la experiencia de la reunión.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-130">The new meeting extensibilities provide you with APIs that transform the meeting experience.</span></span> <span data-ttu-id="cfe4c-131">Con esta nueva funcionalidad, puedes crear aplicaciones o integrar aplicaciones existentes en el ciclo de vida de la reunión.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-131">With this new capability, you can build apps or integrate existing apps within the meeting lifecycle.</span></span> <span data-ttu-id="cfe4c-132">Puedes usar las API para que la aplicación conozca la reunión.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-132">You can use the APIs to make your app aware of the meeting.</span></span> <span data-ttu-id="cfe4c-133">Puede elegir qué API desea usar para mejorar la experiencia de la reunión.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-133">You can choose which APIs you want to use to enhance the meeting experience.</span></span>

<span data-ttu-id="cfe4c-134">En la tabla siguiente se proporciona una lista de estas API:</span><span class="sxs-lookup"><span data-stu-id="cfe4c-134">The following table provides a list of these APIs:</span></span>

|<span data-ttu-id="cfe4c-135">API</span><span class="sxs-lookup"><span data-stu-id="cfe4c-135">API</span></span>|<span data-ttu-id="cfe4c-136">Descripción</span><span class="sxs-lookup"><span data-stu-id="cfe4c-136">Description</span></span>|<span data-ttu-id="cfe4c-137">Solicitud</span><span class="sxs-lookup"><span data-stu-id="cfe4c-137">Request</span></span>|<span data-ttu-id="cfe4c-138">Origen</span><span class="sxs-lookup"><span data-stu-id="cfe4c-138">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="cfe4c-139">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="cfe4c-139">**GetUserContext**</span></span>| <span data-ttu-id="cfe4c-140">Esta API le permite obtener información contextual para mostrar contenido relevante en una Teams pestaña.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-140">This API enables you to get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="cfe4c-141">_**microsoftTeams.getContext( ( ) => { /*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="cfe4c-141">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="cfe4c-142">Microsoft Teams SDK de cliente</span><span class="sxs-lookup"><span data-stu-id="cfe4c-142">Microsoft Teams Client SDK</span></span>|
|<span data-ttu-id="cfe4c-143">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="cfe4c-143">**GetParticipant**</span></span>| <span data-ttu-id="cfe4c-144">Esta API permite que un bot obtenga información de los participantes mediante el identificador de reunión y el identificador de participante.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-144">This API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> |<span data-ttu-id="cfe4c-145">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="cfe4c-145">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="cfe4c-146">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="cfe4c-146">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="cfe4c-147">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="cfe4c-147">**NotificationSignal**</span></span> | <span data-ttu-id="cfe4c-148">Esta API le permite proporcionar señales de reunión que se entregan mediante la API de notificación de conversación existente para el chat de bots de usuario.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-148">This API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="cfe4c-149">Le permite señalar en función de la acción del usuario que muestra un cuadro de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-149">It allows you to signal based on user action that shows an in-meeting dialog box.</span></span> |<span data-ttu-id="cfe4c-150">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="cfe4c-150">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="cfe4c-151">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="cfe4c-151">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext-api"></a><span data-ttu-id="cfe4c-152">GetUserContext API</span><span class="sxs-lookup"><span data-stu-id="cfe4c-152">GetUserContext API</span></span>

<span data-ttu-id="cfe4c-153">Para identificar y recuperar información contextual para el contenido de la pestaña, vea [Obtener contexto para su Teams pestaña](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). se usa en una pestaña al ejecutarse en el contexto de la reunión y `meetingId` se agrega para la carga de respuesta.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-153">To identify and retrieve contextual information for your tab content, see [get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). `meetingId` is used by a tab when running in the meeting context and is added for the response payload.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="cfe4c-154">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="cfe4c-154">GetParticipant API</span></span>

> [!NOTE]
> * <span data-ttu-id="cfe4c-155">No almacenar en caché los roles de los participantes, ya que el organizador de la reunión puede cambiar los roles en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-155">Do not cache participant roles since the meeting organizer can change the roles any time.</span></span>
> * <span data-ttu-id="cfe4c-156">Teams actualmente no admite listas de distribución grandes ni tamaños de lista de más de 350 participantes para la `GetParticipant` API.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-156">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

<span data-ttu-id="cfe4c-157">La `GetParticipant` API permite que un bot obtenga información de los participantes mediante el identificador de reunión y el identificador de participante.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-157">The `GetParticipant` API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> <span data-ttu-id="cfe4c-158">La API incluye parámetros de consulta, ejemplos y códigos de respuesta.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-158">The API includes query parameters, examples, and response codes.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="cfe4c-159">Parámetros de consulta</span><span class="sxs-lookup"><span data-stu-id="cfe4c-159">Query parameters</span></span>

<span data-ttu-id="cfe4c-160">La `GetParticipant` API incluye los siguientes parámetros de consulta:</span><span class="sxs-lookup"><span data-stu-id="cfe4c-160">The `GetParticipant` API includes the following query parameters:</span></span>

|<span data-ttu-id="cfe4c-161">Valor</span><span class="sxs-lookup"><span data-stu-id="cfe4c-161">Value</span></span>|<span data-ttu-id="cfe4c-162">Tipo</span><span class="sxs-lookup"><span data-stu-id="cfe4c-162">Type</span></span>|<span data-ttu-id="cfe4c-163">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="cfe4c-163">Required</span></span>|<span data-ttu-id="cfe4c-164">Descripción</span><span class="sxs-lookup"><span data-stu-id="cfe4c-164">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="cfe4c-165">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="cfe4c-165">**meetingId**</span></span>| <span data-ttu-id="cfe4c-166">Cadena</span><span class="sxs-lookup"><span data-stu-id="cfe4c-166">String</span></span> | <span data-ttu-id="cfe4c-167">Sí</span><span class="sxs-lookup"><span data-stu-id="cfe4c-167">Yes</span></span> | <span data-ttu-id="cfe4c-168">El identificador de reunión está disponible a través de Bot Invoke y Teams CLIENT SDK.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-168">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="cfe4c-169">**participantId**</span><span class="sxs-lookup"><span data-stu-id="cfe4c-169">**participantId**</span></span>| <span data-ttu-id="cfe4c-170">Cadena</span><span class="sxs-lookup"><span data-stu-id="cfe4c-170">String</span></span> | <span data-ttu-id="cfe4c-171">Sí</span><span class="sxs-lookup"><span data-stu-id="cfe4c-171">Yes</span></span> | <span data-ttu-id="cfe4c-172">El identificador de participante es el identificador de usuario.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-172">The participant ID is the user ID.</span></span> <span data-ttu-id="cfe4c-173">Está disponible en TAB SSO, Bot Invoke y Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-173">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="cfe4c-174">Se recomienda obtener un identificador de participante del SSO de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-174">It is recommended to get a participant ID from the Tab SSO.</span></span> |
|<span data-ttu-id="cfe4c-175">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="cfe4c-175">**tenantId**</span></span>| <span data-ttu-id="cfe4c-176">Cadena</span><span class="sxs-lookup"><span data-stu-id="cfe4c-176">String</span></span> | <span data-ttu-id="cfe4c-177">Sí</span><span class="sxs-lookup"><span data-stu-id="cfe4c-177">Yes</span></span> | <span data-ttu-id="cfe4c-178">El identificador de inquilino es necesario para los usuarios del espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-178">The tenant ID is required for the tenant users.</span></span> <span data-ttu-id="cfe4c-179">Está disponible en TAB SSO, Bot Invoke y Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-179">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="cfe4c-180">Se recomienda obtener un identificador de inquilino del SSO de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-180">It is recommended to get a tenant ID from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="cfe4c-181">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="cfe4c-181">Example</span></span>

<span data-ttu-id="cfe4c-182">La `GetParticipant` API incluye los siguientes ejemplos:</span><span class="sxs-lookup"><span data-stu-id="cfe4c-182">The `GetParticipant` API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="cfe4c-183">C#</span><span class="sxs-lookup"><span data-stu-id="cfe4c-183">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="cfe4c-184">JavaScript</span><span class="sxs-lookup"><span data-stu-id="cfe4c-184">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="cfe4c-185">JSON</span><span class="sxs-lookup"><span data-stu-id="cfe4c-185">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

* * *

<span data-ttu-id="cfe4c-186">El cuerpo de la respuesta JSON `GetParticipant` para la API es:</span><span class="sxs-lookup"><span data-stu-id="cfe4c-186">The JSON response body for `GetParticipant` API is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="cfe4c-187">Códigos de respuesta</span><span class="sxs-lookup"><span data-stu-id="cfe4c-187">Response codes</span></span>

<span data-ttu-id="cfe4c-188">La `GetParticipant` API incluye los siguientes códigos de respuesta:</span><span class="sxs-lookup"><span data-stu-id="cfe4c-188">The `GetParticipant` API includes the following response codes:</span></span>

|<span data-ttu-id="cfe4c-189">Código de respuesta</span><span class="sxs-lookup"><span data-stu-id="cfe4c-189">Response code</span></span>|<span data-ttu-id="cfe4c-190">Descripción</span><span class="sxs-lookup"><span data-stu-id="cfe4c-190">Description</span></span>|
|---|---|
| <span data-ttu-id="cfe4c-191">**403**</span><span class="sxs-lookup"><span data-stu-id="cfe4c-191">**403**</span></span> | <span data-ttu-id="cfe4c-192">La aplicación no puede obtener información de los participantes.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-192">The app is not allowed to get participant information.</span></span> <span data-ttu-id="cfe4c-193">Esta es la respuesta de error más común y se desencadena si la aplicación no está instalada en la reunión.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-193">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="cfe4c-194">Por ejemplo, si la aplicación está deshabilitada por el administrador del espacio empresarial o bloqueada durante la migración del sitio en directo.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-194">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>|
| <span data-ttu-id="cfe4c-195">**200**</span><span class="sxs-lookup"><span data-stu-id="cfe4c-195">**200**</span></span> | <span data-ttu-id="cfe4c-196">La información del participante se recupera correctamente.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-196">The participant information is successfully retrieved.</span></span>|
| <span data-ttu-id="cfe4c-197">**401**</span><span class="sxs-lookup"><span data-stu-id="cfe4c-197">**401**</span></span> | <span data-ttu-id="cfe4c-198">La aplicación responde con un token no válido.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-198">The app responds with an invalid token.</span></span>|
| <span data-ttu-id="cfe4c-199">**404**</span><span class="sxs-lookup"><span data-stu-id="cfe4c-199">**404**</span></span> | <span data-ttu-id="cfe4c-200">La reunión ha expirado o no se encuentra el participante.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-200">The meeting has either expired or participant cannot be found.</span></span>|
| <span data-ttu-id="cfe4c-201">**500**</span><span class="sxs-lookup"><span data-stu-id="cfe4c-201">**500**</span></span> | <span data-ttu-id="cfe4c-202">La reunión ha expirado (más de 60 días) desde que finalizó la reunión o los participantes no tienen permisos en función de su rol.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-202">The meeting has either expired (more than 60 days) since the meeting ended or the participants do not have permissions based on their role.</span></span>|

### <a name="notificationsignal-api"></a><span data-ttu-id="cfe4c-203">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="cfe4c-203">NotificationSignal API</span></span>

<span data-ttu-id="cfe4c-204">Todos los usuarios de una reunión reciben las notificaciones enviadas a través de la `NotificationSignal` API.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-204">All users in a meeting receive the notifications sent through the `NotificationSignal` API.</span></span>

> [!NOTE]
> * <span data-ttu-id="cfe4c-205">Cuando se invoca un cuadro de diálogo en la reunión, el contenido se presenta como un mensaje de chat.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-205">When an in-meeting dialog box is invoked, the content is presented as a chat message.</span></span>
> * <span data-ttu-id="cfe4c-206">Actualmente, no se admite el envío de notificaciones dirigidas.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-206">Currently, sending targeted notifications is not supported.</span></span>

<span data-ttu-id="cfe4c-207">`NotificationSignal` La API le permite proporcionar señales de reunión que se entregan mediante la API de notificación de conversación existente para el chat de bots de usuario.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-207">`NotificationSignal` API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="cfe4c-208">Esta API le permite señalar en función de la acción del usuario que muestra un cuadro de diálogo en la reunión.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-208">This API allows you to signal based on user action that shows an in-meeting dialog box.</span></span> <span data-ttu-id="cfe4c-209">La API incluye parámetros de consulta, ejemplos y códigos de respuesta.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-209">The API includes query parameter, examples, and response codes.</span></span>

#### <a name="query-parameter"></a><span data-ttu-id="cfe4c-210">Parámetro de consulta</span><span class="sxs-lookup"><span data-stu-id="cfe4c-210">Query parameter</span></span>

<span data-ttu-id="cfe4c-211">La `NotificationSignal` API incluye el siguiente parámetro de consulta:</span><span class="sxs-lookup"><span data-stu-id="cfe4c-211">The `NotificationSignal` API includes the following query parameter:</span></span>

|<span data-ttu-id="cfe4c-212">Valor</span><span class="sxs-lookup"><span data-stu-id="cfe4c-212">Value</span></span>|<span data-ttu-id="cfe4c-213">Tipo</span><span class="sxs-lookup"><span data-stu-id="cfe4c-213">Type</span></span>|<span data-ttu-id="cfe4c-214">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="cfe4c-214">Required</span></span>|<span data-ttu-id="cfe4c-215">Descripción</span><span class="sxs-lookup"><span data-stu-id="cfe4c-215">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="cfe4c-216">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="cfe4c-216">**conversationId**</span></span>| <span data-ttu-id="cfe4c-217">Cadena</span><span class="sxs-lookup"><span data-stu-id="cfe4c-217">String</span></span> | <span data-ttu-id="cfe4c-218">Sí</span><span class="sxs-lookup"><span data-stu-id="cfe4c-218">Yes</span></span> | <span data-ttu-id="cfe4c-219">El identificador de conversación está disponible como parte de Bot Invoke.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-219">The conversation identifier is available as part of Bot Invoke.</span></span> |

#### <a name="examples"></a><span data-ttu-id="cfe4c-220">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="cfe4c-220">Examples</span></span>

<span data-ttu-id="cfe4c-221">Se `Bot ID` declara en el manifiesto y el bot recibe un objeto result.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-221">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span>

> [!NOTE]
> * <span data-ttu-id="cfe4c-222">El `completionBotId` parámetro de la es opcional en el ejemplo de carga `externalResourceUrl` solicitada.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-222">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="cfe4c-223">`Bot ID` se declara en el manifiesto y el bot recibe un objeto result.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-223">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="cfe4c-224">Los `externalResourceUrl` parámetros de ancho y alto deben estar en píxeles.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-224">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="cfe4c-225">Para asegurarse de que las dimensiones están dentro de los límites permitidos, vea [directrices de diseño](design/designing-apps-in-meetings.md).</span><span class="sxs-lookup"><span data-stu-id="cfe4c-225">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="cfe4c-226">La dirección URL es la página cargada como una en el cuadro de diálogo `<iframe>` en la reunión.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-226">The URL is the page loaded as an `<iframe>` in the in-meeting dialog box.</span></span> <span data-ttu-id="cfe4c-227">El dominio debe estar en la matriz de la aplicación `validDomains` en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-227">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

<span data-ttu-id="cfe4c-228">La `NotificationSignal` API incluye los siguientes ejemplos:</span><span class="sxs-lookup"><span data-stu-id="cfe4c-228">The `NotificationSignal` API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="cfe4c-229">C#</span><span class="sxs-lookup"><span data-stu-id="cfe4c-229">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="cfe4c-230">JavaScript</span><span class="sxs-lookup"><span data-stu-id="cfe4c-230">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="cfe4c-231">JSON</span><span class="sxs-lookup"><span data-stu-id="cfe4c-231">JSON</span></span>](#tab/json)

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

#### <a name="response-codes"></a><span data-ttu-id="cfe4c-232">Códigos de respuesta</span><span class="sxs-lookup"><span data-stu-id="cfe4c-232">Response codes</span></span>

<span data-ttu-id="cfe4c-233">La `NotificationSignal` API incluye los siguientes códigos de respuesta:</span><span class="sxs-lookup"><span data-stu-id="cfe4c-233">The `NotificationSignal` API includes the following response codes:</span></span>

|<span data-ttu-id="cfe4c-234">Código de respuesta</span><span class="sxs-lookup"><span data-stu-id="cfe4c-234">Response code</span></span>|<span data-ttu-id="cfe4c-235">Descripción</span><span class="sxs-lookup"><span data-stu-id="cfe4c-235">Description</span></span>|
|---|---|
| <span data-ttu-id="cfe4c-236">**201**</span><span class="sxs-lookup"><span data-stu-id="cfe4c-236">**201**</span></span> | <span data-ttu-id="cfe4c-237">La actividad con señal se envía correctamente.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-237">The activity with signal is successfully sent.</span></span> |
| <span data-ttu-id="cfe4c-238">**401**</span><span class="sxs-lookup"><span data-stu-id="cfe4c-238">**401**</span></span> | <span data-ttu-id="cfe4c-239">La aplicación responde con un token no válido.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-239">The app responds with an invalid token.</span></span> |
| <span data-ttu-id="cfe4c-240">**403**</span><span class="sxs-lookup"><span data-stu-id="cfe4c-240">**403**</span></span> | <span data-ttu-id="cfe4c-241">La aplicación no puede enviar la señal.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-241">The app is unable to send the signal.</span></span> <span data-ttu-id="cfe4c-242">Esto puede ocurrir debido a diversos motivos, como que el administrador de inquilinos deshabilita la aplicación, la aplicación se bloquea durante la migración del sitio en directo, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-242">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="cfe4c-243">En este caso, la carga contiene un mensaje de error detallado.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-243">In this case, the payload contains a detailed error message.</span></span> |
| <span data-ttu-id="cfe4c-244">**404**</span><span class="sxs-lookup"><span data-stu-id="cfe4c-244">**404**</span></span> | <span data-ttu-id="cfe4c-245">El chat de reunión no existe.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-245">The meeting chat does not exist.</span></span> |

## <a name="code-sample"></a><span data-ttu-id="cfe4c-246">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="cfe4c-246">Code sample</span></span>

|<span data-ttu-id="cfe4c-247">Nombre de ejemplo</span><span class="sxs-lookup"><span data-stu-id="cfe4c-247">Sample name</span></span> | <span data-ttu-id="cfe4c-248">Descripción</span><span class="sxs-lookup"><span data-stu-id="cfe4c-248">Description</span></span> | <span data-ttu-id="cfe4c-249">.NET</span><span class="sxs-lookup"><span data-stu-id="cfe4c-249">.NET</span></span> | <span data-ttu-id="cfe4c-250">Node.js</span><span class="sxs-lookup"><span data-stu-id="cfe4c-250">Node.js</span></span> |
|----------------|-----------------|--------------|--------------|
| <span data-ttu-id="cfe4c-251">Extensibilidad de reuniones</span><span class="sxs-lookup"><span data-stu-id="cfe4c-251">Meetings extensibility</span></span> | <span data-ttu-id="cfe4c-252">Microsoft Teams extensibilidad de reunión para pasar tokens.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-252">Microsoft Teams meeting extensibility sample for passing tokens.</span></span> | [<span data-ttu-id="cfe4c-253">View</span><span class="sxs-lookup"><span data-stu-id="cfe4c-253">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [<span data-ttu-id="cfe4c-254">View</span><span class="sxs-lookup"><span data-stu-id="cfe4c-254">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| <span data-ttu-id="cfe4c-255">Bot de burbuja de contenido de reunión</span><span class="sxs-lookup"><span data-stu-id="cfe4c-255">Meeting content bubble bot</span></span> | <span data-ttu-id="cfe4c-256">Microsoft Teams de extensibilidad de reuniones para interactuar con el bot de burbujas de contenido en una reunión.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-256">Microsoft Teams meeting extensibility sample for interacting with content bubble bot in a meeting.</span></span> | [<span data-ttu-id="cfe4c-257">View</span><span class="sxs-lookup"><span data-stu-id="cfe4c-257">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [<span data-ttu-id="cfe4c-258">View</span><span class="sxs-lookup"><span data-stu-id="cfe4c-258">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| <span data-ttu-id="cfe4c-259">MeetingSidePanel</span><span class="sxs-lookup"><span data-stu-id="cfe4c-259">Meeting meetingSidePanel</span></span> | <span data-ttu-id="cfe4c-260">Microsoft Teams extensibilidad de reuniones para interactuar con el panel lateral en la reunión.</span><span class="sxs-lookup"><span data-stu-id="cfe4c-260">Microsoft Teams meeting extensibility sample for interacting with the side panel in-meeting.</span></span> | [<span data-ttu-id="cfe4c-261">View</span><span class="sxs-lookup"><span data-stu-id="cfe4c-261">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [<span data-ttu-id="cfe4c-262">View</span><span class="sxs-lookup"><span data-stu-id="cfe4c-262">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|

## <a name="see-also"></a><span data-ttu-id="cfe4c-263">Consulte también</span><span class="sxs-lookup"><span data-stu-id="cfe4c-263">See also</span></span>

* [<span data-ttu-id="cfe4c-264">Directrices de diseño de cuadros de diálogo en la reunión</span><span class="sxs-lookup"><span data-stu-id="cfe4c-264">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [<span data-ttu-id="cfe4c-265">Teams de autenticación para pestañas</span><span class="sxs-lookup"><span data-stu-id="cfe4c-265">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)
* [<span data-ttu-id="cfe4c-266">Aplicaciones para Teams reuniones</span><span class="sxs-lookup"><span data-stu-id="cfe4c-266">Apps for Teams meetings</span></span>](teams-apps-in-meetings.md)

## <a name="next-step"></a><span data-ttu-id="cfe4c-267">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="cfe4c-267">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cfe4c-268">Habilitar y configurar las aplicaciones para Teams reuniones</span><span class="sxs-lookup"><span data-stu-id="cfe4c-268">Enable and configure your apps for Teams meetings</span></span>](enable-and-configure-your-app-for-teams-meetings.md)

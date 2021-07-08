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
# <a name="prerequisites-and-api-references-for-apps-in-teams-meetings"></a>Requisitos previos y referencias de API para las aplicaciones en las reuniones de Teams

Para expandir las capacidades de tus aplicaciones en todo el ciclo de vida de la reunión, Teams te permite trabajar con aplicaciones para Teams reuniones. Debes pasar por los requisitos previos y puedes usar las referencias a la API de aplicaciones de reunión para mejorar la experiencia de la reunión.

## <a name="prerequisites"></a>Requisitos previos

Antes de trabajar con aplicaciones para Teams reuniones, debes comprender lo siguiente:

* Debes tener conocimientos sobre cómo desarrollar Teams aplicaciones. Para obtener más información, [consulta Teams desarrollo de aplicaciones](../overview.md).

* Debes actualizar el manifiesto Teams aplicación para indicar que la aplicación está disponible para reuniones. Para obtener más información, consulta [manifiesto de la aplicación](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest).

* La aplicación debe admitir pestañas configurables en el ámbito groupchat, para que la aplicación funcione en el ciclo de vida de la reunión como pestaña. Para obtener más información, [vea groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) y [build a group tab](../build-your-first-app/build-channel-tab.md).

* Debe cumplir las directrices generales Teams de diseño de pestañas para escenarios previos y posteriores a la reunión. Para obtener experiencias durante las reuniones, consulte las directrices de diseño de la pestaña en la reunión y del cuadro de diálogo en la reunión. Para obtener más información, [vea Teams de](../tabs/design/tabs.md)diseño de pestañas, directrices de diseño de pestañas en la reunión y directrices de diseño de cuadros de diálogo en la [reunión.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)

* Debes admitir el ámbito para habilitar la aplicación en `groupchat` chats previos y posteriores a la reunión. Con la experiencia de la aplicación previa a la reunión, puedes encontrar y agregar aplicaciones de reunión y realizar tareas previas a la reunión. Con la experiencia de la aplicación posterior a la reunión, puedes ver los resultados de la reunión, como los resultados de encuestas o los comentarios.

* Los parámetros de dirección URL de la API de reunión deben `meetingId` `userId` tener , y `tenantId` . Están disponibles como parte de la actividad del SDK Teams cliente y el bot. Además, puede recuperar información confiable para el identificador de usuario y el identificador de inquilino mediante la [autenticación de SSO de tabulación.](../tabs/how-to/authentication/auth-aad-sso.md)

* La `GetParticipant` API debe tener un registro de bot y un identificador para generar tokens de autenticación. Para obtener más información, vea [bot registration and ID](../build-your-first-app/build-bot.md).

* Para que la aplicación se actualice en tiempo real, debe estar actualizada en función de las actividades de eventos de la reunión. Estos eventos pueden estar dentro del cuadro de diálogo en la reunión y otras etapas a lo largo del ciclo de vida de la reunión. Para el cuadro de diálogo en la reunión, vea el parámetro de `bot Id` finalización en `NotificationSignal` la API.

* La API de detalles de la reunión debe tener un registro del bot y un identificador de bot. Requiere bot SDK para obtener `TurnContext` .

* Para eventos de reunión en tiempo real, debe estar familiarizado con el objeto disponible a través `TurnContext` del SDK de bot. El `Activity` objeto en contiene la carga con la hora de inicio y finalización `TurnContext` real. Los eventos de reunión en tiempo real requieren un identificador de bot registrado de Teams plataforma.

Una vez que haya pasado por los requisitos previos, puede usar las referencias de api de aplicaciones de reunión , , y la API de detalles de reunión que le permiten tener acceso a la información mediante atributos y mostrar contenido `GetUserContext` `GetParticipant` `NotificationSignal` relevante.

## <a name="meeting-apps-api-references"></a>Referencias de API de aplicaciones de reunión

Las nuevas extensibilidades de reuniones le proporcionan API que transforman la experiencia de la reunión. Con esta nueva funcionalidad, puedes crear aplicaciones o integrar aplicaciones existentes en el ciclo de vida de la reunión. Puedes usar las API para que la aplicación conozca la reunión. Puede elegir qué API desea usar para mejorar la experiencia de la reunión.

En la tabla siguiente se proporciona una lista de estas API:

|API|Descripción|Solicitud|Origen|
|---|---|----|---|
|**GetUserContext**| Esta API le permite obtener información contextual para mostrar contenido relevante en una Teams pestaña. |_**microsoftTeams.getContext( ( ) => { /*...* / } )**_|Microsoft Teams SDK de cliente|
|**GetParticipant**| Esta API permite que un bot obtenga información de los participantes mediante el identificador de reunión y el identificador de participante. |**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_ |Microsoft Bot Framework SDK|
|**NotificationSignal** | Esta API le permite proporcionar señales de reunión que se entregan mediante la API de notificación de conversación existente para el chat de bots de usuario. Le permite señalar en función de la acción del usuario que muestra un cuadro de diálogo en la reunión. |**POST** _**/v3/conversations/{conversationId}/activities**_|Microsoft Bot Framework SDK|
|**Detalles de la reunión** | Esta API le permite obtener metadatos estáticos de reunión. |**GET** _**/v1/meetings/{meetingId}**_| Bot SDK |

### <a name="getusercontext-api"></a>GetUserContext API

Para identificar y recuperar información contextual para el contenido de la pestaña, vea [Obtener contexto para su Teams pestaña](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library). se usa en una pestaña al ejecutarse en el contexto de la reunión y `meetingId` se agrega para la carga de respuesta.

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
> * No almacenar en caché los roles de los participantes, ya que el organizador de la reunión puede cambiar los roles en cualquier momento.
> * Teams actualmente no admite listas de distribución grandes ni tamaños de lista de más de 350 participantes para la `GetParticipant` API.

La `GetParticipant` API permite que un bot obtenga información de los participantes mediante el identificador de reunión y el identificador de participante. La API incluye parámetros de consulta, ejemplos y códigos de respuesta.

#### <a name="query-parameters"></a>Parámetros de consulta

La `GetParticipant` API incluye los siguientes parámetros de consulta:

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|---|
|**meetingId**| Cadena | Sí | El identificador de reunión está disponible a través de Bot Invoke y Teams CLIENT SDK.|
|**participantId**| Cadena | Sí | El identificador de participante es el identificador de usuario. Está disponible en TAB SSO, Bot Invoke y Teams Client SDK. Se recomienda obtener un identificador de participante del SSO de la pestaña. |
|**tenantId**| Cadena | Sí | El identificador de inquilino es necesario para los usuarios del espacio empresarial. Está disponible en TAB SSO, Bot Invoke y Teams Client SDK. Se recomienda obtener un identificador de inquilino del SSO de la pestaña. |

#### <a name="example"></a>Ejemplo

La `GetParticipant` API incluye los siguientes ejemplos:

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="javascript"></a>[JavaScript](#tab/javascript)

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

# <a name="json"></a>[JSON](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

---

El cuerpo de la respuesta JSON `GetParticipant` para la API es:

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

#### <a name="response-codes"></a>Códigos de respuesta

La `GetParticipant` API devuelve los siguientes códigos de respuesta:

|Código de respuesta|Descripción|
|---|---|
| **403** | La aplicación no puede obtener información de los participantes. Esta es la respuesta de error más común y se desencadena si la aplicación no está instalada en la reunión. Por ejemplo, si la aplicación está deshabilitada por el administrador del espacio empresarial o bloqueada durante la migración del sitio en directo.|
| **200** | La información del participante se recupera correctamente.|
| **401** | La aplicación responde con un token no válido.|
| **404** | La reunión ha expirado o no se encuentra el participante.|

### <a name="notificationsignal-api"></a>NotificationSignal API

Todos los usuarios de una reunión reciben las notificaciones enviadas a través de la `NotificationSignal` API.

> [!NOTE]
> * Cuando se invoca un cuadro de diálogo en la reunión, el contenido se presenta como un mensaje de chat.
> * Actualmente, no se admite el envío de notificaciones dirigidas.

`NotificationSignal` La API le permite proporcionar señales de reunión que se entregan mediante la API de notificación de conversación existente para el chat de bots de usuario. Esta API le permite señalar en función de la acción del usuario que muestra un cuadro de diálogo en la reunión. La API incluye parámetros de consulta, ejemplos y códigos de respuesta.

#### <a name="query-parameter"></a>Parámetro de consulta

La `NotificationSignal` API incluye el siguiente parámetro de consulta:

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|---|
|**conversationId**| Cadena | Sí | El identificador de conversación está disponible como parte de Bot Invoke. |

#### <a name="examples"></a>Ejemplos

Se `Bot ID` declara en el manifiesto y el bot recibe un objeto result.

> [!NOTE]
> * El `completionBotId` parámetro de la es opcional en el ejemplo de carga `externalResourceUrl` solicitada. `Bot ID` se declara en el manifiesto y el bot recibe un objeto result.
> * Los `externalResourceUrl` parámetros de ancho y alto deben estar en píxeles. Para asegurarse de que las dimensiones están dentro de los límites permitidos, vea [directrices de diseño](design/designing-apps-in-meetings.md).
> * La dirección URL es la página cargada como una en el cuadro de diálogo `<iframe>` en la reunión. El dominio debe estar en la matriz de la aplicación `validDomains` en el manifiesto de la aplicación.

La `NotificationSignal` API incluye los siguientes ejemplos:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");
activity.TeamsNotifyUser(true, "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID");
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

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

# <a name="json"></a>[JSON](#tab/json)

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

#### <a name="response-codes"></a>Códigos de respuesta

La `NotificationSignal` API incluye los siguientes códigos de respuesta:

|Código de respuesta|Descripción|
|---|---|
| **201** | La actividad con señal se envía correctamente. |
| **401** | La aplicación responde con un token no válido. |
| **403** | La aplicación no puede enviar la señal. Esto puede ocurrir debido a diversos motivos, como que el administrador de inquilinos deshabilita la aplicación, la aplicación se bloquea durante la migración del sitio en directo, y así sucesivamente. En este caso, la carga contiene un mensaje de error detallado. |
| **404** | El chat de reunión no existe. |

### <a name="meeting-details-api"></a>API de detalles de reunión

> [!NOTE]
> Esta característica está disponible actualmente solo en [la versión preliminar del desarrollador](../resources/dev-preview/developer-preview-intro.md) público.

La API de detalles de la reunión permite a la aplicación obtener metadatos estáticos de la reunión. Estos son puntos de datos que no cambian dinámicamente.
La API está disponible a través de Bot Services.

#### <a name="prerequisite"></a>Requisito previo

Para usar la API de detalles de reunión, debe obtener permisos de RSC. Use el siguiente ejemplo para configurar la propiedad del manifiesto de la `webApplicationInfo` aplicación:

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```
 
#### <a name="query-parameter"></a>Parámetro de consulta

La API de detalles de reunión incluye el siguiente parámetro de consulta:

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|---|
|**meetingId**| Cadena | Sí | El identificador de reunión está disponible a través de Bot Invoke y Teams CLIENT SDK. |

#### <a name="example"></a>Ejemplo

La API de detalles de la reunión incluye los siguientes ejemplos:

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="javascript"></a>[JavaScript](#tab/javascript)

No disponible

# <a name="json"></a>[JSON](#tab/json)

```http
GET /v1/meetings/{meetingId}
```

---

El cuerpo de la respuesta JSON para la API de detalles de reunión es el siguiente:

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

## <a name="real-time-teams-meeting-events"></a>Eventos de reuniones Teams en tiempo real

> [!NOTE]
> Esta característica está disponible actualmente solo en [la versión preliminar del desarrollador](../resources/dev-preview/developer-preview-intro.md) público.

El usuario puede recibir eventos de reunión en tiempo real. Tan pronto como cualquier aplicación está asociada a una reunión, el inicio real de la reunión y la hora de finalización de la reunión se comparten con el bot.

La hora real de inicio y finalización de una reunión es diferente de la hora de inicio y finalización programada. La API de detalles de la reunión proporciona la hora de inicio y finalización programadas, mientras que el evento proporciona la hora real de inicio y finalización.

### <a name="prerequisite"></a>Requisito previo

El manifiesto de la aplicación debe tener la `webApplicationInfo` propiedad para recibir los eventos de inicio y finalización de la reunión. Use el siguiente ejemplo para configurar el manifiesto:

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

### <a name="example-of-meeting-start-event-payload"></a>Ejemplo de carga del evento de inicio de reunión

El código siguiente proporciona un ejemplo de carga del evento de inicio de reunión:

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

### <a name="example-of-meeting-end-event-payload"></a>Ejemplo de carga del evento de fin de reunión

El código siguiente proporciona un ejemplo de carga del evento de fin de reunión:

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

### <a name="example-of-getting-metadata-of-a-meeting"></a>Ejemplo de obtener metadatos de una reunión

El bot recibe el evento a través del `OnEventActivityAsync` controlador.

Para deserializar la carga json, se introduce un objeto de modelo para obtener los metadatos de una reunión. Los metadatos de una reunión residen en la `value` propiedad de la carga del evento. Se `MeetingStartEndEventvalue` crea el objeto model, cuyas variables de miembro corresponden a las claves de la propiedad en la carga del `value` evento.

El código siguiente muestra cómo capturar los metadatos de una reunión que es , , , , y desde un evento de inicio y finalización de `MeetingType` `Title` la `Id` `JoinUrl` `StartTime` `EndTime` reunión:

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

MeetingStartEndEventvalue.cs incluye el código siguiente:

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

## <a name="code-sample"></a>Ejemplo de código

|Nombre de ejemplo | Descripción | .NET | Node.js |
|----------------|-----------------|--------------|--------------|
| Extensibilidad de reuniones | Microsoft Teams extensibilidad de reunión para pasar tokens. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| Bot de burbuja de contenido de reunión | Microsoft Teams de extensibilidad de reuniones para interactuar con el bot de burbujas de contenido en una reunión. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| MeetingSidePanel | Microsoft Teams extensibilidad de reuniones para interactuar con el panel lateral en la reunión. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|
| Ficha Detalles en reunión | Microsoft Teams de extensibilidad de reuniones para iterar con la pestaña Detalles en la reunión. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/nodejs)|

## <a name="see-also"></a>Vea también

* [Directrices de diseño de cuadros de diálogo en la reunión](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teams de autenticación para pestañas](../tabs/how-to/authentication/auth-flow-tab.md)
* [Aplicaciones para Teams reuniones](teams-apps-in-meetings.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Habilitar y configurar las aplicaciones para Teams reuniones](enable-and-configure-your-app-for-teams-meetings.md)

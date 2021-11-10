---
title: Referencias API de aplicaciones de reuniones
author: surbhigupta
description: Identificar referencias de API de aplicaciones de reunión con ejemplos y ejemplos de código
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
keywords: consulta de señal de notificación usercontext de las reuniones de aplicaciones de teams
ms.openlocfilehash: 29e0e797b3b55dd3fa25071929072957c8d43fd8
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/10/2021
ms.locfileid: "60887709"
---
# <a name="meeting-apps-api-references"></a>Referencias API de aplicaciones de reuniones

Las extensibilidades de la reunión proporcionan API para transformar la experiencia de la reunión:

* Cree aplicaciones o integre aplicaciones existentes en el ciclo de vida de la reunión.
* Usa las API para que la aplicación conozca la reunión.
* Seleccione las API que desea usar para mejorar la experiencia de reunión.

En la tabla siguiente se proporciona una lista de API:

|API|Descripción|Solicitud|Origen|
|---|---|----|---|
|**GetUserContext**| Esta API le permite obtener información contextual para mostrar contenido relevante en una Teams pestaña. |_**microsoftTeams.getContext( ( ) => { /*...* / } )**_|Microsoft Teams SDK de cliente|
|**GetParticipant**| Esta API permite que un bot obtenga información de los participantes mediante el identificador de reunión y el identificador de participante. |**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_ |Microsoft Bot Framework SDK|
|**NotificationSignal** | Esta API le permite proporcionar señales de reunión que se entregan mediante la API de notificación de conversación existente para el chat de bots de usuario. Le permite señalar en función de la acción del usuario que muestra un cuadro de diálogo en la reunión. |**POST** _**/v3/conversations/{conversationId}/activities**_|Microsoft Bot Framework SDK|
|**Detalles de la reunión** | Esta API le permite obtener metadatos estáticos de reunión. |**GET** _**/v1/meetings/{meetingId}**_| Bot SDK |

En la tabla siguiente se proporcionan los métodos del SDK de Bot Framework para las API:

|API|Bot Framework SDK (método)|
|---|---|
|**GetParticipant**| `GetMeetingParticipantAsync (Microsoft.Bot.Builder.ITurnContext turnContext, string meetingId = default, string participantId = default, string tenantId = default, System.Threading.CancellationToken cancellationToken = default);` |
|**NotificationSignal** | `activity.TeamsNotifyUser(true, "https://teams.microsoft.com/l/bubble/APP_ID?url=&height=&width=&title=<title>&completionBotId=BOT_APP_ID");` |
|**Detalles de la reunión** | `TeamsMeetingInfo (string id = default);` |

## <a name="getusercontext-api"></a>GetUserContext API

Para identificar y recuperar información contextual para el contenido de la pestaña, vea [Obtener contexto para su Teams pestaña](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library). se usa en una pestaña al ejecutarse en el contexto de la reunión y `meetingId` se agrega para la carga de respuesta.

## <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
> * No almacenar en caché los roles de los participantes, ya que el organizador de la reunión puede cambiar los roles en cualquier momento.
> * Teams actualmente no admite listas de distribución grandes ni tamaños de lista de más de 350 participantes para la `GetParticipant` API.

La `GetParticipant` API permite que un bot obtenga información de los participantes mediante el identificador de reunión y el identificador de participante. La API incluye parámetros de consulta, ejemplos y códigos de respuesta.

### <a name="query-parameters"></a>Parámetros de consulta

La `GetParticipant` API incluye los siguientes parámetros de consulta:

|Valor|Tipo|Necesario|Descripción|
|---|---|----|---|
|**meetingId**| Cadena | Sí | El identificador de reunión está disponible a través de Bot Invoke y Teams CLIENT SDK.|
|**participantId**| Cadena | Sí | El identificador de participante es el identificador de usuario. Está disponible en TAB SSO, Bot Invoke y Teams Client SDK. Se recomienda obtener un identificador de participante del SSO de la pestaña. |
|**tenantId**| String | Sí | El identificador de inquilino es necesario para los usuarios del espacio empresarial. Está disponible en TAB SSO, Bot Invoke y Teams Client SDK. Se recomienda obtener un identificador de inquilino del SSO de la pestaña. | 

### <a name="example"></a>Ejemplo

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

### <a name="response-codes"></a>Códigos de respuesta

La `GetParticipant` API devuelve los siguientes códigos de respuesta:

|Código de respuesta|Descripción|
|---|---|
| **403** | Obtener información de participante no se comparte con la aplicación. Si la aplicación no está instalada en la reunión, desencadena la respuesta de error 403 más común. Si el administrador del espacio empresarial deshabilita o bloquea la aplicación durante la migración del sitio en directo, se desencadena la respuesta de error 403. |
| **200** | La información del participante se recupera correctamente.|
| **401** | La aplicación responde con un token no válido.|
| **404** | La reunión ha expirado o no se encuentra el participante.|

## <a name="notificationsignal-api"></a>NotificationSignal API

Todos los usuarios de una reunión reciben las notificaciones enviadas a través de la `NotificationSignal` API.

> [!NOTE]
> * Cuando se invoca un cuadro de diálogo en la reunión, el contenido se presenta como un mensaje de chat.
> * Actualmente, no se admite el envío de notificaciones dirigidas.

`NotificationSignal` La API le permite proporcionar señales de reunión que se entregan mediante la API de notificación de conversación existente para el chat de bots de usuario. Esta API le permite señalar en función de la acción del usuario que muestra un cuadro de diálogo en la reunión. La API incluye parámetros de consulta, ejemplos y códigos de respuesta.

### <a name="query-parameter"></a>Parámetro de consulta

La `NotificationSignal` API incluye el siguiente parámetro de consulta:

|Valor|Tipo|Necesario|Descripción|
|---|---|----|---|
|**conversationId**| String | Sí | El identificador de conversación está disponible como parte de Bot Invoke. |

### <a name="examples"></a>Ejemplos

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

### <a name="response-codes"></a>Códigos de respuesta

La `NotificationSignal` API incluye los siguientes códigos de respuesta:

|Código de respuesta|Descripción|
|---|---|
| **201** | La actividad con señal se envía correctamente. |
| **401** | La aplicación responde con un token no válido. |
| **403** | La aplicación no puede enviar la señal. El código de respuesta 403 puede producirse debido a diversos motivos, como que el administrador de inquilinos deshabilita y bloquea la aplicación durante la migración de sitios en directo. En este caso, la carga contiene un mensaje de error detallado. |
| **404** | El chat de reunión no existe. |

## <a name="meeting-details-api"></a>API de detalles de reunión

> [!NOTE]
> Esta característica está disponible actualmente solo en [la versión preliminar del desarrollador](../resources/dev-preview/developer-preview-intro.md) público.

La API de detalles de la reunión permite a la aplicación obtener metadatos estáticos de la reunión. Los metadatos proporcionan puntos de datos que no cambian dinámicamente.
La API está disponible a través de Bot Services.

### <a name="prerequisite"></a>Requisito previo

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
 
### <a name="query-parameter"></a>Parámetro de consulta

La API de detalles de reunión incluye el siguiente parámetro de consulta:

|Valor|Tipo|Necesario|Descripción|
|---|---|----|---|
|**meetingId**| Cadena | Sí | El identificador de reunión está disponible a través de Bot Invoke y Teams CLIENT SDK. |

### <a name="example"></a>Ejemplo

La API de detalles de la reunión incluye los siguientes ejemplos:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
MeetingInfo result = await TeamsInfo.GetMeetingInfoAsync(turnContext);
await turnContext.SendActivityAsync(JsonConvert.SerializeObject(result));
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

El usuario puede recibir eventos de reunión en tiempo real. Tan pronto como cualquier aplicación está asociada a una reunión, la hora real de inicio y finalización de la reunión se comparten con el bot.

La hora real de inicio y finalización de una reunión es diferente de la hora de inicio y finalización programadas. La API de detalles de la reunión proporciona la hora de inicio y finalización programadas. El evento proporciona la hora de inicio y finalización reales.

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
        "Id": "meeting id", 
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

Para deserializar la carga json, se introduce un objeto de modelo para obtener los metadatos de una reunión. Los metadatos de una reunión se encuentra en la `value` propiedad de la carga del evento. Se `MeetingStartEndEventvalue` crea el objeto model, cuyas variables de miembro corresponden a las claves de la propiedad en la carga del `value` evento.
     
> [!NOTE]      
> * Obtener el identificador de reunión de `turnContext.ChannelData` .    
> * No use el identificador de conversación como identificador de reunión.     
> * No use el identificador de reunión de la carga de eventos de reunión `turncontext.activity.value` . 
      
El código siguiente muestra cómo capturar los metadatos de una reunión que es , , , , y desde un evento de inicio y finalización de `MeetingType` `Title` la `Id` `JoinUrl` `StartTime` `EndTime` reunión:

Evento Inicio de reunión
```csharp
protected override async Task OnTeamsMeetingStartAsync(MeetingEndEventDetails meeting, ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    await turnContext.SendActivityAsync(JsonConvert.SerializeObject(meeting));
}
```

Evento de fin de reunión
```csharp
protected override async Task OnTeamsMeetingEndAsync(MeetingEndEventDetails meeting, ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    await turnContext.SendActivityAsync(JsonConvert.SerializeObject(meeting));
}
```

## <a name="code-sample"></a>Ejemplo de código

|Ejemplo de nombre | Descripción | C# | Node.js | 
|----------------|-----------------|--------------|--------------|
| Extensibilidad de reuniones | Microsoft Teams extensibilidad de reunión para pasar tokens. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| Bot de burbuja de contenido de reunión | Microsoft Teams de extensibilidad de reuniones para interactuar con el bot de burbujas de contenido en una reunión. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| MeetingSidePanel | Microsoft Teams extensibilidad de reuniones para interactuar con el panel lateral en la reunión. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|
| Ficha Detalles en reunión | Microsoft Teams extensibilidad de reuniones para interactuar con la pestaña Detalles en la reunión. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/nodejs)|
|Ejemplo de eventos de reunión|Aplicación de ejemplo para mostrar eventos de reunión Teams en tiempo real|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/nodejs)|
|Ejemplo de contratación de reuniones|Aplicación de ejemplo para mostrar la experiencia de reunión para el escenario de contratación.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/nodejs)|
|Instalación de aplicaciones con código QR|Aplicación de ejemplo que genera el código QR e instala la aplicación con el código QR|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/csharp)|[Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/nodejs)|

## <a name="see-also"></a>Consulte también

* [Teams de autenticación para pestañas](../tabs/how-to/authentication/auth-flow-tab.md)
* [Aplicaciones para Teams reuniones](teams-apps-in-meetings.md)

## <a name="next-steps"></a>Siguientes pasos

> [!div class="nextstepaction"]
> [Habilitar y configurar las aplicaciones para Teams reuniones](enable-and-configure-your-app-for-teams-meetings.md)
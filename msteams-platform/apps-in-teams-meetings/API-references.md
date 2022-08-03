---
title: Referencias API de aplicaciones de reuniones
author: surbhigupta
description: Aprenda a identificar las referencias de api de aplicaciones de reunión con ejemplos y ejemplos de código, consultas de señal de notificación de contexto de usuario de las reuniones de las aplicaciones de Teams.
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
ms.date: 04/07/2022
ms.openlocfilehash: 20a0380bb6e8282f9ced47621b17b1633d09e28b
ms.sourcegitcommit: 990a36fb774e614146444d4adaa2c9bcdb835998
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2022
ms.locfileid: "67232263"
---
# <a name="meeting-apps-api-references"></a>Referencias API de aplicaciones de reuniones

La extensibilidad de la reunión proporciona API para mejorar la experiencia de reunión. Puede realizar lo siguiente con la ayuda de las API enumeradas:

* Cree aplicaciones o integre aplicaciones existentes dentro del ciclo de vida de las reuniones.
* Use las API para que la aplicación sea consciente de la reunión.
* Seleccione las API necesarias para mejorar la experiencia de reunión.

> [!NOTE]
> Use Teams [SDK de JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) (*versión*: 1.10 y posteriores) para que SSO funcione en el panel lateral de la reunión.

En la tabla siguiente se proporciona una lista de las API disponibles en los SDK de cliente de Microsoft Teams (MSTC) y Microsoft Bot Framework (MSBF):

|Método| Descripción| Origen|
|---|---|----|
|[**Obtener el contexto de usuario**](#get-user-context-api)| Obtenga información contextual para mostrar el contenido pertinente en una pestaña de Microsoft Teams.| [MSTC SDK](/microsoftteams/platform/tabs/how-to/access-teams-context#get-context-by-using-the-microsoft-teams-javascript-library) |
|[**Obtener participante**](#get-participant-api)| Capture la información de los participantes por id. de reunión e id. de participante. | [MSBF SDK](/dotnet/api/microsoft.bot.builder.teams.teamsinfo.getmeetingparticipantasync?view=botbuilder-dotnet-stable&preserve-view=true)
|[**Enviar notificación en la reunión**](#send-an-in-meeting-notification)| Proporciona señales de reunión utilizando la API de notificación de conversación existente para el chat de usuario-bot y permite notificar la acción del usuario que muestra una notificación en la reunión. | [MSBF SDK](/dotnet/api/microsoft.bot.builder.teams.teamsactivityextensions.teamsnotifyuser?view=botbuilder-dotnet-stable&preserve-view=true) |
|[**Obtener detalles de la reunión**](#get-meeting-details-api)| Obtener los metadatos estáticos de una reunión. | [MSBF SDK](/dotnet/api/microsoft.bot.builder.teams.teamsinfo.getmeetinginfoasync?view=botbuilder-dotnet-stable&preserve-view=true) |
|[**Enviar subtítulos en tiempo real**](#send-real-time-captions-api)| Enviar subtítulos en tiempo real a una reunión en curso. | [MSTC SDK](/azure/cognitive-services/speech-service/speech-sdk?tabs=nodejs%2Cubuntu%2Cios-xcode%2Cmac-xcode%2Candroid-studio#get-the-speech-sdk&preserve-view=true) |
|[**Compartir contenido de la aplicación en la fase**](#share-app-content-to-stage-api)| Comparta partes específicas de la aplicación en la fase de reunión desde el panel lateral de la aplicación en una reunión. | [MSTC SDK](/javascript/api/@microsoft/teams-js/meeting) |
|[**Obtener el estado de uso compartido del contenido de la aplicación**](#get-app-content-stage-sharing-state-api)| Obtenga información sobre el estado de uso compartido de la aplicación en la fase de reunión. | [MSTC SDK](/javascript/api/@microsoft/teams-js/meeting.iappcontentstagesharingstate) |
|[**Obtener funcionalidades de uso compartido de la fase de contenido de la aplicación**](#get-app-content-stage-sharing-capabilities-api)| Capture las capacidades de la aplicación para compartir en la fase de reunión. | [MSTC SDK](/javascript/api/@microsoft/teams-js/meeting.iappcontentstagesharingcapabilities) |
|[**Obtener eventos de reunión de Teams en tiempo real**](#get-real-time-teams-meeting-events-api)|Capturar eventos de reunión en tiempo real, como la hora de inicio y finalización real.| [MSBF SDK](/dotnet/api/microsoft.bot.builder.teams.teamsactivityhandler.onteamsmeetingstartasync?view=botbuilder-dotnet-stable&preserve-view=true) |
| [**Obtener altavoz de audio entrante**](#get-incoming-audio-speaker) | Permite que una aplicación obtenga la configuración del altavoz de audio entrante para el usuario de la reunión.| [MSTC SDK](/javascript/api/@microsoft/teams-js/microsoftteams.meeting?view=msteams-client-js-latest&preserve-view=true) |
| [**Alternar audio entrante**](#toggle-incoming-audio) | Permite que una aplicación alterne la configuración del altavoz de audio entrante para el usuario de la reunión de silenciar a unmute o viceversa.| [MSTC SDK](/javascript/api/@microsoft/teams-js/microsoftteams.meeting?view=msteams-client-js-latest&preserve-view=true) |

## <a name="get-user-context-api"></a>Obtener API de contexto de usuario

Para identificar y recuperar información contextual del contenido de la pestaña, vea [obtener contexto para la pestaña de Teams](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library). `meetingId` se usa en una pestaña que se ejecuta en el contexto de la reunión y se agrega para la carga de respuesta.

## <a name="get-participant-api"></a>Obtener API de participante

La API de `GetParticipant` debe tener un identificador y un registro de bot para generar tokens de autenticación. Para obtener más información, consulte [el registro del bot y el identificador](../build-your-first-app/build-bot.md).

> [!NOTE]
>
> * No almacene en caché los roles de participante, ya que el organizador de la reunión puede cambiar los roles en cualquier momento.
> * Actualmente, la `GetParticipant` API solo se admite para listas de distribuciones o listas con menos de 350 participantes.

### <a name="query-parameters"></a>Parámetros de consulta

> [!TIP]
> Obtenga los identificadores de participante y los identificadores de inquilino de la [pestaña autenticación SSO](../tabs/how-to/authentication/tab-sso-overview.md).

La `Meeting` API debe tener `meetingId`, `participantId`y `tenantId` como parámetros de dirección URL. Los parámetros están disponibles como parte del SDK de cliente de Teams y la actividad del bot.

En la tabla siguiente se incluyen los parámetros de consulta:

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|---|
|**Id. de la reunión**| Cadena | Sí | El identificador de reunión está disponible a través de Bot Invoke y el SDK de cliente de Teams.|
|**Id. del participante**| Cadena | Sí | El id. de participante es el identificador de usuario. Está disponible en la pestaña SSO, Bot Invoke y Cliente SDK de Teams. Se recomienda obtener un ID de participante en la pestaña SSO. |
|**tenantId**| Cadena | Sí | El identificador de inquilino es necesario para los usuarios del inquilino. Está disponible en la pestaña SSO, Bot Invoke y Cliente SDK de Teams. Se recomienda obtener un identificador de inquilino desde la pestaña SSO. |

### <a name="example"></a>Ejemplo

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
      "conversationType": "groupChat", 
      "isGroup":true
   }
}
```

---

| Nombre de propiedad | Descripción |
|---|---|
| **user.id** | Identificador del usuario. |
| **user.aadObjectId** | Identificador de objeto de Azure Active Directory del usuario. |
| **user.name** | Nombre del usuario. |
| **user.givenName** | Nombre del usuario.|
| **user.surname** | Apellidos del usuario. |
| **user.email** | Id. de correo del usuario. |
| **user.userPrincipalName** | UPN del usuario. |
| **user.tenantId** | Identificador del inquilino de Azure Active Directory |
| **user.userRole** | Rol del usuario. Por ejemplo, "admin" o "user". |
| **meeting.role** | El rol del participante en la reunión. Por ejemplo, "Organizer" o "Presenter" o "Attendee". |
| **meeting.inMeeting** | Valor que indica si el participante está en la reunión. |
| **conversation.id** | Identificador de chat de reunión. |
| **conversation.isGroup** | Boolean que indica si la conversación tiene más de dos participantes. |

### <a name="response-codes"></a>Códigos de respuesta

En la tabla siguiente se proporcionan los códigos de respuesta:

|Código de respuesta|Descripción|
|---|---|
| **403** | La obtención de información de participantes no se comparte con la aplicación. Si la aplicación no está instalada en la reunión, desencadena la respuesta de error 403. Si el administrador de inquilinos deshabilita o bloquea la aplicación durante la migración del sitio activo, desencadena la respuesta de error 403. |
| **200** | La información del participante se recupera correctamente.|
| **401** | La aplicación responde con un token no válido.|
| **404** | La reunión ha expirado o los participantes no están disponibles.|

## <a name="send-an-in-meeting-notification"></a>Enviar una notificación en la reunión

Todos los usuarios de una reunión reciben las notificaciones enviadas a través de la carga de notificación en la reunión. La carga de notificación en la reunión desencadena una notificación en la reunión y le permite proporcionar señales de reunión que se entregan mediante la API de notificación de conversación existente para el chat de bot de usuario. Puede enviar una notificación en la reunión en función de la acción del usuario. La carga está disponible a través de Bot Services.

> [!NOTE]
>
> * Cuando se invoca una notificación en la reunión, el contenido se presenta como un mensaje de chat.
> * Actualmente, no se admite el envío de notificaciones dirigidas ni la compatibilidad con la aplicación web.
> * Debe invocar la función [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submit-the-result-of-a-task-module) para descartarla automáticamente después de que un usuario realice una acción en la vista web. Este es un requisito para el envío de aplicaciones. Para obtener más información, vea [módulo de tareas del SDK de Teams](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).
> * Si desea que la aplicación admita usuarios anónimos, la carga de solicitud de invocación inicial debe basarse en `from.id` metadatos de solicitud en `from` objeto, no `from.aadObjectId` metadatos de solicitud. `from.id` es el identificador de usuario y `from.aadObjectId` es el identificador de Microsoft Azure Active Directory (Azure AD) del usuario. Para obtener más información, vea [usar módulos de tareas en pestañas](../task-modules-and-cards/task-modules/task-modules-tabs.md) y [crear y enviar el módulo de tareas](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).

### <a name="query-parameter"></a>Parámetro de consulta

En la tabla siguiente se incluye el parámetro de consulta:

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|---|
|**conversationId**| Cadena | Sí | El identificador de conversación está disponible como parte de Bot Invoke. |

### <a name="examples"></a>Ejemplos

El `Bot ID` se declara en el manifiesto y el bot recibe un objeto de resultado.

> [!NOTE]
>
> * El `completionBotId` parámetro de `externalResourceUrl` es opcional en el ejemplo de carga solicitada.
> * Los `externalResourceUrl` parámetros de ancho y alto deben estar en píxeles. Para obtener más información, vea [instrucciones de diseño](design/designing-apps-in-meetings.md).
> * La dirección URL es la página, que se carga como `<iframe>` en la notificación en la reunión. El dominio debe estar en la matriz `validDomains` de las aplicaciones en el manifiesto de la aplicación.

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
```

```json

{
    "type": "message",
    "text": "John Phillips assigned you a weekly todo",
    "summary": "Don't forget to meet with Marketing next week",
    "channelData": {
        "notification": {
            "alertInMeeting": true,
            "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&<completionBotId>=<BOT_APP_ID>"
        }
    },
    "replyToId": "1493070356924"
}
```

---

| Nombre de propiedad | Descripción |
|---|---|
| **type** | Tipo de actividad. |
| **text** | Contenido de texto del mensaje. |
| **summary** | Texto de resumen del mensaje. |
| **channelData.notification.alertInMeeting** | Boolean que indica si se va a mostrar una notificación al usuario durante una reunión. |
| **channelData.notification.externalResourceUrl** | Valor de la dirección URL del recurso externo de la notificación.|
| **replyToId** | Identificador del mensaje primario o raíz del subproceso. |
| **APP_ID** | Id. de aplicación declarado en manifiesto. |
| **completionBotId** | Id. de aplicación de bot |

### <a name="response-codes"></a>Códigos de respuesta

En la tabla siguiente se incluyen los códigos de respuesta:

|Código de respuesta|Descripción|
|---|---|
| **201** | La actividad con señal se ha enviado correctamente. |
| **401** | La aplicación responde con un token no válido. |
| **403** | La aplicación no puede enviar la señal. El código de respuesta 403 puede producirse debido a varias razones, como que el administrador de inquilinos deshabilite y bloquee la aplicación durante la migración del sitio en vivo. En este caso, la carga contiene un mensaje de error detallado. |
| **404** | El chat de la reunión no existe. |

## <a name="get-meeting-details-api"></a>Api de obtención de detalles de la reunión

La API de detalles de la reunión permite a la aplicación obtener los metadatos estáticos de una reunión. Los metadatos proporcionan puntos de datos que no cambian dinámicamente. La API está disponible a través de Bot Services. Actualmente, las reuniones privadas programadas o periódicas y las reuniones programadas o periódicas de canal admiten la API con diferentes permisos de RSC, respectivamente.

La `Meeting Details` API debe tener un registro de bot y un identificador de bot. Requiere bot SDK para obtener `TurnContext`. Para usar la API Detalles de la reunión, debe obtener distintos permisos RSC en función del ámbito de cualquier reunión, como una reunión privada o una reunión de canal.

### <a name="prerequisite"></a>Requisito previo

Para usar la API Detalles de la reunión, debe obtener distintos permisos RSC en función del ámbito de cualquier reunión, como una reunión privada o una reunión de canal.

<br>

<details>

<summary><b>Para la versión 1.12 y posteriores del manifiesto de la aplicación</b></summary>

Utilice el siguiente ejemplo para configurar los manifiestos `webApplicationInfo` y `authorization`  propiedades de su aplicación para cualquier reunión privada:

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
},
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "OnlineMeeting.ReadBasic.Chat",
                "type": "Application"
            }
        ]
    }
}
 ```

Utilice el siguiente ejemplo para configurar los manifiestos `webApplicationInfo` y `authorization` propiedades de su aplicación para cualquier reunión de canal:

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
},
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "ChannelMeeting.ReadBasic.Group",
                "type": "Application"
            }
        ]
    }
}
 ```

<br>

</details>

<br>

<details>

<summary><b>Para la versión 1.11 del manifiesto de la aplicación y versiones anteriores</b></summary>

Use el ejemplo siguiente para configurar la propiedad `webApplicationInfo` del manifiesto de la aplicación para cualquier reunión privada:

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

Use el ejemplo siguiente para configurar la propiedad `webApplicationInfo` del manifiesto de la aplicación para cualquier reunión de canal:

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "ChannelMeeting.ReadBasic.Group"
    ]
}
 ```

<br>

</details>

> [!NOTE]
>
> * El bot puede recibir automáticamente eventos de inicio o finalización de reuniones de todas las reuniones creadas en todos los canales agregando `ChannelMeeting.ReadBasic.Group` al manifiesto para el permiso RSC.
>
> * Para una llamada `organizer` uno a uno es el iniciador del chat y para las llamadas grupales `organizer` es el iniciador de llamadas.

### <a name="query-parameter"></a>Parámetro de consulta

En la tabla siguiente se muestra el parámetro de consulta:

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|---|
|**Id. de la reunión**| Cadena | Sí | El identificador de reunión está disponible a través de Bot Invoke y el SDK de cliente de Teams. |

### <a name="example"></a>Ejemplo

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
MeetingInfo result = await TeamsInfo.GetMeetingInfoAsync(turnContext);
await turnContext.SendActivityAsync(JsonConvert.SerializeObject(result));
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript

Not available

```

# <a name="json"></a>[JSON](#tab/json)

```http
GET /v1/meetings/{meetingId}
```

El cuerpo de la respuesta JSON para la API de Detalles de la Reunión es el siguiente:

* **Reuniones programadas:**

    ```json

    {
       "details":  { 
             "id": "<meeting ID>", 
             "msGraphResourceId": "MSowYmQ0M2I4OS1lN2QxLTQxNzAtOGZhYi00OWJjYjkwOTk1YWYqMCoqMTk6bWVldGluZ19OVEkyT0RjM01qUXROV1UyW", 
             "scheduledStartTime": "2022-04-24T22:00:00Z", 
             "scheduledEndTime": "2022-04-24T23:00:00Z", 
             "joinUrl": "https://teams.microsoft.com/l/xx", 
             "title": "All Hands", 
             "type": "Scheduled" 
         },
        "conversation": { 
             "isGroup": true, 
             "conversationType": "groupChat", 
             "id": "meeting chat ID" 
             }, 
        "organizer": { 
             "id": "<organizer user ID>", 
             "aadObjectId": "<AAD object ID>",
             "objectId": "<organizer object ID>",
             "tenantId": "<Tenant ID>" 
         }
    } 
    ```

* **Llamadas uno a uno:**

    ```json
    {
        "details": {
             "id": "<meeting ID>",
             "type": "OneToOneCall"
         },
        "conversation": {
             "isGroup": true,
             "conversationType": "groupChat",
             "id": "meeting chat ID"
         },
        "organizer  ": {
             "id": "<organizer user ID>",
             "aadObjectId": "<AAD object ID>",
             "objectId": "<organizer object ID>",
             "tenantId": "<Tenant ID>" 
         }
    }
    
    ```

* **Llamadas de grupo:**

    ```json
    {
        "details": {
             "id": "<meeting ID>",
             "type": "GroupCall",
             "joinUrl": "https://teams.microsoft.com/l/xx"
         },
        "conversation": {
             "isGroup": true,
             "conversationType": "groupChat",
             "id": "meeting chat ID"
         },
        "organizer": {
             "id": "<organizer user ID>",
             "objectId": "<organizer object ID>",
             "aadObjectId": "<AAD object ID>",
             "tenantId": "<Tenant ID>" 
         }
    }
    
    ```

* **Reuniones instantáneas:**

    ```json
    { 
       "details": { 
             "id": "<meeting ID>", 
             "msGraphResourceId": "MSowYmQ0M2I4OS1lN2QxLTQxNzAtOGZhYi00OWJjYjkwOTk1YWYqMCoqMTk6bWVldGluZ19OVEkyT0RjM01qUXROV1UyW", 
             "scheduledStartTime": "2022-04-24T22:00:00Z", 
             "scheduledEndTime": "2022-04-24T23:00:00Z", 
             "joinUrl": "https://teams.microsoft.com/l/xx", 
             "title": "All Hands", 
             "type": "MeetNow" 
         }, 
        "conversation": { 
             "isGroup": true, 
             "conversationType": "groupChat", 
             "id": "meeting chat ID" 
         },
        "organizer": { 
             "id": "<organizer user ID>", 
             "aadObjectId": "<AAD object ID>", 
             "tenantId": "<Tenant ID>" ,
             "objectId": "<organizer object ID>"
         }
    }
    
    ```

---

| Nombre de propiedad | Descripción |
|---|---|
| **details.id** | Identificador de la reunión, codificado como una cadena BASE64. |
| **details.msGraphResourceId** | MsGraphResourceId, que se usa específicamente para llamadas de Graph API de MS. |
| **details.scheduledStartTime** | Hora de inicio programada de la reunión, en UTC. |
| **details.scheduledEndTime** | Hora de finalización programada de la reunión, en UTC. |
| **details.joinUrl** | Dirección URL usada para unirse a la reunión. |
| **details.title** | El título de la reunión. |
| **details.type** | Tipo de reunión (GroupCall, OneToOneCall, Adhoc, Broadcast, MeetNow, Recurring, Scheduled o Unknown). |
| **conversation.isGroup** | Boolean que indica si la conversación tiene más de dos participantes. |
| **conversation.conversationType** | Tipo de conversación. |
| **conversation.id** | Identificador de chat de reunión. |
| **organizer.id** | Identificador de usuario del organizador. |
| **organizer.aadObjectId** | Identificador de objeto de Azure Active Directory del organizador. |
| **organizer.tenantId** | Identificador de inquilino de Azure Active Directory del organizador. |

En el caso del tipo de reunión Periódica,

**startDate**: especifica la fecha para empezar a aplicar el patrón. El valor de startDate debe corresponder al valor de fecha de la propiedad start en el recurso de evento. Tenga en cuenta que es posible que la primera aparición de la reunión no se produzca en esta fecha si no se ajusta al patrón.

**endDate**: especifica la fecha para dejar de aplicar el patrón. Tenga en cuenta que es posible que la última aparición de la reunión no se produzca en esta fecha si no se ajusta al patrón.

## <a name="send-real-time-captions-api"></a>Enviar API de subtítulos en tiempo real

La API de envío de subtítulos en tiempo real expone un punto de conexión POST para los subtítulos de traducción en tiempo real (CART) de acceso a la comunicación de Teams, subtítulos con tipo humano. El contenido de texto enviado a este punto de conexión aparece para los usuarios finales en una reunión de Teams cuando tienen subtítulos habilitados.

### <a name="cart-url"></a>DIRECCIÓN URL CART

Puede obtener la dirección URL de CART para el punto de conexión POST en la página **Opciones de reunión** de una reunión de Teams. Para obtener más información, vea [subtítulos CART en una reunión de Microsoft Teams](https://support.microsoft.com/office/use-cart-captions-in-a-microsoft-teams-meeting-human-generated-captions-2dd889e8-32a8-4582-98b8-6c96cf14eb47). No es necesario modificar la dirección URL de CART para usar subtítulos CART.

#### <a name="query-parameter"></a>Parámetro de consulta

La dirección URL de CART incluye los siguientes parámetros de consulta:

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|----|
|**Id. de la reunión**| Cadena | Sí |El identificador de reunión está disponible a través de Bot Invoke y el SDK de cliente de Teams. <br/>Por ejemplo, meetingid=%7b%22tId%22%3a%2272f234bf-86f1-41af-91ab-2d7cd0321b47%22%2c%22oId%22%3a%22e071f268-4241-47f8-8cf3-fc6b84437f23%22%2c%22thId%22%3a%2219%3ameeting_NzJiMjNkMGQtYzk3NS00ZDI1LWJjN2QtMDgyODVhZmI3NzJj%40thread.v2%22%2c%22mId%22%3a%220%22%7d|
|**token**| Cadena | Sí |Token de autorización.<br/> Por ejemplo, token=04751eac |

#### <a name="example"></a>Ejemplo

```http
https://api.captions.office.microsoft.com/cartcaption?meetingid=%7b%22tId%22%3a%2272f234bf-86f1-41af-91ab-2d7cd0321b47%22%2c%22oId%22%3a%22e071f268-4241-47f8-8cf3-fc6b84437f23%22%2c%22thId%22%3a%2219%3ameeting_NzJiMjNkMGQtYzk3NS00ZDI1LWJjN2QtMDgyODVhZmI3NzJj%40thread.v2%22%2c%22mId%22%3a%220%22%7d&token=gjs44ra
```

### <a name="method"></a>Método

|Resource|Método|Descripción|
|----|----|----|
|/cartcaption|POST|Controlar los subtítulos de la reunión, que se inició|

> [!NOTE]
> Asegúrese de que el tipo de contenido de todas las solicitudes es texto sin formato con codificación UTF-8. El cuerpo de la solicitud solo contiene subtítulos.

#### <a name="example"></a>Ejemplo

```http
POST /cartcaption?meetingid=04751eac-30e6-47d9-9c3f-0b4ebe8e30d9&token=04751eac&lang=en-us HTTP/1.1
Host: api.captions.office.microsoft.com
Content-Type: text/plain
Content-Length: 22
Hello I’m Cortana, welcome to my meeting. 
```

> [!Note]  
> Cada solicitud POST genera una nueva línea de títulos. Para asegurarse de que el usuario final tiene tiempo suficiente para leer el contenido, limite cada cuerpo de la solicitud POST a 80-120 caracteres.

### <a name="error-codes"></a>Códigos de error

En la tabla siguiente se proporcionan los códigos de error:

|Código de error|Descripción|
|---|---|
| **400** | Solicitud incorrecta. El cuerpo de la respuesta tiene más información. Por ejemplo, no de todos los parámetros necesarios presentados.|
| **401** | No autorizado. Token incorrecto o expirado. Si recibe este error, genere una nueva dirección URL de CART en Teams. |
| **404** | Reunión no encontrada o no iniciada. Si recibe este error, asegúrese de iniciar la reunión y seleccione Iniciar subtítulos. Después de habilitar los subtítulos en la reunión, puede empezar a colocar subtítulos en la reunión.|
| **500** |Error interno del servidor. Para obtener más información, [póngase en contacto con el soporte técnico o proporcione comentarios](../feedback.md).|

## <a name="share-app-content-to-stage-api"></a>Compartir contenido de la aplicación para API de fase

La `shareAppContentToStage` API le permite compartir partes específicas de la aplicación en la fase de reunión. La API está disponible a través del SDK de cliente de Teams.

### <a name="prerequisite"></a>Requisito previo

* Para usar la `shareAppContentToStage` API, debe obtener los permisos de RSC. En el manifiesto de la aplicación, configure la propiedad `authorization` y la `name` y `type` en el campo`resourceSpecific`. Por ejemplo:

    ```json
    "authorization": {
        "permissions": { 
        "resourceSpecific": [
        { 
        "name": "MeetingStage.Write.Chat",
        "type": "Delegated"
        }
        ]
    }
    }
    ```

* `appContentUrl` debe estar permitido por la `validDomains` matriz dentro de manifest.json, de lo contrario la API devolvería 501.

### <a name="query-parameter"></a>Parámetro de consulta

En la tabla siguiente se incluyen los parámetros de consulta:

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|---|
|**callback**| Cadena | Sí | La devolución de llamada contiene dos parámetros, error y resultado. El *error* puede contener un error de tipo *SdkError* o NULL cuando el recurso compartido se realiza correctamente. El *resultado* puede contener un valor verdadero, en caso de un recurso compartido correcto, o NULL cuando se produce un error en el recurso compartido.|
|**appContentURL**| Cadena | Sí | Dirección URL que se compartirá en la fase.|

### <a name="example"></a>Ejemplo

```javascript
const appContentUrl = "https://www.bing.com/";

microsoftTeams.meeting.shareAppContentToStage((err, result) => {
    if (result) {
        // handle success
    }
    if (err) {
        // handle error
    }
}, appContentUrl);
```

### <a name="response-codes"></a>Códigos de respuesta

En la tabla siguiente se proporcionan los códigos de respuesta:

|Código de respuesta|Descripción|
|---|---|
| **500** | Error interno. |
| **501** | La API no se admite en el contexto actual.|
| **1 000** | La aplicación no tiene los permisos adecuados para permitir que el recurso compartido se almacene en fase.|

## <a name="get-app-content-stage-sharing-state-api"></a>Obtención de la API de estado de uso compartido de la fase de contenido de la aplicación

La `getAppContentStageSharingState` API le permite capturar información sobre el uso compartido de aplicaciones en la fase de reunión.

### <a name="query-parameter"></a>Parámetro de consulta

En la tabla siguiente se incluye el parámetro de consulta:

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|---|
|**callback**| Cadena | Sí | La devolución de llamada contiene dos parámetros, error y resultado. El *error* puede contener un error de tipo *SdkError*, en caso de error, o NULL cuando el recurso compartido se realiza correctamente. El *resultado* puede contener un objeto `AppContentStageSharingState`, lo que indica una recuperación correcta, o nulo, que indica un error de recuperación.|

### <a name="example"></a>Ejemplo

```javascript
microsoftTeams.meeting.getAppContentStageSharingState((err, result) => {
    if (result.isAppSharing) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
```

El cuerpo de la respuesta JSON para la API de `getAppContentStageSharingState` es:

```json
{
   "isAppSharing":true
} 
```

### <a name="response-codes"></a>Códigos de respuesta

En la tabla siguiente se proporcionan los códigos de respuesta:

|Código de respuesta|Descripción|
|---|---|
| **500** | Error interno. |
| **501** | La API no se admite en el contexto actual.|
| **1 000** | La aplicación no tiene los permisos adecuados para permitir que el recurso compartido se almacene en fase.|

## <a name="get-app-content-stage-sharing-capabilities-api"></a>API de obtención de funcionalidades de uso compartido de la fase de contenido de la aplicación

La `getAppContentStageSharingCapabilities` API le permite capturar las funcionalidades de la aplicación para compartir en la fase de reunión.

### <a name="query-parameter"></a>Parámetro de consulta

En la tabla siguiente se incluye el parámetro de consulta:

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|---|
|**callback**| Cadena | Sí | La devolución de llamada contiene dos parámetros, error y resultado. El *error* puede contener un error de tipo *SdkError* o NULL cuando el recurso compartido se realiza correctamente. El resultado puede contener un `AppContentStageSharingState` objeto, que indica una recuperación correcta, o nulo, que indica que se ha producido un error en la recuperación.|

### <a name="example"></a>Ejemplo

```javascript
microsoftTeams.meeting.getAppContentStageSharingCapabilities((err, result) => {
    if (result.doesAppHaveSharePermission) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
```

El cuerpo de respuesta JSON para `getAppContentStageSharingCapabilities` API es:

```json
{
   "doesAppHaveSharePermission":true
} 
```

### <a name="response-codes"></a>Códigos de respuesta

En la tabla siguiente se proporcionan los códigos de respuesta:

|Código de respuesta|Descripción|
|---|---|
| **500** | Error interno. |
| **1000** | La aplicación no tiene permisos para permitir que el recurso compartido se almacene provisionalmente.|

## <a name="get-real-time-teams-meeting-events-api"></a>Obtener API de eventos de reunión de Teams en tiempo real

> [!NOTE]
> Los eventos de reunión de Teams en tiempo real solo se admiten para las reuniones programadas.

El usuario puede recibir eventos de reunión en tiempo real. En cuanto una aplicación se asocia a una reunión, la hora real de inicio y fin de la misma se comparte con el bot. La hora de inicio y finalización real de una reunión es diferente de la hora de inicio y finalización programada. La API de detalles de la reunión proporciona la hora de inicio y finalización programada. El evento proporciona la hora de inicio y finalización real.

Debe estar familiarizado con el objeto `TurnContext` disponible a través de Bot SDK. El `Activity` objeto de `TurnContext` contiene la carga útil con la hora de inicio y finalización reales. Los eventos de reunión en tiempo real requieren un identificador de bot registrado de la plataforma Teams. El bot puede recibir automáticamente el evento de inicio o finalización de la reunión agregando `ChannelMeeting.ReadBasic.Group` en el manifiesto.

### <a name="prerequisite"></a>Requisito previo

El manifiesto de la aplicación debe tener la propiedad `webApplicationInfo` para recibir los eventos de inicio y finalización de la reunión. Use los ejemplos siguientes para configurar el manifiesto:

<br>

<details>

<summary><b>Para la versión 1.12 y posteriores del manifiesto de la aplicación</b></summary>

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    },
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "OnlineMeeting.ReadBasic.Chat",
                "type": "Application"
            }
        ]    
    }
}
 ```

<br>

</details>

<br>

<details>

<summary><b>Para la versión 1.11 del manifiesto de la aplicación y versiones anteriores</b></summary>

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

<br>

</details>

### <a name="example-of-getting-meetingstartendeventvalue"></a>Ejemplo de obtención `MeetingStartEndEventvalue`

El bot recibe el evento a través del controlador de `OnEventActivityAsync`. Para deserializar la carga JSON, se introduce un objeto de modelo para obtener los metadatos de una reunión. Los metadatos de una reunión están en la propiedad `value` de la carga del evento. Se crea el objeto de modelo `MeetingStartEndEventvalue`, cuyas variables miembro corresponden a las claves de la propiedad `value` en la carga del evento.

> [!NOTE]
>
> * Obtener id. de reunión de `turnContext.ChannelData`.
> * No use el identificador de conversación como id. de reunión.
> * No use el id. de reunión de la carga de eventos de reunión `turncontext.activity.value`.

En el código siguiente se muestra cómo capturar los metadatos de una reunión `MeetingType`, `Title`, `Id`, `JoinUrl`, `StartTime`, y `EndTime` de un evento de inicio y finalización de la reunión:

Evento de inicio de reunión

```csharp
protected override async Task OnTeamsMeetingStartAsync(MeetingStartEventDetails meeting, ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
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

### <a name="example-of-meeting-end-event-payload"></a>Ejemplo de carga del evento de finalización de la reunión

El código siguiente proporciona un ejemplo de carga del evento de finalización de la reunión:

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

| Nombre de propiedad | Descripción |
|---|---|
| **name** | Nombre del usuario.|
| **type** | Tipo de actividad. |
| **timestamp** | Fecha y hora locales del mensaje, expresados en formato ISO-8601. |
| **id** | Identificador de la actividad. |
| **channelId** | Canalizar con el que está asociada esta actividad. |
| **serviceUrl** | Dirección URL del servicio donde se deben enviar respuestas a esta actividad. |
| **from.id** | Id. del usuario que envió la solicitud. |
| **from.aadObjectId** | Id de objeto Azure Active Directory identificador del usuario que envió la solicitud. |
| **conversation.isGroup** | Boolean que indica si la conversación tiene más de dos participantes. |
| **conversation.tenantId** | Identificador de inquilino de Azure Active Directory de la conversación o reunión. |
| **conversation.id** | Identificador de chat de reunión. |
| **recipient.id** | Identificador del usuario que recibe la solicitud. |
| **recipient.name** | Nombre del usuario que recibe la solicitud. |
| **entities.locale** | entidad que contiene metadatos sobre la configuración regional. |
| **entities.country** | entidad que contiene metadatos sobre el país. |
| **entities.type** | entidad que contiene metadatos sobre el cliente. |
| **channelData.tenant.id** | Identificador del inquilino de Azure Active Directory |
| **channelData.source** | Nombre de origen desde el que se desencadena o se invoca el evento. |
| **channelData.meeting.id** | Identificador predeterminado asociado a la reunión. |
| **valor. MeetingType** | Tipo de reunión. |
| **valor. Título** | El tema de la reunión. |
| **valor. Identificación** | Identificador predeterminado asociado a la reunión. |
| **valor. JoinUrl** | Dirección URL de unión de la reunión. |
| **valor. StartTime** | Hora de inicio de la reunión en UTC. |
| **valor. EndTime** | Hora de finalización de la reunión en UTC. |
| **locale**| Configuración regional del mensaje establecido por el cliente. |

## <a name="get-incoming-audio-speaker"></a>Obtener altavoz de audio entrante

La `getIncomingClientAudioState` API permite a una aplicación obtener la configuración de altavoz de audio entrante para el usuario de la reunión. La API está disponible a través del SDK de cliente de Teams.

> [!NOTE]
> Actualmente, la `getIncomingClientAudioState` API para dispositivos móviles solo está disponible en [versión preliminar para desarrolladores públicos](../resources/dev-preview/developer-preview-intro.md).

### <a name="query-parameter"></a>Parámetro de consulta

En la tabla siguiente se incluye el parámetro de consulta:

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|---|
|**callback**| Cadena | Sí | La devolución de llamada contiene dos parámetros `error` y `result`. El *error* puede contener un tipo `SdkError` de error o `null` cuando la captura de audio se realiza correctamente. El *resultado* puede contener un valor true o false cuando la captura de audio es correcta o null cuando se produce un error en la captura de audio. El audio entrante se silencia si el resultado es true y no semuta si el resultado es false. |

### <a name="example"></a>Ejemplo

```typescript
function getIncomingClientAudioState(
    callback: (error: SdkError | null, result: boolean | null) => void,
  ): void {
    if (!callback) {
      throw new Error('[get incoming client audio state] Callback cannot be null');
    }
    ensureInitialized(FrameContexts.sidePanel, FrameContexts.meetingStage);
    sendMessageToParent('getIncomingClientAudioState', callback);
  }

```

### <a name="response-codes"></a>Códigos de respuesta

En la tabla siguiente se proporcionan los códigos de respuesta:

|Código de respuesta|Descripción|
|---|---|
| **500** | Error interno. |
| **501** | La API no se admite en el contexto actual.|
| **1 000** | La aplicación no tiene los permisos adecuados para permitir que el recurso compartido se almacene en fase.|

## <a name="toggle-incoming-audio"></a>Alternar audio entrante

La `toggleIncomingClientAudio` API permite que una aplicación alterne la configuración del altavoz de audio entrante para el usuario de la reunión de silenciar a unmute o viceversa. La API está disponible a través del SDK de cliente de Teams.

> [!NOTE]
> Actualmente, la `toggleIncomingClientAudio` API para dispositivos móviles solo está disponible en [versión preliminar para desarrolladores públicos](../resources/dev-preview/developer-preview-intro.md).

### <a name="query-parameter"></a>Parámetro de consulta

En la tabla siguiente se incluye el parámetro de consulta:

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|---|
|**callback**| Cadena | Sí | La devolución de llamada contiene dos parámetros `error` y `result`. El *error* puede contener un tipo `SdkError` de error o `null` cuando el botón de alternancia se realiza correctamente. El *resultado* puede contener un valor true o false, cuando el botón de alternancia es correcto o null cuando se produce un error en la alternancia. El audio entrante se silencia si el resultado es true y no semuta si el resultado es false. |

### <a name="example"></a>Ejemplo:

```typescript
function toggleIncomingClientAudio(callback: (error: SdkError | null, result: boolean | null) => void): void {
    if (!callback) {
      throw new Error('[toggle incoming client audio] Callback cannot be null');
    }
    ensureInitialized(FrameContexts.sidePanel, FrameContexts.meetingStage);
    sendMessageToParent('toggleIncomingClientAudio', callback);
  }

```

### <a name="response-code"></a>Código de respuesta

En la tabla siguiente se proporcionan los códigos de respuesta:

|Código de respuesta|Descripción|
|---|---|
| **500** | Error interno. |
| **501** | La API no se admite en el contexto actual.|
| **1 000** | La aplicación no tiene los permisos adecuados para permitir que el recurso compartido se almacene en fase.|

## <a name="code-sample"></a>Ejemplo de código

|Ejemplo de nombre | Descripción | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| Extensibilidad de reuniones | Ejemplo de extensibilidad de reuniones de Teams para pasar tokens. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| Bot de burbuja de contenido de reunión | Ejemplo de extensibilidad de reuniones de Teams para interactuar con el bot de burbujas de contenido en una reunión. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| MeetingSidePanel de la reunión | Ejemplo de extensibilidad de reuniones de Teams para interactuar con el panel lateral en la reunión. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|
| Pestaña Detalles de la reunión | Ejemplo de extensibilidad de reuniones de Teams para interactuar con la pestaña Detalles en la reunión. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/nodejs)|
|Ejemplo de eventos de reunión|Aplicación de ejemplo para mostrar eventos de reunión de Teams en tiempo real|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/nodejs)|
|Muestra de contratación de reuniones|Ejemplo de aplicación para mostrar la experiencia de la reunión para el escenario de la contratación.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/nodejs)|
|Instalación de la aplicación con código QR|Aplicación de ejemplo que genera el código QR e instala la aplicación con el código QR|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/csharp)|[Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/nodejs)|

## <a name="see-also"></a>Consulte también

* [Flujo de autenticación de Teams para pestañas](../tabs/how-to/authentication/auth-flow-tab.md)
* [Aplicaciones para reuniones de Teams](teams-apps-in-meetings.md)
* [SDK de Live Share](teams-live-share-overview.md)

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Habilitar y configurar las aplicaciones para reuniones de Teams](enable-and-configure-your-app-for-teams-meetings.md)

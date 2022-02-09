---
title: Referencias API de aplicaciones de reuniones
author: surbhigupta
description: Identificar las referencias de api de aplicaciones de reunión con ejemplos y ejemplos de código
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
keywords: consulta de señal de notificación de contexto de usuario de las reuniones de aplicaciones de teams
ms.openlocfilehash: 681929c85d23f83ffa6742afdae2860ac8dfc356
ms.sourcegitcommit: f5c2090fdd5b55d21ecd9c395423fa277e18d74a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2022
ms.locfileid: "62470791"
---
# <a name="meeting-apps-api-references"></a>Referencias API de aplicaciones de reuniones

La extensibilidad de la reunión proporciona API para mejorar la experiencia de la reunión. Puede realizar lo siguiente con la ayuda de las API enumeradas:

* Cree aplicaciones o integre aplicaciones existentes en el ciclo de vida de la reunión.
* Usa las API para que tu aplicación tenga en cuenta la reunión.
* Seleccione las API necesarias para mejorar la experiencia de la reunión.

En la tabla siguiente se proporciona una lista de API disponibles en los SDK de cliente de Microsoft Teams (MSTC) y Microsoft Bot Framework (MSBF):

|Método| Descripción| Origen|
|---|---|----|
|[**Obtener contexto de usuario**](#get-user-context-api)| Obtenga información contextual para mostrar contenido relevante en una Teams pestaña.| MSTC SDK|
|[**Obtener participante**](#get-participant-api)| Obtenga información del participante por identificador de reunión e identificador de participante. |MSBF SDK|
|[**Enviar señal de notificación**](#send-notification-signal-api)| Proporcione señales de reunión mediante la API de notificación de conversación existente para el chat de bots de usuario y permite notificar a la acción del usuario que muestra un cuadro de diálogo en la reunión. |MSBF SDK|
|[**Obtener detalles de la reunión**](#get-meeting-details-api)| Obtener los metadatos estáticos de una reunión. |MSBF SDK |
|[**Enviar títulos en tiempo real**](#send-real-time-captions-api)| Enviar títulos en tiempo real a una reunión en curso. |MSTC SDK|
|[**Compartir contenido de la aplicación en fase**](#share-app-content-to-stage-api)| Compartir partes específicas de la aplicación a la fase de reunión desde el panel lateral de la aplicación en una reunión. |MSTC SDK|
|[**Obtener el estado de uso compartido de la fase de contenido de la aplicación**](#get-app-content-stage-sharing-state-api)| Obtenga información sobre el estado de uso compartido de la aplicación en la fase de reunión. |MSTC SDK|
|[**Obtener capacidades de uso compartido de fases de contenido de la aplicación**](#get-app-content-stage-sharing-capabilities-api)| Recupera las capacidades de la aplicación para compartir en la fase de reunión. |MSTC SDK|
|[**Obtener eventos de reunión Teams en tiempo real**](#get-real-time-teams-meeting-events-api)|Capturar eventos de reunión en tiempo real, como la hora de inicio y finalización reales.| MSBF SDK|

## <a name="get-user-context-api"></a>Obtener API de contexto de usuario

Para identificar y recuperar información contextual para el contenido de la pestaña, vea Obtener contexto para la pestaña [Teams](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library). `meetingId` Se usa en una pestaña que se ejecuta en el contexto de la reunión y se agrega para la carga de respuesta.

## <a name="get-participant-api"></a>Obtener API de participantes

> [!NOTE]
> * No almacenar en caché los roles de los participantes, ya que el organizador de la reunión puede cambiar los roles en cualquier momento.
> * Actualmente, la `GetParticipant` API solo es compatible con listas de distribuciones o listas con menos de 350 participantes.

### <a name="query-parameters"></a>Parámetros de consulta

> [!TIP]
> Obtenga los identificadores de participantes y los identificadores de inquilino del SSO de la pestaña.

En la tabla siguiente se incluyen los parámetros de consulta:

|Valor|Tipo|Obligatorio|Description|
|---|---|----|---|
|**meetingId**| Cadena | Sí | El identificador de reunión está disponible a través de Bot Invoke y Teams CLIENT SDK.|
|**participantId**| Cadena | Sí | El identificador de participante es el identificador de usuario. Está disponible en TAB SSO, Bot Invoke y Teams Client SDK. Se recomienda obtener un identificador de participante del SSO de la pestaña. |
|**tenantId**| String | Sí | El identificador de inquilino es necesario para los usuarios del espacio empresarial. Está disponible en TAB SSO, Bot Invoke y Teams Client SDK. Se recomienda obtener un identificador de inquilino del SSO de la pestaña. |

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

---

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

En la tabla siguiente se proporcionan los códigos de respuesta:

|Código de respuesta|Description|
|---|---|
| **403** | Obtener información de participante no se comparte con la aplicación. Si la aplicación no está instalada en la reunión, desencadena la respuesta de error 403. Si el administrador del espacio empresarial deshabilita o bloquea la aplicación durante la migración del sitio en directo, desencadena la respuesta de error 403. |
| **200** | La información del participante se recupera correctamente.|
| **401** | La aplicación responde con un token no válido.|
| **404** | La reunión ha expirado o los participantes no están disponibles.|

## <a name="send-notification-signal-api"></a>ENVIAR API de señal de notificación

Todos los usuarios de una reunión reciben las notificaciones enviadas a través de la `NotificationSignal` API. `NotificationSignal` La API le permite proporcionar señales de reunión que se entregan mediante la API de notificación de conversación existente para el chat de bots de usuario. Puede enviar una señal en función de la acción del usuario, un cuadro de diálogo en la reunión. La API incluye parámetros de consulta, ejemplos y códigos de respuesta.

> [!NOTE]
> * Cuando se invoca un cuadro de diálogo en la reunión, el contenido se presenta como un mensaje de chat.
> * Actualmente, no se admite el envío de notificaciones dirigidas.

### <a name="query-parameter"></a>Parámetro de consulta

En la tabla siguiente se incluyen los parámetros de consulta:

|Valor|Tipo|Obligatorio|Description|
|---|---|----|---|
|**conversationId**| Cadena | Sí | El identificador de conversación está disponible como parte de Bot Invoke. |

### <a name="examples"></a>Ejemplos

Se `Bot ID` declara en el manifiesto y el bot recibe un objeto result.

> [!NOTE]
> * El `completionBotId` parámetro de la es `externalResourceUrl` opcional en el ejemplo de carga solicitada.
> * Los `externalResourceUrl` parámetros de ancho y alto deben estar en píxeles. Para obtener más información, consulte [Directrices de diseño](design/designing-apps-in-meetings.md).
> * La dirección URL es la página, que se carga como `<iframe>` en el cuadro de diálogo en la reunión. El dominio debe estar en la matriz de aplicaciones `validDomains` en el manifiesto de la aplicación.

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

En la tabla siguiente se incluyen los códigos de respuesta:

|Código de respuesta|Description|
|---|---|
| **201** | La actividad con señal se envía correctamente. |
| **401** | La aplicación responde con un token no válido. |
| **403** | La aplicación no puede enviar la señal. El código de respuesta 403 puede producirse debido a diversos motivos, como que el administrador de inquilinos deshabilita y bloquea la aplicación durante la migración de sitios en directo. En este caso, la carga contiene un mensaje de error detallado. |
| **404** | El chat de reunión no existe. |

## <a name="get-meeting-details-api"></a>Obtener la API de detalles de la reunión

> [!NOTE]
> Actualmente, la característica solo está disponible en [la versión preliminar del desarrollador](../resources/dev-preview/developer-preview-intro.md) público.

La API de detalles de la reunión permite a la aplicación obtener los metadatos estáticos de una reunión. Los metadatos proporcionan puntos de datos que no cambian dinámicamente. La API está disponible a través de Bot Services. Actualmente, las reuniones privadas programadas o periódicas y las reuniones programadas o periódicas de canal admiten API con diferentes permisos RSC respectivamente.

### <a name="prerequisite"></a>Requisito previo

Para usar la API de detalles de reunión, debe obtener distintos permisos de RSC en función del ámbito de cualquier reunión, como reunión privada o reunión de canal.

<br>

<details>

<summary><b>Para el manifiesto de la aplicación versión 1.12</b></summary>

Use el siguiente ejemplo para configurar las propiedades y el manifiesto de la aplicación `webApplicationInfo` `authorization` para cualquier reunión privada:

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

Use el siguiente ejemplo para configurar las propiedades y el manifiesto de la aplicación `webApplicationInfo` `authorization` para cualquier reunión de canal:

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

<summary><b>Para el manifiesto de la aplicación versión 1.11 o anterior</b></summary>

Use el siguiente ejemplo para configurar la propiedad del manifiesto de la aplicación `webApplicationInfo` para cualquier reunión privada:

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

Use el siguiente ejemplo para configurar la propiedad del manifiesto de la aplicación `webApplicationInfo` para cualquier reunión de canal:

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
> El bot puede recibir eventos de inicio o finalización de reunión automáticamente de todas las reuniones creadas en todos los canales `ChannelMeeting.ReadBasic.Group` agregando un manifiesto para el permiso RSC.
 
### <a name="query-parameter"></a>Parámetro de consulta

En la tabla siguiente se muestra el parámetro de consulta:

|Valor|Tipo|Necesario|Description|
|---|---|----|---|
|**meetingId**| Cadena | Sí | El identificador de reunión está disponible a través de Bot Invoke y Teams CLIENT SDK. |

### <a name="example"></a>Ejemplo

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
            "conversationType": "groupchat", 
            "id": "meeting chat ID" 
    }, 
    "organizer": { 
        "id": "<organizer user ID>", 
        "aadObjectId": "<AAD ID>", 
        "tenantId": "<Tenant ID>" 
    }
} 
```

## <a name="send-real-time-captions-api"></a>Enviar API de subtítulos en tiempo real

La API de envío de títulos en tiempo real expone un punto de conexión POST para Microsoft Teams de traducción en tiempo real (CART), títulos cerrados con tipo humano. El contenido de texto enviado a este punto de conexión aparece para los usuarios finales en una reunión Microsoft Teams cuando tienen títulos habilitados.

### <a name="cart-url"></a>DIRECCIÓN URL DEL CARRO

Puede obtener la dirección URL del CARRO para el extremo POST desde la **página Opciones de** reunión en una Microsoft Teams reunión. Para obtener más información, vea [Títulos cart en una Microsoft Teams reunión](https://support.microsoft.com/office/use-cart-captions-in-a-microsoft-teams-meeting-human-generated-captions-2dd889e8-32a8-4582-98b8-6c96cf14eb47). No es necesario modificar la dirección URL del CARRO para usar los títulos CART.

#### <a name="query-parameter"></a>Parámetro Query

La dirección URL de CART incluye los siguientes parámetros de consulta:

|Valor|Tipo|Obligatorio|Description|
|---|---|----|----|
|**meetingId**| Cadena | Sí |El identificador de reunión está disponible a través de Bot Invoke y Teams CLIENT SDK. <br/>Por ejemplo, meetingid=%7b%22tId%22%3a%2272f234bf-86f1-41af-91ab-2d7cd0321b47%22%2c%22oId%22%3a%22e071f268-42441-47f8-8cf3-fc6b84437f23%22%2c%22thId%22%3a%2219%3ameeting_NzJiMjNkMGQtYzk3NS00ZDI1LWJjN2QtMDgyODVhZmI3NzJj%40thread.v2%22%2c%22mId%22%3a%220%22%7d|
|**token**| Cadena | Sí |Token de autorización.<br/> Por ejemplo, token=04751eac |

#### <a name="example"></a>Ejemplo

```http
https://api.captions.office.microsoft.com/cartcaption?meetingid=%7b%22tId%22%3a%2272f234bf-86f1-41af-91ab-2d7cd0321b47%22%2c%22oId%22%3a%22e071f268-4241-47f8-8cf3-fc6b84437f23%22%2c%22thId%22%3a%2219%3ameeting_NzJiMjNkMGQtYzk3NS00ZDI1LWJjN2QtMDgyODVhZmI3NzJj%40thread.v2%22%2c%22mId%22%3a%220%22%7d&token=gjs44ra
```

### <a name="method"></a>Method

|Recurso|Método|Descripción|
|----|----|----|
|/cartcaption|POST|Controlar los títulos de la reunión, que se inició|

> [!NOTE]
> Asegúrese de que el tipo de contenido de todas las solicitudes es texto sin formato con codificación UTF-8. El cuerpo de la solicitud solo contiene títulos.

#### <a name="example"></a>Ejemplo

```http
POST /cartcaption?meetingid=04751eac-30e6-47d9-9c3f-0b4ebe8e30d9&token=04751eac&lang=en-us HTTP/1.1
Host: api.captions.office.microsoft.com
Content-Type: text/plain
Content-Length: 22
Hello I’m Cortana, welcome to my meeting. 
```

> [!Note]  
> Cada solicitud POST genera una nueva línea de títulos. Para asegurarse de que el usuario final tiene suficiente tiempo para leer el contenido, limite cada cuerpo de solicitud POST a 80-120 caracteres.

### <a name="error-codes"></a>Códigos de error

En la tabla siguiente se proporcionan los códigos de error:

|Código de error|Descripción|
|---|---|
| **400** | Solicitud mala. El cuerpo de la respuesta tiene más información. Por ejemplo, no se presentan todos los parámetros necesarios.|
| **401** | No autorizado. Token mal o expirado. Si recibe este error, genere una nueva dirección URL de CART en Teams. |
| **404** | Reunión no encontrada o no iniciada. Si recibe este error, asegúrese de iniciar la reunión y seleccionar los títulos de inicio. Después de habilitar los títulos en la reunión, puede empezar a crear títulos de posting en la reunión.|
| **500** |Error interno del servidor. Para obtener más información, [póngase en contacto con el soporte técnico o proporcione comentarios](../feedback.md).|

## <a name="share-app-content-to-stage-api"></a>Compartir contenido de la aplicación para la API de fase

La `shareAppContentToStage` API te permite compartir partes específicas de la aplicación en la fase de reunión. La API está disponible a través del SDK Teams cliente.

### <a name="prerequisite"></a>Requisito previo

Para usar la `shareAppContentToStage` API, debe obtener los permisos de RSC. En el manifiesto de la aplicación, configure la `authorization` propiedad y y `type` `name` en el `resourceSpecific` campo. Por ejemplo:

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

### <a name="query-parameter"></a>Parámetro de consulta

En la tabla siguiente se incluyen los parámetros de consulta:

|Valor|Tipo|Necesario|Description|
|---|---|----|---|
|**callback**| Cadena | Sí | La devolución de llamada contiene dos parámetros, error y resultado. El *error* puede contener un error de tipo *SdkError* o null cuando el recurso compartido se realiza correctamente. El *resultado* puede contener un valor true, en caso de un recurso compartido correcto, o null cuando se produce un error en el recurso compartido.|
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

|Código de respuesta|Description|
|---|---|
| **500** | Error interno. |
| **501** | La API no se admite en el contexto actual.|
| **1000** | La aplicación no tiene permisos adecuados para permitir el uso compartido en fase.|

## <a name="get-app-content-stage-sharing-state-api"></a>Obtener api de estado de uso compartido de fase de contenido de la aplicación

La `getAppContentStageSharingState` API te permite obtener información sobre el uso compartido de aplicaciones en la fase de reunión.

### <a name="query-parameter"></a>Parámetro de consulta

En la tabla siguiente se incluyen los parámetros de consulta:

|Valor|Tipo|Necesario|Description|
|---|---|----|---|
|**callback**| Cadena | Sí | La devolución de llamada contiene dos parámetros, error y resultado. El *error* puede contener un error de tipo *SdkError*, en caso de error, o null cuando el recurso compartido se realiza correctamente. El *resultado* puede contener un objeto `AppContentStageSharingState` , que indica una recuperación correcta, o null, que indica un error de recuperación.|

### <a name="example"></a>Ejemplo

```javascript
microsoftTeams.meeting.getAppContentStageSharingState((err, result) => {
    if (result.isAppSharing) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
``` 

El cuerpo de la respuesta JSON para la `getAppContentStageSharingState` API es:

```json
{
   "isAppSharing":true
} 
```

### <a name="response-codes"></a>Códigos de respuesta

En la tabla siguiente se proporcionan los códigos de respuesta:

|Código de respuesta|Description|
|---|---|
| **500** | Error interno. |
| **501** | La API no se admite en el contexto actual.|
| **1000** | La aplicación no tiene permisos adecuados para permitir el uso compartido en fase.|

## <a name="get-app-content-stage-sharing-capabilities-api"></a>Obtener API de funcionalidades de uso compartido de fase de contenido de la aplicación

La `getAppContentStageSharingCapabilities` API te permite capturar las capacidades de la aplicación para compartir en la fase de reunión.

### <a name="query-parameter"></a>Parámetro de consulta

En la tabla siguiente se incluyen los parámetros de consulta:

|Valor|Tipo|Necesario|Description|
|---|---|----|---|
|**callback**| Cadena | Sí | La devolución de llamada contiene dos parámetros, error y resultado. El *error* puede contener un error de tipo *SdkError* o null cuando el recurso compartido se realiza correctamente. El resultado puede contener un objeto `AppContentStageSharingState` , que indica una recuperación correcta, o null, que indica un error de recuperación.|

### <a name="example"></a>Ejemplo

```javascript
microsoftTeams.meeting.getAppContentStageSharingCapabilities((err, result) => {
    if (result.doesAppHaveSharePermission) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
``` 

El cuerpo de la respuesta JSON para `getAppContentStageSharingCapabilities` la API es:

```json
{
   "doesAppHaveSharePermission":true
} 
```

### <a name="response-codes"></a>Códigos de respuesta

En la tabla siguiente se proporcionan los códigos de respuesta:

|Código de respuesta|Description|
|---|---|
| **500** | Error interno. |
| **1000** | La aplicación no tiene permisos para permitir el uso compartido en fase.|

## <a name="get-real-time-teams-meeting-events-api"></a>Obtener API de eventos de Teams en tiempo real

El usuario puede recibir eventos de reunión en tiempo real. Tan pronto como cualquier aplicación está asociada a una reunión, la hora real de inicio y finalización de la reunión se comparten con el bot. La hora real de inicio y finalización de una reunión es diferente de la hora de inicio y finalización programadas. La API de detalles de la reunión proporciona la hora de inicio y finalización programadas. El evento proporciona la hora de inicio y finalización reales.

### <a name="prerequisite"></a>Requisito previo

El manifiesto de la aplicación debe tener la `webApplicationInfo` propiedad para recibir los eventos de inicio y finalización de la reunión. Use los siguientes ejemplos para configurar el manifiesto:

<br>

<details>

<summary><b>Para el manifiesto de la aplicación versión 1.12</b></summary>

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

<summary><b>Para el manifiesto de la aplicación versión 1.11 o anterior</b></summary>

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

El bot recibe un evento a través del `OnEventActivityAsync` controlador. Para deserializar la carga JSON, se introduce un objeto de modelo para obtener los metadatos de una reunión. Los metadatos de una reunión se encuentra en la `value` propiedad de la carga del evento. Se `MeetingStartEndEventvalue` crea el objeto model, cuyas variables de miembro corresponden a las claves de la `value` propiedad en la carga del evento.

> [!NOTE]
> * Obtener el identificador de reunión de `turnContext.ChannelData`.
> * No use el identificador de conversación como identificador de reunión.
> * No use el identificador de reunión de la carga de eventos de reunión `turncontext.activity.value`.

El código siguiente muestra cómo capturar los `MeetingType`metadatos de una reunión que es , `Title`, `Id`, `JoinUrl`, y `StartTime``EndTime` desde un evento de inicio y finalización de la reunión:

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
* [Aplicaciones para reuniones de Teams](teams-apps-in-meetings.md)

## <a name="next-steps"></a>Siguientes pasos

> [!div class="nextstepaction"]
> [Habilitar y configurar las aplicaciones para Teams reuniones](enable-and-configure-your-app-for-teams-meetings.md)

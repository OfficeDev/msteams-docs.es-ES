---
title: Crear aplicaciones para reuniones de equipos
author: laujan
description: crear aplicaciones para reuniones de equipos
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: equipos aplicaciones reuniones usuario participante rol api
ms.openlocfilehash: 84d0f5564d7e8e6e34dde1f3d59cc6e7a68d3332
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565917"
---
# <a name="create-apps-for-teams-meetings"></a>Crear aplicaciones para reuniones de Teams

## <a name="prerequisites-and-considerations"></a>Requisitos previos y consideraciones

Antes de crear aplicaciones para reuniones Teams, debe tener una comprensión de lo siguiente:

* Debe tener conocimiento de cómo desarrollar aplicaciones Teams. Para obtener más información, consulte [Teams desarrollo de aplicaciones.](../overview.md)

* Debe actualizar el manifiesto de Teams aplicación para indicar que la aplicación está disponible para reuniones. Para obtener más información, consulte [manifiesto de aplicación](#update-your-app-manifest).

* Para que la aplicación funcione en el ciclo de vida de la reunión como una pestaña, debe admitir pestañas configurables en el ámbito de groupchat. Para obtener más información, vea [ámbito de groupchat](../resources/schema/manifest-schema.md#configurabletabs) y [cree una pestaña de grupo.](../build-your-first-app/build-channel-tab.md)

* Debe cumplir con las directrices generales de diseño de pestañas Teams para escenarios previos y posteriores a la reunión. Para obtener experiencias durante las reuniones, consulte la pestaña en la reunión y las directrices de diseño del cuadro de diálogo en la reunión. Para obtener más información, consulte [directrices de diseño de pestañas Teams,](../tabs/design/tabs.md)directrices de diseño de [pestañas en la reunión](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) y directrices de diseño de cuadro de diálogo en [reunión.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)

* Debes admitir el `groupchat` ámbito para habilitar la aplicación en chats previos a la reunión y después de la reunión. Con la experiencia de la aplicación previa a la reunión, puede encontrar y agregar aplicaciones de reunión y realizar tareas previas a la reunión. Con la experiencia de la aplicación posterior a la reunión, puede ver los resultados de la reunión, como los resultados de la encuesta de encuestas o los comentarios.

* Los parámetros de url de la API de reunión deben tener `meetingId` `userId` , y `tenantId` . Estos están disponibles como parte de la actividad de Teams SDK y bot de cliente. Además, se puede recuperar información confiable para el ID de usuario y el identificador de inquilino mediante [la autenticación de SSO de tabulación.](../tabs/how-to/authentication/auth-aad-sso.md)

* La `GetParticipant` API debe tener un registro de bots y un identificador para generar tokens de autenticación. Para obtener más información, consulte [registro e ID de bot.](../build-your-first-app/build-bot.md)

* Para que la aplicación se actualice en tiempo real, debe estar actualizada en función de las actividades de eventos de la reunión. Estos eventos pueden estar dentro del cuadro de diálogo en la reunión y otras etapas a lo largo del ciclo de vida de la reunión. Para el cuadro de diálogo en la reunión, vea parámetro de finalización `bot Id` en `Notification Signal API` .

## <a name="meeting-apps-api-reference"></a>Referencia api de aplicaciones de reunión

|API|Descripción|Solicitud|Origen|
|---|---|----|---|
|**GetUserContext**| Esta API le permite obtener información contextual para mostrar contenido relevante en una pestaña de Teams. |_**microsoftTeams.getContext( ( ) => { /*...* / } )**_|MICROSOFT TEAMS SDK de cliente|
|**ObtenerParticipant**| Esta API permite a un bot obtener información de los participantes mediante el ID de reunión y el ID de participante. |**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_ |Microsoft Bot Framework SDK|
|**NotificationSignal** | Esta API le permite proporcionar señales de reunión que se entregan mediante la API de notificación de conversación existente para el chat de bot de usuario. Le permite realizar una señal basada en la acción del usuario que muestra un cuadro de diálogo en la reunión. |**POST** _**/v3/conversaciones/{conversationId}/actividades**_|Microsoft Bot Framework SDK|

### <a name="getusercontext"></a>GetUserContext

Para identificar y recuperar información contextual para el contenido de la pestaña, consulte [obtener contexto para la pestaña Teams](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). `meetingId`se utiliza mediante una pestaña cuando se ejecuta en el contexto de reunión y se agrega para la carga de respuesta.

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
> * No almacene en caché los roles de participante, ya que el organizador de la reunión puede cambiar un rol en cualquier momento.
> * Teams actualmente no admite grandes listas de distribución o tamaños de lista de más de 350 participantes para la `GetParticipant` API.

#### <a name="query-parameters"></a>Parámetros de consulta

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|---|
|**meetingId**| string | Sí | El identificador de reunión está disponible a través de Bot Invoke y Teams SDK de cliente.|
|**participantId**| string | Sí | El ID de participante es el ID de usuario. Está disponible en Tab SSO, Bot Invoke y Teams SDK de cliente. Se recomienda obtener un ID de participante de la pestaña SSO. |
|**tenantId**| string | Sí | El identificador de inquilino es necesario para los usuarios de inquilino. Está disponible en Tab SSO, Bot Invoke y Teams SDK de cliente. Se recomienda obtener un identificador de inquilino de la pestaña SSO. |

#### <a name="example"></a>Ejemplo

# <a name="c"></a>[C#](#tab/dotnet)

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

* * *

El cuerpo de respuesta JSON de `GetParticipant` la API es:

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

|Código de respuesta|Descripción|
|---|---|
| **403** | La aplicación no está permitida para obtener información del participante. Esta es la respuesta de error más común y se desencadena si la aplicación no está instalada en la reunión. Por ejemplo, si la aplicación está deshabilitada por el administrador del inquilino o se bloquea durante la migración al sitio en vivo.|
| **200** | La información del participante se recupera correctamente.|
| **401** | La aplicación responde con un token no válido.|
| **404** | La reunión ha expirado o no se puede encontrar a ningún participante.|
| **500** | La reunión ha expirado más de 60 días desde que terminó la reunión o el participante no tiene permisos basados en su rol.|

### <a name="notificationsignal-api"></a>NotificationSignal API

Todos los usuarios de una reunión reciben las notificaciones enviadas a través de la `NotificationSignal` API.

> [!NOTE]
> * Cuando se invoca un cuadro de diálogo en la reunión, el contenido se presenta como un mensaje de chat.
> * Actualmente, no se admite el envío de notificaciones dirigidas.

#### <a name="query-parameters"></a>Parámetros de consulta

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|---|
|**conversationId**| string | Sí | El identificador de conversación está disponible como parte de la invocación de bot. |

#### <a name="example"></a>Ejemplo

Se `Bot ID` declara en el manifiesto y el bot recibe un objeto de resultado.

> [!NOTE]
> * El `completionBotId` parámetro de la es opcional en el ejemplo de carga útil `externalResourceUrl` solicitado. `Bot ID` se declara en el manifiesto y el bot recibe un objeto de resultado.
> * Los `externalResourceUrl` parámetros de anchura y altura deben estar en píxeles. Para asegurarse de que las dimensiones están dentro de los límites [permitidos,](design/designing-apps-in-meetings.md)consulte las directrices de diseño .
> * La dirección URL es la página cargada como una `<iframe>` en el cuadro de diálogo en la reunión. El dominio debe estar en la matriz de la aplicación en el manifiesto de `validDomains` la aplicación.

# <a name="c"></a>[C#](#tab/dotnet)

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

* * *

#### <a name="response-codes"></a>Códigos de respuesta

|Código de respuesta|Descripción|
|---|---|
| **201** | La actividad con señal se envía correctamente. |
| **401** | La aplicación responde con un token no válido. |
| **403** | La aplicación no puede enviar la señal. Esto puede suceder debido a varias razones, como que el administrador del inquilino deshabilita la aplicación, la aplicación se bloquea durante la migración del sitio en vivo, etc. En este caso, la carga útil contiene un mensaje de error detallado. |
| **404** | El chat de la reunión no existe. |

## <a name="enable-your-app-for-teams-meetings"></a>Habilite la aplicación para reuniones Teams

### <a name="update-your-app-manifest"></a>Actualiza el manifiesto de la aplicación

Las funcionalidades de la aplicación de reuniones se declaran en el manifiesto de la aplicación mediante el `configurableTabs` `scopes` archivo y las `context` matrices. El ámbito define a quién y el contexto definen dónde está disponible la aplicación.

> [!NOTE]
> Intente actualizar el manifiesto de la aplicación con el [esquema de manifiesto.](../resources/schema/manifest-schema-dev-preview.md)
> Las aplicaciones en las reuniones necesitan ámbito *de groupchat.* El ámbito del *equipo* solo funciona para pestañas en canales.

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
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```
> [!NOTE]
> `meetingStage` actualmente solo está disponible en la versión preliminar del desarrollador.

### <a name="context-property"></a>Propiedad context

La pestaña `context` y las propiedades le permiten determinar dónde debe aparecer la `scopes` aplicación. Las pestañas del ámbito o de la `team` extensión pueden tener más de un `groupchat` contexto. A continuación se presentan los valores de la propiedad desde la `context` que puede utilizar todos o algunos de los valores:

|Valor|Descripción|
|---|---|
| **channelTab** | Una pestaña en el encabezado de un canal de equipo. |
| **privateChatTab** | Pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios que no están en el contexto de un equipo o una reunión. |
| **reuniónChatTab** | Pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios en el contexto de una reunión programada. |
| **reuniónDetailsTab** | Una pestaña en el encabezado de la vista de detalles de la reunión del calendario. |
| **reuniónSidePanel** | Se abrió un panel en la reunión a través de la barra unificada (U-bar). |
| **reuniónStage** | Una aplicación del sidepanel se puede compartir en la etapa de reunión. |

> [!NOTE]
> `Context` propiedad actualmente no es compatible con los clientes móviles.

## <a name="configure-your-app-for-meeting-scenarios"></a>Configure la aplicación para escenarios de reunión

> [!NOTE]
> * Para que la aplicación esté visible en la galería de pestañas, debe admitir pestañas configurables y el ámbito de chat de grupo.
> * Los clientes móviles solo admiten pestañas en etapas previas y posteriores a la reunión.
> * Las experiencias en la reunión que se encuentran en el cuadro de diálogo y la pestaña en la reunión actualmente no se admiten en los clientes móviles. Para obtener más información, consulte [instrucciones para pestañas en dispositivos móviles](../tabs/design/tabs-mobile.md) al crear las pestañas para dispositivos móviles.

### <a name="before-a-meeting"></a>Antes de una reunión

Antes de una reunión, los usuarios pueden agregar pestañas, bots y extensiones de mensajería a una reunión. Los usuarios con roles de organizador y presentador pueden agregar pestañas a una reunión.

**Para agregar una pestaña a una reunión**

1. En tu calendario, selecciona una reunión a la que quieras añadir una pestaña.
1. Seleccione la pestaña **Detalles** y seleccione más <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>. Aparece la galería de pestañas.

    ![Experiencia previa a la reunión](../assets/images/apps-in-meetings/PreMeeting.png)

1. En la galería de pestañas, seleccione la aplicación que desea agregar y siga los pasos necesarios. La aplicación se instala como una pestaña.
    > [!NOTE] 
    > Actualmente, en la pestaña reuniones, no se admiten los detalles de la reunión ni la información de los participantes.

**Para agregar una extensión de mensajería a una reunión**

1. Seleccione los puntos suspensivos o el menú de desbordamiento &#x25CF;&#x25CF;&#x25CF; ubicado en el área de mensaje de composición en el chat.
1. Seleccione la aplicación que desea agregar y siga los pasos necesarios. La aplicación se instala como una extensión de mensajería.

**Para agregar un bot a una reunión**

En un chat de reunión, escriba la **@** clave y seleccione Obtener **bots**.

> [!NOTE]
> * La identidad del usuario debe confirmarse mediante [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md). Después de la autenticación, la aplicación puede recuperar el rol de usuario mediante la `GetParticipant` API.
> * En función del rol de usuario, la aplicación tiene la capacidad de proporcionar experiencias específicas de roles. Por ejemplo, una aplicación de sondeo solo permite a los organizadores y presentadores crear una nueva encuesta.
> * Las asignaciones de roles se pueden cambiar mientras se está celebrando una reunión. Para obtener más información, consulte [roles en una reunión Teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).

### <a name="during-a-meeting"></a>Durante una reunión

#### <a name="sidepanel"></a>sidePanel

Con sidePanel, puede personalizar experiencias en una reunión que permitan a los organizadores y presentadores tener diferentes conjunto de vistas y acciones. En el manifiesto de la aplicación, debe agregar sidePanel a la matriz de contexto. En la reunión y en todos los escenarios, la aplicación se representa en una pestaña en la reunión que tiene 320 píxeles de ancho. Para obtener más información, consulte [interfaz FrameContext](/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
).

Para usar la `userContext` API para enrutar las solicitudes en consecuencia, consulte [Teams SDK](../tabs/how-to/access-teams-context.md#user-context). Consulte [Teams flujo de autenticación para las pestañas](../tabs/how-to/authentication/auth-flow-tab.md). El flujo de autenticación para las pestañas es muy similar al flujo de autenticación para los sitios web. Así que las pestañas pueden usar OAuth 2.0 directamente. Consulte, [Plataforma de identidad de Microsoft y flujo de código de autorización de OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

La extensión de mensajería funciona según lo esperado cuando un usuario está en una vista en la reunión y el usuario puede publicar tarjetas de extensión de mensaje de composición. AppName in-meeting es una información sobre herramientas que indica el nombre de la aplicación en la barra en U de reunión.

> [!NOTE]
> Utilice la versión 1.7.0 o superior de [Teams SDK,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)ya que las versiones anteriores no admiten el panel lateral.

#### <a name="in-meeting-dialog"></a>Diálogo en la reunión

El cuadro de diálogo en la reunión se puede utilizar para atraer a los participantes durante la reunión y recopilar información o comentarios durante la reunión. Utilice la [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API para indicar que se debe desencadenar una notificación de burbujas. Como parte de la carga de solicitud de notificación, incluya la dirección URL donde se hospeda el contenido que se va a mostrar.

El cuadro de diálogo en la reunión no debe usar el módulo de tareas. El módulo de tareas no se invoca en un chat de reunión. Se utiliza una dirección URL de recursos externos para mostrar la burbuja de contenido en una reunión. Puede utilizar el `submitTask` método para enviar datos en un chat de reunión.

> [!NOTE]
> * Debe invocar la función [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) para descartarla automáticamente después de que un usuario realice una acción en la vista web. Este es un requisito para el envío de aplicaciones. Para obtener más información, consulte [Teams módulo de tareas del SDK](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).
> * Si desea que la aplicación admita usuarios anónimos, la carga inicial de la solicitud de invocación debe basarse en los `from.id` metadatos de solicitud en el objeto, no en los metadatos de la `from` `from.aadObjectId` solicitud. `from.id`es el ID de usuario y `from.aadObjectId` es el ID de Azure Active Directory (AAD) del usuario. Para obtener más información, consulte [uso de módulos de tareas en pestañas](../task-modules-and-cards/task-modules/task-modules-tabs.md) y cree y envíe el módulo de [tareas.](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)

#### <a name="share-to-stage"></a>Compartir al escenario 

> [!NOTE]
> * Esta funcionalidad solo está disponible actualmente en la versión preliminar del desarrollador.
> * Para usar esta característica, la aplicación debe admitir un sidepanel en la reunión.


Esta funcionalidad ofrece a los desarrolladores la capacidad de compartir una aplicación en la fase de reunión. Al permitir compartir en la etapa de reunión, los participantes de la reunión pueden colaborar en tiempo real. 

El contexto necesario está `meetingStage` en el manifiesto de la aplicación. Un requisito previo para esto es tener el `meetingSidePanel` contexto. Esto habilita el botón **Compartir** en el sidepanel como se despecita en la siguiente imagen:

  ![experiencia share_to_stage_during_meeting](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

El cambio de manifiesto que se necesita para habilitar esta funcionalidad es el siguiente: 

```json

"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "groupchat"
      ],
      "context":[
        
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```



### <a name="after-a-meeting"></a>Después de una reunión

Las configuraciones posteriores a la reunión y a la reunión previa son equivalentes.

## <a name="code-sample"></a>Ejemplo de código

|Nombre de la muestra | Descripción | .NET | Node.js |
|----------------|-----------------|--------------|--------------|
| Extensibilidad de las reuniones | Microsoft Teams ejemplo de extensibilidad de reuniones para pasar tokens. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| Bot de burbuja de contenido de reunión | Microsoft Teams ejemplo de extensibilidad de reunión para interactuar con el bot de burbuja de contenido en una reunión. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| Reunión SidePanel | Microsoft Teams ejemplo de extensibilidad de reuniones para su iteración con el panel lateral en la reunión. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |

## <a name="see-also"></a>Vea también

* [Directrices de diseño de diálogos en la reunión](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teams flujo de autenticación para pestañas](../tabs/how-to/authentication/auth-flow-tab.md)

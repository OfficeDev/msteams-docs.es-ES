---
title: Crear aplicaciones para reuniones de equipos
author: laujan
description: crear aplicaciones para reuniones de teams
ms.topic: conceptual
ms.author: lajanuar
keywords: API de roles de participantes de reuniones de aplicaciones de teams
ms.openlocfilehash: ac0d3dee30e82cde51651f7eab3b05e569b820f7
ms.sourcegitcommit: 94b1d3e50563b31c1ff01c52d563c112a2553611
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2021
ms.locfileid: "51435039"
---
# <a name="create-apps-for-teams-meetings"></a>Crear aplicaciones para reuniones de Teams

## <a name="prerequisites-and-considerations"></a>Requisitos previos y consideraciones

Antes de crear aplicaciones para reuniones de Teams, debes comprender lo siguiente:

* Debes tener conocimientos sobre cómo desarrollar aplicaciones de Teams. Para obtener más información, consulta [Desarrollo de aplicaciones de Teams.](../overview.md)

* Debes actualizar el manifiesto de la aplicación de Teams para indicar que la aplicación está disponible para reuniones. Para obtener más información, consulta [manifiesto de la aplicación](#update-your-app-manifest).

* Para que la aplicación funcione en el ciclo de vida de la reunión como una pestaña, debe admitir pestañas configurables en el ámbito de groupchat. Para obtener más información, [vea groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) y [build a group tab](../build-your-first-app/build-channel-tab.md).

* Debe cumplir las directrices generales de diseño de pestañas de Teams para escenarios previos y posteriores a la reunión. Para obtener experiencias durante las reuniones, consulte las directrices de diseño de la pestaña en la reunión y del cuadro de diálogo en la reunión. Para obtener más información, vea Directrices de diseño [de pestañas](../tabs/design/tabs.md)de Teams, directrices de diseño de [pestañas](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) en la reunión y directrices de diseño de [cuadros de diálogo en la reunión.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)

* Debes admitir el ámbito para habilitar la aplicación en `groupchat` chats previos y posteriores a la reunión. Con la experiencia de la aplicación previa a la reunión, puedes encontrar y agregar aplicaciones de reunión y realizar tareas previas a la reunión. Con la experiencia de la aplicación posterior a la reunión, puedes ver los resultados de la reunión, como los resultados de encuestas o los comentarios.

* Los parámetros de dirección URL de la API de reunión deben `meetingId` `userId` tener , y `tenantId` . Están disponibles como parte del SDK de cliente de Teams y la actividad del bot. Además, se puede recuperar información confiable para el identificador de usuario y el identificador de inquilino mediante la autenticación [de SSO de tabulación.](../tabs/how-to/authentication/auth-aad-sso.md)

* La `GetParticipant` API debe tener un registro de bot y un identificador para generar tokens de autenticación. Para obtener más información, vea [bot registration and ID](../build-your-first-app/build-bot.md).

* Para que la aplicación se actualice en tiempo real, debe estar actualizada en función de las actividades de eventos de la reunión. Estos eventos pueden estar dentro del cuadro de diálogo en la reunión y otras etapas a lo largo del ciclo de vida de la reunión. Para el cuadro de diálogo en la reunión, vea el `bot Id` parámetro de finalización en `Notification Signal API` .

## <a name="meeting-apps-api-reference"></a>Referencia de api de aplicaciones de reunión

|API|Descripción|Solicitud|Origen|
|---|---|----|---|
|**GetUserContext**| Esta API le permite obtener información contextual para mostrar contenido relevante en una pestaña de Teams. |_**microsoftTeams.getContext( ( ) => { /*...* / } )**_|SDK de cliente de Microsoft Teams|
|**GetParticipant**| Esta API permite que un bot obtenga información de los participantes mediante el identificador de reunión y el identificador de participante. |**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_ |Microsoft Bot Framework SDK|
|**NotificationSignal** | Esta API le permite proporcionar señales de reunión que se entregan mediante la API de notificación de conversación existente para el chat de bots de usuario. Le permite señalar en función de la acción del usuario que muestra un cuadro de diálogo en la reunión. |**POST** _**/v3/conversations/{conversationId}/activities**_|Microsoft Bot Framework SDK|

### <a name="getusercontext"></a>GetUserContext

Para identificar y recuperar información contextual del contenido de la pestaña, vea [Obtener contexto para la pestaña Teams](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). se usa en una pestaña al ejecutarse en el contexto de la reunión y `meetingId` se agrega para la carga de respuesta.

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
> * No almacenar en caché los roles de los participantes, ya que el organizador de la reunión puede cambiar un rol en cualquier momento.
> * Actualmente, Teams no admite listas de distribución grandes ni tamaños de lista de más de 350 participantes para la `GetParticipant` API.

#### <a name="query-parameters"></a>Parámetros de consulta

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|---|
|**meetingId**| string | Sí | El identificador de reunión está disponible a través de Bot Invoke y el SDK de cliente de Teams.|
|**participantId**| string | Sí | El identificador de participante es el identificador de usuario. Está disponible en TAB SSO, Bot Invoke y Teams Client SDK. Se recomienda obtener un identificador de participante del SSO de la pestaña. |
|**tenantId**| string | Sí | El identificador de inquilino es necesario para los usuarios del espacio empresarial. Está disponible en TAB SSO, Bot Invoke y Teams Client SDK. Se recomienda obtener un identificador de inquilino del SSO de la pestaña. |

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

|Código de respuesta|Descripción|
|---|---|
| **403** | La aplicación no puede obtener información de los participantes. Esta es la respuesta de error más común y se desencadena si la aplicación no está instalada en la reunión. Por ejemplo, si la aplicación está deshabilitada por el administrador del espacio empresarial o bloqueada durante la migración del sitio en directo.|
| **200** | La información del participante se recupera correctamente.|
| **401** | La aplicación responde con un token no válido.|
| **404** | La reunión ha expirado o no se encuentra el participante.|
| **500** | La reunión ha expirado más de 60 días desde que finalizó la reunión o el participante no tiene permisos en función de su rol.|

### <a name="notificationsignal-api"></a>NotificationSignal API

Todos los usuarios de una reunión reciben las notificaciones enviadas a través de la `NotificationSignal` API.

> [!NOTE]
> * Cuando se invoca un cuadro de diálogo en la reunión, el contenido se presenta como un mensaje de chat.
> * Actualmente, no se admite el envío de notificaciones dirigidas.

#### <a name="query-parameters"></a>Parámetros de consulta

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|---|
|**conversationId**| string | Sí | El identificador de conversación está disponible como parte de la invocación de bot |

#### <a name="example"></a>Ejemplo

Se `Bot ID` declara en el manifiesto y el bot recibe un objeto result.

> [!NOTE]
> * El `completionBotId` parámetro de la es opcional en el ejemplo de carga `externalResourceUrl` solicitada. `Bot ID` se declara en el manifiesto y el bot recibe un objeto result.
> * Los `externalResourceUrl` parámetros de ancho y alto deben estar en píxeles. Para asegurarse de que las dimensiones están dentro de los límites permitidos, vea [directrices de diseño](design/designing-apps-in-meetings.md).
> * La dirección URL es la página cargada como una en el cuadro de diálogo `<iframe>` en la reunión. El dominio debe estar en la matriz de la aplicación `validDomains` en el manifiesto de la aplicación.

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
| **201** | La actividad con señal se envía correctamente |
| **401** | La aplicación responde con un token no válido. |
| **403** | La aplicación no puede enviar la señal. Esto puede ocurrir debido a diversos motivos, como que el administrador de inquilinos deshabilita la aplicación, la aplicación se bloquea durante la migración del sitio en directo, y así sucesivamente. En este caso, la carga contiene un mensaje de error detallado. |
| **404** | El chat de reunión no existe. |

## <a name="enable-your-app-for-teams-meetings"></a>Habilitar la aplicación para reuniones de Teams

### <a name="update-your-app-manifest"></a>Actualizar el manifiesto de la aplicación

Las funcionalidades de la aplicación reuniones se declaran en el manifiesto de la aplicación mediante `configurableTabs` las `scopes` matrices , `context` y. El ámbito define a quién y el contexto define dónde está disponible la aplicación.

> [!NOTE]
> Intente actualizar el manifiesto de la aplicación con el [esquema de manifiesto](../resources/schema/manifest-schema-dev-preview.md).

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

### <a name="context-property"></a>Context (propiedad)

La pestaña y las propiedades te permiten determinar dónde debe aparecer `context` `scopes` la aplicación. Las pestañas del `team` ámbito or pueden tener más de un `groupchat` contexto. Estos son los valores de la propiedad desde `context` la que puede usar todos o algunos de los valores:

|Valor|Descripción|
|---|---|
| **channelTab** | Pestaña en el encabezado de un canal de grupo. |
| **privateChatTab** | Pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios que no se encuentra en el contexto de un equipo o reunión. |
| **meetingChatTab** | Pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios en el contexto de una reunión programada. |
| **meetingDetailsTab** | Pestaña en el encabezado de la vista de detalles de la reunión del calendario. |
| **meetingSidePanel** | Un panel en la reunión abierto a través de la barra unificada (barra U). |

> [!NOTE]
> `Context` actualmente no se admite en clientes móviles.

## <a name="configure-your-app-for-meeting-scenarios"></a>Configurar la aplicación para escenarios de reunión

> [!NOTE]
> * Para que la aplicación esté visible en la galería de pestañas, debe admitir pestañas configurables y el ámbito de chat de grupo.
> * Los clientes móviles solo admiten pestañas en fases de reunión previas y posteriores.
> * Las experiencias en la reunión que es el cuadro de diálogo y la pestaña en la reunión actualmente no se admiten en clientes móviles. Para obtener más información, consulta [las instrucciones para las pestañas en el móvil](../tabs/design/tabs-mobile.md) al crear las pestañas para móviles.

### <a name="before-a-meeting"></a>Antes de una reunión

Antes de una reunión, los usuarios pueden agregar pestañas, bots y extensiones de mensajería a una reunión. Los usuarios con roles de organizador y moderador pueden agregar pestañas a una reunión.

**Para agregar una pestaña a una reunión**

1. En el calendario, seleccione una reunión a la que desee agregar una pestaña.
1. Seleccione la **pestaña Detalles** y seleccione más <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>. Aparece la galería de pestañas.

    ![Experiencia previa a la reunión](../assets/images/apps-in-meetings/PreMeeting.png)

1. En la galería de pestañas, selecciona la aplicación que quieras agregar y sigue los pasos según sea necesario. La aplicación se instala como una pestaña.
    > [!NOTE] 
    > Actualmente, en la pestaña reuniones, no se admite la obtención de detalles de la reunión y la información de los participantes.

**Para agregar una extensión de mensajería a una reunión**

1. Seleccione los puntos suspensivos o el menú de desbordamiento &#x25CF;&#x25CF;&#x25CF; ubicado en el área del mensaje de redacción en el chat.
1. Selecciona la aplicación que quieras agregar y sigue los pasos según sea necesario. La aplicación se instala como una extensión de mensajería.

**Para agregar un bot a una reunión**

En un chat de reunión, escriba la **@** clave y seleccione Obtener **bots**.

> [!NOTE]
> * La identidad del usuario debe confirmarse con [tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md). Después de la autenticación, la aplicación puede recuperar el rol de usuario mediante la `GetParticipant` API.
> * En función del rol de usuario, la aplicación tiene la capacidad de proporcionar experiencias específicas del rol. Por ejemplo, una aplicación de sondeo solo permite a los organizadores y presentadores crear un nuevo sondeo.
> * Las asignaciones de roles se pueden cambiar mientras se está en curso una reunión. Para obtener más información, vea [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).

### <a name="during-a-meeting"></a>Durante una reunión

#### <a name="sidepanel"></a>sidePanel

Con sidePanel, puede personalizar experiencias en una reunión que permita a los organizadores y presentadores tener un conjunto diferente de vistas y acciones. En el manifiesto de la aplicación, debes agregar sidePanel a la matriz de contexto. En la reunión y en todos los escenarios, la aplicación se representa en una pestaña en la reunión que tiene 320 píxeles de ancho. Para obtener más información, vea [FrameContext interface](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
).

Para usar la `userContext` API para enrutar las solicitudes en consecuencia, vea [Sdk de Teams](../tabs/how-to/access-teams-context.md#user-context). Consulte [Flujo de autenticación de Teams para las pestañas](../tabs/how-to/authentication/auth-flow-tab.md). El flujo de autenticación para pestañas es muy similar al flujo de autenticación para sitios web. Por lo tanto, las pestañas pueden usar OAuth 2.0 directamente. Vea, Plataforma de identidades de Microsoft y flujo de código de autorización de [OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

La extensión de mensajería funciona según lo esperado cuando un usuario está en una vista en la reunión y el usuario puede publicar tarjetas de extensión de mensaje de redacción. AppName en la reunión es una información sobre herramientas que indica el nombre de la aplicación en la barra U de la reunión.

#### <a name="in-meeting-dialog"></a>Diálogo en la reunión

El cuadro de diálogo en la reunión se puede usar para interactuar con los participantes durante la reunión y recopilar información o comentarios durante la reunión. Use la API para indicar que se debe desencadenar [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) una notificación de burbuja. Como parte de la carga de solicitud de notificación, incluya la dirección URL donde se hospeda el contenido que se va a mostrar.

El cuadro de diálogo en la reunión no debe usar el módulo de tareas. El módulo de tareas no se invoca en un chat de reunión. Se usa una dirección URL de recurso externo para mostrar una burbuja de contenido en una reunión. Puede usar el método `submitTask` para enviar datos en un chat de reunión.

> [!NOTE]
> * Debe invocar la [función submitTask() para](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) descartarla automáticamente después de que un usuario realiza una acción en la vista web. Este es un requisito para el envío de la aplicación. Para obtener más información, vea [Módulo de tareas del SDK de Teams](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).
> * Si quieres que la aplicación admita usuarios anónimos, la carga inicial de la solicitud de invocación debe basarse en los metadatos de solicitud del objeto, no en `from.id` `from` los `from.aadObjectId` metadatos de la solicitud. `from.id` es el identificador de usuario y es el identificador de `from.aadObjectId` Azure Active Directory (AAD) del usuario. Para obtener más información, vea [using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) y create and send the task [module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).

### <a name="after-a-meeting"></a>Después de una reunión

Las configuraciones posteriores a la reunión y previas a la reunión son equivalentes.

## <a name="code-sample"></a>Ejemplo de código

|Nombre de ejemplo | Descripción | C# |
|----------------|-----------------|--------------|
| Extensibilidad de reuniones | Ejemplo de extensibilidad de reuniones de Microsoft Teams para pasar tokens. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) |
| Bot de burbuja de contenido de reunión | Ejemplo de extensibilidad de reuniones de Microsoft Teams para interactuar con el bot de burbujas de contenido en una reunión. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |

## <a name="see-also"></a>Vea también

> [!div class="nextstepaction"]
> [Directrices de diseño de cuadros de diálogo en la reunión](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
> [!div class="nextstepaction"]
> [Flujo de autenticación de Teams para pestañas](../tabs/how-to/authentication/auth-flow-tab.md)

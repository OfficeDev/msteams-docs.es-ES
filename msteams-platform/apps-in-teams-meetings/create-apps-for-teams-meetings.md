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
# <a name="create-apps-for-teams-meetings"></a>Crear aplicaciones para reuniones de Teams

## <a name="prerequisites-and-considerations"></a>Requisitos previos y consideraciones

1. Las aplicaciones en las reuniones necesitan conocimientos básicos del desarrollo de aplicaciones de Microsoft [Teams](../overview.md). Una aplicación en una reunión puede estar formada por [pestañas](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md)y características de [extensiones de mensajería](../messaging-extensions/what-are-messaging-extensions.md) y necesitará actualizaciones en el manifiesto de la [aplicación](#update-your-app-manifest) de Microsoft Teams para indicar que la aplicación está disponible para las reuniones.

1. Para que la aplicación funcione en el ciclo de vida de la reunión como una pestaña, debe admitir pestañas configurables en el [ámbito Groupchat](../resources/schema/manifest-schema.md#configurabletabs). *Consulte* [ampliar la aplicación de Microsoft Teams con una pestaña personalizada](../tabs/how-to/add-tab.md). Admitir el `groupchat` ámbito habilitará la aplicación en chats [anteriores](teams-apps-in-meetings.md#pre-meeting-app-experience) y [posteriores](teams-apps-in-meetings.md#post-meeting-app-experience) a la reunión.

1. Los parámetros de dirección URL `meetingId` de la API de la reunión pueden requerir, `userId` y el [tenantId](/onedrive/find-your-office-365-tenant-id) , están disponibles como parte de la actividad del SDK del cliente de Microsoft Teams y del bot. Además, se puede recuperar información fiable sobre el identificador de usuario y el identificador de inquilino mediante la [autenticación SSO de pestañas](../tabs/how-to/authentication/auth-aad-sso.md).

1. Algunas API de reunión, como `GetParticipant` requerirán un [registro de Bot y un identificador de aplicación de bot](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) para generar tokens de autenticación.

1. Como desarrollador, debe adherirse a las directrices generales de [diseño de pestañas de Microsoft Teams](../tabs/design/tabs.md) para los escenarios anteriores y posteriores a la reunión, así como las directrices de [diálogo en reunión](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) para los diálogos que se desencadenan durante la reunión de Microsoft Teams.

1. Tenga en cuenta que para que su aplicación se actualice en tiempo real, debe estar actualizada en función de las actividades de eventos de la reunión. Estos eventos pueden estar en el cuadro de diálogo de la reunión (consulte parámetro de finalización `bot Id` en `Notification Signal API` ) y otras superficies en el ciclo de vida de la reunión.

## <a name="meeting-apps-api-reference"></a>Referencia de API de las aplicaciones de reunión

|API|Descripción|Solicitud|Origen|
|---|---|----|---|
|**GetUserContext**| Obtener información contextual para mostrar contenido relevante en una pestaña de Microsoft Teams. |_**Microsoft Teams. getContext (() => {/*...* / } )**_|SDK del cliente de Microsoft Teams|
|**GetParticipant**|Esta API permite que un bot obtenga información de un participante por el identificador de la reunión y el identificador del participante.|**Get** _**/v1/Meetings/{meetingId}/participants/{participantId}? tenantid = {tenantid}**_ |SDK de Microsoft bot Framework|
|**NotificationSignal** |Las señales de reunión se entregarán con la siguiente API de notificación de conversación existente (para el chat de bot? o del usuario). Esta API permite que los desarrolladores señalen según la acción del usuario final para mostrar-caso de un burbuja de diálogo en la reunión.|**Publicar** _**/V3/Conversations/{conversationId}/Activities**_|SDK de Microsoft bot Framework|

### <a name="getusercontext"></a>GetUserContext

Consulte nuestro [contexto de obtención de la documentación de la pestaña de Microsoft Teams](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) para obtener instrucciones sobre cómo identificar y recuperar información contextual para el contenido de la pestaña. Como parte de la extensibilidad de las reuniones, se ha agregado un nuevo valor a la carga de respuesta:

✔ **meetingId**: usada por una tabulación cuando se ejecuta en el contexto de la reunión.

### <a name="getparticipant-api"></a>API de GetParticipant

> [!NOTE]
>
> * No almacene en caché roles de participantes, ya que el organizador de la reunión puede cambiar un rol en cualquier punto en el tiempo.
>
> * Actualmente, Microsoft Teams no admite listas de distribución de gran tamaño o tamaños de lista de más de 350 participantes para la `GetParticipant` API.

#### <a name="query-parameters"></a>Parámetros de consulta

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|---|
|**meetingId**| string | Sí | El identificador de la reunión está disponible a través de la invocación de bot? o Teams Client SDK.|
|**participantId**| string | Sí | ParticipantId es el identificador de usuario. Está disponible en el SSO del cliente de pestañas, Bot invocación y el SDK del cliente de Microsoft Teams. Se recomienda encarecidamente obtener un participantId desde el SSO de pestaña. |
|**tenantId**| string | Sí | El tenantId es necesario para los usuarios del inquilino. Está disponible en el SSO del cliente de pestañas, Bot invocación y el SDK del cliente de Microsoft Teams. Se recomienda encarecidamente obtener un tenantId desde el SSO de pestaña. |

#### <a name="example"></a>Ejemplo

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="json"></a>[JSON](#tab/json)

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

El cuerpo de la respuesta es:

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

#### <a name="response-codes"></a>Códigos de respuesta

* **403**: la aplicación no tiene permiso para obtener información sobre los participantes.  Esta es la respuesta de error más común y se desencadena si la aplicación no está instalada en la reunión. Por ejemplo, si la aplicación está deshabilitada por el administrador de inquilinos o se bloquea durante la migración de sitios activos.
* **200**: la información del participante se recuperó correctamente.
* **401**: token no válido.
* **404**: no se encuentra el participante.
* **500**: la reunión ha expirado (más de 60 días desde la finalización de la reunión) o el participante no tiene permisos basados en su rol.


**Próximamente**

* **404**: la reunión ha expirado o el participante no se encuentra.


### <a name="notificationsignal-api"></a>API de NotificationSignal

> [!NOTE]
> Cuando se invoca un cuadro de diálogo en la reunión, el mismo contenido también se presentará como un mensaje de chat.

#### <a name="query-parameters"></a>Parámetros de consulta

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|---|
|**conversationId**| string | Sí | El identificador de conversación está disponible como parte de la invocación de bot |

#### <a name="example"></a>Ejemplo

> [!NOTE]
>
El `completionBotId` parámetro de `externalResourceUrl` es opcional en el ejemplo de carga solicitada. `Bot ID` se declara en el manifiesto y el bot recibe un objeto de resultado.
> * Los parámetros width y height de externalResourceUrl deben estar en píxeles. Consulte las [directrices de diseño](design/designing-apps-in-meetings.md) para asegurarse de que las dimensiones están dentro de los límites permitidos.
> * La dirección URL es la página que se carga como una `<iframe>` en el cuadro de diálogo en la reunión. El dominio debe estar en la matriz de la aplicación `validDomains` en el manifiesto de la aplicación.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

* **201**: la actividad con señal se ha enviado correctamente  
* **401**: token no válido  
* **201**: la actividad con señal se ha enviado correctamente. 
* **401**: token no válido.
* **403**: la aplicación no puede enviar la señal. Esto puede ocurrir debido a diversos motivos como, por ejemplo, que el administrador del espacio empresarial deshabilita la aplicación, la aplicación se bloquea durante la migración de sitios activos y así sucesivamente. En este caso, la carga contiene un mensaje de error detallado. 
* **404**: el chat de reuniones no existe.
 

## <a name="enable-your-app-for-teams-meetings"></a>Habilitar la aplicación para reuniones de Microsoft Teams

### <a name="update-your-app-manifest"></a>Actualizar el manifiesto de la aplicación

Las funcionalidades de la aplicación reuniones se declaran en el manifiesto de la aplicación a través de los  ->  **ámbitos** configurableTabs y los matrices de **contexto** . *Scope* define quién y *Context* define dónde estará disponible la aplicación.

> [!NOTE]
> Use el [esquema del manifiesto de vista previa de desarrollador](../resources/schema/manifest-schema-dev-preview.md) para probar esto en el manifiesto de la aplicación.

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

### <a name="context-property"></a>Propiedad context

La pestaña `context` y `scopes` las propiedades funcionan en armonía para permitirle determinar dónde quiere que aparezca la aplicación. Las pestañas `team` del `groupchat` ámbito o pueden tener más de un contexto. Los valores posibles para la propiedad context son los siguientes:

* **channelTab**: una pestaña en el encabezado de un canal de equipo.
* **privateChatTab**: una pestaña en el encabezado de un grupo de chats entre un conjunto de usuarios que no están en el contexto de un equipo o una reunión.
* **meetingChatTab**: una pestaña en el encabezado de un grupo de chats entre un conjunto de usuarios en el contexto de una reunión programada.
* **meetingDetailsTab**: una pestaña en el encabezado de la vista de detalles de la reunión del calendario.
* **meetingSidePanel**: un panel en reunión que se abre a través de la barra unificada (barra u).

> [!NOTE]
> La propiedad "context" actualmente no se admite y, por lo tanto, se omitirá en clientes móviles

## <a name="configure-your-app-for-meeting-scenarios"></a>Configurar la aplicación para escenarios de reuniones

> [!NOTE]
> * Para que la aplicación esté visible en la galería de pestañas, necesita **admitir las pestañas configurables** y el **ámbito de chat en grupo**.
>
> * Los clientes móviles solo admiten fichas en las superficies anteriores y posteriores a la reunión. Las experiencias en reunión (pestaña y cuadro de diálogo en reunión) en dispositivos móviles estarán disponibles próximamente. Siga las [instrucciones para las pestañas de dispositivos móviles](../tabs/design/tabs-mobile.md) al crear las pestañas para dispositivos móviles.

### <a name="before-a-meeting"></a>Antes de una reunión

Los usuarios con roles de organizador o moderador agregan pestañas a una reunión con el botón más ➕ de las páginas de **chat** de reuniones y **detalles** de reuniones. Las extensiones de mensajería se agregan a a través del menú de puntos suspensivos/desbordamiento &#x25CF;&#x25CF;&#x25CF; situada debajo del área redactar mensaje en el chat. Los bots se agregan a un chat mediante la **@** clave "" y seleccionando **obtener bots**.

✔ La identidad del usuario *debe* confirmarse mediante el [SSO de pestañas](../tabs/how-to/authentication/auth-aad-sso.md). Tras esta autenticación, la aplicación puede recuperar el rol de usuario a través de la API de GetParticipant.

 ✔ Basándose en el rol de usuario, la aplicación ahora tendrá la capacidad de presentar experiencias específicas de roles. Por ejemplo, una aplicación de sondeo puede permitir que solo los organizadores y los moderadores creen un nuevo sondeo.

> **Nota**: las asignaciones de roles se pueden cambiar mientras una reunión está en curso.  *Vea* [roles en una reunión de Microsoft Teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019). 

### <a name="during-a-meeting"></a>Durante una reunión

#### <a name="sidepanel"></a>**sidePanel**

✔ En el manifiesto de la aplicación, agregue **sidePanel** a la matriz de **contexto** , como se ha descrito anteriormente.

✔ En la reunión y en todos los escenarios, la aplicación se representará en una pestaña en la reunión que se 320 PX en ancho. La pestaña debe estar optimizada para esto. *Consulte* la [interfaz FrameContext](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)

✔ Consulte el SDK de Microsoft [Teams](../tabs/how-to/access-teams-context.md#user-context) para usar la API de **userContext** para enrutar las solicitudes en consecuencia.

✔ Consulte el [flujo de autenticación de Teams para pestañas](../tabs/how-to/authentication/auth-flow-tab.md). El flujo de autenticación para pestañas es muy similar al flujo de autenticación de los sitios Web. Por lo tanto, las pestañas pueden usar OAuth 2,0 directamente. *Vea también* el [flujo de código de autorización de Microsoft Identity platform y OAuth 2,0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

✔ Extensión de mensaje debe funcionar como se esperaba cuando un usuario está en una vista en la reunión y debe poder publicar tarjetas de extensión de mensaje de redacción.

✔ AppName en-reunión-información sobre herramientas debe indicar el nombre de la aplicación en la barra U-Meeting.

#### <a name="in-meeting-dialog"></a>**Diálogo en la reunión**

✔ Debe adherirse a las [instrucciones de diseño del cuadro de diálogo en reunión](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).

✔ Consulte el [flujo de autenticación de Teams para pestañas](../tabs/how-to/authentication/auth-flow-tab.md).

✔ Usar la API de [notificación](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) para indicar que se debe desencadenar una notificación de burbuja.

✔ Como parte de la carga de la solicitud de notificación, incluya la dirección URL donde se hospeda el contenido que se va a mostrar.

✔ Cuadro de diálogo de reunión no debe usar el módulo de tareas.

> [!NOTE]
>
> * Estas notificaciones son persistentes en su naturaleza. Debe invocar la función [**submitTask ()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) para descartar automáticamente una vez que un usuario realiza una acción en la vista Web. Este es un requisito para el envío de aplicaciones. *Vea también*, [Teams SDK: módulo de tareas](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).
>
> * Si quiere que la aplicación admita usuarios anónimos, su carga de solicitud de invocación inicial debe basarse en el `from.id`  objeto (ID del usuario) request Metadata in the `from` Object, no el `from.aadObjectId` (ID de Azure Active Directory del usuario) request Metadata. *Consulte* [using Task modules in Tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) y [Create and Send The Task Module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).

### <a name="after-a-meeting"></a>Después de una reunión

Las configuraciones posteriores a la reunión y antes de la reunión son equivalentes.

## <a name="meeting-app-sample"></a>Ejemplo de aplicación de reunión

 > [!div class="nextstepaction"]
> [Aplicación de generador de tokens de reunión](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)

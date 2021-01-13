---
title: Crear aplicaciones para reuniones de equipos
author: laujan
description: crear aplicaciones para reuniones de teams
ms.topic: conceptual
ms.author: lajanuar
keywords: API de roles de participantes de usuario de reuniones de aplicaciones de teams
ms.openlocfilehash: 82327eca86dcdac5c47f5f4471bc91d55484d07e
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797767"
---
# <a name="create-apps-for-teams-meetings"></a>Crear aplicaciones para reuniones de Teams

## <a name="prerequisites-and-considerations"></a>Requisitos previos y consideraciones

* Las aplicaciones en reuniones requieren algunos conocimientos básicos sobre el [desarrollo de aplicaciones de Teams.](../overview.md) Una aplicación de una reunión puede incluir [](../messaging-extensions/what-are-messaging-extensions.md) [pestañas,](../tabs/what-are-tabs.md) [bots](../bots/what-are-bots.md)y características de extensiones de mensajería, y requerirá actualizaciones en el manifiesto de la aplicación [de](#update-your-app-manifest) Teams para indicar que la aplicación está disponible para reuniones

* Para que la aplicación funcione en el ciclo de vida de la reunión como una pestaña, debe admitir pestañas configurables en el ámbito [de groupchat](../resources/schema/manifest-schema.md#configurabletabs) (consulta cómo crear una [pestaña de grupo).](../build-your-first-app/build-channel-tab.md) La compatibilidad con `groupchat` el ámbito habilitará la aplicación en [chats](teams-apps-in-meetings.md#pre-meeting-app-experience) previos a la reunión y [posteriores](teams-apps-in-meetings.md#post-meeting-app-experience) a la reunión.

* Los parámetros de dirección URL de la API de reunión pueden requerir y el tenantId están disponibles como parte del SDK de cliente de Teams y la actividad `meetingId` `userId` de bots. [](/onedrive/find-your-office-365-tenant-id) Además, se puede recuperar información confiable para el identificador de usuario y el identificador de inquilino mediante la autenticación [sso de pestaña.](../tabs/how-to/authentication/auth-aad-sso.md)

* Algunas API de reunión, como , requieren un registro de bot y `GetParticipant` [un identificador](../build-your-first-app/build-bot.md) para generar tokens de autenticación.

* Debe cumplir con las directrices generales [de diseño de pestañas de Teams](../tabs/design/tabs.md) para escenarios previos y posteriores a la reunión. Para obtener experiencias durante las reuniones, consulte las directrices de [diseño](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) de la pestaña en la reunión y del [cuadro de diálogo](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) en la reunión.

* Para que la aplicación se actualice en tiempo real, debe estar actualizada en función de las actividades del evento en la reunión. Estos eventos pueden estar dentro del cuadro de diálogo en la reunión (consulte el parámetro de finalización en ) y `bot Id` `Notification Signal API` otras superficies durante el ciclo de vida de la reunión.

## <a name="meeting-apps-api-reference"></a>Referencia de API de aplicaciones de reunión

|API|Descripción|Solicitud|Origen|
|---|---|----|---|
|**GetUserContext**| Obtenga información contextual para mostrar contenido relevante en una pestaña de Teams. |_**microsoftTeams.getContext( ( ) => { /*...* / } )**_|SDK de cliente de Microsoft Teams|
|**GetParticipant**|Esta API permite que un bot obtenga información de un participante por identificador de reunión e identificador de participante.|**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_ |Microsoft Bot Framework SDK|
|**NotificationSignal** |Las señales de reunión se entregarán mediante la siguiente API de notificación de conversación existente (para chat de bot de usuario). Esta API permite a los desarrolladores señalar en función de la acción del usuario final para mostrar en caso de que se muestre una burbuja de diálogo en la reunión.|**POST** _**/v3/conversations/{conversationId}/activities**_|Microsoft Bot Framework SDK|

### <a name="getusercontext"></a>GetUserContext

Consulte nuestro artículo Obtener contexto para la documentación de la [pestaña de Teams](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) para obtener instrucciones sobre cómo identificar y recuperar información contextual para el contenido de la pestaña. Como parte de la extensibilidad de reuniones, se ha agregado un nuevo valor para la carga de respuesta:

✔ **meetingId:** se usa en una pestaña cuando se ejecuta en el contexto de la reunión.

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
>
> * No almacenar en caché los roles de los participantes, ya que el organizador de la reunión puede cambiar un rol en cualquier momento.
>
> * Actualmente, Teams no admite listas de distribución grandes ni tamaños de lista de más de 350 participantes para la `GetParticipant` API.

#### <a name="query-parameters"></a>Parámetros de consulta

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|---|
|**meetingId**| string | Sí | El identificador de reunión está disponible a través de Bot Invoke y el SDK de cliente de Teams.|
|**participantId**| string | Sí | El participantId es el identificador de usuario. Está disponible en sso de pestaña, invocación de bot y SDK de cliente de Teams. Se recomienda encarecidamente obtener un participantId del SSO de la pestaña. |
|**tenantId**| string | Sí | El tenantId es necesario para los usuarios del espacio empresarial. Está disponible en sso de pestaña, invocación de bot y SDK de cliente de Teams. Se recomienda encarecidamente obtener un tenantId del SSO de pestaña. |

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

* **403**: La aplicación no puede obtener información de participantes.  Esta es la respuesta de error más común y se desencadena si la aplicación no está instalada en la reunión. Por ejemplo, si la aplicación está deshabilitada por el administrador de inquilinos o bloqueada durante la migración de sitios en directo.
* **200**: La información de los participantes se recuperó correctamente.
* **401**: Token no válido.
* **404**: No se encuentra el participante.
* **500**: La reunión ha expirado (más de 60 días desde que finalizó la reunión) o el participante no tiene permisos en función de su rol.


**Próximamente**

* **404**: La reunión ha expirado o no se encuentra el participante.


### <a name="notificationsignal-api"></a>NotificationSignal API

> [!NOTE]
> Cuando se invoca un cuadro de diálogo en la reunión, también se presentará el mismo contenido como mensaje de chat.

#### <a name="query-parameters"></a>Parámetros de consulta

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|---|
|**conversationId**| string | Sí | El identificador de conversación está disponible como parte de la invocación de bot |

#### <a name="example"></a>Ejemplo

> [!NOTE]
>
El `completionBotId` parámetro del parámetro es opcional en el ejemplo de carga `externalResourceUrl` solicitada. `Bot ID` se declara en el manifiesto y el bot recibe un objeto de resultado.
> * Los parámetros de ancho y alto externalResourceUrl deben estar en píxeles. Consulte las [directrices de diseño](design/designing-apps-in-meetings.md) para asegurarse de que las dimensiones se encuentran dentro de los límites permitidos.
> * La dirección URL es la página cargada como un `<iframe>` cuadro de diálogo en la reunión. El dominio debe estar en la matriz de la `validDomains` aplicación en el manifiesto de la aplicación.

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

* **201:** la actividad con señal se envía correctamente  
* **401**: token no válido  
* **201**: La actividad con señal se envía correctamente. 
* **401**: Token no válido.
* **403**: La aplicación no puede enviar la señal. Esto puede ocurrir debido a diversos motivos, como que el administrador de inquilinos deshabilite la aplicación, la aplicación se bloquee durante la migración de sitios en directo, y así sucesivamente. En este caso, la carga contiene un mensaje de error detallado. 
* **404**: El chat de la reunión no existe.
 

## <a name="enable-your-app-for-teams-meetings"></a>Habilitar la aplicación para reuniones de Teams

### <a name="update-your-app-manifest"></a>Actualizar el manifiesto de la aplicación

Las funcionalidades de la aplicación de reuniones se declaran en el manifiesto de la aplicación a través de los   ->  **ámbitos configurableTabs** y las **matrices** de contexto. *El* ámbito define a quién y *el contexto* define dónde estará disponible la aplicación.

> [!NOTE]
> Usa el esquema [de manifiesto de Developer Preview](../resources/schema/manifest-schema-dev-preview.md) para probar esto en el manifiesto de la aplicación.

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

La pestaña `context` y las propiedades funcionan en armonía para permitirte determinar dónde quieres que aparezca la `scopes` aplicación. Las pestañas del `team` ámbito o pueden tener más de un `groupchat` contexto. Los valores posibles para la propiedad context son los siguientes:

* **channelTab:** una pestaña en el encabezado de un canal de equipo.
* **privateChatTab:** una pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios que no está en el contexto de un equipo o reunión.
* **meetingChatTab:** una pestaña en el encabezado de un chat de grupo entre un conjunto de usuarios en el contexto de una reunión programada.
* **meetingDetailsTab:** una pestaña en el encabezado de la vista de detalles de la reunión del calendario.
* **meetingSidePanel:** un panel en la reunión abierto a través de la barra unificada (barra u).

> [!NOTE]
> La propiedad "Context" no se admite actualmente y, por lo tanto, se omitirá en los clientes móviles

## <a name="configure-your-app-for-meeting-scenarios"></a>Configurar la aplicación para escenarios de reunión

> [!NOTE]
> * Para que la aplicación esté visible en la galería de pestañas, debe admitir **pestañas configurables** y el ámbito **de chat en grupo.**
>
> * Los clientes móviles solo admiten pestañas en superficies de reuniones previas y posteriores. Las experiencias en la reunión (cuadro de diálogo y pestaña en la reunión) en dispositivos móviles estarán disponibles próximamente. Siga las [instrucciones para pestañas en dispositivos móviles](../tabs/design/tabs-mobile.md) al crear las pestañas para móviles.

### <a name="before-a-meeting"></a>Antes de una reunión

Los usuarios con roles de organizador o moderador agregan pestañas a una reunión con el botón más ➕ en las páginas **de** detalles de chat y **reunión.** Las extensiones de mensajería se agregan a través del menú de puntos suspensivos o desbordamiento &#x25CF;&#x25CF;&#x25CF; ubicado debajo del área de redacción de mensajes en el chat. Los bots se agregan a un chat de reunión con la tecla **@** " y seleccionando **Obtener bots.**

✔ La identidad del *usuario debe* confirmarse a través del SSO de [pestañas.](../tabs/how-to/authentication/auth-aad-sso.md) Después de esta autenticación, la aplicación puede recuperar el rol de usuario a través de la API GetParticipant.

 ✔ en función del rol de usuario, la aplicación ahora tendrá la capacidad de presentar experiencias específicas de roles. Por ejemplo, una aplicación de sondeo puede permitir que solo los organizadores y los presentadores creen un nuevo sondeo.

> **NOTA:** Las asignaciones de roles se pueden cambiar mientras una reunión está en curso.  *Vea* [Roles en una reunión de Teams.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019) 

### <a name="during-a-meeting"></a>Durante una reunión

#### <a name="sidepanel"></a>**sidePanel**

✔ en el manifiesto de la aplicación, **agrega sidePanel** a **la** matriz de contexto como se ha descrito anteriormente.

✔ en la reunión, así como en todos los escenarios, la aplicación se representará en una pestaña de reunión de 320 píxeles de ancho. La pestaña debe estar optimizada para esto. *Consulta la* interfaz [, FrameContext](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)

✔Referir al SDK de [Teams](../tabs/how-to/access-teams-context.md#user-context) para usar la API **userContext** para enrutar las solicitudes en consecuencia.

✔ consulte el flujo de [autenticación de Teams para ver las pestañas.](../tabs/how-to/authentication/auth-flow-tab.md) El flujo de autenticación para pestañas es muy similar al flujo de autenticación para sitios web. Por lo tanto, las pestañas pueden usar OAuth 2.0 directamente. *Vea también ,* plataforma de identidad de Microsoft y flujo de código de autorización [de OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

✔ extensión de mensaje debe funcionar según lo esperado cuando un usuario está en una vista en la reunión y debe poder publicar tarjetas de extensión de mensaje de redacción.

✔ AppName en la reunión: la información sobre herramientas debe mostrar el nombre de la aplicación en la barra U de la reunión.

#### <a name="in-meeting-dialog"></a>**Diálogo en la reunión**

✔ debe cumplir las directrices de diseño del [cuadro de diálogo en la reunión.](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)

✔ consulte el flujo de [autenticación de Teams para ver las pestañas.](../tabs/how-to/authentication/auth-flow-tab.md)

✔ usar la API [de](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) notificación para indicar que es necesario desencadenar una notificación de burbuja.

✔ como parte de la carga de la solicitud de notificación, incluya la dirección URL donde se hospeda el contenido que se va a presentar.

✔ cuadro de diálogo En reunión no debe usar el módulo de tareas.

> [!NOTE]
>
> * Estas notificaciones son persistentes por naturaleza. Debe invocar la función [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) para descartar automáticamente después de que un usuario realiza una acción en la vista web. Este es un requisito para el envío de aplicaciones. *Vea también*, [SDK de Teams: módulo de tareas.](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)
>
> * Si quieres que la aplicación admita usuarios anónimos, la carga inicial de la solicitud de invocación debe basarse en los metadatos de solicitud (id. del usuario) en el objeto, no en los metadatos de solicitud (id. de Azure Active Directory del `from.id` `from` `from.aadObjectId` usuario). *Vea* [Usar módulos de tareas en pestañas](../task-modules-and-cards/task-modules/task-modules-tabs.md) [y Crear y enviar el módulo de tareas.](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)

### <a name="after-a-meeting"></a>Después de una reunión

Las configuraciones posteriores a la reunión y previas a la reunión son equivalentes.

## <a name="meeting-app-sample"></a>Ejemplo de aplicación de reunión

 > [!div class="nextstepaction"]
> [Aplicación generador de tokens de reunión](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)

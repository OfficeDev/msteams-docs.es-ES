---
title: Creación de aplicaciones para reuniones de Microsoft Teams
author: laujan
description: creación de aplicaciones para reuniones de Microsoft Teams
ms.topic: conceptual
ms.author: lajanuar
keywords: API de las aplicaciones de Microsoft Teams rol de participante de usuario
ms.openlocfilehash: 83e0a5b53e363a090935b4afa9840dd96c5f7381
ms.sourcegitcommit: b01986739a05c65094618fbe76aeb53d038b1c74
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/22/2020
ms.locfileid: "48182036"
---
# <a name="create-apps-for-teams-meetings-preview"></a>Creación de aplicaciones para reuniones de Microsoft Teams (versión preliminar)

>[!IMPORTANT]
> Las características incluidas en Microsoft Teams Preview se proporcionan solo para fines de acceso anticipado, pruebas y comentarios. Pueden sufrir cambios antes de que estén disponibles en la versión pública y no deben usarse en las aplicaciones de producción.

## <a name="prerequisites-and-considerations"></a>Requisitos previos y consideraciones

1. Las aplicaciones en las reuniones necesitan conocimientos básicos del desarrollo de aplicaciones de Microsoft [Teams](../overview.md). Una aplicación en una reunión puede estar formada por [pestañas](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md)y características de [extensiones de mensajería](../messaging-extensions/what-are-messaging-extensions.md) y necesitará actualizaciones en el manifiesto de la [aplicación](#update-your-app-manifest) de Microsoft Teams para indicar que la aplicación está disponible para las reuniones.

1. Para que la aplicación funcione en el ciclo de vida de la reunión como una pestaña, debe admitir pestañas configurables en el [ámbito Groupchat](../resources/schema/manifest-schema.md#configurabletabs). *Consulte* [ampliar la aplicación de Microsoft Teams con una pestaña personalizada](../tabs/how-to/add-tab.md). Admitir el `groupchat` ámbito habilitará la aplicación en chats [anteriores](teams-apps-in-meetings.md#pre-meeting-app-experience) y [posteriores](teams-apps-in-meetings.md#post-meeting-app-experience) a la reunión.

1. Los parámetros de dirección URL `meetingId` de la API de la reunión pueden requerir, `userId` y el [tenantId](/onedrive/find-your-office-365-tenant-id) , están disponibles como parte de la actividad del SDK del cliente de Microsoft Teams y del bot. Además, se puede recuperar información fiable sobre el identificador de usuario y el identificador de inquilino mediante la [autenticación SSO de pestañas](../tabs/how-to/authentication/auth-aad-sso.md).

1. Algunas API de reunión, como `GetParticipant` requerirán un [registro de Bot y un identificador de aplicación de bot](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) para generar tokens de autenticación.

1. Los desarrolladores deben adherirse a las directrices generales de diseño de la pestaña de Microsoft [Teams](../tabs/design/tabs.md) para los escenarios anteriores y posteriores a la reunión, así como las [directrices de diálogo en reunión](designing-in-meeting-dialog.md) para los diálogos que se desencadenan durante la reunión de Microsoft Teams.

## <a name="meeting-apps-api-reference"></a>Referencia de API de las aplicaciones de reunión

|API|Descripción|Solicitud|Origen|
|---|---|----|---|
|**GetUserContext**| Obtener información contextual para mostrar contenido relevante en una pestaña de Microsoft Teams. |_**Microsoft Teams. getContext (() => {/*...* / } )**_|SDK del cliente de Microsoft Teams|
|**GetParticipant**|Esta API permite que un bot obtenga información de un participante por el identificador de la reunión y el identificador del participante.|**Get** _ **/v1/Meetings/{meetingId}/participants/{participantId}? tenantid = {tenantid}**_ |SDK de Microsoft bot Framework|
|**NotificationSignal** |Las señales de reunión se entregarán con la siguiente API de notificación de conversación existente (para el chat de bot? o del usuario). Esta API permite que los desarrolladores señalen según la acción del usuario final para mostrar-caso de un burbuja de diálogo en la reunión.|**Publicar** _ **/V3/Conversations/{conversationId}/Activities**_|SDK de Microsoft bot Framework|

### <a name="getusercontext"></a>GetUserContext

Consulte nuestro [contexto de obtención de la documentación de la pestaña de Microsoft Teams](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) para obtener instrucciones sobre cómo identificar y recuperar información contextual para el contenido de la pestaña. Como parte de la extensibilidad de las reuniones, se ha agregado un nuevo valor a la carga de respuesta:

✔ **meetingId**: usada por una tabulación cuando se ejecuta en el contexto de la reunión.

### <a name="getparticipant-api"></a>API de GetParticipant

> [!NOTE]
>
> * No almacene en caché roles de participantes, ya que el organizador de la reunión puede cambiar un rol en cualquier punto en el tiempo.
>
> * Actualmente, Microsoft Teams no admite listas de distribución de gran tamaño o tamaños de lista de más de 350 participantes para la `GetParticipant` API.
>
> * La compatibilidad con bot Framework SDK estará disponible próximamente.

#### <a name="request"></a>Solicitud

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

*Vea* la [referencia de la API de bot Framework](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).

<!-- markdownlint-disable MD025 -->

**Ejemplo de C#**

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
```

* * *
<!-- markdownlint-disable MD001 -->

#### <a name="query-parameters"></a>Parámetros de consulta

**meetingId**. El identificador de la reunión es obligatorio.  
**participantId**. El identificador del participante es obligatorio.  
**tenantId**. [Identificador de inquilino](/onedrive/find-your-office-365-tenant-id) del participante. Necesario para el usuario del inquilino.

#### <a name="response-payload"></a>Carga de respuesta
<!-- markdownlint-disable MD036 -->

**Ejemplo 1**

```json
{
    "meetingRole":"Presenter",
    "conversation":{
            "isGroup": true,
            "id": "19:meeting_NDQxMzg1YjUtMGIzNC00Yjc1LWFmYWYtYzk1MGY2MTMwNjE0@thread.v2"
        }
}
```

**meetingRole** puede ser *Organizer*, *Presenter*o *Attendee*.

**Ejemplo 2**

```json
{
    "meetingRole": "Attendee",
    "conversation": {
        "isGroup": true,
        "id": "19:meeting_OWIyYWVhZWMtM2ExMi00ZTc2LTg0OGEtYWNhMTM4MmZlZTNj@thread.v2"
        }
}
```

#### <a name="response-codes"></a>Códigos de respuesta

**403**: la aplicación no tiene permiso para obtener información sobre los participantes. Esta será la respuesta de error más común y se desencadenará cuando la aplicación no se instale en la reunión, por ejemplo, cuando la aplicación está deshabilitada por el administrador de inquilinos o bloqueada durante la mitigación del sitio activo.  
**200**: la información del participante se recuperó correctamente  
**401**: token no válido  
**404**: la reunión no existe o el participante no se encuentra.

<!-- markdownlint-disable MD024 -->
### <a name="notificationsignal-api"></a>API de NotificationSignal

> [!NOTE]
> Cuando se invoca un cuadro de diálogo en la reunión, el mismo contenido también se presentará como un mensaje de chat.

#### <a name="request"></a>Solicitud

```http
POST /v3/conversations/{conversationId}/activities
```

#### <a name="query-parameters"></a>Parámetros de consulta

**conversationId**: el identificador de la conversación. Obligatorio

#### <a name="request-payload"></a>Carga de solicitud

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "type": "message",
    "text": "John Phillips assigned you a weekly todo",
    "summary": "Don't forget to meet with Marketing next week",
    "channelData": {
    "notification": {
    "alert": true,
    "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=&height=&width=&title=<TaskInfo.title>"
    }
},
    "replyToId": "1493070356924"
    }
```

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");
MeetingNotification notification = new MeetingNotification
{
    AlertInMeeting = true,
    ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=&height=&width=&title=<TaskInfo.title>"
};
activity.ChannelData = new TeamsChannelData
{
    Notification = notification
};
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript

const replyActivity = MessageFactory.text('Hi'); // this could be an adaptive card instead
        replyActivity.channelData = {
            notification: {
                alertInMeeting: true,
                externalResourceUrl: 'https://teams.microsoft.com/l/bubble/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>’
            }
        };
        await context.sendActivity(replyActivity);
```

* * *

> [!IMPORTANT]
> La dirección URL de la burbuja de contenido (URL de taskInfo) debe incluirse en la lista de [dominios válidos](../resources/schema/manifest-schema.md#validdomains) que se incluye en el manifiesto de la aplicación Teams.

#### <a name="response-codes"></a>Códigos de respuesta

**201**: la actividad con señal se ha enviado correctamente  
**401**: token no válido  
**403**: la aplicación no puede enviar la señal. En este caso, la carga debe contener un mensaje de error más detallado. Puede haber varios motivos: la aplicación está deshabilitada por el administrador de inquilinos, bloqueada durante la mitigación de sitios activos, etc.  
**404**: el chat de reuniones no existe  

## <a name="enable-your-app-for-teams-meetings"></a>Habilitar la aplicación para reuniones de Microsoft Teams

### <a name="update-your-app-manifest"></a>Actualizar el manifiesto de la aplicación

Las funcionalidades de la aplicación reuniones se declaran en el **configurableTabs**manifiesto de la aplicación a través de los  ->  **ámbitos** configurableTabs y los matrices de **contexto** . *Scope* define quién y *Context* define dónde estará disponible la aplicación.

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

La pestaña `context` y `scopes` las propiedades funcionan en armonía para permitirle determinar dónde quiere que aparezca la aplicación. Aunque las pestañas en el `personal` ámbito solo pueden tener un contexto, es decir, `personalTab` o las  `team` `groupchat` pestañas con ámbito pueden tener más de un contexto. Los valores posibles para la propiedad context son los siguientes:

* **channelTab**: una pestaña en el encabezado de un canal de equipo.
* **privateChatTab**: una pestaña en el encabezado de un grupo de chats entre un conjunto de usuarios que no están en el contexto de un equipo o una reunión.
* **meetingChatTab**: una pestaña en el encabezado de un grupo de chats entre un conjunto de usuarios en el contexto de una reunión programada.
* **meetingDetailsTab**: una pestaña en el encabezado de la vista de detalles de la reunión del calendario.
* **meetingSidePanel**: un panel en reunión que se abre a través de la barra unificada (barra u).

## <a name="configure-your-app-for-meeting-scenarios"></a>Configurar la aplicación para escenarios de reuniones

> [!NOTE]
> Para que la aplicación esté visible en la galería de pestañas, necesita **admitir las pestañas configurables** y el **ámbito de chat en grupo**.

### <a name="pre-meeting"></a>Reunión previa

Los usuarios con roles de organizador o moderador agregan pestañas a una reunión con el botón más ➕ de las páginas de **chat** de reuniones y **detalles** de reuniones. Las extensiones de mensajería se agregan a a través del menú de puntos suspensivos/desbordamiento &#x25CF;&#x25CF;&#x25CF; situada debajo del área redactar mensaje en el chat. Los bots se agregan a un chat mediante la **@** clave "" y seleccionando **obtener bots**.

✔ La identidad del usuario *debe* confirmarse mediante el [SSO de pestañas](../tabs/how-to/authentication/auth-aad-sso.md). Tras esta autenticación, la aplicación puede recuperar el rol de usuario a través de la API de GetParticipant.

 ✔ Basándose en el rol de usuario, la aplicación ahora tendrá la capacidad de presentar experiencias específicas de roles. Por ejemplo, una aplicación de sondeo puede permitir que solo los organizadores y los moderadores creen un nuevo sondeo.

> **Nota**: las asignaciones de roles se pueden cambiar mientras una reunión está en curso.  *Vea* [roles en una reunión de Microsoft Teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019). 

### <a name="in-meeting"></a>En reunión

#### <a name="side-panel"></a>**panel lateral**

✔ En el manifiesto de la aplicación agregue **sidePanel** a la matriz **meetingSurfaces** como se ha descrito anteriormente.

✔ En la reunión y en todos los escenarios, la aplicación se representará en una pestaña en la reunión que se 320 PX en ancho. La pestaña debe estar optimizada para esto. *Consulte*la [interfaz FrameContext](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)

✔ Consulte el SDK de Microsoft [Teams](../tabs/how-to/access-teams-context.md#user-context) para usar la API de **userContext** para enrutar las solicitudes en consecuencia.

✔ Consulte el [flujo de autenticación de Teams para pestañas](../tabs/how-to/authentication/auth-flow-tab.md). El flujo de autenticación para pestañas es muy similar al flujo de autenticación de los sitios Web. Por lo tanto, las pestañas pueden usar OAuth 2,0 directamente. *Vea también*el [flujo de código de autorización de Microsoft Identity platform y OAuth 2,0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

#### <a name="in-meeting-dialog"></a>**cuadro de diálogo en la reunión**

✔ Debe adherirse a las [instrucciones de diseño del cuadro de diálogo en reunión](designing-in-meeting-dialog.md).

✔ Consulte el [flujo de autenticación de Teams para pestañas](../tabs/how-to/authentication/auth-flow-tab.md).

✔ Usar la API de [notificación](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) para indicar que se debe desencadenar una notificación de burbuja.

✔ Como parte de la carga de la solicitud de notificación, incluya la dirección URL donde se hospeda el contenido que se va a mostrar.

> [!NOTE]
> Estas notificaciones son persistentes en su naturaleza. Debe invocar la función [**submitTask ()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) para descartar automáticamente una vez que un usuario realiza una acción en la vista Web. Este es un requisito para el envío de aplicaciones. *Vea también*, [Teams SDK: módulo de tareas](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).

### <a name="post-meeting"></a>Después de la reunión

Las configuraciones posteriores a la reunión y antes de la reunión son equivalentes.

## <a name="meeting-app-sample"></a>Ejemplo de aplicación de reunión

 > [!div class="nextstepaction"]
> [Aplicación de generador de tokens de reunión](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)

---
title: Crear vínculos profundos
description: Describe vínculos profundos y cómo usarlos en las aplicaciones
ms.topic: how-to
ms.localizationpriority: high
keywords: vínculo profundo de teams
ms.openlocfilehash: 79be1bcc04c33234859c4b564c9211c699b148e1
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2022
ms.locfileid: "63399313"
---
# <a name="create-deep-links"></a>Crear vínculos profundos

Puede crear vínculos a información y características en Teams. Los escenarios en los que la creación de vínculos profundos es útil son los siguientes:

* Llevar al usuario al contenido dentro de una de las pestañas de la aplicación. Por ejemplo, la aplicación puede tener un bot que envía mensajes que notifican al usuario de una actividad importante. Cuando el usuario pulsa en la notificación, el vínculo profundo navega a la pestaña para que el usuario pueda ver más detalles sobre la actividad.
* La aplicación automatiza o simplifica determinadas tareas de usuario, como crear un chat o programar una reunión, rellenando previamente los vínculos profundos con los parámetros necesarios. Esto evita la necesidad de que los usuarios indiquen la información de forma manual.

> [!NOTE]
>
> Un vínculo profundo inicia primero el explorador antes de navegar al contenido. El comportamiento de los vínculos profundos en las entidades de Teams es el siguiente:
>
> **Pestaña**:  
> ✔ Navega directamente a la dirección URL del vínculo profundo.
>
> **Bot**:  
> ✔ Vínculo profundo en el cuerpo de la tarjeta: se abre primero en el explorador.  
> ✔ Vínculo profundo agregado a la acción OpenURL en la tarjeta adaptable: navega directamente a la dirección URL del vínculo profundo.  
> ✔ Texto de markdown de hipervínculo en la tarjeta: se abre primero en el explorador.  
>
> **Chat**:  
> ✔ Markdown de hipervínculo de mensaje de texto: navega directamente a la dirección URL del vínculo profundo.  
> ✔ Vínculo pegado en la conversación de chat general: navega directamente a la dirección URL deL vínculo profundo.

## <a name="deep-linking-to-your-tab"></a>Vinculación profunda a la pestaña

Puede crear vínculos profundos a entidades en Teams. Se usa para crear vínculos que naveguen al contenido y a la información dentro de la pestaña. Por ejemplo, si la pestaña contiene una lista de tareas, los miembros del equipo pueden crear y compartir vínculos a tareas individuales. Al seleccionar el vínculo, navega a la pestaña que se centra en el elemento específico. Para implementar esto, agregue una acción **copiar vínculo** a cada elemento, de la manera que mejor se adapte a su interfaz de usuario. Cuando el usuario realiza esta acción, se llama a `shareDeepLink()` para mostrar un cuadro de diálogo que contiene un vínculo que el usuario puede copiar en el portapapeles. Al realizar esta llamada, también pasa un identificador para el elemento, que obtiene en el [contexto](~/tabs/how-to/access-teams-context.md) cuando se sigue el vínculo y se vuelve a cargar la pestaña.

Como alternativa, también puede generar vínculos profundos mediante programación, con el formato especificado más adelante en este artículo. Puede usar vínculos profundos en mensajes de [bot](~/bots/what-are-bots.md) y [conector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) que informan a los usuarios sobre los cambios en la pestaña o en los elementos que contiene.

> [!NOTE]
> Este vínculo profundo es diferente de los vínculos proporcionados por el elemento de menú **Copiar vínculo a la pestaña**, que solo genera un vínculo profundo que apunta a esta pestaña.

>[!IMPORTANT]
> Actualmente, shareDeepLink no funciona en plataformas móviles.

### <a name="show-a-deep-link-to-an-item-within-your-tab"></a>Mostrar un vínculo profundo a un elemento de la pestaña

Para mostrar un cuadro de diálogo que contiene un vínculo profundo a un elemento de la pestaña, llame a `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })`.

Proporcione los campos siguientes:

* `subEntityId`: identificador único del elemento de la pestaña al que está vinculando en profundidad.
* `subEntityLabel`: etiqueta del elemento que se va a usar para mostrar el vínculo profundo.
* `subEntityWebUrl`: campo opcional con una dirección URL de reserva que se usará si el cliente no admite la representación de la pestaña.

### <a name="generate-a-deep-link-to-your-tab"></a>Generar un vínculo profundo a la pestaña

> [!NOTE]
>
> * Las pestañas personales tienen un ámbito `personal`, mientras que las pestañas de canal y grupo usan ámbitos `team` o `group`. Los dos tipos de pestaña tienen una sintaxis ligeramente diferente, ya que solo la pestaña configurable tiene una propiedad `channel` asociada a su objeto de contexto. Consulte la referencia del [manifiesto](~/resources/schema/manifest-schema.md) para más información sobre los ámbitos de pestaña.
> * Los vínculos profundos solo funcionan correctamente si la pestaña se configuró mediante la biblioteca v0.4 o posterior y por ello tiene un identificador de entidad. Los vínculos profundos a pestañas sin identificadores de entidad siguen navegando a la pestaña, pero no pueden proporcionar el identificador de subentidad a la pestaña.

Use el formato siguiente para un vínculo profundo que puede usar en un bot, conector o tarjeta de extensión de mensajería:

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> Si el bot envía un mensaje que contiene un `TextBlock` con un vínculo profundo, se abre una nueva pestaña del explorador cuando el usuario selecciona el vínculo. Esto sucede en Chrome y en la aplicación de escritorio de Microsoft Teams, ejecutados en Linux.
> Si el bot envía la misma dirección URL de vínculo profundo a un `Action.OpenUrl`, la pestaña Teams se abre en la pestaña actual del explorador cuando el usuario selecciona el vínculo. No se abre una nueva pestaña del explorador.

<!--- TBD: Edit this article.
* Admonitions/alerts seem to be overused. 
* An important alert at the end of this table does not make sense. Also, it has a code snippet inside it.
* List items in the table are not formatted well in output.
* Some headings use -ing verbs.
* Example values and some URLs should be in backticks and not emphasized.
* Codeblock are missing language.
* Check for markdownlint errors.
* Table with just a row is not really needed. Provide the content without tabulating it.
--->

Los parámetros de consulta son:

| Nombre del parámetro | Descripción | Ejemplo |
|:------------|:--------------|:---------------------|
| `appId`&emsp; | Identificador del manifiesto. |fe4a8eba-2a31-4737-8e33-e5fae6fee194|
| `entityId`&emsp; | Identificador del elemento de la pestaña, que proporcionó al [configurar la pestaña](~/tabs/how-to/create-tab-pages/configuration-page.md).|Lista de tareas123|
| `entityWebUrl` o `subEntityWebUrl`&emsp; | Un campo opcional con una dirección URL de reserva que se usará si el cliente no admite la representación de la pestaña. | `https://tasklist.example.com/123` o `https://tasklist.example.com/list123/task456` |
| `entityLabel` o `subEntityLabel`&emsp; | Etiqueta del elemento de la pestaña que se va a usar al mostrar el vínculo profundo. | Lista de tareas 123 o "Tarea 456 |
| `context.subEntityId`&emsp; | Identificador del elemento dentro de la pestaña. |Tarea 456 |
| `context.channelId`&emsp; | Id. de canal de Microsoft Teams que está disponible en la pestaña [contexto](~/tabs/how-to/access-teams-context.md). Esta propiedad solo está disponible en pestañas configurables con un ámbito de **equipo**. No está disponible en pestañas estáticas, que tienen un ámbito **personal**.| 19:cbe3683f25094106b826c9cada3afbe0@thread.skype |
| `chatId`&emsp; | ChatId que está disponible desde el [contexto](~/tabs/how-to/access-teams-context.md) de la pestaña para el chat de grupo y de reunión | 17:b42de192376346a7906a7dd5cb84b673@thread.v2 |
| `contextType`&emsp; |  Chat es el único contextType admitido para reuniones | chat |

**Ejemplos**:

* Vínculo a una pestaña estática (personal):

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`

* Vínculo a un elemento de tarea dentro de la pestaña estática (personal):

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`

* Vínculo a una pestaña configurable: 

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`

* Vínculo a un elemento de tarea en la pestaña configurable: 

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`

* Vínculo a una aplicación de pestaña agregada a una reunión o chat grupal:

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456?context={"chatId": "17:b42de192376346a7906a7dd5cb84b673@thread.v2","contextType":"chat"}`

> [!IMPORTANT]
> Asegúrese de que todos los parámetros de consulta estén correctamente codificados por URI. Debe seguir los ejemplos anteriores con el último ejemplo:
>
> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consume-a-deep-link-from-a-tab"></a>Consumir un vínculo profundo desde una pestaña

Al navegar a un vínculo profundo, Microsoft Teams simplemente navega a la pestaña y proporciona un mecanismo a través de la biblioteca JavaScript de Microsoft Teams para recuperar el identificador de la subentidad si existe.

La llamada [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) devuelve un contexto que incluye el campo `subEntityId` si se navega a la pestaña a través de un vínculo profundo.

## <a name="deep-linking-from-your-tab"></a>Vinculación profunda desde la pestaña

Puede crear un vínculo profundo al contenido en Teams desde su pestaña. Esto es útil si la pestaña necesita vincular a otro contenido de Teams, como un canal, un mensaje, otra pestaña o incluso para abrir un cuadro de diálogo de programación. Para desencadenar una vinculación profunda de su pestaña, llame a:

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

Esta llamada le dirige a la dirección URL correcta o desencadena una acción de cliente, como abrir un cuadro de diálogo de programación o instalación de aplicaciones. Consulte el siguiente ejemplo:

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a>Vinculación profunda a un chat

Puede crear vínculos profundos a chats privados entre usuarios especificando el conjunto de participantes. Si no existe un chat con los participantes especificados, el vínculo lleva al usuario a un nuevo chat vacío. Los chats nuevos se crean en estado de borrador hasta que el usuario envía el primer mensaje. De lo contrario, puede especificar el nombre del chat si aún no existe, junto con el texto que se debe insertar en el cuadro de redacción del usuario. Puede considerar esta característica como un acceso directo para que el usuario realice la acción manual de ir al chat o crearlo y, después, escribir el mensaje.

Como ejemplo de caso de uso, si va a devolver un perfil de usuario de Office 365 desde el bot como una tarjeta, este vínculo profundo puede permitir que el usuario chatee fácilmente con esa persona.

### <a name="generate-a-deep-link-to-a-chat"></a>Generar un vínculo profundo a un chat

Use este formato para un vínculo profundo que puede usar en un bot, conector o tarjeta de extensión de mensajería:

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

Ejemplo: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

Los parámetros de consulta son:

* `users`: lista separada por comas de identificadores de usuario que representan a los participantes del chat. El usuario que realiza la acción siempre se incluye como participante. Actualmente, el campo Id. de usuario admite el UserPrincipalName de Microsoft Azure Active Directory (Azure AD), como solo una dirección de correo electrónico.
* `topicName`: un campo opcional para el nombre para mostrar del chat, en el caso de un chat con 3 o más usuarios. Si no se especifica este campo, el nombre para mostrar del chat se basa en los nombres de los participantes.
* `message`: un campo opcional para el texto del mensaje que quiere insertar en el cuadro de redacción del usuario actual mientras el chat está en un estado de borrador.

Para usar este vínculo profundo con el bot, puede especificarlo como destino de la dirección URL en el botón de la tarjeta o pulsar la acción a través del tipo de acción `openUrl`.

## <a name="generate-deep-links-to-file-in-channel"></a>Generar vínculos profundos al archivo en el canal

El siguiente formato de vínculo profundo se puede usar en un bot, conector o tarjeta de extensión de mensajería:

`https://teams.microsoft.com/l/file/<fileId>?tenantId=<tenantId>&fileType=<fileType>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadId>&groupId=<groupId>`

Los parámetros de consulta son:

* `fileId`: Identificador de archivo único de Sharepoint Online, también conocido como `sourcedoc`. Por ejemplo, `1FA202A5-3762-4F10-B550-C04F81F6ACBD`.
* `tenantId`: identificador de inquilino como `0d9b645f-597b-41f0-a2a3-ef103fbd91bb`.
* `fileType`: tipo de archivo admitido, como docx, pptx, xlsx y pdf.
* `objectUrl`: dirección URL del objeto del archivo. El formato es `https://{tenantName}.sharepoint.com/sites/{TeamName}/SharedDocuments/{ChannelName}/FileName.ext`. Por ejemplo, `https://microsoft.sharepoint.com/teams/(filepath)`.
* `baseUrl`: dirección URL base del archivo. El formato es `https://{tenantName}.sharepoint.com/sites/{TeamName}`. Por ejemplo, `https://microsoft.sharepoint.com/teams`.
* `serviceName`: nombre del servicio, id. de aplicación. Por ejemplo, `teams`.
* `threadId`: threadId es el identificador del equipo donde se almacena el archivo. Es opcional y no se puede establecer para los archivos almacenados en la carpeta de OneDrive de un usuario. threadId - 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype.
* `groupId`: id. de grupo del archivo. Por ejemplo, `ae063b79-5315-4ddb-ba70-27328ba6c31e`.

> [!NOTE]
> Puede ver `threadId` y `groupId` en la dirección URL del canal.  

El siguiente formato de vínculo profundo se usa en un bot, conector o tarjeta de extensión de mensajería: 

`https://teams.microsoft.com/l/file/<fileId>?tenantId=<tenantId>&fileType=<fileType>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadId>&groupId=<groupId>`

En el siguiente formato de ejemplo se muestra el vínculo profundo a los archivos:

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80?tenantId=0d9b645f-597b-41f0-a2a3-ef103fbd91bb&fileType=pptx&objectUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform%2FShared%20Documents%2FFC7-%20Bot%20and%20Action%20Infra%2FKaizala%20Actions%20in%20Adaptive%20Cards%20-%20Deck.pptx&baseUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform&serviceName=teams&threadId=19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype&groupId=ae063b79-5315-4ddb-ba70-27328ba6c31e`

### <a name="serialization-of-this-object"></a>Serialización de este objeto

```javascript
{
fileId: "5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80",
tenantId: "0d9b645f-597b-41f0-a2a3-ef103fbd91bb",
filetype: = "pptx",
objectUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform/Shared Documents/FC7- Bot and Action Infra/Kaizala Actions in Adaptive Cards - Deck.pptx",
baseUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform",
serviceName: "teams",
threadId: = "19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype",
groupId: "ae063b79-5315-4ddb-ba70-27328ba6c31e"
}
```

## <a name="deep-linking-to-an-app"></a>Vinculación profunda a una aplicación

Cree vínculos profundos para la aplicación después de que la aplicación aparezca en la tienda de Teams. Para crear un vínculo para iniciar Teams, anexe el identificador de aplicación a la siguiente dirección URL: `https://teams.microsoft.com/l/app/<your-app-id>`. Aparece un cuadro de diálogo para instalar la aplicación.
  
## <a name="deep-linking-for-sharepoint-framework-tabs"></a>Vinculación profunda para pestañas de SharePoint Framework

El siguiente formato de vínculo profundo se puede usar en un bot, conector o tarjeta de extensión de mensajería: `https://teams.microsoft.com/l/entity/<AppId>/<EntityId>?webUrl=<entityWebUrl>/<EntityName>`

> [!NOTE]
> Cuando un bot envía un mensaje de TextBlock con un vínculo profundo, se abre una nueva pestaña del explorador cuando los usuarios seleccionan el vínculo. Esto sucede en Chrome y en la aplicación de escritorio de Microsoft Teams, ejecutados en Linux.
> Si el bot envía la misma dirección URL de vínculo profundo a un `Action.OpenUrl`, la pestaña Teams se abre en el explorador actual cuando el usuario selecciona el vínculo. No se abre una nueva pestaña del explorador.

Los parámetros de consulta son:

* `appID`: el identificador del manifiesto, por ejemplo, `fe4a8eba-2a31-4737-8e33-e5fae6fee194`.

* `entityID`: el identificador de elemento que proporcionó al [configurar la pestaña](~/tabs/how-to/create-tab-pages/configuration-page.md). Por ejemplo, `tasklist123`.
* `entityWebUrl`: campo opcional con una dirección URL de reserva que se usará si el cliente no admite la representación de la pestaña (`https://tasklist.example.com/123` o `https://tasklist.example.com/list123/task456`).
* `entityName`: etiqueta del elemento de la pestaña que se usará al mostrar el vínculo profundo, Lista de tareas 123 o Tarea 456.

Ejemplo: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&TaskList`

## <a name="deep-linking-to-the-scheduling-dialog"></a>Vinculación profunda al cuadro de diálogo de programación

> [!NOTE]
> Esta característica está actualmente en versión preliminar para desarrolladores.

Puede crear vínculos profundos al cuadro de diálogo de programación integrado de Teams. Esto es especialmente útil si la aplicación ayuda al usuario a completar el calendario o programar tareas relacionadas.

### <a name="generate-a-deep-link-to-the-scheduling-dialog"></a>Generar un vínculo profundo al cuadro de diálogo de programación

Use el formato siguiente para un vínculo profundo que puede usar en un bot, conector o tarjeta de extensión de mensajería: `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

Ejemplo: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

> [!NOTE]
> Los parámetros de búsqueda no admiten la señal `+` en lugar de espacios en blanco (` `). Asegúrese de que el código de codificación uri devuelve `%20` para los espacios, por ejemplo, `?subject=test%20subject` es correcto, pero `?subject=test+subject` es incorrecto.

Los parámetros de consulta son:

* `attendees`: lista opcional separada por comas de identificadores de usuario que representan a los asistentes a la reunión. El usuario que realiza la acción es el organizador de la reunión. Actualmente, el campo Id. de usuario solo admite el UserPrincipalName de Azure AD, normalmente una dirección de correo electrónico.
* `startTime`: la hora de inicio opcional del evento. Debe tener [formato ISO 8601 largo](https://en.wikipedia.org/wiki/ISO_8601), por ejemplo, *2018-03-12T23:55:25+02:00*.
* `endTime`: la hora de finalización opcional del evento, también en formato ISO 8601.
* `subject`: un campo opcional para el asunto de la reunión.
* `content`: un campo opcional para el campo de detalles de la reunión.

> [!NOTE]
> En estos momentos, no se puede especificar la ubicación. Debe especificar la diferencia horaria con UTC, que significa zonas horarias al generar las horas de inicio y finalización.

Para usar este vínculo profundo con el bot, puede especificarlo como destino de la dirección URL en el botón de la tarjeta o pulsar la acción a través del tipo de acción `openUrl`.

## <a name="deep-linking-to-an-audio-or-audio-video-call"></a>Vinculación profunda a una llamada de audio o de audio y vídeo

Puede crear vínculos profundos para invocar solo audio o llamadas de audio y vídeo a un único usuario o grupo de usuarios, especificando el tipo de llamada, como *audio* o *av*, y los participantes. Después de invocar el vínculo profundo y antes de realizar la llamada, el cliente de Teams solicita una confirmación para realizar la llamada. En el caso de una llamada grupal, puede llamar a un conjunto de usuarios de VoIP y a un conjunto de usuarios de RTC en la misma invocación de vínculo profundo.

En el caso de una videollamada, el cliente pedirá confirmación y activará el vídeo del autor de la llamada para la llamada. El receptor de la llamada tiene la opción de responder solo a través de audio o con audio y vídeo, a través de la ventana de notificación de llamadas de Teams.

> [!NOTE]
> Este vínculo profundo no se puede usar para invocar una reunión.

### <a name="generate-a-deep-link-to-a-call"></a>Generar un vínculo profundo a una llamada

| Vínculo profundo | Formato | Ejemplo |
|-----------|--------|---------|
| Realizar una llamada de audio | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com` |
| Realizar una llamada de audio y vídeo | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>&withVideo=true` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withVideo=true` |
|Realizar una llamada de audio y vídeo con un origen de parámetros opcional | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>&withVideo=true&source=demoApp` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withVideo=true&source=demoApp` |  
| Realizar una llamada de audio y vídeo a una combinación de usuarios de VoIP y RTC | `https://teams.microsoft.com/l/call/0/0?users=<user1>,4:<phonenumber>` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,4:9876543210` |
  
Estos son los parámetros de consulta:

* `users`: lista separada por comas de identificadores de usuario que representan a los participantes de la llamada. Actualmente, el campo Id. de usuario admite el UserPrincipalName de Azure AD, normalmente una dirección de correo electrónico, o en el caso de una llamada RTC, admite un mri 4:&lt;número de teléfono&gt; de rtc.
* `withVideo`: este es un parámetro opcional que puede usar para realizar una videollamada. Al establecer este parámetro, solo se activará la cámara del autor de la llamada. El receptor de la llamada tiene la opción de responder a través de llamada de audio o de audio y vídeo a través de la ventana de notificación de llamadas de Teams.
* `Source`: este es un parámetro opcional, que informa sobre el origen del vínculo profundo.

## <a name="code-sample"></a>Ejemplo de código

| Ejemplo de nombre | Descripción | C# |Node.js|
|-------------|-------------|------|----|
|Vínculo profundo que consume el id. de subentidad  |Aplicación de ejemplo de Microsoft Teams para mostrar el vínculo profundo del chat del bot a la pestaña que consume el identificador de subentidad.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/csharp)|[Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/nodejs)|

## <a name="see-also"></a>Consulte también

* [Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)
* [Moodle LMS](~/resources/moodleinstructions.md)

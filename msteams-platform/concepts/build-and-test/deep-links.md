---
title: Crear vínculos profundos
description: Describe vínculos profundos y cómo usarlos en sus aplicaciones
ms.topic: how-to
localization_priority: Normal
keywords: equipos enlace profundo deeplink
ms.openlocfilehash: 837d180b06f69b9be49d898c62b9ab8ee64d51d0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566057"
---
# <a name="create-deep-links"></a>Crear vínculos profundos 

Puede crear vínculos a información y entidades dentro de Teams. Los escenarios en los que la creación de vínculos profundos son útiles son los siguientes:

* Navegar por el usuario hasta el contenido dentro de una de las pestañas de la aplicación. Por ejemplo, la aplicación puede tener un bot que envía mensajes notificando al usuario de una actividad importante. Cuando el usuario toca la notificación, el vínculo profundo navega a la pestaña para que el usuario pueda ver más detalles sobre la actividad.
* La aplicación automatiza o simplifica ciertas tareas de usuario, como crear un chat o programar una reunión, rellenando previamente los vínculos profundos con los parámetros necesarios. Esto evita la necesidad de que los usuarios introduzcan información manualmente.

> [!NOTE]
>
> Un vínculo profundo inicia el navegador primero antes de navegar hacia el contenido. El comportamiento de los vínculos profundos en Teams entidades es el siguiente:
>
> **Ficha**:  
> ✔ navega directamente a la dirección URL de deeplink.
>
> **Bot**:  
> ✔ Deeplink en el cuerpo de la tarjeta: Se abre primero en el navegador.  
> ✔ Deeplink agregado a la acción OpenURL en la tarjeta adaptable: navega directamente a la url del deeplink.  
> ✔ texto de reducción del hipervínculo en la tarjeta: Se abre primero en el navegador.  
>
> **Chat**:  
> ✔ reducción del hipervínculo del mensaje de texto: navega directamente a la url del vínculo profundo.  
> ✔ Enlace pegado en la conversación de chat general: navega directamente a la url de deeplink.

## <a name="deep-linking-to-your-tab"></a>Enlace profundo a su pestaña

Puede crear vínculos profundos a entidades en Teams. Esto se utiliza para crear vínculos que navegan al contenido y la información dentro de la pestaña. Por ejemplo, si la pestaña contiene una lista de tareas, los miembros del equipo pueden crear y compartir vínculos a tareas individuales. Al seleccionar el vínculo, navega a la pestaña que se centra en el elemento específico. Para implementar esto, agregue una acción **de vínculo de copia** a cada elemento, de la mejor manera que se adapte mejor a su interfaz de usuario. Cuando el usuario realiza esta acción, llama `shareDeepLink()` para mostrar un cuadro de diálogo que contiene un vínculo que el usuario puede copiar en el portapapeles. Al realizar esta llamada, también pasa un ID para el elemento, que se vuelve a obtener en el [contexto](~/tabs/how-to/access-teams-context.md) cuando se sigue el vínculo y se vuelve a cargar la pestaña.

Como alternativa, también puede generar vínculos profundos mediante programación, utilizando el formato especificado más adelante en este tema. Puede usar vínculos profundos en mensajes [de bots](~/bots/what-are-bots.md) y [conectores](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) que informen a los usuarios sobre los cambios en la pestaña o en los elementos que contiene.

> [!NOTE]
> Este vínculo profundo es diferente de los vínculos proporcionados por el enlace Copiar al elemento de menú **de pestañas,** que solo genera un vínculo profundo que apunta a esta pestaña.

>[!NOTE]
> Actualmente, shareDeepLink no funciona en plataformas móviles.

### <a name="show-a-deep-link-to-an-item-within-your-tab"></a>Mostrar un vínculo profundo a un elemento dentro de la pestaña

Para mostrar un cuadro de diálogo que contiene un vínculo profundo a un elemento dentro de la pestaña, llame a `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })` .

Proporcione los siguientes campos:

* `subEntityId`: Un identificador único para el elemento dentro de la pestaña al que está enlazando profundamente.
* `subEntityLabel`: Una etiqueta para el elemento que se va a utilizar para mostrar el vínculo profundo.
* `subEntityWebUrl`: un campo opcional con una dirección URL de reserva para usar si el cliente no admite la representación de la pestaña.

### <a name="generate-a-deep-link-to-your-tab"></a>Genere un vínculo profundo a su pestaña

> [!NOTE]
> Las pestañas personales tienen un `personal` ámbito, mientras que las pestañas de canal y grupo usan `team` o se `group` limitan. Los dos tipos de ficha tienen una sintaxis ligeramente diferente, ya que solo la pestaña configurable tiene una `channel` propiedad asociada a su objeto de contexto. Consulte la referencia de [manifiesto](~/resources/schema/manifest-schema.md) para obtener más información sobre los ámbitos de tabulación.

> [!NOTE]
> Los vínculos profundos solo funcionan correctamente si la pestaña se configuró mediante la biblioteca v0.4 o posterior y, debido a ello, tiene un identificador de entidad. Los vínculos profundos a pestañas sin IDENTIFICADOR de entidad todavía navegan a la pestaña, pero no pueden proporcionar el identificador de sub entidad a la pestaña.

Utilice el siguiente formato para un vínculo profundo que puede usar en una tarjeta de extensión de bot, conector o mensajería:

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> Si el bot envía un mensaje que contiene un `TextBlock` vínculo profundo, se abre una nueva pestaña del explorador cuando el usuario selecciona el vínculo. Esto sucede en Chrome y en la aplicación de escritorio Microsoft Teams, ambos que se ejecutan en Linux.
> Si el bot envía la misma dirección URL de vínculo profundo a un `Action.OpenUrl` , la pestaña Teams se abre en la pestaña actual del explorador cuando el usuario selecciona el vínculo. No se abre una nueva pestaña del navegador.

Los parámetros de consulta son:

| Nombre del parámetro | Descripción | Ejemplo |
|:------------|:--------------|:---------------------|
| `appId`&emsp; | El ID de tu manifiesto. |fe4a8eba-2a31-4737-8e33-e5fae6fee194|
| `entityId`&emsp; | El IDENTIFICADOR del elemento de la pestaña, que proporcionó al [configurar la pestaña](~/tabs/how-to/create-tab-pages/configuration-page.md).|Tasklist123|
| `entityWebUrl` o `subEntityWebUrl`&emsp; | Un campo opcional con una dirección URL de reserva para usar si el cliente no admite la representación de la pestaña. | https://tasklist.example.com/123 o https://tasklist.example.com/list123/task456 |
| `entityLabel` o `subEntityLabel`&emsp; | Una etiqueta para el elemento de la pestaña, para usar al mostrar el vínculo profundo. | Lista de tareas 123 o "Tarea 456 |
| `context`&emsp; </br></br>* `subEntityId`&emsp;</br></br> * `channelId`&emsp;| Objeto JSON que contiene los siguientes campos:</br></br> * Un ID para el elemento dentro de la pestaña. </br></br> * El ID de canal Microsoft Teams que está disponible en el [contexto](~/tabs/how-to/access-teams-context.md)de la pestaña. | 
| `subEntityId`&emsp; | Un IDENTIFICADOR para el elemento dentro de la pestaña. |Tarea456 |
| `channelId`&emsp; | El id. de canal Microsoft Teams que está disponible en el contexto de [tabulación.](~/tabs/how-to/access-teams-context.md) Esta propiedad solo está disponible en pestañas configurables con un ámbito de **equipo.** No está disponible en pestañas estáticas, que tienen un ámbito **personal.**| 19:cbe3683f25094106b826c9cada3afbe0@thread.skype |

Ejemplos:

* Enlace a una pestaña configurable: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* Enlace a un elemento de tarea dentro de la pestaña configurable: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* Enlace a una pestaña estática en sí: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`
* Enlace a un elemento de tarea dentro de la pestaña estática: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`

> [!IMPORTANT]
> Asegúrese de que todos los parámetros de consulta están codificados correctamente por URI. Debe seguir los ejemplos de preceeding utilizando el último ejemplo:

> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consume-a-deep-link-from-a-tab"></a>Consumir un vínculo profundo desde una pestaña

Al navegar a un vínculo profundo, Microsoft Teams simplemente navega a la pestaña y proporciona un mecanismo a través de la biblioteca JavaScript Microsoft Teams para recuperar el ID de subentulación si existe.

La [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) llamada devuelve un contexto que incluye el campo si la pestaña se navega a través de un vínculo `subEntityId` profundo.

## <a name="deep-linking-from-your-tab"></a>Enlace profundo desde su pestaña

Puede vincular profundamente al contenido en Teams desde su pestaña. Esto es útil si la pestaña necesita vincularse a otro contenido en Teams, como a un canal, mensaje, otra pestaña o incluso abrir un cuadro de diálogo de programación. Para activar un vínculo profundo desde la pestaña debe llamar:

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

Esta llamada le navega a la dirección URL correcta o desencadena una acción de cliente, como abrir un cuadro de diálogo de programación o instalación de aplicaciones. Vea el ejemplo siguiente:

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a>Vinculación profunda a un chat

Puede crear vínculos profundos a chats privados entre usuarios especificando el conjunto de participantes. Si no existe un chat con los participantes especificados, el vínculo navega por el usuario a un nuevo chat vacío. Los nuevos chats se crean en estado de borrador hasta que el usuario envía el primer mensaje. De lo contrario, puede especificar el nombre del chat si aún no existe, junto con el texto que se debe insertar en el cuadro de composición del usuario. Puede pensar en esta característica como un acceso directo para el usuario que realiza la acción manual de navegar o crear el chat y, a continuación, escribir el mensaje.

Como ejemplo de caso de uso, si devuelve un perfil de usuario Office 365 desde el bot como tarjeta, este vínculo profundo puede permitir al usuario chatear fácilmente con esa persona.

### <a name="generate-a-deep-link-to-a-chat"></a>Generar un vínculo profundo a un chat

Utilice este formato para un vínculo profundo que puede usar en una tarjeta de extensión de bot, conector o mensajería:

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

Ejemplo: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

Los parámetros de consulta son:

* `users`: La lista separada por comas de ID de usuario que representan a los participantes del chat. El usuario que realiza la acción siempre se incluye como participante. Actualmente, el campo User ID admite el UserPrincipalName de Azure AD, como solo una dirección de correo electrónico.
* `topicName`: Un campo opcional para el nombre para mostrar del chat, en el caso de un chat con 3 o más usuarios. Si no se especifica este campo, el nombre para mostrar del chat se basa en los nombres de los participantes.
* `message`: un campo opcional para el texto del mensaje que desea insertar en el cuadro de composición del usuario actual mientras el chat está en estado de borrador.

Para usar este vínculo profundo con el bot, especifique esto como destino de URL en el botón de la tarjeta o puntee acción a través del `openUrl` tipo de acción.

## <a name="generate-deep-links-to-file-in-channel"></a>Generar vínculos profundos al archivo en el canal

El siguiente formato de vínculo profundo se puede utilizar en una tarjeta de extensión de bot, conector o mensajería:

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80?tenantId=<tenantid>&fileType=<filetype>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadid>&groupId=<groupId>`

Los parámetros de consulta son:

* `tenantId`: Ejemplo de ID de inquilino, 0d9b645f-597b-41f0-a2a3-ef103fbd91bb
* `fileType`: Tipo de archivo compatible, como docx, pptx, xlsx y pdf
* `objectUrl`: URL del objeto del archivo, https://microsoft.sharepoint.com/teams/(filepath)
* `baseUrl`: URL base del archivo, https://microsoft.sharepoint.com/teams
* `serviceName`: Nombre del servicio, ID de aplicación
* `threadId`: El threadId es el id. Es opcional y no se puede establecer para los archivos almacenados en la carpeta de OneDrive de un usuario. threadId - 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype
* `groupId`: ID de grupo del archivo, ae063b79-5315-4ddb-ba70-27328ba6c31e

A continuación se muestra el formato de ejemplo de deeplink a archivos:

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80 ?tenantId=0d9b645f-597b-41f0-a2a3-ef103fbd91bb&fileType=pptx&objectUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform%2FShared%20Documents%2FFC7-%20Bot%20and%20Action%20Infra%2FKaizala%20Actions%20in%20Adaptive%20Cards%20-%20Deck.pptx&baseUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform&serviceName=teams&threadId=19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype&groupId=ae063b79-5315-4ddb-ba70-27328ba6c31e`

### <a name="serialization-of-this-object"></a>Serialización de este objeto:
```
{
tenantId: "0d9b645f-597b-41f0-a2a3-ef103fbd91bb",
filetype: = "pptx",
objectUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform/Shared Documents/FC7- Bot and Action Infra/Kaizala Actions in Adaptive Cards - Deck.pptx",
baseUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform",
serviceName: "teams",
threadId: = "19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype",
groupId: "ae063b79-5315-4ddb-ba70-27328ba6c31e"
}
```
## <a name="deep-linking-for-sharepoint-framework-tabs"></a>Enlace profundo para pestañas de SharePoint Framework

El siguiente formato de vínculo profundo se puede utilizar en una tarjeta de extensión de bot, conector o mensajería: `https://teams.microsoft.com/l/entity/<AppId>/<EntityId>?webUrl=<entityWebUrl>/<EntityName>`

> [!NOTE]
> Cuando un bot envía un mensaje TextBlock con un vínculo profundo, se abre una nueva pestaña del explorador cuando los usuarios seleccionan el vínculo. Esto sucede en Chrome y Microsoft Teams aplicación de escritorio que se ejecuta en Linux.
> Si el bot envía la misma dirección URL de vínculo profundo en un `Action.OpenUrl` , la pestaña Teams se abre en el explorador actual cuando el usuario selecciona el vínculo. No se abre ninguna nueva pestaña del navegador.

Los parámetros de consulta son:

* `appID`: Su ID manifiesto **fe4a8eba-2a31-4737-8e33-e5fae6fee194**.

* `entityID`: el ID de elemento que proporcionó al [configurar la pestaña](~/tabs/how-to/create-tab-pages/configuration-page.md). Por ejemplo, **tasklist123**.
* `entityWebUrl`: un campo opcional con una DIRECCIÓN URL de reserva para usar si el cliente no admite la representación de la pestaña https://tasklist.example.com/123 o https://tasklist.example.com/list123/task456 .
* `entityName`: Una etiqueta para el elemento de la pestaña, para utilizar al mostrar el vínculo profundo, la Lista de tareas 123 o la Tarea 456.

Ejemplo: https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&TaskList

## <a name="deep-linking-to-the-scheduling-dialog"></a>Vinculación profunda al cuadro de diálogo de programación

> [!NOTE]
> Esta característica se encuentra actualmente en la vista previa del desarrollador.

Puede crear vínculos profundos al cuadro de diálogo de programación integrado Teams. Esto es especialmente útil si la aplicación ayuda al usuario a completar el calendario o programar tareas relacionadas.

### <a name="generate-a-deep-link-to-the-scheduling-dialog"></a>Generar un vínculo profundo al cuadro de diálogo de programación

Utilice el siguiente formato para un vínculo profundo que puede usar en una tarjeta de extensión de bot, conector o mensajería: `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

Ejemplo: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

Los parámetros de consulta son:

* `attendees`: la lista opcional separada por comas de id. El usuario que realiza la acción es el organizador de la reunión. El campo User ID actualmente solo admite el UserPrincipalName de Azure AD, normalmente una dirección de correo electrónico.
* `startTime`: La hora de inicio opcional del evento. Esto debe ser en [formato ISO 8601 largo](https://en.wikipedia.org/wiki/ISO_8601), por ejemplo *2018-03-12T23:55:25+02:00*.
* `endTime`: La hora de finalización opcional del evento, también en formato ISO 8601.
* `subject`: Un campo opcional para el tema de la reunión.
* `content`: Un campo opcional para el campo de detalles de la reunión.

> [!NOTE]
> Actualmente, no se admite especificar la ubicación. Debe especificar el desplazamiento UTC, significa zonas horarias al generar las horas de inicio y finalización.

Para usar este vínculo profundo con el bot, puede especificarlo como destino de URL en el botón de la tarjeta o tocar la acción a través del `openUrl` tipo de acción.

## <a name="deep-linking-to-an-audio-or-audio-video-call"></a>Vinculación profunda a una llamada de audio o audio y vídeo

Puede crear vínculos profundos para invocar llamadas de audio o de vídeo a un solo usuario o a un grupo de usuarios, especificando el tipo de llamada, como *audio* o *av,* y los participantes. Después de invocar el vínculo profundo y antes de realizar la llamada, Teams cliente de escritorio solicita una confirmación para realizar la llamada. En caso de llamada de grupo, puede llamar a un conjunto de usuarios VoIP y a un conjunto de usuarios PSTN en la misma invocación de deeplink. 

En caso de una videollamada, el cliente pedirá confirmación y activará el video de la persona que llama para la llamada. El receptor de la llamada tiene la opción de responder sólo a través de audio o audio y vídeo, a través de la ventana de notificación de llamadas Teams.

> [!NOTE]
> Este vínculo profundo no se puede utilizar para invocar una reunión.

### <a name="generate-a-deep-link-to-a-call"></a>Generar un vínculo profundo a una llamada

| Vínculo profundo | Formato | Ejemplo |
|-----------|--------|---------|
| Hacer una llamada de audio | https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; , &lt; user2&gt; | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com |
| Hacer una llamada de audio y video | https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; , &lt; user2&&gt; withvideo=true | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withvideo=true |
|Realice una llamada de audio y vídeo con una fuente de parámetros opcional | https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; , &lt; user2&&gt; withvideo=true&source=demoApp | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withvideo=true&source=demoApp |  
| Realice una llamada de audio y vídeo a una combinación de usuarios de VoIP y PSTN | https://teams.microsoft.com/l/call/0/0?users=&lt&gt;;user1,4: &lt; número de teléfono&gt; | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,4:9876543210 |
  
A continuación se presentan los parámetros de consulta:
* `users`: La lista separada por comas de ID de usuario que representan a los participantes de la llamada. Actualmente, el campo User ID admite el UserPrincipalName de Azure AD, normalmente una dirección de correo electrónico o, en caso de una llamada PSTN, admite una resonancia magnética de pstn 4: &lt; phonenumber &gt; .
* `Withvideo`: Este es un parámetro opcional, que puede utilizar para realizar una videollamada. Al configurar este parámetro, solo se encenderá la cámara del autor de la llamada. El receptor de la llamada tiene la opción de responder a través de audio o audio y videollamada a través de la ventana de notificación de llamadas Teams. 
* `Source`: Este es un parámetro opcional, que informa sobre el origen del deeplink.

## <a name="code-sample"></a>Ejemplo de código

| Nombre de la muestra | Descripción | C# |Node.js|
|-------------|-------------|------|----|
|Deep Link consumiendo id.  |Microsoft Teams aplicación de ejemplo para demostrar deeplink desde el chat de bots hasta el ID de subentidad que consume la pestaña.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/nodejs)|

## <a name="see-also"></a>Vea también

[Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)


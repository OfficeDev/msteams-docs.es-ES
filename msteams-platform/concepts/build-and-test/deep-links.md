---
title: Crear vínculos profundos
description: Describe vínculos profundos y cómo usarlos en sus aplicaciones
ms.topic: how-to
localization_priority: Normal
keywords: vínculo profundo de teams deeplink
ms.openlocfilehash: a7d1490fb2066df1fdd8727b78a1a3047a91c53f
ms.sourcegitcommit: 60561c7cd189c9d6fa5e09e0f2b6c24476f2dff5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2021
ms.locfileid: "52230956"
---
# <a name="create-deep-links"></a>Crear vínculos profundos 

Puede crear vínculos a información y características dentro de Teams. Los escenarios en los que la creación de vínculos profundos son útiles son los siguientes:

* Navegar por el usuario al contenido dentro de una de las pestañas de la aplicación. Por ejemplo, la aplicación puede tener un bot que envía mensajes que notifican al usuario de una actividad importante. Cuando el usuario pulsa en la notificación, el vínculo profundo navega a la pestaña para que el usuario pueda ver más detalles sobre la actividad.
* La aplicación automatiza o simplifica determinadas tareas del usuario, como crear un chat o programar una reunión, mediante la rellenar previamente los vínculos profundos con los parámetros necesarios. Esto evita la necesidad de que los usuarios escriban manualmente información.

> [!NOTE]
>
> Un vínculo profundo inicia el explorador primero antes de navegar al contenido. El comportamiento de los vínculos profundos en Teams entidades son los siguientes:
>
> **Tab**:  
> ✔ Navega directamente a la dirección URL de vínculo profundo.
>
> **Bot**:  
> ✔ Deeplink en el cuerpo de la tarjeta: se abre primero en el explorador.  
> ✔ deeplink agregado a la acción OpenURL en la tarjeta adaptable: navega directamente a la dirección URL del vínculo profundo.  
> ✔ texto de reducción de hipervínculos en la tarjeta: se abre primero en el explorador.  
>
> **Chat**:  
> ✔ de hipervínculo de mensaje de texto: navega directamente a la dirección URL de vínculo profundo.  
> ✔ vínculo pegada en la conversación de chat general: navega directamente a la dirección URL de vínculo profundo.

## <a name="deep-linking-to-your-tab"></a>Vinculación profunda a la pestaña

Puede crear vínculos profundos a entidades en Teams. Esto se usa para crear vínculos que naveguen a contenido e información dentro de la pestaña. Por ejemplo, si la pestaña contiene una lista de tareas, los miembros del equipo pueden crear y compartir vínculos a tareas individuales. Al seleccionar el vínculo, se desplaza a la pestaña que se centra en el elemento específico. Para implementar esto, agregas una **acción de vínculo de** copia a cada elemento, de la forma que mejor se adapte a tu interfaz de usuario. Cuando el usuario realiza esta acción, llama para mostrar un cuadro de diálogo que contiene un vínculo que el usuario `shareDeepLink()` puede copiar en el Portapapeles. Al realizar esta llamada, también pasas un identificador para el [](~/tabs/how-to/access-teams-context.md) elemento, que vuelves al contexto cuando se sigue el vínculo y se vuelve a cargar la pestaña.

Como alternativa, también puede generar vínculos profundos mediante programación, con el formato especificado más adelante en este tema. Puede usar vínculos profundos en [mensajes de bot](~/bots/what-are-bots.md) y [conector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) que informan a los usuarios sobre los cambios realizados en la pestaña o en los elementos que contiene.

> [!NOTE]
> Este vínculo profundo es diferente de  los vínculos proporcionados por el elemento de menú Copiar vínculo a pestaña, que solo genera un vínculo profundo que apunta a esta pestaña.

>[!NOTE]
> Actualmente, shareDeepLink no funciona en plataformas móviles.

### <a name="showing-a-deep-link-to-an-item-within-your-tab"></a>Mostrar un vínculo profundo a un elemento dentro de la pestaña

Para mostrar un cuadro de diálogo que contiene un vínculo profundo a un elemento dentro de la pestaña, llame `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })`

Proporcione los campos siguientes:

* `subEntityId`: un identificador único para el elemento dentro de la pestaña a la que está vinculando profundamente.
* `subEntityLabel`: etiqueta para el elemento que se usará para mostrar el vínculo profundo.
* `subEntityWebUrl`: un campo opcional con una dirección URL de reserva que se usará si el cliente no admite la representación de la pestaña.

### <a name="generating-a-deep-link-to-your-tab"></a>Generación de un vínculo profundo a la pestaña

> [!NOTE]
> Las pestañas personales tienen un ámbito, mientras que las pestañas de canal `personal` y grupo usan o `team` `group` ámbitos. Los dos tipos de pestaña tienen una sintaxis ligeramente diferente, ya que solo la pestaña configurable tiene una `channel` propiedad asociada con su objeto de contexto. Vea la [referencia del manifiesto](~/resources/schema/manifest-schema.md) para obtener más información sobre los ámbitos de tabulación.

> [!NOTE]
> Los vínculos profundos solo funcionan correctamente si la pestaña se configuró mediante la biblioteca v0.4 o posterior y debido a ello tiene un identificador de entidad. Los vínculos profundos a pestañas sin identificadores de entidad siguen navegando a la pestaña, pero no pueden proporcionar el identificador de la sub entidad a la pestaña.

Use el siguiente formato para un vínculo profundo que puede usar en un bot, conector o tarjeta de extensión de mensajería:

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> Si el bot envía un mensaje que contiene un vínculo con un vínculo profundo, se abre una nueva pestaña del explorador cuando el usuario `TextBlock` selecciona el vínculo. Esto sucede en Chrome y en la Microsoft Teams de escritorio, que se ejecutan en Linux.
> Si el bot envía la misma dirección URL de vínculo profundo a un , la pestaña Teams se abre en la pestaña del explorador actual cuando el usuario `Action.OpenUrl` selecciona el vínculo. No se abre una nueva pestaña del explorador.

Los parámetros de consulta son:

| Nombre del parámetro | Descripción | Ejemplo |
|:------------|:--------------|:---------------------|
| `appId`&emsp; | El identificador del manifiesto. |fe4a8eba-2a31-4737-8e33-e5fae6fee194|
| `entityId`&emsp; | El identificador del elemento de la pestaña, que proporcionaste al [configurar la pestaña](~/tabs/how-to/create-tab-pages/configuration-page.md).|Tasklist123|
| `entityWebUrl` o `subEntityWebUrl`&emsp; | Un campo opcional con una dirección URL de reserva que se usará si el cliente no admite la representación de la pestaña. | https://tasklist.example.com/123 o https://tasklist.example.com/list123/task456 |
| `entityLabel` o `subEntityLabel`&emsp; | Una etiqueta para el elemento de la pestaña, que se usará al mostrar el vínculo profundo. | Lista de tareas 123 o "Tarea 456 |
| `context`&emsp; </br></br>* `subEntityId`&emsp;</br></br> * `channelId`&emsp;| Un objeto JSON que contiene los siguientes campos</br></br> * Un identificador para el elemento dentro de la pestaña. </br></br> * El Microsoft Teams de canal que está disponible en el contexto de la [pestaña](~/tabs/how-to/access-teams-context.md). | 
| `subEntityId`&emsp; | Un identificador para el elemento dentro de la pestaña. |Task456 |
| `channelId`&emsp; | El Microsoft Teams de canal que está disponible en el contexto de [la pestaña](~/tabs/how-to/access-teams-context.md). Esta propiedad solo está disponible en pestañas configurables con un ámbito de **equipo**. No está disponible en pestañas estáticas, que tienen un ámbito **de personal**.| 19:cbe3683f25094106b826c9cada3afbe0@thread.skype |

Ejemplos:

* Vínculo a una pestaña configurable en sí: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* Vínculo a un elemento de tarea dentro de la pestaña configurable: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* Vínculo a una pestaña estática en sí: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`
* Vínculo a un elemento de tarea dentro de la pestaña estática: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`

> [!IMPORTANT]
> Asegúrese de que todos los parámetros de consulta estén codificados correctamente en URI. Debe seguir los ejemplos de preceeding con el último ejemplo:

> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consuming-a-deep-link-from-a-tab"></a>Consumir un vínculo profundo desde una pestaña

Al navegar a un vínculo profundo, Microsoft Teams simplemente navega a la pestaña y proporciona un mecanismo a través de la biblioteca de JavaScript de Microsoft Teams para recuperar el identificador de sub entidad si existe.

La [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) llamada devuelve un contexto que incluye el campo si la pestaña se navega a través de un vínculo `subEntityId` profundo.

## <a name="deep-linking-from-your-tab"></a>Vinculación profunda desde la pestaña

Puede vincular profundamente al contenido en Teams desde la pestaña. Esto es útil si la pestaña necesita vincular a otro contenido de Teams, como un canal, un mensaje, otra pestaña o incluso para abrir un cuadro de diálogo de programación. Para desencadenar un vínculo profundo desde la pestaña, debe llamar a:

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

Esta llamada te desplaza a la dirección URL correcta o desencadena una acción de cliente, como abrir un cuadro de diálogo de programación o instalación de aplicaciones. Vea el ejemplo siguiente:

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a>Vinculación profunda a un chat

Puede crear vínculos profundos a chats privados entre usuarios especificando el conjunto de participantes. Si no existe un chat con los participantes especificados, el vínculo navega al usuario a un nuevo chat vacío. Los chats nuevos se crean en estado borrador hasta que el usuario envía el primer mensaje. De lo contrario, puede especificar el nombre del chat si aún no existe, junto con el texto que debe insertarse en el cuadro de redacción del usuario. Puede pensar en esta característica como un acceso directo para que el usuario tome la acción manual de navegar o crear el chat y, a continuación, escriba el mensaje.

Como ejemplo de uso, si devuelve un perfil de usuario de Office 365 del bot como tarjeta, este vínculo profundo puede permitir al usuario chatear fácilmente con esa persona.

### <a name="generate-a-deep-link-to-a-chat"></a>Generar un vínculo profundo a un chat

Use este formato para un vínculo profundo que puede usar en un bot, conector o tarjeta de extensión de mensajería:

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

Ejemplo: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

Los parámetros de consulta son:

* `users`: lista separada por comas de id. de usuario que representa a los participantes del chat. El usuario que realiza la acción siempre se incluye como participante. Actualmente, el campo Id. de usuario admite userPrincipalName de Azure AD, como solo una dirección de correo electrónico.
* `topicName`: un campo opcional para el nombre para mostrar del chat, en el caso de un chat con 3 o más usuarios. Si no se especifica este campo, el nombre para mostrar del chat se basa en los nombres de los participantes.
* `message`: un campo opcional para el texto del mensaje que desea insertar en el cuadro de redacción del usuario actual mientras el chat está en un estado de borrador.

Para usar este vínculo profundo con el bot, especifique esto como destino de dirección URL en el botón de la tarjeta o pulse en la acción a través del `openUrl` tipo de acción.

## <a name="generate-deep-links-to-file-in-channel"></a>Generar vínculos profundos al archivo en el canal

El siguiente formato de vínculo profundo se puede usar en un bot, conector o tarjeta de extensión de mensajería:

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80?tenantId=<tenantid>&fileType=<filetype>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadid>&groupId=<groupId>`

Los parámetros de consulta son:

* `tenantId`: Ejemplo de identificador de inquilino, 0d9b645f-597b-41f0-a2a3-ef103fbd91bb
* `fileType`: Tipo de archivo compatible, como docx, pptx, xlsx y pdf
* `objectUrl`: Dirección URL del objeto del archivo, https://microsoft.sharepoint.com/teams/(filepath)
* `baseUrl`: Dirección URL base del archivo, https://microsoft.sharepoint.com/teams
* `serviceName`: Nombre del servicio, id. de la aplicación
* `threadId`: el threadId es el identificador de equipo del equipo donde se almacena el archivo. Es opcional y no se puede establecer para los archivos almacenados en la carpeta de OneDrive usuario. threadId : 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype
* `groupId`: Id. de grupo del archivo, ae063b79-5315-4ddb-ba70-27328ba6c31e

A continuación se muestra el formato de ejemplo de vínculo profundo a archivos:

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
## <a name="deep-links-for-sharepoint-framework-tabs"></a>Vínculos profundos para SharePoint Framework pestañas

El siguiente formato de vínculo profundo se puede usar en un bot, conector o tarjeta de extensión de mensajería: `https://teams.microsoft.com/l/entity/<AppId>/<EntityId>?webUrl=<entityWebUrl>/<EntityName>`

> [!NOTE]
> Cuando un bot envía un mensaje TextBlock con un vínculo profundo, se abre una nueva pestaña del explorador cuando los usuarios seleccionan el vínculo. Esto sucede en Chrome y Microsoft Teams aplicación de escritorio que se ejecuta en Linux.
> Si el bot envía la misma dirección URL de vínculo profundo a una , la pestaña Teams se abre en el explorador actual cuando el usuario `Action.OpenUrl` selecciona el vínculo. No se abre ninguna nueva pestaña del explorador.

Los parámetros de consulta son:

* `appID`: Su identificador de **manifiesto fe4a8eba-2a31-4737-8e33-e5fae6fee194**.

* `entityID`: El identificador de elemento que proporcionaste [al configurar la pestaña](~/tabs/how-to/create-tab-pages/configuration-page.md). Por ejemplo, **tasklist123**.
* `entityWebUrl`: un campo opcional con una dirección URL de reserva que se usará si el cliente no admite la representación de la pestaña - https://tasklist.example.com/123 o https://tasklist.example.com/list123/task456 .
* `entityName`: una etiqueta para el elemento de la pestaña, que se usará al mostrar el vínculo profundo, la lista de tareas 123 o la tarea 456.

Ejemplo: https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&TaskList

## <a name="linking-to-the-scheduling-dialog"></a>Vinculación al cuadro de diálogo de programación

> [!NOTE]
> Esta característica se encuentra actualmente en versión preliminar del desarrollador.

Puede crear vínculos profundos al Teams de programación integrado. Esto es especialmente útil si la aplicación ayuda al usuario a completar el calendario o programar tareas relacionadas.

### <a name="generating-a-deep-link-to-the-scheduling-dialog"></a>Generar un vínculo profundo al cuadro de diálogo de programación

Use el siguiente formato para un vínculo profundo que puede usar en un bot, connector o tarjeta de extensión de mensajería: `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

Ejemplo: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

Los parámetros de consulta son:

* `attendees`: la lista opcional separada por comas de los id. de usuario que representan a los asistentes a la reunión. El usuario que realiza la acción es el organizador de la reunión. Actualmente, el campo Id. de usuario solo es compatible con UserPrincipalName de Azure AD, normalmente una dirección de correo electrónico.
* `startTime`: la hora de inicio opcional del evento. Debe tener un formato [LARGO ISO 8601](https://en.wikipedia.org/wiki/ISO_8601), por *ejemplo, 2018-03-12T23:55:25+02:00*.
* `endTime`: la hora de finalización opcional del evento, también en formato ISO 8601.
* `subject`: un campo opcional para el asunto de la reunión.
* `content`: un campo opcional para el campo de detalles de la reunión.

> [!NOTE]
> Actualmente, no se admite la especificación de la ubicación. Debe especificar el desplazamiento UTC, significa zonas horarias al generar las horas de inicio y finalización.

Para usar este vínculo profundo con el bot, puedes especificarlo como el destino de la dirección URL en el botón de la tarjeta o pulsar en la acción a través del `openUrl` tipo de acción.

## <a name="code-sample"></a>Ejemplo de código

| Nombre de ejemplo | Descripción | C # |Node.js|
|-------------|-------------|------|----|
|Id. de subentidad de consumo de vínculos profundos  |Microsoft Teams aplicación de ejemplo para demostrar el vínculo profundo desde el chat del bot hasta el identificador de subentidad de consumo de pestañas.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/nodejs)|

## <a name="see-also"></a>Vea también

[Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)


---
title: Crear vínculos profundos al contenido
description: Describe vínculos profundos y cómo usarlos en las aplicaciones
ms.topic: how-to
keywords: vínculo profundo de teams deeplink
ms.openlocfilehash: 96e6fc0a47eb64b9e1c6c03721d386ce4dfbb51d
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014316"
---
# <a name="create-deep-links-to-content-and-features-in-microsoft-teams"></a>Crear vínculos profundos a contenido y características en Microsoft Teams

Puede crear vínculos a información y características dentro de Teams. Ejemplos de dónde puede resultar útil:

* Navegar por el usuario al contenido dentro de una de las pestañas de la aplicación. Por ejemplo, la aplicación puede tener un bot que envía mensajes que notifican al usuario de una actividad importante. Cuando el usuario pulsa en la notificación, el vínculo profundo navega a la pestaña para que el usuario pueda ver más detalles sobre la actividad.
* La aplicación automatiza o simplifica determinadas tareas del usuario, como crear un chat o programar una reunión, mediante la rellenar previamente los vínculos profundos con los parámetros necesarios. Esto evita la necesidad de que los usuarios escriban manualmente información.

> [!NOTE]
>
> Un vínculo profundo inicia el explorador primero antes de navegar a contenido e información de la siguiente manera:
>
> **Pestaña:**  
> ✔ navega directamente a la dirección URL de vínculo profundo.
>
> **Bot:**  
> ✔ Deeplink en el cuerpo de la tarjeta: se abre primero en el explorador.  
> ✔ deeplink agregado a la acción OpenURL en la tarjeta adaptable: navega directamente a la dirección URL de deeplink.  
> ✔ texto de markdown de hipervínculo en la tarjeta: se abre primero en el explorador.  
>
> **Chat:**  
> ✔ markdown de hipervínculo de mensaje de texto: navega directamente a la dirección URL de vínculo profundo.  
> ✔ vínculo pegada en la conversación de chat general: navega directamente a la dirección URL de deeplink.

## <a name="deep-linking-to-your-tab"></a>Vinculación profunda a la pestaña

Puede crear vínculos profundos a entidades en Teams. Normalmente, esto se usa para crear vínculos que navegan a contenido e información dentro de la pestaña. Por ejemplo, si la pestaña contiene una lista de tareas, los miembros del equipo pueden crear y compartir vínculos a tareas individuales. Cuando se hace clic en él, el vínculo navega a la pestaña que se centra en el elemento específico. Para implementar esto, agregue una acción de "copiar vínculo" a cada elemento, de la forma que mejor se adapte a su interfaz de usuario. Cuando el usuario realiza esta acción, se llama para mostrar un cuadro de diálogo que contiene un vínculo que el usuario `shareDeepLink()` puede copiar en el Portapapeles. Al realizar esta llamada, también pasas un identificador para el [](~/tabs/how-to/access-teams-context.md) elemento, que vuelves a obtener en el contexto cuando se sigue el vínculo y se vuelve a cargar la pestaña.

Como alternativa, también puede generar vínculos profundos mediante programación, con el formato especificado más adelante en este tema. Es posible que desee usarlas en mensajes [de bots](~/bots/what-are-bots.md) [y](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) conectores que informan a los usuarios sobre los cambios en la pestaña o en los elementos dentro de ella.

> [!NOTE]
> Esto es diferente de los  vínculos proporcionados por el elemento de menú Copiar vínculo a pestaña, que solo genera un vínculo profundo que apunta a esta pestaña.

>[!NOTE]
> Actualmente, shareDeepLink no funciona en plataformas móviles.

### <a name="showing-a-deep-link-to-an-item-within-your-tab"></a>Mostrar un vínculo profundo a un elemento dentro de la pestaña

Para mostrar un cuadro de diálogo que contiene un vínculo profundo a un elemento dentro de la pestaña, llame `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })`

Proporcione estos campos:

* `subEntityId`&emsp;Un identificador único para el elemento dentro de la pestaña al que se vincula profundamente
* `subEntityLabel`&emsp;Una etiqueta para el elemento que se usará para mostrar el vínculo profundo
* `subEntityWebUrl`&emsp;Un campo opcional con una dirección URL de reserva para usar si el cliente no admite la representación de la pestaña

### <a name="generating-a-deep-link-to-your-tab"></a>Generación de un vínculo profundo a la pestaña

> [!NOTE]
> Las pestañas personales tienen un ámbito, mientras que las pestañas de canal y `personal` grupo usan `team` o `group` ámbitos. Los dos tipos de pestaña tienen una sintaxis ligeramente diferente, ya que solo la ficha configurable tiene una `channel` propiedad asociada a su objeto de contexto. Consulta la referencia [del](~/resources/schema/manifest-schema.md) manifiesto para obtener más información sobre los ámbitos de pestaña.

> [!NOTE]
> Los vínculos profundos solo funcionan correctamente si la pestaña se configuró con la biblioteca v0.4 o posterior y, por ello, tiene un identificador de entidad. Los vínculos profundos a pestañas sin identificadores de entidad siguen navegando a la pestaña, pero no pueden proporcionar el identificador de la sub entity a la pestaña.

Use este formato para un vínculo profundo que puede usar en un bot, conector o tarjeta de extensión de mensajería:

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> Si el bot envía un mensaje que contiene un vínculo profundo, se abre una nueva pestaña del explorador cuando el usuario `TextBlock` selecciona el vínculo. Esto sucede en Chrome y en la aplicación de escritorio de Microsoft Teams, ambos en Linux.
> Si el bot envía la misma dirección URL de vínculo profundo a una , la pestaña Teams se abre en la pestaña del explorador actual cuando el usuario hace clic `Action.OpenUrl` en el vínculo. No se abre ninguna pestaña nueva del explorador.

Los parámetros de consulta son:

* `appId`&emsp;El identificador del manifiesto; por ejemplo, "fe4a8eba-2a31-4737-8e33-e5fae6fee194"
* `entityId`&emsp;El identificador del elemento de la pestaña, que proporcionó [al configurar la pestaña;](~/tabs/how-to/create-tab-pages/configuration-page.md) por ejemplo, "tasklist123"
* `entityWebUrl`o un campo opcional con una dirección URL de reserva para usar si el cliente no admite la representación de la pestaña; por `subEntityWebUrl` &emsp; ejemplo, " https://tasklist.example.com/123 " o https://tasklist.example.com/list123/task456 " "
* `entityLabel`o una etiqueta para el elemento de la pestaña, que se usará al mostrar el vínculo profundo; por ejemplo, "Lista de tareas `subEntityLabel` &emsp; 123" o "Tarea 456"
* `context`&emsp;Un objeto JSON que contiene los siguientes campos:
  * `subEntityId`&emsp;Un identificador para el elemento _dentro de_ la pestaña; por ejemplo, "task456"
  * `channelId`&emsp;El identificador de canal de Microsoft Teams (disponible en el contexto [de](~/tabs/how-to/access-teams-context.md)pestaña; por ejemplo, "19:cbe3683f25094106b826c9cada3afbe0@thread.skype". Esta propiedad solo está disponible en pestañas configurables con un ámbito de "equipo". No está disponible en pestañas estáticas, que tienen un ámbito de "personal".

Ejemplos:

* Vínculo a una pestaña configurable en sí: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* Vínculo a un elemento de tarea dentro de la pestaña configurable: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* Vínculo a una pestaña estática en sí: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`
* Vínculo a un elemento de tarea dentro de la pestaña estática: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`

> [!IMPORTANT]
> Asegúrese de que todos los parámetros de consulta estén codificados correctamente en URI. Por razones de legibilidad, los ejemplos anteriores no lo son, pero debe hacerlo. Con el último ejemplo:
> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consuming-a-deep-link-from-a-tab"></a>Consumo de un vínculo profundo desde una pestaña

Al navegar a un vínculo profundo, Microsoft Teams simplemente navega a la pestaña y proporciona un mecanismo a través de la biblioteca de JavaScript de Microsoft Teams para recuperar el identificador de la sub entity (si existe).

La llamada devuelve un contexto que incluye el campo si la pestaña se ha [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) `subEntityId` navegado a través de un vínculo profundo.

## <a name="deep-linking-from-your-tab"></a>Vinculación profunda desde la pestaña

Puede vincular en profundidad al contenido de Teams desde su pestaña. Esto resulta útil si la pestaña necesita vincularse a otro contenido de Teams, como un canal, un mensaje, otra pestaña o incluso para abrir un cuadro de diálogo de programación. Para desencadenar un vínculo profundo desde la pestaña, debes llamar a:

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

Esto te llevará a la dirección URL correcta o desencadenará una acción del cliente, como abrir un cuadro de diálogo de programación o instalación de la aplicación. Ejemplo:

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a>Vinculación profunda a un chat

Puede crear vínculos profundos a chats privados entre usuarios especificando el conjunto de participantes. Si no existe un chat con los participantes especificados, el vínculo navegará al usuario a un nuevo chat vacío. Los chats nuevos se crearán en estado borrador hasta que el usuario envíe el primer mensaje. Opcionalmente, puede especificar el nombre del chat (si aún no existe), junto con el texto que debe insertarse en el cuadro de redacción del usuario. Puede pensar en esta característica como un acceso directo para que el usuario tome la acción manual de navegar al chat o crearlo y, a continuación, escribir el mensaje.

Como ejemplo de caso de uso, si va a devolver un perfil de usuario de Office 365 desde el bot como tarjeta, este vínculo profundo puede permitir al usuario chatear fácilmente con esa persona.

### <a name="generating-a-deep-link-to-a-chat"></a>Generación de un vínculo profundo a un chat

Use este formato para un vínculo profundo que puede usar en un bot, conector o tarjeta de extensión de mensajería:

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

Ejemplo: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

Los parámetros de consulta son:

* `users`: la lista separada por comas de los id. de usuario que representan a los participantes del chat. El usuario que realiza la acción siempre se incluye como participante. Actualmente, el campo Id. de usuario solo admite el userPrincipalName de Azure AD (normalmente una dirección de correo electrónico).
* `topicName`: un campo opcional para el nombre para mostrar del chat, en el caso de un chat con 3 o más usuarios. Si no se especifica este campo, el nombre para mostrar del chat se basará en los nombres de los participantes.
* `message`: campo opcional para el texto del mensaje que desea insertar en el cuadro de redacción del usuario actual mientras el chat está en un estado de borrador.

Para usar este vínculo profundo con el bot, puedes especificarlo como destino de la dirección URL en el botón de la tarjeta o pulsa en la acción a través del `openUrl` tipo de acción.

## <a name="linking-to-the-scheduling-dialog"></a>Vinculación al cuadro de diálogo de programación

> [!Note]
> Esta característica se encuentra actualmente en versión preliminar para desarrolladores.

Puede crear vínculos profundos al cuadro de diálogo de programación integrado de Teams. Esto es especialmente útil si la aplicación ayuda al usuario a completar el calendario o programar tareas relacionadas.

### <a name="generating-a-deep-link-to-the-scheduling-dialog"></a>Generación de un vínculo profundo al cuadro de diálogo de programación

Use este formato para un vínculo profundo que puede usar en un bot, conector o tarjeta de extensión de mensajería: `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

Ejemplo: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

Los parámetros de consulta son:

* `attendees`: la lista opcional separada por comas de los id. de usuario que representan a los asistentes de la reunión. El usuario que realiza la acción es el organizador de la reunión. Actualmente, el campo Id. de usuario solo admite el userPrincipalName de Azure AD (normalmente una dirección de correo electrónico).
* `startTime`: la hora de inicio opcional del evento. Debe estar en formato [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)largo, por ejemplo "2018-03-12T23:55:25+02:00".
* `endTime`: Hora de finalización opcional del evento, también en formato ISO 8601.
* `subject`: un campo opcional para el asunto de la reunión.
* `content`: un campo opcional para el campo de detalles de la reunión.

Actualmente, no se admite la especificación de la ubicación. Al generar las horas de inicio y finalización, asegúrese de especificar el desplazamiento UTC (zonas horarias).

Para usar este vínculo profundo con el bot, puedes especificarlo como destino de dirección URL en el botón de la tarjeta o pulsa en la acción a través del `openUrl` tipo de acción.

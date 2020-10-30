---
title: Crear vínculos profundos
description: Describe los vínculos profundos y cómo usarlos en las aplicaciones
keywords: vínculo profundo vínculo profundo de Teams
ms.openlocfilehash: 03580c4d15c82da70402d68d85b0d28f8afa670e
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796333"
---
# <a name="create-deep-links-to-content-and-features-in-microsoft-teams"></a>Crear vínculos profundos para el contenido y las características en Microsoft Teams

Puede crear vínculos a información y características dentro del cliente de Microsoft Teams. Ejemplos de dónde puede resultar útil esto:

* Navegar al usuario al contenido dentro de una de las pestañas de la aplicación. Por ejemplo, la aplicación puede tener un bot que envía mensajes que notifican al usuario de una actividad importante. Cuando el usuario pulsa en la notificación, el vínculo profundo navega a la ficha para que el usuario pueda ver más detalles sobre la actividad.
* La aplicación automatiza o simplifica determinadas tareas de usuario, como la creación de un chat o la programación de una reunión, rellenando previamente los vínculos profundos con los parámetros necesarios. Esto evita la necesidad de que los usuarios escriban información manualmente.

## <a name="deep-linking-to-your-tab"></a>Vínculo profundo a su pestaña

Puede crear vínculos profundos a entidades en Microsoft Teams. Normalmente, se usa para crear vínculos que naveguen al contenido y a la información dentro de la pestaña. Por ejemplo, si la ficha contiene una lista de tareas, los miembros del equipo pueden crear y compartir vínculos a tareas individuales. Cuando se hace clic en el vínculo, se desplaza a la ficha que se centra en el elemento específico. Para implementar esto, se agrega una acción "Copiar vínculo" a cada elemento, de la manera que mejor se adapte a la interfaz de usuario. Cuando el usuario realiza esta acción, llama `shareDeepLink()` a para mostrar un cuadro de diálogo que contiene un vínculo que el usuario puede copiar en el portapapeles. Al realizar esta llamada, también pasa un identificador para el elemento, que se obtiene en el [contexto](~/tabs/how-to/access-teams-context.md) cuando se sigue el vínculo y se vuelve a cargar la pestaña.

Como alternativa, también puede generar vínculos profundos mediante programación, usando el formato especificado más adelante en este tema. Es posible que desee usarlos en mensajes de [robot](~/bots/what-are-bots.md) y [conectores](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) que informen a los usuarios sobre los cambios en la pestaña, o los elementos que contiene.

> [!NOTE]
> Esto es diferente de los vínculos que proporciona el elemento de menú **Copiar vínculo a ficha** , que solo genera un vínculo profundo que apunta a esta pestaña.

### <a name="showing-a-deep-link-to-an-item-within-your-tab"></a>Mostrar un vínculo profundo a un elemento dentro de la pestaña

Para mostrar un cuadro de diálogo que contenga un vínculo profundo a un elemento dentro de la pestaña, llame a `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })`

Proporcione estos campos:

* `subEntityId`&emsp;Un identificador único para el elemento dentro de la pestaña al que se va a vincular en profundidad
* `subEntityLabel`&emsp;Etiqueta del elemento que se va a usar para mostrar el vínculo en profundidad.
* `subEntityWebUrl`&emsp;Un campo opcional con una dirección URL de reserva para usar si el cliente no admite la representación de la pestaña

### <a name="generating-a-deep-link-to-your-tab"></a>Creación de un vínculo profundo a su pestaña

> [!NOTE]
> Las pestañas estáticas tienen un ámbito de "personal" y las fichas configurables tienen un ámbito de "equipo". Los dos tipos de pestañas tienen una sintaxis ligeramente diferente, ya que solo la pestaña configurable tiene una `channel` propiedad asociada a su objeto Context. Vea la referencia del [manifiesto](~/resources/schema/manifest-schema.md) para obtener más información sobre los ámbitos personales y de equipo.
> [!NOTE]
> Los vínculos profundos funcionan correctamente sólo si la ficha se configuró con la v 0.4 o la biblioteca posterior y debido a que tiene un identificador de entidad. Vínculos profundos a pestañas sin identificador de entidad siga navegando a la pestaña pero no puede proporcionar el identificador de subentidad a la pestaña.

Use este formato para un vínculo profundo que puede usar en una tarjeta de bot, conector o extensión de mensajería:

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

Los parámetros de consulta son los siguientes:

* `appId`&emsp;El identificador del manifiesto; por ejemplo, "fe4a8eba-2a31-4737-8E33-e5fae6fee194"
* `entityId`&emsp;IDENTIFICADOR del elemento de la ficha, que se ha proporcionado al [configurar la pestaña](~/tabs/how-to/create-tab-pages/configuration-page.md); por ejemplo, "tasklist123"
* `entityWebUrl`o `subEntityWebUrl` &emsp; un campo opcional con una dirección URL de reserva para usar si el cliente no admite la representación de la pestaña; por ejemplo, " https://tasklist.example.com/123 " o " https://tasklist.example.com/list123/task456 "
* `entityLabel`o bien `subEntityLabel` &emsp; , una etiqueta para el elemento de la ficha, para utilizarla al mostrar el vínculo en profundidad; por ejemplo, "lista de tareas 123" o "tarea 456"
* `context`&emsp;Un objeto JSON que contiene los siguientes campos:
  * `subEntityId`&emsp;IDENTIFICADOR del elemento _dentro_ de la pestaña; por ejemplo, "task456"
  * `channelId`&emsp;El identificador de canal de Microsoft Teams (disponible desde el [contexto](~/tabs/how-to/access-teams-context.md)de la pestaña; por ejemplo, "19: cbe3683f25094106b826c9cada3afbe0@thread. Skype". Esta propiedad solo está disponible en pestañas configurables con un ámbito de "Team". No está disponible en las pestañas estáticas, que tienen un ámbito de "personal".

Ejemplos:

* Vincular a una pestaña configurable en sí: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* Vínculo a un elemento de tarea dentro de la pestaña configurable: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* Vínculo a una pestaña estática en sí: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`
* Vínculo a un elemento de tarea dentro de la pestaña estática: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`

> [!IMPORTANT]
> Asegúrese de que todos los parámetros de consulta están codificados con URI correctamente. Por motivos de legibilidad, los ejemplos anteriores no lo son, pero debe hacerlo. Con el último ejemplo:
> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consuming-a-deep-link-from-a-tab"></a>Utilizar un vínculo profundo desde una pestaña

Cuando se navega a un vínculo profundo, Microsoft Teams simplemente se desplaza a la pestaña y proporciona un mecanismo a través de la biblioteca de JavaScript de Microsoft Teams para recuperar el identificador de subentidad (si existe).

La [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) llamada devuelve un contexto que incluye el `subEntityId` campo si la pestaña se navegó a través de un vínculo profundo.

## <a name="deep-linking-from-your-tab"></a>Vínculo profundo desde la pestaña

Puede hacer un vínculo profundo a contenido en Teams desde la pestaña. Esto es útil si la pestaña tiene que vincular a otro contenido de Microsoft Teams, como un canal, un mensaje, otra pestaña o incluso para abrir un cuadro de diálogo de programación. Para desencadenar un vínculo profundo desde la pestaña debe llamar a:

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

Esto le permitirá navegar hasta la dirección URL correcta o desencadenar una acción de cliente como abrir un cuadro de diálogo de programación o instalación de aplicaciones. Ejemplo:

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a>Vinculación profunda a un chat

Puede crear vínculos profundos a chats privados entre usuarios si especifica el conjunto de participantes. Si no existe un chat con los participantes especificados, el vínculo navegará al usuario hacia un chat nuevo vacío. Los chats nuevos se crearán en el estado de borrador hasta que el usuario envíe el primer mensaje. Opcionalmente, puede especificar el nombre del chat (si todavía no existe), junto con el texto que debe insertarse en el cuadro de redacción del usuario. Esta característica se puede considerar como un método abreviado para que el usuario realice la acción manual de navegar o crear el chat y, a continuación, escribir el mensaje.

Como ejemplo de uso de ejemplo, si va a devolver un perfil de usuario de Office 365 de su bot como tarjeta, este vínculo profundo puede permitir al usuario chatear fácilmente con esa persona.

### <a name="generating-a-deep-link-to-a-chat"></a>Creación de un vínculo profundo a un chat

Use este formato para un vínculo profundo que puede usar en una tarjeta de bot, conector o extensión de mensajería:

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

Ejemplo: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

Los parámetros de consulta son los siguientes:

* `users`&emsp;La lista de identificadores de usuario separados por comas que representan los participantes del chat. El usuario que realiza la acción siempre se incluye como un participante. Actualmente, el campo de identificador de usuario solo admite la UserPrincipalName de Azure AD (normalmente una dirección de correo electrónico).
* `topicName`&emsp;Un campo opcional para el nombre para mostrar de un chat, en el caso de un chat con 3 o más usuarios. Si no se especifica este campo, el nombre para mostrar del chat se basará en los nombres de los participantes.
* `message`&emsp;Un campo opcional para el texto del mensaje que desea insertar en el cuadro de redacción del usuario actual mientras el chat está en estado de borrador.

Para usar este vínculo profundo con el bot, puede especificarlo como destino de dirección URL en el botón de la tarjeta o en acción de puntear a través del `openUrl` tipo de acción.

## <a name="linking-to-the-scheduling-dialog"></a>Vinculación al cuadro de diálogo programación

> [!Note]
> Esta característica se encuentra actualmente en versión preliminar para desarrolladores.

Puede crear vínculos profundos al cuadro de diálogo de programación integrada del cliente de Microsoft Teams. Esto es especialmente útil si la aplicación ayuda al usuario a completar tareas relacionadas con el calendario o la programación.

### <a name="generating-a-deep-link-to-the-scheduling-dialog"></a>Generar un vínculo profundo al cuadro de diálogo de programación

Use este formato para un vínculo profundo que puede usar en una tarjeta de bot, conector o extensión de mensajería: `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

Ejemplo: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

Los parámetros de consulta son los siguientes:

* `attendees`&emsp;La lista opcional de identificadores de usuario separados por comas que representa a los asistentes de la reunión. El usuario que realiza la acción es el organizador de la reunión. Actualmente, el campo de identificador de usuario solo admite la UserPrincipalName de Azure AD (normalmente una dirección de correo electrónico).
* `startTime`&emsp;La hora de inicio opcional del evento. Debe estar en [formato ISO 8601 largo](https://en.wikipedia.org/wiki/ISO_8601), por ejemplo, "2018-03-12T23:55:25 + 02:00".
* `endTime`&emsp;La hora de finalización opcional del evento, también en formato ISO 8601.
* `subject`&emsp;Un campo opcional para el asunto de la reunión.
* `content`&emsp;Un campo opcional para el campo detalles de la reunión.

Actualmente, no se admite la especificación de la ubicación. Al generar las horas de inicio y finalización, asegúrese de especificar el desplazamiento de UTC (zonas horarias).

Para usar este vínculo profundo con el bot, puede especificarlo como destino de dirección URL en el botón de la tarjeta o en acción de puntear a través del `openUrl` tipo de acción.

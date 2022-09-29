---
title: Crear vínculos profundos
description: En este artículo, aprenderá a crear vínculos profundos y a navegar por dichos vínculos en las aplicaciones de Microsoft Teams con pestañas.
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: b02a29b74204e9ef8f61633642bd42cd178c8350
ms.sourcegitcommit: c74e1e12175969c75e112a580949f96d2610c24e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/29/2022
ms.locfileid: "68160723"
---
# <a name="create-deep-links"></a>Crear vínculos profundos

Los vínculos profundos son un mecanismo de navegación que puede usar para conectar a los usuarios con información y características dentro de Teams y las aplicaciones de Teams. Los escenarios en los que la creación de vínculos profundos es útil son los siguientes:

* Llevar al usuario al contenido dentro de una de las pestañas de la aplicación. Por ejemplo, la aplicación puede tener un bot que envía mensajes que notifican al usuario de una actividad importante. Cuando el usuario pulsa en la notificación, el vínculo profundo navega a la pestaña para que el usuario pueda ver más detalles sobre la actividad.
* La aplicación automatiza o simplifica determinadas tareas de usuario. Puede crear un chat o programar una reunión rellenando previamente los vínculos profundos con los parámetros necesarios. Evita la necesidad de que los usuarios escriban manualmente la información.

El SDK de cliente de JavaScript de Microsoft Teams (TeamsJS) simplifica el proceso de navegación. Para muchos escenarios, como navegar a contenido e información dentro de la pestaña o iniciar un cuadro de diálogo de chat. El SDK proporciona API con tipo que proporcionan una experiencia mejorada y pueden reemplazar el uso de vínculos profundos. Estas API se recomiendan para las aplicaciones de Teams que se pueden ejecutar en otros hosts (Outlook, Office), ya que también proporcionan una manera de comprobar que ese host admite la funcionalidad que se usa. En las secciones siguientes se muestra información sobre la vinculación en profundidad, pero también se resalta cómo han cambiado los escenarios que solían requerirla con la versión v2 de TeamsJS.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

> [!NOTE]
> El comportamiento de los vínculos profundos depende de una serie de factores. En la siguiente lista se describe el comportamiento de los vínculos profundos en entidades de Teams.
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
> ✔ Vínculo pegado en la conversación de chat general: navega directamente a la dirección URL del vínculo profundo.
>
>
>El comportamiento de navegación de una aplicación de Teams extendida en Microsoft 365 (Outlook/Office) depende de dos factores:
>
> * Destino al que apunta el vínculo profundo.
> * Host en el que se ejecuta la aplicación de Teams.
>
> Si la aplicación Teams se ejecuta dentro del host donde se dirige el vínculo profundo, la aplicación se abrirá directamente dentro del host. Sin embargo, si la aplicación de Teams se ejecuta en un host diferente del destino del vínculo profundo, la aplicación se abrirá primero en el explorador.

## <a name="deep-link-to-your-tab"></a>Vinculación profunda a la pestaña

Puede crear vínculos profundos a entidades en las aplicaciones de Teams. Se usa para crear vínculos que naveguen al contenido y a la información dentro de la pestaña. Por ejemplo, si la pestaña contiene una lista de tareas, los miembros del equipo pueden crear y compartir vínculos a tareas individuales. Al seleccionar el vínculo, navega a la pestaña que se centra en el elemento específico.

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

Para implementar, agregue una acción **copiar vínculo** a cada elemento, de la manera que mejor se adapte a su interfaz de usuario. Cuando el usuario realiza esta acción, se llama a [pages.shareDeepLink()](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest#@microsoft-teams-js-pages-sharedeeplink&preserve-view=true) para mostrar un cuadro de diálogo que contiene un vínculo que el usuario puede copiar en el portapapeles. Cuando realice esta llamada, pase un id. para el elemento. Se devuelve en [contexto](~/tabs/how-to/access-teams-context.md) cuando se sigue el vínculo y se vuelve a cargar la pestaña.

```javascript
pages.shareDeepLink({ subPageId: <subPageId>, subPageLabel: <subPageLabel>, subPageWebUrl: <subPageWebUrl> })
```

Tendrá que reemplazar los campos por la información adecuada:

* `subPageId`: identificador único del elemento de la pestaña al que está vinculando en profundidad.
* `subPageLabel`: etiqueta del elemento que se va a usar para mostrar el vínculo profundo.
* `subPageWebUrl`: dirección URL de reserva que se usará si el cliente no puede representar la página.

Para obtener más información, consulte [pages.shareDeepLink()](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest#@microsoft-teams-js-pages-sharedeeplink&preserve-view=true).

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

Para implementar esto, agregue una acción **copiar vínculo** a cada elemento, de la manera que mejor se adapte a su interfaz de usuario. Cuando el usuario realiza esta acción, se llama a `shareDeepLink()` para mostrar un cuadro de diálogo que contiene un vínculo que el usuario puede copiar en el portapapeles. Al realizar esta llamada, también pasa un identificador para el elemento, que obtiene en el [contexto](~/tabs/how-to/access-teams-context.md) cuando se sigue el vínculo y se vuelve a cargar la pestaña.

```javascript
microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })
```

Tendrá que reemplazar los campos por la información adecuada:

* `subEntityId`: identificador único del elemento de la pestaña al que está vinculando en profundidad.
* `subEntityLabel`: etiqueta del elemento que se va a usar para mostrar el vínculo profundo.
* `subEntityWebUrl`: campo opcional con una dirección URL de reserva que se usará si el cliente no admite la representación de la pestaña.

---

Como alternativa, también puede generar vínculos profundos mediante programación, con el formato especificado más adelante en este artículo. Puede usar vínculos profundos en mensajes de [bot](~/bots/what-are-bots.md) y [conector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) que informan a los usuarios sobre los cambios en la pestaña o en los elementos que contiene.

> [!NOTE]
> Este vínculo profundo es diferente de los vínculos proporcionados por el elemento de menú **Copiar vínculo a la pestaña**, que solo genera un vínculo profundo que apunta a esta pestaña.

>[!IMPORTANT]
> Actualmente, shareDeepLink no funciona en plataformas móviles.

### <a name="consume-a-deep-link-from-a-tab"></a>Consumir un vínculo profundo desde una pestaña

Al navegar a un vínculo profundo, Microsoft Teams simplemente navega a la pestaña y proporciona un mecanismo a través de la biblioteca JavaScript de Teams para recuperar el identificador de la subentidad si existe.

La llamada [`app.getContext()`](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-getcontext&preserve-view=true) (`microsoftTeams.getContext()`) en TeamsJS v1) devuelve una promesa que se resolverá con el contexto que incluye la propiedad `subPageId` (subEntityId para TeamsJS v1) si la pestaña se navega a través de un vínculo profundo. Para obtener más información, vea [la interfaz PageInfo](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-pageinfo&preserve-view=true).

### <a name="generate-a-deep-link-to-your-tab"></a>Generar un vínculo profundo a la pestaña

Aunque se recomienda usar `shareDeepLink()` para generar un vínculo profundo a la pestaña, también es posible crear uno manualmente.

> [!NOTE]
>
> * Las pestañas personales tienen un ámbito `personal`, mientras que las pestañas de canal y grupo usan ámbitos `team` o `group`. Los dos tipos de pestaña tienen una sintaxis ligeramente diferente, ya que solo la pestaña configurable tiene una propiedad `channel` asociada a su objeto de contexto. Para obtener más información sobre los ámbitos de pestaña, vea la referencia del [manifiesto](~/resources/schema/manifest-schema.md).
> * Los vínculos profundos solo funcionan correctamente si la pestaña se configuró mediante la biblioteca v0.4 o posterior y por ello tiene un identificador de entidad. Los vínculos profundos a pestañas sin identificadores de entidad siguen navegando a la pestaña, pero no pueden proporcionar el identificador de subentidad a la pestaña.

Use el formato siguiente para un vínculo profundo que puede usar en un bot, conector o tarjeta de extensión de mensajería:

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> Si el bot envía un mensaje que contiene un `TextBlock` con un vínculo profundo, se abre una nueva pestaña del explorador cuando el usuario selecciona el vínculo. Esto sucede en Chrome y en la aplicación de escritorio de Teams, ejecutados en Linux.
> Si el bot envía la misma dirección URL de vínculo profundo a un `Action.OpenUrl`, la pestaña Teams se abre en la pestaña actual del explorador cuando el usuario selecciona el vínculo. No se abre una nueva pestaña del explorador.

<!--- TBD: Edit this article.
* Admonitions/alerts seem to be overused. 
* An important alert at the end of this table does not make sense. Also, it has a code snippet inside it.
* List items in the table are not formatted well in output.
* Some headings use -ing verbs.
* Example values and some URLs should be in backticks and not emphasized.
* Codeblock are missing language.
* Check for markdownlint errors.
* Table with just a row isn't really needed. Provide the content without tabulating it.
--->

Los parámetros de consulta son:

| Nombre del parámetro | Descripción | Ejemplo |
|:------------|:--------------|:---------------------|
| `appId`&emsp; | Identificador del Centro de administración de Teams. |fe4a8eba-2a31-4737-8e33-e5fae6fee194|
| `entityId`&emsp; | Id. del elemento en la pestaña, que proporcionó al [configurar la pestaña](~/tabs/how-to/create-tab-pages/configuration-page.md). Al generar una dirección URL para la vinculación en profundidad, siga usando entityID como nombre de parámetro en la dirección URL. Al configurar la pestaña, el objeto de contexto hace referencia al entityID como {page.id}. |Lista de tareas123|
| `entityWebUrl` o `subEntityWebUrl`&emsp; | Un campo opcional con una dirección URL de reserva que se usará si el cliente no admite la representación de la pestaña. | `https://tasklist.example.com/123` o `https://tasklist.example.com/list123/task456` |
| `entityLabel` o `subEntityLabel`&emsp; | Etiqueta del elemento de la pestaña que se va a usar al mostrar el vínculo profundo. | Lista de tareas 123 o "Tarea 456 |
| `context.subEntityId`&emsp; | Identificador del elemento dentro de la pestaña. Al generar una dirección URL para la vinculación en profundidad, siga usando subEntityId como nombre de parámetro en la dirección URL. Al configurar la pestaña, el objeto de contexto hace referencia a subEntityID como subPageID. |Tarea 456 |
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

## <a name="navigation-from-your-tab"></a>Navegación desde la pestaña

Puede navegar hasta el contenido de Teams desde la pestaña mediante TeamsJS o vínculos profundos. Esto es útil si la pestaña necesita vincular a otro contenido de Teams, como un canal, un mensaje, otra pestaña o incluso para abrir un cuadro de diálogo de programación. Anteriormente, la navegación podría haber requerido un vínculo profundo, pero ahora se puede realizar en muchas instancias mediante el SDK. En las secciones siguientes se muestran ambos métodos, pero siempre que sea posible se recomienda el uso de las funcionalidades tipeadas del SDK.

Una de las ventajas de usar TeamsJS, especialmente para las aplicaciones Teams que se pueden ejecutar en otros hosts (Outlook y Office), es que es posible comprobar que el host admite la funcionalidad que intenta usar. Para comprobar la compatibilidad de un host con una funcionalidad, puede usar la función `isSupported()` asociada al espacio de nombres de la API. La versión preliminar v2 del SDK de TeamsJS organiza las API en funcionalidades por medio de espacios de nombres. Por ejemplo, antes de usar una API en el espacio de nombres `pages`, puede comprobar el valor booleano devuelto desde `pages.isSupported()` y realizar la acción adecuada en el contexto de la interfaz de usuario de aplicaciones y aplicaciones.  

Para obtener información adicional sobre las funcionalidades y las API en TeamsJS, consulte [Creación de pestañas y otras experiencias hospedadas con el SDK de cliente de JavaScript de Microsoft Teams](~/tabs/how-to/using-teams-client-sdk.md#apis-organized-into-capabilities).

### <a name="navigate-within-your-app"></a>Navegar dentro de la aplicación

Es posible navegar dentro de una aplicación mediante TeamsJS. En el código siguiente se muestra cómo navegar a una entidad específica dentro de la aplicación de Teams.

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

Puede desencadenar una navegación desde la pestaña mediante la función [pages.navigateToApp()](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest#@microsoft-teams-js-pages-navigatetoapp&preserve-view=true) como se muestra en el código siguiente:

```javascript
if (pages.isSupported()) {
  const navPromise = pages.navigateToApp({ appId: <appId>, pageId: <pageId>, webUrl: <webUrl>, subPageId: <subPageId>, channelId:<channelId>});
  navPromise.
     then((result) => {/*Successful navigation*/}).
     catch((error) => {/*Failed navigation*/});
}
else { /* handle case where capability isn't supported */ }
```

Para obtener más información sobre el uso de la funcionalidad páginas, consulte [pages.navigateToApp()](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest#@microsoft-teams-js-pages-navigatetoapp&preserve-view=true) y el espacio de nombres [páginas](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest&preserve-view=true) para ver otras opciones de navegación. Si es necesario, también es posible abrir directamente un vínculo profundo mediante la función [app.openLink().](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-openlink&preserve-view=true)

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

Para desencadenar un vínculo profundo desde la pestaña, llame a:

```javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

---

### <a name="open-a-scheduling-dialog"></a>Abrir un cuadro de diálogo

> [!NOTE]
> Para abrir el cuadro de diálogo de programación en Teams, los desarrolladores deben seguir usando el método original basado en la dirección URL de vínculo profundo, ya que Teams aún no admite la funcionalidad de calendario.

Para obtener más información sobre cómo trabajar con el calendario, consulte el espacio de nombres del [calendario](/javascript/api/@microsoft/teams-js/calendar?view=msteams-client-js-latest&preserve-view=true) en la documentación de referencia de la API.

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```javascript
// Open a scheduling dialog from your tab
if(calendar.isSupported()) {
   const calendarPromise = calendar.composeMeeting({
      attendees: ["joe@contoso.com", "bob@contoso.com"],
      content: "test content",
      endTime: "2018-10-24T10:30:00-07:00",
      startTime: "2018-10-24T10:00:00-07:00",
      subject: "test subject"});
   calendarPromise.
      then((result) => {/*Successful operation*/}).
      catch((error) => {/*Unsuccessful operation*/});
}
else { /* handle case where capability isn't supported */ }
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");
```

---

De forma alternativa, puede crear manualmente vínculos profundos al diálogo de programación integrado de Teams.

#### <a name="generate-a-deep-link-to-the-scheduling-dialog"></a>Generar un vínculo profundo al cuadro de diálogo de programación

Aunque se recomienda usar las API tipadas de TeamsJS, es posible crear manualmente vínculos profundos al cuadro de diálogo de programación integrado Teams. Use el formato siguiente para un vínculo profundo que puede usar en un bot, conector o tarjeta de extensión de mensajería: `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

Ejemplo: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

> [!NOTE]
> Los parámetros de búsqueda no admiten la señal `+` en lugar de espacios en blanco (``). Asegúrese de que el código de codificación uri devuelve `%20` para los espacios, por ejemplo, `?subject=test%20subject` es correcto, pero `?subject=test+subject` es incorrecto.

Los parámetros de consulta son:

* `attendees`: lista opcional separada por comas de identificadores de usuario que representan a los asistentes a la reunión. El usuario que realiza la acción es el organizador de la reunión. Actualmente, el campo Id. de usuario solo admite el UserPrincipalName de Azure AD, normalmente una dirección de correo electrónico.
* `startTime`: la hora de inicio opcional del evento. Debe tener [formato ISO 8601 largo](https://en.wikipedia.org/wiki/ISO_8601), por ejemplo, *2018-03-12T23:55:25+02:00*.
* `endTime`: la hora de finalización opcional del evento, también en formato ISO 8601.
* `subject`: un campo opcional para el asunto de la reunión.
* `content`: un campo opcional para el campo de detalles de la reunión.

> [!NOTE]
> Currently, specifying the location isn't supported. You must specify the UTC offset, it means time zones when generating your start and end times.

Para usar este vínculo profundo con el bot, puede especificarlo como destino de la dirección URL en el botón de la tarjeta o pulsar la acción a través del tipo de acción `openUrl`.

### <a name="open-an-app-install-dialog"></a>Abrir un cuadro de diálogo de instalación de aplicaciones

Puede abrir un cuadro de diálogo de instalación de la aplicación desde la aplicación de Teams, como se muestra en el código siguiente.

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```javascript
// Open an app install dialog from your tab
if(appInstallDialog.isSupported()) {
    const dialogPromise = appInstallDialog.openAppInstallDialog({ appId: <appId>});
    dialogPromise.
      then((result) => {/*Successful operation*/}).
      catch((error) => {/*Unsuccessful operation*/});
}
else { /* handle case where capability isn't supported */ }
```

Para obtener más información sobre el cuadro de diálogo de instalación, consulte la función [appInstallDialog.openAppInstallDialog()](/javascript/api/@microsoft/teams-js/appinstalldialog?view=msteams-client-js-latest#@microsoft-teams-js-appinstalldialog-openappinstalldialog&preserve-view=true) en la documentación de referencia de la API.

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```javascript
// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

---

### <a name="navigate-to-a-chat"></a>Navegar a un chat

Puede crear vínculos profundos a chats privados entre usuarios especificando el conjunto de participantes. Si no existe un chat con los participantes especificados, el vínculo lleva al usuario a un nuevo chat vacío. Los chats nuevos se crean en estado de borrador hasta que el usuario envía el primer mensaje. De lo contrario, puede especificar el nombre del chat si aún no existe, junto con el texto que se debe insertar en el cuadro de redacción del usuario. Puede considerar esta característica como un acceso directo para que el usuario realice la acción manual de ir al chat o crearlo y, después, escribir el mensaje.

Como ejemplo de caso de uso, si va a devolver un perfil de usuario de Office 365 desde el bot como una tarjeta, este vínculo profundo puede permitir que el usuario chatee fácilmente con esa persona. En el ejemplo siguiente se muestra cómo abrir un mensaje de chat a un grupo de participantes con un mensaje inicial.

```javascript
if(chat.isSupported()) {
    const chatPromise = chat.openGroupChat({ users: ["joe@contoso.com","bob@contoso.com"], topic: "Prep For Meeting Tomorrow", message: "Hi folks kicking off chat about our meeting tomorrow"});
    chatPromise.
      then((result) => {/*Successful operation*/}).
      catch((error) => {/*Unsuccessful operation*/});
}
else { /* handle case where capability isn't supported */ }
```

Aunque se recomienda el uso de las API tipeadas, también puede usar el siguiente formato para un vínculo profundo creado manualmente que puede usar en un bot, conector o tarjeta de extensión de mensaje:

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

Ejemplo: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

Los parámetros de consulta son:

* `users`: lista separada por comas de identificadores de usuario que representan a los participantes del chat. El usuario que realiza la acción siempre se incluye como participante. Actualmente, el campo Id. de usuario admite el UserPrincipalName de Microsoft Azure Active Directory (Azure AD), como solo una dirección de correo electrónico.
* `topicName`: un campo opcional para el nombre para mostrar del chat, si un chat tiene tres o más usuarios. Si no se especifica este campo, el nombre para mostrar del chat se basa en los nombres de los participantes.
* `message`: un campo opcional para el texto del mensaje que quiere insertar en el cuadro de redacción del usuario actual mientras el chat está en un estado de borrador.

Para usar este vínculo profundo con el bot, puede especificarlo como destino de la dirección URL en el botón de la tarjeta o pulsar la acción a través del tipo de acción `openUrl`.

### <a name="generate-deep-links-to-channel-conversation"></a>Generar vínculos profundos a la conversación del canal

Use este formato de vínculo profundo para navegar a una conversación determinada dentro de la conversación del canal:

`https://teams.microsoft.com/l/message/<channelId>/<parentMessageId>?tenantId=<tenantId>&groupId=<groupId>&parentMessageId=<parentMessageId>&teamName=<teamName>&channelName=<channelName>&createdTime=<createdTime>`

Ejemplo: `https://teams.microsoft.com/l/message/<channelId>/1648741500652?tenantId=<tenantId>&groupId=<groupId>&parentMessageId=1648741500652&teamName=<teamName>&channelName=<channelName>&createdTime=1648741500652`

Los parámetros de consulta son:

* `channelId`: id. de canal de la conversación. Por ejemplo, `19:3997a8734ee5432bb9cdedb7c432ae7d@thread.tacv2`.
* `tenantId`: identificador de inquilino como `0d9b645f-597b-41f0-a2a3-ef103fbd91bb`.
* `groupId`: id. de grupo del archivo. Por ejemplo, `3606f714-ec2e-41b3-9ad1-6afb331bd35d`.
* `parentMessageId`: id. de mensaje primario de la conversación.
* `teamName`: nombre del equipo.
* `channelName`: nombre del canal del equipo.

> [!NOTE]
> Puede ver `channelId` y `groupId` en la dirección URL del canal.

### <a name="generate-deep-links-to-file-in-channel"></a>Generar vínculos profundos al archivo en el canal

El siguiente formato de vínculo profundo se puede usar en un bot, conector o tarjeta de extensión de mensajería:

`https://teams.microsoft.com/l/file/<fileId>?tenantId=<tenantId>&fileType=<fileType>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadId>&groupId=<groupId>`

Los parámetros de consulta son:

* `fileId`: Unique file ID from Sharepoint Online, also known as `sourcedoc`. For example,`1FA202A5-3762-4F10-B550-C04F81F6ACBD`.
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

#### <a name="serialization-of-this-object"></a>Serialización de este objeto

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

Cree vínculos profundos para la aplicación después de que la aplicación aparezca en la tienda de Teams. Para crear un vínculo para iniciar Teams, anexe el identificador de aplicación a la siguiente dirección URL: `https://teams.microsoft.com/l/app/<your-app-id>`. Aparece un cuadro de diálogo para instalar o abrir la aplicación.

> [!NOTE]
> Si la aplicación se ha aprobado para la plataforma móvil, puede vincularla en profundidad a una aplicación en el móvil. Además, se requiere el id. de equipo de Apple App Store Connect para que el vínculo profundo funcione en Teams-iOS. Para obtener más información, consulte [cómo actualizar el id. de equipo de Apple App Store Connect](../deploy-and-publish/appsource/prepare/update-apple-store-team-connect-id.md).

### <a name="deep-linking-for-sharepoint-framework-tabs"></a>Vinculación en profundidad para pestañas de SharePoint Framework

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

## <a name="navigate-to-an-audio-or-audio-video-call"></a>Vinculación profunda a una llamada de audio o de audio y vídeo

Puede crear vínculos profundos para invocar solo audio o llamadas de audio y vídeo a un único usuario o grupo de usuarios, especificando el tipo de llamada y los participantes. Antes de realizar la llamada, el cliente de Teams solicita una confirmación para realizar la llamada. En el caso de una llamada de grupo, puede llamar a un conjunto de usuarios de VoIP y a un conjunto de usuarios RTC en la misma invocación de vínculo profundo.

En el caso de una videollamada, el cliente pedirá confirmación y activará el vídeo del autor de la llamada para la llamada. El receptor de la llamada tiene la opción de responder solo a través de audio o con audio y vídeo, a través de la ventana de notificación de llamadas de Teams.

> [!NOTE]
> Este vínculo profundo no se puede usar para invocar una reunión.

En el código siguiente se muestra cómo usar el SDK de TeamsJS para iniciar una llamada:

```javascript
if(call.isSupported()) {
    const callPromise = call.startCall({ targets: ["joe@contoso.com","bob@contoso.com","4:9876543210"], requestedModalities: [call.CallModalities.Audio], source: "demoApp"});
    callPromise.
      then((result) => {/*Successful operation*/}).
      catch((error) => {/*Unsuccessful operation*/});
}
else { /* handle case where capability isn't supported */ }

```

## <a name="generate-a-deep-link-to-share-content-to-stage-in-meetings"></a>Generación de un vínculo profundo para compartir contenido para realizar una fase en las reuniones

También puede generar un vínculo profundo para [compartir la aplicación para realizar la fase](~/apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md#share-entire-app-to-stage) e iniciar o unirse a una reunión.

> [!Note]
> El vínculo profundo para compartir contenido para la fase de reunión solo se admite en el cliente de escritorio de Teams.

Cuando un usuario que forma parte de una reunión en curso selecciona un vínculo profundo en una aplicación, la aplicación se comparte en la fase y aparece una ventana emergente de permisos. Los usuarios pueden conceder permisos a los participantes, como la edición conjunta de un documento o la colaboración con una aplicación.

:::image type="content" source="../../assets/images/intergrate-with-teams/screenshot-of-pop-up-permission.png" alt-text="La captura de pantalla es un ejemplo que muestra una ventana emergente de permisos.":::

Cuando el usuario no está en una reunión, se redirige al usuario al calendario de Teams, donde el usuario necesita unirse a una reunión o una reunión instantánea (Reunirse ahora).

:::image type="content" source="../../assets/images/intergrate-with-teams/Instant-meetnow-pop-up.png" alt-text="La captura de pantalla es un ejemplo que muestra una ventana emergente cuando no hay ninguna reunión en curso.":::

Una vez que el usuario inicia una reunión instantánea (Reunirse ahora), puede agregar participantes e interactuar con la aplicación.

:::image type="content" source="../../assets/images/intergrate-with-teams/Screenshot-ofmeet-now-option-pop-up.png" alt-text="La captura de pantalla es un ejemplo que muestra una opción para agregar participantes y cómo interactuar con la aplicación.":::

Para agregar un vínculo profundo para compartir contenido en el escenario, debe tener un contexto de aplicación. El contexto de la aplicación permite al cliente de Teams capturar el manifiesto de la aplicación y comprobar si es posible el uso compartido en el escenario. A continuación se muestra un ejemplo de contexto de aplicación.

* `{ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9ec80a73-1d41-4bcb-8190-4b9eA9e29fbb" , "useMeetNow": false }`

Los parámetros de consulta para el contexto de la aplicación son:

* `appID`: es el identificador que se puede obtener del manifiesto de la aplicación.
* `appSharingUrl`: la dirección URL que debe compartirse en el escenario debe ser un dominio válido definido en el manifiesto de la aplicación. Si la dirección URL no es un dominio válido, aparecerá un cuadro de diálogo de error para proporcionar al usuario una descripción del error.
* `useMeetNow`: incluye un parámetro booleano que puede ser true o false.
  * **True** : cuando el `UseMeetNow` valor es true y no hay ninguna reunión en curso, se iniciará una nueva reunión meet now. Cuando haya una reunión en curso, se omitirá este valor.

  * **False** : el valor predeterminado de `UseMeetNow` es false, lo que significa que cuando se comparte un vínculo profundo en la fase y no hay ninguna reunión en curso, aparecerá un elemento emergente de calendario. Cuando hay una reunión en curso, el uso compartido se puede realizar directamente.

Asegúrese de que todos los parámetros de consulta estén correctamente codificados mediante URI y que el contexto de la aplicación tenga que codificarse dos veces en la dirección URL final. A continuación, se muestra un ejemplo.

```json
var appContext= JSON.stringify({ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9cc80a93-1d41-4bcb-8170-4b9ec9e29fbb", "useMeetNow":false })
var encodedContext = encodeURIComponent(appcontext).replace(/'/g,"%27").replace(/"/g,"%22")
var encodedAppContext = encodeURIComponent(encodedContext).replace(/'/g,"%27").replace(/"/g,"%22")
```

Se puede iniciar un vínculo profundo desde la web de Teams o desde el cliente de escritorio de Teams.

* **Web de Teams** : use el siguiente formato para iniciar un vínculo profundo desde la web de Teams para compartir contenido en el escenario.

    `https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`

    Ejemplo: `https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |Vínculo profundo|Formato|Ejemplo|
    |---------|---------|---------|
    |Para compartir la aplicación y abrir el calendario de Teams, cuando UseMeeetNow es "false", es el valor predeterminado.|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|
    |Para compartir la aplicación e iniciar una reunión instantánea, cuando UseMeeetNow es "true".|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

* **Cliente de escritorio de equipo** : use el siguiente formato para iniciar un vínculo profundo desde el cliente de escritorio de Teams para compartir contenido en el escenario.

    `msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`

    Ejemplo: `msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |Vínculo profundo|Formato|Ejemplo|
    |---------|---------|---------|
    |Para compartir la aplicación y abrir el calendario de Teams, cuando UseMeeetNow es "false", es el valor predeterminado.|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|
    |Para compartir la aplicación e iniciar una reunión instantánea, cuando UseMeeetNow es "true".|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

Los parámetros de consulta son:

* `deepLinkId`: cualquier identificador usado para la correlación de telemetría.
* `fqdn`: `fqdn` es un parámetro opcional, que se puede usar para cambiar a un entorno adecuado de una reunión para compartir una aplicación en el escenario. Admite escenarios en los que se produce un recurso compartido de aplicaciones específico en un entorno determinado. El valor predeterminado de es dirección URL de `fqdn` empresa y los valores posibles son `Teams.live.com` para Teams for Life, `teams.microsoft.com`o `teams.microsoft.us`.

Para compartir toda la aplicación para la fase, en el manifiesto de la aplicación, debe configurar `meetingStage` y `meetingSidePanel` , como contextos de marco, consulte [manifiesto de la aplicación](../../resources/schema/manifest-schema.md). De lo contrario, es posible que los asistentes a la reunión no puedan ver el contenido en el escenario.

## <a name="generate-a-deep-link-to-a-call"></a>Generar un vínculo profundo a una llamada

Aunque se recomienda el uso de las API tipeadas de TeamsJS, también puede usar un vínculo profundo creado manualmente para iniciar una llamada.

| Vínculo profundo | Formato | Ejemplo |
|-----------|--------|---------|
| Realizar una llamada de audio | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com` |
| Realizar una llamada de audio y vídeo | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>&withVideo=true` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withVideo=true` |
|Realizar una llamada de audio y vídeo con un origen de parámetros opcional | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>&withVideo=true&source=demoApp` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withVideo=true&source=demoApp` |  
| Realizar una llamada de audio y vídeo a una combinación de usuarios de VoIP y RTC | `https://teams.microsoft.com/l/call/0/0?users=<user1>,4:<phonenumber>` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,4:9876543210` |
  
Estos son los parámetros de consulta:

* `users`: lista separada por comas de identificadores de usuario que representan a los participantes de la llamada. Actualmente, el campo Id. de usuario admite el UserPrincipalName de Azure AD, normalmente una dirección de correo electrónico, o en el caso de una llamada RTC, admite un pstn mri 4:&lt;número de teléfono&gt;.
* `withVideo`: este es un parámetro opcional que puede usar para realizar una videollamada. Al establecer este parámetro, solo se activará la cámara del autor de la llamada. El receptor de la llamada tiene la opción de responder a través de llamada de audio o de audio y vídeo a través de la ventana de notificación de llamadas de Teams.
* `Source`: este es un parámetro opcional, que informa sobre el origen del vínculo profundo.

## <a name="code-sample"></a>Ejemplo de código

| Ejemplo de nombre | Descripción | C# |Node.js|
|-------------|-------------|------|----|
|Vínculo profundo que consume el id. de subentidad  | Aplicación de ejemplo de Teams para mostrar el vínculo profundo del chat del bot a la pestaña que consume el identificador de subentidad.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/csharp)|[Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/nodejs)|

## <a name="see-also"></a>Consulte también

* [Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)
* [Moodle LMS](~/resources/moodleinstructions.md)

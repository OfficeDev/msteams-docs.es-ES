---
title: Referencia de esquema de manifiesto
description: Describe el esquema del manifiesto para Microsoft Teams
keywords: esquema del manifiesto de Microsoft Teams
author: laujan
ms.author: lajanuar
ms.openlocfilehash: c66add190b0492170acf9756980ee16fb1fdf1fd
ms.sourcegitcommit: 5f1d6c12d80d48f403b73586f68bacf15785c855
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/30/2020
ms.locfileid: "49739059"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>Referencia: esquema de manifiesto para Microsoft Teams

El manifiesto de Microsoft Teams describe cómo se integra la aplicación en el producto de Microsoft Teams. El manifiesto debe cumplir el esquema hospedado en [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json) . También se admiten las versiones anteriores 1.0-1.4 (mediante "v1. x" en la dirección URL).

En el siguiente ejemplo de esquema se muestran todas las opciones de extensibilidad.

## <a name="sample-full-manifest"></a>Manifiesto completo de ejemplo

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.8",
  "version": "1.0.0",
  "id": "%MICROSOFT-APP-ID%",
  "packageName": "com.example.myapp",
  "localizationInfo": {
    "defaultLanguageTag": "en-us",
    "additionalLanguages": [
      {
        "languageTag": "es-es",
        "file": "en-us.json"
      }
    ]
  },
  "developer": {
    "name": "Publisher Name",
    "websiteUrl": "https://website.com/",
    "privacyUrl": "https://website.com/privacy",
    "termsOfUseUrl": "https://website.com/app-tos",
    "mpnId": "1234567890"
  },
  "name": {
    "short": "Name of your app (<=30 chars)",
    "full": "Full name of app, if longer than 30 characters (<=100 chars)"
  },
  "description": {
    "short": "Short description of your app (<= 80 chars)",
    "full": "Full description of your app (<= 4000 chars)"
  },
  "icons": {
    "outline": "A relative path to a transparent .png icon — 32px X 32px",
    "color": "A relative path to a full color .png icon — 192px X 192px"
  },
  "accentColor": "A valid HTML color code.",
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "scopes": [
        "team",
        "groupchat"
      ],
      "canUpdateConfiguration": true,
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel",
        "meetingStage"
      ],
      "sharePointPreviewImage": "Relative path to a tab preview image for use in SharePoint — 1024px X 768",
      "supportedSharePointHosts": [
         "sharePointFullPage",
         "sharePointWebPart"
      ]
    }
  ],
  "staticTabs": [
    {
      "entityId": "unique Id for the page entity",
      "scopes": [
        "personal"
      ],
      "context":[
        "personalTab",
        "channelTab"
        ],
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content (displayed in Teams canvas)",
      "websiteUrl": "https://contoso.com/content (displayed in web browser)",
       "searchUrl":  "https://contoso.com/content (displayed in web browser)"
    }
  ],
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "scopes": [
        "team",
        "personal",
        "groupchat"
      ],
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "supportsFiles": true,
      "supportsCalling": false,
      "supportsVideo": true,
      "commandLists": [
        {
          "scopes": [
            "team",
            "groupchat"
          ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command 2",
              "description": "Description of Command 2"
            }
          ]
        },
        {
          "scopes": [
            "personal",
            "groupchat"
          ],
          "commands": [
            {
              "title": "Personal command 1",
              "description": "Description of Personal command 1"
            },
            {
              "title": "Personal command N",
              "description": "Description of Personal command N"
            }
          ]
        }
      ]
    }
  ],
  "connectors": [
    {
      "connectorId": "GUID-FROM-CONNECTOR-DEV-PORTAL%",
      "scopes": [
        "team"
      ],
      "configurationUrl": "https://contoso.com/teamsconnector/configure"
    }
  ],
  "composeExtensions": [
    {
      "canUpdateConfiguration": true,
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "commands": [
        {
          "id": "exampleCmd1",
          "title": "Example Command",
          "type": "query",
          "context": [
            "compose",
            "commandBox"
          ],
          "description": "Command Description; e.g., Search on the web",
          "initialRun": true,
          "fetchTask": false,
          "parameters": [
            {
              "name": "keyword",
              "title": "Search keywords",
              "inputType": "text",
              "description": "Enter the keywords to search for",
              "value": "Initial value for the parameter",
              "choices": [
                {
                  "title": "Title of the choice",
                  "value": "Value of the choice"
                }
              ]
            }
          ]
        },
        {
          "id": "exampleCmd2",
          "title": "Example Command 2",
          "type": "action",
          "context": [
            "message"
          ],
          "description": "Command Description; e.g., Search for a customer",
          "initialRun": true,
          "fetchTask": true,
          "parameters": [
            {
              "name": "custinfo",
              "title": "Customer name",
              "description": "Enter a customer name",
              "inputType": "text"
            }
          ]
        }
      ],
      "taskInfo": {
        "title": "Initial dialog title",
        "width": "Dialog width",
        "height": "Dialog height",
        "url": "Initial webview URL"
      },
      "messageHandlers": [
        {
          "type": "link",
          "value": {
            "domains": [
              "mysite.someplace.com",
              "othersite.someplace.com"
            ]
          }
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "devicePermissions": [
    "geolocation",
    "media",
    "notifications",
    "midi",
    "openExternal"
  ],
  "validDomains": [
    "contoso.com",
    "mysite.someplace.com",
    "othersite.someplace.com"
  ],
  "webApplicationInfo": {
    "id": "AAD App ID",
    "resource": "Resource URL for acquiring auth token for SSO",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelSettings.Read.Group",
      "ChannelSettings.Edit.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "ChannelMessage.Read.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.Edit.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group",
      "Member.ReadWrite.Group",
      "Owner.ReadWrite.Group"
    ],
  },
  "showLoadingIndicator": false,
  "isFullScreen": false,
  "activities": {
    "activityTypes": [
      {
        "type": "taskCreated",
        "description": "Task created activity",
        "templateText": "<team member> created task <taskId> for you"
      },
      {
        "type": "userMention",
        "description": "Personal mention activity",
        "templateText": "<team member> mentioned you"
      }
    ]
  }
}
```

El esquema define las siguientes propiedades:

## <a name="schema"></a>$schema

*Opcional, pero recomendado* , String

La dirección URL de https://que hace referencia al esquema JSON del manifiesto.

## <a name="manifestversion"></a>manifestVersion

**Obligatorio** : String

La versión del esquema del manifiesto que está usando este manifiesto. Debe ser "1,7".

## <a name="version"></a>version

**Obligatorio** : String

La versión de la aplicación específica. Si actualiza algo en el manifiesto, la versión también debe incrementarse. De este modo, cuando se instale el nuevo manifiesto, se sobrescribirá el anterior y el usuario podrá disfrutar de las funciones nuevas. Si esta aplicación se envió a la tienda, el nuevo manifiesto tendrá que volver a enviarse y a validarse. A continuación, los usuarios de esta aplicación recibirán el nuevo manifiesto actualizado automáticamente en unas pocas horas, después de que se apruebe.

Si la aplicación ha solicitado un cambio de permisos, se pedirá a los usuarios que actualicen y vuelvan a dar su consentimiento a la aplicación.

Esta cadena de versión debe seguir el estándar [SemVer](http://semver.org/) (Major. Secundaria. REVISIÓN).

## <a name="id"></a>id

**Obligatorio** : identificador de aplicación de Microsoft

El identificador único generado por Microsoft para esta aplicación. Si ha registrado un bot a través de Microsoft bot Framework o la aplicación Web de su pestaña ya inicia sesión en Microsoft, debe tener ya un identificador y escribirlo aquí. De lo contrario, debe generar un nuevo identificador en el portal de registro de aplicaciones de Microsoft ([mis aplicaciones](https://apps.dev.microsoft.com)), escribirlo aquí y volver a usarlo cuando agregue un bot. Nota: Si va a enviar una actualización a su aplicación existente en AppSource, el identificador del manifiesto no debe modificarse.

## <a name="developer"></a>developer

**Obligatorio** : Object

Especifica información sobre la compañía. Para las aplicaciones enviadas a AppSource (anteriormente tienda Office), estos valores deben coincidir con la información de la entrada AppSource. Consulte nuestras [directrices de publicación](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) para obtener más información.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`name`|32 caracteres|✔|El nombre para mostrar del desarrollador.|
|`websiteUrl`|2048 caracteres|✔|La dirección URL https://al sitio web del desarrollador. Este vínculo debe llevar a los usuarios a su compañía o a la página de aterrizaje específica del producto.|
|`privacyUrl`|2048 caracteres|✔|La dirección URL de https://a la Directiva de privacidad del desarrollador.|
|`termsOfUseUrl`|2048 caracteres|✔|La dirección URL de https://a las condiciones de uso del desarrollador.|
|`mpnId`|10 caracteres| |**Opcional** IDENTIFICADOR de red de los socios de Microsoft que identifica la organización asociada que crea la aplicación.|

## <a name="name"></a>name

**Obligatorio** : Object

El nombre de la experiencia de la aplicación, que se muestra a los usuarios en la experiencia de Microsoft Teams. Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource. Los valores de `short` y `full` no deben ser iguales.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`short`|30 caracteres|✔|El nombre para mostrar corto de la aplicación.|
|`full`|100 caracteres||El nombre completo de la aplicación, que se usa si el nombre completo de la aplicación supera los 30 caracteres.|

## <a name="description"></a>description

**Obligatorio** : Object

Describe la aplicación a los usuarios. Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource.

Asegúrese de que la descripción describe con precisión su experiencia y proporciona información para ayudar a los clientes potenciales a comprender lo que hace su experiencia. También debe tener en cuenta, en la descripción completa, si se requiere uso de una cuenta externa. Los valores de `short` y `full` no deben ser iguales.  La descripción breve no debe repetirse en la descripción larga y no debe incluir ningún otro nombre de aplicación.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`short`|80 caracteres|✔|Una breve descripción de la experiencia de la aplicación, que se usa cuando el espacio es limitado.|
|`full`|4000 caracteres|✔|La descripción completa de la aplicación.|

## <a name="packagename"></a>packageName

**Opcional** : cadena

Un identificador único para esta aplicación en la notación de dominio inverso; por ejemplo, com. example. myapp. Longitud máxima: 64 caracteres.

## <a name="localizationinfo"></a>localizationInfo

**Opcional** : objeto

Permite la especificación de un idioma predeterminado, así como punteros a archivos de idioma adicionales. Consulte [localización](~/concepts/build-and-test/apps-localization.md).

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`defaultLanguageTag`||✔|La etiqueta de idioma de las cadenas en este archivo de manifiesto de nivel superior.|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

Una matriz de objetos que especifica traducciones de idioma adicionales.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`languageTag`||✔|La etiqueta de idioma de las cadenas en el archivo proporcionado.|
|`file`||✔|Una ruta de acceso relativa a un archivo. JSON que contiene las cadenas traducidas.|

## <a name="icons"></a>iconos

**Obligatorio** : Object

Iconos usados en la aplicación Microsoft Teams. Los archivos de icono deben incluirse como parte del paquete de carga. Vea [iconos](../../concepts/build-and-test/apps-package.md#app-icons) para obtener más información.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`outline`|32 x 32 píxeles|✔|Una ruta de acceso relativa a un icono de esquema PNG transparente de 32x32.|
|`color`|192 x 192 píxeles|✔|Una ruta de acceso de archivo relativa a un icono PNG 192x192 de color completo.|

## <a name="accentcolor"></a>accentColor

**Opcional** : código de color hexadecimal HTML

Color que se va a usar junto con y como fondo de los iconos de esquema.

El valor debe ser un código de color HTML válido que empiece por ' # ', por ejemplo `#4464ee` .

## <a name="configurabletabs"></a>configurableTabs

**Opcional** : matriz

Se usa cuando la experiencia de la aplicación tiene una experiencia de la pestaña de canal de equipo que requiere una configuración adicional antes de que se agregue. Las pestañas configurables solo se admiten en el ámbito de Teams (no en personal) y actualmente solo se admite **una** pestaña por aplicación.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`configurationUrl`|string|2048 caracteres|✔|Dirección URL de https://que se va a usar al configurar la pestaña.|
|`scopes`|matriz de enumeraciones|1 |✔|Actualmente, las pestañas configurables solo admiten los `team` `groupchat` ámbitos y. |
|`canUpdateConfiguration`|boolean|||Un valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de crearla. Valor predeterminado: **true**.|
|`context` |matriz de enumeraciones|6 ||El conjunto de `contextItem` ámbitos en los que se admite una pestaña. Valor predeterminado: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.|
|`sharePointPreviewImage`|string|2048||Una ruta de acceso de archivo relativa a una imagen de vista previa de pestaña para su uso en SharePoint. Tamaño 1024x768. |
|`supportedSharePointHosts`|matriz de enumeraciones|1 ||Define cómo estará disponible la pestaña en SharePoint. Las opciones son `sharePointFullPage` y `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**Opcional** : matriz

Define un conjunto de pestañas que se pueden "anclar" de forma predeterminada, sin que el usuario las agregue manualmente. Las pestañas estáticas declaradas en `personal` el ámbito siempre están ancladas a la experiencia personal de la aplicación. Actualmente no se admiten las pestañas estáticas declaradas en el `team` ámbito.

Este elemento es una matriz (un máximo de 16 elementos) con todos los elementos del tipo `object` . Este bloque solo es necesario para las soluciones que proporcionan una solución de pestaña estática.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`entityId`|string|64 caracteres|✔|Un identificador único para la entidad que muestra la pestaña.|
|`name`|string|128 caracteres|✔|El nombre para mostrar de la pestaña en la interfaz de canal.|
|`contentUrl`|string||✔|Dirección URL de https://que señala a la interfaz de usuario de la entidad que se va a mostrar en el lienzo de Microsoft Teams.|
|`websiteUrl`|string|||Dirección URL de https://para apuntar a si un usuario opta por verlo en un explorador.|
|`searchUrl`|string|||Dirección URL de https://para apuntar a las consultas de búsqueda de un usuario.|
|`scopes`|matriz de enumeraciones|1 |✔|Actualmente, las pestañas estáticas solo admiten el `personal` ámbito, lo que significa que solo se puede aprovisionar como parte de la experiencia personal.|
|`context` | matriz de enumeraciones| 2 || El conjunto de `contextItem` ámbitos en los que se admite una pestaña.|

> [!NOTE]
> Si las pestañas requieren información dependiente del contexto para mostrar contenido relevante o para iniciar un flujo de autenticación, *vea* [obtener contexto para la pestaña de Microsoft Teams](../../tabs/how-to/access-teams-context.md).

## <a name="bots"></a>transferido

**Opcional** : matriz

Define una solución de bot, junto con información opcional como propiedades de comando predeterminadas.

El elemento es una matriz (un máximo solo de un elemento, &mdash; actualmente solo se permite un bot por aplicación) con todos los elementos del tipo `object` . Este bloque solo es necesario para las soluciones que proporcionan una experiencia de bot.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`botId`|string|64 caracteres|✔|El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework. Puede ser el mismo que el [identificador de aplicación](#id)general.|
|`scopes`|matriz de enumeraciones|3 |✔|Especifica si el bot ofrece una experiencia en el contexto de un canal en un `team`, en un chat de grupo (`groupchat`) o una experiencia específica para un solo usuario (`personal`). Estas opciones no son exclusivas.|
|`needsChannelSelector`|boolean|||Describe si el bot usa una sugerencia del usuario para agregar el bot a un canal específico. Predeterminada **`false`**|
|`isNotificationOnly`|boolean|||Indica si un bot es un bot unidireccional de solo notificación o un bot de conversación. Predeterminada **`false`**|
|`supportsFiles`|boolean|||Indica si el bot es compatible con la capacidad para cargar y descargar archivos en chat personal. Predeterminada **`false`**|
|`supportsCalling`|boolean|||Un valor que indica dónde es compatible un bot con las llamadas de audio. **Importante**: esta propiedad es experimental actualmente. Es posible que las propiedades experimentales no estén completas y puedan sufrir cambios antes de que estén completamente disponibles.  Se proporciona solo para fines de prueba y exploración y no debe usarse en aplicaciones de producción. Predeterminada **`false`**|
|`supportsVideo`|boolean|||Un valor que indica dónde es compatible una llamada de vídeo con un bot. **Importante**: esta propiedad es experimental actualmente. Es posible que las propiedades experimentales no estén completas y puedan sufrir cambios antes de que estén completamente disponibles.  Se proporciona solo para fines de prueba y exploración y no debe usarse en aplicaciones de producción. Predeterminada **`false`**|

### <a name="botscommandlists"></a>bots. commandLists

Una lista opcional de comandos que el bot puede recomendar a los usuarios. El objeto es una matriz (máximo de 2 elementos) con todos los elementos de tipo `object` ; debe definir una lista de comandos independiente para cada ámbito que admita el bot. Consulte [menús de bot](~/bots/how-to/create-a-bot-commands-menu.md) para obtener más información.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`items.scopes`|matriz de enumeraciones|3 |✔|Especifica el ámbito para el que la lista de comandos es válida. Las opciones son `team`, `personal` y `groupchat`.|
|`items.commands`|matriz de objetos|10 |✔|Una matriz de comandos que el bot admite:<br>`title`: el nombre de comando del bot (cadena, 32)<br>`description`: una descripción o un ejemplo sencillo de la sintaxis del comando y su argumento (cadena, 128).|

### <a name="botscommandlistscommands"></a>bots. commandLists. Commands

|Nombre| Tipo| Tamaño máximo | Necesario | Description|
|---|---|---|---|---|
|title|string|12 |✔|El nombre del comando bot|
|description|string|128 caracteres|✔|Una descripción de texto simple o un ejemplo de la sintaxis del comando y sus argumentos.|

## <a name="connectors"></a>Connector

**Opcional** : matriz

El `connectors` bloque define un conector de Office 365 para la aplicación.

El objeto es una matriz (un máximo de 1 elemento) con todos los elementos de tipo `object` . Este bloque solo es necesario para las soluciones que proporcionan un conector.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`configurationUrl`|string|2048 caracteres|✔|Dirección URL de https://que se va a usar al configurar el conector.|
|`scopes`|matriz de enumeraciones|1 |✔|Especifica si el conector ofrece una experiencia en el contexto de un canal en un `team` o una experiencia en el ámbito de un solo usuario individual ( `personal` ). Actualmente, solo `team` se admite el ámbito.|
|`connectorId`|string|64 caracteres|✔|Un identificador único para el conector que coincide con su identificador en el [panel del programador de conectores](https://aka.ms/connectorsdashboard).|

## <a name="composeextensions"></a>composeExtensions

**Opcional** : matriz

Define una extensión de mensajería para la aplicación.

> [!NOTE]
> El nombre de la característica se cambió de "redactar extensión" a "extensión de mensajería" en noviembre de 2017, pero el nombre del manifiesto sigue siendo el mismo para que las extensiones existentes sigan funcionando.

El elemento es una matriz (un máximo de 1 elemento) con todos los elementos de tipo `object` . Este bloque solo es necesario para las soluciones que proporcionan una extensión de mensajería.

|Nombre| Tipo | Tamaño máximo | Obligatorio | Descripción|
|---|---|---|---|---|
|`botId`|string|64|✔|IDENTIFICADOR único de la aplicación de Microsoft para el bot que respalda la extensión de mensajería, tal como se registró con bot Framework. Puede ser el mismo que el identificador de aplicación general.|
|`commands`|matriz de objetos|10 |✔|matriz de comandos que admite la extensión de mensajería|
|`canUpdateConfiguration`|boolean|||Un valor que indica si el usuario puede actualizar la configuración de una extensión de mensajería. Valor predeterminado: **false**.|
|`messageHandlers`|matriz de objetos|5 ||Una lista de controladores que permiten invocar las aplicaciones cuando se cumplen ciertas condiciones. Los dominios también deben aparecer en `validDomains`|
|`messageHandlers.type`|string|||El tipo de controlador de mensajes. Debe ser `"link"`.|
|`messageHandlers.value.domains`|matriz de cadenas|||matriz de dominios para los que el controlador de mensajes de vínculo puede registrarse.|

### <a name="composeextensionscommands"></a>composeExtensions. Commands

La extensión de mensajería debe declarar uno o más comandos. Cada comando aparece en Microsoft Teams como una posible interacción desde el punto de entrada basado en la interfaz de usuario. Hay un máximo de 10 comandos.

Cada elemento de comando es un objeto con la estructura siguiente:

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`id`|string|64 caracteres|✔|IDENTIFICADOR del comando.|
|`title`|string|32 caracteres|✔|Nombre de comando fácil de tener.|
|`type`|string|64 caracteres||Tipo del comando. Uno de `query` o `action` . Valor predeterminado: **consulta**.|
|`description`|string|128 caracteres||La descripción que se muestra a los usuarios para indicar el propósito de este comando.|
|`initialRun`|boolean|||Un valor booleano que indica si el comando se debe ejecutar inicialmente sin ningún parámetro. Valor predeterminado: **false**.|
|`context`|matriz de cadenas|3 ||Define desde dónde se puede invocar la extensión de mensajes. Cualquier combinación de `compose` , `commandBox` , `message` . El valor predeterminado es `["compose","commandBox"]`.|
|`fetchTask`|boolean|||Un valor booleano que indica si debe recuperar el módulo de tarea de forma dinámica. Valor predeterminado: **false**.|
|`taskInfo`|object|||Especifique el módulo de tarea que se cargará previamente cuando se use un comando de extensión de mensajería.|
|`taskInfo.title`|string|64 caracteres||Título del cuadro de diálogo inicial.|
|`taskInfo.width`|string|||Ancho del cuadro de diálogo, ya sea un número en píxeles o un diseño predeterminado, como "Large", "Medium" o "Small".|
|`taskInfo.height`|string|||Alto del cuadro de diálogo: número en píxeles o diseño predeterminado, como "Large", "Medium" o "Small".|
|`taskInfo.url`|string|||Dirección URL de la WebView inicial.|
|`parameters`|matriz de objetos|5 elementos|✔|La lista de parámetros que toma el comando. Mínimo: 1; máximo: 5.|
|`parameters.name`|string|64 caracteres|✔|El nombre del parámetro tal y como aparece en el cliente. Se incluye en la solicitud del usuario.|
|`parameters.title`|string|32 caracteres|✔|Título descriptivo del parámetro.|
|`parameters.description`|string|128 caracteres||Cadena descriptiva que describe el propósito de este parámetro.|
|`parameters.value`|string|512 caracteres||Valor inicial del parámetro.|
|`parameters.inputType`|string|128 caracteres||Define el tipo de control que se muestra en un módulo de tareas para `fetchTask: true` . Uno de `text, textarea, number, date, time, toggle, choiceset` .|
|`parameters.choices`|matriz de objetos|10 elementos||Las opciones de opción del `choiceset` . Use sólo cuando `parameter.inputType` sea `choiceset` .|
|`parameters.choices.title`|string|128 caracteres|✔|Título de la elección.|
|`parameters.choices.value`|string|512 caracteres|✔|Valor de la elección.|

## <a name="permissions"></a>permissions

**Opcional** : matriz de cadenas

Una matriz de `string` que especifica los permisos que solicita la aplicación, lo que permite a los usuarios finales saber cómo se realizará la extensión. Las siguientes opciones no son exclusivas:

* `identity`&emsp;Requiere información de identidad del usuario
* `messageTeamMembers`&emsp;Requiere permiso para enviar mensajes directos a los miembros del equipo

Cambiar estos permisos al actualizar la aplicación hará que los usuarios repitan el proceso de consentimiento la primera vez que ejecuten la aplicación actualizada. Consulte [actualizar la aplicación](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) para obtener más información.

## <a name="devicepermissions"></a>devicePermissions

**Opcional** : matriz de cadenas

Especifica las características nativas del dispositivo de un usuario al que la aplicación puede solicitar acceso. Las opciones son:

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**Opcional**, excepto **obligatorio** donde se indica

Una lista de dominios válidos para los sitios web que la aplicación espera que se carguen dentro del cliente de Teams. Las listas de dominios pueden incluir caracteres comodín, por ejemplo `*.example.com` . Esto coincide exactamente con un segmento del dominio; Si tiene que hacer coincidir `a.b.example.com` , use `*.*.example.com` . Si la configuración de la pestaña o la interfaz de usuario de contenido debe navegar a cualquier otro dominio además del uso de la configuración de pestañas, dicho dominio debe especificarse aquí.

No obstante, **no** es necesario incluir los dominios de los proveedores de identidades que desea admitir en la aplicación. Por ejemplo, para autenticarse con un identificador de Google, es necesario redirigir a accounts.google.com, pero no se debe incluir accounts.google.com en `validDomains[]` .

Las aplicaciones de Microsoft teams que requieren sus propias direcciones URL de SharePoint para que funcionen correctamente pueden incluir "{teamsitedomain}" en su lista de dominios válidos.

> [!IMPORTANT]
> No agregue dominios que estén fuera de su control, ya sea directamente o mediante caracteres comodín. Por ejemplo, `yourapp.onmicrosoft.com` es válido, pero `*.onmicrosoft.com` no es válido.

El objeto es una matriz con todos los elementos del tipo `string` .

## <a name="webapplicationinfo"></a>webApplicationInfo

**Opcional** : objeto

Especifique el identificador de aplicación de Azure Active Directory (Azure AD) y la información de Microsoft Graph para ayudar a los usuarios a iniciar sesión sin problemas en la aplicación. Si la aplicación está registrada en Azure AD, debe proporcionar el identificador de la aplicación para que los administradores puedan revisar fácilmente los permisos y conceder el consentimiento en el centro de administración de Teams.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`id`|string|36 caracteres|✔|Identificador de la aplicación de AAD de la aplicación. Este identificador debe ser un GUID.|
|`resource`|string|2048 caracteres|✔|Dirección URL de recurso de la aplicación para adquirir el token de autenticación para el SSO.|
|`applicationPermissions`|matriz de cadenas|128 caracteres||Especificar el [consentimiento específico del recurso](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions) granular|

## <a name="showloadingindicator"></a>showLoadingIndicator

**Opcional** : Boolean

Indica si se va a mostrar el indicador de carga cuando se cargue una aplicación o pestaña. Valor predeterminado: **false**.
>[!NOTE]
>Si establece "showLoadingIndicator: true" en el manifiesto de la aplicación, para que la página se cargue correctamente, debe modificar las páginas de contenido de sus fichas y módulos de tareas según el protocolo que se describe en [Mostrar un documento de indicador de carga nativo](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) .


## <a name="isfullscreen"></a>isFullScreen

 **Opcional** : Boolean

Indicar dónde se representa una aplicación personal con o sin una barra de encabezado de pestañas. Valor predeterminado: **false**.

## <a name="activities"></a>activities

**Opcional** : objeto

Defina las propiedades que usará la aplicación para publicar en una fuente de actividad de usuario.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`activityTypes`|matriz de objetos|de 128 elementos| | Especifique los tipos de actividades que la aplicación puede publicar en la fuente de actividades de los usuarios.|

### <a name="activitiesactivitytypes"></a>Activities. activityTypes

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`type`|string|32 caracteres|✔|El tipo de notificación. *Vea a continuación*.|
|`description`|string|128 caracteres|✔|Una breve descripción de la notificación. *Vea a continuación*.|
|`templateText`|string|128 caracteres|✔|Ejemplo: "{actor} tarea creada {taskId} para usted"|

```json
{
   "activities":{
      "activityTypes":[
         {
            "type":"taskCreated",
            "description":"Task Created Activity",
            "templateText":"{actor} created task {taskId} for you"
         },
         {
            "type":"teamMention",
            "description":"Team Mention Activity",
            "templateText":"{actor} mentioned team"
         },
         {
            "type":"channelMention",
            "description":"Channel Mention Activity",
            "templateText":"{actor} mentioned channel"
         },
         {
            "type":"userMention",
            "description":"Personal Mention Activity",
            "templateText":"{actor} mentioned user"
         },
         {
            "type":"calendarForward",
            "description":"Forwarding a Calendar Event",
            "templateText":"{actor} sent user an invite on behalf of {eventOwner}"
         },
         {
            "type":"calendarForward",
            "description":"Forwarding a Calendar Event",
            "templateText":"{actor} sent user an invite on behalf of {eventOwner}"
         },
         {
            "type":"creatorTaskCreated",
            "description":"Created Task Created",
            "templateText":"The Creator created task {taskId} for you"
         }
      ]
   }
}
```

***
>
>

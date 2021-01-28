---
title: Referencia del esquema de manifiesto
description: Describe el esquema de manifiesto de Microsoft Teams
ms.topic: reference
keywords: Esquema de manifiesto de teams
author: laujan
ms.author: lajanuar
ms.openlocfilehash: 8fff56d229cc137df8356b06214893dc984396a0
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014610"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>Referencia: esquema de manifiesto para Microsoft Teams

El manifiesto de Microsoft Teams describe cómo se integra la aplicación en el producto de Microsoft Teams. El manifiesto debe cumplir con el esquema hospedado en [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json) . Las versiones anteriores 1.0-1.4 también son compatibles (con "v1.x" en la dirección URL).

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

*Cadena opcional, pero* recomendada

La https:// URL que hace referencia al esquema JSON del manifiesto.

## <a name="manifestversion"></a>manifestVersion

**Obligatorio:** cadena

La versión del esquema de manifiesto que usa este manifiesto. Debe ser "1.7".

## <a name="version"></a>version

**Obligatorio:** cadena

La versión de la aplicación específica. Si actualiza algo en el manifiesto, también debe incrementarse la versión. De este modo, cuando se instale el nuevo manifiesto, se sobrescribirá el anterior y el usuario podrá disfrutar de las funciones nuevas. Si esta aplicación se envió a la tienda, el nuevo manifiesto tendrá que volver a enviarse y validarse. A continuación, los usuarios de esta aplicación recibirán el nuevo manifiesto actualizado automáticamente en unas horas, después de su aprobación.

Si la aplicación solicita cambios en los permisos, se pedirá a los usuarios que actualicen y vuelvan a dar su consentimiento a la aplicación.

Esta cadena de versión debe seguir el [estándar semver](http://semver.org/) (MAJOR. MINOR. PATCH).

## <a name="id"></a>id

**Obligatorio:** Id. de aplicación de Microsoft

Identificador único generado por Microsoft para esta aplicación. Si ha registrado un bot a través de Microsoft Bot Framework o la aplicación web de la pestaña ya inicia sesión con Microsoft, ya debe tener un identificador y debe escribirlo aquí. De lo contrario, debe generar un nuevo identificador en el Portal de registro de aplicaciones de Microsoft[(Mis](https://apps.dev.microsoft.com)aplicaciones), escribirlo aquí y volver a usarlo cuando agregue un bot. Nota: Si vas a enviar una actualización a tu aplicación existente en AppSource, no se debe modificar el identificador del manifiesto.

## <a name="developer"></a>developer

**Obligatorio:** objeto

Especifica información sobre su empresa. Para las aplicaciones enviadas a AppSource (anteriormente Tienda Office), estos valores deben coincidir con la información de la entrada de AppSource. Vea nuestras [directrices de publicación](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) para obtener información adicional.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`name`|32 caracteres|✔|Nombre para mostrar del desarrollador.|
|`websiteUrl`|2048 caracteres|✔|La https:// url del sitio web del desarrollador. Este vínculo debe llevar a los usuarios a su empresa o página de aterrizaje específica del producto.|
|`privacyUrl`|2048 caracteres|✔|La https:// url a la directiva de privacidad del desarrollador.|
|`termsOfUseUrl`|2048 caracteres|✔|La https:// url a los términos de uso del desarrollador.|
|`mpnId`|10 caracteres| |**Opcional** El id. de Microsoft Partner Network que identifica la organización asociada que está creando la aplicación.|

## <a name="name"></a>name

**Obligatorio:** objeto

El nombre de la experiencia de la aplicación, que se muestra a los usuarios en la experiencia de Teams. Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada de AppSource. Los valores de `short` y no deben ser los `full` mismos.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`short`|30 caracteres|✔|Nombre corto para mostrar de la aplicación.|
|`full`|100 caracteres||El nombre completo de la aplicación, que se usa si el nombre completo de la aplicación supera los 30 caracteres.|

## <a name="description"></a>descripción

**Obligatorio:** objeto

Describe la aplicación a los usuarios. Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada de AppSource.

Asegúrate de que tu descripción describa con precisión tu experiencia y proporciona información para ayudar a los clientes potenciales a comprender lo que hace tu experiencia. También debe tener en cuenta, en la descripción completa, si se requiere una cuenta externa para su uso. Los valores de `short` y no deben ser los `full` mismos.  La descripción breve no debe repetirse dentro de la descripción larga y no debe incluir ningún otro nombre de aplicación.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`short`|80 caracteres|✔|Una breve descripción de la experiencia de la aplicación, que se usa cuando el espacio es limitado.|
|`full`|4000 caracteres|✔|Descripción completa de la aplicación.|

## <a name="packagename"></a>packageName

**Opcional:** cadena

Un identificador único para esta aplicación en la notación de dominio inverso; por ejemplo, com.example.myapp. Longitud máxima: 64 caracteres.

## <a name="localizationinfo"></a>localizationInfo

**Opcional:** objeto

Permite especificar un idioma predeterminado, así como punteros a archivos de idioma adicionales. Vea [localización.](~/concepts/build-and-test/apps-localization.md)

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`defaultLanguageTag`||✔|La etiqueta de idioma de las cadenas de este archivo de manifiesto de nivel superior.|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

Una matriz de objetos que especifica traducciones de idioma adicionales.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`languageTag`||✔|La etiqueta de idioma de las cadenas en el archivo proporcionado.|
|`file`||✔|Una ruta de acceso de archivo relativa a un archivo .json que contiene las cadenas traducidas.|

## <a name="icons"></a>iconos

**Obligatorio:** objeto

Iconos usados dentro de la aplicación teams. Los archivos de icono deben incluirse como parte del paquete de carga. Consulta [Iconos para](../../concepts/build-and-test/apps-package.md#app-icons) obtener más información.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`outline`|32 x 32 píxeles|✔|Una ruta de acceso de archivo relativa a un icono de esquema PNG transparente de 32 x 32.|
|`color`|192 x 192 píxeles|✔|Una ruta de acceso de archivo relativa a un icono PNG de color completo de 192 x 192.|

## <a name="accentcolor"></a>accentColor

**Opcional:** código de color hexadecimal HTML

Color que se usa junto con los iconos de esquema y como fondo.

El valor debe ser un código de color HTML válido que comience por '#', por `#4464ee` ejemplo.

## <a name="configurabletabs"></a>configurableTabs

**Opcional:** matriz

Se usa cuando la experiencia de la aplicación tiene una experiencia de pestaña de canal de equipo que requiere configuración adicional antes de agregarla. Las pestañas configurables solo se admiten en  el ámbito de teams (no en el personal) y actualmente solo se admite una pestaña por aplicación.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`configurationUrl`|string|2048 caracteres|✔|La https:// url que se va a usar al configurar la pestaña.|
|`scopes`|matriz de enumeraciones|1 |✔|Actualmente, las pestañas configurables solo admiten `team` los `groupchat` ámbitos y los ámbitos. |
|`canUpdateConfiguration`|boolean|||Valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de su creación. Valor predeterminado: **true**.|
|`context` |matriz de enumeraciones|6 ||Conjunto de `contextItem` ámbitos en los que se admite una pestaña. Valor predeterminado: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.|
|`sharePointPreviewImage`|cadena|2048||Una ruta de acceso de archivo relativa a una imagen de vista previa de pestaña para su uso en SharePoint. Tamaño 1024 x 768. |
|`supportedSharePointHosts`|matriz de enumeraciones|1 ||Define cómo estará disponible la pestaña en SharePoint. Las opciones son `sharePointFullPage` y `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**Opcional:** matriz

Define un conjunto de pestañas que se pueden "anclar" de forma predeterminada, sin que el usuario las agregue manualmente. Las pestañas estáticas declaradas en el ámbito `personal` siempre se anclan a la experiencia personal de la aplicación. Las pestañas estáticas declaradas en `team` el ámbito no se admiten actualmente.

Este elemento es una matriz (máximo de 16 elementos) con todos los elementos del tipo `object` . Este bloque solo es necesario para las soluciones que proporcionan una solución de pestaña estática.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`entityId`|string|64 caracteres|✔|Identificador único de la entidad que muestra la pestaña.|
|`name`|cadena|128 caracteres|✔|Nombre para mostrar de la pestaña en la interfaz de canal.|
|`contentUrl`|cadena||✔|La https:// url que apunta a la interfaz de usuario de la entidad que se mostrará en el lienzo de Teams.|
|`websiteUrl`|cadena|||La https:// url que se debe señalar si un usuario opta por ver en un explorador.|
|`searchUrl`|cadena|||La https:// url a la que se debe apuntar para las consultas de búsqueda de un usuario.|
|`scopes`|matriz de enumeraciones|1 |✔|Actualmente, las pestañas estáticas solo admiten el ámbito, lo que significa que solo se pueden aprovisionar como `personal` parte de la experiencia personal.|
|`context` | matriz de enumeraciones| 2 || Conjunto de `contextItem` ámbitos en los que se admite una pestaña.|

> [!NOTE]
> Si las pestañas requieren información dependiente del contexto para mostrar contenido  relevante o para iniciar un flujo de autenticación, consulte Obtener contexto [para la pestaña de Microsoft Teams.](../../tabs/how-to/access-teams-context.md)

## <a name="bots"></a>bots

**Opcional:** matriz

Define una solución de bot, junto con información opcional, como las propiedades de comandos predeterminadas.

El elemento es una matriz (actualmente solo se permite un único elemento por aplicación) con todos los &mdash; elementos del tipo `object` . Este bloque solo es necesario para las soluciones que proporcionan una experiencia de bot.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`botId`|string|64 caracteres|✔|El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework. Esto puede ser igual que el identificador general [de la aplicación.](#id)|
|`scopes`|matriz de enumeraciones|3|✔|Especifica si el bot ofrece una experiencia en el contexto de un canal en un `team`, en un chat de grupo (`groupchat`) o una experiencia específica para un solo usuario (`personal`). Estas opciones no son exclusivas.|
|`needsChannelSelector`|boolean|||Describe si el bot usa una sugerencia del usuario para agregar el bot a un canal específico. Valor predeterminado: **`false`**|
|`isNotificationOnly`|boolean|||Indica si un bot es un bot unidireccional de solo notificación o un bot de conversación. Valor predeterminado: **`false`**|
|`supportsFiles`|boolean|||Indica si el bot es compatible con la capacidad para cargar y descargar archivos en chat personal. Valor predeterminado: **`false`**|
|`supportsCalling`|boolean|||Un valor que indica dónde admite un bot las llamadas de audio. **IMPORTANTE:** esta propiedad es actualmente experimental. Es posible que las propiedades experimentales no estén completas y que se someta a cambios antes de estar totalmente disponibles.  Se proporciona únicamente con fines de prueba y exploración y no debe usarse en aplicaciones de producción. Valor predeterminado: **`false`**|
|`supportsVideo`|boolean|||Valor que indica dónde admite un bot las videollamadas. **IMPORTANTE:** esta propiedad es actualmente experimental. Es posible que las propiedades experimentales no estén completas y que se someta a cambios antes de estar totalmente disponibles.  Se proporciona únicamente con fines de prueba y exploración y no debe usarse en aplicaciones de producción. Valor predeterminado: **`false`**|

### <a name="botscommandlists"></a>bots.commandLists

Una lista opcional de comandos que el bot puede recomendar a los usuarios. El objeto es una matriz (máximo de 2 elementos) con todos los elementos de tipo; debe definir una lista de comandos independiente para cada ámbito compatible `object` con el bot. Vea [los menús del bot](~/bots/how-to/create-a-bot-commands-menu.md) para obtener más información.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`items.scopes`|matriz de enumeraciones|3|✔|Especifica el ámbito para el que la lista de comandos es válida. Las opciones son `team`, `personal` y `groupchat`.|
|`items.commands`|matriz de objetos|10 |✔|Una matriz de comandos que el bot admite:<br>`title`: el nombre de comando del bot (cadena, 32)<br>`description`: una descripción o un ejemplo sencillo de la sintaxis del comando y su argumento (cadena, 128).|

### <a name="botscommandlistscommands"></a>bots.commandLists.commands

|Nombre| Tipo| Tamaño máximo | Necesario | Description|
|---|---|---|---|---|
|title|string|12 |✔|El nombre del comando bot|
|description|cadena|128 caracteres|✔|Una descripción de texto simple o un ejemplo de la sintaxis del comando y sus argumentos.|

## <a name="connectors"></a>conectores

**Opcional:** matriz

El `connectors` bloque define un conector de Office 365 para la aplicación.

El objeto es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` . Este bloque solo es necesario para las soluciones que proporcionan un conector.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`configurationUrl`|string|2048 caracteres|✔|La https:// url que se va a usar al configurar el conector.|
|`scopes`|matriz de enumeraciones|1 |✔|Especifica si el conector ofrece una experiencia en el contexto de un canal en un , o una experiencia en el ámbito de `team` un usuario individual solo ( `personal` ). Actualmente, solo se `team` admite el ámbito.|
|`connectorId`|cadena|64 caracteres|✔|Un identificador único para el conector que coincide con su identificador en el panel del programador [de conectores.](https://aka.ms/connectorsdashboard)|

## <a name="composeextensions"></a>composeExtensions

**Opcional:** matriz

Define una extensión de mensajería para la aplicación.

> [!NOTE]
> The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.

El elemento es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` . Este bloque solo es necesario para las soluciones que proporcionan una extensión de mensajería.

|Nombre| Tipo | Tamaño máximo | Obligatorio | Descripción|
|---|---|---|---|---|
|`botId`|string|64|✔|El identificador único de la aplicación de Microsoft para el bot que hace una copia de seguridad de la extensión de mensajería, tal como se registró con Bot Framework. Esto puede ser igual que el identificador general de la aplicación.|
|`commands`|matriz de objetos|10 |✔|Matriz de comandos que admite la extensión de mensajería|
|`canUpdateConfiguration`|boolean|||Valor que indica si el usuario puede actualizar la configuración de una extensión de mensajería. Valor predeterminado: **false**.|
|`messageHandlers`|matriz de objetos|5 ||Una lista de controladores que permiten invocar aplicaciones cuando se cumplen ciertas condiciones.|
|`messageHandlers.type`|cadena|||El tipo de controlador de mensajes. Debe ser `"link"`.|
|`messageHandlers.value.domains`|matriz de cadenas|||Matriz de dominios para los que se puede registrar el controlador de mensajes de vínculo.|

### <a name="composeextensionscommands"></a>composeExtensions.commands

La extensión de mensajería debe declarar uno o más comandos. Cada comando aparece en Microsoft Teams como una posible interacción desde el punto de entrada basado en la interfaz de usuario. Hay un máximo de 10 comandos.

Cada elemento de comando es un objeto con la estructura siguiente:

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`id`|string|64 caracteres|✔|Identificador del comando.|
|`title`|cadena|32 caracteres|✔|El nombre de comando fácil de usar.|
|`type`|cadena|64 caracteres||Tipo del comando. Uno de `query` o `action` . Valor predeterminado: **consulta**.|
|`description`|cadena|128 caracteres||Descripción que los usuarios parecen indicar el propósito de este comando.|
|`initialRun`|boolean|||Valor booleano que indica si el comando debe ejecutarse inicialmente sin parámetros. Valor predeterminado: **false**.|
|`context`|matriz de cadenas|3||Define desde dónde se puede invocar la extensión de mensaje. Cualquier combinación `compose` de , `commandBox` `message` . El valor predeterminado es `["compose","commandBox"]`.|
|`fetchTask`|boolean|||Un valor booleano que indica si debe capturar el módulo de tarea dinámicamente. Valor predeterminado: **false**.|
|`taskInfo`|object|||Especifique el módulo de tareas que se debe cargar previamente al usar un comando de extensión de mensajería.|
|`taskInfo.title`|cadena|64 caracteres||Título del cuadro de diálogo inicial.|
|`taskInfo.width`|cadena|||Ancho del cuadro de diálogo: un número en píxeles o un diseño predeterminado, como "grande", "mediano" o "pequeño".|
|`taskInfo.height`|cadena|||Alto del cuadro de diálogo: un número en píxeles o un diseño predeterminado, como "grande", "mediano" o "pequeño".|
|`taskInfo.url`|cadena|||Dirección URL de vista web inicial.|
|`parameters`|matriz de objeto|5 elementos|✔|La lista de parámetros que toma el comando. Mínimo: 1; máximo: 5.|
|`parameters.name`|cadena|64 caracteres|✔|Nombre del parámetro tal como aparece en el cliente. Esto se incluye en la solicitud de usuario.|
|`parameters.title`|cadena|32 caracteres|✔|Título descriptivo para el parámetro.|
|`parameters.description`|cadena|128 caracteres||Cadena fácil de usar que describe el propósito de este parámetro.|
|`parameters.value`|cadena|512 caracteres||Valor inicial del parámetro.|
|`parameters.inputType`|cadena|128 caracteres||Define el tipo de control que se muestra en un módulo de tareas para `fetchTask: true` . Uno de `text, textarea, number, date, time, toggle, choiceset` .|
|`parameters.choices`|matriz de objetos|10 elementos||Las opciones de opción para `choiceset` el archivo . Usar solo cuando `parameter.inputType` es `choiceset` .|
|`parameters.choices.title`|cadena|128 caracteres|✔|Título de la elección.|
|`parameters.choices.value`|cadena|512 caracteres|✔|Valor de la elección.|

## <a name="permissions"></a>permissions

**Opcional:** matriz de cadenas

Matriz de la que se especifican los permisos que solicita la aplicación, lo que permite a los usuarios finales `string` saber cómo se llevará a cabo la extensión. Las siguientes opciones no son exclusivas:

* `identity`&emsp;Requiere información de identidad de usuario
* `messageTeamMembers`&emsp;Requiere permiso para enviar mensajes directos a los miembros del equipo

Al cambiar estos permisos al actualizar la aplicación, los usuarios repetirán el proceso de consentimiento la primera vez que ejecuten la aplicación actualizada. Consulta [Actualizar la aplicación](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) para obtener más información.

## <a name="devicepermissions"></a>devicePermissions

**Opcional:** matriz de cadenas

Especifica las características nativas del dispositivo de un usuario a las que la aplicación puede solicitar acceso. Las opciones son:

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**Opcional**, excepto **requerido cuando** se indica

Una lista de dominios válidos para los sitios web que la aplicación espera cargar en el cliente de Teams. Las listas de dominios pueden incluir caracteres comodín, por `*.example.com` ejemplo. Esto coincide exactamente con un segmento del dominio; si necesita hacer coincidir, `a.b.example.com` use `*.*.example.com` . Si la configuración de la pestaña o la interfaz de usuario de contenido necesitan navegar a cualquier otro dominio aparte del que se usa para la configuración de pestañas, ese dominio debe especificarse aquí.

Sin **embargo,** no es necesario incluir los dominios de proveedores de identidades que desea admitir en la aplicación. Por ejemplo, para autenticarse con un id. de Google, es necesario redirigir a accounts.google.com, pero no debe incluir accounts.google.com `validDomains[]` en .

Las aplicaciones de Teams que requieren sus propias direcciones URL de SharePoint para funcionar correctamente, pueden incluir "{teamsitedomain}" en su lista de dominios válida.

> [!IMPORTANT]
> No agregue dominios que estén fuera de su control, ya sea directamente o a través de caracteres comodín. Por ejemplo, `yourapp.onmicrosoft.com` es válido, pero `*.onmicrosoft.com` no es válido.

El objeto es una matriz con todos los elementos del tipo `string` .

## <a name="webapplicationinfo"></a>webApplicationInfo

**Opcional:** objeto

Especifique su id. de aplicación de Azure Active Directory (Azure AD) y la información de Microsoft Graph para ayudar a los usuarios a iniciar sesión sin problemas en la aplicación. Si la aplicación está registrada en Azure AD, debe proporcionar el id. de aplicación para que los administradores puedan revisar fácilmente los permisos y conceder consentimiento en el Centro de administración de Teams.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`id`|string|36 caracteres|✔|Id. de aplicación de AAD de la aplicación. Este identificador debe ser un GUID.|
|`resource`|cadena|2048 caracteres|✔|Dirección URL de recurso de la aplicación para adquirir un token de autenticación para SSO. </br> **NOTA:** Si no usa SSO, asegúrese de escribir un valor de cadena ficticia en este campo en el manifiesto de la aplicación, por ejemplo, para evitar https://notapplicable una respuesta de error. |
|`applicationPermissions`|matriz de cadenas|128 caracteres||Especifique el consentimiento [específico del recurso pormenorizados.](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)|

## <a name="showloadingindicator"></a>showLoadingIndicator

**Opcional:** booleano

Indica si se va a mostrar el indicador de carga cuando se carga una aplicación o pestaña. Valor predeterminado: **false**.
>[!NOTE]
>Si estableces "showLoadingIndicator : true" en el manifiesto de la aplicación, para que la página se cargue correctamente, debes modificar las páginas de contenido de las pestañas y los módulos de tareas según el protocolo descrito en [Mostrar](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) un documento de indicador de carga nativo.


## <a name="isfullscreen"></a>isFullScreen

 **Opcional:** booleano

Indica dónde se representa una aplicación personal con o sin una barra de encabezado de pestaña. Valor predeterminado: **false**.

## <a name="activities"></a>activities

**Opcional:** objeto

Define las propiedades que usará la aplicación para publicar en una fuente de actividad de usuario.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`activityTypes`|matriz de objetos|128 elementos| | Especifica los tipos de actividades que la aplicación puede publicar en una fuente de actividades de los usuarios.|

### <a name="activitiesactivitytypes"></a>activities.activityTypes

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`type`|string|32 caracteres|✔|El tipo de notificación. *Vea a continuación*.|
|`description`|cadena|128 caracteres|✔|Breve descripción de la notificación. *Vea a continuación*.|
|`templateText`|cadena|128 caracteres|✔|Por ejemplo: "{actor} creó la tarea {taskId} por usted"|

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

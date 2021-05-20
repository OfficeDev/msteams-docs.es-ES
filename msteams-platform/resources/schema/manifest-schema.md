---
title: Referencia de esquema manifiesto
description: Describe el esquema de manifiesto para Microsoft Teams
ms.topic: reference
ms.author: lajanuar
localization_priority: Normal
keywords: equipos manifiestan esquema
ms.openlocfilehash: 6c7cd02480f78d19aed269b5d78d0c6f470621d2
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566449"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>Referencia: Esquema de manifiesto para Microsoft Teams

El manifiesto Teams describe cómo se integra la aplicación en el producto Microsoft Teams. El manifiesto debe ajustarse al esquema hospedado en [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json) . Las versiones anteriores 1.0, 1.1,..., 1.6, etc., también son compatibles (usando "v1.x" en la DIRECCIÓN URL).

En el ejemplo de esquema siguiente se muestran todas las opciones de extensibilidad:

## <a name="sample-full-manifest"></a>Muestra de manifiesto completo

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json",
  "manifestVersion": "1.10",
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
  },
  "defaultInstallScope": "meetings",
  "defaultGroupCapability": {
    "meetings": "tab", 
    "team": "bot", 
    "groupchat": "bot"
  },
  "configurableProperties": [
     "name",
     "shortDescription",
     "longDescription",
     "smallImageUrl", 
     "largeImageUrl", 
     "accentColor",
     "websiteUrl",
     "privacyUrl",
     "termsOfUseUrl"        
  ]              
}
```

El esquema define las siguientes propiedades:

## <a name="schema"></a>$schema

Opcional, pero recomendado — cadena

La dirección URL https:// que hace referencia al esquema JSON del manifiesto.

## <a name="manifestversion"></a>manifestVersion

**Requerido** — cadena

La versión del esquema de manifiesto que este manifiesto está utilizando. Debe ser 1.10.

## <a name="version"></a>version

**Requerido** — cadena

La versión de una aplicación específica. Si actualiza algo en el manifiesto, la versión también debe incrementarse. De esta manera, cuando se instala el nuevo manifiesto, sobrescribe el existente y el usuario recibe la nueva funcionalidad. Si esta aplicación se envió a la tienda, el nuevo manifiesto debe volver a enviarse y volver a validarse. Los usuarios de la aplicación reciben el nuevo manifiesto actualizado automáticamente dentro de las pocas horas después de la aprobación del manifiesto.

Si las solicitudes de permisos de la aplicación cambian, se pide a los usuarios que actualicen y vuelvan a dar su consentimiento a la aplicación.

Esta cadena de versión debe seguir el estándar [de semver](http://semver.org/) (MAJOR. menor. PARCHE).

## <a name="id"></a>id

**Obligatorio** : identificador de aplicación de Microsoft

El identificador es un identificador único generado por Microsoft para la aplicación. Tienes un identificador si el bot está registrado a través de la Microsoft Bot Framework o la aplicación web de tu pestaña ya inicia sesión con Microsoft. Debe introducir el ID aquí. De lo contrario, debe generar un nuevo identificador en el [Portal de registro de aplicaciones de Microsoft.](https://aka.ms/appregistrations) Utilice el mismo ID si agrega un bot.

> [!NOTE]
> Si va a enviar una actualización a la aplicación existente en AppSource, el identificador del manifiesto no debe modificarse.

## <a name="developer"></a>developer

**Requerido** — objeto

Especifica información sobre su empresa. Para las aplicaciones enviadas a la tienda Teams, estos valores deben coincidir con la información de la lista de la tienda. Para obtener más información, consulte las [directrices de publicación de Teams tienda.](~/concepts/deploy-and-publish/appsource/publish.md)

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`name`|32 caracteres|✔|El nombre para mostrar del desarrollador.|
|`websiteUrl`|2048 caracteres|✔|La URL de https:// al sitio web del desarrollador. Este enlace debe llevar a los usuarios a su empresa o página de destino específica del producto.|
|`privacyUrl`|2048 caracteres|✔|La dirección URL de https:// a la política de privacidad del desarrollador.|
|`termsOfUseUrl`|2048 caracteres|✔|La dirección URL https:// a los términos de uso del desarrollador.|
|`mpnId`|10 caracteres| |**Opcional** Identificador de red de partners de Microsoft que identifica la organización asociada que compilará la aplicación.|

## <a name="name"></a>name

**Requerido** — objeto

El nombre de la experiencia de la aplicación, que se muestra a los usuarios en la experiencia Teams. Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada de AppSource. Los valores de `short` y `full` debe ser diferente.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`short`|30 caracteres|✔|El nombre para mostrar corto de la aplicación.|
|`full`|100 caracteres||El nombre completo de la aplicación, utilizado si el nombre completo de la aplicación supera los 30 caracteres.|

## <a name="description"></a>description

**Requerido** — objeto

Describe la aplicación a los usuarios. Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada de AppSource.

Asegúrese de que su descripción describe con precisión su experiencia y proporciona información para ayudar a los clientes potenciales a entender lo que hace su experiencia. Debe tener en cuenta en la descripción completa, si se requiere una cuenta externa para su uso. Los valores de `short` y `full` debe ser diferente. La breve descripción no debe repetirse dentro de la descripción larga y no debe incluir ningún otro nombre de aplicación.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`short`|80 caracteres|✔|Una breve descripción de la experiencia de la aplicación, utilizada cuando el espacio es limitado.|
|`full`|4000 caracteres|✔|La descripción completa de la aplicación.|

## <a name="packagename"></a>packageName

**Opcional** — cadena

Un identificador único para la aplicación en notación de dominio inverso; por ejemplo, com.example.myapp. Longitud máxima: 64 caracteres.

## <a name="localizationinfo"></a>localizaciónInfo

**Opcional** — objeto

Permite la especificación de un idioma predeterminado, así como punteros a archivos de idioma adicionales. Para obtener más información, consulte [localización](~/concepts/build-and-test/apps-localization.md).

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`defaultLanguageTag`||✔|La etiqueta de idioma de las cadenas de este archivo de manifiesto de nivel superior.|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

Matriz de objetos que especifica traducciones de idioma adicionales.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`languageTag`||✔|La etiqueta de idioma de las cadenas del archivo proporcionado.|
|`file`||✔|Una ruta de acceso de archivo relativa a un archivo .json que contiene las cadenas traducidas.|

## <a name="icons"></a>iconos

**Requerido** — objeto

Iconos utilizados en la aplicación Teams. Los archivos de icono deben incluirse como parte del paquete de carga. Consulte [Iconos](../../concepts/build-and-test/apps-package.md#app-icons) para obtener más información.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`outline`|32 x 32 píxeles|✔|Una ruta de acceso de archivo relativa a un icono de contorno PNG 32x32 transparente.|
|`color`|192 x 192 píxeles|✔|Una ruta de acceso de archivo relativa a un icono PNG 192x192 a todo color.|

## <a name="accentcolor"></a>accentColor

**Opcional** — Código de color HTML Hexagonal

Un color para usar junto con y como fondo para los iconos de contorno.

El valor debe ser un código de color HTML válido que comience por '#', por `#4464ee` ejemplo.

## <a name="configurabletabs"></a>configurableTabs

**Opcional** — matriz

Se usa cuando la experiencia de la aplicación tiene una experiencia de pestaña de canal de equipo que requiere configuración adicional antes de agregarla. Las pestañas configurables solo se admiten en el ámbito de los equipos y puede configurar las mismas pestañas varias veces. Sin embargo, solo puede definirlo en el manifiesto una sola vez.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`configurationUrl`|string|2048 caracteres|✔|La dirección URL https:// que se usará al configurar la pestaña.|
|`scopes`|variedad de enumeraciones|1|✔|Actualmente, las pestañas configurables solo admiten el `team` `groupchat` ámbito. |
|`canUpdateConfiguration`|boolean|||Valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de la creación. Predeterminado: **true**.|
|`context` |variedad de enumeraciones|6 ||El conjunto de `contextItem` ámbitos donde se admite una [pestaña.](../../tabs/how-to/access-teams-context.md) Valor predeterminado: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.|
|`sharePointPreviewImage`|cadena|2048||Una ruta de acceso de archivo relativa a una imagen de vista previa de tabulación para su uso en SharePoint. Tamaño 1024x768. |
|`supportedSharePointHosts`|variedad de enumeraciones|1||Define cómo la pestaña está disponible en SharePoint. Las opciones son `sharePointFullPage` y `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**Opcional** — matriz

Define un conjunto de pestañas que se pueden "anclar" de forma predeterminada, sin que el usuario las agregue manualmente. Las pestañas estáticas declaradas en `personal` el ámbito siempre están ancladas a la experiencia personal de la aplicación. Actualmente no se admiten pestañas estáticas declaradas en el `team` ámbito.

Este elemento es una matriz (máximo de 16 elementos) con todos los elementos del tipo `object` . Este bloque solo es necesario para soluciones que proporcionan una solución de pestaña estática.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`entityId`|string|64 caracteres|✔|Identificador único de la entidad que muestra la pestaña.|
|`name`|cadena|128 caracteres|✔|El nombre para mostrar de la pestaña en la interfaz del canal.|
|`contentUrl`|cadena||✔|La dirección URL de https:// que apunta a la interfaz de usuario de la entidad que se mostrará en el lienzo de Teams.|
|`websiteUrl`|cadena|||La dirección URL https:// a la que apuntar si un usuario opta por verlo en un explorador.|
|`searchUrl`|cadena|||La dirección URL https:// a la que se debe apuntar para las consultas de búsqueda de un usuario.|
|`scopes`|variedad de enumeraciones|1|✔|Actualmente, las pestañas estáticas solo admiten el `personal` ámbito, lo que significa que solo se puede aprovisionar como parte de la experiencia personal.|
|`context` | variedad de enumeraciones| 2|| El conjunto de `contextItem` ámbitos donde se admite una pestaña.|

> [!NOTE]
>  La característica searchUrl no está disponible para los desarrolladores de terceros.
> Si las pestañas requieren información dependiente del contexto para mostrar contenido relevante o para iniciar un flujo de autenticación, para obtener más información, consulte [Obtener contexto para la pestaña Microsoft Teams](../../tabs/how-to/access-teams-context.md).

## <a name="bots"></a>Bots

**Opcional** — matriz

Define una solución de bot, junto con información opcional, como las propiedades de comando predeterminadas.

El elemento es una matriz (máximo de solo 1 elemento &mdash; actualmente solo se permite un bot por aplicación) con todos los elementos del tipo `object` . Este bloque solo es necesario para soluciones que proporcionan una experiencia de bot.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`botId`|string|64 caracteres|✔|El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework. Esto bien puede ser el mismo que el IDENTIFICADOR general de la [aplicación.](#id)|
|`scopes`|variedad de enumeraciones|3|✔|Especifica si el bot ofrece una experiencia en el contexto de un canal en un `team`, en un chat de grupo (`groupchat`) o una experiencia específica para un solo usuario (`personal`). Estas opciones no son exclusivas.|
|`needsChannelSelector`|boolean|||Describe si el bot usa una sugerencia del usuario para agregar el bot a un canal específico. predeterminado: **`false`**|
|`isNotificationOnly`|boolean|||Indica si un bot es un bot unidireccional de solo notificación o un bot de conversación. predeterminado: **`false`**|
|`supportsFiles`|boolean|||Indica si el bot es compatible con la capacidad para cargar y descargar archivos en chat personal. predeterminado: **`false`**|
|`supportsCalling`|boolean|||Valor que indica dónde un bot admite llamadas de audio. **IMPORTANTE**: Esta propiedad es actualmente experimental. Es posible que las propiedades experimentales no estén completas y puedan sufrir cambios antes de estar completamente disponibles.  Se proporciona únicamente con fines de pruebas y exploración y no debe utilizarse en aplicaciones de producción. predeterminado: **`false`**|
|`supportsVideo`|boolean|||Valor que indica dónde un bot admite videollamadas. **IMPORTANTE**: Esta propiedad es actualmente experimental. Es posible que las propiedades experimentales no estén completas y puedan sufrir cambios antes de estar completamente disponibles.  Se proporciona únicamente con fines de pruebas y exploración y no debe utilizarse en aplicaciones de producción. predeterminado: **`false`**|

### <a name="botscommandlists"></a>bots.commandLists

Una lista opcional de comandos que el bot puede recomendar a los usuarios. El objeto es una matriz (máximo de 2 elementos) con todos los elementos de tipo; debe definir una lista de `object` comandos independiente para cada ámbito que admita el bot. Consulte [menús bot](~/bots/how-to/create-a-bot-commands-menu.md) para obtener más información.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`items.scopes`|variedad de enumeraciones|3|✔|Especifica el ámbito para el que la lista de comandos es válida. Las opciones son `team`, `personal` y `groupchat`.|
|`items.commands`|matriz de objetos|10|✔|Una matriz de comandos que el bot admite:<br>`title`: el nombre de comando del bot (cadena, 32)<br>`description`: una descripción simple o ejemplo de la sintaxis del comando y su argumento (cadena, 128).|

### <a name="botscommandlistscommands"></a>bots.commandLists.commands

|Nombre| Tipo| Tamaño máximo | Necesario | Description|
|---|---|---|---|---|
|title|string|12 |✔|El nombre del comando bot.|
|description|cadena|128 caracteres|✔|Una descripción de texto simple o un ejemplo de la sintaxis del comando y sus argumentos.|

## <a name="connectors"></a>Conectores

**Opcional** — matriz

El `connectors` bloque define un conector de Office 365 para la aplicación.

El objeto es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` . Este bloque solo es necesario para las soluciones que proporcionan un conector.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`configurationUrl`|string|2048 caracteres|✔|La dirección URL https:// que se usará al configurar el conector.|
|`scopes`|variedad de enumeraciones|1|✔|Especifica si connector ofrece una experiencia en el contexto de un canal en un `team` objeto y una experiencia con ámbito a un usuario individual solo ( `personal` ). Actualmente, solo se admite el `team` ámbito.|
|`connectorId`|cadena|64 caracteres|✔|Identificador único del conector que coincide con su identificador en el [panel de desarrollador de conectores.](https://aka.ms/connectorsdashboard)|

## <a name="composeextensions"></a>composeExtensions

**Opcional** — matriz

Define una extensión de mensajería para la aplicación.

> [!NOTE]
> El nombre de la característica se cambió de "extensión de composición" a "extensión de mensajería" en noviembre de 2017, pero el nombre del manifiesto sigue siendo el mismo para que las extensiones existentes sigan funcionando.

El elemento es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` . Este bloque solo es necesario para las soluciones que proporcionan una extensión de mensajería.

|Nombre| Tipo | Tamaño máximo | Obligatorio | Descripción|
|---|---|---|---|---|
|`botId`|string|64|✔|El identificador único de la aplicación de Microsoft para el bot que respalda la extensión de mensajería, registrado con Bot Framework. Esto bien puede ser el mismo que el ID de aplicación general.|
|`commands`|matriz de objetos|10|✔|Matriz de comandos que admite la extensión de mensajería.|
|`canUpdateConfiguration`|boolean|||Valor que indica si el usuario puede actualizar la configuración de una extensión de mensajería. Valor predeterminado: **false**.|
|`messageHandlers`|matriz de objetos|5 ||Una lista de controladores que permiten invocar aplicaciones cuando se cumplen ciertas condiciones.|
|`messageHandlers.type`|cadena|||El tipo de controlador de mensajes. Debe ser `"link"`.|
|`messageHandlers.value.domains`|matriz de cuerdas|||Matriz de dominios para los que el controlador de mensajes de vínculo puede registrarse.|

### <a name="composeextensionscommands"></a>composeExtensions.commands

La extensión de mensajería debe declarar uno o varios comandos. Cada comando aparece en Microsoft Teams como una interacción potencial desde el punto de entrada basado en la interfaz de usuario. Hay un máximo de 10 comandos.

Cada elemento de comando es un objeto con la siguiente estructura:

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`id`|string|64 caracteres|✔|El ID del comando.|
|`title`|cadena|32 caracteres|✔|El nombre del comando fácil de usar.|
|`type`|cadena|64 caracteres||Tipo de comando. Uno de `query` o `action` . Predeterminado: **consulta**.|
|`description`|cadena|128 caracteres||La descripción que aparece a los usuarios para indicar el propósito de este comando.|
|`initialRun`|boolean|||Un valor booleano indica si el comando se ejecuta inicialmente sin parámetros. El valor predeterminado es **false**.|
|`context`|matriz de cuerdas|3||Define desde dónde se puede invocar la extensión de mensaje. Cualquier combinación de `compose` `commandBox` , `message` . El valor predeterminado es `["compose","commandBox"]`.|
|`fetchTask`|boolean|||Valor booleano que indica si debe capturar el módulo de tareas dinámicamente. El valor predeterminado es **false**.|
|`taskInfo`|object|||Especifique el módulo de tareas que se va a cargar previamente cuando utilice un comando de extensión de mensajería.|
|`taskInfo.title`|cadena|64 caracteres||Título inicial del cuadro de diálogo.|
|`taskInfo.width`|cadena|||Ancho del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "medio" o "pequeño".|
|`taskInfo.height`|cadena|||Altura del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "medio" o "pequeño".|
|`taskInfo.url`|cadena|||URL de vista web inicial.|
|`parameters`|matriz de objetos|5 artículos|✔|La lista de parámetros que toma el comando. Mínimo: 1; máximo: 5.|
|`parameters.name`|cadena|64 caracteres|✔|El nombre del parámetro tal como aparece en el cliente. Esto se incluye en la solicitud de usuario.|
|`parameters.title`|cadena|32 caracteres|✔|Título fácil de usar para el parámetro.|
|`parameters.description`|cadena|128 caracteres||Cadena fácil de usar que describe el propósito de este parámetro.|
|`parameters.value`|cadena|512 caracteres||Valor inicial para el parámetro.|
|`parameters.inputType`|cadena|128 caracteres||Define el tipo de control que se muestra en un módulo de tareas para `fetchTask: true` . Uno de `text, textarea, number, date, time, toggle, choiceset` .|
|`parameters.choices`|matriz de objetos|10 artículos||Las opciones de elección para el `choiceset` archivo . Utilice únicamente cuando `parameter.inputType` sea `choiceset` .|
|`parameters.choices.title`|cadena|128 caracteres|✔|Título de la elección.|
|`parameters.choices.value`|cadena|512 caracteres|✔|Valor de la elección.|

## <a name="permissions"></a>permisos

**Opcional** — matriz de cadenas

Una matriz de `string` la que se especifica qué permisos solicita la aplicación, lo que permite a los usuarios finales saber cómo funciona la extensión. Las siguientes opciones no son exclusivas:

* `identity`&emsp;Requiere información de identidad de usuario.
* `messageTeamMembers`&emsp;Requiere permiso para enviar mensajes directos a los miembros del equipo.

Cambiar estos permisos durante la actualización de la aplicación, hace que los usuarios repitan el proceso de consentimiento después de ejecutar la aplicación actualizada. Consulta [Actualización de la aplicación](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) para obtener más información.

## <a name="devicepermissions"></a>dispositivoPermissions

**Opcional** — matriz de cadenas

Proporciona las características nativas en el dispositivo de un usuario al que la aplicación solicita acceso. Las opciones son:

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**Opcional,** excepto **Obligatorio** cuando se indique.

Una lista de dominios válidos para los sitios web que la aplicación espera cargar dentro del cliente Teams. Los listados de dominios pueden incluir comodines, por ejemplo, `*.example.com` . Esto coincide exactamente con un segmento del dominio; si necesita `a.b.example.com` coincidir, utilice `*.*.example.com` . Si la configuración de la pestaña o la interfaz de usuario de contenido deben navegar a cualquier otro dominio además del que se usa para la configuración de pestañas, ese dominio debe especificarse aquí.

**No** es necesario incluir los dominios de los proveedores de identidades que desea admitir en la aplicación. Por ejemplo, para autenticarse con un ID de Google, es necesario redirigir a accounts.google.com, sin embargo, no debe incluir accounts.google.com en `validDomains[]` .

Teams aplicaciones que requieren que sus propias direcciones URL de sharepoint funcionen bien, incluye "{teamsitedomain}" en su lista de dominios válida.

> [!IMPORTANT]
> No agregue dominios que estén fuera del control, ya sea directamente o a través de comodines. Por ejemplo, `yourapp.onmicrosoft.com` es válido, sin embargo, `*.onmicrosoft.com` no es válido.

El objeto es una matriz con todos los elementos del tipo `string` .

## <a name="webapplicationinfo"></a>webApplicationInfo

**Opcional** — objeto

Proporcione el identificador de aplicación de Azure Active Directory (AAD) y microsoft Graph información para ayudar a los usuarios a iniciar sesión sin problemas en la aplicación. Si la aplicación está registrada en AAD, debe proporcionar el IDENTIFICADOR de aplicación para que los administradores puedan revisar fácilmente los permisos y conceder su consentimiento en Teams centro de administración.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`id`|string|36 caracteres|✔|Identificador de aplicación AAD de la aplicación. Este id debe ser un GUID.|
|`resource`|cadena|2048 caracteres|✔|Dirección URL de recursos de la aplicación para adquirir token de autenticación para SSO. </br> **NOTA:** Si no usa SSO, asegúrese de introducir un valor de cadena ficticio en este campo en el manifiesto de la aplicación, por ejemplo, https://notapplicable para evitar una respuesta de error. |
|`applicationPermissions`|matriz de cadenas|128 caracteres||Especifique el [consentimiento específico del recurso](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)granular.|

## <a name="showloadingindicator"></a>showLoadingIndicator

**Opcional** — booleano

Indica si se debe mostrar o no el indicador de carga cuando se carga una aplicación o pestaña. El valor predeterminado es **false**.
>[!NOTE]
>Si selecciona `showLoadingIndicator` como true en el manifiesto de la aplicación, para cargar la página correctamente, modifique las páginas de contenido de las pestañas y los módulos de tareas como se describe en Mostrar un documento indicador de carga [nativo.](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)


## <a name="isfullscreen"></a>isFullScreen

 **Opcional** — booleano

Indique dónde se representa una aplicación personal con o sin una barra de encabezado de tabulación. El valor predeterminado es **false**.

## <a name="activities"></a>activities

**Opcional** — objeto

Defina las propiedades que usa la aplicación para publicar una fuente de actividad de usuario.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`activityTypes`|matriz de objetos|128 artículos| | Proporcione los tipos de actividades que la aplicación puede publicar en una fuente de actividades de usuarios.|

### <a name="activitiesactivitytypes"></a>activities.activityTypes

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`type`|string|32 caracteres|✔|El tipo de notificación. *Vea a continuación*.|
|`description`|cadena|128 caracteres|✔|Una breve descripción de la notificación. *Vea a continuación*.|
|`templateText`|cadena|128 caracteres|✔|Por ejemplo: "{actor} creó la tarea {taskId} para usted"|

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

## <a name="defaultinstallscope"></a>defaultInstallScope

**Opcional** - cadena

Especifica el ámbito de instalación definido para esta aplicación de forma predeterminada. El ámbito definido será la opción que se muestra en el botón cuando un usuario intenta agregar la aplicación. Las opciones son:
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a>defaultGroupCapability

**Opcional** - objeto

Cuando se selecciona un ámbito de instalación de grupo, definirá la funcionalidad predeterminada cuando el usuario instale la aplicación. Las opciones son:
* `team`
* `groupchat`
* `meetings`
 
|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`team`|string|||Cuando se selecciona el ámbito de `team` instalación, este campo especifica la capacidad predeterminada disponible. Opciones: `tab` , `bot` o `connector` .|
|`groupchat`|cadena|||Cuando se selecciona el ámbito de `groupchat` instalación, este campo especifica la capacidad predeterminada disponible. Opciones: `tab` , `bot` o `connector` .|
|`meetings`|cadena|||Cuando se selecciona el ámbito de `meetings` instalación, este campo especifica la capacidad predeterminada disponible. Opciones: `tab` , `bot` o `connector` .|

## <a name="configurableproperties"></a>configurableProperties

**Opcional** - matriz

El `configurableProperties` bloque define las propiedades de la aplicación que Teams administrador puede personalizar. Para obtener más información, consulte [personalizar aplicaciones en Microsoft Teams](/MicrosoftTeams/customize-apps).

> [!NOTE]
> Se debe definir un mínimo de una propiedad. Puede definir un máximo de nueve propiedades en este bloque.
> Como práctica recomendada, debe proporcionar directrices de personalización para que los usuarios y clientes de la aplicación las sigan al personalizar la aplicación.

Puede definir cualquiera de las siguientes propiedades:
* `name`: Permite al administrador cambiar el nombre para mostrar de la aplicación.
* `shortDescription`: Permite al administrador cambiar la breve descripción de la aplicación.
* `longDescription`: Permite al administrador cambiar la descripción detallada de la aplicación.
* `smallImageUrl`: Es la `outline` propiedad en el bloque del `icons` manifiesto.
* `largeImageUrl`: Es la `color` propiedad en el bloque del `icons` manifiesto.
* `accentColor`: Es el color a utilizar junto con y como fondo para sus iconos de contorno.
* `websiteUrl`: Es la URL https:// al sitio web del desarrollador.
* `privacyUrl`: Es la URL https:// a la política de privacidad del desarrollador.
* `termsOfUseUrl`: Es la URL https:// a los términos de uso del desarrollador.



---
title: Referencia de esquema de manifiesto
description: Describe el esquema de manifiesto para Microsoft Teams
ms.topic: reference
ms.author: lajanuar
localization_priority: Normal
keywords: esquema de manifiesto de teams
ms.openlocfilehash: c0b8b6f5baa163d2292227f7d361b6d12849edec
ms.sourcegitcommit: 3475927e1c7964dc25c363d0d2026e5c898c97c7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/12/2021
ms.locfileid: "52336520"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>Referencia: esquema de manifiesto para Microsoft Teams

El Teams describe cómo se integra la aplicación en el Microsoft Teams producto. El manifiesto debe cumplir con el esquema hospedado en [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json) . También se admiten las versiones anteriores 1.0, 1.1,..., 1.6, y así sucesivamente (con "v1.x" en la dirección URL).

En el ejemplo de esquema siguiente se muestran todas las opciones de extensibilidad.

## <a name="sample-full-manifest"></a>Manifiesto completo de ejemplo

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

Opcional, pero recomendado: cadena

La https:// url que hace referencia al esquema JSON para el manifiesto.

## <a name="manifestversion"></a>manifestVersion

**Obligatorio:** cadena

La versión del esquema de manifiesto que usa este manifiesto. Debe ser 1.10.

## <a name="version"></a>version

**Obligatorio:** cadena

La versión de una aplicación específica. Si actualiza algo en el manifiesto, la versión también debe incrementarse. De este modo, cuando se instala el nuevo manifiesto, se sobrescribe el existente y el usuario recibe la nueva funcionalidad. Si esta aplicación se envió a la tienda, el nuevo manifiesto debe volver a enviarse y volver a validarse. Los usuarios de la aplicación reciben el nuevo manifiesto actualizado automáticamente en pocas horas después de que se apruebe el manifiesto.

Si cambian las solicitudes de permisos de la aplicación, se pedirá a los usuarios que actualicen y vuelvan a dar su consentimiento a la aplicación.

Esta cadena de versión debe seguir el [estándar de semver](http://semver.org/) (MAJOR. MINOR. PATCH).

## <a name="id"></a>id

**Obligatorio:** id. de aplicación de Microsoft

El identificador es un identificador único generado por Microsoft para la aplicación. Tienes un identificador si el bot está registrado a través del Microsoft Bot Framework o la aplicación web de la pestaña ya inicia sesión con Microsoft. Debe escribir el identificador aquí. De lo contrario, debe generar un nuevo identificador en el Portal de [registro de aplicaciones de Microsoft](https://aka.ms/appregistrations). Use el mismo identificador si agrega un bot.

> [!NOTE]
> Si vas a enviar una actualización a la aplicación existente en AppSource, no se debe modificar el identificador del manifiesto.

## <a name="developer"></a>developer

**Obligatorio** : objeto

Especifica información sobre su empresa. Para las aplicaciones enviadas a la Teams, estos valores deben coincidir con la información de la descripción de la tienda. Para obtener más información, consulte [las Teams de publicación del almacén de almacenamiento.](~/concepts/deploy-and-publish/appsource/publish.md)

|Nombre| Tamaño máximo | Necesario | Description|
|---|---|---|---|
|`name`|32 caracteres|✔|Nombre para mostrar del desarrollador.|
|`websiteUrl`|2048 caracteres|✔|La https:// url del sitio web del desarrollador. Este vínculo debe llevar a los usuarios a su empresa o página de aterrizaje específica del producto.|
|`privacyUrl`|2048 caracteres|✔|La https:// url a la directiva de privacidad del desarrollador.|
|`termsOfUseUrl`|2048 caracteres|✔|La https:// url a los términos de uso del desarrollador.|
|`mpnId`|10 caracteres| |**Opcional** Id. de red de partners de Microsoft que identifica la organización asociada que está creando la aplicación.|

## <a name="name"></a>name

**Obligatorio** : objeto

El nombre de la experiencia de la aplicación, que se muestra a los usuarios en la Teams usuario. Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource. Los valores de `short` y `full` deben ser diferentes.

|Nombre| Tamaño máximo | Necesario | Description|
|---|---|---|---|
|`short`|30 caracteres|✔|El nombre para mostrar corto de la aplicación.|
|`full`|100 caracteres||El nombre completo de la aplicación, que se usa si el nombre completo de la aplicación supera los 30 caracteres.|

## <a name="description"></a>description

**Obligatorio** : objeto

Describe la aplicación a los usuarios. Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource.

Asegúrese de que su descripción describe con precisión su experiencia y proporciona información para ayudar a los clientes potenciales a comprender lo que hace su experiencia. Debe tener en cuenta en la descripción completa, si se requiere una cuenta externa para su uso. Los valores de `short` y `full` deben ser diferentes. La descripción breve no debe repetirse dentro de la descripción larga y no debe incluir ningún otro nombre de aplicación.

|Nombre| Tamaño máximo | Necesario | Description|
|---|---|---|---|
|`short`|80 caracteres|✔|Una breve descripción de la experiencia de la aplicación, que se usa cuando el espacio es limitado.|
|`full`|4000 caracteres|✔|Descripción completa de la aplicación.|

## <a name="packagename"></a>packageName

**Opcional:** cadena

Un identificador único para la aplicación en la notación de dominio inverso; por ejemplo, com.example.myapp. Longitud máxima: 64 caracteres.

## <a name="localizationinfo"></a>localizationInfo

**Opcional** : objeto

Permite la especificación de un idioma predeterminado, así como punteros a archivos de idioma adicionales. Vea [localización](~/concepts/build-and-test/apps-localization.md).

|Nombre| Tamaño máximo | Necesario | Description|
|---|---|---|---|
|`defaultLanguageTag`||✔|La etiqueta de idioma de las cadenas de este archivo de manifiesto de nivel superior.|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

Una matriz de objetos que especifica traducciones de idioma adicionales.

|Nombre| Tamaño máximo | Necesario | Description|
|---|---|---|---|
|`languageTag`||✔|Etiqueta de idioma de las cadenas del archivo proporcionado.|
|`file`||✔|Una ruta de acceso de archivo relativa a un archivo .json que contiene las cadenas traducidas.|

## <a name="icons"></a>iconos

**Obligatorio** : objeto

Iconos usados dentro de la Teams aplicación. Los archivos de icono deben incluirse como parte del paquete de carga. Consulta [Iconos](../../concepts/build-and-test/apps-package.md#app-icons) para obtener más información.

|Nombre| Tamaño máximo | Necesario | Description|
|---|---|---|---|
|`outline`|32 x 32 píxeles|✔|Una ruta de acceso de archivo relativa a un icono de esquema PNG transparente de 32 x 32.|
|`color`|192 x 192 píxeles|✔|Una ruta de acceso de archivo relativa a un icono PNG de color completo de 192 x 192.|

## <a name="accentcolor"></a>accentColor

**Opcional:** código de color Hexadecimal HTML

Color que se usará junto con y como fondo para los iconos de esquema.

El valor debe ser un código de color HTML válido a partir de '#', por ejemplo `#4464ee` .

## <a name="configurabletabs"></a>configurableTabs

**Opcional:** matriz

Se usa cuando la experiencia de la aplicación tiene una experiencia de pestaña de canal de grupo que requiere una configuración adicional antes de agregarla. Las pestañas configurables solo se admiten en el ámbito de teams y puede configurar las mismas pestañas varias veces. Sin embargo, solo puede definirlo en el manifiesto una vez.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`configurationUrl`|string|2048 caracteres|✔|La https:// url que se va a usar al configurar la pestaña.|
|`scopes`|matriz de enumeraciones|1|✔|Actualmente, las pestañas configurables solo admiten `team` los `groupchat` ámbitos y. |
|`canUpdateConfiguration`|boolean|||Valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de su creación. Valor predeterminado: **true**.|
|`context` |matriz de enumeraciones|6 ||Conjunto de `contextItem` ámbitos donde se admite [una pestaña](../../tabs/how-to/access-teams-context.md). Valor predeterminado: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.|
|`sharePointPreviewImage`|cadena|2048||Una ruta de acceso de archivo relativa a una imagen de vista previa de tabulación para su uso en SharePoint. Tamaño 1024x768. |
|`supportedSharePointHosts`|matriz de enumeraciones|1||Define cómo la pestaña está disponible en SharePoint. Las opciones son `sharePointFullPage` y `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**Opcional:** matriz

Define un conjunto de pestañas que se pueden "anclar" de forma predeterminada, sin que el usuario las agregue manualmente. Las pestañas estáticas declaradas en el ámbito siempre se anclan a la experiencia `personal` personal de la aplicación. Actualmente no se admiten las pestañas estáticas declaradas `team` en el ámbito.

Este elemento es una matriz (máximo de 16 elementos) con todos los elementos del tipo `object` . Este bloque solo es necesario para las soluciones que proporcionan una solución de tabulación estática.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`entityId`|string|64 caracteres|✔|Identificador único para la entidad que muestra la pestaña.|
|`name`|cadena|128 caracteres|✔|Nombre para mostrar de la pestaña en la interfaz de canal.|
|`contentUrl`|cadena||✔|Dirección URL https:// que apunta a la interfaz de usuario de la entidad que se va a mostrar en el Teams usuario.|
|`websiteUrl`|cadena|||La https:// dirección URL que se debe apuntar si un usuario opta por ver en un explorador.|
|`searchUrl`|cadena|||La https:// dirección URL que se va a apuntar a las consultas de búsqueda de un usuario.|
|`scopes`|matriz de enumeraciones|1|✔|Actualmente, las pestañas estáticas solo admiten el ámbito, lo que significa que solo se puede aprovisionar como `personal` parte de la experiencia personal.|
|`context` | matriz de enumeraciones| 2|| Conjunto de `contextItem` ámbitos donde se admite una pestaña.|

> [!NOTE]
>  La característica searchUrl no está disponible para los desarrolladores de terceros.
> Si las pestañas requieren información dependiente del contexto para mostrar contenido  relevante o para iniciar un flujo de autenticación, consulte [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).

## <a name="bots"></a>bots

**Opcional:** matriz

Define una solución de bot, junto con información opcional, como las propiedades de comando predeterminadas.

El elemento es una matriz (máximo de solo 1 elemento actualmente solo se permite un bot por aplicación) con todos los &mdash; elementos del tipo `object` . Este bloque solo es necesario para las soluciones que proporcionan una experiencia de bot.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`botId`|string|64 caracteres|✔|El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework. Esto bien puede ser el mismo que el identificador general [de la aplicación](#id).|
|`scopes`|matriz de enumeraciones|3|✔|Especifica si el bot ofrece una experiencia en el contexto de un canal en un `team`, en un chat de grupo (`groupchat`) o una experiencia específica para un solo usuario (`personal`). Estas opciones no son exclusivas.|
|`needsChannelSelector`|boolean|||Describe si el bot usa una sugerencia del usuario para agregar el bot a un canal específico. Valor predeterminado: **`false`**|
|`isNotificationOnly`|boolean|||Indica si un bot es un bot unidireccional de solo notificación o un bot de conversación. Valor predeterminado: **`false`**|
|`supportsFiles`|boolean|||Indica si el bot es compatible con la capacidad para cargar y descargar archivos en chat personal. Valor predeterminado: **`false`**|
|`supportsCalling`|boolean|||Valor que indica dónde un bot admite llamadas de audio. **IMPORTANTE:** Esta propiedad es actualmente experimental. Es posible que las propiedades experimentales no estén completas y que se someten a cambios antes de estar totalmente disponibles.  Se proporciona solo con fines de prueba y exploración y no debe usarse en aplicaciones de producción. Valor predeterminado: **`false`**|
|`supportsVideo`|boolean|||Valor que indica dónde un bot admite videollamadas. **IMPORTANTE:** Esta propiedad es actualmente experimental. Es posible que las propiedades experimentales no estén completas y que se someten a cambios antes de estar totalmente disponibles.  Se proporciona solo con fines de prueba y exploración y no debe usarse en aplicaciones de producción. Valor predeterminado: **`false`**|

### <a name="botscommandlists"></a>bots.commandLists

Una lista opcional de comandos que el bot puede recomendar a los usuarios. El objeto es una matriz (máximo de 2 elementos) con todos los elementos de tipo; debe definir una lista de comandos independiente para cada ámbito compatible `object` con el bot. Consulta [Menús bot para](~/bots/how-to/create-a-bot-commands-menu.md) obtener más información.

|Nombre| Tipo| Tamaño máximo | Necesario | Description|
|---|---|---|---|---|
|`items.scopes`|matriz de enumeraciones|3|✔|Especifica el ámbito para el que la lista de comandos es válida. Las opciones son `team`, `personal` y `groupchat`.|
|`items.commands`|matriz de objetos|10|✔|Una matriz de comandos que el bot admite:<br>`title`: el nombre de comando del bot (cadena, 32)<br>`description`: una descripción o un ejemplo sencillo de la sintaxis del comando y su argumento (cadena, 128).|

### <a name="botscommandlistscommands"></a>bots.commandLists.commands

|Nombre| Tipo| Tamaño máximo | Necesario | Description|
|---|---|---|---|---|
|title|string|12 |✔|Nombre del comando bot|
|description|cadena|128 caracteres|✔|Una descripción de texto simple o un ejemplo de la sintaxis del comando y sus argumentos.|

## <a name="connectors"></a>conectores

**Opcional:** matriz

El `connectors` bloque define un Office 365 connector para la aplicación.

El objeto es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` . Este bloque solo es necesario para las soluciones que proporcionan un conector.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`configurationUrl`|string|2048 caracteres|✔|La https:// url que se va a usar al configurar el conector.|
|`scopes`|matriz de enumeraciones|1|✔|Especifica si connector ofrece una experiencia en el contexto de un canal en un , o una experiencia ámbito a un `team` usuario individual solo ( `personal` ). Actualmente, solo se `team` admite el ámbito.|
|`connectorId`|cadena|64 caracteres|✔|Identificador único del conector que coincide con su identificador en el [Panel de desarrolladores de conectores.](https://aka.ms/connectorsdashboard)|

## <a name="composeextensions"></a>composeExtensions

**Opcional:** matriz

Define una extensión de mensajería para la aplicación.

> [!NOTE]
> El nombre de la característica se cambió de "extensión de redacción" a "extensión de mensajería" en noviembre de 2017, pero el nombre del manifiesto sigue siendo el mismo para que las extensiones existentes sigan funcionando.

El elemento es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` . Este bloque solo es necesario para las soluciones que proporcionan una extensión de mensajería.

|Nombre| Tipo | Tamaño máximo | Obligatorio | Descripción|
|---|---|---|---|---|
|`botId`|string|64|✔|El identificador único de la aplicación de Microsoft para el bot que hace una copia de seguridad de la extensión de mensajería, tal como se registró con Bot Framework. Esto bien puede ser el mismo que el identificador general de la aplicación.|
|`commands`|matriz de objetos|10|✔|Matriz de comandos que admite la extensión de mensajería|
|`canUpdateConfiguration`|boolean|||Valor que indica si el usuario puede actualizar la configuración de una extensión de mensajería. Valor predeterminado: **false**.|
|`messageHandlers`|matriz de objetos|5 ||Una lista de controladores que permiten invocar aplicaciones cuando se cumplen determinadas condiciones.|
|`messageHandlers.type`|cadena|||El tipo de controlador de mensajes. Debe ser `"link"`.|
|`messageHandlers.value.domains`|matriz de cadenas|||Matriz de dominios para los que se puede registrar el controlador de mensajes de vínculo.|

### <a name="composeextensionscommands"></a>composeExtensions.commands

La extensión de mensajería debe declarar uno o varios comandos. Cada comando aparece en Microsoft Teams como una interacción potencial desde el punto de entrada basado en la interfaz de usuario. Hay un máximo de 10 comandos.

Cada elemento de comando es un objeto con la siguiente estructura:

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`id`|string|64 caracteres|✔|El identificador del comando.|
|`title`|cadena|32 caracteres|✔|Nombre de comando fácil de usar.|
|`type`|cadena|64 caracteres||Tipo del comando. Uno de `query` o `action` . Valor predeterminado: **consulta**.|
|`description`|cadena|128 caracteres||La descripción que se muestra a los usuarios para indicar el propósito de este comando.|
|`initialRun`|boolean|||Un valor booleano indica si el comando se ejecuta inicialmente sin parámetros. El valor predeterminado es **false**.|
|`context`|matriz de cadenas|3||Define desde dónde se puede invocar la extensión de mensaje. Cualquier combinación de `compose` , `commandBox` , `message` . El valor predeterminado es `["compose","commandBox"]`.|
|`fetchTask`|boolean|||Valor booleano que indica si debe capturar el módulo de tareas dinámicamente. El valor predeterminado es **false**.|
|`taskInfo`|object|||Especifique el módulo de tareas que se debe cargar previamente al usar un comando de extensión de mensajería.|
|`taskInfo.title`|cadena|64 caracteres||Título del cuadro de diálogo inicial.|
|`taskInfo.width`|cadena|||Ancho del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "mediano" o "pequeño".|
|`taskInfo.height`|cadena|||Alto del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "mediano" o "pequeño".|
|`taskInfo.url`|cadena|||Dirección URL de vista web inicial.|
|`parameters`|matriz de objeto|5 elementos|✔|La lista de parámetros que toma el comando. Mínimo: 1; máximo: 5.|
|`parameters.name`|cadena|64 caracteres|✔|Nombre del parámetro tal como aparece en el cliente. Esto se incluye en la solicitud de usuario.|
|`parameters.title`|cadena|32 caracteres|✔|Título fácil de usar para el parámetro.|
|`parameters.description`|cadena|128 caracteres||Cadena fácil de usar que describe el propósito de este parámetro.|
|`parameters.value`|cadena|512 caracteres||Valor inicial del parámetro.|
|`parameters.inputType`|cadena|128 caracteres||Define el tipo de control que se muestra en un módulo de tareas para `fetchTask: true` . Uno de `text, textarea, number, date, time, toggle, choiceset` .|
|`parameters.choices`|matriz de objetos|10 elementos||Las opciones de elección para `choiceset` el archivo . Use solo cuando `parameter.inputType` es `choiceset` .|
|`parameters.choices.title`|cadena|128 caracteres|✔|Título de la elección.|
|`parameters.choices.value`|cadena|512 caracteres|✔|Valor de la elección.|

## <a name="permissions"></a>permisos

**Opcional:** matriz de cadenas

Una matriz de los cuales especifica qué permisos solicita la aplicación, lo que permite a los usuarios `string` finales saber cómo funciona la extensión. Las siguientes opciones no son exclusivas:

* `identity`&emsp;Requiere información de identidad de usuario
* `messageTeamMembers`&emsp;Requiere permiso para enviar mensajes directos a miembros del equipo

Al cambiar estos permisos durante la actualización de la aplicación, los usuarios repiten el proceso de consentimiento después de ejecutar la aplicación actualizada. Consulta [Actualizar la aplicación para](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) obtener más información.

## <a name="devicepermissions"></a>devicePermissions

**Opcional:** matriz de cadenas

Proporciona las características nativas en el dispositivo de un usuario al que la aplicación solicita acceso. Las opciones son:

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**Opcional**, excepto **Requerido cuando** se indica

Una lista de dominios válidos para sitios web que la aplicación espera cargar en el Teams cliente. Las listas de dominios pueden incluir caracteres comodín, por ejemplo, `*.example.com` . Esto coincide exactamente con un segmento del dominio; si necesita hacer `a.b.example.com` coincidir, use `*.*.example.com` . Si la interfaz de usuario de contenido o configuración de pestañas necesita navegar a cualquier otro dominio además del uso para la configuración de pestañas, este dominio debe especificarse aquí.

No es **necesario** incluir los dominios de los proveedores de identidades que quieres admitir en la aplicación. Por ejemplo, para autenticar con un identificador de Google, es necesario redirigir a accounts.google.com, sin embargo, no debe incluir accounts.google.com en `validDomains[]` .

Teams aplicaciones que requieren que sus propias direcciones URL de sharepoint funcionen correctamente, incluye "{teamsitedomain}" en su lista de dominios válida.

> [!IMPORTANT]
> No agregue dominios que estén fuera del control, ya sea directamente o a través de caracteres comodín. Por ejemplo, `yourapp.onmicrosoft.com` es válido, sin embargo, `*.onmicrosoft.com` no es válido.

El objeto es una matriz con todos los elementos del tipo `string` .

## <a name="webapplicationinfo"></a>webApplicationInfo

**Opcional** : objeto

Proporcione su Azure Active Directory de aplicación (AAD) y microsoft Graph información para ayudar a los usuarios a iniciar sesión sin problemas en la aplicación. Si la aplicación está registrada en AAD, debes proporcionar el identificador de la aplicación, para que los administradores puedan revisar fácilmente los permisos y conceder el consentimiento en Teams centro de administración.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`id`|string|36 caracteres|✔|Id. de aplicación de AAD de la aplicación. Este identificador debe ser un GUID.|
|`resource`|cadena|2048 caracteres|✔|Dirección URL de recurso de la aplicación para adquirir token de autenticación para SSO. </br> **NOTA:** Si no usa SSO, asegúrese de escribir un valor de cadena ficticia en este campo en el manifiesto de la aplicación, por ejemplo, para evitar https://notapplicable una respuesta de error. |
|`applicationPermissions`|matriz de cadenas|128 caracteres||Especifique el consentimiento [específico del recurso pormenorizados](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).|

## <a name="showloadingindicator"></a>showLoadingIndicator

**Opcional:** booleano

Indica si se va a mostrar el indicador de carga cuando se carga una aplicación o una pestaña. El valor predeterminado es **false**.
>[!NOTE]
>Si seleccionas como true en el manifiesto de la aplicación, para cargar la página correctamente, modifica las páginas de contenido de las pestañas y los módulos de tareas como se describe en Mostrar un documento de indicador de carga `showLoadingIndicator` nativo. [](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)


## <a name="isfullscreen"></a>isFullScreen

 **Opcional:** booleano

Indica dónde se representa una aplicación personal con o sin una barra de encabezado de pestaña. El valor predeterminado es **false**.

## <a name="activities"></a>activities

**Opcional** : objeto

Define las propiedades que usa la aplicación para publicar una fuente de actividad de usuario.

|Nombre| Tipo| Tamaño máximo | Necesario | Description|
|---|---|---|---|---|
|`activityTypes`|matriz de objetos|128 elementos| | Proporciona los tipos de actividades que la aplicación puede publicar en una fuente de actividad de usuarios.|

### <a name="activitiesactivitytypes"></a>activities.activityTypes

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`type`|string|32 caracteres|✔|Tipo de notificación. *Vea a continuación*.|
|`description`|cadena|128 caracteres|✔|Breve descripción de la notificación. *Vea a continuación*.|
|`templateText`|cadena|128 caracteres|✔|Ex: "{actor} created task {taskId} for you"|

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

**Opcional** : cadena

Especifica el ámbito de instalación definido para esta aplicación de forma predeterminada. El ámbito definido será la opción que se muestra en el botón cuando un usuario intente agregar la aplicación. Las opciones son:
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a>defaultGroupCapability

**Opcional** : objeto

Cuando se selecciona un ámbito de instalación de grupo, se definirá la funcionalidad predeterminada cuando el usuario instale la aplicación. Las opciones son:
* `team`
* `groupchat`
* `meetings`
 
|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`team`|string|||Cuando el ámbito de instalación seleccionado es `team` , este campo especifica la funcionalidad predeterminada disponible. Opciones: `tab` `bot` , o `connector` .|
|`groupchat`|cadena|||Cuando el ámbito de instalación seleccionado es `groupchat` , este campo especifica la funcionalidad predeterminada disponible. Opciones: `tab` `bot` , o `connector` .|
|`meetings`|cadena|||Cuando el ámbito de instalación seleccionado es `meetings` , este campo especifica la funcionalidad predeterminada disponible. Opciones: `tab` `bot` , o `connector` .|

## <a name="configurableproperties"></a>configurableProperties

**Opcional** : matriz

El `configurableProperties` bloque define las propiedades de la aplicación que Teams puede personalizar el administrador. Para obtener más información, consulta [Personalizar aplicaciones en Microsoft Teams](/MicrosoftTeams/customize-apps).

> [!NOTE]
> Debe definirse un mínimo de una propiedad. Puede definir un máximo de nueve propiedades en este bloque.
> Como práctica recomendada, debes proporcionar directrices de personalización para que los usuarios de la aplicación y los clientes puedan seguir al personalizar la aplicación.

Puede definir cualquiera de las siguientes propiedades:
* `name`: permite al administrador cambiar el nombre para mostrar de la aplicación.
* `shortDescription`: permite al administrador cambiar la descripción breve de la aplicación.
* `longDescription`: permite al administrador cambiar la descripción detallada de la aplicación.
* `smallImageUrl`: es la `outline` propiedad del bloque del `icons` manifiesto.
* `largeImageUrl`: es la `color` propiedad del bloque del `icons` manifiesto.
* `accentColor`: es el color que se debe usar junto con y como fondo para los iconos de esquema.
* `websiteUrl`: es la dirección HTTPS:// url del sitio web del desarrollador.
* `privacyUrl`: es la dirección URL https:// a la directiva de privacidad del desarrollador.
* `termsOfUseUrl`: es la dirección URL https:// los términos de uso del desarrollador.



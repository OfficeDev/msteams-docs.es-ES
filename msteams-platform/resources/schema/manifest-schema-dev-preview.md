---
title: Referencia del esquema del manifiesto de versión preliminar del desarrollador
description: Describe el esquema admitido por el manifiesto de Microsoft Teams
ms.topic: reference
keywords: Vista previa del programador del esquema de manifiesto de teams
ms.date: 05/20/2019
ms.openlocfilehash: 0776ced1704f46c95054308c8a1898ed938e47cb
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014106"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a>Esquema de manifiesto de versión preliminar para desarrolladores de Microsoft Teams

> [!NOTE]
> Consulta [developer preview](~/resources/dev-preview/developer-preview-intro.md) para obtener información sobre el programa y cómo puedes unirte.
> Si no usa la vista previa del desarrollador, no debería usar esta versión del manifiesto. See [Reference: Manifest schema for Microsoft Teams](~/resources/schema/manifest-schema.md) for the public version of the manifest.

El manifiesto de Microsoft Teams describe cómo se integra la aplicación en el producto de Microsoft Teams. El manifiesto debe cumplir con el esquema hospedado en [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) .

Para obtener más información sobre las características disponibles, vea: Características en la versión preliminar [para desarrolladores públicos de Microsoft Teams.](~/resources/dev-preview/developer-preview-features.md)

## <a name="sample-full-manifest"></a>Manifiesto completo de ejemplo

```json
{
  "$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
  "manifestVersion": "devPreview",
  "version": "1.0.0",
  "id": "%MICROSOFT-APP-ID%",
  "packageName": "com.example.myapp",
  "devicePermissions" : [ "geolocation", "media" ],
  "developer": {
    "name": "Publisher Name",
    "websiteUrl": "https://website.com/",
    "privacyUrl": "https://website.com/privacy",
    "termsOfUseUrl": "https://website.com/app-tos",
    "mpnId": "1234567890"
  },
  "localizationInfo": {
    "defaultLanguageTag": "es-es",
    "additionalLanguages": [
      {
        "languageTag": "en-us",
        "file": "en-us.json"
      }
    ]
  },
  "name": {
    "short": "Name of your app (<=30 chars)",
    "full": "Full name of app, if longer than 30 characters"
  },
  "description": {
    "short": "Short description of your app",
    "full": "Full description of your app"
  },
  "icons": {
    "outline": "%FILENAME-32x32px%",
    "color": "%FILENAME-192x192px"
  },
  "accentColor": "%HEX-COLOR%",
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [ "team", "groupchat" ]
    }
  ],
  "staticTabs": [
    {
      "entityId": "idForPage",
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content?host=msteams",
      "websiteUrl": "https://contoso.com/content",
      "scopes": [ "personal" ]
    }
  ],
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "scopes": [ "team", "personal", "groupchat" ],
      "supportsFiles": true,
      "commandLists": [
        {
          "scopes": [ "team", "groupchat" ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command N",
              "description": "Description of Command N"
            }
          ]
        },
        {
          "scopes": [ "personal", "groupchat" ],
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
      "configurationUrl": "https://contoso.com/teamsconnector/configure",
      "scopes": [ "team"]
    }
  ],
  "composeExtensions": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "exampleCmd1",
          "title": "Example Command",
          "description": "Command Description; e.g., Search on the web",
          "initialRun": true,
          "type" : "search",
          "context" : ["compose", "commandBox"],
          "parameters": [
            {
              "name": "keyword",
              "title": "Search keywords",
              "description": "Enter the keywords to search for"
            }
          ]
        },
        {
          "id": "exampleCmd2",
          "title": "Example Command 2",
          "description": "Command Description; e.g., Search for a customer",
          "initialRun": true,
          "type" : "action",
          "fetchTask" : true,
          "context" : ["message"],
          "parameters": [
            {
              "name": "custinfo",
              "title": "Customer name",
              "description": "Enter a customer name",
              "inputType" : "text"
            }
          ]
        },
        {
          "id": "exampleMessageHandler",
          "title": "Message Handler",
          "description": "Domains that will create a preview when pasted into the compose box",
          "messageHandlers": [
            {
              "type" : "link",
              "value" : {
                "domains" : [
                  "mysite.someplace.com",
                  "othersite.someplace.com"
                ]
              }
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers",
  ],
  "validDomains": [
     "contoso.com",
     "mysite.someplace.com",
     "othersite.someplace.com"
  ]
}
```

El esquema define las siguientes propiedades:

## <a name="schema"></a>$schema

*Opcional, pero recomendado* &ndash; String

La https:// URL que hace referencia al esquema JSON del manifiesto.

## <a name="manifestversion"></a>manifestVersion

**Obligatorio** &ndash; String

La versión del esquema de manifiesto que usa este manifiesto. Debe ser "devPreview".

## <a name="version"></a>version

**Obligatorio** &ndash; String

La versión de la aplicación específica. Si actualiza algo en el manifiesto, también debe incrementarse la versión. De este modo, cuando se instale el nuevo manifiesto, se sobrescribirá el anterior y el usuario podrá disfrutar de las funciones nuevas. Si esta aplicación se envió a la tienda, el nuevo manifiesto tendrá que volver a enviarse y validarse. A continuación, los usuarios de esta aplicación recibirán el nuevo manifiesto actualizado automáticamente en unas horas, después de su aprobación.

Si la aplicación solicitó cambios en los permisos, se pedirá a los usuarios que actualicen y vuelvan a dar su consentimiento a la aplicación.

Esta cadena de versión debe seguir el [estándar semver](http://semver.org/) (MAJOR. MINOR. PATCH).

## <a name="id"></a>id

**Obligatorio** &ndash; Id. de aplicación de Microsoft

Identificador único generado por Microsoft para esta aplicación. Si ha registrado un bot a través de Microsoft Bot Framework o la aplicación web de la pestaña ya inicia sesión con Microsoft, ya debe tener un identificador y debe escribirlo aquí. De lo contrario, debe generar un nuevo identificador en el Portal de registro de aplicaciones de Microsoft[(Mis](https://apps.dev.microsoft.com)aplicaciones), escribirlo aquí y, a continuación, volver a usarlo cuando [agregue un bot.](~/bots/how-to/create-a-bot-for-teams.md)

## <a name="packagename"></a>packageName

**Obligatorio** &ndash; String

Un identificador único para esta aplicación en la notación de dominio inverso; por ejemplo, com.example.myapp.

## <a name="developer"></a>developer

**Required**

Especifica información sobre su empresa. Para las aplicaciones enviadas a AppSource (anteriormente Tienda Office), estos valores deben coincidir con la información de la entrada de AppSource.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`name`|32 caracteres|✔|Nombre para mostrar del desarrollador.|
|`websiteUrl`|2048 caracteres|✔|La https:// url del sitio web del desarrollador. Este vínculo debe llevar a los usuarios a su empresa o página de aterrizaje específica del producto.|
|`privacyUrl`|2048 caracteres|✔|La https:// url a la directiva de privacidad del desarrollador.|
|`termsOfUseUrl`|2048 caracteres|✔|La https:// url a los términos de uso del desarrollador.|
|`mpnId`|10 caracteres|✔|**Opcional** El id. de Microsoft Partner Network que identifica la organización asociada que está creando la aplicación.|

## <a name="localizationinfo"></a>localizationInfo

**Optional**

Permite especificar un idioma predeterminado, así como punteros a archivos de idioma adicionales. Vea [localización.](~/concepts/build-and-test/apps-localization.md)

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`defaultLanguageTag`|4 caracteres|✔|La etiqueta de idioma de las cadenas de este archivo de manifiesto de nivel superior.|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

Matriz de objetos que especifica traducciones de idioma adicionales.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`languageTag`|4 caracteres|✔|La etiqueta de idioma de las cadenas en el archivo proporcionado.|
|`file`|4 caracteres|✔|Una ruta de acceso de archivo relativa a un archivo .json que contiene las cadenas traducidas.|

## <a name="name"></a>name

**Required**

El nombre de la experiencia de la aplicación, que se muestra a los usuarios en la experiencia de Teams. Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada de AppSource. Los valores de `short` y no deben ser los `full` mismos.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`short`|30 caracteres|✔|Nombre corto para mostrar de la aplicación.|
|`full`|100 caracteres||El nombre completo de la aplicación, que se usa si el nombre completo de la aplicación supera los 30 caracteres.|

## <a name="description"></a>descripción

**Required**

Describe la aplicación a los usuarios. Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada de AppSource.

Asegúrate de que la descripción describa con precisión tu experiencia y proporciona información para ayudar a los clientes potenciales a comprender lo que hace tu experiencia. También debe tener en cuenta, en la descripción completa, si se requiere una cuenta externa para su uso. Los valores de `short` y no deben ser los `full` mismos.  La descripción breve no debe repetirse dentro de la descripción larga y no debe incluir ningún otro nombre de aplicación.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`short`|80 caracteres|✔|Una breve descripción de la experiencia de la aplicación, que se usa cuando el espacio es limitado.|
|`full`|4000 caracteres|✔|Descripción completa de la aplicación.|

## <a name="icons"></a>iconos

**Required**

Iconos usados dentro de la aplicación teams. Los archivos de icono deben incluirse como parte del paquete de carga.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`outline`|2048 caracteres|✔|Una ruta de acceso de archivo relativa a un icono de esquema PNG transparente de 32 x 32.|
|`color`|2048 caracteres|✔|Una ruta de acceso de archivo relativa a un icono PNG de color completo de 192 x 192.|

## <a name="accentcolor"></a>accentColor

**Obligatorio** &ndash; String

Color que se usa junto con los iconos de esquema y como fondo.

El valor debe ser un código de color HTML válido que comience por '#', por `#4464ee` ejemplo.

## <a name="configurabletabs"></a>configurableTabs

**Optional**

Se usa cuando la experiencia de la aplicación tiene una experiencia de pestaña de canal de equipo que requiere configuración adicional antes de agregarla. Las pestañas configurables solo se admiten en el ámbito de teams y actualmente solo se admite una pestaña por aplicación.

El objeto es una matriz con todos los elementos del tipo `object` . Este bloque solo es necesario para las soluciones que proporcionan una solución de pestaña de canal configurable.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`configurationUrl`|Cadena|2048 caracteres|✔|La https:// url que se va a usar al configurar la pestaña.|
|`canUpdateConfiguration`|Boolean|||Valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de su creación. Valor predeterminado: `true`|
|`scopes`|Matriz de enumeración|1 |✔|Actualmente, las pestañas configurables solo admiten `team` los `groupchat` ámbitos y los ámbitos. |
|`sharePointPreviewImage`|Cadena|2048||Una ruta de acceso de archivo relativa a una imagen de vista previa de pestaña para su uso en SharePoint. Tamaño 1024 x 768. |
|`supportedSharePointHosts`|Matriz de enumeración|1 ||Define cómo estará disponible la pestaña en SharePoint. Las opciones son `sharePointFullPage` y `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**Optional**

Define un conjunto de pestañas que se pueden "anclar" de forma predeterminada, sin que el usuario las agregue manualmente. Las pestañas estáticas declaradas en el ámbito `personal` siempre se anclan a la experiencia personal de la aplicación. Las pestañas estáticas declaradas en `team` el ámbito no se admiten actualmente.

El objeto es una matriz (máximo de 16 elementos) con todos los elementos del tipo `object` . Este bloque solo es necesario para las soluciones que proporcionan una solución de pestaña estática.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`entityId`|String|64 caracteres|✔|Identificador único de la entidad que muestra la pestaña.|
|`name`|Cadena|128 caracteres|✔|Nombre para mostrar de la pestaña en la interfaz de canal.|
|`contentUrl`|Cadena|2048 caracteres|✔|La https:// url que apunta a la interfaz de usuario de la entidad que se mostrará en el lienzo de Teams.|
|`websiteUrl`|Cadena|2048 caracteres||La https:// url que debe señalar si un usuario opta por ver en un explorador.|
|`scopes`|Matriz de enumeración|1 |✔|Actualmente, las pestañas estáticas solo admiten el ámbito, lo que significa que solo se pueden aprovisionar como `personal` parte de la experiencia personal.|

## <a name="bots"></a>bots

**Optional**

Define una solución de bot, junto con información opcional, como las propiedades de comandos predeterminadas.

El objeto es una matriz (actualmente solo se permite un elemento de un bot por aplicación) con todos los &mdash; elementos del tipo `object` . Este bloque solo es necesario para las soluciones que proporcionan una experiencia de bot.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`botId`|String|64 caracteres|✔|El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework. Esto puede ser igual que el identificador general [de la aplicación.](#id)|
|`needsChannelSelector`|Booleano|||Describe si el bot usa una sugerencia del usuario para agregar el bot a un canal específico. Valor predeterminado: `false`|
|`isNotificationOnly`|Booleano|||Indica si un bot es un bot unidireccional de solo notificación o un bot de conversación. Valor predeterminado: `false`|
|`supportsFiles`|Booleano|||Indica si el bot es compatible con la capacidad para cargar y descargar archivos en chat personal. Valor predeterminado: `false`|
|`scopes`|Matriz de enumeración|3|✔|Especifica si el bot ofrece una experiencia en el contexto de un canal en un `team`, en un chat de grupo (`groupchat`) o una experiencia específica para un solo usuario (`personal`). Estas opciones no son exclusivas.|

### <a name="botscommandlists"></a>bots.commandLists

Una lista opcional de comandos que el bot puede recomendar a los usuarios. El objeto es una matriz (máximo de 2 elementos) con todos los elementos de tipo; debe definir una lista de comandos independiente para cada ámbito compatible `object` con el bot. Vea [los menús del bot](~/bots/how-to/create-a-bot-commands-menu.md) para obtener más información.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`items.scopes`|matriz de enumeración|3|✔|Especifica el ámbito para el que la lista de comandos es válida. Las opciones son `team`, `personal` y `groupchat`.|
|`items.commands`|matriz de objetos|10 |✔|Una matriz de comandos que el bot admite:<br>`title`: el nombre de comando del bot (cadena, 32)<br>`description`: una descripción o un ejemplo sencillo de la sintaxis del comando y su argumento (cadena, 128).|

## <a name="connectors"></a>conectores

**Optional**

El `connectors` bloque define un conector de Office 365 para la aplicación.

El objeto es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` . Este bloque solo es necesario para las soluciones que proporcionan un conector.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`configurationUrl`|Cadena|2048 caracteres|✔|La https:// url que se va a usar al configurar el conector.|
|`connectorId`|String|64 caracteres|✔|Un identificador único para el conector que coincide con su identificador en el panel del programador [de conectores.](https://aka.ms/connectorsdashboard)|
|`scopes`|Matriz de enumeración|1 |✔|Especifica si el conector ofrece una experiencia en el contexto de un canal en un , o una experiencia en el ámbito de `team` un usuario individual solo ( `personal` ). Actualmente, solo se `team` admite el ámbito.|

## <a name="composeextensions"></a>composeExtensions

**Optional**

Define una extensión de mensajería para la aplicación.

> [!NOTE]
> The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.

El objeto es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` . Este bloque solo es necesario para las soluciones que proporcionan una extensión de mensajería.

|Nombre| Tipo | Tamaño máximo | Obligatorio | Descripción|
|---|---|---|---|---|
|`botId`|Cadena|64|✔|El identificador de aplicación de Microsoft único para el bot que hace una copia de seguridad de la extensión de mensajería, tal como se registró con Bot Framework. Esto puede ser igual que el identificador general [de la aplicación.](#id)|
|`canUpdateConfiguration`|Boolean|||Valor que indica si el usuario puede actualizar la configuración de una extensión de mensajería. El valor predeterminado es `false` .|
|`commands`|Matriz de objeto|10 |✔|Matriz de comandos que admite la extensión de mensajería|

### <a name="composeextensionscommands"></a>composeExtensions.commands

La extensión de mensajería debe declarar uno o más comandos. Cada comando aparece en Microsoft Teams como una posible interacción desde el punto de entrada basado en la interfaz de usuario. Hay un máximo de 10 comandos.

Cada elemento de comando es un objeto con la estructura siguiente:

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`id`|String|64 caracteres|✔|El identificador del comando|
|`type`|String|64 caracteres||Tipo del comando. Uno de `query` o `action` . Valor predeterminado: `query`|
|`title`|Cadena|32 caracteres|✔|El nombre de comando fácil de usar|
|`description`|Cadena|128 caracteres||La descripción que los usuarios parecen indicar el propósito de este comando|
|`initialRun`|Boolean|||Un valor booleano que indica si el comando debe ejecutarse inicialmente sin parámetros. Valor predeterminado: `false`|
|`context`|Matriz de cadenas|3||Define desde dónde se puede invocar la extensión de mensaje. Cualquier combinación `compose` de , `commandBox` `message` . El valor predeterminado es `["compose", "commandBox"]`|
|`fetchTask`|Boolean|||Un valor booleano que indica si debe capturar el módulo de tareas dinámicamente|
|`taskInfo`|Objeto|||Especificar el módulo de tareas que se debe precargar al usar un comando de extensión de mensajería|
|`taskInfo.title`|Cadena|64||Título del cuadro de diálogo inicial|
|`taskInfo.width`|Cadena|||Ancho del cuadro de diálogo: un número en píxeles o un diseño predeterminado, como "grande", "mediano" o "pequeño".|
|`taskInfo.height`|Cadena|||Alto del cuadro de diálogo: un número en píxeles o un diseño predeterminado, como "grande", "mediano" o "pequeño".|
|`taskInfo.url`|Cadena|||Dirección URL de vista web inicial|
|`messageHandlers`|Matriz de objetos|5 ||Una lista de controladores que permiten invocar aplicaciones cuando se cumplen ciertas condiciones. Los dominios también deben aparecer en `validDomains`|
|`messageHandlers.type`|Cadena|||El tipo de controlador de mensajes. Debe ser `"link"`.|
|`messageHandlers.value.domains`|Matriz de cadenas|||Matriz de dominios para los que se puede registrar el controlador de mensajes de vínculo.|
|`parameters`|Matriz de objeto|5 |✔|La lista de parámetros que toma el comando. Mínimo: 1; máximo: 5|
|`parameter.name`|String|64 caracteres|✔|Nombre del parámetro tal como aparece en el cliente. Esto se incluye en la solicitud de usuario.|
|`parameter.title`|Cadena|32 caracteres|✔|Título descriptivo para el parámetro.|
|`parameter.description`|Cadena|128 caracteres||Cadena fácil de usar que describe el propósito de este parámetro.|
|`parameter.inputType`|Cadena|128 caracteres||Define el tipo de control que se muestra en un módulo de tareas para `fetchTask: true` . Uno de `text` , `textarea` , `number` `date` , `time` `toggle``choiceset`|
|`parameter.choices`|Matriz de objetos|10 ||Las opciones de elección para `choiceset` el archivo . Usar solo cuando `parameter.inputType` sea `choiceset`|
|`parameter.choices.title`|Cadena|128||Título de la elección|
|`parameter.choices.value`|Cadena|512||Valor de la elección|

## <a name="permissions"></a>permissions

**Optional**

Una matriz que especifica qué permisos solicita la aplicación, lo que permite a los usuarios finales saber cómo se realizará `string` la extensión. Las siguientes opciones no son exclusivas:

* `identity`&emsp;Requiere información de identidad de usuario
* `messageTeamMembers`&emsp;Requiere permiso para enviar mensajes directos a los miembros del equipo

Al cambiar estos permisos al actualizar la aplicación, los usuarios repetirán el proceso de consentimiento la primera vez que ejecuten la aplicación actualizada.

## <a name="devicepermissions"></a>devicePermissions

**Opcional** Matriz de cadenas

Especifica las características nativas del dispositivo de un usuario a las que la aplicación puede solicitar acceso. Las opciones son:

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**Opcional**, excepto **requerido cuando** se indica

Una lista de dominios válidos desde los que la aplicación espera cargar cualquier contenido. Las listas de dominios pueden incluir caracteres comodín, por `*.example.com` ejemplo. Esto coincide exactamente con un segmento del dominio; si necesita hacer coincidir, `a.b.example.com` use `*.*.example.com` . Si la configuración de la pestaña o la interfaz de usuario de contenido necesitan navegar a cualquier otro dominio aparte del que se usa para la configuración de pestañas, ese dominio debe especificarse aquí.

No **obstante,** no es necesario incluir los dominios de proveedores de identidades que desea admitir en la aplicación. Por ejemplo, para autenticarse con un id. de Google, es necesario redirigir a accounts.google.com, pero no debe incluir accounts.google.com `validDomains[]` en .

> [!IMPORTANT]
> No agregue dominios que estén fuera de su control, ya sea directamente o a través de caracteres comodín. Por ejemplo, `yourapp.onmicrosoft.com` es válido, pero `*.onmicrosoft.com` no es válido.

El objeto es una matriz con todos los elementos del tipo `string` .

## <a name="webapplicationinfo"></a>webApplicationInfo

**Optional**

Especifique su id. de aplicación de AAD y la información de Graph para ayudar a los usuarios a iniciar sesión sin problemas en su aplicación de AAD.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`id`|Cadena|36 caracteres|✔|Id. de aplicación de AAD de la aplicación. Este identificador debe ser un GUID.|
|`resource`|Cadena|2048 caracteres|✔|Dirección URL de recurso de la aplicación para adquirir un token de autenticación para SSO.|
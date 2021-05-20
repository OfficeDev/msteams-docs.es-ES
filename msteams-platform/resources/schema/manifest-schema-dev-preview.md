---
title: Referencia de esquema de manifiesto de vista previa del desarrollador
description: Describe el esquema admitido por el manifiesto para Microsoft Teams
ms.topic: reference
keywords: equipos manifiestan esquema Developer Preview
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: b52d52f96312dc2978844b07a0f7ebb1d817166d
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566708"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a>Esquema de manifiesto de vista previa del desarrollador para Microsoft Teams

> [!NOTE]
> Consulte [Vista previa para desarrolladores](~/resources/dev-preview/developer-preview-intro.md) para obtener información sobre el programa y cómo puede unirse.
> Si no está utilizando la vista previa del desarrollador, no debería usar esta versión del manifiesto. Consulte [Referencia: esquema de manifiesto para Microsoft Teams](~/resources/schema/manifest-schema.md) para la versión pública del manifiesto.

El manifiesto Microsoft Teams describe cómo se integra la aplicación en el producto Microsoft Teams. El manifiesto debe ajustarse al esquema hospedado en [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) .

Para obtener más información sobre las características disponibles, consulte: [Características de la vista previa del desarrollador público para Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).

## <a name="sample-full-manifest"></a>Muestra de manifiesto completo

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
  ],
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
  ],
  "defaultInstallScope": "meetings",
  "defaultGroupCapability": {
    "meetings": "tab", 
    "team": "bot", 
    "groupchat": "bot"
  }
}
```

El esquema define las siguientes propiedades:

## <a name="schema"></a>$schema

*Opcional, pero recomendado* &ndash; cuerda

La dirección URL https:// que hace referencia al esquema JSON del manifiesto.

## <a name="manifestversion"></a>manifestVersion

**Requerido** &ndash; cuerda

La versión del esquema de manifiesto que este manifiesto está utilizando. Debe ser "devPreview".

## <a name="version"></a>version

**Requerido** &ndash; cuerda

La versión de la aplicación específica. Si actualiza algo en el manifiesto, la versión también debe incrementarse. De este modo, cuando se instale el nuevo manifiesto, se sobrescribirá el anterior y el usuario podrá disfrutar de las funciones nuevas. Si esta aplicación se envió a la tienda, el nuevo manifiesto tendrá que volver a enviarse y volver a validarse. A continuación, los usuarios de esta aplicación obtendrán el nuevo manifiesto actualizado automáticamente en unas horas, después de que se apruebe.

Si cambian los permisos solicitados por la aplicación, se pedirá a los usuarios que actualicen y vuelvan a dar su consentimiento a la aplicación.

Esta cadena de versión debe seguir el estándar [de semver](http://semver.org/) (MAJOR. menor. PARCHE).

## <a name="id"></a>id

**Requerido** &ndash; Identificador de aplicación de Microsoft

El identificador único generado por Microsoft para esta aplicación. Si ha registrado un bot a través de la Microsoft Bot Framework, o la aplicación web de su pestaña ya inicia sesión con Microsoft, ya debe tener un IDENTIFICADOR y debe introducirlo aquí. De lo contrario, debe generar un nuevo identificador en el Portal de registro de aplicaciones de Microsoft ([Mis aplicaciones](https://apps.dev.microsoft.com)), escribirlo aquí y, a continuación, reutilizarlo al agregar [un bot](~/bots/how-to/create-a-bot-for-teams.md).

## <a name="packagename"></a>packageName

**Requerido** &ndash; cuerda

Un identificador único para esta aplicación en notación de dominio inverso; por ejemplo, com.example.myapp.

## <a name="developer"></a>developer

**Required**

Especifica información sobre su empresa. Para las aplicaciones enviadas a AppSource (anteriormente Office Store), estos valores deben coincidir con la información de la entrada de AppSource.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`name`|32 caracteres|✔|El nombre para mostrar del desarrollador.|
|`websiteUrl`|2048 caracteres|✔|La URL de https:// al sitio web del desarrollador. Este enlace debe llevar a los usuarios a su empresa o página de destino específica del producto.|
|`privacyUrl`|2048 caracteres|✔|La dirección URL de https:// a la política de privacidad del desarrollador.|
|`termsOfUseUrl`|2048 caracteres|✔|La dirección URL https:// a los términos de uso del desarrollador.|
|`mpnId`|10 caracteres|✔|**Opcional** Identificador de red de partners de Microsoft que identifica la organización asociada que compilará la aplicación.|

## <a name="localizationinfo"></a>localizaciónInfo

**Optional**

Permite la especificación de un idioma predeterminado, así como punteros a archivos de idioma adicionales. Consulte [localización](~/concepts/build-and-test/apps-localization.md).

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`defaultLanguageTag`|4 caracteres|✔|La etiqueta de idioma de las cadenas de este archivo de manifiesto de nivel superior.|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

Matriz de objetos que especifica traducciones de idioma adicionales.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`languageTag`|4 caracteres|✔|La etiqueta de idioma de las cadenas del archivo proporcionado.|
|`file`|4 caracteres|✔|Una ruta de acceso de archivo relativa a un archivo .json que contiene las cadenas traducidas.|

## <a name="name"></a>name

**Required**

El nombre de la experiencia de la aplicación, que se muestra a los usuarios en la experiencia Teams. Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada de AppSource. Los valores de `short` y no deben ser los `full` mismos.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`short`|30 caracteres|✔|El nombre para mostrar corto de la aplicación.|
|`full`|100 caracteres||El nombre completo de la aplicación, utilizado si el nombre completo de la aplicación supera los 30 caracteres.|

## <a name="description"></a>description

**Required**

Describe la aplicación a los usuarios. Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada de AppSource.

Asegúrese de que su descripción describe con precisión su experiencia y proporciona información para ayudar a los clientes potenciales a entender lo que hace su experiencia. También debe tener en cuenta, en la descripción completa, si se requiere una cuenta externa para su uso. Los valores de `short` y no deben ser los `full` mismos.  La breve descripción no debe repetirse dentro de la descripción larga y no debe incluir ningún otro nombre de aplicación.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`short`|80 caracteres|✔|Una breve descripción de la experiencia de la aplicación, utilizada cuando el espacio es limitado.|
|`full`|4000 caracteres|✔|La descripción completa de la aplicación.|

## <a name="icons"></a>iconos

**Required**

Iconos utilizados en la aplicación Teams. Los archivos de icono deben incluirse como parte del paquete de carga.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`outline`|2048 caracteres|✔|Una ruta de acceso de archivo relativa a un icono de contorno PNG 32x32 transparente.|
|`color`|2048 caracteres|✔|Una ruta de acceso de archivo relativa a un icono PNG 192x192 a todo color.|

## <a name="accentcolor"></a>accentColor

**Requerido** &ndash; cuerda

Un color para usar junto con y como fondo para los iconos de contorno.

El valor debe ser un código de color HTML válido que comience por '#', por `#4464ee` ejemplo.

## <a name="configurabletabs"></a>configurableTabs

**Optional**

Se usa cuando la experiencia de la aplicación tiene una experiencia de pestaña de canal de equipo que requiere configuración adicional antes de agregarla. Las pestañas configurables solo se admiten en el ámbito de los equipos y actualmente solo se admite una pestaña por aplicación.

El objeto es una matriz con todos los elementos del tipo `object` . Este bloque solo es necesario para soluciones que proporcionan una solución de pestaña de canal configurable.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`configurationUrl`|Cadena|2048 caracteres|✔|La dirección URL https:// que se usará al configurar la pestaña.|
|`canUpdateConfiguration`|Boolean|||Valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de la creación. predeterminado: `true`|
|`scopes`|Matriz de enumeración|1|✔|Actualmente, las pestañas configurables solo admiten el `team` `groupchat` ámbito. |
|`sharePointPreviewImage`|Cadena|2048||Una ruta de acceso de archivo relativa a una imagen de vista previa de tabulación para su uso en SharePoint. Tamaño 1024x768. |
|`supportedSharePointHosts`|Matriz de enumeración|1||Define cómo se pondrá a disposición su pestaña en SharePoint. Las opciones son `sharePointFullPage` y `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**Optional**

Define un conjunto de pestañas que se pueden "anclar" de forma predeterminada, sin que el usuario las agregue manualmente. Las pestañas estáticas declaradas en `personal` el ámbito siempre están ancladas a la experiencia personal de la aplicación. Actualmente no se admiten pestañas estáticas declaradas en el `team` ámbito.

El objeto es una matriz (máximo de 16 elementos) con todos los elementos del tipo `object` . Este bloque solo es necesario para soluciones que proporcionan una solución de pestaña estática.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`entityId`|String|64 caracteres|✔|Identificador único de la entidad que muestra la pestaña.|
|`name`|Cadena|128 caracteres|✔|El nombre para mostrar de la pestaña en la interfaz del canal.|
|`contentUrl`|Cadena|2048 caracteres|✔|La dirección URL de https:// que apunta a la interfaz de usuario de la entidad que se mostrará en el lienzo de Teams.|
|`websiteUrl`|Cadena|2048 caracteres||La dirección URL https:// a la que apuntar si un usuario opta por verlo en un explorador.|
|`scopes`|Matriz de enumeración|1|✔|Actualmente, las pestañas estáticas solo admiten el `personal` ámbito, lo que significa que solo se puede aprovisionar como parte de la experiencia personal.|

## <a name="bots"></a>Bots

**Optional**

Define una solución de bot, junto con información opcional, como las propiedades de comando predeterminadas.

El objeto es una matriz (máximo de solo 1 elemento &mdash; actualmente solo se permite un bot por aplicación) con todos los elementos del tipo `object` . Este bloque solo es necesario para soluciones que proporcionan una experiencia de bot.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`botId`|String|64 caracteres|✔|El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework. Esto bien puede ser el mismo que el IDENTIFICADOR general de la [aplicación.](#id)|
|`needsChannelSelector`|Booleano|||Describe si el bot usa una sugerencia del usuario para agregar el bot a un canal específico. predeterminado: `false`|
|`isNotificationOnly`|Booleano|||Indica si un bot es un bot unidireccional de solo notificación o un bot de conversación. predeterminado: `false`|
|`supportsFiles`|Booleano|||Indica si el bot es compatible con la capacidad para cargar y descargar archivos en chat personal. predeterminado: `false`|
|`scopes`|Matriz de enumeración|3|✔|Especifica si el bot ofrece una experiencia en el contexto de un canal en un `team`, en un chat de grupo (`groupchat`) o una experiencia específica para un solo usuario (`personal`). Estas opciones no son exclusivas.|

### <a name="botscommandlists"></a>bots.commandLists

Una lista opcional de comandos que el bot puede recomendar a los usuarios. El objeto es una matriz (máximo de 2 elementos) con todos los elementos de tipo; debe definir una lista de `object` comandos independiente para cada ámbito que admita el bot. Para obtener más información, consulte [menús Bot](~/bots/how-to/create-a-bot-commands-menu.md).

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`items.scopes`|matriz de enumeración|3|✔|Especifica el ámbito para el que la lista de comandos es válida. Las opciones son `team`, `personal` y `groupchat`.|
|`items.commands`|matriz de objetos|10|✔|Una matriz de comandos que el bot admite:<br>`title`: el nombre del comando bot (cadena, 32).<br>`description`: una descripción simple o ejemplo de la sintaxis del comando y su argumento (cadena, 128).|

## <a name="connectors"></a>Conectores

**Optional**

El `connectors` bloque define un conector de Office 365 para la aplicación.

El objeto es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` . Este bloque solo es necesario para las soluciones que proporcionan un conector.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`configurationUrl`|Cadena|2048 caracteres|✔|La dirección URL https:// que se usará al configurar el conector.|
|`connectorId`|String|64 caracteres|✔|Identificador único del conector que coincide con su identificador en el [panel de desarrollador de conectores.](https://aka.ms/connectorsdashboard)|
|`scopes`|Matriz de enumeración|1|✔|Especifica si connector ofrece una experiencia en el contexto de un canal en un `team` objeto y una experiencia con ámbito a un usuario individual solo ( `personal` ). Actualmente, solo se admite el `team` ámbito.|

## <a name="composeextensions"></a>composeExtensions

**Optional**

Define una extensión de mensajería para la aplicación.

> [!NOTE]
> El nombre de la característica se cambió de "extensión de composición" a "extensión de mensajería" en noviembre de 2017, pero el nombre del manifiesto sigue siendo el mismo para que las extensiones existentes sigan funcionando.

El objeto es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` . Este bloque solo es necesario para las soluciones que proporcionan una extensión de mensajería.

|Nombre| Tipo | Tamaño máximo | Obligatorio | Descripción|
|---|---|---|---|---|
|`botId`|Cadena|64|✔|El identificador único de la aplicación de Microsoft para el bot que respalda la extensión de mensajería, registrado con Bot Framework. Esto bien puede ser el mismo que el IDENTIFICADOR general de la [aplicación.](#id)|
|`canUpdateConfiguration`|Boolean|||Valor que indica si el usuario puede actualizar la configuración de una extensión de mensajería. El valor predeterminado es `false`.|
|`commands`|Matriz de objetos|10|✔|Matriz de comandos que admite la extensión de mensajería|

### <a name="composeextensionscommands"></a>composeExtensions.commands

La extensión de mensajería debe declarar uno o varios comandos. Cada comando aparece en Microsoft Teams como una interacción potencial desde el punto de entrada basado en la interfaz de usuario. Hay un máximo de 10 comandos.

Cada elemento de comando es un objeto con la siguiente estructura:

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`id`|String|64 caracteres|✔|El ID del comando.|
|`type`|String|64 caracteres||Tipo de comando. Uno de `query` o `action` . predeterminado: `query`|
|`title`|Cadena|32 caracteres|✔|El nombre del comando fácil de usar.|
|`description`|Cadena|128 caracteres||La descripción que aparece a los usuarios para indicar el propósito de este comando.|
|`initialRun`|Boolean|||Un valor booleano que indica si el comando debe ejecutarse inicialmente sin parámetros. predeterminado: `false`|
|`context`|Matriz de cadenas|3||Define desde dónde se puede invocar la extensión de mensaje. Cualquier combinación de `compose` `commandBox` , `message` . El valor predeterminado es `["compose", "commandBox"]`|
|`fetchTask`|Boolean|||Valor booleano que indica si debe recuperar el módulo de tareas dinámicamente.|
|`taskInfo`|Objeto|||Especifique el módulo de tareas que se va a precargar al utilizar un comando de extensión de mensajería.|
|`taskInfo.title`|Cadena|64||Título inicial del cuadro de diálogo.|
|`taskInfo.width`|Cadena|||Ancho del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "medio" o "pequeño".|
|`taskInfo.height`|Cadena|||Altura del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "medio" o "pequeño".|
|`taskInfo.url`|Cadena|||URL de vista web inicial.|
|`messageHandlers`|Matriz de objetos|5 ||Una lista de controladores que permiten invocar aplicaciones cuando se cumplen ciertas condiciones. Los dominios también deben aparecer en `validDomains` .|
|`messageHandlers.type`|Cadena|||El tipo de controlador de mensajes. Debe ser `"link"`.|
|`messageHandlers.value.domains`|Matriz de cadenas|||Matriz de dominios para los que el controlador de mensajes de vínculo puede registrarse.|
|`parameters`|Matriz de objetos|5 |✔|La lista de parámetros que toma el comando. Mínimo: 1; máximo: 5|
|`parameter.name`|String|64 caracteres|✔|El nombre del parámetro tal como aparece en el cliente. Esto se incluye en la solicitud de usuario.|
|`parameter.title`|Cadena|32 caracteres|✔|Título fácil de usar para el parámetro.|
|`parameter.description`|Cadena|128 caracteres||Cadena fácil de usar que describe el propósito de este parámetro.|
|`parameter.inputType`|Cadena|128 caracteres||Define el tipo de control que se muestra en un módulo de tareas para `fetchTask: true` . Uno de `text` , , , , , `textarea` `number` `date` `time` `toggle` `choiceset` .|
|`parameter.choices`|Matriz de objetos|10||Las opciones de elección para el `choiceset` archivo . Utilice únicamente cuando `parameter.inputType` sea `choiceset` .|
|`parameter.choices.title`|Cadena|128||Título de la elección.|
|`parameter.choices.value`|Cadena|512||Valor de la elección.|

## <a name="permissions"></a>permisos

**Optional**

Una matriz de `string` la que se especifica qué permisos solicita la aplicación, lo que permite a los usuarios finales saber cómo se realizará la extensión. Las siguientes opciones no son exclusivas:

* `identity`&emsp;Requiere información de identidad de usuario.
* `messageTeamMembers`&emsp;Requiere permiso para enviar mensajes directos a los miembros del equipo.

Cambiar estos permisos al actualizar la aplicación hará que los usuarios repitan el proceso de consentimiento la primera vez que ejecuten la aplicación actualizada.

## <a name="devicepermissions"></a>dispositivoPermissions

**Opcional** Matriz de cuerdas

Especifica las características nativas en el dispositivo de un usuario al que la aplicación puede solicitar acceso. Las opciones son:

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**Opcional,** excepto **requerido** cuando se indique

Una lista de dominios válidos desde los que la aplicación espera cargar cualquier contenido. Los listados de dominios pueden incluir comodines, por `*.example.com` ejemplo. Esto coincide exactamente con un segmento del dominio; si necesita `a.b.example.com` coincidir, utilice `*.*.example.com` . Si la configuración de la pestaña o la interfaz de usuario de contenido deben navegar a cualquier otro dominio además del que se usa para la configuración de pestañas, ese dominio debe especificarse aquí.

Sin embargo, **no** es necesario incluir los dominios de los proveedores de identidades que desea admitir en la aplicación. Por ejemplo, para autenticarse con un ID de Google, es necesario redirigir a accounts.google.com, pero no debe incluir accounts.google.com en `validDomains[]` .

> [!IMPORTANT]
> No agregue dominios que estén fuera de su control, ya sea directamente o a través de comodines. Por ejemplo, `yourapp.onmicrosoft.com` es válido, pero `*.onmicrosoft.com` no es válido.

El objeto es una matriz con todos los elementos del tipo `string` .

## <a name="webapplicationinfo"></a>webApplicationInfo

**Optional**

Especifique el ID de aplicación de AAD y Graph información para ayudar a los usuarios a iniciar sesión sin problemas en la aplicación AAD.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`id`|Cadena|36 caracteres|✔|Identificador de aplicación AAD de la aplicación. Este id debe ser un GUID.|
|`resource`|Cadena|2048 caracteres|✔|Url de recurso de la aplicación para adquirir token de autenticación para SSO.|

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


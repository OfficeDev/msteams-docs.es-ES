---
title: Referencia de esquema de manifiesto
description: Describe el esquema admitido por el manifiesto para Microsoft Teams.
keywords: esquema del manifiesto de Microsoft Teams
ms.openlocfilehash: 1a1a690e6e382dcad3ceb200ec02286e8c9171f8
ms.sourcegitcommit: 060b486c38b72a3e6b63b4d617b759174082a508
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2020
ms.locfileid: "41953491"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>Referencia: esquema de manifiesto para Microsoft Teams

El manifiesto de Microsoft Teams describe cómo se integra la aplicación en el producto de Microsoft Teams. El manifiesto debe cumplir el esquema hospedado en [`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json). También se admiten las versiones anteriores 1.0-1.4 (mediante "v1. x" en la dirección URL).

En el siguiente ejemplo de esquema se muestran todas las opciones de extensibilidad.

## <a name="sample-full-manifest"></a>Manifiesto completo de ejemplo

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
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
    "defaultLanguageTag": "en-us",
    "additionalLanguages": [
      {
        "languageTag": "es-es",
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
        }
      ],
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
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
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

*Opcional, pero* &ndash; la cadena recomendada

La dirección URL de https://que hace referencia al esquema JSON del manifiesto.

## <a name="manifestversion"></a>manifestVersion

String **requerida** &ndash;

La versión del esquema del manifiesto que está usando este manifiesto. Debe ser "1,5".

## <a name="version"></a>version

String **requerida** &ndash;

La versión de la aplicación específica. Si actualiza algo en el manifiesto, la versión también debe incrementarse. De este modo, cuando se instale el nuevo manifiesto, se sobrescribirá el anterior y el usuario podrá disfrutar de las funciones nuevas. Si esta aplicación se envió a la tienda, el nuevo manifiesto tendrá que volver a enviarse y a validarse. A continuación, los usuarios de esta aplicación recibirán el nuevo manifiesto actualizado automáticamente en unas pocas horas, después de que se apruebe.

Si la aplicación ha solicitado un cambio de permisos, se pedirá a los usuarios que actualicen y vuelvan a dar su consentimiento a la aplicación.

Esta cadena de versión debe seguir el estándar [SemVer](http://semver.org/) (Major. Secundaria. REVISIÓN).

## <a name="id"></a>id

Identificador de aplicación de Microsoft **necesario** &ndash;

El identificador único generado por Microsoft para esta aplicación. Si ha registrado un bot a través de Microsoft bot Framework o la aplicación Web de su pestaña ya inicia sesión en Microsoft, debe tener ya un identificador y escribirlo aquí. De lo contrario, debe generar un nuevo identificador en el portal de registro de aplicaciones de Microsoft ([mis aplicaciones](https://apps.dev.microsoft.com)), escribirlo aquí y volver a usarlo cuando agregue un bot. Nota: Si va a enviar una actualización a su aplicación existente en AppSource, el identificador del manifiesto no debe modificarse.

## <a name="packagename"></a>packageName

String **requerida** &ndash;

Un identificador único para esta aplicación en la notación de dominio inverso; por ejemplo, com. example. myapp.

## <a name="developer"></a>developer

**Required**

Especifica información sobre la compañía. Para las aplicaciones enviadas a AppSource (anteriormente tienda Office), estos valores deben coincidir con la información de la entrada AppSource. Consulte nuestras [directrices de publicación](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) para obtener más información.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`name`|32 caracteres|✔|El nombre para mostrar del desarrollador.|
|`websiteUrl`|2048 caracteres|✔|La dirección URL https://al sitio web del desarrollador. Este vínculo debe llevar a los usuarios a su compañía o a la página de aterrizaje específica del producto.|
|`privacyUrl`|2048 caracteres|✔|La dirección URL de https://a la Directiva de privacidad del desarrollador.|
|`termsOfUseUrl`|2048 caracteres|✔|La dirección URL de https://a las condiciones de uso del desarrollador.|
|`mpnId`|10 caracteres| |**Opcional** IDENTIFICADOR de red de los socios de Microsoft que identifica la organización asociada que crea la aplicación.|

## <a name="localizationinfo"></a>localizationInfo

**Optional**

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

## <a name="name"></a>name

**Required**

El nombre de la experiencia de la aplicación, que se muestra a los usuarios en la experiencia de Microsoft Teams. Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource. Los valores de `short` y `full` no deben ser iguales.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`short`|30 caracteres|✔|El nombre para mostrar corto de la aplicación.|
|`full`|100 caracteres||El nombre completo de la aplicación, que se usa si el nombre completo de la aplicación supera los 30 caracteres.|

## <a name="description"></a>description

**Required**

Describe la aplicación a los usuarios. Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource.

Asegúrese de que la descripción describe con precisión su experiencia y proporciona información para ayudar a los clientes potenciales a comprender lo que hace su experiencia. También debe tener en cuenta, en la descripción completa, si se requiere uso de una cuenta externa. Los valores de `short` y `full` no deben ser iguales.  La descripción breve no debe repetirse en la descripción larga y no debe incluir ningún otro nombre de aplicación.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`short`|80 caracteres|✔|Una breve descripción de la experiencia de la aplicación, que se usa cuando el espacio es limitado.|
|`full`|4000 caracteres|✔|La descripción completa de la aplicación.|

## <a name="icons"></a>iconos

**Required**

Iconos usados en la aplicación Microsoft Teams. Los archivos de icono deben incluirse como parte del paquete de carga. Vea [iconos](~/concepts/build-and-test/apps-package.md#icons) para obtener más información.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`outline`|2048 caracteres|✔|Una ruta de acceso relativa a un icono de esquema PNG transparente de 32x32.|
|`color`|2048 caracteres|✔|Una ruta de acceso de archivo relativa a un icono PNG 192x192 de color completo.|

## <a name="accentcolor"></a>accentColor

String **requerida** &ndash;

Color que se va a usar junto con y como fondo de los iconos de esquema.

El valor debe ser un código de color HTML válido que empiece por ' # ', `#4464ee`por ejemplo.

## <a name="configurabletabs"></a>configurableTabs

**Optional**

Se usa cuando la experiencia de la aplicación tiene una experiencia de la pestaña de canal de equipo que requiere una configuración adicional antes de que se agregue. Las pestañas configurables solo se admiten en el ámbito de Teams y actualmente solo se admite una pestaña por aplicación.

El objeto es una matriz con todos los elementos del tipo `object`. Este bloque solo es necesario para las soluciones que proporcionan una solución de ficha de canal configurable.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`configurationUrl`|String|2048 caracteres|✔|Dirección URL de https://que se va a usar al configurar la pestaña.|
|`canUpdateConfiguration`|Boolean|||Un valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de crearla. Predeterminada`true`|
|`scopes`|Matriz de enumeración|1 |✔|Actualmente, las pestañas configurables solo admiten los `team` ámbitos y `groupchat` . |
|`sharePointPreviewImage`|String|2048||Una ruta de acceso de archivo relativa a una imagen de vista previa de pestaña para su uso en SharePoint. Tamaño 1024x768. |
|`supportedSharePointHosts`|Matriz de enumeración|1 ||Define cómo estará disponible la pestaña en SharePoint. Las opciones `sharePointFullPage` son y`sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**Optional**

Define un conjunto de pestañas que se pueden "anclar" de forma predeterminada, sin que el usuario las agregue manualmente. Las pestañas estáticas declaradas en `personal` el ámbito siempre están ancladas a la experiencia personal de la aplicación. Actualmente no se admiten `team` las pestañas estáticas declaradas en el ámbito.

El objeto es una matriz (un máximo de 16 elementos) con todos los elementos del `object`tipo. Este bloque solo es necesario para las soluciones que proporcionan una solución de pestaña estática.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`entityId`|String|64 caracteres|✔|Un identificador único para la entidad que muestra la pestaña.|
|`name`|String|128 caracteres|✔|El nombre para mostrar de la pestaña en la interfaz de canal.|
|`contentUrl`|String|2048 caracteres|✔|Dirección URL de https://que señala a la interfaz de usuario de la entidad que se va a mostrar en el lienzo de Microsoft Teams.|
|`websiteUrl`|String|2048 caracteres||La dirección URL de https://para apuntar a si un usuario opta por verlo en un explorador.|
|`scopes`|Matriz de enumeración|1 |✔|Actualmente, las pestañas estáticas `personal` solo admiten el ámbito, lo que significa que solo se puede aprovisionar como parte de la experiencia personal.|

> [!NOTE]
> Si las pestañas requieren información dependiente del contexto para mostrar contenido relevante o para iniciar un flujo de autenticación, *vea* [obtener contexto para la pestaña de Microsoft Teams](../../tabs/how-to/access-teams-context.md).

## <a name="bots"></a>transferido

**Optional**

Define una solución de bot, junto con información opcional como propiedades de comando predeterminadas.

El objeto es una matriz (un máximo de solo 1&mdash;elemento solo es posible para cada aplicación) con todos los elementos del tipo `object`. Este bloque solo es necesario para las soluciones que proporcionan una experiencia de bot.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`botId`|String|64 caracteres|✔|El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework. Puede ser el mismo que el [identificador de aplicación](#id)general.|
|`needsChannelSelector`|Boolean|||Describe si el bot usa una sugerencia del usuario para agregar el bot a un canal específico. Predeterminada`false`|
|`isNotificationOnly`|Boolean|||Indica si un bot es un bot unidireccional de solo notificación o un bot de conversación. Predeterminada`false`|
|`supportsFiles`|Booleano|||Indica si el bot es compatible con la capacidad para cargar y descargar archivos en chat personal. Predeterminada`false`|
|`scopes`|Matriz de enumeración|3 |✔|Especifica si el bot ofrece una experiencia en el contexto de un canal en un `team`, en un chat de grupo (`groupchat`) o una experiencia específica para un solo usuario (`personal`). Estas opciones no son exclusivas.|

### <a name="botscommandlists"></a>bots. commandLists

Una lista opcional de comandos que el bot puede recomendar a los usuarios. El objeto es una matriz (un máximo de 2 elementos) con todos los elementos `object`de tipo; debe definir una lista de comandos independiente para cada ámbito que admita el bot. Consulte [menús de bot](~/bots/how-to/create-a-bot-commands-menu.md) para obtener más información.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`items.scopes`|matriz de enumeración|3 |✔|Especifica el ámbito para el que la lista de comandos es válida. Las opciones son `team`, `personal` y `groupchat`.|
|`items.commands`|matriz de objetos|10 |✔|Una matriz de comandos que el bot admite:<br>`title`: el nombre de comando del bot (cadena, 32)<br>`description`: una descripción o un ejemplo sencillo de la sintaxis del comando y su argumento (cadena, 128).|

## <a name="connectors"></a>Connector

**Optional**

El `connectors` bloque define un conector de Office 365 para la aplicación.

El objeto es una matriz (un máximo de 1 elemento) con todos los elementos `object`de tipo. Este bloque solo es necesario para las soluciones que proporcionan un conector.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`configurationUrl`|String|2048 caracteres|✔|Dirección URL de https://que se va a usar al configurar el conector.|
|`connectorId`|String|64 caracteres|✔|Un identificador único para el conector que coincide con su identificador en el [panel del programador de conectores](https://aka.ms/connectorsdashboard).|
|`scopes`|Matriz de enumeración|1 |✔|Especifica si el conector ofrece una experiencia en el contexto de un canal en un `team`o una experiencia en el ámbito de un solo usuario individual (`personal`). Actualmente, solo se `team` admite el ámbito.|

## <a name="composeextensions"></a>composeExtensions

**Optional**

Define una extensión de mensajería para la aplicación.

> [!NOTE]
> El nombre de la característica se cambió de "redactar extensión" a "extensión de mensajería" en noviembre de 2017, pero el nombre del manifiesto sigue siendo el mismo para que las extensiones existentes sigan funcionando.

El objeto es una matriz (un máximo de 1 elemento) con todos los elementos `object`de tipo. Este bloque solo es necesario para las soluciones que proporcionan una extensión de mensajería.

|Nombre| Tipo | Tamaño máximo | Obligatorio | Descripción|
|---|---|---|---|---|
|`botId`|String|64|✔|IDENTIFICADOR único de la aplicación de Microsoft para el bot que respalda la extensión de mensajería, tal como se registró con bot Framework. Puede ser el mismo que el identificador de aplicación general.|
|`canUpdateConfiguration`|Boolean|||Un valor que indica si el usuario puede actualizar la configuración de una extensión de mensajería. El valor predeterminado `false`es.|
|`commands`|Matriz de objetos|10 |✔|Matriz de comandos que admite la extensión de mensajería|
|`messageHandlers`|Matriz de objetos|5 ||Una lista de controladores que permiten invocar las aplicaciones cuando se cumplen ciertas condiciones. Los dominios también deben aparecer en`validDomains`|
|`messageHandlers.type`|String|||El tipo de controlador de mensajes. Debe ser `"link"`.|
|`messageHandlers.value.domains`|Matriz de cadenas|||Matriz de dominios para los que el controlador de mensajes de vínculo puede registrarse.|

### <a name="composeextensionscommands"></a>composeExtensions. Commands

La extensión de mensajería debe declarar uno o más comandos. Cada comando aparece en Microsoft Teams como una posible interacción desde el punto de entrada basado en la interfaz de usuario. Hay un máximo de 10 comandos.

Cada elemento de comando es un objeto con la estructura siguiente:

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`id`|String|64 caracteres|✔|Identificador del comando.|
|`type`|String|64 caracteres||Tipo del comando. Uno de `query` o `action`. Predeterminada`query`|
|`title`|String|32 caracteres|✔|El nombre de comando descriptivo|
|`description`|String|128 caracteres||La descripción que se muestra a los usuarios para indicar el propósito de este comando|
|`initialRun`|Boolean|||Un valor booleano que indica si el comando se debe ejecutar inicialmente sin ningún parámetro. Predeterminada`false`|
|`context`|Matriz de cadenas|3 ||Define desde dónde se puede invocar la extensión de mensajes. Cualquier combinación de `compose`, `commandBox`, `message`. El valor predeterminado es`["compose", "commandBox"]`|
|`fetchTask`|Boolean|||Un valor booleano que indica si debe recuperar el módulo de tareas de forma dinámica.|
|`taskInfo`|Objeto|||Especificar el módulo de tarea para cargar previamente cuando se usa un comando de extensión de mensajería|
|`taskInfo.title`|String|64||Título del cuadro de diálogo inicial|
|`taskInfo.width`|String|||Ancho del cuadro de diálogo, ya sea un número en píxeles o un diseño predeterminado, como "Large", "Medium" o "Small"|
|`taskInfo.height`|String|||Alto del cuadro de diálogo: número en píxeles o diseño predeterminado, como "Large", "Medium" o "Small"|
|`taskInfo.url`|String|||Dirección URL de la WebView inicial|
|`parameters`|Matriz de objetos|5 |✔|La lista de parámetros que toma el comando. Mínimo: 1; máximo: 5|
|`parameter.name`|String|64 caracteres|✔|El nombre del parámetro tal y como aparece en el cliente. Se incluye en la solicitud del usuario.|
|`parameter.title`|String|32 caracteres|✔|Título descriptivo del parámetro.|
|`parameter.description`|String|128 caracteres||Cadena descriptiva que describe el propósito de este parámetro.|
|`parameter.inputType`|String|128 caracteres||Define el tipo de control que se muestra en un módulo `fetchTask: true`de tareas para. Uno de `text`, `textarea`, `number`, `date` `time` `toggle`,,`choiceset`|
|`parameter.choices`|Matriz de objetos|10 ||Las opciones de opción del `choiceset`. Use solo cuando `parameter.inputType` sea`choiceset`|
|`parameter.choices.title`|String|128||Título de la opción|
|`parameter.choices.value`|String|512||Valor de la opción|

## <a name="permissions"></a>permissions

**Optional**

Una matriz de `string` que especifica los permisos que solicita la aplicación, lo que permite a los usuarios finales saber cómo se realizará la extensión. Las siguientes opciones no son exclusivas:

* `identity`&emsp; Requiere información de identidad del usuario
* `messageTeamMembers`&emsp; Requiere permiso para enviar mensajes directos a los miembros del equipo

Cambiar estos permisos al actualizar la aplicación hará que los usuarios repitan el proceso de consentimiento la primera vez que ejecuten la aplicación actualizada. Consulte [actualizar la aplicación](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) para obtener más información.

## <a name="devicepermissions"></a>devicePermissions

**Opcional** Matriz de cadenas

Especifica las características nativas del dispositivo de un usuario al que la aplicación puede solicitar acceso. Las opciones son:

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**Opcional**, excepto **obligatorio** donde se indica

Una lista de dominios válidos para los sitios web que la aplicación espera que se carguen dentro del cliente de Teams. Las listas de dominios pueden incluir caracteres comodín, por `*.example.com`ejemplo. Esto coincide exactamente con un segmento del dominio; Si tiene que hacer coincidir `a.b.example.com` , `*.*.example.com`use. Si la configuración de la pestaña o la interfaz de usuario de contenido debe navegar a cualquier otro dominio además del uso de la configuración de pestañas, dicho dominio debe especificarse aquí.

No obstante, **no** es necesario incluir los dominios de los proveedores de identidades que desea admitir en la aplicación. Por ejemplo, para autenticarse con un identificador de Google, es necesario redirigir a accounts.google.com, pero no se debe incluir accounts.google.com en `validDomains[]`.

Las aplicaciones de Microsoft teams que requieren sus propias direcciones URL de SharePoint para que funcionen correctamente pueden incluir "{teamsitedomain}" en su lista de dominios válidos.

> [!IMPORTANT]
> No agregue dominios que estén fuera de su control, ya sea directamente o mediante caracteres comodín. Por ejemplo, `yourapp.onmicrosoft.com` es válido, pero `*.onmicrosoft.com` no es válido.

El objeto es una matriz con todos los elementos del tipo `string`.

## <a name="webapplicationinfo"></a>webApplicationInfo

**Optional**

Especifique la información del grafo y el identificador de la aplicación de AAD para ayudar a los usuarios a iniciar sesión sin problemas en su aplicación de AAD.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`id`|String|36 caracteres|✔|Identificador de la aplicación de AAD de la aplicación. Este identificador debe ser un GUID.|
|`resource`|String|2048 caracteres|✔|Dirección URL de recurso de la aplicación para adquirir el token de autenticación para el SSO.|

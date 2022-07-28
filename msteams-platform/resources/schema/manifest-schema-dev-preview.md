---
title: Referencia del esquema de manifiesto de versión preliminar del desarrollador público
description: Obtenga información sobre el archivo de manifiesto de ejemplo y la descripción de todos sus componentes compatibles con Microsoft Teams.
ms.topic: reference
ms.localizationpriority: medium
ms.date: 11/15/2021
ms.openlocfilehash: c6552ce9a216dbf8c2f416002f6c98b977650160
ms.sourcegitcommit: dd70fedbe74f13725e0cb8dd4f56ff6395a1c8bc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2022
ms.locfileid: "67058210"
---
# <a name="public-developer-preview-manifest-schema-for-teams"></a>Versión preliminar pública de esquema de manifiesto para desarrolladores de Teams

Para obtener información sobre cómo habilitar la versión preliminar para desarrolladores, consulte [versión preliminar para desarrolladores públicos para Microsoft Teams](~/resources/dev-preview/developer-preview-intro.md).

> [!NOTE]
> Si no usa características de versión preliminar para desarrolladores, incluida la ejecución de [pestañas personales de Teams y extensiones de mensajes en Outlook y Office](../../m365-apps/overview.md), use el [manifiesto de aplicación para las características de disponibilidad general](~/resources/schema/manifest-schema.md) en su lugar.

El manifiesto de Teams describe cómo se integra la aplicación en el producto de Microsoft Teams. El manifiesto debe ajustarse al esquema alojado en [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).

## <a name="sample-full-manifest"></a>Manifiesto completo de ejemplo

```json
{
    "$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion": "devPreview",
    "version": "1.0.0",
    "id": "%MICROSOFT-APP-ID%",
    "packageName": "com.example.myapp",
    "devicePermissions": [
        "geolocation",
        "media"
    ],
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
            "scopes": [
                "team",
                "groupchat"
            ]"context": []
        }
    ],
    "staticTabs": [
        {
            "entityId": "idForPage",
            "name": "Display name of tab",
            "contentUrl": "https://contoso.com/content?host=msteams",
            "contentBotId": "Specifies to the app that tab is an Adaptive Card Tab. You can either provide the contentBotId or contentUrl.",
            "websiteUrl": "https://contoso.com/content",
            "scopes": [
                "personal"
            ]
        }
    ],
    "bots": [
        {
            "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
            "needsChannelSelector": false,
            "isNotificationOnly": false,
            "scopes": [
                "team",
                "personal",
                "groupchat"
            ],
            "supportsFiles": true,
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
                            "title": "Command N",
                            "description": "Description of Command N"
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
            "configurationUrl": "https://contoso.com/teamsconnector/configure",
            "scopes": [
                "team"
            ]
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
                    "type": "search",
                    "context": [
                        "compose",
                        "commandBox"
                    ],
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
                    "type": "action",
                    "fetchTask": true,
                    "context": [
                        "message"
                    ],
                    "parameters": [
                        {
                            "name": "custinfo",
                            "title": "Customer name",
                            "description": "Enter a customer name",
                            "inputType": "text"
                        }
                    ]
                },
                {
                    "id": "exampleMessageHandler",
                    "title": "Message Handler",
                    "description": "Domains that will create a preview when pasted into the compose box",
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
    ],
    "webApplicationInfo": {
        "id": "AAD App ID",
        "resource": "Resource URL for acquiring auth token for SSO"
    },
    "authorization": {
        "permissions": {
            "resourceSpecific": [
                {
                    "type": "Application",
                    "name": "ChannelSettings.Read.Group"
                },
                {
                    "type": "Delegated",
                    "name": "ChannelMeetingParticipant.Read.Group"
                }
            ]
        }
    },
    "configurableProperties": [
        "name",
        "shortDescription",
        "longDescription",
        "smallImageUrl",
        "largeImageUrl",
        "accentColor",
        "developerUrl",
        "privacyUrl",
        "termsOfUseUrl"
    ],
    "defaultInstallScope": "meetings",
    "defaultGroupCapability": {
        "meetings": "tab",
        "team": "bot",
        "groupchat": "bot"
    },
    "subscriptionOffer": {
        "offerId": "publisherId.offerId"
    },
    "meetingExtensionDefinition": {
        "scenes": [
            {
                "id": "9082c811-7e6a-4174-8173-6ccd57d377e6",
                "name": "Getting started sample",
                "file": "scenes/sceneMetadata.json",
                "preview": "scenes/scenePreview.png",
                "maxAudience": 15,
                "seatsReservedForOrganizersOrPresenters": 0
            },
            {
                "id": "afeaed22-f89b-48e1-98b4-46a514344e4a",
                "name": "Sample-1",
                "file": "scenes/sceneMetadata.json",
                "preview": "scenes/scenePreview.png",
                "maxAudience": 15,
                "seatsReservedForOrganizersOrPresenters": 3
            }
        ]
    }
}
```

El esquema define las siguientes propiedades:

## <a name="schema"></a>$schema

*Opcional, pero recomendado* &ndash; Cadena

La dirección URL `https://`, que hace referencia al esquema JSON para el manifiesto.

## <a name="manifestversion"></a>manifestVersion

**Necesario** &ndash; String

Versión del esquema de manifiesto que usa este manifiesto.

## <a name="version"></a>version

**Necesario** &ndash; String

Versión de la aplicación específica. Si actualiza algo en el manifiesto, la versión también debe incrementarse. De este modo, cuando se instale el nuevo manifiesto, se sobrescribirá el anterior y el usuario podrá disfrutar de las funciones nuevas. Si esta aplicación se envió a la tienda, el nuevo manifiesto tendrá que volver a enviarse y volver a validarse. A continuación, los usuarios de esta aplicación obtendrán el nuevo manifiesto actualizado automáticamente en unas horas, una vez aprobado.

Si cambian los permisos solicitados del complemento, los usuarios deberán actualizar y volver a autorizar el complemento.

La versión de esta cadena debe seguir el estándar de [SemVer](http://semver.org/) (MAJOR.MINOR.PATCH).

## <a name="id"></a>id

**Necesario** &ndash; Identificador de aplicación de Microsoft

El id. es un identificador único generado por Microsoft para la aplicación. Si ha registrado un bot a través de la Microsoft Bot Framework o la aplicación web de la pestaña ya inicia sesión con Microsoft, ya debería tener un identificador y debe escribirlo aquí. De lo contrario, debe generar un nuevo identificador en el Portal de registro de aplicaciones de Microsoft ([Mis aplicaciones](https://apps.dev.microsoft.com)), escribirlo aquí y reutilizarlo cuando [agregue un bot](~/bots/how-to/create-a-bot-for-teams.md).

## <a name="packagename"></a>packageName

**Necesario** &ndash; String

Un identificador único para la aplicación en notación de dominio inverso, por ejemplo com.example.myapp.

## <a name="developer"></a>developer

Necesario:

Especifica información sobre su empresa. Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada de AppSource.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`name`|32 caracteres|✔️|Nombre para mostrar del desarrollador.|
|`websiteUrl`|2048 caracteres|✔️|La dirección URL https:// al sitio web del desarrollador. Este vínculo debe llevar a los usuarios a la página de aterrizaje específica de su empresa o producto.|
|`privacyUrl`|2048 caracteres|✔️|La dirección URL https:// a la directiva de privacidad del desarrollador.|
|`termsOfUseUrl`|2048 caracteres|✔️|La https:// dirección URL a las condiciones de uso del desarrollador.|
|`mpnId`|10 caracteres|✔️|El id. de Microsoft Partner Network que identifica la organización asociada que genera la aplicación es **opcional**.|

## <a name="localizationinfo"></a>localizationInfo

Opcional:

Permite la especificación de un idioma predeterminado y punteros a archivos de idioma adicionales. Consulte [localización](~/concepts/build-and-test/apps-localization.md).

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`defaultLanguageTag`|4 caracteres|✔️|La etiqueta de idioma de las cadenas de este archivo de manifiesto de nivel superior.|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

Una matriz de objetos que especifican más traducciones de idiomas.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`languageTag`|4 caracteres|✔️|Etiqueta de idioma de las cadenas del archivo proporcionado.|
|`file`|4 caracteres|✔️|Ruta de acceso al archivo relativa al archivo .json que contiene las cadenas traducidas.|

## <a name="name"></a>name

Necesario:

El nombre de la experiencia de la aplicación, que se muestra a los usuarios en la experiencia de Teams. Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada de AppSource. Los valores de `short` y `full` no deben ser los mismos.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`short`|30 caracteres|✔️|El nombre corto para mostrar de la aplicación.|
|`full`|100 caracteres||Nombre completo de la aplicación, que se usa si el nombre completo de la aplicación supera los 30 caracteres.|

## <a name="description"></a>description

Necesario:

Describe la aplicación a los usuarios. En el caso de las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada de AppSource.

Asegúrese de que la descripción describe su experiencia y ayuda a los clientes potenciales a comprender lo que hace su experiencia. Debe anotar en la descripción completa si se requiere una cuenta externa para su uso. Los valores de `short` y `full` no deben ser los mismos.  La descripción breve no se puede repetir dentro de la descripción larga y no debe incluir ningún otro nombre de la aplicación.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`short`|80 caracteres|✔️|Una breve descripción de la experiencia de la aplicación, que se usa cuando el espacio es limitado.|
|`full`|4000 caracteres|✔️|La descripción completa de la aplicación.|

## <a name="icons"></a>iconos

Necesario:

Iconos usados en la aplicación Teams. Los archivos de icono deben incluirse como parte del paquete de carga.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`outline`|2048 caracteres|✔️|Ruta de acceso de archivo relativa a un icono de esquema PNG transparente de 32x32.|
|`color`|2048 caracteres|✔️|Ruta de acceso de archivo relativa a un icono PNG 192x192 de color completo.|

## <a name="accentcolor"></a>accentColor

**Necesario** &ndash; String

Color que se usará con y como fondo para los iconos de esquema.

El valor debe ser un código de color HTML válido que empiece por "#", como por ejemplo `#4464ee`.

## <a name="configurabletabs"></a>configurableTabs

Opcional:

Se usa cuando la experiencia de la aplicación tiene una experiencia de pestaña de canal de equipo que requiere una configuración adicional antes de agregarla. Las pestañas configurables solo se admiten en el ámbito de Teams y actualmente solo se admite una pestaña por aplicación.

El objeto es una matriz con todos los elementos del tipo `object`. Este bloque solo es necesario para las soluciones que proporcionan una solución de pestaña de canal configurable.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`configurationUrl`|Cadena|2048 caracteres|✔️|Dirección URL de https:// que se va a usar al configurar la pestaña.|
|`canUpdateConfiguration`|Boolean|||El valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de la creación. Predeterminado: `true`.|
|`scopes`|Matriz de enumeración|1|✔️|Actualmente, las pestañas configurables solo admiten los ámbitos `team` y `groupchat`. |
|`context` |Matriz de enumeración|6||Cojunto de ámbitos `contextItem` donde [se admite una pestaña](../../tabs/how-to/access-teams-context.md). Valor predeterminado: `channelTab`, `privateChatTab`, `meetingChatTab`, `meetingDetailsTab`, `meetingSidePanel` y `meetingStage`.|
|`sharePointPreviewImage`|Cadena|2048||Una ruta de acceso de archivo relativa a una imagen de vista previa de pestaña para su uso en SharePoint. Tamaño 1024x768. |
|`supportedSharePointHosts`|Matriz de enumeración|1||Define cómo está disponible la pestaña en SharePoint. Las opciones son `sharePointFullPage` y `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

Opcional:

Define un conjunto de pestañas que se puede "anclar" de manera predeterminada, sin que el usuario las agregue manualmente. Las pestañas estáticas declaradas en el ámbito `personal` siempre se anclan a la experiencia personal de la aplicación. Actualmente no se admiten las pestañas estáticas declaradas en el ámbito `team`.

Representar pestañas con tarjetas adaptables especificando `contentBotId` en lugar de `contentUrl` en el bloque **staticTabs**.

El objeto es una matriz (con un máximo de 16 elementos) y todos los elementos de tipo `object`. Este bloque solo es necesario para las soluciones que proporcionan una solución de pestaña estática.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`entityId`|String|64 caracteres|✔️|Un identificador único de la entidad que la pestaña muestra.|
|`name`|Cadena|128 caracteres|✔️|El nombre para mostrar de la pestaña en la interfaz del canal.|
|`contentUrl`|Cadena|2048 caracteres|✔️|La https:// dirección URL que apunta a la interfaz de usuario de entidad que se mostrará en el lienzo de Teams.|
|`contentBotId`|   | | | El identificador de la aplicación Microsoft Teams especificado para el bot en el portal de Bot Framework. |
|`websiteUrl`|Cadena|2048 caracteres||La dirección URL https:// a la que apuntar si un usuario opta por la vista en un explorador.|
|`scopes`|Matriz de enumeración|1|✔️|Actualmente, las pestañas estáticas solo admiten el ámbito `personal`, lo que significa que solo se puede aprovisionar como parte de la experiencia personal.|

## <a name="bots"></a>bots

Opcional:

Define una solución de bot, junto con información opcional, como las propiedades de comando predeterminadas.

El elemento es una matriz (como máximo 1 elemento&mdash;actualmente solo se permite un bot por aplicación) con todos los elementos del tipo `object`. Este bloque solo es necesario para las soluciones que proporcionan una experiencia de bot.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`botId`|String|64 caracteres|✔️|El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework. Este puede ser el mismo que el [identificador de aplicación general](#id).|
|`needsChannelSelector`|Boolean|||Describe si el bot usa una sugerencia del usuario para agregar el bot a un canal específico. Predeterminado: `false`|
|`isNotificationOnly`|Boolean|||Indica si un bot es un bot unidireccional de solo notificación, en lugar de un bot conversacional. Valor predeterminado: `false`|
|`supportsFiles`|Boolean|||Indica si el bot admite la capacidad de cargar o descargar archivos en el chat personal. Valor predeterminado: `false`|
|`scopes`|Matriz de enumeración|3|✔️|Especifica si el bot ofrece una experiencia en el contexto de un canal en un `team`, en un chat de grupo (`groupchat`) o una experiencia con ámbito solo para un usuario individual (`personal`). Estas opciones no son exclusivas.|

### <a name="botscommandlists"></a>bots.commandLists

Lista opcional de comandos que el bot puede recomendar a los usuarios. El objeto es una matriz (máximo de 2 elementos) con todos los elementos de tipo`object`; debe definir una lista de comandos independiente para cada ámbito que admita el bot. Para obtener más información, consulte [Menús de bot](~/bots/how-to/create-a-bot-commands-menu.md).

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`items.scopes`|matriz de enumeración|3|✔️|Especifica el ámbito para el que la lista de comandos es válida. Las opciones son `team`, `personal`y `groupchat`.|
|`items.commands`|matriz de objetos|10|✔️|Una matriz de comandos que el bot admite:<br>`title`: el nombre de comando del bot (cadena, 32).<br>`description`: una descripción o un ejemplo sencillos de la sintaxis del comando y su argumento (cadena, 128).|

## <a name="connectors"></a>conectores

Opcional:

El bloque `connectors` define un conector de Office 365 para la aplicación.

El objeto es una matriz (con un máximo de 1 elemento) y todos los elementos de tipo `object`. Este bloque solo es necesario para las soluciones que proporcionan un conector.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`configurationUrl`|Cadena|2048 caracteres|✔️|Dirección URL de https:// que se va a usar al configurar el conector.|
|`connectorId`|String|64 caracteres|✔️|Un identificador único del conector que coincide con su identificador en el [Panel de desarrolladores de conectores](https://aka.ms/connectorsdashboard).|
|`scopes`|Matriz de enumeración|1|✔️|Especifica si el conector ofrece una experiencia en el contexto de un canal en un `team` o una experiencia con ámbito solo para un usuario individual (`personal`). Actualmente, solo se admite el ámbito de `team`.|

## <a name="composeextensions"></a>composeExtensions

Opcional:

Define una extensión de mensajería para la aplicación.

> [!NOTE]
> El nombre de la característica se cambió de «extensión de redacción» a «extensión de mensajería» en noviembre de 2017, pero el nombre del manifiesto sigue siendo el mismo para que las extensiones existentes sigan funcionando.

El objeto es una matriz (con un máximo de 1 elemento) y todos los elementos de tipo `object`. Este bloque solo es necesario para las soluciones que proporcionan una extensión de mensajería.

|Nombre| Tipo | Tamaño máximo | Obligatorio | Descripción|
|---|---|---|---|---|
|`botId`|Cadena|64|✔️|El id. único de la aplicación de Microsoft para el bot que respalda la extensión de mensajería, tal como está registrado con el Bot Framework. Este puede ser el mismo que el [identificador de aplicación general](#id).|
|`canUpdateConfiguration`|Boolean|||Un valor que indica si el usuario puede actualizar la configuración de una extensión de mensajería. El valor predeterminado es `false`.|
|`commands`|Matriz de objeto|10|✔️|Matriz de comandos que admite la extensión de mensajería.|

### <a name="composeextensionscommands"></a>composeExtensions.commands

La extensión de mensaje debe declarar uno o varios comandos. Cada comando aparece en Teams como una posible interacción desde el punto de entrada basado en la interfaz de usuario. Hay un máximo de 10 comandos.

Cada elemento de comando es un objeto con la estructura siguiente:

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`id`|String|64 caracteres|✔️|Id. para el comando.|
|`type`|String|64 caracteres||Tipo de comando. Uno de `query` o `action`. Predeterminado: `query`|
|`title`|Cadena|32 caracteres|✔️|Nombre del comando fácil de usar.|
|`description`|Cadena|128 caracteres||Descripción que aparece a los usuarios para indicar el propósito de este comando.|
|`initialRun`|Booleano|||Un valor booleano que indica si el comando debe ejecutarse inicialmente sin parámetros. Predeterminado: `false`|
|`context`|Matriz de cadenas|3||Define desde dónde se puede invocar la extensión de mensaje. Cualquier combinación de `compose`,`commandBox`,`message`. El valor predeterminado es `["compose", "commandBox"]`|
|`fetchTask`|Boolean|||Un valor booleano que indica si debe capturar dinámicamente el módulo de tareas.|
|`taskInfo`|Objeto|||Especifique el módulo de tareas que se va a cargar previamente al usar un comando de extensión de mensajería.|
|`taskInfo.title`|Cadena|64||Título del cuadro de diálogo inicial.|
|`taskInfo.width`|Cadena|||Ancho del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "mediano" o "pequeño".|
|`taskInfo.height`|Cadena|||Alto del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "mediano" o "pequeño".|
|`taskInfo.url`|Cadena|||Dirección URL de la vista web inicial.|
|`messageHandlers`|Matriz de objetos|5||Una lista de controladores que permiten invocar aplicaciones cuando se cumplen determinadas condiciones. Los dominios también deben aparecer en `validDomains`.|
|`messageHandlers.type`|Cadena|||Tipo de controlador de mensajes. Debe estar `"link"`.|
|`messageHandlers.value.domains`|Matriz de cadenas|||Matriz de dominios para los que se puede registrar el controlador de mensajes de vínculo.|
|`parameters`|Matriz de objeto|5|✔️|Lista de parámetros que toma el comando. Mínimo: 1; máximo: 5.|
|`parameter.name`|String|64 caracteres|✔️|El nombre del parámetro tal como aparece en el cliente de Teams y se incluye en la solicitud del usuario|
|`parameter.title`|Cadena|32 caracteres|✔️|Título fácil de usar para el parámetro.|
|`parameter.description`|Cadena|128 caracteres||Cadena fácil de usar que describe el propósito de este parámetro.|
|`parameter.inputType`|Cadena|128 caracteres||Define el tipo de control que se muestra en un módulo de tareas para `fetchTask: true`. Uno de `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`.|
|`parameter.choices`|Matriz de objetos|10||Las opciones de elección para el `choiceset`. Use solo cuando `parameter.inputType` sea `choiceset`.|
|`parameter.choices.title`|Cadena|128||Título de la elección.|
|`parameter.choices.value`|Cadena|512||Valor de la elección.|

## <a name="permissions"></a>permissions

Opcional:

Matriz de `string`, que especifica qué permisos solicita la aplicación, lo que permite a los usuarios finales saber cómo funcionará la extensión. Las siguientes opciones no son exclusivas:

* `identity`&emsp;Requiere la información de identidad del usuario.
* `messageTeamMembers`&emsp;Requiere permiso para enviar mensajes directos a los miembros del equipo.

Cambiar estos permisos al actualizar la aplicación hará que los usuarios repitan el proceso de consentimiento la primera vez que ejecuten la aplicación actualizada.

## <a name="devicepermissions"></a>devicePermissions

**Opcional** Matriz de cadenas

Proporciona las características nativas en el dispositivo de un usuario al que la aplicación solicita acceso. Las opciones son:

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**Opcional**, excepto cuando se indique que es **necesario**.

Lista de dominios válidos desde los que la aplicación espera cargar cualquier contenido. Las listas de dominios pueden incluir caracteres comodín, por ejemplo `*.example.com`. El dominio válido coincide exactamente con un segmento del dominio; si necesita que coincida con `a.b.example.com`, use `*.*.example.com`. Si la interfaz de usuario de contenido o configuración de pestaña necesita navegar a cualquier otro dominio además del que se usa para la configuración de pestañas, ese dominio debe especificarse aquí.

**No** es necesario que incluya los dominios de proveedores de identidades que desea admitir en la aplicación. Por ejemplo, para autenticarse con un identificador de Google, es necesario redirigir a accounts.google.com, pero no debe incluir accounts.google.com en `validDomains[]`.

> [!IMPORTANT]
> No agregue dominios que estén fuera de su control, ya sea directamente o a través de caracteres comodín. Por ejemplo, `yourapp.onmicrosoft.com` es válido pero `*.onmicrosoft.com` no es válido.

El objeto es una matriz con todos los elementos del tipo `string`.

## <a name="webapplicationinfo"></a>WebApplicationInfo

Opcional:

Especifique el identificador de aplicación de Microsoft Azure Active Directory (Azure AD) y la información de Graph para ayudar a los usuarios a iniciar sesión sin problemas en la aplicación de Azure AD.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`id`|Cadena|36 caracteres|✔️|Id. de aplicación de la aplicación de Microsoft Azure Active Directory (Azure AD). Este identificador debe ser un GUID.|
|`resource`|Cadena|2048 caracteres|✔️|Dirección URL de recurso de la aplicación para adquirir el token de autenticación para SSO.|
|`applicationPermissions`|Matriz|100 elementos como máximo|✔️|Permisos de recursos para la aplicación.|

## <a name="graphconnector"></a>graphConnector

Objeto **opcional**

Especifique la configuración del conector de Graph de la aplicación. Si está presente, también se debe especificar [webApplicationInfo.id](#webapplicationinfo).

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`notificationUrl`|string|2048 caracteres|✔️|Dirección URL a la que se deben enviar las notificaciones del conector de Graph para la aplicación.|

## <a name="showloadingindicator"></a>showLoadingIndicator

Booleano **opcional**

Indica si se va a mostrar o no el indicador de carga cuando se está cargando una aplicación o una pestaña. El valor predeterminado es **false**.
> [!NOTE]
> Si selecciona `showLoadingIndicator` como true en el manifiesto de la aplicación, para cargar la página correctamente, modifique las páginas de contenido de las pestañas y los módulos de tareas tal como se describe en el documento [Mostrar un indicador de carga nativo](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator).

## <a name="isfullscreen"></a>IsFullScreen

 Booleano **opcional**

Indica dónde se representa una aplicación personal con o sin una barra de encabezado de pestaña. El valor predeterminado es **false**.

> [!NOTE]
> `isFullScreen` funciona solo para las aplicaciones publicadas en su organización.

## <a name="activities"></a>activities

Objeto **opcional**

Defina las propiedades que usa la aplicación para publicar una fuente de actividades del usuario.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`activityTypes`|Matriz de objetos|128 elementos| | Proporciona los tipos de actividades que la aplicación puede publicar en una fuente de actividades de los usuarios.|

### <a name="activitiesactivitytypes"></a>activities.activityTypes

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`type`|string|32 caracteres|✔️|El tipo de notificación. *Véalo a continuación*.|
|`description`|string|128 caracteres|✔️|Breve descripción de la notificación. *Vea a continuación*.|
|`templateText`|string|128 caracteres|✔️|P. ej.: " {actor} creó la tarea {taskId} para usted"|

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

## <a name="configurableproperties"></a>configurableProperties

Matriz **opcional**

El bloque `configurableProperties` define las propiedades de la aplicación que los administradores de Teams pueden personalizar. Para más información, consulte [Habilitar la personalización de aplicaciones](~/concepts/design/enable-app-customization.md).

> [!NOTE]
> Se debe definir una propiedad como mínimo. Puede definir un máximo de nueve propiedades en este bloque.

Puede definir cualquiera de las siguientes propiedades:

* `name`: nombre para mostrar de la aplicación.
* `shortDescription`: descripción breve de la aplicación.
* `longDescription`: descripción detallada de la aplicación.
* `smallImageUrl`: icono de esquema de la aplicación.
* `largeImageUrl`: icono de color de la aplicación.
* `accentColor`: color que se va a usar con y como fondo para los iconos de esquema.
* `developerUrl`: la dirección URL HTTPS del sitio web del desarrollador.
* `privacyUrl`: la dirección URL HTTPS de la directiva de privacidad del desarrollador.
* `termsOfUseUrl`: la dirección URL HTTPS de los términos de uso del desarrollador.

## <a name="supportedchanneltypes"></a>supportedChannelTypes

Matriz **opcional**

Habilita la aplicación en canales no estándar. Si la aplicación admite un ámbito de equipo y esta propiedad está definida, Teams habilita la aplicación en cada tipo de canal en consecuencia. Actualmente, se admiten los tipos de canal privado y compartido.

> [!NOTE]
>
> * Si la aplicación admite un ámbito de equipo, funciona en los canales estándar independientemente de los valores definidos en esta propiedad.
> * La aplicación puede tener en cuenta las propiedades únicas de cada uno de los tipos de canal para que funcionen correctamente. Para habilitar la pestaña para canales privados y compartidos, vea [Recuperar contexto en canales privados](~/tabs/how-to/access-teams-context.md#retrieve-context-in-private-channels) y [recuperar contexto en canales compartidos](~/tabs/how-to/access-teams-context.md#retrieve-context-in-microsoft-teams-connect-shared-channels).

## <a name="defaultinstallscope"></a>defaultInstallScope

Cadena **opcional**

Especifica el ámbito de instalación definido para esta aplicación de forma predeterminada. El ámbito definido será la opción que se muestra en el botón cuando un usuario intenta agregar la aplicación. Las opciones son:

* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a>defaultGroupCapability

Objeto **opcional**

Cuando se selecciona un ámbito de instalación de grupo, definirá la funcionalidad predeterminada cuando el usuario instale la aplicación. Las opciones son:

* `team`
* `groupchat`
* `meetings`

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`team`|string|||Cuando el ámbito de instalación seleccionado es `team`, este campo especifica la funcionalidad predeterminada disponible. Opciones: `tab`, `bot`o `connector`.|
|`groupchat`|string|||Cuando el ámbito de instalación seleccionado es `groupchat`, este campo especifica la funcionalidad predeterminada disponible. Opciones: `tab`, `bot`o `connector`.|
|`meetings`|string|||Cuando el ámbito de instalación seleccionado es `meetings`, este campo especifica la funcionalidad predeterminada disponible. Opciones: `tab`, `bot`o `connector`.|

## <a name="subscriptionoffer"></a>subscriptionOffer

Objeto **opcional**

Especifica la oferta de SaaS asociada a la aplicación.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`offerId`| string | 2 048 caracteres | ✔️ | Identificador único que incluye el identificador de publicador y el identificador de oferta, que puede encontrar en [Centro de partners](https://partner.microsoft.com/dashboard). Debe dar formato a la cadena como `publisherId.offerId`.|

## <a name="meetingextensiondefinition"></a>meetingExtensionDefinition

Objeto **opcional**

Especifique la definición de la extensión de reunión. Para obtener más información, vea [escenas personalizadas del modo conjunto en Teams](../../apps-in-teams-meetings/teams-together-mode.md).

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`scenes`|matriz de objetos| 5 elementos||Escenas admitidas de la reunión.|
|`supportsStreaming`|Boolean|||Valor que indica si una aplicación puede transmitir contenido de audio y vídeo de la reunión a un punto de conexión de protocolo de reunión en tiempo real (RTMP). El valor predeterminado es **False**.|

### <a name="meetingextensiondefinitionscenes"></a>meetingExtensionDefinition.scenes

|Nombre| Tipo|Tamaño máximo|Necesario |Descripción|
|---|---|---|---|---|
|`id`|||✔️| Identificador único de la escena. Este identificador debe ser un GUID. |
|`name`| string | 128 caracteres |✔️| Nombre de la escena. |
|`file`|||✔️| Ruta de acceso relativa al archivo JSON de metadatos de las escenas. |
|`preview`|||✔️| Ruta de acceso relativa del archivo al icono de vista previa PNG de las escenas. |
|`maxAudience`| integer | 50  |✔️| Número máximo de audiencias admitidas en la escena. |
|`seatsReservedForOrganizersOrPresenters`| integer | 50 |✔️| Número de puestos reservados para organizadores o moderadores.|

## <a name="authorization"></a>Autorización

Objeto **opcional**

Especifique y consolide la información relacionada con la autorización de la aplicación.

|Nombre| Tipo|Tamaño máximo|Necesario |Descripción|
|---|---|---|---|---|
|`permissions`||||Lista de permisos que la aplicación necesita para funcionar.|

### <a name="authorizationpermissions"></a>authorization.permissions

|Nombre| Tipo|Tamaño máximo|Necesario |Descripción|
|---|---|---|---|---|
|`resourceSpecific`| matriz de objetos|16 elementos||Permisos que protege el acceso a los datos en el nivel de instancia de recursos.|

### <a name="authorizationpermissionsresourcespecific"></a>authorization.permissions.resourceSpecific

|Nombre| Tipo|Tamaño máximo|Necesario |Descripción|
|---|---|---|---|---|
|`type`|string||✔️| Tipo del permiso específico del recurso. Opciones: `Application` y `Delegated`.|
|`name`|string|128 caracteres|✔️|Nombre del permiso específico del recurso. Para obtener más información, consulte [permisos de aplicación específicos de recursos](#resource-specific-application-permissions) y [permisos delegados específicos de recursos](#resource-specific-delegated-permissions)|

#### <a name="resource-specific-application-permissions"></a>Permisos de aplicación específicos del recurso

Los permisos de aplicación permiten a la aplicación acceder a los datos sin que un usuario haya iniciado sesión. Para obtener información sobre los permisos de aplicación, consulte [consentimiento específico de recursos para MS Graph y MS BotSDK](../../graph-api/rsc/resource-specific-consent.md).

#### <a name="resource-specific-delegated-permissions"></a>Permisos delegados específicos de recursos

Los permisos delegados permiten a la aplicación acceder a los datos en nombre del usuario que ha iniciado sesión.

* **Permisos delegados específicos de recursos para equipos**

    |**Nombre**|**Descripción**|
    |---|---|
    |`ChannelMeetingParticipant.Read.Group`| Permite que la aplicación lea la información de los participantes, incluidos el nombre, rol, identificador, horas de unión y salida de las reuniones de canal asociadas a este equipo, en nombre del usuario que ha iniciado sesión.|
    |`InAppPurchase.Allow.Group`| Permite que la aplicación muestre ofertas de Marketplace a los usuarios de este equipo y complete sus compras dentro de la aplicación, en nombre del usuario que ha iniciado sesión.|
    |`ChannelMeetingStage.Write.Group`| Permite que la aplicación muestre contenido en la escena de reunión en reuniones asociadas a este chat, en nombre del usuario que ha iniciado sesión.|

* **Permisos delegados específicos de recursos para chats o reuniones**

    |**Nombre**|**Descripción**|
    |---|---|
    |`InAppPurchase.Allow.Chat`|Permite que la aplicación muestre ofertas de Marketplace a los usuarios de este chat y a cualquier reunión asociada, y complete sus compras en la aplicación, en nombre del usuario que ha iniciado sesión.|
    |`MeetingStage.Write.Chat`|Permite que la aplicación muestre contenido en la fase de reunión en reuniones asociadas a este chat, en nombre del usuario que ha iniciado sesión.|
    |`OnlineMeetingParticipant.Read.Chat`|Permite que la aplicación lea la información de los participantes, incluidos el nombre, rol, identificador, horas de unión y salida de las reuniones asociadas a este chat, en nombre del usuario que ha iniciado sesión.|
    |`OnlineMeetingParticipant.ToggleIncomingAudio.Chat`|Permite que la aplicación alterne el audio entrante para los participantes en las reuniones asociadas a este chat, en nombre del usuario que ha iniciado sesión.|

* **Permisos delegados específicos de recursos para usuarios**

    |**Nombre**|**Descripción**|
    |---|---|
    |`InAppPurchase.Allow.User`|Permite que la aplicación muestre las ofertas de Marketplace del usuario y complete las compras del usuario dentro de la aplicación, en nombre del usuario que ha iniciado sesión.|

* **Permisos específicos de recursos para el recurso compartido en directo de Teams**

   |Nombre| Descripción |
   | ----- | ----- |
   |`LiveShareSession.ReadWrite.Chat`|<!--- need info --->|
   |`LiveShareSession.ReadWrite.Channel`|<!--- need info --->|
   |`MeetingStage.Write.Chat`|<!--- need info --->|
   |`OnlineMeetingIncomingAudio.Detect.Chat`|<!--- need info --->|

## <a name="see-also"></a>Vea también

* [Comprender la estructura de la aplicación de Microsoft Teams](~/concepts/design/app-structure.md)
* [Habilitar la personalización de aplicaciones](~/concepts/design/enable-app-customization.md)
* [Localizar la aplicación](~/concepts/build-and-test/apps-localization.md)
* [Integrar capacidades multimedia](~/concepts/device-capabilities/media-capabilities.md)

---
title: Referencia del esquema de manifiesto
description: En este artículo, tendrá el esquema de manifiesto para la referencia de Microsoft Teams, el esquema y el manifiesto completo de ejemplo.
ms.topic: reference
ms.localizationpriority: high
ms.openlocfilehash: 488929d98b9dff04086e5c3496550da9fd111aa1
ms.sourcegitcommit: d92e14fad6567fe91fd52ee6c213836740316683
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2022
ms.locfileid: "67605029"
---
# <a name="app-manifest-schema-for-teams"></a>Esquema del manifiesto de la aplicación de Teams

El manifiesto de la aplicación de Microsoft Teams describe cómo se integra la aplicación en el producto de Microsoft Teams. El manifiesto de la aplicación debe ajustarse al esquema hospedado en [`https://developer.microsoft.com/json-schemas/teams/v1.14/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.14/MicrosoftTeams.schema.json). Se admiten las versiones anteriores 1.0, 1.1,...,1.13 y la versión  actual 1.14 (con "v1.x" en la dirección URL).
Para obtener más información sobre los cambios realizados en cada versión, consulte [registro de cambios del manifiesto](https://github.com/OfficeDev/microsoft-teams-app-schema/releases).

En la tabla siguiente se enumeran las versiones de manifiesto de aplicación y versión de TeamsJS según diferentes escenarios de aplicación:

[!INCLUDE [pre-release-label](~/includes/teamjs-version-details.md)]

En el ejemplo de esquema siguiente se muestran todas las opciones de extensibilidad:

## <a name="sample-full-manifest"></a>Manifiesto completo de ejemplo

```json
{
    "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.14/MicrosoftTeams.schema.json",
    "manifestVersion": "1.14",
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
            "context": [
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
            "context": [
                "personalTab",
                "channelTab"
            ],
            "name": "Display name of tab",
            "contentUrl": "https://contoso.com/content (displayed in Teams canvas)",
            "websiteUrl": "https://contoso.com/content (displayed in web browser)",
            "searchUrl": "https://contoso.com/content (displayed in web browser)"
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
                    "description": "Command Description; e.g., Add a customer",
                    "initialRun": true,
                    "fetchTask": false ,
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
                    "id": "exampleCmd3",
                    "title": "Example Command 3",
                    "type": "action",
                    "context": [
                        "compose",
                        "commandBox",
                        "message"
                    ],
                    "description": "Command Description; e.g., Add a customer",
                    "fetchTask": false,
                    "taskInfo": {
                        "title": "Initial dialog title",
                        "width": "Dialog width",
                        "height": "Dialog height",
                        "url": "Initial webview URL"
                    }
                }
            ],
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
    "defaultBlockUntilAdminAction": true,
    "publisherDocsUrl": "https://website.com/app-info",
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
        "developerUrl",
        "privacyUrl",
        "termsOfUseUrl"
    ],
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

Cadena opcional, pero recomendada

Dirección URL https:// que hace referencia al esquema JSON para el manifiesto.

## <a name="manifestversion"></a>manifestVersion

Cadena **necesaria**

Versión del esquema de manifiesto que usa este manifiesto. Use `1.13` para habilitar la compatibilidad con aplicaciones de Teams en Outlook y Office; use `1.12` (o versiones anteriores) para aplicaciones de solo Teams.

## <a name="version"></a>version

Cadena **necesaria**

La versión de una aplicación específica. Cuando se actualiza algo en el manifiesto, también se debe aumentar la versión. De esta manera, cuando el nuevo manifiesto esté instalado, sobrescribirá el existente y el usuario obtendrá las nuevas características. Cuando esta aplicación se envió a la tienda, el nuevo manifiesto debe volver a enviarse y validarse. Los usuarios de la aplicación reciben el nuevo manifiesto actualizado automáticamente en pocas horas después de que se apruebe el manifiesto.

Si la aplicación solicita un cambio de permisos de acceso, se pide a los usuarios que actualicen y vuelvan a dar los permisos a la aplicación.

La versión de esta cadena debe seguir el estándar de [SemVer](http://semver.org/) (MAJOR.MINOR.PATCH).

## <a name="id"></a>Id.

Identificador de aplicación de Microsoft **necesario**

El id. es un identificador único generado por Microsoft para la aplicación. Usted tiene un id. si su bot está registrado a través de Microsoft Bot Framework. Usted tiene un id. si la aplicación web de la pestaña ya inicia sesión con Microsoft. Debe escribir el identificador aquí. De lo contrario, debe generar un nuevo id. en el [portal de registro de aplicación de Microsoft](https://aka.ms/appregistrations). Use el mismo id. si agrega un bot.

> [!NOTE]
> Si va a enviar una actualización a la aplicación existente en AppSource, no debe modificar el identificador del manifiesto.

## <a name="developer"></a>developer

Objeto **necesario**

Especifica información sobre su empresa. Para las aplicaciones enviadas a la tienda de Teams, estos valores deben coincidir con la información de la descripción de la tienda. Para más información, consulte las [directrices de publicación de la tienda de Teams](~/concepts/deploy-and-publish/appsource/publish.md).

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`name`|32 caracteres|✔️|Nombre para mostrar del desarrollador.|
|`websiteUrl`|2048 caracteres|✔️|La dirección URL https:// al sitio web del desarrollador. Este vínculo debe llevar a los usuarios a la página de aterrizaje específica de su empresa o producto.|
|`privacyUrl`|2048 caracteres|✔️|La dirección URL https:// a la directiva de privacidad del desarrollador.|
|`termsOfUseUrl`|2048 caracteres|✔️|La https:// dirección URL a las condiciones de uso del desarrollador.|
|`mpnId`|10 caracteres| |El id. de Microsoft Partner Network que identifica la organización asociada que genera la aplicación es **opcional**.|

## <a name="name"></a>name

Objeto **necesario**

El nombre de la experiencia de la aplicación, que se muestra a los usuarios en la experiencia de Teams. Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada de AppSource. Los valores de `short` y `full` deben ser diferentes.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`short`|30 caracteres|✔️|El nombre corto para mostrar de la aplicación.|
|`full`|100 caracteres||Nombre completo de la aplicación, que se usa si el nombre completo de la aplicación supera los 30 caracteres.|

## <a name="description"></a>description

Objeto **necesario**

Describe la aplicación a los usuarios. En el caso de las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada de AppSource.

Asegúrese de que la descripción describe su experiencia y ayuda a los clientes potenciales a comprender lo que hace su experiencia. Debe anotar en la descripción completa si se requiere una cuenta externa para su uso. Los valores de `short` y `full` deben ser diferentes. La descripción breve no se puede repetir dentro de la descripción larga y no debe incluir ningún otro nombre de aplicación.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`short`|80 caracteres|✔️|Una breve descripción de la experiencia de la aplicación, que se usa cuando el espacio es limitado.|
|`full`|4000 caracteres|✔️|La descripción completa de la aplicación.|

## <a name="packagename"></a>packageName

Cadena **opcional**

Un identificador único para la aplicación en notación de dominio inverso; por ejemplo, com.example.myapp. Longitud máxima: 64 caracteres.

## <a name="localizationinfo"></a>localizationInfo

Objeto **opcional**

Permite la especificación de un idioma predeterminado y proporciona punteros a más archivos de idioma. Para obtener más información, vea [localización](~/concepts/build-and-test/apps-localization.md).

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`defaultLanguageTag`||✔️|Etiqueta de idioma de las cadenas de este archivo de manifiesto de nivel superior.|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

Una matriz de objetos que especifican más traducciones de idiomas.

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`languageTag`||✔️|Etiqueta de idioma de las cadenas del archivo proporcionado.|
|`file`||✔️|Ruta de acceso al archivo relativa al archivo .json que contiene las cadenas traducidas.|

## <a name="icons"></a>iconos

Objeto **necesario**

Iconos usados en la aplicación Teams. Los archivos de icono deben incluirse como parte del paquete de carga. Para obtener más información, consulte [Iconos](../../concepts/build-and-test/apps-package.md#app-icons).

|Nombre| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|
|`outline`|32 por 32 píxeles|✔️|Ruta de acceso de archivo relativa a un icono de esquema PNG transparente de 32x32.|
|`color`|192 por 192 píxeles|✔️|Ruta de acceso de archivo relativa a un icono PNG 192x192 de color completo.|

## <a name="accentcolor"></a>accentColor

Código de color hexadecimal HTLM **necesario**.

Es el color que se usará y que servirá como fondo para los iconos de esquema.

El valor debe ser un código de color HTML válido que empiece por "#", como por ejemplo `#4464ee`.

## <a name="configurabletabs"></a>configurableTabs

Matriz **opcional**

Se usa cuando la experiencia de la aplicación tiene una experiencia de pestaña de canal de equipo que requiere una configuración adicional antes de agregarla. Las pestañas configurables solo se admiten en los ámbitos `team` y `groupchat` y se pueden configurar las mismas pestañas varias veces. Sin embargo, solo se puede definir en el manifiesto una vez.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`configurationUrl`|string|2048 caracteres|✔️|Dirección URL de https:// que se va a usar al configurar la pestaña.|
|`scopes`|Matriz de enumeración|1|✔️|Actualmente, las pestañas configurables solo admiten los ámbitos `team` y `groupchat`. |
|`canUpdateConfiguration`|Booleano|||Valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de la creación. Valor predeterminado: **true**.|
|`context` |Matriz de enumeración|6||Cojunto de ámbitos `contextItem` donde [se admite una pestaña](../../tabs/how-to/access-teams-context.md). Valor predeterminado: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.|
|`sharePointPreviewImage`|string|2048||Una ruta de acceso de archivo relativa a una imagen de vista previa de pestaña para su uso en SharePoint. Tamaño 1024x768. |
|`supportedSharePointHosts`|Matriz de enumeración|1||Define cómo está disponible la pestaña en SharePoint. Las opciones son `sharePointFullPage` y `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

Matriz **opcional**

Define un conjunto de pestañas que se puede "anclar" de manera predeterminada, sin que el usuario las agregue manualmente. Las pestañas estáticas declaradas en el ámbito `personal` siempre se anclan a la experiencia personal de la aplicación. Actualmente no se admiten las pestañas estáticas declaradas en el ámbito `team`.

Este elemento es una matriz (con un máximo de 16 elementos) y todos los elementos de tipo `object`. Este bloque solo es necesario para las soluciones que proporcionan una solución de pestaña estática.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`entityId`|string|64 caracteres|✔️|Un identificador único de la entidad que la pestaña muestra.|
|`name`|string|128 caracteres|✔️|El nombre para mostrar de la pestaña en la interfaz del canal.|
|`contentUrl`|string||✔️|La https:// dirección URL que apunta a la interfaz de usuario de entidad que se mostrará en el lienzo de Teams.|
|`websiteUrl`|string|||La dirección URL de https:// a la que apuntar si un usuario opta por la vista en un explorador.|
|`searchUrl`|string|||La dirección URL de https:// a la que apuntar para las consultas de búsqueda de un usuario.|
|`scopes`|Matriz de enumeración|1|✔️|Actualmente, las pestañas estáticas solo admiten el ámbito `personal`, lo que significa que solo se puede aprovisionar como parte de la experiencia personal.|
|`context` | Matriz de enumeración| 2|| El conjunto de ámbitos `contextItem` donde se admite una pestaña.|

> [!NOTE]
> La característica searchUrl no está disponible para los desarrolladores de terceros. Si las pestañas requieren información dependiente del contexto para mostrar contenido relevante o para iniciar un flujo de autenticación, consulte [Obtener contexto para la pestaña de Microsoft Teams](../../tabs/how-to/access-teams-context.md).

## <a name="bots"></a>bots

Matriz **opcional**

Define una solución de bot, junto con información opcional, como las propiedades de comando predeterminadas.

El elemento es una matriz (un elemento como máximo&mdash;actualmente solo se permite un bot por aplicación) con todos los elementos del tipo `object`. Este bloque solo es necesario para las soluciones que proporcionan una experiencia de bot.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`botId`|string|64 caracteres|✔️|El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework. El id. puede ser el mismo que el [id. general de la aplicación](#id).|
|`scopes`|Matriz de enumeración|3|✔️|Especifica si el bot ofrece una experiencia en el contexto de un canal en un `team`, en un chat de grupo (`groupchat`) o una experiencia con ámbito solo para un usuario individual (`personal`). Estas opciones no son exclusivas.|
|`needsChannelSelector`|Booleano|||Describe si el bot usa o no una sugerencia de usuario para agregar al bot a un canal específico. Valor predeterminado: **`false`**|
|`isNotificationOnly`|Booleano|||Indica si un bot es un bot unidireccional de solo notificación, en lugar de un bot conversacional. Valor predeterminado: **`false`**|
|`supportsFiles`|Booleano|||Indica si el bot admite la capacidad de cargar o descargar archivos en el chat personal. Valor predeterminado: **`false`**|
|`supportsCalling`|Booleano|||Valor que indica dónde admite llamadas de audio un bot. **IMPORTANTE**: esta propiedad es actualmente experimental. Es posible que las propiedades experimentales no estén completas y que se produzcan cambios antes de estar totalmente disponibles.  La propiedad se proporciona solo con fines de prueba y exploración y no se debe usar en aplicaciones de producción. Predeterminado: **`false`**|
|`supportsVideo`|Booleano|||Valor que indica dónde admite llamadas de vídeo un bot. **IMPORTANTE**: esta propiedad es actualmente experimental. Es posible que las propiedades experimentales no estén completas y que se produzcan cambios antes de estar totalmente disponibles.  La propiedad se proporciona solo con fines de prueba y exploración y no se debe usar en aplicaciones de producción. Predeterminado: **`false`**|

### <a name="botscommandlists"></a>bots.commandLists

Lista de comandos que el bot puede recomendar a los usuarios. El objeto es una matriz (máximo de dos elementos) con todos los elementos de tipo`object`; usted debe definir una lista de comandos independiente para cada ámbito que admita el bot. Para obtener más información, consulte [Menús de bot](~/bots/how-to/create-a-bot-commands-menu.md).

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`items.scopes`|Matriz de enumeración|3|✔️|Especifica el ámbito para el que la lista de comandos es válida. Las opciones son `team`, `personal`y `groupchat`.|
|`items.commands`|matriz de objetos|10|✔️|Una matriz de comandos que el bot admite:<br>`title`: el nombre de comando del bot (cadena, 32)<br>`description`: una descripción o un ejemplo sencillos de la sintaxis del comando y su argumento (cadena, 128).|

### <a name="botscommandlistscommands"></a>bots.commandLists.commands

|Nombre| Tipo| Tamaño máximo | Necesario | Description|
|---|---|---|---|---|
|title|string|12 |✔️|Nombre del comando del bot.|
|description|string|128 caracteres|✔️|Una descripción del texto o un ejemplo sencillos de la sintaxis del comando y sus argumentos.|

## <a name="connectors"></a>conectores

Matriz **opcional**

El bloque `connectors` define un conector de Office 365 para la aplicación.

El objeto es una matriz (con un máximo de un elemento) y todos los elementos de tipo `object`. Este bloque solo es necesario para las soluciones que proporcionan un conector.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`configurationUrl`|string|2048 caracteres|✔️|Dirección URL de https:// que se va a usar al configurar el conector.|
|`scopes`|Matriz de enumeración|1|✔️|Especifica si el conector ofrece una experiencia en el contexto de un canal en un `team` o una experiencia con ámbito solo para un usuario individual (`personal`). Actualmente, solo se admite el ámbito de `team`.|
|`connectorId`|string|64 caracteres|✔️|Un identificador único del conector que coincide con su identificador en el [Panel de desarrolladores de conectores](https://aka.ms/connectorsdashboard).|

## <a name="composeextensions"></a>composeExtensions

Matriz **opcional**

Define una extensión de mensajería para la aplicación.

> [!NOTE]
> El nombre de la característica se cambió de «extensión de redacción» a «extensión de mensajería» en noviembre de 2017, pero el nombre del manifiesto sigue siendo el mismo para que las extensiones existentes sigan funcionando.

El elemento es una matriz (máximo de un elemento) con todos los elementos de tipo `object`. Este bloque solo es necesario para las soluciones que proporcionan una extensión de mensajería.

|Nombre| Tipo | Tamaño máximo | Obligatorio | Descripción|
|---|---|---|---|---|
|`botId`|string|64|✔️|El id. único de la aplicación de Microsoft para el bot que respalda la extensión de mensajería, tal como está registrado con el Bot Framework. El id. puede ser el mismo que el id. de aplicación general.|
|`commands`|matriz de objetos|10|✔️|Matriz de comandos que admite la extensión de mensajería.|
|`canUpdateConfiguration`|Boolean|||Valor que indica si el usuario puede actualizar la configuración de una extensión de mensajería. Valor predeterminado: **falso**.|
|`messageHandlers`|Matriz de objetos|5||Una lista de controladores que permiten invocar aplicaciones cuando se cumplen determinadas condiciones.|
|`messageHandlers.type`|string|||Tipo de controlador de mensajes. Debe estar `"link"`.|
|`messageHandlers.value.domains`|matriz de cadenas|||Matriz de dominios para los que se puede registrar el controlador de mensajes de vínculo.|

### <a name="composeextensionscommands"></a>composeExtensions.commands

Su extensión de mensajería debe declarar uno o más comandos con un máximo de 10 comandos. Cada comando aparece en Microsoft Teams como una posible interacción desde el punto de entrada basado en la interfaz de usuario.

Cada elemento de comando es un objeto con la estructura siguiente:

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`id`|string|64 caracteres|✔️|Id. para el comando.|
|`title`|string|32 caracteres|✔️|Nombre del comando fácil de usar.|
|`type`|string|64 caracteres||Tipo de comando. Uno de `query` o `action`. Valor predeterminado: **consulta**.|
|`description`|string|128 caracteres||Descripción que aparece a los usuarios para indicar el propósito de este comando.|
|`initialRun`|Booleano|||Un valor booleano indica si el comando se ejecuta inicialmente sin parámetros. El valor predeterminado es **false**.|
|`context`|matriz de cadenas|3||Define desde dónde se puede invocar la extensión de mensaje. Cualquier combinación de `compose`,`commandBox`,`message`. El valor predeterminado es `["compose","commandBox"]`.|
|`fetchTask`|Booleano|||Valor booleano que indica si debe capturar dinámicamente el módulo de tareas. El valor predeterminado es **false**.|
|`taskInfo`|object|||Especifique el módulo de tareas que se va a cargar previamente al usar un comando de extensión de mensajería.|
|`taskInfo.title`|string|64 caracteres||Título del cuadro de diálogo inicial.|
|`taskInfo.width`|string|||Ancho del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "mediano" o "pequeño".|
|`taskInfo.height`|string|||Alto del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "mediano" o "pequeño".|
|`taskInfo.url`|string|||Dirección URL de la vista web inicial.|
|`parameters`|matriz de objetos|5 elementos|✔️|Lista de parámetros que toma el comando. Mínimo: 1; máximo: 5.|
|`parameters.name`|string|64 caracteres|✔️|Nombre del parámetro tal como aparece en el cliente. El nombre del parámetro se incluye en la solicitud de usuario.|
|`parameters.title`|string|32 caracteres|✔️|Título fácil de usar para el parámetro.|
|`parameters.description`|string|128 caracteres||Cadena fácil de usar que describe el propósito de este parámetro.|
|`parameters.value`|string|512 caracteres||Valor inicial del parámetro. Actualmente no se admite el valor|
|`parameters.inputType`|string|128 caracteres||Define el tipo de control que se muestra en un módulo de tareas para`fetchTask: false` . Uno de `text, textarea, number, date, time, toggle, choiceset` .|
|`parameters.choices`|matriz de objetos|10 elementos||Las opciones de elección para el `choiceset`. Use solo cuando `parameter.inputType` sea `choiceset`.|
|`parameters.choices.title`|string|128 caracteres|✔️|Título de la elección.|
|`parameters.choices.value`|string|512 caracteres|✔️|Valor de la elección.|

## <a name="permissions"></a>permissions

Matriz de cadenas **opcional**

Matriz de `string`, que especifica qué permisos solicita la aplicación, lo que permite a los usuarios finales saber cómo funciona la extensión. Las siguientes opciones no son exclusivas:

* `identity`&emsp;Requiere la información de identidad del usuario.
* `messageTeamMembers`&emsp;Requiere permiso para enviar mensajes directos a los miembros del equipo.

Al cambiar estos permisos durante la actualización de la aplicación, los usuarios repiten el proceso de consentimiento después de ejecutar la aplicación actualizada. Para obtener más información, vea [Actualizar la aplicación](~/concepts/deploy-and-publish/appsource/post-publish/overview.md).

> [!NOTE]
> Actualmente, los permisos están en desuso.

## <a name="devicepermissions"></a>devicePermissions

Matriz de cadenas **opcional**

Proporciona las características nativas en el dispositivo de un usuario al que la aplicación solicita acceso. Las opciones son:

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**Opcional**, excepto cuando se indique que es **necesario**.

Una lista de dominios válidos para sitios web que la aplicación espera cargar en el cliente de Teams. Las listas de dominios pueden incluir caracteres comodín, por ejemplo `*.example.com`. El dominio válido coincide exactamente con un segmento del dominio; si necesita que coincida con `a.b.example.com` entonces use `*.*.example.com`. Si la configuración de pestañas o la interfaz de usuario de contenido navega a cualquier otro dominio que no sea la configuración de pestañas, ese dominio debe especificarse aquí.

**No** incluya los dominios de proveedores de identidades que desea admitir en la aplicación. Por ejemplo, para autenticarse mediante un identificador de Google, es necesario redirigir a accounts.google.com, pero no debe incluir accounts.google.com en `validDomains[]`.

Las aplicaciones de Teams que requieren sus propias direcciones URL de SharePoint para funcionar bien, incluyen " {teamsitedomain}" en su lista de dominios válidos.

> [!IMPORTANT]
> No agregue dominios que estén fuera de su control, ya sea directamente o a través de caracteres comodín. Por ejemplo, `yourapp.onmicrosoft.com` es válido, pero `*.onmicrosoft.com` no es válido.

El objeto es una matriz con todos los elementos del tipo `string`.

## <a name="webapplicationinfo"></a>WebApplicationInfo

Objeto **opcional**

Proporcione su identificador de aplicación de Azure Active Directory e información Microsoft Graph para ayudar a los usuarios a iniciar sesión sin problemas en la aplicación. Si la aplicación está registrada en Microsoft Azure Active Directory (Azure AD), deberá proporcionar el identificador de la aplicación. Los administradores pueden revisar fácilmente los permisos y conceder consentimiento en el Centro de administración de Teams.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`id`|string|36 caracteres|✔️|Azure AD identificador de aplicación de la aplicación. Este identificador debe ser un GUID.|
|`resource`|string|2048 caracteres|✔️|Dirección URL de recurso de la aplicación para adquirir el token de autenticación para SSO. </br> **NOTA:** Si no usa el inicio de sesión único, asegúrese de escribir un valor de cadena ficticio en este campo en el manifiesto de la aplicación, por ejemplo, <https://notapplicable> para evitar una respuesta de error. |

## <a name="graphconnector"></a>graphConnector

Objeto **opcional**

Especifique la configuración del conector de Graph de la aplicación. Si está presente, también debe especificarse [webApplicationInfo.id](#webapplicationinfo) .

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`notificationUrl`|string|2048 caracteres|✔️|Dirección URL a la que se deben enviar las notificaciones del conector de Graph para la aplicación.|

## <a name="showloadingindicator"></a>showLoadingIndicator

Booleano **opcional**

Indica si se va a mostrar o no el indicador de carga cuando se carga una aplicación o pestaña. El valor predeterminado es **false**.
>[!NOTE]
>Si selecciona `showLoadingIndicator` como true en el manifiesto de la aplicación, para cargar la página correctamente, modifique las páginas de contenido de las pestañas y los módulos de tareas tal como se describe en el documento [Mostrar un indicador de carga nativo](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator).

## <a name="isfullscreen"></a>IsFullScreen

 Booleano **opcional**

Indica si una aplicación personal se representa sin una barra de encabezado de pestaña (lo que significa el modo de pantalla completa). El valor predeterminado es **false**.

> [!NOTE]
>
> * `isFullScreen` solo funciona para las aplicaciones publicadas en su organización. Las aplicaciones de terceros publicadas y transferidas localmente no pueden usar esta propiedad (se omite).
>
> * `isFullScreen=true` quita la barra de encabezado y el título proporcionados por Teams de los cuadros de diálogo de módulos de tareas y aplicaciones personales.

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

## <a name="configurableproperties"></a>configurableProperties

Matriz **opcional**

El bloque `configurableProperties` define las propiedades de la aplicación que los administradores de Teams pueden personalizar. Para más información, consulte [Habilitar la personalización de aplicaciones](~/concepts/design/enable-app-customization.md). La característica de personalización de aplicaciones no se admite en aplicaciones personalizadas o LOB.

> [!NOTE]
> Se debe definir una propiedad como mínimo. Puede definir un máximo de nueve propiedades en este bloque.

Puede definir cualquiera de las siguientes propiedades:

* [name](#name): nombre para mostrar de la aplicación.
* [shortDescription](#description): descripción breve de la aplicación.
* [longDescription](#description): la descripción larga de la aplicación.
* [smallImageUrl](#icons): icono de esquema de la aplicación.
* [largeImageUrl](#icons): icono de color de la aplicación.
* [accentColor](#accentcolor): el color que se va a usar y un fondo para los iconos de esquema.
* [developerUrl](#developer): dirección URL HTTPS del sitio web del desarrollador.
* [privacyUrl](#developer): dirección URL HTTPS de la directiva de privacidad del desarrollador.
* [termsOfUseUrl](#developer): dirección URL HTTPS de los términos de uso del desarrollador.

## <a name="supportedchanneltypes"></a>supportedChannelTypes

Matriz **opcional**

Habilita la aplicación en canales no estándar. Si la aplicación admite un ámbito de equipo y se define esta propiedad, Teams habilita la aplicación en cada tipo de canal en consecuencia. Actualmente, se admiten los tipos de canal privado y compartido.

> [!NOTE]
>
> * Si la aplicación admite un ámbito de equipo, funciona en los canales estándar, independientemente de los valores definidos en esta propiedad.
> * La aplicación puede tener en cuenta las propiedades únicas de cada uno de los tipos de canal para que funcione correctamente. Para habilitar la pestaña para canales privados y compartidos, consulte [Recuperar contexto en canales privados](~/tabs/how-to/access-teams-context.md#retrieve-context-in-private-channels) y [Recuperar contexto en canales compartidos](~/tabs/how-to/access-teams-context.md#retrieve-context-in-microsoft-teams-connect-shared-channels).

## <a name="defaultblockuntiladminaction"></a>defaultBlockUntilAdminAction

**Opcional**: booleano

Cuando la propiedad `defaultBlockUntilAdminAction` se establece en **true**, la aplicación se oculta a los usuarios de forma predeterminada hasta que el administrador la permita. Si se establece en **true**, la aplicación se oculta para todos los inquilinos y usuarios finales. Los administradores de inquilinos pueden ver la aplicación en el Centro de administración de Teams y tomar medidas para permitir o bloquear la aplicación. El valor predeterminado es **False**. Para obtener más información sobre el bloque de aplicaciones predeterminado, consulte [Bloquear aplicaciones de forma predeterminada para los usuarios hasta que un administrador lo apruebe](../../concepts/design/enable-app-customization.md#block-apps-by-default-for-users-until-an-admin-approves).

## <a name="publisherdocsurl"></a>publisherDocsUrl

Cadena **opcional**

**Tamaño máximo**: 128 caracteres

El `publisherDocsUrl` es una dirección URL HTTPS a una página de información para que los administradores obtengan instrucciones antes de dar permisos a una aplicación, que está bloqueada de forma predeterminada. También se puede usar para proporcionar instrucciones o información sobre la aplicación que pueda ser útil para el administrador de inquilinos.

## <a name="subscriptionoffer"></a>subscriptionOffer

Objeto **opcional**

Especifica la oferta de SaaS asociada a la aplicación.

|Nombre| Tipo|Tamaño máximo|Necesario|Descripción|
|---|---|---|---|---|
|`offerId`| string | 2 048 caracteres | ✔️ | Identificador único que incluye el identificador de publicador y el identificador de oferta, que puede encontrar en [Centro de partners](https://partner.microsoft.com/dashboard). Debe dar formato a la cadena como `publisherId.offerId`.|

## <a name="meetingextensiondefinition"></a>meetingExtensionDefinition

Objeto **opcional**

Especifique la definición de la extensión de reunión. Para obtener más información, vea [escenas personalizadas del modo conjunto en Teams](../../apps-in-teams-meetings/teams-together-mode.md).

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`scenes`|matriz de objetos| 5 elementos||Escenas admitidas de la reunión.|
|`supportsStreaming`|Boolean|||Valor que indica si una aplicación puede transmitir el contenido de audio y vídeo de la reunión a un punto de conexión del protocolo de reunión en tiempo real (RTMP). El valor predeterminado es **False**.|

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

**Opcional** — Objeto

> [!NOTE]
> Si establece la propiedad `manifestVersion` en 1.12, la propiedad de autorización es incompatible con las versiones anteriores (versión 1.11 o anterior) del manifiesto. La autorización admite la versión 1.12 del manifiesto.

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

## <a name="create-a-manifest-file"></a>Crear un archivo de manifiesto

Si la aplicación no tiene un archivo de manifiesto de aplicación de Teams, deberá crearlo.

Para crear un archivo de manifiesto de aplicación de Teams:

1. Use el [esquema de manifiesto de ejemplo](#sample-full-manifest) para crear un archivo .json.
1. Guárdelo en la raíz de la carpeta del proyecto como `manifest.json`.

<br>
<details>
<summary>Este es un ejemplo de esquema de manifiesto para una aplicación de pestañas con SSO habilitado:</summary>
<br>

> [!NOTE]
> El contenido de ejemplo del manifiesto que se muestra aquí es solo para una aplicación de pestañas. Usa valores de ejemplo para el URI de subdominio y el nombre del paquete. Para obtener más información, consulte [esquema de manifiesto de ejemplo](#sample-full-manifest).

  ```json
{ 
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json", 
 "manifestVersion": "1.12", 
 "version": "1.0.0", 
 "id": "{new GUID for this Teams app - not the Azure AD App ID}", 
 "packageName": "com.contoso.teamsauthsso", 
 "developer": { 
 "name": "Microsoft", 
 "websiteUrl": "https://www.microsoft.com", 
 "privacyUrl": "https://www.microsoft.com/privacy", 
 "termsOfUseUrl": "https://www.microsoft.com/termsofuse" 
  }, 

  "name": { 
    "short": "Teams Auth SSO", 
    "full": "Teams Auth SSO" 
  }, 


  "description": { 
    "short": "Teams Auth SSO app", 
    "full": "The Teams Auth SSO app" 
  }, 

  "icons": { 
    "outline": "outline.png", 
    "color": "color.png" 
  }, 

  "accentColor": "#60A18E", 
  "staticTabs": [ 
    { 
     "entityId": "auth", 
     "name": "Auth", 
     "contentUrl": "https://https://subdomain.example.com/Home/Index", 
     "scopes": [ "personal" ] 
    } 
  ], 

  "configurableTabs": [ 
    { 
     "configurationUrl": "https://subdomain.example.com/Home/Configure", 
     "canUpdateConfiguration": true, 
     "scopes": [ 
     "team" 
      ] 
    } 
  ], 
  "permissions": [ "identity", "messageTeamMembers" ], 
  "validDomains": [ 
   "{subdomain or ngrok url}" 
  ], 
  "webApplicationInfo": { 
    "id": "{Azure AD AppId}", 
    "resource": "api://subdomain.example.com/{Azure AD AppId}" 
  }
} 
```

</details>

## <a name="see-also"></a>Vea también

* [Comprender la estructura de la aplicación de Microsoft Teams](~/concepts/design/app-structure.md)
* [Habilitar la personalización de aplicaciones](~/concepts/design/enable-app-customization.md)
* [Localizar la aplicación](~/concepts/build-and-test/apps-localization.md)
* [Integrar capacidades multimedia](~/concepts/device-capabilities/media-capabilities.md)
* [Versión preliminar de esquema de manifiesto para desarrolladores públicos de Microsoft Teams](manifest-schema-dev-preview.md)

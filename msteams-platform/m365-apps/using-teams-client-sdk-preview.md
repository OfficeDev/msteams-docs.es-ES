---
title: Versión preliminar del SDK v2 de cliente de JavaScript en Microsoft Teams
description: Descripción de los cambios que se incluyen con la versión preliminar del SDK v2 de cliente de JavaScript de Microsoft Teams
ms.date: 11/15/2021
ms.topic: conceptual
ms.custom: m365apps
ms.localizationpriority: high
ms.openlocfilehash: 91f012821efacd0f0ff6032703d0520d5bd469e0
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111699"
---
# <a name="microsoft-teams-javascript-client-sdk-v2-preview"></a>Versión preliminar del SDK v2 de cliente de JavaScript en Microsoft Teams

Con la [Versión preliminar v2 del SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-beta&preserve-view=true), el SDK de Teams existente (`@microsoft/teams-js`o simplemente `TeamsJS`) ha sido refactorizado para permitir a los desarrolladores de Teams la capacidad de [ampliar las aplicaciones de Teams para que se ejecuten en Outlook y Office](overview.md). Desde una perspectiva funcional, la versión preliminar v2 del SDK de TeamsJS (`@microsoft/teams-js@next`) es un superconjunto del SDK de TeamsJS actual, admite la funcionalidad de la aplicación de Teams existente al tiempo que agrega la capacidad de hospedar aplicaciones de Teams en Outlook y Office.

Hay dos cambios importantes en la versión preliminar v2 del SDK de TeamsJS que su código tendrá que tener en cuenta para poder ejecutarse en otras aplicaciones de Microsoft 365:

* [**Las funciones callback ahora devuelven objetos Promise.**](#callbacks-converted-to-promises) Todas las funciones existentes con un parámetro de callback se han modernizado para devolver un objeto JavaScript [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) para mejorar el control de las operaciones asincrónicas y la legibilidad del código.

* [**Las API ahora están organizadas en *funcionalidades*.**](#apis-organized-into-capabilities) Las funcionalidades se pueden considerar como agrupaciones lógicas de API que proporcionan una funcionalidad similar, como `authentication`, `calendar`, `mail`, `monetization`, `meeting`, y `sharing`.

 Puede usar la [extensión Kit de herramientas de Teams](https://aka.ms/teams-toolkit) para Microsoft Visual Studio Code a fin de simplificar el proceso de actualización de la aplicación de Teams, como se describe en la sección siguiente.

> [!NOTE]
> La habilitación de una aplicación de Teams existente para ejecutarse en Outlook y Office requiere lo siguiente:
>
> 1. Dependencia del `@microsoft/teams-js@2.0.0-beta.1` o posterior y
> 2. Modificar el código de aplicación existente según los cambios necesarios descritos en este documento.
>
> Si hace referencia a `@microsoft/teams-js@2.0.0-beta.1` (o posterior) desde una aplicación de Teams existente, verá advertencias de desuso si el código llama a las API que han cambiado. Se proporciona una capa de traducción de API (asignación del SDK actual a la versión preliminar de las llamadas API del SDK) para permitir que las aplicaciones de Teams existentes sigan funcionando en Teams hasta que puedan actualizar el código para que funcione con la versión preliminar del SDK v2 de TeamsJS. Después de actualizar el código con los cambios descritos en este artículo, la pestaña personal también se ejecutará en Outlook y Office.

## <a name="updating-to-the-teams-client-sdk-v2-preview"></a>Actualización a la versión preliminar v2 del SDK de cliente de Teams

La manera más sencilla de actualizar la aplicación de Teams para usar la versión preliminar v2 del SDK de TeamsJS es usar la extensión [Kit de herramientas de Teams](https://aka.ms/teams-toolkit) para Visual Studio Code. Esta sección le guiará a través de los pasos para hacerlo. Si prefiere actualizar manualmente el código, consulte las secciones [Callbacks convertidos en promises](#callbacks-converted-to-promises) y [APIs organizados en funcionalidades](#apis-organized-into-capabilities) para obtener más detalles sobre los cambios necesarios en la API.

### <a name="1-install-the-latest-teams-toolkit-visual-studio-code-extension"></a>1. Instalar la extensión Kit de herramientas de Teams de Visual Studio Code más reciente

En el *Marketplace de extensiones de Visual Studio Code*, busque **Kit de herramientas de Teams** e instale la versión `2.10.0` o posterior. El kit de herramientas proporciona dos comandos para ayudar en el proceso:

1. Un comando para actualizar el esquema del manifiesto
1. Un comando para actualizar las referencias del SDK y llamar a sitios

Estas son las dos actualizaciones clave que necesitará para ejecutar una aplicación de pestaña personal de Teams en otras aplicaciones de Microsoft 365: ``

### <a name="2-updating-the-manifest"></a>2. Actualizar el manifiesto

# <a name="teams-toolkit"></a>[Kit de herramientas de Teams](#tab/manifest-teams-toolkit)

1. Abra la *Paleta de comandos*: `Ctrl+Shift+P`
1. Ejecute el comando **Teams: actualizar el manifiesto de Teams para admitir las aplicaciones de Outlook y Office** y seleccione el archivo de manifiesto de la aplicación. Se realizarán cambios en el sitio.

# <a name="manual-steps"></a>[Pasos manuales](#tab/manifest-manual)

Abra el manifiesto de la aplicación de Teams y actualice `$schema` y `manifestVersion` con los siguientes valores:

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```

---

Si ha usado el Kit de herramientas de Teams para crear su aplicación personal, también puede usarlo para validar los cambios en el archivo de manifiesto e identificar los errores. Abra la paleta de comandos `Ctrl+Shift+P` y busque **Teams: validar el archivo de manifiesto** o seleccione la opción en el menú Implementación del Kit de herramientas de Teams (busque el icono de Teams en el lado izquierdo de Visual Studio Code).

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="La opción &quot;Validar archivo de manifiesto&quot; del Kit de herramientas de Teams en el menú &quot;Implementación&quot;":::

### <a name="2-update-sdk-references"></a>2. Actualizar referencias del SDK

Para ejecutarse en Outlook y Office, la aplicación tendrá que depender del paquete [npm](https://www.npmjs.com/package/@microsoft/teams-js/v/2.0.0-beta.1) >`@microsoft/teams-js@2.0.0-beta.1` (o una versión *beta* posterior). Para realizar estos pasos manualmente y obtener más información sobre los cambios en la API, vea las secciones siguientes sobre [Callbacks convertidas en promises](#callbacks-converted-to-promises) y [API organizados en funcionalidades](#apis-organized-into-capabilities).

1. Asegúrese de que tiene [Kit de herramientas de Teams](https://aka.ms/teams-toolkit) `v2.10.0` o posterior
1. Abra la *Paleta de comandos*: `Ctrl+Shift+P`
1. Ejecute el comando `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`

Después de la finalización, la utilidad habrá actualizado el archivo `package.json` con la dependencia de la versión preliminar v2 del SDK de TeamsJS (`@microsoft/teams-js@2.0.0-beta.1` o posterior) y los archivos de `*.js/.ts` y `*.jsx/.tsx` se actualizarán con:

> [!div class="checklist"]
>
> * referencias de `package.json` a la versión preliminar v2 del SDK de TeamsJS
> * Instrucciones de importación para la versión preliminar v2 del SDK de TeamsJS
> * [Llamadas de funciones, enumeraciones e interfaces](#apis-organized-into-capabilities) a la versión preliminar v2 del SDK de TeamsJS
> * Comentarios `TODO` de recordatorios para revisar las áreas que podrían verse afectadas por los cambios en la interfaz [Context](#updates-to-the-context-interface)
> * Comentarios `TODO` de recordatorios para garantizar la [conversión de funciones de tipo callback a promises](#callbacks-converted-to-promises) ha ido bien en cada sitio de llamada que encontró la herramienta

> [!IMPORTANT]
> Las herramientas de actualización no admiten el código dentro de archivos HTML y requerirán cambios manuales.

## <a name="callbacks-converted-to-promises"></a>Callbacks convertidas a promises

Las API de Teams que anteriormente tomaban un parámetro de callback se han actualizado para devolver un objeto JavaScript [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). Entre ellas se incluyen las siguientes API:

```js
app.getContext, app.initialize, appInstallDialog.openAppInstallDialog, authentication.authenticate, authentication.getAuthToken, authentication.getUser, authentication.registerAuthenticationHandlers was removed to support using Promises, calendar.openCalendarItem, calendar.composeMeeting, call.startCall, core.executeDeepLink, location.getLocation, location.showLocation, mail.openMailItem, mail.composeMail, media.captureImage, media.getMedia, media.selectMedia, media.viewImages, media.scanBarCode, meeting.getAppContentStageSharingCapabilities, meeting.getAuthenticationTokenForAnonymousUser, meeting.getIncomingClientAudioState, meeting.getLiveStreamState, meeting.getMeetingDetails, meeting.requestStartLiveStreaming, meeting.requestStopLiveStreaming, meeting.shareAppContentToStage, meeting.stopSharingAppContentToStage, meeting.toggleIncomingClientAudio, meeting.getAppContentStageSharingState, pages.backStack.navigateBack, pages.navigateCrossDomain, pages.navigateToTab, pages.tabs.getMruTabInstances, pages.tabs.getTabInstances, pages.config.setConfig, pages.config.getConfig, people.selectPeople, ChildAppWindow.postMessage, ParentAppWindow.postMessage
```

Tendrá que actualizar la forma en que el código llama a cualquiera de estas API para usar Promises. Por ejemplo, si el código llama a una API de Teams como esta:

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Este código:

```js
import microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context) => { /* ... */ });
```

Debe actualizarse a:

```js
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context) => {
    /*...*/
});
```

... o el patrón equivalente `async/await`:

```js
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context = await app.getContext();
  /*...*/
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Este código:

```TypeScript
import * as microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context: microsoftTeams.Context) => {
  /* ... */
});
```

Debe actualizarse a:

```TypeScript
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context: Context) => {
    /*...*/
});
```

... o el patrón equivalente `async/await`:

```TypeScript
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context: Context = await app.getContext();
  /*...*/
}
```

---

> [!TIP]
> Al actualizar el código para la versión preliminar v2 del SDK de TeamsJS mediante el [Kit de herramientas de Teams](#updating-to-the-teams-client-sdk-v2-preview), las actualizaciones necesarias se marcan automáticamente con comentarios `TODO` en el código de cliente.

## <a name="apis-organized-into-capabilities"></a>API organizadas en funcionalidades

Una *funcionalidad* es una agrupación lógica de API que proporciona una funcionalidad similar. Puede considerar a Microsoft Teams, Outlook y Office como hosts. Un host admite una funcionalidad determinada si admite todas las API definidas dentro de esa funcionalidad. Un host no puede implementar parcialmente una funcionalidad.  Las funcionalidades pueden basarse en características o contenido, como *diálogo* o *autenticación*. También hay funcionalidades para los tipos de aplicación, como *pestañas/páginas* o *bots*, y otras agrupaciones.

En la versión preliminar v2 del SDK de TeamsJS, las API se definen como funciones en un espacio de nombres de JavaScript cuyo nombre coincide con su funcionalidad necesaria. Si una aplicación se ejecuta en un host que admite la funcionalidad de diálogo, la aplicación puede llamar de forma segura a las API como `dialog.open` (además de otras API relacionadas con cuadros diálogo definidas en el espacio de nombres). Mientras tanto, si una aplicación intenta llamar a una API que no se admite en ese host, la API iniciará una excepción.

### <a name="differentiate-your-app-experience"></a>Diferenciar la experiencia de la aplicación

Puede comprobar la compatibilidad del host de una funcionalidad determinada en tiempo de ejecución llamando a la función `isSupported()` en esa funcionalidad (espacio de nombres). Devolverá `true` si es compatible y `false` si no es así, y puede ajustar el comportamiento de la aplicación según corresponda. Esto permite a la aplicación iluminar la interfaz de usuario y la funcionalidad en los hosts que la admiten, mientras continúa ejecutándose en los hosts que no la admiten.

El nombre del host en el que se ejecuta la aplicación se expone como una propiedad *hostName* en la interfaz Context (`app.Context.app.host.name`), que se puede consultar en tiempo de ejecución llamando a `getContext`. También está disponible como un `{hostName}` [valor de marcador de posición de dirección URL](../tabs/how-to/access-teams-context.md#get-context-by-inserting-url-placeholder-values). El procedimiento recomendado es usar el mecanismo *hostName* con moderación:

* **No** asuma que cierta funcionalidad está o no está disponible en un host basándose en el valor de propiedad *hostName*. En su lugar, compruebe la compatibilidad con la funcionalidad (`isSupported`).
* **No** use *hostName* para realizar llamadas a la API. En su lugar, compruebe la compatibilidad con la funcionalidad (`isSupported`).
* **Use***hostName* para diferenciar el tema de la aplicación en función del host en el que se ejecuta. Por ejemplo, puede usar el color púrpura de Microsoft Teams como color de énfasis principal cuando se ejecuta en Teams y el azul de Outlook cuando se ejecuta en Outlook.
* **Use***hostName* para diferenciar los mensajes que se muestran al usuario en función del host en el que se ejecuta. Por ejemplo, muestre *Administrar las tareas en Office* cuando se ejecute en Office en la web y *Administrar las tareas en Teams* cuando se ejecute en Microsoft Teams.

### <a name="namespaces"></a>Espacios de nombres

La versión preliminar v2 del SDK de TeamsJS organiza las API en *funcionalidades* por medio de espacios de nombres. Varios espacios de nombres nuevos de importancia particular son *app*, *pages*, *dialog* y *teamsCore*.

#### <a name="app-namespace"></a>espacio de nombres *app*

El espacio de nombres `app` contiene las API de nivel superior necesarias para el uso general de la aplicación, en Microsoft Teams, Office y Outlook. Todas las API de otros espacios de nombres de TeamsJS se han movido al espacio de nombres `app` en la versión preliminar v2 del SDK de TeamsJS:

| Espacio de nombres original `global (window)` | Nuevo espacio de nombres `app` |
| - | - |
| `initialize` | `app.initialize` |
| `getContext` | `app.getContext` |
| `registerOnThemeChangeHandler` | `app.registerOnThemeChangeHandler` |

| Espacio de nombres original `appInitialization` | Nuevo espacio de nombres `app` |
| - | - |
| `appInitialization.notifyAppLoaded` | `app.notifyAppLoaded` |
| `appInitialization.notifySuccess` | `app.notifySuccess` |
| `appInitialization.notifyFailure` | `app.notifyFailure` |
| `appInitialization.notifyExpectedFailure` | `app.notifyExpectedFailure` |
| enumeración `appInitialization.FailedReason` | `app.FailedReason` |
| enumeración `appInitialization.ExpectedFailureReason` | `app.ExpectedFailureReason` |
| enumeración `appInitialization.IFailedRequest` | `app.IFailedRequest` |
| enumeración `appInitialization.IExpectedFailureRequest` | `app.IExpectedFailureRequest` |

#### <a name="core-namespace"></a>espacio de nombres *core*

El espacio de nombres `core` incluye funcionalidad para vínculos profundos.

| Espacio de nombres original `publicAPIs` | Nuevo espacio de nombres `core` |
| - | - |
| `shareDeepLink` | `core.shareDeepLink` |
| `executeDeepLink` | `core.executeDeepLink` |

#### <a name="pages-namespace"></a>espacio de nombres *pages*

El espacio de nombres `pages` incluye funcionalidad para ejecutar y navegar por páginas web dentro de varios clientes de Microsoft 365, incluidos Teams, Office y Outlook. También incluye varias sub-funcionalidades, implementadas como sub-espacios de nombres.

| Espacio de nombres original `global (window)` | Nuevo espacio de nombres `pages` |
| - | - |
| `setFrameContext` | `pages.setCurrentFrame` (nombre cambiado) |
| `initializeWithFrameContext` | `pages.initializeWithFrameContext` |
| `registerFullScreenHandler` | `pages.registerFullScreenHandler` |
| `navigateCrossDomain` | `pages.navigateCrossDomain` |
| `returnFocus` | `pages.returnFocus` |

##### <a name="pagestabs"></a>*pages.tabs*

| Espacio de nombres original `global (window)` | Nuevo espacio de nombres `pages.tabs` |
| - | - |
| `getTabInstances` |  `pages.tabs.getTabInstances` |
| `getMruTabInstances` | `pages.tabs.getMruTabInstances` |
| `navigateToTab` | `pages.tabs.navigateToTab` |

| Espacio de nombres original `navigation` | Nuevo espacio de nombres `pages.tabs` |
| - | - |
| `navigation.navigateToTab` | `pages.tabs.navigateToTab` |

##### <a name="pagesconfig"></a>*pages.config*

| Espacio de nombres original `settings` | Nuevo espacio de nombres `pages.config`  |
| - | - |
| `settings.setSettings` | `pages.config.setConfig` (nombre cambiado)
| `settings.getSettings` | `pages.config.getConfig` (nombre cambiado)
| `settings.setValidityState`| `pages.config.setValidityState`
| `settings.initialize` | `pages.config.initialize`
| `settings.registerOnSaveHandler`| `pages.config.registerOnSaveHandler`
| `settings.registerOnRemoveHandler` | `pages.config.registerOnRemoveHandler`
| interfaz `settings.Settings` | `pages.config.Config` (nombre cambiado)
| interfaz `settings.SaveEvent` | `pages.config.SaveEvent` (nombre cambiado)
| interfaz `settings.RemoveEvent` | `pages.config.RemoveEvent` (nombre cambiado)
| interfaz `settings.SaveParameters` | `pages.config.SaveParameters` (nombre cambiado)
| interfaz `settings.SaveEventImpl` | `pages.config.SaveEventImpl` (nombre cambiado)

| Espacio de nombres original `global (window)` | Nuevo espacio de nombres `pages.config` |
| - | - |
| `registerEnterSettingsHandler` | `pages.config.registerChangeConfigHandler` (nombre cambiado)

##### <a name="pagesbackstack"></a>*pages.backStack*

| Espacio de nombres original `navigation` | Nuevo espacio de nombres `pages.backStack`  |
| - | - |
| `navigation.navigateBack` | `pages.backStack.navigateBack`

| Espacio de nombres original `global (window)` | Nuevo espacio de nombres `pages.backStack`  |
| - | - |
| `registerBackButtonHandler` | `pages.backStack.registerBackButtonHandler`

##### <a name="pagesappbutton"></a>*pages.appButton*

| Espacio de nombres original `global (window)` | Nuevo espacio de nombres `pages.appButton`  |
| - | - |
| `registerAppButtonClickHandler` | `pages.appButton.onClick` (nombre cambiado)
| `registerAppButtonHoverEnterHandler` | `pages.appButton.onHoverEnter` (nombre cambiado)
| `registerAppButtonHoverLeaveEnter` | `pages.appButton.onHoverLeave` (nombre cambiado)
| interfaz `FrameContext` | `pages.appButton.FrameInfo` (nombre cambiado) |

#### <a name="dialog-namespace"></a>espacio de nombres *dialog*

El espacio de nombres *tasks* de TeamsJS se ha cambiado *dialog*, y se ha cambiado el nombre de las siguientes API:

| Espacio de nombres original `tasks` | Nuevo espacio de nombres `dialog`  |
| - | - |
| `tasks.startTask` | `dialog.open` (nombre cambiado) |
| `tasks.submitTasks` | `dialog.submit` (nombre cambiado) |
| `tasks.updateTasks` | `dialog.resize` (nombre cambiado) |
| enumeración `tasks.TaskModuleDimension` | `dialog.DialogDimension` (nombre cambiado) |
| interfaz `tasks.TaskInfo` | `dialog.DialogInfo` (nombre cambiado) |

#### <a name="teamscore-namespace"></a>espacio de nombres *teamsCore*

Para generalizar el SDK de TeamsJS para ejecutar otros hosts de Microsoft 365 como Office y Outlook, la funcionalidad específica de Teams (originalmente en el espacio de nombres *global*) se ha movido a un espacio de nombres *teamsCore*:

| Espacio de nombres original `global (window)` | Nuevo espacio de nombres `teamsCore`  |
| - | - |
| `enablePrintCapability` | `teamsCore.enablePrintCapability`
| `print` | `teamsCore.print`
| `registerOnLoadHandler` | `teamsCore.registerOnLoadHandler`
| `registerBeforeUnloadHandler` | `teamsCore.registerBeforeUnloadHandler`
| `registerFocusEnterHandler` | `teamsCore.registerFocusEnterHandler`

### <a name="updates-to-the-context-interface"></a>Actualizaciones de la interfaz *Context*

La interfaz `Context` se ha movido al espacio de nombres `app` y se ha actualizado para agrupar propiedades similares para mejorar la escalabilidad mientras se ejecuta en Outlook y Office, además de Teams.

Se ha agregado una nueva propiedad `app.Context.app.host.name` para permitir que las pestañas personales diferencien la experiencia del usuario en función de la aplicación host.

También puede visualizar los cambios revisando la función  [`transformLegacyContextToAppContext`](https://github.com/OfficeDev/microsoft-teams-library-js/blob/2.0-preview/packages/teams-js/src/public/app.ts) en el origen de la versión preliminar v2 del SDK de TeamsJS.

| Nombre original en la interfaz `Context` | Nueva ubicación en `app.Context` |
| - | - |
| `appIconPosition` | `app.Context.app.iconPositionVertical` |
| `appLaunchId`| *NO está disponible en la versión preliminar v2 del SDK de cliente de Teams* |
| `appSessionId` | `app.Context.app.sessionId`|
| `channelId`| `app.Context.channel.id` |
| `channelName`| `app.Context.channel.displayName`|
| `channelRelativeUrl` | `app.Context.channel.relativeUrl`|
| `channelType`| `app.Context.channel.membershipType` |
| `chatId` | `app.Context.chat.id`|
| `defaultOneNoteSectionId`| `app.Context.channel.defaultOneNoteSectionId`|
| `entityId` | `app.Context.page.id`|
| `frameContext` | `app.Context.page.frameContext`|
| `groupId`| `app.Context.team.groupId` |
| `hostClientType` | `app.Context.app.host.clientType`|
| `hostTeamGroupId`| `app.Context.channel.ownerGroupId` |
| `hostTeamTenantId` | `app.Context.channel.ownerTenantId`|
| `isCallingAllowed` | `app.Context.user.isCallingAllowed`|
| `isFullScreen` | `app.Context.page.isFullScreen`|
| `isMultiWindow`| `app.Context.page.isMultiWindow` |
| `isPSTNCallingAllowed` | `app.Context.user.isPSTNCallingAllowed`|
| `isTeamArchived` | `app.Context.team.isArchived`|
| `locale` | `app.Context.app.locale` |
| `loginHint`| `app.Context.user.loginHint` |
| `meetingId`| `app.Context.meeting.id` |
| `osLocaleInfo` | `app.Context.app.osLocaleInfo` |
| `parentMessageId`| `app.Context.app.parentMessageId`|
| `ringId` | `app.Context.app.host.ringId`|
| `sessionId`| `app.Context.app.host.sessionId` |
| `sourceOrigin` | `app.Context.page.sourceOrigin`|
| `subEntityId`| `app.Context.page.subPageId` |
| `teamId` | `app.Context.team.internalId`|
| `teamSiteDomain` | `app.Context.sharepointSite.domain`|
| `teamSitePath` | `app.Context.sharepointSite.path`|
| `teamSiteUrl`| `app.Context.sharepointSite.url` |
| `teamTemplateId` | `app.Context.team.templateId`|
| `teamType` | `app.Context.team.type`|
| `tenantSKU`| `app.Context.user.tenant.teamsSku` |
| `tid`| `app.Context.user.tenant.id` |
| `upn` | `app.Context.user.userPrincipalName` |
|`userClickTime`| `app.Context.app.userClickTime`|
| `userFileOpenPreference` | `app.Context.app.userFileOpenPreference` |
| `userLicenseType`| `app.Context.user.licenseType` |
| `userObjectId` | `app.Context.user.id`|
| `userTeamRole` | `app.Context.team.userRole`|
| `userDisplayName` | `app.Context.user.displayName` |
| N/D | `app.Context.app.host.name`|

## <a name="next-steps"></a>Pasos siguientes

También puede obtener más información sobre los cambios importantes en el [Registro de cambios de la versión preliminar v2 del SDK de TeamsJS](https://github.com/OfficeDev/microsoft-teams-library-js/blob/2.0-preview/packages/teams-js/CHANGELOG.md)y la [Referencia de la API de la versión preliminar v2 del SDK de TeamsJS](/javascript/api/overview/msteams-client?view=msteams-client-js-beta&preserve-view=true).

Cuando esté listo para probar las aplicaciones de Teams que se ejecutan en Outlook y Office, vea:

> [!div class="nextstepaction"]
> [Ampliar la aplicación de Teams en Microsoft 365](overview.md)

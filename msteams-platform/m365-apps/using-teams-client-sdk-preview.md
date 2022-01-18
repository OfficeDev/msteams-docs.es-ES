---
title: Microsoft Teams sdk de cliente de JavaScript v2 Preview
description: Comprender los cambios que se Microsoft Teams sdk de cliente de JavaScript v2 Preview
ms.date: 11/15/2021
ms.topic: conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 7a8b5ed919cac07b1d0710a1f23c0ade0cca2ffb
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059824"
---
# <a name="microsoft-teams-javascript-client-sdk-v2-preview"></a>Microsoft Teams sdk de cliente de JavaScript v2 Preview

Con la versión preliminar del SDK de cliente de JavaScript de [Microsoft Teams,](/javascript/api/overview/msteams-client?view=msteams-client-js-beta&preserve-view=true)el SDK de Teams existente ( , o simplemente ) se ha `@microsoft/teams-js` `TeamsJS` refactorizado para permitir Teams los desarrolladores de Teams la capacidad de ampliar las aplicaciones de [Teams](overview.md)para que se ejecuten en Outlook y Office . Desde una perspectiva funcional, el SDK de TeamsJS v2 Preview ( ) es un superconjunto del SDK de TeamsJS actual, admite la funcionalidad de la aplicación Teams existente al tiempo que agrega la capacidad de hospedar aplicaciones Teams en Outlook y `@microsoft/teams-js@next` Office.

Hay dos cambios significativos en teamsJS SDK v2 Preview que el código tendrá que tener en cuenta para poder ejecutarse en otras Microsoft 365 aplicaciones:

* [**Ahora, las funciones de devolución de llamada devuelven objetos Promise.**](#callbacks-converted-to-promises) Todas las funciones existentes con un parámetro de devolución de llamada se han modernizado para devolver un objeto Promise de [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) para mejorar el control de las operaciones asincrónicas y la legibilidad del código.

 - [**Las API ahora están organizadas en *funcionalidades.***](#apis-organized-into-capabilities) Puede pensar en las capacidades como agrupaciones lógicas de API que proporcionan funciones similares, como `authentication` , , , , y `calendar` `mail` `monetization` `meeting` `sharing` .

 Puedes usar la extensión [Teams Toolkit para](https://aka.ms/teams-toolkit) Visual Studio Code para simplificar el proceso de actualización de la aplicación Teams, como se describe en la siguiente sección.

> [!NOTE]
> Habilitar una aplicación de Teams existente para que se ejecute en Outlook y Office requiere:
> 1. Dependencia de la `@microsoft/teams-js@2.0.0-beta.1` o posterior, y
> 2. Modificar el código de aplicación existente de acuerdo con los cambios necesarios descritos en este documento.
>
>  Si hace referencia (o posterior) desde una aplicación de Teams existente, verá advertencias de desuso si el código llama a las API que `@microsoft/teams-js@2.0.0-beta.1` han cambiado. Se proporciona una capa de traducción de API (asignación del SDK actual a las llamadas a la API del SDK de vista previa) para permitir que las aplicaciones de Teams existentes continúen trabajando en Teams hasta que puedan actualizar el código para que funcione con teamsJS SDK v2 Preview. Después de actualizar el código con los cambios descritos en este artículo, la pestaña personal también se ejecutará en Outlook y Office.

## <a name="updating-to-the-teams-client-sdk-v2-preview"></a>Actualización a la versión preliminar Teams SDK de cliente de Teams versión preliminar

La forma más sencilla de actualizar la aplicación Teams para usar teamsJS SDK v2 Preview es usar la extensión Teams Toolkit para Visual Studio Code. [](https://aka.ms/teams-toolkit) Esta sección le llevará a través de los pasos para hacerlo. Si prefiere actualizar manualmente el código, consulte las secciones Devoluciones de llamada convertida en promesas y [API](#apis-organized-into-capabilities) [organizadas](#callbacks-converted-to-promises) en funcionalidades para obtener más información sobre los cambios en la API necesarios.

### <a name="1-install-the-latest-teams-toolkit-vs-code-extension"></a>1. Instalar la última extensión Teams Toolkit VS Code archivo

En el *marketplace Visual Studio Code extensiones,* busque **Teams Toolkit** e instale la versión o `2.10.0` posterior. El kit de herramientas proporciona dos comandos para ayudar al proceso:

1. Un comando para actualizar el esquema de manifiesto
1. Un comando para actualizar las referencias del SDK y los sitios de llamada

Estas son las dos actualizaciones clave que necesitarás para ejecutar una aplicación Teams pestaña personal en otras aplicaciones Microsoft 365: ''

### <a name="2-updating-the-manifest"></a>2. Actualización del manifiesto

# <a name="teams-toolkit"></a>[Teams Toolkit](#tab/manifest-teams-toolkit)

1. Abra la *paleta Comandos*: `Ctrl+Shift+P`
1. Ejecutar **Teams: actualizar el Teams para** admitir Outlook y Office aplicaciones y seleccionar el archivo de manifiesto de la aplicación. Los cambios se realizarán en su lugar.

# <a name="manual-steps"></a>[Pasos manuales](#tab/manifest-manual)

Abre el Teams de la aplicación y actualiza `$schema` el y con los siguientes `manifestVersion` valores:

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```
---

Si usó Teams Toolkit para crear su aplicación personal, también puede usarla para validar los cambios en el archivo de manifiesto e identificar los errores. Abra la paleta de comandos y busque Teams: validar el archivo de manifiesto o seleccione la opción en el menú Implementación del Teams Toolkit (busque el icono Teams a la izquierda de `Ctrl+Shift+P` Visual Studio Code). 

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams Toolkit &quot;Validar archivo de manifiesto&quot; en el menú &quot;Implementación&quot;":::

### <a name="2-update-sdk-references"></a>2. Actualizar referencias de SDK

Para ejecutar en Outlook y Office, la aplicación tendrá que depender del paquete [npm](https://www.npmjs.com/package/@microsoft/teams-js/v/2.0.0-beta.1) `@microsoft/teams-js@2.0.0-beta.1` (o de una versión *beta* posterior). Para realizar estos pasos manualmente y para obtener más información sobre los cambios en la API, consulte las siguientes secciones sobre devoluciones de llamada convertida en [promesas](#callbacks-converted-to-promises) y API organizadas [en funcionalidades.](#apis-organized-into-capabilities)

1. Asegúrese de que tiene [Teams Toolkit](https://aka.ms/teams-toolkit) `v2.10.0` o posterior
1. Abra la *paleta Comandos*: `Ctrl+Shift+P`
1. Ejecutar el comando `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`

Después de finalizar, la utilidad habrá actualizado el archivo con la dependencia `package.json` de TeamsJS SDK v2 Preview (o posterior) y los archivos y se `@microsoft/teams-js@2.0.0-beta.1` `*.js/.ts` `*.jsx/.tsx` actualizarán con:

> [!div class="checklist"]
> * `package.json` referencias a TeamsJS SDK v2 Preview
> * Instrucciones Import para TeamsJS SDK v2 Preview
> * [Llamadas de función, enumeración e interfaz](#apis-organized-into-capabilities) a TeamsJS SDK v2 Preview
> * `TODO` avisos de comentarios para revisar las áreas que podrían estar afectadas por los [cambios en](#updates-to-the-context-interface) la interfaz de contexto
> * `TODO` avisos de comentarios para asegurarse de que la conversión [a funciones de promesas](#callbacks-converted-to-promises) de funciones de estilo de devolución de llamada ha ido bien en cada sitio de llamada que encontró la herramienta

> [!IMPORTANT]
> El código dentro de los archivos html no es compatible con las herramientas de actualización y requerirá cambios manuales.

## <a name="callbacks-converted-to-promises"></a>Devoluciones de llamada convertida en promesas

Teams las API que anteriormente tomaron un parámetro de devolución de llamada se actualizaron para devolver un objeto Promise [de](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) JavaScript. Entre ellas se incluyen las siguientes API:

```js
app.getContext, app.initialize, appInstallDialog.openAppInstallDialog, authentication.authenticate, authentication.getAuthToken, authentication.getUser, authentication.registerAuthenticationHandlers was removed to support using Promises, calendar.openCalendarItem, calendar.composeMeeting, call.startCall, core.executeDeepLink, location.getLocation, location.showLocation, mail.openMailItem, mail.composeMail, media.captureImage, media.getMedia, media.selectMedia, media.viewImages, media.scanBarCode, meeting.getAppContentStageSharingCapabilities, meeting.getAuthenticationTokenForAnonymousUser, meeting.getIncomingClientAudioState, meeting.getLiveStreamState, meeting.getMeetingDetails, meeting.requestStartLiveStreaming, meeting.requestStopLiveStreaming, meeting.shareAppContentToStage, meeting.stopSharingAppContentToStage, meeting.toggleIncomingClientAudio, meeting.getAppContentStageSharingState, pages.backStack.navigateBack, pages.navigateCrossDomain, pages.navigateToTab, pages.tabs.getMruTabInstances, pages.tabs.getTabInstances, pages.config.setConfig, pages.config.getConfig, people.selectPeople, ChildAppWindow.postMessage, ParentAppWindow.postMessage
```

Tendrás que actualizar la forma en que el código llama a cualquiera de estas API para usar Promesas. Por ejemplo, si el código llama a una API Teams como esta:

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Este código:

```js
import microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context) => { /* ... */ });
```

Debe actualizarse a:

```js
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context: Context) => {
    /*...*/
});
```

... o el patrón `async/await` equivalente:

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

... o el patrón `async/await` equivalente:

```TypeScript
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context: Context = await app.getContext();
  /*...*/
}
```

---

> [!TIP]
> Al actualizar el código de TeamsJS SDK v2 Preview con [Teams Toolkit,](#updating-to-the-teams-client-sdk-v2-preview)las actualizaciones necesarias se marcan automáticamente con comentarios `TODO` en el código de cliente.

## <a name="apis-organized-into-capabilities"></a>API organizadas en funcionalidades

Una *funcionalidad es* una agrupación lógica de API que proporcionan una funcionalidad similar. Puede pensar en Microsoft Teams, Outlook y Office, como hosts. Un host admite una funcionalidad determinada si admite todas las API definidas dentro de esa funcionalidad. Un host no puede implementar parcialmente una funcionalidad.  Las funcionalidades pueden estar basadas en características o contenido, como el *cuadro de diálogo o* la *autenticación.* También hay capacidades para tipos de aplicación, como *pestañas/páginas o* *bots,* y otras agrupaciones.

En TeamsJS SDK v2 Preview, las API se definen como funciones en un espacio de nombres de JavaScript cuyo nombre coincide con la funcionalidad necesaria. Si una aplicación se ejecuta en un host que admite la funcionalidad de cuadro de diálogo, la aplicación puede llamar de forma segura a API como (además de otras API relacionadas con cuadros de diálogo definidas en el espacio de `dialog.open` nombres). Mientras tanto, si una aplicación intenta llamar a una API que no es compatible con ese host, la API producirá una excepción.

### <a name="differentiate-your-app-experience"></a>Diferenciar la experiencia de la aplicación

Puede comprobar la compatibilidad de host de una funcionalidad determinada en tiempo de ejecución llamando a la `isSupported()` función en esa funcionalidad (espacio de nombres). Se devolverá si es compatible y, si `true` no es así, y puedes ajustar el comportamiento de la aplicación según `false` corresponda. Esto permite a la aplicación iluminar la interfaz de usuario y la funcionalidad de los hosts que la admiten, al tiempo que se continúa con la ejecución de hosts que no lo son.

El nombre del host en el que se ejecuta la aplicación se expone como una propiedad *hostName* en la interfaz de contexto ( ), que se puede consultar en tiempo de ejecución llamando `app.Context.app.host.name` `getContext` a . También está disponible como un valor de `{hostName}` [marcador de posición de dirección URL](../tabs/how-to/access-teams-context.md#get-context-by-inserting-url-placeholder-values). El procedimiento recomendado es usar el *mecanismo hostName* con moderación:

* **No suponga que** cierta funcionalidad está o no está disponible en un host en función del valor de *la propiedad hostName.* En su lugar, compruebe si hay compatibilidad con la funcionalidad ( `isSupported` ).
* **No use** *hostName* para puerta de llamadas API. En su lugar, compruebe si hay compatibilidad con la funcionalidad ( `isSupported` ).
* **Use** *hostName para* diferenciar el tema de la aplicación en función del host en el que se ejecuta. Por ejemplo, puede usar el Microsoft Teams púrpura como color de énfeño principal al ejecutarse en Teams y Outlook azul cuando se ejecuta en Outlook.
* **Use** *hostName para* diferenciar los mensajes que se muestran al usuario en función del host en el que se ejecuta. Por ejemplo, muestra *Administrar las* tareas en Office cuando se ejecutan en Office en la Web y Administrar las tareas en *Teams* cuando se ejecutan en Microsoft Teams.

### <a name="namespaces"></a>Espacios de nombres

TeamsJS SDK v2 Preview organiza las API en *funcionalidades* mediante espacios de nombres. Varios espacios de nombres nuevos de especial importancia son *app,* *pages,* *dialog* y *teamsCore*.

#### <a name="app-namespace"></a>*Espacio de nombres de la aplicación*

El espacio de nombres contiene las API de nivel superior necesarias para el uso general de la aplicación, en `app` Microsoft Teams, Office y Outlook. Todas las API de otros espacios de nombres de TeamsJS se han movido al espacio de nombres `app` en TeamsJS SDK v2 Preview:

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
| `appInitialization.FailedReason` enumeración | `app.FailedReason` |
| `appInitialization.ExpectedFailureReason` enumeración | `app.ExpectedFailureReason` |
| `appInitialization.IFailedRequest` enumeración | `app.IFailedRequest` |
| `appInitialization.IExpectedFailureRequest` enumeración | `app.IExpectedFailureRequest` |

#### <a name="core-namespace"></a>*espacio de nombres principal*

El `core` espacio de nombres incluye funcionalidad para vínculos profundos.

| Espacio de nombres original `publicAPIs` | Nuevo espacio de nombres `core` |
| - | - |
| `shareDeepLink` | `core.shareDeepLink` |
| `executeDeepLink` | `core.executeDeepLink` |

#### <a name="pages-namespace"></a>*espacio de nombres pages*

El espacio de nombres incluye funciones para ejecutar y navegar páginas web dentro de varios clientes `pages` Microsoft 365, incluidos Teams, Office y Outlook. También incluye varias sub-funcionalidades, implementadas como sub-espacios de nombres.

| Espacio de nombres original `global (window)` | Nuevo espacio de nombres `pages` |
| - | - |
| `setFrameContext` | `pages.setCurrentFrame` (cambiado de nombre) |
| `initializeWithFrameContext` | `pages.initializeWithFrameContext` |
| `registerFullScreenHandler` | `pages.registerFullScreenHandler` |
| `navigateCrossDomain` | `pages.navigateCrossDomain` |
| `returnFocus` | `pages.returnFocus` |

##### <a name="pagestabs"></a>*pages.tabs*

| Espacio de nombres original `global (window)` | Nuevo espacio de nombres `pages.tabs` |
| - | - |
| `getTabInstances` |  `pages.tabs.getTabInstances` |
| `getMruTabInstances` | `pages.tabs.getMruTabInstances` |
| ` navigateToTab` | `pages.tabs.navigateToTab` |

| Espacio de nombres original `navigation` | Nuevo espacio de nombres `pages.tabs` |
| - | - |
| `navigation.navigateToTab` | `pages.tabs.navigateToTab` |

##### <a name="pagesconfig"></a>*pages.config*

| Espacio de nombres original `settings` | Nuevo espacio de nombres `pages.config`  |
| - | - |
| `settings.setSettings` | `pages.config.setConfig` (cambiado de nombre)
| `settings.getSettings` | `pages.config.getConfig` (cambiado de nombre)
| `settings.setValidityState`| `pages.config.setValidityState`
| `settings.initialize` | `pages.config.initialize`
| `settings.registerOnSaveHandler`| `pages.config.registerOnSaveHandler`
| `settings.registerOnRemoveHandler` | `pages.config.registerOnRemoveHandler`
| `settings.Settings` interfaz | `pages.config.Config` (cambiado de nombre)
| `settings.SaveEvent` interfaz | `pages.config.SaveEvent` (cambiado de nombre)
| `settings.RemoveEvent` interfaz | `pages.config.RemoveEvent` (cambiado de nombre)
| `settings.SaveParameters` interfaz | `pages.config.SaveParameters` (cambiado de nombre)
| `settings.SaveEventImpl` interfaz | `pages.config.SaveEventImpl` (cambiado de nombre)

| Espacio de nombres original `global (window)` | Nuevo espacio de nombres `pages.config` |
| - | - |
| `registerEnterSettingsHandler` | `pages.config.registerChangeConfigHandler` (cambiado de nombre)

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
| `registerAppButtonClickHandler` | `pages.appButton.onClick` (cambiado de nombre)
| `registerAppButtonHoverEnterHandler` | `pages.appButton.onHoverEnter` (cambiado de nombre)
| `registerAppButtonHoverLeaveEnter` | `pages.appButton.onHoverLeave` (cambiado de nombre)
| `FrameContext` interfaz | `pages.appButton.FrameInfo` (con el nombre cambiado)) |

#### <a name="dialog-namespace"></a>*espacio de nombres dialog*

El espacio de nombres de tareas *de* TeamsJS se ha cambiado a *cuadro* de diálogo y se ha cambiado el nombre de las siguientes API:

| Espacio de nombres original `tasks` | Nuevo espacio de nombres `dialog`  |
| - | - |
| `tasks.startTask` | `dialog.open` (cambiado de nombre) |
| `tasks.submitTasks` | `dialog.submit` (cambiado de nombre) |
| `tasks.updateTasks` | `dialog.resize` (cambiado de nombre) |
| `tasks.TaskModuleDimension` enumeración | `dialog.DialogDimension` (cambiado de nombre) |
| `tasks.TaskInfo` interfaz | `dialog.DialogInfo` (cambiado de nombre) |

#### <a name="teamscore-namespace"></a>*espacio de nombres teamsCore*

Para generalizar el SDK de TeamsJS para ejecutar otros hosts de Microsoft 365 como Office y Outlook, la funcionalidad específica de Teams (originalmente en el espacio de nombres *global)* se ha movido a un espacio de nombres *teamsCore:*

| Espacio de nombres original `global (window)` | Nuevo espacio de nombres `teamsCore`  |
| - | - |
| `enablePrintCapability` | `teamsCore.enablePrintCapability`
| `print` | `teamsCore.print`
| `registerOnLoadHandler` | `teamsCore.registerOnLoadHandler`
| `registerBeforeUnloadHandler` | `teamsCore.registerBeforeUnloadHandler`
| `registerFocusEnterHandler` | `teamsCore.registerFocusEnterHandler`

### <a name="updates-to-the-context-interface"></a>Actualizaciones de la *interfaz de* contexto

La interfaz se ha movido al espacio de nombres y se ha actualizado para agrupar propiedades similares para mejorar la escalabilidad a medida que se ejecuta en Outlook y Office, además `Context` `app` de Teams.

Se ha agregado `app.Context.app.host.name` una nueva propiedad para permitir que las pestañas personales diferencien la experiencia del usuario en función de la aplicación host.

También puede visualizar los cambios revisando la función en el origen  [`transformLegacyContextToAppContext`](https://github.com/OfficeDev/microsoft-teams-library-js/blob/2.0-preview/packages/teams-js/src/public/app.ts) de TeamsJS SDK v2 Preview.

| Nombre original en la `Context` interfaz | Nueva ubicación en `app.Context` |
| - | - |
| `appIconPosition` | `app.Context.app.iconPositionVertical` |
| `appLaunchId`| *NOT IN Teams client SDK v2 Preview* |
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
|` userClickTime`| `app.Context.app.userClickTime`|
| `userFileOpenPreference` | `app.Context.app.userFileOpenPreference` |
| `userLicenseType`| `app.Context.user.licenseType` |
| `userObjectId` | `app.Context.user.id`|
| ` userTeamRole` | `app.Context.team.userRole`|
| `userDisplayName` | `app.Context.user.displayName` |
| N/D | `app.Context.app.host.name`|

## <a name="next-steps"></a>Siguientes pasos

También puede obtener más información sobre cómo romper los cambios en el registro de cambios de [TeamsJS SDK v2 Preview y](https://github.com/OfficeDev/microsoft-teams-library-js/blob/2.0-preview/CHANGELOG.md) en la Referencia de api de vista previa del [SDK de TeamsJS v2](/javascript/api/overview/msteams-client?view=msteams-client-js-beta&preserve-view=true).

Cuando estés listo para probar las aplicaciones Teams que se ejecutan en Outlook y Office, consulta:

> [!div class="nextstepaction"]
> [Extender la aplicación Teams aplicación en Microsoft 365](overview.md)

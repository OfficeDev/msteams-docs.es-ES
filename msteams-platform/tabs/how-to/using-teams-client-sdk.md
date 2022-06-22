---
title: Creación de pestañas y otras experiencias hospedadas con el SDK de cliente de JavaScript de Microsoft Teams
author: heath-hamilton
ms.author: surbhigupta
description: En este módulo, aprenderá a usar el SDK de cliente de JavaScript de Microsoft Teams, que puede ayudarle a crear experiencias de aplicación hospedadas en <iframe> Teams, Office y Outlook.
ms.localizationpriority: high
ms.topic: conceptual
ms.openlocfilehash: 165b08b3936afe03f492d8e6983c5504d38bad8b
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189511"
---
# <a name="building-tabs-and-other-hosted-experiences-with-the-microsoft-teams-javascript-client-sdk"></a>Creación de pestañas y otras experiencias hospedadas con el SDK de cliente de JavaScript de Microsoft Teams

El SDK de cliente de JavaScript de Microsoft Teams puede ayudarle a crear experiencias hospedadas en Teams, Office y Outlook, donde el contenido de la aplicación se hospeda en un [iframe](https://developer.mozilla.org/docs/Web/HTML/Element/iframe). El SDK es útil para desarrollar aplicaciones con cualquiera de las siguientes funcionalidades de Teams:

* [Pestañas](../../tabs/what-are-tabs.md)
* [Diálogos (módulos de tareas)](../../task-modules-and-cards/what-are-task-modules.md)

A partir de la versión `2.0.0`, el SDK de cliente de Teams existente (`@microsoft/teams-js` o simplemente `TeamsJS`) fue refactorizado para permitir que las [aplicaciones de Teams se ejecuten en Outlook y Office](/microsoftteams/platform/m365-apps/overview), además de Microsoft Teams. Desde una perspectiva funcional, la versión más reciente de TeamsJS admite toda la funcionalidad de la aplicación de Teams existente (v.1.x.x) al tiempo que agrega la capacidad opcional de hospedar aplicaciones de Teams en Outlook y Office.

Esta es la guía de control de versiones actual para varios escenarios de aplicaciones:

[!INCLUDE [pre-release-label](~/includes/teamjs-version-details.md)]

El resto de este artículo le guiará a través de la estructura y las actualizaciones más recientes del SDK de cliente de JavaScript de Teams.

### <a name="microsoft-365-support-running-teams-apps-in-office-and-outlook"></a>Compatibilidad de Microsoft 365 (ejecución de aplicaciones de Teams en Office y Outlook)

TeamsJS v.2.0 presenta la capacidad de que determinados tipos de aplicaciones de Teams se ejecuten en el ecosistema de Microsoft 365. Actualmente, otros hosts de aplicación de Microsoft 365 (incluidos Office y Outlook) para las aplicaciones de Teams admiten un subconjunto de los tipos de aplicaciones y capacidades que puede crear para la plataforma de Teams. Esta compatibilidad se ampliará con el tiempo. Para obtener un resumen de la compatibilidad del host con las aplicaciones de Teams, consulte [Extensión de las aplicaciones de Teams en Microsoft 365](../../m365-apps/overview.md).

En la tabla siguiente se enumeran las funciones de pestañas y cuadros de diálogo (módulos de tareas) de Teams (espacios de nombres públicos) con compatibilidad ampliada para ejecutarse en otros hosts de Microsoft 365.

> [!TIP]
> Puede comprobar la compatibilidad del host de una funcionalidad determinada en runtime llamando a la función `isSupported()` en esa funcionalidad (espacio de nombres).

|Funcionalidad | Soporte del host | Notas |
|-----------|--------------|-------|
| aplicación | Teams, Outlook, Office | Espacio de nombres que representa la inicialización y el ciclo de vida de la aplicación. |
| appInitialization| | Obsoleto. Reemplazado por el espacio de nombres de `app`. |
| appInstallDialog | Teams||
| autenticación | Teams, Outlook, Office | |
| calendar | Teams, Outlook ||
| llamada | Teams||
| chat |Teams||
| cuadro de diálogo | Teams, Outlook, Office | Espacio de nombres que representa cuadros de diálogo (anteriormente denominados *módulos de tareas*). Vea las notas en [Diálogos](#dialogs). |
| Ubicación |Teams| Vea las notas en [Permisos de la aplicación](#app-permissions).|
| mail | Outlook (solo para escritorio de Windows)||
| medios |Teams| Vea las notas en [Permisos de la aplicación](#app-permissions).|
| páginas | Teams, Outlook, Office | Espacio de nombres que representa la navegación de la página. Vea las notas en [Vinculación en profundidad](#deep-linking). |
| people |Teams||
| configuración || Obsoleto. Reemplazado por `pages.config`.|
| uso compartido | Teams||
| tasks | | Obsoleto. Reemplazado por la funcionalidad de `dialog`. Vea las notas en [Diálogos](#dialogs).|
| teamsCore | Teams | Espacio de nombres que contiene la funcionalidad específica de Teams.|
| video | Teams||

#### <a name="app-permissions"></a>Permisos de aplicación

Las funcionalidades de la aplicación que requieren que el usuario conceda [permisos de dispositivo](../../concepts/device-capabilities/device-capabilities-overview.md) (como la *ubicación*) aún no se admiten para las aplicaciones que se ejecutan fuera de Teams. Actualmente no hay ninguna manera de comprobar los permisos de la aplicación en Configuración o en el encabezado de la aplicación cuando se ejecuta en Outlook u Office. Si una aplicación de Teams que se ejecuta en Office o Outlook llama a una API de TeamsJS (o HTML5) que desencadena los permisos del dispositivo, la API generará un error y no mostrará el cuadro de diálogo del sistema que solicita el consentimiento del usuario.

Por ahora, la guía actual consiste en modificar el código para detectar el error:

* Compruebe [isSupported()](#differentiate-your-app-experience) en una funcionalidad antes de usarla. `media`, `meeting` y `files` aún no admiten llamadas *isSupported* y aún no funcionan fuera de Teams.
* Detecte y controle los errores al llamar a las API de TeamsJS y HTML5.

Cuando una API no se admite o genera un error, agregue lógica para que se produzca un error leve o proporcione una solución alternativa. Por ejemplo:

* Dirija al usuario al sitio web de la aplicación.
* Indique al usuario que use la aplicación en Teams para completar el flujo.
* Notifique al usuario que la funcionalidad aún no está disponible.

Además, el procedimiento recomendado es asegurarse de que el manifiesto de la aplicación solo especifique los permisos del dispositivo que está usando.

#### <a name="deep-linking"></a>Vinculación en profundidad

Antes de la versión 2.0 de TeamsJS, todos los escenarios de vinculación en profundidad fueron controlados mediante `shareDeepLink` (para generar un vínculo *a* una parte específica de la aplicación) y `executeDeepLink` (para navegar a un vínculo profundo *desde* o *dentro* de la aplicación). TeamsJS v.2.0 presenta una nueva API, `navigateToApp`, para navegar a páginas (y subpáginas) dentro de una aplicación de forma coherente entre hosts de aplicaciones (Office y Outlook, además de Teams). Esta es la guía actualizada para escenarios de vinculación en profundidad:

##### <a name="deep-links-into-your-app"></a>Vínculos profundos a la aplicación

Use `pages.shareDeepLink` (conocido como *shareDeepLink* antes de TeamsJS v.2.0) para generar y mostrar un vínculo que se pueda copiar para que el usuario lo comparta. Al hacer clic en él, se le pedirá al usuario que instale la aplicación si aún no está instalada para el host de la aplicación (especificada en la ruta de acceso del vínculo).

##### <a name="navigation-within-your-app"></a>Navegación dentro de la aplicación

Use la nueva API de `pages.navigateToApp` para navegar dentro de la aplicación en la aplicación de hospedaje.

Esta API proporciona el equivalente a la navegación a un vínculo profundo (igual a como se usaba *executeDeepLink* antes de caer en desuso) sin necesidad de que la aplicación construya una dirección URL ni administre diferentes formatos de vínculo profundo para distintos hosts de aplicación.

##### <a name="deep-links-out-of-your-app"></a>Vínculos profundos fuera de la aplicación

Para obtener vínculos profundos desde la aplicación a varias áreas de su host actual, use las API fuertemente tipadas proporcionadas por el SDK de TeamsJS. Por ejemplo, use la funcionalidad *Calendario* para abrir un cuadro de diálogo de programación o un elemento de calendario desde la aplicación.

Para vínculos profundos desde la aplicación a otras aplicaciones que se ejecutan en el mismo host, use `pages.navigateToApp`.

Para cualquier otro escenario de vinculación en profundidad externa, puede usar `app.openLink`, que proporciona una funcionalidad similar a la API ahora en desuso (a partir de TeamsJS v.2.0) *executeDeepLink*.

#### <a name="dialogs"></a>Diálogos

A partir de la versión 2.0 de TeamsJS, el concepto de plataforma de Teams de [módulo de tareas](../../task-modules-and-cards/what-are-task-modules.md) fue cambiado a *dialog* para mejorar la coherencia con los conceptos existentes en el ecosistema de desarrolladores de Microsoft 365. En consecuencia, el espacio de nombres `tasks` ha quedado en desuso en favor del nuevo espacio de nombres `dialog`.

Esta nueva funcionalidad de diálogo se divide en una funcionalidad principal (`dialog`) para admitir diálogos basados en HTML y una subfunción, `dialog.bot`, para el desarrollo de diálogos basados en bots.

La funcionalidad de cuadro de diálogo aún no admite [Diálogos de tarjetas adaptables](../../task-modules-and-cards/task-modules/design-teams-task-modules.md). Los diálogos basados en tarjetas adaptables todavía deben invocarse mediante `tasks.startTask()`.

Actualmente, la función `dialog.open` solo funciona para abrir diálogos basados en HTML y devuelve una función de devolución de llamada (`PostMessageChannel`) que puede usar para pasar mensajes (`ChildAppWindow.postMessage`) al cuadro de diálogo recién abierto.  `dialog.open` devuelve una devolución de llamada (en lugar de una Promesa) porque no requiere que la ejecución de la aplicación se pause en espera a que se cierre el cuadro de diálogo (lo que proporciona más flexibilidad para varios patrones de interacción del usuario).

## <a name="whats-new-in-teamsjs-version-20"></a>Novedades de TeamsJS versión 2.0

Hay dos cambios significativos entre las versiones de TeamsJS 1.x.x y v.2.0.0 y posteriores:

* [**Las funciones callback ahora devuelven objetos Promise.**](#callbacks-converted-to-promises) Todas las funciones existentes con parámetros de devolución de llamada en TeamsJS v.1.12 fueron modernizadas para devolver un objeto JavaScript de [Promesa](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise) para mejorar el control de las operaciones asincrónicas y la legibilidad del código.

* [**Las API ahora están organizadas en *funcionalidades*.**](#apis-organized-into-capabilities) Las funcionalidades se pueden considerar como agrupaciones lógicas de API que proporcionan una funcionalidad similar, como `authentication`, `dialog`, `chat` y `calendar`. Cada espacio de nombres representa una funcionalidad independiente.

> [!TIP]
> Puede usar la extensión del [Kit de herramientas de Teams](https://aka.ms/teams-toolkit) para Microsoft Visual Studio Code para simplificar el [Proceso de actualización de TeamsJS v.2.0](#updating-to-the-teams-client-sdk-v200) para una aplicación de Teams existente.

### <a name="backwards-compatibility"></a>Compatibilidad con versiones anteriores

Una vez que empiece a hacer referencia a `@microsoft/teams-js@2.0.0` (o posterior) desde una aplicación de Teams existente, verá advertencias de desuso para cualquier código que llame a las API que hayan cambiado.

Se proporciona una capa de traducción de API (asignación del SDK v.1 a las llamadas API del SDK v.2) para permitir que las aplicaciones de Teams existentes sigan funcionando en Teams hasta que puedan actualizar el código de aplicación para usar los patrones de API de TeamsJS v.2.

#### <a name="teams-only-apps"></a>Aplicaciones solo de Teams

Incluso si pretende que la aplicación solo se ejecute en Teams (y no en Office y Outlook), el procedimiento recomendado es empezar a hacer referencia a la versión más reciente de TeamsJS (*v.2.0* o posterior) tan pronto como sea conveniente con el fin de beneficiarse de las últimas mejoras, las características nuevas y el soporte técnico (incluso para aplicaciones solo de Teams). TeamsJS v.1.12 seguirá siendo compatible, aunque no se agregarán nuevas características ni mejoras.

Una vez que pueda, el siguiente paso es [actualizar el código de aplicación existente](#2-update-sdk-references) con los cambios descritos en este artículo. Mientras tanto, la capa de traducción de API de v.1 a v.2 proporciona compatibilidad con versiones anteriores, lo que garantiza que la aplicación de Teams existente siga funcionando en TeamsJS versión 2.0.

#### <a name="teams-apps-running-across-microsoft-365"></a>Aplicaciones de Teams que se ejecutan en Microsoft 365

La habilitación de una aplicación de Teams existente para que se ejecute en Outlook y Office requiere lo siguiente:

1. Dependencia de TeamsJS versión 2.0 (`@microsoft/teams-js@2.0`) o posterior,

2. [Modificar el código de aplicación existente](#2-update-sdk-references) según los cambios necesarios descritos en este documento y

3. [Actualizar el manifiesto de la aplicación](#3-update-the-manifest-optional) a la versión 1.13 o posterior.

Para obtener más información, vea [Extienda la aplicación de Teams en Microsoft 365](../../m365-apps/overview.md).

### <a name="callbacks-converted-to-promises"></a>Callbacks convertidas a promises

Las API de Teams que anteriormente tomaban un parámetro de devolución de llamada fueron actualizados para devolver un objeto JavaScript de [Promesa](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). Estas incluyen las siguientes API:

```js
app.getContext, app.initialize, appInstallDialog.openAppInstallDialog, app.openLink, authentication.authenticate, authentication.getAuthToken, authentication.getUser, authentication.registerAuthenticationHandlers was removed to support using Promises, calendar.openCalendarItem, calendar.composeMeeting, call.startCall, chat.getChatMembers, conversations.openConversation, location.getLocation, location.showLocation, mail.openMailItem, mail.composeMail, pages.backStack.navigateBack, pages.navigateCrossDomain, pages.navigateToTab, pages.tabs.getMruTabInstances, pages.tabs.getTabInstances, pages.getConfig, pages.config.setConfig, pages.backStack.navigateBack, people.selectPeople, teams.fullTrust.getConfigSetting, teams.fullTrust.joinedTeams.getUserJoinedTeams
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
> Cuando usa el [Kit de herramientas de Teams para actualizar a TeamsJS v.2.0](#updating-to-the-teams-client-sdk-v200), las actualizaciones necesarias se marcan automáticamente con `TODO` comentarios en el código de cliente.

### <a name="apis-organized-into-capabilities"></a>API organizadas en funcionalidades

Una *funcionalidad* es una agrupación lógica de API (mediante el espacio de nombres) que proporciona una funcionalidad similar. Puede considerar a Microsoft Teams, Outlook y Office como hosts para la pestaña de su aplicación. Un host admite una funcionalidad determinada si admite todas las API definidas dentro de esa funcionalidad. Un host no puede implementar parcialmente una funcionalidad. Las funcionalidades pueden basarse en características o contenido, como *diálogo* o *autenticación*. También hay funcionalidades para los tipos de aplicación, como *pestañas* y otras agrupaciones.

A partir de TeamsJS v.2.0, las API se definen como funciones en un espacio de nombres de JavaScript cuyo nombre coincide con su funcionalidad necesaria. Si una aplicación se ejecuta en un host que admite la funcionalidad de *diálogo*, la aplicación puede llamar de forma segura a las API como `dialog.open` (además de otras API relacionadas con cuadros diálogo definidas en el espacio de nombres). Si una aplicación intenta llamar a una API que no se admite en ese host, la API genera una excepción. Para comprobar si el host actual que ejecuta la aplicación admite una funcionalidad determinada, llame a la función [isSupported()](#differentiate-your-app-experience) de su espacio de nombres.

#### <a name="differentiate-your-app-experience"></a>Diferenciar la experiencia de la aplicación

Puede comprobar la compatibilidad del host de una funcionalidad determinada en tiempo de ejecución llamando a la función `isSupported()` en esa funcionalidad (espacio de nombres). Devolverá `true` si es compatible y `false` si no es así, y puede ajustar el comportamiento de la aplicación según corresponda. Esto permite a la aplicación iluminar la interfaz de usuario y la funcionalidad en los hosts que la admiten, mientras continúa ejecutándose en los hosts que no la admiten.

El nombre del host en el que se ejecuta la aplicación se expone como una propiedad *hostName* en la interfaz Context (`app.Context.app.host.name`), que se puede consultar en tiempo de ejecución llamando a `getContext`. También está disponible como un [valor de marcador de posición de dirección URL](./access-teams-context.md#get-context-by-inserting-url-placeholder-values) `{hostName}`. El procedimiento recomendado es usar el mecanismo *hostName* con moderación:

* **No** suponga que cierta funcionalidad está o no está disponible en un host según el valor de la propiedad *hostName*. En su lugar, compruebe la compatibilidad con la funcionalidad (`isSupported`).
* **No** use *hostName* para realizar llamadas a la API. En su lugar, compruebe la compatibilidad con la funcionalidad (`isSupported`).
* **Use** el *hostName* para diferenciar el tema de la aplicación en función del host en el que se ejecuta. Por ejemplo, puede usar el color púrpura de Microsoft Teams como color de énfasis principal cuando se ejecuta en Teams y el azul de Outlook cuando se ejecuta en Outlook.
* **Use***hostName* para diferenciar los mensajes que se muestran al usuario en función del host en el que se ejecuta. Por ejemplo, muestre *Administrar las tareas en Office* cuando se ejecute en Office en la web y *Administrar las tareas en Teams* cuando se ejecute en Teams.

#### <a name="namespaces"></a>Espacios de nombres

A partir de TeamsJS v.2.0, las API se organizan en *funcionalidades* por medio de los espacios de nombres. Varios espacios de nombres nuevos de importancia particular son *app*, *pages*, *dialog* y *teamsCore*.

##### <a name="app-namespace"></a>espacio de nombres *app*

El espacio de nombres `app` contiene las API de nivel superior necesarias para el uso general de la aplicación, en Teams, Office y Outlook. Todas las API de otros espacios de nombres de TeamsJS se movieron al espacio de nombres `app` a partir de TeamsJS v.2.0:

| Espacio de nombres original `global (window)` | Nuevo espacio de nombres `app` |
| - | - |
| `executeDeepLink` | `app.openLink` (nombre cambiado) |
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

##### <a name="pages-namespace"></a>espacio de nombres *pages*

El espacio de nombres `pages` incluye funcionalidad para ejecutar y navegar por páginas web dentro de varios hosts de Microsoft 365, incluidos Teams, Office y Outlook. También incluye varias subfuncionalidades, implementadas como sub-espacios de nombres.

| Espacio de nombres original `global (window)` | Nuevo espacio de nombres `pages` |
| - | - |
| `setFrameContext` | `pages.setCurrentFrame` (nombre cambiado) |
| `initializeWithFrameContext` | `pages.initializeWithFrameContext` |
| `registerFocusEnterHandler` | `pages.registerFocusEnterHandler`
| `registerFullScreenHandler` | `pages.registerFullScreenHandler` |
| `navigateCrossDomain` | `pages.navigateCrossDomain` |
| `returnFocus` | `pages.returnFocus` |
| `shareDeepLink` | `pages.shareDeepLink` |

| Espacio de nombres original `settings` | Nuevo espacio de nombres `pages`  |
| - | - |
| `settings.getSettings` | `pages.getConfig` (nombre cambiado)

###### <a name="pagestabs"></a>*pages.tabs*

| Espacio de nombres original `global (window)` | Nuevo espacio de nombres `pages.tabs` |
| - | - |
| `getTabInstances` |  `pages.tabs.getTabInstances` |
| `getMruTabInstances` | `pages.tabs.getMruTabInstances` |

| Espacio de nombres original `navigation` | Nuevo espacio de nombres `pages.tabs` |
| - | - |
| `navigation.navigateToTab` | `pages.tabs.navigateToTab` |

###### <a name="pagesconfig"></a>*pages.config*

| Espacio de nombres original `settings` | Nuevo espacio de nombres `pages.config`  |
| - | - |
| `settings.setSettings` | `pages.config.setConfig` (nombre cambiado)
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
| `registerChangeConfigHandler` | `pages.config.registerChangeConfigHandler` (nombre cambiado)

###### <a name="pagesbackstack"></a>*pages.backStack*

| Espacio de nombres original `navigation` | Nuevo espacio de nombres `pages.backStack`  |
| - | - |
| `navigation.navigateBack` | `pages.backStack.navigateBack`

| Espacio de nombres original `global (window)` | Nuevo espacio de nombres `pages.backStack`  |
| - | - |
| `registerBackButtonHandler` | `pages.backStack.registerBackButtonHandler`

###### <a name="pagesappbutton"></a>*pages.appButton*

| Espacio de nombres original `global (window)` | Nuevo espacio de nombres `pages.appButton`  |
| - | - |
| `registerAppButtonClickHandler` | `pages.appButton.onClick` (nombre cambiado)
| `registerAppButtonHoverEnterHandler` | `pages.appButton.onHoverEnter` (nombre cambiado)
| `registerAppButtonHoverLeaveEnter` | `pages.appButton.onHoverLeave` (nombre cambiado)
| interfaz `FrameContext` | `pages.appButton.FrameInfo` (nombre cambiado) |

##### <a name="dialog-namespace"></a>espacio de nombres *dialog*

El espacio de nombres *tasks* de TeamsJS se ha cambiado *dialog*, y se ha cambiado el nombre de las siguientes API:

| Espacio de nombres original `tasks` | Nuevo espacio de nombres `dialog`  |
| - | - |
| `tasks.startTask` | `dialog.open` (nombre cambiado) |
| `tasks.submitTasks` | `dialog.submit` (nombre cambiado) |
| `tasks.updateTasks` | `dialog.update.resize` (nombre cambiado) |
| enumeración `tasks.TaskModuleDimension` | `dialog.DialogDimension` (nombre cambiado) |
| interfaz `tasks.TaskInfo` | `dialog.DialogInfo` (nombre cambiado) |

Además, esta funcionalidad se ha dividido en una funcionalidad principal (`dialog`) para admitir diálogos basados en HTML y una subfunción para diálogos basados en bots, `dialog.bot`.

##### <a name="teamscore-namespace"></a>espacio de nombres *teamsCore*

Para generalizar el SDK de TeamsJS para ejecutar otros hosts de Microsoft 365 como Office y Outlook, la funcionalidad específica de Teams (originalmente en el espacio de nombres *global*) se ha movido a un espacio de nombres *teamsCore*:

| Espacio de nombres original `global (window)` | Nuevo espacio de nombres `teamsCore`  |
| - | - |
| `enablePrintCapability` | `teamsCore.enablePrintCapability`
| `print` | `teamsCore.print`
| `registerOnLoadHandler` | `teamsCore.registerOnLoadHandler`
| `registerBeforeUnloadHandler` | `teamsCore.registerBeforeUnloadHandler`

#### <a name="updates-to-the-context-interface"></a>Actualizaciones de la interfaz *Context*

La interfaz `Context` se ha movido al espacio de nombres `app` y se ha actualizado para agrupar propiedades similares para mejorar la escalabilidad mientras se ejecuta en Outlook y Office, además de Teams.

Se ha agregado una nueva propiedad `app.Context.app.host.name` para permitir que las pestañas diferencien la experiencia del usuario en función de la aplicación host.

También puede visualizar los cambios revisando la función `transformLegacyContextToAppContext` en el [origen de TeamsJS v.2.0](https://github.com/OfficeDev/microsoft-teams-library-js/blob/main/packages/teams-js/src/public/app.ts) (archivo *app.ts*).

| Nombre original en la interfaz `Context` | Nueva ubicación en `app.Context` |
| - | - |
| `appIconPosition` | `app.Context.app.iconPositionVertical` |
| `appLaunchId`| *NO EN TeamsJS v.2.0* |
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

## <a name="updating-to-the-teams-client-sdk-v200"></a>Actualización al SDK v.2.0.0 del cliente de Teams

La manera más sencilla de actualizar la aplicación de Teams para usar TeamsJS v.2.0 es usar la extensión del [Kit de herramientas de Teams](https://aka.ms/teams-toolkit) para Visual Studio Code. Esta sección le guiará a través de los pasos para hacerlo. Si prefiere actualizar manualmente el código, consulte las secciones [Callbacks convertidos en promises](#callbacks-converted-to-promises) y [APIs organizados en funcionalidades](#apis-organized-into-capabilities) para obtener más detalles sobre los cambios necesarios en la API.

### <a name="1-install-the-latest-teams-toolkit-visual-studio-code-extension"></a>1. Instalar la extensión Kit de herramientas de Teams de Visual Studio Code más reciente

En el *Marketplace de extensiones de Visual Studio Code*, busque **Kit de herramientas de Teams** e instale la versión `2.10.0` o posterior.

### <a name="2-update-sdk-references"></a>2. Actualizar referencias del SDK

Para ejecutarse en Outlook y Office, la aplicación tendrá que depender del [paquete npm](https://www.npmjs.com/package/@microsoft/teams-js/v/2.0.0) `@microsoft/teams-js@2.0.0` (o una versión posterior). Para realizar estos pasos manualmente y obtener más información sobre los cambios en la API, vea las secciones siguientes sobre [Callbacks convertidas en promises](#callbacks-converted-to-promises) y [API organizados en funcionalidades](#apis-organized-into-capabilities).

1. Asegúrese de que tiene [Kit de herramientas de Teams](https://aka.ms/teams-toolkit) `v.2.10.0` o posterior
1. Abra la *Paleta de comandos*: `Ctrl+Shift+P`
1. Ejecute el comando `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`

Después de la finalización, la utilidad habrá actualizado el archivo `package.json` con la dependencia de TeamsJS v.2.0 (`@microsoft/teams-js@2.0.0` o posterior) y los archivos de `*.js/.ts` y `*.jsx/.tsx` se actualizarán con:

> [!div class="checklist"]
>
> * `package.json` referencias a TeamsJS v.2.0
> * Instrucciones de importación para TeamsJS v.2.0
> * [Llamadas de función, enumeración e interfaz](#apis-organized-into-capabilities) a TeamsJS v.2.0
> * Comentarios `TODO` de recordatorios para revisar las áreas que podrían verse afectadas por los cambios en la interfaz [Context](#updates-to-the-context-interface)
> * `TODO` recordatorios de comentario para [convertir las funciones de devolución de llamada a promesas](#callbacks-converted-to-promises)

> [!IMPORTANT]
> Las herramientas de actualización no admiten el código dentro de archivos HTML y requerirán cambios manuales.

### <a name="3-update-the-manifest-optional"></a>3. Actualizar el manifiesto (opcional)

Si va a actualizar una aplicación de Teams para que se ejecute en Office y Outlook, también deberá actualizar el manifiesto de la aplicación a la versión 1.13 o posterior. Puede hacerlo fácilmente con el Kit de herramientas de Teams o manualmente.

# <a name="teams-toolkit"></a>[Kit de herramientas de Teams](#tab/manifest-teams-toolkit)

1. Abra la *Paleta de comandos*: `Ctrl+Shift+P`
1. Ejecute el comando **Teams: Actualizar el manifiesto de Teams para admitir las aplicaciones de Outlook y Office** y seleccione el archivo de manifiesto de la aplicación. Se harán cambios.

# <a name="manual-steps"></a>[Pasos manuales](#tab/manifest-manual)

Abra el manifiesto de la aplicación de Teams y actualice `$schema` y `manifestVersion` con los siguientes valores:

```json
{
    "$schema" : "https://developer.microsoft.com/json-schemas/teams/v1.13/MicrosoftTeams.schema.json",
    "manifestVersion" : "1.13"
}
```

---

Si ha usado el Kit de herramientas de Teams para crear su aplicación personal, también puede usarlo para validar los cambios en el archivo de manifiesto e identificar los errores. Abra la paleta de comandos `Ctrl+Shift+P` y busque **Teams: validar el archivo de manifiesto** o seleccione la opción en el menú Implementación del Kit de herramientas de Teams (busque el icono de Teams en el lado izquierdo de Visual Studio Code).

:::image type="content" source="../../m365-apps/images/toolkit-validate-manifest-file.png" alt-text="La opción &quot;Validar archivo de manifiesto&quot; del Kit de herramientas de Teams en el menú &quot;Implementación&quot;":::

## <a name="next-steps"></a>Pasos siguientes

* Use la [referencia de TeamsJS](/javascript/api/overview/msteams-client) para empezar a usar el SDK del cliente de JavaScript de Teams.
* Revise el [registro de cambios](https://github.com/OfficeDev/microsoft-teams-library-js/blob/main/packages/teams-js/CHANGELOG.md) para obtener las actualizaciones más recientes de TeamsJS.

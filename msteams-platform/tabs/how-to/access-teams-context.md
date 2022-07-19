---
title: Obtener contexto para su pestaña
description: En este módulo, aprenderá a obtener el contexto del usuario en las pestañas, el contexto de usuario y la información del contexto de acceso.
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: 63bbc9c0e5f20e293f9230000597860e3f053274
ms.sourcegitcommit: 79d525c0be309200e930cdd942bc2c753d0b718c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2022
ms.locfileid: "66841725"
---
# <a name="get-context-for-your-tab"></a>Obtención del contexto de Teams para la pestaña

La pestaña requiere información contextual para mostrar el contenido pertinente:

* Información básica sobre el usuario, el equipo o la empresa.
* Configuración regional e información del tema.
* `page.id` y `page.subPageId` que identifican lo que hay en esta pestaña (conocido como `entityId` y `subEntityId` antes de TeamsJS v.2.0.0).

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="user-context"></a>Contexto del usuario

El contexto sobre el usuario, el equipo o la empresa puede ser especialmente útil cuando:

* Crea o asocia recursos en la aplicación con el usuario o equipo especificados.
* Se inicia un flujo de autenticación desde Microsoft Azure Active Directory (Azure AD) u otro proveedor de identidades y no es necesario que el usuario vuelva a escribir su nombre de usuario.

Para obtener más información, consulte [Autenticación de un usuario en Microsoft Teams](~/concepts/authentication/authentication.md).

> [!IMPORTANT]
> Aunque esta información de usuario puede ayudar a proporcionar una experiencia de usuario fluida, no debe usarla como prueba de identidad.  Por ejemplo, un atacante puede cargar la página en un explorador y representar información o solicitudes dañinas.

## <a name="access-context-information"></a>Acceso a la información de contexto

Puede acceder a la información contextual de dos formas:

* Usar [valores de marcador de posición de dirección URL](#get-context-by-inserting-url-placeholder-values).
* Desde el objeto de [contexto](/javascript/api/@microsoft/teams-js/app.context) del SDK de cliente javaScript de Microsoft Teams.

### <a name="get-context-by-inserting-url-placeholder-values"></a>Obtener contexto insertando valores de marcador de posición de dirección URL

Use marcadores de posición en la configuración o en las direcciones URL de contenido. Microsoft Teams reemplaza los marcadores de posición por valores pertinentes al determinar la configuración o la dirección URL real del contenido. Los marcadores de posición disponibles incluyen todos los campos del objeto [de contexto](/javascript/api/@microsoft/teams-js/app.context) . Los marcadores de posición comunes incluyen las siguientes listas:

* [{page.id}](/javascript/api/@microsoft/teams-js/app.pageinfo#@microsoft-teams-js-app-pageinfo-id): identificador único definido por el desarrollador para la página definida al [configurar la página](~/tabs/how-to/create-tab-pages/configuration-page.md) por primera vez. (Conocido como `{entityId}` anterior a TeamsJS v.2.0.0).
* [{page.subPageId}](/javascript/api/@microsoft/teams-js/app.pageinfo#@microsoft-teams-js-app-pageinfo-subpageid): el identificador único definido por el desarrollador para la subpágina que estos puntos de contenido definen al generar un [vínculo profundo](~/concepts/build-and-test/deep-links.md) para un elemento específico dentro de la página. (Conocido como `{subEntityId}` anterior a TeamsJS v.2.0.0).
* [{user.loginHint}](/javascript/api/@microsoft/teams-js/app.userinfo#@microsoft-teams-js-app-userinfo-loginhint): valor adecuado como sugerencia de inicio de sesión para Azure AD. Este suele ser el nombre de inicio de sesión del usuario actual en su inquilino principal. (Conocido como `{loginHint}` anterior a TeamsJS v.2.0.0).
* [{user.userPrincipalName}](/javascript/api/@microsoft/teams-js/app.userinfo#@microsoft-teams-js-app-userinfo-userprincipalname): el nombre principal de usuario del usuario actual en el inquilino actual. (Conocido como `{userPrincipalName}` anterior a TeamsJS v.2.0.0).
* [{user.id}](/javascript/api/@microsoft/teams-js/app.userinfo#@microsoft-teams-js-app-userinfo-id): el identificador de objeto de Azure AD del usuario actual en el inquilino actual. (Conocido como `{userObjectId}` anterior a TeamsJS v.2.0.0).
* [{app.theme}](/javascript/api/@microsoft/teams-js/app.appinfo#@microsoft-teams-js-app-appinfo-theme): tema de la interfaz de usuario (UI) actual, como `default`, `dark`o `contrast`. (Conocido como `{theme}` anterior a TeamsJS v.2.0.0).
* [{team.groupId}](/javascript/api/@microsoft/teams-js/app.teaminfo#@microsoft-teams-js-app-teaminfo-groupid): el identificador del grupo de Office 365 en el que reside la pestaña. (Conocido como `{groupId}` anterior a TeamsJS v.2.0.0)
* [{user.tenant.id}](/javascript/api/@microsoft/teams-js/app.tenantinfo#@microsoft-teams-js-app-tenantinfo-id): el identificador de inquilino de Azure AD del usuario actual. (Conocido como `{tid}` anterior a TeamsJS v.2.0.0).
* [{app.locale}](/javascript/api/@microsoft/teams-js/app.appinfo#@microsoft-teams-js-app-appinfo-locale): la configuración regional actual del usuario con formato *languageId-countryId*, por ejemplo `en-us`. (Conocido como `{locale}` anterior a TeamsJS v.2.0.0).

> [!NOTE]
> El marcador de posición `{upn}` anterior está en desuso. Para la compatibilidad con versiones anteriores, actualmente es un sinónimo de `{user.loginHint}`.

Por ejemplo, en el manifiesto de la aplicación si establece el atributo `"https://www.contoso.com/config?name={user.loginHint}&tenant={user.tenant.id}&group={team.groupId}&theme={app.theme}"` tab *configurationUrl* en y el usuario que ha iniciado sesión tiene los siguientes atributos:

* Su nombre de usuario es **user@example.com**.
* Su identificador de inquilino de empresa es **e2653c-etc**.
* Son miembros del grupo de Office 365 con el identificador **00209384-etc**.
* El usuario ha establecido su tema de Teams en **oscuro**.

. . . a continuación, Teams llamará a la siguiente dirección URL al configurar la pestaña:

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="get-context-by-using-the-microsoft-teams-javascript-library"></a>Obtener contexto mediante la biblioteca JavaScript de Microsoft Teams

También puede recuperar la información mencionada previamente usando el [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client)llamando a `microsoftTeams.getContext(function(context) { /* ... */ })`.

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

## <a name="typescript"></a>TypeScript

```TypeScript
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context: Context) => {
    /*...*/
});
```

Patrón equivalente `async/await` :

```TypeScript
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context: Context = await app.getContext();
  /*...*/
}
```

## <a name="javascript"></a>JavaScript

```js
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context) => {
    /*...*/
});
```

Patrón equivalente `async/await` :

```js
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context = await app.getContext();
  /*...*/
}
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

## <a name="typescript"></a>TypeScript

```TypeScript
import * as microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context: microsoftTeams.Context) => {
  /* ... */
});
```

## <a name="javascript"></a>JavaScript

```js
import microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context) => {
  /* ... */ 
});
```

---

En la tabla siguiente se enumeran las propiedades de contexto usadas habitualmente del objeto *de contexto* :

| Nombre de TeamsJS v2 | Nombre de TeamsJS v1 | Descripción |
|-----------------|-----------------|-------------|
| team.internalId | teamId | Identificador de Microsoft Teams para el equipo con el que está asociado el contenido. |
| team.displayName | teamName | Nombre del equipo al que está asociado el contenido. |
| channel.id | channelId | Identificador de Microsoft Teams para el canal con el que está asociado el contenido. |
| channel.displayName | channelName | Nombre del canal con el que está asociado el contenido. |
| chat.id | chatId | Identificador de Microsoft Teams para el chat con el que está asociado el contenido. |
| app.locale | configuración regional | Configuración regional actual que el usuario ha configurado para la aplicación con formato languageId-countryId (por ejemplo, en-us). |
| page.id | entityId | Identificador único definido por el desarrollador para la página a la que apunta este contenido. |
| page.subPageId | subEntityId | Identificador único definido por el desarrollador para la subpágina a la que apunta este contenido. Este campo debe usarse para restaurar a un estado específico dentro de una página, como desplazarse hacia o activar un fragmento de contenido específico. |
| user.loginHint | loginHint | Valor adecuado para su uso como login_hint al autenticarse con Azure AD. Dado que un usuario malintencionado puede ejecutar el contenido en un explorador, este valor solo debe usarse como sugerencia sobre quién es el usuario y nunca como prueba de identidad. Este campo solo está disponible cuando se solicita el permiso de identidad en el manifiesto. |
| user.userPrincipalName | Upn | UPN del usuario actual. Puede ser un UPN autenticado externamente (por ejemplo, usuarios invitados). Dado que una entidad malintencionada ejecuta el contenido en un explorador, este valor solo se debe usar como sugerencia sobre quién es el usuario y nunca como prueba de identidad. Este campo solo está disponible cuando se solicita el permiso de identidad en el manifiesto. |
| user.id | userObjectId | Identificador de objeto de Azure AD del usuario actual. Dado que una entidad malintencionada ejecuta el contenido en un explorador, este valor solo se debe usar como sugerencia sobre quién es el usuario y nunca como prueba de identidad. Este campo solo está disponible cuando se solicita el permiso de identidad en el manifiesto. |
| user.tenant.id | Tid | Identificador de inquilino de Azure AD del usuario actual. Dado que un usuario malintencionado puede ejecutar el contenido en un explorador, este valor solo debe usarse como sugerencia sobre quién es el usuario y nunca como prueba de identidad. Este campo solo está disponible cuando se solicita el permiso de identidad en el manifiesto. |
| team.groupId | groupId | El identificador de grupo Office 365 para el equipo al que está asociado el contenido. Este campo solo está disponible cuando se solicita el permiso de identidad en el manifiesto. |
| app.theme  | theme | El tema actual de la interfaz de usuario: predeterminado, oscuro, contraste |
| page.isFullScreen | IsFullScreen | Indica si la página está en modo de pantalla completa. |
| team.type | teamType | Tipo del equipo. |
| sharepointSite.teamSiteUrl | teamSiteUrl | Sitio de SharePoint raíz asociado al equipo. |
| sharepointSite.teamSiteDomain | teamSiteDomain | Dominio del sitio de SharePoint raíz asociado al equipo. |
| sharepointSite.teamSitePath | teamSitePath | Ruta de acceso relativa al sitio de SharePoint asociado al equipo. |
| channel.relativeUrl | channelRelativeUrl | Ruta de acceso relativa a la carpeta de SharePoint asociada al canal. |
| app.host.sessionId | sessionId | Identificador único de la sesión de host actual para su uso en la correlación de datos de telemetría. |
| team.userRole | userTeamRole | Rol del usuario en el equipo. Dado que un usuario malintencionado puede ejecutar el contenido en un explorador, este valor solo debe usarse como sugerencia en cuanto al rol del usuario y nunca como prueba de su rol. |
| team.isArchived | isTeamArchived | Indica si el equipo está archivado. Las aplicaciones deben usarlo como señal para evitar cambios en el contenido asociado a los equipos archivados. |
| app.host.clientType | hostClientType | Tipo del cliente host. Los valores posibles son: android, ios, web, desktop, rigel |
| page.frameContext | frameContext | Contexto donde se carga la dirección URL de página (contenido, tarea, configuración, eliminación, sidePanel) |
| sharepoint | sharepoint | Contexto de SharePoint. Esto solo está disponible cuando se hospeda en SharePoint. |
| user.tenant.teamsSku | tenantSKU | Tipo de licencia para el inquilino de usuario actual. Los valores posibles son enterprise, free, edu, unknown |
| user.licenseType | userLicenseType | Tipo de licencia para el usuario actual. Los valores posibles son planes empresariales E1, E3 y E5 |
| app.parentMessageId | parentMessageId | Identificador del mensaje primario desde el que se inició este módulo de tareas. Esto solo está disponible en los módulos de tareas iniciados desde tarjetas de bot. |
| app.host.ringId | ringId | Identificador de anillo actual. |
| app.sessionId | appSessionId | Identificador único de la sesión de host actual para su uso en la correlación de datos de telemetría. |
| user.isCallingAllowed | isCallingAllowed | Representa si se permite la llamada para el usuario que ha iniciado sesión actual. |
| user.isPSTNCallingAllowed | isPSTNCallingAllowed | Indica si se permite la llamada RTC para el usuario actual. |
| meeting.id | Id. de la reunión | Identificador de reunión que usa la pestaña al ejecutarse en el contexto de la reunión. |
| channel.defaultOneNoteSectionId | defaultOneNoteSectionId | Identificador de sección de OneNote vinculado al canal. |
| page.isMultiWindow | isMultiWindow | Indicación de si la pestaña está en una ventana emergente. |

Para obtener más información, consulte [Novedades a la interfaz *context*](using-teams-client-sdk.md#updates-to-the-context-interface) y la referencia de la API [de interfaz de contexto](/javascript/api/@microsoft/teams-js/app.context).

## <a name="retrieve-context-in-private-channels"></a>Recuperar contexto en canales privados

Cuando la página de contenido se carga en un canal privado, los datos que recibe de la `getContext` llamada se ofuscan para proteger la privacidad del canal.

Los campos siguientes se cambian cuando la página de contenido está en un canal privado:

* `team.groupId`: no definido para canales privados
* `team.internalId`: se establece en el threadId del canal privado.
* `team.displayName`: se establece en el nombre del canal privado.
* `sharepointSite.url`: se establece en la dirección URL de un sitio de SharePoint único y distinto para el canal privado.
* `sharepointSite.path`: se establece en la ruta de acceso de un sitio de SharePoint único y distinto para el canal privado.
* `sharepointSite.domain`: se establece en el dominio de un dominio de sitio de SharePoint único y distinto para el canal privado.

Si la página usa cualquiera de estos valores, el valor del `channel.membershipType` campo debe ser `Private` determinar si la página se carga en un canal privado y puede responder correctamente.

## <a name="retrieve-context-in-microsoft-teams-connect-shared-channels"></a>Recuperación del contexto en Microsoft Teams Connect canales compartidos

> [!NOTE]
> Actualmente, Microsoft Teams Connect canales compartidos solo están en [versión preliminar para desarrolladores](../../resources/dev-preview/developer-preview-intro.md).

Cuando la página de contenido se carga en un canal compartido Microsoft Teams Connect, los datos que recibe de la `getContext` llamada se modifican debido a la lista única de usuarios en canales compartidos.

Los campos siguientes se cambian cuando la página de contenido está en un canal compartido:

* `team.groupId`: no definido para canales compartidos.
* `team.internalId`: se establece en el `threadId` del equipo, el canal se comparte para el usuario actual. Si el usuario tiene acceso a varios equipos, se establece en el equipo que hospeda (crea) el canal compartido.
* `team.displayName`: se establece en el nombre del equipo, el canal se comparte para el usuario actual. Si el usuario tiene acceso a varios equipos, se establece en el equipo que hospeda (crea) el canal compartido.
* `sharepointSite.url`: se establece en la dirección URL de un sitio de SharePoint único y distinto para el canal compartido.
* `sharepointSite.path`: se establece en la ruta de acceso de un sitio de SharePoint único y distinto para el canal compartido.
* `sharepointSite.domain`: se establece en el dominio de un dominio de sitio de SharePoint único y distinto para el canal compartido.

Además de estos cambios de campo, hay dos nuevos campos disponibles para los canales compartidos:

* `hostTeamGroupId`: se establece en el `team.groupId` asociado al equipo de hospedaje o al equipo que creó el canal compartido. La propiedad puede hacer que las llamadas de Microsoft Graph API recuperen la pertenencia del canal compartido.
* `hostTeamTenantId`: se establece en el `channel.ownerTenantId` asociado al equipo de hospedaje o al equipo que creó el canal compartido. Se puede hacer referencia cruzada a la propiedad con el identificador de inquilino del usuario actual que se encuentra en el `user.tenant.id` campo del objeto de *contexto* para determinar si el usuario es interno o externo al inquilino del equipo de hospedaje.

Si la página usa cualquiera de estos valores, el valor del `channel.membershipType` campo debe ser `Shared` determinar si la página se carga en un canal compartido y puede responder correctamente.

> [!NOTE]
> Cada vez que un usuario reinicia o vuelve a cargar el cliente web o de escritorio de Teams, se crea un nuevo id. de sesión, al que realiza un seguimiento la sesión de Teams, mientras que, cuando un usuario sale de las aplicaciones de Teams y lo vuelve a cargar en la plataforma teams, se crea un nuevo id. de sesión de aplicación, al que realiza un seguimiento la sesión de la aplicación.

## <a name="handle-theme-change"></a>Controlar el cambio de tema

Puede registrar la aplicación para que se le informe si el tema cambia llamando a `microsoftTeams.app.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.

El `theme` argumento de la función es una cadena con un valor de `default`, `dark`o `contrast`.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Compilar pestañas con tarjetas adaptables](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="see-also"></a>Vea también

* [Directrices de diseño de pestañas](../../tabs/design/tabs.md)
* [Pestañas de Teams](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de grupo o de canal](~/tabs/how-to/create-channel-group-tab.md)
* [Uso de módulos de tareas en pestañas](~/task-modules-and-cards/task-modules/task-modules-tabs.md)

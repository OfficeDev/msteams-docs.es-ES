---
title: Obtener contexto para su pestaña
description: Describe cómo obtener el contexto del usuario para las pestañas
ms.localizationpriority: medium
ms.topic: how-to
keywords: contexto de usuario de las pestañas de Teams
ms.openlocfilehash: 0539f1dc3f31a2b068e80b4ff12b93a26e09b766
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757363"
---
# <a name="get-context-for-your-tab"></a>Obtención del contexto de Teams para la pestaña

La pestaña requiere información contextual para mostrar el contenido pertinente:

* Información básica sobre el usuario, el equipo o la empresa.
* Configuración regional e información del tema.
* Lea o `entityId` `subEntityId` que identifique lo que hay en esta pestaña.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="user-context"></a>Contexto del usuario

El contexto sobre el usuario, el equipo o la empresa puede ser especialmente útil cuando:

* Crea o asocia recursos en la aplicación con el usuario o equipo especificados.
* Se inicia un flujo de autenticación desde Microsoft Azure Active Directory (Azure AD) u otro proveedor de identidades y no es necesario que el usuario vuelva a escribir su nombre de usuario.

Para obtener más información, consulte [autenticación de un usuario en el Microsoft Teams](~/concepts/authentication/authentication.md).

> [!IMPORTANT]
> Aunque esta información de usuario puede ayudar a proporcionar una experiencia de usuario fluida, no debe usarla como prueba de identidad.  Por ejemplo, un atacante puede cargar la página en un explorador y representar información o solicitudes dañinas.

## <a name="access-context-information"></a>Acceso a la información de contexto

Puede acceder a la información contextual de dos formas:

* Insertar valores de marcador de posición de dirección URL.
* Use el [SDK de cliente de JavaScript Microsoft Teams](/javascript/api/overview/msteams-client).

### <a name="get-context-by-inserting-url-placeholder-values"></a>Obtener contexto insertando valores de marcador de posición de dirección URL

Use marcadores de posición en la configuración o en las direcciones URL de contenido. Microsoft Teams reemplaza los marcadores de posición por valores pertinentes al determinar la configuración o la dirección URL real del contenido. Los marcadores de posición disponibles incluyen todos los campos del objeto [de contexto](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-1.12.1&preserve-view=true) . Entre los marcadores de posición comunes se incluyen los siguientes:

* {entityId}: el id. que proporcionó para el elemento en esta pestaña al [configurar la pestaña](~/tabs/how-to/create-tab-pages/configuration-page.md) por primera vez.
* {subEntityId}: el identificador que proporcionó al generar un [vínculo profundo](~/concepts/build-and-test/deep-links.md) para un elemento específico dentro de esta pestaña. Esto se debe usar para restaurar a un estado específico dentro de una entidad; por ejemplo, desplazarse hacia o activar un fragmento de contenido específico.
* {loginHint}: valor adecuado como sugerencia de inicio de sesión para Azure AD. Este suele ser el nombre de inicio de sesión del usuario actual en su inquilino principal.
* {userPrincipalName}: el nombre principal de usuario del usuario actual en el inquilino actual.
* {userObjectId}: el identificador de objeto de Azure AD del usuario actual en el inquilino actual.
* {theme}: tema de la interfaz de usuario (UI) actual, como `default`, `dark`o `contrast`.
* {groupId}: el identificador del grupo de Office 365 en el que reside la pestaña.
* {tid}: el id. del espacio empresarial de Azure AD del usuario actual.
* {locale}: la configuración regional actual del usuario con formato languageId-countryId(en-us).

> [!NOTE]
> El marcador de posición `{upn}` anterior está en desuso. Para la compatibilidad con versiones anteriores, actualmente es un sinónimo de `{loginHint}`.

Por ejemplo, en el manifiesto de pestaña, establezca el `configURL` atributo `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`en , el usuario que ha iniciado sesión tiene los siguientes atributos:

* Su nombre de usuario es **user@example.com**.
* Su identificador de inquilino de empresa es **e2653c-etc**.
* Son miembros del grupo de Office 365 con el identificador **00209384-etc**.
* El usuario ha establecido su tema de Teams en **oscuro**.

Al configurar la pestaña, Teams llama a la siguiente dirección URL:

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="get-context-by-using-the-microsoft-teams-javascript-library"></a>Obtener contexto mediante la biblioteca de JavaScript de Microsoft Teams

git-issue-clarify-the-full-set-of-values-any-context-object-property-can-take También puede recuperar la información enumerada anteriormente mediante el [SDK de cliente de JavaScript Microsoft Teams](/javascript/api/overview/msteams-client) llamando a `microsoftTeams.getContext(function(context) { /* ... */ })`.

El código siguiente proporciona un ejemplo de variable de contexto:

```json
{
    "teamId": "The Microsoft Teams ID in the format 19:[id]@thread.skype",
    "teamName": "The name of the current team",
    "channelId": "The channel ID in the format 19:[id]@thread.skype",
    "channelName": "The name of the current channel",
    "chatId": "The chat ID in the format 19:[id]@thread.skype",
    "locale": "The current locale of the user formatted as languageId-countryId (for example, en-us)",
    "entityId": "The developer-defined unique ID for the entity this content points to",
    "subEntityId": "The developer-defined unique ID for the sub-entity this content points to",
    "loginHint": "A value suitable as a login hint for Azure AD. This is usually the login name of the current user, in their home tenant",
    "userPrincipalName": "The principal name of the current user, in the current tenant",
    "userObjectId": "The Azure AD object id of the current user, in the current tenant",
    "tid": "The Azure AD tenant ID of the current user",
    "groupId": "Guid identifying the current Office 365 Group ID",
    "theme": "The current UI theme: default | dark | contrast",
    "isFullScreen": "Indicates if the tab is in full-screen",
    "teamType": "The type of team",
    "teamSiteUrl": "The root SharePoint site associated with the team",
    "teamSiteDomain": "The domain of the root SharePoint site associated with the team",
    "teamSitePath": "The relative path to the SharePoint site associated with the team",
    "channelRelativeUrl": "The relative path to the SharePoint folder associated with the channel",
    "sessionId": "The unique ID for the current Teams session for use in correlating telemetry data",
    "userTeamRole": "The user's role in the team",
    "isTeamArchived": "Indicates if team is archived",
    "hostClientType": "The type of host client. Possible values are android, ios, web, desktop, surfaceHub, teamsRoomsAndroid, teamsPhones, teamsDisplays rigel (deprecated, use teamsRoomsWindows instead)",
    "frameContext": "The context where tab URL is loaded (for example, content, task, setting, remove, sidePanel)",
    "sharepoint": "The SharePoint context is available only when hosted in SharePoint",
    "tenantSKU": "The license type for the current user tenant. Possible values are enterprise, free, edu, unknown",
    "userLicenseType": "The license type for the current user. Possible values are E1, E3, and E5 enterprise plans",
    "parentMessageId": "The parent message ID from which this task module is launched",
    "ringId": "The current ring ID",
    "appSessionId": "The unique ID for the current session used for correlating telemetry data",
    "isCallingAllowed": "Indicates if calling is allowed for the current logged in user",
    "isPSTNCallingAllowed": "Indicates if PSTN calling is allowed for the current logged in user",
    "meetingId": "The meeting ID used by tab when running in meeting context",
    "defaultOneNoteSectionId": "The OneNote section ID that is linked to the channel",
    "isMultiWindow": "The indication whether the tab is in a pop out window"
}
```

También puede recuperar la información enumerada anteriormente mediante el [SDK de cliente de JavaScript Microsoft Teams](/javascript/api/overview/msteams-client) llamando a la `app.getContext()` función . Para obtener más información, vea las propiedades de la [interfaz Context](/javascript/api/@microsoft/teams-js/app.context?view=msteams-client-js-latest&preserve-view=true).


## <a name="retrieve-context-in-private-channels"></a>Recuperar contexto en canales privados

Cuando la página de contenido se carga en un canal privado, los datos que recibe de la `getContext` llamada se ofuscan para proteger la privacidad del canal.

Los campos siguientes se cambian cuando la página de contenido está en un canal privado:

* `groupId`: no definido para canales privados
* `teamId`: se establece en el threadId del canal privado.
* `teamName`: se establece en el nombre del canal privado.
* `teamSiteUrl`: se establece en la dirección URL de un sitio de SharePoint único y distinto para el canal privado.
* `teamSitePath`: se establece en la ruta de acceso de un sitio de SharePoint único y distinto para el canal privado.
* `teamSiteDomain`: se establece en el dominio de un dominio de sitio de SharePoint único y distinto para el canal privado.

Si la página usa cualquiera de estos valores, el valor del `channelType` campo debe ser `Private` determinar si la página se carga en un canal privado y puede responder correctamente.

## <a name="retrieve-context-in-microsoft-teams-connect-shared-channels"></a>Recuperación del contexto en Microsoft Teams Connect canales compartidos

> [!NOTE]
> Actualmente, Microsoft Teams Connect canales compartidos solo están en [versión preliminar para desarrolladores](../../resources/dev-preview/developer-preview-intro.md).

Cuando la página de contenido se carga en un canal compartido Microsoft Teams Connect, los datos que recibe de la `getContext` llamada se modifican debido a la lista única de usuarios en canales compartidos.

Los campos siguientes se cambian cuando la página de contenido está en un canal compartido:

* `groupId`: no definido para canales compartidos.
* `teamId`: se establece en el `threadId` del equipo, el canal se comparte para el usuario actual. Si el usuario tiene acceso a varios equipos, `teamId` se establece en el equipo que hospeda (crea) el canal compartido.
* `teamName`: se establece en el nombre del equipo, el canal se comparte para el usuario actual. Si el usuario tiene acceso a varios equipos, `teamName` se establece en el equipo que hospeda (crea) el canal compartido.
* `teamSiteUrl`: se establece en la dirección URL de un sitio SharePoint único y distinto para el canal compartido.
* `teamSitePath`: se establece en la ruta de acceso de un sitio de SharePoint único y distinto para el canal compartido.
* `teamSiteDomain`: se establece en el dominio de un dominio de sitio SharePoint único y distinto para el canal compartido.

Además de estos cambios de campo, hay dos nuevos campos disponibles para los canales compartidos:

* `hostTeamGroupId`: se establece en el `groupId` asociado al equipo de hospedaje o al equipo que creó el canal compartido. La propiedad puede hacer que las llamadas de Microsoft Graph API recuperen la pertenencia del canal compartido.
* `hostTeamTenantId`: se establece en el `tenantId` asociado al equipo de hospedaje o al equipo que creó el canal compartido. Se puede hacer referencia cruzada a la propiedad con el identificador de inquilino del usuario actual que se encuentra en el `tid` campo de `getContext` para determinar si el usuario es interno o externo al inquilino del equipo de hospedaje.

Si la página usa cualquiera de estos valores, el valor del `channelType` campo debe ser `Shared` determinar si la página se carga en un canal compartido y puede responder correctamente.

> [!NOTE]
> Cada vez que un usuario reinicia o vuelve a cargar el Teams cliente de escritorio o web, se crea un nuevo sessionID, al que realiza un seguimiento Teams sesión, mientras que, cuando un usuario sale de las aplicaciones de Teams y lo vuelve a cargar en Teams plataforma, se crea un nuevo id. de sesión de aplicación, al que realiza un seguimiento la sesión de la aplicación.

## <a name="handle-theme-change"></a>Controlar el cambio de tema

Puede registrar la aplicación para que se le informe si el tema cambia llamando a `app.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.

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

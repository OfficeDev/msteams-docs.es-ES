---
title: Obtener contexto para su pestaña
description: Describe cómo obtener el contexto del usuario para las pestañas
ms.localizationpriority: medium
ms.topic: how-to
keywords: contexto de usuario de las pestañas de Teams
ms.openlocfilehash: a8e8fe6d638f8887a30f65dbf812046738d12dfb
ms.sourcegitcommit: b9af51e24c9befcf46945400789e750c34723e56
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2022
ms.locfileid: "62821734"
---
# <a name="get-context-for-your-tab"></a>Obtención del contexto de Teams para la pestaña

La pestaña requiere información contextual para mostrar contenido relevante:

* Información básica sobre el usuario, el equipo o la compañía.
* Información sobre la configuración regional y el tema.
* Lea el `entityId` o `subEntityId` que identifica lo que hay en esta pestaña.

## <a name="user-context"></a>Contexto del usuario

El contexto sobre el usuario, el equipo o la empresa puede ser especialmente útil cuando:

* Creas o asocias recursos en la aplicación con el usuario o equipo especificado.
* Se inicia un flujo de autenticación Microsoft Azure Active Directory (Azure AD) u otro proveedor de identidades, y no es necesario que el usuario vuelva a escribir su nombre de usuario. 

Para obtener más información, vea [autenticar un usuario en su Microsoft Teams](~/concepts/authentication/authentication.md).

> [!IMPORTANT]
> Aunque esta información de usuario puede ayudar a proporcionar una experiencia de usuario fluida, no debe usarla como prueba de identidad.  Por ejemplo, un atacante puede cargar la página en un explorador y representar información o solicitudes nocivas.

## <a name="access-context-information"></a>Acceder a información de contexto

Puede acceder a la información contextual de dos formas:

* Insertar valores de marcador de posición de dirección URL.
* Use el [MICROSOFT TEAMS cliente de JavaScript](/javascript/api/overview/msteams-client).

### <a name="get-context-by-inserting-url-placeholder-values"></a>Obtener contexto insertando valores de marcador de posición de dirección URL

Use marcadores de posición en la configuración o en las direcciones URL de contenido. Microsoft Teams reemplaza los marcadores de posición por valores pertinentes al determinar la configuración o la dirección URL real del contenido. Los marcadores de posición disponibles incluyen todos los campos del [objeto de](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) contexto. Entre los marcadores de posición comunes se incluyen los siguientes:

* {entityId}: el id. que proporcionó para el elemento en esta pestaña al [configurar la pestaña](~/tabs/how-to/create-tab-pages/configuration-page.md) por primera vez.
* {subEntityId}: el identificador que proporcionó al generar un [vínculo](~/concepts/build-and-test/deep-links.md) profundo para un elemento específico dentro de esta pestaña. Esto debe usarse para restaurar a un estado específico dentro de una entidad; por ejemplo, desplazarse a o activar un elemento de contenido específico.
* {loginHint}: valor adecuado como sugerencia de inicio de sesión para Azure AD. Normalmente, este es el nombre de inicio de sesión del usuario actual en su inquilino principal.
* {userPrincipalName}: el nombre principal de usuario del usuario actual en el inquilino actual.
* {userObjectId}: el Azure AD de objeto del usuario actual en el inquilino actual.
* {theme}: el tema actual de la interfaz de usuario (UI) como `default`, `dark`o `contrast`.
* {groupId}: el identificador del grupo Office 365 en el que reside la pestaña.
* {tid}: el id. del espacio empresarial de Azure AD del usuario actual.
* {locale}: la configuración regional actual del usuario con el formato languageId-countryId(es-es).

> [!NOTE]
> El marcador de posición `{upn}` anterior está en desuso. Para la compatibilidad con versiones anteriores, actualmente es un sinónimo de `{loginHint}`.

Por ejemplo, en el manifiesto de la pestaña se establece el `configURL` atributo en `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`, el usuario que ha iniciado sesión tiene los siguientes atributos:

* Su nombre de usuario **es user@example.com**.
* Su identificador de inquilino de empresa **es e2653c-etc**.
* Son miembros del grupo de Office 365 con el identificador **00209384-etc**.
* El usuario ha establecido su Teams en **oscuro**.

Al configurar la pestaña, Teams llama a la siguiente dirección URL:

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="get-context-by-using-the-microsoft-teams-javascript-library"></a>Obtener contexto mediante la biblioteca Microsoft Teams JavaScript

También puede recuperar la información mencionada previamente usando el [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client)llamando a `microsoftTeams.getContext(function(context) { /* ... */ })`.

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
    "hostClientType": "The type of host client. Possible values are android, ios, web, desktop, rigel",
    "frameContext": "The context where tab URL is loaded (for example, content, task, setting, remove, sidePanel)",
    "sharepoint": "The SharePoint context is available only when hosted in SharePoint",
    "tenantSKU": "The license type for the current user tenant. Possible values are enterprise, free, edu, unknown",
    "userLicenseType": "The license type for the current user",
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

## <a name="retrieve-context-in-private-channels"></a>Recuperar contexto en canales privados

> [!Note]
> Los canales privados están actualmente en la versión preliminar privada para desarrolladores.

Cuando la página de contenido se carga en un canal privado, `getContext` los datos que recibe de la llamada se ocultan para proteger la privacidad del canal. 

Los siguientes campos se cambian cuando la página de contenido está en un canal privado:

* `groupId`: No definido para canales privados
* `teamId`: Establecer en el threadId del canal privado
* `teamName`: Se establece en el nombre del canal privado
* `teamSiteUrl`: Se establece en la dirección URL de un sitio de SharePoint distinto y único para el canal privado
* `teamSitePath`: Se establece en la ruta de acceso de un sitio de SharePoint distinto y único para el canal privado
* `teamSiteDomain`: Se establece en el dominio de un dominio de sitio SharePoint único para el canal privado

Si la página usa cualquiera de estos valores, `channelType` debe comprobar el campo para determinar si la página se carga en un canal privado y responder correctamente.

> [!Note]
> `teamSiteUrl` también funciona bien para los canales estándar.

## <a name="handle-theme-change"></a>Controlar el cambio de tema

Puedes registrar la aplicación para que se te informe si el tema cambia llamando a `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.

El `theme` argumento de la función es una cadena con un valor de `default`, `dark`o `contrast`.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Compilar pestañas con tarjetas adaptables](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="see-also"></a>Vea también

* [Directrices de diseño de pestañas](../../tabs/design/tabs.md)
* [Teams pestañas](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de canal o grupo](~/tabs/how-to/create-channel-group-tab.md)
* [Uso de módulos de tareas en pestañas](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
---
title: Obtener contexto para su pestaña
description: Describe cómo obtener el contexto del usuario para las pestañas
localization_priority: Normal
ms.topic: how-to
keywords: contexto de usuario de las pestañas de Teams
ms.openlocfilehash: 0d9224a941ae4f6a5ad125c93d5877ec49b6df28
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566869"
---
# <a name="get-context-for-your-microsoft-teams-tab"></a>Obtener contexto para la pestaña Microsoft Teams

La pestaña debe requerir información contextual para mostrar contenido relevante:

* Información básica sobre el usuario, el equipo o la compañía.
* Información sobre la configuración regional y el tema.
* Lea el `entityId` o que identifica lo que hay en esta `subEntityId` pestaña.

## <a name="user-context"></a>Contexto del usuario

El contexto sobre el usuario, el equipo o la empresa puede ser especialmente útil cuando:

* Creas o asocias recursos en la aplicación con el usuario o equipo especificado.
* Inicia un flujo de autenticación Azure Active Directory otro proveedor de identidades y no desea que el usuario vuelva a escribir su nombre de usuario. Para obtener más información sobre la autenticación en la Microsoft Teams, vea Autenticar a un [usuario en la Microsoft Teams pestaña](~/concepts/authentication/authentication.md).

> [!IMPORTANT]
> Aunque esta información de usuario puede ayudar a proporcionarle una experiencia de usuario fluida, *no* debe usarla como prueba de identidad. Por ejemplo, un atacante podría cargar su página en un "explorador malo" y representar información o solicitudes dañinas.

## <a name="accessing-context"></a>Acceder al contexto

Puede acceder a la información contextual de dos formas:

* Insertar valores de marcador de posición de dirección URL.
* Use el [MICROSOFT TEAMS cliente de JavaScript](/javascript/api/overview/msteams-client).

### <a name="getting-context-by-inserting-url-placeholder-values"></a>Obtener contexto insertando valores de marcador de posición de la URL

Use marcadores de posición en la configuración o en las direcciones URL de contenido. Microsoft Teams reemplaza los marcadores de posición por valores pertinentes al determinar la configuración o la dirección URL real del contenido. Los marcadores de posición disponibles incluyen todos los campos del objeto del [Contexto](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true). Entre los marcadores de posición comunes se incluyen los siguientes:

* {entityId}: el id. que proporcionó para el elemento en esta pestaña al [configurar la pestaña](~/tabs/how-to/create-tab-pages/configuration-page.md) por primera vez.
* {subEntityId}: el id. que proporcionó al generar un [vínculo profundo](~/concepts/build-and-test/deep-links.md) para un elemento específico _dentro_ de esta pestaña. Debe usarse para restaurar un estado específico dentro de una entidad; por ejemplo, al desplazarse a un elemento de contenido específico o activarlo.
* {loginHint}: un valor adecuado como sugerencia de inicio de sesión de Azure AD. Suele ser el nombre de inicio de sesión del usuario actual, en su espacio empresarial principal.
* {userPrincipalName}: el nombre principal de usuario del usuario actual en el espacio empresarial actual.
* {userObjectId}: el id. del objeto de Azure AD del usuario actual en el espacio empresarial actual.
* {theme}: el tema actual de la interfaz de usuario como `default`, `dark` o `contrast`.
* {groupId}: el id. del grupo de Office 365 en el que se encuentra la pestaña.
* {tid}: el id. del espacio empresarial de Azure AD del usuario actual.
* {locale}: la configuración regional actual del usuario con formato de languageId-countryId. Por ejemplo, en-us.

>[!NOTE]
>El marcador de posición `{upn}` anterior está en desuso. Para la compatibilidad con versiones anteriores, actualmente es un sinónimo de `{loginHint}`.

Por ejemplo, supongamos que en el manifiesto de la pestaña establece el atributo en , el usuario que ha iniciado sesión `configURL` `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"` tiene los siguientes atributos:

* Su nombre de usuario es "user@example.com".
* Su identificador de inquilino de empresa es "e2653c-etc".
* Son miembros del grupo de Office 365 con el identificador '00209384-etc'.
* El usuario ha establecido su Teams en "oscuro".

Al configurar la pestaña, Teams llama a la siguiente dirección URL:

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a>Obtener contexto mediante el uso de la biblioteca de JavaScript de Microsoft Teams

También puede recuperar la información mencionada previamente usando el [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client)llamando a `microsoftTeams.getContext(function(context) { /* ... */ })`.

La variable de contexto es similar al ejemplo siguiente:

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
    "groupId": "Guid identifying the current O365 Group ID",
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
    "defaultOneNoteSectionId": "The OneNote section ID that is linked to the channel"
}
```

## <a name="retrieving-context-in-private-channels"></a>Recuperación del contexto en canales privados

> [!Note]
> Los canales privados están actualmente en la versión preliminar privada para desarrolladores.

Cuando la página de contenido se carga en un canal privado, los datos que reciba de la llamada `getContext` estarán ocultos para proteger la privacidad del canal. Los siguientes campos se cambian cuando la página de contenido está en un canal privado. Si la página utiliza cualquiera de los valores siguientes, tendrá que comprobar el campo `channelType` para determinar si la página se carga en un canal privado y responder según adecuadamente.

* `groupId`: No definido para canales privados
* `teamId`: Establecer en el threadId del canal privado
* `teamName`: Se establece en el nombre del canal privado
* `teamSiteUrl`: Se establece en la dirección URL de un sitio de SharePoint distinto y único para el canal privado
* `teamSitePath`: Se establece en la ruta de acceso de un sitio de SharePoint distinto y único para el canal privado
* `teamSiteDomain`: Se establece en el dominio de un dominio de sitio SharePoint único para el canal privado

> [!Note]
>  teamSiteUrl también funciona bien para los canales estándar.

## <a name="theme-change-handling"></a>Manejo de los cambios de tema

Puede registrar la aplicación para que se le diga si el tema cambia llamando a `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.

El argumento `theme` de la función será una cadena con el valor `default`, `dark` o `contrast`.

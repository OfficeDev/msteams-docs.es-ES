---
title: Obtener contexto para la pestaña
description: Describe cómo obtener el contexto del usuario a las pestañas.
keywords: contexto de usuario de pestañas de Microsoft Teams
ms.openlocfilehash: 5c52e6eea21f0c059f3cd650770e1076f903fb8e
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552440"
---
# <a name="get-context-for-your-microsoft-teams-tab"></a>Obtener contexto para la pestaña de Microsoft Teams

Es posible que la pestaña requiera información contextual para mostrar contenido relevante.

* Es posible que su pestaña necesite información básica sobre el usuario, el equipo o la compañía.
* Es posible que su pestaña necesite información de temas y configuraciones regionales.
* Es posible que la pestaña necesite leer el `entityId` o `subEntityId` que identifique lo que se encuentra en esta ficha.

## <a name="user-context"></a>Contexto de usuario

El contexto del usuario, el equipo o la empresa puede ser especialmente útil cuando

* Debe crear o asociar recursos en la aplicación con el usuario o equipo especificado.
* Desea iniciar un flujo de autenticación con Azure Active Directory u otro proveedor de identidad, y no quiere pedir al usuario que vuelva a escribir su nombre de usuario. (Para obtener más información sobre la autenticación en la pestaña de Microsoft Teams, consulte [Authenticate users in your Microsoft Teams Tab](~/concepts/authentication/authentication.md)).

> [!IMPORTANT]
> Aunque esta información de usuario puede ayudar a proporcionar una experiencia de usuario sin problemas, *no* debería usarla como prueba de identidad. Por ejemplo, un atacante podría cargar la página en un "examinador de errores" y presentar información o solicitudes dañinas.

## <a name="accessing-context"></a>Acceso al contexto

Puede tener acceso a la información de contexto de dos maneras:

* Insertar valores de marcador de dirección URL
* Usar el [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client)

### <a name="getting-context-by-inserting-url-placeholder-values"></a>Obtener el contexto mediante la inserción de valores de marcador de posición de dirección URL

Use marcadores de posición en las direcciones URL de configuración o de contenido. Microsoft Teams sustituye los marcadores de posición por los valores pertinentes al determinar la dirección URL de configuración o de contenido real. Los marcadores de posición disponibles incluyen todos los campos en el objeto de [contexto](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) . Los marcadores de posición comunes son los siguientes:

* {entityId}: el identificador que ha proporcionado para el elemento en esta ficha cuando [configuró la pestaña](~/tabs/how-to/create-tab-pages/configuration-page.md)por primera vez.
* {subEntityId}: el identificador que ha proporcionado al generar un [vínculo profundo](~/concepts/build-and-test/deep-links.md) para un elemento específico _en_ esta ficha. Debe usarse para restaurar un estado específico dentro de una entidad; por ejemplo, el desplazamiento o activación de una parte específica del contenido.
* {loginHint}: un valor adecuado como sugerencia de inicio de sesión para Azure AD. Suele ser el nombre de inicio de sesión del usuario actual, en su inquilino de inicio.
* {userPrincipalName}: el nombre principal de usuario del usuario actual, en el espacio empresarial actual.
* {userObjectId}: el identificador de objeto de Azure AD del usuario actual, en el inquilino actual.
* {Theme}: tema de la interfaz de usuario actual como `default` , `dark` o `contrast` .
* {groupId}: el identificador del grupo de Office 365 en el que reside la pestaña.
* {TID}: el identificador de inquilino de Azure AD del usuario actual.
* {locale}: la configuración regional actual del usuario con formato languageId-countryId (por ejemplo, en-US).

>[!NOTE]
>El `{upn}` marcador de posición anterior ahora está en desuso. Para la compatibilidad con versiones anteriores, actualmente es un sinónimo de `{loginHint}` .

Por ejemplo, supongamos que en su manifiesto de pestaña el atributo se establece `configURL` en

`"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`

Y el usuario que ha iniciado sesión tiene los siguientes atributos:

* Su nombre de usuario es "user@example.com"
* El identificador de inquilino de su compañía es "e2653c-etc"
* Son miembros del grupo Office 365 con el identificador ' 00209384-etc '
* El usuario ha establecido el tema de Teams en ' Dark '

Al configurar la pestaña, Teams llama a esta dirección URL:

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a>Obtención de contexto mediante la biblioteca de JavaScript de Microsoft Teams

También puede recuperar la información mostrada anteriormente usando el [SDK de Microsoft Teams para cliente de JavaScript](/javascript/api/overview/msteams-client) llamando a `microsoftTeams.getContext(function(context) { /* ... */ })` .

La variable de contexto tendrá un aspecto similar al del ejemplo siguiente.

```json
{
    "teamId": "The Microsoft Teams ID in the format 19:[id]@thread.skype",
    "teamName": "The name of the current team",
    "channelId": "The channel ID in the format 19:[id]@thread.skype",
    "channelName": "The name of the current channel",
    "chatId": "The chat ID in the in the format 19:[id]@thread.skype",
    "locale": "The current locale of the user formatted as languageId-countryId (for example, en-us)",
    "entityId": "The developer-defined unique ID for the entity this content points to",
    "subEntityId": "The developer-defined unique ID for the sub-entity this content points to",
    "loginHint": "A value suitable as a login hint for Azure AD. This is usually the login name of the current user, in their home tenant",
    "userPrincipalName": "The User Principal Name of the current user, in the current tenant",
    "userObjectId": "The Azure AD object id of the current user, in the current tenant",
    "tid": "The Azure AD tenant ID of the current user",
    "groupId": "Guid identifying the current O365 Group ID",
    "theme": "The current UI theme: default | dark | contrast",
    "isFullScreen": "Indicates whether the tab is in full-screen mode",
    "userLicenseType": "Indicates the user licence type in the given SKU (for example, student or teacher)",
    "tenantSKU": "Indicates the SKU category of the tenant (for example, EDU)",
    "channelType": "microsoftTeams.ChannelType.Private | microsoftTeams.ChannelType.Regular"
}
```

## <a name="retrieving-context-in-private-channels"></a>Recuperación de contexto en canales privados

> [!Note]
> Los canales privados están actualmente en versión preliminar para desarrolladores privados.

Cuando la página de contenido se carga en un canal privado, los datos que recibe de la `getContext` llamada se ofuscarán para proteger la privacidad del canal. Los siguientes campos cambian cuando la página de contenido está en un canal privado. Si la página usa cualquiera de los valores siguientes, deberá comprobar el `channelType` campo para determinar si la página se ha cargado en un canal privado y responder de forma adecuada.

* `groupId` -Sin definir para canales privados
* `teamId` : Establecer en el threadId del canal privado
* `teamName` -Establecido en el nombre del canal privado
* `teamSiteUrl` -Establecido en la dirección URL de un sitio de SharePoint único y único para el canal privado
* `teamSitePath` -Establecido en la ruta de un sitio de SharePoint único e independiente para el canal privado
* `teamSiteDomain` -Establecido en el dominio de un dominio de sitio de SharePoint distinto y único para el canal privado

> [!Note]
>  teamSiteUrl funciona bien para los canales estándar también.

## <a name="theme-change-handling"></a>Control de cambios de temas

Puede registrar la aplicación para que se le indique si el tema cambia llamando a `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })` .

El `theme` argumento de la función será una cadena con un valor de `default` , `dark` o `contrast` .

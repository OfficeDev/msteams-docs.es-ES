---
title: Obtener contexto para su pestaña
description: Describe cómo obtener el contexto del usuario para las pestañas
localization_priority: Normal
ms.topic: how-to
keywords: contexto de usuario de las pestañas de Teams
ms.openlocfilehash: 8c91cf5a65f13d9f58f6ae8aa2678266c37338c8
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179730"
---
# <a name="get-context-for-your-tab"></a><span data-ttu-id="3056c-104">Obtención del contexto de Teams para la pestaña</span><span class="sxs-lookup"><span data-stu-id="3056c-104">Get context for your tab</span></span>

<span data-ttu-id="3056c-105">La pestaña requiere información contextual para mostrar contenido relevante:</span><span class="sxs-lookup"><span data-stu-id="3056c-105">Your tab requires contextual information to display relevant content:</span></span>

* <span data-ttu-id="3056c-106">Información básica sobre el usuario, el equipo o la compañía.</span><span class="sxs-lookup"><span data-stu-id="3056c-106">Basic information about the user, team, or company.</span></span>
* <span data-ttu-id="3056c-107">Información sobre la configuración regional y el tema.</span><span class="sxs-lookup"><span data-stu-id="3056c-107">Locale and theme information.</span></span>
* <span data-ttu-id="3056c-108">Lea el `entityId` o que identifica lo que hay en esta `subEntityId` pestaña.</span><span class="sxs-lookup"><span data-stu-id="3056c-108">Read the `entityId` or `subEntityId` that identifies what is in this tab.</span></span>

## <a name="user-context"></a><span data-ttu-id="3056c-109">Contexto del usuario</span><span class="sxs-lookup"><span data-stu-id="3056c-109">User context</span></span>

<span data-ttu-id="3056c-110">El contexto sobre el usuario, el equipo o la empresa puede ser especialmente útil cuando:</span><span class="sxs-lookup"><span data-stu-id="3056c-110">Context about the user, team, or company can be especially useful when:</span></span>

* <span data-ttu-id="3056c-111">Creas o asocias recursos en la aplicación con el usuario o equipo especificado.</span><span class="sxs-lookup"><span data-stu-id="3056c-111">You create or associate resources in your app with the specified user or team.</span></span>
* <span data-ttu-id="3056c-112">Se inicia un flujo de autenticación Azure Active Directory (AAD) u otro proveedor de identidades, y no es necesario que el usuario vuelva a escribir su nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="3056c-112">You initiate an authentication flow from Azure Active Directory (AAD) or other identity provider, and you do not require the user to enter their username again.</span></span> <span data-ttu-id="3056c-113">Para obtener más información, vea [autenticar a un usuario en la Microsoft Teams pestaña](~/concepts/authentication/authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3056c-113">For more information, see [authenticate a user in your Microsoft Teams tab](~/concepts/authentication/authentication.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3056c-114">Aunque esta información de usuario puede ayudar a proporcionar una experiencia de usuario fluida, no debe usarla como prueba de identidad.</span><span class="sxs-lookup"><span data-stu-id="3056c-114">Although this user information can help provide a smooth user experience, you must not use it as proof of identity.</span></span> <span data-ttu-id="3056c-115">Por ejemplo, un atacante puede cargar la página en un explorador y representar información o solicitudes nocivas.</span><span class="sxs-lookup"><span data-stu-id="3056c-115">For example, an attacker can load your page in a browser and render harmful information or requests.</span></span>

## <a name="access-context-information"></a><span data-ttu-id="3056c-116">Acceder a información de contexto</span><span class="sxs-lookup"><span data-stu-id="3056c-116">Access context information</span></span>

<span data-ttu-id="3056c-117">Puede acceder a la información contextual de dos formas:</span><span class="sxs-lookup"><span data-stu-id="3056c-117">You can access context information in two ways:</span></span>

* <span data-ttu-id="3056c-118">Insertar valores de marcador de posición de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="3056c-118">Insert URL placeholder values.</span></span>
* <span data-ttu-id="3056c-119">Use el [MICROSOFT TEAMS cliente de JavaScript](/javascript/api/overview/msteams-client).</span><span class="sxs-lookup"><span data-stu-id="3056c-119">Use the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client).</span></span>

### <a name="get-context-by-inserting-url-placeholder-values"></a><span data-ttu-id="3056c-120">Obtener contexto insertando valores de marcador de posición de dirección URL</span><span class="sxs-lookup"><span data-stu-id="3056c-120">Get context by inserting URL placeholder values</span></span>

<span data-ttu-id="3056c-121">Use marcadores de posición en la configuración o en las direcciones URL de contenido.</span><span class="sxs-lookup"><span data-stu-id="3056c-121">Use placeholders in your configuration or content URLs.</span></span> <span data-ttu-id="3056c-122">Microsoft Teams reemplaza los marcadores de posición por valores pertinentes al determinar la configuración o la dirección URL real del contenido.</span><span class="sxs-lookup"><span data-stu-id="3056c-122">Microsoft Teams replaces the placeholders with the relevant values when determining the actual configuration or content URL.</span></span> <span data-ttu-id="3056c-123">Los marcadores de posición disponibles incluyen todos los campos del [objeto de](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) contexto.</span><span class="sxs-lookup"><span data-stu-id="3056c-123">The available placeholders include all fields on the [context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) object.</span></span> <span data-ttu-id="3056c-124">Entre los marcadores de posición comunes se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="3056c-124">Common placeholders include the following:</span></span>

* <span data-ttu-id="3056c-125">{entityId}: el id. que proporcionó para el elemento en esta pestaña al [configurar la pestaña](~/tabs/how-to/create-tab-pages/configuration-page.md) por primera vez.</span><span class="sxs-lookup"><span data-stu-id="3056c-125">{entityId}: The ID you supplied for the item in this tab when first [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md).</span></span>
* <span data-ttu-id="3056c-126">{subEntityId}: el identificador que proporcionó al generar un [vínculo](~/concepts/build-and-test/deep-links.md) profundo para un elemento específico dentro de esta pestaña. Esto debe usarse para restaurar a un estado específico dentro de una entidad; por ejemplo, desplazarse a o activar un elemento de contenido específico.</span><span class="sxs-lookup"><span data-stu-id="3056c-126">{subEntityId}: The ID you supplied when generating a [deep link](~/concepts/build-and-test/deep-links.md) for a specific item within this tab. This must be used to restore to a specific state within an entity; for example, scrolling to or activating a specific piece of content.</span></span>
* <span data-ttu-id="3056c-127">{loginHint}: valor adecuado como sugerencia de inicio de sesión para AAD.</span><span class="sxs-lookup"><span data-stu-id="3056c-127">{loginHint}: A value suitable as a login hint for AAD.</span></span> <span data-ttu-id="3056c-128">Normalmente, este es el nombre de inicio de sesión del usuario actual en su inquilino principal.</span><span class="sxs-lookup"><span data-stu-id="3056c-128">This is usually the login name of the current user in their home tenant.</span></span>
* <span data-ttu-id="3056c-129">{userPrincipalName}: el nombre principal de usuario del usuario actual en el inquilino actual.</span><span class="sxs-lookup"><span data-stu-id="3056c-129">{userPrincipalName}: The User Principal Name of the current user in the current tenant.</span></span>
* <span data-ttu-id="3056c-130">{userObjectId}: el identificador de objeto AAD del usuario actual en el inquilino actual.</span><span class="sxs-lookup"><span data-stu-id="3056c-130">{userObjectId}: The AAD object ID of the current user in the current tenant.</span></span>
* <span data-ttu-id="3056c-131">{theme}: el tema actual de la interfaz de usuario (UI) como `default` , `dark` o `contrast` .</span><span class="sxs-lookup"><span data-stu-id="3056c-131">{theme}: The current user interface (UI) theme such as `default`, `dark`, or `contrast`.</span></span>
* <span data-ttu-id="3056c-132">{groupId}: el identificador del grupo Office 365 en el que reside la pestaña.</span><span class="sxs-lookup"><span data-stu-id="3056c-132">{groupId}: The ID of the Office 365 group in which the tab resides.</span></span>
* <span data-ttu-id="3056c-133">{tid}: el identificador de inquilino de AAD del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="3056c-133">{tid}: The AAD tenant ID of the current user.</span></span>
* <span data-ttu-id="3056c-134">{locale}: la configuración regional actual del usuario con formato de languageId-countryId.</span><span class="sxs-lookup"><span data-stu-id="3056c-134">{locale}: The current locale of the user formatted as languageId-countryId.</span></span> <span data-ttu-id="3056c-135">Por ejemplo, en-us.</span><span class="sxs-lookup"><span data-stu-id="3056c-135">For example, en-us.</span></span>

> [!NOTE]
> <span data-ttu-id="3056c-136">El marcador de posición `{upn}` anterior está en desuso.</span><span class="sxs-lookup"><span data-stu-id="3056c-136">The previous `{upn}` placeholder is now deprecated.</span></span> <span data-ttu-id="3056c-137">Para la compatibilidad con versiones anteriores, actualmente es un sinónimo de `{loginHint}`.</span><span class="sxs-lookup"><span data-stu-id="3056c-137">For backward compatibility, it is currently a synonym for `{loginHint}`.</span></span>

<span data-ttu-id="3056c-138">Por ejemplo, en el manifiesto de la pestaña se establece el atributo en , el usuario que ha iniciado sesión `configURL` `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"` tiene los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="3056c-138">For example, in your tab manifest you set the `configURL` attribute to `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`, the signed-in user has the following attributes:</span></span>

* <span data-ttu-id="3056c-139">Su nombre de usuario **es user@example.com**.</span><span class="sxs-lookup"><span data-stu-id="3056c-139">Their username is **user@example.com**.</span></span>
* <span data-ttu-id="3056c-140">Su identificador de inquilino de empresa **es e2653c-etc.**</span><span class="sxs-lookup"><span data-stu-id="3056c-140">Their company tenant ID is **e2653c-etc**.</span></span>
* <span data-ttu-id="3056c-141">Son miembros del grupo de Office 365 con el identificador **00209384-etc.**</span><span class="sxs-lookup"><span data-stu-id="3056c-141">They are a member of the Office 365 group with id **00209384-etc**.</span></span>
* <span data-ttu-id="3056c-142">El usuario ha establecido su Teams en **oscuro**.</span><span class="sxs-lookup"><span data-stu-id="3056c-142">The user has set their Teams theme to **dark**.</span></span>

<span data-ttu-id="3056c-143">Al configurar la pestaña, Teams llama a la siguiente dirección URL:</span><span class="sxs-lookup"><span data-stu-id="3056c-143">When they configure the tab, Teams calls the following URL:</span></span>

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="get-context-by-using-the-microsoft-teams-javascript-library"></a><span data-ttu-id="3056c-144">Obtener contexto mediante la biblioteca Microsoft Teams JavaScript</span><span class="sxs-lookup"><span data-stu-id="3056c-144">Get context by using the Microsoft Teams JavaScript library</span></span>

<span data-ttu-id="3056c-145">También puede recuperar la información mencionada previamente usando el [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client)llamando a `microsoftTeams.getContext(function(context) { /* ... */ })`.</span><span class="sxs-lookup"><span data-stu-id="3056c-145">You can also retrieve the information listed above using the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) by calling `microsoftTeams.getContext(function(context) { /* ... */ })`.</span></span>

<span data-ttu-id="3056c-146">El código siguiente proporciona un ejemplo de variable de contexto:</span><span class="sxs-lookup"><span data-stu-id="3056c-146">The following code provides an example of context variable:</span></span>

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

## <a name="retrieve-context-in-private-channels"></a><span data-ttu-id="3056c-147">Recuperar contexto en canales privados</span><span class="sxs-lookup"><span data-stu-id="3056c-147">Retrieve context in private channels</span></span>

> [!Note]
> <span data-ttu-id="3056c-148">Los canales privados están actualmente en la versión preliminar privada para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="3056c-148">Private channels are currently in private developer preview.</span></span>

<span data-ttu-id="3056c-149">Cuando la página de contenido se carga en un canal privado, los datos que recibe de la llamada se ocultan para proteger la `getContext` privacidad del canal.</span><span class="sxs-lookup"><span data-stu-id="3056c-149">When your content page is loaded in a private channel, the data you receive from the `getContext` call is obfuscated to protect the privacy of the channel.</span></span> <span data-ttu-id="3056c-150">Los siguientes campos se cambian cuando la página de contenido está en un canal privado:</span><span class="sxs-lookup"><span data-stu-id="3056c-150">The following fields are changed when your content page is in a private channel:</span></span>

* <span data-ttu-id="3056c-151">`groupId`: No definido para canales privados</span><span class="sxs-lookup"><span data-stu-id="3056c-151">`groupId`: Undefined for private channels</span></span>
* <span data-ttu-id="3056c-152">`teamId`: Establecer en el threadId del canal privado</span><span class="sxs-lookup"><span data-stu-id="3056c-152">`teamId`: Set to the threadId of the private channel</span></span>
* <span data-ttu-id="3056c-153">`teamName`: Se establece en el nombre del canal privado</span><span class="sxs-lookup"><span data-stu-id="3056c-153">`teamName`: Set to the name of the private channel</span></span>
* <span data-ttu-id="3056c-154">`teamSiteUrl`: Se establece en la dirección URL de un sitio de SharePoint distinto y único para el canal privado</span><span class="sxs-lookup"><span data-stu-id="3056c-154">`teamSiteUrl`: Set to the URL of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="3056c-155">`teamSitePath`: Se establece en la ruta de acceso de un sitio de SharePoint distinto y único para el canal privado</span><span class="sxs-lookup"><span data-stu-id="3056c-155">`teamSitePath`: Set to the path of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="3056c-156">`teamSiteDomain`: Se establece en el dominio de un dominio de sitio SharePoint único para el canal privado</span><span class="sxs-lookup"><span data-stu-id="3056c-156">`teamSiteDomain`: Set to the domain of a distinct, unique SharePoint site domain for the private channel</span></span>

<span data-ttu-id="3056c-157">Si la página usa cualquiera de estos valores, debe comprobar el campo para determinar si la página se carga en un canal privado y `channelType` responder correctamente.</span><span class="sxs-lookup"><span data-stu-id="3056c-157">If your page makes use of any of these values, you must check the `channelType` field to determine if your page is loaded in a private channel and respond appropriately.</span></span>

> [!Note]
> <span data-ttu-id="3056c-158">`teamSiteUrl` también funciona bien para los canales estándar.</span><span class="sxs-lookup"><span data-stu-id="3056c-158">`teamSiteUrl` also works well for standard channels.</span></span>

## <a name="handle-theme-change"></a><span data-ttu-id="3056c-159">Controlar el cambio de tema</span><span class="sxs-lookup"><span data-stu-id="3056c-159">Handle theme change</span></span>

<span data-ttu-id="3056c-160">Puedes registrar la aplicación para que se te informe si el tema cambia llamando a `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })` .</span><span class="sxs-lookup"><span data-stu-id="3056c-160">You can register your app to be informed if the theme changes by calling `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.</span></span>

<span data-ttu-id="3056c-161">El `theme` argumento de la función es una cadena con un valor de , o `default` `dark` `contrast` .</span><span class="sxs-lookup"><span data-stu-id="3056c-161">The `theme` argument in the function is a string with a value of `default`, `dark`, or `contrast`.</span></span>

## <a name="see-also"></a><span data-ttu-id="3056c-162">Vea también</span><span class="sxs-lookup"><span data-stu-id="3056c-162">See also</span></span>

* [<span data-ttu-id="3056c-163">Directrices de diseño de pestañas</span><span class="sxs-lookup"><span data-stu-id="3056c-163">Tab design guidelines</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)
* [<span data-ttu-id="3056c-164">Teams pestañas</span><span class="sxs-lookup"><span data-stu-id="3056c-164">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="3056c-165">Crear una pestaña personal</span><span class="sxs-lookup"><span data-stu-id="3056c-165">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="3056c-166">Crear una pestaña de canal o grupo</span><span class="sxs-lookup"><span data-stu-id="3056c-166">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)

## <a name="next-step"></a><span data-ttu-id="3056c-167">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="3056c-167">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3056c-168">Compilar pestañas con tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="3056c-168">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)
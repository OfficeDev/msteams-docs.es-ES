---
title: Obtener contexto para su pestaña
description: Describe cómo obtener el contexto del usuario para las pestañas
ms.topic: how-to
keywords: contexto de usuario de las pestañas de Teams
ms.openlocfilehash: 88a9c8ac5b2bca539b931147e6f6feb1483a3b6c
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696482"
---
# <a name="get-context-for-your-microsoft-teams-tab"></a><span data-ttu-id="53390-104">Obtener contexto para la pestaña Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="53390-104">Get context for your Microsoft Teams tab</span></span>

<span data-ttu-id="53390-105">Puede que su pestaña necesite información contextual para mostrar contenido relevante.</span><span class="sxs-lookup"><span data-stu-id="53390-105">Your tab might require contextual information to display relevant content.</span></span>

* <span data-ttu-id="53390-106">O bien, puede que necesite información básica sobre el usuario, el equipo o la empresa.</span><span class="sxs-lookup"><span data-stu-id="53390-106">Your tab might need basic information about the user, team, or company.</span></span>
* <span data-ttu-id="53390-107">También es posible que la pestaña necesite información local y del tema.</span><span class="sxs-lookup"><span data-stu-id="53390-107">Your tab might need locale and theme information.</span></span>
* <span data-ttu-id="53390-108">La pestaña podría necesitar leer el `entityId` o `subEntityId` que identifica lo que hay en esta pestaña.</span><span class="sxs-lookup"><span data-stu-id="53390-108">Your tab might need to read the `entityId` or `subEntityId` that identifies what is in this tab.</span></span>

## <a name="user-context"></a><span data-ttu-id="53390-109">Contexto del usuario</span><span class="sxs-lookup"><span data-stu-id="53390-109">User context</span></span>

<span data-ttu-id="53390-110">El contexto sobre el usuario, el equipo o la compañía puede ser especialmente útil cuando</span><span class="sxs-lookup"><span data-stu-id="53390-110">Context about the user, team or company can be especially useful when</span></span>

* <span data-ttu-id="53390-111">Necesita crear o asociar recursos en la aplicación con el usuario o el equipo especificados.</span><span class="sxs-lookup"><span data-stu-id="53390-111">You need to create or associate resources in your app with the specified user or team.</span></span>
* <span data-ttu-id="53390-112">Quiere iniciar un flujo de autenticación con Azure Active Directory u otro proveedor de identidades y no quiere que el usuario vuelva a introducir su nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="53390-112">You want to initiate an authentication flow against Azure Active Directory or other identity provider, and you don't want to require the user to enter their username again.</span></span> <span data-ttu-id="53390-113">(Para obtener más información sobre la autenticación en la pestaña de Microsoft Teams, consulte [Autenticar a un usuario en la pestaña de Microsoft Teams](~/concepts/authentication/authentication.md)).</span><span class="sxs-lookup"><span data-stu-id="53390-113">(For more information on authenticating within your Microsoft Teams tab, see [Authenticate a user in your Microsoft Teams tab](~/concepts/authentication/authentication.md).)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="53390-114">Aunque esta información de usuario puede ayudar a proporcionarle una experiencia de usuario fluida, *no* debe usarla como prueba de identidad.</span><span class="sxs-lookup"><span data-stu-id="53390-114">Although this user information can help provide a smooth user experience, you should *not* use it as proof of identity.</span></span> <span data-ttu-id="53390-115">Por ejemplo, un atacante podría cargar su página en un "explorador malo" y representar información o solicitudes dañinas.</span><span class="sxs-lookup"><span data-stu-id="53390-115">For example, an attacker could load your page in a "bad browser" and render harmful information or requests.</span></span>

## <a name="accessing-context"></a><span data-ttu-id="53390-116">Acceder al contexto</span><span class="sxs-lookup"><span data-stu-id="53390-116">Accessing context</span></span>

<span data-ttu-id="53390-117">Puede acceder a la información contextual de dos formas:</span><span class="sxs-lookup"><span data-stu-id="53390-117">You can access context information in two ways:</span></span>

* <span data-ttu-id="53390-118">Insertando valores de marcador de posición de la dirección URL</span><span class="sxs-lookup"><span data-stu-id="53390-118">Insert URL placeholder values</span></span>
* <span data-ttu-id="53390-119">Usando el [cliente de SDK JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client)</span><span class="sxs-lookup"><span data-stu-id="53390-119">Use the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client)</span></span>

### <a name="getting-context-by-inserting-url-placeholder-values"></a><span data-ttu-id="53390-120">Obtener contexto insertando valores de marcador de posición de la URL</span><span class="sxs-lookup"><span data-stu-id="53390-120">Getting context by inserting URL placeholder values</span></span>

<span data-ttu-id="53390-121">Use marcadores de posición en la configuración o en las direcciones URL de contenido.</span><span class="sxs-lookup"><span data-stu-id="53390-121">Use placeholders in your configuration or content URLs.</span></span> <span data-ttu-id="53390-122">Microsoft Teams reemplaza los marcadores de posición por valores pertinentes al determinar la configuración o la dirección URL real del contenido.</span><span class="sxs-lookup"><span data-stu-id="53390-122">Microsoft Teams replaces the placeholders with the relevant values when determining the actual configuration or content URL.</span></span> <span data-ttu-id="53390-123">Los marcadores de posición disponibles incluyen todos los campos del objeto del [Contexto](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="53390-123">The available placeholders include all fields on the [Context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) object.</span></span> <span data-ttu-id="53390-124">Entre los marcadores de posición comunes se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="53390-124">Common placeholders include the following:</span></span>

* <span data-ttu-id="53390-125">{entityId}: el id. que proporcionó para el elemento en esta pestaña al [configurar la pestaña](~/tabs/how-to/create-tab-pages/configuration-page.md) por primera vez.</span><span class="sxs-lookup"><span data-stu-id="53390-125">{entityId}: The ID you supplied for the item in this tab when first [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md).</span></span>
* <span data-ttu-id="53390-126">{subEntityId}: el id. que proporcionó al generar un [vínculo profundo](~/concepts/build-and-test/deep-links.md) para un elemento específico _dentro_ de esta pestaña. Debe usarse para restaurar un estado específico dentro de una entidad; por ejemplo, al desplazarse a un elemento de contenido específico o activarlo.</span><span class="sxs-lookup"><span data-stu-id="53390-126">{subEntityId}: The ID you supplied when generating a [deep link](~/concepts/build-and-test/deep-links.md) for a specific item _within_ this tab. This should be used to restore to a specific state within an entity; for example, scrolling to or activating a specific piece of content.</span></span>
* <span data-ttu-id="53390-127">{loginHint}: un valor adecuado como sugerencia de inicio de sesión de Azure AD. Suele ser el nombre de inicio de sesión del usuario actual, en su espacio empresarial principal.</span><span class="sxs-lookup"><span data-stu-id="53390-127">{loginHint}: A value suitable as a login hint for Azure AD.This is usually the login name of the current user, in their home tenant.</span></span>
* <span data-ttu-id="53390-128">{userPrincipalName}: el nombre principal de usuario del usuario actual en el espacio empresarial actual.</span><span class="sxs-lookup"><span data-stu-id="53390-128">{userPrincipalName}: The User Principal Name of the current user, in the current tenant.</span></span>
* <span data-ttu-id="53390-129">{userObjectId}: el id. del objeto de Azure AD del usuario actual en el espacio empresarial actual.</span><span class="sxs-lookup"><span data-stu-id="53390-129">{userObjectId}: The Azure AD object ID of the current user, in the current tenant.</span></span>
* <span data-ttu-id="53390-130">{theme}: el tema actual de la interfaz de usuario como `default`, `dark` o `contrast`.</span><span class="sxs-lookup"><span data-stu-id="53390-130">{theme}: The current UI theme such as `default`, `dark`, or `contrast`.</span></span>
* <span data-ttu-id="53390-131">{groupId}: el id. del grupo de Office 365 en el que se encuentra la pestaña.</span><span class="sxs-lookup"><span data-stu-id="53390-131">{groupId}: The ID of the Office 365 Group in which the tab resides.</span></span>
* <span data-ttu-id="53390-132">{tid}: el id. del espacio empresarial de Azure AD del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="53390-132">{tid}: The Azure AD tenant ID of the current user.</span></span>
* <span data-ttu-id="53390-133">{locale}: la configuración regional actual del usuario con formato de languageId-countryId (por ejemplo, en-us).</span><span class="sxs-lookup"><span data-stu-id="53390-133">{locale}: The current locale of the user formatted as languageId-countryId (for example, en-us).</span></span>

>[!NOTE]
><span data-ttu-id="53390-134">El marcador de posición `{upn}` anterior está en desuso.</span><span class="sxs-lookup"><span data-stu-id="53390-134">The previous `{upn}` placeholder is now deprecated.</span></span> <span data-ttu-id="53390-135">Para la compatibilidad con versiones anteriores, actualmente es un sinónimo de `{loginHint}`.</span><span class="sxs-lookup"><span data-stu-id="53390-135">For backward compatibility, it is currently a synonym for `{loginHint}`.</span></span>

<span data-ttu-id="53390-136">Por ejemplo, supongamos que en el manifiesto de la pestaña establece el atributo `configURL` para</span><span class="sxs-lookup"><span data-stu-id="53390-136">For example, suppose in your tab manifest you set the `configURL` attribute to</span></span>

`"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`

<span data-ttu-id="53390-137">Y el usuario que ha iniciado sesión tiene los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="53390-137">And the signed-in user has the following attributes:</span></span>

* <span data-ttu-id="53390-138">Su nombre de usuario es "user@example.com"</span><span class="sxs-lookup"><span data-stu-id="53390-138">Their username is 'user@example.com'</span></span>
* <span data-ttu-id="53390-139">Su id. de espacio empresarial es "e2653c-etc"</span><span class="sxs-lookup"><span data-stu-id="53390-139">Their company tenant ID is 'e2653c-etc'</span></span>
* <span data-ttu-id="53390-140">Es miembro del grupo de Office 365 con el id. "00209384-etc"</span><span class="sxs-lookup"><span data-stu-id="53390-140">They are a member of the Office 365 group with id '00209384-etc'</span></span>
* <span data-ttu-id="53390-141">El usuario estableció su tema de Teams en "oscuro"</span><span class="sxs-lookup"><span data-stu-id="53390-141">The user has set their Teams theme to 'dark'</span></span>

<span data-ttu-id="53390-142">Cuando configure su pestaña, Teams llama a esta dirección URL:</span><span class="sxs-lookup"><span data-stu-id="53390-142">When they configure your tab, Teams calls this URL:</span></span>

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a><span data-ttu-id="53390-143">Obtener contexto mediante el uso de la biblioteca de JavaScript de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="53390-143">Getting context by using the Microsoft Teams JavaScript library</span></span>

<span data-ttu-id="53390-144">También puede recuperar la información mencionada previamente usando el [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client)llamando a `microsoftTeams.getContext(function(context) { /* ... */ })`.</span><span class="sxs-lookup"><span data-stu-id="53390-144">You can also retrieve the information listed above using the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) by calling `microsoftTeams.getContext(function(context) { /* ... */ })`.</span></span>

<span data-ttu-id="53390-145">La variable de contexto se verá como el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="53390-145">The context variable will look like the following example.</span></span>

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
    "tenantSKU": "The license type for the current user tenant",
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

## <a name="retrieving-context-in-private-channels"></a><span data-ttu-id="53390-146">Recuperación del contexto en canales privados</span><span class="sxs-lookup"><span data-stu-id="53390-146">Retrieving context in private channels</span></span>

> [!Note]
> <span data-ttu-id="53390-147">Los canales privados están actualmente en la versión preliminar privada para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="53390-147">Private channels are currently in private developer preview.</span></span>

<span data-ttu-id="53390-148">Cuando la página de contenido se carga en un canal privado, los datos que reciba de la llamada `getContext` estarán ocultos para proteger la privacidad del canal.</span><span class="sxs-lookup"><span data-stu-id="53390-148">When your content page is loaded in a private channel, the data you receive from the `getContext` call will be obfuscated to protect the privacy of the channel.</span></span> <span data-ttu-id="53390-149">Los siguientes campos se cambian cuando la página de contenido está en un canal privado.</span><span class="sxs-lookup"><span data-stu-id="53390-149">The following fields are changed when your content page is in a private channel.</span></span> <span data-ttu-id="53390-150">Si la página utiliza cualquiera de los valores siguientes, tendrá que comprobar el campo `channelType` para determinar si la página se carga en un canal privado y responder según adecuadamente.</span><span class="sxs-lookup"><span data-stu-id="53390-150">If your page makes use of any of the values below, you'll need to check the `channelType` field to determine if your page is loaded in a private channel, and respond appropriately.</span></span>

* <span data-ttu-id="53390-151">`groupId` - No definido para canales privados</span><span class="sxs-lookup"><span data-stu-id="53390-151">`groupId` - Undefined for private channels</span></span>
* <span data-ttu-id="53390-152">`teamId` - Establecer en el threadId del canal privado</span><span class="sxs-lookup"><span data-stu-id="53390-152">`teamId` - Set to the threadId of the private channel</span></span>
* <span data-ttu-id="53390-153">`teamName` - Establecer como el nombre del canal privado</span><span class="sxs-lookup"><span data-stu-id="53390-153">`teamName` - Set to the name of the private channel</span></span>
* <span data-ttu-id="53390-154">`teamSiteUrl` - Establecer la dirección URL de un sitio de SharePoint único y distinto para el canal privado</span><span class="sxs-lookup"><span data-stu-id="53390-154">`teamSiteUrl` - Set to the URL of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="53390-155">`teamSitePath` - Establecer la ruta de acceso de un sitio de SharePoint único y distinto para el canal privado</span><span class="sxs-lookup"><span data-stu-id="53390-155">`teamSitePath` - Set to the path of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="53390-156">`teamSiteDomain` - Establecer el dominio de un dominio del sitio de SharePoint único y distinto para el canal privado</span><span class="sxs-lookup"><span data-stu-id="53390-156">`teamSiteDomain` - Set to the domain of a distinct, unique SharePoint site domain for the private channel</span></span>

> [!Note]
>  <span data-ttu-id="53390-157">teamSiteUrl también funciona bien para los canales estándar.</span><span class="sxs-lookup"><span data-stu-id="53390-157">teamSiteUrl works well for standard channels also.</span></span>

## <a name="theme-change-handling"></a><span data-ttu-id="53390-158">Manejo de los cambios de tema</span><span class="sxs-lookup"><span data-stu-id="53390-158">Theme change handling</span></span>

<span data-ttu-id="53390-159">Puede registrar la aplicación para que se le diga si el tema cambia llamando a `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.</span><span class="sxs-lookup"><span data-stu-id="53390-159">You can register your app to be told if the theme changes by calling `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.</span></span>

<span data-ttu-id="53390-160">El argumento `theme` de la función será una cadena con el valor `default`, `dark` o `contrast`.</span><span class="sxs-lookup"><span data-stu-id="53390-160">The `theme` argument in the function will be a string with a value of `default`, `dark`, or `contrast`.</span></span>

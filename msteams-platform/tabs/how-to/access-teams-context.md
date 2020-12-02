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
# <a name="get-context-for-your-microsoft-teams-tab"></a><span data-ttu-id="e5fd0-104">Obtener contexto para la pestaña de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e5fd0-104">Get context for your Microsoft Teams tab</span></span>

<span data-ttu-id="e5fd0-105">Es posible que la pestaña requiera información contextual para mostrar contenido relevante.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-105">Your tab might require contextual information to display relevant content.</span></span>

* <span data-ttu-id="e5fd0-106">Es posible que su pestaña necesite información básica sobre el usuario, el equipo o la compañía.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-106">Your tab might need basic information about the user, team, or company.</span></span>
* <span data-ttu-id="e5fd0-107">Es posible que su pestaña necesite información de temas y configuraciones regionales.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-107">Your tab might need locale and theme information.</span></span>
* <span data-ttu-id="e5fd0-108">Es posible que la pestaña necesite leer el `entityId` o `subEntityId` que identifique lo que se encuentra en esta ficha.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-108">Your tab might need to read the `entityId` or `subEntityId` that identifies what is in this tab.</span></span>

## <a name="user-context"></a><span data-ttu-id="e5fd0-109">Contexto de usuario</span><span class="sxs-lookup"><span data-stu-id="e5fd0-109">User context</span></span>

<span data-ttu-id="e5fd0-110">El contexto del usuario, el equipo o la empresa puede ser especialmente útil cuando</span><span class="sxs-lookup"><span data-stu-id="e5fd0-110">Context about the user, team or company can be especially useful when</span></span>

* <span data-ttu-id="e5fd0-111">Debe crear o asociar recursos en la aplicación con el usuario o equipo especificado.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-111">You need to create or associate resources in your app with the specified user or team.</span></span>
* <span data-ttu-id="e5fd0-112">Desea iniciar un flujo de autenticación con Azure Active Directory u otro proveedor de identidad, y no quiere pedir al usuario que vuelva a escribir su nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-112">You want to initiate an authentication flow against Azure Active Directory or other identity provider, and you don't want to require the user to enter their username again.</span></span> <span data-ttu-id="e5fd0-113">(Para obtener más información sobre la autenticación en la pestaña de Microsoft Teams, consulte [Authenticate users in your Microsoft Teams Tab](~/concepts/authentication/authentication.md)).</span><span class="sxs-lookup"><span data-stu-id="e5fd0-113">(For more information on authenticating within your Microsoft Teams tab, see [Authenticate a user in your Microsoft Teams tab](~/concepts/authentication/authentication.md).)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5fd0-114">Aunque esta información de usuario puede ayudar a proporcionar una experiencia de usuario sin problemas, *no* debería usarla como prueba de identidad.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-114">Although this user information can help provide a smooth user experience, you should *not* use it as proof of identity.</span></span> <span data-ttu-id="e5fd0-115">Por ejemplo, un atacante podría cargar la página en un "examinador de errores" y presentar información o solicitudes dañinas.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-115">For example, an attacker could load your page in a "bad browser" and render harmful information or requests.</span></span>

## <a name="accessing-context"></a><span data-ttu-id="e5fd0-116">Acceso al contexto</span><span class="sxs-lookup"><span data-stu-id="e5fd0-116">Accessing context</span></span>

<span data-ttu-id="e5fd0-117">Puede tener acceso a la información de contexto de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="e5fd0-117">You can access context information in two ways:</span></span>

* <span data-ttu-id="e5fd0-118">Insertar valores de marcador de dirección URL</span><span class="sxs-lookup"><span data-stu-id="e5fd0-118">Insert URL placeholder values</span></span>
* <span data-ttu-id="e5fd0-119">Usar el [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client)</span><span class="sxs-lookup"><span data-stu-id="e5fd0-119">Use the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client)</span></span>

### <a name="getting-context-by-inserting-url-placeholder-values"></a><span data-ttu-id="e5fd0-120">Obtener el contexto mediante la inserción de valores de marcador de posición de dirección URL</span><span class="sxs-lookup"><span data-stu-id="e5fd0-120">Getting context by inserting URL placeholder values</span></span>

<span data-ttu-id="e5fd0-121">Use marcadores de posición en las direcciones URL de configuración o de contenido.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-121">Use placeholders in your configuration or content URLs.</span></span> <span data-ttu-id="e5fd0-122">Microsoft Teams sustituye los marcadores de posición por los valores pertinentes al determinar la dirección URL de configuración o de contenido real.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-122">Microsoft Teams replaces the placeholders with the relevant values when determining the actual configuration or content URL.</span></span> <span data-ttu-id="e5fd0-123">Los marcadores de posición disponibles incluyen todos los campos en el objeto de [contexto](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) .</span><span class="sxs-lookup"><span data-stu-id="e5fd0-123">The available placeholders include all fields on the [Context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) object.</span></span> <span data-ttu-id="e5fd0-124">Los marcadores de posición comunes son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="e5fd0-124">Common placeholders include the following:</span></span>

* <span data-ttu-id="e5fd0-125">{entityId}: el identificador que ha proporcionado para el elemento en esta ficha cuando [configuró la pestaña](~/tabs/how-to/create-tab-pages/configuration-page.md)por primera vez.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-125">{entityId}: The ID you supplied for the item in this tab when first [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md).</span></span>
* <span data-ttu-id="e5fd0-126">{subEntityId}: el identificador que ha proporcionado al generar un [vínculo profundo](~/concepts/build-and-test/deep-links.md) para un elemento específico _en_ esta ficha. Debe usarse para restaurar un estado específico dentro de una entidad; por ejemplo, el desplazamiento o activación de una parte específica del contenido.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-126">{subEntityId}: The ID you supplied when generating a [deep link](~/concepts/build-and-test/deep-links.md) for a specific item _within_ this tab. This should be used to restore to a specific state within an entity; for example, scrolling to or activating a specific piece of content.</span></span>
* <span data-ttu-id="e5fd0-127">{loginHint}: un valor adecuado como sugerencia de inicio de sesión para Azure AD. Suele ser el nombre de inicio de sesión del usuario actual, en su inquilino de inicio.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-127">{loginHint}: A value suitable as a login hint for Azure AD.This is usually the login name of the current user, in their home tenant.</span></span>
* <span data-ttu-id="e5fd0-128">{userPrincipalName}: el nombre principal de usuario del usuario actual, en el espacio empresarial actual.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-128">{userPrincipalName}: The User Principal Name of the current user, in the current tenant.</span></span>
* <span data-ttu-id="e5fd0-129">{userObjectId}: el identificador de objeto de Azure AD del usuario actual, en el inquilino actual.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-129">{userObjectId}: The Azure AD object ID of the current user, in the current tenant.</span></span>
* <span data-ttu-id="e5fd0-130">{Theme}: tema de la interfaz de usuario actual como `default` , `dark` o `contrast` .</span><span class="sxs-lookup"><span data-stu-id="e5fd0-130">{theme}: The current UI theme such as `default`, `dark`, or `contrast`.</span></span>
* <span data-ttu-id="e5fd0-131">{groupId}: el identificador del grupo de Office 365 en el que reside la pestaña.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-131">{groupId}: The ID of the Office 365 Group in which the tab resides.</span></span>
* <span data-ttu-id="e5fd0-132">{TID}: el identificador de inquilino de Azure AD del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-132">{tid}: The Azure AD tenant ID of the current user.</span></span>
* <span data-ttu-id="e5fd0-133">{locale}: la configuración regional actual del usuario con formato languageId-countryId (por ejemplo, en-US).</span><span class="sxs-lookup"><span data-stu-id="e5fd0-133">{locale}: The current locale of the user formatted as languageId-countryId (for example, en-us).</span></span>

>[!NOTE]
><span data-ttu-id="e5fd0-134">El `{upn}` marcador de posición anterior ahora está en desuso.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-134">The previous `{upn}` placeholder is now deprecated.</span></span> <span data-ttu-id="e5fd0-135">Para la compatibilidad con versiones anteriores, actualmente es un sinónimo de `{loginHint}` .</span><span class="sxs-lookup"><span data-stu-id="e5fd0-135">For backward compatibility, it is currently a synonym for `{loginHint}`.</span></span>

<span data-ttu-id="e5fd0-136">Por ejemplo, supongamos que en su manifiesto de pestaña el atributo se establece `configURL` en</span><span class="sxs-lookup"><span data-stu-id="e5fd0-136">For example, suppose in your tab manifest you set the `configURL` attribute to</span></span>

`"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`

<span data-ttu-id="e5fd0-137">Y el usuario que ha iniciado sesión tiene los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="e5fd0-137">And the signed-in user has the following attributes:</span></span>

* <span data-ttu-id="e5fd0-138">Su nombre de usuario es "user@example.com"</span><span class="sxs-lookup"><span data-stu-id="e5fd0-138">Their username is 'user@example.com'</span></span>
* <span data-ttu-id="e5fd0-139">El identificador de inquilino de su compañía es "e2653c-etc"</span><span class="sxs-lookup"><span data-stu-id="e5fd0-139">Their company tenant ID is 'e2653c-etc'</span></span>
* <span data-ttu-id="e5fd0-140">Son miembros del grupo Office 365 con el identificador ' 00209384-etc '</span><span class="sxs-lookup"><span data-stu-id="e5fd0-140">They are a member of the Office 365 group with id '00209384-etc'</span></span>
* <span data-ttu-id="e5fd0-141">El usuario ha establecido el tema de Teams en ' Dark '</span><span class="sxs-lookup"><span data-stu-id="e5fd0-141">The user has set their Teams theme to 'dark'</span></span>

<span data-ttu-id="e5fd0-142">Al configurar la pestaña, Teams llama a esta dirección URL:</span><span class="sxs-lookup"><span data-stu-id="e5fd0-142">When they configure your tab, Teams calls this URL:</span></span>

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a><span data-ttu-id="e5fd0-143">Obtención de contexto mediante la biblioteca de JavaScript de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e5fd0-143">Getting context by using the Microsoft Teams JavaScript library</span></span>

<span data-ttu-id="e5fd0-144">También puede recuperar la información mostrada anteriormente usando el [SDK de Microsoft Teams para cliente de JavaScript](/javascript/api/overview/msteams-client) llamando a `microsoftTeams.getContext(function(context) { /* ... */ })` .</span><span class="sxs-lookup"><span data-stu-id="e5fd0-144">You can also retrieve the information listed above using the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) by calling `microsoftTeams.getContext(function(context) { /* ... */ })`.</span></span>

<span data-ttu-id="e5fd0-145">La variable de contexto tendrá un aspecto similar al del ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-145">The context variable will look like the following example.</span></span>

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

## <a name="retrieving-context-in-private-channels"></a><span data-ttu-id="e5fd0-146">Recuperación de contexto en canales privados</span><span class="sxs-lookup"><span data-stu-id="e5fd0-146">Retrieving context in private channels</span></span>

> [!Note]
> <span data-ttu-id="e5fd0-147">Los canales privados están actualmente en versión preliminar para desarrolladores privados.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-147">Private channels are currently in private developer preview.</span></span>

<span data-ttu-id="e5fd0-148">Cuando la página de contenido se carga en un canal privado, los datos que recibe de la `getContext` llamada se ofuscarán para proteger la privacidad del canal.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-148">When your content page is loaded in a private channel, the data you receive from the `getContext` call will be obfuscated to protect the privacy of the channel.</span></span> <span data-ttu-id="e5fd0-149">Los siguientes campos cambian cuando la página de contenido está en un canal privado.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-149">The following fields are changed when your content page is in a private channel.</span></span> <span data-ttu-id="e5fd0-150">Si la página usa cualquiera de los valores siguientes, deberá comprobar el `channelType` campo para determinar si la página se ha cargado en un canal privado y responder de forma adecuada.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-150">If your page makes use of any of the values below, you'll need to check the `channelType` field to determine if your page is loaded in a private channel, and respond appropriately.</span></span>

* <span data-ttu-id="e5fd0-151">`groupId` -Sin definir para canales privados</span><span class="sxs-lookup"><span data-stu-id="e5fd0-151">`groupId` - Undefined for private channels</span></span>
* <span data-ttu-id="e5fd0-152">`teamId` : Establecer en el threadId del canal privado</span><span class="sxs-lookup"><span data-stu-id="e5fd0-152">`teamId` - Set to the threadId of the private channel</span></span>
* <span data-ttu-id="e5fd0-153">`teamName` -Establecido en el nombre del canal privado</span><span class="sxs-lookup"><span data-stu-id="e5fd0-153">`teamName` - Set to the name of the private channel</span></span>
* <span data-ttu-id="e5fd0-154">`teamSiteUrl` -Establecido en la dirección URL de un sitio de SharePoint único y único para el canal privado</span><span class="sxs-lookup"><span data-stu-id="e5fd0-154">`teamSiteUrl` - Set to the URL of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="e5fd0-155">`teamSitePath` -Establecido en la ruta de un sitio de SharePoint único e independiente para el canal privado</span><span class="sxs-lookup"><span data-stu-id="e5fd0-155">`teamSitePath` - Set to the path of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="e5fd0-156">`teamSiteDomain` -Establecido en el dominio de un dominio de sitio de SharePoint distinto y único para el canal privado</span><span class="sxs-lookup"><span data-stu-id="e5fd0-156">`teamSiteDomain` - Set to the domain of a distinct, unique SharePoint site domain for the private channel</span></span>

> [!Note]
>  <span data-ttu-id="e5fd0-157">teamSiteUrl funciona bien para los canales estándar también.</span><span class="sxs-lookup"><span data-stu-id="e5fd0-157">teamSiteUrl works well for standard channels also.</span></span>

## <a name="theme-change-handling"></a><span data-ttu-id="e5fd0-158">Control de cambios de temas</span><span class="sxs-lookup"><span data-stu-id="e5fd0-158">Theme change handling</span></span>

<span data-ttu-id="e5fd0-159">Puede registrar la aplicación para que se le indique si el tema cambia llamando a `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })` .</span><span class="sxs-lookup"><span data-stu-id="e5fd0-159">You can register your app to be told if the theme changes by calling `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.</span></span>

<span data-ttu-id="e5fd0-160">El `theme` argumento de la función será una cadena con un valor de `default` , `dark` o `contrast` .</span><span class="sxs-lookup"><span data-stu-id="e5fd0-160">The `theme` argument in the function will be a string with a value of `default`, `dark`, or `contrast`.</span></span>

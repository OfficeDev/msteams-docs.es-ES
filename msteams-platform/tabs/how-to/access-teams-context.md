---
title: Obtener contexto para la pestaña
description: Describe cómo obtener el contexto del usuario a las pestañas.
keywords: contexto de usuario de pestañas de Microsoft Teams
ms.openlocfilehash: 8c94c4fd895896186ddda20bfaafd1d6ccdc1e73
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346801"
---
# <a name="get-context-for-your-microsoft-teams-tab"></a><span data-ttu-id="f395f-104">Obtener contexto para la pestaña de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f395f-104">Get context for your Microsoft Teams tab</span></span>

<span data-ttu-id="f395f-105">Es posible que la pestaña requiera información contextual para mostrar contenido relevante.</span><span class="sxs-lookup"><span data-stu-id="f395f-105">Your tab might require contextual information to display relevant content.</span></span>

* <span data-ttu-id="f395f-106">Es posible que su pestaña necesite información básica sobre el usuario, el equipo o la compañía.</span><span class="sxs-lookup"><span data-stu-id="f395f-106">Your tab might need basic information about the user, team, or company.</span></span>
* <span data-ttu-id="f395f-107">Es posible que su pestaña necesite información de temas y configuraciones regionales.</span><span class="sxs-lookup"><span data-stu-id="f395f-107">Your tab might need locale and theme information.</span></span>
* <span data-ttu-id="f395f-108">Es posible que la pestaña necesite leer el `entityId` o `subEntityId` que identifique lo que se encuentra en esta ficha.</span><span class="sxs-lookup"><span data-stu-id="f395f-108">Your tab might need to read the `entityId` or `subEntityId` that identifies what is in this tab.</span></span>

## <a name="user-context"></a><span data-ttu-id="f395f-109">Contexto de usuario</span><span class="sxs-lookup"><span data-stu-id="f395f-109">User context</span></span>

<span data-ttu-id="f395f-110">El contexto del usuario, el equipo o la empresa puede ser especialmente útil cuando</span><span class="sxs-lookup"><span data-stu-id="f395f-110">Context about the user, team or company can be especially useful when</span></span>

* <span data-ttu-id="f395f-111">Debe crear o asociar recursos en la aplicación con el usuario o equipo especificado.</span><span class="sxs-lookup"><span data-stu-id="f395f-111">You need to create or associate resources in your app with the specified user or team.</span></span>
* <span data-ttu-id="f395f-112">Desea iniciar un flujo de autenticación con Azure Active Directory u otro proveedor de identidad, y no quiere pedir al usuario que vuelva a escribir su nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="f395f-112">You want to initiate an authentication flow against Azure Active Directory or other identity provider, and you don't want to require the user to enter their username again.</span></span> <span data-ttu-id="f395f-113">(Para obtener más información sobre la autenticación en la pestaña de Microsoft Teams, consulte [Authenticate users in your Microsoft Teams Tab](~/concepts/authentication/authentication.md)).</span><span class="sxs-lookup"><span data-stu-id="f395f-113">(For more information on authenticating within your Microsoft Teams tab, see [Authenticate a user in your Microsoft Teams tab](~/concepts/authentication/authentication.md).)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f395f-114">Aunque esta información de usuario puede ayudar a proporcionar una experiencia de usuario sin problemas, *no* debería usarla como prueba de identidad.</span><span class="sxs-lookup"><span data-stu-id="f395f-114">Although this user information can help provide a smooth user experience, you should *not* use it as proof of identity.</span></span> <span data-ttu-id="f395f-115">Por ejemplo, un atacante puede cargar la página en un "examinador de errores" y proporcionarle la información que desee.</span><span class="sxs-lookup"><span data-stu-id="f395f-115">For example, an attacker could you load your page in a "bad browser" and provide it with any information they want.</span></span>

## <a name="accessing-context"></a><span data-ttu-id="f395f-116">Acceso al contexto</span><span class="sxs-lookup"><span data-stu-id="f395f-116">Accessing context</span></span>

<span data-ttu-id="f395f-117">Puede tener acceso a la información de contexto de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="f395f-117">You can access context information in two ways:</span></span>

* <span data-ttu-id="f395f-118">Insertar valores de marcador de dirección URL</span><span class="sxs-lookup"><span data-stu-id="f395f-118">Insert URL placeholder values</span></span>
* <span data-ttu-id="f395f-119">Usar el [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client)</span><span class="sxs-lookup"><span data-stu-id="f395f-119">Use the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client)</span></span>

### <a name="getting-context-by-inserting-url-placeholder-values"></a><span data-ttu-id="f395f-120">Obtener el contexto mediante la inserción de valores de marcador de posición de dirección URL</span><span class="sxs-lookup"><span data-stu-id="f395f-120">Getting context by inserting URL placeholder values</span></span>

<span data-ttu-id="f395f-121">Use marcadores de posición en las direcciones URL de configuración o de contenido.</span><span class="sxs-lookup"><span data-stu-id="f395f-121">Use placeholders in your configuration or content URLs.</span></span> <span data-ttu-id="f395f-122">Microsoft Teams reemplaza los marcadores de posición por los valores pertinentes al determinar la dirección URL de configuración o de contenido real a la que navegar.</span><span class="sxs-lookup"><span data-stu-id="f395f-122">Microsoft Teams replaces the placeholders with the relevant values when determining the actual configuration or content URL to navigate to.</span></span> <span data-ttu-id="f395f-123">Los marcadores de posición disponibles incluyen todos los campos en el objeto de [contexto](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) .</span><span class="sxs-lookup"><span data-stu-id="f395f-123">The available placeholders include all fields on the [Context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) object.</span></span> <span data-ttu-id="f395f-124">Los marcadores de posición comunes son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="f395f-124">Common placeholders include the following:</span></span>

* <span data-ttu-id="f395f-125">{entityId}: el identificador que ha proporcionado para el elemento en esta ficha cuando [configuró la pestaña](~/tabs/how-to/create-tab-pages/configuration-page.md)por primera vez.</span><span class="sxs-lookup"><span data-stu-id="f395f-125">{entityId}: The ID you supplied for the item in this tab when first [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md).</span></span>
* <span data-ttu-id="f395f-126">{subEntityId}: el identificador que ha proporcionado al generar un [vínculo profundo](~/concepts/build-and-test/deep-links.md) para un elemento específico _en_ esta ficha. Debe usarse para restaurar un estado específico dentro de una entidad; por ejemplo, el desplazamiento o activación de una parte específica del contenido.</span><span class="sxs-lookup"><span data-stu-id="f395f-126">{subEntityId}: The ID you supplied when generating a [deep link](~/concepts/build-and-test/deep-links.md) for a specific item _within_ this tab. This should be used to restore to a specific state within an entity; for example, scrolling to or activating a specific piece of content.</span></span>
* <span data-ttu-id="f395f-127">{loginHint}: un valor adecuado como sugerencia de inicio de sesión para Azure AD. Suele ser el nombre de inicio de sesión del usuario actual, en su inquilino de inicio.</span><span class="sxs-lookup"><span data-stu-id="f395f-127">{loginHint}: A value suitable as a login hint for Azure AD.This is usually the login name of the current user, in their home tenant.</span></span>
* <span data-ttu-id="f395f-128">{userPrincipalName}: el nombre principal de usuario del usuario actual, en el espacio empresarial actual.</span><span class="sxs-lookup"><span data-stu-id="f395f-128">{userPrincipalName}: The User Principal Name of the current user, in the current tenant.</span></span>
* <span data-ttu-id="f395f-129">{userObjectId}: el identificador de objeto de Azure AD del usuario actual, en el inquilino actual.</span><span class="sxs-lookup"><span data-stu-id="f395f-129">{userObjectId}: The Azure AD object ID of the current user, in the current tenant.</span></span>
* <span data-ttu-id="f395f-130">{Theme}: tema de la interfaz de usuario actual como `default` , `dark` o `contrast` .</span><span class="sxs-lookup"><span data-stu-id="f395f-130">{theme}: The current UI theme such as `default`, `dark`, or `contrast`.</span></span>
* <span data-ttu-id="f395f-131">{groupId}: el identificador del grupo de Office 365 en el que reside la pestaña.</span><span class="sxs-lookup"><span data-stu-id="f395f-131">{groupId}: The ID of the Office 365 Group in which the tab resides.</span></span>
* <span data-ttu-id="f395f-132">{TID}: el identificador de inquilino de Azure AD del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="f395f-132">{tid}: The Azure AD tenant ID of the current user.</span></span>
* <span data-ttu-id="f395f-133">{locale}: la configuración regional actual del usuario con formato languageId-countryId (por ejemplo, en-US).</span><span class="sxs-lookup"><span data-stu-id="f395f-133">{locale}: The current locale of the user formatted as languageId-countryId (for example, en-us).</span></span>
* <span data-ttu-id="f395f-134">{osLocaleInfo}: información de configuración regional más detallada del sistema operativo del usuario si está disponible.</span><span class="sxs-lookup"><span data-stu-id="f395f-134">{osLocaleInfo}: More detailed locale info from the user's OS if available.</span></span> <span data-ttu-id="f395f-135">Se puede usar junto con:</span><span class="sxs-lookup"><span data-stu-id="f395f-135">Can be used together with:</span></span>
    * <span data-ttu-id="f395f-136">el paquete de @microsoft/Globe NPM para garantizar que la aplicación respeta la fecha del sistema operativo del usuario y</span><span class="sxs-lookup"><span data-stu-id="f395f-136">the @microsoft/globe NPM package to ensure your app respects the user's OS date and</span></span>
    * <span data-ttu-id="f395f-137">configuración de formato de hora.</span><span class="sxs-lookup"><span data-stu-id="f395f-137">time format configuration.</span></span>
* <span data-ttu-id="f395f-138">{Idsesión}: identificador único de la sesión actual de teams que se usa en correlacionar los datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="f395f-138">{sessionId}: Unique ID for the current Teams session for use in correlating telemetry data.</span></span>
* <span data-ttu-id="f395f-139">{channelId}: identificador de Microsoft Teams para el canal al que está asociado el contenido.</span><span class="sxs-lookup"><span data-stu-id="f395f-139">{channelId}: The Microsoft Teams ID for the channel with which the content is associated.</span></span>
* <span data-ttu-id="f395f-140">{channelName}: el nombre del canal al que está asociado el contenido.</span><span class="sxs-lookup"><span data-stu-id="f395f-140">{channelName}: The name for the channel with which the content is associated.</span></span>
* <span data-ttu-id="f395f-141">{chatId}: el identificador de Microsoft Teams para el chat con el que está asociado el contenido.</span><span class="sxs-lookup"><span data-stu-id="f395f-141">{chatId}: The Microsoft Teams ID for the chat with which the content is associated.</span></span>
* <span data-ttu-id="f395f-142">{URL}: dirección URL de contenido de esta pestaña.</span><span class="sxs-lookup"><span data-stu-id="f395f-142">{url}: Content URL of this tab.</span></span>
* <span data-ttu-id="f395f-143">{websiteUrl}: dirección URL del sitio web de esta pestaña.</span><span class="sxs-lookup"><span data-stu-id="f395f-143">{websiteUrl}: Website URL of this tab.</span></span>
* <span data-ttu-id="f395f-144">{favoriteChannelsOnly}: marca que permite seleccionar solo canales favoritos.</span><span class="sxs-lookup"><span data-stu-id="f395f-144">{favoriteChannelsOnly}: Flag allowing to select favorite channels only.</span></span>
* <span data-ttu-id="f395f-145">{favoriteTeamsOnly}: marca que permite seleccionar solo equipos favoritos.</span><span class="sxs-lookup"><span data-stu-id="f395f-145">{favoriteTeamsOnly}: Flag allowing to select favorite teams only.</span></span>
* <span data-ttu-id="f395f-146">{userTeamRole}: rol del usuario actual en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f395f-146">{userTeamRole}: Role of current user in the team.</span></span>
* <span data-ttu-id="f395f-147">{teamType}: el tipo de equipo.</span><span class="sxs-lookup"><span data-stu-id="f395f-147">{teamType}: The type of the team.</span></span>
* <span data-ttu-id="f395f-148">{isTeamLocked}: el estado de bloqueo del equipo.</span><span class="sxs-lookup"><span data-stu-id="f395f-148">{isTeamLocked}: The locked status of the team.</span></span>
* <span data-ttu-id="f395f-149">{isTeamArchived}: el estado archivado del equipo.</span><span class="sxs-lookup"><span data-stu-id="f395f-149">{isTeamArchived}: The archived status of the team.</span></span>
* <span data-ttu-id="f395f-150">{isFullScreen}: indicación de si la pestaña está en modo de pantalla completa.</span><span class="sxs-lookup"><span data-stu-id="f395f-150">{isFullScreen}: Indication whether the tab is in full-screen mode.</span></span>
* <span data-ttu-id="f395f-151">{teamSiteUrl}: el sitio de SharePoint raíz asociado con el equipo.</span><span class="sxs-lookup"><span data-stu-id="f395f-151">{teamSiteUrl}: The root SharePoint site associated with the team.</span></span>
* <span data-ttu-id="f395f-152">{teamSiteDomain}: el dominio del sitio de SharePoint raíz asociado con el equipo.</span><span class="sxs-lookup"><span data-stu-id="f395f-152">{teamSiteDomain}: The domain of the root SharePoint site associated with the team.</span></span>
* <span data-ttu-id="f395f-153">{teamSitePath}: ruta de acceso relativa al sitio de SharePoint asociado con el equipo.</span><span class="sxs-lookup"><span data-stu-id="f395f-153">{teamSitePath}: The relative path to the SharePoint site associated with the team.</span></span>
* <span data-ttu-id="f395f-154">{channelRelativeUrl}: ruta de acceso relativa a la carpeta de SharePoint asociada con el canal.</span><span class="sxs-lookup"><span data-stu-id="f395f-154">{channelRelativeUrl}: The relative path to the SharePoint folder associated with the channel.</span></span>
* <span data-ttu-id="f395f-155">{tenantSKU}: el tipo de licencia para el inquilino de usuarios actual.</span><span class="sxs-lookup"><span data-stu-id="f395f-155">{tenantSKU}: The type of license for the current users tenant.</span></span>
* <span data-ttu-id="f395f-156">{ringId}: identificador de timbre actual.</span><span class="sxs-lookup"><span data-stu-id="f395f-156">{ringId}: Current ring ID.</span></span>
* <span data-ttu-id="f395f-157">{appSessionId}: identificador único de la sesión actual que se usa en correlacionar los datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="f395f-157">{appSessionId}: Unique ID for the current session for use in correlating telemetry data.</span></span>
* <span data-ttu-id="f395f-158">{completionBotId}: especifica un identificador de bot para enviar el resultado de la interacción del usuario con el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="f395f-158">{completionBotId}: Specifies a bot ID to send the result of the user's interaction with the task module.</span></span>
* <span data-ttu-id="f395f-159">{conversationId}: el identificador de la conversación.</span><span class="sxs-lookup"><span data-stu-id="f395f-159">{conversationId}: The Id of the conversation.</span></span>
* <span data-ttu-id="f395f-160">{hostClientType}: tipo de cliente de host. (Los valores posibles son: Android, iOS, Web, escritorio y Rigel).</span><span class="sxs-lookup"><span data-stu-id="f395f-160">{hostClientType}: Type of the host client.(Possible values are: android, ios, web, desktop, and rigel.)</span></span>
* <span data-ttu-id="f395f-161">{frameContext}: el contexto en el que se carga la dirección URL de la pestaña (contenido, tarea, configuración, quitar, sidePanel).</span><span class="sxs-lookup"><span data-stu-id="f395f-161">{frameContext}: The context where the tab url is loaded (content, task, setting, remove, sidePanel).</span></span>
* <span data-ttu-id="f395f-162">{SharePoint}: solo está disponible cuando se hospeda en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f395f-162">{sharepoint}: This is only available when hosted in SharePoint.</span></span>
* <span data-ttu-id="f395f-163">{meetingId}: lo usa la pestaña cuando se ejecuta en el contexto de la reunión.</span><span class="sxs-lookup"><span data-stu-id="f395f-163">{meetingId}: It is used by tab when running in meeting context.</span></span>
* <span data-ttu-id="f395f-164">{userLicenseType} El tipo de licencia para el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="f395f-164">{userLicenseType} The license type for the current user.</span></span>

>[!NOTE]
><span data-ttu-id="f395f-165">El `{upn}` marcador de posición anterior ahora está en desuso.</span><span class="sxs-lookup"><span data-stu-id="f395f-165">The previous `{upn}` placeholder is now deprecated.</span></span> <span data-ttu-id="f395f-166">Para la compatibilidad con versiones anteriores, actualmente es un sinónimo de `{loginHint}` .</span><span class="sxs-lookup"><span data-stu-id="f395f-166">For backward compatibility, it is currently a synonym for `{loginHint}`.</span></span>

<span data-ttu-id="f395f-167">Por ejemplo, supongamos que en su manifiesto de pestaña el atributo se establece `configURL` en</span><span class="sxs-lookup"><span data-stu-id="f395f-167">For example, suppose in your tab manifest you set the `configURL` attribute to</span></span>

`"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`

<span data-ttu-id="f395f-168">Y el usuario que ha iniciado sesión tiene los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="f395f-168">And the signed-in user has the following attributes:</span></span>

* <span data-ttu-id="f395f-169">Su nombre de usuario es "user@example.com"</span><span class="sxs-lookup"><span data-stu-id="f395f-169">Their username is 'user@example.com'</span></span>
* <span data-ttu-id="f395f-170">El identificador de inquilino de su compañía es "e2653c-etc"</span><span class="sxs-lookup"><span data-stu-id="f395f-170">Their company tenant ID is 'e2653c-etc'</span></span>
* <span data-ttu-id="f395f-171">Son miembros del grupo Office 365 con el identificador ' 00209384-etc '</span><span class="sxs-lookup"><span data-stu-id="f395f-171">They are a member of the Office 365 group with id '00209384-etc'</span></span>
* <span data-ttu-id="f395f-172">El usuario ha establecido el tema de Teams en ' Dark '</span><span class="sxs-lookup"><span data-stu-id="f395f-172">The user has set their Teams theme to 'dark'</span></span>

<span data-ttu-id="f395f-173">Al configurar la pestaña, Teams llama a esta dirección URL:</span><span class="sxs-lookup"><span data-stu-id="f395f-173">When they configure your tab, Teams calls this URL:</span></span>

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a><span data-ttu-id="f395f-174">Obtención de contexto mediante la biblioteca de JavaScript de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f395f-174">Getting context by using the Microsoft Teams JavaScript library</span></span>

<span data-ttu-id="f395f-175">También puede recuperar la información mostrada anteriormente usando el [SDK de Microsoft Teams para cliente de JavaScript](/javascript/api/overview/msteams-client) llamando a `microsoftTeams.getContext(function(context) { /* ... */ })` .</span><span class="sxs-lookup"><span data-stu-id="f395f-175">You can also retrieve the information listed above using the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) by calling `microsoftTeams.getContext(function(context) { /* ... */ })`.</span></span>

<span data-ttu-id="f395f-176">La variable de contexto tendrá un aspecto similar al del ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="f395f-176">The context variable will look like the following example.</span></span>

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

## <a name="retrieving-context-in-private-channels"></a><span data-ttu-id="f395f-177">Recuperación de contexto en canales privados</span><span class="sxs-lookup"><span data-stu-id="f395f-177">Retrieving context in private channels</span></span>

> [!Note]
> <span data-ttu-id="f395f-178">Los canales privados están actualmente en versión preliminar para desarrolladores privados.</span><span class="sxs-lookup"><span data-stu-id="f395f-178">Private channels are currently in private developer preview.</span></span>

<span data-ttu-id="f395f-179">Cuando la página de contenido se carga en un canal privado, los datos que recibe de la `getContext` llamada se ofuscarán para proteger la privacidad del canal.</span><span class="sxs-lookup"><span data-stu-id="f395f-179">When your content page is loaded in a private channel, the data you receive from the `getContext` call will be obfuscated to protect the privacy of the channel.</span></span> <span data-ttu-id="f395f-180">Los siguientes campos cambian cuando la página de contenido está en un canal privado.</span><span class="sxs-lookup"><span data-stu-id="f395f-180">The following fields are changed when your content page is in a private channel.</span></span> <span data-ttu-id="f395f-181">Si la página usa cualquiera de los valores siguientes, deberá comprobar el `channelType` campo para determinar si la página se ha cargado en un canal privado y responder de forma adecuada.</span><span class="sxs-lookup"><span data-stu-id="f395f-181">If your page makes use of any of the values below, you'll need to check the `channelType` field to determine if your page is loaded in a private channel, and respond appropriately.</span></span>

* <span data-ttu-id="f395f-182">`groupId` -Sin definir para canales privados</span><span class="sxs-lookup"><span data-stu-id="f395f-182">`groupId` - Undefined for private channels</span></span>
* <span data-ttu-id="f395f-183">`teamId` : Establecer en el threadId del canal privado</span><span class="sxs-lookup"><span data-stu-id="f395f-183">`teamId` - Set to the threadId of the private channel</span></span>
* <span data-ttu-id="f395f-184">`teamName` -Establecido en el nombre del canal privado</span><span class="sxs-lookup"><span data-stu-id="f395f-184">`teamName` - Set to the name of the private channel</span></span>
* <span data-ttu-id="f395f-185">`teamSiteUrl` -Establecido en la dirección URL de un sitio de SharePoint único y único para el canal privado</span><span class="sxs-lookup"><span data-stu-id="f395f-185">`teamSiteUrl` - Set to the URL of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="f395f-186">`teamSitePath` -Establecido en la ruta de un sitio de SharePoint único e independiente para el canal privado</span><span class="sxs-lookup"><span data-stu-id="f395f-186">`teamSitePath` - Set to the path of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="f395f-187">`teamSiteDomain` -Establecido en el dominio de un dominio de sitio de SharePoint distinto y único para el canal privado</span><span class="sxs-lookup"><span data-stu-id="f395f-187">`teamSiteDomain` - Set to the domain of a distinct, unique SharePoint site domain for the private channel</span></span>

## <a name="theme-change-handling"></a><span data-ttu-id="f395f-188">Control de cambios de temas</span><span class="sxs-lookup"><span data-stu-id="f395f-188">Theme change handling</span></span>

<span data-ttu-id="f395f-189">Puede registrar la aplicación para que se le indique si el tema cambia llamando a `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })` .</span><span class="sxs-lookup"><span data-stu-id="f395f-189">You can register your app to be told if the theme changes by calling `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.</span></span>

<span data-ttu-id="f395f-190">El `theme` argumento de la función será una cadena con un valor de `default` , `dark` o `contrast` .</span><span class="sxs-lookup"><span data-stu-id="f395f-190">The `theme` argument in the function will be a string with a value of `default`, `dark`, or `contrast`.</span></span>

---
title: Creación de una página de configuración
author: laujan
description: cómo crear una página de configuración
keywords: equipos pestañas canal de grupo configurable
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: aeab1cf96d1e875db79d9143fefd0e46348f585a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566687"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="85ac6-104">Creación de una página de configuración</span><span class="sxs-lookup"><span data-stu-id="85ac6-104">Create a configuration page</span></span>

<span data-ttu-id="85ac6-105">Una página de configuración es un tipo especial de página de [contenido.](content-page.md)</span><span class="sxs-lookup"><span data-stu-id="85ac6-105">A configuration page is a special type of [content page](content-page.md).</span></span> <span data-ttu-id="85ac6-106">Los usuarios configuran algunos aspectos de la aplicación Microsoft Teams mediante la página de configuración y usan esa configuración como parte de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="85ac6-106">The users configure some aspects of the Microsoft Teams app using the configuration page and use that configuration as part of the following:</span></span>

* <span data-ttu-id="85ac6-107">Una pestaña de chat de canal o grupo: recopile información de los usuarios y establezca la `contentUrl` página de contenido que se va a mostrar.</span><span class="sxs-lookup"><span data-stu-id="85ac6-107">A channel or group chat tab: Collect information from the users and set the `contentUrl` of the content page to display.</span></span>
* <span data-ttu-id="85ac6-108">Una [extensión de mensajería](~/messaging-extensions/what-are-messaging-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="85ac6-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md).</span></span>
* <span data-ttu-id="85ac6-109">Un [conector de Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="85ac6-109">An [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

## <a name="configuring-a-channel-or-group-chat-tab"></a><span data-ttu-id="85ac6-110">Configuración de un canal o pestaña de chat de grupo</span><span class="sxs-lookup"><span data-stu-id="85ac6-110">Configuring a channel or group chat tab</span></span>

<span data-ttu-id="85ac6-111">La aplicación debe hacer referencia al [SDK de cliente de JavaScript Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) y llamar a `microsoft.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="85ac6-111">The application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="85ac6-112">Además, las direcciones URL utilizadas deben estar protegidas y estar disponibles en la nube.</span><span class="sxs-lookup"><span data-stu-id="85ac6-112">Also, the URLs used must be secured HTTPS endpoints and available from the cloud.</span></span> 

### <a name="example"></a><span data-ttu-id="85ac6-113">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="85ac6-113">Example</span></span>

<span data-ttu-id="85ac6-114">Un ejemplo de una página de configuración se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="85ac6-114">An example of a configuration page is shown in the following image:</span></span> 

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

<span data-ttu-id="85ac6-115">El código correspondiente para la página de configuración se muestra en la siguiente sección:</span><span class="sxs-lookup"><span data-stu-id="85ac6-115">The corresponding code for configuration page is shown in the following section:</span></span>

```html
<head>
<script src='https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js'></script>
</head>
    <body>
        <button onclick="(document.getElementById('icon').src = '/images/iconGray.png'); colorClickGray()">Select Gray</button>
        <img id="icon" src="/images/teamsIcon.png" alt="icon" style="width:100px" />
        <button onclick="(document.getElementById('icon').src = '/images/iconRed.png'); colorClickRed()">Select Red</button>

        <script>
            microsoftTeams.initialize();
            let saveGray = () => {
                microsoftTeams.settings.registerOnSaveHandler((saveEvent) => {
                    microsoftTeams.settings.setSettings({
                        websiteUrl: "https://yourWebsite.com",
                        contentUrl: "https://yourWebsite.com/gray",
                        entityId: "grayIconTab",
                        suggestedDisplayName: "MyNewTab"
                    });
                    saveEvent.notifySuccess();
                });
            }
            let saveRed = () => {
                microsoftTeams.settings.registerOnSaveHandler((saveEvent) => {
                    microsoftTeams.settings.setSettings({
                        websiteUrl: "https://yourWebsite.com",
                        contentUrl: "https://yourWebsite.com/red",
                        entityId: "redIconTab",
                        suggestedDisplayName: "MyNewTab"
                    });
                    saveEvent.notifySuccess();
                });
            }

            let gr = document.getElementById("gray").style;
            let rd = document.getElementById("red").style;

            const colorClickGray = () => {
                gr.display = "block";
                rd.display = "none";
                microsoftTeams.settings.setValidityState(true);
                saveGray()
            }

            const colorClickRed = () => {
                rd.display = "block";
                gr.display = "none";
                microsoftTeams.settings.setValidityState(true);
                saveRed();
            }
        </script>
    </body>
...
```

<span data-ttu-id="85ac6-116">Elija **el** botón Seleccionar gris o **Seleccionar rojo** en la página de configuración para mostrar el contenido de la pestaña con un icono gris o rojo.</span><span class="sxs-lookup"><span data-stu-id="85ac6-116">Choose either **Select Gray** or **Select Red** button in the configuration page, to display the tab content with a gray or red icon.</span></span> 

<span data-ttu-id="85ac6-117">La siguiente imagen muestra el contenido de la pestaña con el icono gris:</span><span class="sxs-lookup"><span data-stu-id="85ac6-117">The following image displays the tab content with gray icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

<span data-ttu-id="85ac6-118">La siguiente imagen muestra el contenido de la pestaña con el icono rojo:</span><span class="sxs-lookup"><span data-stu-id="85ac6-118">The following image displays the tab content with red icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

<span data-ttu-id="85ac6-119">La elección del botón relativo desencadena `saveGray()` uno o varios e invoca lo `saveRed()` siguiente:</span><span class="sxs-lookup"><span data-stu-id="85ac6-119">Choosing the relative button triggers either `saveGray()` or `saveRed()`, and invokes the following:</span></span>

1. <span data-ttu-id="85ac6-120">El `settings.setValidityState(true)` está establecido en true.</span><span class="sxs-lookup"><span data-stu-id="85ac6-120">The `settings.setValidityState(true)` is set to true.</span></span>
1. <span data-ttu-id="85ac6-121">`microsoftTeams.settings.registerOnSaveHandler()`Se desencadena el controlador de eventos.</span><span class="sxs-lookup"><span data-stu-id="85ac6-121">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
1. <span data-ttu-id="85ac6-122">El botón **Guardar** de la página de configuración de la aplicación, cargado en Teams, está habilitado.</span><span class="sxs-lookup"><span data-stu-id="85ac6-122">The **Save** button on the app's configuration page, uploaded in Teams, is enabled.</span></span>

<span data-ttu-id="85ac6-123">El código de página de configuración informa a la Teams que se cumplen los requisitos de configuración y la instalación puede continuar.</span><span class="sxs-lookup"><span data-stu-id="85ac6-123">The configuration page code informs the Teams that the configuration requirements are satisfied and the installation can proceed.</span></span> <span data-ttu-id="85ac6-124">Cuando el usuario selecciona **Guardar,** se establecen los parámetros de `settings.setSettings()` la interfaz, tal como se `Settings` define.</span><span class="sxs-lookup"><span data-stu-id="85ac6-124">When the user selects **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface.</span></span> <span data-ttu-id="85ac6-125">Para obtener más información, consulte [Configuración interfaz](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="85ac6-125">For more information, see [Settings interface](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="85ac6-126">En el último paso, `saveEvent.notifySuccess()` se llama para indicar que la dirección URL del contenido se ha resuelto correctamente.</span><span class="sxs-lookup"><span data-stu-id="85ac6-126">In the last step, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="85ac6-127">Si registra un controlador de guardado mediante `microsoftTeams.settings.registerOnSaveHandler()` , la devolución de llamada debe invocar o indicar el resultado de la `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` configuración.</span><span class="sxs-lookup"><span data-stu-id="85ac6-127">If you register a save handler using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="85ac6-128">Si no registra un controlador de guardado, la `saveEvent.notifySuccess()` llamada se realiza automáticamente cuando el usuario selecciona **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="85ac6-128">If you don't register a save handler, the `saveEvent.notifySuccess()` call is made automatically when the user selects **Save**.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="85ac6-129">Obtenga datos de contexto para la configuración de la pestaña</span><span class="sxs-lookup"><span data-stu-id="85ac6-129">Get context data for your tab settings</span></span>

<span data-ttu-id="85ac6-130">Puede que su pestaña necesite información contextual para mostrar contenido relevante.</span><span class="sxs-lookup"><span data-stu-id="85ac6-130">Your tab might require contextual information to display relevant content.</span></span> <span data-ttu-id="85ac6-131">La información contextual mejora aún más el atractivo de su pestaña al proporcionar una experiencia de usuario más personalizada.</span><span class="sxs-lookup"><span data-stu-id="85ac6-131">Contextual information further enhances your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="85ac6-132">Para obtener más información sobre las propiedades utilizadas para la configuración de pestañas, consulte [Interfaz de contexto](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="85ac6-132">For more information on the properties used for tab configuration, see [Context interface](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="85ac6-133">Recopile los valores de las variables de datos de contexto de las dos maneras siguientes:</span><span class="sxs-lookup"><span data-stu-id="85ac6-133">Collect the values of context data variables in the following two ways:</span></span>

1. <span data-ttu-id="85ac6-134">Inserte marcadores de posición de cadena de consulta de DIRECCIÓN URL en el `configurationURL` manifiesto.</span><span class="sxs-lookup"><span data-stu-id="85ac6-134">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

1. <span data-ttu-id="85ac6-135">Utilice el método [SDK de Teams.](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})`</span><span class="sxs-lookup"><span data-stu-id="85ac6-135">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="85ac6-136">Insertar marcadores de posición en el `configurationUrl`</span><span class="sxs-lookup"><span data-stu-id="85ac6-136">Insert placeholders in the `configurationUrl`</span></span>

<span data-ttu-id="85ac6-137">Agregue marcadores de posición de interfaz de contexto a la `configurationUrl` base.</span><span class="sxs-lookup"><span data-stu-id="85ac6-137">Add context interface placeholders to your base `configurationUrl`.</span></span> <span data-ttu-id="85ac6-138">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="85ac6-138">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="85ac6-139">Base URL</span><span class="sxs-lookup"><span data-stu-id="85ac6-139">Base URL</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="85ac6-140">URL base con cadenas de consulta</span><span class="sxs-lookup"><span data-stu-id="85ac6-140">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="85ac6-141">Después de cargar la página, el Teams actualiza los marcadores de posición de cadena de consulta con valores relevantes.</span><span class="sxs-lookup"><span data-stu-id="85ac6-141">After your page uploads, the Teams updates the query string placeholders with relevant values.</span></span> <span data-ttu-id="85ac6-142">Incluya lógica en la página de configuración para recuperar y usar esos valores.</span><span class="sxs-lookup"><span data-stu-id="85ac6-142">Include logic in the configuration page to retrieve and use those values.</span></span> <span data-ttu-id="85ac6-143">Para obtener más información sobre cómo trabajar con cadenas de consulta de DIRECCIÓN URL, vea [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) en MDN Web Docs. En el ejemplo siguiente se describe la forma de extraer un valor de la `configurationUrl` propiedad:</span><span class="sxs-lookup"><span data-stu-id="85ac6-143">For more information on working with URL query strings, see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. The following example describes the way to extract a value from the `configurationUrl` property:</span></span>

```html
<script>
   microsoftTeams.initialize();
   const getId = () => {
        let urlParams = new URLSearchParams(document.location.search.substring(1));
        let blueTeamId = urlParams.get('team');
        return blueTeamId
    }
//For testing, you can invoke the following to view the pertinent value:
document.write(getId());
</script>
```

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="85ac6-144">Utilice la `getContext()` función para recuperar el contexto</span><span class="sxs-lookup"><span data-stu-id="85ac6-144">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="85ac6-145">La `microsoftTeams.getContext((context) => {})` función recupera la interfaz [Context](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) cuando se invoca.</span><span class="sxs-lookup"><span data-stu-id="85ac6-145">The `microsoftTeams.getContext((context) => {})` function retrieves the [Context interface](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) when invoked.</span></span> <span data-ttu-id="85ac6-146">Agregue esta función a la página de configuración para recuperar valores de contexto:</span><span class="sxs-lookup"><span data-stu-id="85ac6-146">Add this function to the configuration page to retrieve context values:</span></span>

```html
<!-- `userPrincipalName` will render in the span with the id "user". -->

<span id="user"></span>
...
<script>
    microsoftTeams.getContext((context) =>{
        let userId = document.getElementById('user');
        userId.innerHTML = context.userPrincipalName;
    });
</script>
...
```

## <a name="context-and-authentication"></a><span data-ttu-id="85ac6-147">Contexto y autenticación</span><span class="sxs-lookup"><span data-stu-id="85ac6-147">Context and authentication</span></span>

 <span data-ttu-id="85ac6-148">Autentique antes de permitir que un usuario configure la aplicación.</span><span class="sxs-lookup"><span data-stu-id="85ac6-148">Authenticate before allowing a user to configure your app.</span></span> <span data-ttu-id="85ac6-149">De lo contrario, el contenido podría incluir orígenes que tienen sus protocolos de autenticación.</span><span class="sxs-lookup"><span data-stu-id="85ac6-149">Otherwise, your content might include sources that have their authentication protocols.</span></span> <span data-ttu-id="85ac6-150">Para obtener más información, consulte [Autenticar a un usuario en una pestaña Microsoft Teams](~/tabs/how-to/authentication/auth-flow-tab.md). Use información de contexto para construir las solicitudes de autenticación y las direcciones URL de página de autorización.</span><span class="sxs-lookup"><span data-stu-id="85ac6-150">For more information, see [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md). Use context information to construct the authentication requests and authorization page URLs.</span></span>
<span data-ttu-id="85ac6-151">Asegúrese de que todos los dominios utilizados en las páginas de pestañas se enumeran en la `manifest.json` matriz y `validDomains` la matriz.</span><span class="sxs-lookup"><span data-stu-id="85ac6-151">Ensure that all domains used in your tab pages are listed in the `manifest.json` and `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="85ac6-152">Modificar o eliminar una pestaña</span><span class="sxs-lookup"><span data-stu-id="85ac6-152">Modify or remove a tab</span></span>

<span data-ttu-id="85ac6-153">Las opciones de eliminación compatibles refinan aún más la experiencia del usuario.</span><span class="sxs-lookup"><span data-stu-id="85ac6-153">Supported removal options further refine the user experience.</span></span> <span data-ttu-id="85ac6-154">Establezca la propiedad del manifiesto `canUpdateConfiguration` en , que permite a los usuarios `true` modificar, reconfigurar o cambiar el nombre de un grupo o canal pestaña. Además, indique lo que sucede con el contenido cuando se quita una pestaña, incluyendo una página de opciones de eliminación en la aplicación y estableciendo un valor para la `removeUrl` propiedad en la  `setSettings()` configuración.</span><span class="sxs-lookup"><span data-stu-id="85ac6-154">Set your manifest's `canUpdateConfiguration` property to `true`, that enables the users to modify, reconfigure, or rename a group or channel tab. Also, indicate what happens to the content when a tab is removed, by including a removal options page in the app and setting a value for the `removeUrl` property in the  `setSettings()` configuration.</span></span> <span data-ttu-id="85ac6-155">El usuario puede desinstalar las pestañas Personal, pero no puede modificarlas.</span><span class="sxs-lookup"><span data-stu-id="85ac6-155">The user can uninstall the Personal tabs but cannot modify them.</span></span> <span data-ttu-id="85ac6-156">Para obtener más información, consulte [Crear una página de eliminación para la pestaña](~/tabs/how-to/create-tab-pages/removal-page.md).</span><span class="sxs-lookup"><span data-stu-id="85ac6-156">For more information, see [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

<span data-ttu-id="85ac6-157">Microsoft Teams configuración setSettings() para la página de eliminación:</span><span class="sxs-lookup"><span data-stu-id="85ac6-157">Microsoft Teams setSettings() configuration for removal page:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a><span data-ttu-id="85ac6-158">Clientes móviles</span><span class="sxs-lookup"><span data-stu-id="85ac6-158">Mobile clients</span></span>

<span data-ttu-id="85ac6-159">Si decide que la pestaña de canal o grupo aparezca en la Teams clientes móviles, la `setSettings()` configuración debe tener un valor para la `websiteUrl` propiedad.</span><span class="sxs-lookup"><span data-stu-id="85ac6-159">If you choose to have your channel or group tab appear on the Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span> <span data-ttu-id="85ac6-160">Para obtener más información, consulte [instrucciones para pestañas en dispositivos móviles.](~/tabs/design/tabs-mobile.md)</span><span class="sxs-lookup"><span data-stu-id="85ac6-160">For more information, see [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span></span>

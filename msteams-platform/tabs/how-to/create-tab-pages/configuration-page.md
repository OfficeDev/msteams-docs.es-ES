---
title: Creación de una página de configuración
author: surbhigupta
description: cómo crear una página de configuración
keywords: Canal de grupo de pestañas de teams configurable
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 6f79480fb3ec6eb50de622e0b67b70e021d8cce7
ms.sourcegitcommit: a6253e89cb8c8c34d45b06e08c9668daeebc30a3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2021
ms.locfileid: "53300315"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="fb3f1-104">Creación de una página de configuración</span><span class="sxs-lookup"><span data-stu-id="fb3f1-104">Create a configuration page</span></span>

<span data-ttu-id="fb3f1-105">Una página de configuración es un tipo especial de [página de contenido](content-page.md).</span><span class="sxs-lookup"><span data-stu-id="fb3f1-105">A configuration page is a special type of [content page](content-page.md).</span></span> <span data-ttu-id="fb3f1-106">Los usuarios configuran algunos aspectos de la aplicación Microsoft Teams con la página de configuración y la usan como parte de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fb3f1-106">The users configure some aspects of the Microsoft Teams app using the configuration page and use that configuration as part of the following:</span></span>

* <span data-ttu-id="fb3f1-107">Una pestaña de chat de canal o grupo: recopilar información de los usuarios y establecer la `contentUrl` página de contenido que se va a mostrar.</span><span class="sxs-lookup"><span data-stu-id="fb3f1-107">A channel or group chat tab: Collect information from the users and set the `contentUrl` of the content page to be displayed.</span></span>
* <span data-ttu-id="fb3f1-108">Una [extensión de mensajería](~/messaging-extensions/what-are-messaging-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="fb3f1-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md).</span></span>
* <span data-ttu-id="fb3f1-109">Un [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="fb3f1-109">An [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

## <a name="configure-a-channel-or-group-chat-tab"></a><span data-ttu-id="fb3f1-110">Configurar una pestaña de chat de canal o grupo</span><span class="sxs-lookup"><span data-stu-id="fb3f1-110">Configure a channel or group chat tab</span></span>

<span data-ttu-id="fb3f1-111">La aplicación debe hacer referencia al [sdk Microsoft Teams cliente de JavaScript y](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) llamar a `microsoft.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="fb3f1-111">The application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="fb3f1-112">Las direcciones URL usadas deben estar protegidas con puntos de conexión HTTPS y disponibles desde la nube.</span><span class="sxs-lookup"><span data-stu-id="fb3f1-112">The URLs used must be secured HTTPS endpoints and available from the cloud.</span></span>

### <a name="example"></a><span data-ttu-id="fb3f1-113">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="fb3f1-113">Example</span></span>

<span data-ttu-id="fb3f1-114">En la siguiente imagen se muestra un ejemplo de una página de configuración:</span><span class="sxs-lookup"><span data-stu-id="fb3f1-114">An example of a configuration page is shown in the following image:</span></span>

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

<span data-ttu-id="fb3f1-115">El siguiente código es un ejemplo de código correspondiente para la página de configuración:</span><span class="sxs-lookup"><span data-stu-id="fb3f1-115">The following code is an example of corresponding code for the configuration page:</span></span>

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
    ...
</body>
```

<span data-ttu-id="fb3f1-116">Elija seleccionar **el botón Gris** o **Seleccionar** rojo en la página de configuración para mostrar el contenido de la pestaña con un icono gris o rojo.</span><span class="sxs-lookup"><span data-stu-id="fb3f1-116">Choose either **Select Gray** or **Select Red** button in the configuration page, to display the tab content with a gray or red icon.</span></span>

<span data-ttu-id="fb3f1-117">La siguiente imagen muestra el contenido de la pestaña con un icono gris:</span><span class="sxs-lookup"><span data-stu-id="fb3f1-117">The following image displays the tab content with a gray icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

<span data-ttu-id="fb3f1-118">La siguiente imagen muestra el contenido de la pestaña con un icono rojo:</span><span class="sxs-lookup"><span data-stu-id="fb3f1-118">The following image displays the tab content with a red icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

<span data-ttu-id="fb3f1-119">Elegir el botón adecuado desencadena `saveGray()` o , e invoca lo `saveRed()` siguiente:</span><span class="sxs-lookup"><span data-stu-id="fb3f1-119">Choosing the appropriate button triggers either `saveGray()` or `saveRed()`, and invokes the following:</span></span>

* <span data-ttu-id="fb3f1-120">Se `settings.setValidityState(true)` establece en true.</span><span class="sxs-lookup"><span data-stu-id="fb3f1-120">Set `settings.setValidityState(true)` to true.</span></span> 
* <span data-ttu-id="fb3f1-121">Se `microsoftTeams.settings.registerOnSaveHandler()` desencadena el controlador de eventos.</span><span class="sxs-lookup"><span data-stu-id="fb3f1-121">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
* <span data-ttu-id="fb3f1-122">**Guardar** en la página de configuración de la aplicación está habilitado.</span><span class="sxs-lookup"><span data-stu-id="fb3f1-122">**Save** on the app's configuration page, is enabled.</span></span>

<span data-ttu-id="fb3f1-123">El código de página de configuración informa Teams que los requisitos de configuración se cumplen y la instalación puede continuar.</span><span class="sxs-lookup"><span data-stu-id="fb3f1-123">The configuration page code informs Teams that the configuration requirements are satisfied and the installation can proceed.</span></span> <span data-ttu-id="fb3f1-124">Cuando el usuario selecciona **Guardar**, los parámetros de `settings.setSettings()` se establecen, según lo define la `Settings` interfaz.</span><span class="sxs-lookup"><span data-stu-id="fb3f1-124">When the user selects **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface.</span></span> <span data-ttu-id="fb3f1-125">Para obtener más información, vea [la interfaz de configuración](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="fb3f1-125">For more information, see [settings interface](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="fb3f1-126">`saveEvent.notifySuccess()` se llama para indicar que la dirección URL de contenido se ha resuelto correctamente.</span><span class="sxs-lookup"><span data-stu-id="fb3f1-126">`saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="fb3f1-127">Si registra un controlador de guardado mediante , la devolución de llamada debe invocar o indicar `microsoftTeams.settings.registerOnSaveHandler()` el resultado de la `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` configuración.</span><span class="sxs-lookup"><span data-stu-id="fb3f1-127">If you register a save handler using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="fb3f1-128">Si no registra un controlador de guardado, la llamada se realiza `saveEvent.notifySuccess()` automáticamente cuando el usuario selecciona **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fb3f1-128">If you do not register a save handler, the `saveEvent.notifySuccess()` call is made automatically when the user selects **Save**.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="fb3f1-129">Obtener datos de contexto para la configuración de la pestaña</span><span class="sxs-lookup"><span data-stu-id="fb3f1-129">Get context data for your tab settings</span></span>

<span data-ttu-id="fb3f1-130">La pestaña requiere información contextual para mostrar contenido relevante.</span><span class="sxs-lookup"><span data-stu-id="fb3f1-130">Your tab requires contextual information to display relevant content.</span></span> <span data-ttu-id="fb3f1-131">La información contextual mejora aún más el atractivo de la pestaña al proporcionar una experiencia de usuario más personalizada.</span><span class="sxs-lookup"><span data-stu-id="fb3f1-131">Contextual information further enhances your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="fb3f1-132">Para obtener más información sobre las propiedades usadas para la configuración de pestañas, vea [context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="fb3f1-132">For more information on the properties used for tab configuration, see [context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="fb3f1-133">Recopile los valores de las variables de datos de contexto de las dos maneras siguientes:</span><span class="sxs-lookup"><span data-stu-id="fb3f1-133">Collect the values of context data variables in the following two ways:</span></span>

* <span data-ttu-id="fb3f1-134">Inserte marcadores de posición de cadena de consulta url en el `configurationURL` manifiesto .</span><span class="sxs-lookup"><span data-stu-id="fb3f1-134">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

* <span data-ttu-id="fb3f1-135">Use el [Teams SDK.](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})`</span><span class="sxs-lookup"><span data-stu-id="fb3f1-135">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="fb3f1-136">Insertar marcadores de posición en el `configurationUrl`</span><span class="sxs-lookup"><span data-stu-id="fb3f1-136">Insert placeholders in the `configurationUrl`</span></span>

<span data-ttu-id="fb3f1-137">Agregue marcadores de posición de interfaz de contexto a la base `configurationUrl` .</span><span class="sxs-lookup"><span data-stu-id="fb3f1-137">Add context interface placeholders to your base `configurationUrl`.</span></span> <span data-ttu-id="fb3f1-138">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fb3f1-138">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="fb3f1-139">Base URL</span><span class="sxs-lookup"><span data-stu-id="fb3f1-139">Base URL</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="fb3f1-140">Dirección URL base con cadenas de consulta</span><span class="sxs-lookup"><span data-stu-id="fb3f1-140">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="fb3f1-141">Después de cargar la página, Teams los marcadores de posición de cadena de consulta con valores relevantes.</span><span class="sxs-lookup"><span data-stu-id="fb3f1-141">After your page uploads, Teams updates the query string placeholders with relevant values.</span></span> <span data-ttu-id="fb3f1-142">Incluya lógica en la página de configuración para recuperar y usar esos valores.</span><span class="sxs-lookup"><span data-stu-id="fb3f1-142">Include logic in the configuration page to retrieve and use those values.</span></span> <span data-ttu-id="fb3f1-143">Para obtener más información sobre cómo trabajar con cadenas de consulta de dirección URL, vea [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. En el siguiente ejemplo de código se proporciona la forma de extraer un valor de la `configurationUrl` propiedad:</span><span class="sxs-lookup"><span data-stu-id="fb3f1-143">For more information on working with URL query strings, see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. The following code example provides the way to extract a value from the `configurationUrl` property:</span></span>

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="fb3f1-144">Usar la `getContext()` función para recuperar contexto</span><span class="sxs-lookup"><span data-stu-id="fb3f1-144">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="fb3f1-145">La `microsoftTeams.getContext((context) => {})` función recupera la interfaz de [contexto](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) cuando se invoca.</span><span class="sxs-lookup"><span data-stu-id="fb3f1-145">The `microsoftTeams.getContext((context) => {})` function retrieves the [context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) when invoked.</span></span>

<span data-ttu-id="fb3f1-146">El código siguiente proporciona un ejemplo de cómo agregar esta función a la página de configuración para recuperar valores de contexto:</span><span class="sxs-lookup"><span data-stu-id="fb3f1-146">The following code provides an example of adding this function to the configuration page to retrieve context values:</span></span>

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

## <a name="context-and-authentication"></a><span data-ttu-id="fb3f1-147">Contexto y autenticación</span><span class="sxs-lookup"><span data-stu-id="fb3f1-147">Context and authentication</span></span>

<span data-ttu-id="fb3f1-148">Autentica antes de permitir que un usuario configure la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fb3f1-148">Authenticate before allowing a user to configure your app.</span></span> <span data-ttu-id="fb3f1-149">De lo contrario, el contenido podría incluir orígenes que tienen sus protocolos de autenticación.</span><span class="sxs-lookup"><span data-stu-id="fb3f1-149">Otherwise, your content might include sources that have their authentication protocols.</span></span> <span data-ttu-id="fb3f1-150">Para obtener más información, vea [autenticar un usuario en una Microsoft Teams pestaña](~/tabs/how-to/authentication/auth-flow-tab.md). Use información de contexto para crear las direcciones URL de la página de autorización y las solicitudes de autenticación.</span><span class="sxs-lookup"><span data-stu-id="fb3f1-150">For more information, see [authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md). Use context information to construct the authentication requests and authorization page URLs.</span></span> <span data-ttu-id="fb3f1-151">Asegúrese de que todos los dominios usados en las páginas de pestañas se enumeran en la `manifest.json` matriz `validDomains` and.</span><span class="sxs-lookup"><span data-stu-id="fb3f1-151">Ensure that all domains used in your tab pages are listed in the `manifest.json` and `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="fb3f1-152">Modificar o quitar una pestaña</span><span class="sxs-lookup"><span data-stu-id="fb3f1-152">Modify or remove a tab</span></span>

<span data-ttu-id="fb3f1-153">Establezca la propiedad del manifiesto en , que permite a los usuarios `canUpdateConfiguration` modificar, reconfigurar o cambiar el nombre `true` de una pestaña de canal o grupo. Además, indica lo que sucede con el contenido cuando se quita una pestaña, incluyendo una página de opciones de eliminación en la aplicación y estableciendo un valor para la propiedad `removeUrl` en la  `setSettings()` configuración.</span><span class="sxs-lookup"><span data-stu-id="fb3f1-153">Set your manifest's `canUpdateConfiguration` property to `true`, that enables the users to modify, reconfigure, or rename a channel or group tab. Also, indicate what happens to the content when a tab is removed, by including a removal options page in the app and setting a value for the `removeUrl` property in the  `setSettings()` configuration.</span></span> <span data-ttu-id="fb3f1-154">El usuario puede desinstalar pestañas personales, pero no puede modificarlas.</span><span class="sxs-lookup"><span data-stu-id="fb3f1-154">The user can uninstall personal tabs but cannot modify them.</span></span> <span data-ttu-id="fb3f1-155">Para obtener más información, [vea crear una página de eliminación para la pestaña](~/tabs/how-to/create-tab-pages/removal-page.md).</span><span class="sxs-lookup"><span data-stu-id="fb3f1-155">For more information, see [create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

<span data-ttu-id="fb3f1-156">`setSettings()`Microsoft Teams configuración para la página de eliminación:</span><span class="sxs-lookup"><span data-stu-id="fb3f1-156">Microsoft Teams `setSettings()` configuration for removal page:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a><span data-ttu-id="fb3f1-157">Clientes móviles</span><span class="sxs-lookup"><span data-stu-id="fb3f1-157">Mobile clients</span></span>

<span data-ttu-id="fb3f1-158">Si decide que la pestaña canal o grupo aparezca en el Teams móviles, la configuración `setSettings()` debe tener un valor para `websiteUrl` .</span><span class="sxs-lookup"><span data-stu-id="fb3f1-158">If you choose to have your channel or group tab appear on the Teams mobile clients, the `setSettings()` configuration must have a value for `websiteUrl`.</span></span> <span data-ttu-id="fb3f1-159">Para obtener más información, consulte [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span><span class="sxs-lookup"><span data-stu-id="fb3f1-159">For more information, see [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="fb3f1-160">Vea también</span><span class="sxs-lookup"><span data-stu-id="fb3f1-160">See also</span></span>

* [<span data-ttu-id="fb3f1-161">Teams pestañas</span><span class="sxs-lookup"><span data-stu-id="fb3f1-161">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="fb3f1-162">Crear una pestaña personal</span><span class="sxs-lookup"><span data-stu-id="fb3f1-162">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="fb3f1-163">Crear una pestaña de canal o grupo</span><span class="sxs-lookup"><span data-stu-id="fb3f1-163">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="fb3f1-164">Creación de una página de contenido</span><span class="sxs-lookup"><span data-stu-id="fb3f1-164">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
* [<span data-ttu-id="fb3f1-165">Pestañas en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="fb3f1-165">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)

## <a name="next-step"></a><span data-ttu-id="fb3f1-166">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="fb3f1-166">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fb3f1-167">Crear una página de eliminación para la pestaña</span><span class="sxs-lookup"><span data-stu-id="fb3f1-167">Create a removal page for your tab</span></span>](~/tabs/how-to/create-tab-pages/removal-page.md)

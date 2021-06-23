---
title: Creación de una página de configuración
author: surbhigupta
description: cómo crear una página de configuración
keywords: Canal de grupo de pestañas de teams configurable
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 041ef78fcc6e3f5203842e808949e86e8dd3aae4
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069213"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="fc87a-104">Creación de una página de configuración</span><span class="sxs-lookup"><span data-stu-id="fc87a-104">Create a configuration page</span></span>

<span data-ttu-id="fc87a-105">Una página de configuración es un tipo especial de [página de contenido](content-page.md).</span><span class="sxs-lookup"><span data-stu-id="fc87a-105">A configuration page is a special type of [content page](content-page.md).</span></span> <span data-ttu-id="fc87a-106">Los usuarios configuran algunos aspectos de la aplicación Microsoft Teams con la página de configuración y la usan como parte de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fc87a-106">The users configure some aspects of the Microsoft Teams app using the configuration page and use that configuration as part of the following:</span></span>

* <span data-ttu-id="fc87a-107">Una pestaña de chat de canal o grupo: recopilar información de los usuarios y establecer la `contentUrl` página de contenido que se mostrará.</span><span class="sxs-lookup"><span data-stu-id="fc87a-107">A channel or group chat tab: Collect information from the users and set the `contentUrl` of the content page to display.</span></span>
* <span data-ttu-id="fc87a-108">Una [extensión de mensajería](~/messaging-extensions/what-are-messaging-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="fc87a-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md).</span></span>
* <span data-ttu-id="fc87a-109">Un [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="fc87a-109">An [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

## <a name="configuring-a-channel-or-group-chat-tab"></a><span data-ttu-id="fc87a-110">Configuración de una pestaña de chat de grupo o canal</span><span class="sxs-lookup"><span data-stu-id="fc87a-110">Configuring a channel or group chat tab</span></span>

<span data-ttu-id="fc87a-111">La aplicación debe hacer referencia al [sdk Microsoft Teams cliente de JavaScript y](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) llamar a `microsoft.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="fc87a-111">The application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="fc87a-112">Además, las direcciones URL usadas deben estar protegidas con puntos de conexión HTTPS y disponibles desde la nube.</span><span class="sxs-lookup"><span data-stu-id="fc87a-112">Also, the URLs used must be secured HTTPS endpoints and available from the cloud.</span></span> 

### <a name="example"></a><span data-ttu-id="fc87a-113">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="fc87a-113">Example</span></span>

<span data-ttu-id="fc87a-114">En la siguiente imagen se muestra un ejemplo de una página de configuración:</span><span class="sxs-lookup"><span data-stu-id="fc87a-114">An example of a configuration page is shown in the following image:</span></span> 

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

<span data-ttu-id="fc87a-115">El código correspondiente para la página de configuración se muestra en la siguiente sección:</span><span class="sxs-lookup"><span data-stu-id="fc87a-115">The corresponding code for configuration page is shown in the following section:</span></span>

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

<span data-ttu-id="fc87a-116">Elija seleccionar **el botón Gris** o **Seleccionar** rojo en la página de configuración para mostrar el contenido de la pestaña con un icono gris o rojo.</span><span class="sxs-lookup"><span data-stu-id="fc87a-116">Choose either **Select Gray** or **Select Red** button in the configuration page, to display the tab content with a gray or red icon.</span></span> 

<span data-ttu-id="fc87a-117">La siguiente imagen muestra el contenido de la pestaña con el icono gris:</span><span class="sxs-lookup"><span data-stu-id="fc87a-117">The following image displays the tab content with gray icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

<span data-ttu-id="fc87a-118">La siguiente imagen muestra el contenido de la pestaña con el icono rojo:</span><span class="sxs-lookup"><span data-stu-id="fc87a-118">The following image displays the tab content with red icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

<span data-ttu-id="fc87a-119">Elegir el botón relativo desencadena `saveGray()` o , e invoca lo `saveRed()` siguiente:</span><span class="sxs-lookup"><span data-stu-id="fc87a-119">Choosing the relative button triggers either `saveGray()` or `saveRed()`, and invokes the following:</span></span>

1. <span data-ttu-id="fc87a-120">Se `settings.setValidityState(true)` establece en true.</span><span class="sxs-lookup"><span data-stu-id="fc87a-120">The `settings.setValidityState(true)` is set to true.</span></span>
1. <span data-ttu-id="fc87a-121">Se `microsoftTeams.settings.registerOnSaveHandler()` desencadena el controlador de eventos.</span><span class="sxs-lookup"><span data-stu-id="fc87a-121">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
1. <span data-ttu-id="fc87a-122">El **botón** Guardar de la página de configuración de la aplicación, cargado en Teams, está habilitado.</span><span class="sxs-lookup"><span data-stu-id="fc87a-122">The **Save** button on the app's configuration page, uploaded in Teams, is enabled.</span></span>

<span data-ttu-id="fc87a-123">El código de página de configuración informa a Teams que los requisitos de configuración se cumplen y la instalación puede continuar.</span><span class="sxs-lookup"><span data-stu-id="fc87a-123">The configuration page code informs the Teams that the configuration requirements are satisfied and the installation can proceed.</span></span> <span data-ttu-id="fc87a-124">Cuando el usuario selecciona **Guardar**, los parámetros de `settings.setSettings()` se establecen, según lo define la `Settings` interfaz.</span><span class="sxs-lookup"><span data-stu-id="fc87a-124">When the user selects **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface.</span></span> <span data-ttu-id="fc87a-125">Para obtener más información, [vea Configuración interfaz](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="fc87a-125">For more information, see [Settings interface](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="fc87a-126">En el último paso, se llama para indicar que la dirección URL de `saveEvent.notifySuccess()` contenido se ha resuelto correctamente.</span><span class="sxs-lookup"><span data-stu-id="fc87a-126">In the last step, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="fc87a-127">Si registra un controlador de guardado mediante , la devolución de llamada debe invocar o indicar `microsoftTeams.settings.registerOnSaveHandler()` el resultado de la `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` configuración.</span><span class="sxs-lookup"><span data-stu-id="fc87a-127">If you register a save handler using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="fc87a-128">Si no registra un controlador de guardado, la llamada se realiza `saveEvent.notifySuccess()` automáticamente cuando el usuario selecciona **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fc87a-128">If you don't register a save handler, the `saveEvent.notifySuccess()` call is made automatically when the user selects **Save**.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="fc87a-129">Obtener datos de contexto para la configuración de la pestaña</span><span class="sxs-lookup"><span data-stu-id="fc87a-129">Get context data for your tab settings</span></span>

<span data-ttu-id="fc87a-130">Puede que su pestaña necesite información contextual para mostrar contenido relevante.</span><span class="sxs-lookup"><span data-stu-id="fc87a-130">Your tab might require contextual information to display relevant content.</span></span> <span data-ttu-id="fc87a-131">La información contextual mejora aún más el atractivo de la pestaña al proporcionar una experiencia de usuario más personalizada.</span><span class="sxs-lookup"><span data-stu-id="fc87a-131">Contextual information further enhances your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="fc87a-132">Para obtener más información sobre las propiedades usadas para la configuración de pestañas, vea [Context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="fc87a-132">For more information on the properties used for tab configuration, see [Context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="fc87a-133">Recopile los valores de las variables de datos de contexto de las dos maneras siguientes:</span><span class="sxs-lookup"><span data-stu-id="fc87a-133">Collect the values of context data variables in the following two ways:</span></span>

1. <span data-ttu-id="fc87a-134">Inserte marcadores de posición de cadena de consulta url en el `configurationURL` manifiesto .</span><span class="sxs-lookup"><span data-stu-id="fc87a-134">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

1. <span data-ttu-id="fc87a-135">Use el [Teams SDK.](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})`</span><span class="sxs-lookup"><span data-stu-id="fc87a-135">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="fc87a-136">Insertar marcadores de posición en el `configurationUrl`</span><span class="sxs-lookup"><span data-stu-id="fc87a-136">Insert placeholders in the `configurationUrl`</span></span>

<span data-ttu-id="fc87a-137">Agregue marcadores de posición de interfaz de contexto a la base `configurationUrl` .</span><span class="sxs-lookup"><span data-stu-id="fc87a-137">Add context interface placeholders to your base `configurationUrl`.</span></span> <span data-ttu-id="fc87a-138">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fc87a-138">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="fc87a-139">Base URL</span><span class="sxs-lookup"><span data-stu-id="fc87a-139">Base URL</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="fc87a-140">Dirección URL base con cadenas de consulta</span><span class="sxs-lookup"><span data-stu-id="fc87a-140">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="fc87a-141">Después de cargar la página, el Teams actualiza los marcadores de posición de cadena de consulta con valores relevantes.</span><span class="sxs-lookup"><span data-stu-id="fc87a-141">After your page uploads, the Teams updates the query string placeholders with relevant values.</span></span> <span data-ttu-id="fc87a-142">Incluya lógica en la página de configuración para recuperar y usar esos valores.</span><span class="sxs-lookup"><span data-stu-id="fc87a-142">Include logic in the configuration page to retrieve and use those values.</span></span> <span data-ttu-id="fc87a-143">Para obtener más información sobre cómo trabajar con cadenas de consulta de dirección URL, vea [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. En el siguiente ejemplo se describe la forma de extraer un valor de la `configurationUrl` propiedad:</span><span class="sxs-lookup"><span data-stu-id="fc87a-143">For more information on working with URL query strings, see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. The following example describes the way to extract a value from the `configurationUrl` property:</span></span>

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="fc87a-144">Usar la `getContext()` función para recuperar contexto</span><span class="sxs-lookup"><span data-stu-id="fc87a-144">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="fc87a-145">La `microsoftTeams.getContext((context) => {})` función recupera la interfaz context [cuando](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) se invoca.</span><span class="sxs-lookup"><span data-stu-id="fc87a-145">The `microsoftTeams.getContext((context) => {})` function retrieves the [Context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) when invoked.</span></span> <span data-ttu-id="fc87a-146">Agregue esta función a la página de configuración para recuperar valores de contexto:</span><span class="sxs-lookup"><span data-stu-id="fc87a-146">Add this function to the configuration page to retrieve context values:</span></span>

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

## <a name="context-and-authentication"></a><span data-ttu-id="fc87a-147">Contexto y autenticación</span><span class="sxs-lookup"><span data-stu-id="fc87a-147">Context and authentication</span></span>

 <span data-ttu-id="fc87a-148">Autentica antes de permitir que un usuario configure la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fc87a-148">Authenticate before allowing a user to configure your app.</span></span> <span data-ttu-id="fc87a-149">De lo contrario, el contenido podría incluir orígenes que tienen sus protocolos de autenticación.</span><span class="sxs-lookup"><span data-stu-id="fc87a-149">Otherwise, your content might include sources that have their authentication protocols.</span></span> <span data-ttu-id="fc87a-150">Para obtener más información, vea [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md). Use información de contexto para crear las direcciones URL de la página de autorización y las solicitudes de autenticación.</span><span class="sxs-lookup"><span data-stu-id="fc87a-150">For more information, see [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md). Use context information to construct the authentication requests and authorization page URLs.</span></span>
<span data-ttu-id="fc87a-151">Asegúrese de que todos los dominios usados en las páginas de pestañas se enumeran en la `manifest.json` matriz `validDomains` and.</span><span class="sxs-lookup"><span data-stu-id="fc87a-151">Ensure that all domains used in your tab pages are listed in the `manifest.json` and `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="fc87a-152">Modificar o quitar una pestaña</span><span class="sxs-lookup"><span data-stu-id="fc87a-152">Modify or remove a tab</span></span>

<span data-ttu-id="fc87a-153">Las opciones de eliminación admitidas refinan aún más la experiencia del usuario.</span><span class="sxs-lookup"><span data-stu-id="fc87a-153">Supported removal options further refine the user experience.</span></span> <span data-ttu-id="fc87a-154">Establezca la propiedad del manifiesto en , que permite a los usuarios `canUpdateConfiguration` modificar, reconfigurar o cambiar el nombre de una pestaña de grupo `true` o canal. Además, indica lo que sucede con el contenido cuando se quita una pestaña, incluyendo una página de opciones de eliminación en la aplicación y estableciendo un valor para la propiedad `removeUrl` en la  `setSettings()` configuración.</span><span class="sxs-lookup"><span data-stu-id="fc87a-154">Set your manifest's `canUpdateConfiguration` property to `true`, that enables the users to modify, reconfigure, or rename a group or channel tab. Also, indicate what happens to the content when a tab is removed, by including a removal options page in the app and setting a value for the `removeUrl` property in the  `setSettings()` configuration.</span></span> <span data-ttu-id="fc87a-155">El usuario puede desinstalar las pestañas Personales, pero no puede modificarlas.</span><span class="sxs-lookup"><span data-stu-id="fc87a-155">The user can uninstall the Personal tabs but cannot modify them.</span></span> <span data-ttu-id="fc87a-156">Para obtener más información, vea [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span><span class="sxs-lookup"><span data-stu-id="fc87a-156">For more information, see [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

<span data-ttu-id="fc87a-157">Microsoft Teams setSettings() para la página de eliminación:</span><span class="sxs-lookup"><span data-stu-id="fc87a-157">Microsoft Teams setSettings() configuration for removal page:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a><span data-ttu-id="fc87a-158">Clientes móviles</span><span class="sxs-lookup"><span data-stu-id="fc87a-158">Mobile clients</span></span>

<span data-ttu-id="fc87a-159">Si decide que la pestaña canal o grupo aparezca en el Teams móviles, la configuración `setSettings()` debe tener un valor para `websiteUrl` .</span><span class="sxs-lookup"><span data-stu-id="fc87a-159">If you choose to have your channel or group tab appear on the Teams mobile clients, the `setSettings()` configuration must have a value for `websiteUrl`.</span></span> <span data-ttu-id="fc87a-160">Para obtener más información, consulte [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span><span class="sxs-lookup"><span data-stu-id="fc87a-160">For more information, see [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span></span>

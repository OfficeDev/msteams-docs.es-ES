---
title: Creación de una página de configuración
author: laujan
description: cómo crear una página de configuración
keywords: Canal de grupo de pestañas de teams configurable
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: b6da8437b6988f863288d77aedc1acb786c12d4b
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034687"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="582f0-104">Creación de una página de configuración</span><span class="sxs-lookup"><span data-stu-id="582f0-104">Create a configuration page</span></span>

<span data-ttu-id="582f0-105">Una página de configuración es un tipo especial de [página de contenido](content-page.md).</span><span class="sxs-lookup"><span data-stu-id="582f0-105">A configuration page is a special type of [content page](content-page.md).</span></span> <span data-ttu-id="582f0-106">Los usuarios configuran algunos aspectos de la aplicación de Microsoft Teams con la página de configuración y usan esa configuración como parte de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="582f0-106">The users configure some aspects of the Microsoft Teams app using the configuration page and use that configuration as part of the following:</span></span>

* <span data-ttu-id="582f0-107">Una pestaña de chat de canal o grupo: recopila información de los usuarios y establece la `contentUrl` página de contenido que se mostrará.</span><span class="sxs-lookup"><span data-stu-id="582f0-107">A channel or group chat tab - Collect information from the users and set the `contentUrl` of the content page to display.</span></span>
* <span data-ttu-id="582f0-108">Una [extensión de mensajería](~/messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="582f0-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md)</span></span>
* <span data-ttu-id="582f0-109">Un [conector de Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span><span class="sxs-lookup"><span data-stu-id="582f0-109">An [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span></span>

## <a name="configuring-a-channel-or-group-chat-tab"></a><span data-ttu-id="582f0-110">Configuración de una pestaña de chat de grupo o canal</span><span class="sxs-lookup"><span data-stu-id="582f0-110">Configuring a channel or group chat tab</span></span>

<span data-ttu-id="582f0-111">La aplicación debe hacer referencia al [SDK de cliente javaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) de Microsoft Teams y llamar a `microsoft.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="582f0-111">The application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="582f0-112">Además, las direcciones URL usadas deben estar protegidas con puntos de conexión HTTPS y disponibles desde la nube.</span><span class="sxs-lookup"><span data-stu-id="582f0-112">Also, the URLs used must be secured HTTPS endpoints and available from the cloud.</span></span> <span data-ttu-id="582f0-113">El siguiente código es un ejemplo de una página de configuración:</span><span class="sxs-lookup"><span data-stu-id="582f0-113">The following code is an example of a configuration page:</span></span>

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

<span data-ttu-id="582f0-114">Elija seleccionar **el botón Gris** o **Seleccionar** rojo en la página de configuración para mostrar el contenido de la pestaña con un icono gris o rojo.</span><span class="sxs-lookup"><span data-stu-id="582f0-114">Choose either **Select Gray** or **Select Red** button in the configuration page, to display the tab content with a gray or red icon.</span></span> <span data-ttu-id="582f0-115">Elegir el botón relativo se desavoca `saveGray()` o , e invoca lo `saveRed()` siguiente:</span><span class="sxs-lookup"><span data-stu-id="582f0-115">Choosing the relative button fires either `saveGray()` or `saveRed()`, and invokes the following:</span></span>

1. <span data-ttu-id="582f0-116">Se `settings.setValidityState(true)` establece en true.</span><span class="sxs-lookup"><span data-stu-id="582f0-116">The `settings.setValidityState(true)` is set to true.</span></span>
1. <span data-ttu-id="582f0-117">Se `microsoftTeams.settings.registerOnSaveHandler()` desencadena el controlador de eventos.</span><span class="sxs-lookup"><span data-stu-id="582f0-117">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
1. <span data-ttu-id="582f0-118">El **botón** Guardar de la página de configuración de la aplicación, cargado en Teams, está habilitado.</span><span class="sxs-lookup"><span data-stu-id="582f0-118">The **Save** button on the app's configuration page, uploaded in Teams, is enabled.</span></span>

<span data-ttu-id="582f0-119">El código de página de configuración informa a Teams de que los requisitos de configuración se cumplen y la instalación puede continuar.</span><span class="sxs-lookup"><span data-stu-id="582f0-119">The configuration page code informs the Teams that the configuration requirements are satisfied and the installation can proceed.</span></span> <span data-ttu-id="582f0-120">Cuando el usuario selecciona **Guardar**, los parámetros de `settings.setSettings()` se establecen, según lo define la `Settings` interfaz.</span><span class="sxs-lookup"><span data-stu-id="582f0-120">When the user selects **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface.</span></span> <span data-ttu-id="582f0-121">Para obtener más información, vea [Settings interface](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="582f0-121">For more information, see [Settings interface](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="582f0-122">En el último paso, se llama para indicar que la dirección URL de `saveEvent.notifySuccess()` contenido se ha resuelto correctamente.</span><span class="sxs-lookup"><span data-stu-id="582f0-122">In the last step, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="582f0-123">Si registra un controlador de guardado mediante , la devolución de llamada debe invocar o indicar `microsoftTeams.settings.registerOnSaveHandler()` el resultado de la `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` configuración.</span><span class="sxs-lookup"><span data-stu-id="582f0-123">If you register a save handler using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="582f0-124">Si no registra un controlador de guardado, la llamada se realiza `saveEvent.notifySuccess()` automáticamente cuando el usuario selecciona **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="582f0-124">If you don't register a save handler, the `saveEvent.notifySuccess()` call is made automatically when the user selects **Save**.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="582f0-125">Obtener datos de contexto para la configuración de la pestaña</span><span class="sxs-lookup"><span data-stu-id="582f0-125">Get context data for your tab settings</span></span>

<span data-ttu-id="582f0-126">La pestaña puede requerir información contextual para mostrar contenido relevante.</span><span class="sxs-lookup"><span data-stu-id="582f0-126">Your tab might require contextual information to display relevant content.</span></span> <span data-ttu-id="582f0-127">La información contextual mejora aún más el atractivo de la pestaña al proporcionar una experiencia de usuario más personalizada.</span><span class="sxs-lookup"><span data-stu-id="582f0-127">Contextual information further enhances your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="582f0-128">Para obtener más información sobre las propiedades usadas para la configuración de pestañas, vea [Context interface](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="582f0-128">For more information on the properties used for tab configuration, see [Context interface](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="582f0-129">Recopile los valores de las variables de datos de contexto de las dos maneras siguientes:</span><span class="sxs-lookup"><span data-stu-id="582f0-129">Collect the values of context data variables in the following two ways:</span></span>

1. <span data-ttu-id="582f0-130">Inserte marcadores de posición de cadena de consulta url en el `configurationURL` manifiesto .</span><span class="sxs-lookup"><span data-stu-id="582f0-130">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

1. <span data-ttu-id="582f0-131">Use el [método SDK de Teams.](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})`</span><span class="sxs-lookup"><span data-stu-id="582f0-131">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="582f0-132">Insertar marcadores de posición en el `configurationUrl`</span><span class="sxs-lookup"><span data-stu-id="582f0-132">Insert placeholders in the `configurationUrl`</span></span>

<span data-ttu-id="582f0-133">Agregue marcadores de posición de interfaz de contexto a la base `configurationUrl` .</span><span class="sxs-lookup"><span data-stu-id="582f0-133">Add context interface placeholders to your base `configurationUrl`.</span></span> <span data-ttu-id="582f0-134">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="582f0-134">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="582f0-135">Base URL</span><span class="sxs-lookup"><span data-stu-id="582f0-135">Base URL</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="582f0-136">Dirección URL base con cadenas de consulta</span><span class="sxs-lookup"><span data-stu-id="582f0-136">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="582f0-137">Después de cargar la página, Teams actualiza los marcadores de posición de cadena de consulta con valores relevantes.</span><span class="sxs-lookup"><span data-stu-id="582f0-137">After your page uploads, the Teams updates the query string placeholders with relevant values.</span></span> <span data-ttu-id="582f0-138">Incluya lógica en la página de configuración para recuperar y usar esos valores.</span><span class="sxs-lookup"><span data-stu-id="582f0-138">Include logic in the configuration page to retrieve and use those values.</span></span> <span data-ttu-id="582f0-139">Para obtener más información sobre cómo trabajar con cadenas de consulta de dirección URL, vea [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. En el siguiente ejemplo se describe la forma de extraer un valor de la `configurationUrl` propiedad:</span><span class="sxs-lookup"><span data-stu-id="582f0-139">For more information on working with URL query strings, see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. The following example describes the way to extract a value from the `configurationUrl` property:</span></span>

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="582f0-140">Usar la `getContext()` función para recuperar contexto</span><span class="sxs-lookup"><span data-stu-id="582f0-140">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="582f0-141">La `microsoftTeams.getContext((context) => {})` función recupera la interfaz context [cuando](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) se invoca.</span><span class="sxs-lookup"><span data-stu-id="582f0-141">The `microsoftTeams.getContext((context) => {})` function retrieves the [Context interface](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) when invoked.</span></span> <span data-ttu-id="582f0-142">Agregue esta función a la página de configuración para recuperar valores de contexto:</span><span class="sxs-lookup"><span data-stu-id="582f0-142">Add this function to the configuration page to retrieve context values:</span></span>

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

## <a name="context-and-authentication"></a><span data-ttu-id="582f0-143">Contexto y autenticación</span><span class="sxs-lookup"><span data-stu-id="582f0-143">Context and authentication</span></span>

 <span data-ttu-id="582f0-144">Autentica antes de permitir que un usuario configure la aplicación.</span><span class="sxs-lookup"><span data-stu-id="582f0-144">Authenticate before allowing a user to configure your app.</span></span> <span data-ttu-id="582f0-145">De lo contrario, el contenido podría incluir orígenes que tienen sus protocolos de autenticación.</span><span class="sxs-lookup"><span data-stu-id="582f0-145">Otherwise, your content might include sources that have their authentication protocols.</span></span> <span data-ttu-id="582f0-146">Para obtener más información, vea [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md). Use información de contexto para crear las direcciones URL de la página de autorización y las solicitudes de autenticación.</span><span class="sxs-lookup"><span data-stu-id="582f0-146">For more information, see [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md). Use context information to construct the authentication requests and authorization page URLs.</span></span>
<span data-ttu-id="582f0-147">Asegúrese de que todos los dominios usados en las páginas de pestañas se enumeran en la `manifest.json` matriz `validDomains` and.</span><span class="sxs-lookup"><span data-stu-id="582f0-147">Ensure that all domains used in your tab pages are listed in the `manifest.json` and `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="582f0-148">Modificar o quitar una pestaña</span><span class="sxs-lookup"><span data-stu-id="582f0-148">Modify or remove a tab</span></span>

<span data-ttu-id="582f0-149">Las opciones de eliminación admitidas refinan aún más la experiencia del usuario.</span><span class="sxs-lookup"><span data-stu-id="582f0-149">Supported removal options further refine the user experience.</span></span> <span data-ttu-id="582f0-150">Establezca la propiedad del manifiesto en , que permite a los usuarios `canUpdateConfiguration` modificar, reconfigurar o cambiar el nombre de una pestaña de grupo `true` o canal. Además, indica lo que sucede con el contenido cuando se quita una pestaña, incluyendo una página de opciones de eliminación en la aplicación y estableciendo un valor para la propiedad `removeUrl` en la  `setSettings()` configuración.</span><span class="sxs-lookup"><span data-stu-id="582f0-150">Set your manifest's `canUpdateConfiguration` property to `true`, that enables the users to modify, reconfigure, or rename a group or channel tab. Also, indicate what happens to the content when a tab is removed, by including a removal options page in the app and setting a value for the `removeUrl` property in the  `setSettings()` configuration.</span></span> <span data-ttu-id="582f0-151">El usuario puede desinstalar las pestañas Personales, pero no puede modificarlas.</span><span class="sxs-lookup"><span data-stu-id="582f0-151">The user can uninstall the Personal tabs but cannot modify them.</span></span> <span data-ttu-id="582f0-152">Para obtener más información, vea [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span><span class="sxs-lookup"><span data-stu-id="582f0-152">For more information, see [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

<span data-ttu-id="582f0-153">Configuración de Microsoft Teams setSettings() para la página de eliminación:</span><span class="sxs-lookup"><span data-stu-id="582f0-153">Microsoft Teams setSettings() configuration for removal page:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a><span data-ttu-id="582f0-154">Clientes móviles</span><span class="sxs-lookup"><span data-stu-id="582f0-154">Mobile clients</span></span>

<span data-ttu-id="582f0-155">Si decide que la pestaña canal o grupo aparezca en los clientes móviles de Teams, la configuración debe tener un `setSettings()` valor para la `websiteUrl` propiedad.</span><span class="sxs-lookup"><span data-stu-id="582f0-155">If you choose to have your channel or group tab appear on the Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span> <span data-ttu-id="582f0-156">Para obtener más información, consulte [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span><span class="sxs-lookup"><span data-stu-id="582f0-156">For more information, see [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span></span>
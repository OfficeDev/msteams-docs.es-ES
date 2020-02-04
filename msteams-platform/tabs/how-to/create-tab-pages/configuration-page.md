---
title: Crear una página de configuración
author: laujan
description: ''
keywords: canal de grupo de pestañas de Teams configurable
ms.topic: conceptualF
ms.author: laujan
ms.openlocfilehash: c7b6b636a342c650667a1131e7899908744beedf
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675715"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="420b8-103">Crear una página de configuración</span><span class="sxs-lookup"><span data-stu-id="420b8-103">Create a configuration page</span></span>

<span data-ttu-id="420b8-104">Una página de configuración es un tipo especial de [Página de contenido](content-page.md) que permite a los usuarios configurar algún aspecto de la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="420b8-104">A configuration page is a special type of [content page](content-page.md) that allows your users to configure some aspect of your Teams app.</span></span> <span data-ttu-id="420b8-105">Normalmente se usan como parte de:</span><span class="sxs-lookup"><span data-stu-id="420b8-105">Typically these are used as part of:</span></span>

* <span data-ttu-id="420b8-106">Una pestaña de canal o de chat de Grupo: la página de configuración permite recopilar información de los usuarios `contentUrl` y establecer la de la página de contenido que se va a mostrar.</span><span class="sxs-lookup"><span data-stu-id="420b8-106">A channel or group chat tab - The configuration page allows you to collect information from your users and set the `contentUrl` of the content page to display.</span></span>
* <span data-ttu-id="420b8-107">Una [extensión de mensajería](~/messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="420b8-107">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md)</span></span>
* <span data-ttu-id="420b8-108">Un [conector de Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span><span class="sxs-lookup"><span data-stu-id="420b8-108">A [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span></span>

## <a name="configuring-a-channel-or-group-chat-tab"></a><span data-ttu-id="420b8-109">Configuración de una pestaña de chat de grupo o de canal</span><span class="sxs-lookup"><span data-stu-id="420b8-109">Configuring a channel or group chat tab</span></span>

<span data-ttu-id="420b8-110">Una página de configuración informa A la página de contenido sobre cómo debe representarse.</span><span class="sxs-lookup"><span data-stu-id="420b8-110">A configuration page informs the content page how it should render.</span></span> <span data-ttu-id="420b8-111">La aplicación debe hacer referencia al SDK del cliente de JavaScript de `microsoft.initialize()` [Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) y llamar a.</span><span class="sxs-lookup"><span data-stu-id="420b8-111">Your application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="420b8-112">Además, las direcciones URL deben ser extremos HTTPS seguros y disponibles en la nube.</span><span class="sxs-lookup"><span data-stu-id="420b8-112">Additionally, your URLs must be secure HTTPS endpoints and available from the cloud.</span></span> <span data-ttu-id="420b8-113">A continuación se muestra un ejemplo de página de configuración.</span><span class="sxs-lookup"><span data-stu-id="420b8-113">Below is a configuration page example.</span></span>

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

<span data-ttu-id="420b8-114">Aquí, al usuario se le presentan dos botones de opción, **Seleccione gris** o **Seleccione rojo** para mostrar el contenido de la pestaña con un icono rojo o gris.</span><span class="sxs-lookup"><span data-stu-id="420b8-114">Here, the user is presented with two option buttons, **Select Gray** or **Select Red** to display the tab content with either a red or gray icon.</span></span> <span data-ttu-id="420b8-115">Elegir el botón relativo se `saveGray()` activa `saveRed()` o llama a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="420b8-115">Choosing the relative button fires `saveGray()` or `saveRed()` and invokes the following:</span></span>

1. <span data-ttu-id="420b8-116">El `settings.setValidityState(true)` está establecido en true.</span><span class="sxs-lookup"><span data-stu-id="420b8-116">The `settings.setValidityState(true)` is set to true.</span></span>
1. <span data-ttu-id="420b8-117">Se `microsoftTeams.settings.registerOnSaveHandler()` desencadena el controlador de eventos.</span><span class="sxs-lookup"><span data-stu-id="420b8-117">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
1. <span data-ttu-id="420b8-118">El botón **Guardar** de la página Configuración de la aplicación, cargado en Microsoft Teams, está habilitado.</span><span class="sxs-lookup"><span data-stu-id="420b8-118">The **Save** button on the app's configuration page, uploaded in Teams, is enabled.</span></span>

<span data-ttu-id="420b8-119">Este código permite que los equipos sepan que se han cumplido los requisitos de configuración y que la instalación puede continuar.</span><span class="sxs-lookup"><span data-stu-id="420b8-119">This code lets Teams know that the configuration requirements have been satisfied and the installation can proceed.</span></span> <span data-ttu-id="420b8-120">Al **Guardar**, se configuran los parámetros de `settings.setSettings()` , tal y `Settings` como se define en la interfaz, para la instancia actual (consulte la [interfaz de configuración](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest) ).</span><span class="sxs-lookup"><span data-stu-id="420b8-120">On **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface, for the current instance (See [Settings interface](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest) ).</span></span> <span data-ttu-id="420b8-121">Por último `saveEvent.notifySuccess()` , se llama a para indicar que la dirección URL del contenido se ha resuelto correctamente.</span><span class="sxs-lookup"><span data-stu-id="420b8-121">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="420b8-122">Si se registró un controlador de `microsoftTeams.settings.registerOnSaveHandler()`guardado con, la devolución `saveEvent.notifySuccess()` de `saveEvent.notifyFailure()` llamada debe invocar o para indicar el resultado de la configuración.</span><span class="sxs-lookup"><span data-stu-id="420b8-122">If a save handler was registered using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="420b8-123">Si no se registró ningún controlador de `saveEvent.notifySuccess()` guardado, la llamada se realiza automáticamente inmediatamente después de que el usuario seleccione el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="420b8-123">If no save handler was registered, the `saveEvent.notifySuccess()` call is automatically made immediately upon the user selecting the **Save** button.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="420b8-124">Obtener datos de contexto para la configuración de pestañas</span><span class="sxs-lookup"><span data-stu-id="420b8-124">Get context data for your tab settings</span></span>

<span data-ttu-id="420b8-125">Es posible que la pestaña requiera información contextual para mostrar contenido relevante.</span><span class="sxs-lookup"><span data-stu-id="420b8-125">Your tab might require contextual information to display relevant content.</span></span> <span data-ttu-id="420b8-126">La información contextual puede mejorar aún más el atractivo de su pestaña proporcionando una experiencia de usuario más personalizada.</span><span class="sxs-lookup"><span data-stu-id="420b8-126">Contextual information can further enhance your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="420b8-127">La [interfaz de contexto](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) de Microsoft Teams define las propiedades que se pueden usar para la configuración de pestañas.</span><span class="sxs-lookup"><span data-stu-id="420b8-127">The Teams [Context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) defines the properties that can be used for your tab configuration.</span></span> <span data-ttu-id="420b8-128">Puede recopilar los valores de las variables de datos de contexto de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="420b8-128">You can collect the values of context data variables in two ways:</span></span>

1. <span data-ttu-id="420b8-129">Insertar marcadores de posición de cadena de consulta de URL `configurationURL`en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="420b8-129">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

1. <span data-ttu-id="420b8-130">Usar el método de [Team SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) `microsoftTeams.getContext((context) =>{}` .</span><span class="sxs-lookup"><span data-stu-id="420b8-130">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) `microsoftTeams.getContext((context) =>{}` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="420b8-131">Insertar marcadores de posición en el`configurationURL`</span><span class="sxs-lookup"><span data-stu-id="420b8-131">Insert placeholders in the `configurationURL`</span></span>

<span data-ttu-id="420b8-132">Los marcadores de posición de la interfaz de contexto se `configurationUrl`pueden agregar a la base.</span><span class="sxs-lookup"><span data-stu-id="420b8-132">Context interface placeholders can be added to your base `configurationUrl`.</span></span> <span data-ttu-id="420b8-133">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="420b8-133">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="420b8-134">Dirección URL base</span><span class="sxs-lookup"><span data-stu-id="420b8-134">Base Url</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="420b8-135">Dirección URL base con cadenas de consulta</span><span class="sxs-lookup"><span data-stu-id="420b8-135">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="420b8-136">Una vez que se haya cargado la página, los marcadores de posición de la cadena de consulta se actualizarán en Microsoft Teams con los valores relevantes.</span><span class="sxs-lookup"><span data-stu-id="420b8-136">After your page has uploaded, the query string placeholders will be updated by Teams with the relevant values.</span></span> <span data-ttu-id="420b8-137">Puede incluir lógica en la página de configuración para recuperar y usar esos valores.</span><span class="sxs-lookup"><span data-stu-id="420b8-137">You can include logic in your configuration page to retrieve and use those values.</span></span> <span data-ttu-id="420b8-138">Para obtener más información sobre cómo trabajar con cadenas de consulta de dirección URL, vea [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) en los documentos web de MDN. A continuación, se muestra un ejemplo de cómo extraer un valor de `configurationURL` la propiedad anterior:</span><span class="sxs-lookup"><span data-stu-id="420b8-138">For more information on working with URL query strings see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN web docs. Here is an example of how to extract a value from the above `configurationURL` property:</span></span>

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="420b8-139">Usar la `getContext()` función para recuperar el contexto</span><span class="sxs-lookup"><span data-stu-id="420b8-139">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="420b8-140">Cuando se invoca, la `microsoftTeams.getContext((context) => {})` función recupera la [interfaz de contexto](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest).</span><span class="sxs-lookup"><span data-stu-id="420b8-140">When invoked, the `microsoftTeams.getContext((context) => {})` function retrieves the [Context interface](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest).</span></span> <span data-ttu-id="420b8-141">Puede Agregar esta función a la página de configuración para recuperar los valores de contexto:</span><span class="sxs-lookup"><span data-stu-id="420b8-141">You can add this function to your configuration page to retrieve context values:</span></span>

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

## <a name="context-and-authentication"></a><span data-ttu-id="420b8-142">Contexto y autenticación</span><span class="sxs-lookup"><span data-stu-id="420b8-142">Context and Authentication</span></span>

<span data-ttu-id="420b8-143">Es posible que necesite autenticación antes de permitir que un usuario configure la aplicación o que el contenido pueda incluir orígenes que tengan sus propios protocolos de autenticación.</span><span class="sxs-lookup"><span data-stu-id="420b8-143">You might require authentication before allowing a user to configure your app or your content might include sources that have their own authentication protocols.</span></span> <span data-ttu-id="420b8-144">Consulte [autenticar a un usuario en una pestaña de Microsoft teams la información de](~/tabs/how-to/authentication/auth-flow-tab.md) contexto se puede usar para ayudar a construir solicitudes de autenticación y direcciones URL de la página de autorización.</span><span class="sxs-lookup"><span data-stu-id="420b8-144">See [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md) Context information can be used to help construct authentication requests and authorization page URLs.</span></span>
<span data-ttu-id="420b8-145">Asegúrese de que todos los dominios usados en las páginas de pestañas se `manifest.json` `validDomains` enumeran en la matriz.</span><span class="sxs-lookup"><span data-stu-id="420b8-145">Make sure that all domains used in your tab pages are listed in the `manifest.json` `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="420b8-146">Modificación o eliminación de una pestaña</span><span class="sxs-lookup"><span data-stu-id="420b8-146">Modify or remove a tab</span></span>

<span data-ttu-id="420b8-147">Las opciones de eliminación admitidas pueden restringir aún más la experiencia del usuario.</span><span class="sxs-lookup"><span data-stu-id="420b8-147">Supported removal options can further refine the user experience.</span></span> <span data-ttu-id="420b8-148">Puede habilitar a los usuarios para modificar, reconfigurar o cambiar el nombre de una pestaña de grupo o canal al establecer `canUpdateConfiguration` la propiedad `true`del manifiesto en.</span><span class="sxs-lookup"><span data-stu-id="420b8-148">You can enable users to modify, reconfigure, or rename a group/channel tab by setting your manifest's `canUpdateConfiguration` property to `true`.</span></span>  <span data-ttu-id="420b8-149">Además, puede designar lo que ocurre con el contenido cuando se quita una pestaña incluyendo una página Opciones de eliminación en la aplicación y estableciendo un valor para la `removeUrl` propiedad en la `setSettings()` configuración (vea a continuación).</span><span class="sxs-lookup"><span data-stu-id="420b8-149">In addition, you can designate what happens to the content when a tab is removed by including a removal options page in your app and setting a value for the `removeUrl` property in the  `setSettings()` configuration (see below).</span></span> <span data-ttu-id="420b8-150">Las pestañas personales no se pueden modificar, pero el usuario puede desinstalarlas.</span><span class="sxs-lookup"><span data-stu-id="420b8-150">Personal tabs can't be modified but can be uninstalled by the user.</span></span> <span data-ttu-id="420b8-151">Para obtener más información, vea [crear una página de eliminación para la ficha](~/tabs/how-to/create-tab-pages/removal-page.md).</span><span class="sxs-lookup"><span data-stu-id="420b8-151">For more information, see [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

## <a name="mobile-clients"></a><span data-ttu-id="420b8-152">Clientes móviles</span><span class="sxs-lookup"><span data-stu-id="420b8-152">Mobile clients</span></span>

<span data-ttu-id="420b8-153">Si elige que la ficha canal/grupo aparezca en los clientes móviles de Teams, `setSettings()` la configuración debe tener un valor para `websiteUrl` la propiedad (vea a continuación).</span><span class="sxs-lookup"><span data-stu-id="420b8-153">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span> <span data-ttu-id="420b8-154">Pronto se ofrecerá compatibilidad completa para las pestañas en los clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="420b8-154">Full support for tabs on mobile clients will be released soon.</span></span> <span data-ttu-id="420b8-155">Para preparar la actualización, debe seguir las [instrucciones para las pestañas de dispositivos móviles](~/tabs/design/tabs-mobile.md) al crear las pestañas.</span><span class="sxs-lookup"><span data-stu-id="420b8-155">To prepare for the update, you should follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span>

<span data-ttu-id="420b8-156">Configuración de Microsoft Teams setSettings () para la página de eliminación o los clientes móviles:</span><span class="sxs-lookup"><span data-stu-id="420b8-156">Microsoft Teams setSettings() configuration for removal page and/or mobile clients:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "URL REQUIRED FOR MOBILE CLIENTS",
    removeUrl: "ADD REMOVAL PAGE URL HERE"
});
```

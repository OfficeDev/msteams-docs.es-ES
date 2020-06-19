---
title: Autenticación para pestañas con Azure Active Directory
description: Describe la autenticación en Microsoft Teams y cómo usarla en las pestañas.
keywords: pestañas de autenticación de Teams AAD
ms.openlocfilehash: 211c08ce1a51a8f0f13e622856a808661dc97b39
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801469"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a><span data-ttu-id="f011f-104">Autenticar a un usuario en una pestaña de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f011f-104">Authenticate a user in a Microsoft Teams tab</span></span>

> [!Note]
> <span data-ttu-id="f011f-105">Para que la autenticación funcione para su pestaña en clientes móviles, debe asegurarse de que está usando la versión 1.4.1 o posterior del SDK de Teams de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f011f-105">For authentication to work for your tab on mobile clients, you need to ensure you're using version 1.4.1 or later of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="f011f-106">Hay muchos servicios que puede que desee consumir dentro de la aplicación de Teams y la mayoría de esos servicios requieren autenticación y autorización para obtener acceso al servicio.</span><span class="sxs-lookup"><span data-stu-id="f011f-106">There are many services that you may wish to consume inside your Teams app, and most of those services require authentication and authorization to get access to the service.</span></span> <span data-ttu-id="f011f-107">Los servicios incluyen Facebook, Twitter y los equipos del curso.</span><span class="sxs-lookup"><span data-stu-id="f011f-107">Services include Facebook, Twitter, and of course Teams.</span></span> <span data-ttu-id="f011f-108">Los usuarios de Microsoft Teams tienen información de Perfil de usuario almacenada en Azure Active Directory (Azure AD) con Microsoft Graph y este artículo se centrará en la autenticación mediante Azure AD para obtener acceso a esta información.</span><span class="sxs-lookup"><span data-stu-id="f011f-108">Users of Teams have user profile information stored in Azure Active Directory (Azure AD) using Microsoft Graph and this article will focus on authentication using Azure AD to get access to this information.</span></span>

<span data-ttu-id="f011f-109">OAuth 2,0 es un estándar abierto para la autenticación que usa Azure AD y muchos otros proveedores de servicios.</span><span class="sxs-lookup"><span data-stu-id="f011f-109">OAuth 2.0 is an open standard for authentication used by Azure AD and many other service providers.</span></span> <span data-ttu-id="f011f-110">La comprensión de OAuth 2,0 es un requisito previo para trabajar con la autenticación en Microsoft Teams y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f011f-110">Understanding OAuth 2.0 is a prerequisite for working with authentication in Teams and Azure AD.</span></span> <span data-ttu-id="f011f-111">En los ejemplos siguientes se usa el flujo de concesión implícita de OAuth 2,0 con el objetivo de leer eventualmente la información de perfil del usuario de Azure AD y Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="f011f-111">The examples below use the OAuth 2.0 Implicit Grant flow with the goal of eventually reading the user's profile information from Azure AD and Microsoft Graph.</span></span>

<span data-ttu-id="f011f-112">El código de este artículo procede de la aplicación de ejemplo de Teams de [Microsoft Teams, ejemplo de autenticación de pestañas de Microsoft Teams (nodo)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node).</span><span class="sxs-lookup"><span data-stu-id="f011f-112">The code in this article comes from the Teams sample app [Microsoft Teams tab authentication sample (Node)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node).</span></span> <span data-ttu-id="f011f-113">Contiene una pestaña estática que solicita un token de acceso para Microsoft Graph y muestra la información básica del perfil del usuario actual de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f011f-113">It contains a static tab that requests an access token for Microsoft Graph and shows the current user's basic profile information from Azure AD.</span></span>

<span data-ttu-id="f011f-114">Para obtener información general sobre el flujo de autenticación de las pestañas, vea el tema [flujo de autenticación en las pestañas](~/tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="f011f-114">For a general overview of authentication flow for tabs see the topic [Authentication flow in tabs](~/tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="f011f-115">El flujo de autenticación en las pestañas difiere ligeramente del flujo de autenticación en los bots.</span><span class="sxs-lookup"><span data-stu-id="f011f-115">Authentication flow in tabs differs slightly from authentication flow in bots.</span></span>

## <a name="configuring-identity-providers"></a><span data-ttu-id="f011f-116">Configuración de proveedores de identidad</span><span class="sxs-lookup"><span data-stu-id="f011f-116">Configuring identity providers</span></span>

<span data-ttu-id="f011f-117">Vea el tema [configuración de proveedores de identidades](~/concepts/authentication/configure-identity-provider.md) para obtener pasos detallados sobre cómo configurar las direcciones URL de redireccionamiento de devolución de llamada de OAuth 2,0 al usar Azure Active Directory como proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="f011f-117">See the topic [Configure identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps on configuring OAuth 2.0 callback redirect URL(s) when using Azure Active Directory as an identity provider.</span></span>

## <a name="initiate-authentication-flow"></a><span data-ttu-id="f011f-118">Iniciar el flujo de autenticación</span><span class="sxs-lookup"><span data-stu-id="f011f-118">Initiate authentication flow</span></span>

<span data-ttu-id="f011f-119">El flujo de autenticación debe activarse mediante una acción del usuario.</span><span class="sxs-lookup"><span data-stu-id="f011f-119">Authentication flow should be triggered by a user action.</span></span> <span data-ttu-id="f011f-120">No debe abrir la ventana emergente de autenticación automáticamente porque es probable que desencadene el bloqueador de ventanas emergentes del explorador, así como confundir al usuario.</span><span class="sxs-lookup"><span data-stu-id="f011f-120">You should not open the authentication pop-up automatically because this is likely to trigger the browser's pop-up blocker as well as confuse the user.</span></span>

<span data-ttu-id="f011f-121">Agregue un botón a la página de configuración o de contenido para permitir que el usuario inicie sesión cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f011f-121">Add a button to your configuration or content page to enable the user to sign in when needed.</span></span> <span data-ttu-id="f011f-122">Esto se puede hacer en la página de [configuración](~/tabs/how-to/create-tab-pages/configuration-page.md) de pestañas o en cualquier página de [contenido](~/tabs/how-to/create-tab-pages/content-page.md) .</span><span class="sxs-lookup"><span data-stu-id="f011f-122">This can be done in the tab [configuration](~/tabs/how-to/create-tab-pages/configuration-page.md) page or any [content](~/tabs/how-to/create-tab-pages/content-page.md) page.</span></span>

<span data-ttu-id="f011f-123">Azure AD, al igual que la mayoría de los proveedores de identidades, no permite que su contenido se coloque en un iframe.</span><span class="sxs-lookup"><span data-stu-id="f011f-123">Azure AD, like most identity providers, does not allow its content to be placed in an iframe.</span></span> <span data-ttu-id="f011f-124">Esto significa que tendrá que agregar una página emergente para hospedar el proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="f011f-124">This means that you will need to add a pop-up page to host the identity provider.</span></span> <span data-ttu-id="f011f-125">En el siguiente ejemplo, esta página es `/tab-auth/simple-start` .</span><span class="sxs-lookup"><span data-stu-id="f011f-125">In the following example this page is `/tab-auth/simple-start`.</span></span> <span data-ttu-id="f011f-126">Use la `microsoftTeams.authenticate()` función del SDK del cliente de Microsoft Teams para iniciar esta página cuando se selecciona el botón.</span><span class="sxs-lookup"><span data-stu-id="f011f-126">Use the `microsoftTeams.authenticate()` function of the Microsoft Teams client SDK to launch this page when your button is selected.</span></span>

```javascript
microsoftTeams.authentication.authenticate({
    url: window.location.origin + "/tab-auth/simple-start",
    width: 600,
    height: 535,
    successCallback: function (result) {
        getUserProfile(result.accessToken);
    },
    failureCallback: function (reason) {
        handleAuthError(reason);
    }
});
```

### <a name="notes"></a><span data-ttu-id="f011f-127">Notas</span><span class="sxs-lookup"><span data-stu-id="f011f-127">Notes</span></span>

* <span data-ttu-id="f011f-128">La dirección URL a la que se pasa `microsoftTeams.authentication.authenticate()` es la página de inicio del flujo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="f011f-128">The URL you pass to `microsoftTeams.authentication.authenticate()` is the start page of the authentication flow.</span></span> <span data-ttu-id="f011f-129">En este ejemplo es `/tab-auth/simple-start` .</span><span class="sxs-lookup"><span data-stu-id="f011f-129">In this example that is `/tab-auth/simple-start`.</span></span> <span data-ttu-id="f011f-130">Esto debe coincidir con lo registrado en el [portal de registro de aplicaciones de Azure ad](https://apps.dev.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f011f-130">This should match what you registered in the [Azure AD Application Registration Portal](https://apps.dev.microsoft.com).</span></span>

* <span data-ttu-id="f011f-131">El flujo de autenticación debe iniciarse en una página que se encuentra en el dominio.</span><span class="sxs-lookup"><span data-stu-id="f011f-131">Authentication flow must start on a page that's on your domain.</span></span> <span data-ttu-id="f011f-132">Este dominio también debe aparecer en la [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) sección del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="f011f-132">This domain should also be listed in the [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) section of the manifest.</span></span> <span data-ttu-id="f011f-133">Si no lo hace, se producirá un elemento emergente vacío.</span><span class="sxs-lookup"><span data-stu-id="f011f-133">Failure to do so will result in an empty pop-up.</span></span>

* <span data-ttu-id="f011f-134">Si no se usa `microsoftTeams.authentication.authenticate()` , se producirá un problema con el elemento emergente que no se cerrará al final del proceso de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="f011f-134">Failing to use `microsoftTeams.authentication.authenticate()` will cause a problem with the popup not closing at the end of the sign in process.</span></span>

## <a name="navigate-to-the-authorization-page-from-your-popup-page"></a><span data-ttu-id="f011f-135">Ir a la página autorización desde la página emergente</span><span class="sxs-lookup"><span data-stu-id="f011f-135">Navigate to the authorization page from your popup page</span></span>

<span data-ttu-id="f011f-136">Cuando se muestra la página emergente ( `/tab-auth/simple-start` ), se ejecuta el siguiente código.</span><span class="sxs-lookup"><span data-stu-id="f011f-136">When your popup page (`/tab-auth/simple-start`) is displayed the following code is run.</span></span> <span data-ttu-id="f011f-137">El objetivo principal de esta página es redirigir al proveedor de identidades para que el usuario pueda iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="f011f-137">The main goal of this page is to redirect to your identity provider so the user can sign in.</span></span> <span data-ttu-id="f011f-138">Esta redirección puede realizarse en el lado servidor con HTTP 302, pero en este caso se realiza en el lado cliente con una llamada a `window.location.assign()` .</span><span class="sxs-lookup"><span data-stu-id="f011f-138">This redirection could be done on the server side using HTTP 302, but in this case it is done on the client side using with a call to `window.location.assign()`.</span></span> <span data-ttu-id="f011f-139">Esto también permite que `microsoftTeams.getContext()` se use para recuperar información de sugerencias que se puede pasar a Azure ad.</span><span class="sxs-lookup"><span data-stu-id="f011f-139">This also allows `microsoftTeams.getContext()` to be used to retrieve hinting information which can be passed to Azure AD.</span></span>

```javascript
microsoftTeams.getContext(function (context) {
    // Generate random state string and store it, so we can verify it in the callback
    let state = _guid(); // _guid() is a helper function in the sample
    localStorage.setItem("simple.state", state);
    localStorage.removeItem("simple.error");
    // Go to the Azure AD authorization endpoint
    let queryParams = {
        client_id: "YOUR_APP_ID_HERE",
        response_type: "id_token token",
        response_mode: "fragment",
        resource: "https://graph.microsoft.com/User.Read openid",
        redirect_uri: window.location.origin + "/tab-auth/simple-end",
        nonce: _guid(),
        state: state,
        // The context object is populated by Teams; the loginHint attribute
         // is used as hinting information
        login_hint: context.loginHint,
    };

    let authorizeEndpoint = "https://login.microsoftonline.com/" + context.tid + "/oauth2/v2.0/authorize?" + toQueryString(queryParams);
    window.location.assign(authorizeEndpoint);
});
```

<span data-ttu-id="f011f-140">Una vez que el usuario completa la autorización, se redirige al usuario a la página de devolución de llamada que especificó para la aplicación en `/tab-auth/simple-end` .</span><span class="sxs-lookup"><span data-stu-id="f011f-140">After the user completes authorization, the user is redirected to the callback page you specified for your app at `/tab-auth/simple-end`.</span></span>

### <a name="notes"></a><span data-ttu-id="f011f-141">Notas</span><span class="sxs-lookup"><span data-stu-id="f011f-141">Notes</span></span>

* <span data-ttu-id="f011f-142">Consulte [obtener información de contexto del usuario](~/tabs/how-to/access-teams-context.md) para obtener ayuda para crear solicitudes de autenticación y direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="f011f-142">See [get user context information](~/tabs/how-to/access-teams-context.md) for help building authentication requests and URLs.</span></span> <span data-ttu-id="f011f-143">Por ejemplo, puede usar el nombre de inicio de sesión del usuario como el valor para el inicio de `login_hint` sesión de Azure ad, lo que significa que el usuario podría tener que escribir menos.</span><span class="sxs-lookup"><span data-stu-id="f011f-143">For example, you can use the user's login name as the `login_hint` value for Azure AD sign-in, which means the user might need to type less.</span></span> <span data-ttu-id="f011f-144">Recuerde que no debe usar este contexto directamente como prueba de identidad, ya que un atacante podría cargar la página en un explorador malintencionado y proporcionarla con cualquier información que desee.</span><span class="sxs-lookup"><span data-stu-id="f011f-144">Remember that you should not use this context directly as proof of identity since an attacker could load your page in a malicious browser and provide it with any information they want.</span></span>
* <span data-ttu-id="f011f-145">Aunque el contexto de la pestaña proporciona información útil acerca del usuario, no use esta información para autenticar al usuario si los obtiene como parámetros URL en la dirección URL de contenido de la pestaña o mediante una llamada a la `microsoftTeams.getContext()` función en el SDK del cliente de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="f011f-145">Although the tab context provides useful information regarding the user, don't use this information to authenticate the user whether you get it as URL parameters to your tab content URL or by calling the `microsoftTeams.getContext()` function in the Microsoft Teams client SDK.</span></span> <span data-ttu-id="f011f-146">Un actor malintencionado podría invocar la dirección URL de contenido de pestaña con sus propios parámetros y una página web que suplanta a Microsoft Teams podría cargar la URL de contenido de la pestaña en un iframe y devolver sus propios datos a la `getContext()` función.</span><span class="sxs-lookup"><span data-stu-id="f011f-146">A malicious actor could invoke your tab content URL with its own parameters, and a web page impersonating Microsoft Teams could load your tab content URL in an iframe and return its own data to the `getContext()` function.</span></span> <span data-ttu-id="f011f-147">Debe tratar la información relacionada con la identidad en el contexto de pestañas simplemente como sugerencias y validarlas antes de usarlas.</span><span class="sxs-lookup"><span data-stu-id="f011f-147">You should treat the identity-related information in the tab context simply as hints and validate them before use.</span></span>
* <span data-ttu-id="f011f-148">El `state` parámetro se usa para confirmar que el servicio que llama al URI de devolución de llamada es el servicio al que ha llamado.</span><span class="sxs-lookup"><span data-stu-id="f011f-148">The `state` parameter is used to confirm that the service calling the callback URI is the service you called.</span></span> <span data-ttu-id="f011f-149">Si el `state` parámetro de la devolución de llamada no coincide con el parámetro enviado durante la llamada, la llamada a la devolución no se comprueba y debe finalizarse.</span><span class="sxs-lookup"><span data-stu-id="f011f-149">If the `state` parameter in the callback does not match the parameter you sent during the call the return call is not verified and should be terminated.</span></span>
* <span data-ttu-id="f011f-150">No es necesario incluir el dominio del proveedor de identidades en la `validDomains` lista de la manifest.jsdel archivo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f011f-150">It is not necessary to include the identity provider's domain in the `validDomains` list in the app's manifest.json file.</span></span>

## <a name="the-callback-page"></a><span data-ttu-id="f011f-151">La página de devolución de llamada</span><span class="sxs-lookup"><span data-stu-id="f011f-151">The callback page</span></span>

<span data-ttu-id="f011f-152">En la última sección, llamó al servicio de autorización de Azure AD y pasó la información de usuario y de la aplicación para que Azure AD pudiera presentar al usuario su propia experiencia de autorización de monolíticas.</span><span class="sxs-lookup"><span data-stu-id="f011f-152">In the last section you called the Azure AD authorization service and passed in user and app information so that Azure AD could present the user with its own monolithic authorization experience.</span></span> <span data-ttu-id="f011f-153">La aplicación no tiene control sobre lo que sucede en esta experiencia.</span><span class="sxs-lookup"><span data-stu-id="f011f-153">Your app has no control over what happens in this experience.</span></span> <span data-ttu-id="f011f-154">Todo lo que sabe es lo que se devuelve cuando Azure AD llama a la página de devolución de llamada que ha proporcionado ( `/tab-auth/simple-end` ).</span><span class="sxs-lookup"><span data-stu-id="f011f-154">All it knows is what is returned when Azure AD calls the  callback page that you provided (`/tab-auth/simple-end`).</span></span>

<span data-ttu-id="f011f-155">En esta página, debe determinar si se ha realizado correctamente o no el error en función de la información devuelta por Azure AD y llamar a `microsoftTeams.authentication.notifySuccess()` o `microsoftTeams.authentication.notifyFailure()` .</span><span class="sxs-lookup"><span data-stu-id="f011f-155">In this page you need to determine success or failure based on the information returned by Azure AD and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()`.</span></span> <span data-ttu-id="f011f-156">Si el inicio de sesión tuvo éxito, tendrá acceso a los recursos de servicio.</span><span class="sxs-lookup"><span data-stu-id="f011f-156">If the login was successful you will have access to service resources.</span></span>

````javascript
// Split the key-value pairs passed from Azure AD
// getHashParameters is a helper function that parses the arguments sent
// to the callback URL by Azure AD after the authorization call
let hashParams = getHashParameters();
if (hashParams["error"]) {
    // Authentication/authorization failed
    microsoftTeams.authentication.notifyFailure(hashParams["error"]);
} else if (hashParams["access_token"]) {
    // Get the stored state parameter and compare with incoming state
    // This validates that the data is coming from Azure AD
    let expectedState = localStorage.getItem("simple.state");
    if (expectedState !== hashParams["state"]) {
        // State does not match, report error
        microsoftTeams.authentication.notifyFailure("StateDoesNotMatch");
    } else {
        // Success: return token information to the tab
        microsoftTeams.authentication.notifySuccess({
            idToken: hashParams["id_token"],
            accessToken: hashParams["access_token"],
            tokenType: hashParams["token_type"],
            expiresIn: hashParams["expires_in"]
        })
    }
} else {
    // Unexpected condition: hash does not contain error or access_token parameter
    microsoftTeams.authentication.notifyFailure("UnexpectedFailure");
}
````

<span data-ttu-id="f011f-157">Este código analiza los pares clave-valor recibidos de Azure AD `window.location.hash` con la `getHashParameters()` función auxiliar.</span><span class="sxs-lookup"><span data-stu-id="f011f-157">This code parses the key-value pairs received from Azure AD in `window.location.hash` using the `getHashParameters()` helper function.</span></span> <span data-ttu-id="f011f-158">Si encuentra un `access_token` , y el `state` valor es el mismo que el proporcionado al principio del flujo de autenticación, devuelve el token de acceso a la pestaña mediante una llamada `notifySuccess()` ; en caso contrario, informa de un error `notifyFailure()` .</span><span class="sxs-lookup"><span data-stu-id="f011f-158">If it finds an `access_token`, and the `state` value is the same as the one provided at the start of the authentication flow, it returns the access token to the tab by calling `notifySuccess()`; otherwise it reports an error with `notifyFailure()`.</span></span>

### <a name="notes"></a><span data-ttu-id="f011f-159">Notas</span><span class="sxs-lookup"><span data-stu-id="f011f-159">Notes</span></span>

<span data-ttu-id="f011f-160">`NotifyFailure()`tiene los siguientes motivos de error predefinidos:</span><span class="sxs-lookup"><span data-stu-id="f011f-160">`NotifyFailure()` has the following predefined failure reasons:</span></span>

* <span data-ttu-id="f011f-161">`CancelledByUser`el usuario ha cerrado la ventana del elemento emergente antes de completar el flujo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="f011f-161">`CancelledByUser` the user closed the popup window before completing the authentication flow.</span></span>
* <span data-ttu-id="f011f-162">`FailedToOpenWindow`no se pudo abrir la ventana emergente.</span><span class="sxs-lookup"><span data-stu-id="f011f-162">`FailedToOpenWindow` the popup window could not be opened.</span></span> <span data-ttu-id="f011f-163">Cuando se ejecuta Microsoft Teams en un explorador, suele significar que la ventana fue bloqueada por un bloqueador de elementos emergentes.</span><span class="sxs-lookup"><span data-stu-id="f011f-163">When running Microsoft Teams in a browser, this typically means that the window was blocked by a popup blocker.</span></span>

<span data-ttu-id="f011f-164">Si se ejecuta correctamente, puede actualizar o volver a cargar la página y mostrar contenido relevante para el usuario autenticado ahora.</span><span class="sxs-lookup"><span data-stu-id="f011f-164">If successful, you can refresh or reload the page and show content relevant to the now-authenticated user.</span></span> <span data-ttu-id="f011f-165">Si se produce un error en la autenticación, mostrar un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="f011f-165">If authentication fails, display an error message.</span></span>

<span data-ttu-id="f011f-166">La aplicación puede establecer su propia cookie de sesión para que el usuario no tenga que volver a iniciarla cuando vuelva a su pestaña en el dispositivo actual.</span><span class="sxs-lookup"><span data-stu-id="f011f-166">Your app can set its own session cookie so that the user need not sign in again when they return to your tab on the current device.</span></span>

> [!NOTE]
> <span data-ttu-id="f011f-167">Chrome 80, programado para su lanzamiento en principios de 2020, presenta nuevos valores de cookies e impone directivas de cookies de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f011f-167">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="f011f-168">Se recomienda establecer el uso previsto para las cookies en lugar de basarse en el comportamiento predeterminado del explorador.</span><span class="sxs-lookup"><span data-stu-id="f011f-168">It's recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="f011f-169">*Consulte* [SameSite cookie Attribute (2020 Update)](../../../resources/samesite-cookie-update.md).</span><span class="sxs-lookup"><span data-stu-id="f011f-169">*See* [SameSite cookie attribute (2020 update)](../../../resources/samesite-cookie-update.md).</span></span>

<span data-ttu-id="f011f-170">Para obtener más información sobre el inicio de sesión único (SSO), vea el artículo [autenticación silenciosa](~/tabs/how-to/authentication/auth-silent-AAD.md).</span><span class="sxs-lookup"><span data-stu-id="f011f-170">For more information on Single Sign-On (SSO) see the article [Silent authentication](~/tabs/how-to/authentication/auth-silent-AAD.md).</span></span>

## <a name="samples"></a><span data-ttu-id="f011f-171">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="f011f-171">Samples</span></span>

<span data-ttu-id="f011f-172">Para ver el código de ejemplo que muestra el proceso de autenticación de pestañas con Azure AD, consulte:</span><span class="sxs-lookup"><span data-stu-id="f011f-172">For sample code showing the tab authentication process using Azure AD see:</span></span>

* [<span data-ttu-id="f011f-173">Ejemplo de autenticación de pestañas de Microsoft Teams (nodo)</span><span class="sxs-lookup"><span data-stu-id="f011f-173">Microsoft Teams tab authentication sample (Node)</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)

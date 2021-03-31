---
title: Autenticación silenciosa
description: Describe la autenticación silenciosa
ms.topic: conceptual
keywords: AAD silencioso de SSO de autenticación de teams
ms.openlocfilehash: 7a68c532cadf181b15c16d6bc4d4ab861d5c9922
ms.sourcegitcommit: 2bf651dfbaf5dbab6d466788f668e7a6c5d69c36
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2021
ms.locfileid: "51421611"
---
# <a name="silent-authentication"></a><span data-ttu-id="50071-104">Autenticación silenciosa</span><span class="sxs-lookup"><span data-stu-id="50071-104">Silent authentication</span></span>

> [!NOTE]
> <span data-ttu-id="50071-105">Para que la autenticación funcione para su pestaña en clientes móviles, asegúrese de que está usando al menos la versión 1.4.1 del SDK de JavaScript de Teams.</span><span class="sxs-lookup"><span data-stu-id="50071-105">For authentication to work for your tab on mobile clients, ensure you are using at least 1.4.1 version of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="50071-106">La autenticación silenciosa en Azure Active Directory (AAD) minimiza el número de veces que un usuario escribe sus credenciales de inicio de sesión actualizando silenciosamente el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="50071-106">Silent authentication in Azure Active Directory (AAD) minimizes the number of times a user enters their sign in credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="50071-107">Para obtener soporte para el inicio de sesión único verdadero, vea [la documentación de SSO](~/tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="50071-107">For true single sign-on support, see [SSO documentation](~/tabs/how-to/authentication/auth-aad-sso.md).</span></span>

<span data-ttu-id="50071-108">Si desea mantener el código completamente del lado cliente, puede usar la biblioteca de autenticación de [AAD](/azure/active-directory/develop/active-directory-authentication-libraries) para JavaScript para obtener un token de acceso de AAD de forma silenciosa.</span><span class="sxs-lookup"><span data-stu-id="50071-108">If you want to keep your code completely client-side, you can use the [AAD authentication library](/azure/active-directory/develop/active-directory-authentication-libraries) for JavaScript to get an AAD access token silently.</span></span> <span data-ttu-id="50071-109">Si el usuario ha iniciado sesión recientemente, nunca verá un cuadro de diálogo emergente.</span><span class="sxs-lookup"><span data-stu-id="50071-109">If the user has signed in recently, they never see a popup dialog box.</span></span>

<span data-ttu-id="50071-110">Aunque la biblioteca ADAL.js está optimizada para aplicaciones angularJS, también funciona con aplicaciones de página única de JavaScript puras.</span><span class="sxs-lookup"><span data-stu-id="50071-110">Even though the ADAL.js library is optimized for AngularJS applications, it also works with pure JavaScript single-page applications.</span></span>

> [!NOTE]
> <span data-ttu-id="50071-111">Actualmente, la autenticación silenciosa solo funciona para las pestañas.</span><span class="sxs-lookup"><span data-stu-id="50071-111">Currently, silent authentication only works for tabs.</span></span> <span data-ttu-id="50071-112">No funciona al iniciar sesión desde un bot.</span><span class="sxs-lookup"><span data-stu-id="50071-112">It does not work when signing in from a bot.</span></span>

## <a name="how-silent-authentication-works"></a><span data-ttu-id="50071-113">Cómo funciona la autenticación silenciosa</span><span class="sxs-lookup"><span data-stu-id="50071-113">How silent authentication works</span></span>

<span data-ttu-id="50071-114">La ADAL.js crea un iframe oculto para el flujo de concesión implícito de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="50071-114">The ADAL.js library creates a hidden iframe for OAuth 2.0 implicit grant flow.</span></span> <span data-ttu-id="50071-115">Pero la biblioteca especifica `prompt=none` , por lo que Azure AD nunca muestra la página de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="50071-115">But the library specifies `prompt=none`, so Azure AD never shows the sign in page.</span></span> <span data-ttu-id="50071-116">Si la interacción del usuario es necesaria porque el usuario necesita iniciar sesión o conceder acceso a la aplicación, AAD devuelve inmediatamente un error que ADAL.js informes a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="50071-116">If user interaction is required because the user needs to sign in or grant access to the application, AAD immediately returns an error that ADAL.js reports to your app.</span></span> <span data-ttu-id="50071-117">En este punto, la aplicación puede mostrar un botón de inicio de sesión si es necesario.</span><span class="sxs-lookup"><span data-stu-id="50071-117">At this point your app can show a sign in button if required.</span></span>

## <a name="how-to-do-silent-authentication"></a><span data-ttu-id="50071-118">Cómo realizar la autenticación silenciosa</span><span class="sxs-lookup"><span data-stu-id="50071-118">How to do silent authentication</span></span>

<span data-ttu-id="50071-119">El código de este artículo proviene de la aplicación de ejemplo de Teams que es el nodo de ejemplo [de autenticación de Teams](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs).</span><span class="sxs-lookup"><span data-stu-id="50071-119">The code in this article comes from the Teams sample app that is [Teams authentication sample node](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs).</span></span>

<span data-ttu-id="50071-120">[Inicie la pestaña configurable de autenticación](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) silenciosa y sencilla con AAD y siga las instrucciones para ejecutar el ejemplo en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="50071-120">[Initiate silent and simple authentication configurable tab using AAD](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) and follow the instructions to run the sample on your local machine.</span></span>

### <a name="include-and-configure-adal"></a><span data-ttu-id="50071-121">Incluir y configurar ADAL</span><span class="sxs-lookup"><span data-stu-id="50071-121">Include and configure ADAL</span></span>

<span data-ttu-id="50071-122">Incluya la biblioteca ADAL.js en las páginas de pestañas y configure ADAL con el identificador de cliente y la dirección URL de redireccionamiento:</span><span class="sxs-lookup"><span data-stu-id="50071-122">Include the ADAL.js library in your tab pages and configure ADAL with your client ID and redirect URL:</span></span>

```html
<script src="https://secure.aadcdn.microsoftonline-p.com/lib/1.0.15/js/adal.min.js" integrity="sha384-lIk8T3uMxKqXQVVfFbiw0K/Nq+kt1P3NtGt/pNexiDby2rKU6xnDY8p16gIwKqgI" crossorigin="anonymous"></script>
<script type="text/javascript">
    // ADAL.js configuration
    let config = {
        clientId: "YOUR_APP_ID_HERE",
        // redirectUri must be in the list of redirect URLs for the Azure AD app
        redirectUri: window.location.origin + "/tab-auth/silent-end",
        cacheLocation: "localStorage",
        navigateToLoginRequestUrl: false,
    };
</script>
```

### <a name="get-the-user-context"></a><span data-ttu-id="50071-123">Obtener el contexto de usuario</span><span class="sxs-lookup"><span data-stu-id="50071-123">Get the user context</span></span>

<span data-ttu-id="50071-124">En la página de contenido de la pestaña, llama para obtener una sugerencia de `microsoftTeams.getContext()` inicio de sesión para el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="50071-124">In the tab's content page, call `microsoftTeams.getContext()` to get a sign in hint for the current user.</span></span> <span data-ttu-id="50071-125">Esto se usa como loginHint en la llamada a AAD.</span><span class="sxs-lookup"><span data-stu-id="50071-125">This is used as a loginHint in the call to AAD.</span></span>

```javascript
// Set up extra query parameters for ADAL
// - openid and profile scope adds profile information to the id_token
// - login_hint provides the expected user name
if (loginHint) {
    config.extraQueryParameter = "scope=openid+profile&login_hint=" + encodeURIComponent(loginHint);
} else {
    config.extraQueryParameter = "scope=openid+profile";
}
```

### <a name="authenticate"></a><span data-ttu-id="50071-126">Autenticar</span><span class="sxs-lookup"><span data-stu-id="50071-126">Authenticate</span></span>

<span data-ttu-id="50071-127">Si ADAL tiene un token almacenado en caché para el usuario que no ha expirado, use ese token.</span><span class="sxs-lookup"><span data-stu-id="50071-127">If ADAL has a token cached for the user that has not expired, use that token.</span></span> <span data-ttu-id="50071-128">Como alternativa, intente obtener un token de forma silenciosa llamando a `acquireToken(resource, callback)` .</span><span class="sxs-lookup"><span data-stu-id="50071-128">Alternately, attempt to get a token silently by calling `acquireToken(resource, callback)`.</span></span> <span data-ttu-id="50071-129">ADAL.js llama a la función de devolución de llamada con el token solicitado o genera un error si se produce un error en la autenticación.</span><span class="sxs-lookup"><span data-stu-id="50071-129">ADAL.js calls the callback function with the requested token, or gives an error if authentication fails.</span></span>

<span data-ttu-id="50071-130">Si recibe un error en la función de devolución de llamada, muestre un botón de inicio de sesión y vuelva a un inicio de sesión explícito.</span><span class="sxs-lookup"><span data-stu-id="50071-130">If you get an error in the callback function, show a sign in button and fall back to an explicit sign in.</span></span>

```javascript
let authContext = new AuthenticationContext(config); // from the ADAL.js library
// See if there's a cached user and it matches the expected user
let user = authContext.getCachedUser();
if (user) {
    if (user.profile.oid !== userObjectId) {
        // User doesn't match, clear the cache
        authContext.clearCache();
    }
}

// In this example we are getting an id token (which ADAL.js returns if we ask for resource = clientId)
authContext.acquireToken(config.clientId, function (errDesc, token, err, tokenType) {
    if (token) {
        // Make sure ADAL gave us an id token
        if (tokenType !== authContext.CONSTANTS.ID_TOKEN) {
            token = authContext.getCachedToken(config.clientId);
        }
        showProfileInformation(idToken);
    } else {
        console.log("Renewal failed: " + err);
        // Failed to get the token silently; show the login button
        showLoginButton();
        // You could attempt to launch the login popup here, but in browsers this could be blocked by
        // a popup blocker, in which case the login attempt will fail with the reason FailedToOpenWindow.
    }
});
```

### <a name="process-the-return-value"></a><span data-ttu-id="50071-131">Procesar el valor devuelto</span><span class="sxs-lookup"><span data-stu-id="50071-131">Process the return value</span></span>

<span data-ttu-id="50071-132">ADAL.js analiza el resultado de AAD llamando a la página de devolución `AuthenticationContext.handleWindowCallback(hash)` de llamada de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="50071-132">ADAL.js parses the result from AAD by calling `AuthenticationContext.handleWindowCallback(hash)` in the sign in callback page.</span></span>

<span data-ttu-id="50071-133">Compruebe que tiene un usuario válido y llame o para notificar el estado a la página de contenido `microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()` de la pestaña principal.</span><span class="sxs-lookup"><span data-stu-id="50071-133">Check that you have a valid user and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()` to report the status to your main tab content page.</span></span>

```javascript
if (authContext.isCallback(window.location.hash)) {
    authContext.handleWindowCallback(window.location.hash);
    if (window.parent === window) {
        if (authContext.getCachedUser()) {
            microsoftTeams.authentication.notifySuccess();
        } else {
            microsoftTeams.authentication.notifyFailure(authContext.getLoginError());
        }
    }
}
```

### <a name="handle-sign-out-flow"></a><span data-ttu-id="50071-134">Controlar el flujo de salida</span><span class="sxs-lookup"><span data-stu-id="50071-134">Handle sign out flow</span></span>

<span data-ttu-id="50071-135">Use el siguiente código para controlar el flujo de salida en AAD Auth:</span><span class="sxs-lookup"><span data-stu-id="50071-135">Use the following code to handle sign out flow in AAD Auth:</span></span>

> [!NOTE]
> <span data-ttu-id="50071-136">Mientras se realiza el cierre de sesión de la pestaña o bot de Teams, también se borra la sesión actual.</span><span class="sxs-lookup"><span data-stu-id="50071-136">While logout for Teams tab or bot is done, the current session is also cleared.</span></span>

```javascript
function logout() {
localStorage.clear();
window.location.href = "@Url.Action("<<Action Name>>", "<<Controller Name>>")";
}
```

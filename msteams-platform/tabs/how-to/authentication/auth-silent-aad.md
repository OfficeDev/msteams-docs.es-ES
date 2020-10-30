---
title: Autenticación silenciosa
description: Describe la autenticación silenciosa
keywords: autenticación de Teams AAD en modo silencioso de SSO
ms.openlocfilehash: b8a5b8cb9328635f5730ca089da29140d0a17ac4
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796368"
---
# <a name="silent-authentication"></a><span data-ttu-id="47a26-104">Autenticación silenciosa</span><span class="sxs-lookup"><span data-stu-id="47a26-104">Silent authentication</span></span>

> [!NOTE]
> <span data-ttu-id="47a26-105">Para que la autenticación funcione para su pestaña en clientes móviles, debe asegurarse de que está usando al menos la versión 1.4.1 del SDK de Teams para JavaScript.</span><span class="sxs-lookup"><span data-stu-id="47a26-105">For authentication to work for your tab on mobile clients, you need to ensure you're using at least the 1.4.1 version of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="47a26-106">La autenticación silenciosa en Azure Active Directory (Azure AD) minimiza el número de veces que un usuario necesita escribir sus credenciales de inicio de sesión mediante la actualización silenciosa del token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="47a26-106">Silent authentication in Azure Active Directory (Azure AD) minimizes the number of times a user needs to enter their login credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="47a26-107">(Para admitir un verdadero inicio de sesión único, vea nuestra [documentación de SSO](~/tabs/how-to/authentication/auth-aad-sso.md))</span><span class="sxs-lookup"><span data-stu-id="47a26-107">(For true single sign-on support, view our [SSO Documentation](~/tabs/how-to/authentication/auth-aad-sso.md))</span></span>

<span data-ttu-id="47a26-108">Si desea mantener el código completamente en el lado cliente, puede usar la biblioteca de [autenticación de Azure Active Directory](/azure/active-directory/develop/active-directory-authentication-libraries) para JavaScript para intentar adquirir un token de acceso de Azure ad de forma silenciosa.</span><span class="sxs-lookup"><span data-stu-id="47a26-108">If you want to keep your code completely client-side, you can use the [Azure Active Directory Authentication Library](/azure/active-directory/develop/active-directory-authentication-libraries) for JavaScript to attempt to acquire an Azure AD access token silently.</span></span> <span data-ttu-id="47a26-109">Esto significa que es posible que el usuario nunca vea un cuadro de diálogo emergente si ha iniciado sesión recientemente.</span><span class="sxs-lookup"><span data-stu-id="47a26-109">This means that the user may never see a popup dialog if they have signed in recently.</span></span>

<span data-ttu-id="47a26-110">Aunque la biblioteca de ADAL.js está optimizada para las aplicaciones de AngularJS, también funciona con aplicaciones de una sola página de JavaScript pura.</span><span class="sxs-lookup"><span data-stu-id="47a26-110">Even though the ADAL.js library is optimized for AngularJS applications, it also works with pure JavaScript single-page applications.</span></span>

> [!NOTE]
> <span data-ttu-id="47a26-111">Actualmente, la autenticación silenciosa solo funciona en las pestañas.</span><span class="sxs-lookup"><span data-stu-id="47a26-111">Currently, silent authentication only works for tabs.</span></span> <span data-ttu-id="47a26-112">Todavía no funciona al iniciar sesión desde un bot.</span><span class="sxs-lookup"><span data-stu-id="47a26-112">It does not yet work when signing in from a bot.</span></span>

## <a name="how-silent-authentication-works"></a><span data-ttu-id="47a26-113">Cómo funciona la autenticación silenciosa</span><span class="sxs-lookup"><span data-stu-id="47a26-113">How silent authentication works</span></span>

<span data-ttu-id="47a26-114">La biblioteca de ADAL.js crea un iframe oculto para OAuth 2,0 el flujo de concesión implícito, pero especifica que `prompt=none` Azure ad nunca muestre la página de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="47a26-114">The ADAL.js library creates a hidden iframe for OAuth 2.0 implicit grant flow, but it specifies `prompt=none` so that Azure AD never shows the login page.</span></span> <span data-ttu-id="47a26-115">Si se requiere la interacción del usuario porque el usuario tiene que iniciar sesión o conceder acceso a la aplicación, Azure AD devolverá inmediatamente un error que ADAL.js, a continuación, informa a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="47a26-115">If user interaction is required because the user needs to log in or grant access to the application, Azure AD will immediately return an error that ADAL.js then reports to your app.</span></span> <span data-ttu-id="47a26-116">En este punto, la aplicación puede mostrar un botón de inicio de sesión si es necesario.</span><span class="sxs-lookup"><span data-stu-id="47a26-116">At this point your app can show a login button if needed.</span></span>

## <a name="how-to-do-silent-authentication"></a><span data-ttu-id="47a26-117">Cómo realizar la autenticación silenciosa</span><span class="sxs-lookup"><span data-stu-id="47a26-117">How to do silent authentication</span></span>

<span data-ttu-id="47a26-118">El código de este artículo procede de la aplicación de ejemplo de Microsoft Teams de ejemplo de [autenticación de Microsoft Teams (nodo)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node).</span><span class="sxs-lookup"><span data-stu-id="47a26-118">The code in this article comes from the Teams sample app [Microsoft Teams Authentication Sample (Node)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node).</span></span>

### <a name="include-and-configure-adal"></a><span data-ttu-id="47a26-119">incluir y configurar ADAL</span><span class="sxs-lookup"><span data-stu-id="47a26-119">include and configure ADAL</span></span>

<span data-ttu-id="47a26-120">Incluya la biblioteca de ADAL.js en las páginas de pestañas y configure ADAL con el identificador de cliente y la dirección URL de redireccionamiento:</span><span class="sxs-lookup"><span data-stu-id="47a26-120">Include the ADAL.js library in your tab pages and configure ADAL with your client ID and redirect URL:</span></span>

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

### <a name="get-the-user-context"></a><span data-ttu-id="47a26-121">Obtener el contexto de usuario</span><span class="sxs-lookup"><span data-stu-id="47a26-121">Get the user context</span></span>

<span data-ttu-id="47a26-122">En la página contenido de la pestaña, llame `microsoftTeams.getContext()` a para obtener una sugerencia de inicio de sesión para el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="47a26-122">In the tab's content page, call `microsoftTeams.getContext()` to get a login hint for the current user.</span></span> <span data-ttu-id="47a26-123">Se usará como login_hint en la llamada a Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47a26-123">This will be used as a login_hint in the call to Azure AD.</span></span>

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

### <a name="authenticate"></a><span data-ttu-id="47a26-124">Autenticar</span><span class="sxs-lookup"><span data-stu-id="47a26-124">Authenticate</span></span>

<span data-ttu-id="47a26-125">Si ADAL tiene un token no expirado almacenado en caché para el usuario, úselo.</span><span class="sxs-lookup"><span data-stu-id="47a26-125">If ADAL has an unexpired token cached for the user, use that.</span></span> <span data-ttu-id="47a26-126">De lo contrario, intente obtener un token silenciosamente llamando a `acquireToken(resource, callback)` .</span><span class="sxs-lookup"><span data-stu-id="47a26-126">Otherwise, attempt to get a token silently by calling `acquireToken(resource, callback)`.</span></span> <span data-ttu-id="47a26-127">ADAL.js llamará a la función de devolución de llamada con el token solicitado o un error si se produce un error en la autenticación.</span><span class="sxs-lookup"><span data-stu-id="47a26-127">ADAL.js will call your callback function with the requested token, or an error if authentication fails.</span></span>

<span data-ttu-id="47a26-128">Si recibe un error en la función de devolución de llamada, muestre un botón de inicio de sesión y vuelva a un inicio de sesión explícito.</span><span class="sxs-lookup"><span data-stu-id="47a26-128">If you get an error in the callback function, show a login button and fall back to an explicit login.</span></span>

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

### <a name="process-the-return-value"></a><span data-ttu-id="47a26-129">Procesar el valor devuelto</span><span class="sxs-lookup"><span data-stu-id="47a26-129">Process the return value</span></span>

<span data-ttu-id="47a26-130">Deje que ADAL.js se encargue de analizar el resultado de Azure AD llamando a `AuthenticationContext.handleWindowCallback(hash)` la página de devolución de llamada de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="47a26-130">Let ADAL.js take care of parsing the result from Azure AD by calling `AuthenticationContext.handleWindowCallback(hash)` in the login callback page.</span></span>

<span data-ttu-id="47a26-131">Compruebe que tenemos un usuario válido y llame `microsoftTeams.authentication.notifySuccess()` o `microsoftTeams.authentication.notifyFailure()` para informar del estado a la página de contenido de la ficha principal.</span><span class="sxs-lookup"><span data-stu-id="47a26-131">Check that we have a valid user and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()` to report status back to your main tab content page.</span></span>

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

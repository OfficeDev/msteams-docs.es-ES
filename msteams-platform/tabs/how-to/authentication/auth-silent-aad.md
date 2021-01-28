---
title: Autenticación silenciosa
description: Describe la autenticación silenciosa
ms.topic: conceptual
keywords: AAD silencioso de SSO de autenticación de teams
ms.openlocfilehash: e55e415aba08fdedf4409abf39115838c3a5faf0
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014099"
---
# <a name="silent-authentication"></a><span data-ttu-id="da32e-104">Autenticación silenciosa</span><span class="sxs-lookup"><span data-stu-id="da32e-104">Silent authentication</span></span>

> [!NOTE]
> <span data-ttu-id="da32e-105">Para que la autenticación funcione con la pestaña en clientes móviles, debe asegurarse de que está usando al menos la versión 1.4.1 del SDK de JavaScript de Teams.</span><span class="sxs-lookup"><span data-stu-id="da32e-105">For authentication to work for your tab on mobile clients, you need to ensure you're using at least the 1.4.1 version of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="da32e-106">La autenticación silenciosa en Azure Active Directory (Azure AD) minimiza el número de veces que un usuario necesita escribir sus credenciales de inicio de sesión actualizando silenciosamente el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="da32e-106">Silent authentication in Azure Active Directory (Azure AD) minimizes the number of times a user needs to enter their login credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="da32e-107">(Para obtener compatibilidad con el inicio de sesión único verdadero, consulte nuestra [documentación de SSO)](~/tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="da32e-107">(For true single sign-on support, view our [SSO Documentation](~/tabs/how-to/authentication/auth-aad-sso.md))</span></span>

<span data-ttu-id="da32e-108">Si desea mantener el código completamente del lado cliente, puede usar la Biblioteca de autenticación de [Azure Active Directory](/azure/active-directory/develop/active-directory-authentication-libraries) para JavaScript para intentar adquirir un token de acceso de Azure AD de forma silenciosa.</span><span class="sxs-lookup"><span data-stu-id="da32e-108">If you want to keep your code completely client-side, you can use the [Azure Active Directory Authentication Library](/azure/active-directory/develop/active-directory-authentication-libraries) for JavaScript to attempt to acquire an Azure AD access token silently.</span></span> <span data-ttu-id="da32e-109">Esto significa que es posible que el usuario nunca vea un cuadro de diálogo emergente si ha iniciado sesión recientemente.</span><span class="sxs-lookup"><span data-stu-id="da32e-109">This means that the user may never see a popup dialog if they have signed in recently.</span></span>

<span data-ttu-id="da32e-110">Aunque la biblioteca ADAL.js está optimizada para aplicaciones de AngularJS, también funciona con aplicaciones puras de una sola página de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="da32e-110">Even though the ADAL.js library is optimized for AngularJS applications, it also works with pure JavaScript single-page applications.</span></span>

> [!NOTE]
> <span data-ttu-id="da32e-111">Actualmente, la autenticación silenciosa solo funciona para las pestañas.</span><span class="sxs-lookup"><span data-stu-id="da32e-111">Currently, silent authentication only works for tabs.</span></span> <span data-ttu-id="da32e-112">Aún no funciona al iniciar sesión desde un bot.</span><span class="sxs-lookup"><span data-stu-id="da32e-112">It does not yet work when signing in from a bot.</span></span>

## <a name="how-silent-authentication-works"></a><span data-ttu-id="da32e-113">Funcionamiento de la autenticación silenciosa</span><span class="sxs-lookup"><span data-stu-id="da32e-113">How silent authentication works</span></span>

<span data-ttu-id="da32e-114">La ADAL.js web crea un iframe oculto para el flujo de concesión implícito de OAuth 2.0, pero especifica para que Azure AD nunca muestre la página `prompt=none` de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="da32e-114">The ADAL.js library creates a hidden iframe for OAuth 2.0 implicit grant flow, but it specifies `prompt=none` so that Azure AD never shows the login page.</span></span> <span data-ttu-id="da32e-115">Si se requiere la interacción del usuario porque el usuario necesita iniciar sesión o conceder acceso a la aplicación, Azure AD devolverá inmediatamente un error que ADAL.js informa a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="da32e-115">If user interaction is required because the user needs to log in or grant access to the application, Azure AD will immediately return an error that ADAL.js then reports to your app.</span></span> <span data-ttu-id="da32e-116">En este punto, la aplicación puede mostrar un botón de inicio de sesión si es necesario.</span><span class="sxs-lookup"><span data-stu-id="da32e-116">At this point your app can show a login button if needed.</span></span>

## <a name="how-to-do-silent-authentication"></a><span data-ttu-id="da32e-117">Cómo realizar la autenticación silenciosa</span><span class="sxs-lookup"><span data-stu-id="da32e-117">How to do silent authentication</span></span>

<span data-ttu-id="da32e-118">El código de este artículo proviene de la aplicación de ejemplo de [Microsoft Teams Authentication Sample (Node).](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)</span><span class="sxs-lookup"><span data-stu-id="da32e-118">The code in this article comes from the Teams sample app [Microsoft Teams Authentication Sample (Node)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node).</span></span>

### <a name="include-and-configure-adal"></a><span data-ttu-id="da32e-119">incluir y configurar ADAL</span><span class="sxs-lookup"><span data-stu-id="da32e-119">include and configure ADAL</span></span>

<span data-ttu-id="da32e-120">Incluya la biblioteca ADAL.js en las páginas de la pestaña y configure ADAL con el identificador de cliente y la dirección URL de redireccionamiento:</span><span class="sxs-lookup"><span data-stu-id="da32e-120">Include the ADAL.js library in your tab pages and configure ADAL with your client ID and redirect URL:</span></span>

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

### <a name="get-the-user-context"></a><span data-ttu-id="da32e-121">Obtener el contexto de usuario</span><span class="sxs-lookup"><span data-stu-id="da32e-121">Get the user context</span></span>

<span data-ttu-id="da32e-122">En la página de contenido de la pestaña, llama para obtener una sugerencia de `microsoftTeams.getContext()` inicio de sesión para el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="da32e-122">In the tab's content page, call `microsoftTeams.getContext()` to get a login hint for the current user.</span></span> <span data-ttu-id="da32e-123">Esto se usará como una login_hint en la llamada a Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da32e-123">This will be used as a login_hint in the call to Azure AD.</span></span>

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

### <a name="authenticate"></a><span data-ttu-id="da32e-124">Autenticar</span><span class="sxs-lookup"><span data-stu-id="da32e-124">Authenticate</span></span>

<span data-ttu-id="da32e-125">Si ADAL tiene un token no explorado almacenado en caché para el usuario, úselo.</span><span class="sxs-lookup"><span data-stu-id="da32e-125">If ADAL has an unexpired token cached for the user, use that.</span></span> <span data-ttu-id="da32e-126">De lo contrario, intente obtener un token en modo silencioso llamando `acquireToken(resource, callback)` a .</span><span class="sxs-lookup"><span data-stu-id="da32e-126">Otherwise, attempt to get a token silently by calling `acquireToken(resource, callback)`.</span></span> <span data-ttu-id="da32e-127">ADAL.js llamará a la función de devolución de llamada con el token solicitado o un error si se produce un error en la autenticación.</span><span class="sxs-lookup"><span data-stu-id="da32e-127">ADAL.js will call your callback function with the requested token, or an error if authentication fails.</span></span>

<span data-ttu-id="da32e-128">Si recibe un error en la función de devolución de llamada, muestre un botón de inicio de sesión y vuelva a un inicio de sesión explícito.</span><span class="sxs-lookup"><span data-stu-id="da32e-128">If you get an error in the callback function, show a login button and fall back to an explicit login.</span></span>

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

### <a name="process-the-return-value"></a><span data-ttu-id="da32e-129">Procesar el valor devuelto</span><span class="sxs-lookup"><span data-stu-id="da32e-129">Process the return value</span></span>

<span data-ttu-id="da32e-130">Deje ADAL.js analizar el resultado de Azure AD llamando en la página de devolución de llamada `AuthenticationContext.handleWindowCallback(hash)` de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="da32e-130">Let ADAL.js take care of parsing the result from Azure AD by calling `AuthenticationContext.handleWindowCallback(hash)` in the login callback page.</span></span>

<span data-ttu-id="da32e-131">Compruebe que tenemos un usuario válido y llama o para notificar el estado a la página de contenido `microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()` de la pestaña principal.</span><span class="sxs-lookup"><span data-stu-id="da32e-131">Check that we have a valid user and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()` to report status back to your main tab content page.</span></span>

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

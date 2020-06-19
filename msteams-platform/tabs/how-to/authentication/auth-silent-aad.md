---
title: Autenticación silenciosa
description: Describe la autenticación silenciosa
keywords: autenticación de Teams AAD en modo silencioso de SSO
ms.openlocfilehash: b8a5b8cb9328635f5730ca089da29140d0a17ac4
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801454"
---
# <a name="silent-authentication"></a>Autenticación silenciosa

> [!NOTE]
> Para que la autenticación funcione para su pestaña en clientes móviles, debe asegurarse de que está usando al menos la versión 1.4.1 del SDK de Teams para JavaScript.

La autenticación silenciosa en Azure Active Directory (Azure AD) minimiza el número de veces que un usuario necesita escribir sus credenciales de inicio de sesión mediante la actualización silenciosa del token de autenticación. (Para admitir un verdadero inicio de sesión único, vea nuestra [documentación de SSO](~/tabs/how-to/authentication/auth-aad-sso.md))

Si desea mantener el código completamente en el lado cliente, puede usar la biblioteca de [autenticación de Azure Active Directory](/azure/active-directory/develop/active-directory-authentication-libraries) para JavaScript para intentar adquirir un token de acceso de Azure ad de forma silenciosa. Esto significa que es posible que el usuario nunca vea un cuadro de diálogo emergente si ha iniciado sesión recientemente.

Aunque la biblioteca de ADAL.js está optimizada para las aplicaciones de AngularJS, también funciona con aplicaciones de una sola página de JavaScript pura.

> [!NOTE]
> Actualmente, la autenticación silenciosa solo funciona en las pestañas. Todavía no funciona al iniciar sesión desde un bot.

## <a name="how-silent-authentication-works"></a>Cómo funciona la autenticación silenciosa

La biblioteca de ADAL.js crea un iframe oculto para OAuth 2,0 el flujo de concesión implícito, pero especifica que `prompt=none` Azure ad nunca muestre la página de inicio de sesión. Si se requiere la interacción del usuario porque el usuario tiene que iniciar sesión o conceder acceso a la aplicación, Azure AD devolverá inmediatamente un error que ADAL.js, a continuación, informa a la aplicación. En este punto, la aplicación puede mostrar un botón de inicio de sesión si es necesario.

## <a name="how-to-do-silent-authentication"></a>Cómo realizar la autenticación silenciosa

El código de este artículo procede de la aplicación de ejemplo de Microsoft Teams de ejemplo de [autenticación de Microsoft Teams (nodo)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node).

### <a name="include-and-configure-adal"></a>incluir y configurar ADAL

Incluya la biblioteca de ADAL.js en las páginas de pestañas y configure ADAL con el identificador de cliente y la dirección URL de redireccionamiento:

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

### <a name="get-the-user-context"></a>Obtener el contexto de usuario

En la página contenido de la pestaña, llame `microsoftTeams.getContext()` a para obtener una sugerencia de inicio de sesión para el usuario actual. Se usará como login_hint en la llamada a Azure AD.

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

### <a name="authenticate"></a>Autenticar

Si ADAL tiene un token no expirado almacenado en caché para el usuario, úselo. De lo contrario, intente obtener un token silenciosamente llamando a `acquireToken(resource, callback)` . ADAL.js llamará a la función de devolución de llamada con el token solicitado o un error si se produce un error en la autenticación.

Si recibe un error en la función de devolución de llamada, muestre un botón de inicio de sesión y vuelva a un inicio de sesión explícito.

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

### <a name="process-the-return-value"></a>Procesar el valor devuelto

Deje que ADAL.js se encargue de analizar el resultado de Azure AD llamando a `AuthenticationContext.handleWindowCallback(hash)` la página de devolución de llamada de inicio de sesión.

Compruebe que tenemos un usuario válido y llame `microsoftTeams.authentication.notifySuccess()` o `microsoftTeams.authentication.notifyFailure()` para informar del estado a la página de contenido de la ficha principal.

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

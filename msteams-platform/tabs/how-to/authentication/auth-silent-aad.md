---
title: Autenticación silenciosa
description: Describe la autenticación silenciosa
ms.topic: conceptual
keywords: AAD silencioso de SSO de autenticación de teams
ms.openlocfilehash: db8409cd4a6edface6d5dc3b3de6698852eaaa24
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449231"
---
# <a name="silent-authentication"></a>Autenticación silenciosa

> [!NOTE]
> Para que la autenticación funcione para su pestaña en clientes móviles, asegúrese de que está usando al menos la versión 1.4.1 del SDK de JavaScript de Teams.

La autenticación silenciosa en Azure Active Directory (AAD) minimiza el número de veces que un usuario escribe sus credenciales de inicio de sesión actualizando silenciosamente el token de autenticación. Para obtener soporte para el inicio de sesión único verdadero, vea [la documentación de SSO](~/tabs/how-to/authentication/auth-aad-sso.md).

Si desea mantener el código completamente del lado cliente, puede usar la biblioteca de autenticación de [AAD](/azure/active-directory/develop/active-directory-authentication-libraries) para JavaScript para obtener un token de acceso de AAD de forma silenciosa. Si el usuario ha iniciado sesión recientemente, nunca verá un cuadro de diálogo emergente.

Aunque la biblioteca ADAL.js está optimizada para aplicaciones angularJS, también funciona con aplicaciones de página única de JavaScript puras.

> [!NOTE]
> Actualmente, la autenticación silenciosa solo funciona para las pestañas. No funciona al iniciar sesión desde un bot.

## <a name="how-silent-authentication-works"></a>Cómo funciona la autenticación silenciosa

La ADAL.js crea un iframe oculto para el flujo de concesión implícito de OAuth 2.0. Pero la biblioteca especifica `prompt=none` , por lo que Azure AD nunca muestra la página de inicio de sesión. Si la interacción del usuario es necesaria porque el usuario necesita iniciar sesión o conceder acceso a la aplicación, AAD devuelve inmediatamente un error que ADAL.js informes a la aplicación. En este punto, la aplicación puede mostrar un botón de inicio de sesión si es necesario.

## <a name="how-to-do-silent-authentication"></a>Cómo realizar la autenticación silenciosa

El código de este artículo proviene de la aplicación de ejemplo de Teams que es el nodo de ejemplo [de autenticación de Teams](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs).

### <a name="include-and-configure-adal"></a>incluir y configurar ADAL

Incluya la biblioteca ADAL.js en las páginas de pestañas y configure ADAL con el identificador de cliente y la dirección URL de redireccionamiento:

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

En la página de contenido de la pestaña, llama para obtener una sugerencia de `microsoftTeams.getContext()` inicio de sesión para el usuario actual. Esto se usa como loginHint en la llamada a AAD.

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

Si ADAL tiene un token no explorado almacenado en caché para el usuario, use el token. Como alternativa, intente obtener un token de forma silenciosa llamando a `acquireToken(resource, callback)` . ADAL.js llamará a la función de devolución de llamada con el token solicitado o dará un error si se produce un error en la autenticación.

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

ADAL.js analiza el resultado de AAD llamando a la página de devolución `AuthenticationContext.handleWindowCallback(hash)` de llamada de inicio de sesión.

Compruebe que tiene un usuario válido y llame o para notificar el estado a la página de contenido `microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()` de la pestaña principal.

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

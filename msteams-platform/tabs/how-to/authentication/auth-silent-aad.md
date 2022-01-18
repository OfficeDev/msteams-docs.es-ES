---
title: Autenticación silenciosa
description: Describe autenticación silenciosa, inicio de sesión único, Azure Active Directory para pestañas
ms.topic: conceptual
ms.localizationpriority: medium
keywords: ficha de inicio de sesión Azure AD autenticación de teams
ms.openlocfilehash: bf50f1840996371292b94ef6d3b2f16d5377a3f9
ms.sourcegitcommit: 25a33b31cc56c05169fc52c65d44c65c601aefef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/14/2022
ms.locfileid: "62043220"
---
# <a name="silent-authentication"></a>Autenticación silenciosa

> [!IMPORTANT]
> El soporte técnico y el desarrollo de Microsoft para la Biblioteca de autenticación de Active Directory (ADAL), incluidas las correcciones de seguridad, finaliza el 30 de junio de **2022**. Actualice las aplicaciones para que usen la Biblioteca de autenticación de Microsoft (MSAL) para seguir recibiendo soporte técnico. Vea [Migrar aplicaciones a la Biblioteca de autenticación de Microsoft (MSAL).](/azure/active-directory/develop/msal-migration)

> [!NOTE]
> Para que la autenticación funcione para su pestaña en clientes móviles, asegúrese de que está usando Teams SDK de JavaScript versión 1.4.1 o posterior.

La autenticación silenciosa Azure Active Directory minimiza el número de veces que un usuario escribe sus credenciales actualizando silenciosamente el token de autenticación. Para obtener soporte para el inicio de sesión único verdadero, vea [la documentación de SSO](~/tabs/how-to/authentication/auth-aad-sso.md).

Para mantener el lado cliente de código, use la biblioteca de autenticación Azure AD [de](/azure/active-directory/develop/active-directory-authentication-libraries) JavaScript para obtener un token de acceso Azure AD de forma silenciosa. Si el usuario ha iniciado sesión recientemente, no verá un cuadro de diálogo emergente.

Aunque la biblioteca de autenticación de Active Directory está optimizada para aplicaciones angularJS, también funciona con aplicaciones de página única (SPA) de JavaScript.

> [!NOTE]
> Actualmente, la autenticación silenciosa solo funciona para las pestañas. No funciona al iniciar sesión desde un bot.

## <a name="how-silent-authentication-works"></a>Cómo funciona la autenticación silenciosa

La biblioteca de autenticación de Active Directory crea un iframe oculto para el flujo de concesión implícito de OAuth 2.0. Pero la biblioteca especifica `prompt=none` , por lo Azure AD no muestra la página de inicio de sesión. La interacción del usuario puede ser necesaria si el usuario necesita iniciar sesión o conceder acceso a la aplicación. Si es necesaria la interacción del usuario, Azure AD devuelve un error que la biblioteca informa a la aplicación. Si es necesario, la aplicación ahora puede mostrar una opción de inicio de sesión.

## <a name="how-to-do-silent-authentication"></a>Cómo realizar la autenticación silenciosa

El código de este artículo proviene de la Teams de ejemplo que se Teams [de ejemplo de autenticación.](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs)

[Inicie la pestaña configurable de autenticación](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) silenciosa y sencilla Azure AD y siga las instrucciones para ejecutar el ejemplo en el equipo local.

### <a name="include-and-configure-active-directory-authentication-library"></a>Incluir y configurar la biblioteca de autenticación de Active Directory

Incluya la biblioteca de autenticación de Active Directory en las páginas de pestañas y configure la biblioteca con el id. de cliente y la dirección URL de redireccionamiento:

```html
<script src="https://secure.aadcdn.microsoftonline-p.com/lib/1.0.15/js/adal.min.js" integrity="sha384-lIk8T3uMxKqXQVVfFbiw0K/Nq+kt1P3NtGt/pNexiDby2rKU6xnDY8p16gIwKqgI" crossorigin="anonymous"></script>
<script type="text/javascript">
    // Active Directory Authentication Library configuration
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

En la página de contenido de la pestaña, llama para obtener una sugerencia de inicio de `microsoftTeams.getContext()` sesión para el usuario actual. La sugerencia se usa como una `loginHint` en la llamada a Azure AD.

```javascript
// Set up extra query parameters for Active Directory Authentication Library
// - openid and profile scope adds profile information to the id_token
// - login_hint provides the expected user name
if (loginHint) {
    config.extraQueryParameter = "scope=openid+profile&login_hint=" + encodeURIComponent(loginHint);
} else {
    config.extraQueryParameter = "scope=openid+profile";
}
```

### <a name="authenticate"></a>Autenticar

Si la biblioteca de autenticación de Active Directory tiene un token no explorado almacenado en caché para el usuario, use el token. Como alternativa, llama `acquireToken(resource, callback)` para recibir silenciosamente un token. La biblioteca llama a una función de devolución de llamada con el token solicitado o genera un error si se produce un error en la autenticación.

Si obtiene un error en la función de devolución de llamada, muestre y use una opción de inicio de sesión explícita.

```javascript
let authContext = new AuthenticationContext(config); // from Active Directory Authentication Library
// See if there is a cached user and it matches the expected user
let user = authContext.getCachedUser();
if (user) {
    if (user.profile.oid !== userObjectId) {
        // User doesn't match, clear the cache
        authContext.clearCache();
    }
}

// In this example we are getting an id token (which Active Directory Authentication Library returns if we ask for resource = clientId)
authContext.acquireToken(config.clientId, function (errDesc, token, err, tokenType) {
    if (token) {
        // Make sure Active Directory Authentication Library gave us an ID token
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

La biblioteca de autenticación de Active Directory analiza el resultado de Azure AD llamando a la página de devolución `AuthenticationContext.handleWindowCallback(hash)` de llamada de inicio de sesión.

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

### <a name="handle-the-sign-out-flow"></a>Controlar el flujo de salida

Use el siguiente código para controlar el flujo de salida en Azure AD autenticación:

> [!NOTE]
> Al cerrar sesión desde Teams o bot, se borra la sesión actual.

```javascript
function logout() {
localStorage.clear();
window.location.href = "@Url.Action("<<Action Name>>", "<<Controller Name>>")";
}
```

## <a name="see-also"></a>Vea también

* [Configurar proveedores de identidades para que usen Azure AD](../../../concepts/authentication/configure-identity-provider.md)
* [Información sobre la Biblioteca de autenticación de Microsoft (MSAL)](/azure/active-directory/develop/msal-overview)

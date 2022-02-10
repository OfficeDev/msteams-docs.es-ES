---
title: Autenticación silenciosa
description: Describe la autenticación silenciosa, inicio de sesión único, Microsoft Azure Active Directory (Azure AD) para pestañas
ms.topic: conceptual
ms.localizationpriority: medium
keywords: autenticación de teams sso silent Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: 700f0d3f752beb7b09b76a805f2bbcd7adf82fb9
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518467"
---
# <a name="silent-authentication"></a>Autenticación silenciosa

> [!IMPORTANT]
> El soporte técnico y el desarrollo de Microsoft para la Biblioteca de autenticación de Active Directory (ADAL), incluidas las correcciones de seguridad, finaliza el 30 de junio de **2022**. Actualice las aplicaciones para que usen la Biblioteca de autenticación de Microsoft (MSAL) para seguir recibiendo soporte técnico. Consulte [Migrar aplicaciones a la Biblioteca de autenticación de Microsoft (MSAL).](/azure/active-directory/develop/msal-migration)

> [!NOTE]
> Para que la autenticación funcione para su pestaña en clientes móviles, asegúrese de que está usando Teams SDK de JavaScript versión 1.4.1 o posterior.

La autenticación silenciosa Microsoft Azure Active Directory (Azure AD) minimiza el número de veces que un usuario escribe sus credenciales actualizando silenciosamente el token de autenticación. Para obtener compatibilidad con el inicio de sesión único verdadero, consulte [la documentación de SSO](~/tabs/how-to/authentication/auth-aad-sso.md).

Para mantener el lado cliente de código, use la biblioteca de autenticación Microsoft Azure Active Directory [(Azure AD)](/azure/active-directory/develop/active-directory-authentication-libraries) para JavaScript para obtener un token de acceso Microsoft Azure Active Directory (Azure AD) de forma silenciosa. Si el usuario ha iniciado sesión recientemente, no verá un cuadro de diálogo emergente.

Aunque la biblioteca de autenticación de Active Directory está optimizada para aplicaciones angularJS, también funciona con aplicaciones de página única (SPA) de JavaScript.

> [!NOTE]
> Actualmente, la autenticación silenciosa solo funciona para las pestañas. No funciona al iniciar sesión desde un bot.

## <a name="how-silent-authentication-works"></a>Cómo funciona la autenticación silenciosa

La biblioteca de autenticación de Active Directory crea un iframe oculto para el flujo de concesión implícito de OAuth 2.0. Pero la biblioteca especifica `prompt=none`, por lo que Microsoft Azure Active Directory (Azure AD)no muestra la página de inicio de sesión. La interacción del usuario puede ser necesaria si el usuario necesita iniciar sesión o conceder acceso a la aplicación. Si es necesaria la interacción del usuario, Microsoft Azure Active Directory (Azure AD) devuelve un error que la biblioteca informa a la aplicación. Si es necesario, la aplicación ahora puede mostrar una opción de inicio de sesión.

## <a name="how-to-do-silent-authentication"></a>Cómo realizar la autenticación silenciosa

El código de este artículo proviene de la Teams de ejemplo que se Teams [de ejemplo de autenticación](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs).

[Inicie la pestaña configurable de](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) autenticación silenciosa y sencilla Microsoft Azure Active Directory (Azure AD) y siga las instrucciones para ejecutar el ejemplo en el equipo local.

### <a name="include-and-configure-active-directory-authentication-library"></a>Incluir y configurar la biblioteca de autenticación de Active Directory

Incluya la biblioteca de autenticación de Active Directory en las páginas de pestañas y configure la biblioteca con el id. de cliente y la dirección URL de redireccionamiento:

```html
<script src="https://secure.aadcdn.microsoftonline-p.com/lib/1.0.15/js/adal.min.js" integrity="sha384-lIk8T3uMxKqXQVVfFbiw0K/Nq+kt1P3NtGt/pNexiDby2rKU6xnDY8p16gIwKqgI" crossorigin="anonymous"></script>
<script type="text/javascript">
    // Active Directory Authentication Library configuration
    let config = {
        clientId: "YOUR_APP_ID_HERE",
        // redirectUri must be in the list of redirect URLs for the Microsoft Azure Active Directory (Azure AD) app
        redirectUri: window.location.origin + "/tab-auth/silent-end",
        cacheLocation: "localStorage",
        navigateToLoginRequestUrl: false,
    };
</script>
```

### <a name="get-the-user-context"></a>Obtener el contexto de usuario

En la página de contenido de la pestaña, llama `microsoftTeams.getContext()` para obtener una sugerencia de inicio de sesión para el usuario actual. La sugerencia se usa como una en `loginHint` la llamada a Microsoft Azure Active Directory (Azure AD).

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

Si la biblioteca de autenticación de Active Directory tiene un token no explorado almacenado en caché para el usuario, use el token. Como alternativa, llama para `acquireToken(resource, callback)` recibir silenciosamente un token. La biblioteca llama a una función de devolución de llamada con el token solicitado o genera un error si se produce un error en la autenticación.

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

La biblioteca de autenticación de Active Directory analiza el resultado de Microsoft Azure Active Directory (Azure AD) `AuthenticationContext.handleWindowCallback(hash)` llamando a la página de devolución de llamada de inicio de sesión.

Compruebe que tiene un usuario válido y llame `microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()` o para notificar el estado a la página de contenido de la pestaña principal.

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

Use el siguiente código para controlar el flujo de salida en Microsoft Azure Active Directory (Azure AD):

> [!NOTE]
> Al cerrar sesión desde Teams o bot, se borra la sesión actual.

```javascript
function logout() {
localStorage.clear();
window.location.href = "@Url.Action("<<Action Name>>", "<<Controller Name>>")";
}
```

## <a name="see-also"></a>Vea también

* [Configurar proveedores de identidades para Microsoft Azure Active Directory (Azure AD)](../../../concepts/authentication/configure-identity-provider.md)
* [Información sobre la Biblioteca de autenticación de Microsoft (MSAL)](/azure/active-directory/develop/msal-overview)

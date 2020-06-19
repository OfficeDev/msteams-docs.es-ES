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
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a>Autenticar a un usuario en una pestaña de Microsoft Teams

> [!Note]
> Para que la autenticación funcione para su pestaña en clientes móviles, debe asegurarse de que está usando la versión 1.4.1 o posterior del SDK de Teams de JavaScript.

Hay muchos servicios que puede que desee consumir dentro de la aplicación de Teams y la mayoría de esos servicios requieren autenticación y autorización para obtener acceso al servicio. Los servicios incluyen Facebook, Twitter y los equipos del curso. Los usuarios de Microsoft Teams tienen información de Perfil de usuario almacenada en Azure Active Directory (Azure AD) con Microsoft Graph y este artículo se centrará en la autenticación mediante Azure AD para obtener acceso a esta información.

OAuth 2,0 es un estándar abierto para la autenticación que usa Azure AD y muchos otros proveedores de servicios. La comprensión de OAuth 2,0 es un requisito previo para trabajar con la autenticación en Microsoft Teams y Azure AD. En los ejemplos siguientes se usa el flujo de concesión implícita de OAuth 2,0 con el objetivo de leer eventualmente la información de perfil del usuario de Azure AD y Microsoft Graph.

El código de este artículo procede de la aplicación de ejemplo de Teams de [Microsoft Teams, ejemplo de autenticación de pestañas de Microsoft Teams (nodo)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node). Contiene una pestaña estática que solicita un token de acceso para Microsoft Graph y muestra la información básica del perfil del usuario actual de Azure AD.

Para obtener información general sobre el flujo de autenticación de las pestañas, vea el tema [flujo de autenticación en las pestañas](~/tabs/how-to/authentication/auth-flow-tab.md).

El flujo de autenticación en las pestañas difiere ligeramente del flujo de autenticación en los bots.

## <a name="configuring-identity-providers"></a>Configuración de proveedores de identidad

Vea el tema [configuración de proveedores de identidades](~/concepts/authentication/configure-identity-provider.md) para obtener pasos detallados sobre cómo configurar las direcciones URL de redireccionamiento de devolución de llamada de OAuth 2,0 al usar Azure Active Directory como proveedor de identidades.

## <a name="initiate-authentication-flow"></a>Iniciar el flujo de autenticación

El flujo de autenticación debe activarse mediante una acción del usuario. No debe abrir la ventana emergente de autenticación automáticamente porque es probable que desencadene el bloqueador de ventanas emergentes del explorador, así como confundir al usuario.

Agregue un botón a la página de configuración o de contenido para permitir que el usuario inicie sesión cuando sea necesario. Esto se puede hacer en la página de [configuración](~/tabs/how-to/create-tab-pages/configuration-page.md) de pestañas o en cualquier página de [contenido](~/tabs/how-to/create-tab-pages/content-page.md) .

Azure AD, al igual que la mayoría de los proveedores de identidades, no permite que su contenido se coloque en un iframe. Esto significa que tendrá que agregar una página emergente para hospedar el proveedor de identidades. En el siguiente ejemplo, esta página es `/tab-auth/simple-start` . Use la `microsoftTeams.authenticate()` función del SDK del cliente de Microsoft Teams para iniciar esta página cuando se selecciona el botón.

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

### <a name="notes"></a>Notas

* La dirección URL a la que se pasa `microsoftTeams.authentication.authenticate()` es la página de inicio del flujo de autenticación. En este ejemplo es `/tab-auth/simple-start` . Esto debe coincidir con lo registrado en el [portal de registro de aplicaciones de Azure ad](https://apps.dev.microsoft.com).

* El flujo de autenticación debe iniciarse en una página que se encuentra en el dominio. Este dominio también debe aparecer en la [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) sección del manifiesto. Si no lo hace, se producirá un elemento emergente vacío.

* Si no se usa `microsoftTeams.authentication.authenticate()` , se producirá un problema con el elemento emergente que no se cerrará al final del proceso de inicio de sesión.

## <a name="navigate-to-the-authorization-page-from-your-popup-page"></a>Ir a la página autorización desde la página emergente

Cuando se muestra la página emergente ( `/tab-auth/simple-start` ), se ejecuta el siguiente código. El objetivo principal de esta página es redirigir al proveedor de identidades para que el usuario pueda iniciar sesión. Esta redirección puede realizarse en el lado servidor con HTTP 302, pero en este caso se realiza en el lado cliente con una llamada a `window.location.assign()` . Esto también permite que `microsoftTeams.getContext()` se use para recuperar información de sugerencias que se puede pasar a Azure ad.

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

Una vez que el usuario completa la autorización, se redirige al usuario a la página de devolución de llamada que especificó para la aplicación en `/tab-auth/simple-end` .

### <a name="notes"></a>Notas

* Consulte [obtener información de contexto del usuario](~/tabs/how-to/access-teams-context.md) para obtener ayuda para crear solicitudes de autenticación y direcciones URL. Por ejemplo, puede usar el nombre de inicio de sesión del usuario como el valor para el inicio de `login_hint` sesión de Azure ad, lo que significa que el usuario podría tener que escribir menos. Recuerde que no debe usar este contexto directamente como prueba de identidad, ya que un atacante podría cargar la página en un explorador malintencionado y proporcionarla con cualquier información que desee.
* Aunque el contexto de la pestaña proporciona información útil acerca del usuario, no use esta información para autenticar al usuario si los obtiene como parámetros URL en la dirección URL de contenido de la pestaña o mediante una llamada a la `microsoftTeams.getContext()` función en el SDK del cliente de Microsoft Teams. Un actor malintencionado podría invocar la dirección URL de contenido de pestaña con sus propios parámetros y una página web que suplanta a Microsoft Teams podría cargar la URL de contenido de la pestaña en un iframe y devolver sus propios datos a la `getContext()` función. Debe tratar la información relacionada con la identidad en el contexto de pestañas simplemente como sugerencias y validarlas antes de usarlas.
* El `state` parámetro se usa para confirmar que el servicio que llama al URI de devolución de llamada es el servicio al que ha llamado. Si el `state` parámetro de la devolución de llamada no coincide con el parámetro enviado durante la llamada, la llamada a la devolución no se comprueba y debe finalizarse.
* No es necesario incluir el dominio del proveedor de identidades en la `validDomains` lista de la manifest.jsdel archivo de la aplicación.

## <a name="the-callback-page"></a>La página de devolución de llamada

En la última sección, llamó al servicio de autorización de Azure AD y pasó la información de usuario y de la aplicación para que Azure AD pudiera presentar al usuario su propia experiencia de autorización de monolíticas. La aplicación no tiene control sobre lo que sucede en esta experiencia. Todo lo que sabe es lo que se devuelve cuando Azure AD llama a la página de devolución de llamada que ha proporcionado ( `/tab-auth/simple-end` ).

En esta página, debe determinar si se ha realizado correctamente o no el error en función de la información devuelta por Azure AD y llamar a `microsoftTeams.authentication.notifySuccess()` o `microsoftTeams.authentication.notifyFailure()` . Si el inicio de sesión tuvo éxito, tendrá acceso a los recursos de servicio.

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

Este código analiza los pares clave-valor recibidos de Azure AD `window.location.hash` con la `getHashParameters()` función auxiliar. Si encuentra un `access_token` , y el `state` valor es el mismo que el proporcionado al principio del flujo de autenticación, devuelve el token de acceso a la pestaña mediante una llamada `notifySuccess()` ; en caso contrario, informa de un error `notifyFailure()` .

### <a name="notes"></a>Notas

`NotifyFailure()`tiene los siguientes motivos de error predefinidos:

* `CancelledByUser`el usuario ha cerrado la ventana del elemento emergente antes de completar el flujo de autenticación.
* `FailedToOpenWindow`no se pudo abrir la ventana emergente. Cuando se ejecuta Microsoft Teams en un explorador, suele significar que la ventana fue bloqueada por un bloqueador de elementos emergentes.

Si se ejecuta correctamente, puede actualizar o volver a cargar la página y mostrar contenido relevante para el usuario autenticado ahora. Si se produce un error en la autenticación, mostrar un mensaje de error.

La aplicación puede establecer su propia cookie de sesión para que el usuario no tenga que volver a iniciarla cuando vuelva a su pestaña en el dispositivo actual.

> [!NOTE]
> Chrome 80, programado para su lanzamiento en principios de 2020, presenta nuevos valores de cookies e impone directivas de cookies de forma predeterminada. Se recomienda establecer el uso previsto para las cookies en lugar de basarse en el comportamiento predeterminado del explorador. *Consulte* [SameSite cookie Attribute (2020 Update)](../../../resources/samesite-cookie-update.md).

Para obtener más información sobre el inicio de sesión único (SSO), vea el artículo [autenticación silenciosa](~/tabs/how-to/authentication/auth-silent-AAD.md).

## <a name="samples"></a>Ejemplos

Para ver el código de ejemplo que muestra el proceso de autenticación de pestañas con Azure AD, consulte:

* [Ejemplo de autenticación de pestañas de Microsoft Teams (nodo)](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)

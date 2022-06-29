---
title: Configuración de la autenticación de OAuth de terceros
description: En este artículo, aprenderá las pestañas de autenticación de Teams Microsoft Azure AD, la autenticación en Teams y cómo usarla en pestañas.
ms.topic: how-to
ms.localizationpriority: medium
ms.openlocfilehash: f3a3e9d4ae848459c4804895aa2f28a66868ddb0
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503469"
---
# <a name="configure-third-party-oauth-idp-authentication"></a>Configuración de la autenticación de IdP de OAuth de terceros

> [!Note]
> Para que la autenticación funcione para la pestaña en clientes móviles, asegúrese de que usa la versión 1.4.1 o posterior del SDK de JavaScript de Teams.

Es posible que desee consumir muchos servicios dentro de la aplicación de Teams, y la mayoría de esos servicios requieren autenticación y autorización para obtener acceso al servicio. Los servicios incluyen Facebook, Twitter y Teams.
La información de perfil de usuario de Teams se almacena en Azure AD mediante Microsoft Graph y este artículo se centrará en la autenticación mediante Azure AD para obtener acceso a esta información.

OAuth 2.0 es un estándar abierto para la autenticación usado por Azure Active Directory (Azure AD) y muchos otros proveedores de identidad. Comprender OAuth 2.0 es un requisito previo para trabajar con la autenticación en Teams y Azure AD. En los ejemplos siguientes se usa el flujo de concesión implícita de OAuth 2.0. Lee la información del perfil del usuario de Azure AD y Microsoft Graph.

El código de este artículo procede de la aplicación de ejemplo de Teams [Ejemplo de autenticación de tabulación de Microsoft Teams (Node)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node). Contiene una pestaña estática que solicita un token de acceso para Microsoft Graph y muestra la información básica del perfil del usuario actual de Azure AD.

Para obtener información general sobre el flujo de autenticación de las pestañas, consulte [Flujo de autenticación en pestañas](~/tabs/how-to/authentication/auth-flow-tab.md).

El flujo de autenticación en pestañas difiere del flujo de autenticación en los bots.

## <a name="configure-your-app-to-use-azure-ad-as-an-identity-provider"></a>Configuración de la aplicación para usar Azure AD como proveedor de identidades

Los proveedores de identidades que admiten OAuth 2.0 no autentican solicitudes de aplicaciones desconocidas. Debe registrar las aplicaciones con antelación. Para ello con Azure AD, siga estos pasos:

1. Abra el [Portal de registro de aplicaciones](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).

2. Seleccione la aplicación para ver sus propiedades o seleccione el botón "Nuevo registro". Busque la sección **URI de redirección** de la aplicación.

3. Seleccione **Web** en el menú desplegable. Actualice la dirección URL al punto de conexión de autenticación. Para las aplicaciones de ejemplo TypeScript/Node.js y C# en GitHub, las direcciones URL de redireccionamiento serán similares a las siguientes:

    URL de redireccionamiento`https://<hostname>/bot-auth/simple-start`

Reemplace por `<hostname>` el host real. Este host puede ser un sitio de hospedaje dedicado, como Azure, Glitch o un túnel ngrok a localhost en la máquina de desarrollo, como `abcd1234.ngrok.io`. Si no tiene esta información, asegúrese de que ha completado o hospedado la aplicación (o la aplicación de ejemplo). Reanude este proceso cuando tenga esta información.

> [!NOTE]
> Puede elegir cualquier proveedor de OAuth de terceros, como LinkedIn, Google y otros. El proceso para habilitar la autenticación para estos proveedores es similar al uso de Azure AD como proveedor de OAuth de terceros. Para obtener más información sobre el uso de cualquier proveedor de OAuth de terceros, visite el sitio web del proveedor en particular.

## <a name="initiate-authentication-flow"></a>Iniciar el flujo de autenticación

El flujo de autenticación debe desencadenarse mediante una acción del usuario. No debe abrir el elemento emergente de autenticación automáticamente porque es probable que desencadene el bloqueador emergente del explorador y confunda al usuario.

Agregue un botón a la página de configuración o contenido para permitir que el usuario inicie sesión cuando sea necesario. Esto se puede hacer en la página de [configuración](~/tabs/how-to/create-tab-pages/configuration-page.md) de la pestaña o en cualquier página de [contenido](~/tabs/how-to/create-tab-pages/content-page.md).

Azure AD, al igual que la mayoría de los proveedores de identidades, no permite que su contenido se coloque en .`iframe` Esto significa que tendrá que agregar una página emergente para hospedar el proveedor de identidades. En el ejemplo siguiente, esta página es `/tab-auth/simple-start`. Use la `microsoftTeams.authenticate()` función del SDK de cliente de Microsoft Teams para iniciar esta página cuando se seleccione el botón.

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

* La dirección URL a la que se pasa `microsoftTeams.authentication.authenticate()` es la página de inicio del flujo de autenticación. En este ejemplo que es `/tab-auth/simple-start`. Debe coincidir con lo que registró en el [portal de registro de aplicaciones de Azure AD](https://apps.dev.microsoft.com).

* El flujo de autenticación debe iniciarse en una página que esté en el dominio. Este dominio también debe aparecer en la sección [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) del manifiesto. Si no lo hace, se producirá un elemento emergente vacío.

* Si no se usa `microsoftTeams.authentication.authenticate()` , el elemento emergente no se cerrará al final del proceso de inicio de sesión.

## <a name="navigate-to-the-authorization-page-from-your-pop-up-page"></a>Vaya a la página de autorización desde la página emergente.

Cuando se muestra la página emergente (`/tab-auth/simple-start`) se ejecuta el código siguiente. El objetivo principal de esta página es redirigir al proveedor de identidades para que el usuario pueda iniciar sesión. Esta redirección podría realizarse en el lado servidor mediante HTTP 302, pero en este caso se hace en el lado cliente mediante con una llamada a `window.location.assign()`. Esto también permite usar `microsoftTeams.getContext()` para recuperar información de sugerencias, que se puede pasar a Azure AD.

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
        scope: "https://graph.microsoft.com/User.Read openid",
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

Una vez que el usuario completa la autorización, se redirige al usuario a la página de devolución de llamada que especificó para la aplicación en `/tab-auth/simple-end`.

### <a name="notes"></a>Notas

* Consulte [Obtención de información de contexto de usuario](~/tabs/how-to/access-teams-context.md) para obtener ayuda para crear solicitudes de autenticación y direcciones URL. Por ejemplo, puede usar el nombre de inicio de sesión del usuario como valor `login_hint` para el inicio de sesión de Azure AD, lo que significa que puede que el usuario tenga que escribir menos. Recuerde que no debe usar este contexto directamente como prueba de identidad, ya que un atacante podría cargar la página en un explorador malintencionado y proporcionarle toda la información que desee.
* Aunque el contexto de pestaña proporciona información útil sobre el usuario, no use esta información para autenticar al usuario, ya sea como parámetros de dirección URL en la dirección URL del contenido de la pestaña o llamando a la función `microsoftTeams.getContext()` en el SDK de cliente de Microsoft Teams. Un actor malintencionado podría invocar la dirección URL de contenido de la pestaña con sus propios parámetros y una página web que suplanta Microsoft Teams podría cargar la dirección URL de contenido de la pestaña en un iframe y devolver sus propios datos a la función `getContext()`. Debe tratar la información relacionada con la identidad en el contexto de tabulación simplemente como sugerencias y validarla antes de usarla.
* El parámetro `state` se usa para confirmar que el servicio que llama al URI de devolución de llamada es el servicio al que llamó. Si el `state` parámetro de la devolución de llamada no coincide con el parámetro que envió durante la llamada, la llamada de devolución no se comprueba y debe finalizarse.
* No es necesario incluir el dominio del proveedor de identidades en la `validDomains` lista en el archivo manifest.json de la aplicación.

## <a name="the-callback-page"></a>Página de devolución de llamada

En la última sección, llamó al servicio de autorización de Azure AD y pasó información de usuario y aplicación para que Azure AD pudiera presentar al usuario su propia experiencia de autorización monolítica. La aplicación no tiene control sobre lo que sucede en esta experiencia. Todo lo que sabe es lo que se devuelve cuando Azure AD llama a la página de devolución de llamada que proporcionó (`/tab-auth/simple-end`).

En esta página, debe determinar si se ha realizado correctamente o no en función de la información devuelta por Azure AD y llamar a `microsoftTeams.authentication.notifySuccess()` o `microsoftTeams.authentication.notifyFailure()`. Si el inicio de sesión se realizó correctamente, tendrá acceso a los recursos del servicio.

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

Este código analiza los pares clave-valor recibidos de Azure AD en el uso `window.location.hash` de la función auxiliar `getHashParameters()`. Si encuentra un `access_token` y el valor `state` es el mismo que el proporcionado al principio del flujo de autenticación, devuelve el token de acceso a la pestaña llamando a `notifySuccess()`; de lo contrario, notifica un error con `notifyFailure()`.

### <a name="notes"></a>Notas

`NotifyFailure()` tiene los siguientes motivos de error predefinidos:

* `CancelledByUser` el usuario cerró la ventana emergente antes de completar el flujo de autenticación.
* `FailedToOpenWindow` no se pudo abrir la ventana emergente. Cuando Microsoft Teams se ejecuta en un explorador, este error indica que la ventana fue bloqueada por el bloqueador de elementos emergentes del explorador.

Si se ejecuta correctamente, puede actualizar o volver a cargar la página y mostrar contenido relevante para el usuario ahora autenticado. Si se produce un error en la autenticación, muestra un mensaje de error.

La aplicación puede establecer su propia cookie de sesión para que el usuario no tenga que volver a iniciar sesión cuando vuelva a la pestaña del dispositivo actual.

> [!NOTE]
>
> * Chrome 80, programado para lanzarse a principios de 2020, presenta nuevos valores de cookies e impone directivas de cookies de forma predeterminada. Se recomienda establecer el uso previsto para las cookies en lugar de basarse en el comportamiento predeterminado del explorador. *Consulte* [Atributo de cookies SameSite (actualización de 2020)](../../../resources/samesite-cookie-update.md).
> * Para obtener el token correcto para usuarios gratuitos e invitados en Microsoft Teams, es importante que las aplicaciones usen el punto de conexión específico del inquilino `https://login.microsoftonline.com/**{tenantId}**`. Puede obtener tenantId desde el mensaje del bot o el contexto de la pestaña. Si las aplicaciones usan `https://login.microsoftonline.com/common`, los usuarios obtendrán tokens incorrectos e iniciarán sesión en el inquilino “home” en lugar del inquilino en el que han iniciado sesión actualmente.

Para obtener más información sobre Single Sign-On (SSO), consulte el artículo [Autenticación silenciosa](~/tabs/how-to/authentication/auth-silent-AAD.md).

## <a name="code-sample"></a>Ejemplo de código

Código de ejemplo que muestra el proceso de autenticación de tabulación mediante Azure AD:

| **Ejemplo de nombre** | **description** | **.NET** | **Node.js** |
|-----------------|-----------------|-------------|
| Crear una pestaña de Microsoft Teams que use la autenticación SSO | Proceso de autenticación de tabulación mediante Azure AD. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs) |

## <a name="see-also"></a>Consulte también

* [Planear la autenticación de usuarios](../../../concepts/design/understand-use-cases.md)
* [Diseñar la pestaña para Microsoft Teams](~/tabs/design/tabs.md)
* [Autenticación silenciosa](~/tabs/how-to/authentication/auth-silent-aad.md)
* [Agregar autenticación a la extensión de mensaje](~/messaging-extensions/how-to/add-authentication.md)
* [Compatibilidad con inicio de sesión (SSO) único para bots](~/bots/how-to/authentication/auth-aad-sso-bots.md)

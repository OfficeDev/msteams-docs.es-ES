---
title: Autenticación para pestañas mediante Azure Active Directory
description: Describe la autenticación en Teams y cómo usarla en pestañas
ms.topic: how-to
localization_priority: Normal
keywords: fichas de autenticación de teams AAD
ms.openlocfilehash: 138575ab28280f167c0627731c8219eccb07b7d9
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52629987"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a>Autenticar a un usuario en una Microsoft Teams pestaña

> [!Note]
> Para que la autenticación funcione para su pestaña en clientes móviles, debe asegurarse de que está usando la versión 1.4.1 o posterior del SDK Teams JavaScript.

Es posible que desee usar muchos servicios dentro de la aplicación Teams y la mayoría de esos servicios requieren autenticación y autorización para obtener acceso al servicio. Los servicios incluyen Facebook, Twitter y, por supuesto, Teams. Los usuarios de Teams tienen información de perfil de usuario almacenada en Azure Active Directory (Azure AD) con Microsoft Graph y este artículo se centrará en la autenticación con Azure AD para obtener acceso a esta información.

OAuth 2.0 es un estándar abierto para la autenticación usada por Azure AD y muchos otros proveedores de servicios. Comprender OAuth 2.0 es un requisito previo para trabajar con la autenticación en Teams y Azure AD. Los ejemplos siguientes usan el flujo de concesión implícita de OAuth 2.0 con el objetivo de leer finalmente la información de perfil del usuario de Azure AD y Microsoft Graph.

El código de este artículo proviene de la aplicación Teams ejemplo de Microsoft Teams de autenticación de [pestañas (Node).](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) Contiene una pestaña estática que solicita un token de acceso para Microsoft Graph y muestra la información básica del perfil del usuario actual de Azure AD.

Para obtener información general sobre el flujo de autenticación de las pestañas, vea el tema [Flujo de autenticación en pestañas](~/tabs/how-to/authentication/auth-flow-tab.md).

El flujo de autenticación en las pestañas difiere ligeramente del flujo de autenticación en bots.

## <a name="configuring-identity-providers"></a>Configuración de proveedores de identidades

Consulte el tema [Configurar](~/concepts/authentication/configure-identity-provider.md) proveedores de identidades para obtener pasos detallados sobre cómo configurar las direcciones URL de redireccionamiento de devolución de llamada de OAuth 2.0 al usar Azure Active Directory como proveedor de identidades.

## <a name="initiate-authentication-flow"></a>Iniciar flujo de autenticación

El flujo de autenticación debe desencadenarse mediante una acción del usuario. No debe abrir la ventana emergente de autenticación automáticamente porque es probable que esto desencadene el bloqueador de elementos emergentes del explorador y confunda al usuario.

Agregue un botón a la página de configuración o contenido para permitir que el usuario inicie sesión cuando sea necesario. Esto se puede hacer en la página de configuración [de pestañas](~/tabs/how-to/create-tab-pages/configuration-page.md) o en cualquier [página de](~/tabs/how-to/create-tab-pages/content-page.md) contenido.

Azure AD, como la mayoría de los proveedores de identidades, no permite que su contenido se coloque en un iframe. Esto significa que tendrá que agregar una página emergente para hospedar el proveedor de identidades. En el siguiente ejemplo, esta página es `/tab-auth/simple-start` . Usa la `microsoftTeams.authenticate()` función del SDK Microsoft Teams cliente para iniciar esta página cuando se selecciona el botón.

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

* La dirección URL a la que `microsoftTeams.authentication.authenticate()` se pasa es la página de inicio del flujo de autenticación. En este ejemplo que es `/tab-auth/simple-start` . Esto debe coincidir con lo que registró en el Portal de registro [de aplicaciones de Azure AD](https://apps.dev.microsoft.com).

* El flujo de autenticación debe iniciarse en una página que se encuentra en su dominio. Este dominio también debe aparecer en la [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) sección del manifiesto. Si no lo hace, se mostrará una ventana emergente vacía.

* Si no se usa, se produce un problema con que el elemento emergente no se cierre `microsoftTeams.authentication.authenticate()` al final del proceso de inicio de sesión.

## <a name="navigate-to-the-authorization-page-from-your-popup-page"></a>Navegue a la página de autorización desde la página emergente

Cuando se muestra la página emergente ( `/tab-auth/simple-start` ) se ejecuta el siguiente código. El objetivo principal de esta página es redirigir al proveedor de identidades para que el usuario pueda iniciar sesión. Esta redirección podría realizarse en el lado del servidor mediante HTTP 302, pero en este caso se realiza en el lado cliente mediante una llamada a `window.location.assign()` . Esto también permite `microsoftTeams.getContext()` usarse para recuperar información de sugerencias que se puede pasar a Azure AD.

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

Una vez que el usuario completa la autorización, se redirige al usuario a la página de devolución de llamada que especificó para la aplicación en `/tab-auth/simple-end` .

### <a name="notes"></a>Notas

* Consulte [Obtener información de contexto de usuario](~/tabs/how-to/access-teams-context.md) para obtener ayuda para crear solicitudes de autenticación y direcciones URL. Por ejemplo, puede usar el nombre de inicio de sesión del usuario como valor para el inicio de sesión de Azure AD, lo que significa que es posible que el usuario necesite `login_hint` escribir menos. Recuerde que no debe usar este contexto directamente como prueba de identidad, ya que un atacante podría cargar la página en un explorador malintencionado y proporcionarle la información que desee.
* Aunque el contexto de pestaña proporciona información útil sobre el usuario, no use esta información para autenticar al usuario, ya sea que la obtenga como parámetros de dirección URL en la dirección URL de contenido de la pestaña o llamando a la función en el SDK de cliente de `microsoftTeams.getContext()` Microsoft Teams. Un actor malintencionado podría invocar la dirección URL de contenido de la pestaña con sus propios parámetros y una página web que suplanta Microsoft Teams podría cargar la dirección URL de contenido de la pestaña en un iframe y devolver sus propios datos a la `getContext()` función. Debe tratar la información relacionada con la identidad en el contexto de la pestaña simplemente como sugerencias y validarlas antes de usarlas.
* El parámetro se usa para confirmar que el servicio que llama al URI de devolución de `state` llamada es el servicio al que llamó. Si el parámetro de la devolución de llamada no coincide con el parámetro que envió durante la llamada, la llamada de devolución no se comprueba `state` y debe finalizarse.
* No es necesario incluir el dominio del proveedor de identidades en la lista en el archivo de manifest.js`validDomains` de la aplicación.

## <a name="the-callback-page"></a>La página de devolución de llamada

En la última sección, llamó al servicio de autorización de Azure AD y pasó información de usuario y aplicación para que Azure AD pudiera presentar al usuario su propia experiencia de autorización monolítica. La aplicación no tiene control sobre lo que sucede en esta experiencia. Todo lo que sabe es lo que se devuelve cuando Azure AD llama a la página de devolución de llamada que proporcionó ( `/tab-auth/simple-end` ).

En esta página debe determinar el éxito o error en función de la información devuelta por Azure AD y llamar `microsoftTeams.authentication.notifySuccess()` o `microsoftTeams.authentication.notifyFailure()` . Si el inicio de sesión se ha realizado correctamente, tendrá acceso a los recursos de servicio.

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

Este código analiza los pares clave-valor recibidos de Azure AD `window.location.hash` mediante la `getHashParameters()` función auxiliar. Si encuentra un y el valor es el mismo que el proporcionado al principio del flujo de autenticación, devuelve el token de acceso a la pestaña llamando; de lo contrario, informa de un `access_token` `state` error con `notifySuccess()` `notifyFailure()` .

### <a name="notes"></a>Notas

`NotifyFailure()` tiene los siguientes motivos de error predefinidos:

* `CancelledByUser` el usuario cerró la ventana emergente antes de completar el flujo de autenticación.
* `FailedToOpenWindow` no se pudo abrir la ventana emergente. Al ejecutar Microsoft Teams en un explorador, esto suele significar que un bloqueador emergente bloqueó la ventana.

Si se realiza correctamente, puede actualizar o volver a cargar la página y mostrar contenido relevante para el usuario autenticado ahora. Si se produce un error en la autenticación, muestre un mensaje de error.

La aplicación puede establecer su propia cookie de sesión para que el usuario no tenga que volver a iniciar sesión cuando vuelva a la pestaña en el dispositivo actual.

> [!NOTE]
> Chrome 80, programado para su lanzamiento a principios de 2020, introduce nuevos valores de cookies e impone directivas de cookies de forma predeterminada. Se recomienda establecer el uso previsto para las cookies en lugar de basarse en el comportamiento predeterminado del explorador. *Consulte* [Atributo de cookie SameSite (actualización de 2020).](../../../resources/samesite-cookie-update.md)

>[!NOTE]
>Para obtener el token correcto para Microsoft Teams usuarios invitados y gratuitos, es importante que las aplicaciones usen el punto de conexión específico del inquilino `https://login.microsoftonline.com/**{tenantId}**` . Puede obtener tenantId desde el contexto del mensaje del bot o de la pestaña. Si las aplicaciones usan , los usuarios recibirán tokens incorrectos e iniciarán sesión en el inquilino "hogar" en lugar del espacio empresarial en el que `https://login.microsoftonline.com/common` han iniciado sesión actualmente.

Para obtener más información sobre single Sign-On (SSO), consulte el artículo [Silent authentication](~/tabs/how-to/authentication/auth-silent-AAD.md).

## <a name="code-sample"></a>Ejemplo de código

Código de ejemplo que muestra el proceso de autenticación de tabulación con Azure AD:

| **Nombre de ejemplo** | **description** | **.NET** | **Node.js** |
|-----------------|-----------------|-------------|
| Microsoft Teams de pestañas | Proceso de autenticación de tabulación con Azure AD. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs) |

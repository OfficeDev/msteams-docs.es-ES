---
title: Configuración de código para habilitar el inicio de sesión único para pestañas
description: Describe la configuración de código para habilitar el inicio de sesión único para pestañas
ms.topic: how-to
ms.localizationpriority: medium
keywords: Pestañas de autenticación de teams De Microsoft Azure Active Directory (Azure AD) Graph API
ms.openlocfilehash: 3f095f3e2b0737b7afcdfe3bdcc96bd36d2f3847
ms.sourcegitcommit: e16b51a49756e0fe4eaf239898e28d3021f552da
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2022
ms.locfileid: "65888132"
---
# <a name="add-code-to-enable-sso"></a>Adición de código para habilitar el inicio de sesión único

Antes de agregar código para habilitar el inicio de sesión único, asegúrese de que ha registrado la aplicación con Azure AD.

> [!div class="nextstepaction"]
> [Registro con Azure AD](tab-sso-register-aad.md)

Debe configurar el código del lado cliente de la aplicación de pestaña para obtener un token de acceso de Azure AD. El token de acceso se emite en nombre de la aplicación de pestaña. Si la aplicación de pestaña requiere permisos adicionales de Microsoft Graph, deberá pasar el token de acceso al lado servidor e intercambiarlo por el token de Microsoft Graph.

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-config-code.png" alt-text="configurar código para controlar el token de acceso" border="false":::

En esta sección se describen estos temas:

- [Agregar código del lado cliente](#add-client-side-code)
- [Pasar el token de acceso al código del lado servidor](#pass-the-access-token-to-server-side-code)
- [Validar el token de acceso](#validate-the-access-token)

## <a name="add-client-side-code"></a>Agregar código del lado cliente

Para obtener acceso a la aplicación para el usuario de la aplicación actual, el código del lado cliente debe realizar una llamada a Teams para obtener un token de acceso. Debe actualizar el código del lado cliente para usarlo `getAuthToken()` para iniciar el proceso de validación.

<br>
<details>
<summary>Más información sobre getAuthToken()</summary>
<br>
`getAuthToken()` es un método del SDK de JavaScript de Microsoft Teams. Solicita que se emita un token de acceso de Azure AD en nombre de la aplicación. El token se adquiere de la memoria caché, si no ha expirado. Si ha expirado, se envía una solicitud a Azure AD para obtener un nuevo token de acceso.

 Para obtener más información, vea [getAuthToken](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-authentication-getauthtoken&preserve-view=true).
</details>

### <a name="when-to-call-getauthtoken"></a>Cuándo llamar a getAuthToken

Use `getAuthToken()` en el momento en que necesite un token de acceso para el usuario de la aplicación actual:

| Si se necesita un token de acceso... | Llame a getAuthToken()... |
| --- | --- |
| Cuando el usuario de la aplicación accede a la aplicación | Desde dentro `microsoftTeams.initialize()`de . |
| Para usar una funcionalidad determinada de la aplicación | Cuando el usuario de la aplicación realiza una acción que requiere el inicio de sesión. |

### <a name="add-code-for-getauthtoken"></a>Agregar código para getAuthToken

Agregue un fragmento de código JavaScript a la aplicación de pestaña a:

- Llamar a `getAuthToken()`.
- Analice el token de acceso o páselo al código del lado servidor.

El siguiente fragmento de código muestra un ejemplo de llamada a `getAuthToken()`.

```javascript
microsoftTeams.initialize();
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Error getting token: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

Puede agregar llamadas de `getAuthToken()` a todas las funciones y controladores que inician una acción en la que se necesita el token.

<br>
<details>
<summary>Este es un ejemplo del código del lado cliente:</summary>

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/config-client-code.png" alt-text="Configuración del código de cliente" lightbox="../../../assets/images/authentication/teams-sso-tabs/config-client-code.png":::

</details>

Cuando Teams recibe el token de acceso, se almacena en caché y se reutiliza según sea necesario. Este token se puede usar siempre que `getAuthToken()` se llame a , hasta que expire, sin realizar otra llamada a Azure AD.

> [!IMPORTANT]
> Como procedimiento recomendado para la seguridad del token de acceso:
>
> - `getAuthToken()` Llame siempre solo cuando necesite un token de acceso.
> - Teams almacenará en caché el token de acceso. No almacenes en caché ni la almacenes en el código de la aplicación.

### <a name="consent-dialog-for-getting-access-token"></a>Cuadro de diálogo consentimiento para obtener el token de acceso

Cuando se llama `getAuthToken()` y se requiere el consentimiento del usuario de la aplicación para los permisos de nivel de usuario, se muestra un cuadro de diálogo de Azure AD al usuario de la aplicación que ha iniciado sesión actualmente.

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/tabs-sso-prompt.png" alt-text="Símbolo del diálogo de inicio de sesión único de tabulación":::

El cuadro de diálogo de consentimiento que aparece es para los ámbitos de identificador abierto definidos en Azure AD. El usuario de la aplicación solo debe dar su consentimiento una vez. Después de dar su consentimiento, el usuario de la aplicación puede acceder y usar la aplicación de pestaña para los permisos y ámbitos concedidos.

> [!IMPORTANT]
> Escenarios en los que no se necesitan diálogos de consentimiento:
>
> - Si el administrador de inquilinos ha concedido el consentimiento en nombre del inquilino, no es necesario solicitar consentimiento a los usuarios de la aplicación. Esto significa que los usuarios de la aplicación no ven los diálogos de consentimiento y pueden acceder a la aplicación sin problemas.
> - Si la aplicación de Azure AD está registrada en el mismo inquilino desde el que solicita una autenticación en Teams, no se puede pedir al usuario de la aplicación que dé su consentimiento y se le conceda un token de acceso de inmediato. Los usuarios de la aplicación dan su consentimiento a estos permisos solo si la aplicación de Azure AD está registrada en un inquilino diferente.

Si encuentra algún error, consulte [Solución de problemas de autenticación de SSO en Teams](tab-sso-troubleshooting.md).

### <a name="use-the-access-token-as-an-identity-token"></a>Usar el token de acceso como token de identidad

El token devuelto a la aplicación de pestaña es un token de acceso y un token de identificador. La aplicación de pestaña puede usar el token como token de acceso para realizar solicitudes HTTPS autenticadas a las API en el lado servidor.

El token de acceso devuelto desde `getAuthToken()` se puede usar para establecer la identidad del usuario de la aplicación mediante las siguientes notificaciones en el token:

- `name`: nombre para mostrar del usuario de la aplicación.
- `preferred_username`: dirección de correo electrónico del usuario de la aplicación.
- `oid`: GUID que representa el identificador del usuario de la aplicación.
- `tid`: GUID que representa el inquilino en el que el usuario de la aplicación inicia sesión.

Teams puede almacenar en caché esta información asociada a la identidad del usuario de la aplicación, como las preferencias del usuario.

> [!NOTE]
> Si necesita crear un identificador único para representar al usuario de la aplicación en el sistema, consulte [Uso de notificaciones para identificar de forma confiable a un usuario](/azure/active-directory/develop/id-tokens#using-claims-to-reliably-identify-a-user-subject-and-object-id).

## <a name="pass-the-access-token-to-server-side-code"></a>Pasar el token de acceso al código del lado servidor

Si necesita acceder a las API web en el servidor, deberá pasar el token de acceso al código del lado servidor. Las API web deben descodificar el token de acceso para ver las notificaciones de ese token.

> [!NOTE]
> Si no recibe el nombre principal de usuario (UPN) en el token de acceso devuelto, agréguelo como una [notificación opcional](/azure/active-directory/develop/active-directory-optional-claims) en Azure AD.
> Para obtener más información, consulte [Tokens de acceso](/azure/active-directory/develop/access-tokens).

El token de acceso recibido en la devolución de llamada correcta de `getAuthToken()` proporciona acceso (para el usuario de aplicación autenticado) a las API web. El código del lado servidor también puede analizar el token para obtener [información de identidad](#use-the-access-token-as-an-identity-token), si es necesario.

Si necesita pasar el token de acceso para obtener datos de Microsoft Graph, consulte [Extensión de la aplicación de pestaña con permisos de Microsoft Graph](tab-sso-graph-api.md).

### <a name="code-for-passing-access-token-to-server-side"></a>Código para pasar el token de acceso al lado servidor

El código siguiente muestra un ejemplo de pasar el token de acceso al lado del servidor. El token se pasa en un encabezado `Authorization` al enviar una solicitud a una API web del lado servidor. En este ejemplo se envían datos JSON, por lo que se usa el `POST` método . `GET` es suficiente para enviar el token de acceso cuando no escribe en el servidor.

```javascript
$.ajax({
    type: "POST",
    url: "/api/DoSomething",
    headers: {
        "Authorization": "Bearer " + accessToken
    },
    data: { /* some JSON payload */ },
    contentType: "application/json; charset=utf-8"
}).done(function (data) {
    // Handle success
}).fail(function (error) {
    // Handle error
}).always(function () {
    // Cleanup
});
```

### <a name="validate-the-access-token"></a>Validar el token de acceso

Las API web del servidor deben descodificar el token de acceso y comprobar si se envían desde el cliente. El token es un JSON Web Token (JWT), lo que significa que la validación funciona igual que la validación des tokens en la mayoría de los flujos de OAuth normales. Las API web deben descodificar el token de acceso. Opcionalmente, puede copiar y pegar el token de acceso manualmente en una herramienta, como jwt.ms.

Hay varias bibliotecas disponibles que pueden controlar la validación JWT. La validación básica incluye:

- Comprobar que el token es correcto
- Comprobar que la autoridad prevista emitió el token
- Comprobación de que el token está destinado a la API web

Tenga en cuenta las siguientes instrucciones para validar el token:

- Azure AD emite tokens de SSO válidos. La notificación `iss` en el token debería empezar por este valor.
- El parámetro del `aud1` token se establecerá en el identificador de aplicación generado durante el registro de la aplicación de Azure AD.
- El parámetro `scp` del token se establece en `access_as_user`.

#### <a name="example-access-token"></a>Ejemplo de token de acceso

La siguiente es una carga ?til decodificada t?pica de un token de acceso.

```javascript
{
    aud: "2c3caa80-93f9-425e-8b85-0745f50c0d24",
    iss: "https://login.microsoftonline.com/fec4f964-8bc9-4fac-b972-1c1da35adbcd/v2.0",
    iat: 1521143967,
    nbf: 1521143967,
    exp: 1521147867,
    aio: "ATQAy/8GAAAA0agfnU4DTJUlEqGLisMtBk5q6z+6DB+sgiRjB/Ni73q83y0B86yBHU/WFJnlMQJ8",
    azp: "e4590ed6-62b3-5102-beff-bad2292ab01c",
    azpacr: "0",
    e_exp: 262800,
    name: "Mila Nikolova",
    oid: "6467882c-fdfd-4354-a1ed-4e13f064be25",
    preferred_username: "milan@contoso.com",
    scp: "access_as_user",
    sub: "XkjgWjdmaZ-_xDmhgN1BMP2vL2YOfeVxfPT_o8GRWaw",
    tid: "fec4f964-8bc9-4fac-b972-1c1da35adbcd",
    uti: "MICAQyhrH02ov54bCtIDAA",
    ver: "2.0"
}
```

## <a name="code-samples"></a>Ejemplos de código

| Ejemplo de nombre | Descripción | C#/.NET| Node.js |
|---------------|---------------|------|--------------|
| Inicio de sesión único de pestaña |Aplicación de ejemplo para el SSO para pestañas de Azure AD de Microsoft Teams| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|[Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs), </br>[Kit de herramientas de Teams](../../../toolkit/visual-studio-code-tab-sso.md)|
| Inicio de sesión único (SSO) de pestaña, bot y extensión de mensajes (ME) | En este ejemplo se muestra SSO para pestaña, Bot y ME: búsqueda, acción, linkunfurl. |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Actualización del manifiesto de aplicación de Teams y vista previa de la aplicación](tab-sso-manifest.md)

## <a name="see-also"></a>Vea también

- [jwt.ms](https://jwt.ms/)
- [Notificación opcional de Active Directory](/azure/active-directory/develop/active-directory-optional-claims)
- [Tokens de acceso](/azure/active-directory/develop/access-tokens)
- [Información general de la biblioteca de autenticación de Microsoft (MSAL)](/azure/active-directory/develop/msal-overview)
- [Tokens de identificador de la plataforma de identidad de Microsoft](/azure/active-directory/develop/id-tokens)
- [ Tokens de acceso de la Plataforma de identidad de Microsoft](/azure/active-directory/develop/access-tokens#validating-tokens)

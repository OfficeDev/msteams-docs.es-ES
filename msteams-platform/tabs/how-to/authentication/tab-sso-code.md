---
title: Configuración de código para habilitar el inicio de sesión único para pestañas
description: Actualice el código de la aplicación de pestaña para solicitar y recibir un token de acceso mediante la identidad de Teams del usuario de la aplicación para habilitar el inicio de sesión único (SSO).
ms.topic: how-to
ms.localizationpriority: high
keywords: pestañas de autenticación de teams Microsoft Azure Active Directory (Azure AD) Graph API
ms.openlocfilehash: 20b11032227a08d057a6cdae8e46154004bfdb02
ms.sourcegitcommit: bb15ce26cd65bec90991b703069424ab4b4e1a61
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/28/2022
ms.locfileid: "68772268"
---
# <a name="add-code-to-enable-sso"></a>Agregar código para habilitar el inicio de sesión único

Antes de agregar código para habilitar el inicio de sesión único, asegúrese de que ha registrado la aplicación con Azure AD.

> [!div class="nextstepaction"]
> [Registre con Azure AD.](tab-sso-register-aad.md)

Debe configurar el código del lado cliente de la aplicación de pestaña para obtener un token de acceso de Azure AD. El token de acceso se emite en nombre de la aplicación de pestaña. Si la aplicación de pestaña requiere permisos adicionales de Microsoft Graph, deberá pasar el token de acceso al lado servidor e intercambiarlo por el token de Microsoft Graph.

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-config-code.png" alt-text="configurar código para controlar el token de acceso":::

En esta sección se describen estos temas:

- [Agregar código del lado cliente](#add-client-side-code)
- [Pasar el token de acceso al código del lado servidor](#pass-the-access-token-to-server-side-code)
- [Validar el token de acceso](#validate-the-access-token)

## <a name="add-client-side-code"></a>Agregar código del lado cliente

Para obtener acceso a la aplicación para el usuario de la aplicación actual, el código del lado cliente debe realizar una llamada a Teams para obtener un token de acceso. Debe actualizar el código del lado cliente para usar `getAuthToken()` para iniciar el proceso de validación.

<br>
<details>
<summary>Obtenga más información sobre getAuthToken()</summary>
<br>
`getAuthToken()` es un método del SDK de JavaScript de Microsoft Teams. Solicita que se emita un token de acceso de Azure AD en nombre de la aplicación. El token se adquiere de la memoria caché, si no ha expirado. De lo contrario, se envía una solicitud a Azure AD para obtener un nuevo token.

 Para más información, vea [getAuthToken](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-authentication-getauthtoken&preserve-view=true).
</details>

### <a name="when-to-call-getauthtoken"></a>Cuándo llamar a getAuthToken

Use `getAuthToken()` en el momento en que necesite un token de acceso para el usuario de la aplicación actual:

| Si se necesita un token de acceso... | Llame a getAuthToken()... |
| --- | --- |
| Cuando el usuario de la aplicación accede a la aplicación | Después de `microsoftTeams.initialize()`. |
| Para usar una funcionalidad determinada de la aplicación | Cuando el usuario de la aplicación realiza una acción que requiere el inicio de sesión. |

### <a name="add-code-for-getauthtoken"></a>Agregar código para getAuthToken

Agregue un fragmento de código JavaScript a la aplicación de pestaña a:

- Llamar a `getAuthToken()`.
- Analice el token de acceso o páselo al código del lado del servidor.

El fragmento de código siguiente muestra un ejemplo de llamada `getAuthToken()`.

```javascript
microsoftTeams.initialize();
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Error getting token: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

Por lo que puede agregar llamadas de `getAuthToken()` a todas las funciones y controladores que inician una acción en la que se requiere el token.

<br>
<details>
<summary>Este es un ejemplo del código del lado cliente:</summary>

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/config-client-code.png" alt-text="Configuración del código de cliente" lightbox="../../../assets/images/authentication/teams-sso-tabs/config-client-code.png":::

</details>

Cuando Teams recibe el token de acceso, se almacena en caché y se reutiliza según sea necesario. Este token se puede usar siempre que se llame a `getAuthToken()`, hasta que expire, sin realizar otra llamada a Azure AD.

> [!IMPORTANT]
> Como procedimiento recomendado para la seguridad del token de acceso:
>
> - Llame siempre a `getAuthToken()` cuando necesite un token de acceso.
> - Teams almacenará en caché el token de acceso. No almacene en caché ni la almacene en el código de la aplicación.

### <a name="consent-dialog-for-getting-access-token"></a>Cuadro de diálogo consentimiento para obtener el token de acceso

Cuando se llama a `getAuthToken()` y se requiere el consentimiento del usuario de la aplicación para los permisos de nivel de usuario, se muestra un cuadro de diálogo de Azure AD al usuario de la aplicación que ha iniciado sesión actualmente.

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/tabs-sso-prompt.png" alt-text="Símbolo del cuadro de diálogo de inicio de sesión único de pestaña":::

El cuadro de diálogo de consentimiento que aparece es para los ámbitos de identificador abierto definidos en Azure AD. El usuario de la aplicación solo debe dar su consentimiento una vez. Después de dar su consentimiento, el usuario de la aplicación puede acceder y usar la aplicación de pestaña para los permisos y ámbitos concedidos.

> [!IMPORTANT]
> Escenarios en los que no se necesitan cuadros de diálogo de consentimiento:
>
> - Si el administrador de inquilinos ha concedido el consentimiento en nombre del inquilino, no es necesario solicitar consentimiento a los usuarios de la aplicación. Esto significa que los usuarios de la aplicación no ven los cuadros de diálogo de consentimiento y pueden acceder a la aplicación sin problemas.
> - Si su aplicación de Azure AD está registrada con el mismo inquilino con el que está haciendo una solicitud de autenticación en Teams, no se puede pedir consentimiento al usuario de la aplicación y se le concede un token de acceso inmediatamente. Los usuarios solo dan su consentimiento a estos permisos si la aplicación de Azure AD está registrada en un inquilino diferente.

Si encuentra algún error, consulte [Solución de problemas de autenticación de SSO en Teams](tab-sso-troubleshooting.md).

### <a name="use-the-access-token-as-an-identity-token"></a>Usar el token de acceso como token de identidad

El token devuelto a la aplicación de pestaña es un token de acceso y un token de identificador. La aplicación de pestaña puede usar el token como un token de acceso para realizar solicitudes HTTPS autenticadas a las API en el lado del servidor.

El token de acceso devuelto desde `getAuthToken()` se puede usar para establecer la identidad del usuario de la aplicación mediante las siguientes notificaciones en el token:

- `name`: el nombre para mostrar del usuario de la aplicación
- `preferred_username`: la dirección de correo electrónico del usuario de la aplicación.
- `oid` - Un GUID que representa el identificador del usuario de la aplicación.
- `tid` - Un GUID que representa el inquilino en el que el usuario de la aplicación está iniciando sesión.

Teams puede almacenar en caché esta información asociada a la identidad del usuario de la aplicación, como las preferencias del usuario.

> [!NOTE]
> Si necesita crear un identificador único para representar al usuario de la aplicación en el sistema, consulte [Uso de notificaciones para identificar de forma fiable a un usuario](/azure/active-directory/develop/id-tokens#using-claims-to-reliably-identify-a-user-subject-and-object-id).

## <a name="pass-the-access-token-to-server-side-code"></a>Pasar el token de acceso al código del lado servidor

Si necesita tener acceso a las API web en el servidor, deberá pasar el token de acceso al código del lado servidor. Las API web deben descodificar el token de acceso para ver las notificaciones de ese token.

> [!NOTE]
> Si no recibe el nombre principal de usuario (UPN) en el token de acceso devuelto, agréguelo como una [notificación opcional](/azure/active-directory/develop/active-directory-optional-claims) en Azure AD.
> Para obtener más información, consulte [tokens de acceso](/azure/active-directory/develop/access-tokens).

El token de acceso recibido en la devolución de llamada correcta de `getAuthToken()` proporciona acceso (para el usuario de aplicación autenticado) a las API web. También el código del lado servidor puede analizar el token para obtener [información de identidad](#use-the-access-token-as-an-identity-token), si lo necesita.

Si necesita pasar el token de acceso para obtener datos de Microsoft Graph, consulte [Extensión de la aplicación de pestaña con permisos de Microsoft Graph](tab-sso-graph-api.md).

### <a name="code-for-passing-access-token-to-server-side"></a>Código para pasar el token de acceso al lado servidor

El código siguiente muestra un ejemplo de pasar el token de acceso al lado del servidor. El token se pasa en un encabezado `Authorization` al enviar una solicitud a una API web del lado servidor. En este ejemplo se envían datos JSON, por lo que se usa el método `POST`. `GET` es suficiente para enviar el token de acceso cuando no escribe en el servidor.

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

Las API web del servidor deben descodificar el token de acceso y verificar si se envía desde el cliente. El token es un JSON Web Token (JWT), lo que significa que la validación funciona igual que la validación des tokens en la mayoría de los flujos de OAuth normales. Las API web deben descodificar el token de acceso. Opcionalmente, copie y pegue manualmente el token de acceso en una herramienta, como jwt.ms.

Hay muchas bibliotecas disponibles que pueden encargarse de la validación JWT. La validación básica incluye:

- Comprobar que el token es correcto
- Comprobar que la autoridad prevista emitió el token
- Comprobar que el token se destina a la API web

Tenga en cuenta las siguientes instrucciones para validar el token:

- Azure AD emite tokens de SSO válidos. La notificación `iss` en el token debería empezar por este valor.
- El parámetro del token `aud1` se establecerá en el identificador de aplicación generado durante el registro de la aplicación de Azure AD.
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
> [Actualización del manifiesto de aplicación de Teams y vista previa de aplicación](tab-sso-manifest.md)

## <a name="see-also"></a>Recursos adicionales

- [jwt.ms](https://jwt.ms/)
- [Notificación opcional de Active Directory](/azure/active-directory/develop/active-directory-optional-claims)
- [Tokens de acceso](/azure/active-directory/develop/access-tokens)
- [Información general de Biblioteca de autenticación de Microsoft (MSAL)](/azure/active-directory/develop/msal-overview).
- [ Tokens de identificador de la Plataforma de identidad de Microsoft](/azure/active-directory/develop/id-tokens)
- [ Tokens de acceso de la Plataforma de identidad de Microsoft](/azure/active-directory/develop/access-tokens#validating-tokens)

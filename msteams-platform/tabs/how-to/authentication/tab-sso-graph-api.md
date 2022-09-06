---
title: Extensión de la aplicación de pestañas con permisos de Microsoft Graph
description: Configure permisos y ámbitos adicionales con Microsoft Graph para habilitar el inicio de sesión único (SSO).
ms.topic: how-to
ms.localizationpriority: high
keywords: pestañas de autenticación de teams Microsoft Azure Active Directory (Azure AD) Graph API ámbito del token de acceso a permisos delegados
ms.openlocfilehash: 3232d1104a715b8c50f39b1e70d58fa18d970b7c
ms.sourcegitcommit: d92e14fad6567fe91fd52ee6c213836740316683
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2022
ms.locfileid: "67605092"
---
# <a name="extend-tab-app-with-microsoft-graph-permissions-and-scope"></a>Extender la aplicación de pestañas con permisos y ámbito de Microsoft Graph

Puede extender la aplicación de pestañas mediante Microsoft Graph para permitir a los usuarios permisos adicionales, como ver el perfil de usuario de la aplicación, leer correo y mucho más. La aplicación debe solicitar ámbitos de permiso específicos para obtener los tokens de acceso con el consentimiento del usuario de la aplicación.

Los ámbitos de grafo, como `User.Read` o `Mail.Read`, le permiten especificar cómo la aplicación accede a la cuenta de un usuario de Teams. Debe especificar sus ámbitos en la solicitud de autorización.

En esta sección, aprenderá a:

- [Configuración de permisos de API en Azure AD](#configure-api-permissions-in-azure-ad)
- [Configuración de la autenticación para distintas plataformas](#configure-authentication-for-different-platforms)
- [ Adquirir token de acceso para MS Graph](#acquire-access-token-for-ms-graph)

## <a name="configure-api-permissions-in-azure-ad"></a>Configuración de permisos de API en Azure AD

Puede configurar ámbitos de gráfico adicionales en Azure AD para la aplicación. Estos son permisos delegados, que usan las aplicaciones que requieren acceso de inicio de sesión. Un usuario o administrador de la aplicación que haya iniciado sesión debe dar su consentimiento. La aplicación de pestaña puede dar su consentimiento en nombre del usuario que ha iniciado sesión cuando llama a Microsoft Graph.

### <a name="to-configure-api-permissions"></a>Para configurar los permisos de API

1. Abra la aplicación que registró en el [Azure Portal](https://ms.portal.azure.com/).

2. Seleccione **Administrar** > **permiso de API** en el panel izquierdo.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/api-permission-menu.png" alt-text="Opción de menú Permisos de la aplicación.":::

    Aparece la página **de permisos de API** 

3. Seleccione **+ Agregar permisos** para agregar permisos de API de Microsoft Graph.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-permission.png" alt-text="Página de permisos de la aplicación.":::

    Aparece la página **Solicitar permisos de API**.

4. Seleccione **Microsoft Graph**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/request-api-permission.png" alt-text=" Página Solicitar permisos de API.":::

    Se muestran las opciones de permisos de gráfico.

5. Seleccione **Permisos delegados** para ver la lista de permisos.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/delegated-permission.png" alt-text="Permisos delegados":::.

6. Seleccione los permisos relevantes para la aplicación y, a continuación, seleccione **Agregar permisos**.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/select-permission.png" alt-text="Seleccione permisos.":::

    También puede introducir el nombre del permiso en el cuadro de búsqueda para encontrarlo.

    Aparece un mensaje en el navegador que indica que los permisos se actualizaron.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/updated-permission-msg.png" alt-text="Mensaje de permisos actualizados.":::

    Los permisos agregados se muestran en la página de **permisos de API**.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/configured-permissions.png" alt-text="Los permisos de API están configurados.":::

    Ha configurado la aplicación con permisos de Microsoft Graph.

## <a name="configure-authentication-for-different-platforms"></a>Configurar la autenticación para distintas plataformas

Dependiendo de la plataforma o el dispositivo al que quieras dirigirte a tu aplicación, es posible que se requiera una configuración adicional, como URI de redireccionamiento, configuraciones de autenticación específicas o detalles específicos de la plataforma.

> [!NOTE]
>
> - Si la aplicación de pestañas no ha recibido el consentimiento del administrador de TI, los usuarios de la aplicación deben dar su consentimiento la primera vez que usen la aplicación en una plataforma diferente.
> - No se requiere concesión implícita si SSO está habilitado en una aplicación de pestañas.

Puede configurar la autenticación para varias plataformas siempre que la dirección URL sea única.

### <a name="to-configure-authentication-for-a-platform"></a>Para configurar la autenticación para una plataforma

1. Abra la aplicación que registró en el el[Azure Portal](https://ms.portal.azure.com/).

1. Seleccione **Administrar****autenticación** > en el panel izquierdo.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-portal-platform.png" alt-text="Autenticación para plataformas":::

    Aparece la página **Configuraciones de la plataforma**.

1. Seleccione **+ Agregar una plataforma**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-platform.png" alt-text="Agregar una plataforma":::

    Aparece la página **Configurar plataformas**.

1. Seleccione la plataforma que desea configurar para la aplicación de pestañas. Puede elegir el tipo de plataforma entre web o SPA.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/configure-platform.png" alt-text="Seleccione la plataforma web":::

    Puede configurar varias plataformas para un tipo de plataforma en particular. Asegúrese de que el URI de redireccionamiento es único para cada plataforma que configure.

    Aparece la página de Configuración de la web.

    > [!NOTE]
    > Las configuraciones serán diferentes en función de la plataforma que seleccione.

1. Introduzca los detalles de configuración de la plataforma.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/config-web-platform.png" alt-text="Configurar plataforma web":::

    1. Introduzca el URI de redireccionamiento. El URI debe ser único.
    2. Introduzca la URL de cierre de sesión del canal frontal.
    3. Seleccione los tokens que desea que Azure AD envíe para su aplicación.

1. Seleccione **Configurar**.

    La plataforma se configura y se muestra en la página **Configuraciones de la plataforma**.

## <a name="acquire-access-token-for-ms-graph"></a>Adquirir token de acceso para MS Graph

Deberá adquirir el token de acceso para Microsoft Graph. Puede hacerlo mediante el flujo de OBO de Azure AD.

La implementación actual para SSO otorga consentimiento solo para los permisos de nivel de usuario que no se pueden usar para realizar llamadas a Graph. Para obtener los permisos (ámbitos) necesarios para realizar una llamada a Graph, las aplicaciones de SSO deben implementar un servicio web personalizado para intercambiar el token recibido del SDK de JavaScript de Teams por un token que incluya los ámbitos necesarios. Puede usar la biblioteca de autenticación de Microsoft (MSAL) para obtener el token desde el lado del cliente.

Después de configurar los permisos de Graph en Azure AD:

- [Configurar el código del lado cliente para obtener el token de acceso mediante MSAL](#configure-code-to-fetch-access-token-using-msal)
- [Pasar el token de acceso al código del lado servidor](#pass-the-access-token-to-server-side-code)

### <a name="configure-code-to-fetch-access-token-using-msal"></a>Configurar código para obtener el token de acceso mediante MSAL

El código siguiente proporciona un ejemplo de flujo OBO para obtener el token de acceso del cliente de Teams mediante MSAL.

### <a name="c"></a>[C#](#tab/dotnet)

```csharp

IConfidentialClientApplication app = ConfidentialClientApplicationBuilder.Create(<"Client id">)
                                                .WithClientSecret(<"Client secret">)
                                                .WithAuthority($"https://login.microsoftonline.com/<"Tenant id">")
                                                .Build();
 
            try
            {
                var idToken = <"Client side token">;
                UserAssertion assert = new UserAssertion(idToken);
                List<string> scopes = new List<string>();
                scopes.Add("https://graph.microsoft.com/User.Read");
                var responseToken = await app.AcquireTokenOnBehalfOf(scopes, assert).ExecuteAsync();
                return responseToken.AccessToken.ToString();
            }
            catch (Exception ex)
            {
                return ex.Message;
            }
        }
```

### <a name="nodejs"></a>[Node.js](#tab/nodejs)

```Node.js

// Exchange client Id side token with server token
  app.post('/getProfileOnBehalfOf', function(req, res) {
        var tid = < "Tenant id" >
    var token = < "Client side token" >
    var scopes = ["https://graph.microsoft.com/User.Read"];

        // Creating MSAL client
        const msalClient = new msal.ConfidentialClientApplication({
            auth: {
                clientId: < "Client ID" >,
                clientSecret: < "Client Secret" >
      }
        });

        var oboPromise = new Promise((resolve, reject) => {
            msalClient.acquireTokenOnBehalfOf({
                authority: `https://login.microsoftonline.com/${tid}`,
                oboAssertion: token,
                scopes: scopes,
                skipCache: true
            }).then(result => {
                console.log("Token is: " + result.accessToken);
            }).catch(error => {
                reject({ "error": error.errorCode });
            });
        });
```

---

### <a name="pass-the-access-token-to-server-side-code"></a>Pasar el token de acceso al código del lado servidor

Si necesita acceder a los datos de Microsoft Graph, configure el código del lado del servidor para:

1. Validar el token de acceso. Para obtener más información, consulte [Validar el token de acceso](tab-sso-code.md#validate-the-access-token).
1. Inicie el flujo de OBO de OAuth 2.0 con una llamada a la plataforma de identidad de Microsoft que incluye el token de acceso, algunos metadatos sobre el usuario y las credenciales de la aplicación de pestaña (su identificador de aplicación y secreto de cliente). La plataforma de identidad de Microsoft devolverá un nuevo token de acceso que se puede usar para obtener acceso a Microsoft Graph.
1. Obtener datos de Microsoft Graph mediante el nuevo token.
1. Use la serialización de caché de tokens en MSAL.NET para almacenar en caché el nuevo token de acceso para varios, si es necesario.

> [!IMPORTANT]
> Como procedimiento recomendado de seguridad, use siempre el código del lado servidor para realizar llamadas de Microsoft Graph, u otras llamadas que requieran pasar un token de acceso. Nunca devuelva el token OBO al cliente para permitir que el cliente realice llamadas directas a Microsoft Graph. Esto ayuda a proteger el token de ser interceptado o filtrado.

## <a name="known-limitations"></a>Limitaciones conocidas

Consentimiento del administrador del inquilino: una manera sencilla de [dar su consentimiento en nombre de una organización como administrador del inquilino](/azure/active-directory/manage-apps/consent-and-permissions-overview#admin-consent) es obtener [el consentimiento del administrador](/azure/active-directory/manage-apps/grant-admin-consent).

Puede solicitar su consentimiento utilizando la API de autenticación. Otro enfoque para obtener ámbitos de Graph es presentar un cuadro de diálogo de consentimiento mediante nuestro [enfoque de autenticación de proveedor de OAuth de terceros](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page)existente. Este enfoque implica la creación de un cuadro de diálogo de consentimiento de Azure AD.

<details>
<summary>Para solicitar consentimiento adicional mediante la API de autenticación, siga estos pasos:</summary>

1. El token recuperado `getAuthToken()` debe ser intercambiado en el lado del servidor utilizando Azure AD[en nombre del flujo](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) para obtener acceso a esas otras API de Graph. Asegúrese de usar el punto de conexión de Graph v2 para este intercambio.
2. Si se produce un error en el intercambio, Azure AD devuelve una excepción de concesión no válida. Por lo general, responde con uno de los dos mensajes de error, `invalid_grant` o `interaction_required`.
3. Cuando se produce un error en el intercambio, debe solicitar consentimiento. Use la interfaz de usuario (UI) para pedir al usuario de la aplicación que otorgue otro consentimiento. Esta interfaz de usuario debe incluir un botón que desencadene un cuadro de diálogo de consentimiento Azure AD mediante [la autenticación silenciosa](~/concepts/authentication/auth-silent-aad.md).
4. Al solicitar más consentimiento de Azure AD, debe incluir `prompt=consent` en el [parámetro de cadena de consulta](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) para Azure AD; de lo contrario, Azure AD no pediría otros ámbitos.
    - En lugar de `?scope={scopes}`, use `?prompt=consent&scope={scopes}`
    - Asegúrese de que `{scopes}` incluye todos los ámbitos que está solicitando al usuario, por ejemplo, `Mail.Read` o `User.Read`.
5. Después de que el usuario de la aplicación haya concedido más permisos, vuelva a intentar el flujo de OBO para obtener acceso a estas otras API.

    </details>

## <a name="see-also"></a>Recursos adicionales

- [Flujo OAuth 2.0 On-Behalf-Of](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow)
- [ Obtener acceso para MS Graph](/graph/auth-v2-user)
- [Serialización de caché de tokens en MSAL.NET](/azure/active-directory/develop/msal-net-token-cache-serialization?tabs=aspnet)
- [ Proveedor MSAL2 de Microsoft Teams](/graph/toolkit/providers/teams-msal2)

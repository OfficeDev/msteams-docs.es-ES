---
title: Extensión de la aplicación de pestaña con permisos de Microsoft Graph
description: Describe la configuración de permisos de API con Microsoft Graph
ms.topic: how-to
ms.localizationpriority: medium
keywords: Pestañas de autenticación de teams Microsoft Azure Active Directory (Azure AD) Graph API Ámbito de token de acceso delegado de permisos
ms.openlocfilehash: 76b474f69b31d9c9b9925803ee7c0240f9e5a7c4
ms.sourcegitcommit: e16b51a49756e0fe4eaf239898e28d3021f552da
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2022
ms.locfileid: "65888174"
---
# <a name="extend-tab-app-with-microsoft-graph-permissions-and-scope"></a>Extensión de la aplicación de pestaña con permisos y ámbito de Microsoft Graph

Puede ampliar la aplicación de pestaña mediante Microsoft Graph para permitir a los usuarios permisos adicionales, como ver el perfil de usuario de la aplicación, leer correo y mucho más. La aplicación debe solicitar ámbitos de permiso específicos para obtener los tokens de acceso con el consentimiento del usuario de la aplicación.

Los ámbitos de grafos, como `User.Read` o `Mail.Read`, le permiten especificar cómo accede la aplicación a la cuenta de un usuario de Teams. Debe especificar los ámbitos en la solicitud de autorización.

En esta sección, aprenderá a:

- [Configuración de permisos de API en Azure AD](#configure-api-permissions-in-azure-ad)
- [Configuración de la autenticación para distintas plataformas](#configure-authentication-for-different-platforms)
- [Adquisición de un token de acceso para MS Graph](#acquire-access-token-for-ms-graph)

## <a name="configure-api-permissions-in-azure-ad"></a>Configuración de permisos de API en Azure AD

Puede configurar ámbitos de Graph adicionales en Azure AD para la aplicación. Estos son permisos delegados, que usan las aplicaciones que requieren acceso con sesión iniciada. Un usuario o administrador de la aplicación que ha iniciado sesión debe dar su consentimiento. La aplicación de pestaña puede dar su consentimiento en nombre del usuario que ha iniciado sesión cuando llama a Microsoft Graph.

### <a name="to-configure-api-permissions"></a>Para configurar permisos de API

1. Abra la aplicación que registró en [Azure Portal](https://ms.portal.azure.com/).

2. Seleccione **Administrar** > **permiso de API** en el panel izquierdo.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/api-permission-menu.png" alt-text="Opción de menú Permisos de aplicación." border="true":::

    Aparece la página **Permisos de API** .

3. Seleccione **+ Agregar permisos** para agregar permisos de Microsoft Graph API.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-permission.png" alt-text="Página Permisos de aplicación." border="true":::

    Aparece **la página Solicitar permisos de API** .

4. Seleccione **Microsoft Graph**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/request-api-permission.png" alt-text="Página Solicitar permisos de API." border="true":::

    Se muestran las opciones de permisos de Graph.

5. Seleccione **Permisos delegados** para ver la lista de permisos.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/delegated-permission.png" alt-text="Permisos delegados." border="true":::

6. Seleccione los permisos pertinentes para la aplicación y, a continuación, seleccione **Agregar permisos**.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/select-permission.png" alt-text="Seleccione permisos." border="true":::

    También puede escribir el nombre del permiso en el cuadro de búsqueda para encontrarlo.

    Aparece un mensaje en el explorador que indica que se actualizaron los permisos.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/updated-permission-msg.png" alt-text="Mensaje de permisos actualizados." border="false":::

    Los permisos agregados se muestran en la página **Permisos de API** .

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/configured-permissions.png" alt-text="Se configuran los permisos de API." border="true":::

    Ha configurado la aplicación con permisos de Microsoft Graph.

## <a name="configure-authentication-for-different-platforms"></a>Configuración de la autenticación para distintas plataformas

En función de la plataforma o dispositivo en el que quiera dirigirse a la aplicación, es posible que se requiera una configuración adicional, como uri de redireccionamiento, configuración de autenticación específica o detalles específicos de la plataforma.

> [!NOTE]
>
> - Si a la aplicación de pestaña no se le ha concedido el consentimiento del administrador de TI, los usuarios de la aplicación tendrán que proporcionar su consentimiento la primera vez que usen la aplicación en otra plataforma.
> - La concesión implícita no es necesaria si el inicio de sesión único está habilitado en una aplicación de pestaña.

Puede configurar la autenticación para varias plataformas siempre y cuando la dirección URL sea única.

### <a name="to-configure-authentication-for-a-platform"></a>Para configurar la autenticación para una plataforma

1. Abra la aplicación que registró en [Azure Portal](https://ms.portal.azure.com/).

1. Seleccione **Administrar** > **autenticación** en el panel izquierdo.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-portal-platform.png" alt-text="Autenticación para plataformas" border="true":::

    Aparece **la página Configuraciones de plataforma** .

1. Seleccione **+ Agregar una plataforma**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-platform.png" alt-text="Adición de una plataforma" border="true":::

    Aparece **la página Configurar plataformas** .

1. Seleccione la plataforma que desea configurar para la aplicación de pestaña. Puede elegir el tipo de plataforma de web o SPA.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/configure-platform.png" alt-text="Seleccionar plataforma web" border="true":::

    Puede configurar varias plataformas para un tipo de plataforma determinado. Asegúrese de que el URI de redireccionamiento es único para cada plataforma que configure.

    Aparece la página Configurar web.

    > [!NOTE]
    > Las configuraciones serán diferentes en función de la plataforma que seleccione.

1. Escriba los detalles de configuración de la plataforma.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/config-web-platform.png" alt-text="Configuración de la plataforma web" border="true":::

    1. Escriba el URI de redireccionamiento. El URI debe ser único.
    2. Escriba la dirección URL de cierre de sesión del canal frontal.
    3. Seleccione los tokens que quiere que Azure AD envíe para la aplicación.

1. Seleccione **Configurar**.

    La plataforma se configura y se muestra en la página **Configuraciones** de la plataforma.

## <a name="acquire-access-token-for-ms-graph"></a>Adquisición de un token de acceso para MS Graph

Tendrá que adquirir el token de acceso para Microsoft Graph. Para ello, use el flujo de OBO de Azure AD.

La implementación actual de SSO concede consentimiento solo para los permisos de nivel de usuario que no se pueden usar para realizar llamadas a Graph. Para obtener los permisos (ámbitos) necesarios para realizar una llamada a Graph, las aplicaciones de SSO deben implementar un servicio web personalizado para intercambiar el token recibido del SDK de JavaScript de Teams por un token que incluya los ámbitos necesarios. Puede usar la Biblioteca de autenticación de Microsoft (MSAL) para capturar el token del lado cliente.

Después de configurar los permisos de Graph en Azure AD:

- [Configuración del código del lado cliente para capturar el token de acceso mediante MSAL](#configure-code-to-fetch-access-token-using-msal)
- [Pasar el token de acceso al código del lado servidor](#pass-the-access-token-to-server-side-code)

### <a name="configure-code-to-fetch-access-token-using-msal"></a>Configuración del código para capturar el token de acceso mediante MSAL

El código siguiente proporciona un ejemplo de flujo de OBO para capturar el token de acceso desde el cliente de Teams mediante MSAL.

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

Si necesita acceder a los datos de Microsoft Graph, configure el código del lado servidor para:

1. Valide el token de acceso. Para obtener más información, consulte [Validar el token de acceso](tab-sso-code.md#validate-the-access-token).
1. Inicie el flujo de OBO de OAuth 2.0 con una llamada a la plataforma de identidad de Microsoft que incluya el token de acceso, algunos metadatos sobre el usuario y las credenciales de la aplicación de pestaña (su identificador de aplicación y su secreto de cliente). La plataforma de identidad de Microsoft devolverá un nuevo token de acceso que se puede usar para obtener acceso a Microsoft Graph.
1. Obtener datos de Microsoft Graph mediante el nuevo token.
1. Use la serialización de caché de tokens en MSAL.NET para almacenar en caché el nuevo token de acceso para varios, si es necesario.

> [!IMPORTANT]
> Como procedimiento recomendado para la seguridad, use siempre el código del lado servidor para realizar llamadas a Microsoft Graph u otras llamadas que requieran pasar un token de acceso. Nunca devuelva el token OBO al cliente para permitir que el cliente realice llamadas directas a Microsoft Graph. Esto ayuda a proteger el token de ser interceptado o filtrado.

## <a name="known-limitations"></a>Limitaciones conocidas

Consentimiento del administrador de inquilinos: una forma sencilla de [dar su consentimiento en nombre de una organización como administrador de inquilinos](/azure/active-directory/manage-apps/consent-and-permissions-overview#admin-consent) es obtener [el consentimiento del administrador](/azure/active-directory/manage-apps/grant-admin-consent).

Puede solicitar consentimiento mediante la API de autenticación. Otro enfoque para obtener ámbitos de Graph es presentar un cuadro de diálogo de consentimiento mediante nuestro [enfoque de autenticación de proveedor de OAuth de terceros](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page) existente. Este enfoque implica la creación de un cuadro de diálogo de consentimiento de Azure AD.

<details>
<summary>Para solicitar consentimiento adicional mediante la API de autenticación, siga estos pasos:</summary>

1. El token recuperado mediante `getAuthToken()` debe intercambiarse en el lado servidor mediante el [flujo en nombre de](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) Azure AD para obtener acceso a esas otras API de Graph. Asegúrese de usar el punto de conexión de Graph v2 para este intercambio.
2. Si se produce un error en el intercambio, Azure AD devuelve una excepción de concesión no válida. Normalmente responde con uno de los dos mensajes de error, `invalid_grant` o `interaction_required`.
3. Cuando se produce un error en el intercambio, debe solicitar consentimiento. Use la interfaz de usuario (UI) para pedir al usuario de la aplicación que conceda otro consentimiento. Esta interfaz de usuario debe incluir un botón que desencadene un cuadro de diálogo de consentimiento de Azure AD mediante [la autenticación silenciosa](~/concepts/authentication/auth-silent-aad.md).
4. Al solicitar más consentimiento de Azure AD, debe incluir `prompt=consent` en el [parámetro query-string-parameter](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) en Azure AD; de lo contrario, Azure AD no pediría otros ámbitos.
    - En lugar de `?scope={scopes}`, use `?prompt=consent&scope={scopes}`
    - Asegúrese de que `{scopes}` incluye todos los ámbitos para los que solicita al usuario, por ejemplo, `Mail.Read` o `User.Read`.
5. Una vez que el usuario de la aplicación haya concedido más permisos, vuelva a intentar el flujo de OBO para obtener acceso a estas otras API.

    </details>

## <a name="see-also"></a>Vea también

- [Flujo en nombre de OAuth 2.0](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow)
- [Obtener acceso para MS Graph](/graph/auth-v2-user)
- [Serialización de caché de tokens en MSAL.NET](/azure/active-directory/develop/msal-net-token-cache-serialization?tabs=aspnet)

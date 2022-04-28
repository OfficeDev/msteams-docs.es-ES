---
title: Compatibilidad con inicio de sesión único para pestañas
description: Describe el inicio de sesión único (SSO)
ms.topic: how-to
ms.localizationpriority: high
keywords: API de inicio de sesión único de Microsoft Azure Active Directory (Azure AD), autenticación SSO de teams
ms.openlocfilehash: d9391489c8bafafa24ba52528f5d0b8440319a55
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104423"
---
# <a name="single-sign-on-sso-support-for-tabs"></a>Compatibilidad con inicio de sesión único (SSO) para pestañas

Los usuarios inician sesión en Microsoft Teams a través de su cuenta profesional, educativa o de Microsoft que es Office 365, Outlook, y puede aprovechar la ventaja al permitir un inicio de sesión único para autorizar su pestaña de Teams o módulo de tareas en clientes de escritorio o móviles. Si un usuario inicia sesión una vez, no tiene que volver a iniciar sesión en otro dispositivo, ya que inicia sesión automáticamente. Además, el token de acceso se captura previamente para mejorar el rendimiento y los tiempos de carga.

> [!NOTE]
> **Versiones de cliente móvil de Teams compatibles con SSO**  
>
> ✔Teams para Android (1416/1.0.0.2020073101 y versiones posteriores)
>
> ✔Teams para iOS (_Versión_: 2.0.18 y versiones posteriores)  
>
> ✔SDK de JavaScript de Teams (_Versión_: 1.11 y posteriores) para que SSO funcione en el panel lateral de la reunión.
>
> Para la mejor experiencia con Teams, use la última versión de iOS y Android.[!NOTE]
> **Inicio rápido**  
>
> La ruta de acceso más sencilla para empezar con la pestaña SSO es con el kit de herramientas de Teams para Microsoft Visual Studio Code. Para obtener más información, consulte [SSO con el kit de herramientas de Teams y Visual Studio Code para pestañas](../../../toolkit/visual-studio-code-tab-sso.md)

<!--- TBD: Edit this article.
* Admonitions/alerts seem to be overused.
* Don't add note for a list of items.
* Don't add numbers to headings.
* Don't copy-paste superscript characters as is. Use HTML entities. See https://sitefarm.ucdavis.edu/training/all/using-wysiwyg/special-characters for the values.
* Same for the check marks added in the content in the note above. The content should not be in a note anyway.
--->

## <a name="how-sso-works-at-runtime"></a>Cómo funciona el SSO en tiempo de ejecución

La siguiente imagen muestra cómo funciona el proceso de SSO:

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. En la pestaña, se realiza una llamada de JavaScript a `getAuthToken()`. `getAuthToken()` indica a Teams que obtenga un token de acceso para la aplicación de pestaña.
2. Si el usuario actual usa la aplicación de pestañas por primera vez, hay una solicitud de consentimiento si es necesario. Como alternativa, hay un mensaje de solicitud para controlar la autenticación de paso a paso, como la autenticación en dos fases.
3. Teams solicita el token de acceso a la pestaña desde el punto de conexión de Azure AD para el usuario actual.
4. Azure AD envía el token de acceso a la pestaña hacia la aplicación de Teams.
5. Teams envía el token de acceso de pestaña a la pestaña como parte del objeto de resultado devuelto por la llamada `getAuthToken()`.
6. El token se analiza en la aplicación de pestaña mediante JavaScript para extraer la información necesaria, como la dirección de correo electrónico del usuario.

> [!NOTE]
> El `getAuthToken()` solo es válido para dar su consentimiento a un conjunto limitado de API de nivel de usuario que son correo electrónico, perfil, offline_access y OpenId. No se usa para otros ámbitos Graph, como `User.Read` o `Mail.Read`. Para obtener soluciones alternativas sugeridas, consulte [Obtener un token de acceso con permisos de Graph](#get-an-access-token-with-graph-permissions).

La API de SSO también funciona en [módulos de tareas](../../../task-modules-and-cards/what-are-task-modules.md) que insertan contenido web.

## <a name="develop-an-sso-microsoft-teams-tab"></a>Desarrollar una pestaña de Microsoft Teams SSO

En esta sección se describen las tareas implicadas en la creación de una pestaña de Teams que usa SSO. Estas tareas son independientes del lenguaje y del marco.

### <a name="1-create-your-azure-ad-application"></a>1. Cree su aplicación de Azure AD

> [!NOTE]
> Hay algunas restricciones importantes que debe conocer:
>
> * Solo se admiten permisos de Graph API de nivel de usuario, es decir, correo electrónico, perfil, offline_access, OpenId. Si debe tener acceso a otros ámbitos Graph, como `User.Read` o `Mail.Read`, consulte [Obtener un token de acceso con permisos de Graph](#get-an-access-token-with-graph-permissions).
> * Es importante que el nombre de dominio de su aplicación sea el mismo que el nombre de dominio que ha registrado para su aplicación de Azure AD.
> * Actualmente, no se admiten varios dominios por aplicación.
> * El usuario debe establecer `accessTokenAcceptedVersion` en `2` para una nueva aplicación.

Para registrar la aplicación a través del portal de Azure AD, siga estos pasos:

1. Registre una nueva aplicación en el portal de [registro de aplicaciones de Azure AD](https://go.microsoft.com/fwlink/?linkid=2083908).
1. Seleccione **Nuevo registro**. Aparece la página **Registrar una aplicación**.
1. En la página **Registrar una aplicación**, escriba los siguientes valores:
    1. Escriba un **nombre** para la aplicación.
    2. Elija los **Tipos de cuenta admitidos**, seleccione un tipo de cuenta de un único espacio empresarial o de varios espacios empresariales. ¹
    * Deje **URI de redireccionamiento** vacía.
    3. Elija **Registrar**.
1. En la página de información general, copie y guarde el **identificador de solicitud (cliente)**. Debe tenerlo más adelante al actualizar el manifiesto de aplicación de Teams.
1. En **Administrar**, seleccione **Exponer una API**

    > [!NOTE]
    >
    > * Si va a compilar una aplicación con un bot y una pestaña, escriba el URI del identificador de aplicación como `api://fully-qualified-domain-name.com/botid-{YourBotId}`.
    >
    > * Use letras minúsculas para el nombre de dominio, no use mayúsculas. Por ejemplo, para crear un servicio de aplicaciones o una aplicación web, escriba el nombre del recurso base como `demoapplication` y, a continuación, la dirección URL será `https://demoapplication.azurewebsites.net`. Pero si usa el nombre del recurso base como `DemoApplication`, la dirección URL será `https://DemoApplication.azurewebsites.net` y esto es compatible con escritorio, web e iOS, pero no Android.

1. Seleccione el vínculo **Establecer** para generar el URI de identificador de aplicación en el formulario `api://{AppID}`. Inserte el nombre de dominio completo con una barra inclinada "/" anexada al final, entre las barras inclinadas dobles y el GUID. El identificador completo debe tener el formato de `api://fully-qualified-domain-name.com/{AppID}`. ² Por ejemplo, `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`. El nombre de dominio completo es el nombre de dominio legible desde el que se sirve la aplicación. Si usa un servicio de tunelización como ngrok, debe actualizar este valor cada vez que cambie el subdominio de ngrok.
1. Seleccione **Agregar un ámbito**. En el panel que se abre, escriba **access_as_user** como **nombre de ámbito**.
1. En el cuadro **¿Quién puede dar su consentimiento?**, escriba **administradores y usuarios**.
1. Escriba los detalles en los cuadros para configurar las solicitudes de consentimiento del administrador y del usuario con los valores adecuados para el ámbito de `access_as_user`:
    * **Título de consentimiento del administrador:** Teams puede acceder al perfil del usuario.
    * **Descripción del consentimiento del administrador**: Teams puede llamar a las API web de la aplicación como el usuario actual.
    * **Título de consentimiento del usuario**: Teams puede acceder a su perfil y realizar solicitudes en su nombre.
    * **Descripción del consentimiento del usuario**: Teams puede llamar a las API de esta aplicación con los mismos derechos que tiene.
1. Asegúrese de que **Estado** se establece en **Habilitado**.
1. Seleccione **Agregar ámbito** para guardar los detalles. La parte de dominio del **nombre de ámbito** que se muestra debajo del campo de texto debe coincidir automáticamente con el URI de **identificador de aplicación** establecido en el paso anterior, con `/access_as_user` anexado al final `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`.
1. En la sección **Aplicaciones cliente autorizadas**, identifique las aplicaciones que quiere autorizar en la aplicación web de la aplicación. Seleccione **Agregar una aplicación cliente**. Escriba cada uno de los siguientes Id. de cliente y seleccione el ámbito autorizado que creó en el paso anterior:
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264` para la aplicación móvil o de escritorio de Teams.
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346` para la aplicación web de Teams.
1. Vaya a **Permisos de API**. Seleccione **Agregar un permiso** > **Microsoft Graph** > **Permisos delegados** y, a continuación, agregue los siguientes permisos desde Graph API:
    * User.Read habilitado de forma predeterminada
    * correo electrónico
    * offline_access
    * OpenID
    * perfil

1. Navegue a **Autenticación**.

    > [!IMPORTANT]
    > Si no se ha concedido el consentimiento del administrador de TI a una aplicación, los usuarios tendrán que dar su consentimiento la primera vez que usen una aplicación.

    Para escribir un URI de redireccionamiento:
    * Seleccione **Agregar una plataforma**.
    * Seleccione **Web**.
    * Escriba el **URI de redireccionamiento** de la aplicación. Este URI es el mismo nombre de dominio completo que escribió en el paso 5. También le sigue la ruta de API a la que se envía una respuesta de autenticación. Si sigue cualquiera de los ejemplos de Teams, el URI es `https://subdomain.example.com/auth-end`. Para obtener más información, consulte [Flujo de código de autorización de OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

    > [!NOTE]
    > La concesión implícita no es necesaria para el SSO de pestaña.

Bien hecho. Ha completado los requisitos previos de registro de la aplicación para continuar con la aplicación SSO de pestaña.

> [!NOTE]
>
> * ¹ Si su aplicación de Azure AD está registrada con el mismo inquilino con el que está haciendo una solicitud de autenticación en Teams, no se puede pedir consentimiento al usuario y concederle un token de acceso inmediatamente. Los usuarios solo dan su consentimiento a estos permisos si la aplicación de Azure AD está registrada en un inquilino diferente.
> * ² Si no se agrega el dominio personalizado en Azure AD, se genera un error que indica que el nombre del host no debe basarse en un dominio que ya se posea. Para agregar un dominio personalizado a Azure AD y registrarlo, siga el procedimiento [agregar un nombre de dominio personalizado a Azure AD](/azure/active-directory/fundamentals/add-custom-domain) y, a continuación, repita el paso 5. También puede obtener este error si no ha iniciado sesión con las credenciales de administrador en el espacio empresarial de Office 365.
> * Si no recibe el nombre principal de usuario (UPN) en el token de acceso devuelto, puede agregarlo como una [notificación opcional](/azure/active-directory/develop/active-directory-optional-claims) en Azure AD

### <a name="2-update-your-teams-application-manifest"></a>2. Actualizar el manifiesto de aplicación de Teams

Use el siguiente código para agregar nuevas propiedades al manifiesto de Teams:

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

* **WebApplicationInfo** es el elemento primario de los siguientes elementos:

> [!div class="checklist"]
>
> * **id**: el Id. de cliente de la aplicación. Este es el identificador de aplicación que obtuvo como parte del registro de la aplicación con Azure AD.
>* **resource**: el dominio y el subdominio de la aplicación. Este es el mismo URI (incluido el protocolo `api://`) que registró al crear el `scope` en el paso 6. No debe incluir la ruta de acceso `access_as_user` en el recurso. La parte de dominio de este identificador URI debe coincidir con el dominio, incluidos los subdominios, que se usan en las direcciones URL del manifiesto de la aplicación de Teams.
> [!NOTE]
>
>* El recurso de una aplicación de Azure AD suele ser la raíz de la dirección URL de su sitio y el appID (por ejemplo, `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`). Este valor también se usa para garantizar que la solicitud procede del mismo dominio. Asegúrese de que el `contentURL` de la pestaña usa los mismos dominios que la propiedad de recurso.
>* Debe usar la versión 1.5 del manifiesto o posterior para implementar el campo `webApplicationInfo`.

### <a name="3-get-an-access-token-from-your-client-side-code"></a>3. Obtener un token de acceso desde el código del lado cliente

> [!NOTE]
> Para evitar errores como `Teams SDK Error: resourceDisabled`, asegúrese de que el URI del identificador de aplicación esté configurado correctamente en el registro de aplicaciones de Azure AD y en la aplicación de Teams.

Use la siguiente API de autenticación:

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

Cuando se llama a `getAuthToken` y se requiere el consentimiento del usuario para los permisos de nivel de usuario, se muestra un cuadro de diálogo al usuario para conceder el consentimiento.

Después de recibir el token de acceso en la devolución de llamada correcta, descodifique el token de acceso para ver las notificaciones de ese token. Opcionalmente, copie y pegue manualmente el token de acceso en una herramienta, como [jwt.ms](https://jwt.ms/). Si no recibe el UPN en el token de acceso devuelto, agréguelo como una [notificación opcional](/azure/active-directory/develop/active-directory-optional-claims) en Azure AD. Para obtener más información, consulte [tokens de acceso](/azure/active-directory/develop/access-tokens).

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="code-snippets"></a>Fragmentos de código

El código siguiente proporciona un ejemplo de flujo con derechos delegados para capturar el token de acceso mediante la biblioteca MSAL:

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

```javascript

// Exchange cliend side token with server token
  app.post('/getProfileOnBehalfOf', function(req, res) {
        var tid = < "Tenand id" >
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

## <a name="code-sample"></a>Ejemplo de código

|**Ejemplo de nombre**|**Descripción**|**C#**|**Node.js**|
|---------------|---------------|------|--------------|
| Inicio de sesión único de pestaña |Aplicación de ejemplo para el SSO para pestañas de Azure AD de Microsoft Teams| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|[Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs), </br>[Kit de herramientas de Teams](../../../toolkit/visual-studio-code-tab-sso.md)|

## <a name="known-limitations"></a>Limitaciones conocidas

### <a name="get-an-access-token-with-graph-permissions"></a>Obtener un token de acceso con permisos de Graph

Nuestra implementación actual para SSO solo concede consentimiento para permisos de nivel de usuario que no se pueden usar para realizar llamadas de Graph. Para obtener los permisos (ámbitos) necesarios para realizar una llamada de Graph, las soluciones de SSO deben implementar un servicio web personalizado para intercambiar el token recibido del SDK de JavaScript de Teams por un token que incluya los ámbitos necesarios. Esto se consigue mediante el [flujo con derechos delegados](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow) de Azure AD.

### <a name="tenant-admin-consent"></a>Consentimiento de administrador de inquilinos

Una forma sencilla de dar su consentimiento en nombre de una organización como administrador de inquilinos es hacer referencia a `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`.

#### <a name="ask-for-consent-using-the-auth-api"></a>Solicitar consentimiento mediante la API de autenticación

Otro enfoque para obtener ámbitos de Graph es presentar un cuadro de diálogo de consentimiento mediante nuestro [enfoque de autenticación de Azure AD basado en web existente.](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page) Este enfoque implica la creación de un cuadro de diálogo de consentimiento de Azure AD.

Para solicitar consentimiento adicional mediante la API de autenticación, siga estos pasos:

1. El token recuperado `getAuthToken()` debe intercambiarse en el lado del servidor mediante el [flujo con derechos delegados](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) de Azure AD para obtener acceso a esas otras API de Graph. Asegúrese de usar el punto de conexión de Graph v2 para este intercambio.
2. Si se produce un error en el intercambio, Azure AD devuelve una excepción de concesión no válida. Normalmente hay uno de los dos mensajes de error, `invalid_grant` o `interaction_required`.
3. Cuando se produce un error en el intercambio, debe solicitar consentimiento. Muestra alguna interfaz de usuario (UI) que pide al usuario que conceda otro consentimiento. Esta interfaz de usuario debe incluir un botón que active un cuadro de diálogo de consentimiento de Azure AD utilizando nuestra [API de autenticación de Azure AD.](~/concepts/authentication/auth-silent-aad.md).
4. Al pedir más consentimiento de Azure AD, debe incluir `prompt=consent` en su [parámetro de consulta](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) a Azure AD; de lo contrario, Azure AD no solicita los demás ámbitos.
    * En lugar de `?scope={scopes}`
    * Use esto `?prompt=consent&scope={scopes}`
    * Asegúrese de que `{scopes}` incluye todos los ámbitos que solicita al usuario, por ejemplo, Mail.Read o User.Read.
5. Una vez que el usuario haya concedido más permisos, vuelva a intentar el flujo en nombre de para obtener acceso a estas otras API.

### <a name="non-azure-ad-authentication"></a>Autenticación sin Azure AD

La solución de autenticación descrita anteriormente solo funciona para aplicaciones y servicios compatibles con Azure AD como proveedor de identidad. Las aplicaciones que deseen autenticarse utilizando servicios no basados en Azure AD deben seguir utilizando el [flujo de autenticación web](~/concepts/authentication.md) basado en ventanas emergentes.

> [!NOTE]
> El SSO es compatible con las aplicaciones propietarias dentro de los inquilinos B2C de Azure AD.

## <a name="step-by-step-guides"></a>Guías paso a paso

* Siga la [guía paso a paso](../../../sbs-tabs-and-messaging-extensions-with-sso.yml) para autenticar las pestañas y las extensiones de mensajería.
* Sigue la [guía paso a paso](../../../sbs-tab-with-adaptive-cards.yml) para crear pestañas con tarjetas adaptables.

## <a name="see-also"></a>Vea también

[Bot de Teams con inicio de sesión único](../../../sbs-bots-with-sso.yml)

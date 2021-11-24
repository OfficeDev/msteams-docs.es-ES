---
title: Compatibilidad con inicio de sesión único para pestañas
description: Describe el inicio de sesión único (SSO)
ms.topic: how-to
ms.localizationpriority: medium
keywords: Autenticación de teams SSO AAD api de inicio de sesión único
ms.openlocfilehash: 96916d526dba7a6ff7b019fb070b53943b3c216c
ms.sourcegitcommit: 345d713a680c0e0978d7f82c0330c1fd0d6b3e7b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/23/2021
ms.locfileid: "61151900"
---
# <a name="single-sign-on-sso-support-for-tabs"></a>Compatibilidad con inicio de sesión único (SSO) para pestañas

Los usuarios inician sesión en Microsoft Teams a través de su cuenta de trabajo, escuela o Microsoft que es Office 365, Outlook, puede aprovechar la ventaja al permitir un inicio de sesión único para autorizar su pestaña o módulo de tareas de Teams en clientes de escritorio o móviles. Si un usuario inicia sesión una vez, no tiene que volver a iniciar sesión en otro dispositivo al iniciar sesión automáticamente. Además, el token de acceso se captura previamente para mejorar el rendimiento y los tiempos de carga.

> [!NOTE]
> **Teams versiones de cliente móvil compatibles con SSO**  
>
> ✔Teams para Android (1416/1.0.0.2020073101 y versiones posteriores)
>
> ✔Teams para iOS (_Versión_: 2.0.18 y versiones posteriores)  
> 
> ✔Teams SDK de JavaScript (_versión_: 1.10 y versiones posteriores) para que SSO funcione en el panel lateral de la reunión. 
>
> Para obtener la mejor experiencia con Teams, usa la versión más reciente de iOS y Android.

> [!NOTE]
> **Inicio rápido**  
>
> La ruta de acceso más sencilla para empezar con la pestaña SSO es con Teams kit de herramientas para Visual Studio Code. Para obtener más información, vea [SSO with Teams toolkit and Visual Studio Code for tabs](../../../toolkit/visual-studio-code-tab-sso.md)

## <a name="how-sso-works-at-runtime"></a>Cómo funciona el SSO en tiempo de ejecución

La siguiente imagen muestra cómo funciona el proceso de SSO:

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. En la pestaña, se realiza una llamada de JavaScript a `getAuthToken()`. `getAuthToken()`indica Teams obtener un token de acceso para la aplicación de tabulación.
2. Si el usuario actual usa la aplicación de tabulación por primera vez, hay una solicitud para dar su consentimiento si es necesario. Como alternativa, hay un mensaje de solicitud para controlar la autenticación de paso a paso, como la autenticación en dos fases.
3. Teams solicita el token de acceso de tabulación desde el punto de Azure Active Directory (AAD) para el usuario actual.
4. AAD envía el token de acceso de tabulación a la Teams aplicación.
5. Teams envía el token de acceso de tabulación a la pestaña como parte del objeto de resultado devuelto por la `getAuthToken()` llamada.
6. El token se analiza en la aplicación de pestaña mediante JavaScript, para extraer la información necesaria, como la dirección de correo electrónico del usuario.

> [!NOTE]
> El solo es válido para dar su consentimiento a un conjunto limitado de API de nivel de usuario que son correo `getAuthToken()` electrónico, perfil, offline_access y OpenId. No se usa para otros ámbitos Graph como `User.Read` o `Mail.Read` . Para obtener soluciones alternativas sugeridas, consulte [Get an access token with Graph permissions](#get-an-access-token-with-graph-permissions).

La API de SSO también funciona en [módulos de tareas](../../../task-modules-and-cards/what-are-task-modules.md) que insertan contenido web.

## <a name="develop-an-sso-microsoft-teams-tab"></a>Desarrollar una pestaña de Microsoft Teams SSO

En esta sección se describen las tareas relacionadas con la creación de una Teams que usa SSO. Estas tareas son independientes del lenguaje y del marco.

### <a name="1-create-your-aad-application"></a>1. Cree su AAD aplicación

**Para registrar la aplicación en la información [general AAD portal](https://azure.microsoft.com/features/azure-portal/)**

1. Obtenga el [identificador AAD de aplicación](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in). 
1. Especifique los permisos que la aplicación necesita para el punto de conexión AAD y, opcionalmente, Graph.
1. [Conceda permisos para](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) Teams escritorio, web y aplicaciones móviles.
1. Pre-authorize Teams seleccionando el botón Agregar **un** ámbito y en el panel que se abre, escriba **access_as_user** como **nombre de ámbito**.

> [!NOTE]
> Hay algunas restricciones importantes que debe saber:
>
> * Solo se admiten permisos Graph API de nivel de usuario, es decir, correo electrónico, perfil, offline_access, OpenId. Si debe tener acceso a otros ámbitos Graph, como o , vea Obtener un token de acceso `User.Read` `Mail.Read` con Graph [permisos](#get-an-access-token-with-graph-permissions).
> * Es importante que el nombre de dominio de la aplicación sea el mismo que el nombre de dominio registrado para la AAD aplicación.
> * Actualmente, no se admiten varios dominios por aplicación.
> * El usuario debe `accessTokenAcceptedVersion` establecerse `2` en para una nueva aplicación.

**Para registrar la aplicación a través del portal AAD web**

1. Registre una nueva aplicación en el portal [AAD registros de aplicaciones.](https://go.microsoft.com/fwlink/?linkid=2083908)
1. Seleccione **Nuevo registro**. Aparece **la página** Registrar una aplicación.
1. En la **página Registrar una aplicación,** escriba los siguientes valores:
    1. Escribe un **nombre** para la aplicación.
    2. Elija los **tipos de cuenta admitidos,** seleccione un único inquilino o tipo de cuenta multiempresa. ¹
    * Deje **URI de redireccionamiento** vacía.
    3. Elija **Registrar**.
1. En la página de información general, copie y guarde el **identificador de aplicación (cliente).** Debe tenerla más adelante al actualizar el manifiesto Teams aplicación.
1. En **Administrar**, seleccione **Exponer una API**

    > [!NOTE]
    > Si estás creando una aplicación con un bot y una pestaña, escribe el URI de id. de aplicación como `api://fully-qualified-domain-name.com/botid-{YourBotId}` .

1. Seleccione el **vínculo Establecer** para generar el URI de id. de aplicación con el formato `api://{AppID}` de . Inserte el nombre de dominio completo con una barra diagonal "/" anexada al final, entre las barras diagonales dobles y el GUID. El identificador completo debe tener el formato `api://fully-qualified-domain-name.com/{AppID}` de . ² Por ejemplo, `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` . El nombre de dominio completo es el nombre de dominio legible desde el que se sirve la aplicación. Si usa un servicio de túnel como ngrok, debe actualizar este valor siempre que cambie su subdominio ngrok.
1. Seleccione **Agregar un ámbito**. En el panel que se abre, **escriba access_as_user** como el nombre **de ámbito**.
1. En el **cuadro Quién puede dar su consentimiento,** escriba **Administradores y usuarios**.
1. Escriba los detalles en los cuadros para configurar los mensajes de consentimiento de usuario y administrador con los valores adecuados para el `access_as_user` ámbito:
    * **Título de consentimiento del administrador:** Teams puede acceder al perfil del usuario.
    * **Descripción del consentimiento** de administrador: Teams puede llamar a las API web de la aplicación como el usuario actual.
    * **Título de consentimiento de** usuario: Teams puede acceder a su perfil y realizar solicitudes en su nombre.
    * Descripción del consentimiento del **usuario:** Teams llamar a las API de esta aplicación con los mismos derechos que tiene.
1. Asegúrese de que **Estado** se establece en **Habilitado**.
1. Seleccione **Agregar ámbito** para guardar los detalles. La parte de dominio del **nombre de** ámbito que se muestra debajo del campo de texto debe coincidir automáticamente con el URI de **id.** de aplicación establecido en el paso anterior, con `/access_as_user` anexado al final `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user` .
1. En la **sección Aplicaciones cliente autorizadas,** identifique las aplicaciones que desea autorizar para la aplicación web de la aplicación. Seleccione **Agregar una aplicación cliente**. Escriba cada uno de los siguientes IDs de cliente y seleccione el ámbito autorizado que creó en el paso anterior:
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264`para Teams móvil o de escritorio.
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346`para Teams web.
1. Vaya a **Permisos de API**. Seleccione **Agregar un permiso** Microsoft  >  **Graph**  >  **permisos delegados** y, a continuación, agregue los siguientes permisos desde Graph API:
    * User.Read habilitado de forma predeterminada
    * correo electrónico
    * offline_access
    * OpenId
    * perfil

1. Vaya a **Autenticación**.

    > [!IMPORTANT]
    > Si no se ha concedido el consentimiento de administrador de TI a una aplicación, los usuarios tendrán que dar su consentimiento la primera vez que usen una aplicación.

    Para escribir un URI de redireccionamiento:
    * Seleccione **Agregar una plataforma**.
    * Seleccione **web**.
    * Escribe el **URI de redireccionamiento** de la aplicación. Este URI es el mismo nombre de dominio completo que escribió en el paso 5. También le sigue la ruta de api en la que se envía una respuesta de autenticación. Si sigue cualquiera de los ejemplos de Teams, el URI es `https://subdomain.example.com/auth-end` . Para obtener más información, vea Flujo de código de autorización de [OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

    > [!NOTE]
    > La concesión implícita no es necesaria para el SSO de tabulación.

¡Enhorabuena! Has completado los requisitos previos de registro de la aplicación para continuar con la aplicación sso de pestaña.

> [!NOTE]
>
> * ¹ Si la aplicación AAD está registrada en el mismo espacio empresarial donde está realizando una solicitud de autenticación en Teams, no se le puede pedir al usuario su consentimiento y se le concede un token de acceso de inmediato. Los usuarios solo consienten estos permisos si la AAD está registrada en un inquilino diferente.
> * ² Si el dominio personalizado no se agrega a AAD, se produce un error que indica que el nombre de host no debe basarse en un dominio ya propiedad. Para agregar un dominio personalizado AAD y registrarlo, siga el procedimiento agregar un nombre de dominio personalizado [a AAD](/azure/active-directory/fundamentals/add-custom-domain) procedimiento y, a continuación, repita el paso 5. También puede obtener este error si no ha iniciado sesión con credenciales de administrador en el Office 365 arrendamiento.
> * Si no recibe el nombre principal de usuario (UPN) en el token de acceso devuelto, puede agregarlo como una notificación opcional [en](/azure/active-directory/develop/active-directory-optional-claims) AAD.

### <a name="2-update-your-teams-application-manifest"></a>2. Actualizar el manifiesto Teams aplicación

Use el siguiente código para agregar nuevas propiedades al manifiesto de Teams:

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

* **WebApplicationInfo** es el elemento principal de los siguientes elementos:

> [!div class="checklist"]
> * **id:** el identificador de cliente de la aplicación. Este es el identificador de aplicación que obtuvo como parte del registro de la aplicación con Azure AD.
>* **resource:** el dominio y el subdominio de la aplicación. Este es el mismo URI (incluido el `api://` protocolo) que registró al crear `scope` el paso 6. No debe incluir la ruta `access_as_user` de acceso en el recurso. La parte de dominio de este URI debe coincidir con el dominio, incluidos los subdominios, que se usan en las direcciones URL del manifiesto Teams aplicación.

> [!NOTE]
>
>* El recurso de una AAD es normalmente la raíz de su dirección URL del sitio y el appID (por ejemplo, `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` ). Este valor también se usa para garantizar que la solicitud viene del mismo dominio. Asegúrese de que `contentURL` la pestaña usa los mismos dominios que la propiedad de recurso.
>* Debe usar la versión 1.5 del manifiesto o posterior para implementar el `webApplicationInfo` campo.

### <a name="3-get-an-access-token-from-your-client-side-code"></a>3. Obtener un token de acceso desde el código del lado cliente

Use la siguiente API de autenticación:

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

Cuando se llama y se requiere el consentimiento del usuario para los permisos de nivel de usuario, se muestra un cuadro de diálogo al usuario `getAuthToken` para conceder el consentimiento.

Después de recibir el token de acceso en la devolución de llamada correcta, descodifica el token de acceso para ver las notificaciones de ese token. Opcionalmente, copie y pegue manualmente el token de acceso en una herramienta, como [jwt.ms](https://jwt.ms/). Si no recibe el UPN en el token de acceso devuelto, agrégrelo como una notificación opcional [en](/azure/active-directory/develop/active-directory-optional-claims) AAD. Para obtener más información, vea [access tokens](/azure/active-directory/develop/access-tokens).

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="code-sample"></a>Ejemplo de código

|**Ejemplo de nombre**|**Descripción**|**C#**|**Node.js**|
|---------------|---------------|------|--------------|
| Tab SSO |Microsoft Teams de ejemplo para pestañas Azure AD SSO| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|[Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs), </br>[Teams Toolkit](../../../toolkit/visual-studio-code-tab-sso.md)|

## <a name="known-limitations"></a>Limitaciones conocidas

### <a name="get-an-access-token-with-graph-permissions"></a>Obtener un token de acceso con Graph permisos

Nuestra implementación actual para SSO solo concede consentimiento para permisos de nivel de usuario que no se pueden usar para realizar Graph llamadas. Para obtener los permisos (ámbitos) necesarios para realizar una llamada Graph, las soluciones de SSO deben implementar un servicio web personalizado para intercambiar el token del SDK de JavaScript de Teams para un token que incluya los ámbitos necesarios. Esto se logra mediante el AAD en [nombre del flujo](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow).

#### <a name="tenant-admin-consent"></a>Consentimiento de administrador de inquilinos

Una forma sencilla de dar su consentimiento en nombre de una organización como administrador de inquilinos es hacer referencia a `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>` .

#### <a name="ask-for-consent-using-the-auth-api"></a>Pedir consentimiento mediante la API de autenticación

Otro enfoque para obtener Graph es presentar un cuadro de diálogo de consentimiento mediante nuestro enfoque de autenticación de Azure AD [web existente.](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page) Este enfoque implica crear un cuadro de Azure AD de diálogo de consentimiento.

**Para solicitar consentimiento adicional mediante la API de autenticación**

1. El token recuperado mediante debe intercambiarse en el servidor mediante AAD en nombre del flujo para obtener acceso a esas otras API Graph `getAuthToken()` servidor. [](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) Asegúrese de usar el punto de conexión Graph v2 para este intercambio.
2. Si se produce un error en el intercambio, AAD devuelve una excepción de concesión no válida. Normalmente hay uno de los dos mensajes de error o `invalid_grant` `interaction_required` .
3. Cuando se produce un error en el intercambio, debe solicitar el consentimiento. Muestra una interfaz de usuario (UI) que pide al usuario que conceda otro consentimiento. Esta interfaz de usuario debe incluir un botón que active un cuadro de diálogo AAD de consentimiento mediante nuestra API AAD [autenticación](~/concepts/authentication/auth-silent-aad.md).
4. Al solicitar más consentimiento de AAD, debe incluir en el `prompt=consent` [parámetro query-string-parameter](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) para AAD, de lo contrario AAD no pide los otros ámbitos.
    * En lugar de `?scope={scopes}`
    * Use esta opción `?prompt=consent&scope={scopes}`
    * Asegúrese de que incluye todos los ámbitos que está solicitando al usuario, por `{scopes}` ejemplo, Mail.Read o User.Read.
5. Una vez que el usuario haya concedido más permisos, vuelva a intentar el flujo en nombre del flujo para obtener acceso a estas otras API.

### <a name="non-aad-authentication"></a>Autenticación sin AAD de usuario

La solución de autenticación descrita anteriormente solo funciona para aplicaciones y servicios que admiten AAD como proveedor de identidades. Las aplicaciones que desean autenticarse mediante servicios no AAD basados en archivos deben seguir usando el flujo de autenticación [web basado en elementos emergentes](~/concepts/authentication.md).

> [!NOTE]
> Sso es compatible con aplicaciones de propiedad del cliente dentro de AAD inquilinos B2C.

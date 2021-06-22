---
title: Compatibilidad con inicio de sesión único para pestañas
description: Describe el inicio de sesión único (SSO)
ms.topic: how-to
localization_priority: Normal
keywords: API de inicio de sesión único de SSO AAD de autenticación de teams
ms.openlocfilehash: 1e26189a9a04991c2ad384e58f4fd6d68ca69b6d
ms.sourcegitcommit: 3d02dfc13331b28cffba42b39560cfeb1503abe2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/22/2021
ms.locfileid: "53049039"
---
# <a name="single-sign-on-sso-support-for-tabs"></a>Compatibilidad con inicio de sesión único (SSO) para pestañas

Los usuarios inician sesión Microsoft Teams a través de sus cuentas de trabajo, escuela o Microsoft que Office 365, Outlook, y así sucesivamente. Puede aprovechar esta ventaja al permitir que un inicio de sesión único autorice su pestaña o módulo de tareas Teams de escritorio o móvil. Si un usuario da su consentimiento para usar la aplicación, no tiene que volver a dar su consentimiento en otro dispositivo, ya que ha iniciado sesión automáticamente. Además, el token de acceso está predefinido para mejorar el rendimiento y los tiempos de carga.

> [!NOTE]
> **Teams versiones de cliente móvil compatibles con SSO**  
>
> ✔Teams para Android (1416/1.0.0.2020073101 y versiones posteriores)
>
> ✔Teams para iOS (_Versión_: 2.0.18 y versiones posteriores)  
>
> Para obtener la mejor experiencia con Teams, usa la versión más reciente de iOS y Android.

> [!NOTE]
> **Inicio rápido**  
>
> La ruta de acceso más sencilla para empezar con sso de pestaña es con el kit de herramientas Teams para Visual Studio Code. Para obtener más información, vea [SSO with Teams toolkit and Visual Studio Code for tabs](../../../toolkit/visual-studio-code-tab-sso.md)

## <a name="how-sso-works-at-runtime"></a>Cómo funciona el SSO en tiempo de ejecución

La siguiente imagen muestra cómo funciona el proceso de SSO:

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. En la pestaña, se realiza una llamada de JavaScript a `getAuthToken()` . Esto indica Teams obtener un token de autenticación para la aplicación de tabulación.
2. Si es la primera vez que el usuario actual usa la aplicación de pestaña, hay un mensaje de solicitud para dar su consentimiento si se requiere consentimiento o para administrar la autenticación de paso a paso, como la autenticación en dos fases.
3. Teams solicita el token de aplicación de tabulación desde el punto de conexión Azure Active Directory (AAD) para el usuario actual.
4. AAD envía el token de aplicación de tabulación a Teams aplicación.
5. Teams envía el token de aplicación de tabulación a la pestaña como parte del objeto de resultado devuelto por la `getAuthToken()` llamada.
6. El token se analiza en la aplicación de pestaña mediante JavaScript, para extraer la información necesaria, como la dirección de correo electrónico del usuario.

> [!NOTE]
> El solo es válido para dar su consentimiento a un conjunto limitado de API de nivel de usuario que son correo `getAuthToken()` electrónico, perfil, offline_access y OpenId. No se usa para otros ámbitos Graph como `User.Read` o `Mail.Read` . Para obtener soluciones alternativas sugeridas, [consulte Graph adicionales](#apps-that-require-additional-graph-scopes).

La API de SSO también funciona en [módulos de tareas](../../../task-modules-and-cards/what-are-task-modules.md) que insertan contenido web.

## <a name="develop-an-sso-microsoft-teams-tab"></a>Desarrollar una pestaña de Microsoft Teams SSO

En esta sección se describen las tareas relacionadas con la creación de una Teams que usa SSO. Estas tareas son independientes del lenguaje y del marco.

### <a name="1-create-your-aad-application"></a>1. Crear la aplicación de AAD

**Para registrar la aplicación en la información general [del portal de AAD](https://azure.microsoft.com/features/azure-portal/)**

1. Obtener el [identificador de aplicación de AAD](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in). 
1. Especifique los permisos que la aplicación necesita para el extremo de AAD y, opcionalmente, Graph.
1. [Conceda permisos para](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) Teams escritorio, web y aplicaciones móviles.
1. Pre-authorize Teams seleccionando el botón Agregar **un** ámbito y en el panel que se abre, escriba **access_as_user** como **nombre de ámbito**.

> [!NOTE]
> Hay algunas restricciones importantes que debe saber:
>
> * Solo se admiten permisos Graph API de nivel de usuario, es decir, correo electrónico, perfil, offline_access, OpenId. Si debe tener acceso a otros ámbitos Graph como `User.Read` o , vea la solución alternativa `Mail.Read` [recomendada](#apps-that-require-additional-graph-scopes).
> * Es importante que el nombre de dominio de la aplicación sea el mismo que el nombre de dominio registrado para la aplicación de AAD.
> * Actualmente, no se admiten varios dominios por aplicación.

**Para registrar la aplicación a través del portal de AAD**

1. Registrar una nueva aplicación en el portal [de registros de aplicaciones de AAD.](https://go.microsoft.com/fwlink/?linkid=2083908)
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
    * **Título del consentimiento de administrador:** Teams puede acceder al perfil del usuario.
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
    * email
    * offline_access
    * OpenId
    * perfil

1. Vaya a **Autenticación**.

    Si no se ha concedido el consentimiento de administrador de TI a una aplicación, los usuarios tendrán que dar su consentimiento la primera vez que usen una aplicación.

    Para escribir un URI de redireccionamiento:
    * Seleccione **Agregar una plataforma**.
    * Seleccione **web**.
    * Escribe el **URI de redireccionamiento** de la aplicación. Esta es la página donde un flujo de concesión implícito correcto redirige al usuario. Este es el mismo nombre de dominio completo que escribió en el paso 5 seguido de la ruta de api a la que se envía una respuesta de autenticación. Si está siguiendo cualquiera de los ejemplos Teams, este es `https://subdomain.example.com/auth-end` .

    Habilite la concesión implícita activando los siguientes cuadros: ✔ token de identificador ✔ token de acceso

¡Enhorabuena! Has completado los requisitos previos de registro de la aplicación para continuar con la pestaña APLICACIÓN SSO.

> [!NOTE]
>
> * ¹ Si la aplicación de AAD está registrada en el mismo espacio empresarial donde realiza una solicitud de autenticación en Teams, no se le puede pedir al usuario su consentimiento y se le concede un token de acceso de inmediato. Los usuarios solo consienten estos permisos si la aplicación AAD está registrada en un inquilino diferente.
> * ² Si el dominio personalizado no se agrega a AAD, se produce un error que indica que el nombre de host no debe basarse en un dominio ya propiedad. Para agregar un dominio personalizado a AAD y registrarlo, siga el procedimiento agregar un nombre de dominio [personalizado al procedimiento de AAD](/azure/active-directory/fundamentals/add-custom-domain) y, a continuación, repita el paso 5. También puede obtener este error si no ha iniciado sesión con credenciales de administrador en el Office 365 arrendamiento.
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
>* El recurso de una aplicación de AAD suele ser la raíz de la dirección URL del sitio y el appID (por ejemplo, `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` ). Este valor también se usa para garantizar que la solicitud viene del mismo dominio. Asegúrese de que `contentURL` la pestaña usa los mismos dominios que la propiedad de recurso.
>* Debe usar la versión 1.5 del manifiesto o posterior para implementar el `webApplicationInfo` campo.

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a>3. Obtener un token de autenticación del código del lado cliente

Use la siguiente API de autenticación:

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

Al llamar: y se requiere un consentimiento de usuario adicional para los permisos de nivel de usuario, se muestra un cuadro de diálogo al usuario `getAuthToken` para conceder un consentimiento adicional.

Después de recibir el token de acceso en la devolución de llamada correcta, puede descodificar el token de acceso para ver las notificaciones asociadas con ese token. Opcionalmente, puedes copiar y pegar manualmente el token de acceso en una herramienta, como jwt.ms [inspeccionar](https://jwt.ms/) su contenido. Si no recibe el UPN en el token de acceso devuelto, puede agregarlo como una notificación [opcional](/azure/active-directory/develop/active-directory-optional-claims) en AAD.

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="code-sample"></a>Ejemplo de código

|**Nombre de ejemplo**|**Description**|**C#**|**Node.js**|
|---------------|---------------|------|--------------|
| Tab SSO |Microsoft Teams de ejemplo para pestañas SSO de Azure AD| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|[Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs), </br>[Teams Toolkit](../../../toolkit/visual-studio-code-tab-sso.md)|

## <a name="known-limitations"></a>Limitaciones conocidas

### <a name="apps-that-require-additional-graph-scopes"></a>Aplicaciones que requieren ámbitos Graph adicionales

Nuestra implementación actual para SSO solo concede consentimiento para permisos de nivel de usuario que son correo electrónico, perfil, offline_access, OpenId y no para otras API como User.Read o Mail.Read. Si la aplicación necesita más Graph ámbitos, en la siguiente sección se proporcionan algunas soluciones alternativas de habilitación.

#### <a name="tenant-admin-consent"></a>Consentimiento de administrador de inquilinos

El enfoque más sencillo es conseguir que un administrador de inquilinos preconsiente en nombre de la organización. Esto significa que los usuarios no tienen que dar su consentimiento a estos ámbitos y, a continuación, puede intercambiar el lado del servidor de tokens con el flujo en nombre [de](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)AAD. Esta solución alternativa es aceptable para aplicaciones internas de línea de negocio, pero no es suficiente para desarrolladores de terceros que no pueden confiar en la aprobación del administrador de inquilinos.

Una forma sencilla de dar su consentimiento en nombre de una organización como administrador de inquilinos es hacer referencia a `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>` .

#### <a name="ask-for-additional-consent-using-the-auth-api"></a>Solicitar consentimiento adicional mediante la API de autenticación

Otro enfoque para obtener ámbitos Graph adicionales es presentar un cuadro de diálogo de consentimiento mediante nuestro enfoque de autenticación de [Azure AD](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) basado en web existente, que implica crear un cuadro de diálogo de consentimiento de Azure AD. 

**Para solicitar consentimiento adicional mediante la API de autenticación**

1. El token recuperado mediante debe intercambiarse en el lado servidor mediante AAD en nombre del flujo para obtener acceso a esas API de Graph `getAuthToken()` adicionales. [](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) Asegúrese de usar el punto de conexión Graph v2 para este intercambio.
2. Si se produce un error en el intercambio, AAD devuelve una excepción de concesión no válida. Normalmente hay uno de los dos mensajes de error o `invalid_grant` `interaction_required` .
3. Cuando se produce un error en el intercambio, debe solicitar el consentimiento adicional. Muestra una interfaz de usuario (UI) que pide al usuario que conceda un consentimiento adicional. Esta interfaz de usuario debe incluir un botón que active un cuadro de diálogo de consentimiento de AAD mediante nuestra [API de autenticación de AAD](~/concepts/authentication/auth-silent-aad.md).
4. Al solicitar el consentimiento adicional de AAD, debe incluir en el parámetro `prompt=consent` [query-string-parameter](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) a AAD, de lo contrario, AAD no pide los ámbitos adicionales.
    * En lugar de `?scope={scopes}`
    * Use esta opción `?prompt=consent&scope={scopes}`
    * Asegúrese de que incluye todos los ámbitos que está solicitando al usuario, por `{scopes}` ejemplo, Mail.Read o User.Read.
5. Una vez que el usuario haya concedido permisos adicionales, vuelva a intentar el flujo en nombre del usuario para obtener acceso a estas API adicionales.

### <a name="non-aad-authentication"></a>Autenticación que no es AAD

La solución de autenticación descrita anteriormente solo funciona para aplicaciones y servicios que admiten AAD como proveedor de identidades. Las aplicaciones que quieran autenticarse con servicios no basados en AAD deben seguir usando el flujo de autenticación web basado [en elementos emergentes](~/concepts/authentication.md).

> [!NOTE]
> Sso es compatible con aplicaciones de propiedad del cliente dentro de los inquilinos de AAD B2C.

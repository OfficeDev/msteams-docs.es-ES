---
title: Compatibilidad con inicio de sesión único para pestañas
description: Describe el inicio de sesión único (SSO)
ms.topic: how-to
keywords: API de inicio de sesión único de SSO AAD de autenticación de teams
ms.openlocfilehash: 7b8406473b8356b9c26948641b49f7e1239e697a
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449265"
---
# <a name="single-sign-on-sso-support-for-tabs"></a>Compatibilidad con inicio de sesión único (SSO) para pestañas

Los usuarios inician sesión en Microsoft Teams a través de sus cuentas profesionales, educativas o microsoft (Office 365, Outlook, etc.). Puedes aprovechar esto al permitir que un inicio de sesión único autorice la pestaña de Microsoft Teams (o módulo de tareas) en clientes móviles o de escritorio. Por lo tanto, si un usuario da su consentimiento para usar la aplicación, no tendrá que dar su consentimiento de nuevo en otro dispositivo, sino que se iniciará sesión automáticamente. Además, se busca previamente el token de acceso para mejorar el rendimiento y los tiempos de carga.

> [!NOTE]
> **Versiones de cliente móvil de Teams que admiten SSO**  
>
> ✔Teams para Android (1416/1.0.0.2020073101 y versiones posteriores)
>
> ✔Teams para iOS (_Versión_: 2.0.18 y versiones posteriores)  
>
> Para disfrutar de la mejor experiencia con Teams, usa la versión más reciente de iOS y Android.

> [!NOTE]
> **Inicio rápido**  
>
> La ruta de acceso más sencilla para empezar con sso de pestaña es con Microsoft Teams Toolkit para Visual Studio código. [Más información](../../../toolkit/visual-studio-code-tab-sso.md)

## <a name="how-sso-works-at-runtime"></a>Cómo funciona el SSO en tiempo de ejecución

En el siguiente diagrama se muestra cómo funciona el proceso de SSO:

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. En la pestaña, se realiza una llamada de JavaScript a `getAuthToken()` . Esto indica a Teams que obtenga un token de autenticación para la aplicación de pestaña.
2. Si es la primera vez que el usuario actual usa la aplicación de pestaña, habrá un mensaje de solicitud para dar su consentimiento (si es necesario el consentimiento) o para administrar la autenticación de paso a paso (como la autenticación en dos fases).
3. Teams solicita el token de aplicación de pestaña del punto de conexión de Azure AD para el usuario actual.
4. Azure AD envía el token de aplicación de pestaña a la aplicación teams.
5. Teams envía el token de aplicación de pestaña a la pestaña como parte del objeto de resultado devuelto por la `getAuthToken()` llamada.
6. El token se analizará en la aplicación de pestaña, a través de JavaScript, para extraer la información necesaria, como la dirección de correo electrónico del usuario.

> [!NOTE]
> El solo es válido para dar su consentimiento a un conjunto limitado de API de nivel de usuario `getAuthToken()` (correo electrónico, perfil, offline_access y OpenId) y no para otros ámbitos de Microsoft Graph como `User.Read` o `Mail.Read` . Consulte nuestra sección al final de este documento para obtener soluciones alternativas sugeridas si necesita [ámbitos de Graph adicionales.](#apps-that-require-additional-microsoft-graph-scopes)

La API de SSO también funcionará en [módulos de tareas](../../../task-modules-and-cards/what-are-task-modules.md) que insertan contenido web.

## <a name="develop-an-sso-microsoft-teams-tab"></a>Desarrollar una pestaña sso de Microsoft Teams

En esta sección se describen las tareas relacionadas con la creación de una pestaña de Teams que usa SSO. Estas tareas se describen aquí que son independientes del lenguaje y del marco.

### <a name="1-create-your-azure-active-directory-azure-ad-application"></a>1. Crear la aplicación de Azure Active Directory (Azure AD)

#### <a name="registering-your-application-in-theazure-ad-portal-overview"></a>Registro de la aplicación en la introducción[al portal de Azure AD:](https://azure.microsoft.com/features/azure-portal/)

1. Obtener el identificador [de aplicación de Azure AD](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).
2. Especifica los permisos que la aplicación necesita para el punto de conexión de Azure AD y, opcionalmente, Microsoft Graph.
3. [Conceder permisos para](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) aplicaciones de escritorio, web y móviles de Teams.
4. Para autorizar previamente Teams, seleccione el botón Agregar **un** ámbito y, en el panel que se abre, escriba `access_as_user` como nombre de **ámbito**.

> [!NOTE]
> Hay algunas restricciones importantes que debe tener en cuenta:
>
> * Solo se admiten permisos de api de Microsoft Graph de nivel de usuario, es decir, correo electrónico, perfil, offline_access, OpenId. Si necesita acceso a otros ámbitos de Microsoft Graph (por ejemplo, o ), consulte nuestra solución alternativa recomendada `User.Read` al final de esta `Mail.Read` documentación. [](#apps-that-require-additional-microsoft-graph-scopes)
> * Es importante que el nombre de dominio de la aplicación sea el mismo que el nombre de dominio que registró para la aplicación de Azure AD.
> * Actualmente no se admiten varios dominios por aplicación.
> * No se admiten aplicaciones que usan el `azurewebsites.net` dominio porque es demasiado común y puede ser un riesgo de seguridad. Sin embargo, estamos buscando activamente eliminar esta restricción.

#### <a name="registering-your-app-through-the-azure-active-directory-portal-in-depth"></a>Registrar la aplicación a través del portal de Azure Active Directory en profundidad:

1. Registrar una nueva aplicación en el [portal Azure Active Directory – Registros de aplicaciones.](https://go.microsoft.com/fwlink/?linkid=2083908)
2. Seleccione **Nuevo registro** y, en la página Registrar una *aplicación,* establezca los siguientes valores:
    * Establece **el nombre** en el nombre de la aplicación.
    * Elegir los **tipos de cuenta admitidos** (cualquier tipo de cuenta funcionará) ¹
    * Deje **URI de redireccionamiento** vacía.
    * Elija **Registrar**.
3. En la página de información general, copie y guarde el **identificador de aplicación (cliente).** Lo necesitarás más adelante al actualizar el manifiesto de la aplicación de Teams.
4. En **Administrar**, seleccione **Exponer una API** 
5. Seleccione el **vínculo Establecer** para generar el URI de id. de aplicación con el formato `api://{AppID}` de . Inserte el nombre de dominio completo (con una barra diagonal "/" anexada al final) entre las barras diagonales dobles y el GUID. El identificador completo debe tener la forma de: `api://fully-qualified-domain-name.com/{AppID}` ²
    * ex: `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` .
    
    El nombre de dominio completo es el nombre de dominio legible desde el que se sirve la aplicación. Si usa un servicio de túnel como ngrok, deberá actualizar este valor siempre que cambie el subdominio ngrok. 
6. Seleccione el botón **Agregar un ámbito** En el panel que se abre, escriba `access_as_user` como el **Nombre de ámbito**.
7. Establecer **¿Quién puede dar su consentimiento?**`Admins and users`
8. Rellene los campos para configurar los mensajes de consentimiento de administrador y usuario con los valores adecuados para el `access_as_user` ámbito:
    * **Título del consentimiento de administrador:** Teams puede tener acceso al perfil del usuario.
    * **Descripción del consentimiento de administrador:** permite a Teams llamar a las API web de la aplicación como el usuario actual.
    * **Título de consentimiento de** usuario: Teams puede tener acceso al perfil de usuario y realizar solicitudes en nombre del usuario.
    * **Descripción del consentimiento del usuario:** Habilita Teams para llamar a las API de esta aplicación con los mismos derechos que el usuario.
9. Asegúrese de **que el estado** está establecido en **Habilitado**
10. Seleccione el **botón Agregar ámbito** para guardar 
    * La parte de  dominio del nombre de ámbito que se muestra justo debajo del campo de texto debe coincidir automáticamente con el URI de **id.** de aplicación establecido en el paso anterior, con anexado `/access_as_user` al final:
        * `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`
11. En la **sección Aplicaciones cliente autorizadas,** identifique las aplicaciones que desea autorizar para la aplicación web de la aplicación. Seleccione *Agregar una aplicación cliente*. Escriba cada uno de los siguientes IDs de cliente y seleccione el ámbito autorizado que creó en el paso anterior:
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264` (Aplicación móvil/de escritorio de Teams)
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346` (aplicación web de Teams)
12. Vaya a **Permisos de API**. Seleccione *Agregar permisos delegados* de Microsoft Graph y, a continuación,  >    >  agregue los siguientes permisos de la API de Microsoft Graph:
    * User.Read (habilitado de forma predeterminada)
    * correo electrónico
    * offline_access
    * OpenId
    * perfil

13. Vaya a **Autenticación**

    Si no se ha concedido el consentimiento de administrador de TI a una aplicación, los usuarios tendrán que dar su consentimiento la primera vez que usen una aplicación.

    Establecer un URI de redireccionamiento:
    * Seleccione **Agregar una plataforma**.
    * Seleccione **web**.
    * Escribe el **URI de redireccionamiento** de la aplicación. Esta será la página donde un flujo de concesión implícito correcto redirigirá al usuario. Este será el mismo nombre de dominio completo que escribió en el paso 5 seguido de la ruta de api donde se debe enviar una respuesta de autenticación. Si sigue cualquiera de los ejemplos de Teams, esto será: `https://subdomain.example.com/auth-end`

    A continuación, habilite la concesión implícita activando las siguientes casillas:  
    ✔ token de id.  
    ✔ token de acceso  
    
¡Enhorabuena! Has completado los requisitos previos de registro de la aplicación para continuar con la pestaña APLICACIÓN SSO.     

> [!NOTE]
>
> * ¹ Si la aplicación de  Azure AD está registrada en el mismo espacio empresarial donde está realizando una solicitud de autenticación en Teams, no se le pedirá al usuario su consentimiento y se le concederá un token de acceso de inmediato. Los usuarios solo necesitan dar su consentimiento a estos permisos si la aplicación de Azure AD está registrada en un inquilino diferente.
> * ² Si recibe un error que indica que el dominio ya es propiedad y que es el propietario, siga el procedimiento de [Inicio rápido:](/azure/active-directory/fundamentals/add-custom-domain) Agregue un nombre de dominio personalizado a Azure Active Directory para registrar el dominio y repita el paso 5 anterior. (Este error también puede producirse si no ha iniciado sesión con credenciales de administrador en el arrendamiento de Office 365).
> * Si no recibe el UPN (nombre principal de usuario) en el token de acceso devuelto, puede agregarlo como una notificación opcional [en](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) Azure AD.

### <a name="2-update-your-microsoft-teams-application-manifest"></a>2. Actualizar el manifiesto de la aplicación de Microsoft Teams

Agregue nuevas propiedades al manifiesto de Microsoft Teams:

* **WebApplicationInfo:** el elemento primario de los siguientes elementos:

> [!div class="checklist"]
> * **id:** el identificador de cliente de la aplicación. Este es el identificador de aplicación que obtuvo como parte del registro de la aplicación con Azure AD.
>* **resource:** el dominio y el subdominio de la aplicación. Este es el mismo URI (incluido el `api://` protocolo) que registró al crear el paso `scope` 6 anterior. No debe incluir la ruta `access_as_user` de acceso en el recurso. La parte de dominio de este URI debe coincidir con el dominio, incluidos los subdominios, que se usan en las direcciones URL del manifiesto de la aplicación de Teams.

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

> [!NOTE]
>
>* El recurso de una aplicación de AAD suele ser la raíz de su dirección URL del sitio y el appID (por ejemplo, `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` ). También usamos este valor para garantizar que la solicitud viene del mismo dominio. Por lo tanto, asegúrese de que `contentURL` la pestaña para use los mismos dominios que la propiedad de recurso.
>* Debe usar la versión de manifiesto 1.5 o posterior para implementar el `webApplicationInfo` campo.

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a>3. Obtener un token de autenticación del código del lado cliente

Este es el aspecto de la API de autenticación:

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

Cuando llame y se requiera un consentimiento de usuario adicional (para permisos de nivel de usuario), se mostrará un cuadro de diálogo al usuario que le animará a conceder `getAuthToken` un consentimiento adicional. 

Después de recibir el token de acceso en la devolución de llamada correcta, puede descodificar el token de acceso para ver las notificaciones asociadas con ese token. Opcionalmente, puedes copiar y pegar manualmente el token de acceso en una herramienta, como jwt.ms [inspeccionar](https://jwt.ms/) su contenido. Si no recibe el nombre principal de usuario (UPN) en el token de acceso devuelto, puede agregarlo como una notificación opcional [en](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) Azure AD.

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="code-sample"></a>Ejemplo de código

|**Nombre de ejemplo**|**Descripción**|**C#**|**TypeScript**|
|---------------|---------------|------|--------------|
| Tab SSO |Aplicación de ejemplo de Microsoft Teams para pestañas SSO de Azure AD| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|[Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs), </br>[Kit de herramientas de Teams](../../../toolkit/visual-studio-code-tab-sso.md)|

## <a name="known-limitations"></a>Limitaciones conocidas

### <a name="apps-that-require-additional-microsoft-graph-scopes"></a>Aplicaciones que requieren ámbitos de Microsoft Graph adicionales

Nuestra implementación actual para SSO solo concede consentimiento para permisos de nivel de usuario (correo electrónico, perfil, offline_access, OpenId) no para otras API (como User.Read o Mail.Read). Si la aplicación necesita más ámbitos de Microsoft Graph, estas son algunas soluciones alternativas de habilitación:

#### <a name="tenant-admin-consent"></a>Consentimiento de administrador de inquilinos

El enfoque más sencillo es conseguir que un administrador de inquilinos preconsiente en nombre de la organización. Esto significa que los usuarios no tendrán que dar su consentimiento a estos ámbitos y, a continuación, puede intercambiar el lado del servidor de tokens con el flujo en nombre [del flujo](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)de Azure AD. Esta solución alternativa es aceptable para aplicaciones de línea de negocio internas, pero puede que no sea suficiente para desarrolladores de terceros que no puedan confiar en la aprobación del administrador de inquilinos.

Una forma sencilla de dar su consentimiento en nombre de una organización (como administrador de inquilinos) es visitar:

* `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`

#### <a name="asking-for-additional-consent-using-the-auth-api"></a>Pedir consentimiento adicional mediante la API de autenticación

Otro enfoque para obtener ámbitos adicionales de Microsoft Graph es presentar un cuadro de diálogo de consentimiento con nuestro enfoque de autenticación de [Azure AD](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) basado en web existente, que implica crear un cuadro de diálogo de consentimiento de Azure AD. Hay algunas adiciones notables:

1. El token recuperado mediante debe intercambiarse en el lado servidor con Azure AD en nombre del flujo para obtener acceso a esas API `getAuthToken()` de Microsoft Graph adicionales. [](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow)
    * Asegúrese de usar el punto de conexión de Microsoft Graph v2 para este exchange
2. Si se produce un error en exchange, Azure AD devolverá una excepción de concesión no válida. Normalmente hay uno de dos mensajes de error: `invalid_grant` o `interaction_required`
3. Cuando se produce un error en el intercambio, debe solicitar el consentimiento adicional. Se recomienda mostrar una interfaz de usuario que pida al usuario que conceda un consentimiento adicional. Esta interfaz de usuario debe incluir un botón que active un cuadro de diálogo de consentimiento de Azure AD mediante nuestra API de autenticación [de Azure AD](~/concepts/authentication/auth-silent-aad.md).
4. Al solicitar el consentimiento adicional de Azure AD, debe incluir en el parámetro `prompt=consent` [query-string-parameter](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) a Azure AD de lo contrario Azure AD no pedirá los ámbitos adicionales.
    * En lugar de: `?scope={scopes}`
    * Use esto: `?prompt=consent&scope={scopes}`
    * Asegúrese de que incluye todos los ámbitos que está solicitando al usuario `{scopes}` (por ejemplo: Mail.Read o User.Read).
5. Una vez que el usuario haya concedido permisos adicionales, vuelva a intentar el flujo en nombre del usuario para obtener acceso a estas API adicionales.

### <a name="non-azure-ad-authentication"></a>Autenticación que no es de Azure AD

La solución de autenticación descrita anteriormente solo funciona para aplicaciones y servicios que admiten Azure AD como proveedor de identidades. Las aplicaciones que quieran autenticarse con servicios no basados en Azure AD deben seguir usando el flujo de autenticación web basado [en elementos emergentes](~/concepts/authentication.md).

> [!NOTE] 
> Sso es compatible con aplicaciones de propiedad del cliente dentro de los inquilinos de Azure AD B2C.

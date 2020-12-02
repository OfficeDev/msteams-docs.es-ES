---
title: Compatibilidad de inicio de sesión único para pestañas
description: Describe el inicio de sesión único (SSO)
keywords: API de autenticación de Microsoft Teams SSO de inicio de sesión único de AAD
ms.openlocfilehash: 08ad1ab55a06ccb887755322fbd572f745952d8e
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552454"
---
# <a name="single-sign-on-sso-support-for-tabs"></a>Compatibilidad de inicio de sesión único (SSO) para pestañas

Los usuarios inician sesión en Microsoft Teams a través de sus cuentas de trabajo, centro educativo o Microsoft (Office 365, Outlook, etc.). Puede beneficiarse de esto si permite que un único inicio de sesión autorice la pestaña de Microsoft Teams (o el módulo de tareas) en clientes móviles o de escritorio. Por lo tanto, si un usuario consiente usar la aplicación, no tendrá que volver a dar su consentimiento en otro dispositivo, sino que se iniciará sesión automáticamente. Además, recuperamos previamente el token de acceso para mejorar el rendimiento y los tiempos de carga.

>[!NOTE]
> **Teams versiones de cliente móviles compatibles con SSO**  
>
> ✔ Teams para Android (1416/1.0.0.2020073101 y versiones posteriores)
>
> ✔ Teams para iOS (_versión_: 2.0.18 y versiones posteriores)  
>
> Para obtener la mejor experiencia con Microsoft Teams, use la versión más reciente de iOS y Android.

>[!NOTE]
> **Inicio rápido**  
>
> La ruta más sencilla para empezar con el SSO de pestañas es con el kit de herramientas de Microsoft Teams para Visual Studio Code. [Más información](../../../toolkit/visual-studio-code-tab-sso.md)


## <a name="how-sso-works-at-runtime"></a>Cómo funciona el SSO en tiempo de ejecución

El siguiente diagrama muestra cómo funciona el proceso de SSO:

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. En la pestaña, se realiza una llamada de JavaScript `getAuthToken()` . Esto indica a teams que debe obtener un token de autenticación para la aplicación de pestañas.
2. Si esta es la primera vez que el usuario actual ha usado la aplicación de pestañas, se le pedirá una solicitud de consentimiento (si se requiere consentimiento) o para controlar la autenticación de paso a través (por ejemplo, la autenticación en dos fases).
3. Microsoft Teams solicita el token de aplicación de pestañas del punto de conexión de Azure AD para el usuario actual.
4. Azure AD envía el token de aplicación de la pestaña a la aplicación Teams.
5. Microsoft Teams envía el token de la aplicación de la pestaña como parte del objeto de resultado devuelto por la `getAuthToken()` llamada.
6. El token se analizará en la aplicación de pestañas, a través de JavaScript, para extraer la información necesaria, como la dirección de correo electrónico del usuario.

> [!NOTE]
> El `getAuthToken()` solo es válido para conformar a un conjunto limitado de API de nivel de usuario (email, Profile, offline_access y OpenID) y no para más ámbitos de Microsoft Graph, como `User.Read` o `Mail.Read` . Consulte nuestra sección al final de este documento para obtener soluciones alternativas si necesita [ámbitos de gráficos adicionales](#apps-that-require-additional-microsoft-graph-scopes).

La API de SSO también funcionará en [módulos de tareas](../../../task-modules-and-cards/what-are-task-modules.md) que incrusten contenido Web.

## <a name="develop-an-sso-microsoft-teams-tab"></a>Desarrollar una pestaña de Microsoft Teams de SSO

En esta sección se describen las tareas necesarias para crear una pestaña de Microsoft teams que use SSO. Estas tareas se describen a continuación: independiente del marco y del idioma.

### <a name="1-create-your-azure-active-directory-azure-ad-application"></a>1. crear la aplicación de Azure Active Directory (Azure AD)

#### <a name="registering-your-application-in-theazure-ad-portal-overview"></a>Registrar la aplicación en el[portal de Azure ad](https://azure.microsoft.com/features/azure-portal/) información general:

1. Obtener el [identificador de la aplicación de Azure ad](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).
2. Especifique los permisos que necesita la aplicación para el punto de conexión de Azure AD y, opcionalmente, Microsoft Graph.
3. [Conceda permisos](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) para equipos de escritorio, Web y aplicaciones móviles de Microsoft Teams.
4. Autorice previamente a los equipos seleccionando el botón **Agregar un ámbito** y, en el panel que se abre, escriba `access_as_user` como **nombre del ámbito**.

> [!NOTE]
> Hay algunas restricciones importantes que debe tener en cuenta:
>
> * Solo se admiten los permisos de la API de Microsoft Graph en el nivel de usuario, por ejemplo, email, Profile, offline_access, OpenId. Si necesita acceso a otros ámbitos de Microsoft Graph (como `User.Read` o `Mail.Read` ), vea nuestra [solución alternativa](#apps-that-require-additional-microsoft-graph-scopes) al final de esta documentación.
> * Es importante que el nombre de dominio de la aplicación sea el mismo que el nombre de dominio que ha registrado para la aplicación de Azure AD.
> * Actualmente no se admiten varios dominios por aplicación.
> * No se admiten aplicaciones que usan el `azurewebsites.net` dominio porque es demasiado común y pueden ser un riesgo para la seguridad. Sin embargo, estamos buscando activamente quitar esta restricción.

#### <a name="registering-your-app-through-the-azure-active-directory-portal-in-depth"></a>Registrar la aplicación a través de Azure Active Directory portal en profundidad:

1. Registre una nueva aplicación en el portal de [registro de aplicaciones de Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=2083908) .
2. Seleccione **registro nuevo** y, en la *Página registrar una aplicación*, establezca los siguientes valores:
    * Establezca el **nombre** en el nombre de la aplicación.
    * Elija los **tipos de cuenta admitidos** (funcionará cualquier tipo de cuenta) ¹
    * Deje **URI de redireccionamiento** vacía.
    * Elija **Registrar**.
3. En la página información general, copie y guarde el identificador de la **aplicación (cliente)**. Lo necesitará más adelante al actualizar el manifiesto de aplicación de Teams.
4. En **Administrar**, seleccione **Exponer una API** 
5. Seleccione el vínculo **establecer** para generar el URI del identificador de aplicación con el formato de `api://{AppID}` . Inserte el nombre de dominio completo (con una barra diagonal "/" anexada al final) entre las dos barras diagonales y el GUID. El identificador completo debe tener el siguiente formato: `api://fully-qualified-domain-name.com/{AppID}` ²
    * por ejemplo: `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` .
    
    El nombre de dominio completo es el nombre de dominio inteligible desde el que se sirve la aplicación. Si usa un servicio de túnel como ngrok, tendrá que actualizar este valor siempre que cambie el subdominio ngrok. 
6. Seleccione el botón **Agregar un ámbito** En el panel que se abre, escriba `access_as_user` como el **Nombre de ámbito**.
7. **¿Establecer quién puede conceder autorización?** para`Admins and users`
8. Rellene los campos para configurar las solicitudes de consentimiento del usuario y el administrador con valores que sean apropiados para el `access_as_user` ámbito:
    * **Título de consentimiento de administración:** Los equipos pueden tener acceso al perfil del usuario.
    * **Descripción del consentimiento del administrador**: permite a los equipos llamar a las API Web de la aplicación como el usuario actual.
    * **Título de consentimiento del usuario**: Microsoft Teams puede tener acceso al perfil de usuario y realizar solicitudes en nombre del usuario.
    * **Descripción del consentimiento del usuario:** Habilite Microsoft Teams para que llame a las API de esta aplicación con los mismos derechos que el usuario.
9. Asegurarse de que el **Estado** está establecido en **habilitado**
10. Seleccione el botón **Agregar ámbito** para guardar 
    * La parte de dominio del **nombre de ámbito** que se muestra justo debajo del campo de texto debe coincidir automáticamente con el URI del **identificador de aplicación** establecido en el paso anterior, `/access_as_user` que se ha anexado al final:
        * `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`
11. En la sección **aplicaciones cliente autorizadas** , identifique las aplicaciones que desea autorizar para la aplicación Web de la aplicación. Seleccione *Agregar una aplicación cliente*. Escriba cada uno de los siguientes identificadores de cliente y seleccione el ámbito autorizado que creó en el paso anterior:
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264` (Aplicación para equipos móviles o de escritorio)
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346` (Aplicación Web de Teams)
12. Navegue a **permisos** de la API. Seleccione *Agregar* permisos  >  *Microsoft Graph*  >  *delegados* de permisos de Microsoft Graph y, a continuación, agregue los siguientes permisos a la API de Microsoft Graph:
    * User. Read (habilitado de forma predeterminada)
    * email
    * offline_access
    * OpenId
    * perfil

13. Navegar a **autenticación**

    Si una aplicación no ha recibido el consentimiento del administrador de ti, los usuarios tendrán que proporcionar consentimiento la primera vez que usen una aplicación.

    Establezca un URI de redireccionamiento:
    * Seleccione **Agregar una plataforma**.
    * Seleccione **Web**.
    * Escriba el **URI de redireccionamiento** de la aplicación. Ésta será la página a la que se redirigirá al usuario un flujo de concesión implícito correcto. Se trata del mismo nombre de dominio completo que especificó en el paso 5 seguido de la ruta de la API donde debe enviarse una respuesta de autenticación. Si sigue alguno de los ejemplos de Teams, será: `https://subdomain.example.com/auth-end`

    A continuación, habilite la concesión implícita comprobando las siguientes casillas:  
    Token de identificador de ✔  
    Token de acceso ✔  
    
¡Enhorabuena! Ha completado los requisitos previos de registro de aplicaciones para continuar con la aplicación SSO de pestañas.     

> [!NOTE]
>
> * ¹ si su aplicación de Azure AD está registrada en el _mismo_ inquilino donde está realizando una solicitud de autenticación en Microsoft Teams, el usuario no se le pedirá consentimiento y se le concederá un token de acceso inmediatamente. Los usuarios solo deben dar su consentimiento a estos permisos si la aplicación de Azure AD está registrada en un inquilino diferente.
> * ² si recibe un mensaje de error que indica que el dominio ya tiene propietario y es el propietario, siga el procedimiento descrito en [QuickStart: agregar un nombre de dominio personalizado a Azure Active Directory](/azure/active-directory/fundamentals/add-custom-domain) para registrar el dominio y, a continuación, repita el paso 5 más arriba. (Este error también puede producirse si no ha iniciado sesión con las credenciales de administrador en el espacio empresarial de Office 365).
> * Si no recibe el UPN (nombre principal de usuario) en el token de acceso devuelto, puede agregarlo como una [notificación opcional](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) en Azure ad.

### <a name="2-update-your-microsoft-teams-application-manifest"></a>2. actualizar el manifiesto de aplicación de Microsoft Teams

Agregue nuevas propiedades al manifiesto de Microsoft Teams:

* **WebApplicationInfo** : el elemento primario de los siguientes elementos:

> [!div class="checklist"]
> * **ID** -el identificador de cliente de la aplicación. Se trata del identificador de la aplicación que ha obtenido como parte del registro de la aplicación con Azure AD.
>* **Resource** : el dominio y el subdominio de la aplicación. Se trata del mismo URI (incluido el `api://` Protocolo) que registró al crear el `scope` en el paso 6 anterior. No debe incluir la `access_as_user` ruta de acceso en el recurso. La parte de dominio de este URI debe coincidir con el dominio, incluidos los subdominios, que se usan en las direcciones URL del manifiesto de aplicación de Teams.

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

> [!NOTE]
>
>* El recurso de una aplicación de AAD normalmente será la raíz de la dirección URL del sitio y el appID (por ejemplo, `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` ). Este valor también se usa para garantizar que la solicitud procede del mismo dominio. Por lo tanto, asegúrese de que el `contentURL` de la pestaña use los mismos dominios que la propiedad de recurso.
>* Debe usar el manifiesto versión 1,5 o superior para implementar el `webApplicationInfo` campo.

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a>3. obtener un token de autenticación del código del lado cliente

Esto es lo que la API de autenticación tiene como:

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

Cuando se `getAuthToken` requiere el consentimiento del usuario adicional (para los permisos de nivel de usuario), se muestra un cuadro de diálogo al usuario para alentarlo a conceder consentimiento adicional. 

Una vez que haya recibido el token de acceso en la devolución de llamada correcta, puede descodificar el token de acceso para ver las notificaciones asociadas con ese token. (Opcionalmente, puede copiar o pegar manualmente el token de acceso en una herramienta como [JWT.IO](https://jwt.io/) para inspeccionar su contenido). Si no recibe el UPN (nombre principal de usuario) en el token de acceso devuelto, puede agregarlo como una [notificación opcional](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) en Azure ad.

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="sample-code"></a>Código de ejemplo

Visite nuestra aplicación de ejemplo: [MSTeams de SSO de ejemplo de pestañas-NodeJS](https://github.com/OfficeDev/msteams-tabs-sso-sample-nodejs)

En el archivo Léame se explica cómo configurar el entorno de desarrollo y cómo configurar la aplicación en Azure AD. También puede encontrar más información sobre cómo se estructura la muestra en la [sección estructura](https://github.com/OfficeDev/msteams-tabs-sso-sample-nodejs#app-structure) de la aplicación para que le resulte más fácil familiarizarse con el código base.

## <a name="known-limitations"></a>Limitaciones conocidas

### <a name="apps-that-require-additional-microsoft-graph-scopes"></a>Aplicaciones que requieren ámbitos adicionales de Microsoft Graph

Nuestra implementación actual de SSO solo concede el consentimiento para los permisos de nivel de usuario (correo, perfil, offline_access, OpenId) no para otras API (como User. Read o mail. Read). Si la aplicación necesita más ámbitos de Microsoft Graph, aquí le presentamos algunas soluciones alternativas:

#### <a name="tenant-admin-consent"></a>Consentimiento del administrador de inquilinos

El enfoque más sencillo es conseguir que un administrador de espacios empresariales dé su consentimiento previo en nombre de la organización. Esto significa que los usuarios no tendrán que dar su consentimiento a estos ámbitos y, a continuación, podrá intercambiar el lado del servidor de tokens mediante el [flujo en nombre de](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)Azure ad. Esta solución es aceptable para las aplicaciones de línea de negocio internas, pero es posible que no sea suficiente para desarrolladores de terceros que no puedan confiar en la aprobación del administrador de inquilinos.

Una forma sencilla de conformar en nombre de una organización (como administrador de inquilinos) es visitar:

* `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`

#### <a name="asking-for-additional-consent-using-the-auth-api"></a>Pedir consentimiento adicional usando la API de autenticación

Otro enfoque para obtener ámbitos de Microsoft Graph adicionales es presentar un cuadro de diálogo de consentimiento mediante nuestro [enfoque de autenticación de Azure ad existente basado en Web](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) que implica mostrar un cuadro de diálogo de consentimiento de Azure ad. Hay adiciones notables:

1. El token recuperado con `getAuthToken()` debe intercambiarse del servidor mediante el [flujo en nombre de](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) Azure ad para obtener acceso a las API adicionales de Microsoft Graph.
    * Asegúrese de usar el punto de conexión V2 de Microsoft Graph para este intercambio
2. Si se produce un error en el intercambio, Azure AD devolverá una excepción de concesión no válida. Suele haber un mensaje de error de dos: `invalid_grant` o `interaction_required`
3. Cuando se produzca un error en el intercambio, deberá pedir consentimiento adicional. Le recomendamos que muestre una interfaz de usuario que pida al usuario que conceda el consentimiento adicional. Esta interfaz de usuario debe incluir un botón que desencadene un cuadro de diálogo de consentimiento de Azure AD mediante nuestra [API de autenticación de Azure ad](~/concepts/authentication/auth-silent-aad.md).
4. Al solicitar el consentimiento adicional de Azure AD, debe incluir `prompt=consent` en el parámetro de [cadena de consulta](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) a Azure ad, de lo contrario, Azure ad no pedirá los ámbitos adicionales.
    * En lugar de: `?scope={scopes}`
    * Use lo siguiente: `?prompt=consent&scope={scopes}`
    * Asegúrese de que `{scopes}` incluye todos los ámbitos que solicita al usuario (por ejemplo: mail. Read o User. Read).
5. Una vez que el usuario haya concedido permiso adicional, vuelva a intentar el en nombre de flujo para obtener acceso a estas API adicionales.

### <a name="non-azure-ad-authentication"></a>Autenticación que no es de Azure AD

La solución de autenticación descrita anteriormente solo funciona con aplicaciones y servicios que admitan Azure AD como proveedor de identidades. Las aplicaciones que quieran autenticarse con servicios que no están basados en Azure AD deben seguir usando el [flujo de autenticación Web](~/concepts/authentication.md)basada en ventanas emergentes.

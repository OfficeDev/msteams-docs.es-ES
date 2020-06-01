---
title: Inicio de sesión único
description: Describe el inicio de sesión único (SSO)
keywords: autenticación de SSO de Microsoft Teams AAD
ms.openlocfilehash: 8f9d94346aad7c096e4310f80b6cda73856afc8c
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/31/2020
ms.locfileid: "44455516"
---
# <a name="single-sign-on"></a>Inicio de sesión único

> [!NOTE]
> La API de "Inicio de sesión único" solo se admite actualmente en _Developer Preview_ .

Los usuarios inician sesión en Microsoft Teams con su cuenta profesional o educativa (Office 365) y puede aprovecharlas usando el inicio de sesión único (SSO) para autorizar al usuario a su pestaña de Microsoft Teams. Esto significa que si un usuario consiente usar la aplicación en el escritorio, no tendrá que volver a dar su consentimiento en dispositivos móviles y se iniciará sesión automáticamente. 

## <a name="how-sso-works-at-runtime"></a>Cómo funciona el SSO en tiempo de ejecución

El siguiente diagrama muestra cómo funciona el proceso de SSO:

<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. En la pestaña, JavaScript llama a getAuthToken (). Esto indica a la aplicación de Microsoft teams que debe obtener un token de autenticación para la aplicación de pestañas.
2. Si esta es la primera vez que el usuario actual ha usado la aplicación de pestañas, se le pedirá que lo solicite (si se requiere consentimiento) o que se le pida que controle la autenticación de paso a paso (por ejemplo, la autenticación en dos fases).
3. La aplicación Microsoft Teams solicita el token de la aplicación Tab desde el punto de conexión de Azure AD v 1.0 para el usuario actual.
4. Azure AD envía el token de aplicación de la pestaña a la aplicación Teams.
5. La aplicación Microsoft Teams envía el token de aplicación de la pestaña a la ficha como parte del objeto de resultado devuelto por la llamada de getAuthToken ().
6. JavaScript en la aplicación de pestañas puede analizar el token y extraer la información que necesita, como la dirección de correo electrónico del usuario.
    * Nota: este token solo es válido para Consent? a un conjunto limitado de API de nivel de usuario (por ejemplo: email, Profile, etc) y no para otros ámbitos de gráficos (como mail. Read). Consulte nuestra sección al final de este documento para obtener soluciones alternativas si necesita ámbitos de gráficos adicionales.

## <a name="develop-an-sso-microsoft-teams-tab"></a>Desarrollar una pestaña de Microsoft Teams de SSO

En esta sección se describen las tareas necesarias para crear una pestaña de Microsoft teams que usen SSO. Estas tareas se describen aquí de forma independiente del lenguaje y el marco.

### <a name="1-create-your-aad-application-in-azure"></a>1. crear una aplicación de AAD en Azure

Registre su aplicación en el portal de registro para el punto de conexión de Azure AD v 1.0. Este es un proceso de 5 a 10 minutos que incluye las siguientes tareas:

* Obtener el identificador de la aplicación de AAD
* Especifique los permisos que necesita la aplicación para el punto de conexión de AAD (y opcionalmente para Microsoft Graph). 
* Conceder confianza a la aplicación de escritorio, Web y aplicación móvil de Microsoft Teams a la aplicación
* Autorizar previamente la aplicación Microsoft Teams a la aplicación con el nombre de ámbito predeterminado de `access_as_user` .

> [!NOTE]
> Hay algunas restricciones importantes que debe tener en cuenta:
>
> * Solo se admiten los permisos de la API Graph de nivel de usuario, por ejemplo, email, Profile, offline_access, OpenID. Si necesita acceso a otros ámbitos de Graph, lea nuestra solución recomendada al final de esta documentación.
> * Es importante que el nombre de dominio de la aplicación se registre con la aplicación de Azure AD. Debe ser el mismo nombre de dominio en el que se ejecuta la aplicación cuando se solicita un token de autenticación en Microsoft Teams y también cuando se especifica la propiedad Resource en el manifiesto de Microsoft Teams (más detalles en la sección siguiente).
> * Actualmente no se admiten varios dominios por aplicación
> * Tampoco se admiten aplicaciones que usan el `azurewebsites.net` dominio, ya que este dominio es demasiado común y puede ser un riesgo para la seguridad.

#### <a name="steps"></a>Pasos

1. Registrar una nueva aplicación en el portal de [registro de aplicaciones de Azure Active Directory:](https://go.microsoft.com/fwlink/?linkid=2083908)
2. Seleccione "nuevo registro". En la página registrar una aplicación, establezca los valores de la siguiente manera:
    * Establecer el **nombre** del nombre de la aplicación
    * Establecer **tipos de cuenta admitidos** **en cuentas de cualquier directorio de la organización y cuentas personales de Microsoft**
    * Dejar el **URI de redireccionamiento** vacío
    * Elegir **registro**
3. En la página información general, copie y guarde el identificador de la **aplicación (cliente)**. Lo necesitará más adelante al actualizar el manifiesto de aplicación de Teams.
4. Seleccione **Exponer una API** en **Administrar**. Seleccione el vínculo **establecer** para generar el URI del identificador de aplicación con el formato de `api://{AppID}` . Inserte el nombre de dominio completo (con una barra diagonal "/" anexada al final) entre las dos barras diagonales y el GUID. El identificador completo debe tener el siguiente formato:`api://fully-qualified-domain-name.com/{AppID}`
    * por ejemplo: `api://subdomain.example.com:6789/c6c1f32b-5e55-4997-881a-753cc1d563b7` .

> [!NOTE]
> Si recibe un error que indica que el dominio ya tiene propietario, pero es usted su propietario, siga el procedimiento de [Inicio rápido: agregar un nombre de dominio personalizado a Azure Active Directory](/azure/active-directory/fundamentals/add-custom-domain) para registrarlo y repita este paso. (Este error también puede producirse si no ha iniciado sesión con las credenciales de un administrador en el inquilino de Office 365).

5. Seleccione el botón **Agregar un ámbito** En el panel que se abre, escriba `access_as_user` como el **Nombre de ámbito**.
6. ¿Quién puede dar su consentimiento? para administradores y usuarios
7. Rellene los campos para configurar las solicitudes de consentimiento del usuario y el administrador con valores que sean apropiados para el `access_as_user` ámbito. Sugerencias:
    * **Título de consentimiento de administración:** Teams puede tener acceso al perfil del usuario
    * **Descripción del consentimiento del administrador**: permite a los equipos llamar a las API Web de la aplicación como el usuario actual.
    * **Título de consentimiento del usuario**: Microsoft Teams puede obtener acceso a su perfil de usuario y realizar solicitudes en su nombre
    * **Descripción del consentimiento del usuario:** Permitir que Microsoft Teams llame a las API de la aplicación con los mismos derechos que usted
8. Asegurarse de que el **Estado** está establecido en **habilitado**
9. Seleccionar **Agregar ámbito**
    * Nota: la parte de dominio del **nombre de ámbito** que se muestra justo debajo del campo de texto debe coincidir automáticamente con el URI de **identificador de aplicación** establecido en el paso anterior, con `/access_as_user` anexado al final; por ejemplo: 
        * `api://subdomain.example.com:6789/c6c1f32b-5e55-4997-881a-753cc1d563b7/access_as_user`
10. En la sección **aplicaciones cliente autorizadas** , se identifican las aplicaciones que se desea autorizar en la aplicación Web de la aplicación. Debe especificarse cada uno de los siguientes identificadores:
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264`(Aplicación para equipos móviles o de escritorio)
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346`(Aplicación Web de Teams)
11. Navegue a **permisos**de la API y asegúrese de agregar los siguientes permisos:
    * User. Read (habilitado de forma predeterminada)
    * email
    * offline_access
    * OpenID
    * perfil

### <a name="2-update-your-microsoft-teams-application-manifest"></a>2. actualizar el manifiesto de aplicación de Microsoft Teams

Agregue nuevas propiedades al manifiesto de Microsoft Teams:

* **WebApplicationInfo**: elemento primario de los siguientes elementos.
* **ID** -el identificador de cliente de la aplicación. Se trata de un identificador de aplicación que se obtiene como parte del registro de la aplicación con el punto de conexión de Azure AD 1,0.
* **Resource** : el dominio y el subdominio de la aplicación. Se trata del mismo URI (incluido el `api://` Protocolo) que usó al registrar la aplicación en AAD. La parte de dominio de este URI debe coincidir con el dominio, incluidos los subdominios, que se usan en las direcciones URL en la sección del manifiesto de aplicación de Teams.

```json
"webApplicationInfo": {
  "id": "<application_GUID here>",
  "resource": "<web_API resource here>"
}
```

Notas:

* El recurso de una aplicación de AAD normalmente será simplemente la raíz de la dirección URL del sitio y el appID (por ejemplo, `api://subdomain.example.com/6789/c6c1f32b-5e55-4997-881a-753cc1d563b7` ). Este valor también se usa para garantizar que la solicitud procede del mismo dominio. Por ello, asegúrese de que su `contentURL` para su pestaña use los mismos dominios que la propiedad de recurso.
* Debe usar la versión del manifiesto 1,5 o superior para usar estos campos.
* Los ámbitos no se admiten en el manifiesto y, en su lugar, deben especificarse en la sección permisos de la API de Azure portal.

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a>3. obtener un token de autenticación del código del lado cliente

Esto es lo que la API de autenticación tiene como:

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); },
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

Cuando se `getAuthToken` requiere el consentimiento del usuario adicional (para los permisos de nivel de usuario), se muestra un cuadro de diálogo al usuario para alentarlo a conceder consentimiento adicional. 

<img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>

## <a name="demo-code"></a>Código de demostración

Por ahora, puede visitar nuestra [tarea](https://github.com/ydogandjiev/taskmeow) de aplicación de prueba Meow y usar el manifiesto de SSO y desproteger el `teams.auth.service.js` `sso.auth.service.js` archivo y para ver cómo se controla el flujo de trabajo de autenticación.

## <a name="known-limitations"></a>Limitaciones conocidas

### <a name="apps-that-require-additional-graph-scopes"></a>Aplicaciones que requieren ámbitos de gráficos adicionales

Nuestra implementación actual de SSO solo concede el consentimiento para los permisos de nivel de usuario (email, Profile, offline_access, OpenID), pero no para otras API (como mail. Read). Si la aplicación necesita más ámbitos de gráficos, hay algunas soluciones para habilitarlo.

#### <a name="tenant-admin-consent"></a>Consentimiento del administrador de inquilinos

El método más sencillo sería obtener un administrador de inquilinos para el consentimiento previo en nombre de la organización. Esto significa que los usuarios no tendrán que dar su consentimiento a estos ámbitos y, a continuación, puede tener libertad para intercambiar el lado servidor de tokens mediante el [flujo en nombre de](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)AAD. Esta solución es aceptable para las aplicaciones de línea de negocio internas, pero es posible que no sea suficiente para los ISV que no puedan confiar en la aprobación del administrador de inquilinos.

Una forma sencilla de conformar en nombre de una organización (como administrador de inquilinos) es visitar:

* `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`

#### <a name="asking-for-additional-consent-using-the-auth-api"></a>Pedir consentimiento adicional usando la API de autenticación

Otro enfoque para obtener ámbitos de gráficos adicionales sería presentar un cuadro de diálogo de consentimiento mediante nuestro [enfoque de autenticación de AAD basado en Web](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) existente que implica mostrar un cuadro de diálogo de consentimiento de AAD. Hay adiciones notables:

1. El token recuperado con getAuthToken tendría que intercambiar el servidor usando el [flujo en nombre de](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow) AADs para obtener acceso a las API de Graph adicionales.
    * Asegúrese de usar el punto de conexión de Graph v2 para este intercambio
2. Si se produce un error en el intercambio, AAD devolverá una excepción de concesión no válida. Suele haber un mensaje de error de dos: `ConsentRequired` o`InteractionRequired`
3. Cuando se produzca un error en el intercambio, deberá pedir consentimiento adicional. Le recomendamos que muestre una interfaz de usuario que pida al usuario que conceda el consentimiento adicional. Esta interfaz de usuario debe incluir un botón que desencadene un cuadro de diálogo de consentimiento de AAD mediante nuestra [API de autenticación de AAD](~/concepts/authentication/auth-silent-aad.md).
4. Al solicitar consentimiento adicional de AAD, debe incluir `prompt=consent` en el [parámetro de cadena de consulta](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) a AAD, de lo contrario, AAD no pedirá los ámbitos adicionales.
    * En lugar de:`?scope={scopes}`
    * Use lo siguiente:`?prompt=consent&scope={scopes}`
    * Asegúrese de que `{scopes}` incluye todos los ámbitos que solicita al usuario (por ejemplo: mail. Read o User. Read).
5. Una vez que el usuario haya concedido permiso adicional, vuelva a intentar el en nombre de flujo para obtener acceso a estas API adicionales.

### <a name="non-aad-authentication"></a>Autenticación que no es AAD

La solución de autenticación descrita anteriormente solo funciona con aplicaciones y servicios que admitan Azure AD como proveedor de identidades. Las aplicaciones que quieran autenticarse con servicios no basados en AAD deben seguir usando el [flujo de autenticación Web](~/concepts/authentication.md)basada en Popup.

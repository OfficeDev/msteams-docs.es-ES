---
title: Registrar la aplicación de pestañas con Azure AD
description: Configure el inicio de sesión único (SSO) con Azure AD mediante la configuración del URI del identificador de aplicación, el ámbito del token de acceso y la autorización previa de clientes de confianza.
ms.topic: how-to
ms.localizationpriority: high
keywords: pestañas de autenticación de teams Microsoft Azure Active Directory (Azure AD) ámbito de inquilino de SSO de token de acceso
ms.openlocfilehash: 1387b1f426e433ea98bc950c932f271785fa5dd4
ms.sourcegitcommit: 82c585d287d61924ce3a3bba3e9caeff35c9a27a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/02/2022
ms.locfileid: "67586801"
---
# <a name="register-your-tab-app-in-azure-ad"></a>Registrar la aplicación de pestaña en Azure AD

Azure AD proporciona acceso a la aplicación de pestañas en función de la identidad de Teams del usuario de la aplicación. Deberá registrar la aplicación de pestañas con Azure AD para que el usuario de la aplicación que haya iniciado sesión en Teams pueda tener acceso a la aplicación de pestañas.

## <a name="enabling-sso-on-azure-ad"></a>Habilitación del inicio de sesión único SSO en Azure AD

El registro de la aplicación de pestañas en Azure AD y su habilitación para SSO requiere la realización de configuraciones de aplicaciones, como la generación del identificador de aplicación, la definición del ámbito de API y la autorización previa de Id. de cliente para aplicaciones de confianza.

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/register-azure-ad.png" alt-text="Configurar Azure AD para enviar el token de acceso a la aplicación cliente de Teams":::

Cree un nuevo registro de aplicación en Azure AD y exponga su API (web) mediante ámbitos (permisos). Configure una relación de confianza entre la API expuesta en Azure AD y la aplicación. Esto permite a Teams Client obtener un token de acceso en nombre de la aplicación y del usuario que ha iniciado sesión. Puede agregar Id. de cliente para las aplicaciones móviles, de escritorio y web de confianza que desea autorizar previamente.

Es posible que también deba configurar detalles adicionales, como autenticar a los usuarios de la aplicación en la plataforma o el dispositivo al que desea dirigirse la aplicación de pestañas.

Se admiten permisos de Graph API a nivel de usuario, es decir, correo electrónico, perfil, offline_access y OpenId. Si necesita acceso a ámbitos de Graph adicionales, como `User.Read` o `Mail.Read`, consulte [Obtener un token de acceso con permisos de Graph](tab-sso-graph-api.md).

La configuración de Azure AD habilita el inicio de sesión único para la aplicación de pestañas en Teams. Responde con un token de acceso para validar al usuario de la aplicación.

> [!NOTE]
> Microsoft Teams Toolkit registra la aplicación de Azure AD en un proyecto de SSO.

### <a name="before-you-register-with-azure-ad"></a>Antes de registrarse en Azure AD

Es útil si obtiene información previa sobre la configuración para registrar la aplicación en Azure AD. Asegúrese de que se ha preparado para configurar los siguientes detalles antes de registrar la aplicación:

- **Opciones de inquilino único o multiinquilino**: ¿se usará la aplicación solo en el inquilino de Microsoft 365 donde está registrada o la usarán muchos inquilinos de Microsoft 365? Las aplicaciones escritas para una empresa suelen ser de un solo inquilino; las aplicaciones escritas por un proveedor de software independiente y utilizadas por muchos clientes deben ser multiinquilino para que el inquilino de cada cliente pueda acceder a la aplicación.
- **URI de id. de aplicación**: es un URI único mundial que identifica la API web que expone para el acceso de la aplicación a través de ámbitos. También se conoce como un URI de identificador. El URI del identificador de aplicación incluye el identificador de la aplicación y el subdominio donde se hospeda la aplicación. El nombre de dominio de la aplicación y el nombre de dominio que registre para la aplicación de Azure AD deben ser los mismos. Actualmente, no se admiten varios dominios por aplicación.
- **Ámbito**: es el permiso que se puede conceder a un usuario de aplicación autorizado o a su aplicación para acceder a un recurso expuesto por la API.

> [!NOTE]
>
> - **Aplicaciones de LOB**: su organización puede hacer que las aplicaciones lob estén disponibles a través de Microsoft Store. Estas aplicaciones son personalizadas para su organización. Son internos o específicos dentro de su organización o negocio.
> - **A aplicaciones propiedad del Cliente**: SSO también se admite para las aplicaciones propiedad del cliente dentro de los inquilinos de Azure AD B2C.

Para crear y configurar la aplicación en Azure AD para habilitar el SSO:

- [Registre y configure la aplicación Azure AD.](#create-an-app-registration-in-azure-ad)
- [Configure el ámbito del token de acceso.](#configure-scope-for-access-token)
- [Configure la versión del token de acceso.](#configure-access-token-version)

## <a name="create-an-app-registration-in-azure-ad"></a>Creación de un registro de aplicación en Azure AD

Registre una nueva aplicación en Azure AD y configure el arrendamiento y la plataforma de la aplicación. Generará un nuevo identificador de aplicación que se actualizará más adelante en el archivo de manifiesto de la aplicación de Teams.

### <a name="to-register-a-new-app-in-azure-ad"></a>Para registrar una nueva aplicación en Azure AD

1. Abra el [Azure Portal](https://ms.portal.azure.com/) en el explorador web.
   Se abre la página Microsoft Azure AD Portal.

2. Seleccione el icono **Registros de aplicaciones**.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-portal.png" alt-text="Página del Portal de Azure AD.":::

   Aparece la página **Registros de aplicaciones**.

3. Seleccione **+ Nuevo icono de registro.**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-registrations.png" alt-text="Nuevo registro en Azure AD Portal.":::

    Aparece la página **Registrar una aplicación**.

4. Escriba el nombre de la aplicación que desea que se muestre al usuario de la aplicación. Puede cambiar este nombre en una etapa posterior, si lo desea.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/register-app.png" alt-text="Página de registro de aplicaciones en Azure AD Portal.":::

5. Seleccione el tipo de cuenta de usuario que puede acceder a su aplicación. Puede elegir entre opciones de inquilino único o múltiple, o cuenta privada de Microsoft.

    <details>
    <summary><b>Opciones para los tipos de cuenta admitidos</b></summary>

    | Opción | Seleccione esta opción para... |
    | --- | --- |
    | Cuentas solo en este directorio de la organización (solo Microsoft - Inquilino único) | Compile una aplicación para que solo la usen los usuarios (o invitados) de su inquilino. <br> A menudo denominada aplicación LOB, esta aplicación es una aplicación de un solo inquilino en la Plataforma de identidad de Microsoft. |
    | Cuentas en cualquier directorio de la organización (cualquier directorio Azure AD: multiinquilino) | Permitir que los usuarios de cualquier inquilino de Azure AD usen su aplicación. Esta opción es adecuada si, por ejemplo, está compilando una aplicación SaaS y pretende ponerla a disposición de varias organizaciones. <br> Este tipo de aplicación se conoce como aplicación multiinquilino en la Plataforma de identidad de Microsoft.|
    | Cuentas de cualquier directorio de la organización (cualquier directorio Azure AD: multiinquilino) y cuentas personales de Microsoft | Dirigirse al conjunto más amplio de clientes. <br> Al seleccionar esta opción, está registrando una aplicación multiinquilino que puede admitir usuarios de aplicaciones que también tienen cuentas personales de Microsoft. |
    | Solo cuentas personales de Microsoft | Cree una aplicación solo para los usuarios que tengan cuentas personales de Microsoft. |

    </details>

    > [!NOTE]
    > No es necesario que introduzca el **URI de redirección** para habilitar SSO para una aplicación de pestañas.

7. Seleccione **Registrar**.
    Aparece un mensaje en el explorador que indica que se ha creado la aplicación.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-created-msg.png" alt-text="Registrar la aplicación en Azure AD Portal.":::

    Se muestra la página con el identificador de la aplicación y otras configuraciones.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/tab-app-created.png" alt-text="El registro de la aplicación se ha realizado correctamente.":::

8. Anote y guarde el identificador de aplicación desde el **identificador de aplicación (cliente).** La necesitará para actualizar el manifiesto de la aplicación de Teams más adelante.

    La aplicación está registrada en Azure AD. Ahora debería tener el identificador de aplicación para la aplicación de pestañas.

## <a name="configure-scope-for-access-token"></a>Configurar el ámbito para el token de acceso

Después de crear un nuevo registro de aplicación, configure las opciones de ámbito (permiso) para enviar token de acceso a Teams Client y autorizar aplicaciones cliente de confianza para habilitar SSO.

Para configurar el ámbito y autorizar aplicaciones cliente de confianza, necesitará:

- [Para exponer una API](#to-expose-an-api): configure las opciones de ámbito (permiso) para la aplicación. Expondrá una API web y configurará el URI del identificador de la aplicación.
- [Para configurar el ámbito de la API](#to-configure-api-scope): defina el ámbito de la API y los usuarios que pueden dar su consentimiento para un ámbito. Solo puede permitir que los administradores den su consentimiento para permisos con privilegios superiores.
- [Para configurar la aplicación cliente autorizado](#to-configure-authorized-client-application): cree Id. de cliente autorizados para las aplicaciones que desea autorizar previamente. Permite al usuario de la aplicación acceder a los ámbitos de la aplicación (permisos) que ha configurado, sin necesidad de ningún consentimiento adicional. Autorice previamente solo aquellas aplicaciones de cliente en las que confíe, ya que los usuarios de la aplicación no tendrán la oportunidad de rechazar el consentimiento.

### <a name="to-expose-an-api"></a>Para exponer una API

1. Seleccione **Administrar** > **Exponer una API** en el panel izquierdo.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/expose-api-menu.png" alt-text="Exponer una opción de menú de API.":::

    Aparece la página **Exponer una API**.

1. Seleccione **Establecer** para generar el identificador de la aplicación URI en forma de `api://{AppID}`.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/expose-an-api.png" alt-text="Establecer URI de id. de aplicación":::

    Aparece la sección para establecer el URI del ID de la aplicación.

1. Introduzca el URI del ID de la aplicación en el formato que se explica aquí.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/set-app-id-uri.png" alt-text="URI de Id. de la aplicación"::::

    - El **URI de id. de aplicación** se rellena previamente con el identificador de aplicación (GUID) con el formato `api://{AppID}`.
    - El formato del URI del identificador de aplicación debe ser: `api://fully-qualified-domain-name.com/{AppID}`.
    - Inserte el `fully-qualified-domain-name.com` entre `api://` y `{AppID}` (el cual es, GUID). Por ejemplo, api://example.com/{AppID}.

    donde,
    - `fully-qualified-domain-name.com` es el nombre de dominio legible por humanos desde el que se sirve la aplicación de pestañas. El nombre de dominio de la aplicación y el nombre de dominio que registre para la aplicación de Azure AD deben ser los mismos.

      Si está utilizando un servicio de tunelización, como ngrok, debe actualizar este valor cada vez que cambie el subdominio ngrok.
    - `AppID` es el identificador de aplicación (GUID) que se generó al registrar la aplicación. Puede verlo en la sección **Información general**.

    > [!IMPORTANT]
    >
    > - **URI de id. de aplicación para la aplicación con varias funcionalidades**: si va a compilar una aplicación con un bot, una extensión de mensajería y una pestaña, escriba el URI del identificador de aplicación como `api://fully-qualified-domain-name.com/BotId-{YourClientId}`, donde BotID es el identificador de la aplicación del bot.
    >
    > - **Formato para el nombre de dominio**: use letras minúsculas para el nombre de dominio. No use mayúsculas.
    >
    >   Por ejemplo, para crear un servicio de aplicaciones o una aplicación web con el nombre del recurso, "demoapplication":
    >
    >   | Si el nombre del recurso base usado es | La dirección URL será... | El formato es compatible con... |
    >   | --- | --- | --- |
    >   | *demoapplication* | **<https://demoapplication.example.net>** | Todas las plataformas|
    >   | *DemoApplication* | **<https://DemoApplication.example.net>** | Solo para escritorio, web e iOS. No es compatible con Android. |
    >
    >    Use la opción en minúsculas *demoapplication* como nombre de recurso base.

1. Haga clic en **Guardar**.

    Aparece un mensaje en el explorador que indica que se ha actualizado el URI del identificador de aplicación.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-id-uri-msg.png" alt-text=" Mensaje de URI de id. de la aplicación":::

    El URI del identificador de aplicación se muestra en la página.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-id-uri-added.png" alt-text=" URI de id. de aplicación actualizado":::

1. Anote y guarde el URI del identificador de aplicación. La necesitará para actualizar el manifiesto de la aplicación de Teams más adelante.

### <a name="to-configure-api-scope"></a>Para configurar el ámbito de la API

1. Seleccione **+ Agregar un ámbito** en la sección **Ámbitos definidos por esta API**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/select-scope.png" alt-text="Seleccionar un ámbito":::

    Aparece la página **Agregar un ámbito**.

1. Introduzca los detalles para configurar el ámbito.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-scope.png" alt-text="Agregar detalles del ámbito":::

    1. Introduzca el nombre del ámbito. Este campo es obligatorio.
    2. Seleccione el usuario que puede dar su consentimiento para este ámbito. La opción predeterminada es **Solo administradores**.
    3. Introduzca el **nombre para mostrar del consentimiento del administrador**. Este campo es obligatorio.
    4. Introduzca la descripción para el consentimiento del administrador. Este campo es obligatorio.
    5. Introduzca el **nombre para mostrar del consentimiento del usuario**.
    6. Introduzca la descripción del consentimiento del usuario.
    7. Seleccione la opción **Habilitado** para el estado.
    8. Seleccione **Agregar ámbito**.

    Aparece un mensaje en el explorador que indica que se ha agregado el ámbito.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/scope-added-msg.png" alt-text="Se ha agregado un mensaje de ámbito":::

    El nuevo ámbito definido se muestra en la página.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/scope-added.png" alt-text="Ámbito agregado y mostrado":::

### <a name="to-configure-authorized-client-application"></a>Para configurar la aplicación cliente autorizada

1. Desplácese por la página **Exponer una API** hasta la sección **Aplicación cliente autorizada**, y seleccione **+ Agregar una aplicación cliente**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/auth-client-apps.png" alt-text="A aplicación cliente autorizada":::

    Aparece la página **Agregar una aplicación cliente**.

1. Introduzca el Id. de cliente apropiado para el cliente de Teams para las aplicaciones que desea autorizar para la aplicación web de su app.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-client-app.png" alt-text="Agregar una aplicación cliente":::

    > [!NOTE]
    >
    > - Los id de cliente para la aplicación móvil, de escritorio y web de Teams son los identificadores reales que debe agregar.
    > - Para una aplicación de pestañas de Teams, necesitará Web o SPA, ya que no puede tener una aplicación cliente móvil o de escritorio en Teams.

    1. Elija uno de los siguientes identificadores de cliente:

       | Usar Id. de cliente | Para autorizar... |
       | --- | --- |
       | 1fec8e78-bli4-4aaf-ab1b-5451cc387264 | Aplicación móvil o de escritorio de Teams |
       | 5e3ce6c0-2b1f-4285-8d4b-75ee78787346 | Aplicación web de Teams |

    1. Seleccione el URI de identificador de aplicación que creó para la aplicación en **Ámbitos autorizados** para agregar el ámbito a la API web que ha expuesto.

    1. Seleccione **Agregar aplicación**.

    Aparece un mensaje en el explorador que indica que se ha agregado la aplicación cliente autorizada.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/update-app-auth-msg.png" alt-text="Se ha agregado un mensaje a la aplicación cliente":::

    El Id. de cliente se muestra en la página.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/client-app-added.png" alt-text="Aplicación cliente agregada y mostrada":::

> [!NOTE]
> Puede autorizar más de una aplicación cliente. Repita los pasos de este procedimiento para configurar otra aplicación cliente autorizada.

## <a name="configure-access-token-version"></a>Configuración de la versión del token de acceso

Debe definir la versión del token de acceso que sea aceptable para la aplicación. Esta configuración se realiza en el manifiesto de la aplicación de Azure AD.

### <a name="to-define-the-access-token-version"></a>Para definir la versión del token de acceso

1. Seleccione **Administrar** > **manifiesto** en el panel izquierdo.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-portal-manifest.png" alt-text="Manifiesto del portal de Azure AD":::

    Aparece el manifiesto de la aplicación de Azure AD.

1. Introduzca **2** como valor de la `accessTokenAcceptedVersion` propiedad.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-manifest-value.png" alt-text="Valor para la versión del token de acceso aceptado":::

1. Seleccione **Guardar**.

    Aparece un mensaje en el explorador que indica que el manifiesto se actualizó correctamente.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/update-aad-manifest-msg.png" alt-text="Mensaje actualizado del manifiesto":::

¡Enhorabuena! Ha completado la configuración de la aplicación en Azure AD necesaria para habilitar el inicio de sesión único SSO para la aplicación de pestañas.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Configurar el código para habilitar el SSO](tab-sso-code.md)

## <a name="see-also"></a>Recursos adicionales

- [Inquilinato en Azure Active Directory](/azure/active-directory/develop/single-and-multi-tenant-apps)
- [Extender la aplicación de pestañas con permisos y ámbito de Microsoft Graph](tab-sso-graph-api.md)
- [Inicio rápido: Registrar una aplicación con la Plataforma de identidad de Microsoft](/azure/active-directory/develop/quickstart-register-app)
- [Guía de inicio rápido: Configuración de una aplicación para exponer una API web](/azure/active-directory/develop/quickstart-configure-app-expose-web-apis)
- [Flujo de código de autorización de OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow)

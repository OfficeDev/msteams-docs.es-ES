---
title: Registro de la aplicación de pestaña con Azure AD
description: Describe el registro de la aplicación de pestaña con Azure AD
ms.topic: how-to
ms.localizationpriority: medium
keywords: Pestañas de autenticación de teams Microsoft Azure Active Directory (Azure AD) ámbito del inquilino de sso del token de acceso
ms.openlocfilehash: 01cb6cd54cf150af05b54617aec3159e9483d260
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558600"
---
# <a name="register-your-tab-app-in-azure-ad"></a>Registrar la aplicación de pestaña en Azure AD

Azure AD proporciona acceso a la aplicación de pestaña en función de la identidad de Teams del usuario de la aplicación. Tendrá que registrar la aplicación de pestaña en Azure AD para que el usuario de la aplicación que ha iniciado sesión en Teams pueda tener acceso a la aplicación de pestaña.

## <a name="enabling-sso-on-azure-ad"></a>Habilitación del inicio de sesión único en Azure AD

Para registrar la aplicación de pestaña en Azure AD y habilitarla para el inicio de sesión único, es necesario realizar configuraciones de aplicación, como generar el identificador de aplicación, definir el ámbito de la API y autorizar previamente los identificadores de cliente para las aplicaciones de confianza.

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/register-azure-ad.png" alt-text="Configuración de Azure AD para enviar un token de acceso a la aplicación cliente de Teams":::

Cree un registro de aplicación en Azure AD y exponga su API (web) mediante ámbitos (permisos). Configure una relación de confianza entre la API expuesta en Azure AD y la aplicación. Esto permite al cliente de Teams obtener un token de acceso en nombre de la aplicación y del usuario que ha iniciado sesión. Puede agregar identificadores de cliente para las aplicaciones móviles, de escritorio y web de confianza que desea autorizar previamente.

También es posible que deba configurar detalles adicionales, como autenticar a los usuarios de la aplicación en la plataforma o el dispositivo en el que quiera dirigirse a la aplicación de pestaña.

Se admiten los permisos de Graph API de nivel de usuario, es decir, correo electrónico, perfil, offline_access y OpenId. Si necesita acceso a ámbitos de Graph adicionales, como `User.Read` o `Mail.Read`, consulte [Obtención de un token de acceso con permisos de Graph](tab-sso-graph-api.md).

La configuración de Azure AD habilita el inicio de sesión único para la aplicación de pestaña en Teams. Responde con un token de acceso para validar al usuario de la aplicación.

> [!NOTE]
> Microsoft Teams Toolkit registra la aplicación de Azure AD en un proyecto de SSO.

### <a name="before-you-register-with-azure-ad"></a>Antes de registrarse en Azure AD

Es útil si aprende sobre la configuración para registrar la aplicación en Azure AD de antemano. Asegúrese de que está preparado para configurar los siguientes detalles antes de registrar la aplicación:

- **Opciones de un solo inquilino o multiinquilino**: ¿se usará la aplicación solo en el inquilino de Microsoft 365 donde está registrada, o la usarán muchos inquilinos de Microsoft 365? Las aplicaciones escritas para una empresa suelen ser de un solo inquilino; las aplicaciones escritas por un proveedor de software independiente y usadas por muchos clientes deben ser multiinquilino para que el inquilino de cada cliente pueda acceder a la aplicación.
- **URI de identificador** de aplicación: es un URI único global que identifica la API web que expone para el acceso de la aplicación a través de ámbitos. También se conoce como URI de identificador. El URI del identificador de aplicación incluye el identificador de la aplicación y el subdominio donde se hospeda la aplicación. El nombre de dominio de la aplicación y el nombre de dominio que registre para la aplicación de Azure AD deben ser los mismos. Actualmente, no se admiten varios dominios por aplicación.
- **Ámbito**: es el permiso que se puede conceder a un usuario de aplicación autorizado o a la aplicación para acceder a un recurso expuesto por la API.

> [!NOTE]
>
> - **Aplicaciones LOB**: su organización puede hacer que las aplicaciones lob estén disponibles a través de Microsoft Store. Estas aplicaciones son personalizadas para su organización. Son internas o específicas dentro de su organización o negocio.
> - **Aplicaciones propiedad del cliente**: el inicio de sesión único también se admite para las aplicaciones propiedad del cliente dentro de los inquilinos de Azure AD B2C.

Para crear y configurar la aplicación en Azure AD para habilitar el inicio de sesión único:

- [Registre y configure la aplicación de Azure AD.](#create-an-app-registration-in-azure-ad)
- [Configure el ámbito del token de acceso.](#configure-scope-for-access-token)
- [Configure la versión del token de acceso.](#configure-access-token-version)

## <a name="create-an-app-registration-in-azure-ad"></a>Creación de un registro de aplicación en Azure AD

Registre una nueva aplicación en Azure AD y configure el inquilino y la plataforma de la aplicación. Generará un nuevo identificador de aplicación que se actualizará más adelante en el archivo de manifiesto de aplicación de Teams.

### <a name="to-register-a-new-app-in-azure-ad"></a>Para registrar una nueva aplicación en Azure AD

1. Abra el [Azure Portal](https://ms.portal.azure.com/) en el explorador web.
   Se abre la página portal de Microsoft Azure AD.

2. Seleccione el icono **de Registros de aplicaciones**.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-portal.png" alt-text="Página del Portal de Azure AD.":::

   Aparece **la página Registros de aplicaciones**.

3. Seleccione **+ Nuevo icono de registro** .

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-registrations.png" alt-text="Nueva página de registro en el Portal de Azure AD.":::

    Aparece la página **Registrar una aplicación**.

4. Escriba el nombre de la aplicación que desea que se muestre al usuario de la aplicación. Puede cambiar este nombre en una fase posterior, si lo desea.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/register-app.png" alt-text="Página de registro de aplicaciones en el Portal de Azure AD.":::

5. Seleccione el tipo de cuenta de usuario que puede acceder a la aplicación. Puede elegir entre opciones de un solo inquilino o multiinquilino, o una cuenta privada de Microsoft.

    <details>
    <summary><b>Opciones para tipos de cuenta admitidos</b></summary>

    | Opción | Seleccione esta opción para... |
    | --- | --- |
    | Solo cuentas en este directorio organizativo (solo Microsoft: inquilino único) | Cree una aplicación para que la usen solo los usuarios (o invitados) del inquilino. <br> A menudo denominada aplicación LOB, esta aplicación es una aplicación de inquilino único en el Plataforma de identidad de Microsoft. |
    | Cuentas en cualquier directorio organizativo (cualquier directorio de Azure AD: multiinquilino) | Permitir que los usuarios de cualquier inquilino de Azure AD usen la aplicación. Esta opción es adecuada si, por ejemplo, está creando una aplicación SaaS y pretende que esté disponible para varias organizaciones. <br> Este tipo de aplicación se conoce como aplicación multiinquilino en el Plataforma de identidad de Microsoft.|
    | Cuentas en cualquier directorio organizativo (cualquier directorio de Azure AD: multiinquilino) y cuentas personales de Microsoft | Dirigirse al conjunto más amplio de clientes. <br> Al seleccionar esta opción, va a registrar una aplicación multiinquilino que puede admitir a los usuarios de aplicaciones que también tienen cuentas personales de Microsoft. |
    | Solo cuentas personales de Microsoft | Cree una aplicación solo para los usuarios que tengan cuentas personales de Microsoft. |

    </details>

    > [!NOTE]
    > No es necesario escribir el URI de **redirección** para habilitar el inicio de sesión único para una aplicación de pestaña.

7. Seleccione **Registrar**.
    Aparece un mensaje en el explorador que indica que se creó la aplicación.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-created-msg.png" alt-text="Registre la aplicación en el Portal de Azure AD.":::

    Se muestra la página con el identificador de aplicación y otras configuraciones.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/tab-app-created.png" alt-text="El registro de aplicaciones se realiza correctamente.":::

8. Tenga en cuenta y guarde el identificador de aplicación del **identificador de aplicación (cliente).** Lo necesitará para actualizar el manifiesto de aplicación de Teams más adelante.

    La aplicación está registrada en Azure AD. Ahora debe tener el identificador de la aplicación para la aplicación de pestaña.

## <a name="configure-scope-for-access-token"></a>Configuración del ámbito para el token de acceso

Después de crear un nuevo registro de aplicaciones, configure las opciones de ámbito (permiso) para enviar el token de acceso al cliente de Teams y autorizar aplicaciones cliente de confianza para habilitar el inicio de sesión único.

Para configurar el ámbito y autorizar aplicaciones cliente de confianza, necesitará lo siguiente:

- [Para exponer una API](#to-expose-an-api): configure las opciones de ámbito (permiso) para la aplicación. Expondrá una API web y configurará el URI del identificador de aplicación.
- [Para configurar el ámbito de la API](#to-configure-api-scope): defina el ámbito de la API y los usuarios que pueden dar su consentimiento para un ámbito. Solo puede permitir que los administradores proporcionen consentimiento para permisos con privilegios superiores.
- [Para configurar la aplicación cliente autorizada](#to-configure-authorized-client-application): cree identificadores de cliente autorizados para las aplicaciones que quiera autorizar previamente. Permite al usuario de la aplicación acceder a los ámbitos de aplicación (permisos) que ha configurado, sin necesidad de más consentimiento. Autorice previamente solo las aplicaciones cliente en las que confíe, ya que los usuarios de la aplicación no tendrán la oportunidad de rechazar el consentimiento.

### <a name="to-expose-an-api"></a>Para exponer una API

1. Seleccione **Administrar** > **Exponer una API** en el panel izquierdo.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/expose-api-menu.png" alt-text="Opción de menú Exponer una API.":::

    Aparece **la página Exponer una API** .

1. Seleccione **Establecer** para generar el URI del identificador de aplicación en forma de `api://{AppID}`.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/expose-an-api.png" alt-text="Establecimiento del URI del identificador de aplicación":::

    Aparece la sección para establecer el URI del identificador de aplicación.

1. Escriba el URI del identificador de aplicación en el formato que se explica aquí.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/set-app-id-uri.png" alt-text="URI del identificador de aplicación":::

    - El **URI del identificador de aplicación** se rellena previamente con el identificador de aplicación (GUID) en el formato `api://{AppID}`.
    - El formato uri del identificador de aplicación debe ser: `api://fully-qualified-domain-name.com/{AppID}`.
    - Inserte el `fully-qualified-domain-name.com` valor entre `api://` y `{AppID}` (es el GUID). Por ejemplo, api://example.com/{AppID}.

    Dónde
    - `fully-qualified-domain-name.com` es el nombre de dominio legible desde el que se sirve la aplicación de pestaña. El nombre de dominio de la aplicación y el nombre de dominio que registre para la aplicación de Azure AD deben ser los mismos.

      Si usa un servicio de tunelización, como ngrok, debe actualizar este valor cada vez que cambie el subdominio ngrok.
    - `AppID` es el identificador de aplicación (GUID) que se generó al registrar la aplicación. Puede verlo en la sección **Información general** .

    > [!IMPORTANT]
    >
    > - **URI de identificador de aplicación para la aplicación con varias funcionalidades**: si va a compilar una aplicación con un bot, una extensión de mensajería y una pestaña, escriba el URI del identificador de aplicación como `api://fully-qualified-domain-name.com/BotId-{YourClientId}`, donde BotID es el identificador de la aplicación de bot.
    >
    > - **Formato para el nombre de dominio**: use letras minúsculas para el nombre de dominio. No use mayúsculas.
    >
    >   Por ejemplo, para crear una aplicación web o un servicio de aplicaciones con el nombre del recurso, "demoapplication":
    >
    >   | Si el nombre del recurso base usado es | La dirección URL será... | El formato se admite en... |
    >   | --- | --- | --- |
    >   | *demoapplication* | **<https://demoapplication.example.net>** | Todas las plataformas.|
    >   | *DemoApplication* | **<https://DemoApplication.example.net>** | Solo escritorio, web e iOS. No se admite en Android. |
    >
    >    Use la opción *de minúsculas demoapplication* como nombre de recurso base.

1. Seleccione **Guardar**.

    Aparece un mensaje en el explorador que indica que se actualizó el URI del identificador de aplicación.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-id-uri-msg.png" alt-text="Mensaje uri del identificador de aplicación":::

    El URI del identificador de aplicación se muestra en la página.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-id-uri-added.png" alt-text="URI del identificador de aplicación actualizado":::

1. Tenga en cuenta y guarde el URI del identificador de aplicación. Lo necesitará para actualizar el manifiesto de aplicación de Teams más adelante.

### <a name="to-configure-api-scope"></a>Para configurar el ámbito de la API

1. Seleccione **+ Agregar un ámbito** en la sección **Ámbitos definidos por esta API** .

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/select-scope.png" alt-text="Seleccionar ámbito":::

    Aparece **la página Agregar un ámbito** .

1. Escriba los detalles para configurar el ámbito.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-scope.png" alt-text="Agregar detalles del ámbito":::

    1. Escriba el nombre del ámbito. Este campo es obligatorio.
    2. Seleccione el usuario que puede dar su consentimiento para este ámbito. La opción predeterminada es **Solo administradores**.
    3. Escriba el **nombre para mostrar Administración consentimiento**. Este campo es obligatorio.
    4. Escriba la descripción del consentimiento del administrador. Este campo es obligatorio.
    5. Escriba el **nombre para mostrar consentimiento del usuario**.
    6. Escriba la descripción del consentimiento del usuario.
    7. Seleccione la opción **Habilitado** para el estado.
    8. Seleccione **Agregar ámbito**.

    Aparece un mensaje en el explorador que indica que se agregó el ámbito.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/scope-added-msg.png" alt-text="Mensaje agregado de ámbito":::

    El nuevo ámbito definido se muestra en la página.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/scope-added.png" alt-text="Ámbito agregado y mostrado":::

### <a name="to-configure-authorized-client-application"></a>Para configurar la aplicación cliente autorizada

1. Vaya a la página **Exponer una API** a la sección **Aplicación cliente autorizada** y seleccione **+ Agregar una aplicación cliente**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/auth-client-apps.png" alt-text="Aplicación cliente autorizada":::

    Aparece **la página Agregar una aplicación cliente** .

1. Escriba el identificador de cliente adecuado para el cliente de Teams para las aplicaciones que desea autorizar para la aplicación web de la aplicación.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-client-app.png" alt-text="Adición de una aplicación cliente":::

    > [!NOTE]
    >
    > - Los identificadores de cliente para aplicaciones móviles, de escritorio y web de Teams son los identificadores reales que debe agregar.
    > - Para una aplicación de pestaña de Teams, necesitará web o SPA, ya que no puede tener una aplicación cliente de escritorio o móvil en Teams.

    1. Elija uno de los siguientes identificadores de cliente:

       | Uso del identificador de cliente | Para autorizar... |
       | --- | --- |
       | 1fec8e78-bli4-4aaf-ab1b-5451cc387264 | Aplicación móvil o de escritorio de Teams |
       | 5e3ce6c0-2b1f-4285-8d4b-75ee78787346 | Aplicación web de Teams |

    1. Seleccione el URI de identificador de aplicación que creó para la aplicación en **Ámbitos autorizados** para agregar el ámbito a la API web que ha expuesto.

    1. Seleccione **Agregar aplicación**.

    Aparece un mensaje en el explorador que indica que se agregó la aplicación cliente autorizada.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/update-app-auth-msg.png" alt-text="Mensaje agregado de la aplicación cliente":::

    El identificador de cliente se muestra en la página.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/client-app-added.png" alt-text="Aplicación cliente agregada y mostrada":::

> [!NOTE]
> Puede autorizar más de una aplicación cliente. Repita los pasos de este procedimiento para configurar otra aplicación cliente autorizada.

## <a name="configure-access-token-version"></a>Configuración de la versión del token de acceso

Debe definir la versión del token de acceso que es aceptable para la aplicación. Esta configuración se realiza en el manifiesto de aplicación de Azure AD.

### <a name="to-define-the-access-token-version"></a>Para definir la versión del token de acceso

1. Seleccione **Administrar** > **manifiesto** en el panel izquierdo.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-portal-manifest.png" alt-text="Manifiesto del portal de Azure AD":::

    Aparece el manifiesto de aplicación de Azure AD.

1. Escriba **2** como valor de la `accessTokenAcceptedVersion` propiedad .

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-manifest-value.png" alt-text="Valor para la versión del token de acceso aceptado":::

1. Seleccione **Guardar**.

    Aparece un mensaje en el explorador que indica que el manifiesto se actualizó correctamente.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/update-aad-manifest-msg.png" alt-text="Mensaje actualizado del manifiesto":::

¡Enhorabuena! Ha completado la configuración de la aplicación en Azure AD necesaria para habilitar el inicio de sesión único para la aplicación de pestaña.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Configuración del código para habilitar el inicio de sesión único](tab-sso-code.md)

## <a name="see-also"></a>Vea también

- [Arrendamiento en Azure Active Directory](/azure/active-directory/develop/single-and-multi-tenant-apps)
- [Extensión de la aplicación de pestaña con permisos y ámbito de Microsoft Graph](tab-sso-graph-api.md)
- [Inicio rápido: Registro de una aplicación con el Plataforma de identidad de Microsoft](/azure/active-directory/develop/quickstart-register-app)
- [Inicio rápido: Configuración de una aplicación para exponer una API web](/azure/active-directory/develop/quickstart-configure-app-expose-web-apis)
- [Flujo de código de autorización de OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow)

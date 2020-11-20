---
title: Consentimiento específico de recursos en Microsoft Teams
description: Describe el consentimiento específico del recurso en Microsoft Teams y cómo aprovecharlo.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: Gráfico RSC de OAuth SSO de OAuth para Microsoft Teams
ms.openlocfilehash: 3cafbb090c4e4bc44a814c840a7a297357341bba
ms.sourcegitcommit: 43e1be9d9e3651ce73a8d2139e44d75550a0ca60
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2020
ms.locfileid: "49366864"
---
# <a name="resource-specific-consent-rsc"></a>Autorización específica de recursos (RSC)

>[!IMPORTANT]
> Estas API son accesibles en el https://graph.microsoft.com/beta punto de conexión.  El punto de conexión de la [versión beta](/graph/versioning-and-support#beta-version) incluye API que actualmente están en versión preliminar y todavía no están disponibles en general. Las API del punto de conexión beta están sujetas a cambios y no se recomienda usarlas en las aplicaciones de producción. 

El consentimiento específico de recursos (RSC) es una integración de Microsoft Teams y de la API de Microsoft Graph que permite a la aplicación usar puntos de conexión de API para administrar equipos específicos dentro de una organización. El modelo de permisos de autorización específica de recursos (RSC) permite a los *propietarios del equipo* conceder el consentimiento para que una aplicación acceda a los datos de un equipo o los modifique. Los permisos de RSC específicos, específicos de Teams, definen lo que una aplicación puede hacer dentro de un equipo específico:

## <a name="resource-specific-permissions"></a>Permisos específicos de recursos

|Permisos de aplicación| Action |
| ----- | ----- |
|TeamSettings.Read.Group | Obtener la configuración de este equipo.|
|TeamSettings.ReadWrite.Group|Actualizar la configuración de este equipo.|
|ChannelSettings.Read.Group|Obtenga los nombres de canal, las descripciones de canales y la configuración de canal para este equipo.|
|ChannelSettings.ReadWrite.Group|Actualice los nombres de canal, las descripciones de canal y la configuración de canal para este equipo.|
|Channel.Create.Group|Crear canales en este equipo.|
|Channel.Delete.Group|Eliminar los canales de este equipo.|
|ChannelMessage.Read.Group |Obtiene los mensajes del canal de este equipo.|
|TeamsAppInstallation.Read.Group|Obtenga una lista de las aplicaciones instaladas de este equipo.|
|TeamsTab.Read.Group|Obtener una lista de las pestañas de este equipo.|
|TeamsTab.Create.Group|Crear pestañas en este equipo.|
|TeamsTab.ReadWrite.Group|Actualizar las pestañas de este equipo.|
|TeamsTab.Delete.Group|Eliminar las pestañas de este equipo.|
|TeamMember.Read.Group|Obtener los miembros de este equipo.|

>[!NOTE]
>Los permisos específicos de recursos solo están disponibles para las aplicaciones de Teams instaladas en el cliente de Teams y actualmente no forman parte del portal de Azure Active Directory.

## <a name="enable-resource-specific-consent-in-your-application"></a>Habilitar el consentimiento específico de recursos en la aplicación

Los pasos para habilitar RSC en la aplicación son los siguientes:

1. [Configure las opciones de consentimiento del propietario del grupo en el portal de Azure Active Directory](#configure-group-owner-consent-settings-in-the-azure-ad-portal).
1. [Registre su aplicación con la plataforma de identidad de Microsoft a través del portal de Azure ad](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).
1. [Revise los permisos de la aplicación en el portal de Azure ad](#review-your-application-permissions-in-the-azure-ad-portal).
1. [Obtener un token de acceso desde la plataforma de identidad de Microsoft](#obtain-an-access-token-from-the-microsoft-identity-platform).
1. [Actualizar el manifiesto de la aplicación de Teams](#update-your-teams-app-manifest).
1. [Instale la aplicación directamente en Teams](#install-your-app-directly-in-teams).
1. [Compruebe si la aplicación tiene permisos RSC agregados](#check-your-app-for-added-rsc-permissions).

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a>Configurar las opciones de consentimiento del propietario del grupo en el portal de Azure AD

Puede habilitar o deshabilitar el [consentimiento del propietario del grupo](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data) directamente en Azure Portal:

> [!div class="checklist"]
>
>- Inicie sesión en [Azure portal](https://portal.azure.com) como administrador [global o administrador](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)de la compañía.  
 > - [Seleccione](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) permisos de consentimiento del usuario de **Azure Active Directory**  =>  **Enterprise Applications**  =>  **y permisos**  =>  **User consent settings**.
> - Habilitar, deshabilitar o limitar el consentimiento del usuario con el control etiquetado como **consentimiento de propietario de grupo para las aplicaciones que obtienen acceso a los datos** (el valor predeterminado es **permitir el consentimiento del propietario del grupo para todos los propietarios del grupo**). Para que el propietario de un equipo Instale una aplicación con RSC, el consentimiento del propietario del grupo debe estar habilitado para ese usuario.

![configuración de RSC de Azure](../../assets/images/azure-rsc-configuration.png)

Para habilitar o deshabilitar el consentimiento del propietario del grupo dentro de Azure portal con PowerShell, siga los pasos descritos en [configurar el consentimiento del propietario del grupo con PowerShell](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell).

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a>Registrar la aplicación con la plataforma de identidad de Microsoft mediante el portal de Azure AD

El portal de Azure Active Directory proporciona una plataforma central para registrar y configurar las aplicaciones. La aplicación debe estar registrada en el portal de Azure AD para integrarse con la plataforma de identidad de Microsoft y llamar a las API de Microsoft Graph. *Consulte* [registrar una aplicación con la plataforma de identidad de Microsoft](/graph/auth-register-app-v2).

>[!WARNING]
>No registre varias aplicaciones de Microsoft Teams en el mismo identificador de aplicación de Azure AD. El identificador de la aplicación debe ser único para cada aplicación. Se producirá un error si intenta instalar varias aplicaciones en el mismo identificador de la aplicación.

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Revisar los permisos de la aplicación en el portal de Azure AD

Vaya a la página registros de aplicaciones **domésticas**  =>  **App registrations** y seleccione su aplicación RSC. Elija **permisos de API** en la barra de navegación izquierda y examine la lista de permisos configurados para la aplicación. Si la aplicación solo va a realizar llamadas a la API de gráficos RSC, elimine todos los permisos de esa página. Si la aplicación también va a realizar llamadas que no son RSC, conserve dichos permisos según sea necesario.

>[!IMPORTANT]
>El portal de Azure AD no se puede usar para solicitar permisos RSC. Los permisos RSC actualmente son exclusivos de las aplicaciones de Teams instaladas en el cliente de Microsoft Teams y se declaran en el archivo de manifiesto de la aplicación (JSON).

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Obtener un token de acceso desde la plataforma de identidad de Microsoft

Para realizar llamadas a la API de Graph, debe obtener un token de acceso para la aplicación desde la plataforma de identidad. Para que la aplicación pueda obtener un token de la plataforma de identidad de Microsoft, debe estar registrado en el portal de Azure AD. El token de acceso contiene información sobre la aplicación y los permisos que tiene para los recursos y las API disponibles a través de Microsoft Graph.

Necesitará tener los siguientes valores del proceso de registro de Azure AD para recuperar un token de acceso de la plataforma de identidad:

- IDENTIFICADOR de la **aplicación** asignado por el portal de registro de aplicaciones. Si la aplicación admite el inicio de sesión único (SSO), debe usar el mismo identificador de aplicación para la aplicación y el SSO.
- El  **secreto de cliente/contraseña** o un par de claves pública y privada (**certificado**). Esto no es necesario para las aplicaciones nativas.
- Un **URI de redireccionamiento** (o dirección URL de respuesta) de la aplicación para recibir respuestas de Azure ad.

 *Vea* [obtener acceso en nombre de un usuario](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token) y [obtener acceso sin un usuario](/graph/auth-v2-service)

## <a name="update-your-teams-app-manifest"></a>Actualizar el manifiesto de la aplicación de Teams

Los permisos RSC se declaran en el archivo de manifiesto de la aplicación (JSON).  Agregue una clave [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) al manifiesto de la aplicación con los siguientes valores:

> [!div class="checklist"]
>
> - **ID**  : el identificador de la aplicación de Azure ad. *consulte* [registrar la aplicación en el portal de Azure ad](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).
> - **recurso**  : cualquier cadena. Este campo no tiene ninguna operación en RSC, pero debe agregarse y tener un valor para evitar una respuesta de error; se realizará cualquier cadena.
> - **permisos de aplicación** : permisos RSC para la aplicación. *Consulte* [permisos específicos de recursos](resource-specific-consent.md#resource-specific-permissions).

>
>[!IMPORTANT]
> Los permisos no RSC se almacenan en Azure portal. No los agregue al manifiesto de la aplicación.
>

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelMessage.Read.Group",
      "TeamSettings.Edit.Group",
      "ChannelSettings.ReadWrite.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.ReadWrite.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group"
    ]
  }
```

## <a name="install-your-app-directly-in-teams"></a>Instalar la aplicación directamente en Teams

Una vez que haya creado la aplicación, puede [cargar el paquete de la aplicación](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) directamente a un equipo específico.  Para ello, la configuración de directiva **cargar aplicaciones personalizadas** debe estar habilitada como parte de las directivas de configuración de aplicaciones personalizadas. *Consulte* [Custom App Policy Settings](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings).

## <a name="check-your-app-for-added-rsc-permissions"></a>Comprobar si la aplicación tiene permisos RSC agregados

>[!IMPORTANT]
>Los permisos RSC no se atribuyen a un usuario. Las llamadas se realizan con los permisos de aplicaciones, no con los permisos delegados de usuario. Por lo tanto, es posible que se permita a la aplicación realizar acciones que el usuario no puede, como crear un canal o eliminar una pestaña. Debe revisar la intención del propietario del equipo de su caso de uso antes de hacer llamadas a la API RSC. *Vea* [información general de la API de Microsoft Teams](/graph/teams-concept-overview).

Una vez instalada la aplicación en un equipo, puede usar el [probador de Graph](https://developer.microsoft.com/graph/graph-explorer)  para ver los permisos que se han concedido a la aplicación en un equipo:

> [!div class="checklist"]
>
>- Obtenga el **GROUPID** del equipo del cliente de Teams.
> - En el cliente de Microsoft Teams, seleccione **Teams** en la barra de navegación de la parte izquierda.
> - Seleccione el equipo en el que se instalará la aplicación desde el menú desplegable.
> - Seleccione el icono **más opciones** (&#8943;).
> - Seleccione **obtener vínculo a equipo**.
> - Copie y guarde el valor **GROUPID** de la cadena.
> - Inicie sesión en el **probador de Graph**.
> - Realice una llamada **Get** al siguiente punto de conexión: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` . El campo clientAppId de la respuesta se asignará al appId especificado en el manifiesto de la aplicación Teams.
  ![Respuesta del explorador de Graph para obtener la llamada.](../../assets/images/graph-permissions.png)
 
## <a name="test-resource-specific-consent"></a>Probar el consentimiento específico del recurso
 
> [!div class="nextstepaction"]
> [**Probar permisos de consentimiento específicos de recursos en Microsoft Teams**](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a>Tema relacionado para administradores de Microsoft Teams

> [!div class="nextstepaction"]
> [**Consentimiento específico de recursos en Microsoft Teams para administradores**](/MicrosoftTeams/resource-specific-consent)
> 

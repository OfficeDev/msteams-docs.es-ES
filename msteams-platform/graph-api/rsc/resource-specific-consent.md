---
title: Consentimiento específico de recursos en Teams
description: Describe el consentimiento específico de los recursos en Teams y cómo aprovecharlo.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: OAuth SSO AAD rsc Graph de autorización de teams
ms.openlocfilehash: 97f642b203a1f7fb4cd9332b61265c0b27788e2b
ms.sourcegitcommit: 6caf503de5544fb8b9c8c6bef8eff4ff5a46068c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/17/2021
ms.locfileid: "50270801"
---
# <a name="resource-specific-consent-rsc"></a>Consentimiento específico de recursos (RSC)

El consentimiento específico de los recursos (RSC) es una integración de Microsoft Teams y la API de Microsoft Graph que permite a la aplicación usar puntos de conexión de API para administrar equipos específicos dentro de una organización. El modelo de permisos de consentimiento específico  de recursos (RSC) permite a los propietarios del equipo conceder consentimiento para que una aplicación acceda o modifique los datos de un equipo. Los permisos RSC específicos de Teams definen lo que una aplicación puede hacer dentro de un equipo específico:

## <a name="resource-specific-permissions"></a>Permisos específicos de recursos

|Permisos de aplicación| Action |
| ----- | ----- |
|TeamSettings.Read.Group | Obtenga la configuración de este equipo.|
|TeamSettings.ReadWrite.Group|Actualizar la configuración de este equipo.|
|ChannelSettings.Read.Group|Obtiene los nombres de canal, las descripciones de canales y la configuración del canal para este equipo.|
|ChannelSettings.ReadWrite.Group|Actualice los nombres de canal, las descripciones de los canales y la configuración del canal para este equipo.|
|Channel.Create.Group|Crear canales en este equipo.|
|Channel.Delete.Group|Elimine los canales de este equipo.|
|ChannelMessage.Read.Group |Obtenga los mensajes de canal de este equipo.|
|TeamsAppInstallation.Read.Group|Obtenga una lista de las aplicaciones instaladas de este equipo.|
|TeamsTab.Read.Group|Obtenga una lista de las pestañas de este equipo.|
|TeamsTab.Create.Group|Crear pestañas en este equipo.|
|TeamsTab.ReadWrite.Group|Actualizar las pestañas de este equipo.|
|TeamsTab.Delete.Group|Eliminar las pestañas de este equipo.|
|TeamMember.Read.Group|Obtenga los miembros de este equipo.|

>[!NOTE]
>Los permisos específicos de recursos solo están disponibles para las aplicaciones de Teams instaladas en el cliente de Teams y actualmente no forman parte del portal de Azure Active Directory.

## <a name="enable-resource-specific-consent-in-your-application"></a>Habilitar el consentimiento específico de recursos en la aplicación

Los pasos para habilitar RSC en la aplicación son los siguientes:

1. [Configure las opciones de consentimiento del propietario del grupo en el portal de Azure Active Directory.](#configure-group-owner-consent-settings-in-the-azure-ad-portal)
1. [Registra tu aplicación con la plataforma de identidad de Microsoft a través del portal de Azure AD.](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)
1. [Revise los permisos de la aplicación en el portal de Azure AD.](#review-your-application-permissions-in-the-azure-ad-portal)
1. [Obtenga un token de acceso de la plataforma de Identidad de Microsoft.](#obtain-an-access-token-from-the-microsoft-identity-platform)
1. [Actualice el manifiesto de la aplicación de Teams.](#update-your-teams-app-manifest)
1. [Instale la aplicación directamente en Teams.](#install-your-app-directly-in-teams)
1. [Compruebe la aplicación para obtener permisos de RSC agregados.](#check-your-app-for-added-rsc-permissions)

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a>Configurar las opciones de consentimiento del propietario del grupo en el portal de Azure AD

Puede habilitar o deshabilitar el consentimiento del [propietario del grupo](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directamente en Azure Portal:

> [!div class="checklist"]
>
>- Inicie sesión en [Azure Portal como](https://portal.azure.com) administrador global o administrador de la [compañía.](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)  
 > - [Seleccione Aplicaciones](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **de Azure Active Directory** Enterprise  =>  **Consentimiento** y  =>  **permisos** Configuración de consentimiento de  =>  **usuario.**
> - Habilitar, deshabilitar o limitar el consentimiento del usuario con el control etiquetado Consentimiento del propietario del grupo para que las aplicaciones accedan a datos **(El** valor predeterminado es Permitir el consentimiento del propietario del grupo para todos los propietarios **del grupo).** Para que el propietario de un equipo instale una aplicación mediante RSC, el consentimiento del propietario del grupo debe estar habilitado para ese usuario.

![configuración de azure rsc](../../assets/images/azure-rsc-configuration.png)

Para habilitar o deshabilitar el consentimiento del propietario del grupo con PowerShell, siga los pasos descritos en Configurar el consentimiento del propietario del grupo [con PowerShell.](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a>Registrar la aplicación con la plataforma de identidad de Microsoft a través del portal de Azure AD

El portal de Azure Active Directory proporciona una plataforma central para registrar y configurar las aplicaciones. La aplicación debe estar registrada en el portal de Azure AD para integrarse con la plataforma de identidad de Microsoft y llamar a las API de Microsoft Graph. *Vea* [Registrar una aplicación con la plataforma de identidad de Microsoft.](/graph/auth-register-app-v2)

>[!WARNING]
>No registre varias aplicaciones de Teams en el mismo identificador de aplicación de Azure AD. El identificador de aplicación debe ser único para cada aplicación. Se producirá un error al intentar instalar varias aplicaciones en el mismo identificador de aplicación.

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Revisar los permisos de la aplicación en el portal de Azure AD

Ve a la **página de** registros de la  =>  **aplicación principal** y selecciona la aplicación RSC. Elija **permisos de API en** la barra de navegación izquierda y examine la lista de permisos configurados para la aplicación. Si la aplicación solo realizará llamadas a la API de Graph de RSC, elimine todos los permisos de esa página. Si tu aplicación también realizará llamadas que no son RSC, mantén esos permisos según sea necesario.

>[!IMPORTANT]
>El portal de Azure AD no se puede usar para solicitar permisos RSC. Actualmente, los permisos RSC son exclusivos de las aplicaciones de Teams instaladas en el cliente de Teams y se declaran en el archivo de manifiesto de la aplicación (JSON).

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Obtener un token de acceso de la plataforma de identidad de Microsoft

Para realizar llamadas a la API de Graph, debe obtener un token de acceso para la aplicación desde la plataforma de identidad. Para que la aplicación pueda obtener un token de la plataforma de identidad de Microsoft, debe registrarse en el portal de Azure AD. El token de acceso contiene información sobre la aplicación y los permisos que tiene para los recursos y las API disponibles a través de Microsoft Graph.

Deberá tener los siguientes valores del proceso de registro de Azure AD para recuperar un token de acceso de la plataforma de identidad:

- El **id. de aplicación** asignado por el portal de registro de aplicaciones. Si la aplicación admite el inicio de sesión único (SSO), debe usar el mismo id. de aplicación para la aplicación y sso.
- El  **secreto de cliente/contraseña** o un par de claves pública y privada (**Certificado**). Esto no es necesario para las aplicaciones nativas.
- Un **URI de redireccionamiento** (o dirección URL de respuesta) para que la aplicación reciba respuestas de Azure AD.

 *Vea* [Obtener acceso en nombre de un usuario y](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) Obtener acceso sin un [usuario](/graph/auth-v2-service)

## <a name="update-your-teams-app-manifest"></a>Actualizar el manifiesto de la aplicación de Teams

Los permisos de RSC se declaran en el archivo de manifiesto de la aplicación (JSON).  Agrega una [clave webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) al manifiesto de la aplicación con los siguientes valores:

> [!div class="checklist"]
>
> - **id.:** su identificador de aplicación de Azure AD. *Vea* [Registrar la aplicación en el portal de Azure AD.](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)
> - **recurso:**  cualquier cadena. Este campo no tiene ninguna operación en RSC, pero debe agregarse y tener un valor para evitar una respuesta de error; cualquier cadena.
> - **permisos de aplicación:** permisos de RSC para la aplicación. *Vea* [Permisos específicos de recursos.](resource-specific-consent.md#resource-specific-permissions)

>
>[!IMPORTANT]
> Los permisos que no son RSC se almacenan en Azure Portal. No las agregues al manifiesto de la aplicación.
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

Una vez que hayas creado la aplicación, puedes [cargar el paquete](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) de la aplicación directamente a un equipo específico.  Para ello, la configuración **de directiva cargar aplicaciones** personalizadas debe estar habilitada como parte de las directivas de configuración de aplicaciones personalizadas. *Consulta Configuración* [de directiva de aplicación personalizada.](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)

## <a name="check-your-app-for-added-rsc-permissions"></a>Comprobar la aplicación para obtener permisos RSC agregados

>[!IMPORTANT]
>Los permisos de RSC no se atribuyen a un usuario. Las llamadas se realizan con permisos de aplicación, no con permisos delegados por el usuario. Por lo tanto, es posible que la aplicación pueda realizar acciones que el usuario no pueda, como crear un canal o eliminar una pestaña. Debe revisar la intención del propietario del equipo para su caso de uso antes de realizar llamadas a la API de RSC. *Vea información* [general sobre la API de Microsoft Teams.](/graph/teams-concept-overview)

Una vez instalada la aplicación en un equipo, puede usar el Explorador de [Graph](https://developer.microsoft.com/graph/graph-explorer)  para ver los permisos concedidos a la aplicación en un equipo:

> [!div class="checklist"]
>
>- Obtenga el **groupId** del equipo desde el cliente de Teams.
> - En el cliente de Teams, seleccione **Teams en** la barra de navegación del extremo izquierdo.
> - Seleccione el equipo donde está instalada la aplicación en el menú desplegable.
> - Seleccione el **icono Más opciones** (&#8943;).
> - Seleccione **Obtener vínculo al equipo.**
> - Copie y guarde el **valor groupId** de la cadena.
> - Inicie sesión en **el Explorador de Graph.**
> - Realice una **llamada GET** al siguiente punto de conexión: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` . El campo clientAppId de la respuesta se asignará al appId especificado en el manifiesto de la aplicación de Teams.
  ![Respuesta del explorador de Graph a la llamada GET.](../../assets/images/graph-permissions.png)

## <a name="code-sample"></a>Ejemplo de código
| **Nombre de ejemplo** | **Descripción** | **C#** |
|-----------------|-----------------|----------------|
| Consentimiento específico de recursos (RSC) | Use RSC para llamar a las API de Graph. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|

## <a name="test-resource-specific-consent"></a>Probar el consentimiento específico del recurso
 
> [!div class="nextstepaction"]
> [**Probar permisos de consentimiento específicos de recursos en Teams**](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a>Tema relacionado para los administradores de Teams

> [!div class="nextstepaction"]
> [**Consentimiento específico de recursos en Microsoft Teams para administradores**](/MicrosoftTeams/resource-specific-consent)
> 


---
title: Consentimiento específico de los recursos en Teams
description: Describe el consentimiento específico de los recursos en Teams y cómo aprovecharlo.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: autorizan a los equipos OAuth SSO AAD rsc Graph
ms.openlocfilehash: dabe0c33013fbb398eee7bf00ac2881cd86e6bc5
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566136"
---
# <a name="resource-specific-consent-rsc"></a>Consentimiento específico de los recursos (RSC)

El consentimiento específico de los recursos (RSC) es una integración de API Microsoft Teams y Microsoft Graph que permite a la aplicación usar puntos de conexión de API para administrar equipos específicos dentro de una organización. El modelo de permisos de consentimiento específico de recursos (RSC) permite a *los propietarios* de equipos conceder consentimiento para que una aplicación acceda y/o modifique los datos de un equipo. Los permisos RSC granulares, específicos Teams definen lo que una aplicación puede hacer dentro de un equipo específico:

## <a name="resource-specific-permissions"></a>Permisos específicos de recursos

|Permisos de aplicación| Action |
| ----- | ----- |
|TeamSettings.Read.Group | Obtenga la configuración de este equipo.|
|TeamSettings.ReadWrite.Group|Actualizar la configuración de este equipo.|
|ChannelSettings.Read.Group|Obtenga los nombres de canal, las descripciones de canal y la configuración del canal para este equipo.|
|ChannelSettings.ReadWrite.Group|Actualice los nombres de canal, las descripciones de canal y la configuración del canal de este equipo.|
|Channel.Create.Group|Crear canales en este equipo.|
|Channel.Delete.Group|Elimine los canales de este equipo.|
|ChannelMessage.Read.Group |Recibe los mensajes de canal de este equipo.|
|TeamsAppInstallation.Read.Group|Obtenga una lista de las aplicaciones instaladas de este equipo.|
|TeamsTab.Read.Group|Obtenga una lista de las pestañas de este equipo.|
|TeamsTab.Create.Group|Crear pestañas en este equipo.|
|TeamsTab.ReadWrite.Group|Actualizar las pestañas de este equipo.|
|TeamsTab.Delete.Group|Eliminar las pestañas de este equipo.|
|TeamMember.Read.Group|Consigue a los miembros de este equipo.|

>[!NOTE]
>Los permisos específicos de recursos solo están disponibles para Teams aplicaciones instaladas en el cliente Teams y actualmente no forman parte del portal de Azure Active Directory.

## <a name="enable-resource-specific-consent-in-your-application"></a>Habilite el consentimiento específico de recursos en su aplicación

Los pasos para habilitar RSC en la aplicación son los siguientes:

1. [Configure la configuración de consentimiento del propietario del grupo en el portal de Azure Active Directory.](#configure-group-owner-consent-settings-in-the-azure-ad-portal)
1. [Registre la aplicación con Plataforma de identidad de Microsoft a través de Azure AD Portal.](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)
1. [Revise los permisos de la aplicación en Azure AD Portal](#review-your-application-permissions-in-the-azure-ad-portal).
1. [Obtenga un token de acceso de la plataforma Microsoft Identity.](#obtain-an-access-token-from-the-microsoft-identity-platform)
1. [Actualiza el manifiesto de la aplicación Teams](#update-your-teams-app-manifest).
1. [Instale la aplicación directamente en Teams.](#sideload-your-app-in-teams)
1. [Compruebe si la aplicación tiene permisos RSC agregados.](#check-your-app-for-added-rsc-permissions)

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a>Configure la configuración de consentimiento del propietario del grupo en Azure AD Portal

Puede habilitar o deshabilitar el [consentimiento del propietario del grupo](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directamente en Azure Portal:

> [!div class="checklist"]
>
>- Inicie sesión en [Azure Portal](https://portal.azure.com) como [administrador global/administrador de la empresa.](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)  
 > - [Seleccione](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory**  =>  **Enterprise aplicaciones** Consentimiento y  =>  **permisos** Configuración de  =>  **consentimiento de usuario**.
> - Habilite, deshabilite o limite el consentimiento del usuario con el consentimiento del propietario del grupo etiquetado por el control **para las aplicaciones que acceden a los datos** (El valor predeterminado es Permitir el consentimiento del propietario del grupo para todos los propietarios de **grupos).** Para que el propietario de un equipo instale una aplicación mediante RSC, el consentimiento del propietario del grupo debe estar habilitado para ese usuario.

![configuración de azure rsc](../../assets/images/azure-rsc-configuration.png)

Para habilitar o deshabilitar el consentimiento del propietario del grupo mediante PowerShell, siga los pasos descritos en [Configurar el consentimiento del propietario del grupo mediante PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a>Registre la aplicación con Plataforma de identidad de Microsoft a través del portal de Azure AD

El portal de Azure Active Directory proporciona una plataforma central para que pueda registrarse y configurar las aplicaciones. La aplicación debe estar registrada en Azure AD Portal para integrarse con la Plataforma de identidad de Microsoft y llamar a las API de Microsoft Graph. Para obtener más información, consulte [Registrar una aplicación con el Plataforma de identidad de Microsoft](/graph/auth-register-app-v2).

>[!WARNING]
>No registre varias aplicaciones Teams en el mismo identificador de aplicación de Azure AD. El identificador de aplicación debe ser único para cada aplicación. Se producirá un error al intentar instalar varias aplicaciones en el mismo identificador de aplicación.

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Revise los permisos de la aplicación en el portal de Azure AD

Vaya a la página  =>  **Registros de la aplicación** doméstica y seleccione la aplicación RSC. Elija permisos de **API** en la barra de navegación izquierda y examine la lista de permisos configurados para la aplicación. Si la aplicación solo realizará llamadas a la API de RSC Graph, elimine todo el permiso de esa página. Si la aplicación también realizará llamadas que no sean RSC, conserve esos permisos según sea necesario.

>[!IMPORTANT]
>Azure AD Portal no se puede usar para solicitar permisos RSC. Los permisos RSC son actualmente exclusivos para Teams aplicaciones instaladas en el cliente Teams y se declaran en el archivo de manifiesto de aplicación (JSON).

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Obtener un token de acceso de la Plataforma de identidad de Microsoft

Para realizar llamadas a Graph API, debe obtener un token de acceso para la aplicación desde la plataforma de identidad. Para que la aplicación pueda obtener un token de la Plataforma de identidad de Microsoft, debe registrarse en Azure AD Portal. El token de acceso contiene información sobre la aplicación y los permisos que tiene para los recursos y las API disponibles a través de Microsoft Graph.

Deberá tener los siguientes valores del proceso de registro de Azure AD para recuperar un token de acceso de la plataforma de identidad:

- El **identificador de aplicación** asignado por el portal de registro de la aplicación. Si la aplicación admite el inicio de sesión único (SSO), debe usar el mismo identificador de aplicación para la aplicación y SSO.
- El  **secreto/contraseña del cliente** o un par de claves pública/privada (**Certificado**). Esto no es necesario para las aplicaciones nativas.
- Un **URI de redirección** (o dirección URL de respuesta) para que la aplicación reciba respuestas de Azure AD.

 *Consulte* [Obtener acceso en nombre de un usuario](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) y Obtener acceso sin un [usuario](/graph/auth-v2-service)

## <a name="update-your-teams-app-manifest"></a>Actualiza el manifiesto de la aplicación Teams

Los permisos RSC se declaran en el archivo de manifiesto de aplicación (JSON).  Agregue una clave [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) al manifiesto de la aplicación con los siguientes valores:

> [!div class="checklist"]
>
> - **id:**  el identificador de la aplicación de Azure AD. Para obtener más información, consulte [Registrar la aplicación en Azure AD Portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).
> - **recurso**  — cualquier cadena. Este campo no tiene ninguna operación en RSC, pero debe agregarse y tener un valor para evitar una respuesta de error; cualquier cadena hará.
> - **permisos de aplicación:** permisos RSC para la aplicación. Para obtener más información, consulte [Permisos específicos de recursos](resource-specific-consent.md#resource-specific-permissions).

>
>[!IMPORTANT]
> Los permisos que no son RSC se almacenan en Azure Portal. No los agregue al manifiesto de la aplicación.
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

## <a name="sideload-your-app-in-teams"></a>Descarga tu aplicación en Teams

Si el administrador de Teams permite cargas de aplicaciones personalizadas, puedes [descargar la aplicación](~/concepts/deploy-and-publish/apps-upload.md) directamente en un equipo específico.

## <a name="check-your-app-for-added-rsc-permissions"></a>Compruebe si la aplicación tiene permisos RSC agregados

>[!IMPORTANT]
>Los permisos RSC no se atribuyen a un usuario. Las llamadas se realizan con permisos de aplicación, no con permisos delegados por el usuario. Por lo tanto, es posible que se permita a la aplicación realizar acciones que el usuario no pueda, como crear un canal o eliminar una pestaña. Debe revisar la intención del propietario del equipo para su caso de uso antes de realizar llamadas a la API de RSC. Para obtener más información, consulte [información general sobre Microsoft Teams API.](/graph/teams-concept-overview)

Una vez instalada la aplicación en un equipo, puede usar [Graph Explorador](https://developer.microsoft.com/graph/graph-explorer) para ver los permisos que se han concedido a la aplicación en un equipo:

> [!div class="checklist"]
>
>- Obtenga el **groupId** del equipo del cliente Teams.
> - En el cliente Teams, seleccione **Teams** desde la barra de navegación izquierda.
> - Seleccione el equipo donde está instalada la aplicación en el menú desplegable.
> - Seleccione el icono **Más opciones** (&#8943;).
> - Seleccione **Obtener vínculo al equipo**.
> - Copie y guarde el valor **groupId** de la cadena.
> - Inicie sesión en **Graph Explorador**.
> - Realice una llamada **GET** al siguiente punto de conexión: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` . El campo clientAppId de la respuesta se asignará al appId especificado en el manifiesto de la aplicación Teams.
  ![Graph respuesta del explorador a la llamada GET.](../../assets/images/graph-permissions.png)

## <a name="code-sample"></a>Ejemplo de código
| **Nombre de la muestra** | **Descripción** | **.NET** |**Node.js** |
|-----------------|-----------------|----------------|----------------|
| Consentimiento específico de recursos (RSC) | Use RSC para llamar a Graph API. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|



## <a name="see-also"></a>Vea también
 
* [Pruebe los permisos de consentimiento específicos de los recursos en Teams](test-resource-specific-consent.md)
* [Consentimiento específico de recursos en Microsoft Teams para administradores](/MicrosoftTeams/resource-specific-consent)



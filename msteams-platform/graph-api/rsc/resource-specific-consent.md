---
title: Consentimiento específico de recursos en Teams
description: Describe el consentimiento específico de los recursos en Teams y cómo aprovecharlo.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: autorización de teams OAuth SSO AAD rsc Graph
ms.openlocfilehash: 39e5c1bb8375fb5b5a3bd3900cb6ad870a3ff677
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101796"
---
# <a name="resource-specific-consent-rsc"></a>Consentimiento específico de recursos (RSC)

El consentimiento específico de recursos (RSC) es una integración de api de Microsoft Teams y Microsoft Graph que permite a la aplicación usar puntos de conexión de API para administrar equipos específicos dentro de una organización. El modelo de permisos de consentimiento específico  de recursos (RSC) permite a los propietarios del equipo conceder el consentimiento para que una aplicación acceda o modifique los datos de un equipo. Los permisos de RSC pormenorizados, Teams específicos de la aplicación definen lo que una aplicación puede hacer dentro de un equipo específico:

## <a name="resource-specific-permissions"></a>Permisos específicos de recursos

|Permisos de aplicación| Acción |
| ----- | ----- |
|TeamSettings.Read.Group | Obtén la configuración de este equipo.|
|TeamSettings.ReadWrite.Group|Actualizar la configuración de este equipo.|
|ChannelSettings.Read.Group|Obtenga los nombres de canal, las descripciones de canales y la configuración del canal para este equipo.|
|ChannelSettings.ReadWrite.Group|Actualice los nombres de canal, las descripciones de canales y la configuración del canal para este equipo.|
|Channel.Create.Group|Crear canales en este equipo.|
|Channel.Delete.Group|Eliminar canales en este equipo.|
|ChannelMessage.Read.Group |Obtener los mensajes de canal de este equipo.|
|TeamsAppInstallation.Read.Group|Obtén una lista de las aplicaciones instaladas de este equipo.|
|TeamsTab.Read.Group|Obtener una lista de las pestañas de este equipo.|
|TeamsTab.Create.Group|Crear pestañas en este equipo.|
|TeamsTab.ReadWrite.Group|Actualizar las pestañas de este equipo.|
|TeamsTab.Delete.Group|Eliminar las pestañas de este equipo.|
|TeamMember.Read.Group|Obtener los miembros de este equipo.|

>[!NOTE]
>Los permisos específicos de recursos solo están disponibles para Teams aplicaciones instaladas en el cliente Teams y actualmente no forman parte del portal Azure Active Directory web.

## <a name="enable-resource-specific-consent-in-your-application"></a>Habilitar el consentimiento específico de recursos en la aplicación

Los pasos para habilitar RSC en la aplicación son los siguientes:

1. [Configure las opciones de consentimiento del](#configure-group-owner-consent-settings-in-the-azure-ad-portal)propietario del grupo en Azure Active Directory portal .
1. [Registre la aplicación con Plataforma de identidad de Microsoft a través del portal de Azure AD](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).
1. [Revise los permisos de la aplicación en el Portal de Azure AD](#review-your-application-permissions-in-the-azure-ad-portal).
1. [Obtener un token de acceso de la plataforma Microsoft Identity](#obtain-an-access-token-from-the-microsoft-identity-platform).
1. [Actualizar el manifiesto Teams aplicación](#update-your-teams-app-manifest).
1. [Instala la aplicación directamente en Teams](#sideload-your-app-in-teams).
1. [Comprueba si la aplicación tiene permisos RSC agregados.](#check-your-app-for-added-rsc-permissions)

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a>Configurar la configuración del consentimiento del propietario del grupo en el Portal de Azure AD

Puede habilitar o deshabilitar el consentimiento del [propietario del grupo](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directamente en Azure Portal:

> [!div class="checklist"]
>
>- Inicie sesión en [Azure Portal](https://portal.azure.com) como administrador [global/administrador de la compañía](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).  
 > - [Seleccione](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** Enterprise  =>  **aplicaciones Consent** y  =>  **permisos** Configuración de  =>  **consentimiento de usuario**.
> - Habilitar, deshabilitar o limitar el consentimiento del usuario con el control etiquetado Consentimiento del propietario del grupo para las aplicaciones que tienen acceso a datos **(El** valor predeterminado es Permitir el consentimiento del propietario del grupo para todos **los propietarios del grupo).** Para que el propietario de un equipo instale una aplicación con RSC, el consentimiento del propietario del grupo debe estar habilitado para ese usuario.

![configuración de azure rsc](../../assets/images/azure-rsc-configuration.png)

Para habilitar o deshabilitar el consentimiento del propietario del grupo con PowerShell, siga los pasos descritos en [Configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a>Registrar la aplicación con Plataforma de identidad de Microsoft a través del portal de Azure AD

El Azure Active Directory web proporciona una plataforma central para que se registren y configuren las aplicaciones. La aplicación debe estar registrada en Azure AD Portal para integrarse con el Plataforma de identidad de Microsoft y llamar a las API Graph Microsoft. *Vea* [Registrar una aplicación con el Plataforma de identidad de Microsoft](/graph/auth-register-app-v2).

>[!WARNING]
>No registre varias aplicaciones Teams en el mismo identificador de aplicación de Azure AD. El identificador de la aplicación debe ser único para cada aplicación. Se producirá un error al intentar instalar varias aplicaciones en el mismo identificador de aplicación.

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Revisar los permisos de la aplicación en el Portal de Azure AD

Vaya a la **página Registros** de la aplicación principal y seleccione la aplicación  =>   RSC. Elija **permisos de API en** la barra de navegación izquierda y examine la lista de permisos configurados para la aplicación. Si la aplicación solo realizará llamadas Graph API de RSC, elimina todos los permisos de esa página. Si la aplicación también realizará llamadas que no son de RSC, mantén esos permisos según sea necesario.

>[!IMPORTANT]
>El portal de Azure AD no se puede usar para solicitar permisos de RSC. Actualmente, los permisos RSC son exclusivos Teams aplicaciones instaladas en el cliente de Teams y se declaran en el archivo de manifiesto de aplicación (JSON).

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Obtener un token de acceso de la Plataforma de identidad de Microsoft

Para realizar Graph API, debes obtener un token de acceso para la aplicación desde la plataforma de identidad. Para que la aplicación pueda obtener un token del Plataforma de identidad de Microsoft, debe registrarse en el Portal de Azure AD. El token de acceso contiene información sobre la aplicación y los permisos que tiene para los recursos y las API disponibles a través de Microsoft Graph.

Deberá tener los siguientes valores del proceso de registro de Azure AD para recuperar un token de acceso de la plataforma de identidad:

- Id. **de aplicación** asignado por el portal de registro de aplicaciones. Si la aplicación admite el inicio de sesión único (SSO), debes usar el mismo identificador de aplicación para tu aplicación y SSO.
- El  **secreto de cliente/contraseña** o un par de claves público/privado (**Certificado**). Esto no es necesario para las aplicaciones nativas.
- Uri **de redireccionamiento** (o dirección URL de respuesta) para que la aplicación reciba respuestas de Azure AD.

 *Consulta* [Obtener acceso en nombre de un usuario y](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) Obtener acceso sin un [usuario](/graph/auth-v2-service)

## <a name="update-your-teams-app-manifest"></a>Actualizar el manifiesto Teams aplicación

Los permisos RSC se declaran en el archivo de manifiesto de aplicación (JSON).  Agregue una [clave webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) al manifiesto de la aplicación con los siguientes valores:

> [!div class="checklist"]
>
> - **id:**  el identificador de la aplicación de Azure AD. *Vea* [Registrar la aplicación en el Portal de Azure AD](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).
> - **resource:**  cualquier cadena. Este campo no tiene ninguna operación en RSC, pero debe agregarse y tener un valor para evitar una respuesta de error; cualquier cadena lo hará.
> - **permisos de aplicación:** permisos RSC para la aplicación. *Consulte* [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).

>
>[!IMPORTANT]
> Los permisos que no son RSC se almacenan en Azure Portal. No los agregues al manifiesto de la aplicación.
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

## <a name="sideload-your-app-in-teams"></a>Descarga local de la aplicación en Teams

Si el Teams permite cargas de aplicaciones personalizadas, [puedes](~/concepts/deploy-and-publish/apps-upload.md) realizar la instalación local de la aplicación directamente en un equipo específico.

## <a name="check-your-app-for-added-rsc-permissions"></a>Comprueba la aplicación para obtener permisos RSC agregados

>[!IMPORTANT]
>Los permisos RSC no se atribuyó a un usuario. Las llamadas se realizan con permisos de aplicación, no con permisos delegados por el usuario. Por lo tanto, es posible que la aplicación pueda realizar acciones que el usuario no pueda, como crear un canal o eliminar una pestaña. Debe revisar la intención del propietario del equipo para su caso de uso antes de realizar llamadas a la API de RSC. *Vea* [Microsoft Teams introducción a la API .](/graph/teams-concept-overview)

Una vez instalada la aplicación en un equipo, puedes usar [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) para ver los permisos que se han concedido a la aplicación en un equipo:

> [!div class="checklist"]
>
>- Obtenga el **groupId** del equipo desde el Teams cliente.
> - En el Teams, seleccione **Teams** de la barra de navegación de la izquierda.
> - Selecciona el equipo donde está instalada la aplicación en el menú desplegable.
> - Seleccione el **icono Más opciones** (&#8943;).
> - Seleccione **Obtener vínculo al equipo**.
> - Copie y guarde el **valor groupId** de la cadena.
> - Inicie sesión **en Graph Explorer**.
> - Realice una **llamada GET** al siguiente extremo: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` . El campo clientAppId de la respuesta se asignará al appId especificado en el manifiesto Teams aplicación.
  ![Graph respuesta del explorador a la llamada GET.](../../assets/images/graph-permissions.png)

## <a name="code-sample"></a>Ejemplo de código
| **Nombre de ejemplo** | **Descripción** | **.NET** |**Node.js** |
|-----------------|-----------------|----------------|----------------|
| Consentimiento específico de recursos (RSC) | Use RSC para llamar a Graph API. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|



## <a name="test-resource-specific-consent"></a>Probar el consentimiento específico de los recursos
 
> [!div class="nextstepaction"]
> [**Probar permisos de consentimiento específicos de recursos en Teams**](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a>Tema relacionado para Teams administradores

> [!div class="nextstepaction"]
> [**Consentimiento específico de recursos en Microsoft Teams para administradores**](/MicrosoftTeams/resource-specific-consent)
> 


---
title: Habilitar el consentimiento específico de recursos en Teams
description: Describe el consentimiento específico de los recursos en Teams y cómo aprovecharlo.
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: reference
keywords: autorización de teams OAuth SSO AAD rsc Graph
ms.openlocfilehash: c013153470b4be54df82fa313b5d2f8dca16fe9a
ms.sourcegitcommit: 95e0c767ca0f2a51c4a7ca87700ce50b7b154b7c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2021
ms.locfileid: "58528953"
---
# <a name="resource-specific-consent"></a>Consentimiento específico del recurso

> [!NOTE]
> El consentimiento específico de los recursos para el ámbito de chat solo está disponible en [la versión preliminar del desarrollador](../../resources/dev-preview/developer-preview-intro.md) público.

El consentimiento específico de recursos (RSC) es una integración de api de Microsoft Teams y Microsoft Graph que permite a la aplicación usar puntos de conexión de API para administrar recursos específicos, ya sea de equipos o chats, dentro de una organización. El modelo de permisos  RSC permite a los propietarios de equipos y propietarios de *chat* conceder consentimiento para que una aplicación acceda y modifique los datos de un equipo y los datos de un chat, respectivamente. 

**Nota:** Si un chat tiene una reunión o una llamada asociada a ella, los permisos de RSC relevantes también se aplican a esos recursos.

## <a name="resource-specific-permissions"></a>Permisos específicos de recursos

Los permisos de RSC pormenorizados, Teams específicos de la aplicación definen lo que una aplicación puede hacer dentro de un recurso específico.

### <a name="resource-specific-permissions-for-a-team"></a>Permisos específicos de recursos para un equipo

|Permiso de aplicación| Acción |
| ----- | ----- |
|TeamSettings.Read.Group | Obtén la configuración de este equipo.|
|TeamSettings.ReadWrite.Group|Actualice la configuración de este equipo.|
|ChannelSettings.Read.Group|Obtén los nombres de canal de este equipo, las descripciones de canales y la configuración del canal.|
|ChannelSettings.ReadWrite.Group|Actualice los nombres de canal de este equipo, las descripciones de canales y la configuración del canal.|
|Channel.Create.Group|Crear canales en este equipo. |
|Channel.Delete.Group|Eliminar canales en este equipo. |
|ChannelMessage.Read.Group |Obtener los mensajes de canal de este equipo. |
|TeamsAppInstallation.Read.Group|Obtén una lista de las aplicaciones instaladas de este equipo.|
|TeamsTab.Read.Group|Obtener una lista de las pestañas de este equipo.|
|TeamsTab.Create.Group|Crear pestañas en este equipo. |
|TeamsTab.ReadWrite.Group|Actualizar las pestañas de este equipo. |
|TeamsTab.Delete.Group|Eliminar las pestañas de este equipo. |
|TeamMember.Read.Group|Obtener los miembros de este equipo. |

Para obtener más información, vea [permisos de consentimiento específicos de recursos de equipo.](/graph/permissions-reference#teams-resource-specific-consent-permissions)

### <a name="resource-specific-permissions-for-a-chat"></a>Permisos específicos de recursos para un chat

En la tabla siguiente se proporcionan permisos específicos de recursos para un chat:

|Permiso de aplicación| Acción |
| ----- | ----- |
| ChatSettings.Read.Chat         | Obtén la configuración de este chat.                                    |
| ChatSettings.ReadWrite.Chat    | Actualice la configuración de este chat.                          |
| ChatMessage.Read.Chat          | Obtener los mensajes de este chat.                                    |
| ChatMember.Read.Chat           | Obtener los miembros de este chat.                                     |
| Chat.Manage.Chat               | Administrar este chat.                                             |
| TeamsTab.Read.Chat             | Obtén las pestañas de este chat.                                        |
| TeamsTab.Create.Chat           | Crear pestañas en este chat.                                     |
| TeamsTab.Delete.Chat           | Eliminar las pestañas de este chat.                                      |
| TeamsTab.ReadWrite.Chat        | Administrar las pestañas de este chat.                                      |
| TeamsAppInstallation.Read.Chat | Obtén las aplicaciones instaladas en este chat.                   |
| OnlineMeeting.ReadBasic.Chat   | Lea las propiedades básicas, como el nombre, la programación, el organizador, el vínculo de unión y las notificaciones de inicio y finalización de una reunión asociada a este chat. |
| Calls.AccessMedia.Chat         | Accede a secuencias multimedia en llamadas asociadas a este chat o reunión.                                    |
| Calls.JoinGroupCalls.Chat         | Unirse a llamadas asociadas a este chat o reunión.                                    |

Para obtener más información, vea [permisos de consentimiento específicos de recursos de chat.](/graph/permissions-reference#chat-resource-specific-consent-permissions)

> [!NOTE]
> Los permisos específicos de recursos solo están disponibles para Teams aplicaciones instaladas en el cliente de Teams y actualmente no forman parte del portal de Azure Active Directory (AAD).

## <a name="enable-rsc-in-your-application"></a>Habilitar RSC en la aplicación

1. [Configure las opciones de consentimiento en el portal de AAD](#configure-consent-settings-in-the-aad-portal).
    1. [Configurar la configuración de consentimiento del propietario del grupo para RSC en un equipo](#configure-group-owner-consent-settings-for-rsc-in-a-team).
    1. [Configurar las opciones de consentimiento del usuario para RSC en un chat](#configure-user-consent-settings-for-rsc-in-a-chat).
1. [Registra tu aplicación con Plataforma de identidad de Microsoft el portal de AAD](#register-your-app-with-microsoft-identity-platform-using-the-aad-portal).
1. [Revise los permisos de la aplicación en el portal de AAD](#review-your-application-permissions-in-the-aad-portal).
1. [Obtener un token de acceso de la plataforma de identidad](#obtain-an-access-token-from-the-microsoft-identity-platform).
1. [Actualizar el manifiesto Teams aplicación](#update-your-teams-app-manifest).
1. [Instala la aplicación directamente en Teams](#sideload-your-app-in-teams).
1. [Comprueba si la aplicación tiene permisos RSC agregados.](#check-your-app-for-added-rsc-permissions)
    1. [Comprueba que la aplicación tenga permisos de RSC agregados en un equipo](#check-your-app-for-added-rsc-permissions-in-a-team).
    1. [Comprueba que la aplicación tenga permisos RSC agregados en un chat.](#check-your-app-for-added-rsc-permissions-in-a-chat)

## <a name="configure-consent-settings-in-the-aad-portal"></a>Configurar las opciones de consentimiento en el portal de AAD

### <a name="configure-group-owner-consent-settings-for-rsc-in-a-team"></a>Configurar la configuración de consentimiento del propietario del grupo para RSC en un equipo

Puede habilitar o deshabilitar el consentimiento del [propietario del grupo](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directamente en Azure Portal:

1. Inicie sesión en [Azure Portal](https://portal.azure.com) como administrador global o administrador de [la compañía.](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)
1. Seleccione **Azure Active Directory** Enterprise permisos Configuración de consentimiento de usuario y  >    >    >  [**permisos.**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)
1. Habilitar, deshabilitar o limitar el consentimiento del usuario con el control etiquetado Consentimiento del propietario del grupo **para las aplicaciones que tienen acceso a datos.** El valor predeterminado es **Permitir el consentimiento del propietario del grupo para todos los propietarios del grupo.** Para que el propietario de un equipo instale una aplicación con RSC, el consentimiento del propietario del grupo debe estar habilitado para ese usuario.

    ![Configuración del equipo de Azure RSC](../../assets/images/azure-rsc-team-configuration.png)

Además, puede habilitar o deshabilitar el consentimiento del propietario del grupo con PowerShell, siga los pasos descritos en configurar el consentimiento del propietario del grupo [con PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).

### <a name="configure-user-consent-settings-for-rsc-in-a-chat"></a>Configurar las opciones de consentimiento del usuario para RSC en un chat

Puede habilitar o deshabilitar el [consentimiento del usuario](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) directamente en Azure Portal:

1. Inicie sesión en [Azure Portal](https://portal.azure.com) como administrador global o administrador de [la compañía.](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)
1. Seleccione **Azure Active Directory** Enterprise permisos Configuración de consentimiento de usuario y  >    >    >  [**permisos.**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)
1. Habilitar, deshabilitar o limitar el consentimiento del usuario con el control etiquetado Consentimiento de **usuario para aplicaciones**. El valor predeterminado es **Permitir el consentimiento del usuario para aplicaciones.** Para que un miembro de chat instale una aplicación con RSC, el consentimiento del usuario debe estar habilitado para ese usuario.

    ![Configuración de chat de Azure RSC](../../assets/images/azure-rsc-chat-configuration.png)

Además, puede habilitar o deshabilitar el consentimiento de usuario con PowerShell, siga los pasos descritos en configurar el consentimiento de usuario [con PowerShell](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell).

## <a name="register-your-app-with-microsoft-identity-platform-using-the-aad-portal"></a>Registrar la aplicación con Plataforma de identidad de Microsoft el portal de AAD

El portal de AAD proporciona una plataforma central para que se registren y configuren las aplicaciones. La aplicación debe estar registrada en el portal de AAD para integrarse con la plataforma de identidad y llamar a las API Graph Microsoft. Para obtener más información, vea [registrar una aplicación con la plataforma de identidad](/graph/auth-register-app-v2).

> [!WARNING]
> Un identificador de aplicación de AAD no debe compartirse entre varias Teams aplicaciones. Debe haber una asignación 1:1 entre una Teams y una aplicación de AAD. Los intentos de instalar Teams aplicaciones asociadas con el mismo identificador de aplicación de AAD provocarán errores de instalación o tiempo de ejecución.

## <a name="review-your-application-permissions-in-the-aad-portal"></a>Revisar los permisos de la aplicación en el portal de AAD

1. Ve a la **página Registros** de la  >  **aplicación principal** y selecciona la aplicación RSC.
1. Elija **permisos de API** en el panel izquierdo y vaya a la lista de permisos **configurados** para la aplicación. Si la aplicación solo realiza llamadas Graph API de RSC, elimina todos los permisos de esa página. Si la aplicación también realiza llamadas que no son RSC, mantén esos permisos según sea necesario.

> [!IMPORTANT]
> El portal de AAD no se puede usar para solicitar permisos RSC. Actualmente, los permisos RSC son exclusivos de las aplicaciones Teams instaladas en el cliente de Teams y se declaran en el archivo de manifiesto de Teams aplicación (JSON).

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Obtener un token de acceso de la Plataforma de identidad de Microsoft

Para realizar Graph API, debes obtener un token de acceso para la aplicación desde la plataforma de identidad. Para que la aplicación pueda obtener un token de la plataforma de identidad, debe registrarse en el portal de AAD. El token de acceso contiene información sobre la aplicación y los permisos que tiene para los recursos y las API disponibles a través de Microsoft Graph.

Debe tener los siguientes valores del proceso de registro de AAD para recuperar un token de acceso de la plataforma de identidad:

- Id. **de aplicación** asignado por el portal de registro de aplicaciones. Si la aplicación admite el inicio de sesión único (SSO), debes usar el mismo identificador de aplicación para tu aplicación y SSO.
- El **secreto de cliente/contraseña** o un par de claves pública o privada que es **Certificate**. Esto no es necesario para las aplicaciones nativas.
- Uri **de redireccionamiento** o dirección URL de respuesta para que la aplicación reciba respuestas de AAD.

Para obtener más información, [vea obtener acceso en nombre de un usuario y](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) obtener acceso sin un [usuario](/graph/auth-v2-service).

## <a name="update-your-teams-app-manifest"></a>Actualizar el manifiesto Teams aplicación

Los permisos RSC se declaran en el archivo JSON del manifiesto de la aplicación. Agregue una [clave webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) al manifiesto de la aplicación con los siguientes valores:

|Nombre| Tipo | Descripción|
|---|---|---|
|`id` |String |Id. de aplicación de AAD. Para obtener más información, [consulta Registrar la aplicación en el portal de AAD](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-aad-portal).|
|`resource`|String| Este campo no tiene ninguna operación en RSC, pero debe agregarse y tener un valor para evitar una respuesta de error; cualquier cadena lo hará.|
|`applicationPermissions`|Matriz de cadenas|Permisos RSC para la aplicación. Para obtener más información, [consulte resource-specific permissions](resource-specific-consent.md#resource-specific-permissions).|

>
> [!IMPORTANT]
> Los permisos que no son RSC se almacenan en Azure Portal. No los agregues al manifiesto de la aplicación.
>

### <a name="example-for-rsc-in-a-team"></a>Ejemplo de RSC en un equipo

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
        "TeamSettings.Read.Group",
        "TeamSettings.ReadWrite.Group",
        "ChannelSettings.Read.Group",
        "ChannelSettings.ReadWrite.Group",
        "Channel.Create.Group",
        "Channel.Delete.Group",
        "ChannelMessage.Read.Group",
        "TeamsAppInstallation.Read.Group",
        "TeamsTab.Read.Group",
        "TeamsTab.Create.Group",
        "TeamsTab.ReadWrite.Group",
        "TeamsTab.Delete.Group",
        "TeamMember.Read.Group"
    ]
  }
```

### <a name="example-for-rsc-in-a-chat"></a>Ejemplo de RSC en un chat

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
        "ChatSettings.Read.Chat",
        "ChatSettings.ReadWrite.Chat",
        "ChatMessage.Read.Chat",
        "ChatMember.Read.Chat",
        "Chat.Manage.Chat",
        "TeamsTab.Read.Chat",
        "TeamsTab.Create.Chat",
        "TeamsTab.Delete.Chat",
        "TeamsTab.ReadWrite.Chat",
        "TeamsAppInstallation.Read.Chat",
        "OnlineMeeting.ReadBasic.Chat",
        "Calls.AccessMedia.Chat",
        "Calls.JoinGroupCalls.Chat"
    ]
  }
```

> [!NOTE]
> Si la aplicación está pensada para admitir la instalación en ámbitos de equipo y chat, los permisos de equipo y chat se pueden especificar en el mismo manifiesto en `applicationPermissions` .

## <a name="sideload-your-app-in-teams"></a>Descarga local de la aplicación en Teams

Si el Teams permite cargas de aplicaciones personalizadas, puedes realizar la instalación local de la aplicación directamente en un equipo o chat específico. [](~/concepts/deploy-and-publish/apps-upload.md)

## <a name="check-your-app-for-added-rsc-permissions"></a>Comprueba la aplicación para obtener permisos RSC agregados

> [!IMPORTANT]
> Los permisos RSC no se atribuyó a un usuario. Las llamadas se realizan con permisos de aplicación, no con permisos delegados por el usuario. Se puede permitir que la aplicación realice acciones que el usuario no puede, como eliminar una pestaña. Debe revisar la intención del propietario del equipo o del propietario del chat para su uso antes de realizar llamadas a la API de RSC. Para obtener más información, [vea Microsoft Teams introducción a la API.](/graph/teams-concept-overview)

Después de instalar la aplicación en un recurso, puedes usar [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) para ver los permisos que se han concedido a la aplicación en el recurso.

### <a name="check-your-app-for-added-rsc-permissions-in-a-team"></a>Comprobar la aplicación para obtener permisos de RSC agregados en un equipo

1. Obtenga el **groupId** del equipo desde Teams.
1. En Teams, seleccione **Teams** en el panel situado más a la izquierda.
1. Selecciona el equipo donde se va a instalar la aplicación.
1. Seleccione los puntos suspensivos &#x25CF;&#x25CF;&#x25CF; para ese equipo.
1. Selecciona **Obtener vínculo al equipo** en el menú desplegable del equipo.
1. Copie y guarde el **valor groupId** del **cuadro** de diálogo emergente Obtener un vínculo al equipo.
1. Inicie sesión en **Graph Explorer**.
1. Realice una **llamada GET** a este extremo: `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants` . El `clientAppId` campo de la respuesta se asignará al especificado en el manifiesto Teams `webApplicationInfo.id` aplicación.

    ![Graph respuesta del explorador a la llamada GET para permisos de RSC de equipo](../../assets/images/team-graph-permissions.png)

Para obtener más información sobre cómo obtener detalles de las aplicaciones instaladas en un equipo específico, consulta obtener los nombres y otros detalles de las aplicaciones instaladas [en el equipo especificado.](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps)

### <a name="check-your-app-for-added-rsc-permissions-in-a-chat"></a>Comprueba que la aplicación tenga permisos RSC agregados en un chat

1. Obtenga el identificador de subproceso de chat del Teams *web.*
1. En el Teams web, seleccione **Chat** en el panel situado más a la izquierda.
1. Selecciona el chat donde está instalada la aplicación en el menú desplegable.
1. Copie la dirección URL web y guarde el identificador del subproceso de chat de la cadena.

    ![Identificador de subproceso de chat desde la dirección URL web](../../assets/images/chat-thread-id.png)

1. Inicie sesión en **Graph Explorer**.
1. Realice una **llamada GET** al siguiente extremo: `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants` . El `clientAppId` campo de la respuesta se asignará al especificado en el manifiesto Teams `webApplicationInfo.id` aplicación.

    ![Graph respuesta del explorador a la llamada GET para permisos RSC de chat](../../assets/images/chat-graph-permissions.png)

Para obtener más información sobre cómo obtener detalles de las aplicaciones instaladas en un chat específico, consulta obtener los nombres y otros detalles de las aplicaciones instaladas en [el chat especificado.](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat)

## <a name="code-sample"></a>Ejemplo de código

| **Ejemplo de nombre** | **Descripción** | **.NET** |**Node.js** |
|-----------------|-----------------|----------------|----------------|
| Resource-Specific consentimiento (RSC) | Use RSC para llamar a Graph API. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|

## <a name="see-also"></a>Consulte también
 
* [Probar permisos de consentimiento específicos de recursos en Teams](test-resource-specific-consent.md)
* [Consentimiento específico de recursos en Microsoft Teams para administradores](/MicrosoftTeams/resource-specific-consent)

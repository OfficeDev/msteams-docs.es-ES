---
title: Habilitar el consentimiento específico del recurso en Teams
description: En este artículo, aprenderá el consentimiento específico de recursos en Microsoft Teams y cómo aprovecharlo.
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 7321c3dbf1f2a3493a1d457cfd80d7fc1efb01d6
ms.sourcegitcommit: 82c585d287d61924ce3a3bba3e9caeff35c9a27a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/02/2022
ms.locfileid: "67586710"
---
# <a name="resource-specific-consent"></a>Consentimiento específico del recurso

> [!NOTE]
> El consentimiento específico del recurso para el ámbito de chat solo está disponible en [versión preliminar pública para desarrolladores](../../resources/dev-preview/developer-preview-intro.md).

El consentimiento específico de recursos (RSC) es una integración de la API de Microsoft Teams y Microsoft Graph que permite a la aplicación usar puntos de conexión de API para administrar recursos específicos, ya sean equipos o chats, dentro de una organización. El modelo de permisos de RSC permite a los *propietarios de equipo* y *propietarios de chats* dar consentimiento para que una aplicación acceda y modifique los datos de un equipo y los datos de un chat, respectivamente.

**Nota:** Si un chat tiene asociada una reunión o una llamada, los permisos de RSC pertinentes también se aplican a esos recursos.

## <a name="resource-specific-permissions"></a>Permisos específicos del recurso

Los permisos de RSC específicos de Teams y granulares definen lo que una aplicación puede hacer dentro de un recurso específico.

### <a name="resource-specific-permissions-for-a-team"></a>Permisos específicos del recurso para un equipo

|Permisos de aplicación| Action |
| ----- | ----- |
|TeamSettings.Read.Group | Obtener la configuración de este equipo.|
|TeamSettings.ReadWrite.Group|Actualizar la configuración de este equipo.|
|ChannelSettings.Read.Group|Obtener los nombres de canal, las descripciones de canales y la configuración del canal de este equipo.|
|ChannelSettings.ReadWrite.Group|Actualizar los nombres de canal, las descripciones de canales y la configuración del canal de este equipo.|
|Channel.Create.Group|Crear canales en este equipo. |
|Channel.Delete.Group|Eliminar canales en este equipo. |
|ChannelMessage.Read.Group |Obtener los mensajes del canal de este equipo. |
|TeamsAppInstallation.Read.Group|Obtener una lista de las aplicaciones instaladas de este equipo.|
|TeamsTab.Read.Group|Obtener una lista de las pestañas de este equipo.|
|TeamsTab.Create.Group|Crear pestañas en este equipo. |
|TeamsTab.ReadWrite.Group|Actualizar las pestañas de este equipo. |
|TeamsTab.Delete.Group|Eliminar las pestañas de este equipo. |
|TeamMember.Read.Group|Obtener los miembros de este equipo. |
|TeamsActivity.Send.Group|Crear nuevas notificaciones en las fuentes de actividad de los usuarios de este equipo. |

Para obtener más información, consulte [permisos de consentimiento específicos del recurso de equipo](/graph/permissions-reference#team-resource-specific-consent-permissions).

### <a name="resource-specific-permissions-for-a-chat"></a>Permisos específicos de recursos para un chat

En la tabla siguiente se proporcionan permisos específicos de recursos para un chat:

|Permisos de aplicación| Action |
| ----- | ----- |
| ChatSettings.Read.Chat         | Obtener la configuración de este chat.                                    |
| ChatSettings.ReadWrite.Chat    | Actualizar la configuración de este chat.                          |
| ChatMessage.Read.Chat          | Obtener los mensajes de este chat.                                    |
| ChatMember.Read.Chat           | Obtener los miembros de este chat.                                     |
| Chat.Manage.Chat               | Administrar este chat.                                             |
| TeamsTab.Read.Chat             | Obtener las pestañas de este chat.                                        |
| TeamsTab.Create.Chat           | Crear pestañas en este chat.                                     |
| TeamsTab.Delete.Chat           | Eliminar las pestañas de este chat.                                      |
| TeamsTab.ReadWrite.Chat        | Administrar las pestañas de este chat.                                      |
| TeamsAppInstallation.Read.Chat | Obtener qué aplicaciones están instaladas en este chat.                   |
| OnlineMeeting.ReadBasic.Chat   | Leer las propiedades básicas de una reunión asociada a este chat tales como el nombre, la programación, el organizador, el vínculo para unirse y las notificaciones de inicio y finalización. |
| Calls.AccessMedia.Chat         | Accede a secuencias multimedia en llamadas asociadas a este chat o reunión.                                    |
| Calls.JoinGroupCalls.Chat         | Unirse a llamadas asociadas a este chat o reunión.                                    |
| TeamsActivity.Send.Chat         | Crear nuevas notificaciones en las fuentes de actividad de los usuarios de este chat. |
| OnlineMeetingTranscript.Read.Chat | Lea las transcripciones de la reunión asociada a este chat. |

Para obtener más información, consulte [permisos de consentimiento específicos del recurso de chat](/graph/permissions-reference#chat-resource-specific-consent-permissions).

> [!NOTE]
> Los permisos específicos de recursos solo están disponibles para las aplicaciones de Teams instaladas en el cliente de Teams y actualmente no forman parte del portal de Azure Active Directory (AAD).

## <a name="enable-rsc-in-your-application"></a>Habilitar RSC en la aplicación

1. [Configure las opciones de consentimiento](#configure-consent-settings).
    1. [Configure la configuración de consentimiento del propietario del grupo para RSC en un equipo mediante el portal de Azure AD](#configure-group-owner-consent-settings-for-rsc-in-a-team-using-the-azure-ad-portal).
    1. [Configure las opciones de consentimiento del propietario del chat para RSC en un chat mediante las API de Microsoft Graph](#configure-chat-owner-consent-settings-for-rsc-in-a-chat-using-the-microsoft-graph-apis).
1. [Registre la aplicación con la Plataforma de identidad de Microsoft mediante el portal de Azure AD](#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal).
1. [Revise los permisos de la aplicación en el portal de Azure AD](#review-your-application-permissions-in-the-azure-ad-portal).
1. [Obtenga un token de acceso de la plataforma de identidad](#obtain-an-access-token-from-the-microsoft-identity-platform).
1. [Actualice el manifiesto de la aplicación de Teams](#update-your-teams-app-manifest).
1. [Instale la aplicación directamente en Teams](#sideload-your-app-in-teams).
1. [Compruebe si la aplicación tiene permisos RSC agregados](#check-your-app-for-added-rsc-permissions).
    1. [Compruebe si la aplicación tiene permisos RSC agregados en un equipo](#check-your-app-for-added-rsc-permissions-in-a-team).
    1. [Compruebe si la aplicación tiene permisos RSC agregados en un chat](#check-your-app-for-added-rsc-permissions-in-a-chat).

## <a name="configure-consent-settings"></a>Configuración de la configuración del consentimiento

### <a name="configure-group-owner-consent-settings-for-rsc-in-a-team-using-the-azure-ad-portal"></a>Configuración del consentimiento del propietario del grupo para RSC en un equipo mediante el portal de Azure AD

Puede habilitar o deshabilitar el [grupo de consentimiento del propietario](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directamente en el Microsoft Azure Portal:

1. Inicie sesión en el [Azure Portal](https://portal.azure.com) como [Administrador global o Administrador de empresa](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true).
1. Seleccione **Azure Active Directory** > **Aplicaciones empresariales** > **Consentimiento y permisos** > [**Configuración de consentimiento del usuario**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings).
1. Habilite, deshabilite o limite el consentimiento del usuario con el control etiquetado **Grupo de consentimiento del propietario para las aplicaciones que tienen acceso a los datos**. El valor predeterminado es **Permitir el consentimiento del propietario del grupo para todos los propietarios del grupo**. Para que el propietario del equipo instale una aplicación mediante RSC, el consentimiento del propietario del grupo debe estar habilitado para ese usuario.

    ![Configuración del equipo de RSC de Azure](../../assets/images/azure-rsc-team-configuration.png)

Además, puede habilitar o deshabilitar el consentimiento del propietario del grupo mediante PowerShell. Siga los pasos descritos en [configurar el consentimiento del propietario del grupo mediante PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).

### <a name="configure-chat-owner-consent-settings-for-rsc-in-a-chat-using-the-microsoft-graph-apis"></a>Configuración del consentimiento del propietario del chat para RSC en un chat mediante las API de Microsoft Graph

Puede habilitar o deshabilitar RSC para chats mediante Graph API. La propiedad `isChatResourceSpecificConsentEnabled` de [**teamsAppSettings**](/graph/api/teamsappsettings-update#example-1-enable-installation-of-apps-that-require-resource-specific-consent-in-chats-meetings) controla si el RSC de chat está habilitado en el inquilino.

   ![Configuración del equipo de Graph RSC](../../assets/images/rsc/graph-rsc-chat-configuration.png)

> El valor predeterminado de la propiedad **esChatResourceSpecificConsentEnabled** en función de si la [configuración de consentimiento del usuario](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) está activada o desactivada en el inquilino cuando se usa RSC para chats por primera vez. Esta puede ser la primera vez que a) recuperar [**teamsAppSettings**](/graph/api/teamsappsettings-get) o b) instalar una aplicación de Teams con permisos específicos de recursos en un chat o reunión.

## <a name="register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal"></a>Registro de la aplicación con la Plataforma de identidad de Microsoft mediante el portal de Azure AD

El portal de Azure AD proporciona una plataforma central para registrar y configurar las aplicaciones. La aplicación debe estar registrada en el portal de Azure AD para integrarse con la plataforma de identidad y llamar a las API de Microsoft Graph. Para obtener más información, consulte [ registrar una aplicación con la plataforma de identidad](/graph/auth-register-app-v2).

> [!WARNING]
> No se debe compartir un identificador de aplicación de Azure AD entre varias aplicaciones de Teams. Debe haber una asignación 1:1 entre una aplicación de Teams y una aplicación Azure AD. Los intentos de instalar varias aplicaciones de Teams que están asociadas con el mismo identificador de aplicación de Azure AD provocarán errores de instalación o tiempo de ejecución.

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Revisión de los permisos de la aplicación en el portal de Azure AD

1. Vaya a la página **Inicio** > **Registros de aplicaciones** y seleccione la aplicación RSC.
1. Elija **Permisos de API** en el panel izquierdo y revise la lista de **Permisos configurados** de la aplicación. Si la aplicación solo realiza llamadas de API RSC de Graph, elimine todos los permisos de esa página. Si la aplicación también realiza llamadas que no son de RSC, mantenga esos permisos según sea necesario.

> [!IMPORTANT]
> No se puede usar el portal de Azure AD para solicitar permisos RSC. Los permisos de RSC son exclusivos actualmente de las aplicaciones de Teams instaladas en el cliente de Teams y se declaran en el archivo de manifiesto de aplicación de Teams (JSON).

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Obtención de un token de acceso de la Plataforma de identidad de Microsoft

Para realizar llamadas a la API de Graph, debe obtener un token de acceso para la aplicación desde la plataforma de identidad. Antes de que la aplicación pueda obtener un token de la plataforma de identidad, debe registrarla en el portal de Azure AD. El token de acceso contiene información sobre la aplicación y los permisos que tiene para los recursos y las API disponibles a través de Microsoft Graph.

Debe tener los siguientes valores del proceso de registro de Azure AD para recuperar un token de acceso de la plataforma de identidad:

* El **id. de aplicación** asignado por el portal de registro de aplicaciones. Si la aplicación admite el inicio de sesión único (SSO), debe usar el mismo identificador de aplicación para la aplicación y el inicio de sesión único.
* El **secreto de cliente o contraseña** o un par de claves públicas o privadas que sean **Certificadas**. Esto no es necesario para las aplicaciones nativas.
* Un **URI de redireccionamiento** o URL de respuesta para que la aplicación reciba respuestas de Azure AD.

Para obtener más información, vea [ obtener acceso en nombre de un usuario](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) y [ obtener acceso sin un usuario](/graph/auth-v2-service).

## <a name="update-your-teams-app-manifest"></a>Actualizar el manifiesto de la aplicación de Teams

Los permisos de RSC se declaran en el archivo JSON del manifiesto de la aplicación.

> [!IMPORTANT]
> Los permisos que no son de RSC se almacenan en el Azure Portal. No los agregue al manifiesto de la aplicación.

### <a name="manifest-changes-for-resource-specific-consent"></a>Cambios de manifiesto para el consentimiento específico del recurso

<br>

<details>

<summary><b>Permisos de RSC para el manifiesto de aplicación versión 1.12</b></summary>

Agregue una clave [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) al manifiesto de la aplicación con los siguientes valores:

|Nombre| Tipo | Descripción|
|---|---|---|
|`id` |Cadena |Su id. de la aplicación de Azure AD. Para obtener más información, consulte [ registrar la aplicación en el portal de Azure AD](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal).|
|`resource`|Cadena| Este campo no tiene ninguna operación en RSC, pero debe agregarse y tener un valor para evitar una respuesta de error; cualquier cadena servirá.|

Especifique los permisos necesarios para la aplicación.

|Nombre| Tipo | Descripción|
|---|---|---|
|`authorization`|Object|Lista de permisos que la aplicación necesita para funcionar. Para obtener más información, vea [marcador de posición para la autorización de vínculos en el manifiesto]

Ejemplo de RSC en un equipo

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp"
    },
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "TeamSettings.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamSettings.ReadWrite.Group",
                "type": "Application"
            },
            {
                "name": "ChannelSettings.Read.Group",
                "type": "Application"
            },
            {
                "name": "ChannelSettings.ReadWrite.Group",
                "type": "Application"
            },
            {
                "name": "Channel.Create.Group",
                "type": "Application"
            },
            {
                "name": "Channel.Delete.Group",
                "type": "Application"
            },
            {
                "name": "ChannelMessage.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamsAppInstallation.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Create.Group",
                "type": "Application"
            },
            {
                "name": "TeamsTab.ReadWrite.Group",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Delete.Group",
                "type": "Application"
            },
            {
                "name": "TeamMember.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamsActivity.Send.Group",
                "type": "Application"
            }
        ]    
    }
}
```

Ejemplo de RSC en un chat

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp"
    },
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "ChatSettings.Read.Chat",
                "type": "Application"
            },
            {
                "name": "ChatSettings.ReadWrite.Chat",
                "type": "Application"
            },
            {
                "name": "ChatMessage.Read.Chat",
                "type": "Application"
            },
            {
                "name": "ChatMember.Read.Chat",
                "type": "Application"
            },
            {
                "name": "Chat.Manage.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Read.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Create.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Delete.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsTab.ReadWrite.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsAppInstallation.Read.Chat",
                "type": "Application"
            },
            {
                "name": "OnlineMeeting.ReadBasic.Chat",
                "type": "Application"
            },
            {
                "name": "Calls.AccessMedia.Chat",
                "type": "Application"
            },
            {
                "name": "Calls.JoinGroupCalls.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsActivity.Send.Chat",
                "type": "Application"
            }
        ]    
    }
}
```

> [!NOTE]
> Si la aplicación está pensada para admitir la instalación en ámbitos de equipo y chat, se pueden especificar permisos de equipo y chat en el mismo manifiesto en `authorization`.

<br>

</details>

<br>

<details>

<summary><b>Permisos de RSC para la versión 1.11 o anterior del manifiesto de aplicación</b></summary>

Agregue una clave [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) al manifiesto de la aplicación con los siguientes valores:

|Nombre| Tipo | Descripción|
|---|---|---|
|`id` |Cadena |Su id. de la aplicación de Azure AD. Para obtener más información, consulte [ registrar la aplicación en el portal de Azure AD](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal).|
|`resource`|Cadena| Este campo no tiene ninguna operación en RSC, pero debe agregarse y tener un valor para evitar una respuesta de error; cualquier cadena servirá.|
|`applicationPermissions`|Matriz de cadenas|Permisos de RSC para la aplicación. Para obtener más información, vea [permisos específicos del recurso](resource-specific-consent.md#resource-specific-permissions).|

Ejemplo de RSC en un equipo

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
        "TeamMember.Read.Group",
        "TeamsActivity.Send.Group"
    ]
  }
```

Ejemplo de RSC en un chat

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
        "Calls.JoinGroupCalls.Chat",
        "TeamsActivity.Send.Chat"
    ]
  }
```

> [!NOTE]
> Si la aplicación está pensada para admitir la instalación en ámbitos de equipo y chat, se pueden especificar permisos de equipo y chat en el mismo manifiesto en `applicationPermissions`.

<br>

</details>

## <a name="sideload-your-app-in-teams"></a>Transferir localmente la aplicación en Teams

Si el administrador de Teams permite cargas de aplicaciones personalizadas, puede [transferir localmente la aplicación](~/concepts/deploy-and-publish/apps-upload.md) directamente a un equipo o chat específico.

## <a name="check-your-app-for-added-rsc-permissions"></a>Comprobación de los permisos de RSC agregados en la aplicación

> [!IMPORTANT]
> Los permisos de RSC no se atribuirán a un usuario. Las llamadas se realizan con permisos de aplicación, no con permisos delegados de usuario. La aplicación puede tener permiso para realizar acciones que el usuario no puede realizar, como eliminar una pestaña. Debe revisar la intención del propietario del equipo o del propietario del chat para su uso antes de realizar llamadas a la API de RSC. Para obtener más información, vea [Introducción a la API de Microsoft Teams](/graph/teams-concept-overview).

Una vez instalada la aplicación en un recurso, puede usar el [Probador de Graph](https://developer.microsoft.com/graph/graph-explorer) para ver los permisos que se han concedido a la aplicación en el recurso.

### <a name="check-your-app-for-added-rsc-permissions-in-a-team"></a>Comprobar si la aplicación tiene permisos RSC agregados en un equipo

1. Obtenga el **groupId** del equipo de Teams.
1. En Teams, seleccione **Equipos** en el panel izquierdo.
1. Seleccione el equipo donde se va a instalar la aplicación.
1. Seleccione los puntos suspensivos &#x25CF;&#x25CF;&#x25CF; para ese equipo.
1. Seleccione **Obtener vínculo al equipo** en el menú desplegable del equipo.
1. Copie y guarde el valor **groupId** del cuadro de diálogo emergente **Obtener un vínculo al equipo**.
1. Inicie sesión en el **Probador de Graph**.
1. Realice una llamada **GET** a este punto de conexión: `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants`. El campo `clientAppId` de la respuesta se asignará al `webApplicationInfo.id` especificado en el manifiesto de aplicación de Teams.

    ![Respuesta del Probador de Graph a la llamada GET para los permisos RSC del equipo](../../assets/images/team-graph-permissions.png)

Para obtener más información sobre cómo obtener detalles de las aplicaciones instaladas en un equipo específico, vea [obtener los nombres y otros detalles de las aplicaciones instaladas en el equipo especificado](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps).

### <a name="check-your-app-for-added-rsc-permissions-in-a-chat"></a>Comprobar si la aplicación tiene permisos RSC agregados en un chat

1. Obtenga el identificador de subproceso de chat del cliente *web* de Teams.
1. En el cliente web de Teams, seleccione **Chat** en el panel izquierdo.
1. Seleccione el chat donde se instala la aplicación en el menú desplegable.
1. Copie la dirección URL web y guarde el identificador de subproceso de chat de la cadena.

    ![Id. de subproceso de chat de la dirección URL web](../../assets/images/chat-thread-id.png)

1. Inicie sesión en el **Probador de Graph**.
1. Realice una llamada **GET** al siguiente punto de conexión: `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants`. El campo `clientAppId` de la respuesta se asignará al `webApplicationInfo.id` especificado en el manifiesto de aplicación de Teams.

    ![Respuesta del Probador de Graph a la llamada GET para los permisos RSC del chat](../../assets/images/chat-graph-permissions.png)

Para obtener más información sobre cómo obtener detalles de aplicaciones instaladas en un chat específico, vea [obtener los nombres y otros detalles de las aplicaciones instaladas en el chat especificado](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat).

## <a name="code-sample"></a>Ejemplo de código

| **Ejemplo de nombre** | **Descripción** | **.NET** |**Node.js** |
|-----------------|-----------------|----------------|----------------|
| Consentimiento específico de recursos (RSC) | Use RSC para llamar a la API de Graph. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|

## <a name="see-also"></a>Consulte también

* [Probar permisos de consentimiento específicos del recurso en Teams](test-resource-specific-consent.md)
* [Consentimiento específico del recurso en Microsoft Teams para administradores](/MicrosoftTeams/resource-specific-consent)

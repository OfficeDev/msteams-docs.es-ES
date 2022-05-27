---
title: Probar permisos de consentimiento específicos del recurso en Teams
description: Detalles de la prueba del consentimiento específico de recursos en Teams mediante Postman con ejemplos de código
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: tutorial
keywords: teams autorización del inicio de sesión único de OAuth Microsoft Azure Active Directory (Azure AD) rsc Postman Graph
ms.openlocfilehash: 60014699aa1275df787fcf553ae04671d1105f1c
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757447"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a>Probar permisos de consentimiento específicos del recurso en Teams

> [!NOTE]
> El consentimiento específico del recurso para el ámbito de chat solo está disponible en [versión preliminar pública para desarrolladores](../../resources/dev-preview/developer-preview-intro.md).

El consentimiento específico de recursos (RSC) es una integración de la API de Microsoft Teams y Microsoft Graph que permite a la aplicación usar puntos de conexión de API para administrar recursos específicos, ya sean equipos o chats, dentro de una organización. Para obtener más información, consulte [ Consentimiento específico del recurso (RSC) — Graph API](resource-specific-consent.md) de Microsoft Teams.

## <a name="prerequisites"></a>Requisitos previos

Asegúrese de comprobar los siguientes cambios en el manifiesto de la aplicación para el consentimiento específico del recurso antes de realizar las pruebas:

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
|`authorization`|Object|Lista de permisos que la aplicación necesita para funcionar. Para obtener más información, vea [autorización](../../resources/schema/manifest-schema.md#authorization).|

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

<br>

> [!NOTE]
> Si la aplicación está pensada para admitir la instalación en ámbitos de equipo y chat, se pueden especificar permisos de equipo y chat en el mismo manifiesto en `applicationPermissions`.

</details>

> [!IMPORTANT]
> En el manifiesto de la aplicación, incluya solo los permisos de RSC que quiera que tenga la aplicación.

> [!NOTE]
> Si la aplicación está diseñada para acceder a las API de llamadas o multimedia, el `webApplicationInfo.Id` debe ser el identificador de aplicación Azure AD de un [Azure Bot Service](/graph/cloud-communications-get-started#register-a-bot).

## <a name="test-added-rsc-permissions-to-a-team-using-the-postman-app"></a>Prueba de los permisos de RSC agregados a un equipo mediante la aplicación Postman

Para comprobar si los permisos RSC son respetados por la carga útil de la solicitud de la API, debe copiar el código de prueba [RSC JSON para el equipo](test-team-rsc-json-file.md) en su entorno local y actualizar los siguientes valores:

* `azureADAppId`: id. de aplicación Azure AD de la aplicación.
* `azureADAppSecret`: Contraseña de la aplicación de Azure AD.
* `token_scope`: El ámbito es necesario para obtener un token. Establecer el valor en https://graph.microsoft.com/.default.
* `teamGroupId`: puede obtener el identificador del grupo de equipo del cliente de Teams de la siguiente manera:

    1. En el cliente de Teams, seleccione **Teams** en la barra de navegación izquierda.
    2. Seleccione el chat donde se instala la aplicación en el menú desplegable.
    3. Seleccione el icono **Más opciones** (&#8943;)
    4. Seleccione **Obtener el vínculo para el equipo**.
    5. Copie y guarde el valor **groupId** de la cadena.

## <a name="test-added-rsc-permissions-to-a-chat-using-the-postman-app"></a>Prueba de los permisos RSC agregados a un chat mediante la aplicación Postman

Para comprobar si la carga de solicitud de API respeta los permisos de RSC, debe copiar el [ código de prueba JSON RSC para chats](test-chat-rsc-json-file.md) en el entorno local y actualizar los valores siguientes:

* `azureADAppId`: id. de aplicación Azure AD de la aplicación.
* `azureADAppSecret`: Contraseña de la aplicación de Azure AD.
* `token_scope`: El ámbito es necesario para obtener un token. Establecer el valor en https://graph.microsoft.com/.default.
* `tenantId`: el nombre o el identificador de objeto Azure AD del inquilino.
* `chatId`: puede obtener el identificador de subproceso de chat del cliente de Teams *web* de la siguiente manera:

    1. En el cliente web de Teams, seleccione **Chat** en la barra de navegación izquierda.
    2. Seleccione el chat donde se instala la aplicación en el menú desplegable.
    3. Copie la dirección URL web y guarde el identificador de subproceso de chat de la cadena.
![Id. de subproceso de chat de la dirección URL web.](../../assets/images/chat-thread-id.png)

### <a name="use-postman"></a>Usar Postman

1. Abra la aplicación [Postman](https://www.postman.com).
2. Seleccione **Archivo** > **Importar** > **Importar archivo** para cargar el archivo JSON actualizado desde su entorno.  
3. Seleccione la pestaña **Collections**.
4. Seleccione el botón de contenido adicional **>** junto a la **Test RSC** para expandir la vista de detalles y ver las solicitudes de API.

Ejecute toda la colección de permisos para cada llamada API. Los permisos especificados en el manifiesto de la aplicación deben ser correctos, mientras que los que no se especifiquen deben producir un error con un código de estado HTTP 403. Compruebe todos los códigos de estado de respuesta para confirmar que el comportamiento de los permisos de RSC en la aplicación cumple las expectativas.

> [!NOTE]
> Para probar llamadas a DELETE y READ API específicas, agregue esos escenarios de instancia al archivo JSON.

## <a name="test-revoked-rsc-permissions-using-postman"></a>Pruebe los permisos RSC revocados mediante [Postman](https://www.postman.com/)

1. Desinstale la aplicación del recurso específico.
2. Siga los pasos para chat o equipo:
    1. [Test agregó permisos RSC a un equipo mediante Postman](#test-added-rsc-permissions-to-a-team-using-the-postman-app).
    2. [Test agregó permisos RSC a un chat mediante Postman](#test-added-rsc-permissions-to-a-chat-using-the-postman-app).
3. Compruebe todos los códigos de estado de respuesta para confirmar que las llamadas API específicas **se produjo un error con un código de estado HTTP 403**.

## <a name="see-also"></a>Consulte también

* [Microsoft Graph API y Teams](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)
* [Consentimiento específico del recurso](~/graph-api/rsc/resource-specific-consent.md)

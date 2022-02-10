---
title: Probar permisos de consentimiento específicos de recursos en Teams
description: Detalles que prueban el consentimiento específico de los recursos Teams usar Postman con ejemplos de código
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: tutorial
keywords: autorización de OAuth SSO Microsoft Azure Active Directory (Azure AD) rsc Postman Graph
ms.openlocfilehash: 15a2a80a8f1ce280b462ed6e6e99242fb30f0dc3
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518124"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a>Probar permisos de consentimiento específicos de recursos en Teams

> [!NOTE]
> El consentimiento específico de los recursos para el ámbito de chat solo está disponible en [la versión preliminar del desarrollador](../../resources/dev-preview/developer-preview-intro.md) público.

El consentimiento específico de recursos (RSC) es una integración de api de Microsoft Teams y Graph que permite a la aplicación usar puntos de conexión de API para administrar recursos específicos (ya sea equipos o chats) dentro de una organización. Para obtener más información, vea [Resource-specific consent (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).

## <a name="prerequisites"></a>Requisitos previos

Asegúrese de comprobar los siguientes cambios en el manifiesto de la aplicación para obtener el consentimiento específico de los recursos antes de realizar las pruebas:

<br>

<details>

<summary><b>Permisos de RSC para el manifiesto de la aplicación versión 1.12</b></summary>

Agregue una [clave webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) al manifiesto de la aplicación con los siguientes valores:

|Nombre| Tipo | Descripción|
|---|---|---|
|`id` |String |El Microsoft Azure Active Directory de aplicación Azure AD (Azure AD). Para obtener más información, [consulta registrar la aplicación en el Microsoft Azure Active Directory (Azure AD).](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)|
|`resource`|String| Este campo no tiene ninguna operación en RSC, pero debe agregarse y tener un valor para evitar una respuesta de error; cualquier cadena lo hará.|

Especifica los permisos necesarios para la aplicación.

|Nombre| Tipo | Descripción|
|---|---|---|
|`authorization`|Object|Lista de permisos que la aplicación necesita para funcionar. Para obtener más información, consulte [autorización](../../resources/schema/manifest-schema.md#authorization).|

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
> Si la aplicación está pensada para admitir la instalación en ámbitos de equipo y chat, los permisos de equipo y chat se pueden especificar en el mismo manifiesto en `authorization`.

</details>

<br>

<details>

<summary><b>Permisos de RSC para manifiesto de aplicación versión 1.11 o anterior</b></summary>

Agregue una [clave webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) al manifiesto de la aplicación con los siguientes valores:

|Nombre| Tipo | Descripción|
|---|---|---|
|`id` |String |El Microsoft Azure Active Directory de aplicación Azure AD (Azure AD). Para obtener más información, [consulta registrar la aplicación en el Microsoft Azure Active Directory (Azure AD).](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)|
|`resource`|String| Este campo no tiene ninguna operación en RSC, pero debe agregarse y tener un valor para evitar una respuesta de error; cualquier cadena lo hará.|
|`applicationPermissions`|Matriz de cadenas|Permisos RSC para la aplicación. Para obtener más información, vea [permisos específicos de recursos](resource-specific-consent.md#resource-specific-permissions).|

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
> Si la aplicación está pensada para admitir la instalación en ámbitos de equipo y chat, los permisos de equipo y chat se pueden especificar en el mismo manifiesto en `applicationPermissions`.
    
</details>

> [!IMPORTANT]
> En el manifiesto de la aplicación, solo incluye los permisos de RSC que quieras que tenga la aplicación.

> [!NOTE]
> Si la aplicación está destinada a tener acceso a las API de llamadas o medios, `webApplicationInfo.Id` debe ser el identificador de aplicación Microsoft Azure Active Directory (Azure AD) de un servicio [bot de Azure](/graph/cloud-communications-get-started#register-a-bot).

## <a name="test-added-rsc-permissions-to-a-team-using-the-postman-app"></a>Probar los permisos RSC agregados a un equipo mediante la aplicación Postman

Para comprobar si la carga de solicitud de API está respetando los permisos RSC, debe copiar el código de prueba [JSON de RSC](test-team-rsc-json-file.md) para el equipo en el entorno local y actualizar los siguientes valores:

* `azureADAppId`: El identificador de aplicación Microsoft Azure Active Directory aplicación (Azure AD) de la aplicación.
* `azureADAppSecret`: La contraseña Microsoft Azure Active Directory aplicación de Azure AD (Azure AD).
* `token_scope`: el ámbito es necesario para obtener un token. establezca el valor en https://graph.microsoft.com/.default.
* `teamGroupId`: Puede obtener el identificador de grupo de grupo del Teams de la siguiente manera:

    1. En el Teams **, seleccione Teams** en la barra de navegación de la izquierda.
    2. Selecciona el equipo donde está instalada la aplicación en el menú desplegable.
    3. Seleccione el **icono Más opciones** (&#8943;).
    4. Seleccione **Obtener vínculo al equipo**. 
    5. Copie y guarde el **valor groupId** de la cadena.

## <a name="test-added-rsc-permissions-to-a-chat-using-the-postman-app"></a>Probar los permisos RSC agregados a un chat con la aplicación Postman

Para comprobar si la carga de solicitud de API está respetando los permisos RSC, debe copiar el código de prueba [JSON de RSC para chats](test-chat-rsc-json-file.md) en el entorno local y actualizar los siguientes valores:

* `azureADAppId`: El identificador de aplicación Microsoft Azure Active Directory aplicación (Azure AD) de la aplicación.
* `azureADAppSecret`: La contraseña Microsoft Azure Active Directory aplicación de Azure AD (Azure AD).
* `token_scope`: el ámbito es necesario para obtener un token. establezca el valor en https://graph.microsoft.com/.default.
* `tenantId`: el nombre o el Microsoft Azure Active Directory de objeto (Azure AD) del espacio empresarial.
* `chatId`: Puede obtener el identificador de subproceso de chat del Teams *web* de la siguiente manera:

    1. En el Teams web, seleccione **Chat** en la barra de navegación de la izquierda.
    2. Selecciona el chat donde está instalada la aplicación en el menú desplegable.
    3. Copie la dirección URL web y guarde el identificador del subproceso de chat de la cadena.
![Identificador de subproceso de chat desde la dirección URL web.](../../assets/images/chat-thread-id.png)

### <a name="use-postman"></a>Usar Postman

1. Abre la [aplicación Postman](https://www.postman.com) .
2. Seleccione **Archivo** **FileImportImport** >  >  **para** cargar el archivo JSON actualizado desde el entorno.  
3. Seleccione la **pestaña Colecciones** . 
4. Seleccione el chevron junto **>** al **RSC** de prueba para expandir la vista de detalles y ver las solicitudes de API.

Ejecute toda la colección de permisos para cada llamada a la API. Los permisos especificados en el manifiesto de la aplicación deben ser correctos, mientras que los no especificados deben producir un error con un código de estado HTTP 403. Comprueba todos los códigos de estado de respuesta para confirmar que el comportamiento de los permisos de RSC en la aplicación cumple las expectativas.

> [!NOTE]
> Para probar llamadas API DELETE y READ específicas, agregue esos escenarios de instancia al archivo JSON.

## <a name="test-revoked-rsc-permissions-using-postman"></a>Probar permisos RSC revocados con [Postman](https://www.postman.com/)

1. Desinstale la aplicación del recurso específico.
2. Siga los pasos para chat o equipo: 
    1. [Probar los permisos RSC agregados a un equipo mediante Postman](#test-added-rsc-permissions-to-a-team-using-the-postman-app).
    2. [Prueba agregó permisos RSC a un chat con Postman](#test-added-rsc-permissions-to-a-chat-using-the-postman-app).
3. Compruebe todos los códigos de estado de respuesta para confirmar que las llamadas API específicas han **fallado con un código de estado HTTP 403**.

## <a name="see-also"></a>Vea también

* [API Graph Microsoft y Teams](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)
* [Consentimiento específico del recurso](~/graph-api/rsc/resource-specific-consent.md)

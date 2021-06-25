---
title: Probar permisos de consentimiento específicos de recursos en Teams
description: Detalles que prueban el consentimiento específico de recursos Teams con Postman
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: tutorial
keywords: autorización de teams OAuth SSO AAD rsc Postman Graph
ms.openlocfilehash: 8f5b293557ef7de9e4d551c5ae2bd7216e6e3fc0
ms.sourcegitcommit: 261058171f1e3bbc822c5bcc0e9fba5a4de68000
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/24/2021
ms.locfileid: "53111131"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a>Probar permisos de consentimiento específicos de recursos en Teams

> [!NOTE]
> El consentimiento específico de los recursos para el ámbito de chat solo está disponible en [la versión preliminar del desarrollador](../../resources/dev-preview/developer-preview-intro.md) público.

El consentimiento específico de recursos (RSC) es una integración de api de Microsoft Teams y Graph que permite a la aplicación usar puntos de conexión de API para administrar recursos específicos (ya sea equipos o chats) dentro de una organización. Para obtener más información, vea [Resource-specific consent (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).

> [!NOTE]
> Para probar los permisos de RSC, el archivo de manifiesto Teams aplicación debe incluir una clave **webApplicationInfo** rellenada con los campos siguientes:
>
> - **id:** El identificador de la aplicación de Azure AD, consulte [Registrar la aplicación en el Portal de Azure AD](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-aad-portal).
> - **resource**: Any string, see the note in [Update your Teams app manifest](resource-specific-consent.md#update-your-teams-app-manifest).
> - **permisos de aplicación:** permisos RSC para la aplicación, consulta [Permisos específicos de recursos](resource-specific-consent.md#resource-specific-permissions).

## <a name="example-for-a-team"></a>Ejemplo para un equipo
```json
"webApplicationInfo":{
      "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
      "resource":"https://AnyString",
      "applicationPermissions":[
         "Channel.Create.Group",
         "Channel.Delete.Group",
         "ChannelMessage.Read.Group",
         "ChannelSettings.Read.Group",
         "ChannelSettings.Edit.Group",
         "Member.Read.Group",
         "Owner.Read.Group",
         "TeamsApp.Read.Group",
         "TeamsTab.Read.Group",
         "TeamsTab.Create.Group",
         "TeamsTab.Edit.Group",
         "TeamsTab.Delete.Group",
         "TeamSettings.Read.Group",
         "TeamSettings.Edit.Group"
      ]
   }
```

## <a name="example-for-a-chat"></a>Ejemplo para un chat
```json
"webApplicationInfo":{
      "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
      "resource":"https://AnyString",
      "applicationPermissions":[
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
          "OnlineMeeting.ReadBasic.Chat"
      ]
   }
```

> [!IMPORTANT]
> En el manifiesto de la aplicación, solo incluye los permisos de RSC que quieras que tenga la aplicación.

>[!NOTE]
>Si la aplicación está pensada para admitir la instalación en ámbitos de equipo y chat, los permisos de equipo y chat se pueden especificar en el mismo manifiesto en `applicationPermissions` .

## <a name="test-added-rsc-permissions-to-a-team-using-the-postman-app"></a>Probar los permisos RSC agregados a un equipo mediante la aplicación Postman

Para comprobar si la carga de solicitud de API está respetando los permisos RSC, debe copiar el código de prueba JSON de [RSC](test-team-rsc-json-file.md) para el equipo en el entorno local y actualizar los siguientes valores:

* `azureADAppId`: Id. de aplicación de Azure AD de la aplicación.
* `azureADAppSecret`: la contraseña de la aplicación de Azure AD.
* `token_scope`: el ámbito es necesario para obtener un token. establezca el valor en https://graph.microsoft.com/.default .
* `teamGroupId`: Puede obtener el identificador de grupo de grupo del Teams de la siguiente manera:

    1. En el Teams, seleccione **Teams** en la barra de navegación de la izquierda.
    2. Selecciona el equipo donde está instalada la aplicación en el menú desplegable.
    3. Seleccione el **icono Más opciones** (&#8943;).
    4. Seleccione **Obtener vínculo al equipo**. 
    5. Copie y guarde el **valor groupId** de la cadena.

## <a name="test-added-rsc-permissions-to-a-chat-using-the-postman-app"></a>Probar los permisos RSC agregados a un chat con la aplicación Postman

Para comprobar si la carga de solicitud de API está respetando los permisos RSC, debe copiar el código de prueba JSON de [RSC](test-chat-rsc-json-file.md) para chats en el entorno local y actualizar los siguientes valores:

* `azureADAppId`: Id. de aplicación de Azure AD de la aplicación.
* `azureADAppSecret`: la contraseña de la aplicación de Azure AD.
* `token_scope`: el ámbito es necesario para obtener un token. establezca el valor en https://graph.microsoft.com/.default .
* `tenantId`: el nombre o el identificador de objeto de AAD del inquilino.
* `chatId`: Puede obtener el identificador de subproceso de chat del Teams *web* de la siguiente manera:

    1. En el Teams web, seleccione **Chat** en la barra de navegación de la izquierda.
    2. Selecciona el chat donde está instalada la aplicación en el menú desplegable.
    3. Copie la dirección URL web y guarde el identificador del subproceso de chat de la cadena.
![Identificador de subproceso de chat desde la dirección URL web.](../../assets/images/chat-thread-id.png)

### <a name="use-postman"></a>Usar Postman

1. Abre la [aplicación Postman.](https://www.postman.com)
2. Seleccione **Importar**  >    >  **archivo Importar archivo para** cargar el archivo JSON actualizado desde el entorno.  
3. Seleccione la **pestaña Colecciones.** 
4. Seleccione el chevron **>** junto al **RSC** de prueba para expandir la vista de detalles y ver las solicitudes de API.

Ejecute toda la colección de permisos para cada llamada a la API. Los permisos especificados en el manifiesto de la aplicación deben ser correctos, mientras que los no especificados deben producir un error con un código de estado HTTP 403. Comprueba todos los códigos de estado de respuesta para confirmar que el comportamiento de los permisos de RSC en la aplicación cumple las expectativas.

> [!NOTE]
> Para probar llamadas API DELETE y READ específicas, agregue esos escenarios de instancia al archivo JSON.

## <a name="test-revoked-rsc-permissions-using-postman"></a>Probar permisos RSC revocados con [Postman](https://www.postman.com/)

1. Desinstale la aplicación del recurso específico.
2. Siga los pasos para chat o equipo: 
    1. [Probar los permisos RSC agregados a un equipo mediante Postman](#test-added-rsc-permissions-to-a-team-using-the-postman-app).
    2. [Probar los permisos RSC agregados a un chat con Postman](#test-added-rsc-permissions-to-a-chat-using-the-postman-app).
3. Compruebe todos los códigos de estado de respuesta para confirmar que las llamadas API específicas han fallado con un código de estado **HTTP 403**.

## <a name="see-also"></a>Vea también

[API Graph Microsoft y Teams](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)


---
title: Probar permisos de consentimiento específicos de recursos en Teams
description: Detalles que prueban el consentimiento específico de recursos en Teams con Postman
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: tutorial
keywords: Autorización de teams OAuth SSO AAD rsc Postman Graph
ms.openlocfilehash: 0d3d1c895c77bb417a9fdd84e319103485aa8944
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634715"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a>Probar permisos de consentimiento específicos de recursos en Teams

El consentimiento específico de los recursos (RSC) es una integración de Microsoft Teams y la API de Graph que permite a la aplicación usar puntos de conexión de API para administrar equipos específicos dentro de una organización. Para obtener más información, vea [Resource-specific consent (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).

> [!NOTE]
> Para probar los permisos de RSC, el archivo de manifiesto de la aplicación teams debe incluir una clave **webApplicationInfo** rellenada con los campos siguientes:
>
> - **id:** El identificador de la aplicación de Azure AD, consulte [Registrar la aplicación en el Portal de Azure AD](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).
> - **resource**: Any string, see the note in  [Update your Teams app manifest](resource-specific-consent.md#update-your-teams-app-manifest)
> - **permisos de aplicación:** permisos RSC para la aplicación, consulta [Permisos específicos de recursos](resource-specific-consent.md#resource-specific-permissions).

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

> [!IMPORTANT]
> En el manifiesto de la aplicación, solo incluye los permisos de RSC que quieras que tenga la aplicación.

## <a name="test-added-rsc-permissions-using-the-postman-app"></a>Probar permisos RSC agregados mediante la aplicación Postman

Para comprobar si la carga de solicitud de API está respetando los permisos RSC, debe copiar el código de prueba JSON de [RSC](test-rsc-json-file.md) en el entorno local y actualizar los siguientes valores:

* `azureADAppId`: Id. de aplicación de Azure AD de la aplicación
* `azureADAppSecret`: El secreto de la aplicación de Azure AD (contraseña)
* `token_scope`: El ámbito es necesario para obtener un token: establezca el valor en https://graph.microsoft.com/.default
* `teamGroupId`: Puede obtener el identificador de grupo de grupo del cliente de Teams de la siguiente manera:

  > [!div class="checklist"]
  >
  > * En el cliente de Teams, seleccione **Teams en** la barra de navegación de la izquierda.
  > * Selecciona el equipo donde está instalada la aplicación en el menú desplegable.
  > * Seleccione el **icono Más opciones** (&#8943;)
  > * Seleccionar **Obtener vínculo al equipo** 
  > * Copie y guarde el **valor groupId** de la cadena.

### <a name="use-postman"></a>Usar Postman

1. Abre la [aplicación Postman.](https://www.postman.com)
2. Seleccione **Importar**  >    >  **archivo Importar archivo para** cargar el archivo JSON actualizado desde el entorno.  
3. Seleccione la **pestaña Colecciones.** 
4. Seleccione el chevron **>** junto al **RSC** de prueba para expandir la vista de detalles y ver las solicitudes de API.

Ejecute toda la colección de permisos para cada llamada a la API. Los permisos especificados en el manifiesto de la aplicación deben ser correctos, mientras que los no especificados deben producir un error con un código de estado HTTP 403. Comprueba todos los códigos de estado de respuesta para confirmar que el comportamiento de los permisos de RSC en la aplicación cumple las expectativas.

> [!NOTE]
> Para probar llamadas API DELETE y READ específicas, agregue esos escenarios de instancia al archivo JSON.

## <a name="test-revoked-rsc-permissions-using-postman"></a>Probar permisos RSC revocados con [Postman](https://www.postman.com/)

1. Desinstale la aplicación del equipo específico.
2. Siga los pasos para probar los permisos [RSC agregados mediante Postman](#test-added-rsc-permissions-using-the-postman-app).
3. Compruebe todos los códigos de estado de respuesta para confirmar que las llamadas API específicas, correctamente, han fallado con un código de estado **HTTP 403**.

## <a name="see-also"></a>Vea también

> [!div class="nextstepaction"]
> [API de Microsoft Graph y Teams](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)


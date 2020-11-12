---
title: Probar el consentimiento específico de los recursos en Microsoft Teams
description: Detalles de prueba del consentimiento específico del recurso en Microsoft Teams con Postman
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: tutorial
keywords: Gráfico de autorización de equipo de OAuth de OAuth SSO de AAD de Microsoft Teams
ms.openlocfilehash: f780829100e47ad04a588106e83843876b8d7932
ms.sourcegitcommit: f6029c8ff0c5315613a3efcd86777aa4cede39e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/11/2020
ms.locfileid: "48995012"
---
# <a name="test-resource-specific-consent-permissions--in-teams"></a>Probar permisos de consentimiento específicos de recursos en Microsoft Teams

El consentimiento específico de recursos (RSC) es una integración de Microsoft Teams y Graph API que permite a su aplicación usar puntos de conexión de API para administrar equipos específicos dentro de una organización. *Consulte*[autorización específica de recursos (RSC): API de Microsoft Teams Graph](resource-specific-consent.md).  

> [!NOTE]
>Para probar los permisos RSC, el archivo de manifiesto de la aplicación de Microsoft Teams debe incluir una clave **webApplicationInfo** rellenada con los siguientes campos:
>
> - **ID**  : el identificador de la aplicación de Azure ad, *vea* [registrar la aplicación en el portal de Azure ad](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).
> - **recurso**  : cualquier cadena, *vea* la nota en  [actualizar el manifiesto de la aplicación Teams](resource-specific-consent.md#update-your-teams-app-manifest)
> - **permisos de aplicación** : permisos RSC para la aplicación, *vea* [permisos específicos de recursos](resource-specific-consent.md#resource-specific-permissions).

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

>[!IMPORTANT]
>En el manifiesto de la aplicación, incluya solo los permisos RSC que desea que tenga la aplicación.

## <a name="test-added-rsc-permissions-using-the-postman-app"></a>Probar los permisos RSC agregados mediante la aplicación Postman

Para comprobar si la carga de solicitud de API respeta los permisos RSC, deberá copiar el [código de prueba JSON de RSC](test-rsc-json-file.md) en su entorno local y actualizar los siguientes valores:

1. `azureADAppId`  -identificador de la aplicación de Azure AD de la aplicación.
1. `azureADAppSecret`  : su secreto de la aplicación de Azure AD (contraseña)
1. `token_scope`  — el ámbito es obligatorio para obtener un token: establezca el valor en https://graph.microsoft.com/.default
1. `teamGroupId` puede obtener el identificador del grupo de equipos desde el cliente de Microsoft Teams de la siguiente manera:

> [!div class="checklist"]
>
> * En el cliente de Microsoft Teams, seleccione **Teams** en la barra de navegación de la parte izquierda.
> * Seleccione el equipo en el que se instalará la aplicación desde el menú desplegable.
> * Seleccione el icono **más opciones** (&#8943;)
> * Seleccione **obtener vínculo a equipo** 
> * Copie y guarde el valor **GROUPID** de la cadena.

### <a name="using-postman"></a>Uso de Postman

> [!div class="checklist"]
>
> * Abra la aplicación [Postman](https://www.postman.com) .
> * Seleccione **archivo**  =>  **importar**  =>  **Importar archivo** para cargar el archivo JSON actualizado desde su entorno.  
> * Seleccione la pestaña **colecciones** . 
> * Seleccione la comilla angular (>) junto a la **prueba RSC** para expandir la vista de detalles y ver las solicitudes de la API.

Ejecutar toda la colección de permisos para cada llamada a la API. Los permisos especificados en el manifiesto de la aplicación deben realizarse correctamente, mientras que los que no se hayan especificado deben generar un error con un código de Estado HTTP 403. Compruebe todos los códigos de estado de respuesta para confirmar que el comportamiento de los permisos RSC en la aplicación cumple las expectativas.

>[!NOTE]
>Para probar las llamadas específicas de eliminación y lectura de la API, agregue los escenarios de instancia al archivo JSON.

## <a name="test--revoked-rsc-permissions-using-postman"></a>Probar los permisos RSC revocados mediante [Postman](https://www.postman.com/)

> [!div class="checklist"]
>
> * Desinstalar la aplicación del equipo específico.
> * Siga los pasos anteriores para [probar los permisos RSC agregados mediante Postman](#test-added-rsc-permissions-using-the-postman-app).
> * Compruebe todos los códigos de estado de respuesta para confirmar que se han producido errores en las llamadas API específicas que han tenido éxito con un código de Estado HTTP 403.

> [!div class="nextstepaction"]
>
> [Obtenga más información sobre la API de Graph y Microsoft Teams](/graph/api/resources/teams-api-overview?view=graph-rest-1.0)

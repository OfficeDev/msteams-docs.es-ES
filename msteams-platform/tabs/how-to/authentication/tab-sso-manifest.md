---
title: Actualización del manifiesto para habilitar el inicio de sesión único para las pestañas
description: Actualice el manifiesto de Teams para habilitar el inicio de sesión único (SSO) para pestañas y transferirlo localmente al cliente de Teams para probar la autenticación sso.
ms.topic: how-to
ms.localizationpriority: high
keywords: pestañas de autenticación de teams del Graph API de Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: bd5b7257a131a11e861b94221c533d8364b6bb54
ms.sourcegitcommit: 176bbca74ba46b7ac298899d19a2d75087fb37c1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/04/2022
ms.locfileid: "68376588"
---
# <a name="update-manifest-for-sso-and-preview-app"></a>Actualizar el manifiesto para el SSO y versión preliminar de la aplicación

Antes de actualizar el manifiesto de aplicación de Teams, asegúrese de que ha configurado el código para habilitar el inicio de sesión único en la aplicación de pestañas.

> [!div class="nextstepaction"]
> [Configuración del código](tab-sso-code.md)

Ha registrado la aplicación de pestaña en Azure AD y ha obtenido un identificador de la aplicación. También ha configurado el código para llamar a `getAuthToken()` y controlar el token de acceso. Ahora debe actualizar el manifiesto de la aplicación de Teams para habilitar el inicio de sesión único de la aplicación de pestañas. El manifiesto de la aplicación de Teams describe cómo se integra la aplicación en Teams.

## <a name="webapplicationinfo-property"></a>propiedad webApplicationInfo

Configure la propiedad `webApplicationInfo` en el archivo de manifiesto de la aplicación de Teams. Esta propiedad permite que el inicio de sesión único de la aplicación ayude a los usuarios de esta a acceder sin problemas a la aplicación de pestañas.

&nbsp;&nbsp;:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-manifest.png" alt-text="Configuración del manifiesto de la aplicación de Teams":::

`webApplicationInfo` tiene dos elementos: `id` y `resource`.

| Elemento | Descripción |
| --- | --- |
| id | Escriba el identificador de aplicación (GUID) que creó en Azure AD. |
| resource | Escriba el URI del subdominio de la aplicación y el URI del identificador de aplicación que creó en Azure AD con el ámbito. Puede copiarlo desde la sección **Exponer una API** de **Azure AD** > . |

> [!NOTE]
> Debe usar la versión 1.5 del manifiesto o una posterior para implementar la propiedad `webApplicationInfo`.

El URI del identificador de aplicación que registró en Azure AD se configura con el ámbito de la API que ha expuesto. Configure el URI de subdominio de la aplicación en `resource` para asegurarse de que la solicitud de autenticación que usa `getAuthToken()` procede del dominio especificado en el manifiesto de aplicación de Teams.

Para obtener más información, consulte [webApplicationInfo](../../../resources/schema/manifest-schema.md#webapplicationinfo).

## <a name="to-configure-teams-app-manifest"></a>Para configurar el manifiesto de la aplicación de Teams

1. Abra el proyecto de la aplicación de pestañas.
2. Abra la carpeta del manifiesto.

  > [!NOTE]
  >
  > - La carpeta del manifiesto debe estar en la raíz del proyecto. Para obtener más información, consulte [Crear un paquete de la aplicación Microsoft Teams](../../../concepts/build-and-test/apps-package.md).
  > - Para obtener más información sobre cómo crear un archivo manifest.json, consulte [Referencia: esquema de manifiesto para Microsoft Teams](../../../resources/schema/manifest-schema.md).

1. Abrir el archivo manifest.json.
1. Anexe el siguiente fragmento de código al archivo de manifiesto para agregar la nueva propiedad:

    ```json
    "webApplicationInfo": {
    "id": "{Azure AD AppId}",
    "resource": "api://{Subdomain}.example.com/{Azure AD AppId}"
    }
    ```

    where,
    - {Azure AD AppId} es el identificador de aplicación que creó al registrar la aplicación en Azure AD. Es el GUID.
    - {{Subdomain}.app ID URI} es el URI de identificador de la aplicación que registró al crear el ámbito en Azure AD.

4. Actualice el identificador de aplicación de Azure AD en la propiedad **id**.
5. Actualice la URL del subdominio en las propiedades siguientes:
   1. `contentUrl`
   2. `configurationUrl`
   3. `validDomains`
6. Guarde el archivo de manifiesto de la aplicación de Teams.

<br>
<details>
<summary>Este es un ejemplo del manifiesto de aplicación después de actualizarlo</summary>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
  "manifestVersion": "1.11",
  "version": "1.0.0",
  "id": "bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c",
  "developer": {
    "name": "Microsoft",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.microsoft.com/privacy",
    "termsOfUseUrl": "https://www.microsoft.com/termsofuse"
  },
  "name": {
    "short": "Teams Auth SSO",
    "full": "Teams Auth SSO"
  },
  "description": {
    "short": "Teams Auth SSO app",
    "full": "The Teams Auth SSO app"
  },
  "icons": {
    "outline": "outline.png",
    "color": "color.png"
  },
  "accentColor": "#60A18E",
  "staticTabs": [
    {
      "entityId": "auth",
      "name": "Auth",
      "contentUrl": "https://contoso.com/Home/Index",
      "scopes": [ "personal" ]
    }
  ],
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/Home/Configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "team"
      ]
    }
  ],
  "permissions": [ "identity", "messageTeamMembers" ],
  "validDomains": [
    "contoso.com"
  ],
  "webApplicationInfo": {
    "id": "bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c",
    "resource": "api://contoso.com/bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c"
  }
}
```

</details>

> [!NOTE]
> Durante la depuración, puede usar ngrok para probar la aplicación en Azure AD. En ese caso, debe reemplazar el subdominio en `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` por la URL de ngrok. Tendrá que actualizar la URL cada vez que cambie el subdominio ngrok. Por ejemplo, api://23c3-103-50-148-128.ngrok.io/bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c.

## <a name="sideload-and-preview-in-teams"></a>Transferir localmente y vista previa en Teams

Ha configurado la aplicación de pestañas para habilitar el inicio de sesión único en Azure AD, en el código de la aplicación y en el archivo de manifiesto de Teams. Ahora puede transferir localmente la aplicación de pestaña en Teams y obtener una vista previa de ella en el entorno de Teams.

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-flow.png" alt-text="Aplicación de inicio de sesión único":::

Para obtener una vista previa de la aplicación de pestañas en Teams:

1. Cree un paquete de aplicación de Microsoft Teams

   El paquete de aplicación es un archivo ZIP que contiene un archivo de manifiesto e iconos de aplicación.

1. Abra Teams.

1. Seleccione **Aplicaciones** > **Administrar las aplicaciones** > **Cargar una aplicación**.

    Aparecen las opciones para cargar una aplicación.

1. Seleccione **Cargar una aplicación personalizada** para transferir localmente la aplicación de pestañas a Teams.

1. Seleccione el archivo ZIP del paquete de aplicación y, a continuación, seleccione **Agregar**.

    La aplicación de pestañas se carga de forma local y el cuadro de diálogo aparece para informarle de los permisos adicionales que pueden ser necesarios.

1. Seleccione **Continuar**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/teams-sso-consent.png" alt-text="Cuadro de diálogo de Teams que informa sobre los permisos adicionales necesarios":::

    Aparece el cuadro de diálogo de consentimiento de Azure AD.

1. Seleccione **Aceptar** para dar su consentimiento para los ámbitos de open-id.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/aad-sso-consent.png" alt-text="Cuadro de diálogo de consentimiento de Azure AD":::

    Teams abre la aplicación de pestañas y puede usarla.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/teams-sso-app.png" alt-text="Ejemplo de aplicación de pestañas de Teams con SSO habilitado":::

    ¡Enhorabuena! Ha habilitado el inicio de sesión único para la aplicación de pestañas.

## <a name="see-also"></a>Recursos adicionales

- [Esquema de manifiesto para Microsoft Teams](../../../resources/schema/manifest-schema.md)
- [Formato de esquema de manifiesto](https://developer.microsoft.com/json-schemas/teams/v1.12/MicrosoftTeams.schema.json)
- [Crear un paquete de aplicación de Microsoft Teams](../../../concepts/build-and-test/apps-package.md)

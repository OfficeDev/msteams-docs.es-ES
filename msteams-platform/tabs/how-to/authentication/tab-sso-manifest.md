---
title: Actualización del manifiesto para habilitar el inicio de sesión único para pestañas
description: Describe la actualización del manifiesto para habilitar el inicio de sesión único para pestañas
ms.topic: how-to
ms.localizationpriority: medium
keywords: pestañas de autenticación de teams Microsoft Azure Active Directory (Azure AD) Graph API
ms.openlocfilehash: 90a1ac781ef521f4b236bdf26f50d44533fa815a
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558740"
---
# <a name="update-manifest-for-sso-and-preview-app"></a>Actualización del manifiesto para el inicio de sesión único y la aplicación en versión preliminar

Antes de actualizar el manifiesto de aplicación de Teams, asegúrese de que ha configurado el código para habilitar el inicio de sesión único en la aplicación de pestaña.

> [!div class="nextstepaction"]
> [Configuración del código](tab-sso-code.md)

Ha registrado la aplicación de pestaña en Azure AD y ha obtenido un identificador de aplicación. También ha configurado el código para llamar `getAuthToken()` al token de acceso y controlarlo. Ahora, debe actualizar el manifiesto de aplicación de Teams para habilitar el inicio de sesión único para la aplicación de pestaña. El manifiesto de aplicación de Teams describe cómo se integra una aplicación en Teams.

## <a name="webapplicationinfo-property"></a>webApplicationInfo (propiedad)

Configure la `webApplicationInfo` propiedad en el archivo de manifiesto de aplicación de Teams. Esta propiedad permite que el inicio de sesión único de la aplicación ayude a los usuarios de la aplicación a acceder a la aplicación de pestaña sin problemas.

&nbsp;&nbsp;:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-manifest.png" alt-text="Configuración del manifiesto de aplicación de Teams":::

`webApplicationInfo` tiene dos elementos, `id` y `resource`.

| Elemento | Descripción |
| --- | --- |
| id | Escriba el identificador de aplicación (GUID) que creó en Azure AD. |
| resource | Escriba el URI del subdominio de la aplicación y el URI del identificador de aplicación que creó en Azure AD al crear el ámbito. Puede copiarlo desde la sección **Exponer una API** de **Azure AD** > . |

> [!NOTE]
> Use la versión de manifiesto 1.5 o posterior para implementar la `webApplicationInfo` propiedad .

El URI del identificador de aplicación que registró en Azure AD se configura con el ámbito de la API que ha expuesto. Configure el URI de subdominio de la aplicación en `resource` para asegurarse de que la solicitud de autenticación que usa `getAuthToken()` procede del dominio especificado en el manifiesto de aplicación de Teams.

Para obtener más información, vea [webApplicationInfo](../../../resources/schema/manifest-schema.md#webapplicationinfo).

## <a name="to-configure-teams-app-manifest"></a>Para configurar el manifiesto de aplicación de Teams

1. Abra el proyecto de aplicación de pestaña.
2. Abra la carpeta del manifiesto.

  > [!NOTE]
  >
  > - La carpeta de manifiesto debe estar en la raíz del proyecto. Para obtener más información, consulte [Creación de un paquete de aplicación de Microsoft Teams](../../../concepts/build-and-test/apps-package.md).
  > - Para obtener más información sobre cómo crear un archivo manifest.json, consulte [Referencia: Esquema de manifiesto para Microsoft Teams](../../../resources/schema/manifest-schema.md).

1. Abra el archivo manifest.json.
1. Anexe el siguiente fragmento de código al archivo de manifiesto para agregar la nueva propiedad:

    ```json
    "webApplicationInfo": {
    "id": "{Azure AD AppId}",
    "resource": "api://{Subdomain}.example.com/{Azure AD AppId}"
    }
    ```

    Dónde
    - {Azure AD AppId} es el identificador de aplicación que creó al registrar la aplicación en Azure AD. Es el GUID.
    - {{Subdomain}.app ID URI} es el URI de identificador de aplicación que registró al crear el ámbito en Azure AD.

4. Actualice el identificador de aplicación de Azure AD en la propiedad **id** .
5. Actualice la dirección URL del subdominio en las propiedades siguientes:
   1. `contentUrl`
   2. `configurationUrl`
   3. `validDomains`
6. Guarde el archivo de manifiesto de aplicación de Teams.

<br>
<details>
<summary>Este es un ejemplo de manifiesto de aplicación después de actualizarlo</summary>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
  "manifestVersion": "1.11",
  "version": "1.0.0",
  "id": "bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c",
  "packageName": "com.contoso.teamsauthsso",
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
> Durante la depuración, puede usar ngrok para probar la aplicación en Azure AD. En ese caso, debe reemplazar el subdominio en `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` por la dirección URL de ngrok. Tendrá que actualizar la dirección URL cada vez que cambie el subdominio ngrok Por ejemplo, api://23c3-103-50-148-128.ngrok.io/bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c.

## <a name="sideload-and-preview-in-teams"></a>Instalación local y versión preliminar en Teams

Ha configurado la aplicación de pestaña para habilitar el inicio de sesión único en Azure AD, en el código de la aplicación y en el archivo de manifiesto de Teams. Ahora puede transferir localmente la aplicación de pestaña en Teams y obtener una vista previa de ella en el entorno de Teams.

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-flow.png" alt-text="Aplicación sso":::

Para obtener una vista previa de la aplicación de pestaña en Teams:

1. Cree un paquete de aplicación.

   El paquete de la aplicación es un archivo ZIP que contiene el archivo de manifiesto de la aplicación y los iconos de la aplicación.

1. Abra Teams.

1. Seleccione **Aplicaciones** > **Administrar las aplicaciones** > **Cargar una aplicación**.

    Aparecen las opciones para cargar una aplicación.

1. Seleccione **Cargar una aplicación personalizada** para transferir localmente la aplicación de pestaña a Teams.

1. Seleccione el archivo zip del paquete de aplicación y, a continuación, seleccione **Agregar**.

    La aplicación de pestaña se carga de forma local y el cuadro de diálogo aparece para informarle de los permisos adicionales que pueden ser necesarios.

1. Seleccione **Continuar**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/teams-sso-consent.png" alt-text="Cuadro de diálogo de Teams que informa sobre los permisos adicionales necesarios":::

    Aparece el cuadro de diálogo de consentimiento de Azure AD.

1. Seleccione **Aceptar** para dar su consentimiento para los ámbitos de id. abierto.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/aad-sso-consent.png" alt-text="Cuadro de diálogo de consentimiento de Azure AD":::

    Teams abre la aplicación de pestaña y puede usarla.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/teams-sso-app.png" alt-text="Ejemplo de aplicación de pestaña de Teams con sso habilitado":::

    ¡Enhorabuena! Ha habilitado el inicio de sesión único para la aplicación de pestaña.

## <a name="see-also"></a>Vea también

- [Esquema de manifiesto para Microsoft Teams](../../../resources/schema/manifest-schema.md)
- [Formato de esquema de manifiesto](https://developer.microsoft.com/json-schemas/teams/v1.12/MicrosoftTeams.schema.json)
- [Crear un paquete de aplicación de Microsoft Teams](../../../concepts/build-and-test/apps-package.md)

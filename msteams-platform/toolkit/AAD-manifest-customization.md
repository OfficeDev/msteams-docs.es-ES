---
title: Edición del manifiesto de Azure Active Directory en el kit de herramientas de Teams
author: zyxiaoyuer
description: Describe la administración de una aplicación de Azure Active Directory en el kit de herramientas de Teams
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/20/2022
ms.openlocfilehash: 0df9cc75b6a9775f9369b6a3bf8b95c35941207b
ms.sourcegitcommit: 637b8f93b103297b1ff9f1af181680fca6f4499d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2022
ms.locfileid: "68499324"
---
# <a name="edit-azure-ad-manifest"></a>Edición del manifiesto de Azure AD

El [manifiesto de Azure Active Directory (Azure AD)](/azure/active-directory/develop/reference-app-manifest) contiene definiciones de todos los atributos de un objeto de aplicación de Azure AD en el Plataforma de identidad de Microsoft.

Teams Toolkit ahora administra la aplicación de Azure AD con el archivo de manifiesto como el origen de la verdad durante el ciclo de vida de desarrollo de aplicaciones de Teams.

En esta sección se describen estos temas:

* [Personalización de la plantilla de manifiesto de Azure AD](#customize-azure-ad-manifest-template)
* [Marcadores de posición de plantilla de manifiesto de Azure AD](#azure-ad-manifest-template-placeholders)
* [Creación y vista previa del manifiesto de Azure AD con la lente de código](#author-and-preview-azure-ad-manifest-with-code-lens)
* [Implementación de cambios de la aplicación de Azure AD para el entorno local](#deploy-azure-ad-application-changes-for-local-environment)
* [Implementación de cambios de aplicaciones de Azure AD para un entorno remoto](#deploy-azure-ad-application-changes-for-remote-environment)
* [Visualización de la aplicación de Azure AD en el Azure Portal](#view-azure-ad-application-on-the-azure-portal)
* [Uso de una aplicación de Azure AD existente](#use-an-existing-azure-ad-application)
* [Ciclo de vida de desarrollo de aplicaciones de Azure AD en Teams](#azure-ad-application-in-teams-application-development-lifecycle)

## <a name="customize-azure-ad-manifest-template"></a>Personalización de la plantilla de manifiesto de Azure AD

Puede personalizar la plantilla de manifiesto de Azure AD para actualizar la aplicación de Azure AD.

1. Abra `aad.template.json` en el proyecto.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add template.png" alt-text="template":::

2. Actualice la plantilla directamente o [haga referencia a los valores de otro archivo](https://github.com/OfficeDev/TeamsFx/wiki/Manage-AAD-application-in-Teams-Toolkit#Placeholders-in-AAD-manifest-template). Puede ver varios escenarios de personalización aquí:
  
   * [Agregar un permiso de aplicación](#add-an-application-permission)
   * [Autenticación previa de una aplicación cliente](#preauthorize-a-client-application)
   * [Actualización de la dirección URL de redireccionamiento para la respuesta de autenticación](#update-redirect-url-for-authentication-response)

3. [Implemente los cambios de la aplicación de Azure AD para el entorno local](#deploy-azure-ad-application-changes-for-local-environment).
  
4. [Implemente los cambios de la aplicación de Azure AD para el entorno remoto](#deploy-azure-ad-application-changes-for-remote-environment).

### <a name="add-an-application-permission"></a>Agregar un permiso de aplicación

Si la aplicación de Teams requiere más permisos para llamar a la API con permisos adicionales, debe actualizar `requiredResourceAccess` la propiedad en la plantilla de manifiesto de Azure AD. Puede ver el ejemplo siguiente para esta propiedad:

```JSON

   "requiredResourceAccess": [
    {
        "resourceAppId": "Microsoft Graph",
        "resourceAccess": [
            {
                "id": "User.Read", // For Microsoft Graph API, you can also use uuid for permission id
                "type": "Scope" // Scope is for delegated permission
            },
            {
                "id": "User.Export.All",
                "type": "Role" // Role is for application permission
            }
        ]
    },
    {
        "resourceAppId": "Office 365 SharePoint Online",
        "resourceAccess": [
            {
                "id": "AllSites.Read",
                "type": "Scope"
            }
        ]
    }
]
```

* `resourceAppId` se usa para distintas API. Para `Microsoft Graph` y `Office 365` `SharePoint Online`, escriba el nombre directamente en lugar de UUID y, para otras API, use UUID.

* `resourceAccess.id` se usa para permisos diferentes. Para `Microsoft Graph` y `Office 365 SharePoint Online`, escriba el nombre del permiso directamente en lugar de UUID y, para otras API, use UUID.

* `resourceAccess.type` se usa para el permiso delegado o el permiso de aplicación. `Scope` significa permiso delegado y `Role` significa permiso de aplicación.

### <a name="preauthorize-a-client-application"></a>Autenticación previa de una aplicación cliente

Puede usar `preAuthorizedApplications` la propiedad para autorizar a una aplicación cliente para indicar que la API confía en la aplicación. Los usuarios no dan su consentimiento cuando el cliente la llama a la API expuesta. Puede ver el ejemplo siguiente para esta propiedad:

```JSON

    "preAuthorizedApplications": [
        {
            "appId": "1fec8e78-bce4-4aaf-ab1b-5451cc387264",
            "permissionIds": [
                "{{state.fx-resource-aad-app-for-teams.oauth2PermissionScopeId}}"
            ]
        }
        ...
    ]
```

`preAuthorizedApplications.appId` se usa para la aplicación que desea autorizar. Si no conoce el identificador de la aplicación y solo conoce el nombre de la aplicación, siga estos pasos para buscar el identificador de la aplicación:

1. Vaya a [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) y abra **Registros de aplicaciones**.

1. Seleccione **Todas las aplicaciones** y busque el nombre de la aplicación.

1. Seleccione el nombre de la aplicación y obtenga el identificador de la aplicación en la página de información general.

### <a name="update-redirect-url-for-authentication-response"></a>Actualización de la dirección URL de redireccionamiento para la respuesta de autenticación

  Las direcciones URL de redireccionamiento se usan al devolver respuestas de autenticación como tokens después de la autenticación correcta. Puede personalizar las direcciones URL de redireccionamiento mediante la propiedad `replyUrlsWithType`. Por ejemplo, para agregar `https://www.examples.com/auth-end.html` como dirección URL de redireccionamiento, puede agregarla como el ejemplo siguiente:

``` JSON
"replyUrlsWithType": [
    ...
    {
        "url": "https://www.examples.com/auth-end.html",
        "type": "Spa"
    }
]
```

## <a name="azure-ad-manifest-template-placeholders"></a>Marcadores de posición de plantilla de manifiesto de Azure AD

El archivo de manifiesto de Azure AD contiene argumentos de marcador de posición con {{...}} instrucciones que se reemplazan durante la compilación para diferentes entornos. Puede crear referencias al archivo de configuración, el archivo de estado y las variables de entorno con los argumentos de marcador de posición.

### <a name="reference-state-file-values-in-azure-ad-manifest-template"></a>Referencia de valores de archivo de estado en la plantilla de manifiesto de Azure AD

El archivo de estado se encuentra en `.fx\states\state.xxx.json` (xxx representa un entorno diferente). En el ejemplo siguiente se muestra el archivo de estado típico:

``` JSON
{
    "solution": {
        "teamsAppTenantId": "uuid",
        ...
    },
    "fx-resource-aad-app-for-teams": {
        "applicationIdUris": "api://xxx.com/uuid",
        ...
    }
    ...
}
```

Puede usar este argumento de marcador de posición en el manifiesto de Azure AD: `{{state.fx-resource-aad-app-for-teams.applicationIdUris}}` para señalar `applicationIdUris` el valor de la `fx-resource-aad-app-for-teams` propiedad .

### <a name="reference-config-file-values-in-azure-ad-manifest-template"></a>Referencia de valores de archivo de configuración en la plantilla de manifiesto de Azure AD

El archivo de configuración se encuentra en `.fx\configs\config.xxx.json` (xxx representa un entorno diferente). En el ejemplo siguiente se muestra el archivo de configuración:

``` JSON
{
  "$schema": "https://aka.ms/teamsfx-env-config-schema",
  "description": "description.",
  "manifest": {
    "appName": {
      "short": "app",
      "full": "Full name for app"
    }
  }
}
```

Puede usar el argumento de marcador de posición en el manifiesto de Azure AD: `{{config.manifest.appName.short}}` para hacer referencia `short` al valor.

### <a name="reference-environment-variable-in-azure-ad-manifest-template"></a>Variable de entorno de referencia en la plantilla de manifiesto de Azure AD

En ocasiones, no quiere codificar de forma rígida los valores de la plantilla de manifiesto de Azure AD. Por ejemplo, cuando el valor es un secreto. El archivo de plantilla de manifiesto de Azure AD admite valores de variables de entorno de referencia. Puede usar la sintaxis `{{env.YOUR_ENV_VARIABLE_NAME}}` en los valores de parámetro para indicar a las herramientas que resuelvan la variable de entorno actual del valor.

## <a name="author-and-preview-azure-ad-manifest-with-code-lens"></a>Creación y vista previa del manifiesto de Azure AD con la lente de código

El archivo de plantilla de manifiesto de Azure AD tiene la lente de código para revisar y editar.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/preview view.png" alt-text="vista previa":::

### <a name="azure-ad-manifest-template-file"></a>Archivo de plantilla de manifiesto de Azure AD

Hay una lente de código de vista previa al principio del archivo de plantilla de manifiesto de Azure AD. Seleccione el objetivo de código para generar un manifiesto de Azure AD en función del entorno seleccionado.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/add codelens.png" alt-text="addcodelens":::

### <a name="placeholder-argument-code-lens"></a>Lente de código de argumento de marcador de posición

La lente de código de argumento de marcador de posición le ayuda a examinar rápidamente los valores del entorno de depuración y desarrollo local. Si el mouse mantiene el puntero sobre el argumento de marcador de posición, muestra el cuadro de información sobre herramientas para los valores de todo el entorno.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/add arguments.png" alt-text="addarguments":::

### <a name="required-resource-access-code-lens"></a>Lente de código de acceso a recursos requerida

Es diferente del esquema de manifiesto oficial de [Azure AD](/azure/active-directory/develop/reference-app-manifest) que `resourceAppId` y `resourceAccess` el identificador de `requiredResourceAccess` la propiedad solo admiten UUID. La plantilla de manifiesto de Azure AD en Teams Toolkit también admite cadenas legibles para el usuario y `Microsoft Graph` `Office 365 SharePoint Online` permisos. Si escribe UUID, code lens muestra cadenas legibles por el usuario; de lo contrario, muestra UUID.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/add resource.png" alt-text="addresource":::

### <a name="pre-authorized-applications-code-lens"></a>Lente de código de aplicaciones previamente autorizadas

La lente de código muestra el nombre de la aplicación para el identificador de aplicación previamente autorizado para la `preAuthorizedApplications` propiedad .

## <a name="deploy-azure-ad-application-changes-for-local-environment"></a>Implementación de cambios de la aplicación de Azure AD para el entorno local

1. Seleccione `Preview` la lente de código en `aad.template.json`.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy1.png" alt-text="deploy1":::

2. Seleccione **entorno local** .
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy2.png" alt-text="deploy2":::

3. Seleccione `Deploy Azure AD Manifest` la lente de código en `aad.local.json`.

     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy3.png" alt-text="deploy3":::

4. Se implementan los cambios de la aplicación de Azure AD que se usa en el entorno local.
  
## <a name="deploy-azure-ad-application-changes-for-remote-environment"></a>Implementación de cambios de aplicaciones de Azure AD para un entorno remoto

1. Abra la paleta de comandos y seleccione: `Teams: Deploy Azure Active Directory application manifest`.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy4.png" alt-text="deploy4":::

2. También puede hacer clic con el `aad.template.json` botón derecho en y seleccionar `Deploy Azure Active Directory application manifest` en el menú contextual.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy5.png" alt-text="deploy5":::

## <a name="view-azure-ad-application-on-the-azure-portal"></a>Visualización de la aplicación de Azure AD en el Azure Portal

1. Copie el identificador de cliente de aplicación de Azure AD del `state.xxx.json` archivo () de la `fx-resource-aad-app-for-teams` propiedad .
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add view1.png" alt-text="view1":::

   > [!NOTE]
   > xxx en el identificador de cliente indica el nombre del entorno donde ha implementado la aplicación de Azure AD.

2. Vaya a [Azure Portal](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) e inicie sesión en la cuenta de Microsoft 365.
  
   > [!NOTE]
   > Asegúrese de que las credenciales de inicio de sesión de la aplicación Teams y la cuenta de M365 son las mismas.

3. Abra [la página Registros](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) de aplicaciones y busque en la aplicación de Azure AD el identificador de cliente que copió antes.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add view2.png" alt-text="view2":::

4. Seleccione la aplicación de Azure AD en el resultado de la búsqueda para ver la información detallada.
  
5. En la página de información de la aplicación de Azure AD, seleccione el menú para ver el `Manifest` manifiesto de esta aplicación. El esquema del manifiesto es el mismo que el del `aad.template.json` archivo. Para obtener más información sobre el manifiesto, consulte [Manifiesto de aplicación de Azure Active Directory](/azure/active-directory/develop/reference-app-manifest).
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add view3.png" alt-text="view3":::

6. Puede seleccionar **Otro menú** para ver o configurar la aplicación de Azure AD a través del portal.
  
## <a name="use-an-existing-azure-ad-application"></a>Uso de una aplicación de Azure AD existente

Puede usar la aplicación de Azure AD existente para el proyecto de Teams. Para obtener más información, consulte [Uso de una aplicación de Azure AD existente para la aplicación de Teams](https://github.com/OfficeDev/TeamsFx/wiki/Customize-provision-behaviors#use-an-existing-aad-app-for-your-teams-app).

## <a name="azure-ad-application-in-teams-application-development-lifecycle"></a>Ciclo de vida de desarrollo de aplicaciones de Azure AD en Teams

Debe interactuar con la aplicación de Azure AD durante varias fases del ciclo de vida de desarrollo de aplicaciones de Teams.

1. **Para crear un proyecto**

      Puede crear un proyecto con El kit de herramientas de Teams que incluye compatibilidad con SSO de forma predeterminada, como `SSO-enabled tab`. Para obtener más información sobre cómo crear una nueva aplicación, consulte [Creación de una nueva aplicación de Teams con Teams Toolkit](create-new-project.md). Se crea automáticamente un archivo de manifiesto de Azure AD en `templates\appPackage\aad.template.json`. Teams Toolkit crea o actualiza la aplicación de Azure AD durante el desarrollo local o mientras mueve la aplicación a la nube.

2. **Para agregar el inicio de sesión único al bot o a la pestaña**

      Después de crear una aplicación de Teams sin sso integrado, Teams Toolkit le ayuda incrementalmente a agregar sso para el proyecto. Como resultado, se crea automáticamente un archivo de manifiesto de Azure AD en `templates\appPackage\aad.template.json`.

      Teams Toolkit crea o actualiza la aplicación de Azure AD durante la siguiente sesión de depuración local o mientras mueve la aplicación a la nube.

3. **Para compilar localmente**

    Teams Toolkit realiza las siguientes funciones durante el desarrollo local o se conoce como F5:

    * Lea el `state.local.json` archivo para buscar una aplicación de Azure AD existente. Si ya existe una aplicación de Azure AD, Teams Toolkit reutiliza la aplicación de Azure AD existente. De lo contrario, debe crear una nueva aplicación mediante el `aad.template.json` archivo .

    * Inicialmente omite algunas propiedades del archivo de manifiesto que requieren más contexto (como la propiedad replyUrls que requiere un punto de conexión de depuración local) durante la creación de una nueva aplicación de Azure AD con el archivo de manifiesto.

    * Una vez que el entorno de desarrollo local se inicia correctamente, el identificador de la aplicación de Azure ADUris, replyUrls y otras propiedades que no están disponibles durante la fase de creación se actualizan en consecuencia.

    * Los cambios realizados en la aplicación de Azure AD se cargan durante la siguiente sesión de depuración local. Puede ver [los cambios de la aplicación de Azure AD](https://github.com/OfficeDev/TeamsFx/wiki/) para aplicar los cambios manualmente a los cambios de la aplicación de Azure AD.

4. **Para aprovisionar recursos en la nube**

      Debe aprovisionar recursos en la nube e implementar la aplicación mientras mueve la aplicación a la nube. En las fases, como el desarrollo local, teams Toolkit hará lo siguiente:

      * Lea el `state.{env}.json` archivo para buscar una aplicación de Azure AD existente. Si ya existe una aplicación de Azure AD, teams Toolkit vuelve a usar la aplicación de Azure AD existente. De lo contrario, debe crear una nueva aplicación mediante el `aad.template.json` archivo .

      * Inicialmente omite algunas propiedades del archivo de manifiesto que requieren más contexto (como la propiedad replyUrls requiere un punto de conexión de bot o front-end) durante la creación de una nueva aplicación de Azure AD con el archivo de manifiesto.

      * Una vez completado el aprovisionamiento de otros recursos, los identificadores y replyUrls de la aplicación de Azure AD se actualizan según los puntos de conexión correctos.

5. **Para compilar la aplicación**

    * La implementación en el comando en la nube implementa la aplicación en los recursos aprovisionados. No incluye la implementación de los cambios de aplicación de Azure AD realizados.

    * Puede ver Implementación de [cambios de aplicación de Azure AD para un entorno remoto](#deploy-azure-ad-application-changes-for-remote-environment) con el fin de implementar los cambios de aplicación de Azure AD para el entorno remoto.

    * Teams Toolkit actualiza la aplicación de Azure AD según el archivo de plantilla de manifiesto de Azure AD.

## <a name="limitations"></a>Limitaciones

1. La extensión del kit de herramientas de Teams no admite todas las propiedades enumeradas en el esquema de manifiesto de Azure AD.
  
      En la tabla siguiente se enumeran las propiedades que no se admiten en la extensión del kit de herramientas de Teams:

      |**Propiedades no admitidas**|**Motivo**|
      |-----------|----------|
      |passwordCredentials|No permitido en el manifiesto|
      |createdDateTime|Solo lectura y no se puede cambiar|
      |logoUrl|Solo lectura y no se puede cambiar|
      |publisherDomain|Solo lectura y no se puede cambiar|
      |oauth2RequirePostResponse|No existe en Graph API|
      |oauth2AllowUrlPathMatching|No existe en Graph API|
      |samlMetadataUrl|No existe en Graph API|
      |orgRestrictions|No existe en Graph API|
      |certificación|No existe en Graph API|

2. Actualmente `requiredResourceAccess` , la propiedad puede usar cadenas de nombre de aplicación de recursos legibles por el usuario o cadenas de nombre de permiso solo para `Microsoft Graph` las API y `Office 365 SharePoint Online` . Para otras API, debe usar UUID en su lugar. Puede seguir estos pasos para recuperar identificadores de Azure Portal:

    * Registre una nueva aplicación de Azure AD en [Azure Portal](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps).
    * Seleccione `API permissions` en la página de la aplicación de Azure AD.
    * Seleccione `add a permission` esta opción para agregar el permiso que desee.
    * Seleccione `Manifest`, en la `requiredResourceAccess` propiedad , puede encontrar los identificadores de API y permisos.

## <a name="see-also"></a>Vea también

* [Vista previa y personalización del manifiesto de la aplicación en el kit de herramientas](TeamsFx-preview-and-customize-app-manifest.md)

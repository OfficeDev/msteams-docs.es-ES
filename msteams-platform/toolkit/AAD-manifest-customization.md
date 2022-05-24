---
title: Administración de Azure Active Directory aplicación en Teams Toolkit
author: zyxiaoyuer
description: Describe la administración de Azure Active Directory aplicación en Teams Toolkit
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/20/2022
ms.openlocfilehash: 4067b86bc3a8de0ed891e84ceef68f5f95741479
ms.sourcegitcommit: 80edf3c964bb47a2ee13f9eda4334ad19e21f331
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2022
ms.locfileid: "65655651"
---
# <a name="azure-ad-manifest"></a>Manifiesto de Azure AD

El [manifiesto de Azure Active Directory (Azure AD)](/azure/active-directory/develop/reference-app-manifest) contiene definiciones de todos los atributos de un objeto de aplicación de Azure AD en el Plataforma de identidad de Microsoft.

Teams Toolkit ahora administra la aplicación de Azure AD con el archivo de manifiesto como el origen de la verdad durante los ciclos de vida de desarrollo de Teams aplicación.

## <a name="customize-azure-ad-manifest-template"></a>Personalización de la plantilla de manifiesto de Azure AD

Puede personalizar la plantilla de manifiesto de Azure AD para actualizar la aplicación de Azure AD.

1. Abra `aad.template.json` en el proyecto.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add template.png" alt-text="template":::

2. Actualice la plantilla directamente o [haga referencia a los valores de otro archivo](https://github.com/OfficeDev/TeamsFx/wiki/Manage-AAD-application-in-Teams-Toolkit#Placeholders-in-AAD-manifest-template). Puede ver varios escenarios de personalización aquí:
  
* [Agregar un permiso de aplicación](#customize-requiredresourceaccess)
* [Autenticación previa de una aplicación cliente](#customize-preauthorizedapplications)
* [Actualización de la dirección URL de redireccionamiento para la respuesta de autenticación](#customize-redirect-urls)

3. [Implemente los cambios de la aplicación de Azure AD para el entorno local](#deploy-azure-ad-application-changes-for-local-environment).
  
4. [Implemente los cambios de la aplicación de Azure AD para el entorno remoto](#deploy-azure-ad-application-changes-for-remote-environment).

### <a name="customize-requiredresourceaccess"></a>Personalización de requiredResourceAccess

Si la aplicación Teams requiere más permisos para llamar a la API con permisos adicionales, debe actualizar `requiredResourceAccess` la propiedad en la plantilla de manifiesto de Azure AD. Puede ver el ejemplo siguiente para esta propiedad:

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

* `resourceAppId` la propiedad es para distintas API, para `Microsoft Graph` y `Office 365` `SharePoint Online`, escriba el nombre directamente en lugar de UUID y, para otras API, use UUID.

* `resourceAccess.id` la propiedad es para permisos diferentes, para `Microsoft Graph` y `Office 365 SharePoint Online`, escriba el nombre del permiso directamente en lugar de UUID y, para otras API, use UUID.

* `resourceAccess.type` se usa para el permiso delegado o el permiso de aplicación. `Scope` significa permiso delegado y `Role` significa permiso de aplicación.

### <a name="customize-preauthorizedapplications"></a>Personalización de preAuthorizedApplications

Puede usar `preAuthorizedApplications` la propiedad para autorizar a una aplicación cliente para indicar que la API confía en la aplicación y los usuarios no dan su consentimiento cuando el cliente la llama a la API expuesta. Puede ver el ejemplo siguiente para esta propiedad:

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

`preAuthorizedApplications.appId` se usa para la aplicación que desea autorizar. Si no conoce el identificador de la aplicación, pero solo conoce el nombre de la aplicación, puede ir a Azure Portal y seguir los pasos para buscar en la aplicación el identificador :

1. Vaya a [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) y abra registros de aplicaciones.

1. Seleccione **Todas las aplicaciones** y busque el nombre de la aplicación.

1. Seleccione el nombre de la aplicación y obtenga el identificador de la aplicación en la página de información general.

### <a name="customize-redirect-urls"></a>Personalización de direcciones URL de redireccionamiento

  Las direcciones URL de redireccionamiento se usan al devolver respuestas de autenticación como tokens después de la autenticación correcta. Puede personalizar las direcciones URL de redireccionamiento mediante la propiedad `replyUrlsWithType`, por ejemplo, para agregar `https://www.examples.com/auth-end.html` como dirección URL de redireccionamiento, puede agregarla como el ejemplo siguiente:

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

Puede usar este argumento de marcador de posición en el manifiesto de Azure AD: `{{state.fx-resource-aad-app-for-teams.applicationIdUris}}` para hacer referencia `applicationIdUris` al valor de la `fx-resource-aad-app-for-teams` propiedad .

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

Al principio del archivo de plantilla de manifiesto de Azure AD, hay una lente de código en versión preliminar. Seleccione la lente de código, genera el manifiesto de Azure AD en función del entorno seleccionado.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/add codelens.png" alt-text="addcodelens":::

### <a name="placeholder-argument-code-lens"></a>Lente de código de argumento de marcador de posición

La lente de código de argumento de marcador de posición le ayuda a examinar rápidamente los valores del entorno de depuración y desarrollo local. Si el mouse mantiene el puntero sobre el argumento de marcador de posición, muestra el cuadro de información sobre herramientas para los valores de todo el entorno.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/add arguments.png" alt-text="addarguments":::

### <a name="required-resource-access-code-lens"></a>Lente de código de acceso a recursos requerida

Es diferente del esquema de manifiesto oficial de [Azure AD](/azure/active-directory/develop/reference-app-manifest) que `resourceAppId` y `resourceAccess` el identificador de `requiredResourceAccess` la propiedad solo admiten UUID, la plantilla de manifiesto de Azure AD en Teams Toolkit también admite cadenas legibles por el usuario para `Microsoft Graph` y `Office 365 SharePoint Online` permisos. Si escribe UUID, code lens muestra cadenas legibles por el usuario; de lo contrario, muestra UUID.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/add resource.png" alt-text="addresource":::

### <a name="pre-authorized-applications-code-lens"></a>Lente de código de aplicaciones previamente autorizadas

La lente de código muestra el nombre de la aplicación para el identificador de aplicación por autorización de la `preAuthorizedApplications` propiedad .

## <a name="deploy-azure-ad-application-changes-for-local-environment"></a>Implementación de cambios de la aplicación de Azure AD para el entorno local

1. Seleccione `Preview` la lente de código en `aad.template.json`.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy1.png" alt-text="deploy1":::

2. Seleccione `local` entorno.
  
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

1. Copie el identificador de cliente de la aplicación de Azure AD del `state.xxx.json` archivo (xxx es el nombre del entorno que ha implementado la aplicación de Azure AD) en la `fx-resource-aad-app-for-teams` propiedad .
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add view1.png" alt-text="view1":::

2. Vaya a [Azure Portal](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) e inicie sesión en Microsoft 365 cuenta.
  
> [!NOTE]
> Asegúrese de que las credenciales de inicio de sesión de Teams aplicación y cuenta de M365 sean las mismas.

3. Abra [la página Registros](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) de aplicaciones y busque la aplicación de Azure AD mediante el identificador de cliente que copió antes.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add view2.png" alt-text="view2":::

4. Seleccione la aplicación de Azure AD en el resultado de la búsqueda para ver la información detallada.
  
5. En la página de información de la aplicación de Azure AD, seleccione `Manifest` el menú para ver el manifiesto de esta aplicación. El esquema del manifiesto es el mismo que el del `aad.template.json` archivo. Para obtener más información sobre el manifiesto, consulte [Azure Active Directory manifiesto de aplicación](/azure/active-directory/develop/reference-app-manifest).
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add view3.png" alt-text="view3":::

6. Puede seleccionar **Otro menú** para ver o configurar la aplicación de Azure AD a través del portal.
  
## <a name="use-an-existing-azure-ad-application"></a>Uso de una aplicación de Azure AD existente

Puede usar la aplicación de Azure AD existente para el proyecto de Teams. Para obtener más información, consulte [Uso de una aplicación de Azure AD existente para la aplicación de Teams](https://github.com/OfficeDev/TeamsFx/wiki/Customize-provision-behaviors#use-an-existing-aad-app-for-your-teams-app).

## <a name="azure-ad-application-in-teams-application-development-lifecycle"></a>Aplicación de Azure AD en Teams ciclo de vida de desarrollo de aplicaciones

Debe interactuar con la aplicación de Azure AD durante varias fases del ciclo de vida de desarrollo de Teams aplicación.

1. **Para crear Project**

      Puede crear un proyecto con Teams Toolkit que incluye compatibilidad con SSO de forma predeterminada, como `SSO-enabled tab`. Para obtener más información para crear una nueva aplicación, consulte [Creación de una nueva aplicación Teams mediante Teams Toolkit](create-new-project.md). Se crea automáticamente un archivo de manifiesto de Azure AD: `templates\appPackage\aad.template.json`. Teams Toolkit crea o actualiza la aplicación de Azure AD durante el desarrollo local o mientras mueve la aplicación a la nube.

2. **Para agregar el inicio de sesión único al bot o a la pestaña**

      Después de crear una aplicación de Teams sin sso integrado, Teams Toolkit ayuda incrementalmente a agregar el inicio de sesión único para el proyecto. Como resultado, se crea automáticamente un archivo de manifiesto de Azure AD: `templates\appPackage\aad.template.json`.

      Teams Toolkit crea o actualiza la aplicación de Azure AD durante la siguiente sesión de depuración local o mientras mueve la aplicación a la nube.

3. **Para compilar localmente**

    Teams Toolkit realiza las siguientes funciones durante el desarrollo local (conocido como F5):

    * Lea el `state.local.json` archivo para buscar una aplicación de Azure AD existente. Si ya existe una aplicación de Azure AD, Teams Toolkit vuelve a usar la aplicación de Azure AD existente; de lo contrario, debe crear una nueva aplicación mediante el `aad.template.json` archivo .

    * Inicialmente omite algunas propiedades del archivo de manifiesto que requieren contexto adicional (como la propiedad replyUrls que requiere un punto de conexión de depuración local) durante la creación de una nueva aplicación de Azure AD con el archivo de manifiesto.

    * Una vez que el entorno de desarrollo local se inicia correctamente, el identificador de la aplicación de Azure ADUris, replyUrls y otras propiedades que no están disponibles durante la fase de creación se actualizan en consecuencia.

    * Los cambios realizados en la aplicación de Azure AD se cargan durante la siguiente sesión de depuración local. Puede ver [los cambios de la aplicación de Azure AD](https://github.com/OfficeDev/TeamsFx/wiki/) para aplicar los cambios manualmente a la aplicación de Azure AD.

4. **Para aprovisionar recursos en la nube**

      Debe aprovisionar recursos en la nube e implementar la aplicación mientras mueve la aplicación a la nube. En las fases, como el desarrollo local, Teams Toolkit:

      * Lea el `state.{env}.json` archivo para buscar una aplicación de Azure AD existente. Si ya existe una aplicación de Azure AD, Teams Toolkit vuelve a usar la aplicación de Azure AD existente; de lo contrario, debe crear una nueva aplicación mediante el `aad.template.json` archivo .

      * Inicialmente omite algunas propiedades del archivo de manifiesto que requieren contexto adicional (como la propiedad replyUrls requiere el punto de conexión de front-end o bot) durante la creación de una nueva aplicación de Azure AD con el archivo de manifiesto.

      * Una vez completado el aprovisionamiento de otros recursos, los identificadores y replyUrls de la aplicación de Azure AD se actualizan según los puntos de conexión correctos.

5. **Para compilar la aplicación**

    * La implementación en el comando en la nube implementa la aplicación en los recursos aprovisionados. No incluye la implementación de los cambios de aplicación de Azure AD que realizó.

    * Puede ver [Implementación de cambios de aplicación de Azure AD para el entorno remoto](#deploy-azure-ad-application-changes-for-remote-environment) para implementar cambios de aplicación de Azure AD para el entorno remoto

    * Teams Toolkit actualiza la aplicación de Azure AD según el archivo de plantilla de manifiesto de Azure AD

## <a name="limitations"></a>Limitaciones

1. Teams Toolkit extensión no admite todas las propiedades enumeradas en el esquema de manifiesto de Azure AD.
  
      En la tabla siguiente se enumeran las propiedades que no se admiten en Teams Toolkit extensión:

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

    * Registro de una nueva aplicación de Azure AD en [Azure Portal](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)
    * Selección `API permissions` en la página de la aplicación de Azure AD
    * Seleccione `add a permission` esta opción para agregar el permiso que desee.
    * Seleccione `Manifest`, en la `requiredResourceAccess` propiedad , puede encontrar los identificadores de api y permisos.

## <a name="see-also"></a>Vea también

* [Personalizar el manifiesto de la aplicación en el kit de herramientas](TeamsFx-manifest-customization.md)
* [Vista previa del manifiesto de aplicación en el kit de herramientas](TeamsFx-manifest-preview.md)

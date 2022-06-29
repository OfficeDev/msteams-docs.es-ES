---
title: usar el kit de herramientas de Teams para aprovisionar recursos en la nube
author: MuyangAmigo
description: En este módulo, aprenderá a aprovisionar recursos en la nube mediante el kit de herramientas de Teams, a crear y personalizar el aprovisionamiento de recursos.
ms.author: shenwe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 7d95c5310147f9f974802d007a951d80a12acbe0
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503371"
---
# <a name="provision-cloud-resources-using-teams-toolkit"></a>Aprovisionamiento de recursos en la nube mediante el kit de herramientas de Teams

TeamsFx se integra con Azure y la nube de Microsoft 365, lo que le permite colocar la aplicación en Azure con un solo comando. TeamsFx se integra con Azure Resource Manager que le permite aprovisionar los recursos de Azure que su aplicación necesita para el enfoque de código.

## <a name="prerequisites"></a>Requisitos previos

* Requisitos previos. Para aprovisionar recursos en la nube, debe tener las siguientes cuentas:

  * Cuenta de Microsoft 365 con una suscripción válida.
  * Azure con una suscripción válida.
  Para obtener más información, vea [cómo preparar cuentas para crear aplicaciones de Teams](accounts.md).

* [Instale el Kit de herramientas de Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión v3.0.0+.

> [!TIP]
> Asegúrese de que ha abierto un proyecto de aplicación de Teams en VS Code.

## <a name="provision-using-teams-toolkit"></a>Aprovisionamiento mediante el kit de herramientas de Teams

El aprovisionamiento se realiza con un solo comando en el kit de herramientas de Teams para Visual Studio Code o la CLI de TeamsFx como se indica a continuación:

[Aprovisionamiento de una aplicación basada en Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8)

## <a name="resource-creation"></a>Creación de recursos

Al desencadenar el comando de aprovisionamiento en el kit de herramientas de Teams o la CLI de TeamsFx, puede obtener los siguientes recursos:

* Microsoft Azure Active Directory aplicación (Azure AD) en el inquilino de Microsoft 365.
* Registro de aplicaciones de Teams en la plataforma de Teams del inquilino de Microsoft 365.
* Recursos de Azure en la suscripción de Azure seleccionada.

Al crear un nuevo proyecto, puede usar todos los recursos de Azure. La plantilla de ARM define todos los recursos de Azure y ayuda a crear los recursos de Azure necesarios durante el aprovisionamiento. Al [añadir nuevos recursos de funcionalidad](./add-resource.md) a un proyecto existente, la plantilla de ARM actualizada refleja el cambio más reciente.

> [!NOTE]
> Los servicios de Azure incurren en costes en su suscripción. Para obtener más información sobre la estimación de costes, consulte [la calculadora de precios](https://azure.microsoft.com/pricing/calculator/).

### <a name="resource-creation-for-teams-tab-application"></a>Creación de recursos para aplicaciones de pestaña de Teams

|Resource|Objetivo|Descripción |
|----------|--------------------------------|-----|
| Azure Storage | Alojar su aplicación de pestaña | Habilita la característica de aplicación web estática para alojar la aplicación de pestaña |
| Plan de servicio de aplicación para autenticación simple | Alojar la aplicación web de autenticación simple |No aplicable |
| Aplicación web para autenticación simple | Alojar un servidor de autenticación simple para obtener acceso a otros servicios en su aplicación de página única | Añade la identidad asignada por el usuario para acceder a otros recursos de Azure |
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure | Compartido entre diferentes funcionalidades y recursos |

### <a name="resource-creation-for-teams-bot-or-message-extension-application"></a>Creación de recursos para aplicación de extensión de mensaje o bot de Teams

|Resource|Objetivo| Descripción |
|----------|--------------------------------|-----|
| Servicio de bot de Azure | Registra su aplicación como bot con Bot Framework | Conecta el bot a Teams |
| Plan de servicio de aplicación para el bot | Alojar la aplicación web del bot |No aplicable |
| Aplicación web para el bot | Alojar la aplicación de bot | Añade la identidad asignada por el usuario para acceder a otros recursos de Azure. <br /> Añade la configuración de la aplicación requerida por el [SDK de TeamsFx](https://www.npmjs.com/package/@microsoft/teamsfx). |
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure | Compartido entre diferentes funcionalidades y recursos |

### <a name="resource-creation-for-azure-functions-in-the-project"></a>Creación de recursos para Azure Functions en el proyecto

|Resource|Objetivo| Descripción|
|----------|--------------------------------|-----|
| Plan de servicio para aplicación de funciones | Alojar la aplicación de funciones |No aplicable |
| Aplicación de funciones | Alojar las API de funciones de Azure | Añade la identidad asignada por el usuario para acceder a otros recursos de Azure. <br /> Añade una regla de uso compartido de recursos entre orígenes (CORS) para permitir solicitudes desde su aplicación de pestaña <br /> Añade la configuración de autenticación que solo permite las solicitudes de su aplicación de Teams. <br /> Añade la configuración de la aplicación requerida por el [SDK de TeamsFx](https://www.npmjs.com/package/@microsoft/teamsfx). |
| Almacenamiento de Azure para la aplicación de funciones | Necesario para crear una aplicación de funciones |No aplicable|
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure | Compartido entre diferentes funcionalidades y recursos |

### <a name="resource-creation-for-azure-sql-in-the-project"></a>Creación de recursos para Azure SQL en el proyecto

|Resource|Objetivo | Descripción |
|----------|--------------------------------|-----|
| Servidor de Azure SQL | Alojar la instancia de base de datos Azure SQL | Permite que todos los servicios de Azure accedan al servidor |
| Base de datos SQL Azure | Almacenar datos para la aplicación | Concede permisos de lectura o escritura en la base de datos a la identidad asignada por el usuario |
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure | Compartido entre diferentes funcionalidades y recursos |

### <a name="resource-creation-for-azure-api-management-in-the-project"></a>Creación de recursos para Azure API Management en el proyecto

|Resource|Objetivo|
|----------|--------------------------------|
| Aplicación Azure AD para el servicio de administración de API | Permite a Microsoft Power Platform acceder a las API administradas por el servicio de administración de API |
| Servicio de administración de API | Administrar las API alojadas en la aplicación de funciones |
| Producto de administración de API | Agrupar las API, definir términos de uso y directivas en tiempo de ejecución |
| Servidor OAuth de administración de API | Permite a Microsoft Power Platform acceder a las API alojadas en la aplicación de funciones |
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure |

### <a name="resources-created-when-including-azure-key-vault-in-the-project"></a>Recursos creados al incluir Azure Key Vault en el proyecto

|Recursos|Propósito de este recurso|
|----------|--------------------------------|
| Servicio Azure Key Vault | Administrar secretos (por ejemplo, secreto de cliente de aplicación Azure AD) que usan otros servicios de Azure |
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure |

## <a name="customize-resource-provision"></a>Personalización del aprovisionamiento de recursos

El kit de herramientas de Teams le permite usar un enfoque de infraestructura como código para definir qué recursos de Azure quiere aprovisionar y cómo quiere configurarlos. La herramienta usa la plantilla de ARM para definir recursos de Azure. La plantilla de ARM es un conjunto de archivos bicep que define la infraestructura y configuración del proyecto. Puede personalizar los recursos de Azure modificando la plantilla de ARM. Para obtener más información, consulte la [documentación de bicep](/azure/azure-resource-manager/bicep).

Aprovisionar con ARM implica cambiar los siguientes conjuntos de archivos, parámetros y plantillas:

* Archivos de parámetros de ARM (`azure.parameters.{your_env_name}.json`) ubicados en la carpeta `.fx/configs`, para pasar parámetros a plantillas.
* Los archivos de plantilla de ARM ubicados en `templates/azure`, esta carpeta contiene los siguientes archivos:

| Archivo | Función | Permitir personalización |
| --- | --- | --- |
| main.bicep | Proporcionar punto de entrada para el aprovisionamiento de recursos de Azure | Sí |
| provision.bicep | Crear y configurar recursos de Azure | Sí |
| config.bicep | Añadir las configuraciones necesarias de TeamsFx a los recursos de Azure | Sí |
| provision/xxx.bicep | Crear y configurar cada recurso de Azure consumido por `provision.bicep` | Sí |
| teamsfx/xxx.bicep | Añadir las configuraciones necesarias de TeamsFx a cada recurso de Azure consumido por `config.bicep`| No |

> [!NOTE]
> Al añadir recursos o funcionalidades al proyecto, `teamsfx/xxx.bicep` se volverá a generar. No puede personalizarlo. Para modificar los archivos bicep puede usar Git para hacer un seguimiento de los cambios de los archivos `teamsfx/xxx.bicep`, lo que le ayuda a no perder los cambios al añadir recursos o funcionalidades.

### <a name="customize-arm-parameters-and-templates"></a>Personalización de parámetros y plantillas de ARM

Puede personalizar los recursos de Azure personalizando los archivos de parámetros y personalizando los archivos bicep.

#### <a name="customize-arm-template-parameter-files"></a>Personalización de archivos de parámetros de plantillas de ARM

El kit de herramientas proporciona un conjunto de parámetros predefinidos para personalizar los recursos de Azure. Los archivos de parámetros se encuentran en `.fx/configs/azure.parameters.{env}.json` y todos los parámetros disponibles se definen en la propiedad `provisionParameters`. Se recomienda personalizar los archivos de parámetros si los parámetros predefinidos satisfacen sus necesidades.

En la tabla siguiente se proporciona una lista de parámetros predefinidos disponibles:

| Nombre del parámetro | Valor predeterminado | Qué puede personalizar el parámetro | Restricciones de valor |
| --- | --- | --- | --- |
| resourceBaseName | Generado automáticamente para cada entorno | Nombre predeterminado para todos los recursos | De 2 a 20 letras minúsculas y números |
| simpleAuthServerFarmsName | ${resourceBaseName}simpleAuth | Nombre del plan de servicio de aplicación de autenticación simple | De 1 a 40 caracteres alfanuméricos y guiones |
| simpleAuthWebAppName | ${resourceBaseName}simpleAuth | Nombre de la aplicación web de autenticación simple | De 2 a 60 caracteres alfanuméricos y guiones <br /> No puede empezar ni terminar con guión |
| simpleAuthSku | F1 | SKU del plan de servicio de aplicación de autenticación simple | No aplicable |
| frontendHostingStorageName | ${resourceBaseName}tab | Nombre de la cuenta de almacenamiento de alojamiento de frontend | De 3 a 24 letras minúsculas y números |
| frontendHostingStorageSku | Standard_LRS | SKU de la cuenta de almacenamiento de alojamiento de frontend |[SKU disponibles](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep)|
| functionServerfarmsName | ${resourceBaseName}api | Nombre del plan de servicio de aplicaciones de funciones | De 1 a 40 caracteres alfanuméricos y guiones |
| functionServerfarmsSku | Y1 | SKU del plan de servicio de aplicaciones de funciones | No aplicable|
| functionAppName | ${resourceBaseName}api | Nombre de la aplicación de funciones | De 2 a 60 caracteres alfanuméricos y guiones <br /> No puede empezar ni terminar con guión |
| functionStorageName | ${resourceBaseName}api | Nombre de la cuenta de almacenamiento de la aplicación de funciones | De 3 a 24 letras minúsculas y números |
| functionStorageSku | Standard_LRS | SKU de la cuenta de almacenamiento de la aplicación de funciones | [SKU disponibles](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep) |
| botServiceName | ${resourceBaseName} | Nombre del servicio de bot de Azure | De 2 a 64 caracteres alfanuméricos, guiones bajos, puntos y guiones <br /> Debe empezar con un carácter alfanumérico |
| botServiceSku | F0 | SKU del servicio de bot de Azure | [SKU disponibles](/azure/templates/microsoft.botservice/2021-05-01-preview/botservices?tabs=bicep) |
| botDisplayName | ${resourceBaseName} | Nombre para mostrar del bot | De 1 a 42 caracteres |
| botServerfarmsName | ${resourceBaseName}bot | Nombre del plan de servicio de aplicación del bot | De 1 a 40 caracteres alfanuméricos y guiones |
| botWebAppName | ${resourceBaseName}bot | Nombre de la aplicación web del bot | De 2 a 60 caracteres alfanuméricos y guiones <br /> No puede empezar ni terminar con guión |
| botWebAppSKU | F1 | SKU del plan de servicio de aplicación del bot | No aplicable |
| userAssignedIdentityName | ${resourceBaseName} | Nombre de la identidad asignada por el usuario | De 3 a 128 caracteres alfanuméricos, guiones y guiones bajos <br /> Debe empezar con una letra o un número |
| sqlServerName | ${resourceBaseName} | Nombre del servidor de Azure SQL | De 1 a 63 letras minúsculas, números y guiones <br /> No puede empezar ni terminar con guión |
| sqlDatabaseName | ${resourceBaseName} | Nombre de la base de datos Azure SQL | De 1 a 128 caracteres, no se puede usar <>*%&:\/? o caracteres de control <br /> No puede terminar con punto o espacio |
| sqlDatabaseSku | Básico | SKU de la base de datos Azure SQL | No aplicable  |
| apimServiceName | ${resourceBaseName} | Nombre del servicio APIM | De 1 a 50 caracteres alfanuméricos y guiones <br /> Debe empezar con una letra y terminar con un carácter alfanumérico |
| apimServiceSku | Consumo | SKU del servicio APIM | [SKU disponibles](/azure/templates/microsoft.apimanagement/service?tabs=bicep) |
| apimProductName | ${resourceBaseName} | Nombre del producto APIM | De 1 a 80 caracteres alfanuméricos y guiones <br /> Debe empezar con una letra y terminar con un carácter alfanumérico |
| apimOauthServerName | ${resourceBaseName} | Nombre del servidor OAuth de APIM | De 1 a 80 caracteres alfanuméricos y guiones <br /> Debe empezar con una letra y terminar con un carácter alfanumérico |
| keyVaultSkuName | estándar | Nombre de SKU del servicio Azure Key Vault| |

Mientras tanto, los siguientes parámetros están disponibles con valores rellenados durante el aprovisionamiento. El propósito de estos marcadores de posición es asegurarse de que podemos crear nuevos recursos para usted en el nuevo entorno. Los valores reales se resuelven a partir de `.fx/states/state.{env}.json`.

##### <a name="azure-ad-application-related-parameters"></a>Parámetros relacionados con la aplicación de Azure AD

| Nombre del parámetro | Marcador de posición de valor predeterminado | Significado del marcador de posición | Cómo personalizar |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | Id. de cliente de la aplicación de Azure AD creada durante el aprovisionamiento | [Personalice el valor](#use-an-existing-azure-ad-app-for-your-teams-app) |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | Secreto de cliente de la aplicación Azure AD creado durante el aprovisionamiento | [Personalice el valor](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | Identificador de inquilino de la aplicación de Azure AD | [Personalice el valor](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 OAuthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | Host de autoridad OAuth de la aplicación de Azure AD | [Personalice el valor](#use-an-existing-azure-ad-app-for-your-teams-app) |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | Id. de cliente de la aplicación de Azure AD del bot creada durante el aprovisionamiento | [Personalice el valor](#use-an-existing-azure-ad-app-for-your-bot) |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | Secreto de cliente de la aplicación de Azure AD del bot creado durante el aprovisionamiento | [Personalice el valor](#use-an-existing-azure-ad-app-for-your-bot) |
| apimClientId | {{state.fx-resource-apim.apimClientAADClientId}} | Id. de cliente de la aplicación de APIM de Azure AD creada durante el aprovisionamiento | Elimine el marcador de posición y rellene con el valor real |
| apimClientSecret | {{state.fx-resource-apim.apimClientAADClientSecret}} | Secreto de cliente de la aplicación APIM de Azure AD creado durante el aprovisionamiento | Elimine el marcador de posición y rellene con el valor real |

##### <a name="azure-resource-related-parameters"></a>Parámetros de Azure relacionados con recursos

| Nombre del parámetro | Marcador de posición de valor predeterminado | Significado del marcador de posición | Cómo personalizar |
| --- | --- | --- | --- |
| azureSqlAdmin | {{state.fx-resource-azure-sql.admin}} | Cuenta de administrador de Azure SQL Server que proporcionó durante el aprovisionamiento | Elimine el marcador de posición y rellene con el valor real |
| azureSqlAdminPassword | {{state.fx-resource-azure-sql.adminPassword}} | Contraseña de administrador de Azure SQL Server que proporcionó durante el aprovisionamiento | Elimine el marcador de posición y rellene con el valor real |
| apimPublisherEmail | {{state.fx-resource-apim.publisherEmail}} | Correo electrónico del publicador de APIM. El valor predeterminado es su cuenta de Azure | Elimine el marcador de posición y rellene con el valor real |
| apimPublisherName | {{state.fx-resource-apim.publisherName}} | Nombre del publicador de APIM. El valor predeterminado es su cuenta de Azure | Elimine el marcador de posición y rellene con el valor real |

#### <a name="referencing-environment-variables-in-parameter-files"></a>Referenciando variables de entorno en archivos de parámetros

Si no desea escribir los valores en archivos de parámetros, por ejemplo, cuando el valor es un secreto, los archivos de parámetros admiten referenciar valores de las variables de entorno. Puede usar la sintaxis `{{$env.YOUR_ENV_VARIABLE_NAME}}` en los valores de parámetro para que la herramienta los resuelva a partir de la variable de entorno actual.

En el ejemplo siguiente se lee el valor del parámetro `mySelfHostedDbConnectionString` de la variable de entorno `DB_CONNECTION_STRING`:

```json
...
    "mySelfHostedDbConnectionString": "{{$env.DB_CONNECTION_STRING}}"
...
```

#### <a name="customize-arm-template-files"></a>Personalización de archivos de plantilla de ARM

Si las plantillas predefinidas no cumplen los requisitos de su aplicación, puede personalizar las plantillas de ARM en la carpeta `templates/azure`. Por ejemplo, puede personalizar la plantilla de ARM para crear algunos recursos adicionales de Azure para la aplicación. Debe tener conocimientos básicos del lenguaje bicep, que se usa para crear una plantilla de ARM. Puede empezar a trabajar con bicep con la [documentación de bicep](/azure/azure-resource-manager/bicep/).

> [!NOTE]
> Todos los entornos comparten la plantilla de ARM. Puede usar la [implementación condicional](/azure/azure-resource-manager/bicep/conditional-resource-deployment) si el comportamiento de aprovisionamiento varía entre entornos.

Para asegurarse de que la herramienta TeamsFx funciona correctamente, asegúrese de personalizar la plantilla de ARM, que debe cumplir los siguientes requisitos. Si usa otra herramienta de desarrollo, puede ignorar estos requisitos.

* No modifique la estructura de carpetas ni el nombre de archivo. La herramienta puede anexar contenido nuevo a los archivos existentes al añadir más recursos o funcionalidades al proyecto.
* No modifique los nombres de los parámetros generados automáticamente ni de sus propiedades. Puede que se usen los parámetros generados automáticamente al añadir más recursos o funcionalidades al proyecto.
* No modifique la salida de la plantilla de ARM generada automáticamente. Puede añadir salidas adicionales a la plantilla de ARM. La salida es `.fx/states/state.{env}.json` y se puede usar en otras características, como implementar y validar el archivo de manifiesto.

### <a name="customization-scenarios"></a>Escenarios de personalización

Puede personalizar los siguientes escenarios:

#### <a name="use-an-existing-azure-ad-app-for-your-bot"></a>Uso de una aplicación de Azure AD existente para el bot

Puede añadir el siguiente fragmento de código de configuración al archivo `.fx/configs/config.{env}.json` para usar una aplicación de Azure AD creada por usted mismo para la aplicación de Teams. Para crear una aplicación de Azure AD, consulte <https://aka.ms/teamsfx-existing-aad-doc>.

```json
"auth": {
    "clientId": "<your Azure AD app client id>",
    "clientSecret": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}",
    "objectId": "<your Azure AD app object id>",
    "accessAsUserScopeId": "<id of the access_as_user scope>"
}
```

Después de añadir el fragmento de código, añada el secreto a la variable de entorno relacionada para que la herramienta pueda resolver el secreto real durante el aprovisionamiento.

> [!NOTE]
> Asegúrese de no compartir la misma aplicación Azure AD en varios entornos. Si no tiene permiso para actualizar la aplicación de Azure AD, puede obtener una advertencia con instrucciones sobre cómo actualizar manualmente la aplicación de Azure AD. Siga las instrucciones para actualizar la aplicación de Azure AD después del aprovisionamiento.

#### <a name="use-an-existing-azure-ad-app-for-your-teams-app"></a>Uso de una aplicación de Azure AD existente para su aplicación de Teams

Puede añadir el siguiente fragmento de código de configuración al archivo `.fx/configs/config.{env}.json` para usar una aplicación de Azure AD creada por usted mismo para el bot:

```json
"bot": {
    "appId": "<your Azure AD app client id>",
    "appPassword": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}"
}
```

Después de añadir el fragmento de código anterior, añada el secreto a la variable de entorno relacionada para que la herramienta resuelva el secreto real durante el aprovisionamiento.

#### <a name="skip-adding-user-for-sql-database"></a>Omisión de la adición de usuario a la base de datos SQL

Si recibe un error de permiso insuficiente cuando la herramienta intenta añadir un usuario a la base de datos SQL, puede añadir el siguiente fragmento de código de configuración al archivo `.fx/configs/config.{env}.json` para omitir la adición de usuario a la base de datos SQL:

```json
"skipAddingSqlUser": true
```

### <a name="specifying-the-name-of-function-app-instance"></a>Especificación del nombre de la instancia de la aplicación de funciones

Puede usar `contosoteamsappapi` para la instancia de la aplicación de funciones en lugar de usar el nombre predeterminado.

> [!NOTE]
> Si ya ha aprovisionado el entorno, especificar el nombre puede crear una nueva instancia de aplicación de funciones automáticamente, en lugar de renombrar la instancia creada anteriormente.

Los pasos siguientes son:

1. Abra `.fx/configs/azure.parameters.{env}.json` para el entorno actual.
2. Añada una nueva propiedad `functionAppName` al valor del parámetro `provisionParameters`.
3. Escriba `contosoteamsappapi` como valor de `functionAppName`.
4. El archivo de parámetros definitivo se muestra en el siguiente fragmento de código:

    ```json
    {
        "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "provisionParameters": {
            "value": {
                "functionAppName": "contosoteamsappapi"
                ...
                }
            }
        }
    }
    ```

### <a name="scenerio"></a>Situación

Para añadir otro recurso o almacenamiento de Azure a la aplicación:

Tenga en cuenta la siguiente situación: desea añadir almacenamiento de Azure al backend de la función de Azure para almacenar datos BLOB. No hay ningún flujo automático para actualizar la plantilla bicep con compatibilidad con el almacenamiento de Azure. Sin embargo, puede editar el archivo bicep y añadir el recurso. Los pasos son los siguientes:

1. Cree un proyecto de pestaña.
2. Añada la función al proyecto. Para obtener más información, consulte [añadir recursos](./add-resource.md).
3. Declare la nueva cuenta de almacenamiento en la plantilla de ARM. Puede declarar el recurso directamente en `templates/azure/provision/function.bicep`. También puede declarar los recursos en otros lugares.

    `````````bicep
    var applicationStorageAccountName = 'myapp${uniqueString(resourceGroup().id)}'
    resource applicationStorageAccount 'Microsoft.Storage/storageAccounts@2021-06-01' = {
        name: applicationStorageAccountName
        location: resourceGroup().location
        kind: 'Storage'
        sku: {
            name: 'Standard_LRS'
        }
    }
    `````````

4. Actualice la configuración de la aplicación de funciones de Azure con la cadena de conexión de almacenamiento de Azure en `templates/azure/provision/function.bicep`. Añada el siguiente fragmento de código a la matriz `appSettings` del recurso `functionApp`:

    ``````````````````bicep
    {
        name: 'MyAppStorageAccountConnectionString'
        value: 'DefaultEndpointsProtocol=https;AccountName=${applicationStorageAccount.name};AccountKey=${listKeys(applicationStorageAccount.id, '2021-06-01').keys[0].value}'
    }
    ```````````````````

5. Puede actualizar la función con enlaces de salida de Azure Storage.

## <a name="faq"></a>Preguntas más frecuentes

<br>

<details>

<summary><b>Solución de problemas</b></summary>

Si recibe errores con el kit de herramientas de Teams en Visual Studio Code, puede seleccionar **Obtener ayuda** en la notificación del error para navegar al documento relacionado. Si usa la CLI de TeamsFx, al final del mensaje habrá un hipervínculo que apunta al documento de ayuda. También puede ver el [documento de ayuda de aprovisionamiento](https://aka.ms/teamsfx-arm-help) directamente.

<br>

</details>

<details>

<summary><b>¿Cómo puedo cambiar a otra suscripción de Azure durante el aprovisionamiento?</b></summary>

1. Cambie la suscripción en la cuenta actual o cierre la sesión y seleccione una nueva suscripción.
2. Si ya ha aprovisionado el entorno actual, debe crear un nuevo entorno y realizar el aprovisionamiento porque ARM no admite el traslado de recursos.
3. Si no aprovisionó el entorno actual, puede desencadenar el aprovisionamiento directamente.

<br>

</details>

<details>

<summary><b>¿Cómo puedo cambiar el grupo de recursos durante el aprovisionamiento?</b></summary>

Antes del aprovisionamiento, la herramienta le pregunta si desea crear un nuevo grupo de recursos o usar uno existente. Puede proporcionar un nuevo nombre de grupo de recursos o elegir uno existente en este paso.

<br>

</details>

<details>

<summary><b>¿Cómo puedo aprovisionar una aplicación basada en SharePoint?</b></summary>

Puede consultar [aprovisionamiento de aplicaciones basadas en SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4).

> [!NOTE]
> Actualmente, compilar aplicaciones de Teams con SharePoint Framework con el kit de herramientas de Teams no tiene integración directa con Azure. Los contenidos en el documento no se aplican a aplicaciones basadas en SPFx.

<br>

</details>

## <a name="see-also"></a>Consulte también

* [Implementar la aplicación de Teams en la nube](deploy.md)
* [Administrar varios entornos](TeamsFx-multi-env.md)
* [Colaborar con otros desarrolladores en proyectos de Teams](TeamsFx-collaboration.md)

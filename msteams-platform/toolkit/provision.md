---
title: usar el kit de herramientas de Teams para aprovisionar recursos en la nube
author: MuyangAmigo
description: Aprovisionar recursos en la nube
ms.author: shenwe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 24b058957ab0db7ebd2ab9178ac95fe9473257e6
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104122"
---
# <a name="use-teams-toolkit-to-provision-cloud-resources"></a>usar el kit de herramientas de Teams para aprovisionar recursos en la nube

TeamsFx se integra con Azure y Microsoft 365 nube, lo que permite colocar la aplicación en Azure con un solo comando. TeamsFx se integra con Azure Resource Manager que le permite aprovisionar recursos de Azure, que la aplicación necesita para el enfoque de código.  

## <a name="prerequisites"></a>Requisitos previos

* Requisitos previos de la cuenta Para aprovisionar recursos en la nube, debe tener las siguientes cuentas:

  * Microsoft 365 cuenta con una suscripción válida
  * Azure con una suscripción válida Para obtener más información, consulte [preparación de cuentas para compilar Teams aplicación](accounts.md).

* [Instale Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión v3.0.0+.

> [!TIP]
> Asegúrese de que ha abierto Teams proyecto de aplicación en vs code.

## <a name="provision-using-teams-toolkit"></a>Aprovisionamiento mediante Teams Toolkit

El aprovisionamiento se realiza con un solo comando en Teams Toolkit para Visual Studio Code o la CLI de TeamsFx como se indica a continuación:

[Aprovisionamiento de una aplicación basada en Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8)

## <a name="resource-creation"></a>Creación de recursos

Al desencadenar el comando de aprovisionamiento en Teams Toolkit o la CLI de TeamsFx, puede obtener los siguientes recursos:

* aplicación Microsoft Azure Active Directory (Azure AD) en el inquilino de Microsoft 365
* Teams registro de aplicaciones en la plataforma de Teams del inquilino de Microsoft 365
* Recursos de Azure en la suscripción de Azure seleccionada

Al crear un nuevo proyecto, puede usar todos los recursos de Azure. La plantilla de ARM define todos los recursos de Azure y ayuda a crear los recursos de Azure necesarios durante el aprovisionamiento. Al [agregar un nuevo recurso de funcionalidad](./add-resource.md) a un proyecto existente, la plantilla de ARM actualizada refleja el cambio más reciente.

> [!NOTE]
> Los servicios de Azure incurren en costos en su suscripción. Para obtener más información sobre la estimación de costos, consulte [la calculadora de precios](https://azure.microsoft.com/pricing/calculator/).

### <a name="resource-creation-for-teams-tab-application"></a>Creación de recursos para Teams aplicación Tab

|Resource|Objetivo|Descripción |
|----------|--------------------------------|-----|
| Azure Storage | Hospedar la aplicación de pestaña | Habilita la característica de aplicación web estática para hospedar la aplicación de pestaña |
| Plan de App Service para la autenticación simple | Hospedar la aplicación web de autenticación simple |No aplicable |
| Aplicación web para la autenticación simple | Hospedar un servidor de autenticación simple para obtener acceso a otros servicios en la aplicación de página única | Agrega la identidad asignada por el usuario para acceder a otros recursos de Azure. |
| Identidad asignada por el usuario | Autenticación de solicitudes de servicio a servicio de Azure | Compartido entre diferentes funcionalidades y recursos |

### <a name="resource-creation-for-teams-bot-or-message-extension-application"></a>Creación de recursos para Teams aplicación de extensión de mensaje o bot

|Resource|Objetivo| Descripción |
|----------|--------------------------------|-----|
| Servicio bot de Azure | Registra la aplicación como bot con bot framework | Conecta el bot a Teams |
| Plan de App Service para bot | Hospedar la aplicación web del bot |No aplicable |
| Aplicación web para bot | Hospedar la aplicación de bot | Agrega la identidad asignada por el usuario para acceder a otros recursos de Azure. <br /> Agrega la configuración de la aplicación requerida por [el SDK de TeamsFx](https://www.npmjs.com/package/@microsoft/teamsfx) |
| Identidad asignada por el usuario | Autenticación de solicitudes de servicio a servicio de Azure | Compartido entre diferentes funcionalidades y recursos |

### <a name="resource-creation-for-azure-functions-in-the-project"></a>Creación de recursos para Azure Functions en el proyecto

|Resource|Objetivo| Descripción|
|----------|--------------------------------|-----|
| Plan de App Service para la aplicación de funciones | Hospedar la aplicación de funciones |No aplicable |
| Aplicación de funciones | Hospedar las API de Azure Functions | Agrega la identidad asignada por el usuario para acceder a otros recursos de Azure. <br /> Agrega una regla de uso compartido de recursos entre orígenes (CORS) para permitir solicitudes desde la aplicación de pestaña <br /> Agrega la configuración de autenticación que solo permite las solicitudes de la aplicación de Teams. <br /> Agrega la configuración de la aplicación requerida por [el SDK de TeamsFx](https://www.npmjs.com/package/@microsoft/teamsfx) |
| Azure Storage para la aplicación de funciones | Necesario para crear una aplicación de funciones |No aplicable|
| Identidad asignada por el usuario | Autenticación de solicitudes de servicio a servicio de Azure | Compartido entre diferentes funcionalidades y recursos |

### <a name="resource-creation-for-azure-sql-in-the-project"></a>Creación de recursos para Azure SQL en el proyecto

|Resource|Objetivo | Descripción |
|----------|--------------------------------|-----|
| servidor de Azure SQL | Hospedar la instancia de base de datos Azure SQL | Permite que todos los servicios de Azure accedan al servidor. |
| Base de datos SQL Azure | Almacenar datos para la aplicación | Concede a la base de datos permisos de identidad, lectura o escritura asignados por el usuario |
| Identidad asignada por el usuario | Autenticación de solicitudes de servicio a servicio de Azure | Compartido entre diferentes funcionalidades y recursos |

### <a name="resource-creation-for-azure-api-management-in-the-project"></a>Creación de recursos para Azure API Management en el proyecto

|Resource|Objetivo|
|----------|--------------------------------|
| Azure AD aplicación para el servicio API Management | Permite a Las API de acceso de Microsoft Power Platform administradas por el servicio API Management |
| Servicio API Management | Administración de las API hospedadas en la aplicación de funciones |
| Producto de API Management | Agrupación de las API, definición de términos de uso y directivas en tiempo de ejecución |
| Servidor OAuth de API Management | Permite a Microsoft Power Platform acceder a las API hospedadas en la aplicación de funciones |
| Identidad asignada por el usuario | Autenticación de solicitudes de servicio a servicio de Azure |

### <a name="resources-created-when-including-azure-key-vault-in-the-project"></a>Recursos creados al incluir Azure Key Vault en el proyecto

|Recursos|Propósito de este recurso|
|----------|--------------------------------|
| Servicio azure Key Vault | Administración de secretos (por ejemplo, Azure AD secreto de cliente de aplicación) que usan otros servicios de Azure |
| Identidad asignada por el usuario | Autenticación de solicitudes de servicio a servicio de Azure |

## <a name="customize-resource-provision"></a>Personalización del aprovisionamiento de recursos

Teams Toolkit permite usar una infraestructura como enfoque de código para definir qué recursos de Azure desea aprovisionar y cómo desea configurar. La herramienta usa la plantilla de ARM para definir recursos de Azure. La plantilla de ARM es un conjunto de archivos bicep que define la infraestructura y la configuración del proyecto. Puede personalizar los recursos de Azure modificando la plantilla de ARM. Para obtener más información, consulte [el documento de bicep](/azure/azure-resource-manager/bicep).

Aprovisionar con ARM implica cambiar los siguientes conjuntos de archivos, parámetros y plantillas:

* Archivos de parámetros de ARM (`azure.parameters.{your_env_name}.json`) ubicados en la `.fx/configs` carpeta para pasar parámetros a plantillas.
* Los archivos de plantilla de ARM ubicados en `templates/azure`, esta carpeta contiene los siguientes archivos:

| Archivo | Función | Permitir personalización |
| --- | --- | --- |
| main.bicep | Proporcionar punto de entrada para el aprovisionamiento de recursos de Azure | Sí |
| provision.bicep | Creación y configuración de recursos de Azure | Sí |
| config.bicep | Adición de las configuraciones necesarias de TeamsFx a los recursos de Azure | Sí |
| provision/xxx.bicep | Creación y configuración de cada recurso de Azure consumido por `provision.bicep` | Sí |
| teamsfx/xxx.bicep | Adición de las configuraciones necesarias de TeamsFx a cada recurso de Azure consumido por `config.bicep`| No |

> [!NOTE]
> Al agregar recursos o funcionalidades al proyecto, `teamsfx/xxx.bicep` se volverán a generar, no se puede personalizar lo mismo. Para modificar los archivos de bicep, puede usar Git para realizar un seguimiento de los cambios en los `teamsfx/xxx.bicep` archivos, lo que le ayuda a no perder los cambios al agregar recursos o funcionalidades.

### <a name="customize-arm-parameters-and-templates"></a>Personalización de parámetros y plantillas de ARM

Puede personalizar los recursos de Azure personalizando los archivos de parámetros y personalizando los archivos bicep.

#### <a name="customize-arm-template-parameter-files"></a>Personalización de archivos de parámetros de plantilla de ARM

El kit de herramientas proporciona un conjunto de parámetros predefinidos para personalizar los recursos de Azure. Los archivos de parámetros se encuentran en `.fx/configs/azure.parameters.{env}.json` y todos los parámetros disponibles se definen en la `provisionParameters` propiedad . Se recomienda personalizar los archivos de parámetros si los parámetros predefinidos satisfacen sus necesidades.

En la tabla siguiente se proporciona una lista de parámetros predefinidos disponibles:

| Nombre del parámetro | Valor predeterminado | Qué puede personalizar el parámetro | Restricciones de valor |
| --- | --- | --- | --- |
| resourceBaseName | Generado automáticamente para cada entorno | Nombre predeterminado para todos los recursos | 2-20 letras minúsculas y números |
| simpleAuthServerFarmsName | ${resourceBaseName}simpleAuth | Nombre del plan de App Service de autenticación simple | 1-40 alfanuméricos y guiones |
| simpleAuthWebAppName | ${resourceBaseName}simpleAuth | Nombre de la aplicación web de autenticación simple | 2-60 alfanuméricos y guiones <br /> No se puede iniciar o finalizar con guion |
| simpleAuthSku | F1 | SKU del plan de App Service de autenticación simple | No aplicable |
| frontendHostingStorageName | Pestaña ${resourceBaseName} | Nombre de la cuenta de almacenamiento de hospedaje de front-end | 3-24 letras minúsculas y números |
| frontendHostingStorageSku | Standard_LRS | SKU de la cuenta de almacenamiento de hospedaje de front-end |[SKU disponibles](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep)|
| functionServerfarmsName | ${resourceBaseName}api | Nombre del plan de servicio de las aplicaciones de función | 1-40 alfanuméricos y guiones |
| functionServerfarmsSku | Y1 | SKU del plan de servicio de las aplicaciones de función | No aplicable|
| functionAppName | ${resourceBaseName}api | Nombre de la aplicación de funciones | 2-60 alfanuméricos y guiones <br /> No se puede iniciar o finalizar con guion |
| functionStorageName | ${resourceBaseName}api | Nombre de la cuenta de almacenamiento de la aplicación de función | 3-24 letras minúsculas y números |
| functionStorageSku | Standard_LRS | SKU de la cuenta de almacenamiento de la aplicación de funciones | [SKU disponibles](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep) |
| botServiceName | ${resourceBaseName} | Nombre del servicio bot de Azure | 2-64 alfanuméricos, caracteres de subrayado, puntos y guiones <br /> Empezar con alfanumérico |
| botServiceSku | F0 | SKU de Azure Bot Service | [SKU disponibles](/azure/templates/microsoft.botservice/2021-05-01-preview/botservices?tabs=bicep) |
| botDisplayName | ${resourceBaseName} | Nombre para mostrar del bot | 1-42 caracteres |
| botServerfarmsName | Bot ${resourceBaseName} | Nombre del plan de App Service del bot | 1-40 alfanuméricos y guiones |
| botWebAppName | Bot ${resourceBaseName} | Nombre de la aplicación web del bot | 2-60 alfanuméricos y guiones <br /> No se puede iniciar o finalizar con guion |
| botWebAppSKU | F1 | SKU del plan de bot App Service | No aplicable |
| userAssignedIdentityName | ${resourceBaseName} | Nombre de la identidad asignada por el usuario | 3-128 alfanuméricos, guiones y caracteres de subrayado <br /> Empezar con letra o número |
| sqlServerName | ${resourceBaseName} | Nombre del servidor de Azure SQL | 1-63 letras minúsculas, números y guiones <br /> No se puede iniciar ni terminar con guiones |
| sqlDatabaseName | ${resourceBaseName} | Nombre de Azure SQL base de datos | De 1 a 128 caracteres, no se puede usar <>*%&:\/? o caracteres de control <br /> No se puede terminar con punto o espacio |
| sqlDatabaseSku | Básico | SKU de Azure SQL base de datos | No aplicable  |
| apimServiceName | ${resourceBaseName} | Nombre del servicio APIM | 1-50 alfanuméricos y guiones <br /> Comience con letra y termine con alfanumérico |
| apimServiceSku | Consumo | SKU del servicio APIM | [SKU disponibles](/azure/templates/microsoft.apimanagement/service?tabs=bicep) |
| apimProductName | ${resourceBaseName} | Nombre del producto APIM | 1-80 alfanuméricos y guiones <br /> Comience con letra y termine con alfanumérico |
| apimOauthServerName | ${resourceBaseName} | Nombre del servidor OAuth de APIM | 1-80 alfanuméricos y guiones <br /> Comience con letra y termine con alfanumérico |
| keyVaultSkuName | Estándar | Nombre de SKU de Azure Key Vault Service| |

Mientras tanto, los siguientes parámetros están disponibles con valores rellenados durante el aprovisionamiento. El propósito de estos marcadores de posición es asegurarse de que podemos crear nuevos recursos para usted en un nuevo entorno. Los valores reales se resuelven a partir de `.fx/states/state.{env}.json`.

##### <a name="azure-ad-application-related-parameters"></a>Azure AD parámetros relacionados con la aplicación

| Nombre del parámetro | Soporte de posición de valor predeterminado | Significado del titular del lugar | Cómo personalizar |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | Id. de cliente de la aplicación Azure AD creado durante el aprovisionamiento | [Personalización del valor](#use-an-existing-azure-ad-app-for-your-teams-app) |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | El secreto de cliente de la aplicación Azure AD de la aplicación creado durante el aprovisionamiento | [Personalización del valor](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | Identificador de inquilino de la aplicación Azure AD aplicación | [Personalización del valor](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 OAuthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | Host de autoridad de OAuth de la aplicación de Azure AD | [Personalización del valor](#use-an-existing-azure-ad-app-for-your-teams-app) |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | Identificador de cliente de Azure AD aplicación del bot creado durante el aprovisionamiento | [Personalización del valor](#use-an-existing-azure-ad-app-for-your-bot) |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | Secreto de cliente de Azure AD aplicación del bot creado durante el aprovisionamiento | [Personalización del valor](#use-an-existing-azure-ad-app-for-your-bot) |
| apimClientId | {{state.fx-resource-apim.apimClientAADClientId}} | Identificador de cliente de la aplicación Azure AD de APIM creado durante el aprovisionamiento | Eliminar el marcador de posición y rellenar el valor real |
| apimClientSecret | {{state.fx-resource-apim.apimClientAADClientSecret}} | Secreto de cliente de la aplicación Azure AD de APIM creado durante el aprovisionamiento | Eliminar el marcador de posición y rellenar el valor real |

##### <a name="azure-resource-related-parameters"></a>Parámetros relacionados con recursos de Azure

| Nombre del parámetro | Soporte de posición de valor predeterminado | Significado del titular del lugar | Cómo personalizar |
| --- | --- | --- | --- |
| azureSqlAdmin | {{state.fx-resource-azure-sql.admin}} | Azure SQL cuenta de administrador del servidor que proporcionó durante el aprovisionamiento | Eliminar el marcador de posición y rellenar el valor real |
| azureSqlAdminPassword | {{state.fx-resource-azure-sql.adminPassword}} | Azure SQL contraseña de administrador del servidor que proporcionó durante el aprovisionamiento | Eliminar el marcador de posición y rellenar el valor real |
| apimPublisherEmail | {{state.fx-resource-apim.publisherEmail}} | Correo electrónico del publicador de APIM, el valor predeterminado es su cuenta de Azure | Eliminar el marcador de posición y rellenar el valor real |
| apimPublisherName | {{state.fx-resource-apim.publisherName}} | Nombre del publicador de APIM, el valor predeterminado es su cuenta de Azure | Eliminar el marcador de posición y rellenar el valor real |

#### <a name="referencing-environment-variables-in-parameter-files"></a>Referencia a variables de entorno en archivos de parámetros

Si no desea codificar de forma rígida los valores de los archivos de parámetros, por ejemplo, cuando el valor es un secreto. Los archivos de parámetros admiten la referencia a los valores de las variables de entorno. Puede usar la sintaxis `{{$env.YOUR_ENV_VARIABLE_NAME}}` en los valores de parámetro para que la herramienta se resuelva a partir de la variable de entorno actual.

En el ejemplo siguiente se lee el valor del parámetro de `mySelfHostedDbConnectionString` la variable `DB_CONNECTION_STRING`de entorno :

```json
...
    "mySelfHostedDbConnectionString": "{{$env.DB_CONNECTION_STRING}}"
...
```

#### <a name="customize-arm-template-files"></a>Personalización de archivos de plantilla de ARM

Si las plantillas predefinidas no cumplen los requisitos de la aplicación, puede personalizar las plantillas de ARM en `templates/azure` la carpeta . Por ejemplo, puede personalizar la plantilla de ARM para crear algunos recursos adicionales de Azure para la aplicación. Debe tener conocimientos básicos del lenguaje bicep, que se usa para crear una plantilla de ARM. Puede empezar a trabajar con bicep en la [documentación de bicep](/azure/azure-resource-manager/bicep/).

> [!NOTE]
> Todos los entornos comparten la plantilla de ARM. Puede usar la [implementación condicional](/azure/azure-resource-manager/bicep/conditional-resource-deployment) si el comportamiento de aprovisionamiento varía entre entornos.

Para asegurarse de que la herramienta TeamsFx funciona correctamente, asegúrese de personalizar la plantilla de ARM, que satisface el siguiente requisito. Si usa otra herramienta para el desarrollo posterior, puede omitir estos requisitos.

* Mantenga la estructura de carpetas y el nombre de archivo sin cambios. La herramienta puede anexar contenido nuevo a los archivos existentes al agregar más recursos o funcionalidades al proyecto.
* Mantenga el nombre de los parámetros generados automáticamente, así como sus nombres de propiedad sin cambios. Los parámetros generados automáticamente se pueden usar al agregar más recursos o funcionalidades al proyecto.
* Mantenga la salida de la plantilla de ARM generada automáticamente sin cambios. Puede agregar salidas adicionales a la plantilla de ARM. La salida es `.fx/states/state.{env}.json` y se puede usar en otras características, como implementar y validar el archivo de manifiesto.

### <a name="customization-scenarios"></a>Escenarios de personalización

Puede personalizar los siguientes escenarios:

#### <a name="use-an-existing-azure-ad-app-for-your-bot"></a>Uso de una aplicación de Azure AD existente para el bot

Puede agregar el siguiente fragmento de código de configuración al `.fx/configs/config.{env}.json` archivo para usar una aplicación de Azure AD creada por usted mismo para la aplicación de Teams. Para crear una aplicación Azure AD, consulte <https://aka.ms/teamsfx-existing-aad-doc>.

```json
"auth": {
    "clientId": "<your Azure AD app client id>",
    "clientSecret": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}",
    "objectId": "<your Azure AD app object id>",
    "accessAsUserScopeId": "<id of the access_as_user scope>"
}
```

Después de agregar el fragmento de código, agregue el secreto a la variable de entorno relacionada para que la herramienta pueda resolver el secreto real durante el aprovisionamiento.

> [!NOTE]
> Asegúrese de no compartir la misma aplicación Azure AD en varios entornos. Si no tiene permiso para actualizar la aplicación Azure AD, puede obtener una advertencia con instrucciones sobre cómo actualizar manualmente la aplicación Azure AD. Siga las instrucciones para actualizar la aplicación Azure AD después del aprovisionamiento.

#### <a name="use-an-existing-azure-ad-app-for-your-teams-app"></a>Uso de una aplicación de Azure AD existente para la aplicación de Teams

Puede agregar el siguiente fragmento de código de configuración al `.fx/configs/config.{env}.json` archivo para usar una aplicación de Azure AD creada por usted mismo para el bot:

```json
"bot": {
    "appId": "<your Azure AD app client id>",
    "appPassword": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}"
}
```

Después de agregar el fragmento de código anterior, agregue el secreto a la variable de entorno relacionada para que la herramienta resuelva el secreto real durante el aprovisionamiento.

#### <a name="skip-adding-user-for-sql-database"></a>Omitir la adición de usuario para SQL base de datos

Si no tiene ningún error de permiso insuficiente cuando la herramienta intenta agregar un usuario a SQL base de datos, puede agregar el siguiente fragmento de código de configuración al `.fx/configs/config.{env}.json` archivo para omitir la adición de SQL usuario de base de datos:

```json
"skipAddingSqlUser": true
```

### <a name="specifying-the-name-of-function-app-instance"></a>Especificación del nombre de la instancia de Function App

Puede usar `contosoteamsappapi` para la instancia de la aplicación de funciones en lugar de usar el nombre predeterminado.

> [!NOTE]
> Si ya ha aprovisionado el entorno, especificar el nombre puede crear una nueva instancia de aplicación de función automáticamente, en lugar de cambiar el nombre de la instancia creada anteriormente.

Los pasos siguientes son:

1. Abra `.fx/configs/azure.parameters.{env}.json` para el entorno actual.
2. Agregue una nueva propiedad `functionAppName` al valor del parámetro `provisionParameters`.
3. Escriba `contosoteamsappapi` como valor de `functionAppName`
4. El archivo de parámetros final se muestra en el siguiente fragmento de código:

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

### <a name="scenerio"></a>Scenerio

Para agregar otro recurso o almacenamiento de Azure a la aplicación:

Tenga en cuenta el escenario, quiere agregar Azure Storage al back-end de la función de Azure para almacenar datos de blobs. No hay ningún flujo automático para actualizar la plantilla de bicep con compatibilidad con Azure Storage. Sin embargo, puede editar el archivo bicep y agregar el recurso. Los pasos son los siguientes:

1. Cree un proyecto de pestaña.
2. Agregue la función al proyecto. Para obtener más información, vea [Agregar recursos](./add-resource.md).
3. Declare la nueva cuenta de almacenamiento en la plantilla de ARM. Puede declarar el recurso directamente en `templates/azure/provision/function.bicep` . Puede declarar los recursos en otros lugares.

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

4. Actualice la configuración de la aplicación de funciones de Azure con la cadena de conexión de Azure Storage en `templates/azure/provision/function.bicep`. Agregue el siguiente fragmento de código a la `functionApp` matriz del `appSettings` recurso:

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

<summary><b>¿Cómo solucionar problemas?</b></summary>

Si recibe errores con Teams Toolkit en Visual Studio Code, puede seleccionar **Obtener ayuda** en la notificación de error para navegar al documento relacionado. Si usa la CLI de TeamsFx, habrá un hipervínculo al final del mensaje de error que apunte al documento de ayuda. También puede ver el [documento de ayuda de aprovisionamiento](https://aka.ms/teamsfx-arm-help) directamente.

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

Antes de aprovisionar, la herramienta le preguntará si desea crear un nuevo grupo de recursos o usar uno existente. Puede proporcionar un nuevo nombre de grupo de recursos o elegir uno existente en este paso.

<br>

</details>

<details>

<summary><b>¿Cómo puedo aprovisionar una aplicación basada en SharePoint?</b></summary>

Puede seguir el [aprovisionamiento SharePoint aplicación basada en](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4) .

> [!NOTE]
> Actualmente, la compilación de Teams aplicación con SharePoint Framework con Teams Toolkit no tiene integración directa con Azure; el contenido del documento no se aplica a las aplicaciones basadas en SPFx.

<br>

</details>

## <a name="see-also"></a>Vea también

* [Implementar la aplicación de Teams en la nube](deploy.md)
* [Administrar varios entornos](TeamsFx-multi-env.md)
* [Colaborar con otros desarrolladores en proyectos de Teams](TeamsFx-collaboration.md)

---
title: Usar Teams Toolkit para aprovisionar recursos en la nube
author: MuyangAmigo
description: Aprovisionar recursos en la nube
ms.author: shenwe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: c8899131876533fdd64913fb6790cff9f258e8f5
ms.sourcegitcommit: aede47694894d281f6b725083bc0b46ab0e4846d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/22/2021
ms.locfileid: "61591788"
---
# <a name="use-teams-toolkit-to-provision-cloud-resources"></a>Usar Teams Toolkit para aprovisionar recursos en la nube

TeamsFx proporciona una integración perfecta con Azure y Microsoft 365 nube que le permite colocar la aplicación en Azure con un solo comando. TeamsFx se integra con Azure Resource Manager que le permite aprovisionar declarativamente los recursos de Azure que necesita la aplicación mediante la infraestructura como método de código.  

## <a name="prerequisites"></a>Requisitos previos

* Requisitos previos de la cuenta

    Para aprovisionar recursos en la nube, debe tener las siguientes cuentas con los permisos adecuados. Para obtener más información, [consulta Preparar cuentas para crear Teams aplicación](accounts.md).
    * Microsoft 365
    * Azure con suscripción válida

* [Instale Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión 3.0.0+.

> [!TIP]
> Ya debería tener abierto un proyecto Teams aplicación en el código VS.

## <a name="provision-using-teams-toolkit"></a>Aprovisionar mediante Teams Toolkit

La aprovisionamiento se realiza con un solo comando en Teams Toolkit para Visual Studio Code o CLI de TeamsFx de la siguiente manera:

[Aprovisionar aplicación basada en Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)

## <a name="resource-creation"></a>Creación de recursos

Al desencadenar el comando de aprovisionamiento en Teams Toolkit CLI de TeamsFx, puede obtener los siguientes recursos:

* AAD aplicación en el inquilino Microsoft 365 usuario
* Teams registro de la aplicación en la Microsoft 365 de la plataforma de Teams inquilino
* Recursos de Azure en la suscripción de Azure seleccionada

Al crear un nuevo proyecto, obtiene todos los recursos de Azure que se crearán. La plantilla ARM de azure define todos los recursos de Azure y ayuda a crear los recursos de Azure necesarios durante la provisión. Cuando agrega [nueva funcionalidad o](./add-resource.md) recurso a un proyecto existente, la plantilla de ARM plantilla refleja el cambio más reciente.

> [!NOTE]
> Los servicios de Azure incurren en costos en la suscripción, puede consultar la calculadora [de precios](https://azure.microsoft.com/pricing/calculator/) para comprender una estimación.

### <a name="resource-creation-for-teams-tab-application"></a>Creación de recursos para Teams tab

|Recursos|Finalidad de este recurso| Notas |
|----------|--------------------------------|-----|
| Azure Storage | Hospedar la aplicación de pestaña | Habilita la característica de aplicación web estática para hospedar la aplicación de pestañas |
| Plan de App Service para Auth simple | Hospedar la aplicación web de Simple Auth | |
| Aplicación web para autenticación simple | Host simple auth server that helps you gain access to other services in your single page application | Agrega identidad asignada al usuario para facilitar el acceso a otros recursos de Azure |
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure | Compartido entre diferentes capacidades y recursos |

### <a name="resources-created-for-teams-bot-or-messaging-extension-application"></a>Recursos creados para Teams bot o aplicación de extensión de mensajería

|Recursos|Finalidad de este recurso| Notas |
|----------|--------------------------------|-----|
| Servicio de bots de Azure | Registra la aplicación como un bot con bot Framework | Conecta el bot a Teams |
| Plan de App Service para bot | Hospedar la aplicación web de Bot | |
| Aplicación web para bot | Hospedar la aplicación bot | Agrega la identidad asignada por el usuario para facilitar el acceso a otros recursos de Azure. <br /> Agrega la configuración de la aplicación requerida [por el SDK de TeamsFx](https://www.npmjs.com/package/@microsoft/teamsfx) |
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure | Compartido entre diferentes capacidades y recursos |

### <a name="resources-created-when-including-azure-functions-in-the-project"></a>Recursos creados al incluir Azure Functions en el proyecto

|Recursos|Finalidad de este recurso| Notas |
|----------|--------------------------------|-----|
| Plan de App Service para function app | Hospedar la aplicación function | |
| Function App | Hospedar las API de Azure Functions | Agrega la identidad asignada por el usuario para facilitar el acceso a otros recursos de Azure. <br /> Agrega una regla CORS para permitir solicitudes desde la aplicación de pestaña <br /> Agrega la configuración de autenticación que solo permite las solicitudes de Teams aplicación. <br /> Agrega la configuración de la aplicación requerida [por el SDK de TeamsFx](https://www.npmjs.com/package/@microsoft/teamsfx) |
| Azure Storage para function app | Necesario al crear function app | |
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure | Compartido entre diferentes capacidades y recursos |

### <a name="resources-created-when-including-azure-sql-in-the-project"></a>Recursos creados al incluir Azure SQL en el proyecto

|Recursos|Finalidad de este recurso| Notas |
|----------|--------------------------------|-----|
| Azure SQL Server | Hospedar la Azure SQL Database de datos | Permite que todos los servicios de Azure accedan al servidor |
| Base de datos SQL de Azure | Almacenar datos para la aplicación | Concede al usuario permiso de lectura y escritura de identidad asignado a la base de datos |
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure | Compartido entre diferentes capacidades y recursos |

### <a name="resources-created-when-including-azure-api-management-in-the-project"></a>Recursos creados al incluir Azure API Management en el proyecto

|Recursos|Finalidad de este recurso|
|----------|--------------------------------|
| Azure Active Directory aplicación para el servicio de administración de API | Permite a las API de acceso de Microsoft Power Platform administradas por el servicio de administración de API |
| Servicio de administración de API | Administrar las API hospedadas en Function App |
| Producto de administración de API | Agrupar las API, definir términos de uso y directivas de tiempo de ejecución |
| Servidor OAuth de administración de API | Permite que Microsoft Power Platform obtenga acceso a las API hospedadas en Function App |
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure |

## <a name="customize-resource-provision"></a>Personalizar la provisión de recursos

Teams Toolkit permite usar una infraestructura como método de código para definir qué recursos de Azure desea aprovisionar y cómo desea configurarlos. Las herramientas usan ARM plantilla para definir recursos de Azure. La ARM es un conjunto de archivos bíceps que define la infraestructura y la configuración del proyecto. Puede personalizar los recursos de Azure creados modificando la ARM plantilla. Para obtener más información, vea [el documento bícep](/azure/azure-resource-manager/bicep.md). Aprovisionar con ARM implica cambiar los siguientes dos conjuntos de archivos, parámetros y plantillas:

* ARM archivos de parámetros ( `azure.parameters.{your_env_name}.json` ) se encuentran en la `.fx/configs` carpeta, para pasar parámetros a plantillas.
* ARM archivos de plantilla ubicados en `templates/azure` , esta carpeta contiene los siguientes archivos:

| Archivo | ¿Qué hace? | Permitir la personalización |
| --- | --- | --- |
| main.bicep | Proporcionar punto de entrada para la provisión de recursos de Azure | Sí |
| provision.bicep | Crear y configurar recursos de Azure | Sí |
| config.bicep | Agregar configuraciones necesarias de TeamsFx a recursos de Azure | Sí |
| provision/xxx.bicep | crear y configurar cada recurso de Azure consumido por `provision.bicep` | Sí |
| teamsfx/xxx.bicep | Agregar configuraciones necesarias de TeamsFx a cada recurso de Azure consumido por `config.bicep`| No |

> [!NOTE]
> cuando agregue recursos o capacidades al proyecto, `teamsfx/xxx.bicep` se regenerará. Por eso se marca como no personalizable. Si realmente tiene el requisito de modificar estos archivos bíceps, se recomienda usar Git para realizar un seguimiento de los cambios en los archivos para que no pierda los cambios al agregar recursos `teamsfx/xxx.bicep` o capacidades.

### <a name="customize-arm-parameters-and-templates"></a>Personalizar ARM parámetros y plantillas

Puede personalizar los recursos de Azure personalizando los archivos de parámetros y personalizando los archivos bíceps.

#### <a name="customize-arm-template-parameter-files"></a>Personalizar ARM de parámetros de plantilla

El kit de herramientas proporciona un conjunto de parámetros predefinidos para personalizar los recursos de Azure. Los archivos de parámetros se encuentran en `.fx/configs/azure.parameters.{env}.json` y todos los parámetros disponibles se definen en la `provisionParameters` propiedad. Es preferible personalizar los archivos de parámetros si los parámetros predefinidos satisfacen sus requisitos.

Esta es una lista de parámetros predefinidos disponibles:

| Nombre del parámetro | Valor predeterminado | Qué puede personalizar el parámetro | Restricciones de valor |
| --- | --- | --- | --- |
| resourceBaseName | Generado automáticamente para cada entorno | Nombre predeterminado para todos los recursos | 2-20 minúsculas y números |
| simpleAuthServerFarmsName | ${resourceBaseName}simpleAuth | Nombre del plan simple de Auth App Service | 1-40 alfanuméricos y guiones |
| simpleAuthWebAppName | ${resourceBaseName}simpleAuth | Nombre de Auth Web App simple | 2-60 alfanuméricos y guiones <br /> No se puede iniciar ni terminar con guion |
| simpleAuthSku | F1 | SKU del plan simple de Auth App Service |  |
| frontendHostingStorageName | Ficha ${resourceBaseName} | Nombre de la cuenta de Storage front-end | 3-24 minúsculas y números |
| frontendHostingStorageSku | Standard_LRS | SKU de frontend hosting Storage account | Consulte esta página [para ver](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep&branch) las SKU disponibles |
| functionServerfarmsName | ${resourceBaseName}api | Nombre del plan de App Service de Function App | 1-40 alfanuméricos y guiones |
| functionServerfarmsSku | Y1 | SKU del Plan de App Service de FUnction App |
| functionAppName | ${resourceBaseName}api | Nombre de function app | 2-60 alfanuméricos y guiones <br /> No se puede iniciar ni terminar con guion |
| functionStorageName | ${resourceBaseName}api | Nombre de la cuenta de Storage function app | 3-24 minúsculas y números |
| functionStorageSku | Standard_LRS | SKU de la cuenta de Storage function app | Consulte esta página [para ver](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep&branch=pr-en-us-4713)las SKU disponibles |
| botServiceName | ${resourceBaseName} | Nombre del servicio bot de Azure | 2-64 alfanuméricos, guiones bajos, puntos y guiones <br /> Empezar por alfanumérico |
| botServiceSku | F0 | SKU del servicio bot de Azure | Consulte esta página [para ver](/azure/templates/microsoft.botservice/2021-05-01-preview/botservices?tabs=bicep&branch) las SKU disponibles |
| botDisplayName | ${resourceBaseName} | Nombre para mostrar del bot | De 1 a 42 caracteres |
| botServerfarmsName | Bot ${resourceBaseName} | Nombre del plan de App Service del Bot | 1-40 alfanuméricos y guiones |
| botWebAppName | Bot ${resourceBaseName} | Nombre de la aplicación web del bot | 2-60 alfanuméricos y guiones <br /> No se puede iniciar ni terminar con guion |
| botWebAppSKU | F1 | SKU de Bot App Service Plan |  |
| userAssignedIdentityName | ${resourceBaseName} | Nombre de la identidad asignada por el usuario | 3-128 alfanuméricos, guiones y guiones bajos <br /> Empezar con letra o número |
| sqlServerName | ${resourceBaseName} | Nombre de Azure SQL Server | 1-63 minúsculas, números y guiones <br /> No se puede iniciar ni terminar con guion |
| sqlDatabaseName | ${resourceBaseName} | Nombre de Azure SQL Database | De 1 a 128 caracteres, no se puede usar <>*%&: \/ ? o caracteres de control <br /> No se puede terminar con punto o espacio |
| sqlDatabaseSku | Básico | SKU de Azure SQL Database |  |
| apimServiceName | ${resourceBaseName} | Nombre del servicio APIM | 1-50 alfanuméricos y guiones <br /> Comience por letra y termine con alfanumérico |
| apimServiceSku | Consumo | SKU del servicio APIM | Consulte esta página [para ver](/azure/templates/microsoft.apimanagement/service?tabs=bicep&branch)las SKU disponibles |
| apimProductName | ${resourceBaseName} | Nombre del producto APIM | 1-80 alfanuméricos y guiones <br /> Comience por letra y termine con alfanumérico |
| apimOauthServerName | ${resourceBaseName} | Nombre del servidor OAuth de APIM | 1-80 alfanuméricos y guiones <br /> Comience por letra y termine con alfanumérico |

Mientras tanto, los siguientes parámetros están disponibles con valores rellenados durante la provisión. El propósito de estos marcadores de posición es garantizar que podamos crear nuevos recursos al crear un nuevo entorno. Los valores reales se resuelven desde `.fx/states/state.{env}.json` .

##### <a name="aad-application-related-parameters"></a>AAD parámetros relacionados con la aplicación

| Nombre del parámetro | Soporte de posición de valor predeterminado | Significado del soporte de la posición | Cómo personalizar |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | El identificador de cliente de AAD de la aplicación creado durante la provisión | Consulte [esta sección](#use-an-existing-aad-app-for-your-teams-app) para personalizar el valor |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | Secreto de cliente de aplicación AAD la aplicación creada durante la provisión | Consulte [esta sección](#use-an-existing-aad-app-for-your-teams-app) para personalizar el valor |
| Microsoft 365TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | Identificador de inquilino de la aplicación AAD aplicación | Consulte [esta sección](#use-an-existing-aad-app-for-your-teams-app) para personalizar el valor |
| Microsoft 365 OauthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | Host de autoridad de OAuth de la aplicación AAD aplicación | Consulte [esta sección](#use-an-existing-aad-app-for-your-teams-app) para personalizar el valor |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | Identificador de cliente de AAD aplicación de bot creado durante la provisión | Consulte [esta sección](#use-an-existing-aad-app-for-your-bot) para personalizar el valor |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | Secreto de cliente AAD aplicación de bot creado durante la provisión | Consulte [esta sección](#use-an-existing-aad-app-for-your-bot) para personalizar el valor |
| apimClientId | {{state.fx-resource-apim.apimClientAADClientId}} | Identificador de cliente de AAD apim creado durante la provisión | Eliminar el marcador de posición y rellenar el valor real |
| apimClientSecret | {{state.fx-resource-apim.apimClientAADClientSecret}} | Secreto de cliente de AAD apim creado durante la provisión | Eliminar el marcador de posición y rellenar el valor real |

##### <a name="azure-resource-related-parameters"></a>Parámetros relacionados con recursos de Azure

| Nombre del parámetro | Soporte de posición de valor predeterminado | Significado del soporte de la posición | Cómo personalizar |
| --- | --- | --- | --- |
| azureSqlAdmin | {{state.fx-resource-azure-sql.admin}} | Cuenta SQL Server administrador de Azure que proporcionó durante la aprovisionamiento | Eliminar el marcador de posición y rellenar el valor real |
| azureSqlAdminPassword | {{state.fx-resource-azure-sql.adminPassword}} | Contraseña SQL Server administrador de Azure que proporcionó durante la provisión | Eliminar el marcador de posición y rellenar el valor real |
| apimPublisherEmail | {{state.fx-resource-apim.publisherEmail}} | Correo electrónico del editor de APIM, el valor predeterminado es su cuenta de Azure | Eliminar el marcador de posición y rellenar el valor real |
| apimPublisherName | {{state.fx-resource-apim.publisherName}} | Nombre del editor de APIM, el valor predeterminado es su cuenta de Azure | Eliminar el marcador de posición y rellenar el valor real |

#### <a name="referencing-environment-variables-in-parameter-files"></a>Referencia a variables de entorno en archivos de parámetros

Es posible que algunas veces no quiera codificar los valores de los archivos de parámetros. Por ejemplo, cuando el valor es un secreto. Los archivos de parámetros admiten hacer referencia a los valores de las variables de entorno. Puede usar la sintaxis en los valores de parámetros para decir a las herramientas que el valor debe resolverse desde `{{$env.YOUR_ENV_VARIABLE_NAME}}` la variable de entorno actual.

En el siguiente ejemplo se leerá el valor del `mySelfHostedDbConnectionString` parámetro de la variable de entorno `DB_CONNECTION_STRING` :

```json
...
    "mySelfHostedDbConnectionString": "{{$env.DB_CONNECTION_STRING}}"
...
```

#### <a name="customize-arm-template-files"></a>Personalizar ARM de plantilla

Si las plantillas predefinidas no cumplen los requisitos de la aplicación, puede personalizar las plantillas ARM en la `templates/azure` carpeta. Por ejemplo, puedes personalizar la plantilla ARM para crear algunos recursos de Azure adicionales para la aplicación. Este es un escenario avanzado y requiere que tenga conocimientos básicos del lenguaje bícep que se usa para crear ARM plantilla. You can get started with icep at [bicep documentation](/azure/azure-resource-manager/bicep/?branch).
> [!NOTE]
> Todos los ARM comparten la plantilla de configuración. Puede usar la [implementación condicional si](/azure/azure-resource-manager/bicep/conditional-resource-deployment?branch) el comportamiento de aprovisionamiento es distinto entre entornos.

Para asegurarse de que las herramientas de TeamsFx funcionan correctamente, asegúrese de que su plantilla personalizada ARM cumpla los requisitos siguientes. Si usa otras herramientas para un desarrollo posterior, puede omitir estos requisitos.

* Mantenga la estructura de carpetas y el nombre del archivo sin cambios. La herramienta puede anexar contenido nuevo a los archivos existentes cuando agregue más recursos o capacidades al proyecto.
* Mantenga el nombre de los parámetros generados automáticamente, así como sus nombres de propiedad sin cambios. Los parámetros generados automáticamente pueden usarse al agregar más recursos o capacidades al proyecto.
* Mantenga el resultado de la plantilla generada automáticamente ARM sin cambios. Puede agregar resultados adicionales a ARM plantilla. El resultado se conservará y se usará en otras características como `.fx/states/state.{env}.json` implementar, validar el archivo de manifiesto, etc.

### <a name="customization-scenarios"></a>Escenarios de personalización

Estos son algunos escenarios comunes que puede personalizar el comportamiento de aprovisionamiento.

#### <a name="use-an-existing-aad-app-for-your-teams-app"></a>Usar una aplicación de AAD existente para tu Teams aplicación

Puedes agregar el siguiente fragmento de código de configuración al archivo para usar una aplicación AAD creada por ti mismo `.fx/configs/config.{env}.json` para tu Teams aplicación. Para crear una aplicación AAD, consulta <https://aka.ms/teamsfx-existing-aad-doc> .

```json
"auth": {
    "clientId": "<your AAD app client id>",
    "clientSecret": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}",
    "objectId": "<your AAD app object id>",
    "accessAsUserScopeId": "<id of the access_as_user scope>"
}
```

Después de agregar el fragmento de código anterior, agregue el secreto a la variable de entorno relacionada para que las herramientas puedan resolver el secreto real durante la provisión.

> [!NOTE]
> No debes compartir una aplicación AAD en varios entornos. Si no tienes permiso para actualizar la aplicación AAD, recibirás una advertencia con instrucciones sobre cómo actualizar manualmente la AAD aplicación. Sigue las instrucciones para actualizar la aplicación AAD después de aprovisionar.

#### <a name="use-an-existing-aad-app-for-your-bot"></a>Usar una aplicación de AAD existente para el bot

Puedes agregar el siguiente fragmento de código de configuración al archivo para usar una AAD creada por `.fx/configs/config.{env}.json` ti mismo para el bot.

```json
"bot": {
    "appId": "<your AAD app client id>",
    "appPassword": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}"
}
```

Después de agregar el fragmento de código anterior, agregue el secreto a la variable de entorno relacionada para que las herramientas puedan resolver el secreto real durante la provisión.

> [!NOTE]
> No debes compartir una aplicación AAD en varios entornos.

#### <a name="skip-adding-user-for-sql-database"></a>Omitir agregar usuario para la SQL base de datos

A veces, es posible que reciba un error de permiso insuficiente cuando la herramienta intente agregar un usuario a SQL base de datos. Puede agregar el siguiente fragmento de código de configuración al `.fx/configs/config.{env}.json` archivo para omitir la adición de SQL de base de datos.

```json
"skipAddingSqlUser": true
```

### <a name="specifying-the-name-of-function-app-instance"></a>Especificación del nombre de la instancia de Function App

En este ejemplo, especificaré otro nombre para `contosoteamsappapi` la instancia de Function App en lugar de usar el nombre predeterminado.

> [!NOTE]
> Si ya aprovisionó el entorno, al especificar el nombre, se creará una nueva instancia de Function App, en lugar de cambiar el nombre de la instancia creada anteriormente.

Los siguientes pasos son:

1. Abra `.fx/configs/azure.parameters.{env}.json` para el entorno actual.
2. Agregue una nueva propiedad `functionAppName` al valor del parámetro `provisionParameters` .
3. Rellenar "contosoteamsappapi" como valor de `functionAppName`
4. El archivo de parámetro final se muestra de la siguiente manera:

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

**Para agregar otro recurso de Azure (Azure Storage) a la aplicación**

Tenga en cuenta el escenario, desea agregar una Azure Storage al back-end de función de Azure para almacenar algunos datos de blob. No hay ningún flujo automático para actualizar la plantilla de bícep con Azure Storage compatibilidad. Sin embargo, puede editar el archivo bícep y agregar el recurso. Los pasos son los siguientes

1. Crear un proyecto de pestaña
2. Agregue una función al proyecto. Puede visitar [Agregar recursos para](./add-resource.md) obtener más información sobre cómo agregar recursos.
3. Declare la nueva Storage cuenta en ARM plantilla. Para simplificar, declararemos el recurso `templates/azure/provision/function.bicep` directamente. Puede declarar los recursos en otros lugares.

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

4. Actualice la aplicación de función de Azure Configuración con Azure Storage de conexión en , que `templates/azure/provision/function.bicep` es el mismo archivo del paso 3. Agregue el siguiente fragmento de código `functionApp` a la matriz del `appSettings` recurso.

    ``````````````````bicep
    {
        name: 'MyAppStorageAccountConnectionString'
        value: 'DefaultEndpointsProtocol=https;AccountName=${applicationStorageAccount.name};AccountKey=${listKeys(applicationStorageAccount.id, '2021-06-01').keys[0].value}'
    }
    ```````````````````

5. Ahora puede actualizar la función con Azure Storage enlaces de salida.

## <a name="faq"></a>Preguntas más frecuentes

<br>

<details>

<summary><b>¿Cómo solucionar problemas?</b></summary>

Si ha encontrado errores con Teams Toolkit en Visual Studio Code, puede hacer clic en el botón de la notificación de error para navegar `Get Help` al documento de ayuda relacionado. Si usa la CLI de TeamsFx, habrá un vínculo hiper al final del mensaje de error que apunta al documento de ayuda. También puede ver el [documento de ayuda de aprovisionamiento](https://aka.ms/teamsfx-arm-help) directamente.

<br>

</details>

<details>

<summary><b>¿Cómo puedo cambiar a otra suscripción de Azure durante el aprovisionamiento?</b></summary>

1. Cambie la suscripción en la cuenta actual o cierre la sesión y seleccione una nueva suscripción.
2. Si ya ha aprovisionado el entorno actual, debe crear un nuevo entorno y realizar la provisión porque ARM no admite el movimiento de recursos.
3. Si no aprovisionó el entorno actual, puede desencadenar la provisión directamente.

<br>

</details>

<details>

<summary><b>¿Cómo puedo cambiar el grupo de recursos durante el aprovisionamiento?</b></summary>

Antes de aprovisionar, la herramienta le preguntará si desea crear un nuevo grupo de recursos o usar uno existente. Puede proporcionar un nuevo nombre de grupo de recursos o elegir uno existente en este paso.

<br>

</details>

<details>

<summary><b>¿Cómo puedo aprovisionar SharePoint aplicación basada en aplicaciones?</b></summary>

Puedes seguir [Aprovisionar SharePoint aplicación basada en aplicaciones para](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch) aprovisionar SharePoint basada en aplicaciones.

> [!NOTE]
> Actualmente, la creación de Teams app con SharePoint Framework con Teams Toolkit no tiene integración directa con Azure, el contenido de este documento no se aplica SPFx aplicaciones basadas en SPFx.


<br>

</details>

## <a name="see-also"></a>Consulte también

> [!div class="nextstepaction"]
> [Implementar Teams aplicación en la nube](deploy.md)

> [!div class="nextstepaction"]
> [Administrar varios entornos](TeamsFx-multi-env.md)

> [!div class="nextstepaction"]
> [Colaborar con otros desarrolladores en Teams proyecto](TeamsFx-collaboration.md)

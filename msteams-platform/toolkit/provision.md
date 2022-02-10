---
title: Usar Teams Toolkit para aprovisionar recursos en la nube
author: MuyangAmigo
description: Aprovisionar recursos en la nube
ms.author: shenwe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 6a922c98dc158105abf1225a6f292c95d063428d
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/10/2022
ms.locfileid: "62517963"
---
# <a name="use-teams-toolkit-to-provision-cloud-resources"></a>Usar Teams Toolkit para aprovisionar recursos en la nube

TeamsFx se integra con Azure y Microsoft 365 nube, lo que le permite colocar la aplicación en Azure con un solo comando. TeamsFx se integra con Azure Resource Manager que permite aprovisionar recursos de Azure, que la aplicación necesita para el enfoque de código.  

## <a name="prerequisites"></a>Requisitos previos

* Requisitos previos de la cuenta Para aprovisionar recursos en la nube, debe tener las siguientes cuentas:

    * Microsoft 365 cuenta con suscripción válida
    * Azure con suscripción válida Para obtener más información, vea [cómo preparar cuentas para crear Teams aplicación](accounts.md).

* [Instale Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión 3.0.0+.

> [!TIP]
> Asegúrate de que tienes Teams proyecto de aplicación abierto en código VS.

## <a name="provision-using-teams-toolkit"></a>Aprovisionar mediante Teams Toolkit

La aprovisionamiento se realiza con un solo comando en Teams Toolkit para Visual Studio Code o CLI de TeamsFx de la siguiente manera:

[Aprovisionar aplicación basada en Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)

## <a name="resource-creation"></a>Creación de recursos

Al desencadenar el comando de aprovisionamiento en Teams Toolkit CLI de TeamsFx, puede obtener los siguientes recursos:

* Microsoft Azure Active Directory (Azure AD) bajo el inquilino Microsoft 365 usuario
* Teams registro de la aplicación en la Microsoft 365 de la plataforma de Teams inquilino
* Recursos de Azure en la suscripción de Azure seleccionada

Al crear un nuevo proyecto, puede usar todos los recursos de Azure. La ARM define todos los recursos de Azure y ayuda a crear los recursos de Azure necesarios durante la provisión. Al agregar [un nuevo recurso de funcionalidad](./add-resource.md) a un proyecto existente, la plantilla de ARM actualizada refleja el cambio más reciente.

> [!NOTE]
> Los servicios de Azure incurren en costos en la suscripción, para obtener más información sobre la estimación de costos, consulte [la calculadora de precios](https://azure.microsoft.com/pricing/calculator/).

### <a name="resource-creation-for-teams-tab-application"></a>Creación de recursos para Teams tab

|Recurso|Objetivo|Descripción |
|----------|--------------------------------|-----|
| Almacenamiento de Azure | Hospedar la aplicación de pestaña | Habilita la característica de aplicación web estática para hospedar la aplicación de pestañas |
| Plan de app service para autenticación sencilla | Hospedar la aplicación web de Simple Auth |No aplicable |
| Aplicación web para autenticación sencilla | Host simple auth server to gain access to other services in your single page application | Agrega identidad asignada al usuario para obtener acceso a otros recursos de Azure |
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure | Compartido entre diferentes capacidades y recursos |

### <a name="resource-creation-for-teams-bot-or-messaging-extension-application"></a>Creación de recursos para Teams bot o aplicación de extensión de mensajería

|Recurso|Objetivo| Descripción |
|----------|--------------------------------|-----|
| Servicio de bots de Azure | Registra la aplicación como un bot con el marco del bot | Conecta el bot a Teams |
| Plan de servicio de aplicaciones para bot | Hospedar la aplicación web del bot |No aplicable |
| Aplicación web para bot | Hospedar la aplicación bot | Agrega la identidad asignada por el usuario para obtener acceso a otros recursos de Azure. <br /> Agrega la configuración de la aplicación requerida [por el SDK de TeamsFx](https://www.npmjs.com/package/@microsoft/teamsfx) |
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure | Compartido entre diferentes capacidades y recursos |

### <a name="resource-creation-for-azure-functions-in-the-project"></a>Creación de recursos para Azure Functions en el proyecto

|Recurso|Objetivo| Descripción|
|----------|--------------------------------|-----|
| Plan de servicio de aplicaciones para la aplicación de función | Hospedar la aplicación de función |No aplicable |
| Aplicación function | Hospedar las API de funciones de Azure | Agrega la identidad asignada por el usuario para obtener acceso a otros recursos de Azure. <br /> Agrega una regla de uso compartido de recursos entre orígenes (CORS) para permitir solicitudes desde la aplicación de pestañas <br /> Agrega la configuración de autenticación que solo permite las solicitudes de Teams aplicación. <br /> Agrega la configuración de la aplicación requerida [por el SDK de TeamsFx](https://www.npmjs.com/package/@microsoft/teamsfx) |
| Azure Storage para la aplicación de función | Necesario para crear una aplicación de función |No aplicable|
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure | Compartido entre diferentes capacidades y recursos |

### <a name="resource-creation-for-azure-sql-in-the-project"></a>Creación de recursos para Azure SQL en el proyecto

|Recurso|Objetivo | Descripción |
|----------|--------------------------------|-----|
| Servidor SQL Azure | Hospedar la instancia de base de SQL azure | Permite que todos los servicios de Azure accedan al servidor |
| Base de datos SQL Azure | Almacenar datos para la aplicación | Concede al usuario permiso de identidad asignada, lectura o escritura en la base de datos |
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure | Compartido entre diferentes capacidades y recursos |

### <a name="resource-creation-for-azure-api-management-in-the-project"></a>Creación de recursos para Azure API Management en el proyecto

|Recurso|Objetivo|
|----------|--------------------------------|
| Microsoft Azure Active Directory (Azure AD) para el servicio de administración de API | Permite a las API de acceso de Microsoft Power Platform administradas por el servicio de administración de API |
| Servicio de administración de API | Administrar las API hospedadas en la aplicación de función |
| Producto de administración de API | Agrupar las API, definir términos de uso y directivas de tiempo de ejecución |
| Servidor OAuth de administración de API | Permite que Microsoft Power Platform acceda a las API hospedadas en la aplicación de función |
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure |

### <a name="resources-created-when-including-azure-key-vault-in-the-project"></a>Recursos creados al incluir Azure Key Vault en el proyecto

|Recursos|Finalidad de este recurso|
|----------|--------------------------------|
| Servicio de Azure Key Vault | Administrar secretos (por ejemplo, el secreto de cliente Microsoft Azure Active Directory (Azure AD) de aplicaciones) usado por otros servicios de Azure |
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure |

## <a name="customize-resource-provision"></a>Personalizar la provisión de recursos

Teams Toolkit permite usar una infraestructura como método de código para definir qué recursos de Azure desea aprovisionar y cómo desea configurar. La herramienta usa ARM plantilla para definir recursos de Azure. La ARM es un conjunto de archivos bíceps que define la infraestructura y la configuración del proyecto. Puede personalizar los recursos de Azure modificando la ARM plantilla. Para obtener más información, vea [documento bícep](/azure/azure-resource-manager/bicep.md). 

Aprovisionar con ARM implica cambiar los siguientes conjuntos de archivos, parámetros y plantillas:

* ARM de parámetros (`azure.parameters.{your_env_name}.json`) ubicados en la `.fx/configs` carpeta, para pasar parámetros a plantillas.
* ARM archivos de plantilla ubicados en `templates/azure`, esta carpeta contiene los siguientes archivos:

| Archivo | Función | Permitir la personalización |
| --- | --- | --- |
| main.bicep | Proporcionar punto de entrada para la provisión de recursos de Azure | Sí |
| provision.bicep | Crear y configurar recursos de Azure | Sí |
| config.bicep | Agregar configuraciones necesarias de TeamsFx a recursos de Azure | Sí |
| provision/xxx.bicep | Crear y configurar cada recurso de Azure consumido por `provision.bicep` | Sí |
| teamsfx/xxx.bicep | Agregar configuraciones necesarias de TeamsFx a cada recurso de Azure consumido por `config.bicep`| No |

> [!NOTE]
> Al agregar recursos o capacidades al proyecto, `teamsfx/xxx.bicep` se regenerará, no se puede personalizar lo mismo. Para modificar los archivos bíceps, puedes usar Git `teamsfx/xxx.bicep` para realizar un seguimiento de los cambios en los archivos, lo que te ayuda a no perder los cambios al agregar recursos o funcionalidades.

### <a name="customize-arm-parameters-and-templates"></a>Personalizar ARM parámetros y plantillas

Puede personalizar los recursos de Azure personalizando los archivos de parámetros y personalizando los archivos bíceps.

#### <a name="customize-arm-template-parameter-files"></a>Personalizar ARM de parámetros de plantilla

El kit de herramientas proporciona un conjunto de parámetros predefinidos para personalizar los recursos de Azure. Los archivos de parámetros se encuentran en `.fx/configs/azure.parameters.{env}.json` y todos los parámetros disponibles se definen en la `provisionParameters` propiedad. Se recomienda personalizar los archivos de parámetros si los parámetros predefinidos satisfacen sus requisitos.

En la tabla siguiente se proporciona una lista de parámetros predefinidos disponibles:

| Nombre del parámetro | Valor predeterminado | Qué puede personalizar el parámetro | Restricciones de valor |
| --- | --- | --- | --- |
| resourceBaseName | Generado automáticamente para cada entorno | Nombre predeterminado para todos los recursos | 2-20 minúsculas y números |
| simpleAuthServerFarmsName | ${resourceBaseName}simpleAuth | Nombre del plan de servicio de aplicaciones de autenticación simple | 1-40 alfanuméricos y guiones |
| simpleAuthWebAppName | ${resourceBaseName}simpleAuth | Nombre de la aplicación web de autenticación simple | 2-60 alfanuméricos y guiones <br /> No se puede iniciar ni terminar con guion |
| simpleAuthSku | F1 | SKU del plan de servicio de aplicaciones de autenticación simple | No aplicable |
| frontendHostingStorageName | Ficha ${resourceBaseName} | Nombre de la cuenta de almacenamiento de hospedaje front-end | 3-24 minúsculas y números |
| frontendHostingStorageSku | Standard_LRS | SKU de la cuenta de almacenamiento de hospedaje front-end |[SKU disponibles](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep&branch)|
| functionServerfarmsName | ${resourceBaseName}api | Nombre del plan de servicio de aplicaciones de función | 1-40 alfanuméricos y guiones |
| functionServerfarmsSku | Y1 | SKU del plan de servicio de aplicaciones de función | No aplicable|
| functionAppName | ${resourceBaseName}api | Nombre de la aplicación de función | 2-60 alfanuméricos y guiones <br /> No se puede iniciar ni terminar con guion |
| functionStorageName | ${resourceBaseName}api | Nombre de la cuenta de almacenamiento de la aplicación de función | 3-24 minúsculas y números |
| functionStorageSku | Standard_LRS | SKU de la cuenta de almacenamiento de la aplicación de función | [SKU disponibles](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep&branch=pr-en-us-4713) |
| botServiceName | ${resourceBaseName} | Nombre del servicio de bots de Azure | 2-64 alfanuméricos, guiones bajos, puntos y guiones <br /> Empezar por alfanumérico |
| botServiceSku | F0 | SKU del servicio de bots de Azure | [SKU disponibles](/azure/templates/microsoft.botservice/2021-05-01-preview/botservices?tabs=bicep&branch) |
| botDisplayName | ${resourceBaseName} | Nombre para mostrar del bot | De 1 a 42 caracteres |
| botServerfarmsName | Bot ${resourceBaseName} | Nombre del plan de servicio de aplicaciones del bot | 1-40 alfanuméricos y guiones |
| botWebAppName | Bot ${resourceBaseName} | Nombre de la aplicación web del bot | 2-60 alfanuméricos y guiones <br /> No se puede iniciar ni terminar con guion |
| botWebAppSKU | F1 | SKU de Bot App Service Plan | No aplicable |
| userAssignedIdentityName | ${resourceBaseName} | Nombre de la identidad asignada por el usuario | 3-128 alfanuméricos, guiones y guiones bajos <br /> Empezar con letra o número |
| sqlServerName | ${resourceBaseName} | Nombre del servidor SQL Azure | 1-63 minúsculas, números y guiones <br /> No se puede iniciar ni terminar con guión |
| sqlDatabaseName | ${resourceBaseName} | Nombre de la base de datos SQL Azure | De 1 a 128 caracteres, no se puede usar <>*%&:\/? o caracteres de control <br /> No se puede terminar con punto o espacio |
| sqlDatabaseSku | Básico | SKU de azure SQL base de datos | No aplicable  |
| apimServiceName | ${resourceBaseName} | Nombre del servicio APIM | 1-50 alfanuméricos y guiones <br /> Comience por letra y termine con alfanumérico |
| apimServiceSku | Consumo | SKU del servicio APIM | [SKU disponibles](/azure/templates/microsoft.apimanagement/service?tabs=bicep&branch) |
| apimProductName | ${resourceBaseName} | Nombre del producto APIM | 1-80 alfanuméricos y guiones <br /> Comience por letra y termine con alfanumérico |
| apimOauthServerName | ${resourceBaseName} | Nombre del servidor OAuth de APIM | 1-80 alfanuméricos y guiones <br /> Comience por letra y termine con alfanumérico |
| keyVaultSkuName | estándar | Nombre sku del servicio de Almacén de claves de Azure| |

Mientras tanto, los siguientes parámetros están disponibles con valores rellenados durante la provisión. El propósito de estos marcadores de posición es garantizar que podamos crear nuevos recursos en un entorno nuevo. Los valores reales se resuelven desde `.fx/states/state.{env}.json`.

##### <a name="azure-ad-application-related-parameters"></a>Azure AD parámetros relacionados con la aplicación

| Nombre del parámetro | Soporte de posición de valor predeterminado | Significado del soporte de la posición | Cómo personalizar |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | El identificador de cliente de Azure AD la aplicación creada durante la aprovisionamiento | [Personalizar el valor](#use-an-existing-azure-ad-app-for-your-teams-app) |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | Secreto de cliente de aplicación Azure AD la aplicación creada durante la provisión | [Personalizar el valor](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | Identificador de inquilino de la aplicación Azure AD aplicación | [Personalizar el valor](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 OAuthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | Host de autoridad de OAuth de la aplicación Azure AD aplicación | [Personalizar el valor](#use-an-existing-azure-ad-app-for-your-teams-app) |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | Identificador de cliente de Azure AD de aplicación de bot creado durante la provisión | [Personalizar el valor](#use-an-existing-azure-ad-app-for-your-bot) |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | Secreto de cliente de Azure AD de aplicación de bot creado durante la provisión | [Personalizar el valor](#use-an-existing-azure-ad-app-for-your-bot) |
| apimClientId | {{state.fx-resource-apim.apimClientAADClientId}} | Identificador de cliente de Azure AD apim creado durante la provisión | Eliminar el marcador de posición y rellenar el valor real |
| apimClientSecret | {{state.fx-resource-apim.apimClientAADClientSecret}} | Secreto de cliente de Azure AD apim creado durante la provisión | Eliminar el marcador de posición y rellenar el valor real |

##### <a name="azure-resource-related-parameters"></a>Parámetros relacionados con recursos de Azure

| Nombre del parámetro | Soporte de posición de valor predeterminado | Significado del soporte de la posición | Cómo personalizar |
| --- | --- | --- | --- |
| azureSqlAdmin | {{state.fx-resource-azure-sql.admin}} | Cuenta SQL Server administrador de Azure que proporcionó durante la aprovisionamiento | Eliminar el marcador de posición y rellenar el valor real |
| azureSqlAdminPassword | {{state.fx-resource-azure-sql.adminPassword}} | Contraseña SQL Server administrador de Azure que proporcionó durante la provisión | Eliminar el marcador de posición y rellenar el valor real |
| apimPublisherEmail | {{state.fx-resource-apim.publisherEmail}} | Correo electrónico del editor de APIM, el valor predeterminado es su cuenta de Azure | Eliminar el marcador de posición y rellenar el valor real |
| apimPublisherName | {{state.fx-resource-apim.publisherName}} | Nombre del editor de APIM, el valor predeterminado es su cuenta de Azure | Eliminar el marcador de posición y rellenar el valor real |

#### <a name="referencing-environment-variables-in-parameter-files"></a>Referencia a variables de entorno en archivos de parámetros

Si no desea codificar los valores de los archivos de parámetros, por ejemplo, cuando el valor es un secreto. Los archivos de parámetros admiten hacer referencia a los valores de las variables de entorno. Puede usar la sintaxis en `{{$env.YOUR_ENV_VARIABLE_NAME}}` los valores de parámetro para que la herramienta se resuelva desde la variable de entorno actual.

En el ejemplo siguiente se lee el valor del parámetro `mySelfHostedDbConnectionString` de la variable de entorno `DB_CONNECTION_STRING`:

```json
...
    "mySelfHostedDbConnectionString": "{{$env.DB_CONNECTION_STRING}}"
...
```

#### <a name="customize-arm-template-files"></a>Personalizar ARM de plantilla

Si las plantillas predefinidas no cumplen los requisitos de la aplicación, puede personalizar las plantillas ARM en la `templates/azure` carpeta. Por ejemplo, puedes personalizar la plantilla ARM para crear algunos recursos de Azure adicionales para la aplicación. Debe tener conocimientos básicos del idioma bícep, que se usa para crear ARM plantilla. Puede empezar con el bícep en la [documentación del bícep](/azure/azure-resource-manager/bicep/?branch).

> [!NOTE]
> Todos los ARM comparten la plantilla de configuración. Puede usar la [implementación condicional si](/azure/azure-resource-manager/bicep/conditional-resource-deployment?branch) el comportamiento de aprovisionamiento varía entre entornos.

Para garantizar que la herramienta TeamsFx funciona correctamente, asegúrese de personalizar ARM plantilla, lo que satisface los siguientes requisitos. Si usa otra herramienta para el desarrollo posterior, puede omitir estos requisitos.

* Mantenga la estructura de carpetas y el nombre del archivo sin cambios. La herramienta puede anexar contenido nuevo a los archivos existentes al agregar más recursos o funcionalidades al proyecto.
* Mantenga el nombre de los parámetros generados automáticamente, así como sus nombres de propiedad sin cambios. Los parámetros generados automáticamente pueden usarse al agregar más recursos o funcionalidades al proyecto.
* Mantenga el resultado de la plantilla generada automáticamente ARM sin cambios. Puede agregar resultados adicionales a ARM plantilla. El resultado es `.fx/states/state.{env}.json` y se puede usar en otras características, como implementar, validar el archivo de manifiesto.

### <a name="customization-scenarios"></a>Escenarios de personalización

Puede personalizar los siguientes escenarios:

#### <a name="use-an-existing-azure-ad-app-for-your-bot"></a>Usar una aplicación de Azure AD existente para el bot

Puedes agregar el siguiente fragmento de código `.fx/configs/config.{env}.json` de configuración al archivo para usar una aplicación Microsoft Azure Active Directory (Azure AD) creada por ti mismo para tu Teams aplicación. Para crear una aplicación Microsoft Azure Active Directory (Azure AD), consulta <https://aka.ms/teamsfx-existing-aad-doc>.

```json
"auth": {
    "clientId": "<your Azure AD app client id>",
    "clientSecret": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}",
    "objectId": "<your Azure AD app object id>",
    "accessAsUserScopeId": "<id of the access_as_user scope>"
}
```

Después de agregar el fragmento de código, agregue el secreto a la variable de entorno relacionada para que la herramienta pueda resolver el secreto real durante la provisión.

> [!NOTE]
> Asegúrate de no compartir la misma Microsoft Azure Active Directory (Azure AD) en varios entornos. Si no tienes permiso para actualizar la aplicación Microsoft Azure Active Directory (Azure AD), puedes obtener una advertencia con instrucciones sobre cómo actualizar manualmente la aplicación Microsoft Azure Active Directory (Azure AD). Sigue las instrucciones para actualizar la aplicación Microsoft Azure Active Directory (Azure AD) después de aprovisionar.

#### <a name="use-an-existing-azure-ad-app-for-your-teams-app"></a>Usar una aplicación de Azure AD existente para tu Teams aplicación

Puedes agregar el siguiente fragmento de código de `.fx/configs/config.{env}.json` configuración al archivo para usar una aplicación Microsoft Azure Active Directory (Azure AD) creada por ti mismo para el bot:

```json
"bot": {
    "appId": "<your Azure AD app client id>",
    "appPassword": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}"
}
```

Después de agregar el fragmento de código anterior, agrega el secreto a la variable de entorno relacionada para que la herramienta resuelva el secreto real durante la provisión.

#### <a name="skip-adding-user-for-sql-database"></a>Omitir agregar usuario para la SQL base de datos

Si no tiene un error de permiso insuficiente cuando la herramienta intenta agregar un usuario SQL una base de datos, `.fx/configs/config.{env}.json` puede agregar el siguiente fragmento de código de configuración al archivo para omitir la adición de SQL de base de datos:

```json
"skipAddingSqlUser": true
```

### <a name="specifying-the-name-of-function-app-instance"></a>Especificación del nombre de la instancia de Function App

Puedes usar para la `contosoteamsappapi` instancia de la aplicación de función en lugar de usar el nombre predeterminado.

> [!NOTE]
> Si ya ha aprovisionado el entorno, especificar el nombre puede crear una nueva instancia de aplicación de función, en lugar de cambiar el nombre de la instancia creada anteriormente.

Los siguientes pasos son:

1. Abra `.fx/configs/azure.parameters.{env}.json` para el entorno actual.
2. Agregue una nueva propiedad `functionAppName` al valor del parámetro `provisionParameters`.
3. Escriba `contosoteamsappapi` como valor de `functionAppName`
4. El archivo de parámetro final se muestra en el siguiente fragmento de código:

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

**Para agregar otro recurso o almacenamiento de Azure a la aplicación**

Tenga en cuenta el escenario, desea agregar Azure Storage al back-end de la función de Azure para almacenar datos de blobs. No hay ningún flujo automático para actualizar la plantilla de bícep con compatibilidad con Azure Storage. Sin embargo, puede editar el archivo bícep y agregar el recurso. Los pasos son los siguientes:

1. Crear un proyecto de pestaña.
2. Agregue la función al proyecto. Para obtener más información, vea [Agregar recursos](./add-resource.md).
3. Declare la nueva cuenta de almacenamiento en ARM plantilla. Puede declarar el recurso directamente `templates/azure/provision/function.bicep` . Puede declarar los recursos en otros lugares.

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

4. Actualice la configuración de la aplicación de función de Azure con la cadena de conexión de Azure Storage en `templates/azure/provision/function.bicep`. Agregue el siguiente fragmento de código a `functionApp` la matriz del `appSettings` recurso:

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

Si obtiene errores con Teams Toolkit en Visual Studio Code, puede seleccionar Obtener ayuda en la notificación de error para navegar  al documento relacionado. Si usa la CLI de TeamsFx, habrá un hipervínculo al final del mensaje de error que apunta al documento de ayuda. También puede ver el [documento de ayuda de aprovisionamiento](https://aka.ms/teamsfx-arm-help) directamente.

<br>

</details>

<details>

<summary><b>¿Cómo puedo cambiar a otra suscripción de Azure durante el aprovisionamiento?</b></summary>

1. Cambie la suscripción en la cuenta actual o cierre la sesión y seleccione una nueva suscripción.
2. Si ya ha aprovisionado el entorno actual, debe crear un nuevo entorno y realizar la aprovisionamiento porque ARM no admite el movimiento de recursos.
3. Si no aprovisionó el entorno actual, puede desencadenar la provisión directamente.

<br>

</details>

<details>

<summary><b>¿Cómo puedo cambiar el grupo de recursos durante el aprovisionamiento?</b></summary>

Antes de aprovisionar, la herramienta le preguntará si desea crear un nuevo grupo de recursos o usar uno existente. Puede proporcionar un nuevo nombre de grupo de recursos o elegir uno existente en este paso.

<br>

</details>

<details>

<summary><b>¿Cómo puedo aprovisionar una aplicación basada en SharePoint?</b></summary>

Puedes seguir la [aprovisionamiento SharePoint aplicación basada en aplicaciones](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch).

> [!NOTE]
> Actualmente, la aplicación de creación Teams con sharepoint framework con Teams Toolkit no tiene integración directa con Azure, el contenido del documento no se aplica SPFx aplicaciones basadas en SPFx.


<br>

</details>

## <a name="see-also"></a>Vea también

* [Implementar la aplicación de Teams en la nube](deploy.md)
* [Administrar varios entornos](TeamsFx-multi-env.md)
* [Colaborar con otros desarrolladores en Teams proyecto](TeamsFx-collaboration.md)

---
title: usar el kit de herramientas de Teams para aprovisionar recursos en la nube
author: MuyangAmigo
description: En este módulo, aprenderá a aprovisionar recursos en la nube mediante el kit de herramientas de Teams, a crear y personalizar el aprovisionamiento de recursos.
ms.author: shenwe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 175854db36b85a1fc68cc299bd733b7abd539ac9
ms.sourcegitcommit: de7496f9586316bed12d115cd3e4c18ba0854d4f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2022
ms.locfileid: "67780989"
---
# <a name="provision-cloud-resources"></a>Aprovisionar recursos en la nube

TeamsFx se integra con Azure y la nube de Microsoft 365, lo que le permite colocar la aplicación en Azure con un solo comando. TeamsFx se integra con Azure Resource Manager que le permite aprovisionar los recursos de Azure que su aplicación necesita para el enfoque de código.

::: zone pivot="visual-studio-code"

## <a name="provision-using-teams-toolkit-in-visual-studio-code"></a>Aprovisionamiento mediante el kit de herramientas de Teams en Visual Studio Code

El aprovisionamiento se realiza con un solo comando en Teams Toolkit para Visual Studio Code o la CLI de TeamsFx. Para obtener más información, consulte [Aprovisionamiento de una aplicación basada en Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8).

## <a name="create-resources"></a>Creación de recursos

Al desencadenar el comando de aprovisionamiento en el kit de herramientas de Teams o la CLI de TeamsFx, puede obtener los siguientes recursos:

* Microsoft Azure Active Directory aplicación (Azure AD) en el inquilino de Microsoft 365.
* Registro de aplicaciones de Teams en la plataforma de Teams del inquilino de Microsoft 365.
* Recursos de Azure en la suscripción de Azure seleccionada.

Al crear un nuevo proyecto, puede usar todos los recursos de Azure. La plantilla de ARM define todos los recursos de Azure y ayuda a crear los recursos de Azure necesarios durante el aprovisionamiento. Al [añadir nuevos recursos de funcionalidad](./add-resource.md) a un proyecto existente, la plantilla de ARM actualizada refleja el cambio más reciente.

> [!NOTE]
> Los servicios de Azure incurren en costes en su suscripción. Para obtener más información sobre la estimación de costes, consulte [la calculadora de precios](https://azure.microsoft.com/pricing/calculator/).

En la lista siguiente se muestra la creación de recursos para diferentes tipos de recursos de aplicación y azure:
<br>

<details>
<summary><b>Creación de recursos para aplicaciones de pestaña de Teams</b></summary>

|Resource|Objetivo|Descripción |
|----------|--------------------------------|-----|
| Azure Storage | Alojar su aplicación de pestaña | Habilita la característica de aplicación web estática para alojar la aplicación de pestaña |
| Plan de servicio de aplicación para autenticación simple | Alojar la aplicación web de autenticación simple |No aplicable |
| Aplicación web para autenticación simple | Alojar un servidor de autenticación simple para obtener acceso a otros servicios en su aplicación de página única | Añade la identidad asignada por el usuario para acceder a otros recursos de Azure |
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure | Compartido entre diferentes funcionalidades y recursos |

</details>
<br>

<details>
<summary><b>Creación de recursos para aplicación de extensión de mensaje o bot de Teams</b></summary>

|Resource|Objetivo| Descripción |
|----------|--------------------------------|-----|
| Servicio de bot de Azure | Registra su aplicación como bot con Bot Framework | Conecta el bot a Teams |
| Plan de servicio de aplicación para el bot | Alojar la aplicación web del bot |No aplicable |
| Aplicación web para el bot | Alojar la aplicación de bot | Añade la identidad asignada por el usuario para acceder a otros recursos de Azure. <br /> Añade la configuración de la aplicación requerida por el [SDK de TeamsFx](https://www.npmjs.com/package/@microsoft/teamsfx). |
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure | Compartido entre diferentes funcionalidades y recursos |

</details>
<br>

<details>
<summary><b>Creación de recursos para Azure Functions en el proyecto</b></summary>

|Resource|Objetivo| Descripción|
|----------|--------------------------------|-----|
| Plan de servicio para aplicación de funciones | Alojar la aplicación de funciones |No aplicable |
| Aplicación de funciones | Alojar las API de funciones de Azure | Añade la identidad asignada por el usuario para acceder a otros recursos de Azure. <br /> Añade una regla de uso compartido de recursos entre orígenes (CORS) para permitir solicitudes desde su aplicación de pestaña <br /> Añade la configuración de autenticación que solo permite las solicitudes de su aplicación de Teams. <br /> Añade la configuración de la aplicación requerida por el [SDK de TeamsFx](https://www.npmjs.com/package/@microsoft/teamsfx). |
| Almacenamiento de Azure para la aplicación de funciones | Necesario para crear una aplicación de funciones |No aplicable|
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure | Compartido entre diferentes funcionalidades y recursos |

</details>
<br>

<details>
<summary><b>Creación de recursos para Azure SQL en el proyecto</b></summary>

|Resource|Objetivo | Descripción |
|----------|--------------------------------|-----|
| Servidor de Azure SQL | Alojar la instancia de base de datos Azure SQL | Permite que todos los servicios de Azure accedan al servidor |
| Base de datos SQL Azure | Almacenar datos para la aplicación | Concede permisos de lectura o escritura en la base de datos a la identidad asignada por el usuario |
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure | Compartido entre diferentes funcionalidades y recursos |

</details>
<br>

<details>
<summary><b>Creación de recursos para Azure API Management en el proyecto</b></summary>

|Resource|Objetivo|
|----------|--------------------------------|
| Aplicación Azure AD para el servicio de administración de API | Permite a Microsoft Power Platform acceder a las API administradas por el servicio de administración de API |
| Servicio de administración de API | Administrar las API alojadas en la aplicación de funciones |
| Producto de administración de API | Agrupar las API, definir términos de uso y directivas en tiempo de ejecución |
| Servidor OAuth de administración de API | Permite a Microsoft Power Platform acceder a las API alojadas en la aplicación de funciones |
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure |

</details>
<br>

<details>
<summary><b>Recursos creados al incluir Azure Key Vault en el proyecto</b></summary>

|Recursos|Propósito de este recurso|
|----------|--------------------------------|
| Servicio Azure Key Vault | Administrar secretos (por ejemplo, secreto de cliente de aplicación Azure AD) que usan otros servicios de Azure |
| Identidad asignada por el usuario | Autenticar solicitudes de servicio a servicio de Azure |

</details>
<br>

## <a name="customize-resource-provision"></a>Personalización del aprovisionamiento de recursos

Teams Toolkit le permite usar un enfoque de infraestructura como código para definir los recursos de Azure que desea aprovisionar y cómo desea configurar. La herramienta usa la plantilla de ARM para definir recursos de Azure. La plantilla de ARM es un conjunto de archivos bicep que define la infraestructura y configuración del proyecto. Puede personalizar los recursos de Azure modificando la plantilla de ARM. Para obtener más información, consulte la [documentación de bicep](/azure/azure-resource-manager/bicep).

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

### <a name="azure-ad-parameters"></a>Parámetros de Azure AD

Los archivos de plantilla de ARM usan marcadores de posición para los parámetros. El propósito de estos marcadores de posición es garantizar la creación de nuevos recursos en un nuevo entorno. Los valores reales se resuelven a partir de `.fx/states/state.{env}.json`.

Hay dos tipos de parámetros, como los parámetros relacionados con la aplicación de Azure AD y los parámetros relacionados con los recursos de Azure.

##### <a name="azure-ad-application-related-parameters"></a>Parámetros relacionados con la aplicación de Azure AD

| Nombre del parámetro | Marcador de posición de valor predeterminado | Significado del marcador de posición | Cómo personalizar |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | Id. de cliente de la aplicación de Azure AD creada durante el aprovisionamiento | [Uso de una aplicación existente de Azure AD para el bot](#use-an-existing-azure-ad-app-for-your-bot) |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | Secreto de cliente de la aplicación Azure AD creado durante el aprovisionamiento | [Uso de una aplicación de Azure AD existente para la aplicación de Teams](#use-an-existing-azure-ad-app-for-your-teams-app) |
| Microsoft 365 TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | Identificador de inquilino de la aplicación de Azure AD | [Uso de una aplicación de Azure AD existente para la aplicación de Teams](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 OAuthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | Host de autoridad OAuth de la aplicación de Azure AD | [Uso de una aplicación de Azure AD existente para la aplicación de Teams](#use-an-existing-azure-ad-app-for-your-teams-app) |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | Id. de cliente de la aplicación de Azure AD del bot creada durante el aprovisionamiento | [Uso de una aplicación existente de Azure AD para el bot](#use-an-existing-azure-ad-app-for-your-bot) |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | Secreto de cliente de la aplicación de Azure AD del bot creado durante el aprovisionamiento | [Uso de una aplicación existente de Azure AD para el bot](#use-an-existing-azure-ad-app-for-your-bot) |

##### <a name="azure-resource-related-parameters"></a>Parámetros de Azure relacionados con recursos

| Nombre del parámetro | Marcador de posición de valor predeterminado | Significado del marcador de posición | Cómo personalizar |
| --- | --- | --- | --- |
| azureSqlAdmin | {{state.fx-resource-azure-sql.admin}} | Cuenta de administrador de Azure SQL Server que proporcionó durante el aprovisionamiento | Elimine el marcador de posición y rellene con el valor real |
| azureSqlAdminPassword | {{state.fx-resource-azure-sql.adminPassword}} | Contraseña de administrador de Azure SQL Server que proporcionó durante el aprovisionamiento | Elimine el marcador de posición y rellene con el valor real |

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
2. Agregue una nueva propiedad, por ejemplo, `functionAppName` en la `provisionParameters` sección .
3. Escriba un valor de `functionAppName`, por ejemplo `contosoteamsappapi`.
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

Para añadir otro recurso o almacenamiento de Azure a la aplicación:

Imagine la siguiente situación:

Quiere agregar Azure Storage al back-end de la función de Azure para almacenar datos de blobs. No hay ningún flujo automático para actualizar la plantilla bicep con compatibilidad con el almacenamiento de Azure. Sin embargo, puede editar el archivo bicep y añadir el recurso. Los pasos son los siguientes:

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

::: zone-end

::: zone pivot="visual-studio"

## <a name="provision-using-teams-toolkit-in-visual-studio"></a>Aprovisionamiento mediante el kit de herramientas de Teams en Visual Studio

Los pasos siguientes le ayudan a aprovisionar recursos en la nube mediante Visual Studio:

### <a name="sign-in-to-your-microsoft-365-account"></a>Inicio de sesión en su cuenta de Microsoft 365

1. Abra Visual Studio 2022.
1. Abra el proyecto de aplicación de Microsoft Teams.
1. Seleccione **Project** > **Teams Toolkit** > **Prepare Teams App Dependencies (Preparar dependencias de aplicaciones de Teams**).

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-prepare-app-dependencies1.png" alt-text="Preparación de dependencias de aplicaciones de Teams":::

1. Seleccione **Iniciar sesión** para iniciar sesión en su cuenta de Azure.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-prepare1.png" alt-text="Iniciar sesión en Microsoft 365":::

    > [!NOTE]
    > Si ya ha iniciado sesión, se muestra el nombre de usuario o puede seleccionar el mismo para cambiar su cuenta.

1. Se abre el explorador web predeterminado para permitirle [iniciar sesión en](https://developer.microsoft.com/en-us/microsoft-365/dev-program) la cuenta.

1. Seleccione **Continuar** después de haber iniciado sesión en su cuenta.

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-signin-M365.png" alt-text="Para confirmar, seleccione Continuar.":::

### <a name="sign-in-to-your-azure-account"></a>Inicio de sesión en su cuenta de Azure

1. Abra Visual Studio 2022.
1. Abra el proyecto Aplicación de Teams.
1. Seleccione Project **Teams Toolkit****Provision in the cloud (Aprovisionamiento del** kit  >  de herramientas de **Project** >  Teams en la nube).

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-in-cloud2.png" alt-text="Inicio de sesión en la cuenta de Azure":::

1. Seleccione **Iniciar sesión...** para iniciar sesión en su cuenta de Azure.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-start.png" alt-text="Inicio de sesión en su cuenta de Azure":::

   > [!NOTE]
   > Si ya ha iniciado sesión, se muestra el nombre de usuario o tiene la opción de cambiar de cuenta.

   Después de iniciar sesión en la cuenta de Azure con sus credenciales, el explorador se cierra automáticamente.

### <a name="to-provision-cloud-resources"></a>Para aprovisionar recursos en la nube

Después de abrir el proyecto en Visual Studio:

1. Seleccione Project **Teams Toolkit****Provision in the cloud (Aprovisionamiento del** kit  >  de herramientas de **Project** >  Teams en la nube).

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-in-cloud2.png" alt-text="Aprovisionamiento en la nube":::

   Aparece **la ventana Aprovisionar** .

1. Escriba los detalles siguientes para aprovisionar los recursos.

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-select-subscription1.png" alt-text="Seleccionar grupo de recursos":::

   1. Seleccione el **nombre** de la suscripción en la lista desplegable.
   1. Seleccione el **Grupo de recursos** en la lista desplegable.
   1. Seleccione la **región en** la lista desplegable.

      > [!NOTE]
      > Para crear un nuevo grupo de recursos, seleccione **Nuevo**.

   1. Seleccione **Aprovisionar**.

1. El cuadro de diálogo aparece mencionando que los cargos se pueden agregar según el uso de Azure. Seleccione **Aprovisionar**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-warning.png" alt-text="Advertencia de aprovisionamiento":::

   El proceso de aprovisionamiento crea recursos en la nube de Azure. Puede supervisar el progreso observando la ventana de salida del kit de herramientas de Teams.

1. Se le pedirá una vez completado el aprovisionamiento. Seleccione **Ver recursos aprovisionados** para ver todos los recursos aprovisionados.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-provision-success.png" alt-text="Visualización de recursos aprovisionados":::

## <a name="create-resources"></a>Creación de recursos

Al desencadenar el comando de aprovisionamiento en Teams Toolkit o la CLI de TeamsFx, puede crear los siguientes recursos:

* Microsoft Azure Active Directory aplicación (Azure AD) en el inquilino de Microsoft 365.
* Registro de aplicaciones de Teams en la plataforma de Teams del inquilino de Microsoft 365.
* Recursos de Azure en la suscripción de Azure seleccionada.

Al crear un nuevo proyecto, también debe crear recursos de Azure. Las plantillas de Azure Resource Manager (ARM) definen todos los recursos de Azure y le ayudan a crear los recursos de Azure necesarios durante el aprovisionamiento.

En la lista siguiente se muestra la creación de recursos para diferentes tipos de recursos de aplicación y azure:
<br>

<details>
<summary><b>Creación de recursos para aplicaciones de pestaña de Teams</b></summary>

| Resource | Objetivo | Descripción |
| --- | --- | --- |
| Plan de App Service | Hospeda la aplicación web de la pestaña. | No aplicable |
| App Service | Hospeda la aplicación de pestaña Blazor y el servidor de autenticación simple que ayuda a obtener acceso a otros servicios. | Añade la identidad asignada por el usuario para acceder a otros recursos de Azure. |
| Administrar identidad | Autentique las solicitudes de servicio a servicio de Azure. | Recursos compartidos entre diferentes funcionalidades y recursos. |

</details>
<br>

<details>
<summary><b>Creación de recursos para la aplicación de extensión de mensajes de Teams</b></summary>

| Resource | Objetivo | Descripción |
| --- | --- | --- |
| Bot de Azure | Registra la aplicación como un bot con bot framework. | Conecta el bot a Teams. |
| plan de App Service | Hospeda la aplicación de bot web. | No aplicable |
| App Service | Hospeda la aplicación de bot. | Añade la identidad asignada por el usuario para acceder a otros recursos de Azure. |
| Administrar identidad | Autentique las solicitudes de servicio a servicio de Azure. | Recursos compartidos entre diferentes funcionalidades y recursos. |

</details>
<br>

<details>
<summary><b>Creación de recursos para la aplicación de bot de comandos de Teams</b></summary>

| Resource | Objetivo | Descripción |
| --- | --- | --- |
| Bot de Azure | Registra la aplicación como un bot con bot framework. | Conecta el bot a Teams. |
| Plan de App Service | Hospeda la aplicación de bot web. | No aplicable |
| App Service | Hospeda la aplicación de bot. | Añade la identidad asignada por el usuario para acceder a otros recursos de Azure. |
| Administrar identidad | Autentique las solicitudes de servicio a servicio de Azure. | Recursos compartidos entre diferentes funcionalidades y recursos. |

</details>
<br>

<details>
<summary><b>Creación de recursos para el bot de notificación de Teams con una aplicación de desencadenador HTTP (servidor de API web)</b></summary>

| Resource | Objetivo | Descripción |
| --- | --- | --- |
| Bot de Azure | Registra la aplicación como un bot con bot framework. | Conecta el bot a Teams. |
| Plan de App Service | Hospeda la aplicación de bot web. | No aplicable |
| App Service | Hospede la aplicación de bot. | Añade la identidad asignada por el usuario para acceder a otros recursos de Azure. |
| Identidad administrada | Autentique las solicitudes de servicio a servicio de Azure. | Recursos compartidos entre diferentes funcionalidades y recursos. |

</details>
<br>

<details>
<summary><b>Creación de recursos para el bot de notificación de Teams con una aplicación de desencadenador HTTP (función de Azure)</b></summary>

| Resource | Objetivo | Descripción |
| --- | --- | --- |
| Bot de Azure | Registra la aplicación como un bot con bot framework. | Conecta el bot a Teams. |
| Administrar identidad | Autentica las solicitudes de servicio a servicio de Azure. | Compartido entre diferentes funcionalidades y recursos. |
| Cuenta de almacenamiento | Ayuda a crear la aplicación de funciones. | No aplicable |
| Plan de App Service | Hospeda la aplicación del bot de función. | No aplicable |
| Aplicación de funciones | Hospeda la aplicación de bot. | -Agrega la identidad asignada por el usuario para acceder a otros recursos de Azure.<br>-Agrega la regla de uso compartido de recursos entre orígenes (CORS) para permitir solicitudes desde la aplicación de pestaña.<br>-Agrega la configuración de autenticación que solo permite las solicitudes de la aplicación de Teams.<br>-Agrega la configuración de la aplicación requerida por el SDK de TeamsFx. |

</details>
<br>

<details>
<summary><b>Creación de recursos para el bot de notificación de Teams con una aplicación de desencadenador de temporizador (función de Azure)</b></summary>

| Resource | Objetivo | Descripción |
| --- | --- | --- |
| Bot de Azure | Registra la aplicación como un bot con bot framework. | Conecta el bot a Teams. |
| Administrar identidad | Autentique las solicitudes de servicio a servicio de Azure. | Recursos compartidos entre diferentes funcionalidades y recursos. |
| Cuenta de almacenamiento | Ayuda a crear la aplicación de funciones. | No procede. |
| Plan de App Service | Hospeda la aplicación de bot de función. | No aplicable |
| Aplicación de funciones | Hospeda la aplicación de bot. | -Agrega la identidad asignada por el usuario para acceder a otros recursos de Azure.<br>-Agrega la regla de uso compartido de recursos entre orígenes (CORS) para permitir solicitudes desde la aplicación de pestaña.<br>-Agrega la configuración de autenticación que solo permite las solicitudes de la aplicación de Teams.<br>-Agrega la configuración de la aplicación requerida por el SDK de TeamsFx. |

</details>
<br>

<details>
<summary><b>Creación de recursos para el bot de notificación de Teams con la aplicación desencadenador HTTP y desencadenador de temporizador (función de Azure)</b></summary>

| Resource | Objetivo | Descripción |
| --- | --- | --- |
| Bot de Azure | Registra la aplicación como un bot con bot framework. | Conecta el bot a Teams. |
| Administrar identidad | Autentique las solicitudes de servicio a servicio de Azure. | Recursos compartidos entre diferentes funcionalidades y recursos. |
| Cuenta de almacenamiento | Ayuda a crear la aplicación de funciones. | No aplicable |
| Plan de App Service | Hospeda la aplicación de bot de función. | No aplicable |
| Function App | Hospeda la aplicación de bot. | -Agrega la identidad asignada por el usuario para acceder a otros recursos de Azure.<br>-Agrega la regla de uso compartido de recursos entre orígenes (CORS) para permitir solicitudes desde la aplicación de pestaña.<br>-Agrega la configuración de autenticación que solo permite las solicitudes de la aplicación de Teams.<br>-Agrega la configuración de la aplicación requerida por el SDK de TeamsFx. |

</details>
<br>

### <a name="manage-your-resources"></a>Administrar los recursos

Puede iniciar sesión para [Azure Portal](https://portal.azure.com/) y administrar todos los recursos creados por Teams Toolkit.

* Puede seleccionar el grupo de recursos de la lista existente o el nuevo grupo de recursos que ha creado.
* Puede ver los detalles del grupo de recursos que ha seleccionado en la sección de información general de la tabla de contenido.

## <a name="customize-resource-provision"></a>Personalización del aprovisionamiento de recursos

Teams Toolkit le permite usar una infraestructura para el enfoque de código para definir los recursos de Azure que desea aprovisionar. Puede cambiar la configuración en el kit de herramientas de Teams según sus necesidades.

Teams Toolkit usa una plantilla de ARM para definir recursos de Azure. La plantilla de ARM es un conjunto de archivos bicep que define la infraestructura y configuración del proyecto. Puede personalizar los recursos de Azure modificando la plantilla de ARM. Para obtener más información, consulte la [documentación de bicep](/azure/azure-resource-manager/bicep).

Aprovisionar con ARM implica cambiar los siguientes conjuntos de archivos, parámetros y plantillas:

* Archivos de parámetros de ARM (`azure.parameters.{your_env_name}.json`) ubicados en `.fx/configs` la carpeta para pasar parámetros a plantillas.
* Los archivos de plantilla de ARM ubicados en `templates/azure` la carpeta contienen los siguientes archivos:

| Archivo | Función | Permitir personalización |
| --- | --- | --- |
| main.bicep | Proporcione un punto de entrada para el recurso de Azure. Provisión | Sí |
| provision.bicep | Cree y configure recursos de Azure. | Sí |
| config.bicep | Agregue las configuraciones necesarias de TeamsFx a los recursos de Azure. | Sí |
| provision/xxx.bicep | Cree y configure cada recurso de Azure consumido por `provision.bicep`. | Sí |
| teamsfx/xxx.bicep | Agregue las configuraciones necesarias de TeamsFx a cada recurso de Azure consumido por `config.bicep`.| No |

> [!NOTE]
> Después de agregar recursos o funcionalidades al proyecto, `teamsfx/xxx.bicep` se vuelve a generar. Para modificar los archivos de bicep, puede usar Git para realizar un seguimiento de los cambios en `teamsfx/xxx.bicep` los archivos. Esto no hace que pierda ningún cambio al agregar recursos o funcionalidades al proyecto.

Los archivos de plantilla de ARM usan marcadores de posición para los parámetros. El propósito de los marcadores de posición es asegurarse de que se pueden crear nuevos recursos en el nuevo entorno. Los valores reales se resuelven desde el `.fx/states/state.{env}.json` archivo.

### <a name="azure-ad-application-related-parameters"></a>Parámetros relacionados con la aplicación de Azure AD

| Nombre del parámetro | Marcador de posición de valor predeterminado | Significado del marcador de posición | Cómo personalizar |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | El identificador de cliente de la aplicación de Azure AD creado durante el aprovisionamiento. | [Uso de una aplicación de Azure AD existente para la aplicación de Teams](#use-an-existing-azure-ad-app-for-your-teams-app) |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | El secreto de cliente de la aplicación de Azure AD creado durante el aprovisionamiento. | [Uso de una aplicación de Azure AD existente para la aplicación de Teams](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | Identificador de inquilino de la aplicación de Azure AD. | [Uso de una aplicación de Azure AD existente para la aplicación de Teams](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 OAuthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | Host de autoridad de OAuth de la aplicación de Azure AD de la aplicación. | [Uso de una aplicación de Azure AD existente para la aplicación de Teams](#use-an-existing-azure-ad-app-for-your-teams-app) |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | Identificador de cliente de la aplicación de Azure AD del bot creado durante el aprovisionamiento. | [Uso de una aplicación existente de Azure AD para el bot](#use-an-existing-azure-ad-app-for-your-bot) |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | Secreto de cliente de la aplicación de Azure AD del bot creado durante el aprovisionamiento. | [Uso de una aplicación existente de Azure AD para el bot](#use-an-existing-azure-ad-app-for-your-bot) |

### <a name="reference-environment-variables-in-parameter-files"></a>Variables de entorno de referencia en archivos de parámetros

Cuando el valor es secreto, no es necesario codificarlos de forma rígida en el archivo de parámetros. los archivos de parámetros admiten referenciar valores de las variables de entorno. Puede usar esta sintaxis `{{$env.YOUR_ENV_VARIABLE_NAME}}` en los valores de parámetro del kit de herramientas de Teams para resolver a partir de la variable de entorno actual.

En el ejemplo siguiente se lee el valor del parámetro `mySelfHostedDbConnectionString` de la variable de entorno `DB_CONNECTION_STRING`:

```json
...
    "mySelfHostedDbConnectionString": "{{$env.DB_CONNECTION_STRING}}"
...
```

### <a name="customize-arm-template-files"></a>Personalización de archivos de plantilla de ARM

Si las plantillas predefinidas no cumplen los requisitos de la aplicación, puede personalizar las plantillas de ARM en `templates/azure` la carpeta . Por ejemplo, puede personalizar la plantilla de ARM para crear algunos recursos adicionales de Azure para la aplicación. Debe tener conocimientos básicos del lenguaje bicep, que se usa para crear una plantilla de ARM.

Para asegurarse de que la herramienta TeamsFx funciona correctamente, personalice la plantilla de ARM que satisfaga el siguiente requisito:

* Asegúrese de que la estructura de carpetas y el nombre de archivo permanecen sin cambios. La herramienta puede anexar contenido nuevo a los archivos existentes al agregar más recursos o funcionalidades al proyecto.
* Asegúrese de que el nombre de los parámetros generados automáticamente y sus nombres de propiedad permanecen sin voladizo. Puede que se usen los parámetros generados automáticamente al añadir más recursos o funcionalidades al proyecto.
* Asegúrese de que la salida de la plantilla de ARM generada automáticamente también no cambia. Puede agregar más salidas a la plantilla de ARM. La salida es `.fx/states/state.{env}.json` y se puede usar en otras características, como implementar y validar el archivo de manifiesto.

### <a name="customize-teams-app"></a>Personalización de la aplicación Teams

Puede personalizar el bot o la aplicación de Teams agregando fragmentos de código de configuración para usar una aplicación de Azure AD creada por usted. Puede realizar de las siguientes maneras:

#### <a name="use-an-existing-azure-ad-app-for-your-bot"></a>Uso de una aplicación de Azure AD existente para el bot

Puede agregar el siguiente fragmento de código de `.fx/configs/config.{env}.json` configuración para usar una aplicación de Azure AD creada por usted para la aplicación de Teams. Para crear una aplicación de Azure AD, siga el vínculo <https://aka.ms/teamsfx-existing-aad-doc>.

```json
"auth": {
    "clientId": "<your Azure AD app client id>",
    "clientSecret": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}",
    "objectId": "<your Azure AD app object id>",
    "accessAsUserScopeId": "<id of the access_as_user scope>"
}
```

Después de agregar el fragmento de código, agregue el secreto de cliente a la variable de entorno relacionada para que teams Toolkit pueda resolver el secreto de cliente real durante el aprovisionamiento.

> [!NOTE]
> Asegúrese de no compartir la misma aplicación Azure AD en varios entornos. Si no tiene permiso para actualizar la aplicación de Azure AD, recibirá una advertencia con instrucciones para actualizar manualmente la aplicación de Azure AD. Siga estas instrucciones para actualizar la aplicación de Azure AD después del aprovisionamiento.

#### <a name="use-an-existing-azure-ad-app-for-your-teams-app"></a>Uso de una aplicación de Azure AD existente para su aplicación de Teams

Puede agregar el siguiente fragmento de código de configuración para `.fx/configs/config.{env}.json` usar la aplicación de Azure AD creada para el bot:

```json
"bot": {
    "appId": "<your Azure AD app client id>",
    "appPassword": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}"
}
```

Después de agregar el fragmento de código, agregue el secreto de cliente a la variable de entorno relacionada para que Teams Toolkit resuelva el secreto de cliente real durante el aprovisionamiento.

#### <a name="skip-adding-user-for-sql-database"></a>Omisión de la adición de usuario a la base de datos SQL

Si recibe un error de permiso insuficiente cuando Teams Toolkit intenta agregar un usuario a SQL Database, puede agregar el siguiente fragmento de código de configuración para `.fx/configs/config.{env}.json` omitir la adición de un usuario de base de datos SQL:

```json
"skipAddingSqlUser": true
```

::: zone-end

## <a name="see-also"></a>Consulte también

* [Implementar la aplicación de Teams en la nube](deploy.md)
* [Administrar varios entornos](TeamsFx-multi-env.md)
* [Colaborar con otros desarrolladores en proyectos de Teams](TeamsFx-collaboration.md)
* [Implementación de una aplicación de Teams en la nube mediante Visual Studio](deploy-teams-app.md)
* [Edición del manifiesto de aplicación de Teams mediante Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md)
* [Depuración local de aplicaciones de Teams para Visual Studio](debug-teams-app-visual-studio.md)

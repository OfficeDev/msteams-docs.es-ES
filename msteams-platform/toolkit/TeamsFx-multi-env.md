---
title: TeamsFX varios entornos en Teams Toolkit
author: MuyangAmigo
description: Acerca del entorno múltiple de TeamsFX
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview of multiple environment
ms.date: 11/29/2021
ms.openlocfilehash: 0e53d90dd6ead30200dd1f07ba9a100a3d1f4ca1
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/30/2021
ms.locfileid: "61228183"
---
# <a name="manage-multiple-environments-in-teams-toolkit"></a>Administrar varios entornos en Teams Toolkit

 Teams Toolkit proporciona una forma sencilla para que los desarrolladores creen y administren varios entornos, aprovisionan e implementan artefactos en el entorno de destino para Teams App.

 Con varios entornos, los desarrolladores pueden:

1. **Probar antes** de la producción: es una práctica común configurar varios entornos (desarrollo, prueba, almacenamiento provisional) antes de publicar una aplicación Teams en el entorno de producción en el ciclo de vida de desarrollo de aplicaciones moderno.

2. **Administrar comportamientos de** aplicaciones en diferentes entornos: los desarrolladores pueden establecer comportamientos diferentes para entornos diferentes, como los desarrolladores, que quieran habilitar la telemetría en el entorno de producción, pero deshabilitarla en el entorno de desarrollo.

## <a name="prerequisite"></a>Requisito previo

* [Instale Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión 3.0.0+.

>[!TIP]
> Ya debería tener abierto un proyecto Teams aplicación en el código VS.

## <a name="create-a-new-environment"></a>Crear un nuevo entorno

Después de crear un nuevo proyecto, Teams Toolkit crea de forma predeterminada:

- Un `local` entorno para representar las configuraciones del entorno de máquina local.
- Un `dev` entorno para representar las configuraciones de entorno remoto/en la nube.

> [!NOTE]
> Cada proyecto solo puede tener un `local` entorno, pero varios entornos remotos.

Para agregar otro entorno remoto, seleccione el icono Teams en la barra lateral, haga clic en el botón Más en la sección Entorno y siga las preguntas que se deben crear como se muestra en la siguiente imagen:

![add-env](./images/create-env.png)

> [!NOTE]
> Si tiene más de un entorno existente, deberá seleccionar un entorno existente para crear el entorno. El comando copiará el contenido del archivo del entorno existente que seleccionó y del mismo en `config.<newEnv>.json` el nuevo entorno que se va a `azure.parameters.<newEnv>.json` crear.

## <a name="select-target-environment"></a>Seleccionar entorno de destino 

Con el concepto de entorno introducido en Teams Toolkit, para todas las operaciones relacionadas con el entorno, puede seleccionar el entorno de destino en el que realizar las operaciones. El kit de herramientas pedirá y pedirá un entorno de destino cuando tenga varios entornos remotos, como se muestra en la siguiente imagen:

![seleccionar env](./images/select-env.png)

## <a name="project-folder-structure"></a>Project de carpetas 

Después de crear el proyecto, puede ver las carpetas y archivos del proyecto en el área Explorador de Visual Studio Code. Además de los códigos personalizados, algunos archivos se usan Teams Toolkit para mantener la configuración, el estado y la plantilla de la aplicación. A continuación, enumera esos archivos y describe su relación con varios entornos.

- `.fx/configs`: archivos de configuración que el usuario puede personalizar para la Teams aplicación.
  - `config.<envName>.json`: archivo de configuración por entorno.
  - `azure.parameters.<envName>.json`: archivo de parámetros por entorno para la aprovisionamiento de Azure BICEP.
  - `projectSettings.json`: configuración global del proyecto, que se aplica a todos los entornos.
  - `localSettings.json`: archivo de configuración de depuración local.
- `.fx/states`: resultado de aprovisionamiento generado por el Toolkit.
  - `state.<envName>.json`: archivo de salida de aprovisionamiento por entorno.
  - `<env>.userdata`: datos de usuario confidenciales por entorno para la salida de aprovisionamiento.
- `templates`
  - `appPackage`: archivos de plantilla de manifiesto de aplicación.
  - `azure`: archivos de plantilla BICEP.

## <a name="customize-the-provision"></a>Personalizar la provisión 

Teams Toolkit permite cambiar los archivos de configuración y los archivos de plantilla para personalizar la provisión de recursos en cada entorno.

En la tabla siguiente se enumeran los escenarios comunes admitidos para la provisión personalizada y dónde personalizar:

| Escenarios | Dónde personalizar | Cómo personalizar |
| --- | --- | --- |
| Personalizar recurso de Azure | <ul> <li>Archivos BICEP en `templates/azure` .</li> <li>`.fx/azure.parameters.<envName>.json`.</li></ul> | Consulte para [personalizar ARM parámetros y plantillas para](provision.md#customize-arm-parameters-and-templates) obtener más información. |
| Volver a la aplicación AAD existente para Teams aplicación | <ul> <li>`auth` sección en `.fx/config.<envName>.json` .</li> </ul> | Consulta usar [una aplicación de AAD existente para tu Teams para](provision.md#use-an-existing-aad-app-for-your-teams-app) obtener más detalles. |
| Volver a la aplicación AAD existente para bot | <ul> <li>`bot` sección en `.fx/config.<envName>.json` .</li> </ul> | Consulta usar [una aplicación de AAD existente para el bot](provision.md#use-an-existing-aad-app-for-your-bot) para obtener más información. |
| Omitir agregar usuario al aprovisionar SQL | <ul> <li>`skipAddingSqlUser` propiedad en `.fx/config.<envName>.json` .</li> </ul> | Consulte omitir [la adición de usuarios SQL base de datos para](provision.md#skip-adding-user-for-sql-database) obtener más información. |
| Personalizar manifiesto de aplicación | <ul> <li>`templates/manifest.remote.template.json`.</li> <li>`manifest` sección en `.fx/config.<envName>.json` .</li>  </ul> | Consulte para [personalizar Teams manifiesto de aplicación en Teams Toolkit](TeamsFx-manifest-customization.md) para obtener más detalles. |

## <a name="scenarios"></a>Escenarios

### <a name="scenario-1-customize-teams-app-name-for-different-environment"></a>Escenario 1: personalizar el Teams de la aplicación para diferentes entornos

En este ejemplo, aprenderá a establecer el nombre de la aplicación Teams para el entorno predeterminado y `myapp(dev)` para el entorno de almacenamiento provisional `dev` `myapp(staging)` `staging` .

Siga los pasos para la personalización:

- Paso 1: abrir archivo de configuración `.fx/configs/config.dev.json` .
- Paso 2: actualizar la propiedad del manifiesto > *appName > short* to `myapp(dev)`

  Actualizaciones a `.fx/configs/config.dev.json` :

  ```json
  {
      "$schema": "https://aka.ms/teamsfx-env-config-schema",
      "description": "You can customize the TeamsFx config for different environments.   Visit https://aka.ms/teamsfx-env-config to learn more about this.",
      "manifest": {
          "appName": {
              "short": "myapp(dev)"
              ...
          }
      }
      ...
  }
  ```

- Paso 3: crear un nuevo entorno denominado `staging` si no existe.
- Paso 4: abrir archivo de configuración `.fx/configs/config.staging.json` .
- Paso 5: actualizar la misma propiedad del paso 2 a `myapp(staging)` .
- Paso 6: ejecutar el comando de aprovisionamiento en y el entorno para actualizar el nombre de la aplicación `dev` `staging` en entornos remotos. Para ejecutar el comando de aprovisionamiento con Teams Toolkit. Para obtener más información, vea [este documento](provision.md#provision-using-teams-toolkit).

### <a name="scenario-2-customize-teams-app-description-for-different-environment"></a>Escenario 2: personalizar Teams descripción de la aplicación para diferentes entornos

En este escenario, aprenderás a establecer diferentes Teams descripción de la aplicación para distintos entornos:

- Para el entorno `dev` predeterminado, la descripción será `my app description for dev` ;
- Para el entorno de `staging` almacenamiento provisional, la descripción será `my app description for staging` ;

Pasos para realizar la personalización:

- Paso 1: abrir archivo de configuración `.fx/configs/config.dev.json` .
- Paso 2: Agregar nueva propiedad del manifiesto > *descripción > con el* valor `my app description for dev` .

  Actualizaciones para `.fx/configs/config.dev.json`

  ```json
  {
      "$schema": "https://aka.ms/teamsfx-env-config-schema",
      "description": "You can customize the TeamsFx config for different environments.   Visit https://aka.ms/teamsfx-env-config to learn more about this.",
      "manifest": {
          ...
          "description": {
              "short": "`my app description for dev"
              ...
          }
      }
      ...
  }
  ```

- Paso 3: crear un nuevo entorno denominado `staging` si no existe.
- Paso 4: abrir archivo de configuración `.fx/configs/config.staging.json` .
- Paso 5: agregar la misma propiedad del paso 2 a `my app description for staging` .
- Paso 6: abrir Teams de manifiesto de la aplicación para el control `templates/appPackage/manifest.remote.template.json` remoto .
- Paso 7: actualizar la propiedad para usar la variable definida en los archivos `description > short` de configuración con sintaxis de mustache  `{{config.manifest.description.short}}` .
  
  Actualizaciones a `manifest.remote.template.json` :

  ```json
  {
    "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
    "manifestVersion": "1.11",
    "version": "1.0.0",
    ...
    "description": {
      "short": "{{config.manifest.description.short}}",
      ...
    },
    ...
  }
  ```
- Paso 8: ejecutar el comando de aprovisionamiento en y el entorno para actualizar el nombre de `dev` `staging` la aplicación en entornos remotos. Para ver cómo ejecutar el comando de aprovisionamiento Teams Toolkit, puede consultar [este documento para](provision.md#provision-using-teams-toolkit) obtener más información.

### <a name="scenario-3-customize-teams-app-description-for-all-environments"></a>Escenario 3: personalizar Teams descripción de la aplicación para todos los entornos

En este escenario, aprenderás a establecer la descripción de Teams aplicación en `my app description` todos los entornos.

Como la Teams de manifiesto de la aplicación se comparte en todos los entornos, podemos actualizar el valor de descripción en ella para nuestro destino:

- Paso 1: abrir Teams de manifiesto de la aplicación para el control `templates/appPackage/manifest.remote.template.json` remoto .
- Paso 2: actualizar la propiedad `description > short` con **una cadena codificada de forma automática.** `my app description`
  
  Actualizaciones a `manifest.remote.template.json` :

  ```json
  {
    "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
    "manifestVersion": "1.11",
    "version": "1.0.0",
    ...
    "description": {
      "short": "my app description",
      ...
    },
    ...
  }

- Step 3: run provision command against **all** environment to update the app name in remote environments. For how to run provision command with Teams Toolkit, you can refer to [this document](provision.md#provision-using-teams-toolkit) for more details.

### Scenario 4: customize Azure resources for different environment

You can customize Azure resources for each environment, for example specifying Azure Function name, by editing the environment corresponding `.fx/configs/azure.parameters.{env}.json` file.

For more information on BICEP template and parameter files, see [provision cloud resources](provision.md)

## See also

> [!div class="nextstepaction"]
> [Provision cloud resources](provision.md)

> [!div class="nextstepaction"]
> [Add more cloud resources](add-resource.md)

> [!div class="nextstepaction"]
> [Collaborate with other developers on Teams project](TeamsFx-collaboration.md)

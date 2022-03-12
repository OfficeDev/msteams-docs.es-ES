---
title: TeamsFX varios entornos en Teams Toolkit
author: MuyangAmigo
description: Acerca del entorno múltiple de TeamsFX
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview of multiple environment
ms.date: 11/29/2021
ms.openlocfilehash: 27172617db35126fb086d8691486e86c2946f0bd
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453589"
---
# <a name="manage-multiple-environments-in-teams-toolkit"></a>Administrar varios entornos en Teams Toolkit

 Teams Toolkit una forma sencilla de crear y administrar varios entornos, aprovisionar e implementar artefactos en el entorno de destino para Teams App.

 Con varios entornos, puede realizar lo siguiente:

1. **Probar** antes de la producción: es una práctica común configurar varios entornos, como desarrollo, prueba y almacenamiento provisional antes de publicar una aplicación Teams en el entorno de producción en el ciclo de vida de desarrollo de aplicaciones moderno.

2. **Administrar comportamientos de aplicaciones en diferentes entornos**: puede establecer comportamientos diferentes para varios entornos, como habilitar la telemetría en el entorno de producción, pero deshabilitarla en el entorno de desarrollo.

## <a name="prerequisite"></a>Requisito previo

* [Instale Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión 3.0.0+.

> [!TIP]
> Asegúrate de que tienes Teams proyecto de aplicación abierto en Microsoft Visual Studio código.

## <a name="create-a-new-environment"></a>Crear un nuevo entorno

Después de crear un nuevo proyecto, Teams Toolkit crea de forma predeterminada:

* Un `local` entorno para representar las configuraciones del entorno de máquina local.
* Un `dev` entorno para representar las configuraciones remotas o del entorno en la nube.

> [!NOTE]
> Cada proyecto solo puede tener un entorno `local` , pero varios entornos remotos.

Para agregar otro entorno remoto, seleccione el icono Teams en la barra lateral, seleccione crear nuevo entorno en la sección Debajo de Entorno, como se muestra en la siguiente imagen:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create new env.png" alt-text="crear":::

> [!NOTE]
> Si tiene más de un entorno existente, debe seleccionar un entorno existente para crear el mismo. El comando copiará el contenido del archivo del `config.<newEnv>.json` `azure.parameters.<newEnv>.json` entorno existente que seleccionó y del mismo en el nuevo entorno que se va a crear.

## <a name="select-target-environment"></a>Seleccionar entorno de destino

Puede seleccionar el entorno de destino para todas las operaciones relacionadas con el entorno. El kit de herramientas solicita y pide un entorno de destino cuando tiene varios entornos remotos, como se muestra en la siguiente imagen:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="agregar env":::

## <a name="project-folder-structure"></a>Project de carpetas

Después de crear el proyecto, puede ver las carpetas y archivos del proyecto en el área del explorador de Visual Studio Code. Además de los códigos personalizados, algunos archivos se usan Teams Toolkit para mantener la configuración, el estado y la plantilla de la aplicación. En la siguiente lista se proporcionan archivos y se describe su relación con varios entornos.

* `.fx/configs`: configure los archivos que el usuario puede personalizar para la Teams aplicación.
  * `config.<envName>.json`: archivo de configuración por entorno.
  * `azure.parameters.<envName>.json`: archivo de parámetros por entorno para la aprovisionamiento de bíceps de Azure.
  * `projectSettings.json`: configuración global del proyecto, que se aplica a todos los entornos.
  * `localSettings.json`: archivo de configuración de depuración local.
* `.fx/states`: resultado de aprovisionamiento generado por el Toolkit.
  * `state.<envName>.json`: archivo de salida de aprovisionamiento por entorno.
  * `<env>.userdata`: datos de usuario confidenciales por entorno para la salida de aprovisionamiento.
* `templates`
  * `appPackage`: archivos de plantilla de manifiesto de aplicación.
  * `azure`: archivos de plantilla Bicep.

## <a name="customize-the-provision"></a>Personalizar la provisión

Teams Toolkit permite cambiar los archivos de configuración y los archivos de plantilla para personalizar la provisión de recursos en cada entorno.

En la tabla siguiente se enumeran los escenarios comunes admitidos para la provisión personalizada y dónde personalizar:

| Escenarios | Ubicación| Descripción |
| --- | --- | --- |
| Personalizar recurso de Azure | <ul> <li>Archivos Bicep en `templates/azure`.</li> <li>`.fx/azure.parameters.<envName>.json`.</li></ul> | [Personalice ARM parámetros y plantillas](provision.md#customize-arm-parameters-and-templates). |
| Reutilizar la aplicación Azure AD existente para Teams aplicación | <ul> <li>`auth` sección en`.fx/config.<envName>.json`.</li> </ul> |  [Usa una aplicación de Azure AD existente para tu Teams aplicación](provision.md#use-an-existing-azure-ad-app-for-your-teams-app). |
| Reutilizar la aplicación Azure AD existente para bot | <ul> <li>`bot` sección en`.fx/config.<envName>.json`.</li> </ul> | [Usa una aplicación Azure AD para el bot](provision.md#use-an-existing-azure-ad-app-for-your-bot). |
| Omitir la adición de usuarios al aprovisionar SQL | <ul> <li>`skipAddingSqlUser` propiedad in`.fx/config.<envName>.json`.</li> </ul> | [Omitir la adición de usuarios SQL base de datos](provision.md#skip-adding-user-for-sql-database). |
| Personalizar manifiesto de aplicación | <ul> <li>`templates/manifest.remote.template.json`.</li> <li>`manifest` sección en`.fx/config.<envName>.json`.</li>  </ul> | [Personalizar Teams de aplicación en Teams Toolkit](TeamsFx-manifest-customization.md). |

## <a name="scenarios"></a>Escenarios

### <a name="scenario-1-customize-teams-app-name-for-different-environment"></a>Escenario 1: personalizar el Teams de la aplicación para diferentes entornos

Puede establecer el nombre Teams aplicación en `myapp(dev)` para el entorno predeterminado `dev` y `myapp(staging)` para el entorno de almacenamiento provisional `staging`.

Realice los pasos siguientes para la personalización:

* 1. Abra el archivo de configuración `.fx/configs/config.dev.json`.
* 2. Actualizar la propiedad del *manifiesto > appName > short* to `myapp(dev)`

  Las actualizaciones son `.fx/configs/config.dev.json` las siguientes:

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

* 3. Cree un nuevo entorno y así mismo `staging` , si no existe.
* 4. Abra el archivo de configuración `.fx/configs/config.staging.json`.
* 5. Actualice la misma propiedad `myapp(staging)`.
* 6. Ejecute el comando de aprovisionamiento en `dev` y `staging` el entorno para actualizar el nombre de la aplicación en entornos remotos. Para ejecutar el comando de aprovisionamiento Teams Toolkit, vea [provision](provision.md#provision-using-teams-toolkit).

### <a name="scenario-2-customize-teams-app-description-for-different-environment"></a>Escenario 2: personalizar Teams descripción de la aplicación para diferentes entornos

En este escenario, aprenderás a establecer diferentes Teams descripción de la aplicación para diferentes entornos:

* Para el entorno predeterminado `dev`, la descripción será `my app description for dev`;
* Para el entorno de almacenamiento `staging`provisional, la descripción será `my app description for staging`;

Realice los pasos siguientes para la personalización:

* 1. Abra el archivo de configuración `.fx/configs/config.dev.json`.
* 2. Agregue una nueva propiedad del *manifiesto > descripción > con el* valor `my app description for dev`.

  Las actualizaciones son `.fx/configs/config.dev.json` las siguientes:

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

* 3. Cree un nuevo entorno y así mismo `staging` , si no existe.
* 4. Abra el archivo de configuración `.fx/configs/config.staging.json`.
* 5. Agregue la misma propiedad a `my app description for staging`.
* 6. Abra Teams de manifiesto de la aplicación para el control remoto `templates/appPackage/manifest.remote.template.json`.
* 7. Actualice la propiedad para `description > short` usar la **variable definida** en configurar archivos con sintaxis de mustache `{{config.manifest.description.short}}`.
  
  Las actualizaciones son `manifest.remote.template.json` las siguientes:

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

* 8. Ejecute el comando de aprovisionamiento en `dev` y `staging` el entorno para actualizar el nombre de la aplicación en entornos remotos. Para ejecutar el comando de aprovisionamiento Teams Toolkit, vea [provision](provision.md#provision-using-teams-toolkit).

### <a name="scenario-3-customize-teams-app-description-for-all-environments"></a>Escenario 3: personalizar Teams descripción de la aplicación para todos los entornos

En este escenario, aprenderás a establecer la descripción de Teams aplicación en `my app description` todos los entornos.

Como la Teams de manifiesto de la aplicación se comparte en todos los entornos, podemos actualizar el valor de descripción en ella para nuestro destino:

* 1. Abra Teams de manifiesto de la aplicación para el control remoto `templates/appPackage/manifest.remote.template.json`.
* 2. Actualice la propiedad `description > short` con **una cadena codificada de forma automática**`my app description`.
  
  Las actualizaciones son `manifest.remote.template.json` las siguientes:

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

* 3. Run provision command against **all** environment to update the app name in remote environments. To run provision command with Teams Toolkit, see [provision](provision.md#provision-using-teams-toolkit).

### Scenario 4: customize Azure resources for different environment

You can customize Azure resources for each environment, for example specify Azure Function name, by editing the environment corresponding to `.fx/configs/azure.parameters.{env}.json` file.

For more information on Bicep template and parameter files, see [provision cloud resources](provision.md)

## See also

* [Provision cloud resources](provision.md)
* [Add more cloud resources](add-resource.md)
* [Collaborate with other developers on Teams project](TeamsFx-collaboration.md)

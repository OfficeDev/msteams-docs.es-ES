---
title: Entorno múltiple de TeamsFX en el kit de herramientas de Teams
author: MuyangAmigo
description: Acerca del entorno múltiple de TeamsFX
ms.author: nintan
ms.localizationpriority: high
ms.topic: overview of multiple environment
ms.date: 11/29/2021
ms.openlocfilehash: b9719add5036ae533ce6d7c395ab95a5905bcbb8
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111867"
---
# <a name="manage-multiple-environments"></a>Administrar varios entornos

 El kit de herramientas de Teams proporciona una manera sencilla de crear y administrar varios entornos, aprovisionar e implementar artefactos en el entorno de destino para la aplicación de Teams.

 Puede realizar lo siguiente con los distintos entornos:

1. **Prueba antes de producción**: puede configurar varios entornos, como desarrollo, prueba y ensayo antes de publicar una aplicación de Teams en el entorno de producción en el ciclo de vida moderno de desarrollo de aplicaciones.

2. **Administrar comportamientos de aplicaciones en diferentes entornos**: puede configurar diferentes comportamientos para varios entornos, como habilitar la telemetría en el entorno de producción, pero deshabilitarlo en el entorno de desarrollo.

## <a name="prerequisite"></a>Requisito previo

* Instale la versión [más reciente del kit de herramientas de Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

> [!TIP]
> Asegúrese de que ha abierto el proyecto de aplicación de Teams en el código de Microsoft Visual Studio.

## <a name="create-a-new-environment"></a>Crear un nuevo entorno

Después de crear un nuevo proyecto, el kit de herramientas de Teams crea de forma predeterminada:

* Un entorno `local` para representar las configuraciones de entorno de máquina local
* Un entorno `dev` para representar las configuraciones de entorno remoto o en la nube

> [!NOTE]
> Cada proyecto solo puede tener un entorno `local`, pero varios entornos remotos.

**Para agregar otro entorno remoto**:

1. Seleccione el icono de **Teams** en la barra lateral.
2. Seleccione **+Teams: Crear nuevo entorno** en la sección Entorno, como se muestra en la siguiente imagen:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create new env.png" alt-text="crear":::

Si tiene más de un entorno, debe seleccionar un entorno existente para crear el mismo. El comando copia el contenido del archivo de `config.<newEnv>.json` y `azure.parameters.<newEnv>.json` del entorno existente seleccionado en el nuevo entorno creado.

## <a name="select-target-environment"></a>Seleccionar entorno de destino

Puede seleccionar el entorno de destino para todas las operaciones relacionadas con el entorno. El kit de herramientas solicita y pide un entorno de destino cuando tiene varios entornos remotos, como se muestra en la siguiente imagen:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="agregar entorno":::

## <a name="project-folder-structure"></a>Estructura de carpetas del proyecto

Después de crear el proyecto, puede ver las carpetas y los archivos del proyecto en el área del explorador de Visual Studio Code. Además de los códigos personalizados, el kit de herramientas de Teams usa algunos archivos para mantener la configuración, el estado y la plantilla de la aplicación. En esta lista se proporcionan archivos y se describe su relación con varios entornos.

* `.fx/configs`: configura los archivos que el usuario puede personalizar para la aplicación de Teams
  * `config.<envName>.json`: archivo de configuración para cada entorno 
  * `azure.parameters.<envName>.json`: archivo de parámetros para cada entorno para el aprovisionamiento de Azure Bicep
  * `projectSettings.json`: configuración global del proyecto que se aplica a todos los entornos
* `.fx/states`: resultado del aprovisionamiento generado por el kit de herramientas
  * `state.<envName>.json`: archivo de salida de aprovisionamiento para cada entorno
  * `<env>.userdata`: datos de usuario confidenciales para cada entorno para la salida de aprovisionamiento
* `templates`
  * `appPackage`: archivos de plantilla del manifiesto de aplicación
  * `azure`: archivos de plantilla de Bicep

## <a name="customize-resource-provision"></a>Personalización del aprovisionamiento de recursos

El kit de herramientas de Teams permite cambiar los archivos de configuración y los archivos de plantilla para personalizar el aprovisionamiento de recursos en cada entorno.

En la siguiente tabla se enumeran los escenarios comunes para el aprovisionamiento de recursos personalizados:

| Escenarios | Ubicación| Descripción |
| --- | --- | --- |
| Personalización del recurso de Azure | <ul> <li>Archivos de Bicep en `templates/azure`</li> <li>`.fx/azure.parameters.<envName>.json`</li></ul> | [Personalización de parámetros y plantillas de ARM](provision.md#customize-arm-parameters-and-templates) |
| Reutilización de la aplicación de Azure AD existente para la aplicación de Teams | <ul> <li>`auth` sección en`.fx/config.<envName>.json`</li> </ul> |  [Uso de una aplicación de Azure AD existente para la aplicación de Teams](provision.md#use-an-existing-azure-ad-app-for-your-teams-app) |
| Reutilización de la aplicación de Azure AD existente para el bot | <ul> <li>`bot` sección en`.fx/config.<envName>.json`</li> </ul> | [Uso de una aplicación existente de Azure AD para el bot](provision.md#use-an-existing-azure-ad-app-for-your-bot) |
| Omitir la adición de usuario al aprovisionar SQL | <ul> <li>`skipAddingSqlUser` propiedad en`.fx/config.<envName>.json`</li> </ul> | [Omitir la adición de usuario para la base de datos de SQL](provision.md#skip-adding-user-for-sql-database) |
| Personalizar el manifiesto de la aplicación | <ul> <li>`templates/manifest.template.json`</li> <li>`manifest` sección en `.fx/config.<envName>.json`</li>  </ul> | [Personalizar el manifiesto de aplicación de Teams en el kit de herramientas de Teams](TeamsFx-manifest-customization.md) |

## <a name="scenarios"></a>Escenarios

Hay cuatro escenarios para personalizar el aprovisionamiento de recursos en diferentes entornos.
<br>

<br><details>
<summary><b>Escenario 1: Personalizar el nombre de la aplicación de Teams para un entorno diferente</b></summary>

Puede establecer el nombre de la aplicación de Teams en `myapp(dev)` para el entorno predeterminado `dev` y `myapp(staging)` para el entorno de prueba`staging`.

Siga los siguientes pasos para la personalización:

1. Abra el archivo de configuración `.fx/configs/config.dev.json`
2. Actualice la propiedad del *manifiesto > appName > abreviatura* a `myapp(dev)`

  Las actualizaciones de `.fx/configs/config.dev.json` son las siguientes:

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

3. Cree un nuevo entorno y asígnele un nombre `staging` si no existe
4. Abra el archivo de configuración `.fx/configs/config.staging.json`
5. Actualice la misma propiedad `myapp(staging)`
6. Ejecute el comando de aprovisionamiento en `dev` y el entorno `staging` para actualizar el nombre de la aplicación en entornos remotos. Para ejecutar el comando de aprovisionamiento con el kit de herramientas de Teams, consulte [aprovisionamiento](provision.md#provision-using-teams-toolkit)
</details>
<br>


<details>
<summary><b>Escenario 2: Personalizar la descripción de la aplicación de Teams para diferentes entornos</b></summary>

En este escenario, aprenderá a establecer diferentes descripciones de la aplicación de Teams para los distintos entornos:

* Para el entorno predeterminado `dev`, la descripción es `my app description for dev`
* Para el entorno de prueba `staging`, la descripción es `my app description for staging`

Siga los siguientes pasos para la personalización:

1. Abra el archivo de configuración `.fx/configs/config.dev.json`
2. Agregue la nueva propiedad del *manifiesto > descripción > abreviar* con el valor `my app description for dev`

  Las actualizaciones de `.fx/configs/config.dev.json` son las siguientes:

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

3. Cree un nuevo entorno y asígnele un nombre `staging` si no existe
4. Abra el archivo de configuración `.fx/configs/config.staging.json`
5. Agregue la misma propiedad a `my app description for staging`
6. Abra la plantilla del manifiesto de la aplicación de Teams `templates/appPackage/manifest.template.json`
7. Actualice la propiedad `description > short` para usar la **variable** definida en la configuración de archivos con sintaxis de mustache `{{config.manifest.description.short}}`
  
  Las actualizaciones de `manifest.template.json` son las siguientes:

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

8. Ejecute el comando de aprovisionamiento en `dev` y en el entorno `staging` para actualizar el nombre de la aplicación en entornos remotos. Para ejecutar el comando de aprovisionamiento con el kit de herramientas de Teams, consulte [aprovisionamiento](provision.md#provision-using-teams-toolkit)

</details>
<br>

<details>
<summary><b>Escenario 3: Personalizar la descripción de la aplicación de Teams para todos los entornos</b></summary>

En este escenario, aprenderá a establecer la descripción de la aplicación de Teams en `my app description` para todos los entornos.

A medida que se comparte la plantilla de manifiesto de la aplicación de Teams en todos los entornos, podemos actualizar el valor de la descripción en ella para nuestro destino:

1. Abra la plantilla del manifiesto de la aplicación de Teams `templates/appPackage/manifest.template.json`
2. Actualice la propiedad `description > short` con **una cadena codificada de forma rígida** `my app description`
  
  Las actualizaciones de `manifest.template.json` son las siguientes:

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
 ```
3. Ejecute el comando de aprovisionamiento en **todo** el entorno para actualizar el nombre de la aplicación en entornos remotos. Para ejecutar el comando de aprovisionamiento con el kit de herramientas de Teams, consulte [aprovisionamiento](provision.md#provision-using-teams-toolkit)
<br></details>
<br>
<details>
<br><summary><b>Escenario 4: personalización de recursos de Azure para diferentes entornos</b></summary>
Puede personalizar los recursos de Azure para cada entorno, por ejemplo, especificar el nombre de la función de Azure; para ello, edite el entorno correspondiente a fx/configs/azure.parameters. {env}.json. archivo.

Para obtener más información sobre los archivos de plantilla y parámetros de Bicep, consulte [aprovisionamiento de recursos](provision.md)
</details> en la nube <br.



## <a name="see-also"></a>Vea también

* [Aprovisionar recursos en la nube](provision.md)
* [Incorporación de más recursos en la nube](add-resource.md)
* [Colaborar con otros desarrolladores en proyectos de Teams](TeamsFx-collaboration.md)
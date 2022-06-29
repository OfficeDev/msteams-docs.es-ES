---
title: Entorno múltiple de TeamsFX en el kit de herramientas de Teams
author: MuyangAmigo
description: En este módulo, obtenga información sobre el entorno multifactor de TeamsFX, como crear un nuevo entorno, seleccionar el entorno de destino y mucho más.
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview of multiple environment
ms.date: 11/29/2021
ms.openlocfilehash: da5da86bf5e96989cf962d88105c47affa899f6e
ms.sourcegitcommit: c7fbb789b9654e9b8238700460b7ae5b2a58f216
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2022
ms.locfileid: "66485653"
---
# <a name="manage-multiple-environments"></a>Administrar varios entornos

 El kit de herramientas de Teams proporciona una manera sencilla de crear y administrar varios entornos, aprovisionar e implementar artefactos en el entorno de destino para la aplicación de Teams.

 Puede realizar lo siguiente con los distintos entornos:

1. **Prueba antes de producción**: puede configurar varios entornos, como desarrollo, pruebas y almacenamiento provisional antes de publicar una aplicación de Teams en el entorno de producción en el ciclo de vida de desarrollo de aplicaciones moderno.

2. **Administrar comportamientos de aplicaciones en diferentes entornos**: puede configurar diferentes comportamientos para varios entornos, como habilitar la telemetría en el entorno de producción, pero deshabilitarlo en el entorno de desarrollo.

## <a name="prerequisite"></a>Requisito previo

* Instale la versión [más reciente del kit de herramientas de Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

> [!TIP]
> Asegúrese de que ha abierto el proyecto de aplicación de Teams en Visual Studio código.

## <a name="create-a-new-environment"></a>Crear un nuevo entorno

Después de crear un nuevo proyecto, el kit de herramientas de Teams crea de forma predeterminada:

* Un entorno `local` para representar las configuraciones de entorno de máquina local
* Un entorno `dev` para representar las configuraciones de entorno remoto o en la nube

> [!NOTE]
> Cada proyecto solo puede tener un entorno `local`, pero varios entornos remotos.

**Para agregar otro entorno remoto**:

1. Seleccione la :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/teams-toolkit-sidebar-icon.png" alt-text="barra lateral Agregar inicio de sesión único"::: de **Teams** en la barra de navegación izquierda.
2. Seleccione **+Teams: Crear nuevo entorno** en la sección **Entorno** , como se muestra en la siguiente imagen:

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create new env.png" alt-text="crear":::

   Si tiene más de un entorno, debe seleccionar un entorno existente para crear el mismo. El comando copia el contenido del archivo de `config.<newEnv>.json` y `azure.parameters.<newEnv>.json` del entorno existente seleccionado en el nuevo entorno creado.

## <a name="select-target-environment"></a>Seleccionar entorno de destino

Puede seleccionar el entorno de destino para todas las operaciones relacionadas con el entorno. El kit de herramientas solicita y pide un entorno de destino cuando tiene varios entornos remotos, como se muestra en la siguiente imagen:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="agregar entorno":::

## <a name="project-folder-structure"></a>Estructura de carpetas del proyecto

Después de crear el proyecto, puede ver las carpetas y los archivos del proyecto en **el Explorador** en VS Code. Además de los códigos personalizados, Teams Toolkit usa algunos archivos para mantener la configuración, el estado y la plantilla de la aplicación. En esta lista se proporcionan archivos y se describe su relación con varios entornos.

* `.fx/configs`: configure los archivos que el usuario puede personalizar para la aplicación de Teams.
  * `config.<envName>.json`: archivo de configuración por entorno.
  * `azure.parameters.<envName>.json`: archivo de parámetros para el aprovisionamiento de Bicep de Azure por entorno.
  * `projectSettings.json`: configuración global del proyecto que se aplica a todos los entornos.
* `.fx/states`: resultado de aprovisionamiento generado por el kit de herramientas.
  * `state.<envName>.json`: aprovisione el archivo de salida por entorno.
  * `<env>.userdata`: datos de usuario para la salida de aprovisionamiento por entorno.
* `templates`
  * `appPackage`: archivos de plantilla de manifiesto de aplicación.
  * `azure`: archivos de plantilla de Bicep.

## <a name="customize-resource-provision"></a>Personalización del aprovisionamiento de recursos

El kit de herramientas de Teams permite cambiar los archivos de configuración y los archivos de plantilla para personalizar el aprovisionamiento de recursos en cada entorno.

En la siguiente tabla se enumeran los escenarios comunes para el aprovisionamiento de recursos personalizados:

| Escenarios | Ubicación| Descripción |
| --- | --- | --- |
| Personalización del recurso de Azure | <ul> <li>Archivos de Bicep en `templates/azure`</li> <li>`.fx/azure.parameters.<envName>.json`</li></ul> | [Personalización de parámetros y plantillas de ARM](provision.md#customize-arm-parameters-and-templates) |
| Reutilización de la aplicación de Azure AD existente para la aplicación de Teams | <ul> <li>`auth` sección en`.fx/config.<envName>.json`</li> </ul> |  [Uso de una aplicación de Azure AD existente para la aplicación de Teams](provision.md#use-an-existing-azure-ad-app-for-your-teams-app) |
| Reutilización de la aplicación de Azure AD existente para el bot | <ul> <li>`bot` sección en`.fx/config.<envName>.json`</li> </ul> | [Uso de una aplicación existente de Azure AD para el bot](provision.md#use-an-existing-azure-ad-app-for-your-bot) |
| Omitir la adición de usuario al aprovisionar SQL | <ul> <li>`skipAddingSqlUser` propiedad en`.fx/config.<envName>.json`</li> </ul> | [Omitir la adición de usuario para la base de datos de SQL](provision.md#skip-adding-user-for-sql-database) |
| Personalizar el manifiesto de la aplicación | <ul> <li>`templates/manifest.template.json`</li> <li>`manifest` sección en `.fx/config.<envName>.json`</li>  </ul> | [Vista previa del manifiesto de aplicación en el kit de herramientas](TeamsFx-preview-and-customize-app-manifest.md)|

## <a name="scenarios"></a>Escenarios

Puede ver los siguientes escenarios para personalizar el aprovisionamiento de recursos en diferentes entornos.
<br>

<br><details>
<summary><b>Escenario 1: Personalización del nombre de la aplicación de Teams para diferentes entornos </b></summary>

Puede establecer el nombre `myapp(dev)` de la aplicación de Teams en para el entorno `dev` predeterminado y `myapp(staging)` para el entorno `staging`de ensayo .

Siga los pasos para la personalización:

1. Abra el archivo `.fx/configs/config.dev.json`de configuración .
2. Actualice la propiedad del *manifiesto > appName > abreviatura* a `myapp(dev)`.

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

3. Cree un nuevo entorno y asígnele `staging` el nombre si no existe.
4. Abra el archivo `.fx/configs/config.staging.json`de configuración .
5. Actualice la misma propiedad `myapp(staging)`.
6. Ejecute el comando de aprovisionamiento en `dev` y el entorno `staging` para actualizar el nombre de la aplicación en entornos remotos. Para ejecutar el comando de aprovisionamiento con El kit de herramientas de Teams, consulte [aprovisionamiento](provision.md#provision-using-teams-toolkit).

</details>

<details>
<summary><b>Escenario 2: Personalizar la descripción de la aplicación de Teams para diferentes entornos</b></summary>

Puede establecer una descripción de aplicación de Teams diferente para los diferentes entornos:

* Para el entorno `dev`predeterminado , la descripción es `my app description for dev`.
* Para el entorno `staging`de ensayo , la descripción es `my app description for staging`.

Siga los pasos para la personalización:

1. Abra el archivo `.fx/configs/config.dev.json`de configuración .
2. Agregue una nueva propiedad del *manifiesto > descripción > abreviatura* con el valor `my app description for dev`.

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

3. Cree un nuevo entorno y asígnele `staging` el nombre si no existe.
4. Abra el archivo `.fx/configs/config.staging.json`de configuración .
5. Agregue la misma propiedad a `my app description for staging`.
6. Abra la plantilla `templates/appPackage/manifest.template.json`de manifiesto de aplicación de Teams .
7. Actualice la propiedad `description > short` para usar la **variable** definida en configurar archivos con sintaxis `{{config.manifest.description.short}}`de mustache .
  
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

8. Ejecute el comando de aprovisionamiento en `dev` y en el entorno `staging` para actualizar el nombre de la aplicación en entornos remotos.

</details>

<details>
<summary><b>Escenario 3: Personalizar la descripción de la aplicación de Teams para todos los entornos</b></summary>

Puede establecer la descripción de la aplicación `my app description` de Teams en para todos los entornos.

A medida que se comparte la plantilla de manifiesto de la aplicación de Teams en todos los entornos, podemos actualizar el valor de la descripción en ella para nuestro destino:

1. Abra la plantilla `templates/appPackage/manifest.template.json`de manifiesto de aplicación de Teams .
2. Actualice la propiedad `description > short` con **una cadena** `my app description`codificada de forma rígida.
  
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

3. Ejecute el comando de aprovisionamiento en **todo** el entorno para actualizar el nombre de la aplicación en entornos remotos.

</details>

<details>
<br><summary><b>Escenario 4: personalización de recursos de Azure para diferentes entornos</b></summary>
Puede personalizar los recursos de Azure para cada entorno, por ejemplo, editar el entorno correspondiente a fx/configs/azure.parameters. {env}.json para especificar el nombre de la función de Azure.

Para obtener más información sobre los archivos de plantilla y parámetros de Bicep, consulte [aprovisionamiento de recursos en la nube](provision.md).
</details>
</br>

## <a name="see-also"></a>Vea también

* [Aprovisionar recursos en la nube](provision.md)
* [Incorporación de más recursos en la nube](add-resource.md)
* [Colaborar con otros desarrolladores en proyectos de Teams](TeamsFx-collaboration.md)

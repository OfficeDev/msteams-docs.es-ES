---
title: Entorno múltiple de TeamsFX en el kit de herramientas de Teams
author: surbhigupta
description: En este módulo, obtenga información sobre el entorno multifactor de TeamsFX, como crear un nuevo entorno, seleccionar el entorno de destino y mucho más.
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 11/29/2021
ms.openlocfilehash: 4a4b67399b2ec7c78fa536b06ee7faa9bb352468
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616946"
---
# <a name="manage-multiple-environments"></a>Administrar varios entornos

 Microsoft Teams Toolkit proporciona una manera sencilla de crear y administrar varios entornos, aprovisionar e implementar artefactos en el entorno de destino para la aplicación de Microsoft Teams.

 Puede realizar lo siguiente con varios entornos:

1. **Prueba antes de producción**: puede configurar varios entornos, como desarrollo, pruebas y almacenamiento provisional antes de publicar una aplicación de Teams en el entorno de producción en el ciclo de vida de desarrollo de aplicaciones moderno.

2. **Administrar comportamientos de aplicaciones en diferentes entornos**: puede configurar diferentes comportamientos de aplicación para varios entornos, como habilitar la telemetría en el entorno de producción.

   > [!NOTE]
   > Asegúrese de que la telemetría está deshabilitada en el entorno de desarrollo.

   > [!TIP]
   > Asegúrese de que ha abierto el proyecto de aplicación de Teams en Visual Studio código.

## <a name="create-new-environment"></a>Creación de un nuevo entorno

Después de crear un proyecto, Teams Toolkit configura de forma predeterminada:

* Un `local` entorno para representar la configuración del entorno de máquina local.
* Un `dev` entorno para representar la configuración del entorno remoto o en la nube.

> [!NOTE]
> Cada proyecto solo puede tener un entorno `local`, pero varios entornos remotos.

**Agregar entorno remoto**:

1. Seleccione el **kit de herramientas de Teams** :::image type="content" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png" alt-text="en la barra de actividad"::: de la barra de actividad.
2. Seleccione **+Teams: Crear nuevo entorno** en la sección **ENTORNO** , como se muestra en la siguiente imagen:

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create new env.png" alt-text="crear un nuevo entorno":::

> [!Note]
> Si tiene más de un entorno, debe seleccionar un entorno existente para crear el mismo. El comando copia el contenido del archivo de `config.<newEnv>.json` y `azure.parameters.<newEnv>.json` del entorno existente que ha seleccionado en el nuevo entorno creado.

## <a name="target-environment"></a>Entorno de destino

Puede seleccionar el entorno de destino, Teams Toolkit le pide que seleccione un entorno de destino cuando tenga varios entornos remotos:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="agregar entorno":::

## <a name="project-folder-structure"></a>Estructura de carpetas del proyecto

Después de crear el proyecto, puede ver las carpetas y los archivos del proyecto en **el Explorador** en Visual Studio Code. Además de los códigos personalizados, Teams Toolkit usa algunos archivos para mantener `configs`, `states`y `templates` de la aplicación. En esta lista se proporcionan archivos y se describe su relación con varios entornos.

* `.fx/configs`: configura los archivos que el usuario puede personalizar para la aplicación teams.
  * `config.<envName>.json`: archivo de configuración por entorno.
  * `azure.parameters.<envName>.json`: archivo de parámetros para el aprovisionamiento de Bicep de Azure por entorno.
  * `projectSettings.json`: configuración global del proyecto que se aplica a todos los entornos.
* `.fx/states`: resultado de aprovisionamiento generado por el kit de herramientas de Teams.
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
| Personalización del recurso de Azure |Archivos de Bicep en `templates/azure` `.fx/azure.parameters.<envName>.json` | [Personalización de parámetros y plantillas de ARM](provision.md#customize-arm-template-files) |
| Reutilización de la aplicación de Azure AD existente para la aplicación de Teams | `auth` sección en`.fx/config.<envName>.json`|  [Uso de una aplicación de Azure AD existente para la aplicación de Teams](provision.md#use-an-existing-azure-ad-app-for-your-teams-app) |
| Reutilización de la aplicación de Azure AD existente para el bot |`bot` sección en`.fx/config.<envName>.json`| [Uso de una aplicación existente de Azure AD para el bot](provision.md#use-an-existing-azure-ad-app-for-your-bot) |
| Omitir la adición de usuario al aprovisionar SQL |`skipAddingSqlUser` propiedad en`.fx/config.<envName>.json`| [Omitir la adición de usuario para la base de datos de SQL](provision.md#skip-adding-user-for-sql-database) |
| Personalizar el manifiesto de la aplicación |`templates/manifest.template.json` archivo en `manifest` la sección en `.fx/config.<envName>.json`| [Vista previa del manifiesto de aplicación en el kit de herramientas](TeamsFx-preview-and-customize-app-manifest.md)|

## <a name="scenarios"></a>Escenarios

Puede ver los siguientes escenarios para personalizar el aprovisionamiento de recursos en diferentes entornos.
<br>

<br><details>
<summary><b>Escenario 1: Personalización del nombre de la aplicación de Teams para diferentes entornos </b></summary>

Puede establecer el nombre `myapp(dev)` de la aplicación de Teams en para el entorno `dev` predeterminado y `myapp(staging)` para el entorno `staging`de ensayo .

Pasos para la personalización:

1. Abra el archivo `.fx/configs/config.dev.json`de configuración .
2. Actualice la propiedad de **`manifest`** > **`appName`** > **short** a **`myapp(dev)`**.

  Las actualizaciones de `.fx/configs/config.dev.json` son:

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

3. Puede crear un nuevo entorno y asignarle `staging` un nombre si no existe.
4. Abra el archivo `.fx/configs/config.staging.json`de configuración .
5. Actualice la misma propiedad `myapp(staging)`.
6. Ahora puede ejecutar el comando de aprovisionamiento en y `staging` el `dev` entorno para actualizar el nombre de la aplicación en entornos remotos. Para ejecutar el comando de aprovisionamiento con El kit de herramientas de Teams, consulte [aprovisionamiento](provision.md#provision-using-teams-toolkit).

</details>

<details>
<summary><b>Escenario 2: Personalizar la descripción de la aplicación de Teams para diferentes entornos</b></summary>

Puede establecer una descripción de aplicación de Teams diferente para los diferentes entornos:

* Para el entorno `dev`predeterminado , la descripción es `my app description for dev`.
* Para el entorno `staging`de ensayo , la descripción es `my app description for staging`.

Pasos para la personalización:

1. Abra el archivo `.fx/configs/config.dev.json`de configuración .
2. Agregue una nueva propiedad de **`manifest`** >  > **`description`****`short`** con el valor .**`my app description for dev`**

  Las actualizaciones de `.fx/configs/config.dev.json` son:

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
7. Actualice la propiedad **`description`** > **`short`** para usar la **variable** definida en configurar archivos con sintaxis **`{{config.manifest.description.short}}`** de mustache .
  
  Las actualizaciones de `manifest.template.json` son:

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

8. Ahora puede ejecutar el comando de aprovisionamiento en `dev` y `staging` el entorno para actualizar el nombre de la aplicación en entornos remotos.

</details>

<details>
<summary><b>Escenario 3: Personalizar la descripción de la aplicación de Teams para todos los entornos</b></summary>

Puede establecer la descripción de la aplicación `my app description` de Teams en para todos los entornos.

A medida que se comparte la plantilla de manifiesto de la aplicación de Teams en todos los entornos, podemos actualizar el valor de la descripción en ella para nuestro destino:

1. Abra la plantilla `templates/appPackage/manifest.template.json`de manifiesto de aplicación de Teams .
2. Actualice la propiedad **`description`** > **`short`** con una cadena **`my app description`** codificada de forma rígida.
  
  Las actualizaciones de `manifest.template.json` son:

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

3. Ahora puede ejecutar el comando de aprovisionamiento en **todo** el entorno para actualizar el nombre de la aplicación en entornos remotos.

</details>

<details>
<br><summary><b>Escenario 4: Personalización de recursos de Azure para diferentes entornos</b></summary>

Puede personalizar los recursos de Azure para cada entorno, por ejemplo, editar el entorno correspondiente a fx/configs/azure.parameters. {env}.json para especificar el nombre de la función de Azure.

Para obtener más información sobre los archivos de plantilla y parámetros de Bicep, consulte [aprovisionamiento de recursos en la nube](provision.md).
</details>
</br>

## <a name="see-also"></a>Vea también

* [Aprovisionar recursos en la nube](provision.md)
* [Incorporación de más recursos en la nube](add-resource.md)
* [Colaborar con otros desarrolladores en proyectos de Teams](TeamsFx-collaboration.md)
* [Prueba del comportamiento de la aplicación en un entorno diferente](test-app-behavior.md)

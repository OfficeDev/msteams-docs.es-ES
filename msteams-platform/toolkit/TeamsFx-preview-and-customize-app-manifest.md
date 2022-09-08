---
title: Personalizar el manifiesto de la aplicación de Teams en el kit de herramientas de Teams
author: zyxiaoyuer
description: En este módulo, aprenderá a editar, obtener una vista previa y personalizar el manifiesto de aplicación de Teams en el entorno diferente.
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/13/2022
ms.openlocfilehash: 3828c357307c5f7bfd94935a75dc9d6f5cedbc39
ms.sourcegitcommit: c806c5ffe277c740d0d7b8f62e72ade562029194
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617792"
---
# <a name="customize-teams-app-manifest"></a>Personalizar manifiesto de aplicación de Teams

El manifiesto de aplicación de Teams describe cómo se integra la aplicación en el producto de Microsoft Teams. Para obtener más información sobre el manifiesto, consulte [Esquema de manifiesto de aplicación para Teams](../resources/schema/manifest-schema.md). En esta sección se describen estos temas:

* [Vista previa del archivo de manifiesto en el entorno local](#preview-manifest-file-in-local-environment)
* [Vista previa del archivo de manifiesto en un entorno remoto](#preview-manifest-file-in-remote-environment)
* [Sincronización de cambios locales en el Portal de desarrollo](#sync-local-changes-to-dev-portal)
* [Personalización del manifiesto de aplicación de Teams](#customize-your-teams-app-manifest)
* [Validar manifiesto](#validate-manifest)

El archivo `manifest.template.json` de plantilla de manifiesto está disponible en la `templates/appPackage` carpeta después del scaffolding. El archivo de plantilla con marcadores de posición y los valores reales se resuelven mediante el kit de herramientas de Teams mediante archivos en `.fx/configs` y `.fx/states` para diferentes entornos.

Para obtener una vista previa del manifiesto con contenido real, Teams Toolkit genera archivos de manifiesto de vista previa en la `build/appPackage` carpeta :

```text
└───build
    └───appPackage
        ├───appPackage.{env}.zip - Zipped app package of remote Teams app
        ├───appPackage.local.zip - Zipped app package of local Teams app
        ├───manifest.{env}.json  - Previewed manifest of remote Teams app
        └───manifest.local.json  - Previewed manifest of local Teams app
```

Puede obtener una vista previa del archivo de manifiesto en entornos locales y remotos.

* [Vista previa del archivo de manifiesto en el entorno local](#preview-manifest-file-in-local-environment)
* [Vista previa del archivo de manifiesto en un entorno remoto](#preview-manifest-file-in-remote-environment)

## <a name="preview-manifest-file-in-local-environment"></a>Vista previa del archivo de manifiesto en el entorno local

Para obtener una vista previa del archivo de manifiesto en el entorno local, puede presionar **F5** para ejecutar la depuración local. Genera la configuración local predeterminada automáticamente y, a continuación, el paquete de la aplicación y la vista previa del manifiesto se compilan en la carpeta `build/appPackage`.

También puede obtener una vista previa del archivo de manifiesto local mediante dos métodos

* Mediante la opción de vista previa en codelens
* Mediante **la opción de paquete de metadatos de Zip Teams**

Los pasos siguientes ayudan a obtener una vista previa del archivo de manifiesto local mediante la opción de vista previa en codelens:

1. Seleccione **Preview (Vista previa**) en codelens of file (Versión preliminar) en el archivo codelens.`manifest.template.json`

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Vista previa":::

1. Seleccione **local**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-env1.png" alt-text="Seleccionar entorno1":::

Los pasos siguientes ayudan a obtener una vista previa del archivo de manifiesto local mediante **la opción paquete de metadatos zip de Teams** :

1. Seleccione `manifest.template.json` archivo.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manifest-json.png" alt-text="Seleccionar manifiesto":::

1. Seleccione el icono kit de herramientas de :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: Teams en la barra de herramientas de Visual Studio Code.

1. Seleccione **Zip Teams metadata package (Paquete de metadatos de Teams** ) en **DEPLOYMENT (IMPLEMENTACIÓN**).

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-metadata-package.png" alt-text="Selección del paquete de metadatos de Teams":::

1. Seleccione **local**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-env1.png" alt-text="Seleccionar entorno":::

La galería de ejemplos aparece como se muestra en la siguiente imagen:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Versión preliminar":::

## <a name="preview-manifest-file-in-remote-environment"></a>Vista previa del archivo de manifiesto en un entorno remoto

Para obtener una vista previa del archivo de manifiesto mediante Visual Studio Code:

* Seleccione **Aprovisionar en la nube en** **DESARROLLO** en la extensión del kit de herramientas de Teams.
  
  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/provision.png" alt-text="Aprovisionamiento de recursos en la nube":::

Para obtener una vista previa del archivo de manifiesto mediante el comando palatte:

* Desencadenar **teams: aprovisionamiento en la nube desde la** paleta de comandos.

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/command palatte.png" alt-text="Aprovisionamiento de recursos en la nube mediante la palata de comandos":::

Genera la configuración para la aplicación remota de Teams y compila el paquete y el manifiesto de vista previa en la `build/appPackage` carpeta .

También puede obtener una vista previa del archivo de manifiesto mediante dos métodos en el entorno remoto.

* Mediante la opción de vista previa en codelens
* Mediante **la opción de paquete de metadatos de Zip Teams**

Los pasos siguientes ayudan a obtener una vista previa del archivo de manifiesto mediante la opción de vista previa en codelens:

1. Seleccione **Preview (Vista previa**) en codelens of file (Versión preliminar) en el archivo codelens.`manifest.template.json`

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Vista previa":::

1. Seleccione el entorno.

   > [!NOTE]
   > Si hay más de un entorno, debe seleccionar el entorno del que desea obtener una vista previa, como se muestra en la imagen:

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="Agregar entorno":::

Los pasos siguientes ayudan a obtener una vista previa del archivo de manifiesto mediante **la opción paquete de metadatos de Zip Teams** en el entorno remoto:

1. Seleccione `manifest.template.json` archivo.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manifest-json.png" alt-text="Seleccionar manifiesto":::

1. Seleccione el icono kit de herramientas de :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: Teams en la barra de herramientas de Visual Studio Code.

1. Seleccione **Zip Teams metadata package (Paquete de metadatos de Teams** ) en **DEPLOYMENT (IMPLEMENTACIÓN**).

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-metadata-package.png" alt-text="Selección del paquete de metadatos de Teams":::

1. Seleccione el entorno.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="Agregar entorno":::

   > [!NOTE]
   > Si hay más de un entorno, debe seleccionar el entorno del que desea obtener una vista previa, como se muestra en la imagen:

## <a name="sync-local-changes-to-dev-portal"></a>Sincronización de cambios locales en el Portal de desarrollo

Después de obtener una vista previa del archivo de manifiesto, puede sincronizar los cambios locales con el Portal de desarrollo de las siguientes maneras:

> [!NOTE]
> Para obtener más información sobre el portal [para desarrolladores, consulte Portal para desarrolladores para Teams](../concepts/build-and-test/teams-developer-portal.md).

1. Implementar el manifiesto de aplicación de Teams.

   Puede implementar el manifiesto de aplicación de Teams de cualquiera de las siguientes maneras:

   * Vaya al `manifest.template.json` archivo y haga clic con el botón derecho para seleccionar `Deploy Teams app manifest` en el menú contextual.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-manifest.png" alt-text="Implementar manifiesto":::

   * Desencadenador `Teams: Deploy Teams app manifest` desde la paleta de comandos.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-command.png" alt-text="Implementación desde la paleta de comandos":::

2. Actualice a la plataforma teams.

   Puede actualizar a la plataforma Teams de cualquiera de las siguientes maneras:

   * Seleccione **Actualizar a la plataforma de Teams** en la esquina superior izquierda de `manifest.{env}.json`.

   * Desencadenar **Teams: actualice el manifiesto a la plataforma Teams** en la barra de menús de `manifest.{env}.json`.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/update-to-teams.png" alt-text="Actualización a los equipos":::

También puede desencadenar **Teams: Actualizar manifiesto a la plataforma Teams** desde la paleta de comandos:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="vista de árbol":::

> [!NOTE]
> El desencadenador de codelens del editor o la barra de menús actualiza el archivo de manifiesto actual a la plataforma Teams. El desencadenador de la paleta de comandos requiere seleccionar el entorno de destino.

 Comando de la CLI:

``` bash
        teamsfx deploy manifest --include-app-manifest yes
```

---

> [!NOTE]
> El cambio se actualiza en el Portal de desarrollo. Las actualizaciones manuales del Portal de desarrollo se sobrescriben.

Si el archivo de manifiesto no está actualizado debido al cambio de archivo de configuración o al cambio de plantilla, seleccione cualquiera de las siguientes acciones:

* **Solo versión preliminar**: el archivo de manifiesto local se sobrescribe según la configuración actual.
* **Versión preliminar y actualización**: el archivo de manifiesto local se sobrescribe según la configuración actual y también se actualiza a la plataforma Teams.
* **Cancelar**: no se realiza ninguna acción.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="pre":::

## <a name="customize-your-teams-app-manifest"></a>Personalización del manifiesto de aplicación de Teams

El kit de herramientas de Teams consta de los siguientes archivos de plantilla de manifiesto en la carpeta `manifest.template.json` en entornos locales y remotos:

* `manifest.template.json`
* `templates/appPackage`

Durante la depuración o el aprovisionamiento local, el kit de herramientas de Teams carga el manifiesto desde `manifest.template.json`, con las configuraciones de `state.{env}.json`, `config.{env}.json`y crea la aplicación teams en [el Portal de desarrollo](https://dev.teams.microsoft.com/apps).

### <a name="supported-placeholders-in-manifesttemplatejson"></a>Marcadores de posición admitidos en manifest.template.json

En la lista siguiente se proporcionan marcadores de posición admitidos en `manifest.template.json`:

* `{{state.xx}}` es un marcador de posición predefinido y el kit de herramientas de Teams resuelve su valor, definido en `state.{env}.json`. Asegúrese de no modificar los valores en `state.{env}.json`
* `{{config.manifest.xx}}` es un marcador de posición personalizado y su valor se resuelve desde `config.{env}.json`

**Para agregar un parámetro personalizado**

1. Agregue el parámetro personalizado como se indica a continuación:</br>
   a. Agregue un marcador de posición en `manifest.template.json` con el patrón `{{config.manifest.xx}}`.</br>
   b. Agregue un valor de configuración en `config.{env}.json`.

     ```json
     {
         "manifest": {
          "KEY": "VALUE"
          }
     }
     ```

2. Puede navegar al archivo de configuración seleccionando cualquiera de los marcadores de posición de configuración **Ir al archivo de configuración** o **Ver el archivo de estado** en `manifest.template.json`.

### <a name="validate-manifest"></a>Validar manifiesto

Durante operaciones como, por ejemplo, **el paquete de metadatos zip de Teams**, teams Toolkit valida el manifiesto en su esquema. En la lista siguiente se proporcionan diferentes formas de validar el manifiesto:

* En VSC, desencadene `Teams: Validate manifest file` desde la paleta de comandos:

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/validate.png" alt-text="Validar archivo":::

* En la CLI, use el comando :

     ``` bash
        teamsfx validate --env local
        teamsfx validate --env dev
        ```

---

## To preview values for local and dev environment

In `manifest.template.json`, you can navigate to codelens to preview the values for `local` and `dev` environment.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/codelens.png" alt-text="Preview values":::

> [!NOTE]
> Provision the environment or execute local debug to generate values for placeholders.

You can navigate to state file or configuration file by selecting the codelens, which provides a drop-down list with all the environment names. After selecting one environment, the corresponding state file or configuration file opens.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-environment.png" alt-text="Select your environment":::

To preview values for all the environments, you can hover over the placeholder. It shows a list with environment names and corresponding values. If you haven't provisioned the environment or executed the local debug, select `Trigger Teams: Provision in the cloud command to see placeholder value` or `Trigger local debug to see placeholder value`.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/hover.png" alt-text="Preview all values":::

## See also

* [Manage multiple environments](TeamsFx-multi-env.md)
* [Reference: Manifest schema for Microsoft Teams](../resources/schema/manifest-schema.md)
* [Public developer preview for Microsoft Teams](../resources/dev-preview/developer-preview-intro.md)

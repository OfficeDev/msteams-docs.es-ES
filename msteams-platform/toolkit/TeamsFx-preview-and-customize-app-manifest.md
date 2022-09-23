---
title: Personalizar el manifiesto de la aplicación de Teams en el kit de herramientas de Teams
author: zyxiaoyuer
description: En este módulo, aprenderá a editar, obtener una vista previa y personalizar el manifiesto de aplicación de Teams en el entorno diferente.
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/13/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 2a06953ede09d9486dab239557a4941c590c882b
ms.sourcegitcommit: ef545fac5c0dbe970d81f53b1631930e9196eba3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/23/2022
ms.locfileid: "67991666"
---
# <a name="customize-teams-app-manifest"></a>Personalizar manifiesto de aplicación de Teams

El manifiesto de aplicación de Teams describe cómo se integra la aplicación en el producto de Microsoft Teams.

::: zone pivot="visual-studio-code"

## <a name="customize-teams-app-manifest-for-visual-studio-code"></a>Personalización del manifiesto de aplicación de Teams para Visual Studio Code

El manifiesto de aplicación de Teams describe cómo se integra la aplicación en el producto de Microsoft Teams. Para obtener más información sobre el manifiesto, consulte [Esquema de manifiesto de aplicación para Teams](../resources/schema/manifest-schema.md). En esta sección se describen estos temas:

* [Vista previa del archivo de manifiesto en el entorno local](#preview-manifest-file-in-local-environment)
* [Vista previa del archivo de manifiesto en un entorno remoto](#preview-manifest-file-in-remote-environment)
* [Sincronización de cambios locales en el portal para desarrolladores](#sync-local-changes-to-developer-portal)
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

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Captura de pantalla de un ejemplo que muestra la vista previa en el archivo codelens del manifiesto.":::

1. Seleccione **local**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-env1.png" alt-text="La captura de pantalla es un ejemplo de cómo mostrar la selección de local en el entorno.":::

Los pasos siguientes ayudan a obtener una vista previa del archivo de manifiesto local mediante **la opción paquete de metadatos zip de Teams** :

1. Seleccione `manifest.template.json` archivo.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manifest-json.png" alt-text="Captura de pantalla que muestra la selección de manifest.template.json.":::

1. Seleccione el icono kit de herramientas de :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: Teams en la barra de herramientas de Visual Studio Code.

1. Seleccione **Zip Teams metadata package (Paquete de metadatos de Teams** ) en **DEPLOYMENT (IMPLEMENTACIÓN**).

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-metadata-package.png" alt-text="Captura de pantalla que muestra la selección del paquete de metadatos zip de Teams.":::

1. Seleccione **local**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-env1.png" alt-text="La captura de pantalla es un ejemplo de cómo mostrar la selección de local en el entorno.":::

La galería de ejemplos aparece como se muestra en la siguiente imagen:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="La captura de pantalla es un ejemplo de cómo mostrar la vista previa de local.":::

## <a name="preview-manifest-file-in-remote-environment"></a>Vista previa del archivo de manifiesto en un entorno remoto

Para obtener una vista previa del archivo de manifiesto mediante Visual Studio Code:

* Seleccione **Aprovisionar en la nube en** **DESARROLLO** en la extensión del kit de herramientas de Teams.
  
  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/provision.png" alt-text="La captura de pantalla es un ejemplo de cómo mostrar la selección de aprovisionamiento en el recurso en la nube.":::

Para obtener una vista previa del archivo de manifiesto mediante el comando palatte:

* Desencadenar **teams: aprovisionamiento en la nube desde la** paleta de comandos.

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/command palatte.png" alt-text="Captura de pantalla que muestra un ejemplo de aprovisionamiento de recursos en la nube mediante la palata de comandos.":::

Genera la configuración para la aplicación remota de Teams y compila el paquete y el manifiesto de vista previa en la `build/appPackage` carpeta .

También puede obtener una vista previa del archivo de manifiesto mediante dos métodos en el entorno remoto.

* Mediante la opción de vista previa en codelens
* Mediante **la opción de paquete de metadatos de Zip Teams**

Los pasos siguientes ayudan a obtener una vista previa del archivo de manifiesto mediante la opción de vista previa en codelens:

1. Seleccione **Preview (Vista previa**) en codelens of file (Versión preliminar) en el archivo codelens.`manifest.template.json`

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Captura de pantalla que muestra una vista previa en el archivo codelens del manifiesto.":::

1. Seleccione el entorno.

   > [!NOTE]
   > Si hay más de un entorno, debe seleccionar el entorno del que desea obtener una vista previa, como se muestra en la imagen:

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="La captura de pantalla es un ejemplo de cómo mostrar la adición de un entorno.":::

Los pasos siguientes ayudan a obtener una vista previa del archivo de manifiesto mediante **la opción paquete de metadatos de Zip Teams** en el entorno remoto:

1. Seleccione `manifest.template.json` archivo.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manifest-json.png" alt-text="Captura de pantalla que muestra la selección de manifest.template.json.":::

1. Seleccione el icono kit de herramientas de :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: Teams en la barra de herramientas de Visual Studio Code.

1. Seleccione **Zip Teams metadata package (Paquete de metadatos de Teams** ) en **DEPLOYMENT (IMPLEMENTACIÓN**).

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-metadata-package.png" alt-text="Captura de pantalla que muestra la selección del paquete de metadatos zip de Teams.":::

1. Seleccione el entorno.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="La captura de pantalla es un ejemplo de cómo mostrar la adición de un entorno.":::

   > [!NOTE]
   > Si hay más de un entorno, debe seleccionar el entorno del que desea obtener una vista previa, como se muestra en la imagen:

## <a name="sync-local-changes-to-developer-portal"></a>Sincronización de cambios locales en el portal para desarrolladores

Después de obtener una vista previa del archivo de manifiesto, puede sincronizar los cambios locales con el Portal para desarrolladores de las siguientes maneras:

> [!NOTE]
> Para obtener más información en el Portal para [desarrolladores, vea Portal para desarrolladores para Teams](../concepts/build-and-test/teams-developer-portal.md).

1. Implementar el manifiesto de aplicación de Teams.

   Puede implementar el manifiesto de aplicación de Teams de cualquiera de las siguientes maneras:

   * Vaya al `manifest.template.json` archivo y haga clic con el botón derecho para seleccionar `Deploy Teams app manifest` en el menú contextual.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-manifest.png" alt-text="Captura de pantalla que muestra la selección del manifiesto de implementación de aplicaciones de Teams.":::

   * Desencadenador `Teams: Deploy Teams app manifest` desde la paleta de comandos.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-command.png" alt-text="La captura de pantalla es un ejemplo de cómo mostrar la implementación desde la paleta de comandos.":::

2. Actualice a la plataforma teams.

   Puede actualizar a la plataforma Teams de cualquiera de las siguientes maneras:

   * Seleccione **Actualizar a la plataforma de Teams** en la esquina superior izquierda de `manifest.{env}.json`.

   * Desencadenar **Teams: actualice el manifiesto a la plataforma Teams** en la barra de menús de `manifest.{env}.json`.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/update-to-teams.png" alt-text="Captura de pantalla que muestra la actualización a la plataforma Teams en la barra de menús del manifiesto.":::

También puede desencadenar **Teams: Actualizar manifiesto a la plataforma Teams** desde la paleta de comandos:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="Captura de pantalla que muestra la selección de Teams: actualizar el manifiesto a la plataforma teams desde la paleta de comandos.":::

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

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="La captura de pantalla es un ejemplo de las opciones de visualización, navegación para seleccionar solo vista previa, vista previa y actualización y cancelación cuando el archivo de manifiesto está obsoleto debido al cambio de plantilla o configuración.":::

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

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/validate.png" alt-text="La captura de pantalla es un ejemplo de cómo mostrar teams validar el archivo de manifiesto desde la paleta de comandos.":::

* En la CLI, use el comando :

     ``` bash
        teamsfx validate --env local
        teamsfx validate --env dev
        ```

---

## To preview values for local and dev environment

In `manifest.template.json`, you can navigate to codelens to preview the values for `local` and `dev` environment.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/codelens.png" alt-text="Screenshot is an example of showing preview values for local and dev environment.":::

> [!NOTE]
> Provision the environment or execute local debug to generate values for placeholders.

You can navigate to state file or configuration file by selecting the codelens, which provides a drop-down list with all the environment names. After selecting one environment, the corresponding state file or configuration file opens.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-environment.png" alt-text="Screenshot is an example of showing the selection of an environment.":::

To preview values for all the environments, you can hover over the placeholder. It shows a list with environment names and corresponding values. If you haven't provisioned the environment or executed the local debug, select `Trigger Teams: Provision in the cloud command to see placeholder value` or `Trigger local debug to see placeholder value`.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/hover.png" alt-text="Screenshot is an example of showing the preview values for all environments.":::

::: zone-end

::: zone pivot="visual-studio"

## Edit Teams app manifest using Visual Studio

Teams Toolkit in Visual Studio loads manifest from `manifest.template.json` with configurations from `state.{env}.json` and `config.{env}.json` while provisioning and preparing app dependencies. You can also create Microsoft Teams app in [Developer Portal](https://dev.teams.microsoft.com/apps) with the manifest.

After scaffolding, in the manifest template file under `templates/appPackage` folder,
`manifest.template.json` is shared between local and remote environment.

In the manifest template, select **Project** > **Teams Toolkit** > **Open Manifest File**.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-open-manifest.png" alt-text="Screenshot is an example of showing the navigation to open manifest file." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-open-manifest.png":::

### Customize app manifest in Teams Toolkit

There are two types of placeholders in `manifest.template.json`:

* `{{state.xx}}` is pre-defined placeholder, whose value is resolved by Teams Toolkit, defined in `state.{env}.json`. It's recommended to not modify the values in `state.{env}.json`.
* `{{config.manifest.xx}}` is customized placeholder, whose value is resolved from `config.{env}.json`.

You can add a customized parameter by:

* Adding a placeholder in `manifest.template.json` with pattern: `{{config.manifest.xx}}`.
* Adding a config value in `config.{env}.json`.

    ```
        {
            "manifest": {
            "KEY": "VALUE"
            }
    }
    ```

### Preview app manifest in Teams Toolkit

You can preview values in app manifest in two ways:

* When you hover over the placeholder in `manifest.template.json`, then you can see the values for **dev** and **local** environment.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-placeholder1.png" alt-text="Screenshot is an example showing when you hover over placeholder, can view the values for dev and local environment." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-placeholder1.png":::

* You can also hover over the key besides each placeholder in `manifest.template.json`, and you can see the same values for **dev** and **local** environment.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-key-placeholder.png" alt-text="Screenshot is an example showing when you hover over key beside placeholder can view the same values for dev and local environment." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-key-placeholder.png":::

   > [!NOTE]
   > If the environment has not been provisioned, or the Teams app dependencies have not been prepared, it indicates that the values for placeholder have not been generated. Please follow the guidance inside hover to generate corresponding values.

### Preview manifest file

To preview the manifest file, you can sideload for local or deploy for Azure. You can preview the manifest file by performing the following step:

* Select **Project** > **Teams Toolkit** and trigger **Prepare Teams App Dependencies** or **Provision in the Cloud** that generates configuration for local or remote Teams app.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview-manifest1.png" alt-text="Screenshot is an example of showing preview manifest file." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview-manifest1.png":::

There are two other ways to upload zip app package before you can preview manifest file:

1. From the list of menu select **Project** > **Teams Toolkit** > **Zip App Package**, and select **For Local** or **For Azure**.

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-zip1.png" alt-text="Screenshot is an example of showing the navigation to zip app package for local and azure." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-zip1.png":::

1. You can also upload zip app package from Solution Explorer, if you right-click on **MyTeamsApp1** and then select **Teams Toolkit** > **Zip App Package** > **For Local** or **For Azure**.

  > [!NOTE]
  > In this scenario the project name is **MyTeamsApp1**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-solution-explorer1.png" alt-text="Screenshot is an example of showing the list of Teams toolkit menus from solution explorer." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-solution-explorer1.png":::

Teams Toolkit generates the zip app package, and to preview manifest file content you can follow the step below:

* Right-click on **manifest.template.json** under **appPackage** folder, select **Preview Manifest File** > **For Local** or **For Azure**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview1.png" alt-text="Screenshot is an example of showing the preview manifest menu for local and azure." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview1.png":::

This displays the preview of the manifest file in Visual Studio.

### Sync local changes to Developer Portal

After you've previewed the manifest file in Visual Studio, you can now sync the local changes to the Developer Portal. Select **Project** > **Teams Toolkit** > **Update Manifest in Teams Developer Portal**, or context menu from Solution Explorer. You can now preview the manifest file in Developer Portal as a result of syncing the local changes.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-update-manifest1.png" alt-text="Screenshot is an example of showing the navigation to update manifest in Teams developer portal." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-update-manifest1.png":::

The changes are updated to Teams Developer Portal.

> [!NOTE]
>
> * Select **Overwrite and update** or **Cancel** from the **Warning** dialog box to make any maual updates that can be overwritten in the Develope Portal.
> * When you create a Teams command bot using Visual Studio, two app IDs are registered in Azure Active Directory. You can identify the app IDs in the Developer Portal as **Application client ID** under Basic information and existing **Bot ID** under **App features**.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-overwrite.png" alt-text="Screenshot is an example of showing the update warning." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-overwrite.png":::

::: zone-end

## See also

* [Manage multiple environments](TeamsFx-multi-env.md)
* [Reference: Manifest schema for Microsoft Teams](../resources/schema/manifest-schema.md)
* [Public developer preview for Microsoft Teams](../resources/dev-preview/developer-preview-intro.md)

* [Provision cloud resources using Visual Studio](provision-cloud-resources.md)

* [Deploy Teams app to the cloud using Visual Studio](deploy-teams-app.md)

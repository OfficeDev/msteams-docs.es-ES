---
title: Manifiesto de aplicación de Teams en Teams Toolkit
author: zyxiaoyuer
description: En este módulo, aprenderá a editar, obtener una vista previa y personalizar Teams manifiesto de aplicación en el entorno diferente.
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/13/2022
ms.openlocfilehash: 505f5aeaf6cdae995efd182535c4d5a8814f9ea1
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143875"
---
# <a name="edit-teams-app-manifest"></a>Edición Teams manifiesto de aplicación

El archivo `manifest.template.json` de plantilla de manifiesto está disponible en la `templates/appPackage` carpeta después del scaffolding. El archivo de plantilla con marcadores de posición y los valores reales se resuelven Teams Toolkit mediante archivos en `.fx/configs` y `.fx/states` para diferentes entornos.

**Para obtener una vista previa del manifiesto con contenido real, Teams Toolkit genera archivos de manifiesto de vista previa en la `build/appPackage` carpeta** :

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

También puede obtener una vista previa del archivo de manifiesto local siguiendo estos pasos:

1. Seleccione **Preview (Vista previa** ) en codelens of file (Versión preliminar) en `manifest.template.json` el archivo y seleccione **local**.
2. Seleccione **Vista previa del archivo de manifiesto** en la barra de menús del `manifest.template.json` archivo.
3. Seleccione **Zip Teams paquete de metadatos** en Treeview y seleccione **local**.

La galería de ejemplos aparece como se muestra en la siguiente imagen:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Versión preliminar":::

## <a name="preview-manifest-file-in-remote-environment"></a>Vista previa del archivo de manifiesto en un entorno remoto

**Para obtener una vista previa del archivo de manifiesto en un entorno remoto**

* Seleccione **Aprovisionar en la nube** en **DESARROLLO** en Teams Toolkit extensión o
* Desencadenar **Teams: aprovisionamiento en la nube desde la** paleta de comandos.

Genera la configuración de la aplicación Teams remota y compila el paquete y el manifiesto de vista previa en la `build/appPackage` carpeta .

También puede obtener una vista previa del archivo de manifiesto en un entorno remoto siguiendo estos pasos:

1. Seleccione **Preview (Vista previa**) en codelens of file (Versión preliminar) en el archivo codelens.`manifest.template.json`
2. Seleccione **Vista previa del archivo de manifiesto** en la barra de menús del `manifest.template.json` archivo.
3. Seleccione **Zip Teams paquete de metadatos** en Treeview.
4. Seleccione el entorno.

> [!NOTE]
> Si hay más de un entorno, debe seleccionar el entorno del que desea obtener una vista previa, como se muestra en la imagen:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="Agregar entorno":::

## <a name="sync-local-changes-to-dev-portal"></a>Sincronización de cambios locales en el Portal de desarrollo

Después de obtener una vista previa del archivo de manifiesto, puede sincronizar los cambios locales con el Portal de desarrollo de las siguientes maneras:

1. Implementar Teams manifiesto de aplicación.

   Puede implementar Teams manifiesto de aplicación de cualquiera de las siguientes maneras:

   * Vaya al `manifest.template.json` archivo y haga clic con el botón derecho para seleccionar `Deploy Teams app manifest` en el menú contextual.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-manifest.png" alt-text="Implementar manifiesto":::

   * Desencadenador `Teams: Deploy Teams app manifest` desde la paleta de comandos.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-command.png" alt-text="Implementación desde la paleta de comandos":::

2. Actualice a Teams plataforma.

   Puede actualizar a Teams plataforma de cualquiera de las siguientes maneras:

   * Seleccione **Actualizar para Teams plataforma** en la esquina superior izquierda de `manifest.{env}.json`.

   * Desencadenar **Teams: actualice el manifiesto a Teams plataforma** en la barra de menús de `manifest.{env}.json`.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/update-to-teams.png" alt-text="Actualización a los equipos":::

También puede desencadenar **Teams: Actualizar manifiesto a Teams plataforma** desde la paleta de comandos:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="vista de árbol":::

> [!NOTE]
> El desencadenador de codelens del editor o la barra de menús actualiza el archivo de manifiesto actual a Teams plataforma. El desencadenador de la paleta de comandos requiere seleccionar el entorno de destino.

 Comando de la CLI:

``` bash
        teamsfx deploy manifest --include-app-manifest yes
```

---

> [!NOTE]
> El cambio se actualiza en el Portal de desarrollo. Las actualizaciones manuales del Portal de desarrollo se sobrescriben.

Si el archivo de manifiesto no está actualizado debido al cambio de archivo de configuración o al cambio de plantilla, seleccione cualquiera de las siguientes acciones:

* **Solo versión preliminar**: el archivo de manifiesto local se sobrescribe según la configuración actual.
* **Versión preliminar y actualización**: el archivo de manifiesto local se sobrescribe según la configuración actual y también se actualiza a Teams plataforma.
* **Cancelar**: no se realiza ninguna acción.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="pre" border="true":::

## <a name="customize-teams-app-manifest"></a>Personalizar manifiesto de aplicación de Teams

El kit de herramientas de Teams consta de los siguientes archivos de plantilla de manifiesto en la carpeta `manifest.template.json` en entornos locales y remotos:

* `manifest.template.json`
* `templates/appPackage`

Durante la depuración o aprovisionamiento local, Teams Toolkit carga el manifiesto desde `manifest.template.json`, con las configuraciones de `state.{env}.json`, `config.{env}.json`y crea Teams aplicación en [el Portal de desarrollo](https://dev.teams.microsoft.com/apps).

## <a name="supported-placeholders-in-manifesttemplatejson"></a>Marcadores de posición admitidos en manifest.template.json

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

Durante operaciones como, **zip Teams paquete de metadatos**, Teams Toolkit valida el manifiesto con su esquema. En la lista siguiente se proporcionan diferentes formas de validar el manifiesto:

* En VSC, desencadene `Teams: Validate manifest file` desde la paleta de comandos:

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/validate.png" alt-text="Validar archivo":::

* En la CLI, use el comando :

     ``` bash
        teamsfx validate --env local
        teamsfx validate --env dev
        ```

---

## Codelenses and hovers

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

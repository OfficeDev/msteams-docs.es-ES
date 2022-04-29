---
title: Vista previa del manifiesto de la aplicación de Teams en el kit de herramientas de Teams
author: zyxiaoyuer
description: Vista previa del manifiesto de la aplicación de Teams
ms.author: nliu
ms.localizationpriority: high
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 91bc070d30136ce1f004676172594f26ca37dea5
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111874"
---
# <a name="preview-app-manifest-in-toolkit"></a>Vista previa del manifiesto de aplicación en el kit de herramientas

El archivo `manifest.template.json` de plantilla de manifiesto está disponible en la `templates/appPackage` carpeta después del scaffolding. El archivo de plantilla con marcadores de posición y los valores reales se resuelven en el kit de herramientas de Teams desde los archivos en `.fx/configs` y `.fx/states` para diferentes entornos.

## <a name="prerequisite"></a>Requisito previo

* Instale la [versión más reciente del kit de herramientas de Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

> [!TIP]
> Asegúrese de que ha abierto el proyecto de aplicación de Teams en Visual Studio código.

## <a name="preview-manifest"></a>Vista previa del manifiesto

Para obtener una vista previa del manifiesto con contenido real, el kit de herramientas de Teams genera archivos de manifiesto de vista previa en la carpeta `build/appPackage`:

```text
└───build
    └───appPackage
        ├───appPackage.{env}.zip - Zipped app package of remote teams app
        ├───appPackage.local.zip - Zipped app package of local team app
        ├───manifest.{env}.json  - Previewed manifest of remote teams app
        └───manifest.local.json  - Previewed manifest of local teams app
```

### <a name="preview-local-manifest-file"></a>Vista previa del archivo de manifiesto local

Para obtener una vista previa del archivo de manifiesto de la aplicación de Teams local, puede presionar **F5** para ejecutar la depuración local. Genera la configuración local predeterminada automáticamente y, a continuación, el paquete de la aplicación y la vista previa del manifiesto se compilan en la carpeta `build/appPackage`.

También puede obtener una vista previa del manifiesto local siguiendo estos pasos:

1. Seleccione **Vista previa** en el codelens del `manifest.template.json` archivo y seleccione **local**.
2. Seleccione **Vista previa del archivo de manifiesto** en la barra de menús del archivo `manifest.template.json`.
3. Seleccione **paquete zip de metadatos de Teams** en vista de árbol y seleccione **local**.

La galería de ejemplos aparece como se muestra en la siguiente imagen:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Versión preliminar":::

### <a name="preview-manifest-in-remote-environment"></a>Vista previa del manifiesto en un entorno remoto

Para obtener una vista previa del archivo de manifiesto de la aplicación remota de Teams, seleccione **Aprovisionar en la nube** en el panel **DESARROLLO** de la extensión del kit de herramientas de Teams en vista de árbol, o desencadenar **Teams: Aprovisionamiento en la nube** desde la paleta de comandos. Genera la configuración de la aplicación de Teams remota y compila el paquete y el manifiesto de vista previa en la carpeta `build/appPackage`.

También puede obtener una vista previa del manifiesto en un entorno remoto siguiendo estos pasos:

1. Seleccione **Vista previa** en el codelens del archivo `manifest.template.json`
2. Seleccione **Vista previa del archivo de manifiesto** en la barra de menús del archivo `manifest.template.json`.
3. Seleccione **paquete zip de metadatos de Teams** en la vista de árbol
4. Seleccione el entorno

Si hay más de un entorno, debe seleccionar el entorno del que desea obtener una vista previa, como se muestra en la imagen:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="Agregar entorno":::

## <a name="sync-local-changes-to-developer-portal"></a>Sincronización de cambios locales en el portal para desarrolladores

Después de obtener una vista previa del archivo de manifiesto, puede sincronizar los cambios locales con el portal para desarrolladores siguiendo estos pasos:

1. Seleccione **Actualizar a la plataforma de Teams** en la esquina superior izquierda de`manifest.{env}.json`
2. Seleccione **Teams: Actualizar manifiesto a la plataforma de Teams** en la barra de menús de `manifest.{env}.json`

 También puede desencadenar **Teams: Actualizar manifiesto a la plataforma de Teams** desde la paleta de comandos:

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="vista de árbol":::

> [!NOTE]
> Desencadenar desde codelens del editor o el **título** actualiza el archivo de manifiesto actual a Teams plataforma. El desencadenador de la paleta de comandos requiere seleccionar el entorno de destino

  

Si el archivo de manifiesto no está actualizado debido al cambio de archivo de configuración o al cambio de plantilla, seleccione cualquiera de las siguientes acciones:

* **Solo versión preliminar**: el archivo de manifiesto local se sobrescribe según la configuración actual
* **Versión preliminar y actualización**: el archivo de manifiesto local se sobrescribe según la configuración actual y también se actualiza a Teams plataforma
* **Cancelar**: No se realiza ninguna acción.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="pre":::



> [!NOTE]
> Los cambios se actualizan en el portal para desarrolladores. Las actualizaciones manuales del portal de desarrolladores se sobrescriben.

## <a name="see-also"></a>Vea también

[Personalizar el manifiesto de aplicación de Teams en el kit de herramientas de Teams](TeamsFx-manifest-customization.md)

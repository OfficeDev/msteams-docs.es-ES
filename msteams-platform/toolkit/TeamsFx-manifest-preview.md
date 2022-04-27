---
title: Vista previa Teams manifiesto de aplicación en Teams Toolkit
author: zyxiaoyuer
description: Vista previa del manifiesto de la aplicación de Teams
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 57dc719f872d502beded14c30a09d72c27ee74c3
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073288"
---
# <a name="preview-app-manifest-in-toolkit"></a>Vista previa del manifiesto de aplicación en Toolkit

El archivo `manifest.template.json` de plantilla de manifiesto está disponible en la `templates/appPackage` carpeta después del scaffolding. El archivo de plantilla con marcadores de posición y los valores reales se resuelven Teams Toolkit de archivos en `.fx/configs` y `.fx/states` para diferentes entornos.

## <a name="prerequisite"></a>Requisito previo

* Instale la [versión más reciente de Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

> [!TIP]
> Asegúrese de que ha abierto Teams proyecto de aplicación en Visual Studio código.

## <a name="preview-manifest"></a>Manifiesto de vista previa

Para obtener una vista previa del manifiesto con contenido real, Teams Toolkit genera archivos de manifiesto de vista previa en la `build/appPackage` carpeta :

```text
└───build
    └───appPackage
        ├───appPackage.{env}.zip - Zipped app package of remote teams app
        ├───appPackage.local.zip - Zipped app package of local team app
        ├───manifest.{env}.json  - Previewed manifest of remote teams app
        └───manifest.local.json  - Previewed manifest of local teams app
```

### <a name="preview-local-manifest-file"></a>Vista previa del archivo de manifiesto local

Para obtener una vista previa del archivo de manifiesto de la aplicación de teams local, puede presionar **F5** para ejecutar la depuración local. Genera la configuración local predeterminada automáticamente y, a continuación, el paquete de la aplicación y el manifiesto de vista previa se compilan en la `build/appPackage` carpeta .

También puede obtener una vista previa del manifiesto local siguiendo estos pasos:

1. Seleccione **Vista previa** en el codelens del `manifest.template.json` archivo y seleccione **local**.
2. Seleccione **Preview manifest file (Vista previa del archivo de manifiesto** ) en la barra de menús del `manifest.template.json` archivo.
3. Seleccione **Zip Teams paquete de metadatos** en Treeview y seleccione **local**.

La vista previa local aparece como se muestra en la imagen:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Versión preliminar":::

### <a name="preview-manifest-in-remote-environment"></a>Vista previa del manifiesto en un entorno remoto

Para obtener una vista previa del archivo de manifiesto de la aplicación de Equipos remotos, seleccione **Aprovisionar en la nube en el** panel **DESARROLLO** de Teams Toolkit extensión Treeview o desencadenar **Teams: Aprovisionar en la nube desde la** paleta de comandos. Genera la configuración de la aplicación de Teams remota y compila el paquete y el manifiesto de vista previa en la `build/appPackage` carpeta .

También puede obtener una vista previa del manifiesto en un entorno remoto siguiendo estos pasos:

1. Seleccione **Preview (Vista previa**) en codelens of file (Versión preliminar) en el archivo codelens `manifest.template.json`
2. Seleccione **Preview manifest file (Vista previa del archivo de manifiesto** ) en la barra de menús del `manifest.template.json` archivo.
3. Seleccione **Zip Teams paquete de metadatos** en Treeview.
4. Selección del entorno

Si hay más de un entorno, debe seleccionar el entorno que desea obtener una vista previa, como se muestra en la imagen:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="Agregar env":::

## <a name="sync-local-changes-to-developer-portal"></a>Sincronización de cambios locales en el Portal para desarrolladores

Después de obtener una vista previa del archivo de manifiesto, puede sincronizar los cambios locales con el Portal para desarrolladores siguiendo estos pasos:

1. Seleccione **Actualizar para Teams plataforma** en la esquina superior izquierda de`manifest.{env}.json`
2. Seleccione **Teams: Actualizar manifiesto a Teams plataforma** en la barra de menús de`manifest.{env}.json`

 También puede desencadenar **Teams: Actualizar manifiesto a Teams plataforma** desde la paleta de comandos:

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="vista de árbol":::

> [!NOTE]
> Desencadenar desde codelens del editor o **el título** actualiza el archivo de manifiesto actual a Teams plataforma. El desencadenador de la paleta de comandos requiere seleccionar el entorno de destino.

  

Si el archivo de manifiesto no está actualizado debido al cambio de archivo de configuración o al cambio de plantilla, seleccione cualquiera de las siguientes acciones:

* **Solo versión preliminar**: el archivo de manifiesto local se sobrescribe según la configuración actual
* **Versión preliminar y actualización**: el archivo de manifiesto local se sobrescribe según la configuración actual y también se actualiza a Teams plataforma
* **Cancelar**: no se realiza ninguna acción

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="pre":::



> [!NOTE]
> Los cambios se actualizan en el Portal de desarrollo. Las actualizaciones manuales del portal de desarrollo se sobrescriben.

## <a name="see-also"></a>Ver también

[Personalizar Teams manifiesto de aplicación en Teams Toolkit](TeamsFx-manifest-customization.md)

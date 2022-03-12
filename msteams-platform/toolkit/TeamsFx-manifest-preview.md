---
title: Vista Teams manifiesto de aplicación en Teams Toolkit
author: zyxiaoyuer
description: Vista previa del manifiesto de la aplicación de Teams
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: aa80636a4fdb3c27d66bc08f9d308a009e183570
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453246"
---
# <a name="preview-teams-app-manifest-in-teams-toolkit"></a>Vista Teams manifiesto de la aplicación en Teams Toolkit

Después de scaffolding, los siguientes son los archivos de plantilla de manifiesto disponibles en la `templates/appPackage` carpeta:

* `manifest.local.template.json` - Aplicación de equipos de depuración local.
* `manifest.remote.template.json` - compartido entre todos los entornos remotos.

Los archivos Template que constan de marcadores de posición y los valores reales de Teams Toolkit se resuelven en archivos en `.fx/configs` y `.fx/states`.

## <a name="prerequisite"></a>Requisito previo

* [Instale Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión 3.0.0+.

> [!TIP]
> Asegúrate de que tienes Teams proyecto de aplicación abierto en Visual Studio código.

## <a name="preview-manifest"></a>Manifiesto de vista previa

Para obtener una vista previa del manifiesto con contenido real, Teams Toolkit genera archivos de manifiesto de vista previa en la `build/appPackage` carpeta:

```text
└───build
    └───appPackage
        ├───appPackage.{env}.zip - Zipped app package of remote teams app
        ├───appPackage.local.zip - Zipped app package of local team app
        ├───manifest.{env}.json  - Previewed manifest of remote teams app
        └───manifest.local.json  - Previewed manifest of local teams app
```

### <a name="preview-local-manifest-file"></a>Vista previa del archivo de manifiesto local

Para obtener una vista previa del archivo de manifiesto de la aplicación de teams local, debes presionar **F5** para ejecutar la depuración local. Genera la configuración local predeterminada y, a continuación, el paquete de la aplicación y las compilaciones de manifiesto de vista previa en **la carpeta build/appPackage** .

También puede obtener una vista previa del manifiesto local siguiendo los pasos siguientes:

1. Seleccione **Vista** previa en los codelens del **archivo manifest.local.template.json** .
2. Seleccione **Vista previa del archivo de** manifiesto en la barra de **menús del archivo manifest.local.template.json** .
3. Seleccione **Zip Teams de metadatos en** Treeview y seleccione **Local**.
La vista previa local aparece como se muestra en la imagen:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-1.png" alt-text="Versión preliminar":::

### <a name="preview-manifest-in-remote-environment"></a>Manifiesto de vista previa en entorno remoto

Para obtener una vista previa del archivo de manifiesto de  la aplicación de teams remotos, selecciona Aprovisionar en la nube en **Teams Toolkit el panel** DESARROLLO de la extensión Treeview o desencadenar Teams **:** Aprovisionar en la nube desde la paleta de comandos. Genera configuración para la aplicación de teams remotos y compila el paquete y el manifiesto de vista previa en la **carpeta build/appPackage** .

También puede obtener una vista previa del manifiesto en un entorno remoto siguiendo los pasos siguientes:

1. Seleccione **Vista** previa en los codelens del **archivo manifest.remote.template.json** .
2. Seleccione **Vista previa del archivo de** manifiesto en la barra de **menús del archivo manifest.remote.template.json** .
3. Seleccione **Zip Teams de metadatos en** Treeview.
4. Seleccione el entorno.

Si hay más de un entorno, debe seleccionar el entorno que desea obtener una vista previa como se muestra en la imagen:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="Agregar env":::

## <a name="sync-local-changes-to-dev-portal"></a>Sincronizar cambios locales en el portal de desarrollo

Después de obtener una vista previa del archivo de manifiesto, puede sincronizar los cambios locales en el portal de desarrollo siguiendo los pasos siguientes:

1. Seleccione **Actualizar para Teams plataforma** en la esquina superior izquierda de`manifest.{env}.json`
2. Seleccione **Teams: Actualizar manifiesto a Teams plataforma** en la barra de menús de`manifest.{env}.json`

 También puede desencadenar el Teams **: actualizar manifiesto a Teams desde la** paleta de comandos

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="vista de árbol":::

> [!NOTE]
> El desencadenador de codelens o **title** del editor actualizará el archivo de manifiesto actual a Teams plataforma. El desencadenador de la paleta de comandos requiere seleccionar el entorno de destino.

Si el archivo de manifiesto está obsoleto debido al cambio de archivo de configuración o al cambio de plantilla, asegúrese de confirmar la siguiente acción:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="pre":::

* **Solo vista previa**: el archivo de manifiesto local se sobrescribirá según la configuración actual
* **Vista previa y actualización**: el archivo de manifiesto local se sobrescribirá según la configuración actual y también se actualizará a Teams plataforma
* **Cancelar**: no hacer nada

> [!NOTE]
> Los cambios se actualizarán al portal de desarrollo. Si tiene algunas actualizaciones manuales en el portal de desarrollo, se sobrescribirá.

## <a name="see-also"></a>Vea también

[Personalizar Teams de aplicación en Teams Toolkit](TeamsFx-manifest-customization.md)

---
title: Manifiesto de aplicación de Teams en el kit de herramientas de Teams para Visual Studio
author: surbhigupta
description: En este módulo, aprenderá a editar, obtener una vista previa y personalizar el manifiesto de aplicación de Teams en el entorno diferente para Visual Studio.
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/13/2022
ms.openlocfilehash: c391df383c97638d3c8ff5944afab75db2400580
ms.sourcegitcommit: 65ae3ccc2312ddc6cdaa05096e30bdf9dca10c3f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027484"
---
# <a name="edit-teams-app-manifest-using-visual-studio"></a>Edición del manifiesto de aplicación de Teams mediante Visual Studio

El kit de herramientas de Teams en Visual Studio carga el manifiesto desde `manifest.template.json` con configuraciones desde `state.{env}.json` y `config.{env}.json` mientras aprovisiona y prepara las dependencias de la aplicación. También puede crear una aplicación de Microsoft Teams en el [Portal para desarrolladores](https://dev.teams.microsoft.com/apps) con el manifiesto.

Después del scaffolding, en el archivo `templates/appPackage` de plantilla de manifiesto en la carpeta, `manifest.template.json` se comparte entre el entorno local y remoto.

En la plantilla de manifiesto, seleccione Archivo de **manifiesto abierto** **del kit de herramientas de** >  **Project** >  Teams.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-open-manifest.png" alt-text="Abrir archivo de manifiesto":::

### <a name="customize-app-manifest-in-teams-toolkit"></a>Personalización del manifiesto de la aplicación en el kit de herramientas de Teams

Hay dos tipos de marcadores de posición en `manifest.template.json`:

- `{{state.xx}}` es un marcador de posición predefinido, cuyo valor se resuelve mediante el kit de herramientas de Teams, definido en `state.{env}.json`. Se recomienda no modificar los valores de `state.{env}.json`.
- `{{config.manifest.xx}}` es un marcador de posición personalizado, cuyo valor se resuelve a partir de `config.{env}.json`.

Puede agregar un parámetro personalizado mediante:

- Agregar un marcador de posición en `manifest.template.json` con el patrón : `{{config.manifest.xx}}`.
- Agregar un valor de configuración en `config.{env}.json`.

    ```
        {
            "manifest": {
            "KEY": "VALUE"
            }
    }
    ```

### <a name="preview-app-manifest-in-teams-toolkit"></a>Vista previa del manifiesto de la aplicación en Teams Toolkit

Puede obtener una vista previa de los valores en el manifiesto de la aplicación de dos maneras:

- Al mantener el puntero sobre el marcador de posición en `manifest.template.json`, se pueden ver los valores de **desarrollo** y entorno **local** .

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-placeholder1.png" alt-text="Mantener el puntero sobre el marcador de posición":::

- También puede mantener el puntero sobre la clave además de cada marcador de posición en `manifest.template.json`, se pueden ver los mismos **valores para desarrollo** y entorno **local** .

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-key-placeholder.png" alt-text="Mantener el puntero sobre la tecla junto al marcador de posición":::

   > [!NOTE]
   > Si el entorno no se ha aprovisionado o las dependencias de la aplicación de Teams no se han preparado, indica que no se han generado los valores del marcador de posición. Siga las instrucciones dentro del mouse para generar los valores correspondientes.

### <a name="preview-manifest-file"></a>Vista previa del archivo de manifiesto

Para obtener una vista previa del archivo de manifiesto, siga estos pasos:

- Seleccione el menú **Kit de herramientas de** **Project** >  Teams y desencadene **Preparar dependencias de aplicaciones de Teams** o **Aprovisionar en la nube** que genera la configuración para la aplicación de Teams local o remota.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview-manifest1.png" alt-text="Vista previa del archivo de manifiesto":::

- Para obtener una vista previa del manifiesto con contenido real, Teams Toolkit genera los archivos de manifiesto de vista previa, haga clic con el botón derecho en **manifest.template.json** en la carpeta **appPackage** . Seleccione **Preview Manifest File for Local (Vista previa del archivo** >  de manifiesto **) para Local (Local**) o **For Azure (Azure**).

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview1.png" alt-text="Menú contextual Vista previa":::

Hay otras dos maneras de obtener una vista previa del archivo de manifiesto:

- Seleccione Paquete de **aplicación zip** **del kit** >  de herramientas de **Project** >  Teams y, a continuación, seleccione **Para local** o **Para Azure**.

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-zip1.png" alt-text="Paquete de aplicación zip":::

- También puede ver la misma lista de menús que se encuentran en Project > Teams Toolkit si hace clic con el botón derecho en el nombre del proyecto y, a continuación, selecciona **Teams Toolkit (Kit de herramientas de Teams**) en **Explorador de soluciones**.

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-solution-explorer1.png" alt-text="Lista de menús del kit de herramientas de Teams desde el Explorador de soluciones":::

    > [!NOTE]
    >En este escenario, el nombre del proyecto es **MyTeamsApp1**.

### <a name="sync-local-changes-to-developer-portal"></a>Sincronización de cambios locales en el portal para desarrolladores

Los cambios locales se pueden sincronizar con el Portal para desarrolladores, después de obtener una vista previa del archivo de manifiesto. Seleccione Manifiesto de actualización **del kit** >  de herramientas de **Project** >  Teams **en el Portal para desarrolladores de Teams** o el menú contextual de Explorador de soluciones.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-update-manifest1.png" alt-text="Actualización del manifiesto en el portal para desarrolladores de Teams":::

> [!NOTE]
> Los cambios se actualizan en el Portal para desarrolladores de Teams. Si tiene algunas actualizaciones manuales en el Portal para desarrolladores, se pueden sobrescribir. En el cuadro de diálogo **Advertencia** , puede seleccionar **Sobrescribir y actualizar** o **Cancelar**.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-overwrite.png" alt-text="Advertencia de actualización":::

## <a name="see-also"></a>Vea también

- [Aprovisionamiento de recursos en la nube mediante Visual Studio](provision-cloud-resources.md)
- [Implementación de una aplicación de Teams en la nube mediante Visual Studio](deploy-teams-app.md)

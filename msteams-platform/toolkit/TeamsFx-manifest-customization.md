---
title: Personalizar Teams manifiesto de aplicación en Teams Toolkit
author: zyxiaoyuer
description: Personalizar manifiesto de aplicación de Teams
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: de85674891a53c1e87b43ae1d472daf35716c348
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073543"
---
# <a name="customize-app-manifest-in-toolkit"></a>Personalización del manifiesto de aplicación en Toolkit

Teams Toolkit consta de los siguientes archivos de plantilla de manifiesto en `manifest.template.json` la carpeta en entornos locales y remotos:

* `manifest.template.json`
* `templates/appPackage`


## <a name="prerequisite"></a>Requisito previo

* Instale la versión [más reciente del kit de herramientas de Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

> [!TIP]
> Asegúrese de que ha abierto Teams proyecto de aplicación en Visual Studio Code.

Durante la depuración o el aprovisionamiento locales, Teams Toolkit carga el manifiesto desde `manifest.template.json`, con configuraciones de `state.{env}.json`, `config.{env}.json`y crea la aplicación teams en [el Portal de desarrollo](https://dev.teams.microsoft.com/apps).


## <a name="placeholders-supported-in-manifesttemplatejson"></a>Marcadores de posición admitidos en manifest.template.json

* `{{state.xx}}`es un marcador de posición predefinido y su valor se resuelve mediante Teams Toolkit, definido en `state.{env}.json`. Asegúrese de no modificar los valores en estado. {env}.json
* `{{config.manifest.xx}}` es un marcador de posición personalizado y su valor se resuelve desde `config.{env}.json`

  1. Puede agregar un parámetro personalizado como se indica a continuación:
      1. Agregue un marcador de posición en manifest.template.json con el patrón : `{{config.manifest.xx}}`
      2. Agregue un valor de configuración en la configuración. {env}.json

        ```json
        {
            "manifest": {
                "KEY": "VALUE"
            }
        }
        ```

   2. Puede navegar al archivo de configuración seleccionando cualquiera de los marcadores de posición de configuración **Ir al archivo de configuración** o **Ver el archivo de estado** en `manifest.template.json`

## <a name="see-also"></a>Ver también

[Vista previa Teams manifiesto de aplicación en Teams Toolkit](TeamsFx-manifest-preview.md)

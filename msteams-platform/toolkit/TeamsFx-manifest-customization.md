---
title: Personalizar el manifiesto de la aplicación de Teams en el kit de herramientas de Teams
author: zyxiaoyuer
description: Personalizar manifiesto de aplicación de Teams
ms.author: nliu
ms.localizationpriority: high
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 28a06da170ee52e4340aa3d401d39ad08f58e2ba
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65110263"
---
# <a name="customize-app-manifest-in-toolkit"></a>Personalizar el manifiesto de la aplicación en el kit de herramientas

El kit de herramientas de Teams consta de los siguientes archivos de plantilla de manifiesto en la carpeta `manifest.template.json` en entornos locales y remotos:

* `manifest.template.json`
* `templates/appPackage`


## <a name="prerequisite"></a>Requisito previo

* Instale la versión [más reciente del kit de herramientas de Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

> [!TIP]
> Asegúrese de que tiene el proyecto de aplicación de Teams abierto en Visual Studio Code.

Durante la depuración o el aprovisionamiento local, el kit de herramientas de Teams carga el manifiesto desde `manifest.template.json`, con configuraciones de `state.{env}.json`, `config.{env}.json`y crea la aplicación de Teams en [Portal de desarrollo](https://dev.teams.microsoft.com/apps).


## <a name="placeholders-supported-in-manifesttemplatejson"></a>Marcadores de posición admitidos en manifest.template.json

* `{{state.xx}}` es un marcador de posición predefinido y el kit de herramientas de Teams resuelve su valor, definido en `state.{env}.json`. Asegúrese de no modificar los valores en estado. {env}.json
* `{{config.manifest.xx}}` es un marcador de posición personalizado y su valor se resuelve a partir de `config.{env}.json`

  1. Puede agregar un parámetro personalizado como se indica a continuación:
      1. Agregue un marcador de posición en manifest.template.json con el patrón: `{{config.manifest.xx}}`
      2. Agregue un valor de configuración en config.{env}.json

        ```json
        {
            "manifest": {
                "KEY": "VALUE"
            }
        }
        ```

   2. Puede ir al archivo de configuración seleccionando cualquiera de los marcadores de posición de configuración **Ir al archivo de configuración** o **Ver el archivo de estado** en `manifest.template.json`

## <a name="see-also"></a>Consulte también

[Vista previa del manifiesto de la aplicación de Teams en el kit de herramientas de Teams](TeamsFx-manifest-preview.md)

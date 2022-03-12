---
title: Personalizar Teams de aplicación en Teams Toolkit
author: zyxiaoyuer
description: Personalizar manifiesto de aplicación de Teams
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 047cd9bcd86c103c3c9cab22793fb7d187f7493d
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453603"
---
# <a name="customize-app-manifest-in-teams-toolkit"></a>Personalizar manifiesto de aplicación en Teams Toolkit

Teams Toolkit consta de los siguientes archivos de plantilla de manifiesto en la `templates/appPackage` carpeta:

* `manifest.local.template.json` - Aplicación de equipos de depuración local
* `manifest.remote.template.json` - compartido en todos los entornos

## <a name="prerequisite"></a>Requisito previo

* [Instale Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión 3.0.0+.

> [!TIP]
> Asegúrate de que tienes Teams proyecto de aplicación abierto en Visual Studio Code.

Durante la provisión, Teams Toolkit carga el manifiesto `manifest.remote.template.json`de , combinado con las configuraciones de `state.{env}.json` y `config.{env}.json`, y crea la aplicación teams en [el Portal de desarrollo](https://dev.teams.microsoft.com/apps).

Durante la depuración local, Teams Toolkit carga el manifiesto `manifest.local.template.json`de , combinado con `localSettings.json`las configuraciones de y crea la aplicación teams en [el Portal de desarrollo](https://dev.teams.microsoft.com/apps).

## <a name="supported-placeholder-in-manifestremotetemplatejson"></a>Marcador de posición admitido en manifest.remote.template.json

* `{{state.xx}}`es un marcador de posición predefinido cuyo valor se resuelve Teams Toolkit, definido en `state.{env}.json`. Asegúrese de no modificar los valores en estado. {env}.json.
* `{{config.manifest.xx}}` es marcador de posición personalizado cuyo valor se resuelve desde `config.{env}.json`.
  * Puede agregar un parámetro personalizado de la siguiente manera:
    * Agregue un marcador de posición en manifest.remote.template.json con pattern: `{{config.manifest.xx}}`
    * Agregue un valor de configuración en config. {env}.json

        ```json
        {
            "manifest": {
                "KEY": "VALUE"
            }
        }
        ```

    Además de cada marcador de posición de configuración en `manifest.remote.template.json`, hay un `Go to config file`. Puede navegar hasta el archivo de configuración seleccionándoselo.

## <a name="supported-placeholder-in-manifestlocaltemplatejson"></a>Marcador de posición admitido en manifest.local.template.json

`{{localSettings.xx}}`es un marcador de posición predefinido cuyo valor se resuelve Teams Toolkit, definido en `localSettings.json`. Asegúrese de no modificar los valores de localSettings.json.

 > [!NOTE]
 > Asegúrese de no personalizar el manifiesto local.

## <a name="see-also"></a>Vea también

[Vista Teams manifiesto de aplicación en Teams Toolkit](TeamsFx-manifest-preview.md)

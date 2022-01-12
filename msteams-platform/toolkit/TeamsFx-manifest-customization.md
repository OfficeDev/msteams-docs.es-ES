---
title: Personalizar Teams de aplicación en Teams Toolkit
author: zyxiaoyuer
description: Personalizar manifiesto de aplicación de Teams
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: d9f2ea49ece8728101a738129e45dd8155887ebc
ms.sourcegitcommit: 2d5bdda6c52693ed682bbd543b0aa66e1feb3392
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2022
ms.locfileid: "61768080"
---
# <a name="customize-app-manifest-in-teams-toolkit"></a>Personalizar manifiesto de aplicación en Teams Toolkit

Teams Toolkit consta de los siguientes archivos de plantilla de manifiesto en `templates/appPackage` la carpeta:

- `manifest.local.template.json` - Aplicación de equipos de depuración local
- `manifest.remote.template.json` - compartido en todos los entornos

## <a name="prerequisite"></a>Requisito previo

* [Instale Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión 3.0.0+.

> [!TIP]
> Asegúrate de que tienes Teams proyecto de aplicación abierto en VS Code.

Durante la aprovisionamiento, Teams Toolkit carga el manifiesto de , combinado con las configuraciones de y , y crea la aplicación `manifest.remote.template.json` teams en el Portal de `state.{env}.json` `config.{env}.json` [desarrollo](https://dev.teams.microsoft.com/apps).

Durante la depuración local, Teams Toolkit carga el manifiesto de , combinado con las configuraciones de , y crea la aplicación `manifest.local.template.json` teams en el Portal de `localSettings.json` [desarrollo](https://dev.teams.microsoft.com/apps).

## <a name="supported-placeholder-in-manifestremotetemplatejson"></a>Marcador de posición admitido en manifest.remote.template.json

- `{{state.xx}}`es un marcador de posición predefinido cuyo valor se resuelve Teams Toolkit, definido en `state.{env}.json` . Asegúrese de no modificar los valores en estado. {env}.json.
- `{{config.manifest.xx}}` es marcador de posición personalizado cuyo valor se resuelve desde `config.{env}.json` .
  - Puede agregar un parámetro personalizado de la siguiente manera:
    - Agregue un marcador de posición en manifest.remote.template.json con pattern: `{{config.manifest.xx}}`
    - Agregue un valor de configuración en config. {env}.json

        ```json
        {
            "manifest": {
                "KEY": "VALUE"
            }
        }
        ```

    Además de cada marcador de posición de configuración `manifest.remote.template.json` en , hay un `Go to config file` . Puede navegar hasta el archivo de configuración seleccionándoselo.

## <a name="supported-placeholder-in-manifestlocaltemplatejson"></a>Marcador de posición admitido en manifest.local.template.json

`{{localSettings.xx}}`es un marcador de posición predefinido cuyo valor se resuelve Teams Toolkit, definido en `localSettings.json` . Asegúrese de no modificar los valores de localSettings.json.

 > [!NOTE]
 > Asegúrese de no personalizar el manifiesto local.

## <a name="see-also"></a>Vea también

[Vista Teams manifiesto de la aplicación en Teams Toolkit](TeamsFx-manifest-preview.md)

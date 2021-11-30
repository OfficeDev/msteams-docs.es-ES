---
title: Personalizar Teams de aplicación en Teams Toolkit
author: zyxiaoyuer
description: Personalizar Teams de aplicación
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 34b454f63eb900fce2f38748838ce46558835ac5
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/30/2021
ms.locfileid: "61228208"
---
# <a name="customize-teams-app-manifest-in-teams-toolkit"></a>Personalizar Teams de aplicación en Teams Toolkit

Teams Toolkit consta de dos archivos de plantilla de manifiesto en `templates/appPackage` la carpeta:

- `manifest.local.template.json` - Aplicación de equipos de depuración local
- `manifest.remote.template.json` - compartido en todos los entornos

## <a name="prerequisite"></a>Requisito previo

* [Instale Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión 3.0.0+.

> [!TIP]
> Ya debería tener abierto un proyecto Teams aplicación en el código VS.

Durante la provisión, Teams Toolkit cargará el manifiesto de `manifest.remote.template.json` , combinado con las configuraciones de y `state.{env}.json` `config.{env}.json` . A continuación, crea una aplicación de teams en [El Portal de desarrollo](https://dev.teams.microsoft.com/apps) con este manifiesto.

Durante la depuración local, Teams Toolkit cargará el manifiesto de `manifest.local.template.json` , combinado con las configuraciones de `localSettings.json` . A continuación, crea una aplicación de teams en [El Portal de desarrollo](https://dev.teams.microsoft.com/apps) con este manifiesto.

## <a name="supported-placeholder-in-manifestremotetemplatejson"></a>Marcador de posición admitido en manifest.remote.template.json

- `{{state.xx}}`es un marcador de posición predefinido cuyo valor se resuelve Teams Toolkit, definido en `state.{env}.json` . No debe modificar los valores en estado. {env}.json.
- `{{config.manifest.xx}}` es marcador de posición personalizado cuyo valor se resuelve desde `config.{env}.json` .
  - Para agregar un parámetro personalizado, haga lo siguiente:
    - Agregue un marcador de posición en manifest.remote.template.json con pattern: `{{config.manifest.xx}}`
    - Agregue un valor de configuración en config. {env}.json

        ```json
        {
            "manifest": {
                "KEY": "VALUE"
            }
        }
        ```

    Además de cada marcador de posición de configuración `manifest.remote.template.json` en , hay un `Go to config file` botón. Puede navegar hasta el archivo de configuración seleccionándose como se muestra en la imagen:

    ![ir al archivo de configuración](./images/gotoconfigfile.png)

## <a name="supported-placeholder-in-manifestlocaltemplatejson"></a>Marcador de posición admitido en manifest.local.template.json

`{{localSettings.xx}}`es un marcador de posición predefinido cuyo valor se resuelve Teams Toolkit, definido en `localSettings.json` . No debe modificar los valores de localSettings.json.

 > [!NOTE]
 > No se sugiere la personalización del manifiesto local.

## <a name="see-also"></a>Consulte también

> [!div class="nextstepaction"]
> [Vista Teams manifiesto de la aplicación en Teams Toolkit](TeamsFx-manifest-preview.md)

---
title: Agregar funcionalidades a las Teams aplicaciones
author: MuyangAmigo
description: Describe Agregar funcionalidades de Teams Toolkit
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 3e704b08caa9a3aafc388fe4aa2e8851292c944f
ms.sourcegitcommit: c66da76fb766df6270095265e1da8c49a3afd195
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/07/2022
ms.locfileid: "62435806"
---
# <a name="add-capabilities-to-your-teams-apps"></a>Agregar funcionalidades a tus Teams aplicaciones

Puedes crear una nueva aplicación Teams con una de las Teams de la aplicación. Durante el desarrollo de aplicaciones, puedes usar Teams Toolkit para agregar más funcionalidades a tu Teams aplicación. En la tabla siguiente se enumeran las Teams funcionalidades de la aplicación:

|**Capacidad**|**Descripción**|
|--------|-------------|
| Pestañas |  Las pestañas son etiquetas HTML sencillas que apuntan a dominios declarados en el manifiesto de la aplicación. Puedes agregar pestañas como parte del canal dentro de un equipo, chat de grupo o aplicación personal para un usuario individual.|
| Bots |  Los bots ayudan a interactuar con el servicio web a través de texto, tarjetas interactivas y módulos de tareas.|
| Extensiones de mensajería | Las extensiones de mensajería ayudan a interactuar con el servicio web a través de botones y formularios en el Microsoft Teams cliente.|

## <a name="prerequisite"></a>Requisito previo

[Instale Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión 3.0.0+.

> [!TIP]
> Asegúrate de que tienes Teams proyecto de aplicación abierto en código VS.

## <a name="add-capabilities-using-teams-toolkit"></a>Agregar funcionalidades mediante Teams Toolkit

> [!IMPORTANT]
> Debes realizar la provisión para cada entorno después de agregar correctamente funcionalidades a tu Teams aplicación.

1. Abra **Microsoft Visual Studio código**.
1. Seleccione **Teams Toolkit** desde el panel izquierdo.
1. Seleccione **Agregar funcionalidades**:

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add capabilities.png" alt-text="capabilities":::

   También puede abrir la paleta de comandos y **escribir Teams: Agregar funcionalidades**: 
      
    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/tree view capabilities.png" alt-text="Funcionalidades alternativas":::

1. En la ventana emergente, seleccione las capacidades que desea incluir en el proyecto:

    :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select capabilities.png" alt-text="select":::

1. Seleccione **Aceptar**.

Las funcionalidades seleccionadas se agregan correctamente al proyecto. El Teams Toolkit código fuente para las funcionalidades recién agregadas.

## <a name="add-capabilities-using-teamsfx-cli-in-command-window"></a>Agregar funcionalidades mediante la CLI de TeamsFx en la ventana de comandos

1. Cambie el directorio al **directorio del proyecto**.
1. Ejecute el siguiente comando para agregar diferentes funcionalidades al proyecto:

   |Capacidad y escenario| Comando|
   |-----------------------|----------|
   |Para agregar pestaña|`teamsfx capability add tab`|
   |Para agregar bot|`teamsfx capability add bot`|
   |Para agregar extensión de mensajería|`teamsfx capability add messaging-extension`|

## <a name="supported-capabilities-matrix"></a>Matriz de capacidades compatibles

Aparte de las capacidades que ya Teams aplicación, puedes elegir agregar diferentes funcionalidades a tu Teams aplicación. En la tabla siguiente se proporcionan las diferentes Teams funcionalidades de la aplicación: 

|Capacidades existentes|Se pueden agregar otras funcionalidades compatibles|
|--------------------|--------------------|
|Pestañas con SPFx|Ninguno|
|Pestañas con Azure|Bot y extensión de mensajería|
|Bot|Pestañas|
|Extensión de mensajería|Pestañas y bot|
|Pestañas y bot|Pestañas y extensión de mensaje|
|Pestañas y extensión de mensajería|Pestañas y bot|
|Pestañas, bot y extensión de mensajería|Pestañas|
|Pestañas |Bot y extensión de mensaje|

## <a name="add-capabilities"></a>Agregar funcionalidades

Después de agregar la extensión de bot y mensajería, los cambios en el proyecto son los siguientes:

- Se agrega un código de plantilla de bot a una subcarpeta con ruta de acceso `yourProjectFolder/bot`. Esto incluye una plantilla **de aplicación** de bot hello world en el proyecto.
- `launch.json`y `task.json` en `.vscode` carpeta se actualizan, que incluye scripts necesarios para Visual Studio Code y se ejecuta cuando desea depurar la aplicación localmente. 
- `manifest.remote.template.json`y `manifest.local.template.json` el archivo en `templates/appPackage` carpeta se actualizan, lo que incluye información relacionada con bots en el archivo de manifiesto que representa la aplicación en la Teams plataforma. Estos son los cambios:
  - El identificador del bot.
  - Los ámbitos del bot.
  - Los comandos a los que la aplicación de bot hello world puede responder.
- Los archivos debajo `templates/azure/teamsfx` se actualizarán y `templates/azure/provision/xxx`se regenerará el archivo .bicep.
- Los archivos debajo `.fx/config` se regeneran, lo que garantiza que el proyecto esté configurado con configuraciones correctas para la funcionalidad recién agregada.

Después de agregar la pestaña, los cambios en el proyecto son los siguientes:

- Se agrega un código de plantilla de pestaña front-end a `yourProjectFolder/tab`una subcarpeta con ruta de acceso, que incluye una plantilla de aplicación de pestaña **hello world** en el proyecto.
- `launch.json`y `task.json` en `.vscode` carpeta se actualizan, que incluye scripts necesarios para Visual Studio Code y se ejecuta cuando desea depurar la aplicación localmente. 
- `manifest.remote.template.json`y `manifest.local.template.json` el archivo en `templates/appPackage` carpeta se actualizan, que incluye información relacionada con pestañas en el archivo de manifiesto que representa la aplicación en la plataforma Teams, los cambios son los siguientes:
  - Pestañas configurables y estáticas.
  - Los ámbitos de las pestañas.
- Los archivos debajo `templates/azure/teamsfx` se actualizarán y `templates/azure/provision/xxx`se regenerará el archivo .bicep.
- El archivo debajo `.fx/config` se regenera, lo que garantiza que el proyecto esté configurado con configuraciones correctas para la funcionalidad recién agregada.

## <a name="limitations"></a>Limitaciones

Las limitaciones de TeamsFx al agregar más funcionalidades son las siguientes:

* Puede agregar pestañas de hasta 16 instancias.
* Puede agregar bot y extensión de mensajería para una instancia cada una.

## <a name="see-also"></a>Vea también

* [Aprovisionar recursos en la nube](provision.md)
* [Crear nuevo Teams proyecto](create-new-project.md)

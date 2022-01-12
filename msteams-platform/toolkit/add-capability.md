---
title: Agregar funcionalidades a las Teams aplicaciones
author: MuyangAmigo
description: Describe Agregar funcionalidades de Teams Toolkit
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 8aedcef132eee34a72f0f2f873bdae3a45529c7c
ms.sourcegitcommit: 2d5bdda6c52693ed682bbd543b0aa66e1feb3392
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2022
ms.locfileid: "61768528"
---
# <a name="add-capabilities-to-your-teams-apps"></a>Agregar funcionalidades a tus Teams aplicaciones

Puedes crear una nueva aplicación Teams con una de las Teams de la aplicación. Durante el desarrollo de aplicaciones, puedes usar Teams Toolkit para agregar más funcionalidades a tu Teams aplicación. En la tabla siguiente se enumeran las Teams funcionalidades de la aplicación:

|**Capacidad**|**Descripción**|
|--------|-------------|
| Pestañas |  Las pestañas son etiquetas HTML sencillas que apuntan a dominios declarados en el manifiesto de la aplicación. Puedes agregar pestañas como parte del canal dentro de un equipo, chat de grupo o aplicación personal para un usuario individual.|
| Bots |  Los bots ayudan a interactuar con el servicio web a través de texto, tarjetas interactivas y módulos de tareas.|
| Extensiones de mensajería | Las extensiones de mensajería ayudan a interactuar con el servicio web a través de botones y formularios en el Microsoft Teams cliente.|

## <a name="prerequisite"></a>Requisito previo

* [Instale Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión 3.0.0+.

> [!TIP]
> Asegúrate de que tienes Teams proyecto de aplicación abierto en código VS.

## <a name="add-capabilities-using-teams-toolkit"></a>Agregar funcionalidades mediante Teams Toolkit

> [!IMPORTANT]
> Debes realizar la provisión para cada entorno después de agregar correctamente funcionalidades a tu Teams aplicación.

1. Abra **Visual Studio Code**.
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

   |Capacidad y escenario| Get-Help|
   |-----------------------|----------|
   |Para agregar pestaña|`teamsfx capability add tab`|
   |Para agregar bot|`teamsfx capability add bot`|
   |Para agregar extensión de mensajería|`teamsfx capability add messaging-extension`|

## <a name="supported-capabilities-matrix"></a>Matriz de capacidades compatibles

Aparte de las capacidades que ya Teams aplicación, puedes elegir agregar diferentes funcionalidades a tu Teams aplicación. En la tabla siguiente se proporcionan las diferentes Teams funcionalidades de la aplicación: 

|Capacidades existentes|Se pueden agregar otras funcionalidades compatibles|
|--------------------|--------------------|
|Pestañas con SPFx|Ninguno|
|Pestañas con Azure|Bots y extensiones de mensajería|
|Bots|Pestañas|
|Extensiones de mensajería|Pestañas|
|Pestañas y bots|Ninguno|
|Pestañas y extensiones de mensajería|Ninguno|
|Pestañas, bots y extensiones de mensajería|Ninguno|

## <a name="add-capabilities"></a>Agregar funcionalidades

Después de agregar la extensión de bot y mensajería, los cambios en el proyecto son los siguientes:

- Se agrega un código de plantilla de bot a una subcarpeta con ruta de `yourProjectFolder/bot` acceso. Esto incluye una plantilla **de aplicación** de bot hello world en el proyecto.
- `launch.json`y en carpeta se actualizan, que incluye scripts necesarios para Visual Studio Code y se ejecuta cuando desea depurar la `task.json` `.vscode` aplicación localmente. 
- `manifest.remote.template.json`y se actualiza el archivo en carpeta, que incluye información relacionada con bots en el archivo de manifiesto que representa la `manifest.local.template.json` aplicación en la Teams `templates/appPackage` plataforma. Estos son los cambios:
  - El identificador del bot.
  - Los ámbitos del bot.
  - Los comandos a los que la aplicación de bot hello world puede responder.
- Los archivos debajo se actualizarán y se regenerará el archivo `templates/azure/teamsfx` `templates/azure/provision/xxx` .bicep.
- Los archivos debajo se regeneran, lo que garantiza que el proyecto esté configurado con configuraciones `.fx/config` correctas para la funcionalidad recién agregada.

Después de agregar la pestaña, los cambios en el proyecto son los siguientes:

- Se agrega un código de plantilla de pestaña front-end a una subcarpeta con ruta de acceso, que incluye una plantilla de aplicación de `yourProjectFolder/tab` pestaña **hello world** en el proyecto.
- `launch.json`y en carpeta se actualizan, que incluye scripts necesarios para Visual Studio Code y se ejecuta cuando desea depurar la `task.json` `.vscode` aplicación localmente. 
- `manifest.remote.template.json`y el archivo en carpeta se actualizan, que incluye información relacionada con pestañas en el archivo de manifiesto que representa la aplicación en la plataforma Teams, los cambios son `manifest.local.template.json` `templates/appPackage` los siguientes:
  - Pestañas configurables y estáticas.
  - Los ámbitos de las pestañas.
- Los archivos debajo se actualizarán y se regenerará el archivo `templates/azure/teamsfx` `templates/azure/provision/xxx` .bicep.
- El archivo debajo se regenera, lo que garantiza que el proyecto esté configurado con configuraciones `.fx/config` correctas para la funcionalidad recién agregada.

## <a name="limitations"></a>Limitaciones

Las limitaciones con TeamsFx al agregar más funcionalidades son las siguientes:

- No puede agregar capacidad de proyecto para más de una instancia.
- No puede agregar funcionalidades de bot si el proyecto contiene extensión de mensajería.
- No puede agregar una extensión de mensajería si el proyecto contiene un bot.

> [!NOTE]
> Si desea incluir las funciones de bot y extensión de mensajería, selecciónelos al mismo tiempo. Solo puede agregarlas al crear un nuevo proyecto o una aplicación de pestaña.

## <a name="see-also"></a>Vea también

* [Aprovisionar recursos en la nube](provision.md)
* [Crear nuevo Teams proyecto](create-new-project.md)

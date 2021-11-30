---
title: Agregar funcionalidades a las Teams aplicaciones
author: MuyangAmigo
description: Describe Agregar funcionalidades de Teams Toolkit
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: f5563b16646b66795b9451eebc865879294dfd98
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/30/2021
ms.locfileid: "61228127"
---
# <a name="add-capabilities-to-your-teams-apps"></a>Agregar funcionalidades a tus Teams aplicaciones

Puedes empezar a crear una aplicación Teams con una de las Teams de la aplicación. Durante el desarrollo de aplicaciones, puedes usar Teams Toolkit para agregar de forma flexible más funcionalidades a tu Teams aplicación. En la tabla siguiente se describen las Teams de la aplicación:

|**Capacidad**|**Descripción**|
|--------|-------------|
| Pestañas |  Las pestañas son etiquetas HTML sencillas que apuntan a dominios declarados en el manifiesto de la aplicación. Puedes agregar pestañas como parte del canal dentro de un equipo, chat de grupo o aplicación personal para un usuario individual.|
| Bots |  Los bots ayudan a interactuar con el servicio web a través de texto, tarjetas interactivas y módulos de tareas.|
| Extensiones de mensajería | Las extensiones de mensajería ayudan a interactuar con el servicio web a través de botones y formularios en el Microsoft Teams cliente.|

## <a name="prerequisite"></a>Requisito previo

* [Instale Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión 3.0.0+.

> [!TIP]
> Ya debería tener abierto un proyecto Teams aplicación en el código VS.

## <a name="add-capabilities-using-teams-toolkit"></a>Agregar funcionalidades mediante Teams Toolkit

> [!IMPORTANT]
> Debes realizar la provisión para cada entorno después de agregar correctamente funcionalidades a tu Teams aplicación.

1. Seleccione **Teams Toolkit** desde el panel izquierdo:

    ![Activar Teams Toolkit](./images/activate-teams-toolkit.png)
  
1. Seleccione **Agregar funcionalidades**:

    ![Agregar funcionalidades](./images/add-capabilities.png)

      También puede abrir la paleta de comandos y **escribir Teams: Agregar funcionalidades**: 
      
      > [!NOTE]
      > Esto equivale a desencadenar desde la vista de árbol.

    ![Funcionalidades alternativas de adición](./images/alternate-capabilities.png)

1. En la ventana emergente, seleccione las capacidades que desea incluir en el proyecto:

    ![Seleccionar funcionalidades](./images/select-capabilities.png)

1. Seleccione **Aceptar**.

Las funcionalidades seleccionadas se agregan correctamente al proyecto. El Teams Toolkit código fuente para las funcionalidades recién agregadas.

## <a name="add-capabilities-using-teamsfx-cli-in-command-window"></a>Agregar funcionalidades Mediante la CLI de TeamsFx en la ventana de comandos

1. Cambie el directorio al **directorio del proyecto**.
1. Ejecute el siguiente comando para agregar diferentes funcionalidades al proyecto:

   |Capacidad y escenario| Comando|
   |-----------------------|----------|
   |Para agregar una pestaña|`teamsfx capability add tab`|
   |Para agregar un bot|`teamsfx capability add bot`|
   |Para agregar una extensión de mensajería|`teamsfx capability add messaging-extension`|

## <a name="supported-capabilities-matrix"></a>Matriz de capacidades compatibles

Aparte de las capacidades que ya Teams aplicación, puedes elegir agregar diferentes funcionalidades a tu Teams aplicación. En la tabla siguiente se proporciona varias funcionalidades Teams aplicaciones compatibles: 

|Capacidades existentes|Se pueden agregar otras funcionalidades|
|--------------------|--------------------|
|Pestañas con SPFx|Ninguno|
|Pestañas con Azure|Bots y extensiones de mensajería|
|Bots|Pestañas|
|Extensiones de mensajería|Pestañas|
|Pestañas y bots|Ninguno|
|Pestañas y extensiones de mensajería|Ninguno|
|Pestañas, bots y extensiones de mensajería|Ninguno|

## <a name="what-happens-when-you-add-capabilities"></a>Qué sucede cuando se agregan funcionalidades

Después de agregar la extensión de bot y mensajería, los siguientes cambios en el proyecto son:

- Se agrega un código de plantilla de bot a una subcarpeta con ruta de `yourProjectFolder/bot` acceso. Esto incluye una plantilla de aplicación de bot "hello world" en el proyecto.
- `launch.json` y `task.json` en carpeta se `.vscode` actualizan. Esto incluye scripts necesarios para Visual Studio Code se ejecuta cuando desea depurar la aplicación localmente. 
- `manifest.remote.template.json` y `manifest.local.template.json` el archivo en carpeta se `templates/appPackage` actualizan. Esto incluye información relacionada con bots en el archivo de manifiesto que representa la aplicación en la Teams plataforma. El cambio incluye:
  - El identificador del bot.
  - Los ámbitos del bot.
  - Los comandos a los que la aplicación de bot hello world puede responder.
- Los archivos `templates/azure/teamsfx` debajo se actualizarán y se regenerarán las plantillas/azure/provision/xxx.bicep.
- El archivo `.fx/config` debajo se regenera. Esto garantiza que el conjunto de proyectos con configuraciones correctas para la funcionalidad recién agregada.

Después de agregar la pestaña, los siguientes cambios en el proyecto son:

- Se agrega un código de plantilla de pestaña front-end a una subcarpeta con ruta de `yourProjectFolder/tab` acceso. Esto incluye una plantilla de aplicación de pestaña "hello world" en el proyecto.
- `launch.json` y `task.json` en carpeta se `.vscode` actualizan. Esto incluye scripts necesarios para Visual Studio Code se ejecuta cuando desea depurar la aplicación localmente. 
- `manifest.remote.template.json` y `manifest.local.template.json` el archivo en carpeta se `templates/appPackage` actualizan. Esto incluye información relacionada con pestañas en el archivo de manifiesto que representa la aplicación en la plataforma Teams, los cambios incluyen:
  - Pestañas configurables y estáticas.
  - Los ámbitos de las pestañas.
- Los archivos `templates/azure/teamsfx` debajo se actualizarán y se regenerarán las plantillas/azure/provision/xxx.bicep.
- El archivo `.fx/config` debajo se regenera. Esto garantiza que el conjunto de proyectos con configuraciones correctas para la funcionalidad recién agregada.

## <a name="limitations"></a>Limitaciones

Actualmente, existen limitaciones con TeamsFx al agregar más funcionalidades. Las limitaciones son las siguientes:

- Cada funcionalidad de proyecto más de una vez
- Cualquier funcionalidad si empieza con una aplicación Tab con SPFx
- Más funcionalidades de bot si el proyecto contiene extensión de mensajería
- Más extensión de mensajería si el proyecto contiene un bot.

> [!NOTE]
> Si desea incluir las funciones de bot y extensión de mensajería, selecciónelos al mismo tiempo. Puede agregarlas al crear un nuevo proyecto o una aplicación de pestaña.

## <a name="see-also"></a>Consulte también

> [!div class="nextstepaction"]
> [Aprovisionar recursos en la nube](provision.md)

> [!div class="nextstepaction"]
> [Crear nuevo Teams proyecto](create-new-project.md)

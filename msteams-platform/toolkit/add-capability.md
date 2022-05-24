---
title: Agregar funcionalidades a las aplicaciones de Teams
author: MuyangAmigo
description: Describe Agregar funcionalidades de Teams Toolkit
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 7778a5747ae6b5118d5ebeac857e2a9944cff62b
ms.sourcegitcommit: 80edf3c964bb47a2ee13f9eda4334ad19e21f331
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2022
ms.locfileid: "65654539"
---
# <a name="add-capabilities-to-your-teams-apps"></a>Agregar funcionalidades a las aplicaciones de Teams

Durante el desarrollo de aplicaciones, puede crear una nueva aplicación de Teams con Teams funcionalidad de aplicación. En la tabla siguiente se enumeran las funcionalidades de la aplicación Teams:

|**Capacidad**|**Descripción**|
|--------|-------------|
| Pestañas |  Las pestañas son etiquetas HTML sencillas que apuntan a dominios declarados en el manifiesto de la aplicación. Puede agregar pestañas como parte del canal dentro de un equipo, chat en grupo o aplicación personal para un usuario individual.|
| Bots |  Los bots ayudan a interactuar con el servicio web a través de texto, tarjetas interactivas y módulos de tareas|
| Extensiones de mensajería | Las extensiones de mensaje ayudan a interactuar con el servicio web a través de botones y formularios en el cliente Microsoft Teams|

## <a name="prerequisite"></a>Requisito previo

* Instale la versión [más reciente del kit de herramientas de Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

> [!TIP]
> Asegúrese de que ha abierto un proyecto de aplicación de Teams en VS Code.

## <a name="limitations"></a>Limitaciones

Las limitaciones de TeamsFx al agregar más funcionalidades son las siguientes:

* Puede agregar pestañas hasta 16 instancias
* Puede agregar bot y extensión de mensaje para una instancia cada una.

## <a name="add-capabilities"></a>Agregar funcionalidades

> [!Note]
> Debe realizar el aprovisionamiento para cada entorno, después de agregar correctamente funcionalidades a la aplicación de Teams.
* Puede agregar funcionalidades mediante Teams Toolkit en Visual Studio Code

    1. Abrir **código Microsoft Visual Studio**
    1. Seleccione **Teams Toolkit** en el panel izquierdo.
    1. Seleccione **Agregar funcionalidades.**

        :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add capabilities.png" alt-text="capabilities":::

*   También puede abrir la paleta de comandos y escribir Teams: Agregar funcionalidades:

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/tree view capabilities.png" alt-text="Funcionalidades alternativas":::


    1. En el elemento emergente, seleccione las funcionalidades que se van a incluir en el proyecto:

    :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select capabilities.png" alt-text="select":::

    2. Seleccione **Aceptar.**

Las funcionalidades seleccionadas se agregan correctamente al proyecto. El Teams Toolkit generar código fuente para las funcionalidades recién agregadas

## <a name="add-capabilities-using-teamsfx-cli-in-command-window"></a>Agregar funcionalidades mediante la CLI de TeamsFx en la ventana de comandos

1. Cambiar el directorio al **directorio del proyecto**
1. Ejecute el siguiente comando para agregar diferentes funcionalidades al proyecto:

   |Funcionalidad y escenario| Comando|
   |-----------------------|----------|
   |Para agregar pestaña|`teamsfx capability add tab`|
   |Para agregar bot|`teamsfx capability add bot`|
   |Para agregar la extensión de mensaje|`teamsfx capability add messaging-extension`|

## <a name="supported-capabilities"></a>Funciones admitidas

Además de las funcionalidades que ya tiene la aplicación Teams, puede elegir agregar diferentes funcionalidades a la aplicación de Teams. En la tabla siguiente se proporcionan las diferentes funcionalidades de Teams aplicación:

|Funcionalidades existentes|Otras funcionalidades admitidas|
|--------------------|--------------------|
|Pestañas con SPFx|Ninguno|
|Pestañas con Azure|Bot y extensión de mensaje|
|Bot|Pestañas|
|Extensión de mensajería|Pestañas y bots|
|Pestañas y bots|Pestañas y extensión de mensaje|
|Pestañas y extensión de mensaje|Pestañas y bots|
|Pestañas, bot y extensión de mensaje|Pestañas|
|Pestañas |Bot y extensión de mensaje|

## <a name="add-bot-tab-and-message-extension"></a>Agregar bot, pestaña y extensión de mensaje

Después de agregar un bot y una extensión de mensaje, los cambios en el proyecto son los siguientes:

* Se agrega un código de plantilla de bot a una subcarpeta con la ruta de acceso `yourProjectFolder/bot`. Esto incluye una plantilla de aplicación de bot **hello world** en el proyecto.
* `launch.json`y `task.json` en `.vscode` la carpeta se actualizan, lo que incluye los scripts necesarios para Visual Studio Code y se ejecuta cuando desea depurar la aplicación localmente.
* `manifest.template.json`se actualiza el archivo en `templates/appPackage` la carpeta , que incluye la información relacionada con el bot en el archivo de manifiesto que representa la aplicación en Teams Platform. Estos son los cambios:
  * El identificador del bot
  * Ámbitos del bot
  * Los comandos a los que la aplicación de bot hello world puede responder
* Los archivos de `templates/azure/teamsfx` se actualizan y `templates/azure/provision/xxx`los archivos .bicep se vuelven a generar.
* Los archivos de `.fx/config` se vuelven a generar, lo que garantiza que el proyecto esté configurado con las configuraciones adecuadas para la funcionalidad recién agregada.

Después de agregar la pestaña , los cambios en el proyecto son los siguientes:

* Se agrega un código de plantilla de pestaña de front-end a una subcarpeta con ruta de acceso `yourProjectFolder/tab`, que incluye una plantilla de aplicación **de pestaña hello world** en el proyecto.
* `launch.json`y `task.json` en `.vscode` la carpeta se actualizan, lo que incluye los scripts necesarios para Visual Studio Code y se ejecuta cuando desea depurar la aplicación localmente.
* `manifest.template.json`Se actualiza el archivo en `templates/appPackage` la carpeta , que incluye información relacionada con pestañas en el archivo de manifiesto que representa la aplicación en la plataforma de Teams. Los cambios son:
  * Pestañas configurables y estáticas
  * Ámbitos de las pestañas
* Los archivos de `templates/azure/teamsfx` se actualizarán y `templates/azure/provision/xxx`se volverá a generar el archivo .bicep.
* El archivo en `.fx/config` se regenera, lo que garantiza que el proyecto esté configurado con las configuraciones adecuadas para la funcionalidad recién agregada.

## <a name="step-by-step-guide"></a>Guía paso a paso

* Siga la guía [paso a paso](../sbs-gs-commandbot.yml) para compilar el bot de comandos en Microsoft Teams

* Siga la [guía paso a paso](../sbs-gs-notificationbot.yml) para compilar el bot de notificación en Microsoft Teams.

## <a name="see-also"></a>Vea también

* [Aprovisionar recursos en la nube](provision.md)
* [Creación de un nuevo proyecto de Teams](create-new-project.md)

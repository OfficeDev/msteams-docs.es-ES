---
title: Agregar funcionalidades a las aplicaciones de Teams
author: MuyangAmigo
description: En este módulo, aprenderá a agregar funcionalidades del kit de herramientas de Teams, ventajas, limitaciones y funcionalidades.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 90a1e28f4c7bb3d0bc9530fc1af8ad4d4e373c9b
ms.sourcegitcommit: 0c734a5809ad6eb36255c97f38589c67d0971741
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2022
ms.locfileid: "66830795"
---
# <a name="add-capabilities-to-teams-apps"></a>Adición de funcionalidades a aplicaciones de Teams

Agregar funcionalidad en el kit de herramientas de Teams le ayuda a agregar funcionalidad adicional a la aplicación de Teams existente. En la tabla siguiente se enumeran las funcionalidades de aplicación de Teams:

|**Capacidad**|**Descripción**|
|--------|-------------|
| Pestañas |  Las pestañas son etiquetas HTML sencillas que hacen referencia a los dominios declarados en el manifiesto de la aplicación. Puede agregar pestañas como parte del canal dentro de un equipo, chat en grupo o aplicación personal para un usuario individual.|
| Bots |  Los bots ayudan a interactuar con el servicio web a través de texto, tarjetas interactivas y módulos de tareas.|
| Extensiones de mensajes | Las extensiones de mensaje ayudan a interactuar con el servicio web a través de botones y formularios en el cliente de Microsoft Teams.|

## <a name="advantages"></a>Ventajas

En la lista siguiente se proporcionan ventajas para agregar más funcionalidades en TeamsFx:

* Proporciona comodidad.
* Agrega más funciones a la aplicación agregando automáticamente códigos fuente mediante Teams Toolkit.

## <a name="limitations"></a>Limitaciones

En la lista siguiente se proporcionan limitaciones para agregar más funcionalidades en TeamsFx:

* Puede agregar pestañas de hasta 16 instancias.
* Puede agregar un bot y una extensión de mensaje para una instancia cada una.

## <a name="add-capabilities"></a>Agregar funcionalidades

**Puede agregar funcionalidades mediante los métodos siguientes:**

* Para agregar funcionalidades mediante el kit de herramientas de Teams en Visual Studio Code.
* Para agregar funcionalidades mediante la paleta de comandos.

  > [!Note]
  > Debe aprovisionar para cada entorno, después de haber agregado correctamente las funcionalidades en la aplicación de Teams.

* **Para agregar funcionalidades mediante el kit de herramientas de Teams en Visual Studio Code:**

   1. Abra **Visual Studio Code**.
   1. Seleccione **Kit de herramientas de Teams** en el panel izquierdo.
   1. Seleccione **Agregar características** en **DESARROLLO**.

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/select-feature123.png" alt-text="actualizado uno":::

* **Para agregar funcionalidades mediante la paleta de comandos:**

   1. Abra **la paleta de comandos**.
   1. Escriba **Teams:Agregar características**.
   1. Presione **Entrar**.

      :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/teams-add-features.png" alt-text="Para agregar funcionalidades mediante la paleta de comandos.":::

   1. En el elemento emergente, seleccione la funcionalidad que se va a agregar en el proyecto.

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/notification-add-capabilities.png" alt-text="Notificación":::

## <a name="add-capabilities-using-teamsfx-cli"></a>Adición de funcionalidades mediante la CLI de TeamsFx

* Cambie el directorio de trabajo al **directorio del proyecto**.
* En la tabla siguiente se enumeran las funcionalidades y los comandos necesarios:

  |Funcionalidad y escenario| Comando|
  |-----------------------|----------|
  |Para agregar un bot de notificación |`teamsfx add notification`|
  |Para agregar un bot de comandos |`teamsfx add command-and-response`|
  |Para agregar la pestaña habilitada para sso |`teamsfx add sso-tab`|
  |Para agregar pestaña |`teamsfx add tab`|
  |Para agregar bot |`teamsfx add bot`|
  |Para agregar la extensión de mensaje |`teamsfx add message extension`|

## <a name="available-capabilities-to-add-for-different-teams-project"></a>Funcionalidades disponibles para agregar para diferentes proyectos de Teams

Puede elegir agregar diferentes funcionalidades en función del proyecto que haya creado en la aplicación Teams.
En la tabla siguiente se enumeran las funcionalidades disponibles para agregar en el proyecto:

|Funcionalidades existentes|Otras funcionalidades admitidas|
|--------------------|--------------------|
|Pestaña SPFx |Ninguno|
|Pestaña habilitada para SSO |Pestaña habilitada para SSO, bot de notificación, bot de comandos, bot, extensión de mensaje|
|Bot de notificación |Pestaña habilitada para SSO, pestaña|
|Bot de comandos |Pestaña habilitada para SSO, pestaña|
|Tab |Pestaña, bot de notificación, bot de comandos, bot, extensión de mensaje|
|Bot |Extensión de mensaje, pestaña habilitada para SSO, pestaña|
|Extensión de mensaje |Bot, pestaña habilitada para SSO, pestaña |

## <a name="add-bot-tab-and-message-extension"></a>Agregar bot, pestaña y extensión de mensaje

Después de agregar un bot y una extensión de mensaje, los cambios en el proyecto son los siguientes:

* Se agrega un código de plantilla de bot a una subcarpeta con la ruta de acceso `yourProjectFolder/bot`. Esto incluye una plantilla de aplicación de bot **hello world** en el proyecto.
* `launch.json`y `task.json` en `.vscode` la carpeta se actualizan, lo que incluye los scripts necesarios para Visual Studio Code y se ejecuta cuando desea depurar la aplicación localmente.
* `manifest.template.json` Se actualiza el archivo en `templates/appPackage` la carpeta , que incluye la información relacionada con el bot en el archivo de manifiesto que representa la aplicación en la Plataforma de Teams. Estos son los cambios:
  * El identificador del bot
  * Ámbitos del bot
  * Los comandos a los que la aplicación de bot hello world puede responder
* Los archivos de `templates/azure/teamsfx` se actualizan y `templates/azure/provision/xxx`los archivos .bicep se vuelven a generar.
* Los archivos de `.fx/config` se vuelven a generar, lo que garantiza que el proyecto se establece con las configuraciones adecuadas para la funcionalidad recién agregada.

Después de agregar la pestaña , los cambios en el proyecto son los siguientes:

* Se agrega un código de plantilla de pestaña de front-end a una subcarpeta con ruta de acceso `yourProjectFolder/tab`, que incluye una plantilla de aplicación **de pestaña hello world** en el proyecto.
* `launch.json`y `task.json` en `.vscode` la carpeta se actualizan, lo que incluye los scripts necesarios para Visual Studio Code y se ejecuta cuando desea depurar la aplicación localmente.
* `manifest.template.json` Se actualiza el archivo en `templates/appPackage` la carpeta , que incluye información relacionada con pestañas en el archivo de manifiesto que representa la aplicación en la Plataforma de Teams. Los cambios son:
  * Pestañas configurables y estáticas
  * Ámbitos de las pestañas
* Los archivos de `templates/azure/teamsfx` se actualizarán y `templates/azure/provision/xxx`se volverá a generar el archivo .bicep.
* El archivo en `.fx/config` se regenera, lo que garantiza que el proyecto se establece con las configuraciones adecuadas para la funcionalidad recién agregada.

## <a name="step-by-step-guide"></a>Guía paso a paso

* Siga la guía [paso a paso](../sbs-gs-commandbot.yml) para compilar un bot de comandos en Microsoft Teams

* Siga la guía [paso a paso](../sbs-gs-notificationbot.yml) para compilar el bot de notificación en Microsoft Teams.

## <a name="see-also"></a>Vea también

* [Aprovisionar recursos en la nube](provision.md)
* [Creación de un nuevo proyecto de Teams](create-new-project.md)

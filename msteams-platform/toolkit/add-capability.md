---
title: Agregar funcionalidades a las aplicaciones de Teams
author: surbhigupta
description: En este módulo, aprenderá a agregar funcionalidades del kit de herramientas de Teams.
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: abcda0dd19388d1cdce2f2b440ecbae833b5f9c3
ms.sourcegitcommit: 6926cf5eee55d5047c11ca13afc7f6f23e270396
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/27/2022
ms.locfileid: "68740607"
---
# <a name="add-capabilities-to-teams-apps"></a>Adición de funcionalidades a aplicaciones de Teams

Agregar funcionalidades con Teams Toolkit le ayuda a incluir características adicionales en la aplicación de Microsoft Teams existente. La ventaja de agregar más funcionalidades es que puede agregar más funciones a la aplicación agregando automáticamente códigos fuente mediante el kit de herramientas de Teams. También puede elegir diferentes funcionalidades en función del proyecto que haya creado en la aplicación de Teams. En la tabla siguiente se enumeran las funcionalidades de aplicación de Teams:

|Funcionalidad|Descripción|Otras funcionalidades admitidas|
|--------|-------------|-----------------|
|**Aplicación básica de Teams**|              |
| Tab |  Las pestañas son etiquetas HTML sencillas que hacen referencia a los dominios declarados en el manifiesto de la aplicación. Puede agregar pestañas como parte del canal dentro de un equipo, chat en grupo o aplicación personal para un usuario individual.|Pestaña, bot de notificación, bot de comandos, bot, extensión de mensaje|
|Pestaña SPFx| Las aplicaciones de pestaña SPFx se hospedan en Microsoft 365 y admiten el desarrollo y el hospedaje de la solución SPFx del lado cliente|Ninguno|
|Pestaña habilitada para SSO|Puede crear una aplicación de pestaña habilitada para SSO que permita al usuario con la característica de inicio de sesión único|Pestaña habilitada para SSO, bot de notificación, bot de comandos, bot, extensión de mensaje|
| Bot |  Los bots ayudan a interactuar con el servicio web a través de texto, tarjetas interactivas y módulos de tareas.|Extensión de mensaje, pestaña habilitada para SSO, pestaña|
| Extensión de mensaje | Las extensiones de mensaje ayudan a interactuar con el servicio web a través de botones y formularios en el cliente de Microsoft Teams.|Bot, pestaña habilitada para SSO, pestaña|
|**Aplicación de Teams basada en escenarios**|             |
| Bot de notificación | El bot de notificación envía de forma proactiva mensajes en el canal de Teams, el chat grupal o el chat personal. Puede desencadenar el bot de notificación con una solicitud HTTP, como tarjetas o textos. |Pestaña habilitada para SSO, pestaña|
| Bot de comandos | El bot de comandos le permite automatizar tareas repetitivas mediante un bot de comandos. Responde a comandos simples enviados en chats con tarjetas adaptables. |Pestaña habilitada para SSO, pestaña|
| Bot de flujo de trabajo| El bot de flujo de trabajo permite a los usuarios interactuar con una tarjeta adaptable habilitada por la característica de controlador de acciones tarjeta adaptable en la aplicación de bot de flujo de trabajo.|Pestaña habilitada para SSO, pestaña|

> [!NOTE]
> Puede agregar pestañas de hasta 16 instancias. En cuanto al bot y la extensión de mensaje, puede agregar uno para cada instancia a la vez.

## <a name="add-capabilities"></a>Agregar funcionalidades

Puede agregar funcionalidades mediante los métodos siguientes:

* [Uso del kit de herramientas de Teams en Microsoft Visual Studio Code](#using-teams-toolkit-in-microsoft-visual-studio-code)
* [Uso de la paleta de comandos](#using-the-command-palette)
* [Uso de la CLI de TeamsFx](#using-teamsfx-cli)

### <a name="using-teams-toolkit-in-microsoft-visual-studio-code"></a>Uso del kit de herramientas de Teams en Microsoft Visual Studio Code

   1. Abra **Visual Studio Code**.
   1. Seleccione **Kit de herramientas de Teams** en la barra de actividad.
   1. Seleccione **Agregar características** en **DESARROLLO**.

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/select-feature123.png" alt-text="Adición de funcionalidades del kit de herramientas de Teams":::

      > [!NOTE]
      > Después de agregar correctamente las funcionalidades en la aplicación de Teams, debe aprovisionar para cada entorno.

### <a name="using-the-command-palette"></a>Uso de la paleta de comandos

   1. Seleccione **Ver** > **paleta de comandos...** o **Ctrl+Mayús+P**.

      :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add-capabilities-command-palette.png" alt-text="Adición de funcionalidades desde la palata de comandos":::

   1. Escriba **Teams: Agregar características**.
   1. Presione Entrar.

      :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/teams-add-features.png" alt-text="Para agregar funcionalidades mediante la paleta de comandos.":::

   1. En el elemento emergente, seleccione la funcionalidad que necesita agregar en el proyecto.

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/notification-add-capabilities.png" alt-text="Notificación":::

### <a name="using-teamsfx-cli"></a>Uso de la CLI de TeamsFx

* Cambie el directorio de trabajo al **directorio del proyecto**.
* En la tabla siguiente se enumeran las funcionalidades y los comandos necesarios:

  |Funcionalidad y escenario| Get-Help|
  |-----------------------|----------|
  |Para agregar un bot de notificación |`teamsfx add notification`|
  |Para agregar un bot de comandos |`teamsfx add command-and-response`|
  |Para agregar la pestaña habilitada para SSO |`teamsfx add sso-tab`|
  |Para agregar pestaña |`teamsfx add tab`|
  |Para agregar bot |`teamsfx add bot`|
  |Para agregar la extensión de mensaje |`teamsfx add message extension`|

## <a name="changes-after-adding-capabilities"></a>Cambios después de agregar funcionalidades

En la tabla siguiente se muestran los cambios que se pueden ver en los archivos de la aplicación al agregar las funcionalidades:

|Agregar funcionalidad|Descripción| Cambios|
|------------|------------------------|---------|
|Bot, extensión de mensaje y pestaña|Incluye un bot **hello world**&nbsp;o una plantilla de aplicación de pestaña en el proyecto.|Se agrega un código de plantilla de pestaña o bot de front-end a una subcarpeta con ruta de acceso `yourProjectFolder/bot` o `yourProjectFolder/tab` respectivamente.|
| Bot, extensión de mensaje y pestaña |Incluye los scripts necesarios para Visual Studio Code y se ejecuta cuando desea depurar la aplicación localmente. |Los archivos `launch.json` y `task.json` en `.vscode` la carpeta se actualizan.|
| Bot y extensión de mensaje|Incluye información relacionada con bots o pestañas en el archivo de manifiesto que representa la aplicación en la plataforma teams.|Se actualiza el archivo`manifest.template.json` en `templates/appPackage` la carpeta , que incluye información relacionada con pestañas en el archivo de manifiesto que representa la aplicación en la Plataforma de Teams. Los cambios son visibles en el identificador del bot, los ámbitos del bot y los comandos a los que hello world bot o la aplicación de pestaña pueden responder.|
|Tab|Incluye información relacionada con bots o pestañas en el archivo de manifiesto que representa la aplicación en la plataforma teams.|Se actualiza el archivo `manifest.template.json` en `templates/appPackage` la carpeta , que incluye información relacionada con pestañas en el archivo de manifiesto que representa la aplicación en la Plataforma de Teams. Los cambios son visibles en pestañas configurables y estáticas, y ámbitos de las pestañas.|
|Bot, extensión de mensaje y pestaña|Incluye información relacionada con&nbsp;bots o pestañas en teamsfx y archivos de aprovisionamiento que son para integrar funciones de Azure.|Los archivos de `templates/azure/teamsfx` se actualizan y `templates/azure/provision/xxx`los archivos .bicep se vuelven a generar.|
|Bot, extensión de mensaje y pestaña|Garantiza que el proyecto está configurado con las configuraciones adecuadas para la funcionalidad recién agregada.|Los archivos de `.fx/config` se vuelven a generar|

## <a name="step-by-step-guide"></a>Guía paso a paso

* Siga la guía [paso a paso](../sbs-gs-commandbot.yml) para compilar un bot de comandos en Microsoft Teams.

* Siga la guía [paso a paso](../sbs-gs-notificationbot.yml) para compilar el bot de notificación en Microsoft Teams.

* Siga la guía [paso a paso](../sbs-gs-workflow-bot.yml) para crear un bot de flujo de trabajo en Microsoft Teams.

## <a name="see-also"></a>Vea también

* [Aprovisionar recursos en la nube](provision.md)
* [Creación de un nuevo proyecto de Teams](create-new-project.md)

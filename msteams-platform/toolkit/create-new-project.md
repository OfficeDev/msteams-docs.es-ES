---
title: Crear una nueva aplicación de Teams
author: zyxiaoyuer
description: En este módulo, aprenderá a crear una nueva aplicación de Teams mediante el kit de herramientas de Teams.
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
ms.openlocfilehash: e64daa0c3288f97286177e814204404522a6d6b9
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616623"
---
# <a name="create-a-new-teams-project"></a>Creación de un nuevo proyecto de Teams

Puede crear un nuevo proyecto de Teams seleccionando **Crear una nueva aplicación de Teams** en Teams Toolkit. Puede crear los siguientes tipos de aplicación en el kit de herramientas de Teams:

| Tipo de aplicación | Definición |
| --- | --- |
| Aplicación básica de Teams | Las aplicaciones básicas de Teams son aplicaciones de extensión de pestañas, bots o mensajes que puede crear y personalizar según sus necesidades. |
| Aplicación de Teams basada en escenarios | Las aplicaciones de Teams basadas en escenarios son bot de notificación, bot de comandos, pestaña habilitada para SSO o aplicación de pestaña SPFx y es adecuada para un escenario determinado. Por ejemplo, el bot de notificación solo es adecuado para enviar notificaciones y no se usa para el chat. |

## <a name="create-a-new-teams-app"></a>Crear una nueva aplicación de Teams

Los pasos para crear una nueva aplicación de Teams son similares para todos los tipos de aplicación, excepto SPFx y bot de notificación. Los pasos siguientes le ayudan a crear una nueva aplicación de pestaña:

**Para crear una aplicación**

1. Abrir Visual Studio Code.
1. Seleccione el icono kit de herramientas de :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: Teams.
1. Seleccione **Crear una nueva aplicación de Teams**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-teams-app.png" alt-text="Barra lateral del kit de herramientas de Teams":::

1. Seleccione **Crear una nueva aplicación de Teams** para crear una aplicación mediante el kit de herramientas de Teams.

   :::image type="content" source="../assets/images/teams-toolkit-v2/select-create-app.png" alt-text="Crear una aplicación":::

1. En este tutorial, seleccione **Tab** como la funcionalidad para compilar la aplicación.

   :::image type="content" source="../assets/images/teams-toolkit-v2/select-tabapp1.png" alt-text="Seleccionar funcionalidad de la aplicación":::

   > [!NOTE]
   > Puede seleccionar cualquier tipo de funcionalidad según sus necesidades.

1. Seleccione **JavaScript** como lenguaje de programación.

    :::image type="content" source="../assets/images/teams-toolkit-v2/select-language-tab.png" alt-text="Captura de pantalla que muestra cómo seleccionar el lenguaje de programación":::

1. Seleccione la ubicación del área de trabajo del proyecto y **seleccione Carpeta**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/select-folder1.png" alt-text="select-folder":::

1. En este tutorial, escriba `helloworld` como nombre de la aplicación. Seleccione **Introducir**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/enter-name-tab.png" alt-text="Captura de pantalla que muestra dónde escribir el nombre de la aplicación":::

   > [!NOTE]
   > Puede escribir su propio nombre de aplicación para otras funcionalidades y asegurarse de que solo usa caracteres alfanuméricos.

   La aplicación de pestaña Teams se crea en unos segundos.

    :::image type="content" source="../assets/images/teams-toolkit-v2/tap-app-created1.png" alt-text="Captura de pantalla que muestra la aplicación creada":::

### <a name="directory-structure-for-different-app-types"></a>Estructura de directorios para diferentes tipos de aplicaciones

Teams Toolkit proporciona todos los componentes para crear una aplicación. Después de crear el proyecto, puede ver las carpetas y los archivos del proyecto en **el Explorador**.

<br>
<details>
<summary><b>Estructura de directorios para la aplicación básica de Teams</b></summary>

Tiene tres tipos diferentes de aplicación básica de Teams y la estructura de directorios es similar para todos los tipos de aplicaciones. En el ejemplo siguiente se muestra una estructura básica de directorios de aplicación de pestaña de Teams:

| Nombre de la carpeta | Contenido |
| --- | --- |
| `.fx/configs` | Archivos de configuración que el usuario puede personalizar para la aplicación teams. |
| - `.fx/configs/config.<envName>.json` | Archivo de configuración para cada entorno. |
| - `.fx/configs/azure.parameters.<envName>.json` | Archivo de parámetros para el aprovisionamiento de Azure BICEP para cada entorno. |
| - `.fx/configs/projectSettings.json` | Configuración global del proyecto que se aplica a todos los entornos. |
| `tabs` | Código para la funcionalidad Tab necesaria en tiempo de ejecución, como el aviso de privacidad, los términos de uso y las pestañas de configuración. |
| - `tabs/src/index.jsx` | Punto de entrada para la aplicación front-end, donde se representa el componente principal de la aplicación con `ReactDOM.render()` |
| - `tabs/src/components/App.jsx` | Código para controlar el enrutamiento de direcciones URL en la aplicación. Llama al [SDK del cliente de JavaScript de Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md) para establecer la comunicación entre la aplicación y Teams. |
| - `tabs/src/components/Tab.jsx` | Código para implementar la interfaz de usuario de la aplicación. |
| - `tabs/src/components/TabConfig.jsx` | Código para implementar la interfaz de usuario que configura la aplicación. |
| `templates/appPackage` | Archivos de plantilla de manifiesto de aplicación e iconos de aplicación: color.png y outline.png. |
| - `templates/appPackage/manifest.template.json` | Manifiesto de aplicación para ejecutar la aplicación en un entorno local o remoto.  |
| `templates/azure` | Archivos de plantilla de BICEP |

> [!NOTE]
> Si tiene una aplicación de extensión de bot o mensaje, se agregan carpetas pertinentes a la estructura de directorios.

Para obtener más información sobre la estructura de directorios de los distintos tipos de aplicaciones básicas de Teams, consulte la tabla siguiente:

| Tipo de aplicación | Vínculos |
| --- | --- |
| Para la aplicación de pestaña | [Cree su primera aplicación de pestaña con JavaScript](../sbs-gs-javascript.yml) |
| Para la aplicación bot | [Cree su primera aplicación de bot con JavaScript](../sbs-gs-bot.yml) |
| Para la aplicación de extensión de mensaje | [Cree su primera aplicación de extensión de mensajes con JavaScript](../sbs-gs-msgext.yml) |

</details>
<br>
<details>
<summary><b>Estructura de directorios para una aplicación de Teams basada en escenarios</b></summary>

Tiene cuatro tipos diferentes de aplicaciones de Teams basadas en escenarios y la estructura de directorios es similar para todos los tipos de aplicaciones. En el ejemplo siguiente se muestra una estructura de directorio de la aplicación teams del bot de notificación basada en escenarios:

La nueva carpeta del proyecto contiene el siguiente contenido:

| Nombre de la carpeta | Contenido |
| --- | --- |
| `.fx` | Configuración de nivel de proyecto, configuración e información del entorno |
| `.vscode` | Archivos de código de VS para la depuración local |
| `bot` | Código fuente del bot |
| `templates` | Plantillas para el manifiesto de aplicación de Teams y los recursos de Azure correspondientes |

La implementación de notificación principal en la carpeta **bot** y contiene:

| Nombre de archivo | Contenido |
| --- | --- |
| `src/adaptiveCards/` | Plantillas para tarjeta adaptable  |
| `src/internal/` | Código de inicialización generado para la funcionalidad de notificación |
| `src/index.*s` | El punto de entrada para controlar los mensajes del bot y enviar notificaciones |
| `.gitignore` | Archivo para excluir archivos locales del proyecto de bot |
| `package.json` | El archivo de paquete npm para el proyecto de bot |

> [!NOTE]
> Si tiene un bot de comandos, una pestaña habilitada para SSO o una aplicación de pestaña SPFx, se agregan carpetas pertinentes a la estructura de directorios.

Para obtener más información sobre la estructura de directorios de diferentes tipos de aplicaciones de Teams basadas en escenarios, consulte la tabla siguiente:

| Tipo de aplicación | Vínculos |
| --- | --- |
| Para la aplicación de bot de notificación | [Enviar notificación a Teams](../sbs-gs-notificationbot.yml) |
| Para la aplicación de bot de comandos | [Crear un bot de comandos](../sbs-gs-commandbot.yml) |
| Para la aplicación de pestaña SPFx | [Crear una aplicación Teams con SPFx](../sbs-gs-spfx.yml) |

</details>
<br>
<details>
<summary><b>Estructura de directorios para la aplicación de varias funcionalidades</b></summary>

Puede agregar más características a la aplicación de Teams existente mediante agregar características. Por ejemplo, si agrega una aplicación de bot a la aplicación de pestaña existente, Teams Toolkit agrega la carpeta del bot con los archivos y el código pertinentes.

En la imagen siguiente se muestra la estructura de directorios de la aplicación de tabulación:

   :::image type="content" source="../assets/images/teams-toolkit-v2/tabapp-directory.png" alt-text="Estructura del directorio de la aplicación de tabulación":::

En la imagen siguiente se muestra la estructura de directorios de la aplicación de pestaña con la característica bot:

   :::image type="content" source="../assets/images/teams-toolkit-v2/tab-app-with-bot-app.png" alt-text="Tab app with bot app directory structure (Aplicación de tabulación con estructura de directorio de aplicación de bot)":::

</details>

## <a name="see-also"></a>Vea también

* [Crear una aplicación de Teams con Blazor](../sbs-gs-blazorupdate.yml)
* [Crear una aplicación Teams con C# o .NET](../sbs-gs-csharp.yml)
* [Requisitos previos para todos los tipos de entorno y creación de la aplicación de Teams](tools-prerequisites.md)
* [Preparación para compilar aplicaciones mediante el kit de herramientas de Microsoft Teams](build-environments.md)

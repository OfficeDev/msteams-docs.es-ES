---
title: Crear una nueva aplicación de Teams
author: zyxiaoyuer
description: En este módulo, aprenderá a crear una nueva aplicación de Teams mediante el kit de herramientas de Teams.
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 8ed7d882ba7d58862539e77bfc8b6ea5277a3729
ms.sourcegitcommit: 637b8f93b103297b1ff9f1af181680fca6f4499d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2022
ms.locfileid: "68499247"
---
# <a name="create-a-new-teams-project"></a>Creación de un nuevo proyecto de Teams

En esta sección, puede aprender a crear un nuevo proyecto de Teams mediante Visual Studio Code y Visual Studio.

::: zone pivot="visual-studio-code"

## <a name="create-a-new-teams-project-for-visual-studio-code"></a>Creación de un nuevo proyecto de Teams para Visual Studio Code

Puede crear un nuevo proyecto de Teams seleccionando **Crear una nueva aplicación de Teams** en Teams Toolkit. Puede crear los siguientes tipos de aplicación en el kit de herramientas de Teams:

| Tipo de aplicación | Definición |
| --- | --- |
| Aplicación básica de Teams | Las aplicaciones básicas de Teams son aplicaciones de extensión de pestañas, bots o mensajes que puede crear y personalizar según sus necesidades. |
| Aplicación de Teams basada en escenarios | Las aplicaciones de Teams basadas en escenarios son bot de notificación, bot de comandos, pestaña habilitada para SSO o aplicación de pestaña SPFx y es adecuada para un escenario determinado. Por ejemplo, el bot de notificación solo es adecuado para enviar notificaciones y no se usa para el chat. |

## <a name="create-a-new-teams-app"></a>Crear una nueva aplicación de Teams

Los pasos para crear una nueva aplicación de Teams son similares para todos los tipos de aplicación, excepto SPFx y bot de notificación. Los pasos siguientes le ayudan a crear una nueva aplicación de pestaña:

**Para crear una aplicación**

1. Abrir Visual Studio Code.

1. Seleccione el icono kit de herramientas de :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png"::: Teams en la barra de navegación izquierda.

1. Seleccione **Crear una nueva aplicación de Teams**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/create-project.png" alt-text="Ubicación del vínculo Crear nuevo proyecto en la barra lateral del Kit de herramientas de Teams.":::

1. Asegúrese de que **La pestaña** está seleccionada como funcionalidad de la aplicación.

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-capabilities-tabapp.png" alt-text="Seleccionar funcionalidad de la aplicación":::

1. Seleccione **JavaScript** como lenguaje de programación.

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-language-tab.png" alt-text="Captura de pantalla que muestra cómo seleccionar el lenguaje de programación.":::

1. Seleccione **Carpeta predeterminada** para almacenar la carpeta raíz del proyecto en la ubicación predeterminada.

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-default-location.png" alt-text="Selección de la ubicación predeterminada":::

   Los pasos siguientes le guían para cambiar la ubicación predeterminada:

      1. Seleccione **Examinar**.

          :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-browse.png" alt-text="Seleccionar examinar para el almacenamiento":::

      1. Seleccione la ubicación del área de trabajo del proyecto.

      1. Seleccione **seleccionar carpeta**.

          :::image type="content" source="../assets/images/teams-toolkit-v2/select-folder.png" alt-text="select-folder para el almacenamiento":::

1. Escriba `helloworld` como el nombre de la aplicación. Asegúrese de usar solo caracteres alfanuméricos. Seleccione **Introducir**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/enter-name-tab1.png" alt-text="Captura de pantalla que muestra dónde escribir el nombre de la aplicación.":::

1. De forma predeterminada, el proyecto se abre en una nueva ventana en 10 segundos. Si desea abrir en la ventana actual, seleccione **Abrir en la ventana actual**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/new-window-notification.png" alt-text="Nueva notificación de ventana":::

   La aplicación de pestaña Teams se crea en unos segundos.

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/tap-app-created1.png" alt-text="Captura de pantalla que muestra la aplicación creada.":::

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
| `src/index.*s` | Punto de entrada para controlar los mensajes del bot y enviar notificaciones |
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

::: zone-end

::: zone pivot="visual-studio"

## <a name="create-new-teams-app-in-visual-studio"></a>Creación de una nueva aplicación de Teams en Visual Studio

Teams Toolkit proporciona plantillas de aplicación de Microsoft Teams en Visual Studio para crear una aplicación de Teams.  Puede buscar y seleccionar la plantilla de aplicación de Teams que necesite al crear un nuevo proyecto. Puede tener plantillas de aplicación de Teams para crear:

* Aplicación tab
* Bot de comandos
* Bot de notificación
* Aplicación de extensión de mensaje

## <a name="prerequisites"></a>Requisitos previos

| &nbsp; | Instalar | Para usar... |
| --- | --- | --- |
| &nbsp; | **Required** | &nbsp; |
| &nbsp; | Versión 17.3 de Visual Studio | Puede instalar la edición enterprise de Visual Studio e instalar la carga de trabajo "ASP.NET" y las herramientas de desarrollo de Microsoft Teams. |
| &nbsp; | Kit de herramientas de Teams | Extensión de Visual Studio que crea un scaffolding de proyecto para la aplicación. Use la versión más reciente. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams para colaborar con todos los usuarios con los que trabaja a través de aplicaciones de chat, reuniones, llamadas, todo en un solo lugar. |
 | &nbsp; | [Preparar el espacio empresarial de Microsoft 365](../concepts/build-and-test/prepare-your-o365-tenant.md) | Acceso a la cuenta de Teams con los permisos adecuados para instalar una aplicación. |

## <a name="create-a-new-teams-app"></a>Crear una nueva aplicación de Teams

Los pasos para crear una nueva aplicación de Teams son similares para todos los tipos de aplicación, excepto para el bot de notificación. Los pasos siguientes le ayudarán a crear una nueva aplicación de pestaña:

1. Abra Visual Studio.
1. Cree un nuevo proyecto mediante una de las dos opciones siguientes.

     :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project1_1.png" alt-text="Creación de un nuevo proyecto con código a partir de la introducción":::

    * Seleccione **Crear un nuevo proyecto** en **Introducción** para elegir la plantilla de proyecto con scaffolding de código.
    * Seleccione **Continuar sin código** para crear un proyecto sin scaffolding de código y seleccione **Archivo** > **nuevo** > **proyecto** en Visual Studio.

        :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project2_1.png" alt-text="Menú Crear nuevo proyecto desde el archivo":::

   Aparece **la ventana Crear un nuevo proyecto** .  

1. Escriba teams en el cuadro de búsqueda y, en la lista, seleccione **Aplicación de Microsoft Teams** y, a continuación, seleccione **Siguiente**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/visual-studio.png" alt-text="Buscar y elegir una aplicación de Microsoft Teams":::

   Aparecerá **la ventana Configurar el nuevo proyecto** .

     :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app-project-name_1.png" alt-text="Asignar un nombre a la aplicación":::

    1. Escriba un nombre adecuado para el proyecto.

         > [!NOTE]
         > El nombre del proyecto que escribe también se rellena automáticamente en nombre **de la solución** . Si lo desea, puede cambiar el nombre de la solución sin afectar al nombre del proyecto.

    1. Seleccione la ruta de acceso de la carpeta donde desea crear el área de trabajo del proyecto.
    1. Escriba un nombre de solución diferente, si lo desea.
    1. Active la opción para guardar el proyecto y la solución en la misma carpeta, si lo desea. Para este tutorial, no necesita esta opción.
    1. Seleccione **Crear**.

   Aparece **la ventana Crear una nueva aplicación de Teams** .

1. En este tutorial, se selecciona **Tab** para crear una nueva aplicación de Teams y seleccionar **Crear**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app-type_3.png" alt-text="Seleccionar el tipo de aplicación de Teams":::

   > [!NOTE]
   > Puede seleccionar el tipo necesario de aplicación de Teams para el proyecto.

   Aparece **la ventana Introducción** con **Bienvenido al kit de herramientas de Teams**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-getting-started-page.png" alt-text="Seleccione el kit de herramientas Introducción teams":::

### <a name="directory-structure"></a>Estructura de directorios

Teams Toolkit proporciona todos los componentes para crear una aplicación. Después de crear el proyecto, puede ver las carpetas y los archivos del proyecto en el Explorador.

* **Estructura de directorios para la aplicación básica de Teams**

  :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project-solution-explorer_1.png" alt-text="Seleccione la pestaña Explorador de soluciones kit de herramientas de teams":::

* **Estructura de directorios para una aplicación de Teams basada en escenarios**

  :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project-solution-explorer.png" alt-text="Seleccione el kit de herramientas Explorador de soluciones teams":::

## <a name="teams-app-templates-in-teams-toolkit-for-visual-studio"></a>Plantillas de aplicación de Teams en Teams Toolkit for Visual Studio

Puede ver las plantillas de aplicación de Teams ya rellenadas en Teams Toolkit para varios tipos de aplicación de Teams. En la tabla siguiente se enumeran todas las plantillas disponibles:

|Plantilla de aplicación de Teams  |Descripción  |
|---------|---------|
|Bot de notificación     |La aplicación Bot de notificación puede enviar una notificación al cliente de Teams; hay varias maneras de desencadenar la notificación. Por ejemplo, desencadene la notificación por solicitud HTTP o por tiempo. También puede seleccionar la notificación desencadenada en función del escenario empresarial.         |
|Bot de comandos     |Los usuarios pueden escribir un comando para interactuar con el bot mediante la aplicación Bot de comandos.         |
|Tab     |La aplicación Tab muestra una página web dentro de Teams y habilita el inicio de sesión único con la cuenta de Teams.         |
|Extensión de mensaje     |La aplicación extensión de mensaje implementa características sencillas como crear tarjeta adaptable, buscar paquetes Nugget, desenvolver vínculos para el dominio "dev.botframework.com".         |

> [!NOTE]
> Una vez creado el proyecto, El kit de herramientas de Teams abre automáticamente la ventana **Introducción** . Ahora puede ver las instrucciones en la ventana **Introducción** y consultar las distintas características del kit de herramientas de Teams.

::: zone-end

## <a name="see-also"></a>Vea también

* [Crear una aplicación de Teams con Blazor](../sbs-gs-blazorupdate.yml)
* [Crear una aplicación Teams con C# o .NET](../sbs-gs-csharp.yml)
* [Requisitos previos para todos los tipos de entorno y creación de la aplicación de Teams](tools-prerequisites.md)
* [Preparación para compilar aplicaciones mediante el kit de herramientas de Microsoft Teams](build-environments.md)
* [Aprovisionamiento de recursos en la nube mediante Visual Studio](provision-cloud-resources.md)
* [Implementación de una aplicación de Teams en la nube mediante Visual Studio](deploy-teams-app.md)

---
title: Crear aplicaciones con el Microsoft Teams Toolkit y Visual Studio Code
description: Introducción a la creación de excelentes aplicaciones personalizadas directamente Visual Studio Code con el Microsoft Teams Toolkit
keywords: Kit de herramientas de código visual studio de teams
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: d51ccf3ed62e22fb417eec72d1f409b1b77b9da6
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52629840"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>Crear aplicaciones con el Teams Toolkit y Visual Studio Code

El kit de herramientas de Microsoft Teams le permite crear aplicaciones personalizadas de Teams directamente desde el entorno de Visual Studio Code. El kit de herramientas le orienta en el proceso y le ofrece todo lo que necesita para crear, depurar e iniciar su aplicación de Teams.

## <a name="installing-the-teams-toolkit"></a>Instalación del Teams Toolkit

El Microsoft Teams Toolkit para Visual Studio Code está disponible para su descarga desde [Visual Studio Marketplace](https://aka.ms/teams-toolkit) o directamente como una extensión dentro de Visual Studio Code.

> [!TIP]
> Después de la instalación, debería ver el Teams Toolkit en la barra Visual Studio Code actividad. Si no es así, haga clic con el botón secundario en la barra de actividades **y seleccione Microsoft Teams** para anclar el kit de herramientas para facilitar el acceso.

## <a name="using-the-toolkit"></a>Uso del kit de herramientas

- [Configurar un nuevo proyecto](#set-up-a-new-teams-project)
- [Importar un proyecto existente](#import-an-existing-teams-app-project)
- [Configurar la aplicación](#configure-your-app)
- [Empaquetar la aplicación](#package-your-app)
- [Ejecute la aplicación localmente o en Teams](#run-your-app)

## <a name="set-up-a-new-teams-project"></a>Configurar un nuevo proyecto Teams proyecto

1. Cree un área de trabajo o una carpeta para el proyecto en el entorno local.
1. En Visual Studio Code, seleccione el icono Teams icono ![Icono de Teams](../assets/icons/favicon-16x16.png) de la barra de actividades en el lado izquierdo de la ventana.
1. Seleccione **Abrir el Microsoft Teams Toolkit** en el menú de comandos.
1. Selecciona **Crear una nueva aplicación Teams en** el menú de comandos.
1. Cuando se le pida, escriba el nombre del área de trabajo . Se usará como el nombre de la carpeta donde residirá el proyecto y el nombre predeterminado de la aplicación.
1. Presiona **Entrar** y llegarás a la pantalla Agregar **capacidades** para configurar las propiedades de la nueva aplicación.
1. Seleccione el **botón Finalizar** para completar el proceso de configuración.

## <a name="import-an-existing-teams-app-project"></a>Importar un proyecto de Teams aplicación existente

1. En Visual Studio Code, seleccione el icono Teams icono ![Icono de Teams](../assets/icons/favicon-16x16.png) de la barra de actividades en el lado izquierdo de la ventana.
1. Selecciona **Importar paquete de aplicación** en el menú de comandos.
1. Elige el archivo zip Teams [paquete de](/microsoftteams/platform/concepts/build-and-test/apps-package?view=msteams-client-js-latest&preserve-view=true) la aplicación existente.
1. Elija el **botón Seleccionar paquete de** publicación. La pestaña de configuración del kit de herramientas ahora debe rellenarse con los detalles de la aplicación.
1. En Visual Studio Code, seleccione **Agregar** carpeta de archivo al área de trabajo para agregar el directorio de código fuente  ->   al área Visual Studio Code de trabajo.

## <a name="configure-your-app"></a>Configurar la aplicación

En su núcleo, la aplicación Teams abarca tres componentes:

  1. El Microsoft Teams (web, de escritorio o móvil) donde los usuarios interactúan con la aplicación.
  1. Un servidor que responde a las solicitudes de contenido que se mostrarán en Teams. Por ejemplo, contenido de pestaña HTML o una tarjeta adaptable de bot.
  1. Un Teams de la aplicación consta de tres archivos:

      > [!div class="checklist"]
      >
      > - El manifest.jsen. 
      > - Icono [de color para](../resources/schema/manifest-schema.md#icons) que la aplicación se muestre en el catálogo de aplicaciones públicas u de la organización.
      > - Icono [de esquema para](../resources/schema/manifest-schema.md#icons) mostrar en la barra Teams actividad.

Cuando se instala una aplicación, el cliente Teams analiza el archivo de manifiesto para determinar la información necesaria, como el nombre de la aplicación y la dirección URL donde se encuentran los servicios.

1. Para configurar la aplicación, ve a la **pestaña Microsoft Teams Toolkit** en Visual Studio Code.
1. Selecciona **Editar paquete de aplicación** para ver la página detalles de **la** aplicación.
1. La edición de los campos de la página detalles de la aplicación actualiza el contenido del archivo manifest.jsen que, en última instancia, se enviará como parte del paquete de la aplicación. Para obtener más información, consulta [Editor de manifiestos de App Studio](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>Empaquetar la aplicación

La modificación de **los archivos** de **página,** manifiesto o **.env** de la carpeta  **.publish** de la aplicación generará automáticamente el **Development.zip** aplicación. Tendrás que incluir dos [iconos](../concepts/build-and-test/apps-package.md#app-icons) en esa misma carpeta.

## <a name="install-and-run-your-app-locally"></a>Instalar y ejecutar la aplicación localmente

## <a name="run-your-app"></a>Ejecutar la aplicación

### <a name="install-and-run-your-app-locally"></a>Instalar y ejecutar la aplicación localmente

Consulta la **página principal crear y** ejecutar contenido en la página principal del proyecto para obtener instrucciones detalladas sobre cómo empaquetar y probar la aplicación. En general, debes instalar el servidor de la aplicación, ejecutarla y, a continuación, configurar una solución de túnel para que Teams el contenido que se ejecuta desde localhost.

### <a name="enable-development-from-localhost"></a>Habilitar el desarrollo desde localhost

Si quieres depurar la aplicación basada en pestañas en localhost con HTTPS, deberás decir a tu explorador que confíe en la aplicación desde `<https://localhost>` . Vaya a `<https://localhost:3000/tab>`. Si ve una advertencia que indica que el sitio no es de confianza, elija la opción para continuar de todos modos. La aplicación ahora debe ser accesible desde el Teams cliente.

### <a name="run-your-app-in-teams"></a>Ejecute la aplicación en Teams

Requisitos previos: [habilitar Teams modo de vista previa para desarrolladores](https://aka.ms/teams-toolkit-enable-devpreview)

1. Vaya a la barra de actividades de la parte izquierda de la ventana Visual Studio Code actividad.
1. Seleccione el **icono Ejecutar** para mostrar la vista **Ejecutar y** depurar.
1. También puede usar el método abreviado de teclado `Ctrl+Shift+D` .

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Mantenimiento y soporte técnico de la aplicación publicada](../concepts/deploy-and-publish/appsource/post-publish/overview.md)

---
title: Cree aplicaciones con el Microsoft Teams Toolkit y el Visual Studio Code
description: Comience a crear grandes aplicaciones personalizadas directamente dentro de Visual Studio Code con la Microsoft Teams Toolkit
keywords: equipos visual studio code toolkit
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: efd0962e9c4c0d64dbac47caf29b2e56907937b3
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566561"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>Cree aplicaciones con el Teams Toolkit y Visual Studio Code

El kit de herramientas de Microsoft Teams le permite crear aplicaciones personalizadas de Teams directamente desde el entorno de Visual Studio Code. El kit de herramientas le orienta en el proceso y le ofrece todo lo que necesita para crear, depurar e iniciar su aplicación de Teams.

## <a name="installing-the-teams-toolkit"></a>Instalación de la Teams Toolkit

El Microsoft Teams Toolkit para Visual Studio Code está disponible para su descarga desde [el Mercado de Visual Studio](https://aka.ms/teams-toolkit) o directamente como una extensión dentro de Visual Studio Code.

> [!TIP]
> Después de la instalación, debería ver la Teams Toolkit en la barra de actividades Visual Studio Code. Si no es así, haga clic con el botón derecho en la barra de actividades y seleccione **Microsoft Teams** para anclar el kit de herramientas para facilitar el acceso.

## <a name="using-the-toolkit"></a>Uso del kit de herramientas

- [Establecer un nuevo proyecto](#set-up-a-new-teams-project)
- [Importar un proyecto existente](#import-an-existing-teams-app-project)
- [Configurar la aplicación](#configure-your-app)
- [Empaqueta tu aplicación](#package-your-app)
- [Ejecute la aplicación localmente o en Teams](#run-your-app)

## <a name="set-up-a-new-teams-project"></a>Establecer un nuevo proyecto de Teams

1. Cree un área de trabajo o una carpeta para el proyecto en el entorno local.
1. En Visual Studio Code, seleccione el icono de Teams ![Icono de Teams](../assets/icons/favicon-16x16.png) desde la barra de actividades en el lado izquierdo de la ventana.
1. Seleccione **Abrir el Microsoft Teams Toolkit** en el menú de comandos.
1. Seleccione **Crear una nueva aplicación de Teams** en el menú de comandos.
1. Cuando se le solicite, escriba el nombre del área de trabajo. Esto se usará como el nombre de la carpeta donde residirá el proyecto y el nombre predeterminado de la aplicación.
1. Pulse **Intro** y llegará a la pantalla **Agregar funcionalidades** para configurar las propiedades de la nueva aplicación.
1. Seleccione el botón **Finalizar** para completar el proceso de configuración.

## <a name="import-an-existing-teams-app-project"></a>Importar un proyecto de aplicación de Teams existente

1. En Visual Studio Code, seleccione el icono de Teams ![Icono de Teams](../assets/icons/favicon-16x16.png) desde la barra de actividades en el lado izquierdo de la ventana.
1. Seleccione **Importar paquete** de aplicación en el menú de comandos.
1. Elija el archivo zip [del paquete de Teams aplicación](../concepts/build-and-test/apps-package.md) existente.
1. Elija el botón **Seleccionar paquete de publicación.** La pestaña de configuración del kit de herramientas ahora debe rellenarse con los detalles de la aplicación.
1. En Visual Studio Code, seleccione   ->  **Agregar carpeta de archivos al área de trabajo** para agregar el directorio de código fuente al área de trabajo Visual Studio Code.

## <a name="configure-your-app"></a>Configurar la aplicación

En esencia, la aplicación Teams abarca tres componentes:

  1. El cliente Microsoft Teams (web, de escritorio o móvil) donde los usuarios interactúan con la aplicación.
  1. Servidor que responde a las solicitudes de contenido que se mostrarán en Teams. Por ejemplo, contenido de la pestaña HTML o una tarjeta adaptable a bots.
  1. Un paquete de [aplicación](/concepts/build-and-test/apps-package.md) Teams que consta de tres archivos:

      > [!div class="checklist"]
      >
      > - El manifest.js. 
      > - Icono [de color](../resources/schema/manifest-schema.md#icons) para que la aplicación se muestre en el catálogo de aplicaciones públicas u organizativas.
      > - Icono [de contorno](../resources/schema/manifest-schema.md#icons) para mostrar en la barra de actividades Teams.

Cuando se instala una aplicación, el cliente Teams analiza el archivo de manifiesto para determinar la información necesaria, como el nombre de la aplicación y la dirección URL donde se encuentran los servicios.

1. Para configurar la aplicación, vaya a la pestaña **Microsoft Teams Toolkit** en Visual Studio Code.
1. Seleccione **Editar paquete de aplicación** para ver la página Detalles de la **aplicación.**
1. La edición de los campos de la página Detalles de la aplicación actualiza el contenido de la manifest.jsen el archivo que, en última instancia, se enviará como parte del paquete de la aplicación. Para obtener más información, consulte [Editor de manifiestos de App Studio](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>Empaqueta tu aplicación

La modificación de la página de detalles de la **aplicación,** **el manifiesto** o los archivos **.env** en la carpeta **.publish** de la aplicación generará automáticamente el archivo **Development.zip.** Deberá incluir dos [iconos](../concepts/build-and-test/apps-package.md#app-icons) en esa misma carpeta.

## <a name="install-and-run-your-app-locally"></a>Instale y ejecute la aplicación localmente

## <a name="run-your-app"></a>Ejecute la aplicación

### <a name="install-and-run-your-app-locally"></a>Instale y ejecute la aplicación localmente

Consulte la página **principal Compilar y ejecutar** del proyecto para obtener instrucciones detalladas sobre cómo empaquetar y probar la aplicación. En general, debe instalar el servidor de la aplicación, ponerlo en ejecución y, a continuación, configurar una solución de tunelización para que Teams pueda acceder al contenido que se ejecuta desde localhost.

### <a name="enable-development-from-localhost"></a>Habilitar el desarrollo desde localhost

Si desea depurar la aplicación basada en la pestaña en localhost mediante HTTPS, deberá indicar a su navegador que confíe en la aplicación desde la que se <https://localhost> sirve. Vaya a <https://localhost:3000/tab>. Si ve una advertencia que indica que el sitio no es de confianza, elija la opción para continuar de todos modos. La aplicación ahora debe ser accesible desde el cliente Teams.

### <a name="run-your-app-in-teams"></a>Ejecute la aplicación en Teams

Requisitos previos: [habilite Teams modo de vista previa del desarrollador](https://aka.ms/teams-toolkit-enable-devpreview)

1. Vaya a la barra de actividades en el lado izquierdo de la ventana de Visual Studio Code.
1. Seleccione el icono **Ejecutar** para mostrar la vista **Ejecutar y depurar.**
1. También puede utilizar el método abreviado de `Ctrl+Shift+D` teclado.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Mantener y apoyar la aplicación publicada](../concepts/deploy-and-publish/appsource/post-publish/overview.md)

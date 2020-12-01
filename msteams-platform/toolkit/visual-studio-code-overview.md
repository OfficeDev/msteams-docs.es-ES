---
title: Compilar aplicaciones con el kit de herramientas de Microsoft Teams y Visual Studio Code
description: Introducción a la creación de excelentes aplicaciones personalizadas directamente en Visual Studio Code con el kit de herramientas de Microsoft Teams
keywords: Teams Visual Studio Code Toolkit
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 41b0eeaeef1c7094fc9c8cbdc05c2db899245fc6
ms.sourcegitcommit: 7e47bf158249050c36d97509eea00e77089a54e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/30/2020
ms.locfileid: "49476933"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>Compilar aplicaciones con el kit de herramientas de Microsoft Teams y Visual Studio Code

El kit de herramientas de Microsoft Teams le permite crear aplicaciones de Team personalizadas directamente en el entorno de Visual Studio Code. El kit de herramientas le guiará por el proceso y le proporciona todo lo que necesita para crear, depurar e iniciar la aplicación de Microsoft Teams.

## <a name="installing-the-teams-toolkit"></a>Instalación de Team Toolkit

El kit de herramientas de Microsoft Teams para Visual Studio Code está disponible para su descarga desde [Visual Studio Marketplace](https://aka.ms/teams-toolkit) o directamente como una extensión de Visual Studio Code.

> [!TIP]
> Después de la instalación, debería ver Team Toolkit en la barra de actividad del código de Visual Studio. Si no es así, haga clic con el botón derecho en la barra de actividad y seleccione **Microsoft Teams** para anclar el kit de herramientas para facilitar el acceso.

## <a name="using-the-toolkit"></a>Uso del kit de herramientas

- [Configurar un nuevo proyecto](#set-up-a-new-teams-project)
- [Importar un proyecto existente](#import-an-existing-teams-app-project)
- [Configurar la aplicación](#configure-your-app)
- [Empaquetar la aplicación](#package-your-app)
- [Ejecutar la aplicación de forma local o en Microsoft Teams](#run-your-app)

## <a name="set-up-a-new-teams-project"></a>Configurar un nuevo proyecto de Teams

1. Cree un área de trabajo o una carpeta para el proyecto en su entorno local.
1. En Visual Studio Code, seleccione el icono de Teams ![Icono de Teams](../assets/icons/favicon-16x16.png) en la barra de actividades del lado izquierdo de la ventana.
1. Seleccione **Abrir Microsoft Teams Toolkit** desde el menú de comandos.
1. Seleccione **crear una nueva aplicación de Teams** desde el menú de comandos.
1. Cuando se le solicite, escriba el nombre del área de trabajo. Se usará como el nombre de la carpeta en la que residirá el proyecto y el nombre predeterminado de la aplicación.
1. Presione **entrar** para que llegue a la pantalla **Agregar funcionalidad** , configure las propiedades de la nueva aplicación.
1. Seleccione el botón **Finalizar** para completar el proceso de configuración.

## <a name="import-an-existing-teams-app-project"></a>Importar un proyecto de aplicación de Teams existente

1. En Visual Studio Code, seleccione el icono de Teams ![Icono de Teams](../assets/icons/favicon-16x16.png) en la barra de actividades del lado izquierdo de la ventana.
1. Seleccione **importar paquete de aplicaciones** en el menú comando.
1. Elija el archivo zip del paquete de aplicaciones de Microsoft [Teams](../concepts/build-and-test/apps-package.md) existente.
1. Elija el botón **seleccionar paquete de publicación** . La pestaña de configuración del kit de herramientas ahora debe rellenarse con los detalles de la aplicación.
1. En Visual Studio Code, seleccione **archivo**  ->  **Agregar carpeta al área de trabajo** para agregar el directorio de código fuente al área de trabajo de Visual Studio Code.

## <a name="configure-your-app"></a>Configurar la aplicación

En esencia, la aplicación de Microsoft Teams adopta tres componentes:

  1. El cliente de Microsoft Teams (Web, escritorio o móvil) donde los usuarios interactúan con la aplicación.
  1. Un servidor que responde a las solicitudes de contenido que se mostrarán en Microsoft Teams, por ejemplo, contenido de la ficha HTML o una tarjeta adaptable de bot.
  1. Un paquete de la [aplicación](/concepts/build-and-test/apps-package.md) teams que consta de tres archivos:

  > [!div class="checklist"]
  >
  > - La manifest.jsen 
  > - Un [icono de color](../resources/schema/manifest-schema.md#icons) de la aplicación para que se muestre en el catálogo de aplicaciones públicas o de la organización
 > - Un [icono de esquema](../resources/schema/manifest-schema.md#icons) para mostrar en la barra de actividad de Microsoft Teams.

Cuando se instala una aplicación, el cliente de Microsoft Teams analiza el archivo de manifiesto para determinar la información necesaria, como el nombre de la aplicación y la dirección URL en la que se encuentran los servicios.

1. Para configurar la aplicación, navegue a la pestaña **Microsoft Team Toolkit** en Visual Studio Code.
1. Seleccione **Editar paquete** de la aplicación para ver la página de detalles de la **aplicación** .
1. Al editar los campos en la página de detalles de la aplicación, se actualiza el contenido del manifest.jsen el archivo que se entregará como parte del paquete de la aplicación. *Consulte* [Editor de manifiesto de App Studio](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>Empaquetar la aplicación

Al modificar la página de detalles de la **aplicación** o actualizar el **manifiesto**, o los archivos **. env** en la carpeta  **. Publish** de la aplicación, se generará automáticamente el archivo de **Development.zip** . Deberá incluir [dos iconos](../concepts/build-and-test/apps-package.md#icons) en la misma carpeta.

## <a name="run-your-app"></a>Ejecutar la aplicación

### <a name="install-and-run-your-app-locally"></a>Instalar y ejecutar la aplicación de forma local

Para obtener instrucciones detalladas sobre cómo empaquetar y probar la aplicación, consulte la página de inicio *y ejecutar* contenido en la Página principal del proyecto. En general, debe instalar el servidor de la aplicación, ponerlo en ejecución y, a continuación, configurar una solución de tunelización para que Microsoft Teams pueda obtener acceso al contenido que se ejecuta desde localhost.

### <a name="enable-development-from-localhost"></a>Habilitar el desarrollo desde localhost

Si desea depurar la aplicación basada en pestañas en localhost mediante HTTPS, tendrá que decirle al explorador que confíe en la aplicación a la que se atiende <https://localhost> . Vaya a <https://localhost:3000/tab>. Si ve una advertencia que indica que el sitio no es de confianza, elija la opción para continuar de todos modos. La aplicación ahora debería ser accesible desde el cliente de Microsoft Teams.

### <a name="run-your-app-in-teams"></a>Ejecutar la aplicación en Microsoft Teams

Requisitos previos: [Habilitar el modo de vista previa para desarrolladores de Teams](https://aka.ms/teams-toolkit-enable-devpreview)

1. Navegue a la barra de actividades en el lado izquierdo de la ventana de Visual Studio Code.
1. Seleccione el icono **Ejecutar** para mostrar la vista **Ejecutar y depurar** .
1. También puede usar el método abreviado de teclado `Ctrl+Shift+D` .

> [!div class="nextstepaction"]
> [Siguiente paso: mantenimiento y soporte de la aplicación publicada](../concepts/deploy-and-publish/appsource/post-publish/overview.md)

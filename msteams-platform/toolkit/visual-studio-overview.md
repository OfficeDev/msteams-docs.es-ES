---
title: Crear aplicaciones con Microsoft Teams Toolkit y Visual Studio
description: Introducción a la creación de excelentes aplicaciones personalizadas directamente Visual Studio con Microsoft Teams Toolkit
keywords: Kit de herramientas de Teams visual studio
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 08df1d3907a1a3683eb42222e247cd7fd6c0177b
ms.sourcegitcommit: 5e1300d6f4f2ea23beb3cdbbf4bd46999eef4e87
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/15/2021
ms.locfileid: "49875010"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a>Crear aplicaciones con Teams Toolkit y Visual Studio

Microsoft Teams Toolkit le permite crear aplicaciones personalizadas de Teams directamente en el Visual Studio de desarrollo integrado (IDE). El kit de herramientas de Microsoft Teams le guiará a través del proceso y le proporciona todo lo que necesita para crear, depurar e iniciar su aplicación de Teams.

## <a name="prerequisites"></a>Requisitos previos

1. [Habilitar la vista previa del desarrollador](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. Asegúrese de que el **<span>ASP.NE</span>T** y el módulo de desarrollo web se hayan agregado a la Visual Studio web. Puede comprobar si sigue los pasos de la página Modificar Visual Studio agregando o quitando cargas [de trabajo y documentación de](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) componentes.

![módulo de asp.net visual studio](../assets/images/visual-studio-web-dev-module.png)

3. Si desea probar la aplicación implementando la aplicación desde Visual Studio, necesitará tener IIS (Internet Information Services) instalado en el entorno de desarrollo. Visual Studio no incluye IIS y no se incluye en la configuración predeterminada de Windows 10, Windows 8 o Windows 7; sin embargo, puede descargar la versión más reciente del Centro [de descarga de Microsoft.](https://www.microsoft.com/download/details.aspx?id=48264)

![Vista de página de descarga de IIS](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a>Instalación del kit de herramientas de Teams

Microsoft Teams Toolkit for Visual Studio está disponible para su descarga desde Visual Studio  [Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) o directamente desde el menú Extensiones dentro de Visual Studio.

## <a name="using-the-toolkit"></a>Uso del kit de herramientas

- [Configurar un nuevo proyecto](#set-up-a-new-teams-project)
- [Configurar la aplicación](#configure-your-app)
- [Empaquetar la aplicación](#package-your-app)
- [Ejecutar la aplicación en Teams](#install-and-run-your-app-locally)
- [Valide su aplicación](#validate-your-app)
- [Publicar la aplicación](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>Configurar un nuevo proyecto de Teams

1. Seleccione **Crear un nuevo proyecto.**
1. Elija **La aplicación de Microsoft Teams** y seleccione **Siguiente.**
1. Llegará a la pantalla **Configurar el** nuevo proyecto, donde puede elegir el nombre del **proyecto,** la ubicación y el nombre de **la solución.**
1. Active la casilla con la etiqueta **Colocar solución y proyecto en el mismo directorio.**
1. Una ventana emergente con la etiqueta **Agregar funcionalidades** le permitirá elegir una o más funcionalidades para la configuración del proyecto.
1. Seleccione el **botón** Siguiente para completar el proceso de configuración.
1. Una ventana emergente con la etiqueta **Agregar funcionalidades** te permitirá elegir las propiedades de cada funcionalidad seleccionada.
1. Seleccione **Finalizar y** llegará a la página de aterrizaje de Microsoft Teams **Toolkit.**

## <a name="configure-your-app"></a>Configurar la aplicación

En esencia, la aplicación teams abarca tres componentes:

  1. El cliente de Microsoft Teams (web, de escritorio o móvil) en el que los usuarios interactúan con la aplicación.
  1. Un servidor que responde a las solicitudes de contenido que se mostrarán en Teams, por ejemplo, contenido de pestaña HTML o una tarjeta adaptable de bot.
  1. Un paquete [de aplicación de](/concepts/build-and-test/apps-package.md) Teams que consta de tres archivos:

  > [!div class="checklist"]
  >
  > - El manifest.jsen
  > - Un [icono de color](../resources/schema/manifest-schema.md#icons) para que la aplicación se muestre en el catálogo de aplicaciones público u organización
 > - Un [icono de esquema para](../resources/schema/manifest-schema.md#icons) mostrar en la barra de actividades de Teams.

Cuando se instala una aplicación, el cliente de Teams analiza el archivo de manifiesto para determinar la información necesaria, como el nombre de la aplicación y la dirección URL donde se encuentran los servicios.

> [!NOTE]
>Si aún no lo ha hecho, tendrá que iniciar sesión en su cuenta o microsoft 365 para continuar con el proceso de desarrollo.
>
> Si no tiene una cuenta de Microsoft 365, puede registrarse para obtener una suscripción al Programa de desarrolladores de [Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program) Es gratuito *durante* 90 días y se renovará continuamente siempre que lo use para la actividad de desarrollo. Si tiene una suscripción a Visual Studio *Enterprise* o *Professional,* ambos programas incluyen una suscripción gratuita de desarrollador de Microsoft 365, activa durante el período de vida de su Visual Studio suscripción. [](https://aka.ms/MyVisualStudioBenefits) *Consulte* [Configurar una suscripción de desarrollador de Microsoft 365.](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)
>

### <a name="configuration-steps"></a>Pasos de la configuración 

1. Para configurar la aplicación, en la página de aterrizaje del Kit de herramientas de **Microsoft Teams,** seleccione **Editar paquete de la aplicación.**
1. En el **menú desplegable Mis entornos,** seleccione **desarrollo.**
1. Llegarás a la página de **detalles de la** aplicación, donde puedes editar los campos de propiedad de la aplicación.
1. La edición de los campos de la página de detalles de la aplicación actualiza el contenido del archivo manifest.json que, en última instancia, se enviará como parte del paquete de la aplicación. [Más información](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>Empaquetar la aplicación

La modificación de la **página** de detalles de la aplicación o la actualización del **manifiesto,** o los archivos **.env** de la carpeta  **.publish** de la aplicación generarán automáticamente el **archivoDevelopment.zip** aplicación. El Development.zip archivo incluye tres archivos obligatorios: **elmanifest.jsy** dos [iconos.](../concepts/build-and-test/apps-package.md#app-icons)

## <a name="install-and-run-your-app-locally"></a>Instalar y ejecutar la aplicación localmente

1. En el **menú desplegable Configuraciones de** soluciones, seleccione **Implementar**.

![Menú de configuraciones de soluciones](../assets/images/solution-configurations.png)

2. Seleccione el **botón IIS Express + Teams.**

1. Teams se iniciará y el cuadro de diálogo de instalación de la aplicación debe aparecer en el cliente de Teams.

## <a name="validate-your-app"></a>Valide su aplicación

La **página** Validar te permite comprobar el paquete de la aplicación antes de enviar la aplicación a AppSource. Simplemente cargue el paquete de manifiesto y la herramienta de validación comprobará la aplicación en todos los casos de prueba relacionados con el manifiesto. Para cada prueba con errores, la descripción proporciona un vínculo de documentación que le ayudará a solucionar el error. Para las pruebas difíciles de automatizar, la lista de comprobación **preliminar** detalla 7 de los casos de prueba con errores más comunes, así como un vínculo a una lista de comprobación de envío completa.

## <a name="publish-your-app-to-teams"></a>Publicar la aplicación en Teams

✔ En la página principal del proyecto, puede cargar la aplicación en un equipo, enviar la aplicación a la tienda de aplicaciones personalizada de su empresa para los usuarios de su organización o enviar la aplicación al origen de la aplicación para todos los usuarios de Teams.

✔ el administrador de TI revisará estos envíos.

✔ puedes volver a la  página Publicar para comprobar el estado del envío y saber si el administrador de TI aprobó o rechazó la aplicación. Aquí también es donde podrás enviar actualizaciones a tu aplicación o cancelar los envíos actualmente activos.

> [!div class="nextstepaction"]
> [Siguiente paso: Mantener y dar soporte técnico a la aplicación publicada](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>

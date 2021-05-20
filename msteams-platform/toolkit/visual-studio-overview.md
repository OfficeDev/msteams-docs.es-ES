---
title: Cree aplicaciones con el Microsoft Teams Toolkit y el Visual Studio
description: Comience a crear grandes aplicaciones personalizadas directamente dentro de Visual Studio con el Microsoft Teams Toolkit
keywords: equipo de herramientas de estudio visual
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: eb94a8de0355283344ebe890a6fa3a3050e243ea
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566554"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a>Cree aplicaciones con el Teams Toolkit y Visual Studio

El kit de herramientas de Microsoft Teams le permite crear aplicaciones personalizadas de Teams directamente desde el entorno de desarrollo integrado (IDE) de Visual Studio. El kit de herramientas de Microsoft Teams le orienta en el proceso y le ofrece todo lo que necesita para crear, depurar e iniciar su aplicación de Teams.

## <a name="prerequisites"></a>Requisitos previos

1. [Habilite la vista previa del desarrollador.](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. Asegúrese de que el **<span>módulo de</span>desarrollo web y T de ASP.NE** se ha agregado a la instancia de Visual Studio. Puede comprobar siguiendo los pasos descritos en la [Visual Studio Modificar agregando o quitando cargas de trabajo y](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentación de componentes.

![módulo de asp.net de estudio visual](../assets/images/visual-studio-web-dev-module.png)

3. Si desea probar la aplicación implementándola desde Visual Studio, deberá tener IIS (Internet Information Services) instalado en el entorno de desarrollo. Visual Studio no incluye IIS y no se incluye en la configuración predeterminada de Windows 10, Windows 8 o Windows 7; sin embargo, puede descargar la última versión desde el Centro de [descarga de Microsoft.](https://www.microsoft.com/download/details.aspx?id=48264)

![Vista de página de descarga de IIS](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a>Instale la Teams Toolkit

El Microsoft Teams Toolkit para Visual Studio está disponible para su descarga desde [el Marketplace de Visual Studio](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) o directamente desde el menú **Extensiones** dentro de Visual Studio.

## <a name="using-the-toolkit"></a>Uso del kit de herramientas

- [Establecer un nuevo proyecto](#set-up-a-new-teams-project)
- [Configurar la aplicación](#configure-your-app)
- [Empaqueta tu aplicación](#package-your-app)
- [Ejecute la aplicación en Teams](#install-and-run-your-app-locally)
- [Valide su aplicación](#validate-your-app)
- [Publicar la aplicación](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>Establecer un nuevo proyecto de Teams

1. Seleccione **Crear un nuevo proyecto**.
1. Elija **Microsoft Teams App** y seleccione **Siguiente**.
1. Llegará a la pantalla **Configurar el nuevo proyecto** donde puede elegir el nombre **Project,** **ubicación** y nombre de **la solución.**
1. Marque la casilla con la etiqueta **Colocar solución y proyecto en el mismo directorio**.
1. Una ventana emergente con la etiqueta **Agregar capacidades** le permitirá elegir una o varias capacidades para la configuración del proyecto.
1. Seleccione el botón **Siguiente** para completar el proceso de configuración.
1. Una ventana emergente con la etiqueta **Agregar capacidades** le permitirá elegir las propiedades para cada capacidad seleccionada.
1. Seleccione **Finalizar** y aterrizará en la página de destino **Microsoft Teams Toolkit.**

## <a name="configure-your-app"></a>Configurar la aplicación

En esencia, la aplicación Teams abarca tres componentes:

  1. El cliente Microsoft Teams (web, de escritorio o móvil) donde los usuarios interactúan con la aplicación.
  1. Un servidor que responde a las solicitudes de contenido que se mostrarán en Teams, por ejemplo, contenido de la pestaña HTML o una tarjeta adaptable a bots.
  1. Un paquete de Teams aplicación consta de tres archivos:

      > [!div class="checklist"]
      >
      > - El manifest.js
      > - Un [icono de color](../resources/schema/manifest-schema.md#icons) para que la aplicación se muestre en el catálogo de aplicaciones públicas u organizativas
      > - Icono [de contorno](../resources/schema/manifest-schema.md#icons) para mostrar en la barra de actividades Teams.

Cuando se instala una aplicación, el cliente Teams analiza el archivo de manifiesto para determinar la información necesaria, como el nombre de la aplicación y la dirección URL donde se encuentran los servicios.

> [!NOTE]
>Si aún no lo ha hecho, deberá iniciar sesión en su Microsoft 365 o cuenta para continuar con el proceso de desarrollo.
>
> Si no tiene una cuenta Microsoft 365, puede registrarse para obtener una [suscripción Microsoft 365 Programa para desarrolladores.](https://developer.microsoft.com/microsoft-365/dev-program) Es *gratis* durante 90 días y se renovará continuamente siempre y cuando lo esté utilizando para la actividad de desarrollo. Si tienes una suscripción *Visual Studio Enterprise* o *Professional,* ambos programas incluyen una suscripción gratuita Microsoft 365 [para desarrolladores,](https://aka.ms/MyVisualStudioBenefits)activa durante toda la vida de tu suscripción Visual Studio. Para obtener más información, consulte [Configurar una suscripción Microsoft 365 desarrollador.](/office/developer-program/office-365-developer-program-get-started)
>

### <a name="configuration-steps"></a>Pasos de la configuración 

1. Para configurar la aplicación, en la página de destino **Microsoft Teams Toolkit,** seleccione **Editar paquete de aplicación**.
1. En el menú desplegable **Mis entornos,** seleccione **desarrollo.**
1. Aterrizarás en la página **detalles de** la aplicación donde puedes editar los campos de propiedades de la aplicación.
1. La edición de los campos de la página Detalles de la aplicación actualiza el contenido de la manifest.jsen el archivo que, en última instancia, se enviará como parte del paquete de la aplicación. [Más información](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>Empaqueta tu aplicación

La modificación de la página **de detalles** de la aplicación o la actualización de los archivos **de manifiesto** o **.env** en la carpeta **.publish** de la aplicación generará automáticamente el archivo **Development.zip.** El archivo Development.zip incluye tres archivos necesarios: el **manifest.jsactivado** y [dos iconos.](../concepts/build-and-test/apps-package.md#app-icons)

## <a name="install-and-run-your-app-locally"></a>Instale y ejecute la aplicación localmente

1. En el menú desplegable **Configuraciones de soluciones,** seleccione **Implementar** como se muestra en la siguiente imagen:

    ![Menú de configuraciones de soluciones](../assets/images/solution-configurations.png)

2. Seleccione el botón **IIS Express + Teams.**

1. Teams se iniciará y el diálogo de instalación de la aplicación debe aparecer en el cliente Teams.

## <a name="validate-your-app"></a>Valide su aplicación

La página **Validar** le permite comprobar el paquete de la aplicación antes de enviar la aplicación a AppSource. Simplemente cargue el paquete de manifiesto y la herramienta de validación comprobará su aplicación en todos los casos de prueba relacionados con el manifiesto. Para cada prueba con errores, la descripción proporciona un vínculo de documentación para ayudarle a corregir el error. Para las pruebas que son difíciles de automatizar, la **lista de comprobación preliminar** detalla 7 de los casos de prueba fallidos más comunes, así como el enlace a una lista de comprobación de envío completa.

## <a name="publish-your-app-to-teams"></a>Publicar la aplicación en Teams

✔ En la página principal del proyecto, puede cargar la aplicación en un equipo, enviar la aplicación a la tienda de aplicaciones personalizadas de su empresa para los usuarios de su organización o enviar la aplicación al origen de la aplicación para todos los usuarios Teams.

✔ su administrador de TI revisará estos envíos.

✔ Puede volver a la página **Publicar** para comprobar el estado de envío y obtener información sobre si la aplicación fue aprobada o rechazada por el administrador de TI. Aquí es también donde vendrás a enviar actualizaciones a tu aplicación o cancelar cualquier envío activo actualmente.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Mantener y apoyar la aplicación publicada](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>

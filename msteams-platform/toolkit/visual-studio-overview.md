---
title: Crear aplicaciones con el Microsoft Teams Toolkit y Visual Studio
description: Introducción a la creación de excelentes aplicaciones personalizadas directamente Visual Studio con el Microsoft Teams Toolkit
keywords: Kit de herramientas de visual studio de teams
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
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a>Crear aplicaciones con el Teams Toolkit y Visual Studio

El kit de herramientas de Microsoft Teams le permite crear aplicaciones personalizadas de Teams directamente desde el entorno de desarrollo integrado (IDE) de Visual Studio. El kit de herramientas de Microsoft Teams le orienta en el proceso y le ofrece todo lo que necesita para crear, depurar e iniciar su aplicación de Teams.

## <a name="prerequisites"></a>Requisitos previos

1. [Habilitar la vista previa del desarrollador](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).

1. Asegúrese de que el **<span>ASP.NE</span>T y el** módulo de desarrollo web se han agregado a la instancia Visual Studio web. Puede comprobar si sigue los pasos de la página [Modificar Visual Studio agregando o](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) quitando cargas de trabajo y documentación de componentes.

![módulo de asp.net visual studio](../assets/images/visual-studio-web-dev-module.png)

3. Si quieres probar la aplicación implementandola desde Visual Studio, tendrás que tener IIS (Internet Information Services) instalado en el entorno de desarrollo. Visual Studio no incluye IIS y no se incluye en la configuración Windows 10, Windows 8 o Windows 7; sin embargo, puede descargar la versión más reciente del Centro [de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=48264).

![Vista de página de descarga de IIS](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a>Instale el Teams Toolkit

El Microsoft Teams Toolkit para Visual Studio está disponible para su descarga desde [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) o directamente desde el menú **Extensiones** de Visual Studio.

## <a name="using-the-toolkit"></a>Uso del kit de herramientas

- [Configurar un nuevo proyecto](#set-up-a-new-teams-project)
- [Configurar la aplicación](#configure-your-app)
- [Empaquetar la aplicación](#package-your-app)
- [Ejecute la aplicación en Teams](#install-and-run-your-app-locally)
- [Valide su aplicación](#validate-your-app)
- [Publicar la aplicación](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>Configurar un nuevo proyecto Teams proyecto

1. Seleccione **Crear un nuevo proyecto**.
1. Elija **Microsoft Teams app y** seleccione **Siguiente**.
1. Llegará a la pantalla **Configurar el** nuevo proyecto, donde puede elegir el nombre Project **,** **Ubicación** y Nombre de **la solución**.
1. Active la casilla Colocar solución **y proyecto en el mismo directorio**.
1. Una ventana emergente con la etiqueta **Agregar funcionalidades** le permitirá elegir una o más funciones para la configuración del proyecto.
1. Seleccione el **botón** Siguiente para completar el proceso de configuración.
1. Una ventana emergente con la etiqueta **Agregar funcionalidades** te permitirá elegir las propiedades de cada funcionalidad seleccionada.
1. Selecciona **Finalizar** y llegarás a la **Microsoft Teams Toolkit** de aterrizaje.

## <a name="configure-your-app"></a>Configurar la aplicación

En su núcleo, la aplicación Teams abarca tres componentes:

  1. El Microsoft Teams (web, de escritorio o móvil) donde los usuarios interactúan con la aplicación.
  1. Un servidor que responde a solicitudes de contenido que se mostrarán en Teams, por ejemplo, contenido de pestaña HTML o una tarjeta adaptable de bot .
  1. Un Teams de la aplicación consta de tres archivos:

      > [!div class="checklist"]
      >
      > - El manifest.jsen
      > - Icono [de color para](../resources/schema/manifest-schema.md#icons) que la aplicación se muestre en el catálogo de aplicaciones públicas u de la organización
      > - Icono [de esquema para](../resources/schema/manifest-schema.md#icons) mostrar en la barra Teams actividad.

Cuando se instala una aplicación, el cliente Teams analiza el archivo de manifiesto para determinar la información necesaria, como el nombre de la aplicación y la dirección URL donde se encuentran los servicios.

> [!NOTE]
>Si aún no lo ha hecho, tendrá que iniciar sesión en su cuenta o Microsoft 365 para continuar con el proceso de desarrollo.
>
> Si no tienes una cuenta Microsoft 365, puedes suscribirte a una suscripción Microsoft 365 [Developer Program.](https://developer.microsoft.com/microsoft-365/dev-program) Es gratuito *durante* 90 días y se renovará continuamente siempre que lo use para la actividad de desarrollo. Si tiene una suscripción Visual Studio *Enterprise* o *Professional,* ambos programas incluyen una suscripción Microsoft 365 desarrollador [gratuita,](https://aka.ms/MyVisualStudioBenefits)activa durante la vida de su Visual Studio suscripción. Para obtener más información, vea [Set up a Microsoft 365 developer subscription](/office/developer-program/office-365-developer-program-get-started).
>

### <a name="configuration-steps"></a>Pasos de la configuración 

1. Para configurar la aplicación, en la **Microsoft Teams Toolkit** de aterrizaje, seleccione **Editar paquete de la aplicación**.
1. En el menú desplegable Mis **entornos,** seleccione **desarrollo**.
1. Llegarás a la página de detalles **de la aplicación** donde puedes editar los campos de propiedad de la aplicación.
1. La edición de los campos de la página detalles de la aplicación actualiza el contenido del archivo manifest.jsen que, en última instancia, se enviará como parte del paquete de la aplicación. [Más información](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>Empaquetar la aplicación

Al modificar la página de **detalles de** la aplicación o actualizar el manifiesto **o** los archivos **.env** de la carpeta  **.publish** de la aplicación, se generará automáticamente el **Development.zip** archivo. El Development.zip incluye tres archivos necesarios: **elmanifest.jsy** dos [iconos.](../concepts/build-and-test/apps-package.md#app-icons)

## <a name="install-and-run-your-app-locally"></a>Instalar y ejecutar la aplicación localmente

1. En el **menú desplegable Configuraciones de solución,** seleccione **Implementar** como se muestra en la siguiente imagen:

    ![Menú Configuraciones de solución](../assets/images/solution-configurations.png)

2. Seleccione el **IIS Express + Teams** botón.

1. Teams se iniciará y el diálogo de instalación de la aplicación debe aparecer en el Teams cliente.

## <a name="validate-your-app"></a>Valide su aplicación

La **página Validar** te permite comprobar el paquete de la aplicación antes de enviar la aplicación a AppSource. Simplemente cargue el paquete de manifiesto y la herramienta de validación comprobará la aplicación en todos los casos de prueba relacionados con el manifiesto. Para cada prueba con errores, la descripción proporciona un vínculo de documentación que le ayudará a corregir el error. Para las pruebas difíciles de automatizar, la lista de comprobación **preliminar** detalla 7 de los casos de prueba con errores más comunes, así como un vínculo a una lista de comprobación de envío completa.

## <a name="publish-your-app-to-teams"></a>Publicar la aplicación en Teams

✔ En la página principal del proyecto, puedes cargar la aplicación en un equipo, enviar la aplicación a la tienda de aplicaciones personalizada de la empresa para los usuarios de tu organización o enviar la aplicación a App Source para todos los Teams usuarios.

✔ El administrador de TI revisará estos envíos.

✔ Puedes volver a la  página Publicar para comprobar el estado del envío y saber si tu administrador de TI aprobó o rechazó la aplicación. Aquí es también donde llegarás a enviar actualizaciones a tu aplicación o cancelar cualquier envío activo actualmente.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Mantenimiento y soporte técnico de la aplicación publicada](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>

---
title: Crear aplicaciones con el Teams Toolkit y Visual Studio
description: Introducción a la creación de excelentes aplicaciones personalizadas directamente Visual Studio con el Microsoft Teams Toolkit
keywords: Kit de herramientas de visual studio de teams
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 996037f5bb1caaa2493e1eebe51039724822fef9
ms.sourcegitcommit: 9f499908437655d6ebdc6c4b3c3603ee220315b7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2021
ms.locfileid: "52949719"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a>Crear aplicaciones con el Teams Toolkit y Visual Studio

El kit de herramientas de Microsoft Teams le permite crear aplicaciones personalizadas de Teams directamente desde el entorno de desarrollo integrado (IDE) de Visual Studio. El kit de herramientas de Microsoft Teams le orienta en el proceso y le ofrece todo lo que necesita para crear, depurar e iniciar su aplicación de Teams.

## <a name="prerequisites"></a>Requisitos previos

1. [Habilitar la vista previa del desarrollador](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).

1. Asegúrese de que el **<span>ASP.NE</span>T y el** módulo de desarrollo web se han agregado a la instancia Visual Studio web. Puede comprobar si sigue los pasos de la Visual Studio [agregando o](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) quitando cargas de trabajo y documentación de componentes.

![Módulo de asp.net Visual studio](../assets/images/visual-studio-web-dev-module.png)

3. Si quieres probar la aplicación implementandola desde Visual Studio, debes tener Servicios de Internet Information Server (IIS)) instalado en el entorno de desarrollo. Visual Studio no incluye IIS y no se incluye en la configuración predeterminada Windows 10, Windows 8 o Windows 7; sin embargo, puede descargar la versión más reciente del Centro [de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=48264).

![Vista de página de descarga de IIS](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a>Instale el Teams Toolkit

El Microsoft Teams Toolkit para Visual Studio está disponible para su descarga desde [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) o directamente desde el menú **Extensiones** de Visual Studio. Desde el Visual Studio Marketplace también descargar [Teams Toolkit para Visual Studio 2019](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit).

## <a name="using-the-toolkit"></a>Uso del kit de herramientas

- [Configurar un nuevo proyecto](#set-up-a-new-teams-project)
- [Configurar la aplicación](#configure-your-app)
- [Empaquetar la aplicación](#package-your-app)
- [Instalar y ejecutar la aplicación en Teams](#install-and-run-your-app-locally)
- [Valide su aplicación](#validate-your-app)
- [Publicar la aplicación](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>Configurar un nuevo proyecto Teams proyecto

![Teams kit de herramientas instalado](../assets/images/teamstoolkiticon.png)

1. Seleccione **Crear nuevo proyecto**.

    ![Crear un nuevo proyecto](../assets/images/createnewproject.png)

1. Elija la herramienta de inicio rápido **para Microsoft Teams app** y seleccione **Siguiente**.
1. En la **página Configurar el nuevo** proyecto, escriba el nombre **Project**, **Ubicación** y Nombre de **la solución**.
1. Active la **casilla Colocar solución y proyecto en el mismo directorio.**
1. En la ventana emergente Agregar **capacidades,** elija una o más funciones para la configuración del proyecto.
1. Seleccione el **botón** Siguiente para completar el proceso de configuración.
1. En la **ventana** emergente Agregar capacidades, elija las propiedades de cada funcionalidad seleccionada.
1. Seleccione **Finalizar**. Se **muestra Microsoft Teams Toolkit** página de aterrizaje.

    ![Teams de aterrizaje del kit de herramientas](../assets/images/Teamstoolkitpage.png)

## <a name="configure-your-app"></a>Configurar la aplicación

En su núcleo, la aplicación Teams abarca tres componentes:

  1. El Microsoft Teams web, de escritorio o móvil, donde los usuarios interactúan con la aplicación.
  1. Un servidor que responde a solicitudes de contenido que se muestra en Teams, por ejemplo, contenido de pestaña HTML o una tarjeta adaptable de bot.
  1. Un Teams de la aplicación consta de tres archivos:

      - El manifest.jsen
      - Icono [de color para](../resources/schema/manifest-schema.md#icons) que la aplicación se muestre en el catálogo de aplicaciones públicas u de la organización.
      - Icono [de esquema para](../resources/schema/manifest-schema.md#icons) mostrar en la barra Teams actividad.

Cuando se instala una aplicación, el cliente Teams analiza el archivo de manifiesto para determinar la información necesaria, como el nombre de la aplicación y la dirección URL donde se encuentran los servicios.

> [!NOTE]
>Si aún no lo ha hecho, debe iniciar sesión en su cuenta de Microsoft 365 para continuar con el proceso de desarrollo.
>
> Si no tiene una cuenta Microsoft 365, puede registrarse para una suscripción Microsoft 365 [Programa para desarrolladores.](https://developer.microsoft.com/microsoft-365/dev-program) Es gratuito durante 90 días y se renueva siempre que lo use para la actividad de desarrollo. Si tiene una suscripción Visual Studio Enterprise o Professional, ambos programas incluyen una suscripción Microsoft 365 desarrollador [gratuita,](https://aka.ms/MyVisualStudioBenefits)activa durante la vida de su Visual Studio suscripción. Para obtener más información, vea [Configurar una Microsoft 365 de desarrollador](/office/developer-program/office-365-developer-program-get-started).

### <a name="configuration-steps"></a>Pasos de la configuración 

1. Para configurar la aplicación, en la **Microsoft Teams Toolkit** de aterrizaje, seleccione **Editar paquete de la aplicación**.
1. En el menú desplegable Mis **entornos,** seleccione **desarrollo**.
1. En la **página Detalles de** la aplicación, edite los campos de propiedad de la aplicación.
    
    La edición de los campos de la página detalles de la aplicación actualiza el contenido del archivo manifest.jsque se enviará como parte del paquete de la aplicación. Para obtener más información, [vea Teams Toolkit manifest](https://aka.ms/teams-toolkit-manifest).

## <a name="package-your-app"></a>Empaquetar la aplicación

Al modificar la página de **detalles de** la aplicación o actualizar el manifiesto **o** los archivos **.env** de la carpeta  **.publish** de la aplicación, se generará automáticamente el **Development.zip** archivo. El Development.zip incluye tres archivos obligatorios, el **manifest.jsy** [dos iconos.](../concepts/build-and-test/apps-package.md#app-icons)

## <a name="install-and-run-your-app-locally"></a>Instalar y ejecutar la aplicación localmente

1. En el **menú desplegable Configuraciones de solución,** seleccione **Implementar** como se muestra en la siguiente imagen:

    ![Menú Configuraciones de solución](../assets/images/solution-configurations.png)

1. Seleccione el **IIS Express + Teams** botón.

    El cuadro de diálogo de instalación de la aplicación aparece en el Teams cliente.

## <a name="validate-your-app"></a>Valide su aplicación

La **página Validar** te permite comprobar el paquete de la aplicación antes de enviar la aplicación a AppSource. Simplemente cargue el paquete de manifiesto y la herramienta de validación comprobará la aplicación en todos los casos de prueba relacionados con el manifiesto. Para cada prueba con errores, la descripción proporciona un vínculo de documentación que le ayudará a corregir el error. Para las pruebas difíciles de automatizar, la lista de comprobación **preliminar** detalla 7 de los casos de prueba con errores más comunes, así como un vínculo a una lista de comprobación de envío completa.

## <a name="publish-your-app-to-teams"></a>Publicar la aplicación en Teams

* En la página principal del proyecto, puede cargar la aplicación a un equipo, enviarla a la tienda de aplicaciones personalizada de la organización para los usuarios de su organización o enviarla al origen de la aplicación para todos los usuarios de Teams.

* El administrador de TI revisará estas entregas.

* Puedes volver a la **página Publicar** para comprobar el estado del envío y saber si tu administrador de TI aprobó o rechazó la aplicación. Aquí también puedes enviar actualizaciones a la aplicación o cancelar cualquier envío activo actualmente.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Mantenimiento y soporte técnico de la aplicación publicada](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>

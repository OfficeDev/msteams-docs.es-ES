---
title: Compilar aplicaciones con el kit de herramientas de Microsoft Teams y Visual Studio
description: Introducción a la creación de excelentes aplicaciones personalizadas directamente en Visual Studio con el kit de herramientas de Microsoft Teams
keywords: Teams Visual Studio Toolkit
ms.topic: overview
ms.openlocfilehash: 79ea22cfd154313247132c22684d444c0813c66f
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819206"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio"></a>Compilar aplicaciones con el kit de herramientas de Microsoft Teams y Visual Studio

El kit de herramientas de Microsoft Teams permite crear aplicaciones de Team personalizadas directamente en el entorno de desarrollo integrado (IDE) de Visual Studio. El kit de herramientas de Microsoft Teams le guiará por el proceso y le proporciona todo lo que necesita para crear, depurar e iniciar la aplicación de Teams.

## <a name="prerequisites"></a>Requisitos previos

1. [Habilitar la vista previa para desarrolladores](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. Asegúrese de que ** <span>ASP.ne</span>T y el módulo de desarrollo web** se hayan agregado a la instancia de Visual Studio. Puede comprobarlo siguiendo los pasos descritos en la documentación sobre [Cómo modificar Visual Studio agregando o quitando cargas de trabajo y componentes](/visualstudio/install/modify-visual-studio?view=vs-2019) .

![módulo de Visual Studio asp.net](../assets/images/visual-studio-web-dev-module.png)

3. Si desea probar la aplicación mediante su implementación desde Visual Studio, tendrá que tener instalado IIS (Internet Information Services) en el entorno de desarrollo. Visual Studio no incluye IIS y no se incluye en la configuración predeterminada de Windows 10, Windows 8 o Windows 7; sin embargo, puede descargar la versión más reciente desde el [centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=48264).

![Vista de la página de descarga de IIS](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a>Instalar el kit de herramientas de Teams

El kit de herramientas de Microsoft Teams para Visual Studio está disponible para su descarga desde [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) o directamente desde el menú **extensiones** de Visual Studio.

## <a name="using-the-toolkit"></a>Uso del kit de herramientas

- [Configurar un nuevo proyecto](#set-up-a-new-teams-project)
- [Configurar la aplicación](#configure-your-app)
- [Empaquetar la aplicación](#package-your-app)
- [Ejecutar la aplicación en Microsoft Teams](#install-and-run-your-app-locally)
- [Validar la aplicación](#validate-your-app)
- [Publicar la aplicación](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>Configurar un nuevo proyecto de Teams

1. Seleccione **crear un nuevo proyecto**.
1. Elija **aplicación de Microsoft Teams** y seleccione **siguiente**.
1. Llegará a la pantalla **configurar el nuevo proyecto** , donde podrá elegir el **nombre del proyecto**, la **Ubicación**y el nombre de la **solución**.
1. Active la casilla etiquetar la **solución y el proyecto en el mismo directorio**.
1. Una ventana emergente con la etiqueta **Agregar funciones** le permitirá elegir una o más funcionalidades para la configuración del proyecto.
1. Seleccione el botón **siguiente** para completar el proceso de configuración.
1. Una ventana emergente con la etiqueta **Agregar funciones** le permitirá elegir las propiedades de cada funcionalidad seleccionada.
1. Seleccione **Finalizar** y estará en la página de aterrizaje de **Microsoft Teams Toolkit** .

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

> [!NOTE]
>Si aún no lo ha hecho, tendrá que iniciar sesión en su cuenta de Microsoft 365 o para continuar con el proceso de desarrollo.
>
> Si no tiene una cuenta de 365 de Microsoft, puede registrarse para obtener una suscripción del [programa de desarrolladores de microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program) . Es *gratuita* durante 90 días y se renovará continuamente siempre que la use para la actividad de desarrollo. Si tiene una suscripción de Visual Studio *Enterprise* o *Professional* , ambos programas incluyen una suscripción gratuita al [desarrollador](https://aka.ms/MyVisualStudioBenefits)de Microsoft 365, activa durante la vida de su suscripción a Visual Studio. *Consulte* [configurar una suscripción de desarrollador de Microsoft 365](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).
>

### <a name="configuration-steps"></a>Pasos de la configuración 

1. Para configurar la aplicación, en la página de aterrizaje de **Microsoft Teams Toolkit** , seleccione **Editar paquete** de la aplicación.
1. En el menú desplegable **mis entornos** , seleccione **desarrollo**.
1. Encontrarás en la página de detalles de la **aplicación** donde puedes editar los campos de propiedades de la aplicación.
1. Al editar los campos en la página de detalles de la aplicación, se actualiza el contenido del manifest.jsen el archivo que se entregará como parte del paquete de la aplicación. [Más información](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>Empaquetar la aplicación

Al modificar la página de detalles de la **aplicación** o actualizar el **manifiesto**, o los archivos **. env** en la carpeta  **. Publish** de la aplicación, se generará automáticamente el archivo de **Development.zip** . El archivo de Development.zip incluye tres archivos necesarios: el **manifest.jsen** y [dos archivos de icono](../concepts/build-and-test/apps-package.md#icons).

## <a name="install-and-run-your-app-locally"></a>Instalar y ejecutar la aplicación de forma local

1. En el menú desplegable **configuraciones de soluciones** , seleccione **implementar**.

![Menú Configuraciones de soluciones](../assets/images/solution-configurations.png)

2. Seleccione el botón de **ISS Express + Teams** .

1. Se iniciará Microsoft Teams y el cuadro de diálogo de instalación de la aplicación debería aparecer en el cliente de Microsoft Teams.

## <a name="validate-your-app"></a>Validar la aplicación

La página **validar** permite comprobar el paquete de la aplicación antes de enviar la aplicación a AppSource. Simplemente cargue el paquete del manifiesto y la herramienta de validación comprobará la aplicación en todos los casos de prueba relacionados con el manifiesto. Para cada prueba con errores, la descripción proporciona un vínculo de documentación para ayudarle a corregir el error. Para las pruebas que son difíciles de automatizar, los detalles de la **lista de comprobación preliminar** 7 de los casos de prueba con errores más comunes, así como un vínculo a una lista de comprobación de envío completa.

## <a name="publish-your-app-to-teams"></a>Publicar la aplicación en Teams

✔ En la Página principal de su proyecto, puede cargar la aplicación en un equipo, enviar la aplicación a la tienda de aplicaciones personalizada de la empresa para los usuarios de su organización o bien enviar la aplicación al origen de la aplicación para todos los usuarios de Microsoft Teams.

✔ El administrador de ti consultará estos envíos.

✔ Puede volver a la página **publicar** para comprobar el estado del envío y saber si su administrador de ti aprobó o rechazó la aplicación. Aquí también puede ir a enviar actualizaciones a la aplicación o cancelar los envíos actualmente activos.

> [!div class="nextstepaction"]
> [Siguiente paso: mantenimiento y soporte de la aplicación publicada](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>

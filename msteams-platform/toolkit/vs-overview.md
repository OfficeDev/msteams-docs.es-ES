---
title: Compilar aplicaciones con el kit de herramientas de Microsoft Teams y Visual Studio
description: Introducción a la creación de excelentes aplicaciones personalizadas directamente en Visual Studio con el kit de herramientas de Microsoft Teams
keywords: Teams Visual Studio Toolkit
ms.date: 06/30/2020
ms.openlocfilehash: e5715cf23cfd221b65afe0e6258ce06ff98770aa
ms.sourcegitcommit: 694babb79d379360a20cf928a9d2b88dd6d3bdd0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/07/2020
ms.locfileid: "45051734"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio"></a>Compilar aplicaciones con el kit de herramientas de Microsoft Teams y Visual Studio

El kit de herramientas de Microsoft Teams permite crear aplicaciones de Team personalizadas directamente en el entorno de Visual Studio. El kit de herramientas le guiará por el proceso y le proporciona todo lo que necesita para crear, depurar e iniciar la aplicación de Microsoft Teams.

## <a name="installing-the-teams-toolkit"></a>Instalación de Team Toolkit

El kit de herramientas de Microsoft Teams para Visual Studio está disponible para su descarga desde [Visual Studio Marketplace](https://aka.ms/teams-toolkit) o directamente como una extensión en Visual Studio.

## <a name="using-the-toolkit"></a>Uso del kit de herramientas

- [Configurar un nuevo proyecto](#set-up-a-new-teams-project)
- [Configurar la aplicación](#configure-your-app)
- [Empaquetar la aplicación](#package-your-app)
- [Ejecutar la aplicación en Microsoft Teams](#install-and-run-your-app-locally)
- [Validar la aplicación](#validate-your-app)
- [Publicar la aplicación](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>Configurar un nuevo proyecto de Teams

1. Cree un nuevo proyecto y seleccione la plantilla Microsoft Terams Toolkit.
1. Llegará a la pantalla **Agregar funcionalidad** para configurar las propiedades de la nueva aplicación.
1. Seleccione el botón **Finalizar** para completar el proceso de configuración.

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

1. Para configurar la aplicación, navegue a la ventana de extensiones de **Microsoft Team Toolkit** .
1. Seleccione **Editar paquete** de la aplicación para ver la página de detalles de la **aplicación** .
1. Al editar los campos en la página de detalles de la aplicación, se actualiza el contenido del manifest.jsen el archivo que se entregará como parte del paquete de la aplicación. [Más información](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>Empaquetar la aplicación

La modificación es la página de detalles de la **aplicación** o la actualización del **manifiesto**, o los archivos **. env** en la carpeta **. Publish** de la aplicación generarán automáticamente el archivo de **Development.zip** . Deberá incluir [dos iconos](../concepts/build-and-test/apps-package.md#icons) en la misma carpeta.

## <a name="install-and-run-your-app-locally"></a>Instalar y ejecutar la aplicación de forma local

En el menú desplegable de *configuraciones de soluciones* , seleccione *implementar*. Pulse el botón *ISS Express + Teams* . Se iniciará Microsoft Teams y el cuadro de diálogo de instalación de la aplicación debería aparecer en el cliente de Microsoft Teams.

## <a name="validate-your-app"></a>Validar la aplicación

La página **validar** permite comprobar el paquete de la aplicación antes de enviar la aplicación a AppSource. Simplemente cargue el paquete del manifiesto y la herramienta de validación comprobará la aplicación en todos los casos de prueba relacionados con el manifiesto. Para cada prueba con errores, la descripción proporciona un vínculo de documentación para ayudarle a corregir el error. Para las pruebas que son difíciles de automatizar, los detalles de la **lista de comprobación preliminar** 7 de los casos de prueba con errores más comunes, así como un vínculo a una lista de comprobación de envío completa.

## <a name="publish-your-app-to-teams"></a>Publicar la aplicación en Teams

En la Página principal de su proyecto, puede cargar su aplicación en un equipo, enviar la aplicación a la tienda de aplicaciones personalizada de la empresa para los usuarios de su organización o bien enviar la aplicación al origen de la aplicación para todos los usuarios de Microsoft Teams. El administrador de ti consultará estos envíos. Puede volver a la página *publicar* para comprobar el estado del envío y saber si su administrador de ti aprobó o rechazó la aplicación. Aquí también puede ir a enviar actualizaciones a la aplicación o cancelar los envíos actualmente activos.

> [!div class="nextstepaction"]
> [Siguiente paso: mantenimiento y soporte de la aplicación publicada](../concepts/deploy-and-publish/appsource/post-publish/overview.md)

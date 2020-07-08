---
title: Compilar aplicaciones con el kit de herramientas de Microsoft Teams y Visual Studio Code
description: Introducción a la creación de excelentes aplicaciones personalizadas directamente en Visual Studio Code con el kit de herramientas de Microsoft Teams
keywords: Teams Visual Studio Code Toolkit
ms.date: 06/30/2020
ms.openlocfilehash: 17f21d1656b32074318030b9df9e643200f58f80
ms.sourcegitcommit: ecf7ca8e77e77fe3f4cad1b13e3d31a825155555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/07/2020
ms.locfileid: "45054255"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio-code"></a>Compilar aplicaciones con el kit de herramientas de Microsoft Teams y Visual Studio Code

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
- [Ejecutar la aplicación en Microsoft Teams](#run-your-app-in-teams)
- [Validar la aplicación](#validate-your-app)
- [Publicar la aplicación](#publish-your-app-to-teams)

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
1. Al editar los campos en la página de detalles de la aplicación, se actualiza el contenido del manifest.jsen el archivo que se entregará como parte del paquete de la aplicación. [Más información](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>Empaquetar la aplicación

La modificación es la página de detalles de la **aplicación** o la actualización del **manifiesto**, o los archivos **. env** en la carpeta **. Publish** de la aplicación generarán automáticamente el archivo de **Development.zip** . Deberá incluir [dos iconos](../concepts/build-and-test/apps-package.md#icons) en la misma carpeta.

## <a name="install-and-run-your-app-locally"></a>Instalar y ejecutar la aplicación de forma local

Para obtener instrucciones detalladas sobre cómo empaquetar y probar la aplicación, consulte la página de inicio*y ejecutar* contenido en la Página principal del proyecto. En general, debe instalar el servidor de la aplicación, ponerlo en ejecución y, a continuación, configurar una solución de tunelización para que Microsoft Teams pueda obtener acceso al contenido que se ejecuta desde localhost.

## <a name="add-a-trusted-certificate-for-localhost"></a>Agregar un certificado de confianza para localhost

Si desea depurar la aplicación basada en pestañas en localhost mediante HTTPS, tendrá que agregar un certificado para localhost a `Trusted Root Certification Authorities` Catalog. Solo necesita realizar este paso una vez por máquina.</br></br>

**Cree e instale un certificado de confianza:**
<details>
  <summary>Expandir aquí</summary>

* Compilar y ejecutar la aplicación
  * Siga el instuctions en la sección **generar y ejecutar** del archivo README del proyecto para que se atienda desde https://localhost:3000/tab . Por lo general, esto implicará que se ejecute `npm install``npm start`
  * Navegar https://localhost:3000/tab desde Google Chrome

* Adquirir el certificado SSL:
  * Abra la ventana herramientas de desarrollo de Chrome ( `ctrl + shift + i`  /  `cmd + option + i` ).
  * Haga clic en la `Security` pestaña
  * Haga clic en `View certificate` y tendrá la opción de descargar el certificado, ya sea arrastrándolo al escritorio en OS X, o haciendo clic en la `Details` pestaña de Windows y haciendo clic en`Copy to File…`
  * Asigne al archivo el nombre <*nada*>. cer y guárdelo en una carpeta que no requiera el consentimiento del administrador para realizar una acción de escritura.
  
* Instalar el certificado en **Windows**
  * Elija la `DER encoded binary X.509 (.CER)` opción (la primera) y guárdela.
  * Haga doble clic en el certificado e instálelo.
  * Elección`Local Machine`
  * Anula`Place all certificates in the following store`
  * Elección`Trusted Root Certification Authorities`
  * Confirmar la instalación
  
* Instalar el certificado **Mac OS X**
  * En OS X, abra la utilidad de acceso a llaves y seleccione en `System` el menú de la izquierda. Haga clic en el icono de candado para habilitar los cambios.
  * Haga clic en el botón más cerca de la parte inferior para agregar un certificado nuevo y seleccione el `localhost.cer` archivo que arrastró al escritorio. Haga clic `Always Trust` en el cuadro de diálogo que aparece.
  * Después de agregar el certificado a la cadena de claves del sistema, haga doble clic en el certificado y expanda la `Trust` sección de los detalles del certificado. Seleccione `Always Trust` para cada opción.

> [!IMPORTANT]
> Si recibe una advertencia de certificado de seguridad, vaya a https://localhost:3000/tab . Si el sitio sigue sin ser de confianza, reinicie el equipo y el host local debería aceptarse como de confianza.
</details>

## <a name="run-your-app-in-teams"></a>Ejecutar la aplicación en Microsoft Teams
- Requisitos previos:
  - [Habilitar el modo de vista previa de desarrolladores de Microsoft Teams](https://aka.ms/teams-toolkit-enable-devpreview)

1. Navegue a la barra de actividades en el lado izquierdo de la ventana de Visual Studio Code.
1. Seleccione el icono **Ejecutar** para mostrar la vista **Ejecutar y depurar** .
1. También puede usar el método abreviado de teclado `Ctrl+Shift+D` .

## <a name="validate-your-app"></a>Validar la aplicación

La página **validar** permite comprobar el paquete de la aplicación antes de enviar la aplicación a AppSource. Simplemente cargue el paquete del manifiesto y la herramienta de validación comprobará la aplicación en todos los casos de prueba relacionados con el manifiesto. Para cada prueba con errores, la descripción proporciona un vínculo de documentación para ayudarle a corregir el error. Para las pruebas que son difíciles de automatizar, los detalles de la **lista de comprobación preliminar** 7 de los casos de prueba con errores más comunes, así como un vínculo a una lista de comprobación de envío completa.

## <a name="publish-your-app-to-teams"></a>Publicar la aplicación en Teams

En la Página principal de su proyecto, puede cargar su aplicación en un equipo, enviar la aplicación a la tienda de aplicaciones personalizada de la empresa para los usuarios de su organización o bien enviar la aplicación al origen de la aplicación para todos los usuarios de Microsoft Teams. El administrador de ti consultará estos envíos. Puede volver a la página *publicar* para comprobar el estado del envío y saber si su administrador de ti aprobó o rechazó la aplicación. Aquí también puede ir a enviar actualizaciones a la aplicación o cancelar los envíos actualmente activos.

> [!div class="nextstepaction"]
> [Siguiente paso: mantenimiento y soporte de la aplicación publicada](../concepts/deploy-and-publish/appsource/post-publish/overview.md)

---
title: 'Introducción: creación y ejecución de la primera aplicación'
author: heath-hamilton
description: Cree rápidamente una aplicación de Microsoft teams que muestre un "Hola a todos". mensaje mediante el kit de herramientas de Microsoft Teams.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 62c4bd950183ceb64fb30b528661cf84e9210d89
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931787"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a>Crear y ejecutar su primera aplicación de Microsoft Teams

Puede ir directamente a desarrollo de Microsoft Teams creando una pestaña personal que muestre "Hola a todos".

## <a name="1-create-your-app-project"></a>1. crear un proyecto de aplicación

Use el kit de herramientas de Microsoft Teams en Visual Studio Code para configurar su primer proyecto de aplicación.

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **crear una nueva aplicación de Teams**.
1. Cuando se le solicite, inicie sesión con su cuenta de desarrollo de 365 de Microsoft.
1. En la pantalla **Agregar funciones** , seleccione la **pestaña** **siguiente**.
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Captura de pantalla que muestra cómo configurar el proyecto de aplicación con Visual Studio Code Teams Toolkit.":::
1. Escriba un nombre para la aplicación de Teams. (Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de la aplicación en el equipo local).
1. Compruebe solo la opción de la **pestaña personal** y seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.

## <a name="2-understand-important-app-project-components"></a>2. comprender los componentes importantes del proyecto de aplicación

Una vez que el kit de herramientas configura el proyecto, tiene los componentes para crear una pestaña básica personal para Teams. Los archivos y directorios del proyecto se muestran en el área del explorador de Visual Studio Code.

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Captura de pantalla que muestra archivos de proyecto de aplicación para una pestaña personal en Visual Studio Code.":::

### <a name="app-scaffolding"></a>Scaffolding de la aplicación

El kit de herramientas crea automáticamente scaffolding en el `src` directorio en función de las funciones que agregó durante la instalación.

Si crea una ficha durante la configuración, por ejemplo, el `App.js` archivo del `src/components` directorio es importante porque controla la inicialización y el enrutamiento de la aplicación. Llama al [SDK de Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md) para establecer la comunicación entre la aplicación y los equipos.

### <a name="app-id"></a>Identificador de la aplicación

El identificador de aplicación de Teams es necesario para configurar la aplicación con App Studio. Puede encontrar el identificador en el `teamsAppId` objeto, que se encuentra en el archivo del proyecto `package.json` .

## <a name="3-build-and-run-your-app"></a>3. compilar y ejecutar la aplicación

En aras del tiempo, se creará y se ejecutará la aplicación de forma local.

(Esta información también está disponible en el kit de herramientas `README` ).

1. En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .
1. Ejecutar `npm start` .

Una vez completada la **compilación correctamente.** mensaje en el terminal. La aplicación se está ejecutando en `https://localhost:3000` .

## <a name="4-sideload-your-app-in-teams"></a>4. transferir localmente la aplicación en Microsoft Teams

La aplicación está lista para realizar pruebas en Microsoft Teams. Para ello, debe tener una cuenta que permita la transferencia local de aplicaciones. (Si no está seguro de ello, obtenga información sobre cómo obtener una cuenta de desarrollo de Microsoft [Teams](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)).

> [!TIP]
> Antes de transferir localmente la aplicación, compruebe si hay problemas con la [característica de validación en App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), que se incluye en el kit de herramientas. Los errores deben corregirse para realizar una instalación de prueba de la aplicación correctamente.

1. En Visual Studio Code, presione la tecla **F5** para iniciar un cliente web de Teams.
1. Para mostrar el contenido de la aplicación en Teams, especifique que la aplicación en ejecución ( `localhost` ) sea de confianza:
   1. Abrir una nueva pestaña en la misma ventana del explorador (Google Chrome de forma predeterminada) que se abre después de presionar **F5**.
   1. Vaya a `https://localhost:3000/tab` la página y continúe con ella.
1. Vuelva a teams. En el cuadro de diálogo, seleccione **agregarme para** instalar la aplicación.
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Captura de pantalla que muestra un ejemplo de la aplicación de pestaña personal ' Hello, World! ' en Teams.":::

¡ Felicidades 🎉! La aplicación se está ejecutando en Teams.

## <a name="next-step"></a>Paso siguiente

Amplíe en la pestaña personal que acaba de crear o compile otro tipo de aplicación de Microsoft Teams.

> [!div class="nextstepaction"]
> [Agregar a la pestaña personal](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [Crear una pestaña de canal](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [Crear un bot](../build-your-first-app/build-bot.md)

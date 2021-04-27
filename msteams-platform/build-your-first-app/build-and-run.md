---
title: 'Introducción: compilación y ejecución de la primera aplicación'
author: heath-hamilton
description: Crea rápidamente una aplicación de Microsoft Teams que muestre un "¡Hola, mundo!" con Microsoft Teams Toolkit.
ms.author: lajanuar
localization_priority: Normal
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 1b34c3f3121e834abc8a8a92a8a0ac9a049c9e07
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020887"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a>Crear y ejecutar la primera aplicación de Microsoft Teams

Inicie el desarrollo de Microsoft Teams creando una pestaña personal que muestre "Hello, World!".
Cree y ejecute la primera aplicación de Teams con los pasos siguientes:

## <a name="1-create-your-app-project"></a>1. Crear el proyecto de aplicación

Usa Microsoft Teams Toolkit en Visual Studio code para configurar el primer proyecto de aplicación. Cree el proyecto de la aplicación con los pasos siguientes:

1. En Visual Studio, selecciona **Microsoft Teams en** la barra de actividades izquierda y elige Crear una nueva aplicación de :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Teams**.
1. Cuando se le pida, inicie sesión con su cuenta de desarrollo de Microsoft 365.
1. En la **pantalla Agregar funcionalidades,** seleccione **Ficha** y, a **continuación, Siguiente**.
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Captura de pantalla que muestra cómo configurar el proyecto de la aplicación con Visual Studio Code Teams Toolkit.":::
1. Escribe un nombre para la aplicación de Teams. (Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de aplicación en el equipo local).
1. Compruebe solo la **opción pestaña Personal** y seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.

## <a name="2-understand-important-app-project-components"></a>2. Comprender los componentes importantes del proyecto de la aplicación

Una vez que el kit de herramientas configura el proyecto, tiene los componentes para crear una pestaña personal básica para Teams. Los directorios y archivos del proyecto se muestran en el área Explorador de Visual Studio código.

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Captura de pantalla que muestra los archivos de proyecto de la aplicación para una pestaña personal en Visual Studio código.":::

### <a name="app-scaffolding"></a>Scaffolding de aplicaciones

El kit de herramientas crea automáticamente scaffolding en el directorio en función de las capacidades que `src` agregó durante la instalación.

Si creas una pestaña durante la instalación, por ejemplo, el archivo del directorio es importante porque controla la inicialización y `App.js` el enrutamiento de la `src/components` aplicación. Llama al [SDK de cliente de JavaScript](../tabs/how-to/using-teams-client-sdk.md) de Microsoft Teams para establecer la comunicación entre la aplicación y Teams.

### <a name="app-id"></a>Identificador de la aplicación

Configura la aplicación con App Studio con el id. de aplicación de Teams. Busque el identificador en el `teamsAppId` objeto, que se encuentra en el archivo del `package.json` proyecto.

## <a name="3-build-and-run-your-app"></a>3. Crear y ejecutar la aplicación

Compila y ejecuta la aplicación localmente para ahorrar tiempo. Esta información también está disponible en el kit de herramientas `README` . Cree y ejecute la aplicación con los pasos siguientes:

1. En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .
1. Ejecute `npm start` .

Una vez completado, hay un **compilado correctamente.** en el terminal. La aplicación se está ejecutando en `https://localhost:3000` .

## <a name="4-sideload-your-app-in-teams"></a>4. Instalación local de la aplicación en Teams

La aplicación está lista para probarse en Teams. Para ello, debes tener una cuenta de desarrollo de Microsoft 365 que permita la instalación local de aplicaciones. Para obtener más información sobre la apertura de cuentas, vea [Cuenta de desarrollo de Teams](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account). 

> [!TIP]
> Comprueba si hay problemas antes de descargar localmente la aplicación, mediante la característica de validación de [App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), que se incluye en el kit de herramientas. Se corrigen los errores para que la aplicación se desacargue correctamente.

La instalación local de la aplicación en Teams sigue estos pasos:

> [!NOTE]
> Para habilitar la instalación local antes de la instalación local de la aplicación en Teams, siga los pasos descritos en Activar la instalación [local de la aplicación](../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading).

1. Seleccione la **clave F5** para iniciar un cliente web de Teams en Visual Studio código.
1. Para mostrar el contenido de la aplicación en Teams, especifica que el lugar donde se ejecuta la aplicación ( `localhost` ) es de confianza:
   1. Abra una nueva pestaña en la misma ventana del explorador (Google Chrome de forma predeterminada) que se abrió después de presionar **F5**.
   1. Vaya a `https://localhost:3000/tab` y continúe con la página.
1. Vuelva a Teams. En el cuadro de diálogo, **selecciona Agregar para mí** para instalar la aplicación.
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Captura de pantalla que muestra un ejemplo de aplicación de pestaña personal &quot;Hello, World!&quot; que se ejecuta en Teams.":::

🎉 Enhorabuena! La aplicación se ejecuta en Teams.

## <a name="next-step"></a>Paso siguiente

Expande en la pestaña personal que acaba de crear o crea otro tipo de aplicación de Teams.

> [!div class="nextstepaction"]
> [Agregar a la pestaña personal](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [Crear una pestaña de canal](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [Crear un bot](../build-your-first-app/build-bot.md)

---
title: 'Introducción: compilar y ejecutar la primera aplicación'
author: heath-hamilton
description: Cree rápidamente una aplicación de Microsoft Teams que muestre un mensaje de "Hola a todos". con Microsoft Teams Toolkit.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 46a92f54cdbf68e28510c0bd4cc0b7018cfaae3c
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093953"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a>Crear y ejecutar la primera aplicación de Microsoft Teams

Inicie el desarrollo de Microsoft Teams creando una pestaña personal que muestre "Hello, World!".
Cree y ejecute su primera aplicación de Teams siguiendo estos pasos:

## <a name="1-create-your-app-project"></a>1. Crear el proyecto de aplicación

Use Microsoft Teams Toolkit en Visual Studio code para configurar su primer proyecto de aplicación. Cree el proyecto de aplicación siguiendo estos pasos:

1. In Visual Studio Code, select **Microsoft Teams** on the left Activity Bar and choose Create a new Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **app**.
1. Cuando se le solicite, inicie sesión con su cuenta de desarrollo de Microsoft 365.
1. En la **pantalla Agregar funcionalidades,** seleccione **Pestaña** y, a **continuación, Siguiente.**
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Captura de pantalla que muestra cómo configurar el proyecto de aplicación con Visual Studio Kit de herramientas de Code Teams.":::
1. Escriba un nombre para su aplicación de Teams. (Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de aplicación en el equipo local).
1. Comprueba solo la **opción de pestaña Personal** y selecciona **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.

## <a name="2-understand-important-app-project-components"></a>2. Comprender los componentes importantes del proyecto de la aplicación

Una vez que el kit de herramientas configura el proyecto, tiene los componentes para crear una pestaña personal básica para Teams. Los archivos y directorios del proyecto se muestran en el área Explorador de Visual Studio código.

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Captura de pantalla que muestra los archivos de proyecto de la aplicación para una pestaña personal en Visual Studio código.":::

### <a name="app-scaffolding"></a>Scaffolding de aplicaciones

El kit de herramientas crea automáticamente scaffolding para ti en el directorio en función de las `src` funcionalidades que agregaste durante la instalación.

Si creas una pestaña durante la instalación, por ejemplo, el archivo del directorio es importante porque controla la inicialización y el `App.js` `src/components` enrutamiento de la aplicación. Llama al SDK del cliente [de JavaScript](../tabs/how-to/using-teams-client-sdk.md) de Microsoft Teams para establecer la comunicación entre la aplicación y Teams.

### <a name="app-id"></a>Identificador de la aplicación

Configure su aplicación con App Studio con el id. de aplicación de Teams. Busque el identificador en el `teamsAppId` objeto, que se encuentra en el archivo del `package.json` proyecto.

## <a name="3-build-and-run-your-app"></a>3. Compilar y ejecutar la aplicación

Compila y ejecuta la aplicación localmente para ahorrar tiempo. Esta información también está disponible en el kit de `README` herramientas. Compila y ejecuta la aplicación mediante los siguientes pasos:

1. En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .
1. Ejecute `npm start` .

Una vez completado, se compila **correctamente.** en el terminal. La aplicación se está ejecutando en `https://localhost:3000` .

## <a name="4-sideload-your-app-in-teams"></a>4. Instalación local de la aplicación en Teams

La aplicación está lista para probarse en Teams. Para ello, debe tener una cuenta de desarrollo de Microsoft 365 que permita la instalación de prueba de aplicaciones. Para obtener más información sobre la apertura de cuentas, consulte [Cuenta de desarrollo de Teams.](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account) 

> [!TIP]
> Comprueba si hay problemas antes de realizar la instalación de prueba de la aplicación, mediante la característica de validación [de App Studio,](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)que se incluye en el kit de herramientas. Se solucionan los errores para que la aplicación se trascargue correctamente.

Haga una instalación de instalación local de la aplicación en Teams siguiendo estos pasos:

> [!NOTE]
> Para habilitar la instalación de instalación de local antes de realizar la instalación de local de la aplicación en Teams, siga los pasos descritos en [Turn on app sideloading](../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading).

1. Seleccione la **tecla F5** para iniciar un cliente web de Teams en Visual Studio código.
1. Para mostrar el contenido de la aplicación en Teams, especifique que el lugar donde se ejecuta la aplicación ( `localhost` ) es de confianza:
   1. Abra una nueva pestaña en la misma ventana del explorador (Google Chrome de forma predeterminada) que se abrió después de presionar **F5**.
   1. Vaya a `https://localhost:3000/tab` la página y continúe.
1. Vuelva a Teams. En el cuadro de diálogo, **selecciona Agregar para instalar** la aplicación.
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Captura de pantalla que muestra un ejemplo de aplicación de pestaña personal &quot;Hello, World!&quot; que se ejecuta en Teams.":::

🎉 Enhorabuena. La aplicación se está ejecutando en Teams.

## <a name="next-step"></a>Paso siguiente

Expanda la pestaña personal que acaba de crear o cree otro tipo de aplicación de Teams.

> [!div class="nextstepaction"]
> [Agregar a la pestaña personal](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [Crear una pestaña de canal](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [Crear un bot](../build-your-first-app/build-bot.md)

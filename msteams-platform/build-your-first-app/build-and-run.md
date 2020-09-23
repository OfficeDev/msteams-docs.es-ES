---
title: Compilar y ejecutar una "Hello, World!" Aplicación de Teams
author: heath-hamilton
description: Cree y ejecute su primera aplicación de Microsoft Teams, una pestaña personal que muestra "Hola a todos".
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: quickstart
ms.openlocfilehash: 5be2e8f2932a91ed11137f3a7be544e12bd65559
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210338"
---
# <a name="build-a-hello-world-teams-app"></a>Crear un "Hello, World!" Aplicación de Teams

Puede ir directamente a desarrollo de la plataforma Microsoft Teams creando una pestaña personal que muestre "Hola a todos".

## <a name="create-your-app-project"></a>Crear el proyecto de la aplicación

Use el kit de herramientas de Microsoft Teams en Visual Studio Code para configurar su primer proyecto de aplicación.

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **crear una nueva aplicación de Teams**.
:::image type="content" source="../assets/images/build-your-first-app/create-teams-app.png" alt-text="Captura de pantalla que muestra cómo crear una nueva aplicación con el kit de herramientas de Visual Studio Code Teams.":::
1. Escriba un nombre para la aplicación de Teams. (Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de la aplicación en el equipo local).
1. En la pantalla **Agregar funciones** , seleccione la **pestaña** **siguiente**.
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Captura de pantalla que muestra cómo configurar el proyecto de aplicación con Visual Studio Code Teams Toolkit.":::
1. Compruebe la opción de la **ficha personal** y seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.

## <a name="understand-important-app-project-components"></a>Comprender los componentes importantes del proyecto de aplicación

Una vez que el kit de herramientas configura el proyecto, tiene los componentes para crear una pestaña básica personal para Teams. Los archivos y directorios del proyecto se muestran en el área del explorador de Visual Studio Code.

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Captura de pantalla que muestra archivos de proyecto de aplicación para una pestaña personal en Visual Studio Code.":::

Dedique un momento a comprender algunos de los archivos principales con los que trabajan los desarrolladores de aplicaciones.

### <a name="app-manifest-manifestjson"></a>Manifiesto de la aplicación ( `manifest.json` )

Ubicado en el `.publish` directorio, el manifiesto de la aplicación es el punto de partida para cualquier proyecto de aplicación. El manifiesto define los atributos fundamentales de la aplicación y apunta a los recursos necesarios. Al instalar una aplicación, Microsoft Teams analiza el manifiesto para comprender cómo representar la aplicación en el cliente.

### <a name="app-scaffolding"></a>Scaffolding de la aplicación

El kit de herramientas crea automáticamente scaffolding en el `src` directorio en función de las funciones que agregó durante la instalación.

Si crea una ficha durante la configuración, por ejemplo, el `App.js` archivo del `src/components` directorio es importante porque controla la inicialización y el enrutamiento de la aplicación. Llama al [SDK de Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md) para establecer la comunicación entre la aplicación y los equipos.

### <a name="app-package-developmentzip"></a>Paquete de la aplicación ( `Development.zip` )

Ubicado en el `.publish` directorio, necesita que el paquete de la aplicación [transfiera localmente la aplicación](../concepts/deploy-and-publish/overview.md#upload-your-app-directly) en Teams. El paquete también se usa cuando se [publica en el catálogo de aplicaciones de la organización](../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) o [AppSource](../concepts/deploy-and-publish/appsource/publish.md).

Estos son algunos detalles sobre los archivos del paquete de la aplicación:

|Nombre|Tipo|Size|Ubicación del manifiesto|Nombre de archivo Toolkit|
|---|---|:---:|:---:|-----|
|**Manifiesto de la aplicación**|`.json`| — | — |`.publish/manifest.json`|
|**Logotipo-color**|`.png`|192 &times; 192 píxeles|`icon.color`|`.publish/color.png`|
|**Logotipo de contorno**|`.png`|32 &times; 32 píxeles|`icon.outline`|`.publish/outline.png`|

## <a name="run-your-app"></a>Ejecutar la aplicación

En aras del tiempo, se creará y se ejecutará la aplicación de forma local.

(Esta información también está disponible en el kit de herramientas `README` ).

1. En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .
1. Ejecutar `npm start` . Una vez completada la **compilación correctamente.** mensaje en el terminal.
1. Abra un explorador y vaya a `https://localhost:3000` para ver una página web en blanco denominada **pestaña de Microsoft Teams**. (No se preocupe porque no puede ver ningún contenido en la página).<br/>
   :::image type="content" source="../assets/images/build-your-first-app/local-host-tab.png" alt-text="Captura de pantalla que muestra el aspecto que tiene para ver la aplicación que se está ejecutando en un explorador.":::

## <a name="set-up-a-secure-tunnel-to-your-app"></a>Configurar un túnel seguro para la aplicación

La aplicación está en funcionamiento en el servidor Web local. Para ejecutar la aplicación en Microsoft Teams, debe ser `localhost` accesible a través de HTTPS.

Instale [ngrok](https://ngrok.com/download) si todavía no lo ha hecho. Al ejecutar esta herramienta, se crean dos direcciones URL disponibles globalmente que apuntan a su servidor Web local ( `http://localhost:3000` ). Necesita la dirección URL de reenvío que comienza con `HTTPS` .

1. Abra un nuevo terminal y ejecute `ngrok http 3000` .
1. Copie la dirección URL HTTPS que ha proporcionado (vea el siguiente ejemplo).
:::image type="content" source="../assets/images/build-your-first-app/ngrok-running.png" alt-text="Captura de pantalla que muestra un terminal con ngrok en ejecución.":::
1. En el `.publish` directorio, Abra `Development.env` .
1. Reemplace el `baseUrl0` valor por la dirección URL copiada. (Por ejemplo, cambie `baseUrl0=http://localhost:3000` a `baseUrl0=https://85528b2b3ba5.ngrok.io` ).

El manifiesto de la aplicación ahora apunta al lugar donde se hospeda la aplicación.

## <a name="sideload-your-app-in-teams"></a>Transferir localmente la aplicación en Microsoft Teams

Una vez que la aplicación se ejecute y sea accesible a través de HTTPS, estará listo para cargarla a teams.

> [!TIP]
> Antes de transferir localmente la aplicación, compruebe si hay problemas con la [característica de validación del kit de herramientas](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool). Los errores deben corregirse para realizar una instalación de prueba de la aplicación correctamente.

1. Inicie sesión en el cliente de Teams con su cuenta que permite la transferencia local de aplicaciones. (Si no está seguro de ello, obtenga información sobre cómo obtener una cuenta de desarrollo de Microsoft [Teams](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)).
1. Seleccione **aplicaciones**y, después, elija **cargar una aplicación personalizada**.
1. Vaya a la carpeta de proyecto de la aplicación `.publish` y seleccione `Development.zip` . Se muestra un modal de instalación.
:::image type="content" source="../assets/images/build-your-first-app/add-teams-app.png" alt-text="Captura de pantalla que muestra un ejemplo de una instalación de aplicación de Teams modal.":::
1. Seleccione **Agregar** para instalar la aplicación.
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Captura de pantalla que muestra un ejemplo de la aplicación de pestaña personal ' Hello, World! ' en Teams.":::

¡ Felicidades 🎉! La aplicación se está ejecutando en Teams.

## <a name="next-step"></a>Paso siguiente

Amplíe en la pestaña personal que acaba de crear o compile otro tipo de aplicación de Microsoft Teams.

> [!div class="nextstepaction"]
> [Agregar a la pestaña personal](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [Crear una ficha de canal](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [Crear un bot](../build-your-first-app/build-bot.md)

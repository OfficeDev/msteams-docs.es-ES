---
title: Compilar y ejecutar la aplicación primera aplicación de Microsoft Teams
author: heath-hamilton
description: Ejecute su primera aplicación de Microsoft Teams.
ms.openlocfilehash: 98af8d8d6d89007e36c24bd34661ec21b33cbdf1
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652228"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a>Crear y ejecutar su primera aplicación de Microsoft Teams

Puede pasar directamente al desarrollo en la plataforma de Microsoft Teams creando y ejecutando rápidamente una aplicación básica.

> [!NOTE]
> Resulta útil tener un conocimiento práctico de JavaScript (en concreto reaccionar) al seguir estos tutoriales.

## <a name="set-up-your-development-account"></a>Configurar la cuenta de desarrollo

Para compilar aplicaciones para Microsoft Teams, necesita una cuenta de teams que permita la transferencia local (es posible que la cuenta ya la proporcione). Si no es así, Regístrese para obtener una suscripción de desarrollador de Microsoft 365 para que pueda obtener un inquilino de prueba.

1. Compruebe si puede transferir aplicaciones en Microsoft Teams:
    1. En el cliente de Microsoft Teams, seleccione **aplicaciones**.
    1. Busca una opción para **cargar una aplicación personalizada**.
1. Si tiene esta opción, puede empezar a crear. Si no es así, haga lo siguiente:
    1. Regístrese para obtener una [suscripción de desarrollador de Microsoft 365](../doc-links/prepare-your-o365-tenant.md).
    1. [Habilite la transferencia local de aplicaciones personalizada](../doc-links/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) para su cuenta de prueba.

## <a name="get-your-development-tools"></a>Obtener las herramientas de desarrollo

Puede crear aplicaciones de Teams con sus herramientas preferidas, pero esto es lo que necesita para empezar rápidamente con Visual Studio Code y el kit de herramientas de Microsoft Teams.

1. Instale la versión más reciente de [Visual Studio Code](https://code.visualstudio.com/download).
1. En Visual Studio Code, seleccione **extensions** ![ Visual Studio Toolkit View ](../doc-links/images/vs-code-extensions.png) en la barra de actividad izquierda e instale **Microsoft Teams Toolkit**.
1. Instale [Node.js](https://nodejs.org/en/).

## <a name="create-an-app-project"></a>Crear un proyecto de aplicación

El kit de herramientas de Microsoft Teams puede ayudarle a configurar su primer proyecto de aplicación.

1. En Visual Studio Code, abra el kit de herramientas seleccionando el icono de Teams ![icono de Teams](../doc-links/images/favicon-16x16.png) en la barra de actividad izquierda.
1. Seleccione **crear una nueva aplicación de Teams**.
1. Cuando se le solicite, escriba un nombre para la aplicación. Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto en el equipo local.
1. En la pantalla **Agregar funciones** , seleccione la **pestaña** **siguiente**.
1. Compruebe la opción de la **ficha personal** y seleccione **Finalizar** para configurar el proyecto.

![vista del kit de herramientas agregar pestañas](../doc-links/images/toolkit-add-tabs.PNG)

Una vez completada, tiene los componentes de scaffolding de la aplicación para crear una pestaña personal.

## <a name="run-your-app"></a>Ejecutar la aplicación

Siga el `README.md` en su proyecto para compilar, ejecutar e implementar la aplicación en Teams. En general, estas instrucciones le ayudarán a hacer lo siguiente:

* Hospedar la aplicación `localhost` .
* [Configure un túnel seguro con ngrok](../doc-links/debug.md#locally-hosted) para que Microsoft Teams pueda acceder a la aplicación. (Instalar [ngrok](https://ngrok.com/download)).
* [Transfiera localmente la aplicación](../doc-links/apps-upload.md) en el cliente de Microsoft Teams usando el `Development.zip` de la `.publish` carpeta.

Después de transferir localmente la aplicación, debe tener este aspecto en el cliente de Microsoft Teams.

![Ficha de ejemplo Hello World](../doc-links/images/tab-running.png)

## <a name="important-app-project-files"></a>Archivos de proyecto de aplicación importantes

Con el proyecto de la aplicación y la configuración de scaffolding, dedique algún tiempo a comprender algunos de los archivos clave en los que trabajan los desarrolladores de aplicaciones.

### <a name="app-manifest-manifestjson"></a>Manifiesto de la aplicación ( `manifest.json` )

Ubicado en el `.publish` directorio, el manifiesto de la aplicación es el punto de partida para cualquier proyecto de aplicación. El manifiesto define los atributos fundamentales de la aplicación y apunta a los recursos necesarios. Al instalar una aplicación, Microsoft Teams analiza el manifiesto para comprender cómo representar la aplicación en el cliente.

En los siguientes tutoriales, nos centraremos en las secciones del manifiesto de la aplicación para crear pestañas personales y de canal.

### <a name="package-developmentzip"></a>Package ( `Development.zip` )

También se encuentra en el `.publish` directorio, necesita el paquete de la aplicación para [transferir localmente la aplicación](../../overview.md#how-can-you-share-your-teams-app) en Teams. También se usa cuando se [publica en el catálogo de aplicaciones de la organización](../../overview.md#how-can-you-share-your-teams-app) o [AppSource](../../concepts/deploy-and-publish/appsource/publish.md).

Estos son algunos detalles sobre los archivos del paquete de la aplicación:

|Nombre|Tipo|Size|Ubicación del manifiesto|Nombre de archivo Toolkit|
|---|---|:---:|:---:|-----|
|**Manifiesto de la aplicación**|`.json`| — | — |`.publish/manifest.json`|
|**Logotipo-color**|`.png`|192 &times; 192 píxeles|`icon.color`|`.publish/color.png`|
|**Logotipo de contorno**|`.png`|32 &times; 32 píxeles|`icon.outline`|`.publish/outline.png`|

### <a name="scaffolding-src"></a>Scaffolding ( `src` )

El kit de herramientas crea automáticamente scaffolding en el `src` directorio en función de las funciones que agregó durante la instalación.

Aunque algunos archivos se crean sin importar el tipo de aplicación que tenga. Por ejemplo, el `App.js` archivo en el `src/components` directorio es importante porque controla la inicialización y el enrutamiento de la aplicación. Lo más importante es que llama al [SDK de Microsoft Teams](../doc-links/using-teams-client-sdk.md) para establecer la comunicación entre la aplicación y los equipos.

Puede obtener más información sobre la técnica de scaffolding en los tutoriales para crear pestañas personales y de canal.

## <a name="next-step"></a>Paso siguiente

¡ Felicidades 🎉! Tiene una aplicación de Teams en ejecución. Seleccione el siguiente botón para obtener información sobre cómo agregar una característica real al mismo.

> [!div class="nextstepaction"]
> [Crear una pestaña personal](add-personal-tab.md)

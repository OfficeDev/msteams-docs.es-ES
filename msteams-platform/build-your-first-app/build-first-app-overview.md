---
title: 'Introducción: crear la primera introducción a la aplicación y los requisitos previos'
author: heath-hamilton
description: Obtenga información sobre cómo empezar a desarrollar aplicaciones de Microsoft Teams y configurar su entorno.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 06e26c57e6f6d3fd0bbeb981ef7ab46c8217bb4a
ms.sourcegitcommit: 5687a901d48bcf2f5a3a086e0f703f854e8b9c21
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/11/2021
ms.locfileid: "49795464"
---
# <a name="build-your-first-microsoft-teams-app-overview"></a>Crear la primera introducción a la aplicación de Microsoft Teams

En la **compilación de las primeras lecciones de** aplicación, se crean aplicaciones básicas de Teams. Cada tutorial le guiará a través de cómo crear una aplicación de Teams sencilla y real, a la vez que le presenta herramientas comunes, conceptos fundamentales y características más avanzadas.

## <a name="what-youll-learn"></a>Lo que aprenderás

Esta es una idea de lo que sabrá después de pasar por las lecciones.

> [!div class="checklist"]
  >
  > * Empezar a trabajar rápidamente con el kit de herramientas de **Teams:** Microsoft Teams Toolkit para Visual Studio Code se encarga de crear el proyecto de aplicación y el scaffolding para que pueda tener una aplicación en ejecución en minutos.
  > * **Configure su aplicación con App Studio:** especifique las funcionalidades y los servicios que usa la aplicación de Teams.
  > * **Ámbito de la audiencia de la aplicación:** cree una aplicación de Teams para uso personal, colaboración o ambos.
> * **Obtenga experiencia con las herramientas y SDK** de Teams: personalice su aplicación con la ayuda del SDK del cliente de JavaScript de Teams. Por ejemplo, cambie la combinación de colores de la aplicación para que coincida con el tema de Teams. Además, obtenga información sobre las herramientas comunes para crear y administrar bots.
  > * **Expande tu aplicación:** a lo largo de las lecciones, encontrarás temas relacionados que probablemente te interesen (como las directrices de autenticación y diseño).

## <a name="teams-app-fundamentals"></a>Aspectos básicos de la aplicación de Teams

Antes de comenzar los tutoriales, debe conocer lo siguiente sobre la creación de aplicaciones para Teams.

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a>Las aplicaciones pueden tener varias funcionalidades y puntos de entrada

Una aplicación de Teams está integrada por una o más funcionalidades de plataforma [(cómo](../concepts/capabilities-overview.md) los demás usan la aplicación) y puntos de entrada [(donde](../concepts/extensibility-points.md) los demás descubren la aplicación).

### <a name="teams-doesnt-host-your-app"></a>Teams no hospeda la aplicación

Una aplicación de Teams incluye las siguientes partes importantes:

* La lógica, el almacenamiento de datos y las llamadas API que potencian la aplicación. Estos servicios no se hospedan en Teams y deben ser accesibles a través de HTTPS.
* El cliente de Teams (web, de escritorio o móvil) donde los usuarios usan la aplicación.
* El id. de la aplicación, que te permite configurar la aplicación con App Studio.

## <a name="get-prerequisites"></a>Obtener requisitos previos

Compruebe que tiene la cuenta adecuada para crear aplicaciones de Teams e instale algunas herramientas de desarrollo recomendadas.

### <a name="set-up-your-development-account"></a>Configurar la cuenta de desarrollo

Necesita una cuenta de Teams que permita la instalación de prueba de aplicaciones personalizadas. (Es posible que su cuenta ya lo proporcione).

1. Si tiene una cuenta de Teams, compruebe si puede realizar la instalación de instalación local de aplicaciones en Teams:
    1. En el cliente de Teams, seleccione **Aplicaciones.**
    1. Busque una opción para **cargar una aplicación personalizada.**

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Ilustración que muestra dónde se puede cargar una aplicación personalizada en Teams.":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><b>Seleccione aquí</b> si no puede ver la opción de instalación de local o no tiene una cuenta de Teams.</summary>

Puede obtener una cuenta de prueba gratuita de Teams que permita la instalación de prueba de aplicaciones si se une al programa de desarrolladores de Microsoft 365. (El proceso de registro tarda aproximadamente dos minutos).

1. Vaya al programa de desarrolladores de [Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program)
1. Seleccione **Unirse ahora** y siga las instrucciones en pantalla.
1. Cuando llegue a la pantalla de bienvenida, seleccione **Configurar suscripción E5.**
1. Configure su cuenta de administrador. Una vez que termines, deberías ver una pantalla como esta.
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Ejemplo de lo que ve después de registrarse en el programa de desarrolladores de Microsoft 365.":::
1. Inicie sesión en Teams con la cuenta de administrador que acaba de configurar.
1. Comprueba si ahora tienes la opción **Cargar una aplicación** personalizada.

</details>

> [!Note]
> Si aún no puede realizar la instalación de instalación local de aplicaciones, vea habilitar aplicaciones personalizadas de Teams y activar la carga [de aplicaciones personalizadas.](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)

### <a name="install-your-development-tools"></a>Instalar las herramientas de desarrollo

Puede crear aplicaciones de Teams con sus herramientas preferidas, pero estas lecciones muestran cómo puede empezar rápidamente con Microsoft Teams Toolkit for Visual Studio Code.

Teams muestra el contenido de la aplicación solo a través de conexiones HTTPS. Para depurar ciertos tipos de aplicaciones localmente, como un bot, aprenderá a usar [ngrok](../concepts/build-and-test/debug.md#locally-hosted) para configurar un túnel seguro entre Teams y su aplicación. (Las aplicaciones de Teams de producción se hospedan en la nube).

1. Instale [Node.js](https://nodejs.org/en/).
1. Instale [ngrok](https://ngrok.com/download) si tiene previsto crear un bot o una extensión de mensajería.
1. Instale la versión más reciente [de Visual Studio código.](https://code.visualstudio.com/download) (Es posible que las versiones anteriores no funcionen con el kit de herramientas).
1. En Visual Studio, seleccione **Extensiones en** la barra de actividades de la izquierda e instale Microsoft :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: Teams **Toolkit.**

    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Ilustración que muestra dónde en Visual Studio código puede instalar la extensión de Microsoft Teams Toolkit.":::

## <a name="about-the-tutorials"></a>Acerca de los tutoriales

Puede empezar con cualquiera de las lecciones de teams **para crear sus primeras lecciones de** aplicación. Si no estás seguro de dónde ir primero, sigue nuestra ruta de acceso fácil para principiantes y crea un "Hello, World!". app.

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="Árbol de aptitudes que muestra las rutas de aprendizaje para los tutoriales de Teams &quot;crear la primera aplicación&quot;." border="false":::

## <a name="next-step"></a>Paso siguiente

Una vez configurada la cuenta y el entorno, puede empezar a compilar.

### <a name="beginner-friendly-tutorial"></a>Tutorial descriptivo para principiantes

> [!div class="nextstepaction"]
> [Crear una aplicación "Hello, World!"](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a>Otros tutoriales

> [!div class="nextstepaction"]
> [Crear un bot](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [Crear una extensión de mensajería](../build-your-first-app/build-messaging-extension.md)

---
title: 'Introducción: crear la primera introducción a la aplicación y los requisitos previos'
author: heath-hamilton
description: Obtén información sobre cómo empezar con el desarrollo de aplicaciones de Microsoft Teams y cómo configurar el entorno.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 11bc263fae28866338abf37456ccf483d9f0a9fd
ms.sourcegitcommit: e78c9f51c4538212c53bb6c6a45a09d994896f09
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/05/2021
ms.locfileid: "51585865"
---
# <a name="build-your-first-microsoft-teams-app-overview"></a>Crear la primera introducción a la aplicación de Microsoft Teams

En las **lecciones de introducción,** aprenderás a crear aplicaciones básicas de Teams. Cada tutorial explica cómo crear una aplicación de Teams sencilla y real al mismo tiempo que te presenta herramientas comunes, conceptos fundamentales y características más avanzadas.

## <a name="what-youll-learn"></a>Lo que aprenderás

Esta es una idea de lo que sabrá después de pasar por las lecciones.

> [!div class="checklist"]
  >
  > * Descárgase y ejecutándose rápidamente con **Teams Toolkit:** Microsoft Teams Toolkit for Visual Studio Code se encarga de crear el proyecto de aplicación y el scaffolding para que pueda tener una aplicación en ejecución en minutos.
  > * **Configurar la aplicación con App Studio:** especifica las funcionalidades y los servicios que usa la aplicación de Teams.
  > * **Ámbito de la audiencia de la aplicación:** crear una aplicación de Teams para uso personal, colaboración o ambos.
> * **Obtenga experiencia con las herramientas y SDK** de Teams: personalice la aplicación con la ayuda del SDK de cliente de JavaScript de Teams. Por ejemplo, cambia la combinación de colores de la aplicación para que coincida con el tema de Teams. Además, obtenga información sobre las herramientas comunes para crear y administrar bots.
  > * **Expande tu aplicación:** a lo largo de las lecciones, encontrarás temas relacionados que probablemente te interesen (como la autenticación y las directrices de diseño).

## <a name="teams-app-fundamentals"></a>Conceptos básicos de la aplicación de Teams

Antes de comenzar los tutoriales, debes saber lo siguiente sobre cómo crear aplicaciones para Teams.

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a>Las aplicaciones pueden tener varias funcionalidades y puntos de entrada

Una aplicación de Teams está integrada por una o más funcionalidades de plataforma [(cómo](../concepts/capabilities-overview.md) usan las personas la aplicación) y puntos de entrada [(donde](../concepts/extensibility-points.md) las personas usan la aplicación).

### <a name="teams-doesnt-host-your-app"></a>Teams no hospeda la aplicación

Una aplicación de Teams incluye las siguientes partes importantes:

* La lógica, el almacenamiento de datos y las llamadas API que potencian la aplicación. Teams no hospeda estos servicios y deben ser accesibles a través de HTTPS.
* El cliente de Teams (web, de escritorio o móvil) donde los usuarios usan la aplicación.
* El identificador de la aplicación, que te permite configurar la aplicación con App Studio.

## <a name="get-prerequisites"></a>Obtener requisitos previos

Comprueba que tienes la cuenta adecuada para crear aplicaciones de Teams e instalar algunas herramientas de desarrollo recomendadas.

### <a name="set-up-your-development-account"></a>Configurar la cuenta de desarrollo

Necesitas una cuenta de Teams que permita la instalación local de aplicaciones personalizadas. (Es posible que su cuenta ya lo proporcione).

1. Si tienes una cuenta de Teams, comprueba si puedes realizar la instalación local de aplicaciones en Teams:
    1. En el cliente de Teams, seleccione **Aplicaciones**.
    1. Busque una opción para **Cargar una aplicación personalizada.**

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Ilustración que muestra dónde se puede cargar una aplicación personalizada en Teams.":::
    
    Si no ves el botón, no tienes permiso para cargar aplicaciones personalizadas en tu organización. Puedes obtener esta característica al suscribirte a una suscripción gratuita para desarrolladores de Microsoft 365.

<!-- markdownlint-disable MD033 -->
<details>

<summary><b>Obtener la suscripción gratuita para desarrolladores de Microsoft 365</b></summary>

Puedes obtener una cuenta de prueba gratuita de Teams que permite la instalación local de aplicaciones uniéndose al programa para desarrolladores de Microsoft 365. (El proceso de registro tarda aproximadamente dos minutos).

1. Vaya al programa para desarrolladores de [Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).
1. Selecciona **Unirse ahora** y sigue las instrucciones en pantalla.
1. Cuando llegue a la pantalla de bienvenida, seleccione **Configurar la suscripción de E5**.
1. Configurar la cuenta de administrador. Una vez que termines, deberías ver una pantalla como esta.
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Ejemplo de lo que ve después de registrarse en el programa para desarrolladores de Microsoft 365.":::
1. Inicie sesión en Teams con la cuenta de administrador que acaba de configurar.
1. Comprueba si ahora tienes la opción **Cargar una aplicación** personalizada.

</details>

> [!Note]
> Si aún no puedes realizar la instalación local de aplicaciones, consulta Habilitar aplicaciones personalizadas de Teams y activar la carga [de aplicaciones personalizadas.](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)

### <a name="install-your-development-tools"></a>Instalar las herramientas de desarrollo

Puedes crear aplicaciones de Teams con tus herramientas preferidas, pero estas lecciones muestran cómo puedes empezar rápidamente con Microsoft Teams Toolkit for Visual Studio Code.

Teams muestra el contenido de la aplicación solo a través de conexiones HTTPS. Para depurar ciertos tipos de aplicaciones localmente, como un bot, aprenderás a usar [ngrok](../concepts/build-and-test/debug.md#locally-hosted) para configurar un túnel seguro entre Teams y tu aplicación. (Las aplicaciones de Production Teams se hospedan en la nube).

1. Instale [Node.js](https://nodejs.org/en/).
1. Instale [ngrok](https://ngrok.com/download) si tiene previsto crear un bot o una extensión de mensajería.
1. Instale la versión más reciente [de Visual Studio Code](https://code.visualstudio.com/download). (Es posible que las versiones anteriores no funcionen con el kit de herramientas).
1. En Visual Studio, seleccione **Extensiones en** la barra de actividades izquierda e instale Microsoft :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: Teams **Toolkit**.

    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Ilustración que muestra dónde en Visual Studio código puede instalar la extensión microsoft Teams Toolkit.":::

## <a name="about-the-tutorials"></a>Acerca de los tutoriales

Puedes empezar con cualquiera de las lecciones de introducción **de** Teams. Si no estás seguro de dónde ir primero, sigue nuestra ruta de acceso fácil para principiantes y crea un "Hello, World!" app.

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="Árbol de aptitudes que muestra rutas de aprendizaje para las lecciones de &quot;introducción&quot; de Teams." border="false":::

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

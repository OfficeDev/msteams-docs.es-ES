---
title: 'Introducción: compilar la primera introducción a la aplicación y requisitos previos'
author: heath-hamilton
description: Obtenga información sobre cómo empezar a trabajar con el desarrollo de aplicaciones de Microsoft Teams y configurar el entorno.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: e2e73e755c45fa3bff3b6320dfbf0999a575fe99
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346815"
---
# <a name="build-your-first-microsoft-teams-app-overview"></a>Crear su primera información general de la aplicación Microsoft Teams

En la lección **compilar la primera aplicación** , puede crear aplicaciones básicas de Teams. En cada tutorial se explica cómo crear una aplicación sencilla y real de Teams, a la vez que se presentan herramientas comunes, conceptos fundamentales y características más avanzadas.

## <a name="what-youll-learn"></a>Qué aprenderá

Esta es una idea de lo que sabrá después de pasar por las lecciones.

> [!div class="checklist"]
  >
  > * **Póngase en marcha rápidamente con Team Toolkit**: el kit de herramientas de Microsoft Teams para Visual Studio Code se encarga de crear el proyecto de la aplicación y el scaffolding para que pueda tener una aplicación en ejecución en minutos.
  > * **Configurar la aplicación con App Studio**: especificar las capacidades y los servicios que usa la aplicación de Microsoft Teams.
  > * **Alcance la audiencia de la aplicación**: cree una aplicación de Microsoft Teams para uso personal, colaboración o ambos.
  > * **Obtenga experiencia con las herramientas y los SDK** de Microsoft: Personalice la aplicación (por ejemplo, cambie su combinación de colores para que sea igual que la del tema de Microsoft Teams) con la ayuda del SDK de Microsoft Teams. Además, obtenga información sobre las herramientas comunes para crear y administrar bots.
  > * **Expandir en la aplicación**: en todas las lecciones, encontrará temas relacionados que probablemente le interesan (como las directrices de autenticación y de diseño).

## <a name="teams-app-fundamentals"></a>Conceptos básicos de las aplicaciones de Microsoft Teams

Antes de empezar con los tutoriales, debe conocer lo siguiente acerca de la creación de aplicaciones para Microsoft Teams.

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a>Las aplicaciones pueden tener varias capacidades y puntos de entrada

Una aplicación de Microsoft Teams se compone de una o varias [capacidades de plataforma](../concepts/capabilities-overview.md) (cómo los usuarios usan la aplicación) y [puntos de entrada](../concepts/extensibility-points.md) (donde los usuarios detectan la aplicación).

### <a name="teams-doesnt-host-your-app"></a>Microsoft Teams no hospeda la aplicación

Una aplicación de Microsoft Teams incluye los siguientes elementos importantes:

* La lógica, el almacenamiento de datos y las llamadas API que encienden la aplicación. Estos servicios no se hospedan en Microsoft Teams y deben ser accesibles a través de HTTPS.
* El cliente de Microsoft Teams (Web, escritorio o móvil) donde los usuarios usan la aplicación.
* El identificador de la aplicación, que permite configurar la aplicación con App Studio.

## <a name="get-prerequisites"></a>Obtener requisitos previos

Compruebe que tiene la cuenta correcta para crear aplicaciones de Teams e instalar algunas herramientas de desarrollo recomendadas.

### <a name="set-up-your-development-account"></a>Configurar la cuenta de desarrollo

Necesita una cuenta de teams que permita la transferencia de una aplicación personalizada. (Es posible que la cuenta ya la proporcione).

1. Si tiene una cuenta de Teams, compruebe si puede transferir aplicaciones en Microsoft Teams:
    1. En el cliente de Microsoft Teams, seleccione **aplicaciones**.
    1. Busca una opción para **cargar una aplicación personalizada**.

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Ilustración en la que se muestra dónde en Teams puede cargar una aplicación personalizada.":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><b>Seleccione aquí</b> si no ve la opción de instalación de prueba o si no tiene una cuenta de Teams.</summary>

Puede obtener una cuenta gratuita de prueba de Microsoft teams que permite la transferencia de aplicaciones mediante la incorporación al programa de desarrolladores de Microsoft 365. (El proceso de registro dura aproximadamente dos minutos).

1. Vaya al [programa de desarrolladores de Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).
1. Seleccione **unirse ahora** y siga las instrucciones que aparecen en pantalla.
1. Cuando llegue a la pantalla de bienvenida, seleccione **configurar la suscripción a E5**.
1. Configure la cuenta de administrador. Una vez que haya terminado, debería ver una pantalla como esta.
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Ejemplo de lo que ve después de registrarse para el programa de desarrolladores de Microsoft 365.":::
1. Inicie sesión en Teams con la cuenta de administrador que acaba de configurar.
1. Compruebe si ahora tiene la opción **cargar una aplicación personalizada** .

</details>

> [!Note]
> Si sigue sin poder transferir localmente aplicaciones, consulte [Habilitar aplicaciones personalizadas de Teams y activar la carga de aplicaciones personalizadas](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).

### <a name="install-your-development-tools"></a>Instalar las herramientas de desarrollo

Puede crear aplicaciones de Teams con sus herramientas preferidas, pero estas lecciones muestran cómo puede empezar rápidamente con Microsoft Teams Toolkit para Visual Studio Code.

Teams muestra el contenido de la aplicación solo a través de conexiones HTTPS. Para depurar determinados tipos de aplicaciones de forma local, como un bot, aprenderá a usar [ngrok para configurar un túnel seguro](../concepts/build-and-test/debug.md#locally-hosted) entre Microsoft Teams y la aplicación. (Las aplicaciones de producción de Teams se hospedan en la nube).

1. Instale [Node.js](https://nodejs.org/en/).
1. Instale [ngrok](https://ngrok.com/download) si tiene previsto crear una extensión de robot o de mensajería.
1. Instale la versión más reciente de [Visual Studio Code](https://code.visualstudio.com/download). (Es posible que las versiones anteriores no funcionen con el kit de herramientas).
1. En Visual Studio Code, seleccione **extensiones** :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: en la barra de actividad izquierda e instale el **Kit de herramientas de Microsoft Teams**.

    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Ilustración que muestra dónde en Visual Studio Code puede instalar la extensión de Microsoft Teams Toolkit.":::

## <a name="about-the-tutorials"></a>Acerca de los tutoriales

Puede empezar con cualquiera de los equipos **compilar sus primeras** lecciones de la aplicación. Si no está seguro de dónde ir primero, siga nuestra ruta de acceso accesible para principiantes y cree un "Hola a todos". XXX.

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="Árbol de habilidades que muestra los caminos de aprendizaje para los tutoriales &quot;crear su primera aplicación&quot;." border="false":::

## <a name="next-step"></a>Paso siguiente

Una vez configurada la cuenta y el entorno, puede empezar a crear.

### <a name="beginner-friendly-tutorial"></a>Tutorial práctico para principiante

> [!div class="nextstepaction"]
> [Crear una aplicación "Hello, World!"](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a>Otros tutoriales

> [!div class="nextstepaction"]
> [Crear un bot](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [Crear una extensión de mensajería](../build-your-first-app/build-messaging-extension.md)

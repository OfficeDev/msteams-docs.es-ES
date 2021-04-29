---
title: 'Introducción: crear la primera introducción a la aplicación y los requisitos previos'
author: girliemac
description: Obtén información sobre cómo empezar con el desarrollo de aplicaciones de Microsoft Teams y cómo configurar el entorno.
ms.author: timura
ms.date: 03/18/2021
ms.topic: quickstart
ms.openlocfilehash: 3bc99c535ea659f046b65dc26d9a60de0dd49cab
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068570"
---
# <a name="get-started-with-microsoft-teams-app-development"></a>Introducción al desarrollo de aplicaciones de Microsoft Teams

Crea una aplicación sencilla para aprender los conceptos básicos del desarrollo de aplicaciones de Teams. Una vez que veas "Hello, World!", prueba cualquiera de los otros artículos de introducción para obtener más información sobre herramientas comunes, conceptos fundamentales y características avanzadas.



## <a name="what-youll-learn"></a>Lo que aprenderás

* Se ejecuta rápidamente con Teams Toolkit, una extensión Visual Studio code 
* Configurar la aplicación con App Studio 
* Familiarizarse con las herramientas de desarrollo y SDK de Teams
* Considera conceptos importantes de la aplicación de Teams, como la autenticación y los procedimientos recomendados de diseño

Puedes crear la aplicación de Teams con cualquier tecnología que prefieras, por ejemplo, la interfaz de línea de comandos (CLI). Sin embargo, estos artículos le ayudan a empezar con las siguientes herramientas y tecnologías recomendadas:

* Teams Toolkit, una extensión Visual Studio code
* React.js para pestañas
* Node.js para bots y extensiones de mensajería


## <a name="teams-app-fundamentals"></a>Conceptos básicos de la aplicación de Teams

Puedes crear aplicaciones personalizadas de Teams para ti, personas de tu organización o personas de todo el mundo. Antes de empezar, debes comprender los siguientes conceptos fundamentales sobre el desarrollo de aplicaciones de Teams:

### <a name="common-app-use-cases"></a>Casos comunes de uso de aplicaciones

Algunos escenarios típicos con los que puede ayudar una aplicación personalizada de Teams son:

* Insertar contenido basado en web, como una aplicación web o parte de un sitio web, en el cliente de Teams
* Buscar información rápidamente en otro sistema y agregarla a una conversación de Teams 
* Desencadenar flujos de trabajo y procesos directamente desde lo que se dice en una conversación 

### <a name="app-capabilities-and-tools"></a>Herramientas y funcionalidades de la aplicación

Una aplicación está integrada por una o más capacidades de Teams y puntos de interacción del usuario. El conjunto de herramientas de desarrollo variará en función de las capacidades que desee.

| **Capacidades de la aplicación**| **Puntos de interacción** | **Herramientas recomendadas** | **SDK** | **Pilas de tecnología** |
|--------|--------|--------|--------|--------|
| Pestañas | Espacios donde los usuarios pueden interactuar con contenido web incrustado en contextos personales y compartidos | VS Code with Teams Toolkit extension or Yeoman Generator | SDK para cliente de JavaScript en Teams | Tecnologías web generales (HTML, CSS y JavaScript) o React.js |
| Bots | Chatbots que interactúan con usuarios en contextos personales y compartidos | VS Code with Teams Toolkit extension or Yeoman Generator | Bot Franework SDK | Node.js, C# o Python | 
| Extensiones de mensajería | Accesos directos para insertar contenido de la aplicación o actuar en un mensaje sin salir de la conversación | VS Code with Teams Toolkit extension or Yeoman Generator | Bot Framework SDK | Node.js, C# o Python |

### <a name="teams-doesnt-host-your-app"></a>Teams no hospeda la aplicación

Cuando un usuario instala la aplicación en Teams, solo instala un paquete de aplicación que contiene un archivo de configuración (también conocido como un manifiesto de la aplicación) y los iconos de la aplicación. La lógica y el almacenamiento de datos de la aplicación se hospedan en otro lugar, como Azure Web Services o localhost durante el desarrollo. Teams tiene acceso a estos recursos a través de HTTPS.

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="La ilustración que muestra la aplicación en Teams apunta a la lógica de la aplicación en el servidor en la nube.":::

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear y ejecutar la primera aplicación de Teams](../build-your-first-app/build-and-run.md)

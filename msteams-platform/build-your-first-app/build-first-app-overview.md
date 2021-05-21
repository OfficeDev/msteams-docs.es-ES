---
title: 'Introducción: crear la primera introducción a la aplicación y los requisitos previos'
author: girliemac
description: Obtén información sobre cómo empezar a usar Microsoft Teams desarrollo de aplicaciones y configurar el entorno.
ms.author: timura
ms.date: 03/18/2021
ms.topic: quickstart
ms.openlocfilehash: dae942be9383ef1e0a931d238e6148651f334ef5
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565882"
---
# <a name="get-started-with-microsoft-teams-app-development"></a>Introducción al desarrollo Microsoft Teams aplicaciones

Crea una aplicación sencilla para aprender los conceptos básicos de Teams desarrollo de aplicaciones. Una vez que veas "Hello, World!", prueba cualquiera de los otros artículos de introducción para obtener más información sobre herramientas comunes, conceptos fundamentales y características avanzadas.



## <a name="what-youll-learn"></a>Lo que aprenderás

* Se ejecuta rápidamente con el Teams Toolkit, una Visual Studio Code extensión. 
* Configura la aplicación con App Studio.
* Familiarícese con Teams y SDK para desarrolladores.
* Ten en cuenta Teams conceptos de aplicación, como la autenticación y los procedimientos recomendados de diseño.

Puedes crear una aplicación Teams con cualquier tecnología que prefieras, por ejemplo, la interfaz de línea de comandos (CLI). Sin embargo, estos artículos le ayudan a empezar con las siguientes herramientas y tecnologías recomendadas:

* Teams Toolkit, una Visual Studio Code extensión
* React.js para pestañas
* Node.js para bots y extensiones de mensajería


## <a name="teams-app-fundamentals"></a>Teams fundamentales de la aplicación

Puedes crear aplicaciones de Teams personalizadas para ti, personas de tu organización o personas de todo el mundo. Antes de comenzar, debes comprender los siguientes conceptos fundamentales sobre el Teams de aplicaciones:

### <a name="common-app-use-cases"></a>Casos comunes de uso de aplicaciones

Algunos escenarios típicos con los que una aplicación Teams personalizada puede ayudar son:

* Inserte contenido basado en web, como una aplicación web o parte de un sitio web, en el Teams cliente.
* Busque información rápidamente en otro sistema y adición a una Teams conversación.
* Desencadenar flujos de trabajo y procesos directamente desde lo que se dice en una conversación.

### <a name="app-capabilities-and-tools"></a>Herramientas y funcionalidades de la aplicación

Una aplicación está integrada por uno o más Teams capacidades y puntos de interacción del usuario. El conjunto de herramientas de desarrollo variará en función de las capacidades que desee.

| **Funcionalidades de la aplicación**| **Puntos de interacción** | **Herramientas recomendadas** | **SDK** | **Pilas de tecnología** |
|--------|--------|--------|--------|--------|
| Pestañas | Espacios donde los usuarios pueden interactuar con el contenido web incrustado en contextos personales y compartidos. | VS Code con Teams Toolkit o generador de Yeoman | SDK para cliente de JavaScript en Teams | Tecnologías web generales (HTML, CSS y JavaScript) o React.js |
| Bots | Bots de chat que interactúan con usuarios en contextos personales y compartidos. | VS Code con Teams Toolkit o generador de Yeoman | Bot Framework SDK | Node.js, C# o Python | 
| Extensiones de mensajería | Accesos directos para insertar contenido de la aplicación o actuar en un mensaje sin salir de la conversación. | VS Code con Teams Toolkit o generador de Yeoman | Bot Framework SDK | Node.js, C# o Python |

### <a name="teams-doesnt-host-your-app"></a>Teams no hospeda la aplicación

Cuando un usuario instala la aplicación en Teams, solo instala un paquete de aplicación que contiene un archivo de configuración (también conocido como manifiesto de aplicación) y los iconos de la aplicación. La lógica y el almacenamiento de datos de la aplicación se hospedan en otro lugar, como Azure Web Services o localhost durante el desarrollo. Teams accede a estos recursos a través de HTTPS.

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="La ilustración que muestra la aplicación en Teams está apuntando a la lógica de la aplicación en el servidor en la nube.":::

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Compilación y ejecución de la primera Teams aplicación](../build-your-first-app/build-and-run.md)

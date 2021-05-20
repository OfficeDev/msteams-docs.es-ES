---
title: 'Introducción: cree la primera descripción general de la aplicación y requisitos previos'
author: girliemac
description: Obtén información sobre cómo empezar a usar Microsoft Teams desarrollo de aplicaciones y configurar tu entorno.
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
# <a name="get-started-with-microsoft-teams-app-development"></a>Comience con el desarrollo de aplicaciones Microsoft Teams

Cree una aplicación sencilla para aprender los conceptos básicos del desarrollo de Teams aplicación. Una vez que veas "¡Hola, Mundo!", prueba cualquiera de los otros artículos de introducción para obtener más información sobre herramientas comunes, conceptos fundamentales y características avanzadas.



## <a name="what-youll-learn"></a>Lo que aprenderás

* Ponte en marcha rápidamente con el Teams Toolkit, una extensión Visual Studio Code. 
* Configure la aplicación con App Studio.
* Familiarícese con Teams herramientas de desarrollo y SDK.
* Considere la posibilidad de importantes Teams conceptos de aplicación, como la autenticación y las prácticas recomendadas de diseño.

Puede crear una aplicación Teams utilizando cualquier tecnología de su elección, por ejemplo, la interfaz de línea de comandos (CLI). Sin embargo, estos artículos le ayudan a empezar con las siguientes herramientas y tecnologías recomendadas:

* Teams Toolkit, una extensión de Visual Studio Code
* React.js para pestañas
* Node.js para bots y extensiones de mensajería


## <a name="teams-app-fundamentals"></a>Teams fundamentos de la aplicación

Puedes crear aplicaciones de Teams personalizadas para ti, personas en tu organización o personas de todo el mundo. Antes de empezar, debe comprender los siguientes conceptos fundamentales sobre Teams desarrollo de aplicaciones:

### <a name="common-app-use-cases"></a>Casos comunes de uso de aplicaciones

Algunos escenarios típicos con los que una aplicación de Teams personalizada puede ayudar son:

* Incrustar contenido basado en web, como una aplicación web o parte de un sitio web, en el cliente Teams.
* Busque información rápidamente en otro sistema y agregársela a una conversación Teams.
* Desencadene flujos de trabajo y procesos directamente desde lo que se dice en una conversación.

### <a name="app-capabilities-and-tools"></a>Capacidades y herramientas de la aplicación

Una aplicación se compone de una o más capacidades Teams y puntos de interacción del usuario. El conjunto de herramientas de desarrollo variará en función de las capacidades que desee.

| **Capacidades de la aplicación**| **Puntos de interacción** | **Herramientas recomendadas** | **SDK** | **Pilas tecnológicas** |
|--------|--------|--------|--------|--------|
| Pestañas | Espacios donde los usuarios pueden interactuar con contenido web incrustado en contextos personales y compartidos. | VS Code con extensión de Teams Toolkit o generador Yeoman | SDK para cliente de JavaScript en Teams | Tecnologías web generales (HTML, CSS y JavaScript) o React.js |
| Bots | Chatbots que interactúan con los usuarios en contextos personales y compartidos. | VS Code con extensión de Teams Toolkit o generador Yeoman | Bot Framework SDK | Node.js, C#o Python | 
| Extensiones de mensajería | Accesos directos para insertar contenido de la aplicación o actuar en un mensaje sin navegar lejos de la conversación. | VS Code con extensión de Teams Toolkit o generador Yeoman | Bot Framework SDK | Node.js, C#o Python |

### <a name="teams-doesnt-host-your-app"></a>Teams no aloja la aplicación

Cuando un usuario instala la aplicación en Teams, solo instala un paquete de aplicación que contiene un archivo de configuración (también conocido como manifiesto de aplicación) y los iconos de la aplicación. La lógica y el almacenamiento de datos de la aplicación se hospedan en otro lugar, como Azure Web Services o localhost durante el desarrollo. Teams accede a estos recursos a través de HTTPS.

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="Ilustración que muestra la aplicación en Teams apunta a la lógica de la aplicación en el servidor en la nube.":::

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Compila y ejecuta tu primera aplicación de Teams](../build-your-first-app/build-and-run.md)

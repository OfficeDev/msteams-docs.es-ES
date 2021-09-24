---
title: Ejemplos de código de aplicación
description: Vínculos y descripciones de aplicaciones de ejemplo para la Microsoft Teams de desarrolladores
ms.localizationpriority: medium
ms.topic: reference
keywords: Microsoft Teams de desarrolladores
ms.openlocfilehash: 34c914898f7ae83022f1278bc11cc33ac5084ba5
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157338"
---
# <a name="overview"></a>Información general

En este tutorial, aprenderás a crear una aplicación con React, Blazor, SPFx, C# o .NET, Node.js y generador de Yeoman. También aprenderás a crear tu primer bot y la extensión de mensajería. Este tutorial te llevará a través de varios ejemplos de código para pestañas, bots, extensiones de mensajería, webhooks y conectores y API de Graph que te ayudarán a personalizar y configurar tus aplicaciones. Además, también puedes consultar las secciones de Microsoft Learn donde puedes ampliar las capacidades de la plataforma Teams desarrolladores mediante la creación de aplicaciones personalizadas.  

## <a name="getting-started-with-microsoft-learn"></a>Introducción a Microsoft Learn

| **Funcionalidad**| **Módulo Learn**|
|--------|-------------|
| Pestañas: experiencias web incrustadas  |  [Crear experiencias web integradas con pestañas para Microsoft Teams](/learn/modules/embedded-web-experiences/) |
| Webhooks y conectores  |  [Conectar servicios web a Microsoft Teams con webhooks y conectores de Office 365](/learn/modules/msteams-webhooks-connectors/) |
|Extensiones de mensajería  | [Interacciones orientadas a tareas en Microsoft Teams con las extensiones de mensajería](/learn/modules/msteams-messaging-extensions/)  |
| Módulos de tareas |  [Recopilar entradas en Microsoft Teams módulos de tareas](/learn/modules/msteams-task-modules/) |
| Bots conversacionales  | [Crear robots de conversación interactivos para Microsoft Teams](/learn/modules/msteams-conversation-bots/)  |

## <a name="build-your-first-microsoft-teams-app-overview"></a>Crear la primera introducción Microsoft Teams aplicación

En las **lecciones de introducción,** aprenderás a crear aplicaciones Teams básicas. Cada tutorial explica cómo crear una aplicación sencilla y real Teams a la vez que te presenta herramientas comunes, conceptos fundamentales y características más avanzadas.

### <a name="teams-app-fundamentals"></a>Teams fundamentales de la aplicación

La [Teams para desarrolladores](../overview.md) te permite crear aplicaciones personalizadas. Algunos escenarios comunes con los que puede ayudar una aplicación personalizada de Microsoft Teams son los siguientes:

* Inserte su sitio web o aplicación web directamente en el cliente de Teams.
* Ayude a los usuarios a buscar rápidamente información en otro sistema y agregar los resultados a una conversación en Teams.
* Desencadene flujos de trabajo y procesos basados en una conversación en Teams, y conserve el contexto de la conversación.

Antes de comenzar los tutoriales, debes saber lo siguiente sobre cómo crear aplicaciones para Teams.

### <a name="app-capabilities"></a>Capacidades de la aplicación

Una aplicación Teams está integrada por una o más [capacidades de plataforma](../concepts/capabilities-overview.md) y puntos [de interacción del usuario.](../concepts/extensibility-points.md)

Dependiendo de las capacidades que quieras para tu aplicación, necesitarás un conjunto de herramientas de desarrollo adecuado.

| Capacidades de la aplicación | Interacciones del usuario | Herramientas recomendadas | SDK | Pilas de tecnología |
|--------|-------------|--------|--------|--------|
| Pestañas | Una experiencia web incrustada a pantalla completa. | VS Code con Teams Toolkit o YoTeams (generador de Yeoman) | [Teams SDK de cliente](/javascript/api/overview/msteams-client) | Tecnología web en general, HTML, CSS y JavaScript |
| Bots | Bot de chat que conversa con miembros. | VS Code con Teams Toolkit o YoTeams (generador de Yeoman) | [Bot Framework SDK](https://dev.botframework.com/) | Node.js, C# o Python |
| Extensiones de mensajería | Accesos directos para insertar contenido externo en una conversación o realizar acciones en los mensajes. | VS Code con Teams Toolkit o YoTeams (generador de Yeoman) | [Bot Framework SDK](https://dev.botframework.com/) | Node.js, C# o Python |

La sección Introducción le llevará a través de conjuntos de herramientas recomendados y tecnologías de uso común, como Visual Studio Code con extensión Teams, React.js para pestañas y Node.js para bots y extensiones de mensajería, aunque no se limita al uso de estas pilas en *particular.*

Si prefieres usar una interfaz de línea de comandos (CLI), consulta crear la primera aplicación Microsoft Teams [con el generador de Yeoman](../get-started/get-started-yeoman.md).

### <a name="teams-does-not-host-your-app"></a>Teams no hospeda la aplicación

Solo instalará un paquete de aplicación que contenga un archivo de configuración, denominado iconos de manifiesto y de aplicación para Teams cliente. El resto de las lógicas de la aplicación y el almacenamiento de datos se hospedan en otro lugar, como Azure Web Services. La aplicación en la nube o localhost durante el desarrollo accede Teams mediante HTTPS.

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="La ilustración que muestra la aplicación en Teams está apuntando a la lógica de la aplicación en el servidor en la nube.":::

## <a name="see-also"></a>Vea también

* [Crear una aplicación con React](first-app-react.md)
* [Crear una aplicación con Blazor](first-app-blazor.md)
* [Crear una aplicación con SPFx](first-app-spfx.md)
* [Crear una aplicación con C# o .NET](get-started-dotnet-app-studio.md)
* [Crear una aplicación con Node.js](get-started-nodejs-app-studio.md)
* [Crear una aplicación con el generador de Yeoman](get-started-yeoman.md)
* [Crear una aplicación de bots de conversación](first-app-bot.md)
* [Crear una extensión de mensajería](first-message-extension.md)
* [Muestras de código](https://github.com/OfficeDev/Microsoft-Teams-Samples)

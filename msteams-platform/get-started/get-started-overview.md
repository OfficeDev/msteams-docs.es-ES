---
title: 'Introducción: Información general'
description: Introducción a Introducción a la documentación Microsoft Teams para desarrolladores
ms.localizationpriority: medium
ms.topic: reference
keywords: Microsoft Teams de desarrolladores
ms.openlocfilehash: ee986f04ca760fbf9090f7dda94e1378261db7df
ms.sourcegitcommit: e45742fd2aa2ff5e5c15e8f7c20cc14fbef6d441
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2021
ms.locfileid: "61075482"
---
# <a name="get-started"></a>Introducción

Bienvenido a Introducción para crear e implementar aplicaciones personalizadas para Microsoft Teams!

Siga los pasos para crear una aplicación básica y real Teams aplicación. La introducción también le presenta herramientas comunes, conceptos fundamentales y características más avanzadas.

Esta es una idea de lo que aprenderá:

- Se ejecuta rápidamente con el Microsoft Teams Toolkit (una Visual Studio Code extensión).
- Obtenga experiencia con los Toolkit y SDK.
- Configure y cree diferentes tipos de Teams aplicaciones.

Echemos un vistazo rápido a las opciones del entorno de compilación entre las que puedes elegir y la hoja de ruta para crear e implementar una Teams aplicación.

:::image type="content" source="../assets/images/get-started/gs-build-options.png" alt-text="Ilustración que muestra los pasos básicos para crear e implementar una Teams aplicación.":::

## <a name="app-capabilities-and-development-tools"></a>Funcionalidades de aplicaciones y herramientas de desarrollo

En función de las capacidades que quieras para la aplicación, elige un conjunto de herramientas de desarrollo adecuado.

| Capacidades de la aplicación | Interacciones del usuario | Herramientas recomendadas | SDK | Pilas de tecnología / idiomas |
|--------|-------------|--------|--------|--------|
| Pestañas | Una experiencia web incrustada a pantalla completa. | VS Code con Teams Toolkit o CLI de [TeamsFx](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) si prefiere usar la CLI | [SDK de TeamsFx](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) para libs principales [y SDK Teams cliente para](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) funcionalidades de interfaz de usuario | Tecnología web en general, HTML, CSS y JavaScript (incluido React). |
| Bots | Bot de chat que conversa con miembros. | VS Code con Teams Toolkit o cli [de TeamsFx](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | [SDK de TeamsFx](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) y [SDK de Bot Framework](https://dev.botframework.com/) | Node.js, C#, Java y Python. |
| Extensiones de mensajería | Accesos directos para insertar contenido externo en una conversación o realizar acciones en los mensajes. | VS Code con Teams Toolkit o cli [de TeamsFx](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | [SDK de TeamsFx](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) y [SDK de Bot Framework](https://dev.botframework.com/) | Node.js, C#, Java y Python. |

*No estás limitado a usar estas pilas en particular.*

Si ya estás familiarizado con el flujo de trabajo de Yeoman, es posible que prefieras usar [YoTeams Yeoman Generator](https://github.com/pnp/generator-teams/blob/master/docs/docs/tutorials/build-your-first-microsoft-teams-app.md) para crear tus aplicaciones.

> [!NOTE]
> Si has estado usando App Studio, te recomendamos que pruebes el Portal de desarrolladores para configurar, distribuir y administrar tus aplicaciones Teams aplicaciones.


## <a name="build-your-first-teams-app"></a>Crear la primera Teams aplicación

Ahora, vamos a crear la primera Teams aplicación. Pero en primer lugar, elija el idioma (o marco) y prepare el entorno de desarrollo.

> [!div class="nextstepaction"]
> [Crear una aplicación Teams con JavaScript mediante React](../sbs-gs-javascript.yml)

> [!div class="nextstepaction"]
> [Crear una aplicación Teams con SPFx](../sbs-gs-spfx.yml)

> [!div class="nextstepaction"]
> [Crear una aplicación Teams con C# o .NET](../sbs-gs-csharp.yml)

> [!div class="nextstepaction"]
> [Crear una aplicación Teams con Node.js](../sbs-gs-nodejs.yml)

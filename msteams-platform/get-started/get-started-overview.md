---
title: 'Introducción: Información general'
description: Empiece. Compile su primera aplicación de Microsoft Teams en función del lenguaje (Node.js, C#, Java, Python) y el entorno de desarrollo, comprenda las funcionalidades de la aplicación y los SDK.
ms.localizationpriority: high
ms.topic: reference
ms.openlocfilehash: 4ad64240c97ab11da6a999f87621fdff6d70ebe2
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100437"
---
# <a name="get-started"></a>Introducción

Le damos la bienvenida a Introducción para crear e implementar aplicaciones personalizadas para Microsoft Teams.

Siga los pasos para crear una aplicación básica de Teams en el mundo real. La Introducción también le presenta herramientas comunes, conceptos fundamentales y características más avanzadas.

Aquí tiene una idea de lo que aprenderá:

- Póngase en marcha rápidamente con el kit de herramientas de Microsoft Teams (una extensión de Visual Studio Code).
- Obtenga experiencia con el kit de herramientas y SDK.
- Configure y cree diferentes tipos de aplicaciones de Teams.

Echemos un rápido vistazo a las opciones de entorno de compilación que puede elegir, y a la hoja de ruta para construir e implementar una aplicación de Teams.

:::image type="content" source="../assets/images/get-started/gs-build-options.png" alt-text="Ilustración en la que se muestran los pasos básicos para compilar e implementar una aplicación de Teams":::

## <a name="app-capabilities-and-development-tools"></a>Funcionalidades de aplicaciones y herramientas de desarrollo

En función de las capacidades que quiera para la aplicación, elija un conjunto de herramientas de desarrollo adecuado.

| Capacidades de la aplicación | Interacciones del usuario | Herramientas recomendadas | SDK | Pilas de tecnología / idiomas |
|--------|-------------|--------|--------|--------|
| Pestañas | Una experiencia web incorporada en pantalla completa. | Microsoft Visual Studio Code con la extensión Kit de herramientas de Teams o [CLI de TeamsFx](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) si prefiere usar CLI | [SDK TeamsFx](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) para bibliotecas principales y [SDK de cliente de Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) para funcionalidades de interfaz de usuario | Tecnología web en general, HTML, CSS y JavaScript (incl. React). |
| Bots | Un bot de chat que se comunica con los miembros. | Visual Studio Code con la extensión Kit de herramientas de Teams o [CLI TeamsFx](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | [SDK TeamsFx](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) y [SDK de Bot Framework](https://dev.botframework.com/) | Node.js, C#, Java y Python. |
| Extensiones de mensajes | Métodos abreviados de teclado para insertar contenido externo en una conversación o realizar acciones en los mensajes. | Visual Studio Code con la extensión Kit de herramientas de Teams o [CLI TeamsFx](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | [SDK TeamsFx](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) y [SDK de Bot Framework](https://dev.botframework.com/) | Node.js, C#, Java y Python. |

*No está limitado al uso de estas pilas concretas.*

Si ya está familiarizado con el flujo de trabajo de Yeoman, puede que prefiera usar [Generador Yeoman YoTeams](https://github.com/pnp/generator-teams/blob/master/docs/docs/tutorials/build-your-first-microsoft-teams-app.md) para crear las aplicaciones.

## <a name="build-your-first-teams-app"></a>Crear la primera aplicación de Teams

Ahora, vamos a crear su primera aplicación de Teams. Pero primero, elija su idioma (o marco de trabajo) y prepare su entorno de desarrollo.

> [!div class="nextstepaction"]
> [Crear una aplicación de pestaña de Teams con JavaScript mediante React](../sbs-gs-javascript.yml)
> [!div class="nextstepaction"]
> [Crear una aplicación de bot de Teams con JavaScript](../sbs-gs-bot.yml)
> [!div class="nextstepaction"]
> [Crear una aplicación de extensión de mensajería de Teams con JavaScript mediante React](../sbs-gs-msgext.yml)
> [!div class="nextstepaction"]
> [Crear una aplicación de Teams con Blazor](../sbs-gs-blazorupdate.yml)
> [!div class="nextstepaction"]
> [Crear una aplicación Teams con SPFx](../sbs-gs-spfx.yml)
> [!div class="nextstepaction"]
> [Crear una aplicación Teams con C# o .NET](../sbs-gs-csharp.yml)
> [!div class="nextstepaction"]
> [Crear una aplicación Teams con Node.js](../sbs-gs-nodejs.yml)
> [!div class="nextstepaction"]
> [Crear un bot de notificaciones con JavaScript](../sbs-gs-notificationbot.yml)
> [!div class="nextstepaction"]
> [Crear un bot de comandos con JavaScript](../sbs-gs-commandbot.yml)
> [!div class="nextstepaction"]

## <a name="see-also"></a>Vea también

- [Ejemplos de Microsoft Teams](https://github.com/OfficeDev/Microsoft-Teams-Samples#microsoft-teams-samples)
- [Recursos de Git y GitHub](/contribute/additional-resources)

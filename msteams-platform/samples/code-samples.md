---
title: Ejemplos de código de Microsoft Teams
description: Vínculos y descripciones de aplicaciones de ejemplo para la plataforma de desarrolladores de Microsoft Teams
keywords: Ejemplos para desarrolladores de Microsoft Teams
ms.openlocfilehash: eb7794e788f8eb39102ac874748e23d8621f281e
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675695"
---
# <a name="code-samples-for-the-microsoft-teams-developer-platform"></a>Ejemplos de código para la plataforma de desarrolladores de Microsoft Teams

Aquí encontrará una lista de ejemplos de código que muestran varias capacidades de la plataforma de desarrollo de Microsoft Teams y cómo crear aplicaciones para aprovechar dichas características.

## <a name="getting-samples"></a>Obtener ejemplos

Para descargar nuestros ejemplos de GitHub:

1. Seleccione uno de los proyectos que aparecen a continuación y abra el proyecto en GitHub.
2. Elija el botón **clonar o descargar** y copie la dirección URL.
3. Abra un símbolo del sistema en el directorio principal en el que desea instalar el proyecto de ejemplo
4. Realizar`git clone <pasted url>`

### <a name="for-netc-samples"></a>Para ejemplos de .NET/C#

Cada uno de nuestros ejemplos de .NET incluye un archivo de solución de Visual Studio que puede compilar la solución por completo, incluida la restauración de los paquetes NuGet.

### <a name="for-nodejs-samples"></a>Ejemplos de node. js

Se proporciona un archivo packages. JSON que enumera todos los paquetes necesarios para un ejemplo. Simplemente ejecute `npm install` desde la línea de comandos en el directorio del proyecto node. js para instalar los paquetes necesarios. Ya está listo para abrir el proyecto en Visual Studio Code y comenzar a experimentar.

### <a name="for-other-samples"></a>Para ver otros ejemplos

Como siempre, el archivo Léame del proyecto debe tener más información sobre necesidades específicas para ejemplos específicos.

## <a name="get-started"></a>Introducción

| Muestra | Descripción|
|--------|-------------|
| [Hola a todos en Microsoft Teams con node. js](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) | Una aplicación de Teams `Node.js` de muestra que le presenta las funcionalidades básicas de la aplicación.|
| [Hola a todos en Microsoft Teams con C# .NET](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) | Una aplicación de Teams `C# .NET` de muestra que le presenta las funcionalidades básicas de la aplicación.|
| [Introducción al generador de Yeoman para Teams](~/tutorials/get-started-yeoman.md) | Cree una aplicación de Teams desde el principio con el generador de Yeoman para Microsoft Teams. |

## <a name="bots-using-the-v4-sdk"></a>Bots (mediante el SDK de V4)

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## <a name="messaging-extensions-using-the-v4-sdk"></a>Extensiones de mensajería (mediante el SDK de V4)

| Muestra | Descripción | .NET Core | JavaScript |
|--------|------------- |---|---|
| Comando Buscar | Extensión de mensajería simple con un comando de búsqueda | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)| [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|
| Comando de acción | Extensión de mensajería simple con un comando de acción. Respuesta insertada en el área de mensaje de redacción. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)|
| Comando de acción con respuesta de bot | Extensión de mensajería con un comando de acción. Respuesta insertada en la conversación por el bot. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/53.teams-messaging-extensions-action-preview)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/53.teams-messaging-extensions-action-preview)|
| Comando Buscar | extensión de mensajería con un comando de búsqueda y autenticación y configuración | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)| [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)|

## <a name="outgoing-webhooks"></a>Webhooks salientes

| Muestra | Descripción
|--------|-------------
| [Webhook de salida para C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook) | Ilustra cómo crear un **webhook de salida** para Microsoft Teams en C#/.net.
| [Webhook de salida para node. js](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs) | Ilustra cómo crear un **webhook de salida** sencillo para Microsoft Teams en un ~ 50 líneas de código de node. js.

## <a name="connectors"></a>Conectores

| Muestra | Descripción
|--------|-------------
| [Conector de ejemplo para node. js](https://github.com/OfficeDev/microsoft-teams-sample-connector-nodejs) | Este ejemplo, escrito en node. js, describe cómo crear un conector para Microsoft Teams mediante GitHub como ejemplo para generar notificaciones de conector.
| [Conector de ejemplo para C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-connector-csharp) | Este ejemplo, escrito en C#, muestra cómo crear un conector para Microsoft Teams con una aplicación de lista de tareas de ejemplo como ejemplo para generar notificaciones de conector.

## <a name="graph-api"></a>API de Graph

| Muestra | Descripción
|--------|-------------
| [Ejemplos de la API de Microsoft Graph](https://github.com/OfficeDev/microsoft-teams-sample-graph) | Estos ejemplos muestran el uso de llamadas a la API de Microsoft Graph para realizar tareas como la consulta de equipos y canales desde un servicio Web que se ejecuta fuera de Microsoft Teams.

## <a name="others"></a>Otros

| Código | Descripción |
|------|------------- |
| [Ejemplo completo en node. js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) | En este ejemplo se muestra cómo usar todas las características de la plataforma de Microsoft Teams. Nota: en este ejemplo se usa el SDK de bot Framework V3.|
| [Ejemplo completo en C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) | En este ejemplo se muestra cómo usar todas las características de la plataforma de Microsoft Teams. Nota: en este ejemplo se usa el SDK de bot Framework V3. |
| [Aplicaciones de línea de negocio en C#/.NET](https://github.com/OfficeDev/msteams-sample-line-of-business-apps-csharp) | Este repositorio contiene varios ejemplos de aplicaciones de línea de negocio que se pueden usar para inspiración o como plantillas para crear en la parte superior de. Nota: en estos ejemplos se usa el SDK de bot Framework V3.|
| [Aplicación de pestañas de muestra de lista "tareas pendientes"](https://github.com/OfficeDev/microsoft-teams-sample-todo) | En este ejemplo de node. js se muestra lo fácil que es convertir una aplicación web existente en una pestaña. |
| [Orky](https://github.com/OfficeDev/Orky) | Puede usar Orky para registrar su bot? n local propio en Microsoft Teams y ejecutar scripts desde cualquier lugar. |
| [Tiempo de compilación 2017](https://github.com/OfficeDev/microsoft-teams-build2017-weather) | Obsoleta. Código fuente para la sesión de//Build 2017 para agregar una ficha Meteorología a la aplicación esqueleto generada anteriormente en la sesión. |

### <a name="bot-framework-sdk-v3-samples"></a>Ejemplos del SDK de bot Framework V3

| Muestra | Descripción |
|--------|------------- |
| [Ejemplo de bot para C#/.NET](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/CSharp/Samples/Microsoft.Bot.Connector.Teams.SampleBot) | Ejemplos de bot Framework V3|
| [Bot de ejemplo para node. js](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/Node/samples) | Ejemplos de bot Framework V3 |

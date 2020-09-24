---
title: Ejemplos de código de Microsoft Teams
description: Vínculos y descripciones de aplicaciones de ejemplo para la plataforma de desarrolladores de Microsoft Teams
keywords: Ejemplos para desarrolladores de Microsoft Teams
ms.openlocfilehash: 7a81494d7808c27c495c660b5d58f7779ba87c83
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237961"
---
# <a name="tutorials-and-code-samples-for-the-microsoft-teams-developer-platform"></a>Tutoriales y ejemplos de código para la plataforma de desarrolladores de Microsoft Teams

Aquí encontrará una lista de tutoriales y ejemplos de código que muestran cómo se pueden ampliar las capacidades de la plataforma de desarrollo de Teams mediante la creación de aplicaciones personalizadas.

## <a name="getting-started-with-microsoft-learn"></a>Introducción a Microsoft Learn

| Funcionalidad| Módulo de aprendizaje|
|--------|-------------|
| Pestañas: experiencias Web integradas  |  [Crear experiencias Web insertadas con pestañas para Microsoft Teams](https://docs.microsoft.com/learn/modules/embedded-web-experiences/) |
| Webhooks y conectores  |  [Conexión de servicios web a Microsoft Teams con webhooks y conectores de Office 365](https://docs.microsoft.com/learn/modules/msteams-webhooks-connectors/) |
|Extensiones de mensajería  | [Interacciones orientadas a tareas en Microsoft Teams con extensiones de mensajería](https://docs.microsoft.com/learn/modules/msteams-messaging-extensions/)  |
| Módulos de tareas |  [Recopilar datos en Microsoft Teams con módulos de tareas](https://docs.microsoft.com/learn/modules/msteams-task-modules/) |
| Bots de conversación  | [Crear bots interactivos de conversación para Microsoft Teams](https://docs.microsoft.com/learn/modules/msteams-conversation-bots/)  |

## <a name="getting-started-with-code-samples"></a>Introducción a los ejemplos de código

Para descargar nuestros ejemplos de GitHub:

1. Seleccione uno de los proyectos que aparecen a continuación y abra el proyecto en GitHub.
2. Elija el botón **clonar o descargar** y copie la dirección URL.
3. Abra un símbolo del sistema en el directorio principal en el que desea instalar el proyecto de ejemplo
4. Realizar `git clone <pasted url>`

### <a name="for-netc-samples"></a>Para ejemplos de .NET/C#

Cada uno de nuestros ejemplos de .NET incluye un archivo de solución de Visual Studio que puede compilar la solución por completo, incluida la restauración de los paquetes NuGet.

### <a name="for-nodejs-samples"></a>Para obtener ejemplos de Node.js

Se proporciona un packages.jsen el archivo en el que se enumeran todos los paquetes necesarios para obtener un ejemplo. Simplemente ejecute `npm install` desde la línea de comandos en el Node.js directorio del proyecto para instalar los paquetes necesarios. Ya está listo para abrir el proyecto en Visual Studio Code y comenzar a experimentar.

### <a name="for-other-samples"></a>Para ver otros ejemplos

Como siempre, el archivo Léame del proyecto debe tener más información sobre necesidades específicas para ejemplos específicos.

## <a name="bots-using-the-v4-sdk"></a>Bots (mediante el SDK de V4)

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

>[!TIP]
>Visite el [repositorio de ejemplos de bot Framework](https://github.com/Microsoft/BotBuilder-Samples) para ver ejemplos centrados en tareas del SDK de Microsoft bot Framework V4 para C#, JavaScript, TypeScript y Python.

## <a name="messaging-extensions-using-the-v4-sdk"></a>Extensiones de mensajería (mediante el SDK de V4)

| Muestra | Descripción | .NET Core | JavaScript | Python|
|--------|------------- |---|---|----|
| Extensiones de mensajería: búsqueda | Extensión de mensajería que acepta solicitudes de búsqueda y devuelve resultados. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |
| Extensiones de mensajería: acción | Extensión de mensajería que acepta parámetros y devuelve una tarjeta. Además, cómo recibir un mensaje reenviado como parámetro en una extensión de mensajería. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
| Extensiones de mensajería: auth y config | La extensión de mensajería que tiene una página de configuración, acepta solicitudes de búsqueda y devuelve resultados después de que el usuario haya iniciado sesión. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config) |
| Extensiones de mensajería: vista previa de la acción | Muestra cómo crear una vista previa y editar el flujo de una extensión de mensajería. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/53.teams-messaging-extensions-action-preview) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/53.teams-messaging-extensions-action-preview) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/53.teams-messaging-extensions-action-preview) |
| Apertura de vínculos | Extensión de mensajería que realiza unfurling de vínculos. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/55.teams-link-unfurling) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/55.teams-link-unfurling) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/55.teams-link-unfurling) |


## <a name="outgoing-webhooks"></a>Webhooks salientes

| Muestra | Descripción
|--------|-------------
| [Webhook de salida para C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook) | Ilustra cómo crear un **webhook de salida** para Microsoft Teams en C#/.net.
| [Webhook de salida para Node.js](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs) | Ilustra cómo crear un **webhook de salida** sencillo para Microsoft Teams en una ~ 50 líneas de código Node.js.

## <a name="connectors"></a>Conectores

| Muestra | Descripción
|--------|-------------
| [Conector de ejemplo para Node.js](https://github.com/OfficeDev/microsoft-teams-sample-connector-nodejs) | Este ejemplo, escrito en Node.js, muestra cómo crear un conector para Microsoft Teams mediante GitHub como ejemplo para generar notificaciones de conector.
| [Conector de ejemplo para C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-connector-csharp) | Este ejemplo, escrito en C#, muestra cómo crear un conector para Microsoft Teams con una aplicación de lista de tareas de ejemplo como ejemplo para generar notificaciones de conector.

## <a name="graph-api"></a>API de Graph

| Muestra | Descripción
|--------|-------------
| [Ejemplos de la API de Microsoft Graph](https://github.com/OfficeDev/microsoft-teams-sample-graph) | Estos ejemplos muestran el uso de llamadas a la API de Microsoft Graph para realizar tareas como la consulta de equipos y canales desde un servicio Web que se ejecuta fuera de Microsoft Teams.

### <a name="bot-framework-sdk-v3-samples"></a>Ejemplos del SDK de bot Framework V3

| Muestra | Descripción |
|--------|------------- |
| [Ejemplo de bot para C#/.NET](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/CSharp/Samples/Microsoft.Bot.Connector.Teams.SampleBot) | Ejemplos de bot Framework V3|
| [Bot de ejemplo para Node.js](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/Node/samples) | Ejemplos de bot Framework V3 |

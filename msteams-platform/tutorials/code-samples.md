---
title: Ejemplos de código de aplicación
description: Vínculos y descripciones de aplicaciones de ejemplo para la plataforma para desarrolladores de Microsoft Teams
ms.topic: reference
keywords: Ejemplos de desarrolladores de Microsoft Teams
ms.openlocfilehash: f51ffb22a5e6b3b757d1971422adf955d95fb223
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014113"
---
# <a name="tutorials-and-code-samples-for-the-microsoft-teams-developer-platform"></a>Tutoriales y ejemplos de código para la plataforma para desarrolladores de Microsoft Teams

Aquí encontrará una lista de tutoriales y ejemplos de código que muestran cómo puede ampliar las capacidades de la plataforma de desarrolladores de Teams mediante la creación de aplicaciones personalizadas.

## <a name="getting-started-with-microsoft-learn"></a>Introducción a Microsoft Learn

| Funcionalidad| Módulo learn|
|--------|-------------|
| Pestañas: experiencias web incrustadas  |  [Crear experiencias web incrustadas con pestañas para Microsoft Teams](https://docs.microsoft.com/learn/modules/embedded-web-experiences/) |
| Webhooks y conectores  |  [Conectar servicios web a Microsoft Teams con webhooks y conectores de Office 365](https://docs.microsoft.com/learn/modules/msteams-webhooks-connectors/) |
|Extensiones de mensajería  | [Interacciones orientadas a tareas en Microsoft Teams con extensiones de mensajería](https://docs.microsoft.com/learn/modules/msteams-messaging-extensions/)  |
| Módulos de tareas |  [Recopilar entradas en Microsoft Teams con módulos de tareas](https://docs.microsoft.com/learn/modules/msteams-task-modules/) |
| Bots conversacionales  | [Crear bots interactivos conversacionales para Microsoft Teams](https://docs.microsoft.com/learn/modules/msteams-conversation-bots/)  |

## <a name="getting-started-with-code-samples"></a>Introducción a los ejemplos de código

Para descargar nuestros ejemplos desde GitHub:

1. Seleccione uno de los proyectos que aparecen a continuación y abra el proyecto en GitHub.
2. Elija el **botón Clonar o descargar** y copie la dirección URL
3. Abra un símbolo del sistema en el directorio primario en el que desea instalar el proyecto de ejemplo
4. Ejecutar `git clone <pasted url>`

### <a name="for-netc-samples"></a>Para ejemplos de .NET/C#

Cada uno de nuestros ejemplos de .NET incluye un Visual Studio de solución que puede compilar la solución por completo, incluida la restauración de los paquetes NuGet.

### <a name="for-nodejs-samples"></a>Para Node.js ejemplos

Proporcionamos una packages.jsen el archivo que enumera todos los paquetes necesarios para un ejemplo. Simplemente ejecute `npm install` desde la línea de comandos del Node.js del proyecto para instalar los paquetes necesarios. Ya estás listo para abrir el proyecto en Visual Studio código y empezar a experimentar.

### <a name="for-other-samples"></a>Para otras muestras

Como siempre, el archivo README del proyecto debe tener más información sobre las necesidades específicas de muestras específicas.

## <a name="bots-using-the-v4-sdk"></a>Bots (con el SDK de v4)

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

>[!TIP]
>Visite el [repositorio de ejemplos de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples) para ver ejemplos centrados en tareas del SDK de Microsoft Bot Framework v4 para C#, JavaScript, TypeScript y Python.

## <a name="messaging-extensions-using-the-v4-sdk"></a>Extensiones de mensajería (con el SDK de v4)

| Muestra | Descripción | .NET Core | JavaScript | Python|
|--------|------------- |---|---|----|
| Extensiones de mensajería: búsqueda | Extensión de mensajería que acepta solicitudes de búsqueda y devuelve resultados. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |
| Extensiones de mensajería: acción | Extensión de mensajería que acepta parámetros y devuelve una tarjeta. Además, cómo recibir un mensaje reenviado como parámetro en una extensión de mensajería. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
| Extensiones de mensajería: autenticación y configuración | Extensión de mensajería que tiene una página de configuración, acepta solicitudes de búsqueda y devuelve resultados después de que el usuario haya iniciado sesión. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config) |
| Extensiones de mensajería: vista previa de la acción | Muestra cómo crear un flujo de vista previa y edición para una extensión de mensajería. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/53.teams-messaging-extensions-action-preview) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/53.teams-messaging-extensions-action-preview) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/53.teams-messaging-extensions-action-preview) |
| Apertura de vínculos | Extensión de mensajería que realiza el desenlazaje de vínculos. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/55.teams-link-unfurling) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/55.teams-link-unfurling) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/55.teams-link-unfurling) |


## <a name="outgoing-webhooks"></a>Webhooks salientes

| Muestra | Descripción
|--------|-------------
| [Webhook saliente para C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook) | Ilustra cómo crear un **webhook saliente** para Microsoft Teams en C#/.NET.
| [Webhook saliente para Node.js](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs) | Ilustra cómo crear un **webhook** saliente simple para Microsoft Teams en ~50 líneas Node.js código.

## <a name="connectors"></a>Conectores

| Muestra | Descripción
|--------|-------------
| [Conector de ejemplo para Node.js](https://github.com/OfficeDev/microsoft-teams-sample-connector-nodejs) | En este ejemplo, escrito en Node.js, se muestra cómo crear un conector para Microsoft Teams con GitHub como ejemplo para generar notificaciones de conector.
| [Conector de ejemplo para C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-connector-csharp) | En este ejemplo, escrito en C#, se muestra cómo crear un conector para Microsoft Teams con una aplicación de lista de tareas de ejemplo como ejemplo para generar notificaciones de conectores. En este ejemplo también se muestra cómo implementar la funcionalidad de inicio de sesión en la página de configuración del conector. 

## <a name="graph-api"></a>Graph API

| Muestra | Descripción
|--------|-------------
| [Ejemplos de API de Microsoft Graph](https://github.com/OfficeDev/microsoft-teams-sample-graph) | Estos ejemplos muestran el uso de llamadas a la API de Microsoft Graph para realizar tareas como consultar equipos y canales desde un servicio web que se ejecuta fuera de Microsoft Teams.

### <a name="bot-framework-sdk-v3-samples"></a>Ejemplos de SDK de Bot Framework v3

| Muestra | Descripción |
|--------|------------- |
| [Bot de ejemplo para C#/.NET](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/CSharp/Samples/Microsoft.Bot.Connector.Teams.SampleBot) | Ejemplos de Bot Framework v3|
| [Bot de ejemplo para Node.js](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/Node/samples) | Ejemplos de Bot Framework v3 |

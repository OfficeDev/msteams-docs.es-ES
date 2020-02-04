---
title: ¿Qué son los bots de conversación?
author: clearab
description: Información general sobre los bots de conversación en Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 7bde886b67788a355181c83287d999a3bfb9727a
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675832"
---
# <a name="what-are-conversational-bots"></a>¿Qué son los bots de conversación?

Los bots de conversación permiten que los usuarios interactúen con el servicio Web a través de texto, tarjetas interactivas y módulos de tareas. Son increíblemente flexibles: los bots de conversación pueden tener un ámbito de control con pocos comandos sencillos o con asistentes de inteligencia virtual complejos y artificiales y de procesamiento de lenguaje natural. Pueden ser un aspecto de una aplicación más grande o ser completamente independientes.

El GIF siguiente muestra un usuario que conversa con un bot en una conversación de uno a uno mediante tarjetas interactivas y de texto. Buscar la combinación correcta de módulos de tarjetas, texto y tareas es clave para crear un bot útil. No olvide que los bots son mucho más que texto.

![P + f más GIF](~/assets/images/FAQPlusEndUser.gif)

## <a name="what-tasks-are-best-handled-by-bots"></a>¿Qué tareas se controlan mejor mediante bots?

Los bots en Microsoft Teams pueden formar parte de una conversación de uno a uno, de un chat en grupo o de un canal de un equipo. Cada ámbito proporcionará oportunidades y desafíos únicos para el bot conversador.

### <a name="in-a-channel"></a>En un canal

Los canales contienen conversaciones encadenadas entre varias personas, potencialmente muchas personas (actualmente, hasta 2000). Esto proporciona potencialmente a su bot un alcance masivo, pero las interacciones individuales deben ser concisas. Las interacciones de varios torneados tradicionales probablemente no funcionarán correctamente. En su lugar, use tarjetas interactivas o módulos de tareas, o bien, puede mover la conversación a una conversación uno a uno si necesita recopilar mucha información. El bot también tendrá acceso a los mensajes en los que se `@mentioned` encuentra directamente, no puede recuperar mensajes adicionales de la conversación con Microsoft Graph y permisos de nivel de organización elevados.

Algunos escenarios en los que Excel de los bots en un canal son:

* **Notificaciones**, especialmente si proporciona una tarjeta interactiva para que los usuarios tomen información adicional.
* **Escenarios de comentarios** como sondeos y encuestas.
* Interacciones que se pueden resolver en un **ciclo de solicitud/respuesta único**, donde los resultados son útiles para varios miembros de la conversación.
* **Bots sociales/divertidos** : Obtenga una imagen de gato increíbles, elija un ganador de forma aleatoria, etc.

### <a name="in-a-group-chat"></a>En un chat en grupo

Los chats de grupo son conversaciones sin encadenamientos entre tres o más personas. Tienden a tener menos miembros que un canal y son más transitorios. De forma similar a un canal, el bot solo tendrá acceso a los mensajes en `@mentioned` los que esté directamente.

Los escenarios que funcionan bien en un canal suelen funcionar tan bien en un chat en grupo.

### <a name="in-a-one-to-one-chat"></a>En un chat de uno a uno

Esta es la forma tradicional de que un bot de conversación interactúe con un usuario. Pueden habilitar cargas de trabajo increíblemente heterogéneas. P&los bots, bots que inician flujos de trabajo en otros sistemas, bots que indican chistes y bots que toman notas son solo algunos ejemplos. No olvide tener en cuenta si una interfaz basada en conversaciones es la mejor forma de presentar la funcionalidad.

## <a name="how-do-bots-work"></a>¿Cómo funcionan los bots?

El bot consta de tres partes:

* Un servicio web accesible públicamente que se hospeda.
* El registro de bot que registra el bot con el marco de bot.
* El paquete de la aplicación teams que contiene el manifiesto de la aplicación. Esto es lo que los usuarios instalan y conectan el cliente de Microsoft Teams a su servicio Web (enrutado a través del servicio de bot).

Los bots para Microsoft Teams se basan en [Microsoft bot Framework](https://dev.botframework.com/). (Si ya tiene un bot basado en el marco de robots, puede adaptarlo fácilmente para que funcione en Microsoft Teams). Le recomendamos que use C# o node. js para aprovechar los [SDK](/microsoftteams/platform/#pivot=sdk-tools). Estos paquetes amplían las clases y métodos básicos del SDK de bot Builder:

* Uso de tipos de tarjeta especializados como la tarjeta de conector de Office 365.
* Consumo y configuración de datos de canal específicos de cada equipo en actividades.
* Procesamiento de solicitudes de extensión de mensajería.

> [!IMPORTANT]
> Puede desarrollar aplicaciones de Teams en cualquier tecnología de programación web y llamar directamente a las [API de REST de bot Framework](/bot-framework/rest-api/bot-framework-rest-overview) , pero debe realizar el control de los tokens de forma manual.

*Teams App Studio* le ayuda a crear y configurar el manifiesto de la aplicación, y puede registrar el servicio web como un bot en el marco de trabajo de bot. También contiene una biblioteca de controles de reAct y un generador de tarjetas interactivas. *Consulte* [Introducción a teams App Studio](~/concepts/build-and-test/app-studio-overview.md).

## <a name="webhooks-and-connectors"></a>Webhooks y conectores

Los webhooks y los conectores le permiten crear un bot sencillo para la interacción básica, como iniciar un flujo de trabajo u otros comandos sencillos. Solo residen en el equipo en el que los crea y están destinados a procesos sencillos específicos del flujo de trabajo de su empresa. *Consulte* [¿Qué son los webhooks y los conectores?](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) para obtener más información.

## <a name="get-started"></a>Introducción

* [Robot de conversaciones de Microsoft Teams en C#/dotnet](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)
* [Robot de conversaciones de Microsoft Teams en JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a>Más información

* [Conceptos básicos de los bots en Teams](~/bots/bot-basics.md)
* [Crear un bot para Teams](~/bots/how-to/create-a-bot-for-teams.md)

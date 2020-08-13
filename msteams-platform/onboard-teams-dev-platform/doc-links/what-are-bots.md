---
title: ¿Qué son los bots?
author: clearab
description: Información general sobre los bots en Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 1e07d56769cbb303f9af98f84c8ae6064325c1a7
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652185"
---
# <a name="what-are-bots"></a>¿Qué son los bots?

Los bots permiten que los usuarios interactúen con el servicio Web a través de texto, tarjetas interactivas y módulos de tareas. Son increíblemente flexibles: puede usar el ámbito de los bots para controlar algunos comandos sencillos o asistentes virtuales con tecnología de inteligencia artificial y procesamiento de idiomas naturales. Pueden ser un aspecto de una aplicación más grande o completamente independientes.

Buscar la combinación correcta de módulos de tarjetas, texto y tareas es clave para crear un bot útil. No olvide que los bots son mucho más que texto.

![P + f más GIF](~/assets/images/FAQPlusEndUser.gif)

## <a name="user-scenarios"></a>Escenarios de usuario

Los bots en Microsoft Teams pueden formar parte de un canal, de un chat de grupo o de un chat uno a uno. Cada ámbito proporcionará oportunidades y desafíos únicos para el bot conversador.

### <a name="in-a-channel"></a>En un canal

Los canales contienen conversaciones encadenadas entre varias personas, potencialmente muchas personas (actualmente, hasta 2000). Esto proporciona potencialmente a su bot un alcance masivo, pero las interacciones individuales deben ser concisas. Las interacciones de varios torneados tradicionales probablemente no funcionarán correctamente. En su lugar, use tarjetas interactivas o módulos de tareas, o bien, puede mover la conversación a una conversación uno a uno si necesita recopilar mucha información. El bot también tendrá acceso a los mensajes en los que se encuentra `@mentioned` directamente, aunque puede recuperar mensajes adicionales de la conversación con Microsoft Graph y permisos de nivel de organización elevados.

Algunos escenarios en los que Excel de los bots en un canal son:

* **Notificaciones**, especialmente si proporciona una tarjeta interactiva para que los usuarios tomen información adicional.
* **Escenarios de comentarios** como sondeos y encuestas.
* Interacciones que se pueden resolver en un **ciclo de solicitud/respuesta único**, donde los resultados son útiles para varios miembros de la conversación.
* **Bots sociales/divertidos** : Obtenga una imagen de gato increíbles, elija un ganador de forma aleatoria, etc.

### <a name="in-a-group-chat"></a>En un chat en grupo

Los chats de grupo son conversaciones sin encadenamientos entre tres o más personas. Tienden a tener menos miembros que un canal y son más transitorios. De forma similar a un canal, el bot solo tendrá acceso a los mensajes en los que esté `@mentioned` directamente.

Los escenarios que funcionan bien en un canal suelen funcionar tan bien en un chat en grupo.

### <a name="in-a-one-on-one-chat"></a>En un chat de uno a uno

Esta es la forma tradicional de que un bot de conversación interactúe con un usuario. Pueden habilitar cargas de trabajo increíblemente heterogéneas. P&los bots, bots que inician flujos de trabajo en otros sistemas, bots que indican chistes y bots que toman notas son solo algunos ejemplos. No olvide tener en cuenta si una interfaz basada en conversaciones es la mejor forma de presentar la funcionalidad.

## <a name="building-a-teams-bot-with-the-microsoft-bot-framework"></a>Creación de un bot de Teams con Microsoft bot Framework

[Microsoft bot Framework](https://dev.botframework.com/) es un completo SDK para la creación de bots con C#, Java, Python o JavaScript. Si ya tiene un bot basado en el marco de robots, puede adaptarlo fácilmente para que funcione en Microsoft Teams. Le recomendamos que use C# o Node.js para aprovechar los [SDK](/microsoftteams/platform/#pivot=sdk-tools). Estos paquetes amplían las clases y los métodos del SDK de bot Builder básico de la siguiente manera:

* Use tipos de tarjeta especializados como la tarjeta de conector de Office 365.
* Consume y establece los datos de canal específicos de cada equipo en actividades.
* Procesar las solicitudes de extensión de mensajería.

> [!IMPORTANT]
> Puede desarrollar las aplicaciones de Microsoft Teams en cualquier tecnología de programación web y llamar a las [API de REST de bot Framework](/bot-framework/rest-api/bot-framework-rest-overview) directamente, pero debe realizar el control de los tokens de forma manual.

El bot de Teams consta de tres elementos:

* Un servicio web accesible públicamente que se hospeda.
* El registro de los robots con bot Framework.
* El paquete de la aplicación Teams con el manifiesto de la aplicación. Esto es lo que los usuarios instalarán y conectarán el cliente de Microsoft Teams al servicio Web, que se enrutará a través del servicio de bot.

> [!TIP]
> Teams App Studio * le ayuda a crear y configurar el manifiesto de la aplicación y puede registrar el servicio web como un bot en el marco de trabajo de bot. También contiene una biblioteca de controles de reAct y un generador de tarjetas interactivas. *Consulte* [Introducción a teams App Studio](~/concepts/build-and-test/app-studio-overview.md).

## <a name="building-a-teams-bot-with-microsoft-power-virtual-agents"></a>Creación de un bot Teams con Microsoft Power virtual Agents

[Power virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) es un servicio basado en Microsoft Power Platform y bot Framework. El proceso de desarrollo del agente virtual de Power utiliza un enfoque de interfaz gráfica, sin código y guiado para dotar a todos los miembros de su equipo de crear y mantener fácilmente un agente virtual inteligente. Una vez que haya terminado de crear el Chatbot en el [portal de agentes de Power virtual](https://powervirtualagents.microsoft.com), puede [integrar fácilmente su Chatbot de agentes de Power virtual con Microsoft Teams](../../bots/how-to/add-power-virtual-agents-bot-to-teams.md). Para empezar a crear su Chatbot de agentes de Power virtual, *consulte* la documentación de los [agentes virtuales de Power](https://docs.microsoft.com/power-virtual-agents/).

## <a name="connectors-and-bots"></a>Conectores y bots

Los conectores le permiten crear un bot sencillo para la interacción básica, como iniciar un flujo de trabajo u otros comandos sencillos. Solo residen en el equipo en el que los crea y están destinados a procesos sencillos específicos del flujo de trabajo de su empresa. *Consulte* [¿Qué son los webhooks y los conectores?](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) para obtener más información.

## <a name="bot-fails"></a>Error de bot

### <a name="having-multi-turn-experiences-in-chat"></a>Tener experiencia de varios turnos en el chat

Un cuadro de diálogo extensivo entre su bot y el usuario es una forma lenta y demasiado compleja de realizar una tarea y también requiere que el desarrollador mantenga el estado. Para salir de este estado, un usuario debe agotar el tiempo de espera o escribir "*Cancelar*". Sobre todo, el proceso es tedioso innecesariamente:

USUARIO: programar una reunión con Nuria.

BOT: he encontrado 200 resultados, por lo que debe incluir un nombre y un apellido.

USUARIO: programar una reunión con Nuria Bowen.

BOT: correcto, ¿a qué hora desea reunirse con Nuria Bowen?

USUARIO: 1:00 pm.

BOT: ¿en qué día?

### <a name="supporting-too-many-commands"></a>Compatibilidad con demasiados comandos

Un bot que admite demasiados comandos, especialmente una amplia gama de comandos, no tendrá éxito o los usuarios los verán de forma positiva. Dado que solo hay 6 comandos visibles en el menú bot actual, es poco probable que se use cualquier cosa más con cualquier frecuencia. Los bots que profundizan en un área específica en lugar de intentar ser un amplio asistente funcionarán mejor y tarifar.

### <a name="maintaining-a-large-retrieval-knowledge-base-with-unranked-responses"></a>Mantener una base de conocimientos de recuperación de gran tamaño con respuestas sin clasificar

Los bots son idóneos para las interacciones breves y rápidas, sin examinar las listas largas en busca de una respuesta.

## <a name="get-started"></a>Introducción

* [Robot de conversaciones de Microsoft Teams en C#/dotnet](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)
* [Bot de conversación de Teams en JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a>Más información

* [Conceptos básicos de los bots en Teams](~/bots/bot-basics.md)
* [Creación de un bot para Teams](~/bots/how-to/create-a-bot-for-teams.md)
* [Planeación de la aplicación](../../concepts/extensibility-points.md)
* [Diseñando la aplicación].. /(.. /designing-your-app/designing-overview.md)
* [Compilar la aplicación](../../concepts/building-an-app.md)
* [Publicación de la aplicación](../../concepts/deploy-and-publish/overview.md)

---
title: ¿Qué son los bots de conversación?
author: clearab
description: Información general sobre los bots de conversación en Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 0304ae436b54db0d111eaed507beb350f1ca4632
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797872"
---
# <a name="what-are-conversational-bots-in-microsoft-teams"></a>¿Qué son los bots de conversación en Microsoft Teams?

Los bots de conversación permiten a los usuarios interactuar con el servicio web a través de texto, tarjetas interactivas y módulos de tareas. Son increíblemente flexibles: los bots de conversación pueden tener un ámbito para controlar algunos comandos simples o asistentes virtuales complejos, de inteligencia artificial y de procesamiento de lenguaje natural. Pueden ser un aspecto de una aplicación más grande o completamente independientes.

El GIF siguiente muestra a un usuario conversando con un bot en un chat de uno a uno con tarjetas interactivas y de texto. Encontrar la combinación adecuada de tarjetas, texto y módulos de tareas es clave para crear un bot útil. No olvide que los bots son mucho más que texto.

![Preguntas más frecuentes más gif](~/assets/images/FAQPlusEndUser.gif)

## <a name="build--a-bot-for-teams-with-the-microsoft-bot-framework"></a>Crear un bot para Teams con Microsoft Bot Framework

[Microsoft Bot Framework es](https://dev.botframework.com/) un SDK enriquecido para crear bots con C#, Java, Python y JavaScript. Si ya tiene un bot basado en Bot Framework, puede adaptarlo fácilmente para que funcione en Microsoft Teams. Se recomienda usar C# o Node.js para aprovechar nuestros [SDK.](/microsoftteams/platform/#pivot=sdk-tools) Estos paquetes amplían las clases y los métodos básicos del SDK de Bot Builder de la siguiente manera:

* Use tipos de tarjetas especializadas como la tarjeta de conector de Office 365.
* Consumir y establecer datos de canal específicos de Teams en las actividades.
* Procesar solicitudes de extensión de mensajería.

El bot de Teams consta de tres elementos:

* Un servicio web de acceso público que se hospeda.
* El registro del bot con Bot Framework.
* El paquete de la aplicación de Teams con el manifiesto de la aplicación. Esto es lo que instalarán los usuarios y conectará el cliente de Teams al servicio web, enrutado a través del servicio bot.

> [!IMPORTANT]
> Puede desarrollar aplicaciones de Teams en cualquier tecnología de programación web y llamar directamente a las API de REST de [Bot Framework,](/bot-framework/rest-api/bot-framework-rest-overview) pero debe realizar todo el control de tokens usted mismo.

> [!TIP]
> Teams App Studio* le ayuda a crear y configurar el manifiesto de la aplicación, y puede registrar su servicio web como un bot en Bot Framework. También contiene una biblioteca de control de React y un generador de tarjetas interactivas. *Consulte* [Introducción a Teams App Studio.](~/concepts/build-and-test/app-studio-overview.md)

## <a name="create-a-chatbot-for-teams-with-microsoft-power-virtual-agents"></a>Crear un bot de chat para Teams con microsoft Power Virtual Agents

[Power Virtual Agents es](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) un servicio chatbot, integrado en la plataforma Microsoft Power y Bot Framework.  El proceso de desarrollo de Power Virtual Agent usa un enfoque de interfaz gráfica guiado sin código para que todos los miembros del equipo puedan crear y mantener fácilmente un agente virtual inteligente.  Una vez que haya completado la creación de su bot de chat en el portal de [Power Virtual Agents,](https://powervirtualagents.microsoft.com)puede integrar fácilmente el bot de chat de [Power Virtual Agents con Teams.](how-to/add-power-virtual-agents-bot-to-teams.md) Para empezar a crear el bot de chat de Power Virtual Agents, *consulte la* documentación de Power [Virtual Agents.](https://docs.microsoft.com/power-virtual-agents/)

## <a name="webhooks-and-connectors"></a>Webhooks y conectores

Los webhooks y conectores permiten crear un bot simple para una interacción básica, como iniciar un flujo de trabajo u otros comandos simples. Solo se encuentran en el equipo en el que los crea y están diseñados para procesos sencillos específicos del flujo de trabajo de su empresa. *Vea* [¿Qué son los webhooks y conectores?](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) para obtener más información.

## <a name="where-bots-work-best"></a>Dónde funcionan mejor los bots

Los bots de Microsoft Teams pueden formar parte de una conversación uno a uno, un chat en grupo o un canal de un equipo. Cada ámbito proporcionará oportunidades y desafíos únicos para el bot de conversación.

### <a name="in-a-channel"></a>En un canal

Los canales contienen conversaciones en subproceso entre varias personas, lo que puede ser una gran cantidad de personas (actualmente, hasta dos mil). Esto potencialmente le da al bot un alcance masivo, pero las interacciones individuales deben ser concisas. Las interacciones tradicionales de varios giros probablemente no funcionen bien. En su lugar, busque usar tarjetas interactivas o módulos de tareas, o mover la conversación a una conversación uno a uno si necesita recopilar una gran cantidad de información. El bot solo tendrá acceso a los mensajes donde está directamente, aunque puede recuperar mensajes adicionales de la conversación con Microsoft Graph y permisos elevados de nivel `@mentioned` de organización.

Algunos escenarios en los que los bots excel en un canal son:

* **Notificaciones,** especialmente si proporciona una tarjeta interactiva para que los usuarios puedan tomar información adicional.
* **Escenarios de comentarios** como sondeos y encuestas.
* Interacciones que se pueden resolver en un único ciclo de **solicitud/respuesta,** donde los resultados son útiles para varios miembros de la conversación.
* **Bots sociales y divertidos:** obtener una imagen de gato increíble, elegir aleatoriamente un ganador, etc.

### <a name="in-a-group-chat"></a>En un chat en grupo

Los chats en grupo son conversaciones sin subprocesos entre tres o más personas. Tienden a tener menos miembros que un canal y son más transitorios. De forma similar a un canal, el bot solo tendrá acceso a los mensajes en los que está `@mentioned` directamente.

Los escenarios que funcionan bien en un canal normalmente funcionarán igual de bien en un chat en grupo.

### <a name="in-a-one-to-one-chat"></a>En un chat de uno a uno

Esta es la forma tradicional de que un bot de conversación interactúe con un usuario. Pueden habilitar cargas de trabajo increíblemente diversas. P&Bots A, bots que inician flujos de trabajo en otros sistemas, bots que cuentan las diferencias y bots que toman notas son solo algunos ejemplos. Recuerda tener en cuenta si una interfaz basada en conversación es la mejor manera de presentar tu funcionalidad.

## <a name="bot-fails"></a>Error de bot

### <a name="having-multi-turn-experiences-in-chat"></a>Tener experiencias de varios turnos en el chat

Un amplio cuadro de diálogo entre el bot y el usuario es una forma lenta y demasiado compleja de completar una tarea y también requiere que el desarrollador mantenga el estado. Para salir de este estado, un usuario debe tiempo de espera o escribir "*Cancelar*". Por encima de todo, el proceso es innecesariamente tedioso:

USUARIO: programar una reunión con Megan.

BOT: He encontrado 200 resultados, incluya un nombre y apellidos.

USUARIO: Programar una reunión con Megan Bowen.

BOT: ¿Qué hora le gustaría reunirse con Megan Bowen?

USUARIO: 1:00 p.m.

BOT: ¿en qué día?

### <a name="supporting-too-many-commands"></a>Compatibilidad con demasiados comandos

Un bot que admite demasiados comandos, especialmente una amplia gama de comandos, no se realizará correctamente ni los usuarios lo verán de forma positiva. Dado que solo hay 6 comandos visibles en el menú bot actual, es poco probable que se utilice algo más con cualquier frecuencia. Los bots que se arrasen en un área específica en lugar de intentar ser un asistente general funcionarán y se mejorarán.

### <a name="maintaining-a-large-retrieval-knowledge-base-with-unranked-responses"></a>Mantener una base de conocimientos de recuperación de gran tamaño con respuestas no aprovisionadas

Los bots son ideales para interacciones breves y rápidas, no para el control de listas largas que buscan una respuesta.

## <a name="get-started"></a>Introducción

* [Bot de conversación de Teams en C#/dotnet](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)
* [Bot de conversación de Teams en JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a>Más información

> [!div class="nextstepaction"]
> [Conceptos básicos de los bots en Teams](~/bots/bot-basics.md)

> [!div class="nextstepaction"]
> [Creación de un bot para Teams](~/bots/how-to/create-a-bot-for-teams.md)

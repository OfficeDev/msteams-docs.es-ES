---
title: Agregar bots a las aplicaciones de Microsoft Teams
description: Describe cómo empezar a desarrollar bots en Microsoft Teams
keywords: desarrollo de bots de Microsoft Teams
ms.date: 05/20/2018
ms.openlocfilehash: 0ecb268c34275e958103c9905b2ed1f0858cafda
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675745"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>Agregar bots a las aplicaciones de Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Cree y conecte bots inteligentes para interactuar con los usuarios de Microsoft Teams de forma natural a través de chat. O proporcionar un bot basado en comandos sencillo, que se usará como interfaz de "línea de comandos" para la experiencia de la aplicación de Microsoft Teams más amplia. Puede crear un bot de solo notificación, que puede insertar información relevante para los usuarios directamente en un canal o mensaje directo. Incluso puede llevar el bot existente basado en el marco de bots y agregar la compatibilidad específica de Microsoft Teams para que su experiencia sea brillante.

![Ejemplo de un bot para ayudar a un usuario](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>Lo que debe saber: bots

Un bot aparece igual que cualquier otro miembro del equipo con el que interactúe en una conversación, excepto que tiene un icono de Avatar hexagonal y siempre está en línea.

Un bot se comporta de forma diferente en función del tipo de conversación en el que participa. Los bots en Teams admiten varios tipos de conversaciones (denominados ámbitos en el manifiesto de la [aplicación](~/resources/schema/manifest-schema.md)).

* `teams`También se denominan conversaciones de canal.
* `personal`Conversaciones entre un bot y un único usuario
* `groupChat`Una conversación entre un bot y 2 o más usuarios

Consulte [tener una conversación con un bot de Microsoft Teams](~/resources/bot-v3/bot-conversations/bots-conversations.md) para obtener más información.

Con las aplicaciones de Microsoft Teams, puede convertir el bot en la estrella de su experiencia o solo una aplicación auxiliar. Los bots se distribuyen como parte de su paquete de aplicaciones más amplio, que puede incluir otras funciones, como [fichas](~/tabs/what-are-tabs.md) o [extensiones de mensajería](~/messaging-extensions/what-are-messaging-extensions.md).

## <a name="bot-apis"></a>API de bot

Microsoft Teams es compatible con la mayor parte de [Microsoft bot Framework](https://dev.botframework.com/). (Si ya tiene un bot basado en el marco de robots, puede adaptarlo fácilmente para que funcione en Microsoft Teams). Le recomendamos que use C# o node. js para aprovechar los [SDK](/microsoftteams/platform/#pivot=sdk-tools). Estos paquetes amplían las clases y métodos básicos del SDK de bot Builder:

* Uso de tipos de tarjeta especializados como la tarjeta de conector de Office 365
* Consumo y configuración de datos de canal específicos de cada equipo en actividades
* Procesamiento de solicitudes de extensión de mensajería

Las dependencias de instalación de extensiones de SDK, incluido el SDK de bot Builder.

* **.Net** Para usar las extensiones de Microsoft Teams para el SDK de bot Builder para .NET, instale el paquete NuGet [Microsoft. bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) en el proyecto de Visual Studio.
* **Node. js** para usar las extensiones de Microsoft Teams para el SDK de bot Builder para node. js, agregue el paquete NPM [de botbuilder-Teams](https://www.npmjs.com/package/botbuilder-teams) .
* **Código fuente** Puede encontrar el código fuente completo para las extensiones en el repositorio [BotBuilder-Microsoft Teams](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams) en github.

> [!IMPORTANT]
> Puede desarrollar aplicaciones de Teams en cualquier otra tecnología de programación web y llamar directamente a las [API de REST de bot Framework](/bot-framework/rest-api/bot-framework-rest-overview) , pero debe realizar el control de los tokens de forma manual.

*Teams App Studio* le ayudará a crear y configurar el manifiesto de la aplicación, y puede crear su bot Framework de bot. También contiene una biblioteca de controles de reAct y un generador de tarjetas interactivas.

## <a name="outgoing-webhooks"></a>Webhooks salientes

Los webhooks salientes le permiten crear un bot sencillo para la interacción básica, como iniciar un flujo de trabajo u otros comandos sencillos que pueda necesitar. Los webhooks salientes viven solo en el equipo en el que los crea y están destinados a procesos sencillos específicos del flujo de trabajo de su empresa. Vea los [webhooks de salida](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md) para obtener más información.

## <a name="build-a-great-teams-bot"></a>Crear un robot de equipos estupendo

Los siguientes temas le guiarán por el proceso de creación de un gran robot para Teams.

* [Crear un bot](~/resources/bot-v3/bots-create.md): aproveche las excelentes herramientas, la documentación y la comunidad que proporciona el equipo del marco de robots.
* [Hable con su bot](~/resources/bot-v3/bot-conversations/bots-conversations.md): agregar un flujo de conversación básico y aprovechar la funcionalidad específica de canal. Si desarrolla en .NET o en node. js, use nuestras extensiones para el SDK de bot Builder para simplificar su trabajo.
* [Uso de tarjetas en el bot](~/resources/bot-v3/bots-cards.md) Diseñe tarjetas para comunicar y aceptar la respuesta del usuario.
* [Responder a los eventos de bot](~/resources/bot-v3/bots-notifications.md).
* [Bots de solo notificación](~/resources/bot-v3/bots-notification-only.md) Uso de bots para enviar notificaciones para la aplicación.
* [Obtener contexto](~/resources/bot-v3/bots-context.md) Obtener información sobre el usuario.
* [Menús de bot](~/resources/bot-v3/bots-menus.md) Uso de menús en bots.
* [Bots y archivos](~/resources/bot-v3/bots-files.md) Enviar y recibir archivos desde bots.
* [Uso de pestañas con bots](~/resources/bot-v3/bots-with-tabs.md) Hacer que las pestañas y los bots trabajen juntos.
* [Pruebe el bot](~/resources/bot-v3/bots-test.md): agregue el bot para las conversaciones personales o del equipo para verlo en acción.

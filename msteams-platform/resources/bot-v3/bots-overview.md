---
title: Agregar bots a aplicaciones de Microsoft Teams
description: Describe cómo empezar a desarrollar bots en Microsoft Teams
ms.topic: conceptual
keywords: desarrollo de bots de teams
ms.date: 05/20/2018
ms.openlocfilehash: 226340500f59754d603f21b7868eecab38f942af
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014407"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>Agregar bots a aplicaciones de Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Cree y conecte bots inteligentes para interactuar con los usuarios de Microsoft Teams de forma natural a través del chat. O bien, proporcione un bot sencillo basado en comandos, que se usará como la interfaz de la "línea de comandos" para su experiencia de aplicación de Teams más amplia. Puede crear un bot de solo notificación, que puede enviar información relevante a los usuarios directamente a ellos en un canal o mensaje directo. Incluso puede traer el bot basado en Bot Framework existente y agregar soporte específico de Teams para hacer que su experiencia desluciente.

![Ejemplo de un bot que ayuda a un usuario](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>Lo que necesita saber: Bots

Un bot aparece como cualquier otro miembro del equipo con el que interactúes en una conversación, excepto que tiene un icono de avatar hexágono y siempre está en línea.

Un bot se comporta de forma diferente en función del tipo de conversación en la que esté implicado. Los bots de Teams admiten varios tipos de conversaciones (denominadas ámbitos en el manifiesto [de la aplicación).](~/resources/schema/manifest-schema.md)

* `teams` También se denominan conversaciones de canal
* `personal` Conversaciones entre un bot y un solo usuario
* `groupChat` Una conversación entre un bot y 2 o más usuarios

Consulte [Tener una conversación con un bot de Microsoft Teams](~/resources/bot-v3/bot-conversations/bots-conversations.md) para obtener más información.

Con las aplicaciones de Microsoft Teams, puede hacer que el bot sea la estrella de su experiencia o simplemente una aplicación auxiliar. Los bots se distribuyen como parte del paquete de la aplicación más amplio, que puede incluir [otras](~/tabs/what-are-tabs.md) funcionalidades, como pestañas o extensiones [de mensajería.](~/messaging-extensions/what-are-messaging-extensions.md)

## <a name="bot-apis"></a>API de bot

Microsoft Teams es compatible con la mayor parte de [Microsoft Bot Framework.](https://dev.botframework.com/) (Si ya tiene un bot basado en Bot Framework, puede adaptarlo fácilmente para que funcione en Microsoft Teams). Se recomienda usar C# o Node.js para aprovechar nuestros [SDK.](/microsoftteams/platform/#pivot=sdk-tools) Estos paquetes amplían las clases y los métodos básicos del SDK de Bot Builder:

* Usar tipos de tarjetas especializadas como la tarjeta de conector de Office 365
* Consumo y configuración de datos de canal específicos de Teams en actividades
* Procesamiento de solicitudes de extensión de mensajería

Las extensiones sdk instalan dependencias, incluido el SDK de Bot Builder.

* **.NET** Para usar las extensiones de Microsoft Teams para el SDK de Bot Builder para .NET, instale el paquete [NuGet Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) en su proyecto Visual Studio web. Para Node.js desarrollo, la funcionalidad de BotBuilder para Microsoft Teams se incorporó al SDK de [Bot Framework](https://github.com/microsoft/botframework-sdk) a partir de la versión 4.6.

*Vea también ejemplos* [de Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)

> [!IMPORTANT]
> Puede desarrollar aplicaciones de Teams en cualquier otra tecnología de programación web y llamar directamente a las API de REST de [Bot Framework,](/bot-framework/rest-api/bot-framework-rest-overview) pero debe realizar todo el control de tokens usted mismo.

*Teams App Studio le* ayuda a crear y configurar el manifiesto de la aplicación, y puede crear el bot de Bot Framework por usted. También contiene una biblioteca de control de React y un generador de tarjetas interactivas.

## <a name="outgoing-webhooks"></a>Webhooks salientes

Los webhooks salientes le permiten crear un bot simple para una interacción básica, como iniciar un flujo de trabajo u otros comandos simples que pueda necesitar. Los webhooks salientes solo se encuentran en el equipo en el que los crea y están diseñados para procesos sencillos específicos del flujo de trabajo de su empresa. Vea [los webhooks salientes](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md) para obtener más información.

## <a name="build-a-great-teams-bot"></a>Crear un excelente bot de Teams

Los siguientes temas le guiarán a través del proceso de creación de un excelente bot para Teams.

* [Cree un bot:](~/resources/bot-v3/bots-create.md)aproveche las excelentes herramientas, documentación y comunidad proporcionadas por el equipo de Bot Framework.
* [Hable con su bot:](~/resources/bot-v3/bot-conversations/bots-conversations.md)agregue flujo de conversación básico y aproveche la funcionalidad específica del canal. Si desarrolla en .NET o Node.js, use nuestras extensiones para el SDK de Bot Builder para simplificar su trabajo.
* [Uso de tarjetas en el bot](~/resources/bot-v3/bots-cards.md) Diseñar tarjetas para comunicar y aceptar la respuesta del usuario.
* [Responder a eventos de bot](~/resources/bot-v3/bots-notifications.md).
* [Bots de solo notificación](~/resources/bot-v3/bots-notification-only.md) Usar bots para enviar notificaciones para la aplicación.
* [Obtener contexto](~/resources/bot-v3/bots-context.md) Obtener información sobre el usuario.
* [Menús de bot](~/resources/bot-v3/bots-menus.md) Usar menús en bots.
* [Bots y archivos](~/resources/bot-v3/bots-files.md) Enviar y recibir archivos de bots.
* [Uso de pestañas con bots](~/resources/bot-v3/bots-with-tabs.md) Hacer que las pestañas y los bots funcionen conjuntamente.
* [Pruebe el bot:](~/resources/bot-v3/bots-test.md)agregue el bot para las conversaciones personales o de equipo para verlo en acción.

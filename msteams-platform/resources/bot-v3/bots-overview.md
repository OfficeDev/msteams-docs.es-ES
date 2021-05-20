---
title: Agregar bots a aplicaciones Microsoft Teams
description: Describe cómo empezar a desarrollar bots en Microsoft Teams
ms.topic: conceptual
keywords: equipos de desarrollo de bots
localization_priority: Normal
ms.date: 05/20/2018
ms.openlocfilehash: 674576efccb2916b8a82ae27310d8fe49909a782
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566757"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>Agregar bots a aplicaciones Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Cree y conecte bots inteligentes para interactuar con usuarios de Microsoft Teams de forma natural a través del chat. O proporcione un bot basado en comandos simple, que se utilizará como su interfaz de "línea de comandos" para su experiencia de aplicación más amplia Teams. Puede crear un bot de solo notificación, que puede insertar información relevante para los usuarios directamente a ellos en un canal o mensaje directo. Incluso puede traer su bot basado en Bot Framework existente y agregar soporte específico de Teams para hacer brillar su experiencia.

![Ejemplo de un bot que ayuda a un usuario](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>Lo que necesita saber: Bots

Un bot aparece como cualquier otro miembro del equipo con el que interactúas en una conversación, excepto que tiene un icono de avatar hexagonal y siempre está en línea.

Un bot se comporta de manera diferente dependiendo del tipo de conversación en la que esté involucrado. Los bots de Teams admiten varios tipos de conversaciones denominadas ámbitos en el manifiesto de la [aplicación.](~/resources/schema/manifest-schema.md)

* `teams` También se denominan conversaciones de canal.
* `personal` Conversaciones entre un bot y un solo usuario.
* `groupChat` Una conversación entre un bot y 2 o más usuarios.

Para obtener más información, consulte [Tener una conversación con un bot de Microsoft Teams](~/resources/bot-v3/bot-conversations/bots-conversations.md).

Con Microsoft Teams aplicaciones, puedes hacer del bot la estrella de tu experiencia, o simplemente un ayudante. Los bots se distribuyen como parte del paquete de aplicaciones más amplio, lo que puede incluir otras funcionalidades, como [pestañas](~/tabs/what-are-tabs.md) o [extensiones de mensajería.](~/messaging-extensions/what-are-messaging-extensions.md)

## <a name="bot-apis"></a>API de bots

Microsoft Teams admite la mayoría de los [Microsoft Bot Framework.](https://dev.botframework.com/) (Si ya tiene un bot basado en Bot Framework, puede adaptarlo fácilmente para que funcione en Microsoft Teams.) Le recomendamos que utilice C# o Node.js para aprovechar nuestros [SDK.](/microsoftteams/platform/#pivot=sdk-tools) En estos paquetes, se amplían las clases y métodos básicos del SDK de Bot Builder:

* Uso de tipos de tarjetas especializadas como la tarjeta conector Office 365.
* Consumir y establecer datos de canal específicos de Teams en las actividades.
* Procesamiento de solicitudes de extensión de mensajería.

Las extensiones del SDK instalan dependencias, incluido el SDK de Bot Builder.

* **.NET** Para usar las extensiones de Microsoft Teams para el SDK de Bot Builder para .NET, instale el paquete [microsoft.bot.connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet en el proyecto de Visual Studio. Para Node.js desarrollo, botbuilder para Microsoft Teams funcionalidad se ha incorporado en el [BOT Framework SDK](https://github.com/microsoft/botframework-sdk) a partir de v4.6.

> [!IMPORTANT]
> Puede desarrollar aplicaciones Teams en cualquier otra tecnología de programación web y llamar directamente a [las API de REST de Bot Framework,](/bot-framework/rest-api/bot-framework-rest-overview) pero debe realizar todo el control de tokens usted mismo.

*Teams App Studio* le ayuda a crear y configurar el manifiesto de la aplicación y puede crear el bot de Bot Framework automáticamente. También contiene una biblioteca de control React y un generador de tarjetas interactivo.

## <a name="outgoing-webhooks"></a>Webhooks salientes

Los webhooks salientes le permiten crear un bot simple para la interacción básica, como iniciar un flujo de trabajo u otros comandos simples que pueda necesitar. Los webhooks salientes solo viven en el equipo en el que los crea y están destinados a procesos sencillos específicos del flujo de trabajo de su empresa. Para obtener más información, consulte [webhooks salientes](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).

## <a name="build-a-great-teams-bot"></a>Construir un gran bot Teams

Los siguientes temas le guiarán a través del proceso de creación de un gran bot para Teams:

* [Crear un bot:](~/resources/bot-v3/bots-create.md)aproveche las excelentes herramientas, documentación y comunidad proporcionadas por el equipo de Bot Framework.
* [Hable con su bot:](~/resources/bot-v3/bot-conversations/bots-conversations.md)Agregue flujo de conversación básico y aproveche la funcionalidad específica del canal. Si se desarrolla en .NET o Node.js, use nuestras extensiones para el SDK de Bot Builder para simplificar el trabajo.
* [Uso de tarjetas en el bot](~/resources/bot-v3/bots-cards.md): Diseñar tarjetas para comunicarse y aceptar la respuesta del usuario.
* [Responder a eventos de bots](~/resources/bot-v3/bots-notifications.md)
* [Bots solo de notificación:](~/resources/bot-v3/bots-notification-only.md)usar bots para enviar notificaciones para la aplicación.
* [Obtener contexto](~/resources/bot-v3/bots-context.md): Obtenga información sobre el usuario.
* [Menús de bots](~/resources/bot-v3/bots-menus.md): Uso de menús en bots.
* [Bots y archivos](~/resources/bot-v3/bots-files.md): Envío y recepción de archivos de bots.
* [Uso de pestañas con bots:](~/resources/bot-v3/bots-with-tabs.md)Hacer que las pestañas y los bots funcionen juntos.
* [Prueba tu bot:](~/resources/bot-v3/bots-test.md)añade tu bot para conversaciones personales o de equipo para verlo en acción.

## <a name="see-also"></a>Vea también

[Muestras de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).
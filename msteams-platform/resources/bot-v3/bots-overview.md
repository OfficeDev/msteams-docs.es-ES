---
title: Agregar bots a Microsoft Teams aplicaciones
description: Describe cómo empezar a desarrollar bots en Microsoft Teams
ms.topic: conceptual
keywords: desarrollo de bots de teams
localization_priority: Normal
ms.date: 05/20/2018
ms.openlocfilehash: 674576efccb2916b8a82ae27310d8fe49909a782
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566757"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>Agregar bots a Microsoft Teams aplicaciones

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Crea y conecta bots inteligentes para interactuar con Microsoft Teams usuarios de forma natural a través del chat. O bien, proporcione un bot simple basado en comandos, que se usará como la interfaz de la "línea de comandos" para la experiencia de la aplicación Teams más amplia. Puede crear un bot de solo notificación, que puede enviar información relevante para los usuarios directamente a ellos en un canal o mensaje directo. Incluso puedes traer el bot basado en Bot Framework existente y agregar Teams compatibilidad específica para hacer que tu experiencia brille.

![Ejemplo de un bot que ayuda a un usuario](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>Lo que necesita saber: Bots

Un bot aparece igual que cualquier otro miembro del equipo con el que interactúes en una conversación, excepto que tiene un icono de avatar hexagonal y siempre está en línea.

Un bot se comporta de forma diferente en función del tipo de conversación en la que esté implicado. Los bots de Teams admiten varios tipos de conversaciones denominadas ámbitos en el [manifiesto de la aplicación](~/resources/schema/manifest-schema.md).

* `teams` También se denomina conversaciones de canal.
* `personal` Conversaciones entre un bot y un solo usuario.
* `groupChat` Una conversación entre un bot y 2 o más usuarios.

Para obtener más información, vea [Tener una conversación con un Microsoft Teams bot](~/resources/bot-v3/bot-conversations/bots-conversations.md).

Con Microsoft Teams aplicaciones, puedes convertir el bot en la estrella de tu experiencia, o simplemente una aplicación auxiliar. Los bots se distribuyen como parte del paquete de aplicaciones más amplio, que puede incluir [otras](~/tabs/what-are-tabs.md) funcionalidades, como pestañas o extensiones [de mensajería.](~/messaging-extensions/what-are-messaging-extensions.md)

## <a name="bot-apis"></a>API de bot

Microsoft Teams admite la mayoría de los [Microsoft Bot Framework](https://dev.botframework.com/). (Si ya tienes un bot basado en bot Framework, puedes adaptarlo fácilmente para que funcione en Microsoft Teams). Le recomendamos que use C# o Node.js para aprovechar nuestros [SDK.](/microsoftteams/platform/#pivot=sdk-tools) En estos paquetes, se amplían las clases y métodos básicos del SDK de Bot Builder:

* Usar tipos de tarjeta especializados como la Office 365 connector.
* Consumir y establecer datos Teams canal específicos de las actividades.
* Procesamiento de solicitudes de extensión de mensajería.

Las extensiones del SDK instalan dependencias, incluido el SDK de Bot Builder.

* **.NET** Para usar las extensiones Microsoft Teams para el SDK de Bot Builder para .NET, instale el [paquete Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet en el Visual Studio proyecto. Para Node.js desarrollo, la funcionalidad botBuilder para Microsoft Teams se incorporó al [SDK de Bot Framework](https://github.com/microsoft/botframework-sdk) a partir de la versión 4.6.

> [!IMPORTANT]
> Puede desarrollar aplicaciones Teams en cualquier otra tecnología de programación web y llamar a las API de REST de [Bot Framework](/bot-framework/rest-api/bot-framework-rest-overview) directamente, pero debe realizar el control de todos los tokens usted mismo.

*Teams App Studio* te ayuda a crear y configurar el manifiesto de la aplicación y puedes crear el bot de Bot Framework por ti. También contiene una biblioteca React control y un generador de tarjetas interactivas.

## <a name="outgoing-webhooks"></a>Webhooks salientes

Los webhooks salientes te permiten crear un bot simple para la interacción básica, como iniciar un flujo de trabajo u otros comandos simples que necesites. Los webhooks salientes solo se encuentran en el equipo en el que se crean y están diseñados para procesos sencillos específicos del flujo de trabajo de su empresa. Para obtener más información, vea [webhooks salientes](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).

## <a name="build-a-great-teams-bot"></a>Crear un excelente Teams bot

Los siguientes temas le guiarán a través del proceso de creación de un gran bot para Teams:

* [Crear un bot:](~/resources/bot-v3/bots-create.md)aproveche las excelentes herramientas, documentación y comunidad proporcionadas por el equipo de Bot Framework.
* [Habla con el bot:](~/resources/bot-v3/bot-conversations/bots-conversations.md)agrega flujo de conversación básico y aprovecha la funcionalidad específica del canal. Si desarrolla en .NET o Node.js, use nuestras extensiones para el SDK de Bot Builder para simplificar su trabajo.
* [Uso de tarjetas en el bot:](~/resources/bot-v3/bots-cards.md)diseña tarjetas para comunicar y aceptar la respuesta del usuario.
* [Responder a eventos de bot](~/resources/bot-v3/bots-notifications.md)
* [Bots de solo notificación:](~/resources/bot-v3/bots-notification-only.md)usar bots para enviar notificaciones para la aplicación.
* [Obtener contexto:](~/resources/bot-v3/bots-context.md)obtener información sobre el usuario.
* [Menús bot:](~/resources/bot-v3/bots-menus.md)usar menús en bots.
* [Bots y archivos:](~/resources/bot-v3/bots-files.md)enviar y recibir archivos de bots.
* [Usar pestañas con bots:](~/resources/bot-v3/bots-with-tabs.md)hacer que las pestañas y los bots funcionen juntos.
* [Prueba el bot:](~/resources/bot-v3/bots-test.md)agrega el bot para conversaciones personales o de equipo para verlo en acción.

## <a name="see-also"></a>Consulte también

[Ejemplos de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).
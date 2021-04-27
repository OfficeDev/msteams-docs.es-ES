---
title: Agregar bots a aplicaciones de Microsoft Teams
description: Describe cómo empezar a desarrollar bots en Microsoft Teams
ms.topic: conceptual
keywords: desarrollo de bots de teams
localization_priority: Normal
ms.date: 05/20/2018
ms.openlocfilehash: c7b719aae3a8d1b09ed8a1be7f54028fe7f2481e
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019758"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>Agregar bots a aplicaciones de Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Crea y conecta bots inteligentes para interactuar con los usuarios de Microsoft Teams de forma natural a través del chat. O bien, proporcione un bot sencillo basado en comandos, que se usará como la interfaz de la "línea de comandos" para su experiencia de aplicación de Teams más amplia. Puede crear un bot de solo notificación, que puede enviar información relevante para los usuarios directamente a ellos en un canal o mensaje directo. Incluso puedes traer el bot basado en Bot Framework existente y agregar compatibilidad específica de Teams para que tu experiencia brille.

![Ejemplo de un bot que ayuda a un usuario](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>Lo que necesita saber: Bots

Un bot aparece igual que cualquier otro miembro del equipo con el que interactúes en una conversación, excepto que tiene un icono de avatar hexagonal y siempre está en línea.

Un bot se comporta de forma diferente en función del tipo de conversación en la que esté implicado. Los bots de Teams admiten varios tipos de conversaciones (denominadas ámbitos en el [manifiesto de la aplicación).](~/resources/schema/manifest-schema.md)

* `teams` Conversaciones de canal también denominadas
* `personal` Conversaciones entre un bot y un solo usuario
* `groupChat` Una conversación entre un bot y 2 o más usuarios

Consulta [Tener una conversación con un bot de Microsoft Teams](~/resources/bot-v3/bot-conversations/bots-conversations.md) para obtener más información.

Con las aplicaciones de Microsoft Teams, puedes convertir el bot en la estrella de tu experiencia, o simplemente un ayudante. Los bots se distribuyen como parte del paquete de aplicaciones más amplio, que puede incluir [otras](~/tabs/what-are-tabs.md) funcionalidades, como pestañas o extensiones [de mensajería.](~/messaging-extensions/what-are-messaging-extensions.md)

## <a name="bot-apis"></a>API de bot

Microsoft Teams admite la mayoría de [Microsoft Bot Framework](https://dev.botframework.com/). (Si ya tienes un bot basado en Bot Framework, puedes adaptarlo fácilmente para que funcione en Microsoft Teams). Le recomendamos que use C# o Node.js para aprovechar nuestros [SDK.](/microsoftteams/platform/#pivot=sdk-tools) En estos paquetes, se amplían las clases y métodos básicos del SDK de Bot Builder:

* Uso de tipos de tarjeta especializados como la tarjeta de Conector de Office 365
* Consumo y configuración de datos de canal específicos de Teams en actividades
* Procesamiento de solicitudes de extensión de mensajería

Las extensiones del SDK instalan dependencias, incluido el SDK de Bot Builder.

* **.NET** Para usar las extensiones de Microsoft Teams para el SDK de Bot Builder para .NET, instale el paquete [NuGet de Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) en el Visual Studio proyecto. Para Node.js desarrollo, la funcionalidad botBuilder para Microsoft Teams se incorporó al [SDK de Bot Framework](https://github.com/microsoft/botframework-sdk) a partir de la versión 4.6.

*Vea también ejemplos* [de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).

> [!IMPORTANT]
> Puede desarrollar aplicaciones de Teams en cualquier otra tecnología de programación web y llamar a las API de REST de [Bot Framework](/bot-framework/rest-api/bot-framework-rest-overview) directamente, pero debe realizar el control de todos los tokens usted mismo.

*Teams App Studio te* ayuda a crear y configurar el manifiesto de la aplicación y a crear tu bot de Bot Framework. También contiene una biblioteca de controles de React y un generador de tarjetas interactivas.

## <a name="outgoing-webhooks"></a>Webhooks salientes

Los webhooks salientes te permiten crear un bot simple para la interacción básica, como iniciar un flujo de trabajo u otros comandos simples que necesites. Los webhooks salientes solo se encuentran en el equipo en el que se crean y están diseñados para procesos sencillos específicos del flujo de trabajo de su empresa. Vea [webhooks salientes](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md) para obtener más información.

## <a name="build-a-great-teams-bot"></a>Crear un excelente bot de Teams

Los temas siguientes le guiarán a través del proceso de creación de un excelente bot para Teams.

* [Crear un bot:](~/resources/bot-v3/bots-create.md)aproveche las excelentes herramientas, documentación y comunidad proporcionadas por el equipo de Bot Framework.
* [Habla con el bot:](~/resources/bot-v3/bot-conversations/bots-conversations.md)agrega flujo de conversación básico y aprovecha la funcionalidad específica del canal. Si desarrolla en .NET o Node.js, use nuestras extensiones para el SDK de Bot Builder para simplificar su trabajo.
* [Uso de tarjetas en el bot](~/resources/bot-v3/bots-cards.md) Diseñar tarjetas para comunicar y aceptar la respuesta del usuario.
* [Responder a eventos del bot](~/resources/bot-v3/bots-notifications.md).
* [Bots de solo notificación](~/resources/bot-v3/bots-notification-only.md) Usar bots para enviar notificaciones para la aplicación.
* [Obtener contexto](~/resources/bot-v3/bots-context.md) Obtenga información sobre el usuario.
* [Menús bot](~/resources/bot-v3/bots-menus.md) Usar menús en bots.
* [Bots y archivos](~/resources/bot-v3/bots-files.md) Enviar y recibir archivos de bots.
* [Uso de pestañas con bots](~/resources/bot-v3/bots-with-tabs.md) Hacer que las pestañas y los bots funcionen juntos.
* [Prueba el bot:](~/resources/bot-v3/bots-test.md)agrega el bot para conversaciones personales o de equipo para verlo en acción.

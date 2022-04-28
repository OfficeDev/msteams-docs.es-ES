---
title: Adición de bots a aplicaciones Microsoft Teams
description: Describe cómo empezar a desarrollar bots en Microsoft Teams
ms.topic: conceptual
keywords: desarrollo de bots de teams
ms.localizationpriority: medium
ms.date: 05/20/2018
ms.openlocfilehash: 164c8e518e38d506bbaf80f59edebfb18c07acec
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103428"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>Adición de bots a aplicaciones Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Cree y conecte bots inteligentes para interactuar con Microsoft Teams usuarios de forma natural a través del chat. O bien, proporcione un bot simple basado en comandos que se usará como interfaz de "línea de comandos" para una experiencia de aplicación más amplia Teams. Puede crear un bot de solo notificación, que puede insertar información relevante para los usuarios directamente en un canal o mensaje directo. Incluso puede traer su bot existente basado en Bot Framework y agregar Teams compatibilidad específica para que su experiencia brille.

> [!IMPORTANT]
> Actualmente, los bots están disponibles en Government Community Cloud (GCC), pero no están disponibles en GCC-High ni en el Departamento de Defensa (DOD).

![Ejemplo de bot que ayuda a un usuario](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>Lo que necesita saber: bots

Un bot aparece igual que cualquier otro miembro del equipo con el que interactúe en una conversación, salvo que tiene un icono de avatar hexagonal y siempre está en línea.

Un bot se comporta de forma diferente en función del tipo de conversación en la que esté implicado. Los bots de Teams admiten varios tipos de conversaciones denominadas ámbitos en el manifiesto de [la aplicación](~/resources/schema/manifest-schema.md).

* `teams` También se denominan conversaciones de canal.
* `personal` Conversaciones entre un bot y un único usuario.
* `groupChat` Una conversación entre un bot y 2 o más usuarios.

Para obtener más información, consulte [Tener una conversación con un bot de Microsoft Teams](~/resources/bot-v3/bot-conversations/bots-conversations.md).

Con Microsoft Teams aplicaciones, puede hacer que el bot sea la estrella de su experiencia o simplemente un asistente. Los bots se distribuyen como parte del paquete de aplicación más amplio, que puede incluir otras funcionalidades, como [pestañas](~/tabs/what-are-tabs.md) o [extensiones de mensajes](~/messaging-extensions/what-are-messaging-extensions.md).

## <a name="bot-apis"></a>API de bot

Microsoft Teams admite la mayoría de los [Microsoft Bot Framework](https://dev.botframework.com/). (Si ya tiene un bot basado en Bot Framework, puede adaptarlo fácilmente para que funcione en Microsoft Teams). Se recomienda usar C# o Node.js para aprovechar nuestros [SDK](/microsoftteams/platform/#pivot=sdk-tools). En estos paquetes, se amplían las clases y métodos básicos del SDK de Bot Builder:

* Usar tipos de tarjeta especializados, como la tarjeta Office 365 Connector.
* Consumo y configuración Teams datos de canal específicos en las actividades.
* Procesamiento de solicitudes de extensión de mensajes.

Las extensiones del SDK instalan dependencias, incluido el SDK de Bot Builder.

* **.NET** Para usar las extensiones de Microsoft Teams del SDK de Bot Builder para .NET, instale el paquete [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet en el proyecto de Visual Studio. Para Node.js desarrollo, la funcionalidad BotBuilder for Microsoft Teams se ha incorporado al [SDK de Bot Framework](https://github.com/microsoft/botframework-sdk) a partir de la versión 4.6.

> [!IMPORTANT]
> Puede desarrollar aplicaciones Teams en cualquier otra tecnología de programación web y llamar directamente a las [API REST de Bot Framework](/bot-framework/rest-api/bot-framework-rest-overview), pero debe realizar todo el control de tokens usted mismo.

*Teams App Studio* le ayuda a crear y configurar el manifiesto de la aplicación, y puede crear el bot de Bot Framework automáticamente. También contiene una biblioteca de control de React y un generador de tarjetas interactivo.

## <a name="outgoing-webhooks"></a>Webhooks salientes

Los webhooks salientes le permiten crear un bot sencillo para la interacción básica, como iniciar un flujo de trabajo u otros comandos simples que pueda necesitar. Los webhooks salientes solo se encuentran en el equipo en el que se crean y están diseñados para procesos simples específicos del flujo de trabajo de la empresa. Para obtener más información, consulte [webhooks salientes](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).

## <a name="build-a-great-teams-bot"></a>Creación de un bot de Teams excelente

Los temas siguientes le guiarán a través del proceso de creación de un bot excelente para Teams:

* [Creación de un bot](~/resources/bot-v3/bots-create.md): aproveche las excelentes herramientas, documentación y comunidad proporcionadas por el equipo de Bot Framework.
* [Hable con el bot](~/resources/bot-v3/bot-conversations/bots-conversations.md): agregue un flujo de conversación básico y aproveche la funcionalidad específica del canal. Si desarrolla en .NET o Node.js, use nuestras extensiones para el SDK de Bot Builder para simplificar el trabajo.
* [Uso de tarjetas en el bot](~/resources/bot-v3/bots-cards.md): diseñe tarjetas para comunicarse y aceptar la respuesta del usuario.
* [Respuesta a eventos de bot](~/resources/bot-v3/bots-notifications.md)
* [Bots de solo notificación](~/resources/bot-v3/bots-notification-only.md): uso de bots para enviar notificaciones para la aplicación.
* [Obtener contexto](~/resources/bot-v3/bots-context.md): obtenga información sobre el usuario.
* [Menús de bot:](~/resources/bot-v3/bots-menus.md) uso de menús en bots.
* [Bots y archivos](~/resources/bot-v3/bots-files.md): enviar y recibir archivos de bots.
* [Uso de pestañas con bots](~/resources/bot-v3/bots-with-tabs.md): hacer que las pestañas y los bots funcionen juntos.
* [Prueba del bot](~/resources/bot-v3/bots-test.md): agregue el bot para conversaciones personales o de equipo para verlo en acción.

## <a name="see-also"></a>Vea también

[Ejemplos de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).

---
title: Agregar bots a aplicaciones de Microsoft Teams
description: En este módulo, aprenderá a empezar a desarrollar bots en Microsoft Teams y cuáles son todos los requisitos para agregar un bot en Teams.
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 05/20/2018
ms.openlocfilehash: a1563d72ada21810393d7a0118b5a2b94463a27b
ms.sourcegitcommit: 69a45722c5c09477bbff3ba1520e6c81d2d2d997
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/11/2022
ms.locfileid: "67312215"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>Agregar bots a aplicaciones de Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Cree y conecte bots inteligentes para interactuar con los usuarios de Microsoft Teams con naturalidad a través del chat. O bien proporcione un bot sencillo basado en comandos, que se usará como su interfaz de "línea de comandos” para ampliar su experiencia en la aplicación de Teams. Puede crear un bot con solo notificaciones, que puede insertar información relevante para los usuarios directamente en un canal o mensaje directo. Incluso puede traer su bot existente basado en Bot Framework y agregar soporte técnico específico para Teams para que su experiencia sea deslumbrante.

> [!IMPORTANT]
> Actualmente, los bots están disponibles en Government Community Cloud (GCC) y GCC-High pero no están disponibles en el Departamento de Defensa (DOD).

:::image type="content" source="../../assets/images/bot_example.png" alt-text="Ejemplo de un bot ayudando a un usuario":::

## <a name="what-you-need-to-know-bots"></a>Aspectos que debe saber sobre los bots

Un bot aparece igual que cualquier otro miembro del equipo con el que interactúe en una conversación, salvo que aparece con un icono de avatar de forma hexagonal y siempre está en línea.

Un bot se comporta de forma diferente en función del tipo de conversación en la que esté implicado. Los bots de Teams admiten varios tipos de conversaciones denominadas ámbitos en el [manifiesto de aplicación](~/resources/schema/manifest-schema.md).

* `teams` También se denominan conversaciones de canal.
* `personal` Conversaciones entre bots y un único usuario.
* `groupChat` Una conversación entre un bot y dos o más usuarios.

Para obtener más información, consulte [Mantener una conversación con un bot de Microsoft Teams](~/resources/bot-v3/bot-conversations/bots-conversations.md).

Con las aplicaciones de Teams, puede hacer que el bot sea la estrella de su experiencia, o simplemente un asistente. Los bots se distribuyen como parte de un paquete de aplicación más amplio, que puede incluir otras funcionalidades, como [pestañas](~/tabs/what-are-tabs.md) o [extensiones de mensaje](~/messaging-extensions/what-are-messaging-extensions.md).

## <a name="bot-apis"></a>Las API del bot

Teams admite la mayoría de los [Microsoft Bot Framework](https://dev.botframework.com/). (Si ya tiene un bot basado en Bot Framework, puede adaptarlo fácilmente para que funcione en Teams). Se recomienda usar C# o Node.js para aprovechar nuestros [SDK](/microsoftteams/platform/#pivot=sdk-tools). En estos paquetes, se amplían las clases y métodos básicos del SDK de Bot Builder:

* Usar tipos de tarjeta especializados, como la tarjeta del conector Office 365.
* Consumo y configuración de datos de canal específicos de Teams en actividades.
* Procesar solicitudes de extensión de mensaje.

Las extensiones del SDK instalan dependencias, incluido el SDK de Bot Builder.

* **.NET** Para usar las extensiones de Microsoft Teams para el SDK de Bot Builder para .NET, instale el paquete NuGet [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) en el proyecto de Visual Studio. Para el desarrollo de Node.js, la funcionalidad BotBuilder para Microsoft Teams se ha incorporado al [SDK de Bot Framework](https://github.com/microsoft/botframework-sdk) a partir de la versión 4.6.

> [!IMPORTANT]
> Puede desarrollar aplicaciones de Teams en cualquier otra herramienta de programación web y llamar [a las API de REST de Bot Framework](/bot-framework/rest-api/bot-framework-rest-overview) directamente, pero debe realizar usted mismo toda la gestión de los tokens.

*El Portal para desarrolladores de Teams* le ayuda a crear y configurar el manifiesto de la aplicación, y puede crear el bot de Bot Framework automáticamente. También contiene una biblioteca de control de React y un generador de tarjetas interactivo.

## <a name="outgoing-webhooks"></a>Webhooks salientes

Los webhooks salientes permiten crear un bot sencillo para una interacción básica, como iniciar un flujo de trabajo u otros comandos sencillos que pueda necesitar. Los webhooks salientes solo residen en el equipo donde los crea y están diseñados para procesos simples específicos del flujo de trabajo de su empresa. Para obtener más información, consulte [webhooks salientes](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).

## <a name="build-a-great-teams-bot"></a>Cree un bot de Teams espectacular

Los siguientes artículos le guiarán a través del proceso de creación de un bot excelente para Teams:

* [Crear un bot](~/resources/bot-v3/bots-create.md): saque provecho de las excelentes herramientas, la documentación y la comunidad proporcionados por el equipo de Bot Framework.
* [Hablar con el bot](~/resources/bot-v3/bot-conversations/bots-conversations.md): agregue un flujo de conversación básico y aproveche la funcionalidad específica del canal. Si lo desarrolla en .NET o Node.js, use nuestras extensiones para el SDK de Bot Builder para simplificar el trabajo.
* [Usar tarjetas en el bot](~/resources/bot-v3/bots-cards.md): diseñe tarjetas para comunicarse y aceptar la respuesta del usuario.
* [Responder a eventos del bot](~/resources/bot-v3/bots-notifications.md)
* [Bots de solo notificación](~/resources/bot-v3/bots-notification-only.md): uso de bots para enviar notificaciones en la aplicación.
* [Obtener contexto](~/resources/bot-v3/bots-context.md): obtener información sobre el usuario.
* [Menús de bot](~/resources/bot-v3/bots-menus.md): uso de menús en bots.
* [Bots y archivos](~/resources/bot-v3/bots-files.md): envío y recepción de archivos por parte de los bots.
* [Usar pestañas con bots](~/resources/bot-v3/bots-with-tabs.md): hacer que las pestañas y los bots funcionen juntos.
* [Probar el bot](~/resources/bot-v3/bots-test.md): agregue el bot para conversaciones personales o de equipo para comprobar cómo funciona.

## <a name="see-also"></a>Consulte también

[Ejemplos de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).

---
title: Bots en Microsoft Teams
author: surbhigupta
description: En este artículo, use bots conversacionales en Microsoft Teams para compartir archivos, enviar notificaciones proactivas, tarjetas interactivas, realizar llamadas, invocar el comando de bot, IVR.
ms.topic: overview
ms.localizationpriority: high
ms.author: anclear
ms.openlocfilehash: 90176b63c64d23ae76a8c98515e37455ab0742c0
ms.sourcegitcommit: 217025a61ed9c3b76b507fe95563142abc6d0318
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2022
ms.locfileid: "67363517"
---
# <a name="build-bots-for-teams"></a>Crear bots para Teams

> [!NOTE]
> Se recomienda crear su primera aplicación de bot o aplicación de bot de notificación mediante la herramienta de desarrollo de nueva generación para Teams. Para obtener más información, vea [Teams Toolkit for Visual Studio Code](../toolkit/teams-toolkit-fundamentals.md) y [Teams Toolkit for Visual Studio](../toolkit/teams-toolkit-overview-visual-studio.md).

Un bot también se conoce como bot de chat o bot de conversación. Se trata de una aplicación que ejecuta tareas sencillas y repetitivas por parte de usuarios como el servicio de atención al cliente o el personal de soporte técnico. Los bots se usan a diario para, por ejemplo, proporcionar información sobre el tiempo, reservar cenas o facilitar información sobre viajes. Las interacciones con bots pueden ser preguntas y respuestas rápidas o conversaciones complejas.

> [!IMPORTANT]
>
> * Actualmente, los bots están disponibles en Government Community Cloud (GCC) y GCC-High, pero no en el Departamento de defensa (DOD).
>
> * Las aplicaciones de bot de Microsoft Teams están disponibles en GCC-High a través de [Azure bot Service](/azure/bot-service/how-to-deploy-gov-cloud-high) y el registro del canal de bot debe realizarse en el portal de Azure Government.
>
> * Las aplicaciones de GCCH solo admiten hasta la versión 1.10 del manifiesto. Las direcciones URL de imagen en Tarjetas adaptables no se admiten en el entorno GCCH. Puede reemplazar una dirección URL de imagen por DataUri codificado en Base64.

Los bots de conversación permiten que los usuarios interactúen con el servicio web mediante texto, tarjetas interactivas y módulos de tareas.

:::image type="content" source="../assets/images/invokebotwithtext.png" alt-text="La captura de pantalla es un ejemplo que muestra un servicio web con texto."lightbox="../assets/images/invokebotwithtext.png":::

:::image type="content" source="../assets/images/invokebotwithcard.png" alt-text="La captura de pantalla es un ejemplo que muestra un servicio web con tarjetas interactivas."lightbox="../assets/images/invokebotwithcard.png"border="true":::

:::image type="content" source="../assets/images/task-module-example.png" alt-text="La captura de pantalla es un ejemplo que muestra un servicio web mediante el módulo de tareas." lightbox="../assets/images/task-module-example-expanded.png":::

Los bots de conversación están dotados de gran flexibilidad. Los bots pueden controlar algunos comandos básicos y tareas más complejas que implican inteligencia artificial y procesamiento de lenguaje natural. Los bots pueden formar parte de una aplicación más grande o ser independientes.

Use la combinación correcta de tarjetas, texto y módulos de tareas para crear un bot que sea útil. En la siguiente imagen se muestra a un usuario conversando con un bot en un chat individual con texto y tarjetas interactivas.

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="La captura de pantalla es un ejemplo que muestra un bot de preguntas más frecuentes de ejemplo.":::

Cada interacción entre el usuario y el bot se representa como una actividad. Cuando un bot recibe una actividad, se la pasa a sus controladores de actividad. Vea los [controladores de actividad de bots](~/bots/bot-basics.md).

Los bots son aplicaciones que tienen una interfaz de conversación. Se puede interactuar con un bot mediante texto, tarjetas interactivas y voz. Un bot se comporta de forma diferente en función de si se trata de una conversación de chat de un canal o grupo o una conversación individual. Las conversaciones se controlan a través del conector de Bot Framework. Vea [conceptos básicos de la conversación](~/bots/how-to/conversations/conversation-basics.md).

El bot requiere información contextual, como los detalles del perfil de usuario, para tener acceso al contenido relevante y mejorar la experiencia de uso del bot. Vea [obtener el contexto de Teams](~/bots/how-to/get-teams-context.md).

Puede enviar y recibir archivos a través del bot mediante Graph API o las API de bot de Teams. Vea [enviar y recibir archivos a través del bot](~/bots/how-to/bots-filesv4.md).

La limitación de velocidad se usa para optimizar los bots que se usan para la aplicación de Teams. Para proteger Teams y a sus usuarios, las API del bot proporcionan un límite de velocidad para las solicitudes entrantes. Consulte [optimizar el bot con limitación de velocidad en Teams](~/bots/how-to/rate-limit.md).

Con Microsoft Graph API para llamadas y reuniones en línea, las aplicaciones de Teams ya pueden interactuar con los usuarios mediante voz y vídeo. Consulte [llamadas y bots de reuniones](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).

Puede usar las API de bot de Teams para obtener información de miembros de un chat o equipo. Vea [cambios en las API de bot de Teams para capturar miembros del equipo o chat](~/resources/team-chat-member-api-changes.md).

<!--- TBD: For quick scanning, see if the above information can be itemized as a list.
--->

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Bots y SDK](~/bots/bot-features.md)

## <a name="code-samples"></a>Ejemplos de código

|Ejemplo de nombre | Descripción | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| Recordatorio diario de tareas del bot| Demostrar cómo programar una tarea periódica y recibir un recordatorio a una hora programada. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/nodejs) |
| bot de Hola mundo | Se trata de una sencilla aplicación hello world con funcionalidades de extensión Bot y Message. |  | [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/v1.0.0/hello-world-bot) |
| Notificación de tarjeta adaptable | Este es un ejemplo que muestra cómo enviar notificaciones con diferentes tarjetas adaptables mediante bots. |  | [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/v1.0.0/adaptive-card-notification) |
| Notificación de webhook entrante | Este es un ejemplo que muestra cómo enviar notificaciones a través de Webhook entrante en canales de Microsoft Teams. |  | [Ver](https://github.com/OfficeDev/TeamsFx-Samples/tree/v1.0.0/incoming-webhook-notification) |

## <a name="see-also"></a>Consulte también

* [Creación de un bot para Teams](../resources/bot-v3/bots-create.md)
* [Cómo funcionan los bots de Microsoft Teams](/azure/bot-service/bot-builder-basics-teams)
* [Registro de llamadas y bots de reuniones para Microsoft teams](~/bots/calls-and-meetings/registering-calling-bot.md)
* [Agregar autenticación al bot de Teams](~/bots/how-to/authentication/add-authentication.md)
* [Controladores de actividad de bots](~/bots/bot-basics.md)
* [Eventos de conversación en el bot de Teams](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* [Cree su primera aplicación de bot con JavaScript](../sbs-gs-bot.yml)
* [Crear un bot de notificaciones con JavaScript](../sbs-gs-notificationbot.yml)

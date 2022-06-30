---
title: Bots en Microsoft Teams
author: surbhigupta
description: Con esta ruta de aprendizaje, empiece a trabajar con bots conversacionales en Microsoft Teams y sus ejemplos de código.
ms.topic: overview
ms.localizationpriority: high
ms.author: anclear
ms.openlocfilehash: 6eea7c4d42ff63e11b5096542271e22d3e71328c
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503763"
---
# <a name="build-bots-for-teams"></a>Crear bots para Teams

Un bot también se conoce como bot de chat o bot de conversación. Es una aplicación que ejecuta tareas sencillas y repetitivas de usuarios como, por ejemplo, el servicio de atención al cliente o el personal de soporte técnico. Los bots se usan a diario para, por ejemplo, proporcionar información sobre el tiempo, reservar cenas o facilitar información sobre viajes. Las interacciones con bots pueden ser preguntas y respuestas rápidas o conversaciones complejas.

> [!IMPORTANT]
> Actualmente, los bots están disponibles en Government Community Cloud (GCC) y GCC-High, pero no en el Departamento de defensa (DOD).
>
> Las aplicaciones de bots en Microsoft Teams están disponibles en GCC-High a través de [Azure Bot Service](/azure/bot-service/channel-connect-teams).

Los bots de conversación permiten que los usuarios interactúen con el servicio web mediante texto, tarjetas interactivas y módulos de tareas.

:::image type="content" source="../assets/images/invokebotwithtext.png" alt-text="Servicio web mediante texto"lightbox="../assets/images/invokebotwithtext.png":::

:::image type="content" source="../assets/images/invokebotwithcard.png" alt-text="Servicio web mediante tarjetas interactivas"lightbox="../assets/images/invokebotwithcard.png"border="true":::

:::image type="content" source="../assets/images/task-module-example.png" alt-text="Servicio web mediante módulo de tareas"lightbox="../assets/images/task-module-example.png"border="true":::

Los bots de conversación están dotados de gran flexibilidad. Los bots pueden controlar algunos comandos básicos y tareas más complejas que implican inteligencia artificial y procesamiento de lenguaje natural. Los bots pueden formar parte de una aplicación más grande o ser independientes.

Use la combinación correcta de tarjetas, texto y módulos de tareas para crear un bot que sea útil. En la siguiente imagen se muestra a un usuario conversando con un bot en un chat individual con texto y tarjetas interactivas.

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="Bot de preguntas frecuentes de ejemplo" border="true":::

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
| Recordatorio diario de tareas del bot| Demostrar cómo programar una tarea periódica y recibir un recordatorio a una hora programada. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/csharp) | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/nodejs) |

## <a name="see-also"></a>Consulte también

* [Creación de un bot para Teams](../resources/bot-v3/bots-create.md)
* [Cómo funcionan los bots de Microsoft Teams](/azure/bot-service/bot-builder-basics-teams)
* [Registro de llamadas y bots de reuniones para Microsoft teams](~/bots/calls-and-meetings/registering-calling-bot.md)
* [Agregar autenticación al bot de Teams](~/bots/how-to/authentication/add-authentication.md)
* [Controladores de actividad de bots](~/bots/bot-basics.md)
* [Eventos de conversación en el bot de Teams](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

---
title: Bots en Microsoft Teams
author: surbhigupta
description: Una introducción a los bots en Microsoft Teams.
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: a9f53654ba3240b973b77c05cd64a22c80237350
ms.sourcegitcommit: a6c39106ccc002d02a65e11627659e0c48981d8a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/13/2022
ms.locfileid: "62014566"
---
# <a name="bots-in-microsoft-teams"></a>Bots en Microsoft Teams

Un bot también se conoce como bot de chat o bot conversacional. Es una aplicación que ejecuta tareas sencillas y repetitivas por parte de los usuarios, como el servicio de atención al cliente o el personal de soporte técnico. El uso diario de bots incluye bots que proporcionan información sobre el tiempo, reservan la cena o proporcionan información de viaje. Las interacciones con bots pueden responder y preguntas rápidas o pueden ser una conversación compleja.

> [!IMPORTANT]
> Actualmente, los bots están disponibles en Government Community Cloud (GCC) y no están disponibles en GCC-High y departamento de defensa (DOD).

Los bots conversacionales permiten a los usuarios interactuar con el servicio web mediante texto, tarjetas interactivas y módulos de tareas.

![Invocar bot con texto](~/assets/images/invokebotwithtext.png)

![Invocar bot con tarjeta](~/assets/images/invokebotwithcard.png)

<img src="~/assets/images/task-module-example.png" alt="Invoke bot using task module" width="400"/>

Los bots conversacionales son increíblemente flexibles. Los bots pueden controlar algunos comandos básicos o tareas complejas que implican inteligencia artificial y procesamiento de lenguaje natural. Los bots pueden formar parte de una aplicación más grande o ser independientes.

Use la combinación correcta de tarjetas, texto y módulos de tareas para crear un bot útil. En la siguiente imagen se muestra a un usuario conversando con un bot en un chat uno a uno con texto y tarjetas interactivas.

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="Bot de preguntas frecuentes de ejemplo" border="true":::

Cada interacción entre el usuario y el bot se representa como una actividad. Cuando un bot recibe una actividad, la pasa a sus controladores de actividad. Vea [controladores de actividad de bot](~/bots/bot-basics.md).

Los bots son aplicaciones que tienen una interfaz de conversación. Puedes interactuar con un bot con texto, tarjetas interactivas y voz. Un bot se comporta de forma diferente en una conversación de chat de canal o grupo y en una conversación uno a uno. Las conversaciones se controlan a través del conector de Bot Framework. Vea [conceptos básicos de la conversación](~/bots/how-to/conversations/conversation-basics.md).

El bot requiere información contextual, como los detalles del perfil de usuario para tener acceso al contenido relevante y mejorar la experiencia del bot. Vea [obtener Teams contexto](~/bots/how-to/get-teams-context.md).

Puede enviar y recibir archivos a través del bot Graph API o Teams API de bot. Vea [enviar y recibir archivos a través del bot](~/bots/how-to/bots-filesv4.md).

La limitación de velocidad se usa para optimizar los bots usados para la Teams aplicación. Para proteger Microsoft Teams y sus usuarios, las API del bot proporcionan un límite de velocidad para las solicitudes entrantes. Consulta [optimizar el bot con limitación de](~/bots/how-to/rate-limit.md)velocidad en Teams .

Con las API Graph Microsoft para llamadas y reuniones en línea, Microsoft Teams aplicaciones ahora pueden interactuar con los usuarios mediante voz y vídeo. Vea [bots de llamadas y reuniones](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).

Puedes usar las API Teams bot para obtener información para los miembros de un chat o equipo. Vea [cambios en las API Teams bot para obtener miembros de equipo o chat.](~/resources/team-chat-member-api-changes.md)

<!--- TBD: For quick scanning, see if the above information can be itemized as a list.
--->

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Bots y SDK](~/bots/bot-features.md)

## <a name="code-sample"></a>Ejemplo de código

|Ejemplo de nombre | Descripción | C # | Node.js |
|----------------|-----------------|--------------|--------------|
| Aviso de tarea diaria del bot| Muestra cómo programar una tarea periódica y obtener un aviso a una hora programada. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/csharp) | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/nodejs) |

## <a name="see-also"></a>Consulte también

* [Creación de un bot para Teams](~/bots/how-to/create-a-bot-for-teams.md)
* [Registrar llamadas y reuniones bot para Microsoft Teams](~/bots/calls-and-meetings/registering-calling-bot.md)
* [Agregar autenticación al bot Teams usuario](~/bots/how-to/authentication/add-authentication.md)
* [Controladores de actividad de bots](~/bots/bot-basics.md)
* [Eventos de conversación en el bot de Teams](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

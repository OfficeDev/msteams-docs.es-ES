---
title: Bots en Microsoft Teams
author: clearab
description: Una introducción a los bots en Microsoft Teams.
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 70240b7396fc5e7a77749dc4e7326bfb30ea4415
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020894"
---
# <a name="bots-in-microsoft-teams"></a>Bots en Microsoft Teams

Un bot también conocido como bot de chat o bot de conversación es una aplicación que ejecuta tareas automatizadas simples y repetitivas realizadas por los usuarios, como el servicio de atención al cliente o el personal de soporte técnico. Algunos ejemplos de bots de uso diario incluyen bots que proporcionan información sobre el tiempo, reservan la cena o proporcionan información de viaje. Una interacción de bot puede ser una pregunta y una respuesta rápidas, o puede ser una conversación compleja que proporciona acceso a los servicios.

> [!VIDEO https://www.youtube-nocookie.com/embed/zSIysk0yL0Q]

Los robots de conversación permiten que los usuarios interactúen con el servicio web mediante texto, tarjetas interactivas y módulos de tareas.

![Invocar bot con texto](~/assets/images/invokebotwithtext.png)

![Invocar bot con tarjeta](~/assets/images/invokebotwithcard.png)

<img src="~/assets/images/task-module-example.png" alt="Invoke bot using task module" width="400"/>

Los bots conversacionales son increíblemente flexibles y se pueden tener en cuenta para controlar algunos comandos simples o tareas complejas, basadas en inteligencia artificial y procesamiento de lenguaje natural. Pueden ser un aspecto de una aplicación más grande o ser completamente independientes.

Encontrar la combinación adecuada de tarjetas, texto y módulos de tareas es clave para crear un bot útil. En la siguiente imagen se muestra a un usuario conversando con un bot en un chat uno a uno con tarjetas interactivas y de texto:

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="Bot de preguntas frecuentes de ejemplo" border="true":::

Cada interacción entre el usuario y el bot se representa como una actividad. Cuando un bot recibe una actividad, la pasa a sus controladores de actividad. Para obtener más información, vea [controladores de actividad de bot .](~/bots/bot-basics.md) 

Además, los bots son aplicaciones que tienen una interfaz de conversación. Puedes interactuar con un bot con texto, tarjetas interactivas y voz. Un bot se comporta de forma diferente en función de si la conversación es un canal o una conversación de chat de grupo, o si es una conversación uno a uno. Las conversaciones se controlan a través del conector de Bot Framework. Para obtener más información, vea [conceptos básicos de la conversación](~/bots/how-to/conversations/conversation-basics.md).

El bot requiere información contextual, como los detalles del perfil de usuario para tener acceso al contenido relevante y mejorar la experiencia del bot. Para obtener más información, vea [obtener el contexto de Teams](~/bots/how-to/get-teams-context.md). 

También puedes enviar y recibir archivos a través del bot mediante API de Graph o API de bots de Teams. Para obtener más información, [vea Enviar y recibir archivos a través del bot](~/bots/how-to/bots-filesv4.md).

Además, la limitación de velocidad se usa para optimizar los bots usados para la aplicación de Teams. Para proteger Microsoft Teams y sus usuarios, las API de bot proporcionan un límite de velocidad para las solicitudes entrantes. Para obtener más información, consulta [optimizar el bot con limitación de velocidad en Teams](~/bots/how-to/rate-limit.md).

Con las API de Microsoft Graph para llamadas y reuniones en línea, las aplicaciones de Microsoft Teams ahora pueden interactuar con los usuarios mediante voz y vídeo. Para obtener más información, vea [bots de llamadas y reuniones](~/bots/calls-and-meetings/calls-meetings-bots-overview.md). 

Puedes usar las API de bots de Teams para obtener información para uno o varios miembros de un chat o equipo. Para obtener más información, vea cambios en las API de bots de [Teams para obtener miembros de equipo o chat.](~/resources/team-chat-member-api-changes.md)

## <a name="see-also"></a>Consulte también

> [!div class="nextstepaction"]
> [Creación de un bot para Teams](~/bots/how-to/create-a-bot-for-teams.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Bots y SDK](~/bots/bot-features.md)

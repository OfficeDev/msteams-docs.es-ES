---
title: Bots en Microsoft Teams
author: surbhigupta
description: Una introducción a los bots en Microsoft Teams.
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 94540e4d9edd3cb41c249563d50780448d4e08dbe285967eaaece715930a29be
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2021
ms.locfileid: "57706247"
---
# <a name="bots-in-microsoft-teams"></a>Bots en Microsoft Teams

Un bot también conocido como bot de chat o bot de conversación es una aplicación que ejecuta tareas automatizadas simples y repetitivas realizadas por los usuarios, como el servicio de atención al cliente o el personal de soporte técnico. Algunos ejemplos de bots de uso diario incluyen bots que proporcionan información sobre el tiempo, reservan la cena o proporcionan información de viaje. Una interacción de bot puede ser una pregunta y una respuesta rápidas, o puede ser una conversación compleja que proporciona acceso a los servicios.

> [!IMPORTANT]
> Actualmente, los bots están disponibles en Government Community Cloud (GCC) pero no están disponibles en GCC-High departamento de defensa (DOD).

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

El bot requiere información contextual, como los detalles del perfil de usuario para tener acceso al contenido relevante y mejorar la experiencia del bot. Para obtener más información, vea [obtener Teams contexto](~/bots/how-to/get-teams-context.md). 

También puede enviar y recibir archivos a través del bot mediante Graph API o Teams API de bots. Para obtener más información, [vea Enviar y recibir archivos a través del bot](~/bots/how-to/bots-filesv4.md).

Además, la limitación de velocidad se usa para optimizar los bots usados para la Teams aplicación. Para proteger Microsoft Teams y sus usuarios, las API del bot proporcionan un límite de velocidad para las solicitudes entrantes. Para obtener más información, vea [optimizar el bot con limitación de](~/bots/how-to/rate-limit.md)velocidad en Teams .

Con las API Graph Microsoft para llamadas y reuniones en línea, Microsoft Teams aplicaciones ahora pueden interactuar con los usuarios mediante voz y vídeo. Para obtener más información, vea [bots de llamadas y reuniones](~/bots/calls-and-meetings/calls-meetings-bots-overview.md). 

Puede usar las API Teams bot para obtener información para uno o más miembros de un chat o equipo. Para obtener más información, vea [cambios en las API Teams bot para capturar miembros de equipo o chat.](~/resources/team-chat-member-api-changes.md)

## <a name="see-also"></a>Vea también

[Creación de un bot para Teams](~/bots/how-to/create-a-bot-for-teams.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Bots y SDK](~/bots/bot-features.md)

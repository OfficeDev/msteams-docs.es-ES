---
title: Conceptos básicos de la conversación
description: Introducción a las conversaciones
ms.topic: overview
ms.author: anclear
localization_priority: Normal
keyword: conversations basics messages
ms.openlocfilehash: 886c2764c2d8dceecb0f6a0e960b3487d9360c3682e46c9a8098f6fb8a2876bf
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2021
ms.locfileid: "57705864"
---
# <a name="conversation-basics"></a>Conceptos básicos de la conversación

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Una conversación es una serie de mensajes enviados entre el bot Microsoft Teams y uno o más usuarios. En la tabla siguiente se proporcionan los tres tipos de conversaciones, también denominadas ámbitos en Teams:

| Tipo de conversación | Descripción |
| ------- | ----------- |
| `channel` | Este tipo de conversación es visible para todos los miembros del canal. |
| `personal` | Este tipo de conversación incluye conversaciones entre bots y un solo usuario. |
| `groupChat` | Este tipo de conversación incluye chat entre un bot y dos o más usuarios. También habilita el bot en chats de reunión. |

Un bot se comporta de forma diferente en función de la conversación en la que esté implicado:

* Los bots en conversaciones de chat de canal y grupo requieren que el usuario lo @mencione para se lo invoque en un canal.

* Los bots de una conversación uno a uno no requieren una @mention. Todos los mensajes enviados por el usuario se enrutan al bot.

> [!NOTE]
> Los bots se pueden habilitar para recibir todos los mensajes de canal de un equipo sin que se @mentioned permisos de consentimiento específicos de recursos (RSC). Esta característica está disponible actualmente solo en [la versión preliminar del desarrollador](../../../resources/dev-preview/developer-preview-intro.md) público. Para obtener más información, vea [recibir todos los mensajes de canal con RSC](channel-messages-with-rsc.md).

Para que el bot funcione en una conversación o ámbito en particular, agregue compatibilidad a ese ámbito en el manifiesto [de la aplicación](~/resources/schema/manifest-schema.md).

Cada mensaje de una conversación de bot es `Activity` un objeto de tipo `messageType: message` . Cuando un usuario envía un mensaje, Teams el mensaje al bot y el bot lo controla. Además, para definir los comandos principales a los que responde el bot, puede agregar un menú de comandos con una lista desplegable de comandos para el bot. Los bots de un grupo o canal solo reciben mensajes cuando se mencionan @botname. Teams envía notificaciones al bot para eventos de conversación que se suceden en ámbitos donde el bot está activo. Puede capturar estos eventos en el código y realizar acciones en ellos.

Un bot también puede enviar mensajes proactivos a los usuarios. Un mensaje proactivo es cualquier mensaje enviado por un bot que no responde a una solicitud de un usuario. Puedes dar formato a los mensajes del bot para que incluyan tarjetas enriquecciones que incluyan elementos interactivos, como botones, texto, imágenes, audio, vídeo, entre otros. Bot puede actualizar dinámicamente los mensajes después de enviarlos, en lugar de tener los mensajes como instantáneas estáticas de datos. Los mensajes también se pueden eliminar mediante el método de Bot `DeleteActivity` Framework.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Mensajes en conversaciones de bot](~/bots/how-to/conversations/conversation-messages.md)

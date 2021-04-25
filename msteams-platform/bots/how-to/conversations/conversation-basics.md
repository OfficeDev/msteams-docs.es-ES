---
title: Conceptos básicos de la conversación
description: Introducción a las conversaciones
ms.topic: overview
ms.author: anclear
keyword: conversations basics messages
ms.openlocfilehash: eff1c6fe18f7b2ba082b5075b6c1806f41b68a6b
ms.sourcegitcommit: dd2220f691029d043aaddfc7c229e332735acb1d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2021
ms.locfileid: "51996040"
---
# <a name="conversation-basics"></a>Conceptos básicos de la conversación

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Una conversación es una serie de mensajes enviados entre el bot de Microsoft Teams y uno o varios usuarios. En la tabla siguiente se proporcionan los tres tipos de conversaciones, también denominadas ámbitos en Teams:

| Tipo de conversación | Descripción |
| ------- | ----------- |
| `channel` | Este tipo de conversación es visible para todos los miembros del canal. |
| `personal` | Este tipo de conversación incluye conversaciones entre bots y un solo usuario. |
| `groupChat` | Este tipo de conversación incluye chat entre un bot y dos o más usuarios. También habilita el bot en chats de reunión. |

Un bot se comporta de forma diferente en función de la conversación en la que esté implicado:

* Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.
* Los bots de una conversación uno a uno no requieren una mención @. Todos los mensajes enviados por el usuario se enrutan al bot.

Para que el bot funcione en una conversación o ámbito en particular, agregue compatibilidad a ese ámbito en el manifiesto [de la aplicación](~/resources/schema/manifest-schema.md).

Cada mensaje de una conversación de bot es `Activity` un objeto de tipo `messageType: message` . Cuando un usuario envía un mensaje, Teams publica el mensaje en el bot y el bot controla el mensaje. Además, para definir los comandos principales a los que responde el bot, puede agregar un menú de comandos con una lista desplegable de comandos para el bot. Los bots de un grupo o canal solo reciben mensajes cuando se mencionan @botname. Teams envía notificaciones al bot para eventos de conversación que se suceden en ámbitos donde el bot está activo. Puede capturar estos eventos en el código y realizar acciones en ellos. 

Un bot también puede enviar mensajes proactivos a los usuarios. Un mensaje proactivo es cualquier mensaje enviado por un bot que no responde a una solicitud de un usuario. Puedes dar formato a los mensajes del bot para que incluyan tarjetas enriquecciones que incluyan elementos interactivos, como botones, texto, imágenes, audio, vídeo, entre otros. Bot puede actualizar dinámicamente los mensajes después de enviarlos, en lugar de tener los mensajes como instantáneas estáticas de datos. Los mensajes también se pueden eliminar mediante el método de Bot `DeleteActivity` Framework.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Mensajes en conversaciones de bot](~/bots/how-to/conversations/conversation-messages.md)

---
title: Conceptos básicos de la conversación
description: En este módulo, obtenga información sobre el tipo de conversación del bot en un canal, chat personal y ámbitos de chat de grupo en Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: 23a72486ffb76d207eeabbef23b5ec5238234dc4
ms.sourcegitcommit: b918181217995a47be34632e1051d0f4d4d481b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2022
ms.locfileid: "67321218"
---
# <a name="conversation-basics"></a>Conceptos básicos de la conversación

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Una conversación es una serie de mensajes enviados entre el bot de Microsoft Teams y uno o varios usuarios. En la tabla siguiente se proporcionan los tres tipos de conversaciones, también denominadas ámbitos en Teams:

| Tipo de conversación | Descripción |
| ------- | ----------- |
| `channel` | Este tipo de conversación es visible para todos los miembros del canal. |
| `personal` | Este tipo de conversación incluye conversaciones entre bots y un único usuario. |
| `groupChat` | Este tipo de conversación incluye el chat entre un bot y dos o más usuarios. También habilita el bot en los chats de reuniones. |

Un bot se comporta de forma diferente en función de la conversación en la que esté implicado:

* Los bots en conversaciones de chat de canal y grupo requieren que el usuario lo @mencione para se lo invoque en un canal.

* Los bots de una conversación uno a uno no requieren un @mention. Todos los mensajes enviados por el usuario se enrutan al bot.

> [!NOTE]
> Los bots se pueden habilitar para recibir todos los mensajes de canal de un equipo sin @mentioned mediante permisos de consentimiento específico de recursos (RSC). Esta característica solo está disponible actualmente en la [versión preliminar para desarrolladores públicos](../../../resources/dev-preview/developer-preview-intro.md). Para obtener más información, consulte [Recepción de todos los mensajes del canal con RSC](channel-messages-with-rsc.md).

Para que el bot funcione en una conversación o ámbito determinados, agregue compatibilidad a ese ámbito en el manifiesto de la [aplicación](~/resources/schema/manifest-schema.md).

Cada mensaje de una conversación de bot es un `Activity` objeto de tipo `messageType: message`. Cuando un usuario envía un mensaje, Teams publica el mensaje en el bot y el bot controla el mensaje. Además, para definir los comandos principales a los que responde el bot, puede agregar un menú de comandos con una lista desplegable de comandos para el bot. Los bots de un grupo o canal solo reciben mensajes cuando se menciona @botname. Microsoft Teams envía notificaciones al bot para los eventos que se suceden en ámbitos donde el bot está activo. Puede capturar estos eventos en el código y tomar medidas en ellos.

Un bot también puede enviar mensajes proactivos a los usuarios. Un mensaje proactivo es cualquier mensaje enviado por un bot que no responde a una solicitud de un usuario. Puede dar formato a los mensajes del bot para incluir tarjetas enriquecidas que incluyan elementos interactivos, como botones, texto, imágenes, audio, vídeo, etc. El bot puede actualizar dinámicamente los mensajes después de enviarlos, en lugar de tener los mensajes como instantáneas estáticas de datos. Los mensajes también se pueden eliminar mediante el método `DeleteActivity` de Bot Framework.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Mensajes en conversaciones de bot](~/bots/how-to/conversations/conversation-messages.md)

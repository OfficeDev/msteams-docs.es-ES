---
title: conversaciones 1 a 1 con bots
description: Describe el escenario de un extremo a otro de tener una conversación de 1 en 1 con un bot en Microsoft Teams.
keywords: escenarios de Microsoft Teams 1on1 de 1to1 de conversación
ms.date: 05/20/2019
ms.openlocfilehash: e23bb98160125d7fdbb4521467e2f522d6b6ce40
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676204"
---
# <a name="have-a-personal-one-on-one-conversation-with-a-microsoft-teams-bot"></a>Tener una conversación personal (uno a uno) con un bot de Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams permite a los usuarios participar en conversaciones directas con bots integrados en [Microsoft bot Framework](/azure/bot-service/?view=azure-bot-service-3.0). Los usuarios pueden encontrar bots en la galería de aplicaciones de Discover y agregarlos a la experiencia de Microsoft Teams para conversaciones personales. Los propietarios de equipo y los usuarios con los permisos adecuados también pueden agregar bots como miembros del equipo (consulte [interactuar en un canal de equipo](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)), lo que no solo los hace disponibles en los canales del equipo, sino también para chats personales para todos los usuarios.

Chat personal difiere de chat en los canales en el que el usuario no necesita @mention el bot. Si se usa un bot en varios contextos (personales, groupChat o Channel), tendrá que detectar si el bot se encuentra en un canal o un chat de grupo y procesar los mensajes de forma un poco diferente. Para obtener más información, consulte [interactuar en un canal de equipo o un chat en grupo](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) .

## <a name="designing-a-great-personal-bot"></a>Diseño de un gran robot personal

Un gran bot en Microsoft Teams ayuda a los usuarios a obtener la información que necesitan, todo ello en el contexto de la experiencia de Microsoft Teams. Las conversaciones personales con un bot son intercambios privados entre un bot y su usuario; son una buena forma de proporcionar información específica y relevante para ese usuario en el contexto personal. Un bot en chat personal es, en realidad, un cuadro de diálogo entre su servicio y el individuo, donde un bot en un canal o un chat de grupo difunde todo a un grupo de personas.

En función de la experiencia que desee crear, es posible que el bot deba funcionar en varios ámbitos: personal, groupChat o Team. El trabajo para admitir más de un ámbito es mínimo. No existe ninguna expectativa en Teams de que su bot funcione en todos los ámbitos, pero debe asegurarse de que su bot tiene sentido y proporciona valor de usuario en el ámbito o los ámbitos que desee admitir.

## <a name="best-practice-welcome-messages-in-personal-conversations"></a>Procedimiento recomendado: mensajes de bienvenida en conversaciones personales

El bot debe [enviar de forma proactiva](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) un mensaje de bienvenida a un chat personal la primera vez (y sólo la primera vez) que un usuario inicie un chat personal con su bot. (Esta recomendación no se aplica a los contactos por primera vez en un canal).

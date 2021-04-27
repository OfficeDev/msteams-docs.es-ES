---
title: Conversaciones 1 a 1 con bots
description: Describe el escenario completo de tener una conversación 1 a 1 con un bot en Microsoft Teams
keywords: teams scenarios 1on1 1to1 conversation bot
localization_priority: Normal
ms.topic: conceptual
ms.date: 05/20/2019
ms.openlocfilehash: 2942a6c53bc99ce3199e140263d939e8b16d9db6
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020677"
---
# <a name="have-a-personal-one-on-one-conversation-with-a-microsoft-teams-bot"></a>Tener una conversación personal (uno a uno) con un bot de Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams permite a los usuarios participar en conversaciones directas con bots integrados en [Microsoft Bot Framework.](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true) Los usuarios pueden encontrar bots en la galería Descubrir aplicaciones y agregarlos a su experiencia de Teams para conversaciones personales. Los propietarios del equipo y los usuarios con los permisos adecuados también pueden agregar bots como miembros del equipo (consulta [Interactuar](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)en un canal de grupo), lo que no solo los hace disponibles en los canales de ese equipo, sino también para chat personal para todos esos usuarios.

El chat personal difiere del chat en canales en que el usuario no necesita @mention el bot. Si un bot se usa en varios contextos (personal, groupChat o canal), deberá detectar si el bot está en un canal o chat de grupo y procesar mensajes de forma un poco diferente. Consulta [Interactuar en un chat de grupo o canal de grupo](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) para obtener más información.

## <a name="designing-a-great-personal-bot"></a>Diseño de un gran bot personal

Un excelente bot en Microsoft Teams ayuda a los usuarios a obtener la información que necesitan, todo dentro del contexto de la experiencia de Teams. Las conversaciones personales con un bot son intercambios privados entre un bot y su usuario; son una excelente manera de proporcionar información específica y relevante para ese usuario en el contexto personal. Un bot en el chat personal es realmente un cuadro de diálogo entre el servicio y el individuo, donde un bot en un chat de grupo o canal transmite todo a un grupo de personas.

Según la experiencia que quieras crear, es posible que el bot necesite trabajar en varios ámbitos: personal, groupChat o equipo. El trabajo para admitir más de un ámbito es mínimo. En Teams no hay ninguna expectativa de que el bot funcione en todos los ámbitos, pero debe asegurarse de que el bot tiene sentido y proporciona valor de usuario en los ámbitos que elija admitir.

## <a name="best-practice-welcome-messages-in-personal-conversations"></a>Procedimiento recomendado: Recibir mensajes en conversaciones personales

El bot debe [enviar de](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) forma proactiva un mensaje de bienvenida a un chat personal la primera vez (y solo la primera vez) que un usuario inicie un chat personal con el bot. (Esta recomendación no se aplica a los contactos por primera vez en un canal).

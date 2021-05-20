---
title: 1 contra 1 conversaciones con bots
description: Describe el escenario de extremo a extremo de tener una conversación 1 contra 1 con un bot en Microsoft Teams
keywords: escenarios de equipos 1on1 1to1 bot de conversación
localization_priority: Normal
ms.topic: conceptual
ms.date: 05/20/2019
ms.openlocfilehash: dff65e919485eff0443032995b934b7ae93c64eb
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566505"
---
# <a name="have-a-personal-one-on-one-conversation-with-a-microsoft-teams-bot"></a>Tener una conversación personal (uno a uno) con un bot Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams permite a los usuarios entablar conversaciones directas con bots construidos en el [Microsoft Bot Framework.](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true) Los usuarios pueden encontrar bots en la galería Discover Apps y agregarlos a su experiencia Teams para conversaciones personales. Los propietarios de equipos y los usuarios con los permisos adecuados también pueden agregar bots como miembros del equipo. Para obtener más información, consulte Interactuar en un canal de [equipo),](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)que no solo los pone a disposición en los canales de ese equipo, sino también para el chat personal para todos esos usuarios.

El chat personal difiere del chat en canales en los que el usuario no necesita @mention el bot. Si se utiliza un bot en varios contextos como personal, groupChat o canal, debe detectar si el bot está en un chat o canal grupal y procesar mensajes un poco diferente. Para obtener más información, consulte [Interactuar en un canal de equipo o chat de grupo.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)

## <a name="designing-a-great-personal-bot"></a>Diseñar un gran bot personal

Un gran bot en Microsoft Teams ayuda a los usuarios a obtener la información que necesitan, todo en el contexto de la experiencia Teams. Las conversaciones personales con un bot son intercambios privados entre un bot y su usuario; son una gran manera de proporcionar información específica y relevante para ese usuario en el contexto personal. Un bot en el chat personal es realmente un diálogo entre su servicio y el individuo, donde un bot en un chat de grupo o canal transmite todo a un grupo de personas.

Dependiendo de la experiencia que desee crear, es posible que el bot deba trabajar en varios ámbitos: personal, groupchat y equipo. El trabajo para admitir más de un ámbito es mínimo. No hay ninguna expectativa en Teams que el bot funcione en todos los ámbitos, pero debe asegurarse de que el bot tiene sentido y proporciona valor de usuario en los ámbitos que elija admitir.

## <a name="best-practice-welcome-messages-in-personal-conversations"></a>Mejores prácticas: Mensajes de bienvenida en conversaciones personales

El bot debe [enviar proactivamente](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) un mensaje de bienvenida a un chat personal la primera vez (y solo la primera vez) que un usuario inicia un chat personal con su bot. Esta recomendación no se aplica a los contactos por primera vez en un canal.

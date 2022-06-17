---
title: Conversaciones uno a uno con bots
description: En este módulo, aprenderá el escenario de un extremo a otro de tener una conversación uno a uno con un bot en Microsoft Teams
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 05/20/2019
ms.openlocfilehash: e973e335558a54187a11d5146b52c5774d3cf758
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144330"
---
# <a name="have-a-personal-one-on-one-conversation-with-a-microsoft-teams-bot"></a>Tener una conversación personal (uno a uno) con un bot de Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams permite a los usuarios interactuar en conversaciones directas con bots basados en el [Microsoft Bot Framework](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true). Los usuarios pueden encontrar bots en la galería Detección de aplicaciones y agregarlos a su experiencia de Teams para conversaciones personales. Los propietarios del equipo y los usuarios con los permisos adecuados también pueden agregar bots como miembros del equipo. Para obtener más información, consulte [Interactuar en un canal de equipo](~/resources/bot-v3/bot-conversations/bots-conv-channel.md), que no solo los hace disponibles en los canales de ese equipo, sino también para los usuarios de chat personales.

El chat personal difiere del chat en los canales en que el usuario no necesita @mention el bot. Si se usa un bot en varios contextos, como en los ámbitos siguientes:
* Personal
* Chat de grupo
* Canal

Debe detectar si el bot está en un chat de grupo o canal y procesar los mensajes de forma un poco diferente. Para obtener más información, consulte [Interacción en un canal de equipo o chat grupal](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).

## <a name="designing-a-great-personal-bot"></a>Diseño de un bot personal excelente

Un bot excelente en Microsoft Teams ayuda a los usuarios a obtener la información que necesitan, todo ello en el contexto de la experiencia Teams. Las conversaciones personales con un bot son intercambios privados entre un bot y su usuario; son una excelente manera de proporcionar información específica y relevante para ese usuario en el contexto personal. Un bot en chat personal es un diálogo entre el servicio y el individuo, donde un bot en un chat grupal o canal difunde todo a un grupo de personas.

En función de la experiencia que quiera crear, es posible que el bot tenga que trabajar en varios ámbitos: personal, chat grupal y equipo. El trabajo para admitir más de un ámbito es mínimo. No hay ninguna expectativa en Teams que el bot funcione en todos los ámbitos, pero debe asegurarse de que el bot tiene sentido y proporciona valor de usuario en los ámbitos que elija admitir.

## <a name="best-practice-welcome-messages-in-personal-conversations"></a>Procedimiento recomendado: Mensajes de bienvenida en conversaciones personales

El bot debe [enviar de forma proactiva](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)un mensaje de bienvenida a un chat personal la primera vez (y solo la primera vez) que un usuario inicie un chat personal con el bot. Esta recomendación no se aplica a los contactos de primera vez en un canal.

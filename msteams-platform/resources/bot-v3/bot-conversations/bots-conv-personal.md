---
title: Conversaciones 1 a 1 con bots
description: Describe el escenario completo de tener una conversación 1 a 1 con un bot en Microsoft Teams
keywords: teams scenarios 1on1 1to1 conversation bot
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 05/20/2019
ms.openlocfilehash: 2fd76b8bc5fa4cd260b70e15b92bef2dec2de683
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157079"
---
# <a name="have-a-personal-one-on-one-conversation-with-a-microsoft-teams-bot"></a>Tener una conversación personal (uno a uno) con un bot Microsoft Teams personal

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams permite a los usuarios participar en conversaciones directas con bots integrados en el [Microsoft Bot Framework](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true). Los usuarios pueden encontrar bots en la galería Descubrir aplicaciones y agregarlos a su Teams experiencia para conversaciones personales. Los propietarios del equipo y los usuarios con los permisos adecuados también pueden agregar bots como miembros del equipo. Para obtener más información, consulta [Interactuar](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)en un canal de grupo ), que no solo los hace disponibles en los canales de ese equipo, sino también para chat personal para todos esos usuarios.

El chat personal difiere del chat en canales en que el usuario no necesita @mention el bot. Si un bot se usa en varios contextos como personal, groupChat o canal, debes detectar si el bot está en un canal o chat de grupo y procesar mensajes de forma un poco diferente. Para obtener más información, vea [Interact in a team channel or group chat](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).

## <a name="designing-a-great-personal-bot"></a>Diseño de un gran bot personal

Un excelente bot en Microsoft Teams ayuda a los usuarios a obtener la información que necesitan, todo en el contexto de la Teams experiencia. Las conversaciones personales con un bot son intercambios privados entre un bot y su usuario; son una excelente manera de proporcionar información específica y relevante para ese usuario en el contexto personal. Un bot en el chat personal es realmente un cuadro de diálogo entre el servicio y el individuo, donde un bot en un chat de grupo o canal transmite todo a un grupo de personas.

Según la experiencia que quieras crear, es posible que el bot necesite trabajar en varios ámbitos: personal, groupchat y team. El trabajo para admitir más de un ámbito es mínimo. No hay ninguna expectativa en Teams que el bot funcione en todos los ámbitos, pero debe asegurarse de que el bot tiene sentido y proporciona valor de usuario en los ámbitos que elija admitir.

## <a name="best-practice-welcome-messages-in-personal-conversations"></a>Procedimiento recomendado: Recibir mensajes en conversaciones personales

El bot debe [enviar de](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) forma proactiva un mensaje de bienvenida a un chat personal la primera vez (y solo la primera vez) que un usuario inicie un chat personal con el bot. Esta recomendación no se aplica a los contactos por primera vez en un canal.

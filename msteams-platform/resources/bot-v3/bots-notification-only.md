---
title: Bots solo de notificación
description: Describe qué son los bots que son para la notificación en Microsoft Teams
keywords: notificación de los bots de Microsoft Teams
ms.date: 05/20/2019
ms.openlocfilehash: 37652bc2d6171191c81be4e5a2875f47c79574f9
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675747"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>Notificar solo bots en Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Si el único propósito de su bot es entregar notificaciones a los usuarios y no es de conversación, puede habilitar `isNotificationOnly` el campo en el manifiesto de la aplicación. Esto produce los siguientes cambios:

* Los usuarios no pueden recibir mensajes de un bot de solo notificación.
* Los usuarios no pueden @mention el bot.

## <a name="app-manifest"></a>Manifiesto de la aplicación

Para habilitar esto, establezca `isNotificationOnly` en `true`.

> [!NOTE]
> Tenga en cuenta que el valor `isNotificationOnly` de es Boolean y no de String.

```json
{
  ⋮
  "bots":[
    {
      "botId":"[Microsoft App ID for your bot]",
      "isNotificationOnly": true,
      "scopes": [
        "personal",
        "team"
      ],
    }
  ],
  ...
}
```

## <a name="best-practices-and-limitations"></a>Procedimientos recomendados y limitaciones

* No se puede crear `personal` un bot de solo notificación con ámbito, ya que el usuario no puede notificar el bot solo de notificación en un chat personal. Esto significa que no puede recibir un `conversationUpdate` evento que le proporcione los detalles necesarios para enviar una notificación. El bot de solo notificación solo funcionará correctamente si admite el `team` ámbito y se agrega a un equipo. En la configuración de equipo, el bot tendrá acceso a la información necesaria para enviar una notificación a un canal o de forma privada a un usuario.
* Notificación solo los bots usan la mensajería proactiva para comunicarse con el usuario. Para obtener más información, vea [Mensajería proactiva para bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) .

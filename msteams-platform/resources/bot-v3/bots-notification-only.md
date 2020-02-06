---
title: Bots de solo notificación
description: Describe los bots de solo notificación en Microsoft Teams
keywords: notificación de los bots de Microsoft Teams
ms.date: 01/29/2020
ms.openlocfilehash: d312f9cd4558d35fc2492b5cf0b4f77b65660833
ms.sourcegitcommit: 44ac886c0ca34a16222d3991a61606f8483b8481
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/05/2020
ms.locfileid: "41783909"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>Bots de solo notificación en Microsoft Teams

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

* Los bots de solo notificación usan la mensajería proactiva para comunicarse con el usuario. Para obtener más información, vea [Mensajería proactiva para bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) .

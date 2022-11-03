---
title: Bots de solo notificación
description: En este módulo, obtenga información sobre qué son los bots de solo notificación en Microsoft Teams, el manifiesto de la aplicación y sus procedimientos recomendados y limitaciones.
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 01/29/2020
ms.openlocfilehash: ac412f37cba03c5da43163bf2eadd47adc676f08
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833019"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>Bots de solo notificación en Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Si el único propósito del bot es entregar notificaciones a los usuarios y no es conversacional, puede habilitar el campo en el `isNotificationOnly` manifiesto de la aplicación. Esto genera los siguientes cambios:

* Los usuarios no pueden enviar mensajes al bot de solo notificación.
* Los usuarios no pueden @mention el bot.

> [!NOTE]
> Las aplicaciones solo de bot aparecerán en la bandeja de la aplicación personal en ambos casos: `isNotificationOnly: true` o `isNotificationOnly: false`.

## <a name="app-manifest"></a>Manifiesto de la aplicación

Para habilitar esto, establezca `isNotificationOnly` en `true`.

> [!NOTE]
> El valor de `isNotificationOnly` es booleano y no una cadena.

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

Los bots de solo notificación usan mensajería proactiva para comunicarse con el usuario. Para más información, consulte [Mensajería proactiva para bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).

---
title: Bots de solo notificación
description: En este módulo, obtenga información sobre qué bots de solo notificación están en Microsoft Teams, manifiesto de aplicación y sus procedimientos recomendados y limitaciones.
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 01/29/2020
ms.openlocfilehash: 547ef73cfd036efe566afe15e4f50701a275c2cd
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144302"
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

* Los bots de solo notificación usan mensajería proactiva para comunicarse con el usuario. Para más información, consulte [Mensajería proactiva para bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).

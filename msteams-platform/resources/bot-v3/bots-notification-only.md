---
title: Bots de solo notificación
description: Describe qué bots de solo notificación están en Microsoft Teams
keywords: notificación de bots de teams
ms.topic: conceptual
localization_priority: Normal
ms.date: 01/29/2020
ms.openlocfilehash: 3de462f73733f5f7cf223444ffe6deeb53faaaaa
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566764"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>Bots de solo notificación en Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Si el único propósito del bot es entregar notificaciones a los usuarios y no es conversacional, puedes habilitar el campo `isNotificationOnly` en el manifiesto de la aplicación. Esto produce los siguientes cambios:

* Los usuarios no pueden enviar un mensaje al bot de solo notificación.
* Los usuarios no @mention el bot.

> [!NOTE]
> Las aplicaciones solo bot aparecerán en la bandeja de aplicaciones personal en ambos `isNotificationOnly: true` casos: o `isNotificationOnly: false` .

## <a name="app-manifest"></a>Manifiesto de la aplicación

Para habilitar esto, establezca `isNotificationOnly` en `true` .

> [!NOTE]
> Tenga en cuenta que el valor `isNotificationOnly` de es booleano y no una cadena.

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

* Los bots de solo notificación usan mensajería proactiva para comunicarse con el usuario. Para obtener más información, vea [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).

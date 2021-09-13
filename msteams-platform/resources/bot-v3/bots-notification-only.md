---
title: Bots de solo notificación
description: Describe qué bots de solo notificación están en Microsoft Teams
keywords: notificación de bots de teams
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 01/29/2020
ms.openlocfilehash: 71dbc07445a57194e90ba3985c3aff1e2d4f2cdf
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157081"
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

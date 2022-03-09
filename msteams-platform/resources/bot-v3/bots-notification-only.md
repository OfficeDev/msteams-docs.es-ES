---
title: Bots de solo notificación
description: Describe qué bots de solo notificación están en Microsoft Teams
keywords: notificación de bots de teams
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 01/29/2020
ms.openlocfilehash: d3ee5343ea159950859237f2a488557d9063eb6e
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2022
ms.locfileid: "63355730"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>Bots de solo notificación en Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Si el único propósito del bot es entregar notificaciones a los usuarios y no es conversacional, `isNotificationOnly` puedes habilitar el campo en el manifiesto de la aplicación. Esto produce los siguientes cambios:

* Los usuarios no pueden enviar un mensaje al bot de solo notificación.
* Los usuarios no @mention el bot.

> [!NOTE]
> Las aplicaciones solo bot aparecerán en la bandeja de aplicaciones personal en ambos casos: `isNotificationOnly: true` o `isNotificationOnly: false`.

## <a name="app-manifest"></a>Manifiesto de la aplicación

Para habilitar esto, establezca `isNotificationOnly` en `true`.

> [!NOTE]
> El valor de `isNotificationOnly` es Boolean y no una cadena.

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

* Los bots de solo notificación usan mensajería proactiva para comunicarse con el usuario. Para obtener más información, consulta [Mensajería proactiva para bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).

---
title: Bots de solo notificación
description: Describe qué bots solo de notificación hay en Microsoft Teams
keywords: notificación de bots de equipos
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
# <a name="notification-only-bots-in-microsoft-teams"></a><span data-ttu-id="5284f-104">Bots solo de notificación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="5284f-104">Notification-only bots in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="5284f-105">Si el único propósito del bot es entregar una notificación a los usuarios y no es conversacional, puede habilitar el campo en el `isNotificationOnly` manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5284f-105">If your bot's sole purpose is to deliver notification to users and is not conversational, you can enable the `isNotificationOnly` field in your app manifest.</span></span> <span data-ttu-id="5284f-106">Esto produce los siguientes cambios:</span><span class="sxs-lookup"><span data-stu-id="5284f-106">This produces the following changes:</span></span>

* <span data-ttu-id="5284f-107">Los usuarios no pueden enviar mensajes al bot de solo notificación.</span><span class="sxs-lookup"><span data-stu-id="5284f-107">Users cannot message your notification-only bot.</span></span>
* <span data-ttu-id="5284f-108">Los usuarios no pueden @mention el bot.</span><span class="sxs-lookup"><span data-stu-id="5284f-108">Users cannot @mention the bot.</span></span>

> [!NOTE]
> <span data-ttu-id="5284f-109">Las aplicaciones solo para bots aparecerán en la bandeja de aplicaciones personales en ambos casos: `isNotificationOnly: true` o `isNotificationOnly: false` .</span><span class="sxs-lookup"><span data-stu-id="5284f-109">The bot-only apps will surface in the personal app tray in both cases: `isNotificationOnly: true` or `isNotificationOnly: false`.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="5284f-110">Manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="5284f-110">App manifest</span></span>

<span data-ttu-id="5284f-111">Para habilitar esto, establezca `isNotificationOnly` en `true` .</span><span class="sxs-lookup"><span data-stu-id="5284f-111">To enable this, set `isNotificationOnly` to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="5284f-112">Tenga en cuenta que el valor de `isNotificationOnly` es booleano y no una cadena.</span><span class="sxs-lookup"><span data-stu-id="5284f-112">Be aware that the value of `isNotificationOnly` is boolean and not a string.</span></span>

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

## <a name="best-practices-and-limitations"></a><span data-ttu-id="5284f-113">Procedimientos recomendados y limitaciones</span><span class="sxs-lookup"><span data-stu-id="5284f-113">Best practices and limitations</span></span>

* <span data-ttu-id="5284f-114">Los bots de solo notificación usan mensajería proactiva para comunicarse con el usuario.</span><span class="sxs-lookup"><span data-stu-id="5284f-114">Notification-only bots use proactive messaging to communicate with the user.</span></span> <span data-ttu-id="5284f-115">Para obtener más información, consulte [Mensajería proactiva para bots.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)</span><span class="sxs-lookup"><span data-stu-id="5284f-115">For more information, see [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span></span>

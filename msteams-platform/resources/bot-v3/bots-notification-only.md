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
# <a name="notification-only-bots-in-microsoft-teams"></a><span data-ttu-id="d7e6f-104">Bots de solo notificación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d7e6f-104">Notification-only bots in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="d7e6f-105">Si el único propósito de su bot es entregar notificaciones a los usuarios y no es de conversación, puede habilitar `isNotificationOnly` el campo en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-105">If your bot's sole purpose is to deliver notification to users and is not conversational, you can enable the `isNotificationOnly` field in your app manifest.</span></span> <span data-ttu-id="d7e6f-106">Esto produce los siguientes cambios:</span><span class="sxs-lookup"><span data-stu-id="d7e6f-106">This produces the following changes:</span></span>

* <span data-ttu-id="d7e6f-107">Los usuarios no pueden recibir mensajes de un bot de solo notificación.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-107">Users cannot message your notification-only bot.</span></span>
* <span data-ttu-id="d7e6f-108">Los usuarios no pueden @mention el bot.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-108">Users cannot @mention the bot.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="d7e6f-109">Manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="d7e6f-109">App manifest</span></span>

<span data-ttu-id="d7e6f-110">Para habilitar esto, establezca `isNotificationOnly` en `true`.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-110">To enable this, set `isNotificationOnly` to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="d7e6f-111">Tenga en cuenta que el valor `isNotificationOnly` de es Boolean y no de String.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-111">Be aware that the value of `isNotificationOnly` is boolean and not a string.</span></span>

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

## <a name="best-practices-and-limitations"></a><span data-ttu-id="d7e6f-112">Procedimientos recomendados y limitaciones</span><span class="sxs-lookup"><span data-stu-id="d7e6f-112">Best practices and limitations</span></span>

* <span data-ttu-id="d7e6f-113">Los bots de solo notificación usan la mensajería proactiva para comunicarse con el usuario.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-113">Notification-only bots use proactive messaging to communicate with the user.</span></span> <span data-ttu-id="d7e6f-114">Para obtener más información, vea [Mensajería proactiva para bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) .</span><span class="sxs-lookup"><span data-stu-id="d7e6f-114">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more details.</span></span>

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
# <a name="notification-only-bots-in-microsoft-teams"></a><span data-ttu-id="8b872-104">Notificar solo bots en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8b872-104">Notification only bots in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="8b872-105">Si el único propósito de su bot es entregar notificaciones a los usuarios y no es de conversación, puede habilitar `isNotificationOnly` el campo en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8b872-105">If your bot's sole purpose is to deliver notification to users and is not conversational, you can enable the `isNotificationOnly` field in your app manifest.</span></span> <span data-ttu-id="8b872-106">Esto produce los siguientes cambios:</span><span class="sxs-lookup"><span data-stu-id="8b872-106">This produces the following changes:</span></span>

* <span data-ttu-id="8b872-107">Los usuarios no pueden recibir mensajes de un bot de solo notificación.</span><span class="sxs-lookup"><span data-stu-id="8b872-107">Users cannot message your notification only bot.</span></span>
* <span data-ttu-id="8b872-108">Los usuarios no pueden @mention el bot.</span><span class="sxs-lookup"><span data-stu-id="8b872-108">Users cannot @mention the bot.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="8b872-109">Manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="8b872-109">App manifest</span></span>

<span data-ttu-id="8b872-110">Para habilitar esto, establezca `isNotificationOnly` en `true`.</span><span class="sxs-lookup"><span data-stu-id="8b872-110">To enable this, set `isNotificationOnly` to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="8b872-111">Tenga en cuenta que el valor `isNotificationOnly` de es Boolean y no de String.</span><span class="sxs-lookup"><span data-stu-id="8b872-111">Be aware that the value of `isNotificationOnly` is boolean and not a string.</span></span>

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

## <a name="best-practices-and-limitations"></a><span data-ttu-id="8b872-112">Procedimientos recomendados y limitaciones</span><span class="sxs-lookup"><span data-stu-id="8b872-112">Best practices and limitations</span></span>

* <span data-ttu-id="8b872-113">No se puede crear `personal` un bot de solo notificación con ámbito, ya que el usuario no puede notificar el bot solo de notificación en un chat personal.</span><span class="sxs-lookup"><span data-stu-id="8b872-113">You cannot create a `personal` scoped notification only bot, as the user cannot message your notification only bot in a personal chat.</span></span> <span data-ttu-id="8b872-114">Esto significa que no puede recibir un `conversationUpdate` evento que le proporcione los detalles necesarios para enviar una notificación.</span><span class="sxs-lookup"><span data-stu-id="8b872-114">This means that you can't receive a `conversationUpdate` event that would provide you with the necessary details to send a notification.</span></span> <span data-ttu-id="8b872-115">El bot de solo notificación solo funcionará correctamente si admite el `team` ámbito y se agrega a un equipo.</span><span class="sxs-lookup"><span data-stu-id="8b872-115">Your notification only bot will only function correctly if it supports the `team` scope and is added to a team.</span></span> <span data-ttu-id="8b872-116">En la configuración de equipo, el bot tendrá acceso a la información necesaria para enviar una notificación a un canal o de forma privada a un usuario.</span><span class="sxs-lookup"><span data-stu-id="8b872-116">In the team setting, your bot will have access to the necessary information to either send a notification to a channel or privately to a user.</span></span>
* <span data-ttu-id="8b872-117">Notificación solo los bots usan la mensajería proactiva para comunicarse con el usuario.</span><span class="sxs-lookup"><span data-stu-id="8b872-117">Notification only bots use proactive messaging to communicate with the user.</span></span> <span data-ttu-id="8b872-118">Para obtener más información, vea [Mensajería proactiva para bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) .</span><span class="sxs-lookup"><span data-stu-id="8b872-118">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more details.</span></span>

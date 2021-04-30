---
title: Vistas actualizadas
description: Ejemplo de vistas actualizadas con Bot universal
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 2027d07961929fb40e7afc3ee268e1267b235a02
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088886"
---
# <a name="up-to-date-cards"></a><span data-ttu-id="04a5c-103">Tarjetas actualizadas</span><span class="sxs-lookup"><span data-stu-id="04a5c-103">Up to date cards</span></span>

<span data-ttu-id="04a5c-104">Ahora puede proporcionar información más reciente a los usuarios en tarjetas adaptables con una combinación de actualizaciones y ediciones de mensajes en Teams.</span><span class="sxs-lookup"><span data-stu-id="04a5c-104">You can now provide latest information to your users on Adaptive Cards with a combination of refresh and message edits in Teams.</span></span> <span data-ttu-id="04a5c-105">Con esto, puede actualizar dinámicamente las vistas específicas del usuario a su estado más reciente como y cuando hay un cambio en el servicio.</span><span class="sxs-lookup"><span data-stu-id="04a5c-105">With this you are able to update the User Specific Views dynamically to its latest state as and when there is a change on your service.</span></span> <span data-ttu-id="04a5c-106">Por ejemplo, en el caso de la administración de proyectos o las tarjetas de emisión de vales, puede actualizar los comentarios y el estado de la tarea.</span><span class="sxs-lookup"><span data-stu-id="04a5c-106">For example, in the case of project management or ticketing cards, you can update comments and the status of the task.</span></span> <span data-ttu-id="04a5c-107">En caso de aprobaciones, el estado más reciente se refleja a la vez que proporciona información y acciones diferenciadas.</span><span class="sxs-lookup"><span data-stu-id="04a5c-107">In case of approvals the latest state is reflected while also providing differentiated information and actions.</span></span>

<span data-ttu-id="04a5c-108">Por ejemplo, un usuario puede crear una solicitud de aprobación de activos en una Teams conversación.</span><span class="sxs-lookup"><span data-stu-id="04a5c-108">For example, a user can create an asset approval request in a Teams conversation.</span></span> <span data-ttu-id="04a5c-109">Alex crea una solicitud de aprobación y la asigna a Megan y Nestor.</span><span class="sxs-lookup"><span data-stu-id="04a5c-109">Alex creates an approval request and assigns it to Megan and Nestor.</span></span> <span data-ttu-id="04a5c-110">Las siguientes son las dos partes para crear la solicitud de aprobación:</span><span class="sxs-lookup"><span data-stu-id="04a5c-110">The following are the two parts to create the approval request:</span></span>

* <span data-ttu-id="04a5c-111">Las vistas específicas del usuario se pueden aprovechar mediante la `refresh` propiedad de las tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="04a5c-111">User Specific Views can be leveraged using the `refresh` property of the Adaptive Cards.</span></span>
<span data-ttu-id="04a5c-112">Al usar Vistas específicas del usuario,  se puede mostrar una tarjeta con botones **Aprobar** o Rechazar a un conjunto de usuarios y mostrar una tarjeta sin estos botones a otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="04a5c-112">Using User Specific Views one can show a card with **Approve** or **Reject** buttons to a set of users, and show a card without these buttons to other users.</span></span>

* <span data-ttu-id="04a5c-113">Para mantener el estado de la tarjeta actualizado en todo momento, Teams mecanismo de edición de mensajes se puede aprovechar.</span><span class="sxs-lookup"><span data-stu-id="04a5c-113">To keep the card state updated at all times, Teams message edit mechanism can be leveraged.</span></span> <span data-ttu-id="04a5c-114">Por ejemplo, cada vez que hay una aprobación, el bot puede desencadenar una edición de mensaje para todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="04a5c-114">For example, each time there is an approval, bot can trigger a message edit to all users.</span></span> <span data-ttu-id="04a5c-115">Esta edición de mensajes del bot desencadena una solicitud de invocación para todos los usuarios de actualización automática, a la que el bot puede responder con la tarjeta específica `adaptiveCard/action` del usuario actualizada.</span><span class="sxs-lookup"><span data-stu-id="04a5c-115">This bot message edit triggers an `adaptiveCard/action` invoke request for all automatic refresh users, to which the bot can respond with the updated user specific card.</span></span>

<span data-ttu-id="04a5c-116">Para obtener más información, [vea cómo realizar una edición de mensaje de bot](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/update-and-delete-bot-messages?tabs=dotnet#update-cards).</span><span class="sxs-lookup"><span data-stu-id="04a5c-116">For more information, see [how to do a bot message edit](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/update-and-delete-bot-messages?tabs=dotnet#update-cards).</span></span>

## <a name="approval-base-card"></a><span data-ttu-id="04a5c-117">Tarjeta base de aprobación</span><span class="sxs-lookup"><span data-stu-id="04a5c-117">Approval base card</span></span>

<span data-ttu-id="04a5c-118">El código siguiente proporciona un ejemplo de una tarjeta base de aprobación:</span><span class="sxs-lookup"><span data-stu-id="04a5c-118">The following code provides an example of an approval base card:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>", "<Nestor's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan and Nestor**"
    }
  ]
}
```

## <a name="approval-card-with-approve-and-reject-buttons"></a><span data-ttu-id="04a5c-119">Tarjeta de aprobación con botones Aprobar y Rechazar</span><span class="sxs-lookup"><span data-stu-id="04a5c-119">Approval card with Approve and Reject buttons</span></span>

<span data-ttu-id="04a5c-120">El código siguiente proporciona un ejemplo de una tarjeta de aprobación con botones **Aprobar** **y** Rechazar:</span><span class="sxs-lookup"><span data-stu-id="04a5c-120">The following code provides an example of an approval card with **Approve** and **Reject** buttons:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Nestor's user MRI>", "<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Approval Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan and Nestor**"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Approve",
      "verb": "approve",
      "data": {
            "more info": "<more info>"
      }
    },
    {
      "type": "Action.Execute",
      "title": "Reject",
      "verb": "reject",
      "data": {
            "more info": "<more info>"
      }
    }
  ]
}
```

<span data-ttu-id="04a5c-121">A continuación se muestran los dos roles que se muestran a los usuarios en función de su participación en la solicitud de aprobación:</span><span class="sxs-lookup"><span data-stu-id="04a5c-121">Following are the two roles that are shown to users depending on their involvement in the approval request:</span></span>

* <span data-ttu-id="04a5c-122">Tarjeta base de aprobación: se muestra a los usuarios que no forman parte de la lista de aprobadores y que aún no han aprobado o rechazado la solicitud y que no forman parte de la lista en propiedad del JSON de `userIds` `refresh` tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="04a5c-122">Approval base card: Shown to users who are not part of approvers list and have not yet approved or rejected the request, and are not part of `userIds` list in `refresh` property of the Adaptive Card JSON.</span></span>
* <span data-ttu-id="04a5c-123">Tarjeta de **aprobación con botones** Aprobar o Rechazar: se muestra a los usuarios que forman parte de la lista de aprobadores y a la lista de la propiedad del JSON de tarjeta  `userIds` `refresh` adaptable.</span><span class="sxs-lookup"><span data-stu-id="04a5c-123">Approval card with **Approve** or **Reject** buttons: Shown to the users who are part of the approvers list and the `userIds` list in the `refresh` property of the Adaptive Card JSON.</span></span>

<span data-ttu-id="04a5c-124">**Para enviar la solicitud de aprobación de activos**</span><span class="sxs-lookup"><span data-stu-id="04a5c-124">**To send the asset approval request**</span></span>

1. <span data-ttu-id="04a5c-125">Alex genera una solicitud de aprobación de activos en Teams conversación y la asigna a Megan y Nestor.</span><span class="sxs-lookup"><span data-stu-id="04a5c-125">Alex raises an asset approval request in a Teams conversation and assigns it to Megan and Nestor.</span></span>
2. <span data-ttu-id="04a5c-126">Bot envía la tarjeta base de aprobación en la conversación.</span><span class="sxs-lookup"><span data-stu-id="04a5c-126">Bot sends the approval base card in the conversation.</span></span>
3. <span data-ttu-id="04a5c-127">Todos los demás usuarios de la conversación ven la tarjeta enviada por el bot.</span><span class="sxs-lookup"><span data-stu-id="04a5c-127">All other users in the conversation see the card sent by the bot.</span></span> <span data-ttu-id="04a5c-128">La actualización automática se desencadena para Megan y Nestor,  que ahora ven la tarjeta específica del usuario con los botones **Aprobar** o Rechazar cuando sus MRIs de usuario se agregan a la lista en la propiedad de la `userIds` tarjeta `refresh` adaptable.</span><span class="sxs-lookup"><span data-stu-id="04a5c-128">Automatic refresh is triggered for Megan and Nestor, who now see the user specific card with **Approve** or **Reject** buttons as their user MRIs are added to the `userIds` list in the `refresh` property of the Adaptive Card.</span></span>

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-1.png" alt-text="Vistas específicas del usuario":::

4. <span data-ttu-id="04a5c-130">Nestor selecciona el botón **Aprobar** que está alimentado con `Action.Execute` .</span><span class="sxs-lookup"><span data-stu-id="04a5c-130">Nestor selects the **Approve** button which is powered with `Action.Execute`.</span></span> <span data-ttu-id="04a5c-131">El bot obtiene una `adaptiveCard/action` solicitud de invocación a la que puede devolver una tarjeta adaptable en respuesta.</span><span class="sxs-lookup"><span data-stu-id="04a5c-131">The bot gets an `adaptiveCard/action` invoke request to which it can return an Adaptive Card in response.</span></span>
5. <span data-ttu-id="04a5c-132">El bot desencadena una edición de mensajes con una tarjeta actualizada que indica que Nestor ha aprobado la solicitud mientras la aprobación de Megan está pendiente.</span><span class="sxs-lookup"><span data-stu-id="04a5c-132">The bot triggers a message edit with an updated card which says Nestor has approved the request while Megan's approval is pending.</span></span>
6. <span data-ttu-id="04a5c-133">La edición de mensajes bot desencadena una actualización automática para Megan y ve la tarjeta específica del usuario actualizada, que indica que Nestor ha aprobado la solicitud, pero también ve los botones **Aprobar** o **Rechazar.**</span><span class="sxs-lookup"><span data-stu-id="04a5c-133">Bot message edit triggers an automatic refresh for Megan and she sees the updated user specific card, which says Nestor has approved the request, but also sees the **Approve** or **Reject** buttons.</span></span> <span data-ttu-id="04a5c-134">La MRI de usuario de Nestor se quita de la lista en la propiedad de este JSON de tarjeta adaptable en los pasos `userIds` `refresh` 4 y 5.</span><span class="sxs-lookup"><span data-stu-id="04a5c-134">Nestor's user MRI is removed from the `userIds` list in `refresh` property of this Adaptive Card JSON in steps 4 and 5.</span></span> <span data-ttu-id="04a5c-135">Ahora, la actualización automática solo se desencadena para Megan.</span><span class="sxs-lookup"><span data-stu-id="04a5c-135">Now, automatic refresh is only triggered for Megan.</span></span>

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-2.png" alt-text="Vistas específicas del usuario actualizadas":::

7. <span data-ttu-id="04a5c-137">Ahora, Megan selecciona el **botón Aprobar,** que funciona con `Action.Execute` .</span><span class="sxs-lookup"><span data-stu-id="04a5c-137">Now, Megan selects the **Approve** button, which is powered with `Action.Execute`.</span></span> <span data-ttu-id="04a5c-138">El bot obtiene una `adaptiveCard/action` solicitud de invocación a la que puede devolver una tarjeta adaptable en respuesta.</span><span class="sxs-lookup"><span data-stu-id="04a5c-138">The bot gets an `adaptiveCard/action` invoke request to which it can return an Adaptive Card in response.</span></span>
8. <span data-ttu-id="04a5c-139">El bot desencadena una edición de mensajes con una tarjeta actualizada, que indica que Nestor y Megan han aprobado la solicitud.</span><span class="sxs-lookup"><span data-stu-id="04a5c-139">The bot triggers a message edit with an updated card, which says Nestor and Megan have approved the request.</span></span>
9. <span data-ttu-id="04a5c-140">La edición de mensajes del bot no desencadena ninguna actualización automática.</span><span class="sxs-lookup"><span data-stu-id="04a5c-140">Bot message edit does not trigger any automatic refresh.</span></span> <span data-ttu-id="04a5c-141">La MRI de usuario de Megan también se quita de la lista en la propiedad de este JSON de tarjeta adaptable en los pasos `userIds` `refresh` 7 y 8.</span><span class="sxs-lookup"><span data-stu-id="04a5c-141">Megan's user MRI is also removed from the `userIds` list in `refresh` property of this Adaptive Card JSON in steps 7 and 8.</span></span>

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-3.png" alt-text="Vistas actualizadas":::

## <a name="adaptive-card-sent-as-response-of-adaptivecardaction-and-message-edit"></a><span data-ttu-id="04a5c-143">Tarjeta adaptable enviada como respuesta de `adaptiveCard/action` y `message edit`</span><span class="sxs-lookup"><span data-stu-id="04a5c-143">Adaptive Card sent as response of `adaptiveCard/action` and `message edit`</span></span>

<span data-ttu-id="04a5c-144">El código siguiente proporciona un ejemplo de tarjetas adaptables enviadas como respuesta de los `adaptiveCard/action` `message edit` pasos 4 y 5 y para ellos:</span><span class="sxs-lookup"><span data-stu-id="04a5c-144">The following code provides an example of Adaptive Cards sent as response of `adaptiveCard/action` and `message edit` for steps 4 and 5:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor**"
    }
  ]
}
```

<span data-ttu-id="04a5c-145">El siguiente código proporciona un ejemplo de tarjetas adaptables enviadas como respuesta a la invocación a través `adaptiveCard/action` de la actualización automática para el paso 6:</span><span class="sxs-lookup"><span data-stu-id="04a5c-145">The following code provides an example of Adaptive Cards sent as response of `adaptiveCard/action` invoke through automatic refresh for step 6:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Approval Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor**"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Approve",
      "verb": "approve",
      "data": {
            "more info": "<more info>"
      }
    },
    {
      "type": "Action.Execute",
      "title": "Reject",
      "verb": "reject",
      "data": {
            "more info": "<more info>"
      }
    }
  ]
}
```

<span data-ttu-id="04a5c-146">El código siguiente proporciona un ejemplo de tarjetas adaptables enviadas como respuesta de y `adaptiveCard/action` `message edit` para los pasos 7 y 8:</span><span class="sxs-lookup"><span data-stu-id="04a5c-146">The following code provides an example of Adaptive Cards sent as response of `adaptiveCard/action` and `message edit` for steps 7 and 8:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": []
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor and Megan**"
    }
  ]
}
```

## <a name="see-also"></a><span data-ttu-id="04a5c-147">Vea también</span><span class="sxs-lookup"><span data-stu-id="04a5c-147">See also</span></span>

* [<span data-ttu-id="04a5c-148">Trabajar con acciones universales para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="04a5c-148">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
* [<span data-ttu-id="04a5c-149">Vistas específicas del usuario</span><span class="sxs-lookup"><span data-stu-id="04a5c-149">User Specific Views</span></span>](User-Specific-Views.md)

---
title: Vistas específicas de usuario
description: Ejemplo de vistas específicas del usuario mediante acciones universales
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 696fc5ce25c79d749b301309bfe0c737e39ad294
ms.sourcegitcommit: 9ef3b415cbba484c2201abe9c6927e08d974388e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52555447"
---
# <a name="user-specific-views"></a><span data-ttu-id="1fb77-103">Vistas específicas de usuario</span><span class="sxs-lookup"><span data-stu-id="1fb77-103">User Specific Views</span></span>

<span data-ttu-id="1fb77-104">Anteriormente, si las tarjetas adaptables se enviaba en una conversación Teams, todos los usuarios ven exactamente el mismo contenido de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="1fb77-104">Earlier if Adaptive Cards was sent in a Teams conversation, all users see the exact same card content.</span></span> <span data-ttu-id="1fb77-105">Con la introducción del modelo de acciones universales y `refresh` para tarjetas adaptables, los desarrolladores de bots ahora pueden proporcionar vistas específicas del usuario de tarjetas adaptables a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="1fb77-105">With the introduction of the Universal Actions model and `refresh` for Adaptive Cards, bot developers can now provide User Specific Views of Adaptive Cards to users.</span></span> <span data-ttu-id="1fb77-106">La misma tarjeta adaptable ahora puede actualizar a una tarjeta adaptable específica del usuario.</span><span class="sxs-lookup"><span data-stu-id="1fb77-106">The same Adaptive Card can now refresh to a User Specific Adaptive Card.</span></span>

<span data-ttu-id="1fb77-107">Por ejemplo, Megan, un inspector de seguridad de Contoso, desea crear un incidente y asignarlo a Alex.</span><span class="sxs-lookup"><span data-stu-id="1fb77-107">For example, Megan, a safety inspector at Contoso, wants to create an incident and assign it to Alex.</span></span> <span data-ttu-id="1fb77-108">También quiere que todos en el equipo estén al tanto del incidente.</span><span class="sxs-lookup"><span data-stu-id="1fb77-108">She also wants everyone in the team to be aware about the incident.</span></span> <span data-ttu-id="1fb77-109">Megan usa la extensión de mensaje de informes de incidentes de Contoso con tecnología de acciones universales para tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="1fb77-109">Megan uses Contoso incident reporting message extension powered by Universal Actions for Adaptive Cards.</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Vistas específicas de usuario":::

## <a name="user-specific-views-for-adaptive-cards"></a><span data-ttu-id="1fb77-111">Vistas específicas del usuario para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="1fb77-111">User Specific Views for Adaptive Cards</span></span>

<span data-ttu-id="1fb77-112">El código siguiente proporciona un ejemplo de tarjetas adaptables:</span><span class="sxs-lookup"><span data-stu-id="1fb77-112">The following code provides an example of Adaptive Cards:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView",
      "data": {
              "refresh info": "<refresh info>"
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ]
}
```

<span data-ttu-id="1fb77-113">**Para enviar tarjetas adaptables, actualice vistas específicas del usuario e invoque solicitudes al bot**</span><span class="sxs-lookup"><span data-stu-id="1fb77-113">**To send Adaptive Cards, refresh User Specific Views, and invoke requests to the bot**</span></span>

1. <span data-ttu-id="1fb77-114">Cuando Megan crea un nuevo incidente, el bot envía la tarjeta adaptable o la tarjeta común con los detalles del incidente en la conversación Teams.</span><span class="sxs-lookup"><span data-stu-id="1fb77-114">When Megan creates a new incident, the bot sends the Adaptive Card or common card with incident details in the Teams conversation.</span></span>
2. <span data-ttu-id="1fb77-115">Ahora esta tarjeta se actualiza automáticamente a la vista específica del usuario para Megan y Alex.</span><span class="sxs-lookup"><span data-stu-id="1fb77-115">Now this card automatically refreshes to User Specific View for Megan and Alex.</span></span> <span data-ttu-id="1fb77-116">Las resonancias magnéticas de usuario de Alex y Megan se agregan en `userIds` propiedad de la propiedad del JSON de la tarjeta `refresh` adaptable.</span><span class="sxs-lookup"><span data-stu-id="1fb77-116">Alex's and Megan's user MRIs are added in `userIds` property of `refresh` property of the Adaptive Card JSON.</span></span> <span data-ttu-id="1fb77-117">La tarjeta sigue siendo la misma para otros usuarios en la conversación.</span><span class="sxs-lookup"><span data-stu-id="1fb77-117">The card remains the same for other users in the conversation.</span></span>
3. <span data-ttu-id="1fb77-118">Para Megan, la actualización automática desencadena una `adaptiveCard/action` solicitud de invocación al bot.</span><span class="sxs-lookup"><span data-stu-id="1fb77-118">For Megan, automatic refresh triggers an `adaptiveCard/action` invoke request to the bot.</span></span> <span data-ttu-id="1fb77-119">El bot puede devolver una tarjeta creadora de incidentes con `Edit` el botón como respuesta a esta solicitud de invocación.</span><span class="sxs-lookup"><span data-stu-id="1fb77-119">The bot can return an incident creator card with `Edit` button as a response to this invoke request.</span></span>
4. <span data-ttu-id="1fb77-120">De forma similar para Alex, la actualización automática desencadena otra `adaptiveCard/action` solicitud de invocación al bot.</span><span class="sxs-lookup"><span data-stu-id="1fb77-120">Similarly for Alex, automatic refresh triggers another `adaptiveCard/action` invoke request to the bot.</span></span> <span data-ttu-id="1fb77-121">El bot puede devolver un botón de tarjeta de propietario de incidente `Resolve` como respuesta a esta solicitud de invocación.</span><span class="sxs-lookup"><span data-stu-id="1fb77-121">The bot can return an incident owner card `Resolve` button as a response to this invoke request.</span></span>

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a><span data-ttu-id="1fb77-122">Invocar solicitud enviada desde Teams cliente al bot</span><span class="sxs-lookup"><span data-stu-id="1fb77-122">Invoke request sent from Teams client to the bot</span></span>

<span data-ttu-id="1fb77-123">El código siguiente proporciona un ejemplo de una solicitud de invocación enviada desde el cliente Teams de Alex y Megan al bot:</span><span class="sxs-lookup"><span data-stu-id="1fb77-123">The following code provides an example of an invoke request sent from Alex's and Megan's Teams client to the bot:</span></span>

```JSON
{ 
  "type": "invoke",
  "name": "adaptiveCard/action",

  // ... other properties omitted for brevity

  "value": { 
    "action": { 
      "type": "Action.Execute", 
      "id": "", 
      "verb": "editOrResolveView",
      "data": { 
            "refresh info": "<refresh info>"
      } 
    },
    "trigger": "automatic" 
  }
}
```

## <a name="adaptivecardaction-invoke-response-card"></a><span data-ttu-id="1fb77-124">adaptiveCard/action invocan tarjeta de respuesta</span><span class="sxs-lookup"><span data-stu-id="1fb77-124">adaptiveCard/action invoke response card</span></span>

<span data-ttu-id="1fb77-125">El código siguiente proporciona un ejemplo de una tarjeta de respuesta de invocación adaptiveCard/action para Megan:</span><span class="sxs-lookup"><span data-stu-id="1fb77-125">The following code provides an example of an adaptiveCard/action invoke response card for Megan:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView"
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Edit",
      "verb": "edit",
      "data": {
            "additional info": "<additional info>",
            ...
      }
    }
  ]
}
```

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a><span data-ttu-id="1fb77-126">adaptiveCard/action invocan tarjeta de respuesta para Alex</span><span class="sxs-lookup"><span data-stu-id="1fb77-126">adaptiveCard/action invoke response card for Alex</span></span>

<span data-ttu-id="1fb77-127">El código siguiente proporciona un ejemplo de una tarjeta de respuesta de invocación adaptiveCard/action para Alex:</span><span class="sxs-lookup"><span data-stu-id="1fb77-127">The following code provides an example of an adaptiveCard/action invoke response card for Alex:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView"
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Resolve",
      "verb": "resolve",
      "data": {
            "additional info": "<additional info>",
            ...
      }
    }
  ]
}
```

## <a name="invoke-response-to-return-adaptive-cards"></a><span data-ttu-id="1fb77-128">Invocar respuesta para devolver tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="1fb77-128">Invoke response to return Adaptive Cards</span></span>

<span data-ttu-id="1fb77-129">El código siguiente proporciona un ejemplo de una respuesta de invocación para devolver tarjetas adaptables:</span><span class="sxs-lookup"><span data-stu-id="1fb77-129">The following code provides an example of an invoke response to return Adaptive Cards:</span></span>

```C#
string cardJson = "<adaptive card json>";
var card = JsonConvert.DeserializeObject(cardJson);

var adaptiveCardResponse = JObject.FromObject(new
 {
    statusCode = 200,
    type = "application/vnd.microsoft.adaptive.card",
    value = card
 });
```

<span data-ttu-id="1fb77-130">Directrices de diseño de tarjetas a tener en cuenta al diseñar vistas específicas del usuario:</span><span class="sxs-lookup"><span data-stu-id="1fb77-130">Card design guidelines to keep in mind while designing User Specific Views:</span></span>

* <span data-ttu-id="1fb77-131">Puede crear un máximo de **60 vistas específicas** de usuario para una tarjeta determinada que se envía a un chat o canal especificando las `userIds` suyas en la `refresh` sección.</span><span class="sxs-lookup"><span data-stu-id="1fb77-131">You can create a maximum of **60 User Specific Views** for a particular card being sent to a chat or channel by specifying their `userIds` in the `refresh` section.</span></span>
* <span data-ttu-id="1fb77-132">**Tarjeta base:** La versión base de la tarjeta que el desarrollador del bot envía al chat.</span><span class="sxs-lookup"><span data-stu-id="1fb77-132">**Base Card:** The base version of the card that the bot developer sends to the chat.</span></span> <span data-ttu-id="1fb77-133">Esta es la versión de la tarjeta adaptable para todos los usuarios que no se especifican en la `userIds` sección.</span><span class="sxs-lookup"><span data-stu-id="1fb77-133">This is the version of the Adaptive Card for all users who are not specified in the `userIds` section.</span></span>
* <span data-ttu-id="1fb77-134">Se puede utilizar una actualización o edición de mensajes para actualizar la tarjeta base y actualizar simultáneamente la tarjeta específica del usuario.</span><span class="sxs-lookup"><span data-stu-id="1fb77-134">A message update or edit can be used to update the base card and simultaneously refresh the User Specific Card.</span></span>

## <a name="see-also"></a><span data-ttu-id="1fb77-135">Vea también</span><span class="sxs-lookup"><span data-stu-id="1fb77-135">See also</span></span>

* [<span data-ttu-id="1fb77-136">Trabajar con Acciones universales para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="1fb77-136">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
* [<span data-ttu-id="1fb77-137">Vistas actualizadas</span><span class="sxs-lookup"><span data-stu-id="1fb77-137">Up to date views</span></span>](Up-To-Date-Views.md)

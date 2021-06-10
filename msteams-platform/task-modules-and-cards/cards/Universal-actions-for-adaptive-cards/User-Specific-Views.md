---
title: Vistas específicas de usuario
description: Ejemplo de vistas específicas del usuario mediante acciones universales
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: c24697b300d07ed53a172df162d0d3851361f579
ms.sourcegitcommit: 37325179a532897fafbe827dcf9a7ca5fa5e7d0b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2021
ms.locfileid: "52853518"
---
# <a name="user-specific-views"></a><span data-ttu-id="06adb-103">Vistas específicas de usuario</span><span class="sxs-lookup"><span data-stu-id="06adb-103">User Specific Views</span></span>

<span data-ttu-id="06adb-104">Anteriormente si se enviaron tarjetas adaptables en una Teams conversación, todos los usuarios verán exactamente el mismo contenido de la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="06adb-104">Earlier if Adaptive Cards was sent in a Teams conversation, all users see the exact same card content.</span></span> <span data-ttu-id="06adb-105">Con la introducción del modelo de acciones universales y las tarjetas adaptables, los desarrolladores de bots ahora pueden proporcionar vistas específicas del usuario de tarjetas adaptables `refresh` a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="06adb-105">With the introduction of the Universal Actions model and `refresh` for Adaptive Cards, bot developers can now provide User Specific Views of Adaptive Cards to users.</span></span> <span data-ttu-id="06adb-106">La misma tarjeta adaptable ahora puede actualizarse a una tarjeta adaptable específica del usuario.</span><span class="sxs-lookup"><span data-stu-id="06adb-106">The same Adaptive Card can now refresh to a User Specific Adaptive Card.</span></span> <span data-ttu-id="06adb-107">Un máximo de 60 usuarios diferentes pueden ver una versión diferente de la tarjeta con información o acciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="06adb-107">Maximum 60 different users can see a different version of the card with additional information or actions.</span></span> <span data-ttu-id="06adb-108">Esto proporciona escenarios eficaces como aprobaciones, controles de creador de sondeos, vales, administración de incidentes y tarjetas de administración de proyectos.</span><span class="sxs-lookup"><span data-stu-id="06adb-108">This provides powerful scenarios like approvals, poll creator controls, ticketing, incident management, and project management cards.</span></span>

<span data-ttu-id="06adb-109">Por ejemplo, Megan, un inspector de seguridad de Contoso, quiere crear un incidente y asignarlo a Alex.</span><span class="sxs-lookup"><span data-stu-id="06adb-109">For example, Megan, a safety inspector at Contoso, wants to create an incident and assign it to Alex.</span></span> <span data-ttu-id="06adb-110">También quiere que todos los miembros del equipo sean conscientes del incidente.</span><span class="sxs-lookup"><span data-stu-id="06adb-110">She also wants everyone in the team to be aware about the incident.</span></span> <span data-ttu-id="06adb-111">Megan usa la extensión de mensaje de informes de incidentes de Contoso con tecnología de acciones universales para tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="06adb-111">Megan uses Contoso incident reporting message extension powered by Universal Actions for Adaptive Cards.</span></span>

# <a name="mobile"></a>[<span data-ttu-id="06adb-112">Móvil</span><span class="sxs-lookup"><span data-stu-id="06adb-112">Mobile</span></span>](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="Vistas específicas del usuario móvil":::

# <a name="desktop"></a>[<span data-ttu-id="06adb-114">Escritorio</span><span class="sxs-lookup"><span data-stu-id="06adb-114">Desktop</span></span>](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Vistas específicas de usuario":::

* * *

## <a name="user-specific-views-for-adaptive-cards"></a><span data-ttu-id="06adb-116">Vistas específicas del usuario para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="06adb-116">User Specific Views for Adaptive Cards</span></span>

<span data-ttu-id="06adb-117">El siguiente código proporciona un ejemplo de tarjetas adaptables:</span><span class="sxs-lookup"><span data-stu-id="06adb-117">The following code provides an example of Adaptive Cards:</span></span>

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

<span data-ttu-id="06adb-118">**Para enviar tarjetas adaptables, actualizar vistas específicas del usuario e invocar solicitudes al bot**</span><span class="sxs-lookup"><span data-stu-id="06adb-118">**To send Adaptive Cards, refresh User Specific Views, and invoke requests to the bot**</span></span>

1. <span data-ttu-id="06adb-119">Cuando Megan crea un nuevo incidente, el bot envía la tarjeta adaptable o la tarjeta común con detalles de incidentes en la Teams conversación.</span><span class="sxs-lookup"><span data-stu-id="06adb-119">When Megan creates a new incident, the bot sends the Adaptive Card or common card with incident details in the Teams conversation.</span></span>
2. <span data-ttu-id="06adb-120">Ahora, esta tarjeta se actualiza automáticamente a la vista específica del usuario para Megan y Alex.</span><span class="sxs-lookup"><span data-stu-id="06adb-120">Now this card automatically refreshes to User Specific View for Megan and Alex.</span></span> <span data-ttu-id="06adb-121">Los MRIs de usuario de Alex y Megan se agregan en propiedad `userIds` de la propiedad del JSON de tarjeta `refresh` adaptable.</span><span class="sxs-lookup"><span data-stu-id="06adb-121">Alex's and Megan's user MRIs are added in `userIds` property of `refresh` property of the Adaptive Card JSON.</span></span> <span data-ttu-id="06adb-122">La tarjeta sigue siendo la misma para otros usuarios de la conversación.</span><span class="sxs-lookup"><span data-stu-id="06adb-122">The card remains the same for other users in the conversation.</span></span>
3. <span data-ttu-id="06adb-123">Para Megan, la actualización automática desencadena una `adaptiveCard/action` solicitud de invocación al bot.</span><span class="sxs-lookup"><span data-stu-id="06adb-123">For Megan, automatic refresh triggers an `adaptiveCard/action` invoke request to the bot.</span></span> <span data-ttu-id="06adb-124">El bot puede devolver una tarjeta de creador de incidentes con `Edit` botón como respuesta a esta solicitud de invocación.</span><span class="sxs-lookup"><span data-stu-id="06adb-124">The bot can return an incident creator card with `Edit` button as a response to this invoke request.</span></span>
4. <span data-ttu-id="06adb-125">De forma similar para Alex, la actualización automática desencadena otra `adaptiveCard/action` solicitud de invocación al bot.</span><span class="sxs-lookup"><span data-stu-id="06adb-125">Similarly for Alex, automatic refresh triggers another `adaptiveCard/action` invoke request to the bot.</span></span> <span data-ttu-id="06adb-126">El bot puede devolver un botón de tarjeta de propietario `Resolve` de incidentes como respuesta a esta solicitud de invocación.</span><span class="sxs-lookup"><span data-stu-id="06adb-126">The bot can return an incident owner card `Resolve` button as a response to this invoke request.</span></span>

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a><span data-ttu-id="06adb-127">Invocar solicitud enviada desde Teams cliente al bot</span><span class="sxs-lookup"><span data-stu-id="06adb-127">Invoke request sent from Teams client to the bot</span></span>

<span data-ttu-id="06adb-128">El código siguiente proporciona un ejemplo de una solicitud de invocación enviada desde el cliente de Teams de Alex y Megan al bot:</span><span class="sxs-lookup"><span data-stu-id="06adb-128">The following code provides an example of an invoke request sent from Alex's and Megan's Teams client to the bot:</span></span>

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

## <a name="adaptivecardaction-invoke-response-card"></a><span data-ttu-id="06adb-129">adaptiveCard/action invoke response card</span><span class="sxs-lookup"><span data-stu-id="06adb-129">adaptiveCard/action invoke response card</span></span>

<span data-ttu-id="06adb-130">El código siguiente proporciona un ejemplo de una tarjeta de respuesta adaptiveCard/action invoke para Megan:</span><span class="sxs-lookup"><span data-stu-id="06adb-130">The following code provides an example of an adaptiveCard/action invoke response card for Megan:</span></span>

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

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a><span data-ttu-id="06adb-131">adaptiveCard/action invoke response card for Alex</span><span class="sxs-lookup"><span data-stu-id="06adb-131">adaptiveCard/action invoke response card for Alex</span></span>

<span data-ttu-id="06adb-132">El siguiente código proporciona un ejemplo de una tarjeta de respuesta adaptiveCard/action invoke para Alex:</span><span class="sxs-lookup"><span data-stu-id="06adb-132">The following code provides an example of an adaptiveCard/action invoke response card for Alex:</span></span>

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

## <a name="invoke-response-to-return-adaptive-cards"></a><span data-ttu-id="06adb-133">Invocar respuesta para devolver tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="06adb-133">Invoke response to return Adaptive Cards</span></span>

<span data-ttu-id="06adb-134">El código siguiente proporciona un ejemplo de una respuesta de invocación para devolver tarjetas adaptables:</span><span class="sxs-lookup"><span data-stu-id="06adb-134">The following code provides an example of an invoke response to return Adaptive Cards:</span></span>

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

<span data-ttu-id="06adb-135">Directrices de diseño de tarjetas a tener en cuenta al diseñar vistas específicas del usuario:</span><span class="sxs-lookup"><span data-stu-id="06adb-135">Card design guidelines to keep in mind while designing User Specific Views:</span></span>

* <span data-ttu-id="06adb-136">Puede crear un máximo de **60** vistas específicas de usuario para una tarjeta determinada enviada a un chat o canal especificando sus `userIds` en la `refresh` sección.</span><span class="sxs-lookup"><span data-stu-id="06adb-136">You can create a maximum of **60 User Specific Views** for a particular card sent to a chat or channel by specifying their `userIds` in the `refresh` section.</span></span>
* <span data-ttu-id="06adb-137">**Tarjeta base:** La versión base de la tarjeta que el desarrollador del bot envía al chat.</span><span class="sxs-lookup"><span data-stu-id="06adb-137">**Base Card:** The base version of the card that the bot developer sends to the chat.</span></span> <span data-ttu-id="06adb-138">Esta es la versión de la tarjeta adaptable para todos los usuarios que no se especifican en la `userIds` sección.</span><span class="sxs-lookup"><span data-stu-id="06adb-138">This is the version of the Adaptive Card for all users who are not specified in the `userIds` section.</span></span>
* <span data-ttu-id="06adb-139">Se puede usar una actualización de mensajes para actualizar la tarjeta base y actualizar simultáneamente la tarjeta específica del usuario.</span><span class="sxs-lookup"><span data-stu-id="06adb-139">A message update can be used to update the base card and simultaneously refresh the User Specific Card.</span></span> <span data-ttu-id="06adb-140">Al abrir el chat o el canal, también se actualiza la tarjeta para los usuarios con la actualización habilitada.</span><span class="sxs-lookup"><span data-stu-id="06adb-140">Opening the chat or channel also refreshes the card for users with refresh enabled.</span></span>
* <span data-ttu-id="06adb-141">Para escenarios con grupos más grandes donde los usuarios cambian a una vista de acción, que necesita actualizaciones dinámicas para los respondedores, puede seguir sumando hasta 60 usuarios a la `userIds` lista.</span><span class="sxs-lookup"><span data-stu-id="06adb-141">For scenarios with larger groups where users switch to a view on action, which needs dynamic updates for responders, you can keep adding up to 60 users to the `userIds` list.</span></span> <span data-ttu-id="06adb-142">Puede quitar el primer respondedor de la lista cuando el usuario número 61 responda.</span><span class="sxs-lookup"><span data-stu-id="06adb-142">You can remove the first responder from the list when the 61st user responds.</span></span> <span data-ttu-id="06adb-143">Para los usuarios que se quitan de la lista, puede proporcionar un botón de actualización manual o usar el botón actualizar en el menú opciones del mensaje para `userIds` obtener el resultado más reciente.</span><span class="sxs-lookup"><span data-stu-id="06adb-143">For the users who get removed from the `userIds` list, you can provide a manual refresh button or use the refresh button in the message options menu to get the latest result.</span></span>
* <span data-ttu-id="06adb-144">Pida a los usuarios que obtengan una vista específica del usuario, donde solo ven una vista determinada de la tarjeta o algunas acciones.</span><span class="sxs-lookup"><span data-stu-id="06adb-144">Give a prompt to users to get a User Specific View, where they see only a particular view of the card or some actions.</span></span>

## <a name="see-also"></a><span data-ttu-id="06adb-145">Consulte también</span><span class="sxs-lookup"><span data-stu-id="06adb-145">See also</span></span>

* [<span data-ttu-id="06adb-146">Trabajar con Acciones universales para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="06adb-146">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
* [<span data-ttu-id="06adb-147">Vistas actualizadas</span><span class="sxs-lookup"><span data-stu-id="06adb-147">Up to date views</span></span>](Up-To-Date-Views.md)

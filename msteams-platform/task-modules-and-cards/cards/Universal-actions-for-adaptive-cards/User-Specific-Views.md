---
title: Vistas específicas del usuario
description: Ejemplo de vistas específicas del usuario mediante acciones universales
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 984b32511dda544942df11f7c5d8a25cca8e9a8a
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088870"
---
# <a name="user-specific-views"></a>Vistas específicas del usuario

Anteriormente si se enviaron tarjetas adaptables en una Teams conversación, todos los usuarios verán exactamente el mismo contenido de la tarjeta. Con la introducción del modelo de acciones universales y las tarjetas adaptables, los desarrolladores de bots ahora pueden proporcionar vistas específicas del usuario de tarjetas adaptables `refresh` a los usuarios. La misma tarjeta adaptable ahora puede actualizarse a una tarjeta adaptable específica del usuario.

Por ejemplo, Megan, un inspector de seguridad de Contoso, quiere crear un incidente y asignarlo a Alex. También quiere que todos los miembros del equipo sean conscientes del incidente. Megan usa la extensión de mensaje de informes de incidentes de Contoso con tecnología de acciones universales para tarjetas adaptables.

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Vistas específicas del usuario":::

## <a name="user-specific-views-for-adaptive-cards"></a>Vistas específicas del usuario para tarjetas adaptables

El siguiente código proporciona un ejemplo de tarjetas adaptables:

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

**Para enviar tarjetas adaptables, actualizar vistas específicas del usuario e invocar solicitudes al bot**

1. Cuando Megan crea un nuevo incidente, el bot envía la tarjeta adaptable o la tarjeta común con detalles de incidentes en la Teams conversación.
2. Ahora, esta tarjeta se actualiza automáticamente a la vista específica del usuario para Megan y Alex. Los MRIs de usuario de Alex y Megan se agregan en propiedad `userIds` de la propiedad del JSON de tarjeta `refresh` adaptable. La tarjeta sigue siendo la misma para otros usuarios de la conversación.
3. Para Megan, la actualización automática desencadena una `adaptiveCard/action` solicitud de invocación al bot. El bot puede devolver una tarjeta de creador de incidentes con `Edit` botón como respuesta a esta solicitud de invocación.
4. De forma similar para Alex, la actualización automática desencadena otra `adaptiveCard/action` solicitud de invocación al bot. El bot puede devolver un botón de tarjeta de propietario `Resolve` de incidentes como respuesta a esta solicitud de invocación.

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a>Invocar solicitud enviada desde Teams cliente al bot

El código siguiente proporciona un ejemplo de una solicitud de invocación enviada desde el cliente de Teams de Alex y Megan al bot:

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

## <a name="adaptivecardaction-invoke-response-card"></a>adaptiveCard/action invoke response card

El código siguiente proporciona un ejemplo de una tarjeta de respuesta adaptiveCard/action invoke para Megan:

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

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a>adaptiveCard/action invoke response card for Alex

El siguiente código proporciona un ejemplo de una tarjeta de respuesta adaptiveCard/action invoke para Alex:

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

## <a name="invoke-response-to-return-adaptive-cards"></a>Invocar respuesta para devolver tarjetas adaptables

El código siguiente proporciona un ejemplo de una respuesta de invocación para devolver tarjetas adaptables:

```C#
string cardJson = "<adaptive card json>";
var card = JsonConvert.DeserializeObject(cardJson);

var adaptiveCardResponse = JObject.FromObject(new
 {
    statusCode = 200,
    type = "application/vnd.microsoft.card.adaptive",
    value = card
 });
```

Directrices de diseño de tarjetas a tener en cuenta al diseñar vistas específicas del usuario:

* Puede crear un máximo de **60** vistas específicas de usuario para una tarjeta determinada que se envía a un chat o canal especificando sus `userIds` en la `refresh` sección.
* **Tarjeta base:** La versión base de la tarjeta que el desarrollador del bot envía al chat. Esta es la versión de la tarjeta adaptable para todos los usuarios que no se especifican en la `userIds` sección.
* Se puede usar una actualización o edición de mensajes para actualizar la tarjeta base y actualizar simultáneamente la tarjeta específica del usuario.

## <a name="see-also"></a>Vea también

* [Trabajar con acciones universales para tarjetas adaptables](Work-with-universal-actions-for-adaptive-cards.md)
* [Vistas actualizadas](Up-To-Date-Views.md)

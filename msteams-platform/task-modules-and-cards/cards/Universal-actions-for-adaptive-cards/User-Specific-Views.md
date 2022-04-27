---
title: Vistas específicas de usuario
description: Más información sobre vistas específicas del usuario mediante acciones universales con ejemplo de código
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: b2e5b8d6dd00104fab819ba7d05d5913bb891d83
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073683"
---
# <a name="user-specific-views"></a>Vistas específicas de usuario

Anteriormente, si se enviaron tarjetas adaptables en una conversación Teams, todos los usuarios verían exactamente el mismo contenido de tarjeta. Con la introducción del modelo de acciones universales y `refresh` las tarjetas adaptables, los desarrolladores de bots ahora pueden proporcionar vistas específicas del usuario de tarjetas adaptables a los usuarios. La misma tarjeta adaptable ahora puede actualizarse a una tarjeta adaptable específica del usuario. Un máximo de 60 usuarios diferentes pueden ver una versión diferente de la tarjeta con información o acciones adicionales. La tarjeta adaptable proporciona escenarios eficaces, como aprobaciones, controles de creador de sondeos, vales, administración de incidentes y tarjetas de administración de proyectos.

> [!NOTE]
> La vista específica del usuario es compatible con las tarjetas adaptables enviadas por un bot y depende de Las acciones universales.

Por ejemplo, Megan, un inspector de seguridad de Contoso, quiere crear un incidente y asignarlo a Alex. Megan también quiere que todos los miembros del equipo estén al tanto del incidente. Megan usa la extensión de mensajes de informes de incidentes de Contoso con tecnología de Acciones universales para tarjetas adaptables.

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="Vistas específicas del usuario móvil" lightbox="../../../assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg":::

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Vistas específicas de usuario" lightbox="../../../assets/images/adaptive-cards/universal-bots-incident-management.png":::

* * *

## <a name="user-specific-views-for-adaptive-cards"></a>Vistas específicas del usuario para tarjetas adaptables

El código siguiente proporciona un ejemplo de tarjetas adaptables:

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
      }
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

Para enviar tarjetas adaptables, actualice vistas específicas del usuario e invoque solicitudes al bot:

1. Cuando Megan crea un nuevo incidente, el bot envía la tarjeta adaptable o la tarjeta común con los detalles del incidente en la conversación de Teams.
2. Ahora esta tarjeta se actualiza automáticamente a la vista específica del usuario para Megan y Alex. Las MRI de usuario de Alex y Megan se agregan en `userIds` la propiedad de la `refresh` propiedad del JSON de la tarjeta adaptable. La tarjeta sigue siendo la misma para otros usuarios de la conversación.
3. Para Megan, la actualización automática desencadena una `adaptiveCard/action` solicitud de invocación al bot. El bot puede devolver una tarjeta de creador de incidentes con `Edit` el botón como respuesta a esta solicitud de invocación.
4. De forma similar para Alex, la actualización automática desencadena otra `adaptiveCard/action` solicitud de invocación al bot. El bot puede devolver un botón de tarjeta `Resolve` de propietario del incidente como respuesta a esta solicitud de invocación.

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a>Invocación de la solicitud enviada desde Teams cliente al bot

El código siguiente proporciona un ejemplo de una solicitud de invocación enviada desde el cliente Teams de Alex y Megan al bot:

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

## <a name="adaptivecardaction-invoke-response-card"></a>tarjeta de respuesta adaptiveCard/action invoke

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

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a>tarjeta de respuesta adaptiveCard/action invoke para Alex

El código siguiente proporciona un ejemplo de una tarjeta de respuesta adaptiveCard/action invoke para Alex:

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

## <a name="invoke-response-to-return-adaptive-cards"></a>Invocación de la respuesta para devolver tarjetas adaptables

El código siguiente proporciona un ejemplo de una respuesta de invocación para devolver tarjetas adaptables:

### <a name="c"></a>[C#](#tab/C)

```csharp
string cardJson = "<adaptive card json>";
var card = JsonConvert.DeserializeObject(cardJson);

var adaptiveCardResponse = JObject.FromObject(new
 {
    statusCode = 200,
    type = "application/vnd.microsoft.adaptive.card",
    value = card
 });
```

### <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript
var card = "<adaptive card json>";
 
const cardRes = {
        statusCode: 200,
        type: 'application/vnd.microsoft.card.adaptive',
        value: card
    };
    const res = {
        status: 200,
        body: cardRes
    };
    return res;

```

***

Directrices de diseño de tarjetas que se deben tener en cuenta al diseñar vistas específicas del usuario:

* Puede crear un máximo de **60 vistas específicas de usuario** para una tarjeta determinada enviada a un chat o canal especificando su `userIds` en la `refresh` sección .
* **Tarjeta base:** La versión base de la tarjeta que el desarrollador del bot envía al chat. La versión base es la versión de la tarjeta adaptable para todos los usuarios que no se especifican en la `userIds` sección.
* Se puede usar una actualización de mensajes para actualizar la tarjeta base y actualizar simultáneamente la tarjeta específica del usuario. Al abrir el chat o el canal también se actualiza la tarjeta para los usuarios con la actualización habilitada.
* En escenarios con grupos más grandes en los que los usuarios cambian a una vista sobre la acción, que necesita actualizaciones dinámicas para los respondedores, puede seguir sumando hasta 60 usuarios a la `userIds` lista. Puede quitar el primer respondedor de la lista cuando el usuario 61 responda. Para los usuarios que se quitan de la `userIds` lista, puede proporcionar un botón de actualización manual o usar el botón Actualizar en el menú de opciones de mensaje para obtener el resultado más reciente.
* Proporcione un mensaje a los usuarios para obtener una vista específica del usuario, donde solo ven una vista determinada de la tarjeta o algunas acciones.

## <a name="code-sample"></a>Ejemplo de código

|Ejemplo de nombre | Descripción | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Tarjetas adaptables de flujos de trabajo secuenciales | Muestra cómo implementar flujos de trabajo secuenciales, vistas específicas del usuario y tarjetas adaptables actualizadas en bots. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>Consulte también

* [Trabajar con Acciones universales para tarjetas adaptables](Work-with-universal-actions-for-adaptive-cards.md)
* [Vistas actualizadas](Up-To-Date-Views.md)
* [Comentarios de finalización de formularios](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)

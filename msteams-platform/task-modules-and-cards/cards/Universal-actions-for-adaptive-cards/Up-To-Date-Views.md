---
title: Vistas actualizadas
description: En este módulo, obtenga información sobre las vistas actualizadas de tarjetas mediante el bot universal con ejemplos de Código en Microsoft Teams
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 5c6f7d13cd884baf9ffbc1fd30cafb7cfab33295
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143623"
---
# <a name="up-to-date-cards"></a>Tarjetas actualizadas

Ahora puede proporcionar información más reciente a los usuarios en tarjetas adaptables. Incluya una combinación de actualizaciones y ediciones de mensajes en Teams. Actualice las vistas específicas del usuario dinámicamente a su estado más reciente como y cuando haya un cambio en el servicio. Por ejemplo, para la administración de proyectos o las tarjetas de vales, actualice los comentarios y el estado de la tarea. Para las aprobaciones, el estado más reciente se refleja al tiempo que proporciona información y acciones diferenciadas.

Por ejemplo, un usuario puede crear una solicitud de aprobación de recursos en una conversación Teams. Alex crea una solicitud de aprobación y la asigna a Megan y Nestor. A continuación se muestran las dos partes para crear la solicitud de aprobación:

* Las vistas específicas del usuario se pueden aplicar mediante la `refresh` propiedad de las tarjetas adaptables.
Con vistas específicas del usuario, se puede mostrar una tarjeta con los botones **Aprobar** o **Rechazar** a un conjunto de usuarios y mostrar una tarjeta sin estos botones a otros usuarios.

* Para mantener siempre actualizado el estado de la tarjeta, se puede usar Teams mecanismo de edición de mensajes. Por ejemplo, para cada aprobación, el bot puede desencadenar una edición de mensajes para todos los usuarios. Esta edición de mensajes de bot desencadena una `adaptiveCard/action` solicitud de invocación para todos los usuarios de actualización automática, a la que el bot puede responder con la tarjeta específica del usuario actualizada.

Para obtener más información, consulte [cómo realizar una edición de mensajes de bot](/microsoftteams/platform/bots/how-to/update-and-delete-bot-messages?tabs=dotnet#update-cards).

## <a name="approval-base-card"></a>Tarjeta base de aprobación

El código siguiente proporciona un ejemplo de una tarjeta base de aprobación:

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

## <a name="approval-card-with-approve-and-reject-buttons"></a>Tarjeta de aprobación con botones Aprobar y Rechazar

El código siguiente proporciona un ejemplo de una tarjeta de aprobación con los botones **Aprobar** y **Rechazar** :

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

A continuación se muestran los dos roles que se muestran a los usuarios en función de la solicitud de aprobación:

* Tarjeta base de aprobación: se muestra a los usuarios que no forman parte de la lista de aprobadores y la solicitud aún no se ha aprobado o rechazado, y no forma parte de la `userIds` lista en `refresh` la propiedad del JSON de tarjeta adaptable.
* Tarjeta de aprobación con botones **Aprobar** o **Rechazar** : se muestra a los usuarios que forman parte de la lista de aprobadores y a la `userIds` lista de la `refresh` propiedad del JSON de tarjeta adaptable.

Para enviar la solicitud de aprobación de recursos:

1. Alex genera una solicitud de aprobación de recursos en una conversación Teams y la asigna a Megan y Nestor.
2. El bot envía la tarjeta base de aprobación en la conversación.
3. Todos los demás usuarios de la conversación ven la tarjeta enviada por el bot. La actualización automática se desencadena para Megan y Nestor, que ahora ven la tarjeta específica del usuario con los botones **Aprobar** o **Rechazar** a medida que sus MRI de usuario se agregan a la `userIds` lista en la `refresh` propiedad de la tarjeta adaptable.

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-1.png" alt-text="Vistas específicas de usuario":::

4. Nestor selecciona el botón **Aprobar** , que funciona con `Action.Execute`. El bot obtiene una solicitud de invocación `adaptiveCard/action` a la que puede devolver una tarjeta adaptable en respuesta.
5. El bot desencadena una edición de mensajes con una tarjeta actualizada, que indica que Nestor ha aprobado la solicitud mientras la aprobación de Megan está pendiente.
6. La edición de mensajes del bot desencadena una actualización automática para Megan y ve la tarjeta específica del usuario actualizada, que indica que Nestor ha aprobado la solicitud, pero también ve los botones **Aprobar** o **Rechazar** . La MRI de usuario de Nestor se quita de la lista en `refresh` la `userIds` propiedad de este JSON de tarjeta adaptable en los pasos 4 y 5. Ahora, la actualización automática solo se desencadena para Megan.

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-2.png" alt-text="Vistas actualizadas específicas del usuario":::

7. Ahora, Megan selecciona el botón **Aprobar** , que funciona con `Action.Execute`. El bot obtiene una solicitud de invocación `adaptiveCard/action` a la que puede devolver una tarjeta adaptable en respuesta.
8. El bot desencadena una edición de mensajes con una tarjeta actualizada, lo que indica que Nestor y Megan han aprobado la solicitud.
9. La edición de mensajes del bot no desencadena ninguna actualización automática. La MRI de usuario de Megan también se quita de la lista en `refresh` la `userIds` propiedad de esta tarjeta adaptable JSON en los pasos 7 y 8.

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-3.png" alt-text="Vistas actualizadas":::

## <a name="adaptive-card-sent-as-response-of-adaptivecardaction-and-message-edit"></a>Tarjeta adaptable enviada como respuesta de `adaptiveCard/action` y `message edit`

El código siguiente proporciona un ejemplo de tarjetas adaptables enviadas como respuesta de `adaptiveCard/action` y `message edit` para los pasos 4 y 5:

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

El código siguiente proporciona un ejemplo de tarjetas adaptables enviadas como respuesta de `adaptiveCard/action` invocación mediante la actualización automática para el paso 6:

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

El código siguiente proporciona un ejemplo de tarjetas adaptables enviadas como respuesta de `adaptiveCard/action` y `message edit` para los pasos 7 y 8:

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

## <a name="code-sample"></a>Ejemplo de código

|Ejemplo de nombre | Descripción | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Tarjetas adaptables de flujos de trabajo secuenciales | Demostrar cómo implementar flujos de trabajo secuenciales, vistas específicas del usuario y Tarjetas adaptables actualizadas en bots. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>Consulte también

* [Trabajar con Acciones universales para tarjetas adaptables](Work-with-universal-actions-for-adaptive-cards.md)
* [Vistas específicas de usuario](User-Specific-Views.md)
* [Comentarios de finalización de formularios](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)

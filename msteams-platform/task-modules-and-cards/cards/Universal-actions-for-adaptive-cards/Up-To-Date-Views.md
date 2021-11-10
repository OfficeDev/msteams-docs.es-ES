---
title: Vistas actualizadas
description: Obtenga información sobre las vistas actualizadas mediante bot universal con ejemplos de código
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
keywords: tarjeta base de aprobación rechazar adaptable
ms.openlocfilehash: 2e7feb96ecefd0e6253c0f3a86e3863e0ae7a53b
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/10/2021
ms.locfileid: "60887409"
---
# <a name="up-to-date-cards"></a>Tarjetas actualizadas

Ahora puede proporcionar información más reciente a los usuarios en tarjetas adaptables. Incluya una combinación de actualizaciones y ediciones de mensajes en Teams. Actualice las vistas específicas del usuario dinámicamente a su estado más reciente como y cuando haya un cambio en el servicio. Por ejemplo, para la administración de proyectos o las tarjetas de emisión de vales, actualice los comentarios y el estado de la tarea. Para las aprobaciones, el estado más reciente se refleja a la vez que proporciona información y acciones diferenciadas.

Por ejemplo, un usuario puede crear una solicitud de aprobación de activos en una Teams conversación. Alex crea una solicitud de aprobación y la asigna a Megan y Nestor. Las siguientes son las dos partes para crear la solicitud de aprobación:

* Las vistas específicas del usuario se pueden aplicar mediante la `refresh` propiedad de las tarjetas adaptables.
Al usar Vistas específicas del usuario,  se puede mostrar una tarjeta con botones **Aprobar** o Rechazar a un conjunto de usuarios y mostrar una tarjeta sin estos botones a otros usuarios.

* Para mantener siempre actualizado el estado de la tarjeta, Teams se puede usar el mecanismo de edición de mensajes. Por ejemplo, para cada aprobación, el bot puede desencadenar una edición de mensaje para todos los usuarios. Esta edición de mensajes del bot desencadena una solicitud de invocación para todos los usuarios de actualización automática, a la que el bot puede responder con la tarjeta específica `adaptiveCard/action` del usuario actualizada.

Para obtener más información, [vea cómo realizar una edición de mensaje de bot](/microsoftteams/platform/bots/how-to/update-and-delete-bot-messages?tabs=dotnet#update-cards).

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

El código siguiente proporciona un ejemplo de una tarjeta de aprobación con botones **Aprobar** **y** Rechazar:

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

* Tarjeta base de aprobación: se muestra a los usuarios que no forman parte de la lista de aprobadores y la solicitud aún no se ha aprobado o rechazado, y no forma parte de la lista en propiedad del `userIds` `refresh` JSON de tarjeta adaptable.
* Tarjeta de **aprobación con botones** Aprobar o Rechazar: se muestra a los usuarios que forman parte de la lista de aprobadores y a la lista de la propiedad del JSON de tarjeta  `userIds` `refresh` adaptable.

**Para enviar la solicitud de aprobación de activos**

1. Alex genera una solicitud de aprobación de activos en Teams conversación y la asigna a Megan y Nestor.
2. Bot envía la tarjeta base de aprobación en la conversación.
3. Todos los demás usuarios de la conversación ven la tarjeta enviada por el bot. La actualización automática se desencadena para Megan y Nestor,  que ahora ven la tarjeta específica del usuario con los botones **Aprobar** o Rechazar cuando sus MRIs de usuario se agregan a la lista en la propiedad de la `userIds` tarjeta `refresh` adaptable.

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-1.png" alt-text="Vistas específicas de usuario":::

4. Nestor selecciona el botón **Aprobar,** que funciona con `Action.Execute` . El bot obtiene una `adaptiveCard/action` solicitud de invocación a la que puede devolver una tarjeta adaptable en respuesta.
5. El bot desencadena una edición de mensajes con una tarjeta actualizada, que indica que Nestor ha aprobado la solicitud mientras la aprobación de Megan está pendiente.
6. La edición de mensajes bot desencadena una actualización automática para Megan y ve la tarjeta específica del usuario actualizada, que indica que Nestor ha aprobado la solicitud, pero también ve los botones **Aprobar** o **Rechazar.** La MRI de usuario de Nestor se quita de la lista en la propiedad de este JSON de tarjeta adaptable en los pasos `userIds` `refresh` 4 y 5. Ahora, la actualización automática solo se desencadena para Megan.

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-2.png" alt-text="Vistas específicas del usuario actualizadas":::

7. Ahora, Megan selecciona el **botón Aprobar,** que funciona con `Action.Execute` . El bot obtiene una `adaptiveCard/action` solicitud de invocación a la que puede devolver una tarjeta adaptable en respuesta.
8. El bot desencadena una edición de mensajes con una tarjeta actualizada, que indica que Nestor y Megan han aprobado la solicitud.
9. La edición de mensajes del bot no desencadena ninguna actualización automática. La MRI de usuario de Megan también se quita de la lista en la propiedad de este JSON de tarjeta adaptable en los pasos `userIds` `refresh` 7 y 8.

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-3.png" alt-text="Vistas actualizadas":::

## <a name="adaptive-card-sent-as-response-of-adaptivecardaction-and-message-edit"></a>Tarjeta adaptable enviada como respuesta de `adaptiveCard/action` y `message edit`

El código siguiente proporciona un ejemplo de tarjetas adaptables enviadas como respuesta de los `adaptiveCard/action` `message edit` pasos 4 y 5 y para ellos:

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

El siguiente código proporciona un ejemplo de tarjetas adaptables enviadas como respuesta a la invocación a través `adaptiveCard/action` de la actualización automática para el paso 6:

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

El código siguiente proporciona un ejemplo de tarjetas adaptables enviadas como respuesta de y `adaptiveCard/action` `message edit` para los pasos 7 y 8:

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
| Tarjetas adaptables de flujos de trabajo secuenciales | Muestra cómo implementar flujos de trabajo secuenciales, vistas específicas del usuario y tarjetas adaptables actualizadas en bots. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>Consulte también

* [Trabajar con Acciones universales para tarjetas adaptables](Work-with-universal-actions-for-adaptive-cards.md)
* [Vistas específicas de usuario](User-Specific-Views.md)

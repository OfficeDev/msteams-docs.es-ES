---
title: Enviar identificador de inquilino e identificador de conversación a los encabezados de solicitud del bot
description: describe cómo enviar el identificador de inquilino y el identificador de conversación a los encabezados de solicitud del bot.
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 76f667453114ab202d43217b9a4c01a6d14cc1a8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565896"
---
# <a name="send-tenant-id-and-conversation-id-to-the-request-headers-of-the-bot"></a>Enviar identificador de inquilino e identificador de conversación a los encabezados de solicitud del bot

Las solicitudes salientes actuales al bot no contienen en el encabezado ni en la dirección URL ninguna información que ayude a los bots a enrutar el tráfico sin desempaquetar toda la carga. Las actividades se envían al bot a través de una dirección URL similar a https://<your_domain>/api/messages. Las solicitudes se reciben para mostrar el identificador de conversación y el identificador de inquilino en los encabezados.

## <a name="request-header-fields"></a>Campos de encabezado de solicitud

Se agregan dos campos de encabezado de solicitud no estándar a todas las solicitudes enviadas a bots, tanto para flujo asincrónico como para flujo sincrónico. En la tabla siguiente se proporcionan los campos de encabezado de solicitud y sus valores:

| Clave de campo | Valor |
|----------------|-----------------|
| x-ms-conversation-id | El identificador de conversación correspondiente a la actividad de solicitud si corresponde y confirmado o comprobado. |
| x-ms-tenant-id | El identificador de inquilino correspondiente a la conversación en la actividad de solicitud. |

Si el inquilino o el identificador de conversación no está presente en la actividad o no se validó en el lado del servicio, el valor está vacío.

![Campos de encabezado de solicitud](~/assets/images/bots/requestheaderfields.png)

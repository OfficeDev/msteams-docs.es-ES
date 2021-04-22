---
title: Enviar identificador de inquilino e identificador de conversación a los encabezados de solicitud del bot
description: describe cómo enviar el identificador de inquilino y el identificador de conversación a los encabezados de solicitud del bot.
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: b3938b3011e09016f8594b2b17ba627d4922947b
ms.sourcegitcommit: 35bc2a31b92f3f7c6524373108f095a870d9ad09
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2021
ms.locfileid: "51922536"
---
# <a name="send-tenant-id-and-conversation-id-to-the-request-headers-of-the-bot"></a>Enviar identificador de inquilino e identificador de conversación a los encabezados de solicitud del bot

Las solicitudes salientes actuales al bot no contienen en el encabezado ni en la dirección URL ninguna información que ayude a los bots a enrutar el tráfico sin desempaquetar toda la carga. Las actividades se envían al bot a través de una dirección URL similar a https://<your_domain>/api/messages. Las solicitudes se reciben para mostrar el identificador de conversación y el identificador de inquilino en los encabezados.

## <a name="request-header-fields"></a>Campos de encabezado de solicitud

Se agregan dos campos de encabezado de solicitud no estándar a todas las solicitudes enviadas a bots, tanto para flujo asincrónico como para flujo sincrónico. En la tabla siguiente se proporcionan los campos de encabezado de solicitud y sus valores.

| Clave de campo | Valor |
|----------------|-----------------|
| x-ms-conversation-id | El identificador de conversación correspondiente a la actividad de solicitud si corresponde y confirmado o comprobado. |
| x-ms-tenant-id | El identificador de inquilino correspondiente a la conversación en la actividad de solicitud. |

Si el inquilino o el identificador de conversación no está presente en la actividad o no se validó en el lado del servicio, el valor está vacío.

![Campos de encabezado de solicitud](~/assets/images/bots/requestheaderfields.png)

---
title: Envío del identificador de inquilino y el identificador de conversación a los encabezados de solicitud del bot
description: Describe cómo enviar el identificador de inquilino y el identificador de conversación a los encabezados de solicitud del bot.
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 8aca2c11dbdfc84abe8c4d0ec40e2748d04f6301
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757293"
---
# <a name="send-tenant-id-and-conversation-id-to-the-request-headers-of-the-bot"></a>Envío del identificador de inquilino y el identificador de conversación a los encabezados de solicitud del bot

Las solicitudes salientes actuales al bot no contienen en el encabezado ni en la dirección URL información que ayude a los bots a enrutar el tráfico sin desempaquetar toda la carga. Las actividades se envían al bot a través de una dirección URL similar a https://<your_domain>/api/messages. Se reciben solicitudes para mostrar el identificador de conversación y el identificador de inquilino en los encabezados.

## <a name="request-header-fields"></a>Campos de encabezado de solicitud

Se agregan dos campos de encabezado de solicitud no estándar a todas las solicitudes enviadas a los bots, tanto para el flujo asincrónico como para el flujo sincrónico. En la tabla siguiente se proporcionan los campos de encabezado de solicitud y sus valores:

| Clave de campo | Valor |
|----------------|-----------------|
| x-ms-conversation-id | Identificador de conversación correspondiente a la actividad de solicitud, si procede, y confirmado o verificado. |
| x-ms-tenant-id | Identificador de inquilino correspondiente a la conversación en la actividad de solicitud. |

Si el identificador de inquilino o conversación no está presente en la actividad o no se validó en el lado del servicio, el valor está vacío.

![Campos de encabezado de solicitud](~/assets/images/bots/requestheaderfields.png)

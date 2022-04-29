---
title: Envío del identificador de inquilino y el identificador de conversación a los encabezados de solicitud del bot
description: Describe cómo enviar el identificador de inquilino y el identificador de conversación a los encabezados de solicitud del bot.
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 9b63dd81eeccbf78989a31a06baa5d678916acef
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111293"
---
# <a name="send-tenant-id-and-conversation-id-to-the-request-headers-of-the-bot"></a>Envío del identificador de inquilino y el identificador de conversación a los encabezados de solicitud del bot

Las solicitudes salientes actuales al bot no contienen en el encabezado o la dirección URL ninguna información que ayude a los bots a enrutar el tráfico sin desempaquetar toda la carga. Las actividades se envían al bot a través de una dirección URL similar a https://<your_domain>/api/messages. Se reciben solicitudes para mostrar el identificador de conversación y el identificador de inquilino en los encabezados.

## <a name="request-header-fields"></a>Campos de encabezado de solicitud

Se agregan dos campos de encabezado de solicitud no estándar a todas las solicitudes enviadas a los bots, tanto para el flujo asincrónico como para el flujo sincrónico. En la tabla siguiente se proporcionan los campos de encabezado de solicitud y sus valores:

| Clave de campo | Valor |
|----------------|-----------------|
| x-ms-conversation-id | Identificador de conversación correspondiente a la actividad de solicitud, si procede, y confirmado o verificado. |
| x-ms-tenant-id | Identificador de inquilino correspondiente a la conversación en la actividad de solicitud. |

Si el identificador de inquilino o conversación no está presente en la actividad o no se validó en el lado del servicio, el valor está vacío.

![Campos de encabezado de solicitud](~/assets/images/bots/requestheaderfields.png)

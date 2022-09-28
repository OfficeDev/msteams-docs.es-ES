---
title: Envío del identificador de inquilino y el identificador de conversación a los encabezados de solicitud del bot
description: Obtenga información sobre cómo enrutar el tráfico del bot sin desempaquetar toda la carga con el identificador de inquilino y el identificador de conversación presentes en los encabezados de solicitud del bot en Teams.
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 3132d91d4b3d0b290ee8e1fb35ebeea076217fe8
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100150"
---
# <a name="request-headers-of-the-bot"></a>Solicitar encabezados del bot

Las solicitudes salientes actuales al bot no contienen en el encabezado ni en la dirección URL información que ayude a los bots a enrutar el tráfico sin desempaquetar toda la carga. Las actividades se envían al bot a través de una dirección URL similar a https://<your_domain>/api/messages. Se reciben solicitudes para mostrar el identificador de conversación y el identificador de inquilino en los encabezados.

## <a name="request-header-fields"></a>Campos de encabezado de solicitud

Se agregan dos campos de encabezado de solicitud no estándar a todas las solicitudes enviadas a los bots, tanto para el flujo asincrónico como para el flujo sincrónico. En la tabla siguiente se proporcionan los campos de encabezado de solicitud y sus valores:

| Clave de campo | Valor |
|----------------|-----------------|
| x-ms-conversation-id | Identificador de conversación correspondiente a la actividad de solicitud, si procede, y confirmado o verificado. |
| x-ms-tenant-id | Identificador de inquilino correspondiente a la conversación en la actividad de solicitud. |

Si el identificador de inquilino o conversación no está presente en la actividad o no se validó en el lado del servicio, el valor está vacío.

![Campos de encabezado de solicitud](~/assets/images/bots/requestheaderfields.png)

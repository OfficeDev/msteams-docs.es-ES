---
title: Creación de una notificación en la reunión para la reunión de Teams
author: v-sdhakshina
description: En este artículo, aprenderá a crear una notificación en la reunión para la reunión de Microsoft Teams y su ejemplo de código.
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.openlocfilehash: e62958535fa1bcbcdeb104b5fd5fdd2882250aa3
ms.sourcegitcommit: 372aade09e62ac7e5936215173a6632fbb042c9d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2022
ms.locfileid: "68699132"
---
# <a name="build-in-meeting-notification-for-teams-meeting"></a>Creación de una notificación en la reunión para la reunión de Teams

La notificación en la reunión se usa para interactuar con los participantes y recopilar información o comentarios durante la reunión. Use una [carga de notificación en la reunión](meeting-apps-apis.md#send-an-in-meeting-notification) para desencadenar una notificación en la reunión. Como parte de la solicitud de carga de notificación, incluya la dirección URL donde se hospeda el contenido que se va a mostrar.

Se usa una dirección URL de recurso externo para mostrar la notificación en la reunión. Puede usar el método `submitTask` para enviar datos en un chat de reunión.

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-dialogbox.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo puede usar un cuadro de diálogo en la reunión.":::

Además, puede agregar la imagen de visualización de Teams y la tarjeta de contactos del usuario a la notificación de la reunión basada en el `onBehalfOf`token con el MRI del usuario y el nombre para mostrar pasado en la carga útil. A continuación se muestra una carga útil de ejemplo:

```json
    {
       "type": "message",
       "text": "John Phillips assigned you a weekly todo",
       "summary": "Don't forget to meet with Marketing next week",
       "channelData": {
           onBehalfOf: [
             { 
               itemId: 0, 
               mentionType: 'person', 
               mri: context.activity.from.id, 
               displayname: context.activity.from.name 
             }
            ],
           "notification": {
           "alertInMeeting": true,
           "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
            }
        },
       "replyToId": "1493070356924"
    }
```

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-people-card.png" alt-text="En esta captura de pantalla se muestra cómo se usa la imagen de presentación de Teams y la tarjeta de personas con el cuadro de diálogo en la reunión." border="true":::

## <a name="code-sample"></a>Ejemplo de código

Ejemplo de nombre | Descripción | C# | Node.js |
|----------------|-----------------|--------------|----------------|
| Notificación en la reunión | Muestra cómo implementar la notificación en la reunión mediante el bot. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs) |

## <a name="step-by-step-guide"></a>Guía paso a paso

Siga la [guía paso a paso](../sbs-meeting-content-bubble.yml) para generar una notificación en la reunión de Teams.

## <a name="see-also"></a>Vea también

* [Pestañas de compilación para la reunión](~/apps-in-teams-meetings/build-tabs-for-meeting.md)
* [Compilación de aplicaciones para la fase de reunión de Teams](build-apps-for-teams-meeting-stage.md)
* [Creación de una conversación extensible para el chat de reuniones](build-extensible-conversation-for-meeting-chat.md)
* [Compilación de aplicaciones para usuarios anónimos](build-apps-for-anonymous-user.md)
* [API avanzadas de reunión](meeting-apps-apis.md)

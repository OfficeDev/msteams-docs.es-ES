---
title: Webhooks y conectores
author: clearab
description: Comprenda cómo los webhooks y los conectores pueden conectar los servicios web al cliente de Teams.
ms.localizationpriority: high
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 27b1647620291b278cc76491da13fe8687c4e314
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059675"
---
# <a name="webhooks-and-connectors"></a>Webhooks y conectores

Los webhooks y conectores ayudan a conectar los servicios web a canales y equipos en Microsoft Teams. Los webhooks son devoluciones de llamada HTTP definidas por el usuario que notifican a los usuarios cualquier acción que haya tenido lugar en el canal de Microsoft Teams. Es una forma de que una aplicación obtenga datos en tiempo real. Los conectores permiten a los usuarios suscribirse para recibir notificaciones y mensajes de los servicios web. Exponen un punto de conexión HTTPS para que el servicio publique mensajes en forma de tarjetas.

## <a name="outgoing-webhooks"></a>Webhooks salientes

Los webhooks ayudan a Teams a integrarse con aplicaciones externas. Los webhooks salientes permiten que los usuarios envíen mensajes de texto desde un canal a los servicios web. Después de configurar los webhooks salientes, los usuarios pueden @mention webhook saliente y enviar un mensaje a los servicios web. El servicio responde en un plazo de diez segundos al mensaje con un texto o una tarjeta.

> [!NOTE]
> Los webhooks salientes se configuran por equipo y no se pueden incluir como parte de una aplicación de Teams normal.

## <a name="connectors"></a>Conectores

Los conectores permiten a los usuarios suscribirse para recibir notificaciones y mensajes de los servicios web. Exponen el punto de conexión HTTPS para que el servicio publique mensajes en canales de Teams, normalmente en forma de tarjetas.

### <a name="incoming-webhooks"></a>Webhooks entrantes

Los webhooks entrantes ayudan a publicar mensajes de aplicaciones en Teams. Si los webhooks entrantes están habilitados para un equipo en cualquier canal, exponen el punto de conexión HTTPS, que acepta el archivo JSON con el formato correcto e inserta los mensajes en ese canal. Por ejemplo, puede crear un webhook entrante en el canal de DevOps, configurar la compilación e implementar y supervisar servicios simultáneamente para enviar alertas.

### <a name="office-365-connectors"></a>Conectores de Office 365

Los conectores de Office 365 le permiten crear una página de configuración personalizada para el webhook entrante y empaquetarlas como parte de una aplicación de Teams. Los mensajes se envían principalmente mediante tarjetas del Conector de Office 365 y tienen la capacidad de agregar un conjunto limitado de acciones de tarjeta. Por ejemplo, un conector meteorológico que permite a los usuarios seleccionar una ubicación y una hora del día para recibir actualizaciones sobre el tiempo de mañana. Se configuran en un nivel de canal, pero se instalan en el nivel de equipo.

> [!NOTE]
> Puede distribuir la aplicación de Teams de Conector de Office 365 a nuestra AppStore.

## <a name="create-and-send-messages"></a>Crear y enviar mensajes

Los mensajes que requieren acción permiten a los usuarios tomar medidas sin salir de su cliente de correo electrónico, lo que aumenta la involucración del usuario. Con Office 365 y los webhooks entrantes, puede enviar mensajes publicando una carga JSON en la dirección URL del webhook.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear un webhook saliente](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)

## <a name="see-also"></a>Vea también

* [Crear un webhook entrante](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Crear un Conector de Office 365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Crear y enviar mensajes](~/webhooks-and-connectors/how-to/connectors-using.md)

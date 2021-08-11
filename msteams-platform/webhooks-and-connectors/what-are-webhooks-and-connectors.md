---
title: Webhooks y conectores
author: clearab
description: Comprenda cómo los webhooks y conectores pueden conectar los servicios web al Teams cliente.
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 199f1e8a82f067cbd8124553481ed54693d241f1c3a50c085b32203b89f4f63d
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2021
ms.locfileid: "57708639"
---
# <a name="webhooks-and-connectors"></a>Webhooks y conectores

Webhooks and connectors help to connect the web services to channels and teams in Microsoft Teams. Los webhooks son una devolución de llamada HTTP definida por el usuario que notifica a los usuarios sobre cualquier acción que haya tenido lugar en el Microsoft Teams web. Es una forma de que una aplicación obtenga datos en tiempo real. Los conectores permiten a los usuarios suscribirse para recibir notificaciones y mensajes de los servicios web. Exponen un extremo HTTPS para que el servicio publique mensajes en forma de tarjetas.

## <a name="outgoing-webhooks"></a>Webhooks salientes

Los webhooks ayudan Teams integrar con aplicaciones externas. Con webhooks salientes, puede enviar mensajes de texto desde un canal a los servicios web. Después de configurar los webhooks salientes, los usuarios @mention webhook saliente y enviar un mensaje a los servicios web. El servicio responde en un plazo de diez segundos al mensaje con un texto o una tarjeta.

> [!NOTE]
> Los webhooks salientes se configuran por equipo y no se pueden incluir como parte de una aplicación Teams normal.

## <a name="connectors"></a>Conectores

Los conectores permiten a los usuarios suscribirse para recibir notificaciones y mensajes de los servicios web. Exponen el punto de conexión HTTPS para que el servicio publique mensajes Teams canales, normalmente en forma de tarjetas.

### <a name="incoming-webhooks"></a>Webhooks entrantes

Los webhooks entrantes ayudan a publicar mensajes desde aplicaciones a Teams. Si los webhooks entrantes están habilitados para un equipo en cualquier canal, expone el extremo HTTPS, que acepta JSON con el formato correcto e inserta los mensajes en ese canal. Por ejemplo, puede crear un webhook entrante en el canal de DevOps, configurar la compilación e implementar y supervisar simultáneamente servicios para enviar alertas.

### <a name="office-365-connectors"></a>Conectores de Office 365

Office 365 Los conectores te permiten crear una página de configuración personalizada para el webhook entrante y empaquetarlos como parte de una Teams aplicación. Los mensajes se envían principalmente mediante Office 365 connector y tienen la capacidad de agregarles un conjunto limitado de acciones de tarjeta. Por ejemplo, un conector meteorológico que permite a los usuarios seleccionar una ubicación y hora del día, para recibir actualizaciones sobre el tiempo del mañana. Se configuran en un nivel de canal, pero se instalan en un nivel de equipo.

> [!NOTE]
> Puedes distribuir la aplicación Office 365 Connector Teams a nuestra AppStore.

## <a name="create-and-send-messages"></a>Crear y enviar mensajes

Los mensajes que se pueden usar permiten a los usuarios tomar medidas sin salir de su cliente de correo electrónico, lo que aumenta la participación de los usuarios. Con Office 365 webhooks entrantes y de entrada, puede enviar mensajes publicando una carga JSON en la dirección URL del webhook.

## <a name="see-also"></a>Vea también

* [Crear un webhook entrante](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Crear un Conector de Office 365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Crear y enviar mensajes](~/webhooks-and-connectors/how-to/connectors-using.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear un webhook saliente](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)

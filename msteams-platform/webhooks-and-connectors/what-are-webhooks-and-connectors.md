---
title: ¿Qué son los webhooks y los conectores?
author: clearab
description: Comprenda cómo los conectores y webhooks pueden conectar sus servicios web con el cliente de Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 6a2453cb7d0c2d55a8df938849313f47702e5585
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796375"
---
# <a name="what-are-webhooks-and-connectors"></a>¿Qué son los webhooks y los conectores?

Los webhooks y los conectores son una forma sencilla de conectar los servicios web a los canales y los equipos dentro de Microsoft Teams. 

## <a name="outgoing-webhooks"></a>Webhooks salientes

Los webhooks salientes permiten a los usuarios enviar mensajes de texto desde un canal a los servicios Web. Una vez configurados, los usuarios podrán @mention el webhook saliente y enviar un mensaje a su servicio. El servicio tendrá cinco segundos para enviar una respuesta al mensaje, posiblemente con texto o con una tarjeta.

Los webhooks salientes se configuran por cada equipo, no se pueden incluir como parte de una aplicación normal de Microsoft Teams. Son los más adecuados para completar cargas de trabajo específicas del equipo que no requieren que se recopilen o intercambien grandes cantidades de información.

Consulte [crear un webhook saliente](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).

## <a name="connectors"></a>Conectores

Los conectores permiten a los usuarios suscribirse para recibir notificaciones y mensajes de los servicios Web. Exponen un extremo HTTPS para que el servicio envíe mensajes, normalmente en forma de tarjetas.

### <a name="incoming-webhooks"></a>Webhooks entrantes

Los webhooks entrantes son el tipo más sencillo de conector. Para cualquier canal del equipo (si están habilitados para ese equipo), puede elegir exponer un extremo HTTPS que acepte el JSON con el formato correcto e insertar mensajes en ese canal. Son una forma rápida y sencilla de conectar un canal a su servicio y se usan mejor para escenarios únicos de un equipo en particular. Por ejemplo, puede crear un webhook entrante en el canal de DevOps y configurar los servicios de compilación, implementación y supervisión para enviar alertas.

Consulte [crear un webhook entrante](~/webhooks-and-connectors/how-to/add-incoming-webhook.md).

### <a name="office-365-connectors"></a>Conectores de Office 365

Los conectores de Office 365 le permiten crear una página de configuración personalizada para el webhook entrante y empaquetarla como parte de una aplicación de Microsoft Teams. A continuación, puede distribuir esa aplicación de forma más amplia o incluso en nuestra tienda de aplicaciones. Los mensajes se envían principalmente mediante tarjetas de conector de Office 365 y también es posible agregar a ellos un conjunto limitado de acciones de tarjeta. Un buen ejemplo de esto es un conector meteorológico que permite a los usuarios elegir una ubicación y la hora del día para recibir actualizaciones sobre el tiempo de mañana. Se configuran en un nivel de canal, pero se instalan en el nivel de equipo.

Consulte [Create an Office 365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md).

---
title: ¿Qué son los webhooks y los conectores?
author: clearab
description: Comprenda cómo los conectores y webhooks pueden conectar sus servicios web con el cliente de Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 740806e43af94d5a5da876affec2070a5a461b11
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652181"
---
# <a name="what-are-webhooks-and-connectors"></a>¿Qué son los webhooks y los conectores?

Los webhooks y los conectores son formas sencillas de conectar sistemas y servicios externos con canales y chats de Microsoft Teams.

Por ejemplo, los usuarios pueden suscribirse a las notificaciones de otra aplicación (normalmente en forma de tarjetas).

## <a name="incoming-webhooks"></a>Webhooks entrantes

Los webhooks entrantes son el tipo más sencillo de conector y una forma rápida y sencilla de conectar el canal de un equipo a un servicio externo. Para cualquier canal (si está habilitado para ese equipo), puede exponer un extremo HTTPS que acepte el JSON con el formato correcto e inserte mensajes en el canal.

Consulte [crear un webhook entrante](~/webhooks-and-connectors/how-to/add-incoming-webhook.md).

### <a name="user-scenarios"></a>Escenarios de usuario

Los webhooks entrantes son los más idóneos para escenarios exclusivos de un equipo en particular. Por ejemplo, puede crear un webhook entrante en el canal de DevOps y configurar los servicios de compilación, implementación y supervisión para enviar alertas.

## <a name="office-365-connectors"></a>Conectores de Office 365

Un conector de Office 365 permite crear una página de configuración personalizada para el webhook entrante y empaquetarla como parte de una aplicación de Teams. A continuación, puede distribuir esa aplicación de forma más amplia o incluso en nuestra tienda de aplicaciones. Los mensajes se envían principalmente mediante tarjetas de conector de Office 365 que también pueden tener un conjunto limitado de acciones de tarjeta. Se configuran en el nivel de canal, pero se instalan en el nivel de equipo.

Consulte [Create an Office 365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md).

### <a name="user-scenarios"></a>Escenarios de usuario

Un conector meteorológico que permite elegir una ubicación y una hora del día para recibir actualizaciones sobre la previsión del futuro.

## <a name="outgoing-webhooks"></a>Webhooks salientes

Los webhooks salientes permiten a los usuarios enviar mensajes de texto desde un canal a los servicios Web. Una vez configurados, los usuarios pueden @mention la aplicación y enviar un mensaje al servicio externo. El servicio tiene cinco segundos para enviar una respuesta al mensaje, posiblemente con texto o con una tarjeta.

Los webhooks salientes se configuran por equipo y no pueden incluirse como parte de una aplicación normal de Microsoft Teams.

Consulte [crear un webhook saliente](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).

### <a name="user-scenarios"></a>Escenarios de usuario

Los webhooks salientes son idóneos para completar flujos de trabajo específicos del equipo que no requieran la recopilación o el intercambio de grandes cantidades de información.

## <a name="learn-more"></a>Más información

* [Planeación de la aplicación](../../concepts/extensibility-points.md)
* [Compilar la aplicación](../../concepts/building-an-app.md)
* [Publicación de la aplicación](../../concepts/deploy-and-publish/overview.md)

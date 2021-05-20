---
title: ¿Qué son los webhooks y los conectores?
author: clearab
description: Comprenda cómo los webhooks y conectores pueden conectar sus servicios web al cliente Teams.
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: e36b73c0eaed5068311dae6c1ef8fdc073432334
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566806"
---
# <a name="what-are-webhooks-and-connectors"></a>¿Qué son los webhooks y los conectores?

Los webhook y los conectores son una forma simple de conectar los servicios web a canales y equipos en Microsoft Teams. 

## <a name="outgoing-webhooks"></a>Webhooks salientes

Los webhooks salientes permiten que los usuarios envíen mensajes de texto desde un canal a los servicios web. Una vez configurado, los usuarios podrán @mention el webhook saliente y enviar un mensaje a su servicio. Su servicio tendrá cinco segundos para enviar una respuesta al mensaje, que podría contener texto o una tarjeta.

Los webhooks salientes se configuran por equipo, no se pueden incluir como parte de una aplicación de Teams normal. Son los más adecuados para completar cargas de trabajo específicas del equipo que no requieren que se recopilen o intercambien grandes cantidades de información.

Para obtener más información, consulte [Crear un webhook saliente.](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)

## <a name="connectors"></a>Conectores

Los conectores permiten a los usuarios suscribirse para recibir notificaciones y mensajes de los servicios web. Exponen un punto de conexión HTTPS para que el servicio publique mensajes, normalmente en forma de tarjetas.

### <a name="incoming-webhooks"></a>Webhooks entrantes

Los webhooks entrantes son el tipo más simple de conector. Para cualquier canal del equipo (si están habilitados para ese equipo) puede optar por exponer un punto de conexión HTTPS que acepte JSON con el formato correcto e insertar mensajes en ese canal. Son una forma rápida y fácil de conectar un canal a su servicio, y se utilizan mejor para escenarios que son únicos para un equipo en particular. Por ejemplo, podría crear un webhook entrante en el canal de DevOps y configurar los servicios de compilación, implementación y supervisión para enviar alertas.

Para obtener más información, consulte [Crear un webhook entrante](~/webhooks-and-connectors/how-to/add-incoming-webhook.md).

### <a name="office-365-connectors"></a>Conectores de Office 365

Office 365 Los conectores le permiten crear una página de configuración personalizada para el webhook entrante y empaquetarlos como parte de una aplicación Teams. A continuación, puede distribuir esa aplicación de forma más amplia, o incluso a nuestra tienda de aplicaciones. También envía mensajes principalmente con tarjetas de conector de Office 365 y tiene la capacidad de agregarles un conjunto limitado de acciones de tarjeta. Un buen ejemplo de esto es un conector meteorológico que permite a los usuarios elegir una ubicación y hora del día para recibir actualizaciones sobre el clima de mañana. Se configuran en un nivel de canal, pero se instalan a nivel de equipo.

Para obtener más información, consulte [Crear un conector de Office 365](~/webhooks-and-connectors/how-to/connectors-creating.md).

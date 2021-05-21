---
title: ¿Qué son los webhooks y conectores?
author: clearab
description: Comprenda cómo los webhooks y conectores pueden conectar los servicios web al Teams cliente.
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
# <a name="what-are-webhooks-and-connectors"></a>¿Qué son los webhooks y conectores?

Los webhook y los conectores son una forma simple de conectar los servicios web a canales y equipos en Microsoft Teams. 

## <a name="outgoing-webhooks"></a>Webhooks salientes

Los webhooks salientes permiten que los usuarios envíen mensajes de texto desde un canal a los servicios web. Una vez configurado, los usuarios podrán @mention webhook saliente y enviar un mensaje al servicio. El servicio tendrá cinco segundos para enviar una respuesta al mensaje, que puede contener texto o una tarjeta.

Los webhooks salientes se configuran por equipo, no se pueden incluir como parte de una aplicación Teams normal. Son las más adecuadas para completar cargas de trabajo específicas del equipo que no requieren grandes cantidades de información para recopilarse o intercambiarse.

Para obtener más información, [vea Create an outgoing webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).

## <a name="connectors"></a>Conectores

Los conectores permiten a los usuarios suscribirse para recibir notificaciones y mensajes de los servicios web. Exponen un punto de conexión HTTPS para que el servicio publique mensajes, normalmente en forma de tarjetas.

### <a name="incoming-webhooks"></a>Webhooks entrantes

Los webhooks entrantes son el tipo más sencillo de conector. Para cualquier canal del equipo (si están habilitados para ese equipo), puede elegir exponer un extremo HTTPS que acepte JSON con el formato correcto e inserte mensajes en ese canal. Son una forma rápida y fácil de conectar un canal al servicio y se usan mejor para escenarios que son exclusivos de un equipo en particular. Por ejemplo, puede crear un webhook entrante en el canal de DevOps y configurar los servicios de compilación, implementación y supervisión para enviar alertas.

Para obtener más información, [vea Create an incoming webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md).

### <a name="office-365-connectors"></a>Conectores de Office 365

Office 365 Los conectores te permiten crear una página de configuración personalizada para el webhook entrante y empaquetarlos como parte de una Teams aplicación. A continuación, puedes distribuir esa aplicación de forma más amplia o incluso a nuestra tienda de aplicaciones. Los mensajes se envían principalmente Office 365 tarjetas connector y tienen la capacidad de agregarles también un conjunto limitado de acciones de tarjeta. Un buen ejemplo de esto es un conector meteorológico que permite a los usuarios elegir una ubicación y hora del día para recibir actualizaciones sobre el tiempo del mañana. Se configuran en un nivel de canal, pero se instalan en un nivel de equipo.

Para obtener más información, vea [Create an Office 365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md).

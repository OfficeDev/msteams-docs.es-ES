---
title: Descripción de las funcionalidades de la aplicación Teams
author: heath-hamilton
description: Información general sobre las capacidades de la plataforma de Microsoft Teams, que son los puntos de extensión para crear aplicaciones de Teams.
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 9bb94d2cfd5c30b2245c5ccf580d374972315e72
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964567"
---
# <a name="understanding-teams-app-capabilities"></a>Descripción de las funcionalidades de la aplicación Teams

Las *funcionalidades* son los puntos de extensión para crear aplicaciones en la plataforma de Microsoft Teams.

Hay varias formas de ampliar el cliente de Microsoft Teams, de modo que cada aplicación sea única: algunas solo tienen una capacidad (como un webhook), mientras que otras tienen algunas para conceder opciones a los usuarios. Por ejemplo, la aplicación puede mostrar datos en una ubicación central (pestaña) y presentar la misma información a través de una interfaz de conversación (bot).

La aplicación de Microsoft Teams puede tener una de las siguientes capacidades principales, o todas ellas:

* [Pestañas](../tabs/what-are-tabs.md)
* [Extensiones de mensajería](../messaging-extensions/what-are-messaging-extensions.md)
* [Webhooks y conectores](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)
* [Bots](../bots/what-are-bots.md)

La aplicación también puede aprovechar las funcionalidades avanzadas, como la [API de REST de Microsoft Graph](../graph-api/rsc/resource-specific-consent.md).

Vea la siguiente ilustración para obtener una idea de las funcionalidades que proporcionarán las características que desea en la aplicación.

![Diagrama de ideas ilustrativo de las funcionalidades de la aplicación Teams](doc-links/images/capabilities-overview.png)

## <a name="doing-whats-best-for-your-users"></a>¿Qué es lo mejor para los usuarios?

A medida que se familiarice con el desarrollo de aplicaciones de Microsoft Teams, empezará a comprender sus matices. Hay más de una forma de crear determinadas características (como la recopilación de entradas de usuario). Por ejemplo, puede insertar un formulario basado en Web en una pestaña usando un `<iframe>` . También puede hacerlo en una pestaña usando un módulo de tareas, una Convención de interfaz de usuario de Microsoft Teams, para una experiencia más nativa que los usuarios prefieren.

La elección de la combinación correcta de capacidades y convenciones, controles y elementos de la interfaz de usuario se refiere a [comprender los casos de uso de la audiencia](../concepts/design/understand-use-cases.md).

## <a name="learn-more"></a>Obtén más información

* [Empezar a planear la aplicación](../concepts/extensibility-points.md)

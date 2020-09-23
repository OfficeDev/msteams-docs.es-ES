---
title: Descripción de las funcionalidades de la aplicación Teams
author: heath-hamilton
description: Explicación de las funcionalidades de la aplicación Teams
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: e7a6fe61fa5c74547ce20cc895afdd044f35e512
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210358"
---
# <a name="understanding-teams-app-capabilities"></a>Descripción de las funcionalidades de la aplicación Teams

Las *funcionalidades* son los puntos de extensión para crear aplicaciones en la plataforma de Microsoft Teams.

Hay varias formas de ampliar Teams, de modo que cada aplicación es única: algunas solo tienen una capacidad (como un webhook), mientras que otras tienen algunas para conceder opciones a los usuarios. Por ejemplo, la aplicación puede mostrar datos en una ubicación central (pestaña) y presentar la misma información a través de una interfaz de conversación (bot).

La aplicación de Microsoft Teams puede tener una de las siguientes capacidades principales, o todas ellas:

* [Pestañas](../tabs/what-are-tabs.md)
* [Extensiones de mensajería](../messaging-extensions/what-are-messaging-extensions.md)
* [Bots](../bots/what-are-bots.md)
* [Webhooks y conectores](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

La aplicación también puede aprovechar las funcionalidades avanzadas, como la [API de Microsoft Graph para Teams](https://docs.microsoft.com/graph/teams-concept-overview).

Vea la siguiente ilustración para obtener una idea de las funcionalidades que proporcionarán las características que desea en la aplicación.

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Diagrama de ideas en el que se ilustra qué son las funcionalidades de la aplicación Teams.":::

## <a name="doing-whats-best-for-your-users"></a>¿Qué es lo mejor para los usuarios?

A medida que se familiarice con el desarrollo de aplicaciones de Microsoft Teams, empezará a comprender sus matices. Hay más de una forma de crear determinadas características (como la recopilación de entradas de usuario). Por ejemplo, puede insertar un formulario basado en Web en una pestaña usando un `<iframe>` . También puede hacerlo en una pestaña usando un módulo de tareas, una Convención de interfaz de usuario de Microsoft Teams, para una experiencia más nativa que los usuarios prefieren.

La elección de las capacidades y el diseño adecuados se despliega para [comprender primero los casos de uso de la audiencia](../concepts/design/understand-use-cases.md).

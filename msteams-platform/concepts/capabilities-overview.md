---
title: Descripción de las capacidades de la aplicación de Teams
author: heath-hamilton
description: Características de la aplicación de Teams explicadas
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 5336b36b52cf81be414f18ccaaf9e235c079e626
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034708"
---
# <a name="understanding-teams-app-capabilities"></a>Descripción de las capacidades de la aplicación de Teams

*Las funcionalidades* son los puntos de extensión para crear aplicaciones en la plataforma de Microsoft Teams.

Hay varias formas de extender Teams, por lo que cada aplicación es única: algunas solo tienen una funcionalidad (como un webhook), mientras que otras tienen algunas para dar opciones a los usuarios. Por ejemplo, la aplicación podría mostrar datos en una ubicación central (pestaña) y presentar esa misma información a través de una interfaz conversacional (bot).

La aplicación de Teams tiene una o todas las siguientes funcionalidades principales:

* [Pestañas](../tabs/what-are-tabs.md)
* [Extensiones de mensajería](../messaging-extensions/what-are-messaging-extensions.md)
* [Bots](../bots/what-are-bots.md)
* [Webhooks y conectores](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

La aplicación también puede aprovechar las capacidades avanzadas, como la API de [Microsoft Graph para Teams](https://docs.microsoft.com/graph/teams-concept-overview).

Consulta la siguiente ilustración para obtener una idea de qué capacidades proporcionarían las características que quieres en la aplicación.

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Mapa de la mente que ilustra las funcionalidades de la aplicación de Teams.":::

## <a name="doing-whats-best-for-your-users"></a>Hacer lo mejor para los usuarios

A medida que te familiarices con el desarrollo de aplicaciones de Teams, empezarás a comprender sus sutilezas. Hay más de una forma de crear determinadas características (como recopilar la entrada del usuario). Por ejemplo, puede insertar un formulario basado en web en una pestaña mediante un `<iframe>` . También puedes hacerlo en una pestaña con un módulo de tareas, una convención de la interfaz de usuario de Teams, para una experiencia más nativa que los usuarios prefieran.

Elegir las capacidades y el diseño adecuados se debe a comprender primero [los casos de uso de la audiencia.](../concepts/design/understand-use-cases.md)

---
title: Comprender las capacidades de la aplicación
author: heath-hamilton
description: Teams capacidades de la aplicación explicadas
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 209d187681b1370440931fcd40744965395b13e8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565154"
---
# <a name="understand-microsoft-teams-app-capabilities"></a>Comprender Microsoft Teams capacidades de la aplicación

La extensibilidad o los puntos de entrada son formas diferentes en las que una aplicación puede manifestarse ante un usuario. Por ejemplo, un usuario puede interactuar con una aplicación en una pestaña de lienzo para realizar una actividad o puede elegir hacer lo mismo mediante un bot conversacional. Las distintas capacidades utilizadas para crear la aplicación Teams le permiten aumentar su ámbito de uso.

Hay varias maneras de extender Teams, por lo que cada aplicación es única. Algunos solo tienen una capacidad, como un webhook, mientras que otros tienen más de una característica para dar a los usuarios varias opciones. Por ejemplo, la aplicación puede mostrar datos en una ubicación central, es decir, la **pestaña** y presentar esa misma información a través de una interfaz conversacional, es decir, el **bot.**

## <a name="app-capabilities"></a>Capacidades de la aplicación

La aplicación Teams tiene una o todas las siguientes capacidades principales:

* [Pestañas](../tabs/what-are-tabs.md)
* [Extensiones de mensajería](../messaging-extensions/what-are-messaging-extensions.md)
* [Bots](../bots/what-are-bots.md)
* [Webhooks y conectores](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

La aplicación también puede aprovechar las capacidades avanzadas, como la [API de Microsoft Graph para Teams.](/graph/teams-concept-overview)

La siguiente ilustración le da una idea de qué capacidades proporcionará las características que desea en la aplicación:

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Mapa mental que ilustra cuáles son Teams capacidades de la aplicación.":::

## <a name="always-consider-your-user"></a>Siempre considere a su usuario

A medida que te familiarizas con Teams desarrollo de aplicaciones, entiendes sus fundamentos fundamentales. Usted entiende que hay más de una manera de construir ciertas características. En estos escenarios, considere cómo puede proporcionar una experiencia más nativa al usuario.
Por ejemplo, puede recopilar la entrada del usuario en un formulario creado como una pestaña en la aplicación. También puede hacerlo mediante un módulo de tareas sin cambiar de vista e interrumpir el flujo de trabajo del usuario. Es importante elegir puntos de extensión que proporcionen menos desviación del flujo de trabajo regular de un usuario.

## <a name="see-also"></a>Vea también

[Crear aplicaciones para Teams](../overview.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Puntos de entrada de la aplicación de Teams](../concepts/extensibility-points.md)

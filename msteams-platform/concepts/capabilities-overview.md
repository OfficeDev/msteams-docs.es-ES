---
title: Comprender las funcionalidades de la aplicación
author: heath-hamilton
description: Características de la aplicación de Teams explicadas
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: f670f1f7b3db01f89fab4335c33f92e02cad1d9a
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058491"
---
# <a name="understand-microsoft-teams-app-capabilities"></a>Comprender las capacidades de la aplicación de Microsoft Teams

La extensibilidad o los puntos de entrada son diferentes formas en las que una aplicación puede manifestarse a un usuario. Por ejemplo, un usuario puede interactuar con una aplicación en una pestaña de lienzo para realizar una actividad o puede optar por hacer lo mismo con un bot de conversación. Las distintas funcionalidades usadas para crear la aplicación de Teams te permiten aumentar su ámbito de uso.

Hay varias formas de extender Teams, por lo que cada aplicación es única. Algunos solo tienen una funcionalidad, como un webhook, mientras que otros tienen más de una característica para ofrecer a los usuarios varias opciones. Por ejemplo, la aplicación puede mostrar datos en  una ubicación central, es decir, la pestaña y presentar esa misma información a través de una interfaz conversacional, es decir, el **bot**.

## <a name="app-capabilities"></a>Capacidades de la aplicación

La aplicación de Teams tiene una o todas las siguientes funcionalidades principales:

* [Pestañas](../tabs/what-are-tabs.md)
* [Extensiones de mensajería](../messaging-extensions/what-are-messaging-extensions.md)
* [Bots](../bots/what-are-bots.md)
* [Webhooks y conectores](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

La aplicación también puede aprovechar las capacidades avanzadas, como la API de [Microsoft Graph para Teams](https://docs.microsoft.com/graph/teams-concept-overview).

La siguiente ilustración te ofrece una idea de qué funcionalidades proporcionarán las características que quieras en la aplicación.

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Mapa de la mente que ilustra las funcionalidades de la aplicación de Teams.":::

## <a name="always-consider-your-user"></a>Tenga en cuenta siempre al usuario

A medida que te familiarices con el desarrollo de aplicaciones de Teams, comprendes sus fundamentos básicos. Comprende que hay más de una forma de crear determinadas características. En estos escenarios, considere cómo puede proporcionar una experiencia más nativa al usuario.
Por ejemplo, puedes recopilar la entrada del usuario en un formulario creado como una pestaña en la aplicación. También puede hacerlo con un módulo de tareas sin cambiar las vistas y interrumpir el flujo de trabajo del usuario. Es importante elegir puntos de extensión que proporcionen una desviación mínima del flujo de trabajo normal de un usuario.

## <a name="see-also"></a>Vea también

- [Crear aplicaciones para Teams](../overview.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Puntos de entrada de la aplicación de Teams](../concepts/extensibility-points.md)

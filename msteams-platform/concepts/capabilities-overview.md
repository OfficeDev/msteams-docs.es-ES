---
title: Comprender las características de la aplicación
author: heath-hamilton
description: Descripción de las funcionalidades de la aplicación Teams, como pestañas, bots, extensiones de mensajería y webhooks y conectores; ámbito de la aplicación, como aplicaciones personales y compartidas
ms.topic: conceptual
ms.localizationpriority: high
ms.author: lajanuar
ms.date: 09/22/2020
keywords: pestañas bots extensiones de mensajería webhooks conectores
ms.openlocfilehash: 7200e785bc7c857aa65cf8b228720fe8e1d40a66
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2022
ms.locfileid: "63398956"
---
# <a name="understand-microsoft-teams-app-features"></a>Comprender las características de la aplicación Microsoft Teams

Hay varias maneras de ampliar Teams para que cada aplicación sea única. Una aplicación de Teams puede manifestarse a sí misma para un usuario de maneras diferentes. Las características de una aplicación de Teams incluyen:

* Capacidades de la aplicación
* Ámbito de la aplicación

Por ejemplo, un usuario puede interactuar con una aplicación en una pestaña de lienzo para realizar una actividad o puede optar por hacer lo mismo con un bot de conversación. Solo puede usar una funcionalidad, como un webhook, mientras que otros tienen más de una característica para ofrecer a los usuarios varias opciones.

Estas capacidades pueden existir en diferentes ámbitos. Por ejemplo, su aplicación puede mostrar datos en una ubicación central compartida, es decir, la pestaña y presentar esa misma información a través de una interfaz de conversación personal, es decir, el bot.

## <a name="app-capabilities"></a>Capacidades de la aplicación

Para poder ampliar la aplicación, debe comprender todas las funcionalidades principales y los puntos de entrada que funcionan en un espacio de colaboración. Puede experimentar con los puntos de extensión para compilar las aplicaciones. Los componentes importantes del proyecto de la aplicación le ayudan a configurar correctamente la página de la aplicación.

Las aplicaciones Teams tienen una o todas las funcionalidades principales siguientes:

:::row:::
   :::column span="":::

### <a name="personal-apps"></a>Aplicaciones personales

Una [aplicación personal](../concepts/design/personal-apps.md) es un espacio dedicado o un bot para ayudar a los usuarios a centrarse en sus propias tareas o ver actividades importantes para ellos.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-personal-apps-2021.png" alt-text="Representación conceptual de cómo son las aplicaciones personales en el cliente de Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::
   :::column span="":::

### <a name="tabs"></a>Pestañas

Muestre el contenido basado en la web en una [pestaña](../tabs/what-are-tabs.md) donde los usuarios puedan analizarlo y trabajar en él juntos.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-channel-chat-apps-2021.png" alt-text="Representación conceptual de cómo son las pestañas en el cliente de Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::
   :::column span="":::

### <a name="bots"></a>Bots

Las conversaciones suelen dar lugar a una necesidad de hacer algo (generar un pedido, revisar mi código, comprobar el estado del vale, etc.). Un [bot](../bots/what-are-bots.md) puede iniciar estos tipos de flujos de trabajo directamente dentro de Teams.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-bots-2021.png" alt-text="Representación conceptual de cómo son los bots en el cliente de Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a>Extensiones de mensajería

Con las [extensiones de mensajería](../messaging-extensions/what-are-messaging-extensions.md), puede compartir rápidamente información externa en una conversación. También puede actuar sobre un mensaje, como crear una incidencia de ayuda basada en el contenido de una publicación del canal.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-messaging-extensions-2021.png" alt-text="Representación conceptual de cómo son las extensiones de mensajería en el cliente de Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="meeting-extensions"></a>Extensiones de reunión

Hay algunas opciones para [incorporar la aplicación a la experiencia de llamada de Teams](../apps-in-teams-meetings/design/designing-apps-in-meetings.md).

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-meeting-extensions-2021.png" alt-text="Representación conceptual de cómo son las extensiones de reunión en el cliente de Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="webhooks-and-connectors"></a>Webhooks y conectores

Los [webhooks entrantes](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) son una manera sencilla de enviar automáticamente notificaciones desde otra aplicación a un canal de Teams. Con los [webhooks salientes](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), envíe un mensaje al servicio web con un @mention.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-connectors.png" alt-text="Representación conceptual de cómo son los conectores en el cliente de Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph para Teams

La [API de Microsoft Graph para Teams](/graph/teams-concept-overview) proporciona acceso a información sobre equipos, canales, usuarios y mensajes que pueden ayudarle a crear o mejorar características para su aplicación (como notificaciones enriquecidas).

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-graph.png" alt-text="Representación conceptual de la API de Microsoft Graph para Teams." border="false":::

   :::column-end:::
:::row-end:::

> [!NOTE]
> La tienda de Teams ha evolucionado: anteriormente, las aplicaciones LOB se actualizaban seleccionando los puntos suspensivos en el mosaico. Con la experiencia actualizada de la tienda de Teams, ahora puede actualizar las aplicaciones LOB iniciando sesión en el [Centro de administración de Teams](https://admin.teams.microsoft.com).

## <a name="choose-the-correct-scope-for-your-app"></a>Elegir el ámbito correcto para la aplicación

Puede elegir el ámbito de la aplicación entre los siguientes:

* Experiencia de aplicación personal: una aplicación personal es un bot o espacio dedicado para ayudar a los usuarios a centrarse en sus propias tareas o ver actividades importantes para ellos.
* Experiencia de aplicación compartida: el equipo, el canal y el chat son espacios de colaboración. Las aplicaciones en estos contextos están disponibles para todos los usuarios de ese espacio. Normalmente, los espacios de colaboración se centran en los flujos de trabajo para las interacciones de la aplicación o para desbloquear nuevas interacciones sociales.

## <a name="see-also"></a>Consulte también

* [Crear aplicaciones para Teams](../overview.md)
* [Crear su primera aplicación de Microsoft Teams](../build-your-first-app/build-first-app-overview.md)

---
title: Diseñar notificaciones de fuentes de actividades
author: heath-hamilton
description: 'Obtenga información sobre cómo diseñar notificaciones de fuente de actividad para la aplicación de Teams y obtener el kit de interfaz de usuario de Teams. Desarrollo de notificaciones desde el canal de Teams en Visual Studio C #'
ms.localizationpriority: medium
ms.author: surbhigupta
ms.topic: reference
ms.openlocfilehash: 9a17027f7dd68993a118f24bb23cfff0a56651e1
ms.sourcegitcommit: 4ba6392eced76ba6baeb6d6dd9ba426ebf4ab24f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2022
ms.locfileid: "66919770"
---
# <a name="designing-activity-feed-notifications-for-your-microsoft-teams-app"></a>Diseño de notificaciones de fuente de actividad para la aplicación de Microsoft Teams

La fuente de actividad es una superficie para que los usuarios accedan a sus notificaciones en Microsoft Teams. La fuente conserva las notificaciones de las últimas cuatro semanas.

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-overview.png" alt-text="En el ejemplo se muestra una notificación de aplicación que se muestra en la fuente de actividades de Teams en el móvil.":::

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/desktop-overview.png" alt-text="En el ejemplo se muestra una notificación de aplicación que se muestra en la fuente de actividad de Teams.":::

---

## <a name="anatomy"></a>Anatomía

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-anatomy.png" alt-text="Diseño de la anatomía de la notificación de fuente de actividad de Teams.":::

|Contador|Descripción|
|----------|-----------|
|1|**Avatar**: muestra quién inició la actividad.|
|2|**Icono de tipo de actividad o aplicación**: representa el tipo de actividad. En el caso de las notificaciones de aplicación, el icono de línea se reemplaza por un icono de aplicación.|
|3|**Título (primera línea): Actor y motivo**: *Actor*: Nombre del usuario o la aplicación que inició la actividad. *Motivo*: describe la actividad.|
|4|**Marca de tiempo**: muestra cuándo se produjo la actividad.|
|5|**Ubicación (segunda línea):** muestra dónde se produjo la actividad en Teams.|
|6|**Vista previa de texto (tercera línea):** muestra una línea truncada desde el inicio de la notificación.|

## <a name="types-of-activity-feed-notification-cards"></a>Tipos de tarjetas de notificación de fuente de actividad

Las siguientes variantes muestran los tipos de tarjetas de notificación de fuente de actividad que puede mostrar. El logotipo de la aplicación reemplaza el avatar del usuario para las notificaciones generadas por la aplicación.

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-types.png" alt-text="Variantes de las tarjetas de fuente de actividad de Teams.":::

## <a name="manage-activity-feed-notifications"></a>Administración de notificaciones de fuente de actividad

Los usuarios pueden administrar las notificaciones enviadas desde la aplicación en la página de configuración de Teams.

## <a name="related-system-notifications"></a>Notificaciones del sistema relacionadas

Cada actividad genera una notificación del sistema. Lo que se muestra depende de lo que el usuario configure en sus opciones de notificación. Los usuarios también pueden elegir un estilo de notificación en función de su sistema operativo.

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-related-system-notifications.png" alt-text="Variantes de las tarjetas de fuente de actividad de Teams en Android e iOS.":::

|Contador|Descripción|
|----------|-----------|
|1|Android|
|2|iOS|

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/related-system-notifications.png" alt-text="Variantes de tarjetas de actividad de Teams en diferentes sistemas operativos.":::

|Contador|Descripción|
|----------|-----------|
|1|Personalizado de Teams|
|2|Windows|
|3|Mac|

---

## <a name="step-by-step-guide"></a>Guía paso a paso

Siga la [guía paso a paso](../../sbs-graphactivity-feedbroadcast.yml) para enviar notificaciones de fuente de actividad en Teams.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Implementar notificaciones de fuente de actividad](/graph/teams-send-activityfeednotifications)

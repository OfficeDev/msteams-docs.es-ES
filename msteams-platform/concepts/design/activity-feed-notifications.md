---
title: Diseño de notificaciones de fuentes de actividad
author: heath-hamilton
description: Obtén información sobre cómo diseñar notificaciones de fuentes de actividad para tu Teams aplicación y obtener el kit Microsoft Teams interfaz de usuario.
ms.localizationpriority: medium
ms.author: surbhigupta
ms.topic: reference
ms.openlocfilehash: 552541e17422d20297d857a4273ec807d11e6928
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157529"
---
# <a name="designing-activity-feed-notifications-for-your-microsoft-teams-app"></a>Diseño de notificaciones de fuente de actividad para la Microsoft Teams aplicación

La fuente de actividad es una superficie para que los usuarios puedan acceder a sus notificaciones en Microsoft Teams. La fuente conserva las notificaciones de las últimas cuatro semanas.

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-overview.png" alt-text="Ejemplo muestra una notificación de aplicación que se muestra en la fuente Teams actividad en el móvil." border="false":::

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/desktop-overview.png" alt-text="En el ejemplo se muestra una notificación de aplicación en la Teams de actividad." border="false":::

---

## <a name="anatomy"></a>Anatomía

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-anatomy.png" alt-text="Diseñar la anatomía de la notificación Teams fuente de actividad." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Avatar:** muestra quién inició la actividad.|
|2|**Icono de tipo de actividad/aplicación:** muestra el tipo de actividad. Para las notificaciones de aplicaciones, el icono de línea se reemplaza por un icono de aplicación.|
|3|**Título (primera línea): Actor + motivo**: *Actor*: Nombre del usuario o aplicación que inició la actividad. *Motivo:* describe la actividad.|
|4 |**Marca de** tiempo: muestra cuándo se produjo la actividad.|
|5 |**Ubicación (segunda línea):** muestra dónde se produjo la actividad en Teams.|
|6 |**Información terciaria (tercera línea):** opcional. Muestra texto de vista previa o información adicional.|

## <a name="types-of-activity-feed-notification-cards"></a>Tipos de tarjetas de notificación de fuente de actividad

Las siguientes variantes muestran los tipos de tarjetas de notificación de fuente de actividad que puede mostrar. El logotipo de la aplicación reemplaza el avatar del usuario para las notificaciones generadas por la aplicación.

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-types.png" alt-text="Variantes de Teams de fuente de actividad." border="false":::

## <a name="manage-activity-feed-notifications"></a>Administrar notificaciones de fuentes de actividad

Los usuarios pueden administrar las notificaciones enviadas desde la aplicación en la Teams de configuración.

## <a name="related-system-notifications"></a>Notificaciones del sistema relacionadas

Cada actividad genera una notificación del sistema. Lo que se muestra depende de lo que el usuario configure en sus opciones de notificación. Los usuarios también pueden elegir un estilo de notificación basado en su sistema operativo.

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-related-system-notifications.png" alt-text="Variantes de Teams de fuente de actividad en Android e iOS." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|Android|
|2|iOS|

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/related-system-notifications.png" alt-text="Variantes de Teams de actividad en diferentes sistemas operativos." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|Teams personalizado|
|2|Windows|
|3|Mac|

---

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Implementar notificaciones de fuente de actividades](/graph/teams-send-activityfeednotifications)

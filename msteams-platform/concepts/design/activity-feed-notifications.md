---
title: Diseño de notificaciones de fuentes de actividad
author: heath-hamilton
description: Obtén información sobre cómo diseñar notificaciones de fuentes de actividad para tu Teams aplicación y obtener el kit Microsoft Teams interfaz de usuario.
localization_priority: Normal
ms.author: surbhigupta
ms.topic: reference
ms.openlocfilehash: 61a2a6da2a5ed0cb3126b9798094b06c575c9b6c
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631361"
---
# <a name="designing-activity-feed-notifications-for-your-microsoft-teams-app"></a><span data-ttu-id="1a599-103">Diseño de notificaciones de fuente de actividad para la Microsoft Teams aplicación</span><span class="sxs-lookup"><span data-stu-id="1a599-103">Designing activity feed notifications for your Microsoft Teams app</span></span>

<span data-ttu-id="1a599-104">La fuente de actividad es una superficie para que los usuarios puedan acceder a sus notificaciones en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1a599-104">The activity feed is a surface for users to access their notifications in Microsoft Teams.</span></span> <span data-ttu-id="1a599-105">La fuente conserva las notificaciones de las últimas cuatro semanas.</span><span class="sxs-lookup"><span data-stu-id="1a599-105">The feed retains notifications from the past four weeks.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="1a599-106">Escritorio</span><span class="sxs-lookup"><span data-stu-id="1a599-106">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/desktop-overview.png" alt-text="En el ejemplo se muestra una notificación de aplicación en la Teams de actividad." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="1a599-108">Móvil</span><span class="sxs-lookup"><span data-stu-id="1a599-108">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-overview.png" alt-text="Ejemplo muestra una notificación de aplicación que se muestra en la fuente Teams actividad en el móvil." border="false":::

---

## <a name="anatomy"></a><span data-ttu-id="1a599-110">Anatomía</span><span class="sxs-lookup"><span data-stu-id="1a599-110">Anatomy</span></span>

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-anatomy.png" alt-text="Diseñar la anatomía de la notificación Teams fuente de actividad." border="false":::

|<span data-ttu-id="1a599-112">Contador</span><span class="sxs-lookup"><span data-stu-id="1a599-112">Counter</span></span>|<span data-ttu-id="1a599-113">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a599-113">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="1a599-114">1</span><span class="sxs-lookup"><span data-stu-id="1a599-114">1</span></span>|<span data-ttu-id="1a599-115">**Avatar:** muestra quién inició la actividad.</span><span class="sxs-lookup"><span data-stu-id="1a599-115">**Avatar**: Shows who initiated the activity.</span></span>|
|<span data-ttu-id="1a599-116">2</span><span class="sxs-lookup"><span data-stu-id="1a599-116">2</span></span>|<span data-ttu-id="1a599-117">**Icono de tipo de actividad/aplicación:** muestra el tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="1a599-117">**Activity type/app icon**: Depicts the type of activity.</span></span> <span data-ttu-id="1a599-118">Para las notificaciones de aplicaciones, el icono de línea se reemplaza por un icono de aplicación.</span><span class="sxs-lookup"><span data-stu-id="1a599-118">For app notifications, the line icon is replaced with an app icon.</span></span>|
|<span data-ttu-id="1a599-119">3</span><span class="sxs-lookup"><span data-stu-id="1a599-119">3</span></span>|<span data-ttu-id="1a599-120">**Título (primera línea): Actor + motivo**: *Actor*: Nombre del usuario o aplicación que inició la actividad.</span><span class="sxs-lookup"><span data-stu-id="1a599-120">**Title (first line): Actor + reason**: *Actor*: Name of the user or app that initiated the activity.</span></span> <span data-ttu-id="1a599-121">*Motivo:* describe la actividad.</span><span class="sxs-lookup"><span data-stu-id="1a599-121">*Reason*: Describes the activity.</span></span>|
|<span data-ttu-id="1a599-122">4 </span><span class="sxs-lookup"><span data-stu-id="1a599-122">4</span></span>|<span data-ttu-id="1a599-123">**Marca de** tiempo: muestra cuándo se produjo la actividad.</span><span class="sxs-lookup"><span data-stu-id="1a599-123">**Timestamp**: Shows when the activity happened.</span></span>|
|<span data-ttu-id="1a599-124">5 </span><span class="sxs-lookup"><span data-stu-id="1a599-124">5</span></span>|<span data-ttu-id="1a599-125">**Ubicación (segunda línea):** muestra dónde se produjo la actividad en Teams.</span><span class="sxs-lookup"><span data-stu-id="1a599-125">**Location (second line)**: Shows where the activity happened in Teams.</span></span>|
|<span data-ttu-id="1a599-126">6 </span><span class="sxs-lookup"><span data-stu-id="1a599-126">6</span></span>|<span data-ttu-id="1a599-127">**Información terciaria (tercera línea):** opcional.</span><span class="sxs-lookup"><span data-stu-id="1a599-127">**Tertiary information (third line)**: Optional.</span></span> <span data-ttu-id="1a599-128">Muestra texto de vista previa o información adicional.</span><span class="sxs-lookup"><span data-stu-id="1a599-128">Shows preview text or additional information.</span></span>|

## <a name="types-of-activity-feed-notification-cards"></a><span data-ttu-id="1a599-129">Tipos de tarjetas de notificación de fuente de actividad</span><span class="sxs-lookup"><span data-stu-id="1a599-129">Types of activity feed notification cards</span></span>

<span data-ttu-id="1a599-130">Las siguientes variantes muestran los tipos de tarjetas de notificación de fuente de actividad que puede mostrar.</span><span class="sxs-lookup"><span data-stu-id="1a599-130">The following variants show the kinds of activity feed notification cards you can display.</span></span> <span data-ttu-id="1a599-131">El logotipo de la aplicación reemplaza el avatar del usuario para las notificaciones generadas por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1a599-131">The app logo replaces the user avatar for app-generated notifications.</span></span>

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-types.png" alt-text="Variantes de Teams de fuente de actividad." border="false":::

## <a name="manage-activity-feed-notifications"></a><span data-ttu-id="1a599-133">Administrar notificaciones de fuentes de actividad</span><span class="sxs-lookup"><span data-stu-id="1a599-133">Manage activity feed notifications</span></span>

<span data-ttu-id="1a599-134">Los usuarios pueden administrar las notificaciones enviadas desde la aplicación en la Teams de configuración.</span><span class="sxs-lookup"><span data-stu-id="1a599-134">Users can manage notifications sent from your app in the Teams settings page.</span></span>

## <a name="related-system-notifications"></a><span data-ttu-id="1a599-135">Notificaciones del sistema relacionadas</span><span class="sxs-lookup"><span data-stu-id="1a599-135">Related system notifications</span></span>

<span data-ttu-id="1a599-136">Cada actividad genera una notificación del sistema.</span><span class="sxs-lookup"><span data-stu-id="1a599-136">Each activity generates a system notification.</span></span> <span data-ttu-id="1a599-137">Lo que se muestra depende de lo que el usuario configure en sus opciones de notificación.</span><span class="sxs-lookup"><span data-stu-id="1a599-137">What displays depends on what the user configures in their notification settings.</span></span> <span data-ttu-id="1a599-138">Los usuarios también pueden elegir un estilo de notificación basado en su sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="1a599-138">Users can also choose a notification style based on their operating system.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="1a599-139">Escritorio</span><span class="sxs-lookup"><span data-stu-id="1a599-139">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/related-system-notifications.png" alt-text="Variantes de Teams de actividad en diferentes sistemas operativos." border="false":::

|<span data-ttu-id="1a599-141">Contador</span><span class="sxs-lookup"><span data-stu-id="1a599-141">Counter</span></span>|<span data-ttu-id="1a599-142">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a599-142">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="1a599-143">1</span><span class="sxs-lookup"><span data-stu-id="1a599-143">1</span></span>|<span data-ttu-id="1a599-144">Teams personalizado</span><span class="sxs-lookup"><span data-stu-id="1a599-144">Teams custom</span></span>|
|<span data-ttu-id="1a599-145">2</span><span class="sxs-lookup"><span data-stu-id="1a599-145">2</span></span>|<span data-ttu-id="1a599-146">Windows</span><span class="sxs-lookup"><span data-stu-id="1a599-146">Windows</span></span>|
|<span data-ttu-id="1a599-147">3</span><span class="sxs-lookup"><span data-stu-id="1a599-147">3</span></span>|<span data-ttu-id="1a599-148">Mac</span><span class="sxs-lookup"><span data-stu-id="1a599-148">Mac</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="1a599-149">Móvil</span><span class="sxs-lookup"><span data-stu-id="1a599-149">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-related-system-notifications.png" alt-text="Variantes de Teams de fuente de actividad en Android e iOS." border="false":::

|<span data-ttu-id="1a599-151">Contador</span><span class="sxs-lookup"><span data-stu-id="1a599-151">Counter</span></span>|<span data-ttu-id="1a599-152">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a599-152">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="1a599-153">1</span><span class="sxs-lookup"><span data-stu-id="1a599-153">1</span></span>|<span data-ttu-id="1a599-154">Android</span><span class="sxs-lookup"><span data-stu-id="1a599-154">Android</span></span>|
|<span data-ttu-id="1a599-155">2</span><span class="sxs-lookup"><span data-stu-id="1a599-155">2</span></span>|<span data-ttu-id="1a599-156">iOS</span><span class="sxs-lookup"><span data-stu-id="1a599-156">iOS</span></span>|

---

## <a name="next-step"></a><span data-ttu-id="1a599-157">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="1a599-157">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1a599-158">Implementar notificaciones de fuente de actividades</span><span class="sxs-lookup"><span data-stu-id="1a599-158">Implement activity feed notifications</span></span>](/graph/teams-send-activityfeednotifications)

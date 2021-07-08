---
title: Diseñar la aplicación con componentes de interfaz de usuario avanzados
author: heath-hamilton
description: Obtenga información sobre los componentes de la interfaz de usuario usados Teams .
ms.author: surbhigupta
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: 6f2bd9cd237751adb15db45bbd6e3cdfea35ce09
ms.sourcegitcommit: b1f9162a0bbcd276064ae9e4f1e8bccc06cb7035
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/07/2021
ms.locfileid: "53328082"
---
# <a name="designing-your-microsoft-teams-app-with-advanced-ui-components"></a><span data-ttu-id="62649-103">Diseñar la aplicación Microsoft Teams con componentes de interfaz de usuario avanzados</span><span class="sxs-lookup"><span data-stu-id="62649-103">Designing your Microsoft Teams app with advanced UI components</span></span>

<span data-ttu-id="62649-104">Los siguientes componentes son una combinación de componentes básicos de [la](~/concepts/design/design-teams-app-basic-ui-components.md) interfaz de usuario que puedes usar para situaciones comunes Teams de diseño, como la navegación.</span><span class="sxs-lookup"><span data-stu-id="62649-104">The following components are a combination of [basic UI components](~/concepts/design/design-teams-app-basic-ui-components.md) that you can use for common Teams design situations, such as navigation.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="62649-105">Kit de interfaz de usuario de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="62649-105">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="62649-106">En función <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">de Fluent interfaz de</a>usuario, el kit Microsoft Teams de interfaz de usuario incluye componentes y patrones diseñados específicamente para crear Teams aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="62649-106">Based on <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent UI</a>, the Microsoft Teams UI Kit includes components and patterns that are designed specifically for building Teams apps.</span></span> <span data-ttu-id="62649-107">En el kit de interfaz de usuario, puedes agarrar e insertar los componentes enumerados aquí directamente en el diseño y ver más ejemplos de cómo usar cada componente.</span><span class="sxs-lookup"><span data-stu-id="62649-107">In the UI kit, you can grab and insert the components listed here directly into your design and see more examples of how to use each component.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="62649-108">Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="62649-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="breadcrumb"></a><span data-ttu-id="62649-109">Ruta de navegación</span><span class="sxs-lookup"><span data-stu-id="62649-109">Breadcrumb</span></span>

<span data-ttu-id="62649-110">Las rutas de navegación son una ayuda de navegación que transmite la jerarquía de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="62649-110">Breadcrumbs are a navigational aid that convey your app’s hierarchy.</span></span> <span data-ttu-id="62649-111">Ayudan a los usuarios a comprender cómo la página que están viendo se ajusta a la experiencia general y ofrecen acceso con un solo clic a niveles más altos de esa jerarquía.</span><span class="sxs-lookup"><span data-stu-id="62649-111">They help users understand how the page they’re viewing fits into the overall experience and afford one-click access to higher levels in that hierarchy.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="62649-112">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="62649-112">Top use cases</span></span>

* <span data-ttu-id="62649-113">Jerarquía de comunicación</span><span class="sxs-lookup"><span data-stu-id="62649-113">Communicate hierarchy</span></span>
* <span data-ttu-id="62649-114">Navegación</span><span class="sxs-lookup"><span data-stu-id="62649-114">Navigation</span></span>

# <a name="desktop"></a>[<span data-ttu-id="62649-115">Escritorio</span><span class="sxs-lookup"><span data-stu-id="62649-115">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="En el ejemplo se muestra una plantilla de ruta de navegación en el escritorio." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="62649-117">Móvil</span><span class="sxs-lookup"><span data-stu-id="62649-117">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-breadcrumb.png" alt-text="En el ejemplo se muestra una plantilla de ruta de navegación en el móvil." border="false":::

---

## <a name="left-nav"></a><span data-ttu-id="62649-119">Navegación izquierda</span><span class="sxs-lookup"><span data-stu-id="62649-119">Left nav</span></span>

<span data-ttu-id="62649-120">Use la navegación izquierda para examinar varias páginas dentro de la Teams pestaña. En el siguiente ejemplo, la navegación izquierda se encuentra entre la lista de canales y el contenido de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="62649-120">Use the left nav to browse multiple pages within your Teams tab. In the following example, the left nav is between the channel list and tab content.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="62649-121">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="62649-121">Top use cases</span></span>

* <span data-ttu-id="62649-122">Examinar varias páginas dentro de una Teams pestaña.</span><span class="sxs-lookup"><span data-stu-id="62649-122">Browse multiple pages within a Teams tab.</span></span>
* <span data-ttu-id="62649-123">Dividir aplicaciones complejas en varias páginas.</span><span class="sxs-lookup"><span data-stu-id="62649-123">Break down complex apps into multiple pages.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="62649-124">Escritorio</span><span class="sxs-lookup"><span data-stu-id="62649-124">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="En el ejemplo se muestra una plantilla de navegación izquierda en el escritorio." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="62649-126">Móvil</span><span class="sxs-lookup"><span data-stu-id="62649-126">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-left-nav.png" alt-text="En el ejemplo se muestra una plantilla de navegación izquierda en el móvil." border="false":::

---

## <a name="notification-bar"></a><span data-ttu-id="62649-128">Barra de notificaciones</span><span class="sxs-lookup"><span data-stu-id="62649-128">Notification bar</span></span>

<span data-ttu-id="62649-129">Una barra de notificaciones es un área dedicada para mostrar mensajes breves e importantes que no requieren que el usuario tome medidas inmediatas.</span><span class="sxs-lookup"><span data-stu-id="62649-129">A notification bar is a dedicated area for displaying a brief, important messages that do not require the user to take immediate action.</span></span> <span data-ttu-id="62649-130">Los iconos y los colores de fondo específicos están asociados con tipos específicos de mensajes (vea a continuación).</span><span class="sxs-lookup"><span data-stu-id="62649-130">Specific background colors and icons are associated with specific types of messages (see below).</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="62649-131">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="62649-131">Top use cases</span></span>

* <span data-ttu-id="62649-132">Mensajes críticos, errores y advertencias</span><span class="sxs-lookup"><span data-stu-id="62649-132">Critical messages, errors, and warnings</span></span>
* <span data-ttu-id="62649-133">Mensajes de éxito</span><span class="sxs-lookup"><span data-stu-id="62649-133">Success messages</span></span>
* <span data-ttu-id="62649-134">Mensajes informativos o promocionales</span><span class="sxs-lookup"><span data-stu-id="62649-134">Informational or promotional messages</span></span>

# <a name="desktop"></a>[<span data-ttu-id="62649-135">Escritorio</span><span class="sxs-lookup"><span data-stu-id="62649-135">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="En el ejemplo se muestran las plantillas de interfaz de usuario de la barra de notificaciones en el escritorio." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="62649-137">Móvil</span><span class="sxs-lookup"><span data-stu-id="62649-137">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-notification-bar.png" alt-text="En el ejemplo se muestra la plantilla de interfaz de usuario de la barra de notificaciones en el móvil." border="false":::

---

## <a name="stage"></a><span data-ttu-id="62649-139">Etapa</span><span class="sxs-lookup"><span data-stu-id="62649-139">Stage</span></span>

<span data-ttu-id="62649-140">Stage permite a los usuarios ver contenido (como una imagen, un archivo o un sitio web) en una superficie grande Teams sin cambiar de contexto.</span><span class="sxs-lookup"><span data-stu-id="62649-140">Stage lets users view content—like an image, file, or website—on a large surface in Teams without switching context.</span></span> <span data-ttu-id="62649-141">La fase es principalmente para ver contenido.</span><span class="sxs-lookup"><span data-stu-id="62649-141">Stage is primarily for viewing content.</span></span> <span data-ttu-id="62649-142">No use fases para interacciones complejas.</span><span class="sxs-lookup"><span data-stu-id="62649-142">Don’t use stage for complex interactions.</span></span>

<span data-ttu-id="62649-143">Obtenga información sobre cómo implementar [la fase](~/tabs/tabs-link-unfurling.md).</span><span class="sxs-lookup"><span data-stu-id="62649-143">Learn how to implement [stage](~/tabs/tabs-link-unfurling.md).</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="62649-144">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="62649-144">Top use cases</span></span>

* <span data-ttu-id="62649-145">Mostrar contenido en una superficie grande dentro de Teams en lugar de otra aplicación o explorador</span><span class="sxs-lookup"><span data-stu-id="62649-145">Display content in a large surface within Teams instead of another app or browser</span></span>
* <span data-ttu-id="62649-146">Contenido multimedia destacado u otro contenido enriquecido</span><span class="sxs-lookup"><span data-stu-id="62649-146">Spotlight media or other rich content</span></span>

# <a name="desktop"></a>[<span data-ttu-id="62649-147">Escritorio</span><span class="sxs-lookup"><span data-stu-id="62649-147">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="En el ejemplo se muestra una plantilla de fase en el escritorio." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="62649-149">Móvil</span><span class="sxs-lookup"><span data-stu-id="62649-149">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="62649-150">La aplicación puede iniciar una fase desde una tarjeta adaptable, un vínculo compartido o componentes visuales (como un gráfico).</span><span class="sxs-lookup"><span data-stu-id="62649-150">Your app can launch a stage from an Adaptive Card, shared link, or visual components (such as a chart).</span></span>

:::image type="content" source="../../assets/images/ui-templates/mobile-stage.png" alt-text="En el ejemplo se muestra una plantilla de fase en el móvil." border="false":::

---

## <a name="toolbar"></a><span data-ttu-id="62649-152">Barra de herramientas</span><span class="sxs-lookup"><span data-stu-id="62649-152">Toolbar</span></span>

<span data-ttu-id="62649-153">Una barra de herramientas es un contenedor para agrupar un conjunto de controles.</span><span class="sxs-lookup"><span data-stu-id="62649-153">A toolbar is a container for grouping a set of controls.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="62649-154">Casos de uso principales</span><span class="sxs-lookup"><span data-stu-id="62649-154">Top use cases</span></span>

* <span data-ttu-id="62649-155">Acciones contextuales en el contenido de la aplicación</span><span class="sxs-lookup"><span data-stu-id="62649-155">Contextual actions on app content</span></span>
* <span data-ttu-id="62649-156">Filtro contextual y búsqueda</span><span class="sxs-lookup"><span data-stu-id="62649-156">Contextual filter and find</span></span>
* <span data-ttu-id="62649-157">Navegación y rutas de navegación</span><span class="sxs-lookup"><span data-stu-id="62649-157">Navigation and breadcrumbs</span></span>

# <a name="desktop"></a>[<span data-ttu-id="62649-158">Escritorio</span><span class="sxs-lookup"><span data-stu-id="62649-158">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="En el ejemplo se muestra una plantilla de barra de herramientas en el escritorio." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="62649-160">Móvil</span><span class="sxs-lookup"><span data-stu-id="62649-160">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-toolbar.png" alt-text="En el ejemplo se muestra una plantilla de barra de herramientas en el móvil." border="false":::

---

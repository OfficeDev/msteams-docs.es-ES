---
title: Quitar márgenes de tabulación en Microsoft Teams
author: laujan
description: Describe cómo la eliminación de márgenes de tabulación mejorará la experiencia del desarrollador.
keywords: tab removing margins padding
ms.topic: reference
localization_priority: Normal
ms.author: lomeybur
ms.openlocfilehash: 78d97dca73e7fce2bf4b911f5ea4588525667378
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019716"
---
# <a name="tab-margin-changes"></a><span data-ttu-id="b3319-104">Cambios del margen de pestaña</span><span class="sxs-lookup"><span data-stu-id="b3319-104">Tab margin changes</span></span>

<span data-ttu-id="b3319-105">En este documento se describe cómo la eliminación de márgenes alrededor de todas las pestañas de Microsoft Teams mejorará la experiencia del desarrollador al crear aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b3319-105">This document describes how the removal of margins around all tabs in Microsoft Teams will enhance the developer's experience when building apps.</span></span> <span data-ttu-id="b3319-106">Esta es una mejora introducida en Microsoft Teams 2021.</span><span class="sxs-lookup"><span data-stu-id="b3319-106">This is an enhancement introduced in Microsoft Teams in 2021.</span></span>
<span data-ttu-id="b3319-107">La eliminación de los márgenes alrededor de todas las pestañas permitirá a los desarrolladores crear aplicaciones que se vean más nativas de Teams.</span><span class="sxs-lookup"><span data-stu-id="b3319-107">Removing the margins around all tabs will allow developers to build apps that look more native to Teams.</span></span> <span data-ttu-id="b3319-108">Esto también se alineará con nuestros diseños [de kit de interfaz de usuario.](~/tabs/design/tabs.md)</span><span class="sxs-lookup"><span data-stu-id="b3319-108">This will also align with our [UI kit designs](~/tabs/design/tabs.md).</span></span> <span data-ttu-id="b3319-109">La mayoría de las aplicaciones ya se ven mejor sin los márgenes que rodean sus experiencias.</span><span class="sxs-lookup"><span data-stu-id="b3319-109">Most apps already look better without the margins surrounding their experiences.</span></span> <span data-ttu-id="b3319-110">Sin embargo, algunas pestañas se ven afectadas visualmente por este cambio y los desarrolladores deben realizar los cambios necesarios.</span><span class="sxs-lookup"><span data-stu-id="b3319-110">However, some tabs are visually affected by this change, and developers must make the necessary changes.</span></span>

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="Inteligencia de tabulación y sin márgenes" border="false":::

> [!NOTE]
> <span data-ttu-id="b3319-112">Esta característica no se aplica a los clientes móviles, ya que las pestañas vistas en los clientes móviles no tienen márgenes.</span><span class="sxs-lookup"><span data-stu-id="b3319-112">This feature is not applicable to mobile clients, as the tabs viewed in the mobile clients do not have margins.</span></span> 

## <a name="timelines"></a><span data-ttu-id="b3319-113">Escalas de tiempo</span><span class="sxs-lookup"><span data-stu-id="b3319-113">Timelines</span></span>

* <span data-ttu-id="b3319-114">5 de marzo de 2021: Márgenes eliminados en [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="b3319-114">March 5, 2021 - Margins removed in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
* <span data-ttu-id="b3319-115">15 de junio de 2021: los márgenes se quitarán en producción.</span><span class="sxs-lookup"><span data-stu-id="b3319-115">June 15, 2021 - Margins will be removed in production.</span></span>

## <a name="guidelines"></a><span data-ttu-id="b3319-116">Instrucciones</span><span class="sxs-lookup"><span data-stu-id="b3319-116">Guidelines</span></span>

<span data-ttu-id="b3319-117">Microsoft Teams aplicaciones que usan pestañas se verán afectadas por este cambio.</span><span class="sxs-lookup"><span data-stu-id="b3319-117">Microsoft Teams apps that use tabs will be affected by this change.</span></span> <span data-ttu-id="b3319-118">Los desarrolladores deben cambiar a [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) para determinar cómo se ven afectadas sus pestañas y realizar los cambios necesarios.</span><span class="sxs-lookup"><span data-stu-id="b3319-118">Developers must switch to [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) in order to determine how their tabs are affected and make the necessary changes.</span></span>

<span data-ttu-id="b3319-119">Los desarrolladores de pestañas no deben confiar Teams para proporcionar márgenes que rodean sus pestañas.</span><span class="sxs-lookup"><span data-stu-id="b3319-119">Tab developers must not rely on Teams to provide margins surrounding their tabs.</span></span> <span data-ttu-id="b3319-120">Se recomienda a los desarrolladores que agreguen márgenes alrededor de sus diseños de pestañas cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b3319-120">Developers are encouraged to add margins around their tab designs where it is required.</span></span> <span data-ttu-id="b3319-121">Los diseños de aplicaciones en producción pueden parecer que hay un relleno adicional, es decir, los márgenes proporcionados por Teams y los márgenes proporcionados por la pestaña. Sin embargo, el relleno adicional es solo temporal y desaparecerá en unas semanas, dejando solo el relleno proporcionado por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b3319-121">App designs in production can look like there is extra padding, that is, margins provided by Teams and margins provided by the tab. However, the extra padding is only temporary and will go away in a few weeks, leaving only the app's provided padding.</span></span>

## <a name="faq"></a><span data-ttu-id="b3319-122">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="b3319-122">FAQ</span></span>

<span data-ttu-id="b3319-123">**¿Está bien que chrome de la aplicación, como la barra de encabezado o la barra de tareas, toque los bordes de nuestros diseños?**</span><span class="sxs-lookup"><span data-stu-id="b3319-123">**Is it OK for app chrome, such as header bar or taskbar, to touch the edges of our designs?**</span></span>

<span data-ttu-id="b3319-124">Sí, esto está bien y se recomienda.</span><span class="sxs-lookup"><span data-stu-id="b3319-124">Yes, this is fine and encouraged.</span></span> <span data-ttu-id="b3319-125">Esto ayuda a que la aplicación se sienta nativa.</span><span class="sxs-lookup"><span data-stu-id="b3319-125">This helps the app feel native.</span></span>

<span data-ttu-id="b3319-126">**¿Está bien que el contenido de la aplicación, como texto, logotipos e imágenes, toque los bordes izquierdo y derecho de nuestros diseños?**</span><span class="sxs-lookup"><span data-stu-id="b3319-126">**Is it OK for app content, such as text, logos, and images, to touch the left and right edges of our designs?**</span></span>

<span data-ttu-id="b3319-127">No, debes proporcionar tu propio relleno o márgenes a la izquierda y a la derecha de todo el contenido de la aplicación para asegurarte de que no toque los bordes de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="b3319-127">No, you must provide your own padding or margins to the left and right of all app content to ensure it does not touch the edges of your UI.</span></span> <span data-ttu-id="b3319-128">También puede agregar márgenes en la parte superior de la pestaña, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="b3319-128">You can also add margins at the top of your tab, if required.</span></span>

<span data-ttu-id="b3319-129">**¿Cuál es el tamaño de los márgenes Teams aplicados anteriormente?**</span><span class="sxs-lookup"><span data-stu-id="b3319-129">**What's the size of the margins Teams previously applied?**</span></span>

* <span data-ttu-id="b3319-130">Izquierda y derecha: 20 píxeles</span><span class="sxs-lookup"><span data-stu-id="b3319-130">Left and right: 20px</span></span>
* <span data-ttu-id="b3319-131">Top: 16px</span><span class="sxs-lookup"><span data-stu-id="b3319-131">Top: 16px</span></span>
* <span data-ttu-id="b3319-132">Inferior: 0px</span><span class="sxs-lookup"><span data-stu-id="b3319-132">Bottom: 0px</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="b3319-133">Todas las pestañas tienen sus márgenes quitados: pestañas personales, pestañas de chat (grupo), pestañas de reunión y pestañas de canal.</span><span class="sxs-lookup"><span data-stu-id="b3319-133">All tabs have their margins removed: personal tabs, (group) chat tabs, meeting tabs, and channel tabs.</span></span>
> * <span data-ttu-id="b3319-134">No hay forma de participar o no participar en este cambio.</span><span class="sxs-lookup"><span data-stu-id="b3319-134">There is no way to opt-in or opt-out of this change.</span></span> <span data-ttu-id="b3319-135">Se aplicará a todas las pestañas.</span><span class="sxs-lookup"><span data-stu-id="b3319-135">It will apply to all tabs.</span></span>
> * <span data-ttu-id="b3319-136">Este cambio puede afectar a las pestañas que dependen de Microsoft Teams para proporcionar márgenes que rodean su interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="b3319-136">This change can affect tabs that rely on Microsoft Teams to provide margins surrounding their UI.</span></span>

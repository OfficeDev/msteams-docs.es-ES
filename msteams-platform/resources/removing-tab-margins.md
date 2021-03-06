---
title: Quitar márgenes de tabulación en Microsoft Teams
author: laujan
description: Describe cómo la eliminación de márgenes de tabulación mejorará la experiencia del desarrollador.
keywords: tab removing margins padding
ms.topic: reference
ms.author: lomeybur
ms.openlocfilehash: 87766a40730fdaa2da80c2e0031eab655a993c33
ms.sourcegitcommit: 9cfbc44912980a33d2d7c7c85739aeea6ccb41de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2021
ms.locfileid: "50479964"
---
# <a name="tab-margin-changes"></a><span data-ttu-id="f352f-104">Cambios del margen de pestaña</span><span class="sxs-lookup"><span data-stu-id="f352f-104">Tab margin changes</span></span>

<span data-ttu-id="f352f-105">En este documento se describe cómo la eliminación de márgenes alrededor de todas las pestañas de Microsoft Teams mejorará la experiencia del desarrollador al crear aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f352f-105">This document describes how the removal of margins around all tabs in Microsoft Teams will enhance the developer's experience when building apps.</span></span> <span data-ttu-id="f352f-106">Esta es una mejora introducida en Microsoft Teams en 2021.</span><span class="sxs-lookup"><span data-stu-id="f352f-106">This is an enhancement introduced in Microsoft Teams in 2021.</span></span>
<span data-ttu-id="f352f-107">La eliminación de los márgenes alrededor de todas las pestañas permitirá a los desarrolladores crear aplicaciones que parezcan más nativas de Teams.</span><span class="sxs-lookup"><span data-stu-id="f352f-107">Removing the margins around all tabs will allow developers to build apps that look more native to Teams.</span></span> <span data-ttu-id="f352f-108">Esto también se alineará con nuestros diseños [de kit de interfaz de usuario.](~/tabs/design/tabs.md)</span><span class="sxs-lookup"><span data-stu-id="f352f-108">This will also align with our [UI kit designs](~/tabs/design/tabs.md).</span></span> <span data-ttu-id="f352f-109">La mayoría de las aplicaciones ya se ven mejor sin los márgenes que rodean sus experiencias.</span><span class="sxs-lookup"><span data-stu-id="f352f-109">Most apps already look better without the margins surrounding their experiences.</span></span> <span data-ttu-id="f352f-110">Sin embargo, algunas pestañas se ven afectadas visualmente por este cambio y los desarrolladores deben realizar los cambios necesarios.</span><span class="sxs-lookup"><span data-stu-id="f352f-110">However, some tabs are visually affected by this change, and developers must make the necessary changes.</span></span>

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="Inteligencia de tabulación y sin márgenes" border="false":::

## <a name="timelines"></a><span data-ttu-id="f352f-112">Escalas de tiempo</span><span class="sxs-lookup"><span data-stu-id="f352f-112">Timelines</span></span>

* <span data-ttu-id="f352f-113">5 de marzo de 2021: Márgenes eliminados en [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="f352f-113">March 5, 2021 - Margins removed in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
* <span data-ttu-id="f352f-114">1 de mayo de 2021: los márgenes se quitarán en producción.</span><span class="sxs-lookup"><span data-stu-id="f352f-114">May 1, 2021 - Margins will be removed in production.</span></span>

## <a name="guidelines"></a><span data-ttu-id="f352f-115">Instrucciones</span><span class="sxs-lookup"><span data-stu-id="f352f-115">Guidelines</span></span>

<span data-ttu-id="f352f-116">Las aplicaciones de Microsoft Teams que usan pestañas se verán afectadas por este cambio.</span><span class="sxs-lookup"><span data-stu-id="f352f-116">Microsoft Teams apps that use tabs will be affected by this change.</span></span> <span data-ttu-id="f352f-117">Los desarrolladores deben cambiar [a Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) para determinar cómo se ven afectadas sus pestañas y realizar los cambios necesarios.</span><span class="sxs-lookup"><span data-stu-id="f352f-117">Developers should switch to [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) in order to determine how their tabs are affected and make the necessary changes.</span></span>

<span data-ttu-id="f352f-118">Los desarrolladores de pestañas no deben depender de Teams para proporcionar márgenes alrededor de sus pestañas.</span><span class="sxs-lookup"><span data-stu-id="f352f-118">Tab developers must not rely on Teams to provide margins surrounding their tabs.</span></span> <span data-ttu-id="f352f-119">Se recomienda a los desarrolladores que agreguen márgenes alrededor de sus diseños de pestañas cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f352f-119">Developers are encouraged to add margins around their tab designs where it is required.</span></span> <span data-ttu-id="f352f-120">Los diseños de aplicaciones en producción pueden parecer que hay un relleno adicional, es decir, los márgenes proporcionados por Teams y los márgenes proporcionados por la pestaña. Sin embargo, el relleno adicional es solo temporal y desaparecerá en unas semanas, dejando solo el relleno proporcionado por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f352f-120">App designs in production can look like there is extra padding, that is, margins provided by Teams and margins provided by the tab. However, the extra padding is only temporary and will go away in a few weeks, leaving only the app's provided padding.</span></span>

## <a name="faq"></a><span data-ttu-id="f352f-121">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="f352f-121">FAQ</span></span>

<span data-ttu-id="f352f-122">**¿Está bien que chrome de la aplicación, como la barra de encabezado o la barra de tareas, toque los bordes de nuestros diseños?**</span><span class="sxs-lookup"><span data-stu-id="f352f-122">**Is it OK for app chrome, such as header bar or taskbar, to touch the edges of our designs?**</span></span>

<span data-ttu-id="f352f-123">Sí, esto está bien y se recomienda.</span><span class="sxs-lookup"><span data-stu-id="f352f-123">Yes, this is fine and encouraged.</span></span> <span data-ttu-id="f352f-124">Esto ayuda a que la aplicación se sienta nativa.</span><span class="sxs-lookup"><span data-stu-id="f352f-124">This helps the app feel native.</span></span>

<span data-ttu-id="f352f-125">**¿Está bien que el contenido de la aplicación, como texto, logotipos e imágenes, toque los bordes izquierdo y derecho de nuestros diseños?**</span><span class="sxs-lookup"><span data-stu-id="f352f-125">**Is it OK for app content, such as text, logos, and images, to touch the left and right edges of our designs?**</span></span>

<span data-ttu-id="f352f-126">No, debes proporcionar tu propio relleno o márgenes a la izquierda y a la derecha de todo el contenido de la aplicación para asegurarte de que no toque los bordes de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="f352f-126">No, you must provide your own padding or margins to the left and right of all app content to ensure it does not touch the edges of your UI.</span></span> <span data-ttu-id="f352f-127">También puede agregar márgenes en la parte superior de la pestaña, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="f352f-127">You can also add margins at the top of your tab, if required.</span></span>

<span data-ttu-id="f352f-128">**¿Cuál es el tamaño de los márgenes aplicados anteriormente por Teams?**</span><span class="sxs-lookup"><span data-stu-id="f352f-128">**What's the size of the margins Teams previously applied?**</span></span>

* <span data-ttu-id="f352f-129">Izquierda y derecha: 20 píxeles</span><span class="sxs-lookup"><span data-stu-id="f352f-129">Left and right: 20px</span></span>
* <span data-ttu-id="f352f-130">Top: 16px</span><span class="sxs-lookup"><span data-stu-id="f352f-130">Top: 16px</span></span>
* <span data-ttu-id="f352f-131">Inferior: 0px</span><span class="sxs-lookup"><span data-stu-id="f352f-131">Bottom: 0px</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="f352f-132">Todas las pestañas tienen sus márgenes quitados: pestañas personales, pestañas de chat (grupo), pestañas de reunión y pestañas de canal.</span><span class="sxs-lookup"><span data-stu-id="f352f-132">All tabs have their margins removed: personal tabs, (group) chat tabs, meeting tabs, and channel tabs.</span></span>
> * <span data-ttu-id="f352f-133">No hay forma de participar o no participar en este cambio.</span><span class="sxs-lookup"><span data-stu-id="f352f-133">There is no way to opt-in or opt-out of this change.</span></span> <span data-ttu-id="f352f-134">Se aplicará a todas las pestañas.</span><span class="sxs-lookup"><span data-stu-id="f352f-134">It will apply to all tabs.</span></span>
> * <span data-ttu-id="f352f-135">Este cambio puede afectar a las pestañas que dependen de Microsoft Teams para proporcionar márgenes que rodean su interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="f352f-135">This change can affect tabs that rely on Microsoft Teams to provide margins surrounding their UI.</span></span>

---
title: Referencia de directrices de diseño
description: Describe las directrices para usar el color en las aplicaciones
keywords: Directrices de diseño de Microsoft Teams color de componentes de referencia
ms.openlocfilehash: dab223891e88615b52386d3692d4a98607d6d449
ms.sourcegitcommit: aca9990e1f84b07b9e77c08bfeca4440eb4e64f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/25/2020
ms.locfileid: "49409067"
---
# <a name="color"></a><span data-ttu-id="b0eae-104">Color</span><span class="sxs-lookup"><span data-stu-id="b0eae-104">Color</span></span>

<span data-ttu-id="b0eae-105">El uso de nuestra paleta neutra aprobada para fondos, notificaciones, texto y botones ayudará a que la aplicación se sienta más en casa en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="b0eae-105">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="b0eae-106">Como los equipos tienen dos temas de color (claros y oscuros), es una buena idea asegurarse de que la aplicación tenga un aspecto excelente en ambos temas.</span><span class="sxs-lookup"><span data-stu-id="b0eae-106">Since Teams has two color themes (light and dark), it’s a good idea to make sure your app looks great in both themes.</span></span>

### <a name="app-black-252423"></a><span data-ttu-id="b0eae-107">$app-negro (#252423)</span><span class="sxs-lookup"><span data-stu-id="b0eae-107">$app-black (#252423)</span></span>

<span data-ttu-id="b0eae-108">El color de texto que se usa con más frecuencia.</span><span class="sxs-lookup"><span data-stu-id="b0eae-108">Our most commonly-used text color.</span></span> <span data-ttu-id="b0eae-109">Se usa en cinco niveles de opacidad para el texto.</span><span class="sxs-lookup"><span data-stu-id="b0eae-109">We use it at five levels of opacity for text.</span></span> <span data-ttu-id="b0eae-110">El texto se debe usar principalmente al 100%, 74%, 64% de opacidad porque es accesible.</span><span class="sxs-lookup"><span data-stu-id="b0eae-110">Text should mainly be used at 100%, 74%, 64% opacity since it is accessible.</span></span> <span data-ttu-id="b0eae-111">El texto del 52% y el 36% deben usarse con moderación, ya que no es accesible.</span><span class="sxs-lookup"><span data-stu-id="b0eae-111">Text at 52% and 36% should be used sparingly since it is not accessible.</span></span>

[!include[Appblack color and text](~/includes/design/color-image-appblack-text.html)]

1. <span data-ttu-id="b0eae-112">100%: encabezados y texto base</span><span class="sxs-lookup"><span data-stu-id="b0eae-112">100% - Headers and base text</span></span>
2. <span data-ttu-id="b0eae-113">74%: etiquetas, subencabezados, atribuciones y botones de icono</span><span class="sxs-lookup"><span data-stu-id="b0eae-113">74% - Labels, subheads, attributions, and icon buttons</span></span>
3. <span data-ttu-id="b0eae-114">64%: vistas previas de mensajes, texto de ayuda (no se muestra)</span><span class="sxs-lookup"><span data-stu-id="b0eae-114">64% - Message previews, help text (not shown)</span></span>
4. <span data-ttu-id="b0eae-115">52%: marcas de tiempo</span><span class="sxs-lookup"><span data-stu-id="b0eae-115">52% - Timestamps</span></span>
5. <span data-ttu-id="b0eae-116">36%: texto deshabilitado</span><span class="sxs-lookup"><span data-stu-id="b0eae-116">36% - Disabled text</span></span>

<span data-ttu-id="b0eae-117">También usamos `$app-black` en otras opacities para algunos elementos de la interfaz de usuario:</span><span class="sxs-lookup"><span data-stu-id="b0eae-117">We also use `$app-black` at other opacities for some UI elements:</span></span>

[!include[Appblack color and text](~/includes/design/color-image-appblack-ui.html)]

1. <span data-ttu-id="b0eae-118">14%: fondos de banner</span><span class="sxs-lookup"><span data-stu-id="b0eae-118">14% - Banner backgrounds</span></span>
2. <span data-ttu-id="b0eae-119">5%-deshabilitado y bordes de tarjeta</span><span class="sxs-lookup"><span data-stu-id="b0eae-119">5% - Disabled button and card borders</span></span>

### <a name="default-theme-color-ramp"></a><span data-ttu-id="b0eae-120">Rampa de colores del tema predeterminado</span><span class="sxs-lookup"><span data-stu-id="b0eae-120">Default theme color ramp</span></span>

<span data-ttu-id="b0eae-121">Vea las [guías de diseño de Microsoft Teams-rampa de colores del tema predeterminado](https://codepen.io/msteams/pen/KyPmqL/) en CodePen.</span><span class="sxs-lookup"><span data-stu-id="b0eae-121">See the Pen [Microsoft Teams design guidelines - default theme color ramp](https://codepen.io/msteams/pen/KyPmqL/) on CodePen.</span></span>

<iframe height='620' scrolling='no' title='<span data-ttu-id="b0eae-122">Instrucciones de diseño de Microsoft Teams: rampa de colores del tema predeterminado</span><span class="sxs-lookup"><span data-stu-id="b0eae-122">Microsoft Teams design guidelines - default theme color ramp</span></span>' src='//codepen.io/msteams/embed/KyPmqL/?height=682&theme-id=31655&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="b0eae-123">Consulte las <a href='https://codepen.io/msteams/pen/KyPmqL/'>guías de diseño de Microsoft Teams-gradación de colores del tema predeterminado</a> de Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) en <a href='https://codepen.io'>CodePen</a>.</span><span class="sxs-lookup"><span data-stu-id="b0eae-123">See the Pen <a href='https://codepen.io/msteams/pen/KyPmqL/'>Microsoft Teams design guidelines - default theme color ramp</a> by Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

### <a name="other-default-theme-colors"></a><span data-ttu-id="b0eae-124">Otros colores del tema predeterminados</span><span class="sxs-lookup"><span data-stu-id="b0eae-124">Other default theme colors</span></span>

<span data-ttu-id="b0eae-125">Vea las [guías de diseño de Microsoft Teams, otros colores predeterminados del tema](https://codepen.io/msteams/pen/zPOdYJ/) en CodePen.</span><span class="sxs-lookup"><span data-stu-id="b0eae-125">See the Pen [Microsoft Teams design guidelines - other default theme colors](https://codepen.io/msteams/pen/zPOdYJ/) on CodePen.</span></span>

<iframe height='392' scrolling='no' title='<span data-ttu-id="b0eae-126">Directrices de diseño de Microsoft Teams: otros colores predeterminados del tema</span><span class="sxs-lookup"><span data-stu-id="b0eae-126">Microsoft Teams design guidelines - other default theme colors</span></span>' src='//codepen.io/msteams/embed/zPOdYJ/?height=442&theme-id=31655&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="b0eae-127">Vea las <a href='https://codepen.io/msteams/pen/zPOdYJ/'>guías de diseño de Microsoft Teams-otros colores predeterminados del tema</a> de Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) en <a href='https://codepen.io'>CodePen</a>.</span><span class="sxs-lookup"><span data-stu-id="b0eae-127">See the Pen <a href='https://codepen.io/msteams/pen/zPOdYJ/'>Microsoft Teams design guidelines - other default theme colors</a> by Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

### <a name="dark-theme-color-ramp"></a><span data-ttu-id="b0eae-128">Rampa de colores del tema oscuro</span><span class="sxs-lookup"><span data-stu-id="b0eae-128">Dark theme color ramp</span></span>

<span data-ttu-id="b0eae-129">Vea las [guías de diseño de Microsoft Teams: rampa de colores del tema oscuro](https://codepen.io/msteams/pen/BmBwjx/) en CodePen.</span><span class="sxs-lookup"><span data-stu-id="b0eae-129">See the Pen [Microsoft Teams design guidelines - dark theme color ramp](https://codepen.io/msteams/pen/BmBwjx/) on CodePen.</span></span>

<iframe height='798' scrolling='no' title='<span data-ttu-id="b0eae-130">Directrices de diseño de Microsoft Teams: rampa de colores del tema oscuro</span><span class="sxs-lookup"><span data-stu-id="b0eae-130">Microsoft Teams design guidelines - dark theme color ramp</span></span>' src='//codepen.io/msteams/embed/BmBwjx/?height=846&theme-id=31655&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="b0eae-131">Vea las <a href='https://codepen.io/msteams/pen/BmBwjx/'>guías de diseño de Microsoft Teams: rampa de colores del tema oscuro</a> de Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) en <a href='https://codepen.io'>CodePen</a>.</span><span class="sxs-lookup"><span data-stu-id="b0eae-131">See the Pen <a href='https://codepen.io/msteams/pen/BmBwjx/'>Microsoft Teams design guidelines - dark theme color ramp</a> by Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

> <span data-ttu-id="b0eae-132">**Nota:** La biblioteca msteams-UI-Styles-Core tiene los valores reales codificados como variables.</span><span class="sxs-lookup"><span data-stu-id="b0eae-132">**Note:** The msteams-ui-styles-core library has the actual values coded as variables.</span></span> <span data-ttu-id="b0eae-133">Estas variables serán útiles si los colores se actualizan en algún momento.</span><span class="sxs-lookup"><span data-stu-id="b0eae-133">These variables will be helpful if the colors are ever updated.</span></span>


### <a name="other-dark-theme-colors"></a><span data-ttu-id="b0eae-134">Otros colores del tema oscuro</span><span class="sxs-lookup"><span data-stu-id="b0eae-134">Other dark theme colors</span></span>

<span data-ttu-id="b0eae-135">Vea las [guías de diseño de Microsoft Teams con lápiz, otros colores de temas oscuros](https://codepen.io/msteams/pen/zPOEXN/) en CodePen.</span><span class="sxs-lookup"><span data-stu-id="b0eae-135">See the Pen [Microsoft Teams design guidelines - other dark theme colors](https://codepen.io/msteams/pen/zPOEXN/) on CodePen.</span></span>

<iframe height='390' scrolling='no' title='<span data-ttu-id="b0eae-136">Directrices de diseño de Microsoft Teams: otros colores del tema oscuro</span><span class="sxs-lookup"><span data-stu-id="b0eae-136">Microsoft Teams design guidelines - other dark theme colors</span></span>' src='//codepen.io/msteams/embed/zPOEXN/?height=442&theme-id=31655&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="b0eae-137">Consulte las <a href='https://codepen.io/msteams/pen/zPOEXN/'>guías de diseño de Microsoft Teams para Pen-otros colores oscuros del tema</a> de Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) en <a href='https://codepen.io'>CodePen</a>.</span><span class="sxs-lookup"><span data-stu-id="b0eae-137">See the Pen <a href='https://codepen.io/msteams/pen/zPOEXN/'>Microsoft Teams design guidelines - other dark theme colors</a> by Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

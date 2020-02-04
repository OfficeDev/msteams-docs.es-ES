---
title: Referencia de directrices de diseño
description: Describe las instrucciones para usar los campos y los controles flotantes en las aplicaciones.
keywords: Directrices de diseño de Microsoft Teams campos de referencia de componentes y controles flotantes
ms.openlocfilehash: 0f62d38bf961ae79b05c599638cefb3c76f46ed4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676140"
---
# <a name="fields-and-flyouts"></a><span data-ttu-id="62d51-104">Campos y controles flotantes</span><span class="sxs-lookup"><span data-stu-id="62d51-104">Fields and flyouts</span></span>

---

## <a name="fields"></a><span data-ttu-id="62d51-105">Fields</span><span class="sxs-lookup"><span data-stu-id="62d51-105">Fields</span></span>

<span data-ttu-id="62d51-106">Los campos son áreas en las que los usuarios pueden escribir texto.</span><span class="sxs-lookup"><span data-stu-id="62d51-106">Fields are areas where users can input text.</span></span>

### <a name="padding-and-size"></a><span data-ttu-id="62d51-107">Relleno y tamaño</span><span class="sxs-lookup"><span data-stu-id="62d51-107">Padding and size</span></span>

<span data-ttu-id="62d51-108">Los campos de texto de una línea son un alto fijo de 32 que coinciden con el alto de otros componentes.</span><span class="sxs-lookup"><span data-stu-id="62d51-108">Single-line text fields are a fixed height of 32px to match the height of other components.</span></span> <span data-ttu-id="62d51-109">Algunos campos de texto, como los campos Description, pueden ser más altos verticalmente para permitir más texto.</span><span class="sxs-lookup"><span data-stu-id="62d51-109">Some text fields such as description fields may be taller vertically to allow more text.</span></span>
[!include[Padding and size](~/includes/design/fields-image-padding.html)]

### <a name="states"></a><span data-ttu-id="62d51-110">Miembros</span><span class="sxs-lookup"><span data-stu-id="62d51-110">States</span></span>

<span data-ttu-id="62d51-111">Estos son los Estados de los campos de texto.</span><span class="sxs-lookup"><span data-stu-id="62d51-111">These are the states of our text fields.</span></span> <span data-ttu-id="62d51-112">Los campos de texto existen en distintos Estados.</span><span class="sxs-lookup"><span data-stu-id="62d51-112">Text fields exist in different states.</span></span> <span data-ttu-id="62d51-113">Tenemos diseños específicos dedicados a nueve escenarios posibles, entre los que se incluyen (de arriba a abajo): campo de texto, teclado en el foco y cursor dentro del campo, teclado en foco con el texto escrito, el tratamiento de errores se ha realizado correctamente; error en el control de errores, texto no cifrado campo (incluido un icono X), campo de búsqueda (incluido un icono de búsqueda), campo de carga y un campo deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="62d51-113">We have specific designs dedicated to nine possible scenarios, including (top to bottom): Resting text field, Keyboard in focus and cursor inside the field, Keyboard in focus with text entered, Error handling has succeeded, Error handling has failed, Clear text field (including an X icon), Search field (including a Search icon), Loading field, and a Disabled field.</span></span>
[!include[Field states](~/includes/design/fields-image-states.html)]

### <a name="formatting-help-text-and-labels"></a><span data-ttu-id="62d51-114">Dar formato al texto y las etiquetas de ayuda</span><span class="sxs-lookup"><span data-stu-id="62d51-114">Formatting help text and labels</span></span>

<span data-ttu-id="62d51-115">Los campos pueden contener texto de marcador de posición para proporcionar un ejemplo del tipo de información necesaria.</span><span class="sxs-lookup"><span data-stu-id="62d51-115">Fields can contain placeholder text to give an example of the kind of information that is required.</span></span> <span data-ttu-id="62d51-116">También pueden contener etiquetas que proporcionen al usuario más contexto.</span><span class="sxs-lookup"><span data-stu-id="62d51-116">They can also hold labels that give the user more context.</span></span> <span data-ttu-id="62d51-117">Dentro de un campo, el texto siempre debe justificarse a la izquierda.</span><span class="sxs-lookup"><span data-stu-id="62d51-117">Within a field, your text should always be justified left.</span></span> <span data-ttu-id="62d51-118">También se utiliza la grafía de oraciones en este caso.</span><span class="sxs-lookup"><span data-stu-id="62d51-118">We use sentence casing throughout here, as well.</span></span>

<span data-ttu-id="62d51-119">Usamos la interfaz de usuario de Segoe regular en 12 PTO (Caption) y $app-Gray-02 para las etiquetas.</span><span class="sxs-lookup"><span data-stu-id="62d51-119">We use Segoe UI Regular at 12 pt (caption) and $app-gray-02 for labels.</span></span> <span data-ttu-id="62d51-120">Para el texto de ayuda, usamos Segoe UI regular en 14 PT (base) y $app-Gray-02.</span><span class="sxs-lookup"><span data-stu-id="62d51-120">For help text, we use Segoe UI Regular at 14 pt (base) and $app-gray-02.</span></span>
[!include[Fields typography](~/includes/design/fields-image-typography.html)]

---

## <a name="flyouts"></a><span data-ttu-id="62d51-121">Flota</span><span class="sxs-lookup"><span data-stu-id="62d51-121">Flyouts</span></span>

<span data-ttu-id="62d51-122">Los controles flotantes son más sencillos que los cuadros de diálogo y se pueden desechar rápidamente.</span><span class="sxs-lookup"><span data-stu-id="62d51-122">Flyouts are more lightweight than dialogs and can be dismissed quickly.</span></span> <span data-ttu-id="62d51-123">Pueden contener botones, campos y otros componentes.</span><span class="sxs-lookup"><span data-stu-id="62d51-123">They can contain buttons, fields, and other components.</span></span>
[!include[Flyouts](~/includes/design/flyouts-image.html)]

### <a name="sizing-and-padding"></a><span data-ttu-id="62d51-124">Tamaño y relleno</span><span class="sxs-lookup"><span data-stu-id="62d51-124">Sizing and padding</span></span>

<span data-ttu-id="62d51-125">Se recomienda un relleno de 16px a la izquierda y derecha del contenido.</span><span class="sxs-lookup"><span data-stu-id="62d51-125">We recommend a 16px padding to the left and right of the content.</span></span>
[!include[Flyouts size and padding](~/includes/design/flyouts-image-sizepadding.html)]

### <a name="placement"></a><span data-ttu-id="62d51-126">Placement</span><span class="sxs-lookup"><span data-stu-id="62d51-126">Placement</span></span>

<span data-ttu-id="62d51-127">Los controles flotantes son contextuales y deben colocarse por encima, por debajo o junto al elemento que lo ha desactivado.</span><span class="sxs-lookup"><span data-stu-id="62d51-127">Flyouts are contextual and should be placed above, below, or beside the element that triggered it.</span></span>

### <a name="scrolling"></a><span data-ttu-id="62d51-128">Desplazamiento</span><span class="sxs-lookup"><span data-stu-id="62d51-128">Scrolling</span></span>

<span data-ttu-id="62d51-129">El encabezado permanece en su ubicación para dar contexto al contenido que se va a desplazar.</span><span class="sxs-lookup"><span data-stu-id="62d51-129">The header remains in place to give context to the content being scrolled.</span></span>
[!include[Flyouts scrolling](~/includes/design/flyouts-image-scrolling.html)]

## <a name="mobile"></a><span data-ttu-id="62d51-130">Mobile</span><span class="sxs-lookup"><span data-stu-id="62d51-130">Mobile</span></span>

<span data-ttu-id="62d51-131">Los campos son cuadros de entrada de texto que aceptan la entrada de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="62d51-131">Fields are text-entry boxes that accept input from users.</span></span> <span data-ttu-id="62d51-132">Los menús desplegables son ventanas emergentes horizontales que aparecen en el panel superior y se pueden usar para mostrar más detalles sobre un elemento.</span><span class="sxs-lookup"><span data-stu-id="62d51-132">Flyout menus are horizontal pop-up windows that appear from the top pane and can be used to show more detail about an item.</span></span>

### <a name="field-controls"></a><span data-ttu-id="62d51-133">Controles de campo</span><span class="sxs-lookup"><span data-stu-id="62d51-133">Field Controls</span></span>

[!include[Mobile fields](~/includes/design/fields-mobile-image.html)]

### <a name="flyout-menu-list-controls"></a><span data-ttu-id="62d51-134">Controles de lista de menús desplegables</span><span class="sxs-lookup"><span data-stu-id="62d51-134">Flyout menu list controls</span></span>

[!include[Mobile flyout menu controls](~/includes/design/flyout-menu-mobile-image.html)]

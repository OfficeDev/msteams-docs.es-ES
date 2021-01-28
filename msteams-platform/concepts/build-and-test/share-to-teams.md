---
title: Crear un botón de Compartir en Teams
description: Cómo agregar el botón Compartir a Teams insertado en su sitio web
ms.topic: reference
keywords: Compartir teams de forma share-to-teams
ms.openlocfilehash: 46091c957137cc871095ca6a57c0d61fa79d9458
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014337"
---
# <a name="create-a-share-to-teams-button-for-your-website"></a><span data-ttu-id="d6dca-104">Creación de un botón Compartir en Teams para el sitio web</span><span class="sxs-lookup"><span data-stu-id="d6dca-104">Create a Share-to-Teams button for your website</span></span>

>[!NOTE]
> * <span data-ttu-id="d6dca-105">Solo se admiten las versiones de escritorio de Edge y Chrome.</span><span class="sxs-lookup"><span data-stu-id="d6dca-105">Only the desktop versions of Edge and Chrome are supported.</span></span>
> * <span data-ttu-id="d6dca-106">No se admite el uso de cuentas de invitado o freemium.</span><span class="sxs-lookup"><span data-stu-id="d6dca-106">Use of Freemium or guest accounts is not supported.</span></span>

<span data-ttu-id="d6dca-107">Los sitios web de terceros pueden usar el script del iniciador para insertar botones Compartir en Teams en sus páginas web, lo que iniciará la experiencia Compartir en Teams en una ventana emergente cuando se haga clic en ellos.</span><span class="sxs-lookup"><span data-stu-id="d6dca-107">Third-party websites can use the launcher script to embed Share to Teams buttons on their webpages which will launch the Share to Teams experience in a popup window when clicked.</span></span> <span data-ttu-id="d6dca-108">Esto le permitirá compartir un vínculo directamente con cualquier persona o canal de Microsoft Teams sin cambiar de contexto.</span><span class="sxs-lookup"><span data-stu-id="d6dca-108">This will allow you to share a link directly to any person or Microsoft Teams channel without switching context.</span></span>

![Compartir en un elemento emergente de Teams](~/assets/images/share-to-teams-popup.png)

## <a name="how-to-embed-a-share-to-teams-button"></a><span data-ttu-id="d6dca-110">Cómo insertar un botón Compartir en Teams</span><span class="sxs-lookup"><span data-stu-id="d6dca-110">How to embed a Share to Teams button</span></span>

<span data-ttu-id="d6dca-111">En primer lugar, tendrá que agregar el `launcher.js` script en su página web.</span><span class="sxs-lookup"><span data-stu-id="d6dca-111">First, you'll need to add the `launcher.js` script on your webpage.</span></span>

```html
<script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
```

<span data-ttu-id="d6dca-112">A continuación, agregue un elemento HTML en la página web con el atributo `teams-share-button` de clase y el vínculo para compartir en el `data-href` atributo.</span><span class="sxs-lookup"><span data-stu-id="d6dca-112">Next, add an HTML element on your webpage with the `teams-share-button` class attribute and the link to share in the `data-href` attribute.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>">
</div>
```

<span data-ttu-id="d6dca-113">Esto agregará el icono de Microsoft Teams a su sitio web.</span><span class="sxs-lookup"><span data-stu-id="d6dca-113">This will add the Microsoft Teams icon to your website.</span></span>

![Icono Compartir en Teams](~/assets/icons/share-to-teams-icon.png)

<span data-ttu-id="d6dca-115">Opcionalmente, si desea un tamaño de icono diferente para el botón Compartir en Teams, use el `data-icon-px-size` atributo.</span><span class="sxs-lookup"><span data-stu-id="d6dca-115">Optionally, if you want a different icon size for the Share to Teams button, use the `data-icon-px-size` attribute.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-icon-px-size="64">
</div>
```

<span data-ttu-id="d6dca-116">Si sabe que la vista previa de la dirección URL del vínculo que se va a compartir no se representará bien en Teams (por ejemplo, el vínculo requeriría autenticación de usuario), puede deshabilitar la vista previa de la dirección URL agregando el conjunto de atributos a `data-preview` `false` .</span><span class="sxs-lookup"><span data-stu-id="d6dca-116">If you know that the URL preview from your link to be shared won't render well in Teams (for example the link would require user authentication) you can disable the URL preview by adding the `data-preview` attribute set to `false`.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-preview="false">
</div>
```

<span data-ttu-id="d6dca-117">Si la página representa contenido dinámicamente, puede usar el método para forzar que el botón Compartir se represente en el `shareToMicrosoftTeams.renderButtons()` lugar adecuado de la canalización. </span><span class="sxs-lookup"><span data-stu-id="d6dca-117">If your page dynamically renders content, you can use the the `shareToMicrosoftTeams.renderButtons()` method to force the **Share** button to render at the appropriate place in the pipeline.</span></span>

## <a name="crafting-your-website-preview"></a><span data-ttu-id="d6dca-118">Creación de la vista previa del sitio web</span><span class="sxs-lookup"><span data-stu-id="d6dca-118">Crafting your website preview</span></span>

<span data-ttu-id="d6dca-119">Cuando su sitio web se comparte con Teams, la tarjeta que se inserta en el canal seleccionado contendrá una vista previa de su sitio web.</span><span class="sxs-lookup"><span data-stu-id="d6dca-119">When your website is shared to Teams, the card that is inserted into the selected channel will contain a preview of your website.</span></span> <span data-ttu-id="d6dca-120">Puede controlar el comportamiento de esta vista previa asegurándose de que los metadatos adecuados se agregan al sitio web que se comparte (la `data-href` dirección URL).</span><span class="sxs-lookup"><span data-stu-id="d6dca-120">You can control the behavior of this preview by ensuring the appropriate meta-data is added to the website being shared (the `data-href` URL).</span></span> <span data-ttu-id="d6dca-121">En la tabla siguiente se describen las etiquetas necesarias.</span><span class="sxs-lookup"><span data-stu-id="d6dca-121">The table below outlines the necessary tags.</span></span> <span data-ttu-id="d6dca-122">Puede usar las versiones predeterminadas html o la versión de Open Graph.</span><span class="sxs-lookup"><span data-stu-id="d6dca-122">You can use either the html default versions, or the Open Graph version.</span></span>

<span data-ttu-id="d6dca-123">Para que se muestre la vista previa, debe:</span><span class="sxs-lookup"><span data-stu-id="d6dca-123">In order for the preview to be displayed you must:</span></span>

* <span data-ttu-id="d6dca-124">Incluya una imagen en miniatura o un título y una descripción (para obtener los mejores resultados, incluya los tres).</span><span class="sxs-lookup"><span data-stu-id="d6dca-124">Include either a Thumbnail image, or both a Title and Description (for best results, include all three).</span></span>
* <span data-ttu-id="d6dca-125">La dirección URL que se comparte no puede requerir autenticación.</span><span class="sxs-lookup"><span data-stu-id="d6dca-125">The URL being shared cannot require authentication.</span></span> <span data-ttu-id="d6dca-126">Si lo hace, puede seguir compartiéndola, pero no se creará la vista previa.</span><span class="sxs-lookup"><span data-stu-id="d6dca-126">If it does you can still share it, but the preview will not be created.</span></span>

|<span data-ttu-id="d6dca-127">Valor</span><span class="sxs-lookup"><span data-stu-id="d6dca-127">Value</span></span>|<span data-ttu-id="d6dca-128">Etiqueta meta</span><span class="sxs-lookup"><span data-stu-id="d6dca-128">Meta tag</span></span>| <span data-ttu-id="d6dca-129">Open Graph</span><span class="sxs-lookup"><span data-stu-id="d6dca-129">Open Graph</span></span>|
|----|----|----|
|<span data-ttu-id="d6dca-130">El título</span><span class="sxs-lookup"><span data-stu-id="d6dca-130">Title</span></span>|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|<span data-ttu-id="d6dca-131">Descripción</span><span class="sxs-lookup"><span data-stu-id="d6dca-131">Description</span></span>|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|<span data-ttu-id="d6dca-132">Imagen en miniatura</span><span class="sxs-lookup"><span data-stu-id="d6dca-132">Thumbnail Image</span></span>| <span data-ttu-id="d6dca-133">none</span><span class="sxs-lookup"><span data-stu-id="d6dca-133">none</span></span> |`<meta property="og:image" content="http://example.com/image.jpg">`|

## <a name="share-to-teams-for-education"></a><span data-ttu-id="d6dca-134">Compartir con Teams para educación</span><span class="sxs-lookup"><span data-stu-id="d6dca-134">Share to Teams for Education</span></span>

<span data-ttu-id="d6dca-135">Para los profesores que usan el botón Compartir en Teams, se le dará una opción adicional para `Create an Assignment` .</span><span class="sxs-lookup"><span data-stu-id="d6dca-135">For teachers using the Share to Teams button you'll be given an additional option to `Create an Assignment`.</span></span> <span data-ttu-id="d6dca-136">Esto le permite crear rápidamente una asignación en el equipo elegido en función del vínculo compartido.</span><span class="sxs-lookup"><span data-stu-id="d6dca-136">This enables you to quickly create an assignment in the chosen Team based on the shared link.</span></span>

![Compartir en un elemento emergente de Teams](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a><span data-ttu-id="d6dca-138">Definición launcher.js completa</span><span class="sxs-lookup"><span data-stu-id="d6dca-138">Full launcher.js definition</span></span>

| <span data-ttu-id="d6dca-139">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d6dca-139">Property</span></span> | <span data-ttu-id="d6dca-140">Atributo HTML</span><span class="sxs-lookup"><span data-stu-id="d6dca-140">HTML attribute</span></span> | <span data-ttu-id="d6dca-141">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6dca-141">Type</span></span> | <span data-ttu-id="d6dca-142">Predeterminado</span><span class="sxs-lookup"><span data-stu-id="d6dca-142">Default</span></span> | <span data-ttu-id="d6dca-143">Descripción</span><span class="sxs-lookup"><span data-stu-id="d6dca-143">Description</span></span> |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| <span data-ttu-id="d6dca-144">href</span><span class="sxs-lookup"><span data-stu-id="d6dca-144">href</span></span> | `data-href` | <span data-ttu-id="d6dca-145">cadena</span><span class="sxs-lookup"><span data-stu-id="d6dca-145">string</span></span> | <span data-ttu-id="d6dca-146">No aplicable</span><span class="sxs-lookup"><span data-stu-id="d6dca-146">n/a</span></span> | <span data-ttu-id="d6dca-147">El href del contenido que se desea compartir.</span><span class="sxs-lookup"><span data-stu-id="d6dca-147">The href of the content to share.</span></span> |
| <span data-ttu-id="d6dca-148">preview</span><span class="sxs-lookup"><span data-stu-id="d6dca-148">preview</span></span> | `data-preview` | <span data-ttu-id="d6dca-149">boolean (como una cadena)</span><span class="sxs-lookup"><span data-stu-id="d6dca-149">boolean (as a string)</span></span> | `true` | <span data-ttu-id="d6dca-150">Indica si se va a mostrar una vista previa del contenido que se va a compartir.</span><span class="sxs-lookup"><span data-stu-id="d6dca-150">Whether or not to show a preview of the content to share.</span></span> |
| <span data-ttu-id="d6dca-151">iconPxSize</span><span class="sxs-lookup"><span data-stu-id="d6dca-151">iconPxSize</span></span> | `data-icon-px-size` | <span data-ttu-id="d6dca-152">number (como una cadena)</span><span class="sxs-lookup"><span data-stu-id="d6dca-152">number (as a string)</span></span> | `32` | <span data-ttu-id="d6dca-153">El tamaño en píxeles del botón Compartir a Teams que se representará.</span><span class="sxs-lookup"><span data-stu-id="d6dca-153">The size in pixels of the Share-to-Teams button to render.</span></span> |
| <span data-ttu-id="d6dca-154">msgText</span><span class="sxs-lookup"><span data-stu-id="d6dca-154">msgText</span></span> | `data-msg-text` | <span data-ttu-id="d6dca-155">cadena</span><span class="sxs-lookup"><span data-stu-id="d6dca-155">string</span></span> | <span data-ttu-id="d6dca-156">No aplicable</span><span class="sxs-lookup"><span data-stu-id="d6dca-156">n/a</span></span> | <span data-ttu-id="d6dca-157">Texto predeterminado que se insertará antes del vínculo en el cuadro de redacción del mensaje (límite de 200 caracteres)</span><span class="sxs-lookup"><span data-stu-id="d6dca-157">Default Text to be inserted before the link in the message compose box (200 character limit)</span></span> |
| <span data-ttu-id="d6dca-158">assignInstr</span><span class="sxs-lookup"><span data-stu-id="d6dca-158">assignInstr</span></span> | `data-assign-instr` | <span data-ttu-id="d6dca-159">cadena</span><span class="sxs-lookup"><span data-stu-id="d6dca-159">string</span></span> | <span data-ttu-id="d6dca-160">No aplicable</span><span class="sxs-lookup"><span data-stu-id="d6dca-160">n/a</span></span> | <span data-ttu-id="d6dca-161">Texto predeterminado que se va a insertar en el campo "Instrucciones" de asignaciones (límite de 200 caracteres)</span><span class="sxs-lookup"><span data-stu-id="d6dca-161">Default Text to be inserted in the assignments "Instructions" field (200 character limit)</span></span> |
| <span data-ttu-id="d6dca-162">assignTitle</span><span class="sxs-lookup"><span data-stu-id="d6dca-162">assignTitle</span></span> | `data-assign-title` | <span data-ttu-id="d6dca-163">cadena</span><span class="sxs-lookup"><span data-stu-id="d6dca-163">string</span></span> | <span data-ttu-id="d6dca-164">No aplicable</span><span class="sxs-lookup"><span data-stu-id="d6dca-164">n/a</span></span> | <span data-ttu-id="d6dca-165">Texto predeterminado que se va a insertar en el campo "Título" de las asignaciones (límite de 50 caracteres)</span><span class="sxs-lookup"><span data-stu-id="d6dca-165">Default Text to be inserted in the assignments "Title" field (50 character limit)</span></span> |

### <a name="methods"></a><span data-ttu-id="d6dca-166">Métodos</span><span class="sxs-lookup"><span data-stu-id="d6dca-166">Methods</span></span>

**`shareToMicrosoftTeams.renderButtons(options)`**

<span data-ttu-id="d6dca-167">`options` (opcional): `{ elements?: HTMLElement[] }`</span><span class="sxs-lookup"><span data-stu-id="d6dca-167">`options` (optional): `{ elements?: HTMLElement[] }`</span></span>

<span data-ttu-id="d6dca-168">Representa todos los botones de recurso compartido que hay actualmente en la página.</span><span class="sxs-lookup"><span data-stu-id="d6dca-168">Renders all share buttons currently on the page.</span></span> <span data-ttu-id="d6dca-169">Si se proporciona un objeto opcional con una lista de elementos, esos elementos se representarán `options` en botones de uso compartido.</span><span class="sxs-lookup"><span data-stu-id="d6dca-169">If an optional `options` object is supplied with a list of elements, those elements will be rendered into share buttons.</span></span>

### <a name="setting-default-form-values"></a><span data-ttu-id="d6dca-170">Establecer valores de formulario predeterminados</span><span class="sxs-lookup"><span data-stu-id="d6dca-170">Setting default form values</span></span>

<span data-ttu-id="d6dca-171">Opcionalmente, puede elegir establecer valores predeterminados para los siguientes campos en el formulario Compartir en Teams:</span><span class="sxs-lookup"><span data-stu-id="d6dca-171">Optionally, you can choose to set default values for the following fields on the Share to Teams form:</span></span>

* <span data-ttu-id="d6dca-172">Diga algo al respecto ( `msgText` )</span><span class="sxs-lookup"><span data-stu-id="d6dca-172">Say something about this (`msgText`)</span></span>
* <span data-ttu-id="d6dca-173">Instrucciones de asignación ( `assignInstr` )</span><span class="sxs-lookup"><span data-stu-id="d6dca-173">Assignment Instructions (`assignInstr`)</span></span>
* <span data-ttu-id="d6dca-174">Título de asignación ( `assignTitle` )</span><span class="sxs-lookup"><span data-stu-id="d6dca-174">Assignment Title (`assignTitle`)</span></span>

#### <a name="example-default-form-values"></a><span data-ttu-id="d6dca-175">Ejemplo: valores de formulario predeterminados</span><span class="sxs-lookup"><span data-stu-id="d6dca-175">Example: Default form values</span></span>

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```

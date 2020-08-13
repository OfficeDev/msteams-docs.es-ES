---
title: Adición de un recurso compartido en el botón de Microsoft Teams en el sitio web
description: Cómo agregar el botón compartir a Microsoft Teams insertado en el sitio web
keywords: Compartir recursos compartidos entre equipos
ms.openlocfilehash: 0ebd47af068bf523f27c19241b85d2137af3ada6
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652199"
---
# <a name="adding-a-share-to-teams-button-to-your-website"></a><span data-ttu-id="6dc2e-104">Adición de un recurso compartido en el botón de Microsoft Teams en el sitio web</span><span class="sxs-lookup"><span data-stu-id="6dc2e-104">Adding a Share to Teams button to your website</span></span>

>[!NOTE]
> * <span data-ttu-id="6dc2e-105">Solo se admiten las versiones de escritorio de Edge y Chrome.</span><span class="sxs-lookup"><span data-stu-id="6dc2e-105">Only the desktop versions of Edge and Chrome are supported.</span></span>
> * <span data-ttu-id="6dc2e-106">No se admite el uso de cuentas de Freemium o invitado.</span><span class="sxs-lookup"><span data-stu-id="6dc2e-106">Use of Freemium or guest accounts is not supported.</span></span>

<span data-ttu-id="6dc2e-107">Los sitios web de terceros pueden usar el script del iniciador para incrustar recursos compartidos en los equipos de sus páginas web, lo que iniciará la experiencia compartir a Microsoft Teams en una ventana emergente al hacer clic en ella.</span><span class="sxs-lookup"><span data-stu-id="6dc2e-107">Third-party websites can use the launcher script to embed Share to Teams buttons on their webpages which will launch the Share to Teams experience in a popup window when clicked.</span></span> <span data-ttu-id="6dc2e-108">Esto le permitirá compartir un vínculo directamente a cualquier persona o canal de Microsoft Teams sin cambiar el contexto.</span><span class="sxs-lookup"><span data-stu-id="6dc2e-108">This will allow you to share a link directly to any person or Microsoft Teams channel without switching context.</span></span>

![Menú emergente compartir a Microsoft Teams](~/assets/images/share-to-teams-popup.png)

## <a name="how-to-embed-a-share-to-teams-button"></a><span data-ttu-id="6dc2e-110">Cómo incrustar un recurso compartido en el botón de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="6dc2e-110">How to embed a Share to Teams button</span></span>

<span data-ttu-id="6dc2e-111">En primer lugar, tendrá que agregar el `launcher.js` script en su página web.</span><span class="sxs-lookup"><span data-stu-id="6dc2e-111">First, you'll need to add the `launcher.js` script on your webpage.</span></span>

```html
<script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
```

<span data-ttu-id="6dc2e-112">A continuación, agregue un elemento HTML en la página web con el `teams-share-button` atributo class y el vínculo para compartir en el `data-href` atributo.</span><span class="sxs-lookup"><span data-stu-id="6dc2e-112">Next, add an HTML element on your webpage with the `teams-share-button` class attribute and the link to share in the `data-href` attribute.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>">
</div>
```

<span data-ttu-id="6dc2e-113">Se agregará el icono de Microsoft Teams a su sitio Web.</span><span class="sxs-lookup"><span data-stu-id="6dc2e-113">This will add the Microsoft Teams icon to your website.</span></span>

![Icono compartir a teams](~/assets/icons/share-to-teams-icon.png)

<span data-ttu-id="6dc2e-115">De manera opcional, si desea un tamaño de icono diferente para el botón compartir a Teams, use el `data-icon-px-size` atributo.</span><span class="sxs-lookup"><span data-stu-id="6dc2e-115">Optionally, if you want a different icon size for the Share to Teams button, use the `data-icon-px-size` attribute.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-icon-px-size="64">
</div>
```

<span data-ttu-id="6dc2e-116">Si sabe que la vista previa de la dirección URL del vínculo que se va a compartir no se representará correctamente en Teams (por ejemplo, el vínculo requerirá la autenticación del usuario), puede deshabilitar la vista previa de la dirección URL agregando el `data-preview` atributo set a `false` .</span><span class="sxs-lookup"><span data-stu-id="6dc2e-116">If you know that the URL preview from your link to be shared won't render well in Teams (for example the link would require user authentication) you can disable the URL preview by adding the `data-preview` attribute set to `false`.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-preview="false">
</div>
```

<span data-ttu-id="6dc2e-117">Si la página representa el contenido de forma dinámica, puede usar el `shareToMicrosoftTeams.renderButtons()` método para forzar que el botón **compartir** se represente en el punto adecuado de la canalización.</span><span class="sxs-lookup"><span data-stu-id="6dc2e-117">If your page dynamically renders content, you can use the the `shareToMicrosoftTeams.renderButtons()` method to force the **Share** button to render at the appropriate place in the pipeline.</span></span>

## <a name="crafting-your-website-preview"></a><span data-ttu-id="6dc2e-118">Diseñar la vista previa del sitio web</span><span class="sxs-lookup"><span data-stu-id="6dc2e-118">Crafting your website preview</span></span>

<span data-ttu-id="6dc2e-119">Cuando se comparta su sitio web con Microsoft Teams, la tarjeta que se inserte en el canal seleccionado contendrá una vista previa de su sitio Web.</span><span class="sxs-lookup"><span data-stu-id="6dc2e-119">When your website is shared to Teams, the card that is inserted into the selected channel will contain a preview of your website.</span></span> <span data-ttu-id="6dc2e-120">Puede controlar el comportamiento de esta vista previa garantizando que se agreguen los metadatos adecuados al sitio web que se va a compartir (la `data-href` dirección URL).</span><span class="sxs-lookup"><span data-stu-id="6dc2e-120">You can control the behavior of this preview by ensuring the appropriate meta-data is added to the website being shared (the `data-href` URL).</span></span> <span data-ttu-id="6dc2e-121">En la tabla siguiente se describen las etiquetas necesarias.</span><span class="sxs-lookup"><span data-stu-id="6dc2e-121">The table below outlines the necessary tags.</span></span> <span data-ttu-id="6dc2e-122">Puede usar las versiones predeterminadas de HTML o la versión de Open Graph.</span><span class="sxs-lookup"><span data-stu-id="6dc2e-122">You can use either the html default versions, or the Open Graph version.</span></span>

<span data-ttu-id="6dc2e-123">Para que se muestre la vista previa, debe:</span><span class="sxs-lookup"><span data-stu-id="6dc2e-123">In order for the preview to be displayed you must:</span></span>

* <span data-ttu-id="6dc2e-124">Incluya una imagen en miniatura, o bien un título y una descripción (para obtener mejores resultados, incluir los tres).</span><span class="sxs-lookup"><span data-stu-id="6dc2e-124">Include either a Thumbnail image, or both a Title and Description (for best results, include all three).</span></span>
* <span data-ttu-id="6dc2e-125">La dirección URL que se comparte no puede requerir autenticación.</span><span class="sxs-lookup"><span data-stu-id="6dc2e-125">The URL being shared cannot require authentication.</span></span> <span data-ttu-id="6dc2e-126">Si es así, puede compartirla, pero no se creará la vista previa.</span><span class="sxs-lookup"><span data-stu-id="6dc2e-126">If it does you can still share it, but the preview will not be created.</span></span>

|<span data-ttu-id="6dc2e-127">Valor</span><span class="sxs-lookup"><span data-stu-id="6dc2e-127">Value</span></span>|<span data-ttu-id="6dc2e-128">Etiqueta meta</span><span class="sxs-lookup"><span data-stu-id="6dc2e-128">Meta tag</span></span>| <span data-ttu-id="6dc2e-129">Abrir gráfico</span><span class="sxs-lookup"><span data-stu-id="6dc2e-129">Open Graph</span></span>|
|----|----|----|
|<span data-ttu-id="6dc2e-130">El título</span><span class="sxs-lookup"><span data-stu-id="6dc2e-130">Title</span></span>|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|<span data-ttu-id="6dc2e-131">Description</span><span class="sxs-lookup"><span data-stu-id="6dc2e-131">Description</span></span>|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|<span data-ttu-id="6dc2e-132">Imagen en miniatura</span><span class="sxs-lookup"><span data-stu-id="6dc2e-132">Thumbnail Image</span></span>| <span data-ttu-id="6dc2e-133">ninguno</span><span class="sxs-lookup"><span data-stu-id="6dc2e-133">none</span></span> |`<meta property="og:image" content="http://example.com/image.jpg">`|

## <a name="share-to-teams-for-education"></a><span data-ttu-id="6dc2e-134">Compartir con Teams para el ámbito educativo</span><span class="sxs-lookup"><span data-stu-id="6dc2e-134">Share to Teams for Education</span></span>

<span data-ttu-id="6dc2e-135">Para los profesores que usen el botón compartir a Microsoft Teams, se le ofrecerá una opción adicional `Create an Assignment` .</span><span class="sxs-lookup"><span data-stu-id="6dc2e-135">For teachers using the Share to Teams button you'll be given an additional option to `Create an Assignment`.</span></span> <span data-ttu-id="6dc2e-136">Esto le permite crear rápidamente una tarea en el equipo seleccionado en función del vínculo compartido.</span><span class="sxs-lookup"><span data-stu-id="6dc2e-136">This enables you to quickly create an assignment in the chosen Team based on the shared link.</span></span>

![Menú emergente compartir a Microsoft Teams](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a><span data-ttu-id="6dc2e-138">Definición de launcher.js completo</span><span class="sxs-lookup"><span data-stu-id="6dc2e-138">Full launcher.js definition</span></span>

| <span data-ttu-id="6dc2e-139">Propiedad</span><span class="sxs-lookup"><span data-stu-id="6dc2e-139">Property</span></span> | <span data-ttu-id="6dc2e-140">Atributo HTML</span><span class="sxs-lookup"><span data-stu-id="6dc2e-140">HTML attribute</span></span> | <span data-ttu-id="6dc2e-141">Tipo</span><span class="sxs-lookup"><span data-stu-id="6dc2e-141">Type</span></span> | <span data-ttu-id="6dc2e-142">Predeterminado</span><span class="sxs-lookup"><span data-stu-id="6dc2e-142">Default</span></span> | <span data-ttu-id="6dc2e-143">Descripción</span><span class="sxs-lookup"><span data-stu-id="6dc2e-143">Description</span></span> |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| <span data-ttu-id="6dc2e-144">href</span><span class="sxs-lookup"><span data-stu-id="6dc2e-144">href</span></span> | `data-href` | <span data-ttu-id="6dc2e-145">string</span><span class="sxs-lookup"><span data-stu-id="6dc2e-145">string</span></span> | <span data-ttu-id="6dc2e-146">No aplicable</span><span class="sxs-lookup"><span data-stu-id="6dc2e-146">n/a</span></span> | <span data-ttu-id="6dc2e-147">Href del contenido que se va a compartir.</span><span class="sxs-lookup"><span data-stu-id="6dc2e-147">The href of the content to share.</span></span> |
| <span data-ttu-id="6dc2e-148">preview</span><span class="sxs-lookup"><span data-stu-id="6dc2e-148">preview</span></span> | `data-preview` | <span data-ttu-id="6dc2e-149">booleano (como una cadena)</span><span class="sxs-lookup"><span data-stu-id="6dc2e-149">boolean (as a string)</span></span> | `true` | <span data-ttu-id="6dc2e-150">Indica si se va a mostrar una vista previa del contenido que se va a compartir.</span><span class="sxs-lookup"><span data-stu-id="6dc2e-150">Whether or not to show a preview of the content to share.</span></span> |
| <span data-ttu-id="6dc2e-151">iconPxSize</span><span class="sxs-lookup"><span data-stu-id="6dc2e-151">iconPxSize</span></span> | `data-icon-px-size` | <span data-ttu-id="6dc2e-152">número (como una cadena)</span><span class="sxs-lookup"><span data-stu-id="6dc2e-152">number (as a string)</span></span> | `32` | <span data-ttu-id="6dc2e-153">Tamaño en píxeles del botón Share-to-teams que se va a representar.</span><span class="sxs-lookup"><span data-stu-id="6dc2e-153">The size in pixels of the Share-to-Teams button to render.</span></span> |
| <span data-ttu-id="6dc2e-154">msgText</span><span class="sxs-lookup"><span data-stu-id="6dc2e-154">msgText</span></span> | `data-msg-text` | <span data-ttu-id="6dc2e-155">string</span><span class="sxs-lookup"><span data-stu-id="6dc2e-155">string</span></span> | <span data-ttu-id="6dc2e-156">No aplicable</span><span class="sxs-lookup"><span data-stu-id="6dc2e-156">n/a</span></span> | <span data-ttu-id="6dc2e-157">Texto predeterminado que se inserta delante del vínculo en el cuadro de redacción del mensaje (límite de 200 caracteres)</span><span class="sxs-lookup"><span data-stu-id="6dc2e-157">Default Text to be inserted before the link in the message compose box (200 character limit)</span></span> |
| <span data-ttu-id="6dc2e-158">assignInstr</span><span class="sxs-lookup"><span data-stu-id="6dc2e-158">assignInstr</span></span> | `data-assign-instr` | <span data-ttu-id="6dc2e-159">string</span><span class="sxs-lookup"><span data-stu-id="6dc2e-159">string</span></span> | <span data-ttu-id="6dc2e-160">No aplicable</span><span class="sxs-lookup"><span data-stu-id="6dc2e-160">n/a</span></span> | <span data-ttu-id="6dc2e-161">Texto predeterminado que se insertará en el campo "instrucciones" de las asignaciones (límite de 200 caracteres)</span><span class="sxs-lookup"><span data-stu-id="6dc2e-161">Default Text to be inserted in the assignments "Instructions" field (200 character limit)</span></span> |
| <span data-ttu-id="6dc2e-162">assignTitle</span><span class="sxs-lookup"><span data-stu-id="6dc2e-162">assignTitle</span></span> | `data-assign-title` | <span data-ttu-id="6dc2e-163">string</span><span class="sxs-lookup"><span data-stu-id="6dc2e-163">string</span></span> | <span data-ttu-id="6dc2e-164">No aplicable</span><span class="sxs-lookup"><span data-stu-id="6dc2e-164">n/a</span></span> | <span data-ttu-id="6dc2e-165">Texto predeterminado que se va a insertar en el campo "título" de las asignaciones (límite de 50 caracteres)</span><span class="sxs-lookup"><span data-stu-id="6dc2e-165">Default Text to be inserted in the assignments "Title" field (50 character limit)</span></span> |

### <a name="methods"></a><span data-ttu-id="6dc2e-166">Métodos</span><span class="sxs-lookup"><span data-stu-id="6dc2e-166">Methods</span></span>

**`shareToMicrosoftTeams.renderButtons(options)`**

<span data-ttu-id="6dc2e-167">`options`(opcional):`{ elements?: HTMLElement[] }`</span><span class="sxs-lookup"><span data-stu-id="6dc2e-167">`options` (optional): `{ elements?: HTMLElement[] }`</span></span>

<span data-ttu-id="6dc2e-168">Representa todos los botones compartir que hay actualmente en la página.</span><span class="sxs-lookup"><span data-stu-id="6dc2e-168">Renders all share buttons currently on the page.</span></span> <span data-ttu-id="6dc2e-169">Si `options` se proporciona un objeto opcional con una lista de elementos, esos elementos se representarán en botones para compartir.</span><span class="sxs-lookup"><span data-stu-id="6dc2e-169">If an optional `options` object is supplied with a list of elements, those elements will be rendered into share buttons.</span></span>

### <a name="setting-default-form-values"></a><span data-ttu-id="6dc2e-170">Establecer valores de formulario predeterminado</span><span class="sxs-lookup"><span data-stu-id="6dc2e-170">Setting default form values</span></span>

<span data-ttu-id="6dc2e-171">De manera opcional, puede elegir establecer los valores predeterminados para los siguientes campos en el formulario compartir a Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="6dc2e-171">Optionally, you can choose to set default values for the following fields on the Share to Teams form:</span></span>

* <span data-ttu-id="6dc2e-172">Indique algo sobre esto ( `msgText` ).</span><span class="sxs-lookup"><span data-stu-id="6dc2e-172">Say something about this (`msgText`)</span></span>
* <span data-ttu-id="6dc2e-173">Instrucciones de asignación ( `assignInstr` )</span><span class="sxs-lookup"><span data-stu-id="6dc2e-173">Assignment Instructions (`assignInstr`)</span></span>
* <span data-ttu-id="6dc2e-174">Título de la asignación ( `assignTitle` )</span><span class="sxs-lookup"><span data-stu-id="6dc2e-174">Assignment Title (`assignTitle`)</span></span>

#### <a name="example-default-form-values"></a><span data-ttu-id="6dc2e-175">Ejemplo: valores predeterminados del formulario</span><span class="sxs-lookup"><span data-stu-id="6dc2e-175">Example: Default form values</span></span>

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```

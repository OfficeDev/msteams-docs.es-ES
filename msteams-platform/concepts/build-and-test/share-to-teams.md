---
title: Crear un botón Compartir en Teams
description: Cómo agregar el botón Compartir a Teams incrustado en su sitio web
ms.topic: reference
localization_priority: Normal
keywords: Share Teams Share-to-Teams
ms.openlocfilehash: c8bbb371e2d68bf063c3aa5e02c7cf3ec911c0b8
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058477"
---
# <a name="create-share-to-teams-button"></a><span data-ttu-id="47469-104">Crear un botón Compartir en Teams</span><span class="sxs-lookup"><span data-stu-id="47469-104">Create Share-to-Teams button</span></span>

<span data-ttu-id="47469-105">Los sitios web de terceros pueden usar el script del iniciador para insertar botones de Share-to-Teams en sus páginas web.</span><span class="sxs-lookup"><span data-stu-id="47469-105">Third-party websites can use the launcher script to embed Share-to-Teams buttons on their webpages.</span></span> <span data-ttu-id="47469-106">Cuando selecciona, inicia la experiencia de Share-to-Teams en una ventana emergente.</span><span class="sxs-lookup"><span data-stu-id="47469-106">When you select, it launches the Share-to-Teams experience in a pop-up window.</span></span> <span data-ttu-id="47469-107">Esto le permite compartir un vínculo directamente con cualquier persona o canal de Microsoft Teams sin cambiar el contexto.</span><span class="sxs-lookup"><span data-stu-id="47469-107">This allows you to share a link directly to any person or Microsoft Teams channel without switching the context.</span></span> <span data-ttu-id="47469-108">Este documento le guía sobre cómo crear e insertar un botón Compartir a Teams para su sitio web, crear la vista previa del sitio web y ampliar Share-to-Teams for Education.</span><span class="sxs-lookup"><span data-stu-id="47469-108">This document guides you on how to create, and embed a Share-to-Teams button for your website, craft your website preview, and extend Share-to-Teams for Education.</span></span>

> [!NOTE]
> * <span data-ttu-id="47469-109">Solo se admiten las versiones de escritorio de Edge y Chrome.</span><span class="sxs-lookup"><span data-stu-id="47469-109">Only the desktop versions of Edge and Chrome are supported.</span></span>
> * <span data-ttu-id="47469-110">No se admite el uso de freemium o cuentas de invitado.</span><span class="sxs-lookup"><span data-stu-id="47469-110">Use of Freemium or guest accounts is not supported.</span></span>  

<span data-ttu-id="47469-111">En la siguiente imagen se muestra la experiencia emergente de Share-to-Teams:</span><span class="sxs-lookup"><span data-stu-id="47469-111">The following image displays the Share-to-Teams pop-up experience:</span></span>

![Elemento emergente de Share-to-Teams](~/assets/images/share-to-teams-popup.png)

## <a name="embed-a-share-to-teams-button"></a><span data-ttu-id="47469-113">Insertar un botón Compartir en Teams</span><span class="sxs-lookup"><span data-stu-id="47469-113">Embed a Share to Teams button</span></span>

1. <span data-ttu-id="47469-114">Agregue el `launcher.js` script en la página web.</span><span class="sxs-lookup"><span data-stu-id="47469-114">Add the `launcher.js` script on your webpage.</span></span>

    ```html
    <script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
    ```

1. <span data-ttu-id="47469-115">Agregue un elemento HTML en la página web con el atributo `teams-share-button` class y el vínculo para compartir en el `data-href` atributo.</span><span class="sxs-lookup"><span data-stu-id="47469-115">Add a HTML element on your webpage with the `teams-share-button` class attribute and the link to share in the `data-href` attribute.</span></span>

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>">
    </div>
    ```

    <span data-ttu-id="47469-116">Después de completar esto, el icono de Microsoft Teams se agrega a su sitio web.</span><span class="sxs-lookup"><span data-stu-id="47469-116">After completing this, the Microsoft Teams icon gets added to your website.</span></span> <span data-ttu-id="47469-117">En la siguiente imagen se muestra el icono de Share-to-Teams:</span><span class="sxs-lookup"><span data-stu-id="47469-117">The following image shows Share-to-Teams icon:</span></span>

    ![Icono Compartir en Teams](~/assets/icons/share-to-teams-icon.png)

1. <span data-ttu-id="47469-119">Como alternativa, si desea un tamaño de icono diferente para el botón Compartir con Teams, use el `data-icon-px-size` atributo.</span><span class="sxs-lookup"><span data-stu-id="47469-119">Alternatively, if you want a different icon size for the Share-to Teams button, use the `data-icon-px-size` attribute.</span></span>

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```
1. <span data-ttu-id="47469-120">Si el vínculo compartido requiere autenticación de usuario y la vista previa de la dirección URL del vínculo que se va a compartir no se representa correctamente en Teams, puede deshabilitar la vista previa de la dirección URL agregando el atributo establecido `data-preview` en `false` .</span><span class="sxs-lookup"><span data-stu-id="47469-120">If the shared link requires user authentication, and the URL preview from your link to be shared does not render well in Teams then, you can disable the URL preview by adding the `data-preview` attribute set to `false`.</span></span>

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-preview="false">
    </div>
    ```

1. <span data-ttu-id="47469-121">Si la página representa contenido dinámicamente, puede usar el método para forzar que el botón Compartir se represente en el `shareToMicrosoftTeams.renderButtons()` lugar adecuado de la canalización. </span><span class="sxs-lookup"><span data-stu-id="47469-121">If your page dynamically renders content, you can use the the `shareToMicrosoftTeams.renderButtons()` method to force the **Share** button to render at the appropriate place in the pipeline.</span></span>

## <a name="craft-your-website-preview"></a><span data-ttu-id="47469-122">Crear una vista previa del sitio web</span><span class="sxs-lookup"><span data-stu-id="47469-122">Craft your website preview</span></span>

<span data-ttu-id="47469-123">Cuando el sitio web se comparte con Teams, la tarjeta que se inserta en el canal seleccionado contiene una vista previa del sitio web.</span><span class="sxs-lookup"><span data-stu-id="47469-123">When your website is shared to Teams, the card that is inserted into the selected channel contains a preview of your website.</span></span> <span data-ttu-id="47469-124">Puedes controlar el comportamiento de esta vista previa asegurando que los metadatos adecuados se agregan al sitio web que se comparte, como la `data-href` dirección URL.</span><span class="sxs-lookup"><span data-stu-id="47469-124">You can control the behavior of this preview by ensuring the appropriate meta-data is added to the website being shared, such as the `data-href` URL.</span></span>  

<span data-ttu-id="47469-125">**Para mostrar la vista previa**</span><span class="sxs-lookup"><span data-stu-id="47469-125">**To display the preview**</span></span>

* <span data-ttu-id="47469-126">Debe incluir una imagen **en miniatura** o un **título** y una **descripción**.</span><span class="sxs-lookup"><span data-stu-id="47469-126">You must include either a **Thumbnail image**, or both a **Title** and **Description**.</span></span> <span data-ttu-id="47469-127">Para obtener los mejores resultados, incluya los tres.</span><span class="sxs-lookup"><span data-stu-id="47469-127">For best results, include all three.</span></span>
* <span data-ttu-id="47469-128">La dirección URL compartida no requiere autenticación.</span><span class="sxs-lookup"><span data-stu-id="47469-128">The shared URL does not require authentication.</span></span> <span data-ttu-id="47469-129">Si requiere autenticación, puede compartirla, pero no se crea la vista previa.</span><span class="sxs-lookup"><span data-stu-id="47469-129">If it requires authentication, you can share it, but the preview is not created.</span></span>

<span data-ttu-id="47469-130">En la tabla siguiente se describen las etiquetas necesarias:</span><span class="sxs-lookup"><span data-stu-id="47469-130">The following table outlines the necessary tags:</span></span>

|<span data-ttu-id="47469-131">Valor</span><span class="sxs-lookup"><span data-stu-id="47469-131">Value</span></span>|<span data-ttu-id="47469-132">Etiqueta meta</span><span class="sxs-lookup"><span data-stu-id="47469-132">Meta tag</span></span>| <span data-ttu-id="47469-133">Open Graph</span><span class="sxs-lookup"><span data-stu-id="47469-133">Open Graph</span></span>|
|----|----|----|
|<span data-ttu-id="47469-134">Title</span><span class="sxs-lookup"><span data-stu-id="47469-134">Title</span></span>|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|<span data-ttu-id="47469-135">Description</span><span class="sxs-lookup"><span data-stu-id="47469-135">Description</span></span>|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|<span data-ttu-id="47469-136">Imagen en miniatura</span><span class="sxs-lookup"><span data-stu-id="47469-136">Thumbnail Image</span></span>| <span data-ttu-id="47469-137">ninguno.</span><span class="sxs-lookup"><span data-stu-id="47469-137">none.</span></span> |`<meta property="og:image" content="http://example.com/image.jpg">`|

<span data-ttu-id="47469-138">Puede usar las versiones predeterminadas html o la versión de Open Graph.</span><span class="sxs-lookup"><span data-stu-id="47469-138">You can use either the html default versions, or the Open Graph version.</span></span>

## <a name="share-to-teams-for-education"></a><span data-ttu-id="47469-139">Compartir con Teams para Educación</span><span class="sxs-lookup"><span data-stu-id="47469-139">Share to Teams for Education</span></span>

<span data-ttu-id="47469-140">Para los profesores que usan el botón Compartir en Teams, hay una opción adicional para `Create an Assignment` .</span><span class="sxs-lookup"><span data-stu-id="47469-140">For teachers using the Share to Teams button, there is an additional option to `Create an Assignment`.</span></span> <span data-ttu-id="47469-141">Esto le permite crear rápidamente una asignación en el equipo elegido, en función del vínculo compartido.</span><span class="sxs-lookup"><span data-stu-id="47469-141">This enables you to quickly create an assignment in the chosen Team, based on the shared link.</span></span> <span data-ttu-id="47469-142">En la siguiente imagen se muestra Share-to-Teams para educación:</span><span class="sxs-lookup"><span data-stu-id="47469-142">The following image displays Share-to-Teams for education:</span></span> 

![Compartir con educación emergente de Teams](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a><span data-ttu-id="47469-144">Definición launcher.js completa</span><span class="sxs-lookup"><span data-stu-id="47469-144">Full launcher.js definition</span></span>

| <span data-ttu-id="47469-145">Propiedad</span><span class="sxs-lookup"><span data-stu-id="47469-145">Property</span></span> | <span data-ttu-id="47469-146">Atributo HTML</span><span class="sxs-lookup"><span data-stu-id="47469-146">HTML attribute</span></span> | <span data-ttu-id="47469-147">Tipo</span><span class="sxs-lookup"><span data-stu-id="47469-147">Type</span></span> | <span data-ttu-id="47469-148">Predeterminado</span><span class="sxs-lookup"><span data-stu-id="47469-148">Default</span></span> | <span data-ttu-id="47469-149">Descripción</span><span class="sxs-lookup"><span data-stu-id="47469-149">Description</span></span> |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| <span data-ttu-id="47469-150">href</span><span class="sxs-lookup"><span data-stu-id="47469-150">href</span></span> | `data-href` | <span data-ttu-id="47469-151">string</span><span class="sxs-lookup"><span data-stu-id="47469-151">string</span></span> | <span data-ttu-id="47469-152">No aplicable</span><span class="sxs-lookup"><span data-stu-id="47469-152">n/a</span></span> | <span data-ttu-id="47469-153">Href del contenido que se debe compartir.</span><span class="sxs-lookup"><span data-stu-id="47469-153">The href of the content to share.</span></span> |
| <span data-ttu-id="47469-154">preview</span><span class="sxs-lookup"><span data-stu-id="47469-154">preview</span></span> | `data-preview` | <span data-ttu-id="47469-155">boolean (como una cadena)</span><span class="sxs-lookup"><span data-stu-id="47469-155">boolean (as a string)</span></span> | `true` | <span data-ttu-id="47469-156">Mostrar o no una vista previa del contenido que se va a compartir.</span><span class="sxs-lookup"><span data-stu-id="47469-156">Whether or not to show a preview of the content to share.</span></span> |
| <span data-ttu-id="47469-157">iconPxSize</span><span class="sxs-lookup"><span data-stu-id="47469-157">iconPxSize</span></span> | `data-icon-px-size` | <span data-ttu-id="47469-158">número (como una cadena)</span><span class="sxs-lookup"><span data-stu-id="47469-158">number (as a string)</span></span> | `32` | <span data-ttu-id="47469-159">Tamaño en píxeles del botón Compartir a Teams que se representará.</span><span class="sxs-lookup"><span data-stu-id="47469-159">The size in pixels of the Share-to-Teams button to render.</span></span> |
| <span data-ttu-id="47469-160">msgText</span><span class="sxs-lookup"><span data-stu-id="47469-160">msgText</span></span> | `data-msg-text` | <span data-ttu-id="47469-161">string</span><span class="sxs-lookup"><span data-stu-id="47469-161">string</span></span> | <span data-ttu-id="47469-162">No aplicable</span><span class="sxs-lookup"><span data-stu-id="47469-162">n/a</span></span> | <span data-ttu-id="47469-163">Texto predeterminado que se va a insertar antes del vínculo en el cuadro de redacción del mensaje.</span><span class="sxs-lookup"><span data-stu-id="47469-163">Default Text to be inserted before the link in the message compose box.</span></span> <span data-ttu-id="47469-164">El número máximo de caracteres es 200.</span><span class="sxs-lookup"><span data-stu-id="47469-164">Maximum number of characters is 200.</span></span> |
| <span data-ttu-id="47469-165">assignInstr</span><span class="sxs-lookup"><span data-stu-id="47469-165">assignInstr</span></span> | `data-assign-instr` | <span data-ttu-id="47469-166">string</span><span class="sxs-lookup"><span data-stu-id="47469-166">string</span></span> | <span data-ttu-id="47469-167">No aplicable</span><span class="sxs-lookup"><span data-stu-id="47469-167">n/a</span></span> | <span data-ttu-id="47469-168">Texto predeterminado que se insertará en el campo asignaciones "Instrucciones".</span><span class="sxs-lookup"><span data-stu-id="47469-168">Default Text to be inserted in the assignments "Instructions" field.</span></span> <span data-ttu-id="47469-169">El número máximo de caracteres es 200.</span><span class="sxs-lookup"><span data-stu-id="47469-169">Maximum number of characters is 200.</span></span> |
| <span data-ttu-id="47469-170">assignTitle</span><span class="sxs-lookup"><span data-stu-id="47469-170">assignTitle</span></span> | `data-assign-title` | <span data-ttu-id="47469-171">string</span><span class="sxs-lookup"><span data-stu-id="47469-171">string</span></span> | <span data-ttu-id="47469-172">No aplicable</span><span class="sxs-lookup"><span data-stu-id="47469-172">n/a</span></span> | <span data-ttu-id="47469-173">Texto predeterminado que se insertará en el campo asignaciones "Título".</span><span class="sxs-lookup"><span data-stu-id="47469-173">Default Text to be inserted in the assignments "Title" field.</span></span> <span data-ttu-id="47469-174">El número máximo de caracteres es 50.</span><span class="sxs-lookup"><span data-stu-id="47469-174">Maximum number of characters is 50.</span></span> |

### <a name="methods"></a><span data-ttu-id="47469-175">Métodos</span><span class="sxs-lookup"><span data-stu-id="47469-175">Methods</span></span>

**`shareToMicrosoftTeams.renderButtons(options)`**

<span data-ttu-id="47469-176">`options` (opcional): `{ elements?: HTMLElement[] }`</span><span class="sxs-lookup"><span data-stu-id="47469-176">`options` (optional): `{ elements?: HTMLElement[] }`</span></span>

<span data-ttu-id="47469-177">Actualmente, todos los botones de recurso compartido se representan en la página.</span><span class="sxs-lookup"><span data-stu-id="47469-177">Currently, all share buttons are rendered on the page.</span></span> <span data-ttu-id="47469-178">Si se proporciona `options` un objeto opcional con una lista de elementos, estos elementos se representan en botones de uso compartido.</span><span class="sxs-lookup"><span data-stu-id="47469-178">If an optional `options` object is supplied with a list of elements, those elements are rendered into share buttons.</span></span>

### <a name="set-default-form-values"></a><span data-ttu-id="47469-179">Establecer valores de formulario predeterminados</span><span class="sxs-lookup"><span data-stu-id="47469-179">Set default form values</span></span>

<span data-ttu-id="47469-180">Puede seleccionar para establecer los valores predeterminados de los siguientes campos en el formulario Compartir en Teams:</span><span class="sxs-lookup"><span data-stu-id="47469-180">You can select to set default values for the following fields on the Share to Teams form:</span></span>

* <span data-ttu-id="47469-181">Diga algo al respecto: `msgText`</span><span class="sxs-lookup"><span data-stu-id="47469-181">Say something about this: `msgText`</span></span>
* <span data-ttu-id="47469-182">Instrucciones de asignación: `assignInstr`</span><span class="sxs-lookup"><span data-stu-id="47469-182">Assignment Instructions: `assignInstr`</span></span>
* <span data-ttu-id="47469-183">Título de asignación: `assignTitle`</span><span class="sxs-lookup"><span data-stu-id="47469-183">Assignment Title: `assignTitle`</span></span>

#### <a name="example"></a><span data-ttu-id="47469-184">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="47469-184">Example</span></span>

 <span data-ttu-id="47469-185">Los valores de formulario predeterminados se dan en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="47469-185">Default form values are given in the following example:</span></span>

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```

## <a name="see-also"></a><span data-ttu-id="47469-186">Vea también</span><span class="sxs-lookup"><span data-stu-id="47469-186">See also</span></span>

- [<span data-ttu-id="47469-187">Integrar aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="47469-187">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)

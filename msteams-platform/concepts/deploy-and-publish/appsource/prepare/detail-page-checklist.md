---
title: Crear una descripción de la tienda para la aplicación
description: Describe cómo crear una descripción de la tienda para tu Microsoft Teams aplicación.
ms.topic: how-to
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 270936ca967c17caaa8a56f85057b20ca3d6a409
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101432"
---
# <a name="create-a-store-listing-for-your-microsoft-teams-app"></a><span data-ttu-id="760b3-103">Crear una descripción de la tienda para tu Microsoft Teams aplicación</span><span class="sxs-lookup"><span data-stu-id="760b3-103">Create a store listing for your Microsoft Teams app</span></span>

<span data-ttu-id="760b3-104">La información que envías al Centro de partners [&#8212;](https://partner.microsoft.com) incluyendo tu nombre, descripciones, iconos e imágenes&#8212;se convierte en la tienda Microsoft Teams y la descripción de Microsoft AppSource para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="760b3-104">The information that you submit to [Partner Center](https://partner.microsoft.com)&#8212;including your name, descriptions, icons, and images&#8212;becomes the Microsoft Teams store and Microsoft AppSource listing for your app.</span></span>

<span data-ttu-id="760b3-105">Una descripción de la tienda puede ser la primera impresión de alguien de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="760b3-105">A store listing may be someone's first impression of your app.</span></span> <span data-ttu-id="760b3-106">Aumente las instalaciones con una descripción que transmita eficazmente las ventajas, funcionalidad y marca de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="760b3-106">Increase your installations with a listing that effectively conveys your app's benefits, functionality, and brand.</span></span>

## <a name="specify-a-short-name"></a><span data-ttu-id="760b3-107">Especificar un nombre corto</span><span class="sxs-lookup"><span data-stu-id="760b3-107">Specify a short name</span></span>

<span data-ttu-id="760b3-108">El nombre de la aplicación (específicamente, su [*nombre*](~/resources/schema/manifest-schema.md#name)corto) desempeña un papel fundamental en la forma en que los usuarios lo descubren en la tienda.</span><span class="sxs-lookup"><span data-stu-id="760b3-108">Your app's name (specifically, its [*short name*](~/resources/schema/manifest-schema.md#name)) plays a crucial role in how users discover it in the store.</span></span>

<span data-ttu-id="760b3-109">En el ejemplo siguiente se resalta dónde se muestra el nombre corto de una aplicación en una descripción de la tienda.</span><span class="sxs-lookup"><span data-stu-id="760b3-109">The following example highlights where an app's short name displays in a store listing.</span></span>

:::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="La captura de pantalla de ejemplo resalta dónde se muestra el nombre corto de una aplicación en una descripción de la tienda.":::

### <a name="best-practices-for-names"></a><span data-ttu-id="760b3-111">Procedimientos recomendados para nombres</span><span class="sxs-lookup"><span data-stu-id="760b3-111">Best practices for names</span></span>

<span data-ttu-id="760b3-112">**Sí:**</span><span class="sxs-lookup"><span data-stu-id="760b3-112">**Do:**</span></span>

* <span data-ttu-id="760b3-113">Elige un nombre sencillo y memorable que insinúa lo que hace la aplicación.</span><span class="sxs-lookup"><span data-stu-id="760b3-113">Choose a simple, memorable name that hints at what your app does.</span></span>
* <span data-ttu-id="760b3-114">Ser distintivo.</span><span class="sxs-lookup"><span data-stu-id="760b3-114">Be distinctive.</span></span>
* <span data-ttu-id="760b3-115">Evite errores ortográficos y gramaticales.</span><span class="sxs-lookup"><span data-stu-id="760b3-115">Avoid typos and grammatical errors.</span></span>

<span data-ttu-id="760b3-116">**No:**</span><span class="sxs-lookup"><span data-stu-id="760b3-116">**Don't:**</span></span>

* <span data-ttu-id="760b3-117">Use términos profanos o despectivos.</span><span class="sxs-lookup"><span data-stu-id="760b3-117">Use profane or derogatory terms.</span></span>
* <span data-ttu-id="760b3-118">Use un lenguaje racial o culturalmente insensible.</span><span class="sxs-lookup"><span data-stu-id="760b3-118">Use racially or culturally insensitive language.</span></span>
* <span data-ttu-id="760b3-119">Usa términos genéricos o nombres similares a las aplicaciones existentes.</span><span class="sxs-lookup"><span data-stu-id="760b3-119">Use generic terms or names similar to existing apps.</span></span>
* <span data-ttu-id="760b3-120">Incluya "Teams", "Microsoft", nombres de producto de Microsoft existentes o próximos, o "aplicación" en el nombre.</span><span class="sxs-lookup"><span data-stu-id="760b3-120">Include "Teams", "Microsoft", existing/upcoming Microsoft product names, or  "app" in the name.</span></span>

> [!NOTE]
> <span data-ttu-id="760b3-121">Si la aplicación forma parte de una asociación oficial con Microsoft, el nombre de la aplicación debe ser el primero (por ejemplo, *Salesforce Connector para Microsoft Teams*).</span><span class="sxs-lookup"><span data-stu-id="760b3-121">If your app is part of an official partnership with Microsoft, the name of your app must come first (for example, *Salesforce Connector for Microsoft Teams*).</span></span>

## <a name="write-descriptions"></a><span data-ttu-id="760b3-122">Escribir descripciones</span><span class="sxs-lookup"><span data-stu-id="760b3-122">Write descriptions</span></span>

<span data-ttu-id="760b3-123">Necesitas una descripción corta y larga de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="760b3-123">You need a short and long description of your app.</span></span>

### <a name="short-description"></a><span data-ttu-id="760b3-124">La descripción breve</span><span class="sxs-lookup"><span data-stu-id="760b3-124">Short description</span></span>

<span data-ttu-id="760b3-125">Un resumen conciso de la aplicación que debe ser original, atractivo y dirigido a la audiencia de destino.</span><span class="sxs-lookup"><span data-stu-id="760b3-125">A concise summary of your app that should be original, engaging, and directed at your target audience.</span></span> <span data-ttu-id="760b3-126">Lo ideal es mantener la descripción corta en una oración.</span><span class="sxs-lookup"><span data-stu-id="760b3-126">Ideally, keep the short description to one sentence.</span></span>

<span data-ttu-id="760b3-127">En el ejemplo siguiente se resalta dónde se muestra la descripción breve de una aplicación en una descripción de la tienda:</span><span class="sxs-lookup"><span data-stu-id="760b3-127">The following example highlights where an app's short description displays in a store listing:</span></span>

:::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="La captura de pantalla de ejemplo resalta dónde se muestra la breve descripción de una aplicación en una descripción de la tienda.":::

#### <a name="best-practices-for-short-descriptions"></a><span data-ttu-id="760b3-129">Procedimientos recomendados para descripciones breves</span><span class="sxs-lookup"><span data-stu-id="760b3-129">Best practices for short descriptions</span></span>

<span data-ttu-id="760b3-130">**Sí:**</span><span class="sxs-lookup"><span data-stu-id="760b3-130">**Do:**</span></span>

* <span data-ttu-id="760b3-131">Coloque primero la información más importante.</span><span class="sxs-lookup"><span data-stu-id="760b3-131">Put the most important information first.</span></span>
* <span data-ttu-id="760b3-132">Incluir palabras clave que es probable que los clientes busquen.</span><span class="sxs-lookup"><span data-stu-id="760b3-132">Include keywords that customers are likely to search for.</span></span>

<span data-ttu-id="760b3-133">**No:**</span><span class="sxs-lookup"><span data-stu-id="760b3-133">**Don't:**</span></span>

* <span data-ttu-id="760b3-134">Repita el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="760b3-134">Repeat your app name.</span></span>
* <span data-ttu-id="760b3-135">Dependa de la jerga o terminología especializada.</span><span class="sxs-lookup"><span data-stu-id="760b3-135">Rely on jargon or specialized terminology.</span></span> <span data-ttu-id="760b3-136">(No puede asumir que los usuarios saben qué buscar).</span><span class="sxs-lookup"><span data-stu-id="760b3-136">(You can't assume users know what to look for.)</span></span>

### <a name="long-description"></a><span data-ttu-id="760b3-137">La descripción larga</span><span class="sxs-lookup"><span data-stu-id="760b3-137">Long description</span></span>

<span data-ttu-id="760b3-138">La descripción larga puede proporcionar una narrativa atractiva que resalta las características principales de la aplicación, los problemas que resuelve y su audiencia de destino.</span><span class="sxs-lookup"><span data-stu-id="760b3-138">The long description can provide an engaging narrative that highlights your app's main features, the problems it solves, and its target audience.</span></span> <span data-ttu-id="760b3-139">Aunque esta descripción puede tener hasta 4000 caracteres, la mayoría de los usuarios solo leerán entre 300 y 500 palabras.</span><span class="sxs-lookup"><span data-stu-id="760b3-139">While this description can be as long as 4000 characters, most users will only read between 300-500 words.</span></span>

<span data-ttu-id="760b3-140">En el ejemplo siguiente se resalta dónde se muestra la descripción larga de una aplicación en una descripción de la tienda:</span><span class="sxs-lookup"><span data-stu-id="760b3-140">The following example highlights where an app's long description displays in a store listing:</span></span>

:::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="Destaca la captura de pantalla de ejemplo donde se muestra la descripción larga de una aplicación en una descripción de la tienda.":::

#### <a name="usage-examples"></a><span data-ttu-id="760b3-142">Ejemplos de uso</span><span class="sxs-lookup"><span data-stu-id="760b3-142">Usage examples</span></span>

<span data-ttu-id="760b3-143">Las siguientes frases son ejemplos de lo que se permite al escribir descripciones largas:</span><span class="sxs-lookup"><span data-stu-id="760b3-143">The following phrases are examples of what's allowed when writing long descriptions:</span></span>

* <span data-ttu-id="760b3-144">"<El *nombre de la* aplicación> funciona con Microsoft Teams"</span><span class="sxs-lookup"><span data-stu-id="760b3-144">"<*Your app name*> works with Microsoft Teams"</span></span>
* <span data-ttu-id="760b3-145">"... un <*de aplicación>* para Microsoft Teams"</span><span class="sxs-lookup"><span data-stu-id="760b3-145">"... a <*type of app*> for Microsoft Teams"</span></span>
* <span data-ttu-id="760b3-146">"<el *nombre de la* aplicación> se integra con Microsoft Teams"</span><span class="sxs-lookup"><span data-stu-id="760b3-146">"<*Your app name*> integrates with Microsoft Teams"</span></span>
* <span data-ttu-id="760b3-147">"... integrado con Microsoft Teams"</span><span class="sxs-lookup"><span data-stu-id="760b3-147">"... integrated with Microsoft Teams"</span></span>
* <span data-ttu-id="760b3-148">"... para usuarios que trabajan con Microsoft Teams"</span><span class="sxs-lookup"><span data-stu-id="760b3-148">"... for users working with Microsoft Teams"</span></span>
* <span data-ttu-id="760b3-149">"... para <*tareas específicas>* dentro de Microsoft Teams"</span><span class="sxs-lookup"><span data-stu-id="760b3-149">"... for <*specific task*> within Microsoft Teams"</span></span>
* <span data-ttu-id="760b3-150">"... basado en ..."</span><span class="sxs-lookup"><span data-stu-id="760b3-150">"... built on ..."</span></span>
* <span data-ttu-id="760b3-151">"... se ejecuta en ..."</span><span class="sxs-lookup"><span data-stu-id="760b3-151">"... runs on ..."</span></span>
* <span data-ttu-id="760b3-152">"... habilitado por ..."</span><span class="sxs-lookup"><span data-stu-id="760b3-152">"... enabled by ..."</span></span>
* <span data-ttu-id="760b3-153">"... desarrollado para ..."</span><span class="sxs-lookup"><span data-stu-id="760b3-153">"... developed for ..."</span></span>
* <span data-ttu-id="760b3-154">"... diseñado para ..."</span><span class="sxs-lookup"><span data-stu-id="760b3-154">"... designed for ..."</span></span>

#### <a name="best-practices-for-long-descriptions"></a><span data-ttu-id="760b3-155">Procedimientos recomendados para descripciones largas</span><span class="sxs-lookup"><span data-stu-id="760b3-155">Best practices for long descriptions</span></span>

<span data-ttu-id="760b3-156">**Sí:**</span><span class="sxs-lookup"><span data-stu-id="760b3-156">**Do:**</span></span>

* <span data-ttu-id="760b3-157">Use [Markdown para](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) dar formato a la descripción.</span><span class="sxs-lookup"><span data-stu-id="760b3-157">Use [Markdown](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) to format your description.</span></span>
* <span data-ttu-id="760b3-158">Enumera las características con puntos de viñeta para que sea más fácil examinar la descripción.</span><span class="sxs-lookup"><span data-stu-id="760b3-158">List features with bullet points so it's easier to scan the description.</span></span>
* <span data-ttu-id="760b3-159">Use voz activa y hable directamente con los usuarios (por ejemplo, *Puede ...*).</span><span class="sxs-lookup"><span data-stu-id="760b3-159">Use active voice and speak to users directly (for example, *You can ...*).</span></span>
* <span data-ttu-id="760b3-160">Incluye un vínculo de ayuda o soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="760b3-160">Include a help or support link.</span></span>
* <span data-ttu-id="760b3-161">Identifique lo siguiente si procede: limitaciones, configurar información, dependencias de cuenta y actualizaciones de versiones.</span><span class="sxs-lookup"><span data-stu-id="760b3-161">Identify the following if applicable: limitations, set up information, account dependencies, and release updates.</span></span>

<span data-ttu-id="760b3-162">**No:**</span><span class="sxs-lookup"><span data-stu-id="760b3-162">**Don't:**</span></span>

* <span data-ttu-id="760b3-163">Supere las 500 palabras.</span><span class="sxs-lookup"><span data-stu-id="760b3-163">Exceed 500 words.</span></span>
* <span data-ttu-id="760b3-164">Incluir demasiadas palabras clave.</span><span class="sxs-lookup"><span data-stu-id="760b3-164">Include too many keywords.</span></span> <span data-ttu-id="760b3-165">(Es una distracción y no ayuda a los usuarios a encontrar la aplicación).</span><span class="sxs-lookup"><span data-stu-id="760b3-165">(It's distracting and won't help people find your app.)</span></span>
* <span data-ttu-id="760b3-166">Usa el siguiente idioma a menos que la aplicación haya pasado por un proceso de certificación oficial:</span><span class="sxs-lookup"><span data-stu-id="760b3-166">Use the following language unless the app has gone through an official certification process:</span></span>
  * <span data-ttu-id="760b3-167">"... certificado para ..."</span><span class="sxs-lookup"><span data-stu-id="760b3-167">"... certified for ..."</span></span>
  * <span data-ttu-id="760b3-168">" ... powered by ..."</span><span class="sxs-lookup"><span data-stu-id="760b3-168">" ... powered by ..."</span></span>

### <a name="best-practices-for-all-descriptions"></a><span data-ttu-id="760b3-169">Procedimientos recomendados para todas las descripciones</span><span class="sxs-lookup"><span data-stu-id="760b3-169">Best practices for all descriptions</span></span>

<span data-ttu-id="760b3-170">**Sí:**</span><span class="sxs-lookup"><span data-stu-id="760b3-170">**Do:**</span></span>

* <span data-ttu-id="760b3-171">Haga referencia a nombres de productos de Microsoft solo cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="760b3-171">Reference Microsoft product names only when necessary.</span></span> <span data-ttu-id="760b3-172">Para obtener más información sobre las directrices, consulte [Directrices de marca y marca de Microsoft](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general).</span><span class="sxs-lookup"><span data-stu-id="760b3-172">For more information on the guidelines, see [Microsoft Trademark and Brand Guidelines](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general).</span></span>
* <span data-ttu-id="760b3-173">Si necesita hacer referencia a **Teams**, escriba la primera referencia como **Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="760b3-173">If you need to reference **Teams**, write the first reference as **Microsoft Teams**.</span></span> <span data-ttu-id="760b3-174">Las referencias posteriores se pueden acortar **a Teams**.</span><span class="sxs-lookup"><span data-stu-id="760b3-174">Subsequent references can be shortened to **Teams**.</span></span>
* <span data-ttu-id="760b3-175">Consulte **Microsoft 365** en lugar de **Office 365**.</span><span class="sxs-lookup"><span data-stu-id="760b3-175">Refer to **Microsoft 365** instead of **Office 365**.</span></span>
* <span data-ttu-id="760b3-176">Evite errores ortográficos y gramaticales.</span><span class="sxs-lookup"><span data-stu-id="760b3-176">Avoid typos and grammatical errors.</span></span>
* <span data-ttu-id="760b3-177">Evite mayúsculas innecesarias (por ejemplo, **Usuarios** en lugar de **usuarios**).</span><span class="sxs-lookup"><span data-stu-id="760b3-177">Avoid unnecessary capitalizations (for example, **Users** instead of **users**).</span></span>
* <span data-ttu-id="760b3-178">Evite los acrónimos.</span><span class="sxs-lookup"><span data-stu-id="760b3-178">Avoid acronyms.</span></span>

<span data-ttu-id="760b3-179">**No:**</span><span class="sxs-lookup"><span data-stu-id="760b3-179">**Don't:**</span></span>

* <span data-ttu-id="760b3-180">Abreviar Microsoft como **MS** o **MSFT**.</span><span class="sxs-lookup"><span data-stu-id="760b3-180">Abbreviate Microsoft as **MS** or **MSFT**.</span></span>
* <span data-ttu-id="760b3-181">Indica que la aplicación es una oferta de Microsoft, incluido el uso de lemas o lemas de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="760b3-181">Indicate the app is an offering from Microsoft, including using Microsoft slogans or taglines.</span></span>
* <span data-ttu-id="760b3-182">Usa nombres de marca con derechos de autor que no posees.</span><span class="sxs-lookup"><span data-stu-id="760b3-182">Use copyrighted brand names you don't own.</span></span>

## <a name="adhere-to-icon-design-guidelines"></a><span data-ttu-id="760b3-183">Cumplir las directrices de diseño de iconos</span><span class="sxs-lookup"><span data-stu-id="760b3-183">Adhere to icon design guidelines</span></span>

<span data-ttu-id="760b3-184">Los iconos son uno de los elementos principales que los usuarios ven al navegar por la tienda.</span><span class="sxs-lookup"><span data-stu-id="760b3-184">Icons are one of the main elements users see when browsing the store.</span></span> <span data-ttu-id="760b3-185">Los iconos deben comunicar el propósito de la marca de la aplicación a la vez que se adhieren a Teams requisitos.</span><span class="sxs-lookup"><span data-stu-id="760b3-185">Your icons should communicate your app's brand purpose while also adhering to Teams requirements.</span></span>

<span data-ttu-id="760b3-186">Para obtener más información, [consulta instrucciones específicas sobre cómo diseñar Teams iconos de la aplicación](~/concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="760b3-186">For more information, see [specific guidance on designing Teams app icons](~/concepts/build-and-test/apps-package.md#app-icons).</span></span>

## <a name="capture-screenshots"></a><span data-ttu-id="760b3-187">Capturar capturas de pantalla</span><span class="sxs-lookup"><span data-stu-id="760b3-187">Capture screenshots</span></span>

<span data-ttu-id="760b3-188">Las capturas de pantalla proporcionan una vista previa visual destacada de la aplicación para complementar el nombre, el icono y las descripciones de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="760b3-188">Screenshots provide a prominent visual preview of your app to complement your app name, icon, and descriptions.</span></span>

### <a name="requirements-for-screenshots"></a><span data-ttu-id="760b3-189">Requisitos para capturas de pantalla</span><span class="sxs-lookup"><span data-stu-id="760b3-189">Requirements for screenshots</span></span>

* <span data-ttu-id="760b3-190">Hasta cinco capturas de pantalla por descripción.</span><span class="sxs-lookup"><span data-stu-id="760b3-190">Up to five screenshots per listing.</span></span>
* <span data-ttu-id="760b3-191">Los tipos de archivo admitidos incluyen PNG, JPEG y GIF.</span><span class="sxs-lookup"><span data-stu-id="760b3-191">Supported file types include PNG, JPEG, and GIF.</span></span>
* <span data-ttu-id="760b3-192">Las dimensiones deben ser de 1366 x 768 píxeles.</span><span class="sxs-lookup"><span data-stu-id="760b3-192">Dimensions should be 1366x768 pixels.</span></span>
* <span data-ttu-id="760b3-193">Tamaño máximo de 1.024 KB.</span><span class="sxs-lookup"><span data-stu-id="760b3-193">Maximum size of 1,024 KB.</span></span>

### <a name="best-practices-for-screenshots"></a><span data-ttu-id="760b3-194">Procedimientos recomendados para capturas de pantalla</span><span class="sxs-lookup"><span data-stu-id="760b3-194">Best practices for screenshots</span></span>

<span data-ttu-id="760b3-195">**Sí:**</span><span class="sxs-lookup"><span data-stu-id="760b3-195">**Do:**</span></span>

* <span data-ttu-id="760b3-196">Céntrate en las capacidades de la aplicación (por ejemplo, cómo las personas pueden comunicarse con el bot).</span><span class="sxs-lookup"><span data-stu-id="760b3-196">Focus on your app's capabilities (for example, how people can communicate with your bot).</span></span>
* <span data-ttu-id="760b3-197">Incluye contenido que represente con precisión la aplicación.</span><span class="sxs-lookup"><span data-stu-id="760b3-197">Include content that accurately represents your app.</span></span>
* <span data-ttu-id="760b3-198">Use el texto con juicio.</span><span class="sxs-lookup"><span data-stu-id="760b3-198">Use text judiciously.</span></span>
* Capturas de pantalla de fotogramas con un color que refleje su marca e incluya contenido de marketing, similar al siguiente ejemplo de [Freshdesk](https://appsource.microsoft.com/product/office/WA104381505?src=office&tab=Overview) (los requisitos de dimensión se aplican a toda la imagen y no solo a la captura de pantalla): ejemplo de captura de pantalla de :::image type="content" source="../../../../assets/images/freshdesk.png" alt-text="Freshdesk"::: de aplicaciones de terceros

<span data-ttu-id="760b3-200">**No:**</span><span class="sxs-lookup"><span data-stu-id="760b3-200">**Don't:**</span></span>

* <span data-ttu-id="760b3-201">Mostrar dispositivos específicos, como teléfonos o portátiles.</span><span class="sxs-lookup"><span data-stu-id="760b3-201">Show specific devices, such as phones or laptops.</span></span>
* <span data-ttu-id="760b3-202">Muestra cromo o interfaz de usuario que no esté en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="760b3-202">Display chrome or UI that isn't in your app.</span></span>
* <span data-ttu-id="760b3-203">Captura cualquier Teams o interfaz de usuario del explorador en las capturas de pantalla.</span><span class="sxs-lookup"><span data-stu-id="760b3-203">Capture any Teams or browser UI in your screenshots.</span></span>
* <span data-ttu-id="760b3-204">Incluye mockups que reflejen inexactamente la interfaz de usuario real de la aplicación, como mostrar la aplicación en un explorador en lugar de una Teams pestaña.</span><span class="sxs-lookup"><span data-stu-id="760b3-204">Include mockups that inaccurately reflect your app's actual UI, such as showing your app in  a browser instead of a Teams tab.</span></span>

<span data-ttu-id="760b3-205">Para obtener más prácticas recomendadas, consulta [Crear imágenes eficaces para las tiendas de aplicaciones de Microsoft.](/office/dev/store/craft-effective-appsource-store-images)</span><span class="sxs-lookup"><span data-stu-id="760b3-205">For more best practices, see [craft effective images for Microsoft app stores](/office/dev/store/craft-effective-appsource-store-images).</span></span>

## <a name="create-a-video"></a><span data-ttu-id="760b3-206">Crear un vídeo</span><span class="sxs-lookup"><span data-stu-id="760b3-206">Create a video</span></span>

<span data-ttu-id="760b3-207">Un vídeo puede ser la forma más eficaz de comunicar por qué las personas deben usar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="760b3-207">A video can be the most effective way to communicate why people should use your app.</span></span> <span data-ttu-id="760b3-208">Debe abordar las siguientes preguntas en un vídeo:</span><span class="sxs-lookup"><span data-stu-id="760b3-208">You should address the following questions in a video:</span></span>

* <span data-ttu-id="760b3-209">Quién Cuál es tu aplicación?</span><span class="sxs-lookup"><span data-stu-id="760b3-209">Who is your app for?</span></span>
* <span data-ttu-id="760b3-210">¿Qué problemas puede resolver la aplicación?</span><span class="sxs-lookup"><span data-stu-id="760b3-210">What problems can your app solve?</span></span>
* <span data-ttu-id="760b3-211">¿Cómo funciona la aplicación?</span><span class="sxs-lookup"><span data-stu-id="760b3-211">How does your app work?</span></span>
* <span data-ttu-id="760b3-212">¿Qué otras ventajas obtienes al usar la aplicación?</span><span class="sxs-lookup"><span data-stu-id="760b3-212">What other benefits do you get from using your app?</span></span>

<span data-ttu-id="760b3-213">Si incluyes un vídeo, aparecerá antes de las capturas de pantalla en la descripción.</span><span class="sxs-lookup"><span data-stu-id="760b3-213">If you include a video, it appears before your screenshots in the listing.</span></span>

### <a name="best-practices-for-videos"></a><span data-ttu-id="760b3-214">Procedimientos recomendados para vídeos</span><span class="sxs-lookup"><span data-stu-id="760b3-214">Best practices for videos</span></span>

* <span data-ttu-id="760b3-215">Mantén el vídeo entre 30 y 90 segundos.</span><span class="sxs-lookup"><span data-stu-id="760b3-215">Keep your video between 30-90 seconds.</span></span>
* <span data-ttu-id="760b3-216">Apunta a la calidad.</span><span class="sxs-lookup"><span data-stu-id="760b3-216">Aim for quality.</span></span> <span data-ttu-id="760b3-217">En una descripción, los usuarios verán el vídeo antes de las capturas de pantalla.</span><span class="sxs-lookup"><span data-stu-id="760b3-217">In a listing, users will see your video before screenshots.</span></span>

## <a name="localize-your-store-listing"></a><span data-ttu-id="760b3-218">Localización de la descripción de la tienda</span><span class="sxs-lookup"><span data-stu-id="760b3-218">Localize your store listing</span></span>

<span data-ttu-id="760b3-219">El Centro de partners admite [listados de almacenes localizados.](https://docs.microsoft.com/office/dev/store/prepare-localized-solutions)</span><span class="sxs-lookup"><span data-stu-id="760b3-219">Partner Center supports [localized store listings](https://docs.microsoft.com/office/dev/store/prepare-localized-solutions).</span></span> <span data-ttu-id="760b3-220">Para obtener más información, [consulta cómo encontrar la descripción](../../../../concepts/build-and-test/apps-localization.md)Teams aplicación .</span><span class="sxs-lookup"><span data-stu-id="760b3-220">For more information, see [how to localize your Teams app listing](../../../../concepts/build-and-test/apps-localization.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="760b3-221">Vea también</span><span class="sxs-lookup"><span data-stu-id="760b3-221">See also</span></span>

* [<span data-ttu-id="760b3-222">Crear listas Microsoft 365 almacenes eficaces</span><span class="sxs-lookup"><span data-stu-id="760b3-222">Create effective Microsoft 365 Stores listings</span></span>](/office/dev/store/create-effective-office-store-listings)
* <span data-ttu-id="760b3-223">Teams de diseño de aplicaciones para [copiar y contenido y](~/concepts/design/design-teams-app-fundamentals.md#copy-and-content) expresión de [marca](~/concepts/design/design-teams-app-fundamentals.md#brand-expression)</span><span class="sxs-lookup"><span data-stu-id="760b3-223">Teams app design guidelines for [copy and content](~/concepts/design/design-teams-app-fundamentals.md#copy-and-content) and [brand expression](~/concepts/design/design-teams-app-fundamentals.md#brand-expression)</span></span>
* [<span data-ttu-id="760b3-224">Directrices de marca y marca de Microsoft</span><span class="sxs-lookup"><span data-stu-id="760b3-224">Microsoft Trademark and Brand Guidelines</span></span>](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general)

## <a name="next-step"></a><span data-ttu-id="760b3-225">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="760b3-225">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="760b3-226">Preparar el envío de la tienda</span><span class="sxs-lookup"><span data-stu-id="760b3-226">Prepare your store submission</span></span>](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)

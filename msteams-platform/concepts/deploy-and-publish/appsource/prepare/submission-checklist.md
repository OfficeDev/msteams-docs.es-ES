---
title: Preparar el envío de la tienda
description: Describe los pasos finales antes de enviar la aplicación Microsoft Teams que aparecerá en la tienda.
ms.topic: how-to
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 975d3ef8fc8bdc8d6d7c336cf3a61a3a42ef5315
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566036"
---
# <a name="prepare-your-microsoft-teams-store-submission"></a><span data-ttu-id="c0ec9-103">Prepare el envío de su tienda Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c0ec9-103">Prepare your Microsoft Teams store submission</span></span>

<span data-ttu-id="c0ec9-104">Ha diseñado, creado y probado su aplicación Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-104">You've designed, built, and tested your Microsoft Teams app.</span></span> <span data-ttu-id="c0ec9-105">Ahora estás listo para enumerarlo para que la gente pueda descubrirlo y empezar a usar tu aplicación.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-105">Now you're ready to list it so people can discover and start using your app.</span></span>

<span data-ttu-id="c0ec9-106">Antes de enviar la aplicación al [Centro de partners,](/office/dev/store/use-partner-center-to-submit-to-appsource)asegúrate de haber hecho lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-106">Before you submit your app to [Partner Center](/office/dev/store/use-partner-center-to-submit-to-appsource), make sure you've done the following.</span></span>

## <a name="validate-your-app-package"></a><span data-ttu-id="c0ec9-107">Valida el paquete de la aplicación</span><span class="sxs-lookup"><span data-stu-id="c0ec9-107">Validate your app package</span></span>

<span data-ttu-id="c0ec9-108">Aunque la aplicación puede estar funcionando en un entorno de prueba, debe comprobar el paquete de la aplicación para evitar tener problemas durante el proceso de envío.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-108">While your app may be working in a test environment, you should check your app package to avoid running into issues during the submission process.</span></span>

<span data-ttu-id="c0ec9-109">La herramienta de validación de aplicaciones Microsoft Teams le ayuda a identificar y solucionar problemas antes de enviarla al Centro de partners.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-109">The Microsoft Teams app validation tool helps you identify and fix issues before submitting to Partner Center.</span></span> <span data-ttu-id="c0ec9-110">La herramienta comprueba automáticamente las configuraciones de la aplicación con los mismos casos de prueba utilizados durante la validación de la tienda.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-110">The tool automatically checks your app's configurations against the same test cases used during store validation.</span></span>

1. <span data-ttu-id="c0ec9-111">Vaya a la [herramienta de validación de aplicaciones Microsoft Teams](https://dev.teams.microsoft.com/appvalidation.html).</span><span class="sxs-lookup"><span data-stu-id="c0ec9-111">Go to the [Microsoft Teams app validation tool](https://dev.teams.microsoft.com/appvalidation.html).</span></span> <span data-ttu-id="c0ec9-112">(Nota: La herramienta también está disponible en [App Studio](../../../build-and-test/app-studio-overview.md).)</span><span class="sxs-lookup"><span data-stu-id="c0ec9-112">(Note: The tool is also available in [App Studio](../../../build-and-test/app-studio-overview.md).)</span></span>
1. <span data-ttu-id="c0ec9-113">Upload el paquete de la aplicación para ejecutar las pruebas automatizadas.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-113">Upload your app package to run the automated tests.</span></span>
1. <span data-ttu-id="c0ec9-114">Vaya a la **lista de verificación preliminar** y revise los casos de prueba que son difíciles de automatizar.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-114">Go to the **Preliminary checklist** and review the test cases that are difficult to automate.</span></span>
1. <span data-ttu-id="c0ec9-115">[Corrija problemas con sus configuraciones](~/resources/schema/manifest-schema.md) o aplicación en general si las pruebas automatizadas le dan errores o no ha cumplido todos los criterios de la lista de comprobación.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-115">[Fix issues with your configurations](~/resources/schema/manifest-schema.md) or app in general if the automated tests give you errors or you haven't met all the criteria in the checklist.</span></span>

## <a name="compile-testing-instructions"></a><span data-ttu-id="c0ec9-116">Compilar instrucciones de prueba</span><span class="sxs-lookup"><span data-stu-id="c0ec9-116">Compile testing instructions</span></span>

<span data-ttu-id="c0ec9-117">Proporcione instrucciones y recursos para ayudar a los revisores a probar la aplicación, incluidas las cuentas de prueba, las credenciales y las claves de licencia.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-117">Provide instructions and resources to help the reviewers test your app, including test accounts, credentials, and license keys.</span></span> <span data-ttu-id="c0ec9-118">Puede agregar instrucciones en el Centro de partners o cargarlas en una ubicación disponible públicamente en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-118">You can add instructions in Partner Center or upload them to a publicly available location on SharePoint.</span></span>

### <a name="feature-list"></a><span data-ttu-id="c0ec9-119">Lista de características</span><span class="sxs-lookup"><span data-stu-id="c0ec9-119">Feature list</span></span>

<span data-ttu-id="c0ec9-120">Proporcione detalles sobre las capacidades de la aplicación en Teams y los pasos para probar cada una de ellas.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-120">Provide details about your app's capabilities in Teams and steps for testing each one.</span></span>

### <a name="accounts"></a><span data-ttu-id="c0ec9-121">Cuentas</span><span class="sxs-lookup"><span data-stu-id="c0ec9-121">Accounts</span></span>

<span data-ttu-id="c0ec9-122">Debe proporcionar cuentas de prueba si la aplicación requiere una licencia o una lista segura de back-end.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-122">You must provide test accounts if your app requires a license or backend safelisting.</span></span> <span data-ttu-id="c0ec9-123">Todas las cuentas que proporcione deben incluir datos rellenados previamente para facilitar las pruebas.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-123">All accounts you provide must include pre-populated data to facilitate testing.</span></span>

<span data-ttu-id="c0ec9-124">Dependiendo de las características de la aplicación, es posible que deba proporcionar todo lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c0ec9-124">Depending on your app's features, you may need to provide all of the following:</span></span>

* <span data-ttu-id="c0ec9-125">Cuenta de administrador (obligatorio)</span><span class="sxs-lookup"><span data-stu-id="c0ec9-125">Admin account (required)</span></span>
* <span data-ttu-id="c0ec9-126">Cuenta no administrativa (obligatorio)</span><span class="sxs-lookup"><span data-stu-id="c0ec9-126">Non-admin account (required)</span></span>
* <span data-ttu-id="c0ec9-127">Una cuenta que no está preconfigurada para probar correctamente la experiencia de inicio de sesión de la primera ejecución (necesaria)</span><span class="sxs-lookup"><span data-stu-id="c0ec9-127">An account that isn't pre-configured in order to properly test the first-run sign-in experience (required)</span></span>
* <span data-ttu-id="c0ec9-128">Una cuenta con acceso a funciones premium o actualizadas (si corresponde)</span><span class="sxs-lookup"><span data-stu-id="c0ec9-128">An account with access to premium or upgraded features (if applicable)</span></span>
* <span data-ttu-id="c0ec9-129">Dos cuentas del mismo inquilino para probar la experiencia de colaboración de las aplicaciones que funcionan en contextos compartidos (si corresponde)</span><span class="sxs-lookup"><span data-stu-id="c0ec9-129">Two accounts in the same tenant to test the collaboration experience for apps that work in shared contexts (if applicable)</span></span>

### <a name="tenant-configurations"></a><span data-ttu-id="c0ec9-130">Configuraciones de inquilinos</span><span class="sxs-lookup"><span data-stu-id="c0ec9-130">Tenant configurations</span></span>

<span data-ttu-id="c0ec9-131">Si debe configurar un inquilino Teams para usar la aplicación, incluya esas instrucciones y cuentas de administrador y no administrador para la validación.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-131">If you must configure a Teams tenant to use your app, include those instructions and admin and non-admin accounts for validation.</span></span>

### <a name="video-optional"></a><span data-ttu-id="c0ec9-132">Vídeo (opcional)</span><span class="sxs-lookup"><span data-stu-id="c0ec9-132">Video (optional)</span></span>

<span data-ttu-id="c0ec9-133">Proporcione una grabación de la aplicación para que Microsoft pueda comprender completamente su funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-133">Provide a recording of your app so that Microsoft can fully understand its functionality.</span></span>

## <a name="create-your-store-listing-details"></a><span data-ttu-id="c0ec9-134">Crea los detalles de tu tienda</span><span class="sxs-lookup"><span data-stu-id="c0ec9-134">Create your store listing details</span></span>

<span data-ttu-id="c0ec9-135">La información que envías al [Centro de partners](https://partner.microsoft.com)&#8212;incluido tu nombre, descripciones, iconos e imágenes&#8212;se convierte en la tienda Teams y la lista de Microsoft AppSource para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-135">The information that you submit to [Partner Center](https://partner.microsoft.com)&#8212;including your name, descriptions, icons, and images&#8212;becomes the Teams store and Microsoft AppSource listing for your app.</span></span>

<span data-ttu-id="c0ec9-136">Un anuncio de tienda puede ser la primera impresión de alguien de tu aplicación.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-136">A store listing may be someone's first impression of your app.</span></span> <span data-ttu-id="c0ec9-137">Aumente las instalaciones con un listado que transmita eficazmente los beneficios, la funcionalidad y la marca de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-137">Increase installations with a listing that effectively conveys your app's benefits, functionality, and brand.</span></span>

### <a name="specify-a-short-name"></a><span data-ttu-id="c0ec9-138">Especifique un nombre corto</span><span class="sxs-lookup"><span data-stu-id="c0ec9-138">Specify a short name</span></span>

<span data-ttu-id="c0ec9-139">El nombre de la aplicación (específicamente, su [*nombre corto)*](~/resources/schema/manifest-schema.md#name)juega un papel crucial en la forma en que los usuarios la descubren en la tienda.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-139">Your app's name (specifically, its [*short name*](~/resources/schema/manifest-schema.md#name)) plays a crucial role in how users discover it in the store.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="La captura de pantalla de ejemplo resalta dónde se muestra el nombre corto de una aplicación en un listado de tienda.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="c0ec9-141">Asegúrese de que su nombre corto se adhiere a las directrices de validación de la [tienda.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#11-app-name)</span><span class="sxs-lookup"><span data-stu-id="c0ec9-141">Make sure your short name adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#11-app-name).</span></span>

### <a name="write-descriptions"></a><span data-ttu-id="c0ec9-142">Escribir descripciones</span><span class="sxs-lookup"><span data-stu-id="c0ec9-142">Write descriptions</span></span>

<span data-ttu-id="c0ec9-143">Debe tener una descripción corta y larga de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-143">You must have a short and long description of your app.</span></span>

#### <a name="short-description"></a><span data-ttu-id="c0ec9-144">La descripción breve</span><span class="sxs-lookup"><span data-stu-id="c0ec9-144">Short description</span></span>

<span data-ttu-id="c0ec9-145">Un resumen conciso de la aplicación que debe ser original, atractivo y dirigido a su público objetivo.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-145">A concise summary of your app that should be original, engaging, and directed at your target audience.</span></span> <span data-ttu-id="c0ec9-146">Mantenga la breve descripción en una oración.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-146">Keep the short description to one sentence.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="La captura de pantalla del ejemplo resalta dónde se muestra la breve descripción de una aplicación en una lista de la tienda.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="c0ec9-148">Asegúrese de que la breve descripción se adhiere a las directrices de validación de la [tienda.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#431-short-description)</span><span class="sxs-lookup"><span data-stu-id="c0ec9-148">Make sure your short description adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#431-short-description).</span></span>

#### <a name="long-description"></a><span data-ttu-id="c0ec9-149">La descripción larga</span><span class="sxs-lookup"><span data-stu-id="c0ec9-149">Long description</span></span>

<span data-ttu-id="c0ec9-150">La descripción larga puede proporcionar una narrativa que resalta las principales características de la aplicación, los problemas que resuelve y su público objetivo.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-150">The long description can provide a narrative that highlights your app's main features, the problems it solves, and its target audience.</span></span> <span data-ttu-id="c0ec9-151">Aunque esta descripción puede tener hasta 4.000 caracteres, la mayoría de los usuarios solo leerán entre 300 y 500 palabras.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-151">While this description can be as long as 4,000 characters, most users will only read between 300-500 words.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/LongDescription-02.png" alt-text="La captura de pantalla de ejemplo resalta dónde se muestra la descripción larga de una aplicación en un listado de tienda.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="c0ec9-153">Asegúrese de que la descripción larga se adhiere a las directrices de validación de la [tienda.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#432-long-description)</span><span class="sxs-lookup"><span data-stu-id="c0ec9-153">Make sure your long description adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#432-long-description).</span></span>

### <a name="adhere-to-icon-design-guidelines"></a><span data-ttu-id="c0ec9-154">Cumplir con las directrices de diseño de iconos</span><span class="sxs-lookup"><span data-stu-id="c0ec9-154">Adhere to icon design guidelines</span></span>

<span data-ttu-id="c0ec9-155">Los iconos son uno de los principales elementos que los usuarios ven al navegar por la tienda.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-155">Icons are one of the main elements users see when browsing the store.</span></span> <span data-ttu-id="c0ec9-156">Los iconos deben comunicar la marca y el propósito de la aplicación, al tiempo que se adhieren a los requisitos Teams.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-156">Your icons should communicate your app's brand and purpose while also adhering to Teams requirements.</span></span>

<span data-ttu-id="c0ec9-157">Para obtener más información, consulte [instrucciones sobre cómo crear iconos de Teams aplicación.](~/concepts/build-and-test/apps-package.md#app-icons)</span><span class="sxs-lookup"><span data-stu-id="c0ec9-157">For more information, see [guidance on creating Teams app icons](~/concepts/build-and-test/apps-package.md#app-icons).</span></span>

### <a name="capture-screenshots"></a><span data-ttu-id="c0ec9-158">Captura de pantalla de capturas de pantalla</span><span class="sxs-lookup"><span data-stu-id="c0ec9-158">Capture screenshots</span></span>

<span data-ttu-id="c0ec9-159">Las capturas de pantalla proporcionan una vista previa visual destacada de la aplicación para complementar el nombre, el icono y las descripciones de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-159">Screenshots provide a prominent visual preview of your app to complement your app name, icon, and descriptions.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/Screenshot-01.png" alt-text="Ejemplo de captura de pantalla resalta dónde se muestran las capturas de pantalla de la aplicación en un listado de la tienda.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="c0ec9-161">Recuerde lo siguiente acerca de las capturas de pantalla:</span><span class="sxs-lookup"><span data-stu-id="c0ec9-161">Remember the following about screenshots:</span></span>

* <span data-ttu-id="c0ec9-162">Puede tener hasta cinco capturas de pantalla por anuncio.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-162">You can have up to five screenshots per listing.</span></span>
* <span data-ttu-id="c0ec9-163">Los tipos de archivo compatibles incluyen PNG, JPEG y GIF.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-163">Supported file types include PNG, JPEG, and GIF.</span></span>
* <span data-ttu-id="c0ec9-164">Las dimensiones deben ser de 1366x768 píxeles.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-164">Dimensions should be 1366x768 pixels.</span></span>
* <span data-ttu-id="c0ec9-165">Tamaño máximo de 1.024 KB.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-165">Maximum size of 1,024 KB.</span></span>

<span data-ttu-id="c0ec9-166">Para obtener las prácticas recomendadas, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="c0ec9-166">For best practices, see the following resources:</span></span>

* [<span data-ttu-id="c0ec9-167">Teams las directrices de validación de la tienda</span><span class="sxs-lookup"><span data-stu-id="c0ec9-167">Teams store validation guidelines</span></span>](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#44-screenshots)
* [<span data-ttu-id="c0ec9-168">Crear imágenes eficaces para las tiendas de aplicaciones de Microsoft</span><span class="sxs-lookup"><span data-stu-id="c0ec9-168">Craft effective images for Microsoft app stores</span></span>](/office/dev/store/craft-effective-appsource-store-images)

### <a name="create-a-video"></a><span data-ttu-id="c0ec9-169">Crear un vídeo</span><span class="sxs-lookup"><span data-stu-id="c0ec9-169">Create a video</span></span>

<span data-ttu-id="c0ec9-170">Un vídeo de tu anuncio puede ser la forma más eficaz de comunicar por qué las personas deben usar tu aplicación.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-170">A video in your listing can be the most effective way to communicate why people should use your app.</span></span> <span data-ttu-id="c0ec9-171">Debe abordar las siguientes preguntas en un vídeo:</span><span class="sxs-lookup"><span data-stu-id="c0ec9-171">You should address the following questions in a video:</span></span>

* <span data-ttu-id="c0ec9-172">Quién es su aplicación para?</span><span class="sxs-lookup"><span data-stu-id="c0ec9-172">Who is your app for?</span></span>
* <span data-ttu-id="c0ec9-173">¿Qué problemas puede resolver la aplicación?</span><span class="sxs-lookup"><span data-stu-id="c0ec9-173">What problems can your app solve?</span></span>
* <span data-ttu-id="c0ec9-174">¿Cómo funciona la aplicación?</span><span class="sxs-lookup"><span data-stu-id="c0ec9-174">How does your app work?</span></span>
* <span data-ttu-id="c0ec9-175">¿Qué otros beneficios obtienes al usar tu aplicación?</span><span class="sxs-lookup"><span data-stu-id="c0ec9-175">What other benefits do you get from using your app?</span></span>

#### <a name="best-practices-for-videos"></a><span data-ttu-id="c0ec9-176">Mejores prácticas para vídeos</span><span class="sxs-lookup"><span data-stu-id="c0ec9-176">Best practices for videos</span></span>

* <span data-ttu-id="c0ec9-177">Mantén tu vídeo entre 30 y 90 segundos.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-177">Keep your video between 30-90 seconds.</span></span>
* <span data-ttu-id="c0ec9-178">Apunta a la calidad.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-178">Aim for quality.</span></span> <span data-ttu-id="c0ec9-179">En un anuncio, los usuarios verán el vídeo antes de las capturas de pantalla.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-179">In a listing, users will see your video before screenshots.</span></span>

### <a name="select-a-category-for-your-app"></a><span data-ttu-id="c0ec9-180">Selecciona una categoría para tu aplicación</span><span class="sxs-lookup"><span data-stu-id="c0ec9-180">Select a category for your app</span></span>

<span data-ttu-id="c0ec9-181">Durante el envío, se te pedirá que clasifiques la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-181">During submission, you're asked to categorize your app.</span></span> <span data-ttu-id="c0ec9-182">En la tabla siguiente se asignan categorías de almacén Teams a las categorías enumeradas en [el Centro de partners](https://aka.ms/PartnerCenterHomePage).</span><span class="sxs-lookup"><span data-stu-id="c0ec9-182">The following table maps Teams store categories to the categories listed in [Partner Center](https://aka.ms/PartnerCenterHomePage).</span></span>

| <span data-ttu-id="c0ec9-183">categorías de Teams</span><span class="sxs-lookup"><span data-stu-id="c0ec9-183">Teams categories</span></span>       | <span data-ttu-id="c0ec9-184">Categorías del Centro de Partners</span><span class="sxs-lookup"><span data-stu-id="c0ec9-184">Partner Center categories</span></span>  |
|:---------------------|:---------------|
| <span data-ttu-id="c0ec9-185">Análisis y BI</span><span class="sxs-lookup"><span data-stu-id="c0ec9-185">Analytics and BI</span></span> | <span data-ttu-id="c0ec9-186">Análisis, visualización de datos y BI</span><span class="sxs-lookup"><span data-stu-id="c0ec9-186">Analytics, Data Visualization and BI</span></span> |
| <span data-ttu-id="c0ec9-187">Desarrollador e TI</span><span class="sxs-lookup"><span data-stu-id="c0ec9-187">Developer and IT</span></span> | <span data-ttu-id="c0ec9-188">Herramientas para desarrolladores, administrador de TI</span><span class="sxs-lookup"><span data-stu-id="c0ec9-188">Developer Tools, IT Admin</span></span> |
| <span data-ttu-id="c0ec9-189">Educación</span><span class="sxs-lookup"><span data-stu-id="c0ec9-189">Education</span></span> | <span data-ttu-id="c0ec9-190">Educación</span><span class="sxs-lookup"><span data-stu-id="c0ec9-190">Education</span></span> |
| <span data-ttu-id="c0ec9-191">Recursos humanos</span><span class="sxs-lookup"><span data-stu-id="c0ec9-191">Human resources</span></span> | <span data-ttu-id="c0ec9-192">Recursos Humanos y Reclutamiento</span><span class="sxs-lookup"><span data-stu-id="c0ec9-192">Human Resources and Recruiting</span></span> |
| <span data-ttu-id="c0ec9-193">Productividad</span><span class="sxs-lookup"><span data-stu-id="c0ec9-193">Productivity</span></span> | <span data-ttu-id="c0ec9-194">Gestión de contenidos, archivos y documentos, productividad, formación y tutoriales, y utilidades</span><span class="sxs-lookup"><span data-stu-id="c0ec9-194">Content Management, Files and documents, Productivity, Training and Tutorials, and Utilities</span></span> |
| <span data-ttu-id="c0ec9-195">Administración de proyectos</span><span class="sxs-lookup"><span data-stu-id="c0ec9-195">Project management</span></span> | <span data-ttu-id="c0ec9-196">Comunicación, administración de Project, flujo de trabajo y administración de empresas</span><span class="sxs-lookup"><span data-stu-id="c0ec9-196">Communication, Project Management, Workflow, and Business Management</span></span> |
| <span data-ttu-id="c0ec9-197">Ventas y apoyo</span><span class="sxs-lookup"><span data-stu-id="c0ec9-197">Sales and support</span></span> | <span data-ttu-id="c0ec9-198">Gestión de clientes y contactos, atención al cliente, gestión financiera, ventas y marketing</span><span class="sxs-lookup"><span data-stu-id="c0ec9-198">Customer and Contact Management, Customer Support, Financial Management, Sales and Marketing</span></span> |
| <span data-ttu-id="c0ec9-199">Social y divertido</span><span class="sxs-lookup"><span data-stu-id="c0ec9-199">Social and fun</span></span> | <span data-ttu-id="c0ec9-200">Galerías de imágenes y vídeos, estilo de vida, noticias y tiempo, social, viajes y navegación</span><span class="sxs-lookup"><span data-stu-id="c0ec9-200">Image and Video Galleries, Lifestyle, News and Weather, Social, Travel, and Navigation</span></span> |

### <a name="localize-your-store-listing"></a><span data-ttu-id="c0ec9-201">Localiza tu anuncio de tienda</span><span class="sxs-lookup"><span data-stu-id="c0ec9-201">Localize your store listing</span></span>

<span data-ttu-id="c0ec9-202">Partner Center admite [listados de tiendas localizadas.](/office/dev/store/prepare-localized-solutions)</span><span class="sxs-lookup"><span data-stu-id="c0ec9-202">Partner Center supports [localized store listings](/office/dev/store/prepare-localized-solutions).</span></span> <span data-ttu-id="c0ec9-203">Para obtener más información, consulta [cómo localizar la lista de aplicaciones de Teams.](../../../../concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="c0ec9-203">For more information, see [how to localize your Teams app listing](../../../../concepts/build-and-test/apps-localization.md).</span></span>

## <a name="complete-publisher-verification"></a><span data-ttu-id="c0ec9-204">Verificación completa de Publisher</span><span class="sxs-lookup"><span data-stu-id="c0ec9-204">Complete Publisher Verification</span></span>

<span data-ttu-id="c0ec9-205">[Publisher Se](/azure/active-directory/develop/publisher-verification-overview) requiere verificación para Teams aplicaciones que aparecen en la tienda.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-205">[Publisher Verification](/azure/active-directory/develop/publisher-verification-overview) is required for Teams apps listed in the store.</span></span> <span data-ttu-id="c0ec9-206">Para obtener más información, consulta [las preguntas más frecuentes,](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions) [cómo marcar la aplicación como editor verificado](/azure/active-directory/develop/mark-app-as-publisher-verified)y solucionar problemas de verificación [del editor.](/azure/active-directory/develop/troubleshoot-publisher-verification)</span><span class="sxs-lookup"><span data-stu-id="c0ec9-206">For more information, see [frequently asked questions](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions), [how to mark your app as publisher verified](/azure/active-directory/develop/mark-app-as-publisher-verified), and [troubleshoot publisher verification](/azure/active-directory/develop/troubleshoot-publisher-verification).</span></span>

## <a name="complete-publisher-attestation"></a><span data-ttu-id="c0ec9-207">Atestación Publisher completa</span><span class="sxs-lookup"><span data-stu-id="c0ec9-207">Complete Publisher Attestation</span></span>

<span data-ttu-id="c0ec9-208">[Publisher Attestation](/microsoft-365-app-certification/docs/attestation) también es necesario para Teams aplicaciones que aparecen en la tienda.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-208">[Publisher Attestation](/microsoft-365-app-certification/docs/attestation) is also required for Teams apps listed in the store.</span></span> <span data-ttu-id="c0ec9-209">El proceso incluye completar una autoevaluación de las prácticas de seguridad, control de datos y cumplimiento de la aplicación que pueden ayudar a los clientes potenciales a tomar decisiones informadas sobre el uso de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-209">The process includes completing a self-assessment of your app's security, data handling, and compliance practices that can help potential customers make informed decisions about using your app.</span></span>

> [!NOTE]
> <span data-ttu-id="c0ec9-210">Si envías una nueva aplicación, no podrás completar oficialmente Publisher Attestation hasta que la aplicación aparezca en la tienda de Teams.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-210">If you're submitting a new app, you can't officially complete Publisher Attestation until your app is listed on the Teams store.</span></span> <span data-ttu-id="c0ec9-211">Si estás actualizando una aplicación listada, completa Publisher Attestation antes de enviar la versión más reciente de la aplicación para su validación.</span><span class="sxs-lookup"><span data-stu-id="c0ec9-211">If you're updating a listed app, complete Publisher Attestation before you submit the latest version of the app for validation.</span></span>

## <a name="next-step"></a><span data-ttu-id="c0ec9-212">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="c0ec9-212">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c0ec9-213">Enviar la aplicación</span><span class="sxs-lookup"><span data-stu-id="c0ec9-213">Submit your app</span></span>](/office/dev/store/add-in-submission-guide)

---
title: Preparar el envío de la tienda
description: Describe los pasos finales antes de enviar Microsoft Teams aplicación para que aparezca en la tienda.
ms.topic: how-to
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: d46d21c3d984b5688c00857e485210b0f0fcf2c7
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101684"
---
# <a name="prepare-your-microsoft-teams-store-submission"></a><span data-ttu-id="5d9db-103">Preparar el envío Microsoft Teams almacén</span><span class="sxs-lookup"><span data-stu-id="5d9db-103">Prepare your Microsoft Teams store submission</span></span>

<span data-ttu-id="5d9db-104">Has diseñado, creado y probado tu Microsoft Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="5d9db-104">You've designed, built, and tested your Microsoft Teams app.</span></span> <span data-ttu-id="5d9db-105">Ahora estás listo para enumerar para que los usuarios puedan descubrir y empezar a usar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5d9db-105">Now you're ready to list it so people can discover and start using your app.</span></span>

<span data-ttu-id="5d9db-106">Antes de enviar la aplicación al [Centro de partners,](/office/dev/store/use-partner-center-to-submit-to-appsource)asegúrate de que has hecho lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="5d9db-106">Before you submit your app to [Partner Center](/office/dev/store/use-partner-center-to-submit-to-appsource), make sure you've done the following.</span></span>

## <a name="validate-your-app-package"></a><span data-ttu-id="5d9db-107">Validar el paquete de la aplicación</span><span class="sxs-lookup"><span data-stu-id="5d9db-107">Validate your app package</span></span>

<span data-ttu-id="5d9db-108">Aunque la aplicación puede estar funcionando en un entorno de prueba, debes comprobar el paquete de la aplicación para evitar que se presenten problemas durante el proceso de envío.</span><span class="sxs-lookup"><span data-stu-id="5d9db-108">While your app may be working in a test environment, you should check your app package to avoid running into issues during the submission process.</span></span>

<span data-ttu-id="5d9db-109">La Microsoft Teams de validación de aplicaciones te ayuda a identificar y solucionar problemas antes de enviarte al Centro de partners.</span><span class="sxs-lookup"><span data-stu-id="5d9db-109">The Microsoft Teams app validation tool helps you identify and fix issues before submitting to Partner Center.</span></span> <span data-ttu-id="5d9db-110">La herramienta comprueba automáticamente las configuraciones de la aplicación en los mismos casos de prueba usados durante la validación de la tienda.</span><span class="sxs-lookup"><span data-stu-id="5d9db-110">The tool automatically checks your app's configurations against the same test cases used during store validation.</span></span>

1. <span data-ttu-id="5d9db-111">Vaya a la [herramienta Microsoft Teams validación de aplicaciones.](https://dev.teams.microsoft.com/appvalidation.html)</span><span class="sxs-lookup"><span data-stu-id="5d9db-111">Go to the [Microsoft Teams app validation tool](https://dev.teams.microsoft.com/appvalidation.html).</span></span> <span data-ttu-id="5d9db-112">(Nota: La herramienta también está disponible en [App Studio](../../../build-and-test/app-studio-overview.md).)</span><span class="sxs-lookup"><span data-stu-id="5d9db-112">(Note: The tool is also available in [App Studio](../../../build-and-test/app-studio-overview.md).)</span></span>
1. <span data-ttu-id="5d9db-113">Upload el paquete de la aplicación para ejecutar las pruebas automatizadas.</span><span class="sxs-lookup"><span data-stu-id="5d9db-113">Upload your app package to run the automated tests.</span></span>
1. <span data-ttu-id="5d9db-114">Vaya a la **lista de comprobación preliminar** y revise los casos de prueba que son difíciles de automatizar.</span><span class="sxs-lookup"><span data-stu-id="5d9db-114">Go to the **Preliminary checklist** and review the test cases that are difficult to automate.</span></span>
1. <span data-ttu-id="5d9db-115">[Se solucionan problemas con las configuraciones](~/resources/schema/manifest-schema.md) o la aplicación en general si las pruebas automatizadas te dan errores o no has cumplido todos los criterios de la lista de comprobación.</span><span class="sxs-lookup"><span data-stu-id="5d9db-115">[Fix issues with your configurations](~/resources/schema/manifest-schema.md) or app in general if the automated tests give you errors or you haven't met all the criteria in the checklist.</span></span>

## <a name="compile-testing-instructions"></a><span data-ttu-id="5d9db-116">Compilar instrucciones de prueba</span><span class="sxs-lookup"><span data-stu-id="5d9db-116">Compile testing instructions</span></span>

<span data-ttu-id="5d9db-117">Proporcione instrucciones y recursos para ayudar a los revisores a probar la aplicación, incluidas las cuentas de prueba, las credenciales y las claves de licencia.</span><span class="sxs-lookup"><span data-stu-id="5d9db-117">Provide instructions and resources to help the reviewers test your app, including test accounts, credentials, and license keys.</span></span> <span data-ttu-id="5d9db-118">Puede agregar instrucciones en el Centro de partners o cargarlas en una ubicación disponible públicamente en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5d9db-118">You can add instructions in Partner Center or upload them to a publicly available location on SharePoint.</span></span>

### <a name="feature-list"></a><span data-ttu-id="5d9db-119">Lista de características</span><span class="sxs-lookup"><span data-stu-id="5d9db-119">Feature list</span></span>

<span data-ttu-id="5d9db-120">Proporciona detalles sobre las capacidades de la aplicación en Teams y los pasos para probar cada una de ellas.</span><span class="sxs-lookup"><span data-stu-id="5d9db-120">Provide details about your app's capabilities in Teams and steps for testing each one.</span></span>

### <a name="accounts"></a><span data-ttu-id="5d9db-121">Cuentas </span><span class="sxs-lookup"><span data-stu-id="5d9db-121">Accounts</span></span>

<span data-ttu-id="5d9db-122">Debes proporcionar cuentas de prueba si la aplicación requiere una licencia o una lista segura de back-end.</span><span class="sxs-lookup"><span data-stu-id="5d9db-122">You must provide test accounts if your app requires a license or backend safelisting.</span></span> <span data-ttu-id="5d9db-123">Todas las cuentas que proporciones deben incluir datos rellenados previamente para facilitar las pruebas.</span><span class="sxs-lookup"><span data-stu-id="5d9db-123">All accounts you provide must include pre-populated data to facilitate testing.</span></span>

<span data-ttu-id="5d9db-124">Según las características de la aplicación, es posible que deba proporcionar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5d9db-124">Depending on your app's features, you may need to provide all of the following:</span></span>

* <span data-ttu-id="5d9db-125">Cuenta de administrador (obligatorio)</span><span class="sxs-lookup"><span data-stu-id="5d9db-125">Admin account (required)</span></span>
* <span data-ttu-id="5d9db-126">Cuenta que no es de administrador (obligatorio)</span><span class="sxs-lookup"><span data-stu-id="5d9db-126">Non-admin account (required)</span></span>
* <span data-ttu-id="5d9db-127">Una cuenta que no está preconfigurado para probar correctamente la experiencia de inicio de sesión de primera ejecución (obligatorio)</span><span class="sxs-lookup"><span data-stu-id="5d9db-127">An account that isn't pre-configured in order to properly test the first-run sign-in experience (required)</span></span>
* <span data-ttu-id="5d9db-128">Una cuenta con acceso a características premium o actualizadas (si procede)</span><span class="sxs-lookup"><span data-stu-id="5d9db-128">An account with access to premium or upgraded features (if applicable)</span></span>
* <span data-ttu-id="5d9db-129">Dos cuentas en el mismo inquilino para probar la experiencia de colaboración de aplicaciones que funcionan en contextos compartidos (si procede)</span><span class="sxs-lookup"><span data-stu-id="5d9db-129">Two accounts in the same tenant to test the collaboration experience for apps that work in shared contexts (if applicable)</span></span>

### <a name="tenant-configurations"></a><span data-ttu-id="5d9db-130">Configuraciones de inquilinos</span><span class="sxs-lookup"><span data-stu-id="5d9db-130">Tenant configurations</span></span>

<span data-ttu-id="5d9db-131">Si debes configurar un inquilino Teams para usar la aplicación, incluye esas instrucciones y cuentas de administrador y no administrador para la validación.</span><span class="sxs-lookup"><span data-stu-id="5d9db-131">If you must configure a Teams tenant to use your app, include those instructions and admin and non-admin accounts for validation.</span></span>

### <a name="video-optional"></a><span data-ttu-id="5d9db-132">Vídeo (opcional)</span><span class="sxs-lookup"><span data-stu-id="5d9db-132">Video (optional)</span></span>

<span data-ttu-id="5d9db-133">Proporciona una grabación de la aplicación para que Microsoft pueda comprender completamente su funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="5d9db-133">Provide a recording of your app so that Microsoft can fully understand its functionality.</span></span>

## <a name="create-your-store-listing-details"></a><span data-ttu-id="5d9db-134">Crear los detalles de la descripción de la tienda</span><span class="sxs-lookup"><span data-stu-id="5d9db-134">Create your store listing details</span></span>

<span data-ttu-id="5d9db-135">La información que envías al Centro de partners [&#8212;](https://partner.microsoft.com) incluyendo tu nombre, descripciones, iconos e imágenes&#8212;se convierte en la tienda Teams y la descripción de Microsoft AppSource para tu aplicación.</span><span class="sxs-lookup"><span data-stu-id="5d9db-135">The information that you submit to [Partner Center](https://partner.microsoft.com)&#8212;including your name, descriptions, icons, and images&#8212;becomes the Teams store and Microsoft AppSource listing for your app.</span></span>

<span data-ttu-id="5d9db-136">Una descripción de la tienda puede ser la primera impresión de alguien de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5d9db-136">A store listing may be someone's first impression of your app.</span></span> <span data-ttu-id="5d9db-137">Aumente las instalaciones con una descripción que transmita eficazmente las ventajas, la funcionalidad y la marca de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5d9db-137">Increase installations with a listing that effectively conveys your app's benefits, functionality, and brand.</span></span>

### <a name="specify-a-short-name"></a><span data-ttu-id="5d9db-138">Especificar un nombre corto</span><span class="sxs-lookup"><span data-stu-id="5d9db-138">Specify a short name</span></span>

<span data-ttu-id="5d9db-139">El nombre de la aplicación (específicamente, su [*nombre*](~/resources/schema/manifest-schema.md#name)corto) desempeña un papel fundamental en la forma en que los usuarios lo descubren en la tienda.</span><span class="sxs-lookup"><span data-stu-id="5d9db-139">Your app's name (specifically, its [*short name*](~/resources/schema/manifest-schema.md#name)) plays a crucial role in how users discover it in the store.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="La captura de pantalla de ejemplo resalta dónde se muestra el nombre corto de una aplicación en una descripción de la tienda.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="5d9db-141">Asegúrese de que su nombre corto se adhiera a las [directrices de validación de la tienda.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#11-app-name)</span><span class="sxs-lookup"><span data-stu-id="5d9db-141">Make sure your short name adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#11-app-name).</span></span>

### <a name="write-descriptions"></a><span data-ttu-id="5d9db-142">Escribir descripciones</span><span class="sxs-lookup"><span data-stu-id="5d9db-142">Write descriptions</span></span>

<span data-ttu-id="5d9db-143">Debes tener una descripción corta y larga de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5d9db-143">You must have a short and long description of your app.</span></span>

#### <a name="short-description"></a><span data-ttu-id="5d9db-144">La descripción breve</span><span class="sxs-lookup"><span data-stu-id="5d9db-144">Short description</span></span>

<span data-ttu-id="5d9db-145">Un resumen conciso de la aplicación que debe ser original, atractivo y dirigido a la audiencia de destino.</span><span class="sxs-lookup"><span data-stu-id="5d9db-145">A concise summary of your app that should be original, engaging, and directed at your target audience.</span></span> <span data-ttu-id="5d9db-146">Mantenga la descripción corta en una oración.</span><span class="sxs-lookup"><span data-stu-id="5d9db-146">Keep the short description to one sentence.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="La captura de pantalla de ejemplo resalta dónde se muestra la breve descripción de una aplicación en una descripción de la tienda.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="5d9db-148">Asegúrese de que su breve descripción se adhiera a las [directrices de validación de la tienda.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#431-short-description)</span><span class="sxs-lookup"><span data-stu-id="5d9db-148">Make sure your short description adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#431-short-description).</span></span>

#### <a name="long-description"></a><span data-ttu-id="5d9db-149">La descripción larga</span><span class="sxs-lookup"><span data-stu-id="5d9db-149">Long description</span></span>

<span data-ttu-id="5d9db-150">La descripción larga puede proporcionar una narrativa que resalte las características principales de la aplicación, los problemas que resuelve y su audiencia de destino.</span><span class="sxs-lookup"><span data-stu-id="5d9db-150">The long description can provide a narrative that highlights your app's main features, the problems it solves, and its target audience.</span></span> <span data-ttu-id="5d9db-151">Aunque esta descripción puede tener hasta 4.000 caracteres, la mayoría de los usuarios solo leerán entre 300 y 500 palabras.</span><span class="sxs-lookup"><span data-stu-id="5d9db-151">While this description can be as long as 4,000 characters, most users will only read between 300-500 words.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/LongDescription-02.png" alt-text="Destaca la captura de pantalla de ejemplo donde se muestra la descripción larga de una aplicación en una descripción de la tienda.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="5d9db-153">Asegúrese de que la descripción larga se adhiera a las [directrices de validación de la tienda.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#432-long-description)</span><span class="sxs-lookup"><span data-stu-id="5d9db-153">Make sure your long description adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#432-long-description).</span></span>

### <a name="adhere-to-icon-design-guidelines"></a><span data-ttu-id="5d9db-154">Cumplir las directrices de diseño de iconos</span><span class="sxs-lookup"><span data-stu-id="5d9db-154">Adhere to icon design guidelines</span></span>

<span data-ttu-id="5d9db-155">Los iconos son uno de los elementos principales que los usuarios ven al navegar por la tienda.</span><span class="sxs-lookup"><span data-stu-id="5d9db-155">Icons are one of the main elements users see when browsing the store.</span></span> <span data-ttu-id="5d9db-156">Los iconos deben comunicar la marca y el propósito de la aplicación, al tiempo que se adhieren a Teams requisitos.</span><span class="sxs-lookup"><span data-stu-id="5d9db-156">Your icons should communicate your app's brand and purpose while also adhering to Teams requirements.</span></span>

<span data-ttu-id="5d9db-157">Para obtener más información, consulta las instrucciones para [crear Teams iconos de la aplicación](~/concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="5d9db-157">For more information, see [guidance on creating Teams app icons](~/concepts/build-and-test/apps-package.md#app-icons).</span></span>

### <a name="capture-screenshots"></a><span data-ttu-id="5d9db-158">Capturar capturas de pantalla</span><span class="sxs-lookup"><span data-stu-id="5d9db-158">Capture screenshots</span></span>

<span data-ttu-id="5d9db-159">Las capturas de pantalla proporcionan una vista previa visual destacada de la aplicación para complementar el nombre, el icono y las descripciones de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5d9db-159">Screenshots provide a prominent visual preview of your app to complement your app name, icon, and descriptions.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/Screenshot-01.png" alt-text="Destaca la captura de pantalla de ejemplo en la que las capturas de pantalla de la aplicación se muestran en una descripción de la tienda.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="5d9db-161">Recuerde lo siguiente acerca de las capturas de pantalla:</span><span class="sxs-lookup"><span data-stu-id="5d9db-161">Remember the following about screenshots:</span></span>

* <span data-ttu-id="5d9db-162">Puedes tener hasta cinco capturas de pantalla por descripción.</span><span class="sxs-lookup"><span data-stu-id="5d9db-162">You can have up to five screenshots per listing.</span></span>
* <span data-ttu-id="5d9db-163">Los tipos de archivo admitidos incluyen PNG, JPEG y GIF.</span><span class="sxs-lookup"><span data-stu-id="5d9db-163">Supported file types include PNG, JPEG, and GIF.</span></span>
* <span data-ttu-id="5d9db-164">Las dimensiones deben ser de 1366 x 768 píxeles.</span><span class="sxs-lookup"><span data-stu-id="5d9db-164">Dimensions should be 1366x768 pixels.</span></span>
* <span data-ttu-id="5d9db-165">Tamaño máximo de 1.024 KB.</span><span class="sxs-lookup"><span data-stu-id="5d9db-165">Maximum size of 1,024 KB.</span></span>

<span data-ttu-id="5d9db-166">Para obtener los procedimientos recomendados, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="5d9db-166">For best practices, see the following resources:</span></span>

* [<span data-ttu-id="5d9db-167">Teams de validación del almacén</span><span class="sxs-lookup"><span data-stu-id="5d9db-167">Teams store validation guidelines</span></span>](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#44-screenshots)
* [<span data-ttu-id="5d9db-168">Crear imágenes eficaces para almacenes de aplicaciones de Microsoft</span><span class="sxs-lookup"><span data-stu-id="5d9db-168">Craft effective images for Microsoft app stores</span></span>](/office/dev/store/craft-effective-appsource-store-images)

### <a name="create-a-video"></a><span data-ttu-id="5d9db-169">Crear un vídeo</span><span class="sxs-lookup"><span data-stu-id="5d9db-169">Create a video</span></span>

<span data-ttu-id="5d9db-170">Un vídeo de la descripción puede ser la forma más eficaz de comunicar por qué las personas deben usar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5d9db-170">A video in your listing can be the most effective way to communicate why people should use your app.</span></span> <span data-ttu-id="5d9db-171">Debe abordar las siguientes preguntas en un vídeo:</span><span class="sxs-lookup"><span data-stu-id="5d9db-171">You should address the following questions in a video:</span></span>

* <span data-ttu-id="5d9db-172">Quién Cuál es tu aplicación?</span><span class="sxs-lookup"><span data-stu-id="5d9db-172">Who is your app for?</span></span>
* <span data-ttu-id="5d9db-173">¿Qué problemas puede resolver la aplicación?</span><span class="sxs-lookup"><span data-stu-id="5d9db-173">What problems can your app solve?</span></span>
* <span data-ttu-id="5d9db-174">¿Cómo funciona la aplicación?</span><span class="sxs-lookup"><span data-stu-id="5d9db-174">How does your app work?</span></span>
* <span data-ttu-id="5d9db-175">¿Qué otras ventajas obtienes al usar la aplicación?</span><span class="sxs-lookup"><span data-stu-id="5d9db-175">What other benefits do you get from using your app?</span></span>

#### <a name="best-practices-for-videos"></a><span data-ttu-id="5d9db-176">Procedimientos recomendados para vídeos</span><span class="sxs-lookup"><span data-stu-id="5d9db-176">Best practices for videos</span></span>

* <span data-ttu-id="5d9db-177">Mantén el vídeo entre 30 y 90 segundos.</span><span class="sxs-lookup"><span data-stu-id="5d9db-177">Keep your video between 30-90 seconds.</span></span>
* <span data-ttu-id="5d9db-178">Apunta a la calidad.</span><span class="sxs-lookup"><span data-stu-id="5d9db-178">Aim for quality.</span></span> <span data-ttu-id="5d9db-179">En una descripción, los usuarios verán el vídeo antes de las capturas de pantalla.</span><span class="sxs-lookup"><span data-stu-id="5d9db-179">In a listing, users will see your video before screenshots.</span></span>

### <a name="select-a-category-for-your-app"></a><span data-ttu-id="5d9db-180">Seleccionar una categoría para la aplicación</span><span class="sxs-lookup"><span data-stu-id="5d9db-180">Select a category for your app</span></span>

<span data-ttu-id="5d9db-181">Durante el envío, se te pide que clasifices tu aplicación.</span><span class="sxs-lookup"><span data-stu-id="5d9db-181">During submission, you're asked to categorize your app.</span></span> <span data-ttu-id="5d9db-182">En la tabla siguiente se Teams categorías de almacén a las categorías enumeradas en [el Centro de partners](https://aka.ms/PartnerCenterHomePage).</span><span class="sxs-lookup"><span data-stu-id="5d9db-182">The following table maps Teams store categories to the categories listed in [Partner Center](https://aka.ms/PartnerCenterHomePage).</span></span>

| <span data-ttu-id="5d9db-183">Teams categorías</span><span class="sxs-lookup"><span data-stu-id="5d9db-183">Teams categories</span></span>       | <span data-ttu-id="5d9db-184">Categorías del Centro de partners</span><span class="sxs-lookup"><span data-stu-id="5d9db-184">Partner Center categories</span></span>  |
|:---------------------|:---------------|
| <span data-ttu-id="5d9db-185">Análisis e BI</span><span class="sxs-lookup"><span data-stu-id="5d9db-185">Analytics and BI</span></span> | <span data-ttu-id="5d9db-186">Análisis, visualización de datos e BI</span><span class="sxs-lookup"><span data-stu-id="5d9db-186">Analytics, Data Visualization and BI</span></span> |
| <span data-ttu-id="5d9db-187">Desarrollador y IT</span><span class="sxs-lookup"><span data-stu-id="5d9db-187">Developer and IT</span></span> | <span data-ttu-id="5d9db-188">Herramientas para desarrolladores, administrador de TI</span><span class="sxs-lookup"><span data-stu-id="5d9db-188">Developer Tools, IT Admin</span></span> |
| <span data-ttu-id="5d9db-189">Educación</span><span class="sxs-lookup"><span data-stu-id="5d9db-189">Education</span></span> | <span data-ttu-id="5d9db-190">Educación</span><span class="sxs-lookup"><span data-stu-id="5d9db-190">Education</span></span> |
| <span data-ttu-id="5d9db-191">Recursos humanos</span><span class="sxs-lookup"><span data-stu-id="5d9db-191">Human resources</span></span> | <span data-ttu-id="5d9db-192">Recursos humanos y contratación</span><span class="sxs-lookup"><span data-stu-id="5d9db-192">Human Resources and Recruiting</span></span> |
| <span data-ttu-id="5d9db-193">Productividad</span><span class="sxs-lookup"><span data-stu-id="5d9db-193">Productivity</span></span> | <span data-ttu-id="5d9db-194">Administración de contenido, archivos y documentos, productividad, aprendizaje y tutoriales y utilidades</span><span class="sxs-lookup"><span data-stu-id="5d9db-194">Content Management, Files and documents, Productivity, Training and Tutorials, and Utilities</span></span> |
| <span data-ttu-id="5d9db-195">Administración de proyectos</span><span class="sxs-lookup"><span data-stu-id="5d9db-195">Project management</span></span> | <span data-ttu-id="5d9db-196">Administración de Project, flujo de trabajo y administración empresarial</span><span class="sxs-lookup"><span data-stu-id="5d9db-196">Communication, Project Management, Workflow, and Business Management</span></span> |
| <span data-ttu-id="5d9db-197">Ventas y soporte técnico</span><span class="sxs-lookup"><span data-stu-id="5d9db-197">Sales and support</span></span> | <span data-ttu-id="5d9db-198">Administración de clientes y contactos, soporte al cliente, administración financiera, ventas y marketing</span><span class="sxs-lookup"><span data-stu-id="5d9db-198">Customer and Contact Management, Customer Support, Financial Management, Sales and Marketing</span></span> |
| <span data-ttu-id="5d9db-199">Social y divertido</span><span class="sxs-lookup"><span data-stu-id="5d9db-199">Social and fun</span></span> | <span data-ttu-id="5d9db-200">Galerías de imágenes y vídeo, Estilo de vida, Noticias y Tiempo, Social, Viajes y Navegación</span><span class="sxs-lookup"><span data-stu-id="5d9db-200">Image and Video Galleries, Lifestyle, News and Weather, Social, Travel, and Navigation</span></span> |

### <a name="localize-your-store-listing"></a><span data-ttu-id="5d9db-201">Localización de la descripción de la tienda</span><span class="sxs-lookup"><span data-stu-id="5d9db-201">Localize your store listing</span></span>

<span data-ttu-id="5d9db-202">El Centro de partners admite [listados de almacenes localizados.](https://docs.microsoft.com/office/dev/store/prepare-localized-solutions)</span><span class="sxs-lookup"><span data-stu-id="5d9db-202">Partner Center supports [localized store listings](https://docs.microsoft.com/office/dev/store/prepare-localized-solutions).</span></span> <span data-ttu-id="5d9db-203">Para obtener más información, [consulta cómo encontrar la descripción](../../../../concepts/build-and-test/apps-localization.md)Teams aplicación .</span><span class="sxs-lookup"><span data-stu-id="5d9db-203">For more information, see [how to localize your Teams app listing](../../../../concepts/build-and-test/apps-localization.md).</span></span>

## <a name="complete-publisher-verification"></a><span data-ttu-id="5d9db-204">Verificación Publisher completa</span><span class="sxs-lookup"><span data-stu-id="5d9db-204">Complete Publisher Verification</span></span>

<span data-ttu-id="5d9db-205">[Publisher se requiere](/azure/active-directory/develop/publisher-verification-overview) la verificación de Teams aplicaciones enumeradas en la tienda. Para obtener más información, consulta [preguntas más frecuentes,](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)cómo marcar tu aplicación como editor [comprobado](/azure/active-directory/develop/mark-app-as-publisher-verified)y solucionar problemas de verificación [del editor.](/azure/active-directory/develop/troubleshoot-publisher-verification)</span><span class="sxs-lookup"><span data-stu-id="5d9db-205">[Publisher Verification](/azure/active-directory/develop/publisher-verification-overview) is required for Teams apps listed in the store.For more information, see [frequently asked questions](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions), [how to mark your app as publisher verified](/azure/active-directory/develop/mark-app-as-publisher-verified), and [troubleshoot publisher verification](/azure/active-directory/develop/troubleshoot-publisher-verification).</span></span>

## <a name="complete-publisher-attestation"></a><span data-ttu-id="5d9db-206">Certificación Publisher completa</span><span class="sxs-lookup"><span data-stu-id="5d9db-206">Complete Publisher Attestation</span></span>

<span data-ttu-id="5d9db-207">[Publisher atestación también](/microsoft-365-app-certification/docs/attestation) es necesaria para las Teams que aparecen en la tienda.</span><span class="sxs-lookup"><span data-stu-id="5d9db-207">[Publisher Attestation](/microsoft-365-app-certification/docs/attestation) is also required for Teams apps listed in the store.</span></span> <span data-ttu-id="5d9db-208">El proceso incluye completar una autoevaluación de las prácticas de seguridad, control de datos y cumplimiento de la aplicación que pueden ayudar a los clientes potenciales a tomar decisiones fundamentadas sobre el uso de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5d9db-208">The process includes completing a self-assessment of your app's security, data handling, and compliance practices that can help potential customers make informed decisions about using your app.</span></span>

> [!NOTE]
> <span data-ttu-id="5d9db-209">Si vas a enviar una nueva aplicación, no puedes completar oficialmente Publisher atestación hasta que la aplicación aparezca en la Teams tienda.</span><span class="sxs-lookup"><span data-stu-id="5d9db-209">If you're submitting a new app, you can't officially complete Publisher Attestation until your app is listed on the Teams store.</span></span> <span data-ttu-id="5d9db-210">Si estás actualizando una aplicación enumerada, completa Publisher atestación antes de enviar la versión más reciente de la aplicación para su validación.</span><span class="sxs-lookup"><span data-stu-id="5d9db-210">If you're updating a listed app, complete Publisher Attestation before you submit the latest version of the app for validation.</span></span>

## <a name="next-step"></a><span data-ttu-id="5d9db-211">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="5d9db-211">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5d9db-212">Enviar la aplicación</span><span class="sxs-lookup"><span data-stu-id="5d9db-212">Submit your app</span></span>](https://docs.microsoft.com/office/dev/store/add-in-submission-guide)

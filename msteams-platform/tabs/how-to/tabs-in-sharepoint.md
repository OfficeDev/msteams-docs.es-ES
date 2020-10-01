---
title: Adición de una pestaña de Microsoft Teams en SharePoint como un elemento Web de SPFx
author: laujan
description: Cómo implementar la pestaña de Microsoft Teams existente en SharePoint como un elemento Web de SharePoint Framework.
keywords: pestañas de Teams desarrollo de SharePoint Framework
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: d7f617f0967743eab84423cd31f78d4700db1c1c
ms.sourcegitcommit: e92408e751a8f51028908ab7e2415a8051a536c0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2020
ms.locfileid: "48326350"
---
# <a name="adding-a-microsoft-teams-tab-in-sharepoint-as-an-spfx-web-part"></a><span data-ttu-id="956a5-104">Adición de una pestaña de Microsoft Teams en SharePoint como un elemento Web de SPFx</span><span class="sxs-lookup"><span data-stu-id="956a5-104">Adding a Microsoft Teams tab in SharePoint as an SPFx web part</span></span>

## <a name="rich-integration-between-teams-and-sharepoint"></a><span data-ttu-id="956a5-105">Integración enriquecida entre Teams y SharePoint</span><span class="sxs-lookup"><span data-stu-id="956a5-105">Rich integration between Teams and SharePoint</span></span>

<span data-ttu-id="956a5-106">Con la versión de noviembre de Teams y SharePoint Framework v.</span><span class="sxs-lookup"><span data-stu-id="956a5-106">With the November release of Teams and SharePoint Framework v.</span></span> <span data-ttu-id="956a5-107">1,7, los desarrolladores tienen dos eficaces capacidades:</span><span class="sxs-lookup"><span data-stu-id="956a5-107">1.7, developers have two powerful capabilities:</span></span>

<ul  class="panelContent cardsC">
<li>
    <a href="#introduction">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img src="~/assets/images/tabs/tabs-in-sharepoint/image084.png" alt="tab-in-sharepoint view"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3><span data-ttu-id="956a5-108">Pestañas de Microsoft Teams en SharePoint</span><span class="sxs-lookup"><span data-stu-id="956a5-108">Teams Tabs in SharePoint</span></span></h3>
                        <p><span data-ttu-id="956a5-109">Cree experiencias de aplicaciones enriquecidas en SharePoint llevando su aplicación de Teams a SharePoint (este artículo).</span><span class="sxs-lookup"><span data-stu-id="956a5-109">Create rich app experiences in SharePoint by bringing your Teams app into Sharepoint (this article).</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li>
    <a href="https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img src="~/assets/images/tabs/tabs-in-sharepoint/SharePoint-web-part-exposed-as-a-Tab-in-Microsoft-Teams.png" alt="web-part-exposed-as-a-tab" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3><span data-ttu-id="956a5-110">SharePoint Framework en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="956a5-110">SharePoint Framework in Teams</span></span></h3>
                        <p><span data-ttu-id="956a5-111">Incorpore los elementos Web de SharePoint a teams y deje que SharePoint administre el hospedaje.</span><span class="sxs-lookup"><span data-stu-id="956a5-111">Bring your SharePoint web parts to Teams and let SharePoint manage the hosting for you.</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a><span data-ttu-id="956a5-112">Pestañas de Microsoft Teams en SharePoint</span><span class="sxs-lookup"><span data-stu-id="956a5-112">Teams tabs in SharePoint</span></span>

<span data-ttu-id="956a5-113">Con SharePoint Framework v. 1.7, ahora somos compatibles con la capacidad para que los desarrolladores tomen sus pestañas de Microsoft Teams y la hospeden en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="956a5-113">With SharePoint Framework v.1.7, we’re now supporting the ability for developers to take their Teams tabs and host it in SharePoint.</span></span> <span data-ttu-id="956a5-114">Como las pestañas hospedadas en SharePoint obtienen una experiencia similar a "página completa", exponiendo todas las características de las pestañas de Microsoft Teams y conserva el contexto y la familiaridad de un sitio de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="956a5-114">As Tabs hosted in SharePoint get a similar "full page" experience, exposing the all the features of Teams tabs while retaining the context and familiarity of a SharePoint site.</span></span>

### <a name="sharepoint-framework-in-teams"></a><span data-ttu-id="956a5-115">SharePoint Framework en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="956a5-115">SharePoint Framework in Teams</span></span>

<span data-ttu-id="956a5-116">También puede implementar las pestañas de Microsoft Teams con SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="956a5-116">You can also implement your Microsoft Teams tabs using SharePoint Framework.</span></span> <span data-ttu-id="956a5-117">Para los desarrolladores de SharePoint, esto simplifica considerablemente el proceso de desarrollo de las pestañas de Microsoft Teams, ya que los elementos Web de SharePoint Framework se hospedan en SharePoint sin necesidad de servicios externos como Azure.</span><span class="sxs-lookup"><span data-stu-id="956a5-117">For SharePoint developers, this significantly simplifies the development process for Teams tabs because SharePoint Framework web parts are hosted within SharePoint without any need for external services such as Azure.</span></span> [<span data-ttu-id="956a5-118">Obtenga más información sobre el uso de SharePoint Framework en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="956a5-118">Learn more about using the SharePoint Framework in Teams.</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a><span data-ttu-id="956a5-119">Introducción</span><span class="sxs-lookup"><span data-stu-id="956a5-119">Introduction</span></span>

<span data-ttu-id="956a5-120">Estas instrucciones le explicarán cómo puede tomar una pestaña de una aplicación de ejemplo de Microsoft Teams y usarla en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="956a5-120">These instructions will explain how you can take a tab from a Microsoft Teams sample app and use it in SharePoint.</span></span> <span data-ttu-id="956a5-121">Usaremos una pestaña que ya está hospedada en Azure para centrarse en el trabajo de integración necesario.</span><span class="sxs-lookup"><span data-stu-id="956a5-121">We will be using a tab that's already hosted on Azure in order to focus on the required integration work.</span></span>

<span data-ttu-id="956a5-122">La aplicación de ejemplo que estamos usando es una aplicación de administración del talento.</span><span class="sxs-lookup"><span data-stu-id="956a5-122">The sample app we're using is a Talent Management application.</span></span> <span data-ttu-id="956a5-123">Administra el proceso de contratación de candidatos para puestos abiertos en un equipo.</span><span class="sxs-lookup"><span data-stu-id="956a5-123">It manages the hiring process of candidates for open positions in a team.</span></span> <span data-ttu-id="956a5-124">(La propia aplicación, aunque parece buena, realmente no hace nada.</span><span class="sxs-lookup"><span data-stu-id="956a5-124">(The app itself, while it looks nice, doesn't actually do anything.</span></span> <span data-ttu-id="956a5-125">Queremos centrarnos en la creación de una aplicación de Microsoft Teams y en cargarla en Teams, no crear una aplicación de administración de talento real.)</span><span class="sxs-lookup"><span data-stu-id="956a5-125">We want to focus on building a Teams app and loading it into Teams, not create a real talent management application.)</span></span>

### <a name="benefits-of-this-approach"></a><span data-ttu-id="956a5-126">Ventajas de este enfoque</span><span class="sxs-lookup"><span data-stu-id="956a5-126">Benefits of this approach</span></span>

- <span data-ttu-id="956a5-127">Obtener acceso a los usuarios de SharePoint con la pestaña de Microsoft Teams existente</span><span class="sxs-lookup"><span data-stu-id="956a5-127">Reach SharePoint users with your existing Teams tab</span></span>
- <span data-ttu-id="956a5-128">Cargue el manifiesto de la aplicación directamente en el catálogo de aplicaciones de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="956a5-128">Upload your app manifest directly to your SharePoint app catalog.</span></span> <span data-ttu-id="956a5-129">Los [paquetes de aplicación de Teams](~/concepts/build-and-test/apps-package.md) ahora son compatibles con SharePoint</span><span class="sxs-lookup"><span data-stu-id="956a5-129">[Teams application packages](~/concepts/build-and-test/apps-package.md) are now supported by SharePoint</span></span>
- <span data-ttu-id="956a5-130">Los usuarios finales configuran la pestaña en una página al igual que cualquier otro elemento Web de SharePoint</span><span class="sxs-lookup"><span data-stu-id="956a5-130">End users configure the tab on a page just like any other SharePoint web part</span></span>
- <span data-ttu-id="956a5-131">La pestaña puede tener acceso al [contexto](~/tabs/how-to/access-teams-context.md) de la misma manera que cuando se ejecuta dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="956a5-131">Your tab can access its [context](~/tabs/how-to/access-teams-context.md) just as it can when running inside Teams</span></span>

## <a name="step-1-testing-the-sample-app"></a><span data-ttu-id="956a5-132">Paso 1: probar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="956a5-132">Step 1: Testing the sample app</span></span>

<span data-ttu-id="956a5-133">Descargue el manifiesto de la aplicación de ejemplo desde [**aquí**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span><span class="sxs-lookup"><span data-stu-id="956a5-133">Download the sample app manifest from [**here**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span></span>

<span data-ttu-id="956a5-134">En Microsoft Teams, haga clic en el icono de la tienda en la esquina inferior izquierda y, a continuación, "cargar una aplicación personalizada" en la parte inferior izquierda.</span><span class="sxs-lookup"><span data-stu-id="956a5-134">In Microsoft Teams, click on the Store icon at the lower left and then "Upload a custom app" at the lower left.</span></span> <span data-ttu-id="956a5-135">El archivo que se cargará se ubicará en la carpeta descargas; se llama TalentMgmt-Azure.zip.</span><span class="sxs-lookup"><span data-stu-id="956a5-135">The file to upload will be located in your Downloads folder; it's called TalentMgmt-Azure.zip.</span></span> <span data-ttu-id="956a5-136">Si todo va bien, verá la pantalla de instalación/consentimiento de la aplicación de administración del talento.</span><span class="sxs-lookup"><span data-stu-id="956a5-136">If all goes well, you'll see the install/consent screen for the talent management app.</span></span> <span data-ttu-id="956a5-137">Elija el equipo en el que desea instalar y haga clic en el botón instalar.</span><span class="sxs-lookup"><span data-stu-id="956a5-137">Choose the team you want to install to and click the Install button.</span></span> <span data-ttu-id="956a5-138">Ahora tiene la libertad de experimentar con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="956a5-138">You're now free to experiment with the app.</span></span>

## <a name="step-2-using-the-teams-tab-in-sharepoint"></a><span data-ttu-id="956a5-139">Paso 2: uso de la pestaña Microsoft Teams en SharePoint</span><span class="sxs-lookup"><span data-stu-id="956a5-139">Step 2: Using the Teams tab in SharePoint</span></span>

<span data-ttu-id="956a5-140">Para cargar e implementar el paquete de la aplicación Microsoft Teams en el catálogo de aplicaciones de SharePoint `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` , visite, por ejemplo, `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` .</span><span class="sxs-lookup"><span data-stu-id="956a5-140">Upload and deploy your Teams app package to your SharePoint App Catalog by visiting `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`, e.g. `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span>

<span data-ttu-id="956a5-141">Cuando se le solicite, habilite "hacer que esta solución esté disponible en todos los sitios de la organización":</span><span class="sxs-lookup"><span data-stu-id="956a5-141">When prompted, enable "Make this solution available to all sites in the organization":</span></span>

![Pestañas en la vista de SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

<span data-ttu-id="956a5-143">En el sitio, cree una página nueva haciendo clic en el botón de engranaje situado en la esquina superior derecha y, a continuación, "agregar una página":</span><span class="sxs-lookup"><span data-stu-id="956a5-143">In your site, create a new page by clicking in the gear button at the upper right and then "Add a page":</span></span>

![Vista de SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

<span data-ttu-id="956a5-145">Verá la experiencia de creación de páginas de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="956a5-145">You'll see the SharePoint Pages authoring experience.</span></span> <span data-ttu-id="956a5-146">Asigne a la página el nombre "mi pestaña de Microsoft Teams".</span><span class="sxs-lookup"><span data-stu-id="956a5-146">Name your page "My Teams Tab".</span></span>

<span data-ttu-id="956a5-147">Abra el cuadro de herramientas del elemento Web presionando el botón + y seleccione la pestaña Microsoft Teams (denominada "Contoso HR").</span><span class="sxs-lookup"><span data-stu-id="956a5-147">Open the web part toolbox by pressing the + button, and select your Teams Tab (named "Contoso HR").</span></span> <span data-ttu-id="956a5-148">Los elementos Web se ordenan alfabéticamente; Si se trata de una lista larga, puede usar la barra de búsqueda para encontrarla.</span><span class="sxs-lookup"><span data-stu-id="956a5-148">Web parts are sorted alphabetically; if it's a long list, you can use the search bar to find it.</span></span> <span data-ttu-id="956a5-149">Se creará un elemento Web en el lienzo que contiene la pestaña de Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="956a5-149">This will create a web part in the canvas that contains your Teams tab:</span></span>

![Vista de pestaña](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

<span data-ttu-id="956a5-151">Haga clic en el botón "publicar" cuando termine la edición.</span><span class="sxs-lookup"><span data-stu-id="956a5-151">Press the "Publish" button when you are finished editing.</span></span>

<span data-ttu-id="956a5-152">Puede que quiera hacer clic en "agregar página a navegación" para tener una referencia rápida a la página en la barra de navegación izquierda:</span><span class="sxs-lookup"><span data-stu-id="956a5-152">You may want to click "Add page to navigation" to have a quick reference to your page in the left navigation bar:</span></span>

![Pestaña en imagen de SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="step-3-explore-app-pages-in-sharepoint"></a><span data-ttu-id="956a5-154">Paso 3: explorar las páginas de la aplicación en SharePoint</span><span class="sxs-lookup"><span data-stu-id="956a5-154">Step 3: Explore App Pages in SharePoint</span></span>

<span data-ttu-id="956a5-155">Una vez publicada la página, puede explorar [la conversión de la aplicación de Microsoft Teams en una experiencia más completa dentro de SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span><span class="sxs-lookup"><span data-stu-id="956a5-155">Once your page is published, you can explore [turning your Teams app into a more complete experience inside SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span></span> <span data-ttu-id="956a5-156">Esto convierte la página actual en una página de la aplicación, que muestra el diseño de página de SharePoint normal con una experiencia de página completa para la pestaña Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="956a5-156">This converts the current page into an App Page, showing the normal SharePoint page layout with a full-page experience for the Teams tab:</span></span>

![Imagen de pestañas en SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="more-information"></a><span data-ttu-id="956a5-158">Más información</span><span class="sxs-lookup"><span data-stu-id="956a5-158">More information</span></span>

- [<span data-ttu-id="956a5-159">Creación de la pestaña de Microsoft Teams con SharePoint Framework: tutorial</span><span class="sxs-lookup"><span data-stu-id="956a5-159">Building Microsoft Teams tab using SharePoint Framework - Tutorial</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
- [<span data-ttu-id="956a5-160">Usar páginas de aplicación de elemento único en SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="956a5-160">Using single part app pages in SharePoint Online</span></span>](/sharepoint/dev/spfx/web-parts/single-part-app-pages)

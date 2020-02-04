---
title: Adición de una pestaña de Microsoft Teams en SharePoint como un elemento Web de SPFx
author: laujan
description: Cómo implementar la pestaña de Microsoft Teams existente en SharePoint como un elemento Web de SharePoint Framework.
keywords: pestañas de Teams desarrollo de SharePoint Framework
ms.topic: conceptual
ms.author: ''
ms.openlocfilehash: b29cd29891779a69a0342f10d383792b3818590a
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675945"
---
# <a name="adding-a-microsoft-teams-tab-in-sharepoint-as-an-spfx-web-part"></a><span data-ttu-id="1fd27-104">Adición de una pestaña de Microsoft Teams en SharePoint como un elemento Web de SPFx</span><span class="sxs-lookup"><span data-stu-id="1fd27-104">Adding a Microsoft Teams tab in SharePoint as an SPFx web part</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1fd27-105">Esta característica se encuentra en versión preliminar en este momento y está sujeta a cambios.</span><span class="sxs-lookup"><span data-stu-id="1fd27-105">This feature is currently in preview and is subject to change.</span></span> <span data-ttu-id="1fd27-106">No es compatible con el uso en entornos de producción.</span><span class="sxs-lookup"><span data-stu-id="1fd27-106">It is not supported for use in production environments.</span></span> <span data-ttu-id="1fd27-107">Sus comentarios y sugerencias sobre esta función son bienvenidos en la [lista de problemas de SharePoint Dev Docs](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="1fd27-107">Your feedback and input around this capability is welcome using the [SharePoint Dev Docs issue list](https://github.com/SharePoint/sp-dev-docs/issues).</span></span>

## <a name="rich-integration-between-teams-and-sharepoint"></a><span data-ttu-id="1fd27-108">Integración enriquecida entre Teams y SharePoint</span><span class="sxs-lookup"><span data-stu-id="1fd27-108">Rich integration between Teams and SharePoint</span></span>

<span data-ttu-id="1fd27-109">Con la versión de noviembre de Teams y SharePoint Framework v.</span><span class="sxs-lookup"><span data-stu-id="1fd27-109">With the November release of Teams and SharePoint Framework v.</span></span> <span data-ttu-id="1fd27-110">1,7, los desarrolladores tienen dos eficaces capacidades:</span><span class="sxs-lookup"><span data-stu-id="1fd27-110">1.7, developers have two powerful capabilities:</span></span>

<ul  class="panelContent cardsC">
<li>
    <a href="#introduction">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img src="~/assets/images/tabs/tabs-in-sharepoint/image084.png" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3><span data-ttu-id="1fd27-111">Pestañas de Microsoft Teams en SharePoint</span><span class="sxs-lookup"><span data-stu-id="1fd27-111">Teams Tabs in SharePoint</span></span></h3>
                        <p><span data-ttu-id="1fd27-112">Cree experiencias de aplicaciones enriquecidas en SharePoint llevando su aplicación de Teams a SharePoint (este artículo).</span><span class="sxs-lookup"><span data-stu-id="1fd27-112">Create rich app experiences in SharePoint by bringing your Teams app into Sharepoint (this article).</span></span></p>
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
                            <img src="~/assets/images/tabs/tabs-in-sharepoint/SharePoint-web-part-exposed-as-a-Tab-in-Microsoft-Teams.png" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3><span data-ttu-id="1fd27-113">SharePoint Framework en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1fd27-113">SharePoint Framework in Teams</span></span></h3>
                        <p><span data-ttu-id="1fd27-114">Incorpore los elementos Web de SharePoint a teams y deje que SharePoint administre el hospedaje.</span><span class="sxs-lookup"><span data-stu-id="1fd27-114">Bring your SharePoint web parts to Teams and let SharePoint manage the hosting for you.</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a><span data-ttu-id="1fd27-115">Pestañas de Microsoft Teams en SharePoint</span><span class="sxs-lookup"><span data-stu-id="1fd27-115">Teams tabs in SharePoint</span></span>

<span data-ttu-id="1fd27-116">Con SharePoint Framework v. 1.7, ahora somos compatibles con la capacidad para que los desarrolladores tomen sus pestañas de Microsoft Teams y la hospeden en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1fd27-116">With SharePoint Framework v.1.7, we’re now supporting the ability for developers to take their Teams tabs and host it in SharePoint.</span></span> <span data-ttu-id="1fd27-117">Como las pestañas hospedadas en SharePoint obtienen una experiencia similar a "página completa", exponiendo todas las características de las pestañas de Microsoft Teams y conserva el contexto y la familiaridad de un sitio de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1fd27-117">As Tabs hosted in SharePoint get a similar "full page" experience, exposing the all the features of Teams tabs while retaining the context and familiarity of a SharePoint site.</span></span>

### <a name="sharepoint-framework-in-teams"></a><span data-ttu-id="1fd27-118">SharePoint Framework en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1fd27-118">SharePoint Framework in Teams</span></span>

<span data-ttu-id="1fd27-119">También puede implementar las pestañas de Microsoft Teams con SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="1fd27-119">You can also implement your Microsoft Teams tabs using SharePoint Framework.</span></span> <span data-ttu-id="1fd27-120">Para los desarrolladores de SharePoint, esto simplifica considerablemente el proceso de desarrollo de las pestañas de Microsoft Teams, ya que los elementos Web de SharePoint Framework se hospedan en SharePoint sin necesidad de servicios externos como Azure.</span><span class="sxs-lookup"><span data-stu-id="1fd27-120">For SharePoint developers, this significantly simplifies the development process for Teams tabs because SharePoint Framework web parts are hosted within SharePoint without any need for external services such as Azure.</span></span> [<span data-ttu-id="1fd27-121">Obtenga más información sobre el uso de SharePoint Framework en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1fd27-121">Learn more about using the SharePoint Framework in Teams.</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a><span data-ttu-id="1fd27-122">Introducción</span><span class="sxs-lookup"><span data-stu-id="1fd27-122">Introduction</span></span>

<span data-ttu-id="1fd27-123">Estas instrucciones le explicarán cómo puede tomar una pestaña de una aplicación de ejemplo de Microsoft Teams y usarla en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1fd27-123">These instructions will explain how you can take a tab from a Microsoft Teams sample app and use it in SharePoint.</span></span> <span data-ttu-id="1fd27-124">Usaremos una pestaña que ya está hospedada en Azure para centrarse en el trabajo de integración necesario.</span><span class="sxs-lookup"><span data-stu-id="1fd27-124">We will be using a tab that's already hosted on Azure in order to focus on the required integration work.</span></span>

<span data-ttu-id="1fd27-125">La aplicación de ejemplo que estamos usando es una aplicación de administración del talento.</span><span class="sxs-lookup"><span data-stu-id="1fd27-125">The sample app we're using is a Talent Management application.</span></span> <span data-ttu-id="1fd27-126">Administra el proceso de contratación de candidatos para puestos abiertos en un equipo.</span><span class="sxs-lookup"><span data-stu-id="1fd27-126">It manages the hiring process of candidates for open positions in a team.</span></span> <span data-ttu-id="1fd27-127">(La propia aplicación, aunque parece buena, realmente no hace nada.</span><span class="sxs-lookup"><span data-stu-id="1fd27-127">(The app itself, while it looks nice, doesn't actually do anything.</span></span> <span data-ttu-id="1fd27-128">Queremos centrarnos en la creación de una aplicación de Microsoft Teams y en cargarla en Teams, no crear una aplicación de administración de talento real.)</span><span class="sxs-lookup"><span data-stu-id="1fd27-128">We want to focus on building a Teams app and loading it into Teams, not create a real talent management application.)</span></span>

### <a name="benefits-of-this-approach"></a><span data-ttu-id="1fd27-129">Ventajas de este enfoque</span><span class="sxs-lookup"><span data-stu-id="1fd27-129">Benefits of this approach</span></span>

- <span data-ttu-id="1fd27-130">Obtener acceso a los usuarios de SharePoint con la pestaña de Microsoft Teams existente</span><span class="sxs-lookup"><span data-stu-id="1fd27-130">Reach SharePoint users with your existing Teams tab</span></span>
- <span data-ttu-id="1fd27-131">Cargue el manifiesto de la aplicación directamente en el catálogo de aplicaciones de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1fd27-131">Upload your app manifest directly to your SharePoint app catalog.</span></span> <span data-ttu-id="1fd27-132">Los [paquetes de aplicación de Teams](~/concepts/build-and-test/apps-package.md) ahora son compatibles con SharePoint</span><span class="sxs-lookup"><span data-stu-id="1fd27-132">[Teams application packages](~/concepts/build-and-test/apps-package.md) are now supported by SharePoint</span></span>
- <span data-ttu-id="1fd27-133">Los usuarios finales configuran la pestaña en una página al igual que cualquier otro elemento Web de SharePoint</span><span class="sxs-lookup"><span data-stu-id="1fd27-133">End users configure the tab on a page just like any other SharePoint web part</span></span>
- <span data-ttu-id="1fd27-134">La pestaña puede tener acceso al [contexto](~/tabs/how-to/access-teams-context.md) de la misma manera que cuando se ejecuta dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="1fd27-134">Your tab can access its [context](~/tabs/how-to/access-teams-context.md) just as it can when running inside Teams</span></span>

## <a name="step-1-testing-the-sample-app"></a><span data-ttu-id="1fd27-135">Paso 1: probar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1fd27-135">Step 1: Testing the sample app</span></span>

<span data-ttu-id="1fd27-136">Descargue el manifiesto de la aplicación de ejemplo desde [**aquí**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span><span class="sxs-lookup"><span data-stu-id="1fd27-136">Download the sample app manifest from [**here**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span></span>

<span data-ttu-id="1fd27-137">En Microsoft Teams, haga clic en el icono de la tienda en la esquina inferior izquierda y, a continuación, "cargar una aplicación personalizada" en la parte inferior izquierda.</span><span class="sxs-lookup"><span data-stu-id="1fd27-137">In Microsoft Teams, click on the Store icon at the lower left and then "Upload a custom app" at the lower left.</span></span> <span data-ttu-id="1fd27-138">El archivo que se cargará se ubicará en la carpeta descargas; se denomina TalentMgmt-Azure. zip.</span><span class="sxs-lookup"><span data-stu-id="1fd27-138">The file to upload will be located in your Downloads folder; it's called TalentMgmt-Azure.zip.</span></span> <span data-ttu-id="1fd27-139">Si todo va bien, verá la pantalla de instalación/consentimiento de la aplicación de administración del talento.</span><span class="sxs-lookup"><span data-stu-id="1fd27-139">If all goes well, you'll see the install/consent screen for the talent management app.</span></span> <span data-ttu-id="1fd27-140">Elija el equipo en el que desea instalar y haga clic en el botón instalar.</span><span class="sxs-lookup"><span data-stu-id="1fd27-140">Choose the team you want to install to and click the Install button.</span></span> <span data-ttu-id="1fd27-141">Ahora tiene la libertad de experimentar con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1fd27-141">You're now free to experiment with the app.</span></span>

## <a name="step-2-using-the-teams-tab-in-sharepoint"></a><span data-ttu-id="1fd27-142">Paso 2: uso de la pestaña Microsoft Teams en SharePoint</span><span class="sxs-lookup"><span data-stu-id="1fd27-142">Step 2: Using the Teams tab in SharePoint</span></span>

<span data-ttu-id="1fd27-143">Para cargar e implementar el paquete de la aplicación Microsoft Teams en el `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`catálogo de aplicaciones `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`de SharePoint, visite, por ejemplo,.</span><span class="sxs-lookup"><span data-stu-id="1fd27-143">Upload and deploy your Teams app package to your SharePoint App Catalog by visiting `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`, e.g. `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span>

<span data-ttu-id="1fd27-144">Cuando se le solicite, habilite "hacer que esta solución esté disponible en todos los sitios de la organización":</span><span class="sxs-lookup"><span data-stu-id="1fd27-144">When prompted, enable "Make this solution available to all sites in the organization":</span></span>

![](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

<span data-ttu-id="1fd27-145">En el sitio, cree una página nueva haciendo clic en el botón de engranaje situado en la esquina superior derecha y, a continuación, "agregar una página":</span><span class="sxs-lookup"><span data-stu-id="1fd27-145">In your site, create a new page by clicking in the gear button at the upper right and then "Add a page":</span></span>

![](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

<span data-ttu-id="1fd27-146">Verá la experiencia de creación de páginas de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1fd27-146">You'll see the SharePoint Pages authoring experience.</span></span> <span data-ttu-id="1fd27-147">Asigne a la página el nombre "mi pestaña de Microsoft Teams".</span><span class="sxs-lookup"><span data-stu-id="1fd27-147">Name your page "My Teams Tab".</span></span>

<span data-ttu-id="1fd27-148">Abra el cuadro de herramientas del elemento Web presionando el botón + y seleccione la pestaña Microsoft Teams (denominada "Contoso HR").</span><span class="sxs-lookup"><span data-stu-id="1fd27-148">Open the web part toolbox by pressing the + button, and select your Teams Tab (named "Contoso HR").</span></span> <span data-ttu-id="1fd27-149">Los elementos Web se ordenan alfabéticamente; Si se trata de una lista larga, puede usar la barra de búsqueda para encontrarla.</span><span class="sxs-lookup"><span data-stu-id="1fd27-149">Web parts are sorted alphabetically; if it's a long list, you can use the search bar to find it.</span></span> <span data-ttu-id="1fd27-150">Se creará un elemento Web en el lienzo que contiene la pestaña de Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="1fd27-150">This will create a web part in the canvas that contains your Teams tab:</span></span>

![](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

<span data-ttu-id="1fd27-151">Haga clic en el botón "publicar" cuando termine la edición.</span><span class="sxs-lookup"><span data-stu-id="1fd27-151">Press the "Publish" button when you are finished editing.</span></span>

<span data-ttu-id="1fd27-152">Puede que quiera hacer clic en "agregar página a navegación" para tener una referencia rápida a la página en la barra de navegación izquierda:</span><span class="sxs-lookup"><span data-stu-id="1fd27-152">You may want to click "Add page to navigation" to have a quick reference to your page in the left navigation bar:</span></span>

![](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="step-3-explore-app-pages-in-sharepoint"></a><span data-ttu-id="1fd27-153">Paso 3: explorar las páginas de la aplicación en SharePoint</span><span class="sxs-lookup"><span data-stu-id="1fd27-153">Step 3: Explore App Pages in SharePoint</span></span>

<span data-ttu-id="1fd27-154">Una vez publicada la página, puede explorar [la conversión de la aplicación de Microsoft Teams en una experiencia más completa dentro de SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span><span class="sxs-lookup"><span data-stu-id="1fd27-154">Once your page is published, you can explore [turning your Teams app into a more complete experience inside SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span></span> <span data-ttu-id="1fd27-155">Esto convierte la página actual en una página de la aplicación, que muestra el diseño de página de SharePoint normal con una experiencia de página completa para la pestaña Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="1fd27-155">This converts the current page into an App Page, showing the normal SharePoint page layout with a full-page experience for the Teams tab:</span></span>

![](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="more-information"></a><span data-ttu-id="1fd27-156">Más información</span><span class="sxs-lookup"><span data-stu-id="1fd27-156">More information</span></span>

- [<span data-ttu-id="1fd27-157">Creación de la pestaña de Microsoft Teams con SharePoint Framework: tutorial</span><span class="sxs-lookup"><span data-stu-id="1fd27-157">Building Microsoft Teams tab using SharePoint Framework - Tutorial</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
- [<span data-ttu-id="1fd27-158">Usar páginas de aplicación de elemento único en SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="1fd27-158">Using single part app pages in SharePoint Online</span></span>](/sharepoint/dev/spfx/web-parts/single-part-app-pages)

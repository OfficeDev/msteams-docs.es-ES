---
title: Agregar una pestaña de Microsoft Teams en SharePoint como elemento web de SPFx
author: laujan
description: Cómo implementar la pestaña de Teams existente en SharePoint como un elemento web de SharePoint Framework.
keywords: Desarrollo de SharePoint Framework con pestañas de teams
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 2e5d1b01aa5f7566e25c7720d6a0539386226576
ms.sourcegitcommit: 6caf503de5544fb8b9c8c6bef8eff4ff5a46068c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/17/2021
ms.locfileid: "50270794"
---
# <a name="adding-a-microsoft-teams-tab-in-sharepoint-as-an-spfx-web-part"></a><span data-ttu-id="41b03-104">Agregar una pestaña de Microsoft Teams en SharePoint como elemento web de SPFx</span><span class="sxs-lookup"><span data-stu-id="41b03-104">Adding a Microsoft Teams tab in SharePoint as an SPFx web part</span></span>

## <a name="rich-integration-between-teams-and-sharepoint"></a><span data-ttu-id="41b03-105">Integración enriquecte entre Teams y SharePoint</span><span class="sxs-lookup"><span data-stu-id="41b03-105">Rich integration between Teams and SharePoint</span></span>

<span data-ttu-id="41b03-106">Con la versión de noviembre de Teams y SharePoint Framework v.</span><span class="sxs-lookup"><span data-stu-id="41b03-106">With the November release of Teams and SharePoint Framework v.</span></span> <span data-ttu-id="41b03-107">1.7, los desarrolladores tienen dos capacidades eficaces:</span><span class="sxs-lookup"><span data-stu-id="41b03-107">1.7, developers have two powerful capabilities:</span></span>

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
                        <h3><span data-ttu-id="41b03-108">Pestañas de Teams en SharePoint</span><span class="sxs-lookup"><span data-stu-id="41b03-108">Teams Tabs in SharePoint</span></span></h3>
                        <p><span data-ttu-id="41b03-109">Cree experiencias de aplicación enriqueciendo su aplicación de Teams en SharePoint (este artículo).</span><span class="sxs-lookup"><span data-stu-id="41b03-109">Create rich app experiences in SharePoint by bringing your Teams app into Sharepoint (this article).</span></span></p>
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
                        <h3><span data-ttu-id="41b03-110">SharePoint Framework en Teams</span><span class="sxs-lookup"><span data-stu-id="41b03-110">SharePoint Framework in Teams</span></span></h3>
                        <p><span data-ttu-id="41b03-111">Bring your SharePoint web parts to Teams and let SharePoint manage the hosting for you.</span><span class="sxs-lookup"><span data-stu-id="41b03-111">Bring your SharePoint web parts to Teams and let SharePoint manage the hosting for you.</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a><span data-ttu-id="41b03-112">Pestañas de Teams en SharePoint</span><span class="sxs-lookup"><span data-stu-id="41b03-112">Teams tabs in SharePoint</span></span>

<span data-ttu-id="41b03-113">Con SharePoint Framework v.1.7, ahora se admite la capacidad para que los desarrolladores tomen sus pestañas de Teams y la alomen en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="41b03-113">With SharePoint Framework v.1.7, we’re now supporting the ability for developers to take their Teams tabs and host it in SharePoint.</span></span> <span data-ttu-id="41b03-114">A medida que las pestañas hospedadas en SharePoint obtienen una experiencia de "página completa" similar, exponiendo todas las características de las pestañas de Teams a la vez que conservan el contexto y la familiaridad de un sitio de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="41b03-114">As Tabs hosted in SharePoint get a similar "full page" experience, exposing the all the features of Teams tabs while retaining the context and familiarity of a SharePoint site.</span></span>

### <a name="sharepoint-framework-in-teams"></a><span data-ttu-id="41b03-115">SharePoint Framework en Teams</span><span class="sxs-lookup"><span data-stu-id="41b03-115">SharePoint Framework in Teams</span></span>

<span data-ttu-id="41b03-116">También puede implementar las pestañas de Microsoft Teams con SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="41b03-116">You can also implement your Microsoft Teams tabs using SharePoint Framework.</span></span> <span data-ttu-id="41b03-117">Para los desarrolladores de SharePoint, esto simplifica significativamente el proceso de desarrollo para las pestañas de Teams porque los elementos web de SharePoint Framework se hospedan en SharePoint sin necesidad de servicios externos como Azure.</span><span class="sxs-lookup"><span data-stu-id="41b03-117">For SharePoint developers, this significantly simplifies the development process for Teams tabs because SharePoint Framework web parts are hosted within SharePoint without any need for external services such as Azure.</span></span> [<span data-ttu-id="41b03-118">Obtenga más información sobre cómo usar SharePoint Framework en Teams.</span><span class="sxs-lookup"><span data-stu-id="41b03-118">Learn more about using the SharePoint Framework in Teams.</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a><span data-ttu-id="41b03-119">Introducción</span><span class="sxs-lookup"><span data-stu-id="41b03-119">Introduction</span></span>

<span data-ttu-id="41b03-120">Estas instrucciones explicarán cómo puede tomar una pestaña de una aplicación de ejemplo de Microsoft Teams y usarla en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="41b03-120">These instructions will explain how you can take a tab from a Microsoft Teams sample app and use it in SharePoint.</span></span> <span data-ttu-id="41b03-121">Usaremos una pestaña que ya está hospedada en Azure para centrarse en el trabajo de integración necesario.</span><span class="sxs-lookup"><span data-stu-id="41b03-121">We will be using a tab that's already hosted on Azure in order to focus on the required integration work.</span></span>

<span data-ttu-id="41b03-122">La aplicación de ejemplo que estamos usando es una aplicación de administración de talento.</span><span class="sxs-lookup"><span data-stu-id="41b03-122">The sample app we're using is a Talent Management application.</span></span> <span data-ttu-id="41b03-123">Administra el proceso de contratación de candidatos para puestos abiertos en un equipo.</span><span class="sxs-lookup"><span data-stu-id="41b03-123">It manages the hiring process of candidates for open positions in a team.</span></span> <span data-ttu-id="41b03-124">(La propia aplicación, aunque tiene un aspecto agradable, no hace nada en realidad.</span><span class="sxs-lookup"><span data-stu-id="41b03-124">(The app itself, while it looks nice, doesn't actually do anything.</span></span> <span data-ttu-id="41b03-125">Queremos centrarnos en crear una aplicación de Teams y cargarla en Teams, no crear una aplicación de administración de talento real).</span><span class="sxs-lookup"><span data-stu-id="41b03-125">We want to focus on building a Teams app and loading it into Teams, not create a real talent management application.)</span></span>

### <a name="benefits-of-this-approach"></a><span data-ttu-id="41b03-126">Ventajas de este enfoque</span><span class="sxs-lookup"><span data-stu-id="41b03-126">Benefits of this approach</span></span>

- <span data-ttu-id="41b03-127">Llegar a los usuarios de SharePoint con la pestaña de Teams existente</span><span class="sxs-lookup"><span data-stu-id="41b03-127">Reach SharePoint users with your existing Teams tab</span></span>
- <span data-ttu-id="41b03-128">Cargue el manifiesto de la aplicación directamente en el catálogo de aplicaciones de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="41b03-128">Upload your app manifest directly to your SharePoint app catalog.</span></span> <span data-ttu-id="41b03-129">[Los paquetes de](~/concepts/build-and-test/apps-package.md) aplicaciones de Teams ahora son compatibles con SharePoint</span><span class="sxs-lookup"><span data-stu-id="41b03-129">[Teams application packages](~/concepts/build-and-test/apps-package.md) are now supported by SharePoint</span></span>
- <span data-ttu-id="41b03-130">Los usuarios finales configuran la pestaña en una página como cualquier otro elemento web de SharePoint</span><span class="sxs-lookup"><span data-stu-id="41b03-130">End users configure the tab on a page just like any other SharePoint web part</span></span>
- <span data-ttu-id="41b03-131">La pestaña puede acceder a su [contexto de](~/tabs/how-to/access-teams-context.md) la mismo forma que cuando se ejecuta dentro de Teams</span><span class="sxs-lookup"><span data-stu-id="41b03-131">Your tab can access its [context](~/tabs/how-to/access-teams-context.md) just as it can when running inside Teams</span></span>

## <a name="step-1-testing-the-sample-app"></a><span data-ttu-id="41b03-132">Paso 1: Probar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="41b03-132">Step 1: Testing the sample app</span></span>

<span data-ttu-id="41b03-133">Descargue el manifiesto de la aplicación de ejemplo [**desde aquí.**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)</span><span class="sxs-lookup"><span data-stu-id="41b03-133">Download the sample app manifest from [**here**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span></span>

<span data-ttu-id="41b03-134">En Microsoft Teams, haga clic en el icono de la Tienda en la esquina inferior izquierda y, a continuación, en "Cargar una aplicación personalizada" en la parte inferior izquierda.</span><span class="sxs-lookup"><span data-stu-id="41b03-134">In Microsoft Teams, click on the Store icon at the lower left and then "Upload a custom app" at the lower left.</span></span> <span data-ttu-id="41b03-135">El archivo que se va a cargar se ubicará en la carpeta Descargas; se denomina TalentMgmt-Azure.zip.</span><span class="sxs-lookup"><span data-stu-id="41b03-135">The file to upload will be located in your Downloads folder; it's called TalentMgmt-Azure.zip.</span></span> <span data-ttu-id="41b03-136">Si todo va bien, verás la pantalla de instalación o consentimiento de la aplicación de administración de talento.</span><span class="sxs-lookup"><span data-stu-id="41b03-136">If all goes well, you'll see the install/consent screen for the talent management app.</span></span> <span data-ttu-id="41b03-137">Elija el equipo en el que desea instalar y haga clic en el botón Instalar.</span><span class="sxs-lookup"><span data-stu-id="41b03-137">Choose the team you want to install to and click the Install button.</span></span> <span data-ttu-id="41b03-138">Ahora puedes experimentar con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="41b03-138">You're now free to experiment with the app.</span></span>

## <a name="step-2-using-the-teams-tab-in-sharepoint"></a><span data-ttu-id="41b03-139">Paso 2: Usar la pestaña Teams en SharePoint</span><span class="sxs-lookup"><span data-stu-id="41b03-139">Step 2: Using the Teams tab in SharePoint</span></span>

<span data-ttu-id="41b03-140">Cargue e implemente el paquete de la aplicación de Teams en el Catálogo de aplicaciones de SharePoint visitando `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` , por ejemplo. `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`</span><span class="sxs-lookup"><span data-stu-id="41b03-140">Upload and deploy your Teams app package to your SharePoint App Catalog by visiting `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`, e.g. `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span>

<span data-ttu-id="41b03-141">Cuando se le pida, habilite "Hacer que esta solución esté disponible para todos los sitios de la organización":</span><span class="sxs-lookup"><span data-stu-id="41b03-141">When prompted, enable "Make this solution available to all sites in the organization":</span></span>

![Pestañas en la vista de SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

<span data-ttu-id="41b03-143">En el sitio, cree una nueva página haciendo clic en el botón de engranaje situado en la esquina superior derecha y, a continuación, haga clic en "Agregar una página":</span><span class="sxs-lookup"><span data-stu-id="41b03-143">In your site, create a new page by clicking in the gear button at the upper right and then "Add a page":</span></span>

![Vista de SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

<span data-ttu-id="41b03-145">Verá la experiencia de creación de páginas de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="41b03-145">You'll see the SharePoint Pages authoring experience.</span></span> <span data-ttu-id="41b03-146">Asigne a su página el nombre "Pestaña Mis equipos".</span><span class="sxs-lookup"><span data-stu-id="41b03-146">Name your page "My Teams Tab".</span></span>

<span data-ttu-id="41b03-147">Abra el cuadro de herramientas del elemento web presionando el botón + y seleccione la pestaña Teams (denominada "Contoso HR").</span><span class="sxs-lookup"><span data-stu-id="41b03-147">Open the web part toolbox by pressing the + button, and select your Teams Tab (named "Contoso HR").</span></span> <span data-ttu-id="41b03-148">Los elementos web se ordenan alfabéticamente; si es una lista larga, puede usar la barra de búsqueda para encontrarla.</span><span class="sxs-lookup"><span data-stu-id="41b03-148">Web parts are sorted alphabetically; if it's a long list, you can use the search bar to find it.</span></span> <span data-ttu-id="41b03-149">Esto creará un elemento web en el lienzo que contiene la pestaña de Teams:</span><span class="sxs-lookup"><span data-stu-id="41b03-149">This will create a web part in the canvas that contains your Teams tab:</span></span>

![Vista de pestaña](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

<span data-ttu-id="41b03-151">Presione el botón "Publicar" cuando haya terminado de editar.</span><span class="sxs-lookup"><span data-stu-id="41b03-151">Press the "Publish" button when you are finished editing.</span></span>

<span data-ttu-id="41b03-152">Es posible que desee hacer clic en "Agregar página a la navegación" para tener una referencia rápida a la página en la barra de navegación izquierda:</span><span class="sxs-lookup"><span data-stu-id="41b03-152">You may want to click "Add page to navigation" to have a quick reference to your page in the left navigation bar:</span></span>

![Pestaña en la imagen de SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="step-3-explore-app-pages-in-sharepoint"></a><span data-ttu-id="41b03-154">Paso 3: Explorar páginas de aplicación en SharePoint</span><span class="sxs-lookup"><span data-stu-id="41b03-154">Step 3: Explore App Pages in SharePoint</span></span>

<span data-ttu-id="41b03-155">Una vez publicada la página, puede explorar cómo convertir la aplicación teams en una [experiencia más completa dentro de SharePoint.](/sharepoint/dev/spfx/web-parts/single-part-app-pages)</span><span class="sxs-lookup"><span data-stu-id="41b03-155">Once your page is published, you can explore [turning your Teams app into a more complete experience inside SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span></span> <span data-ttu-id="41b03-156">Esto convierte la página actual en una página de aplicación, que muestra el diseño de página normal de SharePoint con una experiencia de página completa para la pestaña Teams:</span><span class="sxs-lookup"><span data-stu-id="41b03-156">This converts the current page into an App Page, showing the normal SharePoint page layout with a full-page experience for the Teams tab:</span></span>

![Imagen de pestañas en SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a><span data-ttu-id="41b03-158">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="41b03-158">Code sample</span></span>
| <span data-ttu-id="41b03-159">**Nombre de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="41b03-159">**Sample name**</span></span> | <span data-ttu-id="41b03-160">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="41b03-160">**Description**</span></span> | <span data-ttu-id="41b03-161">**SPFx**</span><span class="sxs-lookup"><span data-stu-id="41b03-161">**SPFx**</span></span> |
|-----------------|-----------------|----------|
| <span data-ttu-id="41b03-162">Elemento web de SPFx</span><span class="sxs-lookup"><span data-stu-id="41b03-162">SPFx web part</span></span> | <span data-ttu-id="41b03-163">Ejemplos de elementos web de SPFx para pestañas, canales y grupos.</span><span class="sxs-lookup"><span data-stu-id="41b03-163">SPFx web part samples for tabs, channels, and groups.</span></span> | [<span data-ttu-id="41b03-164">View</span><span class="sxs-lookup"><span data-stu-id="41b03-164">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="more-information"></a><span data-ttu-id="41b03-165">Más información</span><span class="sxs-lookup"><span data-stu-id="41b03-165">More information</span></span>

- [<span data-ttu-id="41b03-166">Creación de la pestaña de Microsoft Teams con SharePoint Framework: tutorial</span><span class="sxs-lookup"><span data-stu-id="41b03-166">Building Microsoft Teams tab using SharePoint Framework - Tutorial</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
- [<span data-ttu-id="41b03-167">Usar páginas de aplicación de elemento único en SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="41b03-167">Using single part app pages in SharePoint Online</span></span>](/sharepoint/dev/spfx/web-parts/single-part-app-pages)

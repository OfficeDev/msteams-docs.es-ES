---
title: Añadir una pestaña de Teams a SharePoint
author: laujan
description: Cómo implementar la pestaña teams existente en SharePoint como un elemento web de SharePoint Framework.
keywords: desarrollo de sharepoint framework de pestañas de teams
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: a2ea6c470f094a9d7b8617a210559e911f5f81c9
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058484"
---
# <a name="add-teams-tab-to-sharepoint"></a><span data-ttu-id="5c842-104">Añadir una pestaña de Teams a SharePoint</span><span class="sxs-lookup"><span data-stu-id="5c842-104">Add Teams tab to SharePoint</span></span> 

<span data-ttu-id="5c842-105">Puede obtener una amplia experiencia de integración entre Microsoft Teams y SharePoint agregando una pestaña de Microsoft Teams en SharePoint como un elemento web de SPFx.</span><span class="sxs-lookup"><span data-stu-id="5c842-105">You can get a rich integration experience between Microsoft Teams and SharePoint by adding a Microsoft Teams tab in SharePoint as an SPFx web part.</span></span> <span data-ttu-id="5c842-106">Este documento le guía sobre cómo tomar una pestaña de una aplicación de ejemplo de Microsoft Teams y usarla en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5c842-106">This document guides you on how you to take a tab from a Microsoft Teams sample app and use it in SharePoint.</span></span> 

## <a name="rich-integration-between-teams-and-sharepoint"></a><span data-ttu-id="5c842-107">Integración enriquecte entre Teams y SharePoint</span><span class="sxs-lookup"><span data-stu-id="5c842-107">Rich integration between Teams and SharePoint</span></span>

<span data-ttu-id="5c842-108">Con la versión de noviembre de Teams y SharePoint Framework v.1.7, los desarrolladores tienen dos funciones eficaces:</span><span class="sxs-lookup"><span data-stu-id="5c842-108">With the November release of Teams and SharePoint Framework v.1.7, developers have two powerful capabilities:</span></span>

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
                        <h3><span data-ttu-id="5c842-109">Pestañas de Teams en SharePoint</span><span class="sxs-lookup"><span data-stu-id="5c842-109">Teams Tabs in SharePoint</span></span></h3>
                        <p><span data-ttu-id="5c842-110">Cree experiencias de aplicación enriquecciones en SharePoint llevando la aplicación de Teams a Sharepoint (en este artículo).</span><span class="sxs-lookup"><span data-stu-id="5c842-110">Create rich app experiences in SharePoint by bringing your Teams app into Sharepoint (this article).</span></span></p>
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
                        <h3><span data-ttu-id="5c842-111">SharePoint Framework en Teams</span><span class="sxs-lookup"><span data-stu-id="5c842-111">SharePoint Framework in Teams</span></span></h3>
                        <p><span data-ttu-id="5c842-112">Lleve los elementos web de SharePoint a Teams y deje que SharePoint administre el hospedaje por usted.</span><span class="sxs-lookup"><span data-stu-id="5c842-112">Bring your SharePoint web parts to Teams and let SharePoint manage the hosting for you.</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a><span data-ttu-id="5c842-113">Pestañas de Teams en SharePoint</span><span class="sxs-lookup"><span data-stu-id="5c842-113">Teams tabs in SharePoint</span></span>

<span data-ttu-id="5c842-114">Con SharePoint Framework v.1.7, puede hospedar las pestañas de Teams en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5c842-114">With SharePoint Framework v.1.7, you can host your Teams tabs in SharePoint.</span></span> <span data-ttu-id="5c842-115">A medida que las pestañas hospedadas en SharePoint obtienen una experiencia de página completa **similar,** exponiendo todas las características de las pestañas de Teams a la vez que conservan el contexto y la familiaridad de un sitio de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5c842-115">As tabs hosted in SharePoint get a similar **full page** experience, exposing all the features of Teams tabs while retaining the context and familiarity of a SharePoint site.</span></span>

### <a name="sharepoint-framework-in-teams"></a><span data-ttu-id="5c842-116">SharePoint Framework en Teams</span><span class="sxs-lookup"><span data-stu-id="5c842-116">SharePoint Framework in Teams</span></span>

<span data-ttu-id="5c842-117">También puede implementar las pestañas de Microsoft Teams con SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="5c842-117">You can also implement your Microsoft Teams tabs using SharePoint Framework.</span></span> <span data-ttu-id="5c842-118">Los elementos web de SharePoint Framework se hospedan en SharePoint sin necesidad de servicios externos, como Azure.</span><span class="sxs-lookup"><span data-stu-id="5c842-118">SharePoint Framework web parts are hosted within SharePoint without any need for external services, such as Azure.</span></span> <span data-ttu-id="5c842-119">Para los desarrolladores de SharePoint, esto simplifica significativamente el proceso de desarrollo de las pestañas de Teams.</span><span class="sxs-lookup"><span data-stu-id="5c842-119">For SharePoint developers, this significantly simplifies the development process for Teams tabs.</span></span> <span data-ttu-id="5c842-120">Para obtener más información sobre SharePoint Framework en Teams, vea [cómo usar SharePoint Framework en Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)</span><span class="sxs-lookup"><span data-stu-id="5c842-120">For more information on SharePoint Framework in Teams, see [how to use the SharePoint Framework in Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)</span></span>

## <a name="introduction"></a><span data-ttu-id="5c842-121">Introducción</span><span class="sxs-lookup"><span data-stu-id="5c842-121">Introduction</span></span>

<span data-ttu-id="5c842-122">La pestaña usada aquí ya está hospedada en Azure, para centrarse en el trabajo de integración necesario.</span><span class="sxs-lookup"><span data-stu-id="5c842-122">The tab used here is already hosted on Azure, to focus on the required integration work.</span></span>

<span data-ttu-id="5c842-123">La aplicación de ejemplo que se usa es una aplicación de administración de talento.</span><span class="sxs-lookup"><span data-stu-id="5c842-123">The sample app that is being used is a Talent Management application.</span></span> <span data-ttu-id="5c842-124">Administra el proceso de contratación de candidatos para puestos abiertos en un equipo.</span><span class="sxs-lookup"><span data-stu-id="5c842-124">It manages the hiring process of candidates for open positions in a team.</span></span> <span data-ttu-id="5c842-125">Crea una aplicación de Teams de ejemplo y cárbala en Teams.</span><span class="sxs-lookup"><span data-stu-id="5c842-125">Build a sample Teams app and load it into Teams.</span></span> <span data-ttu-id="5c842-126">No cree una aplicación de administración de talento real.</span><span class="sxs-lookup"><span data-stu-id="5c842-126">Do not create a real talent management application.</span></span>

### <a name="benefits-of-this-approach"></a><span data-ttu-id="5c842-127">Ventajas de este enfoque</span><span class="sxs-lookup"><span data-stu-id="5c842-127">Benefits of this approach</span></span>

* <span data-ttu-id="5c842-128">Llegue a los usuarios de SharePoint con la pestaña Teams existente.</span><span class="sxs-lookup"><span data-stu-id="5c842-128">Reach SharePoint users with your existing Teams tab.</span></span>
* <span data-ttu-id="5c842-129">Cargue el manifiesto de la aplicación directamente en el catálogo de aplicaciones de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5c842-129">Upload your app manifest directly to your SharePoint app catalog.</span></span> <span data-ttu-id="5c842-130">[Los paquetes de](~/concepts/build-and-test/apps-package.md) aplicaciones de Teams ahora son compatibles con SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5c842-130">[Teams application packages](~/concepts/build-and-test/apps-package.md) are now supported by SharePoint.</span></span>
* <span data-ttu-id="5c842-131">Los usuarios configuran la pestaña en una página como cualquier otro elemento web de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5c842-131">The users configure the tab on a page just like any other SharePoint web part.</span></span>
* <span data-ttu-id="5c842-132">La pestaña puede tener acceso a [su contexto](~/tabs/how-to/access-teams-context.md) del mismo modo que cuando se ejecuta dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="5c842-132">Your tab can access its [context](~/tabs/how-to/access-teams-context.md) sameas it can, when running inside Teams.</span></span>

<span data-ttu-id="5c842-133">**Para agregar la pestaña Teams a SharePoint**</span><span class="sxs-lookup"><span data-stu-id="5c842-133">**To add Teams tab to SharePoint**</span></span>

<span data-ttu-id="5c842-134">Realice los siguientes pasos para agregar la pestaña Teams a SharePoint:</span><span class="sxs-lookup"><span data-stu-id="5c842-134">Perform the following steps to add Teams tab to SharePoint:</span></span>

## <a name="1-test-the-sample-app"></a><span data-ttu-id="5c842-135">1. Probar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="5c842-135">1. Test the sample app</span></span>

<span data-ttu-id="5c842-136">Descargue el [manifiesto de la aplicación de ejemplo](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span><span class="sxs-lookup"><span data-stu-id="5c842-136">Download the [sample app manifest](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span></span>

1. <span data-ttu-id="5c842-137">Abra Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="5c842-137">Open Microsoft Teams.</span></span>
1. <span data-ttu-id="5c842-138">Seleccione el **icono de la Appstore** en la parte inferior izquierda de la ficha lateral.</span><span class="sxs-lookup"><span data-stu-id="5c842-138">Select the **Appstore** icon at the lower left of side tab.</span></span>
1. <span data-ttu-id="5c842-139">Selecciona **Cargar una aplicación personalizada** en la parte inferior izquierda.</span><span class="sxs-lookup"><span data-stu-id="5c842-139">Select **Upload a custom app** at the lower left.</span></span> <span data-ttu-id="5c842-140">La siguiente imagen muestra la pantalla correspondiente:</span><span class="sxs-lookup"><span data-stu-id="5c842-140">The following image displays the corresponding screen:</span></span>  

    ![cargar una aplicación personalizada](~/assets/images/tabs/tabs-in-sharepoint/upload-custom-app.png)

1. <span data-ttu-id="5c842-142">El archivo que se va a cargar se encuentra en la **carpeta Descargas.**</span><span class="sxs-lookup"><span data-stu-id="5c842-142">The file to upload is located in your **Downloads** folder.</span></span> <span data-ttu-id="5c842-143">Se denomina TalentMgmt-Azure.zip.</span><span class="sxs-lookup"><span data-stu-id="5c842-143">It is called TalentMgmt-Azure.zip.</span></span> <span data-ttu-id="5c842-144">La siguiente imagen muestra la pantalla correspondiente:</span><span class="sxs-lookup"><span data-stu-id="5c842-144">The following image displays the corresponding screen:</span></span>
 
    ![TalentMgmt en Azure](~/assets/images/tabs/tabs-in-sharepoint/talentmgmt-azure.png)

1. <span data-ttu-id="5c842-146">Puedes ver la pantalla de instalación o consentimiento de la aplicación de administración de talento.</span><span class="sxs-lookup"><span data-stu-id="5c842-146">You can see the install or consent screen for the talent management app.</span></span> <span data-ttu-id="5c842-147">Seleccione el equipo que desea instalar.</span><span class="sxs-lookup"><span data-stu-id="5c842-147">Select the team you want to install.</span></span> 
1. <span data-ttu-id="5c842-148">Selecciona **instalar** e iniciar la experimentación con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5c842-148">Select the **Install** and start experimenting with the app.</span></span>

## <a name="2-use-teams-tab-in-sharepoint"></a><span data-ttu-id="5c842-149">2. Usar la pestaña Teams en SharePoint</span><span class="sxs-lookup"><span data-stu-id="5c842-149">2. Use Teams tab in SharePoint</span></span>

1. <span data-ttu-id="5c842-150">Cargue e implemente el paquete de la aplicación de Teams en el Catálogo de aplicaciones de SharePoint visitando `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` .</span><span class="sxs-lookup"><span data-stu-id="5c842-150">Upload and deploy your Teams app package to your SharePoint App Catalog by visiting `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span> <span data-ttu-id="5c842-151">Por ejemplo, `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span><span class="sxs-lookup"><span data-stu-id="5c842-151">For example, `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span>

1. <span data-ttu-id="5c842-152">Cuando se le solicite, habilite **Hacer que esta solución esté disponible para todos los sitios de la organización**.</span><span class="sxs-lookup"><span data-stu-id="5c842-152">When prompted, enable **Make this solution available to all sites in the organization**.</span></span>
<span data-ttu-id="5c842-153">La siguiente imagen muestra la pantalla correspondiente:</span><span class="sxs-lookup"><span data-stu-id="5c842-153">The following image displays the corresponding screen:</span></span>

   ![Pestañas en la vista sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

1. <span data-ttu-id="5c842-155">En el sitio, cree una nueva página seleccionando el botón de engranaje situado en la parte superior derecha y, a continuación, **seleccione Agregar una página**.</span><span class="sxs-lookup"><span data-stu-id="5c842-155">In your site, create a new page by selecting the gear button at the upper right and then  select **Add a page**.</span></span>
<span data-ttu-id="5c842-156">La siguiente imagen muestra la pantalla correspondiente:</span><span class="sxs-lookup"><span data-stu-id="5c842-156">The following image displays the corresponding screen:</span></span>

   ![Vista de Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

1. <span data-ttu-id="5c842-158">Puede ver la experiencia de creación de páginas de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5c842-158">You can see the SharePoint pages authoring experience.</span></span> <span data-ttu-id="5c842-159">Asigne un nombre a su página **como Pestaña Mis equipos**.</span><span class="sxs-lookup"><span data-stu-id="5c842-159">Name your page as **My Teams Tab**.</span></span>

1. <span data-ttu-id="5c842-160">Abra el cuadro de herramientas del elemento web presionando el botón y seleccione la pestaña `+` Teams, denominada **Contoso HR**.</span><span class="sxs-lookup"><span data-stu-id="5c842-160">Open the web part toolbox by pressing the `+` button, and select your Teams Tab, named **Contoso HR**.</span></span> <span data-ttu-id="5c842-161">Los elementos web se ordenan alfabéticamente.</span><span class="sxs-lookup"><span data-stu-id="5c842-161">Web parts are sorted alphabetically.</span></span> <span data-ttu-id="5c842-162">Si es una lista larga, puede usar la barra de búsqueda para buscarla.</span><span class="sxs-lookup"><span data-stu-id="5c842-162">If it is a long list, you can use the search bar to find it.</span></span> <span data-ttu-id="5c842-163">Esto crea un elemento web en el lienzo que contiene la pestaña Teams. La siguiente imagen muestra la vista de tabulación:</span><span class="sxs-lookup"><span data-stu-id="5c842-163">This creates a web part in the canvas that contains your Teams tab. The following image displays the tab view:</span></span>

   ![Vista de tabulación](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

1. <span data-ttu-id="5c842-165">Presione el **botón Publicar** después de finalizar la edición.</span><span class="sxs-lookup"><span data-stu-id="5c842-165">Press the **Publish** button after you finish  editing.</span></span>

1. <span data-ttu-id="5c842-166">Seleccione **Agregar página a la navegación** para tener una referencia rápida a la página en la barra de navegación izquierda.</span><span class="sxs-lookup"><span data-stu-id="5c842-166">Select **Add page to navigation** to have a quick reference to your page in the left navigation bar.</span></span> <span data-ttu-id="5c842-167">La siguiente imagen muestra la pestaña en Sharepoint:</span><span class="sxs-lookup"><span data-stu-id="5c842-167">The following image displays the tab in Sharepoint:</span></span> 

   ![Ficha en la imagen de Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="3-explore-app-pages-in-sharepoint"></a><span data-ttu-id="5c842-169">3. Explorar páginas de aplicaciones en SharePoint</span><span class="sxs-lookup"><span data-stu-id="5c842-169">3. Explore App Pages in SharePoint</span></span>

<span data-ttu-id="5c842-170">Después de publicar la página, puede explorar cómo convertir la aplicación de Teams en una [experiencia más completa dentro de SharePoint.](/sharepoint/dev/spfx/web-parts/single-part-app-pages)</span><span class="sxs-lookup"><span data-stu-id="5c842-170">After your page is published, you can explore [turning your Teams app into a more complete experience inside SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span></span> <span data-ttu-id="5c842-171">Esto convierte la página actual en una página de aplicación, que muestra el diseño de página normal de SharePoint con una experiencia de página completa para la pestaña Teams.</span><span class="sxs-lookup"><span data-stu-id="5c842-171">This converts the current page into an App Page, showing the normal SharePoint page layout with a full page experience for the Teams tab.</span></span> 

<span data-ttu-id="5c842-172">La siguiente imagen muestra la experiencia completa de la aplicación de Teams en Sharepoint: ![ Imagen de pestañas en Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)</span><span class="sxs-lookup"><span data-stu-id="5c842-172">The following image displays the complete experience of Teams app in Sharepoint: ![Image of Tabs in Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)</span></span>

## <a name="code-sample"></a><span data-ttu-id="5c842-173">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="5c842-173">Code sample</span></span>
| <span data-ttu-id="5c842-174">**Nombre de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="5c842-174">**Sample name**</span></span> | <span data-ttu-id="5c842-175">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="5c842-175">**Description**</span></span> | <span data-ttu-id="5c842-176">**SPFx**</span><span class="sxs-lookup"><span data-stu-id="5c842-176">**SPFx**</span></span> |
|-----------------|-----------------|----------|
| <span data-ttu-id="5c842-177">Elemento web spfx</span><span class="sxs-lookup"><span data-stu-id="5c842-177">SPFx web part</span></span> | <span data-ttu-id="5c842-178">Ejemplos de elementos web de SPFx para pestañas, canales y grupos.</span><span class="sxs-lookup"><span data-stu-id="5c842-178">SPFx web part samples for tabs, channels, and groups.</span></span> | [<span data-ttu-id="5c842-179">View</span><span class="sxs-lookup"><span data-stu-id="5c842-179">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="see-also"></a><span data-ttu-id="5c842-180">Vea también</span><span class="sxs-lookup"><span data-stu-id="5c842-180">See also</span></span>

- [<span data-ttu-id="5c842-181">Creación de la pestaña de Microsoft Teams con SharePoint Framework: tutorial</span><span class="sxs-lookup"><span data-stu-id="5c842-181">Building Microsoft Teams tab using SharePoint Framework - Tutorial</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

- [<span data-ttu-id="5c842-182">Usar páginas de aplicación de elemento único en SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="5c842-182">Using single part app pages in SharePoint Online</span></span>](/sharepoint/dev/spfx/web-parts/single-part-app-pages)

- [<span data-ttu-id="5c842-183">Integrar aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="5c842-183">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)

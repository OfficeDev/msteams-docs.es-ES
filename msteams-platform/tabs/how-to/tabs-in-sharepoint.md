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
# <a name="adding-a-microsoft-teams-tab-in-sharepoint-as-an-spfx-web-part"></a>Agregar una pestaña de Microsoft Teams en SharePoint como elemento web de SPFx

## <a name="rich-integration-between-teams-and-sharepoint"></a>Integración enriquecte entre Teams y SharePoint

Con la versión de noviembre de Teams y SharePoint Framework v. 1.7, los desarrolladores tienen dos capacidades eficaces:

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
                        <h3>Pestañas de Teams en SharePoint</h3>
                        <p>Cree experiencias de aplicación enriqueciendo su aplicación de Teams en SharePoint (este artículo).</p>
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
                        <h3>SharePoint Framework en Teams</h3>
                        <p>Bring your SharePoint web parts to Teams and let SharePoint manage the hosting for you.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a>Pestañas de Teams en SharePoint

Con SharePoint Framework v.1.7, ahora se admite la capacidad para que los desarrolladores tomen sus pestañas de Teams y la alomen en SharePoint. A medida que las pestañas hospedadas en SharePoint obtienen una experiencia de "página completa" similar, exponiendo todas las características de las pestañas de Teams a la vez que conservan el contexto y la familiaridad de un sitio de SharePoint.

### <a name="sharepoint-framework-in-teams"></a>SharePoint Framework en Teams

También puede implementar las pestañas de Microsoft Teams con SharePoint Framework. Para los desarrolladores de SharePoint, esto simplifica significativamente el proceso de desarrollo para las pestañas de Teams porque los elementos web de SharePoint Framework se hospedan en SharePoint sin necesidad de servicios externos como Azure. [Obtenga más información sobre cómo usar SharePoint Framework en Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a>Introducción

Estas instrucciones explicarán cómo puede tomar una pestaña de una aplicación de ejemplo de Microsoft Teams y usarla en SharePoint. Usaremos una pestaña que ya está hospedada en Azure para centrarse en el trabajo de integración necesario.

La aplicación de ejemplo que estamos usando es una aplicación de administración de talento. Administra el proceso de contratación de candidatos para puestos abiertos en un equipo. (La propia aplicación, aunque tiene un aspecto agradable, no hace nada en realidad. Queremos centrarnos en crear una aplicación de Teams y cargarla en Teams, no crear una aplicación de administración de talento real).

### <a name="benefits-of-this-approach"></a>Ventajas de este enfoque

- Llegar a los usuarios de SharePoint con la pestaña de Teams existente
- Cargue el manifiesto de la aplicación directamente en el catálogo de aplicaciones de SharePoint. [Los paquetes de](~/concepts/build-and-test/apps-package.md) aplicaciones de Teams ahora son compatibles con SharePoint
- Los usuarios finales configuran la pestaña en una página como cualquier otro elemento web de SharePoint
- La pestaña puede acceder a su [contexto de](~/tabs/how-to/access-teams-context.md) la mismo forma que cuando se ejecuta dentro de Teams

## <a name="step-1-testing-the-sample-app"></a>Paso 1: Probar la aplicación de ejemplo

Descargue el manifiesto de la aplicación de ejemplo [**desde aquí.**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)

En Microsoft Teams, haga clic en el icono de la Tienda en la esquina inferior izquierda y, a continuación, en "Cargar una aplicación personalizada" en la parte inferior izquierda. El archivo que se va a cargar se ubicará en la carpeta Descargas; se denomina TalentMgmt-Azure.zip. Si todo va bien, verás la pantalla de instalación o consentimiento de la aplicación de administración de talento. Elija el equipo en el que desea instalar y haga clic en el botón Instalar. Ahora puedes experimentar con la aplicación.

## <a name="step-2-using-the-teams-tab-in-sharepoint"></a>Paso 2: Usar la pestaña Teams en SharePoint

Cargue e implemente el paquete de la aplicación de Teams en el Catálogo de aplicaciones de SharePoint visitando `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` , por ejemplo. `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`

Cuando se le pida, habilite "Hacer que esta solución esté disponible para todos los sitios de la organización":

![Pestañas en la vista de SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

En el sitio, cree una nueva página haciendo clic en el botón de engranaje situado en la esquina superior derecha y, a continuación, haga clic en "Agregar una página":

![Vista de SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

Verá la experiencia de creación de páginas de SharePoint. Asigne a su página el nombre "Pestaña Mis equipos".

Abra el cuadro de herramientas del elemento web presionando el botón + y seleccione la pestaña Teams (denominada "Contoso HR"). Los elementos web se ordenan alfabéticamente; si es una lista larga, puede usar la barra de búsqueda para encontrarla. Esto creará un elemento web en el lienzo que contiene la pestaña de Teams:

![Vista de pestaña](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

Presione el botón "Publicar" cuando haya terminado de editar.

Es posible que desee hacer clic en "Agregar página a la navegación" para tener una referencia rápida a la página en la barra de navegación izquierda:

![Pestaña en la imagen de SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="step-3-explore-app-pages-in-sharepoint"></a>Paso 3: Explorar páginas de aplicación en SharePoint

Una vez publicada la página, puede explorar cómo convertir la aplicación teams en una [experiencia más completa dentro de SharePoint.](/sharepoint/dev/spfx/web-parts/single-part-app-pages) Esto convierte la página actual en una página de aplicación, que muestra el diseño de página normal de SharePoint con una experiencia de página completa para la pestaña Teams:

![Imagen de pestañas en SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a>Ejemplo de código
| **Nombre de ejemplo** | **Descripción** | **SPFx** |
|-----------------|-----------------|----------|
| Elemento web de SPFx | Ejemplos de elementos web de SPFx para pestañas, canales y grupos. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="more-information"></a>Más información

- [Creación de la pestaña de Microsoft Teams con SharePoint Framework: tutorial](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
- [Usar páginas de aplicación de elemento único en SharePoint Online](/sharepoint/dev/spfx/web-parts/single-part-app-pages)

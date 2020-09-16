---
title: Adición de una pestaña de Microsoft Teams en SharePoint como un elemento Web de SPFx
author: laujan
description: Cómo implementar la pestaña de Microsoft Teams existente en SharePoint como un elemento Web de SharePoint Framework.
keywords: pestañas de Teams desarrollo de SharePoint Framework
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 2bdc7ab578be485eee33020b3b0c1a4099fd8ade
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818944"
---
# <a name="adding-a-microsoft-teams-tab-in-sharepoint-as-an-spfx-web-part"></a>Adición de una pestaña de Microsoft Teams en SharePoint como un elemento Web de SPFx

> [!IMPORTANT]
> Esta característica se encuentra en versión preliminar en este momento y está sujeta a cambios. No es compatible con el uso en entornos de producción. Sus comentarios y sugerencias sobre esta función son bienvenidos en la [lista de problemas de SharePoint Dev Docs](https://github.com/SharePoint/sp-dev-docs/issues).

## <a name="rich-integration-between-teams-and-sharepoint"></a>Integración enriquecida entre Teams y SharePoint

Con la versión de noviembre de Teams y SharePoint Framework v. 1,7, los desarrolladores tienen dos eficaces capacidades:

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
                        <h3>Pestañas de Microsoft Teams en SharePoint</h3>
                        <p>Cree experiencias de aplicaciones enriquecidas en SharePoint llevando su aplicación de Teams a SharePoint (este artículo).</p>
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
                        <h3>SharePoint Framework en Microsoft Teams</h3>
                        <p>Incorpore los elementos Web de SharePoint a teams y deje que SharePoint administre el hospedaje.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a>Pestañas de Microsoft Teams en SharePoint

Con SharePoint Framework v. 1.7, ahora somos compatibles con la capacidad para que los desarrolladores tomen sus pestañas de Microsoft Teams y la hospeden en SharePoint. Como las pestañas hospedadas en SharePoint obtienen una experiencia similar a "página completa", exponiendo todas las características de las pestañas de Microsoft Teams y conserva el contexto y la familiaridad de un sitio de SharePoint.

### <a name="sharepoint-framework-in-teams"></a>SharePoint Framework en Microsoft Teams

También puede implementar las pestañas de Microsoft Teams con SharePoint Framework. Para los desarrolladores de SharePoint, esto simplifica considerablemente el proceso de desarrollo de las pestañas de Microsoft Teams, ya que los elementos Web de SharePoint Framework se hospedan en SharePoint sin necesidad de servicios externos como Azure. [Obtenga más información sobre el uso de SharePoint Framework en Microsoft Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a>Introducción

Estas instrucciones le explicarán cómo puede tomar una pestaña de una aplicación de ejemplo de Microsoft Teams y usarla en SharePoint. Usaremos una pestaña que ya está hospedada en Azure para centrarse en el trabajo de integración necesario.

La aplicación de ejemplo que estamos usando es una aplicación de administración del talento. Administra el proceso de contratación de candidatos para puestos abiertos en un equipo. (La propia aplicación, aunque parece buena, realmente no hace nada. Queremos centrarnos en la creación de una aplicación de Microsoft Teams y en cargarla en Teams, no crear una aplicación de administración de talento real.)

### <a name="benefits-of-this-approach"></a>Ventajas de este enfoque

- Obtener acceso a los usuarios de SharePoint con la pestaña de Microsoft Teams existente
- Cargue el manifiesto de la aplicación directamente en el catálogo de aplicaciones de SharePoint. Los [paquetes de aplicación de Teams](~/concepts/build-and-test/apps-package.md) ahora son compatibles con SharePoint
- Los usuarios finales configuran la pestaña en una página al igual que cualquier otro elemento Web de SharePoint
- La pestaña puede tener acceso al [contexto](~/tabs/how-to/access-teams-context.md) de la misma manera que cuando se ejecuta dentro de Teams.

## <a name="step-1-testing-the-sample-app"></a>Paso 1: probar la aplicación de ejemplo

Descargue el manifiesto de la aplicación de ejemplo desde [**aquí**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).

En Microsoft Teams, haga clic en el icono de la tienda en la esquina inferior izquierda y, a continuación, "cargar una aplicación personalizada" en la parte inferior izquierda. El archivo que se cargará se ubicará en la carpeta descargas; se llama TalentMgmt-Azure.zip. Si todo va bien, verá la pantalla de instalación/consentimiento de la aplicación de administración del talento. Elija el equipo en el que desea instalar y haga clic en el botón instalar. Ahora tiene la libertad de experimentar con la aplicación.

## <a name="step-2-using-the-teams-tab-in-sharepoint"></a>Paso 2: uso de la pestaña Microsoft Teams en SharePoint

Para cargar e implementar el paquete de la aplicación Microsoft Teams en el catálogo de aplicaciones de SharePoint `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` , visite, por ejemplo, `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` .

Cuando se le solicite, habilite "hacer que esta solución esté disponible en todos los sitios de la organización":

![Pestañas en la vista de SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

En el sitio, cree una página nueva haciendo clic en el botón de engranaje situado en la esquina superior derecha y, a continuación, "agregar una página":

![Vista de SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

Verá la experiencia de creación de páginas de SharePoint. Asigne a la página el nombre "mi pestaña de Microsoft Teams".

Abra el cuadro de herramientas del elemento Web presionando el botón + y seleccione la pestaña Microsoft Teams (denominada "Contoso HR"). Los elementos Web se ordenan alfabéticamente; Si se trata de una lista larga, puede usar la barra de búsqueda para encontrarla. Se creará un elemento Web en el lienzo que contiene la pestaña de Microsoft Teams:

![Vista de pestaña](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

Haga clic en el botón "publicar" cuando termine la edición.

Puede que quiera hacer clic en "agregar página a navegación" para tener una referencia rápida a la página en la barra de navegación izquierda:

![Pestaña en imagen de SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="step-3-explore-app-pages-in-sharepoint"></a>Paso 3: explorar las páginas de la aplicación en SharePoint

Una vez publicada la página, puede explorar [la conversión de la aplicación de Microsoft Teams en una experiencia más completa dentro de SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages). Esto convierte la página actual en una página de la aplicación, que muestra el diseño de página de SharePoint normal con una experiencia de página completa para la pestaña Microsoft Teams:

![Imagen de pestañas en SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="more-information"></a>Más información

- [Creación de la pestaña de Microsoft Teams con SharePoint Framework: tutorial](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
- [Usar páginas de aplicación de elemento único en SharePoint Online](/sharepoint/dev/spfx/web-parts/single-part-app-pages)

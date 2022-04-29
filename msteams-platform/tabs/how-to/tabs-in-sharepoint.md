---
title: Añadir una pestaña de Teams a SharePoint
author: surbhigupta
description: Obtenga información sobre cómo implementar la pestaña de Teams existente en SharePoint como un elemento web de SharePoint Framework mediante ejemplos de código.
keywords: pestañas de teams de desarrollo de SharePoint Framework
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: c11356750f78a015c8d404f519f45476f947b80a
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111692"
---
# <a name="add-teams-tab-to-sharepoint"></a>Añadir una pestaña de Teams a SharePoint

Puede obtener una experiencia de integración enriquecida entre Microsoft Teams y SharePoint agregando una pestaña de Microsoft Teams en SharePoint como un elemento web SPFx. Este documento le guía sobre cómo tomar una pestaña de una aplicación de ejemplo de Microsoft Teams y usarla en SharePoint.

## <a name="rich-integration-between-teams-and-sharepoint"></a>Integración enriquecida entre Teams y SharePoint

Con la versión de noviembre de Teams y SharePoint Framework v.1.7, los desarrolladores tienen dos capacidades eficaces:

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
                        <p>Cree experiencias de aplicación enriquecidas en SharePoint incorporando su aplicación de Teams a SharePoint (este artículo).</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li>
    <a href="/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab">
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
                        <p>Traiga sus elementos web de SharePoint a Teams y deje que SharePoint administre el hospedaje automáticamente.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a>Pestañas de Teams en SharePoint

Con SharePoint Framework v.1.7, puede hospedar las pestañas de Teams en SharePoint. A medida que las pestañas hospedadas en SharePoint obtienen una experiencia de **página completa** similar, que expone todas las características de las pestañas de Teams y conserva el contexto y la familiaridad de un sitio de SharePoint.

### <a name="sharepoint-framework-in-teams"></a>SharePoint Framework en Teams

También puede implementar las pestañas de Microsoft Teams con SharePoint Framework. Los elementos web de SharePoint Framework se hospedan en SharePoint sin necesidad de servicios externos, como Azure. Para los desarrolladores de SharePoint, esto simplifica significativamente el proceso de desarrollo de las pestañas de Teams. Para obtener más información sobre SharePoint Framework en Teams, vea [cómo usar SharePoint Framework en Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a>Introducción

La pestaña que se usa aquí ya está hospedada en Azure para centrarse en el trabajo de integración necesario.

La aplicación de ejemplo que se usa es una aplicación de administración de talento. Administra el proceso de contratación de candidatos para puestos abiertos en un equipo. Cree una aplicación de Teams de ejemplo y cárguela en Teams. No cree una aplicación de administración de talento real.

### <a name="benefits-of-this-approach"></a>Ventajas de este enfoque

* Llegue a los usuarios de SharePoint con la pestaña de Teams existente.
* Cargue el manifiesto de la aplicación directamente en el catálogo de aplicaciones de SharePoint. [Paquetes da aplicación de Teams](~/concepts/build-and-test/apps-package.md) ahora son compatibles con SharePoint.
* Los usuarios configuran la pestaña en una página igual que cualquier otro elemento web de SharePoint.
* La pestaña puede acceder a su [contexto](~/tabs/how-to/access-teams-context.md) igual que puede, cuando se ejecuta dentro de Teams.

Para agregar la pestaña Teams a SharePoint, siga estos pasos para agregar la pestaña Teams a SharePoint:

## <a name="1-test-the-sample-app"></a>1. Probar la aplicación de ejemplo

Descargue el [manifiesto de aplicación de ejemplo](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).

1. Abra Microsoft Teams.
1. Seleccione el icono **Appstore** en la parte inferior izquierda de la pestaña lateral.
1. Seleccione **Cargar una aplicación personalizada** en la parte inferior izquierda. En la imagen siguiente se muestra la pantalla correspondiente:  

    ![cargar una aplicación personalizada](~/assets/images/tabs/tabs-in-sharepoint/upload-custom-app.png)

1. El archivo que se va a cargar se encuentra en la carpeta **Descargas** Se denomina TalentMgmt-Azure.zip. En la imagen siguiente se muestra la pantalla correspondiente:

    ![TalentMgmt en Azure](~/assets/images/tabs/tabs-in-sharepoint/talentmgmt-azure.png)

1. Puede ver la pantalla de instalación o consentimiento de la aplicación de administración de talento. Seleccione el equipo que desea instalar.
1. Seleccione **Instalar** y empiece a experimentar con la aplicación.

## <a name="2-use-teams-tab-in-sharepoint"></a>2. Usar la pestaña Teams en SharePoint

1. Cargue e implemente el paquete de la aplicación de Teams en el catálogo de aplicaciones de SharePoint visitando `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`. Por ejemplo, `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.

1. Cuando se le solicite, habilite **Haga que esta solución esté disponible para todos los sitios de la organización**.
En la imagen siguiente se muestra la pantalla correspondiente:

   ![Pestañas en la vista de SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

1. En el sitio, cree una página seleccionando el botón de engranaje situado en la esquina superior derecha y, a continuación, seleccione **Agregar una página**.
En la imagen siguiente se muestra la pantalla correspondiente:

   ![Vista de SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

1. Puede ver la experiencia de creación de páginas de SharePoint. Asigne un nombre a la página como **Pestaña Mis equipos**.

1. Abra el cuadro de herramientas del elemento web seleccionando el botón `+` y seleccione la pestaña Teams, denominada **RR. HH. DE Contoso**. Los elementos web se ordenan alfabéticamente. Si es una lista larga, puede usar la barra de búsqueda para encontrarla. Esto crea un elemento web en el lienzo que contiene la pestaña Teams. En la imagen siguiente se muestra la vista de pestaña:

   ![Vista de pestaña](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

1. Seleccione el botón **Publicar** después de finalizar la edición.

1. Seleccione **Agregar página a la navegación** para tener una referencia rápida a la página en la barra de navegación izquierda.
En la imagen siguiente se muestra la pestaña en SharePoint:

   ![Pestaña en la imagen de SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="3-explore-app-pages-in-sharepoint"></a>3. Explorar páginas de aplicaciones en SharePoint

Una vez publicada la página, puede explorar [convertir la aplicación de Teams en una experiencia más completa dentro de SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages). Esto convierte la página actual en una página de la aplicación, mostrando el diseño de página de SharePoint normal con una experiencia de página completa para la pestaña Teams.

En la imagen siguiente se muestra la experiencia completa de la aplicación Teams en SharePoint: ![Imagen de pestañas en SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a>Ejemplo de código

| **Ejemplo de nombre** | **Descripción** | **SPFx** |
|-----------------|-----------------|----------|
| Elemento web SPFx | Ejemplos de elementos web de SPFx para pestañas, canales y grupos. | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="see-also"></a>Consulte también

* [Creación de la pestaña de Microsoft Teams con SharePoint Framework: tutorial](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
* [Usar páginas de aplicación de elemento único en SharePoint Online](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
* [Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)

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
# <a name="add-teams-tab-to-sharepoint"></a>Añadir una pestaña de Teams a SharePoint 

Puede obtener una amplia experiencia de integración entre Microsoft Teams y SharePoint agregando una pestaña de Microsoft Teams en SharePoint como un elemento web de SPFx. Este documento le guía sobre cómo tomar una pestaña de una aplicación de ejemplo de Microsoft Teams y usarla en SharePoint. 

## <a name="rich-integration-between-teams-and-sharepoint"></a>Integración enriquecte entre Teams y SharePoint

Con la versión de noviembre de Teams y SharePoint Framework v.1.7, los desarrolladores tienen dos funciones eficaces:

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
                        <p>Cree experiencias de aplicación enriquecciones en SharePoint llevando la aplicación de Teams a Sharepoint (en este artículo).</p>
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
                        <p>Lleve los elementos web de SharePoint a Teams y deje que SharePoint administre el hospedaje por usted.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a>Pestañas de Teams en SharePoint

Con SharePoint Framework v.1.7, puede hospedar las pestañas de Teams en SharePoint. A medida que las pestañas hospedadas en SharePoint obtienen una experiencia de página completa **similar,** exponiendo todas las características de las pestañas de Teams a la vez que conservan el contexto y la familiaridad de un sitio de SharePoint.

### <a name="sharepoint-framework-in-teams"></a>SharePoint Framework en Teams

También puede implementar las pestañas de Microsoft Teams con SharePoint Framework. Los elementos web de SharePoint Framework se hospedan en SharePoint sin necesidad de servicios externos, como Azure. Para los desarrolladores de SharePoint, esto simplifica significativamente el proceso de desarrollo de las pestañas de Teams. Para obtener más información sobre SharePoint Framework en Teams, vea [cómo usar SharePoint Framework en Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a>Introducción

La pestaña usada aquí ya está hospedada en Azure, para centrarse en el trabajo de integración necesario.

La aplicación de ejemplo que se usa es una aplicación de administración de talento. Administra el proceso de contratación de candidatos para puestos abiertos en un equipo. Crea una aplicación de Teams de ejemplo y cárbala en Teams. No cree una aplicación de administración de talento real.

### <a name="benefits-of-this-approach"></a>Ventajas de este enfoque

* Llegue a los usuarios de SharePoint con la pestaña Teams existente.
* Cargue el manifiesto de la aplicación directamente en el catálogo de aplicaciones de SharePoint. [Los paquetes de](~/concepts/build-and-test/apps-package.md) aplicaciones de Teams ahora son compatibles con SharePoint.
* Los usuarios configuran la pestaña en una página como cualquier otro elemento web de SharePoint.
* La pestaña puede tener acceso a [su contexto](~/tabs/how-to/access-teams-context.md) del mismo modo que cuando se ejecuta dentro de Teams.

**Para agregar la pestaña Teams a SharePoint**

Realice los siguientes pasos para agregar la pestaña Teams a SharePoint:

## <a name="1-test-the-sample-app"></a>1. Probar la aplicación de ejemplo

Descargue el [manifiesto de la aplicación de ejemplo](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).

1. Abra Microsoft Teams.
1. Seleccione el **icono de la Appstore** en la parte inferior izquierda de la ficha lateral.
1. Selecciona **Cargar una aplicación personalizada** en la parte inferior izquierda. La siguiente imagen muestra la pantalla correspondiente:  

    ![cargar una aplicación personalizada](~/assets/images/tabs/tabs-in-sharepoint/upload-custom-app.png)

1. El archivo que se va a cargar se encuentra en la **carpeta Descargas.** Se denomina TalentMgmt-Azure.zip. La siguiente imagen muestra la pantalla correspondiente:
 
    ![TalentMgmt en Azure](~/assets/images/tabs/tabs-in-sharepoint/talentmgmt-azure.png)

1. Puedes ver la pantalla de instalación o consentimiento de la aplicación de administración de talento. Seleccione el equipo que desea instalar. 
1. Selecciona **instalar** e iniciar la experimentación con la aplicación.

## <a name="2-use-teams-tab-in-sharepoint"></a>2. Usar la pestaña Teams en SharePoint

1. Cargue e implemente el paquete de la aplicación de Teams en el Catálogo de aplicaciones de SharePoint visitando `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` . Por ejemplo, `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.

1. Cuando se le solicite, habilite **Hacer que esta solución esté disponible para todos los sitios de la organización**.
La siguiente imagen muestra la pantalla correspondiente:

   ![Pestañas en la vista sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

1. En el sitio, cree una nueva página seleccionando el botón de engranaje situado en la parte superior derecha y, a continuación, **seleccione Agregar una página**.
La siguiente imagen muestra la pantalla correspondiente:

   ![Vista de Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

1. Puede ver la experiencia de creación de páginas de SharePoint. Asigne un nombre a su página **como Pestaña Mis equipos**.

1. Abra el cuadro de herramientas del elemento web presionando el botón y seleccione la pestaña `+` Teams, denominada **Contoso HR**. Los elementos web se ordenan alfabéticamente. Si es una lista larga, puede usar la barra de búsqueda para buscarla. Esto crea un elemento web en el lienzo que contiene la pestaña Teams. La siguiente imagen muestra la vista de tabulación:

   ![Vista de tabulación](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

1. Presione el **botón Publicar** después de finalizar la edición.

1. Seleccione **Agregar página a la navegación** para tener una referencia rápida a la página en la barra de navegación izquierda. La siguiente imagen muestra la pestaña en Sharepoint: 

   ![Ficha en la imagen de Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="3-explore-app-pages-in-sharepoint"></a>3. Explorar páginas de aplicaciones en SharePoint

Después de publicar la página, puede explorar cómo convertir la aplicación de Teams en una [experiencia más completa dentro de SharePoint.](/sharepoint/dev/spfx/web-parts/single-part-app-pages) Esto convierte la página actual en una página de aplicación, que muestra el diseño de página normal de SharePoint con una experiencia de página completa para la pestaña Teams. 

La siguiente imagen muestra la experiencia completa de la aplicación de Teams en Sharepoint: ![ Imagen de pestañas en Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a>Ejemplo de código
| **Nombre de ejemplo** | **Descripción** | **SPFx** |
|-----------------|-----------------|----------|
| Elemento web spfx | Ejemplos de elementos web de SPFx para pestañas, canales y grupos. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="see-also"></a>Vea también

- [Creación de la pestaña de Microsoft Teams con SharePoint Framework: tutorial](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

- [Usar páginas de aplicación de elemento único en SharePoint Online](/sharepoint/dev/spfx/web-parts/single-part-app-pages)

- [Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)

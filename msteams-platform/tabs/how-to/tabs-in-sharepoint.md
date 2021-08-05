---
title: Añadir una pestaña de Teams a SharePoint
author: surbhigupta
description: Cómo implementar la pestaña de Teams existente para SharePoint como un SharePoint Framework web.
keywords: desarrollo de sharepoint framework de pestañas de teams
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 6a9eead19685afb41c71e57cb44c7608973db1ad
ms.sourcegitcommit: ec79bbbc3a8daa1ad96de809fc6d17367e8f0c6b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/04/2021
ms.locfileid: "53726918"
---
# <a name="add-teams-tab-to-sharepoint"></a>Añadir una pestaña de Teams a SharePoint 

Puede obtener una experiencia de integración enriquecida entre Microsoft Teams y SharePoint agregando una pestaña Microsoft Teams en SharePoint como elemento web SPFx web. Este documento te guía sobre cómo tomar una pestaña de una Microsoft Teams de ejemplo y usarla en SharePoint. 

## <a name="rich-integration-between-teams-and-sharepoint"></a>Integración enriquec Teams y SharePoint

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
                        <h3>Teams Pestañas en SharePoint</h3>
                        <p>Crea experiencias de aplicación enrique SharePoint mediante la Teams aplicación a SharePoint (en este artículo).</p>
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
                        <p>Lleve sus SharePoint web a Teams y deje que SharePoint el hospedaje por usted.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a>Teams pestañas en SharePoint

Con SharePoint Framework v.1.7, puede hospedar las pestañas de Teams en SharePoint. A medida que las pestañas hospedadas en SharePoint obtienen una experiencia de página completa **similar,** exponiendo todas las características de las pestañas Teams conservando el contexto y la familiaridad de un SharePoint sitio.

### <a name="sharepoint-framework-in-teams"></a>SharePoint Framework en Teams

También puede implementar las pestañas Microsoft Teams con SharePoint Framework. SharePoint Framework los elementos web se hospedan en SharePoint sin necesidad de servicios externos, como Azure. Para SharePoint desarrolladores, esto simplifica significativamente el proceso de desarrollo de Teams pestañas. Para obtener más información sobre SharePoint Framework en Teams, vea cómo usar el [SharePoint Framework en Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a>Introducción

La pestaña usada aquí ya está hospedada en Azure, para centrarse en el trabajo de integración necesario.

La aplicación de ejemplo que se usa es una aplicación de administración de talento. Administra el proceso de contratación de candidatos para puestos abiertos en un equipo. Crea un ejemplo Teams aplicación y cárbala en Teams. No cree una aplicación de administración de talento real.

### <a name="benefits-of-this-approach"></a>Ventajas de este enfoque

* Llegue SharePoint usuarios con la pestaña de Teams existente.
* Upload el manifiesto de la aplicación directamente al catálogo SharePoint aplicación. [Teams paquetes de](~/concepts/build-and-test/apps-package.md) aplicaciones ahora son compatibles con SharePoint.
* Los usuarios configuran la pestaña en una página como cualquier otro elemento SharePoint web.
* La pestaña puede tener acceso a [su contexto](~/tabs/how-to/access-teams-context.md) del mismo modo que puede, cuando se ejecuta dentro de Teams.

**Para agregar Teams pestaña a SharePoint**

Realice los siguientes pasos para agregar Teams pestaña a SharePoint:

## <a name="1-test-the-sample-app"></a>1. Probar la aplicación de ejemplo

Descargue el [manifiesto de la aplicación de ejemplo](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).

1. Abra Microsoft Teams.
1. Seleccione el **icono de la Appstore** en la parte inferior izquierda de la ficha lateral.
1. Selecciona **Upload una aplicación personalizada** en la parte inferior izquierda. La siguiente imagen muestra la pantalla correspondiente:  

    ![cargar una aplicación personalizada](~/assets/images/tabs/tabs-in-sharepoint/upload-custom-app.png)

1. El archivo que se va a cargar se encuentra en la **carpeta Descargas.** Se denomina TalentMgmt-Azure.zip. La siguiente imagen muestra la pantalla correspondiente:
 
    ![TalentMgmt en Azure](~/assets/images/tabs/tabs-in-sharepoint/talentmgmt-azure.png)

1. Puedes ver la pantalla de instalación o consentimiento de la aplicación de administración de talento. Seleccione el equipo que desea instalar. 
1. Selecciona **instalar** e iniciar la experimentación con la aplicación.

## <a name="2-use-teams-tab-in-sharepoint"></a>2. Use Teams pestaña en SharePoint

1. Upload e implemente el paquete Teams aplicación en su catálogo de aplicaciones SharePoint de aplicaciones visitando `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` . Por ejemplo, `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.

1. Cuando se le solicite, habilite **Hacer que esta solución esté disponible para todos los sitios de la organización**.
La siguiente imagen muestra la pantalla correspondiente:

   ![Pestañas en la vista sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

1. En el sitio, cree una nueva página seleccionando el botón de engranaje situado en la parte superior derecha y, a continuación, **seleccione Agregar una página**.
La siguiente imagen muestra la pantalla correspondiente:

   ![Vista de Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

1. Puede ver la experiencia de SharePoint de creación de páginas. Asigne a la página el nombre **Mi Teams Tab**.

1. Abra el cuadro de herramientas del elemento web seleccionando el botón y seleccione la pestaña `+` Teams, denominada **Contoso HR**. Los elementos web se ordenan alfabéticamente. Si es una lista larga, puede usar la barra de búsqueda para buscarla. Esto crea un elemento web en el lienzo que contiene la Teams pestaña. La siguiente imagen muestra la vista de tabulación:

   ![Vista de tabulación](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

1. Seleccione el **botón Publicar** después de finalizar la edición.

1. Seleccione **Agregar página a la navegación** para tener una referencia rápida a la página en la barra de navegación izquierda. La siguiente imagen muestra la pestaña en Sharepoint: 

   ![Ficha en la imagen de Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="3-explore-app-pages-in-sharepoint"></a>3. Explorar páginas de aplicaciones en SharePoint

Después de publicar la página, puedes explorar cómo convertir la aplicación Teams en una [experiencia más completa dentro de SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages). Esto convierte la página actual en una página de aplicación, que muestra el diseño SharePoint página normal con una experiencia de página completa para la pestaña Teams aplicación. 

La siguiente imagen muestra la experiencia completa de Teams aplicación en SharePoint: ![ Imagen de pestañas en Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a>Ejemplo de código
| **Ejemplo de nombre** | **Descripción** | **SPFx** |
|-----------------|-----------------|----------|
| SPFx elemento web | SPFx ejemplos de elementos web para pestañas, canales y grupos. | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="see-also"></a>Consulte también

* [Creación de la pestaña de Microsoft Teams con SharePoint Framework: tutorial](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
* [Usar páginas de aplicación de elemento único en SharePoint Online](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
* [Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)

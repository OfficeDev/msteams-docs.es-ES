---
title: Preparar el envío de la tienda
description: Describe los pasos finales antes de enviar la aplicación Microsoft Teams que aparecerá en la tienda.
ms.topic: how-to
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 975d3ef8fc8bdc8d6d7c336cf3a61a3a42ef5315
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566036"
---
# <a name="prepare-your-microsoft-teams-store-submission"></a>Prepare el envío de su tienda Microsoft Teams

Ha diseñado, creado y probado su aplicación Microsoft Teams. Ahora estás listo para enumerarlo para que la gente pueda descubrirlo y empezar a usar tu aplicación.

Antes de enviar la aplicación al [Centro de partners,](/office/dev/store/use-partner-center-to-submit-to-appsource)asegúrate de haber hecho lo siguiente.

## <a name="validate-your-app-package"></a>Valida el paquete de la aplicación

Aunque la aplicación puede estar funcionando en un entorno de prueba, debe comprobar el paquete de la aplicación para evitar tener problemas durante el proceso de envío.

La herramienta de validación de aplicaciones Microsoft Teams le ayuda a identificar y solucionar problemas antes de enviarla al Centro de partners. La herramienta comprueba automáticamente las configuraciones de la aplicación con los mismos casos de prueba utilizados durante la validación de la tienda.

1. Vaya a la [herramienta de validación de aplicaciones Microsoft Teams](https://dev.teams.microsoft.com/appvalidation.html). (Nota: La herramienta también está disponible en [App Studio](../../../build-and-test/app-studio-overview.md).)
1. Upload el paquete de la aplicación para ejecutar las pruebas automatizadas.
1. Vaya a la **lista de verificación preliminar** y revise los casos de prueba que son difíciles de automatizar.
1. [Corrija problemas con sus configuraciones](~/resources/schema/manifest-schema.md) o aplicación en general si las pruebas automatizadas le dan errores o no ha cumplido todos los criterios de la lista de comprobación.

## <a name="compile-testing-instructions"></a>Compilar instrucciones de prueba

Proporcione instrucciones y recursos para ayudar a los revisores a probar la aplicación, incluidas las cuentas de prueba, las credenciales y las claves de licencia. Puede agregar instrucciones en el Centro de partners o cargarlas en una ubicación disponible públicamente en SharePoint.

### <a name="feature-list"></a>Lista de características

Proporcione detalles sobre las capacidades de la aplicación en Teams y los pasos para probar cada una de ellas.

### <a name="accounts"></a>Cuentas

Debe proporcionar cuentas de prueba si la aplicación requiere una licencia o una lista segura de back-end. Todas las cuentas que proporcione deben incluir datos rellenados previamente para facilitar las pruebas.

Dependiendo de las características de la aplicación, es posible que deba proporcionar todo lo siguiente:

* Cuenta de administrador (obligatorio)
* Cuenta no administrativa (obligatorio)
* Una cuenta que no está preconfigurada para probar correctamente la experiencia de inicio de sesión de la primera ejecución (necesaria)
* Una cuenta con acceso a funciones premium o actualizadas (si corresponde)
* Dos cuentas del mismo inquilino para probar la experiencia de colaboración de las aplicaciones que funcionan en contextos compartidos (si corresponde)

### <a name="tenant-configurations"></a>Configuraciones de inquilinos

Si debe configurar un inquilino Teams para usar la aplicación, incluya esas instrucciones y cuentas de administrador y no administrador para la validación.

### <a name="video-optional"></a>Vídeo (opcional)

Proporcione una grabación de la aplicación para que Microsoft pueda comprender completamente su funcionalidad.

## <a name="create-your-store-listing-details"></a>Crea los detalles de tu tienda

La información que envías al [Centro de partners](https://partner.microsoft.com)&#8212;incluido tu nombre, descripciones, iconos e imágenes&#8212;se convierte en la tienda Teams y la lista de Microsoft AppSource para la aplicación.

Un anuncio de tienda puede ser la primera impresión de alguien de tu aplicación. Aumente las instalaciones con un listado que transmita eficazmente los beneficios, la funcionalidad y la marca de la aplicación.

### <a name="specify-a-short-name"></a>Especifique un nombre corto

El nombre de la aplicación (específicamente, su [*nombre corto)*](~/resources/schema/manifest-schema.md#name)juega un papel crucial en la forma en que los usuarios la descubren en la tienda.

:::row:::

   :::column span="3":::
      :::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="La captura de pantalla de ejemplo resalta dónde se muestra el nombre corto de una aplicación en un listado de tienda.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

Asegúrese de que su nombre corto se adhiere a las directrices de validación de la [tienda.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#11-app-name)

### <a name="write-descriptions"></a>Escribir descripciones

Debe tener una descripción corta y larga de la aplicación.

#### <a name="short-description"></a>La descripción breve

Un resumen conciso de la aplicación que debe ser original, atractivo y dirigido a su público objetivo. Mantenga la breve descripción en una oración.

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="La captura de pantalla del ejemplo resalta dónde se muestra la breve descripción de una aplicación en una lista de la tienda.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

Asegúrese de que la breve descripción se adhiere a las directrices de validación de la [tienda.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#431-short-description)

#### <a name="long-description"></a>La descripción larga

La descripción larga puede proporcionar una narrativa que resalta las principales características de la aplicación, los problemas que resuelve y su público objetivo. Aunque esta descripción puede tener hasta 4.000 caracteres, la mayoría de los usuarios solo leerán entre 300 y 500 palabras.

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/LongDescription-02.png" alt-text="La captura de pantalla de ejemplo resalta dónde se muestra la descripción larga de una aplicación en un listado de tienda.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

Asegúrese de que la descripción larga se adhiere a las directrices de validación de la [tienda.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#432-long-description)

### <a name="adhere-to-icon-design-guidelines"></a>Cumplir con las directrices de diseño de iconos

Los iconos son uno de los principales elementos que los usuarios ven al navegar por la tienda. Los iconos deben comunicar la marca y el propósito de la aplicación, al tiempo que se adhieren a los requisitos Teams.

Para obtener más información, consulte [instrucciones sobre cómo crear iconos de Teams aplicación.](~/concepts/build-and-test/apps-package.md#app-icons)

### <a name="capture-screenshots"></a>Captura de pantalla de capturas de pantalla

Las capturas de pantalla proporcionan una vista previa visual destacada de la aplicación para complementar el nombre, el icono y las descripciones de la aplicación.

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/Screenshot-01.png" alt-text="Ejemplo de captura de pantalla resalta dónde se muestran las capturas de pantalla de la aplicación en un listado de la tienda.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

Recuerde lo siguiente acerca de las capturas de pantalla:

* Puede tener hasta cinco capturas de pantalla por anuncio.
* Los tipos de archivo compatibles incluyen PNG, JPEG y GIF.
* Las dimensiones deben ser de 1366x768 píxeles.
* Tamaño máximo de 1.024 KB.

Para obtener las prácticas recomendadas, consulte los siguientes recursos:

* [Teams las directrices de validación de la tienda](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#44-screenshots)
* [Crear imágenes eficaces para las tiendas de aplicaciones de Microsoft](/office/dev/store/craft-effective-appsource-store-images)

### <a name="create-a-video"></a>Crear un vídeo

Un vídeo de tu anuncio puede ser la forma más eficaz de comunicar por qué las personas deben usar tu aplicación. Debe abordar las siguientes preguntas en un vídeo:

* Quién es su aplicación para?
* ¿Qué problemas puede resolver la aplicación?
* ¿Cómo funciona la aplicación?
* ¿Qué otros beneficios obtienes al usar tu aplicación?

#### <a name="best-practices-for-videos"></a>Mejores prácticas para vídeos

* Mantén tu vídeo entre 30 y 90 segundos.
* Apunta a la calidad. En un anuncio, los usuarios verán el vídeo antes de las capturas de pantalla.

### <a name="select-a-category-for-your-app"></a>Selecciona una categoría para tu aplicación

Durante el envío, se te pedirá que clasifiques la aplicación. En la tabla siguiente se asignan categorías de almacén Teams a las categorías enumeradas en [el Centro de partners](https://aka.ms/PartnerCenterHomePage).

| categorías de Teams       | Categorías del Centro de Partners  |
|:---------------------|:---------------|
| Análisis y BI | Análisis, visualización de datos y BI |
| Desarrollador e TI | Herramientas para desarrolladores, administrador de TI |
| Educación | Educación |
| Recursos humanos | Recursos Humanos y Reclutamiento |
| Productividad | Gestión de contenidos, archivos y documentos, productividad, formación y tutoriales, y utilidades |
| Administración de proyectos | Comunicación, administración de Project, flujo de trabajo y administración de empresas |
| Ventas y apoyo | Gestión de clientes y contactos, atención al cliente, gestión financiera, ventas y marketing |
| Social y divertido | Galerías de imágenes y vídeos, estilo de vida, noticias y tiempo, social, viajes y navegación |

### <a name="localize-your-store-listing"></a>Localiza tu anuncio de tienda

Partner Center admite [listados de tiendas localizadas.](/office/dev/store/prepare-localized-solutions) Para obtener más información, consulta [cómo localizar la lista de aplicaciones de Teams.](../../../../concepts/build-and-test/apps-localization.md)

## <a name="complete-publisher-verification"></a>Verificación completa de Publisher

[Publisher Se](/azure/active-directory/develop/publisher-verification-overview) requiere verificación para Teams aplicaciones que aparecen en la tienda. Para obtener más información, consulta [las preguntas más frecuentes,](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions) [cómo marcar la aplicación como editor verificado](/azure/active-directory/develop/mark-app-as-publisher-verified)y solucionar problemas de verificación [del editor.](/azure/active-directory/develop/troubleshoot-publisher-verification)

## <a name="complete-publisher-attestation"></a>Atestación Publisher completa

[Publisher Attestation](/microsoft-365-app-certification/docs/attestation) también es necesario para Teams aplicaciones que aparecen en la tienda. El proceso incluye completar una autoevaluación de las prácticas de seguridad, control de datos y cumplimiento de la aplicación que pueden ayudar a los clientes potenciales a tomar decisiones informadas sobre el uso de la aplicación.

> [!NOTE]
> Si envías una nueva aplicación, no podrás completar oficialmente Publisher Attestation hasta que la aplicación aparezca en la tienda de Teams. Si estás actualizando una aplicación listada, completa Publisher Attestation antes de enviar la versión más reciente de la aplicación para su validación.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Enviar la aplicación](/office/dev/store/add-in-submission-guide)

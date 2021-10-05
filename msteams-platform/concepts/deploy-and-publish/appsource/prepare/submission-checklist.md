---
title: Preparar el envío de la tienda
description: Describe los pasos finales antes de enviar Microsoft Teams aplicación para que aparezca en la tienda.
ms.topic: how-to
ms.localizationpriority: medium
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: a01d08e4d1892109395a541522a0bb12e1a9c2e2
ms.sourcegitcommit: 6573881f7e69d8e5ec8861f54df84e7d519f0511
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/04/2021
ms.locfileid: "60096566"
---
# <a name="prepare-your-microsoft-teams-store-submission"></a>Preparar el envío Microsoft Teams almacén

Has diseñado, creado y probado tu Microsoft Teams aplicación. Ahora estás listo para enumerar para que los usuarios puedan descubrir y empezar a usar la aplicación.

Antes de enviar la aplicación al [Centro de partners,](/office/dev/store/use-partner-center-to-submit-to-appsource)asegúrate de que has hecho lo siguiente.

## <a name="validate-your-app-package"></a>Validar el paquete de la aplicación

Aunque la aplicación puede estar funcionando en un entorno de prueba, debes comprobar el paquete de la aplicación para evitar que se presenten problemas durante el proceso de envío.

> [!NOTE]
>  App Studio pronto se depricará. Configurar, distribuir y administrar las aplicaciones Teams con el nuevo [Portal de desarrolladores](https://dev.teams.microsoft.com/)

La Microsoft Teams de validación de aplicaciones te ayuda a identificar y solucionar problemas antes de enviarte al Centro de partners. La herramienta comprueba automáticamente las configuraciones de la aplicación en los mismos casos de prueba usados durante la validación de la tienda.

1. Ve a [Microsoft Teams de validación de aplicaciones en](https://dev.teams.microsoft.com/validation) el portal de desarrolladores. 
    > [!NOTE]
    > La herramienta de validación de aplicaciones también está disponible en [App Studio](../../../build-and-test/app-studio-overview.md).
1. Upload el paquete de la aplicación para ejecutar las pruebas automatizadas.
1. Vaya a la **lista de comprobación preliminar** y revise los casos de prueba que son difíciles de automatizar.
1. [Se solucionan problemas con las configuraciones](~/resources/schema/manifest-schema.md) o la aplicación en general. Estos problemas se producen si las pruebas automatizadas le dan errores o no ha cumplido todos los criterios de la lista de comprobación.

## <a name="compile-testing-instructions"></a>Compilar instrucciones de prueba

Proporcione instrucciones y recursos para ayudar a los revisores a probar la aplicación, como:
* Cuentas de prueba
* Credenciales
* Claves de licencia

Puede agregar instrucciones en el Centro de partners o cargarlas en una ubicación disponible públicamente en SharePoint.

### <a name="feature-list"></a>Lista de características

Proporciona detalles sobre las capacidades de la aplicación en Teams y los pasos para probar cada una de ellas.

### <a name="accounts"></a>Cuentas

Proporcione cuentas de prueba si la aplicación requiere una licencia o una lista segura de back-end. Todas las cuentas que proporciones deben incluir datos rellenados previamente para ayudar en las pruebas.

Según las características de la aplicación, es posible que deba proporcionar todas las siguientes cuentas:

* Cuenta de administrador (obligatorio)
* Cuenta que no es de administrador (obligatorio)
* Una cuenta que no está preconfigurado para probar correctamente la experiencia de inicio de sesión de primera ejecución (obligatorio)
* Una cuenta con acceso a características premium o actualizadas (si procede)
* Dos cuentas en el mismo inquilino para probar la experiencia de colaboración de aplicaciones que funcionan en contextos compartidos (si procede)

### <a name="tenant-configurations"></a>Configuraciones de inquilinos

Si debes configurar un inquilino Teams para usar la aplicación, incluye esas instrucciones y cuentas de administrador y no administrador para la validación.

### <a name="video-optional"></a>Vídeo (opcional)

Proporciona una grabación de la aplicación para que Microsoft pueda comprender completamente su funcionalidad.

## <a name="create-your-store-listing-details"></a>Crear los detalles de la descripción de la tienda

La información que envías al Centro de partners [&#8212;](https://partner.microsoft.com) incluyendo tu nombre, descripciones, iconos e imágenes&#8212;se convierte en la tienda Teams y la descripción de Microsoft AppSource para tu aplicación.

Una descripción de la tienda puede ser la primera impresión de alguien de la aplicación. Aumente las instalaciones con una descripción que transmita eficazmente las ventajas, la funcionalidad y la marca de la aplicación.

### <a name="specify-a-short-name"></a>Especificar un nombre corto

El nombre de la aplicación (específicamente, su [*nombre*](~/resources/schema/manifest-schema.md#name)corto) desempeña un papel fundamental en la forma en que los usuarios lo descubren en la tienda.

:::row:::

   :::column span="3":::
      :::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="La captura de pantalla de ejemplo resalta dónde se muestra el nombre corto de una aplicación en una descripción de la tienda.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

Asegúrese de que su nombre corto se adhiera a las [directrices de validación de la tienda.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#app-name)

### <a name="write-descriptions"></a>Escribir descripciones

Debe tener una descripción corta y larga de su aplicación.

#### <a name="short-description"></a>Descripción breve

Un resumen conciso de la aplicación que debe ser original, atractivo y dirigido a la audiencia de destino. Limite la descripción a una sola frase.

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="La captura de pantalla de ejemplo resalta dónde se muestra la breve descripción de una aplicación en una descripción de la tienda.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

Asegúrese de que su breve descripción se adhiera a las [directrices de validación de la tienda.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#short-description)

#### <a name="long-description"></a>Descripción larga

La descripción larga puede proporcionar una descripción que resalte las aplicaciones:

* Características principales
* Los problemas que resuelve
* Público objetivo

Aunque esta descripción puede tener hasta 4 000 caracteres, la mayoría de los usuarios sólo leerán entre 300 y 500 palabras.

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/LongDescription-02.png" alt-text="Destaca la captura de pantalla de ejemplo donde se muestra la descripción larga de una aplicación en una descripción de la tienda.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

Asegúrese de que la descripción larga se adhiera a las [directrices de validación de la tienda.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#long-description)

### <a name="adhere-to-icon-design-guidelines"></a>Cumplir las directrices de diseño de iconos

Los iconos son uno de los elementos principales que los usuarios ven al navegar por la tienda. Los iconos deben comunicar la marca y el propósito de la aplicación, al tiempo que se adhieren a Teams requisitos.

Para obtener más información, consulta las instrucciones para [crear Teams iconos de la aplicación](~/concepts/build-and-test/apps-package.md#app-icons).

### <a name="capture-screenshots"></a>Capturar capturas de pantalla

Las capturas de pantalla proporcionan una destacada vista previa de su aplicación para complementar el nombre, el icono y las descripciones de la misma.

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/Screenshot-01.png" alt-text="Destaca la captura de pantalla de ejemplo en la que las capturas de pantalla de la aplicación se muestran en una descripción de la tienda.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

Recuerde los siguientes procedimientos recomendados sobre capturas de pantalla:

* Puede tener hasta cinco capturas de pantalla por anuncio.
* Los tipos de archivo admitidos son PNG, JPEG y GIF.
* Las dimensiones deben ser de 1366x768 píxeles.
* Tamaño máximo de 1 024 KB.

Para obtener los procedimientos recomendados, consulte los siguientes recursos:

* [Teams Directrices de validación de la Tienda](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#screenshots)
* [Crear imágenes eficaces para almacenes de aplicaciones de Microsoft](/office/dev/store/craft-effective-appsource-store-images)

### <a name="create-a-video"></a>Crear un vídeo

Un vídeo de la descripción puede ser la forma más eficaz de comunicar por qué las personas deben usar la aplicación. En un vídeo, se abordan las siguientes preguntas:

* Quién Cuál es tu aplicación?
* ¿Qué problemas puede resolver la aplicación?
* ¿Cómo funciona la aplicación?
* ¿Qué otras ventajas obtienes al usar la aplicación?

Puedes agregar una dirección URL para el vídeo de YouTube o Vimeo.

#### <a name="best-practices-for-videos"></a>Procedimientos recomendados para vídeos

* Mantenga el vídeo entre 60 y 90 segundos.
* Apunta a la calidad. En una descripción, los usuarios verán el vídeo antes de las capturas de pantalla.
* Comunicar el valor del producto en forma narrativa.
* Muestra cómo funciona el producto.

### <a name="select-a-category-for-your-app"></a>Seleccionar una categoría para la aplicación

Durante el envío, se te pide que clasifices tu aplicación. En la tabla siguiente se Teams categorías de la Tienda a las categorías enumeradas en [el Centro de partners](https://aka.ms/PartnerCenterHomePage).

| Teams categorías       | Categorías del Centro de partners  |
|:---------------------|:---------------|
| Análisis e BI | Análisis, visualización de datos e BI |
| Desarrollador y IT | Herramientas para desarrolladores, administrador de TI |
| Educación | Educación |
| Recursos humanos | Recursos humanos y contratación |
| Productividad | Administración de contenido, archivos y documentos, productividad, aprendizaje y tutoriales y utilidades |
| Administración de proyectos | Administración de Project, flujo de trabajo y administración empresarial |
| Ventas y soporte técnico | Administración de clientes y contactos, soporte al cliente, administración financiera y ventas y marketing |
| Social y divertido | Galerías de imágenes y vídeo, Estilo de vida, Noticias y Tiempo, Social, Viajes y Navegación |

### <a name="localize-your-store-listing"></a>Localización de la descripción de la tienda

El Centro de partners admite [listados de almacenes localizados.](/office/dev/store/prepare-localized-solutions) Para obtener más información, [consulta cómo encontrar la descripción](../../../../concepts/build-and-test/apps-localization.md)Teams aplicación .

## <a name="complete-publisher-verification"></a>Verificación Publisher completa

[Publisher se requiere](/azure/active-directory/develop/publisher-verification-overview) la verificación de Teams aplicaciones enumeradas en la tienda. Para obtener más información, consulte [las preguntas más frecuentes](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions), [cómo marcar su aplicación como verificada por el editor](/azure/active-directory/develop/mark-app-as-publisher-verified), y [cómo solucionar el problema de la verificación del editor](/azure/active-directory/develop/troubleshoot-publisher-verification).

## <a name="complete-publisher-attestation"></a>Certificación Publisher completa

[Publisher atestación también](/microsoft-365-app-certification/docs/attestation) es necesaria para Teams aplicaciones enumeradas en la Tienda. El proceso incluye completar una autoevaluación de las prácticas de seguridad, control de datos y cumplimiento de la aplicación. El proceso puede ayudar a los clientes potenciales a tomar decisiones fundamentadas sobre el uso de la aplicación.

> [!NOTE]
> Si vas a enviar una nueva aplicación, no puedes completar oficialmente Publisher atestación hasta que la aplicación aparezca en la Teams tienda. Si estás actualizando una aplicación enumerada, completa Publisher atestación antes de enviar la versión más reciente de la aplicación para su validación.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Enviar la aplicación](/office/dev/store/add-in-submission-guide)

---
title: Preparar el envío de la tienda
description: Pasos finales antes de enviar la aplicación de Microsoft Teams para que aparezca en la tienda. Valide el paquete de la aplicación y complete la comprobación y la atestación del publicador.
ms.topic: how-to
ms.localizationpriority: high
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: bec6c900a0f478b2243685215f094b9a051c44f1
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560683"
---
# <a name="prepare-your-teams-store-submission"></a>Preparar el envío de la tienda de Microsoft Teams

Has diseñado, creado y probado tu aplicación de Microsoft Teams. Ahora estás listo para describirla y que los usuarios puedan descubrir la aplicación y empezar a usarla.

Vea el siguiente vídeo para obtener más información sobre cómo publicar la aplicación en la tienda de aplicaciones de Microsoft Teams:
<br>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4WG3l]
<br>

Antes de enviar la aplicación al [Centro de partners](/office/dev/store/use-partner-center-to-submit-to-appsource), debe asegurarse de haber hecho lo siguiente.

## <a name="validate-your-app-package"></a>Validar el paquete de la aplicación

Aunque la aplicación puede estar funcionando en un entorno de prueba, debes comprobar el paquete de la aplicación para evitar que se presenten problemas durante el proceso de envío.

La herramienta de validación de aplicaciones de Microsoft Teams ayuda a identificar y solucionar problemas antes de enviarlos al Centro de partners. La herramienta comprueba automáticamente las configuraciones de la aplicación en los mismos casos de prueba usados durante la validación de la tienda.

1. Vaya a la [herramienta de validación de aplicaciones de Microsoft Teams](https://dev.teams.microsoft.com/appvalidation.html).

   También puede validar la aplicación mediante [el Portal para desarrolladores para Teams.](~/concepts/build-and-test/teams-developer-portal.md)

1. Carga el paquete de la aplicación para ejecutar las pruebas automatizadas.
1. Vaya a la **lista de comprobación preliminar** y revise los casos de prueba que son difíciles de automatizar.
1. [Fix issues with your configurations](~/resources/schema/manifest-schema.md) or app in general. These issues occur if the automated tests give you errors or you haven't met all the criteria in the checklist.

## <a name="compile-testing-instructions"></a>Compilar instrucciones de prueba

Proporciona instrucciones y recursos para ayudar a los revisores a probar la aplicación, como:

* Cuentas de prueba
* Credenciales
* Claves de licencia

Puedes agregar instrucciones en el Centro de partners o cargarlas en una ubicación disponible públicamente en SharePoint.

### <a name="feature-list"></a>Lista de características

Proporciona detalles sobre las capacidades de la aplicación en Teams y los pasos para probar cada una de ellas.

### <a name="accounts"></a>Cuentas

Proporciona cuentas de prueba si la aplicación requiere una licencia o una lista segura de backend. Todas las cuentas que proporciones deben incluir datos previamente rellenados para ayudar en las pruebas.

Según las características de la aplicación, es posible que debas proporcionar todas las siguientes cuentas:

* Cuenta de administrador (obligatorio)
* Cuenta que no es de administrador (obligatorio)
* Una cuenta no preconfigurada para probar correctamente la experiencia de inicio de sesión de primera ejecución (obligatorio)
* Una cuenta con acceso a características premium o actualizadas (si procede)
* Dos cuentas en el mismo inquilino para probar la experiencia de colaboración de aplicaciones que funcionan en contextos compartidos (si procede)

### <a name="tenant-configurations"></a>Configuraciones de inquilinos

Si debes configurar un inquilino de Teams para usar la aplicación, incluye esas instrucciones y cuentas de administrador y no administrador para la validación.

### <a name="video-optional"></a>Vídeo (opcional)

Proporciona una grabación de la aplicación para que Microsoft pueda comprender completamente su funcionalidad.

## <a name="create-your-store-listing-details"></a>Crea los detalles de la descripción de la tienda

La información que envías al [Centro de partners](https://partner.microsoft.com)&#8212;incluyendo tu nombre, descripciones, iconos e imágenes&#8212;se convierte en la descripción de la tienda de Teams y Microsoft AppSource para la aplicación.

Una descripción de la tienda puede ser la primera impresión de alguien de la aplicación. Aumente las instalaciones con una descripción que transmita eficazmente las ventajas, la funcionalidad y la marca de la aplicación.

### <a name="specify-a-short-name"></a>Especificar un nombre corto

El nombre de la aplicación (específicamente, su *[nombre corto](~/resources/schema/manifest-schema.md#name)*) desempeña un papel fundamental en la forma en que los usuarios lo descubren en la tienda.

:::row:::

:::column span="3":::
:::image type="content" source="../../../../assets/images/store-detail-page/specifying-short-name-under-submission.png" alt-text="La captura de pantalla de ejemplo destaca dónde se muestra el nombre corto de una aplicación en una descripción de la tienda.":::
:::column-end:::
:::column span="1":::
:::column-end:::

:::row-end:::

Asegúrese de que el nombre corto se cumple las [directrices de validación de la tienda](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#app-name).

### <a name="write-descriptions"></a>Escribir descripciones

Debe tener una descripción corta y larga de su aplicación.

#### <a name="short-description"></a>Descripción breve

A concise summary of your app that should be original, engaging, and directed at your target audience. Keep the short description to one sentence.

:::row:::

:::column span="3":::
:::image type="content" source="~/assets/images/store-detail-page/specifying-short-description-under-submission.png" alt-text="La captura de pantalla de ejemplo resalta dónde se muestra la descripción corta de una aplicación en una descripción de la tienda.":::
:::column-end:::
:::column span="1":::
:::column-end:::

:::row-end:::

Asegúrese de que la descripción corta cumple las [directrices de validación de la tienda](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#short-description).

#### <a name="long-description"></a>Descripción larga

La descripción larga puede proporcionar una descripción que resalte estos aspectos de las aplicaciones:

* Características principales
* Los problemas que resuelve
* Público objetivo

Aunque esta descripción puede tener hasta 4 000 caracteres, la mayoría de los usuarios sólo leerán entre 300 y 500 palabras.

:::row:::

:::column span="3":::
:::image type="content" source="~/assets/images/store-detail-page/specifying-long-description-under-submission.png" alt-text="La captura de pantalla de ejemplo destaca dónde se muestra la descripción larga de una aplicación en una descripción de la tienda.":::
:::column-end:::
:::column span="1":::
:::column-end:::

:::row-end:::

Asegúrese de que la descripción larga cumple a las [directrices de validación de la tienda](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#long-description).

### <a name="adhere-to-icon-design-guidelines"></a>Cumplir las directrices de diseño de iconos

Los iconos son uno de los elementos principales que los usuarios ven cuando navegan por la tienda. Sus iconos deben comunicar la marca y el propósito de su aplicación, y también cumplir los requisitos de Teams.

Para obtener más información, consulte [Instrucciones para crear iconos de aplicaciones de Teams](~/concepts/build-and-test/apps-package.md#app-icons).

### <a name="capture-screenshots"></a>Capturas de pantalla

Las capturas de pantalla proporcionan una destacada vista previa de su aplicación para complementar el nombre, el icono y las descripciones de la misma.

:::row:::

:::column span="3":::
:::image type="content" source="~/assets/images/store-detail-page/specifying-of-capturing-screenshots-submission.png" alt-text="La captura de pantalla de ejemplo destaca dónde se muestran las capturas de pantalla de la aplicación en una descripción de la tienda.":::
:::column-end:::
:::column span="1":::
:::column-end:::

:::row-end:::

Recuerde los siguientes procedimientos recomendados sobre las capturas de pantalla:

* Puede tener hasta cinco capturas de pantalla por anuncio.
* Los tipos de archivo admitidos incluyen formatos de imagen .png, .jpeg y gif.
* Las dimensiones deben ser de 1366 x 768 píxeles.
* Tamaño máximo de 1 024 KB.

Para conocer los procedimientos recomendados, consulte los siguientes recursos:

* [Directrices de validación de la tienda de Teams](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#screenshots)
* [Crear imágenes eficaces para tiendas de aplicaciones de Microsoft](/office/dev/store/craft-effective-appsource-store-images)

### <a name="create-a-video"></a>Crear un vídeo

A video in your listing can be the most effective way to communicate why people should use your app. Address the following questions in a video:

* ¿Para quién es la aplicación?
* ¿Qué problemas puede resolver la aplicación?
* ¿Cómo funciona la aplicación?
* ¿Qué otras ventajas se obtienen al usar la aplicación?

Puede agregar una dirección URL para el vídeo de YouTube o Vimeo.

#### <a name="best-practices-for-videos"></a>Procedimientos recomendados para vídeos

* Mantenga el vídeo entre 60 y 90 segundos.
* Aim for quality. In a listing, users will see your video before screenshots.
* Comunique el valor del producto de forma narrativa.
* Muestre cómo funciona el producto.

### <a name="select-a-category-for-your-app"></a>Seleccionar una categoría para la aplicación

Durante el envío, se le pedirá que clasifique la aplicación. Puede clasificar la aplicación en función de las siguientes categorías:

|Categories  |
|--------------|
| Microsoft |
| Education |
| Productividad |
| Imágenes & galerías de vídeos |
| Administración de proyectos |
| Utilidades |
| Social |
| Comunicación |
| Administración de contenido |
| Archivos & documentos |
| Administración de flujos de trabajo & empresariales |
| TI/Administración |
| Recursos humanos & contratación|
| Herramientas de desarrollo |
| Programación de reuniones & |
| Visualización de datos & BI |
| Tutorial de & de entrenamiento |
| Noticias & el tiempo |
| Asistencia al cliente |
| Referencia |
| Marketing & ventas |
| Apariencia & |
| Administración de contactos & cliente (CRM) |
| Administración financiera |
| Fuentes de & de Mapas |
| Otros |

### <a name="localize-your-store-listing"></a>Localización de la descripción de la tienda

El Centro de partners admite [descripciones de tiendas localizadas](/office/dev/store/prepare-localized-solutions). Para obtener más información, consulte [cómo localizar la descripción de su aplicación de Teams.](../../../../concepts/build-and-test/apps-localization.md)

## <a name="complete-publisher-verification"></a>Completar la verificación de Publisher

[La verificación de Publisher](/azure/active-directory/develop/publisher-verification-overview) es necesaria para las aplicaciones de Teams que aparecen en la tienda. Para obtener más información, consulte [las preguntas más frecuentes](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions), [cómo marcar su aplicación como verificada por el editor](/azure/active-directory/develop/mark-app-as-publisher-verified), y [cómo solucionar el problema de la verificación del editor](/azure/active-directory/develop/troubleshoot-publisher-verification).

## <a name="complete-publisher-attestation"></a>Completar la atestación de Publisher

La [atestación de Publisher](/microsoft-365-app-certification/docs/attestation) también es necesaria para las aplicaciones de Teams que aparecen en la tienda. El proceso incluye completar una autoevaluación de las prácticas de seguridad, control de datos y cumplimiento de la aplicación. El proceso puede ayudar a los clientes potenciales a tomar decisiones fundamentadas sobre el uso de la aplicación.

> [!NOTE]
> Si presenta una nueva aplicación, no puede completar oficialmente la atestación de Publisher hasta que la aplicación aparezca en la tienda de Teams. Si está actualizando una aplicación de la lista, complete la atestación de Publisher antes de enviar la última versión de la aplicación para su validación.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Enviar la aplicación](/office/dev/store/add-in-submission-guide)

## <a name="see-also"></a>Vea también

[Resolver problemas si se produce un error en el envío de la tienda de Microsoft Teams](~/concepts/deploy-and-publish/appsource/resolve-submission-issues.md)

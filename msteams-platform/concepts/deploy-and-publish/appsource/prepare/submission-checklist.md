---
title: Lista de comprobación de envíos
description: La lista de comprobación que se debe usar antes de publicar la aplicación de Microsoft Teams en AppSource
keywords: preparación del envío de la lista de comprobación de publicación de Office de Microsoft Teams
ms.openlocfilehash: 3379fe670c9835c1f2223067592d9574fff83a69
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2020
ms.locfileid: "44801486"
---
# <a name="prepare-for-appsource-submission"></a>Preparar el envío de AppSource  

Para que aparezcan en AppSource, la aplicación debe pasar por un proceso de aprobación. Este es un servicio gratuito proporcionado por el grupo de Microsoft teams que comprueba que la aplicación funciona como se describe, contiene todos los metadatos adecuados y proporciona contenido que sería valioso para un usuario final. Para ayudarle a conseguir una aprobación rápida, asegúrese de que su aplicación cumple los siguientes requisitos y directrices:

* **Método de distribución:** Asegúrese de que la aplicación está diseñada para una tienda. Hay [otras opciones](../../overview.md) para distribuir la aplicación sin publicarla en AppSource.
* **Página de detalles de la aplicación:** La aplicación cumple la [lista de comprobación de página de detalles de aplicación](detail-page-checklist.md)
* **Sugerencias y casos con errores frecuentes:** Preste especial atención a estos [consejos y a los casos con errores frecuentes](frequently-failed-cases.md) para mejorar el envío de la aplicación al tiempo de aprobación.
* **Manifiesto de la aplicación:** Comprobar el manifiesto de la aplicación en la [lista de comprobación del manifiesto](app-manifest-checklist.md) de la aplicación y el comprobador de manifiesto en App Studio
* **Pruebas y depuración:** Ha [probado y depurado completamente la aplicación](../../../build-and-test/debug.md).
* **Directivas de validación:** Debe pasar todas [las directivas de validación de AppSource](https://docs.microsoft.com/legal/marketplace/certification-policies#1140-teams) actuales para los bots y las pestañas de Teams. Tenga en cuenta que estas directivas están sujetas a cambios.
* **Notas de prueba:** Incluir [notas de prueba para la validación](#test-notes-for-validation)
* **Directivas de privacidad:** Asegúrese de que la [Directiva de privacidad, las condiciones de uso y las direcciones URL de soporte](#privacy-policy-terms-of-use-and-support-urls) sigan nuestras instrucciones.

Una vez que haya completado todos los requisitos anteriores, puede enviar el paquete al origen de la aplicación a través del [centro de asociados](/office/dev/store/use-partner-center-to-submit-to-appsource).

## <a name="privacy-policy-terms-of-use-and-support-urls"></a>Directiva de privacidad, condiciones de uso y URL de soporte técnico

### <a name="privacy-policy"></a>Directiva de privacidad

Directrices de la Directiva de privacidad:
* La Directiva de privacidad puede ser específica de la aplicación o el complemento o una directiva global para todos los servicios. 
* Si usa una directiva de privacidad genérica, debe hacer referencia a "servicios, aplicaciones y plataformas" para abarcar la aplicación de Microsoft Teams, así como el sitio Web. 
* Debe incluir la forma en que se administra el almacenamiento de datos de usuario, la retención de datos de usuario, la eliminación y la información de controles de seguridad.
* Debe incluir su información de contacto.
* No debe contener vínculos rotos, URL de versiones beta o direcciones URL provisionales. 

### <a name="terms-of-use"></a>Términos de uso

La instrucción de uso de términos de uso debe ser específica y aplicable a la aplicación o a la oferta de complementos.

### <a name="support-urls"></a>Admitir direcciones URL

Las direcciones URL de soporte técnico no deben requerir autenticación ni credencial de inicio de sesión para ponerse en contacto con usted en busca de problemas con la aplicación.

## <a name="test-notes-for-validation"></a>Notas de prueba para validación

Por ejemplo, incluya lo siguiente:

* Debe proporcionar al menos dos credenciales de inicio de sesión, un administrador y un usuario no administrador.

* Para fines de comprobación, las cuentas que proporcione deben tener suficientes datos rellenados previamente.

* Para las aplicaciones empresariales, las aplicaciones en las que se necesita una suscripción o las aplicaciones en las que hay una dependencia de inquilino/dominio de Office 365, debe proporcionar una tercera cuenta en el mismo dominio que no está preconfigurada para la aplicación, de modo que podamos validar la experiencia de usuario de primera ejecución.

* Si la aplicación tiene características Premium o actualizada, se debe proporcionar una cuenta con el acceso necesario para probar dicha experiencia.

* Puede elegir cargar las notas de prueba en SharePoint. Si es así, indique un vínculo público al archivo.

* **Cuentas de prueba**. Se requiere una cuenta de prueba si la aplicación solo permite cuentas de licencia o listas blancas desde el back-end. Además, si hay un ámbito de chat de equipo o grupo permitido en la aplicación, se necesitan dos cuentas de prueba en el mismo inquilino para validar el escenario de colaboración del equipo.

* **Pasos de integración**. Si se requiere la configuración previa de un administrador de inquilinos para usar la aplicación, incluya los pasos o proporcione cuentas de administrador y de no administrador para la validación. Nota: puede registrarse para obtener una suscripción al [programa de desarrolladores de Office 365](https://developer.microsoft.com/microsoft-365/dev-program) . Es *gratuita* durante 90 días y se renovará continuamente siempre que la use para la actividad de desarrollo.

* **Notas sobre las características de la aplicación en Microsoft Teams**: detalle todas las funcionalidades que ofrece la aplicación en Microsoft Teams y los pasos para probar cada característica.

* **Vídeo que muestra la funcionalidad de la aplicación (opcional)**: puede proporcionar una grabación de vídeo del producto para que podamos comprender completamente la funcionalidad de la aplicación.




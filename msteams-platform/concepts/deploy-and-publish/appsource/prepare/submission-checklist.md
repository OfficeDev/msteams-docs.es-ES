---
title: Lista de comprobación de envíos
description: La lista de comprobación que se debe usar antes de publicar la aplicación de Microsoft Teams en AppSource
keywords: Teams publicar lista de comprobación de publicación de Office Teams Teams AppSource validación de aplicaciones
ms.openlocfilehash: 1b25a449901c303269334e5cea6de46fa3b6f6e5
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796305"
---
# <a name="prepare-for-appsource-submission"></a>Preparar el envío de AppSource  

Para que aparezcan en AppSource, la aplicación debe pasar por un proceso de aprobación. Este es un servicio gratuito proporcionado por el grupo de Microsoft teams que comprueba que la aplicación funciona como se describe, contiene todos los metadatos adecuados y proporciona contenido que sería valioso para un usuario final. Para ayudarle a conseguir una aprobación rápida, asegúrese de que su aplicación cumple los siguientes requisitos y directrices:

* **Método de distribución:** Asegúrese de que la aplicación está diseñada para su publicación en una plataforma de tienda. Hay [otras opciones](../../overview.md) para distribuir la aplicación sin publicarla en AppSource.
* **Directivas de validación:** La aplicación debe pasar todas [las directivas de validación de AppSource](https://docs.microsoft.com/legal/marketplace/certification-policies#1140-teams) actuales antes de enviarse. Tenga en cuenta que estas directivas están sujetas a cambios. 
* * * Autoprueba la aplicación con la [herramienta de validación del manifiesto](#teams-app-validation-tool) .
* **Página de detalles de la aplicación:** La aplicación debe alinearse con la  [lista de comprobación de página de detalles](detail-page-checklist.md)de la aplicación.
* **Sugerencias y casos con errores frecuentes:** Preste especial atención a las sugerencias de la lista y a los [casos con errores frecuentes](frequently-failed-cases.md)  para mejorar el tiempo de envío y aprobación de la aplicación.
* **Manifiesto de la aplicación:** Compruebe el manifiesto de la aplicación con la [lista de comprobación del manifiesto](app-manifest-checklist.md)de la aplicación.
* **Pruebas y depuración:** Asegúrese de que ha [probado y depurado completamente la aplicación](../../../build-and-test/debug.md).
* **Notas de prueba:** Incluir las [notas de prueba para la validación](#test-notes-for-validation)
* **Directivas de privacidad:** Asegúrese de que la [Directiva de privacidad, las condiciones de uso y las direcciones URL de soporte](#privacy-policy-terms-of-use-and-support-urls) sigan nuestras instrucciones.

Una vez que haya completado todos los requisitos anteriores, envíe el paquete a AppSource a través del [centro de asociados](/office/dev/store/use-partner-center-to-submit-to-appsource).

## <a name="teams-app-validation-tool"></a>Herramienta de validación de aplicaciones de Microsoft Teams

La herramienta de validación de aplicaciones consta de un [validador de aplicaciones](#teams-app-validator) y una [lista de comprobación preliminar](#preliminary-checklist). La herramienta replica los mismos casos de prueba usados por [AppSource](/office/dev/store/submit-to-appsource-via-partner-center) para evaluar el envío de la aplicación. Por lo tanto, es crucial pasar todos los casos de prueba antes de enviar la solución a AppSource para su aprobación. La herramienta se puede encontrar en varias áreas dentro de la plataforma de Microsoft Teams:

> [!div class="checklist"]
>
> * [**Página principal del validador de aplicaciones**](https://dev.teams.microsoft.com/appvalidation.html)
> * [**Teams Visual Studio Code Toolkit**](/toolkit/visual-studio-code-overview.md)
> * [**App Studio**](/concepts/build-and-test/app-studio-overview.md)

### <a name="teams-app-validator"></a>Validador de aplicaciones de Microsoft Teams

La página **validar** permite comprobar el paquete de la aplicación antes de enviarla a AppSource. Simplemente cargue el paquete de la aplicación y la herramienta de validación comprobará la aplicación en todos los casos de prueba relacionados con el manifiesto. Para cada prueba con errores, la descripción proporciona un vínculo de documentación para ayudarle a corregir el error.

![Herramienta de validación](../../../../assets/images/validation-tool/validator.png)

### <a name="preliminary-checklist"></a>Lista de comprobación preliminar

Para los escenarios de prueba que son difíciles de automatizar, las superficies de lista de comprobación preliminares son siete de los casos de prueba con errores más comunes.

![Lista de comprobación preliminar](../../../../assets/images/validation-tool/preliminary-checklist.png)

## <a name="privacy-policy-terms-of-use-and-support-urls"></a>Directiva de privacidad, condiciones de uso y URL de soporte técnico

### <a name="privacy-policy"></a>Directiva de privacidad

Directrices de la Directiva de privacidad:

> [!div class="checklist"]
>
> * La Directiva de privacidad puede ser específica de su aplicación o de una directiva global para todos sus servicios.
> * Si usa una directiva de privacidad genérica, debe hacer referencia a "servicios", "aplicaciones" y "plataformas" para incluir la aplicación de Microsoft Teams, así como el sitio Web.
> * Debe incluir cómo controlar el almacenamiento de datos de usuario, la retención de datos de usuario, la eliminación y los controles de seguridad.
> * Debe incluir su información de contacto.
> * No debe contener vínculos rotos, URL de versiones beta o direcciones URL provisionales.

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

* **Cuentas de prueba** . Se requiere una cuenta de prueba si la aplicación solo permite cuentas con licencia o safelisting del back-end. Además, si hay un ámbito de chat de equipo o grupo permitido en la aplicación, se necesitan dos cuentas de prueba en el mismo inquilino para validar el escenario de colaboración del equipo.

* **Pasos de integración** . Si se requiere la configuración previa de un administrador de inquilinos para usar la aplicación, incluya los pasos o proporcione cuentas de administrador y de no administrador para la validación. Nota: puede registrarse para obtener una suscripción al [programa de desarrolladores de Office 365](https://developer.microsoft.com/microsoft-365/dev-program) . Es *gratuita* durante 90 días y se renovará continuamente siempre que la use para la actividad de desarrollo.

* **Notas sobre las características de la aplicación en Microsoft Teams** : detalle todas las funcionalidades que ofrece la aplicación en Microsoft Teams y los pasos para probar cada característica.

* **Vídeo que muestra la funcionalidad de la aplicación (opcional)** : puede proporcionar una grabación de vídeo del producto para que podamos comprender completamente la funcionalidad de la aplicación.

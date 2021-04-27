---
title: Lista de comprobación de envío de la Tienda
description: La lista de comprobación que se debe usar antes de publicar la aplicación de Microsoft Teams en AppSource
ms.topic: reference
localization_priority: Normal
keywords: Validación de aplicaciones de aplicación de envío de aplicaciones de Teams para publicar listas de comprobación de publicación de la tienda de teams
ms.openlocfilehash: 1e7698e143d313ce46b834eada608571e3280b8a
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020789"
---
# <a name="prepare-for-appsource-submission"></a>Preparar el envío de AppSource  

Para aparecer en AppSource, la aplicación debe pasar por un proceso de aprobación. Este es un servicio gratuito proporcionado por el grupo de Microsoft Teams que comprueba que la aplicación funciona como se describe, contiene todos los metadatos adecuados y proporciona contenido que sería valioso para un usuario final. Para ayudarte a lograr una aprobación rápida, asegúrate de que la aplicación cumple los siguientes requisitos y directrices:

* **Método de distribución:** Asegúrate de que la aplicación está pensada para su publicación en una plataforma de la tienda. Hay [otras opciones para](../../overview.md) distribuir la aplicación sin publicarla en AppSource.
* **Directivas de validación:** La aplicación debe pasar todas las directivas de validación [actuales de AppSource antes](https://docs.microsoft.com/legal/marketplace/certification-policies#1140-teams) del envío. 
  > [!NOTE] 
  > Las directivas de validación de Appsource están sujetas a cambios.
* **Preparación móvil:** La aplicación debe tener capacidad de respuesta móvil. Si la aplicación contiene pestañas, [](~/tabs/design/tabs-mobile.md) deben seguir las directrices de diseño móvil y la aplicación [no](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#-mobile-responsiveness-no-direct-upsell-or-payment) debe cumplir los requisitos de ventas emergentes en el sistema operativo móvil (iOS y Android).
* **Prueba tu aplicación de forma personal:** Pruebe la aplicación con la [herramienta de validación manifiesto](#teams-app-validation-tool).
* **Página de detalles de la aplicación:** La aplicación debe alinearse con la  [lista de comprobación de página de detalles de la aplicación](detail-page-checklist.md).
* **Sugerencias y casos con frecuencia con errores:** Preste especial atención a las sugerencias enumeradas y [a los casos](frequently-failed-cases.md)  con frecuencia con errores para mejorar el tiempo de envío y aprobación de la aplicación.
* **Manifiesto de la aplicación:** Comprueba el manifiesto de la aplicación en la [lista de comprobación del manifiesto de la aplicación.](app-manifest-checklist.md)
* **Pruebas y depuración:** Asegúrese de que ha probado [y depurado completamente la aplicación](../../../build-and-test/debug.md).
* **Notas de prueba:** Incluir las [notas de prueba para la validación](#test-notes-for-validation)
* **Directivas de privacidad:** Asegúrese de [que la directiva de privacidad, los términos de uso y las direcciones URL de soporte técnico](#privacy-policy-terms-of-use-and-support-urls) siguen nuestras directrices.

Una vez que haya completado todos los requisitos anteriores, envíe el paquete a AppSource a través del [Centro de partners](/office/dev/store/use-partner-center-to-submit-to-appsource).

## <a name="teams-app-validation-tool"></a>Herramienta de validación de aplicaciones de Teams

La herramienta de validación de aplicaciones consta de un [validador de](#teams-app-validator) aplicaciones y una [lista de comprobación preliminar.](#preliminary-checklist) La herramienta replica los mismos casos de prueba usados por [AppSource](/office/dev/store/submit-to-appsource-via-partner-center) para evaluar el envío de la aplicación. Por lo tanto, es fundamental pasar todos los casos de prueba antes de enviar la solución a AppSource para su aprobación. La herramienta se puede encontrar en varias áreas dentro de la plataforma de Teams:

> [!div class="checklist"]
>
> * [**Página principal del validador de aplicaciones**](https://dev.teams.microsoft.com/appvalidation.html)
> * [**Kit de herramientas Visual Studio código de Teams**](/toolkit/visual-studio-code-overview.md)
> * [**App Studio**](../../../build-and-test/app-studio-overview.md)

### <a name="teams-app-validator"></a>Validador de aplicaciones de Teams

La **página Validar** te permite comprobar el paquete de la aplicación antes de enviarlo a AppSource. Simplemente cargue el paquete de la aplicación y la herramienta de validación comprobará la aplicación en todos los casos de prueba relacionados con el manifiesto. Para cada prueba con errores, la descripción proporciona un vínculo de documentación que le ayudará a corregir el error.

![Herramienta de validación](../../../../assets/images/validation-tool/validator.png)

### <a name="preliminary-checklist"></a>Lista de comprobación preliminar

Para escenarios de prueba difíciles de automatizar, la lista de comprobación preliminar muestra siete de los casos de prueba con errores más comunes.

![Lista de comprobación preliminar](../../../../assets/images/validation-tool/preliminary-checklist.png)

## <a name="privacy-policy-terms-of-use-and-support-urls"></a>Directiva de privacidad, términos de uso y direcciones URL de soporte técnico

### <a name="privacy-policy"></a>Directiva de privacidad

Directrices de directiva de privacidad:

> [!div class="checklist"]
>
> * La directiva de privacidad puede ser específica de la aplicación o una directiva general para todos los servicios.
> * Si usa una directiva de privacidad genérica, debe hacer referencia a "servicios", "aplicaciones" y "plataformas" para incluir la aplicación de Teams, así como su sitio web.
> * Debe incluir cómo controlar el almacenamiento de datos de usuario, la retención de datos de usuario, la eliminación y los controles de seguridad.
> * Debe incluir su información de contacto.
> * No debe contener vínculos rotos, direcciones URL beta ni direcciones URL provisionales.

### <a name="terms-of-use"></a>Términos de uso

La declaración de términos de uso debe ser específica y aplicable a la oferta de aplicaciones o complementos.

### <a name="support-urls"></a>Direcciones URL de soporte técnico

Las direcciones URL de soporte técnico no deben requerir autenticación o credencial de inicio de sesión para ponerse en contacto con usted para cualquier problema con la aplicación.

## <a name="test-notes-for-validation"></a>Notas de prueba para la validación

Incluya lo siguiente:

* Debe proporcionar al menos dos credenciales de inicio de sesión, un administrador y otro no administrador.

* Para fines de comprobación, las cuentas que proporcione deben tener suficientes datos rellenados previamente.

* Para las aplicaciones empresariales, las aplicaciones en las que se requiere una suscripción o las aplicaciones en las que hay una dependencia de inquilino o dominio de Office 365, debe proporcionar una tercera cuenta en el mismo dominio que no esté configurada previamente para la aplicación para que podamos validar la experiencia de usuario de primera ejecución.

* Si la aplicación tiene características premium/actualizadas, se debe proporcionar una cuenta con el acceso necesario para probar esa experiencia.

* Puede elegir cargar las notas de prueba en SharePoint. Si es así, proporcione un vínculo público al archivo.

* **Cuentas de prueba**. Se requiere una cuenta de prueba si la aplicación solo permite cuentas con licencia o la lista segura desde el back-end. Además, si hay un ámbito de chat de grupo o grupo permitido en la aplicación, se necesitan dos cuentas de prueba en el mismo inquilino para validar el escenario de colaboración de grupo.

* **Pasos de integración**. Si se requiere una configuración previa por parte de un administrador de inquilinos para usar la aplicación, incluya los pasos y/o proporcione cuentas de administrador y no administrador configuradas para la validación. Nota: puede registrarse para obtener una suscripción al Programa de [desarrolladores de Office 365.](https://developer.microsoft.com/microsoft-365/dev-program) Es gratuito *durante* 90 días y se renovará continuamente siempre que lo use para la actividad de desarrollo.

* **Notas sobre las características de la aplicación en Teams:** detalle todas las funcionalidades que ofrece la aplicación dentro de Teams y los pasos para probar cada característica.

* Vídeo que muestra la funcionalidad de la aplicación **(opcional):** puedes proporcionar una grabación de vídeo del producto para que comprendamos completamente la funcionalidad de la aplicación.

---
title: Resolver problemas con el envío de la tienda
description: Comprenda cómo solucionar y corregir problemas con el envío Microsoft Teams almacén.
ms.topic: how-to
author: heath-hamilton
ms.author: surbhigupta
ms.localizationpriority: none
ms.openlocfilehash: 39ab797bf87638e107f55e8b83d002372a4261f5
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157530"
---
# <a name="resolve-issues-if-your-microsoft-teams-store-submission-fails"></a>Resolver problemas si se produce Microsoft Teams envío del almacén

Las aplicaciones publicadas en la tienda Microsoft Teams deben cumplir las Teams de validación de la tienda [y](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) las directivas del [mercado comercial.](/legal/marketplace/certification-policies)

Si se produce un error en el envío de la tienda, Microsoft proporciona un servicio de validación de concierge para ayudar a que la aplicación cumpla y se publique.

## <a name="get-help-directly-from-microsoft"></a>Obtener ayuda directamente de Microsoft

El servicio de validación de concierge proporcionado por Microsoft ayuda a los desarrolladores a publicar sus aplicaciones en Teams tienda. Como parte de este servicio, Microsoft comprueba si la aplicación funciona como se describe, contiene todos los metadatos adecuados y proporciona valor a los usuarios.

Si se produce un error en el envío de la aplicación, Microsoft te envía un informe de revisión con recomendaciones dentro de las 24 horas siguientes al envío.

## <a name="resolve-issues-and-resubmit-your-app"></a>Resolver problemas y volver a enviar la aplicación

Debes corregir todos los problemas notificados por el equipo de validación de concierge de Microsoft antes de volver a enviar la aplicación en el Centro de partners. El informe de Microsoft incluye la siguiente información:

* Una guía [de validación correspondiente](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) para cada problema.
* Instrucciones sobre cómo reproducir cada problema.
* Recomendaciones para resolver cada problema en función de la documentación del desarrollador disponible públicamente.

El proceso para resolver problemas y volver a enviar una aplicación suele ser el siguiente:

1. Se solucionan todos los problemas del informe.
1. Envíe lo siguiente al equipo de validación de concierge de Microsoft en <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a>:
   * Un paquete de aplicación actualizado
   * Notas de prueba para la aplicación, si no las incluyeste en el envío original:
      * Credenciales para al menos dos cuentas (un administrador y otro no administrador).
      * Instrucciones para configurar la aplicación y probar su funcionalidad.
      * Vídeo que muestra la aplicación usada en Teams.
1. El equipo de validación de concierge de Microsoft prueba completamente la aplicación actualizada.
1. Realice una de las siguientes acciones:
   * Si la aplicación no tiene problemas, vuelve a enviar la aplicación en el Centro de partners.
   * Si los problemas no se resuelven o Microsoft encuentra nuevos problemas, recibirá otro informe sobre qué corregir. Resuelva esos problemas y envíe una versión actualizada de la aplicación a <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a>.

> [!CAUTION]
> Para evitar varios errores de envío, no vuelva a enviar la aplicación en el Centro de partners hasta que el equipo de validación de concierge de Microsoft apruebe la aplicación.

## <a name="faq"></a>Preguntas más frecuentes

Obtén respuestas a algunas preguntas comunes al resolver problemas de envío de aplicaciones.

<br>

<details>

<summary><b>¿Cuánto tiempo se necesita para publicar mi aplicación?</b></summary>

Si el envío de la tienda no tiene ningún problema, la aplicación se publicará en un plazo de 1 a 2 días laborables. Si se produce un error en la aplicación, un equipo de Microsoft te ofrece recomendaciones para solucionar los problemas. Una vez que realices esas correcciones y vuelvas a enviar una aplicación actualizada a ese equipo, se te notificará en 24 horas si la aplicación está lista para publicar o aún necesita más trabajo.

<br>

</details>

<details>

<summary><b>¿Cómo puedo aumentar la probabilidad de que mi aplicación pase el envío?</b></summary>

Hacer lo siguiente puede llevar a un envío correcto:

1. Desarrolla tu aplicación según las Teams [de diseño.](~/concepts/design/design-teams-app-overview.md)
1. Asegúrese de que la aplicación cumple las directrices de validación Teams [de la](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) tienda y las directivas de certificación del mercado comercial [de Microsoft.](/legal/marketplace/certification-policies)
1. Pruebe el paquete de la aplicación con la [Microsoft Teams de validación de aplicaciones.](https://dev.teams.microsoft.com/appvalidation.html)
1. [Prepare el envío de Teams de almacenamiento.](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)

<br>

</details>

<details>

<summary><b>Mi aplicación está en pruebas beta. ¿Puedo enviar mi aplicación de todos modos para ahorrar tiempo en el proceso de publicación?</b></summary>

No. Microsoft solo valida las aplicaciones preparadas para producción.

<br>

</details>

<details>

<summary><b>¿Puedo ponerse en contacto teamsubm@microsoft.com correo electrónico antes de enviar mi aplicación por primera vez en el Centro de partners?</b></summary>

No. Microsoft no empieza a validar la aplicación hasta que envías la aplicación por primera vez en el Centro de partners.

<br>

</details>

<details>

<summary><b>Recibí un correo electrónico del Centro de partners que dice que mi aplicación se aprobó para publicarla. ¿Por qué mi aplicación no está en Teams tienda?</b></summary>

Una vez aprobada la aplicación, la publicación suele demorar entre 1 y 2 días laborables según las capacidades de la aplicación.Si la aplicación no se ha publicado después de dos días laborables, ponte en <a href="mailto:teamsubm@microsoft.com">contacto con teamsubm@microsoft.com</a>.

<br>

</details>

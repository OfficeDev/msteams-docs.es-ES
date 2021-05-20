---
title: Resuelve problemas con el envío de tu tienda
description: Comprende cómo solucionar problemas y corregir problemas con el envío de tu tienda Microsoft Teams.
ms.topic: how-to
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 23c751d7a9fec96de128521f660213a559534283
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565112"
---
# <a name="resolve-issues-if-your-microsoft-teams-store-submission-fails"></a>Resuelve problemas si se produce un error en el envío de la tienda de Microsoft Teams

Las aplicaciones publicadas en la tienda de Microsoft Teams deben cumplir con las [directrices de validación de la tienda Teams](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) y las [directivas del mercado comercial.](/legal/marketplace/certification-policies)

Si se produce un error en el envío de la tienda, Microsoft proporciona un servicio de validación de conserjería para ayudar a que la aplicación sea compatible y publicada.

## <a name="get-help-directly-from-microsoft"></a>Obtén ayuda directamente de Microsoft

El servicio de validación de conserjería proporcionado por Microsoft ayuda a los desarrolladores a publicar sus aplicaciones en la tienda Teams. Como parte de este servicio, Microsoft comprueba si la aplicación funciona como se describe, contiene todos los metadatos adecuados y proporciona valor a los usuarios.

Si se produce un error en el envío de la aplicación, Microsoft le envía un informe de revisión con recomendaciones dentro de las 24 horas posteriores al envío.

## <a name="resolve-issues-and-resubmit-your-app"></a>Resuelve problemas y vuelve a enviar la aplicación

Debe solucionar todos los problemas notificados por el equipo de validación de conserjería de Microsoft antes de volver a enviar la aplicación en el Centro de partners. El informe de Microsoft incluye la siguiente información:

* Una [directriz de validación](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) correspondiente para cada problema.
* Instrucciones sobre cómo reproducir cada problema.
* Recomendaciones para resolver cada problema en función de la documentación del desarrollador disponible públicamente.

El proceso para resolver problemas y volver a enviar una aplicación normalmente va así:

1. Solucione todos los problemas del informe.
1. Envíe lo siguiente al equipo de validación de conserjería de Microsoft en <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com:</a>
   * Un paquete de aplicación actualizado
   * Notas de prueba para la aplicación, si no las incluyeste en tu envío original:
      * Credenciales para al menos dos cuentas (una administradora y otra no administradora).
      * Instrucciones para configurar la aplicación y probar su funcionalidad.
      * Un vídeo que muestra la aplicación utilizada en Teams.
1. El equipo de validación de conserjería de Microsoft prueba completamente la aplicación actualizada.
1. Usted hace una de las siguientes acciones:
   * Si la aplicación está libre de problemas, vuelva a enviar la aplicación en el Centro de partners.
   * Si los problemas no se resuelven o Microsoft encuentra nuevos problemas, recibirá otro informe sobre qué corregir. Resuelva esos problemas y envíe una versión actualizada de la aplicación a <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a>.

> [!CAUTION]
> Para evitar varios errores de envío, no vuelva a enviar la aplicación en el Centro de partners hasta que el equipo de validación de conserjería de Microsoft apruebe la aplicación.

## <a name="faq"></a>Preguntas más frecuentes

Obtenga respuestas a algunas preguntas comunes al resolver problemas de envío de aplicaciones.

<br>

<details>

<summary><b>¿Cuánto tiempo se tarda en publicar mi aplicación?</b></summary>

Si el envío de la tienda no tiene problemas, la aplicación se publicará en un plazo de 1 a 2 días hábiles. Si se produce un error en la aplicación, un equipo de Microsoft le proporciona recomendaciones para solucionar los problemas. Una vez que realices esas correcciones y vuelvas a enviar una aplicación actualizada a ese equipo, se te notificará en 24 horas si la aplicación está lista para publicar o aún necesita más trabajo.

<br>

</details>

<details>

<summary><b>¿Cómo puedo aumentar la probabilidad de que mi aplicación pase el envío?</b></summary>

Hacer lo siguiente puede conducir a un envío exitoso:

1. Desarrolle la aplicación en función de las [directrices de diseño Teams.](~/concepts/design/design-teams-app-overview.md)
1. Asegúrese de que la aplicación se adhiere a las directrices de validación de la tienda Teams y [a las directivas](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) [de certificación del mercado comercial de Microsoft.](/legal/marketplace/certification-policies)
1. Pruebe el paquete de la aplicación con la [herramienta de validación de aplicaciones Microsoft Teams.](https://dev.teams.microsoft.com/appvalidation.html)
1. [Prepare el envío de su tienda Teams.](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)

<br>

</details>

<details>

<summary><b>Mi aplicación está en pruebas beta. ¿Puedo enviar mi aplicación de todos modos para ahorrar tiempo en el proceso de publicación?</b></summary>

No. Microsoft solo valida las aplicaciones preparadas para la producción.

<br>

</details>

<details>

<summary><b>¿Puedo ponerme en contacto con el correo electrónico teamsubm@microsoft.com antes de enviar mi aplicación por primera vez en el Centro de partners?</b></summary>

No. Microsoft no comienza a validar la aplicación hasta que envíes la aplicación por primera vez en el Centro de partners.

<br>

</details>

<details>

<summary><b>Recibí un correo electrónico del Centro de partners diciendo que mi aplicación fue aprobada para publicar. ¿Por qué mi aplicación no está en la tienda Teams?</b></summary>

Una vez aprobada la aplicación, la publicación suele tardar entre 1 y 2 días hábiles en función de las capacidades de la aplicación.Si la aplicación no se ha publicado después de dos días hábiles, ponte en contacto con <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a>.

<br>

</details>

---
title: Resolución de problemas con el envío de la tienda
description: En este artículo, aprenderá a solucionar y corregir problemas con el envío de Microsoft Teams tienda.
ms.topic: how-to
author: heath-hamilton
ms.author: surbhigupta
ms.localizationpriority: medium
ms.openlocfilehash: 51427f2023ba566391a3d0b544d74e5658464a7c
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123212"
---
# <a name="resolve-issues-if-your-microsoft-teams-store-submission-fails"></a>Resolver problemas si se produce un error en el envío de la tienda de Microsoft Teams

Las aplicaciones publicadas en el almacén de Microsoft Teams deben cumplir las [directrices de validación de Teams tienda](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) y [las directivas de Marketplace comercial](/legal/marketplace/certification-policies).

Si se produce un error en el envío de la tienda, Microsoft proporciona un servicio de validación de concierge para ayudar a que la aplicación sea compatible y se publique.

## <a name="get-help-directly-from-microsoft"></a>Obtener ayuda directamente de Microsoft

El servicio de validación de concierge proporcionado por Microsoft ayuda a los desarrolladores a publicar sus aplicaciones en la tienda Teams. Como parte de este servicio, Microsoft comprueba si la aplicación funciona como se describe, contiene todos los metadatos adecuados y proporciona valor a los usuarios.

Si se produce un error en el envío de la aplicación, Microsoft le envía un informe de revisión con recomendaciones dentro de las 24 horas posteriores al envío.

## <a name="resolve-issues-and-resubmit-your-app"></a>Resolución de problemas y reenvíe la aplicación

Debe corregir todos los problemas notificados por el equipo de validación de Concierge de Microsoft antes de volver a enviar la aplicación en el Centro de partners. El informe de Microsoft incluye la siguiente información:

* Una [guía de validación](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) correspondiente para cada problema.
* Instrucciones sobre cómo reproducir cada problema.
* Recomendaciones para resolver cada problema en función de la documentación para desarrolladores disponible públicamente.

El proceso para resolver problemas y volver a enviar una aplicación suele ser el siguiente:

1. Se corrigen todos los problemas del informe.
1. Envíe lo siguiente al equipo de validación de Concierge de Microsoft en <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a>:
   * Un paquete de aplicación actualizado
   * Notas de prueba de la aplicación, si no las incluyeste en el envío original:
      * Credenciales para al menos dos cuentas (un administrador y otro no administrador).
      * Instrucciones para configurar la aplicación y probar su funcionalidad.
      * Vídeo en el que se muestra la aplicación usada en Teams.
1. El equipo de validación de Concierge de Microsoft prueba completamente la aplicación actualizada.
1. Realice una de las siguientes acciones:
   * Si la aplicación no tiene problemas, vuelva a enviarla al Centro de partners.
   * Si los problemas no se resuelven o Microsoft encuentra nuevos problemas, recibirá otro informe sobre qué corregir. Resuelva esos problemas y envíe una versión actualizada de la aplicación a <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a>.

> [!CAUTION]
> Para evitar varios errores de envío, no vuelva a enviar la aplicación en el Centro de partners hasta que el equipo de validación de Concierge de Microsoft apruebe la aplicación.

## <a name="faq"></a>Preguntas más frecuentes

Obtenga respuestas a algunas preguntas comunes al resolver problemas de envío de aplicaciones.

<br>

<details>

<summary><b>¿Cuánto tiempo se tarda en publicar mi aplicación?</b></summary>

Si el envío de la tienda no tiene problemas, la aplicación se publicará en un plazo de 1 a 2 días laborables. Si se produce un error en la aplicación, un equipo de Microsoft le proporciona recomendaciones para solucionar los problemas. Una vez que realices esas correcciones y vuelvas a enviar una aplicación actualizada a ese equipo, se te notificará en 24 horas si la aplicación está lista para publicarse o todavía necesita más trabajo.

<br>

</details>

<details>

<summary><b>Cómo aumentar la probabilidad de que mi aplicación pase el envío?</b></summary>

Hacer lo siguiente puede dar lugar a un envío correcto:

1. Desarrolle la aplicación en función de las [directrices de diseño de Teams](~/concepts/design/design-teams-app-overview.md).
1. Asegúrese de que la aplicación cumple las [directrices de validación de Teams tienda y las directivas](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) de [certificación de Marketplace comercial de Microsoft](/legal/marketplace/certification-policies).
1. Pruebe el paquete de la aplicación con la [herramienta de validación de aplicaciones Microsoft Teams](https://dev.teams.microsoft.com/appvalidation.html).
1. [Prepare el envío Teams tienda](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md).

<br>

</details>

<details>

<summary><b>Mi aplicación está en pruebas beta. ¿Puedo enviar mi aplicación de todos modos para ahorrar tiempo en el proceso de publicación?</b></summary>

No. Microsoft solo valida las aplicaciones listas para producción.

<br>

</details>

<details>

<summary><b>¿Puedo ponerse en contacto con el teamsubm@microsoft.com correo electrónico antes de enviar la aplicación por primera vez en el Centro de partners?</b></summary>

No. Microsoft no comienza a validar la aplicación hasta que la envíe por primera vez en el Centro de partners.

<br>

</details>

<details>

<summary><b>He recibido un correo electrónico del Centro de partners que indica que mi aplicación ha sido aprobada para publicarse. ¿Por qué mi aplicación no está en la tienda Teams?</b></summary>

Una vez aprobada la aplicación, la publicación suele tardar entre 1 y 2 días laborables en función de las funcionalidades de la aplicación.Si la aplicación no se ha publicado después de dos días laborables, póngase en contacto con <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a>.

<br>

</details>

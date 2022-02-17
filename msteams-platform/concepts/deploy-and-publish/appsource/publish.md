---
title: 'Información general: Teams de publicación de la tienda de aplicaciones'
description: Describe el proceso para enviar la aplicación al Centro de partners y publicarla en la tienda Microsoft Teams (y AppSource).
ms.topic: overview
author: heath-hamilton
ms.author: surbhigupta
ms.localizationpriority: none
ms.openlocfilehash: eaebde76a3d1f387ba16c9fdc77670144d22fa61
ms.sourcegitcommit: 40aade608ee21f5d7d813bd145bef5736dc647f1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/17/2022
ms.locfileid: "62881654"
---
# <a name="publish-your-app-to-the-microsoft-teams-store"></a>Publicar la aplicación en la tienda Microsoft Teams cliente

Puedes distribuir la aplicación directamente a la tienda dentro de Microsoft Teams y llegar a millones de usuarios de todo el mundo. Si la aplicación también se incluye en la tienda, puedes llegar al instante a los clientes potenciales.

Las aplicaciones publicadas en la Teams también se incluyen automáticamente en [Microsoft AppSource](https://appsource.microsoft.com), que es el mercado oficial para Microsoft 365 aplicaciones y soluciones.

## <a name="understand-the-publishing-process"></a>Comprender el proceso de publicación

Cuando sientas que la aplicación está lista para la producción, puedes comenzar el proceso de obtenerla en la Teams tienda.

> [!TIP]
> Seguir los pasos previos al envío puede aumentar la posibilidad de que Microsoft apruebe la aplicación para su publicación.

:::row:::
   :::column span="":::
      
   :::column-end:::
   :::column span="3":::
      :::image type="content" source="../../../assets/images/submission/teams-app-store-publish-process.png" alt-text="Teams de publicación de la tienda de aplicaciones" lightbox="../../../assets/images/submission/teams-app-store-publish-process.png":::
   :::column-end:::
   :::column span="":::
      
   :::column-end:::
:::row-end:::

1. [Revisa las Teams de validación de](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) la tienda para asegurarte de que la aplicación cumple Teams estándares de la aplicación y la tienda.

1. [Crear una cuenta de desarrollador del Centro de partners](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md).

1. [Prepare el envío de](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md) la tienda, que incluye la ejecución de pruebas automatizadas, la compilación de notas de pruebas, la creación de una descripción de la tienda, entre otras tareas importantes para ayudar a acelerar el proceso de revisión.

1. [Envía tu aplicación a través](/office/dev/store/add-in-submission-guide) del Centro de partners.

1. Si se produce un error en el envío, trabaje con Microsoft directamente para [resolver los problemas y volver a enviar la aplicación](~/concepts/deploy-and-publish/appsource/resolve-submission-issues.md).

## <a name="what-to-expect-after-you-submit-your-app"></a>¿Qué esperar después de enviar la aplicación?

* **Pruebas funcionales y de experiencia profundas**

  Un validador revisa exhaustivamente la aplicación para garantizar el cumplimiento de las directivas de certificación de [Microsoft Commercial Marketplace](/legal/marketplace/certification-policies) con un enfoque en pruebas de experiencia funcional y de usuario profundas, comprobaciones de facilidad de uso y comprobaciones de metadatos. La validación de aplicaciones se realiza en clientes de escritorio, web y móviles.

* **Publicación de aplicaciones guiada a través del servicio de concierge**

  Si no se observa ningún problema con la aplicación, la aplicación se aprobará y se publicará en la Teams tienda. Si hay problemas, recibirá un informe de validación automatizada del Centro de partners con los detalles del error. Para ayudarte a publicar correctamente la aplicación en la tienda de Teams y guiarte a través de este proceso, el equipo de validación te enviará un correo electrónico personalizado desde nuestro servicio de [concierge teamsubm@microsoft.com](mailto:teamsubm@microsoft.com) que incluya la siguiente información:

   * Resumen de todos los problemas

   * Detalles de errores o problemas con vínculos de directiva y categorización: 

     * Corrección obligatoria: estos problemas deben solucionarse antes de la aprobación de la aplicación.

     * Corrección sugerida: estos problemas pueden ser fijos después de la aprobación de la aplicación, ya que son recomendaciones para mejorar la experiencia de la aplicación.

     * Bloqueador: estos problemas impiden al equipo de validación probar aún más la funcionalidad de la aplicación y deben resolverse para que la validación continúe.

     * Consulta: estas consultas se pueden compartir para obtener respuestas a preguntas específicas relacionadas con la aplicación.

   * Pasos para volver a crear problemas a través de instrucciones escritas o formato de vídeo.

   * Recomendaciones solucionar los problemas notificados con vínculos a documentos de orientación.
 
  Después de revisar la lista de problemas, corrija todos los problemas notificados y comparta el paquete de la aplicación actualizado por correo electrónico, para que el equipo de validación vuelva a validar la aplicación a fondo. Si tiene consultas relacionadas con los problemas notificados, póngase en contacto con el equipo de validación en [teamsubm@microsoft.com](mailto:teamsubm@microsoft.com).

  Si hay problemas restantes o de regresión observados en la aplicación, el equipo de validación compartirá contigo un informe de validación actualizado. Si la aplicación tenía bloqueadores, es posible que veas nuevos problemas notificados cuando la aplicación se valide después de que se resuelvan los bloqueadores. A veces, el equipo de validación también ha observado problemas de regresión en las aplicaciones después de la implementación de correcciones. Se necesitan unos pocos envíos de nuevo para cerrar todos los problemas de una aplicación que consta de errores y obtener su aprobación para publicar en la Teams almacén.

  Una vez cerrados todos los problemas notificados y se realiza el envío final en el Centro de partners, el equipo de validación aprobará y publicará la aplicación. Permitir al menos un día laborable para que la aplicación esté disponible en la Teams tienda.

## <a name="tips-for-rapid-approval-to-publish-your-app"></a>Sugerencias para la aprobación rápida para publicar la aplicación

* **Durante la fase de diseño**

  Revisa las [directrices de validación](prepare/teams-store-validation-guidelines.md) de la tienda al principio del ciclo de vida de la aplicación (fase de diseño) para asegurarte de que creas la aplicación de acuerdo con los requisitos de la tienda. Si creas la aplicación de acuerdo con estas directrices, esto impedirá que se vuelvan a trabajar debido a la no adherencia a las directivas de almacenamiento.

* **Antes del envío de la aplicación**

  1. [Crea tu cuenta del Centro de partners](prepare/create-partner-center-dev-account.md) con antelación. Si se encuentra con algún desafío con su cuenta [del Centro de partners](prepare/create-partner-center-dev-account.md), cree un [vale de soporte técnico](/azure/marketplace/partner-center-portal/support).

  1. Revisa de [nuevo las directrices de validación](prepare/teams-store-validation-guidelines.md) de la tienda para asegurarte de que la aplicación está en línea con los requisitos de la tienda. Esto ayuda a reducir el número de problemas observados en la aplicación y, en consecuencia, el tiempo que se necesita para aprobar la aplicación.

  1. Prueba y vuelve a probar la aplicación:

     1. Valide el paquete de la aplicación mediante Teams [Developer Portal](https://dev.teams.microsoft.com/home) para identificar y corregir los errores del paquete.

        :::image type="content" source="../../../assets/images/submission/teams-validation-developer-portal.png" alt-text="validación del almacén":::
 
     1. Prueba tu aplicación a fondo antes del envío de la aplicación para asegurarte de que se adhiere a las directivas de la tienda. Carga local de la aplicación en Teams prueba los flujos de usuario de un extremo a otro para la aplicación. Asegúrese de que la funcionalidad funciona según lo esperado, los vínculos no se rompen, la experiencia del usuario no está bloqueada y las limitaciones están claramente resaltadas.

     1. Pruebe la aplicación en clientes de escritorio, web y móviles. Asegúrate de que la aplicación responde en diferentes factores de forma.

  1. Completa [la verificación del editor](/azure/active-directory/develop/publisher-verification-overview) antes de enviar la aplicación. Si se encuentra con algún problema, puede crear un [vale de soporte técnico](/azure/marketplace/partner-center-portal/support) para la resolución.

  1. Mientras te preparas para el envío de la aplicación, [sigue la lista de comprobación](/microsoftteams/platform/concepts/deploy-and-publish/appsource/prepare/submission-checklist) e incluye los siguientes detalles como parte del paquete de envío:

      1. Paquete de aplicación completamente comprobado.

      1. Credenciales de administrador de trabajo y de usuario no administrador para probar la funcionalidad de la aplicación (si la aplicación ofrece un modelo de suscripción premium).

      1. Instrucciones de prueba que detallan la funcionalidad de la aplicación y los escenarios admitidos.

      1. Instrucciones de configuración si la aplicación requiere una configuración adicional para acceder a la funcionalidad de la aplicación. Como alternativa, si la aplicación requiere una configuración compleja, también puedes proporcionar a un inquilino de [demostración](/office/developer-program/microsoft-365-developer-program-get-started) aprovisionado acceso de administrador para que nuestros validadores puedan omitir los pasos de configuración.

      1. Vínculo a un flujo de usuario clave de grabación de vídeo de demostración para la aplicación. Esto es muy recomendable.

* **Publicar envío de la aplicación**

  * Después de revisar el informe de validación, responda al hilo de correo electrónico con cualquier consulta relacionada con el informe de validación o si necesita soporte adicional para resolver los problemas notificados.

  * Asegúrate de que tienes un ancho de banda de desarrollador adecuado para resolver los problemas notificados hasta que se apruebe la aplicación.

  * Asegúrate de que has [resuelto todos los](/microsoftteams/platform/concepts/deploy-and-publish/appsource/resolve-submission-issues) problemas notificados por el servicio [de teamsubm@microsoft.com](mailto:teamsubm@microsoft.com) antes de compartir el paquete de la aplicación para realizar pruebas adicionales. Esto ayuda a reducir el número de iteraciones necesarias para validar la aplicación y, en consecuencia, el tiempo necesario para aprobar la aplicación.
  
  * Evite cambiar la funcionalidad de la aplicación durante el proceso de validación. Esto puede provocar la detección de nuevos problemas y aumentar el tiempo que se tarda en aprobar la aplicación.

## <a name="see-also"></a>Vea también

* [Publicación en Microsoft 365 app stores](/office/dev/store/)
* [Upload aplicación Teams aplicación](~/concepts/deploy-and-publish/apps-upload.md)
* [Publicar la aplicación Teams en la organización](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
* [Planear la experiencia de incorporación para los usuarios](../../design/understand-use-cases.md#plan-the-onboarding-experience)
* [Distribución de aplicaciones de pestañas en dispositivos móviles](../../../tabs/design/tabs-mobile.md#distribution)
* [Versión preliminar de prueba para aplicaciones monetizadas](prepare/Test-preview-for-monetized-apps.md)

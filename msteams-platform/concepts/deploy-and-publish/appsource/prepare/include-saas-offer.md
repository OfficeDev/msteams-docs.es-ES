---
title: Incluir una oferta de SaaS con la aplicación
description: Aprende a monetizar tu aplicación Microsoft Teams con planes de suscripción.
author: heath-hamilton
ms.author: surbhigupta
ms.topic: how-to
localization_priority: Normal
ms.openlocfilehash: 72dbbfe62e6f5f975a09b7c0538e0847520670d9
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2021
ms.locfileid: "60719801"
---
# <a name="include-a-saas-offer-with-your-microsoft-teams-app"></a>Incluir una oferta SaaS con tu Microsoft Teams aplicación

:::row:::
   :::column span="3":::

Con una oferta de Software como servicio (SaaS) transaccionable, puedes monetizar tu aplicación de Teams mediante la venta de planes de suscripción directamente desde la descripción de la tienda Teams cliente. Por ejemplo, diga que tiene una aplicación gratuita que cualquier persona puede obtener en la tienda. Ahora puedes ofrecer planes premium y de empresa para los usuarios que quieran más características.

Esta es una idea general de cómo monetizar la aplicación:

1.  [Plan your SaaS offer](#plan-your-saas-offer).

1.  [Integre con las API de cumplimiento saas.](#integrate-with-the-saas-fulfillment-apis)

1.  [Cree una página de aterrizaje para la administración de suscripciones.](#build-a-landing-page-for-subscription-management)

1.  [Cree su oferta SaaS](#create-your-saas-offer).

1.  [Configurar la aplicación para la oferta SaaS](#configure-your-app-for-the-saas-offer).

1.  [Publicar la aplicación en la tienda Teams .](#publish-your-app)

   :::column-end:::
   :::column span="1":::
   
:::image type="content" source="~/assets/images/saas-offer/saas-offer-diagram.png" alt-text="Diagrama que muestra el proceso para incluir una oferta SaaS con la Teams aplicación." border="false":::

   :::column-end:::
:::row-end:::

## <a name="plan-your-saas-offer"></a>Plan your SaaS offer

Para obtener instrucciones completas, [vea cómo planear una oferta SaaS para el mercado comercial de Microsoft.](/azure/marketplace/plan-saas-offer)

Al planear cómo monetizar la aplicación Teams, estos son algunos aspectos a tener en cuenta:

* Decida el modelo de suscripción. Una oferta SaaS transaccionable puede incluir varios planes de suscripción. Los planes de suscripción públicos disponibles para cualquier persona son más comunes, pero es posible que también quieras dirigirte a clientes específicos con ofertas solo para ellos. Para obtener más información, [vea ofertas privadas en el mercado comercial de Microsoft.](/azure/marketplace/private-offers)
* Lee la opción Vender a través de [ *Microsoft*](/azure/marketplace/plan-saas-offer#listing-options) para la oferta SaaS, que es necesaria si quieres que los usuarios compren planes de suscripción para tu aplicación directamente a través de la Teams tienda.
* Obtenga información [sobre Azure Active Directory (Azure AD) de](/azure/marketplace/azure-ad-saas) inicio de sesión único (SSO) ayuda a sus clientes a comprar y administrar suscripciones. (Azure AD SSO es necesario para Teams aplicaciones con ofertas SaaS).
* Comprenda que es responsable de administrar y pagar la infraestructura necesaria para admitir el uso de sus clientes de su oferta saas.
* Planee el móvil. Para evitar infringir las directivas de la tienda de aplicaciones de terceros, la aplicación no puede incluir vínculos que permitan a los usuarios comprar planes de suscripción en el móvil. Sin embargo, aún puedes indicar si la aplicación tiene características que requieren un plan de suscripción. Para obtener más información, vea las directivas relacionadas [de certificación del mercado comercial.](/legal/marketplace/certification-policies#114048-mobile-experience)

## <a name="integrate-with-the-saas-fulfillment-apis"></a>Integración con las API de cumplimiento saas

La integración con las API de cumplimiento saas es necesaria para monetizar tu Teams aplicación. Estas API le ayudan a administrar el ciclo de vida de un plan de suscripción una vez que un usuario las compra.

Para obtener instrucciones completas y referencia a la API, consulte la documentación de las API de [cumplimiento saas.](/azure/marketplace/partner-center-portal/pc-saas-fulfillment-api-v2) En general, implementará los siguientes pasos mediante las API una vez que se compre una suscripción:

1.  Recibe un [*token de identificación de compra*](/azure/marketplace/partner-center-portal/pc-saas-fulfillment-api-v2#purchased-but-not-yet-activated-pendingfulfillmentstart) a través de la dirección URL de la página de aterrizaje.

1.  Use el token para recuperar los detalles de la suscripción.

1.  Notificar al mercado comercial que la suscripción está activada.

### <a name="best-practices-for-implementing-subscription-management"></a>Procedimientos recomendados para implementar la administración de suscripciones

* Con ofertas SaaS transaccionables para Teams aplicaciones, los planes de suscripción (licencias) deben asignarse a usuarios individuales en lugar de grupos o a toda una organización.
* Cuando se asigne a los usuarios un plan de suscripción, notifique a los usuarios a través Teams bot o correo electrónico. En la mensajería, incluye información sobre cómo agregar la aplicación a Teams y empezar.
* Admite la idea de varios administradores. En otras palabras, varios usuarios de la misma organización pueden comprar y administrar sus propias suscripciones.

## <a name="build-a-landing-page-for-subscription-management"></a>Crear una página de aterrizaje para la administración de suscripciones 

Cuando alguien termine de comprar un plan de suscripción para la aplicación en la tienda de Teams, el mercado comercial lo dirigirá a la página de aterrizaje donde puede administrar la suscripción (por ejemplo, asignar una licencia a un usuario específico de su organización).

Para obtener instrucciones completas, [consulte build the landing page for your SaaS offer](/azure/marketplace/azure-ad-transactable-saas-landing-page).

### <a name="best-practices-for-landing-pages"></a>Procedimientos recomendados para páginas de aterrizaje

Ten en cuenta los siguientes enfoques al crear una página de aterrizaje para la Teams que estás monetizando. Vea una página de aterrizaje de ejemplo en la [experiencia de compra del usuario final.](#end-user-purchasing-experience)

* Los usuarios deben poder iniciar sesión en la página de aterrizaje con las mismas Azure AD credenciales que usaron para comprar la suscripción. Para obtener más información, [vea Azure AD y ofertas saas transaccionables en el mercado comercial.](/azure/marketplace/azure-ad-saas)
* Permitir a los usuarios realizar las siguientes acciones en la página de aterrizaje. No olvide tener en cuenta lo que es apropiado para el rol y los permisos de un usuario (por ejemplo, puede que desee permitir que solo los administradores de suscripciones busquen usuarios):
  * Busque usuarios en su organización mediante correo electrónico u otra forma de identidad.
  * Consulta los usuarios a los que pueden asignar licencias en una lista.
  * Asignar licencias a uno o varios usuarios al mismo tiempo.
  * Asignar y administrar diferentes tipos de licencias (si están disponibles).
  * Valide si una licencia ya está asignada a otro usuario.
  * Cancelar su suscripción.
* Proporciona una introducción sobre cómo usar la aplicación.
* Agregue formas de obtener soporte técnico, como preguntas frecuentes, knowledge base o correo electrónico de contacto.
* Proporciona un vínculo que facilita al suscriptor volver a la página de aterrizaje. Por ejemplo, incluye este vínculo en la pestaña Acerca **de la** aplicación.

## <a name="create-your-saas-offer"></a>Crear su oferta SaaS

Una vez que haya integrado las API de saas fulfillment y haya creado la página de aterrizaje donde los usuarios puedan administrar sus suscripciones, es el momento de crear, probar y publicar oficialmente la oferta SaaS transaccionable.

### <a name="create-the-offer"></a>Crear la oferta

Consulta [Crear una oferta SaaS para](/azure/marketplace/create-new-saas-offer) obtener instrucciones completas sobre cómo hacerlo en el Centro de partners. Los pasos siguientes describen qué hacer en un nivel alto.

1.  Cree una [cuenta del Centro de](https://partner.microsoft.com/) partners si no tiene una.

1.  Configure los planes de suscripción, los detalles de precios y mucho más para su oferta SaaS transaccionable. En particular, asegúrese de completar los pasos siguientes:

    * En **Detalles del programa de** instalación, seleccione la opción Sí para especificar que va a vender la oferta a través de Microsoft. 
     
    * En **Microsoft 365 integración,** agrega el vínculo AppSource a la descripción de la aplicación. Este paso garantiza que las personas puedan comprar sus planes de suscripción en AppSource además de Teams.

1. Almacena tu editor y ofrece id. (Los necesitas más adelante para vincular la oferta a tu aplicación en el Portal de desarrolladores).

1. Publique su oferta en el mercado comercial.

### <a name="test-the-offer"></a>Probar la oferta

Le recomendamos encarecidamente que compruebe la experiencia de compra de un extremo a otro antes de publicar su oferta saas. Para ello, cree una oferta independiente solo para pruebas. Para obtener información completa, vea Introducción a [la oferta de](/azure/marketplace/plan-saas-offer#test-offer)prueba, crear una oferta de [prueba](/azure/marketplace/create-saas-dev-test-offer)y obtener una vista previa de [la oferta](/azure/marketplace/test-publish-saas-offer).

> [!IMPORTANT]
> Debe probar la oferta SaaS transaccionable en AppSource. Actualmente, no puedes probar una transacción de un extremo a otro en Teams hasta que la aplicación complete la validación de la tienda.

Desde un punto Teams, estas pruebas deben comprobar que el número de licencias y asignaciones coincide con lo que hay en el centro de administración de Teams cuando los usuarios:

* Active y configure su plan de suscripción en la página de aterrizaje.
* Asignar, quitar o reasignar licencias a sí mismos u otras personas.
* Cancelar o renovar su suscripción.

### <a name="publish-the-offer"></a>Publicar la oferta

Una vez que haya terminado de probar, [publique la oferta en directo.](/azure/marketplace/test-publish-saas-offer#publish-your-offer-live)

## <a name="configure-your-app-for-the-saas-offer"></a>Configurar la aplicación para la oferta SaaS

Has publicado la oferta de SaaS, pero aún debes vincularla a tu aplicación de Teams para que los usuarios puedan ver los planes de suscripción en la Teams tienda.

1. Vaya al [Portal de desarrolladores](https://dev.teams.microsoft.com/) y seleccione **Aplicaciones**.
1. En la **página Aplicaciones,** selecciona la aplicación a la que vinculas la oferta SaaS.
1. Vaya a la **página Planes y precios** y especifique su editor y ofrezca id. (Puede encontrar estos IDs en el Centro de partners si no los tiene disponibles fácilmente).
1. Selecciona **Ver** para obtener una vista previa de los planes de suscripción de la oferta SaaS.
1. Si todo se ve bien, seleccione **Guardar**.

   La `subscriptionOffer` propiedad se agrega al manifiesto de la [aplicación](~/resources/schema/manifest-schema-dev-preview.md#subscriptionoffer).

   ```json
      "subscriptionOffer": {
        "offerId": "publisherId.offerId"  
        }
   ```

## <a name="publish-your-app"></a>Publicar la aplicación

Has creado la oferta SaaS y la has vinculado a tu aplicación Teams, ahora es el momento de publicar la aplicación en la Teams tienda. Para obtener instrucciones completas, [consulta Publicar la aplicación en la tienda Teams.](~/concepts/deploy-and-publish/appsource/publish.md)

> [!IMPORTANT]
> Incluso si la aplicación ya aparece en la tienda Teams, debes volver a pasar por el proceso de validación de la tienda para incluir tu oferta SaaS.

Una vez publicado, los usuarios verán una opción Comprar una suscripción en el cuadro de diálogo detalles de la aplicación cuando intenten agregar la aplicación **a** Teams.

## <a name="end-user-purchasing-experience"></a>Experiencia de compra del usuario final

En el ejemplo siguiente se muestra cómo los usuarios pueden comprar planes de suscripción para una aplicación ficticia Teams llamada *Recloud*.

1. En la Teams, busca y selecciona la *aplicación Recloud.*

1. En el cuadro de diálogo detalles de la aplicación, **selecciona Comprar una suscripción.**

    :::image type="content" source="~/assets/images/saas-offer/buysubscriptionplan.png" alt-text="Comprar la suscripción para la aplicación seleccionada.":::

1. Seleccione su país para ver los planes de suscripción para su ubicación.

1. En el **cuadro de diálogo** Elegir un plan de suscripción, elija el plan que desee y seleccione **Checkout**. (Nota: Los planes privados solo son visibles para los usuarios de las organizaciones a las que proporcionas la oferta. Estos planes se indican con un **icono de oferta** :::image type="icon" source="~/assets/icons/special-icon.png"::: especial).

    :::image type="content" source="~/assets/images/saas-offer/choosingsubscriptionplan.png" alt-text="Seleccionar el plan de suscripción adecuado.":::

1. En el **cuadro de diálogo** Desprotección, proporcione la información necesaria y seleccione Realizar **pedido.**

    :::image type="content" source="~/assets/images/saas-offer/placesubscriptionorder.png" alt-text="Realizar el pedido de suscripción.":::

1. Cuando se le pida, seleccione **Configurar ahora** para configurar la suscripción.

    :::image type="content" source="~/assets/images/saas-offer/saas-offer-set-up.png" alt-text="Configurar la suscripción.":::

1. Administrar el plan de suscripción a través del sitio web *de Recloud* (también conocido como página [de aterrizaje).](#build-a-landing-page-for-subscription-management)

    :::image type="content" source="~/assets/images/saas-offer/subscriptionlicenses.png" alt-text="Configuración de licencias de usuario.":::

## <a name="admin-purchasing-experience"></a>Experiencia de compra de administrador

Los administradores pueden comprar planes de suscripción de aplicaciones [en Teams centro de administración.](/MicrosoftTeams/purchase-third-party-apps)

## <a name="remove-a-saas-offer-from-your-app"></a>Quitar una oferta SaaS de la aplicación

Si desvinculas una oferta SaaS incluida en la descripción Teams tienda, debes volver a publicar la aplicación para ver el cambio en la tienda.

1. Vaya al [Portal de desarrolladores](https://dev.teams.microsoft.com/) y seleccione **Aplicaciones**.
1. En la **página Aplicaciones,** selecciona la aplicación de la que estás quitando la oferta.
1. Vaya a la **página Planes y precios** y seleccione **Revertir**.
1. Una vez desvinculada la oferta, haga lo siguiente para actualizar la descripción de la tienda:
   1. Seleccione **Distribuir > publicar en el almacén Teams .**
   1. Selecciona **Abrir centro de partners** para iniciar el proceso de volver a publicar la aplicación sin la oferta.

## <a name="see-also"></a>Consulte también

* [Mantenimiento y soporte técnico de la aplicación publicada](../post-publish/overview.md)

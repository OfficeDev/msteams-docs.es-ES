---
title: Incluir una oferta de SaaS con la aplicación
description: En este artículo, aprenderá a monetizar su aplicación de Microsoft Teams con el modelo de precios basado en suscripciones e incluir una oferta de SaaS en dicha aplicación.
author: heath-hamilton
ms.author: surbhigupta
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: e9182df9f6c3c5d7f84654022e658ac6d670e50d
ms.sourcegitcommit: 209b9942c02b5affdd995348902114d3b9805c61
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2022
ms.locfileid: "67288188"
---
# <a name="include-a-saas-offer-with-your-teams-app"></a>Incluir una oferta de SaaS con la aplicación de Teams

:::row:::
   :::column span="3":::

Una oferta de software como servicio (SaaS) comercializable le permite monetizar su aplicación de Teams mediante la venta de planes de suscripción directamente desde la descripción de su tienda de Teams. Por ejemplo, supongamos que tiene una aplicación gratuita que cualquiera puede obtener en la tienda. Ahora puede ofrecer planes premium y de empresa para los usuarios que quieran más características.

Esta es una visión general de cómo monetizar la aplicación:

1. [Preparar su oferta de SaaS](#plan-your-saas-offer).

1. [Integrar con las API de suministro SaaS](#integrate-with-the-saas-fulfillment-apis).

1. [Crear una página de aterrizaje para la administración de suscripciones](#build-a-landing-page-for-subscription-management).

1. [Crear la oferta de SaaS](#create-your-saas-offer).

1. [Configurar la aplicación para la oferta de SaaS](#configure-your-app-for-the-saas-offer).

1. [Publicar la aplicación en la tienda de Teams](#publish-your-app).

   :::column-end:::
   :::column span="1":::

:::image type="content" source="~/assets/images/saas-offer/saas-offer-diagram.png" alt-text="Diagrama que muestra el proceso para incluir una oferta SaaS con su aplicación de Teams.":::

   :::column-end:::
:::row-end:::

## <a name="plan-your-saas-offer"></a>Preparar su oferta de SaaS

Para obtener instrucciones completas, consulte [Cómo preparar una oferta SaaS para el mercado comercial de Microsoft](/azure/marketplace/plan-saas-offer).

Al preparar la monetización de su aplicación de Teams, estas son algunas cosas a tener en cuenta:

* Decida el modelo de suscripción. Una oferta de SaaS comercializable puede incluir varios planes de suscripción. Los planes de suscripción pública disponibles para todo el mundo son los más comunes, pero puede que también quiera dirigirse a clientes específicos con ofertas solo para ellos. Para obtener más información, consulte los [planes privados en el marketplace comercial de Microsoft](/azure/marketplace/private-plans).
* Infórmese sobre la opción [*Vender a través de Microsoft*](/azure/marketplace/plan-saas-offer#listing-options) para la oferta SaaS. Esto es necesario si quiere que los usuarios compren planes de suscripción para su aplicación directamente a través de la tienda de Teams.
* Descubra cómo el [inicio de sesión único (SSO) de Azure Active Directory](/azure/marketplace/azure-ad-saas) ayuda a sus clientes a comprar y administrar suscripciones. El SSO de Microsoft Azure Active Directory (Azure AD) es obligatorio para las aplicaciones de Teams con ofertas SaaS.
* Tenga en cuenta que es responsable de administrar y pagar la infraestructura necesaria para respaldar el uso que los clientes hagan de su oferta de SaaS.
* Tenga en cuenta la situación con los dispositivos móviles. Para evitar infringir las directivas de la tienda de aplicaciones de terceros, su aplicación no podrá incluir vínculos que permitan a los usuarios comprar planes de suscripción en el móvil. Lo que sí puede hacer es indicar si la aplicación tiene características que requieran un plan de suscripción. Para más información, consulte las [directivas de certificación del mercado comercial relacionadas](/legal/marketplace/certification-policies#114048-mobile-experience).

## <a name="integrate-with-the-saas-fulfillment-apis"></a>Integrar con las API de suministro SaaS

La integración con las API de suministro de SaaS es necesaria para monetizar la aplicación de Teams. Estas API le ayudan a administrar el ciclo de vida de un plan de suscripción, una vez que lo compra un usuario.

Para obtener instrucciones completas y referencias de API, consulte la documentación de las [API de suministro de SaaS](/azure/marketplace/partner-center-portal/pc-saas-fulfillment-apis). En general, una vez comprada una suscripción se implementan los pasos siguientes mediante las API:

1. Recibir un [*token de identificación de compra*](/azure/marketplace/partner-center-portal/pc-saas-fulfillment-life-cycle#purchased-but-not-yet-activated-pendingfulfillmentstart) a través de la dirección URL de la página de aterrizaje.

1. Usar el token para recuperar los detalles de la suscripción.

1. Informar al marketplace de que la suscripción está activada.

### <a name="best-practices-for-implementing-subscription-management"></a>Procedimientos recomendados para implementar la administración de suscripciones

* Con las ofertas SaaS comercializables para Teams aplicaciones, los planes de suscripción (licencias) deben asignarse a usuarios individuales en lugar de a grupos o a toda una organización.
* Cuando se asigne un plan de suscripción a los usuarios, infórmeles de ello a través de un bot o correo electrónico de Teams. En su comunicación, incluya información sobre cómo agregar la aplicación a Teams y empezar.
* Admitir la idea de varios administradores. En otras palabras, varios usuarios de la misma organización pueden comprar y administrar sus propias suscripciones.

## <a name="build-a-landing-page-for-subscription-management"></a>Crear una página de aterrizaje para la administración de suscripciones

Cuando alguien termine de comprar un plan de suscripción para su aplicación en la tienda de Teams, el marketplace le dirigirá a la página de aterrizaje donde podrá administrar la suscripción (por ejemplo, asignar una licencia a un usuario específico de su organización).

Para obtener instrucciones completas, consulte [Crear la página de aterrizaje de la oferta de SaaS](/azure/marketplace/azure-ad-transactable-saas-landing-page).

### <a name="best-practices-for-landing-pages"></a>Procedimientos recomendados para páginas de aterrizaje

Tenga en cuenta las siguientes estrategias al crear una página de aterrizaje para la aplicación de Teams que monetiza. Vea una página de aterrizaje de ejemplo en la [experiencia de compra del usuario final](#end-user-purchasing-experience).

* Los usuarios deben poder iniciar sesión en la página de inicio con las mismas credenciales de Azure AD que usaron para comprar la suscripción. Para obtener más información, consulte [Azure AD y las ofertas de SaaS comercializables en el marketplace comercial](/azure/marketplace/azure-ad-saas).
* Permita que los usuarios realicen las acciones abajo listadas en la página de aterrizaje. Tenga siempre en cuenta qué es apropiado para el rol y los permisos de un usuario. Por ejemplo, quizá desee permitir que solo los administradores de suscripciones busquen usuarios):
  * Buscar usuarios de su organización por correo electrónico o mediante otro tipo de identidad.
  * Ver los usuarios a los que pueden asignar licencias en una lista.
  * Asignar licencias a uno o varios usuarios al mismo tiempo.
  * Asignar y administrar diferentes tipos de licencias (de estar disponible).
  * Validar si una licencia ya está asignada a otro usuario.
  * Cancelar su suscripción.
* Proporcione una introducción sobre cómo usar la aplicación.
* Agregue formas de obtener soporte técnico, como Preguntas más frecuentes, bases de conocimiento o una dirección correo electrónico de contacto.
* Proporcione un vínculo que facilite que el suscriptor vuelva a la página de aterrizaje. Por ejemplo, incluya este vínculo en la pestaña **Acerca de** en su aplicación.

## <a name="create-your-saas-offer"></a>Crear la oferta de SaaS

Una vez que haya integrado las API de suministro de SaaS y creado la página de aterrizaje en la que los usuarios puedan administrar sus suscripciones, es el momento de crear, probar y publicar oficialmente la oferta de SaaS comercializable.

### <a name="create-the-offer"></a>Crear la oferta

Consulte [Crear una oferta SaaS](/azure/marketplace/create-new-saas-offer) para obtener instrucciones completas sobre cómo hacerlo en el Centro de partners. Los pasos siguientes describen de forma general cómo hacerlo.

1. Cree una cuenta en el [Centro de partners](https://partner.microsoft.com/) si no tiene una.

1. Configure los planes de suscripción, los detalles de precios y mucho más para la oferta de SaaS comercializable. En particular, asegúrese de realizar lo siguiente:

    * En **Detalles de configuración**, seleccione la opción **Sí** para especificar que vende la oferta a través de Microsoft.

    * En **Integración con Microsoft 365**, agregue el vínculo AppSource a la descripción de la aplicación. Este paso garantiza que los usuarios puedan comprar sus planes de suscripción en AppSource además de en Teams.

1. Almacene el publicador y los identificadores de la oferta. (Los necesitará más adelante para vincular la oferta a la aplicación en el Portal para desarrolladores).

1. Publique su oferta en el marketplace.

### <a name="test-the-offer"></a>Probar la oferta

Le recomendamos encarecidamente comprobar la experiencia de compra de un extremo a otro antes de publicar la oferta de SaaS. Para ello puede crear una oferta separada solo para pruebas. Para obtener información completa, consulte [Información general de la oferta de prueba](/azure/marketplace/plan-saas-offer#test-offer), [Crear una oferta de prueba](/azure/marketplace/create-saas-dev-test-offer) y [Versión preliminar de la oferta](/azure/marketplace/test-publish-saas-offer).

> [!IMPORTANT]
> Puede probar una transacción de un extremo a otro en Teams mediante la característica [Probar vista previa para aplicaciones monetizadas](Test-preview-for-monetized-apps.md). Para las ofertas en directo, debe completar el proceso de validación de la tienda de aplicaciones.

En lo que respecta a Teams, estas pruebas deben comprobar que el número de licencias y asignaciones coincida con lo que se ve en el Centro de administración de Teams cuando los usuarios:

* Activen y configuren su plan de suscripción en la página de aterrizaje.
* Asignen, quiten o reasignen licencias, tanto para ellos mismos como para otras personas.
* Cancelen o renueven su suscripción.

### <a name="publish-the-offer"></a>Publicar la oferta

Cuando termine de probar, [publique la oferta en directo](/azure/marketplace/test-publish-saas-offer#publish-your-offer-live).

## <a name="configure-your-app-for-the-saas-offer"></a>Configurar la aplicación para la oferta de SaaS

Ya ha publicado la oferta de SaaS, pero todavía debe vincularla a la aplicación de Teams para que los usuarios puedan ver los planes de suscripción en la tienda de Teams.

1. Vaya al [Portal para desarrolladores](https://dev.teams.microsoft.com/) y seleccione **Aplicaciones**.
1. En la página **Aplicaciones**, seleccione la aplicación a la que va a vincular la oferta de SaaS.
1. Vaya a la página **Planes y precios** y especifique el editor y los identificadores de la oferta. Si no los tiene a mano, puede encontrar estos identificadores en el Centro de partners.
1. Seleccione **Ver** para obtener una vista previa de los planes de suscripción de la oferta SaaS.
1. Si todo parece correcto, seleccione **Guardar**.

   La propiedad `subscriptionOffer` se agrega al [manifiesto de aplicación](~/resources/schema/manifest-schema-dev-preview.md#subscriptionoffer).

   ```json
      "subscriptionOffer": {
        "offerId": "publisherId.offerId"  
        }
   ```

## <a name="publish-your-app"></a>Publicar la aplicación

Ha creado la oferta de SaaS y la ha vinculado a su aplicación de Teams. Ahora es el momento de publicar la aplicación en la tienda de Teams. Para obtener instrucciones completas, vea [Publicar la aplicación en la tienda de Teams](~/concepts/deploy-and-publish/appsource/publish.md).

> [!IMPORTANT]
>
> * Aún en el caso de que la aplicación aparezca en la tienda de Teams, tendrá que repetir el proceso de validación de la tienda para incluir su oferta de SaaS.
> * Las ofertas de tarifa plana creadas sin el identificador de oferta y el identificador del publicador en el manifiesto de la aplicación deben actualizarse y volver a enviarse para su validación.

Tras la publicación, los usuarios verán la opción **Comprar una suscripción** en el cuadro de diálogo de detalles de la aplicación cuando intenten agregar la aplicación a Teams.

## <a name="end-user-purchasing-experience"></a>Experiencia de compra del usuario final

En el ejemplo siguiente se muestra cómo los usuarios pueden comprar planes de suscripción para una aplicación ficticia de Teams denominada *Recloud*.

1. En la tienda de Teams, busque y seleccione la aplicación *Recloud*.

1. En el cuadro de diálogo de detalles de la aplicación, seleccione **Comprar una suscripción**.

    :::image type="content" source="~/assets/images/saas-offer/buysubscriptionplan.png" alt-text="Compra de la suscripción para la aplicación seleccionada.":::

1. Seleccione su país para ver los planes de suscripción en su ubicación.

1. En el cuadro de diálogo **Elegir un plan de suscripción**, elija el plan que desee y seleccione **Finalizar la compra**. Nota: Los planes privados solo son visibles para los usuarios de las organizaciones a las que proporciona la oferta. Estos planes se distinguen mediante un **icono de** Oferta especial:::image type="icon" source="~/assets/icons/special-icon.png":::.

    :::image type="content" source="~/assets/images/saas-offer/choosingsubscriptionplan.png" alt-text="Selección del plan de suscripción adecuado.":::

1. En el cuadro de diálogo de **Finalizar la compra**, proporcione la información necesaria y seleccione **Realizar pedido**.

    :::image type="content" source="~/assets/images/saas-offer/placesubscriptionorder.png" alt-text="Realización del pedido de suscripción.":::

1. Cuando se le pida, seleccione **Configurar ahora** para configurar la suscripción.

    :::image type="content" source="~/assets/images/saas-offer/saas-offer-set-up.png" alt-text="Configurar la suscripción.":::

1. Administre su plan de suscripción a través del sitio web de *Recloud* (también conocido como [página de aterrizaje](#build-a-landing-page-for-subscription-management)).

    :::image type="content" source="~/assets/images/saas-offer/subscriptionlicenses.png" alt-text="Configuración de licencias de usuario.":::

## <a name="admin-purchasing-experience"></a>Experiencia de compra de administradores

Los administradores pueden comprar planes de suscripción de aplicaciones en el [Centro de administración de Teams](/MicrosoftTeams/purchase-third-party-apps).

## <a name="remove-a-saas-offer-from-your-app"></a>Quitar una oferta SaaS de la aplicación

Si desvincula una oferta de SaaS incluida en la descripción de la tienda de Teams, tendrá que volver a publicar la aplicación para ver el cambio en la tienda.

1. Vaya al [Portal para desarrolladores](https://dev.teams.microsoft.com/) y seleccione **Aplicaciones**.
1. En la página **Aplicaciones**, seleccione la aplicación de la que va a quitar la oferta.
1. Vaya a la página **Planes y precios** y seleccione **Revertir**.
1. Una vez desvinculada la oferta, haga lo siguiente para actualizar la descripción de la tienda:
   1. Seleccione **Distribuir > Publicar en la tienda de Teams**.
   1. Seleccione **Abrir Centro de partners** para iniciar el proceso de volver a publicar la aplicación sin la oferta.

## <a name="see-also"></a>Vea también

* [Mantenimiento y soporte técnico de su aplicación publicada](../post-publish/overview.md)
* [Directrices de validación para las aplicaciones vinculadas a la oferta de SaaS](teams-store-validation-guidelines.md#apps-linked-to-saas-offer)

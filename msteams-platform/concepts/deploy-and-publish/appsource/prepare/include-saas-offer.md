---
title: Incluir una oferta de SaaS con la aplicación
description: Aprenda a monetizar la aplicación de Microsoft Teams mediante la venta de planes de suscripción directamente desde la descripción de la tienda de Teams. Descripción de la experiencia de compra de administración, usuario final y aplicación de publicación.
author: heath-hamilton
ms.author: surbhigupta
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: 23327ea2765eb5496f8cfb157cdd194fcc13aaf7
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243258"
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
* Apoye la opción de varios administradores. En otras palabras, que varios usuarios de la misma organización puedan comprar y administrar sus propias suscripciones.

## <a name="manage-license-for-third-party-apps-in-teams"></a>Administración de licencias para aplicaciones de terceros en Teams

Teams permite a los administradores o usuarios independientes de proveedores de software (ISV) administrar licencias SaaS para aplicaciones de terceros compradas en el escaparate de Teams. Los administradores o usuarios de ISV pueden asignar, anular la asignación, usar y realizar un seguimiento de las licencias SaaS fácilmente.

Para habilitar la administración de licencias para una aplicación en Teams, siga estos pasos:

1. [Creación de una oferta en el Centro de partners](#create-an-offer-in-partner-center)
1. [Actualización de la aplicación de Teams](#update-your-teams-app)
1. [Después de la compra](#post-purchase)
1. [Integración con Graph Usage Right API](#integrate-with-graph-usage-right-api)

### <a name="create-an-offer-in-partner-center"></a>Creación de una oferta en el Centro de partners

1. Inicie sesión en el [Centro de partners](https://partner.microsoft.com/) y seleccione **Centro de partners**.

   :::image type="content" source="~/assets/images/first-party-license-mgt/partner-center-home-page.png" alt-text="En las capturas de pantalla se muestra cómo iniciar sesión en la cuenta del Centro de partners.":::

1. En la página **Inicio** , seleccione la pestaña **Ofertas de Marketplace** para definir ofertas de Marketplace comercial.

   :::image type="content" source="~/assets/images/first-party-license-mgt/home-page.png" alt-text="En las capturas de pantalla se muestra la página principal y la pestaña oferta de Marketplace en el Centro de partners.":::

1. Seleccione **Información general** en el panel izquierdo.

1. Seleccione **Nuevo software de oferta** > **como servicio**.

   :::image type="content" source="~/assets/images/first-party-license-mgt/commercial-marketplace.png" alt-text="En las capturas de pantalla se muestra la página de la oferta de Marketplace, donde puede seleccionar una nueva oferta.":::

1. Escriba **Id. de oferta** y **Alias de oferta** y seleccione **Crear**.

   > [!NOTE]
   > Si va a crear una oferta con fines de prueba, agregue el texto **-ISVPILOT** al final del alias de la oferta. Esto indica al equipo de certificación que la oferta tiene fines de prueba. Microsoft elimina ofertas con **-ISVPILOT** periódicamente. Por lo tanto, no use esta etiqueta por motivos distintos de probar la funcionalidad de administración de licencias.

   :::image type="content" source="~/assets/images/first-party-license-mgt/saas.png" alt-text="En las capturas de pantalla se muestra cómo escribir el identificador de la oferta y el alias de la oferta en el Centro de partners.":::

1. En la página Configuración de la oferta, en Detalles del programa de instalación, active la casilla **Sí, me gustaría que Microsoft administrara las licencias de cliente en mi nombre**.

   :::image type="content" source="~/assets/images/first-party-license-mgt/saas-isvpilot.png" alt-text="En las capturas de pantalla se muestra la página de configuración de la oferta para configurar la licencia que se va a administrar para la aplicación en Teams.":::

   > [!NOTE]
   >
   > * Se trata de una configuración única y no se puede cambiar una vez publicada la oferta. Esto permite al cliente administrar licencias para la aplicación en Teams.
   > * El manifiesto de aplicación solo admite una oferta para una aplicación. Elija una solución de administración de licencias adecuada para todos los planes disponibles en la oferta y no puede cambiar esta opción después de que la oferta se inserte en vivo.

1. Seleccione **Guardar borrador**.

1. Seleccione **Información general del plan** en el panel izquierdo y, a continuación, seleccione **Crear nuevo plan**.

   > [!NOTE]
   > Debe agregar al menos un plan.

   :::image type="content" source="~/assets/images/first-party-license-mgt/plan-overview.png" alt-text="En las capturas de pantalla se muestra información general del plan para crear un nuevo plan para las aplicaciones en el Centro de partners.":::

1. Escriba Id. de plan y Nombre del plan y, a continuación, seleccione **Crear**.

1. Escriba el **nombre del plan** y la **descripción del plan**.

   > [!NOTE]
   > La información del plan se muestra en Marketplace de Teams y [Appsource](https://appsource.microsoft.com/) en la lista de ofertas (sección planes).

   :::image type="content" source="~/assets/images/first-party-license-mgt/plan-listing.png" alt-text="En las capturas de pantalla se muestra la página del plan para agregar el nombre del plan y la descripción del plan para la aplicación.":::

1. Seleccione **Guardar borrador**.

1. Seleccione **Precios y disponibilidad** en el panel izquierdo.

1. Agregue los detalles de precios y disponibilidad.

   :::image type="content" source="~/assets/images/first-party-license-mgt/pricing-availability.png" alt-text="En las capturas de pantalla se muestra la página precios y disponibilidad para agregar la oferta de SaaS para la aplicación.":::

1. Seleccione **Guardar borrador**.

1. Seleccione **Información general del plan** en la parte superior de la página para ir a la página de lista que muestra todos los planes que ha creado para esta oferta.

   :::image type="content" source="~/assets/images/first-party-license-mgt/list-of-plans-created.png" alt-text="En las capturas de pantalla se muestra la página de lista de planes con el identificador de servicio, el modelo de precios, la disponibilidad, el estado y la acción.":::

1. Copie el identificador de servicio del plan que creó para integrarlo con Microsoft Graph Usage Rights API.

### <a name="update-your-teams-app"></a>Actualización de la aplicación de Teams

Actualice la aplicación de Teams para que se asigne a la funcionalidad de pago y [asigne la aplicación de Teams](https://aka.ms/TMTG) a su oferta y publicación.

### <a name="post-purchase"></a>Después de la compra

1. Después de la activación, se redirige al cliente desde la página de aterrizaje a Administración de licencias de Teams.

1. Una vez completada correctamente la compra de la suscripción, se redirige al cliente a la página de aterrizaje de la aplicación para la activación de la suscripción. Esta es la experiencia existente para que el usuario compre [aplicaciones monetizadas en Teams](https://aka.ms/TMTG).

1. Una vez que el cliente activa la compra de suscripción en la página de aterrizaje, se redirige al cliente a la página de suscripciones de Teams a través de un vínculo o botón de [dirección URL de redireccionamiento](https://teams.microsoft.com/_#/subscriptionManagement) que el cliente selecciona en la página de aterrizaje del publicador.

### <a name="integrate-with-graph-usage-right-api"></a>Integración con Graph Usage Right API

Integre con Graph Usage Right API para administrar los permisos de usuario en el momento del inicio de la aplicación por parte de un cliente que tenga una licencia de compra. Debe determinar los permisos del usuario para la aplicación con una llamada de Graph a usage rights API.

Puede llamar a graph API para determinar si el usuario que ha iniciado sesión actualmente con una suscripción válida del plan tiene acceso a la aplicación. Para llamar a Graph UsageRight API para comprobar los permisos de usuario, siga estos pasos:

1. Obtener el token de OBO de usuario: [obtener acceso en nombre de un usuario: Microsoft Graph | Microsoft Docs](/graph/auth-v2-user).

1. Llamar a Graph para obtener el identificador de objeto del usuario: [use Microsoft Graph API - Microsoft Graph | Microsoft Docs](/graph/use-the-api).

1. Llame a UsageRights API para determinar que el usuario tiene licencia para el plan [Enumerar uso de usuarioRights - Microsoft Graph beta | Microsoft Docs](/graph/api/user-list-usagerights?view=graph-rest-beta&tabs=http&preserve-view=true).

   > [!NOTE]
   > Debe tener permisos mínimos `User.Read` para llamar a UsageRights.
   > La API UsageRights está actualmente en versión beta. Una vez actualizada la versión a V1, los usuarios de ISV deben actualizar de la versión beta a la versión V1.

### <a name="check-license-usage-in-partner-center-analytics"></a>Comprobación del uso de licencias en el análisis del Centro de partners

1. Inicie sesión en el [Centro de partners](https://partner.microsoft.com/).
1. En el panel izquierdo, vaya a **Marketplace comercial > Analizar licencias de >**.
1. Seleccione **Planear e inquilino** en el widget de informes para ver el uso de mes.

## <a name="build-a-landing-page-for-subscription-management"></a>Crear una página de aterrizaje para la administración de suscripciones

Cuando alguien termine de comprar un plan de suscripción para su aplicación en la tienda de Teams, el marketplace le dirigirá a la página de aterrizaje donde podrá administrar la suscripción (por ejemplo, asignar una licencia a un usuario específico de su organización).

Seleccione **No, preferiría administrar las licencias de cliente yo mismo** en tales casos.

Para obtener instrucciones completas, consulte [Crear la página de aterrizaje de la oferta de SaaS](/azure/marketplace/azure-ad-transactable-saas-landing-page).

Cuando alguien termine de comprar un plan de suscripción para la aplicación y quiera permanecer en Teams, sin dirigirlo a la página de aterrizaje, seleccione **Sí, me gustaría que Microsoft administrara las licencias de cliente en mi nombre**.

Para obtener más información, consulte [Administración de licencias de primera persona](/platform/concepts/deploy-and-publish/appsource/prepare/first-party-license-management).

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

1. Almacene su editor y ofrezca los id. (los necesitará más adelante para vincular la oferta a su aplicación en el Portal de desarrolladores).

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

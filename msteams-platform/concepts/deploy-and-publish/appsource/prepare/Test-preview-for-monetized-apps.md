---
title: Vista previa de prueba para aplicaciones monetizadas
author: v-ypalikila
description: Crea y prueba ofertas de SaaS Preview para Teams aplicación antes de impulsar la oferta en directo.
ms.topic: conceptual
ms.author: v-ypalikila
ms.localizationpriority: medium
keywords: SaaS de aplicaciones de teams ofrecen versión preliminar de la oferta de prueba saas monetizadas
ms.openlocfilehash: 849dd2ecd79a4b43d6feb6ceaca599f371df1de1
ms.sourcegitcommit: 54f6690b559beedc330b971618e574d33d69e8a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2022
ms.locfileid: "62363481"
---
# <a name="test-preview-for-monetized-apps"></a>Vista previa de prueba para aplicaciones monetizadas

> [!NOTE]
> La vista previa de prueba para aplicaciones monetizadas solo está disponible actualmente en [**la vista previa del desarrollador**](/microsoftteams/platform/resources/dev-preview/developer-preview-intro).

Puedes crear una oferta de Software como servicio (SaaS) y probar la experiencia de compra de un extremo a otro para tus aplicaciones monetizadas en Teams. Los usuarios que se agregan como la audiencia de vista previa de la aplicación Teams pueden revisar la oferta saas antes de publicarla.

## <a name="create-a-preview-offer-id"></a>Crear un identificador de oferta de vista previa

Puedes generar el identificador de la oferta de vista previa desde el vínculo **de vista previa de AppSource** en el Centro de partners. Asegúrese de que la oferta SaaS se encuentra en la fase de creación de vista previa. Para generar el identificador de la oferta de vista previa:

1. Vaya al [Centro de partners](https://go.microsoft.com/fwlink/?linkid=2166002) e inicie sesión con sus credenciales de desarrollador.
1. Seleccione **Ofertas de Marketplace**.
1. Seleccione la oferta SaaS que desea obtener una vista previa.
1. Agrega una [audiencia de vista previa](/azure/marketplace/create-new-saas-offer-preview) para tu oferta SaaS.
1. Seleccione **Vínculo de vista previa de AppSource** en **Ir** a directo para buscar el identificador de la oferta de vista previa en la barra de direcciones del explorador con el formato *publisherId.offerId-preview* .

    :::image type="content" source="../../../../assets/images/apps-in-meetings/publish-status-publisher-signoff.png" alt-text="identificador de la oferta de vista previa" border="true" :::

1. Copie el identificador de la oferta de vista previa de la barra de direcciones del explorador.

      :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-monetized-apps-preview-offer-id.png" alt-text="Id. de oferta de vista previa" border="true" :::

    > [!NOTE]
    > A diferencia de un identificador de oferta pública, el identificador de la oferta de vista previa se puede reconocer con el *sufijo -preview* . Por ejemplo, **publisherId.offerId-preview**.

## <a name="configure-your-app-with-the-preview-offer-id"></a>Configurar la aplicación con el identificador de la oferta de vista previa

Antes de comenzar, inicie sesión en el **Portal** de desarrolladores con una cuenta  de desarrollador con audiencia de vista previa para que los usuarios puedan ver sus planes de suscripción en Teams tienda.

Después de generar el identificador de la oferta de vista previa, vincula el identificador de la oferta a tu Teams aplicación. Para vincular el identificador de la oferta:

1. Ve a [Portal para desarrolladores](https://dev.teams.microsoft.com/) e inicia sesión con tus credenciales de desarrollador.
1. Selecciona **Aplicaciones** en el panel izquierdo.
1. Selecciona la aplicación a la que vincular la oferta SaaS.
1. Selecciona **Planes y precios e** escribe el identificador **Publisher id**. y **el identificador de oferta**.  
  Asegúrese de que el identificador de la *oferta contiene el sufijo -preview* .
1. Selecciona **Ver para** obtener una vista previa de los planes de suscripción.
1. Revisa los planes enumerados en **Suscripción a aplicaciones** y selecciona **Guardar**.

    :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-add-offer-id.png" alt-text="agregar identificador de oferta" :::

La propiedad subscriptionOffer se agrega al manifiesto de la aplicación.

```json
"subscriptionOffer": {
     "offerId": "publisherId.offerId-preview"  
     }
```

>[!NOTE]
> Busca la etiqueta *Oferta de vista previa* junto **a Suscripción a aplicaciones** para confirmar si la oferta es una oferta de vista previa.

## <a name="sideload-the-app-to-teams"></a>Descargar localmente la aplicación a Teams

Después de configurar la aplicación con el identificador de la oferta de vista previa, crea un paquete de aplicación actualizado y cárbalo en Teams para probar la experiencia de compra de un extremo a otro. Para obtener más información, [consulta Upload la aplicación en Microsoft Teams](../../apps-upload.md). También puedes seleccionar Vista previa **en Teams** en el Portal de desarrolladores para Teams para iniciar la aplicación rápidamente en el Teams cliente.

Si la oferta de vista previa se especifica en el manifiesto de la aplicación y la audiencia de vista previa se define en el Centro de partners para la oferta, el usuario puede ver el **botón Comprar una suscripción** .

:::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-buy-subscription.png" alt-text="comprar una suscripción" border="true":::

### <a name="error-scenarios"></a>Escenarios de error

* Si se especifica el identificador de la oferta, pero el usuario no forma parte de la  audiencia de vista previa definida en el Centro de partners, el botón Comprar una suscripción no está habilitado y la aplicación muestra el siguiente mensaje de advertencia al usuario:

  No se encontraron planes con **-preview**. Asegúrate de que estás en la audiencia de vista previa.

  :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-no-preview-audience.png" alt-text="sin audiencia previa" border="true" :::

* Si el identificador de oferta especificado en el manifiesto de la aplicación no es una oferta de vista previa, la aplicación muestra el siguiente mensaje de advertencia al usuario y la instalación local está deshabilitada:
  
  Esta no es una oferta de vista previa. Asegúrese de anexar **-preview** al Identificador de oferta.

  :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-no-preview-offer-id.png" alt-text="no -preview" border="true" :::

## <a name="see-also"></a>Consulte también

* [Incluir una oferta SaaS con tu Microsoft Teams aplicación](include-saas-offer.md)
* [Crear una oferta de software como servicio (SaaS)](include-saas-offer.md#create-your-saas-offer)
* [Agregar una audiencia de vista previa para una oferta SaaS](/azure/marketplace/create-new-saas-offer-preview)
* [Fase de creación de vista previa](/azure/marketplace/review-publish-offer)
* [Revisar y publicar una oferta en el mercado comercial](/azure/marketplace/review-publish-offer#validation-and-publishing-steps)

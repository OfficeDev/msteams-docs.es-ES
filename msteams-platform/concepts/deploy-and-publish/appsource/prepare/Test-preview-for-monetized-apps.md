---
title: Versión preliminar de prueba para aplicaciones monetizadas
author: v-ypalikila
description: Cree y pruebe las ofertas de la versión preliminar de SaaS para la aplicación Teams antes de publicar la oferta. Cree un identificador de oferta en versión preliminar, configure la aplicación con el identificador de la oferta en versión preliminar y realice la transferencia local.
ms.topic: conceptual
ms.author: v-ypalikila
ms.localizationpriority: high
ms.openlocfilehash: 98b9876a93fe6040cf66a16475fe7fdacf98a520
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100794"
---
# <a name="test-preview-for-monetized-apps"></a>Versión preliminar de prueba para aplicaciones monetizadas

Puede crear una oferta de software como servicio (SaaS) y probar la experiencia de compra de un extremo a otro para sus aplicaciones monetizadas en Teams. Los usuarios que se agregan como público preliminar de la aplicación de Teams pueden revisar la oferta de SaaS antes de publicarla.

## <a name="create-a-preview-offer-id"></a>Creación de un identificador de oferta de versión preliminar

Puede generar el identificador de la oferta de versión preliminar desde el vínculo **versión preliminar de AppSource** en el Centro de partners. Asegúrese de que la oferta de SaaS se encuentra en la fase de creación de la versión preliminar. Para generar el identificador de la oferta de versión preliminar:

1. Vaya al [Centro de partners](https://go.microsoft.com/fwlink/?linkid=2166002) e inicie sesión con sus credenciales de desarrollador.
1. Seleccione **Ofertas de Marketplace**.
1. Seleccione la oferta de SaaS que quiere obtener en versión preliminar.
1. Agregue un [público de versión preliminar](/azure/marketplace/create-new-saas-offer-preview) para la oferta de SaaS.
1. Seleccione el vínculo **Versión preliminar de AppSource** en **Publicar** para buscar el identificador de la oferta de versión preliminar en la barra de direcciones del explorador con formato *publisherId.offerId-preview*.

    :::image type="content" source="../../../../assets/images/apps-in-meetings/publish-status-publisher-signoff.png" alt-text="Id. de oferta de versión preliminar" :::

1. Copie el identificador de la oferta de versión preliminar de la barra de direcciones del explorador.

      :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-monetized-apps-preview-offer-id.png" alt-text="Id. de oferta de versión preliminar" :::

    > [!NOTE]
    > Unlike a public offer ID, the Preview offer ID can be recognized with the *-preview* suffix. For example, **publisherId.offerId-preview**.

## <a name="configure-your-app-with-the-preview-offer-id"></a>Configuración de la aplicación con el identificador de la oferta de versión preliminar

Antes de empezar, inicie sesión en el **Portal para desarrolladores** con una cuenta de desarrollador con **público de versión preliminar** para que los usuarios vean sus planes de suscripción en la tienda de Teams.

After you've generated your Preview offer ID, link the offer ID to your Teams app. To link the offer ID:

1. Vaya al [Portal para desarrolladores](https://dev.teams.microsoft.com/) e inicie sesión con sus credenciales de desarrollador.
1. Seleccione **Aplicaciones** en el panel izquierdo.
1. Seleccione la aplicación a la que vincular la oferta de SaaS.
1. Seleccione **Planes y precios** y escriba el **Id. del publicador** y el **Id. de oferta**.  
  Asegúrese de que el identificador de oferta contiene el sufijo *-preview*.
1. Seleccione **Ver** para obtener una vista previa de los planes de suscripción de la oferta SaaS.
1. Revise los planes que aparecen en **Suscripción de aplicaciones** y seleccione **Guardar**.

    :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-add-offer-id.png" alt-text="agregar id. de oferta" :::

La propiedad subscriptionOffer se agrega al manifiesto de la aplicación.

```json
"subscriptionOffer": {
     "offerId": "publisherId.offerId-preview"  
     }
```

>[!NOTE]
> Compruebe la etiqueta *Oferta de versión preliminar* junto a **Suscripción de aplicaciones** para confirmar si la oferta es una oferta de versión preliminar.

## <a name="sideload-the-app-to-teams"></a>Transferir localmente la aplicación a Teams

Después de configurar la aplicación con el identificador de la oferta de versión preliminar, cree un paquete de aplicación actualizado y cárguelo en Teams para probar la experiencia de compra de un extremo a otro. Para más información, vea [Cargar la aplicación en Microsoft Teams](../../apps-upload.md). También puede seleccionar **Vista previa en Teams** en el Portal para desarrolladores para que Teams inicie la aplicación rápidamente en el cliente de Teams.

Si la oferta de versión preliminar se especifica en el manifiesto de la aplicación y el público para la versión preliminar se define en el Centro de partners para la oferta, el usuario puede ver el botón **Comprar una suscripción**.

:::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-buy-subscription.png" alt-text="comprar una suscripción":::

### <a name="error-scenarios"></a>Escenarios de error

* Si se especifica el identificador de oferta, pero el usuario no forma parte del **Público para la versión preliminar** definido en el Centro de partners, el botón **Comprar una suscripción** no está habilitado y la aplicación muestra el siguiente mensaje de advertencia al usuario:

  No se encontraron planes con **-preview**. Asegúrese de que está en el público para la versión preliminar.

  :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-no-preview-audience.png" alt-text="no hay público para la versión preliminar" :::

* Si el identificador de oferta especificado en el manifiesto de la aplicación no es una oferta de versión preliminar, la aplicación muestra el siguiente mensaje de advertencia al usuario y la instalación de prueba está deshabilitada:
  
  Esta no es una oferta en versión preliminar. Asegúrese de anexar **-preview** al identificador de la oferta.

  :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-no-preview-offer-id.png" alt-text="sin -preview" :::

## <a name="see-also"></a>Vea también

* [Incluir una oferta de SaaS con la aplicación de Microsoft Teams](include-saas-offer.md)
* [Crear una oferta de software como servicio (SaaS)](include-saas-offer.md#create-your-saas-offer)
* [Agregar un público para versión preliminar para una oferta de SaaS](/azure/marketplace/create-new-saas-offer-preview)
* [Fase de creación de versión preliminar](/azure/marketplace/review-publish-offer)
* [Revisar y publicar una oferta en el marketplace comercial](/azure/marketplace/review-publish-offer#validation-and-publishing-steps)

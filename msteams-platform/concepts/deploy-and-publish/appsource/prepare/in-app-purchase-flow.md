---
title: Flujo de compra desde la aplicación para monetización de aplicaciones
description: Obtenga información sobre las tareas y los conceptos básicos necesarios para implementar las compras desde la aplicación y la funcionalidad de prueba en las aplicaciones de Teams.
author: v-npaladugu
ms.author: surbhigupta
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: 59511c62fbc03b2d730bbbcccf5f4d2eadc37885
ms.sourcegitcommit: f192d7685ee3ddf4a55dc9787d56744403c3f8f9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/10/2022
ms.locfileid: "67302461"
---
# <a name="in-app-purchases"></a>Compras desde la aplicación

Microsoft Teams proporciona API que puede usar para implementar las compras desde la aplicación para actualizar las aplicaciones de Teams de gratuitas a pagas. La compra desde la aplicación permite convertir a los usuarios de planes gratuitos en usuarios de pago directamente desde dentro de la aplicación.

## <a name="implement-in-app-purchases"></a>Implementar compras desde la aplicación

Para ofrecer una experiencia de compra desde la aplicación a los usuarios de la aplicación, asegúrese de lo siguiente:

* La aplicación se basa en la [biblioteca del SDK de cliente de Teams](https://github.com/OfficeDev/microsoft-teams-library-js).

* La aplicación está habilitada con una[ oferta de SaaS](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md) transaccionable.

* La aplicación está habilitada con [permisos de RSC](#update-manifest).

* La aplicación se invoca con [`openPurchaseExperience` API](#purchase-experience-api).

La experiencia de compra desde la aplicación se puede habilitar actualizando el archivo `manifest.json` o habilitando **Mostrar ofertas de compra desde la aplicación** desde la sección **Permisos** de la **Portal para desarrolladores**.

### <a name="update-manifest"></a>Actualizar manifiesto

Para habilitar la experiencia de compra desde la aplicación, actualice el archivo `manifest.json` de la aplicación de Teams agregando los permisos de RSC. Permite a los usuarios de la aplicación actualizar a una versión de pago de la aplicación y empezar a usar nuevas funcionalidades. La actualización del manifiesto de la aplicación es la siguiente:

```json

"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "InAppPurchase.Allow.User",
                "type": "Delegated"
            }
        ]
    }
}
```

### <a name="purchase-experience-api"></a>API de experiencia de compra

Para desencadenar la compra desde la aplicación para la aplicación, invoque la API `openPurchaseExperience` desde la aplicación web.

El siguiente fragmento de código es un ejemplo de llamada a la API desde la aplicación Teams creada con el SDK de cliente de JavaScript de Teams:

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/jsonV11)

```json
<div> 
<div class="sectionTitle">openPurchaseExperience</div>
<button onclick="openPurchaseExperience()">openPurchaseExperience</button>
</div>
</body>
<script>
   function openPurchaseExperience()
      microsoftTeams.initialize();
      let callbackcalled = false;
      microsoftTeams.monetization.openPurchaseExperience((e) => {
            console.log("callback is being called");
            console.log(e);
            if (!!e && typeof e !== "string") {
                  alert(JSON.stringify(e));
              }
              return;
            });
      console.log("after callback: ",callbackcalled);
    }
</script>
```

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/jsonV2)

```json
<div>
<div class="sectionTitle">openPurchaseExperience</div>
<button onclick="openPurchaseExperience()">openPurchaseExperience</button>
</div>
</body>
<script>
   function openPurchaseExperience() {
      app.initialize();
    var planInfo = {
        planId: "<Plan id>", // Plan Id of the published SAAS Offer
        term: "<Plan Term>" // Term of the plan.
    }
      monetization.openPurchaseExperience(planInfo);
    }
</script>
```

---

## <a name="end-user-in-app-purchasing-experience"></a>Experiencia de compra desde la aplicación del usuario final

En el ejemplo siguiente se muestra a los usuarios la opción de comprar planes de suscripción para una aplicación ficticia de Teams denominada *Tareas de Contoso para Teams*:

1. En la **tienda** de Teams, busque y seleccione la aplicación

1. En el cuadro de diálogo de detalles de la aplicación, seleccione **Comprar una suscripción** o **Agregar para mí**.

    :::image type="content" source="~/assets/images/saas-offer/buysubscriptionplancontoso.png" alt-text="Compra de la suscripción para la aplicación seleccionada.":::

1. **Agregar para mí** ofrece una versión de evaluación gratuita de la aplicación y, posteriormente, **Actualizar** a una versión de pago.

    :::image type="content" source="~/assets/images/saas-offer/upgradeapp.png" alt-text="Actualizar a la suscripción de la aplicación seleccionada." lightbox="../../../../assets/images/saas-offer/upgradeapp.png":::

1. En el cuadro de diálogo **Elegir un plan de suscripción**, elija el plan y seleccione **Finalizar la compra**.

    :::image type="content" source="~/assets/images/saas-offer/choosingsubscriptionplancontoso.png" alt-text="Selección del plan de suscripción adecuado." lightbox="../../../../assets/images/saas-offer/choosingsubscriptionplancontoso.png":::

1. Complete la transacción y seleccione **Configurar ahora** para configurar la suscripción.

    :::image type="content" source="~/assets/images/saas-offer/saas-offer-configure-now.png" alt-text="Configurar la suscripción." lightbox="../../../../assets/images/saas-offer/saas-offer-configure-now.png":::

    :::image type="content" source="~/assets/images/saas-offer/getstarted.png" alt-text="Página de aterrizaje de la suscripción." lightbox="../../../../assets/images/saas-offer/getstarted.png":::

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Versión preliminar de prueba para aplicaciones monetizadas](~/concepts/deploy-and-publish/appsource/prepare/Test-preview-for-monetized-apps.md)

## <a name="see-also"></a>Vea también

* [Incluir una oferta de SaaS con la aplicación de Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
* [Crear una oferta de software como servicio (SaaS)](include-saas-offer.md#create-your-saas-offer)

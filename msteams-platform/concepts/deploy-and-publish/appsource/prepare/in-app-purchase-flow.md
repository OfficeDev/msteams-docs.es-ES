---
title: Flujo de compra desde la aplicación para la monetización de aplicaciones
description: Obtén información sobre las tareas y conceptos básicos necesarios para implementar las compras desde la aplicación y la funcionalidad de prueba en las aplicaciones de teams.
author: v-npaladugu
ms.author: surbhigupta
ms.topic: how-to
localization_priority: Normal
ms.openlocfilehash: 455809e64a934384d28e00bdf721ae8c66cb7d19
ms.sourcegitcommit: 54f6690b559beedc330b971618e574d33d69e8a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2022
ms.locfileid: "62363470"
---
# <a name="in-app-purchases"></a>Compras desde la aplicación

Microsoft Teams las API que puedes usar para implementar las compras desde la aplicación para actualizar de aplicaciones gratuitas a Teams de pago. La compra desde la aplicación te permite convertir usuarios de planes gratuitos a de pago directamente desde tu aplicación.

> [!NOTE]
> Las compras desde la aplicación para Teams aplicaciones están disponibles actualmente solo en la [**versión preliminar del desarrollador**](/microsoftteams/platform/resources/dev-preview/developer-preview-intro).

## <a name="implement-in-app-purchases"></a>Implementar compras desde la aplicación

Para ofrecer una experiencia de compra desde la aplicación a los usuarios de la aplicación, asegúrate de lo siguiente:

* La aplicación se basa en [Teams de SDK de cliente](https://github.com/OfficeDev/microsoft-teams-library-js).

* La aplicación está habilitada con una oferta [SaaS transaccionable](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md).

* La aplicación está habilitada con [permisos RSC](#update-manifest).

* La aplicación se invoca con [`openPurchaseExperience` la API](#purchase-experience-api).

La experiencia de compra desde la aplicación se puede habilitar actualizando el archivo **manifest.json** o habilitando **Mostrar** ofertas de compra desde  la aplicación desde la sección Permisos del **Portal de desarrolladores**.

### <a name="update-manifest"></a>Manifiesto de actualización

Para habilitar la experiencia de compra desde la aplicación, actualice el archivo **manifest.json** Teams aplicación agregando los permisos de RSC. Permite a los usuarios de la aplicación actualizar a una versión de pago de la aplicación y empezar a usar nuevas funcionalidades. La actualización del manifiesto de la aplicación es la siguiente:

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
```

### <a name="purchase-experience-api"></a>API de experiencia de compra

Para desencadenar la compra desde la aplicación para la aplicación, invoque la `openPurchaseExperience` API desde la aplicación web.

A continuación se muestra un ejemplo de cómo llamar a la API desde la aplicación:

```json
<body> 
<div> 
<div class="sectionTitle">openPurchaseExperience</div> 
<button onclick="openPurchaseExperience()">openPurchaseExperience</button> 
</div> 
</body> 
<script> 
   function openPurchaseExperience() {
      microsoftTeams.initialize();
      let callbackcalled = false;
      microsoftTeams.monetization.openPurchaseExperience((e) => {
      console.log("callback is being called");
      callbackcalled = true;  
      if (!!e && typeof e !== "string") {
            e = JSON.stringify(e);
            alert(e);
        }
        return;
      });
      console.log("after callback: ",callbackcalled);
    } 
</script> 
```

## <a name="end-user-in-app-purchasing-experience"></a>Experiencia de compra desde la aplicación del usuario final

En el ejemplo siguiente se muestra a los usuarios comprar planes de suscripción para una aplicación ficticia Teams llamada *Contoso Tasks for Teams*:

1. En la Teams **,** busca y selecciona la aplicación.

1. En el cuadro de diálogo detalles de la aplicación, selecciona **Comprar una suscripción** o **Agregar para mí**. 

    :::image type="content" source="~/assets/images/saas-offer/buysubscriptionplancontoso.png" alt-text="Comprar la suscripción para la aplicación seleccionada." border="true":::

    
1. **Agregar para mí ofrece** una versión de prueba gratuita de la aplicación y, posteriormente **, actualizarla** a una versión de pago.

    :::image type="content" source="~/assets/images/saas-offer/upgradeapp.png" alt-text="Actualizar a la suscripción de la aplicación seleccionada." border="true":::

1. En el **cuadro de diálogo Elegir un plan de** suscripción, elija el plan y seleccione **Desprotección**.

    :::image type="content" source="~/assets/images/saas-offer/choosingsubscriptionplancontoso.png" alt-text="Seleccionar el plan de suscripción adecuado." border="true":::

1. Complete la transacción y **seleccione Configurar ahora** para configurar la suscripción.

    :::image type="content" source="~/assets/images/saas-offer/saas-offer-configure-now.png" alt-text="Configurar la suscripción." border="true":::

    :::image type="content" source="~/assets/images/saas-offer/getstarted.png" alt-text="Página de aterrizaje de la suscripción." border="true":::


## <a name="see-also"></a>Consulte también

* [Incluir una oferta SaaS con tu Microsoft Teams aplicación](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
* [Crear una oferta de software como servicio (SaaS)](include-saas-offer.md#create-your-saas-offer)
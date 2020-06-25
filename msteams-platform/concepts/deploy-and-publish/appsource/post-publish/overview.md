---
title: Publicación posterior
description: Qué hacer después de publicar la aplicación
keywords: certificado de actualización de publicación de publicaciones de Teams
ms.openlocfilehash: 77b74d77546de0ae93b0ae39aec925d2e3dec2cf
ms.sourcegitcommit: fdc50183f3f4bec9e4b83bcfe5e016b591402f7c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/24/2020
ms.locfileid: "44867106"
---
# <a name="maintain-and-support-your-published-app"></a>Mantener y admitir la aplicación publicada 

Después de aprobar la aplicación y enumerarla en el catálogo de aplicaciones públicas, puede aumentar su alcance si logra la certificación de la aplicación o agrega un botón Descargar en el sitio Web.

## <a name="application-certificate"></a>Certificado de la aplicación

Microsoft proporciona un [programa de certificación de aplicaciones](./application-certification.md) que compila la información de la aplicación y la presenta en la [Página seguridad y cumplimiento de aplicaciones de Microsoft Teams](https://aka.ms/AppCertification). Esta información está destinada a ayudar a los administradores a elegir aplicaciones que sean seguras para sus organizaciones.

## <a name="add-a-download-button-to-your-product-site"></a>Agregar un botón Descargar al sitio del producto

Si la aplicación está en la tienda Microsoft Teams, puede generar un vínculo para su sitio web que inicie Teams y que muestre un cuadro de diálogo de consentimiento e instalación para que los usuarios agreguen la aplicación.
El formato es: `https://teams.microsoft.com/l/app/<appId>` donde appID es el GUID que declaran en el manifiesto enviado.
Ejemplo: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` es el vínculo para instalar Trello.

## <a name="updating-your-existing-teams-app"></a>Actualización de la aplicación de Teams existente

* No use el botón *Agregar una nueva aplicación* para volver a enviar la aplicación. En su lugar, use el icono de la aplicación en la pestaña Información general.
* El appId del manifiesto actualizado debe ser el mismo que el del manifiesto actual, con un número de versión incrementado.
* Aumente el número de versión en el manifiesto si realiza cambios en el manifiesto en el envío.
* Los envíos actualizados son necesarios para someterse a un nuevo proceso de revisión y validación.

## <a name="app-updates-and-the-user-consent-flow"></a>Actualizaciones de aplicaciones y flujo de consentimiento del usuario

Cuando un usuario instala la aplicación, uno de los primeros elementos que conviene dar permiso a la aplicación para acceder a los servicios y la información que la aplicación necesita para realizar su trabajo. En la mayoría de los casos, después de completar una actualización de la aplicación, la nueva versión aparecerá automáticamente para los usuarios finales. Sin embargo, hay algunas actualizaciones en el [manifiesto de la aplicación Teams](../../../../resources/schema/manifest-schema.md) que requieren la aceptación del usuario para completarse y pueden volver a desencadenar este comportamiento de consentimiento:

 >[!div class="checklist"]
>
> * Se ha agregado o quitado un bot.
> * El valor único de un bot existente `botId` cambió.
> * Se ha cambiado el valor booleano de un bot existente `isNotificationOnly` .
> * Se ha cambiado el valor booleano de un bot existente `supportsFiles` .
> * `composeExtensions`Se ha agregado o quitado una extensión de mensajería.
> * Se ha agregado un nuevo conector.
> * Se ha agregado una nueva pestaña estática/personal.
> * Se ha agregado una nueva ficha configurable de grupo o canal.
> * Los `webApplicationInfo` valores cambiados.
>
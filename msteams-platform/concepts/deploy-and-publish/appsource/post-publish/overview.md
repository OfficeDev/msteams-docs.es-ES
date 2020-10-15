---
title: Publicación posterior
description: Qué hacer después de publicar la aplicación
keywords: manifiesto de actualización de la aplicación publicar actualización de Teams post
ms.openlocfilehash: 58e81688ab9a8b55d2b035fc9b43cb58dddb6133
ms.sourcegitcommit: 25afe104d10c9a6a2849decf5ec1d08969d827c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/14/2020
ms.locfileid: "48465918"
---
# <a name="maintain-and-support-your-published-app"></a>Ofrecer mantenimiento y soporte técnico de su aplicación publicada 

Después de aprobar la aplicación y enumerarla en el catálogo de aplicaciones públicas, puede aumentar su alcance completando el programa de cumplimiento de aplicaciones de Microsoft 365 o agregando un botón Descargar en el sitio Web.

## <a name="microsoft-365-certified"></a>Microsoft 365 certificado

El [programa de cumplimiento de aplicaciones 365 de Microsoft](./application-certification.md)es un enfoque de tres niveles para la seguridad y el cumplimiento de aplicaciones. Cada nivel se basa en el siguiente, que ofrece un programa con capas para satisfacer las necesidades del cliente. Puede obtener más información sobre la postura de seguridad y cumplimiento de las aplicaciones de Microsoft Teams visitando la [Página cumplimiento](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps).

## <a name="add-a-download-button-to-your-product-site"></a>Agregar un botón Descargar al sitio del producto

Si la aplicación está en el almacén global de Microsoft Teams, puede generar un vínculo para el sitio web que inicia Teams y que muestra un cuadro de diálogo de consentimiento e instalación para que los usuarios agreguen la aplicación.
El formato es:  `https://teams.microsoft.com/l/app/<appId>` donde appID es el GUID que declaran en el manifiesto enviado.
Ejemplo: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` es el vínculo para instalar Trello.

## <a name="updating-your-existing-teams-app"></a>Actualización de la aplicación de Teams existente

* No use el botón *Agregar una nueva aplicación* para volver a enviar la aplicación. En su lugar, use el icono de la aplicación en la pestaña Información general.
* El appId del manifiesto actualizado debe ser el mismo que el del manifiesto actual, con un número de versión incrementado.
* Aumente el número de versión en el manifiesto si realiza cambios en el envío, incluido el nombre de la aplicación o cualquier metadato del manifiesto.
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

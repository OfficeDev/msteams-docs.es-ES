---
title: Mantenimiento y soporte técnico de la aplicación publicada
description: Qué hacer después de publicar la aplicación
ms.topic: how-to
keywords: Manifiesto de actualización de la aplicación de certificación de actualización posterior a la publicación de teams
ms.openlocfilehash: ce63b840307f7e12a5cd05a1c67aed017cf6199b
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014330"
---
# <a name="maintain-and-support-your-published-app"></a>Ofrecer mantenimiento y soporte técnico de su aplicación publicada 

Después de que la aplicación se apruebe y aparezca en el catálogo de aplicaciones público, puede aumentar su alcance completando el Programa de cumplimiento de aplicaciones de Microsoft 365 o agregando un botón de descarga en su sitio web.

## <a name="microsoft-365-certified"></a>Certificado de Microsoft 365

El [Programa de cumplimiento de aplicaciones de Microsoft 365](./application-certification.md)es un enfoque de tres niveles para la seguridad y el cumplimiento de las aplicaciones. Cada nivel se basa en el siguiente: ofrece un programa en capas para satisfacer las necesidades del cliente. Puede obtener más información sobre la posición de seguridad y cumplimiento de las aplicaciones de Teams visitando la página [de cumplimiento.](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps)

## <a name="add-a-download-button-to-your-product-site"></a>Agregar un botón de descarga al sitio del producto

Si la aplicación está en la tienda global de Microsoft Teams, puede generar un vínculo para su sitio web que inicie Teams y muestre un cuadro de diálogo de consentimiento e instalación para que los usuarios agreguen la aplicación.
El formato es:  `https://teams.microsoft.com/l/app/<appId>` donde appID es el GUID que declaran en el manifiesto enviado.
Ejemplo: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` es el vínculo para instalar Trello.

## <a name="updating-your-existing-teams-app"></a>Actualizar la aplicación de Teams existente

* No use el *botón Agregar una nueva aplicación* para volver a enviar la aplicación. En su lugar, usa el icono de la aplicación en la pestaña Información general.
* El appId del manifiesto actualizado debe ser el mismo que en el manifiesto actual, con un número de versión incrementado.
* Incremente el número de versión en el manifiesto si realiza cambios en el envío, incluido el nombre de la aplicación o los metadatos del manifiesto.
* Los envíos actualizados son necesarios para someterse a un nuevo proceso de revisión y validación.

## <a name="app-updates-and-the-user-consent-flow"></a>Actualizaciones de aplicaciones y flujo de consentimiento del usuario

Cuando un usuario instala la aplicación, una de las primeras cosas que hace es dar permiso a la aplicación para acceder a los servicios e información que la aplicación necesita para realizar su trabajo. En la mayoría de los casos, después de completar una actualización de la aplicación, la nueva versión aparecerá automáticamente para los usuarios finales. Sin embargo, hay algunas actualizaciones en el manifiesto de la aplicación [de Teams](../../../../resources/schema/manifest-schema.md) que requieren la aceptación del usuario para completarse y pueden volver a desencadenar este comportamiento de consentimiento:

 >[!div class="checklist"]
>
> * Se ha agregado o quitado un bot.
> * Se cambió el valor único de un `botId` bot existente.
> * Se cambió el valor `isNotificationOnly` booleano de un bot existente.
> * Se cambió el valor `supportsFiles` booleano de un bot existente.
> * Se agregó o quitó una extensión de mensajería ( `composeExtensions` ).
> * Se ha agregado un nuevo conector.
> * Se agregó una nueva pestaña estática/personal.
> * Se agregó una nueva pestaña de grupo o canal configurable.
> * Los `webApplicationInfo` valores han cambiado.
>

### <a name="images-of-user-consent-flow"></a>Imágenes del flujo de consentimiento del usuario:

**Configurar un conector:** esta pantalla solo aparecerá para los usuarios de Teams.

![Configuración de flujo de consentimiento de un diagrama de conector](../../../../assets/images/connector-teams-consentflow.png)

**Flujo de consentimiento del** usuario: esta pantalla es común tanto para el ámbito personal como para el de grupo. Aquí, active la casilla **Consentimiento en nombre de su organización** y elija **Aceptar.**

![Diagrama de permisos](../../../../assets/images/user-consent-flow.png)

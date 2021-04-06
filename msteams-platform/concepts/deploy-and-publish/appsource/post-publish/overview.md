---
title: Mantenimiento y soporte técnico de la aplicación publicada
description: Qué hacer después de publicar la aplicación
ms.topic: how-to
keywords: manifiesto de actualización de la aplicación de certificación de actualización de publicación de teams
ms.openlocfilehash: 8644db5e329e15d77062553eda4a41a36b2740ee
ms.sourcegitcommit: e78c9f51c4538212c53bb6c6a45a09d994896f09
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/05/2021
ms.locfileid: "51585837"
---
# <a name="maintain-and-support-your-published-app"></a>Ofrecer mantenimiento y soporte técnico de su aplicación publicada 

Después de aprobar y enumerar la aplicación en el catálogo de aplicaciones públicas, puedes aumentar tu alcance completando el Programa de cumplimiento de aplicaciones de Microsoft 365 o agregando un botón de descarga en tu sitio web.

## <a name="microsoft-365-certified"></a>Certificado de Microsoft 365

El Programa de cumplimiento de aplicaciones de [Microsoft 365](./application-certification.md)es un enfoque de tres niveles para la seguridad y el cumplimiento de aplicaciones. Cada nivel se basa en el siguiente: ofrece un programa por capas para satisfacer las necesidades del cliente. Para obtener más información sobre la posición de seguridad y cumplimiento de las aplicaciones de Teams, visite la página [de cumplimiento](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps).

## <a name="add-a-download-button-to-your-product-site"></a>Agregar un botón de descarga al sitio del producto

Si la aplicación está en la tienda global de Microsoft Teams, puedes generar un vínculo para tu sitio web que inicie Teams y muestre un cuadro de diálogo de consentimiento e instalación para que los usuarios agreguen la aplicación.
El formato es:  `https://teams.microsoft.com/l/app/<appId>` donde appID es el GUID que declaran en el manifiesto enviado.
Ejemplo: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` es el vínculo para instalar Trello.

## <a name="updating-your-existing-teams-app"></a>Actualizar la aplicación de Teams existente

* No use el *botón Agregar una nueva aplicación* para volver a enviar la aplicación. Usa el icono de la aplicación en la pestaña Información general en su lugar.
* El appId en el manifiesto actualizado debe ser el mismo que en el manifiesto actual, con un número de versión incrementado.
* Incremente el número de versión en el manifiesto si realiza cambios en el envío, incluido el nombre de la aplicación o los metadatos del manifiesto.
* Los envíos actualizados son necesarios para someterse a un nuevo proceso de revisión y validación.

## <a name="app-updates-and-the-user-consent-flow"></a>Actualizaciones de aplicaciones y flujo de consentimiento del usuario

Cuando un usuario instala la aplicación, una de las primeras cosas que hace es dar permiso a la aplicación para tener acceso a los servicios e información que la aplicación necesita para realizar su trabajo. En la mayoría de los casos, después de completar una actualización de la aplicación, la nueva versión aparecerá automáticamente para los usuarios finales. Sin embargo, hay algunas actualizaciones en el manifiesto de la aplicación [de Teams](../../../../resources/schema/manifest-schema.md) que requieren la aceptación del usuario para completarse y pueden volver a desencadenar este comportamiento de consentimiento:

 >[!div class="checklist"]
>
> * Se agrega o quita un bot.
> * Se cambia el valor único de un bot `botId` existente.
> * Se cambia el valor `isNotificationOnly` booleano de un bot existente.
> * Se cambia el valor booleano o de un `supportsFiles` `supportsCalling` bot existente.
> * Se agrega o `composeExtensions` quita una extensión de mensajería.
> * Se agrega un nuevo conector.
> * Se agrega una nueva pestaña estática o personal.
> * Se agrega una nueva pestaña de canal o grupo configurable.
> * Las propiedades dentro `webApplicationInfo` se cambian. Para los cambios en `webApplicationInfo` , el consentimiento solo es necesario en el ámbito de Teams.

### <a name="images-of-user-consent-flow"></a>Imágenes del flujo de consentimiento del usuario:

**Configurar un conector:** esta pantalla solo aparecerá para los usuarios de Teams.

![Configuración del flujo de consentimiento de un diagrama de conector](../../../../assets/images/connector-teams-consentflow.png)

**Flujo de consentimiento del** usuario: esta pantalla es común para el ámbito personal y de grupo. Aquí, active la casilla **Consentimiento en nombre de su organización** y elija **Aceptar**.

![Diagrama de permisos](../../../../assets/images/user-consent-flow.png)

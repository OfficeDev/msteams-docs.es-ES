---
title: Publicación posterior
description: Qué hacer después de publicar la aplicación
keywords: certificado de actualización de publicación de publicaciones de Teams
ms.openlocfilehash: 54d0615c262e45729a36f556c3eda3b810d2a097
ms.sourcegitcommit: 2a84a3c8b10771e37ce51bf603a967633947a3e4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/10/2020
ms.locfileid: "42582863"
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


### <a name="when-does-updating-your-app-trigger-the-user-consent-flow"></a>¿Cuándo actualizar la aplicación desencadenar el flujo de consentimiento del usuario?

Cuando un usuario instala la aplicación, uno de los primeros elementos que conviene dar permiso a la aplicación para acceder a los servicios y la información que la aplicación necesita para realizar su trabajo. Al actualizar la aplicación, se puede volver a desencadenar este comportamiento de consentimiento, especialmente si ha realizado uno o varios de los siguientes cambios:

* Adición de una nueva funcionalidad a una aplicación, como agregar un bot a una aplicación de solo pestaña.
* Cambiar la matriz de permisos en el manifiesto.
* Incrementar el número de versión de la aplicación en el manifiesto.

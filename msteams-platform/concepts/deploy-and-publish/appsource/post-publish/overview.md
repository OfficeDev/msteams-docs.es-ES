---
title: Ofrecer mantenimiento y soporte técnico de su aplicación publicada
description: Qué pensar una vez que la tienda aparece en la Teams y AppSource.
ms.topic: conceptual
ms.localizationpriority: medium
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 82f85543fcf579f656704bc6c0faa47a322c2707
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157377"
---
# <a name="maintain-your-published-microsoft-teams-app"></a>Mantener la aplicación Microsoft Teams publicada

Con la aplicación incluida en la Microsoft Teams, empieza a pensar en cómo mantendrás la aplicación en el futuro y aumentarás las descargas y el uso.

## <a name="publish-updates-to-your-app"></a>Publicar actualizaciones en la aplicación

Puedes enviar cambios a la aplicación (como nuevas características o incluso metadatos) en el Centro de partners. Estos cambios requieren un nuevo proceso de revisión.

Asegúrese de lo siguiente al publicar actualizaciones:

* No cambies el identificador de la aplicación.
* Incremente el número de versión de la aplicación.
* En el Centro de partners, no seleccione **Agregar una nueva aplicación** para realizar la actualización. En su lugar, ve a la página de la aplicación.

### <a name="app-updates-requiring-user-consent"></a>Actualizaciones de aplicaciones que requieren el consentimiento del usuario

Cuando un usuario instala la aplicación, debe conceder a la aplicación permiso para tener acceso a los servicios e información que la aplicación necesita para funcionar. En la mayoría de los casos, los usuarios solo tienen que hacerlo una vez y las nuevas versiones de la aplicación se instalan automáticamente.

Sin embargo, si realizas alguno de los siguientes cambios en la aplicación, los usuarios existentes deben aceptar otra solicitud de permiso para instalar la actualización:

* Agregar o quitar un bot.
* Cambie el identificador del bot.
* Modifique la configuración de notificaciones uni-way de un bot.
* Modificar la compatibilidad de un bot para cargar y descargar archivos.
* Agregar o quitar una extensión de mensajería.
* Agregue una pestaña personal.
* Agregue una pestaña de canal y grupo.
* Agregue un conector.
* Modifique las configuraciones relacionadas con el registro Azure Active Directory aplicación (Azure AD). Para obtener más información, vea [`webApplicationInfo`](~/resources/schema/manifest-schema.md#webapplicationinfo) .

## <a name="fix-issues-with-your-published-app"></a>Corregir problemas con la aplicación publicada

Microsoft ejecuta pruebas de automatización diarias en las aplicaciones que aparecen en la Teams tienda. Si se identifican problemas con la aplicación, nos comunicaremos contigo con un informe detallado sobre cómo reproducir los problemas y recomendaciones para resolverlos. Si no puedes solucionar los problemas en una escala de tiempo indicada, es posible que la descripción de la aplicación se quite de la tienda.

## <a name="promote-your-app-on-another-site"></a>Promocionar la aplicación en otro sitio

Cuando la aplicación aparezca en la Teams, puedes crear un vínculo que inicie Teams y muestre un cuadro de diálogo para instalar la aplicación. Puede incluir este vínculo, por ejemplo, con un botón de descarga en la página de marketing del producto.

Crea el vínculo con la siguiente dirección URL anexada con el identificador de la aplicación: `https://teams.microsoft.com/l/app/<your-app-id>` .

## <a name="complete-microsoft-365-certification"></a>Certificación Microsoft 365 completa

[Microsoft 365 Certification](/microsoft-365-app-certification/docs/certification) ofrece garantías de que los datos y la privacidad están protegidos y protegidos adecuadamente cuando se instala un Aplicación de Office o complemento de terceros en su ecosistema de Microsoft 365 usuario. La certificación confirma que la aplicación es compatible con las tecnologías de Microsoft, cumple con los procedimientos recomendados de seguridad de aplicaciones en la nube y es compatible con Microsoft.

## <a name="see-also"></a>Vea también

[Monetizar su aplicación a través del Marketplace comercial de Microsoft](/office/dev/store/monetize-addins-through-microsoft-commercial-marketplace)

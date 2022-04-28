---
title: Ofrecer mantenimiento y soporte técnico de su aplicación publicada
description: Qué hay que tener en cuenta una vez que su tienda aparece en la tienda de Teams y en AppSource
ms.topic: conceptual
ms.localizationpriority: high
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 2a85739a5a94109aae87de4579f17fe99df8d28b
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104535"
---
# <a name="maintain-your-published-microsoft-teams-app"></a>Mantener la aplicación publicada de Microsoft Teams

Una vez que su aplicación aparezca en la tienda de Microsoft Teams, empiece a pensar en cómo va a mantener la aplicación en el futuro y a aumentar las descargas y el uso.

## <a name="analyze-app-usage"></a>Analizar el uso de la aplicación

Puede realizar un seguimiento del uso de la aplicación en el [ Informe de uso de la aplicación Teams](/office/dev/store/teams-apps-usage) en Centro de partners. Las métricas incluyen usuarios activos mensuales, diarios y semanales, y gráficos de retención e intensidad que permiten realizar un seguimiento del abandono y la frecuencia de uso.

Los datos de las aplicaciones recién publicadas tardan alrededor de una semana en aparecer en el informe.

## <a name="publish-updates-to-your-app"></a>Publicar actualizaciones en la aplicación

> [!NOTE]
> La tienda de Teams ha evolucionado:
>
> Anteriormente, los vínculos se copiaban seleccionando puntos suspensivos en el icono de la aplicación. Con la experiencia actualizada de la tienda de Teams, tendrá acceso a la misma desde la pestaña de detalles de las aplicaciones. Esta actualización estará disponible con carácter general (GA) antes del 1 de marzo de 2022.

Puede enviar cambios a la aplicación (como nuevas características o incluso metadatos) en Centro de partners. Estos cambios requieren un nuevo proceso de revisión.

Asegúrese de lo siguiente al publicar actualizaciones:

* No cambie el identificador de la aplicación.
* Incremente el número de versión de la aplicación.
* En Centro de partners, no seleccione **Agregar una nueva aplicación** para realizar la actualización. Vaya a la página de la aplicación en su lugar.

### <a name="app-updates-requiring-user-consent"></a>Actualizaciones de aplicaciones que requieren el consentimiento del usuario

Cuando un usuario instala la aplicación, debe conceder permiso a la aplicación para acceder a los servicios y la información que requiere la aplicación para funcionar. En la mayoría de los casos, los usuarios deben hacerlo una vez y las nuevas versiones de la aplicación se instalan automáticamente.
Sin embargo, si realiza cualquiera de los siguientes cambios en la aplicación, los usuarios existentes deben aceptar otra solicitud de permiso para instalar la actualización:

* Agregar o quitar un bot.
* Cambiar el identificador del bot.
* Modificar la configuración de notificaciones unidireccionales de un bot.
* Modificar la compatibilidad de un bot para cargar y descargar archivos.
* Agregar o quitar una extensión de mensaje.
* Agregar una pestaña personal
* Agregar un canal y una pestaña de grupo.
* Agregar un conector.
* Modificar la configuración relacionada con el registro de aplicaciones de Microsoft Azure Active Directory (Azure AD). Para más información, consulte [`webApplicationInfo`](~/resources/schema/manifest-schema.md#webapplicationinfo).

## <a name="fix-issues-with-your-published-app"></a>Corrección de problemas con la aplicación publicada

Microsoft ejecuta pruebas de automatización diarias en las aplicaciones que aparecen en la tienda de Teams. Si se identifican problemas con la aplicación, nos pondremos en contacto con usted con un informe detallado sobre cómo reproducir los problemas y recomendaciones para resolverlos. Si no puede solucionar los problemas dentro de la escala de tiempo indicada, es posible que la descripción de la aplicación se quite de la tienda.

## <a name="promote-your-app-on-another-site"></a>Promover la aplicación en otro sitio

Cuando la aplicación aparezca en la tienda de Teams, puede crear un vínculo que inicie Teams y muestre un cuadro de diálogo para instalar la aplicación. Puede incluir este vínculo, por ejemplo, con un botón de descarga en la página de marketing del producto.

Cree el vínculo con la siguiente dirección URL anexada con el identificador de la aplicación: `https://teams.microsoft.com/l/app/<your-app-id>`.

## <a name="complete-microsoft-365-certification"></a>Completar la certificación de Microsoft 365

[Certificación Microsoft 365](/microsoft-365-app-certification/docs/certification) ofrece garantías de que los datos y la privacidad se protegen adecuadamente cuando se instala una aplicación o complemento de Office de terceros en el ecosistema de Microsoft 365. La certificación confirma que la aplicación es compatible con las tecnologías de Microsoft, cumple con los procedimientos recomendados de seguridad de aplicaciones en la nube y es compatible con Microsoft.

## <a name="see-also"></a>Vea también

[Monetizar su aplicación a través del Marketplace comercial de Microsoft](/office/dev/store/monetize-addins-through-microsoft-commercial-marketplace)

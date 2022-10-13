---
title: Ofrecer mantenimiento y soporte técnico de su aplicación publicada
description: Mantenga la aplicación de Microsoft Teams publicada. Analice el uso de la aplicación, publique actualizaciones, promueva la aplicación y complete la certificación de Microsoft 365.
ms.topic: conceptual
ms.localizationpriority: high
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 77b17cb837312bca5b253fbd99fba2d0503f1744
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560473"
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
* In Partner Center, don't select **Add a new app** to do the update. Go to your app's page instead.

### <a name="app-updates-requiring-user-consent"></a>Actualizaciones de aplicaciones que requieren el consentimiento del usuario

Cuando un usuario instala la aplicación, debe conceder permiso a la aplicación para acceder a los servicios y la información que requiere la aplicación para funcionar. En la mayoría de los casos, los usuarios deben hacerlo una vez y la nueva versión de la aplicación se instala automáticamente.
Sin embargo, si realiza cualquiera de los siguientes cambios en la aplicación, los usuarios existentes deben aceptar otra solicitud de permiso para instalar la actualización:

* Agregar o quitar un bot.
* Cambiar el identificador del bot.
* Modificar la configuración de notificaciones unidireccionales de un bot.
* Modificar la compatibilidad de un bot para cargar y descargar archivos.
* Agregar o quitar una extensión de mensaje.
* Agregar una pestaña personal
* Agregar un canal y una pestaña de grupo.
* Agregar un conector.
* Modify configurations related to your Microsoft Azure Active Directory (Azure AD) app registration. For more information, see [`webApplicationInfo`](~/resources/schema/manifest-schema.md#webapplicationinfo).

## <a name="fix-issues-with-your-published-app"></a>Corrección de problemas con la aplicación publicada

Microsoft ejecuta pruebas de automatización diarias en las aplicaciones que aparecen en la tienda de Teams. Si se identifican problemas con la aplicación, nos pondremos en contacto con usted con un informe detallado sobre cómo reproducir los problemas y recomendaciones para resolverlos. Si no puede solucionar los problemas dentro de la escala de tiempo indicada, es posible que la descripción de la aplicación se quite de la tienda.

## <a name="promote-your-app-on-another-site"></a>Promover la aplicación en otro sitio

Cuando la aplicación aparezca en la tienda de Teams, puede crear un vínculo que inicie Teams y muestre un cuadro de diálogo para instalar la aplicación. Puede incluir este vínculo, por ejemplo, con un botón de descarga en la página de marketing del producto.

Cree el vínculo con la siguiente dirección URL anexada con el identificador de la aplicación: `https://teams.microsoft.com/l/app/<your-app-id>`.

## <a name="complete-microsoft-365-certification"></a>Completar la certificación de Microsoft 365

[Certificación Microsoft 365](/microsoft-365-app-certification/docs/certification) ofrece garantías de que los datos y la privacidad se protegen adecuadamente cuando se instala una aplicación o un complemento de Office de terceros en el ecosistema de Microsoft 365. La certificación confirma que la aplicación es compatible con las tecnologías de Microsoft, cumple con los procedimientos recomendados de seguridad de aplicaciones en la nube y es compatible con Microsoft.

## <a name="stop-app-distribution"></a>Detener la distribución de aplicaciones

Puede quitar una aplicación del [ Marketplace comercial de Microsoft](/azure/marketplace/overview) para evitar su descubrimiento y uso.

Para detener la distribución de una aplicación después de publicarla, siga estos pasos:

1. En la página **Información general del producto**, seleccione **Dejar de vender**. Quita la aplicación de Microsoft AppSource.
1. Para iniciar la cancelación de la lista de la aplicación, en el **Centro de partners**, seleccione la página **Información general** y, a continuación, seleccione **Dejar de vender**.

Después de detener la distribución de una aplicación, todavía puede verla en el Centro de partners con el estado **No disponible**. Si decide volver a mostrar la aplicación, siga las instrucciones para [Publicar la aplicación en la tienda de Microsoft Teams](../publish.md).

## <a name="see-also"></a>Vea también

[Monetizar su aplicación a través del Marketplace comercial de Microsoft](/office/dev/store/monetize-addins-through-microsoft-commercial-marketplace)
